---
title: ICorProfilerInfo3::GetModuleInfo2 — Metoda
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo3.GetModuleInfo2
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo3::GetModuleInfo2
helpviewer_keywords:
- ICorProfilerInfo3::GetModuleInfo2 method [.NET Framework profiling]
- GetModuleInfo2 method [.NET Framework profiling]
ms.assetid: f1f6b8f3-dcfc-49e8-be76-ea50ea90d5a7
topic_type:
- apiref
ms.openlocfilehash: 2213b674cce27c77156b8de1bbf20d2975e3e55c
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95721598"
---
# <a name="icorprofilerinfo3getmoduleinfo2-method"></a><span data-ttu-id="42b3b-102">ICorProfilerInfo3::GetModuleInfo2 — Metoda</span><span class="sxs-lookup"><span data-stu-id="42b3b-102">ICorProfilerInfo3::GetModuleInfo2 Method</span></span>

<span data-ttu-id="42b3b-103">Podano identyfikator modułu, zwraca nazwę pliku modułu, identyfikator zestawu nadrzędnego modułu i maskę bitów opisującą właściwości modułu.</span><span class="sxs-lookup"><span data-stu-id="42b3b-103">Given a module ID, returns the file name of the module, the ID of the module's parent assembly, and a bitmask that describes the properties of the module.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="42b3b-104">Składnia</span><span class="sxs-lookup"><span data-stu-id="42b3b-104">Syntax</span></span>  
  
```cpp  
HRESULT GetModuleInfo2(  
    [in]  ModuleID   moduleId,  
    [out] LPCBYTE    *ppBaseLoadAddress,  
    [in]  ULONG      cchName,  
    [out] ULONG      *pcchName,  
    [out, annotation("__out_ecount_part(cchName, *pcchName)")]  
          WCHAR      szName[] ,  
    [out] AssemblyID *pAssemblyId);  
    [out] DWORD                 *pdwModuleFlags);  
```  
  
