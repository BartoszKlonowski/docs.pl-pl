---
title: Korzystanie z baz danych NoSQL jako infrastruktury trwałości
description: Informacje ogólne na temat używania baz danych NoSql, a w szczególności Azure Cosmos DB jako opcji implementacji trwałości.
ms.date: 01/30/2020
ms.openlocfilehash: 2877c7eaf08dccfdf6126939b195a6a9a7195dfa
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91173382"
---
# <a name="use-nosql-databases-as-a-persistence-infrastructure"></a><span data-ttu-id="2f645-103">Korzystanie z baz danych NoSQL jako infrastruktury trwałości</span><span class="sxs-lookup"><span data-stu-id="2f645-103">Use NoSQL databases as a persistence infrastructure</span></span>

<span data-ttu-id="2f645-104">W przypadku korzystania z baz danych NoSQL dla warstwy dane infrastruktury zazwyczaj nie używasz ORM, takiego jak Entity Framework Core.</span><span class="sxs-lookup"><span data-stu-id="2f645-104">When you use NoSQL databases for your infrastructure data tier, you typically do not use an ORM like Entity Framework Core.</span></span> <span data-ttu-id="2f645-105">Zamiast tego należy użyć interfejsu API dostarczonego przez aparat NoSQL, takiego jak Azure Cosmos DB, MongoDB, Cassandra, RavenDB, CouchDB lub tabel usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="2f645-105">Instead you use the API provided by the NoSQL engine, such as Azure Cosmos DB, MongoDB, Cassandra, RavenDB, CouchDB, or Azure Storage Tables.</span></span>

<span data-ttu-id="2f645-106">Jednak w przypadku korzystania z bazy danych NoSQL Database, szczególnie zorientowanej na dokumenty bazy danych, takiej jak Azure Cosmos DB, CouchDB lub RavenDB, sposób projektowania modelu za pomocą wartości zagregowanych są częściowo podobne do tego, jak można to zrobić w EF Core, w odniesieniu do identyfikacji zagregowanych elementów głównych, klas jednostek podrzędnych i klas obiektów wartości.</span><span class="sxs-lookup"><span data-stu-id="2f645-106">However, when you use a NoSQL database, especially a document-oriented database like Azure Cosmos DB, CouchDB, or RavenDB, the way you design your model with DDD aggregates is partially similar to how you can do it in EF Core, in regards to the identification of aggregate roots, child entity classes, and value object classes.</span></span> <span data-ttu-id="2f645-107">Ostatecznie wybór bazy danych będzie miał wpływ na projekt.</span><span class="sxs-lookup"><span data-stu-id="2f645-107">But, ultimately, the database selection will impact in your design.</span></span>

<span data-ttu-id="2f645-108">W przypadku korzystania z bazy danych zorientowanej na dokumenty należy zaimplementować agregację jako pojedynczy dokument, zserializowaną w formacie JSON lub inny format.</span><span class="sxs-lookup"><span data-stu-id="2f645-108">When you use a document-oriented database, you implement an aggregate as a single document, serialized in JSON or another format.</span></span> <span data-ttu-id="2f645-109">Jednak użycie bazy danych jest niewidoczne z punktu widzenia kodu modelu domeny.</span><span class="sxs-lookup"><span data-stu-id="2f645-109">However, the use of the database is transparent from a domain model code point of view.</span></span> <span data-ttu-id="2f645-110">W przypadku korzystania z bazy danych NoSQL nadal używasz klas jednostek i agregacji klas głównych, ale z większą elastycznością niż w przypadku używania EF Core, ponieważ trwałość nie jest relacyjna.</span><span class="sxs-lookup"><span data-stu-id="2f645-110">When using a NoSQL database, you still are using entity classes and aggregate root classes, but with more flexibility than when using EF Core because the persistence is not relational.</span></span>

<span data-ttu-id="2f645-111">Różnica polega na tym, jak utrzymywać ten model.</span><span class="sxs-lookup"><span data-stu-id="2f645-111">The difference is in how you persist that model.</span></span> <span data-ttu-id="2f645-112">Jeśli model domeny został zaimplementowany na podstawie klas jednostek POCO, niezależny od do trwałości infrastruktury, może to wyglądać podobnie do innej infrastruktury trwałości, nawet od relacyjnej do NoSQL.</span><span class="sxs-lookup"><span data-stu-id="2f645-112">If you implemented your domain model based on POCO entity classes, agnostic to the infrastructure persistence, it might look like you could move to a different persistence infrastructure, even from relational to NoSQL.</span></span> <span data-ttu-id="2f645-113">Jednak nie powinno to być cel.</span><span class="sxs-lookup"><span data-stu-id="2f645-113">However, that should not be your goal.</span></span> <span data-ttu-id="2f645-114">Istnieją zawsze ograniczenia i wady dotyczące różnych technologii baz danych, dzięki czemu nie będzie można korzystać z tego samego modelu dla baz danych relacyjnych lub NoSQL.</span><span class="sxs-lookup"><span data-stu-id="2f645-114">There are always constraints and trade-offs in the different database technologies, so you will not be able to have the same model for relational or NoSQL databases.</span></span> <span data-ttu-id="2f645-115">Zmiana modeli trwałości nie jest zadaniem prostym, ponieważ transakcje i operacje trwałości będą bardzo różne.</span><span class="sxs-lookup"><span data-stu-id="2f645-115">Changing persistence models is not a trivial task, because transactions and persistence operations will be very different.</span></span>

