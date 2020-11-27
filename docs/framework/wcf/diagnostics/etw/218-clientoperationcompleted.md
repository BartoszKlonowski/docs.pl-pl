---
title: 218 — ClientOperationCompleted
ms.date: 03/30/2017
ms.assetid: b069bced-7bb2-4e01-8227-e5dbda17af09
ms.openlocfilehash: d74aa77aff7b45b50f6891c999889011d9e03381
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96278859"
---
# <a name="218---clientoperationcompleted"></a><span data-ttu-id="ce221-102">218 — ClientOperationCompleted</span><span class="sxs-lookup"><span data-stu-id="ce221-102">218 - ClientOperationCompleted</span></span>

## <a name="properties"></a><span data-ttu-id="ce221-103">Właściwości</span><span class="sxs-lookup"><span data-stu-id="ce221-103">Properties</span></span>  
  
|||  
|-|-|  
|<span data-ttu-id="ce221-104">ID (Identyfikator)</span><span class="sxs-lookup"><span data-stu-id="ce221-104">ID</span></span>|<span data-ttu-id="ce221-105">218</span><span class="sxs-lookup"><span data-stu-id="ce221-105">218</span></span>|  
|<span data-ttu-id="ce221-106">Słowa kluczowe</span><span class="sxs-lookup"><span data-stu-id="ce221-106">Keywords</span></span>|<span data-ttu-id="ce221-107">Rozwiązywanie problemów, ServiceModel</span><span class="sxs-lookup"><span data-stu-id="ce221-107">Troubleshooting, ServiceModel</span></span>|  
|<span data-ttu-id="ce221-108">Poziom</span><span class="sxs-lookup"><span data-stu-id="ce221-108">Level</span></span>|<span data-ttu-id="ce221-109">Informacje</span><span class="sxs-lookup"><span data-stu-id="ce221-109">Information</span></span>|  
|<span data-ttu-id="ce221-110">Kanał</span><span class="sxs-lookup"><span data-stu-id="ce221-110">Channel</span></span>|<span data-ttu-id="ce221-111">Microsoft-Windows-Application Server-Applications/Analytics</span><span class="sxs-lookup"><span data-stu-id="ce221-111">Microsoft-Windows-Application Server-Applications/Analytic</span></span>|  
  
## <a name="description"></a><span data-ttu-id="ce221-112">Opis</span><span class="sxs-lookup"><span data-stu-id="ce221-112">Description</span></span>  

 <span data-ttu-id="ce221-113">To zdarzenie jest emitowane przez klientów tuż po zakończeniu operacji.</span><span class="sxs-lookup"><span data-stu-id="ce221-113">This event is emitted by clients just after an operation completes.</span></span> <span data-ttu-id="ce221-114">W przypadku operacji jednokierunkowych jest to zaraz po pomyślnym wysłaniu wiadomości.</span><span class="sxs-lookup"><span data-stu-id="ce221-114">For one-way operations, this is just after the message is sent successfully.</span></span> <span data-ttu-id="ce221-115">W przypadku operacji żądanie-odpowiedź jest to po odebraniu odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="ce221-115">For request-response operations this is after the response is received.</span></span>  
  
## <a name="message"></a><span data-ttu-id="ce221-116">Wiadomość</span><span class="sxs-lookup"><span data-stu-id="ce221-116">Message</span></span>  

 <span data-ttu-id="ce221-117">Klient ukończył wykonywanie akcji "%1" skojarzonej z kontraktem "%2".</span><span class="sxs-lookup"><span data-stu-id="ce221-117">The Client completed executing Action '%1' associated with the '%2' contract.</span></span> <span data-ttu-id="ce221-118">Wiadomość została wysłana do ' %3 '.</span><span class="sxs-lookup"><span data-stu-id="ce221-118">The message was sent to '%3'.</span></span>  
  
## <a name="details"></a><span data-ttu-id="ce221-119">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="ce221-119">Details</span></span>  
  
|<span data-ttu-id="ce221-120">Nazwa elementu danych</span><span class="sxs-lookup"><span data-stu-id="ce221-120">Data Item Name</span></span>|<span data-ttu-id="ce221-121">Typ elementu danych</span><span class="sxs-lookup"><span data-stu-id="ce221-121">Data Item Type</span></span>|<span data-ttu-id="ce221-122">Opis</span><span class="sxs-lookup"><span data-stu-id="ce221-122">Description</span></span>|  
|--------------------|--------------------|-----------------|  
|<span data-ttu-id="ce221-123">Akcja</span><span class="sxs-lookup"><span data-stu-id="ce221-123">Action</span></span>|<span data-ttu-id="ce221-124">XS: ciąg</span><span class="sxs-lookup"><span data-stu-id="ce221-124">xs:string</span></span>|<span data-ttu-id="ce221-125">Nagłówek akcji protokołu SOAP wiadomości wychodzącej.</span><span class="sxs-lookup"><span data-stu-id="ce221-125">The SOAP action header of the outgoing message.</span></span>|  
|<span data-ttu-id="ce221-126">Nazwa kontraktu</span><span class="sxs-lookup"><span data-stu-id="ce221-126">Contract Name</span></span>|`xs:string`|<span data-ttu-id="ce221-127">Nazwa kontraktu.</span><span class="sxs-lookup"><span data-stu-id="ce221-127">The name of the contract.</span></span> <span data-ttu-id="ce221-128">Przykład: ICalculator.</span><span class="sxs-lookup"><span data-stu-id="ce221-128">Example: ICalculator.</span></span>|  
|<span data-ttu-id="ce221-129">Element docelowy</span><span class="sxs-lookup"><span data-stu-id="ce221-129">Destination</span></span>|`xs:string`|<span data-ttu-id="ce221-130">Adres punktu końcowego usługi, do którego wiadomość została wysłana.</span><span class="sxs-lookup"><span data-stu-id="ce221-130">The address of the service endpoint that the message was sent to.</span></span>|  
|<span data-ttu-id="ce221-131">HostReference</span><span class="sxs-lookup"><span data-stu-id="ce221-131">HostReference</span></span>|`xs:string`|<span data-ttu-id="ce221-132">W przypadku usług hostowanych w sieci Web to pole jednoznacznie identyfikuje usługę w hierarchii sieci Web.</span><span class="sxs-lookup"><span data-stu-id="ce221-132">For Web-hosted services, this field uniquely identifies the service in the Web hierarchy.</span></span> <span data-ttu-id="ce221-133">Jego format jest zdefiniowany jako ścieżka wirtualna aplikacji nazwa witryny sieci Web&#124;wirtualnej ścieżki usługi&#124;ServiceName '.</span><span class="sxs-lookup"><span data-stu-id="ce221-133">Its format is defined as 'Web Site Name Application Virtual Path&#124;Service Virtual Path&#124;ServiceName'.</span></span> <span data-ttu-id="ce221-134">Przykład: "Default Web site/CalculatorApplication&#124;/CalculatorService.svc&#124;CalculatorService".</span><span class="sxs-lookup"><span data-stu-id="ce221-134">Example: 'Default Web Site/CalculatorApplication&#124;/CalculatorService.svc&#124;CalculatorService'.</span></span>|  
|<span data-ttu-id="ce221-135">Wywołując</span><span class="sxs-lookup"><span data-stu-id="ce221-135">AppDomain</span></span>|`xs:string`|<span data-ttu-id="ce221-136">Ciąg zwracany przez element AppDomain. CurrentDomain —. FriendlyName.</span><span class="sxs-lookup"><span data-stu-id="ce221-136">The string returned by AppDomain.CurrentDomain.FriendlyName.</span></span>|
