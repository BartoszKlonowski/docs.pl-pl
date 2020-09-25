---
title: Azure Event Grid — aplikacje bezserwerowe
description: Azure Event Grid to rozwiązanie bezserwerowe do niezawodnego dostarczania zdarzeń i routingu na dużą skalę w modelu z wynagrodzeniem dla każdego zdarzenia.
author: JEREMYLIKNESS
ms.author: jeliknes
ms.date: 04/06/2020
ms.openlocfilehash: 30937bafd8069eb4508dce18351964103421373a
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91171887"
---
# <a name="event-grid"></a>Event Grid

[Azure Event Grid](/azure/event-grid/overview) zapewnia infrastrukturę bezserwerową dla aplikacji opartych na zdarzeniach. Możesz publikować w Event Grid z dowolnego źródła i korzystać z komunikatów z dowolnej platformy. Event Grid również ma wbudowaną obsługę zdarzeń z zasobów platformy Azure w celu usprawnienia integracji z aplikacjami. Można na przykład subskrybować zdarzenia usługi BLOB Storage w celu powiadomienia aplikacji o przekazaniu pliku. Aplikacja może następnie opublikować niestandardowy komunikat usługi Event Grid, który jest używany przez inne aplikacje w chmurze lub aplikacji lokalnych. Event Grid został zbudowany w celu niezawodnego obsługi ogromnej skali. Korzyści wynikające z publikowania i subskrybowania komunikatów nie są związane z konfigurowaniem niezbędnej infrastruktury.

![Logo Event Grid](./media/event-grid-logo.png)

Główne funkcje siatki zdarzeń obejmują:

- W pełni zarządzane routing zdarzeń.
- Dostarczanie zdarzeń niemal w czasie rzeczywistym na dużą skalę.
- Szerokie pokrycie zarówno wewnątrz, jak i poza platformą Azure.

## <a name="scenarios"></a>Scenariusze

Event Grid dotyczy kilku różnych scenariuszy. W tej sekcji omówiono trzy najbardziej typowe.

### <a name="ops-automation"></a>Automatyzacja operacji

![Automatyzacja operacji](./media/ops-automation.png)

Event Grid mogą pomóc przyspieszyć automatyzację i uprościć wymuszanie zasad, powiadamiając [Azure Automation](/azure/automation) o aprowizacji infrastruktury.

### <a name="application-integration"></a>Integracja aplikacji

![Integracja aplikacji](./media/app-integration.png)

Możesz użyć Event Grid, aby połączyć aplikację z innymi usługami. Przy użyciu standardowych protokołów HTTP nawet starsze aplikacje można łatwo modyfikować w celu publikowania Event Grid komunikatów. Elementy webhook są dostępne dla innych usług i platform do korzystania z Event Grid komunikatów.

### <a name="serverless-apps"></a>Aplikacje bezserwerowe

![Aplikacje bezserwerowe](./media/serverless-apps.png)

Event Grid może wyzwalać Azure Functions, Logic Apps lub własny kod niestandardowy. Główną zaletą korzystania z Event Grid jest użycie mechanizmu *wypychania* do wysyłania komunikatów, gdy wystąpią zdarzenia. Architektura wypychana zużywa mniej zasobów i skaluje się lepiej niż mechanizmy *sondowania* . Sondowanie musi sprawdzać dostępność aktualizacji w regularnych odstępach czasu.

## <a name="event-grid-vs-other-azure-messaging-services"></a>Event Grid a inne usługi Azure Messaging

Platforma Azure udostępnia kilka usług obsługi komunikatów, w tym [Event Hubs](/azure/event-hubs) i [Service Bus](/azure/service-bus-messaging). Każdy z nich został zaprojektowany w celu rozwiązania określonego zestawu przypadków użycia. Poniższy diagram zawiera ogólne omówienie różnic między usługami.

![Porównanie usługi Azure Messaging](./media/azure-messaging-services.png)

