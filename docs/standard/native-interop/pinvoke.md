---
title: Wywołanie platformy (P/Invoke)
description: Dowiedz się, jak wywoływać funkcje natywne za pomocą P/Invoke w programie .NET.
ms.date: 01/18/2019
ms.openlocfilehash: cde52d9d0a4e3b84fec632b615b635e7b7df3924
ms.sourcegitcommit: 4b79862c5b41fbd86cf38f926f6a49516059f6f2
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/18/2020
ms.locfileid: "97678262"
---
# <a name="platform-invoke-pinvoke"></a>Wywołanie platformy (P/Invoke)

P/Invoke to technologia, która umożliwia dostęp do struktur, wywołań zwrotnych i funkcji w bibliotekach niezarządzanych z kodu zarządzanego. Większość interfejsu API P/Invoke jest zawarta w dwóch obszarach nazw: `System` i `System.Runtime.InteropServices` . Korzystając z tych dwóch przestrzeni nazw, można opisać, w jaki sposób chcesz komunikować się ze składnikiem macierzystym.

Zacznijmy od najbardziej typowego przykładu, który wywołuje funkcje niezarządzane w kodzie zarządzanym. Pokażmy okno komunikatu z aplikacji wiersza polecenia:

[!code-csharp[MessageBox](~/samples/snippets/standard/interop/pinvoke/messagebox.cs)]

Poprzedni przykład jest prosty, ale pokazuje, co jest potrzebne do wywołania niezarządzanych funkcji z kodu zarządzanego. Przejdźmy do przykładu:

- Wiersz #2 pokazuje instrukcję using dla `System.Runtime.InteropServices` przestrzeni nazw, która zawiera wszystkie elementy, które są zbędne.
- Wiersz #8 wprowadza `DllImport` atrybut. Ten atrybut jest decydujący, ponieważ informuje środowisko uruchomieniowe o konieczności załadowania niezarządzanej biblioteki DLL. Przekazaną ciągiem jest biblioteka DLL, w której znajduje się funkcja docelowa. Ponadto określa [zestaw znaków](./charset.md) , który ma być używany do organizowania ciągów. Na koniec określa, że ta funkcja wywołuje [SetLastError](/windows/desktop/api/errhandlingapi/nf-errhandlingapi-setlasterror) i że środowisko uruchomieniowe powinno przechwycić ten kod błędu, aby użytkownik mógł go pobrać za pośrednictwem <xref:System.Runtime.InteropServices.Marshal.GetLastWin32Error?displayProperty=nameWithType> .
- Wiersz #9 jest cruxą działania P/Invoke. Definiuje metodę zarządzaną, która ma **dokładnie taki sam podpis** jak niezarządzany. Deklaracja zawiera nowe słowo kluczowe, które można zauważyć, co oznacza, że `extern` środowisko uruchomieniowe jest metodą zewnętrzną, a po jej wywołaniu środowisko uruchomieniowe powinno je znaleźć w bibliotece DLL określonej w `DllImport` atrybucie.

Pozostała część tego przykładu właśnie wywołuje metodę tak jak każda inna metoda zarządzana.

Przykład jest podobny do macOS. Należy zmienić nazwę biblioteki w atrybucie, `DllImport` ponieważ macOS ma inny schemat nazewnictwa bibliotek dynamicznych. Poniższy przykład używa funkcji, `getpid(2)` Aby uzyskać identyfikator procesu aplikacji i wydrukować go w konsoli programu:

[!code-csharp[getpid macOS](~/samples/snippets/standard/interop/pinvoke/getpid-macos.cs)]

