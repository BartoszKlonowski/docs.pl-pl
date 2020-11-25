---
title: CeeSectionRelocType — Wyliczenie
ms.date: 03/30/2017
api_name:
- CeeSectionRelocType
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- CeeSectionRelocType
helpviewer_keywords:
- CeeSectionRelocType enumeration [.NET Framework metadata]
ms.assetid: 124656f6-0dad-4ceb-9043-d3869ab65cde
topic_type:
- apiref
ms.openlocfilehash: f7aa9699e9929608c90020c6b2d66c301fc11955
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95732713"
---
# <a name="ceesectionreloctype-enumeration"></a><span data-ttu-id="949d9-102">CeeSectionRelocType — Wyliczenie</span><span class="sxs-lookup"><span data-stu-id="949d9-102">CeeSectionRelocType Enumeration</span></span>

<span data-ttu-id="949d9-103">Dostarcza wartości mające wpływ na typ `reloc` instrukcji emitowanej w wywołaniu [ICeeGen:: AddSectionReloc —](iceegen-addsectionreloc-method.md).</span><span class="sxs-lookup"><span data-stu-id="949d9-103">Provides values to influence the type of `reloc` instruction emitted in a call to [ICeeGen::AddSectionReloc](iceegen-addsectionreloc-method.md).</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="949d9-104">Składnia</span><span class="sxs-lookup"><span data-stu-id="949d9-104">Syntax</span></span>  
  
```cpp  
typedef enum  {  
    srRelocAbsolute,  
    srRelocHighLow          = 3,  
    srRelocHighAdj,
    srRelocMapToken,  
    srRelocRelative,  
    srRelocFilePos,  
    srRelocCodeRelative,  
    srRelocIA64Imm64,  
    srRelocDir64,  
    srRelocIA64PcRel25,  
    srRelocIA64PcRel64,    srRelocAbsoluteTagged,    srRelocSentinel,    srNoBaseReloc       = 0x4000,  
    srRelocPtr          = 0x8000,  
    srRelocAbsolutePtr      = srRelocPtr + srRelocAbsolute,  
    srRelocHighLowPtr       = srRelocPtr + srRelocHighLow,  
    srRelocRelativePtr      = srRelocPtr + srRelocRelative,  
    srRelocIA64Imm64Ptr     = srRelocPtr + srRelocIA64Imm64,  
    srRelocDir64Ptr         = srRelocPtr + srRelocDir64  
    } CeeSectionRelocType;  
```  
  
## <a name="members"></a><span data-ttu-id="949d9-105">Elementy członkowskie</span><span class="sxs-lookup"><span data-stu-id="949d9-105">Members</span></span>  
  
