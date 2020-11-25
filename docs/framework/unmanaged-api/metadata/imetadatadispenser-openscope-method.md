---
title: IMetaDataDispenser::OpenScope — Metoda
ms.date: 03/30/2017
api_name:
- IMetaDataDispenser.OpenScope
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataDispenser::OpenScope
helpviewer_keywords:
- IMetaDataDispenser::OpenScope method [.NET Framework metadata]
- OpenScope method, IMetaDataDispenser interface [.NET Framework metadata]
ms.assetid: 65063ad5-e0d9-4c01-8f8b-9a5950109fa6
topic_type:
- apiref
ms.openlocfilehash: f2a85bafc3e2f25b2ed6116a46a9938d869dbaae
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95726083"
---
# <a name="imetadatadispenseropenscope-method"></a><span data-ttu-id="55cca-102">IMetaDataDispenser::OpenScope — Metoda</span><span class="sxs-lookup"><span data-stu-id="55cca-102">IMetaDataDispenser::OpenScope Method</span></span>

<span data-ttu-id="55cca-103">Otwiera istniejący plik na dysku i mapuje jego metadane do pamięci.</span><span class="sxs-lookup"><span data-stu-id="55cca-103">Opens an existing, on-disk file and maps its metadata into memory.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="55cca-104">Składnia</span><span class="sxs-lookup"><span data-stu-id="55cca-104">Syntax</span></span>  
  
