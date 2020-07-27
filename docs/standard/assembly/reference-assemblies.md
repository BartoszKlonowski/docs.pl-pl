---
title: Odwoływanie się do zestawów
description: Dowiedz się więcej na temat zestawów referencyjnych, specjalnego typu zestawów w programie .NET, które zawierają tylko publiczną powierzchnię interfejsu API biblioteki
author: MSDN-WhiteKnight
ms.date: 09/12/2019
ms.technology: dotnet-standard
ms.openlocfilehash: 43a9dab037f4d0f1926ff67f8f38eaa6734a6d67
ms.sourcegitcommit: 87cfeb69226fef01acb17c56c86f978f4f4a13db
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/24/2020
ms.locfileid: "87164523"
---
# <a name="reference-assemblies"></a>Odwoływanie się do zestawów

*Zestawy referencyjne* są specjalnym typem zestawu, który zawiera tylko minimalną ilość metadanych wymaganą do reprezentowania publicznej powierzchni interfejsu API biblioteki. Obejmują one deklaracje dla wszystkich elementów członkowskich, które są istotne w przypadku odwoływania się do zestawu w narzędziach kompilacji, ale wyklucza wszystkie implementacje składowych i deklaracje prywatnych członków, którzy nie mają zauważalnego wpływu na ich kontrakt interfejsu API. Z kolei regularne zestawy są nazywane *zestawami implementacji*.

Nie można załadować zestawów referencyjnych do wykonania, ale mogą one być przesyłane jako dane wejściowe kompilatora w taki sam sposób jak zestawy implementacji. Zestawy referencyjne są zwykle dystrybuowane z zestawem SDK (Software Development Kit) określonej platformy lub biblioteki.

Użycie zestawu referencyjnego umożliwia deweloperom tworzenie programów przeznaczonych dla określonej wersji biblioteki bez konieczności używania pełnego zestawu implementacji dla tej wersji. Załóżmy, że masz tylko najnowszą wersję niektórych bibliotek na swojej maszynie, ale chcesz skompilować program przeznaczony dla wcześniejszej wersji tej biblioteki. Jeśli kompilujesz bezpośrednio względem zestawu implementacji, możesz przypadkowo użyć elementów członkowskich interfejsu API, które nie są dostępne w starszej wersji. Ten błąd zostanie wyszukany tylko podczas testowania programu na maszynie docelowej. Jeśli kompilujesz względem zestawu odwołań dla starszej wersji, natychmiast otrzymasz błąd w czasie kompilacji.

Zestaw referencyjny może również reprezentować kontrakt, czyli zestaw interfejsów API, które nie odpowiadają zestawowi konkretnych implementacji. Takie zestawy referencyjne, nazywane *zestawem kontraktu*, mogą służyć jako ukierunkowane na wiele platform, które obsługują ten sam zestaw interfejsów API. Na przykład .NET Standard zawiera zestaw kontraktu *netstandard.dll*, który reprezentuje zestaw wspólnych interfejsów API współużytkowanych przez różne platformy .NET. Implementacje tych interfejsów API są zawarte w różnych zestawach na różnych platformach, takich jak *mscorlib.dll* na .NET Framework lub *System.Private.CoreLib.dll* na platformie .NET Core. Biblioteka, która jest przeznaczona dla .NET Standard można uruchamiać na wszystkich platformach, które obsługują .NET Standard.

## <a name="using-reference-assemblies"></a>Używanie zestawów odwołań

Aby używać niektórych interfejsów API z projektu, należy dodać odwołania do ich zestawów. Można dodać odwołania do zestawów implementacji lub odwołań do zestawów. Zaleca się używanie zestawów referencyjnych, gdy są one dostępne. To gwarantuje, że używasz tylko obsługiwanych elementów członkowskich interfejsu API w wersji docelowej, które mają być używane przez projektantów interfejsu API. Użycie zestawu referencyjnego gwarantuje, że nie wykonujesz zależności od szczegółów implementacji.