|<span data-ttu-id="949d9-106">Członek</span><span class="sxs-lookup"><span data-stu-id="949d9-106">Member</span></span>|<span data-ttu-id="949d9-107">Opis</span><span class="sxs-lookup"><span data-stu-id="949d9-107">Description</span></span>|  
|------------|-----------------|  
|`srRelocAbsolute`|<span data-ttu-id="949d9-108">Generuje tylko odwołanie względne `reloc` do sekcji, wysyłając Nothing do sekcji. reloc.</span><span class="sxs-lookup"><span data-stu-id="949d9-108">Generates only a section-relative `reloc`, sending nothing into a .reloc section.</span></span>|  
|`srRelocHighLow`|<span data-ttu-id="949d9-109">Generuje `reloc` dla lokalizacji wskaźnika.</span><span class="sxs-lookup"><span data-stu-id="949d9-109">Generates a `reloc` for a pointer-sized location.</span></span> <span data-ttu-id="949d9-110">Jest on przekształcany w BASED_HIGHLOW lub BASED_DIR64 w zależności od platformy.</span><span class="sxs-lookup"><span data-stu-id="949d9-110">This is transformed into BASED_HIGHLOW or BASED_DIR64 depending on the platform.</span></span>|  
|`srRelocHighAdj`|<span data-ttu-id="949d9-111">Generuje `reloc` dla pierwszych 16 bitów o 32-bitowej liczbie, gdzie ostatnie 16 bitów jest uwzględnionych w następnym wyrazie w tabeli. reloc.</span><span class="sxs-lookup"><span data-stu-id="949d9-111">Generates a `reloc` for the top 16 bits of a 32-bit number, where the bottom 16 bits are included in the next word in the .reloc table.</span></span>|  
|`srRelocMapToken`|<span data-ttu-id="949d9-112">Generuje relokację mapy tokenów, wysyłając nic do sekcji. reloc.</span><span class="sxs-lookup"><span data-stu-id="949d9-112">Generates a token map relocation, sending nothing into a .reloc section.</span></span>|  
|`srRelocRelative`|<span data-ttu-id="949d9-113">Wskazuje, że wartość jest korektą adresu względnego.</span><span class="sxs-lookup"><span data-stu-id="949d9-113">Indicates that the value is a relative address fixup.</span></span>|  
|`srRelocFilePos`|<span data-ttu-id="949d9-114">Generuje tylko odwołanie względne `reloc` do sekcji, wysyłając Nothing do sekcji. reloc.</span><span class="sxs-lookup"><span data-stu-id="949d9-114">Generates only a section-relative `reloc`, sending nothing into a .reloc section.</span></span> <span data-ttu-id="949d9-115">`reloc`Jest to względne względem położenia pliku sekcji, a nie adresu wirtualnego sekcji.</span><span class="sxs-lookup"><span data-stu-id="949d9-115">This `reloc` is relative to the file position of the section, not the section's virtual address.</span></span>|  
|`srRelocCodeRelative`|<span data-ttu-id="949d9-116">Określa naprawianie adresów względnych w kodzie.</span><span class="sxs-lookup"><span data-stu-id="949d9-116">Specifies a code-relative address fixup.</span></span>|  
|`srRelocIA64Imm64`|<span data-ttu-id="949d9-117">Generuje `reloc` dla adresu 64 bitowego w `movl` instrukcji ia64.</span><span class="sxs-lookup"><span data-stu-id="949d9-117">Generates a `reloc` for a 64 bit address in an ia64 `movl` instruction.</span></span>|  
|`srRelocDir64`|<span data-ttu-id="949d9-118">Generuje `reloc` dla adresu 64-bitowego.</span><span class="sxs-lookup"><span data-stu-id="949d9-118">Generates a `reloc` for a 64-bit address.</span></span>|  
|`srRelocIA64PcRel25`|<span data-ttu-id="949d9-119">Wygeneruj `reloc` adres 25-bitowy względem komputera w `br.call` instrukcji ia64.</span><span class="sxs-lookup"><span data-stu-id="949d9-119">Generate a `reloc` for a 25-bit PC-relative address in an ia64 `br.call` instruction.</span></span>|  
|`srRelocIA64PcRel64`|<span data-ttu-id="949d9-120">Generuje wartość `reloc` dla 64-bitowego adresu komputera w `brl.call` instrukcji ia64.</span><span class="sxs-lookup"><span data-stu-id="949d9-120">Generates a `reloc` for a 64-bit PC-relative address in an ia64 `brl.call` instruction.</span></span>|  
|`srRelocAbsoluteTagged`|<span data-ttu-id="949d9-121">Generuje 30-bitową względną sekcję `reloc` , używaną dla oznakowanych wartości wskaźnika.</span><span class="sxs-lookup"><span data-stu-id="949d9-121">Generates a 30-bit section-relative `reloc`, used for tagged pointer values.</span></span>|  
|`srRelocSentinel`|<span data-ttu-id="949d9-122">Wartość wskaźnikowa, która pomaga zapewnić, że wszelkie dodatki do tego wyliczenia są odzwierciedlone w wewnętrznej `reloc` tablicy nazw.</span><span class="sxs-lookup"><span data-stu-id="949d9-122">A sentinel value to help ensure any additions to this enum are reflected to the internal `reloc` name array.</span></span>|  
|`srNoBaseReloc`|<span data-ttu-id="949d9-123">Określa, że nie ma być emitowana baza `reloc` .</span><span class="sxs-lookup"><span data-stu-id="949d9-123">Specifies not to emit a base `reloc`.</span></span>|  
|`srRelocPtr`|<span data-ttu-id="949d9-124">Wartość wskazująca, że przed przemieszczeniem sekcji jest wskaźnik, a nie przesunięty sekcję.</span><span class="sxs-lookup"><span data-stu-id="949d9-124">A value indicating that the pre-fixup contents of memory are a pointer rather than a section offset.</span></span>|  
  
## <a name="requirements"></a><span data-ttu-id="949d9-125">Wymagania</span><span class="sxs-lookup"><span data-stu-id="949d9-125">Requirements</span></span>  

 <span data-ttu-id="949d9-126">**Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="949d9-126">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="949d9-127">**Nagłówek:** Cor. h</span><span class="sxs-lookup"><span data-stu-id="949d9-127">**Header:** Cor.h</span></span>  
  
 <span data-ttu-id="949d9-128">**Biblioteka:** Uwzględnione jako zasób w MsCorEE.dll</span><span class="sxs-lookup"><span data-stu-id="949d9-128">**Library:** Included as a resource in MsCorEE.dll</span></span>  
  
 <span data-ttu-id="949d9-129">**.NET Framework wersje:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="949d9-129">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="949d9-130">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="949d9-130">See also</span></span>

- [<span data-ttu-id="949d9-131">Wyliczenia metadanych</span><span class="sxs-lookup"><span data-stu-id="949d9-131">Metadata Enumerations</span></span>](metadata-enumerations.md)
- [<span data-ttu-id="949d9-132">ICeeGen — Interfejs</span><span class="sxs-lookup"><span data-stu-id="949d9-132">ICeeGen Interface</span></span>](iceegen-interface.md)
- [<span data-ttu-id="949d9-133">AddSectionReloc, metoda</span><span class="sxs-lookup"><span data-stu-id="949d9-133">AddSectionReloc Method</span></span>](iceegen-addsectionreloc-method.md)
