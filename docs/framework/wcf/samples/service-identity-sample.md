---
title: Tożsamość usług — przykład
ms.date: 03/30/2017
ms.assetid: 79fa8c1c-85bb-4b67-bc67-bfaf721303f8
ms.openlocfilehash: e3365b8e17d847e6e1dc42062dc7fd5c1e4de80d
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/15/2020
ms.locfileid: "90558137"
---
# <a name="service-identity-sample"></a><span data-ttu-id="82bf5-102">Tożsamość usług — przykład</span><span class="sxs-lookup"><span data-stu-id="82bf5-102">Service Identity Sample</span></span>
<span data-ttu-id="82bf5-103">Ta przykładowa tożsamość usługi pokazuje, jak ustawić tożsamość dla usługi.</span><span class="sxs-lookup"><span data-stu-id="82bf5-103">This service identity sample demonstrates how to set the identity for a service.</span></span> <span data-ttu-id="82bf5-104">W czasie projektowania klient może pobrać tożsamość przy użyciu metadanych usługi, a następnie w czasie wykonywania klient może uwierzytelnić tożsamość usługi.</span><span class="sxs-lookup"><span data-stu-id="82bf5-104">At design time, a client can retrieve the identity using the service's metadata and then at runtime the client can authenticate the service's identity.</span></span> <span data-ttu-id="82bf5-105">Pojęcie tożsamości usługi polega na umożliwieniu klientowi uwierzytelnienia usługi przed wywołaniem jakiejkolwiek z jej operacji, co chroni klienta przed nieuwierzytelnionymi wywołaniami.</span><span class="sxs-lookup"><span data-stu-id="82bf5-105">The concept of service identity is to allow a client to authenticate a service before calling any of its operations, thereby protecting the client from unauthenticated calls.</span></span> <span data-ttu-id="82bf5-106">W przypadku bezpiecznego połączenia usługa uwierzytelnia także poświadczenia klienta przed zezwoleniem na dostęp do niego, ale nie jest to fokus tego przykładu.</span><span class="sxs-lookup"><span data-stu-id="82bf5-106">On a secure connection the service also authenticates a client's credentials before allowing it access, but this is not the focus of this sample.</span></span> <span data-ttu-id="82bf5-107">Zapoznaj się z przykładami w [kliencie](client.md) , który pokazuje uwierzytelnianie serwera.</span><span class="sxs-lookup"><span data-stu-id="82bf5-107">See the samples in [Client](client.md) that show server authentication.</span></span>

> [!NOTE]
> <span data-ttu-id="82bf5-108">Procedura instalacji i instrukcje dotyczące kompilacji dla tego przykładu znajdują się na końcu tego tematu.</span><span class="sxs-lookup"><span data-stu-id="82bf5-108">The setup procedure and build instructions for this sample are located at the end of this topic.</span></span>

 <span data-ttu-id="82bf5-109">Ten przykład ilustruje następujące funkcje:</span><span class="sxs-lookup"><span data-stu-id="82bf5-109">This sample illustrates the following features:</span></span>

- <span data-ttu-id="82bf5-110">Jak ustawić różne typy tożsamości w różnych punktach końcowych dla usługi.</span><span class="sxs-lookup"><span data-stu-id="82bf5-110">How to set the different types of identity on different endpoints for a service.</span></span> <span data-ttu-id="82bf5-111">Każdy typ tożsamości ma różne możliwości.</span><span class="sxs-lookup"><span data-stu-id="82bf5-111">Each type of identity has different capabilities.</span></span> <span data-ttu-id="82bf5-112">Typ tożsamości do użycia zależy od typu poświadczeń zabezpieczeń używanych w powiązaniu punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="82bf5-112">The type of identity to use is dependent on the type of security credentials used on the endpoint's binding.</span></span>

