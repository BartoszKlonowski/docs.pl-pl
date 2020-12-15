---
title: Używanie obsługi wyjątków filtrowanej przez użytkownika
description: Dowiedz się, jak korzystać z obsługi wyjątków filtrowanych przez użytkownika w językach C# i Visual Basic.
ms.date: 12/14/2020
helpviewer_keywords:
- user-filtered exceptions
- exceptions, user-filtered
dev_langs:
- csharp
- vb
ms.openlocfilehash: 2dba43ad2fc685a6555ab43fc973814fd7f359a3
ms.sourcegitcommit: d0990c1c1ab2f81908360f47eafa8db9aa165137
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/15/2020
ms.locfileid: "97512674"
---
# <a name="use-user-filtered-exception-handlers"></a>Używanie obsługi wyjątków filtrowanej przez użytkownika

Programy obsługi wyjątków filtrowane przez użytkownika przechwytują i obsługują wyjątki na podstawie wymagań zdefiniowanych dla wyjątku. Te programy obsługi wykorzystują `catch` instrukcję ze `when` słowem kluczowym ( `Catch` i `When` w Visual Basic).  
  
 Ta technika jest przydatna, gdy określony obiekt wyjątku odnosi się do wielu błędów. W takim przypadku obiekt ma zazwyczaj właściwość, która zawiera konkretny kod błędu skojarzony z błędem. Możesz użyć właściwości kod błędu w wyrażeniu, aby wybrać tylko konkretny błąd, który ma być obsługiwany w tej `catch` klauzuli.  
  
 Poniższy przykład ilustruje `catch` / `when` instrukcję.

```csharp
try
{
    //Try statements.  
}
catch (Exception ex) when (ex.Message.Contains("404"))
{
    //Catch statements.
}
```  
  
```vb
Try  
    'Try statements.  
    Catch When Err = VBErr_ClassLoadException
    'Catch statements.
End Try  
```  
  
 Wyrażenie filtrowanej przez użytkownika klauzuli nie jest w żaden sposób ograniczone. Jeśli wystąpi wyjątek podczas wykonywania wyrażenia filtrowanego przez użytkownika, ten wyjątek zostanie odrzucony i wyrażenie filtru jest uważane za szacowane na wartość false. W takim przypadku środowisko uruchomieniowe języka wspólnego kontynuuje wyszukiwanie programu obsługi dla bieżącego wyjątku.  
  
## <a name="combine-the-specific-exception-and-the-user-filtered-clauses"></a>Połącz określony wyjątek i klauzule filtrowane przez użytkownika  

 `catch`Instrukcja może zawierać zarówno konkretny wyjątek, jak i filtrowane przez użytkownika klauzule. Środowisko uruchomieniowe najpierw sprawdza konkretny wyjątek. Jeśli konkretny wyjątek się powiedzie, środowisko uruchomieniowe wykonuje filtr użytkownika. Filtr generyczny może zawierać odwołanie do zmiennej zadeklarowanej w filtrze klas. Należy zauważyć, że nie można odwrócić kolejności dwóch klauzul filtru.  
  
 Poniższy przykład pokazuje konkretny wyjątek w instrukcji **catch** , a także klauzulę filtrowana przez użytkownika przy użyciu słowa kluczowego **when** .  
  
```csharp
try
{
    //Try statements.  
}
catch (System.Net.Http.HttpRequestException ex) when (ex.Message.Contains("404"))
{
    //Catch statements.
}
```  
  
```vb
Try  
    'Try statements.
    Catch cle As ClassLoadException When cle.IsRecoverable()  
    'Catch statements.
End Try  
```  

## <a name="see-also"></a>Zobacz też

- [Wyjątki](index.md)
