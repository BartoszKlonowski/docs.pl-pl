---
title: Projektowanie przy użyciu typów referencyjnych dopuszczających wartość null
description: Ten zaawansowany samouczek zawiera wprowadzenie do typów referencyjnych dopuszczających wartość null. Dowiesz się, w jaki sposób projekt zostanie zastosowany, gdy wartości odniesienia mogą mieć wartość null, i że kompilator wymusi, gdy nie mogą mieć wartości null.
ms.date: 02/19/2019
ms.technology: csharp-null-safety
ms.custom: mvc
ms.openlocfilehash: 70e6a7a906bc9a35918cf3e26c3e23bd0cfdafde
ms.sourcegitcommit: a8a205034eeffc7c3e1bdd6f506a75b0f7099ebf
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2020
ms.locfileid: "91755853"
---
# <a name="tutorial-express-your-design-intent-more-clearly-with-nullable-and-non-nullable-reference-types"></a><span data-ttu-id="3790a-104">Samouczek: wyraźny cel projektowania dokładniej z typami referencyjnymi nullable i niedopuszczających wartości null</span><span class="sxs-lookup"><span data-stu-id="3790a-104">Tutorial: Express your design intent more clearly with nullable and non-nullable reference types</span></span>

<span data-ttu-id="3790a-105">W języku C# 8,0 wprowadzono wartości [null typów referencyjnych](../nullable-references.md), które uzupełniają typy odwołań w taki sam sposób, jak typy wartości dopełnień.</span><span class="sxs-lookup"><span data-stu-id="3790a-105">C# 8.0 introduces [nullable reference types](../nullable-references.md), which complement reference types the same way nullable value types complement value types.</span></span> <span data-ttu-id="3790a-106">Należy zadeklarować zmienną jako **typ referencyjny dopuszczający wartość null** poprzez dołączenie `?` do typu.</span><span class="sxs-lookup"><span data-stu-id="3790a-106">You declare a variable to be a **nullable reference type** by appending a `?` to the type.</span></span> <span data-ttu-id="3790a-107">Na przykład `string?` reprezentuje wartość null `string` .</span><span class="sxs-lookup"><span data-stu-id="3790a-107">For example, `string?` represents a nullable `string`.</span></span> <span data-ttu-id="3790a-108">Możesz użyć tych nowych typów, aby dokładniej wyznaczać intencje projektowania: niektóre zmienne *muszą zawsze mieć wartość*, inne *mogą nie mieć wartości*.</span><span class="sxs-lookup"><span data-stu-id="3790a-108">You can use these new types to more clearly express your design intent: some variables *must always have a value*, others *may be missing a value*.</span></span>

<span data-ttu-id="3790a-109">Z tego samouczka dowiesz się, jak wykonywać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="3790a-109">In this tutorial, you'll learn how to:</span></span>

> [!div class="checklist"]
>
> - <span data-ttu-id="3790a-110">Uwzględnianie typów referencyjnych dopuszczających wartości null i niedopuszczających wartości null do Twoich projektów</span><span class="sxs-lookup"><span data-stu-id="3790a-110">Incorporate nullable and non-nullable reference types into your designs</span></span>
> - <span data-ttu-id="3790a-111">Włącz kontrolę typu odwołania do wartości null w całym kodzie.</span><span class="sxs-lookup"><span data-stu-id="3790a-111">Enable nullable reference type checks throughout your code.</span></span>
> - <span data-ttu-id="3790a-112">Napisz kod, w którym kompilator wymusza te decyzje projektowe.</span><span class="sxs-lookup"><span data-stu-id="3790a-112">Write code where the compiler enforces those design decisions.</span></span>
> - <span data-ttu-id="3790a-113">Używanie funkcji referencyjnej nullable we własnych projektach</span><span class="sxs-lookup"><span data-stu-id="3790a-113">Use the nullable reference feature in your own designs</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3790a-114">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="3790a-114">Prerequisites</span></span>

<span data-ttu-id="3790a-115">Musisz skonfigurować maszynę do uruchamiania programu .NET Core, w tym kompilatora C# 8,0.</span><span class="sxs-lookup"><span data-stu-id="3790a-115">You'll need to set up your machine to run .NET Core, including the C# 8.0 compiler.</span></span> <span data-ttu-id="3790a-116">Kompilator języka C# 8,0 jest dostępny w programie [Visual Studio 2019](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2019)lub [.NET Core 3,0](https://dotnet.microsoft.com/download/dotnet-core/3.0).</span><span class="sxs-lookup"><span data-stu-id="3790a-116">The C# 8.0 compiler is available with [Visual Studio 2019](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2019), or [.NET Core 3.0](https://dotnet.microsoft.com/download/dotnet-core/3.0).</span></span>

<span data-ttu-id="3790a-117">W tym samouczku założono, że znasz języki C# i .NET, w tym Visual Studio lub interfejs wiersza polecenia platformy .NET Core.</span><span class="sxs-lookup"><span data-stu-id="3790a-117">This tutorial assumes you're familiar with C# and .NET, including either Visual Studio or the .NET Core CLI.</span></span>

