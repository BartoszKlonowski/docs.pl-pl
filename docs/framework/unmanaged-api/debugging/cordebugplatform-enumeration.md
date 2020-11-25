---
title: Wyliczenie CorDebugPlatform
ms.date: 03/30/2017
api_name:
- CorDebugPlatformEnum
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- CorDebugPlatformEnum
helpviewer_keywords:
- CorDebugPlatformEnum enumeration [.NET Framework debugging]
ms.assetid: c5444816-7378-4521-afd3-bf5e4b5303d5
topic_type:
- apiref
ms.openlocfilehash: 5435f78b28975a5426fcb2fce94904efc1051c5b
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95696404"
---
# <a name="cordebugplatform-enumeration"></a><span data-ttu-id="125b8-102">Wyliczenie CorDebugPlatform</span><span class="sxs-lookup"><span data-stu-id="125b8-102">CorDebugPlatform Enumeration</span></span>

<span data-ttu-id="125b8-103">Zapewnia wartości platformy docelowej, które są używane przez metodę [ICorDebugDataTarget:: GetPlatform](icordebugdatatarget-getplatform-method.md) .</span><span class="sxs-lookup"><span data-stu-id="125b8-103">Provides target platform values that are used by the [ICorDebugDataTarget::GetPlatform](icordebugdatatarget-getplatform-method.md) method.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="125b8-104">Składnia</span><span class="sxs-lookup"><span data-stu-id="125b8-104">Syntax</span></span>  
  
```cpp  
typedef enum CorDebugPlatform  
{  
    CORDB_PLATFORM_WINDOWS_X86,    // Windows on Intel x86  
    CORDB_PLATFORM_WINDOWS_AMD64,  // Windows x64 (AMD64, Intel EM64T)  
    CORDB_PLATFORM_WINDOWS_IA64,   // Windows on Intel IA-64  
    CORDB_PLATFORM_MAC_PPC,        // Macintosh OS on PowerPC  
    CORDB_PLATFORM_MAC_X86,        // Macintosh OS on Intel x86  
    CORDB_PLATFORM_WINDOWS_ARM,    // Windows on ARM  
    CORDB_PLATFORM_MAC_AMD64       // MacOS on Intel x64  
} CorDebugPlatform;  
```  
  
## <a name="members"></a><span data-ttu-id="125b8-105">Elementy członkowskie</span><span class="sxs-lookup"><span data-stu-id="125b8-105">Members</span></span>  
  
