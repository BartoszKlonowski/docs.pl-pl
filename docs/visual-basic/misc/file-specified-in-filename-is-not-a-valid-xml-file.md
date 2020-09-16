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
# <a name="file-specified-in-filename-is-not-a-valid-xml-file"></a><span data-ttu-id="99913-102">Plik określony w nazwie pliku nie jest prawidłowym plikiem XML</span><span class="sxs-lookup"><span data-stu-id="99913-102">File specified in FileName is not a valid XML file</span></span>

<span data-ttu-id="99913-103">Podana nazwa pliku nie jest prawidłowym plikiem XML.</span><span class="sxs-lookup"><span data-stu-id="99913-103">The file name that you supplied is not a valid XML file.</span></span> <span data-ttu-id="99913-104">Aby określić dozwoloną strukturę i zawartość dokumentu XML, można użyć definicji typu dokumentu (DTD), schematu z ograniczeniami (XDR) języka Microsoft XML lub schematu definicji schematu XML (XSD).</span><span class="sxs-lookup"><span data-stu-id="99913-104">To specify the allowed structure and content of an XML document, you can use a Document Type Definition (DTD), a Microsoft XML-Data Reduced (XDR) schema, or an XML Schema definition language (XSD) schema.</span></span> <span data-ttu-id="99913-105">Schematy XSD są preferowanym sposobem określania gramatyki XML w .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="99913-105">XSD schemas are the preferred way to specify XML grammars in the .NET Framework.</span></span>

> [!NOTE]
> <span data-ttu-id="99913-106">W niektórych wcześniejszych wersjach programu Visual Studio **Projektant XML** jest projektantem dla wpisanych zestawów danych i schematu XML.</span><span class="sxs-lookup"><span data-stu-id="99913-106">In some earlier versions of Visual Studio, the **XML Designer** is the designer for typed datasets and XML schema.</span></span> <span data-ttu-id="99913-107">**Projektant XML** może nadal służyć do tworzenia i edytowania plików schematu XML.</span><span class="sxs-lookup"><span data-stu-id="99913-107">The **XML Designer** can still be used to create and edit XML schema files.</span></span> <span data-ttu-id="99913-108">Jednak w programie Visual Studio 2012 Projektant do tworzenia i edytowania wpisanych zestawów danych jest **Projektant obiektów DataSet**.</span><span class="sxs-lookup"><span data-stu-id="99913-108">However, in Visual Studio 2012, the designer for creating and editing typed datasets is the **Dataset Designer**.</span></span> <span data-ttu-id="99913-109">Aby uzyskać więcej informacji, zobacz [Tworzenie i edytowanie wpisanych zestawów danych](/previous-versions/visualstudio/visual-studio-2013/314t4see(v=vs.120)).</span><span class="sxs-lookup"><span data-stu-id="99913-109">For more information, see [Creating and Editing Typed Datasets](/previous-versions/visualstudio/visual-studio-2013/314t4see(v=vs.120)).</span></span>

## <a name="to-correct-this-error"></a><span data-ttu-id="99913-110">Aby poprawić ten błąd</span><span class="sxs-lookup"><span data-stu-id="99913-110">To correct this error</span></span>

- <span data-ttu-id="99913-111">Sprawdź, czy podano poprawną nazwę pliku.</span><span class="sxs-lookup"><span data-stu-id="99913-111">Check that you are supplying the correct file name.</span></span>

- <span data-ttu-id="99913-112">Sprawdź, czy określony plik zawiera prawidłowy kod XML przez załadowanie pliku XML, który chcesz zaewidencjonować do **projektanta XML**.</span><span class="sxs-lookup"><span data-stu-id="99913-112">Check that the specified file contains valid XML by loading the XML file that you want to check into the **XML Designer**.</span></span> <span data-ttu-id="99913-113">W menu **XML** kliknij polecenie **Weryfikuj kod XML**.</span><span class="sxs-lookup"><span data-stu-id="99913-113">From the **XML** menu, click **Validate XML**.</span></span> <span data-ttu-id="99913-114">Błędy są wyświetlane w **Lista zadań**.</span><span class="sxs-lookup"><span data-stu-id="99913-114">Errors are displayed in the **Task List**.</span></span>

- <span data-ttu-id="99913-115">Jeśli plik XML ma skojarzony schemat XML, sprawdź, czy elementy są widoczne w zdefiniowanej strukturze i czy zawartość poszczególnych elementów jest zgodna z zadeklarowanymi typami danych określonymi w schemacie.</span><span class="sxs-lookup"><span data-stu-id="99913-115">If the XML file has an associated XML Schema, check that the elements appear in the defined structure and that the content of the individual elements conforms to the declared data types specified in the schema.</span></span>

## <a name="see-also"></a><span data-ttu-id="99913-116">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="99913-116">See also</span></span>

- <xref:System.Xml>
- [<span data-ttu-id="99913-117">Instrukcje: Analizowanie ścieżek plików</span><span class="sxs-lookup"><span data-stu-id="99913-117">How to: Parse File Paths</span></span>](../developing-apps/programming/drives-directories-files/how-to-parse-file-paths.md)
