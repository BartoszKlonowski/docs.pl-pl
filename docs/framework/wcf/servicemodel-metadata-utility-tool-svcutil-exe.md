---
title: Narzędzie do obsługi metadanych elementu ServiceModel (Svcutil.exe)
description: Dowiedz się więcej na temat narzędzia metadanych ServiceModel, które generuje kod modelu usługi WFC z dokumentów metadanych i dokumentów metadanych z kodu modelu usługi.
ms.date: 03/30/2017
helpviewer_keywords:
- clients [WCF], building
- endpoints [WCF]
- Svcutil.exe
- clients [WCF], consuming services
ms.assetid: 1abf3d9f-b420-46f1-b628-df238751f308
ms.openlocfilehash: 65013f43aa0075b6de6999741afb448c2a35afb2
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95689930"
---
# <a name="servicemodel-metadata-utility-tool-svcutilexe"></a>Narzędzie do obsługi metadanych elementu ServiceModel (Svcutil.exe)

Narzędzie do obsługi metadanych ServiceModel służy do generowania kodu modelu usługi z dokumentów metadanych i dokumentów metadanych z kodu modelu usługi.

## <a name="svcutilexe"></a>SvcUtil.exe

Narzędzie metadanych ServiceModel można znaleźć w lokalizacji instalacji Windows SDK, w tym w *SDKs\Windows\v6.0\bin*.

### <a name="functionalities"></a>Funkcje

Poniższa tabela zawiera podsumowanie różnych funkcji oferowanych przez to narzędzie oraz odpowiadających im tematów, które omawiają sposób użycia:

|Zadanie|Temat|
|----------|-----------|
|Generuje kod z uruchomionych usług lub statycznych dokumentów metadanych.|[Generowanie klienta programu WCF na podstawie metadanych usługi](./feature-details/generating-a-wcf-client-from-service-metadata.md)|
|Eksportuje dokumenty metadanych z skompilowanego kodu.|[Instrukcje: eksportowanie metadanych ze skompilowanego kodu usługi za pomocą programu Svcutil.exe](./feature-details/how-to-use-svcutil-exe-to-export-metadata-from-compiled-service-code.md)|
|Sprawdza poprawność skompilowanego kodu usługi.|[Instrukcje: weryfikacja skompilowanego kodu usługi za pomocą programu Svcutil.exe](./feature-details/how-to-use-svcutil-exe-to-validate-compiled-service-code.md)|
|Pobiera dokumenty metadanych z uruchomionych usług.|[Instrukcje: używanie programu Svcutil.exe do pobierania dokumentów metadanych](./feature-details/how-to-use-svcutil-exe-to-download-metadata-documents.md)|
|Generuje kod serializacji.|[Instrukcje: skracanie czasu uruchamiania aplikacji klienckich programu WCF za pomocą elementu XmlSerializer](./feature-details/startup-time-of-wcf-client-applications-using-the-xmlserializer.md)|

> [!CAUTION]
> Svcutil zastępuje istniejące pliki na dysku, jeśli nazwy podane jako parametry są identyczne. Może to dotyczyć plików kodu, konfiguracji lub plików metadanych. Aby uniknąć tego podczas generowania kodu i plików konfiguracji, należy użyć `/mergeConfig` przełącznika.
>
> Ponadto `/r` `/ct` przełączniki i dla typów odwołujących są przeznaczone do generowania kontraktów danych. Te przełączniki nie działają w przypadku używania elementu XmlSerializer.

### <a name="timeout"></a>Limit czasu

Podczas pobierania metadanych narzędzie ma limit czasu równy pięć minut. Ten limit czasu dotyczy pobierania metadanych za pośrednictwem sieci. Nie dotyczy żadnego przetwarzania tych metadanych.

### <a name="multi-targeting"></a>Wiele elementów docelowych

Narzędzie nie obsługuje wielowymiarowego określania wartości docelowej. Jeśli chcesz wygenerować artefakt .NET Framework 4 z *svcutil.exe*, użyj *svcutil.exe* z zestawu SDK .NET Framework 4. Aby wygenerować artefakt .NET Framework 3,5, użyj pliku wykonywalnego z zestawu SDK .NET Framework 3,5.