- <span data-ttu-id="82bf5-113">Tożsamość można skonfigurować w sposób deklaratywny w konfiguracji lub za pomocą kodu.</span><span class="sxs-lookup"><span data-stu-id="82bf5-113">Identity can either be set declaratively in configuration or imperatively in code.</span></span> <span data-ttu-id="82bf5-114">Zwykle dla klienta i usługi należy użyć konfiguracji, aby ustawić tożsamość.</span><span class="sxs-lookup"><span data-stu-id="82bf5-114">Typically for both the client and the service you should use configuration to set the identity.</span></span>

- <span data-ttu-id="82bf5-115">Jak ustawić niestandardową tożsamość na kliencie.</span><span class="sxs-lookup"><span data-stu-id="82bf5-115">How to set a custom identity on the client.</span></span> <span data-ttu-id="82bf5-116">Niestandardowa tożsamość jest zwykle dostosowywana do istniejącego typu tożsamości, która umożliwia klientowi badanie innych informacji o zadaniu w poświadczeniach usługi w celu podejmowania decyzji dotyczących autoryzacji przed wywołaniem usługi.</span><span class="sxs-lookup"><span data-stu-id="82bf5-116">A custom identity is typically a customization of an existing type of identity that enables the client to examine other claim information provided in the service's credentials to make authorization decisions before calling the service.</span></span>

    > [!NOTE]
    > <span data-ttu-id="82bf5-117">Ten przykład umożliwia sprawdzenie tożsamości określonego certyfikatu o nazwie identity.com i klucza RSA zawartego w tym certyfikacie.</span><span class="sxs-lookup"><span data-stu-id="82bf5-117">This sample checks the identity of a specific certificate called identity.com and the RSA key contained within this certificate.</span></span> <span data-ttu-id="82bf5-118">W przypadku korzystania z certyfikatów i typów tożsamości RSA w konfiguracji na kliencie, prostym sposobem na uzyskanie tych wartości jest sprawdzenie WSDL dla usługi, w której te wartości są serializowane.</span><span class="sxs-lookup"><span data-stu-id="82bf5-118">When using the Certificate and RSA identity types in configuration on the client, an easy way to get these values is to inspect the WSDL for the service where these values are serialized.</span></span>

 <span data-ttu-id="82bf5-119">Poniższy przykładowy kod pokazuje, jak skonfigurować tożsamość punktu końcowego usługi za pomocą serwera nazw domen (DNS) certyfikatu przy użyciu WSHttpBinding.</span><span class="sxs-lookup"><span data-stu-id="82bf5-119">The following sample code shows how to configure the identity of a service endpoint with the Domain Name Server (DNS) of a certificate using a WSHttpBinding.</span></span>

```csharp
//Create a service endpoint and set its identity to the certificate's DNS
WSHttpBinding wsAnonbinding = new WSHttpBinding (SecurityMode.Message);
// Client are Anonymous to the service
wsAnonbinding.Security.Message.ClientCredentialType = MessageCredentialType.None;
WServiceEndpoint ep = serviceHost.AddServiceEndpoint(typeof(ICalculator),wsAnonbinding, String.Empty);
EndpointAddress epa = new EndpointAddress(dnsrelativeAddress,EndpointIdentity.CreateDnsIdentity("identity.com"));
ep.Address = epa;
```

 <span data-ttu-id="82bf5-120">Tożsamość można także określić w konfiguracji w pliku App.config.</span><span class="sxs-lookup"><span data-stu-id="82bf5-120">The identity can also be specified in configuration in the App.config file.</span></span> <span data-ttu-id="82bf5-121">Poniższy przykład pokazuje, jak ustawić tożsamość UPN (główna nazwa użytkownika) dla punktu końcowego usługi.</span><span class="sxs-lookup"><span data-stu-id="82bf5-121">The following example shows how to set the UPN (User Principal Name) identity for a service endpoint.</span></span>