## <a name="parameters"></a><span data-ttu-id="42b3b-105">Parametry</span><span class="sxs-lookup"><span data-stu-id="42b3b-105">Parameters</span></span>  

 `moduleId`  
 <span data-ttu-id="42b3b-106">podczas Identyfikator modułu, dla którego będą pobierane informacje.</span><span class="sxs-lookup"><span data-stu-id="42b3b-106">[in] The ID of the module for which information will be retrieved.</span></span>  
  
 `ppBaseLoadAddress`  
 <span data-ttu-id="42b3b-107">określoną Adres podstawowy, z którego moduł jest załadowany.</span><span class="sxs-lookup"><span data-stu-id="42b3b-107">[out] The base address at which the module is loaded.</span></span>  
  
 `cchName`  
 <span data-ttu-id="42b3b-108">podczas Długość (w znakach) `szName` buforu powrotu.</span><span class="sxs-lookup"><span data-stu-id="42b3b-108">[in] The length, in characters, of the `szName` return buffer.</span></span>  
  
 `pcchName`  
 <span data-ttu-id="42b3b-109">określoną Wskaźnik do łącznej długości znaku nazwy pliku modułu, który jest zwracany.</span><span class="sxs-lookup"><span data-stu-id="42b3b-109">[out] A pointer to the total character length of the module's file name that is returned.</span></span>  
  
 `szName`  
 <span data-ttu-id="42b3b-110">określoną Bufor znaków udostępniany przez obiekt wywołujący.</span><span class="sxs-lookup"><span data-stu-id="42b3b-110">[out] A caller-provided wide character buffer.</span></span> <span data-ttu-id="42b3b-111">Gdy metoda zwraca, ten bufor zawiera nazwę pliku modułu.</span><span class="sxs-lookup"><span data-stu-id="42b3b-111">When the method returns, this buffer contains the file name of the module.</span></span>  
  
 `pAssemblyId`  
 <span data-ttu-id="42b3b-112">określoną Wskaźnik do identyfikatora zestawu nadrzędnego modułu.</span><span class="sxs-lookup"><span data-stu-id="42b3b-112">[out] A pointer to the ID of the module's parent assembly.</span></span>  
  
 `pdwModuleFlags`  
 <span data-ttu-id="42b3b-113">określoną Maska bitów wartości z wyliczenia [COR_PRF_MODULE_FLAGS](cor-prf-module-flags-enumeration.md) , która określa właściwości modułu.</span><span class="sxs-lookup"><span data-stu-id="42b3b-113">[out] A bitmask of values from the [COR_PRF_MODULE_FLAGS](cor-prf-module-flags-enumeration.md) enumeration that specify the properties of the module.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="42b3b-114">Uwagi</span><span class="sxs-lookup"><span data-stu-id="42b3b-114">Remarks</span></span>  

 <span data-ttu-id="42b3b-115">Dla modułów dynamicznych `szName` parametr jest nazwą metadanych modułu, a adres podstawowy to 0 (zero).</span><span class="sxs-lookup"><span data-stu-id="42b3b-115">For dynamic modules, the `szName` parameter is the metadata name of the module, and the base address is 0 (zero).</span></span> <span data-ttu-id="42b3b-116">Nazwa metadanych jest wartością w kolumnie Nazwa z tabeli modułu w metadanych.</span><span class="sxs-lookup"><span data-stu-id="42b3b-116">The metadata name is the value in the Name column from the Module table inside metadata.</span></span> <span data-ttu-id="42b3b-117">Jest to również uwidocznione jako <xref:System.Reflection.Module.ScopeName%2A?displayProperty=nameWithType> Właściwość do kodu zarządzanego, a jako `szName` parametr metody [IMetaDataImport:: GetScopeProps —](../metadata/imetadataimport-getscopeprops-method.md) do niezarządzanego kodu klienta metadanych.</span><span class="sxs-lookup"><span data-stu-id="42b3b-117">This is also exposed as the <xref:System.Reflection.Module.ScopeName%2A?displayProperty=nameWithType> property to managed code, and as the `szName` parameter of the [IMetaDataImport::GetScopeProps](../metadata/imetadataimport-getscopeprops-method.md) method to unmanaged metadata client code.</span></span>  
  
 <span data-ttu-id="42b3b-118">Mimo że `GetModuleInfo2` Metoda może być wywoływana, gdy tylko identyfikator modułu już istnieje, identyfikator zestawu nadrzędnego nie będzie dostępny do momentu otrzymania przez profiler wywołania zwrotnego [ICorProfilerCallback:: ModuleAttachedToAssembly —](icorprofilercallback-moduleattachedtoassembly-method.md) .</span><span class="sxs-lookup"><span data-stu-id="42b3b-118">Although the `GetModuleInfo2` method may be called as soon as the module's ID exists, the ID of the parent assembly will not be available until the profiler receives the [ICorProfilerCallback::ModuleAttachedToAssembly](icorprofilercallback-moduleattachedtoassembly-method.md) callback.</span></span>  
  
 <span data-ttu-id="42b3b-119">Gdy `GetModuleInfo2` zwraca, należy sprawdzić, czy `szName` bufor jest wystarczająco duży, aby można było zawierać pełną nazwę pliku modułu.</span><span class="sxs-lookup"><span data-stu-id="42b3b-119">When `GetModuleInfo2` returns, you must verify that the `szName` buffer was large enough to contain the full file name of the module.</span></span> <span data-ttu-id="42b3b-120">W tym celu należy porównać wartość wskazującą wartość `pcchName` `cchName` parametru.</span><span class="sxs-lookup"><span data-stu-id="42b3b-120">To do this, compare the value that `pcchName` points to with the value of the `cchName` parameter.</span></span> <span data-ttu-id="42b3b-121">Jeśli `pcchName` wskazuje wartość, która jest większa niż `cchName` , Przydziel większy `szName` bufor, zaktualizuj `cchName` przy użyciu nowego, większego rozmiaru i ponownie wywołaj `GetModuleInfo2` .</span><span class="sxs-lookup"><span data-stu-id="42b3b-121">If `pcchName` points to a value that is larger than `cchName`, allocate a larger `szName` buffer, update `cchName` with the new, larger size, and call `GetModuleInfo2` again.</span></span>  
  
 <span data-ttu-id="42b3b-122">Alternatywnie, można najpierw wywołać `GetModuleInfo2` z buforem o zerowej długości, `szName` Aby uzyskać prawidłowy rozmiar buforu.</span><span class="sxs-lookup"><span data-stu-id="42b3b-122">Alternatively, you can first call `GetModuleInfo2` with a zero-length `szName` buffer to obtain the correct buffer size.</span></span> <span data-ttu-id="42b3b-123">Następnie można ustawić rozmiar buforu na wartość zwracaną w `pcchName` i `GetModuleInfo2` ponownie wywołać.</span><span class="sxs-lookup"><span data-stu-id="42b3b-123">You can then set the buffer size to the value returned in `pcchName` and call `GetModuleInfo2` again.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="42b3b-124">Wymagania</span><span class="sxs-lookup"><span data-stu-id="42b3b-124">Requirements</span></span>  

 <span data-ttu-id="42b3b-125">**Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="42b3b-125">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="42b3b-126">**Nagłówek:** CorProf. idl, CorProf. h</span><span class="sxs-lookup"><span data-stu-id="42b3b-126">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="42b3b-127">**Biblioteka:** CorGuids. lib</span><span class="sxs-lookup"><span data-stu-id="42b3b-127">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="42b3b-128">**.NET Framework wersje:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="42b3b-128">**.NET Framework Versions:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="42b3b-129">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="42b3b-129">See also</span></span>

- [<span data-ttu-id="42b3b-130">ICorProfilerInfo — Interfejs</span><span class="sxs-lookup"><span data-stu-id="42b3b-130">ICorProfilerInfo Interface</span></span>](icorprofilerinfo-interface.md)
- [<span data-ttu-id="42b3b-131">Interfejsy profilowania</span><span class="sxs-lookup"><span data-stu-id="42b3b-131">Profiling Interfaces</span></span>](profiling-interfaces.md)
- [<span data-ttu-id="42b3b-132">Profilowanie</span><span class="sxs-lookup"><span data-stu-id="42b3b-132">Profiling</span></span>](index.md)
