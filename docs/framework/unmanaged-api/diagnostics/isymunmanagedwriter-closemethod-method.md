---
title: ISymUnmanagedWriter::CloseMethod — Metoda
ms.date: 03/30/2017
api_name:
- ISymUnmanagedWriter.CloseMethod
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedWriter::CloseMethod
helpviewer_keywords:
- ISymUnmanagedWriter::CloseMethod method [.NET Framework debugging]
- CloseMethod method [.NET Framework debugging]
ms.assetid: b8025e04-f0e5-40c8-849c-8cd51323420e
topic_type:
- apiref
ms.openlocfilehash: fcf250f10baf4c65cd1c8c918655e4b9f4f5cc4b
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95731738"
---
# <a name="isymunmanagedwriterclosemethod-method"></a><span data-ttu-id="08494-102">ISymUnmanagedWriter::CloseMethod — Metoda</span><span class="sxs-lookup"><span data-stu-id="08494-102">ISymUnmanagedWriter::CloseMethod Method</span></span>

<span data-ttu-id="08494-103">Zamyka bieżącą metodę.</span><span class="sxs-lookup"><span data-stu-id="08494-103">Closes the current method.</span></span> <span data-ttu-id="08494-104">Po zamknięciu metody nie można definiować więcej symboli.</span><span class="sxs-lookup"><span data-stu-id="08494-104">Once a method is closed, no more symbols can be defined within it.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="08494-105">Składnia</span><span class="sxs-lookup"><span data-stu-id="08494-105">Syntax</span></span>  
  
```cpp  
HRESULT CloseMethod();  
```  
  
## <a name="return-value"></a><span data-ttu-id="08494-106">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="08494-106">Return Value</span></span>  

 <span data-ttu-id="08494-107">S_OK, jeśli metoda się powiedzie; w przeciwnym razie E_FAIL lub inny kod błędu.</span><span class="sxs-lookup"><span data-stu-id="08494-107">S_OK if the method succeeds; otherwise, E_FAIL or some other error code.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="08494-108">Wymagania</span><span class="sxs-lookup"><span data-stu-id="08494-108">Requirements</span></span>  

 <span data-ttu-id="08494-109">**Nagłówek:** CorSym. idl, CorSym. h</span><span class="sxs-lookup"><span data-stu-id="08494-109">**Header:** CorSym.idl, CorSym.h</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="08494-110">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="08494-110">See also</span></span>

- [<span data-ttu-id="08494-111">ISymUnmanagedWriter — Interfejs</span><span class="sxs-lookup"><span data-stu-id="08494-111">ISymUnmanagedWriter Interface</span></span>](isymunmanagedwriter-interface.md)
- [<span data-ttu-id="08494-112">OpenMethod, metoda</span><span class="sxs-lookup"><span data-stu-id="08494-112">OpenMethod Method</span></span>](isymunmanagedwriter-openmethod-method.md)