Aby zapoznać się z bardziej szczegółowym porównaniem, zobacz [porównanie usług obsługi komunikatów](/azure/event-grid/compare-messaging-services).

## <a name="performance-targets"></a>Cele wydajności

Za pomocą Event Grid można wykorzystać następujące gwarancje dotyczące wydajności:

- Opóźnienie od końca do końca w 99 percentylu.
- Dostępność na poziomie 99,99%.
- 10 000 000 zdarzeń na sekundę na region.
- 100 000 000 subskrypcji na region.
- 50 — opóźnienie MS Publisher.
- 24-godzinna ponowna próba z wykładniczym wycofywaniem w celu zapewnienia gwarantowanej dostawy w oknie 1-dniowym.
- Przezroczyste regionalne przejście w tryb failover.

## <a name="event-grid-schema"></a>Schemat usługi Event Grid

Event Grid używa standardowego schematu do zawijania niestandardowych zdarzeń. Schemat jest podobny do koperty, która otacza niestandardowy element danych. Oto przykładowy komunikat Event Grid:

```json
[{
    "id": "03e24f21-a955-43cc-8921-1f61a6081ce0",
    "eventType": "myCustomEvent",
    "subject": "foo/bar/12",
    "eventTime": "2018-09-22T10:36:01+00:00",
    "data": {
        "favoriteColor": "blue",
        "favoriteAnimal": "panther",
        "favoritePlanet": "Jupiter"
    },
    "dataVersion": "1.0"
}]
```

Wszystko, czego dotyczy komunikat, jest standardowe poza `data` właściwością. Można sprawdzić komunikat i użyć `eventType` i `dataVersion` deserializować niestandardowego części ładunku.

## <a name="azure-resources"></a>Zasoby platformy Azure

Główną zaletą korzystania z Event Grid są automatyczne komunikaty generowane przez platformę Azure. Na platformie Azure zasoby są automatycznie publikowane w *temacie* , który pozwala subskrybować różne zdarzenia. W poniższej tabeli wymieniono typy zasobów, typy komunikatów i zdarzenia, które są dostępne automatycznie.

| Zasób platformy Azure | Typ zdarzenia | Opis |
| -------------- | ---------- | ----------- |
| Subskrypcja platformy Azure | Microsoft. resources. ResourceWriteSuccess | Uruchamiany, gdy operacja tworzenia lub aktualizowania zasobu zostanie zakończona pomyślnie. |
| | Microsoft. resources. ResourceWriteFailure | Uruchamiany, gdy operacja tworzenia lub aktualizowania zasobu nie powiedzie się. |
| | Microsoft. resources. ResourceWriteCancel | Uruchamiany, gdy operacja tworzenia lub aktualizowania zasobu zostanie anulowana. |
|  | Microsoft. resources. ResourceDeleteSuccess | Uruchamiany, gdy operacja usunięcia zasobu zostanie zakończona pomyślnie. |
|  | Microsoft. resources. ResourceDeleteFailure | Uruchamiany, gdy operacja usunięcia zasobu nie powiedzie się. |
| | Microsoft. resources. ResourceDeleteCancel | Uruchamiany, gdy operacja usunięcia zasobu zostanie anulowana. To zdarzenie występuje, gdy wdrożenie szablonu zostało anulowane. |
| Blob Storage | Microsoft. Storage. BlobCreated | Uruchamiany po utworzeniu obiektu BLOB. |
| | Microsoft. Storage. BlobDeleted | Uruchamiany, gdy obiekt BLOB zostanie usunięty. |
| Usługa Event Hubs | Microsoft. EventHub. CaptureFileCreated | Uruchamiany podczas tworzenia pliku przechwytywania.
| Usługa IoT Hub | Microsoft.Devices.DeviceCreated | Opublikowano, gdy urządzenie jest zarejestrowane w usłudze IoT Hub. |
| | Microsoft.Devices.DeviceDeleted | Opublikowano, gdy urządzenie zostanie usunięte z Centrum IoT Hub. |
| Grupy zasobów | Microsoft. resources. ResourceWriteSuccess | Uruchamiany, gdy operacja tworzenia lub aktualizowania zasobu zostanie zakończona pomyślnie. |
| | Microsoft. resources. ResourceWriteFailure | Uruchamiany, gdy operacja tworzenia lub aktualizowania zasobu nie powiedzie się. |
| | Microsoft. resources. ResourceWriteCancel | Uruchamiany, gdy operacja tworzenia lub aktualizowania zasobu zostanie anulowana. |
| | Microsoft. resources. ResourceDeleteSuccess | Uruchamiany, gdy operacja usunięcia zasobu zostanie zakończona pomyślnie. |
| | Microsoft. resources. ResourceDeleteFailure | Uruchamiany, gdy operacja usunięcia zasobu nie powiedzie się. |
| | Microsoft. resources. ResourceDeleteCancel | Uruchamiany, gdy operacja usunięcia zasobu zostanie anulowana. To zdarzenie występuje, gdy wdrożenie szablonu zostało anulowane. |