## <a name="incorporate-nullable-reference-types-into-your-designs"></a><span data-ttu-id="3790a-118">Dołączanie typów odwołań do wartości null do projektów</span><span class="sxs-lookup"><span data-stu-id="3790a-118">Incorporate nullable reference types into your designs</span></span>

<span data-ttu-id="3790a-119">W tym samouczku utworzysz bibliotekę, w której będą wykonywane ankiety.</span><span class="sxs-lookup"><span data-stu-id="3790a-119">In this tutorial, you'll build a library that models running a survey.</span></span> <span data-ttu-id="3790a-120">Kod używa zarówno typów referencyjnych dopuszczających wartości null, jak i niedopuszczających wartości null typy odwołań do reprezentowania rzeczywistych koncepcji.</span><span class="sxs-lookup"><span data-stu-id="3790a-120">The code uses both nullable reference types and non-nullable reference types to represent the real-world concepts.</span></span> <span data-ttu-id="3790a-121">Pytania dotyczące ankiety nigdy nie mogą mieć wartości null.</span><span class="sxs-lookup"><span data-stu-id="3790a-121">The survey questions can never be null.</span></span> <span data-ttu-id="3790a-122">Respondent może preferować nie odpowiedzieć na pytanie.</span><span class="sxs-lookup"><span data-stu-id="3790a-122">A respondent might prefer not to answer a question.</span></span> <span data-ttu-id="3790a-123">`null`W takim przypadku odpowiedzi mogą być w tym przypadku.</span><span class="sxs-lookup"><span data-stu-id="3790a-123">The responses might be `null` in this case.</span></span>

<span data-ttu-id="3790a-124">Kod, który napiszesz dla tego przykładu, oznacza, że zamiar, a kompilator wymusza ten cel.</span><span class="sxs-lookup"><span data-stu-id="3790a-124">The code you'll write for this sample expresses that intent, and the compiler enforces that intent.</span></span>

## <a name="create-the-application-and-enable-nullable-reference-types"></a><span data-ttu-id="3790a-125">Tworzenie aplikacji i włączanie typów referencyjnych dopuszczających wartość null</span><span class="sxs-lookup"><span data-stu-id="3790a-125">Create the application and enable nullable reference types</span></span>

<span data-ttu-id="3790a-126">Utwórz nową aplikację konsolową w programie Visual Studio lub za pomocą polecenia `dotnet new console` .</span><span class="sxs-lookup"><span data-stu-id="3790a-126">Create a new console application either in Visual Studio or from the command line using `dotnet new console`.</span></span> <span data-ttu-id="3790a-127">Nadaj nazwę aplikacji `NullableIntroduction` .</span><span class="sxs-lookup"><span data-stu-id="3790a-127">Name the application `NullableIntroduction`.</span></span> <span data-ttu-id="3790a-128">Po utworzeniu aplikacji należy określić, że cały projekt zostanie skompilowany w włączonym **kontekście dopuszczającym wartość null**.</span><span class="sxs-lookup"><span data-stu-id="3790a-128">Once you've created the application, you'll need to specify that the entire project compiles in an enabled **nullable annotation context**.</span></span> <span data-ttu-id="3790a-129">Otwórz plik *. csproj* i Dodaj `Nullable` element do `PropertyGroup` elementu.</span><span class="sxs-lookup"><span data-stu-id="3790a-129">Open the *.csproj* file and add a `Nullable` element to the `PropertyGroup` element.</span></span> <span data-ttu-id="3790a-130">Ustaw dla niej wartość `enable`.</span><span class="sxs-lookup"><span data-stu-id="3790a-130">Set its value to `enable`.</span></span> <span data-ttu-id="3790a-131">Należy wybrać funkcję **typów referencyjnych dopuszczających wartość null** , nawet w projektach C# 8,0.</span><span class="sxs-lookup"><span data-stu-id="3790a-131">You must opt into the **nullable reference types** feature, even in C# 8.0 projects.</span></span> <span data-ttu-id="3790a-132">Dzieje się tak, ponieważ po włączeniu tej funkcji istniejące deklaracje zmiennej odwołania stają się **typami odwołań niedopuszczających wartości null**.</span><span class="sxs-lookup"><span data-stu-id="3790a-132">That's because once the feature is turned on, existing reference variable declarations become **non-nullable reference types**.</span></span> <span data-ttu-id="3790a-133">Chociaż ta decyzja pomoże w znalezieniu problemów, w których istniejący kod może nie mieć odpowiednich testów o wartości null, może nie dokładnie odzwierciedlać pierwotny cel projektowania:</span><span class="sxs-lookup"><span data-stu-id="3790a-133">While that decision will help find issues where existing code may not have proper null-checks, it may not accurately reflect your original design intent:</span></span>

```xml
<Nullable>enable</Nullable>
```

### <a name="design-the-types-for-the-application"></a><span data-ttu-id="3790a-134">Projektowanie typów aplikacji</span><span class="sxs-lookup"><span data-stu-id="3790a-134">Design the types for the application</span></span>

<span data-ttu-id="3790a-135">Ta aplikacja do ankiety wymaga utworzenia szeregu klas:</span><span class="sxs-lookup"><span data-stu-id="3790a-135">This survey application requires creating a number of classes:</span></span>

