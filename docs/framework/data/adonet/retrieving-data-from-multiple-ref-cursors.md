---
title: Pobieranie danych z wielu kursorów REF CURSOR przy użyciu OracleDataReader
ms.date: 03/30/2017
dev_langs:
- vb
ms.assetid: 361e9bd4-447d-44b7-8629-3c11f1a7ffbb
ms.openlocfilehash: e205ad39ca91dec95e54fe26cd79012c6c41ee55
ms.sourcegitcommit: ecd9e9bb2225eb76f819722ea8b24988fe46f34c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/05/2020
ms.locfileid: "96739950"
---
# <a name="retrieving-data-from-multiple-ref-cursors-using-an-oracledatareader"></a>Pobieranie danych z wielu kursorów REF CURSOR przy użyciu OracleDataReader

Ten przykład firmy Microsoft Visual Basic wykonuje procedurę składowaną PL/SQL, która zwraca dwa parametry REF CURSOR i odczytuje wartości przy użyciu <xref:System.Data.OracleClient.OracleDataReader> .

```vb
Private Sub Button1_Click( _
  ByVal sender As Object, ByVal e As System.EventArgs)  _
  Handles Button1.Click

  Dim connString As New String( _
      "Data Source=Oracle9i;User ID=scott;Password=[PLACEHOLDER];")
  Using conn As New OracleConnection(connString)
    Dim cmd As New OracleCommand()
    Dim rdr As OracleDataReader

    conn.Open()
    cmd.Connection = conn
    cmd.CommandText = "CURSPKG.OPEN_TWO_CURSORS"
    cmd.CommandType = CommandType.StoredProcedure
    cmd.Parameters.Add(New OracleParameter( _
      "EMPCURSOR", OracleType.Cursor)).Direction = _
      ParameterDirection.Output
    cmd.Parameters.Add(New OracleParameter(_
      "DEPTCURSOR", OracleType.Cursor)).Direction = _
      ParameterDirection.Output

    rdr = cmd.ExecuteReader(CommandBehavior.CloseConnection)
    While (rdr.Read())
        REM do something with the values from the EMP table
    End While

    rdr.NextResult()
    While (rdr.Read())
        REM do something with the values from the DEPT table
    End While
    rdr.Close()
  End Using
End Sub
```

## <a name="see-also"></a>Zobacz także

- [Oracle REF CURSOR](oracle-ref-cursors.md)
- [Omówienie ADO.NET](ado-net-overview.md)
