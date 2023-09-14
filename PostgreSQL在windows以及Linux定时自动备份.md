# PostgreSQL在windows以及Linux定时自动备份

## Win端

### 1. 编写脚本 `backup_postgresql ` 改后缀为 `.bat`

```shell
@echo off
set PGPASSWORD=wpj@2023 #替换数据库密码
for /f "tokens=2-4 delims=/ " %%a in ('date /t') do set year=%%c&set month=%%a&set day=%%b
"D:\PostgreSQL\14\bin\pg_dump.exe" -U postgres -h localhost -p 5432 postgres > D:\PostgreSQL\Bak\PgSql_backup_%year%%month%%day%.sql

#替换成对应的pg_dump目录  第一个postgres指用户 第二个postgres指数据库  D:\PostgreSQL\Bak 要替换成备份目录
```

### 2. 使用 Windows 计划任务来自动运行备份脚本

1. 打开 Windows 计划任务。
2. 在右侧的操作面板中，选择 "创建基本任务"。
3. 为您的任务命名并提供描述。
4. 选择触发器（例如，每天、每周或其他特定的时间间隔）。
5. 为动作选择 "启动程序"。
6. 浏览并选择您在第上一步中创建的 `backup_postgresql.bat` 文件。
7. 完成设置(不管用户是否登录都要运行)并保存。

现在，计划任务会在指定的时间间隔自动运行备份脚本，从而实现 PostgreSQL 的自动备份。

注意：请确保在生产环境中使用此方法时考虑到安全性。例如，避免在脚本中明文存储密码，并确保备份文件的存储位置安全。

## Linux端

### 1. 使用 `pg_dump` 手动备份

首先，确保您可以手动使用 `pg_dump` 进行备份。例如，备份一个名为 "mydb" 的数据库

```shell
pg_dump -U your_username -h localhost -p 5432 mydb > /path/to/backup/mydb_backup.sql
```

请替换 `your_username` 为 PostgreSQL 的用户名，并修改 `/path/to/backup/mydb_backup.sql` 为您想要的备份文件路径。

### 2. 创建备份脚本

为了简化备份过程，您可以创建一个 shell 脚本（例如，`backup_postgresql.sh`）

```shell
#!/bin/bash
export PGPASSWORD='your_password'
date=$(date +'%Y%m%d')
pg_dump -U your_username -h localhost -p 5432 mydb > /path/to/backup/mydb_backup_$date.sql
```

记得给脚本执行权限

```shell
chmod +x backup_postgresql.sh
```

### 3. 使用 `cron` 计划备份任务

1. 打开 crontab

```shell
crontab -e
```

2. 添加一个新的 cron 任务来每天自动运行备份脚本。例如，要在每天的凌晨 2 点执行脚本，您可以添加以下行

```shell
0 2 * * * /path/to/backup_postgresql.sh
```

```shell
0 0 * * 7 /path/to/backup_postgresql.sh #每周日凌晨 0 点执行备份脚本
```

- 第一个数字 `0` 表示分钟（即 0 分）。
- 第二个数字 `0` 表示小时（即 0 时，也就是凌晨）。
- `*` 表示每个月的任何一天都可以。
- `*` 表示每月。
- `7` 表示星期日。

