---
title: Omówienie transakcji WCF (Windows Communication Foundation)
ms.date: 03/30/2017
helpviewer_keywords:
- transactions [WCF]
- WCF, transactions
- Windows Communication Foundation, transactions
ms.assetid: c7757854-1207-4019-8b31-552578b7d570
ms.openlocfilehash: 1486290241fdb40d415278c4a01738aa711e2182
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96261478"
---
# <a name="windows-communication-foundation-transactions-overview"></a><span data-ttu-id="1c859-102">Omówienie transakcji WCF (Windows Communication Foundation)</span><span class="sxs-lookup"><span data-stu-id="1c859-102">Windows Communication Foundation Transactions Overview</span></span>

<span data-ttu-id="1c859-103">Transakcje umożliwiają grupowanie zestawu akcji lub operacji w pojedynczą niepodzielną jednostkę wykonania.</span><span class="sxs-lookup"><span data-stu-id="1c859-103">Transactions provide a way to group a set of actions or operations into a single indivisible unit of execution.</span></span> <span data-ttu-id="1c859-104">Transakcja jest kolekcją operacji o następujących właściwościach:</span><span class="sxs-lookup"><span data-stu-id="1c859-104">A transaction is a collection of operations with the following properties:</span></span>  
  
- <span data-ttu-id="1c859-105">Niepodzielność.</span><span class="sxs-lookup"><span data-stu-id="1c859-105">Atomicity.</span></span> <span data-ttu-id="1c859-106">Pozwala to zagwarantować, że wszystkie aktualizacje ukończone w ramach określonej transakcji zostaną zatwierdzone i wykonane w sposób trwały lub wszystkie są przerywane i wycofywane do poprzedniego stanu.</span><span class="sxs-lookup"><span data-stu-id="1c859-106">This ensures that either all of the updates completed under a specific transaction are committed and made durable or they are all aborted and rolled back to their previous state.</span></span>  
  
- <span data-ttu-id="1c859-107">Spójność.</span><span class="sxs-lookup"><span data-stu-id="1c859-107">Consistency.</span></span> <span data-ttu-id="1c859-108">Gwarantuje to, że zmiany wprowadzone w ramach transakcji reprezentują transformację z jednego stanu spójnego na inny.</span><span class="sxs-lookup"><span data-stu-id="1c859-108">This guarantees that the changes made under a transaction represent a transformation from one consistent state to another.</span></span> <span data-ttu-id="1c859-109">Na przykład transakcja, która przenosi pieniądze z konta kontroli na konto oszczędnościowe, nie zmienia kwoty pieniędzy w ogólnym koncie bankowym.</span><span class="sxs-lookup"><span data-stu-id="1c859-109">For example, a transaction that transfers money from a checking account to a savings account does not change the amount of money in the overall bank account.</span></span>  
  
- <span data-ttu-id="1c859-110">Izolacja.</span><span class="sxs-lookup"><span data-stu-id="1c859-110">Isolation.</span></span> <span data-ttu-id="1c859-111">Zapobiega to obserwowanie niezatwierdzonych zmian należących do innych współbieżnych transakcji.</span><span class="sxs-lookup"><span data-stu-id="1c859-111">This prevents a transaction from observing uncommitted changes belonging to other concurrent transactions.</span></span> <span data-ttu-id="1c859-112">Izolacja zapewnia abstrakcję współbieżności, przy jednoczesnym zapewnieniu, że jedna transakcja nie może mieć nieoczekiwanego wpływu na wykonywanie innej transakcji.</span><span class="sxs-lookup"><span data-stu-id="1c859-112">Isolation provides an abstraction of concurrency while ensuring one transaction cannot have an unexpected impact on the execution of another transaction.</span></span>  
  
