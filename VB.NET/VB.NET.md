## vb.net窗体关闭的问题！

Private Sub frmNotepad_Closing(ByVal sender As Object, ByVal e As System.ComponentModel.CancelEventArgs) Handles MyBase.Closing

​        Call subexit()

​        End

​    End Sub

Sub subexit()

​        Dim frmNew As frmNotepad

​        frmNew = ActiveForm

​        If frmNew.Text = "未定标题 - 记事本" Then

​            If frmNew.rtb.Text = "" Then

​            Else

​                Dim result As New MsgBoxResult           'result提示对话框yes,no,cancel

​                result = MsgBox("未定标题 文件的文字已经改变。"  Chr(10)  Chr(10)   "想保存文件吗？", MsgBoxStyle.YesNoCancel + MsgBoxStyle.Exclamation, "记事本")

​                If result = MsgBoxResult.Yes Then       'result.Yes表示保存，清空内容，打开新页面

​                    Dim fileSave As New SaveFileDialog

​                    Dim re As New DialogResult          're提示对话框OK，cancel

​                    fileSave.FileName = "*.txt"

​                    fileSave.Filter = "文本文档(*.txt)|*.txt|所有文件|*.*"

​                    re = fileSave.ShowDialog()

​                    If re = DialogResult.OK Then                're.OK表示成功保存，清空内容，打开新页面

​                        filename = fileSave.FileName

​                        Dim fstream As FileStream

​                        Dim sw As StreamWriter

​                        Try

​                            'frmNew.Text = filename.Substring(filename.LastIndexOf("\") + 1)  "- 记事本"

​                            fstream = New FileStream(filename, FileMode.Create, FileAccess.ReadWrite)

​                            sw = New StreamWriter(fstream, System.Text.Encoding.Default)

​                            sw.BaseStream.Seek(0, SeekOrigin.End)

​                            sw.Write(rtb.Text)

​                            sw.Flush()

​                        Catch ex As Exception

​                            MsgBox("保存文件失败")

​                        Finally

​                            sw.Close()

​                        End Try

​                    ElseIf re = DialogResult.Cancel Then        're.cancel表示不保存，不改变任何结果

​                    End If

​                ElseIf result = MsgBoxResult.No Then            'result.no表示不保存，清空内容

​                    rtb.Text = ""

​                End If

End If

​        Else

​            If rtb.Text.Compare(rtb.Text, compareStr)  0 Then

​                Dim result As New MsgBoxResult

​                result = MsgBox(filename + " 文件的文字已经改变。"  Chr(10)   Chr(10)  "想保存文件吗？", MsgBoxStyle.YesNoCancel + MsgBoxStyle.Exclamation,  "记事本")

​                If result = MsgBoxResult.Yes Then

​                    Dim fstream As FileStream

​                    Dim sw As StreamWriter

​                    Try

​                        'frmNew.Text = filename.Substring(filename.LastIndexOf("\") + 1)  "- 记事本"

​                        fstream = New FileStream(filename, FileMode.Create, FileAccess.ReadWrite)

​                        sw = New StreamWriter(fstream, System.Text.Encoding.Default)

​                        sw.BaseStream.Seek(0, SeekOrigin.End)

​                        sw.Write(rtb.Text)

​                        sw.Flush()

​                    Catch ex As Exception

​                        MsgBox("保存文件失败")

​                    Finally

​                        sw.Close()

​                    End Try

ElseIf result = MsgBoxResult.No Then

​                    rtb.Text = ""

​                End If

​            End If

End If

​    End Sub



### 全局热键