<span data-ttu-id="2f645-116">Na przykład w bazie danych zorientowanej na dokument nie jest możliwe, aby zagregowany element główny miał wiele właściwości kolekcji podrzędnych.</span><span class="sxs-lookup"><span data-stu-id="2f645-116">For example, in a document-oriented database, it is okay for an aggregate root to have multiple child collection properties.</span></span> <span data-ttu-id="2f645-117">W relacyjnej bazie danych zapytania z wieloma podrzędnymi właściwościami kolekcji nie są łatwo zoptymalizowane, ponieważ z powrotem uzyskuje się instrukcję UNION ALL języka SQL od EF.</span><span class="sxs-lookup"><span data-stu-id="2f645-117">In a relational database, querying multiple child collection properties is not easily optimized, because you get a UNION ALL SQL statement back from EF.</span></span> <span data-ttu-id="2f645-118">Posiadanie tego samego modelu domeny dla relacyjnych baz danych lub baz danych NoSQL nie jest proste i nie należy go podejmować.</span><span class="sxs-lookup"><span data-stu-id="2f645-118">Having the same domain model for relational databases or NoSQL databases is not simple, and you should not try to do it.</span></span> <span data-ttu-id="2f645-119">Naprawdę musisz zaprojektować model, aby zrozumieć, w jaki sposób dane będą używane w każdej konkretnej bazie danych.</span><span class="sxs-lookup"><span data-stu-id="2f645-119">You really have to design your model with an understanding of how the data is going to be used in each particular database.</span></span>

<span data-ttu-id="2f645-120">Zaletą korzystania z baz danych NoSQL jest to, że jednostki są bardziej znormalizowane, dlatego nie należy ustawiać mapowania tabeli.</span><span class="sxs-lookup"><span data-stu-id="2f645-120">A benefit when using NoSQL databases is that the entities are more denormalized, so you do not set a table mapping.</span></span> <span data-ttu-id="2f645-121">Model domeny może być bardziej elastyczny niż w przypadku korzystania z relacyjnej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="2f645-121">Your domain model can be more flexible than when using a relational database.</span></span>

<span data-ttu-id="2f645-122">Podczas projektowania modelu domeny opartego na agregacjach, przeniesienie do NoSQL i baz danych zorientowane na dokumenty może być jeszcze łatwiejsze niż używanie relacyjnej bazy danych, ponieważ zagregowane wartości są podobne do serializowanych dokumentów w bazie danych zorientowanej na dokument.</span><span class="sxs-lookup"><span data-stu-id="2f645-122">When you design your domain model based on aggregates, moving to NoSQL and document-oriented databases might be even easier than using a relational database, because the aggregates you design are similar to serialized documents in a document-oriented database.</span></span> <span data-ttu-id="2f645-123">Następnie można dołączyć do tych "toreb" wszystkie informacje, które mogą być potrzebne dla tego agregacji.</span><span class="sxs-lookup"><span data-stu-id="2f645-123">Then you can include in those "bags" all the information you might need for that aggregate.</span></span>

<span data-ttu-id="2f645-124">Na przykład poniższy kod JSON to Przykładowa implementacja agregacji zamówienia przy użyciu bazy danych zorientowanej na dokument.</span><span class="sxs-lookup"><span data-stu-id="2f645-124">For instance, the following JSON code is a sample implementation of an order aggregate when using a document-oriented database.</span></span> <span data-ttu-id="2f645-125">Jest to podobne do kolejności agregowania wdrożonej w przykładzie eShopOnContainers, ale bez użycia EF Core poniżej.</span><span class="sxs-lookup"><span data-stu-id="2f645-125">It is similar to the order aggregate we implemented in the eShopOnContainers sample, but without using EF Core underneath.</span></span>

```json
{
    "id": "2017001",
    "orderDate": "2/25/2017",
    "buyerId": "1234567",
    "address": [
        {
        "street": "100 One Microsoft Way",
        "city": "Redmond",
        "state": "WA",
        "zip": "98052",
        "country": "U.S."
        }
    ],
    "orderItems": [
        {"id": 20170011, "productId": "123456", "productName": ".NET T-Shirt",
        "unitPrice": 25, "units": 2, "discount": 0},
        {"id": 20170012, "productId": "123457", "productName": ".NET Mug",
        "unitPrice": 15, "units": 1, "discount": 0}
    ]
}
```

## <a name="introduction-to-azure-cosmos-db-and-the-native-cosmos-db-api"></a><span data-ttu-id="2f645-126">Wprowadzenie do Azure Cosmos DB i natywnego interfejsu API Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="2f645-126">Introduction to Azure Cosmos DB and the native Cosmos DB API</span></span>

<span data-ttu-id="2f645-127">[Azure Cosmos DB](/azure/cosmos-db/introduction) to usługa dystrybuowana globalnie bazy danych firmy Microsoft dla aplikacji o znaczeniu strategicznym.</span><span class="sxs-lookup"><span data-stu-id="2f645-127">[Azure Cosmos DB](/azure/cosmos-db/introduction) is Microsoft's globally distributed database service for mission-critical applications.</span></span> <span data-ttu-id="2f645-128">Usługa Azure Cosmos DB zapewnia [kompleksową globalną dystrybucję](/azure/cosmos-db/distribute-data-globally), [elastyczne skalowanie przepływności i pamięci](/azure/cosmos-db/partition-data) w skali globalnej, milisekundowe opóźnienia w 99. percentylu, [pięć odpowiednio zdefiniowanych poziomów spójności](/azure/cosmos-db/consistency-levels) oraz gwarantowaną wysoką dostępność, wspierane przez [wiodące w branży umowy SLA](https://azure.microsoft.com/support/legal/sla/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="2f645-128">Azure Cosmos DB provides [turn-key global distribution](/azure/cosmos-db/distribute-data-globally), [elastic scaling of throughput and storage](/azure/cosmos-db/partition-data) worldwide, single-digit millisecond latencies at the 99th percentile, [five well-defined consistency levels](/azure/cosmos-db/consistency-levels), and guaranteed high availability, all backed by [industry-leading SLAs](https://azure.microsoft.com/support/legal/sla/cosmos-db/).</span></span> <span data-ttu-id="2f645-129">Usługa Azure Cosmos DB [automatycznie indeksuje dane](https://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) bez konieczności zarządzania schematami i indeksami.</span><span class="sxs-lookup"><span data-stu-id="2f645-129">Azure Cosmos DB [automatically indexes data](https://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) without requiring you to deal with schema and index management.</span></span> <span data-ttu-id="2f645-130">To usługa wielomodelowa, obsługująca modele oparte na dokumentach, parach klucz-wartość, grafach i kolumnach.</span><span class="sxs-lookup"><span data-stu-id="2f645-130">It is multi-model and supports document, key-value, graph, and columnar data models.</span></span>

