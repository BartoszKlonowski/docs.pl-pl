---
title: Wypełnianie zestawu danych przy użyciu przynajmniej jednego kursora REF CURSOR
ms.date: 03/30/2017
dev_langs:
- vb
ms.assetid: 99863e79-5b00-467e-a105-4ffa42de3ff7
ms.openlocfilehash: 744adb87bfc0919e861821c423a8e6a43ba7ed38
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91156371"
---
# <a name="filling-a-dataset-using-one-or-more-ref-cursors"></a><span data-ttu-id="e7ad4-102">Wypełnianie zestawu danych przy użyciu przynajmniej jednego kursora REF CURSOR</span><span class="sxs-lookup"><span data-stu-id="e7ad4-102">Filling a DataSet Using One or More REF CURSORs</span></span>

<span data-ttu-id="e7ad4-103">Ten przykład Microsoft Visual Basic wykonuje procedurę składowaną PL/SQL, która zwraca dwa parametry kursora REF, i wypełnia <xref:System.Data.DataSet> z zwracanymi wierszami.</span><span class="sxs-lookup"><span data-stu-id="e7ad4-103">This Microsoft Visual Basic example executes a PL/SQL stored procedure that returns two REF CURSOR parameters, and fills a <xref:System.Data.DataSet> with the rows that are returned.</span></span>  
  
```vb  
Private Sub Button1_Click(ByVal sender As Object, _  
  ByVal e As System.EventArgs) Handles Button1.Click  
  
  Dim connString As New String(_  
    "Data Source=Oracle9i;User ID=scott;Password=tiger;")  
  Dim ds As New DataSet()  
    Using conn As New OracleConnection(connString)  
    Dim cmd As New OracleCommand()  
  
    cmd.Connection = conn  
    cmd.CommandText = "CURSPKG.OPEN_TWO_CURSORS"  
    cmd.CommandType = CommandType.StoredProcedure  
    cmd.Parameters.Add(New OracleParameter( _  
      "EMPCURSOR", OracleType.Cursor)).Direction = _  
      ParameterDirection.Output  
    cmd.Parameters.Add(New OracleParameter( _  
      "DEPTCURSOR", OracleType.Cursor)).Direction = _  
       ParameterDirection.Output  
  
    Dim da As New OracleDataAdapter(cmd)  
    da.TableMappings.Add("Table", "Emp")  
    da.TableMappings.Add("Table1", "Dept")  
    da.Fill(ds)  
  
    ds.Relations.Add("EmpDept", ds.Tables("Dept").Columns("Deptno"), _  
      ds.Tables("Emp").Columns("Deptno"), False)  
  
    DataGrid1.DataSource = ds.Tables("Dept")  
  End Using  
```  
  
## <a name="see-also"></a><span data-ttu-id="e7ad4-104">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="e7ad4-104">See also</span></span>

- [<span data-ttu-id="e7ad4-105">Oracle REF CURSOR</span><span class="sxs-lookup"><span data-stu-id="e7ad4-105">Oracle REF CURSORs</span></span>](oracle-ref-cursors.md)
- [<span data-ttu-id="e7ad4-106">Omówienie ADO.NET</span><span class="sxs-lookup"><span data-stu-id="e7ad4-106">ADO.NET Overview</span></span>](ado-net-overview.md)
