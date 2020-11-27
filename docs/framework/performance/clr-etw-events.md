---
title: Zdarzenia ETW CLR
description: 'Zobacz artykuły o zdarzeniach śledzenia zdarzeń środowiska uruchomieniowego języka wspólnego (CLR) dla systemu Windows (ETW). Istnieją dwa dostawcy zdarzeń: dostawca środowiska uruchomieniowego i dostawca uwalniania.'
ms.date: 03/30/2017
helpviewer_keywords:
- CLR ETW events
- ETW, common language runtime
- ETW, CLR events
ms.assetid: ef2b31c3-7426-43e7-9924-92339b96556d
ms.openlocfilehash: 8acc792b5217519e2a73c0cdf30c20161373c678
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96283916"
---
# <a name="clr-etw-events"></a><span data-ttu-id="ece44-104">Zdarzenia ETW CLR</span><span class="sxs-lookup"><span data-stu-id="ece44-104">CLR ETW Events</span></span>

<span data-ttu-id="ece44-105">W tematach w tej sekcji opisano zdarzenia śledzenia zdarzeń systemu Windows (ETW).</span><span class="sxs-lookup"><span data-stu-id="ece44-105">The topics in this section describe event tracing for Windows (ETW) events.</span></span> <span data-ttu-id="ece44-106">Każde zdarzenie ma skojarzone słowo kluczowe i poziom, które są opisane w temacie [słowa kluczowe ETW środowiska CLR i poziomy](clr-etw-keywords-and-levels.md) .</span><span class="sxs-lookup"><span data-stu-id="ece44-106">Each event has an associated keyword and level, which are described in the [CLR ETW Keywords and Levels](clr-etw-keywords-and-levels.md) topic.</span></span> <span data-ttu-id="ece44-107">Środowisko CLR ma dwóch dostawców dla zdarzeń:</span><span class="sxs-lookup"><span data-stu-id="ece44-107">The CLR has two providers for the events:</span></span>  
  
- <span data-ttu-id="ece44-108">Dostawca środowiska uruchomieniowego, który wywołuje zdarzenia w zależności od tego, które słowa kluczowe (kategorie zdarzeń) są włączone.</span><span class="sxs-lookup"><span data-stu-id="ece44-108">The runtime provider, which raises events depending on which keywords (categories of events) are enabled.</span></span> <span data-ttu-id="ece44-109">Identyfikator GUID dostawcy środowiska uruchomieniowego CLR to e13c0d23-ccbc-4e12-931b-d9cc2eee27e4.</span><span class="sxs-lookup"><span data-stu-id="ece44-109">The CLR runtime provider GUID is e13c0d23-ccbc-4e12-931b-d9cc2eee27e4.</span></span>  
  
- <span data-ttu-id="ece44-110">Dostawca uwalniania, który ma specjalne zastosowania.</span><span class="sxs-lookup"><span data-stu-id="ece44-110">The rundown provider, which has special-purpose uses.</span></span> <span data-ttu-id="ece44-111">Identyfikator GUID dostawcy uwalniania CLR to a669021c-c450-4609-a035-5af59af4df18.</span><span class="sxs-lookup"><span data-stu-id="ece44-111">The CLR rundown provider GUID is a669021c-c450-4609-a035-5af59af4df18.</span></span>  
  
 <span data-ttu-id="ece44-112">Więcej informacji o dostawcach znajduje się w temacie [dostawcy CLR ETW](clr-etw-providers.md).</span><span class="sxs-lookup"><span data-stu-id="ece44-112">For more information about the providers, see [CLR ETW Providers](clr-etw-providers.md).</span></span>  
  
