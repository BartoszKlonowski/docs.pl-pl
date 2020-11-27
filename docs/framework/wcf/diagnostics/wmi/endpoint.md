---
title: Punkt końcowy
ms.date: 03/30/2017
ms.assetid: fe63370d-81a1-40f3-97c2-59cb357c78d2
ms.openlocfilehash: ceb4e4b41502b00d7bb21f1ecbd8249fccf1ce3b
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96288817"
---
# <a name="endpoint"></a><span data-ttu-id="c81af-102">Punkt końcowy</span><span class="sxs-lookup"><span data-stu-id="c81af-102">Endpoint</span></span>

<span data-ttu-id="c81af-103">Punkt końcowy</span><span class="sxs-lookup"><span data-stu-id="c81af-103">Endpoint</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="c81af-104">Składnia</span><span class="sxs-lookup"><span data-stu-id="c81af-104">Syntax</span></span>  
  
```csharp
class Endpoint  
{  
  string Address;  
  string AddressHeaders[];  
  string AddressIdentity;  
  sint32 AppDomainId;  
  Behavior Behaviors[];  
  Binding Binding;  
  string ContractName;  
  string CounterInstanceName;  
  string ListenUri;  
  string Name;  
  sint32 ProcessId;  
  Contract ref;  
};  
```  
  
## <a name="methods"></a><span data-ttu-id="c81af-105">Metody</span><span class="sxs-lookup"><span data-stu-id="c81af-105">Methods</span></span>  

 <span data-ttu-id="c81af-106">Klasa Endpoint definiuje następującą metodę.</span><span class="sxs-lookup"><span data-stu-id="c81af-106">The Endpoint class defines the following method.</span></span>  
  
|<span data-ttu-id="c81af-107">Metoda</span><span class="sxs-lookup"><span data-stu-id="c81af-107">Method</span></span>|<span data-ttu-id="c81af-108">Opis</span><span class="sxs-lookup"><span data-stu-id="c81af-108">Description</span></span>|  
|------------|-----------------|  
|[<span data-ttu-id="c81af-109">GetOperationCounterInstanceName</span><span class="sxs-lookup"><span data-stu-id="c81af-109">GetOperationCounterInstanceName</span></span>](getoperationcounterinstancename.md)|<span data-ttu-id="c81af-110">Pobiera nazwę wystąpienia licznika wydajności operacji</span><span class="sxs-lookup"><span data-stu-id="c81af-110">Retrieves the operation performance counter instance name</span></span>|  
  
## <a name="properties"></a><span data-ttu-id="c81af-111">Właściwości</span><span class="sxs-lookup"><span data-stu-id="c81af-111">Properties</span></span>  

 <span data-ttu-id="c81af-112">Klasa punktu końcowego ma następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="c81af-112">The Endpoint class has the following properties:</span></span>  
  
### <a name="address"></a><span data-ttu-id="c81af-113">Adres</span><span class="sxs-lookup"><span data-stu-id="c81af-113">Address</span></span>  

 <span data-ttu-id="c81af-114">Typ danych: ciąg</span><span class="sxs-lookup"><span data-stu-id="c81af-114">Data type: string</span></span>  
  
 <span data-ttu-id="c81af-115">Typ dostępu: tylko do odczytu</span><span class="sxs-lookup"><span data-stu-id="c81af-115">Access type: Read-only</span></span>  
  
 <span data-ttu-id="c81af-116">Identyfikator URI zawierający adres punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="c81af-116">A URI that contains the address of the endpoint.</span></span>  
  
### <a name="addressheaders"></a><span data-ttu-id="c81af-117">AddressHeaders</span><span class="sxs-lookup"><span data-stu-id="c81af-117">AddressHeaders</span></span>  

 <span data-ttu-id="c81af-118">Typ danych: tablica ciągów</span><span class="sxs-lookup"><span data-stu-id="c81af-118">Data type: string array</span></span>  
  
 <span data-ttu-id="c81af-119">Typ dostępu: tylko do odczytu</span><span class="sxs-lookup"><span data-stu-id="c81af-119">Access type: Read-only</span></span>  
  
 <span data-ttu-id="c81af-120">Kolekcja nagłówków adresów dołączonych do tego punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="c81af-120">The collection of address headers attached to this endpoint.</span></span>  
  
