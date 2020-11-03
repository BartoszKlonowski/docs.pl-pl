---
title: Koncepcje z zakresu serializacji
description: Serializacja może służyć do przechwytywania stanu obiektu, aby można było utworzyć kopię lub wysłać obiekt przez wartość z jednej domeny aplikacji do innej.
ms.date: 08/07/2017
ms.assetid: e1ff4740-20a1-4c76-a8ad-d857db307054
ms.openlocfilehash: dcaa3fa0d9080c958e63a3ae9d1e8f951ea1f70b
ms.sourcegitcommit: 74d05613d6c57106f83f82ce8ee71176874ea3f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/03/2020
ms.locfileid: "93282302"
---
# <a name="serialization-concepts"></a>Koncepcje z zakresu serializacji
Dlaczego czy chcesz użyć serializacji? Dwa najważniejsze powody to utrwalanie stanu obiektu na nośniku magazynu, dzięki czemu można ponownie utworzyć dokładną kopię na późniejszym etapie i wysłać obiekt przez wartość z jednej domeny aplikacji do innej. Na przykład Serializacja służy do zapisywania stanu sesji w ASP.NET i kopiowania obiektów do Schowka w Windows Forms. Jest on również używany przez funkcję komunikacji zdalnej do przekazywania obiektów według wartości z jednej domeny aplikacji do innej.

[!INCLUDE [binary-serialization-warning](../../../includes/binary-serialization-warning.md)]

## <a name="persistent-storage"></a>Magazyn trwały
Często jest to niezbędne do przechowywania wartości pól obiektu na dysku, a następnie później, pobrania tych danych. Chociaż jest to łatwe do osiągnięcia bez polegania na serializacji, to podejście jest często kłopotliwe i podatne na błędy i jest stopniowo bardziej skomplikowane, gdy trzeba śledzić hierarchię obiektów. Załóżmy, że pisząc duże aplikacje biznesowe, które zawierają tysiące obiektów, i trzeba napisać kod, aby zapisać i przywrócić pola i właściwości do i z dysku dla każdego obiektu. Serializacja oferuje wygodny mechanizm do osiągnięcia tego celu.

Środowisko uruchomieniowe języka wspólnego zarządza sposobem przechowywania obiektów w pamięci i zapewnia automatyczny mechanizm serializacji przy użyciu [odbicia](../../framework/reflection-and-codedom/reflection.md). Gdy obiekt jest serializowany, nazwa klasy, zestaw i wszystkie składowe danych wystąpienia klasy są zapisywane w pamięci masowej. Obiekty przechowywania często odwołuje się do innych wystąpień w zmiennych elementu członkowskiego. Klasa jest serializowana, mechanizm serializacji śledzi występujących w odwołaniu dla obiektów, już, aby upewnić się, że ten sam obiekt nie jest serializowana więcej niż raz. Architektura serializacji udostępniana przez platformę .NET poprawnie obsługuje wykresy obiektów i odwołania cykliczne. Jedynym wymaganiem umieszczonym na wykresach obiektów jest to, że wszystkie obiekty, do których odwołuje się serializowany obiekt, również muszą być oznaczone jako `Serializable` (Aby uzyskać więcej informacji, zobacz [Serializacja podstawowa](basic-serialization.md)). Jeśli nie jest to wykonywane, zostanie zwrócony wyjątek serializator próba serializacji obiektu nieoznaczone.

Po deserializacji klasy serializowanej Klasa jest tworzona, a wartości wszystkich elementów członkowskich danych są przywracane automatycznie.

## <a name="marshal-by-value"></a>Organizowanie według wartości
Obiekty są prawidłowe tylko w domenie aplikacji, w której zostały utworzone. Każda próba przekazania obiektu jako parametru lub zwrócenia go w wyniku zakończy się niepowodzeniem, chyba że obiekt pochodzi z `MarshalByRefObject` lub jest oznaczony jako `Serializable` . Jeśli obiekt jest oznaczony jako `Serializable` , obiekt zostanie automatycznie Zserializowany, transportowany z jednej domeny aplikacji do drugiego, a następnie deserializowany, aby utworzyć dokładną kopię obiektu w drugiej domenie aplikacji. Ten proces jest zwykle określany jako marshal przez wartość.

Gdy obiekt pochodzi z `MarshalByRefObject` , odwołanie do obiektu jest przesyłane z jednej domeny aplikacji do innej, a nie do samego obiektu. Możesz również oznaczyć obiekt, który pochodzi od `MarshalByRefObject` `Serializable` . Gdy ten obiekt jest używany z usługami zdalnymi, program formatujący odpowiedzialny za serializacji, który został wstępnie skonfigurowany przy użyciu selektora zastępcy ( `SurrogateSelector` ), przejmuje kontrolę nad procesem serializacji i zastępuje wszystkie obiekty pochodne z `MarshalByRefObject` serwerem proxy. Bez użycia `SurrogateSelector` Architektura serializacji jest zgodna ze standardowymi regułami serializacji opisanymi w [krokach procesu serializacji](steps-in-the-serialization-process.md).  

## <a name="related-sections"></a>Sekcje pokrewne  
 [Serializacja binarna](binary-serialization.md)  
 Opisuje mechanizm serializacji binarnej, który jest dołączony do aparatu PLików wykonywalnych języka wspólnego.
  
 [Serializacja XML i SOAP](xml-and-soap-serialization.md)  
 Opisuje mechanizm serializacji XML i protokołu SOAP, który jest dołączony do aparatu PLików wykonywalnych języka wspólnego.
