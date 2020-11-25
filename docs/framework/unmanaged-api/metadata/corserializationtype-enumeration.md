---
title: CorSerializationType — Wyliczenie
ms.date: 03/30/2017
api_name:
- CorSerializationType
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- CorSerializationType
helpviewer_keywords:
- CorSerializationType enumeration [.NET Framework metadata]
ms.assetid: 6b1fcd11-c7fb-4be2-8910-abc862d4caf4
topic_type:
- apiref
ms.openlocfilehash: e9c9674bfe0e5a8006a4881e103b633ee8f2af1d
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95706058"
---
# <a name="corserializationtype-enumeration"></a><span data-ttu-id="69ef8-102">CorSerializationType — Wyliczenie</span><span class="sxs-lookup"><span data-stu-id="69ef8-102">CorSerializationType Enumeration</span></span>

<span data-ttu-id="69ef8-103">Określa, jak obiekt jest serializowany przez środowisko uruchomieniowe języka wspólnego.</span><span class="sxs-lookup"><span data-stu-id="69ef8-103">Specifies how an object is serialized by the common language runtime.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="69ef8-104">Składnia</span><span class="sxs-lookup"><span data-stu-id="69ef8-104">Syntax</span></span>  
  
```cpp  
typedef enum CorSerializationType {  
  
    SERIALIZATION_TYPE_UNDEFINED     = 0,  
    SERIALIZATION_TYPE_BOOLEAN       = ELEMENT_TYPE_BOOLEAN,  
    SERIALIZATION_TYPE_CHAR          = ELEMENT_TYPE_CHAR,  
    SERIALIZATION_TYPE_I1            = ELEMENT_TYPE_I1,  
    SERIALIZATION_TYPE_U1            = ELEMENT_TYPE_U1,  
    SERIALIZATION_TYPE_I2            = ELEMENT_TYPE_I2,  
    SERIALIZATION_TYPE_U2            = ELEMENT_TYPE_U2,  
    SERIALIZATION_TYPE_I4            = ELEMENT_TYPE_I4,  
    SERIALIZATION_TYPE_U4            = ELEMENT_TYPE_U4,  
    SERIALIZATION_TYPE_I8            = ELEMENT_TYPE_I8,  
    SERIALIZATION_TYPE_U8            = ELEMENT_TYPE_U8,  
    SERIALIZATION_TYPE_R4            = ELEMENT_TYPE_R4,  
    SERIALIZATION_TYPE_R8            = ELEMENT_TYPE_R8,  
    SERIALIZATION_TYPE_STRING        = ELEMENT_TYPE_STRING,  
    SERIALIZATION_TYPE_SZARRAY       = ELEMENT_TYPE_SZARRAY,  
    SERIALIZATION_TYPE_TYPE          = 0x50,  
    SERIALIZATION_TYPE_TAGGED_OBJECT = 0x51,  
    SERIALIZATION_TYPE_FIELD         = 0x53,  
    SERIALIZATION_TYPE_PROPERTY      = 0x54,  
    SERIALIZATION_TYPE_ENUM          = 0x55  
  
} CorSerializationType;  
```  
  
## <a name="members"></a><span data-ttu-id="69ef8-105">Elementy członkowskie</span><span class="sxs-lookup"><span data-stu-id="69ef8-105">Members</span></span>  
  
