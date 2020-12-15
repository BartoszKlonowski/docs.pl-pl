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
# <a name="how-to-declare-and-use-read-write-properties-c-programming-guide"></a>Jak deklarować i używać właściwości odczytu zapisu (Przewodnik programowania w języku C#)

Właściwości zapewniają wygodę publicznych członków danych bez ryzyka związanego z niechronionym, niekontrolowanym i niezweryfikowanym dostępem do danych obiektu. Jest to realizowane za pośrednictwem metod *dostępu*: specjalne metody, które przypisują i pobierają wartości z bazowego elementu członkowskiego danych. Metoda dostępu [Set](../../language-reference/keywords/set.md) umożliwia składowe danych, a metoda dostępu [Get](../../language-reference/keywords/get.md) pobiera wartości elementu członkowskiego danych.  
  
 Ten przykład pokazuje `Person` klasę, która ma dwie właściwości: `Name` (String) i `Age` (int). Obie właściwości zapewniają `get` i metody `set` dostępu, więc są uznawane za właściwości odczytu i zapisu.  
  
## <a name="example"></a>Przykład  

 [!code-csharp[csProgGuideObjects#33](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#33)]  
  
## <a name="robust-programming"></a>Niezawodne programowanie  

 W poprzednim przykładzie `Name` `Age` właściwości i są [publiczne](../../language-reference/keywords/public.md) i zawierają `get` `set` metodę dostępu a i. Dzięki temu każdy obiekt może odczytywać i zapisywać te właściwości. Jednak czasami pożądane jest wyłączenie jednego z metod dostępu. Z pominięciem `set` metody dostępu, na przykład, powoduje, że właściwość jest tylko do odczytu:  
  
 [!code-csharp[csProgGuideObjects#87](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#87)]  
  
 Alternatywnie można uwidocznić jeden akcesor publicznie, ale drugi prywatny lub chroniony. Aby uzyskać więcej informacji, zobacz [ułatwienia dostępu asymetryczny](./restricting-accessor-accessibility.md).  
  
 Po zadeklarowaniu właściwości można ich używać tak, jakby były polami klasy. Pozwala to na bardzo naturalną składnię podczas pobierania i ustawiania wartości właściwości, jak w następujących instrukcjach:  
  
 [!code-csharp[csProgGuideObjects#35](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#35)]  
  
 Należy pamiętać, że w `set` metodzie właściwości `value` jest dostępna specjalna zmienna. Ta zmienna zawiera wartość określoną przez użytkownika, na przykład:  
  
 [!code-csharp[csProgGuideObjects#36](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#36)]  
  
 Zwróć uwagę na czystą składnię zwiększającą `Age` Właściwość `Person` obiektu:  
  
 [!code-csharp[csProgGuideObjects#37](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#37)]  
  
 Jeśli `set` `get` do właściwości modelu użyto oddzielnych metod i, odpowiedni kod może wyglądać następująco:  
  
```csharp  
person.SetAge(person.GetAge() + 1);
```  
  
 `ToString`Metoda została przesłonięta w tym przykładzie:  
  
 [!code-csharp[csProgGuideObjects#38](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#38)]  
  
 Należy zauważyć, że `ToString` nie jest on jawnie używany w programie. Jest wywoływana domyślnie przez `WriteLine` wywołania.  
  
## <a name="see-also"></a>Zobacz też

- [Przewodnik programowania w języku C#](../index.md)
- [Właściwości](./properties.md)
- [Klasy i struktury](./index.md)
