---
title: Denial of Service (odmowa usługi)
ms.date: 03/30/2017
helpviewer_keywords:
- denial of service [WCF]
ms.assetid: dfb150f3-d598-4697-a5e6-6779e4f9b600
ms.openlocfilehash: 29798a73ec69b7f695068343d9c7b5593eeba4fa
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/15/2020
ms.locfileid: "90557583"
---
# <a name="denial-of-service"></a>Denial of Service (odmowa usługi)
Odmowa usługi występuje, gdy system jest przeciążony w taki sposób, że komunikaty nie mogą być przetwarzane lub są przetwarzane bardzo wolno.  
  
## <a name="excess-memory-consumption"></a>Nadmierne użycie pamięci  
 Podczas odczytywania dokumentu XML o dużej liczbie unikatowych nazw lokalnych, przestrzeni nazw lub prefiksów może wystąpić problem. Jeśli używasz klasy, która pochodzi od <xref:System.Xml.XmlReader> , i wywoływana jest <xref:System.Xml.XmlReader.LocalName%2A> <xref:System.Xml.XmlReader.Prefix%2A> <xref:System.Xml.XmlReader.NamespaceURI%2A> Właściwość lub dla każdego elementu, zwracany ciąg zostanie dodany do <xref:System.Xml.NameTable> . Kolekcja utrzymywana przez <xref:System.Xml.NameTable> nigdy nie zmniejsza rozmiar, tworząc wirtualny "wyciek pamięci" uchwytów ciągów.  
  
 Środki zaradcze obejmują:  
  
- Pochodny od <xref:System.Xml.NameTable> klasy i wymuszanie maksymalnego przydziału rozmiaru. (Nie można zapobiec użyciu <xref:System.Xml.NameTable> lub przełączać, <xref:System.Xml.NameTable> gdy jest on pełny).  
  
- Należy unikać używania powyższych właściwości i zamiast tego używać <xref:System.Xml.XmlReader.MoveToAttribute%2A> metody z <xref:System.Xml.XmlReader.IsStartElement%2A> metodą, jeśli jest to możliwe; metody te nie zwracają ciągów i w ten sposób uniknąć problemu przepełniania <xref:System.Xml.NameTable> kolekcji.  
  
## <a name="malicious-client-sends-excessive-license-requests-to-service"></a>Złośliwy klient wysyła nadmierne żądania licencji do usługi  
 Jeśli złośliwy klient bombards usługę przy użyciu zbyt dużej liczby żądań licencji, może to spowodować, że serwer użyje nadmiernej ilości pamięci.  
  
 Środki zaradcze: Użyj następujących właściwości <xref:System.ServiceModel.Channels.LocalServiceSecuritySettings> klasy:  
  
- <xref:System.ServiceModel.Channels.LocalServiceSecuritySettings.MaxCachedCookies%2A>: określa maksymalną liczbę powiązanych przekroczeń czasu `SecurityContextToken` , po upływie których serwer przeprowadzi pamięć podręczną `SPNego` lub `SSL` negocjacje.  
  
- <xref:System.ServiceModel.Channels.LocalServiceSecuritySettings.IssuedCookieLifetime%2A>: określa okres istnienia `SecurityContextTokens` problemów z serwerem `SPNego` lub `SSL` negocjowania przez serwer. Serwer buforuje `SecurityContextToken` s przez ten okres czasu.  
  
- <xref:System.ServiceModel.Channels.LocalServiceSecuritySettings.MaxPendingSessions%2A>: określa maksymalną liczbę bezpiecznych konwersacji, które są ustanowione na serwerze, ale dla których nie przetworzono komunikatów aplikacji. Ten limit przydziału uniemożliwia klientom ustanawianie bezpiecznych konwersacji w usłudze, co powoduje, że usługa zachowuje stan na klienta, ale nigdy nie korzysta z nich.  
  
- <xref:System.ServiceModel.Channels.LocalServiceSecuritySettings.InactivityTimeout%2A>: określa maksymalny czas, w którym usługa utrzymuje bezpieczną konwersację, bez otrzymywania komunikatu aplikacji z klienta dla konwersacji. Ten limit przydziału uniemożliwia klientom ustanawianie bezpiecznych konwersacji w usłudze, co powoduje, że usługa zachowuje stan na klienta, ale nigdy nie korzysta z nich.  
  
