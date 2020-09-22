---
title: Element „<eventname>” jest zdarzeniem i nie można go wywołać bezpośrednio
ms.date: 07/20/2015
f1_keywords:
- bc32022
- vbc32022
helpviewer_keywords:
- BC32022
ms.assetid: 4dcfcb8d-a9fa-46a7-a034-29d9ff3a59b3
ms.openlocfilehash: 3366bc215a45cd7de9dc2de285758a78144df509
ms.sourcegitcommit: d2db216e46323f73b32ae312c9e4135258e5d68e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/22/2020
ms.locfileid: "90874312"
---
# <a name="eventname-is-an-event-and-cannot-be-called-directly"></a>Element „\<eventname>” jest zdarzeniem i nie można go wywołać bezpośrednio

"<`eventname`>" jest zdarzeniem i dlatego nie można go wywołać bezpośrednio. Użyj `RaiseEvent` instrukcji, aby zgłosić zdarzenie.  
  
 Wywołanie procedury określa zdarzenie dla nazwy procedury. Procedura obsługi zdarzeń jest procedurą, ale samo zdarzenie jest urządzeniem sygnalizującym, które musi zostać podniesione i obsłużone.  
  
 **Identyfikator błędu:** BC32022  
  
## <a name="to-correct-this-error"></a>Aby poprawić ten błąd  
  
1. Użyj `RaiseEvent` instrukcji, aby sygnalizować zdarzenie i wywołać procedury lub procedury, które je obsługują.  
  
## <a name="see-also"></a>Zobacz też

- [RaiseEvent — Instrukcja](../statements/raiseevent-statement.md)
