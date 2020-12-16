---
title: Rozwiązywanie załadowań zestawów
description: W tym artykule opisano zdarzenie .NET AppDomain. AssemblyResolve. Użyj tego zdarzenia dla aplikacji, które wymagają kontroli nad ładowaniem zestawu.
ms.date: 12/15/2020
helpviewer_keywords:
- assemblies [.NET], resolving loads
- application domains, loading assemblies
- resolving assembly loads
- assemblies [.NET], loading
- application domains, resolving assembly loads
ms.assetid: 5099e549-f4fd-49fb-a290-549edd456c6a
dev_langs:
- csharp
- vb
- cpp
ms.openlocfilehash: 63545db31a4290ce933da45c0957dfdb2a00701c
ms.sourcegitcommit: e301979e3049ce412d19b094c60ed95b316a8f8c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/16/2020
ms.locfileid: "97593867"
---
# <a name="resolve-assembly-loads"></a><span data-ttu-id="51c26-104">Rozwiązywanie załadowań zestawów</span><span class="sxs-lookup"><span data-stu-id="51c26-104">Resolve assembly loads</span></span>

<span data-ttu-id="51c26-105">Platforma .NET udostępnia <xref:System.AppDomain.AssemblyResolve?displayProperty=nameWithType> zdarzenie dla aplikacji, które wymagają większej kontroli nad ładowaniem zestawu.</span><span class="sxs-lookup"><span data-stu-id="51c26-105">.NET provides the <xref:System.AppDomain.AssemblyResolve?displayProperty=nameWithType> event for applications that require greater control over assembly loading.</span></span> <span data-ttu-id="51c26-106">Dzięki obsłudze tego zdarzenia aplikacja może załadować zestaw do kontekstu obciążenia spoza normalnej ścieżki sondowania, wybrać kilka wersji zestawu do załadowania, emitować zestaw dynamiczny i zwrócić go i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="51c26-106">By handling this event, your application can load an assembly into the load context from outside the normal probing paths, select which of several assembly versions to load, emit a dynamic assembly and return it, and so on.</span></span> <span data-ttu-id="51c26-107">Ten temat zawiera wskazówki dotyczące obsługi <xref:System.AppDomain.AssemblyResolve> zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="51c26-107">This topic provides guidance for handling the <xref:System.AppDomain.AssemblyResolve> event.</span></span>

> [!NOTE]
> <span data-ttu-id="51c26-108">W celu rozpoznawania obciążeń zestawów w kontekście tylko odbicia należy <xref:System.AppDomain.ReflectionOnlyAssemblyResolve?displayProperty=nameWithType> zamiast tego użyć zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="51c26-108">For resolving assembly loads in the reflection-only context, use the <xref:System.AppDomain.ReflectionOnlyAssemblyResolve?displayProperty=nameWithType> event instead.</span></span>

## <a name="how-the-assemblyresolve-event-works"></a><span data-ttu-id="51c26-109">Jak działa zdarzenie AssemblyResolve</span><span class="sxs-lookup"><span data-stu-id="51c26-109">How the AssemblyResolve event works</span></span>

<span data-ttu-id="51c26-110">Po zarejestrowaniu procedury obsługi dla <xref:System.AppDomain.AssemblyResolve> zdarzenia program obsługi jest wywoływany za każdym razem, gdy środowisko uruchomieniowe nie zostanie powiązane z zestawem według nazwy.</span><span class="sxs-lookup"><span data-stu-id="51c26-110">When you register a handler for the <xref:System.AppDomain.AssemblyResolve> event, the handler is invoked whenever the runtime fails to bind to an assembly by name.</span></span> <span data-ttu-id="51c26-111">Na przykład wywoływanie następujących metod z kodu użytkownika może spowodować <xref:System.AppDomain.AssemblyResolve> podniesienie poziomu zdarzenia:</span><span class="sxs-lookup"><span data-stu-id="51c26-111">For example, calling the following methods from user code can cause the <xref:System.AppDomain.AssemblyResolve> event to be raised:</span></span>

