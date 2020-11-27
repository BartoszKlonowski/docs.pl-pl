---
title: 'Szybki start: rozwiązywanie problemów z architekturą WCF'
ms.date: 03/30/2017
helpviewer_keywords:
- WCF [WCF], troubleshooting
- Windows Communication Foundation [WCF], troubleshooting
ms.assetid: a9ea7a53-f31a-46eb-806e-898e465a4992
ms.openlocfilehash: 7df178334ca3ef5b901e3e82bf39592434ee059e
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96279730"
---
# <a name="wcf-troubleshooting-quickstart"></a><span data-ttu-id="07c3f-102">Szybki start: rozwiązywanie problemów z architekturą WCF</span><span class="sxs-lookup"><span data-stu-id="07c3f-102">WCF Troubleshooting Quickstart</span></span>

<span data-ttu-id="07c3f-103">W tym temacie wymieniono kilka znanych problemów, z którymi klienci korzystali podczas opracowywania klientów i usług WCF.</span><span class="sxs-lookup"><span data-stu-id="07c3f-103">This topic lists a number of known issues customers have run into while developing WCF clients and services.</span></span> <span data-ttu-id="07c3f-104">Jeśli problem, z którym korzystasz, nie znajduje się na liście, zalecamy skonfigurowanie śledzenia dla usługi.</span><span class="sxs-lookup"><span data-stu-id="07c3f-104">If the issue you are running into is not in this list, we recommend you configure tracing for your service.</span></span> <span data-ttu-id="07c3f-105">Spowoduje to wygenerowanie pliku śledzenia, który można wyświetlić za pomocą podglądu plików śledzenia i uzyskać szczegółowe informacje o wyjątkach, które mogą wystąpić w ramach usługi.</span><span class="sxs-lookup"><span data-stu-id="07c3f-105">This will generate a trace file that you can view with the trace file viewer and get detailed information about exceptions that may be occurring within the service.</span></span> <span data-ttu-id="07c3f-106">Aby uzyskać więcej informacji na temat konfigurowania śledzenia, zobacz: [Konfigurowanie śledzenia](./diagnostics/tracing/configuring-tracing.md).</span><span class="sxs-lookup"><span data-stu-id="07c3f-106">For more information on configuring tracing, see: [Configuring Tracing](./diagnostics/tracing/configuring-tracing.md).</span></span> <span data-ttu-id="07c3f-107">Aby uzyskać więcej informacji na temat podglądu plików śledzenia, zobacz: [narzędzie Podgląd śledzenia usługi (SvcTraceViewer.exe)](service-trace-viewer-tool-svctraceviewer-exe.md).</span><span class="sxs-lookup"><span data-stu-id="07c3f-107">For more information on the trace file viewer, see: [Service Trace Viewer Tool (SvcTraceViewer.exe)](service-trace-viewer-tool-svctraceviewer-exe.md).</span></span>  
  
