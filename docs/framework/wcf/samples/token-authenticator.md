---
title: Wystawca uwierzytelnienia tokenów
ms.date: 03/30/2017
ms.assetid: 84382f2c-f6b1-4c32-82fa-aebc8f6064db
ms.openlocfilehash: a493ea48d9d339c0bc1a4b191b084374ad5f2dc4
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/15/2020
ms.locfileid: "90548595"
---
# <a name="token-authenticator"></a>Wystawca uwierzytelnienia tokenów
Ten przykład pokazuje, jak zaimplementować niestandardowy wystawca uwierzytelnienia tokenów. Wystawca uwierzytelnienia w programie Windows Communication Foundation (WCF) służy do sprawdzania poprawności tokenu użytego w komunikacie, weryfikowania, czy jest on spójny, i uwierzytelniania tożsamości skojarzonej z tokenem.

 Niestandardowe wystawcy tokenów są przydatne w różnych przypadkach, takich jak:

- Jeśli chcesz zastąpić domyślny mechanizm uwierzytelniania skojarzony z tokenem.

- Podczas kompilowania niestandardowego tokenu.

 W tym przykładzie przedstawiono następujące elementy:

- Jak klient może uwierzytelniać za pomocą pary username/Password.

- Jak serwer może sprawdzać poprawność poświadczeń klienta przy użyciu niestandardowego wystawcy uwierzytelnienia tokenu.

- Sposób powiązania kodu usługi WCF z niestandardowym wystawcą uwierzytelnienia.

- Jak można uwierzytelniać serwer przy użyciu certyfikatu X. 509 serwera.

 Ten przykład pokazuje również, jak tożsamość wywołującego jest dostępna z programu WCF po procesie uwierzytelniania tokenu niestandardowego.

 Usługa udostępnia jeden punkt końcowy do komunikacji z usługą, zdefiniowany przy użyciu pliku konfiguracji App.config. Punkt końcowy składa się z adresu, powiązania i kontraktu. Powiązanie jest skonfigurowane ze standardem `wsHttpBinding` , z trybem zabezpieczeń ustawionym na komunikat — domyślny tryb `wsHttpBinding` . Ten przykład ustawia standard `wsHttpBinding` do korzystania z uwierzytelniania nazwy użytkownika klienta. Usługa konfiguruje również certyfikat usługi przy użyciu `serviceCredentials` zachowania. `securityCredentials`Zachowanie pozwala określić certyfikat usługi. Certyfikat usługi jest używany przez klienta do uwierzytelniania usługi i zapewniania ochrony komunikatów. Następująca konfiguracja odwołuje się do certyfikatu localhost zainstalowanego podczas konfiguracji przykładowej zgodnie z opisem w poniższych instrukcjach dotyczących instalacji.

```xml
<system.serviceModel>
    <services>
      <service
          name="Microsoft.ServiceModel.Samples.CalculatorService"
          behaviorConfiguration="CalculatorServiceBehavior">
        <host>
          <baseAddresses>
            <!-- configure base address provided by host -->
            <add baseAddress ="http://localhost:8000/servicemodelsamples/service" />
          </baseAddresses>
        </host>
        <!-- use base address provided by host -->
        <endpoint address=""
                  binding="wsHttpBinding"
                  bindingConfiguration="Binding1"
                  contract="Microsoft.ServiceModel.Samples.ICalculator" />
      </service>
    </services>

    <bindings>
      <wsHttpBinding>
        <binding name="Binding1">
          <security mode="Message">
            <message clientCredentialType="UserName" />
          </security>
        </binding>
      </wsHttpBinding>
    </bindings>

    <behaviors>
      <serviceBehaviors>
        <behavior name="CalculatorServiceBehavior">
          <serviceDebug includeExceptionDetailInFaults="False" />
          <!--
          The serviceCredentials behavior allows one to define a service certificate.
          A service certificate is used by a client to authenticate the service and provide message protection.
          This configuration references the "localhost" certificate installed during the setup instructions.
....        -->
          <serviceCredentials>
            <serviceCertificate findValue="localhost" storeLocation="LocalMachine" storeName="My" x509FindType="FindBySubjectName" />
          </serviceCredentials>
        </behavior>
      </serviceBehaviors>
    </behaviors>

  </system.serviceModel>
```

 Konfiguracja punktu końcowego klienta składa się z nazwy konfiguracji, adresu bezwzględnego dla punktu końcowego usługi, powiązania i kontraktu. Powiązanie klienta jest skonfigurowane z odpowiednimi `Mode` i `clientCredentialType` .

