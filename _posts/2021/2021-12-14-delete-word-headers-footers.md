---
title: "批量删除 Word 文档页眉与页脚"
categories:
  - tutorial
tags:
  - 教程
  - 分享
toc: false
toc_sticky: true
toc_label: ""
toc_icon: ""  # Font Awesome对应图标名称 (无fa前缀)	
---
很多时候，从网上下载下来的文档会带有页眉和页脚，如果只是删除一个文件的页眉和页脚很简单，只需要双击页眉或者页脚选中，再点击 `DELETE` 键删除即可.

但是大量的文档，要删除页眉页脚，一个个操作起来工作量就很大了，这时候可以借助办公软件的 **宏** 来批量、自动删除页眉页脚。

这里以 WPS 为例演示怎样创建并使用 **宏**。

## 创建宏
首先在工具栏选择 **开发工具**，点击 **宏**，填写宏名称后点击 **创建**。

[![20211214175153](https://cdn.jsdelivr.net/gh/sunete/imghost/img20211214175153.png)](https://cdn.jsdelivr.net/gh/sunete/imghost/img20211214175153.png)

在新窗口中粘贴以下代码并保存。

注意：保存时文件类型需要选择 `*.docm`。

```
Sub 批量删除页眉页脚()
'此代码功能为列出指定文件夹中所有选取的WORD文件全路径名
Dim myDialog As FileDialog, oDoc As Document, oSec As Section
Dim oFile As Variant, myRange As Range
On Error Resume Next
'定义一个文件夹选取对话框
Set myDialog = Application.FileDialog(msoFileDialogFilePicker)
With myDialog
.Filters.Clear '清除所有文件筛选器中的项目
.Filters.Add "所有Word文件", "*.doc,*.docx", 1 '增加筛选器的项目为所有Word文件
.AllowMultiSelect = True '允许多项选择
If .Show = -1 Then '确定
For Each oFile In .SelectedItems '在所有选取项目中循环
Set oDoc = Word.Documents.Open(FileName:=oFile, Visible:=False)
For Each oSec In oDoc.Sections '文档的节中循环
Set myRange = oSec.Headers(wdHeaderFooterPrimary).Range
myRange.Delete '删除页眉中的内容
myRange.ParagraphFormat.Borders(wdBorderBottom).LineStyle = wdLineStyleNone '段落下边框线
Set myRange = oSec.Footers(wdHeaderFooterPrimary).Range
myRange.Delete '删除页脚中的内容
Next
oDoc.Close True
Next
End If
End With
End Sub
```

## 使用宏
双击打开刚才保存的后缀为 `*.docm` 的宏文件。工具栏选择 **开发工具** 点击 **宏** ，就会出现以下界面。

[![20211214182753](https://cdn.jsdelivr.net/gh/sunete/imghost/img20211214182753.png)](https://cdn.jsdelivr.net/gh/sunete/imghost/img20211214182753.png)

点击 **运行**，选择需要删除页眉页脚的文件（可选择多个文件），点击 **打开** 就会自动删除所有选中文档的页眉和页脚。