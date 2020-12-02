---
title: 'Wprowadzenie do języka F # w Visual Studio dla komputerów Mac'
description: 'Dowiedz się, jak używać języka F # z Visual Studio dla komputerów Mac.'
ms.date: 07/03/2018
ms.openlocfilehash: d2ad24ad18bb31419b39508f2cf555c82fbe2e0b
ms.sourcegitcommit: 721c3e4bdbb1ea0bb420818ec944c538fe5c513a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/01/2020
ms.locfileid: "96437994"
---
# <a name="get-started-with-f-in-visual-studio-for-mac"></a><span data-ttu-id="6e83a-103">Wprowadzenie do języka F # w Visual Studio dla komputerów Mac</span><span class="sxs-lookup"><span data-stu-id="6e83a-103">Get started with F# in Visual Studio for Mac</span></span>

<span data-ttu-id="6e83a-104">Narzędzia F # i Visual F# są obsługiwane w Visual Studio dla komputerów Mac IDE.</span><span class="sxs-lookup"><span data-stu-id="6e83a-104">F# and the Visual F# tooling are supported in the Visual Studio for Mac IDE.</span></span> <span data-ttu-id="6e83a-105">Upewnij się, że [zainstalowano Visual Studio dla komputerów Mac](install-fsharp.md#install-f-with-visual-studio-for-mac).</span><span class="sxs-lookup"><span data-stu-id="6e83a-105">Ensure that you have [Visual Studio for Mac installed](install-fsharp.md#install-f-with-visual-studio-for-mac).</span></span>

## <a name="creating-a-console-application"></a><span data-ttu-id="6e83a-106">Tworzenie aplikacji konsolowej</span><span class="sxs-lookup"><span data-stu-id="6e83a-106">Creating a console application</span></span>

<span data-ttu-id="6e83a-107">Jednym z najpopularniejszych projektów w Visual Studio dla komputerów Mac jest Aplikacja konsolowa.</span><span class="sxs-lookup"><span data-stu-id="6e83a-107">One of the most basic projects in Visual Studio for Mac is the Console Application.</span></span>  <span data-ttu-id="6e83a-108">Oto odpowiednie czynności:</span><span class="sxs-lookup"><span data-stu-id="6e83a-108">Here's how to do it.</span></span>  <span data-ttu-id="6e83a-109">Gdy Visual Studio dla komputerów Mac jest otwarty:</span><span class="sxs-lookup"><span data-stu-id="6e83a-109">Once Visual Studio for Mac is open:</span></span>

1. <span data-ttu-id="6e83a-110">W menu **plik** wskaż polecenie **nowe rozwiązanie**.</span><span class="sxs-lookup"><span data-stu-id="6e83a-110">On the **File** menu, point to **New Solution**.</span></span>

2. <span data-ttu-id="6e83a-111">W oknie dialogowym Nowy projekt istnieją 2 różne szablony dla aplikacji konsolowej.</span><span class="sxs-lookup"><span data-stu-id="6e83a-111">In the New Project dialog, there are 2 different templates for Console Application.</span></span>  <span data-ttu-id="6e83a-112">Istnieje jedna pod innymi > .NET, która jest przeznaczona dla .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="6e83a-112">There is one under Other -> .NET which targets the .NET Framework.</span></span>  <span data-ttu-id="6e83a-113">Drugi szablon jest objęty aplikacją .NET Core->, która jest przeznaczona dla platformy .NET Core.</span><span class="sxs-lookup"><span data-stu-id="6e83a-113">The other template is under .NET Core -> App which targets .NET Core.</span></span>  <span data-ttu-id="6e83a-114">Każdy szablon powinien zadziałał na potrzeby tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="6e83a-114">Either template should work for the purpose of this article.</span></span>

3. <span data-ttu-id="6e83a-115">W obszarze aplikacja konsoli, w razie potrzeby zmień w języku C# na F #.</span><span class="sxs-lookup"><span data-stu-id="6e83a-115">Under console app, change C# to F# if needed.</span></span>  <span data-ttu-id="6e83a-116">Wybierz przycisk **dalej** , aby przejść do przodu!</span><span class="sxs-lookup"><span data-stu-id="6e83a-116">Choose the **Next** button to move forward!</span></span>  

