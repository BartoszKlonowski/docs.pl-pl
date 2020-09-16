---
title: Używanie monikera programu WCF z klientami COM
ms.date: 03/30/2017
ms.assetid: e2799bfe-88bd-49d7-9d6d-ac16a9b16b04
ms.openlocfilehash: b36b646f650c2a2974c7b0689a9367961075ea14
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/15/2020
ms.locfileid: "90553034"
---
# <a name="using-the-wcf-moniker-with-com-clients"></a>Używanie monikera programu WCF z klientami COM
Ten przykład pokazuje, jak używać monikera usługi Windows Communication Foundation (WCF) do integrowania usług sieci Web w środowiskach deweloperskich opartych na modelu COM, takich jak Microsoft Office Visual Basic for Applications (Office VBA) lub Visual Basic 6,0. Ten przykład składa się z klienta hosta skryptów systemu Windows (. vbs), pomocniczej biblioteki klienta (. dll) i biblioteki usług (. dll) hostowanej przez Internet Information Services (IIS). Usługa to usługa kalkulatora, a klient COM wywołuje operacje matematyczne — Dodawanie, odejmowanie, mnożenie i dzielenie — w usłudze. Aktywność klienta jest widoczna w oknach okna komunikatu.  
  
> [!NOTE]
> Procedura konfiguracji i instrukcje dotyczące kompilacji dla tego przykładu znajdują się na końcu tego tematu.  
  