![Diagram przedstawiający dystrybucję globalną Azure Cosmos DB.](./media/nosql-database-persistence-infrastructure/azure-cosmos-db-global-distribution.png)

<span data-ttu-id="2f645-132">**Rysunek 7-19**.</span><span class="sxs-lookup"><span data-stu-id="2f645-132">**Figure 7-19**.</span></span> <span data-ttu-id="2f645-133">Globalna dystrybucja usługi Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="2f645-133">Azure Cosmos DB global distribution</span></span>

<span data-ttu-id="2f645-134">W przypadku używania modelu języka C \# do implementowania agregacji, która ma być używana przez interfejs API Azure Cosmos DB, agregacja może być podobna do \# klas C poco używanych z EF Core.</span><span class="sxs-lookup"><span data-stu-id="2f645-134">When you use a C\# model to implement the aggregate to be used by the Azure Cosmos DB API, the aggregate can be similar to the C\# POCO classes used with EF Core.</span></span> <span data-ttu-id="2f645-135">Różnica polega na sposobie korzystania z nich z warstw aplikacji i infrastruktury, jak w poniższym kodzie:</span><span class="sxs-lookup"><span data-stu-id="2f645-135">The difference is in the way to use them from the application and infrastructure layers, as in the following code:</span></span>

```csharp
// C# EXAMPLE OF AN ORDER AGGREGATE BEING PERSISTED WITH AZURE COSMOS DB API
// *** Domain Model Code ***
// Aggregate: Create an Order object with its child entities and/or value objects.
// Then, use AggregateRoot's methods to add the nested objects so invariants and
// logic is consistent across the nested properties (value objects and entities).

Order orderAggregate = new Order
{
    Id = "2017001",
    OrderDate = new DateTime(2005, 7, 1),
    BuyerId = "1234567",
    PurchaseOrderNumber = "PO18009186470"
}

Address address = new Address
{
    Street = "100 One Microsoft Way",
    City = "Redmond",
    State = "WA",
    Zip = "98052",
    Country = "U.S."
}

orderAggregate.UpdateAddress(address);

OrderItem orderItem1 = new OrderItem
{
    Id = 20170011,
    ProductId = "123456",
    ProductName = ".NET T-Shirt",
    UnitPrice = 25,
    Units = 2,
    Discount = 0;
};

//Using methods with domain logic within the entity. No anemic-domain model
orderAggregate.AddOrderItem(orderItem1);
// *** End of Domain Model Code ***

// *** Infrastructure Code using Cosmos DB Client API ***
Uri collectionUri = UriFactory.CreateDocumentCollectionUri(databaseName,
    collectionName);

await client.CreateDocumentAsync(collectionUri, orderAggregate);

// As your app evolves, let's say your object has a new schema. You can insert
// OrderV2 objects without any changes to the database tier.
Order2 newOrder = GetOrderV2Sample("IdForSalesOrder2");
await client.CreateDocumentAsync(collectionUri, newOrder);
```

<span data-ttu-id="2f645-136">Możesz zobaczyć, że sposób pracy z modelem domeny może być podobny do sposobu korzystania z niego w warstwie modelu domeny, gdy infrastruktura jest Dr.</span><span class="sxs-lookup"><span data-stu-id="2f645-136">You can see that the way you work with your domain model can be similar to the way you use it in your domain model layer when the infrastructure is EF.</span></span> <span data-ttu-id="2f645-137">Nadal używasz tych samych agregacji metod głównych w celu zapewnienia spójności, nieodmian i walidacji w ramach agregacji.</span><span class="sxs-lookup"><span data-stu-id="2f645-137">You still use the same aggregate root methods to ensure consistency, invariants, and validations within the aggregate.</span></span>

<span data-ttu-id="2f645-138">Jednak w przypadku utrwalania modelu w bazie danych NoSQL zmiana kodu i interfejsu API znacznie porównana z kodem EF Core lub innym kodem związanym z relacyjnymi bazami danych.</span><span class="sxs-lookup"><span data-stu-id="2f645-138">However, when you persist your model into the NoSQL database, the code and API change dramatically compared to EF Core code or any other code related to relational databases.</span></span>

## <a name="implement-net-code-targeting-mongodb-and-azure-cosmos-db"></a><span data-ttu-id="2f645-139">Implementowanie kodu platformy .NET dla MongoDB i Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="2f645-139">Implement .NET code targeting MongoDB and Azure Cosmos DB</span></span>

### <a name="use-azure-cosmos-db-from-net-containers"></a><span data-ttu-id="2f645-140">Używanie Azure Cosmos DB z kontenerów platformy .NET</span><span class="sxs-lookup"><span data-stu-id="2f645-140">Use Azure Cosmos DB from .NET containers</span></span>

<span data-ttu-id="2f645-141">Dostęp do Azure Cosmos DB baz danych można uzyskać z kodu platformy .NET działającego w kontenerach, podobnie jak w przypadku dowolnej innej aplikacji platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="2f645-141">You can access Azure Cosmos DB databases from .NET code running in containers, like from any other .NET application.</span></span> <span data-ttu-id="2f645-142">Na przykład w programie eShopOnContainers są implementowane mikrousługi lokalizacji. API i marketingu. API, dzięki czemu mogą korzystać z Azure Cosmos DB baz danych.</span><span class="sxs-lookup"><span data-stu-id="2f645-142">For instance, the Locations.API and Marketing.API microservices in eShopOnContainers are implemented so they can consume Azure Cosmos DB databases.</span></span>

<span data-ttu-id="2f645-143">Istnieje jednak ograniczenie Azure Cosmos DB z punktu widzenia środowiska projektowania platformy Docker.</span><span class="sxs-lookup"><span data-stu-id="2f645-143">However, there’s a limitation in Azure Cosmos DB from a Docker development environment point of view.</span></span> <span data-ttu-id="2f645-144">Mimo że istnieje [Azure Cosmos DB emulatora](/azure/cosmos-db/local-emulator) lokalnego, który można uruchomić na lokalnym komputerze deweloperskim, obsługuje tylko system Windows.</span><span class="sxs-lookup"><span data-stu-id="2f645-144">Even though there’s an on-premises [Azure Cosmos DB Emulator](/azure/cosmos-db/local-emulator) that can run in a local development machine, it only supports Windows.</span></span> <span data-ttu-id="2f645-145">Linux i macOS nie są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="2f645-145">Linux and macOS aren't supported.</span></span>

