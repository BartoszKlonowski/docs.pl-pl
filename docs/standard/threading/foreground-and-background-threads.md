---
title: Wątki pierwszego planu i tła
description: Określ lub Zmień, czy wątek jest wątkiem w tle, czy też wątkiem pierwszego planu przy użyciu właściwości Thread. IsBackground w programie .NET.
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- threading [.NET], foreground
- threading [.NET], background
- foreground threads
- background threads
ms.assetid: cfe0d632-dd35-47e0-91ad-f742a444005e
ms.openlocfilehash: 3b468d2de382719496d5dfaf4c704d43f3e748c3
ms.sourcegitcommit: 7588b1f16b7608bc6833c05f91ae670c22ef56f8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/02/2020
ms.locfileid: "93188071"
---
# <a name="foreground-and-background-threads"></a>Wątki pierwszego planu i tła

Zarządzany wątek jest wątkiem w tle lub wątkiem pierwszego planu. Wątki w tle są takie same jak wątki pierwszego planu z jednym wyjątkiem: wątek w tle nie utrzymuje uruchomionego środowiska wykonywania zarządzanego. Po zatrzymaniu wszystkich wątków pierwszego planu w procesie zarządzanym (gdzie plik exe jest zestawem zarządzanym) system zatrzymuje wszystkie wątki w tle i zamyka.  
  
> [!NOTE]
> Gdy środowisko uruchomieniowe zatrzyma wątek w tle, ponieważ trwa zamykanie procesu, w wątku nie jest zgłaszany żaden wyjątek. Jeśli jednak wątki są zatrzymane, ponieważ <xref:System.AppDomain.Unload%2A?displayProperty=nameWithType> metoda zwalnia domenę aplikacji, <xref:System.Threading.ThreadAbortException> jest zgłaszany zarówno w wątku na pierwszym planie, jak i w tle.  
  
 Użyj <xref:System.Threading.Thread.IsBackground%2A?displayProperty=nameWithType> właściwości, aby określić, czy wątek jest wątkiem w tle, czy na pierwszym planie czy zmienić jego stan. Wątek można w dowolnym momencie zmienić na wątek w tle przez ustawienie jego <xref:System.Threading.Thread.IsBackground%2A> właściwości na `true` .  
  
> [!IMPORTANT]
> Stan pierwszego planu lub tła wątku nie wpływa na wynik nieobsługiwanego wyjątku w wątku. Nieobsłużony wyjątek w wątkach na pierwszym planie lub w tle powoduje zakończenie działania aplikacji. Zobacz [wyjątki w zarządzanych wątkach](exceptions-in-managed-threads.md).  
  
 Wątki należące do puli wątków zarządzanych (czyli wątki, których <xref:System.Threading.Thread.IsThreadPoolThread%2A> Właściwość jest `true` ) są wątkami w tle. Wszystkie wątki, które wprowadzają zarządzane środowisko wykonawcze z kodu niezarządzanego, są oznaczane jako wątki w tle. Wszystkie wątki wygenerowane przez tworzenie i uruchamianie nowego <xref:System.Threading.Thread> obiektu są domyślnie wątki pierwszego planu.  
  
 Jeśli użyjesz wątku do monitorowania działania, takiego jak połączenie gniazda, ustaw jego <xref:System.Threading.Thread.IsBackground%2A> Właściwość na `true` tak, aby wątek nie uniemożliwił przerwania procesu.  
  
## <a name="see-also"></a>Zobacz też

- <xref:System.Threading.Thread.IsBackground%2A?displayProperty=nameWithType>
- <xref:System.Threading.Thread>
- <xref:System.Threading.ThreadAbortException>
