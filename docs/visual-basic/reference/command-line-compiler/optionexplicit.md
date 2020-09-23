---
title: -optionexplicit
ms.date: 07/20/2015
f1_keywords:
- /optionexplicit
- -optionexplicit
helpviewer_keywords:
- /optionexplicit compiler option [Visual Basic]
- optionexplicit compiler option [Visual Basic]
- -optionexplicit compiler option [Visual Basic]
ms.assetid: 5d296ab3-bafe-4c4d-9887-78f162ed86c7
ms.openlocfilehash: 65cc3fb1b2fa9daa04013caa2b93a3949d0a15b9
ms.sourcegitcommit: bf5c5850654187705bc94cc40ebfb62fe346ab02
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/23/2020
ms.locfileid: "91098939"
---
# <a name="-optionexplicit"></a>-optionexplicit

Powoduje, że kompilator zgłasza błędy, jeśli zmienne nie są deklarowane przed ich użyciem.  
  
## <a name="syntax"></a>Składnia  
  
```console  
-optionexplicit[+ | -]  
```  
  
## <a name="arguments"></a>Argumenty  

 `+` &#124; `-`  
 Opcjonalny. Określ `-optionexplicit+` , aby wymagać jawnej deklaracji zmiennych. `-optionexplicit+`Opcja jest wartością domyślną i jest taka sama jak `-optionexplicit` . `-optionexplicit-`Opcja włącza niejawną deklarację zmiennych.  
  
## <a name="remarks"></a>Uwagi  

 Jeśli plik kodu źródłowego zawiera [instrukcję Option Explicit](../../language-reference/statements/option-explicit-statement.md), instrukcja zastępuje `-optionexplicit` ustawienie kompilatora wiersza polecenia.  
  
### <a name="to-set--optionexplicit-in-the-visual-studio-ide"></a>Aby ustawić-optionexplicit w środowisku IDE programu Visual Studio  
  
1. Zaznaczono projekt w **Eksplorator rozwiązań**. W menu **projekt** kliknij polecenie **Właściwości**.
  
2. Kliknij kartę **kompilacja** .  
  
3. Zmodyfikuj wartość w polu **opcja Explicit** .  
  
## <a name="example"></a>Przykład  

 Poniższy kod kompiluje, kiedy `-optionexplicit-` jest używany.  
  
 [!code-vb[VbVbalrCompiler#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrCompiler/VB/OptionExplicitOff.vb#5)]  
  
## <a name="see-also"></a>Zobacz także

- [Kompilator wiersza polecenia Visual Basic](index.md)
- [-optioncompare](optioncompare.md)
- [-optionstrict](optionstrict.md)
- [-optioninfer](optioninfer.md)
- [Przykłady kompilacji — wiersze poleceń](sample-compilation-command-lines.md)
- [Option Explicit, instrukcja](../../language-reference/statements/option-explicit-statement.md)
- [Domyślne ustawienia programu Visual Basic, Projekty, Opcje — okno dialogowe](/visualstudio/ide/reference/visual-basic-defaults-projects-options-dialog-box)