- <span data-ttu-id="3790a-136">Klasa, która modeluje listę pytań.</span><span class="sxs-lookup"><span data-stu-id="3790a-136">A class that models the list of questions.</span></span>
- <span data-ttu-id="3790a-137">Klasa, która modeluje listę osób, którym kontaktowali się na potrzeby ankiety.</span><span class="sxs-lookup"><span data-stu-id="3790a-137">A class that models a list of people contacted for the survey.</span></span>
- <span data-ttu-id="3790a-138">Klasa, która modeluje odpowiedzi od osoby, która przeprowadziła ankietę.</span><span class="sxs-lookup"><span data-stu-id="3790a-138">A class that models the answers from a person that took the survey.</span></span>

<span data-ttu-id="3790a-139">Te typy będą używały typów referencyjnych dopuszczających wartości null i niedopuszczających wartości null do wyznaczania, które elementy członkowskie są wymagane i które są opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="3790a-139">These types will make use of both nullable and non-nullable reference types to express which members are required and which members are optional.</span></span> <span data-ttu-id="3790a-140">Typy referencyjne dopuszczające wartość null komunikują się, że projekt zamierzenia</span><span class="sxs-lookup"><span data-stu-id="3790a-140">Nullable reference types communicate that design intent clearly:</span></span>

- <span data-ttu-id="3790a-141">Pytania, które są częścią ankiety, nie mogą mieć wartości null: nie ma sensu, aby zadać puste pytanie.</span><span class="sxs-lookup"><span data-stu-id="3790a-141">The questions that are part of the survey can never be null: It makes no sense to ask an empty question.</span></span>
- <span data-ttu-id="3790a-142">Respondenci nie mogą być puste.</span><span class="sxs-lookup"><span data-stu-id="3790a-142">The respondents can never be null.</span></span> <span data-ttu-id="3790a-143">Użytkownik chce śledzić osoby, którym nastąpi kontakt, nawet respondentów, którzy odrzucili uczestnictwo.</span><span class="sxs-lookup"><span data-stu-id="3790a-143">You'll want to track people you contacted, even respondents that declined to participate.</span></span>
- <span data-ttu-id="3790a-144">Każda odpowiedź na pytanie może mieć wartość null.</span><span class="sxs-lookup"><span data-stu-id="3790a-144">Any response to a question may be null.</span></span> <span data-ttu-id="3790a-145">Respondenci mogą odrzucić niektóre lub wszystkie pytania.</span><span class="sxs-lookup"><span data-stu-id="3790a-145">Respondents can decline to answer some or all questions.</span></span>

<span data-ttu-id="3790a-146">Jeśli zaznaczono program w języku C#, można to zrobić na typy odwołań, które zezwalają na `null` wartości, które mogły pominąć inne możliwości deklarowania wystąpień niedopuszczających wartości null:</span><span class="sxs-lookup"><span data-stu-id="3790a-146">If you've programmed in C#, you may be so accustomed to reference types that allow `null` values that you may have missed other opportunities to declare non-nullable instances:</span></span>

- <span data-ttu-id="3790a-147">Kolekcje pytań nie mogą dopuszczać wartości null.</span><span class="sxs-lookup"><span data-stu-id="3790a-147">The collection of questions should be non-nullable.</span></span>
- <span data-ttu-id="3790a-148">Kolekcja respondentów nie powinna być dopuszczana do wartości null.</span><span class="sxs-lookup"><span data-stu-id="3790a-148">The collection of respondents should be non-nullable.</span></span>

<span data-ttu-id="3790a-149">Podczas pisania kodu zobaczysz, że typ referencyjny niedopuszczający wartości null jako domyślny dla odwołań pozwala uniknąć częstych pomyłek, które mogą prowadzić do <xref:System.NullReferenceException> s.</span><span class="sxs-lookup"><span data-stu-id="3790a-149">As you write the code, you'll see that a non-nullable reference type as the default for references avoids common mistakes that could lead to <xref:System.NullReferenceException>s.</span></span> <span data-ttu-id="3790a-150">Jedną z lekcji w tym samouczku jest to, że podjęto decyzję o tym, które zmienne mogły lub nie mogą być `null` .</span><span class="sxs-lookup"><span data-stu-id="3790a-150">One lesson from this tutorial is that you made decisions about which variables could or could not be `null`.</span></span> <span data-ttu-id="3790a-151">Język nie dostarczył składni do wyrażania tych decyzji.</span><span class="sxs-lookup"><span data-stu-id="3790a-151">The language didn't provide syntax to express those decisions.</span></span> <span data-ttu-id="3790a-152">Teraz.</span><span class="sxs-lookup"><span data-stu-id="3790a-152">Now it does.</span></span>

<span data-ttu-id="3790a-153">Aplikacja, którą utworzysz, wykonuje następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="3790a-153">The app you'll build does the following steps:</span></span>

