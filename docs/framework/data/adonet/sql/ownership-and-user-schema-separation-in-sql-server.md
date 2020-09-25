---
title: Własność i oddzielenie schematu użytkownika w programie SQL Server
description: Dowiedz się, jak separacja schematów użytkownika umożliwia elastyczność zarządzania uprawnieniami obiektu SQL Server Database. Schematy grupują obiekty w oddzielne przestrzenie nazw.
ms.date: 03/30/2017
ms.assetid: 242830c1-31b5-4427-828c-cc22ff339f30
ms.openlocfilehash: e92799237a90c502aa4000d8d4027df522aa0d87
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91183146"
---
# <a name="ownership-and-user-schema-separation-in-sql-server"></a><span data-ttu-id="d94a5-104">Własność i oddzielenie schematu użytkownika w programie SQL Server</span><span class="sxs-lookup"><span data-stu-id="d94a5-104">Ownership and User-Schema Separation in SQL Server</span></span>

<span data-ttu-id="d94a5-105">Podstawową koncepcją SQL Server zabezpieczeń jest to, że właściciele obiektów mają nieodwołalne uprawnienia do administrowania nimi.</span><span class="sxs-lookup"><span data-stu-id="d94a5-105">A core concept of SQL Server security is that owners of objects have irrevocable permissions to administer them.</span></span> <span data-ttu-id="d94a5-106">Nie można usunąć uprawnień z właściciela obiektu i nie można upuścić użytkowników z bazy danych, jeśli są one właścicielami obiektów.</span><span class="sxs-lookup"><span data-stu-id="d94a5-106">You cannot remove privileges from an object owner, and you cannot drop users from a database if they own objects in it.</span></span>  
  
## <a name="user-schema-separation"></a><span data-ttu-id="d94a5-107">Oddzielanie schematu użytkownika</span><span class="sxs-lookup"><span data-stu-id="d94a5-107">User-Schema Separation</span></span>  

 <span data-ttu-id="d94a5-108">Separacja schematów użytkownika umożliwia większą elastyczność zarządzania uprawnieniami obiektu bazy danych.</span><span class="sxs-lookup"><span data-stu-id="d94a5-108">User-schema separation allows for more flexibility in managing database object permissions.</span></span> <span data-ttu-id="d94a5-109">*Schemat* to nazwany kontener dla obiektów bazy danych, który umożliwia grupowanie obiektów w oddzielne przestrzenie nazw.</span><span class="sxs-lookup"><span data-stu-id="d94a5-109">A *schema* is a named container for database objects, which allows you to group objects into separate namespaces.</span></span> <span data-ttu-id="d94a5-110">Przykładowa baza danych AdventureWorks zawiera schematy dla produkcji, sprzedaży i HumanResources.</span><span class="sxs-lookup"><span data-stu-id="d94a5-110">For example, the AdventureWorks sample database contains schemas for Production, Sales, and HumanResources.</span></span>  
  
 <span data-ttu-id="d94a5-111">Składnia nazewnictwa czterech części dla odwoływania się do obiektów określa nazwę schematu.</span><span class="sxs-lookup"><span data-stu-id="d94a5-111">The four-part naming syntax for referring to objects specifies the schema name.</span></span>  
  
```text
Server.Database.DatabaseSchema.DatabaseObject  
```  
  
