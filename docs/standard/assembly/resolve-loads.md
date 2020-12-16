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
# <a name="resolve-assembly-loads"></a>Rozwiązywanie załadowań zestawów

Platforma .NET udostępnia <xref:System.AppDomain.AssemblyResolve?displayProperty=nameWithType> zdarzenie dla aplikacji, które wymagają większej kontroli nad ładowaniem zestawu. Dzięki obsłudze tego zdarzenia aplikacja może załadować zestaw do kontekstu obciążenia spoza normalnej ścieżki sondowania, wybrać kilka wersji zestawu do załadowania, emitować zestaw dynamiczny i zwrócić go i tak dalej. Ten temat zawiera wskazówki dotyczące obsługi <xref:System.AppDomain.AssemblyResolve> zdarzenia.

> [!NOTE]
> W celu rozpoznawania obciążeń zestawów w kontekście tylko odbicia należy <xref:System.AppDomain.ReflectionOnlyAssemblyResolve?displayProperty=nameWithType> zamiast tego użyć zdarzenia.

## <a name="how-the-assemblyresolve-event-works"></a>Jak działa zdarzenie AssemblyResolve

Po zarejestrowaniu procedury obsługi dla <xref:System.AppDomain.AssemblyResolve> zdarzenia program obsługi jest wywoływany za każdym razem, gdy środowisko uruchomieniowe nie zostanie powiązane z zestawem według nazwy. Na przykład wywoływanie następujących metod z kodu użytkownika może spowodować <xref:System.AppDomain.AssemblyResolve> podniesienie poziomu zdarzenia:

- <xref:System.AppDomain.Load%2A?displayProperty=nameWithType>Przeciążenie metody lub <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> Przeciążenie metody, których pierwszy argument jest ciągiem, który reprezentuje nazwę wyświetlaną zestawu do załadowania (czyli ciąg zwracany przez <xref:System.Reflection.Assembly.FullName%2A?displayProperty=nameWithType> Właściwość).

- <xref:System.AppDomain.Load%2A?displayProperty=nameWithType>Przeciążenie metody lub <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> Przeciążenie metody, których pierwszy argument jest <xref:System.Reflection.AssemblyName> obiektem, który identyfikuje zestaw do załadowania.

- <xref:System.Reflection.Assembly.LoadWithPartialName%2A?displayProperty=nameWithType>Przeciążenie metody.

- <xref:System.AppDomain.CreateInstance%2A?displayProperty=nameWithType> <xref:System.AppDomain.CreateInstanceAndUnwrap%2A?displayProperty=nameWithType> Przeciążenie metody lub, które tworzy wystąpienie obiektu w innej domenie aplikacji.

## <a name="what-the-event-handler-does"></a>Działanie programu obsługi zdarzeń