```xml
<endpoint address="upnidentity"
        behaviorConfiguration=""
        binding="wsHttpBinding"
        bindingConfiguration="WSHttpBinding_Windows"
        name="WSHttpBinding_ICalculator_Windows"
        contract="Microsoft.ServiceModel.Samples.ICalculator">
  <!-- Set the UPN identity for this endpoint -->
  <identity>
      <userPrincipalName value="host\myservice.com" />
  </identity >
</endpoint>
```

 <span data-ttu-id="82bf5-122">Tożsamość niestandardową można ustawić na kliencie, pobierając ją z <xref:System.ServiceModel.EndpointIdentity> <xref:System.ServiceModel.Security.IdentityVerifier> klas i.</span><span class="sxs-lookup"><span data-stu-id="82bf5-122">A custom identity can be set on the client by deriving from the <xref:System.ServiceModel.EndpointIdentity> and the <xref:System.ServiceModel.Security.IdentityVerifier> classes.</span></span> <span data-ttu-id="82bf5-123">Koncepcyjnie <xref:System.ServiceModel.Security.IdentityVerifier> Klasa może być traktowana jako odpowiednik klienta `AuthorizationManager` klasy usługi.</span><span class="sxs-lookup"><span data-stu-id="82bf5-123">Conceptually the <xref:System.ServiceModel.Security.IdentityVerifier> class can be considered to be the client equivalent of the service's `AuthorizationManager` class.</span></span> <span data-ttu-id="82bf5-124">Poniższy przykład kodu pokazuje implementację `OrgEndpointIdentity` , która przechowuje nazwę organizacji do dopasowania w nazwie podmiotu certyfikatu serwera.</span><span class="sxs-lookup"><span data-stu-id="82bf5-124">The following code example shows an implementation of `OrgEndpointIdentity`, which stores an organization name to match in the subject name of the server's certificate.</span></span> <span data-ttu-id="82bf5-125">Sprawdzanie autoryzacji nazwy organizacji występuje w `CheckAccess` metodzie `CustomIdentityVerifier` klasy.</span><span class="sxs-lookup"><span data-stu-id="82bf5-125">The authorization check for the organization name occurs in the `CheckAccess` method on the `CustomIdentityVerifier` class.</span></span>

```csharp
// This custom EndpointIdentity stores an organization name
public class OrgEndpointIdentity : EndpointIdentity
{
    private string orgClaim;
    public OrgEndpointIdentity(string orgName)
    {
        orgClaim = orgName;
    }
    public string OrganizationClaim
    {
        get { return orgClaim; }
        set { orgClaim = value; }
    }
}

//This custom IdentityVerifier uses the supplied OrgEndpointIdentity to
//check that X.509 certificate's distinguished name claim contains
//the organization name e.g. the string value "O=Contoso"
class CustomIdentityVerifier : IdentityVerifier
{
    public override bool CheckAccess(EndpointIdentity identity, AuthorizationContext authContext)
    {
        bool returnvalue = false;
        foreach (ClaimSet claimset in authContext.ClaimSets)
        {
            foreach (Claim claim in claimset)
            {
                if (claim.ClaimType == "http://schemas.microsoft.com/ws/2005/05/identity/claims/x500distinguishedname")
                {
                    X500DistinguishedName name = (X500DistinguishedName)claim.Resource;
                    if (name.Name.Contains(((OrgEndpointIdentity)identity).OrganizationClaim))
                    {
                        Console.WriteLine("Claim Type: {0}",claim.ClaimType);
                        Console.WriteLine("Right: {0}", claim.Right);
                        Console.WriteLine("Resource: {0}",claim.Resource);
                        Console.WriteLine();
                        returnvalue = true;
                    }
                }
            }
        }
        return returnvalue;
    }
}
```

 <span data-ttu-id="82bf5-126">Ten przykład używa certyfikatu o nazwie identity.com, który znajduje się w folderze rozwiązania tożsamości specyficznej dla języka.</span><span class="sxs-lookup"><span data-stu-id="82bf5-126">This sample uses a certificate called identity.com which is in the language-specific Identity solution folder.</span></span>

### <a name="to-set-up-build-and-run-the-sample"></a><span data-ttu-id="82bf5-127">Aby skonfigurować, skompilować i uruchomić przykład</span><span class="sxs-lookup"><span data-stu-id="82bf5-127">To set up, build, and run the sample</span></span>

