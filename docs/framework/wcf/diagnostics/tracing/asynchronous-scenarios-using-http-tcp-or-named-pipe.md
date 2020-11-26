---
title: Scenariusze asynchroniczne z zastosowaniem protokołu HTTP lub TCP albo potoku nazwanego
ms.date: 03/30/2017
ms.assetid: a4d62402-43a4-48a4-9ced-220633ebc4ce
ms.openlocfilehash: 00213c8d117f4319d7e29312dd0b9805d916231a
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96244148"
---
# <a name="asynchronous-scenarios-using-http-tcp-or-named-pipe"></a><span data-ttu-id="c1064-102">Scenariusze asynchroniczne z zastosowaniem protokołu HTTP lub TCP albo potoku nazwanego</span><span class="sxs-lookup"><span data-stu-id="c1064-102">Asynchronous Scenarios using HTTP, TCP, or Named-Pipe</span></span>

<span data-ttu-id="c1064-103">W tym temacie opisano działania i transfery dla różnych scenariuszy żądań asynchronicznych/odpowiedzi z żądaniami wielowątkowymi przy użyciu protokołu HTTP, TCP lub potoku nazwanego.</span><span class="sxs-lookup"><span data-stu-id="c1064-103">This topic describes the activities and transfers for different asynchronous request/reply scenarios, with multithreaded requests using HTTP, TCP, or named pipe.</span></span>  
  
## <a name="asynchronous-requestreply-without-errors"></a><span data-ttu-id="c1064-104">Asynchroniczne żądanie/odpowiedź bez błędów</span><span class="sxs-lookup"><span data-stu-id="c1064-104">Asynchronous Request/Reply without Errors</span></span>  

 <span data-ttu-id="c1064-105">W tej sekcji opisano działania i transfery scenariusza żądania/odpowiedzi asynchronicznej oraz klientów wielowątkowych.</span><span class="sxs-lookup"><span data-stu-id="c1064-105">This section describes the activities and transfers for an asynchronous request/reply scenario, with multithreaded clients.</span></span>  
  
 <span data-ttu-id="c1064-106">Działanie obiektu wywołującego kończy się `beginCall` , gdy zwraca i `endCall` zwraca.</span><span class="sxs-lookup"><span data-stu-id="c1064-106">The caller activity terminates when `beginCall` returns, and `endCall` returns.</span></span> <span data-ttu-id="c1064-107">Wywołanie zwrotne zwraca wartość wywołania zwrotnego.</span><span class="sxs-lookup"><span data-stu-id="c1064-107">If a callback is called, the callback returns.</span></span>  
  
 <span data-ttu-id="c1064-108">Wywołane działanie kończy się `beginCall` , gdy zwraca, `endCall` zwraca lub gdy wywołanie zwrotne zwraca, jeśli zostało wywołane z tego działania.</span><span class="sxs-lookup"><span data-stu-id="c1064-108">The called activity terminates when `beginCall` returns, `endCall` returns, or when the callback returns if it was called from that activity.</span></span>  
  
### <a name="asynchronous-client-without-callback"></a><span data-ttu-id="c1064-109">Klient asynchroniczny bez wywołania zwrotnego</span><span class="sxs-lookup"><span data-stu-id="c1064-109">Asynchronous Client without Callback</span></span>  
  
#### <a name="propagation-is-enabled-on-both-sides-using-http"></a><span data-ttu-id="c1064-110">Propagacja jest włączona po obu stronach, przy użyciu protokołu HTTP</span><span class="sxs-lookup"><span data-stu-id="c1064-110">Propagation is Enabled on Both Sides, using HTTP</span></span>  

 ![Klient asynchroniczny bez wywołania zwrotnego, gdzie w obu stronach jest ustawiona wartość true.](./media/asynchronous-scenarios-using-http-tcp-or-named-pipe/asynchronous-client-no-callback.gif)
  
 <span data-ttu-id="c1064-112">Jeśli `propagateActivity=true` ProcessMessage wskazuje aktywność ProcessAction do przekazania.</span><span class="sxs-lookup"><span data-stu-id="c1064-112">If `propagateActivity=true`, ProcessMessage indicates which ProcessAction activity to transfer to.</span></span>  
  
 <span data-ttu-id="c1064-113">W przypadku scenariuszy opartych na protokole HTTP ReceiveBytes jest wywoływana w pierwszej wiadomości w celu wysłania i istnieje dla okresu istnienia żądania.</span><span class="sxs-lookup"><span data-stu-id="c1064-113">For HTTP-based scenarios, ReceiveBytes is invoked on the first message to send, and exists for the lifetime of the request.</span></span>  
  