Public Class Form1

  Public Const WM_HOTKEY = &H312
  Public Const MOD_ALT = &H1
  Public Const MOD_CONTROL = &H2
  Public Const MOD_SHIFT = &H4
  Public Const GWL_WNDPROC = (-4)

 

  Public Declare Auto Function RegisterHotKey Lib "user32.dll" Alias _
    "RegisterHotKey" (ByVal hwnd As IntPtr, ByVal id As Integer, ByVal fsModifiers As  Integer, ByVal vk As Integer) As Boolean


  Public Declare Auto Function UnRegisterHotKey Lib "user32.dll" Alias _
    "UnregisterHotKey" (ByVal hwnd As IntPtr, ByVal id As Integer) As Boolean

 

  Private Sub Form1_Load(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles MyBase.Load
    '注册全局热键
    RegisterHotKey(Handle, 0, MOD_CONTROL, Asc("T")) '第一个热键 Ctrl+T
    RegisterHotKey(Handle, 1, Nothing, Keys.F4) '第二个热键 F4
  End Sub

 

  Private Sub  Form1_FormClosed(ByVal sender As System.Object, ByVal e As  System.Windows.Forms.FormClosedEventArgs) Handles MyBase.FormClosed
    '注销全局热键
    UnRegisterHotKey(Handle, 0)
    UnRegisterHotKey(Handle, 1)
  End Sub

 

  Protected Overrides Sub WndProc(ByRef m As Message)
    If m.Msg = WM_HOTKEY Then
      MsgBox("在这里添加你要执行的代码", MsgBoxStyle.Information, "全局热键")
    End If
    MyBase.WndProc(m)
  End Sub
End Class





## 局部快捷键

Private Sub Frm_KeyDown(sender As Object, e As KeyEventArgs) Handles Me.KeyDown
        If e.KeyData = (Keys.Control Or Keys.F) Then
            'csControl_Search.Tool_Btn_Find(Me, csXarrayDB, Me.Name, m_strEditStaffCode)

​        End If
​    End Sub

## vb.net编写的程序屏蔽系统热键

使用VB.net编写屏蔽热键的方法有很多中,比如说使用系统的API函数,也可以使用钩子来进行屏蔽.还有一种就是.net带的一种方法,首先来判断所按下去的键,然后再执行操作等事件.比如说:

if (e.keycode==keys.D){e.handle=true}

在keydown事件里面处理!这样就可以屏蔽了D键. 实例:

if  ((Control.ModifierKeys == Keys.Alt)  (e.KeyCode == Keys.F4)){e.Handled = true;}

还有一种办法就是不通过屏蔽热键来实现,就是通过设置焦点.你可以把你程序窗口设置为主焦点,这样其他程序一般就无法在你的程序前面了.实现屏蔽的作用.至于任务管理器的话可以通过杀掉进程的办法做到.如下:   

Process[] p = Process.GetProcesses();

foreach (Process p1  in p){

try{if (p1.ProcessName.ToLower().Trim() == "taskmgr")//这里判断是任务管理器   

{

 p1.Kill();

 return;

 }

 }

 catch{

return;

}

=======


## vb.net中怎么写窗体form关闭的事件?

一般来说都是this.close(); 方法调用一下就可以了。

这像是以前 VB 的写法，VB.net 里不是这样的，应该是：

```vb
Private Sub Form_Closed(ByVal sender As Object, ByVal e As System.EventArgs) Handles MyBase.Closed
MagBox("1111")
End Sub '注意，... Handles MyBase.Closed 是在同一行里的。
```

## VB.NET的窗体的所有事件

|                      名称                      |                             说明                             |
| :--------------------------------------------: | :----------------------------------------------------------: |
|                 Activated激活                  |             当使用代码激活或用户激活窗体时发生。             |
|       AutoSizeChanged自动调整大小已更改        |                 当 AutoSize 属性更改时发生。                 |
|       AutoValidateChanged自动验证已更改        |               当 AutoValidate 属性更改时发生。               |
|         BackColorChanged背面颜色已更改         |    当 BackColor 属性的值更改时发生。（从 Control 继承。）    |
|      BackgroundImageChanged背景图像已更改      | 当 BackgroundImage 属性的值更改时发生。（从 Control 继承。） |
| BackgroundImageLayoutChanged背景图像布局已更改 | 当 BackgroundImageLayout 属性更改时发生。（从 Control 继承。） |
|     BindingContextChanged绑定上下文已更改      | 当 BindingContext 属性的值更改时发生。（从 Control 继承。）  |
|     CausesValidationChanged原因验证已更改      | 当 CausesValidation 属性的值更改时发生。（从 Control 继承。） |
|            ChangeUICues更改用户界面            | 焦点或键盘用户界面 (UI) 提示更改时发生。（从 Control 继承。） |
|                   Click点击                    |           在单击控件时发生。（从 Control 继承。）            |
|       ClientSizeChanged客户端大小已更改        |   当 ClientSize 属性的值更改时发生。（从 Control 继承。）    |
|                    Closed闭                    |                       关闭窗体时发生。                       |
|                  Closing关闭                   |                       关闭窗体时发生。                       |
|       ContextMenuChanged上下文菜单已更改       |   当 ContextMenu 属性的值更改时发生。（从 Control 继承。）   |
|   ContextMenuStripChanged上下文菜单条已更改    | 当 ContextMenuStrip 属性的值更改时发生。（从 Control 继承。） |
|             ControlAdded控件已添加             | 在将新控件添加到 Control.ControlCollection 时发生。（从 Control 继承。） |
|            ControlRemoved控件已删除            | 在从 Control.ControlCollection 移除控件时发生。（从 Control 继承。） |
|            CursorChanged光标已更改             |     当 Cursor 属性的值更改时发生。（从 Control 继承。）      |
|                 Deactivate关闭                 |            当窗体失去焦点并不再是活动窗体时发生。            |
|                  Disposed处置                  | 当通过调用 Dispose 方法释放组件时发生。（从 Component 继承。） |
|             DockChanged坞站已更改              |      当 Dock 属性的值更改时发生。（从 Control 继承。）       |
|                DoubleClick双击                 |           在双击控件时发生。（从 Control 继承。）            |
|                  DragDrop拖放                  |          拖放操作完成时发生。（从 Control 继承。）           |
|               DragEnter拖动输入                |     在将对象拖入控件的边界时发生。（从 Control 继承。）      |
|               DragLeave拖拽离开                |      将对象拖出控件的边界时发生。（从 Control 继承。）       |
|                  DragOver拖拽                  |     在将对象拖到控件的边界上发生。（从 Control 继承。）      |
|           EnabledChanged已启用已更改           |      在 Enabled 属性值更改后发生。（从 Control 继承。）      |
|                   Enter进入                    |            进入控件时发生。（从 Control 继承。）             |
|             FontChanged字体已更改              |       在 Font 属性值更改时发生。（从 Control 继承。）        |
|           ForeColorChanged前色已更改           |     在 ForeColor 属性值更改时发生。（从 Control 继承。）     |
|              FormClosed表单已关闭              |                       关闭窗体后发生。                       |
|              FormClosing表单关闭               |                       关闭窗体前发生。                       |
|              GiveFeedback给予反馈              |        在执行拖动操作期间发生。（从 Control 继承。）         |
|                GotFocus得到焦点                |         在控件接收焦点时发生。（从 Control 继承。）          |
|             HandleCreated句柄创建              |        在为控件创建句柄时发生。（从 Control 继承。）         |
|           HandleDestroyed句柄已销毁            |   在控件的句柄处于销毁过程中时发生。（从 Control 继承。）    |
|        HelpButtonClicked帮助按钮已点击         |                    单击“帮助”按钮时发生。                    |
|           HelpRequested已请求的帮助            |        用户请求控件帮助时发生。（从 Control 继承。）         |
|          ImeModeChanged图像模式已更改          |       在 ImeMode 属性更改后发生。（从 Control 继承。）       |
|       InputLanguageChanged输入语言已更改       |                  更改窗体的输入语言后发生。                  |
|       InputLanguageChanging输入语言更改        |             当用户尝试更改窗体的输入语言时发生。             |
|                Invalidated失效                 |     控件的显示要求重新绘制时发生。（从 Control 继承。）      |
|                 KeyDown键向下                  |   在控件有焦点的情况下按下键时发生。（从 Control 继承。）    |
|                  KeyPress按键                  | 在控件有焦点的情况下字符、空格或退格键时发生。（从 Control 继承。） |
|                   KeyUp键控                    |   在控件有焦点的情况下释放键时发生。（从 Control 继承。）    |
|                   Layout布局                   |    在控件应重新定位其子控件时发生。（从 Control 继承。）     |
|                   Leave离开                    |       在输入焦点离开控件时发生。（从 Control 继承。）        |
|                    Load负荷                    |                   在第一次显示窗体前发生。                   |
|           LocationChanged位置已更改            |     在 Location 属性值更改后发生。（从 Control 继承。）      |
|                 LostFocus失焦                  |         在控件失去焦点时发生。（从 Control 继承。）          |
|            MarginChanged边距已更改             |                  当 Margin 属性更改时发生。                  |
|     MaximizedBoundsChanged最大化边界已更改     |           在 MaximizedBounds 属性的值更改后发生。            |
|        MaximumSizeChanged最大大小已更改        |             在 MaximumSize 属性的值更改后发生。              |
|        MdiChildActivateMdiChildActivate        |  在多文档界面 (MDI) 应用程序内激活或关闭 MDI 子窗体时发生。  |
|              MenuComplete菜单完成              |                  当窗体菜单失去焦点时发生。                  |
|               MenuStart菜单开始                |                  当窗体菜单接收焦点时发生。                  |
|        MinimumSizeChanged最小大小已更改        |             在 MinimumSize 属性的值更改后发生。              |
|       MouseCaptureChanged鼠标捕获已更改        |       当控件失去鼠标捕获时发生。（从 Control 继承。）        |
|               MouseClick鼠标点击               |         用鼠标单击控件时发生。（从 Control 继承。）          |
|            MouseDoubleClick鼠标双击            |         用鼠标双击控件时发生。（从 Control 继承。）          |
|               MouseDown鼠标向下                | 当鼠标指针位于控件上并按下鼠标键时发生。（从 Control 继承。） |
|               MouseEnter鼠标输入               |       在鼠标指针进入控件时发生。（从 Control 继承。）        |
|               MouseHover鼠标悬停               |     在鼠标指针停放在控件上时发生。（从 Control 继承。）      |
|               MouseLeave鼠标离开               |       在鼠标指针离开控件时发生。（从 Control 继承。）        |
|               MouseMove鼠标移动                |      在鼠标指针移到控件上时发生。（从 Control 继承。）       |
|                MouseUp鼠标向上                 | 在鼠标指针在控件上并释放鼠标键时发生。（从 Control 继承。）  |
|               MouseWheel鼠标滚轮               |    在控件有焦点且鼠标轮移动时发生。（从 Control 继承。）     |
|                    Move移动                    |           在移动控件时发生。（从 Control 继承。）            |
|            PaddingChanged填充已更改            |        在控件空白区更改时发生。（从 Control 继承。）         |
|                    Paint漆                     |           在重绘控件时发生。（从 Control 继承。）            |
|               ParentChanged父改                |      在 Parent 属性值更改时发生。（从 Control 继承。）       |
|            PreviewKeyDown预览键向下            | 在焦点位于此控件上的情况下，当有按键动作时发生（在 KeyDown 事件之前发生）。（从Control 继承。） |
|     QueryAccessibilityHelp查询辅助功能帮助     | 在 AccessibleObject 为辅助功能应用程序提供帮助时发生。（从 Control 继承。） |
|         QueryContinueDrag查询继续拖动          | 在拖放操作期间发生，并且允许拖动源确定是否应取消拖放操作。（从 Control 继承。） |
|            RegionChanged区域已更改             |     当 Region 属性的值更改时发生。（从 Control 继承。）      |
|                   Resize调整                   |         在调整控件大小时发生。（从 Control 继承。）          |
|            ResizeBegin调整大小开始             |                 窗体进入大小调整模式时发生。                 |
|             ResizeEnd调整大小结束              |                 窗体退出大小调整模式时发生。                 |
|         RightToLeftChanged从右到左更改         |    在 RightToLeft 属性值更改时发生。（从 Control 继承。）    |
|   RightToLeftLayoutChanged从右到左布局已更改   |           更改 RightToLeftLayout 属性值之后发生。            |
|                   Scroll滚动                   |                 用户或代码滚动工作区时发生。                 |
|             SizeChanged大小已更改              |       在 Size 属性值更改时发生。（从 Control 继承。）        |
|             StyleChanged风格已更改             |                    当窗体样式更改时发生。                    |
|       SystemColorsChanged系统颜色已更改        |                     显示设置更改时发生。                     |
|        TabIndexChanged选项卡索引已更改         |     当 TabIndex 属性值更改时发生。（从 Control 继承。）      |
|          TabStopChangedTabStopChanged          |      当 TabStop 属性值更改时发生。（从 Control 继承。）      |
|             TextChanged文本已更改              |       在 Text 属性值更改时发生。（从 Control 继承。）        |
|                 Validated验证                  |        在验证控件的内容时发生。（从 Control 继承。）         |
|                 Validating验证                 |           在验证控件时发生。（从 Control 继承。）            |
|            VisibleChanged可见已更改            |      在 Visible 属性值更改时发生。（从 Control 继承。）      |
|                 VScrollVScroll                 |        在垂直滚动条滚动时发生。（从 Control 继承。）         |

## vb命令按钮退出怎么设置？

在退出按钮的Click事件中用Unload Me就可以关闭窗体。

```vb
Private Sub Command1_Click()
Unload Me
End Sub
```

答案补充 :

代码就是我回答那些了，双击按钮把代码输入进去就行了。对了，你的是VB6还是VB.Net啊？VB6就是用Unload Me，如果是VB.Net应该用Me.Close()。

```vb
'这个是VB.Net的代码：

Private Sub Button1_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Button2.Click
Me.Close()
End Sub
```

## VB.NET窗体关闭事件

直接上代码

```vb
Private Sub Form1_FormClosing(ByVal sender As System.Object, ByVal e As System.Windows.Forms.FormClosingEventArgs) 
MsgBox("窗口即将关闭....") 
End Sub
Else 
  e.Cancel = True 
End If
```

## 窗体的退出事件 vb.net

既然是VB.NET，那么，窗体关闭的事件，是.net framework提供的，是FormClosed事件。也是两个参数，一个object sender这个是object基类，整个.net framework都是从它派生的，一个 EventArgs  e，事件处理基类，一切事件是从EventArgs基类派生出来的。