- <span data-ttu-id="51c26-112"><xref:System.AppDomain.Load%2A?displayProperty=nameWithType>Przeciążenie metody lub <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> Przeciążenie metody, których pierwszy argument jest ciągiem, który reprezentuje nazwę wyświetlaną zestawu do załadowania (czyli ciąg zwracany przez <xref:System.Reflection.Assembly.FullName%2A?displayProperty=nameWithType> Właściwość).</span><span class="sxs-lookup"><span data-stu-id="51c26-112">An <xref:System.AppDomain.Load%2A?displayProperty=nameWithType> method overload or <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> method overload whose first argument is a string that represents the display name of the assembly to load (that is, the string returned by the <xref:System.Reflection.Assembly.FullName%2A?displayProperty=nameWithType> property).</span></span>

- <span data-ttu-id="51c26-113"><xref:System.AppDomain.Load%2A?displayProperty=nameWithType>Przeciążenie metody lub <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> Przeciążenie metody, których pierwszy argument jest <xref:System.Reflection.AssemblyName> obiektem, który identyfikuje zestaw do załadowania.</span><span class="sxs-lookup"><span data-stu-id="51c26-113">An <xref:System.AppDomain.Load%2A?displayProperty=nameWithType> method overload or <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> method overload whose first argument is an <xref:System.Reflection.AssemblyName> object that identifies the assembly to load.</span></span>

- <span data-ttu-id="51c26-114"><xref:System.Reflection.Assembly.LoadWithPartialName%2A?displayProperty=nameWithType>Przeciążenie metody.</span><span class="sxs-lookup"><span data-stu-id="51c26-114">An <xref:System.Reflection.Assembly.LoadWithPartialName%2A?displayProperty=nameWithType> method overload.</span></span>

- <span data-ttu-id="51c26-115"><xref:System.AppDomain.CreateInstance%2A?displayProperty=nameWithType> <xref:System.AppDomain.CreateInstanceAndUnwrap%2A?displayProperty=nameWithType> Przeciążenie metody lub, które tworzy wystąpienie obiektu w innej domenie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="51c26-115">An <xref:System.AppDomain.CreateInstance%2A?displayProperty=nameWithType> or <xref:System.AppDomain.CreateInstanceAndUnwrap%2A?displayProperty=nameWithType> method overload that instantiates an object in another application domain.</span></span>

## <a name="what-the-event-handler-does"></a><span data-ttu-id="51c26-116">Działanie programu obsługi zdarzeń</span><span class="sxs-lookup"><span data-stu-id="51c26-116">What the event handler does</span></span>

