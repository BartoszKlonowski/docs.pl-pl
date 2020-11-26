---
title: 'Instrukcje: skracanie czasu uruchamiania aplikacji klienckich programu WCF za pomocą elementu XmlSerializer'
ms.date: 03/30/2017
ms.assetid: 21093451-0bc3-4b1a-9a9d-05f7f71fa7d0
ms.openlocfilehash: ac54a766161db146331a3e072b97822b609344c0
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96246384"
---
# <a name="how-to-improve-the-startup-time-of-wcf-client-applications-using-the-xmlserializer"></a>Instrukcje: skracanie czasu uruchamiania aplikacji klienckich programu WCF za pomocą elementu XmlSerializer

Usługi i aplikacje klienckie korzystające z typów danych, które można serializować przy użyciu <xref:System.Xml.Serialization.XmlSerializer> generowania i kompilowania kodu serializacji dla tych typów danych w czasie wykonywania, co może spowodować spowolnienie wydajności.  
  
> [!NOTE]
> Wstępnie wygenerowany kod serializacji może być używany tylko w aplikacjach klienckich, a nie w usługach.  
  
 [Narzędzie do przesyłania metadanych ServiceModel (Svcutil.exe)](../servicemodel-metadata-utility-tool-svcutil-exe.md) może zwiększyć wydajność uruchamiania tych aplikacji, generując wymagany kod serializacji z skompilowanych zestawów dla aplikacji. Svcutil.exe generuje kod serializacji dla wszystkich typów danych używanych w kontraktach usług w skompilowanym zestawie aplikacji, który może być serializowany przy użyciu <xref:System.Xml.Serialization.XmlSerializer> . Kontrakty usługi i operacji używające <xref:System.Xml.Serialization.XmlSerializer> są oznaczone za pomocą <xref:System.ServiceModel.XmlSerializerFormatAttribute> .  
  
### <a name="to-generate-xmlserializer-serialization-code"></a>Aby wygenerować kod serializacji XmlSerializer  
  
1. Skompiluj kod usługi lub klienta w jednym lub kilku zestawach.  
  
2. Otwórz wiersz polecenia zestawu SDK.  
  
3. W wierszu polecenia Uruchom narzędzie Svcutil.exe w następującym formacie.  
  
    ```console  
    svcutil.exe /t:xmlSerializer  <assemblyPath>*  
    ```  
  
     `assemblyPath`Argument określa ścieżkę do zestawu, który zawiera typy kontraktu usługi. Svcutil.exe generuje kod serializacji dla wszystkich typów danych używanych w kontraktach usług w skompilowanym zestawie aplikacji, który może być serializowany przy użyciu <xref:System.Xml.Serialization.XmlSerializer> .  
  
     Svcutil.exe może generować tylko kod serializacji języka C#. Dla każdego zestawu wejściowego jest generowany jeden plik kodu źródłowego. Nie można użyć przełącznika **/Language** , aby zmienić język wygenerowanego kodu.  
  
     Aby określić ścieżkę do zestawów zależnych, użyj opcji **/Reference** .  
  
4. Udostępnij wygenerowany kod serializacji aplikacji przy użyciu jednej z następujących opcji:  
  
    1. Kompiluj wygenerowany kod serializacji w osobnym zestawie o nazwie [*oryginalny zestaw*] .XmlSerializers.dll (na przykład MyApp.XmlSerializers.dll). Aplikacja musi być w stanie załadować zestaw, który musi być podpisany przy użyciu tego samego klucza co oryginalny zestaw. W przypadku ponownej kompilacji oryginalnego zestawu należy ponownie wygenerować zestaw serializacji.  
  
    2. Skompiluj wygenerowany kod serializacji do oddzielnego zestawu i użyj programu <xref:System.Xml.Serialization.XmlSerializerAssemblyAttribute> w ramach kontraktu usługi, który używa <xref:System.ServiceModel.XmlSerializerFormatAttribute> . Ustaw <xref:System.Xml.Serialization.XmlSerializerAssemblyAttribute.AssemblyName%2A> właściwości lub, <xref:System.Xml.Serialization.XmlSerializerAssemblyAttribute.CodeBase%2A> aby wskazywały skompilowany zestaw serializacji.  
  
    3. Skompiluj wygenerowany kod serializacji do zestawu aplikacji i Dodaj <xref:System.Xml.Serialization.XmlSerializerAssemblyAttribute> do kontraktu usługi, który używa <xref:System.ServiceModel.XmlSerializerFormatAttribute> . Nie ustawiaj <xref:System.Xml.Serialization.XmlSerializerAssemblyAttribute.AssemblyName%2A> ani <xref:System.Xml.Serialization.XmlSerializerAssemblyAttribute.CodeBase%2A> właściwości. Przyjęto, że domyślny zestaw serializacji jest bieżącym zestawem.  
  
### <a name="to-generate-xmlserializer-serialization-code-in-visual-studio"></a>Aby wygenerować kod serializacji XmlSerializer w programie Visual Studio  
  
1. Utwórz usługę WCF i projekty klienta w programie Visual Studio. Następnie Dodaj odwołanie do usługi do projektu klienta.  
  
2. Dodaj <xref:System.ServiceModel.XmlSerializerFormatAttribute> do kontraktu usługi w pliku *Reference.cs* w projekcie aplikacji klienta w obszarze **ServiceReference**  ->  **Reference. svcmap**. Zwróć uwagę, że musisz wyświetlić wszystkie pliki w **Eksplorator rozwiązań** , aby wyświetlić te pliki.  
  
3. Utwórz aplikację kliencką.  
  
4. Użyj [Narzędzia do przesyłania metadanych modelu ServiceModel (Svcutil.exe)](../servicemodel-metadata-utility-tool-svcutil-exe.md) , aby utworzyć wstępnie wygenerowany plik serializator *. cs* za pomocą polecenia:  
  
    ```console  
    svcutil.exe /t:xmlSerializer  <assemblyPath>*  
    ```  
  
     Argument assemblyPath określa ścieżkę do zestawu klienta WCF.  
  
     Przykładowe metody:  
  
    ```console  
    svcutil.exe /t:xmlSerializer wcfclient.exe  
    ```  
  
     Zostanie wygenerowany plik *WCFClient.XmlSerializers.dll. cs* .  
  
5. Kompiluj wstępnie wygenerowany zestaw serializacji.  
  
     Na podstawie przykładu w poprzednim kroku polecenie Kompiluj będzie następujące:  
  
    ```console  
    csc /r:wcfclient.exe /out:WCFClient.XmlSerializers.dll /t:library WCFClient.XmlSerializers.dll.cs  
    ```  
  
     Upewnij się, że wygenerowany *WCFClient.XmlSerializers.dll* znajduje się w tym samym katalogu, w którym znajduje się aplikacja kliencka, która jest *WCFClient.exe* w tym przypadku.  
  
6. Uruchom aplikację kliencką w zwykły sposób. Zostanie użyty wstępnie wygenerowany zestaw serializacji.  
  
## <a name="example"></a>Przykład  

 Następujące polecenie generuje typy serializacji dla `XmlSerializer` typów, które są używane przez wszystkie kontrakty usługi w zestawie.  
  
```console  
svcutil /t:xmlserializer myContractLibrary.exe  
```  
  
## <a name="see-also"></a>Zobacz też

- [Narzędzie do obsługi metadanych elementu ServiceModel (Svcutil.exe)](../servicemodel-metadata-utility-tool-svcutil-exe.md)
