---
ms.openlocfilehash: 58dbb54d42d89b450134758072e3133ae4e6b13d
ms.sourcegitcommit: cbacb5d2cebbf044547f6af6e74a9de866800985
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/05/2020
ms.locfileid: "89497515"
---
### <a name="systemthreadingtaskstask-no-longer-throw-objectdisposedexception-after-object-is-disposed"></a><span data-ttu-id="1391c-101">System. Threading. Tasks. Task nie zgłasza już ObjectDisposedException po usunięciu obiektu</span><span class="sxs-lookup"><span data-stu-id="1391c-101">System.Threading.Tasks.Task no longer throw ObjectDisposedException after object is disposed</span></span>

#### <a name="details"></a><span data-ttu-id="1391c-102">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="1391c-102">Details</span></span>

<span data-ttu-id="1391c-103">Z wyjątkiem <xref:System.Threading.Tasks.Task.System%23IAsyncResult%23AsyncWaitHandle> , <xref:System.Threading.Tasks.Task?displayProperty=fullName> metody nie zgłaszają <xref:System.ObjectDisposedException?displayProperty=fullName> wyjątku po usunięciu obiektu. Ta zmiana obsługuje używanie buforowanych zadań.</span><span class="sxs-lookup"><span data-stu-id="1391c-103">Except for <xref:System.Threading.Tasks.Task.System%23IAsyncResult%23AsyncWaitHandle>, <xref:System.Threading.Tasks.Task?displayProperty=fullName> methods no longer throw an <xref:System.ObjectDisposedException?displayProperty=fullName> exception after the object is disposed.This change supports the use of cached tasks.</span></span> <span data-ttu-id="1391c-104">Na przykład metoda może zwracać buforowane zadanie w celu reprezentowania już zakończonej operacji, zamiast przydzielać nowe zadanie.</span><span class="sxs-lookup"><span data-stu-id="1391c-104">For example, a method can return a cached task to represent an already completed operation instead of allocating a new task.</span></span> <span data-ttu-id="1391c-105">Było to niemożliwe w poprzednich wersjach programu .NET Framework, ponieważ każdy konsument zadania mógł je usunąć, co czyniło je bezużytecznym.</span><span class="sxs-lookup"><span data-stu-id="1391c-105">This was impossible in previous .NET Framework versions, because any consumer of the task could dispose of it, which rendered it unusable.</span></span>

#### <a name="suggestion"></a><span data-ttu-id="1391c-106">Sugestia</span><span class="sxs-lookup"><span data-stu-id="1391c-106">Suggestion</span></span>

<span data-ttu-id="1391c-107">Należy pamiętać, że metody zadań nie mogą już zgłaszać <xref:System.ObjectDisposedException?displayProperty=fullName> w przypadkach, gdy obiekt zostanie usunięty.</span><span class="sxs-lookup"><span data-stu-id="1391c-107">Be aware that Task methods may no longer throw <xref:System.ObjectDisposedException?displayProperty=fullName> in cases when the object is disposed.</span></span> <span data-ttu-id="1391c-108">Jeśli aplikacja była zależna od tego wyjątku, aby wiedzieć, że zadanie zostało zlikwidowane, należy je zaktualizować, aby jawnie sprawdzić stan zadania przy użyciu <xref:System.Threading.Tasks.Task.Status> .</span><span class="sxs-lookup"><span data-stu-id="1391c-108">If an app was depending on this exception to know that a task was disposed, it should be updated to explicitly check the task's status using <xref:System.Threading.Tasks.Task.Status>.</span></span>

| <span data-ttu-id="1391c-109">Nazwa</span><span class="sxs-lookup"><span data-stu-id="1391c-109">Name</span></span>    | <span data-ttu-id="1391c-110">Wartość</span><span class="sxs-lookup"><span data-stu-id="1391c-110">Value</span></span>       |
|:--------|:------------|
| <span data-ttu-id="1391c-111">Zakres</span><span class="sxs-lookup"><span data-stu-id="1391c-111">Scope</span></span>   |<span data-ttu-id="1391c-112">Mały</span><span class="sxs-lookup"><span data-stu-id="1391c-112">Minor</span></span>|
|<span data-ttu-id="1391c-113">Wersja</span><span class="sxs-lookup"><span data-stu-id="1391c-113">Version</span></span>|<span data-ttu-id="1391c-114">4.5</span><span class="sxs-lookup"><span data-stu-id="1391c-114">4.5</span></span>|
|<span data-ttu-id="1391c-115">Typ</span><span class="sxs-lookup"><span data-stu-id="1391c-115">Type</span></span>|<span data-ttu-id="1391c-116">Środowisko uruchomieniowe</span><span class="sxs-lookup"><span data-stu-id="1391c-116">Runtime</span></span>|

#### <a name="affected-apis"></a><span data-ttu-id="1391c-117">Dotyczy interfejsów API</span><span class="sxs-lookup"><span data-stu-id="1391c-117">Affected APIs</span></span>

<span data-ttu-id="1391c-118">Nie wykrywalne za pośrednictwem analizy interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="1391c-118">Not detectable via API analysis.</span></span>

<!--

#### Affected APIs

Not detectable via API analysis.

-->
