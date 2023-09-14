| 属性/方法名称           |              功能              |                    示例语法                    |
| :---------------------- | :----------------------------: | :--------------------------------------------: |
| AddItem()               |            增加一行            |             O.A String[, RowIndex]             |
| Aggregate               |  返回集合合计(总数,平均,等等)  |         O.A = (A,Row1,Col1,Row2,Col2)          |
| Align                   |     对象在窗体上的显示位置     |                O.A = 0;1;2;3;4                 |
| AllowBigSelection       |   设定列头是否整行或整列选择   |                   O.A = True                   |
| AllowSelection          |        是否可多单元选择        |                   O.A = True                   |
| AllowUserFreezing       |     运行时用鼠标冻结行或列     |                 O.A = 0;1;2;3                  |
| AllowUserResizing       |      调整(行/列)大小方式       |                O.A = 0;1;2;3;4                 |
| Appearance              |       边框平面/凹陷/凸起       |                  O.A = 0;1;2                   |
| Archive()               |  存储或清除一个二进制文件内容  |        O.A ArcFileName,FileName,0;1;2;3        |
| ArchiveInfo             |     返回一个二进制文件信息     |      O.A ArcFileName,0;1;2;3;4,LineIndex       |
| AutoReSize              |        是否自动调整大小        |                O.A = True;False                |
| AutoSearch              |          设置自动搜索          |                  O.A = 0;1;2                   |
| AutoSearchDelay         |    设置AutoSearch多少秒刷新    |                    O.A = 2                     |
| AutoSize()              |      自动调整列到指定宽度      |         O.A Col1,Col2,True;False,1000          |
| AutoSizeMode            |      自动调整适合行列内容      |                   O.A = 0;1                    |
| AutoSizeMouse           |  是否双击列首自动调整适合行列  |                O.A = True;False                |
| BackColor               |     所有非固定行列的背景色     |                  O.A = Color                   |
| BackColorAlternate      |   所有非固定行列的交替行颜色   |                  O.A = Color                   |
| BackColorBkg            |         表格背景坐底色         |                  O.A = Color                   |
| BackColorFixed          |       固定的行/列背景色        |                  O.A = Color                   |
| BackColorFrozen         |      冻结部分的行列背景色      |                  O.A = Color                   |
| BackColorSel            |       单元被选中的背景色       |                  O.A = Color                   |
| BindToArray()           |            绑定数组            | O.A ArrayStr,RowDim,ColDim,PageDim,CurrentPage |
| Bookmark                | 返回ADO Recordset行书签(只读)  |                    O.A(Row)                    |
| BorderStyle             |          边框粗细样式          |                   O.A = 0;1                    |
| BottomRow               |  返回可见范围的最大行号(只读)  |                      O.A                       |
| BuildComboList()        |   将数据库中的内容写入下拉框   |    O.A(rs, FieldList, KeyField, BackColor)     |
| CausesValidation        |        ???目标事件确认         |                O.A = False;True                |
| Cell                    |      选择部分的相应准则值      |   O.A(准则, Row1, Col1, Row2, Col2) = 准则值   |
| CellAlignment           |    设定单元里数据的排列方式    |                  O.A = 0 至 9                  |
| CellBackColor           |  设定单元或指定范围的背景颜色  |                  O.A = Color                   |
| CellBorder()            |     选择单元范围的边界颜色     |        O.A Color,左,上,右,下,垂直,水平         |
| CellButtonPicture       |     选择单元范围的按钮图片     |        O.A = LoadPicture(“D:\Icon.ico”)        |
| CellChecked             |      选择单元范围的复选框      |                  O.A = 0;1;2                   |
| CellFloodColor          |     选择单元范围的流程颜色     |                  O.A = Color                   |
| CellFloodPercent        |    选择单元范围的流程百分比    |                 O.A = 1 至 100                 |
| CellFontBold            |     指定单元范围设为黑体字     |                O.A = False;True                |
| CellFontItalic          |     指定单元范围设为斜体字     |                O.A = False;True                |
| CellFontName            |      对象所使用的字体名称      |                 O.A = FontName                 |
| CellFontSize            |   对象文字像数大小(默认9pt)    |                    O.A = 9                     |
| CellFontStrikethru      |      选择范围是否有删除线      |                O.A = False;True                |
| CellFontUnderline       |      选择范围是否有下画线      |                O.A = False;True                |
| CellFontWidth           |  设定单元或指定范围字体的宽度  |                    O.A = 2                     |
| CellForeColor           |  设定单元或指定范围字体的颜色  |                  O.A = Color                   |
| CellHeight              | 返回/显示到当前单元高度(只读)  |                      O.A                       |
| CellLeft                |  返回当前单元的左端位置(只读)  |                      O.A                       |
| CellPicture             |  显示在单元或指定范围中的图片  |        O.A = LoadPicture(“D:\Icon.ico”)        |
| CellPictureAlingment    |  单元或指定范围图片的显示位置  |                 O.A = 0 至 10                  |
| CellTextStyle           |     设定单元文本的显示形式     |                O.A = 0;1;2;3;4                 |
| CellTop                 |  返回当前单元的顶端位置(只读)  |                      O.A                       |
| CellWidth               |    返回当前单元的宽度(只读)    |                      O.A                       |
| Clear()                 |          清除表格内容          |             O.A([0;1;2],[0;1;2;3])             |
| ClientHeight            |      返回客户可见范围高度      |                      O.A                       |
| ClientWidth             |      返回客户可见范围宽度      |                      O.A                       |
| Clip                    |       设置选择范围的内容       |                   O.A = Text                   |
| ClipSeparators          |              ???               |                                                |
| Col                     |       设置激活单元的列号       |                    O.A = 2                     |
| ColAlignment            |         列对齐排列方式         |               O.A(Col) = 0 至 9                |
| ColComboList            |      向下拉框写入管道字符      |      O.A(Col) = “\|ListStr1\|ListStr2\|…”      |
| ColData                 |    设置用户定义的长整形数据    |              O.A(Col) = UserLong               |
| ColDataType             |           列数据类型           |   O.A(Col)=0至14到20(&H14),30(&H1E),31(&H1F)   |
| ColEditMask             |      列编辑套用格式字符串      |        O.A(Col) = 指定的格式如：######         |
| ColFormat               |          格式化显示列          |        O.A(Col) = “Currency”\|"#.###%"…        |
| ColHidden               |         是否隐藏指定列         |                O.A(Col) = True                 |
| ColImageList            |      设置图像列表句柄到列      |                                                |
| ColIndent               |           缩进指定列           |                  O.A Col= 100                  |
| ColIndex                |        返回列索引(只读)        |                    O.A Col                     |
| ColIsVisible            |      返回列是否可见(只读)      |                    O.A Col                     |
| ColKey                  |           设置列钥匙           |               O.A(Col) = KeyStr                |
| ColPos                  |     返回列距左边宽度(只读)     |                    O.A Col                     |
| ColPosition             |          移动列的位置          |                O.A(Col) = ReCol                |
| Cols                    |        返回/设置总列数         |                    O.A = 2                     |
| ColSel                  |     返回/设置最后选择的列      |                    O.A = 3                     |
| ColSort                 |           设置列种类           |               O.A(Col) = 0 至 10               |
| ColWidth                |       返回/设置指定列宽        |                 O.A(Col) = 100                 |
| ColWidthMax             |            最大列宽            |                O.A(Col) = 5000                 |
| ColWidthMin             |            最小列宽            |                 O.A(Col) = 100                 |
| ComboCount              |  取得Combo下拉按钮总数(只读)   |                      O.A                       |
| ComboData               |    Combo下拉按钮数据(只读)     |                      O.A                       |
| ComboIndex              |       Combo下拉按钮索引        |                    O.A = 1                     |
| ComboItem               |    Combo下拉按钮项目(只读)     |                      O.A                       |
| ComboList               |    向下拉框写入管道字符内容    |                O.A = “a\|b\|c”                 |
| ComboSearch             |     Combo下拉按钮搜寻方式      |                O.A = 0\|1\|2\|3                |
| Container               |      返回/设置对象的容器       |             O.A.Caption = “Forms”              |
| DataBindings            |      返回数据装入数(只读)      |                      O.A                       |
| DataMember              |     返回/设置数据描述成员      |                 O.A = DataStr                  |
| DataMode                |        设置数据链接状态        |              O.A = 0\|1\|2\|3\|4               |
| DataRefresh()           |           刷新数据源           |                      O.A                       |
| DataSource              |           设置数据源           |               Set O.A = DataDim                |
| Drag()                  |              拖放              |                 O.A [0\|1\|2]                  |
| DragIcon                |            拖放图标            |        O.A = LoadPicture(“D:\Icon.ico”)        |
| DragMode                |            拖放方式            |                    O.A = 0                     |
| DragRow()               | 拖放行(本示例在MouseDown过程)  |                  O.A O.RowSel                  |
| Editable                |     设置表格是否可编辑修改     |                 O.A = 0\|1\|2                  |
| EditCell()              |   当移动到当前单元时自动选择   |                      O.A                       |
| EditMask                |     当编辑时只能使用指定值     |                 O.A = StrValue                 |
| EditMaxLength           |      所有单元限制字节大小      |                    O.A = 2                     |
| EditSelLength           |         编辑时选择长度         |                    O.A = 5                     |
| EditSelStart            |     移动到单元时的光标位置     |           O.A = 0(或者Len(vsg.text))           |
| EditSelText             |        编辑选择处放文本        |                  O.A = “Str”                   |
| EditText                |            编辑文本            |                  O.A = “Str”                   |
| EditWindow              |       返回编辑窗口(只读)       |                      O.A                       |
| Ellipsis                |        超宽字符加省略号        |                 O.A = 0\|1\|2                  |
| Enabled                 |        对象是否激活可用        |               O.A = False\|True                |
| ExplorerBar             | 单击列头的选择、拖动或排序样式 |                 O.A = 0 至 15                  |
| ExtendLastCol           |   是否扩充最后的列到适合宽度   |               O.A = False\|True                |
| FillStyle               |  是否改变当前范围的内容或格式  |                   O.A = 0\|1                   |
| FindRow                 |   查找符和条件返回的行(只读)   |     O.A FindStr,[Row],[Col],[敏感],[精度])     |
| FinishEditing()         |           完成编辑的           |               O.A = False\|True                |
| FixedAlignment          |        固定列的对齐方式        |               O.A(Col) = 0 至 9                |
| FixedCols               |            固定几列            |                    O.A = 1                     |
| FixedRows               |            固定几行            |                    O.A = 1                     |
| FlexDataSource          |           流动数据源           |                  O.A = rsDate                  |
| FloodColor              |          设置流程颜色          |                  O.A = Color                   |
| FocusRect               |     单元的选择虚框样式类型     |             O.A = 0\|1\|2\|3\|4\|5             |
| Font                    |            设定字体            |                 O.A = FontName                 |
| FontBold                |          设定字体粗体          |               O.A = False\|True                |
| FontItalic              |          设定字体斜体          |               O.A = False\|True                |
| FontName                |          设定字体名称          |                 O.A = FontName                 |
| FontSize                |          设定字体大小          |                    O.A = 10                    |
| FontStrikethru          |         设定字体删除线         |               O.A = False\|True                |
| FontUnderline           |         设定字体下划线         |               O.A = False\|True                |
| FontWidth               |     设定字体的宽度(非间距)     |                    O.A = 2                     |
| ForeColor               |        设定字体前景颜色        |           O.A = Color *= False\|True           |
| ForeColorFixed          |     设定固定单元的文本颜色     |                  O.A = Color                   |
| ForeColorFrozen         |   设定字体冻结部分的前景颜色   |                  O.A = Color                   |
| ForeColorSel            |     设定选择单元的文本颜色     |                  O.A = Color                   |
| FormatString            |  设计管道符格式化行/列字符串   |            O.A = Format(1,"#0.00")             |
| FrozenCols              |         需要冻结的列数         |                    O.A = 2                     |
| FrozenRows              |         需要冻结的行数         |                    O.A = 2                     |
| GetMergedRange()        |        ???获得合并山脉         |                                                |
| GetNode()               |          ???获得节点           |                                                |
| GetNodeRow()            |         ???获得节点行          |                                                |
| GetSelection()          |          ???获得选择           |           O.A Row1, Col1, Row2, Col2           |
| GridColor               |      单元行列的网格线颜色      |                  O.A = Color                   |
| GridColorFixed          |      设定固定网格线的颜色      |                  O.A = Color                   |
| GridLines               |      可编辑区的网格线类型      |                 O.A = 0 至 14                  |
| GridLinesFixed          |      固定行列网格效果类型      |                 O.A = 0 至 14                  |
| GridLineWidth           |      编辑区的网格线线粗细      |                    O.A = 1                     |
| Height                  |          设置对象高度          |                   O.A = 1000                   |
| HelpContextID           |      对象缺省上下文帮助ID      |                  O.A = HelpID                  |
| HighLight               |    是否突出加亮显示选中单元    |      O.A = 0[无]\|1[默认]\|2[仅焦点时有]       |
| hWnd                    |          获取对象句柄          |                      O.A                       |
| Index                   |     对象索引号(运行时只读)     |                      O.A                       |
| IsCollapsed             |              ???               |                                                |
| IsSelected              |           是否已选择           |                      O.A                       |
| IsSubtotal              |           是否已小记           |                      O.A                       |
| Left                    |         对象距左边位置         |                   O.A = 100                    |
| LeftCol                 |      指定显示在最左边的列      |                    O.A = 1                     |
| LoadArray()             |            载入数组            |                                                |
| LoadGrid()              |            载入网格            |     O.A FileName, 0 至 6[,True(含固定行列)     |
| LoadGridURL()           |          载入网格URL           |                                                |
| MergeCells              |    相同内容的单元格合并类型    |           O.A = 0\|1\|2\|3\|4\|5\|6            |
| MergeCol 是否上下列合并 |        O.A(Col) = True         |                                                |
| MergeCompare            |     返回/设置合并比较类型      |                 O.A = 0\|1\|2                  |
| MergeRow                |         是否左右行合并         |                O.A(Row) = True                 |
| MouseCol                |     返回鼠标指向的当前列号     |                      O.A                       |
| MouseIcon               |     设定鼠标指向的当前图形     |          O.A = LoadPicture(“C:.ico”)           |
| MousePointer            |     设置对象的鼠标指针样式     |                 O.A = 0 到 15                  |
| MouseRow                |     返回鼠标指向的当前行号     |                      O.A                       |
| Move()                  |            移动对象            |        O.A Left,[Top],[Width],[Height]         |
| MultiTotals             |          ???Multi总数          |                                                |
| Name                    |      对象名称(运行时只读)      |                      O.A                       |
| NodeClosedPicture       |         节点封闭的图标         |          O.A = LoadPicture(“C:.ico”)           |
| NodeOpenPicture         |         节点打开的图标         |          O.A = LoadPicture(“C:.ico”)           |
| Object                  |      返回/设置该对象变量       |              Set DimObjName = O.A              |
| OLEDrag()               |          OLE拖拽数据           |                      O.A                       |
| OLEDragMode             |          OLE拖拽方式           |                   O.A = 0\|1                   |
| OLEDropMode             |        OLE拖拽落下方式         |                 O.A = 0\|1\|2                  |
| Outline()               |          ???外面的线           |                                                |
| OutlineBar              |   返回/设置显示目录树的线条    |                  O.A = 0 至 6                  |
| OutlineCol              |         ???外面的线列          |                                                |
| OwnerDraw               |  返回或设置执行 DrawCell 事件  |                  O.A = 0 至 6                  |
| Parent                  |   返回该对象所在的对象(只读)   |             O.A.Caption = “Forms”              |
| Picture                 |      返回控件的图片(只读)      |            O.A.属性\|方法 = 相应值             |
| PicturesOver            |        返回控件图片结束        |               O.A = False\|True                |
| PictureType             |  用Picture属性生成的图片类型   |                   O.A = 0\|1                   |
| PrintGrid()             |          打印网格数据          |  O.A [“主题”,True\|False,1\|2,左右空,上下空]   |
| Redraw                  |        设定是否刷新控件        |                 O.A = 0\|1\|2                  |
| Refresh()               |            刷新表格            |                      O.A                       |
| RemoveItem()            |           删除指定行           |                O.A VSG1.RowSel                 |
| RightCol                |    返回右边最大的可见列范围    |                      O.A                       |
| RightToLeft             |      是否将固定行放到右边      |                   O.A = True                   |
| Row                     |       设置激活单元的行号       |                    O.A = 2                     |
| RowData                 |    设置用户定义的长整形数据    |              O.A(Row) = UserLong               |
| RowHeight               |       返回/设置指定行高        |                 O.A(Row) = 100                 |
| RowHeightMax            |          行高的最大值          |                 O.A(Row) = 500                 |
| RowHeightMin            |          行高的最小值          |                 O.A(Row) = 230                 |
| RowHidden               |         是否隐藏指定行         |                 O.A(2) = True                  |
| RowIsVisible            |  返回行是否在可见范围中(只读)  |                    O.A(Row)                    |
| RowOutlineLevel         |      返回/设置水平行小记       |                O.A(Row) = 0\|1                 |
| RowPos                  |     返回行距上边高度(只读)     |                    O.A Row                     |
| RowPosition             |          移动行的位置          |               O.A(Row) = NewRow                |
| Rows                    |        返回/设置总行数         |                    O.A = 2                     |
| RowSel                  |     返回/设置最后选择的行      |                    O.A = 2                     |
| RowStatus               |           设置行状态           |                O.A = 0\|1\|2\|3                |
| SaveGrid()              |    保存网格内容到二进制文件    |     O.A FileName, 0 至 6[,True(含固定行列)     |
| ScrollBars              |       设定鼠标滚轮的方式       |                O.A = 0\|1\|2\|3                |
=======
| 属性/方法名称           |              功能              |                    示例语法                    |
| :---------------------- | :----------------------------: | :--------------------------------------------: |
| AddItem()               |            增加一行            |             O.A String[, RowIndex]             |
| Aggregate               |  返回集合合计(总数,平均,等等)  |         O.A = (A,Row1,Col1,Row2,Col2)          |
| Align                   |     对象在窗体上的显示位置     |                O.A = 0;1;2;3;4                 |
| AllowBigSelection       |   设定列头是否整行或整列选择   |                   O.A = True                   |
| AllowSelection          |        是否可多单元选择        |                   O.A = True                   |
| AllowUserFreezing       |     运行时用鼠标冻结行或列     |                 O.A = 0;1;2;3                  |
| AllowUserResizing       |      调整(行/列)大小方式       |                O.A = 0;1;2;3;4                 |
| Appearance              |       边框平面/凹陷/凸起       |                  O.A = 0;1;2                   |
| Archive()               |  存储或清除一个二进制文件内容  |        O.A ArcFileName,FileName,0;1;2;3        |
| ArchiveInfo             |     返回一个二进制文件信息     |      O.A ArcFileName,0;1;2;3;4,LineIndex       |
| AutoReSize              |        是否自动调整大小        |                O.A = True;False                |
| AutoSearch              |          设置自动搜索          |                  O.A = 0;1;2                   |
| AutoSearchDelay         |    设置AutoSearch多少秒刷新    |                    O.A = 2                     |
| AutoSize()              |      自动调整列到指定宽度      |         O.A Col1,Col2,True;False,1000          |
| AutoSizeMode            |      自动调整适合行列内容      |                   O.A = 0;1                    |
| AutoSizeMouse           |  是否双击列首自动调整适合行列  |                O.A = True;False                |
| BackColor               |     所有非固定行列的背景色     |                  O.A = Color                   |
| BackColorAlternate      |   所有非固定行列的交替行颜色   |                  O.A = Color                   |
| BackColorBkg            |         表格背景坐底色         |                  O.A = Color                   |
| BackColorFixed          |       固定的行/列背景色        |                  O.A = Color                   |
| BackColorFrozen         |      冻结部分的行列背景色      |                  O.A = Color                   |
| BackColorSel            |       单元被选中的背景色       |                  O.A = Color                   |
| BindToArray()           |            绑定数组            | O.A ArrayStr,RowDim,ColDim,PageDim,CurrentPage |
| Bookmark                | 返回ADO Recordset行书签(只读)  |                    O.A(Row)                    |
| BorderStyle             |          边框粗细样式          |                   O.A = 0;1                    |
| BottomRow               |  返回可见范围的最大行号(只读)  |                      O.A                       |
| BuildComboList()        |   将数据库中的内容写入下拉框   |    O.A(rs, FieldList, KeyField, BackColor)     |
| CausesValidation        |        ???目标事件确认         |                O.A = False;True                |
| Cell                    |      选择部分的相应准则值      |   O.A(准则, Row1, Col1, Row2, Col2) = 准则值   |
| CellAlignment           |    设定单元里数据的排列方式    |                  O.A = 0 至 9                  |
| CellBackColor           |  设定单元或指定范围的背景颜色  |                  O.A = Color                   |
| CellBorder()            |     选择单元范围的边界颜色     |        O.A Color,左,上,右,下,垂直,水平         |
| CellButtonPicture       |     选择单元范围的按钮图片     |        O.A = LoadPicture(“D:\Icon.ico”)        |
| CellChecked             |      选择单元范围的复选框      |                  O.A = 0;1;2                   |
| CellFloodColor          |     选择单元范围的流程颜色     |                  O.A = Color                   |
| CellFloodPercent        |    选择单元范围的流程百分比    |                 O.A = 1 至 100                 |
| CellFontBold            |     指定单元范围设为黑体字     |                O.A = False;True                |
| CellFontItalic          |     指定单元范围设为斜体字     |                O.A = False;True                |
| CellFontName            |      对象所使用的字体名称      |                 O.A = FontName                 |
| CellFontSize            |   对象文字像数大小(默认9pt)    |                    O.A = 9                     |
| CellFontStrikethru      |      选择范围是否有删除线      |                O.A = False;True                |
| CellFontUnderline       |      选择范围是否有下画线      |                O.A = False;True                |
| CellFontWidth           |  设定单元或指定范围字体的宽度  |                    O.A = 2                     |
| CellForeColor           |  设定单元或指定范围字体的颜色  |                  O.A = Color                   |
| CellHeight              | 返回/显示到当前单元高度(只读)  |                      O.A                       |
| CellLeft                |  返回当前单元的左端位置(只读)  |                      O.A                       |
| CellPicture             |  显示在单元或指定范围中的图片  |        O.A = LoadPicture(“D:\Icon.ico”)        |
| CellPictureAlingment    |  单元或指定范围图片的显示位置  |                 O.A = 0 至 10                  |
| CellTextStyle           |     设定单元文本的显示形式     |                O.A = 0;1;2;3;4                 |
| CellTop                 |  返回当前单元的顶端位置(只读)  |                      O.A                       |
| CellWidth               |    返回当前单元的宽度(只读)    |                      O.A                       |
| Clear()                 |          清除表格内容          |             O.A([0;1;2],[0;1;2;3])             |
| ClientHeight            |      返回客户可见范围高度      |                      O.A                       |
| ClientWidth             |      返回客户可见范围宽度      |                      O.A                       |
| Clip                    |       设置选择范围的内容       |                   O.A = Text                   |
| ClipSeparators          |              ???               |                                                |
| Col                     |       设置激活单元的列号       |                    O.A = 2                     |
| ColAlignment            |         列对齐排列方式         |               O.A(Col) = 0 至 9                |
| ColComboList            |      向下拉框写入管道字符      |      O.A(Col) = “\|ListStr1\|ListStr2\|…”      |
| ColData                 |    设置用户定义的长整形数据    |              O.A(Col) = UserLong               |
| ColDataType             |           列数据类型           |   O.A(Col)=0至14到20(&H14),30(&H1E),31(&H1F)   |
| ColEditMask             |      列编辑套用格式字符串      |        O.A(Col) = 指定的格式如：######         |
| ColFormat               |          格式化显示列          |        O.A(Col) = “Currency”\|"#.###%"…        |
| ColHidden               |         是否隐藏指定列         |                O.A(Col) = True                 |
| ColImageList            |      设置图像列表句柄到列      |                                                |
| ColIndent               |           缩进指定列           |                  O.A Col= 100                  |
| ColIndex                |        返回列索引(只读)        |                    O.A Col                     |
| ColIsVisible            |      返回列是否可见(只读)      |                    O.A Col                     |
| ColKey                  |           设置列钥匙           |               O.A(Col) = KeyStr                |
| ColPos                  |     返回列距左边宽度(只读)     |                    O.A Col                     |
| ColPosition             |          移动列的位置          |                O.A(Col) = ReCol                |
| Cols                    |        返回/设置总列数         |                    O.A = 2                     |
| ColSel                  |     返回/设置最后选择的列      |                    O.A = 3                     |
| ColSort                 |           设置列种类           |               O.A(Col) = 0 至 10               |
| ColWidth                |       返回/设置指定列宽        |                 O.A(Col) = 100                 |
| ColWidthMax             |            最大列宽            |                O.A(Col) = 5000                 |
| ColWidthMin             |            最小列宽            |                 O.A(Col) = 100                 |
| ComboCount              |  取得Combo下拉按钮总数(只读)   |                      O.A                       |
| ComboData               |    Combo下拉按钮数据(只读)     |                      O.A                       |
| ComboIndex              |       Combo下拉按钮索引        |                    O.A = 1                     |
| ComboItem               |    Combo下拉按钮项目(只读)     |                      O.A                       |
| ComboList               |    向下拉框写入管道字符内容    |                O.A = “a\|b\|c”                 |
| ComboSearch             |     Combo下拉按钮搜寻方式      |                O.A = 0\|1\|2\|3                |
| Container               |      返回/设置对象的容器       |             O.A.Caption = “Forms”              |
| DataBindings            |      返回数据装入数(只读)      |                      O.A                       |
| DataMember              |     返回/设置数据描述成员      |                 O.A = DataStr                  |
| DataMode                |        设置数据链接状态        |              O.A = 0\|1\|2\|3\|4               |
| DataRefresh()           |           刷新数据源           |                      O.A                       |
| DataSource              |           设置数据源           |               Set O.A = DataDim                |
| Drag()                  |              拖放              |                 O.A [0\|1\|2]                  |
| DragIcon                |            拖放图标            |        O.A = LoadPicture(“D:\Icon.ico”)        |
| DragMode                |            拖放方式            |                    O.A = 0                     |
| DragRow()               | 拖放行(本示例在MouseDown过程)  |                  O.A O.RowSel                  |
| Editable                |     设置表格是否可编辑修改     |                 O.A = 0\|1\|2                  |
| EditCell()              |   当移动到当前单元时自动选择   |                      O.A                       |
| EditMask                |     当编辑时只能使用指定值     |                 O.A = StrValue                 |
| EditMaxLength           |      所有单元限制字节大小      |                    O.A = 2                     |
| EditSelLength           |         编辑时选择长度         |                    O.A = 5                     |
| EditSelStart            |     移动到单元时的光标位置     |           O.A = 0(或者Len(vsg.text))           |
| EditSelText             |        编辑选择处放文本        |                  O.A = “Str”                   |
| EditText                |            编辑文本            |                  O.A = “Str”                   |
| EditWindow              |       返回编辑窗口(只读)       |                      O.A                       |
| Ellipsis                |        超宽字符加省略号        |                 O.A = 0\|1\|2                  |
| Enabled                 |        对象是否激活可用        |               O.A = False\|True                |
| ExplorerBar             | 单击列头的选择、拖动或排序样式 |                 O.A = 0 至 15                  |
| ExtendLastCol           |   是否扩充最后的列到适合宽度   |               O.A = False\|True                |
| FillStyle               |  是否改变当前范围的内容或格式  |                   O.A = 0\|1                   |
| FindRow                 |   查找符和条件返回的行(只读)   |     O.A FindStr,[Row],[Col],[敏感],[精度])     |
| FinishEditing()         |           完成编辑的           |               O.A = False\|True                |
| FixedAlignment          |        固定列的对齐方式        |               O.A(Col) = 0 至 9                |
| FixedCols               |            固定几列            |                    O.A = 1                     |
| FixedRows               |            固定几行            |                    O.A = 1                     |
| FlexDataSource          |           流动数据源           |                  O.A = rsDate                  |
| FloodColor              |          设置流程颜色          |                  O.A = Color                   |
| FocusRect               |     单元的选择虚框样式类型     |             O.A = 0\|1\|2\|3\|4\|5             |
| Font                    |            设定字体            |                 O.A = FontName                 |
| FontBold                |          设定字体粗体          |               O.A = False\|True                |
| FontItalic              |          设定字体斜体          |               O.A = False\|True                |
| FontName                |          设定字体名称          |                 O.A = FontName                 |
| FontSize                |          设定字体大小          |                    O.A = 10                    |
| FontStrikethru          |         设定字体删除线         |               O.A = False\|True                |
| FontUnderline           |         设定字体下划线         |               O.A = False\|True                |
| FontWidth               |     设定字体的宽度(非间距)     |                    O.A = 2                     |
| ForeColor               |        设定字体前景颜色        |           O.A = Color *= False\|True           |
| ForeColorFixed          |     设定固定单元的文本颜色     |                  O.A = Color                   |
| ForeColorFrozen         |   设定字体冻结部分的前景颜色   |                  O.A = Color                   |
| ForeColorSel            |     设定选择单元的文本颜色     |                  O.A = Color                   |
| FormatString            |  设计管道符格式化行/列字符串   |            O.A = Format(1,"#0.00")             |
| FrozenCols              |         需要冻结的列数         |                    O.A = 2                     |
| FrozenRows              |         需要冻结的行数         |                    O.A = 2                     |
| GetMergedRange()        |        ???获得合并山脉         |                                                |
| GetNode()               |          ???获得节点           |                                                |
| GetNodeRow()            |         ???获得节点行          |                                                |
| GetSelection()          |          ???获得选择           |           O.A Row1, Col1, Row2, Col2           |
| GridColor               |      单元行列的网格线颜色      |                  O.A = Color                   |
| GridColorFixed          |      设定固定网格线的颜色      |                  O.A = Color                   |
| GridLines               |      可编辑区的网格线类型      |                 O.A = 0 至 14                  |
| GridLinesFixed          |      固定行列网格效果类型      |                 O.A = 0 至 14                  |
| GridLineWidth           |      编辑区的网格线线粗细      |                    O.A = 1                     |
| Height                  |          设置对象高度          |                   O.A = 1000                   |
| HelpContextID           |      对象缺省上下文帮助ID      |                  O.A = HelpID                  |
| HighLight               |    是否突出加亮显示选中单元    |      O.A = 0[无]\|1[默认]\|2[仅焦点时有]       |
| hWnd                    |          获取对象句柄          |                      O.A                       |
| Index                   |     对象索引号(运行时只读)     |                      O.A                       |
| IsCollapsed             |              ???               |                                                |
| IsSelected              |           是否已选择           |                      O.A                       |
| IsSubtotal              |           是否已小记           |                      O.A                       |
| Left                    |         对象距左边位置         |                   O.A = 100                    |
| LeftCol                 |      指定显示在最左边的列      |                    O.A = 1                     |
| LoadArray()             |            载入数组            |                                                |
| LoadGrid()              |            载入网格            |     O.A FileName, 0 至 6[,True(含固定行列)     |
| LoadGridURL()           |          载入网格URL           |                                                |
| MergeCells              |    相同内容的单元格合并类型    |           O.A = 0\|1\|2\|3\|4\|5\|6            |
| MergeCol 是否上下列合并 |        O.A(Col) = True         |                                                |
| MergeCompare            |     返回/设置合并比较类型      |                 O.A = 0\|1\|2                  |
| MergeRow                |         是否左右行合并         |                O.A(Row) = True                 |
| MouseCol                |     返回鼠标指向的当前列号     |                      O.A                       |
| MouseIcon               |     设定鼠标指向的当前图形     |          O.A = LoadPicture(“C:.ico”)           |
| MousePointer            |     设置对象的鼠标指针样式     |                 O.A = 0 到 15                  |
| MouseRow                |     返回鼠标指向的当前行号     |                      O.A                       |
| Move()                  |            移动对象            |        O.A Left,[Top],[Width],[Height]         |
| MultiTotals             |          ???Multi总数          |                                                |
| Name                    |      对象名称(运行时只读)      |                      O.A                       |
| NodeClosedPicture       |         节点封闭的图标         |          O.A = LoadPicture(“C:.ico”)           |
| NodeOpenPicture         |         节点打开的图标         |          O.A = LoadPicture(“C:.ico”)           |
| Object                  |      返回/设置该对象变量       |              Set DimObjName = O.A              |
| OLEDrag()               |          OLE拖拽数据           |                      O.A                       |
| OLEDragMode             |          OLE拖拽方式           |                   O.A = 0\|1                   |
| OLEDropMode             |        OLE拖拽落下方式         |                 O.A = 0\|1\|2                  |
| Outline()               |          ???外面的线           |                                                |
| OutlineBar              |   返回/设置显示目录树的线条    |                  O.A = 0 至 6                  |
| OutlineCol              |         ???外面的线列          |                                                |
| OwnerDraw               |  返回或设置执行 DrawCell 事件  |                  O.A = 0 至 6                  |
| Parent                  |   返回该对象所在的对象(只读)   |             O.A.Caption = “Forms”              |
| Picture                 |      返回控件的图片(只读)      |            O.A.属性\|方法 = 相应值             |
| PicturesOver            |        返回控件图片结束        |               O.A = False\|True                |
| PictureType             |  用Picture属性生成的图片类型   |                   O.A = 0\|1                   |
| PrintGrid()             |          打印网格数据          |  O.A [“主题”,True\|False,1\|2,左右空,上下空]   |
| Redraw                  |        设定是否刷新控件        |                 O.A = 0\|1\|2                  |
| Refresh()               |            刷新表格            |                      O.A                       |
| RemoveItem()            |           删除指定行           |                O.A VSG1.RowSel                 |
| RightCol                |    返回右边最大的可见列范围    |                      O.A                       |
| RightToLeft             |      是否将固定行放到右边      |                   O.A = True                   |
| Row                     |       设置激活单元的行号       |                    O.A = 2                     |
| RowData                 |    设置用户定义的长整形数据    |              O.A(Row) = UserLong               |
| RowHeight               |       返回/设置指定行高        |                 O.A(Row) = 100                 |
| RowHeightMax            |          行高的最大值          |                 O.A(Row) = 500                 |
| RowHeightMin            |          行高的最小值          |                 O.A(Row) = 230                 |
| RowHidden               |         是否隐藏指定行         |                 O.A(2) = True                  |
| RowIsVisible            |  返回行是否在可见范围中(只读)  |                    O.A(Row)                    |
| RowOutlineLevel         |      返回/设置水平行小记       |                O.A(Row) = 0\|1                 |
| RowPos                  |     返回行距上边高度(只读)     |                    O.A Row                     |
| RowPosition             |          移动行的位置          |               O.A(Row) = NewRow                |
| Rows                    |        返回/设置总行数         |                    O.A = 2                     |
| RowSel                  |     返回/设置最后选择的行      |                    O.A = 2                     |
| RowStatus               |           设置行状态           |                O.A = 0\|1\|2\|3                |
| SaveGrid()              |    保存网格内容到二进制文件    |     O.A FileName, 0 至 6[,True(含固定行列)     |
| ScrollBars              |       设定鼠标滚轮的方式       |                O.A = 0\|1\|2\|3                |