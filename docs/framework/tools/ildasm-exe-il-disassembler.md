---
title: Ildasm.exe (Dezasembler IL)
description: Użyj Ildasm.exe (IL dezasembler), który pobiera przenośny plik wykonywalny (PE) zawierający kod języka pośredniego (IL) i tworzy plik tekstowy dla Ilasm.exe.
ms.date: 03/30/2017
helpviewer_keywords:
- PE files, MSIL Disassembler
- portable executable files, MSIL Disassembler
- Ildasm.exe
- MSIL Disassembler
- text files produced by MSIL Disassembler
- disassembling file for MSIL Assembler input
ms.assetid: db27f6b2-f1ec-499e-be3a-7eecf95ca42b
ms.openlocfilehash: e94e80d0342f68098a08e184b6bf3f48c14e817b
ms.sourcegitcommit: 30a686fd4377fe6472aa04e215c0de711bc1c322
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/10/2020
ms.locfileid: "94440884"
---
# <a name="ildasmexe-il-disassembler"></a>Ildasm.exe (Dezasembler IL)

Dezasembler IL jest narzędziem towarzyszącym Asemblerowi IL ( *Ilasm.exe* ). *Ildasm.exe* pobiera przenośny plik wykonywalny (PE), który zawiera kod języka pośredniego (IL) i tworzy plik tekstowy odpowiedni jako dane wejściowe do *Ilasm.exe*.

To narzędzie jest instalowane automatycznie z programem Visual Studio. Aby uruchomić narzędzie, użyj wiersz polecenia dla deweloperów dla programu Visual Studio (lub wiersza polecenia programu Visual Studio w systemie Windows 7). Aby uzyskać więcej informacji, zobacz [wiersza polecenia](developer-command-prompt-for-vs.md).

W wierszu polecenia wpisz następujące polecenie:

## <a name="syntax"></a>Składnia

```console
ildasm [options] [PEfilename] [options]
```

## <a name="parameters"></a>Parametry

Dostępne są następujące opcje dla plików *exe* , *dll* , *obj* , *lib* i *winmd* .

| Opcja | Opis |
| ------ | ----------- |
|**/out =**`filename`|Tworzy plik wyjściowy z określonym `filename` , zamiast wyświetlać wyniki w graficznym interfejsie użytkownika.|
|**/rtf**|Generuje wyjście w formacie RTF. Nieprawidłowa z opcją **/Text** .|
|**/Text**|Wyświetla wyniki w oknie konsoli, a nie w graficznym interfejsie użytkownika czy plik wyjściowy.|
|**/html**|Generuje wyjście w formacie HTML. Prawidłowy tylko z opcją **/Output** .|
|**/?**|Wyświetla składnię polecenia i opcje narzędzia.|

Następujące dodatkowe opcje są dostępne dla plików *exe* , *dll* i *winmd* .

| Opcja | Opis |
| ------ | ----------- |
|**/bytes**|Pokazuje rzeczywiste bajty w formacie szesnastkowym, jak mówi instrukcja.|
|**/caverbal**|Generuje obiekty typu blob niestandardowych atrybutów w formie słownej. Domyślnie jest to forma binarna.|
|**/linenum**|Dołącza odwołania do oryginalnych wierszy źródłowych.|
|**/nobar**|Pomija wyskakujące okienko ze wskaźnikiem postępu dezasemblera.|
|**/noca**|Pomija wyjście niestandardowych atrybutów.|
|**/Project**|Wyświetla metadane, tak jak pojawiają się one w kodzie zarządzanym, a nie w sposób pojawiający się w środowisko wykonawcze systemu Windows macierzystym. Jeśli `PEfilename` nie jest plikiem metadanych systemu Windows ( *winmd* ), ta opcja nie ma żadnego wpływu. Zobacz [.NET Framework obsługa aplikacji do sklepu Windows i środowisko wykonawcze systemu Windows](../cross-platform/support-for-windows-store-apps-and-windows-runtime.md).|
|**/pubonly**|Dezasembluje tylko typy publiczne i elementy członkowskie. Odpowiednik **/Visibility: pub**.|
|**/quoteallnames**|Umieszcza wszystkie nazwy w pojedynczym cudzysłowie.|
|**/raweh**|Wyświetla klauzule obsługi błędów w pierwotnej formie.|
|**/source**|Wyświetla wiersze z oryginalnego źródła jako komentarze.|
|**/tokens**|Wyświetla tokeny metadanych klas i składowych.|
|**/Visibility:** `vis` [+`vis`...]|Dezasembluje tylko typy lub elementy członkowskie o określonej widoczności. Poniżej przedstawiono prawidłowe wartości dla `vis` :<br /><br /> **Pub** — publiczny<br /><br /> **Pri** — prywatny<br /><br /> **Farma** — rodzina<br /><br /> **ASM** — zestaw<br /><br /> **FAA** — rodzina i zestaw<br /><br /> **FOA** — rodzina lub zestaw<br /><br /> **PSC** — zakres prywatny<br /><br /> Definicje tych modyfikatorów widoczności można znaleźć w tematach <xref:System.Reflection.MethodAttributes> i <xref:System.Reflection.TypeAttributes> .|

