---
title: Znajdowanie oświadczeń w zestawie oświadczeń
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- claims [WCF], finding in a claimset
- claims [WCF]
ms.assetid: a76ce107-aeb3-47d0-bfa9-134c53664e20
ms.openlocfilehash: c43a47b32a2a3c15d1a51b8b6931ebb021722a64
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96268459"
---
# <a name="finding-claims-in-a-claimset"></a>Znajdowanie oświadczeń w zestawie oświadczeń

Badanie zawartości a <xref:System.IdentityModel.Claims.ClaimSet> dla określonych typów oświadczeń jest typowym zadaniem podczas korzystania z autoryzacji opartej na oświadczeniach. Aby poznać <xref:System.IdentityModel.Claims.ClaimSet> obecność określonych oświadczeń, należy użyć <xref:System.IdentityModel.Claims.ClaimSet.FindClaims%2A> metody. Ta metoda zapewnia lepszą wydajność niż iteracja bezpośrednio w usłudze <xref:System.IdentityModel.Claims.ClaimSet> . Poniższy przykład ilustruje to użycie. Należy pamiętać, `claimType` że `claimRight` Parametry i mogą być `null` . W takim przypadku parametry będą zgodne ze wszystkimi typami i prawami roszczeń.  
  
## <a name="example"></a>Przykład  

 [!code-csharp[c_FindClaimsPerf#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_findclaimsperf/cs/c_findclaimsperf.cs#2)]
 [!code-vb[c_FindClaimsPerf#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_findclaimsperf/vb/c_findclaimsperf.vb#2)]  
  
## <a name="see-also"></a>Zobacz także

- [Zarządzanie oświadczeniami i autoryzacją za pomocą modelu tożsamości](managing-claims-and-authorization-with-the-identity-model.md)
