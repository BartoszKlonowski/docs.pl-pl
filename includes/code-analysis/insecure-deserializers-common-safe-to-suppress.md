---
author: dotpaul
ms.author: paulming
ms.date: 04/17/2019
ms.topic: include
ms.openlocfilehash: 2b60e0e713745b1887ff148c5b3ef151584eb21d
ms.sourcegitcommit: c04535ad05e374fb269fcfc6509217755fbc0d54
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/25/2020
ms.locfileid: "96586680"
---
<span data-ttu-id="d4003-101">Można bezpiecznie pominąć ostrzeżenie z tej reguły, jeśli:</span><span class="sxs-lookup"><span data-stu-id="d4003-101">It's safe to suppress a warning from this rule if:</span></span>

- <span data-ttu-id="d4003-102">Wiadomo, że dane wejściowe są zaufane.</span><span class="sxs-lookup"><span data-stu-id="d4003-102">You know the input is trusted.</span></span> <span data-ttu-id="d4003-103">Należy wziąć pod uwagę, że granica zaufania aplikacji i przepływy danych mogą ulec zmianie z upływem czasu.</span><span class="sxs-lookup"><span data-stu-id="d4003-103">Consider that your application's trust boundary and data flows may change over time.</span></span>
- <span data-ttu-id="d4003-104">Wykonano jedną z tych środków ostrożności w zakresie [rozwiązywania naruszeń](#how-to-fix-violations).</span><span class="sxs-lookup"><span data-stu-id="d4003-104">You've taken one of the precautions in [How to fix violations](#how-to-fix-violations).</span></span>