### <a name="schema-owners-and-permissions"></a><span data-ttu-id="d94a5-112">Właściciele i uprawnienia schematu</span><span class="sxs-lookup"><span data-stu-id="d94a5-112">Schema Owners and Permissions</span></span>  

 <span data-ttu-id="d94a5-113">Schematy mogą należeć do każdego podmiotu zabezpieczeń bazy danych, a jeden podmiot zabezpieczeń może być właścicielem wielu schematów.</span><span class="sxs-lookup"><span data-stu-id="d94a5-113">Schemas can be owned by any database principal, and a single principal can own multiple schemas.</span></span> <span data-ttu-id="d94a5-114">Reguły zabezpieczeń można stosować do schematu, które są dziedziczone przez wszystkie obiekty w schemacie.</span><span class="sxs-lookup"><span data-stu-id="d94a5-114">You can apply security rules to a schema, which are inherited by all objects in the schema.</span></span> <span data-ttu-id="d94a5-115">Po skonfigurowaniu uprawnień dostępu dla schematu te uprawnienia są automatycznie stosowane w miarę dodawania nowych obiektów do schematu.</span><span class="sxs-lookup"><span data-stu-id="d94a5-115">Once you set up access permissions for a schema, those permissions are automatically applied as new objects are added to the schema.</span></span> <span data-ttu-id="d94a5-116">Użytkownikom można przypisać domyślny schemat, a wielu użytkowników bazy danych może współużytkować ten sam schemat.</span><span class="sxs-lookup"><span data-stu-id="d94a5-116">Users can be assigned a default schema, and multiple database users can share the same schema.</span></span>  
  
 <span data-ttu-id="d94a5-117">Domyślnie, gdy deweloperzy tworzą obiekty w schemacie, obiekty są własnością podmiotu zabezpieczeń, który jest właścicielem schematu, a nie deweloperem.</span><span class="sxs-lookup"><span data-stu-id="d94a5-117">By default, when developers create objects in a schema, the objects are owned by the security principal that owns the schema, not the developer.</span></span> <span data-ttu-id="d94a5-118">Własność obiektu można przenieść za pomocą instrukcji języka Transact-SQL ALTER AUTHORIZATION.</span><span class="sxs-lookup"><span data-stu-id="d94a5-118">Object ownership can be transferred with ALTER AUTHORIZATION Transact-SQL statement.</span></span> <span data-ttu-id="d94a5-119">Schemat może również zawierać obiekty należące do różnych użytkowników i mieć bardziej szczegółowe uprawnienia niż te przypisane do schematu, chociaż nie jest to zalecane, ponieważ zwiększa się złożoność zarządzania uprawnieniami.</span><span class="sxs-lookup"><span data-stu-id="d94a5-119">A schema can also contain objects that are owned by different users and have more granular permissions than those assigned to the schema, although this is not recommended because it adds complexity to managing permissions.</span></span> <span data-ttu-id="d94a5-120">Obiekty mogą być przenoszone między schematami, a własność schematu można przenosić między podmiotami zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="d94a5-120">Objects can be moved between schemas, and schema ownership can be transferred between principals.</span></span> <span data-ttu-id="d94a5-121">Użytkowników bazy danych można porzucić bez wpływu na schematy.</span><span class="sxs-lookup"><span data-stu-id="d94a5-121">Database users can be dropped without affecting schemas.</span></span>  
  
### <a name="built-in-schemas"></a><span data-ttu-id="d94a5-122">Schematy wbudowane</span><span class="sxs-lookup"><span data-stu-id="d94a5-122">Built-In Schemas</span></span>  

 <span data-ttu-id="d94a5-123">SQL Server jest dostarczany z dziesięcioma wstępnie zdefiniowanymi schematami, które mają takie same nazwy, jak wbudowanej użytkownika i role bazy danych.</span><span class="sxs-lookup"><span data-stu-id="d94a5-123">SQL Server ships with ten pre-defined schemas that have the same names as the built-in database users and roles.</span></span> <span data-ttu-id="d94a5-124">Istnieją one głównie w celu zapewnienia zgodności z poprzednimi wersjami.</span><span class="sxs-lookup"><span data-stu-id="d94a5-124">These exist mainly for backward compatibility.</span></span> <span data-ttu-id="d94a5-125">Można upuścić schematy mające takie same nazwy jak stałe role bazy danych, jeśli nie są potrzebne.</span><span class="sxs-lookup"><span data-stu-id="d94a5-125">You can drop the schemas that have the same names as the fixed database roles if you do not need them.</span></span> <span data-ttu-id="d94a5-126">Nie można porzucić następujących schematów:</span><span class="sxs-lookup"><span data-stu-id="d94a5-126">You cannot drop the following schemas:</span></span>  
  
- `dbo`  
  
- `guest`  
  
- `sys`  
  
- `INFORMATION_SCHEMA`  
  
 <span data-ttu-id="d94a5-127">Jeśli porzucisz je z bazy danych modelu, nie będą one wyświetlane w nowych bazach danych.</span><span class="sxs-lookup"><span data-stu-id="d94a5-127">If you drop them from the model database, they will not appear in new databases.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="d94a5-128">`sys`Schematy i `INFORMATION_SCHEMA` są zarezerwowane dla obiektów systemowych.</span><span class="sxs-lookup"><span data-stu-id="d94a5-128">The `sys` and `INFORMATION_SCHEMA` schemas are reserved for system objects.</span></span> <span data-ttu-id="d94a5-129">Nie można tworzyć obiektów w tych schematach i nie można ich upuścić.</span><span class="sxs-lookup"><span data-stu-id="d94a5-129">You cannot create objects in these schemas and you cannot drop them.</span></span>  
  
