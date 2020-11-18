---
title: Bloki skryptów i element msxsl:script
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: fde6f43f-c594-486f-abcb-2211197fae20
ms.openlocfilehash: 3cb65142243d1f910ffd0fb85750ba62786d79f0
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/18/2020
ms.locfileid: "94824703"
---
# <a name="script-blocks-using-msxslscript"></a><span data-ttu-id="0be83-102">Bloki skryptów i element msxsl:script</span><span class="sxs-lookup"><span data-stu-id="0be83-102">Script Blocks Using msxsl:script</span></span>
<span data-ttu-id="0be83-103"><xref:System.Xml.Xsl.XslCompiledTransform>Klasa obsługuje skrypty osadzone przy użyciu `msxsl:script` elementu.</span><span class="sxs-lookup"><span data-stu-id="0be83-103">The <xref:System.Xml.Xsl.XslCompiledTransform> class supports embedded scripts using the `msxsl:script` element.</span></span> <span data-ttu-id="0be83-104">Po załadowaniu arkusza stylów wszystkie zdefiniowane funkcje są kompilowane do języka pośredniego firmy Microsoft (MSIL) przez Code Document Object Model (CodeDOM) i są wykonywane w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="0be83-104">When the style sheet is loaded, any defined functions are compiled to Microsoft intermediate language (MSIL) by the Code Document Object Model (CodeDOM) and are executed during run time.</span></span> <span data-ttu-id="0be83-105">Zestaw wygenerowany z osadzonego bloku skryptu jest oddzielony od zestawu wygenerowanego dla arkusza stylów.</span><span class="sxs-lookup"><span data-stu-id="0be83-105">The assembly generated from the embedded script block is separate than the assembly generated for the style sheet.</span></span>  
  
## <a name="enable-xslt-script"></a><span data-ttu-id="0be83-106">Włącz skrypt XSLT</span><span class="sxs-lookup"><span data-stu-id="0be83-106">Enable XSLT Script</span></span>  
 <span data-ttu-id="0be83-107">Obsługa skryptów osadzonych jest opcjonalnym ustawieniem XSLT dla <xref:System.Xml.Xsl.XslCompiledTransform> klasy.</span><span class="sxs-lookup"><span data-stu-id="0be83-107">Support for embedded scripts is an optional XSLT setting on the <xref:System.Xml.Xsl.XslCompiledTransform> class.</span></span> <span data-ttu-id="0be83-108">Obsługa skryptów jest domyślnie wyłączona.</span><span class="sxs-lookup"><span data-stu-id="0be83-108">Script support is disabled by default.</span></span> <span data-ttu-id="0be83-109">Aby włączyć obsługę skryptów, należy utworzyć <xref:System.Xml.Xsl.XsltSettings> obiekt z <xref:System.Xml.Xsl.XsltSettings.EnableScript%2A> właściwością ustawioną na `true` i przekazać obiekt do <xref:System.Xml.Xsl.XslCompiledTransform.Load%2A> metody.</span><span class="sxs-lookup"><span data-stu-id="0be83-109">To enable script support, create an <xref:System.Xml.Xsl.XsltSettings> object with the <xref:System.Xml.Xsl.XsltSettings.EnableScript%2A> property set to `true` and pass the object to the <xref:System.Xml.Xsl.XslCompiledTransform.Load%2A> method.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="0be83-110">Obsługa skryptów XSLT powinna być włączona tylko wtedy, gdy wymagana jest obsługa skryptów i Pracujesz w w pełni zaufanym środowisku.</span><span class="sxs-lookup"><span data-stu-id="0be83-110">XSLT scripting should be enabled only if you require script support and you are working in a fully trusted environment.</span></span>  
  
## <a name="msxslscript-element-definition"></a><span data-ttu-id="0be83-111">msxsl: definicja elementu skryptu</span><span class="sxs-lookup"><span data-stu-id="0be83-111">msxsl:script Element Definition</span></span>  
 <span data-ttu-id="0be83-112">`msxsl:script`Element to rozszerzenie Microsoft do zalecenia XSLT 1,0 i ma następującą definicję:</span><span class="sxs-lookup"><span data-stu-id="0be83-112">The `msxsl:script` element is a Microsoft extension to the XSLT 1.0 recommendation and has the following definition:</span></span>  
  