1. <span data-ttu-id="3790a-154">Tworzy ankietę i dodaje do niej pytania.</span><span class="sxs-lookup"><span data-stu-id="3790a-154">Creates a survey and adds questions to it.</span></span>
1. <span data-ttu-id="3790a-155">Tworzy pseudo-losowy zbiór respondentów dla ankiety.</span><span class="sxs-lookup"><span data-stu-id="3790a-155">Creates a pseudo-random set of respondents for the survey.</span></span>
1. <span data-ttu-id="3790a-156">Osoby odpowiedzialne za kontakty do momentu, aż ukończony rozmiar ankiety osiągnie numer celu.</span><span class="sxs-lookup"><span data-stu-id="3790a-156">Contacts respondents until the completed survey size reaches the goal number.</span></span>
1. <span data-ttu-id="3790a-157">Zapisuje ważne dane statystyczne odpowiedzi na ankiety.</span><span class="sxs-lookup"><span data-stu-id="3790a-157">Writes out important statistics on the survey responses.</span></span>

## <a name="build-the-survey-with-nullable-and-non-nullable-reference-types"></a><span data-ttu-id="3790a-158">Kompilowanie ankiety przy użyciu typów referencyjnych dopuszczających wartości null i niedopuszczających wartości null</span><span class="sxs-lookup"><span data-stu-id="3790a-158">Build the survey with nullable and non-nullable reference types</span></span>

<span data-ttu-id="3790a-159">Pierwszy kod, który napiszesz, tworzy ankietę.</span><span class="sxs-lookup"><span data-stu-id="3790a-159">The first code you'll write creates the survey.</span></span> <span data-ttu-id="3790a-160">Należy napisać klasy do modelowania pytania ankietowego i uruchomienia ankiety.</span><span class="sxs-lookup"><span data-stu-id="3790a-160">You'll write classes to model a survey question and a survey run.</span></span> <span data-ttu-id="3790a-161">Ankieta zawiera trzy typy pytań, które różnią się formatem odpowiedzi: tak/nie odpowiedzi, odpowiedzi na liczbę i odpowiedzi tekstowe.</span><span class="sxs-lookup"><span data-stu-id="3790a-161">Your survey has three types of questions, distinguished by the format of the answer: Yes/No answers, number answers, and text answers.</span></span> <span data-ttu-id="3790a-162">Utwórz `public SurveyQuestion` klasę:</span><span class="sxs-lookup"><span data-stu-id="3790a-162">Create a `public SurveyQuestion` class:</span></span>

```csharp
namespace NullableIntroduction
{
    public class SurveyQuestion
    {
    }
}
```

<span data-ttu-id="3790a-163">Kompilator interpretuje każdą deklarację zmiennej typu odwołania jako typ referencyjny **niedopuszczający wartości null** dla kodu w włączonym kontekście dopuszczającym wartość null.</span><span class="sxs-lookup"><span data-stu-id="3790a-163">The compiler interprets every reference type variable declaration as a **non-nullable** reference type for code in an enabled nullable annotation context.</span></span> <span data-ttu-id="3790a-164">Pierwsze ostrzeżenie można zobaczyć, dodając właściwości dla tekstu pytania i typ pytania, jak pokazano w poniższym kodzie:</span><span class="sxs-lookup"><span data-stu-id="3790a-164">You can see your first warning by adding properties for the question text and the type of question, as shown in the following code:</span></span>

```csharp
namespace NullableIntroduction
{
    public enum QuestionType
    {
        YesNo,
        Number,
        Text
    }

    public class SurveyQuestion
    {
        public string QuestionText { get; }
        public QuestionType TypeOfQuestion { get; }
    }
}
```

<span data-ttu-id="3790a-165">Ponieważ nie zainicjowano `QuestionText` , kompilator generuje ostrzeżenie, że nie zainicjowano właściwości, która nie dopuszcza wartości null.</span><span class="sxs-lookup"><span data-stu-id="3790a-165">Because you haven't initialized `QuestionText`, the compiler issues a warning that a non-nullable property hasn't been initialized.</span></span> <span data-ttu-id="3790a-166">Projekt wymaga, aby tekst pytania miał wartość różną od null, więc można dodać konstruktora, aby go zainicjować i `QuestionType` wartość.</span><span class="sxs-lookup"><span data-stu-id="3790a-166">Your design requires the question text to be non-null, so you add a constructor to initialize it and the `QuestionType` value as well.</span></span> <span data-ttu-id="3790a-167">Gotowa definicja klasy wygląda podobnie do następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="3790a-167">The finished class definition looks like the following code:</span></span>

[!code-csharp[DefineQuestion](~/samples/snippets/csharp/NullableIntroduction/NullableIntroduction/SurveyQuestion.cs)]

<span data-ttu-id="3790a-168">Dodanie konstruktora spowoduje usunięcie ostrzeżenia.</span><span class="sxs-lookup"><span data-stu-id="3790a-168">Adding the constructor removes the warning.</span></span> <span data-ttu-id="3790a-169">Argument konstruktora jest również typem referencyjnym, który nie dopuszcza wartości null, więc kompilator nie wystawia żadnych ostrzeżeń.</span><span class="sxs-lookup"><span data-stu-id="3790a-169">The constructor argument is also a non-nullable reference type, so the compiler doesn't issue any warnings.</span></span>

