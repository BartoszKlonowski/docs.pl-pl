---
ms.openlocfilehash: ceae6b85c14862b1b1183d01def0dda723ee0c2b
ms.sourcegitcommit: cbacb5d2cebbf044547f6af6e74a9de866800985
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/05/2020
ms.locfileid: "89496511"
---
### <a name="ef-no-longer-throws-for-queryviews-with-specific-characteristics"></a><span data-ttu-id="4e290-101">EF nie zgłasza już) obiektów QueryView o określonych cechach</span><span class="sxs-lookup"><span data-stu-id="4e290-101">EF no longer throws for QueryViews with specific characteristics</span></span>

#### <a name="details"></a><span data-ttu-id="4e290-102">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="4e290-102">Details</span></span>

<span data-ttu-id="4e290-103">Entity Framework już nie zgłasza <xref:System.StackOverflowException?displayProperty=fullName> wyjątku, gdy aplikacja wykonuje zapytanie, które obejmuje QueryView z właściwością nawigacji 0.. 1, która próbuje dołączyć powiązane jednostki jako część zapytania.</span><span class="sxs-lookup"><span data-stu-id="4e290-103">Entity Framework no longer throws a <xref:System.StackOverflowException?displayProperty=fullName> exception when an app executes a query that involves a QueryView with a 0..1 navigation property that attempts to include the related entities as part of the query.</span></span> <span data-ttu-id="4e290-104">Na przykład przez wywołanie metody <code>.Include(e =&gt; e.RelatedNavProp)</code> .</span><span class="sxs-lookup"><span data-stu-id="4e290-104">For example, by calling <code>.Include(e =&gt; e.RelatedNavProp)</code>.</span></span>

#### <a name="suggestion"></a><span data-ttu-id="4e290-105">Sugestia</span><span class="sxs-lookup"><span data-stu-id="4e290-105">Suggestion</span></span>

<span data-ttu-id="4e290-106">Ta zmiana ma wpływ tylko na kod, który używa) obiektów QueryView z 1-0.. 1 relacji podczas wykonywania zapytań wywoływanych przez program. Być.</span><span class="sxs-lookup"><span data-stu-id="4e290-106">This change only affects code that uses QueryViews with 1-0..1 relationships when running queries that call .Include.</span></span> <span data-ttu-id="4e290-107">Zwiększa niezawodność i powinien być przejrzysty dla niemal wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4e290-107">It improves reliability and should be transparent to almost all apps.</span></span> <span data-ttu-id="4e290-108">Jeśli jednak spowoduje to nieoczekiwane zachowanie, można je wyłączyć, dodając następujący wpis do <code>&lt;appSettings&gt;</code> sekcji w pliku konfiguracji aplikacji:</span><span class="sxs-lookup"><span data-stu-id="4e290-108">However, if it causes unexpected behavior, you can disable it by adding the following entry to the <code>&lt;appSettings&gt;</code> section of the app's configuration file:</span></span><pre><code class="lang-xml">&lt;add key=&quot;EntityFramework_SimplifyUserSpecifiedViews&quot; value=&quot;false&quot; /&gt;&#13;&#10;</code></pre>

| <span data-ttu-id="4e290-109">Nazwa</span><span class="sxs-lookup"><span data-stu-id="4e290-109">Name</span></span>    | <span data-ttu-id="4e290-110">Wartość</span><span class="sxs-lookup"><span data-stu-id="4e290-110">Value</span></span>       |
|:--------|:------------|
| <span data-ttu-id="4e290-111">Zakres</span><span class="sxs-lookup"><span data-stu-id="4e290-111">Scope</span></span>   |<span data-ttu-id="4e290-112">Edge</span><span class="sxs-lookup"><span data-stu-id="4e290-112">Edge</span></span>|
|<span data-ttu-id="4e290-113">Wersja</span><span class="sxs-lookup"><span data-stu-id="4e290-113">Version</span></span>|<span data-ttu-id="4e290-114">4.5.2</span><span class="sxs-lookup"><span data-stu-id="4e290-114">4.5.2</span></span>|
|<span data-ttu-id="4e290-115">Typ</span><span class="sxs-lookup"><span data-stu-id="4e290-115">Type</span></span>|<span data-ttu-id="4e290-116">Środowisko uruchomieniowe</span><span class="sxs-lookup"><span data-stu-id="4e290-116">Runtime</span></span>|

#### <a name="affected-apis"></a><span data-ttu-id="4e290-117">Dotyczy interfejsów API</span><span class="sxs-lookup"><span data-stu-id="4e290-117">Affected APIs</span></span>

<span data-ttu-id="4e290-118">Nie wykrywalne za pośrednictwem analizy interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="4e290-118">Not detectable via API analysis.</span></span>

<!--

#### Affected APIs

Not detectable via API analysis.

-->