```xml  
<msxsl:script language = "language-name" implements-prefix = "prefix of user namespace"> </msxsl:script>  
```  
  
 <span data-ttu-id="0be83-113">`msxsl`Prefiks jest powiązany z `urn:schemas-microsoft-com:xslt` identyfikatorem URI przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="0be83-113">The `msxsl` prefix is bound to the `urn:schemas-microsoft-com:xslt` namespace URI.</span></span> <span data-ttu-id="0be83-114">Arkusz stylów musi zawierać `xmlns:msxsl=urn:schemas-microsoft-com:xslt` deklarację przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="0be83-114">The style sheet must include the `xmlns:msxsl=urn:schemas-microsoft-com:xslt` namespace declaration.</span></span>  
  
 <span data-ttu-id="0be83-115">`language`Atrybut jest opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="0be83-115">The `language` attribute is optional.</span></span> <span data-ttu-id="0be83-116">Jego wartością jest język kodu osadzonego bloku kodu.</span><span class="sxs-lookup"><span data-stu-id="0be83-116">Its value is the code language of the embedded code block.</span></span> <span data-ttu-id="0be83-117">Język jest mapowany do odpowiedniego kompilatora CodeDOM przy użyciu <xref:System.CodeDom.Compiler.CodeDomProvider.CreateProvider%2A?displayProperty=nameWithType> metody.</span><span class="sxs-lookup"><span data-stu-id="0be83-117">The language is mapped to the appropriate CodeDOM compiler using the <xref:System.CodeDom.Compiler.CodeDomProvider.CreateProvider%2A?displayProperty=nameWithType> method.</span></span> <span data-ttu-id="0be83-118"><xref:System.Xml.Xsl.XslCompiledTransform>Klasa może obsługiwać dowolny język Microsoft .NET, przy założeniu, że odpowiedni Dostawca jest zainstalowany na maszynie i jest zarejestrowany w sekcji System. CodeDom pliku machine.config.</span><span class="sxs-lookup"><span data-stu-id="0be83-118">The <xref:System.Xml.Xsl.XslCompiledTransform> class can support any Microsoft .NET language, assuming the appropriate provider is installed on the machine and is registered in the system.codedom section of the machine.config file.</span></span> <span data-ttu-id="0be83-119">Jeśli `language` atrybut nie jest określony, język domyślny języka JScript.</span><span class="sxs-lookup"><span data-stu-id="0be83-119">If a `language` attribute is not specified, the language defaults to JScript.</span></span> <span data-ttu-id="0be83-120">W nazwie języka nie jest rozróżniana wielkość liter, dlatego "JavaScript" i "JavaScript" są równoważne.</span><span class="sxs-lookup"><span data-stu-id="0be83-120">The language name is not case-sensitive so 'JavaScript' and 'javascript' are equivalent.</span></span>  
  
 <span data-ttu-id="0be83-121">Ten `implements-prefix` atrybut jest obowiązkowy.</span><span class="sxs-lookup"><span data-stu-id="0be83-121">The `implements-prefix` attribute is mandatory.</span></span> <span data-ttu-id="0be83-122">Ten atrybut służy do deklarowania przestrzeni nazw i kojarzenia jej z blokiem skryptu.</span><span class="sxs-lookup"><span data-stu-id="0be83-122">This attribute is used to declare a namespace and associate it with the script block.</span></span> <span data-ttu-id="0be83-123">Wartość tego atrybutu jest prefiks, który reprezentuje obszar nazw.</span><span class="sxs-lookup"><span data-stu-id="0be83-123">The value of this attribute is the prefix that represents the namespace.</span></span> <span data-ttu-id="0be83-124">Ten prefiks można zdefiniować w arkuszu stylów.</span><span class="sxs-lookup"><span data-stu-id="0be83-124">This prefix can be defined somewhere in a style sheet.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="0be83-125">W przypadku korzystania z `msxsl:script` elementu zdecydowanie zalecamy, aby skrypt niezależnie od języka został umieszczony wewnątrz sekcji CDATA.</span><span class="sxs-lookup"><span data-stu-id="0be83-125">When using the `msxsl:script` element, we strongly recommend that the script, regardless of language, be placed inside a CDATA section.</span></span> <span data-ttu-id="0be83-126">Ze względu na to, że skrypt może zawierać operatory, identyfikatory lub ograniczniki dla danego języka, jeśli nie jest zawarty w sekcji CDATA, ma możliwość błędnego interpretowania kodu XML.</span><span class="sxs-lookup"><span data-stu-id="0be83-126">Because the script can contain operators, identifiers, or delimiters for a given language, if it is not contained within a CDATA section, it has the potential of being misinterpreted as XML.</span></span> <span data-ttu-id="0be83-127">W poniższym kodzie XML przedstawiono szablon sekcji CDATA, w której można umieścić kod.</span><span class="sxs-lookup"><span data-stu-id="0be83-127">The following XML shows a template of the CDATA section where code can be placed.</span></span>  
  