#### <a name="propagation-is-disabled-on-either-sides-using-http"></a><span data-ttu-id="c1064-114">Propagacja jest wyłączona po obu stronach, przy użyciu protokołu HTTP</span><span class="sxs-lookup"><span data-stu-id="c1064-114">Propagation is Disabled on Either Sides, using HTTP</span></span>  

 <span data-ttu-id="c1064-115">Jeśli `propagateActivity=false` po obu stronach ProcessMessage nie wskazuje, które działanie ProcessAction do przeniesienia.</span><span class="sxs-lookup"><span data-stu-id="c1064-115">If `propagateActivity=false` on either side, ProcessMessage does not indicate which ProcessAction activity to transfer to.</span></span> <span data-ttu-id="c1064-116">W związku z tym nowe tymczasowe działanie ProcessAction z nowym IDENTYFIKATORem jest wywoływana.</span><span class="sxs-lookup"><span data-stu-id="c1064-116">Therefore, a new temporary ProcessAction activity with a new ID is invoked.</span></span> <span data-ttu-id="c1064-117">Po dopasowaniu asynchronicznej odpowiedzi do żądania w kodzie ServiceModel, identyfikator działania można pobrać z kontekstu lokalnego.</span><span class="sxs-lookup"><span data-stu-id="c1064-117">When the asynchronous response is matched to the request in ServiceModel code, the Activity ID can be retrieved from the local context.</span></span> <span data-ttu-id="c1064-118">Rzeczywiste działanie ProcessAction można przenieść do tego identyfikatora.</span><span class="sxs-lookup"><span data-stu-id="c1064-118">The actual ProcessAction activity can be transferred to with that ID.</span></span>  
  
 ![Klient asynchroniczny bez wywołania zwrotnego, gdzie Propagacja jest ustawiona na wartość false po obu stronach.](./media/asynchronous-scenarios-using-http-tcp-or-named-pipe/asynchronous-scenario-propagation-disabled-either-side.gif)  

 <span data-ttu-id="c1064-120">W przypadku scenariuszy opartych na protokole HTTP ReceiveBytes jest wywoływana w pierwszej wiadomości w celu wysłania i istnieje dla okresu istnienia żądania.</span><span class="sxs-lookup"><span data-stu-id="c1064-120">For HTTP-based scenarios, ReceiveBytes is invoked on the first message to send, and exists for the lifetime of the request.</span></span>  
  
 <span data-ttu-id="c1064-121">Działanie działania procesu jest tworzone na kliencie asynchronicznym, gdy `propagateActivity=false` obiekt wywołujący lub wywoływany, a komunikat odpowiedzi nie zawiera nagłówka akcji.</span><span class="sxs-lookup"><span data-stu-id="c1064-121">A Process Action activity is created on an asynchronous client when `propagateActivity=false` at the caller or callee, and when the response message does not include an Action header.</span></span>  
  
#### <a name="propagation-is-enabled-on-both-sides-using-tcp-or-named-pipe"></a><span data-ttu-id="c1064-122">Propagacja jest włączona po obu stronach, przy użyciu protokołu TCP lub potoku nazwanego</span><span class="sxs-lookup"><span data-stu-id="c1064-122">Propagation is Enabled on Both Sides, using TCP or Named Pipe</span></span>  

 ![Klient asynchroniczny bez wywołania zwrotnego, gdzie Propagacja jest ustawiona na wartość true po obu stronach i nazwanym potoku/TCP.](./media/asynchronous-scenarios-using-http-tcp-or-named-pipe/asynchronous-scenario-propagation-enabled-using-tcp.gif)  
  
 <span data-ttu-id="c1064-124">W przypadku Named-Pipe lub opartego na protokole TCP scenariusza ReceiveBytes jest wywoływana, gdy klient zostanie otwarty i istnieje dla okresu istnienia połączenia.</span><span class="sxs-lookup"><span data-stu-id="c1064-124">For a Named-Pipe or TCP-based scenario, ReceiveBytes is invoked when the client is opened, and exists for the lifetime of the connection.</span></span>  
  
 <span data-ttu-id="c1064-125">Podobnie jak w przypadku pierwszego obrazu, jeśli `propagateActivity=true` ProcessMessage wskazuje aktywność ProcessAction do przekazania.</span><span class="sxs-lookup"><span data-stu-id="c1064-125">Similar to the first image, if `propagateActivity=true`, ProcessMessage indicates which ProcessAction activity to transfer to.</span></span>  
  
