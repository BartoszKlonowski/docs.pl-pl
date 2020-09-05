---
ms.openlocfilehash: 65fa5d8629ce8e426cf1623590a056e5cad0b91f
ms.sourcegitcommit: cbacb5d2cebbf044547f6af6e74a9de866800985
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/05/2020
ms.locfileid: "89497325"
---
### <a name="net-interop-will-now-queryinterface-for-iagileobject-a-winrt-interface"></a><span data-ttu-id="bbac6-101">Platforma .NET Interop będzie teraz w języku QueryInterface dla IAgileObject (interfejs WinRT)</span><span class="sxs-lookup"><span data-stu-id="bbac6-101">.NET Interop will now QueryInterface for IAgileObject (a WinRT interface)</span></span>

#### <a name="details"></a><span data-ttu-id="bbac6-102">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="bbac6-102">Details</span></span>

<span data-ttu-id="bbac6-103">W przypadku użycia zdarzenia WinRT z delegatem platformy .NET system Windows będzie QI do IAgileObject, począwszy od .NET Framework 4,8.</span><span class="sxs-lookup"><span data-stu-id="bbac6-103">When using a WinRT event with a .NET delegate, Windows will QI for IAgileObject starting with the .NET Framework 4.8.</span></span>  <span data-ttu-id="bbac6-104">W poprzednich wersjach .NET Framework środowisko uruchomieniowe zakończy się niepowodzeniem i nie będzie mogło subskrybować tego zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="bbac6-104">In previous versions of the .NET Framework, the runtime would fail that QI, and the event could not be subscribed.</span></span><ul><li><span data-ttu-id="bbac6-105">[x] Quirked</span><span class="sxs-lookup"><span data-stu-id="bbac6-105">[ x ] Quirked</span></span></li></ul>

#### <a name="suggestion"></a><span data-ttu-id="bbac6-106">Sugestia</span><span class="sxs-lookup"><span data-stu-id="bbac6-106">Suggestion</span></span>

<span data-ttu-id="bbac6-107">W przypadku włączenia QI na potrzeby wykonywania przerwań IAgileObject można wyłączyć ten kod, ustawiając poniższą konfigurację.</span><span class="sxs-lookup"><span data-stu-id="bbac6-107">If enabling the QI for IAgileObject breaks execution, you can disable this code by setting the following configuration.</span></span> <h4><span data-ttu-id="bbac6-108">Metoda 1: zmienna środowiskowa</span><span class="sxs-lookup"><span data-stu-id="bbac6-108">Method 1: Environment variable</span></span></h4> <span data-ttu-id="bbac6-109">Ustaw następujące zmienne środowiskowe: Metoda COMPLUS_DisableCCWSupportIAgileObject = 1This ma wpływ na dowolne środowisko, które dziedziczy tę zmienną środowiskową.</span><span class="sxs-lookup"><span data-stu-id="bbac6-109">Set the following environment variable:COMPLUS_DisableCCWSupportIAgileObject=1This method affects any environment that inherits this environment variable.</span></span> <span data-ttu-id="bbac6-110">Może to być tylko jedna sesja konsoli lub może mieć wpływ na całą maszynę, jeśli zmienna środowiskowa jest ustawiona globalnie.</span><span class="sxs-lookup"><span data-stu-id="bbac6-110">This might be just a single console session, or it might affect the entire machine if you set the environment variable globally.</span></span> <span data-ttu-id="bbac6-111">W nazwie zmiennej środowiskowej nie jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="bbac6-111">The environment variable name is not case-sensitive.</span></span> <h4><span data-ttu-id="bbac6-112">Metoda 2. Rejestr</span><span class="sxs-lookup"><span data-stu-id="bbac6-112">Method 2: Registry</span></span></h4> <span data-ttu-id="bbac6-113">Korzystając z edytora rejestru (regedit.exe), Znajdź jeden z następujących podkluczy: HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft.NETFramework HKEY_CURRENT_USER \SOFTWARE\Microsoft.NETFrameworkThen Dodaj następujące: value Name: DisableCCWSupportIAgileObject Type: DWORD (32-bit) Value (zwane również REG_WORD) Value: 1You może użyć narzędzia REG.EXE systemu Windows, aby dodać tę wartość z poziomu wiersza polecenia lub skryptów.</span><span class="sxs-lookup"><span data-stu-id="bbac6-113">Using Registry Editor (regedit.exe), find either of the following subkeys:HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft.NETFramework HKEY_CURRENT_USER\SOFTWARE\Microsoft.NETFrameworkThen add the following:Value name: DisableCCWSupportIAgileObject Type: DWORD (32-bit) Value (also called REG_WORD) Value: 1You can use the Windows REG.EXE tool to add this value from a command-line or scripting environment.</span></span> <span data-ttu-id="bbac6-114">Przykład:</span><span class="sxs-lookup"><span data-stu-id="bbac6-114">For example:</span></span><pre><code class="lang-console">reg add HKLM\SOFTWARE\Microsoft\.NETFramework /v DisableCCWSupportIAgileObject /t REG_DWORD /d 1&#13;&#10;</code></pre><span data-ttu-id="bbac6-115">W tym przypadku <code>HKLM</code> jest używany zamiast <code>HKEY_LOCAL_MACHINE</code> .</span><span class="sxs-lookup"><span data-stu-id="bbac6-115">In this case, <code>HKLM</code> is used instead of <code>HKEY_LOCAL_MACHINE</code>.</span></span> <span data-ttu-id="bbac6-116">Użyj <code>reg add /?</code> , aby wyświetlić pomoc dotyczącą tej składni.</span><span class="sxs-lookup"><span data-stu-id="bbac6-116">Use <code>reg add /?</code> to see help on this syntax.</span></span> <span data-ttu-id="bbac6-117">W nazwie wartości rejestru nie jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="bbac6-117">The registry value name is not case-sensitive.</span></span>

| <span data-ttu-id="bbac6-118">Nazwa</span><span class="sxs-lookup"><span data-stu-id="bbac6-118">Name</span></span>    | <span data-ttu-id="bbac6-119">Wartość</span><span class="sxs-lookup"><span data-stu-id="bbac6-119">Value</span></span>       |
|:--------|:------------|
| <span data-ttu-id="bbac6-120">Zakres</span><span class="sxs-lookup"><span data-stu-id="bbac6-120">Scope</span></span>   |<span data-ttu-id="bbac6-121">Edge</span><span class="sxs-lookup"><span data-stu-id="bbac6-121">Edge</span></span>|
|<span data-ttu-id="bbac6-122">Wersja</span><span class="sxs-lookup"><span data-stu-id="bbac6-122">Version</span></span>|<span data-ttu-id="bbac6-123">4,8</span><span class="sxs-lookup"><span data-stu-id="bbac6-123">4.8</span></span>|
|<span data-ttu-id="bbac6-124">Typ</span><span class="sxs-lookup"><span data-stu-id="bbac6-124">Type</span></span>|<span data-ttu-id="bbac6-125">Środowisko uruchomieniowe</span><span class="sxs-lookup"><span data-stu-id="bbac6-125">Runtime</span></span>|

#### <a name="affected-apis"></a><span data-ttu-id="bbac6-126">Dotyczy interfejsów API</span><span class="sxs-lookup"><span data-stu-id="bbac6-126">Affected APIs</span></span>

<span data-ttu-id="bbac6-127">Nie wykrywalne za pośrednictwem analizy interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="bbac6-127">Not detectable via API analysis.</span></span>

<!--

#### Affected APIs

Not detectable via API analysis.

-->