## <a name="wsdualhttpbinding-or-dual-custom-bindings-require-client-authentication"></a>WSDualHttpBinding lub podwójne powiązania niestandardowe wymagają uwierzytelniania klienta  
 Domyślnie <xref:System.ServiceModel.WSDualHttpBinding> Funkcja ma włączone zabezpieczenia. Jeśli jednak uwierzytelnianie klienta zostanie wyłączone przez ustawienie <xref:System.ServiceModel.MessageSecurityOverHttp.ClientCredentialType%2A> właściwości na <xref:System.ServiceModel.MessageCredentialType.None> , złośliwy użytkownik może spowodować atak typu "odmowa usługi" w trzeciej usłudze. Może to być spowodowane tym, że złośliwy klient może skierować usługę do wysłania strumienia komunikatów do trzeciej usługi.  
  
 Aby rozwiązać ten problem, nie ustawiaj właściwości na `None` . Należy również pamiętać o tej możliwości podczas tworzenia niestandardowego powiązania, które ma podwójny wzorzec wiadomości.  
  
## <a name="auditing-event-log-can-be-filled"></a>Dziennik zdarzeń inspekcji może być wypełniony  
 Jeśli złośliwy użytkownik rozumie, że inspekcja jest włączona, osoba atakująca może wysłać nieprawidłowe komunikaty, które powodują zapisanie wpisów inspekcji. Jeśli dziennik inspekcji zostanie wypełniony w ten sposób, system inspekcji zakończy się niepowodzeniem.  
  
 Aby rozwiązać ten problem, ustaw <xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior.SuppressAuditFailure%2A> Właściwość na `true` i użyj właściwości Podgląd zdarzeń, aby kontrolować zachowanie inspekcji. Aby uzyskać więcej informacji na temat używania Podgląd zdarzeń do wyświetlania dzienników zdarzeń i zarządzania nimi, zobacz [Podgląd zdarzeń](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc766042(v=ws.11)). Aby uzyskać więcej informacji, zobacz [Inspekcja](auditing-security-events.md).  
  
## <a name="invalid-implementations-of-iauthorizationpolicy-can-cause-service-to-become-unresponsive"></a>Nieprawidłowe implementacje interfejsu IAuthorizationPolicy mogą spowodować, że usługa przestanie odpowiadać  
 Wywołanie <xref:System.IdentityModel.Policy.IAuthorizationPolicy.Evaluate%2A> metody w wadliwej implementacji <xref:System.IdentityModel.Policy.IAuthorizationPolicy> interfejsu może spowodować, że usługa przestanie odpowiadać.  
  
 Środki zaradcze: Używaj tylko zaufanego kodu. Oznacza to, że należy używać tylko kodu, który został zapisany i przetestowany lub który pochodzi od zaufanego dostawcy. Nie Zezwalaj na Podłączanie niezaufanych rozszerzeń <xref:System.IdentityModel.Policy.IAuthorizationPolicy> do kodu bez uwzględniania ich. Dotyczy to wszystkich rozszerzeń używanych w implementacji usługi. W programie WCF nie są wprowadzane żadne różnice między kodem aplikacji a kodem obcym, który jest podłączony przy użyciu punktów rozszerzalności.  
  
## <a name="kerberos-maximum-token-size-may-need-resizing"></a>Maksymalny rozmiar tokenu protokołu Kerberos może wymagać zmiany rozmiaru  
 Jeśli klient należy do dużej liczby grup (około 900, chociaż rzeczywista liczba różni się w zależności od grup), problem może wystąpić, gdy blok nagłówka komunikatu przekracza 64 kilobajty. W takim przypadku można zwiększyć maksymalny rozmiar tokenu Kerberos. Może być również konieczne zwiększenie maksymalnego rozmiaru komunikatów WCF w celu uwzględnienia większego tokenu Kerberos.  
  
## <a name="autoenrollment-results-in-multiple-certificates-with-same-subject-name-for-machine"></a>Autorejestrowanie powoduje, że wiele certyfikatów ma tę samą nazwę podmiotu dla komputera  
 Funkcja *autorejestrowania* jest funkcją systemu Windows Server 2003, aby automatycznie rejestrować użytkowników i komputery dla certyfikatów. Gdy komputer znajduje się w domenie z włączoną funkcją, certyfikat X. 509 z zamierzonym celem uwierzytelniania klienta zostanie automatycznie utworzony i wstawiony do magazynu certyfikatów osobistych komputera lokalnego za każdym razem, gdy nowa maszyna jest przyłączona do sieci. Jednak funkcja autorejestrowania używa tej samej nazwy podmiotu dla wszystkich certyfikatów tworzonych w pamięci podręcznej.  
  
 Ma to wpływ na to, że usługi WCF mogą nie być otwierane w domenach z autorejestrowaniem. Dzieje się tak dlatego, że domyślne kryteria wyszukiwania poświadczeń X. 509 usługi mogą być niejednoznaczne, ponieważ istnieje wiele certyfikatów z w pełni kwalifikowaną nazwą systemu nazw domen (DNS) na komputerze. Jeden certyfikat pochodzi z autorejestrowania; drugi może być certyfikatem wystawionym przez siebie.  
  
 Aby rozwiązać ten problem, należy odwołać się do dokładnego certyfikatu do użycia przy użyciu dokładniejszego kryterium wyszukiwania w [\<serviceCredentials>](../../configure-apps/file-schema/wcf/servicecredentials.md) . Na przykład użyj <xref:System.Security.Cryptography.X509Certificates.X509FindType.FindByThumbprint> opcji i Określ certyfikat przy użyciu unikatowego odcisku palca (hash).  
  
 Aby uzyskać więcej informacji na temat funkcji autorejestrowania, zobacz [autorejestrowanie certyfikatów w systemie Windows Server 2003](/previous-versions/windows/it-pro/windows-server-2003/cc778954(v=ws.10)).  
  
