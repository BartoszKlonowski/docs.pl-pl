---
title: Wymagane odwołanie do zestawu „<assemblyidentity>” z typem „<typename>”, ale nie można odnaleźć pasującego odwołania z powodu niejednoznaczności między projektami „<projectname1>” i „<projectname2>”.
ms.date: 07/20/2015
f1_keywords:
- bc30969
- vbc30969
helpviewer_keywords:
- BC30969
ms.assetid: 1b29dbc5-8268-45fe-bfc2-b2070a5c845c
ms.openlocfilehash: ffc6b3c180c86abe272d56d0ecf3042d8181da59
ms.sourcegitcommit: d2db216e46323f73b32ae312c9e4135258e5d68e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/22/2020
ms.locfileid: "90870898"
---
# <a name="reference-required-to-assembly-assemblyidentity-containing-type-typename-but-a-suitable-reference-could-not-be-found-due-to-ambiguity-between-projects-projectname1-and-projectname2"></a>Wymagane odwołanie do zestawu „\<assemblyidentity>” z typem „\<typename>”, ale nie można odnaleźć pasującego odwołania z powodu niejednoznaczności między projektami „\<projectname1>” i „\<projectname2>”.

Wyrażenie używa typu, takiego jak Klasa, struktura, interfejs, Wyliczenie lub delegat, który jest zdefiniowany poza projektem. Istnieją jednak odwołania do projektu do więcej niż jednego zestawu definiującego ten typ.  
  
 Projekty cytowane tworzą zestawy o tej samej nazwie. W związku z tym kompilator nie może określić, który zestaw ma być używany dla typu, do którego uzyskujesz dostęp.  
  
 Aby uzyskać dostęp do typu zdefiniowanego w innym zestawie, kompilator Visual Basic musi mieć odwołanie do tego zestawu. Musi to być jedno, niejednoznaczne odwołanie, które nie powoduje cyklicznych odwołań między projektami.  
  
 **Identyfikator błędu:** BC30969  
  
## <a name="to-correct-this-error"></a>Aby poprawić ten błąd  
  
1. Ustal, który projekt tworzy najlepszy zestaw dla projektu do odwołania. W przypadku tej decyzji można użyć kryteriów, takich jak łatwość dostępu do plików i częstotliwość aktualizacji.  
  
2. We właściwościach projektu Dodaj odwołanie do pliku zawierającego zestaw, który definiuje używany typ.  
  
## <a name="see-also"></a>Zobacz też

- [Zarządzanie odwołaniami w projekcie](/visualstudio/ide/managing-references-in-a-project)
- [Odwołania do elementów zadeklarowanych](../../programming-guide/language-features/declared-elements/references-to-declared-elements.md)

- [Zarządzanie właściwościami projektów i rozwiązań](/visualstudio/ide/managing-project-and-solution-properties)
- [Rozwiązywanie problemów z przerwanymi odwołaniami](/visualstudio/ide/troubleshooting-broken-references)
