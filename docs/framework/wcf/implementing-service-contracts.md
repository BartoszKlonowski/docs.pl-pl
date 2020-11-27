---
title: Implementowanie kontraktów usług
ms.date: 03/30/2017
helpviewer_keywords:
- implementing service contracts [WCF]
ms.assetid: aefb6f56-47e3-4f24-ab0a-9bc07bf9885f
ms.openlocfilehash: 121922e3de62653babdac084d6bd226f7263e33c
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96262739"
---
# <a name="implementing-service-contracts"></a><span data-ttu-id="dfae7-102">Implementowanie kontraktów usług</span><span class="sxs-lookup"><span data-stu-id="dfae7-102">Implementing Service Contracts</span></span>

<span data-ttu-id="dfae7-103">Usługa jest klasą, która udostępnia klientom funkcje dostępne dla klientów w co najmniej jednym punkcie końcowym.</span><span class="sxs-lookup"><span data-stu-id="dfae7-103">A service is a class that exposes functionality available to clients at one or more endpoints.</span></span> <span data-ttu-id="dfae7-104">Aby utworzyć usługę, napisz klasę implementującą kontrakt Windows Communication Foundation (WCF).</span><span class="sxs-lookup"><span data-stu-id="dfae7-104">To create a service, write a class that implements a Windows Communication Foundation (WCF) contract.</span></span> <span data-ttu-id="dfae7-105">Możesz to zrobić na dwa sposoby.</span><span class="sxs-lookup"><span data-stu-id="dfae7-105">You can do this in one of two ways.</span></span> <span data-ttu-id="dfae7-106">Kontrakt można zdefiniować oddzielnie jako interfejs, a następnie utworzyć klasę, która implementuje ten interfejs.</span><span class="sxs-lookup"><span data-stu-id="dfae7-106">You can define the contract separately as an interface and then create a class that implements that interface.</span></span> <span data-ttu-id="dfae7-107">Alternatywnie można utworzyć klasę i umowę bezpośrednio przez umieszczenie <xref:System.ServiceModel.ServiceContractAttribute> atrybutu w samej klasie i <xref:System.ServiceModel.OperationContractAttribute> atrybutu w metodach dostępnych dla klientów usługi.</span><span class="sxs-lookup"><span data-stu-id="dfae7-107">Alternatively, you can create the class and contract directly by placing the <xref:System.ServiceModel.ServiceContractAttribute> attribute on the class itself and the <xref:System.ServiceModel.OperationContractAttribute> attribute on the methods available to the clients of the service.</span></span>  
  
## <a name="creating-a-service-class"></a><span data-ttu-id="dfae7-108">Tworzenie klasy usługi</span><span class="sxs-lookup"><span data-stu-id="dfae7-108">Creating a service class</span></span>  

 <span data-ttu-id="dfae7-109">Poniżej znajduje się przykład usługi implementującej `IMath` kontrakt, który został zdefiniowany osobno.</span><span class="sxs-lookup"><span data-stu-id="dfae7-109">The following is an example of a service that implements an `IMath` contract that has been defined separately.</span></span>  
  
```csharp  
// Define the IMath contract.  
[ServiceContract]  
public interface IMath  
{  
    [OperationContract]
    double Add(double A, double B);  
  
    [OperationContract]  
    double Multiply (double A, double B);  
}  
  
// Implement the IMath contract in the MathService class.  
public class MathService : IMath  
{  
    public double Add (double A, double B) { return A + B; }  
    public double Multiply (double A, double B) { return A * B; }  
}  
```  
  
 <span data-ttu-id="dfae7-110">Alternatywnie usługa może bezpośrednio uwidocznić umowę.</span><span class="sxs-lookup"><span data-stu-id="dfae7-110">Alternatively, a service can expose a contract directly.</span></span> <span data-ttu-id="dfae7-111">Poniżej znajduje się przykład klasy usługi, która definiuje i implementuje `MathService` kontrakt.</span><span class="sxs-lookup"><span data-stu-id="dfae7-111">The following is an example of a service class that defines and implements a `MathService` contract.</span></span>  
  
