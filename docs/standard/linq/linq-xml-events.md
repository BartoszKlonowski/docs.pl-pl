---
title: Zdarzenia LINQ to XML — LINQ to XML
description: Dowiedz się, jak używać zdarzeń XML do monitorowania zmian w drzewie XML.
ms.date: 07/20/2015
dev_langs:
- csharp
- vb
ms.assetid: ce7de951-cba7-4870-9962-733eb01cd680
ms.openlocfilehash: 755aa1a449e873a2c4f5b17d4df3eee7ecfa9969
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/08/2020
ms.locfileid: "89553339"
---
# <a name="linq-to-xml-events-linq-to-xml"></a><span data-ttu-id="ffed6-103">Zdarzenia LINQ to XML (LINQ to XML)</span><span class="sxs-lookup"><span data-stu-id="ffed6-103">LINQ to XML Events (LINQ to XML)</span></span>

<span data-ttu-id="ffed6-104">Zdarzenia LINQ to XML umożliwiają otrzymywanie powiadomień, gdy drzewo XML zostanie zmienione.</span><span class="sxs-lookup"><span data-stu-id="ffed6-104">LINQ to XML events enable you to be notified when an XML tree is altered.</span></span>

<span data-ttu-id="ffed6-105">Zdarzenia można dodawać do dowolnego wystąpienia dowolnego <xref:System.Xml.Linq.XObject> .</span><span class="sxs-lookup"><span data-stu-id="ffed6-105">You can add events to any instance of any <xref:System.Xml.Linq.XObject>.</span></span> <span data-ttu-id="ffed6-106">Procedura obsługi zdarzeń będzie następnie otrzymywać zdarzenia dotyczące modyfikacji tego <xref:System.Xml.Linq.XObject> elementu i jego elementów podrzędnych.</span><span class="sxs-lookup"><span data-stu-id="ffed6-106">The event handler will then receive events for modifications to that <xref:System.Xml.Linq.XObject> and any of its descendants.</span></span> <span data-ttu-id="ffed6-107">Na przykład można dodać program obsługi zdarzeń do elementu głównego drzewa i obsłużyć wszystkie modyfikacje drzewa z tego programu obsługi zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="ffed6-107">For example, you can add an event handler to the root of the tree, and handle all modifications to the tree from that event handler.</span></span>

<span data-ttu-id="ffed6-108">Przykłady zdarzeń LINQ to XML można znaleźć w tematach <xref:System.Xml.Linq.XObject.Changing> i <xref:System.Xml.Linq.XObject.Changed> .</span><span class="sxs-lookup"><span data-stu-id="ffed6-108">For examples of LINQ to XML events, see <xref:System.Xml.Linq.XObject.Changing> and <xref:System.Xml.Linq.XObject.Changed>.</span></span>

## <a name="types-and-events"></a><span data-ttu-id="ffed6-109">Typy i zdarzenia</span><span class="sxs-lookup"><span data-stu-id="ffed6-109">Types and events</span></span>

<span data-ttu-id="ffed6-110">Następujące typy są używane podczas pracy ze zdarzeniami:</span><span class="sxs-lookup"><span data-stu-id="ffed6-110">You use the following types when working with events:</span></span>

|<span data-ttu-id="ffed6-111">Typ</span><span class="sxs-lookup"><span data-stu-id="ffed6-111">Type</span></span>|<span data-ttu-id="ffed6-112">Opis</span><span class="sxs-lookup"><span data-stu-id="ffed6-112">Description</span></span>|
|----------|-----------------|
|<xref:System.Xml.Linq.XObjectChange>|<span data-ttu-id="ffed6-113">Określa typ zdarzenia, gdy zdarzenie jest zgłaszane dla elementu <xref:System.Xml.Linq.XObject> .</span><span class="sxs-lookup"><span data-stu-id="ffed6-113">Specifies the event type when an event is raised for an <xref:System.Xml.Linq.XObject>.</span></span>|
|<xref:System.Xml.Linq.XObjectChangeEventArgs>|<span data-ttu-id="ffed6-114">Dostarcza dane dla <xref:System.Xml.Linq.XObject.Changing> zdarzeń i <xref:System.Xml.Linq.XObject.Changed> .</span><span class="sxs-lookup"><span data-stu-id="ffed6-114">Provides data for the <xref:System.Xml.Linq.XObject.Changing> and <xref:System.Xml.Linq.XObject.Changed> events.</span></span>|

<span data-ttu-id="ffed6-115">Podczas modyfikowania drzewa XML są zgłaszane następujące zdarzenia:</span><span class="sxs-lookup"><span data-stu-id="ffed6-115">The following events are raised when you modify an XML tree:</span></span>

|<span data-ttu-id="ffed6-116">Zdarzenie</span><span class="sxs-lookup"><span data-stu-id="ffed6-116">Event</span></span>|<span data-ttu-id="ffed6-117">Opis</span><span class="sxs-lookup"><span data-stu-id="ffed6-117">Description</span></span>|
|-----------|-----------------|
|<xref:System.Xml.Linq.XObject.Changing>|<span data-ttu-id="ffed6-118">Występuje tuż przed tym <xref:System.Xml.Linq.XObject> lub dowolnym z jego obiektów podrzędnych zostanie zmieniony.</span><span class="sxs-lookup"><span data-stu-id="ffed6-118">Occurs just before this <xref:System.Xml.Linq.XObject> or any of its descendants is going to change.</span></span>|
|<xref:System.Xml.Linq.XObject.Changed>|<span data-ttu-id="ffed6-119">Występuje po <xref:System.Xml.Linq.XObject> zmianie lub dowolnych jego elementów podrzędnych.</span><span class="sxs-lookup"><span data-stu-id="ffed6-119">Occurs when an <xref:System.Xml.Linq.XObject> has changed or any of its descendants have changed.</span></span>|

