---
title: Rejestrowanie i śledzenie — .NET Core
description: Wprowadzenie do rejestrowania i śledzenia w programie .NET Core.
ms.date: 10/12/2020
ms.openlocfilehash: 9af04cceeef3fbfb8392eb91667c21374511548a
ms.sourcegitcommit: 34968a61e9bac0f6be23ed6ffb837f52d2390c85
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/17/2020
ms.locfileid: "94687586"
---
# <a name="net-core-logging-and-tracing"></a><span data-ttu-id="34323-103">Rejestrowanie i śledzenie w programie .NET Core</span><span class="sxs-lookup"><span data-stu-id="34323-103">.NET Core logging and tracing</span></span>

<span data-ttu-id="34323-104">Rejestrowanie i śledzenie są bardzo dwie nazwy dla tej samej techniki.</span><span class="sxs-lookup"><span data-stu-id="34323-104">Logging and tracing are really two names for the same technique.</span></span> <span data-ttu-id="34323-105">Prosta technika została użyta od momentu wczesnego dnia komputerów.</span><span class="sxs-lookup"><span data-stu-id="34323-105">The simple technique has been used since the early days of computers.</span></span> <span data-ttu-id="34323-106">Po prostu obejmuje instrumentację aplikacji w celu zapisania danych wyjściowych do późniejszego wykorzystania.</span><span class="sxs-lookup"><span data-stu-id="34323-106">It simply involves instrumenting an application to write output to be consumed later.</span></span>

## <a name="reasons-to-use-logging-and-tracing"></a><span data-ttu-id="34323-107">Przyczyny używania rejestrowania i śledzenia</span><span class="sxs-lookup"><span data-stu-id="34323-107">Reasons to use logging and tracing</span></span>

<span data-ttu-id="34323-108">Ta prosta technika jest zaskakująco zaawansowana.</span><span class="sxs-lookup"><span data-stu-id="34323-108">This simple technique is surprisingly powerful.</span></span> <span data-ttu-id="34323-109">Może być używana w sytuacjach, w których debuger kończy się niepowodzeniem:</span><span class="sxs-lookup"><span data-stu-id="34323-109">It can be used in situations where a debugger fails:</span></span>

- <span data-ttu-id="34323-110">Problemy występujące w długich okresach mogą być trudne do debugowania przy użyciu tradycyjnego debugera.</span><span class="sxs-lookup"><span data-stu-id="34323-110">Issues occurring over long periods of time, can be difficult to debug with a traditional debugger.</span></span> <span data-ttu-id="34323-111">Dzienniki pozwalają na przeprowadzanie szczegółowych przeglądów obejmujących długie okresy po zakończeniu pracy.</span><span class="sxs-lookup"><span data-stu-id="34323-111">Logs allow for detailed post-mortem review spanning long periods of time.</span></span> <span data-ttu-id="34323-112">Z kolei debugery są ograniczone do analizy w czasie rzeczywistym.</span><span class="sxs-lookup"><span data-stu-id="34323-112">In contrast, debuggers are constrained to real-time analysis.</span></span>
- <span data-ttu-id="34323-113">Aplikacje wielowątkowe i aplikacje rozproszone często są trudne do debugowania.</span><span class="sxs-lookup"><span data-stu-id="34323-113">Multi-threaded applications and distributed applications are often difficult to debug.</span></span>  <span data-ttu-id="34323-114">Dołączenie debugera powoduje modyfikację zachowań.</span><span class="sxs-lookup"><span data-stu-id="34323-114">Attaching a debugger tends to modify behaviors.</span></span> <span data-ttu-id="34323-115">Szczegółowe dzienniki można analizować w miarę potrzeby w celu lepszego zrozumienia złożonych systemów.</span><span class="sxs-lookup"><span data-stu-id="34323-115">Detailed logs can be analyzed as needed to understand complex systems.</span></span>
- <span data-ttu-id="34323-116">Problemy w aplikacjach rozproszonych mogą powstać w wyniku złożonej interakcji między wieloma składnikami i dołączanie debugera do każdej części systemu może nie być uzasadnione.</span><span class="sxs-lookup"><span data-stu-id="34323-116">Issues in distributed applications may arise from a complex interaction between many components and it may not be reasonable to connect a debugger to every part of the system.</span></span>
- <span data-ttu-id="34323-117">Wielu usług nie należy zawieszać.</span><span class="sxs-lookup"><span data-stu-id="34323-117">Many services shouldn't be stalled.</span></span> <span data-ttu-id="34323-118">Dołączanie debugera często powoduje błędy polegające na przekroczeniu limitu czasu.</span><span class="sxs-lookup"><span data-stu-id="34323-118">Attaching a debugger often causes timeout failures.</span></span>
- <span data-ttu-id="34323-119">Problemy nie zawsze można przewidzieć.</span><span class="sxs-lookup"><span data-stu-id="34323-119">Issues aren't always foreseen.</span></span> <span data-ttu-id="34323-120">Rejestrowanie i śledzenie zostało zaprojektowane z myślą o niskim obciążeniu, dzięki czemu program może zawsze rejestrować w przypadku wystąpienia problemu.</span><span class="sxs-lookup"><span data-stu-id="34323-120">Logging and tracing are designed for low overhead so that programs can always be recording in case an issue occurs.</span></span>

