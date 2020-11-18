---
title: Wynikowy fragment drzewa w przekształceniach
ms.date: 03/30/2017
ms.assetid: df363480-ba02-4233-9ddf-8434e421c4f1
ms.openlocfilehash: e5ca285c0b5d6c32d15647508c611a47ed97ee03
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/18/2020
ms.locfileid: "94823566"
---
# <a name="result-tree-fragment-in-transformations"></a><span data-ttu-id="88586-102">Wynikowy fragment drzewa w przekształceniach</span><span class="sxs-lookup"><span data-stu-id="88586-102">Result Tree Fragment in Transformations</span></span>

> [!NOTE]
> <span data-ttu-id="88586-103"><xref:System.Xml.Xsl.XslTransform>Klasa jest przestarzała w .NET Framework 2,0.</span><span class="sxs-lookup"><span data-stu-id="88586-103">The <xref:System.Xml.Xsl.XslTransform> class is obsolete in the .NET Framework 2.0.</span></span> <span data-ttu-id="88586-104">Można wykonać przekształcenia Extensible Stylesheet Language for Transformations (XSLT) przy użyciu <xref:System.Xml.Xsl.XslCompiledTransform> klasy.</span><span class="sxs-lookup"><span data-stu-id="88586-104">You can perform Extensible Stylesheet Language for Transformations (XSLT) transformations using the <xref:System.Xml.Xsl.XslCompiledTransform> class.</span></span> <span data-ttu-id="88586-105">Aby uzyskać więcej informacji, zobacz [Używanie klasy XslCompiledTransform](using-the-xslcompiledtransform-class.md) i [Migrowanie z klasy XslTransform](migrating-from-the-xsltransform-class.md) .</span><span class="sxs-lookup"><span data-stu-id="88586-105">See [Using the XslCompiledTransform Class](using-the-xslcompiledtransform-class.md) and [Migrating From the XslTransform Class](migrating-from-the-xsltransform-class.md) for more information.</span></span>

 <span data-ttu-id="88586-106">Fragmenty drzewa wyników, znane także jako fragmenty drzewa wyników, nie są dłuższe niż specjalny typ zestawu węzłów.</span><span class="sxs-lookup"><span data-stu-id="88586-106">Result tree fragments, also known as result tree fragments, are nothing more than a special type of node set.</span></span> <span data-ttu-id="88586-107">Można wykonać dowolną z nich funkcję, którą można wykonać w zestawie węzłów.</span><span class="sxs-lookup"><span data-stu-id="88586-107">You can perform any function on them that can be performed on a node set.</span></span> <span data-ttu-id="88586-108">Można również skonwertować fragment drzewa wynikowy do zestawu węzłów przy użyciu `node-set()` funkcji, a następnie użyć jej w dowolnym miejscu, w którym można użyć zestawu węzłów.</span><span class="sxs-lookup"><span data-stu-id="88586-108">Or, you can also convert a result tree fragment to a node set using the `node-set()` function and subsequently use it any place that a node set can be used.</span></span>

 <span data-ttu-id="88586-109">Fragment drzewa wynik jest tworzony w wyniku użycia `<xsl:variable>` `<xsl:param>` elementu lub w określony sposób w arkuszu stylów.</span><span class="sxs-lookup"><span data-stu-id="88586-109">A result tree fragment is created as a result of using an `<xsl:variable>` or `<xsl:param>` element in a specific manner in a style sheet.</span></span> <span data-ttu-id="88586-110">Składnia dla `variable` i `parameter` elementów jest następująca:</span><span class="sxs-lookup"><span data-stu-id="88586-110">The syntax for the `variable` and `parameter` elements is as follows:</span></span>

```xml
<xsl:param name=Qname select= XPath Expression >
    template body
</xsl:param>

<xsl:variable name=Qname select=XPath Expression >
    template body
</xsl:variable>
```

