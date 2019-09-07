---
title: Asynchroniczna komunikacja oparta na komunikatach
description: Architektura mikrousług platformy .NET dla aplikacji platformy .NET w kontenerze | Asynchroniczna komunikacja oparta na komunikatach to podstawowe koncepcje w architekturze mikrousług, ponieważ jest to najlepszy sposób, aby mikrousługi były niezależne od siebie, a także ostatecznie zsynchronizowane.
ms.date: 09/20/2018
ms.openlocfilehash: 65bd0cd2b316fe7011ad8e878852547ee5949f09
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/30/2019
ms.locfileid: "70295573"
---
# <a name="asynchronous-message-based-communication"></a><span data-ttu-id="8b0e5-103">Asynchroniczna komunikacja oparta na komunikatach</span><span class="sxs-lookup"><span data-stu-id="8b0e5-103">Asynchronous message-based communication</span></span>

<span data-ttu-id="8b0e5-104">Asynchroniczne komunikaty i komunikacja sterowane zdarzeniami są kluczowe, gdy propagowanie zmian w wielu mikrousługach i związanych z nimi modelach domen.</span><span class="sxs-lookup"><span data-stu-id="8b0e5-104">Asynchronous messaging and event-driven communication are critical when propagating changes across multiple microservices and their related domain models.</span></span> <span data-ttu-id="8b0e5-105">Jak wspomniano wcześniej w przypadku mikrousług dyskusji i ograniczonych kontekstów (BCs), modele (użytkownik, klient, produkt, konto itp.) mogą oznaczać różne rzeczy dla różnych mikrousług lub usług łączności biznesowej.</span><span class="sxs-lookup"><span data-stu-id="8b0e5-105">As mentioned earlier in the discussion microservices and Bounded Contexts (BCs), models (User, Customer, Product, Account, etc.) can mean different things to different microservices or BCs.</span></span> <span data-ttu-id="8b0e5-106">Oznacza to, że gdy wystąpią zmiany, potrzebny jest jakiś sposób uzgadniania zmian w różnych modelach.</span><span class="sxs-lookup"><span data-stu-id="8b0e5-106">That means that when changes occur, you need some way to reconcile changes across the different models.</span></span> <span data-ttu-id="8b0e5-107">Rozwiązanie to spójność ostateczna i komunikacja oparta na zdarzeniach na podstawie asynchronicznych komunikatów.</span><span class="sxs-lookup"><span data-stu-id="8b0e5-107">A solution is eventual consistency and event-driven communication based on asynchronous messaging.</span></span>

<span data-ttu-id="8b0e5-108">W przypadku korzystania z komunikatów procesy komunikują się przez wymianę komunikatów asynchronicznie.</span><span class="sxs-lookup"><span data-stu-id="8b0e5-108">When using messaging, processes communicate by exchanging messages asynchronously.</span></span> <span data-ttu-id="8b0e5-109">Klient wykonuje polecenie lub żądanie do usługi, wysyłając do niego wiadomość.</span><span class="sxs-lookup"><span data-stu-id="8b0e5-109">A client makes a command or a request to a service by sending it a message.</span></span> <span data-ttu-id="8b0e5-110">Jeśli usługa musi odpowiedzieć, wysyła do klienta inny komunikat z powrotem.</span><span class="sxs-lookup"><span data-stu-id="8b0e5-110">If the service needs to reply, it sends a different message back to the client.</span></span> <span data-ttu-id="8b0e5-111">Ponieważ jest to komunikacja oparta na komunikatach, klient zakłada, że odpowiedź nie zostanie natychmiast odebrana, a w ogóle może nie mieć odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="8b0e5-111">Since it's a message-based communication, the client assumes that the reply won't be received immediately, and that there might be no response at all.</span></span>

<span data-ttu-id="8b0e5-112">Komunikat składa się z nagłówka (metadane, takie jak identyfikacja lub informacje o zabezpieczeniach) i treść.</span><span class="sxs-lookup"><span data-stu-id="8b0e5-112">A message is composed by a header (metadata such as identification or security information) and a body.</span></span> <span data-ttu-id="8b0e5-113">Komunikaty są zwykle wysyłane za poorednictwem protokołów asynchronicznych, takich jak AMQP.</span><span class="sxs-lookup"><span data-stu-id="8b0e5-113">Messages are usually sent through asynchronous protocols like AMQP.</span></span>

