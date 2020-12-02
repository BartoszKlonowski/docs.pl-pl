---
ms.openlocfilehash: b1910bf0338bccd77ad9e983990d4d193698ec1f
ms.sourcegitcommit: 721c3e4bdbb1ea0bb420818ec944c538fe5c513a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/01/2020
ms.locfileid: "96476609"
---
### <a name="workflow-xoml-file-checksums-changed-from-md5-to-sha256"></a><span data-ttu-id="ee964-101">Sumy kontrolne pliku XOML przepływu pracy zmieniono z MD5 na SHA256</span><span class="sxs-lookup"><span data-stu-id="ee964-101">Workflow XOML file checksums changed from MD5 to SHA256</span></span>

#### <a name="details"></a><span data-ttu-id="ee964-102">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="ee964-102">Details</span></span>

<span data-ttu-id="ee964-103">W celu obsługi debugowania przepływów pracy opartych na plikach xoml przy użyciu programu Visual Studio, gdy projekty przepływu pracy zawierające pliki XOML są kompilowane, suma kontrolna zawartości pliku XOML jest uwzględniana w kodzie wygenerowanym jako <xref:System.Workflow.ComponentModel.Compiler.WorkflowMarkupSourceAttribute.MD5Digest?displayProperty=nameWithType> wartość.</span><span class="sxs-lookup"><span data-stu-id="ee964-103">To support debugging XOML-based workflows with Visual Studio, when workflow projects containing XOML files build, a checksum of the contents of the XOML file is included in the code generated as a <xref:System.Workflow.ComponentModel.Compiler.WorkflowMarkupSourceAttribute.MD5Digest?displayProperty=nameWithType> value.</span></span> <span data-ttu-id="ee964-104">W .NET Framework 4.7.2 i starszych wersjach tego skrótu sumy kontrolnej używał algorytmu MD5, który spowodował problemy w systemach z obsługą FIPS.</span><span class="sxs-lookup"><span data-stu-id="ee964-104">In the .NET Framework 4.7.2 and earlier versions, this checksum hashing used the MD5 algorithm, which caused issues on FIPS-enabled systems.</span></span> <span data-ttu-id="ee964-105">Począwszy od .NET Framework 4,8, używany algorytm to SHA256.</span><span class="sxs-lookup"><span data-stu-id="ee964-105">Starting with the .NET Framework 4.8, the algorithm used is SHA256.</span></span> <span data-ttu-id="ee964-106">Aby była zgodna z WorkflowMarkupSourceAttribute. MD5Digest, używane są tylko pierwsze 16 bajtów wygenerowanej sumy kontrolnej. Może to spowodować problemy podczas debugowania.</span><span class="sxs-lookup"><span data-stu-id="ee964-106">To be compatible with the WorkflowMarkupSourceAttribute.MD5Digest, only the first 16 bytes of the generated checksum are used.This may cause problems during debugging.</span></span> <span data-ttu-id="ee964-107">Może być konieczne ponowne skompilowanie projektu.</span><span class="sxs-lookup"><span data-stu-id="ee964-107">You may need to re-build your project.</span></span>

#### <a name="suggestion"></a><span data-ttu-id="ee964-108">Sugestia</span><span class="sxs-lookup"><span data-stu-id="ee964-108">Suggestion</span></span>

<span data-ttu-id="ee964-109">Jeśli ponowne skompilowanie projektu nie rozwiąże problemu, spróbuj ustawić `AppContext` przełącznik &quot;Switch.System. Workflow. ComponentModel. UseLegacyHashForXomlFileChecksum &quot; na true. W kodzie:</span><span class="sxs-lookup"><span data-stu-id="ee964-109">If re-building your project does not solve the problem, try setting the `AppContext` switch &quot;Switch.System.Workflow.ComponentModel.UseLegacyHashForXomlFileChecksum&quot; to true.In code:</span></span>

<pre><code class="lang-csharp">System.AppContext.SetSwitch(&quot;Switch.System.Workflow.ComponentModel.UseLegacyHashForXomlFileChecksum&quot;, true);&#13;&#10;</code></pre>

<span data-ttu-id="ee964-110">Lub w pliku konfiguracyjnym (musi być w MSBuild.exe.config dla MSBuild.exe, którego używasz):</span><span class="sxs-lookup"><span data-stu-id="ee964-110">Or in a configuration file (this needs to be in MSBuild.exe.config for the MSBuild.exe that you are using):</span></span>

<pre><code class="lang-xml">&lt;configuration&gt;&#13;&#10;&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.System.Workflow.ComponentModel.UseLegacyHashForXomlFileChecksum=true&quot; /&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;&lt;/configuration&gt;&#13;&#10;</code></pre>

| <span data-ttu-id="ee964-111">Nazwa</span><span class="sxs-lookup"><span data-stu-id="ee964-111">Name</span></span>    | <span data-ttu-id="ee964-112">Wartość</span><span class="sxs-lookup"><span data-stu-id="ee964-112">Value</span></span>       |
|:--------|:------------|
| <span data-ttu-id="ee964-113">Zakres</span><span class="sxs-lookup"><span data-stu-id="ee964-113">Scope</span></span>   | <span data-ttu-id="ee964-114">Mały</span><span class="sxs-lookup"><span data-stu-id="ee964-114">Minor</span></span>       |
| <span data-ttu-id="ee964-115">Wersja</span><span class="sxs-lookup"><span data-stu-id="ee964-115">Version</span></span> | <span data-ttu-id="ee964-116">4.8</span><span class="sxs-lookup"><span data-stu-id="ee964-116">4.8</span></span>         |
| <span data-ttu-id="ee964-117">Typ</span><span class="sxs-lookup"><span data-stu-id="ee964-117">Type</span></span>    | <span data-ttu-id="ee964-118">Przekierowanie</span><span class="sxs-lookup"><span data-stu-id="ee964-118">Retargeting</span></span> |
