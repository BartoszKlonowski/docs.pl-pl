---
title: 'Ograniczenie: Deserializacja obiektów między domenami aplikacji'
description: Dowiedz się, jak zdiagnozować i wyeliminować problem polegający na tym, że próba deserializacji obiektów w kontekście wywołania logicznego w domenach aplikacji zgłasza wyjątek.
ms.date: 03/30/2017
ms.assetid: 30c2d66c-04a8-41a5-ad31-646b937f61b5
ms.openlocfilehash: 1b8060870962ddd26d90c4152a270a65936c2af3
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96256641"
---
# <a name="mitigation-deserialization-of-objects-across-app-domains"></a>Ograniczenie: Deserializacja obiektów między domenami aplikacji

W niektórych przypadkach, gdy aplikacja używa dwóch lub większej liczby domen aplikacji z różnymi bazami aplikacji, próba deserializacji obiektów w logicznym kontekście wywołań między różnymi domenami aplikacji zgłasza wyjątek.  
  
## <a name="diagnosing-the-issue"></a>Diagnozowanie problemu  

 Problem pojawia się w obszarze następującej sekwencji warunków:  
  
1. Aplikacja używa dwóch lub większej liczby domen aplikacji z różnymi bazami aplikacji.  
  
2. Niektóre typy są jawnie dodawane do <xref:System.Runtime.Remoting.Messaging.LogicalCallContext> przez wywołanie metody takiej jak <xref:System.Runtime.Remoting.Messaging.LogicalCallContext.SetData%2A?displayProperty=nameWithType> lub <xref:System.Runtime.Remoting.Messaging.CallContext.LogicalSetData%2A?displayProperty=nameWithType>. Te typu nie są oznaczane jako możliwe do serializacji i nie są przechowywane w globalnej pamięci podręcznej zestawów.  
  
3. Później, kod uruchomiony w domenie aplikacji innej niż domyślna próbuje odczytać wartość z pliku konfiguracji lub zdeserializować obiekt za pomocą XML.  
  
4. Aby czytać z pliku konfiguracji lub deserializować obiekt, obiekt <xref:System.Xml.XmlReader> próbuje uzyskać dostęp do systemu konfiguracji.  
  
5. Jeśli system konfiguracji nie został jeszcze zainicjowany, musi on zakończyć proces inicjacji. Oznacza to, między innymi, że środowisko wykonawcze musi utworzyć stabilną ścieżkę dla systemu konfiguracji, co wykonuje w następujący sposób:  
  
    1. Szuka dowodu dla domeny aplikacji innej niż domyślna.  
  
    2. Próbuje obliczyć dowód dla domeny aplikacji innej niż domyślna na podstawie domyślnej domeny aplikacji.  
  
    3. Wywołanie w celu uzyskania dowodu dla domyślnej domeny aplikacji wyzwala międzyaplikacyjne wywołanie domeny z domeny aplikacji innej niż domyślna do domyślnej domeny aplikacji.  
  
    4. Zgodnie z częścią kontraktu domeny międzyaplikacyjnej w .NET Framework, zawartość logicznego kontekstu wywołań musiała być skierowana poza granice domeny aplikacji.  
  
6. Ponieważ typy znajdujące się w logicznym kontekście wywołań nie mogą być rozpoznane w domyślnej domenie aplikacji, zgłaszany jest wyjątek.  
  
## <a name="mitigation"></a>Ograniczanie ryzyka  

 Aby obejść ten problem, należy wykonać następujące czynności  
  
1. Poszukaj wywołania `get_Evidence` w stosie wywołań gdy wyjątek jest zgłaszany. Może to być dowolny wyjątek z dużego podzbioru wyjątków, łącznie z <xref:System.IO.FileNotFoundException> i <xref:System.Runtime.Serialization.SerializationException>.  
  
2. Następnie należy znaleźć miejsce w aplikacji, gdzie żadne obiekty nie są dodawane do kontekstu wywołania logicznego i dodać następujący kod:  
  
    ```csharp
    System.Configuration.ConfigurationManager.GetSection("system.xml/xmlReader");  
    ```
  
## <a name="see-also"></a>Zobacz też

- [Zgodność aplikacji](application-compatibility.md)