<span data-ttu-id="2f645-146">Istnieje również możliwość uruchomienia tego emulatora na platformie Docker, ale tylko w kontenerach systemu Windows, a nie w przypadku kontenerów z systemem Linux.</span><span class="sxs-lookup"><span data-stu-id="2f645-146">There's also the possibility to run this emulator on Docker, but just on Windows Containers, not with Linux Containers.</span></span> <span data-ttu-id="2f645-147">Jest to wstępna ochrona środowiska programistycznego, jeśli aplikacja jest wdrażana jako kontenery systemu Linux, ponieważ obecnie nie można wdrażać kontenerów systemów Linux i Windows na Docker for Windows w tym samym czasie.</span><span class="sxs-lookup"><span data-stu-id="2f645-147">That's an initial handicap for the development environment if your application is deployed as Linux containers, since, currently, you can't deploy Linux and Windows Containers on Docker for Windows at the same time.</span></span> <span data-ttu-id="2f645-148">Wszystkie wdrażane kontenery muszą być przeznaczone dla systemu Linux lub Windows.</span><span class="sxs-lookup"><span data-stu-id="2f645-148">Either all containers being deployed have to be for Linux or for Windows.</span></span>

<span data-ttu-id="2f645-149">Idealnym i bardziej prostym wdrożeniem rozwiązania deweloperskiego/testowego jest możliwość wdrażania systemów baz danych jako kontenerów wraz z niestandardowymi kontenerami, dzięki czemu środowiska deweloperskie/testowe są zawsze spójne.</span><span class="sxs-lookup"><span data-stu-id="2f645-149">The ideal and more straightforward deployment for a dev/test solution is to be able to deploy your database systems as containers along with your custom containers so your dev/test environments are always consistent.</span></span>

### <a name="use-mongodb-api-for-local-devtest-linuxwindows-containers-plus-azure-cosmos-db"></a><span data-ttu-id="2f645-150">Korzystanie z interfejsu API MongoDB na potrzeby lokalnego tworzenia i testowania kontenerów systemu Linux/Windows oraz Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="2f645-150">Use MongoDB API for local dev/test Linux/Windows containers plus Azure Cosmos DB</span></span>

<span data-ttu-id="2f645-151">Bazy danych Cosmos DB obsługują interfejs API MongoDB dla platformy .NET oraz natywny protokół MongoDB.</span><span class="sxs-lookup"><span data-stu-id="2f645-151">Cosmos DB databases support MongoDB API for .NET as well as the native MongoDB wire protocol.</span></span> <span data-ttu-id="2f645-152">Oznacza to, że korzystając z istniejących sterowników, aplikacja zapisywana dla MongoDB może teraz komunikować się z Cosmos DB i używać Cosmos DB baz danych zamiast baz danych MongoDB, jak pokazano na rysunku 7-20.</span><span class="sxs-lookup"><span data-stu-id="2f645-152">This means that by using existing drivers, your application written for MongoDB can now communicate with Cosmos DB and use Cosmos DB databases instead of MongoDB databases, as shown in Figure 7-20.</span></span>

![Diagram przedstawiający, że Cosmos DB obsługuje protokoły sieciowe .NET i MongoDB.](./media/nosql-database-persistence-infrastructure/mongodb-api-wire-protocol.png)

<span data-ttu-id="2f645-154">**Rysunek 7-20**.</span><span class="sxs-lookup"><span data-stu-id="2f645-154">**Figure 7-20**.</span></span> <span data-ttu-id="2f645-155">Używanie interfejsu API MongoDB i protokołu do uzyskiwania dostępu Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="2f645-155">Using MongoDB API and protocol to access Azure Cosmos DB</span></span>

