---
title: Dostosowywanie organizowania struktury — .NET
description: Dowiedz się, jak dostosować strukturę organizacyjną platformy .NET do natywnej reprezentacji.
ms.date: 01/18/2019
dev_langs:
- csharp
- cpp
ms.openlocfilehash: c82e0099c44b8033cad241d69bdd284243711a50
ms.sourcegitcommit: e7748001b1cee80ced691d8a76ca814c0b02dd9b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/14/2020
ms.locfileid: "86374536"
---
# <a name="customize-structure-marshaling"></a>Dostosowywanie marshalingu struktur

Czasami domyślne reguły organizowania dla struktur nie są dokładnie tym, czego potrzebujesz. Środowiska uruchomieniowe platformy .NET udostępniają kilka punktów rozszerzenia, które umożliwiają dostosowanie układu struktury i sposobu organizowania pól.

## <a name="customizing-structure-layout"></a>Dostosowywanie układu struktury

Platforma .NET udostępnia <xref:System.Runtime.InteropServices.StructLayoutAttribute?displayProperty=nameWithType> atrybut i <xref:System.Runtime.InteropServices.LayoutKind?displayProperty=nameWithType> Wyliczenie umożliwiające dostosowanie sposobu umieszczania pól w pamięci. Poniższe wskazówki pomogą uniknąć typowych problemów.

✔️ ROZWAŻYĆ użycie `LayoutKind.Sequential` wszędzie tam, gdzie to możliwe.

✔️ SĄ używane tylko `LayoutKind.Explicit` w kierowaniu, gdy natywna struktura ma także jawny układ, taki jak Unia.

❌Należy unikać używania `LayoutKind.Explicit` podczas organizowania struktur na platformach innych niż Windows, jeśli trzeba przekierować środowiska uruchomieniowe przed .NET Core 3,0. Środowisko uruchomieniowe platformy .NET Core przed 3,0 nie obsługuje przekazywania jawnych struktur przez wartość do funkcji natywnych w systemach Intel lub AMD 64-bitowym z systemem innym niż Windows. Jednak środowisko uruchomieniowe obsługuje przekazywanie jawnych struktur przez odwołanie na wszystkich platformach.

## <a name="customizing-boolean-field-marshaling"></a>Dostosowywanie kierowania pola logicznego

Kod natywny ma wiele różnych reprezentacji wartości logicznych. W systemie Windows, istnieją trzy sposoby reprezentowania wartości logicznych. Środowisko uruchomieniowe nie zna natywnej definicji struktury, dlatego najlepszym rozwiązaniem jest przypuszczenie metody organizowania wartości logicznych. Środowisko uruchomieniowe platformy .NET zapewnia sposób organizowania pola wartości logicznej. W poniższych przykładach pokazano, jak skierować platformę .NET `bool` do różnych natywnych typów logicznych.

