---
title: Zapisywanie aplikacji transakcyjnej
description: Napisz aplikację transakcyjną w programie .NET. Użyj jawnego lub niejawnego modelu programowania z klasą transakcji lub klasą TransactionScope, odpowiednio.
ms.date: 03/30/2017
ms.assetid: a4d891f2-6fc8-4395-93c6-6819492406e0
ms.openlocfilehash: b4cc33939128e61a69db319491a7d2d60ab9a819
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91186670"
---
# <a name="writing-a-transactional-application"></a><span data-ttu-id="89638-104">Zapisywanie aplikacji transakcyjnej</span><span class="sxs-lookup"><span data-stu-id="89638-104">Writing a Transactional Application</span></span>

<span data-ttu-id="89638-105">Jako programista aplikacji transakcyjnej możesz skorzystać z dwóch modeli programowania dostarczonych przez <xref:System.Transactions> przestrzeń nazw, aby utworzyć transakcję.</span><span class="sxs-lookup"><span data-stu-id="89638-105">As a transactional application programmer, you can take advantage of the two programming models provided by the <xref:System.Transactions> namespace to create a transaction.</span></span> <span data-ttu-id="89638-106">Można użyć jawnego modelu programowania przy użyciu <xref:System.Transactions.Transaction> klasy lub niejawnego modelu programowania, w którym transakcje są automatycznie zarządzane przez infrastrukturę, przy użyciu <xref:System.Transactions.TransactionScope> klasy.</span><span class="sxs-lookup"><span data-stu-id="89638-106">You can utilize the explicit programming model by using the <xref:System.Transactions.Transaction> class, or the implicit programming model in which transactions are automatically managed by the infrastructure, by using the <xref:System.Transactions.TransactionScope> class.</span></span> <span data-ttu-id="89638-107">Zalecamy użycie niejawnego modelu transakcji na potrzeby programowania.</span><span class="sxs-lookup"><span data-stu-id="89638-107">We recommend that you use the implicit transaction model for development.</span></span> <span data-ttu-id="89638-108">Więcej informacji na temat używania zakresu transakcji można znaleźć w temacie [implementowanie niejawnej transakcji przy użyciu zakresu transakcji](implementing-an-implicit-transaction-using-transaction-scope.md) .</span><span class="sxs-lookup"><span data-stu-id="89638-108">You can find more information on how to use a transaction scope in the [Implementing an Implicit Transaction using Transaction Scope](implementing-an-implicit-transaction-using-transaction-scope.md) topic.</span></span>  
  
 <span data-ttu-id="89638-109">Oba modele obsługuje zatwierdzania transakcji, gdy program dociera spójnego stanu.</span><span class="sxs-lookup"><span data-stu-id="89638-109">Both models support committing a transaction when the program reaches a consistent state.</span></span> <span data-ttu-id="89638-110">Jeśli zatwierdzanie zakończy się powodzeniem, transakcja została ona niezawodnie dokonana.</span><span class="sxs-lookup"><span data-stu-id="89638-110">If the commit succeeds, the transaction is durably committed.</span></span> <span data-ttu-id="89638-111">W przypadku niepowodzenia Zatwierdzanie transakcji przerywa.</span><span class="sxs-lookup"><span data-stu-id="89638-111">If the commit fails, the transaction aborts.</span></span> <span data-ttu-id="89638-112">Jeśli program aplikacji nie może pomyślnie ukończyć transakcji, próbuje przerwać i cofnąć skutki transakcji.</span><span class="sxs-lookup"><span data-stu-id="89638-112">If the application program cannot successfully complete the transaction, it attempts to abort and undo the transaction's effects.</span></span>  
  
## <a name="in-this-section"></a><span data-ttu-id="89638-113">W tej sekcji</span><span class="sxs-lookup"><span data-stu-id="89638-113">In This Section</span></span>  
  
### <a name="creating-a-transaction"></a><span data-ttu-id="89638-114">Tworzenie transakcji</span><span class="sxs-lookup"><span data-stu-id="89638-114">Creating a Transaction</span></span>  

 <span data-ttu-id="89638-115"><xref:System.Transactions> Nazw zawiera dwa modele do tworzenia transakcji.</span><span class="sxs-lookup"><span data-stu-id="89638-115">The <xref:System.Transactions> namespace provides two models for creating a transaction.</span></span> <span data-ttu-id="89638-116">Modele te zostały uwzględnione w następujących tematach.</span><span class="sxs-lookup"><span data-stu-id="89638-116">These models are covered in the following topics.</span></span>  
  
 [<span data-ttu-id="89638-117">Implementowanie transakcji niejawnej przy użyciu zakresu transakcji</span><span class="sxs-lookup"><span data-stu-id="89638-117">Implementing an Implicit Transaction using Transaction Scope</span></span>](implementing-an-implicit-transaction-using-transaction-scope.md)  
  
 <span data-ttu-id="89638-118">Opisuje sposób, w jaki <xref:System.Transactions> przestrzeń nazw obsługuje tworzenie niejawnych transakcji przy użyciu <xref:System.Transactions.TransactionScope> klasy.</span><span class="sxs-lookup"><span data-stu-id="89638-118">Describes how the <xref:System.Transactions> namespace supports creating implicit transactions using the <xref:System.Transactions.TransactionScope> class.</span></span>  
  
 [<span data-ttu-id="89638-119">Implementowanie transakcji jawnej przy użyciu CommitableTransaction</span><span class="sxs-lookup"><span data-stu-id="89638-119">Implementing an Explicit Transaction using CommittableTransaction</span></span>](implementing-an-explicit-transaction-using-committabletransaction.md)  
  
 <span data-ttu-id="89638-120">Opisuje sposób, w jaki <xref:System.Transactions> przestrzeń nazw obsługuje tworzenie jawnych transakcji przy użyciu <xref:System.Transactions.CommittableTransaction> klasy.</span><span class="sxs-lookup"><span data-stu-id="89638-120">Describes how the <xref:System.Transactions> namespace supports creating explicit transactions using the <xref:System.Transactions.CommittableTransaction> class.</span></span>  
  
