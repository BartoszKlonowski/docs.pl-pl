---
title: Zachowane odwołania do jednostek
ms.date: 03/30/2017
ms.assetid: 000a6cae-5972-40d6-bd6c-a9b7d9649b3c
ms.openlocfilehash: 484eb5c874c6de05acae7dcd87a477c186b81482
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95687271"
---
# <a name="entity-references-are-preserved"></a><span data-ttu-id="c1435-102">Zachowane odwołania do jednostek</span><span class="sxs-lookup"><span data-stu-id="c1435-102">Entity References are Preserved</span></span>

<span data-ttu-id="c1435-103">Gdy odwołanie do jednostki nie jest rozwinięte, ale zachowane, Document Object Model XML (DOM) kompiluje węzeł **XmlEntityReference** , gdy napotka odwołanie do jednostki.</span><span class="sxs-lookup"><span data-stu-id="c1435-103">When the entity reference is not expanded, but preserved, the XML Document Object Model (DOM) builds an **XmlEntityReference** node when it encounters an entity reference.</span></span>  
  
 <span data-ttu-id="c1435-104">Przy użyciu następującego kodu XML</span><span class="sxs-lookup"><span data-stu-id="c1435-104">Using the following XML,</span></span>  
  
```xml  
<author>Fred</author>  
<pubinfo>Published by &publisher;</pubinfo>  
```  
  
 <span data-ttu-id="c1435-105">DOM kompiluje węzeł **XmlEntityReference** , gdy napotka `&publisher;` odwołanie.</span><span class="sxs-lookup"><span data-stu-id="c1435-105">the DOM builds an **XmlEntityReference** node when it encounters the `&publisher;` reference.</span></span> <span data-ttu-id="c1435-106">**XmlEntityReference** zawiera węzły podrzędne skopiowane z zawartości w deklaracji jednostki.</span><span class="sxs-lookup"><span data-stu-id="c1435-106">The **XmlEntityReference** contains child nodes copied from the content in the entity declaration.</span></span> <span data-ttu-id="c1435-107">Poprzedni przykład kodu zawiera tekst w deklaracji jednostki, więc węzeł **XmlText** jest tworzony jako węzeł podrzędny węzła odwołania do jednostki.</span><span class="sxs-lookup"><span data-stu-id="c1435-107">The preceding code example contains text in the entity declaration, so an **XmlText** node is created as the child node of the entity reference node.</span></span>  
  
 <span data-ttu-id="c1435-108">![Struktura drzewa dla zachowanych odwołań do jednostek](media/xmlentityref-notexpanded-nodes.gif "xmlentityref_notexpanded_nodes")</span><span class="sxs-lookup"><span data-stu-id="c1435-108">![Tree structure for preserved entity references](media/xmlentityref-notexpanded-nodes.gif "xmlentityref_notexpanded_nodes")</span></span>  
<span data-ttu-id="c1435-109">Struktura drzewa dla odwołań do jednostek, które są zachowywane</span><span class="sxs-lookup"><span data-stu-id="c1435-109">Tree structure for entity references that are preserved</span></span>  
  
 <span data-ttu-id="c1435-110">Węzły podrzędne klasy **XmlEntityReference** są kopiami wszystkich węzłów podrzędnych utworzonych na podstawie węzła **XmlEntity** podczas napotkania deklaracji jednostki.</span><span class="sxs-lookup"><span data-stu-id="c1435-110">The child nodes of the **XmlEntityReference** are copies of all the child nodes created from the **XmlEntity** node when the entity declaration was encountered.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="c1435-111">Węzły skopiowane z elementu **XmlEntity** nie zawsze są wiernie kopiowane po umieszczeniu ich w węźle odwołania do jednostki.</span><span class="sxs-lookup"><span data-stu-id="c1435-111">The nodes copied from the **XmlEntity** are not always exact copies once placed under the entity reference node.</span></span> <span data-ttu-id="c1435-112">Mogą istnieć przestrzenie nazw, które znajdują się w zakresie w węźle odwołania do jednostki i mają wpływ na ostateczną konfigurację węzłów podrzędnych.</span><span class="sxs-lookup"><span data-stu-id="c1435-112">There can be namespaces that are in scope at the entity reference node, and that affects the final configuration of the child nodes.</span></span>  
  
 <span data-ttu-id="c1435-113">Domyślnie obiekty ogólne, takie jak `&abc;` są zachowywane, i węzły **XmlEntityReference** są zawsze tworzone.</span><span class="sxs-lookup"><span data-stu-id="c1435-113">By default, general entities like `&abc;` are preserved and **XmlEntityReference** nodes always created.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="c1435-114">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="c1435-114">See also</span></span>

- [<span data-ttu-id="c1435-115">XML Document Object Model (DOM)</span><span class="sxs-lookup"><span data-stu-id="c1435-115">XML Document Object Model (DOM)</span></span>](xml-document-object-model-dom.md)