```xml  
<msxsl:script implements-prefix='your-prefix' language='CSharp'>  
<![CDATA[  
// Code block.  
]]>  
</msxsl:script>  
```  
  
## <a name="script-functions"></a><span data-ttu-id="0be83-128">Funkcje skryptu</span><span class="sxs-lookup"><span data-stu-id="0be83-128">Script Functions</span></span>  
 <span data-ttu-id="0be83-129">Funkcje mogą być deklarowane w obrębie `msxsl:script` elementu.</span><span class="sxs-lookup"><span data-stu-id="0be83-129">Functions can be declared within the `msxsl:script` element.</span></span> <span data-ttu-id="0be83-130">Gdy funkcja jest zadeklarowana, jest zawarta w bloku skryptu.</span><span class="sxs-lookup"><span data-stu-id="0be83-130">When a function is declared, it is contained in a script block.</span></span> <span data-ttu-id="0be83-131">Arkusze stylów mogą zawierać wiele bloków skryptu, z których każda działa niezależnie od siebie.</span><span class="sxs-lookup"><span data-stu-id="0be83-131">Style sheets can contain multiple script blocks, each operating independent of the other.</span></span> <span data-ttu-id="0be83-132">Oznacza to, że jeśli wykonujesz wewnątrz bloku skryptu, nie można wywołać funkcji, która została zdefiniowana w innym bloku skryptu, chyba że jest zadeklarowana jako ma tę samą przestrzeń nazw i ten sam język skryptowy.</span><span class="sxs-lookup"><span data-stu-id="0be83-132">That means that if you are executing inside a script block, you cannot call a function that you defined in another script block unless it is declared to have the same namespace and the same scripting language.</span></span> <span data-ttu-id="0be83-133">Ponieważ każdy blok skryptu może znajdować się w własnym języku, a blok jest analizowany zgodnie z regułami gramatyki tego analizatora języka, zalecamy użycie odpowiedniej składni dla używanego języka.</span><span class="sxs-lookup"><span data-stu-id="0be83-133">Because each script block can be in its own language, and the block is parsed according to the grammar rules of that language parser we recommend that you use the correct syntax for the language in use.</span></span> <span data-ttu-id="0be83-134">Na przykład jeśli jesteś w bloku skryptu w języku Microsoft C#, użyj składni komentarza języka C#.</span><span class="sxs-lookup"><span data-stu-id="0be83-134">For example, if you are in a Microsoft C# script block, use the C# comment syntax.</span></span>  
  
 <span data-ttu-id="0be83-135">Podane argumenty i zwracane wartości do funkcji mogą być dowolnego typu.</span><span class="sxs-lookup"><span data-stu-id="0be83-135">The supplied arguments and return values to the function can be of any type.</span></span> <span data-ttu-id="0be83-136">Ponieważ typy W3C XPath są podzbiorem typów środowiska uruchomieniowego języka wspólnego (CLR), konwersja typu odbywa się na typach, które nie są uważane za typ XPath.</span><span class="sxs-lookup"><span data-stu-id="0be83-136">Because the W3C XPath types are a subset of the common language runtime (CLR) types, type conversion takes place on types that are not considered to be an XPath type.</span></span> <span data-ttu-id="0be83-137">W poniższej tabeli przedstawiono odpowiednie typy W3C i odpowiedni typ środowiska CLR.</span><span class="sxs-lookup"><span data-stu-id="0be83-137">The following table shows the corresponding W3C types and the equivalent CLR type.</span></span>  
  
