---
title: System.ServiceModel.Channels.PeerMaintainerActivity
ms.date: 03/30/2017
ms.assetid: ef28d086-d7fb-4e81-82e9-45a54647783b
ms.openlocfilehash: c1e82611bb776531ad3e3d60283d970602eb7f15
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96293029"
---
# <a name="systemservicemodelchannelspeermaintaineractivity"></a><span data-ttu-id="bdc57-102">System.ServiceModel.Channels.PeerMaintainerActivity</span><span class="sxs-lookup"><span data-stu-id="bdc57-102">System.ServiceModel.Channels.PeerMaintainerActivity</span></span>

<span data-ttu-id="bdc57-103">Moduł PeerMaintainer wykonuje określoną operację (szczegóły zawarte w treści komunikatu śledzenia).</span><span class="sxs-lookup"><span data-stu-id="bdc57-103">The PeerMaintainer module is performing a specific operation (details contained within the trace message body).</span></span>  
  
## <a name="description"></a><span data-ttu-id="bdc57-104">Opis</span><span class="sxs-lookup"><span data-stu-id="bdc57-104">Description</span></span>  

 <span data-ttu-id="bdc57-105">Ten ślad występuje podczas różnych operacji PeerMaintainer.</span><span class="sxs-lookup"><span data-stu-id="bdc57-105">This trace occurs during various PeerMaintainer operations.</span></span>  
  
 <span data-ttu-id="bdc57-106">PeerMaintainer jest wewnętrznym składnikiem elementu równorzędnego.</span><span class="sxs-lookup"><span data-stu-id="bdc57-106">PeerMaintainer is an internal component of PeerNode.</span></span> <span data-ttu-id="bdc57-107">Co minutę lub każde odebrane komunikaty 32 wysyła komunikat LinkUtility do jego sąsiadów z statystykami dotyczącymi liczby wymian komunikatów i liczby ich użytecznych (niezduplikowanych, nienaruszonych).</span><span class="sxs-lookup"><span data-stu-id="bdc57-107">Every minute, or every 32 messages received, it sends a LinkUtility message to its neighbors with statistics about how many messages are exchanged and how many are useful (non-duplicates, untampered).</span></span> <span data-ttu-id="bdc57-108">Ułatwia to określenie narzędzia do łączenia określonego sąsiada.</span><span class="sxs-lookup"><span data-stu-id="bdc57-108">This helps determine a particular neighbor's Link Utility.</span></span> <span data-ttu-id="bdc57-109">W ciągu co pięć minut element utrzymujący sprawdza kondycję połączeń sąsiadów.</span><span class="sxs-lookup"><span data-stu-id="bdc57-109">Approximately every five minutes, the maintainer checks the health of neighbor connections.</span></span> <span data-ttu-id="bdc57-110">Jeśli liczba połączeń sąsiadów przekroczy wartość idealnej, w obszarze obsłudze są oczyszczane najmniejsze przydatne połączenia.</span><span class="sxs-lookup"><span data-stu-id="bdc57-110">If the number of neighbor connections exceeds the ideal amount, the maintainer prunes off the least useful connections.</span></span> <span data-ttu-id="bdc57-111">Jeśli nie ma wystarczającej liczby połączeń, element utrzymujący uzyskuje nowe połączenia.</span><span class="sxs-lookup"><span data-stu-id="bdc57-111">If there are not enough connections, the maintainer acquires new connections.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="bdc57-112">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="bdc57-112">See also</span></span>

- [<span data-ttu-id="bdc57-113">Śledzenie</span><span class="sxs-lookup"><span data-stu-id="bdc57-113">Tracing</span></span>](index.md)
- [<span data-ttu-id="bdc57-114">Rozwiązywanie problemów z aplikacją za pomocą śledzenia</span><span class="sxs-lookup"><span data-stu-id="bdc57-114">Using Tracing to Troubleshoot Your Application</span></span>](using-tracing-to-troubleshoot-your-application.md)
- [<span data-ttu-id="bdc57-115">Administracja i Diagnostyka</span><span class="sxs-lookup"><span data-stu-id="bdc57-115">Administration and Diagnostics</span></span>](../index.md)