### <a name="escalating-transaction-management"></a><span data-ttu-id="89638-121">Eskalowania zarządzania transakcji</span><span class="sxs-lookup"><span data-stu-id="89638-121">Escalating Transaction Management</span></span>  

 <span data-ttu-id="89638-122">Gdy transakcja musi uzyskać dostęp do zasobu w innej domenie aplikacji lub jeśli chcesz zarejestrować się w innym trwałym Menedżerze zasobów, transakcja zostanie automatycznie przekierowane, aby była zarządzana przez usługę MSDTC.</span><span class="sxs-lookup"><span data-stu-id="89638-122">When a transaction needs to access a resource in another application domain, or if you want to enlist in another durable resource manager, the transaction is automatically escalated to be managed by the MSDTC.</span></span> <span data-ttu-id="89638-123">Eskalacja transakcji znajduje się w temacie [Eskalacja zarządzania transakcjami](transaction-management-escalation.md) .</span><span class="sxs-lookup"><span data-stu-id="89638-123">Transaction escalation is covered in the [Transaction Management Escalation](transaction-management-escalation.md) topic.</span></span>  
  
### <a name="concurrency"></a><span data-ttu-id="89638-124">Współbieżność</span><span class="sxs-lookup"><span data-stu-id="89638-124">Concurrency</span></span>  

 <span data-ttu-id="89638-125">Temat [Zarządzanie współbieżnością z DependentTransaction](managing-concurrency-with-dependenttransaction.md) pokazuje, jak współbieżność można osiągnąć między zadaniami asynchronicznymi przy użyciu <xref:System.Transactions.DependentTransaction> klasy.</span><span class="sxs-lookup"><span data-stu-id="89638-125">The topic [Managing Concurrency with DependentTransaction](managing-concurrency-with-dependenttransaction.md) demonstrates how concurrency can be achieved between asynchronous tasks by using the <xref:System.Transactions.DependentTransaction> class.</span></span>  
  
### <a name="com-interop"></a><span data-ttu-id="89638-126">Usługę Międzyoperacyjną modelu COM +</span><span class="sxs-lookup"><span data-stu-id="89638-126">COM+ Interop</span></span>  

 <span data-ttu-id="89638-127">Temat [współdziałania z usługami przedsiębiorstwa i transakcji modelu COM+](interoperability-with-enterprise-services-and-com-transactions.md) ilustruje sposób, w jaki transakcje rozproszone mogą współdziałać z transakcjami modelu com+.</span><span class="sxs-lookup"><span data-stu-id="89638-127">The topic [Interoperability with Enterprise Services and COM+ Transactions](interoperability-with-enterprise-services-and-com-transactions.md) illustrates how you can make your distributed transactions interact with COM+ transactions.</span></span>  
  
### <a name="diagnostics"></a><span data-ttu-id="89638-128">Diagnostyka</span><span class="sxs-lookup"><span data-stu-id="89638-128">Diagnostics</span></span>  

 <span data-ttu-id="89638-129">[Ślady diagnostyczne](diagnostic-traces.md) opisują sposób użycia kodów śledzenia generowanych przez <xref:System.Transactions> infrastrukturę w celu rozwiązywania problemów z błędami w aplikacjach.</span><span class="sxs-lookup"><span data-stu-id="89638-129">[Diagnostic Traces](diagnostic-traces.md) describes how you can use the trace codes that are generated by the <xref:System.Transactions> infrastructure to troubleshoot errors in your applications.</span></span>  
  
### <a name="working-within-aspnet"></a><span data-ttu-id="89638-130">Praca w ramach programu ASP.NET</span><span class="sxs-lookup"><span data-stu-id="89638-130">Working within ASP.NET</span></span>  

 <span data-ttu-id="89638-131">[W temacie using System. Transactions w ASP.NET](using-system-transactions-in-aspnet.md) opisano, jak można pomyślnie użyć <xref:System.Transactions> wewnątrz aplikacji ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="89638-131">The [Using System.Transactions in ASP.NET](using-system-transactions-in-aspnet.md) topic describes how you can successfully use <xref:System.Transactions> inside an ASP.NET application.</span></span>
