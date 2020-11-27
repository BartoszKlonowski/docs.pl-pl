---
title: Sesja
ms.date: 03/30/2017
helpviewer_keywords:
- Sessions
ms.assetid: 36e1db50-008c-4b32-8d09-b56e790b8417
ms.openlocfilehash: 23b42e48c715c9c723ce9ac8ba8c3c1af7ace969
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96290052"
---
# <a name="session"></a>Sesja

Przykład sesji demonstruje sposób implementacji kontraktu wymagającego sesji. Sesja zawiera kontekst do wykonywania wielu operacji. Umożliwia to usłudze kojarzenie stanu z daną sesją, tak aby kolejne operacje mogły korzystać z stanu poprzedniej operacji. Ten przykład jest oparty na [wprowadzenie](getting-started-sample.md), który implementuje usługę kalkulatora. `ICalculator`Kontrakt został zmodyfikowany w taki sposób, aby zezwalał na wykonywanie zestawu operacji arytmetycznych przy zachowaniu uruchomionego wyniku. Ta funkcja jest definiowana przez `ICalculatorSession` umowę. Usługa zachowuje stan klienta w miarę wywoływania wielu operacji usługi, aby wykonać obliczenia. Klient może pobrać bieżący wynik, wywołując `Result()` i czyszcząc wynik do zera przez wywołanie metody `Clear()` .  
  
 W tym przykładzie klient jest aplikacją konsolową (. exe), a usługa jest hostowana przez Internet Information Services (IIS).  
  
> [!NOTE]
> Procedura instalacji i instrukcje dotyczące kompilacji dla tego przykładu znajdują się na końcu tego tematu.  
  
 Ustawienie <xref:System.ServiceModel.SessionMode> kontraktu `Required` zapewnia, że gdy kontrakt zostanie ujawniony nad określonym powiązaniem, powiązanie obsługuje sesje. Jeśli powiązanie nie obsługuje sesji, zgłaszany jest wyjątek. `ICalculatorSession`Interfejs jest zdefiniowany w taki sposób, że można wywołać jedną lub więcej operacji, co powoduje modyfikację uruchomionego wyniku, jak pokazano w poniższym przykładowym kodzie.  
  
```csharp
[ServiceContract(Namespace="http://Microsoft.ServiceModel.Samples", SessionMode=SessionMode.Required)]  
public interface ICalculatorSession  
{  
    [OperationContract(IsOneWay=true)]  
    void Clear();  
    [OperationContract(IsOneWay = true)]  
    void AddTo(double n);  
    [OperationContract(IsOneWay = true)]  
    void SubtractFrom(double n);  
    [OperationContract(IsOneWay = true)]  
    void MultiplyBy(double n);  
    [OperationContract(IsOneWay = true)]  
    void DivideBy(double n);  
    [OperationContract]  
    double Result();  
}  
```  
  
 Usługa używa programu w <xref:System.ServiceModel.InstanceContextMode> <xref:System.ServiceModel.InstanceContextMode.PerSession> celu powiązania danego kontekstu wystąpienia usługi z każdą sesją przychodzącą. Dzięki temu usługa może zachować wynik działania dla każdej sesji w lokalnej zmiennej członkowskiej.  
  
```csharp
[ServiceBehavior(InstanceContextMode=InstanceContextMode.PerSession)]  
public class CalculatorService : ICalculatorSession  
{  
    double result = 0.0D;  
  
    public void Clear()  
    {  result = 0.0D; }  
  
    public void AddTo(double n)  
    {  result += n;   }  
  
    public void SubtractFrom(double n)  
    {  result -= n;   }  
  
    public void MultiplyBy(double n)  
    {  result *= n;   }  
  
    public void DivideBy(double n)  
    {  result /= n;   }  
  
    public double Result()  
    {  return result; }  
}  
```  
  
 Po uruchomieniu przykładu klient wysyła kilka żądań do serwera i żąda wyniku, który następnie jest wyświetlany w oknie konsoli klienta. Naciśnij klawisz ENTER w oknie klienta, aby zamknąć klienta programu.  
  
```console  
(((0 + 100) - 50) * 17.65) / 2 = 441.25  
Press <ENTER> to terminate client.  
```  
  
### <a name="to-set-up-build-and-run-the-sample"></a>Aby skonfigurować, skompilować i uruchomić przykład  
  
1. Upewnij się, że została wykonana [Procedura konfiguracji jednorazowej dla przykładów Windows Communication Foundation](one-time-setup-procedure-for-the-wcf-samples.md).  
  
2. Aby skompilować wersję rozwiązania w języku C# lub Visual Basic .NET, postępuj zgodnie z instrukcjami w temacie [Tworzenie przykładów Windows Communication Foundation](building-the-samples.md).  
  
3. Aby uruchomić przykład w konfiguracji na jednym lub wielu komputerach, postępuj zgodnie z instrukcjami w temacie [Uruchamianie przykładów Windows Communication Foundation](running-the-samples.md).  
  
> [!IMPORTANT]
> Przykłady mogą być już zainstalowane na komputerze. Przed kontynuowaniem Wyszukaj następujący katalog (domyślny).  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> Jeśli ten katalog nie istnieje, przejdź do [przykładów Windows Communication Foundation (WCF) i Windows Workflow Foundation (WF) dla .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) , aby pobrać wszystkie Windows Communication Foundation (WCF) i [!INCLUDE[wf1](../../../../includes/wf1-md.md)] przykłady. Ten przykład znajduje się w następującym katalogu.  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Contract\Service\Session`  
