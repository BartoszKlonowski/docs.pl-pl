---
title: Plik określony w nazwie pliku nie jest prawidłowym plikiem XML
ms.date: 07/20/2015
ms.assetid: c4c30bf3-e0ad-4bc8-89e0-2c3e49e9793b
ms.openlocfilehash: 7d9500e58044f52a4e2508c9cb23a0e8186bc08d
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/15/2020
ms.locfileid: "90553899"
---
# <a name="file-specified-in-filename-is-not-a-valid-xml-file"></a>Plik określony w nazwie pliku nie jest prawidłowym plikiem XML

Podana nazwa pliku nie jest prawidłowym plikiem XML. Aby określić dozwoloną strukturę i zawartość dokumentu XML, można użyć definicji typu dokumentu (DTD), schematu z ograniczeniami (XDR) języka Microsoft XML lub schematu definicji schematu XML (XSD). Schematy XSD są preferowanym sposobem określania gramatyki XML w .NET Framework.

> [!NOTE]
> W niektórych wcześniejszych wersjach programu Visual Studio **Projektant XML** jest projektantem dla wpisanych zestawów danych i schematu XML. **Projektant XML** może nadal służyć do tworzenia i edytowania plików schematu XML. Jednak w programie Visual Studio 2012 Projektant do tworzenia i edytowania wpisanych zestawów danych jest **Projektant obiektów DataSet**. Aby uzyskać więcej informacji, zobacz [Tworzenie i edytowanie wpisanych zestawów danych](/previous-versions/visualstudio/visual-studio-2013/314t4see(v=vs.120)).

## <a name="to-correct-this-error"></a>Aby poprawić ten błąd

- Sprawdź, czy podano poprawną nazwę pliku.

- Sprawdź, czy określony plik zawiera prawidłowy kod XML przez załadowanie pliku XML, który chcesz zaewidencjonować do **projektanta XML**. W menu **XML** kliknij polecenie **Weryfikuj kod XML**. Błędy są wyświetlane w **Lista zadań**.

- Jeśli plik XML ma skojarzony schemat XML, sprawdź, czy elementy są widoczne w zdefiniowanej strukturze i czy zawartość poszczególnych elementów jest zgodna z zadeklarowanymi typami danych określonymi w schemacie.

## <a name="see-also"></a>Zobacz także

- <xref:System.Xml>
- [Instrukcje: Analizowanie ścieżek plików](../developing-apps/programming/drives-directories-files/how-to-parse-file-paths.md)
