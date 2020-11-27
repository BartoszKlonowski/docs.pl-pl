---
title: Grupowanie połączeń
ms.date: 03/30/2017
helpviewer_keywords:
- Internet, connections
- connections [.NET Framework], grouping
- WebRequest class, connection grouping
- network resources, connections
- connection pooling
ms.assetid: 2ec502e8-4ba0-4c22-9410-f28eaf4eee63
ms.openlocfilehash: 8bd4412a4c13dd490fce3118f59b5bb1f0d3ea85
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96250570"
---
# <a name="connection-grouping"></a><span data-ttu-id="76ed9-102">Grupowanie połączeń</span><span class="sxs-lookup"><span data-stu-id="76ed9-102">Connection Grouping</span></span>

<span data-ttu-id="76ed9-103">Grupowanie połączeń kojarzy określone żądania w ramach jednej aplikacji z określoną pulą połączeń.</span><span class="sxs-lookup"><span data-stu-id="76ed9-103">Connection grouping associates specific requests within a single application to a defined connection pool.</span></span> <span data-ttu-id="76ed9-104">Może to być wymagane przez aplikację warstwy środkowej, która łączy się z serwerem zaplecza w imieniu użytkownika i używa protokołu uwierzytelniania obsługującego delegowanie, takiego jak Kerberos lub przez aplikację warstwy środkowej, która dostarcza własne poświadczenia, jak w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="76ed9-104">This can be required by a middle-tier application that connects to a back-end server on behalf of a user and uses an authentication protocol that supports delegation, such as Kerberos, or by a middle-tier application that supplies its own credentials, as in the example below.</span></span> <span data-ttu-id="76ed9-105">Załóżmy na przykład, że użytkownik, Jan znajduje się w wewnętrznej witrynie sieci Web, która wyświetla informacje o płacach.</span><span class="sxs-lookup"><span data-stu-id="76ed9-105">For example, suppose a user, Joe, visits an internal Web site that displays his payroll information.</span></span> <span data-ttu-id="76ed9-106">Po uwierzytelnieniu Jan serwer aplikacji warstwy środkowej używa poświadczeń Jan do łączenia się z serwerem zaplecza w celu pobrania informacji o płacach.</span><span class="sxs-lookup"><span data-stu-id="76ed9-106">After authenticating Joe, the middle-tier application server uses Joe's credentials to connect to the back-end server to retrieve his payroll information.</span></span> <span data-ttu-id="76ed9-107">Następnie Susan odwiedza witrynę i żąda informacji o płacach.</span><span class="sxs-lookup"><span data-stu-id="76ed9-107">Next, Susan visits the site and requests her payroll information.</span></span> <span data-ttu-id="76ed9-108">Ponieważ aplikacja warstwy środkowej ma już połączenie przy użyciu poświadczeń Jan, serwer zaplecza reaguje na informacje o Jan.</span><span class="sxs-lookup"><span data-stu-id="76ed9-108">Because the middle-tier application has already made a connection using Joe's credentials, the back-end server responds with Joe's information.</span></span> <span data-ttu-id="76ed9-109">Jeśli jednak aplikacja przypisze każde żądanie wysyłane do serwera zaplecza do grupy połączeń utworzonej przy użyciu nazwy użytkownika, każdy użytkownik należy do osobnej puli połączeń i nie może przypadkowo udostępnić informacji uwierzytelniania innym użytkownikom.</span><span class="sxs-lookup"><span data-stu-id="76ed9-109">However, if the application assigns each request sent to the back-end server to a connection group formed from the user name, then each user belongs to a separate connection pool and cannot accidentally share authentication information with another user.</span></span>  
  
 <span data-ttu-id="76ed9-110">Aby przypisać żądanie do określonej grupy połączeń, należy przypisać nazwę do <xref:System.Net.WebRequest.ConnectionGroupName%2A> właściwości <xref:System.Net.WebRequest> przed wykonaniem żądania.</span><span class="sxs-lookup"><span data-stu-id="76ed9-110">To assign a request to a specific connection group, you must assign a name to the <xref:System.Net.WebRequest.ConnectionGroupName%2A> property of your <xref:System.Net.WebRequest> before making the request.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="76ed9-111">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="76ed9-111">See also</span></span>

- [<span data-ttu-id="76ed9-112">Zarządzanie połączeniami</span><span class="sxs-lookup"><span data-stu-id="76ed9-112">Managing Connections</span></span>](managing-connections.md)
- [<span data-ttu-id="76ed9-113">Instrukcje: przypisywanie informacji użytkownika do połączeń grupowych</span><span class="sxs-lookup"><span data-stu-id="76ed9-113">How to: Assign User Information to Group Connections</span></span>](how-to-assign-user-information-to-group-connections.md)