### <a name="addressidentity"></a><span data-ttu-id="c81af-121">AddressIdentity</span><span class="sxs-lookup"><span data-stu-id="c81af-121">AddressIdentity</span></span>  

 <span data-ttu-id="c81af-122">Typ danych: ciąg</span><span class="sxs-lookup"><span data-stu-id="c81af-122">Data type: string</span></span>  
  
 <span data-ttu-id="c81af-123">Typ dostępu: tylko do odczytu</span><span class="sxs-lookup"><span data-stu-id="c81af-123">Access type: Read-only</span></span>  
  
 <span data-ttu-id="c81af-124">Tożsamość punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="c81af-124">The identity of the endpoint.</span></span>  
  
### <a name="appdomainid"></a><span data-ttu-id="c81af-125">AppDomainId</span><span class="sxs-lookup"><span data-stu-id="c81af-125">AppDomainId</span></span>  

 <span data-ttu-id="c81af-126">Typ danych: sint32</span><span class="sxs-lookup"><span data-stu-id="c81af-126">Data type: sint32</span></span>  
  
 <span data-ttu-id="c81af-127">Typ dostępu: tylko do odczytu</span><span class="sxs-lookup"><span data-stu-id="c81af-127">Access type: Read-only</span></span>  
  
 <span data-ttu-id="c81af-128">Identyfikator domeny aplikacji, która hostuje punkt końcowy.</span><span class="sxs-lookup"><span data-stu-id="c81af-128">The appdomain id of the appdomain that hosts the endpoint.</span></span>  
  
### <a name="behaviors"></a><span data-ttu-id="c81af-129">Zachowania</span><span class="sxs-lookup"><span data-stu-id="c81af-129">Behaviors</span></span>  

 <span data-ttu-id="c81af-130">Typ danych: tablica zachowań</span><span class="sxs-lookup"><span data-stu-id="c81af-130">Data type: Behavior array</span></span>  
  
 <span data-ttu-id="c81af-131">Typ dostępu: tylko do odczytu</span><span class="sxs-lookup"><span data-stu-id="c81af-131">Access type: Read-only</span></span>  
  
 <span data-ttu-id="c81af-132">Kolekcja zachowań implementowanych przez ten punkt końcowy.</span><span class="sxs-lookup"><span data-stu-id="c81af-132">The collection of behaviors implemented by this endpoint.</span></span>  
  
### <a name="binding"></a><span data-ttu-id="c81af-133">Wiązanie</span><span class="sxs-lookup"><span data-stu-id="c81af-133">Binding</span></span>  

 <span data-ttu-id="c81af-134">Typ danych: powiązanie</span><span class="sxs-lookup"><span data-stu-id="c81af-134">Data type: Binding</span></span>  
  
 <span data-ttu-id="c81af-135">Typ dostępu: tylko do odczytu</span><span class="sxs-lookup"><span data-stu-id="c81af-135">Access type: Read-only</span></span>  
  
 <span data-ttu-id="c81af-136">Powiązanie używane przez ten punkt końcowy.</span><span class="sxs-lookup"><span data-stu-id="c81af-136">The binding used by this endpoint.</span></span>  
  
### <a name="contractname"></a><span data-ttu-id="c81af-137">Nr kontraktu</span><span class="sxs-lookup"><span data-stu-id="c81af-137">ContractName</span></span>  

 <span data-ttu-id="c81af-138">Typ danych: ciąg</span><span class="sxs-lookup"><span data-stu-id="c81af-138">Data type: string</span></span>  
  
 <span data-ttu-id="c81af-139">Typ dostępu: tylko do odczytu</span><span class="sxs-lookup"><span data-stu-id="c81af-139">Access type: Read-only</span></span>  
  
 <span data-ttu-id="c81af-140">Ciąg określający, który kontrakt jest ujawniany przez ten punkt końcowy.</span><span class="sxs-lookup"><span data-stu-id="c81af-140">A string that specifies which contract this endpoint is exposing.</span></span>  
  
### <a name="counterinstancename"></a><span data-ttu-id="c81af-141">CounterInstanceName</span><span class="sxs-lookup"><span data-stu-id="c81af-141">CounterInstanceName</span></span>  

 <span data-ttu-id="c81af-142">Typ danych: ciąg</span><span class="sxs-lookup"><span data-stu-id="c81af-142">Data type: string</span></span>  
  
 <span data-ttu-id="c81af-143">Typ dostępu: tylko do odczytu</span><span class="sxs-lookup"><span data-stu-id="c81af-143">Access type: Read-only</span></span>  
  
 <span data-ttu-id="c81af-144">Nazwa wystąpienia liczników wydajności punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="c81af-144">The name of the instance of performance counters of the endpoint.</span></span>  
  