> [!IMPORTANT]
> Przykłady mogą być już zainstalowane na komputerze. Przed kontynuowaniem Wyszukaj następujący katalog (domyślny).  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> Jeśli ten katalog nie istnieje, przejdź do [przykładów Windows Communication Foundation (WCF) i Windows Workflow Foundation (WF) dla .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) , aby pobrać wszystkie Windows Communication Foundation (WCF) i [!INCLUDE[wf1](../../../../includes/wf1-md.md)] przykłady. Ten przykład znajduje się w następującym katalogu.  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Services\Interop\COM`  
  
 Usługa implementuje `ICalculator` kontrakt zdefiniowany jak pokazano w poniższym przykładzie kodu.  
  
```csharp
[ServiceContract(Namespace="http://Microsoft.ServiceModel.Samples")]  
public interface ICalculator  
{  
    [OperationContract]  
    double Add(double n1, double n2);  
    [OperationContract]  
    double Subtract(double n1, double n2);  
    [OperationContract]  
    double Multiply(double n1, double n2);  
    [OperationContract]  
    double Divide(double n1, double n2);  
}  
```  
  
 Przykład ilustruje trzy alternatywne podejścia do używania monikera:  
  
- Typ kontraktu — kontrakt jest rejestrowany jako widoczny dla modelu COM na komputerze klienckim.  
  
- Kontrakt WSDL — kontrakt jest dostarczany w formie dokumentu WSDL.  
  
- Kontrakt wymiany metadanych — kontrakt jest pobierany w czasie wykonywania z punktu końcowego wymiany metadanych (MEX).  
  
## <a name="typed-contract"></a>Typ kontraktu  
 Aby użyć monikera z określonym umownym użyciem kontraktu, odpowiednie typy atrybutów dla kontraktu usługi muszą być zarejestrowane w modelu COM. Najpierw należy wygenerować klienta przy użyciu [Narzędzia do przesyłania metadanych modelu ServiceModel (Svcutil.exe)](../servicemodel-metadata-utility-tool-svcutil-exe.md). Uruchom następujące polecenie w wierszu polecenia w katalogu klienta, aby wygenerować serwer proxy z określonym typem.  
  
```console  
svcutil.exe /n:http://Microsoft.ServiceModel.Samples,Microsoft.ServiceModel.Samples http://localhost/servicemodelsamples/service.svc /out:generatedClient.cs  
```  
  
 Ta klasa musi być uwzględniona w projekcie, a projekt powinien zostać skonfigurowany w taki sposób, aby generował zestaw z widocznym elementem COM, gdy zostanie skompilowany. Następujący atrybut powinien zostać uwzględniony w pliku AssemblyInfo.cs.  
  
```csharp
[assembly: ComVisible(true)]  
```  
  
 Po skompilowaniu projektu, należy zarejestrować typy widoczne dla modelu COM za pomocą `regasm` , jak pokazano w poniższym przykładzie.  
  
```console  
regasm.exe /tlb:CalcProxy.tlb client.dll  
```  
  
 Utworzony zestaw powinien zostać dodany do globalnej pamięci podręcznej zestawów. Chociaż nie jest to ściśle wymagane, upraszcza to proces środowiska uruchomieniowego, w którym znajduje się zestaw. Poniższe polecenie dodaje zestaw do globalnej pamięci podręcznej zestawów.  
  
```console  
gacutil.exe /i client.dll  
```  
  
> [!NOTE]
> Moniker usługi wymaga tylko rejestracji typu i nie używa serwera proxy do komunikowania się z usługą.  
  
 Aplikacja kliencka ComCalcClient. vbs używa `GetObject` funkcji do konstruowania serwera proxy dla usługi przy użyciu składni krótkiej usługi do określenia adresu, powiązania i kontraktu dla usługi.  
  
```vbscript
Set typedServiceMoniker = GetObject(  
"service4:address=http://localhost/ServiceModelSamples/service.svc, binding=wsHttpBinding,
contractType={9213C6D2-5A6F-3D26-839B-3BA9B82228D3}")  
```  
  
 Parametry używane przez moniker określają:  
  
- Adres punktu końcowego usługi.  
  
- Powiązanie, którego klient powinien używać do łączenia się z tym punktem końcowym. W tym przypadku wsHttpBinding zdefiniowany przez system jest używany, chociaż niestandardowe powiązania można definiować w plikach konfiguracji klienta. W przypadku korzystania z hosta skryptów systemu Windows niestandardowe powiązanie jest zdefiniowane w pliku Cscript.exe.config w tym samym katalogu, co Cscript.exe.  
  
- Typ kontraktu, który jest obsługiwany w punkcie końcowym. Jest to typ wygenerowany i zarejestrowany powyżej. Ponieważ skrypt Visual Basic nie zapewnia środowiska COM o jednoznacznie określonym typie, należy określić identyfikator kontraktu. Ten identyfikator GUID to `interfaceID` CalcProxy. tlb, który można wyświetlić za pomocą narzędzi com, takich jak Przeglądarka obiektów OLE/COM (OleView.exe). W przypadku środowisk o jednoznacznie określonym typie, takich jak pakiet Office VBA lub Visual Basic 6,0, Dodawanie jawnego odwołania do biblioteki typów, a następnie deklarowanie typu obiektu serwera proxy może być używane zamiast parametru kontraktu. Zapewnia to również obsługę technologii IntelliSense podczas tworzenia aplikacji klienckiej.  
  
 Po zbudowaniu wystąpienia serwera proxy za pomocą monikera usługi aplikacja kliencka może wywoływać metody na serwerze proxy, co powoduje, że infrastruktura monikera usługi wywołuje odpowiednie operacje usługi.  
  
```vbscript  
' Call the service operations using the moniker object  
WScript.Echo "Typed service moniker: 100 + 15.99 = " & typedServiceMoniker.Add(100, 15.99)  
```  
  
 Po uruchomieniu przykładu odpowiedź operacji zostanie wyświetlona w oknie komunikatów hosta skryptów systemu Windows. Przedstawia to klientowi COM wywołania COM przy użyciu wpisanej monikera do komunikowania się z usługą WCF. Mimo korzystania z modelu COM w aplikacji klienckiej komunikacja z usługą obejmuje tylko wywołania usługi sieci Web.  
  
## <a name="wsdl-contract"></a>Kontrakt WSDL  
 Aby użyć monikera z kontraktem WSDL, nie jest wymagana żadna rejestracja biblioteki klienta, ale kontrakt WSDL dla usługi musi zostać pobrany za pośrednictwem mechanizmu poza pasmem, takiego jak korzystanie z przeglądarki w celu uzyskania dostępu do punktu końcowego WSDL usługi. Moniker może następnie uzyskać dostęp do tego kontraktu w czasie wykonywania.  
  
 Aplikacja kliencka ComCalcClient. vbs używa programu w `FileSystemObject` celu uzyskania dostępu do lokalnego zapisanego pliku WSDL, a następnie ponownie używa `GetObject` funkcji do konstruowania serwera proxy dla usługi.  
  
```vbscript  
' Open the WSDL contract file and read it all into the wsdlContract string  
Const ForReading = 1  
Set objFSO = CreateObject("Scripting.FileSystemObject")  
Set objFile = objFSO.OpenTextFile("serviceWsdl.xml", ForReading)  
wsdlContract = objFile.ReadAll  
objFile.Close  
  
' Create a string for the service moniker including the content of the WSDL contract file  
wsdlMonikerString = "service4:address='http://localhost/ServiceModelSamples/service.svc'"  
wsdlMonikerString = wsdlMonikerString + ", binding=WSHttpBinding_ICalculator, bindingNamespace='http://Microsoft.ServiceModel.Samples'"  
wsdlMonikerString = wsdlMonikerString + ", wsdl='" & wsdlContract & "'"  
wsdlMonikerString = wsdlMonikerString + ", contract=ICalculator, contractNamespace='http://Microsoft.ServiceModel.Samples'"  
  
' Create the service moniker object  
Set wsdlServiceMoniker = GetObject(wsdlMonikerString)  
```  
  
 Parametry używane przez moniker określają:  
  
- Adres punktu końcowego usługi.  
  
- Powiązanie, którego klient powinien używać do łączenia się z tym punktem końcowym i przestrzeni nazw, w której jest zdefiniowane to powiązanie. W tym przypadku `wsHttpBinding_ICalculator` jest używany.  
  
- WSDL, który definiuje kontrakt. W tym przypadku jest to ciąg, który został odczytany z pliku serviceWsdl.xml.  
  
- Nazwa i przestrzeń nazw kontraktu. Ta identyfikacja jest wymagana, ponieważ WSDL może zawierać więcej niż jeden kontrakt.  
  
    > [!NOTE]
    > Domyślnie usługi WCF generują oddzielne pliki WSDL dla każdej przestrzeni nazw używanej przez program. Są one powiązane z użyciem konstrukcji importu WSDL. Ponieważ moniker oczekuje pojedynczej definicji WSDL, usługa musi albo użyć pojedynczej przestrzeni nazw, jak pokazano w tym przykładzie, albo oddzielne pliki muszą zostać scalone ręcznie.  
  
 Po zbudowaniu wystąpienia serwera proxy za pomocą monikera usługi aplikacja kliencka może wywoływać metody na serwerze proxy, co powoduje, że infrastruktura monikera usługi wywołuje odpowiednie operacje usługi.  
  
```vbscript  
' Call the service operations using the moniker object  
WScript.Echo "WSDL service moniker: 145 - 76.54 = " & wsdlServiceMoniker.Subtract(145, 76.54)  
```  
  
 Po uruchomieniu przykładu odpowiedź operacji zostanie wyświetlona w oknie komunikatów hosta skryptów systemu Windows. Przedstawia to klientowi COM wywołania COM przy użyciu monikera z kontraktem WSDL do komunikowania się z usługą WCF.  
  
## <a name="metadata-exchange-contract"></a>Kontrakt wymiany metadanych  
 Aby użyć monikera z kontraktem MEX, jak w przypadku kontraktu WSDL, rejestracja klienta nie jest wymagana. Kontrakt usługi jest pobierany w czasie wykonywania za pomocą wewnętrznego używania wymiany metadanych.  
  
 Aplikacja kliencka ComCalcClient. vbs ponownie używa `GetObject` funkcji do konstruowania serwera proxy dla usługi.  
  
```vbscript  
' Create a string for the service moniker specifying the address to retrieve the service metadata from  
mexMonikerString = "service4:mexAddress='http://localhost/servicemodelsamples/service.svc/mex'"  
mexMonikerString = mexMonikerString + ", address='http://localhost/ServiceModelSamples/service.svc'"  
mexMonikerString = mexMonikerString + ", binding=WSHttpBinding_ICalculator, bindingNamespace='http://Microsoft.ServiceModel.Samples'"  
mexMonikerString = mexMonikerString + ", contract=ICalculator, contractNamespace='http://Microsoft.ServiceModel.Samples'"  
  
' Create the service moniker object  
Set mexServiceMoniker = GetObject(mexMonikerString)  
```  
  
 Parametry używane przez moniker określają:  
  
- Adres punktu końcowego wymiany metadanych usługi.  
  
- Adres punktu końcowego usługi.  
  
- Powiązanie, którego klient powinien używać do łączenia się z tym punktem końcowym i przestrzeni nazw, w której jest zdefiniowane to powiązanie. W tym przypadku `wsHttpBinding_ICalculator` jest używany.  
  
- Nazwa i przestrzeń nazw kontraktu. Ta identyfikacja jest wymagana, ponieważ WSDL może zawierać więcej niż jeden kontrakt.  
  
 Po zbudowaniu wystąpienia serwera proxy za pomocą monikera usługi aplikacja kliencka może wywoływać metody na serwerze proxy, co powoduje, że infrastruktura monikera usługi wywołuje odpowiednie operacje usługi.  
  
```vbscript  
' Call the service operations using the moniker object  
WScript.Echo "MEX service moniker: 9 * 81.25 = " & mexServiceMoniker.Multiply(9, 81.25)  
```  
  
 Po uruchomieniu przykładu odpowiedź operacji zostanie wyświetlona w oknie komunikatów hosta skryptów systemu Windows. Pokazuje to, że klient COM wywołuje wywołania COM przy użyciu monikera z kontraktem MEX, aby komunikować się z usługą WCF.  
  
#### <a name="to-set-up-and-build-the-sample"></a>Aby skonfigurować i skompilować przykład  
  
1. Upewnij się, że została wykonana [Procedura konfiguracji jednorazowej dla przykładów Windows Communication Foundation](one-time-setup-procedure-for-the-wcf-samples.md).  
  
2. Aby skompilować wersję rozwiązania w języku C# lub Visual Basic .NET, postępuj zgodnie z instrukcjami w temacie [Tworzenie przykładów Windows Communication Foundation](building-the-samples.md).  
  
3. W wiersz polecenia dla deweloperów dla programu Visual Studio Otwórz folder \client\bin w obszarze folder charakterystyczny dla języka.  
  
    > [!NOTE]
    > W przypadku korzystania z systemu Windows Vista, Windows Server 2008, Windows 7 lub Windows Server 2008 R2 upewnij się, że uruchamiasz wiersz polecenia z uprawnieniami administratora.  
  
4. Wpisz tekst, `tlbexp.exe client.dll /out:CalcProxy.tlb` Aby wyeksportować bibliotekę DLL do pliku TLB. Oczekiwana jest wartość "ostrzeżenie eksportera biblioteki typów", ale nie jest to problem, ponieważ typ ogólny nie jest wymagany.  
  
5. Wpisz w, `regasm.exe /tlb:CalcProxy.tlb client.dll` Aby zarejestrować typy z modelem com. Oczekiwana jest wartość "ostrzeżenie eksportera biblioteki typów", ale nie jest to problem, ponieważ typ ogólny nie jest wymagany.  
  
6. Wpisz, `gacutil.exe /i client.dll` Aby dodać zestaw do globalnej pamięci podręcznej zestawów.  
  
#### <a name="to-run-the-sample-on-the-same-computer"></a>Aby uruchomić przykład na tym samym komputerze  
  
1. Sprawdź, czy możesz uzyskać dostęp do usługi przy użyciu przeglądarki, wpisując następujący adres: `http://localhost/servicemodelsamples/service.svc` . W odpowiedzi powinna zostać wyświetlona strona potwierdzenia.  
  
2. Uruchom ComCalcClient. vbs z \Client, z poziomu folderu specyficznego dla języka. Aktywność klienta jest wyświetlana w oknach okna komunikatu.  
  
3. Jeśli klient i usługa nie mogą się komunikować, zobacz Wskazówki dotyczące [rozwiązywania problemów z przykładami programu WCF](/previous-versions/dotnet/netframework-3.5/ms751511(v=vs.90)).  
  
#### <a name="to-run-the-sample-across-computers"></a>Aby uruchomić przykład na wielu komputerach  
  
1. Na komputerze usługi Utwórz katalog wirtualny o nazwie ServiceModelSamples. Skrypt Setupvroot.bat dołączony do przykładu może służyć do tworzenia katalogu dysku i katalogu wirtualnego.  
  
2. Skopiuj pliki programu usługi z%SystemDrive%\Inetpub\wwwroot\servicemodelsamples do katalogu wirtualnego ServiceModelSamples na komputerze usługi. Pamiętaj o uwzględnieniu plików w katalogu \Bin.  
  
3. Skopiuj plik skryptu klienta z folderu \Client, w obszarze folder specyficzny dla języka, do komputera klienckiego.  
  
4. W pliku skryptu Zmień wartość adresu definicji punktu końcowego, aby była zgodna z nowym adresem usługi. Zastąp wszystkie odwołania do "localhost" z w pełni kwalifikowaną nazwą domeny w adresie.  
  
5. Skopiuj plik WSDL na komputer kliencki. W pliku WSDL serviceWsdl.xml Zastąp wszystkie odwołania do wartości "localhost" z w pełni kwalifikowaną nazwą domeny w adresie.  
  
6. Skopiuj bibliotekę Client.dll z folderu \client\bin, w obszarze folder charakterystyczny dla języka, do katalogu na komputerze klienckim.  
  
7. W wierszu polecenia przejdź do katalogu docelowego na komputerze klienckim. W przypadku korzystania z systemu Windows Vista lub Windows Server 2008 upewnij się, że uruchamiasz wiersz polecenia jako administrator.  
  
8. Wpisz tekst, `tlbexp.exe client.dll /out:CalcProxy.tlb` Aby wyeksportować bibliotekę DLL do pliku TLB. Oczekiwana jest wartość "ostrzeżenie eksportera biblioteki typów", ale nie jest to problem, ponieważ typ ogólny nie jest wymagany.  
  
9. Wpisz w, `regasm.exe /tlb:CalcProxy.tlb client.dll` Aby zarejestrować typy z modelem com. Upewnij się, że ścieżka została ustawiona na folder, który zawiera `regasm.exe` przed uruchomieniem polecenia.  
  
10. Wpisz, `gacutil.exe /i client.dll` Aby dodać zestaw do globalnej pamięci podręcznej zestawów. Upewnij się, że ścieżka została ustawiona na folder, który zawiera `gacutil.exe` przed uruchomieniem polecenia.  
  
11. Sprawdź, czy możesz uzyskać dostęp do usługi z komputera klienckiego za pomocą przeglądarki.  
  
12. Na komputerze klienckim uruchom ComCalcClient. vbs.  
  
#### <a name="to-clean-up-after-the-sample"></a>Aby wyczyścić po przykładzie  
  
- Ze względów bezpieczeństwa usuń definicję katalogu wirtualnego i uprawnienia przyznane w procedurach instalacji po zakończeniu pracy z przykładami.
