---
title: Silne nazewnictwo i biblioteki platformy .NET
description: Zalecenia dotyczące najlepszych rozwiązań dotyczących silnych nazw bibliotek platformy .NET.
ms.date: 10/16/2018
ms.openlocfilehash: 6f9533d768331964a8e640243536b12ddde158e5
ms.sourcegitcommit: 7588b1f16b7608bc6833c05f91ae670c22ef56f8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/02/2020
ms.locfileid: "93189215"
---
# <a name="strong-naming"></a><span data-ttu-id="c4a88-103">Silne nazewnictwo</span><span class="sxs-lookup"><span data-stu-id="c4a88-103">Strong naming</span></span>

<span data-ttu-id="c4a88-104">Silne nazewnictwo odnosi się do podpisywania zestawu przy użyciu klucza, który wytwarza [zestaw o silnej nazwie](../assembly/strong-named.md).</span><span class="sxs-lookup"><span data-stu-id="c4a88-104">Strong naming refers to signing an assembly with a key, producing a [strong-named assembly](../assembly/strong-named.md).</span></span> <span data-ttu-id="c4a88-105">Jeśli zestaw ma silną nazwę, tworzy unikatową tożsamość na podstawie nazwy i numeru wersji zestawu i może pomóc zapobiec konfliktom zestawu.</span><span class="sxs-lookup"><span data-stu-id="c4a88-105">When an assembly is strong-named, it creates a unique identity based on the name and assembly version number, and it can help prevent assembly conflicts.</span></span>

<span data-ttu-id="c4a88-106">Minusem silne nazewnictwo to, że .NET Framework w systemie Windows umożliwia ścisłe ładowanie zestawów, gdy zestaw ma silną nazwę.</span><span class="sxs-lookup"><span data-stu-id="c4a88-106">The downside to strong naming is that .NET Framework on Windows enables strict loading of assemblies once an assembly is strong named.</span></span> <span data-ttu-id="c4a88-107">Odwołanie do zestawu o silnej nazwie musi być dokładnie zgodne z wersją załadowanego zestawu, wymuszając deweloperom możliwość [konfigurowania przekierowań powiązań](../../framework/configure-apps/redirect-assembly-versions.md) podczas korzystania z zestawu:</span><span class="sxs-lookup"><span data-stu-id="c4a88-107">A strong-named assembly reference must exactly match the version of the loaded assembly, forcing developers to [configure binding redirects](../../framework/configure-apps/redirect-assembly-versions.md) when using the assembly:</span></span>

```xml
<configuration>
   <runtime>
      <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">
         <dependentAssembly>
            <assemblyIdentity name="myAssembly" publicKeyToken="32ab4ba45e0a69a1" culture="neutral" />
            <bindingRedirect oldVersion="1.0.0.0" newVersion="2.0.0.0"/>
         </dependentAssembly>
      </assemblyBinding>
   </runtime>
</configuration>
```

<span data-ttu-id="c4a88-108">Gdy deweloperzy platformy .NET składają się na silne nazewnictwo, to to, czego zwykle są związane z ładowaniem zestawu.</span><span class="sxs-lookup"><span data-stu-id="c4a88-108">When .NET developers complain about strong naming, what they're usually complaining about is strict assembly loading.</span></span> <span data-ttu-id="c4a88-109">Na szczęście ten problem jest izolowany do .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="c4a88-109">Fortunately, this issue is isolated to .NET Framework.</span></span> <span data-ttu-id="c4a88-110">.NET 5 +, .NET Core, Xamarin, platformy UWP i większość innych implementacji platformy .NET nie mają ścisłego ładowania zestawu, który jest głównym minusemem silnych nazw.</span><span class="sxs-lookup"><span data-stu-id="c4a88-110">.NET 5+, .NET Core, Xamarin, UWP, and most other .NET implementations don't have strict assembly loading, which is the main downside of strong naming.</span></span>

<span data-ttu-id="c4a88-111">Jednym ważnym aspektem silnego nazewnictwa jest wirus: silnie nazwany zestaw może odwoływać się tylko do innych silnych nazwanych zestawów.</span><span class="sxs-lookup"><span data-stu-id="c4a88-111">One important aspect of strong naming is that it's viral: a strong named assembly can only reference other strong named assemblies.</span></span> <span data-ttu-id="c4a88-112">Jeśli biblioteka nie ma silnej nazwy, wykorzystasz deweloperów, którzy tworzą aplikację lub bibliotekę, która wymaga silnego nazewnictwa.</span><span class="sxs-lookup"><span data-stu-id="c4a88-112">If your library isn't strong named, then you have excluded developers who are building an application or library that needs strong naming from using it.</span></span>