1. <span data-ttu-id="82bf5-128">Upewnij się, że została wykonana [Procedura konfiguracji jednorazowej dla przykładów Windows Communication Foundation](one-time-setup-procedure-for-the-wcf-samples.md).</span><span class="sxs-lookup"><span data-stu-id="82bf5-128">Ensure that you have performed the [One-Time Setup Procedure for the Windows Communication Foundation Samples](one-time-setup-procedure-for-the-wcf-samples.md).</span></span>

2. <span data-ttu-id="82bf5-129">Aby skompilować wersję rozwiązania w języku C# lub Visual Basic .NET, postępuj zgodnie z instrukcjami w temacie [Tworzenie przykładów Windows Communication Foundation](building-the-samples.md).</span><span class="sxs-lookup"><span data-stu-id="82bf5-129">To build the C# or Visual Basic .NET edition of the solution, follow the instructions in [Building the Windows Communication Foundation Samples](building-the-samples.md).</span></span>

3. <span data-ttu-id="82bf5-130">Aby uruchomić przykład w konfiguracji na jednym lub wielu komputerach, postępuj zgodnie z instrukcjami w temacie [Uruchamianie przykładów Windows Communication Foundation](running-the-samples.md).</span><span class="sxs-lookup"><span data-stu-id="82bf5-130">To run the sample in a single- or cross-computer configuration, follow the instructions in [Running the Windows Communication Foundation Samples](running-the-samples.md).</span></span>

### <a name="to-run-the-sample-on-the-same-computer"></a><span data-ttu-id="82bf5-131">Aby uruchomić przykład na tym samym komputerze</span><span class="sxs-lookup"><span data-stu-id="82bf5-131">To run the sample on the same computer</span></span>

1. <span data-ttu-id="82bf5-132">W systemie Windows XP lub Windows Vista Zaimportuj plik certyfikatu Identity. pfx w folderze rozwiązania tożsamości do magazynu certyfikatów LocalMachine/my (Personal) za pomocą narzędzia przystawek programu MMC.</span><span class="sxs-lookup"><span data-stu-id="82bf5-132">On Windows XP or Windows Vista, import the Identity.pfx certificate file in the Identity solution folder into the LocalMachine/My (Personal) certificate store using the MMC snap-in tool.</span></span> <span data-ttu-id="82bf5-133">Ten plik jest chroniony hasłem.</span><span class="sxs-lookup"><span data-stu-id="82bf5-133">This file is password protected.</span></span> <span data-ttu-id="82bf5-134">Podczas importowania zostanie wyświetlony monit o podanie hasła.</span><span class="sxs-lookup"><span data-stu-id="82bf5-134">During the import you are asked for a password.</span></span> <span data-ttu-id="82bf5-135">Wpisz `xyz` w polu hasło.</span><span class="sxs-lookup"><span data-stu-id="82bf5-135">Type `xyz` into the password box.</span></span> <span data-ttu-id="82bf5-136">Aby uzyskać więcej informacji, zobacz temat [How to: View Certificates with MMC przystawka](../feature-details/how-to-view-certificates-with-the-mmc-snap-in.md) .</span><span class="sxs-lookup"><span data-stu-id="82bf5-136">For more information, see the [How to: View Certificates with the MMC Snap-in](../feature-details/how-to-view-certificates-with-the-mmc-snap-in.md) topic.</span></span> <span data-ttu-id="82bf5-137">Po wykonaniu tej czynności Uruchom Setup.bat w wiersz polecenia dla deweloperów dla programu Visual Studio z uprawnieniami administratora, które kopiuje ten certyfikat do magazynu CurrentUser/zaufane osoby do użycia na komputerze klienckim.</span><span class="sxs-lookup"><span data-stu-id="82bf5-137">Once this is done, run Setup.bat in a Developer Command Prompt for Visual Studio with administrator privileges, which copies this certificate to the CurrentUser/Trusted People store for use on the client.</span></span>