#### <a name="propagation-is-disabled-on-either-sides-using-tcp-or-named-pipe"></a><span data-ttu-id="c1064-126">Propagacja jest wyłączona po obu stronach, przy użyciu protokołu TCP lub potoku nazwanego</span><span class="sxs-lookup"><span data-stu-id="c1064-126">Propagation is Disabled on Either Sides, using TCP or Named Pipe</span></span>  

 <span data-ttu-id="c1064-127">W przypadku Named-Pipe lub opartego na protokole TCP scenariusza ReceiveBytes jest wywoływana, gdy klient zostanie otwarty i istnieje dla okresu istnienia połączenia.</span><span class="sxs-lookup"><span data-stu-id="c1064-127">For a Named-Pipe or TCP-based scenario, ReceiveBytes is invoked when the client is opened, and exists for the lifetime of the connection.</span></span>  
  
 <span data-ttu-id="c1064-128">Podobnie jak w przypadku drugiego obrazu, jeśli `propagateActivity=false` po obu stronach ProcessMessage nie wskazuje, które działanie ProcessAction ma zostać przesłane.</span><span class="sxs-lookup"><span data-stu-id="c1064-128">Similar to the second image, if `propagateActivity=false` on either side, ProcessMessage does not indicate which ProcessAction activity to transfer to.</span></span> <span data-ttu-id="c1064-129">W związku z tym nowe tymczasowe działanie ProcessAction z nowym IDENTYFIKATORem jest wywoływana.</span><span class="sxs-lookup"><span data-stu-id="c1064-129">Therefore, a new temporary ProcessAction activity with a new ID is invoked.</span></span> <span data-ttu-id="c1064-130">Po dopasowaniu asynchronicznej odpowiedzi do żądania w kodzie ServiceModel, identyfikator działania można pobrać z kontekstu lokalnego.</span><span class="sxs-lookup"><span data-stu-id="c1064-130">When the asynchronous response is matched to the request in ServiceModel code, the Activity ID can be retrieved from the local context.</span></span> <span data-ttu-id="c1064-131">Rzeczywiste działanie ProcessAction można przenieść do tego identyfikatora.</span><span class="sxs-lookup"><span data-stu-id="c1064-131">The actual ProcessAction activity can be transferred to with that ID.</span></span>  
  
 ![Klient asynchroniczny bez wywołania zwrotnego, gdzie Propagacja jest ustawiona na false po obu stronach i nazwanym potoku/TCP.](./media/asynchronous-scenarios-using-http-tcp-or-named-pipe/asynchronous-scenario-propagation-disabled-using-tcp.gif)  