4. <span data-ttu-id="6e83a-117">Nadaj projektowi nazwę, a następnie wybierz odpowiednie opcje dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6e83a-117">Give your project a name, and choose the options you want for the app.</span></span>  <span data-ttu-id="6e83a-118">Zwróć uwagę, że okienko podglądu z boku ekranu spowoduje wyświetlenie struktury katalogów, która zostanie utworzona na podstawie wybranych opcji.</span><span class="sxs-lookup"><span data-stu-id="6e83a-118">Notice, the preview pane to the side of the screen that will show the directory structure that will be created based on the options selected.</span></span>  

5. <span data-ttu-id="6e83a-119">Kliknij pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="6e83a-119">Click **Create**.</span></span>  <span data-ttu-id="6e83a-120">Powinien być teraz widoczny projekt F # w Eksplorator rozwiązań.</span><span class="sxs-lookup"><span data-stu-id="6e83a-120">You should now see an F# project in the Solution Explorer.</span></span>

## <a name="writing-your-code"></a><span data-ttu-id="6e83a-121">Pisanie kodu</span><span class="sxs-lookup"><span data-stu-id="6e83a-121">Writing your code</span></span>

<span data-ttu-id="6e83a-122">Zacznijmy od zapisania najpierw kodu.</span><span class="sxs-lookup"><span data-stu-id="6e83a-122">Let's get started by writing some code first.</span></span>  <span data-ttu-id="6e83a-123">Upewnij się, że `Program.fs` plik jest otwarty, a następnie zastąp jego zawartość następującym:</span><span class="sxs-lookup"><span data-stu-id="6e83a-123">Make sure that the `Program.fs` file is open, and then replace its contents with the following:</span></span>

[!code-fsharp[HelloSquare](~/samples/snippets/fsharp/getting-started/hello-square.fs)]

<span data-ttu-id="6e83a-124">W poprzednim przykładzie kodu zdefiniowano funkcję, `square` która przyjmuje dane wejściowe `x` i mnoży ją przez siebie.</span><span class="sxs-lookup"><span data-stu-id="6e83a-124">In the previous code sample, a function `square` has been defined which takes an input named `x` and multiplies it by itself.</span></span>  <span data-ttu-id="6e83a-125">Ponieważ F # używa [wnioskowania o typie](../language-reference/type-inference.md), `x` nie trzeba określać typu.</span><span class="sxs-lookup"><span data-stu-id="6e83a-125">Because F# uses [Type Inference](../language-reference/type-inference.md), the type of `x` doesn't need to be specified.</span></span>  <span data-ttu-id="6e83a-126">Kompilator F # rozumie typy, w których mnożenie jest prawidłowe i przypisuje typ na `x` podstawie sposobu `square` wywoływania.</span><span class="sxs-lookup"><span data-stu-id="6e83a-126">The F# compiler understands the types where multiplication is valid, and will assign a type to `x` based on how `square` is called.</span></span>  <span data-ttu-id="6e83a-127">Po umieszczeniu wskaźnika myszy na stronie `square` powinny zostać wyświetlone następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="6e83a-127">If you hover over `square`, you should see the following:</span></span>

```console
val square: x:int -> int
```

<span data-ttu-id="6e83a-128">Jest to element znany jako podpis typu funkcji.</span><span class="sxs-lookup"><span data-stu-id="6e83a-128">This is what is known as the function's type signature.</span></span>  <span data-ttu-id="6e83a-129">Można go odczytać w następujący sposób: "kwadrat jest funkcją, która przyjmuje liczbę całkowitą o nazwie x i tworzy liczbę całkowitą".</span><span class="sxs-lookup"><span data-stu-id="6e83a-129">It can be read like this: "Square is a function which takes an integer named x and produces an integer".</span></span>  <span data-ttu-id="6e83a-130">Należy zauważyć, że kompilator `square` nadał `int` teraz typ. jest to spowodowane tym, że mnożenie nie jest ogólne dla *wszystkich* typów, ale raczej jest ogólny w przypadku zamkniętego zestawu typów.</span><span class="sxs-lookup"><span data-stu-id="6e83a-130">Note that the compiler gave `square` the `int` type for now - this is because multiplication is not generic across *all* types, but rather is generic across a closed set of types.</span></span>  <span data-ttu-id="6e83a-131">Kompilator F # został pobrany `int` w tym momencie, ale dopasowuje podpis typu w przypadku wywołania `square` z innym typem danych wejściowych, na przykład `float` .</span><span class="sxs-lookup"><span data-stu-id="6e83a-131">The F# compiler picked `int` at this point, but it will adjust the type signature if you call `square` with a different input type, such as a `float`.</span></span>