### <a name="accessing-wsdl-documents"></a>Uzyskiwanie dostępu do dokumentów WSDL

W przypadku korzystania z Svcutil w celu uzyskania dostępu do dokumentu WSDL, który ma odwołanie do usługi tokenu zabezpieczającego (STS), Svcutil wykonuje wywołanie WS-MetadataExchange w usłudze STS. Jednak usługa może uwidaczniać swoje dokumenty WSDL przy użyciu WS-MetadataExchange lub HTTP GET. W związku z tym, jeśli usługa STS ma tylko uwidoczniony dokument WSDL przy użyciu polecenia HTTP GET, klient zapisany w aplikacji WinFX nie powiedzie się. W przypadku klientów utworzonych w .NET Framework 3,5 Svcutil próbuje użyć obu WS-MetadataExchange i HTTP GET w celu uzyskania WSDL języka STS.

## <a name="using-svcutilexe"></a>Używanie SvcUtil.exe

### <a name="common-usages"></a>Typowe użycia

W poniższej tabeli przedstawiono niektóre często używane opcje tego narzędzia:

|Opcja|Opis|
|------------|-----------------|
|Pliki/katalog\<directory>|Katalog, w którym mają zostać utworzone pliki.<br /><br /> Domyślnie: bieżący katalog.<br /><br /> Krótka forma: `/d`|
|/help|Wyświetla składnię polecenia i opcje narzędzia.<br /><br /> Krótka forma: `/?`|
|/noLogo|Pomijaj prawa autorskie i transparent.|
|/svcutilConfig:\<configFile>|Określa niestandardowy plik konfiguracji, który będzie używany zamiast pliku App.config. Ta wartość może służyć do rejestrowania rozszerzeń system. serviceModel bez modyfikowania pliku konfiguracji narzędzia.|
|/Target\<output type>|Określa dane wyjściowe, które mają zostać wygenerowane przez narzędzie.<br /><br /> Prawidłowe wartości to kod, Metadata lub XmlSerializer.<br /><br /> Krótka forma: `/t`|

### <a name="code-generation"></a>Generowanie kodu

Svcutil.exe może generować kod dla kontraktów usługi, klientów i typów danych z dokumentów metadanych. Te dokumenty metadanych mogą znajdować się w magazynie trwałym lub być pobierane w trybie online. Pobieranie online odbywa się przy użyciu protokołu WS-Metadata Exchange lub protokołu DISCO (Aby uzyskać szczegółowe informacje, zobacz sekcję Pobieranie metadanych).

Za pomocą narzędzia *SvcUtil.exe* można generować kontrakty usługi i danych na podstawie wstępnie zdefiniowanego dokumentu WSDL. Użyj przełącznika/serviceContract i określ adres URL lub lokalizację pliku, w którym można pobrać lub znaleźć dokument WSDL. Spowoduje to wygenerowanie kontraktów usługi i danych zdefiniowanych w dokumencie WSDL, które mogą zostać użyte do zaimplementowania usługi skargi. Aby uzyskać więcej informacji, zobacz [How to: Pobieranie metadanych i implementowanie zgodnej usługi](./feature-details/how-to-retrieve-metadata-and-implement-a-compliant-service.md).

W przypadku usługi z punktem końcowym BasicHttpContextBinding *Svcutil.exe* generuje BasicHttpBinding z `allowCookies` atrybutem ustawionym na `true` . Pliki cookie są używane dla kontekstu na serwerze. Jeśli chcesz zarządzać kontekstem na kliencie, gdy usługa korzysta z plików cookie, możesz ręcznie zmodyfikować konfigurację, aby użyć powiązania kontekstu.

> [!CAUTION]
> Svcutil.exe generuje klienta na podstawie pliku WSDL lub zasad otrzymanego z usługi. Główna nazwa użytkownika (UPN) jest generowana przez złączenie nazwy użytkownika, " \@ " i w pełni kwalifikowanej nazwy domeny (FQDN). Jednak w przypadku użytkowników, którzy zarejestrowali się w Active Directory, ten format jest nieprawidłowy, a nazwa UPN wygenerowanego przez narzędzie powoduje błąd uwierzytelniania Kerberos z komunikatem o błędzie "próba logowania nie powiodła się". Aby rozwiązać ten problem, należy ręcznie naprawić plik klienta wygenerowany przez to narzędzie.

