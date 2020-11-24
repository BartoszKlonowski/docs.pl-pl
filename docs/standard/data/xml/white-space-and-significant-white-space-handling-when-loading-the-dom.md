---
title: Obsługa białych znaków i istotnych białych znaków podczas ładowania modelu DOM
ms.date: 03/30/2017
ms.assetid: 1b141a0a-50d8-4ebd-83cd-a84449bb22b2
ms.openlocfilehash: 6282b47e8a63143e32df39db02e79e7b44d38275
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95675558"
---
# <a name="white-space-and-significant-white-space-handling-when-loading-the-dom"></a><span data-ttu-id="e8f1c-102">Obsługa białych znaków i istotnych białych znaków podczas ładowania modelu DOM</span><span class="sxs-lookup"><span data-stu-id="e8f1c-102">White Space and Significant White Space Handling when Loading the DOM</span></span>

<span data-ttu-id="e8f1c-103">Podczas ładowania dokumentu można ustawić opcję zachowania **białych znaków i utworzyć węzły** XmlSpace w drzewie dokumentu.</span><span class="sxs-lookup"><span data-stu-id="e8f1c-103">When loading the document, you can set the option to preserve white space and create **XmlWhitespace** nodes in the document tree.</span></span> <span data-ttu-id="e8f1c-104">Aby utworzyć białe węzły, ustaw właściwość **PreserveWhitespace** na true.</span><span class="sxs-lookup"><span data-stu-id="e8f1c-104">To create white space nodes, set the **PreserveWhitespace** property to true.</span></span> <span data-ttu-id="e8f1c-105">Jeśli właściwość jest ustawiona na **wartość false**, co oznacza, że domyślnie nie są tworzone węzły białych znaków.</span><span class="sxs-lookup"><span data-stu-id="e8f1c-105">If the property is set to **false**, which is the default, white space nodes are not created.</span></span> <span data-ttu-id="e8f1c-106">Wszystkie węzły białych miejsc są zawsze zachowywane, a węzły **XmlSignificantWhitespace** są zawsze tworzone w pamięci, aby reprezentować te dane, niezależnie od ustawienia flagi **PreserveWhitespace** .</span><span class="sxs-lookup"><span data-stu-id="e8f1c-106">Significant white spaces nodes are always preserved, and **XmlSignificantWhitespace** nodes are always created in memory to represent this data, regardless of the setting of the **PreserveWhitespace** flag.</span></span>  
  
 <span data-ttu-id="e8f1c-107">Jeśli dokument jest ładowany z czytnika, ustawienie właściwości flagi **PreserveWhitespace** w klasie **XmlDocument** ma wpływ na tworzenie węzłów **xmlbiałych** tylko wtedy, gdy właściwość **WhitespaceHandling** w **XmlTextReader** nie jest ustawiona na **WhitespaceHandling. None**.</span><span class="sxs-lookup"><span data-stu-id="e8f1c-107">If the document is loaded from a reader, then setting of the **PreserveWhitespace** flag property on the **XmlDocument** class affects the creation of **XmlWhitespace** nodes only when the **WhitespaceHandling** property on the **XmlTextReader** is not set to **WhitespaceHandling.None**.</span></span> <span data-ttu-id="e8f1c-108">Jest to wartość właściwości **WhitespaceHandling** w czytniku, która ma pierwszeństwo przed ustawieniem tej flagi w **dokumencie XmlDocument**.</span><span class="sxs-lookup"><span data-stu-id="e8f1c-108">It is the value of the **WhitespaceHandling** property on the reader that takes precedence over the setting of that flag on the **XmlDocument**.</span></span> <span data-ttu-id="e8f1c-109">Aby uzyskać więcej informacji na temat **XmlSignificantWhitespace**, zobacz <xref:System.Xml.XmlSignificantWhitespace> .</span><span class="sxs-lookup"><span data-stu-id="e8f1c-109">For more information on **XmlSignificantWhitespace**, see <xref:System.Xml.XmlSignificantWhitespace>.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="e8f1c-110">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="e8f1c-110">See also</span></span>

- [<span data-ttu-id="e8f1c-111">XML Document Object Model (DOM)</span><span class="sxs-lookup"><span data-stu-id="e8f1c-111">XML Document Object Model (DOM)</span></span>](xml-document-object-model-dom.md)
