---
title: Dokumentowanie kodu za pomocą komentarzy XML
description: Dowiedz się, jak udokumentować kod za pomocą komentarzy dokumentacji XML i generować plik dokumentacji XML w czasie kompilacji.
ms.date: 01/21/2020
ms.technology: csharp-fundamentals
ms.assetid: 8e75e317-4a55-45f2-a866-e76124171838
ms.openlocfilehash: 91de11c610ea17999dabff6d0552de9440f532e6
ms.sourcegitcommit: e7acba36517134238065e4d50bb4a1cfe47ebd06
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2020
ms.locfileid: "89465302"
---
# <a name="document-your-code-with-xml-comments"></a><span data-ttu-id="cd07e-103">Dokumentowanie kodu za pomocą komentarzy XML</span><span class="sxs-lookup"><span data-stu-id="cd07e-103">Document your code with XML comments</span></span>

<span data-ttu-id="cd07e-104">Komentarze dokumentacji XML są specjalnym rodzajem komentarza, który został dodany powyżej definicji dowolnego typu lub elementu członkowskiego zdefiniowanego przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="cd07e-104">XML documentation comments are a special kind of comment, added above the definition of any user-defined type or member.</span></span>
<span data-ttu-id="cd07e-105">Są one specyficzne, ponieważ mogą być przetwarzane przez kompilator w celu wygenerowania pliku dokumentacji XML w czasie kompilacji.</span><span class="sxs-lookup"><span data-stu-id="cd07e-105">They are special because they can be processed by the compiler to generate an XML documentation file at compile time.</span></span>
<span data-ttu-id="cd07e-106">Plik XML wygenerowany przez kompilator może być dystrybuowany wraz z zestawem .NET, dzięki czemu program Visual Studio i inne środowisk IDE mogą używać funkcji IntelliSense do wyświetlania szybkich informacji o typach lub elementach członkowskich.</span><span class="sxs-lookup"><span data-stu-id="cd07e-106">The compiler-generated XML file can be distributed alongside your .NET assembly so that Visual Studio and other IDEs can use IntelliSense to show quick information about types or members.</span></span> <span data-ttu-id="cd07e-107">Ponadto plik XML można uruchomić za pomocą narzędzi, takich jak [DocFX](https://dotnet.github.io/docfx/) i [Sandcastle](https://github.com/EWSoftware/SHFB) , aby generować witryny sieci Web dokumentacji interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="cd07e-107">Additionally, the XML file can be run through tools like [DocFX](https://dotnet.github.io/docfx/) and [Sandcastle](https://github.com/EWSoftware/SHFB) to generate API reference websites.</span></span>

<span data-ttu-id="cd07e-108">Komentarze dokumentacji XML, podobnie jak wszystkie inne komentarze, są ignorowane przez kompilator.</span><span class="sxs-lookup"><span data-stu-id="cd07e-108">XML documentation comments, like all other comments, are ignored by the compiler.</span></span>

<span data-ttu-id="cd07e-109">Plik XML można wygenerować w czasie kompilacji, wykonując jedną z następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="cd07e-109">You can generate the XML file at compile time by doing one of the following:</span></span>

- <span data-ttu-id="cd07e-110">Jeśli tworzysz aplikację przy użyciu platformy .NET Core z wiersza polecenia, możesz dodać `GenerateDocumentationFile` element do `<PropertyGroup>` sekcji pliku projektu. csproj.</span><span class="sxs-lookup"><span data-stu-id="cd07e-110">If you are developing an application with .NET Core from the command line, you can add a `GenerateDocumentationFile` element to the `<PropertyGroup>` section of your .csproj project file.</span></span> <span data-ttu-id="cd07e-111">Możesz również określić ścieżkę do pliku dokumentacji bezpośrednio przy użyciu [ `DocumentationFile` elementu](/visualstudio/msbuild/common-msbuild-project-properties).</span><span class="sxs-lookup"><span data-stu-id="cd07e-111">You can also specify the path to the documentation file directly using [`DocumentationFile` element](/visualstudio/msbuild/common-msbuild-project-properties).</span></span> <span data-ttu-id="cd07e-112">Poniższy przykład generuje plik XML w katalogu projektu z tą samą nazwą pliku głównego co zestaw:</span><span class="sxs-lookup"><span data-stu-id="cd07e-112">The following example generates an XML file in the project directory with the same root filename as the assembly:</span></span>

   ```xml
   <GenerateDocumentationFile>true</GenerateDocumentationFile>
   ```

   <span data-ttu-id="cd07e-113">Jest to równoważne z następującymi:</span><span class="sxs-lookup"><span data-stu-id="cd07e-113">This is equivalent to the following:</span></span>

   ```xml
   <DocumentationFile>bin\$(Configuration)\$(TargetFramework)\$(AssemblyName).xml</DocumentationFile>
   ```

- <span data-ttu-id="cd07e-114">Jeśli tworzysz aplikację przy użyciu programu Visual Studio, kliknij prawym przyciskiem myszy projekt i wybierz polecenie **Właściwości**.</span><span class="sxs-lookup"><span data-stu-id="cd07e-114">If you are developing an application using Visual Studio, right-click on the project and select **Properties**.</span></span> <span data-ttu-id="cd07e-115">W oknie dialogowym właściwości wybierz kartę **kompilacja** i sprawdź **plik dokumentacji XML**.</span><span class="sxs-lookup"><span data-stu-id="cd07e-115">In the properties dialog, select the **Build** tab, and check **XML documentation file**.</span></span> <span data-ttu-id="cd07e-116">Możesz również zmienić lokalizację, w której kompilator zapisuje plik.</span><span class="sxs-lookup"><span data-stu-id="cd07e-116">You can also change the location to which the compiler writes the file.</span></span>

- <span data-ttu-id="cd07e-117">Jeśli kompilujesz aplikację .NET z wiersza polecenia, Dodaj [opcję kompilatora-doc](language-reference/compiler-options/doc-compiler-option.md) podczas kompilowania.</span><span class="sxs-lookup"><span data-stu-id="cd07e-117">If you are compiling a .NET application from the command line, add the [-doc compiler option](language-reference/compiler-options/doc-compiler-option.md) when compiling.</span></span>  

<span data-ttu-id="cd07e-118">Komentarze dokumentacji XML używają potrójnych ukośników ( `///` ) i treści komentarzy w formacie XML.</span><span class="sxs-lookup"><span data-stu-id="cd07e-118">XML documentation comments use triple forward slashes (`///`) and an XML formatted comment body.</span></span> <span data-ttu-id="cd07e-119">Przykład:</span><span class="sxs-lookup"><span data-stu-id="cd07e-119">For example:</span></span>

[!code-csharp[XML Documentation Comment](../../samples/snippets/csharp/concepts/codedoc/xml-comment.cs)]

## <a name="walkthrough"></a><span data-ttu-id="cd07e-120">Przewodnik</span><span class="sxs-lookup"><span data-stu-id="cd07e-120">Walkthrough</span></span>

<span data-ttu-id="cd07e-121">Zapoznaj się z dokumentem bardzo podstawową bibliotekę matematyczną, aby ułatwić nowym deweloperom zrozumienie/współtworzenie i współdziałanie z innymi programistami.</span><span class="sxs-lookup"><span data-stu-id="cd07e-121">Let's walk through documenting a very basic math library to make it easy for new developers to understand/contribute and for third-party developers to use.</span></span>

<span data-ttu-id="cd07e-122">Oto kod dla prostej biblioteki matematycznej:</span><span class="sxs-lookup"><span data-stu-id="cd07e-122">Here's code for the simple math library:</span></span>

[!code-csharp[Sample Library](../../samples/snippets/csharp/concepts/codedoc/sample-library.cs)]

<span data-ttu-id="cd07e-123">Biblioteka Przykładowa obsługuje cztery główne operacje arytmetyczne ( `add` , `subtract` , `multiply` i `divide` ) w `int` przypadku `double` typów danych i.</span><span class="sxs-lookup"><span data-stu-id="cd07e-123">The sample library supports four major arithmetic operations (`add`, `subtract`, `multiply`, and `divide`) on `int` and `double` data types.</span></span>

<span data-ttu-id="cd07e-124">Teraz chcesz mieć możliwość utworzenia dokumentu odniesienia interfejsu API z kodu dla deweloperów innych firm, którzy korzystają z biblioteki, ale nie mają dostępu do kodu źródłowego.</span><span class="sxs-lookup"><span data-stu-id="cd07e-124">Now you want to be able to create an API reference document from your code for third-party developers who use your library but don't have access to the source code.</span></span>
<span data-ttu-id="cd07e-125">Jak wspomniano wcześniej Tagi dokumentacji XML, można użyć w tym celu.</span><span class="sxs-lookup"><span data-stu-id="cd07e-125">As mentioned earlier XML documentation tags can be used to achieve this.</span></span> <span data-ttu-id="cd07e-126">Teraz zostanie wprowadzony do standardowych tagów XML obsługiwanych przez kompilator języka C#.</span><span class="sxs-lookup"><span data-stu-id="cd07e-126">You will now be introduced to the standard XML tags the C# compiler supports.</span></span>

## \<summary>

<span data-ttu-id="cd07e-127">`<summary>`Tag dodaje krótkie informacje dotyczące typu lub składowej.</span><span class="sxs-lookup"><span data-stu-id="cd07e-127">The `<summary>` tag adds brief information about a type or member.</span></span>
<span data-ttu-id="cd07e-128">Pokażę swoje użycie przez dodanie go do `Math` definicji klasy i pierwszej `Add` metody.</span><span class="sxs-lookup"><span data-stu-id="cd07e-128">I'll demonstrate its use by adding it to the `Math` class definition and the first `Add` method.</span></span> <span data-ttu-id="cd07e-129">Śmiało, aby zastosować go do pozostałej części kodu.</span><span class="sxs-lookup"><span data-stu-id="cd07e-129">Feel free to apply it to the rest of your code.</span></span>

[!code-csharp[Summary Tag](~/samples/snippets/csharp/concepts/codedoc/summary-tag.cs)]

<span data-ttu-id="cd07e-130">`<summary>`Tag jest istotny i zalecamy dołączenie go, ponieważ jego zawartość jest podstawowym źródłem informacji o typie lub elemencie członkowskim w IntelliSense lub dokumencie odwołania API.</span><span class="sxs-lookup"><span data-stu-id="cd07e-130">The `<summary>` tag is important, and we recommend that you include it because its content is the primary source of type or member information in IntelliSense or an API reference document.</span></span>

## \<remarks>

<span data-ttu-id="cd07e-131">`<remarks>`Tag uzupełnia informacje o typach lub elementach członkowskich `<summary>` udostępnianych przez tag.</span><span class="sxs-lookup"><span data-stu-id="cd07e-131">The `<remarks>` tag supplements the information about types or members that the `<summary>` tag provides.</span></span> <span data-ttu-id="cd07e-132">W tym przykładzie wystarczy dodać go do klasy.</span><span class="sxs-lookup"><span data-stu-id="cd07e-132">In this example, you'll just add it to the class.</span></span>

[!code-csharp[Remarks Tag](~/samples/snippets/csharp/concepts/codedoc/remarks-tag.cs)]

## \<returns>

<span data-ttu-id="cd07e-133">`<returns>`Tag opisuje wartość zwracaną deklaracji metody.</span><span class="sxs-lookup"><span data-stu-id="cd07e-133">The `<returns>` tag describes the return value of a method declaration.</span></span>
<span data-ttu-id="cd07e-134">Tak jak wcześniej Poniższy przykład ilustruje `<returns>` tag w pierwszej `Add` metodzie.</span><span class="sxs-lookup"><span data-stu-id="cd07e-134">As before, the following example illustrates the `<returns>` tag on the first `Add` method.</span></span> <span data-ttu-id="cd07e-135">Można to zrobić w innych metodach.</span><span class="sxs-lookup"><span data-stu-id="cd07e-135">You can do the same on other methods.</span></span>

[!code-csharp[Returns Tag](~/samples/snippets/csharp/concepts/codedoc/returns-tag.cs)]

## \<value>

<span data-ttu-id="cd07e-136">`<value>`Tag jest podobny do `<returns>` znacznika, z tą różnicą, że jest używany do właściwości.</span><span class="sxs-lookup"><span data-stu-id="cd07e-136">The `<value>` tag is similar to the `<returns>` tag, except that you use it for properties.</span></span>
<span data-ttu-id="cd07e-137">Zakładając `Math` , że w bibliotece została wywołana właściwość statyczna `PI` , Oto jak używać tego tagu:</span><span class="sxs-lookup"><span data-stu-id="cd07e-137">Assuming your `Math` library had a static property called `PI`, here's how you'd use this tag:</span></span>

[!code-csharp[Value Tag](~/samples/snippets/csharp/concepts/codedoc/value-tag.cs)]

## \<example>

<span data-ttu-id="cd07e-138">Używasz znacznika, `<example>` Aby dołączyć przykład do dokumentacji XML.</span><span class="sxs-lookup"><span data-stu-id="cd07e-138">You use the `<example>` tag to include an example in your XML documentation.</span></span>
<span data-ttu-id="cd07e-139">Obejmuje to użycie znacznika podrzędnego `<code>` .</span><span class="sxs-lookup"><span data-stu-id="cd07e-139">This involves using the child `<code>` tag.</span></span>

[!code-csharp[Example Tag](~/samples/snippets/csharp/concepts/codedoc/example-tag.cs)]

<span data-ttu-id="cd07e-140">`code`Tag zachowuje podziały wierszy i wcięcia dla dłuższych przykładów.</span><span class="sxs-lookup"><span data-stu-id="cd07e-140">The `code` tag preserves line breaks and indentation for longer examples.</span></span>

## \<para>

<span data-ttu-id="cd07e-141">`<para>`Tag służy do formatowania zawartości w tagu nadrzędnym.</span><span class="sxs-lookup"><span data-stu-id="cd07e-141">You use the `<para>` tag to format the content within its parent tag.</span></span> <span data-ttu-id="cd07e-142">`<para>` jest zwykle używany wewnątrz tagu, takiego jak `<remarks>` lub `<returns>` , aby podzielić tekst na akapity.</span><span class="sxs-lookup"><span data-stu-id="cd07e-142">`<para>` is usually used inside a tag, such as `<remarks>` or `<returns>`, to divide text into paragraphs.</span></span>
<span data-ttu-id="cd07e-143">Można sformatować zawartość `<remarks>` tagu w definicji klasy.</span><span class="sxs-lookup"><span data-stu-id="cd07e-143">You can format the contents of the `<remarks>` tag for your class definition.</span></span>

[!code-csharp[Para Tag](~/samples/snippets/csharp/concepts/codedoc/para-tag.cs)]

## \<c>

<span data-ttu-id="cd07e-144">Nadal w temacie formatowania, używasz `<c>` znacznika do oznaczania części tekstu jako kodu.</span><span class="sxs-lookup"><span data-stu-id="cd07e-144">Still on the topic of formatting, you use the `<c>` tag for marking part of text as code.</span></span>
<span data-ttu-id="cd07e-145">Jest to takie samo, jak `<code>` tag, ale wbudowane.</span><span class="sxs-lookup"><span data-stu-id="cd07e-145">It's like the `<code>` tag but inline.</span></span> <span data-ttu-id="cd07e-146">Jest to przydatne, gdy chcesz pokazać przykładowy kod jako część zawartości znacznika.</span><span class="sxs-lookup"><span data-stu-id="cd07e-146">It's useful when you want to show a quick code example as part of a tag's content.</span></span>
<span data-ttu-id="cd07e-147">Zaktualizujmy dokumentację dla `Math` klasy.</span><span class="sxs-lookup"><span data-stu-id="cd07e-147">Let's update the documentation for the `Math` class.</span></span>

[!code-csharp[C Tag](~/samples/snippets/csharp/concepts/codedoc/c-tag.cs)]

## \<exception>

<span data-ttu-id="cd07e-148">Korzystając ze `<exception>` znacznika, poinformuj deweloperów, że metoda może zgłosić określone wyjątki.</span><span class="sxs-lookup"><span data-stu-id="cd07e-148">By using the `<exception>` tag, you let your developers know that a method can throw specific exceptions.</span></span>
<span data-ttu-id="cd07e-149">Patrząc na `Math` bibliotekę, można zobaczyć, że obie metody zgłaszają `Add` wyjątek w przypadku spełnienia określonego warunku.</span><span class="sxs-lookup"><span data-stu-id="cd07e-149">Looking at your `Math` library, you can see that both `Add` methods throw an exception if a certain condition is met.</span></span> <span data-ttu-id="cd07e-150">Chociaż nie jest to oczywiste, jest to, że `Divide` Metoda Integer zgłasza również, jeśli `b` parametr ma wartość zero.</span><span class="sxs-lookup"><span data-stu-id="cd07e-150">Not so obvious, though, is that integer `Divide` method throws as well if the `b` parameter is zero.</span></span> <span data-ttu-id="cd07e-151">Teraz Dodaj dokumentację wyjątku do tej metody.</span><span class="sxs-lookup"><span data-stu-id="cd07e-151">Now add exception documentation to this method.</span></span>

[!code-csharp[Exception Tag](~/samples/snippets/csharp/concepts/codedoc/exception-tag.cs)]

<span data-ttu-id="cd07e-152">Ten `cref` atrybut reprezentuje odwołanie do wyjątku, który jest dostępny w bieżącym środowisku kompilacji.</span><span class="sxs-lookup"><span data-stu-id="cd07e-152">The `cref` attribute represents a reference to an exception that is available from the current compilation environment.</span></span>
<span data-ttu-id="cd07e-153">Może to być dowolny typ zdefiniowany w projekcie lub przywoływanym zestawie.</span><span class="sxs-lookup"><span data-stu-id="cd07e-153">This can be any type defined in the project or a referenced assembly.</span></span> <span data-ttu-id="cd07e-154">Kompilator wyświetli ostrzeżenie, jeśli nie można rozpoznać jego wartości.</span><span class="sxs-lookup"><span data-stu-id="cd07e-154">The compiler will issue a warning if its value cannot be resolved.</span></span>

## \<see>

<span data-ttu-id="cd07e-155">`<see>`Tag umożliwia utworzenie linku kliknięcia do strony dokumentacji dla innego elementu kodu.</span><span class="sxs-lookup"><span data-stu-id="cd07e-155">The `<see>` tag lets you create a clickable link to a documentation page for another code element.</span></span> <span data-ttu-id="cd07e-156">W następnym przykładzie utworzymy link do kliknięcia między tymi dwoma `Add` metodami.</span><span class="sxs-lookup"><span data-stu-id="cd07e-156">In our next example, we'll create a clickable link between the two `Add` methods.</span></span>

[!code-csharp[See Tag](~/samples/snippets/csharp/concepts/codedoc/see-tag.cs)]

<span data-ttu-id="cd07e-157">`cref`Jest to **wymagany** atrybut, który reprezentuje odwołanie do typu lub jego elementu członkowskiego, który jest dostępny w bieżącym środowisku kompilacji.</span><span class="sxs-lookup"><span data-stu-id="cd07e-157">The `cref` is a **required** attribute that represents a reference to a type or its member that is available from the current compilation environment.</span></span>
<span data-ttu-id="cd07e-158">Może to być dowolny typ zdefiniowany w projekcie lub przywoływanym zestawie.</span><span class="sxs-lookup"><span data-stu-id="cd07e-158">This can be any type defined in the project or a referenced assembly.</span></span>

## \<seealso>

<span data-ttu-id="cd07e-159">Używasz `<seealso>` znacznika w taki sam sposób jak `<see>` tag.</span><span class="sxs-lookup"><span data-stu-id="cd07e-159">You use the `<seealso>` tag in the same way you do the `<see>` tag.</span></span> <span data-ttu-id="cd07e-160">Jedyną różnicą jest to, że jej zawartość jest zwykle umieszczana w sekcji "Zobacz też".</span><span class="sxs-lookup"><span data-stu-id="cd07e-160">The only difference is that its content is typically placed in a "See Also" section.</span></span> <span data-ttu-id="cd07e-161">Tutaj dodamy `seealso` znacznik metody całkowitej, `Add` Aby odwołać się do innych metod w klasie, która akceptuje parametry całkowite:</span><span class="sxs-lookup"><span data-stu-id="cd07e-161">Here we'll add a `seealso` tag on the integer `Add` method to reference other methods in the class that accept integer parameters:</span></span>

[!code-csharp[Seealso Tag](~/samples/snippets/csharp/concepts/codedoc/seealso-tag.cs)]

<span data-ttu-id="cd07e-162">Ten `cref` atrybut reprezentuje odwołanie do typu lub jego elementu członkowskiego, który jest dostępny w bieżącym środowisku kompilacji.</span><span class="sxs-lookup"><span data-stu-id="cd07e-162">The `cref` attribute represents a reference to a type or its member that is available from the current compilation environment.</span></span>
<span data-ttu-id="cd07e-163">Może to być dowolny typ zdefiniowany w projekcie lub przywoływanym zestawie.</span><span class="sxs-lookup"><span data-stu-id="cd07e-163">This can be any type defined in the project or a referenced assembly.</span></span>

## \<param>

<span data-ttu-id="cd07e-164">`<param>`Tag służy do opisywania parametrów metody.</span><span class="sxs-lookup"><span data-stu-id="cd07e-164">You use the `<param>` tag to describe a method's parameters.</span></span> <span data-ttu-id="cd07e-165">Oto przykład na potrzeby podwójnej `Add` metody: parametr opisany w opisie jest określony w **wymaganym** `name` atrybucie.</span><span class="sxs-lookup"><span data-stu-id="cd07e-165">Here's an example on the double `Add` method: The parameter the tag describes is specified in the **required** `name` attribute.</span></span>

[!code-csharp[Param Tag](~/samples/snippets/csharp/concepts/codedoc/param-tag.cs)]

## \<typeparam>

<span data-ttu-id="cd07e-166">Używasz `<typeparam>` znacznika podobnie jak tag, `<param>` ale dla typu ogólnego lub deklaracji metody, aby opisać parametr generyczny.</span><span class="sxs-lookup"><span data-stu-id="cd07e-166">You use `<typeparam>` tag just like the `<param>` tag but for generic type or method declarations to describe a generic parameter.</span></span>
<span data-ttu-id="cd07e-167">Dodaj szybką metodę rodzajową do `Math` klasy, aby sprawdzić, czy jedna ilość jest większa niż inna.</span><span class="sxs-lookup"><span data-stu-id="cd07e-167">Add a quick generic method to your `Math` class to check if one quantity is greater than another.</span></span>

[!code-csharp[Typeparam Tag](~/samples/snippets/csharp/concepts/codedoc/typeparam-tag.cs)]

## \<paramref>

<span data-ttu-id="cd07e-168">Czasami może być w środku opisującym opisywanie metody, która może być `<summary>` tagiem, i można utworzyć odwołanie do parametru.</span><span class="sxs-lookup"><span data-stu-id="cd07e-168">Sometimes you might be in the middle of describing what a method does in what could be a `<summary>` tag, and you might want to make a reference to a parameter.</span></span> <span data-ttu-id="cd07e-169">`<paramref>`Ten tag jest świetny dla samego siebie.</span><span class="sxs-lookup"><span data-stu-id="cd07e-169">The `<paramref>` tag is great for just this.</span></span> <span data-ttu-id="cd07e-170">Zaktualizujmy podsumowanie naszej metody opartej na podwójnej precyzji `Add` .</span><span class="sxs-lookup"><span data-stu-id="cd07e-170">Let's update the summary of our double based `Add` method.</span></span> <span data-ttu-id="cd07e-171">Podobnie jak `<param>` tag, nazwa parametru jest określona w **wymaganym** `name` atrybucie.</span><span class="sxs-lookup"><span data-stu-id="cd07e-171">Like the `<param>` tag, the parameter name is specified in the **required** `name` attribute.</span></span>

[!code-csharp[Paramref Tag](~/samples/snippets/csharp/concepts/codedoc/paramref-tag.cs)]

## \<typeparamref>

<span data-ttu-id="cd07e-172">Używasz `<typeparamref>` znacznika podobnie jak tag, `<paramref>` ale dla typu ogólnego lub deklaracji metody, aby opisać parametr generyczny.</span><span class="sxs-lookup"><span data-stu-id="cd07e-172">You use `<typeparamref>` tag just like the `<paramref>` tag but for generic type or method declarations to describe a generic parameter.</span></span>
<span data-ttu-id="cd07e-173">Możesz użyć tej samej metody generycznej, która została wcześniej utworzona.</span><span class="sxs-lookup"><span data-stu-id="cd07e-173">You can use the same generic method you previously created.</span></span>

[!code-csharp[Typeparamref Tag](~/samples/snippets/csharp/concepts/codedoc/typeparamref-tag.cs)]

## \<list>

<span data-ttu-id="cd07e-174">`<list>`Tag służy do formatowania informacji dokumentacji jako listy uporządkowanej, listy nieuporządkowanej lub tabeli.</span><span class="sxs-lookup"><span data-stu-id="cd07e-174">You use the `<list>` tag to format documentation information as an ordered list, unordered list, or table.</span></span> <span data-ttu-id="cd07e-175">Utwórz nieuporządkowaną listę każdej operacji matematycznej `Math` obsługiwanej przez bibliotekę.</span><span class="sxs-lookup"><span data-stu-id="cd07e-175">Make an unordered list of every math operation your `Math` library supports.</span></span>

[!code-csharp[List Tag](~/samples/snippets/csharp/concepts/codedoc/list-tag.cs)]

<span data-ttu-id="cd07e-176">Można utworzyć uporządkowaną listę lub tabelę, zmieniając `type` odpowiednio atrybut na `number` lub `table` .</span><span class="sxs-lookup"><span data-stu-id="cd07e-176">You can make an ordered list or table by changing the `type` attribute to `number` or `table`, respectively.</span></span>

## \<inheritdoc>

<span data-ttu-id="cd07e-177">Możesz użyć `<inheritdoc>` znacznika, aby odziedziczyć Komentarze XML z klas bazowych, interfejsów i podobnych metod.</span><span class="sxs-lookup"><span data-stu-id="cd07e-177">You can use the `<inheritdoc>` tag to inherit XML comments from base classes, interfaces, and similar methods.</span></span> <span data-ttu-id="cd07e-178">Eliminuje to niechciane kopiowanie i wklejanie zduplikowanych komentarzy XML i automatycznie synchronizuje komentarze XML.</span><span class="sxs-lookup"><span data-stu-id="cd07e-178">This eliminates unwanted copying and pasting of duplicate XML comments and automatically keeps XML comments synchronized.</span></span>

[!code-csharp-interactive[InheritDoc Tag](~/samples/snippets/csharp/concepts/codedoc/inheritdoc-tag.cs)]

### <a name="put-it-all-together"></a><span data-ttu-id="cd07e-179">Zebranie wszystkich elementów</span><span class="sxs-lookup"><span data-stu-id="cd07e-179">Put it all together</span></span>

<span data-ttu-id="cd07e-180">Jeśli wykonano ten samouczek i zastosowano znaczniki do kodu w razie potrzeby, kod powinien teraz wyglądać podobnie do poniższego:</span><span class="sxs-lookup"><span data-stu-id="cd07e-180">If you've followed this tutorial and applied the tags to your code where necessary, your code should now look similar to the following:</span></span>

[!code-csharp[Tagged Library](~/samples/snippets/csharp/concepts/codedoc/tagged-library.cs)]

<span data-ttu-id="cd07e-181">Z poziomu kodu można wygenerować szczegółową witrynę sieci Web, która została ukończona z kliknięciami odwołania krzyżowego.</span><span class="sxs-lookup"><span data-stu-id="cd07e-181">From your code, you can generate a detailed documentation website complete with clickable cross-references.</span></span> <span data-ttu-id="cd07e-182">Ale nastąpiło inne zagadnienie: Twój kod stał się trudno odczytać.</span><span class="sxs-lookup"><span data-stu-id="cd07e-182">But you're faced with another problem: your code has become hard to read.</span></span>
<span data-ttu-id="cd07e-183">Istnieje dużo informacji do przesiania przez to, że jest to okropnej dla każdego dewelopera, który chce współtworzyć ten kod.</span><span class="sxs-lookup"><span data-stu-id="cd07e-183">There's so much information to sift through that this is going to be a nightmare for any developer who wants to contribute to this code.</span></span>
<span data-ttu-id="cd07e-184">Thankfully istnieje tag XML, który może pomóc Ci w poradzić sobie z:</span><span class="sxs-lookup"><span data-stu-id="cd07e-184">Thankfully there's an XML tag that can help you deal with this:</span></span>

## \<include>

<span data-ttu-id="cd07e-185">`<include>`Tag umożliwia odwoływanie się do komentarzy w osobnym pliku XML, który opisuje typy i elementy członkowskie w kodzie źródłowym, zamiast umieszczania komentarzy do dokumentacji bezpośrednio w pliku kodu źródłowego.</span><span class="sxs-lookup"><span data-stu-id="cd07e-185">The `<include>` tag lets you refer to comments in a separate XML file that describe the types and members in your source code, as opposed to placing documentation comments directly in your source code file.</span></span>

<span data-ttu-id="cd07e-186">Teraz można przenieść wszystkie tagi XML do oddzielnego pliku XML o nazwie `docs.xml` .</span><span class="sxs-lookup"><span data-stu-id="cd07e-186">Now you're going to move all your XML tags into a separate XML file named `docs.xml`.</span></span> <span data-ttu-id="cd07e-187">Możesz nawiązać dowolną nazwę pliku.</span><span class="sxs-lookup"><span data-stu-id="cd07e-187">Feel free to name the file whatever you want.</span></span>

[!code-xml[Sample XML](~/samples/snippets/csharp/concepts/codedoc/include.xml)]

<span data-ttu-id="cd07e-188">W powyższym kodzie XML komentarze dokumentacji każdego członka są wyświetlane bezpośrednio wewnątrz tagu o nazwie po tym, co robią.</span><span class="sxs-lookup"><span data-stu-id="cd07e-188">In the above XML, each member's documentation comments appear directly inside a tag named after what they do.</span></span> <span data-ttu-id="cd07e-189">Możesz wybrać własną strategię.</span><span class="sxs-lookup"><span data-stu-id="cd07e-189">You can choose your own strategy.</span></span>
<span data-ttu-id="cd07e-190">Teraz, gdy masz Komentarze XML w osobnym pliku, zobaczmy, jak kod może być bardziej czytelny przy użyciu `<include>` tagu:</span><span class="sxs-lookup"><span data-stu-id="cd07e-190">Now that you have your XML comments in a separate file, let's see how your code can be made more readable by using the `<include>` tag:</span></span>

[!code-csharp[Include Tag](~/samples/snippets/csharp/concepts/codedoc/include-tag.cs)]

<span data-ttu-id="cd07e-191">Jest to możliwe: kod jest z powrotem odczytywany, a informacje o dokumentacji nie zostały utracone.</span><span class="sxs-lookup"><span data-stu-id="cd07e-191">And there you have it: our code is back to being readable, and no documentation information has been lost.</span></span>

<span data-ttu-id="cd07e-192">Ten `file` atrybut reprezentuje nazwę pliku XML zawierającego dokumentację.</span><span class="sxs-lookup"><span data-stu-id="cd07e-192">The `file` attribute represents the name of the XML file containing the documentation.</span></span>

<span data-ttu-id="cd07e-193">Ten `path` atrybut reprezentuje zapytanie [XPath](../standard/data/xml/xpath-queries-and-namespaces.md) do elementu `tag name` obecnego w określonym `file` .</span><span class="sxs-lookup"><span data-stu-id="cd07e-193">The `path` attribute represents an [XPath](../standard/data/xml/xpath-queries-and-namespaces.md) query to the `tag name` present in the specified `file`.</span></span>

<span data-ttu-id="cd07e-194">Ten `name` atrybut reprezentuje specyfikator nazwy w tagu, który poprzedza Komentarze.</span><span class="sxs-lookup"><span data-stu-id="cd07e-194">The `name` attribute represents the name specifier in the tag that precedes the comments.</span></span>

<span data-ttu-id="cd07e-195">`id`Atrybut, który może być użyty zamiast `name` , reprezentuje identyfikator tagu, który poprzedza Komentarze.</span><span class="sxs-lookup"><span data-stu-id="cd07e-195">The `id` attribute, which can be used in place of `name`, represents the ID for the tag that precedes the comments.</span></span>

### <a name="user-defined-tags"></a><span data-ttu-id="cd07e-196">Tagi zdefiniowane przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="cd07e-196">User-defined tags</span></span>

<span data-ttu-id="cd07e-197">Wszystkie Tagi podane powyżej reprezentują te, które są rozpoznawane przez kompilator języka C#.</span><span class="sxs-lookup"><span data-stu-id="cd07e-197">All the tags outlined above represent those that are recognized by the C# compiler.</span></span> <span data-ttu-id="cd07e-198">Jednak użytkownik może definiować własne znaczniki.</span><span class="sxs-lookup"><span data-stu-id="cd07e-198">However, a user is free to define their own tags.</span></span>
<span data-ttu-id="cd07e-199">Narzędzia takie jak Sandcastle zapewniają obsługę dodatkowych tagów, takich jak [\<event>](https://ewsoftware.github.io/XMLCommentsGuide/html/81bf7ad3-45dc-452f-90d5-87ce2494a182.htm) i [\<note>](https://ewsoftware.github.io/XMLCommentsGuide/html/4302a60f-e4f4-4b8d-a451-5f453c4ebd46.htm) , a nawet obsługują [dokumentowanie przestrzeni nazw](https://ewsoftware.github.io/XMLCommentsGuide/html/BD91FAD4-188D-4697-A654-7C07FD47EF31.htm).</span><span class="sxs-lookup"><span data-stu-id="cd07e-199">Tools like Sandcastle bring support for extra tags like [\<event>](https://ewsoftware.github.io/XMLCommentsGuide/html/81bf7ad3-45dc-452f-90d5-87ce2494a182.htm) and [\<note>](https://ewsoftware.github.io/XMLCommentsGuide/html/4302a60f-e4f4-4b8d-a451-5f453c4ebd46.htm), and even support [documenting namespaces](https://ewsoftware.github.io/XMLCommentsGuide/html/BD91FAD4-188D-4697-A654-7C07FD47EF31.htm).</span></span>
<span data-ttu-id="cd07e-200">Niestandardowe i wewnętrzne narzędzia do generowania dokumentacji mogą również być używane ze znacznikami standardowymi i można obsługiwać wiele formatów wyjściowych z formatu HTML do pliku PDF.</span><span class="sxs-lookup"><span data-stu-id="cd07e-200">Custom or in-house documentation generation tools can also be used with the standard tags and multiple output formats from HTML to PDF can be supported.</span></span>

## <a name="recommendations"></a><span data-ttu-id="cd07e-201">Zalecenia</span><span class="sxs-lookup"><span data-stu-id="cd07e-201">Recommendations</span></span>

<span data-ttu-id="cd07e-202">Dokumentowanie kodu jest zalecane z wielu powodów.</span><span class="sxs-lookup"><span data-stu-id="cd07e-202">Documenting code is recommended for many reasons.</span></span> <span data-ttu-id="cd07e-203">Poniżej przedstawiono niektóre najlepsze rozwiązania, ogólne scenariusze przypadków użycia i informacje, które należy znać w przypadku używania tagów dokumentacji XML w kodzie C#.</span><span class="sxs-lookup"><span data-stu-id="cd07e-203">What follows are some best practices, general use case scenarios, and things that you should know when using XML documentation tags in your C# code.</span></span>

- <span data-ttu-id="cd07e-204">Ze względu na spójność wszystkich publicznie widocznych typów i ich członków należy udokumentować.</span><span class="sxs-lookup"><span data-stu-id="cd07e-204">For the sake of consistency, all publicly visible types and their members should be documented.</span></span> <span data-ttu-id="cd07e-205">Jeśli to konieczne, zrób wszystko.</span><span class="sxs-lookup"><span data-stu-id="cd07e-205">If you must do it, do it all.</span></span>
- <span data-ttu-id="cd07e-206">Prywatne elementy członkowskie mogą być również udokumentowane przy użyciu komentarzy XML.</span><span class="sxs-lookup"><span data-stu-id="cd07e-206">Private members can also be documented using XML comments.</span></span> <span data-ttu-id="cd07e-207">Jednak spowoduje to uwidocznienie wewnętrznej (potencjalnie poufnej) pracy biblioteki.</span><span class="sxs-lookup"><span data-stu-id="cd07e-207">However, this exposes the inner (potentially confidential) workings of your library.</span></span>
- <span data-ttu-id="cd07e-208">W przypadku braku systemu operacyjnego typy i ich elementy członkowskie powinny mieć `<summary>` tag, ponieważ jego zawartość jest wymagana przez funkcję IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="cd07e-208">At a bare minimum, types and their members should have a `<summary>` tag because its content is needed for IntelliSense.</span></span>
- <span data-ttu-id="cd07e-209">Tekst dokumentacji należy napisać przy użyciu kompletnych zdań kończących się pełnym zatrzymywaniem.</span><span class="sxs-lookup"><span data-stu-id="cd07e-209">Documentation text should be written using complete sentences ending with full stops.</span></span>
- <span data-ttu-id="cd07e-210">Klasy częściowe są w pełni obsługiwane, a informacje o dokumentacji są łączone w jeden wpis dla tego typu.</span><span class="sxs-lookup"><span data-stu-id="cd07e-210">Partial classes are fully supported, and documentation information will be concatenated into a single entry for that type.</span></span>
- <span data-ttu-id="cd07e-211">Kompilator weryfikuje składnię `<exception>` `<include>` tagów,, `<param>` ,, `<see>` `<seealso>` i `<typeparam>` .</span><span class="sxs-lookup"><span data-stu-id="cd07e-211">The compiler verifies the syntax of the `<exception>`, `<include>`, `<param>`, `<see>`, `<seealso>`, and `<typeparam>` tags.</span></span>
- <span data-ttu-id="cd07e-212">Kompilator sprawdza poprawność parametrów zawierających ścieżki plików i odwołania do innych części kodu.</span><span class="sxs-lookup"><span data-stu-id="cd07e-212">The compiler validates the parameters that contain file paths and references to other parts of the code.</span></span>

## <a name="see-also"></a><span data-ttu-id="cd07e-213">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="cd07e-213">See also</span></span>

- [<span data-ttu-id="cd07e-214">Komentarze dokumentacji XML (Przewodnik programowania w języku C#)</span><span class="sxs-lookup"><span data-stu-id="cd07e-214">XML Documentation Comments (C# Programming Guide)</span></span>](programming-guide/xmldoc/index.md)
- [<span data-ttu-id="cd07e-215">Znaczniki zalecane dla komentarzy do dokumentacji (Przewodnik programowania w języku C#)</span><span class="sxs-lookup"><span data-stu-id="cd07e-215">Recommended Tags for Documentation Comments (C# Programming Guide)</span></span>](programming-guide/xmldoc/recommended-tags-for-documentation-comments.md)