<span data-ttu-id="6e83a-132">Inna funkcja, `main` ,, jest zdefiniowana z `EntryPoint` atrybutem do informowania kompilatora F # o tym, że wykonanie programu powinno się uruchomić.</span><span class="sxs-lookup"><span data-stu-id="6e83a-132">Another function, `main`, is defined, which is decorated with the `EntryPoint` attribute to tell the F# compiler that program execution should start there.</span></span>  <span data-ttu-id="6e83a-133">Ta sama Konwencja jest zgodna z innymi [językami programowania w stylu C](https://en.wikipedia.org/wiki/Entry_point#C_and_C.2B.2B), gdzie argumenty wiersza polecenia mogą być przekazane do tej funkcji i zwracany jest kod liczby całkowitej (zazwyczaj `0` ).</span><span class="sxs-lookup"><span data-stu-id="6e83a-133">It follows the same convention as other [C-style programming languages](https://en.wikipedia.org/wiki/Entry_point#C_and_C.2B.2B), where command-line arguments can be passed to this function, and an integer code is returned (typically `0`).</span></span>

<span data-ttu-id="6e83a-134">Jest to funkcja, która wywołuje `square` funkcję z argumentem `12` .</span><span class="sxs-lookup"><span data-stu-id="6e83a-134">It is in this function that we call the `square` function with an argument of `12`.</span></span>  <span data-ttu-id="6e83a-135">Kompilator F # następnie przypisuje typ `square` do `int -> int` (czyli funkcję, która przyjmuje `int` i tworzy `int` ).</span><span class="sxs-lookup"><span data-stu-id="6e83a-135">The F# compiler then assigns the type of `square` to be `int -> int` (that is, a function which takes an `int` and produces an `int`).</span></span>  <span data-ttu-id="6e83a-136">Wywołanie `printfn` jest sformatowaną funkcją drukowania, która używa ciągu formatu, podobnego do języków programowania w stylu C, parametrów, które odpowiadają określonym w ciągu formatu, a następnie drukuje wynik i nowy wiersz.</span><span class="sxs-lookup"><span data-stu-id="6e83a-136">The call to `printfn` is a formatted printing function which uses a format string, similar to C-style programming languages, parameters which correspond to those specified in the format string, and then prints the result and a new line.</span></span>

## <a name="running-your-code"></a><span data-ttu-id="6e83a-137">Uruchamianie kodu</span><span class="sxs-lookup"><span data-stu-id="6e83a-137">Running your code</span></span>

<span data-ttu-id="6e83a-138">Możesz uruchomić kod i zobaczyć wyniki, klikając polecenie **Uruchom** w menu najwyższego poziomu, a następnie **uruchamiając bez debugowania**.</span><span class="sxs-lookup"><span data-stu-id="6e83a-138">You can run the code and see results by clicking on **Run** from the top level menu and then **Start Without Debugging**.</span></span>  <span data-ttu-id="6e83a-139">Spowoduje to uruchomienie programu bez debugowania i umożliwi wyświetlenie wyników.</span><span class="sxs-lookup"><span data-stu-id="6e83a-139">This will run the program without debugging and allows you to see the results.</span></span>

<span data-ttu-id="6e83a-140">W oknie konsoli powinna zostać wyświetlona następująca wartość, która Visual Studio dla komputerów Mac zdjęte:</span><span class="sxs-lookup"><span data-stu-id="6e83a-140">You should now see the following printed to the console window that Visual Studio for Mac popped up:</span></span>

```console
12 squared is 144!
```

<span data-ttu-id="6e83a-141">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="6e83a-141">Congratulations!</span></span>  <span data-ttu-id="6e83a-142">Utworzono pierwszy projekt F # w Visual Studio dla komputerów Mac, napisanie funkcji języka F # spowodowało wydrukowanie wyników wywołania tej funkcji i uruchomienie projektu w celu wyświetlenia niektórych wyników.</span><span class="sxs-lookup"><span data-stu-id="6e83a-142">You've created your first F# project in Visual Studio for Mac, written an F# function printed the results of calling that function, and run the project to see some results.</span></span>

## <a name="using-f-interactive"></a><span data-ttu-id="6e83a-143">Używanie F# Interactive</span><span class="sxs-lookup"><span data-stu-id="6e83a-143">Using F# Interactive</span></span>

