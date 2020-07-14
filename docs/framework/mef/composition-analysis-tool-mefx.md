---
title: Narzędzie do analizy kompozycji (Mefx)
description: Przeczytaj o narzędziu do analizy kompozycji (Mefx), które analizuje pliki DLL i EXE, które zawierają części Managed Extensibility Framework (MEF) w programie .NET.
ms.date: 03/30/2017
helpviewer_keywords:
- Composition Analysis Tool [MEF]
- MEF, Composition Analysis Tool
- Mefx [MEF], Composition Analysis Tool
ms.assetid: c48a7f93-83bb-4a06-aea0-d8e7bd1502ad
ms.openlocfilehash: abb1459afc5aeb2d39ee553c62fe382bb7af58d5
ms.sourcegitcommit: 97ce5363efa88179dd76e09de0103a500ca9b659
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/13/2020
ms.locfileid: "86281280"
---
# <a name="composition-analysis-tool-mefx"></a>Narzędzie do analizy kompozycji (Mefx)
Narzędzie do analizy kompozycji (Mefx) jest aplikacją wiersza polecenia, która analizuje pliki biblioteki (. dll) i aplikacji (exe) zawierające części Managed Extensibility Framework (MEF). Głównym celem Mefx jest zapewnienie deweloperom metody diagnozowania błędów kompozycji w aplikacjach MEF, bez konieczności dodawania kodu śledzenia skomplikowany do samej aplikacji. Pomocne może być również zrozumienie części z biblioteki udostępnionej przez inną firmę. W tym temacie opisano, jak używać Mefx i zawiera odwołanie do jego składni.  
  
<a name="getting_mefx"></a>
## <a name="getting-mefx"></a>Pobieranie Mefx  
 Mefx jest dostępny w witrynie GitHub w [Managed Extensibility Framework](https://github.com/MicrosoftArchive/mef/releases/tag/4.0). Wystarczy pobrać i rozpakować narzędzie.  
  
<a name="basic_syntax"></a>
## <a name="basic-syntax"></a>Podstawowa składnia  
 Mefx jest wywoływany z wiersza polecenia w następującym formacie:  
  
```console
mefx [files and directories] [action] [options]  
```  
  
 Pierwszy zestaw argumentów określa pliki i katalogi, z których mają zostać załadowane części do analizy. Określ plik z `/file:` przełącznikiem i katalog z `/directory:` przełącznikiem. Można określić wiele plików lub katalogów, jak pokazano w następującym przykładzie:  
  
```console  
mefx /file:MyAddIn.dll /directory:Program\AddIns [action...]  
```  
  
> [!NOTE]
> Każdy plik. dll lub. exe powinien być załadowany tylko jeden raz. Jeśli plik jest ładowany wielokrotnie, narzędzie może zwracać niepoprawne informacje.  
  
 Po wyświetleniu listy plików i katalogów należy określić polecenie i wszystkie opcje dla tego polecenia.  
  
<a name="listing_available_parts"></a>
## <a name="listing-available-parts"></a>Wyświetlanie listy dostępnych części  
 Użyj `/parts` akcji, aby wyświetlić listę wszystkich części zadeklarowanych w załadowanych plikach. Wynik jest prostą listą nazw części.  
  
```console
mefx /file:MyAddIn.dll /parts  
MyAddIn.AddIn  
MyAddIn.MemberPart  
```  
  
 Aby uzyskać więcej informacji na temat części, użyj `/verbose` opcji. Spowoduje to wyjście z dodatkowych informacji dla wszystkich dostępnych części. Aby uzyskać więcej informacji na temat pojedynczej części, użyj `/type` akcji zamiast `/parts` .  
  
```console  
mefx /file:MyAddIn.dll /type:MyAddIn.AddIn /verbose  
[Part] MyAddIn.MemberPart from: AssemblyCatalog (Assembly=" MyAddIn, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null")  
  [Export] MyAddIn.MemberPart (ContractName=" MyAddIn.MemberPart")  
```  
  
<a name="listing_imports_and_exports"></a>
## <a name="listing-imports-and-exports"></a>Wyświetlanie listy importów i eksportów  
 W `/imports` `/exports` akcjach i zostaną wystawione wszystkie zaimportowane części i wszystkie wyeksportowane części. Można również wyświetlić listę składników, które zaimportują lub eksportują określony typ za `/importers` pomocą `/exporters` akcji lub.  
  
```console  
mefx /file:MyAddIn.dll /importers:MyAddin.MemberPart  
MyAddin.AddIn  
```  
  
 Można również zastosować `/verbose` opcję do tych akcji.  
  
<a name="finding_rejected_parts"></a>
## <a name="finding-rejected-parts"></a>Znajdowanie odrzuconych części  
 Po załadowaniu dostępnych części Mefx używa aparatu kompozycji MEF, aby je tworzyć. Części, które nie mogą zostać pomyślnie złożone, są określane jako *odrzucone*. Aby wyświetlić listę wszystkich odrzuconych części, użyj `/rejected` akcji.  
  
 Można użyć `/verbose` opcji z `/rejected` akcją do drukowania szczegółowych informacji o odrzuconych częściach. W poniższym przykładzie `ClassLibrary1` Biblioteka DLL zawiera `AddIn` część, która importuje `MemberPart` `ChainOne` części i. `ChainOne`Importy `ChainTwo` , ale `ChainTwo` nie istnieją. Oznacza to, że `ChainOne` odrzucono, co spowoduje `AddIn` odrzucenie.  
  
```console  
mefx /file:ClassLibrary1.dll /rejected /verbose  
```  
  
 Poniżej przedstawiono pełne dane wyjściowe poprzedniego polecenia:  
  
```output
[Part] ClassLibrary1.AddIn from: AssemblyCatalog (Assembly="ClassLibrary1, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null")  
  [Export] ClassLibrary1.AddIn (ContractName="ClassLibrary1.AddIn")  
  [Import] ClassLibrary1.AddIn.memberPart (ContractName="ClassLibrary1.MemberPart")  
    [SatisfiedBy] ClassLibrary1.MemberPart (ContractName="ClassLibrary1.MemberPart") from: ClassLibrary1.MemberPart from: AssemblyCatalog (Assembly="ClassLibrar  
y1, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null")  
  [Import] ClassLibrary1.AddIn.chain (ContractName="ClassLibrary1.ChainOne")  
    [Exception] System.ComponentModel.Composition.ImportCardinalityMismatchException: No valid exports were found that match the constraint '((exportDefinition.ContractName == "ClassLibrary1.ChainOne") AndAlso (exportDefinition.Metadata.ContainsKey("ExportTypeIdentity") AndAlso "ClassLibrary1.ChainOne".Equals(exportDefinition.Metadata.get_Item("ExportTypeIdentity"))))', invalid exports may have been rejected.  
   at System.ComponentModel.Composition.Hosting.ExportProvider.GetExports(ImportDefinition definition, AtomicComposition atomicComposition)  
   at Microsoft.ComponentModel.Composition.Diagnostics.CompositionInfo.AnalyzeImportDefinition(ExportProvider host, IEnumerable`1 availableParts, ImportDefinition id)  
    [Unsuitable] ClassLibrary1.ChainOne (ContractName="ClassLibrary1.ChainOne")  