Następujące opcje są prawidłowe dla plików *exe* , *dll* i *winmd* tylko dla plików wyjściowych w pliku lub konsoli.

| Opcja | Opis |
| ------ | ----------- |
|**/All**|Określa kombinację opcji **/header** , **/Bytes** , **/stats** , **/classlist** i **/Tokens** .|
|**/classlist**|Dołącza listę klas zdefiniowanych w module.|
|**/forward**|Używa deklaracji przekazującej klasy.|
|**/Headers**|Dołącza informacje nagłówka pliku do wyjścia.|
|**/Item:** `class` [ **::** `member` [`(sig`]]|W zależności od określonego argumentu dezasembluje następujące obiekty:<br /><br /> — Rozkłada określony `class` .<br />— Rozkłada określony `member` z `class` .<br />— Rozkłada z z `member` `class` określoną sygnaturą `sig` . Format `sig` jest:<br />     [`instance`] `returnType`(`parameterType1`, `parameterType2`, …, `parameterTypeN`)<br />     **Uwaga** W .NET Framework wersje 1,0 i 1,1 `sig` muszą następować nawiasy zamykające: `(sig)` . Począwszy od platformy NET Framework 2,0 nawias zamykający musi zostać pominięty: `(sig` .|
|**/noil**|Wyłącza wyjście kodu zestawu IL.|
|**/stats**|Zawiera dane statystyczne dotyczące obrazu.|
|**/typelist**|Generuje pełną listę typów, aby zachować kolejność typów w rundzie.|
|**/unicode**|Używa kodowania Unicode danych wyjściowych.|
|**/utf8**|Używa kodowania UTF-8 danych wyjściowych. Domyślne jest ANSI.|

Następujące opcje są prawidłowe dla plików *exe* , *dll* , *obj* , *lib* i *winmd* tylko w przypadku plików wyjściowych w pliku lub konsoli.

| Opcja | Opis |
| ------ | ----------- |
|**/Metadata** [= `specifier` ]|Pokazuje metadane, gdzie `specifier` :<br /><br /> **MDHEADER** — wyświetla informacje i rozmiary nagłówka metadanych.<br /><br /> **HEX** — Pokaż informacje w postaci szesnastkowej, a także słowa.<br /><br /> **CSV** — pokazuje liczbę rekordów i rozmiary sterty.<br /><br /> **UNREX** — Pokaż nierozpoznane zewnętrzne.<br /><br /> **Schemat** — pokazuje nagłówek metadanych i informacje o schemacie.<br /><br /> **RAW** — wyświetlanie nieprzetworzonych tabel metadanych.<br /><br /> **Sterty** — Pokaż nieprzetworzone sterty.<br /><br /> **Sprawdź** poprawność — Sprawdź spójność metadanych.<br /><br /> Można określić **/Metadata** wiele razy, z różnymi wartościami dla `specifier` .|

Poniższe opcje są prawidłowe dla plików *lib* tylko dla plików wyjściowych w pliku lub konsoli.

| Opcja | Opis |
| ------ | ----------- |
|**/objectfile**=`filename`|Wyświetla metadane pojedynczego pliku obiektu w określonej bibliotece.|