<span data-ttu-id="88586-111">Dla `parameter` elementu wartość jest przypisywana do kwalifikowanej nazwy ( `Qname` ) na kilka sposobów.</span><span class="sxs-lookup"><span data-stu-id="88586-111">For the `parameter` element, the value is assigned to the qualified name (`Qname`) in several ways.</span></span> <span data-ttu-id="88586-112">Do parametru można przypisać wartość domyślną, zwracając zawartość z wyrażenia XML Path Language (XPath) w `select` atrybucie lub przypisując jej zawartość treści szablonu.</span><span class="sxs-lookup"><span data-stu-id="88586-112">You can assign a default value to the parameter by returning content from the XML Path Language (XPath) expression in the `select` attribute, or by assigning it the contents of the template body.</span></span>

<span data-ttu-id="88586-113">Dla `variable` elementu, wartość jest również przypisywana na kilka sposobów.</span><span class="sxs-lookup"><span data-stu-id="88586-113">For the `variable` element, the value is also assigned in several ways.</span></span> <span data-ttu-id="88586-114">Można ją przypisać, zwracając zawartość z wyrażenia XPath w `select` atrybucie lub przypisując jej zawartość treści szablonu.</span><span class="sxs-lookup"><span data-stu-id="88586-114">You can assign it by returning content from the XPath expression in the `select` attribute, or by assigning it the contents of the template body.</span></span>

<span data-ttu-id="88586-115">Dla `parameter` `variable` elementów i, jeśli wartość jest przypisana przez wyrażenie XPath, zostanie zwrócony jeden z czterech podstawowych typów XPath: wartość logiczna, ciąg, liczba lub zestaw węzłów.</span><span class="sxs-lookup"><span data-stu-id="88586-115">For both the `parameter` and `variable` elements, if a value is assigned by the XPath expression, then one of the four basic XPath types will be returned: Boolean, string, number, or node set.</span></span> <span data-ttu-id="88586-116">Gdy wartość jest podawana przy użyciu niepustej treści szablonu, zwracany jest typ danych inny niż XPath, który będzie fragmentem drzewa wyników.</span><span class="sxs-lookup"><span data-stu-id="88586-116">When the value is given by using a non-empty template body, then a non-XPath data type is returned, and that will be a result tree fragment.</span></span>