```xml
<system.serviceModel>
    <client>
      <endpoint name=""
                address="http://localhost:8000/servicemodelsamples/service"
                binding="wsHttpBinding"
                bindingConfiguration="Binding1"
                contract="Microsoft.ServiceModel.Samples.ICalculator">
      </endpoint>
    </client>

    <bindings>
      <wsHttpBinding>
        <binding name="Binding1">
          <security mode="Message">
            <message clientCredentialType="UserName" />
          </security>
        </binding>
      </wsHttpBinding>
    </bindings>
  </system.serviceModel>
```

 Implementacja klienta ustawia nazwę użytkownika i hasło, które mają być używane.

```csharp
static void Main()
{
     ...
     client.ClientCredentials.UserNamePassword.UserName = username;
     client.ClientCredentials.UserNamePassword.Password = password;
     ...
}
```

## <a name="custom-token-authenticator"></a>Niestandardowe wystawcy uwierzytelniania tokenów
 Aby utworzyć niestandardowy wystawca uwierzytelnienia tokenów, wykonaj następujące kroki:

1. Napisz niestandardowy wystawca uwierzytelnienia.

     Przykład implementuje niestandardowy wystawca uwierzytelnienia tokenów, który sprawdza, czy nazwa użytkownika ma prawidłowy format wiadomości e-mail. Dziedziczy <xref:System.IdentityModel.Selectors.UserNameSecurityTokenAuthenticator> . Najważniejszym sposobem w tej klasie jest <xref:System.IdentityModel.Selectors.UserNameSecurityTokenAuthenticator.ValidateUserNamePasswordCore%28System.String%2CSystem.String%29> . W tej metodzie wystawca uwierzytelnienia weryfikuje format nazwy użytkownika, a także że nazwa hosta nie pochodzi z nieautoryzowanej domeny. W przypadku spełnienia obu warunków funkcja zwraca kolekcję wystąpień tylko do odczytu, <xref:System.IdentityModel.Policy.IAuthorizationPolicy> która jest używana do dostarczania oświadczeń, które reprezentują informacje przechowywane wewnątrz tokenu username.

    ```csharp
    protected override ReadOnlyCollection<IAuthorizationPolicy> ValidateUserNamePasswordCore(string userName, string password)
    {
        if (!ValidateUserNameFormat(userName))
            throw new SecurityTokenValidationException("Incorrect UserName format");

        ClaimSet claimSet = new DefaultClaimSet(ClaimSet.System, new Claim(ClaimTypes.Name, userName, Rights.PossessProperty));
        List<IIdentity> identities = new List<IIdentity>(1);
        identities.Add(new GenericIdentity(userName));
        List<IAuthorizationPolicy> policies = new List<IAuthorizationPolicy>(1);
        policies.Add(new UnconditionalPolicy(ClaimSet.System, claimSet, DateTime.MaxValue.ToUniversalTime(), identities));
        return policies.AsReadOnly();
    }
    ```

