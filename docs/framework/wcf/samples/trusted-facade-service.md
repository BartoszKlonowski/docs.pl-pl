---
title: Zaufana usługa fasady
ms.date: 03/30/2017
ms.assetid: c34d1a8f-e45e-440b-a201-d143abdbac38
ms.openlocfilehash: e9459b4cc26ef85adcc59c308d92491fd2d3acba
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/15/2020
ms.locfileid: "90544183"
---
# <a name="trusted-facade-service"></a><span data-ttu-id="8e330-102">Zaufana usługa fasady</span><span class="sxs-lookup"><span data-stu-id="8e330-102">Trusted Facade Service</span></span>
<span data-ttu-id="8e330-103">W tym scenariuszu przedstawiono sposób przepływu informacji o tożsamości wywołującego z jednej usługi do innej przy użyciu infrastruktury zabezpieczeń Windows Communication Foundation (WCF).</span><span class="sxs-lookup"><span data-stu-id="8e330-103">This scenario sample demonstrates how to flow caller's identity information from one service to another using Windows Communication Foundation (WCF) security infrastructure.</span></span>  
  
 <span data-ttu-id="8e330-104">Typowym wzorcem projektu jest udostępnienie funkcjonalności oferowanej przez usługę do sieci publicznej za pomocą usługi fasadowej.</span><span class="sxs-lookup"><span data-stu-id="8e330-104">It is a common design pattern to expose the functionality provided by a service to the public network using a façade service.</span></span> <span data-ttu-id="8e330-105">Usługa elewacji zwykle znajduje się w sieci obwodowej (znanej także jako Strefa DMZ, zdemilitaryzowana Zone i podsieć z osłoną) i komunikuje się z usługą zaplecza, która implementuje logikę biznesową i ma dostęp do danych wewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="8e330-105">The façade service typically resides in the perimeter network (also known as DMZ, demilitarized zone, and screened subnet) and communicates with a backend service that implements the business logic and has access to internal data.</span></span> <span data-ttu-id="8e330-106">Kanał komunikacyjny między usługą fasady a usługą zaplecza przechodzi przez zaporę i jest zwykle ograniczony tylko do jednego celu.</span><span class="sxs-lookup"><span data-stu-id="8e330-106">The communication channel between the façade service and the backend service goes through a firewall and is usually limited for a single purpose only.</span></span>  
  
 <span data-ttu-id="8e330-107">Ten przykład składa się z następujących składników:</span><span class="sxs-lookup"><span data-stu-id="8e330-107">This sample consists of the following components:</span></span>  
  
- <span data-ttu-id="8e330-108">Klient kalkulatora</span><span class="sxs-lookup"><span data-stu-id="8e330-108">Calculator client</span></span>  
  
- <span data-ttu-id="8e330-109">Usługa "elewacja" usługi Kalkulator</span><span class="sxs-lookup"><span data-stu-id="8e330-109">Calculator façade service</span></span>  
  
- <span data-ttu-id="8e330-110">Usługa zaplecza programu Kalkulator</span><span class="sxs-lookup"><span data-stu-id="8e330-110">Calculator backend service</span></span>  
  
 <span data-ttu-id="8e330-111">Usługa fasady jest odpowiedzialna za sprawdzenie poprawności żądania i uwierzytelnienie obiektu wywołującego.</span><span class="sxs-lookup"><span data-stu-id="8e330-111">The façade service is responsible for validating the request and authenticating the caller.</span></span> <span data-ttu-id="8e330-112">Po pomyślnym uwierzytelnieniu i sprawdzeniu zostanie przekazane żądanie do usługi wewnętrznej bazy danych przy użyciu kontrolowanego kanału komunikacyjnego z sieci obwodowej do sieci wewnętrznej.</span><span class="sxs-lookup"><span data-stu-id="8e330-112">After successful authentication and validation, it forwards the request to the backend service using the controlled communication channel from the perimeter network to the internal network.</span></span> <span data-ttu-id="8e330-113">W ramach przekazanego żądania usługa elewacji zawiera informacje o tożsamości wywołującego, dzięki czemu usługa zaplecza może używać tych informacji w jego przetwarzaniu.</span><span class="sxs-lookup"><span data-stu-id="8e330-113">As a part of the forwarded request, the façade service includes information about the caller's identity so that the backend service can use this information in its processing.</span></span> <span data-ttu-id="8e330-114">Tożsamość obiektu wywołującego jest przekazywana przy użyciu `Username` tokenu zabezpieczającego wewnątrz `Security` nagłówka komunikatu.</span><span class="sxs-lookup"><span data-stu-id="8e330-114">The caller's identity is transmitted using a `Username` security token inside the message `Security` header.</span></span> <span data-ttu-id="8e330-115">Przykład używa infrastruktury zabezpieczeń WCF do przesyłania i wyodrębniania tych informacji z `Security` nagłówka.</span><span class="sxs-lookup"><span data-stu-id="8e330-115">The sample uses the WCF security infrastructure to transmit and extract this information from the `Security` header.</span></span>  
  
