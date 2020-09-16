---
title: Zbieranie danych telemetrycznych za pomocą interfejsu wiersza polecenia ML.NET
description: Dowiedz się więcej o funkcjach telemetrycznych interfejsu wiersza polecenia ML.NET, które zbierają informacje o użyciu do analizy, zbierane dane i jak je wyłączyć. Znajdź także linki do umowy licencyjnej platformy .NET oraz informacje o zgodności z programem Microsoft Rodo.
ms.topic: conceptual
ms.date: 06/03/2020
ms.custom: mlnet-tooling
ms.openlocfilehash: 753361abdac5a2e979873003f419232a069b2015
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/15/2020
ms.locfileid: "90546435"
---
# <a name="telemetry-collection-by-the-mlnet-cli"></a><span data-ttu-id="7836e-104">Zbieranie danych telemetrycznych za pomocą interfejsu wiersza polecenia ML.NET</span><span class="sxs-lookup"><span data-stu-id="7836e-104">Telemetry collection by the ML.NET CLI</span></span>

<span data-ttu-id="7836e-105">[Interfejs wiersza polecenia ml.NET](../automate-training-with-cli.md) zawiera funkcję telemetrii, która zbiera anonimowe dane użycia, które są agregowane na użytek firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="7836e-105">The [ML.NET CLI](../automate-training-with-cli.md) includes a telemetry feature that collects anonymous usage data that is aggregated for use by Microsoft.</span></span>

## <a name="how-microsoft-uses-the-data"></a><span data-ttu-id="7836e-106">Jak firma Microsoft używa danych</span><span class="sxs-lookup"><span data-stu-id="7836e-106">How Microsoft uses the data</span></span>

<span data-ttu-id="7836e-107">Zespół produktu używa danych telemetrycznych interfejsu wiersza polecenia ML.NET, aby pomóc zrozumieć, jak ulepszyć narzędzia.</span><span class="sxs-lookup"><span data-stu-id="7836e-107">The product team uses ML.NET CLI telemetry data to help understand how to improve the tools.</span></span> <span data-ttu-id="7836e-108">Na przykład jeśli klienci rzadko wykorzystują określone zadanie uczenia maszynowego, zespół produktu bada dlaczego i korzysta z wyników, aby określić priorytety projektowania funkcji.</span><span class="sxs-lookup"><span data-stu-id="7836e-108">For example, if customers infrequently use a particular machine learning task, the product team investigates why and uses findings to prioritize feature development.</span></span> <span data-ttu-id="7836e-109">Dane telemetryczne interfejsu wiersza polecenia ML.NET pomagają również debugować problemy, takie jak awarie i anomalie w kodzie.</span><span class="sxs-lookup"><span data-stu-id="7836e-109">ML.NET CLI telemetry also helps with debugging of issues such as crashes and code anomalies.</span></span>