```csharp  
// Define the MathService contract directly on the service class.  
[ServiceContract]  
class MathService  
{  
    [OperationContract]  
    public double Add(double A, double B) { return A + B; }  
    [OperationContract]  
    private double Multiply (double A, double B) { return A * B; }  
}  
```  
  
 <span data-ttu-id="dfae7-112">Należy pamiętać, że poprzednie usługi uwidaczniają różne kontrakty, ponieważ nazwy kontraktów są różne.</span><span class="sxs-lookup"><span data-stu-id="dfae7-112">Note that the preceding services expose different contracts because the contract names are different.</span></span> <span data-ttu-id="dfae7-113">W pierwszym przypadku, narażony kontrakt nosi nazwę " `IMath` ", natomiast w drugim przypadku kontrakt nosi nazwę " `MathService` ".</span><span class="sxs-lookup"><span data-stu-id="dfae7-113">In the first case, the exposed contract is named "`IMath`" while in the second case the contract is named "`MathService`".</span></span>  
  
 <span data-ttu-id="dfae7-114">Można ustawić kilka rzeczy na poziomach implementacji usługi i operacji, takich jak współbieżność i Tworzenie wystąpień.</span><span class="sxs-lookup"><span data-stu-id="dfae7-114">You can set a few things at the service and operation implementation levels, such as concurrency and instancing.</span></span> <span data-ttu-id="dfae7-115">Aby uzyskać więcej informacji, zobacz [projektowanie i implementowanie usług](designing-and-implementing-services.md).</span><span class="sxs-lookup"><span data-stu-id="dfae7-115">For more information, see [Designing and Implementing Services](designing-and-implementing-services.md).</span></span>  
  
 <span data-ttu-id="dfae7-116">Po wdrożeniu kontraktu usługi należy utworzyć co najmniej jeden punkt końcowy dla usługi.</span><span class="sxs-lookup"><span data-stu-id="dfae7-116">After implementing a service contract, you must create one or more endpoints for the service.</span></span> <span data-ttu-id="dfae7-117">Aby uzyskać więcej informacji, zobacz [Omówienie tworzenia punktów końcowych](endpoint-creation-overview.md).</span><span class="sxs-lookup"><span data-stu-id="dfae7-117">For more information, see [Endpoint Creation Overview](endpoint-creation-overview.md).</span></span> <span data-ttu-id="dfae7-118">Aby uzyskać więcej informacji na temat sposobu uruchamiania usługi, zobacz [usługi hostingu](hosting-services.md).</span><span class="sxs-lookup"><span data-stu-id="dfae7-118">For more information about how to run a service, see [Hosting Services](hosting-services.md).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="dfae7-119">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="dfae7-119">See also</span></span>

- [<span data-ttu-id="dfae7-120">Projektowanie i implementowanie usług</span><span class="sxs-lookup"><span data-stu-id="dfae7-120">Designing and Implementing Services</span></span>](designing-and-implementing-services.md)
- [<span data-ttu-id="dfae7-121">Instrukcje: tworzenie usługi za pomocą klasy kontraktu</span><span class="sxs-lookup"><span data-stu-id="dfae7-121">How to: Create a Service with a Contract Class</span></span>](./feature-details/how-to-create-a-wcf-contract-with-a-class.md)
- [<span data-ttu-id="dfae7-122">Instrukcje: tworzenie usługi przy użyciu interfejsu kontraktu</span><span class="sxs-lookup"><span data-stu-id="dfae7-122">How to: Create a Service with a Contract Interface</span></span>](./feature-details/how-to-create-a-service-with-a-contract-interface.md)
- [<span data-ttu-id="dfae7-123">Określanie zachowania środowiska uruchomieniowego usługi</span><span class="sxs-lookup"><span data-stu-id="dfae7-123">Specifying Service Run-Time Behavior</span></span>](specifying-service-run-time-behavior.md)
