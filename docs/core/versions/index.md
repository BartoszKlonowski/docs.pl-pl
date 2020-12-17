---
title: Jak są używane wersje środowiska uruchomieniowego .NET i zestawu SDK
description: W tym artykule wyjaśniono, jak są używane wersje zestawu .NET SDK i środowiska uruchomieniowego (podobnie jak w przypadku wersji semantycznej).
ms.date: 12/07/2020
ms.openlocfilehash: 2fbc2775f31b4eab1c9883282c58accd9bb2b9f5
ms.sourcegitcommit: 635a0ff775d2447a81ef7233a599b8f88b162e5d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/17/2020
ms.locfileid: "97633627"
---
# <a name="overview-of-how-net-is-versioned"></a><span data-ttu-id="1255d-103">Omówienie wersji platformy .NET</span><span class="sxs-lookup"><span data-stu-id="1255d-103">Overview of how .NET is versioned</span></span>

<span data-ttu-id="1255d-104">[Środowisko uruchomieniowe platformy .NET i zestaw SDK platformy .NET](../introduction.md#sdk-and-runtimes) dodają nowe funkcje przy użyciu różnych częstotliwości.</span><span class="sxs-lookup"><span data-stu-id="1255d-104">The [.NET Runtime and the .NET SDK](../introduction.md#sdk-and-runtimes) add new features at different frequencies.</span></span> <span data-ttu-id="1255d-105">Ogólnie rzecz biorąc, zestaw SDK jest aktualizowany częściej niż środowisko uruchomieniowe.</span><span class="sxs-lookup"><span data-stu-id="1255d-105">In general, the SDK is updated more frequently than the Runtime.</span></span> <span data-ttu-id="1255d-106">W tym artykule opisano środowisko uruchomieniowe i numery wersji zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="1255d-106">This article explains the runtime and the SDK version numbers.</span></span>

## <a name="versioning-details"></a><span data-ttu-id="1255d-107">Szczegóły dotyczące wersji</span><span class="sxs-lookup"><span data-stu-id="1255d-107">Versioning details</span></span>

<span data-ttu-id="1255d-108">Środowisko uruchomieniowe platformy .NET ma rozwiązane główne/drobne/poprawka do wersji, która następuje po [wersji semantycznej](#semantic-versioning).</span><span class="sxs-lookup"><span data-stu-id="1255d-108">The .NET Runtime has a major/minor/patch approach to versioning that follows [semantic versioning](#semantic-versioning).</span></span>

<span data-ttu-id="1255d-109">Zestaw SDK platformy .NET nie jest zgodny z wersją semantyczną.</span><span class="sxs-lookup"><span data-stu-id="1255d-109">The .NET SDK doesn't follow semantic versioning.</span></span> <span data-ttu-id="1255d-110">Zestaw SDK platformy .NET jest szybszy, a jego numery wersji muszą komunikować się z wyrównanym środowiskiem uruchomieniowym i wersjami pomocniczymi i poprawkami zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="1255d-110">The .NET SDK releases faster and its version numbers must communicate both the aligned runtime and the SDK's own minor and patch releases.</span></span>

<span data-ttu-id="1255d-111">Pierwsze dwa pozycje numeru wersji zestawu .NET SDK są blokowane w wersji środowiska uruchomieniowego .NET wydanej w programie.</span><span class="sxs-lookup"><span data-stu-id="1255d-111">The first two positions of the .NET SDK version number are locked to the .NET Runtime version it released with.</span></span> <span data-ttu-id="1255d-112">Każda wersja zestawu SDK może tworzyć aplikacje dla tego środowiska uruchomieniowego lub dowolnej niższej wersji.</span><span class="sxs-lookup"><span data-stu-id="1255d-112">Each version of the SDK can create applications for this runtime or any lower version.</span></span>

<span data-ttu-id="1255d-113">Trzecia pozycja numeru wersji zestawu SDK komunikuje się zarówno z literą, jak i numerem poprawki.</span><span class="sxs-lookup"><span data-stu-id="1255d-113">The third position of the SDK version number communicates both the minor and patch number.</span></span> <span data-ttu-id="1255d-114">Wersja pomocnicza jest mnożona przez 100.</span><span class="sxs-lookup"><span data-stu-id="1255d-114">The minor version is multiplied by 100.</span></span> <span data-ttu-id="1255d-115">Ostatnie dwie cyfry reprezentują numer poprawki.</span><span class="sxs-lookup"><span data-stu-id="1255d-115">The final two digits represent the patch number.</span></span> <span data-ttu-id="1255d-116">Wersja pomocnicza 1, Poprawka wersja 2 byłaby reprezentowana jako 102.</span><span class="sxs-lookup"><span data-stu-id="1255d-116">Minor version 1, patch version 2 would be represented as 102.</span></span> <span data-ttu-id="1255d-117">Na przykład Oto możliwa sekwencja numerów wersji środowiska uruchomieniowego i zestawu SDK:</span><span class="sxs-lookup"><span data-stu-id="1255d-117">For example, here's a possible sequence of runtime and SDK version numbers:</span></span>

| <span data-ttu-id="1255d-118">Zmiana</span><span class="sxs-lookup"><span data-stu-id="1255d-118">Change</span></span>                | <span data-ttu-id="1255d-119">Środowisko uruchomieniowe platformy .NET</span><span class="sxs-lookup"><span data-stu-id="1255d-119">.NET Runtime</span></span>      | <span data-ttu-id="1255d-120">zestaw SDK platformy .NET ( \* )</span><span class="sxs-lookup"><span data-stu-id="1255d-120">.NET SDK (\*)</span></span>     |
|-----------------------|-------------------|-------------------|
| <span data-ttu-id="1255d-121">Wersja początkowa</span><span class="sxs-lookup"><span data-stu-id="1255d-121">Initial release</span></span>       | <span data-ttu-id="1255d-122">2.2.0</span><span class="sxs-lookup"><span data-stu-id="1255d-122">2.2.0</span></span>             | <span data-ttu-id="1255d-123">2.2.100</span><span class="sxs-lookup"><span data-stu-id="1255d-123">2.2.100</span></span>           |
| <span data-ttu-id="1255d-124">Poprawka zestawu SDK</span><span class="sxs-lookup"><span data-stu-id="1255d-124">SDK patch</span></span>             | <span data-ttu-id="1255d-125">2.2.0</span><span class="sxs-lookup"><span data-stu-id="1255d-125">2.2.0</span></span>             | <span data-ttu-id="1255d-126">2.2.101</span><span class="sxs-lookup"><span data-stu-id="1255d-126">2.2.101</span></span>           |
| <span data-ttu-id="1255d-127">Środowisko uruchomieniowe i poprawka zestawu SDK</span><span class="sxs-lookup"><span data-stu-id="1255d-127">Runtime and SDK patch</span></span> | <span data-ttu-id="1255d-128">2.2.1</span><span class="sxs-lookup"><span data-stu-id="1255d-128">2.2.1</span></span>             | <span data-ttu-id="1255d-129">2.2.102</span><span class="sxs-lookup"><span data-stu-id="1255d-129">2.2.102</span></span>           |
| <span data-ttu-id="1255d-130">Zmiana funkcji zestawu SDK</span><span class="sxs-lookup"><span data-stu-id="1255d-130">SDK feature change</span></span>    | <span data-ttu-id="1255d-131">2.2.1</span><span class="sxs-lookup"><span data-stu-id="1255d-131">2.2.1</span></span>             | <span data-ttu-id="1255d-132">2.2.200</span><span class="sxs-lookup"><span data-stu-id="1255d-132">2.2.200</span></span>           |

<span data-ttu-id="1255d-133">O</span><span class="sxs-lookup"><span data-stu-id="1255d-133">NOTES:</span></span>

- <span data-ttu-id="1255d-134">Jeśli zestaw SDK ma 10 aktualizacji funkcji przed aktualizacją funkcji środowiska uruchomieniowego, numery wersji są przydzielone do serii 1000 z liczbami takimi jak 2.2.1000 jako wersja funkcji po 2.2.900.</span><span class="sxs-lookup"><span data-stu-id="1255d-134">If the SDK has 10 feature updates before a runtime feature update, version numbers roll into the 1000 series with numbers like 2.2.1000 as the feature release following 2.2.900.</span></span> <span data-ttu-id="1255d-135">Ta sytuacja nie powinna wystąpić.</span><span class="sxs-lookup"><span data-stu-id="1255d-135">This situation isn't expected to occur.</span></span>
- <span data-ttu-id="1255d-136">99 wersje poprawek bez wydania funkcji nie zostaną wykonane.</span><span class="sxs-lookup"><span data-stu-id="1255d-136">99 patch releases without a feature release won't occur.</span></span> <span data-ttu-id="1255d-137">Jeśli wersja zbliża się do tej liczby, wymusza wydanie funkcji.</span><span class="sxs-lookup"><span data-stu-id="1255d-137">If a release approaches this number, it forces a feature release.</span></span>

<span data-ttu-id="1255d-138">Więcej szczegółów można znaleźć w wstępnej propozycji w repozytorium [dotnet/Designing](https://github.com/dotnet/designs/pull/29) .</span><span class="sxs-lookup"><span data-stu-id="1255d-138">You can see more details in the initial proposal at the [dotnet/designs](https://github.com/dotnet/designs/pull/29) repository.</span></span>

## <a name="semantic-versioning"></a><span data-ttu-id="1255d-139">Semantyczna obsługa wersji</span><span class="sxs-lookup"><span data-stu-id="1255d-139">Semantic versioning</span></span>

<span data-ttu-id="1255d-140">*Środowisko uruchomieniowe* platformy .NET jest ściśle zgodne z [wersją semantyki (SemVer)](https://semver.org/), `MAJOR.MINOR.PATCH` przy użyciu różnych części numeru wersji do opisania stopnia i typu zmiany.</span><span class="sxs-lookup"><span data-stu-id="1255d-140">The .NET *Runtime* roughly adheres to [Semantic Versioning (SemVer)](https://semver.org/), adopting the use of `MAJOR.MINOR.PATCH` versioning, using the various parts of the version number to describe the degree and type of change.</span></span>

```
MAJOR.MINOR.PATCH[-PRERELEASE-BUILDNUMBER]
```

<span data-ttu-id="1255d-141">Opcjonalne `PRERELEASE` i `BUILDNUMBER` części nie są nigdy częścią obsługiwanych wersji i istnieją tylko w przypadku nocnych kompilacji, lokalne kompilacje ze źródłowych elementów docelowych i nieobsługiwane wersje wersji zapoznawczej.</span><span class="sxs-lookup"><span data-stu-id="1255d-141">The optional `PRERELEASE` and `BUILDNUMBER` parts are never part of supported releases and only exist on nightly builds, local builds from source targets, and unsupported preview releases.</span></span>

### <a name="understand-runtime-version-number-changes"></a><span data-ttu-id="1255d-142">Informacje o zmianach numeru wersji środowiska uruchomieniowego</span><span class="sxs-lookup"><span data-stu-id="1255d-142">Understand runtime version number changes</span></span>

<span data-ttu-id="1255d-143">`MAJOR` jest zwiększana, gdy:</span><span class="sxs-lookup"><span data-stu-id="1255d-143">`MAJOR` is incremented when:</span></span>

- <span data-ttu-id="1255d-144">Wprowadzono znaczące zmiany w produkcie lub nowy kierunek produktu.</span><span class="sxs-lookup"><span data-stu-id="1255d-144">Significant changes occur to the product, or a new product direction.</span></span>
- <span data-ttu-id="1255d-145">Wprowadzono istotne zmiany.</span><span class="sxs-lookup"><span data-stu-id="1255d-145">Breaking changes were taken.</span></span> <span data-ttu-id="1255d-146">Istnieje wysoki poziom akceptowania istotnych zmian.</span><span class="sxs-lookup"><span data-stu-id="1255d-146">There's a high bar to accepting breaking changes.</span></span>
- <span data-ttu-id="1255d-147">Stara wersja nie jest już obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="1255d-147">An old version is no longer supported.</span></span>
- <span data-ttu-id="1255d-148">`MAJOR`Przyjęto nowszą wersję istniejącej zależności.</span><span class="sxs-lookup"><span data-stu-id="1255d-148">A newer `MAJOR` version of an existing dependency is adopted.</span></span>

<span data-ttu-id="1255d-149">`MINOR` jest zwiększana, gdy:</span><span class="sxs-lookup"><span data-stu-id="1255d-149">`MINOR` is incremented when:</span></span>

- <span data-ttu-id="1255d-150">Dodano publiczny obszar powierzchni interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="1255d-150">Public API surface area is added.</span></span>
- <span data-ttu-id="1255d-151">Zostanie dodane nowe zachowanie.</span><span class="sxs-lookup"><span data-stu-id="1255d-151">A new behavior is added.</span></span>
- <span data-ttu-id="1255d-152">`MINOR`Przyjęto nowszą wersję istniejącej zależności.</span><span class="sxs-lookup"><span data-stu-id="1255d-152">A newer `MINOR` version of an existing dependency is adopted.</span></span>
- <span data-ttu-id="1255d-153">Zostanie wprowadzona nowa zależność.</span><span class="sxs-lookup"><span data-stu-id="1255d-153">A new dependency is introduced.</span></span>

<span data-ttu-id="1255d-154">`PATCH` jest zwiększana, gdy:</span><span class="sxs-lookup"><span data-stu-id="1255d-154">`PATCH` is incremented when:</span></span>

- <span data-ttu-id="1255d-155">Wprowadzono poprawki błędów.</span><span class="sxs-lookup"><span data-stu-id="1255d-155">Bug fixes are made.</span></span>
- <span data-ttu-id="1255d-156">Dodano obsługę nowszej platformy.</span><span class="sxs-lookup"><span data-stu-id="1255d-156">Support for a newer platform is added.</span></span>
- <span data-ttu-id="1255d-157">`PATCH`Przyjęto nowszą wersję istniejącej zależności.</span><span class="sxs-lookup"><span data-stu-id="1255d-157">A newer `PATCH` version of an existing dependency is adopted.</span></span>
- <span data-ttu-id="1255d-158">Jakakolwiek inna zmiana nie pasuje do jednego z poprzednich przypadków.</span><span class="sxs-lookup"><span data-stu-id="1255d-158">Any other change doesn't fit one of the previous cases.</span></span>

<span data-ttu-id="1255d-159">W przypadku zmiany wielu zmian najwyższy element, na który wpływają poszczególne zmiany, jest zwiększany, a następujące są resetowane do zera.</span><span class="sxs-lookup"><span data-stu-id="1255d-159">When there are multiple changes, the highest element affected by individual changes is incremented, and the following ones are reset to zero.</span></span> <span data-ttu-id="1255d-160">Na przykład gdy `MAJOR` jest zwiększana, `MINOR` i `PATCH` są resetowane do zera.</span><span class="sxs-lookup"><span data-stu-id="1255d-160">For example, when `MAJOR` is incremented, `MINOR` and `PATCH` are reset to zero.</span></span> <span data-ttu-id="1255d-161">Gdy `MINOR` jest zwiększana, `PATCH` jest resetowana do zera, podczas gdy pozostaje `MAJOR` nienaruszony.</span><span class="sxs-lookup"><span data-stu-id="1255d-161">When `MINOR` is incremented, `PATCH` is reset to zero while `MAJOR` is left untouched.</span></span>

## <a name="version-numbers-in-file-names"></a><span data-ttu-id="1255d-162">Numery wersji w nazwach plików</span><span class="sxs-lookup"><span data-stu-id="1255d-162">Version numbers in file names</span></span>

<span data-ttu-id="1255d-163">Pliki pobrane dla platformy .NET przenoszą wersję, na przykład `dotnet-sdk-2.1.300-win10-x64.exe` .</span><span class="sxs-lookup"><span data-stu-id="1255d-163">The files downloaded for .NET carry the version, for example, `dotnet-sdk-2.1.300-win10-x64.exe`.</span></span>

### <a name="preview-versions"></a><span data-ttu-id="1255d-164">Wersje zapoznawcze</span><span class="sxs-lookup"><span data-stu-id="1255d-164">Preview versions</span></span>

<span data-ttu-id="1255d-165">Wersja zapoznawcza ma `-preview[number]-([build]|"final")` dołączony numer wersji.</span><span class="sxs-lookup"><span data-stu-id="1255d-165">Preview versions have a `-preview[number]-([build]|"final")` appended to the version number.</span></span> <span data-ttu-id="1255d-166">Na przykład `2.0.0-preview1-final`.</span><span class="sxs-lookup"><span data-stu-id="1255d-166">For example, `2.0.0-preview1-final`.</span></span>

### <a name="servicing-versions"></a><span data-ttu-id="1255d-167">Wersje obsługi</span><span class="sxs-lookup"><span data-stu-id="1255d-167">Servicing versions</span></span>

<span data-ttu-id="1255d-168">Po wyjściu z wersji, gałęzie wydań zwykle zatrzymują codzienne kompilacje i zamiast tego uruchamiają kompilacje obsługi.</span><span class="sxs-lookup"><span data-stu-id="1255d-168">After a release goes out, the release branches generally stop producing daily builds and instead start producing servicing builds.</span></span> <span data-ttu-id="1255d-169">Wersje obsługujące zostały `-servicing-[number]` dołączone do wersji.</span><span class="sxs-lookup"><span data-stu-id="1255d-169">Servicing versions have a `-servicing-[number]` appended to the version.</span></span> <span data-ttu-id="1255d-170">Na przykład `2.0.1-servicing-006924`.</span><span class="sxs-lookup"><span data-stu-id="1255d-170">For example, `2.0.1-servicing-006924`.</span></span>

## <a name="relationship-to-net-standard-versions"></a><span data-ttu-id="1255d-171">Relacja z wersjami .NET Standard</span><span class="sxs-lookup"><span data-stu-id="1255d-171">Relationship to .NET Standard versions</span></span>

<span data-ttu-id="1255d-172">.NET Standard składa się z zestawu odwołań platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="1255d-172">.NET Standard consists of a .NET reference assembly.</span></span> <span data-ttu-id="1255d-173">Istnieje wiele implementacji specyficznych dla każdej platformy.</span><span class="sxs-lookup"><span data-stu-id="1255d-173">There are multiple implementations specific to each platform.</span></span> <span data-ttu-id="1255d-174">Zestaw odwołań zawiera definicję interfejsów API platformy .NET, które są częścią danej .NET Standard wersji.</span><span class="sxs-lookup"><span data-stu-id="1255d-174">The reference assembly contains the definition of .NET APIs which are part of a given .NET Standard version.</span></span> <span data-ttu-id="1255d-175">Każda implementacja spełnia umowę .NET Standard na określonej platformie.</span><span class="sxs-lookup"><span data-stu-id="1255d-175">Each implementation fulfills the .NET Standard contract on the specific platform.</span></span>

<span data-ttu-id="1255d-176">Zestaw odwołań .NET Standard używa `MAJOR.MINOR` schematu przechowywania wersji.</span><span class="sxs-lookup"><span data-stu-id="1255d-176">The .NET Standard reference assembly uses a `MAJOR.MINOR` versioning scheme.</span></span> <span data-ttu-id="1255d-177">`PATCH` poziom nie jest użyteczny w przypadku .NET Standard, ponieważ uwidacznia tylko specyfikację interfejsu API (bez implementacji) i według definicji jakakolwiek zmiana w interfejsie API będzie reprezentować zmianę zestawu funkcji i w związku z tym nową `MINOR` wersją.</span><span class="sxs-lookup"><span data-stu-id="1255d-177">`PATCH` level isn't useful for .NET Standard because it exposes only an API specification (no implementation) and by definition any change to the API would represent a change in the feature set, and thus a new `MINOR` version.</span></span>

<span data-ttu-id="1255d-178">Implementacje na każdej platformie mogą być aktualizowane, zazwyczaj jako część wersji platformy, i nie są widoczne dla programistów używających .NET Standard na tej platformie.</span><span class="sxs-lookup"><span data-stu-id="1255d-178">The implementations on each platform may be updated, typically as part of the platform release, and thus not evident to the programmers using .NET Standard on that platform.</span></span>

<span data-ttu-id="1255d-179">Aby uzyskać więcej informacji, zobacz [.NET Standard](../../standard/net-standard.md).</span><span class="sxs-lookup"><span data-stu-id="1255d-179">For more information, see [.NET Standard](../../standard/net-standard.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="1255d-180">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="1255d-180">See also</span></span>

- [<span data-ttu-id="1255d-181">Platformy docelowe</span><span class="sxs-lookup"><span data-stu-id="1255d-181">Target frameworks</span></span>](../../standard/frameworks.md)
- [<span data-ttu-id="1255d-182">Pakowanie dystrybucji .NET</span><span class="sxs-lookup"><span data-stu-id="1255d-182">.NET distribution packaging</span></span>](../distribution-packaging.md)
- [<span data-ttu-id="1255d-183">Arkusz faktów pomocy technicznej dla platformy .NET</span><span class="sxs-lookup"><span data-stu-id="1255d-183">.NET Support Lifecycle Fact Sheet</span></span>](https://dotnet.microsoft.com/platform/support/policy)
- [<span data-ttu-id="1255d-184">Obrazy Docker dla platformy .NET</span><span class="sxs-lookup"><span data-stu-id="1255d-184">Docker images for .NET</span></span>](https://hub.docker.com/_/microsoft-dotnet/)