> [!IMPORTANT]
> <span data-ttu-id="8e330-116">Usługa zaplecza ufa usłudze elewacji do uwierzytelniania obiektu wywołującego.</span><span class="sxs-lookup"><span data-stu-id="8e330-116">The backend service trusts the façade service to authenticate the caller.</span></span> <span data-ttu-id="8e330-117">W związku z tym usługa zaplecza nie uwierzytelnia ponownie obiektu wywołującego; używa on informacji o tożsamości dostarczonych przez usługę elewacji w żądaniu przekazywanym dalej.</span><span class="sxs-lookup"><span data-stu-id="8e330-117">Because of this, the backend service does not authenticate the caller again; it uses the identity information provided by the façade service in the forwarded request.</span></span> <span data-ttu-id="8e330-118">Ze względu na tę relację zaufania usługa zaplecza musi uwierzytelnić usługę elewacji, aby upewnić się, że przekazany komunikat pochodzi z zaufanego źródła — w tym przypadku usługi elewacji.</span><span class="sxs-lookup"><span data-stu-id="8e330-118">Because of this trust relationship, the backend service must authenticate the façade service to ensure that the forwarded message comes from a trusted source - in this case, the façade service.</span></span>  
  
## <a name="implementation"></a><span data-ttu-id="8e330-119">Implementacja</span><span class="sxs-lookup"><span data-stu-id="8e330-119">Implementation</span></span>  
 <span data-ttu-id="8e330-120">W tym przykładzie istnieją dwie ścieżki komunikacji.</span><span class="sxs-lookup"><span data-stu-id="8e330-120">There are two communication paths in this sample.</span></span> <span data-ttu-id="8e330-121">Po pierwsze jest między klientem a usługą elewacji drugi między usługą elewacji a usługą zaplecza.</span><span class="sxs-lookup"><span data-stu-id="8e330-121">First is between the client and the façade service, the second is between the façade service and the backend service.</span></span>  
  
### <a name="communication-path-between-client-and-faade-service"></a><span data-ttu-id="8e330-122">Ścieżka komunikacji między klientem a usługą elewacji</span><span class="sxs-lookup"><span data-stu-id="8e330-122">Communication Path between Client and Façade Service</span></span>  
 <span data-ttu-id="8e330-123">Klient do ścieżki komunikacji usługi elewacji używa `wsHttpBinding` z `UserName` typem poświadczeń klienta.</span><span class="sxs-lookup"><span data-stu-id="8e330-123">The client to the façade service communication path uses `wsHttpBinding` with a `UserName` client credential type.</span></span> <span data-ttu-id="8e330-124">Oznacza to, że klient używa nazwy użytkownika i hasła do uwierzytelniania w usłudze elewacji, a usługa fasada używa certyfikatu X. 509 do uwierzytelniania na kliencie.</span><span class="sxs-lookup"><span data-stu-id="8e330-124">This means that the client uses username and password to authenticate to the façade service and the façade service uses X.509 certificate to authenticate to the client.</span></span> <span data-ttu-id="8e330-125">Konfiguracja powiązania wygląda podobnie do poniższego przykładu.</span><span class="sxs-lookup"><span data-stu-id="8e330-125">The binding configuration looks like the following example.</span></span>  
  
```xml  
<bindings>  
  <wsHttpBinding>  
    <binding name="Binding1">  
      <security mode="Message">  
        <message clientCredentialType="UserName"/>  
      </security>  
    </binding>  
  </wsHttpBinding>  
</bindings>  
```  
  
 <span data-ttu-id="8e330-126">Usługa elewacji uwierzytelnia obiekt wywołujący przy użyciu `UserNamePasswordValidator` implementacji niestandardowej.</span><span class="sxs-lookup"><span data-stu-id="8e330-126">The façade service authenticates the caller using custom `UserNamePasswordValidator` implementation.</span></span> <span data-ttu-id="8e330-127">W celach demonstracyjnych uwierzytelnianie gwarantuje, że nazwa użytkownika wywołującego jest zgodna z przedstawionym hasłem.</span><span class="sxs-lookup"><span data-stu-id="8e330-127">For demonstration purposes, the authentication only ensures that the caller's username matches the presented password.</span></span> <span data-ttu-id="8e330-128">W świecie rzeczywistym użytkownik jest prawdopodobnie uwierzytelniany przy użyciu Active Directory lub niestandardowego dostawcy członkostwa ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="8e330-128">In the real world situation, the user is probably authenticated using Active Directory or custom ASP.NET Membership provider.</span></span> <span data-ttu-id="8e330-129">Implementacja modułu sprawdzania poprawności znajduje się w `FacadeService.cs` pliku.</span><span class="sxs-lookup"><span data-stu-id="8e330-129">The validator implementation resides in `FacadeService.cs` file.</span></span>  
  
