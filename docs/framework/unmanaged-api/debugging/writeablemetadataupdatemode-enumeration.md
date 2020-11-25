---
title: Wyliczenie WriteableMetadataUpdateMode
ms.date: 03/30/2017
dev_langs:
- cpp
api_name:
- WriteableMetadataUpdateMode
api_location:
- mscordbi.dll
api_type:
- COM
ms.assetid: 6758f4d3-6bc7-4c99-8582-e9be00566784
topic_type:
- apiref
ms.openlocfilehash: 1553e18da10844da28bbaf84ba76bc5c34ca49b2
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95725303"
---
# <a name="writeablemetadataupdatemode-enumeration"></a><span data-ttu-id="d2d79-102">Wyliczenie WriteableMetadataUpdateMode</span><span class="sxs-lookup"><span data-stu-id="d2d79-102">WriteableMetadataUpdateMode Enumeration</span></span>

<span data-ttu-id="d2d79-103">[Obsługiwane w .NET Framework 4.5.2 i nowszych wersjach]</span><span class="sxs-lookup"><span data-stu-id="d2d79-103">[Supported in the .NET Framework 4.5.2 and later versions]</span></span>  
  
 <span data-ttu-id="d2d79-104">Zawiera wartości, które określają, czy aktualizacje w pamięci mają być widoczne dla debugera.</span><span class="sxs-lookup"><span data-stu-id="d2d79-104">Provides values that specify whether in-memory updates to metadata are visible to a debugger.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="d2d79-105">Składnia</span><span class="sxs-lookup"><span data-stu-id="d2d79-105">Syntax</span></span>  
  
```cpp
typedef enum WriteableMetadataUpdateMode {  
   LegacyCompatPolicy,  
   AlwaysShowUpdates  
} WriteableMetadataUpdateMode;  
```  
  
## <a name="members"></a><span data-ttu-id="d2d79-106">Elementy członkowskie</span><span class="sxs-lookup"><span data-stu-id="d2d79-106">Members</span></span>  
  
|<span data-ttu-id="d2d79-107">Nazwa elementu członkowskiego</span><span class="sxs-lookup"><span data-stu-id="d2d79-107">Member name</span></span>|<span data-ttu-id="d2d79-108">Opis</span><span class="sxs-lookup"><span data-stu-id="d2d79-108">Description</span></span>|  
|-----------------|-----------------|  
|`LegacyCompatPolicy`|<span data-ttu-id="d2d79-109">Zachowaj zgodność z poprzednimi wersjami .NET Framework, gdy aktualizacje w pamięci mają być widoczne dla metadanych.</span><span class="sxs-lookup"><span data-stu-id="d2d79-109">Maintain compatibility with previous versions of the .NET Framework when making in-memory updates to metadata visible.</span></span> <span data-ttu-id="d2d79-110">Zobacz sekcję Spostrzeżenia, aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="d2d79-110">See the Remarks section for more information.</span></span>|  
|`AlwaysShowUpdates`|<span data-ttu-id="d2d79-111">Wprowadź aktualizacje w pamięci do metadanych widocznych dla debugera.</span><span class="sxs-lookup"><span data-stu-id="d2d79-111">Make in-memory updates to metadata visible to the debugger.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="d2d79-112">Uwagi</span><span class="sxs-lookup"><span data-stu-id="d2d79-112">Remarks</span></span>  

 <span data-ttu-id="d2d79-113">Element członkowski `WriteableMetadataUpdateMode` wyliczenia można przesłać do metody [SetWriteableMetadataUpdateMode](icordebugprocess7-setwriteablemetadataupdatemode-method.md) w celu określenia, czy aktualizacje w pamięci w procesie docelowym są widoczne dla debugera.</span><span class="sxs-lookup"><span data-stu-id="d2d79-113">A member of the `WriteableMetadataUpdateMode` enumeration can be passed to the [SetWriteableMetadataUpdateMode](icordebugprocess7-setwriteablemetadataupdatemode-method.md) method to control whether in-memory updates to metadata in the target process are visible to the debugger.</span></span>  
  
 <span data-ttu-id="d2d79-114">`LegacyCompatPolicy`Opcja wymusza takie samo zachowanie jak w wersjach .NET Framework przed 4.5.2.</span><span class="sxs-lookup"><span data-stu-id="d2d79-114">The `LegacyCompatPolicy` option enforces the same behavior as in versions of the .NET Framework before 4.5.2.</span></span> <span data-ttu-id="d2d79-115">Często oznacza to, że metadane z aktualizacji nie są widoczne.</span><span class="sxs-lookup"><span data-stu-id="d2d79-115">This often means that metadata from updates is not visible.</span></span> <span data-ttu-id="d2d79-116">Jednak wywołania do wielu metod debugowania niejawnie przekształcenie debugera w celu udostępnienia aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="d2d79-116">However, calls to a number of debugging methods implicitly coerce the debugger to make updates visible.</span></span> <span data-ttu-id="d2d79-117">Jeśli na przykład debuger przekaże [ICorDebugILFrame:: GetLocalVariable —](icordebugilframe-getlocalvariable-method.md) indeks zmiennej nie został znaleziony w oryginalnych metadanych metody, wszystkie metadane modułu zostaną zaktualizowane do migawki zgodnej z bieżącym stanem procesu.</span><span class="sxs-lookup"><span data-stu-id="d2d79-117">For example, if the debugger passes [ICorDebugILFrame::GetLocalVariable](icordebugilframe-getlocalvariable-method.md) the index of a variable not found in the method's original metadata, all metadata for the module is updated to a snapshot matching the current state of the process.</span></span> <span data-ttu-id="d2d79-118">Innymi słowy, z `LegacyCompatPolicy` opcją debuger może zobaczyć Brak, niektóre lub wszystkie dostępne aktualizacje metadanych w zależności od tego, w jaki sposób używa innych części niezarządzanego interfejsu API debugowania.</span><span class="sxs-lookup"><span data-stu-id="d2d79-118">In other words, with the `LegacyCompatPolicy` option, the debugger might see none, some, or all of the available metadata updates, depending on how it uses other parts of the unmanaged debugging API.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="d2d79-119">Wymagania</span><span class="sxs-lookup"><span data-stu-id="d2d79-119">Requirements</span></span>  

 <span data-ttu-id="d2d79-120">**Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="d2d79-120">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="d2d79-121">**Nagłówek:** CorDebug. idl, CorDebug. h</span><span class="sxs-lookup"><span data-stu-id="d2d79-121">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="d2d79-122">**Biblioteka:** CorGuids. lib</span><span class="sxs-lookup"><span data-stu-id="d2d79-122">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="d2d79-123">**.NET Framework wersje:**[!INCLUDE[net_current_v452plus](../../../../includes/net-current-v452plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="d2d79-123">**.NET Framework Versions:** [!INCLUDE[net_current_v452plus](../../../../includes/net-current-v452plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="d2d79-124">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="d2d79-124">See also</span></span>

- [<span data-ttu-id="d2d79-125">Debugowanie — wyliczenia</span><span class="sxs-lookup"><span data-stu-id="d2d79-125">Debugging Enumerations</span></span>](debugging-enumerations.md)
- [<span data-ttu-id="d2d79-126">SetWriteableMetadataUpdateMode, metoda</span><span class="sxs-lookup"><span data-stu-id="d2d79-126">SetWriteableMetadataUpdateMode Method</span></span>](icordebugprocess7-setwriteablemetadataupdatemode-method.md)