## <a name="example-use-events-to-maintain-a-proper-total-when-items-are-changed"></a><span data-ttu-id="ffed6-120">Przykład: Użyj zdarzeń, aby zachować prawidłową sumę w przypadku zmiany elementów</span><span class="sxs-lookup"><span data-stu-id="ffed6-120">Example: Use events to maintain a proper total when items are changed</span></span>

<span data-ttu-id="ffed6-121">Zdarzenia są przydatne, gdy chcesz zachować pewne zagregowane informacje w drzewie XML.</span><span class="sxs-lookup"><span data-stu-id="ffed6-121">Events are useful when you want to maintain some aggregate information in an XML tree.</span></span> <span data-ttu-id="ffed6-122">Na przykład możesz chcieć zachować sumę faktury, która jest sumą elementów wiersza faktury.</span><span class="sxs-lookup"><span data-stu-id="ffed6-122">For example, you may want to maintain an invoice total that's the sum of the line items of the invoice.</span></span> <span data-ttu-id="ffed6-123">Ten przykład używa zdarzeń, aby zachować sumę wszystkich elementów podrzędnych w ramach elementu złożonego `Items` .</span><span class="sxs-lookup"><span data-stu-id="ffed6-123">This example uses events to maintain the total of all of the child elements under the complex element `Items`.</span></span>

```csharp
XElement root = new XElement("Root",
    new XElement("Total", "0"),
    new XElement("Items")
);
XElement total = root.Element("Total");
XElement items = root.Element("Items");
items.Changed += (object sender, XObjectChangeEventArgs cea) =>
{
    switch (cea.ObjectChange)
    {
        case XObjectChange.Add:
            if (sender is XElement)
                total.Value = ((int)total + (int)(XElement)sender).ToString();
            if (sender is XText)
                total.Value = ((int)total + (int)((XText)sender).Parent).ToString();
            break;
        case XObjectChange.Remove:
            if (sender is XElement)
                total.Value = ((int)total - (int)(XElement)sender).ToString();
            if (sender is XText)
                total.Value = ((int)total - Int32.Parse(((XText)sender).Value)).ToString();
            break;
    }
    Console.WriteLine("Changed {0} {1}",
      sender.GetType().ToString(), cea.ObjectChange.ToString());
};
items.SetElementValue("Item1", 25);
items.SetElementValue("Item2", 50);
items.SetElementValue("Item2", 75);
items.SetElementValue("Item3", 133);
items.SetElementValue("Item1", null);
items.SetElementValue("Item4", 100);
Console.WriteLine("Total:{0}", (int)total);
Console.WriteLine(root);
```

```vb
Module Module1
    Dim WithEvents items As XElement = Nothing
    Dim total As XElement = Nothing
    Dim root As XElement = _
            <Root>
                <Total>0</Total>
                <Items></Items>
            </Root>

    Private Sub XObjectChanged( _
            ByVal sender As Object, _
            ByVal cea As XObjectChangeEventArgs) _
            Handles items.Changed
        Select Case cea.ObjectChange
            Case XObjectChange.Add
                If sender.GetType() Is GetType(XElement) Then
                    total.Value = CStr(CInt(total.Value) + _
                            CInt((DirectCast(sender, XElement)).Value))
                End If
                If sender.GetType() Is GetType(XText) Then
                    total.Value = CStr(CInt(total.Value) + _
                            CInt((DirectCast(sender, XText)).Value))
                End If
            Case XObjectChange.Remove
                If sender.GetType() Is GetType(XElement) Then
                    total.Value = CStr(CInt(total.Value) - _
                            CInt((DirectCast(sender, XElement)).Value))
                End If
                If sender.GetType() Is GetType(XText) Then
                    total.Value = CStr(CInt(total.Value) - _
                            CInt((DirectCast(sender, XText)).Value))
                End If
        End Select
        Console.WriteLine("Changed {0} {1}", _
                            sender.GetType().ToString(), _
                            cea.ObjectChange.ToString())
    End Sub

    Sub Main()
        total = root.<Total>(0)
        items = root.<Items>(0)
        items.SetElementValue("Item1", 25)
        items.SetElementValue("Item2", 50)
        items.SetElementValue("Item2", 75)
        items.SetElementValue("Item3", 133)
        items.SetElementValue("Item1", Nothing)
        items.SetElementValue("Item4", 100)
        Console.WriteLine("Total:{0}", CInt(total))
        Console.WriteLine(root)
    End Sub
End Module
```

<span data-ttu-id="ffed6-124">Ten przykład generuje następujące wyniki:</span><span class="sxs-lookup"><span data-stu-id="ffed6-124">This example produces the following output:</span></span>

```output
Changed System.Xml.Linq.XElement Add
Changed System.Xml.Linq.XElement Add
Changed System.Xml.Linq.XText Remove
Changed System.Xml.Linq.XText Add
Changed System.Xml.Linq.XElement Add
Changed System.Xml.Linq.XElement Remove
Changed System.Xml.Linq.XElement Add
Total:308
<Root>
  <Total>308</Total>
  <Items>
    <Item2>75</Item2>
    <Item3>133</Item3>
    <Item4>100</Item4>
  </Items>
</Root>
```