<span data-ttu-id="6e83a-144">Jedną z najlepszych funkcji narzędzi Visual F# w Visual Studio dla komputerów Mac jest okno F# Interactive.</span><span class="sxs-lookup"><span data-stu-id="6e83a-144">One of the best features of the Visual F# tooling in Visual Studio for Mac is the F# Interactive Window.</span></span>  <span data-ttu-id="6e83a-145">Umożliwia wysyłanie kodu do procesu, w którym można wywołać ten kod i interaktywnie zobaczyć wynik.</span><span class="sxs-lookup"><span data-stu-id="6e83a-145">It allows you to send code over to a process where you can call that code and see the result interactively.</span></span>

<span data-ttu-id="6e83a-146">Aby rozpocząć korzystanie z niego, zaznacz `square` funkcję zdefiniowaną w kodzie.</span><span class="sxs-lookup"><span data-stu-id="6e83a-146">To begin using it, highlight the `square` function defined in your code.</span></span>  <span data-ttu-id="6e83a-147">Następnie kliknij pozycję **Edytuj** w menu najwyższego poziomu.</span><span class="sxs-lookup"><span data-stu-id="6e83a-147">Next, click on **Edit** from the top level menu.</span></span>  <span data-ttu-id="6e83a-148">Następnie wybierz pozycję **Wyślij zaznaczenie do F# Interactive**.</span><span class="sxs-lookup"><span data-stu-id="6e83a-148">Next select **Send selection to F# Interactive**.</span></span>  <span data-ttu-id="6e83a-149">Spowoduje to wykonanie kodu w oknie F# Interactive.</span><span class="sxs-lookup"><span data-stu-id="6e83a-149">This executes the code in the F# Interactive Window.</span></span>  <span data-ttu-id="6e83a-150">Alternatywnie możesz kliknąć prawym przyciskiem myszy zaznaczenie i wybrać polecenie **Wyślij zaznaczenie do F# Interactive**.</span><span class="sxs-lookup"><span data-stu-id="6e83a-150">Alternatively, you can right click on the selection and choose **Send selection to F# Interactive**.</span></span>  <span data-ttu-id="6e83a-151">Powinno zostać wyświetlone okno F# Interactive z następującym w nim:</span><span class="sxs-lookup"><span data-stu-id="6e83a-151">You should see the F# Interactive Window appear with the following in it:</span></span>

```console
>

val square : x:int -> int

>
```

<span data-ttu-id="6e83a-152">Pokazuje to ten sam podpis funkcji dla `square` funkcji, która została wcześniej umieszczona po umieszczeniu wskaźnika myszy nad funkcją.</span><span class="sxs-lookup"><span data-stu-id="6e83a-152">This shows the same function signature for the `square` function, which you saw earlier when you hovered over the function.</span></span>  <span data-ttu-id="6e83a-153">Ponieważ `square` jest teraz zdefiniowany w procesie F# Interactive, można wywołać go z różnymi wartościami:</span><span class="sxs-lookup"><span data-stu-id="6e83a-153">Because `square` is now defined in the F# Interactive process, you can call it with different values:</span></span>

```console
> square 12;;
val it : int = 144
>square 13;;
val it : int = 169
```

<span data-ttu-id="6e83a-154">Wykonuje funkcję, wiąże wynik z nową nazwą `it` i wyświetla typ i wartość `it` .</span><span class="sxs-lookup"><span data-stu-id="6e83a-154">This executes the function, binds the result to a new name `it`, and displays the type and value of `it`.</span></span>  <span data-ttu-id="6e83a-155">Należy pamiętać, że każdy wiersz należy zamknąć za pomocą `;;` .</span><span class="sxs-lookup"><span data-stu-id="6e83a-155">Note that you must terminate each line with `;;`.</span></span>  <span data-ttu-id="6e83a-156">Jest to sposób, w jaki F# Interactive wie, gdy wywołanie funkcji zostało zakończone.</span><span class="sxs-lookup"><span data-stu-id="6e83a-156">This is how F# Interactive knows when your function call is finished.</span></span>  <span data-ttu-id="6e83a-157">Można także definiować nowe funkcje w F# Interactive:</span><span class="sxs-lookup"><span data-stu-id="6e83a-157">You can also define new functions in F# Interactive:</span></span>

```console
> let isOdd x = x % 2 <> 0;;

val isOdd : x:int -> bool

> isOdd 12;;
val it : bool = false
```