2. Podaj zasady autoryzacji, które są zwracane przez niestandardowy wystawca uwierzytelnienia.

     Ten przykład zawiera własną implementację o <xref:System.IdentityModel.Policy.IAuthorizationPolicy> nazwie `UnconditionalPolicy` , która zwraca zestaw oświadczeń i tożsamości, które zostały do niego przesłane w konstruktorze.

    ```csharp
    class UnconditionalPolicy : IAuthorizationPolicy
    {
        String id = Guid.NewGuid().ToString();
        ClaimSet issuer;
        ClaimSet issuance;
        DateTime expirationTime;
        IList<IIdentity> identities;

        public UnconditionalPolicy(ClaimSet issuer, ClaimSet issuance, DateTime expirationTime, IList<IIdentity> identities)
        {
            if (issuer == null)
                throw new ArgumentNullException("issuer");
            if (issuance == null)
                throw new ArgumentNullException("issuance");

            this.issuer = issuer;
            this.issuance = issuance;
            this.identities = identities;
            this.expirationTime = expirationTime;
        }

        public string Id
        {
            get { return this.id; }
        }

        public ClaimSet Issuer
        {
            get { return this.issuer; }
        }

        public DateTime ExpirationTime
        {
            get { return this.expirationTime; }
        }

        public bool Evaluate(EvaluationContext evaluationContext, ref object state)
        {
            evaluationContext.AddToTarget(this, this.issuance);

            if (this.identities != null)
            {
                object value;
                IList<IIdentity> contextIdentities;
                if (!evaluationContext.Properties.TryGetValue("Identities", out value))
                {
                    contextIdentities = new List<IIdentity>(this.identities.Count);
                    evaluationContext.Properties.Add("Identities", contextIdentities);
                }
                else
                {
                    contextIdentities = value as IList<IIdentity>;
                }
                foreach (IIdentity identity in this.identities)
                {
                    contextIdentities.Add(identity);
                }
            }

            evaluationContext.RecordExpirationTime(this.expirationTime);
            return true;
        }
    }
    ```

3. Napisz niestandardowego menedżera tokenów zabezpieczających.

     Służy <xref:System.IdentityModel.Selectors.SecurityTokenManager> do tworzenia <xref:System.IdentityModel.Selectors.SecurityTokenAuthenticator> dla określonych <xref:System.IdentityModel.Selectors.SecurityTokenRequirement> obiektów, które są do niego przenoszone w `CreateSecurityTokenAuthenticator` metodzie. Menedżer tokenów zabezpieczających jest również używany do tworzenia dostawców tokenów i serializatorów tokenów, ale nie są one objęte tym przykładem. W tym przykładzie niestandardowy Menedżer tokenów zabezpieczających dziedziczy z <xref:System.ServiceModel.Security.ServiceCredentialsSecurityTokenManager> klasy i przesłania `CreateSecurityTokenAuthenticator` metodę w celu zwrócenia niestandardowej wystawcy tokenów username, gdy spełnione wymagania dotyczące tokenu wskazują, że żądanie uwierzytelnienia nazwy użytkownika jest wymagane.

    ```csharp
    public class MySecurityTokenManager : ServiceCredentialsSecurityTokenManager
    {
        MyUserNameCredential myUserNameCredential;

        public MySecurityTokenManager(MyUserNameCredential myUserNameCredential)
            : base(myUserNameCredential)
        {
            this.myUserNameCredential = myUserNameCredential;
        }

        public override SecurityTokenAuthenticator CreateSecurityTokenAuthenticator(SecurityTokenRequirement tokenRequirement, out SecurityTokenResolver outOfBandTokenResolver)
        {
            if (tokenRequirement.TokenType ==  SecurityTokenTypes.UserName)
            {
                outOfBandTokenResolver = null;
                return new MyTokenAuthenticator();
            }
            else
            {
                return base.CreateSecurityTokenAuthenticator(tokenRequirement, out outOfBandTokenResolver);
            }
        }
    }
    ```

4. Napisz niestandardowe poświadczenie usługi.

     Klasa poświadczeń usługi służy do reprezentowania poświadczeń skonfigurowanych dla usługi i tworzy Menedżera tokenów zabezpieczających, który jest używany do uzyskiwania wystawców tokenów, dostawców tokenów i serializatorów tokenów.

    ```csharp
    public class MyUserNameCredential : ServiceCredentials
    {

        public MyUserNameCredential()
            : base()
        {
        }

        protected override ServiceCredentials CloneCore()
        {
            return new MyUserNameCredential();
        }

        public override SecurityTokenManager CreateSecurityTokenManager()
        {
            return new MySecurityTokenManager(this);
        }

    }
    ```