<span data-ttu-id="8b0e5-114">Preferowaną infrastrukturą dla tego typu komunikacji w społeczności mikrousług jest lekki Broker komunikatów, który jest inny niż w przypadku dużych brokerów i koordynatorów używanych w ramach SOA.</span><span class="sxs-lookup"><span data-stu-id="8b0e5-114">The preferred infrastructure for this type of communication in the microservices community is a lightweight message broker, which is different than the large brokers and orchestrators used in SOA.</span></span> <span data-ttu-id="8b0e5-115">W lekkim brokerze komunikatów infrastruktura jest zazwyczaj "Dumb", działającą tylko jako Broker komunikatów, z prostymi implementacjami, takimi jak RabbitMQ, lub skalowalną magistralą usług w chmurze, taką jak Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="8b0e5-115">In a lightweight message broker, the infrastructure is typically "dumb," acting only as a message broker, with simple implementations such as RabbitMQ or a scalable service bus in the cloud like Azure Service Bus.</span></span> <span data-ttu-id="8b0e5-116">W tym scenariuszu większość "inteligentnych" myśli nadal przebywa w punktach końcowych, które produkują i zużywają komunikaty, czyli w mikrousługach.</span><span class="sxs-lookup"><span data-stu-id="8b0e5-116">In this scenario, most of the "smart" thinking still lives in the endpoints that are producing and consuming messages-that is, in the microservices.</span></span>

<span data-ttu-id="8b0e5-117">Kolejną regułą, jaką należy wykonać, tak jak to możliwe, jest użycie tylko asynchronicznych komunikatów między usługami wewnętrznymi i użycie synchronicznej komunikacji (na przykład HTTP) tylko z aplikacji klienckich do usług frontonu (bramy interfejsu API i pierwszy poziom mikrousług).</span><span class="sxs-lookup"><span data-stu-id="8b0e5-117">Another rule you should try to follow, as much as possible, is to use only asynchronous messaging between the internal services, and to use synchronous communication (such as HTTP) only from the client apps to the front-end services (API Gateways plus the first level of microservices).</span></span>

<span data-ttu-id="8b0e5-118">Istnieją dwa rodzaje asynchronicznej komunikacji komunikatów: komunikacja oparta na komunikatach o pojedynczym odbiorniku i komunikacja oparta na komunikatach.</span><span class="sxs-lookup"><span data-stu-id="8b0e5-118">There are two kinds of asynchronous messaging communication: single receiver message-based communication, and multiple receivers message-based communication.</span></span> <span data-ttu-id="8b0e5-119">W poniższych sekcjach znajdują się szczegółowe informacje o nich.</span><span class="sxs-lookup"><span data-stu-id="8b0e5-119">The following sections provide details about them.</span></span>

## <a name="single-receiver-message-based-communication"></a><span data-ttu-id="8b0e5-120">Komunikacja oparta na komunikatach pojedynczego odbiorcy</span><span class="sxs-lookup"><span data-stu-id="8b0e5-120">Single-receiver message-based communication</span></span>

<span data-ttu-id="8b0e5-121">Komunikacja asynchroniczna oparta na komunikatach z pojedynczym odbiornikiem oznacza komunikację typu punkt-punkt, która dostarcza komunikat do dokładnie jednego z odbiorców, który odczytuje z kanału, i że komunikat jest przetwarzany tylko raz.</span><span class="sxs-lookup"><span data-stu-id="8b0e5-121">Message-based asynchronous communication with a single receiver means there's point-to-point communication that delivers a message to exactly one of the consumers that's reading from the channel, and that the message is processed just once.</span></span> <span data-ttu-id="8b0e5-122">Istnieją jednak specjalne sytuacje.</span><span class="sxs-lookup"><span data-stu-id="8b0e5-122">However, there are special situations.</span></span> <span data-ttu-id="8b0e5-123">Na przykład w systemie w chmurze, który próbuje automatycznie odzyskać sprawność po awarii, ten sam komunikat może być wysyłany wiele razy.</span><span class="sxs-lookup"><span data-stu-id="8b0e5-123">For instance, in a cloud system that tries to automatically recover from failures, the same message could be sent multiple times.</span></span> <span data-ttu-id="8b0e5-124">Ze względu na sieć lub inne błędy, klient musi być w stanie ponowić próbę wysłania wiadomości, a serwer musi zaimplementować operację do idempotentne w celu przetworzenia konkretnego komunikatu tylko raz.</span><span class="sxs-lookup"><span data-stu-id="8b0e5-124">Due to network or other failures, the client has to be able to retry sending messages, and the server has to implement an operation to be idempotent in order to process a particular message just once.</span></span>

