---
title: Rozwiązywanie problemów ze złożonościami biznesowymi w mikrousłudze z wzorcami DDD i CQRS
description: Architektura mikrousług platformy .NET dla aplikacji platformy .NET w kontenerze | Dowiedz się, jak rozwiązywać złożone scenariusze biznesowe, stosując wzorce DDD i CQRS
ms.date: 10/08/2018
ms.openlocfilehash: 852073548a66fbe568fc5c2531342db944d5a8b0
ms.sourcegitcommit: ee5b798427f81237a3c23d1fd81fff7fdc21e8d3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/28/2020
ms.locfileid: "84144646"
---
# <a name="tackle-business-complexity-in-a-microservice-with-ddd-and-cqrs-patterns"></a>Rozwiązywanie problemów ze złożonościami biznesowymi w mikrousłudze z wzorcami DDD i CQRS

*Zaprojektuj model domeny dla każdego mikrousług lub kontekstu ograniczonego, który odzwierciedla zrozumienie domeny biznesowej.*

Ta sekcja koncentruje się na bardziej zaawansowanych mikrousługach, które są implementowane, gdy potrzebna jest obsługa złożonych podsystemów lub mikrousług pochodzących od znajomości ekspertów domeny z kiedykolwiek zmienionymi regułami biznesowymi. Wzorce architektury użyte w tej sekcji są oparte na podejściach do projektowania opartego na domenach (DDD) i Command and Query Responsibility Segregation (CQRS), jak pokazano na rysunku 7-1.

:::image type="complex" source="./media/index/internal-versus-external-architecture.png" alt-text="Diagram porównujący wzorce architektury zewnętrznej i wewnętrznej.":::
Różnica między architekturą zewnętrzną: wzorce mikrousług, bramy interfejsu API, komunikacja odporna, publikacje/podpłaty, itp. i architektura wewnętrzna: oparte na danych/CRUD, wzorce DDD, iniekcja zależności, wiele bibliotek itd.
:::image-end:::

**Rysunek 7-1**. Zewnętrzna architektura mikrousług, a wewnętrzne wzorce architektury dla każdej mikrousługi

Jednak większość technik dla mikrousług opartych na danych, takich jak implementacja usługi Web API ASP.NET Core lub sposób ujawniania metadanych struktury Swagger przy użyciu Swashbuckle lub NSwag, ma również zastosowanie do bardziej zaawansowanych mikrousług wdrożonych wewnętrznie z wzorcami DDD. Ta sekcja stanowi rozszerzenie poprzednich sekcji, ponieważ większość praktyk opisanych wcześniej również ma zastosowanie w tym miejscu lub dla dowolnego rodzaju mikrousług.

Ta sekcja najpierw zawiera szczegółowe informacje dotyczące uproszczonych wzorców CQRS używanych w aplikacji eShopOnContainers Reference. Później zostanie wyświetlony przegląd technik, które umożliwiają znalezienie typowych wzorców, których można użyć ponownie w aplikacjach.

DDD to duży temat z bogatym zestawem zasobów do uczenia się. Możesz zacząć od książek, takich jak [Projektowanie oparte na domenach](https://domainlanguage.com/ddd/) przez Eric Evans i dodatkowe materiały z Vaughn Vernon, Jimmy Nilsson, Greg Young, UDI Dahan, Jimmy Bogard i wielu innych ekspertów DDD/CQRS. Ale większość z nich jest konieczna, aby dowiedzieć się, jak zastosować techniki DDD z konwersacji, tablic i sesji modelowania domeny z ekspertami w konkretnej domenie biznesowej.

#### <a name="additional-resources"></a>Zasoby dodatkowe

##### <a name="ddd-domain-driven-design"></a>DDD (Projektowanie oparte na domenie)

- **Eric Evans. Język domeny** \
  <https://domainlanguage.com/>

- **Fowlera Martin. Projektowanie oparte na domenie** \
  <https://martinfowler.com/tags/domain%20driven%20design.html>

- **Jimmy Bogard. Wzmacnianie domeny: podstawowy** \
  <https://lostechies.com/jimmybogard/2010/02/04/strengthening-your-domain-a-primer/>

##### <a name="ddd-books"></a>Książki

- **Eric Evans. Projektowanie oparte na domenie: zapełnianie złożoności w serca oprogramowania** \
  <https://www.amazon.com/Domain-Driven-Design-Tackling-Complexity-Software/dp/0321125215/>

- **Eric Evans. Odwołanie do projektu oparte na domenie: definicje i podsumowania wzorców** \
  <https://www.amazon.com/Domain-Driven-Design-Reference-Definitions-2014-09-22/dp/B01N8YB4ZO/>

- **Vaughn Vernon. Implementowanie projektu opartego na domenie** \
  <https://www.amazon.com/Implementing-Domain-Driven-Design-Vaughn-Vernon/dp/0321834577/>

- **Vaughn Vernon. Projekt oparty na domenie jest odłączony** \
  <https://www.amazon.com/Domain-Driven-Design-Distilled-Vaughn-Vernon/dp/0134434420/>

- **Jimmy Nilsson. Stosowanie projektowania i wzorców opartych na domenie** \
  <https://www.amazon.com/Applying-Domain-Driven-Design-Patterns-Examples/dp/0321268202/>

- **Cesar de La Torre. N-warstwowe wskazówki dotyczące architektury zorientowanej na domeny z platformą .NET** \
  <https://www.amazon.com/N-Layered-Domain-Oriented-Architecture-Guide-NET/dp/8493903612/>

- **Abel Avram i Floyd Marinescu. Szybkie projektowanie oparte na domenie** \
  <https://www.amazon.com/Domain-Driven-Design-Quickly-Abel-Avram/dp/1411609255/>

- **Scott Millett, Nick dostrajania — wzorce, zasady i praktyki dotyczące projektowania opartego na domenie** \
  <https://www.wiley.com/Patterns%2C+Principles%2C+and+Practices+of+Domain+Driven+Design-p-9781118714706>

##### <a name="ddd-training"></a>Uczenie DDD

- **Julie Lerman i Steve Smith. Podstawy projektowania oparte na domenie** \
  <https://bit.ly/PS-DDD>

>[!div class="step-by-step"]
>[Poprzedni](../multi-container-microservice-net-applications/implement-api-gateways-with-ocelot.md) 
> [Dalej](apply-simplified-microservice-cqrs-ddd-patterns.md)