## <a name="net-core-apis"></a><span data-ttu-id="34323-121">Interfejsy API platformy .NET Core</span><span class="sxs-lookup"><span data-stu-id="34323-121">.NET Core APIs</span></span>

### <a name="print-style-apis"></a><span data-ttu-id="34323-122">Interfejsy API stylu drukowania</span><span class="sxs-lookup"><span data-stu-id="34323-122">Print style APIs</span></span>

<span data-ttu-id="34323-123"><xref:System.Console?displayProperty=nameWithType>Klasy, <xref:System.Diagnostics.Trace?displayProperty=nameWithType> i, <xref:System.Diagnostics.Debug?displayProperty=nameWithType> każdy udostępniają podobne interfejsy API stylu drukowania wygodne do rejestrowania.</span><span class="sxs-lookup"><span data-stu-id="34323-123">The <xref:System.Console?displayProperty=nameWithType>, <xref:System.Diagnostics.Trace?displayProperty=nameWithType>, and <xref:System.Diagnostics.Debug?displayProperty=nameWithType> classes each provide similar print style APIs convenient for logging.</span></span>

<span data-ttu-id="34323-124">Wybór interfejsu API w stylu wydruku do użycia należy do Ciebie.</span><span class="sxs-lookup"><span data-stu-id="34323-124">The choice of which print style API to use is up to you.</span></span> <span data-ttu-id="34323-125">Kluczowe różnice są następujące:</span><span class="sxs-lookup"><span data-stu-id="34323-125">The key differences are:</span></span>

- <xref:System.Console?displayProperty=nameWithType>
  - <span data-ttu-id="34323-126">Zawsze włączony i zawsze zapisuje do konsoli.</span><span class="sxs-lookup"><span data-stu-id="34323-126">Always enabled and always writes to the console.</span></span>
  - <span data-ttu-id="34323-127">Przydatny w przypadku informacji, które mogą być wymagane przez klienta w danym wydaniu.</span><span class="sxs-lookup"><span data-stu-id="34323-127">Useful for information that your customer may need to see in the release.</span></span>
  - <span data-ttu-id="34323-128">Ponieważ jest to najprostsze podejście, jest ono często używane podczas tymczasowego debugowania ad hoc.</span><span class="sxs-lookup"><span data-stu-id="34323-128">Because it's the simplest approach, it's often used for ad-hoc temporary debugging.</span></span> <span data-ttu-id="34323-129">Często zdarza się, że ten kod debugowania nie jest nigdy zaewidencjonowany w ramach kontroli źródła.</span><span class="sxs-lookup"><span data-stu-id="34323-129">This debug code is often never checked in to source control.</span></span>
- <xref:System.Diagnostics.Trace?displayProperty=nameWithType>
  - <span data-ttu-id="34323-130">Włączony tylko w przypadku zdefiniowana elementu `TRACE`.</span><span class="sxs-lookup"><span data-stu-id="34323-130">Only enabled when `TRACE` is defined.</span></span>
  - <span data-ttu-id="34323-131">Domyślnie zapisy do załączenia <xref:System.Diagnostics.Trace.Listeners> <xref:System.Diagnostics.DefaultTraceListener> .</span><span class="sxs-lookup"><span data-stu-id="34323-131">Writes to attached <xref:System.Diagnostics.Trace.Listeners>, by default the <xref:System.Diagnostics.DefaultTraceListener>.</span></span>
  - <span data-ttu-id="34323-132">Użyj tego interfejsu API podczas tworzenia dzienników, które będą włączone w większości kompilacji.</span><span class="sxs-lookup"><span data-stu-id="34323-132">Use this API when creating logs that will be enabled in most builds.</span></span>