### <a name="asynchronous-client-with-callback"></a><span data-ttu-id="c1064-133">Klient asynchroniczny z wywołaniem zwrotnym</span><span class="sxs-lookup"><span data-stu-id="c1064-133">Asynchronous client with Callback</span></span>  

 <span data-ttu-id="c1064-134">W tym scenariuszu dodano działania G i ", w przypadku wywołania zwrotnego i `endCall` i ich transfery w/out.</span><span class="sxs-lookup"><span data-stu-id="c1064-134">This scenario adds activities G and A’, for the callback and `endCall`, and their transfers in/out.</span></span>  
  
 <span data-ttu-id="c1064-135">W tej sekcji pokazano tylko, jak używać protokołu HTTP z `propagateActivity` = `true` .</span><span class="sxs-lookup"><span data-stu-id="c1064-135">This section only demonstrates using HTTP with `propagateActivity`=`true`.</span></span> <span data-ttu-id="c1064-136">Jednak dodatkowe działania i transfery mają zastosowanie również do innych przypadków (czyli `propagateActivity` = `false` przy użyciu protokołu TCP lub nazwanego potoka).</span><span class="sxs-lookup"><span data-stu-id="c1064-136">However, the additional activities and transfers also apply to the other cases (that is, `propagateActivity`=`false`, using TCP or Named-Pipe).</span></span>  
  
 <span data-ttu-id="c1064-137">Wywołanie zwrotne tworzy nowe działanie (G), gdy klient wywołuje kod użytkownika w celu powiadomienia, że wyniki są gotowe.</span><span class="sxs-lookup"><span data-stu-id="c1064-137">The callback creates a new activity (G) when the client calls user code to notify that results are ready.</span></span> <span data-ttu-id="c1064-138">Kod użytkownika następnie wywołuje w `endCall` ramach wywołania zwrotnego (jak pokazano na rysunku 5) lub poza wywołaniem zwrotnym (rysunek 6).</span><span class="sxs-lookup"><span data-stu-id="c1064-138">User code then calls `endCall` within the callback (as shown in Figure 5) or outside the callback (Figure 6).</span></span> <span data-ttu-id="c1064-139">Ponieważ nie jest znane, z którego działania użytkownika `endCall` jest wywoływane, to działanie jest oznaczone etykietą `A’` .</span><span class="sxs-lookup"><span data-stu-id="c1064-139">Because it is not known which user activity `endCall` is being called from, this activity is labeled `A’`.</span></span> <span data-ttu-id="c1064-140">Istnieje możliwość, że wartość "może być taka sama jak lub inna od.</span><span class="sxs-lookup"><span data-stu-id="c1064-140">It is possible that A’ can be identical to or different from A.</span></span>  
  
 ![Pokazuje klienta asynchronicznego z wywołaniem zwrotnym, endCall w wywołaniu zwrotnym.](./media/asynchronous-scenarios-using-http-tcp-or-named-pipe/asynchronous-client-callback-endcall-in-callback.gif)  

 ![Pokazuje klienta asynchronicznego z wywołaniem zwrotnym endCall poza wywołaniem zwrotnym.](./media/asynchronous-scenarios-using-http-tcp-or-named-pipe/asynchronous-client-callback-endcall-outside-callback.gif)  

### <a name="asynchronous-server-with-callback"></a><span data-ttu-id="c1064-143">Serwer asynchroniczny z wywołaniem zwrotnym</span><span class="sxs-lookup"><span data-stu-id="c1064-143">Asynchronous Server with Callback</span></span>  

 ![Pokazuje serwer asynchroniczny z wywołaniem zwrotnym.](./media/asynchronous-scenarios-using-http-tcp-or-named-pipe/asynchronous-server-callback.gif)  

 <span data-ttu-id="c1064-145">Stos kanałów wywołuje klienta po odebraniu komunikatu: ślady dla tego przetwarzania są emitowane w samym działaniu ProcessRequest.</span><span class="sxs-lookup"><span data-stu-id="c1064-145">The channel stack calls back the client on Message Receive: traces for this processing are emitted in the ProcessRequest activity itself.</span></span>  
  
## <a name="asynchronous-requestreply-with-errors"></a><span data-ttu-id="c1064-146">Asynchroniczne żądanie/odpowiedź z błędami</span><span class="sxs-lookup"><span data-stu-id="c1064-146">Asynchronous Request/Reply with Errors</span></span>  

 <span data-ttu-id="c1064-147">Błędy komunikatów o błędach są odbierane podczas `endCall` .</span><span class="sxs-lookup"><span data-stu-id="c1064-147">Fault message errors are received during `endCall`.</span></span> <span data-ttu-id="c1064-148">W przeciwnym razie działania i transfery są podobne do poprzednich scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="c1064-148">Otherwise, activities and transfers are similar to previous scenarios.</span></span>  
  
## <a name="asynchronous-one-way-with-or-without-errors"></a><span data-ttu-id="c1064-149">Asynchroniczne One-Way z błędami lub bez nich</span><span class="sxs-lookup"><span data-stu-id="c1064-149">Asynchronous One-Way with or without Errors</span></span>  

 <span data-ttu-id="c1064-150">Klient nie zwrócił odpowiedzi lub błędu.</span><span class="sxs-lookup"><span data-stu-id="c1064-150">No response or fault is returned to the client.</span></span>
