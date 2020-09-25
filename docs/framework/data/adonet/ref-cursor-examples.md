---
title: Przykłady REF CURSOR
ms.date: 03/30/2017
ms.assetid: c257da03-c6c9-4cf8-b591-b7740a962c40
ms.openlocfilehash: b45ef971ccb6b785988cc351d02be9e0844f6e11
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91200540"
---
# <a name="ref-cursor-examples"></a><span data-ttu-id="064e3-102">Przykłady REF CURSOR</span><span class="sxs-lookup"><span data-stu-id="064e3-102">REF CURSOR Examples</span></span>

<span data-ttu-id="064e3-103">Przykłady kursora REF składają się z trzech następujących przykładów Visual Basic firmy Microsoft, które demonstrują korzystanie z kursorów REF.</span><span class="sxs-lookup"><span data-stu-id="064e3-103">The REF CURSOR examples are comprised of the following three Microsoft Visual Basic examples that demonstrate using REF CURSORs.</span></span>  
  
|<span data-ttu-id="064e3-104">Sample</span><span class="sxs-lookup"><span data-stu-id="064e3-104">Sample</span></span>|<span data-ttu-id="064e3-105">Opis</span><span class="sxs-lookup"><span data-stu-id="064e3-105">Description</span></span>|  
|------------|-----------------|  
|[<span data-ttu-id="064e3-106">Parametry kursora REF CURSOR w OracleDataReader</span><span class="sxs-lookup"><span data-stu-id="064e3-106">REF CURSOR Parameters in an OracleDataReader</span></span>](ref-cursor-parameters-in-an-oracledatareader.md)|<span data-ttu-id="064e3-107">W tym przykładzie wykonywana jest procedura składowana PL/SQL, która zwraca parametr REF CURSOR i odczytuje wartość jako <xref:System.Data.OracleClient.OracleDataReader> .</span><span class="sxs-lookup"><span data-stu-id="064e3-107">This example executes a PL/SQL stored procedure that returns a REF CURSOR parameter, and reads the value as an <xref:System.Data.OracleClient.OracleDataReader>.</span></span>|  
|[<span data-ttu-id="064e3-108">Pobieranie danych z wielu kursorów REF CURSOR przy użyciu OracleDataReader</span><span class="sxs-lookup"><span data-stu-id="064e3-108">Retrieving Data from Multiple REF CURSORs Using an OracleDataReader</span></span>](retrieving-data-from-multiple-ref-cursors.md)|<span data-ttu-id="064e3-109">W tym przykładzie wykonywana jest procedura składowana PL/SQL, która zwraca dwa parametry REF CURSOR i odczytuje wartości przy użyciu **OracleDataReader**.</span><span class="sxs-lookup"><span data-stu-id="064e3-109">This example executes a PL/SQL stored procedure that returns two REF CURSOR parameters, and reads the values using an **OracleDataReader**.</span></span>|  
|[<span data-ttu-id="064e3-110">Wypełnianie zestawu danych przy użyciu przynajmniej jednego kursora REF CURSOR</span><span class="sxs-lookup"><span data-stu-id="064e3-110">Filling a DataSet Using One or More REF CURSORs</span></span>](filling-a-dataset-using-one-or-more-ref-cursors.md)|<span data-ttu-id="064e3-111">Ten przykład wykonuje procedurę składowaną PL/SQL, która zwraca dwa parametry kursora REF, i wypełnia <xref:System.Data.DataSet> z zwracanymi wierszami.</span><span class="sxs-lookup"><span data-stu-id="064e3-111">This example executes a PL/SQL stored procedure that returns two REF CURSOR parameters, and fills a <xref:System.Data.DataSet> with the rows that are returned.</span></span>|  
  
 <span data-ttu-id="064e3-112">Aby użyć tych przykładów, może być konieczne utworzenie tabel Oracle i utworzenie pakietu PL/SQL i treści pakietu.</span><span class="sxs-lookup"><span data-stu-id="064e3-112">To use these examples, you may need to create the Oracle tables, and you must create a PL/SQL package and package body.</span></span>  
  