<span data-ttu-id="51c26-117">Procedura obsługi dla <xref:System.AppDomain.AssemblyResolve> zdarzenia otrzymuje nazwę wyświetlaną zestawu, który ma zostać załadowany we <xref:System.ResolveEventArgs.Name%2A?displayProperty=nameWithType> właściwości.</span><span class="sxs-lookup"><span data-stu-id="51c26-117">The handler for the <xref:System.AppDomain.AssemblyResolve> event receives the display name of the assembly to be loaded, in the <xref:System.ResolveEventArgs.Name%2A?displayProperty=nameWithType> property.</span></span> <span data-ttu-id="51c26-118">Jeśli program obsługi nie rozpoznaje nazwy zestawu, zwraca `null` (C#), `Nothing` (Visual Basic) lub `nullptr` (Visual C++).</span><span class="sxs-lookup"><span data-stu-id="51c26-118">If the handler does not recognize the assembly name, it returns `null` (C#), `Nothing` (Visual Basic), or `nullptr` (Visual C++).</span></span>

<span data-ttu-id="51c26-119">Jeśli program obsługi rozpoznaje nazwę zestawu, może ładować i zwracać zestaw, który spełnia żądanie.</span><span class="sxs-lookup"><span data-stu-id="51c26-119">If the handler recognizes the assembly name, it can load and return an assembly that satisfies the request.</span></span> <span data-ttu-id="51c26-120">Na poniższej liście opisano kilka przykładowych scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="51c26-120">The following list describes some sample scenarios.</span></span>

- <span data-ttu-id="51c26-121">Jeśli program obsługi wie lokalizację wersji zestawu, może załadować zestaw za pomocą <xref:System.Reflection.Assembly.LoadFrom%2A?displayProperty=nameWithType> <xref:System.Reflection.Assembly.LoadFile%2A?displayProperty=nameWithType> metody lub i może zwrócić załadowany zestaw, jeśli zakończono pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="51c26-121">If the handler knows the location of a version of the assembly, it can load the assembly by using the <xref:System.Reflection.Assembly.LoadFrom%2A?displayProperty=nameWithType> or <xref:System.Reflection.Assembly.LoadFile%2A?displayProperty=nameWithType> method, and can return the loaded assembly if successful.</span></span>

- <span data-ttu-id="51c26-122">Jeśli program obsługi ma dostęp do bazy danych zestawów przechowywanych jako tablice bajtowe, może załadować tablicę bajtową przy użyciu jednego z <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> przeciążeń metody przyjmujących tablicę bajtów.</span><span class="sxs-lookup"><span data-stu-id="51c26-122">If the handler has access to a database of assemblies stored as byte arrays, it can load a byte array by using one of the <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> method overloads that take a byte array.</span></span>

- <span data-ttu-id="51c26-123">Program obsługi może wygenerować zestaw dynamiczny i zwrócić go.</span><span class="sxs-lookup"><span data-stu-id="51c26-123">The handler can generate a dynamic assembly and return it.</span></span>

> [!NOTE]
> <span data-ttu-id="51c26-124">Program obsługi musi załadować zestaw do kontekstu ładowania z w kontekście ładowania lub bez kontekstu.</span><span class="sxs-lookup"><span data-stu-id="51c26-124">The handler must load the assembly into the load-from context, into the load context, or without context.</span></span> <span data-ttu-id="51c26-125">Jeśli program obsługi ładuje zestaw do kontekstu "tylko odbicie" przy użyciu <xref:System.Reflection.Assembly.ReflectionOnlyLoad%2A?displayProperty=nameWithType> <xref:System.Reflection.Assembly.ReflectionOnlyLoadFrom%2A?displayProperty=nameWithType> metody lub, próba załadowania, która wywołała <xref:System.AppDomain.AssemblyResolve> zdarzenie, kończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="51c26-125">If the handler loads the assembly into the reflection-only context by using the <xref:System.Reflection.Assembly.ReflectionOnlyLoad%2A?displayProperty=nameWithType> or the <xref:System.Reflection.Assembly.ReflectionOnlyLoadFrom%2A?displayProperty=nameWithType> method, the load attempt that raised the <xref:System.AppDomain.AssemblyResolve> event fails.</span></span>

<span data-ttu-id="51c26-126">Do zwrócenia odpowiedniego zestawu jest odpowiedzialna procedura obsługi zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="51c26-126">It is the responsibility of the event handler to return a suitable assembly.</span></span> <span data-ttu-id="51c26-127">Program obsługi może przeanalizować nazwę wyświetlaną żądanego zestawu, przekazując <xref:System.ResolveEventArgs.Name%2A?displayProperty=nameWithType> wartość właściwości do <xref:System.Reflection.AssemblyName.%23ctor%28System.String%29> konstruktora.</span><span class="sxs-lookup"><span data-stu-id="51c26-127">The handler can parse the display name of the requested assembly by passing the <xref:System.ResolveEventArgs.Name%2A?displayProperty=nameWithType> property value to the <xref:System.Reflection.AssemblyName.%23ctor%28System.String%29> constructor.</span></span> <span data-ttu-id="51c26-128">Począwszy od .NET Framework 4, program obsługi może użyć właściwości, <xref:System.ResolveEventArgs.RequestingAssembly%2A?displayProperty=nameWithType> Aby określić, czy bieżące żądanie jest zależne od innego zestawu.</span><span class="sxs-lookup"><span data-stu-id="51c26-128">Beginning with the .NET Framework 4, the handler can use the <xref:System.ResolveEventArgs.RequestingAssembly%2A?displayProperty=nameWithType> property to determine whether the current request is a dependency of another assembly.</span></span> <span data-ttu-id="51c26-129">Te informacje mogą ułatwić zidentyfikowanie zestawu, który będzie spełniał zależność.</span><span class="sxs-lookup"><span data-stu-id="51c26-129">This information can help identify an assembly that will satisfy the dependency.</span></span>

<span data-ttu-id="51c26-130">Program obsługi zdarzeń może zwrócić inną wersję zestawu niż żądana wersja.</span><span class="sxs-lookup"><span data-stu-id="51c26-130">The event handler can return a different version of the assembly than the version that was requested.</span></span>

<span data-ttu-id="51c26-131">W większości przypadków zestaw, który jest zwracany przez program obsługi, pojawia się w kontekście ładowania, niezależnie od kontekstu, w którym program obsługi ładuje go do.</span><span class="sxs-lookup"><span data-stu-id="51c26-131">In most cases, the assembly that is returned by the handler appears in the load context, regardless of the context the handler loads it into.</span></span> <span data-ttu-id="51c26-132">Jeśli na przykład program obsługi używa <xref:System.Reflection.Assembly.LoadFrom%2A?displayProperty=nameWithType> metody do załadowania zestawu do kontekstu ładowania z, zestaw pojawia się w kontekście ładowania, gdy program obsługi zwróci go.</span><span class="sxs-lookup"><span data-stu-id="51c26-132">For example, if the handler uses the <xref:System.Reflection.Assembly.LoadFrom%2A?displayProperty=nameWithType> method to load an assembly into the load-from context, the assembly appears in the load context when the handler returns it.</span></span> <span data-ttu-id="51c26-133">Jednak w poniższym przypadku zestaw pojawia się bez kontekstu, gdy program obsługi zwróci go:</span><span class="sxs-lookup"><span data-stu-id="51c26-133">However, in the following case the assembly appears without context when the handler returns it:</span></span>

- <span data-ttu-id="51c26-134">Procedura obsługi ładuje zestaw bez kontekstu.</span><span class="sxs-lookup"><span data-stu-id="51c26-134">The handler loads an assembly without context.</span></span>

- <span data-ttu-id="51c26-135"><xref:System.ResolveEventArgs.RequestingAssembly%2A?displayProperty=nameWithType>Właściwość nie ma wartości null.</span><span class="sxs-lookup"><span data-stu-id="51c26-135">The <xref:System.ResolveEventArgs.RequestingAssembly%2A?displayProperty=nameWithType> property is not null.</span></span>

- <span data-ttu-id="51c26-136">Zestaw żądający (czyli zestaw, który jest zwracany przez <xref:System.ResolveEventArgs.RequestingAssembly%2A?displayProperty=nameWithType> Właściwość) został załadowany bez kontekstu.</span><span class="sxs-lookup"><span data-stu-id="51c26-136">The requesting assembly (that is, the assembly that is returned by the <xref:System.ResolveEventArgs.RequestingAssembly%2A?displayProperty=nameWithType> property) was loaded without context.</span></span>

<span data-ttu-id="51c26-137">Aby uzyskać informacje na temat kontekstów, zobacz <xref:System.Reflection.Assembly.LoadFrom%28System.String%29?displayProperty=nameWithType> Przeciążenie metody.</span><span class="sxs-lookup"><span data-stu-id="51c26-137">For information about contexts, see the <xref:System.Reflection.Assembly.LoadFrom%28System.String%29?displayProperty=nameWithType> method overload.</span></span>

<span data-ttu-id="51c26-138">Wiele wersji tego samego zestawu może być załadowanych do tej samej domeny aplikacji.</span><span class="sxs-lookup"><span data-stu-id="51c26-138">Multiple versions of the same assembly can be loaded into the same application domain.</span></span> <span data-ttu-id="51c26-139">Ta metoda nie jest zalecana, ponieważ może to prowadzić do problemów z przypisaniem.</span><span class="sxs-lookup"><span data-stu-id="51c26-139">This practice is not recommended, because it can lead to type assignment problems.</span></span> <span data-ttu-id="51c26-140">Zapoznaj się z [najlepszymi rozwiązaniami dotyczącymi ładowania zestawu](../../framework/deployment/best-practices-for-assembly-loading.md).</span><span class="sxs-lookup"><span data-stu-id="51c26-140">See [Best practices for assembly loading](../../framework/deployment/best-practices-for-assembly-loading.md).</span></span>

## <a name="what-the-event-handler-should-not-do"></a><span data-ttu-id="51c26-141">Czego nie powinien wykonać program obsługi zdarzeń</span><span class="sxs-lookup"><span data-stu-id="51c26-141">What the event handler should not do</span></span>

<span data-ttu-id="51c26-142">Podstawową regułą obsługi <xref:System.AppDomain.AssemblyResolve> zdarzenia jest to, że nie należy próbować zwrócić zestawu, który nie jest rozpoznawany.</span><span class="sxs-lookup"><span data-stu-id="51c26-142">The primary rule for handling the <xref:System.AppDomain.AssemblyResolve> event is that you should not try to return an assembly you do not recognize.</span></span> <span data-ttu-id="51c26-143">Podczas pisania procedury obsługi należy wiedzieć, które zestawy mogą spowodować podniesienie poziomu zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="51c26-143">When you write the handler, you should know which assemblies might cause the event to be raised.</span></span> <span data-ttu-id="51c26-144">Program obsługi powinien zwrócić wartość null dla innych zestawów.</span><span class="sxs-lookup"><span data-stu-id="51c26-144">Your handler should return null for other assemblies.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="51c26-145">Począwszy od .NET Framework 4, <xref:System.AppDomain.AssemblyResolve> zdarzenie jest zgłaszane dla zestawów satelickich.</span><span class="sxs-lookup"><span data-stu-id="51c26-145">Beginning with the .NET Framework 4, the <xref:System.AppDomain.AssemblyResolve> event is raised for satellite assemblies.</span></span> <span data-ttu-id="51c26-146">Ta zmiana ma wpływ na procedurę obsługi zdarzeń, która została zapisywana dla starszej wersji .NET Framework, jeśli program obsługi podejmie próbę rozpoznania wszystkich żądań ładowania zestawu.</span><span class="sxs-lookup"><span data-stu-id="51c26-146">This change affects an event handler that was written for an earlier version of the .NET Framework, if the handler tries to resolve all assembly load requests.</span></span> <span data-ttu-id="51c26-147">Procedury obsługi zdarzeń, które ignorują zestawy, które nie są rozpoznawane, nie mają wpływ na tę zmianę: zwracają `null` i są stosowane normalne mechanizmy powrotu.</span><span class="sxs-lookup"><span data-stu-id="51c26-147">Event handlers that ignore assemblies they do not recognize are not affected by this change: They return `null`, and normal fallback mechanisms are followed.</span></span>

<span data-ttu-id="51c26-148">Podczas ładowania zestawu procedura obsługi zdarzeń nie może używać żadnych <xref:System.AppDomain.Load%2A?displayProperty=nameWithType> <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> przeciążeń lub metod, które mogą spowodować <xref:System.AppDomain.AssemblyResolve> rekursywne zdarzenie, ponieważ może to prowadzić do przepełnienia stosu.</span><span class="sxs-lookup"><span data-stu-id="51c26-148">When loading an assembly, the event handler must not use any of the <xref:System.AppDomain.Load%2A?displayProperty=nameWithType> or <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> method overloads that can cause the <xref:System.AppDomain.AssemblyResolve> event to be raised recursively, because this can lead to a stack overflow.</span></span> <span data-ttu-id="51c26-149">(Zobacz listę znajdującą się wcześniej w tym temacie). Dzieje się tak nawet wtedy, gdy podajesz obsługę wyjątków dla żądania ładowania, ponieważ żaden wyjątek nie jest zgłaszany do momentu zwrócenia wszystkich programów obsługi zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="51c26-149">(See the list provided earlier in this topic.) This happens even if you provide exception handling for the load request, because no exception is thrown until all event handlers have returned.</span></span> <span data-ttu-id="51c26-150">W rezultacie następujący kod powoduje przepełnienie stosu, jeśli `MyAssembly` nie zostanie znaleziony:</span><span class="sxs-lookup"><span data-stu-id="51c26-150">Thus, the following code results in a stack overflow if `MyAssembly` is not found:</span></span>

```csharp
using System;
using System.Reflection;

class BadExample
{
    static void Main()
    {
        AppDomain ad = AppDomain.CreateDomain("Test");
        ad.AssemblyResolve += MyHandler;

        try
        {
            object obj = ad.CreateInstanceAndUnwrap(
                "MyAssembly, version=1.2.3.4, culture=neutral, publicKeyToken=null",
                "MyType");
        }
        catch (Exception ex)
        {
            Console.WriteLine(ex.Message);
        }
    }

    static Assembly MyHandler(object source, ResolveEventArgs e)
    {
        Console.WriteLine("Resolving {0}", e.Name);
        // DO NOT DO THIS: This causes a StackOverflowException
        return Assembly.Load(e.Name);
    }
}

/* This example produces output similar to the following:

Resolving MyAssembly, Version=1.2.3.4, Culture=neutral, PublicKeyToken=null
Resolving MyAssembly, Version=1.2.3.4, Culture=neutral, PublicKeyToken=null
...
Resolving MyAssembly, Version=1.2.3.4, Culture=neutral, PublicKeyToken=null
Resolving MyAssembly, Version=1.2.3.4, Culture=neutral, PublicKeyToken=null

Process is terminated due to StackOverflowException.
 */
```

```vb
Imports System.Reflection

Class BadExample

    Shared Sub Main()

        Dim ad As AppDomain = AppDomain.CreateDomain("Test")
        AddHandler ad.AssemblyResolve, AddressOf MyHandler

        Try
            Dim obj As object = ad.CreateInstanceAndUnwrap(
                "MyAssembly, version=1.2.3.4, culture=neutral, publicKeyToken=null",
                "MyType")
        Catch ex As Exception
            Console.WriteLine(ex.Message)
        End Try
    End Sub

    Shared Function MyHandler(ByVal source As Object, _
                              ByVal e As ResolveEventArgs) As Assembly
        Console.WriteLine("Resolving {0}", e.Name)
        // DO NOT DO THIS: This causes a StackOverflowException
        Return Assembly.Load(e.Name)
    End Function
End Class

' This example produces output similar to the following:
'
'Resolving MyAssembly, Version=1.2.3.4, Culture=neutral, PublicKeyToken=null
'Resolving MyAssembly, Version=1.2.3.4, Culture=neutral, PublicKeyToken=null
'...
'Resolving MyAssembly, Version=1.2.3.4, Culture=neutral, PublicKeyToken=null
'Resolving MyAssembly, Version=1.2.3.4, Culture=neutral, PublicKeyToken=null
'
'Process is terminated due to StackOverflowException.
```

```cpp
using namespace System;
using namespace System::Reflection;

ref class Example
{
internal:
    static Assembly^ MyHandler(Object^ source, ResolveEventArgs^ e)
    {
        Console::WriteLine("Resolving {0}", e->Name);
        // DO NOT DO THIS: This causes a StackOverflowException
        return Assembly::Load(e->Name);
    }
};

void main()
{
    AppDomain^ ad = AppDomain::CreateDomain("Test");
    ad->AssemblyResolve += gcnew ResolveEventHandler(&Example::MyHandler);

    try
    {
        Object^ obj = ad->CreateInstanceAndUnwrap(
            "MyAssembly, version=1.2.3.4, culture=neutral, publicKeyToken=null",
            "MyType");
    }
    catch (Exception^ ex)
    {
        Console::WriteLine(ex->Message);
    }
}

/* This example produces output similar to the following:

Resolving MyAssembly, Version=1.2.3.4, Culture=neutral, PublicKeyToken=null
Resolving MyAssembly, Version=1.2.3.4, Culture=neutral, PublicKeyToken=null
...
Resolving MyAssembly, Version=1.2.3.4, Culture=neutral, PublicKeyToken=null
Resolving MyAssembly, Version=1.2.3.4, Culture=neutral, PublicKeyToken=null

Process is terminated due to StackOverflowException.
*/
```

### <a name="the-correct-way-to-handle-assemblyresolve"></a><span data-ttu-id="51c26-151">Prawidłowy sposób obsługi AssemblyResolve</span><span class="sxs-lookup"><span data-stu-id="51c26-151">The correct way to handle AssemblyResolve</span></span>

<span data-ttu-id="51c26-152">Podczas rozpoznawania zestawów z <xref:System.AppDomain.AssemblyResolve> programu obsługi zdarzeń, <xref:System.StackOverflowException> zostanie on ostatecznie wygenerowany, jeśli program obsługi użyje <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> wywołań lub <xref:System.AppDomain.Load%2A?displayProperty=nameWithType> metod.</span><span class="sxs-lookup"><span data-stu-id="51c26-152">When resolving assemblies from the <xref:System.AppDomain.AssemblyResolve> event handler, a <xref:System.StackOverflowException> will eventually be thrown if the handler uses the <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> or <xref:System.AppDomain.Load%2A?displayProperty=nameWithType> method calls.</span></span> <span data-ttu-id="51c26-153">Zamiast tego należy użyć <xref:System.Reflection.Assembly.LoadFile%2A> lub <xref:System.Reflection.Assembly.LoadFrom%2A> metod, ponieważ nie zgłaszają one `AssemblyResolve` zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="51c26-153">Instead, use <xref:System.Reflection.Assembly.LoadFile%2A> or <xref:System.Reflection.Assembly.LoadFrom%2A> methods, as they do not raise the `AssemblyResolve` event.</span></span>

<span data-ttu-id="51c26-154">Wyobraź sobie, że znajduje się `MyAssembly.dll` blisko zestawu wykonawczego, w znanej lokalizacji można go rozwiązać przy użyciu `Assembly.LoadFile` podaną ścieżką do zestawu.</span><span class="sxs-lookup"><span data-stu-id="51c26-154">Imagine that `MyAssembly.dll` is located near the executing assembly, in a known location, it can be resolved using `Assembly.LoadFile` given the path to the assembly.</span></span>

```csharp
using System;
using System.IO;
using System.Reflection;

class CorrectExample
{
    static void Main()
    {
        AppDomain ad = AppDomain.CreateDomain("Test");
        ad.AssemblyResolve += MyHandler;

        try
        {
            object obj = ad.CreateInstanceAndUnwrap(
                "MyAssembly, version=1.2.3.4, culture=neutral, publicKeyToken=null",
                "MyType");
        }
        catch (Exception ex)
        {
            Console.WriteLine(ex.Message);
        }
    }

    static Assembly MyHandler(object source, ResolveEventArgs e)
    {
        Console.WriteLine("Resolving {0}", e.Name);

        var path = Path.GetFullPath("../../MyAssembly.dll");
        return Assembly.LoadFile(path);
     }
}
```

```vb
Imports System.IO
Imports System.Reflection

Class CorrectExample

    Shared Sub Main()

        Dim ad As AppDomain = AppDomain.CreateDomain("Test")
        AddHandler ad.AssemblyResolve, AddressOf MyHandler

        Try
            Dim obj As Object = ad.CreateInstanceAndUnwrap(
                "MyAssembly, version=1.2.3.4, culture=neutral, publicKeyToken=null",
                "MyType")
        Catch ex As Exception
            Console.WriteLine(ex.Message)
        End Try
    End Sub

    Shared Function MyHandler(ByVal source As Object,
                              ByVal e As ResolveEventArgs) As Assembly
        Console.WriteLine("Resolving {0}", e.Name)

        Dim fullPath = Path.GetFullPath("../../MyAssembly.dll")
        Return Assembly.LoadFile(fullPath)
    End Function
End Class
```

```cpp
using namespace System;
using namespace System::IO;
using namespace System::Reflection;

ref class Example
{
internal:
    static Assembly^ MyHandler(Object^ source, ResolveEventArgs^ e)
    {
        Console::WriteLine("Resolving {0}", e->Name);

        String^ fullPath = Path::GetFullPath("../../MyAssembly.dll");
        return Assembly::LoadFile(fullPath);
    }
};

void main()
{
    AppDomain^ ad = AppDomain::CreateDomain("Test");
    ad->AssemblyResolve += gcnew ResolveEventHandler(&Example::MyHandler);

    try
    {
        Object^ obj = ad->CreateInstanceAndUnwrap(
            "MyAssembly, version=1.2.3.4, culture=neutral, publicKeyToken=null",
            "MyType");
    }
    catch (Exception^ ex)
    {
        Console::WriteLine(ex->Message);
    }
}
```

## <a name="see-also"></a><span data-ttu-id="51c26-155">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="51c26-155">See also</span></span>

- [<span data-ttu-id="51c26-156">Najlepsze rozwiązania dotyczące ładowania zestawów</span><span class="sxs-lookup"><span data-stu-id="51c26-156">Best practices for assembly loading</span></span>](../../framework/deployment/best-practices-for-assembly-loading.md)
- [<span data-ttu-id="51c26-157">Korzystanie z domen aplikacji</span><span class="sxs-lookup"><span data-stu-id="51c26-157">Use application domains</span></span>](../../framework/app-domains/use.md)
