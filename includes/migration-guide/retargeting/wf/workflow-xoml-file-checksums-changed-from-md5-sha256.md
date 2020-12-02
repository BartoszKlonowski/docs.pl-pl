---
ms.openlocfilehash: b1910bf0338bccd77ad9e983990d4d193698ec1f
ms.sourcegitcommit: 721c3e4bdbb1ea0bb420818ec944c538fe5c513a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/01/2020
ms.locfileid: "96476609"
---
### <a name="workflow-xoml-file-checksums-changed-from-md5-to-sha256"></a>Sumy kontrolne pliku XOML przepływu pracy zmieniono z MD5 na SHA256

#### <a name="details"></a>Szczegóły

W celu obsługi debugowania przepływów pracy opartych na plikach xoml przy użyciu programu Visual Studio, gdy projekty przepływu pracy zawierające pliki XOML są kompilowane, suma kontrolna zawartości pliku XOML jest uwzględniana w kodzie wygenerowanym jako <xref:System.Workflow.ComponentModel.Compiler.WorkflowMarkupSourceAttribute.MD5Digest?displayProperty=nameWithType> wartość. W .NET Framework 4.7.2 i starszych wersjach tego skrótu sumy kontrolnej używał algorytmu MD5, który spowodował problemy w systemach z obsługą FIPS. Począwszy od .NET Framework 4,8, używany algorytm to SHA256. Aby była zgodna z WorkflowMarkupSourceAttribute. MD5Digest, używane są tylko pierwsze 16 bajtów wygenerowanej sumy kontrolnej. Może to spowodować problemy podczas debugowania. Może być konieczne ponowne skompilowanie projektu.

#### <a name="suggestion"></a>Sugestia

Jeśli ponowne skompilowanie projektu nie rozwiąże problemu, spróbuj ustawić `AppContext` przełącznik &quot;Switch.System. Workflow. ComponentModel. UseLegacyHashForXomlFileChecksum &quot; na true. W kodzie:

<pre><code class="lang-csharp">System.AppContext.SetSwitch(&quot;Switch.System.Workflow.ComponentModel.UseLegacyHashForXomlFileChecksum&quot;, true);&#13;&#10;</code></pre>

Lub w pliku konfiguracyjnym (musi być w MSBuild.exe.config dla MSBuild.exe, którego używasz):

<pre><code class="lang-xml">&lt;configuration&gt;&#13;&#10;&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.System.Workflow.ComponentModel.UseLegacyHashForXomlFileChecksum=true&quot; /&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;&lt;/configuration&gt;&#13;&#10;</code></pre>

| Nazwa    | Wartość       |
|:--------|:------------|
| Zakres   | Mały       |
| Wersja | 4.8         |
| Typ    | Przekierowanie |