<span data-ttu-id="7836e-110">Gdy zespół produktu docenia ten wgląd, wie również, że nie wszyscy chcą wysyłać te dane.</span><span class="sxs-lookup"><span data-stu-id="7836e-110">While the product team appreciates this insight, we also know that not everyone wants to send this data.</span></span> [<span data-ttu-id="7836e-111">Dowiedz się, jak wyłączyć telemetrię.</span><span class="sxs-lookup"><span data-stu-id="7836e-111">Find out how to disable telemetry.</span></span>](#opt-out-of-data-collection)

## <a name="scope"></a><span data-ttu-id="7836e-112">Zakres</span><span class="sxs-lookup"><span data-stu-id="7836e-112">Scope</span></span>

<span data-ttu-id="7836e-113">`mlnet`Polecenie uruchamia interfejs wiersza polecenia ml.NET, ale samo polecenie nie zbiera danych telemetrycznych.</span><span class="sxs-lookup"><span data-stu-id="7836e-113">The `mlnet` command launches the ML.NET CLI, but the command itself doesn't collect telemetry.</span></span>

<span data-ttu-id="7836e-114">Funkcja telemetrii *nie jest włączona* po uruchomieniu `mlnet` polecenia bez innego dołączonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="7836e-114">Telemetry *isn't enabled* when you run the `mlnet` command with no other command attached.</span></span> <span data-ttu-id="7836e-115">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="7836e-115">For example:</span></span>

- `mlnet`
- `mlnet --help`

<span data-ttu-id="7836e-116">Funkcja telemetrii *jest włączona* po uruchomieniu [polecenia ml.NET CLI](../reference/ml-net-cli-reference.md), takiego jak `mlnet classification` .</span><span class="sxs-lookup"><span data-stu-id="7836e-116">Telemetry *is enabled* when you run an [ML.NET CLI command](../reference/ml-net-cli-reference.md), such as `mlnet classification`.</span></span>

## <a name="opt-out-of-data-collection"></a><span data-ttu-id="7836e-117">Rezygnacja z zbierania danych</span><span class="sxs-lookup"><span data-stu-id="7836e-117">Opt out of data collection</span></span>

<span data-ttu-id="7836e-118">Funkcja telemetrii interfejsu wiersza polecenia ML.NET jest domyślnie włączona.</span><span class="sxs-lookup"><span data-stu-id="7836e-118">The ML.NET CLI telemetry feature is enabled by default.</span></span>

<span data-ttu-id="7836e-119">Rezygnacja z funkcji telemetrii przez ustawienie `MLDOTNET_CLI_TELEMETRY_OPTOUT` zmiennej środowiskowej na `1` lub `true` .</span><span class="sxs-lookup"><span data-stu-id="7836e-119">Opt out of the telemetry feature by setting the `MLDOTNET_CLI_TELEMETRY_OPTOUT` environment variable to `1` or `true`.</span></span> <span data-ttu-id="7836e-120">Ta zmienna środowiskowa jest stosowana globalnie do narzędzia interfejsu wiersza polecenia ML.NET.</span><span class="sxs-lookup"><span data-stu-id="7836e-120">This environment variable applies globally to the ML.NET CLI tool.</span></span>

## <a name="data-points-collected"></a><span data-ttu-id="7836e-121">Zebrane punkty danych</span><span class="sxs-lookup"><span data-stu-id="7836e-121">Data points collected</span></span>

<span data-ttu-id="7836e-122">Funkcja zbiera następujące dane:</span><span class="sxs-lookup"><span data-stu-id="7836e-122">The feature collects the following data:</span></span>

- <span data-ttu-id="7836e-123">Jakie polecenie zostało wywołane, na przykład `classification`</span><span class="sxs-lookup"><span data-stu-id="7836e-123">What command was invoked, such as `classification`</span></span>
- <span data-ttu-id="7836e-124">Używane nazwy parametrów wiersza polecenia (czyli "DataSet, etykieta-Kol, wyjście-ścieżka, czas uczenia, poziom szczegółowości")</span><span class="sxs-lookup"><span data-stu-id="7836e-124">Command-line parameter names used (that is, "dataset, label-col, output-path, train-time, verbosity")</span></span>
- <span data-ttu-id="7836e-125">Skrótowy adres MAC: kryptograficzny (SHA256) anonimowy i unikatowy identyfikator dla komputera</span><span class="sxs-lookup"><span data-stu-id="7836e-125">Hashed MAC address: a cryptographically (SHA256) anonymous and unique ID for a machine</span></span>
- <span data-ttu-id="7836e-126">Sygnatura czasowa wywołania</span><span class="sxs-lookup"><span data-stu-id="7836e-126">Timestamp of an invocation</span></span>
- <span data-ttu-id="7836e-127">Trzy oktetowe adresy IP (nie pełny adres IP) używane tylko do określania lokalizacji geograficznej</span><span class="sxs-lookup"><span data-stu-id="7836e-127">Three octet IP address (not full IP address) used only to determine geographical location</span></span>
- <span data-ttu-id="7836e-128">Nazwa wszystkich używanych argumentów/parametrów.</span><span class="sxs-lookup"><span data-stu-id="7836e-128">Name of all arguments/parameters used.</span></span> <span data-ttu-id="7836e-129">Nie wartości klienta, takie jak ciągi</span><span class="sxs-lookup"><span data-stu-id="7836e-129">Not the customer's values, such as strings</span></span>
- <span data-ttu-id="7836e-130">Nazwa pliku zestawu danych skrótów</span><span class="sxs-lookup"><span data-stu-id="7836e-130">Hashed dataset filename</span></span>
- <span data-ttu-id="7836e-131">Zasobnik rozmiaru pliku zestawu danych</span><span class="sxs-lookup"><span data-stu-id="7836e-131">Dataset file-size bucket</span></span>
- <span data-ttu-id="7836e-132">System operacyjny i wersja</span><span class="sxs-lookup"><span data-stu-id="7836e-132">Operating system and version</span></span>
- <span data-ttu-id="7836e-133">Wartość ML polecenia zadania: kategorii wartości, takie jak `regression` , `classification` i `recommendation`</span><span class="sxs-lookup"><span data-stu-id="7836e-133">Value of ML task commands: Categorical values, such as `regression`, `classification`, and `recommendation`</span></span>
- <span data-ttu-id="7836e-134">Wersja interfejsu wiersza polecenia ML.NET (0.3.27703.4)</span><span class="sxs-lookup"><span data-stu-id="7836e-134">ML.NET CLI version (that is, 0.3.27703.4)</span></span>

<span data-ttu-id="7836e-135">Dane są bezpiecznie przesyłane do serwerów firmy Microsoft przy użyciu technologii [Application Insights platformy Azure](https://azure.microsoft.com/services/application-insights/) , w ramach ograniczonego dostępu i stosowane w ramach ścisłej kontroli zabezpieczeń z bezpiecznych systemów [usługi Azure Storage](https://azure.microsoft.com/services/storage/) .</span><span class="sxs-lookup"><span data-stu-id="7836e-135">The data is sent securely to Microsoft servers using [Azure Application Insights](https://azure.microsoft.com/services/application-insights/) technology, held under restricted access, and used under strict security controls from secure [Azure Storage](https://azure.microsoft.com/services/storage/) systems.</span></span>

### <a name="data-points-not-collected"></a><span data-ttu-id="7836e-136">Punkty danych nie są zbierane</span><span class="sxs-lookup"><span data-stu-id="7836e-136">Data points not collected</span></span>

<span data-ttu-id="7836e-137">Funkcja telemetrii *nie* zbiera:</span><span class="sxs-lookup"><span data-stu-id="7836e-137">The telemetry feature *doesn't* collect:</span></span>

- <span data-ttu-id="7836e-138">dane osobowe, takie jak nazwy użytkowników</span><span class="sxs-lookup"><span data-stu-id="7836e-138">personal data, such as usernames</span></span>
- <span data-ttu-id="7836e-139">nazwy plików DataSet</span><span class="sxs-lookup"><span data-stu-id="7836e-139">dataset filenames</span></span>
- <span data-ttu-id="7836e-140">dane z plików DataSet</span><span class="sxs-lookup"><span data-stu-id="7836e-140">data from dataset files</span></span>

<span data-ttu-id="7836e-141">Jeśli podejrzewasz, że Telemetria interfejsu wiersza polecenia ML.NET zbiera poufne dane lub że dane są w sposób niezabezpieczony lub niewłaściwie obsłużony, należy rozwiązać problem w repozytorium [ml.NET](https://github.com/dotnet/machinelearning) w celu zbadania.</span><span class="sxs-lookup"><span data-stu-id="7836e-141">If you suspect that the ML.NET CLI telemetry is collecting sensitive data or that the data is being insecurely or inappropriately handled, file an issue in the [ML.NET](https://github.com/dotnet/machinelearning) repository for investigation.</span></span>

## <a name="license"></a><span data-ttu-id="7836e-142">Licencja</span><span class="sxs-lookup"><span data-stu-id="7836e-142">License</span></span>

<span data-ttu-id="7836e-143">ML.NET interfejs wiersza polecenia firmy Microsoft do dystrybucji jest licencjonowany za pomocą [postanowień licencyjnych dotyczących oprogramowania firmy Microsoft: biblioteka Microsoft .NET](https://aka.ms/dotnet-core-eula).</span><span class="sxs-lookup"><span data-stu-id="7836e-143">The Microsoft distribution of ML.NET CLI is licensed with the [Microsoft Software License Terms: Microsoft .NET Library](https://aka.ms/dotnet-core-eula).</span></span> <span data-ttu-id="7836e-144">Aby uzyskać szczegółowe informacje na temat zbierania i przetwarzania danych, zobacz sekcję zatytułowaną "dane".</span><span class="sxs-lookup"><span data-stu-id="7836e-144">For details on data collection and processing, see the section entitled "Data."</span></span>

## <a name="disclosure"></a><span data-ttu-id="7836e-145">Mogąc</span><span class="sxs-lookup"><span data-stu-id="7836e-145">Disclosure</span></span>

<span data-ttu-id="7836e-146">Gdy po raz pierwszy uruchomisz [polecenie interfejsu wiersza polecenia ml.NET](../reference/ml-net-cli-reference.md) , takie jak `mlnet classification` , narzędzie ml.NET CLI wyświetla tekst, który informuje, jak zrezygnować z telemetrii.</span><span class="sxs-lookup"><span data-stu-id="7836e-146">When you first run a [ML.NET CLI command](../reference/ml-net-cli-reference.md) such as `mlnet classification`, the ML.NET CLI tool displays disclosure text that tells you how to opt out of telemetry.</span></span> <span data-ttu-id="7836e-147">Tekst może się nieco różnić w zależności od używanej wersji interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="7836e-147">Text may vary slightly depending on the version of the CLI you're running.</span></span>

## <a name="see-also"></a><span data-ttu-id="7836e-148">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="7836e-148">See also</span></span>

- [<span data-ttu-id="7836e-149">Dokumentacja interfejsu wiersza polecenia ML.NET</span><span class="sxs-lookup"><span data-stu-id="7836e-149">ML.NET CLI reference</span></span>](../reference/ml-net-cli-reference.md)
- [<span data-ttu-id="7836e-150">Postanowienia licencyjne dotyczące oprogramowania firmy Microsoft: Biblioteka Microsoft .NET</span><span class="sxs-lookup"><span data-stu-id="7836e-150">Microsoft Software License Terms: Microsoft .NET Library</span></span>](https://aka.ms/dotnet-core-eula)
- [<span data-ttu-id="7836e-151">Prywatność w firmie Microsoft</span><span class="sxs-lookup"><span data-stu-id="7836e-151">Privacy at Microsoft</span></span>](https://www.microsoft.com/trustcenter/privacy/)
- [<span data-ttu-id="7836e-152">Oświadczenie o ochronie prywatności w firmie Microsoft</span><span class="sxs-lookup"><span data-stu-id="7836e-152">Microsoft Privacy Statement</span></span>](https://privacy.microsoft.com/privacystatement)