### <a name="listenuri"></a><span data-ttu-id="c81af-145">ListenUri o wartości</span><span class="sxs-lookup"><span data-stu-id="c81af-145">ListenUri</span></span>  

 <span data-ttu-id="c81af-146">Typ danych: ciąg</span><span class="sxs-lookup"><span data-stu-id="c81af-146">Data type: string</span></span>  
  
 <span data-ttu-id="c81af-147">Typ dostępu: tylko do odczytu</span><span class="sxs-lookup"><span data-stu-id="c81af-147">Access type: Read-only</span></span>  
  
 <span data-ttu-id="c81af-148">Identyfikator URI, na którym nasłuchuje punkt końcowy.</span><span class="sxs-lookup"><span data-stu-id="c81af-148">The Uri the endpoint listens on.</span></span>  
  
### <a name="name"></a><span data-ttu-id="c81af-149">Nazwa</span><span class="sxs-lookup"><span data-stu-id="c81af-149">Name</span></span>  

 <span data-ttu-id="c81af-150">Typ danych: ciąg</span><span class="sxs-lookup"><span data-stu-id="c81af-150">Data type: string</span></span>  
  
 <span data-ttu-id="c81af-151">Typ dostępu: tylko do odczytu</span><span class="sxs-lookup"><span data-stu-id="c81af-151">Access type: Read-only</span></span>  
  
 <span data-ttu-id="c81af-152">Unikatowa nazwa tego punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="c81af-152">The unique name of this endpoint.</span></span>  
  
### <a name="processid"></a><span data-ttu-id="c81af-153">Identyfikator procesu</span><span class="sxs-lookup"><span data-stu-id="c81af-153">ProcessId</span></span>  

 <span data-ttu-id="c81af-154">Typ danych: sint32</span><span class="sxs-lookup"><span data-stu-id="c81af-154">Data type: sint32</span></span>  
  
 <span data-ttu-id="c81af-155">Typ dostępu: tylko do odczytu</span><span class="sxs-lookup"><span data-stu-id="c81af-155">Access type: Read-only</span></span>  
  
 <span data-ttu-id="c81af-156">Identyfikator procesu, który hostuje punkt końcowy.</span><span class="sxs-lookup"><span data-stu-id="c81af-156">The process Id of the process that hosts the endpoint.</span></span>  
  
### <a name="ref"></a><span data-ttu-id="c81af-157">ref</span><span class="sxs-lookup"><span data-stu-id="c81af-157">ref</span></span>  

 <span data-ttu-id="c81af-158">Typ danych: kontrakt</span><span class="sxs-lookup"><span data-stu-id="c81af-158">Data type: Contract</span></span>  
  
 <span data-ttu-id="c81af-159">Typ dostępu: tylko do odczytu</span><span class="sxs-lookup"><span data-stu-id="c81af-159">Access type: Read-only</span></span>  
  
 <span data-ttu-id="c81af-160">Kontrakt ujawniany przez ten punkt końcowy.</span><span class="sxs-lookup"><span data-stu-id="c81af-160">The contract this endpoint is exposing.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="c81af-161">Wymagania</span><span class="sxs-lookup"><span data-stu-id="c81af-161">Requirements</span></span>  
  
|<span data-ttu-id="c81af-162">PLIK</span><span class="sxs-lookup"><span data-stu-id="c81af-162">MOF</span></span>|<span data-ttu-id="c81af-163">Zadeklarowany w ServiceModel. mof.</span><span class="sxs-lookup"><span data-stu-id="c81af-163">Declared in Servicemodel.mof.</span></span>|  
|---------|-----------------------------------|  
|<span data-ttu-id="c81af-164">Przestrzeń nazw</span><span class="sxs-lookup"><span data-stu-id="c81af-164">Namespace</span></span>|<span data-ttu-id="c81af-165">Zdefiniowane w root\ServiceModel</span><span class="sxs-lookup"><span data-stu-id="c81af-165">Defined in root\ServiceModel</span></span>|
