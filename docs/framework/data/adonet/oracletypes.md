---
title: OracleTypes
ms.date: 03/30/2017
ms.assetid: 18143304-d5c7-4c95-9995-678088d0c142
ms.openlocfilehash: 37089649c66c964f8a912c5a227a5281f6c0dfb7
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91189152"
---
# <a name="oracletypes"></a><span data-ttu-id="07222-102">OracleTypes</span><span class="sxs-lookup"><span data-stu-id="07222-102">OracleTypes</span></span>

<span data-ttu-id="07222-103">.NET Framework Dostawca danych dla programu Oracle zawiera kilka struktur, których można użyć do pracy z typami danych Oracle.</span><span class="sxs-lookup"><span data-stu-id="07222-103">The .NET Framework Data Provider for Oracle includes several structures you can use to work with Oracle data types.</span></span> <span data-ttu-id="07222-104">Obejmują one <xref:System.Data.OracleClient.OracleNumber> i <xref:System.Data.OracleClient.OracleString> .</span><span class="sxs-lookup"><span data-stu-id="07222-104">These include <xref:System.Data.OracleClient.OracleNumber> and <xref:System.Data.OracleClient.OracleString>.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="07222-105">Aby zapoznać się z pełną listą tych struktur, zobacz <xref:System.Data.OracleClient> .</span><span class="sxs-lookup"><span data-stu-id="07222-105">For a complete list of these structures, see <xref:System.Data.OracleClient>.</span></span>  
  
 <span data-ttu-id="07222-106">Następujące przykłady w języku C#:</span><span class="sxs-lookup"><span data-stu-id="07222-106">The following C# examples:</span></span>  
  
- <span data-ttu-id="07222-107">Utwórz tabelę Oracle i Załaduj ją z danymi.</span><span class="sxs-lookup"><span data-stu-id="07222-107">Create an Oracle table and load it with data.</span></span>  
  
- <span data-ttu-id="07222-108">Użyj <xref:System.Data.OracleClient.OracleDataReader> , aby uzyskać dostęp do danych i użyć kilku <xref:System.Data.OracleClient.OracleType> struktur do wyświetlania danych.</span><span class="sxs-lookup"><span data-stu-id="07222-108">Use an <xref:System.Data.OracleClient.OracleDataReader> to access the data, and use several <xref:System.Data.OracleClient.OracleType> structures to display the data.</span></span>  
  
## <a name="creating-an-oracle-table"></a><span data-ttu-id="07222-109">Tworzenie tabeli Oracle</span><span class="sxs-lookup"><span data-stu-id="07222-109">Creating an Oracle Table</span></span>  

 <span data-ttu-id="07222-110">Ten przykład tworzy tabelę Oracle i ładuje ją z danymi.</span><span class="sxs-lookup"><span data-stu-id="07222-110">This example creates an Oracle table and loads it with data.</span></span> <span data-ttu-id="07222-111">Ten przykład należy uruchomić przed uruchomieniem następnego przykładu.</span><span class="sxs-lookup"><span data-stu-id="07222-111">You must run this example before running the next example.</span></span>  
  
```csharp  
public void Setup(string connectionString)  
   {  
   OracleConnection conn = new OracleConnection(connectionString);  
   try  
      {  
      conn.Open();  
      OracleCommand cmd = conn.CreateCommand();  
      cmd.CommandText ="CREATE TABLE OracleTypesTable " +  
        "(MyVarchar2 varchar2(3000),MyNumber number(28,4) " +  
        "PRIMARY KEY ,MyDate date, MyRaw raw(255))";  
      cmd.ExecuteNonQuery();  
      cmd.CommandText ="INSERT INTO OracleTypesTable VALUES " +  
        "( 'test', 2, to_date('2000-01-11 12:54:01','yyyy-mm-dd " +  
        "hh24:mi:ss'), '0001020304' )";  
      cmd.ExecuteNonQuery();  
      }  
   catch(Exception)  
   {  
   }  
   finally  
   {  
      conn.Close();  
   }  
}  
```  
  
## <a name="retrieving-data-from-the-oracle-table"></a><span data-ttu-id="07222-112">Pobieranie danych z tabeli Oracle</span><span class="sxs-lookup"><span data-stu-id="07222-112">Retrieving Data from the Oracle Table</span></span>  

 <span data-ttu-id="07222-113">Ten przykład używa **OracleDataReader** do uzyskiwania dostępu do danych i używa kilku struktur **OracleType** do wyświetlania danych.</span><span class="sxs-lookup"><span data-stu-id="07222-113">This example uses an **OracleDataReader** to access the data, and uses several **OracleType** structures to display the data.</span></span>  
  
```csharp  
public void ReadOracleTypesExample(string connectionString)  
   {  
   OracleConnection myConnection =
      new OracleConnection(connectionString);  
   myConnection.Open();  
   OracleCommand myCommand = myConnection.CreateCommand();  
  
   try  
      {  
      myCommand.CommandText = "SELECT * from OracleTypesTable";  
      OracleDataReader oracledatareader1 = myCommand.ExecuteReader();  
      oracledatareader1.Read();  
  
      //Using the oracle specific getters for each type is faster than  
      //using GetOracleValue.  
  
      //First column, MyVarchar2, is a VARCHAR2 data type in Oracle  
      //Server and maps to OracleString.  
      OracleString oraclestring1 =
        oracledatareader1.GetOracleString(0);  
      Console.WriteLine("OracleString " + oraclestring1.ToString());  
  
      //Second column, MyNumber, is a NUMBER data type in Oracle Server  
      //and maps to OracleNumber.  
      OracleNumber oraclenumber1 =
        oracledatareader1.GetOracleNumber(1);  
      Console.WriteLine("OracleNumber " + oraclenumber1.ToString());  
  
      //Third column, MyDate, is a DATA data type in Oracle Server  
      //and maps to OracleDateTime.  
      OracleDateTime oracledatetime1 =
        oracledatareader1.GetOracleDateTime(2);  
      Console.WriteLine("OracleDateTime " + oracledatetime1.ToString());  
  
      //Fourth column, MyRaw, is a RAW data type in Oracle Server and  
      //maps to OracleBinary.  
      OracleBinary oraclebinary1 =
        oracledatareader1.GetOracleBinary(3);  
      //Calling value on a null OracleBinary throws  
      //OracleNullValueException; therefore, check for a null value.  
      if (oraclebinary1.IsNull==false)  
      {  
         foreach(byte b in oraclebinary1.Value)  
         {  
            Console.WriteLine("byte " + b.ToString());  
         }  
      }  
      oracledatareader1.Close();  
   }  
   catch(Exception e)  
   {  
       Console.WriteLine(e.ToString());  
   }  
   finally  
   {  
       myConnection.Close();  
   }  
}  
```  
  
## <a name="see-also"></a><span data-ttu-id="07222-114">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="07222-114">See also</span></span>

- [<span data-ttu-id="07222-115">Oracle i ADO.NET</span><span class="sxs-lookup"><span data-stu-id="07222-115">Oracle and ADO.NET</span></span>](oracle-and-adonet.md)
- [<span data-ttu-id="07222-116">Omówienie ADO.NET</span><span class="sxs-lookup"><span data-stu-id="07222-116">ADO.NET Overview</span></span>](ado-net-overview.md)
