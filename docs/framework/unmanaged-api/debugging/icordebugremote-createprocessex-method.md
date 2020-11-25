---
title: ICorDebugRemote::CreateProcessEx — Metoda
ms.date: 03/30/2017
api_name:
- ICorDebugRemote.CreateProcessEx
api_location:
- CorDebug.dll
api_type:
- COM
f1_keywords:
- ICorDebugRemoteTarget::CreateProcessEx
helpviewer_keywords:
- CreateProcessEx method, ICorDebugRemote interface [.NET Framework debugging]
- ICorDebugRemote::CreateProcessEx method [.NET Framework debugging]
ms.assetid: 41af93c7-e448-4251-8d4d-413d38c635f2
topic_type:
- apiref
ms.openlocfilehash: 37bf800f27754d1bf80aece962b7cbb85b1cbedc
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95712186"
---
# <a name="icordebugremotecreateprocessex-method"></a><span data-ttu-id="15046-102">ICorDebugRemote::CreateProcessEx — Metoda</span><span class="sxs-lookup"><span data-stu-id="15046-102">ICorDebugRemote::CreateProcessEx Method</span></span>

<span data-ttu-id="15046-103">Uruchamia proces na maszynie zdalnej pod debugerem.</span><span class="sxs-lookup"><span data-stu-id="15046-103">Launches a process on a remote machine under the debugger.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="15046-104">Składnia</span><span class="sxs-lookup"><span data-stu-id="15046-104">Syntax</span></span>  
  
