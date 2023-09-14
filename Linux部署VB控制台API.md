
<div align='center'><font size='70'>Linux部署VB_API</font></div>

# 方案 1  ASP.NET Core

## **1. 创建一个新的 VB.NET 控制台应用程序**

ASP.NET Core 的应用程序本质上就是控制台应用程序，它们使用 Kestrel Web 服务器启动一个内置的 HTTP 服务。当你从 Visual Studio 或命令行运行一个ASP.NET Core 项目时，你实际上是在启动一个控制台应用程序。

对于.NET Core 和 .NET 5/6（即.NET的跨平台版本），你确实可以在 Linux 上部署并运行 VB.NET 控制台应用程序。但是要注意，传统的 .NET Framework（只限于 Windows）不支持在 Linux 上运行。

## **2. 安装必要的 NuGet 包**

Microsoft.AspNetCore

Microsoft.AspNetCore.Mvc

Npgsql.EntityFrameworkCore.PostgreSQL

## **3. 配置Program**

```vb
Imports Microsoft.AspNetCore.Builder
Imports Microsoft.AspNetCore.Hosting
Imports Microsoft.Extensions.DependencyInjection
Imports Microsoft.Extensions.Hosting
Imports Microsoft.EntityFrameworkCore
Imports Microsoft.Extensions.Configuration

Module Program
    Sub Main(args As String())
        ' 创建WebAPI容器
        Dim WebBuilder As WebApplicationBuilder = WebApplication.CreateBuilder(args)

        ' 注入服务
        WebBuilder.Services.AddEndpointsApiExplorer() ' 访问节点
        WebBuilder.Services.AddControllers() ' 控制器

        '' 配置 PostgreSQL 连接
        'WebBuilder.Services.AddDbContext(Of MyDbContext)(Sub(options)
        '                                                     options.UseNpgsql(WebBuilder.Configuration.GetConnectionString("DefaultConnection"))
        '                                                 End Sub)
        ' 设置端口
        If WebBuilder.Environment.IsProduction() Then
            '生产环境
            WebBuilder.WebHost.ConfigureKestrel(Function(serverOptions)
                                                    serverOptions.ListenAnyIP(8001)
                                                    Return serverOptions
                                                End Function)
        Else
            '本地环境
            WebBuilder.WebHost.ConfigureKestrel(Function(serverOptions)
                                                    serverOptions.ListenLocalhost(8001)
                                                    Return serverOptions
                                                End Function)
        End If

        ' 创建应用
        Dim WebApp As WebApplication = WebBuilder.Build()
        WebApp.UseRouting()
        WebApp.UseEndpoints(Sub(endpoints)
                                endpoints.MapControllers() ' 映射控制器
                            End Sub)

        ' 启动服务
        WebApp.Run()
    End Sub
End Module
```

## **4.配置连接池**

### **1. 安装并引入Npgsql库**

![image-20230911143510686](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20230911143510686.png)

### **2. 更改命名空间和数据访问类**:

- 更换 `System.Data.SqlClient` 为 `Npgsql` 命名空间。
- 将所有 `SqlConnection` 和 `SqlCommand` 等数据访问类更换为 `NpgsqlConnection` 和 `NpgsqlCommand`。

### **3. 调整SQL**

`部分语法不同 如 top N' ' bit和boolean等...`

### **4. 修改连接字符串**

创建 `appsettings.json ` 创建开发环境以及生产环境数据库连接池配置

```json
{
  //生产环境
  "PRODUCTION": {
    "Constr": "Host=localhost;Database=postgres;Username=postgres;Password=wpj@2023;Encoding=UTF8;"
  },
  //开发环境
  "DEVELOPMENT": {
    "Constr": "Host=localhost;Database=postgres;Username=postgres;Password=wpj@2023;Encoding=UTF8;"
  }
}
```

然后在SQLHelper.vb内配置读取json配置

```vb
    Public ConnStr As String = String.Empty

    Sub New()
        Dim builder As IConfigurationBuilder = New ConfigurationBuilder().
                                       SetBasePath(Directory.GetCurrentDirectory()).
                                       AddJsonFile("appsettings.json", False, True)
        Dim configuration As IConfiguration = builder.Build()

        If Debugger.IsAttached Then
            '开发环境
            ConnStr = configuration.GetSection("DEVELOPMENT:Constr").Value
        Else
            '生产环境
            ConnStr = configuration.GetSection("PRODUCTION:Constr").Value
        End If
    End Sub
```

## **5.配置控制器测试连接**

使用根据SQLHelper类使用自写SQL操作数据库