#### <a name="the-dbo-schema"></a><span data-ttu-id="d94a5-130">Schemat dbo</span><span class="sxs-lookup"><span data-stu-id="d94a5-130">The dbo Schema</span></span>  

 <span data-ttu-id="d94a5-131">`dbo`Schemat jest domyślnym schematem nowo utworzonej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="d94a5-131">The `dbo` schema is the default schema for a newly created database.</span></span> <span data-ttu-id="d94a5-132">`dbo`Schemat jest własnością `dbo` konta użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d94a5-132">The `dbo` schema is owned by the `dbo` user account.</span></span> <span data-ttu-id="d94a5-133">Domyślnie użytkownicy utworzeni za pomocą polecenia CREATE USER Transact-SQL mają `dbo` jako domyślny schemat.</span><span class="sxs-lookup"><span data-stu-id="d94a5-133">By default, users created with the CREATE USER Transact-SQL command have `dbo` as their default schema.</span></span>  
  
 <span data-ttu-id="d94a5-134">Użytkownicy, którym przypisano `dbo` schemat, nie dziedziczą uprawnień `dbo` konta użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d94a5-134">Users who are assigned the `dbo` schema do not inherit the permissions of the `dbo` user account.</span></span> <span data-ttu-id="d94a5-135">Żadne uprawnienia nie są dziedziczone przez użytkowników ze schematu; uprawnienia schematu są dziedziczone przez obiekty bazy danych zawarte w schemacie.</span><span class="sxs-lookup"><span data-stu-id="d94a5-135">No permissions are inherited from a schema by users; schema permissions are inherited by the database objects contained in the schema.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="d94a5-136">Gdy odwoływanie się do obiektów bazy danych przy użyciu jednoczęściowej nazwy, SQL Server najpierw szuka domyślnego schematu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d94a5-136">When database objects are referenced by using a one-part name, SQL Server first looks in the user's default schema.</span></span> <span data-ttu-id="d94a5-137">Jeśli obiekt nie zostanie tam znaleziony, SQL Server będzie wyglądał dalej w `dbo` schemacie.</span><span class="sxs-lookup"><span data-stu-id="d94a5-137">If the object is not found there, SQL Server looks next in the `dbo` schema.</span></span> <span data-ttu-id="d94a5-138">Jeśli obiekt nie znajduje się w `dbo` schemacie, zwracany jest błąd.</span><span class="sxs-lookup"><span data-stu-id="d94a5-138">If the object is not in the `dbo` schema, an error is returned.</span></span>  
  
## <a name="external-resources"></a><span data-ttu-id="d94a5-139">Zasoby zewnętrzne</span><span class="sxs-lookup"><span data-stu-id="d94a5-139">External Resources</span></span>  

 <span data-ttu-id="d94a5-140">Aby uzyskać więcej informacji o własności i schematach obiektów, zobacz następujące zasoby.</span><span class="sxs-lookup"><span data-stu-id="d94a5-140">For more information on object ownership and schemas, see the following resources.</span></span>  
  
|<span data-ttu-id="d94a5-141">Zasób</span><span class="sxs-lookup"><span data-stu-id="d94a5-141">Resource</span></span>|<span data-ttu-id="d94a5-142">Opis</span><span class="sxs-lookup"><span data-stu-id="d94a5-142">Description</span></span>|  
|--------------|-----------------|  
|<span data-ttu-id="d94a5-143">[Oddzielanie schematu użytkownika](/previous-versions/sql/sql-server-2008-r2/ms190387(v=sql.105))</span><span class="sxs-lookup"><span data-stu-id="d94a5-143">[User-Schema Separation](/previous-versions/sql/sql-server-2008-r2/ms190387(v=sql.105))</span></span>|<span data-ttu-id="d94a5-144">Opisuje zmiany wprowadzone przez separację w schemacie użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d94a5-144">Describes the changes introduced by user-schema separation.</span></span> <span data-ttu-id="d94a5-145">Obejmuje nowe zachowanie, jego wpływ na własność, widoki katalogów i uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="d94a5-145">Includes new behavior, its impact on ownership, catalog views, and permissions.</span></span>|  
  
## <a name="see-also"></a><span data-ttu-id="d94a5-146">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="d94a5-146">See also</span></span>

- [<span data-ttu-id="d94a5-147">Zabezpieczanie aplikacji ADO.NET</span><span class="sxs-lookup"><span data-stu-id="d94a5-147">Securing ADO.NET Applications</span></span>](../securing-ado-net-applications.md)
- [<span data-ttu-id="d94a5-148">Scenariusze zabezpieczeń aplikacji w programie SQL Server</span><span class="sxs-lookup"><span data-stu-id="d94a5-148">Application Security Scenarios in SQL Server</span></span>](application-security-scenarios-in-sql-server.md)
- [<span data-ttu-id="d94a5-149">Uwierzytelnianie w programie SQL Server</span><span class="sxs-lookup"><span data-stu-id="d94a5-149">Authentication in SQL Server</span></span>](authentication-in-sql-server.md)
- [<span data-ttu-id="d94a5-150">Serwer i role bazy danych w programie SQL Server</span><span class="sxs-lookup"><span data-stu-id="d94a5-150">Server and Database Roles in SQL Server</span></span>](server-and-database-roles-in-sql-server.md)
- [<span data-ttu-id="d94a5-151">Autoryzacja i uprawnienia w programie SQL Server</span><span class="sxs-lookup"><span data-stu-id="d94a5-151">Authorization and Permissions in SQL Server</span></span>](authorization-and-permissions-in-sql-server.md)
- [<span data-ttu-id="d94a5-152">Omówienie ADO.NET</span><span class="sxs-lookup"><span data-stu-id="d94a5-152">ADO.NET Overview</span></span>](../ado-net-overview.md)