`svcutil.exe [/t:code]  <metadataDocumentPath>* | <url>* | <epr>`

|Argument|Opis|
|--------------|-----------------|
|`epr`|Ścieżka do pliku XML, który zawiera WS-Addressing EndpointReference dla punktu końcowego usługi, który obsługuje WS-Metadata Exchange. Aby uzyskać więcej informacji, zobacz sekcję Pobieranie metadanych.|
|`metadataDocumentPath`|Ścieżka do dokumentu metadanych (*WSDL* lub *XSD*), który zawiera kontrakt do zaimportowania do kodu (. WSDL,. xsd,. WSPolicy lub. wsmex).<br /><br /> Svcutil następuje po zaimportowaniu i uwzględnieniu podczas określania zdalnego adresu URL dla metadanych. Jeśli jednak chcesz przetwarzać pliki metadanych w lokalnym systemie plików, musisz określić wszystkie pliki w tym argumencie. W ten sposób można użyć Svcutil w środowisku kompilacji, w którym nie można mieć zależności sieci. Dla tego argumentu można użyć symboli wieloznacznych (*. xsd, \* . WSDL).|
|`url`|Adres URL punktu końcowego usługi, który udostępnia metadane lub dokument metadanych hostowany w trybie online. Aby uzyskać więcej informacji na temat pobierania tych dokumentów, zobacz sekcję Pobieranie metadanych.|