```vb
Imports System.Data
Imports Microsoft.AspNetCore.Mvc
Namespace Controllers
    <Route("test")>
    <ApiController>
    Public Class TestController
        Inherits ControllerBase
        Private csSqlHelper As New SQLHelper
        Private csData As New Data

        'Private ReadOnly _context As MyDbContext
        '' 在构造函数中注入 MyDbContext
        'Public Sub New(context As MyDbContext)
        '    _context = context
        'End Sub

        <HttpGet>
        Public Function GetAllUsers() As AjaxResult
            Try
                Dim strsql As String = $"SELECT * FROM T_USERMaster"
                Dim dt As DataTable = csSqlHelper.GetDataTable(strsql)
                Dim resultList As New List(Of Dictionary(Of String, Object))()

                ' 转换 DataRow 为 Dictionary
                For Each row As DataRow In dt.Rows
                    Dim dict As New Dictionary(Of String, Object)()
                    For Each col As DataColumn In dt.Columns
                        dict.Add(col.ColumnName, row(col))
                    Next
                    resultList.Add(dict)
                Next

                Return New AjaxResult("200", resultList, "")
            Catch ex As Exception
                Return New AjaxResult("500", Nothing, ex.Message)
            End Try
        End Function
    End Class

End Namespace
```

测试结果: 连接成功!

![image-20230911144249402](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20230911144249402.png)

## **6.如何部署?**

### 1. 本地发布

使用vs进行发布 编译后在发布目录可以看到.net6.0编译生成的对应文件

![image-20230911145725389](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20230911145725389.png)

### 2. 传输到CentOS 或者其他Linux主机上

使用GUI直接拖动或者scp命令传输到Linux上

```shell
scp -r /path/to/本地文件夹 user@LinuxServer:/destination/path
```

### **3. 设置权限**

```shell
chmod +x webapiname.exe
```

### 4.运行

```shell
dotnet webapiname.exe
```

尽管它是一个`.exe`文件，但你仍然可以使用`dotnet`命令运行。但是.NET Core设计为跨平台的，所以你可以在Linux上运行它，只要你已经安装了.NET Core运行时并正确设置了文件权限。

**5. 配置开机运行**

1. 使用**`systemd`** 创建服务

```shell
sudo nano /etc/systemd/system/webapi.service
```

2. 添加以下内容到服务文件中

```shell
[Unit]
Description=.NET Core Web API App

[Service]
WorkingDirectory=/path/to/your/app		 #替换成实际目录
ExecStart=/usr/bin/dotnet /path/to/your/app/webapiname.exe  #替换成实际路径
Restart=always
# Restart service after 10 seconds if the dotnet service crashes:
RestartSec=10
KillSignal=SIGINT
SyslogIdentifier=dotnet-webapiname # 替换成你的server名称
User=yourusername #替换你的用户名称
Environment=ASPNETCORE_ENVIRONMENT=Production 
Environment=DOTNET_PRINT_TELEMETRY_MESSAGE=false

[Install]
WantedBy=multi-user.target
```

3. 使服务在启动时自动启动，并立即启动它

```shell
sudo systemctl enable webapiname.service
sudo systemctl start webapiname.service
```

.NET Core应用程序应该在每次系统启动时自动运行，并且如果它崩溃，`systemd`会尝试自动重新启动它。

4. 如果你需要停止或重启你的服务，你可以使用以下命令：

```shell
sudo systemctl stop webapiname.service
sudo systemctl restart webapiname.service
```



# 方案2 容器化

postgresql可以直接使用官方镜像

![image-20230911153443642](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20230911153443642.png)

### 1.添加 Docker 支持

1. 在解决方案资源管理器中右键点击你的项目。
2. 选择“添加” -> “Docker 支持”。
3. 选择目标操作系统（通常为 Linux）。

此操作会自动生成一个 `Dockerfile`，这个文件定义了如何构建你的 Docker 映像。

### 2. 在 Visual Studio 中构建 Docker 映像

1. 在 Visual Studio 主界面的顶部，你应该会看到一个 "Docker" 选项作为启动配置。选择它。
2. 按 `F5` 或点击 "启动" 按钮。Visual Studio 会构建 Docker 映像并在容器中启动你的应用。

### 3. 将 Docker 映像推送到 Docker Hub 或其他容器注册中心

1. 如果你还没有 Docker Hub 账号，先去 [Docker Hub](https://hub.docker.com/) 注册一个。
2. 在命令行中登录 Docker Hub：`docker login`。
3. 为映像打标签：`docker tag yourimage:latest yourusername/yourimage:latest`。
4. 推送映像：`docker push yourusername/yourimage:latest`。

### 4. 在 Linux 服务器上部署容器

1. 登录到你的 Linux 服务器。
2. 确保已安装 Docker。
3. 从 Docker Hub 拉取你的映像：`docker pull yourusername/yourimage:latest`。
4. 运行容器：`docker run -d -p 8080:80 --name yourcontainername yourusername/yourimage:latest`。

此命令将容器绑定到服务器的 8080 端口。你可以根据需要更改。

# 方案3 更换语言

使用C# Java python等...重写webapi项目