```cpp  
HRESULT OpenScope (  
    [in]  LPCWSTR     szScope,
    [in]  DWORD       dwOpenFlags,
    [in]  REFIID      riid,
    [out] IUnknown    **ppIUnk  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="55cca-105">Parametry</span><span class="sxs-lookup"><span data-stu-id="55cca-105">Parameters</span></span>  

 `szScope`  
 <span data-ttu-id="55cca-106">podczas Nazwa pliku, który ma zostać otwarty.</span><span class="sxs-lookup"><span data-stu-id="55cca-106">[in] The name of the file to be opened.</span></span> <span data-ttu-id="55cca-107">Plik musi zawierać metadane środowiska uruchomieniowego języka wspólnego (CLR).</span><span class="sxs-lookup"><span data-stu-id="55cca-107">The file must contain common language runtime (CLR) metadata.</span></span>  
  
 `dwOpenFlags`  
 <span data-ttu-id="55cca-108">podczas Wartość wyliczenia [CorOpenFlags —](coropenflags-enumeration.md) w celu określenia trybu (odczyt, zapis itd.) do otwarcia.</span><span class="sxs-lookup"><span data-stu-id="55cca-108">[in] A value of the [CorOpenFlags](coropenflags-enumeration.md) enumeration to specify the mode (read, write, and so on) for opening.</span></span>  
  
 `riid`  
 <span data-ttu-id="55cca-109">podczas Identyfikator IID żądanego interfejsu metadanych do zwrócenia; Obiekt wywołujący będzie używać interfejsu do importowania metadanych (odczytu) lub emisji (zapisu).</span><span class="sxs-lookup"><span data-stu-id="55cca-109">[in] The IID of the desired metadata interface to be returned; the caller will use the interface to import (read) or emit (write) metadata.</span></span>  
  
 <span data-ttu-id="55cca-110">Wartość `riid` musi określać jeden z interfejsów "Import" lub "Emituj".</span><span class="sxs-lookup"><span data-stu-id="55cca-110">The value of `riid` must specify one of the "import" or "emit" interfaces.</span></span> <span data-ttu-id="55cca-111">Prawidłowe wartości to IID_IMetaDataEmit, IID_IMetaDataImport, IID_IMetaDataAssemblyEmit, IID_IMetaDataAssemblyImport, IID_IMetaDataEmit2 lub IID_IMetaDataImport2.</span><span class="sxs-lookup"><span data-stu-id="55cca-111">Valid values are IID_IMetaDataEmit, IID_IMetaDataImport, IID_IMetaDataAssemblyEmit, IID_IMetaDataAssemblyImport, IID_IMetaDataEmit2, or IID_IMetaDataImport2.</span></span>  
  
 `ppIUnk`  
 <span data-ttu-id="55cca-112">określoną Wskaźnik do zwracanego interfejsu.</span><span class="sxs-lookup"><span data-stu-id="55cca-112">[out] The pointer to the returned interface.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="55cca-113">Uwagi</span><span class="sxs-lookup"><span data-stu-id="55cca-113">Remarks</span></span>  

 <span data-ttu-id="55cca-114">Kopię metadanych w pamięci można zbadać przy użyciu metod z jednego z interfejsów "Import" lub dodać do metod przy użyciu metody z jednego z interfejsów "Emituj".</span><span class="sxs-lookup"><span data-stu-id="55cca-114">The in-memory copy of the metadata can be queried using methods from one of the "import" interfaces, or added to using methods from the one of the "emit" interfaces.</span></span>  
  
 <span data-ttu-id="55cca-115">Jeśli plik docelowy nie zawiera metadanych CLR, `OpenScope` Metoda zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="55cca-115">If the target file does not contain CLR metadata, the `OpenScope` method will fail.</span></span>  
  
 <span data-ttu-id="55cca-116">W .NET Framework w wersji 1,0 i 1,1, jeśli zakres jest otwarty z `dwOpenFlags` ustawionym na ofRead, kwalifikuje się do udostępniania.</span><span class="sxs-lookup"><span data-stu-id="55cca-116">In the .NET Framework version 1.0 and version 1.1, if a scope is opened with `dwOpenFlags` set to ofRead, it is eligible for sharing.</span></span> <span data-ttu-id="55cca-117">Oznacza to, że jeśli kolejne wywołania `OpenScope` przekazane do nazwy pliku, który został wcześniej otwarty, istniejący zakres jest ponownie używany i nie zostanie utworzony nowy zestaw struktur danych.</span><span class="sxs-lookup"><span data-stu-id="55cca-117">That is, if subsequent calls to `OpenScope` pass in the name of a file that was previously opened, the existing scope is reused and a new set of data structures is not created.</span></span> <span data-ttu-id="55cca-118">Problemy mogą jednak wystąpić z powodu tego udostępniania.</span><span class="sxs-lookup"><span data-stu-id="55cca-118">However, problems can arise due to this sharing.</span></span>  
  
 <span data-ttu-id="55cca-119">W .NET Framework w wersji 2,0 zakresy otwarte z `dwOpenFlags` ustawionym na ofRead nie są już udostępniane.</span><span class="sxs-lookup"><span data-stu-id="55cca-119">In the .NET Framework version 2.0, scopes opened with `dwOpenFlags` set to ofRead are no longer shared.</span></span> <span data-ttu-id="55cca-120">Użyj wartości ofReadOnly, aby zezwolić na udostępnianie zakresu.</span><span class="sxs-lookup"><span data-stu-id="55cca-120">Use the ofReadOnly value to allow the scope to be shared.</span></span> <span data-ttu-id="55cca-121">Po udostępnieniu zakresu zapytania, które używają interfejsów metadanych "Odczyt/zapis", zakończą się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="55cca-121">When a scope is shared, queries that use "read/write" metadata interfaces will fail.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="55cca-122">Wymagania</span><span class="sxs-lookup"><span data-stu-id="55cca-122">Requirements</span></span>  

 <span data-ttu-id="55cca-123">**Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="55cca-123">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="55cca-124">**Nagłówek:** Cor. h</span><span class="sxs-lookup"><span data-stu-id="55cca-124">**Header:** Cor.h</span></span>  
  
 <span data-ttu-id="55cca-125">**Biblioteka:** Używane jako zasób w MsCorEE.dll</span><span class="sxs-lookup"><span data-stu-id="55cca-125">**Library:** Used as a resource in MsCorEE.dll</span></span>  
  
 <span data-ttu-id="55cca-126">**.NET Framework wersje:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="55cca-126">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="55cca-127">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="55cca-127">See also</span></span>

- [<span data-ttu-id="55cca-128">IMetaDataDispenser — Interfejs</span><span class="sxs-lookup"><span data-stu-id="55cca-128">IMetaDataDispenser Interface</span></span>](imetadatadispenser-interface.md)
- [<span data-ttu-id="55cca-129">IMetaDataDispenserEx — Interfejs</span><span class="sxs-lookup"><span data-stu-id="55cca-129">IMetaDataDispenserEx Interface</span></span>](imetadatadispenserex-interface.md)
- [<span data-ttu-id="55cca-130">IMetaDataAssemblyEmit — Interfejs</span><span class="sxs-lookup"><span data-stu-id="55cca-130">IMetaDataAssemblyEmit Interface</span></span>](imetadataassemblyemit-interface.md)
- [<span data-ttu-id="55cca-131">IMetaDataAssemblyImport — Interfejs</span><span class="sxs-lookup"><span data-stu-id="55cca-131">IMetaDataAssemblyImport Interface</span></span>](imetadataassemblyimport-interface.md)
- [<span data-ttu-id="55cca-132">IMetaDataEmit — Interfejs</span><span class="sxs-lookup"><span data-stu-id="55cca-132">IMetaDataEmit Interface</span></span>](imetadataemit-interface.md)
- [<span data-ttu-id="55cca-133">IMetaDataEmit2 — Interfejs</span><span class="sxs-lookup"><span data-stu-id="55cca-133">IMetaDataEmit2 Interface</span></span>](imetadataemit2-interface.md)
- [<span data-ttu-id="55cca-134">IMetaDataImport — Interfejs</span><span class="sxs-lookup"><span data-stu-id="55cca-134">IMetaDataImport Interface</span></span>](imetadataimport-interface.md)
- [<span data-ttu-id="55cca-135">IMetaDataImport2 — Interfejs</span><span class="sxs-lookup"><span data-stu-id="55cca-135">IMetaDataImport2 Interface</span></span>](imetadataimport2-interface.md)
