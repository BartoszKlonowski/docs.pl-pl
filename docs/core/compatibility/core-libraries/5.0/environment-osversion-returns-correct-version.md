---
title: 'Istotna zmiana: Environment. OSVersion zwraca poprawną wersję systemu operacyjnego'
description: Dowiedz się więcej na temat istotnej zmiany w programie .NET 5,0 w bibliotekach podstawowych platformy .NET, gdzie Environment. OSVersion zwraca rzeczywistą wersję systemu operacyjnego, a na przykład system operacyjny wybrany do zapewnienia zgodności aplikacji.
ms.date: 11/01/2020
ms.openlocfilehash: c810d9a7a028a0c60c30d69e78a9b9c695d933ef
ms.sourcegitcommit: 81f1bba2c97a67b5ca76bcc57b37333ffca60c7b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/10/2020
ms.locfileid: "97009524"
---
# <a name="environmentosversion-returns-the-correct-operating-system-version"></a><span data-ttu-id="3542c-103">Środowisko. OSVersion zwraca poprawną wersję systemu operacyjnego</span><span class="sxs-lookup"><span data-stu-id="3542c-103">Environment.OSVersion returns the correct operating system version</span></span>

<span data-ttu-id="3542c-104"><xref:System.Environment.OSVersion?displayProperty=nameWithType> zwraca rzeczywistą wersję systemu operacyjnego (OS) zamiast programu, na przykład systemu operacyjnego wybranego na potrzeby zgodności aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3542c-104"><xref:System.Environment.OSVersion?displayProperty=nameWithType> returns the actual version of the operating system (OS) instead of, for example, the OS that's selected for application compatibility.</span></span>

## <a name="change-description"></a><span data-ttu-id="3542c-105">Zmień opis</span><span class="sxs-lookup"><span data-stu-id="3542c-105">Change description</span></span>