Aby uzyskać więcej informacji, zobacz [Azure Event Grid schemacie zdarzeń](/azure/event-grid/event-schema).

Możesz uzyskać dostęp do Event Grid z dowolnego typu aplikacji, nawet jednego działającego lokalnie.

## <a name="conclusion"></a>Podsumowanie

W tym rozdziale przedstawiono platformę bezserwerową platformy Azure, która składa się z Azure Functions, Logic Apps i Event Grid. Za pomocą tych zasobów można utworzyć całkowicie bezserwerową architekturę aplikacji lub utworzyć rozwiązanie hybrydowe, które współdziała z innymi zasobami w chmurze i serwerami lokalnymi. W połączeniu z platformą danych bezserwerową, taką jak [Azure SQL](/azure/sql-database) lub [CosmosDB](/azure/cosmos-db/introduction), można tworzyć w pełni zarządzane aplikacje natywne w chmurze.

## <a name="recommended-resources"></a>Zalecane zasoby

- [Plany usługi App Service](/azure/app-service/azure-web-sites-web-hosting-plans-in-depth-overview)
- [Application Insights](/azure/application-insights)
- [Analiza Application Insights](/azure/application-insights/app-insights-analytics)
- [Azure: Przenieś swoją aplikację do chmury, korzystając z bezserwerowego Azure Functions](https://channel9.msdn.com/events/Connect/2017/E102)
- [Azure Event Grid](/azure/event-grid/overview)
- [Schemat zdarzeń Azure Event Grid](/azure/event-grid/event-schema)
- [Azure Event Hubs](/azure/event-hubs)
- [Dokumentacja usługi Azure Functions](/azure/azure-functions)
- [Pojęcia powiązań i wyzwalaczy usługi Azure Functions](/azure/azure-functions/functions-triggers-bindings)
- [Azure Logic Apps](/azure/logic-apps)
- [Azure Service Bus](/azure/service-bus-messaging)
- [Azure Table Storage](/azure/cosmos-db/table-storage-overview)
- [Łączenie z lokalnymi źródłami danych za pomocą bramy danych lokalnych platformy Azure](/azure/analysis-services/analysis-services-gateway)
- [Tworzenie pierwszej funkcji w witrynie Azure Portal](/azure/azure-functions/functions-create-first-azure-function)
- [Tworzenie pierwszej funkcji z poziomu interfejsu wiersza polecenia platformy Azure](/azure/azure-functions/functions-create-first-azure-function-azure-cli)
- [Tworzenie pierwszej funkcji przy użyciu programu Visual Studio](/azure/azure-functions/functions-create-your-first-function-visual-studio)
- [Obsługiwane języki](/azure/azure-functions/supported-languages)
- [Monitorowanie usługi Azure Functions](/azure/azure-functions/functions-monitoring)

>[!div class="step-by-step"]
>[Poprzedni](logic-apps.md) 
> [Dalej](durable-azure-functions.md)