```csharp  
public class MyUserNamePasswordValidator : UserNamePasswordValidator  
{  
    public override void Validate(string userName, string password)  
    {  
        // check that username matches password  
        if (null == userName || userName != password)  
        {  
            Console.WriteLine("Invalid username or password");  
            throw new SecurityTokenValidationException(  
                       "Invalid username or password");  
        }  
    }  
}  
```  
  
 <span data-ttu-id="8e330-130">Niestandardowy moduł sprawdzania poprawności jest skonfigurowany do użycia wewnątrz `serviceCredentials` zachowania w pliku konfiguracji usługi elewacji.</span><span class="sxs-lookup"><span data-stu-id="8e330-130">The custom validator is configured to be used inside the `serviceCredentials` behavior in the façade service configuration file.</span></span> <span data-ttu-id="8e330-131">To zachowanie służy również do konfigurowania certyfikatu X. 509 usługi.</span><span class="sxs-lookup"><span data-stu-id="8e330-131">This behavior is also used to configure the service's X.509 certificate.</span></span>  
  
```xml  
<behaviors>  
  <serviceBehaviors>  
    <behavior name="FacadeServiceBehavior">  
      <!--The serviceCredentials behavior allows you to define -->  
      <!--a service certificate. -->  
      <!--A service certificate is used by the service to  -->  
      <!--authenticate itself to its clients and to provide  -->  
      <!--message protection. -->  
      <!--This configuration references the "localhost"  -->  
      <!--certificate installed during the setup instructions. -->  
      <serviceCredentials>  
        <serviceCertificate
               findValue="localhost"
               storeLocation="LocalMachine"
               storeName="My"
               x509FindType="FindBySubjectName" />  
        <userNameAuthentication userNamePasswordValidationMode="Custom"  
            customUserNamePasswordValidatorType=  
           "Microsoft.ServiceModel.Samples.MyUserNamePasswordValidator,  
            FacadeService"/>  
      </serviceCredentials>  
    </behavior>  
  </serviceBehaviors>  
</behaviors>  
```  
  
### <a name="communication-path-between-faade-service-and-backend-service"></a><span data-ttu-id="8e330-132">Ścieżka komunikacji między usługą elewacji a usługą zaplecza</span><span class="sxs-lookup"><span data-stu-id="8e330-132">Communication Path between Façade Service and Backend Service</span></span>  
 <span data-ttu-id="8e330-133">Podnosząca się do ścieżki komunikacji usługi wewnętrznej bazy danych używa `customBinding` , która składa się z kilku elementów powiązania.</span><span class="sxs-lookup"><span data-stu-id="8e330-133">The façade service to the backend service communication path uses a `customBinding` that consists of several binding elements.</span></span> <span data-ttu-id="8e330-134">To powiązanie wykonuje dwie rzeczy.</span><span class="sxs-lookup"><span data-stu-id="8e330-134">This binding accomplishes two things.</span></span> <span data-ttu-id="8e330-135">Usługa ta uwierzytelnia usługę fasady i usługę zaplecza, aby upewnić się, że komunikacja jest bezpieczna i pochodzi z zaufanego źródła.</span><span class="sxs-lookup"><span data-stu-id="8e330-135">It authenticates the façade service and backend service to ensure that the communication is secure and is coming from a trusted source.</span></span> <span data-ttu-id="8e330-136">Ponadto również przesyła początkową tożsamość obiektu wywołującego wewnątrz `Username` tokenu zabezpieczającego.</span><span class="sxs-lookup"><span data-stu-id="8e330-136">Additionally, it also transmits the initial caller's identity inside the `Username` security token.</span></span> <span data-ttu-id="8e330-137">W takim przypadku tylko nazwa użytkownika początkowego obiektu wywołującego jest przesyłana do usługi wewnętrznej bazy danych, a hasło nie jest uwzględniane w komunikacie.</span><span class="sxs-lookup"><span data-stu-id="8e330-137">In this case, only the initial caller's username is transmitted to the backend service, the password is not included in the message.</span></span> <span data-ttu-id="8e330-138">Wynika to z faktu, że usługa zaplecza ufa usłudze elewacji do uwierzytelniania obiektu wywołującego przed przekazaniem do niego żądania.</span><span class="sxs-lookup"><span data-stu-id="8e330-138">This is because the backend service trusts the façade service to authenticate the caller before forwarding the request to it.</span></span> <span data-ttu-id="8e330-139">Ponieważ usługa fasady jest uwierzytelniana w usłudze wewnętrznej bazy danych, usługa zaplecza może ufać informacjom zawartym w żądaniu przekazywanym dalej.</span><span class="sxs-lookup"><span data-stu-id="8e330-139">Because the façade service authenticates itself to the backend service, the backend service can trust the information contained in the forwarded request.</span></span>  
  
 <span data-ttu-id="8e330-140">Poniżej znajduje się Konfiguracja powiązania dla tej ścieżki komunikacji.</span><span class="sxs-lookup"><span data-stu-id="8e330-140">The following is the binding configuration for this communication path.</span></span>  
  
