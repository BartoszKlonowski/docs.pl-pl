---
title: Nie można wywnioskować argumentów typu na podstawie obiektu delegowanego
ms.date: 07/20/2015
f1_keywords:
- bc36564
- vbc36564
helpviewer_keywords:
- BC36564
ms.assetid: 21312807-e1cd-4ac1-ae1c-c28a9c25164d
ms.openlocfilehash: f7937a34ab425da684f892250884d21e020e4c57
ms.sourcegitcommit: ff5a4eb5cffbcac9521bc44a907a118cd7e8638d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/17/2020
ms.locfileid: "92161247"
---
# <a name="bc36564-type-arguments-could-not-be-inferred-from-the-delegate"></a>BC36564: nie można wywnioskować argumentów typu na podstawie delegata

Instrukcja przypisania używa `AddressOf` do przypisywania adresu procedury ogólnej do delegata, ale nie dostarcza żadnych argumentów typu do procedury ogólnej.

 Zwykle podczas wywoływania typu ogólnego należy podać argument typu dla każdego parametru typu, który definiuje typ ogólny. Jeśli nie podasz żadnych argumentów typu, kompilator próbuje wywnioskować typy do przekazania do parametrów typu. Jeśli kontekst nie zapewnia wystarczającej ilości informacji do wywnioskowania typów przez kompilator, generowany jest błąd.

 **Identyfikator błędu:** BC36564

## <a name="to-correct-this-error"></a>Aby poprawić ten błąd

- Określ argumenty typu dla procedury ogólnej w `AddressOf` wyrażeniu.

## <a name="see-also"></a>Zobacz też

- [Typy ogólne w Visual Basic](../../programming-guide/language-features/data-types/generic-types.md)
- [AddressOf, operator](../operators/addressof-operator.md)
- [Procedury ogólne w Visual Basic](../../programming-guide/language-features/data-types/generic-procedures.md)
- [Lista typów](../statements/type-list.md)
- [Metody rozszerzające](../../programming-guide/language-features/procedures/extension-methods.md)
