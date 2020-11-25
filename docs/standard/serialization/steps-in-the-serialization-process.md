---
title: Kroki procesu serializacji
description: Proces serializacji rozpoczyna się, gdy wywoływana jest metoda serializacji w programie formatującego. W tym artykule opisano sekwencję zdarzeń.
ms.date: 08/07/2017
helpviewer_keywords:
- binary serialization, steps
- serialization, steps
ms.assetid: 4bcbc883-2a91-418f-b968-6c86a25e9737
ms.openlocfilehash: a22155f3e4cbf665e962ff79f92a6313eca7c223
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95734793"
---
# <a name="steps-in-the-serialization-process"></a><span data-ttu-id="497c9-104">Kroki procesu serializacji</span><span class="sxs-lookup"><span data-stu-id="497c9-104">Steps in the serialization process</span></span>

<span data-ttu-id="497c9-105">Gdy <xref:System.Runtime.Serialization.Formatter.Serialize%2A> Metoda jest wywoływana w programie [formatującego](xref:System.Runtime.Serialization.Formatter), serializacja obiektu odbywa się zgodnie z następującą sekwencją reguł:</span><span class="sxs-lookup"><span data-stu-id="497c9-105">When the <xref:System.Runtime.Serialization.Formatter.Serialize%2A> method is called on a [formatter](xref:System.Runtime.Serialization.Formatter), object serialization proceeds according to the following sequence of rules:</span></span>

- <span data-ttu-id="497c9-106">Dokonuje określić, czy element formatujący selektora znaków.</span><span class="sxs-lookup"><span data-stu-id="497c9-106">A check is made to determine whether the formatter has a surrogate selector.</span></span> <span data-ttu-id="497c9-107">Jeśli element formatujący Sprawdź, czy selektor dwuskładnikowego obsługi obiektów określonego typu.</span><span class="sxs-lookup"><span data-stu-id="497c9-107">If the formatter does, check whether the surrogate selector handles objects of the given type.</span></span> <span data-ttu-id="497c9-108">Jeśli selektor obsługuje typ obiektu, <xref:System.Runtime.Serialization.ISerializable.GetObjectData%2A?displayProperty=nameWithType> jest wywoływana w selektorze surogatu.</span><span class="sxs-lookup"><span data-stu-id="497c9-108">If the selector handles the object type, <xref:System.Runtime.Serialization.ISerializable.GetObjectData%2A?displayProperty=nameWithType> is called on the surrogate selector.</span></span>

- <span data-ttu-id="497c9-109">Jeśli nie ma selektora zastępcy lub jeśli nie obsługuje typu obiektu, sprawdza się w celu ustalenia, czy obiekt jest oznaczony atrybutem [możliwym do serializacji](xref:System.SerializableAttribute) .</span><span class="sxs-lookup"><span data-stu-id="497c9-109">If there is no surrogate selector or if it does not handle the object type, a check is made to determine whether the object is marked with the [Serializable](xref:System.SerializableAttribute) attribute.</span></span> <span data-ttu-id="497c9-110">Jeśli obiekt nie jest, <xref:System.Runtime.Serialization.SerializationException> jest zgłaszany.</span><span class="sxs-lookup"><span data-stu-id="497c9-110">If the object is not, a <xref:System.Runtime.Serialization.SerializationException> is thrown.</span></span>

- <span data-ttu-id="497c9-111">Jeśli obiekt jest odpowiednio oznaczony, sprawdź, czy obiekt implementuje <xref:System.Runtime.Serialization.ISerializable> interfejs.</span><span class="sxs-lookup"><span data-stu-id="497c9-111">If the object is marked appropriately, check whether the object implements the <xref:System.Runtime.Serialization.ISerializable> interface.</span></span> <span data-ttu-id="497c9-112">Jeśli obiekt <xref:System.Runtime.Serialization.ISerializable.GetObjectData%2A> jest wywoływana dla obiektu.</span><span class="sxs-lookup"><span data-stu-id="497c9-112">If the object does, <xref:System.Runtime.Serialization.ISerializable.GetObjectData%2A> is called on the object.</span></span>
  
- <span data-ttu-id="497c9-113">Jeśli obiekt nie jest zaimplementowany <xref:System.Runtime.Serialization.ISerializable> , używane są domyślne zasady serializacji, czyli Serializowanie wszystkich pól, które nie są oznaczone jako [nieserializowane](xref:System.NonSerializedAttribute).</span><span class="sxs-lookup"><span data-stu-id="497c9-113">If the object does not implement <xref:System.Runtime.Serialization.ISerializable>, the default serialization policy is used, serializing all fields not marked as [NonSerialized](xref:System.NonSerializedAttribute).</span></span>

[!INCLUDE [binary-serialization-warning](../../../includes/binary-serialization-warning.md)]
  
## <a name="see-also"></a><span data-ttu-id="497c9-114">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="497c9-114">See also</span></span>

- [<span data-ttu-id="497c9-115">Serializacja binarna</span><span class="sxs-lookup"><span data-stu-id="497c9-115">Binary Serialization</span></span>](binary-serialization.md)
- [<span data-ttu-id="497c9-116">Serializacja XML i SOAP</span><span class="sxs-lookup"><span data-stu-id="497c9-116">XML and SOAP Serialization</span></span>](xml-and-soap-serialization.md)