```cpp  
HRESULT CreateProcessEx (  
    [in]  ICorDebugRemoteTarget*      pRemoteTarget,  
    [in]  LPCWSTR                     lpApplicationName,  
    [in]  LPWSTR                      lpCommandLine,  
    [in]  LPSECURITY_ATTRIBUTES       lpProcessAttributes,  
    [in]  LPSECURITY_ATTRIBUTES       lpThreadAttributes,  
    [in]  BOOL                        bInheritHandles,  
    [in]  DWORD                       dwCreationFlags,  
    [in]  PVOID                       lpEnvironment,  
    [in]  LPCWSTR                     lpCurrentDirectory,  
    [in]  LPSTARTUPINFOW              lpStartupInfo,  
    [in]  LPPROCESS_INFORMATION       lpProcessInformation,  
    [in]  CorDebugCreateProcessFlags  debuggingFlags,  
    [out] ICorDebugProcess**          ppProcess  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="15046-105">Parametry</span><span class="sxs-lookup"><span data-stu-id="15046-105">Parameters</span></span>  

 `pRemoteTarget`  
 <span data-ttu-id="15046-106">podczas Wskaźnik do [interfejsu ICorDebugRemoteTarget](icordebugremotetarget-interface.md).</span><span class="sxs-lookup"><span data-stu-id="15046-106">[in] Pointer to an [ICorDebugRemoteTarget Interface](icordebugremotetarget-interface.md).</span></span> <span data-ttu-id="15046-107">Służy do określania komputera zdalnego, na którym zostanie uruchomiony proces.</span><span class="sxs-lookup"><span data-stu-id="15046-107">Used to determine the remote machine on which the process will be launched.</span></span>  
  
 `lpApplicationName`  
 <span data-ttu-id="15046-108">podczas Wskaźnik na ciąg zakończony znakiem null, który określa moduł, który ma zostać wykonany przez uruchomiony proces.</span><span class="sxs-lookup"><span data-stu-id="15046-108">[in] Pointer to a null-terminated string that specifies the module to be executed by the launched process.</span></span> <span data-ttu-id="15046-109">Moduł jest wykonywany w kontekście zabezpieczeń procesu wywołującego.</span><span class="sxs-lookup"><span data-stu-id="15046-109">The module is executed in the security context of the calling process.</span></span>  
  
 `lpCommandLine`  
 <span data-ttu-id="15046-110">podczas Wskaźnik na ciąg zakończony znakiem null, który określa wiersz polecenia, który ma zostać wykonany przez uruchomiony proces.</span><span class="sxs-lookup"><span data-stu-id="15046-110">[in] Pointer to a null-terminated string that specifies the command line to be executed by the launched process.</span></span>  
  
 `lpProcessAttributes`  
 <span data-ttu-id="15046-111">podczas Nieużywane na potrzeby debugowania zdalnego.</span><span class="sxs-lookup"><span data-stu-id="15046-111">[in] Unused for remote debugging.</span></span>  
  
 `lpThreadAttributes`  
 <span data-ttu-id="15046-112">podczas Nieużywane na potrzeby debugowania zdalnego.</span><span class="sxs-lookup"><span data-stu-id="15046-112">[in] Unused for remote debugging.</span></span>  
  
 `bInheritHandles`  
 <span data-ttu-id="15046-113">podczas Nieużywane na potrzeby debugowania zdalnego.</span><span class="sxs-lookup"><span data-stu-id="15046-113">[in] Unused for remote debugging.</span></span>  
  
 `dwCreationFlags`  
 <span data-ttu-id="15046-114">podczas Nieużywane na potrzeby debugowania zdalnego.</span><span class="sxs-lookup"><span data-stu-id="15046-114">[in] Unused for remote debugging.</span></span>  
  
 `lpEnvironment`  
 <span data-ttu-id="15046-115">podczas Wskaźnik do bloku środowiska dla nowego procesu.</span><span class="sxs-lookup"><span data-stu-id="15046-115">[in] Pointer to an environment block for the new process.</span></span>  
  
 `lpCurrentDirectory`  
 <span data-ttu-id="15046-116">podczas Wskaźnik na ciąg zakończony znakiem null, który określa pełną ścieżkę do bieżącego katalogu dla procesu.</span><span class="sxs-lookup"><span data-stu-id="15046-116">[in] Pointer to a null-terminated string that specifies the full path to the current directory for the process.</span></span> <span data-ttu-id="15046-117">Jeśli ten parametr ma wartość null, nowy proces będzie miał ten sam bieżący dysk i katalog co proces wywołujący.</span><span class="sxs-lookup"><span data-stu-id="15046-117">If this parameter is null, the new process will have the same current drive and directory as the calling process.</span></span>  
  
 `lpStartupInfo`  
 <span data-ttu-id="15046-118">podczas Nieużywane na potrzeby debugowania zdalnego.</span><span class="sxs-lookup"><span data-stu-id="15046-118">[in] Unused for remote debugging.</span></span>  
  
 `lpProcessInformation`  
 <span data-ttu-id="15046-119">podczas Nieużywane na potrzeby debugowania zdalnego.</span><span class="sxs-lookup"><span data-stu-id="15046-119">[in] Unused for remote debugging.</span></span>  
  
 `debuggingFlags`  
 <span data-ttu-id="15046-120">podczas Nieużywane na potrzeby debugowania zdalnego.</span><span class="sxs-lookup"><span data-stu-id="15046-120">[in] Unused for remote debugging.</span></span>  
  
 `ppProcess`  
 <span data-ttu-id="15046-121">określoną Wskaźnik do adresu obiektu "ICorDebugProcess Interface", który reprezentuje proces.</span><span class="sxs-lookup"><span data-stu-id="15046-121">[out] A pointer to the address of a"ICorDebugProcess Interface" object that represents the process.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="15046-122">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="15046-122">Return Value</span></span>  

 <span data-ttu-id="15046-123">S_OK</span><span class="sxs-lookup"><span data-stu-id="15046-123">S_OK</span></span>  
 <span data-ttu-id="15046-124">Pomyślnie uruchomiono proces na maszynie zdalnej i zwróciło "interfejs ICorDebugProcess" do debugowania.</span><span class="sxs-lookup"><span data-stu-id="15046-124">Successfully launched the process on the remote machine and returned an "ICorDebugProcess Interface" for debugging.</span></span>  
  
 <span data-ttu-id="15046-125">E_FAIL (lub inne kody powrotne E_)</span><span class="sxs-lookup"><span data-stu-id="15046-125">E_FAIL (or other E_ return codes)</span></span>  
 <span data-ttu-id="15046-126">Nie można uruchomić procesu na maszynie zdalnej i zwrócić "ICorDebugProcess Interface" w celu debugowania.</span><span class="sxs-lookup"><span data-stu-id="15046-126">Unable to launch the process on the remote machine and return an "ICorDebugProcess Interface" for debugging.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="15046-127">Uwagi</span><span class="sxs-lookup"><span data-stu-id="15046-127">Remarks</span></span>  

 <span data-ttu-id="15046-128">Debugowanie w trybie mieszanym nie jest obsługiwane w programie Silverlight.</span><span class="sxs-lookup"><span data-stu-id="15046-128">Mixed-mode debugging is not supported in Silverlight.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="15046-129">Wymagania</span><span class="sxs-lookup"><span data-stu-id="15046-129">Requirements</span></span>  

 <span data-ttu-id="15046-130">**Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="15046-130">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="15046-131">**Nagłówek:** CorDebug. idl</span><span class="sxs-lookup"><span data-stu-id="15046-131">**Header:** CorDebug.idl</span></span>  
  
 <span data-ttu-id="15046-132">**Biblioteka:** CorGuids. lib</span><span class="sxs-lookup"><span data-stu-id="15046-132">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="15046-133">**.NET Framework wersje:** 4,5, 4, 3,5 SP1</span><span class="sxs-lookup"><span data-stu-id="15046-133">**.NET Framework Versions:** 4.5, 4, 3.5 SP1</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="15046-134">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="15046-134">See also</span></span>

- [<span data-ttu-id="15046-135">ICorDebugRemote — Interfejs</span><span class="sxs-lookup"><span data-stu-id="15046-135">ICorDebugRemote Interface</span></span>](icordebugremote-interface.md)
- [<span data-ttu-id="15046-136">ICorDebug — Interfejs</span><span class="sxs-lookup"><span data-stu-id="15046-136">ICorDebug Interface</span></span>](icordebug-interface.md)

- [<span data-ttu-id="15046-137">Debugowanie — Interfejsy</span><span class="sxs-lookup"><span data-stu-id="15046-137">Debugging Interfaces</span></span>](debugging-interfaces.md)
