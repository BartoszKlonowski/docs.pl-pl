---
title: Określanie punktu wejścia
description: Dowiedz się, jak określić punkt wejścia, który identyfikuje lokalizację funkcji w bibliotece DLL. Można zmienić nazwę funkcji, mapując punkt wejścia na inną nazwę.
ms.date: 03/30/2017
helpviewer_keywords:
- EntryPoint field
- platform invoke, attribute fields
- attribute fields in platform invoke, EntryPoint
ms.assetid: d1247f08-0965-416a-b978-e0b50652dfe3
ms.openlocfilehash: d5c6b651b3b5f19eea8e61bc17da92158be87957
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96266366"
---
# <a name="specifying-an-entry-point"></a>Określanie punktu wejścia

Punkt wejścia określa lokalizację funkcji w bibliotece DLL. W obrębie zarządzanego projektu, oryginalna nazwa lub porządkowy punkt wejścia docelowej funkcji określa tę funkcję wewnątrz międzyoperacyjnej granicy. Co więcej, możesz zmapować punkt wejścia do innej nazwy, efektywnie zmieniając nazwę funkcji.  
  
 Poniżej znajduje się lista możliwych przyczyn zmiany nazwy funkcji DLL:  
  
- Aby uniknąć używania nazw funkcji API wrażliwych na wielkość liter  
  
- Aby postępować zgodnie z istniejącymi standardami nazewnictwa  
  
- Aby pomieścić funkcje, które przyjmują różne typy danych (poprzez deklarację wielu wersji tej samej funkcji DLL)  
  
- Aby uprościć używanie API, które zawierają wersje ANSI i Unicode  
  
 Ten temat demonstruje, w jaki sposób zmienić nazwę funkcji DLL w kodzie zarządzanym.  
  
## <a name="renaming-a-function-in-visual-basic"></a>Zmiana nazwy funkcji w języku Visual Basic  

Visual Basic używa słowa kluczowego **Function** w instrukcji **DECLARE** do ustawienia <xref:System.Runtime.InteropServices.DllImportAttribute.EntryPoint?displayProperty=nameWithType> pola. Poniższy przykład pokazuje podstawową deklarację.  
  
```vb
Friend Class NativeMethods
    Friend Declare Auto Function MessageBox Lib "user32.dll" (
        ByVal hWnd As IntPtr,
        ByVal lpText As String,
        ByVal lpCaption As String,
        ByVal uType As UInteger) As Integer
End Class
```
  
Punkt wejścia **MessageBox** można zastąpić za pomocą **OknoKomunikatu** , dołączając słowo kluczowe **alias** w definicji, jak pokazano w poniższym przykładzie. W obu przykładach słowo kluczowe " **Autouzupełnianie** " eliminuje konieczność określenia wersji zestawu znaków punktu wejścia. Aby uzyskać więcej informacji na temat wybierania zestawu znaków, zobacz [Określanie zestawu znaków](specifying-a-character-set.md).  
  
```vb
Friend Class NativeMethods
    Friend Declare Auto Function MsgBox _
        Lib "user32.dll" Alias "MessageBox" (
        ByVal hWnd As IntPtr,
        ByVal lpText As String,
        ByVal lpCaption As String,
        ByVal uType As UInteger) As Integer
End Class
```
  
## <a name="renaming-a-function-in-c-and-c"></a>Zmiana nazwy funkcji w języku C# i C++  

 Można użyć pola <xref:System.Runtime.InteropServices.DllImportAttribute.EntryPoint?displayProperty=nameWithType>, aby określić funkcję DLL po nazwie lub liczbie porządkowej. Jeśli nazwa funkcji w definicji metody jest taka sama jak punkt wejścia w bibliotece DLL, nie trzeba jawnie identyfikować funkcji z polem **EntryPoint** . W innym wypadku, użyj jednego z poniższych form atrybutów, aby wskazać nazwę lub liczbę porządkową:  
  
```csharp
[DllImport("DllName", EntryPoint = "Functionname")]
[DllImport("DllName", EntryPoint = "#123")]
```
  
 Należy zauważyć, że liczba porządkowa musi być poprzedzona znakiem kratki (#).  
  
 W poniższym przykładzie pokazano, jak zastąpić element **MessageBox** w **kodzie** przy użyciu pola **EntryPoint** .  
  
```csharp
using System;
using System.Runtime.InteropServices;

internal static class NativeMethods
{
    [DllImport("user32.dll", EntryPoint = "MessageBoxA")]
    internal static extern int MessageBox(
        IntPtr hWnd, string lpText, string lpCaption, uint uType);
}
```
  
```cpp
using namespace System;
using namespace System::Runtime::InteropServices;

typedef void* HWND;
[DllImport("user32", EntryPoint = "MessageBoxA")]
extern "C" int MsgBox(
    HWND hWnd, String* lpText, String* lpCaption, unsigned int uType);
```
  
## <a name="see-also"></a>Zobacz też

- <xref:System.Runtime.InteropServices.DllImportAttribute>
- [Tworzenie prototypów w kodzie zarządzanym](creating-prototypes-in-managed-code.md)
- [Przykłady wywołań platformy](platform-invoke-examples.md)
- [Organizowanie danych w wywołaniu platformy](marshaling-data-with-platform-invoke.md)
