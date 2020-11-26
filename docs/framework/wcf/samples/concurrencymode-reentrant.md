---
title: Procedura wielobieżna ConcurrencyMode
ms.date: 03/30/2017
ms.assetid: b2046c38-53d8-4a6c-a084-d6c7091d92b1
ms.openlocfilehash: f5b36e57a45850fec7ac27fb333af3860f1e73d3
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96243262"
---
# <a name="concurrencymode-reentrant"></a><span data-ttu-id="b3b58-102">Procedura wielobieżna ConcurrencyMode</span><span class="sxs-lookup"><span data-stu-id="b3b58-102">ConcurrencyMode Reentrant</span></span>

<span data-ttu-id="b3b58-103">Ten przykład pokazuje konieczność i implikacje użycia ConcurrencyMode. using w implementacji usługi.</span><span class="sxs-lookup"><span data-stu-id="b3b58-103">This sample demonstrates the necessity and implications of using ConcurrencyMode.Reentrant on a service implementation.</span></span> <span data-ttu-id="b3b58-104">Concurrency. repodmiotu oznacza, że usługa (lub wywołania zwrotne) przetwarza tylko jeden komunikat w danym momencie (analogicznie do `ConcurencyMode.Single` ).</span><span class="sxs-lookup"><span data-stu-id="b3b58-104">ConcurrencyMode.Reentrant implies that the service (or callback) processes only one message at a given time (analogous to `ConcurencyMode.Single`).</span></span> <span data-ttu-id="b3b58-105">Aby zapewnić bezpieczeństwo wątków, Windows Communication Foundation (WCF) blokuje `InstanceContext` Przetwarzanie komunikatu, aby nie można było przetworzyć innych komunikatów.</span><span class="sxs-lookup"><span data-stu-id="b3b58-105">To ensure thread safety, Windows Communication Foundation (WCF) locks the `InstanceContext` processing a message so that no other messages can be processed.</span></span> <span data-ttu-id="b3b58-106">W przypadku trybu przechodzenia, `InstanceContext` jest odblokowany tuż przed wykonaniem wywołania wychodzącego przez usługę, co pozwala na kolejne wywołanie (które może być w sposób pokazany w przykładzie), aby uzyskać blokadę po następnym przejściu do usługi.</span><span class="sxs-lookup"><span data-stu-id="b3b58-106">In case of Reentrant mode, the `InstanceContext` is unlocked just before the service makes an outgoing call thereby allowing the subsequent call, (which can be reentrant as demonstrated in the sample) to get the lock next time it comes in to the service.</span></span> <span data-ttu-id="b3b58-107">Aby zademonstrować zachowanie, przykład pokazuje, jak klient i usługa mogą wysyłać komunikaty między sobą przy użyciu kontraktu dupleksowego.</span><span class="sxs-lookup"><span data-stu-id="b3b58-107">To demonstrate the behavior, the sample shows how a client and service can send messages between each other using a duplex contract.</span></span>  
  
 <span data-ttu-id="b3b58-108">Zdefiniowany kontrakt jest umową dupleksową z `Ping` metodą implementowaną przez usługę i metodę wywołania zwrotnego `Pong` implementowaną przez klienta.</span><span class="sxs-lookup"><span data-stu-id="b3b58-108">The contract defined is a duplex contract with the `Ping` method being implemented by the service and the callback method `Pong` being implemented by the client.</span></span> <span data-ttu-id="b3b58-109">Klient wywołuje `Ping` metodę serwera z liczbą cyklów, co spowoduje zainicjowanie wywołania.</span><span class="sxs-lookup"><span data-stu-id="b3b58-109">A client invokes the server's `Ping` method with a tick count thereby initiating the call.</span></span> <span data-ttu-id="b3b58-110">Usługa sprawdza, czy liczba cykli nie jest równa 0, a następnie wywołuje metodę wywołania zwrotnego `Pong` przy zmniejszeniu liczby taktów.</span><span class="sxs-lookup"><span data-stu-id="b3b58-110">The service checks whether the tick count is not equal to 0 and then invokes the callbacks `Pong` method while decrementing the tick count.</span></span> <span data-ttu-id="b3b58-111">Jest to realizowane przez Poniższy kod w przykładzie.</span><span class="sxs-lookup"><span data-stu-id="b3b58-111">This is done by the following code in the sample.</span></span>  
  