1. [<span data-ttu-id="07c3f-108">Po zainstalowaniu systemu Windows 7 i usług IIS podczas próby przeglądania do usługi WCF pojawia się następujący komunikat o błędzie: błąd HTTP 404,3 — nie znaleziono</span><span class="sxs-lookup"><span data-stu-id="07c3f-108">After installing Windows 7 and IIS, when I attempt to browse to a WCF service I get the following error message: HTTP Error 404.3 – Not Found</span></span>](#bkmk_0)  
  
     <span data-ttu-id="07c3f-109">Błąd HTTP 404,3 — nie można obsłużyć żądanej strony FoundThe z powodu konfiguracji rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="07c3f-109">HTTP Error 404.3 – Not FoundThe page you are requesting cannot be served because of the extension configuration.</span></span> <span data-ttu-id="07c3f-110">Jeśli strona jest skryptem, Dodaj program obsługi.</span><span class="sxs-lookup"><span data-stu-id="07c3f-110">If the page is a script, add a handler.</span></span> <span data-ttu-id="07c3f-111">Jeśli plik powinien zostać pobrany, Dodaj mapę MIME.</span><span class="sxs-lookup"><span data-stu-id="07c3f-111">If the file should be downloaded, add a MIME map.</span></span> <span data-ttu-id="07c3f-112">Szczegóły błędu InformationModule StaticFileModule.</span><span class="sxs-lookup"><span data-stu-id="07c3f-112">Detailed Error InformationModule StaticFileModule.</span></span>  
  
2. [<span data-ttu-id="07c3f-113">Czasami otrzymuję MessageSecurityException — w drugim żądaniu, jeśli mój klient jest w stanie bezczynności przez pewien czas po pierwszym żądaniu. Co się dzieje?</span><span class="sxs-lookup"><span data-stu-id="07c3f-113">Sometimes I receive a MessageSecurityException on the second request if my client is idle for a while after the first request. What is happening?</span></span>](#BKMK_q1)  
  
3. [<span data-ttu-id="07c3f-114">Usługa My zaczyna odrzucać nowych klientów po przejściu do niej od około 10 klientów. Co się dzieje?</span><span class="sxs-lookup"><span data-stu-id="07c3f-114">My service starts to reject new clients after about 10 clients are interacting with it. What is happening?</span></span>](#BKMK_q2)  
  
4. [<span data-ttu-id="07c3f-115">Czy mogę załadować moją konfigurację usługi z innej lokalizacji niż plik konfiguracyjny aplikacji WCF?</span><span class="sxs-lookup"><span data-stu-id="07c3f-115">Can I load my service configuration from somewhere other than the WCF application’s configuration file?</span></span>](#BKMK_q3)  
  
5. [<span data-ttu-id="07c3f-116">Moja usługa i klient są doskonałe, ale nie mogę ich używać, gdy klient znajduje się na innym komputerze? Co się dzieje?</span><span class="sxs-lookup"><span data-stu-id="07c3f-116">My service and client work great, but I can’t get them to work when the client is on another computer? What’s happening?</span></span>](#BKMK_q4)  
  
6. [<span data-ttu-id="07c3f-117">Gdy zgłaszam wyjątek FaultException \<Exception> , którego typ jest wyjątkiem, zawsze otrzymuję ogólny typ błęduexception na kliencie, a nie typ ogólny. Co się dzieje?</span><span class="sxs-lookup"><span data-stu-id="07c3f-117">When I throw a FaultException\<Exception> where the type is an exception, I always receive a general FaultException type on the client and not the generic type. What’s happening?</span></span>](#BKMK_q5)  
  
7. [<span data-ttu-id="07c3f-118">Wygląda na to, że operacje jednokierunkowe i typu żądanie-odpowiedź są zwracane z tą samą szybkością, gdy odpowiedź nie zawiera żadnych danych. Co się dzieje?</span><span class="sxs-lookup"><span data-stu-id="07c3f-118">It seems like one-way and request-reply operations return at roughly the same speed when the reply contains no data. What's happening?</span></span>](#BKMK_q6)  
  
8. [<span data-ttu-id="07c3f-119">Używam certyfikatu X. 509 z moją usługą i otrzymuję system. Security. Cryptography. CryptographicException. Co się dzieje?</span><span class="sxs-lookup"><span data-stu-id="07c3f-119">I’m using an X.509 certificate with my service and I get a System.Security.Cryptography.CryptographicException. What’s happening?</span></span>](#BKMK_q77)  
  
9. [<span data-ttu-id="07c3f-120">Pierwszy parametr operacji został zmieniony z wielkich na małe litery; teraz mój klient zgłasza wyjątek. Co się dzieje?</span><span class="sxs-lookup"><span data-stu-id="07c3f-120">I changed the first parameter of an operation from uppercase to lowercase; now my client throws an exception. What's happening?</span></span>](#BKMK_q88)  
  
10. [<span data-ttu-id="07c3f-121">Używam jednego z narzędzi do śledzenia i otrzymuję EndpointNotFoundException. Co się dzieje?</span><span class="sxs-lookup"><span data-stu-id="07c3f-121">I’m using one of my tracing tools and I get an EndpointNotFoundException. What’s happening?</span></span>](#BKMK_q99)  
  
11. [<span data-ttu-id="07c3f-122">Podczas wywoływania aplikacji HTTP sieci Web WCF z aplikacji SOAP WCF usługa zwraca następujący błąd: Metoda 405 nie jest dozwolona</span><span class="sxs-lookup"><span data-stu-id="07c3f-122">When calling a WCF Web HTTP application from a WCF SOAP application the service returns the following error: 405 Method Not Allowed</span></span>](#BK_MK99)  
  
 [<span data-ttu-id="07c3f-123">Jaki jest adres podstawowy? Jak odnosi się do adresu punktu końcowego?</span><span class="sxs-lookup"><span data-stu-id="07c3f-123">What is the base address? How does it relate to an endpoint address?</span></span>](#BKMK_q10)  
  
<a name="bkmk_0"></a>

## <a name="after-installing-windows-7-and-iis-when-i-attempt-to-browse-to-a-wcf-service-i-get-the-following-error-message-http-error-4043--not-found"></a><span data-ttu-id="07c3f-124">Po zainstalowaniu systemu Windows 7 i usług IIS podczas próby przeglądania do usługi WCF pojawia się następujący komunikat o błędzie: błąd HTTP 404,3 — nie znaleziono</span><span class="sxs-lookup"><span data-stu-id="07c3f-124">After installing Windows 7 and IIS, when I attempt to browse to a WCF service I get the following error message: HTTP Error 404.3 – Not Found</span></span>  

 <span data-ttu-id="07c3f-125">Pełny komunikat o błędzie:</span><span class="sxs-lookup"><span data-stu-id="07c3f-125">The full error message is:</span></span>  
  
 <span data-ttu-id="07c3f-126">Błąd HTTP 404,3 — nie można obsłużyć żądanej strony FoundThe z powodu konfiguracji rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="07c3f-126">HTTP Error 404.3 – Not FoundThe page you are requesting cannot be served because of the extension configuration.</span></span> <span data-ttu-id="07c3f-127">Jeśli strona jest skryptem, Dodaj program obsługi.</span><span class="sxs-lookup"><span data-stu-id="07c3f-127">If the page is a script, add a handler.</span></span> <span data-ttu-id="07c3f-128">Jeśli plik powinien zostać pobrany, Dodaj mapę MIME.</span><span class="sxs-lookup"><span data-stu-id="07c3f-128">If the file should be downloaded, add a MIME map.</span></span> <span data-ttu-id="07c3f-129">Szczegóły błędu InformationModule StaticFileModule.</span><span class="sxs-lookup"><span data-stu-id="07c3f-129">Detailed Error InformationModule StaticFileModule.</span></span>  
  
 <span data-ttu-id="07c3f-130">Ten komunikat o błędzie występuje, gdy "Windows Communication Foundation Aktywacja HTTP" nie jest jawnie ustawiony w panelu sterowania.</span><span class="sxs-lookup"><span data-stu-id="07c3f-130">This error message occurs when "Windows Communication Foundation HTTP Activation" is not explicitly set in the Control Panel.</span></span> <span data-ttu-id="07c3f-131">Aby ustawić ten sposób, przejdź do panelu sterowania, kliknij pozycję programy w lewym dolnym rogu okna.</span><span class="sxs-lookup"><span data-stu-id="07c3f-131">To set this go to the Control Panel, click Programs in the lower left-hand corner of the window.</span></span> <span data-ttu-id="07c3f-132">Kliknij pozycję Włącz lub wyłącz funkcje systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="07c3f-132">Click Turn Windows features on or off.</span></span> <span data-ttu-id="07c3f-133">Rozwiń węzeł Microsoft .NET Framework 3.5.1 i wybierz pozycję Windows Communication Foundation Aktywacja HTTP.</span><span class="sxs-lookup"><span data-stu-id="07c3f-133">Expand Microsoft .NET Framework 3.5.1 and select Windows Communication Foundation HTTP Activation.</span></span>  
  
<a name="BKMK_q1"></a>

## <a name="sometimes-i-receive-a-messagesecurityexception-on-the-second-request-if-my-client-is-idle-for-a-while-after-the-first-request-what-is-happening"></a><span data-ttu-id="07c3f-134">Czasami otrzymuję MessageSecurityException — w drugim żądaniu, jeśli mój klient jest w stanie bezczynności przez pewien czas po pierwszym żądaniu.</span><span class="sxs-lookup"><span data-stu-id="07c3f-134">Sometimes I receive a MessageSecurityException on the second request if my client is idle for a while after the first request.</span></span> <span data-ttu-id="07c3f-135">Co się dzieje?</span><span class="sxs-lookup"><span data-stu-id="07c3f-135">What is happening?</span></span>  

 <span data-ttu-id="07c3f-136">Drugie żądanie może zakończyć się niepowodzeniem głównie z dwóch powodów: (1) upłynął limit czasu sesji lub (2) serwer sieci Web, na którym znajduje się usługa, jest odtwarzany.</span><span class="sxs-lookup"><span data-stu-id="07c3f-136">The second request can fail primarily for two reasons: (1) the session has timed out or (2) the Web server that is hosting the service is recycled.</span></span> <span data-ttu-id="07c3f-137">W pierwszym przypadku sesja jest ważna do momentu przekroczenia limitu czasu usługi. Gdy usługa nie otrzymuje żądania od klienta w okresie określonym w powiązaniu usługi ( <xref:System.ServiceModel.Channels.Binding.ReceiveTimeout%2A> ), usługa kończy sesję zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="07c3f-137">In the first case, the session is valid until the service times out. When the service does not receive a request from the client within the period of time specified in the service's binding (<xref:System.ServiceModel.Channels.Binding.ReceiveTimeout%2A>), the service terminates the security session.</span></span> <span data-ttu-id="07c3f-138">Kolejne komunikaty klienta powodują w wyniku <xref:System.ServiceModel.Security.MessageSecurityException> .</span><span class="sxs-lookup"><span data-stu-id="07c3f-138">Subsequent client messages result in the <xref:System.ServiceModel.Security.MessageSecurityException>.</span></span> <span data-ttu-id="07c3f-139">Klient musi ponownie nawiązać bezpieczną sesję z usługą w celu wysłania przyszłych komunikatów lub użycia tokenu stanowego kontekstu zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="07c3f-139">The client must re-establish a secure session with the service to send future messages or use a stateful security context token.</span></span> <span data-ttu-id="07c3f-140">Tokeny kontekstowe kontekstu zabezpieczeń umożliwiają również bezpieczną sesję przetrwania odtwarzania serwera sieci Web.</span><span class="sxs-lookup"><span data-stu-id="07c3f-140">Stateful security context tokens also allow a secure session to survive a Web server being recycled.</span></span> <span data-ttu-id="07c3f-141">Aby uzyskać więcej informacji o korzystaniu ze stanowych tokenów bezpiecznego kontekstu w bezpiecznej sesji, zobacz [How to: Create a Security Context token for a Secure Session](./feature-details/how-to-create-a-security-context-token-for-a-secure-session.md).</span><span class="sxs-lookup"><span data-stu-id="07c3f-141">For more information about using stateful secure context tokens in a secure session, see [How to: Create a Security Context Token for a Secure Session](./feature-details/how-to-create-a-security-context-token-for-a-secure-session.md).</span></span> <span data-ttu-id="07c3f-142">Alternatywnie można wyłączyć bezpieczne sesje.</span><span class="sxs-lookup"><span data-stu-id="07c3f-142">Alternatively, you can disable secure sessions.</span></span> <span data-ttu-id="07c3f-143">Korzystając z [\<wsHttpBinding>](../configure-apps/file-schema/wcf/wshttpbinding.md) powiązania, można ustawić `establishSecurityContext` Właściwość na `false` Aby wyłączyć bezpieczne sesje.</span><span class="sxs-lookup"><span data-stu-id="07c3f-143">When you use the [\<wsHttpBinding>](../configure-apps/file-schema/wcf/wshttpbinding.md) binding, you can set the `establishSecurityContext` property to `false` to disable secure sessions.</span></span> <span data-ttu-id="07c3f-144">Aby wyłączyć bezpieczne sesje dla innych powiązań, należy utworzyć niestandardowe powiązanie.</span><span class="sxs-lookup"><span data-stu-id="07c3f-144">To disable secure sessions for other bindings, you must create a custom binding.</span></span> <span data-ttu-id="07c3f-145">Aby uzyskać szczegółowe informacje o tworzeniu niestandardowego powiązania, zobacz [How to: Create a Custom Binding using the elementu SecurityBindingElement](./feature-details/how-to-create-a-custom-binding-using-the-securitybindingelement.md).</span><span class="sxs-lookup"><span data-stu-id="07c3f-145">For details about creating a custom binding, see [How to: Create a Custom Binding Using the SecurityBindingElement](./feature-details/how-to-create-a-custom-binding-using-the-securitybindingelement.md).</span></span> <span data-ttu-id="07c3f-146">Przed zastosowaniem dowolnej z tych opcji należy zrozumieć wymagania dotyczące zabezpieczeń aplikacji.</span><span class="sxs-lookup"><span data-stu-id="07c3f-146">Before you apply any of these options, you must understand your application's security requirements.</span></span>  
  
<a name="BKMK_q2"></a>

## <a name="my-service-starts-to-reject-new-clients-after-about-10-clients-are-interacting-with-it-what-is-happening"></a><span data-ttu-id="07c3f-147">Usługa My zaczyna odrzucać nowych klientów po przejściu do niej od około 10 klientów.</span><span class="sxs-lookup"><span data-stu-id="07c3f-147">My service starts to reject new clients after about 10 clients are interacting with it.</span></span> <span data-ttu-id="07c3f-148">Co się dzieje?</span><span class="sxs-lookup"><span data-stu-id="07c3f-148">What is happening?</span></span>  

 <span data-ttu-id="07c3f-149">Domyślnie usługi mogą mieć tylko 10 współbieżnych sesji.</span><span class="sxs-lookup"><span data-stu-id="07c3f-149">By default, services can have only 10 concurrent sessions.</span></span> <span data-ttu-id="07c3f-150">W związku z tym, jeśli powiązania usługi używają sesji, usługa akceptuje nowe połączenia klienta, dopóki nie osiągnie tego numeru, po upływie którego nowe połączenia z klientami będą odrzucane do momentu zakończenia jednej z bieżących sesji.</span><span class="sxs-lookup"><span data-stu-id="07c3f-150">Therefore, if the service bindings use sessions, the service accepts new client connections until it reaches that number, after which it refuses new client connections until one of the current sessions ends.</span></span> <span data-ttu-id="07c3f-151">Więcej klientów można obsłużyć na wiele sposobów.</span><span class="sxs-lookup"><span data-stu-id="07c3f-151">You can support more clients in a number of ways.</span></span> <span data-ttu-id="07c3f-152">Jeśli usługa nie wymaga sesji, nie należy używać powiązania sesji.</span><span class="sxs-lookup"><span data-stu-id="07c3f-152">If your service does not require sessions, do not use a sessionful binding.</span></span> <span data-ttu-id="07c3f-153">(Aby uzyskać więcej informacji, zobacz [Korzystanie z sesji](using-sessions.md)). Inną opcją jest zwiększenie limitu sesji przez zmianę wartości <xref:System.ServiceModel.Description.ServiceThrottlingBehavior.MaxConcurrentSessions%2A> właściwości na liczbę odpowiednią do okoliczności.</span><span class="sxs-lookup"><span data-stu-id="07c3f-153">(For more information, see [Using Sessions](using-sessions.md).) Another option is to increase the session limit by changing the value of the <xref:System.ServiceModel.Description.ServiceThrottlingBehavior.MaxConcurrentSessions%2A> property to the number appropriate to your circumstance.</span></span>  
  
<a name="BKMK_q3"></a>

## <a name="can-i-load-my-service-configuration-from-somewhere-other-than-the-wcf-applications-configuration-file"></a><span data-ttu-id="07c3f-154">Czy mogę załadować moją konfigurację usługi z innej lokalizacji niż plik konfiguracyjny aplikacji WCF?</span><span class="sxs-lookup"><span data-stu-id="07c3f-154">Can I load my service configuration from somewhere other than the WCF application’s configuration file?</span></span>  

 <span data-ttu-id="07c3f-155">Tak, jednak trzeba utworzyć niestandardową <xref:System.ServiceModel.ServiceHost> klasę, która zastąpi <xref:System.ServiceModel.ServiceHostBase.ApplyConfiguration%2A> metodę.</span><span class="sxs-lookup"><span data-stu-id="07c3f-155">Yes, however, you have to create a custom <xref:System.ServiceModel.ServiceHost> class that overrides the <xref:System.ServiceModel.ServiceHostBase.ApplyConfiguration%2A> method.</span></span> <span data-ttu-id="07c3f-156">Wewnątrz tej metody można wywołać bazę, aby najpierw załadować konfigurację (Jeśli chcesz również załadować informacje o konfiguracji standardowej), ale możesz również całkowicie zastąpić system ładowania konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="07c3f-156">Inside that method, you can call the base to load configuration first (if you want to load the standard configuration information as well) but you can also entirely replace the configuration loading system.</span></span> <span data-ttu-id="07c3f-157">Jeśli chcesz załadować konfigurację z pliku konfiguracyjnego, który jest inny niż plik konfiguracji aplikacji, musisz przeanalizować plik konfiguracji samodzielnie i załadować konfigurację.</span><span class="sxs-lookup"><span data-stu-id="07c3f-157">If you want to load configuration from a configuration file that is different from the application configuration file, you must parse the configuration file yourself and load the configuration.</span></span>  
  
 <span data-ttu-id="07c3f-158">Poniższy przykład kodu pokazuje, jak zastąpić <xref:System.ServiceModel.ServiceHostBase.ApplyConfiguration%2A> metodę i bezpośrednio skonfigurować punkt końcowy.</span><span class="sxs-lookup"><span data-stu-id="07c3f-158">The following code example shows how to override the <xref:System.ServiceModel.ServiceHostBase.ApplyConfiguration%2A> method and directly configure an endpoint.</span></span>  
  
```csharp
public class MyServiceHost : ServiceHost  
{  
    public MyServiceHost(Type serviceType, params Uri[] baseAddresses)
      : base(serviceType, baseAddresses)  
    {
        Console.WriteLine("MyServiceHost Constructor");
    }  
  
    protected override void ApplyConfiguration()  
    {  
        string straddress = GetAddress();  
        Uri address = new Uri(straddress);  
        Binding binding = GetBinding();  
        base.AddServiceEndpoint(typeof(IData), binding, address);  
    }  
  
    string GetAddress()  
    {
        return "http://MyMachine:7777/MyEndpointAddress/";
    }  
  
    Binding GetBinding()  
    {  
        WSHttpBinding binding = new WSHttpBinding();  
        binding.Security.Mode = SecurityMode.None;  
        return binding;  
    }  
}  
```  
  
<a name="BKMK_q4"></a>

## <a name="my-service-and-client-work-great-but-i-cant-get-them-to-work-when-the-client-is-on-another-computer-whats-happening"></a><span data-ttu-id="07c3f-159">Moja usługa i klient są doskonałe, ale nie mogę ich używać, gdy klient znajduje się na innym komputerze?</span><span class="sxs-lookup"><span data-stu-id="07c3f-159">My service and client work great, but I can’t get them to work when the client is on another computer?</span></span> <span data-ttu-id="07c3f-160">Co się dzieje?</span><span class="sxs-lookup"><span data-stu-id="07c3f-160">What’s happening?</span></span>  

 <span data-ttu-id="07c3f-161">W zależności od wyjątku mogą wystąpić pewne problemy:</span><span class="sxs-lookup"><span data-stu-id="07c3f-161">Depending upon the exception, there may be several issues:</span></span>  
  
- <span data-ttu-id="07c3f-162">Może zajść potrzeba zmiany adresów punktu końcowego klienta na nazwę hosta, a nie "localhost".</span><span class="sxs-lookup"><span data-stu-id="07c3f-162">You might need to change the client endpoint addresses to the host name and not "localhost".</span></span>  
  
- <span data-ttu-id="07c3f-163">Może być konieczne otwarcie portu w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="07c3f-163">You might need to open the port to the application.</span></span> <span data-ttu-id="07c3f-164">Aby uzyskać szczegółowe informacje, zobacz [instrukcje zapory](./samples/firewall-instructions.md) w PRZYKŁADACH zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="07c3f-164">For details, see [Firewall Instructions](./samples/firewall-instructions.md) from the SDK samples.</span></span>  
  
- <span data-ttu-id="07c3f-165">Inne możliwe problemy można znaleźć w temacie przykłady z przykładami [Windows Communication Foundation](./samples/running-the-samples.md).</span><span class="sxs-lookup"><span data-stu-id="07c3f-165">For other possible issues, see the samples topic [Running the Windows Communication Foundation Samples](./samples/running-the-samples.md).</span></span>  
  
- <span data-ttu-id="07c3f-166">Jeśli klient korzysta z poświadczeń systemu Windows, a wyjątek to a <xref:System.ServiceModel.Security.SecurityNegotiationException> , skonfiguruj Kerberos w następujący sposób.</span><span class="sxs-lookup"><span data-stu-id="07c3f-166">If your client is using Windows credentials and the exception is a <xref:System.ServiceModel.Security.SecurityNegotiationException>, configure Kerberos as follows.</span></span>  
  
    1. <span data-ttu-id="07c3f-167">Dodaj poświadczenia tożsamości do elementu punktu końcowego w pliku App.config klienta:</span><span class="sxs-lookup"><span data-stu-id="07c3f-167">Add the identity credentials to the endpoint element in the client’s App.config file:</span></span>  
  
        ```xml
        <endpoint
          address="http://MyServer:8000/MyService/"
          binding="wsHttpBinding"
          bindingConfiguration="WSHttpBinding_IServiceExample"
          contract="IServiceExample"
          behaviorConfiguration="ClientCredBehavior"
          name="WSHttpBinding_IServiceExample">  
          <identity>  
            <userPrincipalName value="name@corp.contoso.com"/>  
          </identity>  
        </endpoint>  
        ```  
  
    2. <span data-ttu-id="07c3f-168">Uruchom usługę samoobsługową w ramach konta system lub NetworkService.</span><span class="sxs-lookup"><span data-stu-id="07c3f-168">Run the self-hosted service under the System or NetworkService account.</span></span> <span data-ttu-id="07c3f-169">Możesz uruchomić to polecenie, aby utworzyć okno polecenia w ramach konta systemowego:</span><span class="sxs-lookup"><span data-stu-id="07c3f-169">You can run this command to create a command window under the System account:</span></span>  
  
        ```console
        at 12:36 /interactive "cmd.exe"  
        ```  
  
    3. <span data-ttu-id="07c3f-170">Hostowanie usługi w obszarze Internet Information Services (IIS), która domyślnie używa konta głównej nazwy usługi (SPN).</span><span class="sxs-lookup"><span data-stu-id="07c3f-170">Host the service under Internet Information Services (IIS), which, by default, uses the service principal name (SPN) account.</span></span>  
  
    4. <span data-ttu-id="07c3f-171">Zarejestruj nową nazwę SPN z domeną przy użyciu narzędzia SetSPN.</span><span class="sxs-lookup"><span data-stu-id="07c3f-171">Register a new SPN with the domain using SetSPN.</span></span> <span data-ttu-id="07c3f-172">Aby to zrobić, musisz być administratorem domeny.</span><span class="sxs-lookup"><span data-stu-id="07c3f-172">You need to be a domain administrator in order to do this.</span></span>  
  
 <span data-ttu-id="07c3f-173">Aby uzyskać więcej informacji na temat protokołu Kerberos, zobacz [pojęcia dotyczące zabezpieczeń używane w programie WCF](./feature-details/security-concepts-used-in-wcf.md) i:</span><span class="sxs-lookup"><span data-stu-id="07c3f-173">For more information about the Kerberos protocol, see [Security Concepts Used in WCF](./feature-details/security-concepts-used-in-wcf.md) and:</span></span>  
  
- [<span data-ttu-id="07c3f-174">Debugowanie błędów uwierzytelniania systemu Windows</span><span class="sxs-lookup"><span data-stu-id="07c3f-174">Debugging Windows Authentication Errors</span></span>](./feature-details/debugging-windows-authentication-errors.md)  
  
- <span data-ttu-id="07c3f-175">[Rejestrowanie nazw głównych usługi Kerberos przy użyciu Http.sys](/previous-versions/sql/sql-server-2008-r2/ms178119(v=sql.105))</span><span class="sxs-lookup"><span data-stu-id="07c3f-175">[Registering Kerberos Service Principal Names by Using Http.sys](/previous-versions/sql/sql-server-2008-r2/ms178119(v=sql.105))</span></span>  
  
- <span data-ttu-id="07c3f-176">[Objaśnienie protokołu Kerberos](/previous-versions/windows/it-pro/windows-2000-server/bb742516(v=technet.10))</span><span class="sxs-lookup"><span data-stu-id="07c3f-176">[Kerberos Explained](/previous-versions/windows/it-pro/windows-2000-server/bb742516(v=technet.10))</span></span>  
  
<a name="BKMK_q5"></a>

## <a name="when-i-throw-a-faultexceptionexception-where-the-type-is-an-exception-i-always-receive-a-general-faultexception-type-on-the-client-and-not-the-generic-type-whats-happening"></a><span data-ttu-id="07c3f-177">Gdy zgłaszam wyjątek FaultException \<Exception> , którego typ jest wyjątkiem, zawsze otrzymuję ogólny typ błęduexception na kliencie, a nie typ ogólny.</span><span class="sxs-lookup"><span data-stu-id="07c3f-177">When I throw a FaultException\<Exception> where the type is an exception, I always receive a general FaultException type on the client and not the generic type.</span></span> <span data-ttu-id="07c3f-178">Co się dzieje?</span><span class="sxs-lookup"><span data-stu-id="07c3f-178">What’s happening?</span></span>  

 <span data-ttu-id="07c3f-179">Zdecydowanie zaleca się utworzenie własnego niestandardowego typu danych błędu i zadeklarowanie, że jako typ szczegółowy w umowie dotyczącej błędu.</span><span class="sxs-lookup"><span data-stu-id="07c3f-179">It is highly recommended that you create your own custom error data type and declare that as the detail type in your fault contract.</span></span> <span data-ttu-id="07c3f-180">Przyczyną jest użycie typów wyjątków dostarczonych przez system:</span><span class="sxs-lookup"><span data-stu-id="07c3f-180">The reason is that using system-provided exception types:</span></span>  
  
- <span data-ttu-id="07c3f-181">Tworzy zależność typu, która usuwa jedną z największych siły aplikacji zorientowanych na usługę.</span><span class="sxs-lookup"><span data-stu-id="07c3f-181">Creates a type dependency that removes one of the biggest strengths of service-oriented applications.</span></span>  
  
- <span data-ttu-id="07c3f-182">Nie może zależeć od wyjątków serializowanych w standardowy sposób.</span><span class="sxs-lookup"><span data-stu-id="07c3f-182">Cannot depend upon exceptions serializing in a standard way.</span></span> <span data-ttu-id="07c3f-183">Niektóre — takie jak <xref:System.Security.SecurityException> — nie można serializować.</span><span class="sxs-lookup"><span data-stu-id="07c3f-183">Some—like <xref:System.Security.SecurityException>—may not be serializable at all.</span></span>  
  
- <span data-ttu-id="07c3f-184">Udostępnia klientom szczegółowe informacje o implementacji wewnętrznej.</span><span class="sxs-lookup"><span data-stu-id="07c3f-184">Exposes internal implementation details to clients.</span></span> <span data-ttu-id="07c3f-185">Aby uzyskać więcej informacji, zobacz [określanie i obsługa błędów w kontraktach i usługach](specifying-and-handling-faults-in-contracts-and-services.md).</span><span class="sxs-lookup"><span data-stu-id="07c3f-185">For more information, see [Specifying and Handling Faults in Contracts and Services](specifying-and-handling-faults-in-contracts-and-services.md).</span></span>  
  
 <span data-ttu-id="07c3f-186">W przypadku debugowania aplikacji można jednak serializować informacje o wyjątkach i zwrócić je do klienta przy użyciu <xref:System.ServiceModel.Description.ServiceDebugBehavior> klasy.</span><span class="sxs-lookup"><span data-stu-id="07c3f-186">If you are debugging an application, however, you can serialize exception information and return it to the client by using the <xref:System.ServiceModel.Description.ServiceDebugBehavior> class.</span></span>  
  
<a name="BKMK_q6"></a>

## <a name="it-seems-like-one-way-and-request-reply-operations-return-at-roughly-the-same-speed-when-the-reply-contains-no-data-whats-happening"></a><span data-ttu-id="07c3f-187">Wygląda na to, że operacje jednokierunkowe i typu żądanie-odpowiedź są zwracane z tą samą szybkością, gdy odpowiedź nie zawiera żadnych danych.</span><span class="sxs-lookup"><span data-stu-id="07c3f-187">It seems like one-way and request-reply operations return at roughly the same speed when the reply contains no data.</span></span> <span data-ttu-id="07c3f-188">Co się dzieje?</span><span class="sxs-lookup"><span data-stu-id="07c3f-188">What's happening?</span></span>  

 <span data-ttu-id="07c3f-189">Określenie, że operacja jest jednym ze sposobów, że kontrakt operacji akceptuje komunikat wejściowy i nie zwraca komunikatu wyjściowego.</span><span class="sxs-lookup"><span data-stu-id="07c3f-189">Specifying that an operation is one way means only that the operation contract accepts an input message and does not return an output message.</span></span> <span data-ttu-id="07c3f-190">W programie WCF wszystkie wywołania klienta zwracają, gdy dane wychodzące zostały zapisaną do sieci lub zgłoszono wyjątek.</span><span class="sxs-lookup"><span data-stu-id="07c3f-190">In WCF, all client invocations return when the outbound data has been written to the wire or an exception is thrown.</span></span> <span data-ttu-id="07c3f-191">Operacje jednokierunkowe działają w ten sam sposób i mogą zgłosić, czy usługa nie może zostać zlokalizowana lub zablokować, jeśli usługa nie jest przygotowana do akceptowania danych z sieci.</span><span class="sxs-lookup"><span data-stu-id="07c3f-191">One-way operations work the same way, and they can throw if the service cannot be located or block if the service is not prepared to accept the data from the network.</span></span> <span data-ttu-id="07c3f-192">Zwykle w programie WCF skutkiem wywołania jednokierunkowego powracają do klienta szybciej niż żądanie-odpowiedź; Jednak każdy warunek, który spowalnia wysyłanie danych wychodzących za pośrednictwem sieci, spowalnia operacje jednokierunkowe oraz operacje odpowiedzi na żądanie.</span><span class="sxs-lookup"><span data-stu-id="07c3f-192">Typically in WCF, this results in one-way calls returning to the client more quickly than request-reply; but any condition that slows the sending of the outbound data over the network slows one-way operations as well as request-reply operations.</span></span> <span data-ttu-id="07c3f-193">Aby uzyskać więcej informacji, zobacz jednokierunkowe [usługi](./feature-details/one-way-services.md) i [dostęp do usług przy użyciu klienta WCF](./feature-details/accessing-services-using-a-client.md).</span><span class="sxs-lookup"><span data-stu-id="07c3f-193">For more information, see [One-Way Services](./feature-details/one-way-services.md) and [Accessing Services Using a WCF Client](./feature-details/accessing-services-using-a-client.md).</span></span>  
  
<a name="BKMK_q77"></a>

## <a name="im-using-an-x509-certificate-with-my-service-and-i-get-a-systemsecuritycryptographycryptographicexception-whats-happening"></a><span data-ttu-id="07c3f-194">Używam certyfikatu X. 509 z moją usługą i otrzymuję system. Security. Cryptography. CryptographicException.</span><span class="sxs-lookup"><span data-stu-id="07c3f-194">I’m using an X.509 certificate with my service and I get a System.Security.Cryptography.CryptographicException.</span></span> <span data-ttu-id="07c3f-195">Co się dzieje?</span><span class="sxs-lookup"><span data-stu-id="07c3f-195">What’s happening?</span></span>  

 <span data-ttu-id="07c3f-196">Jest to często spowodowane zmianą konta użytkownika, pod którym działa proces roboczy usług IIS.</span><span class="sxs-lookup"><span data-stu-id="07c3f-196">This commonly occurs after changing the user account under which the IIS worker process runs.</span></span> <span data-ttu-id="07c3f-197">Jeśli na przykład w systemie Windows XP zmienisz domyślne konto użytkownika, na którym jest uruchamiane Aspnet_wp.exe z poziomu ASPNET na niestandardowe konto użytkownika, ten błąd może zostać wyświetlony.</span><span class="sxs-lookup"><span data-stu-id="07c3f-197">For example, in Windows XP, if you change the default user account that the Aspnet_wp.exe runs under from ASPNET to a custom user account, you may see this error.</span></span> <span data-ttu-id="07c3f-198">W przypadku korzystania z klucza prywatnego proces korzystający z niego musi mieć uprawnienia dostępu do pliku przechowującego ten klucz.</span><span class="sxs-lookup"><span data-stu-id="07c3f-198">If using a private key, the process that uses it will need to have permissions to access the file storing that key.</span></span>  
  
 <span data-ttu-id="07c3f-199">W takim przypadku należy nadać uprawnienia dostępu do odczytu kontu tego procesu dla pliku zawierającego klucz prywatny.</span><span class="sxs-lookup"><span data-stu-id="07c3f-199">If this is the case, you must give read access privileges to the process's account for the file containing the private key.</span></span> <span data-ttu-id="07c3f-200">Na przykład jeśli proces roboczy usług IIS jest uruchomiony na koncie Roberta, należy dać plikowi z dostępem do odczytu do pliku zawierającego klucz prywatny.</span><span class="sxs-lookup"><span data-stu-id="07c3f-200">For example, if the IIS worker process is running under the Bob account, then you will need to give Bob read access to the file containing the private key.</span></span>  
  
 <span data-ttu-id="07c3f-201">Aby uzyskać więcej informacji o tym, jak nadawać poprawnemu kontu użytkownika dostęp do pliku, który zawiera klucz prywatny dla określonego certyfikatu X. 509, zobacz [How to: Make x. 509 Certificates dostępne dla WCF](./feature-details/how-to-make-x-509-certificates-accessible-to-wcf.md).</span><span class="sxs-lookup"><span data-stu-id="07c3f-201">For more information about how to give the correct user account access to the file that contains the private key for a specific X.509 certificate, see [How to: Make X.509 Certificates Accessible to WCF](./feature-details/how-to-make-x-509-certificates-accessible-to-wcf.md).</span></span>  
  
<a name="BKMK_q88"></a>

## <a name="i-changed-the-first-parameter-of-an-operation-from-uppercase-to-lowercase-now-my-client-throws-an-exception-whats-happening"></a><span data-ttu-id="07c3f-202">Pierwszy parametr operacji został zmieniony z wielkich na małe litery; teraz mój klient zgłasza wyjątek.</span><span class="sxs-lookup"><span data-stu-id="07c3f-202">I changed the first parameter of an operation from uppercase to lowercase; now my client throws an exception.</span></span> <span data-ttu-id="07c3f-203">Co się dzieje?</span><span class="sxs-lookup"><span data-stu-id="07c3f-203">What's happening?</span></span>  

 <span data-ttu-id="07c3f-204">Wartości nazw parametrów w sygnaturze operacji są częścią kontraktu i uwzględniają wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="07c3f-204">The values of the parameter names in the operation signature are part of the contract and are case-sensitive.</span></span> <span data-ttu-id="07c3f-205">Użyj <xref:System.ServiceModel.MessageParameterAttribute?displayProperty=nameWithType> atrybutu, gdy musisz rozróżnić nazwę parametru lokalnego i metadane opisujące operację dla aplikacji klienckich.</span><span class="sxs-lookup"><span data-stu-id="07c3f-205">Use the <xref:System.ServiceModel.MessageParameterAttribute?displayProperty=nameWithType> attribute when you need to distinguish between the local parameter name and the metadata that describes the operation for client applications.</span></span>  
  
<a name="BKMK_q99"></a>

## <a name="im-using-one-of-my-tracing-tools-and-i-get-an-endpointnotfoundexception-whats-happening"></a><span data-ttu-id="07c3f-206">Używam jednego z narzędzi do śledzenia i otrzymuję EndpointNotFoundException.</span><span class="sxs-lookup"><span data-stu-id="07c3f-206">I’m using one of my tracing tools and I get an EndpointNotFoundException.</span></span> <span data-ttu-id="07c3f-207">Co się dzieje?</span><span class="sxs-lookup"><span data-stu-id="07c3f-207">What’s happening?</span></span>  

 <span data-ttu-id="07c3f-208">Jeśli używasz narzędzia śledzenia, które nie jest mechanizmem śledzenia WCF dostarczonym przez system i otrzymasz komunikat informujący, że wystąpił <xref:System.ServiceModel.EndpointNotFoundException> niezgodność filtru adresów, musisz użyć <xref:System.ServiceModel.Description.ClientViaBehavior> klasy, aby skierować komunikaty do narzędzia śledzenia, a narzędzie przekieruje te komunikaty do adresu usługi.</span><span class="sxs-lookup"><span data-stu-id="07c3f-208">If you are using a tracing tool that is not the system-provided WCF tracing mechanism and you receive an <xref:System.ServiceModel.EndpointNotFoundException> that indicates that there was an address filter mismatch, you need to use the <xref:System.ServiceModel.Description.ClientViaBehavior> class to direct the messages to the tracing utility and have the utility redirect those messages to the service address.</span></span> <span data-ttu-id="07c3f-209"><xref:System.ServiceModel.Description.ClientViaBehavior>Klasa zmienia `Via` nagłówek adresowania, aby określić Następny adres sieciowy niezależnie od odbiorcy końcowego, wskazywany przez `To` nagłówek adresowania.</span><span class="sxs-lookup"><span data-stu-id="07c3f-209">The <xref:System.ServiceModel.Description.ClientViaBehavior> class alters the `Via` addressing header to specify the next network address separately from the ultimate receiver, indicated by the `To` addressing header.</span></span> <span data-ttu-id="07c3f-210">W takim przypadku nie należy zmieniać adresu punktu końcowego, który jest używany do ustanowienia `To` wartości.</span><span class="sxs-lookup"><span data-stu-id="07c3f-210">When doing this, however, do not change the endpoint address, which is used to establish the `To` value.</span></span>  
  
 <span data-ttu-id="07c3f-211">Poniższy przykład kodu przedstawia przykładowy plik konfiguracji klienta.</span><span class="sxs-lookup"><span data-stu-id="07c3f-211">The following code example shows an example client configuration file.</span></span>  
  
```xml
<endpoint
  address="http://localhost:8000/MyServer/"  
  binding="wsHttpBinding"  
  bindingConfiguration="WSHttpBinding_IMyContract"  
  behaviorConfiguration="MyClient"
  contract="IMyContract"
  name="WSHttpBinding_IMyContract">  
</endpoint>  
<behaviors>  
  <endpointBehaviors>  
    <behavior name="MyClient">  
      <clientVia viaUri="http://localhost:8001/MyServer/"/>  
    </behavior>  
  </endpointBehaviors>  
</behaviors>  
```  
  
<a name="BKMK_q10"></a>

## <a name="what-is-the-base-address-how-does-it-relate-to-an-endpoint-address"></a><span data-ttu-id="07c3f-212">Jaki jest adres podstawowy?</span><span class="sxs-lookup"><span data-stu-id="07c3f-212">What is the base address?</span></span> <span data-ttu-id="07c3f-213">Jak odnosi się do adresu punktu końcowego?</span><span class="sxs-lookup"><span data-stu-id="07c3f-213">How does it relate to an endpoint address?</span></span>  

 <span data-ttu-id="07c3f-214">Adres podstawowy jest adresem głównym <xref:System.ServiceModel.ServiceHost> klasy.</span><span class="sxs-lookup"><span data-stu-id="07c3f-214">A base address is the root address for a <xref:System.ServiceModel.ServiceHost> class.</span></span> <span data-ttu-id="07c3f-215">Domyślnie po dodaniu <xref:System.ServiceModel.Description.ServiceMetadataBehavior> klasy do konfiguracji usługi Web Services Description Language (WSDL) dla wszystkich punktów końcowych publikowanych przez hosta są pobierane z adresu podstawowego http, a także do wszystkich adresów względnych przekazywanych do zachowania metadanych, a także "? WSDL".</span><span class="sxs-lookup"><span data-stu-id="07c3f-215">By default, if you add a <xref:System.ServiceModel.Description.ServiceMetadataBehavior> class into your service configuration, the Web Services Description Language (WSDL) for all endpoints the host publishes are retrieved from the HTTP base address, plus any relative address provided to the metadata behavior, plus "?wsdl".</span></span> <span data-ttu-id="07c3f-216">Jeśli znasz usługi ASP.NET i IIS, adres podstawowy jest równoważny z katalogiem wirtualnym.</span><span class="sxs-lookup"><span data-stu-id="07c3f-216">If you are familiar with ASP.NET and IIS, the base address is equivalent to the virtual directory.</span></span>  
  
## <a name="sharing-a-port-between-a-service-endpoint-and-a-mex-endpoint-using-the-nettcpbinding"></a><span data-ttu-id="07c3f-217">Udostępnianie portu między punktem końcowym usługi a punktem końcowym MEX przy użyciu NetTcpBinding</span><span class="sxs-lookup"><span data-stu-id="07c3f-217">Sharing a port between a service endpoint and a mex endpoint using the NetTcpBinding</span></span>  

 <span data-ttu-id="07c3f-218">W przypadku określenia adresu podstawowego dla usługi jako net. TCP://MyServer: 8080/moje usługi i dodania następujących punktów końcowych:</span><span class="sxs-lookup"><span data-stu-id="07c3f-218">If you specify the base address for a service as net.tcp://MyServer:8080/MyService and add the following endpoints:</span></span>  
  
```xml  
<services>  
  <service name="Microsoft.Samples.NetTcp.CalculatorService">  
    <endpoint address="calcsvc" binding ="netTcpBinding" contract="Microsoft.Samples.NetTcp.ICalculator"/>  
    <endpoint address="mex" binding="mexTcpBinding" contract="IMetadataExchange" />  
  </service>  
</services>  
```  
  
 <span data-ttu-id="07c3f-219">A jeśli zmodyfikujesz jedno z ustawień NetTcpBinding, jak pokazano w poniższym fragmencie kodu:</span><span class="sxs-lookup"><span data-stu-id="07c3f-219">And if you modify one of the NetTcpBinding settings as shown in the following configuration snippet:</span></span>  
  
```xml  
<bindings>  
  <netTcpBinding>  
    <binding closeTimeout="00:01:00" openTimeout="00:01:00" receiveTimeout="00:10:00" sendTimeout="00:01:00" transactionFlow="false" transferMode="Buffered" transactionProtocol="OleTransactions" hostNameComparisonMode="StrongWildcard" listenBacklog="10" maxBufferPoolSize="524288" maxBufferSize="65536" maxConnections="11" maxReceivedMessageSize="65536">  
      <readerQuotas maxDepth="32" maxStringContentLength="8192" maxArrayLength="16384" maxBytesPerRead="4096" maxNameTableCharCount="16384"/>  
      <reliableSession ordered="true" inactivityTimeout="00:10:00" enabled="false"/>  
      <security mode="Transport">  
        <transport clientCredentialType="Windows" protectionLevel="EncryptAndSign"/>  
      </security>  
    </binding>  
  </netTcpBinding>  
</bindings>  
```  
  
 <span data-ttu-id="07c3f-220">Zobaczysz błąd podobny do następującego: nieobsłużony wyjątek: System. ServiceModel. AddressAlreadyInUseException —: istnieje już odbiornik w punkcie końcowym IP 0.0.0.0:9000 można obejść ten błąd, określając w pełni kwalifikowany adres URL z innym portem dla punktu końcowego MEX, jak pokazano w poniższym fragmencie kodu:</span><span class="sxs-lookup"><span data-stu-id="07c3f-220">You will see an error like the following: Unhandled Exception: System.ServiceModel.AddressAlreadyInUseException: There is already a listener on IP endpoint 0.0.0.0:9000 You can work around this error by specifying a fully qualified URL with a different port for the MEX endpoint as shown in the following configuration snippet:</span></span>  
  
```xml
<services>  
  <service name="Microsoft.Samples.NetTcp.CalculatorService">  
    <endpoint address="calcsvc" binding ="netTcpBinding" contract="Microsoft.Samples.NetTcp.ICalculator"/>  
    <endpoint address="net.tcp://localhost:9001/servicemodelsamples/mex" binding="mexTcpBinding" contract="IMetadataExchange" />  
  </service>  
</services>  
```  
  
<a name="BK_MK99"></a>

## <a name="when-calling-a-wcf-web-http-application-from-a-wcf-soap-application-the-service-returns-the-following-error-405-method-not-allowed"></a><span data-ttu-id="07c3f-221">Podczas wywoływania aplikacji HTTP sieci Web WCF z aplikacji SOAP WCF usługa zwraca następujący błąd: Metoda 405 nie jest dozwolona</span><span class="sxs-lookup"><span data-stu-id="07c3f-221">When calling a WCF Web HTTP application from a WCF SOAP application the service returns the following error: 405 Method Not Allowed</span></span>  

 <span data-ttu-id="07c3f-222">Wywołanie aplikacji HTTP sieci Web w programie WCF (usługa, która korzysta z <xref:System.ServiceModel.WebHttpBinding> i <xref:System.ServiceModel.Description.WebHttpBehavior> ) z usługi WCF, może wygenerować następujący wyjątek: ``Unhandled Exception: System.ServiceModel.FaultException`1[System.ServiceModel.ExceptionDetail]: The remote server returned an unexpected response: (405) Method Not Allowed.`` ten wyjątek występuje, ponieważ program WCF zastępuje wychodzące dane <xref:System.ServiceModel.OperationContext> przychodzące z przychodzącą <xref:System.ServiceModel.OperationContext> .</span><span class="sxs-lookup"><span data-stu-id="07c3f-222">Calling a WCF Web HTTP application (a service that uses the <xref:System.ServiceModel.WebHttpBinding> and <xref:System.ServiceModel.Description.WebHttpBehavior>) from a WCF service may generate the following exception: ``Unhandled Exception: System.ServiceModel.FaultException`1[System.ServiceModel.ExceptionDetail]: The remote server returned an unexpected response: (405) Method Not Allowed.`` This exception occurs because WCF overwrites the outgoing <xref:System.ServiceModel.OperationContext> with the incoming <xref:System.ServiceModel.OperationContext>.</span></span> <span data-ttu-id="07c3f-223">Aby rozwiązać ten problem, należy utworzyć <xref:System.ServiceModel.OperationContextScope> w ramach operacji usługi HTTP sieci Web w programie WCF.</span><span class="sxs-lookup"><span data-stu-id="07c3f-223">To solve this problem, create an <xref:System.ServiceModel.OperationContextScope> within the WCF Web HTTP service operation.</span></span> <span data-ttu-id="07c3f-224">Przykład:</span><span class="sxs-lookup"><span data-stu-id="07c3f-224">For example:</span></span>  
  
```csharp
public string Echo(string input)  
{  
    using (new OperationContextScope(this.InnerChannel))  
    {  
        return base.Channel.Echo(input);  
    }  
}  
```  
  
## <a name="see-also"></a><span data-ttu-id="07c3f-225">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="07c3f-225">See also</span></span>

- [<span data-ttu-id="07c3f-226">Debugowanie błędów uwierzytelniania systemu Windows</span><span class="sxs-lookup"><span data-stu-id="07c3f-226">Debugging Windows Authentication Errors</span></span>](./feature-details/debugging-windows-authentication-errors.md)
