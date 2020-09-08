---
title: Tworzenie drzew XML w języku C# — LINQ to XML
description: Drzewo XML można utworzyć w języku C# przy użyciu konstruktorów LINQ to XML XElement i XAttribute i można sprawić, aby kod był podobny do struktury bazowego kodu XML.
ms.date: 08/31/2018
ms.assetid: cc74234a-0bac-4327-9c8c-5a2ead15b595
ms.openlocfilehash: 97bf40d84f40eabf6fa84f10bf4febb7697b10f5
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/08/2020
ms.locfileid: "89553759"
---
# <a name="create-xml-trees-in-c-linq-to-xml"></a><span data-ttu-id="26ea9-103">Tworzenie drzew XML w języku C# (LINQ to XML)</span><span class="sxs-lookup"><span data-stu-id="26ea9-103">Create XML trees in C# (LINQ to XML)</span></span>

<span data-ttu-id="26ea9-104">Ten artykuł zawiera informacje dotyczące tworzenia drzew XML w języku C#.</span><span class="sxs-lookup"><span data-stu-id="26ea9-104">This article provides information about creating XML trees in C#.</span></span>

<span data-ttu-id="26ea9-105">Aby uzyskać informacje o używaniu wyników zapytań LINQ jako zawartości dla elementu <xref:System.Xml.Linq.XElement> , zobacz [funkcjonalne konstruowanie](functional-construction.md).</span><span class="sxs-lookup"><span data-stu-id="26ea9-105">For information about using the results of LINQ queries as the content for an <xref:System.Xml.Linq.XElement>, see [Functional construction](functional-construction.md).</span></span>

## <a name="construct-elements"></a><span data-ttu-id="26ea9-106">Konstruuj elementy</span><span class="sxs-lookup"><span data-stu-id="26ea9-106">Construct elements</span></span>

<span data-ttu-id="26ea9-107">Sygnatury <xref:System.Xml.Linq.XElement> i <xref:System.Xml.Linq.XAttribute> konstruktorów umożliwiają przekazanie zawartości elementu lub atrybutu jako argumenty do konstruktora.</span><span class="sxs-lookup"><span data-stu-id="26ea9-107">The signatures of the <xref:System.Xml.Linq.XElement> and <xref:System.Xml.Linq.XAttribute> constructors let you pass the contents of the element or attribute as arguments to the constructor.</span></span> <span data-ttu-id="26ea9-108">Ponieważ jeden z konstruktorów przyjmuje zmienną liczbę argumentów, można przekazać dowolną liczbę elementów podrzędnych.</span><span class="sxs-lookup"><span data-stu-id="26ea9-108">Because one of the constructors takes a variable number of arguments, you can pass any number of child elements.</span></span> <span data-ttu-id="26ea9-109">Oczywiście każdy z tych elementów podrzędnych może zawierać własne elementy podrzędne.</span><span class="sxs-lookup"><span data-stu-id="26ea9-109">Of course, each of those child elements can contain their own child elements.</span></span> <span data-ttu-id="26ea9-110">Dla dowolnego elementu można dodać dowolną liczbę atrybutów.</span><span class="sxs-lookup"><span data-stu-id="26ea9-110">For any element, you can add any number of attributes.</span></span>

