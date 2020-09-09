---
title: Jak filtrować według atrybutu-LINQ to XML
description: W tym artykule pokazano, jak używać zapytań LINQ to XML i XPath w językach C# i Visual Basic, aby znaleźć elementy podrzędne, które mają określoną nazwę i wartość atrybutu.
ms.date: 07/20/2015
dev_langs:
- csharp
- vb
ms.assetid: 208d6256-1bd7-4237-b2c9-909f26dfd0e2
ms.openlocfilehash: 51867cefcdfc42812d4003fb669c11751fb3ca34
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/08/2020
ms.locfileid: "89552909"
---
# <a name="how-to-filter-on-an-attribute-linq-to-xml"></a><span data-ttu-id="07a3f-103">Jak filtrować atrybut (LINQ to XML)</span><span class="sxs-lookup"><span data-stu-id="07a3f-103">How to filter on an attribute (LINQ to XML)</span></span>

<span data-ttu-id="07a3f-104">W tym artykule pokazano, jak używać zapytań LINQ to XML i XPath w językach C# i Visual Basic, aby znaleźć elementy podrzędne, które mają określoną nazwę i wartość atrybutu.</span><span class="sxs-lookup"><span data-stu-id="07a3f-104">This article shows how to use LINQ to XML query and XPath, in C# and Visual Basic, to find descendant elements that have a specified name and attribute value.</span></span>

## <a name="example-find-all-descendant-elements-that-have-a-specified-name-and-attribute-value"></a><span data-ttu-id="07a3f-105">Przykład: Znajdź wszystkie elementy zależne, które mają określoną nazwę i wartość atrybutu</span><span class="sxs-lookup"><span data-stu-id="07a3f-105">Example: Find all descendant elements that have a specified name and attribute value</span></span>

<span data-ttu-id="07a3f-106">W tym przykładzie używane są zapytania LINQ to XML i XPath do znajdowania w przykładowym [pliku XML dokumentu XML: wiele zamówień zakupu](sample-xml-file-multiple-purchase-orders.md), wszystkie elementy zależne mające nazwę `Address` i `Type` atrybut, którego wartością jest "wysyłka".</span><span class="sxs-lookup"><span data-stu-id="07a3f-106">This example uses LINQ to XML query and XPath to find, in XML document [Sample XML file: Multiple purchase orders](sample-xml-file-multiple-purchase-orders.md), all descendant elements that have the name `Address`, and a `Type` attribute whose value is "Shipping".</span></span> <span data-ttu-id="07a3f-107">Wyrażenie XPath jest `.//Address[@Type='Shipping']`</span><span class="sxs-lookup"><span data-stu-id="07a3f-107">The XPath expression is `.//Address[@Type='Shipping']`</span></span>

```csharp
XDocument po = XDocument.Load("PurchaseOrders.xml");

// LINQ to XML query
IEnumerable<XElement> list1 =
    from el in po.Descendants("Address")
    where (string)el.Attribute("Type") == "Shipping"
    select el;

// XPath expression
IEnumerable<XElement> list2 = po.XPathSelectElements(".//Address[@Type='Shipping']");

if (list1.Count() == list2.Count() &&
        list1.Intersect(list2).Count() == list1.Count())
    Console.WriteLine("Results are identical");
else
    Console.WriteLine("Results differ");
foreach (XElement el in list1)
    Console.WriteLine(el);
```

```vb
Dim po As XDocument = XDocument.Load("PurchaseOrders.xml")

' LINQ to XML query
Dim list1 As IEnumerable(Of XElement) = _
    From el In po...<Address> _
    Where el.@Type = "Shipping" _
    Select el

' XPath expression
Dim list2 As IEnumerable(Of XElement) = _
    po.XPathSelectElements(".//Address[@Type='Shipping']")

If (list1.Count = list2.Count And _
        list1.Intersect(list2).Count() = list1.Count()) Then
    Console.WriteLine("Results are identical")
Else
    Console.WriteLine("Results differ")
End If
For Each el As XElement In list1
    Console.WriteLine(el)
Next
```

<span data-ttu-id="07a3f-108">Ten przykład generuje następujące wyniki:</span><span class="sxs-lookup"><span data-stu-id="07a3f-108">This example produces the following output:</span></span>

```output
Results are identical
<Address Type="Shipping">
  <Name>Ellen Adams</Name>
  <Street>123 Maple Street</Street>
  <City>Mill Valley</City>
  <State>CA</State>
  <Zip>10999</Zip>
  <Country>USA</Country>
</Address>
<Address Type="Shipping">
  <Name>Cristian Osorio</Name>
  <Street>456 Main Street</Street>
  <City>Buffalo</City>
  <State>NY</State>
  <Zip>98112</Zip>
  <Country>USA</Country>
</Address>
<Address Type="Shipping">
  <Name>Jessica Arnold</Name>
  <Street>4055 Madison Ave</Street>
  <City>Seattle</City>
  <State>WA</State>
  <Zip>98112</Zip>
  <Country>USA</Country>
</Address>
```

## <a name="see-also"></a><span data-ttu-id="07a3f-109">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="07a3f-109">See also</span></span>

- [<span data-ttu-id="07a3f-110">LINQ to XML dla użytkowników XPath (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="07a3f-110">LINQ to XML for XPath Users (Visual Basic)</span></span>](/../../visual-basic/programming-guide/concepts/linq/linq-to-xml-for-xpath-users.md)