<span data-ttu-id="8b0e5-125">Komunikacja oparta na komunikatach pojedynczego odbiorcy jest szczególnie przydatna w przypadku wysyłania poleceń asynchronicznych z jednej mikrousługi do innej, jak pokazano na rysunku 4-18, który ilustruje to podejście.</span><span class="sxs-lookup"><span data-stu-id="8b0e5-125">Single-receiver message-based communication is especially well suited for sending asynchronous commands from one microservice to another as shown in Figure 4-18 that illustrates this approach.</span></span>

<span data-ttu-id="8b0e5-126">Po rozpoczęciu wysyłania komunikacji opartej na komunikatach (z poleceniami lub zdarzeniami) należy unikać mieszania komunikacji opartej na komunikatach z synchroniczną komunikacją protokołu HTTP.</span><span class="sxs-lookup"><span data-stu-id="8b0e5-126">Once you start sending message-based communication (either with commands or events), you should avoid mixing message-based communication with synchronous HTTP communication.</span></span>

![Jedna mikrousługa otrzymująca komunikat asynchroniczny](./media/image18.png)

<span data-ttu-id="8b0e5-128">**Rysunek 4-18**.</span><span class="sxs-lookup"><span data-stu-id="8b0e5-128">**Figure 4-18**.</span></span> <span data-ttu-id="8b0e5-129">Jedna mikrousługa otrzymująca komunikat asynchroniczny</span><span class="sxs-lookup"><span data-stu-id="8b0e5-129">A single microservice receiving an asynchronous message</span></span>

<span data-ttu-id="8b0e5-130">Należy pamiętać, że gdy polecenia pochodzą z aplikacji klienckich, można je zaimplementować jako polecenia synchroniczne HTTP.</span><span class="sxs-lookup"><span data-stu-id="8b0e5-130">Note that when the commands come from client applications, they can be implemented as HTTP synchronous commands.</span></span> <span data-ttu-id="8b0e5-131">Należy używać poleceń opartych na komunikatach, gdy potrzebna jest wyższa skalowalność lub jeśli już jesteś w procesie biznesowym opartym na komunikatach.</span><span class="sxs-lookup"><span data-stu-id="8b0e5-131">You should use message-based commands when you need higher scalability or when you're already in a message-based business process.</span></span>

## <a name="multiple-receivers-message-based-communication"></a><span data-ttu-id="8b0e5-132">Komunikacja oparta na komunikatach wielu odbiorników</span><span class="sxs-lookup"><span data-stu-id="8b0e5-132">Multiple-receivers message-based communication</span></span>