> [!NOTE]
> Wszystkie opcje dla *Ildasm.exe* nie uwzględniają wielkości liter i są rozpoznawane przez pierwsze trzy litery. Na przykład **/quo** jest odpowiednikiem **/quoteallnames**. Opcje, które określają argumenty, akceptują dwukropek (:) lub znak równości (=) jako separator między opcją a argumentem. Na przykład **/Output:** *filename* jest równoważne **/Output =** *filename*.

## <a name="remarks"></a>Uwagi

*Ildasm.exe* działa tylko na plikach PE na dysku. Nie wykonuje operacji na plikach zainstalowanych w globalnej pamięci podręcznej zestawów.

Plik tekstowy utworzony przez *Ildasm.exe* może być używany jako dane wejściowe do asemblera IL ( *Ilasm.exe* ). Jest to przydatne na przykład podczas kompilowania kodu w języku programowania, który nie obsługuje wszystkich atrybutów metadanych środowiska uruchomieniowego. Po skompilowaniu kodu i uruchomieniu jego danych wyjściowych za pomocą *Ildasm.exe* , wynikowy plik tekstowy Il może być edytowany ręcznie w celu dodania brakujących atrybutów. Następnie można przetworzyć ten plik tekstowym Asemblerem IL, aby wygenerować ostateczny plik wykonywalny.

> [!NOTE]
> Obecnie nie można używać tej techniki w połączeniu z plikami PE zawierającymi osadzony kod natywny (na przykład pliki PE generowane przez program Visual C++).  

Można użyć domyślnego graficznego interfejsu użytkownika dezasemblera IL, aby wyświetlić metadane i zdezasemblowany kod jakiegokolwiek istniejącego pliku PE w hierarchicznym widoku drzewa. Aby użyć graficznego interfejsu użytkownika, wpisz **Ildasm** w wierszu polecenia bez podawania argumentu *PEfilename* ani żadnych opcji. Z menu **plik** można przejść do pliku PE, który ma zostać załadowany do *Ildasm.exe*. Aby zapisać metadane i rozłożony kod wyświetlany dla wybranego środowiska PE, wybierz polecenie **Zrzuć** z menu **plik** . Aby zapisać hierarchiczny widok drzewa, wybierz polecenie **Zrzuć TreeView** z menu **plik** . Aby uzyskać szczegółowy przewodnik po załadowaniu pliku do *Ildasm.exe* i interpretacji danych wyjściowych, zobacz samouczek *Ildasm.exe* znajdujący się w folderze Samples, który jest dostarczany z Windows SDK.

W przypadku podania *Ildasm.exe* z argumentem *PEfilename* zawierającym osadzone zasoby narzędzie tworzy wiele plików wyjściowych: plik tekstowy zawierający kod IL oraz, dla każdego osadzonego zasobu zarządzanego, plik resources utworzony przy użyciu nazwy zasobu z metadanych. Jeśli zasób niezarządzany jest osadzony w *PEfilename* , plik. res jest tworzony przy użyciu nazwy pliku określonej dla danych wyjściowych Il przez opcję **/Output** .

> [!NOTE]
> *Ildasm.exe* wyświetla tylko opisy metadanych dla plików wejściowych *. obj* i *. lib* . Kod IL dla tych typów plików nie jest dezasemblowany.

Można uruchomić *Ildasm.exe* za pośrednictwem pliku an.exe lub *. dll* , aby określić, czy plik jest zarządzany. Jeśli plik nie jest zarządzany, narzędzie wyświetli komunikat informujący, że plik nie ma prawidłowego nagłówka środowiska uruchomieniowego języka wspólnego i nie może zostać zdezasemblowany. Jeśli plik jest zarządzany, narzędzie zostanie uruchomione pomyślnie.

## <a name="version-information"></a>Informacje o wersji

Począwszy od .NET Framework 4,5, *Ildasm.exe* obsługuje nierozpoznany obiekt typu marshaler (Binary Large Object), wyświetlając nieprzetworzoną zawartość binarną. Na przykład, poniższy kod przedstawia sposób wyświetlania skierowanego obiektu typu BLOB, wygenerowanego przez program C#.