```csharp
public void Ping(int ticks)  
{  
     Console.WriteLine("Ping: Ticks = " + ticks);  
     //Keep pinging back and forth till Ticks reaches 0.  
     if (ticks != 0)  
     {  
         OperationContext.Current.GetCallbackChannel<IPingPongCallback>().Pong((ticks - 1));  
     }  
}  
```  
  
 Implementacja wywołania zwrotnego `Pong` ma taką samą logikę jak `Ping` implementacja. Oznacza to, że sprawdza, czy liczba cykli nie jest równa zero, a następnie wywołuje `Ping` metodę w kanale wywołania zwrotnego (w tym przypadku jest to kanał, który został użyty do wysłania oryginalnej `Ping` wiadomości) z liczbą cykli równą 1. Moment, w którym licznik taktu osiągnie wartość 0, metoda zwraca w ten sposób odpakowanie wszystkich odpowiedzi z powrotem do pierwszego wywołania wykonanego przez klienta, który zainicjował wywołanie. <span data-ttu-id="b3b58-115">Jest to pokazane w implementacji wywołania zwrotnego.</span><span class="sxs-lookup"><span data-stu-id="b3b58-115">This is shown in the callback implementation.</span></span>  
  
```csharp
public void Pong(int ticks)  
{  
    Console.WriteLine("Pong: Ticks = " + ticks);  
    if (ticks != 0)  
    {  
        //Retrieve the Callback  Channel (in this case the Channel which was used to send the  
        //original message) and make an outgoing call until ticks reaches 0.  
        IPingPong channel = OperationContext.Current.GetCallbackChannel<IPingPong>();  
        channel.Ping((ticks - 1));  
    }  
}  
```  
  
 Obie `Ping` metody i `Pong` są żądaniami/odpowiedzi, co oznacza, że pierwsze wywołanie `Ping` nie zwraca do momentu wywołania `CallbackChannel<T>.Pong()` zwrotnego. Na kliencie `Pong` Metoda nie może zwrócić do momentu następnego `Ping` wywołania, które wykona. <span data-ttu-id="b3b58-118">Ponieważ zarówno wywołanie zwrotne, jak i usługa muszą wychodzące wywołania żądania/odpowiedzi, zanim będą mogły odpowiedzieć na oczekujące żądanie, obie implementacje muszą być oznaczone jako takie jak zachowanie.</span><span class="sxs-lookup"><span data-stu-id="b3b58-118">Because both the callback and the service must make outgoing request/reply calls before they can reply for the pending request, both the implementations must be marked with the ConcurrencyMode.Reentrant behavior.</span></span>  
  
### <a name="to-set-up-build-and-run-the-sample"></a><span data-ttu-id="b3b58-119">Aby skonfigurować, skompilować i uruchomić przykład</span><span class="sxs-lookup"><span data-stu-id="b3b58-119">To set up, build, and run the sample</span></span>  
  
1. <span data-ttu-id="b3b58-120">Upewnij się, że została wykonana [Procedura konfiguracji jednorazowej dla przykładów Windows Communication Foundation](one-time-setup-procedure-for-the-wcf-samples.md).</span><span class="sxs-lookup"><span data-stu-id="b3b58-120">Ensure that you have performed the [One-Time Setup Procedure for the Windows Communication Foundation Samples](one-time-setup-procedure-for-the-wcf-samples.md).</span></span>  
  
2. <span data-ttu-id="b3b58-121">Aby skompilować wersję rozwiązania w języku C# lub Visual Basic .NET, postępuj zgodnie z instrukcjami w temacie [Tworzenie przykładów Windows Communication Foundation](building-the-samples.md).</span><span class="sxs-lookup"><span data-stu-id="b3b58-121">To build the C# or Visual Basic .NET edition of the solution, follow the instructions in [Building the Windows Communication Foundation Samples](building-the-samples.md).</span></span>  
  