<span data-ttu-id="26ea9-111">W przypadku dodawania <xref:System.Xml.Linq.XNode> (w tym <xref:System.Xml.Linq.XElement> ) lub <xref:System.Xml.Linq.XAttribute> obiektów, jeśli nowa zawartość nie ma elementu nadrzędnego, obiekty są po prostu dołączone do drzewa XML.</span><span class="sxs-lookup"><span data-stu-id="26ea9-111">When adding <xref:System.Xml.Linq.XNode> (including <xref:System.Xml.Linq.XElement>) or <xref:System.Xml.Linq.XAttribute> objects, if the new content has no parent, the objects are simply attached to the XML tree.</span></span> <span data-ttu-id="26ea9-112">Jeśli nowa zawartość jest już nadrzędna i jest częścią innego drzewa XML, Nowa zawartość jest klonowana, a nowo sklonowana zawartość jest dołączona do drzewa XML.</span><span class="sxs-lookup"><span data-stu-id="26ea9-112">If the new content already is parented, and is part of another XML tree, the new content is cloned, and the newly cloned content is attached to the XML tree.</span></span> <span data-ttu-id="26ea9-113">W ostatnim przykładzie w tym artykule pokazano, jak to zrobić.</span><span class="sxs-lookup"><span data-stu-id="26ea9-113">The last example in this article demonstrates this.</span></span>

<span data-ttu-id="26ea9-114">Aby utworzyć obiekt `contacts` <xref:System.Xml.Linq.XElement> , można użyć następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="26ea9-114">To create a `contacts` <xref:System.Xml.Linq.XElement>, you could use the following code:</span></span>

```csharp
XElement contacts =
    new XElement("Contacts",
        new XElement("Contact",
            new XElement("Name", "Patrick Hines"),
            new XElement("Phone", "206-555-0144"),
            new XElement("Address",
                new XElement("Street1", "123 Main St"),
                new XElement("City", "Mercer Island"),
                new XElement("State", "WA"),
                new XElement("Postal", "68042")
            )
        )
    );
```

<span data-ttu-id="26ea9-115">W przypadku poprawnego wcięcia kod do konstruowania <xref:System.Xml.Linq.XElement> obiektów ściśle przypomina strukturę bazowego kodu XML.</span><span class="sxs-lookup"><span data-stu-id="26ea9-115">If indented properly, the code to construct <xref:System.Xml.Linq.XElement> objects closely resembles the structure of the underlying XML.</span></span>

## <a name="xelement-constructors"></a><span data-ttu-id="26ea9-116">Konstruktory XElement</span><span class="sxs-lookup"><span data-stu-id="26ea9-116">XElement constructors</span></span>

<span data-ttu-id="26ea9-117"><xref:System.Xml.Linq.XElement>Klasa używa następujących konstruktorów dla konstrukcji funkcjonalnej.</span><span class="sxs-lookup"><span data-stu-id="26ea9-117">The <xref:System.Xml.Linq.XElement> class uses the following constructors for functional construction.</span></span> <span data-ttu-id="26ea9-118">Należy zauważyć, że istnieją inne konstruktory dla <xref:System.Xml.Linq.XElement> , ale ponieważ nie są one używane do konstruowania funkcjonalnego, nie są wyświetlane w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="26ea9-118">Note that there are some other constructors for <xref:System.Xml.Linq.XElement>, but because they're not used for functional construction they're not listed here.</span></span>

|<span data-ttu-id="26ea9-119">Konstruktor</span><span class="sxs-lookup"><span data-stu-id="26ea9-119">Constructor</span></span>|<span data-ttu-id="26ea9-120">Opis</span><span class="sxs-lookup"><span data-stu-id="26ea9-120">Description</span></span>|
|-----------------|-----------------|
|`XElement(XName name, object content)`|<span data-ttu-id="26ea9-121">Tworzy <xref:System.Xml.Linq.XElement> .</span><span class="sxs-lookup"><span data-stu-id="26ea9-121">Creates an <xref:System.Xml.Linq.XElement>.</span></span> <span data-ttu-id="26ea9-122">`name`Parametr określa nazwę elementu; `content` określa zawartość elementu.</span><span class="sxs-lookup"><span data-stu-id="26ea9-122">The `name` parameter specifies the name of the element; `content` specifies the content of the element.</span></span>|
|`XElement(XName name)`|<span data-ttu-id="26ea9-123">Tworzy obiekt <xref:System.Xml.Linq.XElement> z <xref:System.Xml.Linq.XName> zainicjowanym do określonej nazwy.</span><span class="sxs-lookup"><span data-stu-id="26ea9-123">Creates an <xref:System.Xml.Linq.XElement> with its <xref:System.Xml.Linq.XName> initialized to the specified name.</span></span>|
|`XElement(XName name, params object[] content)`|<span data-ttu-id="26ea9-124">Tworzy obiekt <xref:System.Xml.Linq.XElement> z <xref:System.Xml.Linq.XName> zainicjowanym do określonej nazwy.</span><span class="sxs-lookup"><span data-stu-id="26ea9-124">Creates an <xref:System.Xml.Linq.XElement> with its <xref:System.Xml.Linq.XName> initialized to the specified name.</span></span> <span data-ttu-id="26ea9-125">Atrybuty i/lub elementy podrzędne są tworzone na podstawie zawartości listy parametrów.</span><span class="sxs-lookup"><span data-stu-id="26ea9-125">The attributes and/or child elements are created from the contents of the parameter list.</span></span>|

