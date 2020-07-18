---
title: Save multiple worksheets into pdf files automatically
tags:
  - VBA
id: '1959'
date: 2019-06-02 16:32:53
---

Recently, I tried to organize a workbook with spreadsheets for my boss. I was then asked to export each sheet to an individual pdf file with the specified layout format. If I do it manually one by one, this task would be something annoying.

* * *

Steps
-----

After doing some searching, I have concluded a Macro written in VBA to this task. The steps of this Macro are introduced below:

1.  Declare variables
2.  Define a path to save all .pdf files
3.  Loop through all the worksheets
    *   Set the page setup (margin, header, footer)
    *   Export pdf file (saving file with the sheet name)
4.  Change focus to the first sheet

* * *

VBA Code
--------

The complete code is shown in the following:

Option Explicit
 
Sub SaveShtsAsBook()
    'declare variables
    Dim Sheet As Worksheet
    Dim SheetName As String
    Dim MyFilePath As String
    Dim NumSheet As Long
    
    'define a path to save all .pdf files.
    MyFilePath$ = ActiveWorkbook.Path & "\\" & Left(ThisWorkbook.Name, Len(ThisWorkbook.Name) - 4)
    
    ' operation of the application
    With Application
        
        ' stop updating screen, stop displaying alters
        .ScreenUpdating = False
        .DisplayAlerts = False

        'ignore the error and resume the execution with the next line of code
        On Error Resume Next
        'create a folder( error if the folder exists)
        MkDir MyFilePath
        
        'loop through all the worksheets
        For NumSheet = 1 To Sheets.Count
        
            Sheets(NumSheet).Activate
            ActiveWindow.View = xlPageLayoutView
            SheetName = ActiveSheet.Name
            
            ' operation of the active sheet
            With .ActiveSheet
            
                ' operation of the page setup
                With .PageSetup
                    
                    .Zoom = False
                    .FitToPagesWide = 1
                    .FitToPagesTall = False
                    
                    ' setting margin on each side
                    .LeftMargin = Application.InchesToPoints(0.5)
                    .RightMargin = Application.InchesToPoints(0.5)
                    .TopMargin = Application.InchesToPoints(0.5)
                    .BottomMargin = Application.InchesToPoints(0.5)
                    
                    ' setting margin of header, footer
                    .HeaderMargin = Application.InchesToPoints(0.2)
                    .FooterMargin = Application.InchesToPoints(0.2)
                    
                    ' print "printing date" on right side of header
                    .RightHeader = Format("Printing date: &D", "yyy/mm/dd")
                    
                    ' print "page of total pages" on right side of footer
                    .RightFooter = " page  &P of &N"
                    
                    ' anything you want to add in the footer
                    .LeftFooter = "your text"
                    .CenterFooter = "your text"
                    
                    ' chose printing paper size
                    .PaperSize = xlPaperA4
                    
                End With    'end of page setup operation
                
                
                ' exporting pdf file
                .ExportAsFixedFormat Type:=xlTypePDF, \_
                Filename:=MyFilePath & "\\" & SheetName & ".pdf", \_
                Quality:=xlQualityStandard, IncludeDocProperties:=True, \_
                IgnorePrintAreas:=False, OpenAfterPublish:=False

            End With    'end of active sheet operation
        Next    ' end of the loop
    End With    ' end of application operation
    
    'back to the first sheet
    Sheet(1).Activate
    
    MsgBox "Complete printing"
    
    'disables any error trapping
    On Error GoTo 0
    
End Sub

* * *

*   Reference:

1.  [VBA to save multiple sheets as individual PDF](https://www.mrexcel.com/forum/excel-questions/747278-vba-save-multiple-sheets-individual-pdf.html)
2.  [Excel VBA – Export Each Worksheet to a Separate PDF – Macro](http://www.chicagocomputerclasses.com/excel-vba-export-worksheet-separate-pdf-macro/)
3.  [What does the $ symbol do in VBA?](https://stackoverflow.com/questions/3389444/what-does-the-symbol-do-in-vba)
4.  [On Error Statement](https://docs.microsoft.com/zh-tw/dotnet/visual-basic/language-reference/statements/on-error-statement)