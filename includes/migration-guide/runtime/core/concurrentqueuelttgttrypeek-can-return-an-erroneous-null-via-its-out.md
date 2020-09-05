---
ms.openlocfilehash: 004e2d1883b631e88ab5e164b1120c3b081b7041
ms.sourcegitcommit: cbacb5d2cebbf044547f6af6e74a9de866800985
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/05/2020
ms.locfileid: "89497481"
---
### <a name="concurrentqueuelttgttrypeek-can-return-an-erroneous-null-via-its-out-parameter"></a><span data-ttu-id="5f9f7-101">ConcurrentQueue &lt; T &gt; . TryPeek może zwrócić błędną wartość null za pośrednictwem jego parametru out</span><span class="sxs-lookup"><span data-stu-id="5f9f7-101">ConcurrentQueue&lt;T&gt;.TryPeek can return an erroneous null via its out parameter</span></span>

#### <a name="details"></a><span data-ttu-id="5f9f7-102">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="5f9f7-102">Details</span></span>

<span data-ttu-id="5f9f7-103">W niektórych scenariuszach wielowątkowych <xref:System.Collections.Concurrent.ConcurrentQueue%601.TryPeek(%600@)?displayProperty=fullName> można zwrócić wartość true, ale wypełnić parametr out wartością null (zamiast poprawnej wartości z możliwością wglądu).</span><span class="sxs-lookup"><span data-stu-id="5f9f7-103">In some multi-threaded scenarios, <xref:System.Collections.Concurrent.ConcurrentQueue%601.TryPeek(%600@)?displayProperty=fullName> can return true, but populate the out parameter with a null value (instead of the correct, peeked value).</span></span>

#### <a name="suggestion"></a><span data-ttu-id="5f9f7-104">Sugestia</span><span class="sxs-lookup"><span data-stu-id="5f9f7-104">Suggestion</span></span>

<span data-ttu-id="5f9f7-105">Ten problem został rozwiązany w .NET Framework 4.5.1.</span><span class="sxs-lookup"><span data-stu-id="5f9f7-105">This issue is fixed in the .NET Framework 4.5.1.</span></span> <span data-ttu-id="5f9f7-106">Uaktualnienie do tego środowiska spowoduje rozwiązanie tego problemu.</span><span class="sxs-lookup"><span data-stu-id="5f9f7-106">Upgrading to that Framework will solve the issue.</span></span>

| <span data-ttu-id="5f9f7-107">Nazwa</span><span class="sxs-lookup"><span data-stu-id="5f9f7-107">Name</span></span>    | <span data-ttu-id="5f9f7-108">Wartość</span><span class="sxs-lookup"><span data-stu-id="5f9f7-108">Value</span></span>       |
|:--------|:------------|
| <span data-ttu-id="5f9f7-109">Zakres</span><span class="sxs-lookup"><span data-stu-id="5f9f7-109">Scope</span></span>   |<span data-ttu-id="5f9f7-110">Duży</span><span class="sxs-lookup"><span data-stu-id="5f9f7-110">Major</span></span>|
|<span data-ttu-id="5f9f7-111">Wersja</span><span class="sxs-lookup"><span data-stu-id="5f9f7-111">Version</span></span>|<span data-ttu-id="5f9f7-112">4.5</span><span class="sxs-lookup"><span data-stu-id="5f9f7-112">4.5</span></span>|
|<span data-ttu-id="5f9f7-113">Typ</span><span class="sxs-lookup"><span data-stu-id="5f9f7-113">Type</span></span>|<span data-ttu-id="5f9f7-114">Środowisko uruchomieniowe</span><span class="sxs-lookup"><span data-stu-id="5f9f7-114">Runtime</span></span>|

#### <a name="affected-apis"></a><span data-ttu-id="5f9f7-115">Dotyczy interfejsów API</span><span class="sxs-lookup"><span data-stu-id="5f9f7-115">Affected APIs</span></span>

- <xref:System.Collections.Concurrent.ConcurrentQueue%601.TryPeek(%600@)?displayProperty=nameWithType>

<!--

#### Affected APIs

- ``M:System.Collections.Concurrent.ConcurrentQueue`1.TryPeek(`0@)``

-->