5. Skonfiguruj usługę tak, aby korzystała z poświadczeń usługi niestandardowej.

     Aby usługa mogła korzystać z poświadczeń usługi niestandardowej, należy usunąć domyślną klasę poświadczeń usługi po przechwyceniu certyfikatu usługi, który jest już wstępnie skonfigurowany w domyślnym poświadczenie usługi, i skonfigurować nowe wystąpienie poświadczeń usługi do korzystania ze wstępnie skonfigurowanych certyfikatów usługi i dodać nowe wystąpienie poświadczeń usługi do zachowań usługi.

    ```csharp
    ServiceCredentials sc = serviceHost.Credentials;
    X509Certificate2 cert = sc.ServiceCertificate.Certificate;
    MyUserNameCredential serviceCredential = new MyUserNameCredential();
    serviceCredential.ServiceCertificate.Certificate = cert;
    serviceHost.Description.Behaviors.Remove((typeof(ServiceCredentials)));
    serviceHost.Description.Behaviors.Add(serviceCredential);
    ```

 Aby wyświetlić informacje o wywołującym, można użyć, <xref:System.ServiceModel.ServiceSecurityContext.PrimaryIdentity%2A> jak pokazano w poniższym kodzie. <xref:System.ServiceModel.ServiceSecurityContext.Current%2A>Zawiera informacje o oświadczeniach dotyczących bieżącego obiektu wywołującego.

```csharp
static void DisplayIdentityInformation()
{
    Console.WriteLine("\t\tSecurity context identity  :  {0}",
            ServiceSecurityContext.Current.PrimaryIdentity.Name);
     return;
}
```

 Po uruchomieniu przykładu żądania operacji i odpowiedzi są wyświetlane w oknie konsoli klienta. Naciśnij klawisz ENTER w oknie klienta, aby zamknąć klienta programu.

## <a name="setup-batch-file"></a>Plik wsadowy konfiguracji
 Plik wsadowy Setup.bat dołączony do tego przykładu umożliwia skonfigurowanie serwera z odpowiednimi certyfikatami w celu uruchomienia aplikacji samohostowanej wymagającej zabezpieczeń opartych na certyfikatach serwera. Ten plik wsadowy należy zmodyfikować, aby mógł działać na różnych komputerach lub działać w nieobsługiwanym przypadku.

 Poniżej przedstawiono krótkie omówienie różnych sekcji plików wsadowych, dzięki czemu można je zmodyfikować do uruchamiania w odpowiedniej konfiguracji.

- Tworzenie certyfikatu serwera.

     Poniższe wiersze z pliku wsadowego Setup.bat utworzyć certyfikat serwera do użycia. `%SERVER_NAME%`Zmienna określa nazwę serwera. Zmień tę zmienną, aby określić własną nazwę serwera. Wartość domyślna w tym pliku wsadowym to localhost.

    ```console
    echo ************
    echo Server cert setup starting
    echo %SERVER_NAME%
    echo ************
    echo making server cert
    echo ************
    makecert.exe -sr LocalMachine -ss MY -a sha1 -n CN=%SERVER_NAME% -sky exchange -pe
    ```

- Instalowanie certyfikatu serwera w magazynie zaufanych certyfikatów klienta.

     Poniższe wiersze w pliku wsadowym Setup.bat kopiują certyfikat serwera do magazynu zaufanych osób klienta. Ten krok jest wymagany, ponieważ certyfikaty wygenerowane przez Makecert.exe nie są niejawnie zaufane przez system klienta. Jeśli masz już certyfikat, który znajduje się w zaufanym certyfikacie głównym klienta — na przykład certyfikat wystawiony przez firmę Microsoft — ten krok zapełniania magazynu certyfikatów klienta z certyfikatem serwera nie jest wymagany.

    ```console
    certmgr.exe -add -r LocalMachine -s My -c -n %SERVER_NAME% -r CurrentUser -s TrustedPeople
    ```

    > [!NOTE]
    > Plik wsadowy instalacji został zaprojektowany tak, aby można go było uruchomić z poziomu wiersza polecenia Windows SDK. Wymaga, aby zmienna środowiskowa MSSDK wskazywała katalog, w którym zainstalowano zestaw SDK. Ta zmienna środowiskowa jest ustawiana automatycznie w wierszu polecenia Windows SDK.