|Opcja|Opis|
|------------|-----------------|
|/async|Generuje sygnatury metod synchronicznych i asynchronicznych.<br /><br /> Domyślnie: Generuj tylko sygnatury metody synchronicznej.<br /><br /> Krótka forma: `/a`|
|CollectionType\<type>|Określa typ kolekcji listy dla klienta WCF.<br/><br /> Wartość domyślna: typ kolekcji to system. Array. <br /><br /> Krótka forma: `/ct`|
|/config\<configFile>|Określa nazwę pliku dla wygenerowanego pliku konfiguracji.<br /><br /> Wartość domyślna: output.config|
|/dataContractOnly|Generuje kod tylko dla typów kontraktu danych. Typy kontraktów usług nie są generowane.<br /><br /> Należy określić tylko lokalne pliki metadanych dla tej opcji.<br /><br /> Krótka forma: `/dconly`|
|/enableDataBinding|Implementuje <xref:System.ComponentModel.INotifyPropertyChanged> interfejs we wszystkich typach kontraktu danych, aby włączyć powiązanie danych.<br /><br /> Krótka forma: `/edb`|
|/excludeType:\<type>|Określa w pełni kwalifikowaną lub kwalifikowaną dla zestawu nazwę typu, który ma zostać wykluczony z przywoływanych typów kontraktu.<br /><br /> W przypadku korzystania z tego przełącznika z `/r` oddzielnych bibliotek DLL jest przywoływana pełna nazwa klasy XSD.<br /><br /> Krótka forma: `/et`|
|/importXmlTypes|Konfiguruje serializator kontraktu danych w celu zaimportowania typów kontraktów niezwiązanych z danymi jako typów IXmlSerializable.|
|/internal|Generuje klasy, które są oznaczone jako wewnętrzne. Wartość domyślna: Generuj tylko klasy publiczne.<br /><br /> Krótka forma: `/i`|
|/Language\<language>|Określa język programowania, który ma być używany do generowania kodu. Należy podać nazwę języka zarejestrowanego w pliku Machine.config lub w pełni kwalifikowaną nazwę klasy, która dziedziczy z <xref:System.CodeDom.Compiler.CodeDomProvider> .<br /><br /> Wartości: c#, CS, CSharp, VB, VisualBasic, c++, CPP<br /><br /> Wartość domyślna: CSharp<br /><br /> Krótka forma: `/l`|
|/mergeConfig|Scala wygenerowaną konfigurację w istniejący plik, zamiast zastąpić istniejący plik.|
|/messageContract|Generuje typy kontraktów komunikatów.<br /><br /> Krótka forma: `/mc`|
|/Namespace\<string,string>|Określa mapowanie z schematu WSDL lub XML do przestrzeni nazw CLR. Użycie elementu " \* " dla elementu targetNamespace mapuje wszystkie obszary nazw targetNamespace bez jawnego mapowania na tę przestrzeń nazw środowiska CLR.<br /><br /> Aby upewnić się, że nazwa kontraktu komunikatu nie koliduje z nazwą operacji, należy zakwalifikować odwołanie do typu z lub upewnić się, `::` że nazwy są unikatowe.<br /><br /> Domyślnie: pochodna z przestrzeni nazw Target dokumentu schematu dla kontraktów danych. Domyślna przestrzeń nazw jest używana dla wszystkich innych typów wygenerowanych.<br /><br /> Krótka forma: `/n` **Uwaga:**  podczas generowania typów do użycia z elementem XmlSerializer obsługiwane jest tylko mapowanie pojedynczej przestrzeni nazw. Wszystkie wygenerowane typy będą znajdować się w domyślnej przestrzeni nazw lub w przestrzeni nazw określonej przez znak "*".|
|/noConfig|Nie Generuj plików konfiguracyjnych.|
|/noStdLib|Nie Odwołuj się do bibliotek standardowych.<br /><br /> Wartość domyślna: Mscorlib.dll i System.servicemodel.dll są przywoływane.|
|/out\<file>|Określa nazwę pliku dla wygenerowanego kodu.<br /><br /> Wartość domyślna: pochodna z nazwy definicji WSDL, nazwy usługi WSDL lub docelowej przestrzeni nazw jednego z schematów.<br /><br /> Krótka forma: `/o`|
|/Reference\<file path>|Odwołuje się do typów w określonym zestawie. Podczas generowania klientów należy użyć tej opcji, aby określić zestawy, które mogą zawierać typy reprezentujące importowane metadane.<br /><br /> Nie można określić kontraktów i <xref:System.Xml.Serialization.XmlSerializer> typów komunikatów przy użyciu tego przełącznika.<br /><br /> Jeśli <xref:System.DateTimeOffset> jest przywoływany, ten typ jest używany zamiast generowania nowego typu. Jeśli aplikacja jest zapisywana przy użyciu .NET Framework 3,5, SvcUtil.exe odwołań <xref:System.DateTimeOffset> automatycznie.<br /><br /> Krótka forma: `/r`|
|/serializable|Generuje klasy oznaczone atrybutem możliwym do serializacji.<br /><br /> Krótka forma: `/s`|
|/serviceContract|Generuj tylko kod dla kontraktów usługi. Nie Wygenerowano klasy klienta i konfiguracji<br /><br /> Krótka forma: `/sc`|
|/Serializer:|Automatycznie wybierz serializator. Spowoduje to próbę użycia serializatora kontraktu danych i użycie elementu XmlSerializer w razie niepowodzenia.<br /><br /> Krótka forma: `/ser`|
|/Serializer: DataContractSerializer|Generuje typy danych używające serializatora kontraktu danych do serializacji i deserializacji.<br /><br /> Krótka forma: `/ser:DataContractSerializer`|
|/Serializer: XmlSerializer|Generuje typy danych używające <xref:System.Xml.Serialization.XmlSerializer> do serializacji i deserializacji.<br /><br /> Krótka forma: `/ser:XmlSerializer`|
|/targetClientVersion|Określ wersję .NET Framework aplikacji docelowej. Prawidłowe wartości to `Version30` i `Version35` . Wartość domyślna to `Version30`.<br /><br /> Krótka forma: `/tcv`<br /><br /> `Version30`: Służy `/tcv:Version30` do generowania kodu dla klientów korzystających z programu WinFX.<br /><br /> `Version35`: Służy do `/tcv:Version35` generowania kodu dla klientów korzystających z .NET Framework 3,5. W przypadku użycia `/tcv:Version35` z `/async` przełącznikiem generowane są zarówno metody asynchroniczne oparte na zdarzeniach, jak i wywołania zwrotne/Delegaty. Ponadto Obsługa zestawów danych obsługujących LINQ i <xref:System.DateTimeOffset> jest włączona.|
|/wrapped|Określa, czy specjalne wielkości liter są używane dla dokumentów z stylem literału dokumentu z opakowanymi parametrami. Aby określić normalne wielkości liter, użyj przełącznika **/Wrapped** w narzędziu Narzędzie [metadanych modelu usług (Svcutil.exe)](servicemodel-metadata-utility-tool-svcutil-exe.md) .|