2. <span data-ttu-id="82bf5-138">W systemie Windows Server 2003 Uruchom Setup.bat z przykładowego folderu instalacyjnego w wierszu polecenia programu Visual Studio 2012 z uprawnieniami administratora.</span><span class="sxs-lookup"><span data-stu-id="82bf5-138">On Windows Server 2003, run Setup.bat from the sample install folder inside a Visual Studio 2012 command prompt with administrator privileges.</span></span> <span data-ttu-id="82bf5-139">Spowoduje to zainstalowanie wszystkich certyfikatów wymaganych do uruchomienia przykładu.</span><span class="sxs-lookup"><span data-stu-id="82bf5-139">This installs all the certificates required for running the sample.</span></span>

    > [!NOTE]
    > <span data-ttu-id="82bf5-140">Plik wsadowy Setup.bat został zaprojektowany do uruchamiania z wiersza polecenia programu Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="82bf5-140">The Setup.bat batch file is designed to be run from a Visual Studio 2012 Command Prompt.</span></span> <span data-ttu-id="82bf5-141">Zmienna środowiskowa PATH ustawiona w wierszu polecenia programu Visual Studio 2012 wskazuje katalog zawierający pliki wykonywalne wymagane przez skrypt Setup.bat.</span><span class="sxs-lookup"><span data-stu-id="82bf5-141">The PATH environment variable set within the Visual Studio 2012 Command Prompt points to the directory that contains executables required by the Setup.bat script.</span></span> <span data-ttu-id="82bf5-142">Upewnij się, że certyfikaty zostały usunięte, uruchamiając Cleanup.bat po zakończeniu korzystania z przykładu.</span><span class="sxs-lookup"><span data-stu-id="82bf5-142">Ensure that you remove the certificates by running Cleanup.bat when you have finished with the sample.</span></span> <span data-ttu-id="82bf5-143">Inne przykłady zabezpieczeń używają tych samych certyfikatów.</span><span class="sxs-lookup"><span data-stu-id="82bf5-143">Other security samples use the same certificates.</span></span>  
  
3. <span data-ttu-id="82bf5-144">Uruchom Service.exe z katalogu \service\bin.</span><span class="sxs-lookup"><span data-stu-id="82bf5-144">Launch Service.exe from the \service\bin directory.</span></span> <span data-ttu-id="82bf5-145">Upewnij się, że usługa wskazuje, że jest gotowa i wyświetla monit, aby \<Enter> zakończyć działanie usługi.</span><span class="sxs-lookup"><span data-stu-id="82bf5-145">Ensure that the service indicates that it is ready and displays a prompt to Press \<Enter> to terminate the service.</span></span>  
  
4. <span data-ttu-id="82bf5-146">Uruchom Client.exe z katalogu \client\bin lub naciskając klawisz F5 w programie Visual Studio, aby skompilować i uruchomić.</span><span class="sxs-lookup"><span data-stu-id="82bf5-146">Launch Client.exe from \client\bin directory or by pressing F5 in Visual Studio to build and run.</span></span> <span data-ttu-id="82bf5-147">Aktywność klienta jest wyświetlana w aplikacji konsoli klienta.</span><span class="sxs-lookup"><span data-stu-id="82bf5-147">Client activity is displayed on the client console application.</span></span>  
  
5. <span data-ttu-id="82bf5-148">Jeśli klient i usługa nie mogą się komunikować, zobacz Wskazówki dotyczące [rozwiązywania problemów z przykładami programu WCF](/previous-versions/dotnet/netframework-3.5/ms751511(v=vs.90)).</span><span class="sxs-lookup"><span data-stu-id="82bf5-148">If the client and service are not able to communicate, see [Troubleshooting Tips for WCF Samples](/previous-versions/dotnet/netframework-3.5/ms751511(v=vs.90)).</span></span>  
  
### <a name="to-run-the-sample-across-computers"></a><span data-ttu-id="82bf5-149">Aby uruchomić przykład na wielu komputerach</span><span class="sxs-lookup"><span data-stu-id="82bf5-149">To run the sample across computers</span></span>  
  