<span data-ttu-id="6e83a-158">Powyższe definiuje nową funkcję, `isOdd` która pobiera `int` i sprawdza, czy jest nieparzysta.</span><span class="sxs-lookup"><span data-stu-id="6e83a-158">The above defines a new function, `isOdd`, which takes an `int` and checks to see if it's odd!</span></span>  <span data-ttu-id="6e83a-159">Możesz wywołać tę funkcję, aby zobaczyć, co zwraca z innymi danymi wejściowymi.</span><span class="sxs-lookup"><span data-stu-id="6e83a-159">You can call this function to see what it returns with different inputs.</span></span>  <span data-ttu-id="6e83a-160">Można wywoływać funkcje w ramach wywołań funkcji:</span><span class="sxs-lookup"><span data-stu-id="6e83a-160">You can call functions within function calls:</span></span>

```console
> isOdd (square 15);;
val it : bool = true
```

<span data-ttu-id="6e83a-161">Można również użyć [operatora przekazywania potoków](../language-reference/symbol-and-operator-reference/index.md) , aby przekierować wartość do dwóch funkcji:</span><span class="sxs-lookup"><span data-stu-id="6e83a-161">You can also use the [pipe-forward operator](../language-reference/symbol-and-operator-reference/index.md) to pipeline the value into the two functions:</span></span>

```console
> 15 |> square |> isOdd;;
val it : bool = true
```

<span data-ttu-id="6e83a-162">Operator przekazujący przekazanie dalej i inne są omówione w kolejnych samouczkach.</span><span class="sxs-lookup"><span data-stu-id="6e83a-162">The pipe-forward operator, and more, are covered in later tutorials.</span></span>

<span data-ttu-id="6e83a-163">Jest to tylko możliwość wypróbowania innowacyjnego do tego, co można zrobić z F# Interactive.</span><span class="sxs-lookup"><span data-stu-id="6e83a-163">This is only a glimpse into what you can do with F# Interactive.</span></span>  <span data-ttu-id="6e83a-164">Aby dowiedzieć się więcej, zapoznaj się [z programowaniem interaktywnym przy użyciu języka F #](../tools/fsharp-interactive/index.md).</span><span class="sxs-lookup"><span data-stu-id="6e83a-164">To learn more, check out [Interactive Programming with F#](../tools/fsharp-interactive/index.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6e83a-165">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6e83a-165">Next steps</span></span>

<span data-ttu-id="6e83a-166">Jeśli jeszcze tego nie zrobiono, zapoznaj się [z przewodnikiem języka f #](../tour.md), który obejmuje niektóre podstawowe funkcje języka f #.</span><span class="sxs-lookup"><span data-stu-id="6e83a-166">If you haven't already, check out the [Tour of F#](../tour.md), which covers some of the core features of the F# language.</span></span>  <span data-ttu-id="6e83a-167">Udostępnimy przegląd niektórych możliwości języka F # i udostępniamy dużo przykładów kodu, które można skopiować do Visual Studio dla komputerów Mac i uruchamiać.</span><span class="sxs-lookup"><span data-stu-id="6e83a-167">It will give you an overview of some of the capabilities of F#, and provide ample code samples that you can copy into Visual Studio for Mac and run.</span></span>  <span data-ttu-id="6e83a-168">Istnieją również pewne doskonałe zasoby zewnętrzne, których można użyć w [przewodniku F #](../index.yml).</span><span class="sxs-lookup"><span data-stu-id="6e83a-168">There are also some great external resources you can use, showcased in the [F# Guide](../index.yml).</span></span>

## <a name="see-also"></a><span data-ttu-id="6e83a-169">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="6e83a-169">See also</span></span>

- [<span data-ttu-id="6e83a-170">Podręcznik języka F#</span><span class="sxs-lookup"><span data-stu-id="6e83a-170">F# guide</span></span>](../index.yml)
- [<span data-ttu-id="6e83a-171">Przewodnik po środowisku F#</span><span class="sxs-lookup"><span data-stu-id="6e83a-171">Tour of F#</span></span>](../tour.md)
- [<span data-ttu-id="6e83a-172">Materiały referencyjne dotyczące języka F#</span><span class="sxs-lookup"><span data-stu-id="6e83a-172">F# language reference</span></span>](../language-reference/index.md)
- [<span data-ttu-id="6e83a-173">Wnioskowanie o typie</span><span class="sxs-lookup"><span data-stu-id="6e83a-173">Type inference</span></span>](../language-reference/type-inference.md)
- [<span data-ttu-id="6e83a-174">Odwołanie do symbolu i operatora</span><span class="sxs-lookup"><span data-stu-id="6e83a-174">Symbol and operator reference</span></span>](../language-reference/symbol-and-operator-reference/index.md)