Procedura obsługi dla <xref:System.AppDomain.AssemblyResolve> zdarzenia otrzymuje nazwę wyświetlaną zestawu, który ma zostać załadowany we <xref:System.ResolveEventArgs.Name%2A?displayProperty=nameWithType> właściwości. Jeśli program obsługi nie rozpoznaje nazwy zestawu, zwraca `null` (C#), `Nothing` (Visual Basic) lub `nullptr` (Visual C++).

Jeśli program obsługi rozpoznaje nazwę zestawu, może ładować i zwracać zestaw, który spełnia żądanie. Na poniższej liście opisano kilka przykładowych scenariuszy.

- Jeśli program obsługi wie lokalizację wersji zestawu, może załadować zestaw za pomocą <xref:System.Reflection.Assembly.LoadFrom%2A?displayProperty=nameWithType> <xref:System.Reflection.Assembly.LoadFile%2A?displayProperty=nameWithType> metody lub i może zwrócić załadowany zestaw, jeśli zakończono pomyślnie.

- Jeśli program obsługi ma dostęp do bazy danych zestawów przechowywanych jako tablice bajtowe, może załadować tablicę bajtową przy użyciu jednego z <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> przeciążeń metody przyjmujących tablicę bajtów.

- Program obsługi może wygenerować zestaw dynamiczny i zwrócić go.

> [!NOTE]
> Program obsługi musi załadować zestaw do kontekstu ładowania z w kontekście ładowania lub bez kontekstu. Jeśli program obsługi ładuje zestaw do kontekstu "tylko odbicie" przy użyciu <xref:System.Reflection.Assembly.ReflectionOnlyLoad%2A?displayProperty=nameWithType> <xref:System.Reflection.Assembly.ReflectionOnlyLoadFrom%2A?displayProperty=nameWithType> metody lub, próba załadowania, która wywołała <xref:System.AppDomain.AssemblyResolve> zdarzenie, kończy się niepowodzeniem.

Do zwrócenia odpowiedniego zestawu jest odpowiedzialna procedura obsługi zdarzeń. Program obsługi może przeanalizować nazwę wyświetlaną żądanego zestawu, przekazując <xref:System.ResolveEventArgs.Name%2A?displayProperty=nameWithType> wartość właściwości do <xref:System.Reflection.AssemblyName.%23ctor%28System.String%29> konstruktora. Począwszy od .NET Framework 4, program obsługi może użyć właściwości, <xref:System.ResolveEventArgs.RequestingAssembly%2A?displayProperty=nameWithType> Aby określić, czy bieżące żądanie jest zależne od innego zestawu. Te informacje mogą ułatwić zidentyfikowanie zestawu, który będzie spełniał zależność.

Program obsługi zdarzeń może zwrócić inną wersję zestawu niż żądana wersja.

W większości przypadków zestaw, który jest zwracany przez program obsługi, pojawia się w kontekście ładowania, niezależnie od kontekstu, w którym program obsługi ładuje go do. Jeśli na przykład program obsługi używa <xref:System.Reflection.Assembly.LoadFrom%2A?displayProperty=nameWithType> metody do załadowania zestawu do kontekstu ładowania z, zestaw pojawia się w kontekście ładowania, gdy program obsługi zwróci go. Jednak w poniższym przypadku zestaw pojawia się bez kontekstu, gdy program obsługi zwróci go:

- Procedura obsługi ładuje zestaw bez kontekstu.

- <xref:System.ResolveEventArgs.RequestingAssembly%2A?displayProperty=nameWithType>Właściwość nie ma wartości null.

- Zestaw żądający (czyli zestaw, który jest zwracany przez <xref:System.ResolveEventArgs.RequestingAssembly%2A?displayProperty=nameWithType> Właściwość) został załadowany bez kontekstu.

Aby uzyskać informacje na temat kontekstów, zobacz <xref:System.Reflection.Assembly.LoadFrom%28System.String%29?displayProperty=nameWithType> Przeciążenie metody.

Wiele wersji tego samego zestawu może być załadowanych do tej samej domeny aplikacji. Ta metoda nie jest zalecana, ponieważ może to prowadzić do problemów z przypisaniem. Zapoznaj się z [najlepszymi rozwiązaniami dotyczącymi ładowania zestawu](../../framework/deployment/best-practices-for-assembly-loading.md).

## <a name="what-the-event-handler-should-not-do"></a>Czego nie powinien wykonać program obsługi zdarzeń

Podstawową regułą obsługi <xref:System.AppDomain.AssemblyResolve> zdarzenia jest to, że nie należy próbować zwrócić zestawu, który nie jest rozpoznawany. Podczas pisania procedury obsługi należy wiedzieć, które zestawy mogą spowodować podniesienie poziomu zdarzenia. Program obsługi powinien zwrócić wartość null dla innych zestawów.

> [!IMPORTANT]
> Począwszy od .NET Framework 4, <xref:System.AppDomain.AssemblyResolve> zdarzenie jest zgłaszane dla zestawów satelickich. Ta zmiana ma wpływ na procedurę obsługi zdarzeń, która została zapisywana dla starszej wersji .NET Framework, jeśli program obsługi podejmie próbę rozpoznania wszystkich żądań ładowania zestawu. Procedury obsługi zdarzeń, które ignorują zestawy, które nie są rozpoznawane, nie mają wpływ na tę zmianę: zwracają `null` i są stosowane normalne mechanizmy powrotu.

Podczas ładowania zestawu procedura obsługi zdarzeń nie może używać żadnych <xref:System.AppDomain.Load%2A?displayProperty=nameWithType> <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> przeciążeń lub metod, które mogą spowodować <xref:System.AppDomain.AssemblyResolve> rekursywne zdarzenie, ponieważ może to prowadzić do przepełnienia stosu. (Zobacz listę znajdującą się wcześniej w tym temacie). Dzieje się tak nawet wtedy, gdy podajesz obsługę wyjątków dla żądania ładowania, ponieważ żaden wyjątek nie jest zgłaszany do momentu zwrócenia wszystkich programów obsługi zdarzeń. W rezultacie następujący kod powoduje przepełnienie stosu, jeśli `MyAssembly` nie zostanie znaleziony:

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

### <a name="the-correct-way-to-handle-assemblyresolve"></a>Prawidłowy sposób obsługi AssemblyResolve

Podczas rozpoznawania zestawów z <xref:System.AppDomain.AssemblyResolve> programu obsługi zdarzeń, <xref:System.StackOverflowException> zostanie on ostatecznie wygenerowany, jeśli program obsługi użyje <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> wywołań lub <xref:System.AppDomain.Load%2A?displayProperty=nameWithType> metod. Zamiast tego należy użyć <xref:System.Reflection.Assembly.LoadFile%2A> lub <xref:System.Reflection.Assembly.LoadFrom%2A> metod, ponieważ nie zgłaszają one `AssemblyResolve` zdarzenia.

Wyobraź sobie, że znajduje się `MyAssembly.dll` blisko zestawu wykonawczego, w znanej lokalizacji można go rozwiązać przy użyciu `Assembly.LoadFile` podaną ścieżką do zestawu.

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

## <a name="see-also"></a>Zobacz także

- [Najlepsze rozwiązania dotyczące ładowania zestawów](../../framework/deployment/best-practices-for-assembly-loading.md)
- [Korzystanie z domen aplikacji](../../framework/app-domains/use.md)
