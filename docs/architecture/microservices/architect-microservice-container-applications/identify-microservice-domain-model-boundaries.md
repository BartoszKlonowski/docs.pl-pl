---
title: Identyfikowanie ograniczeń modelu domeny dla poszczególnych mikrousług
description: Zapoznaj się z istotą partycjonowania dużej aplikacji do mikrousług w celu osiągnięcia architektury dźwiękowej.
ms.date: 09/20/2018
ms.openlocfilehash: aa903e13b20be1084fad60e6fb7bbb1c61403deb
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/30/2019
ms.locfileid: "70295503"
---
# <a name="identify-domain-model-boundaries-for-each-microservice"></a><span data-ttu-id="c061f-103">Określ granice modelu domeny dla każdej mikrousługi</span><span class="sxs-lookup"><span data-stu-id="c061f-103">Identify domain-model boundaries for each microservice</span></span>

<span data-ttu-id="c061f-104">Celem określania granic i rozmiaru modelu dla każdej mikrousługi nie jest uzyskanie bardziej szczegółowego rozdzielenia, chociaż jest to możliwe w przypadku małych mikrousług.</span><span class="sxs-lookup"><span data-stu-id="c061f-104">The goal when identifying model boundaries and size for each microservice isn't to get to the most granular separation possible, although you should tend toward small microservices if possible.</span></span> <span data-ttu-id="c061f-105">Zamiast tego należy zapoznać się z najważniejszym rozdzieleniem podanym przez wiedzę o domenie.</span><span class="sxs-lookup"><span data-stu-id="c061f-105">Instead, your goal should be to get to the most meaningful separation guided by your domain knowledge.</span></span> <span data-ttu-id="c061f-106">Ten nacisk nie jest rozmiarem, ale zamiast możliwości biznesowe.</span><span class="sxs-lookup"><span data-stu-id="c061f-106">The emphasis isn't on the size, but instead on business capabilities.</span></span> <span data-ttu-id="c061f-107">Ponadto, jeśli istnieje wyraźna spójność dla pewnego obszaru aplikacji w oparciu o dużą liczbę zależności, która wskazuje potrzebę tylko jednego mikrousługi.</span><span class="sxs-lookup"><span data-stu-id="c061f-107">In addition, if there's clear cohesion needed for a certain area of the application based on a high number of dependencies, that indicates the need for a single microservice, too.</span></span> <span data-ttu-id="c061f-108">Spójność to sposób, aby określić, jak należy rozdzielić lub zgrupować wspólnie mikrousługi.</span><span class="sxs-lookup"><span data-stu-id="c061f-108">Cohesion is a way to identify how to break apart or group together microservices.</span></span> <span data-ttu-id="c061f-109">Ostatecznie, podczas gdy uzyskasz więcej informacji na temat domeny, należy dostosować rozmiar mikrousługi, iteracyjnie.</span><span class="sxs-lookup"><span data-stu-id="c061f-109">Ultimately, while you gain more knowledge about the domain, you should adapt the size of your microservice, iteratively.</span></span> <span data-ttu-id="c061f-110">Znalezienie odpowiedniego rozmiaru nie jest procesem z jednym zrzutem.</span><span class="sxs-lookup"><span data-stu-id="c061f-110">Finding the right size isn't a one-shot process.</span></span>

