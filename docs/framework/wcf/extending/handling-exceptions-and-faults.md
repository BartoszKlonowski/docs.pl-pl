---
title: Obsługa wyjątków i błędów
ms.date: 03/30/2017
ms.assetid: a64d01c6-f221-4f58-93e5-da4e87a5682e
ms.openlocfilehash: 41ec9cc5138d6b3006d8384203a0bd7cb5aae8fa
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96265625"
---
# <a name="handling-exceptions-and-faults"></a><span data-ttu-id="ddad5-102">Obsługa wyjątków i błędów</span><span class="sxs-lookup"><span data-stu-id="ddad5-102">Handling Exceptions and Faults</span></span>

<span data-ttu-id="ddad5-103">Wyjątki są używane do komunikacji błędów lokalnie w ramach usługi lub implementacji klienta.</span><span class="sxs-lookup"><span data-stu-id="ddad5-103">Exceptions are used to communicate errors locally within the service or the client implementation.</span></span> <span data-ttu-id="ddad5-104">Z drugiej strony są używane do przekazywania błędów między granicami usług, na przykład z serwera do klienta lub na odwrót.</span><span class="sxs-lookup"><span data-stu-id="ddad5-104">Faults, on the other hand, are used to communicate errors across service boundaries, such as from the server to the client or vice versa.</span></span> <span data-ttu-id="ddad5-105">Oprócz błędów, kanały transportu często używają mechanizmów specyficznych dla transportu do przekazywania błędów na poziomie transportu.</span><span class="sxs-lookup"><span data-stu-id="ddad5-105">In addition to faults, transport channels often use transport-specific mechanisms to communicate transport-level errors.</span></span> <span data-ttu-id="ddad5-106">Na przykład transport HTTP używa kodów stanu, takich jak 404 do przekazywania nieistniejącego adresu URL punktu końcowego (nie istnieje punkt końcowy do wysłania błędu).</span><span class="sxs-lookup"><span data-stu-id="ddad5-106">For example, HTTP transport uses status codes such as 404 to communicate a non-existing endpoint URL (there is no endpoint to send back a fault).</span></span> <span data-ttu-id="ddad5-107">Ten dokument składa się z trzech sekcji, które zawierają wskazówki dotyczące niestandardowych autorów kanałów.</span><span class="sxs-lookup"><span data-stu-id="ddad5-107">This document consists of three sections that provide guidance to custom channel authors.</span></span> <span data-ttu-id="ddad5-108">W pierwszej sekcji znajdują się wskazówki dotyczące tego, kiedy i jak definiować i generować wyjątki.</span><span class="sxs-lookup"><span data-stu-id="ddad5-108">The first section provides guidance on when and how to define and throw exceptions.</span></span> <span data-ttu-id="ddad5-109">Druga sekcja zawiera wskazówki dotyczące generowania i zużywania błędów.</span><span class="sxs-lookup"><span data-stu-id="ddad5-109">The second section provides guidance around generating and consuming faults.</span></span> <span data-ttu-id="ddad5-110">Trzecia sekcja wyjaśnia, jak podać informacje o śledzeniu, aby ułatwić użytkownikowi niestandardowego kanału Rozwiązywanie problemów z uruchamianiem aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ddad5-110">The third section explains how to provide trace information to aid the user of your custom channel in troubleshooting running applications.</span></span>  
  
## <a name="exceptions"></a><span data-ttu-id="ddad5-111">Wyjątki</span><span class="sxs-lookup"><span data-stu-id="ddad5-111">Exceptions</span></span>  

 <span data-ttu-id="ddad5-112">Podczas zgłaszania wyjątku należy pamiętać o dwóch kwestiach: najpierw musi być typu, który umożliwia użytkownikom pisanie poprawnego kodu, który może reagować odpowiednio do wyjątku.</span><span class="sxs-lookup"><span data-stu-id="ddad5-112">There are two things to keep in mind when throwing an exception: First it has to be of a type that allows users to write correct code that can react appropriately to the exception.</span></span> <span data-ttu-id="ddad5-113">Po drugie należy zapewnić użytkownikowi wystarczającą ilość informacji, aby zrozumieć, co poszło źle, wpływ na awarie oraz sposób jego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="ddad5-113">Second, it has to provide enough information for the user to understand what went wrong, the failure impact, and how to fix it.</span></span> <span data-ttu-id="ddad5-114">Poniższe sekcje zawierają wskazówki dotyczące typów wyjątków i komunikatów dla kanałów Windows Communication Foundation (WCF).</span><span class="sxs-lookup"><span data-stu-id="ddad5-114">The following sections give guidance around exception types and messages for Windows Communication Foundation (WCF) channels.</span></span> <span data-ttu-id="ddad5-115">Istnieją także ogólne wskazówki dotyczące wyjątków w programie .NET w temacie Wskazówki dotyczące projektowania dla dokumentu wyjątków.</span><span class="sxs-lookup"><span data-stu-id="ddad5-115">There is also general guidance around exceptions in .NET in the Design Guidelines for Exceptions document.</span></span>  
  