> [!NOTE]
> Gdy powiązanie usługi jest jednym z powiązań dostarczonych przez system (zobacz [powiązania dostarczone przez system](system-provided-bindings.md)), a <xref:System.ServiceModel.ServiceContractAttribute.ProtectionLevel%2A> Właściwość jest ustawiona na albo `None` `Sign` , Svcutil generuje plik konfiguracji przy użyciu [\<customBinding>](../configure-apps/file-schema/wcf/custombinding.md) elementu zamiast oczekiwanego elementu określonego przez system. Na przykład jeśli usługa używa `<wsHttpBinding>` elementu z `ProtectionLevel` ustawionym na `Sign` , wygenerowana konfiguracja znajduje `<customBinding>` się w sekcji powiązań zamiast `<wsHttpBinding>` . Aby uzyskać więcej informacji na temat poziomu ochrony, zobacz [Opis poziomu ochrony](understanding-protection-level.md).

### <a name="metadata-export"></a>Eksport metadanych

Svcutil.exe mogą eksportować metadane usług, kontraktów i typów danych w skompilowanych zestawach. Aby wyeksportować metadane dla usługi, należy użyć `/serviceName` opcji, aby określić usługę, którą chcesz wyeksportować. Aby wyeksportować wszystkie typy kontraktów danych w ramach zestawu, należy użyć `/dataContractOnly` opcji. Domyślnie metadane są eksportowane dla wszystkich kontraktów usługi w zestawach wejściowych.

`svcutil.exe [/t:metadata] [/serviceName:<serviceConfigName>] [/dataContractOnly] <assemblyPath>*`

|Argument|Opis|
|--------------|-----------------|
|`assemblyPath`|Określa ścieżkę do zestawu, który zawiera usługi, kontrakty lub typy kontraktów danych do wyeksportowania. Standardowe symbole wieloznaczne wiersza polecenia mogą służyć do udostępniania wielu plików jako dane wejściowe.|

|Opcja|Opis|
|------------|-----------------|
|ServiceName\<serviceConfigName>|Określa nazwę konfiguracji usługi do wyeksportowania. Jeśli ta opcja jest używana, zestaw wykonywalny ze skojarzonym plikiem konfiguracji musi zostać przesłany jako dane wejściowe. Svcutil.exe przeszukuje wszystkie skojarzone pliki konfiguracji dla konfiguracji usługi. Jeśli pliki konfiguracji zawierają jakiekolwiek typy rozszerzeń, zestawy, które zawierają te typy, muszą znajdować się w pamięci podręcznej GAC lub jawnie udostępniane przy użyciu `/reference` opcji.|
|/Reference\<file path>|Dodaje określony zestaw do zestawu zestawów używanych do rozpoznawania odwołań do typu. W przypadku eksportowania lub weryfikowania usługi używającej rozszerzeń innych firm (zachowań, powiązań i BindingElements) zarejestrowanego w konfiguracji należy użyć tej opcji, aby zlokalizować zestawy rozszerzeń, które nie znajdują się w pamięci podręcznej GAC.<br /><br /> Krótka forma: `/r`|
|/dataContractOnly|Działa tylko w przypadku typów kontraktu danych. Kontrakty usług nie są przetwarzane.<br /><br /> Należy określić tylko lokalne pliki metadanych dla tej opcji.<br /><br /> Krótka forma: `/dconly`|
|/excludeType:\<type>|Określa w pełni kwalifikowaną lub kwalifikowaną dla zestawu nazwę typu, który ma zostać wykluczony z eksportu. Tej opcji można użyć podczas eksportowania metadanych dla usługi lub zestawu kontraktów usługi w celu wykluczenia typów z eksportu. Tej opcji nie można używać razem z `/dconly` opcją.<br /><br /> W przypadku jednego zestawu zawierającego wiele usług, a każda z nich używa oddzielnych klas o tej samej nazwie XSD, należy określić nazwę usługi zamiast nazwy klasy XSD dla tego przełącznika.<br /><br /> Typy kontraktów XSD lub danych nie są obsługiwane.<br /><br /> Krótka forma: `/et`|

