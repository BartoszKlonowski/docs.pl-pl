---
title: Kontrakt
ms.date: 03/30/2017
ms.assetid: aa00f6b3-7e1f-4213-841a-206463fca20b
ms.openlocfilehash: 0df39bbd0b273f1e898ccbe585be288cc245b7f5
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96274143"
---
# <a name="contract"></a><span data-ttu-id="37611-102">Kontrakt</span><span class="sxs-lookup"><span data-stu-id="37611-102">Contract</span></span>

<span data-ttu-id="37611-103">Kontrakt</span><span class="sxs-lookup"><span data-stu-id="37611-103">Contract</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="37611-104">Składnia</span><span class="sxs-lookup"><span data-stu-id="37611-104">Syntax</span></span>  
  
```csharp
class Contract  
{  
  sint32 AppDomainId;  
  Behavior Behaviors[];  
  string Name;  
  string Namespace;  
  Operation Operations[];  
  sint32 ProcessId;  
  Contract ref;  
  string SessionMode;  
  string Type;  
};  
```  
  
## <a name="methods"></a><span data-ttu-id="37611-105">Metody</span><span class="sxs-lookup"><span data-stu-id="37611-105">Methods</span></span>  

 <span data-ttu-id="37611-106">Klasa kontraktu nie definiuje żadnych metod.</span><span class="sxs-lookup"><span data-stu-id="37611-106">The Contract class does not define any methods.</span></span>  
  
## <a name="properties"></a><span data-ttu-id="37611-107">Właściwości</span><span class="sxs-lookup"><span data-stu-id="37611-107">Properties</span></span>  

 <span data-ttu-id="37611-108">Klasa kontraktu ma następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="37611-108">The Contract class has the following properties:</span></span>  
  
### <a name="appdomainid"></a><span data-ttu-id="37611-109">AppDomainId</span><span class="sxs-lookup"><span data-stu-id="37611-109">AppDomainId</span></span>  

 <span data-ttu-id="37611-110">Typ danych: sint32</span><span class="sxs-lookup"><span data-stu-id="37611-110">Data type: sint32</span></span>  
  
 <span data-ttu-id="37611-111">Typ dostępu: tylko do odczytu</span><span class="sxs-lookup"><span data-stu-id="37611-111">Access type: Read-only</span></span>  
  
 <span data-ttu-id="37611-112">Identyfikator domeny aplikacji, która hostuje kontrakt.</span><span class="sxs-lookup"><span data-stu-id="37611-112">The appdomain id of the appdomain that hosts the contract.</span></span>  
  
### <a name="behaviors"></a><span data-ttu-id="37611-113">Zachowania</span><span class="sxs-lookup"><span data-stu-id="37611-113">Behaviors</span></span>  

 <span data-ttu-id="37611-114">Typ danych: tablica zachowań</span><span class="sxs-lookup"><span data-stu-id="37611-114">Data type: Behavior array</span></span>  
  
 <span data-ttu-id="37611-115">Typ dostępu: tylko do odczytu</span><span class="sxs-lookup"><span data-stu-id="37611-115">Access type: Read-only</span></span>  
  
 <span data-ttu-id="37611-116">Zachowania skojarzone z tym kontraktem.</span><span class="sxs-lookup"><span data-stu-id="37611-116">The behaviors associated with this contract.</span></span>  
  
### <a name="name"></a><span data-ttu-id="37611-117">Nazwa</span><span class="sxs-lookup"><span data-stu-id="37611-117">Name</span></span>  

 <span data-ttu-id="37611-118">Typ danych: ciąg</span><span class="sxs-lookup"><span data-stu-id="37611-118">Data type: string</span></span>  
  
 <span data-ttu-id="37611-119">Typ dostępu: tylko do odczytu</span><span class="sxs-lookup"><span data-stu-id="37611-119">Access type: Read-only</span></span>  
  
 <span data-ttu-id="37611-120">Nazwa kontraktu w języku WSDL.</span><span class="sxs-lookup"><span data-stu-id="37611-120">The name of the contract in WSDL.</span></span>  
  
### <a name="namespace"></a><span data-ttu-id="37611-121">Przestrzeń nazw</span><span class="sxs-lookup"><span data-stu-id="37611-121">Namespace</span></span>  

 <span data-ttu-id="37611-122">Typ danych: ciąg</span><span class="sxs-lookup"><span data-stu-id="37611-122">Data type: string</span></span>  
  
 <span data-ttu-id="37611-123">Typ dostępu: tylko do odczytu</span><span class="sxs-lookup"><span data-stu-id="37611-123">Access type: Read-only</span></span>  
  
 <span data-ttu-id="37611-124">Przestrzeń nazw `portType` elementu w języku WSDL.</span><span class="sxs-lookup"><span data-stu-id="37611-124">The namespace of the `portType` element in WSDL.</span></span>  
  