<span data-ttu-id="2f645-156">Jest to bardzo wygodne podejście do weryfikacji koncepcji w środowiskach platformy Docker z kontenerami systemu Linux, ponieważ [obraz platformy](https://hub.docker.com/r/_/mongo/) Docker MongoDB jest obrazem wielodostępnym, który obsługuje kontenery platformy Docker Linux i kontenery platformy Docker.</span><span class="sxs-lookup"><span data-stu-id="2f645-156">This is a very convenient approach for proof of concepts in Docker environments with Linux containers because the [MongoDB Docker image](https://hub.docker.com/r/_/mongo/) is a multi-arch image that supports Docker Linux containers and Docker Windows containers.</span></span>

<span data-ttu-id="2f645-157">Jak pokazano na poniższej ilustracji, za pomocą interfejsu API MongoDB, eShopOnContainers obsługuje kontenery systemu Linux i Windows dla lokalnego środowiska programistycznego, ale można przenieść do skalowalnego rozwiązania w chmurze PaaS jako Azure Cosmos DB przez [zmianę parametrów połączenia MongoDB w taki sposób, aby wskazywały Azure Cosmos DB](/azure/cosmos-db/connect-mongodb-account).</span><span class="sxs-lookup"><span data-stu-id="2f645-157">As shown in the following image, by using the MongoDB API, eShopOnContainers supports MongoDB Linux and Windows containers for the local development environment but then, you can move to a scalable, PaaS cloud solution as Azure Cosmos DB by simply [changing the MongoDB connection string to point to Azure Cosmos DB](/azure/cosmos-db/connect-mongodb-account).</span></span>

![Diagram przedstawiający, że mikrousługa lokalizacji w eShopOnContainers może używać Cosmos DB lub Mongo DB.](./media/nosql-database-persistence-infrastructure/eshoponcontainers-mongodb-containers.png)

<span data-ttu-id="2f645-159">**Rysunek 7-21**.</span><span class="sxs-lookup"><span data-stu-id="2f645-159">**Figure 7-21**.</span></span> <span data-ttu-id="2f645-160">eShopOnContainers przy użyciu kontenerów MongoDB do celów deweloperskich lub Azure Cosmos DB produkcyjnych</span><span class="sxs-lookup"><span data-stu-id="2f645-160">eShopOnContainers using MongoDB containers for dev-env or Azure Cosmos DB for production</span></span>

<span data-ttu-id="2f645-161">Azure Cosmos DB produkcyjne będzie działać w chmurze platformy Azure jako usługa PaaS i skalowalna.</span><span class="sxs-lookup"><span data-stu-id="2f645-161">The production Azure Cosmos DB would be running in Azure's cloud as a PaaS and scalable service.</span></span>

<span data-ttu-id="2f645-162">Niestandardowe kontenery programu .NET Core można uruchamiać na lokalnym hoście platformy Docker (używanym Docker for Windows na komputerze z systemem Windows 10) lub wdrożyć w środowisku produkcyjnym, takim jak Kubernetes na platformie Azure AKS lub platformie Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="2f645-162">Your custom .NET Core containers can run on a local development Docker host (that is using Docker for Windows in a Windows 10 machine) or be deployed into a production environment, like Kubernetes in Azure AKS or Azure Service Fabric.</span></span> <span data-ttu-id="2f645-163">W tym drugim środowisku wdrożono tylko kontenery niestandardowe platformy .NET Core, ale nie kontener MongoDB, ponieważ do obsługi danych w środowisku produkcyjnym jest używany Azure Cosmos DB w chmurze.</span><span class="sxs-lookup"><span data-stu-id="2f645-163">In this second environment, you would deploy only the .NET Core custom containers but not the MongoDB container since you'd be using Azure Cosmos DB in the cloud for handling the data in production.</span></span>

<span data-ttu-id="2f645-164">Oczywistą zaletą korzystania z interfejsu API MongoDB jest to, że rozwiązanie może działać zarówno w aparatach baz danych, MongoDB, jak i Azure Cosmos DB, dzięki czemu migracja do różnych środowisk powinna być łatwa.</span><span class="sxs-lookup"><span data-stu-id="2f645-164">A clear benefit of using the MongoDB API is that your solution could run in both database engines, MongoDB or Azure Cosmos DB, so migrations to different environments should be easy.</span></span> <span data-ttu-id="2f645-165">Jednak czasami jest wartościowa użycie natywnego interfejsu API (jest to natywny interfejs API Cosmos DB) w celu pełnego wykorzystania możliwości określonego aparatu bazy danych.</span><span class="sxs-lookup"><span data-stu-id="2f645-165">However, sometimes it is worthwhile to use a native API (that is the native Cosmos DB API) in order to take full advantage of the capabilities of a specific database engine.</span></span>

<span data-ttu-id="2f645-166">Aby uzyskać dalsze porównanie między zwykłym użyciem MongoDB a Cosmos DB w chmurze, zobacz [zalety korzystania z Azure Cosmos DB na tej stronie](/azure/cosmos-db/mongodb-introduction).</span><span class="sxs-lookup"><span data-stu-id="2f645-166">For further comparison between simply using MongoDB versus Cosmos DB in the cloud, see the [Benefits of using Azure Cosmos DB in this page](/azure/cosmos-db/mongodb-introduction).</span></span>

### <a name="analyze-your-approach-for-production-applications-mongodb-api-vs-cosmos-db-api"></a><span data-ttu-id="2f645-167">Analizowanie podejścia do aplikacji produkcyjnych: MongoDB API a interfejs API Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="2f645-167">Analyze your approach for production applications: MongoDB API vs. Cosmos DB API</span></span>

<span data-ttu-id="2f645-168">W eShopOnContainers korzystamy z interfejsu API MongoDB, ponieważ naszym priorytetem było podstawowe środowisko deweloperskie/testowe przy użyciu bazy danych NoSQL, która może również współejść z Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="2f645-168">In eShopOnContainers, we're using MongoDB API because our priority was fundamentally to have a consistent dev/test environment using a NoSQL database that could also work with Azure Cosmos DB.</span></span>

<span data-ttu-id="2f645-169">Jeśli jednak planujesz używać interfejsu API MongoDB do uzyskiwania dostępu do Azure Cosmos DB na platformie Azure dla aplikacji produkcyjnych, należy przeanalizować różnice w zakresie możliwości i wydajności podczas korzystania z interfejsu API MongoDB w celu uzyskania dostępu do Azure Cosmos DB baz danych w porównaniu z użyciem natywnego interfejsu API Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="2f645-169">However, if you are planning to use MongoDB API to access Azure Cosmos DB in Azure for production applications, you should analyze the differences in capabilities and performance when using MongoDB API to access Azure Cosmos DB databases compared to using the native Azure Cosmos DB API.</span></span> <span data-ttu-id="2f645-170">Jeśli jest podobna, można użyć interfejsu API MongoDB i uzyskać korzyści z obsługi dwóch aparatów bazy danych NoSQL w tym samym czasie.</span><span class="sxs-lookup"><span data-stu-id="2f645-170">If it is similar you can use MongoDB API and you get the benefit of supporting two NoSQL database engines at the same time.</span></span>

<span data-ttu-id="2f645-171">Klastry MongoDB można również używać jako produkcyjnej bazy danych w chmurze platformy Azure, za pomocą [usługi MongoDB platformy Azure](https://www.mongodb.com/scale/mongodb-azure-service).</span><span class="sxs-lookup"><span data-stu-id="2f645-171">You could also use MongoDB clusters as the production database in Azure's cloud, too, with [MongoDB Azure Service](https://www.mongodb.com/scale/mongodb-azure-service).</span></span> <span data-ttu-id="2f645-172">Ale nie jest to usługa PaaS świadczona przez firmę Microsoft.</span><span class="sxs-lookup"><span data-stu-id="2f645-172">But that is not a PaaS service provided by Microsoft.</span></span> <span data-ttu-id="2f645-173">W takim przypadku platforma Azure obsługuje tylko to rozwiązanie pochodzące z MongoDB.</span><span class="sxs-lookup"><span data-stu-id="2f645-173">In this case, Azure is just hosting that solution coming from MongoDB.</span></span>

<span data-ttu-id="2f645-174">Zasadniczo jest to tylko oświadczenie stwierdzające, że nie należy zawsze używać interfejsu API MongoDB w odniesieniu do Azure Cosmos DB, tak jak w eShopOnContainers, ponieważ było to wygodne rozwiązanie dla kontenerów systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="2f645-174">Basically, this is just a disclaimer stating that you shouldn't always use MongoDB API against Azure Cosmos DB, as we did in eShopOnContainers because it was a convenient choice for Linux containers.</span></span> <span data-ttu-id="2f645-175">Decyzja powinna być oparta na określonych wymaganiach i testach, które należy wykonać w przypadku aplikacji produkcyjnej.</span><span class="sxs-lookup"><span data-stu-id="2f645-175">The decision should be based on the specific needs and tests you need to do for your production application.</span></span>

### <a name="the-code-use-mongodb-api-in-net-core-applications"></a><span data-ttu-id="2f645-176">Kod: Użyj interfejsu API MongoDB w aplikacjach .NET Core</span><span class="sxs-lookup"><span data-stu-id="2f645-176">The code: Use MongoDB API in .NET Core applications</span></span>

<span data-ttu-id="2f645-177">Interfejs API MongoDB dla platformy .NET jest oparty na pakietach NuGet, które należy dodać do projektów, takich jak w projekcie Locations. API pokazane na poniższej ilustracji.</span><span class="sxs-lookup"><span data-stu-id="2f645-177">MongoDB API for .NET is based on NuGet packages that you need to add to your projects, like in the Locations.API project shown in the following figure.</span></span>

![Zrzut ekranu zależności w pakietach NuGet MongoDB.](./media/nosql-database-persistence-infrastructure/mongodb-api-nuget-packages.png)

<span data-ttu-id="2f645-179">**Rysunek 7-22**.</span><span class="sxs-lookup"><span data-stu-id="2f645-179">**Figure 7-22**.</span></span> <span data-ttu-id="2f645-180">Pakiety NuGet interfejsu API MongoDB w projekcie .NET Core</span><span class="sxs-lookup"><span data-stu-id="2f645-180">MongoDB API NuGet packages references in a .NET Core project</span></span>

<span data-ttu-id="2f645-181">Zbadamy kod w poniższych sekcjach.</span><span class="sxs-lookup"><span data-stu-id="2f645-181">Let's investigate the code in the following sections.</span></span>

#### <a name="a-model-used-by-mongodb-api"></a><span data-ttu-id="2f645-182">Model używany przez interfejs API MongoDB</span><span class="sxs-lookup"><span data-stu-id="2f645-182">A Model used by MongoDB API</span></span>

<span data-ttu-id="2f645-183">Najpierw należy zdefiniować model, który będzie przechowywać dane pochodzące z bazy danych w przestrzeni pamięci aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2f645-183">First, you need to define a model that will hold the data coming from the database in your application's memory space.</span></span> <span data-ttu-id="2f645-184">Poniżej przedstawiono przykładowy model używany do lokalizacji w eShopOnContainers.</span><span class="sxs-lookup"><span data-stu-id="2f645-184">Here's an example of the model used for Locations at eShopOnContainers.</span></span>

```csharp
using MongoDB.Bson;
using MongoDB.Bson.Serialization.Attributes;
using MongoDB.Driver.GeoJsonObjectModel;
using System.Collections.Generic;

public class Locations
{
    [BsonId]
    [BsonRepresentation(BsonType.ObjectId)]
    public string Id { get; set; }
    public int LocationId { get; set; }
    public string Code { get; set; }
    [BsonRepresentation(BsonType.ObjectId)]
    public string Parent_Id { get; set; }
    public string Description { get; set; }
    public double Latitude { get; set; }
    public double Longitude { get; set; }
    public GeoJsonPoint<GeoJson2DGeographicCoordinates> Location
                                                             { get; private set; }
    public GeoJsonPolygon<GeoJson2DGeographicCoordinates> Polygon
                                                             { get; private set; }
    public void SetLocation(double lon, double lat) => SetPosition(lon, lat);
    public void SetArea(List<GeoJson2DGeographicCoordinates> coordinatesList)
                                                    => SetPolygon(coordinatesList);

    private void SetPosition(double lon, double lat)
    {
        Latitude = lat;
        Longitude = lon;
        Location = new GeoJsonPoint<GeoJson2DGeographicCoordinates>(
            new GeoJson2DGeographicCoordinates(lon, lat));
    }

    private void SetPolygon(List<GeoJson2DGeographicCoordinates> coordinatesList)
    {
        Polygon = new GeoJsonPolygon<GeoJson2DGeographicCoordinates>(
                  new GeoJsonPolygonCoordinates<GeoJson2DGeographicCoordinates>(
                  new GeoJsonLinearRingCoordinates<GeoJson2DGeographicCoordinates>(
                                                                 coordinatesList)));
    }
}
```

<span data-ttu-id="2f645-185">Można zobaczyć kilka atrybutów i typów pochodzących z pakietów NuGet MongoDB.</span><span class="sxs-lookup"><span data-stu-id="2f645-185">You can see there are a few attributes and types coming from the MongoDB NuGet packages.</span></span>

<span data-ttu-id="2f645-186">Bazy danych NoSQL są zwykle bardzo dobrze dopasowane do pracy z nierelacyjnymi danymi hierarchicznymi.</span><span class="sxs-lookup"><span data-stu-id="2f645-186">NoSQL databases are usually very well suited for working with non-relational hierarchical data.</span></span> <span data-ttu-id="2f645-187">W tym przykładzie używamy typów MongoDB, szczególnie dla lokalizacji geograficznych, takich jak `GeoJson2DGeographicCoordinates` .</span><span class="sxs-lookup"><span data-stu-id="2f645-187">In this example, we are using MongoDB types especially made for geo-locations, like `GeoJson2DGeographicCoordinates`.</span></span>

#### <a name="retrieve-the-database-and-the-collection"></a><span data-ttu-id="2f645-188">Pobieranie bazy danych i kolekcji</span><span class="sxs-lookup"><span data-stu-id="2f645-188">Retrieve the database and the collection</span></span>

<span data-ttu-id="2f645-189">W eShopOnContainers został utworzony niestandardowy kontekst bazy danych, w którym implementujemy kod w celu pobrania bazy danych i MongoCollections, jak w poniższym kodzie.</span><span class="sxs-lookup"><span data-stu-id="2f645-189">In eShopOnContainers, we have created a custom database context where we implement the code to retrieve the database and the MongoCollections, as in the following code.</span></span>

```csharp
public class LocationsContext
{
    private readonly IMongoDatabase _database = null;

    public LocationsContext(IOptions<LocationSettings> settings)
    {
        var client = new MongoClient(settings.Value.ConnectionString);
        if (client != null)
            _database = client.GetDatabase(settings.Value.Database);
    }

    public IMongoCollection<Locations> Locations
    {
        get
        {
            return _database.GetCollection<Locations>("Locations");
        }
    }
}
```

#### <a name="retrieve-the-data"></a><span data-ttu-id="2f645-190">Pobieranie danych</span><span class="sxs-lookup"><span data-stu-id="2f645-190">Retrieve the data</span></span>

<span data-ttu-id="2f645-191">W kodzie C#, takich jak kontrolery internetowego interfejsu API lub wdrożenie niestandardowych repozytoriów, można napisać podobny kod do poniższego podczas wykonywania zapytań za pomocą interfejsu API MongoDB.</span><span class="sxs-lookup"><span data-stu-id="2f645-191">In C# code, like Web API controllers or custom Repositories implementation, you can write similar code to the following when querying through the MongoDB API.</span></span> <span data-ttu-id="2f645-192">Należy zauważyć, że `_context` obiekt jest wystąpieniem poprzedniej `LocationsContext` klasy.</span><span class="sxs-lookup"><span data-stu-id="2f645-192">Note that the `_context` object is an instance of the previous `LocationsContext` class.</span></span>

```csharp
public async Task<Locations> GetAsync(int locationId)
{
    var filter = Builders<Locations>.Filter.Eq("LocationId", locationId);
    return await _context.Locations
                            .Find(filter)
                            .FirstOrDefaultAsync();
}
```

#### <a name="use-an-env-var-in-the-docker-composeoverrideyml-file-for-the-mongodb-connection-string"></a><span data-ttu-id="2f645-193">Użyj funkcji ENV-var w pliku Docker-Compose. override. yml dla parametrów połączenia MongoDB</span><span class="sxs-lookup"><span data-stu-id="2f645-193">Use an env-var in the docker-compose.override.yml file for the MongoDB connection string</span></span>

<span data-ttu-id="2f645-194">Podczas tworzenia obiektu MongoClient musi on mieć podstawowy parametr, który jest precyzyjnym `ConnectionString` parametrem wskazującym odpowiednią bazę danych.</span><span class="sxs-lookup"><span data-stu-id="2f645-194">When creating a MongoClient object, it needs a fundamental parameter which is precisely the `ConnectionString` parameter pointing to the right database.</span></span> <span data-ttu-id="2f645-195">W przypadku eShopOnContainers parametry połączenia mogą wskazywać lokalny kontener platformy Docker MongoDB lub do bazy danych Azure Cosmos DB produkcyjnych.</span><span class="sxs-lookup"><span data-stu-id="2f645-195">In the case of eShopOnContainers, the connection string can point to a local MongoDB Docker container or to a "production" Azure Cosmos DB database.</span></span>  <span data-ttu-id="2f645-196">Te parametry połączenia pochodzą ze zmiennych środowiskowych zdefiniowanych w `docker-compose.override.yml` plikach używanych podczas wdrażania przy użyciu platformy Docker-redagowanie lub programu Visual Studio, jak w poniższym kodzie YML.</span><span class="sxs-lookup"><span data-stu-id="2f645-196">That connection string comes from the environment variables defined in the `docker-compose.override.yml` files used when deploying with docker-compose or Visual Studio, as in the following yml code.</span></span>

```yml
# docker-compose.override.yml
version: '3.4'
services:
  # Other services
  locations-api:
    environment:
      # Other settings
      - ConnectionString=${ESHOP_AZURE_COSMOSDB:-mongodb://nosqldata}

```

<span data-ttu-id="2f645-197">`ConnectionString`Zmienna środowiskowa jest rozpoznawana w następujący sposób: Jeśli `ESHOP_AZURE_COSMOSDB` zmienna globalna jest zdefiniowana w `.env` pliku z Azure Cosmos DB parametrami połączenia, użyje go w celu uzyskania dostępu do bazy danych Azure Cosmos DB w chmurze.</span><span class="sxs-lookup"><span data-stu-id="2f645-197">The `ConnectionString` environment variable is resolved this way: If the `ESHOP_AZURE_COSMOSDB` global variable is defined in the `.env` file with the Azure Cosmos DB connection string, it will use it to access the Azure Cosmos DB database in the cloud.</span></span> <span data-ttu-id="2f645-198">Jeśli ta wartość nie jest zdefiniowana, zostanie ona przestosowana `mongodb://nosqldata` i będzie używać kontenera MongoDB Development.</span><span class="sxs-lookup"><span data-stu-id="2f645-198">If it’s not defined, it will take the `mongodb://nosqldata` value and use the development MongoDB container.</span></span>

<span data-ttu-id="2f645-199">Poniższy kod przedstawia `.env` plik Azure Cosmos DB z eShopOnContainersą globalną zmienną środowiskową parametrów połączenia, zgodnie z zaimplementowaną w programie:</span><span class="sxs-lookup"><span data-stu-id="2f645-199">The following code shows the `.env` file with the Azure Cosmos DB connection string global environment variable, as implemented in eShopOnContainers:</span></span>

```yml
# .env file, in eShopOnContainers root folder
# Other Docker environment variables

ESHOP_EXTERNAL_DNS_NAME_OR_IP=localhost
ESHOP_PROD_EXTERNAL_DNS_NAME_OR_IP=<YourDockerHostIP>

#ESHOP_AZURE_COSMOSDB=<YourAzureCosmosDBConnData>

#Other environment variables for additional Azure infrastructure assets
#ESHOP_AZURE_REDIS_BASKET_DB=<YourAzureRedisBasketInfo>
#ESHOP_AZURE_STORAGE_CATALOG_URL=<YourAzureStorage_Catalog_BLOB_URL>
#ESHOP_AZURE_SERVICE_BUS=<YourAzureServiceBusInfo>
```

<span data-ttu-id="2f645-200">Usuń komentarz z wiersza ESHOP_AZURE_COSMOSDB i zaktualizuj go przy użyciu parametrów połączenia Azure Cosmos DB uzyskanych z Azure Portal, jak wyjaśniono w temacie [łączenie aplikacji MongoDB z Azure Cosmos DB](/azure/cosmos-db/connect-mongodb-account).</span><span class="sxs-lookup"><span data-stu-id="2f645-200">Uncomment the ESHOP_AZURE_COSMOSDB line and update it with your Azure Cosmos DB connection string obtained from the Azure portal as explained in [Connect a MongoDB application to Azure Cosmos DB](/azure/cosmos-db/connect-mongodb-account).</span></span>

<span data-ttu-id="2f645-201">Jeśli `ESHOP_AZURE_COSMOSDB` zmienna globalna jest pusta, co oznacza, że jest oznaczona jako komentarz do `.env` pliku, kontener używa domyślnych parametrów połączenia MongoDB.</span><span class="sxs-lookup"><span data-stu-id="2f645-201">If the `ESHOP_AZURE_COSMOSDB` global variable is empty, meaning it's commented out in the `.env` file, then the container uses a default MongoDB connection string.</span></span> <span data-ttu-id="2f645-202">Te parametry połączenia wskazują lokalny kontener MongoDB wdrożony w eShopOnContainers o nazwie `nosqldata` i został zdefiniowany w pliku Docker-Zredaguj, jak pokazano w poniższym kodzie. yml:</span><span class="sxs-lookup"><span data-stu-id="2f645-202">This connection string points to the local MongoDB container deployed in eShopOnContainers that is named `nosqldata` and was defined at the docker-compose file, as shown in the following .yml code:</span></span>

``` yml
# docker-compose.yml
version: '3.4'
services:
  # ...Other services...
  nosqldata:
    image: mongo
```

#### <a name="additional-resources"></a><span data-ttu-id="2f645-203">Zasoby dodatkowe</span><span class="sxs-lookup"><span data-stu-id="2f645-203">Additional resources</span></span>

- <span data-ttu-id="2f645-204">**Modelowanie danych dokumentu dla baz danych NoSQL** </span><span class="sxs-lookup"><span data-stu-id="2f645-204">**Modeling document data for NoSQL databases** </span></span>\
  <https://docs.microsoft.com/azure/cosmos-db/modeling-data>

- <span data-ttu-id="2f645-205">**Vaughn Vernon. Idealny magazyn agregacji projektu opartego na domenie?**</span><span class="sxs-lookup"><span data-stu-id="2f645-205">**Vaughn Vernon. The Ideal Domain-Driven Design Aggregate Store?**</span></span> \
  <https://kalele.io/blog-posts/the-ideal-domain-driven-design-aggregate-store/>

- <span data-ttu-id="2f645-206">**Wprowadzenie do Azure Cosmos DB: interfejs API dla MongoDB**  </span><span class="sxs-lookup"><span data-stu-id="2f645-206">**Introduction to Azure Cosmos DB: API for MongoDB**  </span></span>\
  <https://docs.microsoft.com/azure/cosmos-db/mongodb-introduction>

- <span data-ttu-id="2f645-207">**Azure Cosmos DB: Tworzenie aplikacji internetowej interfejsu API MongoDB za pomocą platformy .NET i Azure Portal**  </span><span class="sxs-lookup"><span data-stu-id="2f645-207">**Azure Cosmos DB: Build a MongoDB API web app with .NET and the Azure portal**  </span></span>\
  <https://docs.microsoft.com/azure/cosmos-db/create-mongodb-dotnet>

- <span data-ttu-id="2f645-208">**Korzystanie z emulatora Azure Cosmos DB na potrzeby lokalnego tworzenia i testowania**  </span><span class="sxs-lookup"><span data-stu-id="2f645-208">**Use the Azure Cosmos DB Emulator for local development and testing**  </span></span>\
  <https://docs.microsoft.com/azure/cosmos-db/local-emulator>

- <span data-ttu-id="2f645-209">**Łączenie aplikacji MongoDB z usługą Azure Cosmos DB**  </span><span class="sxs-lookup"><span data-stu-id="2f645-209">**Connect a MongoDB application to Azure Cosmos DB**  </span></span>\
  <https://docs.microsoft.com/azure/cosmos-db/connect-mongodb-account>

- <span data-ttu-id="2f645-210">**Obraz Cosmos DB Docker emulatora (kontener systemu Windows)**  </span><span class="sxs-lookup"><span data-stu-id="2f645-210">**The Cosmos DB Emulator Docker image (Windows Container)**  </span></span>\
  <https://hub.docker.com/r/microsoft/azure-cosmosdb-emulator/>

- <span data-ttu-id="2f645-211">**Obraz platformy Docker MongoDB (kontener Linux i Windows)**  </span><span class="sxs-lookup"><span data-stu-id="2f645-211">**The MongoDB Docker image (Linux and Windows Container)**  </span></span>\
  <https://hub.docker.com/_/mongo/>

- <span data-ttu-id="2f645-212">**Korzystanie z programu korzystanie programu mongochef (Studio 3T) z Azure Cosmos DB: interfejs API dla konta MongoDB**  </span><span class="sxs-lookup"><span data-stu-id="2f645-212">**Use MongoChef (Studio 3T) with an Azure Cosmos DB: API for MongoDB account**  </span></span>\
  <https://docs.microsoft.com/azure/cosmos-db/mongodb-mongochef>

>[!div class="step-by-step"]
><span data-ttu-id="2f645-213">[Poprzedni](infrastructure-persistence-layer-implementation-entity-framework-core.md) 
> [Dalej](microservice-application-layer-web-api-design.md)</span><span class="sxs-lookup"><span data-stu-id="2f645-213">[Previous](infrastructure-persistence-layer-implementation-entity-framework-core.md)
[Next](microservice-application-layer-web-api-design.md)</span></span>
