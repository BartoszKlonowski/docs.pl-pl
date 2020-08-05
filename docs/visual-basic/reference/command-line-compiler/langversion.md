---
title: -langversion
ms.date: 03/10/2018
helpviewer_keywords:
- /langversion compiler option [Visual Basic]
- langversion compiler option [Visual Basic]
- -langversion compiler option [Visual Basic]
ms.assetid: 59b7b0c8-2dde-4e9b-94e7-0237f7e0bafb
ms.openlocfilehash: 286dd8bd9949b584cec38642f44ba9ac5e924732
ms.sourcegitcommit: b7a8b09828bab4e90f66af8d495ecd7024c45042
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/04/2020
ms.locfileid: "87557180"
---
# <a name="-langversion-visual-basic"></a>-langversion (Visual Basic)
Powoduje, że kompilator akceptuje tylko składnię, która jest uwzględniona w określonej Visual Basic wersji językowej.  
  
## <a name="syntax"></a>Składnia  
  
```console  
-langversion:version  
```  
  
## <a name="arguments"></a>Argumenty  
 `version`  
 Wymagany. Wersja języka do użycia podczas kompilacji. Akceptowane wartości to,,,,,, `9` `10` ,, `11` `12` `14` `15` `15.3` `15.5` `default` i `latest` .

 Wszystkie liczby całkowite można także określić za pomocą `.0` jako wersji pomocniczej, na przykład `11.0` .

 Listę wszystkich możliwych wartości można wyświetlić, określając `-langversion:?` w wierszu polecenia.  
  
## <a name="remarks"></a>Uwagi  
 `-langversion`Opcja określa składnię akceptowaną przez kompilator. Na przykład jeśli określisz, że wersja językowa to 9,0, kompilator generuje błędy dla składni, która jest prawidłowa tylko w wersji 10,0 lub nowszej.  
  
 Tej opcji można użyć podczas tworzenia aplikacji przeznaczonych dla różnych wersji .NET Framework. Na przykład jeśli jesteś celem .NET Framework 3,5, możesz użyć tej opcji, aby upewnić się, że nie używasz składni z wersji językowej 10,0.  
  
 Można ustawić `-langversion` bezpośrednio tylko przy użyciu wiersza polecenia. Aby uzyskać więcej informacji, zobacz [Określanie konkretnej wersji .NET Framework](/visualstudio/ide/visual-studio-multi-targeting-overview).  
  
## <a name="example"></a>Przykład  
 Poniższy kod kompiluje `sample.vb` dla Visual Basic 9,0.  
  
```console  
vbc -langversion:9.0 sample.vb  
```  
  
## <a name="see-also"></a>Zobacz też

- [Kompilator wiersza polecenia Visual Basic](index.md)
- [Przykłady kompilacji — wiersze poleceń](sample-compilation-command-lines.md)
