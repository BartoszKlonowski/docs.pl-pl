---
title: Jak zapewnić okno dialogowe postępu dla operacji na plikach — Przewodnik programowania w języku C#
description: Dowiedz się, jak udostępnić okno dialogowe postępu dla operacji na plikach przy użyciu metody CopyFile (String, String, UIOption).
ms.date: 07/20/2015
helpviewer_keywords:
- progress dialog [C#]
ms.assetid: 01b71fe7-8178-4dc8-aeb1-12053be7b51c
ms.openlocfilehash: 5d16aeb3a5394ca250e4a5e26074db797c54216d
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91185889"
---
# <a name="how-to-provide-a-progress-dialog-box-for-file-operations-c-programming-guide"></a>Jak zapewnić okno dialogowe postępu dla operacji na plikach (Przewodnik programowania w języku C#)

Możesz podać standardowe okno dialogowe, które pokazuje postęp operacji na plikach w systemie Windows, jeśli używasz <xref:Microsoft.VisualBasic.FileIO.FileSystem.CopyFile%28System.String%2CSystem.String%2CMicrosoft.VisualBasic.FileIO.UIOption%29> metody z <xref:Microsoft.VisualBasic?displayProperty=nameWithType> przestrzeni nazw.  
  
[!INCLUDE[note_settings_general](~/includes/note-settings-general-md.md)]  
  
### <a name="to-add-a-reference-in-visual-studio"></a>Aby dodać odwołanie w programie Visual Studio  
  
1. Na pasku menu wybierz **projekt**, **Dodaj odwołanie**.  
  
     Zostanie wyświetlone okno dialogowe **Menedżer odwołań** .  
  
2. W obszarze **zestawy** wybierz pozycję **Struktura** , jeśli nie została jeszcze wybrana.  
  
3. Na liście nazw zaznacz pole wyboru **Microsoft. VisualBasic** , a następnie wybierz przycisk **OK** , aby zamknąć okno dialogowe.  
  
## <a name="example"></a>Przykład  

 Poniższy kod kopiuje katalog `sourcePath` określany w katalogu, który określa `destinationPath` . Ten kod udostępnia również standardowe okno dialogowe, które pokazuje szacowany czas pozostały do zakończenia operacji.  
  
 [!code-csharp[csFilesandFolders#11](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csFilesAndFolders/CS/FileIteration.cs#11)]  
  
## <a name="see-also"></a>Zobacz też

- [System plików i rejestr (Przewodnik programowania w języku C#)](./index.md)