```csharp
public void Test([MarshalAs((short)70)] int test) { }
```

```il
// IL from Ildasm.exe output
.method public hidebysig instance void Test(int32  marshal({ 46 }) test) cil managed
```

Począwszy od .NET Framework 4,5, *Ildasm.exe* Wyświetla atrybuty, które są stosowane do implementacji interfejsu, jak pokazano w poniższym fragmencie wycinka z *Ildasm.exe* dane wyjściowe:

```il
.class public auto ansi beforefieldinit MyClass
  extends [mscorlib]System.Object
  implements IMyInterface
  {
    .interfaceimpl type IMyInterface
    .custom instance void
      [mscorlib]System.Diagnostics.DebuggerNonUserCodeAttribute::.ctor() = ( 01 00 00 00 )
      …
```

## <a name="examples"></a>Przykłady

Poniższe polecenie powoduje, że metadane i kod rozbudowy pliku PE są `MyHello.exe` wyświetlane w *Ildasm.exe* domyślnym interfejsie użytkownika.

```console
ildasm myHello.exe
```

Następujące polecenie odłączy plik `MyFile.exe` i zapisuje otrzymany tekst asemblera Il w pliku *myfile.Il*.

```console
ildasm MyFile.exe /output:MyFile.il
```

Następujące polecenie odłączy plik `MyFile.exe` i wyświetla otrzymany tekst asemblera Il do okna konsoli.

```console
ildasm MyFile.exe /text
```

Jeśli plik `MyApp.exe` zawiera osadzone zasoby zarządzane i niezarządzane, następujące polecenie generuje cztery pliki: *MyApp.Il* , *MojaApl. res* , *ikon. resources* i *Message. resources* :

```console
ildasm MyApp.exe /output:MyApp.il
```

Następujące polecenie odłączy metodę w `MyMethod` klasie `MyClass` w `MyFile.exe` i wyświetla dane wyjściowe do okna konsoli.

```console
ildasm /item:MyClass::MyMethod MyFile.exe /text
```

W poprzednim przykładzie może istnieć kilka metod o nazwie `MyMethod` z różnymi podpisami. Następujące polecenie deasembleruje metodę wystąpienia `MyMethod` z typem zwracanym **void** i typami parametrów **Int32** i **String**.

```console
ildasm /item:"MyClass::MyMethod(instance void(int32,string)" MyFile.exe /text
```

> [!NOTE]
> W .NET Framework wersje 1,0 i 1,1, po lewej stronie nazwy metody muszą być zrównoważone po prawej stronie po podpisie: `MyMethod(instance void(int32))` . Począwszy od .NET Framework 2,0 nawias zamykający musi zostać pominięty: `MyMethod(instance void(int32)` .

Aby pobrać `static` metodę ( `Shared` metodę w Visual Basic), Pomiń słowo kluczowe `instance` . Typy klas, które nie są typami pierwotnymi, takich jak `int32` i `string` muszą zawierać przestrzeń nazw i muszą być poprzedzone słowem kluczowym `class` . Typy zewnętrzne muszą być poprzedzone nazwą biblioteki umieszczoną w nawiasach kwadratowych. Następujące polecenie deasembleruje statyczną metodę o nazwie `MyMethod` , która ma jeden parametr typu <xref:System.AppDomain> i ma zwracany typ <xref:System.AppDomain> .

```console
ildasm /item:"MyClass::MyMethod(class [mscorlib]System.AppDomain(class [mscorlib]System.AppDomain)" MyFile.exe /text
```

Typ zagnieżdżony musi być poprzedzony klasą zawierającą i oddzielony od niej ukośnikiem. Na przykład, jeśli `MyNamespace.MyClass` Klasa zawiera zagnieżdżoną klasę o nazwie `NestedClass` , Klasa zagnieżdżona jest identyfikowana w następujący sposób: `class MyNamespace.MyClass/NestedClass` .

## <a name="see-also"></a>Zobacz też

- [Narzędzia](index.md)
- [Ilasm.exe (Asembler IL)](ilasm-exe-il-assembler.md)
- [Zarządzany proces wykonywania](../../standard/managed-execution-process.md)
- [Wiersze poleceń](developer-command-prompt-for-vs.md)