```xml  
<bindings>  
  <customBinding>  
    <binding name="ClientBinding">  
      <security authenticationMode="UserNameOverTransport"/>  
      <windowsStreamSecurity/>  
      <tcpTransport/>  
    </binding>  
  </customBinding>  
</bindings>  
```  
  
 <span data-ttu-id="8e330-141">[\<security>](../../configure-apps/file-schema/wcf/security-of-custombinding.md)Element Binding bierze pod uwagę początkową transmisję i wyodrębnianie nazwy użytkownika.</span><span class="sxs-lookup"><span data-stu-id="8e330-141">The [\<security>](../../configure-apps/file-schema/wcf/security-of-custombinding.md) binding element takes care of the initial caller's username transmission and extraction.</span></span> <span data-ttu-id="8e330-142">[\<windowsStreamSecurity>](../../configure-apps/file-schema/wcf/windowsstreamsecurity.md)I [\<tcpTransport>](../../configure-apps/file-schema/wcf/tcptransport.md) zapoznaj się z uwierzytelnianiem fasady i usług zaplecza oraz ochrony komunikatów.</span><span class="sxs-lookup"><span data-stu-id="8e330-142">The [\<windowsStreamSecurity>](../../configure-apps/file-schema/wcf/windowsstreamsecurity.md) and [\<tcpTransport>](../../configure-apps/file-schema/wcf/tcptransport.md) take care of authenticating façade and backend services and message protection.</span></span>  
  
 <span data-ttu-id="8e330-143">Aby przesłać dalej żądanie, implementacja nieelewacji usługi musi dostarczyć nazwę użytkownika początkowego wywołującego, aby infrastruktura zabezpieczeń WCF mogła je umieścić w przekazywanym komunikacie.</span><span class="sxs-lookup"><span data-stu-id="8e330-143">To forward the request, the façade service implementation must provide the initial caller's username so that WCF security infrastructure can place this into the forwarded message.</span></span> <span data-ttu-id="8e330-144">Początkowa nazwa użytkownika wywołującego jest udostępniana w implementacji usługi fasadowej przez ustawienie jej we `ClientCredentials` właściwości w wystąpieniu serwera proxy klienta, która elewacji usługi używa do komunikowania się z usługą zaplecza.</span><span class="sxs-lookup"><span data-stu-id="8e330-144">The initial caller's username is provided in the façade service implementation by setting it in the `ClientCredentials` property on the client proxy instance that façade service uses to communicate with the backend service.</span></span>  
  
 <span data-ttu-id="8e330-145">Poniższy kod pokazuje, jak `GetCallerIdentity` Metoda jest zaimplementowana w usłudze elewacji.</span><span class="sxs-lookup"><span data-stu-id="8e330-145">The following code shows how `GetCallerIdentity` method is implemented on the façade service.</span></span> <span data-ttu-id="8e330-146">Inne metody używają tego samego wzorca.</span><span class="sxs-lookup"><span data-stu-id="8e330-146">Other methods use the same pattern.</span></span>  
  
