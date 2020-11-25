---
title: ICorProfilerCallback::RemotingClientReceivingReply — Metoda
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.RemotingClientReceivingReply
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::RemotingClientReceivingReply
helpviewer_keywords:
- ICorProfilerCallback::RemotingClientReceivingReply method [.NET Framework profiling]
- RemotingClientReceivingReply method [.NET Framework profiling]
ms.assetid: 15cfc300-8231-4ecb-9a04-19851c3eb484
topic_type:
- apiref
ms.openlocfilehash: 058c66af85da6c902e3d628e1b1479bb88c4fa85
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95704854"
---
# <a name="icorprofilercallbackremotingclientreceivingreply-method"></a><span data-ttu-id="3ecd8-102">ICorProfilerCallback::RemotingClientReceivingReply — Metoda</span><span class="sxs-lookup"><span data-stu-id="3ecd8-102">ICorProfilerCallback::RemotingClientReceivingReply Method</span></span>

<span data-ttu-id="3ecd8-103">Powiadamia program profilujący, że została ukończona część połączenia zdalnego po stronie serwera, a klient otrzymuje i informacje o przetwarzaniu odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="3ecd8-103">Notifies the profiler that the server-side portion of a remoting call has completed and the client is now receiving and about to process the reply.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="3ecd8-104">Składnia</span><span class="sxs-lookup"><span data-stu-id="3ecd8-104">Syntax</span></span>  
  
```cpp  
HRESULT RemotingClientReceivingReply(  
    [in] GUID *pCookie,  
    [in] BOOL fIsAsync);
```  
  
## <a name="parameters"></a><span data-ttu-id="3ecd8-105">Parametry</span><span class="sxs-lookup"><span data-stu-id="3ecd8-105">Parameters</span></span>  

 `pCookie`  
 <span data-ttu-id="3ecd8-106">podczas Wartość, która będzie odpowiadała wartości podanej w [ICorProfilerCallback:: RemotingServerSendingReply —](icorprofilercallback-remotingserversendingreply-method.md) w następujących warunkach:</span><span class="sxs-lookup"><span data-stu-id="3ecd8-106">[in] A value that will correspond with the value provided in [ICorProfilerCallback::RemotingServerSendingReply](icorprofilercallback-remotingserversendingreply-method.md) under these conditions:</span></span>  
  
- <span data-ttu-id="3ecd8-107">Pliki cookie identyfikatorów GUID usług zdalnych są aktywne.</span><span class="sxs-lookup"><span data-stu-id="3ecd8-107">Remoting GUID cookies are active.</span></span>  
  
- <span data-ttu-id="3ecd8-108">Kanał pomyślnie przesyła komunikat.</span><span class="sxs-lookup"><span data-stu-id="3ecd8-108">The channel succeeds in transmitting the message.</span></span>  
  
- <span data-ttu-id="3ecd8-109">Pliki cookie identyfikatorów GUID są aktywne w procesie po stronie serwera.</span><span class="sxs-lookup"><span data-stu-id="3ecd8-109">GUID cookies are active on the server-side process.</span></span>  
  
 <span data-ttu-id="3ecd8-110">Pozwala to na łatwe parowanie wywołań komunikacji zdalnej.</span><span class="sxs-lookup"><span data-stu-id="3ecd8-110">This allows easy pairing of remoting calls.</span></span>  
  
 `fIsAsync`  
 <span data-ttu-id="3ecd8-111">podczas Wartość, która jest, `true` Jeśli wywołanie jest asynchroniczne; w przeciwnym razie `false` .</span><span class="sxs-lookup"><span data-stu-id="3ecd8-111">[in] A value that is `true` if the call is asynchronous; otherwise, `false`.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="3ecd8-112">Wymagania</span><span class="sxs-lookup"><span data-stu-id="3ecd8-112">Requirements</span></span>  

 <span data-ttu-id="3ecd8-113">**Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="3ecd8-113">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="3ecd8-114">**Nagłówek:** CorProf. idl, CorProf. h</span><span class="sxs-lookup"><span data-stu-id="3ecd8-114">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="3ecd8-115">**Biblioteka:** CorGuids. lib</span><span class="sxs-lookup"><span data-stu-id="3ecd8-115">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="3ecd8-116">**.NET Framework wersje:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="3ecd8-116">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="3ecd8-117">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="3ecd8-117">See also</span></span>

- [<span data-ttu-id="3ecd8-118">ICorProfilerCallback — Interfejs</span><span class="sxs-lookup"><span data-stu-id="3ecd8-118">ICorProfilerCallback Interface</span></span>](icorprofilercallback-interface.md)