|<span data-ttu-id="69ef8-106">Członek</span><span class="sxs-lookup"><span data-stu-id="69ef8-106">Member</span></span>|<span data-ttu-id="69ef8-107">Opis</span><span class="sxs-lookup"><span data-stu-id="69ef8-107">Description</span></span>|  
|------------|-----------------|  
|`SERIALIZATION_TYPE_UNDEFINED`|<span data-ttu-id="69ef8-108">Serializacja obiektu jest niezdefiniowana.</span><span class="sxs-lookup"><span data-stu-id="69ef8-108">Serialization of the object is undefined.</span></span>|  
|`SERIALIZATION_TYPE_BOOLEAN`|<span data-ttu-id="69ef8-109">Obiekt jest serializowany jako typ Boolean</span><span class="sxs-lookup"><span data-stu-id="69ef8-109">Object is serialized as a Boolean type</span></span>|  
|`SERIALIZATION_TYPE_CHAR`|<span data-ttu-id="69ef8-110">Obiekt jest serializowany jako typ znaku.</span><span class="sxs-lookup"><span data-stu-id="69ef8-110">Object is serialized as a character type.</span></span>|  
|`SERIALIZATION_TYPE_I1`|<span data-ttu-id="69ef8-111">Obiekt jest serializowany jako 1-bajtowa liczba całkowita ze znakiem.</span><span class="sxs-lookup"><span data-stu-id="69ef8-111">Object is serialized as a signed 1-byte integer.</span></span>|  
|`SERIALIZATION_TYPE_U1`|<span data-ttu-id="69ef8-112">Serializacja obiektu jest serializowana jako 1-bajtowa liczba całkowita bez znaku.</span><span class="sxs-lookup"><span data-stu-id="69ef8-112">Object is serialized as an unsigned 1-byte integer.</span></span>|  
|`SERIALIZATION_TYPE_I2`|<span data-ttu-id="69ef8-113">Obiekt jest serializowany jako 2-bajtowa liczba całkowita ze znakiem.</span><span class="sxs-lookup"><span data-stu-id="69ef8-113">Object is serialized as a signed 2-byte integer.</span></span>|  
|`SERIALIZATION_TYPE_U2`|<span data-ttu-id="69ef8-114">Serializacja obiektu jest serializowana jako 2-bajtowa liczba całkowita bez znaku.</span><span class="sxs-lookup"><span data-stu-id="69ef8-114">Object is serialized as an unsigned 2-byte integer.</span></span>|  
|`SERIALIZATION_TYPE_I4`|<span data-ttu-id="69ef8-115">Serializacja obiektu jest serializowana jako 4-bajtowa liczba całkowita.</span><span class="sxs-lookup"><span data-stu-id="69ef8-115">Object is serialized as a signed 4-byte integer.</span></span>|  
|`SERIALIZATION_TYPE_U4`|<span data-ttu-id="69ef8-116">Serializacja obiektu jest serializowana jako 4-bajtowa liczba całkowita bez znaku.</span><span class="sxs-lookup"><span data-stu-id="69ef8-116">Object is serialized as an unsigned 4-byte integer.</span></span>|  
|`SERIALIZATION_TYPE_I8`|<span data-ttu-id="69ef8-117">Obiekt jest serializowany jako 8-bajtowa liczba całkowita ze znakiem.</span><span class="sxs-lookup"><span data-stu-id="69ef8-117">Object is serialized as a signed 8-byte integer.</span></span>|  
|`SERIALIZATION_TYPE_U8`|<span data-ttu-id="69ef8-118">Serializacja obiektu jest serializowana jako 8-bajtowa liczba całkowita bez znaku.</span><span class="sxs-lookup"><span data-stu-id="69ef8-118">Object is serialized as an unsigned 8-byte integer.</span></span>|  
|`SERIALIZATION_TYPE_R4`|<span data-ttu-id="69ef8-119">Serializacja obiektu jest serializowana jako 4-bajtowy zmiennoprzecinkowy.</span><span class="sxs-lookup"><span data-stu-id="69ef8-119">Object is serialized as a 4-byte floating point.</span></span>|  
|`SERIALIZATION_TYPE_R8`|<span data-ttu-id="69ef8-120">Serializacja obiektu jest serializowana jako 8-bajtowy zmiennoprzecinkowy.</span><span class="sxs-lookup"><span data-stu-id="69ef8-120">Object is serialized as an 8-byte floating point.</span></span>|  
|`SERIALIZATION_TYPE_STRING`|<span data-ttu-id="69ef8-121">Obiekt jest serializowany jako typ System. String.</span><span class="sxs-lookup"><span data-stu-id="69ef8-121">Object is serialized as a System.String type.</span></span>|  
|`SERIALIZATION_TYPE_SZARRAY`|<span data-ttu-id="69ef8-122">Serializacja obiektu jest serializowana jako tablica Jednowymiarowa o zerowej granicy.</span><span class="sxs-lookup"><span data-stu-id="69ef8-122">Object is serialized as a single-dimensional, zero lower-bound array.</span></span>|  
|`SERIALIZATION_TYPE_TYPE`|<span data-ttu-id="69ef8-123">Serializacja obiektu jest typem ogólnym.</span><span class="sxs-lookup"><span data-stu-id="69ef8-123">Object is serialized as a generic type.</span></span>|  
|`SERIALIZATION_TYPE_TAGGED_OBJECT`|<span data-ttu-id="69ef8-124">Obiekt jest serializowany jako obiekt otagowany.</span><span class="sxs-lookup"><span data-stu-id="69ef8-124">Object is serialized as a tagged object.</span></span>|  
|`SERIALIZATION_TYPE_FIELD`|<span data-ttu-id="69ef8-125">Obiekt jest serializowany jako pole.</span><span class="sxs-lookup"><span data-stu-id="69ef8-125">Object is serialized as a field.</span></span>|  
|`SERIALIZATION_TYPE_PROPERTY`|<span data-ttu-id="69ef8-126">Obiekt jest serializowany jako właściwość.</span><span class="sxs-lookup"><span data-stu-id="69ef8-126">Object is serialized as a property.</span></span>|  
|`SERIALIZATION_TYPE_ENUM`|<span data-ttu-id="69ef8-127">Obiekt jest serializowany jako Wyliczenie.</span><span class="sxs-lookup"><span data-stu-id="69ef8-127">Object is serialized as an enumeration.</span></span>|  
  
## <a name="requirements"></a><span data-ttu-id="69ef8-128">Wymagania</span><span class="sxs-lookup"><span data-stu-id="69ef8-128">Requirements</span></span>  

 <span data-ttu-id="69ef8-129">**Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="69ef8-129">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="69ef8-130">**Nagłówek:** CorHdr. h</span><span class="sxs-lookup"><span data-stu-id="69ef8-130">**Header:** CorHdr.h</span></span>  
  
 <span data-ttu-id="69ef8-131">**.NET Framework wersje:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="69ef8-131">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="69ef8-132">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="69ef8-132">See also</span></span>

- [<span data-ttu-id="69ef8-133">Wyliczenia metadanych</span><span class="sxs-lookup"><span data-stu-id="69ef8-133">Metadata Enumerations</span></span>](metadata-enumerations.md)