|<span data-ttu-id="0be83-138">Typ W3C</span><span class="sxs-lookup"><span data-stu-id="0be83-138">W3C type</span></span>|<span data-ttu-id="0be83-139">Typ CLR</span><span class="sxs-lookup"><span data-stu-id="0be83-139">CLR type</span></span>|  
|--------------|--------------|  
|`String`|<xref:System.String>|  
|`Boolean`|<xref:System.Boolean>|  
|`Number`|<xref:System.Double>|  
|`Result Tree Fragment`|<xref:System.Xml.XPath.XPathNavigator>|  
|`Node Set`|<xref:System.Xml.XPath.XPathNodeIterator>|  
  
 <span data-ttu-id="0be83-140">Typy liczbowe CLR są konwertowane na <xref:System.Double> .</span><span class="sxs-lookup"><span data-stu-id="0be83-140">CLR numeric types are converted to <xref:System.Double>.</span></span> <span data-ttu-id="0be83-141"><xref:System.DateTime>Typ jest konwertowany na <xref:System.String> .</span><span class="sxs-lookup"><span data-stu-id="0be83-141">The <xref:System.DateTime> type is converted to <xref:System.String>.</span></span> <span data-ttu-id="0be83-142"><xref:System.Xml.XPath.IXPathNavigable> typy są konwertowane na <xref:System.Xml.XPath.XPathNavigator> .</span><span class="sxs-lookup"><span data-stu-id="0be83-142"><xref:System.Xml.XPath.IXPathNavigable> types are converted to <xref:System.Xml.XPath.XPathNavigator>.</span></span> <span data-ttu-id="0be83-143">Element **XPathNavigator []** jest konwertowany na <xref:System.Xml.XPath.XPathNodeIterator> .</span><span class="sxs-lookup"><span data-stu-id="0be83-143">**XPathNavigator[]** is converted to <xref:System.Xml.XPath.XPathNodeIterator>.</span></span>  
  
 <span data-ttu-id="0be83-144">Wszystkie inne typy zgłaszają błąd.</span><span class="sxs-lookup"><span data-stu-id="0be83-144">All other types throw an error.</span></span>  
  
### <a name="importing-namespaces-and-assemblies"></a><span data-ttu-id="0be83-145">Importowanie przestrzeni nazw i zestawów</span><span class="sxs-lookup"><span data-stu-id="0be83-145">Importing Namespaces and Assemblies</span></span>  
 <span data-ttu-id="0be83-146"><xref:System.Xml.Xsl.XslCompiledTransform>Klasa wstępnie definiuje zestaw zestawów i przestrzeni nazw, które są obsługiwane domyślnie przez `msxsl:script` element.</span><span class="sxs-lookup"><span data-stu-id="0be83-146">The <xref:System.Xml.Xsl.XslCompiledTransform> class predefines a set of assemblies and namespaces that are supported by default by the `msxsl:script` element.</span></span> <span data-ttu-id="0be83-147">Można jednak użyć klas i elementów członkowskich należących do przestrzeni nazw, która nie znajduje się na wstępnie zdefiniowanej liście przez zaimportowanie zestawu i przestrzeni nazw w `msxsl:script` bloku.</span><span class="sxs-lookup"><span data-stu-id="0be83-147">However, you can use classes and members belonging to a namespace that is not on the predefined list by importing the assembly and namespace in `msxsl:script` block.</span></span>  
  