- <span data-ttu-id="1c859-113">Wytrzymałości.</span><span class="sxs-lookup"><span data-stu-id="1c859-113">Durability.</span></span> <span data-ttu-id="1c859-114">Oznacza to, że po zatwierdzeniu aktualizacje zasobów zarządzanych (takich jak rekord bazy danych) będą trwałe w wyniku awarii.</span><span class="sxs-lookup"><span data-stu-id="1c859-114">This means that once committed, updates to managed resources (such as a database record) will be persistent in the face of failures.</span></span>  
  
 <span data-ttu-id="1c859-115">Windows Communication Foundation (WCF) oferuje bogaty zestaw funkcji, które umożliwiają tworzenie transakcji rozproszonych w aplikacji usługi sieci Web.</span><span class="sxs-lookup"><span data-stu-id="1c859-115">Windows Communication Foundation (WCF) provides a rich set of features that enable you to create distributed transactions in your Web service application.</span></span>  
  
 <span data-ttu-id="1c859-116">WCF implementuje obsługę protokołu WS-AtomicTransaction (WS-AT), który umożliwia aplikacjom WCF przepływ transakcji do aplikacji międzyoperacyjnych, takich jak współdziałające usługi sieci Web stworzone przy użyciu technologii innych firm.</span><span class="sxs-lookup"><span data-stu-id="1c859-116">WCF implements support for the WS-AtomicTransaction (WS-AT) protocol that enables WCF applications to flow transactions to interoperable applications, such as interoperable Web services built using third-party technology.</span></span> <span data-ttu-id="1c859-117">Funkcja WCF implementuje również obsługę protokołu transakcji OLE, który może być używany w scenariuszach, w których nie ma potrzeby włączania przepływu transakcji.</span><span class="sxs-lookup"><span data-stu-id="1c859-117">WCF also implements support for the OLE Transactions protocol, which can be used in scenarios where you do not need interop functionality to enable transaction flow.</span></span>  
  
 <span data-ttu-id="1c859-118">Możesz użyć pliku konfiguracji aplikacji, aby skonfigurować powiązania do włączania lub wyłączania przepływu transakcji, a także ustawić żądany protokół transakcyjny dla powiązania.</span><span class="sxs-lookup"><span data-stu-id="1c859-118">You can use an application configuration file to configure bindings to enable or disable transaction flow, as well as set the desired transaction protocol on a binding.</span></span> <span data-ttu-id="1c859-119">Ponadto można ustawić limity czasu transakcji na poziomie usługi przy użyciu pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="1c859-119">In addition, you can set transaction time-outs at the service level using the configuration file.</span></span> <span data-ttu-id="1c859-120">Aby uzyskać więcej informacji, zobacz [Włączanie przepływu transakcji](enabling-transaction-flow.md).</span><span class="sxs-lookup"><span data-stu-id="1c859-120">For more information, see [Enabling Transaction Flow](enabling-transaction-flow.md).</span></span>  
  
 <span data-ttu-id="1c859-121">Atrybuty transakcji w <xref:System.ServiceModel> przestrzeni nazw umożliwiają wykonywanie następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="1c859-121">Transaction attributes in the <xref:System.ServiceModel> namespace allow you to do the following:</span></span>  
  
- <span data-ttu-id="1c859-122">Skonfiguruj limity czasu transakcji i filtrowanie na poziomie izolacji przy użyciu <xref:System.ServiceModel.ServiceBehaviorAttribute> atrybutu.</span><span class="sxs-lookup"><span data-stu-id="1c859-122">Configure transaction time-outs and isolation-level filtering using the <xref:System.ServiceModel.ServiceBehaviorAttribute> attribute.</span></span>  
  
- <span data-ttu-id="1c859-123">Włącz funkcje transakcji i skonfiguruj zachowanie realizacji transakcji przy użyciu <xref:System.ServiceModel.OperationBehaviorAttribute> atrybutu.</span><span class="sxs-lookup"><span data-stu-id="1c859-123">Enable transactions functionality and configure transaction completion behavior using the <xref:System.ServiceModel.OperationBehaviorAttribute> attribute.</span></span>  
  
- <span data-ttu-id="1c859-124">Użyj <xref:System.ServiceModel.ServiceContractAttribute> atrybutów i <xref:System.ServiceModel.OperationContractAttribute> dla metody Contract, aby wymagać, zezwalać lub odmawiać przepływu transakcji.</span><span class="sxs-lookup"><span data-stu-id="1c859-124">Use the <xref:System.ServiceModel.ServiceContractAttribute> and <xref:System.ServiceModel.OperationContractAttribute> attributes on a contract method to require, allow or deny transaction flow.</span></span>  
  
 <span data-ttu-id="1c859-125">Aby uzyskać więcej informacji, zobacz [atrybuty transakcji ServiceModel](servicemodel-transaction-attributes.md).</span><span class="sxs-lookup"><span data-stu-id="1c859-125">For more information, see [ServiceModel Transaction Attributes](servicemodel-transaction-attributes.md).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="1c859-126">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="1c859-126">See also</span></span>

- [<span data-ttu-id="1c859-127">Atrybuty transakcji elementu ServiceModel</span><span class="sxs-lookup"><span data-stu-id="1c859-127">ServiceModel Transaction Attributes</span></span>](servicemodel-transaction-attributes.md)
- [<span data-ttu-id="1c859-128">Włączanie przepływu transakcji</span><span class="sxs-lookup"><span data-stu-id="1c859-128">Enabling Transaction Flow</span></span>](enabling-transaction-flow.md)