## <a name="in-this-section"></a><span data-ttu-id="ece44-113">W tej sekcji</span><span class="sxs-lookup"><span data-stu-id="ece44-113">In This Section</span></span>  

 [<span data-ttu-id="ece44-114">Informacje o zdarzeniach środowiska uruchomieniowego</span><span class="sxs-lookup"><span data-stu-id="ece44-114">Runtime Information Events</span></span>](runtime-information-etw-events.md)  
 <span data-ttu-id="ece44-115">Przechwytuje informacje o środowisku uruchomieniowym, w tym jednostkę SKU, numer wersji, sposób aktywowania środowiska uruchomieniowego, parametry wiersza polecenia, które zostały uruchomione, identyfikator GUID (jeśli dotyczy) i inne istotne informacje.</span><span class="sxs-lookup"><span data-stu-id="ece44-115">Captures information about the runtime, including the SKU, version number, the manner in which the runtime was activated, the command-line parameters it was started with, the GUID (if applicable), and other relevant information.</span></span>  
  
 [<span data-ttu-id="ece44-116">Zdarzenie wyjątku ETW Thrown_V1</span><span class="sxs-lookup"><span data-stu-id="ece44-116">Exception Thrown_V1 Event</span></span>](exception-thrown-v1-etw-event.md)  
 <span data-ttu-id="ece44-117">Przechwytuje informacje o wygenerowanych wyjątkach.</span><span class="sxs-lookup"><span data-stu-id="ece44-117">Captures information about exceptions that are thrown.</span></span>  
  
 [<span data-ttu-id="ece44-118">Zdarzenia rywalizacji</span><span class="sxs-lookup"><span data-stu-id="ece44-118">Contention Events</span></span>](contention-etw-events.md)  
 <span data-ttu-id="ece44-119">Przechwytuje informacje o rywalizacji o blokady monitora lub blokady natywne używane przez środowisko uruchomieniowe.</span><span class="sxs-lookup"><span data-stu-id="ece44-119">Captures information about contention for monitor locks or native locks that the runtime uses.</span></span>  
  
 [<span data-ttu-id="ece44-120">Zdarzenia puli wątków</span><span class="sxs-lookup"><span data-stu-id="ece44-120">Thread Pool Events</span></span>](thread-pool-etw-events.md)  
 <span data-ttu-id="ece44-121">Przechwytuje informacje o pulach wątków roboczych i pulach wątków we/wy.</span><span class="sxs-lookup"><span data-stu-id="ece44-121">Captures information about worker thread pools and I/O thread pools.</span></span>  
  
 [<span data-ttu-id="ece44-122">Zdarzenia modułu ładującego</span><span class="sxs-lookup"><span data-stu-id="ece44-122">Loader Events</span></span>](loader-etw-events.md)  
 <span data-ttu-id="ece44-123">Przechwytuje informacje dotyczące ładowania i zwalniania domen aplikacji, zestawów i modułów.</span><span class="sxs-lookup"><span data-stu-id="ece44-123">Captures information about loading and unloading application domains, assemblies, and modules.</span></span>  
  
 [<span data-ttu-id="ece44-124">Zdarzenia metod</span><span class="sxs-lookup"><span data-stu-id="ece44-124">Method Events</span></span>](method-etw-events.md)  
 <span data-ttu-id="ece44-125">Przechwytuje informacje o metodach CLR rozpoznawania symboli.</span><span class="sxs-lookup"><span data-stu-id="ece44-125">Captures information about CLR methods for symbol resolution.</span></span>  
  
 [<span data-ttu-id="ece44-126">Zdarzenia odzyskiwania pamięci</span><span class="sxs-lookup"><span data-stu-id="ece44-126">Garbage Collection Events</span></span>](garbage-collection-etw-events.md)  
 <span data-ttu-id="ece44-127">Przechwytuje informacje dotyczące wyrzucania elementów bezużytecznych, aby ułatwić diagnostykę i debugowanie.</span><span class="sxs-lookup"><span data-stu-id="ece44-127">Captures information pertaining to garbage collection, to help in diagnostics and debugging.</span></span>  
  
 [<span data-ttu-id="ece44-128">Zdarzenia śledzenia JIT</span><span class="sxs-lookup"><span data-stu-id="ece44-128">JIT Tracing Events</span></span>](jit-tracing-etw-events.md)  
 <span data-ttu-id="ece44-129">Przechwytuje informacje o wywołaniach deokładzinowych i końcowych just-in-Time (JIT).</span><span class="sxs-lookup"><span data-stu-id="ece44-129">Captures information about just-in-time (JIT) inlining and tail calls.</span></span>  
  
 [<span data-ttu-id="ece44-130">Zdarzenia międzyoperacyjności</span><span class="sxs-lookup"><span data-stu-id="ece44-130">Interop Events</span></span>](interop-etw-events.md)  
 <span data-ttu-id="ece44-131">Przechwytuje informacje o generacji i buforowaniu klasy języka pośredniego firmy Microsoft (MSIL).</span><span class="sxs-lookup"><span data-stu-id="ece44-131">Captures information about Microsoft intermediate language (MSIL) stub generation and caching.</span></span>  
  
 [<span data-ttu-id="ece44-132">Zdarzenia ARM</span><span class="sxs-lookup"><span data-stu-id="ece44-132">ARM Events</span></span>](application-domain-resource-monitoring-arm-etw-events.md)  
 <span data-ttu-id="ece44-133">Przechwytuje szczegółowe informacje diagnostyczne o stanie domeny aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ece44-133">Captures detailed diagnostic information about the state of an application domain.</span></span>  
  
 [<span data-ttu-id="ece44-134">Zdarzenia zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="ece44-134">Security Events</span></span>](security-etw-events.md)  
 <span data-ttu-id="ece44-135">Przechwytuje informacje o silnych nazwach i weryfikacji Authenticode.</span><span class="sxs-lookup"><span data-stu-id="ece44-135">Captures information about strong name and Authenticode verification.</span></span>  
  
 [<span data-ttu-id="ece44-136">Zdarzenie stosu</span><span class="sxs-lookup"><span data-stu-id="ece44-136">Stack Event</span></span>](stack-etw-event.md)  
 <span data-ttu-id="ece44-137">Przechwytuje informacje, które są używane z innymi zdarzeniami do generowania śladów stosu po podniesieniu zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="ece44-137">Captures information that is used with other events to generate stack traces after an event is raised.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="ece44-138">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="ece44-138">See also</span></span>

- [<span data-ttu-id="ece44-139">Ulepszanie debugowania i dostrajania wydajności za pomocą funkcji ETW</span><span class="sxs-lookup"><span data-stu-id="ece44-139">Improve Debugging And Performance Tuning With ETW</span></span>](/archive/msdn-magazine/2007/april/event-tracing-improve-debugging-and-performance-tuning-with-etw)
- [<span data-ttu-id="ece44-140">Kontrolowanie logowania w programie .NET Framework</span><span class="sxs-lookup"><span data-stu-id="ece44-140">Controlling .NET Framework Logging</span></span>](controlling-logging.md)
- [<span data-ttu-id="ece44-141">Dostawcy CLR ETW</span><span class="sxs-lookup"><span data-stu-id="ece44-141">CLR ETW Providers</span></span>](clr-etw-providers.md)
- [<span data-ttu-id="ece44-142">Słowa kluczowe i poziomy ETW CLR</span><span class="sxs-lookup"><span data-stu-id="ece44-142">CLR ETW Keywords and Levels</span></span>](clr-etw-keywords-and-levels.md)
- [<span data-ttu-id="ece44-143">Zdarzenia ETW w środowisku CLR</span><span class="sxs-lookup"><span data-stu-id="ece44-143">ETW Events in the Common Language Runtime</span></span>](etw-events-in-the-common-language-runtime.md)
