---
title: CorSymAddrKind — Wyliczenie
ms.date: 03/30/2017
api_name:
- CorSymAddrKind
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- CorSymAddrKind
helpviewer_keywords:
- CorSymAddrKind enumeration [.NET Framework debugging]
ms.assetid: 3ef841c2-cade-42ee-ba34-2ef91d6d0879
topic_type:
- apiref
ms.openlocfilehash: f71d8956e8706cdc71b94b6e6e2e8210e5b9161e
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95725238"
---
# <a name="corsymaddrkind-enumeration"></a><span data-ttu-id="36318-102">CorSymAddrKind — Wyliczenie</span><span class="sxs-lookup"><span data-stu-id="36318-102">CorSymAddrKind Enumeration</span></span>

<span data-ttu-id="36318-103">Wskazuje typ adresu pamięci.</span><span class="sxs-lookup"><span data-stu-id="36318-103">Indicates the type of memory address.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="36318-104">Składnia</span><span class="sxs-lookup"><span data-stu-id="36318-104">Syntax</span></span>  
  
```cpp  
typedef enum CorSymAddrKind  
{  
    ADDR_IL_OFFSET          = 1,  
    ADDR_NATIVE_RVA         = 2,  
    ADDR_NATIVE_REGISTER    = 3,  
    ADDR_NATIVE_REGREL      = 4,  
    ADDR_NATIVE_OFFSET      = 5,  
    ADDR_NATIVE_REGREG      = 6,  
    ADDR_NATIVE_REGSTK      = 7,  
    ADDR_NATIVE_STKREG      = 8,  
    ADDR_BITFIELD           = 9,  
    ADDR_NATIVE_ISECTOFFSET = 10  
} CorSymAddrKind;  
```  
  
## <a name="members"></a><span data-ttu-id="36318-105">Elementy członkowskie</span><span class="sxs-lookup"><span data-stu-id="36318-105">Members</span></span>  
  
|<span data-ttu-id="36318-106">Członek</span><span class="sxs-lookup"><span data-stu-id="36318-106">Member</span></span>|<span data-ttu-id="36318-107">Opis</span><span class="sxs-lookup"><span data-stu-id="36318-107">Description</span></span>|  
|------------|-----------------|  
|`ADDR_IL_OFFSET`|<span data-ttu-id="36318-108">Wskazuje zmienną lokalną języka pośredniego (MSIL) firmy Microsoft lub indeks parametru.</span><span class="sxs-lookup"><span data-stu-id="36318-108">Indicates a Microsoft intermediate language (MSIL) local variable or parameter index.</span></span>|  
|`ADDR_NATIVE_RVA`|<span data-ttu-id="36318-109">Wskazuje względny adres wirtualny do modułu.</span><span class="sxs-lookup"><span data-stu-id="36318-109">Indicates a relative virtual address into a module.</span></span>|  
|`ADDR_NATIVE_REGISTER`|<span data-ttu-id="36318-110">Wskazuje rejestr procesora CPU.</span><span class="sxs-lookup"><span data-stu-id="36318-110">Indicates a CPU register.</span></span>|  
|`ADDR_NATIVE_REGREL`|<span data-ttu-id="36318-111">Wskazuje, że pierwszy adres jest rejestrem, a drugi adres jest przesunięty.</span><span class="sxs-lookup"><span data-stu-id="36318-111">Indicates that the first address is a register and the second address is an offset.</span></span>|  
|`ADDR_NATIVE_OFFSET`|<span data-ttu-id="36318-112">Wskazuje przesunięcie od adresu podstawowego.</span><span class="sxs-lookup"><span data-stu-id="36318-112">Indicates an offset from a base address.</span></span>|  
|`ADDR_NATIVE_REGREG`|<span data-ttu-id="36318-113">Wskazuje, że pierwszy adres jest małą częścią rejestru, a drugi adres jest dużą częścią.</span><span class="sxs-lookup"><span data-stu-id="36318-113">Indicates that the first address is the low portion of a register, and the second address is the high portion.</span></span>|  
|`ADDR_NATIVE_REGSTK`|<span data-ttu-id="36318-114">Wskazuje, że pierwszy adres jest małą częścią rejestru, drugi jest dużą częścią, a trzeci jest przesunięciem.</span><span class="sxs-lookup"><span data-stu-id="36318-114">Indicates that the first address is the low portion of a register, the second is the high portion, and the third is an offset.</span></span>|  
|`ADDR_NATIVE_STKREG`|<span data-ttu-id="36318-115">Wskazuje, że pierwszy adres jest rejestrem, drugi jest przesunięciem, a trzeci to wysoka część rejestru.</span><span class="sxs-lookup"><span data-stu-id="36318-115">Indicates that the first address is a register, the second is an offset, and the third is the high portion of the register.</span></span>|  
|`ADDR_BITFIELD`|<span data-ttu-id="36318-116">Wskazuje, że pierwszy adres jest początkiem pola, a drugi adres jest długością pola.</span><span class="sxs-lookup"><span data-stu-id="36318-116">Indicates that the first address is the start of a field and the second address is the field length.</span></span>|  
|`ADDR_NATIVE_ISECTOFFSET`|<span data-ttu-id="36318-117">Wskazuje, że pierwszy adres jest sekcją, a drugi adres jest przesunięciem.</span><span class="sxs-lookup"><span data-stu-id="36318-117">Indicates that the first address is the section and the second address is an offset.</span></span>|  
  
## <a name="requirements"></a><span data-ttu-id="36318-118">Wymagania</span><span class="sxs-lookup"><span data-stu-id="36318-118">Requirements</span></span>  

 <span data-ttu-id="36318-119">**Nagłówek:** CorSym. idl, CorSym. h</span><span class="sxs-lookup"><span data-stu-id="36318-119">**Header:** CorSym.idl, CorSym.h</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="36318-120">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="36318-120">See also</span></span>

- [<span data-ttu-id="36318-121">Wyliczenia magazynu symboli diagnostycznych</span><span class="sxs-lookup"><span data-stu-id="36318-121">Diagnostics Symbol Store Enumerations</span></span>](diagnostics-symbol-store-enumerations.md)