<span data-ttu-id="3790a-170">Następnie Utwórz `public` klasę o nazwie `SurveyRun` .</span><span class="sxs-lookup"><span data-stu-id="3790a-170">Next, create a `public` class named `SurveyRun`.</span></span> <span data-ttu-id="3790a-171">Ta klasa zawiera listę `SurveyQuestion` obiektów i metod, które umożliwiają dodawanie pytań do ankiety, jak pokazano w poniższym kodzie:</span><span class="sxs-lookup"><span data-stu-id="3790a-171">This class contains a list of `SurveyQuestion` objects and methods to add questions to the survey, as shown in the following code:</span></span>

```csharp
using System.Collections.Generic;

namespace NullableIntroduction
{
    public class SurveyRun
    {
        private List<SurveyQuestion> surveyQuestions = new List<SurveyQuestion>();

        public void AddQuestion(QuestionType type, string question) =>
            AddQuestion(new SurveyQuestion(type, question));
        public void AddQuestion(SurveyQuestion surveyQuestion) => surveyQuestions.Add(surveyQuestion);
    }
}
```

<span data-ttu-id="3790a-172">Tak jak wcześniej, należy zainicjować obiekt listy w wartości innej niż null lub kompilator generuje ostrzeżenie.</span><span class="sxs-lookup"><span data-stu-id="3790a-172">As before, you must initialize the list object to a non-null value or the compiler issues a warning.</span></span> <span data-ttu-id="3790a-173">Brak testów null w drugim przeciążeniu, `AddQuestion` ponieważ nie są one potrzebne: zadeklarowano, że zmienna nie dopuszcza wartości null.</span><span class="sxs-lookup"><span data-stu-id="3790a-173">There are no null checks in the second overload of `AddQuestion` because they aren't needed: You've declared that variable to be non-nullable.</span></span> <span data-ttu-id="3790a-174">Wartość nie może być `null` .</span><span class="sxs-lookup"><span data-stu-id="3790a-174">Its value can't be `null`.</span></span>

<span data-ttu-id="3790a-175">Przejdź do *program.cs* w edytorze i Zastąp zawartość `Main` następującym wierszem kodu:</span><span class="sxs-lookup"><span data-stu-id="3790a-175">Switch to *Program.cs* in your editor and replace the contents of `Main` with the following lines of code:</span></span>