### <a name="exception-types"></a><span data-ttu-id="ddad5-116">Typy wyjątków</span><span class="sxs-lookup"><span data-stu-id="ddad5-116">Exception Types</span></span>  

 <span data-ttu-id="ddad5-117">Wszystkie wyjątki zgłoszone przez kanały muszą być albo albo albo <xref:System.TimeoutException?displayProperty=nameWithType> <xref:System.ServiceModel.CommunicationException?displayProperty=nameWithType> typem pochodnym <xref:System.ServiceModel.CommunicationException> .</span><span class="sxs-lookup"><span data-stu-id="ddad5-117">All exceptions thrown by channels must be either a <xref:System.TimeoutException?displayProperty=nameWithType>, <xref:System.ServiceModel.CommunicationException?displayProperty=nameWithType>, or a type derived from <xref:System.ServiceModel.CommunicationException>.</span></span> <span data-ttu-id="ddad5-118">(Takie wyjątki <xref:System.ObjectDisposedException> mogą również być zgłaszane, ale tylko wtedy, gdy kod wywołujący nie użył kanału.</span><span class="sxs-lookup"><span data-stu-id="ddad5-118">(Exceptions such as <xref:System.ObjectDisposedException> may also be thrown, but only to indicate that the calling code has misused the channel.</span></span> <span data-ttu-id="ddad5-119">Jeśli kanał jest używany prawidłowo, musi zgłosić tylko określone wyjątki. Funkcja WCF udostępnia siedem typów wyjątków, które pochodzą z <xref:System.ServiceModel.CommunicationException> i są przeznaczone do użycia przez kanały.</span><span class="sxs-lookup"><span data-stu-id="ddad5-119">If a channel is used correctly, it must only throw the given exceptions.) WCF provides seven exception types that derive from <xref:System.ServiceModel.CommunicationException> and are designed to be used by channels.</span></span> <span data-ttu-id="ddad5-120">Istnieją inne <xref:System.ServiceModel.CommunicationException> wyjątki pochodne, które są przeznaczone do użycia przez inne części systemu.</span><span class="sxs-lookup"><span data-stu-id="ddad5-120">There are other <xref:System.ServiceModel.CommunicationException>-derived exceptions that are designed to be used by other parts of the system.</span></span> <span data-ttu-id="ddad5-121">Te typy wyjątków są następujące:</span><span class="sxs-lookup"><span data-stu-id="ddad5-121">These exception types are:</span></span>  
  
|<span data-ttu-id="ddad5-122">Typ wyjątku</span><span class="sxs-lookup"><span data-stu-id="ddad5-122">Exception Type</span></span>|<span data-ttu-id="ddad5-123">Znaczenie</span><span class="sxs-lookup"><span data-stu-id="ddad5-123">Meaning</span></span>|<span data-ttu-id="ddad5-124">Wewnętrzna zawartość wyjątku</span><span class="sxs-lookup"><span data-stu-id="ddad5-124">Inner Exception Content</span></span>|<span data-ttu-id="ddad5-125">Strategia odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="ddad5-125">Recovery Strategy</span></span>|  
|--------------------|-------------|-----------------------------|-----------------------|  
|<xref:System.ServiceModel.AddressAlreadyInUseException>|<span data-ttu-id="ddad5-126">Adres punktu końcowego określony do nasłuchiwania jest już używany.</span><span class="sxs-lookup"><span data-stu-id="ddad5-126">The endpoint address specified for listening is already in use.</span></span>|<span data-ttu-id="ddad5-127">Jeśli jest obecny, zawiera więcej szczegółowych informacji o błędzie transportu, który spowodował ten wyjątek.</span><span class="sxs-lookup"><span data-stu-id="ddad5-127">If present, provides more details about the transport error that caused this exception.</span></span> <span data-ttu-id="ddad5-128">Na przykład.</span><span class="sxs-lookup"><span data-stu-id="ddad5-128">For example.</span></span> <span data-ttu-id="ddad5-129"><xref:System.IO.PipeException>, <xref:System.Net.HttpListenerException> lub <xref:System.Net.Sockets.SocketException> .</span><span class="sxs-lookup"><span data-stu-id="ddad5-129"><xref:System.IO.PipeException>, <xref:System.Net.HttpListenerException>, or <xref:System.Net.Sockets.SocketException>.</span></span>|<span data-ttu-id="ddad5-130">Spróbuj użyć innego adresu.</span><span class="sxs-lookup"><span data-stu-id="ddad5-130">Try a different address.</span></span>|  
|<xref:System.ServiceModel.AddressAccessDeniedException>|<span data-ttu-id="ddad5-131">Proces nie ma dostępu do adresu punktu końcowego określonego do nasłuchiwania.</span><span class="sxs-lookup"><span data-stu-id="ddad5-131">The process is not allowed access to the endpoint address specified for listening.</span></span>|<span data-ttu-id="ddad5-132">Jeśli jest obecny, zawiera więcej szczegółowych informacji o błędzie transportu, który spowodował ten wyjątek.</span><span class="sxs-lookup"><span data-stu-id="ddad5-132">If present, provides more details about the transport error that caused this exception.</span></span> <span data-ttu-id="ddad5-133">Na przykład, <xref:System.IO.PipeException> lub <xref:System.Net.HttpListenerException> .</span><span class="sxs-lookup"><span data-stu-id="ddad5-133">For example, <xref:System.IO.PipeException>, or <xref:System.Net.HttpListenerException>.</span></span>|<span data-ttu-id="ddad5-134">Spróbuj użyć innych poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="ddad5-134">Try with different credentials.</span></span>|  
|<xref:System.ServiceModel.CommunicationObjectFaultedException>|<span data-ttu-id="ddad5-135"><xref:System.ServiceModel.ICommunicationObject>Używany jest stan błędu (Aby uzyskać więcej informacji, zobacz temat [Informacje o zmianach stanu](understanding-state-changes.md)).</span><span class="sxs-lookup"><span data-stu-id="ddad5-135">The <xref:System.ServiceModel.ICommunicationObject> being used is in the Faulted state (for more information, see [Understanding State Changes](understanding-state-changes.md)).</span></span> <span data-ttu-id="ddad5-136">Należy zauważyć, że gdy obiekt z wieloma oczekującymi wywołaniami przechodzi do stanu błędu, tylko jedno wywołanie zgłasza wyjątek związany z awarią, a pozostałe wywołania generują <xref:System.ServiceModel.CommunicationObjectFaultedException> .</span><span class="sxs-lookup"><span data-stu-id="ddad5-136">Note that when an object with multiple pending calls transitions to the Faulted state, only one call throws an exception that is related to the failure and the rest of the calls throw a <xref:System.ServiceModel.CommunicationObjectFaultedException>.</span></span> <span data-ttu-id="ddad5-137">Ten wyjątek jest zazwyczaj zgłaszany, ponieważ aplikacja zaobserwuje wyjątek i próbuje użyć już uszkodzonego obiektu, prawdopodobnie w wątku innym niż ten, który przechwycił oryginalny wyjątek.</span><span class="sxs-lookup"><span data-stu-id="ddad5-137">This exception is typically thrown because an application overlooks some exception and tries to use an already faulted object, possibly on a thread other than the one that caught the original exception.</span></span>|<span data-ttu-id="ddad5-138">Jeśli jest obecny, zawiera szczegółowe informacje o wyjątku wewnętrznym.</span><span class="sxs-lookup"><span data-stu-id="ddad5-138">If present provides details about the inner exception.</span></span>|<span data-ttu-id="ddad5-139">Utwórz nowy obiekt.</span><span class="sxs-lookup"><span data-stu-id="ddad5-139">Create a new object.</span></span> <span data-ttu-id="ddad5-140">Należy pamiętać, że w zależności od tego <xref:System.ServiceModel.ICommunicationObject> , co spowodowało błąd w pierwszym miejscu, może być konieczne wykonanie innych czynności wymaganych do odzyskania.</span><span class="sxs-lookup"><span data-stu-id="ddad5-140">Note that depending on what caused the <xref:System.ServiceModel.ICommunicationObject> to fault in the first place, there may be other work required to recover.</span></span>|  
|<xref:System.ServiceModel.CommunicationObjectAbortedException>|<span data-ttu-id="ddad5-141"><xref:System.ServiceModel.ICommunicationObject>Używany program został przerwany (Aby uzyskać więcej informacji, zobacz temat [Informacje o zmianach stanu](understanding-state-changes.md)).</span><span class="sxs-lookup"><span data-stu-id="ddad5-141">The <xref:System.ServiceModel.ICommunicationObject> being used has been Aborted (for more information, see [Understanding State Changes](understanding-state-changes.md)).</span></span> <span data-ttu-id="ddad5-142">Podobnie jak w <xref:System.ServiceModel.CommunicationObjectFaultedException> przypadku, ten wyjątek wskazuje, że aplikacja została wywołana dla <xref:System.ServiceModel.ICommunicationObject.Abort%2A> obiektu, prawdopodobnie z innego wątku, a obiekt nie jest już użyteczny z tego powodu.</span><span class="sxs-lookup"><span data-stu-id="ddad5-142">Similar to <xref:System.ServiceModel.CommunicationObjectFaultedException>, this exception indicates the application has called <xref:System.ServiceModel.ICommunicationObject.Abort%2A> on the object, possibly from another thread, and the object is no longer usable for that reason.</span></span>|<span data-ttu-id="ddad5-143">Jeśli jest obecny, zawiera szczegółowe informacje o wyjątku wewnętrznym.</span><span class="sxs-lookup"><span data-stu-id="ddad5-143">If present provides details about the inner exception.</span></span>|<span data-ttu-id="ddad5-144">Utwórz nowy obiekt.</span><span class="sxs-lookup"><span data-stu-id="ddad5-144">Create a new object.</span></span> <span data-ttu-id="ddad5-145">Należy pamiętać, że w zależności od tego, co spowodowało <xref:System.ServiceModel.ICommunicationObject> przerwanie działania w pierwszym miejscu, może być konieczne wykonanie innych czynności.</span><span class="sxs-lookup"><span data-stu-id="ddad5-145">Note that depending on what caused the <xref:System.ServiceModel.ICommunicationObject> to abort in the first place, there may be other work required to recover.</span></span>|  
|<xref:System.ServiceModel.EndpointNotFoundException>|<span data-ttu-id="ddad5-146">Docelowy zdalny punkt końcowy nie nasłuchuje.</span><span class="sxs-lookup"><span data-stu-id="ddad5-146">The target remote endpoint is not listening.</span></span> <span data-ttu-id="ddad5-147">Może to wynikać z nieprawidłowej części adresu punktu końcowego, nierozwiązywalny lub punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="ddad5-147">This can result from any part of the endpoint address being incorrect, irresolvable, or the endpoint being down.</span></span> <span data-ttu-id="ddad5-148">Przykłady obejmują błąd DNS, Menedżer kolejki jest niedostępny i usługa nie jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="ddad5-148">Examples include DNS error, Queue Manager not available, and service not running.</span></span>|<span data-ttu-id="ddad5-149">Wewnętrzny wyjątek zapewnia szczegóły, zazwyczaj z bazowego transportu.</span><span class="sxs-lookup"><span data-stu-id="ddad5-149">The inner exception provides details, typically from the underlying transport.</span></span>|<span data-ttu-id="ddad5-150">Spróbuj użyć innego adresu.</span><span class="sxs-lookup"><span data-stu-id="ddad5-150">Try a different address.</span></span> <span data-ttu-id="ddad5-151">Alternatywnie nadawca może poczekać chwilę i spróbować ponownie w przypadku, gdy usługa nie działa</span><span class="sxs-lookup"><span data-stu-id="ddad5-151">Alternatively, the sender may wait a while and try again in case the service was down</span></span>|  
|<xref:System.ServiceModel.ProtocolException>|<span data-ttu-id="ddad5-152">Protokoły komunikacyjne, zgodnie z opisem w zasadach punktu końcowego, są niezgodne między punktami końcowymi.</span><span class="sxs-lookup"><span data-stu-id="ddad5-152">The communication protocols, as described by the endpoint's policy, are mismatched between endpoints.</span></span> <span data-ttu-id="ddad5-153">Na przykład niezgodność typu ramki lub maksymalny rozmiar komunikatu został przekroczony.</span><span class="sxs-lookup"><span data-stu-id="ddad5-153">For example, framing content type mismatch or max message size exceeded.</span></span>|<span data-ttu-id="ddad5-154">Jeśli jest obecny, zawiera więcej informacji o konkretnym błędzie protokołu.</span><span class="sxs-lookup"><span data-stu-id="ddad5-154">If present provides more information about the specific protocol error.</span></span> <span data-ttu-id="ddad5-155">Na przykład <xref:System.ServiceModel.QuotaExceededException> jest wewnętrzny wyjątek, gdy przyczyną błędu jest przekraczanie MaxReceivedMessageSize.</span><span class="sxs-lookup"><span data-stu-id="ddad5-155">For example, <xref:System.ServiceModel.QuotaExceededException> is the inner exception when the error cause is exceeding MaxReceivedMessageSize.</span></span>|<span data-ttu-id="ddad5-156">Odzyskiwanie: Upewnij się, że nadawca i odebrane ustawienia protokołu pasują do siebie.</span><span class="sxs-lookup"><span data-stu-id="ddad5-156">Recovery: Ensure sender and received protocol settings match.</span></span> <span data-ttu-id="ddad5-157">Aby to zrobić, należy ponownie zaimportować metadane punktu końcowego usługi i użyć wygenerowanego powiązania do ponownego utworzenia kanału.</span><span class="sxs-lookup"><span data-stu-id="ddad5-157">One way to do this is to re-import the service endpoint's metadata (policy) and use the generated binding to recreate the channel.</span></span>|  
|<xref:System.ServiceModel.ServerTooBusyException>|<span data-ttu-id="ddad5-158">Zdalny punkt końcowy nasłuchuje, ale nie jest przygotowany do przetwarzania komunikatów.</span><span class="sxs-lookup"><span data-stu-id="ddad5-158">The remote endpoint is listening but is not prepared to process messages.</span></span>|<span data-ttu-id="ddad5-159">Jeśli jest obecny, wyjątek wewnętrzny zawiera szczegóły błędu protokołu SOAP lub poziomu transportu.</span><span class="sxs-lookup"><span data-stu-id="ddad5-159">If present, the inner Exception provides the SOAP fault or transport-level error details.</span></span>|<span data-ttu-id="ddad5-160">Odzyskiwanie: Poczekaj i spróbuj ponownie wykonać operację później.</span><span class="sxs-lookup"><span data-stu-id="ddad5-160">Recovery: Wait and retry the operation later.</span></span>|  
|<xref:System.TimeoutException>|<span data-ttu-id="ddad5-161">Nie można ukończyć operacji przed upływem limitu czasu.</span><span class="sxs-lookup"><span data-stu-id="ddad5-161">The operation failed to complete within the timeout period.</span></span>|<span data-ttu-id="ddad5-162">Może podawać szczegółowe informacje o limicie czasu.</span><span class="sxs-lookup"><span data-stu-id="ddad5-162">May provide details about the timeout.</span></span>|<span data-ttu-id="ddad5-163">Poczekaj, a następnie spróbuj ponownie wykonać operację później.</span><span class="sxs-lookup"><span data-stu-id="ddad5-163">Wait and retry the operation later.</span></span>|  
  
 <span data-ttu-id="ddad5-164">Zdefiniuj nowy typ wyjątku tylko wtedy, gdy ten typ odnosi się do konkretnej strategii odzyskiwania innej niż wszystkie istniejące typy wyjątków.</span><span class="sxs-lookup"><span data-stu-id="ddad5-164">Define a new exception type only if that type corresponds to a specific recovery strategy different from all of the existing exception types.</span></span> <span data-ttu-id="ddad5-165">Jeśli zdefiniujesz nowy typ wyjątku, musi on pochodzić z <xref:System.ServiceModel.CommunicationException> lub jednej z jej klas pochodnych.</span><span class="sxs-lookup"><span data-stu-id="ddad5-165">If you do define a new exception type, it must derive from <xref:System.ServiceModel.CommunicationException> or one of its derived classes.</span></span>  
  
### <a name="exception-messages"></a><span data-ttu-id="ddad5-166">Komunikaty o wyjątkach</span><span class="sxs-lookup"><span data-stu-id="ddad5-166">Exception Messages</span></span>  

 <span data-ttu-id="ddad5-167">Komunikaty o wyjątkach są wskazywane przez użytkownika, który nie jest programem, dlatego powinny udostępnić wystarczające informacje, aby pomóc użytkownikom zrozumieć i rozwiązać problem.</span><span class="sxs-lookup"><span data-stu-id="ddad5-167">Exception messages are targeted at the user not the program so they should provide sufficient information to help the user understand and solve the problem.</span></span> <span data-ttu-id="ddad5-168">Trzy podstawowe części dobrego komunikatu o wyjątku:</span><span class="sxs-lookup"><span data-stu-id="ddad5-168">The three essential parts of a good exception message are:</span></span>  
  
 <span data-ttu-id="ddad5-169">co miało miejsce.</span><span class="sxs-lookup"><span data-stu-id="ddad5-169">What happened.</span></span> <span data-ttu-id="ddad5-170">Podaj jasny opis problemu przy użyciu terminów związanych ze środowiskami użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ddad5-170">Provide a clear description of the problem using terms that relate to the user's experience.</span></span> <span data-ttu-id="ddad5-171">Na przykład komunikat o nieprawidłowym wyjątku to "Nieprawidłowa sekcja konfiguracji".</span><span class="sxs-lookup"><span data-stu-id="ddad5-171">For example, a bad exception message would be "Invalid configuration section".</span></span> <span data-ttu-id="ddad5-172">Spowoduje to pozostawienie użytkownika, którego sekcja konfiguracji jest nieprawidłowa i dlaczego jest niepoprawna.</span><span class="sxs-lookup"><span data-stu-id="ddad5-172">This leaves the user wondering which configuration section is incorrect and why it is incorrect.</span></span> <span data-ttu-id="ddad5-173">Ulepszony komunikat to "Nieprawidłowa sekcja konfiguracji \<customBinding> ".</span><span class="sxs-lookup"><span data-stu-id="ddad5-173">An improved message would be "Invalid configuration section \<customBinding>".</span></span> <span data-ttu-id="ddad5-174">Jeszcze lepszym komunikatem może być "nie można dodać transportu o nazwie" Moje Transporting "do powiązania o nazwie Moje powiązanie, ponieważ powiązanie ma już transport o nazwie" transport ".</span><span class="sxs-lookup"><span data-stu-id="ddad5-174">An even better message would be "Cannot add the transport named myTransport to the binding named myBinding because the binding already has a transport named myTransport".</span></span> <span data-ttu-id="ddad5-175">Jest to bardzo konkretny komunikat z użyciem warunków i nazw, które użytkownik może łatwo zidentyfikować w pliku konfiguracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ddad5-175">This is a very specific message using terms and names that the user can easily identify in the application's configuration file.</span></span> <span data-ttu-id="ddad5-176">Jednak nadal brakuje kilku kluczowych składników.</span><span class="sxs-lookup"><span data-stu-id="ddad5-176">However, there are still a few key components missing.</span></span>  
  
 <span data-ttu-id="ddad5-177">Istotność błędu.</span><span class="sxs-lookup"><span data-stu-id="ddad5-177">The significance of the error.</span></span> <span data-ttu-id="ddad5-178">Chyba że komunikat wskazuje, że błąd oznacza, użytkownik może się zastanawiać, czy jest to błąd krytyczny czy można go zignorować.</span><span class="sxs-lookup"><span data-stu-id="ddad5-178">Unless the message states clearly what the error means, the user is likely to wonder whether it is a fatal error or if it can be ignored.</span></span> <span data-ttu-id="ddad5-179">Ogólnie rzecz biorąc komunikaty powinny prowadzić do znaczenia lub znaczenia błędu.</span><span class="sxs-lookup"><span data-stu-id="ddad5-179">In general, messages should lead with the meaning or significance of the error.</span></span> <span data-ttu-id="ddad5-180">Aby ulepszyć poprzedni przykład, może to być komunikat "nie można otworzyć ServiceHost z powodu błędu konfiguracji: nie można dodać transportu o nazwie" Moje Transporting "do powiązania o nazwie Moje powiązanie, ponieważ powiązanie ma już transport o nazwie" transport ".</span><span class="sxs-lookup"><span data-stu-id="ddad5-180">To improve the previous example, the message could be "ServiceHost failed to Open due to a configuration error: Cannot add the transport named myTransport to the binding named myBinding because the binding already has a transport named myTransport".</span></span>  
  
 <span data-ttu-id="ddad5-181">Jak użytkownik powinien rozwiązać problem.</span><span class="sxs-lookup"><span data-stu-id="ddad5-181">How the user should correct the problem.</span></span> <span data-ttu-id="ddad5-182">Najważniejszym elementem wiadomości jest pomoc w rozwiązaniu problemu.</span><span class="sxs-lookup"><span data-stu-id="ddad5-182">The most important part of the message is helping the user fix the problem.</span></span> <span data-ttu-id="ddad5-183">Komunikat powinien zawierać wskazówki lub wskazówki dotyczące tego, co należy sprawdzić lub naprawić, aby rozwiązać problem.</span><span class="sxs-lookup"><span data-stu-id="ddad5-183">The message should include some guidance or hints about what to check or fix to remedy the problem.</span></span> <span data-ttu-id="ddad5-184">Na przykład: "nie można otworzyć ServiceHost z powodu błędu konfiguracji. nie można dodać transportu o nazwie" Moja Transporting "do powiązania o nazwie Moje powiązanie, ponieważ powiązanie ma już transport o nazwie" Moje transport ".</span><span class="sxs-lookup"><span data-stu-id="ddad5-184">For example, "ServiceHost failed to Open due to a configuration error: Cannot add the transport named myTransport to the binding named myBinding because the binding already has a transport named myTransport.</span></span> <span data-ttu-id="ddad5-185">Upewnij się, że w powiązaniu istnieje tylko jeden transport.</span><span class="sxs-lookup"><span data-stu-id="ddad5-185">Please ensure there is only one transport in the binding".</span></span>  
  
## <a name="communicating-faults"></a><span data-ttu-id="ddad5-186">Komunikacja błędów</span><span class="sxs-lookup"><span data-stu-id="ddad5-186">Communicating Faults</span></span>  

 <span data-ttu-id="ddad5-187">Protokoły SOAP 1,1 i SOAP 1,2 definiują określoną strukturę błędów.</span><span class="sxs-lookup"><span data-stu-id="ddad5-187">SOAP 1.1 and SOAP 1.2 both define a specific structure for faults.</span></span> <span data-ttu-id="ddad5-188">Istnieją pewne różnice między tymi dwiema specyfikacjami, ale ogólnie rzecz biorąc, wiadomości i typy MessageFault są używane do tworzenia i korzystania z błędów.</span><span class="sxs-lookup"><span data-stu-id="ddad5-188">There are some differences between the two specifications but in general, the Message and MessageFault types are used to create and consume faults.</span></span>  
  
 <span data-ttu-id="ddad5-189">![Obsługa wyjątków i błędów](./media/wcfc-soap1-1andsoap1-2faultcomparisonc.gif "wcfc_SOAP1-1AndSOAP1-2FaultComparisonc")</span><span class="sxs-lookup"><span data-stu-id="ddad5-189">![Handling exceptions and faults](./media/wcfc-soap1-1andsoap1-2faultcomparisonc.gif "wcfc_SOAP1-1AndSOAP1-2FaultComparisonc")</span></span>  
<span data-ttu-id="ddad5-190">Błąd protokołu SOAP 1,2 (z lewej) i błąd protokołu SOAP 1,1 (prawo).</span><span class="sxs-lookup"><span data-stu-id="ddad5-190">SOAP 1.2 Fault (left) and SOAP 1.1 Fault (right).</span></span> <span data-ttu-id="ddad5-191">Należy pamiętać, że w protokole SOAP 1,1 tylko element Fault ma kwalifikowaną przestrzeń nazw.</span><span class="sxs-lookup"><span data-stu-id="ddad5-191">Note that in SOAP 1.1 only the Fault element is namespace qualified.</span></span>  
  
 <span data-ttu-id="ddad5-192">Protokół SOAP definiuje komunikat o błędzie jako komunikat, który zawiera tylko element błędu (element, którego nazwa jest `<env:Fault>` ) jako element podrzędny `<env:Body>` .</span><span class="sxs-lookup"><span data-stu-id="ddad5-192">SOAP defines a fault message as a message that contains only a fault element (an element whose name is `<env:Fault>`) as a child of `<env:Body>`.</span></span> <span data-ttu-id="ddad5-193">Zawartość elementu Fault różni się nieco od protokołu SOAP 1,1 i protokołu SOAP 1,2, jak pokazano na rysunku 1.</span><span class="sxs-lookup"><span data-stu-id="ddad5-193">The contents of the fault element differ slightly between SOAP 1.1 and SOAP 1.2 as shown in figure 1.</span></span> <span data-ttu-id="ddad5-194">Jednak <xref:System.ServiceModel.Channels.MessageFault?displayProperty=nameWithType> Klasa normalizuje te różnice w jednym modelu obiektów:</span><span class="sxs-lookup"><span data-stu-id="ddad5-194">However, the <xref:System.ServiceModel.Channels.MessageFault?displayProperty=nameWithType> class normalizes these differences into one object model:</span></span>  
  
```csharp
public abstract class MessageFault  
{  
    protected MessageFault();  
  
    public virtual string Actor { get; }  
    public virtual string Node { get; }  
    public static string DefaultAction { get; }  
    public abstract FaultCode Code { get; }  
    public abstract bool HasDetail { get; }  
    public abstract FaultReason Reason { get; }  
  
    public T GetDetail<T>();  
    public T GetDetail<T>( XmlObjectSerializer serializer);  
    public System.Xml.XmlDictionaryReader GetReaderAtDetailContents();  
  
    // other methods omitted  
}  
```  
  
 <span data-ttu-id="ddad5-195">`Code`Właściwość odnosi się do `env:Code` (lub `faultCode` w SOAP 1,1) i identyfikuje typ błędu.</span><span class="sxs-lookup"><span data-stu-id="ddad5-195">The `Code` property corresponds to the `env:Code` (or `faultCode` in SOAP 1.1) and identifies the type of the fault.</span></span> <span data-ttu-id="ddad5-196">Protokół SOAP 1,2 definiuje pięć wartości dopuszczalnych dla `faultCode` (na przykład nadawcy i odbiorcę) i definiuje `Subcode` element, który może zawierać dowolną wartość kodu.</span><span class="sxs-lookup"><span data-stu-id="ddad5-196">SOAP 1.2 defines five allowable values for `faultCode` (for example, Sender and Receiver) and defines a `Subcode` element which can contain any subcode value.</span></span> <span data-ttu-id="ddad5-197">(Patrz [Specyfikacja protokołu SOAP 1,2](https://www.w3.org/TR/soap12-part1/#tabsoapfaultcodes) , aby uzyskać listę dozwolonych kodów błędów i ich znaczenie). Protokół SOAP 1,1 ma nieco inny mechanizm: definiuje cztery `faultCode` wartości (na przykład klienta i serwera), które można rozszerzyć przez zdefiniowanie zupełnie nowych lub przy użyciu notacji kropkowej w celu utworzenia bardziej szczegółowych informacji `faultCodes` na przykład klienta. uwierzytelnianie.</span><span class="sxs-lookup"><span data-stu-id="ddad5-197">(See the [SOAP 1.2 specification](https://www.w3.org/TR/soap12-part1/#tabsoapfaultcodes) for the list of allowable fault codes and their meaning.) SOAP 1.1 has a slightly different mechanism: It defines four `faultCode` values (for example, Client and Server) that can be extended either by defining entirely new ones or by using the dot notation to create more specific `faultCodes`, for example, Client.Authentication.</span></span>  
  
 <span data-ttu-id="ddad5-198">W przypadku używania MessageFault z błędami programu FaultCode.Name i FaultCode. Namespace mapuje do nazwy i przestrzeni nazw protokołu SOAP 1,2 `env:Code` lub soap 1,1 `faultCode` .</span><span class="sxs-lookup"><span data-stu-id="ddad5-198">When you use MessageFault to program faults, the FaultCode.Name and FaultCode.Namespace maps to the name and namespace of the SOAP 1.2 `env:Code` or the SOAP 1.1 `faultCode`.</span></span> <span data-ttu-id="ddad5-199">FaultCode. Subcode mapuje do `env:Subcode` protokołu soap 1,2 i ma wartość null dla protokołu soap 1,1.</span><span class="sxs-lookup"><span data-stu-id="ddad5-199">The FaultCode.SubCode maps to `env:Subcode` for SOAP 1.2 and is null for SOAP 1.1.</span></span>  
  
 <span data-ttu-id="ddad5-200">Należy utworzyć nowe podkody błędów (lub nowe kody błędów w przypadku korzystania z protokołu SOAP 1,1), jeśli jest to interesujące do programistycznego odróżnienia błędu.</span><span class="sxs-lookup"><span data-stu-id="ddad5-200">You should create new fault subcodes (or new fault codes if using SOAP 1.1) if it is interesting to programmatically distinguish a fault.</span></span> <span data-ttu-id="ddad5-201">Jest to analogiczne do tworzenia nowego typu wyjątku.</span><span class="sxs-lookup"><span data-stu-id="ddad5-201">This is analogous to creating a new exception type.</span></span> <span data-ttu-id="ddad5-202">Należy unikać używania notacji kropki z kodami błędów SOAP 1,1.</span><span class="sxs-lookup"><span data-stu-id="ddad5-202">You should avoid using the dot notation with SOAP 1.1 fault codes.</span></span> <span data-ttu-id="ddad5-203">( [Profil usługi WS-I Basic](http://www.ws-i.org/Profiles/BasicProfile-1.1-2004-08-24.html#SOAP_Custom_Fault_Codes) odradza również korzystanie z notacji kropki kodu błędu).</span><span class="sxs-lookup"><span data-stu-id="ddad5-203">(The [WS-I Basic Profile](http://www.ws-i.org/Profiles/BasicProfile-1.1-2004-08-24.html#SOAP_Custom_Fault_Codes) also discourages the use of the fault code dot notation.)</span></span>  
  
```csharp
public class FaultCode  
{  
    public FaultCode(string name);  
    public FaultCode(string name, FaultCode subCode);  
    public FaultCode(string name, string ns);  
    public FaultCode(string name, string ns, FaultCode subCode);  
  
    public bool IsPredefinedFault { get; }  
    public bool IsReceiverFault { get; }  
    public bool IsSenderFault { get; }  
    public string Name { get; }  
    public string Namespace { get; }  
    public FaultCode SubCode { get; }  
  
//  methods omitted  
  
}  
```  
  
 <span data-ttu-id="ddad5-204">`Reason`Właściwość odnosi się do `env:Reason` (lub `faultString` w protokole SOAP 1,1) opis nieprawidłowego stanu błędu analogicznie do komunikatu o wyjątku.</span><span class="sxs-lookup"><span data-stu-id="ddad5-204">The `Reason` property corresponds to the `env:Reason` (or `faultString` in SOAP 1.1) a human-readable description of the error condition analogous to an exception's message.</span></span> <span data-ttu-id="ddad5-205">`FaultReason`Klasa (i SOAP `env:Reason/faultString` ) ma wbudowaną obsługę mającą wiele tłumaczeń w interesie globalizacji.</span><span class="sxs-lookup"><span data-stu-id="ddad5-205">The `FaultReason` class (and SOAP `env:Reason/faultString`) has built-in support for having multiple translations in the interest of globalization.</span></span>  
  
```csharp
public class FaultReason  
{  
    public FaultReason(FaultReasonText translation);  
    public FaultReason(IEnumerable<FaultReasonText> translations);  
    public FaultReason(string text);  
  
    public SynchronizedReadOnlyCollection<FaultReasonText> Translations
    {
       get;
    }  
  
 }  
```  
  
 <span data-ttu-id="ddad5-206">Zawartość szczegółów błędu jest narażona na MessageFault przy użyciu różnych metod, takich jak `GetDetail` \<T> i `GetReaderAtDetailContents` ().</span><span class="sxs-lookup"><span data-stu-id="ddad5-206">The fault detail contents are exposed on MessageFault using various methods including the `GetDetail`\<T> and `GetReaderAtDetailContents`().</span></span> <span data-ttu-id="ddad5-207">Szczegóły błędu to nieprzezroczysty element służący do przeprowadzenia dodatkowych szczegółów dotyczących błędu.</span><span class="sxs-lookup"><span data-stu-id="ddad5-207">The fault detail is an opaque element for carrying additional detail about the fault.</span></span> <span data-ttu-id="ddad5-208">Jest to przydatne, jeśli istnieje pewne szczegółowe informacje strukturalne, które chcesz przenieść wraz z błędem.</span><span class="sxs-lookup"><span data-stu-id="ddad5-208">This is useful if there is some arbitrary structured detail that you want to carry with the fault.</span></span>  
  
### <a name="generating-faults"></a><span data-ttu-id="ddad5-209">Generowanie błędów</span><span class="sxs-lookup"><span data-stu-id="ddad5-209">Generating Faults</span></span>  

 <span data-ttu-id="ddad5-210">W tej sekcji opisano proces generowania błędu w odpowiedzi na warunek błędu wykryty w kanale lub we właściwości komunikatu utworzonej przez kanał.</span><span class="sxs-lookup"><span data-stu-id="ddad5-210">This section explains the process of generating a fault in response to an error condition detected in a channel or in a message property created by the channel.</span></span> <span data-ttu-id="ddad5-211">Typowy przykład wysyła błąd w odpowiedzi na komunikat żądania, który zawiera nieprawidłowe dane.</span><span class="sxs-lookup"><span data-stu-id="ddad5-211">A typical example is sending back a fault in response to a request message that contains invalid data.</span></span>  
  
 <span data-ttu-id="ddad5-212">Podczas generowania błędu kanał niestandardowy nie powinien wysyłać błędu bezpośrednio, raczej powinien zgłosić wyjątek i pozwolić warstwie powyżej zdecydować, czy skonwertować ten wyjątek na błąd i jak go wysłać.</span><span class="sxs-lookup"><span data-stu-id="ddad5-212">When generating a fault, the custom channel should not send the fault directly, rather, it should throw an exception and let the layer above decide whether to convert that exception to a fault and how to send it.</span></span> <span data-ttu-id="ddad5-213">Aby pomóc w tej konwersji, kanał powinien zapewnić `FaultConverter` implementację, która może przekonwertować wyjątek zgłoszony przez niestandardowy kanał na odpowiedni błąd.</span><span class="sxs-lookup"><span data-stu-id="ddad5-213">To aid in this conversion, the channel should provide a `FaultConverter` implementation that can convert the exception thrown by the custom channel to the appropriate fault.</span></span> <span data-ttu-id="ddad5-214">`FaultConverter` jest zdefiniowany jako:</span><span class="sxs-lookup"><span data-stu-id="ddad5-214">`FaultConverter` is defined as:</span></span>  
  
```csharp
public class FaultConverter  
{  
    public static FaultConverter GetDefaultFaultConverter(  
                                   MessageVersion version);  
    protected abstract bool OnTryCreateFaultMessage(  
                                   Exception exception,
                                   out Message message);  
    public bool TryCreateFaultMessage(  
                                   Exception exception,
                                   out Message message);  
}  
```  
  
 <span data-ttu-id="ddad5-215">Każdy kanał generujący błędy niestandardowe musi implementować `FaultConverter` i zwracać z wywołania do `GetProperty<FaultConverter>` .</span><span class="sxs-lookup"><span data-stu-id="ddad5-215">Each channel that generates custom faults must implement `FaultConverter` and return it from a call to `GetProperty<FaultConverter>`.</span></span> <span data-ttu-id="ddad5-216">Implementacja niestandardowa `OnTryCreateFaultMessage` musi wykonać konwersję wyjątku na błąd lub delegata do wewnętrznego kanału `FaultConverter` .</span><span class="sxs-lookup"><span data-stu-id="ddad5-216">The custom `OnTryCreateFaultMessage` implementation must either convert the exception to a fault or delegate to the inner channel's `FaultConverter`.</span></span> <span data-ttu-id="ddad5-217">Jeśli kanał jest transportem, należy przekonwertować wyjątek lub obiekt delegowany do kodera `FaultConverter` lub domyślnego ustawienia usługi `FaultConverter` WCF.</span><span class="sxs-lookup"><span data-stu-id="ddad5-217">If the channel is a transport it must either convert the exception or delegate to the encoder's `FaultConverter` or the default `FaultConverter` provided in WCF .</span></span> <span data-ttu-id="ddad5-218">Domyślnie `FaultConverter` konwertuje błędy odpowiadające komunikatom o błędach określonych przez WS-Addressing i SOAP.</span><span class="sxs-lookup"><span data-stu-id="ddad5-218">The default `FaultConverter` converts errors corresponding to fault messages specified by WS-Addressing and SOAP.</span></span> <span data-ttu-id="ddad5-219">Oto przykładowa `OnTryCreateFaultMessage` implementacja.</span><span class="sxs-lookup"><span data-stu-id="ddad5-219">Here is an example `OnTryCreateFaultMessage` implementation.</span></span>  
  
```csharp
public override bool OnTryCreateFaultMessage(Exception exception,
                                             out Message message)  
{  
    if (exception is ...)  
    {  
        message = ...;  
        return true;  
    }  
  
#if IMPLEMENTING_TRANSPORT_CHANNEL  
    FaultConverter encoderConverter =
                    this.encoder.GetProperty<FaultConverter>();  
    if ((encoderConverter != null) &&
        (encoderConverter.TryCreateFaultMessage(  
         exception, out message)))  
    {  
        return true;  
    }  
  
    FaultConverter defaultConverter =
                   FaultConverter.GetDefaultFaultConverter(  
                   this.channel.messageVersion);  
    return defaultConverter.TryCreateFaultMessage(  
                   exception,
                   out message);  
#else  
    FaultConverter inner =
                   this.innerChannel.GetProperty<FaultConverter>();  
    if (inner != null)  
    {  
        return inner.TryCreateFaultMessage(exception, out message);  
    }  
    else  
    {  
        message = null;  
        return false;  
    }  
#endif  
}  
```  
  
 <span data-ttu-id="ddad5-220">Implikacje tego wzorca polega na tym, że wyjątki zgłaszane między warstwami dla warunków błędów, które wymagają błędów, muszą zawierać wystarczające informacje dla odpowiedniego generatora błędów w celu utworzenia poprawnego błędu.</span><span class="sxs-lookup"><span data-stu-id="ddad5-220">An implication of this pattern is that exceptions thrown between layers for error conditions that require faults must contain enough information for the corresponding fault generator to create the correct fault.</span></span> <span data-ttu-id="ddad5-221">Jako autor niestandardowego kanału możesz zdefiniować typy wyjątków odpowiadające różnym warunkom błędów, jeśli takie wyjątki jeszcze nie istnieją.</span><span class="sxs-lookup"><span data-stu-id="ddad5-221">As a custom channel author, you may define exception types that correspond to different fault conditions if such exceptions do not already exist.</span></span> <span data-ttu-id="ddad5-222">Należy zauważyć, że wyjątki, które przechodzą warstwy kanałów, powinny przekazywać warunek błędu, a nie nieprzezroczyste dane błędów.</span><span class="sxs-lookup"><span data-stu-id="ddad5-222">Note that exceptions traversing channel layers should communicate the error condition rather than opaque fault data.</span></span>  
  
### <a name="fault-categories"></a><span data-ttu-id="ddad5-223">Kategorie błędów</span><span class="sxs-lookup"><span data-stu-id="ddad5-223">Fault Categories</span></span>  

 <span data-ttu-id="ddad5-224">Zazwyczaj istnieją trzy kategorie błędów:</span><span class="sxs-lookup"><span data-stu-id="ddad5-224">There are generally three categories of faults:</span></span>  
  
1. <span data-ttu-id="ddad5-225">Błędy, które są rozpowszechnione w całym stosie.</span><span class="sxs-lookup"><span data-stu-id="ddad5-225">Faults that are pervasive throughout the entire stack.</span></span> <span data-ttu-id="ddad5-226">Te błędy można napotkać w dowolnej warstwie stosu kanału, na przykład InvalidCardinalityAddressingException.</span><span class="sxs-lookup"><span data-stu-id="ddad5-226">These faults could be encountered at any layer in the channel stack, for example InvalidCardinalityAddressingException.</span></span>  
  
2. <span data-ttu-id="ddad5-227">Błędy, które mogą wystąpić w dowolnym miejscu powyżej pewnej warstwy na stosie, na przykład niektóre błędy odnoszące się do transakcji przepływu lub do ról zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="ddad5-227">Faults that can be encountered anywhere above a certain layer in the stack for example some errors that pertain to a flowed transaction or to security roles.</span></span>  
  
3. <span data-ttu-id="ddad5-228">Błędy, które są kierowane do pojedynczej warstwy w stosie, na przykład błędy, takie jak błędne numery sekwencyjne WS-RM.</span><span class="sxs-lookup"><span data-stu-id="ddad5-228">Faults that are directed at a single layer in the stack, for example errors like WS-RM sequence number faults.</span></span>  
  
 <span data-ttu-id="ddad5-229">Kategoria 1.</span><span class="sxs-lookup"><span data-stu-id="ddad5-229">Category 1.</span></span> <span data-ttu-id="ddad5-230">Błędy są zwykle WS-Addressing i błędów SOAP.</span><span class="sxs-lookup"><span data-stu-id="ddad5-230">Faults are generally WS-Addressing and SOAP faults.</span></span> <span data-ttu-id="ddad5-231">Klasa bazowa `FaultConverter` dostarczana przez funkcję WCF konwertuje błędy odpowiadające komunikatom o błędach określonych przez WS-Addressing i SOAP, dzięki czemu nie trzeba obsługiwać konwersji tych wyjątków samodzielnie.</span><span class="sxs-lookup"><span data-stu-id="ddad5-231">The base `FaultConverter` class provided by WCF converts errors corresponding to fault messages specified by WS-Addressing and SOAP so you do not have to handle conversion of these exceptions yourself.</span></span>  
  
 <span data-ttu-id="ddad5-232">Kategoria 2.</span><span class="sxs-lookup"><span data-stu-id="ddad5-232">Category 2.</span></span> <span data-ttu-id="ddad5-233">Błędy występują, gdy warstwa dodaje właściwość do wiadomości, która nie korzysta całkowicie z informacji o komunikatach odnoszących się do tej warstwy.</span><span class="sxs-lookup"><span data-stu-id="ddad5-233">Faults occur when a layer adds a property to the message that does not completely consume message information that pertains to that layer.</span></span> <span data-ttu-id="ddad5-234">Błędy mogą zostać wykryte później, gdy wyższa warstwa będzie pytać Właściwość komunikatu o dalsze przetwarzanie informacji o komunikatach.</span><span class="sxs-lookup"><span data-stu-id="ddad5-234">Errors may be detected later when a higher layer asks the message property to process message information further.</span></span> <span data-ttu-id="ddad5-235">Takie kanały powinny implementować `GetProperty` określony wcześniej, aby umożliwić wyższej warstwie wysłanie poprawnego błędu.</span><span class="sxs-lookup"><span data-stu-id="ddad5-235">Such channels should implement the `GetProperty` specified previously to enable the higher layer to send back the correct fault.</span></span> <span data-ttu-id="ddad5-236">Przykładem jest TransactionMessageProperty.</span><span class="sxs-lookup"><span data-stu-id="ddad5-236">An example of this is the TransactionMessageProperty.</span></span> <span data-ttu-id="ddad5-237">Ta właściwość jest dodawana do komunikatu bez pełnej weryfikacji wszystkich danych w nagłówku (może to wiązać się z kontaktem z koordynatorem transakcji rozproszonych (DTC).</span><span class="sxs-lookup"><span data-stu-id="ddad5-237">This property is added to the message without fully validating all the data in the header (doing so may involve contacting the distributed transaction coordinator (DTC).</span></span>  
  
 <span data-ttu-id="ddad5-238">Kategoria 3.</span><span class="sxs-lookup"><span data-stu-id="ddad5-238">Category 3.</span></span> <span data-ttu-id="ddad5-239">Błędy są generowane i wysyłane przez pojedynczą warstwę w procesorze.</span><span class="sxs-lookup"><span data-stu-id="ddad5-239">Faults are only generated and sent by a single layer in the processor.</span></span> <span data-ttu-id="ddad5-240">W związku z tym wszystkie wyjątki są zawarte w warstwie.</span><span class="sxs-lookup"><span data-stu-id="ddad5-240">Therefore all the exceptions are contained within the layer.</span></span> <span data-ttu-id="ddad5-241">Aby zwiększyć spójność między kanałami i ułatwić konserwację, kanał niestandardowy powinien używać określonego wcześniej wzorca do generowania komunikatów o błędach nawet w przypadku błędów wewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="ddad5-241">To improve consistency among channels and ease maintenance, your custom channel should use the pattern specified previously to generate fault messages even for internal faults.</span></span>  
  
### <a name="interpreting-received-faults"></a><span data-ttu-id="ddad5-242">Interpretowanie odebranych błędów</span><span class="sxs-lookup"><span data-stu-id="ddad5-242">Interpreting Received Faults</span></span>  

 <span data-ttu-id="ddad5-243">Ta sekcja zawiera wskazówki dotyczące generowania odpowiedniego wyjątku podczas otrzymywania komunikatu o błędzie.</span><span class="sxs-lookup"><span data-stu-id="ddad5-243">This section provides guidance for generating the appropriate exception when receiving a fault message.</span></span> <span data-ttu-id="ddad5-244">Drzewo decyzyjne służące do przetwarzania komunikatów w każdej warstwie stosu jest następujące:</span><span class="sxs-lookup"><span data-stu-id="ddad5-244">The decision tree for processing a message at every layer in the stack is as follows:</span></span>  
  
1. <span data-ttu-id="ddad5-245">Jeśli warstwa traktuje komunikat jako nieprawidłowy, warstwa powinna wykonać przetwarzanie "nieprawidłowy komunikat".</span><span class="sxs-lookup"><span data-stu-id="ddad5-245">If the layer considers the message to be invalid, the layer should do its 'invalid message' processing.</span></span> <span data-ttu-id="ddad5-246">Takie przetwarzanie jest specyficzne dla warstwy, ale może obejmować porzucanie komunikatu, śledzenie lub zgłaszanie wyjątku, który jest konwertowany na błąd.</span><span class="sxs-lookup"><span data-stu-id="ddad5-246">Such processing is specific to the layer but could include dropping the message, tracing, or throwing an exception that gets converted to a fault.</span></span> <span data-ttu-id="ddad5-247">Przykłady obejmują zabezpieczenia otrzymujące komunikat, który nie jest prawidłowo zabezpieczony lub Menedżer zasobów otrzymuje komunikat z nieprawidłowym numerem sekwencyjnym.</span><span class="sxs-lookup"><span data-stu-id="ddad5-247">Examples include security receiving a message that is not secured properly, or RM receiving a message with a bad sequence number.</span></span>  
  
2. <span data-ttu-id="ddad5-248">W przeciwnym razie, jeśli komunikat jest komunikatem o błędzie, który jest stosowany w odróżnieniu od warstwy, a komunikat nie ma znaczenia poza interakcją warstwy, warstwa powinna obsłużyć warunek błędu.</span><span class="sxs-lookup"><span data-stu-id="ddad5-248">Otherwise, if the message is a fault message that applies specifically to the layer, and the message is not meaningful outside the layer's interaction, the layer should handle the error condition.</span></span> <span data-ttu-id="ddad5-249">Przykładem jest to, że sekwencja RM odrzuciła błąd, który jest bez względu na warstwy powyżej kanału RM i który oznacza błąd kanału RM i wyrzucanie z oczekujących operacji.</span><span class="sxs-lookup"><span data-stu-id="ddad5-249">An example of this is an RM Sequence Refused fault that is meaningless to layers above the RM channel and that implies faulting the RM channel and throwing from pending operations.</span></span>  
  
3. <span data-ttu-id="ddad5-250">W przeciwnym razie komunikat powinien zostać zwrócony z żądania () lub Receive ().</span><span class="sxs-lookup"><span data-stu-id="ddad5-250">Otherwise, the message should be returned from Request() or Receive().</span></span> <span data-ttu-id="ddad5-251">Obejmuje to przypadki, w których warstwa rozpoznaje błąd, ale tylko wskazuje, że żądanie nie powiodło się i nie implikuje błędu kanału i zostanie wyrzucane z oczekujących operacji.</span><span class="sxs-lookup"><span data-stu-id="ddad5-251">This includes cases where the layer recognizes the fault, but the fault just indicates that a request failed and does not imply faulting the channel and throwing from pending operations.</span></span> <span data-ttu-id="ddad5-252">Aby poprawić użyteczność w takim przypadku, warstwa powinna zaimplementować `GetProperty<FaultConverter>` i zwrócić `FaultConverter` klasę pochodną, która może skonwertować błąd na wyjątek przez zastąpienie `OnTryCreateException` .</span><span class="sxs-lookup"><span data-stu-id="ddad5-252">To improve usability in such a case, the layer should implement `GetProperty<FaultConverter>` and return a `FaultConverter` derived class that can convert the fault to an exception by overriding `OnTryCreateException`.</span></span>  
  
 <span data-ttu-id="ddad5-253">Poniższy model obiektów obsługuje konwertowanie komunikatów na wyjątki:</span><span class="sxs-lookup"><span data-stu-id="ddad5-253">The following object model supports converting messages to exceptions:</span></span>  
  
```csharp
public class FaultConverter  
{  
    public static FaultConverter GetDefaultFaultConverter(  
                                  MessageVersion version);  
    protected abstract bool OnTryCreateException(  
                                 Message message,
                                 MessageFault fault,
                                 out Exception exception);  
    public bool TryCreateException(  
                                 Message message,
                                 MessageFault fault,
                                 out Exception exception);  
}  
```  
  
 <span data-ttu-id="ddad5-254">Warstwę kanału można zaimplementować `GetProperty<FaultConverter>` w celu obsługi konwersji komunikatów o błędach na wyjątki.</span><span class="sxs-lookup"><span data-stu-id="ddad5-254">A channel layer can implement `GetProperty<FaultConverter>` to support converting fault messages to exceptions.</span></span> <span data-ttu-id="ddad5-255">Aby to zrobić, Zastąp `OnTryCreateException` i Sprawdź komunikat o błędzie.</span><span class="sxs-lookup"><span data-stu-id="ddad5-255">To do so, override `OnTryCreateException` and inspect the fault message.</span></span> <span data-ttu-id="ddad5-256">Jeśli jest rozpoznawana, wykonaj konwersję, w przeciwnym razie podawaj wewnętrzny kanał, aby go przekonwertować.</span><span class="sxs-lookup"><span data-stu-id="ddad5-256">If recognized, do the conversion, otherwise ask the inner channel to convert it.</span></span> <span data-ttu-id="ddad5-257">Kanały transportowe powinny być delegowane do programu, aby `FaultConverter.GetDefaultFaultConverter` można było korzystać z protokołu SOAP/WS-Addressing FaultConverter.</span><span class="sxs-lookup"><span data-stu-id="ddad5-257">Transport channels should delegate to `FaultConverter.GetDefaultFaultConverter` to get the default SOAP/WS-Addressing FaultConverter.</span></span>  
  
 <span data-ttu-id="ddad5-258">Typowa implementacja wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="ddad5-258">A typical implementation looks like this:</span></span>  
  
```csharp
public override bool OnTryCreateException(  
                            Message message,
                            MessageFault fault,
                            out Exception exception)  
{  
    if (message.Action == "...")  
    {  
        exception = ...;  
        return true;  
    }  
    // OR  
    if ((fault.Code.Name == "...") && (fault.Code.Namespace == "..."))  
    {  
        exception = ...;  
        return true;  
    }  
  
    if (fault.IsMustUnderstand)  
    {  
        if (fault.WasHeaderNotUnderstood(  
                   message.Headers, "...", "..."))  
        {  
            exception = new ProtocolException(...);  
            return true;  
        }  
    }  
  
#if IMPLEMENTING_TRANSPORT_CHANNEL  
    FaultConverter encoderConverter =
              this.encoder.GetProperty<FaultConverter>();  
    if ((encoderConverter != null) &&
        (encoderConverter.TryCreateException(  
                              message, fault, out exception)))  
    {  
        return true;  
    }  
  
    FaultConverter defaultConverter =  
             FaultConverter.GetDefaultFaultConverter(  
                             this.channel.messageVersion);  
    return defaultConverter.TryCreateException(  
                             message, fault, out exception);  
#else  
    FaultConverter inner =
                    this.innerChannel.GetProperty<FaultConverter>();  
    if (inner != null)  
    {  
        return inner.TryCreateException(message, fault, out exception);  
    }  
    else  
    {  
        exception = null;  
        return false;  
    }  
#endif  
}  
```  
  
 <span data-ttu-id="ddad5-259">W przypadku określonych warunków błędu, które mają odrębne scenariusze odzyskiwania, należy rozważyć Definiowanie klasy pochodnej `ProtocolException` .</span><span class="sxs-lookup"><span data-stu-id="ddad5-259">For specific fault conditions that have distinct recovery scenarios, consider defining a derived class of `ProtocolException`.</span></span>  
  
### <a name="mustunderstand-processing"></a><span data-ttu-id="ddad5-260">Przetwarzanie MustUnderstand</span><span class="sxs-lookup"><span data-stu-id="ddad5-260">MustUnderstand Processing</span></span>  

 <span data-ttu-id="ddad5-261">Protokół SOAP definiuje ogólny błąd sygnalizujący, że wymagany nagłówek nie został rozpoznany przez odbiornik.</span><span class="sxs-lookup"><span data-stu-id="ddad5-261">SOAP defines a general fault for signaling that a required header was not understood by the receiver.</span></span> <span data-ttu-id="ddad5-262">Ten błąd jest znany jako `mustUnderstand` błąd.</span><span class="sxs-lookup"><span data-stu-id="ddad5-262">This fault is known as the `mustUnderstand` fault.</span></span> <span data-ttu-id="ddad5-263">W programie WCF kanały niestandardowe nigdy nie generują `mustUnderstand` błędów.</span><span class="sxs-lookup"><span data-stu-id="ddad5-263">In WCF, custom channels never generate `mustUnderstand` faults.</span></span> <span data-ttu-id="ddad5-264">Zamiast tego, Dyspozytor WCF, który znajduje się w górnej części stosu komunikacji WCF, sprawdza, czy wszystkie nagłówki, które zostały oznaczone jako MustUnderstand = true, zostały zinterpretowane przez bazowego stosu.</span><span class="sxs-lookup"><span data-stu-id="ddad5-264">Instead, the WCF Dispatcher, which is located at the top of the WCF communication stack, checks to see that all headers that were marked as MustUnderstand=true were understood by the underlying stack.</span></span> <span data-ttu-id="ddad5-265">Jeśli nie zostały one zrozumiane, `mustUnderstand` w tym momencie zostanie wygenerowany błąd.</span><span class="sxs-lookup"><span data-stu-id="ddad5-265">If any were not understood, a `mustUnderstand` fault is generated at that point.</span></span> <span data-ttu-id="ddad5-266">(Użytkownik może zdecydować się na wyłączenie tego `mustUnderstand` przetwarzania i wyświetlenie wszystkich nagłówków komunikatów przez aplikację.</span><span class="sxs-lookup"><span data-stu-id="ddad5-266">(The user can choose to turn off this `mustUnderstand` processing and have the application receive all message headers.</span></span> <span data-ttu-id="ddad5-267">W takim przypadku aplikacja jest odpowiedzialna za wykonywanie operacji `mustUnderstand` przetwarzania. Wygenerowany błąd zawiera nagłówek NotUnderstood, który zawiera nazwy wszystkich nagłówków z MustUnderstand = true, które nie zostały zrozumiałe.</span><span class="sxs-lookup"><span data-stu-id="ddad5-267">In that case the application is responsible for performing `mustUnderstand` processing.) The generated fault includes a NotUnderstood header that contains the names of all headers with MustUnderstand=true that were not understood.</span></span>  
  
 <span data-ttu-id="ddad5-268">Jeśli kanał protokołu wysyła niestandardowy nagłówek z parametrem MustUnderstand = true i odbiera `mustUnderstand` błąd, musi ustalić, czy ten błąd jest spowodowany przez plik, który został wysłany.</span><span class="sxs-lookup"><span data-stu-id="ddad5-268">If your protocol channel sends a custom header with MustUnderstand=true and receives a `mustUnderstand` fault, it must figure out whether that fault is due to the header it sent.</span></span> <span data-ttu-id="ddad5-269">Istnieją dwa elementy członkowskie `MessageFault` klasy, które są przydatne dla tego:</span><span class="sxs-lookup"><span data-stu-id="ddad5-269">There are two members on the `MessageFault` class that are useful for this:</span></span>  
  
```csharp
public class MessageFault  
{  
    ...  
    public bool IsMustUnderstandFault { get; }  
    public static bool WasHeaderNotUnderstood(MessageHeaders headers,
        string name, string ns) { }  
    ...  
  
}  
```  
  
 <span data-ttu-id="ddad5-270">`IsMustUnderstandFault` zwraca `true` czy błąd jest `mustUnderstand` błędem.</span><span class="sxs-lookup"><span data-stu-id="ddad5-270">`IsMustUnderstandFault` returns `true` if the fault is a `mustUnderstand` fault.</span></span> <span data-ttu-id="ddad5-271">`WasHeaderNotUnderstood` zwraca `true` czy nagłówek z określoną nazwą i przestrzenią nazw jest uwzględniony w błędzie jako nagłówek NotUnderstood.</span><span class="sxs-lookup"><span data-stu-id="ddad5-271">`WasHeaderNotUnderstood` returns `true` if the header with the specified name and namespace is included in the fault as a NotUnderstood header.</span></span>  <span data-ttu-id="ddad5-272">W przeciwnym razie zwraca `false` .</span><span class="sxs-lookup"><span data-stu-id="ddad5-272">Otherwise, it returns `false`.</span></span>  
  
 <span data-ttu-id="ddad5-273">Jeśli kanał emituje nagłówek, który jest oznaczony jako MustUnderstand = true, wówczas ta warstwa powinna również zaimplementować wzorzec interfejsu API generacji wyjątków i powinna konwertować `mustUnderstand` błędy spowodowane przez ten nagłówek na bardziej przydatny wyjątek, jak opisano wcześniej.</span><span class="sxs-lookup"><span data-stu-id="ddad5-273">If a channel emits a header that is marked MustUnderstand = true, then that layer should also implement the Exception Generation API pattern and should convert `mustUnderstand` faults caused by that header to a more useful exception as described previously.</span></span>  
  
## <a name="tracing"></a><span data-ttu-id="ddad5-274">Śledzenie</span><span class="sxs-lookup"><span data-stu-id="ddad5-274">Tracing</span></span>  

 <span data-ttu-id="ddad5-275">.NET Framework zapewnia mechanizm śledzenia wykonywania programu w celu pomocy w diagnozowaniu aplikacji produkcyjnych lub sporadycznych problemów, gdy nie jest możliwe po prostu dołączenie debugera i przechodzenie przez kod.</span><span class="sxs-lookup"><span data-stu-id="ddad5-275">The .NET Framework provides a mechanism to trace program execution as a way to aid diagnosing production applications or intermittent problems where it is not possible to just attach a debugger and step through the code.</span></span> <span data-ttu-id="ddad5-276">Podstawowe składniki tego mechanizmu znajdują się w <xref:System.Diagnostics?displayProperty=nameWithType> przestrzeni nazw i składają się z:</span><span class="sxs-lookup"><span data-stu-id="ddad5-276">The core components of this mechanism are in the <xref:System.Diagnostics?displayProperty=nameWithType> namespace and consist of:</span></span>  
  
- <span data-ttu-id="ddad5-277"><xref:System.Diagnostics.TraceSource?displayProperty=nameWithType>, czyli źródło informacji śledzenia do zapisania, <xref:System.Diagnostics.TraceListener?displayProperty=nameWithType> która jest abstrakcyjną klasą bazową dla konkretnych odbiorników, które odbierają informacje do śledzenia z <xref:System.Diagnostics.TraceSource> i wyprowadzają je do lokalizacji docelowej specyficznej dla odbiornika.</span><span class="sxs-lookup"><span data-stu-id="ddad5-277"><xref:System.Diagnostics.TraceSource?displayProperty=nameWithType>, which is the source of trace information to be written, <xref:System.Diagnostics.TraceListener?displayProperty=nameWithType>, which is an abstract base class for concrete listeners that receive the information to be traced from the <xref:System.Diagnostics.TraceSource> and output it to a listener-specific destination.</span></span> <span data-ttu-id="ddad5-278">Na przykład <xref:System.Diagnostics.XmlWriterTraceListener> wyprowadza informacje o śledzeniu do pliku XML.</span><span class="sxs-lookup"><span data-stu-id="ddad5-278">For example, <xref:System.Diagnostics.XmlWriterTraceListener> outputs trace information to an XML file.</span></span> <span data-ttu-id="ddad5-279">Na koniec, <xref:System.Diagnostics.TraceSwitch?displayProperty=nameWithType> dzięki czemu użytkownik aplikacji kontroluje szczegółowość śledzenia i jest zazwyczaj określany w konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="ddad5-279">Finally, <xref:System.Diagnostics.TraceSwitch?displayProperty=nameWithType>, which lets the application user control the tracing verbosity and is typically specified in configuration.</span></span>  
  
- <span data-ttu-id="ddad5-280">Oprócz podstawowych składników można użyć [narzędzia Podgląd śledzenia usługi (SvcTraceViewer.exe)](../service-trace-viewer-tool-svctraceviewer-exe.md) do wyświetlania i wyszukiwania śladów WCF.</span><span class="sxs-lookup"><span data-stu-id="ddad5-280">In addition to the core components, you can use the [Service Trace Viewer Tool (SvcTraceViewer.exe)](../service-trace-viewer-tool-svctraceviewer-exe.md) to view and search WCF traces.</span></span> <span data-ttu-id="ddad5-281">Narzędzie jest przeznaczone specjalnie dla plików śledzenia generowanych przez program WCF i pisanych przy użyciu programu <xref:System.Diagnostics.XmlWriterTraceListener> .</span><span class="sxs-lookup"><span data-stu-id="ddad5-281">The tool is designed specifically for trace files generated by WCF and written out using <xref:System.Diagnostics.XmlWriterTraceListener>.</span></span> <span data-ttu-id="ddad5-282">Na poniższej ilustracji przedstawiono różne składniki, które są objęte śledzeniem.</span><span class="sxs-lookup"><span data-stu-id="ddad5-282">The following figure shows the various components involved in tracing.</span></span>  
  
 <span data-ttu-id="ddad5-283">![Obsługa wyjątków i błędów](./media/wcfc-tracinginchannelsc.gif "wcfc_TracingInChannelsc")</span><span class="sxs-lookup"><span data-stu-id="ddad5-283">![Handling exceptions and faults](./media/wcfc-tracinginchannelsc.gif "wcfc_TracingInChannelsc")</span></span>  
  
### <a name="tracing-from-a-custom-channel"></a><span data-ttu-id="ddad5-284">Śledzenie z kanału niestandardowego</span><span class="sxs-lookup"><span data-stu-id="ddad5-284">Tracing from a Custom Channel</span></span>  

 <span data-ttu-id="ddad5-285">Kanały niestandardowe powinny zapisywać komunikaty śledzenia, aby pomóc w diagnozowaniu problemów, gdy nie jest możliwe dołączenie debugera do uruchomionej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ddad5-285">Custom channels should write out trace messages to assist in diagnosing problems when it is not possible to attach a debugger to the running application.</span></span> <span data-ttu-id="ddad5-286">Obejmuje to dwa zadania wysokiego poziomu: Tworzenie wystąpienia a <xref:System.Diagnostics.TraceSource> i wywoływanie metod w celu pisania śladów.</span><span class="sxs-lookup"><span data-stu-id="ddad5-286">This involves two high level tasks: Instantiating a <xref:System.Diagnostics.TraceSource> and calling its methods to write traces.</span></span>  
  
 <span data-ttu-id="ddad5-287">Podczas tworzenia wystąpienia elementu <xref:System.Diagnostics.TraceSource> , określony ciąg otrzymuje nazwę tego źródła.</span><span class="sxs-lookup"><span data-stu-id="ddad5-287">When instantiating a <xref:System.Diagnostics.TraceSource>, the string you specify becomes the name of that source.</span></span> <span data-ttu-id="ddad5-288">Ta nazwa służy do konfigurowania (Włącz/Wyłącz/Ustaw poziom śledzenia) źródła śledzenia.</span><span class="sxs-lookup"><span data-stu-id="ddad5-288">This name is used to configure (enable/disable/set tracing level) the trace source.</span></span> <span data-ttu-id="ddad5-289">Pojawia się również w danych wyjściowych śledzenia.</span><span class="sxs-lookup"><span data-stu-id="ddad5-289">It also appears in the trace output itself.</span></span> <span data-ttu-id="ddad5-290">Kanały niestandardowe powinny używać unikatowej nazwy źródła, aby ułatwić czytelnikom wyników śledzenia zrozumienie, z których pochodzą dane śledzenia.</span><span class="sxs-lookup"><span data-stu-id="ddad5-290">Custom channels should use a unique source name to help readers of the trace output understand where the trace information comes from.</span></span> <span data-ttu-id="ddad5-291">Typowym zastosowaniem jest nazwa zestawu, który zapisuje informacje jako nazwa źródła śledzenia.</span><span class="sxs-lookup"><span data-stu-id="ddad5-291">Using the name of the assembly that is writing the information as the name of the trace source is the common practice.</span></span> <span data-ttu-id="ddad5-292">Na przykład WCF używa elementu System. ServiceModel jako źródła śledzenia dla informacji pisanych z zestawu System. ServiceModel.</span><span class="sxs-lookup"><span data-stu-id="ddad5-292">For example, WCF uses System.ServiceModel as the trace source for information written from the System.ServiceModel assembly.</span></span>  
  
 <span data-ttu-id="ddad5-293">Po utworzeniu źródła śledzenia należy wywołać <xref:System.Diagnostics.TraceSource.TraceData%2A> <xref:System.Diagnostics.TraceSource.TraceEvent%2A> metody, lub, <xref:System.Diagnostics.TraceSource.TraceInformation%2A> Aby pisać wpisy śledzenia do detektorów śledzenia.</span><span class="sxs-lookup"><span data-stu-id="ddad5-293">Once you have a trace source, you call its <xref:System.Diagnostics.TraceSource.TraceData%2A>, <xref:System.Diagnostics.TraceSource.TraceEvent%2A>, or <xref:System.Diagnostics.TraceSource.TraceInformation%2A> methods to write trace entries to the trace listeners.</span></span> <span data-ttu-id="ddad5-294">Dla każdego zapisywanego wpisu śledzenia należy sklasyfikować typ zdarzenia jako jeden z typów zdarzeń zdefiniowanych w <xref:System.Diagnostics.TraceEventType> .</span><span class="sxs-lookup"><span data-stu-id="ddad5-294">For each trace entry you write, you need to classify the type of event as one of the event types defined in <xref:System.Diagnostics.TraceEventType>.</span></span> <span data-ttu-id="ddad5-295">Ta klasyfikacja i ustawienie poziomu śledzenia w obszarze Konfiguracja określają, czy wpis śledzenia jest wyprowadzany do odbiornika.</span><span class="sxs-lookup"><span data-stu-id="ddad5-295">This classification and the trace level setting in configuration determine whether the trace entry is output to the listener.</span></span> <span data-ttu-id="ddad5-296">Na przykład ustawienie poziomu śledzenia w obszarze Konfiguracja pozwala na `Warning` `Warning` `Error` `Critical` zapisywanie wpisów śledzenia, ale bloków informacji i zapisów pełnych.</span><span class="sxs-lookup"><span data-stu-id="ddad5-296">For example, setting the trace level in configuration to `Warning` allows `Warning`, `Error` and `Critical` trace entries to be written but blocks Information and Verbose entries.</span></span> <span data-ttu-id="ddad5-297">Oto przykład tworzenia wystąpienia źródła śledzenia i zapisywania wpisu na poziomie informacji:</span><span class="sxs-lookup"><span data-stu-id="ddad5-297">Here is an example of instantiating a trace source and writing out an entry at Information level:</span></span>  
  
```csharp
using System.Diagnostics;  
//...  
TraceSource udpSource = new TraceSource("Microsoft.Samples.Udp");  
//...  
udpsource.TraceInformation("UdpInputChannel received a message");  
```  
  
> [!IMPORTANT]
> <span data-ttu-id="ddad5-298">Zdecydowanie zaleca się określenie źródłowej nazwy śledzenia, która jest unikatowa dla niestandardowego kanału, aby ułatwić śledzenie odczytywanych danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="ddad5-298">It is highly recommended that you specify a trace source name that is unique to your custom channel to help trace output readers understand where the output came from.</span></span>  
  
#### <a name="integrating-with-the-trace-viewer"></a><span data-ttu-id="ddad5-299">Integracja z podglądem śledzenia</span><span class="sxs-lookup"><span data-stu-id="ddad5-299">Integrating with the Trace Viewer</span></span>  

 <span data-ttu-id="ddad5-300">Ślady generowane przez kanał mogą być wyprowadzane w formacie możliwym do odczytania przez [narzędzie Podgląd śledzenia usługi (SvcTraceViewer.exe)](../service-trace-viewer-tool-svctraceviewer-exe.md) , używając <xref:System.Diagnostics.XmlWriterTraceListener?displayProperty=nameWithType> jako odbiornika śledzenia.</span><span class="sxs-lookup"><span data-stu-id="ddad5-300">Traces generated by your channel can be output in a format readable by the [Service Trace Viewer Tool (SvcTraceViewer.exe)](../service-trace-viewer-tool-svctraceviewer-exe.md) by using <xref:System.Diagnostics.XmlWriterTraceListener?displayProperty=nameWithType> as the trace listener.</span></span> <span data-ttu-id="ddad5-301">Nie jest to coś, co należy zrobić w przypadku deweloperów kanału.</span><span class="sxs-lookup"><span data-stu-id="ddad5-301">This is not something you, as the channel developer, need to do.</span></span> <span data-ttu-id="ddad5-302">Nie jest to jednak użytkownik aplikacji (lub osoba odpowiedzialna za rozwiązywanie problemów z aplikacją), która musi skonfigurować ten odbiornik śledzenia w pliku konfiguracyjnym aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ddad5-302">Rather, it is the application user (or the person troubleshooting the application) that needs to configure this trace listener in the application's configuration file.</span></span> <span data-ttu-id="ddad5-303">Na przykład następująca konfiguracja wyprowadza informacje o śledzeniu z obu <xref:System.ServiceModel?displayProperty=nameWithType> i `Microsoft.Samples.Udp` do pliku o nazwie `TraceEventsFile.e2e` :</span><span class="sxs-lookup"><span data-stu-id="ddad5-303">For example, the following configuration outputs trace information from both <xref:System.ServiceModel?displayProperty=nameWithType> and `Microsoft.Samples.Udp` to the file named `TraceEventsFile.e2e`:</span></span>  
  
```xml  
<configuration>  
  <system.diagnostics>  
    <sources>  
      <!-- configure System.ServiceModel trace source -->  
      <source name="System.ServiceModel" switchValue="Verbose"
              propagateActivity="true">  
        <listeners>  
          <add name="e2e" />  
        </listeners>  
      </source>  
      <!-- configure Microsoft.Samples.Udp trace source -->  
      <source name="Microsoft.Samples.Udp" switchValue="Verbose" >  
        <listeners>  
          <add name="e2e" />  
        </listeners>  
      </source>  
    </sources>  
    <!--   
    Define a shared trace listener that outputs to TraceFile.e2e  
    The listener name is e2e   
    -->  
    <sharedListeners>  
      <add name="e2e" type="System.Diagnostics.XmlWriterTraceListener"  
        initializeData=".\TraceFile.e2e"/>  
    </sharedListeners>  
    <trace autoflush="true" />  
  </system.diagnostics>  
</configuration>  
```  
  
#### <a name="tracing-structured-data"></a><span data-ttu-id="ddad5-304">Śledzenie danych strukturalnych</span><span class="sxs-lookup"><span data-stu-id="ddad5-304">Tracing Structured Data</span></span>  

 <span data-ttu-id="ddad5-305"><xref:System.Diagnostics.TraceSource?displayProperty=nameWithType> ma <xref:System.Diagnostics.TraceSource.TraceData%2A> metodę, która pobiera jeden lub więcej obiektów, które mają być uwzględnione w wpisie śledzenia.</span><span class="sxs-lookup"><span data-stu-id="ddad5-305"><xref:System.Diagnostics.TraceSource?displayProperty=nameWithType> has a <xref:System.Diagnostics.TraceSource.TraceData%2A> method that takes one or more objects that are to be included in the trace entry.</span></span> <span data-ttu-id="ddad5-306">Ogólnie rzecz biorąc <xref:System.Object.ToString%2A?displayProperty=nameWithType> Metoda jest wywoływana dla każdego obiektu, a wynikowy ciąg jest zapisywana jako część wpisu śledzenia.</span><span class="sxs-lookup"><span data-stu-id="ddad5-306">In general, the <xref:System.Object.ToString%2A?displayProperty=nameWithType> method is called on each object and the resulting string is written as part of the trace entry.</span></span> <span data-ttu-id="ddad5-307">Podczas używania <xref:System.Diagnostics.XmlWriterTraceListener?displayProperty=nameWithType> do śledzenia danych wyjściowych można przekazać <xref:System.Xml.XPath.IXPathNavigable?displayProperty=nameWithType> jako obiekt danych do <xref:System.Diagnostics.TraceSource.TraceData%2A> .</span><span class="sxs-lookup"><span data-stu-id="ddad5-307">When using <xref:System.Diagnostics.XmlWriterTraceListener?displayProperty=nameWithType> to output traces, you can pass an <xref:System.Xml.XPath.IXPathNavigable?displayProperty=nameWithType> as the data object to <xref:System.Diagnostics.TraceSource.TraceData%2A>.</span></span> <span data-ttu-id="ddad5-308">Wynikowy wpis śledzenia zawiera kod XML dostarczony przez <xref:System.Xml.XPath.XPathNavigator?displayProperty=nameWithType> .</span><span class="sxs-lookup"><span data-stu-id="ddad5-308">The resulting trace entry includes the XML provided by the <xref:System.Xml.XPath.XPathNavigator?displayProperty=nameWithType>.</span></span> <span data-ttu-id="ddad5-309">Oto przykład wpisu z danymi aplikacji XML:</span><span class="sxs-lookup"><span data-stu-id="ddad5-309">Here is an example entry with XML application data:</span></span>  
  
```xml  
<E2ETraceEvent xmlns="http://schemas.microsoft.com/2004/06/E2ETraceEvent">  
  <System xmlns="...">  
    <EventID>12</EventID>  
    <Type>3</Type>  
    <SubType Name="Information">0</SubType>  
    <Level>8</Level>  
    <TimeCreated SystemTime="2006-01-13T22:58:03.0654832Z" />  
    <Source Name="Microsoft.ServiceModel.Samples.Udp" />  
    <Correlation ActivityID="{00000000-0000-0000-0000-000000000000}" />  
    <Execution  ProcessName="UdpTestConsole"
                ProcessID="3348" ThreadID="4" />  
    <Channel />  
    <Computer>COMPUTER-LT01</Computer>  
  </System>  
<!-- XML application data -->  
  <ApplicationData>  
  <TraceData>  
   <DataItem>  
   <TraceRecord
     Severity="Information"  
     xmlns="…">  
        <TraceIdentifier>some trace id</TraceIdentifier>  
        <Description>EndReceive called</Description>  
        <AppDomain>UdpTestConsole.exe</AppDomain>  
        <Source>UdpInputChannel</Source>  
      </TraceRecord>  
    </DataItem>  
  </TraceData>  
  </ApplicationData>  
</E2ETraceEvent>  
```  
  
 <span data-ttu-id="ddad5-310">Przeglądarka śledzenia danych programu WCF rozumie schemat `TraceRecord` elementu pokazanego wcześniej i wyodrębnia dane z jego elementów podrzędnych i wyświetla go w formacie tabelarycznym.</span><span class="sxs-lookup"><span data-stu-id="ddad5-310">The WCF trace viewer understands the schema of the `TraceRecord` element shown previously and extracts the data from its child elements and displays it in a tabular format.</span></span> <span data-ttu-id="ddad5-311">Kanał powinien używać tego schematu podczas śledzenia danych aplikacji ze strukturą, aby ułatwić Svctraceviewer.exe użytkownikom odczytywanie danych.</span><span class="sxs-lookup"><span data-stu-id="ddad5-311">Your channel should use this schema when tracing structured application data to help Svctraceviewer.exe users read the data.</span></span>
