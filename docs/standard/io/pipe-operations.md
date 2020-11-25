---
title: Operacje potokowe w programie .NET
description: 'Informacje o operacjach potoku w programie .NET. Potoki zapewniają metodę komunikacji międzyprocesowej. Istnieją dwa rodzaje potoków: anonimowe potoki i nazwane potoki.'
ms.date: 03/30/2017
helpviewer_keywords:
- pipes [.NET]
- pipe operations [.NET]
- interprocess communication [.NET], pipes
- I/O [.NET], pipes
ms.assetid: 7b964ebd-7a4f-4d28-8194-7841f9e4c702
ms.openlocfilehash: bb8804c32b9f2b54b05298779bddae117c10dcf5
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95734806"
---
# <a name="pipe-operations-in-net"></a>Operacje potokowe w programie .NET

Potoki zapewniają metodę komunikacji międzyprocesowej. Istnieją dwa typy potoków:  
  
- Potoki anonimowe.  
  
     Potoki anonimowe zapewniają komunikację międzyprocesową na komputerze lokalnym. Potoki anonimowe wymagają mniej obciążenia niż potoki nazwane, ale oferują ograniczone usługi. Potoki anonimowe są jednokierunkowe i nie mogą być używane w sieci. Obsługują one tylko jedno wystąpienie serwera. Potoki anonimowe są przydatne do komunikacji między wątkami lub między procesami nadrzędnymi i podrzędnymi, w których uchwyty potoku mogą być łatwo przesłane do procesu podrzędnego po jego utworzeniu.  
  
     W programie .NET można zaimplementować anonimowe potoki przy <xref:System.IO.Pipes.AnonymousPipeServerStream> użyciu <xref:System.IO.Pipes.AnonymousPipeClientStream> klas i.  
  
     Zobacz [jak: korzystanie z anonimowych potoków do lokalnej komunikacji międzyprocesowej](how-to-use-anonymous-pipes-for-local-interprocess-communication.md).  
  
- Nazwane potoki.  
  
     Nazwane potoki zapewniają komunikację międzyprocesorową pomiędzy serwerem potoku i jednym lub kilkoma klientami potoku. Nazwane potoki mogą być jednokierunkowe lub dwustronne. Obsługują komunikację opartą na komunikatach i umożliwiają wielu klientom jednoczesne łączenie się z procesem serwera przy użyciu tej samej nazwy potoku. Nazwane potoki obsługują również personifikację, która umożliwia łączenie procesów w celu używania ich własnych uprawnień na serwerach zdalnych.  
  
     W programie .NET należy zaimplementować nazwane potoki przy użyciu <xref:System.IO.Pipes.NamedPipeServerStream> <xref:System.IO.Pipes.NamedPipeClientStream> klas i.  
  
     Zobacz [jak: używanie nazwanych potoków do komunikacji międzyprocesowej sieci](how-to-use-named-pipes-for-network-interprocess-communication.md).  
  
## <a name="see-also"></a>Zobacz także

- [We/wy plików i strumieni](index.md)
- [Instrukcje: Stosowanie anonimowych potoków do lokalnej komunikacji międzyprocesowej](how-to-use-anonymous-pipes-for-local-interprocess-communication.md)
- [Instrukcje: Stosowanie nazwanych potoków do sieciowej komunikacji międzyprocesowej](how-to-use-named-pipes-for-network-interprocess-communication.md)
