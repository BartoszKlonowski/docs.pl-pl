---
title: Usługi danych WCF 4.5
description: Informacje na temat Usługi danych programu WCF, składnika .NET Framework, który obsługuje usługi umożliwiające udostępnianie i używanie danych przy użyciu semantyki REST.
ms.date: 03/30/2017
helpviewer_keywords:
- Astoria
- WCF Data Services, getting started
ms.assetid: 73d2bec3-7c92-4110-b905-11bb0462357a
ms.openlocfilehash: c36967236c40efbf432d554c3f551aea22cfb148
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/15/2020
ms.locfileid: "90549682"
---
# <a name="wcf-data-services-45"></a>Usługi danych WCF 4.5

Usługi danych programu WCF (dawniej znany jako "ADO.NET Data Services") jest składnikiem .NET Framework, który umożliwia tworzenie usług korzystających z protokołu Open Data Protocol (OData) do udostępniania danych i korzystania z nich za pośrednictwem sieci Web lub intranet przy użyciu semantyki [przenoszenia stanu (REST)](https://www.ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm). Usługa OData udostępnia dane jako zasoby, które są adresowane przez identyfikatory URI. Dostęp do danych jest uzyskiwany i zmieniany przy użyciu standardowych czasowników HTTP GET, PUT, POST i DELETE. Usługa OData używa Konwencji relacji jednostek [Entity Data Model](../adonet/entity-data-model.md) , aby udostępnić zasoby jako zestawy jednostek, które są powiązane ze skojarzeniami.

Usługi danych programu WCF używa protokołu OData do adresowania i aktualizacji zasobów. W ten sposób można uzyskać dostęp do tych usług z dowolnego klienta, który obsługuje protokół OData. Usługa OData umożliwia żądanie i zapisanie danych w zasobach przy użyciu dobrze znanych formatów transferu: Atom, zestaw standardów do wymiany i aktualizowania danych jako XML, a JavaScript Object Notation (JSON), format wymiany danych oparty na tekście, który jest szeroko używany w aplikacjach AJAX.

Usługi danych programu WCF mogą uwidaczniać dane pochodzące z różnych źródeł jako źródła danych OData. Narzędzia programu Visual Studio ułatwiają tworzenie usługi opartej na protokole OData przy użyciu modelu danych ADO.NET Entity Framework. Można również tworzyć źródła danych OData oparte na klasach środowiska uruchomieniowego języka wspólnego (CLR), a nawet z danymi z późnym wiązaniem lub bez typu.

Usługi danych programu WCF obejmuje również zestaw bibliotek klienckich, jeden dla ogólnych .NET Framework aplikacji klienckich, a drugi przeznaczony dla aplikacji opartych na technologii Silverlight. Te biblioteki klienckie zapewniają model programowania oparty na obiektach, gdy uzyskujesz dostęp do źródła danych OData ze środowisk, takich jak .NET Framework i Silverlight.

## <a name="where-should-i-start"></a>Gdzie należy zacząć?

W zależności od zainteresowań należy rozważyć wprowadzenie do Usługi danych programu WCF w jednym z poniższych tematów.

Chcę przeskoczyć do prawej strony...

- [Szybki start](quickstart-wcf-data-services.md)

- [Wprowadzenie](getting-started-with-wcf-data-services.md)

Pokaż mi tylko jakiś kod...

- [Szybki start](quickstart-wcf-data-services.md)

- [Instrukcje: Wykonywanie zapytań usługi danych](how-to-execute-data-service-queries-wcf-data-services.md)

- [Instrukcje: Wiązanie danych z elementami systemu Windows Presentation Foundation](bind-data-to-wpf-elements-wcf-data-services.md)

Chcę dowiedzieć się więcej o usłudze OData...

- [Oficjalny dokument: wprowadzenie do usługi OData](https://download.microsoft.com/download/E/5/A/E5A59052-EE48-4D64-897B-5F7C608165B8/IntroducingOData.pdf)
- [Otwórz witrynę internetową protokołu danych](https://www.odata.org/)
- [OData: SDK](https://www.odata.org/ecosystem/)

Chcę zobaczyć kompleksowe przykłady...

- [Usługi danych programu WCF — Szybki Start](https://github.com/microsoftarchive/msdn-code-gallery-community-s-z/tree/master/WCF%20Data%20Services%20Quickstart%20(OData%20Service%20and%20WPF%20Client))
- [Zestaw SDK OData — przykładowy kod](https://www.odata.org/ecosystem/#sdk)

Jak integruje się z programem Visual Studio?

- [Generowanie biblioteki klienta usługi danych](generating-the-data-service-client-library-wcf-data-services.md)

- [Tworzenie usługi danych](creating-the-data-service.md)

- [Dostawca programu Entity Framework](entity-framework-provider-wcf-data-services.md)

Co mogę zrobić z nim?

- [Omówienie](wcf-data-services-overview.md)

- [Scenariusze aplikacji](application-scenarios-wcf-data-services.md)

Chcę użyć LINQ...

- [Wykonywanie zapytań do usługi danych](querying-the-data-service-wcf-data-services.md)

- [Zagadnienia dotyczące LINQ](linq-considerations-wcf-data-services.md)

- [Instrukcje: Wykonywanie zapytań usługi danych](how-to-execute-data-service-queries-wcf-data-services.md)

Nadal potrzebuję więcej informacji...

- [Blog zespołu Usługi danych programu WCF](/archive/blogs/astoriateam/)

- [Zasoby](wcf-data-services-resources.md)

## <a name="in-this-section"></a>W tej sekcji

[Omówienie](wcf-data-services-overview.md)

Zawiera przegląd funkcji dostępnych w Usługi danych programu WCF.

[Co nowego w Usługi danych programu WCF 5,0](/previous-versions/dotnet/wcf-data-services/ee373845(v=vs.103))

Opisuje nowe funkcje w Usługi danych programu WCF i obsługę nowych funkcji OData.

[Wprowadzenie](getting-started-with-wcf-data-services.md)

Opisuje sposób udostępniania i korzystania ze źródeł danych OData przy użyciu Usługi danych programu WCF.

[Definiowanie usług danych WCF](defining-wcf-data-services.md)

Opisuje sposób tworzenia i konfigurowania usługi danych, która udostępnia źródła strumieniowego OData.

[Biblioteka klienta usług danych WCF](wcf-data-services-client-library.md)

Opisuje sposób używania bibliotek klienckich do korzystania ze źródeł danych OData z aplikacji klienckiej .NET Framework.

## <a name="see-also"></a>Zobacz także

- [Przenoszenie stanu reprezentacji (REST)](https://www.ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm)
