---
title: 'Instrukcje: tworzenie usługi przy użyciu interfejsu kontraktu'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 7b6803f6-d6f9-4cc2-9f1b-6f4c920475d5
ms.openlocfilehash: 2234e6fe8d0ee2e0029a061ba96ef84f840f0c9b
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96286347"
---
# <a name="how-to-create-a-service-with-a-contract-interface"></a><span data-ttu-id="ae5fc-102">Instrukcje: tworzenie usługi przy użyciu interfejsu kontraktu</span><span class="sxs-lookup"><span data-stu-id="ae5fc-102">How to: Create a Service with a Contract Interface</span></span>

<span data-ttu-id="ae5fc-103">Preferowanym sposobem utworzenia kontraktu Windows Communication Foundation (WCF) jest użycie interfejsu.</span><span class="sxs-lookup"><span data-stu-id="ae5fc-103">The preferred way to create a Windows Communication Foundation (WCF) contract is by using an interface.</span></span> <span data-ttu-id="ae5fc-104">Ta umowa określa zbieranie i strukturę komunikatów wymaganych do uzyskania dostępu do operacji oferowanych przez usługę.</span><span class="sxs-lookup"><span data-stu-id="ae5fc-104">This contract specifies the collection and structure of messages required to access the operations the service offers.</span></span> <span data-ttu-id="ae5fc-105">Ten interfejs definiuje typy wejściowe i wyjściowe przez zastosowanie <xref:System.ServiceModel.ServiceContractAttribute> klasy do interfejsu i <xref:System.ServiceModel.OperationContractAttribute> klasy do metod, które mają zostać ujawnione.</span><span class="sxs-lookup"><span data-stu-id="ae5fc-105">This interface defines the input and output types by applying the <xref:System.ServiceModel.ServiceContractAttribute> class to the interface and the <xref:System.ServiceModel.OperationContractAttribute> class to the methods that you want to expose.</span></span>  
  
 <span data-ttu-id="ae5fc-106">Aby uzyskać więcej informacji na temat umów dotyczących usług, zobacz [Projektowanie kontraktów usług](../designing-service-contracts.md).</span><span class="sxs-lookup"><span data-stu-id="ae5fc-106">For more information about service contracts, see [Designing Service Contracts](../designing-service-contracts.md).</span></span>  
  
### <a name="creating-a-wcf-contract-with-an-interface"></a><span data-ttu-id="ae5fc-107">Tworzenie kontraktu WCF z interfejsem</span><span class="sxs-lookup"><span data-stu-id="ae5fc-107">Creating a WCF contract with an interface</span></span>  
  
1. <span data-ttu-id="ae5fc-108">Utwórz nowy interfejs przy użyciu Visual Basic, C# lub dowolnego innego języka środowiska uruchomieniowego języka wspólnego.</span><span class="sxs-lookup"><span data-stu-id="ae5fc-108">Create a new interface using Visual Basic, C#, or any other common language runtime language.</span></span>  
  
2. <span data-ttu-id="ae5fc-109">Zastosuj <xref:System.ServiceModel.ServiceContractAttribute> klasę do interfejsu.</span><span class="sxs-lookup"><span data-stu-id="ae5fc-109">Apply the <xref:System.ServiceModel.ServiceContractAttribute> class to the interface.</span></span>  
  
3. <span data-ttu-id="ae5fc-110">Zdefiniuj metody w interfejsie.</span><span class="sxs-lookup"><span data-stu-id="ae5fc-110">Define the methods in the interface.</span></span>  
  
4. <span data-ttu-id="ae5fc-111">Zastosuj <xref:System.ServiceModel.OperationContractAttribute> klasę do każdej metody, która musi być ujawniona w ramach publicznego kontraktu WCF.</span><span class="sxs-lookup"><span data-stu-id="ae5fc-111">Apply the <xref:System.ServiceModel.OperationContractAttribute> class to each method that must be exposed as part of the public WCF contract.</span></span>  
  
## <a name="example"></a><span data-ttu-id="ae5fc-112">Przykład</span><span class="sxs-lookup"><span data-stu-id="ae5fc-112">Example</span></span>  

 <span data-ttu-id="ae5fc-113">Poniższy przykład kodu przedstawia interfejs, który definiuje kontrakt usługi.</span><span class="sxs-lookup"><span data-stu-id="ae5fc-113">The following code example shows an interface that defines a service contract.</span></span>  
  
 [!code-csharp[c_HowTo_CreateContractWithInterface#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_createcontractwithinterface/cs/source.cs#1)]
 [!code-vb[c_HowTo_CreateContractWithInterface#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_createcontractwithinterface/vb/source.vb#1)]  
  
 <span data-ttu-id="ae5fc-114">Metody, do których <xref:System.ServiceModel.OperationContractAttribute> zastosowano klasę, domyślnie używają wzorca komunikatów żądanie-odpowiedź.</span><span class="sxs-lookup"><span data-stu-id="ae5fc-114">The methods that have the <xref:System.ServiceModel.OperationContractAttribute> class applied use a request-reply message pattern by default.</span></span> <span data-ttu-id="ae5fc-115">Aby uzyskać więcej informacji na temat tego wzorca wiadomości, zobacz [How to: Create a Request-Reply Contract](how-to-create-a-request-reply-contract.md).</span><span class="sxs-lookup"><span data-stu-id="ae5fc-115">For more information about this message pattern, see [How to: Create a Request-Reply Contract](how-to-create-a-request-reply-contract.md).</span></span> <span data-ttu-id="ae5fc-116">Można również tworzyć i używać innych wzorców komunikatów przez ustawienie właściwości atrybutu.</span><span class="sxs-lookup"><span data-stu-id="ae5fc-116">You can also create and use other message patterns by setting properties of the attribute.</span></span> <span data-ttu-id="ae5fc-117">Aby uzyskać więcej przykładów, zobacz [How to: Create a One-Way Contract](how-to-create-a-one-way-contract.md) i [How to: Create a Duplex kontraktu](how-to-create-a-duplex-contract.md).</span><span class="sxs-lookup"><span data-stu-id="ae5fc-117">For more examples, see [How to: Create a One-Way Contract](how-to-create-a-one-way-contract.md) and [How to: Create a Duplex Contract](how-to-create-a-duplex-contract.md).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="ae5fc-118">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="ae5fc-118">See also</span></span>

- <xref:System.ServiceModel.ServiceContractAttribute>
- <xref:System.ServiceModel.OperationContractAttribute>
