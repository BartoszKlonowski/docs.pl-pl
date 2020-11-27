---
title: Tworzenie plików zasobów dla aplikacji .NET
description: Utwórz pliki zasobów dla aplikacji .NET. Twórz pliki tekstowe z użyciem zasobów ciągów, plików XML lub obiektów binarnych programowo lub plików XML, których dane są ciągami, obrazami lub obiektami.
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- resource files, .resources files
- .resources files
- application resources, creating files
- resource files, creating
ms.assetid: 6c5ad891-66a0-4e7a-adcf-f41863ba6d8d
ms.openlocfilehash: d10af40420c1ab9ab177514c0babeaf5cea96922
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96259079"
---
# <a name="create-resource-files-for-net-apps"></a><span data-ttu-id="d341e-104">Tworzenie plików zasobów dla aplikacji .NET</span><span class="sxs-lookup"><span data-stu-id="d341e-104">Create resource files for .NET apps</span></span>

<span data-ttu-id="d341e-105">Zasoby, takie jak ciągi, obrazy lub dane obiektów, można uwzględnić w plikach zasobów, aby były one łatwo dostępne dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d341e-105">You can include resources, such as strings, images, or object data, in resources files to make them easily available to your application.</span></span> <span data-ttu-id="d341e-106">.NET Framework oferuje pięć metod tworzenia plików zasobów:</span><span class="sxs-lookup"><span data-stu-id="d341e-106">The .NET Framework offers five ways to create resources files:</span></span>

