---
title: ICorProfilerCallback::RemotingServerReceivingMessage — Metoda
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.RemotingServerReceivingMessage
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::RemotingServerReceivingMessage
helpviewer_keywords:
- ICorProfilerCallback::RemotingServerReceivingMessage method [.NET Framework profiling]
- RemotingServerReceivingMessage method [.NET Framework profiling]
ms.assetid: 5604d21f-e6b7-490e-b469-42122a7568e1
topic_type:
- apiref
ms.openlocfilehash: 0fc84a15d3250d5103c1dbc6486960f0ea780a2b
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95676819"
---
# <a name="icorprofilercallbackremotingserverreceivingmessage-method"></a><span data-ttu-id="5e5d1-102">ICorProfilerCallback::RemotingServerReceivingMessage — Metoda</span><span class="sxs-lookup"><span data-stu-id="5e5d1-102">ICorProfilerCallback::RemotingServerReceivingMessage Method</span></span>

<span data-ttu-id="5e5d1-103">Powiadamia program profilujący, że proces otrzymał zdalne wywołanie metody lub żądanie aktywacji.</span><span class="sxs-lookup"><span data-stu-id="5e5d1-103">Notifies the profiler that the process has received a remote method invocation or activation request.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="5e5d1-104">Składnia</span><span class="sxs-lookup"><span data-stu-id="5e5d1-104">Syntax</span></span>  
  
```cpp  
HRESULT RemotingClientSendingMessage(  
    [in] GUID *pCookie,  
    [in] BOOL fIsAsync);  
```  
  
## <a name="parameters"></a><span data-ttu-id="5e5d1-105">Parametry</span><span class="sxs-lookup"><span data-stu-id="5e5d1-105">Parameters</span></span>  

 `pCookie`  
 <span data-ttu-id="5e5d1-106">podczas Wartość, która będzie odpowiadała wartości podanej w [ICorProfilerCallback:: RemotingClientSendingMessage —](icorprofilercallback-remotingclientsendingmessage-method.md) w następujących warunkach:</span><span class="sxs-lookup"><span data-stu-id="5e5d1-106">[in] A value that will correspond with the value provided in [ICorProfilerCallback::RemotingClientSendingMessage](icorprofilercallback-remotingclientsendingmessage-method.md) under these conditions:</span></span>  
  
- <span data-ttu-id="5e5d1-107">Pliki cookie identyfikatorów GUID usług zdalnych są aktywne.</span><span class="sxs-lookup"><span data-stu-id="5e5d1-107">Remoting GUID cookies are active.</span></span>  
  
- <span data-ttu-id="5e5d1-108">Kanał pomyślnie przesyła komunikat.</span><span class="sxs-lookup"><span data-stu-id="5e5d1-108">The channel succeeds in transmitting the message.</span></span>  
  
- <span data-ttu-id="5e5d1-109">Pliki cookie identyfikatorów GUID są aktywne w procesie po stronie klienta.</span><span class="sxs-lookup"><span data-stu-id="5e5d1-109">GUID cookies are active on the client-side process.</span></span>  
  
 <span data-ttu-id="5e5d1-110">Pozwala to na łatwe parowanie wywołań zdalnych i Tworzenie stosu wywołań logicznych.</span><span class="sxs-lookup"><span data-stu-id="5e5d1-110">This allows easy pairing of remoting calls and the creation of a logical call stack.</span></span>  
  
 `fIsAsync`  
 <span data-ttu-id="5e5d1-111">podczas Wartość, która jest, `true` Jeśli wywołanie jest asynchroniczne; w przeciwnym razie `false` .</span><span class="sxs-lookup"><span data-stu-id="5e5d1-111">[in] A value that is `true` if the call is asynchronous; otherwise, `false`.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="5e5d1-112">Uwagi</span><span class="sxs-lookup"><span data-stu-id="5e5d1-112">Remarks</span></span>  

 <span data-ttu-id="5e5d1-113">Jeśli żądanie komunikatu jest asynchroniczne, żądanie może być serwisowane przez dowolny wątek.</span><span class="sxs-lookup"><span data-stu-id="5e5d1-113">If the message request is asynchronous, the request can be serviced by any arbitrary thread.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="5e5d1-114">Wymagania</span><span class="sxs-lookup"><span data-stu-id="5e5d1-114">Requirements</span></span>  

 <span data-ttu-id="5e5d1-115">**Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="5e5d1-115">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="5e5d1-116">**Nagłówek:** CorProf. idl, CorProf. h</span><span class="sxs-lookup"><span data-stu-id="5e5d1-116">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="5e5d1-117">**Biblioteka:** CorGuids. lib</span><span class="sxs-lookup"><span data-stu-id="5e5d1-117">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="5e5d1-118">**.NET Framework wersje:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="5e5d1-118">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="5e5d1-119">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="5e5d1-119">See also</span></span>

- [<span data-ttu-id="5e5d1-120">ICorProfilerCallback — Interfejs</span><span class="sxs-lookup"><span data-stu-id="5e5d1-120">ICorProfilerCallback Interface</span></span>](icorprofilercallback-interface.md)
