---
title: 'Pierwsza instrukcja tego elementu „Sub New” musi być jawnym wywołaniem elementu „MyBase.New” lub „MyClass.New”, ponieważ element „<constructorname>” w klasie bazowej „<baseclassname>” elementu „<derivedclassname>” jest oznaczony jako przestarzały: „<errormessage>"'
ms.date: 07/20/2015
f1_keywords:
- vbc30920
- bc30920
helpviewer_keywords:
- BC30920
ms.assetid: e47dc755-4294-4368-b813-2177b7677957
ms.openlocfilehash: 4b927e3eed8f9d7f46255b907342465f48263724
ms.sourcegitcommit: ff5a4eb5cffbcac9521bc44a907a118cd7e8638d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/17/2020
ms.locfileid: "92163041"
---
# <a name="bc30920-first-statement-of-this-sub-new-must-be-an-explicit-call-to-mybasenew-or-myclassnew-because-the-constructorname-in-the-base-class-baseclassname-of-derivedclassname-is-marked-obsolete-errormessage"></a>BC30920: Pierwsza instrukcja tego elementu "Sub New" musi być jawnym wywołaniem elementu "MyBase. New" lub "MyClass. New", ponieważ element " \<constructorname> " w klasie bazowej "" \<baseclassname> elementu " \<derivedclassname> " jest oznaczony jako przestarzały: " \<errormessage> "

Konstruktor klasy nie wywołuje jawnie konstruktora klasy bazowej, a niejawny Konstruktor klasy bazowej jest oznaczony <xref:System.ObsoleteAttribute> atrybutem i dyrektywą, aby traktować go jako błąd.

 Gdy Konstruktor klasy pochodnej nie wywołuje konstruktora klasy bazowej, Visual Basic próbuje wygenerować niejawnego wywołania konstruktora klasy bazowej bez parametrów. Jeśli w klasie bazowej nie ma dostępnego konstruktora, który można wywołać bez argumentów, Visual Basic nie może wygenerować wywołania niejawnego. W takim przypadku wymagany Konstruktor jest oznaczony <xref:System.ObsoleteAttribute> atrybutem, więc Visual Basic nie może go wywołać.

 Można oznaczyć dowolny element programistyczny jako nieużywany przez zastosowanie <xref:System.ObsoleteAttribute> do niego. W takim przypadku można ustawić <xref:System.ObsoleteAttribute.IsError%2A> właściwość atrybutu na `True` lub `False` . Jeśli ustawisz ją na `True` , kompilator traktuje próbę użycia elementu jako błąd. Jeśli ustawisz ją na `False` lub Zezwól na ustawienie domyślne `False` , kompilator generuje ostrzeżenie w przypadku próby użycia elementu.

 **Identyfikator błędu:** BC30920

## <a name="to-correct-this-error"></a>Aby poprawić ten błąd

1. Przejrzyj cytowany komunikat o błędzie i podejmij odpowiednie działanie.

2. Dołącz wywołanie do `MyBase.New()` lub `MyClass.New()` jako pierwszą instrukcję `Sub New` w klasie pochodnej.

## <a name="see-also"></a>Zobacz też

- [Przegląd atrybutów](../../programming-guide/concepts/attributes/index.md)