<span data-ttu-id="c061f-111">[Sam Newmana](https://samnewman.io/), rozpoznany podwyższanie poziomu mikrousług i autor [tworzenia mikrousług](https://samnewman.io/books/building_microservices/)w książce, oznacza, że należy zaprojektować mikrousługi na podstawie wzorca ograniczone kontekstu (BC) (część projektu opartego na domenie), jak to zostało wprowadzone. wyżej.</span><span class="sxs-lookup"><span data-stu-id="c061f-111">[Sam Newman](https://samnewman.io/), a recognized promoter of microservices and author of the book [Building Microservices](https://samnewman.io/books/building_microservices/), highlights that you should design your microservices based on the Bounded Context (BC) pattern (part of domain-driven design), as introduced earlier.</span></span> <span data-ttu-id="c061f-112">Czasami może składać się z kilku usług fizycznych, ale nie odwrotnie.</span><span class="sxs-lookup"><span data-stu-id="c061f-112">Sometimes, a BC could be composed of several physical services, but not vice versa.</span></span>

<span data-ttu-id="c061f-113">Model domeny z określonymi jednostkami domeny ma zastosowanie w ramach konkretnej BC lub mikrousług.</span><span class="sxs-lookup"><span data-stu-id="c061f-113">A domain model with specific domain entities applies within a concrete BC or microservice.</span></span> <span data-ttu-id="c061f-114">Funkcja BC ogranicza możliwość zastosowania modelu domeny i zapewnia członkom zespołu deweloperów jasne i wspólne zrozumienie, co musi być spójne i co może być opracowane niezależnie.</span><span class="sxs-lookup"><span data-stu-id="c061f-114">A BC delimits the applicability of a domain model and gives developer team members a clear and shared understanding of what must be cohesive and what can be developed independently.</span></span> <span data-ttu-id="c061f-115">Są to te same cele dla mikrousług.</span><span class="sxs-lookup"><span data-stu-id="c061f-115">These are the same goals for microservices.</span></span>

<span data-ttu-id="c061f-116">Innym narzędziem, które informuje o wyborze projektu, jest [Conways](https://en.wikipedia.org/wiki/Conway%27s_law), który stwierdza, że aplikacja będzie odzwierciedlać granice społecznościowe organizacji, która go wygenerowała.</span><span class="sxs-lookup"><span data-stu-id="c061f-116">Another tool that informs your design choice is [Conway's law](https://en.wikipedia.org/wiki/Conway%27s_law), which states that an application will reflect the social boundaries of the organization that produced it.</span></span> <span data-ttu-id="c061f-117">Jednak czasami przeciwieństwem jest wartość true — organizacja firmy jest tworzona przez oprogramowanie.</span><span class="sxs-lookup"><span data-stu-id="c061f-117">But sometimes the opposite is true -the company's organization is formed by the software.</span></span> <span data-ttu-id="c061f-118">Może być konieczne odwrócenie prawa Conways i skompilowanie granic w taki sposób, w jaki ma być zorganizowana firma, a tym samym do konsultacji między procesami biznesowymi.</span><span class="sxs-lookup"><span data-stu-id="c061f-118">You might need to reverse Conway's law and build the boundaries the way you want the company to be organized, leaning toward business process consulting.</span></span>

<span data-ttu-id="c061f-119">Aby zidentyfikować konteksty ograniczone, można użyć deseniu DDD o nazwie [wzorzec mapowania kontekstu](https://www.infoq.com/articles/ddd-contextmapping).</span><span class="sxs-lookup"><span data-stu-id="c061f-119">To identify bounded contexts, you can use a DDD pattern called the [Context Mapping pattern](https://www.infoq.com/articles/ddd-contextmapping).</span></span> <span data-ttu-id="c061f-120">Mapowanie kontekstu pozwala identyfikować różne konteksty w aplikacji i ich granice.</span><span class="sxs-lookup"><span data-stu-id="c061f-120">With Context Mapping, you identify the various contexts in the application and their boundaries.</span></span> <span data-ttu-id="c061f-121">Często istnieją różne konteksty i granice dla każdego małego podsystemu, na przykład.</span><span class="sxs-lookup"><span data-stu-id="c061f-121">It's common to have a different context and boundary for each small subsystem, for instance.</span></span> <span data-ttu-id="c061f-122">Mapowanie kontekstu jest sposobem definiowania i określania jawnych granic między domenami.</span><span class="sxs-lookup"><span data-stu-id="c061f-122">The Context Map is a way to define and make explicit those boundaries between domains.</span></span> <span data-ttu-id="c061f-123">BC jest autonomiczna i zawiera szczegółowe informacje o pojedynczej domenie — szczegóły, takie jak jednostki domeny i definiuje kontrakty integracji z innymi usługami łączności biznesowej.</span><span class="sxs-lookup"><span data-stu-id="c061f-123">A BC is autonomous and includes the details of a single domain -details like the domain entities- and defines integration contracts with other BCs.</span></span> <span data-ttu-id="c061f-124">Jest to podobne do definicji mikrousługi: jest autonomiczna, implementuje pewne możliwości domeny i musi udostępniać interfejsy.</span><span class="sxs-lookup"><span data-stu-id="c061f-124">This is similar to the definition of a microservice: it's autonomous, it implements certain domain capability, and it must provide interfaces.</span></span> <span data-ttu-id="c061f-125">Dzieje się tak dlatego, że mapowanie kontekstu i powiązane wzorce kontekstu są dobrym podejściem do identyfikowania granic modelu domeny mikrousług.</span><span class="sxs-lookup"><span data-stu-id="c061f-125">This is why Context Mapping and the Bounded Context pattern are good approaches for identifying the domain model boundaries of your microservices.</span></span>

<span data-ttu-id="c061f-126">Podczas projektowania dużej aplikacji zobaczysz, jak jej model domeny może być pofragmentowany — ekspert domeny z domeny wykazu będzie określać jednostki jako inaczej w katalogu i domenach spisu niż na przykład dla eksperta domeny wysyłki.</span><span class="sxs-lookup"><span data-stu-id="c061f-126">When designing a large application, you'll see how its domain model can be fragmented - a domain expert from the catalog domain will name entities differently in the catalog and inventory domains than a shipping domain expert, for instance.</span></span> <span data-ttu-id="c061f-127">Lub jednostka domeny użytkownika może być różna od rozmiaru i liczby atrybutów podczas pracy z ekspertem programu CRM, który chce przechowywać wszystkie szczegółowe informacje o kliencie, niż w przypadku podmiotu zamawiającego domeny, który po prostu potrzebuje danych częściowych dotyczących klienta.</span><span class="sxs-lookup"><span data-stu-id="c061f-127">Or the user domain entity might be different in size and number of attributes when dealing with a CRM expert who wants to store every detail about the customer than for an ordering domain expert who just needs partial data about the customer.</span></span> <span data-ttu-id="c061f-128">Bardzo trudno jest odróżnić wszystkie warunki domeny dla wszystkich domen związanych z dużą aplikacją.</span><span class="sxs-lookup"><span data-stu-id="c061f-128">It's very hard to disambiguate all domain terms across all the domains related to a large application.</span></span> <span data-ttu-id="c061f-129">Jednak najważniejsze jest, że nie należy próbować ujednolicić warunków.</span><span class="sxs-lookup"><span data-stu-id="c061f-129">But the most important thing is that you shouldn't try to unify the terms.</span></span> <span data-ttu-id="c061f-130">Zamiast tego należy zaakceptować różnice i rozbudowaność zapewnioną przez poszczególne domeny.</span><span class="sxs-lookup"><span data-stu-id="c061f-130">Instead, accept the differences and richness provided by each domain.</span></span> <span data-ttu-id="c061f-131">Jeśli spróbujesz korzystać z ujednoliconej bazy danych dla całej aplikacji, próby w ujednoliconym słownictwie będą niewygodna i nie będą miały dostępu bezpośrednio do żadnego z wielu ekspertów domeny.</span><span class="sxs-lookup"><span data-stu-id="c061f-131">If you try to have a unified database for the whole application, attempts at a unified vocabulary will be awkward and won't sound right to any of the multiple domain experts.</span></span> <span data-ttu-id="c061f-132">W związku z tym usługa BCs (zaimplementowana jako mikrousługi) pomoże w wyjaśnieniu, gdzie można używać pewnych warunków domeny i gdzie należy podzielić system i utworzyć dodatkowe usługi łączności biznesowej z różnymi domenami.</span><span class="sxs-lookup"><span data-stu-id="c061f-132">Therefore, BCs (implemented as microservices) will help you to clarify where you can use certain domain terms and where you'll need to split the system and create additional BCs with different domains.</span></span>

<span data-ttu-id="c061f-133">Wiadomo, że masz odpowiednie granice i rozmiary każdego modelu BC i domeny, jeśli masz kilka silnych relacji między modelami domen i nie musisz zwykle scalać informacji z wielu modeli domen podczas wykonywania typowych operacji aplikacji .</span><span class="sxs-lookup"><span data-stu-id="c061f-133">You'll know that you got the right boundaries and sizes of each BC and domain model if you have few strong relationships between domain models, and you do not usually need to merge information from multiple domain models when performing typical application operations.</span></span>

<span data-ttu-id="c061f-134">Prawdopodobnie najlepszą odpowiedzią na pytanie, jak duży model domeny dla każdej mikrousługi powinien być następujący: powinien mieć autonomiczną metodę BC, jak to możliwe, która pozwala na działanie bez konieczności ciągłego przełączania się do innych kontekstów (innych modele mikrousług).</span><span class="sxs-lookup"><span data-stu-id="c061f-134">Perhaps the best answer to the question of how large a domain model for each microservice should be is the following: it should have an autonomous BC, as isolated as possible, that enables you to work without having to constantly switch to other contexts (other microservice's models).</span></span> <span data-ttu-id="c061f-135">Na rysunku 4-10 można zobaczyć, jak wiele mikrousług (wiele BCs) ma własny model i jak można definiować ich jednostki, w zależności od określonych wymagań dla każdej z określonych domen w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c061f-135">In Figure 4-10, you can see how multiple microservices (multiple BCs) each has their own model and how their entities can be defined, depending on the specific requirements for each of the identified domains in your application.</span></span>

![Jednostki w kilku granicach modelu (powiązane konteksty), w których ta sama jednostka jest wyświetlana jako "Users", "Kupcs", "Payers" i "Customers" w zależności od powiązanego kontekstu](./media/image10.png)

<span data-ttu-id="c061f-137">**Rysunek 4-10**.</span><span class="sxs-lookup"><span data-stu-id="c061f-137">**Figure 4-10**.</span></span> <span data-ttu-id="c061f-138">Identyfikowanie jednostek i granic modelu mikrousług</span><span class="sxs-lookup"><span data-stu-id="c061f-138">Identifying entities and microservice model boundaries</span></span>

<span data-ttu-id="c061f-139">Rysunek 4-10 ilustruje przykładowy scenariusz związany z systemem zarządzania konferencją online.</span><span class="sxs-lookup"><span data-stu-id="c061f-139">Figure 4-10 illustrates a sample scenario related to an online conference management system.</span></span> <span data-ttu-id="c061f-140">Zidentyfikowano kilka usług BCs, które mogą być zaimplementowane jako mikrousługi, na podstawie domen zdefiniowanych dla Ciebie przez ekspertów domeny.</span><span class="sxs-lookup"><span data-stu-id="c061f-140">You've identified several BCs that could be implemented as microservices, based on domains that domain experts defined for you.</span></span> <span data-ttu-id="c061f-141">Jak widać, istnieją jednostki, które znajdują się tylko w jednym modelu mikrousług, np. w przypadku płatności w mikrousłudze.</span><span class="sxs-lookup"><span data-stu-id="c061f-141">As you can see, there are entities that are present just in a single microservice model, like Payments in the Payment microservice.</span></span> <span data-ttu-id="c061f-142">Ich wdrożenie będzie łatwe.</span><span class="sxs-lookup"><span data-stu-id="c061f-142">Those will be easy to implement.</span></span>

<span data-ttu-id="c061f-143">Można jednak również mieć jednostki o innym kształcie, ale współużytkować tę samą tożsamość w modelach wielu domen z wielu mikrousług.</span><span class="sxs-lookup"><span data-stu-id="c061f-143">However, you might also have entities that have a different shape but share the same identity across the multiple domain models from the multiple microservices.</span></span> <span data-ttu-id="c061f-144">Na przykład jednostka użytkownika jest identyfikowana w mikrousłudze konferencji do zarządzania.</span><span class="sxs-lookup"><span data-stu-id="c061f-144">For example, the User entity is identified in the Conferences Management microservice.</span></span> <span data-ttu-id="c061f-145">Ten sam użytkownik, o tej samej tożsamości, jest jednym z nazwanymi kupującymi w mikrousłudze porządkowania lub jeden nazwany płatnika w mikrousłudze płatniczej, a nawet jeden nazwany klient w mikrousłudze klienta.</span><span class="sxs-lookup"><span data-stu-id="c061f-145">That same user, with the same identity, is the one named Buyers in the Ordering microservice, or the one named Payer in the Payment microservice, and even the one named Customer in the Customer Service microservice.</span></span> <span data-ttu-id="c061f-146">Wynika to z faktu, że w zależności od [języka powszechnie](https://martinfowler.com/bliki/UbiquitousLanguage.html) używanego przez każdego eksperta domeny użytkownik może mieć inną perspektywę nawet z innymi atrybutami.</span><span class="sxs-lookup"><span data-stu-id="c061f-146">This is because, depending on the [ubiquitous language](https://martinfowler.com/bliki/UbiquitousLanguage.html) that each domain expert is using, a user might have a different perspective even with different attributes.</span></span> <span data-ttu-id="c061f-147">Jednostka użytkownika w modelu mikrousług o nazwie Zarządzanie konferencjami może mieć większość prywatnych atrybutów danych.</span><span class="sxs-lookup"><span data-stu-id="c061f-147">The user entity in the microservice model named Conferences Management might have most of its personal data attributes.</span></span> <span data-ttu-id="c061f-148">Jednak ten sam użytkownik w kształcie płatnika w płatności mikrousług lub w kształcie klienta w usłudze mikrousług klienta może nie potrzebować tej samej listy atrybutów.</span><span class="sxs-lookup"><span data-stu-id="c061f-148">However, that same user in the shape of Payer in the microservice Payment or in the shape of Customer in the microservice Customer Service might not need the same list of attributes.</span></span>

<span data-ttu-id="c061f-149">Podobne podejście przedstawiono na rysunku 4-11.</span><span class="sxs-lookup"><span data-stu-id="c061f-149">A similar approach is illustrated in Figure 4-11.</span></span>

![Podczas deredagowania tradycyjnego modelu danych między ograniczonymi kontekstami można mieć różne jednostki, które współużytkują tę samą tożsamość (jest to również użytkownik) z innymi atrybutami w każdym związanym kontekście.](./media/image11.png)

<span data-ttu-id="c061f-151">**Rysunek 4-11**.</span><span class="sxs-lookup"><span data-stu-id="c061f-151">**Figure 4-11**.</span></span> <span data-ttu-id="c061f-152">Tworzenie tradycyjnych modeli danych w wielu modelach domen</span><span class="sxs-lookup"><span data-stu-id="c061f-152">Decomposing traditional data models into multiple domain models</span></span>

<span data-ttu-id="c061f-153">Aby zobaczyć, jak użytkownik jest obecny w modelu mikrousług zarządzania konferencjami jako podmiot użytkownika i jest również obecny w formie jednostki kupca w mikrousłudze cenowej, z alternatywnymi atrybutami lub szczegółami dotyczącymi użytkownika, gdy jest on rzeczywiście nabywcą.</span><span class="sxs-lookup"><span data-stu-id="c061f-153">You can see how the user is present in the Conferences Management microservice model as the User entity and is also present in the form of the Buyer entity in the Pricing microservice, with alternate attributes or details about the user when it's actually a buyer.</span></span> <span data-ttu-id="c061f-154">Każda mikrousługa lub BC może nie potrzebować wszystkich danych związanych z jednostką użytkownika, w zależności od problemu do rozwiązania lub kontekstu.</span><span class="sxs-lookup"><span data-stu-id="c061f-154">Each microservice or BC might not need all the data related to a User entity, just part of it, depending on the problem to solve or the context.</span></span> <span data-ttu-id="c061f-155">Na przykład w modelu mikrousług cenowych nie jest potrzebny adres ani nazwa użytkownika, tylko identyfikator (tożsamość) i stan, które będą miały wpływ na rabaty w przypadku, gdy ceny są dostępne dla każdego nabywcy.</span><span class="sxs-lookup"><span data-stu-id="c061f-155">For instance, in the Pricing microservice model, you do not need the address or the name of the user, just the ID (as identity) and Status, which will have an impact on discounts when pricing the seats per buyer.</span></span>

<span data-ttu-id="c061f-156">Jednostka stanowiska ma taką samą nazwę, ale różne atrybuty w każdym modelu domeny.</span><span class="sxs-lookup"><span data-stu-id="c061f-156">The Seat entity has the same name but different attributes in each domain model.</span></span> <span data-ttu-id="c061f-157">Jednak stanowisko ma tożsamość na podstawie tego samego identyfikatora, co dzieje się z użytkownikami i nabywcą.</span><span class="sxs-lookup"><span data-stu-id="c061f-157">However, Seat shares identity based on the same ID, as happens with User and Buyer.</span></span>

<span data-ttu-id="c061f-158">Zasadniczo istnieje współdzielona koncepcja użytkownika, która istnieje w wielu usługach (domenach), które współużytkują tożsamość tego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c061f-158">Basically, there's a shared concept of a user that exists in multiple services (domains), which all share the identity of that user.</span></span> <span data-ttu-id="c061f-159">Jednak w każdym modelu domeny mogą istnieć dodatkowe lub inne szczegóły dotyczące jednostki użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c061f-159">But in each domain model there might be additional or different details about the user entity.</span></span> <span data-ttu-id="c061f-160">W związku z tym musi być sposobem na mapowanie jednostki użytkownika z jednej domeny (mikrousługi) na inną.</span><span class="sxs-lookup"><span data-stu-id="c061f-160">Therefore, there needs to be a way to map a user entity from one domain (microservice) to another.</span></span>

<span data-ttu-id="c061f-161">Istnieje kilka korzyści, aby nie współużytkować tej samej jednostki użytkownika z tą samą liczbą atrybutów w różnych domenach.</span><span class="sxs-lookup"><span data-stu-id="c061f-161">There are several benefits to not sharing the same user entity with the same number of attributes across domains.</span></span> <span data-ttu-id="c061f-162">Jedną z korzyści jest zredukowanie poziomu duplikowania, dzięki czemu modele mikrousług nie mają żadnych niepotrzebnych danych.</span><span class="sxs-lookup"><span data-stu-id="c061f-162">One benefit is to reduce duplication, so that microservice models do not have any data that they do not need.</span></span> <span data-ttu-id="c061f-163">Kolejną zaletą jest posiadanie mikrousługi, która jest właścicielem pewnego typu danych na jednostkę, tak aby aktualizacje i zapytania dla tego typu danych były sterowane tylko przez tę mikrousługę.</span><span class="sxs-lookup"><span data-stu-id="c061f-163">Another benefit is having a master microservice that owns a certain type of data per entity so that updates and queries for that type of data are driven only by that microservice.</span></span>

>[!div class="step-by-step"]
><span data-ttu-id="c061f-164">[Poprzedni](distributed-data-management.md)Następny
>[](direct-client-to-microservice-communication-versus-the-api-gateway-pattern.md)</span><span class="sxs-lookup"><span data-stu-id="c061f-164">[Previous](distributed-data-management.md)
[Next](direct-client-to-microservice-communication-versus-the-api-gateway-pattern.md)</span></span>