#### <a name="assemblies"></a><span data-ttu-id="0be83-148">Zestawy</span><span class="sxs-lookup"><span data-stu-id="0be83-148">Assemblies</span></span>  
 <span data-ttu-id="0be83-149">Następujące dwa zestawy są domyślnie przywoływane:</span><span class="sxs-lookup"><span data-stu-id="0be83-149">The following two assemblies are referenced by default:</span></span>  
  
- <span data-ttu-id="0be83-150">PLik System.dll</span><span class="sxs-lookup"><span data-stu-id="0be83-150">System.dll</span></span>  
  
- <span data-ttu-id="0be83-151">System.Xml.dll</span><span class="sxs-lookup"><span data-stu-id="0be83-151">System.Xml.dll</span></span>  
  
- <span data-ttu-id="0be83-152">Microsoft.VisualBasic.dll (gdy język skryptu to VB)</span><span class="sxs-lookup"><span data-stu-id="0be83-152">Microsoft.VisualBasic.dll (when the script language is VB)</span></span>  
  
 <span data-ttu-id="0be83-153">Dodatkowe zestawy można zaimportować przy użyciu `msxsl:assembly` elementu.</span><span class="sxs-lookup"><span data-stu-id="0be83-153">You can import the additional assemblies using the `msxsl:assembly` element.</span></span> <span data-ttu-id="0be83-154">Obejmuje to zestaw, gdy arkusz stylów jest kompilowany.</span><span class="sxs-lookup"><span data-stu-id="0be83-154">This includes the assembly when the style sheet is compiled.</span></span> <span data-ttu-id="0be83-155">`msxsl:assembly`Element ma następującą definicję:</span><span class="sxs-lookup"><span data-stu-id="0be83-155">The `msxsl:assembly` element has the following definition:</span></span>  
  
```xml  
<msxsl:script>  
  <msxsl:assembly name="system.assemblyName" />  
  <msxsl:assembly href="path-name" />  
    <![CDATA[  
    // User code  
    ]]>  
</msxsl:script>  
```  
  
 <span data-ttu-id="0be83-156">Ten `name` atrybut zawiera nazwę zestawu, a `href` atrybut zawiera ścieżkę do zestawu.</span><span class="sxs-lookup"><span data-stu-id="0be83-156">The `name` attribute contains the name of the assembly and the `href` attribute contains the path to the assembly.</span></span> <span data-ttu-id="0be83-157">Nazwa zestawu może być pełną nazwą, taką jak "System. Data, Version = 2.0.3600.0, Culture = neutral, PublicKeyToken = b77a5c561934e089" lub krótką nazwą, taką jak "System. Web".</span><span class="sxs-lookup"><span data-stu-id="0be83-157">The assembly name can be a full name, such as "System.Data, Version=2.0.3600.0, Culture=neutral, PublicKeyToken=b77a5c561934e089", or a short name, such as "System.Web".</span></span>  
  
#### <a name="namespaces"></a><span data-ttu-id="0be83-158">Przestrzenie nazw</span><span class="sxs-lookup"><span data-stu-id="0be83-158">Namespaces</span></span>  
 <span data-ttu-id="0be83-159">Domyślnie są uwzględniane następujące przestrzenie nazw:</span><span class="sxs-lookup"><span data-stu-id="0be83-159">The following namespaces are included by default:</span></span>  
  
- <span data-ttu-id="0be83-160">System</span><span class="sxs-lookup"><span data-stu-id="0be83-160">System</span></span>  
  
- <span data-ttu-id="0be83-161">System.Collection</span><span class="sxs-lookup"><span data-stu-id="0be83-161">System.Collection</span></span>  
  
- <span data-ttu-id="0be83-162">System.Text</span><span class="sxs-lookup"><span data-stu-id="0be83-162">System.Text</span></span>  
  
- <span data-ttu-id="0be83-163">System.Text.RegularExpressions</span><span class="sxs-lookup"><span data-stu-id="0be83-163">System.Text.RegularExpressions</span></span>  
  