#### <a name="to-set-up-and-build-the-sample"></a>Aby skonfigurować i skompilować przykład

1. Upewnij się, że została wykonana [Procedura konfiguracji jednorazowej dla przykładów Windows Communication Foundation](one-time-setup-procedure-for-the-wcf-samples.md).

2. Aby skompilować rozwiązanie, postępuj zgodnie z instrukcjami w temacie [Tworzenie przykładów Windows Communication Foundation](building-the-samples.md).

#### <a name="to-run-the-sample-on-the-same-computer"></a>Aby uruchomić przykład na tym samym komputerze

1. Uruchom Setup.bat z przykładowego folderu instalacyjnego w wierszu polecenia programu Visual Studio 2012 otwartym z uprawnieniami administratora. Spowoduje to zainstalowanie wszystkich certyfikatów wymaganych do uruchomienia przykładu.

    > [!NOTE]
    > Plik wsadowy Setup.bat został zaprojektowany do uruchamiania z wiersza polecenia programu Visual Studio 2012. Zmienna środowiskowa PATH ustawiona w wierszu polecenia programu Visual Studio 2012 wskazuje katalog zawierający pliki wykonywalne wymagane przez skrypt Setup.bat.  
  
2. Uruchom service.exe z service\bin.  
  
3. Uruchom client.exe z \client\bin. Aktywność klienta jest wyświetlana w aplikacji konsoli klienta.  
  
4. Jeśli klient i usługa nie mogą się komunikować, zobacz Wskazówki dotyczące [rozwiązywania problemów z przykładami programu WCF](/previous-versions/dotnet/netframework-3.5/ms751511(v=vs.90)).  
  
#### <a name="to-run-the-sample-across-computers"></a>Aby uruchomić przykład na wielu komputerach  
  
1. Utwórz katalog na komputerze usługi dla plików binarnych usługi.  
  
2. Skopiuj pliki programu Service Files do katalogu usługi na komputerze usługi. Skopiuj także pliki Setup.bat i Cleanup.bat na komputer usługi.  
  
3. Musisz mieć certyfikat serwera z nazwą podmiotu zawierającą w pełni kwalifikowaną nazwę domeny komputera. Plik App.config usługi musi zostać zaktualizowany w celu odzwierciedlenia tej nowej nazwy certyfikatu. Można go utworzyć przy użyciu Setup.bat, jeśli ustawisz `%SERVER_NAME%` zmienną na w pełni kwalifikowaną nazwę hosta komputera, na którym zostanie uruchomiona usługa. Należy pamiętać, że plik setup.bat musi być uruchamiany z wiersz polecenia dla deweloperów dla programu Visual Studio otwartego z uprawnieniami administratora.  
  
4. Skopiuj certyfikat serwera do magazynu CurrentUser-TrustedPeople klienta. Nie trzeba tego robić, chyba że certyfikat serwera zostanie wystawiony przez zaufanego wystawcy klienta.  
  
5. W pliku App.config na komputerze usługi Zmień wartość adresu podstawowego, aby określić w pełni kwalifikowaną nazwę komputera zamiast hosta lokalnego.  
  
6. Na komputerze usługi Uruchom service.exe z wiersza polecenia.  
  
7. Skopiuj pliki programu klienckiego z folderu \client\bin\, w obszarze folder specyficzny dla języka, do komputera klienckiego.  
  
8. W pliku Client.exe.config na komputerze klienckim Zmień wartość adresu punktu końcowego, aby odpowiadała nowemu adresowi usługi.  
  
9. Na komputerze klienckim uruchom Client.exe z wiersza polecenia.  
  
10. Jeśli klient i usługa nie mogą się komunikować, zobacz Wskazówki dotyczące [rozwiązywania problemów z przykładami programu WCF](/previous-versions/dotnet/netframework-3.5/ms751511(v=vs.90)).  
  
#### <a name="to-clean-up-after-the-sample"></a>Aby wyczyścić po przykładzie  
  
1. Uruchom Cleanup.bat w folderze Samples po zakończeniu uruchamiania przykładu.