<span data-ttu-id="3542c-106">W poprzednich wersjach programu .NET <xref:System.Environment.OSVersion?displayProperty=nameWithType> Funkcja zwraca wersję systemu operacyjnego, która może być niepoprawna, gdy aplikacja działa w trybie zgodności systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="3542c-106">In previous .NET versions, <xref:System.Environment.OSVersion?displayProperty=nameWithType> returns an OS version that may be incorrect when an application runs under Windows compatibility mode.</span></span> <span data-ttu-id="3542c-107">Aby uzyskać więcej informacji, zobacz [uwagi dotyczące funkcji GetVersionExA](/windows/win32/api/sysinfoapi/nf-sysinfoapi-getversionexa#remarks).</span><span class="sxs-lookup"><span data-stu-id="3542c-107">For more information, see [GetVersionExA function remarks](/windows/win32/api/sysinfoapi/nf-sysinfoapi-getversionexa#remarks).</span></span> <span data-ttu-id="3542c-108">W systemie macOS <xref:System.Environment.OSVersion?displayProperty=nameWithType> zwraca podstawową wersję jądra programu Darwin.</span><span class="sxs-lookup"><span data-stu-id="3542c-108">On macOS, <xref:System.Environment.OSVersion?displayProperty=nameWithType> returns the underlying Darwin kernel version.</span></span>

<span data-ttu-id="3542c-109">Począwszy od platformy .NET 5,0, <xref:System.Environment.OSVersion?displayProperty=nameWithType> zwraca rzeczywistą wersję systemu operacyjnego dla systemu Windows i macOS.</span><span class="sxs-lookup"><span data-stu-id="3542c-109">Starting in .NET 5.0, <xref:System.Environment.OSVersion?displayProperty=nameWithType> returns the actual version of the operating system for Windows and macOS.</span></span>

<span data-ttu-id="3542c-110">W poniższej tabeli przedstawiono różnice w zachowaniu.</span><span class="sxs-lookup"><span data-stu-id="3542c-110">The following table shows the difference in behavior.</span></span>

|  | <span data-ttu-id="3542c-111">Poprzednie wersje .NET</span><span class="sxs-lookup"><span data-stu-id="3542c-111">Previous .NET versions</span></span> | <span data-ttu-id="3542c-112">.NET 5 +</span><span class="sxs-lookup"><span data-stu-id="3542c-112">.NET 5+</span></span> |
|--|------------------------|---------|
| <span data-ttu-id="3542c-113">Windows</span><span class="sxs-lookup"><span data-stu-id="3542c-113">Windows</span></span> | <span data-ttu-id="3542c-114">6.2.9200.0</span><span class="sxs-lookup"><span data-stu-id="3542c-114">6.2.9200.0</span></span> | <span data-ttu-id="3542c-115">10.0.19042.0</span><span class="sxs-lookup"><span data-stu-id="3542c-115">10.0.19042.0</span></span> |
| <span data-ttu-id="3542c-116">macOS</span><span class="sxs-lookup"><span data-stu-id="3542c-116">macOS</span></span> | <span data-ttu-id="3542c-117">19.6.0.0</span><span class="sxs-lookup"><span data-stu-id="3542c-117">19.6.0.0</span></span> | <span data-ttu-id="3542c-118">10.15.7</span><span class="sxs-lookup"><span data-stu-id="3542c-118">10.15.7</span></span> |

## <a name="reason-for-change"></a><span data-ttu-id="3542c-119">Przyczyna zmiany</span><span class="sxs-lookup"><span data-stu-id="3542c-119">Reason for change</span></span>

<span data-ttu-id="3542c-120">Użytkownicy tej właściwości oczekują zwrócenia rzeczywistej wersji systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="3542c-120">Users of this property expect it to return the actual version of the operating system.</span></span> <span data-ttu-id="3542c-121">Większość aplikacji platformy .NET nie określa ich obsługiwanej wersji w manifeście aplikacji i w ten sposób uzyskuje domyślną obsługiwaną wersję z hosta dotnet.</span><span class="sxs-lookup"><span data-stu-id="3542c-121">Most .NET apps don't specify their supported version in their application manifest, and thus get the default supported version from the dotnet host.</span></span> <span data-ttu-id="3542c-122">W związku z tym podkładka dotycząca zgodności ma rzadko znaczenie dla aplikacji, która jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="3542c-122">As a result, the compatibility shim is rarely meaningful for the app that's running.</span></span> <span data-ttu-id="3542c-123">Gdy system Windows zwalnia nową wersję, a starszy Host dotnet jest nadal używany, te aplikacje mogą uzyskać niepoprawną wersję systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="3542c-123">When Windows releases a new version and an older dotnet host is still in use, these apps may get an incorrect OS version.</span></span> <span data-ttu-id="3542c-124">Zwrócenie rzeczywistej wersji jest bardziej wbudowane z oczekiwaniami deweloperów tego interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="3542c-124">Returning the actual version is more inline with developers' expectations of this API.</span></span>

<span data-ttu-id="3542c-125">Wprowadzenie <xref:System.OperatingSystem.IsWindowsVersionAtLeast%2A?displayProperty=nameWithType> <xref:System.OperatingSystem.IsMacOSVersionAtLeast%2A?displayProperty=nameWithType> programów,, i <xref:System.Runtime.Versioning.SupportedOSPlatformAttribute?displayProperty=nameWithType> w programie .NET 5,0, <xref:System.Environment.OSVersion?displayProperty=nameWithType> zostało zmienione tak, aby były spójne dla systemu Windows i macOS.</span><span class="sxs-lookup"><span data-stu-id="3542c-125">With the introduction of <xref:System.OperatingSystem.IsWindowsVersionAtLeast%2A?displayProperty=nameWithType>, <xref:System.OperatingSystem.IsMacOSVersionAtLeast%2A?displayProperty=nameWithType>, and <xref:System.Runtime.Versioning.SupportedOSPlatformAttribute?displayProperty=nameWithType> in .NET 5.0, <xref:System.Environment.OSVersion?displayProperty=nameWithType> was changed to be consistent for Windows and macOS.</span></span>

## <a name="version-introduced"></a><span data-ttu-id="3542c-126">Wprowadzona wersja</span><span class="sxs-lookup"><span data-stu-id="3542c-126">Version introduced</span></span>

<span data-ttu-id="3542c-127">5,0</span><span class="sxs-lookup"><span data-stu-id="3542c-127">5.0</span></span>

## <a name="recommended-action"></a><span data-ttu-id="3542c-128">Zalecana akcja</span><span class="sxs-lookup"><span data-stu-id="3542c-128">Recommended action</span></span>

<span data-ttu-id="3542c-129">Przejrzyj i przetestuj każdy kod, który używa, <xref:System.Environment.OSVersion?displayProperty=nameWithType> Aby upewnić się, że działa zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="3542c-129">Review and test any code that uses <xref:System.Environment.OSVersion?displayProperty=nameWithType> to ensure it behaves as desired.</span></span>

## <a name="affected-apis"></a><span data-ttu-id="3542c-130">Dotyczy interfejsów API</span><span class="sxs-lookup"><span data-stu-id="3542c-130">Affected APIs</span></span>

- <xref:System.Environment.OSVersion?displayProperty=fullName>

<!--

### Category

Core .NET libraries

### Affected APIs

- `P:System.Environment.OSVersion`

-->
