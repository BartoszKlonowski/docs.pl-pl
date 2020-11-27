---
title: Powiązywanie danych w kliencie programu ASP.NET
ms.date: 03/30/2017
ms.assetid: 68b49fa6-94e7-4d4c-a34e-902a2b3770b6
ms.openlocfilehash: 3e30bcb9852b34eeb919339d57d701e4dda8a644
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96266873"
---
# <a name="data-binding-in-an-aspnet-client"></a>Powiązywanie danych w kliencie programu ASP.NET

Ten przykład pokazuje, jak powiązać dane zwrócone przez typową usługę Windows Communication Foundation (WCF) w aplikacji formularzy sieci Web.  
  
> [!NOTE]
> Procedura instalacji i instrukcje dotyczące kompilacji dla tego przykładu znajdują się na końcu tego tematu.  
  
 Ten przykład pokazuje usługę implementującą kontrakt, który definiuje wzorzec komunikacji z odpowiedzią na żądanie. Przykład składa się z aplikacji formularzy sieci Web klienta dostępnej z przeglądarki i usługi WCF hostowanej przez Internet Information Services (IIS).  
  
 Usługa implementuje kontrakt definiujący wzorzec komunikacji żądanie-odpowiedź. Kontrakt jest definiowany przez `IWeatherService` interfejs, który uwidacznia operację o nazwie `GetWeatherData` . Ta operacja akceptuje tablicę miast i zwraca tablicę `WeatherData` obiektów, która reprezentuje górną i niską prognozę dla miasta.  
  
 Na stronie ASP.NET Client. aspx jest zdefiniowany formant sieci Web DataGrid, który zawiera graficzną reprezentację danych zwróconych przez usługę. Kod na stronie. aspx wywołuje usługę WCF dla danych pogody i zwraca dane do tablicy `WeatherData` obiektów. DataGrid określa miejsce, z którego mają zostać pobrane dane, przez ustawienie jego `DataSource` właściwości na tę tablicę. Powiązanie danych odbywa się z wywołaniem `DataBind` metody DataGrid. Cały ten kod jest zawarty w.`aspx` Metoda strony `Page_Load` , za każdym razem, gdy użytkownik Odświeża stronę przeglądarki, dane są aktualizowane w elemencie DataGrid.  
  
### <a name="to-set-up-build-and-run-the-sample"></a>Aby skonfigurować, skompilować i uruchomić przykład  
  
1. Upewnij się, że została wykonana [Procedura konfiguracji jednorazowej dla przykładów Windows Communication Foundation](one-time-setup-procedure-for-the-wcf-samples.md).  
  
2. Aby skompilować wersję rozwiązania w języku C# lub Visual Basic .NET, postępuj zgodnie z instrukcjami w temacie [Tworzenie przykładów Windows Communication Foundation](building-the-samples.md).  
  
3. Klient tego przykładu jest witryną sieci Web, która jest uruchamiana w ramach deweloperskiego serwera sieci Web. Aby uruchomić serwer deweloperski sieci Web, wpisz następujące polecenie w wierszu polecenia: `%SystemDrive%\Program Files\Common Files\Microsoft Shared\DevServer\9.0\WebDev.WebServer.EXE" /port:8000 /path:<WebFormsSamplePath>\CS\client /vpath:/client` . Następnie przejdź do `http://localhost:8000/client` . Aby uruchomić ten przykład między komputerami, Zastąp wszystkie odwołania do `localhost` pliku Web.config klienta z nazwą komputera serwera programu.  
  
> [!IMPORTANT]
> Przykłady mogą być już zainstalowane na komputerze. Przed kontynuowaniem Wyszukaj następujący katalog (domyślny).  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> Jeśli ten katalog nie istnieje, przejdź do [przykładów Windows Communication Foundation (WCF) i Windows Workflow Foundation (WF) dla .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) , aby pobrać wszystkie Windows Communication Foundation (WCF) i [!INCLUDE[wf1](../../../../includes/wf1-md.md)] przykłady. Ten przykład znajduje się w następującym katalogu.  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Scenario\DataBinding\WebForms`