Jest on również podobny w systemie Linux. Nazwa funkcji jest taka sama, ponieważ `getpid(2)` jest standardowym wywołaniem systemu [POSIX](https://en.wikipedia.org/wiki/POSIX) .

[!code-csharp[getpid Linux](~/samples/snippets/standard/interop/pinvoke/getpid-linux.cs)]

## <a name="invoking-managed-code-from-unmanaged-code"></a>Wywoływanie kodu zarządzanego z niezarządzanego kodu

Środowisko uruchomieniowe umożliwia komunikację w obu kierunkach, co umożliwia wywołanie z powrotem do kodu zarządzanego z funkcji natywnych za pomocą wskaźników funkcji. Najbliższy element wskaźnika funkcji w kodzie zarządzanym jest **delegatem**, dlatego jest używany do zezwalania na wywołania zwrotne z kodu natywnego do kodu zarządzanego.

Sposób korzystania z tej funkcji jest podobny do opisanego wcześniej procesu zarządzanego do natywnego. Dla danego wywołania zwrotnego należy zdefiniować delegata, który pasuje do podpisu i przekazać go do metody zewnętrznej. Środowisko uruchomieniowe zajmie się wszystkimi innymi.

[!code-csharp[EnumWindows](~/samples/snippets/standard/interop/pinvoke/enumwindows.cs)]

Przed przeprowadzeniem tego przykładu warto przejrzeć podpisy niezarządzanych funkcji, z którymi należy się skontaktować. Funkcja, która ma zostać wywołana, aby wyliczyć wszystkie okna, ma następujący podpis: `BOOL EnumWindows (WNDENUMPROC lpEnumFunc, LPARAM lParam);`

Pierwszy parametr jest wywołaniem zwrotnym. Wymienione wywołanie zwrotne ma następujący podpis: `BOOL CALLBACK EnumWindowsProc (HWND hwnd, LPARAM lParam);`

Teraz przyjrzyjmy się przykładowi:

- Wiersz #9 w przykładzie definiuje delegata, który pasuje do sygnatury wywołania zwrotnego z kodu niezarządzanego. Zwróć uwagę, jak typy LPARAM i HWND są reprezentowane przy użyciu `IntPtr` w kodzie zarządzanym.
- Linie #13 i #14 wprowadzają `EnumWindows` funkcję z biblioteki user32.dll.
- Linie #17-20 Implementuj delegata. W tym prostym przykładzie chcemy, aby dane były wyprowadzane do konsoli.
- Na koniec w wierszu #24 Metoda zewnętrzna jest wywoływana i przenoszona do delegata.

Przykłady dla systemów Linux i macOS przedstawiono poniżej. Dla nich używana jest funkcja, `ftw` którą można znaleźć w `libc` bibliotece C. Ta funkcja służy do przechodzenia w hierarchie katalogów i przyjmuje wskaźnik do funkcji jako jeden z jej parametrów. Wymieniona funkcja ma następujący podpis: `int (*fn) (const char *fpath, const struct stat *sb, int typeflag)` .

[!code-csharp[ftw Linux](~/samples/snippets/standard/interop/pinvoke/ftw-linux.cs)]

w przykładzie macOS jest stosowana ta sama funkcja, a jedyną różnicą jest argument `DllImport` atrybutu, ponieważ macOS utrzymuje `libc` się w innym miejscu.

[!code-csharp[ftw macOS](~/samples/snippets/standard/interop/pinvoke/ftw-macos.cs)]

Oba poprzednie przykłady zależą od parametrów, a w obu przypadkach parametry są podane jako typy zarządzane. Środowisko uruchomieniowe wykonuje "prawą czynność" i przetwarza je w odpowiedniki po drugiej stronie. Dowiedz się, w jaki sposób typy są organizowane do kodu natywnego na naszej stronie podczas [organizowania typów](type-marshaling.md).

## <a name="more-resources"></a>Dodatkowe zasoby

- [PInvoke.NET wiki](https://www.pinvoke.net/) to świetna witryna typu wiki z informacjami o typowych interfejsach API systemu Windows i sposobach ich wywoływania.
- [P/Invoke w języku C++/CLI](/cpp/dotnet/native-and-dotnet-interoperability)
- [Dokumentacja narzędzia mono dla elementu P/Invoke](https://www.mono-project.com/docs/advanced/pinvoke/)