<span data-ttu-id="8b0e5-133">Bardziej elastyczne podejście może również wymagać użycia mechanizmu publikowania/subskrybowania, aby komunikacja od nadawcy była dostępna dla dodatkowych mikrousług subskrybentów lub aplikacji zewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="8b0e5-133">As a more flexible approach, you might also want to use a publish/subscribe mechanism so that your communication from the sender will be available to additional subscriber microservices or to external applications.</span></span> <span data-ttu-id="8b0e5-134">Z tego względu pomaga to postępować zgodnie z [zasadą otwierania/zamykania](https://en.wikipedia.org/wiki/Open/closed_principle) w usłudze wysyłającej.</span><span class="sxs-lookup"><span data-stu-id="8b0e5-134">Thus, it helps you to follow the [open/closed principle](https://en.wikipedia.org/wiki/Open/closed_principle) in the sending service.</span></span> <span data-ttu-id="8b0e5-135">Dzięki temu dodatkowi Subskrybenci mogą zostać dodani w przyszłości bez konieczności modyfikowania usługi nadawcy.</span><span class="sxs-lookup"><span data-stu-id="8b0e5-135">That way, additional subscribers can be added in the future without the need to modify the sender service.</span></span>

<span data-ttu-id="8b0e5-136">W przypadku korzystania z komunikacji publikowania/subskrybowania można używać interfejsu usługi Event bus do publikowania zdarzeń na dowolnym subskrybencie.</span><span class="sxs-lookup"><span data-stu-id="8b0e5-136">When you use a publish/subscribe communication, you might be using an event bus interface to publish events to any subscriber.</span></span>

## <a name="asynchronous-event-driven-communication"></a><span data-ttu-id="8b0e5-137">Asynchroniczna komunikacja oparta na zdarzeniach</span><span class="sxs-lookup"><span data-stu-id="8b0e5-137">Asynchronous event-driven communication</span></span>

<span data-ttu-id="8b0e5-138">W przypadku korzystania z asynchronicznej komunikacji opartej na zdarzeniach mikrousługa publikuje zdarzenie integracji, gdy coś się dzieje w swojej domenie, a inna mikrousługa musi mieć do niej świadomość, na przykład zmianę cen w mikrousłudze katalogu produktów.</span><span class="sxs-lookup"><span data-stu-id="8b0e5-138">When using asynchronous event-driven communication, a microservice publishes an integration event when something happens within its domain and another microservice needs to be aware of it, like a price change in a product catalog microservice.</span></span> <span data-ttu-id="8b0e5-139">Dodatkowe mikrousługi subskrybują zdarzenia, aby mogli je odbierać asynchronicznie.</span><span class="sxs-lookup"><span data-stu-id="8b0e5-139">Additional microservices subscribe to the events so they can receive them asynchronously.</span></span> <span data-ttu-id="8b0e5-140">W takim przypadku odbiorcy mogą zaktualizować swoje jednostki domeny, co może spowodować opublikowanie większej liczby zdarzeń integracji.</span><span class="sxs-lookup"><span data-stu-id="8b0e5-140">When that happens, the receivers might update their own domain entities, which can cause more integration events to be published.</span></span> <span data-ttu-id="8b0e5-141">Ten system publikowania/subskrybowania jest zwykle wykonywany przy użyciu implementacji magistrali zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="8b0e5-141">This publish/subscribe system is usually performed by using an implementation of an event bus.</span></span> <span data-ttu-id="8b0e5-142">Magistrala zdarzeń może być zaprojektowana jako Abstrakcja lub interfejs, z interfejsem API, który jest wymagany do subskrybowania lub anulowania subskrypcji zdarzeń oraz do publikowania zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="8b0e5-142">The event bus can be designed as an abstraction or interface, with the API that's needed to subscribe or unsubscribe to events and to publish events.</span></span> <span data-ttu-id="8b0e5-143">Magistrala zdarzeń może również mieć co najmniej jedną implementację opartą na dowolnym procesie i brokerze obsługi komunikatów, takim jak kolejka komunikatów lub Usługa Service Bus, która obsługuje komunikację asynchroniczną i model publikowania/subskrybowania.</span><span class="sxs-lookup"><span data-stu-id="8b0e5-143">The event bus can also have one or more implementations based on any inter-process and messaging broker, like a messaging queue or service bus that supports asynchronous communication and a publish/subscribe model.</span></span>

<span data-ttu-id="8b0e5-144">Jeśli system używa spójności ostatecznej opartej na zdarzeniach integracji, zaleca się, aby to podejście było całkowicie jasne dla użytkownika końcowego.</span><span class="sxs-lookup"><span data-stu-id="8b0e5-144">If a system uses eventual consistency driven by integration events, it's recommended that this approach is made completely clear to the end user.</span></span> <span data-ttu-id="8b0e5-145">System nie powinien używać podejścia, które śladuje zdarzenia integracji, takie jak sygnalizujące lub systemy sondowania od klienta.</span><span class="sxs-lookup"><span data-stu-id="8b0e5-145">The system shouldn't use an approach that mimics integration events, like SignalR or polling systems from the client.</span></span> <span data-ttu-id="8b0e5-146">Użytkownik końcowy i właściciel biznesowy muszą jawnie wdrożyć w systemie spójność ostateczną i pamiętać, że w wielu przypadkach firma nie ma żadnego problemu z tym podejściem, o ile jest to jawne.</span><span class="sxs-lookup"><span data-stu-id="8b0e5-146">The end user and the business owner have to explicitly embrace eventual consistency in the system and realize that in many cases the business doesn't have any problem with this approach, as long as it's explicit.</span></span> <span data-ttu-id="8b0e5-147">Jest to ważne, ponieważ użytkownicy mogą od razu zobaczyć niektóre wyniki, co może nie być spowodowane spójnością ostateczną.</span><span class="sxs-lookup"><span data-stu-id="8b0e5-147">This is important because users might expect to see some results immediately and this might not happen with eventual consistency.</span></span>

<span data-ttu-id="8b0e5-148">Jak wspomniano wcześniej w sekcji [wyzwania i rozwiązania dotyczące zarządzania danymi rozproszonymi](distributed-data-management.md) , można użyć zdarzeń integracji w celu zaimplementowania zadań firmowych obejmujących wiele mikrousług.</span><span class="sxs-lookup"><span data-stu-id="8b0e5-148">As noted earlier in the [Challenges and solutions for distributed data management](distributed-data-management.md) section, you can use integration events to implement business tasks that span multiple microservices.</span></span> <span data-ttu-id="8b0e5-149">W ten sposób będziesz mieć ostateczną spójność między tymi usługami.</span><span class="sxs-lookup"><span data-stu-id="8b0e5-149">Thus, you'll have eventual consistency between those services.</span></span> <span data-ttu-id="8b0e5-150">Ostatecznie spójna transakcja składa się z kolekcji rozproszonych akcji.</span><span class="sxs-lookup"><span data-stu-id="8b0e5-150">An eventually consistent transaction is made up of a collection of distributed actions.</span></span> <span data-ttu-id="8b0e5-151">W każdej akcji powiązana mikrousługa aktualizuje jednostkę domeny i publikuje inne zdarzenie integracji, które wywołuje następną akcję w ramach tego samego zadania biznesowego.</span><span class="sxs-lookup"><span data-stu-id="8b0e5-151">At each action, the related microservice updates a domain entity and publishes another integration event that raises the next action within the same end-to-end business task.</span></span>

<span data-ttu-id="8b0e5-152">Ważnym punktem jest to, że możesz chcieć komunikować się z wieloma mikrousługami subskrybowanymi na tym samym zdarzeniu.</span><span class="sxs-lookup"><span data-stu-id="8b0e5-152">An important point is that you might want to communicate to multiple microservices that are subscribed to the same event.</span></span> <span data-ttu-id="8b0e5-153">W tym celu można użyć komunikatów publikowania/subskrybowania na podstawie komunikacji sterowanej zdarzeniami, jak pokazano na rysunku 4-19.</span><span class="sxs-lookup"><span data-stu-id="8b0e5-153">To do so, you can use publish/subscribe messaging based on event-driven communication, as shown in Figure 4-19.</span></span> <span data-ttu-id="8b0e5-154">Ten mechanizm publikowania/subskrybowania nie jest wyłączny dla architektury mikrousług.</span><span class="sxs-lookup"><span data-stu-id="8b0e5-154">This publish/subscribe mechanism isn't exclusive to the microservice architecture.</span></span> <span data-ttu-id="8b0e5-155">Jest to podobne do sposobu, w jaki [ograniczone konteksty](https://martinfowler.com/bliki/BoundedContext.html) w DDD powinny komunikować się, lub w sposób propagowania aktualizacji z bazy danych zapisu do bazy danych odczytu w wzorcu architektury [Command and Query Responsibility Segregation (CQRS)](https://martinfowler.com/bliki/CQRS.html) .</span><span class="sxs-lookup"><span data-stu-id="8b0e5-155">It's similar to the way [Bounded Contexts](https://martinfowler.com/bliki/BoundedContext.html) in DDD should communicate, or to the way you propagate updates from the write database to the read database in the [Command and Query Responsibility Segregation (CQRS)](https://martinfowler.com/bliki/CQRS.html) architecture pattern.</span></span> <span data-ttu-id="8b0e5-156">Celem jest zachowanie spójności ostatecznej między wieloma źródłami danych w systemie rozproszonym.</span><span class="sxs-lookup"><span data-stu-id="8b0e5-156">The goal is to have eventual consistency between multiple data sources across your distributed system.</span></span>

![W przypadku asynchronicznej komunikacji opartej na zdarzeniach jedna mikrousługa publikuje zdarzenia do magistrali zdarzeń, a wiele mikrousług może subskrybować ten element, aby otrzymywać powiadomienia i podejmować działania.](./media/image19.png)

<span data-ttu-id="8b0e5-158">**Rysunek 4-19**.</span><span class="sxs-lookup"><span data-stu-id="8b0e5-158">**Figure 4-19**.</span></span> <span data-ttu-id="8b0e5-159">Asynchroniczna komunikacja komunikatów oparta na zdarzeniach</span><span class="sxs-lookup"><span data-stu-id="8b0e5-159">Asynchronous event-driven message communication</span></span>

<span data-ttu-id="8b0e5-160">Twoja implementacja określi, który protokół ma być używany na potrzeby komunikacji opartej na zdarzeniach.</span><span class="sxs-lookup"><span data-stu-id="8b0e5-160">Your implementation will determine what protocol to use for event-driven, message-based communications.</span></span> <span data-ttu-id="8b0e5-161">[AMQP](https://en.wikipedia.org/wiki/Advanced_Message_Queuing_Protocol) może pomóc w osiągnięciu niezawodnej komunikacji kolejkowanej.</span><span class="sxs-lookup"><span data-stu-id="8b0e5-161">[AMQP](https://en.wikipedia.org/wiki/Advanced_Message_Queuing_Protocol) can help achieve reliable queued communication.</span></span>

<span data-ttu-id="8b0e5-162">Korzystając z magistrali zdarzeń, można użyć poziomu abstrakcji (na przykład interfejsu magistrali zdarzeń) na podstawie powiązanej implementacji w klasach z kodem przy użyciu interfejsu API z brokera komunikatów, takiego jak [RabbitMQ](https://www.rabbitmq.com/) , lub usługi Service Bus, takiej jak [Azure Service Bus z tematami ](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions).</span><span class="sxs-lookup"><span data-stu-id="8b0e5-162">When you use an event bus, you might want to use an abstraction level (like an event bus interface) based on a related implementation in classes with code using the API from a message broker like [RabbitMQ](https://www.rabbitmq.com/) or a service bus like [Azure Service Bus with Topics](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions).</span></span> <span data-ttu-id="8b0e5-163">Alternatywnie możesz chcieć użyć magistrali usług wyższego poziomu, takiej jak NServiceBus, MassTransit lub jaśniejszy, aby ideach swoją magistralę zdarzeń i system publikowania/subskrybowania.</span><span class="sxs-lookup"><span data-stu-id="8b0e5-163">Alternatively, you might want to use a higher-level service bus like NServiceBus, MassTransit, or Brighter to articulate your event bus and publish/subscribe system.</span></span>

## <a name="a-note-about-messaging-technologies-for-production-systems"></a><span data-ttu-id="8b0e5-164">Uwaga dotycząca technologii obsługi komunikatów w systemach produkcyjnych</span><span class="sxs-lookup"><span data-stu-id="8b0e5-164">A note about messaging technologies for production systems</span></span>

<span data-ttu-id="8b0e5-165">Technologie obsługi wiadomości dostępne do wdrożenia abstrakcyjnej magistrali zdarzeń są na różnych poziomach.</span><span class="sxs-lookup"><span data-stu-id="8b0e5-165">The messaging technologies available for implementing your abstract event bus are at different levels.</span></span> <span data-ttu-id="8b0e5-166">Na przykład produkty takie jak RabbitMQ (transport brokera komunikatów) i Azure Service Bus znajdują się na niższym poziomie niż inne produkty, takie jak NServiceBus, MassTransit lub jaśniejszy, które mogą współpracować nad RabbitMQ i Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="8b0e5-166">For instance, products like RabbitMQ (a messaging broker transport) and Azure Service Bus sit at a lower level than other products like, NServiceBus, MassTransit, or Brighter, which can work on top of RabbitMQ and Azure Service Bus.</span></span> <span data-ttu-id="8b0e5-167">Wybór zależy od liczby bogatych funkcji na poziomie aplikacji oraz wbudowanej skalowalności potrzebnej dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8b0e5-167">Your choice depends on how many rich features at the application level and out-of-the-box scalability you need for your application.</span></span> <span data-ttu-id="8b0e5-168">W celu zaimplementowania tylko testowej magistrali zdarzeń dla środowiska deweloperskiego, tak jak zostało to zrobione w przykładzie eShopOnContainers, prosta implementacja na platformie RabbitMQ działającej w kontenerze platformy Docker może być wystarczająca.</span><span class="sxs-lookup"><span data-stu-id="8b0e5-168">For implementing just a proof-of-concept event bus for your development environment, as it was done in the eShopOnContainers sample, a simple implementation on top of RabbitMQ running on a Docker container might be enough.</span></span>

<span data-ttu-id="8b0e5-169">Jednak w przypadku systemów o znaczeniu krytycznym i produkcyjnym, które wymagają skalowalności, możesz chcieć oszacować Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="8b0e5-169">However, for mission-critical and production systems that need hyper-scalability, you might want to evaluate Azure Service Bus.</span></span> <span data-ttu-id="8b0e5-170">W przypadku abstrakcji i funkcji wysokiego poziomu, które ułatwiają tworzenie aplikacji rozproszonych, zalecamy ocenę innych komercyjnych i typu open-source magistrali usług, takich jak NServiceBus, MassTransit i jaśniejszy.</span><span class="sxs-lookup"><span data-stu-id="8b0e5-170">For high-level abstractions and features that make the development of distributed applications easier, we recommend that you evaluate other commercial and open-source service buses, such as NServiceBus, MassTransit, and Brighter.</span></span> <span data-ttu-id="8b0e5-171">Oczywiście możesz tworzyć własne funkcje magistrali usług na podstawie technologii niższego poziomu, takich jak RabbitMQ i Docker.</span><span class="sxs-lookup"><span data-stu-id="8b0e5-171">Of course, you can build your own service-bus features on top of lower-level technologies like RabbitMQ and Docker.</span></span> <span data-ttu-id="8b0e5-172">Jednak w przypadku niestandardowej aplikacji korporacyjnej prace wodociągowe mogą być zbyt duże.</span><span class="sxs-lookup"><span data-stu-id="8b0e5-172">But that plumbing work might cost too much for a custom enterprise application.</span></span>

## <a name="resiliently-publishing-to-the-event-bus"></a><span data-ttu-id="8b0e5-173">Odporne na przepublikowanie do magistrali zdarzeń</span><span class="sxs-lookup"><span data-stu-id="8b0e5-173">Resiliently publishing to the event bus</span></span>

<span data-ttu-id="8b0e5-174">Wyzwanie w przypadku implementowania architektury opartej na zdarzeniach w wielu mikrousługach polega na niepodzielnej aktualizacji stanu w ramach oryginalnej mikrousługi przy jednoczesnym opublikowaniu powiązanego z nim zdarzenia integracji w usłudze Event Bus w sposób w zależności od Akcja.</span><span class="sxs-lookup"><span data-stu-id="8b0e5-174">A challenge when implementing an event-driven architecture across multiple microservices is how to atomically update state in the original microservice while resiliently publishing its related integration event into the event bus, somehow based on transactions.</span></span> <span data-ttu-id="8b0e5-175">Poniżej przedstawiono kilka sposobów osiągnięcia tego celu, chociaż mogą wystąpić również dodatkowe podejścia.</span><span class="sxs-lookup"><span data-stu-id="8b0e5-175">The following are a few ways to accomplish this, although there could be additional approaches as well.</span></span>

- <span data-ttu-id="8b0e5-176">Korzystanie z kolejki transakcyjnej (opartej na usłudze DTC), takiej jak MSMQ.</span><span class="sxs-lookup"><span data-stu-id="8b0e5-176">Using a transactional (DTC-based) queue like MSMQ.</span></span> <span data-ttu-id="8b0e5-177">(Jest to jednak starsze podejście).</span><span class="sxs-lookup"><span data-stu-id="8b0e5-177">(However, this is a legacy approach.)</span></span>

- <span data-ttu-id="8b0e5-178">Korzystanie z [wyszukiwania w dzienniku transakcji](https://www.scoop.it/t/sql-server-transaction-log-mining).</span><span class="sxs-lookup"><span data-stu-id="8b0e5-178">Using [transaction log mining](https://www.scoop.it/t/sql-server-transaction-log-mining).</span></span>

- <span data-ttu-id="8b0e5-179">Używanie wzorca [pozyskiwania pełnego zdarzenia](https://docs.microsoft.com/azure/architecture/patterns/event-sourcing) .</span><span class="sxs-lookup"><span data-stu-id="8b0e5-179">Using full [Event Sourcing](https://docs.microsoft.com/azure/architecture/patterns/event-sourcing) pattern.</span></span>

- <span data-ttu-id="8b0e5-180">Używanie [wzorca skrzynki nadawczej](http://gistlabs.com/2014/05/the-outbox/): transakcyjna tabela bazy danych jako kolejka komunikatów, która będzie podstawą dla składnika Event-Creator, który utworzy zdarzenie i opublikuje je.</span><span class="sxs-lookup"><span data-stu-id="8b0e5-180">Using the [Outbox pattern](http://gistlabs.com/2014/05/the-outbox/): a transactional database table as a message queue that will be the base for an event-creator component that would create the event and publish it.</span></span>

<span data-ttu-id="8b0e5-181">Dodatkowe tematy, które należy wziąć pod uwagę podczas korzystania z komunikacji asynchronicznej, to idempotentność komunikatów i Deduplikacja komunikatów.</span><span class="sxs-lookup"><span data-stu-id="8b0e5-181">Additional topics to consider when using asynchronous communication are message idempotence and message deduplication.</span></span> <span data-ttu-id="8b0e5-182">Te tematy zostały omówione w sekcji [implementowanie komunikacji opartej na zdarzeniach między mikrousługami (zdarzenia integracji)](../multi-container-microservice-net-applications/integration-event-based-microservice-communications.md) w dalszej części tego przewodnika.</span><span class="sxs-lookup"><span data-stu-id="8b0e5-182">These topics are covered in the section [Implementing event-based communication between microservices (integration events)](../multi-container-microservice-net-applications/integration-event-based-microservice-communications.md) later in this guide.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8b0e5-183">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="8b0e5-183">Additional resources</span></span>

- <span data-ttu-id="8b0e5-184">**Obsługa komunikatów opartych na zdarzeniach** </span><span class="sxs-lookup"><span data-stu-id="8b0e5-184">**Event Driven Messaging** </span></span>\
  <http://soapatterns.org/design_patterns/event_driven_messaging>

- <span data-ttu-id="8b0e5-185">**Kanał publikowania/subskrybowania** </span><span class="sxs-lookup"><span data-stu-id="8b0e5-185">**Publish/Subscribe Channel** </span></span>\
  <https://www.enterpriseintegrationpatterns.com/patterns/messaging/PublishSubscribeChannel.html>

- <span data-ttu-id="8b0e5-186">**Udi Dahan. Wyjaśniono CQRS** </span><span class="sxs-lookup"><span data-stu-id="8b0e5-186">**Udi Dahan. Clarified CQRS** </span></span>\
  <http://udidahan.com/2009/12/09/clarified-cqrs/>

- <span data-ttu-id="8b0e5-187">**Command and Query Responsibility Segregation (CQRS)**  </span><span class="sxs-lookup"><span data-stu-id="8b0e5-187">**Command and Query Responsibility Segregation (CQRS)** </span></span>\
  <https://docs.microsoft.com/azure/architecture/patterns/cqrs>

- <span data-ttu-id="8b0e5-188">**Komunikacja między kontekstami ograniczonymi** </span><span class="sxs-lookup"><span data-stu-id="8b0e5-188">**Communicating Between Bounded Contexts** </span></span>\
  <https://docs.microsoft.com/previous-versions/msp-n-p/jj591572(v=pandp.10)>

- <span data-ttu-id="8b0e5-189">**Spójność ostateczna** </span><span class="sxs-lookup"><span data-stu-id="8b0e5-189">**Eventual consistency** </span></span>\
  <https://en.wikipedia.org/wiki/Eventual_consistency>

- <span data-ttu-id="8b0e5-190">**Jimmy Bogard. Refaktoryzacja względem odporności: Ocenianie sprzęgu** </span><span class="sxs-lookup"><span data-stu-id="8b0e5-190">**Jimmy Bogard. Refactoring Towards Resilience: Evaluating Coupling** </span></span>\
  <https://jimmybogard.com/refactoring-towards-resilience-evaluating-coupling/>

> [!div class="step-by-step"]
> <span data-ttu-id="8b0e5-191">[Poprzedni](communication-in-microservice-architecture.md)Następny
> [](maintain-microservice-apis.md)</span><span class="sxs-lookup"><span data-stu-id="8b0e5-191">[Previous](communication-in-microservice-architecture.md)
[Next](maintain-microservice-apis.md)</span></span>