<span data-ttu-id="26ea9-126">`content`Parametr jest niezwykle elastyczny.</span><span class="sxs-lookup"><span data-stu-id="26ea9-126">The `content` parameter is extremely flexible.</span></span> <span data-ttu-id="26ea9-127">Obsługuje wszystkie typy obiektów, które są prawidłowymi elementami podrzędnymi <xref:System.Xml.Linq.XElement> .</span><span class="sxs-lookup"><span data-stu-id="26ea9-127">It supports any type of object that's a valid child of an <xref:System.Xml.Linq.XElement>.</span></span> <span data-ttu-id="26ea9-128">Następujące reguły mają zastosowanie do różnych typów obiektów przekazaną w tym parametrze:</span><span class="sxs-lookup"><span data-stu-id="26ea9-128">The following rules apply to different types of objects passed in this parameter:</span></span>

- <span data-ttu-id="26ea9-129">Ciąg jest dodawany jako zawartość tekstowa.</span><span class="sxs-lookup"><span data-stu-id="26ea9-129">A string is added as text content.</span></span>
- <span data-ttu-id="26ea9-130"><xref:System.Xml.Linq.XElement>Jest dodawany jako element podrzędny.</span><span class="sxs-lookup"><span data-stu-id="26ea9-130">An <xref:System.Xml.Linq.XElement> is added as a child element.</span></span>
- <span data-ttu-id="26ea9-131">Element <xref:System.Xml.Linq.XAttribute> jest dodawany jako atrybut.</span><span class="sxs-lookup"><span data-stu-id="26ea9-131">An <xref:System.Xml.Linq.XAttribute> is added as an attribute.</span></span>
- <span data-ttu-id="26ea9-132">Element <xref:System.Xml.Linq.XProcessingInstruction> , <xref:System.Xml.Linq.XComment> , lub <xref:System.Xml.Linq.XText> jest dodawany jako zawartość podrzędna.</span><span class="sxs-lookup"><span data-stu-id="26ea9-132">An <xref:System.Xml.Linq.XProcessingInstruction>, <xref:System.Xml.Linq.XComment>, or <xref:System.Xml.Linq.XText> is added as child content.</span></span>
- <span data-ttu-id="26ea9-133"><xref:System.Collections.IEnumerable>Wyliczenie jest wyliczane i reguły są stosowane cyklicznie do wyników.</span><span class="sxs-lookup"><span data-stu-id="26ea9-133">An <xref:System.Collections.IEnumerable> is enumerated, and these rules are applied recursively to the results.</span></span>
- <span data-ttu-id="26ea9-134">Dla każdego innego typu `ToString` Metoda jest wywoływana, a wynik jest dodawany jako zawartość tekstowa.</span><span class="sxs-lookup"><span data-stu-id="26ea9-134">For any other type, its `ToString` method is called and the result is added as text content.</span></span>