```csharp  
public string GetCallerIdentity()  
{  
    CalculatorClient client = new CalculatorClient();  
    client.ClientCredentials.UserName.UserName = ServiceSecurityContext.Current.PrimaryIdentity.Name;  
    string result = client.GetCallerIdentity();  
    client.Close();  
    return result;  
}  
```  
  
 <span data-ttu-id="8e330-147">Jak pokazano w poprzednim kodzie, hasło nie jest ustawione dla `ClientCredentials` właściwości, tylko nazwa użytkownika jest ustawiona.</span><span class="sxs-lookup"><span data-stu-id="8e330-147">As shown in the previous code, the password is not set on the `ClientCredentials` property, only the username is set.</span></span> <span data-ttu-id="8e330-148">Infrastruktura zabezpieczeń WCF tworzy w tym przypadku token zabezpieczający username bez hasła, co jest dokładnie wymagane w tym scenariuszu.</span><span class="sxs-lookup"><span data-stu-id="8e330-148">WCF security infrastructure creates a username security token without a password in this case, which is exactly what is required in this scenario.</span></span>  
  
 <span data-ttu-id="8e330-149">W usłudze zaplecza informacje zawarte w tokenie zabezpieczeń username muszą zostać uwierzytelnione.</span><span class="sxs-lookup"><span data-stu-id="8e330-149">On the backend service, the information contained in the username security token must be authenticated.</span></span> <span data-ttu-id="8e330-150">Domyślnie zabezpieczenia WCF próbują zmapować użytkownika na konto systemu Windows przy użyciu podanego hasła.</span><span class="sxs-lookup"><span data-stu-id="8e330-150">By default, WCF security attempts to map the user to a Windows account using the provided password.</span></span> <span data-ttu-id="8e330-151">W takim przypadku nie podano hasła i usługa zaplecza nie jest wymagana do uwierzytelnienia nazwy użytkownika, ponieważ uwierzytelnianie zostało już wykonane przez usługę elewacji.</span><span class="sxs-lookup"><span data-stu-id="8e330-151">In this case, there is no password provided and the backend service is not required to authenticate the username because the authentication was already performed by the façade service.</span></span> <span data-ttu-id="8e330-152">W celu zaimplementowania tej funkcji w programie WCF zostanie udostępniona niestandardowa, `UserNamePasswordValidator` która wymusza, że nazwa użytkownika jest określona w tokenie i nie wykonuje dodatkowego uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="8e330-152">To implement this functionality in WCF, a custom `UserNamePasswordValidator` is provided that only enforces that a username is specified in the token and does not perform any additional authentication.</span></span>  
  
```csharp  
public class MyUserNamePasswordValidator : UserNamePasswordValidator  
{  
    public override void Validate(string userName, string password)  
    {  
        // Ignore the password because it is empty,
        // we trust the facade service to authenticate the client.  
        // Accept the username information here so that the
        // application gets access to it.  
        if (null == userName)  
        {  
            Console.WriteLine("Invalid username");  
            throw new
             SecurityTokenValidationException("Invalid username");  
        }  
    }  
}  
```  
  
 <span data-ttu-id="8e330-153">Niestandardowy moduł sprawdzania poprawności jest skonfigurowany do użycia wewnątrz `serviceCredentials` zachowania w pliku konfiguracji usługi elewacji.</span><span class="sxs-lookup"><span data-stu-id="8e330-153">The custom validator is configured to be used inside the `serviceCredentials` behavior in the façade service configuration file.</span></span>  
  
```xml  
<behaviors>  
  <serviceBehaviors>  
    <behavior name="BackendServiceBehavior">  
      <serviceCredentials>  
        <userNameAuthentication userNamePasswordValidationMode="Custom"  
           customUserNamePasswordValidatorType=  
          "Microsoft.ServiceModel.Samples.MyUserNamePasswordValidator,
           BackendService"/>  
      </serviceCredentials>  
    </behavior>  
  </serviceBehaviors>  
</behaviors>  
```  
  
 <span data-ttu-id="8e330-154">Aby wyodrębnić informacje o nazwie użytkownika i informacje o koncie usługi zaufanej elewacji, implementacja usługi wewnętrznej bazy danych używa `ServiceSecurityContext` klasy.</span><span class="sxs-lookup"><span data-stu-id="8e330-154">To extract the username information and information about the trusted façade service account, the backend service implementation uses the `ServiceSecurityContext` class.</span></span> <span data-ttu-id="8e330-155">Poniższy kod pokazuje, jak `GetCallerIdentity` Metoda jest zaimplementowana.</span><span class="sxs-lookup"><span data-stu-id="8e330-155">The following code shows how the `GetCallerIdentity` method is implemented.</span></span>  
  