1. <span data-ttu-id="82bf5-150">Przed utworzeniem części klienta przykładu należy zmienić wartość adresu punktu końcowego usługi w pliku Client.cs w `CallServiceCustomClientIdentity` metodzie.</span><span class="sxs-lookup"><span data-stu-id="82bf5-150">Before building the client part of the sample, be sure to change the value for the service's endpoint address in the Client.cs file in the `CallServiceCustomClientIdentity` method.</span></span> <span data-ttu-id="82bf5-151">Następnie Skompiluj przykład.</span><span class="sxs-lookup"><span data-stu-id="82bf5-151">Then build the sample.</span></span>  
  
2. <span data-ttu-id="82bf5-152">Utwórz katalog na komputerze usługi.</span><span class="sxs-lookup"><span data-stu-id="82bf5-152">Create a directory on the service computer.</span></span>  
  
3. <span data-ttu-id="82bf5-153">Skopiuj pliki programu Service z usługi service\bin do katalogu na komputerze usługi.</span><span class="sxs-lookup"><span data-stu-id="82bf5-153">Copy the service program files from service\bin to the directory on the service computer.</span></span> <span data-ttu-id="82bf5-154">Skopiuj także pliki Setup.bat i Cleanup.bat na komputer usługi.</span><span class="sxs-lookup"><span data-stu-id="82bf5-154">Also copy the Setup.bat and Cleanup.bat files to the service computer.</span></span>  
  
4. <span data-ttu-id="82bf5-155">Utwórz katalog na komputerze klienckim dla plików binarnych klienta.</span><span class="sxs-lookup"><span data-stu-id="82bf5-155">Create a directory on the client computer for the client binaries.</span></span>  
  
5. <span data-ttu-id="82bf5-156">Skopiuj pliki programu klienckiego do katalogu klienta na komputerze klienckim.</span><span class="sxs-lookup"><span data-stu-id="82bf5-156">Copy the client program files to the client directory on the client computer.</span></span> <span data-ttu-id="82bf5-157">Skopiuj także pliki Setup.bat, Cleanup.bat i ImportServiceCert.bat do klienta programu.</span><span class="sxs-lookup"><span data-stu-id="82bf5-157">Also copy the Setup.bat, Cleanup.bat, and ImportServiceCert.bat files to the client.</span></span>  
  
6. <span data-ttu-id="82bf5-158">W usłudze Uruchom polecenie `setup.bat service` w wiersz polecenia dla deweloperów dla programu Visual Studio otwartego z uprawnieniami administratora.</span><span class="sxs-lookup"><span data-stu-id="82bf5-158">On the service, run `setup.bat service` in a Developer Command Prompt for Visual Studio opened with administrator privileges.</span></span> <span data-ttu-id="82bf5-159">Uruchomienie `setup.bat` z `service` argumentem tworzy certyfikat usługi z w pełni kwalifikowaną nazwą domeny komputera i eksportuje certyfikat usługi do pliku o nazwie Service. cer.</span><span class="sxs-lookup"><span data-stu-id="82bf5-159">Running `setup.bat` with the `service` argument creates a service certificate with the fully-qualified domain name of the computer and exports the service certificate to a file named Service.cer.</span></span>  
  
7. <span data-ttu-id="82bf5-160">Skopiuj plik. cer usługi z katalogu usługi do katalogu klienta na komputerze klienckim.</span><span class="sxs-lookup"><span data-stu-id="82bf5-160">Copy the Service.cer file from the service directory to the client directory on the client computer.</span></span>  
  
8. <span data-ttu-id="82bf5-161">W pliku Client.exe.config na komputerze klienckim Zmień wartość adresu punktu końcowego, aby odpowiadała nowemu adresowi usługi.</span><span class="sxs-lookup"><span data-stu-id="82bf5-161">In the Client.exe.config file on the client computer, change the address value of the endpoint to match the new address of your service.</span></span> <span data-ttu-id="82bf5-162">Istnieje wiele wystąpień, które należy zmienić.</span><span class="sxs-lookup"><span data-stu-id="82bf5-162">There are multiple instances that must be changed.</span></span>  
  
