---
title: 通过查询结果分页
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: fa360c46-e5f8-411e-a711-46997771133d
ms.openlocfilehash: 73475f8521b4112929339cc7f1116e36ffebedb7
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="paging-through-a-query-result"></a>通过查询结果分页
查询结果分页是以较小数据子集（即页）的形式返回查询结果的过程。 它通常用于以易于管理的小块形式向用户显示结果。  
  
 **DataAdapter**为仅返回一页的数据，通过重载提供工具**填充**方法。 但是，这可能不是最适合进行大型查询结果分页，因为，虽然**DataAdapter**填充目标<xref:System.Data.DataTable>或<xref:System.Data.DataSet>仅的请求记录，若要返回的资源仍然用于将整个查询。 若要在从数据源中返回一页数据时不使用返回整个查询的资源，请为查询指定附加条件，使返回的行数减少到只返回所需的行。  
  
 若要使用**填充**方法以返回一页数据，指定**startRecord**参数，第一条记录的页中的数据，和一个**maxRecords**参数的数目中的数据页的记录。  
  
 下面的代码示例演示如何使用**填充**方法以返回查询结果的第一页的页大小为 5 个记录的位置。  
  
```vb  
Dim currentIndex As Integer = 0  
Dim pageSize As Integer = 5  
  
Dim orderSQL As String = "SELECT * FROM dbo.Orders ORDER BY OrderID"  
' Assumes that connection is a valid SqlConnection object.  
Dim adapter As SqlDataAdapter = _  
  New SqlDataAdapter(orderSQL, connection)  
  
Dim dataSet As DataSet = New DataSet()  
adapter.Fill(dataSet, currentIndex, pageSize, "Orders")  
```  
  
```csharp  
int currentIndex = 0;  
int pageSize = 5;  
  
string orderSQL = "SELECT * FROM Orders ORDER BY OrderID";  
// Assumes that connection is a valid SqlConnection object.  
SqlDataAdapter adapter = new SqlDataAdapter(orderSQL, connection);  
  
DataSet dataSet = new DataSet();  
adapter.Fill(dataSet, currentIndex, pageSize, "Orders");  
```  
  
 在前面的示例中，**数据集**只填充了 5 个记录，但整个**订单**返回表。 若要填充**数据集**具有相同的五个记录，但仅返回这 5 个记录，使用 TOP 和 WHERE 子句在 SQL 语句，如下面的代码示例所示。  
  
```vb  
Dim pageSize As Integer = 5  
  
Dim orderSQL As String = "SELECT TOP " & pageSize & _  
  " * FROM Orders ORDER BY OrderID"  
Dim adapter As SqlDataAdapter = _  
  New SqlDataAdapter(orderSQL, connection)  
  
Dim dataSet As DataSet = New DataSet()  
adapter.Fill(dataSet, "Orders")   
```  
  
```csharp  
int pageSize = 5;  
  
string orderSQL = "SELECT TOP " + pageSize +   
  " * FROM Orders ORDER BY OrderID";  
SqlDataAdapter adapter = new SqlDataAdapter(orderSQL, connection);  
  
DataSet dataSet = new DataSet();  
adapter.Fill(dataSet, "Orders");  
```  
  
 请注意，当以这种方式进行查询结果分页时，必须保留用于对行进行排序的唯一标识符，以便将唯一 ID 传递给用于返回下一页记录的命令，如以下代码示例所示。  
  
```vb  
Dim lastRecord As String = _  
  dataSet.Tables("Orders").Rows(pageSize - 1)("OrderID").ToString()  
```  
  
```csharp  
string lastRecord =   
  dataSet.Tables["Orders"].Rows[pageSize - 1]["OrderID"].ToString();  
```  
  
 若要返回下一页记录使用的重载**填充**采用的方法**startRecord**和**maxRecords**参数，递增的当前记录索引页大小和填充表。 请记住，数据库服务器将返回整个查询结果，即使只有一个页的记录添加到**数据集**。 在以下代码示例中，先清除表行，然后再用下一页数据填充这些表行。 您可能需要在本地缓存中保留一定数量的返回行，以减少与数据库服务器的往返次数。  
  
```vb  
currentIndex = currentIndex + pageSize  
  
dataSet.Tables("Orders").Rows.Clear()  
  
adapter.Fill(dataSet, currentIndex, pageSize, "Orders")  
```  
  
```csharp  
currentIndex += pageSize;  
  
dataSet.Tables["Orders"].Rows.Clear();  
  
adapter.Fill(dataSet, currentIndex, pageSize, "Orders");  
```  
  
 若要返回下一页记录而不让数据库服务器返回整个查询，请指定对 SQL SELECT 语句的限制条件。 由于上例保留了返回的最后一个记录，因此可以在 WHERE 子句中使用它来指定查询的起点，如以下代码示例所示。  
  
```vb  
orderSQL = "SELECT TOP " & pageSize & _  
  " * FROM Orders WHERE OrderID > " & lastRecord & " ORDER BY OrderID"  
adapter.SelectCommand.CommandText = orderSQL  
  
dataSet.Tables("Orders").Rows.Clear()  
  
adapter.Fill(dataSet, "Orders")  
```  
  
```csharp  
orderSQL = "SELECT TOP " + pageSize +   
  " * FROM Orders WHERE OrderID > " + lastRecord + " ORDER BY OrderID";  
adapter.SelectCommand.CommandText = orderSQL;  
  
dataSet.Tables["Orders"].Rows.Clear();  
  
adapter.Fill(dataSet, "Orders");  
```  
  
## <a name="see-also"></a>请参阅  
 [DataAdapters 和 DataReaders](../../../../docs/framework/data/adonet/dataadapters-and-datareaders.md)  
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)