from: ClassLibrary1.ChainOne from: AssemblyCatalog (Assembly="ClassLibrary1, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null")  
      [Because] PartDefinitionIsRejected, The part providing the export is rejected because of other issues.  
  
[Part] ClassLibrary1.ChainOne from: AssemblyCatalog (Assembly="ClassLibrary1, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null")  
  [Primary Rejection]  
  [Export] ClassLibrary1.ChainOne (ContractName="ClassLibrary1.ChainOne")  
  [Import] ClassLibrary1.ChainOne.chain (ContractName="ClassLibrary1.ChainTwo")  
    [Exception] System.ComponentModel.Composition.ImportCardinalityMismatchException: No valid exports were found that match the constraint '((exportDefinition.ContractName == "ClassLibrary1.ChainTwo") AndAlso (exportDefinition.Metadata.ContainsKey("ExportTypeIdentity") AndAlso "ClassLibrary1.ChainTwo".Equals(exportDefinition.Metadata.get_Item("ExportTypeIdentity"))))', invalid exports may have been rejected.  
   at System.ComponentModel.Composition.Hosting.ExportProvider.GetExports(ImportDefinition definition, AtomicComposition atomicComposition)  
   at Microsoft.ComponentModel.Composition.Diagnostics.CompositionInfo.AnalyzeImportDefinition(ExportProvider host, IEnumerable`1 availableParts, ImportDefinition id)  
```  
  
 Interesujące informacje są zawarte w `[Exception]` `[Unsuitable]` wynikach i. `[Exception]`Wynik zawiera informacje o tym, dlaczego część została odrzucona. `[Unsuitable]`Wynik wskazuje, dlaczego nie można użyć części dopasowywania w inny sposób, aby wypełnić import; w tym przypadku, ponieważ ta część została odrzucona w przypadku brakujących importów.  
  
<a name="analyzing_primary_causes"></a>
## <a name="analyzing-primary-causes"></a>Analizowanie przyczyn podstawowych  
 Jeśli kilka części jest połączonych w łańcuchu długich zależności, problem związany z częścią znajdującą się u dołu może spowodować odrzucenie całego łańcucha. Diagnozowanie tych problemów może być trudne, ponieważ główna przyczyna awarii nie zawsze jest oczywista. Aby pomóc w rozwiązaniu problemu, możesz użyć `/causes` akcji, która próbuje znaleźć główną przyczynę odrzucenia kaskadowego.  
  
 Użycie `/causes` akcji z poprzedniego przykładu spowoduje wyświetlenie listy informacji dla `ChainOne` , których niewypełniony import jest główną przyczyną odrzucania `AddIn` . `/causes`Akcja może być używana zarówno w normalnych, jak i w `/verbose` opcjach.  
  
> [!NOTE]
> W większości przypadków Mefx będzie mógł zdiagnozować główną przyczynę niepowodzenia kaskadowego. Jednakże w przypadkach, gdy części są dodawane programowo do kontenera, przypadki obejmujące kontenery hierarchiczne lub przypadki z implementacją niestandardową `ExportProvider` , Mefx nie będzie w stanie zdiagnozować przyczyny. Ogólnie opisane wcześniej w miarę możliwości należy unikać błędów, gdy błędy są zwykle trudne do zdiagnozowania.  
  
<a name="white_lists"></a>
## <a name="white-lists"></a>Białe listy  
 `/whitelist`Opcja umożliwia określenie pliku tekstowego zawierającego listę części, które powinny być odrzucane. Nieoczekiwane odrzucenia zostaną następnie oflagowane. Może to być przydatne podczas analizowania niekompletnej biblioteki lub podbiblioteki, w której brakuje niektórych zależności. `/whitelist`Opcja może być stosowana do `/rejected` `/causes` akcji lub.  
  
 Rozważmy plik o nazwie test.txt, który zawiera tekst "ClassLibrary1. ChainOne". Jeśli uruchomisz `/rejected` akcję z `/whitelist` opcją w poprzednim przykładzie, spowoduje to wygenerowanie następujących danych wyjściowych:  
  
```console
mefx /file:ClassLibrary1.dll /rejected /whitelist:test.txt  
[Unexpected] ClassLibrary1.AddIn  
ClassLibrary1.ChainOne  
```