|<span data-ttu-id="125b8-106">Członek</span><span class="sxs-lookup"><span data-stu-id="125b8-106">Member</span></span>|<span data-ttu-id="125b8-107">Opis</span><span class="sxs-lookup"><span data-stu-id="125b8-107">Description</span></span>|  
|------------|-----------------|  
|<span data-ttu-id="125b8-108">CORDB_PLATFORM_WINDOWS_X86</span><span class="sxs-lookup"><span data-stu-id="125b8-108">CORDB_PLATFORM_WINDOWS_X86</span></span>|<span data-ttu-id="125b8-109">Platforma docelowa to system Windows działający na sprzęcie Intel x86.</span><span class="sxs-lookup"><span data-stu-id="125b8-109">The target platform is Windows running on Intel x86 hardware.</span></span>|  
|<span data-ttu-id="125b8-110">CORDB_PLATFORM_WINDOWS_AMD64</span><span class="sxs-lookup"><span data-stu-id="125b8-110">CORDB_PLATFORM_WINDOWS_AMD64</span></span>|<span data-ttu-id="125b8-111">Platforma docelowa to 64 bitowego systemu Windows działającego na sprzęcie AMD64 lub Intel EM64T.</span><span class="sxs-lookup"><span data-stu-id="125b8-111">The target platform is 64 bit Windows running on AMD64 or Intel EM64T hardware.</span></span>|  
|<span data-ttu-id="125b8-112">CORDB_PLATFORM_WINDOWS_IA64</span><span class="sxs-lookup"><span data-stu-id="125b8-112">CORDB_PLATFORM_WINDOWS_IA64</span></span>|<span data-ttu-id="125b8-113">Platforma docelowa to 32 bitowego systemu Windows działającego na sprzęcie Intel IA-64.</span><span class="sxs-lookup"><span data-stu-id="125b8-113">The target platform is 32 bit Windows running on Intel IA-64 hardware.</span></span>|  
|<span data-ttu-id="125b8-114">CORDB_PLATFORM_MAC_PPC</span><span class="sxs-lookup"><span data-stu-id="125b8-114">CORDB_PLATFORM_MAC_PPC</span></span>|<span data-ttu-id="125b8-115">Platforma docelowa to system operacyjny Macintosh działający na sprzęcie PowerPC.</span><span class="sxs-lookup"><span data-stu-id="125b8-115">The target platform is the Macintosh operating system running on PowerPC hardware.</span></span>|  
|<span data-ttu-id="125b8-116">CORDB_PLATFORM_MAC_X86</span><span class="sxs-lookup"><span data-stu-id="125b8-116">CORDB_PLATFORM_MAC_X86</span></span>|<span data-ttu-id="125b8-117">Platforma docelowa to system operacyjny Macintosh działający na sprzęcie Intel x86.</span><span class="sxs-lookup"><span data-stu-id="125b8-117">The target platform is the Macintosh operating system running on Intel x86 hardware.</span></span>|  
|<span data-ttu-id="125b8-118">CORDB_PLATFORM_WINDOWS_ARM</span><span class="sxs-lookup"><span data-stu-id="125b8-118">CORDB_PLATFORM_WINDOWS_ARM</span></span>|<span data-ttu-id="125b8-119">Platforma docelowa to system operacyjny Macintosh działający na sprzęcie ARM systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="125b8-119">The target platform is the Macintosh operating system running on Windows ARM hardware.</span></span>|  
|<span data-ttu-id="125b8-120">CORDB_PLATFORM_MAC_AMD64</span><span class="sxs-lookup"><span data-stu-id="125b8-120">CORDB_PLATFORM_MAC_AMD64</span></span>|<span data-ttu-id="125b8-121">Platforma docelowa to system operacyjny Macintosh działający na sprzęcie AMD64.</span><span class="sxs-lookup"><span data-stu-id="125b8-121">The target platform is the Macintosh operating system running on AMD64 hardware.</span></span>|  
  
## <a name="requirements"></a><span data-ttu-id="125b8-122">Wymagania</span><span class="sxs-lookup"><span data-stu-id="125b8-122">Requirements</span></span>  

 <span data-ttu-id="125b8-123">**Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="125b8-123">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="125b8-124">**Nagłówek:** CorDebug. idl, CorDebug. h</span><span class="sxs-lookup"><span data-stu-id="125b8-124">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="125b8-125">**Biblioteka:** CorGuids. lib</span><span class="sxs-lookup"><span data-stu-id="125b8-125">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="125b8-126">**.NET Framework wersje:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="125b8-126">**.NET Framework Versions:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span></span>  
  
 <span data-ttu-id="125b8-127">`CORDB_PLATFORM_WINDOWS_ARM`Elementy i `CORDB_PLATFORM_MAC_AMD64` są dostępne w .NET Framework 4.5.2 i nowszych wersjach.</span><span class="sxs-lookup"><span data-stu-id="125b8-127">The `CORDB_PLATFORM_WINDOWS_ARM` and `CORDB_PLATFORM_MAC_AMD64` members are available in the .NET Framework 4.5.2 and later versions.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="125b8-128">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="125b8-128">See also</span></span>

- [<span data-ttu-id="125b8-129">Debugowanie — wyliczenia</span><span class="sxs-lookup"><span data-stu-id="125b8-129">Debugging Enumerations</span></span>](debugging-enumerations.md)
