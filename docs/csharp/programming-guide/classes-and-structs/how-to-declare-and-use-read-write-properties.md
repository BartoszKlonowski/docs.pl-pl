---
title: Jak deklarować i używać właściwości odczytu zapisu — Przewodnik programowania w języku C#
description: Dowiedz się, jak używać właściwości odczytu/zapisu w języku C#. Ten przykład obejmuje dwie właściwości, z których każdy ma metody dostępu get i Set, dlatego właściwości są odczytywane i zapisywane.
ms.date: 07/20/2015
helpviewer_keywords:
- get accessor [C#], declaring properties
- set accessor [C#]
- properties [C#], declaring
- read/write properties [C#]
- accessors [C#], declaring properties with
ms.topic: how-to
ms.custom: contperf-fy21q2
ms.assetid: a4962fef-af7e-4c4b-a929-4ae4d646ab8a
ms.openlocfilehash: 824ce8a8cd8f0ef94495a85726331cd6cd024891
ms.sourcegitcommit: d0990c1c1ab2f81908360f47eafa8db9aa165137
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/15/2020
ms.locfileid: "97513015"
---
# <a name="how-to-declare-and-use-read-write-properties-c-programming-guide"></a><span data-ttu-id="25633-104">Jak deklarować i używać właściwości odczytu zapisu (Przewodnik programowania w języku C#)</span><span class="sxs-lookup"><span data-stu-id="25633-104">How to declare and use read write properties (C# Programming Guide)</span></span>

<span data-ttu-id="25633-105">Właściwości zapewniają wygodę publicznych członków danych bez ryzyka związanego z niechronionym, niekontrolowanym i niezweryfikowanym dostępem do danych obiektu.</span><span class="sxs-lookup"><span data-stu-id="25633-105">Properties provide the convenience of public data members without the risks that come with unprotected, uncontrolled, and unverified access to an object's data.</span></span> <span data-ttu-id="25633-106">Jest to realizowane za pośrednictwem metod *dostępu*: specjalne metody, które przypisują i pobierają wartości z bazowego elementu członkowskiego danych.</span><span class="sxs-lookup"><span data-stu-id="25633-106">This is accomplished through *accessors*: special methods that assign and retrieve values from the underlying data member.</span></span> <span data-ttu-id="25633-107">Metoda dostępu [Set](../../language-reference/keywords/set.md) umożliwia składowe danych, a metoda dostępu [Get](../../language-reference/keywords/get.md) pobiera wartości elementu członkowskiego danych.</span><span class="sxs-lookup"><span data-stu-id="25633-107">The [set](../../language-reference/keywords/set.md) accessor enables data members to be assigned, and the [get](../../language-reference/keywords/get.md) accessor retrieves data member values.</span></span>  
  
 <span data-ttu-id="25633-108">Ten przykład pokazuje `Person` klasę, która ma dwie właściwości: `Name` (String) i `Age` (int).</span><span class="sxs-lookup"><span data-stu-id="25633-108">This sample shows a `Person` class that has two properties: `Name` (string) and `Age` (int).</span></span> <span data-ttu-id="25633-109">Obie właściwości zapewniają `get` i metody `set` dostępu, więc są uznawane za właściwości odczytu i zapisu.</span><span class="sxs-lookup"><span data-stu-id="25633-109">Both properties provide `get` and `set` accessors, so they are considered read/write properties.</span></span>  
  
## <a name="example"></a><span data-ttu-id="25633-110">Przykład</span><span class="sxs-lookup"><span data-stu-id="25633-110">Example</span></span>  

 [!code-csharp[csProgGuideObjects#33](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#33)]  
  
## <a name="robust-programming"></a><span data-ttu-id="25633-111">Niezawodne programowanie</span><span class="sxs-lookup"><span data-stu-id="25633-111">Robust Programming</span></span>  

 <span data-ttu-id="25633-112">W poprzednim przykładzie `Name` `Age` właściwości i są [publiczne](../../language-reference/keywords/public.md) i zawierają `get` `set` metodę dostępu a i.</span><span class="sxs-lookup"><span data-stu-id="25633-112">In the previous example, the `Name` and `Age` properties are [public](../../language-reference/keywords/public.md) and include both a `get` and a `set` accessor.</span></span> <span data-ttu-id="25633-113">Dzięki temu każdy obiekt może odczytywać i zapisywać te właściwości.</span><span class="sxs-lookup"><span data-stu-id="25633-113">This allows any object to read and write these properties.</span></span> <span data-ttu-id="25633-114">Jednak czasami pożądane jest wyłączenie jednego z metod dostępu.</span><span class="sxs-lookup"><span data-stu-id="25633-114">It is sometimes desirable, however, to exclude one of the accessors.</span></span> <span data-ttu-id="25633-115">Z pominięciem `set` metody dostępu, na przykład, powoduje, że właściwość jest tylko do odczytu:</span><span class="sxs-lookup"><span data-stu-id="25633-115">Omitting the `set` accessor, for example, makes the property read-only:</span></span>  
  
 [!code-csharp[csProgGuideObjects#87](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#87)]  
  
 <span data-ttu-id="25633-116">Alternatywnie można uwidocznić jeden akcesor publicznie, ale drugi prywatny lub chroniony.</span><span class="sxs-lookup"><span data-stu-id="25633-116">Alternatively, you can expose one accessor publicly but make the other private or protected.</span></span> <span data-ttu-id="25633-117">Aby uzyskać więcej informacji, zobacz [ułatwienia dostępu asymetryczny](./restricting-accessor-accessibility.md).</span><span class="sxs-lookup"><span data-stu-id="25633-117">For more information, see [Asymmetric Accessor Accessibility](./restricting-accessor-accessibility.md).</span></span>  
  
 <span data-ttu-id="25633-118">Po zadeklarowaniu właściwości można ich używać tak, jakby były polami klasy.</span><span class="sxs-lookup"><span data-stu-id="25633-118">Once the properties are declared, they can be used as if they were fields of the class.</span></span> <span data-ttu-id="25633-119">Pozwala to na bardzo naturalną składnię podczas pobierania i ustawiania wartości właściwości, jak w następujących instrukcjach:</span><span class="sxs-lookup"><span data-stu-id="25633-119">This allows for a very natural syntax when both getting and setting the value of a property, as in the following statements:</span></span>  
  
 [!code-csharp[csProgGuideObjects#35](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#35)]  
  
 <span data-ttu-id="25633-120">Należy pamiętać, że w `set` metodzie właściwości `value` jest dostępna specjalna zmienna.</span><span class="sxs-lookup"><span data-stu-id="25633-120">Note that in a property `set` method a special `value` variable is available.</span></span> <span data-ttu-id="25633-121">Ta zmienna zawiera wartość określoną przez użytkownika, na przykład:</span><span class="sxs-lookup"><span data-stu-id="25633-121">This variable contains the value that the user specified, for example:</span></span>  
  
 [!code-csharp[csProgGuideObjects#36](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#36)]  
  
 <span data-ttu-id="25633-122">Zwróć uwagę na czystą składnię zwiększającą `Age` Właściwość `Person` obiektu:</span><span class="sxs-lookup"><span data-stu-id="25633-122">Notice the clean syntax for incrementing the `Age` property on a `Person` object:</span></span>  
  
 [!code-csharp[csProgGuideObjects#37](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#37)]  
  
 <span data-ttu-id="25633-123">Jeśli `set` `get` do właściwości modelu użyto oddzielnych metod i, odpowiedni kod może wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="25633-123">If separate `set` and `get` methods were used to model properties, the equivalent code might look like this:</span></span>  
  
```csharp  
person.SetAge(person.GetAge() + 1);
```  
  
 <span data-ttu-id="25633-124">`ToString`Metoda została przesłonięta w tym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="25633-124">The `ToString` method is overridden in this example:</span></span>  
  
 [!code-csharp[csProgGuideObjects#38](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#38)]  
  
 <span data-ttu-id="25633-125">Należy zauważyć, że `ToString` nie jest on jawnie używany w programie.</span><span class="sxs-lookup"><span data-stu-id="25633-125">Notice that `ToString` is not explicitly used in the program.</span></span> <span data-ttu-id="25633-126">Jest wywoływana domyślnie przez `WriteLine` wywołania.</span><span class="sxs-lookup"><span data-stu-id="25633-126">It is invoked by default by the `WriteLine` calls.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="25633-127">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="25633-127">See also</span></span>

- [<span data-ttu-id="25633-128">Przewodnik programowania w języku C#</span><span class="sxs-lookup"><span data-stu-id="25633-128">C# Programming Guide</span></span>](../index.md)
- [<span data-ttu-id="25633-129">Właściwości</span><span class="sxs-lookup"><span data-stu-id="25633-129">Properties</span></span>](./properties.md)
- [<span data-ttu-id="25633-130">Klasy i struktury</span><span class="sxs-lookup"><span data-stu-id="25633-130">Classes and Structs</span></span>](./index.md)