- <span data-ttu-id="d341e-107">Utwórz plik tekstowy, który zawiera zasoby ciągu.</span><span class="sxs-lookup"><span data-stu-id="d341e-107">Create a text file that contains string resources.</span></span> <span data-ttu-id="d341e-108">Przy użyciu [generatora plików zasobów (Resgen.exe)](../tools/resgen-exe-resource-file-generator.md) można skonwertować plik tekstowy do pliku zasobów binarnych (Resources).</span><span class="sxs-lookup"><span data-stu-id="d341e-108">You can use [Resource File Generator (Resgen.exe)](../tools/resgen-exe-resource-file-generator.md) to convert the text file into a binary resource (.resources) file.</span></span> <span data-ttu-id="d341e-109">Następnie można osadzić plik zasobów binarnych w pliku wykonywalnym aplikacji lub bibliotece aplikacji przy użyciu kompilatora języka lub osadzić go w zestawie satelitarnym za pomocą [konsolidatora zestawu (Al.exe)](../tools/al-exe-assembly-linker.md).</span><span class="sxs-lookup"><span data-stu-id="d341e-109">You can then embed the binary resource file  in an application executable or an application library by using a language compiler, or you can embed it in a satellite assembly by using [Assembly Linker (Al.exe)](../tools/al-exe-assembly-linker.md).</span></span> <span data-ttu-id="d341e-110">Aby uzyskać więcej informacji, zobacz sekcję [zasoby w plikach tekstowych](creating-resource-files-for-desktop-apps.md#TextFiles) .</span><span class="sxs-lookup"><span data-stu-id="d341e-110">For more information, see the [Resources in Text Files](creating-resource-files-for-desktop-apps.md#TextFiles) section.</span></span>

- <span data-ttu-id="d341e-111">Utwórz plik zasobów XML (resx), który zawiera ciąg, obraz lub dane obiektu.</span><span class="sxs-lookup"><span data-stu-id="d341e-111">Create an XML resource (.resx) file that contains string, image, or object data.</span></span> <span data-ttu-id="d341e-112">Przy użyciu [generatora plików zasobów (Resgen.exe)](../tools/resgen-exe-resource-file-generator.md) można skonwertować plik resx do pliku zasobów binarnych (Resources).</span><span class="sxs-lookup"><span data-stu-id="d341e-112">You can use [Resource File Generator (Resgen.exe)](../tools/resgen-exe-resource-file-generator.md) to convert the .resx file into a binary resource (.resources) file.</span></span> <span data-ttu-id="d341e-113">Następnie można osadzić plik zasobów binarnych w pliku wykonywalnym aplikacji lub bibliotece aplikacji przy użyciu kompilatora języka lub osadzić go w zestawie satelitarnym za pomocą [konsolidatora zestawu (Al.exe)](../tools/al-exe-assembly-linker.md).</span><span class="sxs-lookup"><span data-stu-id="d341e-113">You can then embed the binary resource file in an application executable or an application library by using a language compiler, or you can embed it in a satellite assembly by using [Assembly Linker (Al.exe)](../tools/al-exe-assembly-linker.md).</span></span> <span data-ttu-id="d341e-114">Aby uzyskać więcej informacji, zobacz sekcję [zasoby w plikach resx](creating-resource-files-for-desktop-apps.md#ResxFiles) .</span><span class="sxs-lookup"><span data-stu-id="d341e-114">For more information, see the [Resources in .resx Files](creating-resource-files-for-desktop-apps.md#ResxFiles) section.</span></span>

- <span data-ttu-id="d341e-115">Utwórz programowo plik zasobów XML (resx) przy użyciu typów w <xref:System.Resources> przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="d341e-115">Create an XML resource (.resx) file programmatically by using types in the <xref:System.Resources> namespace.</span></span> <span data-ttu-id="d341e-116">Można utworzyć plik resx, wyliczyć jego zasoby i pobrać określone zasoby według nazwy.</span><span class="sxs-lookup"><span data-stu-id="d341e-116">You can create a .resx file, enumerate its resources, and retrieve specific resources by name.</span></span> <span data-ttu-id="d341e-117">Aby uzyskać więcej informacji, zobacz [Praca z plikami resx programowo](working-with-resx-files-programmatically.md).</span><span class="sxs-lookup"><span data-stu-id="d341e-117">For more information, see [Working with .resx Files Programmatically](working-with-resx-files-programmatically.md).</span></span>

- <span data-ttu-id="d341e-118">Utwórz programowo plik zasobów binarnych (Resources).</span><span class="sxs-lookup"><span data-stu-id="d341e-118">Create a binary resource (.resources) file programmatically.</span></span> <span data-ttu-id="d341e-119">Następnie można osadzić plik w pliku wykonywalnym aplikacji lub bibliotece aplikacji przy użyciu kompilatora języka lub osadzić go w zestawie satelickim za pomocą [konsolidatora zestawu (Al.exe)](../tools/al-exe-assembly-linker.md).</span><span class="sxs-lookup"><span data-stu-id="d341e-119">You can then embed the file in an application executable or an application library by using a language compiler, or you can embed it in a satellite assembly by using [Assembly Linker (Al.exe)](../tools/al-exe-assembly-linker.md).</span></span> <span data-ttu-id="d341e-120">Aby uzyskać więcej informacji, zobacz sekcję [Resources in. resources Files](creating-resource-files-for-desktop-apps.md#ResourcesFiles) .</span><span class="sxs-lookup"><span data-stu-id="d341e-120">For more information, see the [Resources in .resources Files](creating-resource-files-for-desktop-apps.md#ResourcesFiles) section.</span></span>

- <span data-ttu-id="d341e-121">Użyj [programu Visual Studio](https://visualstudio.microsoft.com/vs/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link) , aby utworzyć plik zasobów i uwzględnić go w projekcie.</span><span class="sxs-lookup"><span data-stu-id="d341e-121">Use [Visual Studio](https://visualstudio.microsoft.com/vs/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link) to create a resource file and include it in your project.</span></span> <span data-ttu-id="d341e-122">Program Visual Studio udostępnia Edytor zasobów, który pozwala dodawać, usuwać i modyfikować zasoby.</span><span class="sxs-lookup"><span data-stu-id="d341e-122">Visual Studio provides a resource editor that lets you add, delete, and modify resources.</span></span> <span data-ttu-id="d341e-123">W czasie kompilacji plik zasobów jest automatycznie konwertowany na plik binarny. resources i osadzony w zestawie aplikacji lub w zestawie satelickim.</span><span class="sxs-lookup"><span data-stu-id="d341e-123">At compile time, the resource file is automatically converted to a binary .resources file and embedded in an application assembly or satellite assembly.</span></span> <span data-ttu-id="d341e-124">Aby uzyskać więcej informacji, zobacz sekcję [pliki zasobów w programie Visual Studio](creating-resource-files-for-desktop-apps.md#VSResFiles) .</span><span class="sxs-lookup"><span data-stu-id="d341e-124">For more information, see the [Resource Files in Visual Studio](creating-resource-files-for-desktop-apps.md#VSResFiles) section.</span></span>

<a name="TextFiles"></a>

## <a name="resources-in-text-files"></a><span data-ttu-id="d341e-125">Zasoby w plikach tekstowych</span><span class="sxs-lookup"><span data-stu-id="d341e-125">Resources in text files</span></span>

<span data-ttu-id="d341e-126">Pliki tekstowe (. txt lub. restext) można używać do przechowywania tylko zasobów ciągu.</span><span class="sxs-lookup"><span data-stu-id="d341e-126">You can use text (.txt or .restext) files to store string resources only.</span></span> <span data-ttu-id="d341e-127">W przypadku zasobów niebędących ciągami należy używać plików resx lub tworzyć je programowo.</span><span class="sxs-lookup"><span data-stu-id="d341e-127">For non-string resources, use .resx files or create them programmatically.</span></span> <span data-ttu-id="d341e-128">Pliki tekstowe zawierające zasoby ciągów mają następujący format:</span><span class="sxs-lookup"><span data-stu-id="d341e-128">Text files that contain string resources have the following format:</span></span>

```text
# This is an optional comment.
name = value

; This is another optional comment.
name = value

; The following supports conditional compilation if X is defined.
#ifdef X
name1=value1
name2=value2
#endif

# The following supports conditional compilation if Y is undefined.
#if !Y
name1=value1
name2=value2
#endif
```

 <span data-ttu-id="d341e-129">Format pliku zasobów. txt i. restext jest identyczny.</span><span class="sxs-lookup"><span data-stu-id="d341e-129">The resource file format of .txt and .restext files is identical.</span></span> <span data-ttu-id="d341e-130">Rozszerzenie pliku. restext służy tylko do wprowadzania plików tekstowych, które mają być bezpośrednio identyfikowane jako pliki zasobów tekstowych.</span><span class="sxs-lookup"><span data-stu-id="d341e-130">The .restext file extension merely serves to make text files immediately identifiable as text-based resource files.</span></span>

 <span data-ttu-id="d341e-131">Zasoby ciągów są wyświetlane jako pary *nazwa/wartość* , gdzie *name* jest ciągiem, który identyfikuje zasób, a *wartość* to ciąg zasobu, który jest zwracany w przypadku przekazania *nazwy* do metody pobierania zasobu, takiej jak <xref:System.Resources.ResourceManager.GetString%2A?displayProperty=nameWithType> .</span><span class="sxs-lookup"><span data-stu-id="d341e-131">String resources appear as *name/value* pairs, where *name* is a string that identifies the resource, and *value* is the resource string that is returned when you pass *name* to a resource retrieval method such as <xref:System.Resources.ResourceManager.GetString%2A?displayProperty=nameWithType>.</span></span> <span data-ttu-id="d341e-132">*Nazwa* i *wartość* muszą być rozdzielone znakiem równości (=).</span><span class="sxs-lookup"><span data-stu-id="d341e-132">*name* and *value* must be separated by an equal sign (=).</span></span> <span data-ttu-id="d341e-133">Przykład:</span><span class="sxs-lookup"><span data-stu-id="d341e-133">For example:</span></span>

```text
FileMenuName=File
EditMenuName=Edit
ViewMenuName=View
HelpMenuName=Help
```

> [!CAUTION]
> <span data-ttu-id="d341e-134">Nie należy używać plików zasobów do przechowywania haseł, informacji o zabezpieczeniach ani danych prywatnych.</span><span class="sxs-lookup"><span data-stu-id="d341e-134">Do not use resource files to store passwords, security-sensitive information, or private data.</span></span>

 <span data-ttu-id="d341e-135">Puste ciągi (czyli zasób, którego wartość jest <xref:System.String.Empty?displayProperty=nameWithType> ) są dozwolone w plikach tekstowych.</span><span class="sxs-lookup"><span data-stu-id="d341e-135">Empty strings (that is, a resource whose value is <xref:System.String.Empty?displayProperty=nameWithType>) are permitted in text files.</span></span> <span data-ttu-id="d341e-136">Przykład:</span><span class="sxs-lookup"><span data-stu-id="d341e-136">For example:</span></span>

```text
EmptyString=
```

 <span data-ttu-id="d341e-137">Począwszy od .NET Framework 4,5 i we wszystkich wersjach programu .NET Core pliki tekstowe obsługują kompilację warunkową z `#ifdef` *symbolem*... `#endif` i `#if !` *symbolem*... `#endif` konstrukcje.</span><span class="sxs-lookup"><span data-stu-id="d341e-137">Starting with .NET Framework 4.5 and in all versions of .NET Core, text files support conditional compilation with the `#ifdef`*symbol*... `#endif` and `#if !`*symbol*... `#endif` constructs.</span></span> <span data-ttu-id="d341e-138">Następnie można użyć `/define` przełącznika z [generatorem plików zasobów (Resgen.exe)](../tools/resgen-exe-resource-file-generator.md) do definiowania symboli.</span><span class="sxs-lookup"><span data-stu-id="d341e-138">You can then use the `/define` switch with [Resource File Generator (Resgen.exe)](../tools/resgen-exe-resource-file-generator.md) to define symbols.</span></span> <span data-ttu-id="d341e-139">Każdy zasób wymaga własnego `#ifdef` *symbolu*... `#endif` lub `#if !` *symbolu*... `#endif` konstrukcja.</span><span class="sxs-lookup"><span data-stu-id="d341e-139">Each resource requires its own `#ifdef`*symbol*... `#endif` or `#if !`*symbol*... `#endif` construct.</span></span> <span data-ttu-id="d341e-140">Jeśli używasz `#ifdef` instrukcji i *symbol* jest zdefiniowany, skojarzony zasób zostanie uwzględniony w pliku Resources; w przeciwnym razie nie jest uwzględniony.</span><span class="sxs-lookup"><span data-stu-id="d341e-140">If you use an `#ifdef` statement and *symbol* is defined, the associated resource is included in the .resources file; otherwise, it is not included.</span></span> <span data-ttu-id="d341e-141">Jeśli używasz `#if !` instrukcji i *symbol* nie jest zdefiniowany, skojarzony zasób zostanie uwzględniony w pliku Resources; w przeciwnym razie nie jest uwzględniony.</span><span class="sxs-lookup"><span data-stu-id="d341e-141">If you use an `#if !` statement and *symbol* is not defined, the associated resource is included in the .resources file; otherwise, it is not included.</span></span>

 <span data-ttu-id="d341e-142">Komentarze są opcjonalne w plikach tekstowych i poprzedzane średnikami (;) lub znakiem krzyżyka (#) na początku wiersza.</span><span class="sxs-lookup"><span data-stu-id="d341e-142">Comments are optional in text files and are preceded either by a semicolon (;) or by a pound sign (#) at the beginning of a line.</span></span> <span data-ttu-id="d341e-143">Wiersze zawierające Komentarze można umieścić w dowolnym miejscu w pliku.</span><span class="sxs-lookup"><span data-stu-id="d341e-143">Lines that contain comments can be placed anywhere in the file.</span></span> <span data-ttu-id="d341e-144">Komentarze nie są uwzględniane w skompilowanym pliku Resources, który jest tworzony przy użyciu [generatora plików zasobów (Resgen.exe)](../tools/resgen-exe-resource-file-generator.md).</span><span class="sxs-lookup"><span data-stu-id="d341e-144">Comments are not included in a compiled .resources file that is created by using [Resource File Generator (Resgen.exe)](../tools/resgen-exe-resource-file-generator.md).</span></span>

 <span data-ttu-id="d341e-145">Wszystkie puste wiersze w plikach tekstowych są uważane za białe znaki i są ignorowane.</span><span class="sxs-lookup"><span data-stu-id="d341e-145">Any blank lines in the text files are considered to be white space and are ignored.</span></span>

 <span data-ttu-id="d341e-146">W poniższym przykładzie zdefiniowano dwa zasoby ciągu o nazwie `OKButton` i `CancelButton` .</span><span class="sxs-lookup"><span data-stu-id="d341e-146">The following example defines two string resources named `OKButton` and `CancelButton`.</span></span>

```text
#Define resources for buttons in the user interface.
OKButton=OK
CancelButton=Cancel
```

 <span data-ttu-id="d341e-147">Jeśli plik tekstowy zawiera zduplikowane wystąpienia *nazwy*, [Generator plików zasobów (Resgen.exe)](../tools/resgen-exe-resource-file-generator.md) wyświetla ostrzeżenie i ignoruje drugą nazwę.</span><span class="sxs-lookup"><span data-stu-id="d341e-147">If the text file contains duplicate occurrences of *name*, [Resource File Generator (Resgen.exe)](../tools/resgen-exe-resource-file-generator.md) displays a warning and ignores the second name.</span></span>

 <span data-ttu-id="d341e-148">*wartość* nie może zawierać znaków nowego wiersza, ale można użyć znaków ucieczki w stylu języka C, takich jak `\n` do reprezentowania nowego wiersza i `\t` reprezentowania karty. Możesz również uwzględnić znak ukośnika odwrotnego, jeśli zostanie on zmieniony (na przykład " \\ \\ ").</span><span class="sxs-lookup"><span data-stu-id="d341e-148">*value* cannot contain new line characters, but you can use C language-style escape characters such as `\n` to represent a new line and `\t` to represent a tab. You can also include a backslash character if it is escaped (for example, "\\\\").</span></span> <span data-ttu-id="d341e-149">Ponadto dozwolony jest pusty ciąg.</span><span class="sxs-lookup"><span data-stu-id="d341e-149">In addition, an empty string is permitted.</span></span>

 <span data-ttu-id="d341e-150">Zapisz zasoby w formacie pliku tekstowego przy użyciu kodowania UTF-8 lub kodowania UTF-16 w kolejności bajtów little-endian lub big-endian.</span><span class="sxs-lookup"><span data-stu-id="d341e-150">Save resources in text file format by using UTF-8 encoding or UTF-16 encoding in either little-endian or big-endian byte order.</span></span> <span data-ttu-id="d341e-151">Jednak [Generator plików zasobów (Resgen.exe)](../tools/resgen-exe-resource-file-generator.md), który konwertuje plik txt na plik resources, domyślnie traktuje pliki jako UTF-8.</span><span class="sxs-lookup"><span data-stu-id="d341e-151">However, [Resource File Generator (Resgen.exe)](../tools/resgen-exe-resource-file-generator.md), which converts a .txt file to a .resources file, treats files as UTF-8 by default.</span></span> <span data-ttu-id="d341e-152">Jeśli chcesz, aby Resgen.exe rozpoznać plik, który został zakodowany przy użyciu kodowania UTF-16, musisz dołączyć znak kolejności bajtów Unicode (U + FEFF) na początku pliku.</span><span class="sxs-lookup"><span data-stu-id="d341e-152">If you want Resgen.exe to recognize a file that was encoded using UTF-16, you must include a Unicode byte order mark (U+FEFF) at the beginning of the file.</span></span>

 <span data-ttu-id="d341e-153">Aby osadzić plik zasobów w formacie tekstowym w zestawie .NET, należy przekonwertować plik do pliku zasobów binarnych (. resources) przy użyciu [generatora plików zasobów (Resgen.exe)](../tools/resgen-exe-resource-file-generator.md).</span><span class="sxs-lookup"><span data-stu-id="d341e-153">To embed a resource file in text format into a .NET assembly, you must convert the file to a binary resource (.resources) file by using [Resource File Generator (Resgen.exe)](../tools/resgen-exe-resource-file-generator.md).</span></span> <span data-ttu-id="d341e-154">Następnie można osadzić plik resources w zestawie .NET przy użyciu kompilatora języka lub osadzić go w zestawie satelickim za pomocą [konsolidatora zestawu (Al.exe)](../tools/al-exe-assembly-linker.md).</span><span class="sxs-lookup"><span data-stu-id="d341e-154">You can then embed the .resources file in a .NET assembly by using a language compiler or embed it in a satellite assembly by using [Assembly Linker (Al.exe)](../tools/al-exe-assembly-linker.md).</span></span>

 <span data-ttu-id="d341e-155">Poniższy przykład używa pliku zasobu w formacie tekstowym o nazwie GreetingResources.txt dla prostej aplikacji konsolowej "Hello world".</span><span class="sxs-lookup"><span data-stu-id="d341e-155">The following example uses a resource file in text format named GreetingResources.txt for a simple "Hello World" console application.</span></span> <span data-ttu-id="d341e-156">Plik tekstowy definiuje dwa ciągi `prompt` i `greeting` , który monituje użytkownika o wprowadzenie jego nazwy i wyświetlenie powitania.</span><span class="sxs-lookup"><span data-stu-id="d341e-156">The text file defines two strings, `prompt` and `greeting`, that prompt the user to enter their name and display a greeting.</span></span>

```text
# GreetingResources.txt
# A resource file in text format for a "Hello World" application.
#
# Initial prompt to the user.
prompt=Enter your name:
# Format string to display the result.
greeting=Hello, {0}!
```

<span data-ttu-id="d341e-157">Plik tekstowy jest konwertowany na plik resources za pomocą następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="d341e-157">The text file is converted to a .resources file by using the following command:</span></span>

```console
resgen GreetingResources.txt
```

 <span data-ttu-id="d341e-158">Poniższy przykład pokazuje kod źródłowy aplikacji konsolowej, która używa pliku Resources do wyświetlania komunikatów dla użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d341e-158">The following example shows the source code for a console application that uses the .resources file to display messages to the user.</span></span>

 [!code-csharp[Conceptual.Resources.TextFiles#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.resources.textfiles/cs/greeting.cs#1)]
 [!code-vb[Conceptual.Resources.TextFiles#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.resources.textfiles/vb/greeting.vb#1)]

 <span data-ttu-id="d341e-159">Jeśli używasz Visual Basic, a plik kodu źródłowego nosi nazwę Greetinging. vb, następujące polecenie tworzy plik wykonywalny zawierający osadzony plik Resources:</span><span class="sxs-lookup"><span data-stu-id="d341e-159">If you are using Visual Basic, and the source code file is named Greeting.vb, the following command creates an executable file that includes the embedded .resources file:</span></span>

```console
vbc greeting.vb -resource:GreetingResources.resources
```

 <span data-ttu-id="d341e-160">Jeśli używasz języka C#, a plik kodu źródłowego ma nazwę Greeting.cs, następujące polecenie tworzy plik wykonywalny zawierający osadzony plik Resources:</span><span class="sxs-lookup"><span data-stu-id="d341e-160">If you are using C#, and the source code file is named Greeting.cs, the following command creates an executable file that includes the embedded .resources file:</span></span>

```console
csc greeting.cs -resource:GreetingResources.resources
```

<a name="ResxFiles"></a>

## <a name="resources-in-resx-files"></a><span data-ttu-id="d341e-161">Zasoby w plikach resx</span><span class="sxs-lookup"><span data-stu-id="d341e-161">Resources in .resx files</span></span>

 <span data-ttu-id="d341e-162">W przeciwieństwie do plików tekstowych, które mogą przechowywać tylko zasoby ciągów, pliki zasobów XML (. resx) mogą przechowywać ciągi, dane binarne, takie jak obrazy, ikony i klipy audio i obiekty programistyczne.</span><span class="sxs-lookup"><span data-stu-id="d341e-162">Unlike text files, which can only store string resources, XML resource (.resx) files can store strings, binary data such as images, icons, and audio clips, and programmatic objects.</span></span> <span data-ttu-id="d341e-163">Plik. resx zawiera standardowy nagłówek, który opisuje format wpisów zasobów i określa informacje o wersji dla pliku XML, który jest używany do analizy danych.</span><span class="sxs-lookup"><span data-stu-id="d341e-163">A .resx file contains a standard header, which describes the format of the resource entries and specifies the versioning information for the XML that is used to parse the data.</span></span> <span data-ttu-id="d341e-164">Dane pliku zasobu są zgodne z nagłówkiem XML.</span><span class="sxs-lookup"><span data-stu-id="d341e-164">The resource file data follows the XML header.</span></span> <span data-ttu-id="d341e-165">Każdy element danych składa się z pary nazwa/wartość, które znajdują się w `data` tagu.</span><span class="sxs-lookup"><span data-stu-id="d341e-165">Each data item consists of a name/value pair that is contained in a `data` tag.</span></span> <span data-ttu-id="d341e-166">Jego `name` atrybut definiuje nazwę zasobu, a zagnieżdżony `value` tag zawiera wartość zasobu.</span><span class="sxs-lookup"><span data-stu-id="d341e-166">Its `name` attribute defines the resource name, and the nested `value` tag contains the resource value.</span></span> <span data-ttu-id="d341e-167">W przypadku danych ciągu `value` tag zawiera ciąg.</span><span class="sxs-lookup"><span data-stu-id="d341e-167">For string data, the `value` tag contains the string.</span></span>

 <span data-ttu-id="d341e-168">Na przykład następujący `data` tag definiuje zasób ciągu o nazwie, `prompt` którego wartość to "Wprowadź nazwę:".</span><span class="sxs-lookup"><span data-stu-id="d341e-168">For example, the following `data` tag defines a string resource named `prompt` whose value is "Enter your name:".</span></span>

```xml
<data name="prompt" xml:space="preserve">
  <value>Enter your name:</value>
</data>
```

> [!WARNING]
> <span data-ttu-id="d341e-169">Nie należy używać plików zasobów do przechowywania haseł, informacji o zabezpieczeniach ani danych prywatnych.</span><span class="sxs-lookup"><span data-stu-id="d341e-169">Do not use resource files to store passwords, security-sensitive information, or private data.</span></span>

 <span data-ttu-id="d341e-170">W przypadku obiektów zasobów tag **danych** zawiera `type` atrybut wskazujący typ danych zasobu.</span><span class="sxs-lookup"><span data-stu-id="d341e-170">For resource objects, the **data** tag includes a `type` attribute that indicates the data type of the resource.</span></span> <span data-ttu-id="d341e-171">W przypadku obiektów, które składają się z danych binarnych, `data` tag zawiera również `mimetype` atrybut, który wskazuje `base64` Typ danych binarnych.</span><span class="sxs-lookup"><span data-stu-id="d341e-171">For objects that consist of binary data, the `data` tag also includes a `mimetype` attribute, which indicates the `base64` type of the binary data.</span></span>

> [!NOTE]
> <span data-ttu-id="d341e-172">Wszystkie pliki RESX używają binarnego programu formatującego serializacji, aby generować i analizować dane binarne dla określonego typu.</span><span class="sxs-lookup"><span data-stu-id="d341e-172">All .resx files use a binary serialization formatter to generate and parse the binary data for a specified type.</span></span> <span data-ttu-id="d341e-173">W związku z tym plik resx może stać się nieprawidłowy, jeśli format serializacji binarnej obiektu zmienia się w niezgodny sposób.</span><span class="sxs-lookup"><span data-stu-id="d341e-173">As a result, a .resx file can become invalid if the binary serialization format for an object changes in an incompatible way.</span></span>

 <span data-ttu-id="d341e-174">Poniższy przykład przedstawia część pliku resx zawierającego <xref:System.Int32> zasób i obraz mapy bitowej.</span><span class="sxs-lookup"><span data-stu-id="d341e-174">The following example shows a portion of a .resx file that includes an <xref:System.Int32> resource and a bitmap image.</span></span>

```xml
<data name="i1" type="System.Int32, mscorlib">
  <value>20</value>
</data>

<data name="flag" type="System.Drawing.Bitmap, System.Drawing,
    Version=1.0.5000.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a"
    mimetype="application/x-microsoft.net.object.bytearray.base64">
  <value>
    AAEAAAD/////AQAAAAAAAAAMAgAAADtTeX…
  </value>
</data>
```

> [!IMPORTANT]
> <span data-ttu-id="d341e-175">Ponieważ pliki resx muszą zawierać poprawnie sformułowany kod XML w wstępnie zdefiniowanym formacie, nie zaleca się ręcznego pracy z plikami. resx, szczególnie gdy pliki RESX zawierają zasoby inne niż ciągi.</span><span class="sxs-lookup"><span data-stu-id="d341e-175">Because .resx files must consist of well-formed XML in a predefined format, we do not recommend working with .resx files manually, particularly when the .resx files contain resources other than strings.</span></span> <span data-ttu-id="d341e-176">Zamiast tego program [Visual Studio](https://visualstudio.microsoft.com/vs/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link) udostępnia przezroczysty interfejs do tworzenia plików resx i manipulowania nimi.</span><span class="sxs-lookup"><span data-stu-id="d341e-176">Instead, [Visual Studio](https://visualstudio.microsoft.com/vs/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link) provides a transparent interface for creating and manipulating .resx files.</span></span> <span data-ttu-id="d341e-177">Aby uzyskać więcej informacji, zobacz sekcję [pliki zasobów w programie Visual Studio](creating-resource-files-for-desktop-apps.md#VSResFiles) .</span><span class="sxs-lookup"><span data-stu-id="d341e-177">For more information, see the [Resource Files in Visual Studio](creating-resource-files-for-desktop-apps.md#VSResFiles) section.</span></span> <span data-ttu-id="d341e-178">Można również programistycznie tworzyć pliki resx i manipulować nimi.</span><span class="sxs-lookup"><span data-stu-id="d341e-178">You can also create and manipulate .resx files programmatically.</span></span> <span data-ttu-id="d341e-179">Aby uzyskać więcej informacji, zobacz [Praca z plikami resx programowo](working-with-resx-files-programmatically.md).</span><span class="sxs-lookup"><span data-stu-id="d341e-179">For more information, see [Working with .resx Files Programmatically](working-with-resx-files-programmatically.md).</span></span>

<a name="ResourcesFiles"></a>

## <a name="resources-in-resources-files"></a><span data-ttu-id="d341e-180">Zasoby w plikach. resources</span><span class="sxs-lookup"><span data-stu-id="d341e-180">Resources in .resources files</span></span>

<span data-ttu-id="d341e-181">Można użyć <xref:System.Resources.ResourceWriter?displayProperty=nameWithType> klasy do programistycznego tworzenia pliku zasobów binarnych (Resources) bezpośrednio w kodzie.</span><span class="sxs-lookup"><span data-stu-id="d341e-181">You can use the <xref:System.Resources.ResourceWriter?displayProperty=nameWithType> class to programmatically create a binary resource (.resources) file directly from code.</span></span> <span data-ttu-id="d341e-182">Przy użyciu [generatora plików zasobów (Resgen.exe)](../tools/resgen-exe-resource-file-generator.md) można również utworzyć plik resources z pliku tekstowego lub pliku resx.</span><span class="sxs-lookup"><span data-stu-id="d341e-182">You can also use [Resource File Generator (Resgen.exe)](../tools/resgen-exe-resource-file-generator.md) to create a .resources file from a text file or a .resx file.</span></span> <span data-ttu-id="d341e-183">Plik resources może zawierać dane binarne (tablice bajtowe) i dane obiektu oprócz danych ciągu.</span><span class="sxs-lookup"><span data-stu-id="d341e-183">The .resources file can contain binary data (byte arrays) and object data in addition to string data.</span></span> <span data-ttu-id="d341e-184">Programowe tworzenie pliku resources wymaga wykonania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="d341e-184">Programmatically creating a .resources file requires the following steps:</span></span>

1. <span data-ttu-id="d341e-185">Utwórz <xref:System.Resources.ResourceWriter> obiekt z unikatową nazwą pliku.</span><span class="sxs-lookup"><span data-stu-id="d341e-185">Create a <xref:System.Resources.ResourceWriter> object with a unique file name.</span></span> <span data-ttu-id="d341e-186">Można to zrobić, określając nazwę pliku lub strumień pliku do <xref:System.Resources.ResourceWriter> konstruktora klasy.</span><span class="sxs-lookup"><span data-stu-id="d341e-186">You can do this by specifying either a file name or a file stream to a <xref:System.Resources.ResourceWriter> class constructor.</span></span>

2. <span data-ttu-id="d341e-187">Wywołaj jedno z przeciążeń <xref:System.Resources.ResourceWriter.AddResource%2A?displayProperty=nameWithType> metody dla każdego nazwanego zasobu, aby dodać je do pliku.</span><span class="sxs-lookup"><span data-stu-id="d341e-187">Call one of the overloads of the <xref:System.Resources.ResourceWriter.AddResource%2A?displayProperty=nameWithType> method for each named resource to add to the file.</span></span> <span data-ttu-id="d341e-188">Zasób może być ciągiem, obiektem lub kolekcją danych binarnych (tablicą bajtową).</span><span class="sxs-lookup"><span data-stu-id="d341e-188">The resource can be a string, an object, or a collection of binary data (a byte array).</span></span>

3. <span data-ttu-id="d341e-189">Wywołaj <xref:System.Resources.ResourceWriter.Close%2A?displayProperty=nameWithType> metodę, aby zapisać zasoby do pliku i zamknąć <xref:System.Resources.ResourceWriter> obiekt.</span><span class="sxs-lookup"><span data-stu-id="d341e-189">Call the <xref:System.Resources.ResourceWriter.Close%2A?displayProperty=nameWithType> method to write the resources to the file and to close the <xref:System.Resources.ResourceWriter> object.</span></span>

> [!NOTE]
> <span data-ttu-id="d341e-190">Nie należy używać plików zasobów do przechowywania haseł, informacji o zabezpieczeniach ani danych prywatnych.</span><span class="sxs-lookup"><span data-stu-id="d341e-190">Do not use resource files to store passwords, security-sensitive information, or private data.</span></span>

 <span data-ttu-id="d341e-191">Poniższy przykład programowo tworzy plik resources o nazwie CarResources. resources, który przechowuje sześć ciągów, ikonę i dwa obiekty zdefiniowane przez aplikację (dwa `Automobile` obiekty).</span><span class="sxs-lookup"><span data-stu-id="d341e-191">The following example programmatically creates a .resources file named CarResources.resources that stores six strings, an icon, and two application-defined objects (two `Automobile` objects).</span></span> <span data-ttu-id="d341e-192">`Automobile`Klasa, która jest zdefiniowana i tworzona w przykładzie, jest oznaczona przy użyciu <xref:System.SerializableAttribute> atrybutu, co umożliwia jego utrwalanie przez program formatujący serializacji binarnej.</span><span class="sxs-lookup"><span data-stu-id="d341e-192">The `Automobile` class, which is defined and instantiated in the example, is tagged with the <xref:System.SerializableAttribute> attribute, which allows it to be persisted by the binary serialization formatter.</span></span>

 [!code-csharp[Conceptual.Resources.Resources#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.resources.resources/cs/resources1.cs#1)]
 [!code-vb[Conceptual.Resources.Resources#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.resources.resources/vb/resources1.vb#1)]

 <span data-ttu-id="d341e-193">Po utworzeniu pliku Resources można go osadzić w pliku wykonywalnym lub bibliotece środowiska uruchomieniowego, dołączając przełącznik kompilatora języka `/resource` lub osadzić go w zestawie satelitarnym za pomocą [konsolidatora zestawu (Al.exe)](../tools/al-exe-assembly-linker.md).</span><span class="sxs-lookup"><span data-stu-id="d341e-193">After you create the .resources file, you can embed it in a run-time executable or library by including the language compiler's `/resource` switch, or embed it in a satellite assembly by using [Assembly Linker (Al.exe)](../tools/al-exe-assembly-linker.md).</span></span>

<a name="VSResFiles"></a>

## <a name="resource-files-in-visual-studio"></a><span data-ttu-id="d341e-194">Pliki zasobów w programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d341e-194">Resource files in Visual Studio</span></span>

<span data-ttu-id="d341e-195">Po dodaniu pliku zasobów do projektu programu [Visual Studio](https://visualstudio.microsoft.com/vs/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link) program Visual Studio tworzy plik resx w katalogu projektu.</span><span class="sxs-lookup"><span data-stu-id="d341e-195">When you add a resource file to your [Visual Studio](https://visualstudio.microsoft.com/vs/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link) project, Visual Studio creates a .resx file in the project directory.</span></span> <span data-ttu-id="d341e-196">Program Visual Studio udostępnia edytory zasobów, które umożliwiają dodawanie ciągów, obrazów i obiektów binarnych.</span><span class="sxs-lookup"><span data-stu-id="d341e-196">Visual Studio provides resource editors that enable you to add strings, images, and binary objects.</span></span> <span data-ttu-id="d341e-197">Ponieważ edytory są zaprojektowane do obsługi tylko danych statycznych, nie mogą być używane do przechowywania obiektów programistycznych; należy zapisać dane obiektu w pliku resx lub w pliku. resources programowo.</span><span class="sxs-lookup"><span data-stu-id="d341e-197">Because the editors are designed to handle static data only, they cannot be used to store programmatic objects; you must write object data to either a .resx file or to a .resources file programmatically.</span></span> <span data-ttu-id="d341e-198">Aby uzyskać więcej informacji, zobacz [Praca z plikami resx programowo](working-with-resx-files-programmatically.md) i [w sekcji zasoby w plikach. resources](creating-resource-files-for-desktop-apps.md#ResourcesFiles) .</span><span class="sxs-lookup"><span data-stu-id="d341e-198">For more information, see [Working with .resx Files Programmatically](working-with-resx-files-programmatically.md) and the [Resources in .resources Files](creating-resource-files-for-desktop-apps.md#ResourcesFiles) section.</span></span>

<span data-ttu-id="d341e-199">W przypadku dodawania zlokalizowanych zasobów nadaj im taką samą nazwę pliku głównego jak główny plik zasobów.</span><span class="sxs-lookup"><span data-stu-id="d341e-199">If you're adding localized resources, give them the same root file name as the main resource file.</span></span> <span data-ttu-id="d341e-200">Należy również wyznaczyć swoją kulturę w nazwie pliku.</span><span class="sxs-lookup"><span data-stu-id="d341e-200">You should also designate their culture in the file name.</span></span> <span data-ttu-id="d341e-201">Na przykład, jeśli dodasz plik zasobów o nazwie Resources. resx, możesz również utworzyć pliki zasobów o nazwie Resources. en-US. resx i Resources.fr-FR. resx, odpowiednio przechowując zlokalizowane zasoby dla kultur angielskiej (Stany Zjednoczone) i francuski (Francja).</span><span class="sxs-lookup"><span data-stu-id="d341e-201">For example, if you add a resource file named Resources.resx, you might also create resource files named Resources.en-US.resx and Resources.fr-FR.resx to hold localized resources for the English (United States) and French (France) cultures, respectively.</span></span> <span data-ttu-id="d341e-202">Należy również wyznaczyć domyślną kulturę aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d341e-202">You should also designate your application's default culture.</span></span> <span data-ttu-id="d341e-203">Jest to kultura, której zasoby są używane, jeśli nie można znaleźć zlokalizowanych zasobów dla określonej kultury.</span><span class="sxs-lookup"><span data-stu-id="d341e-203">This is the culture whose resources are used if no localized resources for a particular culture can be found.</span></span> <span data-ttu-id="d341e-204">Aby określić domyślną kulturę, w Eksplorator rozwiązań w programie Visual Studio kliknij prawym przyciskiem myszy nazwę projektu, wskaż polecenie aplikacja, kliknij pozycję **Informacje o zestawie** i wybierz odpowiedni język/kulturę na liście **języka neutralnego** .</span><span class="sxs-lookup"><span data-stu-id="d341e-204">To specify the default culture, in Solution Explorer in Visual Studio, right-click the project name, point to Application, click **Assembly Information**, and select the appropriate language/culture in the **Neutral language** list.</span></span>

<span data-ttu-id="d341e-205">W czasie kompilacji program Visual Studio najpierw konwertuje pliki resx w projekcie na pliki zasobów binarnych (. resources) i zapisuje je w podkatalogu katalogu *obj* projektu.</span><span class="sxs-lookup"><span data-stu-id="d341e-205">At compile time, Visual Studio first converts the .resx files in a project to binary resource (.resources) files and stores them in a subdirectory of the project's *obj* directory.</span></span> <span data-ttu-id="d341e-206">Program Visual Studio osadza wszystkie pliki zasobów, które nie zawierają zlokalizowanych zasobów w zestawie głównym, który jest generowany przez ten projekt.</span><span class="sxs-lookup"><span data-stu-id="d341e-206">Visual Studio embeds any resource files that do not contain localized resources in the main assembly that is generated by the project.</span></span> <span data-ttu-id="d341e-207">Jeśli jakiekolwiek pliki zasobów zawierają zlokalizowane zasoby, program Visual Studio osadzi je w oddzielnych zestawach satelickich dla każdej zlokalizowanej kultury.</span><span class="sxs-lookup"><span data-stu-id="d341e-207">If any resource files contain localized resources, Visual Studio embeds them in separate satellite assemblies for each localized culture.</span></span> <span data-ttu-id="d341e-208">Następnie przechowuje każdy zestaw satelicki w katalogu, którego nazwa odpowiada zlokalizowanej kulturze.</span><span class="sxs-lookup"><span data-stu-id="d341e-208">It then stores each satellite assembly in a directory whose name corresponds to the localized culture.</span></span> <span data-ttu-id="d341e-209">Na przykład zlokalizowane zasoby w języku angielskim (Stany Zjednoczone) są przechowywane w zestawie satelity w podkatalogu en-US.</span><span class="sxs-lookup"><span data-stu-id="d341e-209">For example, localized English (United States) resources are stored in a satellite assembly in the en-US subdirectory.</span></span>

## <a name="see-also"></a><span data-ttu-id="d341e-210">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="d341e-210">See also</span></span>

- <xref:System.Resources>
- [<span data-ttu-id="d341e-211">Zasoby w aplikacjach .NET</span><span class="sxs-lookup"><span data-stu-id="d341e-211">Resources in .NET Apps</span></span>](index.md)
- [<span data-ttu-id="d341e-212">Opakowanie i wdrażanie zasobów</span><span class="sxs-lookup"><span data-stu-id="d341e-212">Packaging and Deploying Resources</span></span>](packaging-and-deploying-resources-in-desktop-apps.md)
