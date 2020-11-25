---
title: ICLRMetadataLocator::GetMetadata — Metoda
ms.date: 03/30/2017
api_name:
- ICLRMetadataLocator.GetMetadata
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICLRMetadataLocator::GetMetadata
helpviewer_keywords:
- GetMetadata method, ICLRMetadataLocator interface [.NET Framework debugging]
- ICLRMetadataLocator::GetMetadata method [.NET Framework debugging]
ms.assetid: 704a8893-ac56-43b4-90ea-715f38ccb40e
topic_type:
- apiref
ms.openlocfilehash: f0ba2342e9704ba06dd1d3612f699298c734a5eb
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95723522"
---
# <a name="iclrmetadatalocatorgetmetadata-method"></a><span data-ttu-id="9a9fd-102">ICLRMetadataLocator::GetMetadata — Metoda</span><span class="sxs-lookup"><span data-stu-id="9a9fd-102">ICLRMetadataLocator::GetMetadata Method</span></span>

<span data-ttu-id="9a9fd-103">Wywoływane przez usługi dostępu do danych środowiska uruchomieniowego języka wspólnego (CLR) do pobierania metadanych obrazu.</span><span class="sxs-lookup"><span data-stu-id="9a9fd-103">Called by the common language runtime (CLR) data access services to retrieve the metadata of an image.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="9a9fd-104">Składnia</span><span class="sxs-lookup"><span data-stu-id="9a9fd-104">Syntax</span></span>  
  
```cpp  
HRESULT GetMetadata(  
    [in]  LPCWSTR         imagePath,  
    [in]  ULONG32         imageTimestamp,  
    [in]  ULONG32         imageSize,  
    [in]  GUID*           mvid,  
    [in]  ULONG32         mdRva,  
    [in]  ULONG32         flags,  
    [in]  ULONG32         bufferSize,  
    [out, size_is(bufferSize), length_is(*dataSize)]  
          BYTE*           buffer,  
    [out] ULONG32*        dataSize  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="9a9fd-105">Parametry</span><span class="sxs-lookup"><span data-stu-id="9a9fd-105">Parameters</span></span>  

 `imagePath`  
 <span data-ttu-id="9a9fd-106">podczas Ciąg określający ścieżkę pliku obrazu.</span><span class="sxs-lookup"><span data-stu-id="9a9fd-106">[in] A string that specifies the path of the image file.</span></span>  
  
 `imageTimestamp`  
 <span data-ttu-id="9a9fd-107">podczas Sygnatura czasowa pliku obrazu.</span><span class="sxs-lookup"><span data-stu-id="9a9fd-107">[in] The time stamp of the image file.</span></span>  
  
 `imageSize`  
 <span data-ttu-id="9a9fd-108">podczas Rozmiar pliku obrazu.</span><span class="sxs-lookup"><span data-stu-id="9a9fd-108">[in] The size of the image file.</span></span>  
  
 `mvid`  
 <span data-ttu-id="9a9fd-109">podczas Unikatowy identyfikator globalny obrazu.</span><span class="sxs-lookup"><span data-stu-id="9a9fd-109">[in] The globally unique identifier of the image.</span></span>  
  
 `mdRva`  
 <span data-ttu-id="9a9fd-110">podczas Względny adres wirtualny (RVA) metadanych.</span><span class="sxs-lookup"><span data-stu-id="9a9fd-110">[in] The relative virtual address (RVA) of the metadata.</span></span> <span data-ttu-id="9a9fd-111">Adres jest określany względem adresu podstawowego obrazu.</span><span class="sxs-lookup"><span data-stu-id="9a9fd-111">The address is relative to the image base address.</span></span>  
  
 `flags`  
 <span data-ttu-id="9a9fd-112">podczas Zarezerwowane do użytku w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="9a9fd-112">[in] Reserved for future use.</span></span>  
  
 `bufferSize`  
 <span data-ttu-id="9a9fd-113">podczas Rozmiar buforu, w którym mają zostać umieszczone metadane.</span><span class="sxs-lookup"><span data-stu-id="9a9fd-113">[in] The size of the buffer in which to place the metadata.</span></span>  
  
 `buffer`  
 <span data-ttu-id="9a9fd-114">określoną Bufor, w którym mają zostać umieszczone metadane.</span><span class="sxs-lookup"><span data-stu-id="9a9fd-114">[out] The buffer in which to place the metadata.</span></span>  
  
 `dataSize`  
 <span data-ttu-id="9a9fd-115">określoną Rozmiar zwracanych metadanych.</span><span class="sxs-lookup"><span data-stu-id="9a9fd-115">[out] The size of the metadata that is returned.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="9a9fd-116">Uwagi</span><span class="sxs-lookup"><span data-stu-id="9a9fd-116">Remarks</span></span>  

 <span data-ttu-id="9a9fd-117">Ta metoda jest implementowana przez moduł zapisujący aplikacji debugowania.</span><span class="sxs-lookup"><span data-stu-id="9a9fd-117">This method is implemented by the writer of the debugging application.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="9a9fd-118">Wymagania</span><span class="sxs-lookup"><span data-stu-id="9a9fd-118">Requirements</span></span>  

 <span data-ttu-id="9a9fd-119">**Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="9a9fd-119">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="9a9fd-120">**Nagłówek:** ClrData. idl, ClrData. h</span><span class="sxs-lookup"><span data-stu-id="9a9fd-120">**Header:** ClrData.idl, ClrData.h</span></span>  
  
 <span data-ttu-id="9a9fd-121">**Biblioteka:** CorGuids. lib</span><span class="sxs-lookup"><span data-stu-id="9a9fd-121">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="9a9fd-122">**.NET Framework wersje:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="9a9fd-122">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="9a9fd-123">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="9a9fd-123">See also</span></span>

- [<span data-ttu-id="9a9fd-124">ICLRMetadataLocator — Interfejs</span><span class="sxs-lookup"><span data-stu-id="9a9fd-124">ICLRMetadataLocator Interface</span></span>](iclrmetadatalocator-interface.md)