## <a name="example-create-an-xelement-with-content"></a><span data-ttu-id="26ea9-135">Przykład: Tworzenie elementu XElement z zawartością</span><span class="sxs-lookup"><span data-stu-id="26ea9-135">Example: Create an XElement with content</span></span>

<span data-ttu-id="26ea9-136">Można utworzyć obiekt zawierający <xref:System.Xml.Linq.XElement> prostą zawartość z pojedynczym wywołaniem metody.</span><span class="sxs-lookup"><span data-stu-id="26ea9-136">You can create an <xref:System.Xml.Linq.XElement> that contains simple content with a single method call.</span></span> <span data-ttu-id="26ea9-137">W tym celu określ zawartość jako drugi parametr w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="26ea9-137">To do this, specify the content as the second parameter, as follows:</span></span>

```csharp
XElement n = new XElement("Customer", "Adventure Works");
Console.WriteLine(n);
```

<span data-ttu-id="26ea9-138">Ten przykład generuje następujące wyniki:</span><span class="sxs-lookup"><span data-stu-id="26ea9-138">This example produces the following output:</span></span>

```xml
<Customer>Adventure Works</Customer>
```

<span data-ttu-id="26ea9-139">Każdy typ obiektu można przekazać jako zawartość.</span><span class="sxs-lookup"><span data-stu-id="26ea9-139">You can pass any type of object as the content.</span></span> <span data-ttu-id="26ea9-140">Na przykład poniższy kod tworzy element, który zawiera liczbę zmiennoprzecinkową jako zawartość:</span><span class="sxs-lookup"><span data-stu-id="26ea9-140">For example, the following code creates an element that contains a floating point number as content:</span></span>

```csharp
XElement n = new XElement("Cost", 324.50);
Console.WriteLine(n);
```

<span data-ttu-id="26ea9-141">Ten przykład generuje następujące wyniki:</span><span class="sxs-lookup"><span data-stu-id="26ea9-141">This example produces the following output:</span></span>

```xml
<Cost>324.5</Cost>
```

<span data-ttu-id="26ea9-142">Liczba zmiennoprzecinkowa jest opakowana i przenoszona do konstruktora.</span><span class="sxs-lookup"><span data-stu-id="26ea9-142">The floating point number is boxed and passed in to the constructor.</span></span> <span data-ttu-id="26ea9-143">Numer opakowany jest konwertowany na ciąg i używany jako zawartość elementu.</span><span class="sxs-lookup"><span data-stu-id="26ea9-143">The boxed number is converted to a string and used as the content of the element.</span></span>

## <a name="example-create-an-xelement-with-a-child-element"></a><span data-ttu-id="26ea9-144">Przykład: Tworzenie elementu XElement z elementem podrzędnym</span><span class="sxs-lookup"><span data-stu-id="26ea9-144">Example: Create an XElement with a child element</span></span>

<span data-ttu-id="26ea9-145">Jeśli przekazujesz wystąpienie <xref:System.Xml.Linq.XElement> klasy dla argumentu Content, Konstruktor tworzy element z elementem podrzędnym:</span><span class="sxs-lookup"><span data-stu-id="26ea9-145">If you pass an instance of the <xref:System.Xml.Linq.XElement> class for the content argument, the constructor creates an element with a child element:</span></span>

```csharp
XElement shippingUnit = new XElement("ShippingUnit",
    new XElement("Cost", 324.50)
);
Console.WriteLine(shippingUnit);
```

<span data-ttu-id="26ea9-146">Ten przykład generuje następujące wyniki:</span><span class="sxs-lookup"><span data-stu-id="26ea9-146">This example produces the following output:</span></span>

```xml
<ShippingUnit>
  <Cost>324.5</Cost>
</ShippingUnit>
```

## <a name="example-create-an-xelement-with-multiple-child-elements"></a><span data-ttu-id="26ea9-147">Przykład: Tworzenie elementu XElement z wieloma elementami podrzędnymi</span><span class="sxs-lookup"><span data-stu-id="26ea9-147">Example: Create an XElement with multiple child elements</span></span>

