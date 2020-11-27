---
title: Oświadczenia i odmawianie dostępu do zasobów
ms.date: 03/30/2017
helpviewer_keywords:
- claims [WCF], denying access to resources
ms.assetid: 145ebb41-680e-4256-b14c-1efb4af1e982
ms.openlocfilehash: 2c903d5b5aa520b9c79fb8b36912324feaf9a432
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96264924"
---
# <a name="claims-and-denying-access-to-resources"></a><span data-ttu-id="d49e5-102">Oświadczenia i odmawianie dostępu do zasobów</span><span class="sxs-lookup"><span data-stu-id="d49e5-102">Claims and Denying Access to Resources</span></span>

<span data-ttu-id="d49e5-103">Windows Communication Foundation (WCF) obsługuje mechanizm autoryzacji oparty na oświadczeniach.</span><span class="sxs-lookup"><span data-stu-id="d49e5-103">Windows Communication Foundation (WCF) supports a claims-based authorization mechanism.</span></span> <span data-ttu-id="d49e5-104">Jak również umożliwienie dostępu do zasobów na podstawie obecności oświadczeń, systemy często odmawiają dostępu do zasobów na podstawie obecności oświadczeń.</span><span class="sxs-lookup"><span data-stu-id="d49e5-104">As well as allowing access to resources based on the presence of claims, systems often deny access to resources based on the presence of claims.</span></span> <span data-ttu-id="d49e5-105">Takie systemy powinny sprawdzać <xref:System.IdentityModel.Policy.AuthorizationContext> oświadczenia, które powodują odmowę dostępu przed wyszukiwaniem oświadczeń, w wyniku których jest dozwolony dostęp.</span><span class="sxs-lookup"><span data-stu-id="d49e5-105">Such systems should examine the <xref:System.IdentityModel.Policy.AuthorizationContext> for claims that result in access being denied before looking for claims that result in access being allowed.</span></span>  
  
 <span data-ttu-id="d49e5-106">Na przykład system może odmówić dostępu do zasobu wszystkim osobom, które mają wierzytelność z typem, z `Age` prawej strony <xref:System.IdentityModel.Claims.Rights.PossessProperty%2A> , i wartością zasobu tylko wtedy, `Under 21` gdy ta tożsamość ma również typ `Name` , po prawej stronie <xref:System.IdentityModel.Claims.Rights.Identity%2A> i wartość zasobu `Mallory` .</span><span class="sxs-lookup"><span data-stu-id="d49e5-106">For example, a system might deny access to a resource to anyone who has a claim with a type of `Age`, a right of <xref:System.IdentityModel.Claims.Rights.PossessProperty%2A>, and a resource value of `Under 21` only when that identity also has a claim of type `Name`, a right of <xref:System.IdentityModel.Claims.Rights.Identity%2A>, and a resource value of `Mallory`.</span></span> <span data-ttu-id="d49e5-107">W inny sposób system odmówi dostępu wszystkim osobom, które są w wieku poniżej 21 lat i udzielą dostępu, gdy nazwa jest Mallory.</span><span class="sxs-lookup"><span data-stu-id="d49e5-107">Put another way, the system denies access to anyone who is under 21 years old and grants access when the name is Mallory.</span></span> <span data-ttu-id="d49e5-108">Aby poprawnie zaimplementować tę semantykę, ważne jest, aby najpierw wyszukać zgłoszenie `Age` i określić, czy wiek jest w wieku poniżej 21 lat.</span><span class="sxs-lookup"><span data-stu-id="d49e5-108">To correctly implement this semantic, it is important to look for the `Age` claim first and determine whether the age is under 21 years old.</span></span> <span data-ttu-id="d49e5-109">W przeciwnym razie, jeśli Mallory ma wartość 21, do zasobu można udzielić dostępu wyłącznie na podstawie tego `Name` żądania.</span><span class="sxs-lookup"><span data-stu-id="d49e5-109">Otherwise, if Mallory is under 21, then the resource may be granted access solely on the basis of the `Name` claim.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="d49e5-110">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="d49e5-110">See also</span></span>

- [<span data-ttu-id="d49e5-111">Zarządzanie oświadczeniami i autoryzacją za pomocą modelu tożsamości</span><span class="sxs-lookup"><span data-stu-id="d49e5-111">Managing Claims and Authorization with the Identity Model</span></span>](managing-claims-and-authorization-with-the-identity-model.md)
- [<span data-ttu-id="d49e5-112">Oświadczenia i tokeny</span><span class="sxs-lookup"><span data-stu-id="d49e5-112">Claims and Tokens</span></span>](claims-and-tokens.md)