<span data-ttu-id="c4a88-113">Zalety silnych nazw to:</span><span class="sxs-lookup"><span data-stu-id="c4a88-113">The benefits of strong naming are:</span></span>

1. <span data-ttu-id="c4a88-114">Zestaw może być przywoływany i używany przez inne zestawy o silnych nazwach.</span><span class="sxs-lookup"><span data-stu-id="c4a88-114">The assembly can be referenced and used by other strong-named assemblies.</span></span>
2. <span data-ttu-id="c4a88-115">Zestaw może być przechowywany w globalnej pamięci podręcznej zestawów (GAC).</span><span class="sxs-lookup"><span data-stu-id="c4a88-115">The assembly can be stored in the Global Assembly Cache (GAC).</span></span>
3. <span data-ttu-id="c4a88-116">Zestaw może być ładowany obok innych wersji zestawu.</span><span class="sxs-lookup"><span data-stu-id="c4a88-116">The assembly can be loaded side by side with other versions of the assembly.</span></span> <span data-ttu-id="c4a88-117">Ładowanie zestawów równoległych jest często wymagane przez aplikacje z architekturą wtyczek.</span><span class="sxs-lookup"><span data-stu-id="c4a88-117">Side-by-side assembly loading is commonly required by applications with plug-in architectures.</span></span>

## <a name="create-strong-named-net-libraries"></a><span data-ttu-id="c4a88-118">Tworzenie silnie nazwanych bibliotek platformy .NET</span><span class="sxs-lookup"><span data-stu-id="c4a88-118">Create strong named .NET libraries</span></span>

<span data-ttu-id="c4a88-119">Należy silnej nazwy bibliotek .NET Open Source.</span><span class="sxs-lookup"><span data-stu-id="c4a88-119">You should strong name your open-source .NET libraries.</span></span> <span data-ttu-id="c4a88-120">Silne nazewnictwo zestawu zapewnia, że większość osób może z niego korzystać, a ścisłe ładowanie zestawu ma wpływ tylko na .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="c4a88-120">Strong naming an assembly ensures the most people can use it, and strict assembly loading only affects .NET Framework.</span></span>

> [!NOTE]
> <span data-ttu-id="c4a88-121">Te wskazówki dotyczą publicznie dystrybuowanych bibliotek platformy .NET, takich jak biblioteki .NET opublikowane w witrynie NuGet.org. Silne nazewnictwo nie jest wymagane przez większość aplikacji .NET i nie powinno być wykonywane domyślnie.</span><span class="sxs-lookup"><span data-stu-id="c4a88-121">This guidance is specific to publicly distributed .NET libraries, such as .NET libraries published on NuGet.org. Strong naming is not required by most .NET applications and should not be done by default.</span></span>

<span data-ttu-id="c4a88-122">✔️ ROZWAŻYĆ silne nazewnictwo zestawów biblioteki.</span><span class="sxs-lookup"><span data-stu-id="c4a88-122">✔️ CONSIDER strong naming your library's assemblies.</span></span>

<span data-ttu-id="c4a88-123">✔️ Rozważ dodanie klucza silnego nazewnictwa do systemu kontroli źródła.</span><span class="sxs-lookup"><span data-stu-id="c4a88-123">✔️ CONSIDER adding the strong naming key to your source control system.</span></span>

> <span data-ttu-id="c4a88-124">Publicznie dostępny klucz umożliwia deweloperom modyfikowanie i ponowne kompilowanie kodu źródłowego biblioteki z tym samym kluczem.</span><span class="sxs-lookup"><span data-stu-id="c4a88-124">A publicly available key lets developers modify and recompile your library source code with the same key.</span></span>
>
> <span data-ttu-id="c4a88-125">Klucz silnego nazewnictwa nie powinien być publiczny, jeśli został użyty w przeszłości w celu udzielenia specjalnych uprawnień w [scenariuszach częściowej relacji zaufania](../../framework/misc/using-libraries-from-partially-trusted-code.md).</span><span class="sxs-lookup"><span data-stu-id="c4a88-125">You shouldn't make the strong naming key public if it has been used in the past to give special permissions in [partial-trust scenarios](../../framework/misc/using-libraries-from-partially-trusted-code.md).</span></span> <span data-ttu-id="c4a88-126">W przeciwnym razie mogą naruszać istniejące środowiska.</span><span class="sxs-lookup"><span data-stu-id="c4a88-126">Otherwise, you might compromise existing environments.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c4a88-127">Gdy wymagana jest tożsamość wydawcy kodu, zalecane jest [podpisywanie pakietów](/nuget/create-packages/sign-a-package) [Authenticode](/windows-hardware/drivers/install/authenticode) i NuGet.</span><span class="sxs-lookup"><span data-stu-id="c4a88-127">When the identity of the publisher of the code is desired, [Authenticode](/windows-hardware/drivers/install/authenticode) and [NuGet Package Signing](/nuget/create-packages/sign-a-package) are recommended.</span></span> <span data-ttu-id="c4a88-128">Zabezpieczeń dostępu kodu (CAS) nie należy używać jako środków zaradczych.</span><span class="sxs-lookup"><span data-stu-id="c4a88-128">Code Access Security (CAS) should not be used as a security mitigation.</span></span>