```csharp  
public string GetCallerIdentity()  
{  
    // Facade service is authenticated using Windows authentication.  
    //Its identity is accessible.  
    // On ServiceSecurityContext.Current.WindowsIdentity.  
    string facadeServiceIdentityName =
          ServiceSecurityContext.Current.WindowsIdentity.Name;  
  
    // The client name is transmitted using Username authentication on
    //the message level without the password  
    // using a supporting encrypted UserNameToken.  
    // Claims extracted from this supporting token are available in
    // ServiceSecurityContext.Current.AuthorizationContext.ClaimSets
    // collection.  
    string clientName = null;  
    foreach (ClaimSet claimSet in
        ServiceSecurityContext.Current.AuthorizationContext.ClaimSets)  
    {  
        foreach (Claim claim in claimSet)  
        {  
            if (claim.ClaimType == ClaimTypes.Name &&
                                   claim.Right == Rights.Identity)  
            {  
                clientName = (string)claim.Resource;  
                break;  
            }  
        }  
    }  
    if (clientName == null)  
    {  
        // In case there was no UserNameToken attached to the request.  
        // In the real world implementation the service should reject
        // this request.  
        return "Anonymous caller via " + facadeServiceIdentityName;  
    }  
  
    return clientName + " via " + facadeServiceIdentityName;  
}  
```  
  
 <span data-ttu-id="8e330-156">Informacje o koncie usługi fasady są wyodrębniane przy użyciu `ServiceSecurityContext.Current.WindowsIdentity` właściwości.</span><span class="sxs-lookup"><span data-stu-id="8e330-156">The façade service account information is extracted using the `ServiceSecurityContext.Current.WindowsIdentity` property.</span></span> <span data-ttu-id="8e330-157">Aby uzyskać dostęp do informacji o początkowym wywołującym, usługa zaplecza używa `ServiceSecurityContext.Current.AuthorizationContext.ClaimSets` właściwości.</span><span class="sxs-lookup"><span data-stu-id="8e330-157">To access the information about the initial caller the backend service uses the `ServiceSecurityContext.Current.AuthorizationContext.ClaimSets` property.</span></span> <span data-ttu-id="8e330-158">Szuka on `Identity` zgłoszenia z typem `Name` .</span><span class="sxs-lookup"><span data-stu-id="8e330-158">It looks for an `Identity` claim with a type `Name`.</span></span> <span data-ttu-id="8e330-159">To zgłoszenie jest generowane automatycznie przez infrastrukturę zabezpieczeń WCF z informacji zawartych w `Username` tokenie zabezpieczającym.</span><span class="sxs-lookup"><span data-stu-id="8e330-159">This claim is automatically generated by WCF security infrastructure from the information contained in the `Username` security token.</span></span>  
  
## <a name="running-the-sample"></a><span data-ttu-id="8e330-160">Uruchamianie przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="8e330-160">Running the sample</span></span>  
 <span data-ttu-id="8e330-161">Po uruchomieniu przykładu żądania operacji i odpowiedzi są wyświetlane w oknie konsoli klienta.</span><span class="sxs-lookup"><span data-stu-id="8e330-161">When you run the sample, the operation requests and responses are displayed in the client console window.</span></span> <span data-ttu-id="8e330-162">Naciśnij klawisz ENTER w oknie klienta, aby zamknąć klienta programu.</span><span class="sxs-lookup"><span data-stu-id="8e330-162">Press ENTER in the client window to shut down the client.</span></span> <span data-ttu-id="8e330-163">Aby zamknąć usługi, możesz nacisnąć klawisz ENTER w oknach konsoli usługi elewacji i zaplecza.</span><span class="sxs-lookup"><span data-stu-id="8e330-163">You can press ENTER in the façade and backend service console windows to shut down the services.</span></span>  
  
```console  
Username authentication required.  
Provide a valid machine or domain ac  
   Enter username:  
user  
   Enter password:  
****  
user via MyMachine\testaccount  
Add(100,15.99) = 115.99  
Subtract(145,76.54) = 68.46  
Multiply(9,81.25) = 731.25  
Divide(22,7) = 3.14285714285714  
  
Press <ENTER> to terminate client.  
```  
  
 <span data-ttu-id="8e330-164">Plik wsadowy Setup.bat dołączony do przykładu zaufanego scenariusza zaufana fasady umożliwia skonfigurowanie serwera z odpowiednim certyfikatem w celu uruchomienia usługi fasady wymagającej zabezpieczeń opartych na certyfikatach do samodzielnego uwierzytelnienia klienta.</span><span class="sxs-lookup"><span data-stu-id="8e330-164">The Setup.bat batch file included with the Trusted Facade scenario sample enables you to configure the server with a relevant certificate to run the façade service that requires certificate-based security to authenticate itself to the client.</span></span> <span data-ttu-id="8e330-165">Aby uzyskać szczegółowe informacje, zobacz procedurę instalacji na końcu tego tematu.</span><span class="sxs-lookup"><span data-stu-id="8e330-165">See the setup procedure at the end of this topic for details.</span></span>  
  
 <span data-ttu-id="8e330-166">Poniżej przedstawiono krótkie omówienie różnych sekcji plików wsadowych.</span><span class="sxs-lookup"><span data-stu-id="8e330-166">The following provides a brief overview of the different sections of the batch files.</span></span>  
  
