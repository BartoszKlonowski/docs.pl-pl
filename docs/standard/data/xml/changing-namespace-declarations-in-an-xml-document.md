---
title: Zmienianie deklaracji przestrzeni nazw w dokumencie XML
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: a2758f40-e497-4964-8d8d-1bb68af14dcd
ms.openlocfilehash: f4f081e1db2ccacf4714ad3009eefdfc290b2ed4
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/18/2020
ms.locfileid: "94821830"
---
# <a name="changing-namespace-declarations-in-an-xml-document"></a><span data-ttu-id="3d446-102">Zmienianie deklaracji przestrzeni nazw w dokumencie XML</span><span class="sxs-lookup"><span data-stu-id="3d446-102">Changing Namespace Declarations in an XML Document</span></span>
<span data-ttu-id="3d446-103">Element **XmlDocument** ujawnia deklaracje przestrzeni nazw i atrybuty **xmlns** w ramach modelu obiektów dokumentu.</span><span class="sxs-lookup"><span data-stu-id="3d446-103">The **XmlDocument** exposes namespace declarations and **xmlns** attributes as part of the document object model.</span></span> <span data-ttu-id="3d446-104">Są one przechowywane w **XmlDocument**, dlatego po zapisaniu dokumentu można zachować jego lokalizację.</span><span class="sxs-lookup"><span data-stu-id="3d446-104">These are stored in the **XmlDocument**, so when you save the document, it can preserve the location of those attributes.</span></span> <span data-ttu-id="3d446-105">Zmiana tych atrybutów nie ma wpływu na właściwości **name**, **NamespaceURI** i **prefix** innych węzłów znajdujących się już w drzewie.</span><span class="sxs-lookup"><span data-stu-id="3d446-105">Changing these attributes has no affect on the **Name**, **NamespaceURI**, and **Prefix** properties of other nodes already in the tree.</span></span> <span data-ttu-id="3d446-106">Na przykład, Jeśli załadujesz następujący dokument, `test` element ma **NamespaceURI**`123.`</span><span class="sxs-lookup"><span data-stu-id="3d446-106">For example, if you load the following document, then the `test` element has **NamespaceURI** `123.`</span></span>  
  
```xml  
<test xmlns="123"/>  
```  
  
 <span data-ttu-id="3d446-107">Usunięcie `xmlns` atrybutu w następujący sposób oznacza, że `test` element nadal ma **NamespaceURI** `123` .</span><span class="sxs-lookup"><span data-stu-id="3d446-107">If you remove the `xmlns` attribute as follows, then the `test` element still has the **NamespaceURI** of `123`.</span></span>  
  
```vb  
doc.documentElement.RemoveAttribute("xmlns")  
```  
  
```csharp  
doc.documentElement.RemoveAttribute("xmlns");  
```  
  
 <span data-ttu-id="3d446-108">Podobnie, jeśli dodasz inny `xmlns` atrybut do `doc` elementu w następujący sposób, `test` element nadal ma **NamespaceURI** `123` .</span><span class="sxs-lookup"><span data-stu-id="3d446-108">Likewise, if you add a different `xmlns` attribute to the `doc` element as follows, then the `test` element still has **NamespaceURI** `123`.</span></span>  
  
```vb  
doc.documentElement.SetAttribute("xmlns","456")
```  
  
```csharp  
doc.documentElement.SetAttribute("xmlns","456");  
```  
  
 <span data-ttu-id="3d446-109">W związku z tym zmiana `xmlns` atrybutów nie będzie miała wpływu do momentu zapisania i ponownego załadowania obiektu **XmlDocument** .</span><span class="sxs-lookup"><span data-stu-id="3d446-109">Therefore, changing `xmlns` attributes will have no affect until you save and reload the **XmlDocument** object.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="3d446-110">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="3d446-110">See also</span></span>

- [<span data-ttu-id="3d446-111">XML Document Object Model (DOM)</span><span class="sxs-lookup"><span data-stu-id="3d446-111">XML Document Object Model (DOM)</span></span>](xml-document-object-model-dom.md)
