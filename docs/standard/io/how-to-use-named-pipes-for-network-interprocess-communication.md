---
title: 'Instrukcje: Stosowanie nazwanych potoków do sieciowej komunikacji międzyprocesowej'
description: Zobacz dwa przykłady użycia nazwanych potoków do komunikacji międzyprocesowej między serwerem potoku i jednym lub większą liczbą klientów potoku w sieci.
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- message-based communication [.NET], named pipes
- named pipes [.NET]
- pipes [.NET]
- multiple connections via named pipes
- network communications [.NET], named pipes
- impersonation [.NET], named pipes
- full duplex communication [.NET], named pipes
ms.assetid: 4e4d7e64-9f1b-4026-98f7-20488ac7b42b
ms.openlocfilehash: 8657597bee5855061bb5529d80d2fa5f0318e817
ms.sourcegitcommit: 7588b1f16b7608bc6833c05f91ae670c22ef56f8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/02/2020
ms.locfileid: "93189319"
---
# <a name="how-to-use-named-pipes-for-network-interprocess-communication"></a>Instrukcje: Stosowanie nazwanych potoków do sieciowej komunikacji międzyprocesowej

Nazwane potoki zapewniają komunikację międzyprocesorową pomiędzy serwerem potoku i jednym lub kilkoma klientami potoku. Oferują one więcej funkcji niż potoki anonimowe, które zapewniają komunikację międzyprocesorową na komputerze lokalnym. Nazwane potoki obsługują komunikację pełnodupleksową przez sieć i wiele instancji serwera, komunikację opartą na komunikatach i personifikację klienta, co pozwala łączyć procesy z ich własnymi zestawami uprawnień na serwerach zdalnych.  
  
 Aby zaimplementować nazwane potoki, należy użyć klas <xref:System.IO.Pipes.NamedPipeServerStream> i <xref:System.IO.Pipes.NamedPipeClientStream>.  
  
## <a name="example"></a>Przykład  
 W poniższym przykładzie pokazano jak utworzyć nazwany potok używając klasy <xref:System.IO.Pipes.NamedPipeServerStream>. W tym przykładzie proces serwera tworzy cztery wątki. Każdy wątek może zaakceptować połączenie klienta. Następnie połączony proces klienta dostarcza do serwera nazwę pliku. Jeśli klient ma wystarczające uprawnienia, proces serwera otwiera plik i wysyła jego zawartość z powrotem do klienta.  
  
 [!code-cpp[System.IO.Pipes.NamedPipeServerStream_ImpersonationSample1#01](../../../samples/snippets/cpp/VS_Snippets_CLR_System/system.IO.Pipes.NamedPipeServerStream_ImpersonationSample1/cpp/program.cpp#01)]
 [!code-csharp[System.IO.Pipes.NamedPipeServerStream_ImpersonationSample1#01](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.IO.Pipes.NamedPipeServerStream_ImpersonationSample1/cs/Program.cs#01)]
 [!code-vb[System.IO.Pipes.NamedPipeServerStream_ImpersonationSample1#01](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.IO.Pipes.NamedPipeServerStream_ImpersonationSample1/vb/program.vb#01)]  
  
## <a name="example"></a>Przykład  
 W poniższym przykładzie pokazano proces klienta, który korzysta z klasy <xref:System.IO.Pipes.NamedPipeClientStream>. Klient łączy się z procesem serwera i wysyła nazwę pliku do serwera. W przykładzie użyto personifikacji, więc tożsamość, która uruchamia aplikację klienta, musi mieć uprawnienia dostępu do tego pliku. Serwer wysyła następnie zawartość pliku z powrotem do klienta. Zawartość pliku jest następnie wyświetlana w konsoli.  
  
 [!code-csharp[System.IO.Pipes.NamedPipeClientStream_ImpersonationSample1#01](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.IO.Pipes.NamedPipeClientStream_ImpersonationSample1/cs/Program.cs#01)]
 [!code-vb[System.IO.Pipes.NamedPipeClientStream_ImpersonationSample1#01](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.IO.Pipes.NamedPipeClientStream_ImpersonationSample1/vb/program.vb#01)]  
  
## <a name="robust-programming"></a>Niezawodne programowanie  
 Procesy klienta i serwera w tym przykładzie są przeznaczone do uruchomienia na tym samym komputerze, więc nazwa serwera dostarczona do obiektu <xref:System.IO.Pipes.NamedPipeClientStream> to `"."`. Jeśli procesy klienta i serwera znajdują się na oddzielnych komputerach, `"."` zostanie zamienione na nazwę sieciową komputera, który uruchamia proces serwera.  
  
## <a name="see-also"></a>Zobacz też

- <xref:System.Security.Principal.TokenImpersonationLevel>
- <xref:System.IO.Pipes.NamedPipeServerStream.GetImpersonationUserName%2A>
- [Potoki](pipe-operations.md)
- [Instrukcje: Stosowanie anonimowych potoków do lokalnej komunikacji międzyprocesowej](how-to-use-anonymous-pipes-for-local-interprocess-communication.md)
