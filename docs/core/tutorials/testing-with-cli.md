---
title: Organizowanie i testowanie projektów przy użyciu interfejs wiersza polecenia platformy .NET Core
description: W tym samouczku wyjaśniono sposób organizowania i testowania projektów programu .NET Core z poziomu wiersza polecenia.
author: cartermp
ms.date: 09/10/2018
ms.openlocfilehash: 58c78c0f11ab1b275e4e4d05bf1da32562333c91
ms.sourcegitcommit: 0a798a7e9680e2d0a5a81a3eaa203870ea782883
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/03/2020
ms.locfileid: "84325948"
---
# <a name="organizing-and-testing-projects-with-the-net-core-cli"></a>Organizowanie i testowanie projektów przy użyciu interfejs wiersza polecenia platformy .NET Core

Ten samouczek znajduje [się w samouczku: Tworzenie aplikacji konsolowej przy użyciu platformy .NET Core z użyciem Visual Studio Code, dzięki](with-visual-studio-code.md)czemu nie utworzysz prostej aplikacji konsolowej do tworzenia zaawansowanych i dobrze zorganizowanych aplikacji. Po podaniu, jak używać folderów do organizowania kodu, w tym samouczku pokazano, jak zwiększyć aplikację konsolową za pomocą platformy testowania [xUnit](https://xunit.github.io/) .

## <a name="using-folders-to-organize-code"></a>Organizowanie kodu przy użyciu folderów

Jeśli chcesz wprowadzić nowe typy do aplikacji konsoli, możesz to zrobić przez dodanie plików zawierających typy do aplikacji. Na przykład w przypadku dodawania plików zawierających `AccountInformation` i `MonthlyReportRecords` typów do projektu Struktura pliku projektu jest płaska i łatwa do przechodzenia:

```
/MyProject
|__AccountInformation.cs
|__MonthlyReportRecords.cs
|__MyProject.csproj
|__Program.cs
```

Jednak jest to dobre rozwiązanie tylko wtedy, gdy rozmiar projektu jest stosunkowo mały. Czy można przystąpić do tego, co się stanie, jeśli dodasz 20 typów do projektu? Projekt w nieskończoność nie może być w łatwy sposób przechodzenia i konserwowania w wielu plikach, w których znajduje się katalog główny projektu.

Aby zorganizować projekt, Utwórz nowy folder i nadaj mu nazwę *modele* , aby przechowywać pliki typu. Umieść pliki typu w folderze *modele* :

```
/MyProject
|__/Models
   |__AccountInformation.cs
   |__MonthlyReportRecords.cs
|__MyProject.csproj
|__Program.cs
```

Projekty, które logicznie grupują pliki do folderów, są łatwe do przechodzenia i konserwowania. W następnej sekcji utworzysz bardziej skomplikowany przykład z użyciem folderów i testów jednostkowych.

## <a name="organizing-and-testing-using-the-newtypes-pets-sample"></a>Organizowanie i testowanie przy użyciu przykładu NewTypes zwierząt domowych

### <a name="building-the-sample"></a>Kompilowanie przykładu

Poniższe kroki można wykonać przy użyciu [przykładowej NewTypes zwierząt domowych](https://github.com/dotnet/samples/tree/master/core/console-apps/NewTypesMsBuild) lub utworzyć własne pliki i foldery. Typy są logicznie zorganizowane ze strukturą folderów, która umożliwia dodanie więcej typów później, a testy są również logicznie umieszczane w folderach, co pozwala na dodanie dalszych testów później.

Przykład zawiera dwa typy `Dog` i `Cat` i ma implementację wspólnego interfejsu, `IPet` . W przypadku `NewTypes` projektu celem jest zorganizowanie typów związanych z PET w folderze *zwierząt domowych* . Jeśli później zostanie dodany inny zestaw typów, *WildAnimals* na przykład, są umieszczane w folderze *NewTypes* obok folderu *zwierzęta* . Folder *WildAnimals* może zawierać typy dla zwierząt, które nie są zwierzętami, takimi jak `Squirrel` i `Rabbit` . W ten sposób, gdy są dodawane typy, projekt pozostaje dobrze zorganizowany.

Utwórz następującą strukturę folderów z wyróżnioną zawartością pliku:

```
/NewTypes
|__/src
   |__/NewTypes
      |__/Pets
         |__Dog.cs
         |__Cat.cs
         |__IPet.cs
      |__Program.cs
      |__NewTypes.csproj
```

*IPet.cs*:

[!code-csharp[IPet interface](../../../samples/snippets/core/tutorials/testing-with-cli/csharp/src/NewTypes/Pets/IPet.cs)]

*Dog.cs*:

[!code-csharp[Dog class](../../../samples/snippets/core/tutorials/testing-with-cli/csharp/src/NewTypes/Pets/Dog.cs)]

*Cat.cs*:

[!code-csharp[Cat class](../../../samples/snippets/core/tutorials/testing-with-cli/csharp/src/NewTypes/Pets/Cat.cs)]

*Program.cs*:

[!code-csharp[Main](../../../samples/snippets/core/tutorials/testing-with-cli/csharp/src/NewTypes/Program.cs)]

*NewTypes. csproj*:

[!code-xml[NewTypes csproj](../../../samples/snippets/core/tutorials/testing-with-cli/csharp/src/NewTypes/NewTypes.csproj)]

Wykonaj następujące polecenie:

```dotnetcli
dotnet run
```

Uzyskaj następujące dane wyjściowe:

```console
Woof!
Meow!
```

Ćwiczenie opcjonalne: można dodać nowy typ PET, taki jak `Bird` , rozszerzając ten projekt. `TalkToOwner`Nadaj metodu ptakowi wartość `Tweet!` Owner. Ponownie uruchom aplikację. Dane wyjściowe będą zawierać`Tweet!`

### <a name="testing-the-sample"></a>Testowanie przykładu

`NewTypes`Projekt jest na miejscu i został zorganizowany przez utrzymywanie typów związanych ze zwierzętami ze zwierząt domowych w folderze. Następnie utwórz projekt testowy i zacznij pisać testy za pomocą platformy testów [xUnit](https://xunit.github.io/) . Testy jednostkowe umożliwiają automatyczne sprawdzanie zachowania typów PET w celu potwierdzenia, że działają prawidłowo.

Przejdź z powrotem do folderu *src* i Utwórz folder *testowy* z folderem *NewTypesTests* w nim. W wierszu polecenia w folderze *NewTypesTests* wykonaj polecenie `dotnet new xunit` . Spowoduje to utworzenie dwóch plików: *NewTypesTests. csproj* i *UnitTest1.cs*.

Projekt testowy nie może obecnie testować typów w `NewTypes` i wymaga odwołania projektu do `NewTypes` projektu. Aby dodać odwołanie do projektu, użyj [`dotnet add reference`](../tools/dotnet-add-reference.md) polecenia:

```dotnetcli
dotnet add reference ../../src/NewTypes/NewTypes.csproj
```

Lub można także ręcznie dodać odwołanie do projektu przez dodanie `<ItemGroup>` węzła do pliku *NewTypesTests. csproj* :

```xml
<ItemGroup>
  <ProjectReference Include="../../src/NewTypes/NewTypes.csproj" />
</ItemGroup>
```

*NewTypesTests. csproj*:

[!code-xml[NewTypesTests csproj](../../../samples/snippets/core/tutorials/testing-with-cli/csharp/test/NewTypesTests/NewTypesTests.csproj)]

Plik *NewTypesTests. csproj* zawiera następujące elementy:

* Odwołanie do pakietu `Microsoft.NET.Test.Sdk` , do infrastruktury testowania .NET
* Odwołanie do pakietu `xunit` , do struktury testowania xUnit
* Odwołanie do pakietu `xunit.runner.visualstudio` , do modułu uruchamiającego testy
* Odwołanie do projektu do `NewTypes` , kod do przetestowania

Zmień nazwę *UnitTest1.cs* na *PetTests.cs* i Zastąp kod w pliku następującym:

```csharp
using System;
using Xunit;
using Pets;

public class PetTests
{
    [Fact]
    public void DogTalkToOwnerReturnsWoof()
    {
        string expected = "Woof!";
        string actual = new Dog().TalkToOwner();

        Assert.NotEqual(expected, actual);
    }

    [Fact]
    public void CatTalkToOwnerReturnsMeow()
    {
        string expected = "Meow!";
        string actual = new Cat().TalkToOwner();

        Assert.NotEqual(expected, actual);
    }
}
```

Opcjonalne ćwiczenie: Jeśli wcześniej dodano `Bird` Typ, który przekazuje `Tweet!` do właściciela, Dodaj metodę testową do pliku *PetTests.cs* , `BirdTalkToOwnerReturnsTweet` Aby sprawdzić, czy `TalkToOwner` Metoda działa prawidłowo dla tego `Bird` typu.

> [!NOTE]
> Chociaż oczekuje się, że `expected` `actual` wartości i są równe, wstępne potwierdzenie ze `Assert.NotEqual` sprawdzaniem określa, że te wartości *nie są równe*. Zawsze należy utworzyć test, aby nie można było sprawdzić logiki testu. Po upewnieniu się, że test zakończy się niepowodzeniem, Dostosuj potwierdzenie, aby zezwolić na przekazanie testu.

Poniżej przedstawiono kompletną strukturę projektu:

```
/NewTypes
|__/src
   |__/NewTypes
      |__/Pets
         |__Dog.cs
         |__Cat.cs
         |__IPet.cs
      |__Program.cs
      |__NewTypes.csproj
|__/test
   |__NewTypesTests
      |__PetTests.cs
      |__NewTypesTests.csproj
```

Uruchom w katalogu *test/NewTypesTests* . Przywróć projekt testowy za pomocą [`dotnet restore`](../tools/dotnet-restore.md) polecenia. Uruchom testy za pomocą [`dotnet test`](../tools/dotnet-test.md) polecenia. To polecenie uruchamia program Test Runner określony w pliku projektu.

[!INCLUDE[DotNet Restore Note](~/includes/dotnet-restore-note.md)]

Zgodnie z oczekiwaniami testowanie nie powiedzie się, a w konsoli programu zostaną wyświetlone następujące dane wyjściowe:

```output
Test run for c:\Users\ronpet\repos\samples\core\console-apps\NewTypesMsBuild\test\NewTypesTests\bin\Debug\netcoreapp2.1\NewTypesTests.dll(.NETCoreApp,Version=v2.1)
Microsoft (R) Test Execution Command Line Tool Version 15.8.0
Copyright (c) Microsoft Corporation.  All rights reserved.

Starting test execution, please wait...
[xUnit.net 00:00:00.77]     PetTests.DogTalkToOwnerReturnsWoof [FAIL]
[xUnit.net 00:00:00.78]     PetTests.CatTalkToOwnerReturnsMeow [FAIL]
Failed   PetTests.DogTalkToOwnerReturnsWoof
Error Message:
 Assert.NotEqual() Failure
Expected: Not "Woof!"
Actual:   "Woof!"
Stack Trace:
   at PetTests.DogTalkToOwnerReturnsWoof() in c:\Users\ronpet\repos\samples\core\console-apps\NewTypesMsBuild\test\NewTypesTests\PetTests.cs:line 13
Failed   PetTests.CatTalkToOwnerReturnsMeow
Error Message:
 Assert.NotEqual() Failure
Expected: Not "Meow!"
Actual:   "Meow!"
Stack Trace:
   at PetTests.CatTalkToOwnerReturnsMeow() in c:\Users\ronpet\repos\samples\core\console-apps\NewTypesMsBuild\test\NewTypesTests\PetTests.cs:line 22

Total tests: 2. Passed: 0. Failed: 2. Skipped: 0.
Test Run Failed.
Test execution time: 1.7000 Seconds
```

Zmień potwierdzenia testów z `Assert.NotEqual` na `Assert.Equal` :

[!code-csharp[PetTests class](../../../samples/snippets/core/tutorials/testing-with-cli/csharp/test/NewTypesTests/PetTests.cs)]

Uruchom testy przy użyciu `dotnet test` polecenia i uzyskaj następujące dane wyjściowe:

```output
Test run for c:\Users\ronpet\repos\samples\core\console-apps\NewTypesMsBuild\test\NewTypesTests\bin\Debug\netcoreapp2.1\NewTypesTests.dll(.NETCoreApp,Version=v2.1)
Microsoft (R) Test Execution Command Line Tool Version 15.8.0
Copyright (c) Microsoft Corporation.  All rights reserved.

Starting test execution, please wait...

Total tests: 2. Passed: 2. Failed: 0. Skipped: 0.
Test Run Successful.
Test execution time: 1.6029 Seconds
```

Testowanie przebiega. Metody typów PET zwracają poprawne wartości podczas rozmowy z właścicielem.

Wiesz już, jak można organizować i testować projekty przy użyciu xUnit. Przejdź do tych technik, stosując je we własnych projektach. *Radosne kodowanie!*