- <xref:System.Diagnostics.Debug?displayProperty=nameWithType>
  - <span data-ttu-id="34323-133">Włączony tylko w przypadku zdefiniowana elementu `DEBUG`.</span><span class="sxs-lookup"><span data-stu-id="34323-133">Only enabled when `DEBUG` is defined.</span></span>
  - <span data-ttu-id="34323-134">Zapisuje do dołączonego debugera.</span><span class="sxs-lookup"><span data-stu-id="34323-134">Writes to an attached debugger.</span></span>
  - <span data-ttu-id="34323-135">Przy `*nix` zapisie do stderr, jeśli `COMPlus_DebugWriteToStdErr` jest ustawiona.</span><span class="sxs-lookup"><span data-stu-id="34323-135">On `*nix` writes to stderr if `COMPlus_DebugWriteToStdErr` is set.</span></span>
  - <span data-ttu-id="34323-136">Użyj tego interfejsu API w przypadku tworzenia dzienników, które będą włączone tylko w kompilacjach debugowania.</span><span class="sxs-lookup"><span data-stu-id="34323-136">Use this API when creating logs that will be enabled only in debug builds.</span></span>

### <a name="logging-events"></a><span data-ttu-id="34323-137">Rejestrowanie zdarzeń</span><span class="sxs-lookup"><span data-stu-id="34323-137">Logging events</span></span>

<span data-ttu-id="34323-138">Poniższe interfejsy API są bardziej zorientowane na zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="34323-138">The following APIs are more event oriented.</span></span> <span data-ttu-id="34323-139">Zamiast rejestrowania prostych ciągów rejestruje obiekty zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="34323-139">Rather than logging simple strings they log event objects.</span></span>