### <a name="operations"></a><span data-ttu-id="37611-125">Operacje</span><span class="sxs-lookup"><span data-stu-id="37611-125">Operations</span></span>  

 <span data-ttu-id="37611-126">Typ danych: tablica operacji</span><span class="sxs-lookup"><span data-stu-id="37611-126">Data type: Operation array</span></span>  
  
 <span data-ttu-id="37611-127">Typ dostępu: tylko do odczytu</span><span class="sxs-lookup"><span data-stu-id="37611-127">Access type: Read-only</span></span>  
  
 <span data-ttu-id="37611-128">Operacje na tym kontrakcie.</span><span class="sxs-lookup"><span data-stu-id="37611-128">The operations of this contract.</span></span>  
  
### <a name="processid"></a><span data-ttu-id="37611-129">Identyfikator procesu</span><span class="sxs-lookup"><span data-stu-id="37611-129">ProcessId</span></span>  

 <span data-ttu-id="37611-130">Typ danych: sint32</span><span class="sxs-lookup"><span data-stu-id="37611-130">Data type: sint32</span></span>  
  
 <span data-ttu-id="37611-131">Typ dostępu: tylko do odczytu</span><span class="sxs-lookup"><span data-stu-id="37611-131">Access type: Read-only</span></span>  
  
 <span data-ttu-id="37611-132">Identyfikator procesu, który hostuje kontrakt.</span><span class="sxs-lookup"><span data-stu-id="37611-132">The process Id of the process that hosts the contract.</span></span>  
  
### <a name="ref"></a><span data-ttu-id="37611-133">ref</span><span class="sxs-lookup"><span data-stu-id="37611-133">ref</span></span>  

 <span data-ttu-id="37611-134">Typ danych: kontrakt</span><span class="sxs-lookup"><span data-stu-id="37611-134">Data type: Contract</span></span>  
  
 <span data-ttu-id="37611-135">Typ dostępu: tylko do odczytu</span><span class="sxs-lookup"><span data-stu-id="37611-135">Access type: Read-only</span></span>  
  
 <span data-ttu-id="37611-136">Typ wywołania zwrotnego, gdy kontrakt jest kontraktem dwukierunkowym.</span><span class="sxs-lookup"><span data-stu-id="37611-136">The type of callback when the contract is a duplex contract.</span></span>  
  
### <a name="sessionmode"></a><span data-ttu-id="37611-137">SessionMode</span><span class="sxs-lookup"><span data-stu-id="37611-137">SessionMode</span></span>  

 <span data-ttu-id="37611-138">Typ danych: ciąg</span><span class="sxs-lookup"><span data-stu-id="37611-138">Data type: string</span></span>  
  
 <span data-ttu-id="37611-139">Typ dostępu: tylko do odczytu</span><span class="sxs-lookup"><span data-stu-id="37611-139">Access type: Read-only</span></span>  
  
 <span data-ttu-id="37611-140">Wskazuje, czy kontrakt wymaga powiązania skojarzonego z tym kontraktem, aby można było używać sesji kanału.</span><span class="sxs-lookup"><span data-stu-id="37611-140">Indicates whether the contract requires the binding associated with this contract to use channel sessions.</span></span>  
  
### <a name="type"></a><span data-ttu-id="37611-141">Typ</span><span class="sxs-lookup"><span data-stu-id="37611-141">Type</span></span>  

 <span data-ttu-id="37611-142">Typ danych: ciąg</span><span class="sxs-lookup"><span data-stu-id="37611-142">Data type: string</span></span>  
  
 <span data-ttu-id="37611-143">Typ dostępu: tylko do odczytu</span><span class="sxs-lookup"><span data-stu-id="37611-143">Access type: Read-only</span></span>  
  
 <span data-ttu-id="37611-144">Typ kontraktu.</span><span class="sxs-lookup"><span data-stu-id="37611-144">The type of the contract.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="37611-145">Wymagania</span><span class="sxs-lookup"><span data-stu-id="37611-145">Requirements</span></span>  
  
|<span data-ttu-id="37611-146">PLIK</span><span class="sxs-lookup"><span data-stu-id="37611-146">MOF</span></span>|<span data-ttu-id="37611-147">Zadeklarowany w ServiceModel. mof.</span><span class="sxs-lookup"><span data-stu-id="37611-147">Declared in Servicemodel.mof.</span></span>|  
|---------|-----------------------------------|  
|<span data-ttu-id="37611-148">Przestrzeń nazw</span><span class="sxs-lookup"><span data-stu-id="37611-148">Namespace</span></span>|<span data-ttu-id="37611-149">Zdefiniowane w root\ServiceModel</span><span class="sxs-lookup"><span data-stu-id="37611-149">Defined in root\ServiceModel</span></span>|  
  
## <a name="see-also"></a><span data-ttu-id="37611-150">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="37611-150">See also</span></span>

- <xref:System.ServiceModel.Description.ContractDescription>
