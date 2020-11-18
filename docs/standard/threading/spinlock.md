---
title: SpinLock
ms.date: 03/30/2017
helpviewer_keywords:
- synchronization primitives, SpinLock
ms.assetid: f9af93bb-7a0d-4ba5-afe8-74f48b6b6958
ms.openlocfilehash: 071bde6e8b32d5712256e24c83d713cd63f2bffb
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/18/2020
ms.locfileid: "94819009"
---
# <a name="spinlock"></a>SpinLock
<xref:System.Threading.SpinLock>Struktura jest podstawową synchronizacją typu niskiego poziomu, która jest kręgosłupem, który obraca się podczas oczekiwania na uzyskanie blokady. Na komputerach z procesorem wielordzeniowym, gdy czasy oczekiwania są krótkie i gdy rywalizacja jest minimalna, <xref:System.Threading.SpinLock> może działać lepiej niż w przypadku innych rodzajów blokad. Zaleca się jednak użycie <xref:System.Threading.SpinLock> tylko w przypadku określenia przez profilowanie, że <xref:System.Threading.Monitor?displayProperty=nameWithType> Metoda lub <xref:System.Threading.Interlocked> metody znacząco spowalniają wydajność programu.  
  
 <xref:System.Threading.SpinLock> może spowodować wycinek czasu wątku, nawet jeśli nie uzyskał jeszcze blokady. Ma to na celu uniknięcie niedziałania priorytetu wątku oraz umożliwienie wyrzucania elementów bezużytecznych. W przypadku korzystania z programu <xref:System.Threading.SpinLock> należy się upewnić, że żaden wątek nie może obsłużyć blokady przez więcej niż bardzo krótki zakres czasu i że żaden wątek nie może blokować blokady.  
  
 Ponieważ struktury SpinLock jest typem wartości, należy jawnie przekazać go przez odwołanie, jeśli chcesz, aby te dwie kopie odwołują się do tej samej blokady.  
  
 Więcej informacji o sposobach korzystania z tego typu znajduje się w temacie <xref:System.Threading.SpinLock?displayProperty=nameWithType> . Aby zapoznać się z przykładem, zobacz [How to: use struktury spinlock for Low-Level Synchronization](how-to-use-spinlock-for-low-level-synchronization.md).  
  
 <xref:System.Threading.SpinLock>obsługuje tryb *thread* - *śledzenia* wątków, którego można użyć w fazie tworzenia, aby ułatwić śledzenie wątku utrzymującego blokadę w określonym czasie. Tryb śledzenia wątków jest bardzo przydatny do debugowania, ale zalecamy wyłączenie go w wydanej wersji programu, ponieważ może to spowodować spadek wydajności. Aby uzyskać więcej informacji, zobacz [How to: Enable Thread-Tracking Mode in in struktury spinlock](how-to-enable-thread-tracking-mode-in-spinlock.md).  
  
## <a name="see-also"></a>Zobacz także

- [Wątkowość obiektów i funkcji](threading-objects-and-features.md)