### <a name="service-validation"></a>Weryfikacja usługi

Walidacja może służyć do wykrywania błędów w implementacjach usług bez obsługi usługi. Musisz użyć opcji, `/serviceName` Aby wskazać usługę, którą chcesz zweryfikować.

`svcutil.exe /validate /serviceName:<serviceConfigName>  <assemblyPath>*`

|Argument|Opis|
|--------------|-----------------|
|`assemblyPath`|Określa ścieżkę do zestawu, który zawiera typy usług do zweryfikowania. Zestaw musi mieć skojarzony plik konfiguracji, aby można było dostarczyć konfigurację usługi. Standardowe symbole wieloznaczne wiersza polecenia mogą służyć do udostępniania wielu zestawów.|

|Opcja|Opis|
|------------|-----------------|
|/Validate|Sprawdza poprawność implementacji usługi określonej przez `/serviceName` opcję. Jeśli ta opcja jest używana, zestaw wykonywalny ze skojarzonym plikiem konfiguracji musi zostać przesłany jako dane wejściowe.<br /><br /> Krótka forma: `/v`|
|ServiceName\<serviceConfigName>|Określa nazwę konfiguracji usługi do zweryfikowania. Svcutil.exe przeszukuje wszystkie skojarzone pliki konfiguracyjne wszystkich zestawów wejściowych dla konfiguracji usługi. Jeśli pliki konfiguracji zawierają jakiekolwiek typy rozszerzeń, zestawy, które zawierają te typy, muszą znajdować się w pamięci podręcznej GAC lub jawnie udostępniane przy użyciu `/reference` opcji.|
|/Reference\<file path>|Dodaje określony zestaw do zestawu zestawów używanych do rozpoznawania odwołań do typu. W przypadku eksportowania lub weryfikowania usługi używającej rozszerzeń innych firm (zachowań, powiązań i BindingElements) zarejestrowanego w konfiguracji należy użyć tej opcji, aby zlokalizować zestawy rozszerzeń, które nie znajdują się w pamięci podręcznej GAC.<br /><br /> Krótka forma: `/r`|
|/dataContractOnly|Działa tylko w przypadku typów kontraktu danych. Kontrakty usług nie są przetwarzane.<br /><br /> Należy określić tylko lokalne pliki metadanych dla tej opcji.<br /><br /> Krótka forma: `/dconly`|
|/excludeType:\<type>|Określa w pełni kwalifikowaną lub kwalifikowaną dla zestawu nazwę typu, który ma zostać wykluczony z walidacji.<br /><br /> Krótka forma: `/et`|

### <a name="metadata-download"></a>Pobieranie metadanych

Svcutil.exe może służyć do pobierania metadanych z uruchomionych usług i zapisywania metadanych w plikach lokalnych. Aby pobrać metadane, należy określić `/t:metadata` opcję. W przeciwnym razie kod klienta jest generowany. W przypadku schematów adresów URL protokołu HTTP i HTTPS Svcutil.exe próbuje pobrać metadane przy użyciu WS-Metadata Exchange i DISCO. Dla wszystkich innych schematów adresów URL Svcutil.exe używa tylko WS-Metadata Exchange.

Svcutil wystawia następujące żądania metadanych jednocześnie w celu pobrania metadanych.

- Żądanie MEX (WS-transfer) do podanego adresu

- Żądanie MEX do podanego adresu z dołączonym/Mex

- Żądanie DISCO (przy użyciu DiscoveryClientProtocol z usługi ASMX) do podanego adresu.