- <xref:System.Diagnostics.Tracing.EventSource?displayProperty=nameWithType>
  - <span data-ttu-id="34323-140">EventSource jest podstawowym głównym interfejsem API śledzenia programu .NET Core.</span><span class="sxs-lookup"><span data-stu-id="34323-140">EventSource is the primary root .NET Core tracing API.</span></span>
  - <span data-ttu-id="34323-141">Dostępne we wszystkich wersjach .NET Standard.</span><span class="sxs-lookup"><span data-stu-id="34323-141">Available in all .NET Standard versions.</span></span>
  - <span data-ttu-id="34323-142">Umożliwia tylko śledzenie obiektów, które można serializować.</span><span class="sxs-lookup"><span data-stu-id="34323-142">Only allows tracing serializable objects.</span></span>
  - <span data-ttu-id="34323-143">Może być używany w procesie za pośrednictwem wszystkich wystąpień [odbiornika](xref:System.Diagnostics.Tracing.EventListener) skonfigurowanych do korzystania z EventSource.</span><span class="sxs-lookup"><span data-stu-id="34323-143">Can be consumed in-process via any [EventListener](xref:System.Diagnostics.Tracing.EventListener) instances configured to consume the EventSource.</span></span>
  - <span data-ttu-id="34323-144">Może być zużyte przez:</span><span class="sxs-lookup"><span data-stu-id="34323-144">Can be consumed out-of-process via:</span></span>
    - <span data-ttu-id="34323-145">[EventPipe platformy .NET Core](./eventpipe.md) na wszystkich platformach</span><span class="sxs-lookup"><span data-stu-id="34323-145">[.NET Core's EventPipe](./eventpipe.md) on all platforms</span></span>
    - [<span data-ttu-id="34323-146">Śledzenie zdarzeń systemu Windows (ETW)</span><span class="sxs-lookup"><span data-stu-id="34323-146">Event Tracing for Windows (ETW)</span></span>](/windows/win32/etw/event-tracing-portal)
    - [<span data-ttu-id="34323-147">LTTng — struktura śledzenia dla systemu Linux</span><span class="sxs-lookup"><span data-stu-id="34323-147">LTTng tracing framework for Linux</span></span>](https://lttng.org/)
      - <span data-ttu-id="34323-148">Przewodnik: [gromadzenie LTTng śledzenia przy użyciu PerfCollect](trace-perfcollect-lttng.md).</span><span class="sxs-lookup"><span data-stu-id="34323-148">Walkthrough: [Collect an LTTng trace using PerfCollect](trace-perfcollect-lttng.md).</span></span>

- <xref:System.Diagnostics.DiagnosticSource?displayProperty=nameWithType>
  - <span data-ttu-id="34323-149">Zawarte w oprogramowaniu .NET Core i jako [pakiet NuGet](https://www.nuget.org/packages/System.Diagnostics.DiagnosticSource) dla .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="34323-149">Included in .NET Core and as a [NuGet package](https://www.nuget.org/packages/System.Diagnostics.DiagnosticSource) for .NET Framework.</span></span>
  - <span data-ttu-id="34323-150">Umożliwia śledzenie w procesie obiektów, które nie są możliwe do serializacji.</span><span class="sxs-lookup"><span data-stu-id="34323-150">Allows in-process tracing of non-serializable objects.</span></span>
  - <span data-ttu-id="34323-151">Zawiera mostek umożliwiający Zapisywanie wybranych pól zarejestrowanych obiektów w usłudze <xref:System.Diagnostics.Tracing.EventSource> .</span><span class="sxs-lookup"><span data-stu-id="34323-151">Includes a bridge to allow selected fields of logged objects to be written to an <xref:System.Diagnostics.Tracing.EventSource>.</span></span>

- <xref:System.Diagnostics.Activity?displayProperty=nameWithType>
  - <span data-ttu-id="34323-152">Przedstawia ostateczny sposób identyfikowania komunikatów dziennika pochodzących z określonego działania lub transakcji.</span><span class="sxs-lookup"><span data-stu-id="34323-152">Provides a definitive way to identify log messages resulting from a specific activity or transaction.</span></span> <span data-ttu-id="34323-153">Ten obiekt może służyć do skorelowania dzienników w różnych usługach.</span><span class="sxs-lookup"><span data-stu-id="34323-153">This object can be used to correlate logs across different services.</span></span>

- <xref:System.Diagnostics.EventLog?displayProperty=nameWithType>
  - <span data-ttu-id="34323-154">Tylko system Windows.</span><span class="sxs-lookup"><span data-stu-id="34323-154">Windows only.</span></span>
  - <span data-ttu-id="34323-155">Zapisuje komunikaty w dzienniku zdarzeń systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="34323-155">Writes messages to the Windows Event Log.</span></span>
  - <span data-ttu-id="34323-156">Administratorzy systemu oczekują krytycznych komunikatów o błędach aplikacji w dzienniku zdarzeń systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="34323-156">System administrators expect fatal application error messages to appear in the Windows Event Log.</span></span>

## <a name="ilogger-and-logging-frameworks"></a><span data-ttu-id="34323-157">ILogger i struktury rejestrowania</span><span class="sxs-lookup"><span data-stu-id="34323-157">ILogger and logging frameworks</span></span>

<span data-ttu-id="34323-158">Interfejsy API niskiego poziomu mogą nie być właściwym wyborem dla potrzeb rejestrowania.</span><span class="sxs-lookup"><span data-stu-id="34323-158">The low-level APIs may not be the right choice for your logging needs.</span></span> <span data-ttu-id="34323-159">Warto rozważyć strukturę rejestrowania.</span><span class="sxs-lookup"><span data-stu-id="34323-159">You may want to consider a logging framework.</span></span>

<span data-ttu-id="34323-160"><xref:Microsoft.Extensions.Logging.ILogger>Interfejs został użyty do utworzenia wspólnego interfejsu rejestrowania, w którym rejestratory mogą być wstawiane przez iniekcję zależności.</span><span class="sxs-lookup"><span data-stu-id="34323-160">The <xref:Microsoft.Extensions.Logging.ILogger> interface has been used to create a common logging interface where the loggers can be inserted through dependency injection.</span></span>

<span data-ttu-id="34323-161">Na przykład, aby umożliwić wybranie najlepszego wyboru dla aplikacji .NET, zapewnia obsługę wybranych platform wbudowanych i innych firm:</span><span class="sxs-lookup"><span data-stu-id="34323-161">For instance, to allow you to make the best choice for your application .NET offers support for a selection of built-in and third-party frameworks:</span></span>

- [<span data-ttu-id="34323-162">Dostawcy wbudowanego rejestrowania platformy .NET</span><span class="sxs-lookup"><span data-stu-id="34323-162">.NET Built-in logging providers</span></span>](../extensions/logging-providers.md#built-in-logging-providers)
- [<span data-ttu-id="34323-163">Dostawcy rejestrowania .NET innych firm</span><span class="sxs-lookup"><span data-stu-id="34323-163">.NET Third-party logging providers</span></span>](../extensions/logging-providers.md#third-party-logging-providers)

## <a name="logging-related-references"></a><span data-ttu-id="34323-164">Rejestrowanie powiązanych odwołań</span><span class="sxs-lookup"><span data-stu-id="34323-164">Logging related references</span></span>

- [<span data-ttu-id="34323-165">Instrukcje: Kompilowanie warunkowe ze śledzeniem i debugowaniem</span><span class="sxs-lookup"><span data-stu-id="34323-165">How to: Compile Conditionally with Trace and Debug</span></span>](../../framework/debug-trace-profile/how-to-compile-conditionally-with-trace-and-debug.md)

- [<span data-ttu-id="34323-166">Instrukcje: Dodawanie instrukcji śledzenia do kodu aplikacji</span><span class="sxs-lookup"><span data-stu-id="34323-166">How to: Add Trace Statements to Application Code</span></span>](../../framework/debug-trace-profile/how-to-add-trace-statements-to-application-code.md)

- <span data-ttu-id="34323-167">[Rejestrowanie w programie .NET](../extensions/logging.md) zawiera omówienie technik rejestrowania, które obsługuje.</span><span class="sxs-lookup"><span data-stu-id="34323-167">[Logging in .NET](../extensions/logging.md) provides an overview of the logging techniques it supports.</span></span>

- <span data-ttu-id="34323-168">[Interpolacja ciągów języka C#](../../csharp/language-reference/tokens/interpolated.md) może uprościć pisanie kodu rejestrowania.</span><span class="sxs-lookup"><span data-stu-id="34323-168">[C# string interpolation](../../csharp/language-reference/tokens/interpolated.md) can simplify writing logging code.</span></span>

- <span data-ttu-id="34323-169"><xref:System.Exception.Message?displayProperty=nameWithType>Właściwość jest przydatna do rejestrowania wyjątków.</span><span class="sxs-lookup"><span data-stu-id="34323-169">The <xref:System.Exception.Message?displayProperty=nameWithType> property is useful for logging exceptions.</span></span>

- <span data-ttu-id="34323-170"><xref:System.Diagnostics.StackTrace?displayProperty=nameWithType>Klasa może być przydatna do dostarczania informacji o stosie w dziennikach.</span><span class="sxs-lookup"><span data-stu-id="34323-170">The <xref:System.Diagnostics.StackTrace?displayProperty=nameWithType> class can be useful to provide stack info in your logs.</span></span>

## <a name="performance-considerations"></a><span data-ttu-id="34323-171">Zagadnienia dotyczące wydajności</span><span class="sxs-lookup"><span data-stu-id="34323-171">Performance considerations</span></span>

<span data-ttu-id="34323-172">Formatowanie ciągu może mieć zauważalny czas przetwarzania procesora CPU.</span><span class="sxs-lookup"><span data-stu-id="34323-172">String formatting can take noticeable CPU processing time.</span></span>

<span data-ttu-id="34323-173">W przypadku aplikacji o krytycznym znaczeniu zaleca się:</span><span class="sxs-lookup"><span data-stu-id="34323-173">In performance critical applications, it's recommended that you:</span></span>

- <span data-ttu-id="34323-174">Unikaj wielu rejestracji, gdy nikt nie nasłuchuje.</span><span class="sxs-lookup"><span data-stu-id="34323-174">Avoid lots of logging when no one is listening.</span></span> <span data-ttu-id="34323-175">Unikaj konstruowania kosztownych komunikatów rejestrowania, sprawdzając, czy rejestrowanie jest włączone jako pierwsze.</span><span class="sxs-lookup"><span data-stu-id="34323-175">Avoid constructing costly logging messages by checking if logging is enabled first.</span></span>
- <span data-ttu-id="34323-176">Rejestruj tylko to, co jest przydatne.</span><span class="sxs-lookup"><span data-stu-id="34323-176">Only log what's useful.</span></span>
- <span data-ttu-id="34323-177">Odłóż ozdobne formatowanie do etapu analizy.</span><span class="sxs-lookup"><span data-stu-id="34323-177">Defer fancy formatting to the analysis stage.</span></span>
