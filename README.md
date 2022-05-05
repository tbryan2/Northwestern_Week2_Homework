# Northwestern_Week2_Homework
Week 2 - VBA Homework


Attached are the screenshots of the completed assignment, .bas file of the macro, and a text file of the macro.

```
Sub StockJob():

For Each ws In Worksheets

    'Worksheet name variable
    Dim Worksheet_Name As String
    Worksheet_Name = ws.Name
    
    'Determine the Last Row
    LastRow = ws.Cells(Rows.Count, 1).End(xlUp).Row

    'Row counter integer variable, = 0 to start
    Dim Row_Counter As Integer
    Row_Counter = 0

    'Stock ticker string variable
    Dim Stock_Ticker As String
    
    'First opening price as double variable
    Dim Open_Price As Double
    
    'Last closing price as double variable
    Dim Close_Price As Double
    
    'Yearly change in ticker double variable
    Dim Yearly_Change As Double
    
    'Percent change in ticker double variable
    Dim Percent_Change As Double
    
    'Total stock volume as long variable
    Dim Total_Volume As LongLong
    
    'Keep track of the location for each ticker in the summary table
    Dim Summary_Table_Row As Integer
    Summary_Table_Row = 2
    
    'Loop through to the last row
    For i = 2 To LastRow
    
    'If the next cell equals the current cell
    If ws.Cells(i + 1, 1).Value = ws.Cells(i, 1).Value Then
    
        'Count each row where the ticker is the same
        Row_Counter = Row_Counter + 1
        
        'Add to the volume total
        Total_Volume = Total_Volume + ws.Cells(i, 7).Value
        
        
    'If the cell immediately following a row is the not same ticker
    Else
    
        'Open price is the current row, minus the number of rows for that ticker
        Open_Price = ws.Cells(i - Row_Counter, 3).Value
        
        'Close price is the current row, third column
        Close_Price = ws.Cells(i, 6).Value
        
    
        'Set the stock ticker value to the current row
        Stock_Ticker = ws.Cells(i, 1).Value
        
        'Set yearly change
        Yearly_Change = Close_Price - Open_Price
        
        'Set percent change
        Percent_Change = (Close_Price - Open_Price) / Open_Price
        
        'Add to the total stock volume
        Total_Volume = Total_Volume + ws.Cells(i, 7).Value
        
        'Print the ticker to in the Summary Table J
        ws.Cells(Summary_Table_Row, 10).Value = Stock_Ticker
        
        'Print the yearly change to the summary table K
        ws.Cells(Summary_Table_Row, 11).Value = Yearly_Change
        
        'Print the percentage change to the summary table L
        ws.Cells(Summary_Table_Row, 12).Value = Percent_Change
        
        'Print the total volume to the summary table M
        ws.Cells(Summary_Table_Row, 13).Value = Total_Volume
        
        Summary_Table_Row = Summary_Table_Row + 1
        
        'Reset the variables
        Row_Counter = 0
        Open_Price = 0
        Close_Price = 0
        Yearly_Change = 0
        Percent_Change = 0
        Total_Volume = 0
        
    End If
    
Next i

'Last row dim for coloring cells
ColorLastRow = ws.Cells(Rows.Count, 11).End(xlUp).Row

'Loop through and color yearly change row according to value
For i = 2 To ColorLastRow
    
    If ws.Cells(i, 11).Value < 0 Then
        ws.Cells(i, 11).Interior.ColorIndex = 3
        
    ElseIf ws.Cells(i, 11).Value > 0 Then
        ws.Cells(i, 11).Interior.ColorIndex = 4
        
    Else
        ws.Cells(i, 11).Interior.ColorIndex = 6
    
End If

Next i

Next ws

End Sub

```