- <span data-ttu-id="8e330-167">Tworzenie certyfikatu serwera.</span><span class="sxs-lookup"><span data-stu-id="8e330-167">Creating the server certificate.</span></span>  
  
     <span data-ttu-id="8e330-168">Poniższe wiersze z pliku wsadowego Setup.bat utworzyć certyfikat serwera do użycia.</span><span class="sxs-lookup"><span data-stu-id="8e330-168">The following lines from the Setup.bat batch file create the server certificate to be used.</span></span>  
  
    ```console  
    echo ************  
    echo Server cert setup starting  
    echo %SERVER_NAME%  
    echo ************  
    echo making server cert  
    echo ************  
    makecert.exe -sr LocalMachine -ss MY -a sha1 -n CN=%SERVER_NAME% -sky exchange -pe  
    ```  
  
     <span data-ttu-id="8e330-169">`%SERVER_NAME%`Zmienna określa nazwę serwera — wartość domyślna to localhost.</span><span class="sxs-lookup"><span data-stu-id="8e330-169">The `%SERVER_NAME%` variable specifies the server name - the default value is localhost.</span></span> <span data-ttu-id="8e330-170">Certyfikat jest przechowywany w magazynie LocalMachine.</span><span class="sxs-lookup"><span data-stu-id="8e330-170">The certificate is stored in the LocalMachine store.</span></span>  
  
- <span data-ttu-id="8e330-171">Instalowanie certyfikatu usługi elewacji w zaufanym magazynie certyfikatów klienta.</span><span class="sxs-lookup"><span data-stu-id="8e330-171">Installing the façade service's certificate into the client's trusted certificate store.</span></span>  
  
     <span data-ttu-id="8e330-172">Poniższy wiersz umożliwia skopiowanie certyfikatu usługi elewacji do magazynu zaufanych osób klienta.</span><span class="sxs-lookup"><span data-stu-id="8e330-172">The following line copies the façade service's certificate into the client trusted people store.</span></span> <span data-ttu-id="8e330-173">Ten krok jest wymagany, ponieważ certyfikaty wygenerowane przez Makecert.exe nie są niejawnie zaufane przez system klienta.</span><span class="sxs-lookup"><span data-stu-id="8e330-173">This step is required because certificates generated by Makecert.exe are not implicitly trusted by the client system.</span></span> <span data-ttu-id="8e330-174">Jeśli masz już certyfikat, który znajduje się w zaufanym certyfikacie głównym klienta — na przykład certyfikat wystawiony przez firmę Microsoft — ten krok zapełniania magazynu certyfikatów klienta z certyfikatem serwera nie jest wymagany.</span><span class="sxs-lookup"><span data-stu-id="8e330-174">If you already have a certificate that is rooted in a client trusted root certificate—for example, a Microsoft-issued certificate—this step of populating the client certificate store with the server certificate is not required.</span></span>  
  
    ```console  
    certmgr.exe -add -r LocalMachine -s My -c -n %SERVER_NAME% -r CurrentUser -s TrustedPeople  
    ```  
  
#### <a name="to-set-up-build-and-run-the-sample"></a><span data-ttu-id="8e330-175">Aby skonfigurować, skompilować i uruchomić przykład</span><span class="sxs-lookup"><span data-stu-id="8e330-175">To set up, build, and run the sample</span></span>  
  
1. <span data-ttu-id="8e330-176">Upewnij się, że została wykonana [Procedura konfiguracji jednorazowej dla przykładów Windows Communication Foundation](one-time-setup-procedure-for-the-wcf-samples.md).</span><span class="sxs-lookup"><span data-stu-id="8e330-176">Ensure that you have performed the [One-Time Setup Procedure for the Windows Communication Foundation Samples](one-time-setup-procedure-for-the-wcf-samples.md).</span></span>  
  
2. <span data-ttu-id="8e330-177">Aby skompilować wersję rozwiązania w języku C# lub Visual Basic .NET, postępuj zgodnie z instrukcjami w temacie [Tworzenie przykładów Windows Communication Foundation](building-the-samples.md).</span><span class="sxs-lookup"><span data-stu-id="8e330-177">To build the C# or Visual Basic .NET edition of the solution, follow the instructions in [Building the Windows Communication Foundation Samples](building-the-samples.md).</span></span>  
  