<span data-ttu-id="c4a88-129">✔️ ROZWAŻYĆ zwiększenie wersji zestawu tylko dla głównych zmian wersji, aby ułatwić użytkownikom zredukowanie przekierowań powiązań oraz częstotliwość ich aktualizowania.</span><span class="sxs-lookup"><span data-stu-id="c4a88-129">✔️ CONSIDER incrementing the assembly version on only major version changes to help users reduce binding redirects, and how often they're updated.</span></span>

> <span data-ttu-id="c4a88-130">Przeczytaj więcej [na temat przechowywania wersji i wersji zestawu](./versioning.md#assembly-version).</span><span class="sxs-lookup"><span data-stu-id="c4a88-130">Read more about [versioning and the assembly version](./versioning.md#assembly-version).</span></span>

<span data-ttu-id="c4a88-131">❌ NIE należy dodawać, usuwać ani zmieniać klucza silnego nazewnictwa.</span><span class="sxs-lookup"><span data-stu-id="c4a88-131">❌ DO NOT add, remove, or change the strong naming key.</span></span>

> <span data-ttu-id="c4a88-132">Modyfikacja klucza silnego nazewnictwa zestawu zmienia tożsamość zestawu i dzieli skompilowany kod, który go używa.</span><span class="sxs-lookup"><span data-stu-id="c4a88-132">Modifying an assembly's strong naming key changes the assembly's identity and breaks compiled code that uses it.</span></span> <span data-ttu-id="c4a88-133">Aby uzyskać więcej informacji, zobacz [binarne zmiany](./breaking-changes.md#binary-breaking-change).</span><span class="sxs-lookup"><span data-stu-id="c4a88-133">For more information, see [binary breaking changes](./breaking-changes.md#binary-breaking-change).</span></span>

<span data-ttu-id="c4a88-134">❌ NIE Publikuj w bibliotece o silnej nazwie i niesilnych nazwach biblioteki.</span><span class="sxs-lookup"><span data-stu-id="c4a88-134">❌ DO NOT publish strong-named and non-strong-named versions of your library.</span></span> <span data-ttu-id="c4a88-135">Przykład: `Contoso.Api` i `Contoso.Api.StrongNamed`.</span><span class="sxs-lookup"><span data-stu-id="c4a88-135">For example, `Contoso.Api` and `Contoso.Api.StrongNamed`.</span></span>

> <span data-ttu-id="c4a88-136">Publikowanie dwóch pakietów rozwidlenia systemu dla deweloperów.</span><span class="sxs-lookup"><span data-stu-id="c4a88-136">Publishing two packages forks your developer eco-system.</span></span> <span data-ttu-id="c4a88-137">Ponadto, jeśli aplikacja zostanie zakończona w zależności od obu pakietów, deweloper może napotkać konflikty nazw typów.</span><span class="sxs-lookup"><span data-stu-id="c4a88-137">Also, if an application ends up depending on both packages the developer can encounter type name conflicts.</span></span> <span data-ttu-id="c4a88-138">W odniesieniu do platformy .NET są zainteresowane różne typy w różnych zestawach.</span><span class="sxs-lookup"><span data-stu-id="c4a88-138">As far as .NET is concerned they are different types in different assemblies.</span></span>

>[!div class="step-by-step"]
><span data-ttu-id="c4a88-139">[Poprzedni](cross-platform-targeting.md) 
> [Dalej](nuget.md)</span><span class="sxs-lookup"><span data-stu-id="c4a88-139">[Previous](cross-platform-targeting.md)
[Next](nuget.md)</span></span>