<span data-ttu-id="26ea9-148">Można przekazać wiele <xref:System.Xml.Linq.XElement> obiektów dla zawartości.</span><span class="sxs-lookup"><span data-stu-id="26ea9-148">You can pass in a number of <xref:System.Xml.Linq.XElement> objects for the content.</span></span> <span data-ttu-id="26ea9-149">Każdy <xref:System.Xml.Linq.XElement> obiekt jest dołączony jako element podrzędny.</span><span class="sxs-lookup"><span data-stu-id="26ea9-149">Each of the <xref:System.Xml.Linq.XElement> objects is included as a child element.</span></span>

```csharp
XElement address = new XElement("Address",
    new XElement("Street1", "123 Main St"),
    new XElement("City", "Mercer Island"),
    new XElement("State", "WA"),
    new XElement("Postal", "68042")
);
Console.WriteLine(address);
```

<span data-ttu-id="26ea9-150">Ten przykład generuje następujące wyniki:</span><span class="sxs-lookup"><span data-stu-id="26ea9-150">This example produces the following output:</span></span>

```xml
<Address>
  <Street1>123 Main St</Street1>
  <City>Mercer Island</City>
  <State>WA</State>
  <Postal>68042</Postal>
</Address>
```

<span data-ttu-id="26ea9-151">Rozszerzając poprzedni przykład, można utworzyć całe drzewo XML w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="26ea9-151">By extending the previous example, you can create an entire XML tree, as follows:</span></span>

```csharp
XElement contacts =
    new XElement("Contacts",
        new XElement("Contact",
            new XElement("Name", "Patrick Hines"),
            new XElement("Phone", "206-555-0144"),
            new XElement("Address",
                new XElement("Street1", "123 Main St"),
                new XElement("City", "Mercer Island"),
                new XElement("State", "WA"),
                new XElement("Postal", "68042")
            )
        )
    );
Console.WriteLine(contacts);
```

<span data-ttu-id="26ea9-152">Ten przykład generuje następujące wyniki:</span><span class="sxs-lookup"><span data-stu-id="26ea9-152">This example produces the following output:</span></span>

```xml
<Contacts>
  <Contact>
    <Name>Patrick Hines</Name>
    <Phone>206-555-0144</Phone>
    <Address>
      <Street1>123 Main St</Street1>
      <City>Mercer Island</City>
      <State>WA</State>
      <Postal>68042</Postal>
    </Address>
  </Contact>
</Contacts>
```

## <a name="example-create-an-xelement-with-an-xattribute"></a><span data-ttu-id="26ea9-153">Przykład: Tworzenie elementu XElement za pomocą XAttribute</span><span class="sxs-lookup"><span data-stu-id="26ea9-153">Example: Create an XElement with an XAttribute</span></span>

<span data-ttu-id="26ea9-154">Jeśli przekazujesz wystąpienie <xref:System.Xml.Linq.XAttribute> klasy dla argumentu Content, Konstruktor tworzy element z atrybutem:</span><span class="sxs-lookup"><span data-stu-id="26ea9-154">If you pass an instance of the <xref:System.Xml.Linq.XAttribute> class for the content argument, the constructor creates an element with an attribute:</span></span>

```csharp
XElement phone = new XElement("Phone",
    new XAttribute("Type", "Home"),
    "555-555-5555");
Console.WriteLine(phone);
```

<span data-ttu-id="26ea9-155">Ten przykład generuje następujące wyniki:</span><span class="sxs-lookup"><span data-stu-id="26ea9-155">This example produces the following output:</span></span>

```xml
<Phone Type="Home">555-555-5555</Phone>
```

## <a name="example-create-an-empty-element"></a><span data-ttu-id="26ea9-156">Przykład: Tworzenie pustego elementu</span><span class="sxs-lookup"><span data-stu-id="26ea9-156">Example: Create an empty element</span></span>