Domyślnie Svcutil.exe używa powiązań zdefiniowanych w <xref:System.ServiceModel.Description.MetadataExchangeBindings> klasie w celu uzyskania żądań Mex. Aby skonfigurować powiązanie używane dla WS-Metadata Exchange, należy zdefiniować punkt końcowy klienta w konfiguracji, który używa kontraktu kontraktem IMetadataExchange. Można go zdefiniować w pliku konfiguracyjnym programu Svcutil.exe lub w innym pliku konfiguracyjnym określonym przy użyciu `/svcutilConfig` opcji.

`svcutil.exe /t:metadata  <url>* | <epr>`

|Argument|Opis|
|--------------|-----------------|
|`url`|Adres URL punktu końcowego usługi, który udostępnia metadane lub dokument metadanych hostowany w trybie online.|
|`epr`|Ścieżka do pliku XML, który zawiera WS-Addressing EndpointReference dla punktu końcowego usługi, który obsługuje WS-Metadata Exchange.|

### <a name="xmlserializer-type-generation"></a>Generowanie typu XmlSerializer

Usługi i aplikacje klienckie korzystające z typów danych, które można serializować przy użyciu <xref:System.Xml.Serialization.XmlSerializer> generowania i kompilowania kodu serializacji dla tych typów danych w czasie wykonywania, co może spowodować spowolnienie wydajności.

> [!NOTE]
> Wstępnie wygenerowany kod serializacji może być używany tylko w aplikacjach klienckich, a nie w usługach.

Svcutil.exe może wygenerować wymagany kod serializacji języka C# z skompilowanych zestawów dla aplikacji, a tym samym zwiększyć wydajność uruchamiania tych aplikacji. Aby uzyskać więcej informacji, zobacz [How to: ulepszanie czasu uruchamiania aplikacji klienckich WCF przy użyciu elementu XmlSerializer](./feature-details/startup-time-of-wcf-client-applications-using-the-xmlserializer.md).

> [!NOTE]
> Svcutil.exe generuje tylko kod dla typów używanych przez kontrakty usług, które znajdują się w zestawach wejściowych.

`svcutil.exe /t:xmlSerializer  <assemblyPath>*`

|Argument|Opis|
|--------------|-----------------|
|`assemblyPath`|Określa ścieżkę do zestawu, który zawiera typy kontraktu usługi. Typy serializacji są generowane dla wszystkich typów możliwych do serializacji kodu XML w każdej umowie.|

|Opcja|Opis|
|------------|-----------------|
|/Reference\<file path>|Dodaje określony zestaw do zestawu zestawów używanych do rozpoznawania odwołań do typu.<br /><br /> Krótka forma: `/r`|
|/excludeType:\<type>|Określa w pełni kwalifikowaną lub kwalifikowaną dla zestawu nazwę typu, który ma zostać wykluczony z eksportu lub walidacji.<br /><br /> Krótka forma: `/et`|
|/out\<file>|Określa nazwę pliku dla wygenerowanego kodu. Ta opcja jest ignorowana, gdy wiele zestawów jest przenoszona jako dane wejściowe do narzędzia.<br /><br /> Wartość domyślna: pochodna na podstawie nazwy zestawu.<br /><br /> Krótka forma: `/o`|
|/UseSerializerForFaults|Określa, że <xref:System.Xml.Serialization.XmlSerializer> powinny być używane do odczytu i zapisu błędów zamiast domyślnego <xref:System.Runtime.Serialization.DataContractSerializer> .|

## <a name="examples"></a>Przykłady

Następujące polecenie generuje kod klienta z uruchomionej usługi lub dokumentów metadanych online.

`svcutil http://service/metadataEndpoint`

Następujące polecenie generuje kod klienta z lokalnych dokumentów metadanych.

`svcutil *.wsdl *.xsd /language:C#`

Następujące polecenie generuje typy kontraktów danych w Visual Basic z dokumentów schematu lokalnego.

`svcutil /dconly *.xsd /language:VB`

Następujące polecenie pobiera dokumenty metadanych z uruchomionych usług.

`svcutil /t:metadata http://service/metadataEndpoint`

Następujące polecenie generuje dokumenty metadanych dla kontraktów usługi i skojarzonych z nimi typów w zestawie.

`svcutil myAssembly.dll`

