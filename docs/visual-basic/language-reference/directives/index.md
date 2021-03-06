---
title: Dyrektyw
ms.date: 07/20/2015
helpviewer_keywords:
- directives, Visual Basic compiler
- Visual Basic code, directives
- directives
ms.assetid: 20d5fe65-490a-4c23-88c2-ee4f490ed762
ms.openlocfilehash: b5fcf3cb8801bc99dd2096c28cc41ebefeb34592
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/04/2020
ms.locfileid: "84410000"
---
# <a name="directives-visual-basic"></a>Directives (Visual Basic)

W tematach w tej sekcji udokumentowano dyrektywy kompilatora Visual Basic kodu źródłowego.  
  
## <a name="in-this-section"></a>W tej sekcji  

 [#Const — dyrektywa](const-directive.md) — Definiowanie stałej kompilatora  
  
 [#ExternalSource dyrektywie](externalsource-directive.md) --wskazać mapowanie między liniami źródłowymi a tekstem zewnętrznym względem źródła  
  
 [#If... Then... #Else — dyrektywy](if-then-else-directives.md) — Kompilowanie wybranych bloków kodu  
  
 [#Region dyrektywie](region-directive.md) — zwijanie i ukrywanie fragmentów kodu w edytorze programu Visual Studio  
  
 **#Disable, #Enable** --wyłączyć i włączyć określone ostrzeżenia dla regionów kodu.  
  
```vb  
#Disable Warning BC42356 ' suppress warning about no awaits in this method  
    Async Function TestAsync() As Task  
        Console.WriteLine("testing")  
    End Function  
#Enable Warning BC42356  
```  
  
 Można również wyłączyć i włączyć listę kodów ostrzeżeń rozdzielonych przecinkami.  
  
## <a name="related-sections"></a>Sekcje pokrewne  

 [Dokumentacja języka Visual Basic](../index.md)  
  