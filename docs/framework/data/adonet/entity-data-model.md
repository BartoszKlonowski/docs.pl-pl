---
title: Entity Data Model
description: Entity Data Model opisuje strukturę danych, niezależnie od jej przechowywanego formularza, który rozwiązuje wyzwania związane z przechowywaniem danych w wielu formularzach.
ms.date: 03/30/2017
ms.assetid: 2dda3d5b-4582-4ba0-a91d-fcd7a1498137
ms.openlocfilehash: 9323f652d1cfa27d442d45bd01e546f3b81d7e80
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91200774"
---
# <a name="entity-data-model"></a>Entity Data Model

Entity Data Model (EDM) to zestaw koncepcji, które opisują strukturę danych, niezależnie od ich przechowywanego formularza. Model EDM jest pożyczany z modelu Entity-Relationship opisanego przez Peterowi Chen w 1976, ale również kompiluje się w modelu relacji jednostki i rozszerza jego tradycyjne zastosowania.  
  
 Modelu EDM zaspokaja wyzwania wynikające z posiadania danych przechowywanych w wielu formularzach. Rozważmy na przykład firmę, która przechowuje dane w relacyjnych bazach danych, plikach tekstowych, plikach XML, arkuszach kalkulacyjnych i raportach. Zapewnia to znaczne wyzwania w zakresie modelowania danych, projektowania aplikacji i dostępu do danych. Podczas projektowania aplikacji zorientowanej na dane, wyzwanie polega na napisaniu wydajnego i obsługiwanego kodu bez poświęcania wydajnego dostępu do danych, magazynowania i skalowalności. Gdy dane mają strukturę relacyjną, dostęp do danych, magazyn i skalowalność są bardzo wydajne, ale pisanie wydajnego i konserwowanego kodu jest trudniejsze. W przypadku, gdy dane mają strukturę obiektów, te wady są odwrócone: pisanie wydajnego i obsługiwanego kodu jest kosztem wydajnego dostępu do danych, magazynowania i skalowalności. Nawet w przypadku, gdy można znaleźć odpowiednie saldo między nimi, nowe wyzwania powstają, gdy dane są przenoszone z jednej formy do innej. Entity Data Model rozwiązuje te problemy, opisując strukturę danych w odniesieniu do jednostek i relacji, które są niezależne od schematu magazynu. Dzięki temu przechowywanie danych nie jest istotne dla projektowania i opracowywania aplikacji. I, ponieważ jednostki i relacje opisują strukturę danych, która jest używana w aplikacji (a nie w formie przechowywanej), można je rozwijać w miarę rozwoju aplikacji.  
  
 A `conceptual model` jest określoną reprezentacją struktury danych jako jednostek i relacji i jest ogólnie zdefiniowana w języku specyficznym dla domeny (DSL), który implementuje koncepcje modelu EDM. Przykładem takiego języka specyficznego dla domeny jest [język w języku definicji schematu koncepcyjnego (CSDL)](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec) . Jednostki i relacje opisane w modelu koncepcyjnym można traktować jako abstrakcje obiektów i skojarzeń w aplikacji. Pozwala to deweloperom skupić się na modelu koncepcyjnym bez obaw dla schematu magazynu i umożliwia im pisanie kodu z wydajnością i łatwość utrzymania. Projektanci schematów magazynu mogą skupić się na wydajności dostępu do danych, magazynowania i skalowalności.  
  
## <a name="in-this-section"></a>W tej sekcji  

 Tematy w tej sekcji opisują koncepcje Entity Data Model. Wszystkie DSL, które implementują modelu EDM, powinny zawierać Koncepcje opisane tutaj. Należy pamiętać, że [ADO.NET Entity Framework](./ef/index.md) używa CSDL do definiowania modeli koncepcyjnych. Aby uzyskać więcej informacji, zobacz [Specyfikacja CSDL](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec).  
  
 [Kluczowe założenia modelu danych jednostki](entity-data-model-key-concepts.md)  
  
 [Model danych jednostki: Namespaces](entity-data-model-namespaces.md)  
  
 [Model danych jednostki: Typy danych pierwotnych](entity-data-model-primitive-data-types.md)  
  
 [Model danych jednostki: Dziedziczenie](entity-data-model-inheritance.md)  
  
 [punkt końcowy skojarzenia](association-end.md)  
  
 [skojarzenie i liczebność](association-end-multiplicity.md)  
  
 [zestaw skojarzeń](association-set.md)  
  
 [punkt końcowy zestawu skojarzeń](association-set-end.md)  
  
 [typ skojarzenia](association-type.md)  
  
 [typ złożony](complex-type.md)  
  
 [kontener jednostek](entity-container.md)  
  
 [klucz jednostki](entity-key.md)  
  
 [zestaw jednostek](entity-set.md)  
  
 [typ jednostki](entity-type.md)  
  
 [facet](facet.md)  
  
 [właściwość klucza obcego](foreign-key-property.md)  
  
 [funkcja zadeklarowana modelu](model-declared-function.md)  
  
 [funkcja zdefiniowana przez model](model-defined-function.md)  
  
 [właściwość nawigacji](navigation-property.md)  
  
 [wartość](property.md)  
  
 [ograniczenie integralności referencyjnej](referential-integrity-constraint.md)  
  
## <a name="see-also"></a>Zobacz też

- [Narzędzia Entity Data Model ADO.NET](/previous-versions/dotnet/netframework-4.0/bb399249(v=vs.100))
- [Plik. edmx — Omówienie](/previous-versions/dotnet/netframework-4.0/cc982042(v=vs.100))
- [Specyfikacja CSDL](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec)