Następujące polecenie generuje dokumenty metadanych dla usługi i wszystkie skojarzone kontrakty usługi i typy danych w zestawie.

`svcutil myServiceHost.exe /serviceName:myServiceName`

Następujące polecenie generuje dokumenty metadanych dla typów danych w zestawie.

`svcutil myServiceHost.exe /dconly`

Następujące polecenie sprawdza hosting usług.

`svcutil /validate /serviceName:myServiceName myServiceHost.exe`

Następujące polecenie generuje typy serializacji dla <xref:System.Xml.Serialization.XmlSerializer> typów używanych przez wszystkie kontrakty usługi w zestawie.

`svcutil /t:xmlserializer myContractLibrary.exe`

## <a name="maximum-nametable-character-count-quota"></a>Maksymalny limit przydziału liczby znaków NameTable

W przypadku generowania metadanych dla usługi przy użyciu programu Svcutil może zostać wyświetlony następujący komunikat:

Błąd: nie można uzyskać metadanych z `http://localhost:8000/somesservice/mex` maksymalnego limitu przydziału liczby znaków NameTable (16384) podczas odczytywania danych XML. NameTable jest strukturą danych, która jest używana do przechowywania ciągów napotkanych podczas przetwarzania XML — długie dokumenty XML z niepowtarzającymi się nazwami elementów, nazwy atrybutów i wartości atrybutów mogą wyzwalać ten przydział. Ten limit przydziału można zwiększyć, zmieniając właściwość MaxNameTableCharCount obiektu XmlDictionaryReaderQuotas użytego podczas tworzenia modułu odczytującego XML.

Ten błąd może być spowodowany przez usługę zwracającą duży plik WSDL podczas żądania metadanych. Problem polega na tym, że przekroczony został przydział znaków dla narzędzia svcutil.exe. Ta wartość jest ustawiona, aby zapobiec atakom typu "odmowa usługi" (DOS). Ten limit przydziału można zwiększyć, określając następujący plik konfiguracji dla Svcutil.

Następujący plik konfiguracji pokazuje, jak ustawić przydziały czytnika dla Svcutil

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <system.serviceModel>
        <bindings>
            <customBinding>
                <binding name="MyBinding">
                    <textMessageEncoding>
                        <readerQuotas maxDepth="2147483647" maxStringContentLength="2147483647"
                            maxArrayLength="2147483647" maxBytesPerRead="2147483647" maxNameTableCharCount="2147483647" />
                    </textMessageEncoding>
                    <httpTransport maxReceivedMessageSize="2147483647" maxBufferSize="2147483647" />
                </binding>
            </customBinding>
        </bindings>
        <client>
            <endpoint binding="customBinding" bindingConfiguration="MyBinding"
                contract="IMetadataExchange"
                name="http" />
        </client>
    </system.serviceModel>
</configuration>
```

Utwórz nowy plik o nazwie svcutil.exe.config i skopiuj do niego przykładowy kod XML. Następnie umieść plik w tym samym katalogu co svcutil.exe. Przy następnym uruchomieniu svcutil.exe zostanie wybrane nowe ustawienia.

## <a name="security-concerns"></a>Zagadnienia dotyczące zabezpieczeń

Należy używać odpowiedniej listy Access Control (ACL) do ochrony folderu instalacji Svcutil.exe, Svcutil.config i plików, które są wskazywane przez program `/svcutilConfig` . Może to uniemożliwić rejestrowanie i uruchamianie złośliwych rozszerzeń.

Ponadto aby zminimalizować ryzyko naruszenia zabezpieczeń, nie należy dodawać niezaufanych rozszerzeń jako części systemu ani używać niezaufanych dostawców kodu z Svcutil.exe.

Na koniec nie należy używać tego narzędzia w warstwie środkowej aplikacji, ponieważ może to spowodować odmowę usługi dla bieżącego procesu.

## <a name="see-also"></a>Zobacz także

- <xref:System.Runtime.Serialization.DataContractAttribute>
- <xref:System.Runtime.Serialization.DataMemberAttribute>
- [Instrukcje: tworzenie klienta](how-to-create-a-wcf-client.md)
