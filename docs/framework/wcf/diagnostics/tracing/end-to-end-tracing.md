---
title: Kompleksowe śledzenie
ms.date: 03/30/2017
ms.assetid: f5ac7fc7-f97c-4313-b068-54e0c471b2aa
ms.openlocfilehash: a8c06b9e4f70321e6ef3756863390dc62c659557
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96243953"
---
# <a name="end-to-end-tracing"></a><span data-ttu-id="876e4-102">Kompleksowe śledzenie</span><span class="sxs-lookup"><span data-stu-id="876e4-102">End-to-End Tracing</span></span>

<span data-ttu-id="876e4-103">Śledzenie kompleksowe (E2E) umożliwia deweloperom wykonywanie kodu w infrastrukturze Windows Communication Foundation (WCF) w celu zbadania przyczyny niepowodzenia ścieżki kodu lub zapewnienia szczegółowego śledzenia wydajności planowania pojemności i analizy wydajności.</span><span class="sxs-lookup"><span data-stu-id="876e4-103">End to End (e2e) Tracing allows developers to follow the execution of code in the Windows Communication Foundation (WCF) infrastructure to investigate why a code path has failed, or to provide detailed tracing for capacity planning and performance analysis.</span></span> <span data-ttu-id="876e4-104">Windows Communication Foundation (WCF) oferuje trzy mechanizmy korelacji ułatwiające zdiagnozowanie przyczyny błędu: działania, transfery i Propagacja.</span><span class="sxs-lookup"><span data-stu-id="876e4-104">Windows Communication Foundation (WCF) provides three correlation mechanisms to help diagnose the cause of an error: activities, transfers, and propagation.</span></span>  
  
 <span data-ttu-id="876e4-105">Zapoznaj się z [kompleksowymi scenariuszami śledzenia](end-to-end-tracing-scenarios.md) , aby zapoznać się z listą kompleksowych scenariuszy śledzenia i ich odpowiedniego projektu działań i śledzenia.</span><span class="sxs-lookup"><span data-stu-id="876e4-105">See [End-To-End Tracing Scenarios](end-to-end-tracing-scenarios.md) for a list of end-to-end tracing scenarios, and their respective activity and tracing design.</span></span>  
  
## <a name="in-this-section"></a><span data-ttu-id="876e4-106">W tej sekcji</span><span class="sxs-lookup"><span data-stu-id="876e4-106">In This Section</span></span>  

 <span data-ttu-id="876e4-107">[Działanie](activity.md): opisuje ślady aktywności w modelu śledzenia Windows Communication Foundation (WCF).</span><span class="sxs-lookup"><span data-stu-id="876e4-107">[Activity](activity.md):  Describes activity traces in the Windows Communication Foundation (WCF) tracing model.</span></span>  
  
 <span data-ttu-id="876e4-108">[Transfer](transfer.md): opisuje transfer w modelu śledzenia Windows Communication Foundation (WCF) i używanie transferu do skorelowania działań w punktach końcowych.</span><span class="sxs-lookup"><span data-stu-id="876e4-108">[Transfer](transfer.md):  Describes transfer in the Windows Communication Foundation (WCF) tracing model, and using transfer to correlate activities within endpoints.</span></span>  
  
 <span data-ttu-id="876e4-109">[Propagacja](propagation.md): opisuje propagację działań w modelu śledzenia Windows Communication Foundation (WCF) i używa propagacji do skorelowania działań w punktach końcowych.</span><span class="sxs-lookup"><span data-stu-id="876e4-109">[Propagation](propagation.md):  Describes activity propagation in the Windows Communication Foundation (WCF) tracing model, and using propagation to correlate activities across endpoints.</span></span>  
  
 [<span data-ttu-id="876e4-110">Podsumowanie typu śledzenia</span><span class="sxs-lookup"><span data-stu-id="876e4-110">Trace Type Summary</span></span>](trace-type-summary.md)  
  
 <span data-ttu-id="876e4-111">Zawiera podsumowanie wszystkich typów śledzenia działania</span><span class="sxs-lookup"><span data-stu-id="876e4-111">Provides a summary of all activity trace types</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="876e4-112">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="876e4-112">See also</span></span>

- [<span data-ttu-id="876e4-113">Konfigurowanie śledzenia</span><span class="sxs-lookup"><span data-stu-id="876e4-113">Configuring Tracing</span></span>](configuring-tracing.md)
- [<span data-ttu-id="876e4-114">Używanie przeglądarki danych śledzenia usługi do wyświetlania skorelowanych danych śledzenia i rozwiązywania problemów</span><span class="sxs-lookup"><span data-stu-id="876e4-114">Using Service Trace Viewer for Viewing Correlated Traces and Troubleshooting</span></span>](using-service-trace-viewer-for-viewing-correlated-traces-and-troubleshooting.md)
- [<span data-ttu-id="876e4-115">Scenariusze kompleksowego śledzenia</span><span class="sxs-lookup"><span data-stu-id="876e4-115">End-To-End Tracing Scenarios</span></span>](end-to-end-tracing-scenarios.md)
- [<span data-ttu-id="876e4-116">Narzędzie do przeglądania danych śledzenia usług (SvcTraceViewer.exe)</span><span class="sxs-lookup"><span data-stu-id="876e4-116">Service Trace Viewer Tool (SvcTraceViewer.exe)</span></span>](../../service-trace-viewer-tool-svctraceviewer-exe.md)
