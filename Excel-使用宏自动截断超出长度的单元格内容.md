
1. 在 excel 中，按 alt + F11 调出 VBA 窗口
2. 依次点击 插入 》模块，然后粘贴以下代码到编辑窗口中
```javascript
'定义一个函数，参数为指定列的列号
Function TrimCell(col As Integer)
    '声明一个变量，用来存储当前工作表
    Dim ws As Worksheet
    '声明一个变量，用来存储当前单元格
    Dim cell As Range
    '设置当前工作表为活动工作表
    Set ws = ActiveSheet
    '遍历指定列中的所有单元格
    For Each cell In ws.Columns(col).Cells
        '判断单元格是否为空，如果为空则跳过
        If IsEmpty(cell) Then GoTo NextCell
        '判断单元格中的字符长度是否超过指定大小，如果超过则执行以下操作
        If Len(cell.Value) > 500 Then
            '将单元格中的内容截取最大限制长度，并赋值给单元格
            cell.Value = Left(cell.Value, 500)
            '在单元格后面添加省略号，表示内容被删除了一部分
            cell.Value = cell.Value & "..."
        End If
NextCell:
    Next cell
End Function
Sub xxx()
TrimCell(表格列序号)
End Sub
```
其中，TrimCell(表格列序号) 中的括号内容替换为需要处理的列的对应序号，A 对应填 1，B 对应填 2，依次类推。如：A 列，则应该为 TrimCell(1)
3. 依次点击运行 》子模块/用户窗体，等待完成即可

> 代码可稍作更改，比如限制的单元格字数（500），替换多出来的字符的省略号（"..."），等等