3. <span data-ttu-id="b3b58-122">Aby uruchomić przykład w konfiguracji na jednym lub wielu komputerach, postępuj zgodnie z instrukcjami w temacie [Uruchamianie przykładów Windows Communication Foundation](running-the-samples.md).</span><span class="sxs-lookup"><span data-stu-id="b3b58-122">To run the sample in a single- or cross-machine configuration, follow the instructions in [Running the Windows Communication Foundation Samples](running-the-samples.md).</span></span>  
  
## <a name="demonstrates"></a><span data-ttu-id="b3b58-123">Demonstracje</span><span class="sxs-lookup"><span data-stu-id="b3b58-123">Demonstrates</span></span>  

 <span data-ttu-id="b3b58-124">Aby uruchomić przykład, skompiluj projekty klienta i serwera.</span><span class="sxs-lookup"><span data-stu-id="b3b58-124">To run the sample, build the client and server projects.</span></span> <span data-ttu-id="b3b58-125">Następnie otwórz dwa okna poleceń i zmień katalogi na \<sample> katalogi \CS\Service\bin\debug i \<sample> \CS\Client\bin\debug.</span><span class="sxs-lookup"><span data-stu-id="b3b58-125">Then open two command windows and change the directories to the \<sample>\CS\Service\bin\debug and \<sample>\CS\Client\bin\debug directories.</span></span> <span data-ttu-id="b3b58-126">Następnie uruchom usługę, wpisując `service.exe` , a następnie Wywołaj Client.exe z początkową wartością taktów przekazaną jako argument wejściowy.</span><span class="sxs-lookup"><span data-stu-id="b3b58-126">Then start the service by typing `service.exe` and then invoke the Client.exe with the initial value of ticks passed as an input argument.</span></span> <span data-ttu-id="b3b58-127">Pokazano przykładowe dane wyjściowe dla 10 taktów.</span><span class="sxs-lookup"><span data-stu-id="b3b58-127">A sample output for 10 ticks is shown.</span></span>  
  
```console  
Prompt>Service.exe  
ServiceHost Started. Press Enter to terminate service.  
Ping: Ticks = 10  
Ping: Ticks = 8  
Ping: Ticks = 6  
Ping: Ticks = 4  
Ping: Ticks = 2  
Ping: Ticks = 0  
  
Prompt>Client.exe 10  
Pong: Ticks = 9  
Pong: Ticks = 7  
Pong: Ticks = 5  
Pong: Ticks = 3  
Pong: Ticks = 1  
```  
  
> [!IMPORTANT]
> <span data-ttu-id="b3b58-128">Przykłady mogą być już zainstalowane na komputerze.</span><span class="sxs-lookup"><span data-stu-id="b3b58-128">The samples may already be installed on your machine.</span></span> <span data-ttu-id="b3b58-129">Przed kontynuowaniem Wyszukaj następujący katalog (domyślny).</span><span class="sxs-lookup"><span data-stu-id="b3b58-129">Check for the following (default) directory before continuing.</span></span>  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> <span data-ttu-id="b3b58-130">Jeśli ten katalog nie istnieje, przejdź do [przykładów Windows Communication Foundation (WCF) i Windows Workflow Foundation (WF) dla .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) , aby pobrać wszystkie Windows Communication Foundation (WCF) i [!INCLUDE[wf1](../../../../includes/wf1-md.md)] przykłady.</span><span class="sxs-lookup"><span data-stu-id="b3b58-130">If this directory does not exist, go to [Windows Communication Foundation (WCF) and Windows Workflow Foundation (WF) Samples for .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) to download all Windows Communication Foundation (WCF) and [!INCLUDE[wf1](../../../../includes/wf1-md.md)] samples.</span></span> <span data-ttu-id="b3b58-131">Ten przykład znajduje się w następującym katalogu.</span><span class="sxs-lookup"><span data-stu-id="b3b58-131">This sample is located in the following directory.</span></span>  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Services\Reentrant`  