## <a name="creating-the-oracle-tables"></a><span data-ttu-id="064e3-113">Tworzenie tabel Oracle</span><span class="sxs-lookup"><span data-stu-id="064e3-113">Creating the Oracle Tables</span></span>  

 <span data-ttu-id="064e3-114">W tych przykładach użyto tabel, które są zdefiniowane w schemacie programu Oracle Scott/Tiger.</span><span class="sxs-lookup"><span data-stu-id="064e3-114">These examples use tables that are defined in the Oracle Scott/Tiger schema.</span></span> <span data-ttu-id="064e3-115">Schemat programu Oracle Scott/Tiger jest dołączony do większości instalacji programu Oracle.</span><span class="sxs-lookup"><span data-stu-id="064e3-115">The Oracle Scott/Tiger schema is included with most Oracle installations.</span></span> <span data-ttu-id="064e3-116">Jeśli ten schemat nie istnieje, możesz użyć pliku poleceń SQL w {OracleHome} \rdbms\admin\scott.SQL, aby utworzyć tabele i indeksy używane przez te przykłady.</span><span class="sxs-lookup"><span data-stu-id="064e3-116">If this schema does not exist, you can use the SQL commands file in {OracleHome}\rdbms\admin\scott.sql to create the tables and indexes used by these examples.</span></span>  
  
## <a name="creating-the-oracle-package-and-package-body"></a><span data-ttu-id="064e3-117">Tworzenie pakietu Oracle i treści pakietu</span><span class="sxs-lookup"><span data-stu-id="064e3-117">Creating the Oracle Package and Package Body</span></span>  

 <span data-ttu-id="064e3-118">Poniższe przykłady wymagają pakietu PL/SQL i treści pakietu na serwerze.</span><span class="sxs-lookup"><span data-stu-id="064e3-118">These examples require the following PL/SQL package and package body on your server.</span></span> <span data-ttu-id="064e3-119">Utwórz następujący pakiet Oracle na serwerze Oracle.</span><span class="sxs-lookup"><span data-stu-id="064e3-119">Create the following Oracle package on the Oracle server.</span></span>  
  
```sql
CREATE OR REPLACE PACKAGE CURSPKG AS
    TYPE T_CURSOR IS REF CURSOR;
    PROCEDURE OPEN_ONE_CURSOR (N_EMPNO IN NUMBER,
                               IO_CURSOR IN OUT T_CURSOR);
    PROCEDURE OPEN_TWO_CURSORS (EMPCURSOR OUT T_CURSOR,
                                DEPTCURSOR OUT T_CURSOR);  
END CURSPKG;  
/
```  
  
 <span data-ttu-id="064e3-120">Utwórz na serwerze Oracle następującą treść pakietu Oracle.</span><span class="sxs-lookup"><span data-stu-id="064e3-120">Create the following Oracle package body on the Oracle server.</span></span>  
  
```sql
CREATE OR REPLACE PACKAGE BODY CURSPKG AS  
    PROCEDURE OPEN_ONE_CURSOR (N_EMPNO IN NUMBER,  
                               IO_CURSOR IN OUT T_CURSOR)  
    IS
        V_CURSOR T_CURSOR;
    BEGIN
        IF N_EMPNO <> 0
        THEN  
             OPEN V_CURSOR FOR
             SELECT EMP.EMPNO, EMP.ENAME, DEPT.DEPTNO, DEPT.DNAME
                  FROM EMP, DEPT
                  WHERE EMP.DEPTNO = DEPT.DEPTNO
                  AND EMP.EMPNO = N_EMPNO;  
  
        ELSE
             OPEN V_CURSOR FOR
             SELECT EMP.EMPNO, EMP.ENAME, DEPT.DEPTNO, DEPT.DNAME
                  FROM EMP, DEPT
                  WHERE EMP.DEPTNO = DEPT.DEPTNO;  
  
        END IF;  
        IO_CURSOR := V_CURSOR;
    END OPEN_ONE_CURSOR;
  
    PROCEDURE OPEN_TWO_CURSORS (EMPCURSOR OUT T_CURSOR,  
                                DEPTCURSOR OUT T_CURSOR)  
    IS
        V_CURSOR1 T_CURSOR;
        V_CURSOR2 T_CURSOR;
    BEGIN
        OPEN V_CURSOR1 FOR SELECT * FROM EMP;  
        OPEN V_CURSOR2 FOR SELECT * FROM DEPT;  
        EMPCURSOR  := V_CURSOR1;
        DEPTCURSOR := V_CURSOR2;
    END OPEN_TWO_CURSORS;
END CURSPKG;  
/  
```  
  
## <a name="see-also"></a><span data-ttu-id="064e3-121">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="064e3-121">See also</span></span>

- [<span data-ttu-id="064e3-122">Oracle REF CURSOR</span><span class="sxs-lookup"><span data-stu-id="064e3-122">Oracle REF CURSORs</span></span>](oracle-ref-cursors.md)
- [<span data-ttu-id="064e3-123">Omówienie ADO.NET</span><span class="sxs-lookup"><span data-stu-id="064e3-123">ADO.NET Overview</span></span>](ado-net-overview.md)