9. <span data-ttu-id="82bf5-163">Na kliencie Uruchom ImportServiceCert.bat w wiersz polecenia dla deweloperów dla programu Visual Studio otwartego z uprawnieniami administratora.</span><span class="sxs-lookup"><span data-stu-id="82bf5-163">On the client, run ImportServiceCert.bat in a Developer Command Prompt for Visual Studio opened with administrator privileges.</span></span> <span data-ttu-id="82bf5-164">Spowoduje to zaimportowanie certyfikatu usługi z pliku CER usługi do magazynu CurrentUser-TrustedPeople.</span><span class="sxs-lookup"><span data-stu-id="82bf5-164">This imports the service certificate from the Service.cer file into the CurrentUser - TrustedPeople store.</span></span>  
  
10. <span data-ttu-id="82bf5-165">Na komputerze usługi Uruchom Service.exe z wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="82bf5-165">On the service computer, launch the Service.exe from the command prompt.</span></span>  
  
11. <span data-ttu-id="82bf5-166">Na komputerze klienckim uruchom Client.exe z wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="82bf5-166">On the client computer, launch Client.exe from a command prompt.</span></span> <span data-ttu-id="82bf5-167">Jeśli klient i usługa nie mogą się komunikować, zobacz Wskazówki dotyczące [rozwiązywania problemów z przykładami programu WCF](/previous-versions/dotnet/netframework-3.5/ms751511(v=vs.90)).</span><span class="sxs-lookup"><span data-stu-id="82bf5-167">If the client and service are not able to communicate, see [Troubleshooting Tips for WCF Samples](/previous-versions/dotnet/netframework-3.5/ms751511(v=vs.90)).</span></span>  
  
### <a name="to-clean-up-after-the-sample"></a><span data-ttu-id="82bf5-168">Aby wyczyścić po przykładzie</span><span class="sxs-lookup"><span data-stu-id="82bf5-168">To clean up after the sample</span></span>  
  
- <span data-ttu-id="82bf5-169">Uruchom Cleanup.bat w folderze Samples po zakończeniu uruchamiania przykładu.</span><span class="sxs-lookup"><span data-stu-id="82bf5-169">Run Cleanup.bat in the samples folder once you have finished running the sample.</span></span>  
  
    > [!NOTE]
    > <span data-ttu-id="82bf5-170">Ten skrypt nie powoduje usunięcia certyfikatów usługi na kliencie podczas uruchamiania tego przykładu między komputerami.</span><span class="sxs-lookup"><span data-stu-id="82bf5-170">This script does not remove service certificates on a client when running this sample across computers.</span></span> <span data-ttu-id="82bf5-171">W przypadku uruchamiania przykładów programu Windows Communication Foundation (WCF), które używają certyfikatów między komputerami, należy wyczyścić certyfikaty usługi, które zostały zainstalowane w magazynie CurrentUser-TrustedPeople.</span><span class="sxs-lookup"><span data-stu-id="82bf5-171">If you have run Windows Communication Foundation (WCF) samples that use certificates across computers, be sure to clear the service certificates that have been installed in the CurrentUser - TrustedPeople store.</span></span> <span data-ttu-id="82bf5-172">Aby to zrobić, użyj następującego polecenia: `certmgr -del -r CurrentUser -s TrustedPeople -c -n <Fully Qualified Server Machine Name>` na przykład: `certmgr -del -r CurrentUser -s TrustedPeople -c -n server1.contoso.com` .</span><span class="sxs-lookup"><span data-stu-id="82bf5-172">To do this, use the following command: `certmgr -del -r CurrentUser -s TrustedPeople -c -n <Fully Qualified Server Machine Name>` For example: `certmgr -del -r CurrentUser -s TrustedPeople -c -n server1.contoso.com`.</span></span>