Wartości logiczne są domyślnie organizowane jako natywne 4-bajtowe [`BOOL`](/windows/desktop/winprog/windows-data-types#BOOL) wartości Win32, jak pokazano w następującym przykładzie:

```csharp
public struct WinBool
{
    public bool b;
}
```

```cpp
struct WinBool
{
    public BOOL b;
};
```

Jeśli chcesz być jawnie, możesz użyć <xref:System.Runtime.InteropServices.UnmanagedType.Bool?displayProperty=nameWithType> wartości, aby uzyskać takie samo zachowanie jak powyżej:

```csharp
public struct WinBool
{
    [MarshalAs(UnmanagedType.Bool)]
    public bool b;
}
```

```cpp
struct WinBool
{
    public BOOL b;
};
```

Korzystając z `UnmanagedType.U1` `UnmanagedType.I1` wartości lub poniżej, można powiedzieć środowisko uruchomieniowe, aby zorganizować `b` pole jako 1-bajtowy typ natywny `bool` .

```csharp
public struct CBool
{
    [MarshalAs(UnmanagedType.U1)]
    public bool b;
}
```

```cpp
struct CBool
{
    public bool b;
};
```

W systemie Windows można użyć wartości, <xref:System.Runtime.InteropServices.UnmanagedType.VariantBool?displayProperty=nameWithType> aby poinformować środowisko uruchomieniowe o kierowaniu wartości logicznej do wartości 2-bajtowej `VARIANT_BOOL` :

```csharp
public struct VariantBool
{
    [MarshalAs(UnmanagedType.VariantBool)]
    public bool b;
}
```

```cpp
struct VariantBool
{
    public VARIANT_BOOL b;
};
```

> [!NOTE]
> `VARIANT_BOOL`jest inna niż większość typów bool w tym `VARIANT_TRUE = -1` i `VARIANT_FALSE = 0` . Ponadto wszystkie wartości, które nie są równe, `VARIANT_TRUE` są uważane za fałszywe.

## <a name="customizing-array-field-marshaling"></a>Dostosowywanie organizowania pól tablicy

Platforma .NET zawiera również kilka sposobów dostosowywania organizowania tablic.

Domyślnie program .NET kierowanie tablic jako wskaźnika do ciągłej listy elementów:

```csharp
public struct DefaultArray
{
    public int[] values;
}
```

```cpp
struct DefaultArray
{
    int* values;
};
```

Jeśli korzystasz z interfejsów API modelu COM, może być konieczne kierowanie tablic jako `SAFEARRAY*` obiektów. Można użyć <xref:System.Runtime.InteropServices.MarshalAsAttribute?displayProperty=nameWithType> i <xref:System.Runtime.InteropServices.UnmanagedType.SafeArray?displayProperty=nameWithType> wartości, aby określić, że środowisko uruchomieniowe ma zorganizować tablicę jako `SAFEARRAY*` :

```csharp
public struct SafeArrayExample
{
    [MarshalAs(UnmanagedType.SafeArray)]
    public int[] values;
}
```

```cpp
struct SafeArrayExample
{
    SAFEARRAY* values;
};
```

Jeśli musisz dostosować typ elementu w `SAFEARRAY` , możesz użyć <xref:System.Runtime.InteropServices.MarshalAsAttribute.SafeArraySubType?displayProperty=nameWithType> pól i, <xref:System.Runtime.InteropServices.MarshalAsAttribute.SafeArrayUserDefinedSubType?displayProperty=nameWithType> Aby dostosować dokładny typ elementu `SAFEARRAY` .

Jeśli trzeba zorganizować tablicę w miejscu, można użyć <xref:System.Runtime.InteropServices.UnmanagedType.ByValArray?displayProperty=nameWithType> wartości, aby poinformować organizatora, aby zorganizować tablicę w miejscu. W przypadku korzystania z tego organizowania należy również podać wartość <xref:System.Runtime.InteropServices.MarshalAsAttribute.SizeConst?displayProperty=nameWithType> pola dla liczby elementów w tablicy, aby środowisko uruchomieniowe prawidłowo przydzielić miejsce dla struktury.

```csharp
public struct InPlaceArray
{
    [MarshalAs(UnmanagedType.ByValArray, SizeConst = 4)]
    public int[] values;
}
```

```cpp
struct InPlaceArray
{
    int values[4];
};
```

> [!NOTE]
> Platforma .NET nie obsługuje organizowania pola tablicy o zmiennej długości jako C99 elastycznej składowej tablicy.

## <a name="customizing-string-field-marshaling"></a>Dostosowywanie organizowania pól ciągów

Platforma .NET udostępnia również szeroką gamę dostosowań do organizowania pól ciągów.

Domyślnie program .NET kierujący ciąg jako wskaźnik do ciągu zakończonego wartością null. Kodowanie zależy od wartości <xref:System.Runtime.InteropServices.StructLayoutAttribute.CharSet?displayProperty=nameWithType> pola w <xref:System.Runtime.InteropServices.StructLayoutAttribute?displayProperty=nameWithType> . Jeśli żaden atrybut nie jest określony, kodowanie jest domyślnie zgodne z kodowaniem ANSI.

```csharp
[StructLayout(LayoutKind.Sequential, CharSet = CharSet.Ansi)]
public struct DefaultString
{
    public string str;
}
```

```cpp
struct DefaultString
{
    char* str;
};
```

```csharp
[StructLayout(LayoutKind.Sequential, CharSet = CharSet.Unicode)]
public struct DefaultString
{
    public string str;
}
```

```cpp
struct DefaultString
{
    char16_t* str; // Could also be wchar_t* on Windows.
};
```

Jeśli potrzebujesz użyć innych kodowań dla różnych pól lub wolisz bardziej jawnie w definicji struktury, możesz użyć <xref:System.Runtime.InteropServices.UnmanagedType.LPStr?displayProperty=nameWithType> <xref:System.Runtime.InteropServices.UnmanagedType.LPWStr?displayProperty=nameWithType> wartości lub dla <xref:System.Runtime.InteropServices.MarshalAsAttribute?displayProperty=nameWithType> atrybutu.

```csharp
public struct AnsiString
{
    [MarshalAs(UnmanagedType.LPStr)]
    public string str;
}
```

```cpp
struct AnsiString
{
    char* str;
};
```

```csharp
public struct UnicodeString
{
    [MarshalAs(UnmanagedType.LPWStr)]
    public string str;
}
```

```cpp
struct UnicodeString
{
    char16_t* str; // Could also be wchar_t* on Windows.
};
```

Jeśli chcesz zorganizować ciągi przy użyciu kodowania UTF-8, możesz użyć <xref:System.Runtime.InteropServices.UnmanagedType.LPUTF8Str?displayProperty=nameWithType> wartości w <xref:System.Runtime.InteropServices.MarshalAsAttribute> .

```csharp
public struct UTF8String
{
    [MarshalAs(UnmanagedType.LPUTF8Str)]
    public string str;
}
```

```cpp
struct UTF8String
{
    char* str;
};
```

> [!NOTE]
> Użycie <xref:System.Runtime.InteropServices.UnmanagedType.LPUTF8Str?displayProperty=nameWithType> wymaga .NET Framework 4,7 (lub nowszych) lub .NET Core 1,1 (lub nowszych). Nie jest on dostępny w .NET Standard 2,0.

Jeśli pracujesz z interfejsami API modelu COM, może być konieczne przekierowanie ciągu jako `BSTR` . Korzystając z <xref:System.Runtime.InteropServices.UnmanagedType.BStr?displayProperty=nameWithType> wartości, można zorganizować ciąg jako `BSTR` .

```csharp
public struct BString
{
    [MarshalAs(UnmanagedType.BStr)]
    public string str;
}
```

```cpp
struct BString
{
    BSTR str;
};
```

W przypadku korzystania z interfejsu API opartego na WinRT może być konieczne zorganizowanie ciągu jako `HSTRING` . Korzystając z <xref:System.Runtime.InteropServices.UnmanagedType.HString?displayProperty=nameWithType> wartości, można zorganizować ciąg jako `HSTRING` .

```csharp
public struct HString
{
    [MarshalAs(UnmanagedType.HString)]
    public string str;
}
```

```cpp
struct BString
{
    HSTRING str;
};
```

Jeśli interfejs API wymaga przekazania ciągu w strukturze, można użyć <xref:System.Runtime.InteropServices.UnmanagedType.ByValTStr?displayProperty=nameWithType> wartości. Należy pamiętać, że kodowanie dla ciągu organizowanego przez `ByValTStr` jest określane na podstawie `CharSet` atrybutu. Ponadto wymaga, aby długość ciągu była przenoszona przez <xref:System.Runtime.InteropServices.MarshalAsAttribute.SizeConst?displayProperty=nameWithType> pole.

```csharp
[StructLayout(LayoutKind.Sequential, CharSet = CharSet.Ansi)]
public struct DefaultString
{
    [MarshalAs(UnmanagedType.ByValTStr, SizeConst = 4)]
    public string str;
}
```

```cpp
struct DefaultString
{
    char str[4];
};
```

```csharp
[StructLayout(LayoutKind.Sequential, CharSet = CharSet.Unicode)]
public struct DefaultString
{
    [MarshalAs(UnmanagedType.ByValTStr, SizeConst = 4)]
    public string str;
}
```

```cpp
struct DefaultString
{
    char16_t str[4]; // Could also be wchar_t[4] on Windows.
};
```

## <a name="customizing-decimal-field-marshaling"></a>Dostosowywanie organizowania pól dziesiętnych

Jeśli pracujesz w systemie Windows, możesz napotkać niektóre interfejsy API, które używają natywnego [ `CY` lub `CURRENCY` ](/windows/win32/api/wtypes/ns-wtypes-cy-r1) struktury. Domyślnie `decimal` Typ .net ma kierowanie do struktury natywnej [`DECIMAL`](/windows/win32/api/wtypes/ns-wtypes-decimal-r1) . Można jednak użyć <xref:System.Runtime.InteropServices.MarshalAsAttribute> <xref:System.Runtime.InteropServices.UnmanagedType.Currency?displayProperty=nameWithType> wartości z wartością, aby nakazać Organizatorowi przekonwertowanie `decimal` wartości na wartość natywną `CY` .

```csharp
public struct Currency
{
    [MarshalAs(UnmanagedType.Currency)]
    public decimal dec;
}
```

```cpp
struct Currency
{
    CY dec;
};
```

## <a name="marshal-systemobject"></a>Przeprowadzanie marshalingu`System.Object`

W systemie Windows można skierować `object` pola do kodu natywnego. Można kierować te pola do jednego z trzech typów:

- [`VARIANT`](/windows/win32/api/oaidl/ns-oaidl-variant)
- [`IUnknown*`](/windows/desktop/api/unknwn/nn-unknwn-iunknown)
- [`IDispatch*`](/windows/desktop/api/oaidl/nn-oaidl-idispatch)

Domyślnie `object` pole z określonym typem zostanie zorganizowane do `IUnknown*` obiektu, który otacza obiekt.

```csharp
public struct ObjectDefault
{
    public object obj;
}
```

```cpp
struct ObjectDefault
{
    IUnknown* obj;
};
```

Jeśli chcesz zorganizować pole obiektu do `IDispatch*` , Dodaj element <xref:System.Runtime.InteropServices.MarshalAsAttribute> z <xref:System.Runtime.InteropServices.UnmanagedType.IDispatch?displayProperty=nameWithType> wartością.

```csharp
public struct ObjectDispatch
{
    [MarshalAs(UnmanagedType.IDispatch)]
    public object obj;
}
```

```cpp
struct ObjectDispatch
{
    IDispatch* obj;
};
```

Jeśli chcesz zorganizować ją jako `VARIANT` , Dodaj element <xref:System.Runtime.InteropServices.MarshalAsAttribute> z <xref:System.Runtime.InteropServices.UnmanagedType.Struct?displayProperty=nameWithType> wartością.

```csharp
public struct ObjectVariant
{
    [MarshalAs(UnmanagedType.Struct)]
    public object obj;
}
```

```cpp
struct ObjectVariant
{
    VARIANT obj;
};
```

W poniższej tabeli opisano, jak różne typy środowiska uruchomieniowego są `obj` mapowane na różne typy przechowywane w `VARIANT` :

| Typ .NET | Typ VARIANT | | Typ .NET | Typ VARIANT |
|------------|--------------|-|----------|--------------|
|  `byte`  | `VT_UI1` |     | `System.Runtime.InteropServices.BStrWrapper` | `VT_BSTR` |
| `sbyte`  | `VT_I1`  |     | `object`  | `VT_DISPATCH` |
| `short`  | `VT_I2`  |     | `System.Runtime.InteropServices.UnknownWrapper` | `VT_UNKNOWN` |
| `ushort` | `VT_UI2` |     | `System.Runtime.InteropServices.DispatchWrapper` | `VT_DISPATCH` |
| `int`    | `VT_I4`  |     | `System.Reflection.Missing` | `VT_ERROR` |
| `uint`   | `VT_UI4` |     | `(object)null` | `VT_EMPTY` |
| `long`   | `VT_I8`  |     | `bool` | `VT_BOOL` |
| `ulong`  | `VT_UI8` |     | `System.DateTime` | `VT_DATE` |
| `float`  | `VT_R4`  |     | `decimal` | `VT_DECIMAL` |
| `double` | `VT_R8`  |     | `System.Runtime.InteropServices.CurrencyWrapper` | `VT_CURRENCY` |
| `char`   | `VT_UI2` |     | `System.DBNull` | `VT_NULL` |
| `string` | `VT_BSTR`|