- <span data-ttu-id="0be83-164">System.Xml</span><span class="sxs-lookup"><span data-stu-id="0be83-164">System.Xml</span></span>  
  
- <span data-ttu-id="0be83-165">System.Xml. Kodzie</span><span class="sxs-lookup"><span data-stu-id="0be83-165">System.Xml.Xsl</span></span>  
  
- <span data-ttu-id="0be83-166">System.Xml.XPath</span><span class="sxs-lookup"><span data-stu-id="0be83-166">System.Xml.XPath</span></span>  
  
- <span data-ttu-id="0be83-167">Microsoft. VisualBasic (gdy język skryptu to VB)</span><span class="sxs-lookup"><span data-stu-id="0be83-167">Microsoft.VisualBasic (when the script language is VB)</span></span>  
  
 <span data-ttu-id="0be83-168">Można dodać obsługę dodatkowych przestrzeni nazw przy użyciu `namespace` atrybutu.</span><span class="sxs-lookup"><span data-stu-id="0be83-168">You can add support for additional namespaces using the `namespace` attribute.</span></span> <span data-ttu-id="0be83-169">Wartość atrybutu jest nazwą przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="0be83-169">The attribute value is the name of the namespace.</span></span>  
  
```xml  
<msxsl:script>  
  <msxsl:using namespace="system.namespaceName" />  
    <![CDATA[  
    // User code  
    ]]>  
</msxsl:script>  
```  
  
## <a name="example"></a><span data-ttu-id="0be83-170">Przykład</span><span class="sxs-lookup"><span data-stu-id="0be83-170">Example</span></span>  
 <span data-ttu-id="0be83-171">W poniższym przykładzie zastosowano osadzony skrypt do obliczenia obwodu okręgu, który ma swój promień.</span><span class="sxs-lookup"><span data-stu-id="0be83-171">The following example uses an embedded script to calculate the circumference of a circle given its radius.</span></span>  
  
 [!code-csharp[XSLT_Script#1](../../../../samples/snippets/csharp/VS_Snippets_Data/XSLT_Script/CS/xslt_script.cs#1)]
 [!code-vb[XSLT_Script#1](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XSLT_Script/VB/xslt_script.vb#1)]  
  
#### <a name="numberxml"></a><span data-ttu-id="0be83-172">number.xml</span><span class="sxs-lookup"><span data-stu-id="0be83-172">number.xml</span></span>  
 [!code-xml[XSLT_Script#2](../../../../samples/snippets/xml/VS_Snippets_Data/XSLT_Script/XML/number.xml#2)]  
  
#### <a name="calcxsl"></a><span data-ttu-id="0be83-173">calc. xsl</span><span class="sxs-lookup"><span data-stu-id="0be83-173">calc.xsl</span></span>  
 [!code-xml[XSLT_Script#3](../../../../samples/snippets/xml/VS_Snippets_Data/XSLT_Script/XML/calc.xsl#3)]  
  
### <a name="output"></a><span data-ttu-id="0be83-174">Dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="0be83-174">Output</span></span>  
  
```xml  
<circles xmlns:msxsl="urn:schemas-microsoft-com:xslt" xmlns:user="urn:my-scripts">  
  <circle>  
    <radius>12</radius>  
    <circumference>75.36</circumference>  
  </circle>  
  <circle>  
    <radius>37.5</radius>  
    <circumference>235.5</circumference>  
  </circle>  
</circles>  
```  
  
## <a name="see-also"></a><span data-ttu-id="0be83-175">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="0be83-175">See also</span></span>

- [<span data-ttu-id="0be83-176">Przekształcenia XSLT</span><span class="sxs-lookup"><span data-stu-id="0be83-176">XSLT Transformations</span></span>](xslt-transformations.md)
- [<span data-ttu-id="0be83-177">Dynamiczne generowanie i kompilacja kodu źródłowego</span><span class="sxs-lookup"><span data-stu-id="0be83-177">Dynamic Source Code Generation and Compilation</span></span>](../../../framework/reflection-and-codedom/dynamic-source-code-generation-and-compilation.md)