Zestawy referencyjne dla bibliotek .NET Framework są dystrybuowane z pakietami docelowymi. Można je uzyskać, pobierając Autonomiczny Instalator lub wybierając składnik w Instalatorze programu Visual Studio. Aby uzyskać więcej informacji, zobacz [Install the .NET Framework for Developers](../../framework/install/guide-for-developers.md). W przypadku platformy .NET Core i .NET Standard zestawy odwołań są automatycznie pobierane zgodnie z potrzebami (za pośrednictwem NuGet) i przywoływane. W przypadku platformy .NET Core 3,0 lub nowszej zestawy referencyjne dla podstawowej platformy są w pakiecie [Microsoft. servicecore. app. ref](https://www.nuget.org/packages/Microsoft.NETCore.App.Ref) (w zamian jest używany pakiet [Microsoft. servicecore. app](https://www.nuget.org/packages/Microsoft.NETCore.App) ) dla wersji przed 3,0.

Po dodaniu odwołań do zestawów .NET Framework w programie Visual Studio przy użyciu okna dialogowego **Dodawanie odwołania** można wybrać zestaw z listy, a program Visual Studio automatycznie odnajdzie zestawy referencyjne, które odpowiadają wersji platformy docelowej wybranej w projekcie. To samo dotyczy dodawania odwołań bezpośrednio do projektu MSBuild przy użyciu elementu projektu [referencyjnego](/visualstudio/msbuild/common-msbuild-project-items#reference) : należy określić tylko nazwę zestawu, a nie pełną ścieżkę pliku. Po dodaniu odwołań do tych zestawów w wierszu polecenia przy użyciu `-reference` opcji kompilatora ([w języku C#](../../csharp/language-reference/compiler-options/reference-compiler-option.md) i w [Visual Basic](../../visual-basic/reference/command-line-compiler/reference.md)) lub za pomocą <xref:Microsoft.CodeAnalysis.Compilation.AddReferences%2A?displayProperty=nameWithType> metody w interfejsie API Roslyn należy ręcznie określić pliki zestawu odwołań dla prawidłowej wersji platformy docelowej. Pliki zestawu odwołań .NET Framework znajdują się w *zestawach referencyjnych% ProgramFiles (x86)% \\ \\ Microsoft \\ Framework \\ . Katalog NETFramework* . W przypadku platformy .NET Core można wymusić operację publikowania, aby skopiować zestawy referencyjne dla platformy docelowej do podkatalogu *Publish/ReFS* katalogu wyjściowego przez ustawienie `PreserveCompilationContext` właściwości projektu na `true` . Następnie można przekazać te pliki zestawu odwołań do kompilatora. Korzystanie `DependencyContext` z pakietu [Microsoft. Extensions. DependencyModel](https://www.nuget.org/packages/Microsoft.Extensions.DependencyModel/) może pomóc w znalezieniu ich ścieżek.

Ponieważ nie zawierają one implementacji, nie można załadować zestawów odwołań do wykonania. Próba wykonania tej czynności spowoduje wykonanie <xref:System.BadImageFormatException?displayProperty=nameWithType> . Jeśli chcesz przejrzeć zawartość zestawu odwołania, możesz załadować go do kontekstu tylko odbicia w .NET Framework (przy użyciu <xref:System.Reflection.Assembly.ReflectionOnlyLoad%2A?displayProperty=nameWithType> metody) lub do programu <xref:System.Reflection.MetadataLoadContext> w środowisku .NET Core.

## <a name="generating-reference-assemblies"></a>Generowanie zestawów referencyjnych

Generowanie zestawów referencyjnych dla bibliotek może być przydatne, gdy klienci biblioteki muszą kompilować swoje programy w wielu różnych wersjach biblioteki. Dystrybuowanie zestawów implementacji dla wszystkich tych wersji może być niepraktyczne ze względu na ich duży rozmiar. Zestawy referencyjne są mniejsze w rozmiarze i rozpowszechniane jako część zestawu SDK biblioteki redukują rozmiar pobierania i oszczędzają miejsce na dysku.

Narzędzia środowisk IDE i Build Tools mogą również korzystać z zestawów referencyjnych, aby skrócić czasy kompilacji w przypadku dużych rozwiązań składających się z wielu bibliotek klas. Zwykle w scenariuszach kompilacji przyrostowej projekt jest odbudowany, gdy którykolwiek z jego plików wejściowych zostanie zmieniony, włącznie z zestawami, od których zależy. Zestaw implementacji zmienia się za każdym razem, gdy programista zmieni implementację dowolnego elementu członkowskiego. Zestaw referencyjny zmienia się tylko wtedy, gdy jego publiczny interfejs API ma wartość. Dlatego użycie zestawu referencyjnego jako pliku wejściowego zamiast zestawu implementacji pozwala pominąć kompilację zależnego projektu w niektórych przypadkach.

Można generować zestawy referencyjne:

- W projekcie MSBuild, przy użyciu [ `ProduceReferenceAssembly` właściwości projektu](/visualstudio/msbuild/common-msbuild-project-properties).
- Podczas kompilowania programu z wiersza polecenia, przez specifiying `-refonly` ([c#](../../csharp/language-reference/compiler-options/refonly-compiler-option.md)  /  [Visual Basic](../../visual-basic/reference/command-line-compiler/refonly-compiler-option.md) ) lub `-refout` ([c#](../../csharp/language-reference/compiler-options/refout-compiler-option.md)  /  [Visual Basic](../../visual-basic/reference/command-line-compiler/refout-compiler-option.md)) opcje kompilatora.
- W przypadku korzystania z interfejsu API Roslyn przez <xref:Microsoft.CodeAnalysis.Emit.EmitOptions.EmitMetadataOnly?displayProperty=nameWithType> ustawienie `true` na <xref:Microsoft.CodeAnalysis.Emit.EmitOptions.IncludePrivateMembers?displayProperty=nameWithType> i `false` w obiekcie przekazanym do <xref:Microsoft.CodeAnalysis.Compilation.Emit%2A?displayProperty=nameWithType> metody.

Aby dystrybuować zestawy referencyjne z pakietami NuGet, należy uwzględnić je w podkatalogu *ref \\ * w katalogu pakietu, a nie w podkatalogu *lib \\ * używanym do zestawów implementacji.

## <a name="reference-assemblies-structure"></a>Struktura zestawów odwołań

Zestawy referencyjne są rozwinięciem powiązanej koncepcji, *zestawów samych metadanych*. Zestawy zawierające tylko metadane są zastępowane przez jedną `throw null` treść, ale obejmują wszystkie elementy członkowskie z wyjątkiem typów anonimowych. Przyczyną używania `throw null` treści (w przeciwieństwie do braku treści) jest to, że **PEVerify** może działać i kończyć się powodzeniem (w związku z tym sprawdzanie kompletności metadanych).

Zestawy referencyjne usuwają metadane (prywatne składowe) z zestawów samych metadanych:

- Zestaw odniesienia zawiera odwołania do potrzebnych elementów interfejsu API. Rzeczywisty zestaw może zawierać dodatkowe odwołania dotyczące konkretnych implementacji. Na przykład zestaw odwołania dla `class C { private void M() { dynamic d = 1; ... } }` nie odwołuje się do żadnego typu wymaganego przez `dynamic` .
- Prywatne funkcje — elementy członkowskie (metody, właściwości i zdarzenia) są usuwane w przypadkach, gdy ich usunięcie nie ma zauważalnego wpływu na kompilację. Jeśli nie ma żadnych atrybutów [InternalsVisibleTo](xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute) , składowe funkcji wewnętrznych również są usuwane.

Metadane w zestawach referencyjnych nadal przechowują następujące informacje:

- Wszystkie typy, w tym typy prywatne i zagnieżdżone.
- Wszystkie atrybuty, nawet wewnętrzne.
- Wszystkie metody wirtualne.
- Jawne implementacje interfejsu.
- Jawnie zaimplementowane właściwości i zdarzenia, ponieważ ich metody dostępu są wirtualne.
- Wszystkie pola struktur.

Zestawy referencyjne zawierają atrybut [ReferenceAssembly](xref:System.Runtime.CompilerServices.ReferenceAssemblyAttribute) na poziomie zestawu. Ten atrybut może być określony w źródle; Następnie kompilator nie będzie musiał go przeprowadzić. Z powodu tego atrybutu środowiska uruchomieniowe będą odrzucać ładowanie zestawów odwołań do wykonania (ale mogą być ładowane w trybie tylko odbicie).

Dokładne szczegóły struktury zestawu odwołań zależą od wersji kompilatora. Nowsze wersje mogą zdecydować się na wykluczenie większej liczby metadanych, jeśli zostanie ona określona bez wpływu na publiczną powierzchnię interfejsu API.

> [!NOTE]
> Informacje w tej sekcji dotyczą tylko zestawów referencyjnych wygenerowanych przez kompilatory Roslyn zaczynające się od języka C# w wersji 7,1 lub Visual Basic w wersji 15,3. Struktura zestawów referencyjnych dla bibliotek .NET Framework i .NET Core może różnić się w niektórych szczegółach, ponieważ korzystają z własnego mechanizmu generowania zestawów odwołań. Na przykład mogą mieć całkowicie puste treści metody zamiast `throw null` treści. Jednak ogólna zasada nadal stosuje się: nie mają one przydatnych implementacji metod i zawierają tylko metadane dla elementów członkowskich, które mają zauważalny wpływ z perspektywy publicznego interfejsu API.

## <a name="see-also"></a>Zobacz także

- [Zestawy w środowisku .NET](index.md)
- [Omówienie określania celu platformy](/visualstudio/ide/visual-studio-multi-targeting-overview)
- [Instrukcje: Dodawanie lub usuwanie odwołań za pomocą Menedżera odwołań](/visualstudio/ide/how-to-add-or-remove-references-by-using-the-reference-manager)
