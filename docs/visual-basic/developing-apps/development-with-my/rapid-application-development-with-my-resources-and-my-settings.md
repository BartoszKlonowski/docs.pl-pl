---
title: Szybkie opracowywanie aplikacji przy użyciu My.Resources i My.Settings
ms.date: 07/20/2015
helpviewer_keywords:
- My.Settings object [Visual Basic], developing applications
- rapid application development (RAD), My.Resources
- rapid application development (RAD), My.Settings
- My.Resources object [Visual Basic], developing applications
ms.assetid: 68284ab1-b685-4814-a2a4-01ae40445ff8
ms.openlocfilehash: fd1ec25582e919b84235502f5921edfbc6e1dade
ms.sourcegitcommit: 45c8eed045779b70a47b23169897459d0323dc89
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/18/2020
ms.locfileid: "84990203"
---
# <a name="rapid-application-development-with-myresources-and-mysettings-visual-basic"></a>Szybkie opracowywanie aplikacji przy użyciu My.Resources i My.Settings (Visual Basic)

`My.Resources`Obiekt zapewnia dostęp do zasobów aplikacji i umożliwia dynamiczne pobieranie zasobów dla aplikacji.  
  
## <a name="retrieving-resources"></a>Pobieranie zasobów  

 Wiele zasobów, takich jak pliki audio, ikony, obrazy i ciągi, można pobrać za pomocą `My.Resources` obiektu. Można na przykład uzyskać dostęp do plików zasobów specyficznych dla kultury aplikacji. Poniższy przykład ustawia ikonę formularza na ikonę o nazwie `Form1Icon` przechowywanej w pliku zasobów aplikacji.  
  
 [!code-vb[VbVbcnMy#7](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnMy/VB/Class1.vb#7)]  
  
 `My.Resources`Obiekt uwidacznia tylko zasoby globalne. Nie zapewnia dostępu do plików zasobów skojarzonych z formularzami. Uzyskaj dostęp do formularzy zasoby z formularza.  
  
 Podobnie `My.Settings` obiekt zapewnia dostęp do ustawień aplikacji i umożliwia dynamiczne przechowywanie i pobieranie ustawień właściwości oraz innych informacji dotyczących aplikacji. Aby uzyskać więcej informacji, zobacz [Moje obiekty Resources](../../language-reference/objects/my-resources-object.md) i [My. Settings](../../language-reference/objects/my-settings-object.md).  
  
## <a name="see-also"></a>Zobacz też

- [My.Resources — Obiekt](../../language-reference/objects/my-resources-object.md)
- [My.Settings — Obiekt](../../language-reference/objects/my-settings-object.md)
- [Uzyskiwanie dostępu do ustawień aplikacji](../programming/app-settings/index.md)