<span data-ttu-id="88586-117">Gdy zmienna jest powiązana z fragmentem drzewa wyników zamiast jednego z czterech podstawowych typów danych XPath, jest to jedyna godzina, o której zapytanie XPath zwraca typ, który nie jest jednym z czterech typów obiektów XPath.</span><span class="sxs-lookup"><span data-stu-id="88586-117">When a variable is bound to a result tree fragment instead of one of the four basic XPath data types, this is the only time that an XPath query returns a type that is not one of the four XPath object types.</span></span> <span data-ttu-id="88586-118">Fragmenty drzewa wyników i ich zachowanie zostały omówione w [specyfikacji organizacja World Wide Web Consortium (W3C)](https://www.w3.org/TR/xslt-10/), [sekcja 11,1 fragmenty drzewa wyników](https://www.w3.org/TR/xslt-10/#section-Result-Tree-Fragments) w [sekcji 11,6 Przekazywanie parametrów do szablonów](https://www.w3.org/TR/xslt-10/#section-Passing-Parameters-to-Templates).</span><span class="sxs-lookup"><span data-stu-id="88586-118">Result tree fragments and their behavior are discussed in the [World Wide Web Consortium (W3C) specification](https://www.w3.org/TR/xslt-10/), [section 11.1 Result Tree Fragments](https://www.w3.org/TR/xslt-10/#section-Result-Tree-Fragments) through [section 11.6 Passing Parameters to Templates](https://www.w3.org/TR/xslt-10/#section-Passing-Parameters-to-Templates).</span></span> <span data-ttu-id="88586-119">Ponadto w [sekcji 1](https://www.w3.org/TR/xslt-10/#section-Introduction) opisano sposób, w jaki szablony mogą zawierać elementy z przestrzeni nazw XSLT, które zwracają lub tworzą fragmenty drzewa wyników.</span><span class="sxs-lookup"><span data-stu-id="88586-119">Also, [section 1 Introduction](https://www.w3.org/TR/xslt-10/#section-Introduction) discusses how templates can contain elements from the XSLT namespace that return or create result tree fragments.</span></span>

<span data-ttu-id="88586-120">Fragment drzewa wyników, w koncepcji, zachowuje się jak zestaw węzłów bez więcej niż jeden węzeł główny.</span><span class="sxs-lookup"><span data-stu-id="88586-120">A result tree fragment, in concept, behaves like a node set with nothing more than a single root node.</span></span> <span data-ttu-id="88586-121">Pozostałe zwrócone węzły są jednak węzłami podrzędnymi.</span><span class="sxs-lookup"><span data-stu-id="88586-121">However, the rest of the nodes returned are child nodes.</span></span> <span data-ttu-id="88586-122">Aby programowo wyświetlić węzły podrzędne, skopiuj fragment drzewa wynik do drzewa wynik przy użyciu `<xsl:copy-of>` elementu.</span><span class="sxs-lookup"><span data-stu-id="88586-122">To programmatically see the child nodes, copy the result tree fragment to the result tree using the `<xsl:copy-of>` element.</span></span> <span data-ttu-id="88586-123">Gdy wykonywana jest kopia, wszystkie węzły podrzędne są również kopiowane do drzewa wynik w sekwencji.</span><span class="sxs-lookup"><span data-stu-id="88586-123">When the copy-of is performed, all the child nodes are also copied to the result tree in sequence.</span></span> <span data-ttu-id="88586-124">Do momentu `copy` `copy-of` użycia lub, fragment drzewa wynik nie jest częścią drzewa wyników ani danych wyjściowych transformacji.</span><span class="sxs-lookup"><span data-stu-id="88586-124">Until a `copy` or `copy-of` is used, a result tree fragment is not part of the result tree or the output from the transformation.</span></span>

<span data-ttu-id="88586-125">Do iteracji w zwróconych węzłach fragmentu drzewa wynik <xref:System.Xml.XPath.XPathNavigator> jest używany.</span><span class="sxs-lookup"><span data-stu-id="88586-125">To iterate over the returned nodes of a result tree fragment, an <xref:System.Xml.XPath.XPathNavigator> is used.</span></span> <span data-ttu-id="88586-126">Poniższy przykład kodu pokazuje, jak utworzyć fragment drzewa wyników w arkuszu stylów, wywołując funkcję z parametrem `fragment` , który zawiera kod XML.</span><span class="sxs-lookup"><span data-stu-id="88586-126">The following code sample shows how to create a result tree fragment within a style sheet by calling the function with a parameter `fragment`, which contains XML.</span></span>

```xml
<xsl:stylesheet xmlns:xsl="http://www.w3.org/1999/XSL/Transform"
                xmlns:msxsl="urn:schemas-microsoft-com:xslt"
                xmlns:user="http://www.adventure-works.com"
                version="1.0">
    <xsl:var name="fragment">
        <node1>
            <node2/>
        </node1>
    <xsl:var>

  <msxsl:script language="C#" implements-prefix="user">
    function NodeFragment(XPathNavigator nav)
    {
      if (nav.HasSelection == false)
        XPathNavigator.MoveToNext();
      return;
    }
  </msxsl:script>

    <xsl:template match="/">
            <xsl:value-of select="user:NodeFragment(msxml:node-set($fragment))"/>
    </xsl:template>
</xsl:stylesheet>
```

<span data-ttu-id="88586-127">Oto kolejny przykład pokazujący zmienną, która jest w formacie tekstu sformatowanego (RTF), a tym samym typ fragmentu drzewa wyników, który nie jest konwertowany na zestaw węzłów.</span><span class="sxs-lookup"><span data-stu-id="88586-127">Here is another sample showing a variable, which is in Rich Text Format (RTF), and hence, a type of result tree fragment, that is not converted to a node set.</span></span> <span data-ttu-id="88586-128">Zamiast tego jest przenoszona do funkcji skryptu i <xref:System.Xml.XPath.XPathNavigator> służy do nawigowania po węzłach.</span><span class="sxs-lookup"><span data-stu-id="88586-128">Instead, it is passed to a script function, and the <xref:System.Xml.XPath.XPathNavigator> is used to navigate over the nodes.</span></span>

```xml
<xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform"
        xmlns:msxsl="urn:schemas-microsoft-com:xslt"
        xmlns:user="urn:books"
        exclude-result-prefixes="msxsl">

<xsl:output method="xml" indent="yes" omit-xml-declaration="yes"/>

<xsl:variable name="node-fragment">
    <book>Book1</book>
    <book>Book2</book>
    <book>Book3</book>
    <book>Book4</book>
</xsl:variable>

<msxsl:script implements-prefix="user" language="c#">

<![CDATA[
    string func(XPathNavigator nav)
    {
        bool b = nav.MoveToFirstChild();
        if (b)
            return nav.Value;
        else
            return "Does not exist";
    }

]]>

</msxsl:script>

<xsl:template match="/">
    <first_book>
        <xsl:value-of select="user:func($node-fragment)"/>
    </first_book>
</xsl:template>

</xsl:stylesheet>
```

<span data-ttu-id="88586-129">Wynik przekształcenia dowolnego kodu XML z tym arkuszem stylów jest przedstawiony w następujących danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="88586-129">The result of transforming any XML with this style sheet is shown in the following output.</span></span>

## <a name="output"></a><span data-ttu-id="88586-130">Dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="88586-130">Output</span></span>

```xml
<first_book xmlns:user="urn:books">Book1</first_book>
```

<span data-ttu-id="88586-131">Jak wspomniano powyżej, `node-set` Funkcja umożliwia konwertowanie fragmentu drzewa wynikowego na zestaw węzłów.</span><span class="sxs-lookup"><span data-stu-id="88586-131">As stated above, the `node-set` function enables you to convert a result tree fragment into a node set.</span></span> <span data-ttu-id="88586-132">Węzeł z wynikiem zawsze zawiera pojedynczy węzeł, który jest węzłem głównym drzewa.</span><span class="sxs-lookup"><span data-stu-id="88586-132">The resulting node always contains a single node that is the root node of the tree.</span></span> <span data-ttu-id="88586-133">W przypadku konwertowania fragmentu drzewa wynikowego na zestaw węzłów, można go użyć wszędzie tam, gdzie jest używany zwykły zestaw węzłów, na przykład w instrukcji for-each lub w wartości `select` atrybutu.</span><span class="sxs-lookup"><span data-stu-id="88586-133">If you convert a result tree fragment to a node set, then you can use it anywhere a regular node set is used, such as in a for-each statement or in the value of a `select` attribute.</span></span> <span data-ttu-id="88586-134">Następujące wiersze kodu pokazują fragment konwertowany na zestaw węzłów i używany jako zestaw węzłów:</span><span class="sxs-lookup"><span data-stu-id="88586-134">The following lines of code show the fragment being converted to a node set and used as a node set:</span></span>

`<xsl:for-each select="msxsl:node-set($node-fragment)">`

`<xsl:value-of select="user:func(msxsl:node-set($node-fragment))"/>`

<span data-ttu-id="88586-135">Gdy fragment jest konwertowany na zestaw węzłów, nie jest już używany <xref:System.Xml.XPath.XPathNavigator> do nawigowania nad nim.</span><span class="sxs-lookup"><span data-stu-id="88586-135">When a fragment is converted to a node set, you no longer use the <xref:System.Xml.XPath.XPathNavigator> to navigate over it.</span></span> <span data-ttu-id="88586-136">W przypadku zestawu węzłów zamiast tego należy użyć elementu <xref:System.Xml.XPath.XPathNodeIterator> .</span><span class="sxs-lookup"><span data-stu-id="88586-136">For a node set, you use the <xref:System.Xml.XPath.XPathNodeIterator> instead.</span></span>

<span data-ttu-id="88586-137">W poniższym przykładzie `$var` jest to zmienna, która jest drzewem węzła w arkuszu stylów.</span><span class="sxs-lookup"><span data-stu-id="88586-137">In the following example, `$var` is a variable that is a node tree in the style sheet.</span></span> <span data-ttu-id="88586-138">Instrukcja for-each, w połączeniu z `node-set` funkcją, umożliwia użytkownikowi iterację w tym drzewie jako zestaw węzłów.</span><span class="sxs-lookup"><span data-stu-id="88586-138">The for-each statement, combined with the `node-set` function, allows the user to iterate over this tree as a node set.</span></span>

```xml
<xsl:stylesheet xmlns:xsl="http://www.w3.org/1999/XSL/Transform"
                xmlns:msxsl="urn:schemas-microsoft-com:xslt"
                xmlns:user="http://www.adventure-works.com"
                version="1.0">
    <xsl:variable name="states">
        <node1>AL</node1>
        <node1>CA</node1>
        <node1>CO</node1>
        <node1>WA</node1>
    </xsl:variable>

    <xsl:template match="/">
            <xsl:for-each select="msxsl:node-set($states)"/>
    </xsl:template>
</xsl:stylesheet>
```

<span data-ttu-id="88586-139">Oto inny przykład zmiennej, która znajduje się w formacie RTF, a w związku z tym fragment drzewa wyników, który jest konwertowany na zestaw węzłów przed przekazaniem do funkcji skryptu jako XPathNodeIterator.</span><span class="sxs-lookup"><span data-stu-id="88586-139">Here is another example of a variable that is in RTF, and hence of type result tree fragment, that is converted to a node set before being passed to a script function as XPathNodeIterator.</span></span>

```xml
<xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform"
        xmlns:msxsl="urn:schemas-microsoft-com:xslt"
        xmlns:user="urn:books"
        exclude-result-prefixes="msxsl">

<xsl:output method="xml" indent="yes" omit-xml-declaration="yes"/>

<xsl:variable name="node-fragment">
    <book>Book1</book>
    <book>Book2</book>
    <book>Book3</book>
    <book>Book4</book>
</xsl:variable>

<msxsl:script implements-prefix="user" language="c#">

<![CDATA[
    string func(XPathNodeIterator it)
    {
        it.MoveNext();
        return it.Current.Value;
        //it.Current returns XPathNavigator positioned on the current node
    }

]]>

</msxsl:script>
<xsl:template match="/">
    <books>
        <xsl:value-of select="user:func(msxsl:node-set($node-fragment))"/>
    </books>
</xsl:template>

</xsl:stylesheet>
```

<span data-ttu-id="88586-140">Poniżej przedstawiono wynik przekształcenia XML z tym arkuszem stylów:</span><span class="sxs-lookup"><span data-stu-id="88586-140">The following is the result of transforming XML with this style sheet:</span></span>

```xml
<books xmlns:user="urn:books">Book1Book2Book3Book4</books>
```

## <a name="see-also"></a><span data-ttu-id="88586-141">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="88586-141">See also</span></span>

- <xref:System.Xml.XPath.XPathNodeIterator>
- [<span data-ttu-id="88586-142">Przekształcenia XSLT przy użyciu klasy XslTransform</span><span class="sxs-lookup"><span data-stu-id="88586-142">XSLT Transformations with the XslTransform Class</span></span>](xslt-transformations-with-the-xsltransform-class.md)
- [<span data-ttu-id="88586-143">Implementowanie procesora XSLT przy użyciu klasy XslTransform</span><span class="sxs-lookup"><span data-stu-id="88586-143">XslTransform Class Implements the XSLT Processor</span></span>](xsltransform-class-implements-the-xslt-processor.md)