[!code-csharp[AddQuestions](~/samples/snippets/csharp/NullableIntroduction/NullableIntroduction/Program.cs#AddQuestions)]

<span data-ttu-id="3790a-176">Ponieważ cały projekt jest w włączonym kontekście adnotacji dopuszczający wartość null, otrzymasz ostrzeżenia, gdy przejdziesz `null` do dowolnej metody, która oczekuje typu referencyjnego, który nie dopuszcza wartości null.</span><span class="sxs-lookup"><span data-stu-id="3790a-176">Because the entire project is in an enabled nullable annotation context, you'll get warnings when you pass `null` to any method expecting a non-nullable reference type.</span></span> <span data-ttu-id="3790a-177">Wypróbuj go, dodając następujący wiersz do `Main` :</span><span class="sxs-lookup"><span data-stu-id="3790a-177">Try it by adding the following line to `Main`:</span></span>

```csharp
surveyRun.AddQuestion(QuestionType.Text, default);
```

## <a name="create-respondents-and-get-answers-to-the-survey"></a><span data-ttu-id="3790a-178">Twórz respondenci i uzyskuj odpowiedzi na ankietę</span><span class="sxs-lookup"><span data-stu-id="3790a-178">Create respondents and get answers to the survey</span></span>

<span data-ttu-id="3790a-179">Następnie napisz kod, który generuje odpowiedzi na ankietę.</span><span class="sxs-lookup"><span data-stu-id="3790a-179">Next, write the code that generates answers to the survey.</span></span> <span data-ttu-id="3790a-180">Ten proces obejmuje kilka małych zadań:</span><span class="sxs-lookup"><span data-stu-id="3790a-180">This process involves several small tasks:</span></span>

1. <span data-ttu-id="3790a-181">Kompiluj metodę generującą obiekty respondentów.</span><span class="sxs-lookup"><span data-stu-id="3790a-181">Build a method that generates respondent objects.</span></span> <span data-ttu-id="3790a-182">Reprezentują one osoby, które poprosiły o wypełnienie ankiety.</span><span class="sxs-lookup"><span data-stu-id="3790a-182">These represent people asked to fill out the survey.</span></span>
1. <span data-ttu-id="3790a-183">Utwórz logikę, aby symulować pytania do respondenta i zbierać odpowiedzi lub zauważyć, że respondent nie odpowiedział.</span><span class="sxs-lookup"><span data-stu-id="3790a-183">Build logic to simulate asking the questions to a respondent and collecting answers or noting that a respondent didn't answer.</span></span>
1. <span data-ttu-id="3790a-184">Powtarzaj do momentu, aż wystarczające respondenci przepowieli ankietę.</span><span class="sxs-lookup"><span data-stu-id="3790a-184">Repeat until enough respondents have answered the survey.</span></span>

<span data-ttu-id="3790a-185">Potrzebujesz klasy do reprezentowania odpowiedzi ankiety, więc Dodaj ją teraz.</span><span class="sxs-lookup"><span data-stu-id="3790a-185">You'll need a class to represent a survey response, so add that now.</span></span> <span data-ttu-id="3790a-186">Włącz obsługę dopuszczania wartości null.</span><span class="sxs-lookup"><span data-stu-id="3790a-186">Enable nullable support.</span></span> <span data-ttu-id="3790a-187">Dodaj `Id` Właściwość i konstruktora, która go inicjuje, jak pokazano w poniższym kodzie:</span><span class="sxs-lookup"><span data-stu-id="3790a-187">Add an `Id` property and a constructor that initializes it, as shown in the following code:</span></span>

```csharp
namespace NullableIntroduction
{
    public class SurveyResponse
    {
        public int Id { get; }

        public SurveyResponse(int id) => Id = id;
    }
}
```

<span data-ttu-id="3790a-188">Następnie Dodaj metodę, `static` Aby utworzyć nowych uczestników przez wygenerowanie losowego identyfikatora:</span><span class="sxs-lookup"><span data-stu-id="3790a-188">Next, add a `static` method to create new participants by generating a random ID:</span></span>

[!code-csharp[GenerateRespondents](~/samples/snippets/csharp/NullableIntroduction/NullableIntroduction/SurveyResponse.cs#Random)]

<span data-ttu-id="3790a-189">Główną odpowiedzialnością tej klasy jest generowanie odpowiedzi dla uczestnika na pytania w ankiecie.</span><span class="sxs-lookup"><span data-stu-id="3790a-189">The main responsibility of this class is to generate the responses for a participant to the questions in the survey.</span></span> <span data-ttu-id="3790a-190">Ta odpowiedzialność obejmuje kilka kroków:</span><span class="sxs-lookup"><span data-stu-id="3790a-190">This responsibility has a few steps:</span></span>

1. <span data-ttu-id="3790a-191">Poproś o uczestnictwo w ankiecie.</span><span class="sxs-lookup"><span data-stu-id="3790a-191">Ask for participation in the survey.</span></span> <span data-ttu-id="3790a-192">Jeśli osoba nie wyraża zgody, zwróć odpowiedź o brakującą wartość (lub null).</span><span class="sxs-lookup"><span data-stu-id="3790a-192">If the person doesn't consent, return a missing (or null) response.</span></span>
1. <span data-ttu-id="3790a-193">Zadawaj każde pytanie i zanotuj odpowiedź.</span><span class="sxs-lookup"><span data-stu-id="3790a-193">Ask each question and record the answer.</span></span> <span data-ttu-id="3790a-194">Każda odpowiedź może być również brakująca (lub mieć wartość null).</span><span class="sxs-lookup"><span data-stu-id="3790a-194">Each answer may also be missing (or null).</span></span>

<span data-ttu-id="3790a-195">Dodaj następujący kod do `SurveyResponse` klasy:</span><span class="sxs-lookup"><span data-stu-id="3790a-195">Add the following code to your `SurveyResponse` class:</span></span>

[!code-csharp[AnswerSurvey](~/samples/snippets/csharp/NullableIntroduction/NullableIntroduction/SurveyResponse.cs#AnswerSurvey)]

<span data-ttu-id="3790a-196">Magazyn dla odpowiedzi na ankiety jest `Dictionary<int, string>?` , co oznacza, że może mieć wartość null.</span><span class="sxs-lookup"><span data-stu-id="3790a-196">The storage for the survey answers is a `Dictionary<int, string>?`, indicating that it may be null.</span></span> <span data-ttu-id="3790a-197">Używasz nowej funkcji języka do deklarowania zamiaru projektu, zarówno do kompilatora, jak i do każdego, kto czyta kod później.</span><span class="sxs-lookup"><span data-stu-id="3790a-197">You're using the new language feature to declare your design intent, both to the compiler and to anyone reading your code later.</span></span> <span data-ttu-id="3790a-198">Jeśli kiedykolwiek wyjdziesz `surveyResponses` do wcześniejszego odwołania bez sprawdzania, otrzymasz `null` Ostrzeżenie kompilatora.</span><span class="sxs-lookup"><span data-stu-id="3790a-198">If you ever dereference `surveyResponses` without checking for the `null` value first, you'll get a compiler warning.</span></span> <span data-ttu-id="3790a-199">Nie otrzymujesz ostrzeżenia w `AnswerSurvey` metodzie, ponieważ kompilator może określić, że dla `surveyResponses` zmiennej została ustawiona wartość inna niż null.</span><span class="sxs-lookup"><span data-stu-id="3790a-199">You don't get a warning in the `AnswerSurvey` method because the compiler can determine the `surveyResponses` variable was set to a non-null value above.</span></span>

<span data-ttu-id="3790a-200">Użycie `null` w przypadku brakujących odpowiedzi podświetla kluczowy punkt do pracy z typami odwołań dopuszczających wartość null: nie można usunąć wszystkich `null` wartości z programu.</span><span class="sxs-lookup"><span data-stu-id="3790a-200">Using `null` for missing answers highlights a key point for working with nullable reference types: your goal isn't to remove all `null` values from your program.</span></span> <span data-ttu-id="3790a-201">Zamiast tego celem jest upewnienie się, że napisany kod wyraża zamiar Twojego projektu.</span><span class="sxs-lookup"><span data-stu-id="3790a-201">Rather, your goal is to ensure that the code you write expresses the intent of your design.</span></span> <span data-ttu-id="3790a-202">Brakujące wartości są koniecznym pojęciem do wyrażania w kodzie.</span><span class="sxs-lookup"><span data-stu-id="3790a-202">Missing values are a necessary concept to express in your code.</span></span> <span data-ttu-id="3790a-203">`null`Wartość jest jasne, aby wyrazić te brakujące wartości.</span><span class="sxs-lookup"><span data-stu-id="3790a-203">The `null` value is a clear way to express those missing values.</span></span> <span data-ttu-id="3790a-204">Próba usunięcia wszystkich `null` wartości powoduje tylko określenie, że nie są to wartości brakujące `null` .</span><span class="sxs-lookup"><span data-stu-id="3790a-204">Trying to remove all `null` values only leads to defining some other way to express those missing values without `null`.</span></span>

<span data-ttu-id="3790a-205">Następnie należy napisać `PerformSurvey` metodę w `SurveyRun` klasie.</span><span class="sxs-lookup"><span data-stu-id="3790a-205">Next, you need to write the `PerformSurvey` method in the `SurveyRun` class.</span></span> <span data-ttu-id="3790a-206">Dodaj następujący kod do `SurveyRun` klasy:</span><span class="sxs-lookup"><span data-stu-id="3790a-206">Add the following code in the `SurveyRun` class:</span></span>

[!code-csharp[PerformSurvey](~/samples/snippets/csharp/NullableIntroduction/NullableIntroduction/SurveyRun.cs#PerformSurvey)]

<span data-ttu-id="3790a-207">W tym przypadku wybór wartości null wskazuje, `List<SurveyResponse>?` że odpowiedź może mieć wartość null.</span><span class="sxs-lookup"><span data-stu-id="3790a-207">Here again, your choice of a nullable `List<SurveyResponse>?` indicates the response may be null.</span></span> <span data-ttu-id="3790a-208">Oznacza to, że ankieta nie została jeszcze udzielona żadnym respondentom.</span><span class="sxs-lookup"><span data-stu-id="3790a-208">That indicates the survey hasn't been given to any respondents yet.</span></span> <span data-ttu-id="3790a-209">Zwróć uwagę, że respondenci są dodawani, dopóki nie zostanie osiągnięta wystarczająca liczba.</span><span class="sxs-lookup"><span data-stu-id="3790a-209">Notice that respondents are added until enough have consented.</span></span>

<span data-ttu-id="3790a-210">Ostatnim krokiem do uruchomienia ankiety jest dodanie wywołania do wykonania ankiety na końcu `Main` metody:</span><span class="sxs-lookup"><span data-stu-id="3790a-210">The last step to run the survey is to add a call to perform the survey at the end of the `Main` method:</span></span>

[!code-csharp[RunSurvey](~/samples/snippets/csharp/NullableIntroduction/NullableIntroduction/Program.cs#RunSurvey)]

## <a name="examine-survey-responses"></a><span data-ttu-id="3790a-211">Zbadaj odpowiedzi na ankietę</span><span class="sxs-lookup"><span data-stu-id="3790a-211">Examine survey responses</span></span>

<span data-ttu-id="3790a-212">Ostatnim krokiem jest wyświetlenie wyników ankiety.</span><span class="sxs-lookup"><span data-stu-id="3790a-212">The last step is to display survey results.</span></span> <span data-ttu-id="3790a-213">Dodasz kod do wielu utworzonych klas.</span><span class="sxs-lookup"><span data-stu-id="3790a-213">You'll add code to many of the classes you've written.</span></span> <span data-ttu-id="3790a-214">Ten kod demonstruje wartość odróżniania typów referencyjnych dopuszczających wartości null i niedopuszczających wartości null.</span><span class="sxs-lookup"><span data-stu-id="3790a-214">This code demonstrates the value of distinguishing nullable and non-nullable reference types.</span></span> <span data-ttu-id="3790a-215">Zacznij od dodania następujących dwóch składowych wyrażeń do `SurveyResponse` klasy:</span><span class="sxs-lookup"><span data-stu-id="3790a-215">Start by adding the following two expression-bodied members to the `SurveyResponse` class:</span></span>

[!code-csharp[ReportResponses](~/samples/snippets/csharp/NullableIntroduction/NullableIntroduction/SurveyResponse.cs#SurveyStatus)]

<span data-ttu-id="3790a-216">Ponieważ `surveyResponses` jest typem referencyjnym dopuszczającym wartość null, sprawdzanie wartości null jest niezbędne przed cofnięciem odwołania do niego.</span><span class="sxs-lookup"><span data-stu-id="3790a-216">Because `surveyResponses` is a nullable reference type, null checks are necessary before de-referencing it.</span></span> <span data-ttu-id="3790a-217">`Answer`Metoda zwraca ciąg niedopuszczający wartości null, dlatego musimy uwzględnić przypadek brakującej odpowiedzi przy użyciu operatora łączenia wartości null.</span><span class="sxs-lookup"><span data-stu-id="3790a-217">The `Answer` method returns a non-nullable string, so we have to cover the case of a missing answer by using the null-coalescing operator.</span></span>

<span data-ttu-id="3790a-218">Następnie Dodaj te trzy składowe z wyrażeniami do `SurveyRun` klasy:</span><span class="sxs-lookup"><span data-stu-id="3790a-218">Next, add these three expression-bodied members to the `SurveyRun` class:</span></span>

[!code-csharp[ReportResults](~/samples/snippets/csharp/NullableIntroduction/NullableIntroduction/SurveyRun.cs#RunReport)]

<span data-ttu-id="3790a-219">`AllParticipants`Element członkowski musi wziąć pod uwagę, że `respondents` zmienna może mieć wartość null, ale zwracana wartość nie może być równa null.</span><span class="sxs-lookup"><span data-stu-id="3790a-219">The `AllParticipants` member must take into account that the `respondents` variable might be null, but the return value can't be null.</span></span> <span data-ttu-id="3790a-220">Jeśli zmienisz to wyrażenie poprzez usunięcie `??` i pustej sekwencji, która następuje, kompilator ostrzega o tym, że metoda może zostać zwrócona, `null` a jej sygnatura zwrotna zwraca typ niedopuszczający wartości null.</span><span class="sxs-lookup"><span data-stu-id="3790a-220">If you change that expression by removing the `??` and the empty sequence that follows, the compiler warns you the method might return `null` and its return signature returns a non-nullable type.</span></span>

<span data-ttu-id="3790a-221">Na koniec Dodaj następującą pętlę w dolnej części `Main` metody:</span><span class="sxs-lookup"><span data-stu-id="3790a-221">Finally, add the following loop at the bottom of the `Main` method:</span></span>

[!code-csharp[DisplaySurveyResults](~/samples/snippets/csharp/NullableIntroduction/NullableIntroduction/Program.cs#WriteAnswers)]

<span data-ttu-id="3790a-222">Nie musisz `null` już sprawdzać w tym kodzie, ponieważ zostały zaprojektowane bazowe interfejsy, aby wszystkie zwracane były typy odwołań niedopuszczające wartości null.</span><span class="sxs-lookup"><span data-stu-id="3790a-222">You don't need any `null` checks in this code because you've designed the underlying interfaces so that they all return non-nullable reference types.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="3790a-223">Uzyskiwanie kodu</span><span class="sxs-lookup"><span data-stu-id="3790a-223">Get the code</span></span>

<span data-ttu-id="3790a-224">Możesz uzyskać kod gotowego samouczka z naszego repozytorium [przykładów](https://github.com/dotnet/samples) w folderze [CSharp/NullableIntroduction](https://github.com/dotnet/samples/tree/master/csharp/NullableIntroduction) .</span><span class="sxs-lookup"><span data-stu-id="3790a-224">You can get the code for the finished tutorial from our [samples](https://github.com/dotnet/samples) repository in the [csharp/NullableIntroduction](https://github.com/dotnet/samples/tree/master/csharp/NullableIntroduction) folder.</span></span>

<span data-ttu-id="3790a-225">Eksperymentowanie, zmieniając deklaracje typu między typami odwołań dopuszczających wartości null i niedopuszczające wartości null.</span><span class="sxs-lookup"><span data-stu-id="3790a-225">Experiment by changing the type declarations between nullable and non-nullable reference types.</span></span> <span data-ttu-id="3790a-226">Zobacz, jak generuje różne ostrzeżenia, aby zapobiec przypadkowemu wykorzystaniu `null` .</span><span class="sxs-lookup"><span data-stu-id="3790a-226">See how that generates different warnings to ensure you don't accidentally dereference a `null`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3790a-227">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3790a-227">Next steps</span></span>

<span data-ttu-id="3790a-228">Dowiedz się więcej przez Migrowanie istniejącej aplikacji w celu używania typów referencyjnych dopuszczających wartości null:</span><span class="sxs-lookup"><span data-stu-id="3790a-228">Learn more by migrating an existing application to use nullable reference types:</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="3790a-229">Uaktualnianie aplikacji w celu używania typów referencyjnych dopuszczających wartości null</span><span class="sxs-lookup"><span data-stu-id="3790a-229">Upgrade an application to use nullable reference types</span></span>](upgrade-to-nullable-references.md)

<span data-ttu-id="3790a-230">Dowiedz się, jak używać typu referencyjnego nullable podczas korzystania z Entity Framework:</span><span class="sxs-lookup"><span data-stu-id="3790a-230">Learn how to use nullable reference type when using Entity Framework:</span></span>
> [<span data-ttu-id="3790a-231">Podstawy Entity Framework Core: Praca z typami odwołań dopuszczających wartości null</span><span class="sxs-lookup"><span data-stu-id="3790a-231">Entity Framework Core Fundamentals: Working with Nullable Reference Types</span></span>](https://docs.microsoft.com/en-us/ef/core/miscellaneous/nullable-reference-types)