<span data-ttu-id="26ea9-157">Aby utworzyć pusty <xref:System.Xml.Linq.XElement> , nie przekazuj żadnej zawartości do konstruktora.</span><span class="sxs-lookup"><span data-stu-id="26ea9-157">To create an empty <xref:System.Xml.Linq.XElement>, don't pass any content to the constructor.</span></span> <span data-ttu-id="26ea9-158">Poniższy przykład tworzy pusty element:</span><span class="sxs-lookup"><span data-stu-id="26ea9-158">The following example creates an empty element:</span></span>

```csharp
XElement n = new XElement("Customer");
Console.WriteLine(n);
```

<span data-ttu-id="26ea9-159">Ten przykład generuje następujące wyniki:</span><span class="sxs-lookup"><span data-stu-id="26ea9-159">This example produces the following output:</span></span>

```xml
<Customer />
```

## <a name="example-attach-vs-clone"></a><span data-ttu-id="26ea9-160">Przykład: Attach a klon</span><span class="sxs-lookup"><span data-stu-id="26ea9-160">Example: Attach vs. clone</span></span>

<span data-ttu-id="26ea9-161">Jak wspomniano wcześniej, podczas dodawania <xref:System.Xml.Linq.XNode> (w tym <xref:System.Xml.Linq.XElement> ) lub <xref:System.Xml.Linq.XAttribute> obiektów, jeśli nowa zawartość nie ma elementu nadrzędnego, obiekty są po prostu dołączone do drzewa XML.</span><span class="sxs-lookup"><span data-stu-id="26ea9-161">As mentioned previously, when adding <xref:System.Xml.Linq.XNode> (including <xref:System.Xml.Linq.XElement>) or <xref:System.Xml.Linq.XAttribute> objects, if the new content has no parent, the objects are simply attached to the XML tree.</span></span> <span data-ttu-id="26ea9-162">Jeśli nowa zawartość jest już nadrzędna i jest częścią innego drzewa XML, Nowa zawartość jest klonowana, a nowo sklonowana zawartość jest dołączona do drzewa XML.</span><span class="sxs-lookup"><span data-stu-id="26ea9-162">If the new content already is parented and is part of another XML tree, the new content is cloned, and the newly cloned content is attached to the XML tree.</span></span>

<span data-ttu-id="26ea9-163">Poniższy przykład ilustruje zachowanie po dodaniu elementu nadrzędnego do drzewa i po dodaniu elementu bez elementu nadrzędnego do drzewa:</span><span class="sxs-lookup"><span data-stu-id="26ea9-163">The following example demonstrates the behavior when you add a parented element to a tree, and when you add an element with no parent to a tree:</span></span>

```csharp
// Create a tree with a child element.
XElement xmlTree1 = new XElement("Root",
    new XElement("Child1", 1)
);

// Create an element that's not parented.
XElement child2 = new XElement("Child2", 2);

// Create a tree and add Child1 and Child2 to it.
XElement xmlTree2 = new XElement("Root",
    xmlTree1.Element("Child1"),
    child2
);

// Compare Child1 identity.
Console.WriteLine("Child1 was {0}",
    xmlTree1.Element("Child1") == xmlTree2.Element("Child1") ?
    "attached" : "cloned");

// Compare Child2 identity.
Console.WriteLine("Child2 was {0}",
    child2 == xmlTree2.Element("Child2") ?
    "attached" : "cloned");

// This example produces the following output:
//    Child1 was cloned
//    Child2 was attached
```

## <a name="see-also"></a><span data-ttu-id="26ea9-164">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="26ea9-164">See also</span></span>

- [<span data-ttu-id="26ea9-165">Konstrukcja funkcjonalna</span><span class="sxs-lookup"><span data-stu-id="26ea9-165">Functional construction</span></span>](functional-construction.md)
