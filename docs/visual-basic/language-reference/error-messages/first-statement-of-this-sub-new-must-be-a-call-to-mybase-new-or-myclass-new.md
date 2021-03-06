---
title: Pierwsza instrukcja tego elementu „Sub New” musi być wywołaniem do „MyBase.New” lub „MyClass.New” (Nie jest dostępny żaden konstruktor bez parametrów)
ms.date: 07/20/2015
f1_keywords:
- bc30148
- vbc30148
helpviewer_keywords:
- BC30148
ms.assetid: 4426e8fc-cb39-4eb8-ba95-503cd32fcc89
ms.openlocfilehash: bce8ad10bc201386f34d6623741c7d41a5dec27e
ms.sourcegitcommit: ff5a4eb5cffbcac9521bc44a907a118cd7e8638d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/17/2020
ms.locfileid: "92163028"
---
# <a name="bc30148-first-statement-of-this-sub-new-must-be-a-call-to-mybasenew-or-myclassnew-no-accessible-constructor-without-parameters"></a>BC30148: Pierwsza instrukcja tego elementu "Sub New" musi być wywołaniem elementu "MyBase. New" lub "MyClass. New" (Brak dostępnego konstruktora bez parametrów)

Pierwsza instrukcja tego elementu "Sub New" musi być wywołaniem elementu "MyBase. New" lub "MyClass. New", ponieważ klasa bazowa " \<basename> " z " \<derivedname> " nie ma dostępnego elementu "Sub New", który można wywołać bez argumentów.

 W klasie pochodnej każdy Konstruktor musi wywołać konstruktora klasy bazowej ( `MyBase.New` ). Jeśli klasa bazowa ma konstruktora bez parametrów, które są dostępne dla klas pochodnych, `MyBase.New` może być wywoływana automatycznie. Jeśli nie, Konstruktor klasy bazowej musi być wywołany z parametrami i nie można wykonać tej operacji automatycznie. W takim przypadku pierwsza instrukcja każdego pochodnego konstruktora klasy musi wywołać sparametryzowany Konstruktor w klasie bazowej lub wywołać innego konstruktora w klasie pochodnej, która tworzy wywołanie konstruktora klasy bazowej.

 **Identyfikator błędu:** BC30148

## <a name="to-correct-this-error"></a>Aby poprawić ten błąd

- Wywołanie `MyBase.New` podawania wymaganych parametrów lub wywołanie konstruktora równorzędnego, który wykonuje takie wywołanie.

     Na przykład jeśli klasa bazowa ma Konstruktor, który jest zadeklarowany jako `Public Sub New(ByVal index as Integer)` , pierwsza instrukcja w konstruktorze klasy pochodnej może być `MyBase.New(100)` .

## <a name="see-also"></a>Zobacz też

- [Podstawowe informacje o dziedziczeniu](../../programming-guide/language-features/objects-and-classes/inheritance-basics.md)