#### <a name="to-run-the-sample-on-the-same-machine"></a><span data-ttu-id="8e330-178">Aby uruchomić przykład na tym samym komputerze</span><span class="sxs-lookup"><span data-stu-id="8e330-178">To run the sample on the same machine</span></span>  
  
1. <span data-ttu-id="8e330-179">Upewnij się, że ścieżka zawiera folder, w którym znajduje się Makecert.exe.</span><span class="sxs-lookup"><span data-stu-id="8e330-179">Ensure that the path includes the folder where Makecert.exe is located.</span></span>  
  
2. <span data-ttu-id="8e330-180">Uruchom Setup.bat z przykładowego folderu instalacyjnego.</span><span class="sxs-lookup"><span data-stu-id="8e330-180">Run Setup.bat from the sample install folder.</span></span> <span data-ttu-id="8e330-181">Spowoduje to zainstalowanie wszystkich certyfikatów wymaganych do uruchomienia przykładu.</span><span class="sxs-lookup"><span data-stu-id="8e330-181">This installs all the certificates required for running the sample.</span></span>  
  
3. <span data-ttu-id="8e330-182">Uruchom BackendService.exe z katalogu \BackendService\bin w osobnym oknie konsoli</span><span class="sxs-lookup"><span data-stu-id="8e330-182">Launch the BackendService.exe from \BackendService\bin directory in a separate console window</span></span>  
  
4. <span data-ttu-id="8e330-183">Uruchom FacadeService.exe z katalogu \FacadeService\bin w osobnym oknie konsoli</span><span class="sxs-lookup"><span data-stu-id="8e330-183">Launch the FacadeService.exe from \FacadeService\bin directory in a separate console window</span></span>  
  
5. <span data-ttu-id="8e330-184">Uruchom Client.exe z \client\bin.</span><span class="sxs-lookup"><span data-stu-id="8e330-184">Launch Client.exe from \client\bin.</span></span> <span data-ttu-id="8e330-185">Aktywność klienta jest wyświetlana w aplikacji konsoli klienta.</span><span class="sxs-lookup"><span data-stu-id="8e330-185">Client activity is displayed on the client console application.</span></span>  
  
6. <span data-ttu-id="8e330-186">Jeśli klient i usługa nie mogą się komunikować, zobacz Wskazówki dotyczące [rozwiązywania problemów z przykładami programu WCF](/previous-versions/dotnet/netframework-3.5/ms751511(v=vs.90)).</span><span class="sxs-lookup"><span data-stu-id="8e330-186">If the client and service are not able to communicate, see [Troubleshooting Tips for WCF Samples](/previous-versions/dotnet/netframework-3.5/ms751511(v=vs.90)).</span></span>  
  
#### <a name="to-clean-up-after-the-sample"></a><span data-ttu-id="8e330-187">Aby wyczyścić po przykładzie</span><span class="sxs-lookup"><span data-stu-id="8e330-187">To clean up after the sample</span></span>  
  
1. <span data-ttu-id="8e330-188">Uruchom Cleanup.bat w folderze Samples po zakończeniu uruchamiania przykładu.</span><span class="sxs-lookup"><span data-stu-id="8e330-188">Run Cleanup.bat in the samples folder once you have finished running the sample.</span></span>  
  
> [!IMPORTANT]
> <span data-ttu-id="8e330-189">Przykłady mogą być już zainstalowane na komputerze.</span><span class="sxs-lookup"><span data-stu-id="8e330-189">The samples may already be installed on your machine.</span></span> <span data-ttu-id="8e330-190">Przed kontynuowaniem Wyszukaj następujący katalog (domyślny).</span><span class="sxs-lookup"><span data-stu-id="8e330-190">Check for the following (default) directory before continuing.</span></span>  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> <span data-ttu-id="8e330-191">Jeśli ten katalog nie istnieje, przejdź do [przykładów Windows Communication Foundation (WCF) i Windows Workflow Foundation (WF) dla .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) , aby pobrać wszystkie Windows Communication Foundation (WCF) i [!INCLUDE[wf1](../../../../includes/wf1-md.md)] przykłady.</span><span class="sxs-lookup"><span data-stu-id="8e330-191">If this directory does not exist, go to [Windows Communication Foundation (WCF) and Windows Workflow Foundation (WF) Samples for .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) to download all Windows Communication Foundation (WCF) and [!INCLUDE[wf1](../../../../includes/wf1-md.md)] samples.</span></span> <span data-ttu-id="8e330-192">Ten przykład znajduje się w następującym katalogu.</span><span class="sxs-lookup"><span data-stu-id="8e330-192">This sample is located in the following directory.</span></span>  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Scenario\TrustedFacade`