## <a name="last-of-multiple-alternative-subject-names-used-for-authorization"></a>Ostatnia z wielu alternatywnych nazw podmiotów używanych do autoryzacji  
 W rzadkich przypadkach, gdy certyfikat X. 509 zawiera wiele alternatywnych nazw podmiotu i Użytkownik autoryzuje przy użyciu alternatywnej nazwy podmiotu, autoryzacja może zakończyć się niepowodzeniem.  
  
## <a name="protect-configuration-files-with-acls"></a>Ochrona plików konfiguracji przy użyciu list ACL  
 Można określić wymagane i opcjonalne oświadczenia w kodzie i plikach konfiguracji dla tokenów wystawionych przez CardSpace. Powoduje to odpowiednie elementy `RequestSecurityToken` , które są emitowane w komunikatach wysyłanych do usługi tokenu zabezpieczającego. Osoba atakująca może zmodyfikować kod lub konfigurację w celu usunięcia wymaganych lub opcjonalnych oświadczeń, co może spowodować, że usługa tokenu zabezpieczającego wystawia token, który nie zezwala na dostęp do usługi docelowej.  
  
 Aby wyeliminować problem: Wymagaj dostępu do komputera w celu zmodyfikowania pliku konfiguracji. Użyj list kontroli dostępu do plików (ACL) do zabezpieczania plików konfiguracji. Program WCF wymaga, aby kod znajdował się w katalogu aplikacji lub w globalnej pamięci podręcznej zestawów, zanim zezwoli na załadowanie tego kodu z konfiguracji. Użyj list ACL katalogów do zabezpieczania katalogów.  
  
## <a name="maximum-number-of-secure-sessions-for-a-service-is-reached"></a>Osiągnięto maksymalną liczbę zabezpieczonych sesji dla usługi  
 W przypadku pomyślnego uwierzytelnienia klienta przez usługę i ustanowienia bezpiecznej sesji z usługą Usługa śledzi sesję do momentu jej anulowania przez klienta lub wygaśnięcia sesji. Każdy ustanowiony licznik sesji odnoszący się do limitu maksymalnej liczby aktywnych sesji jednoczesnych z usługą. Po osiągnięciu tego limitu klienci próbujący utworzyć nową sesję z tą usługą są odrzucani do momentu wygaśnięcia co najmniej jednej aktywnej sesji lub anulowania jej przez klienta. Klient może mieć wiele sesji z usługą, a każda z nich jest liczona do limitu.  
  
> [!NOTE]
> W przypadku korzystania z sesji stanowych poprzedni akapit nie ma zastosowania. Aby uzyskać więcej informacji na temat sesji stanowych, zobacz [jak: Tworzenie tokenu kontekstu zabezpieczeń dla bezpiecznej sesji](how-to-create-a-security-context-token-for-a-secure-session.md).  
  
 Aby rozwiązać ten problem, należy ustawić limit maksymalnej liczby aktywnych sesji i maksymalny okres istnienia sesji przez ustawienie <xref:System.ServiceModel.Channels.SecurityBindingElement> właściwości <xref:System.ServiceModel.Channels.SecurityBindingElement> klasy.  
  
## <a name="see-also"></a>Zobacz także

- [Zagadnienia dotyczące zabezpieczeń](security-considerations-in-wcf.md)
- [Information Disclosure (ujawnienie informacji)](information-disclosure.md)
- [Elevation of Privilege (podniesienie uprawnień)](elevation-of-privilege.md)
- [Denial of Service (odmowa usługi)](denial-of-service.md)
- [Ataki oparte na metodzie powtórzeń](replay-attacks.md)
- [Tampering (manipulowanie)](tampering.md)
- [Nieobsługiwane scenariusze](unsupported-scenarios.md)
