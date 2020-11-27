---
title: Ochrona komunikatów za pomocą zabezpieczeń transportu
ms.date: 03/30/2017
ms.assetid: 9029771a-097e-448a-a13a-55d2878330b8
ms.openlocfilehash: b3931d594b585a176be7a9a2e2779df5d844c56b
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96288605"
---
# <a name="securing-messages-using-transport-security"></a>Ochrona komunikatów za pomocą zabezpieczeń transportu

W tej sekcji omówiono zabezpieczenia transportu usługi kolejkowania komunikatów (MSMQ), których można użyć do zabezpieczenia komunikatów wysyłanych do kolejki.  
  
> [!NOTE]
> Przed przeczytaniem z tego tematu zaleca się zapoznanie się z [pojęciami dotyczącymi zabezpieczeń](security-concepts.md).  
  
 Poniższa ilustracja przedstawia model koncepcyjny komunikacji kolejkowanej przy użyciu Windows Communication Foundation (WCF). Ta ilustracja i terminologia są używane w celu wyjaśnienia pojęć związanych z zabezpieczeniami transportu.  
  
 ![Diagram aplikacji znajdujących się w kolejce](media/distributed-queue-figure.jpg "Rozproszona-Queueed-Figure")  
  
 W przypadku wysyłania komunikatów umieszczonych w kolejce przy użyciu programu WCF z usługą <xref:System.ServiceModel.NetMsmqBinding> komunikat WCF jest dołączany jako treść komunikatu usługi MSMQ. Zabezpieczenia transportu zabezpieczają cały komunikat MSMQ (nagłówki lub właściwości wiadomości MSMQ oraz treść wiadomości). Ponieważ jest to treść komunikatu MSMQ, przy użyciu zabezpieczenia transportu jest również zabezpieczony komunikatem WCF.  
  
 Kluczową koncepcją pod względem zabezpieczeń transportu jest to, że klient musi spełnić wymagania dotyczące zabezpieczeń, aby uzyskać komunikat do kolejki docelowej. Jest to w przeciwieństwie do zabezpieczeń komunikatów, w przypadku których komunikat jest zabezpieczony dla aplikacji, która otrzymuje komunikat.  
  
 Zabezpieczenia transportu wykorzystujące <xref:System.ServiceModel.NetMsmqBinding> i <xref:System.ServiceModel.MsmqIntegration.MsmqIntegrationBinding> wpływające na sposób zabezpieczania komunikatów usługi MSMQ między kolejką transmisji i kolejką docelową, w której są zabezpieczone:  
  
- Podpisywanie komunikatu w celu upewnienia się, że nie jest on naruszony.  
  
- Szyfrowanie wiadomości w celu upewnienia się, że nie jest ona widoczna ani naruszona. Jest to zalecane, ale opcjonalne.  
  
- Docelowy Menedżer kolejki, który identyfikuje nadawcę wiadomości dla odrzucania.  
  
 W przypadku usługi MSMQ niezależnie od uwierzytelniania kolejka docelowa ma listę kontroli dostępu (ACL), aby sprawdzić, czy klient ma uprawnienia do wysyłania wiadomości do kolejki docelowej. Aplikacja odbierająca jest również sprawdzana pod kątem uprawnień do odbierania wiadomości z kolejki docelowej.  
  
## <a name="wcf-msmq-transport-security-properties"></a>Właściwości zabezpieczeń transportu MSMQ usługi WCF  

 Usługa MSMQ używa zabezpieczeń systemu Windows do uwierzytelniania. Używa identyfikatora zabezpieczeń systemu Windows (SID) do identyfikowania klienta i używa usługi katalogowej Active Directory jako urzędu certyfikacji podczas uwierzytelniania klienta. Wymaga to zainstalowania usługi MSMQ z integracją Active Directory. Ponieważ identyfikator SID domeny systemu Windows jest używany do identyfikowania klienta, ta opcja zabezpieczeń ma znaczenie tylko wtedy, gdy zarówno klient, jak i usługa są częścią tej samej domeny systemu Windows.  
  
 Usługa MSMQ zapewnia również możliwość dołączenia certyfikatu do wiadomości, która nie jest zarejestrowana w Active Directory. W takim przypadku gwarantuje to, że wiadomość została podpisana przy użyciu dołączonego certyfikatu.  
  
 Program WCF udostępnia obie te opcje w ramach zabezpieczeń transportu usługi MSMQ i są kluczowymi składnikami do zabezpieczenia transportu.  
  
 Domyślnie zabezpieczenia transportu są włączone.  
  
 W poniższych sekcjach opisano szczegółowo właściwości zabezpieczeń transportu powiązane z <xref:System.ServiceModel.NetMsmqBinding> i <xref:System.ServiceModel.MsmqIntegration.MsmqIntegrationBinding> .  
  
#### <a name="msmq-authentication-mode"></a>Tryb uwierzytelniania usługi MSMQ  

 <xref:System.ServiceModel.MsmqTransportSecurity.MsmqAuthenticationMode%2A>Określa, czy należy użyć zabezpieczeń domeny systemu Windows lub zabezpieczeń zewnętrznych opartych na certyfikatach w celu zabezpieczenia wiadomości. W obu trybach uwierzytelniania kanał transportu kolejkowanego WCF używa `CertificateValidationMode` określonego w konfiguracji usługi. Tryb walidacji certyfikatu określa mechanizm służący do sprawdzania poprawności certyfikatu.  
  
 Gdy zabezpieczenia transportu są włączone, ustawienie domyślne to <xref:System.ServiceModel.MsmqAuthenticationMode.WindowsDomain> .  
  
#### <a name="windows-domain-authentication-mode"></a>Tryb uwierzytelniania domeny systemu Windows  

 Wybór korzystania z zabezpieczeń systemu Windows wymaga integracji Active Directory. <xref:System.ServiceModel.MsmqAuthenticationMode.WindowsDomain> jest domyślnym trybem zabezpieczeń transportu. Po ustawieniu tej opcji kanał WCF dołącza identyfikator SID systemu Windows do wiadomości MSMQ i używa certyfikatu wewnętrznego uzyskanego z Active Directory. Usługa MSMQ używa tego certyfikatu wewnętrznego do zabezpieczenia wiadomości. Menedżer kolejki odbioru używa Active Directory do wyszukiwania i znajdowania zgodnego certyfikatu w celu uwierzytelnienia klienta i sprawdza, czy identyfikator SID również jest zgodny z klientem programu. Ten krok uwierzytelniania jest wykonywany, jeśli certyfikat wewnętrznie wygenerowany w przypadku `WindowsDomain` trybu uwierzytelniania lub zewnętrznie wygenerowany w przypadku `Certificate` trybu uwierzytelniania jest dołączony do komunikatu, nawet jeśli kolejka docelowa nie jest oznaczona jako wymagająca uwierzytelniania.  
  
> [!NOTE]
> Podczas tworzenia kolejki można oznaczyć kolejkę jako kolejkę uwierzytelnioną, aby wskazać, że kolejka wymaga uwierzytelniania komunikatów wysyłanych przez klienta do kolejki. Dzięki temu w kolejce nie są akceptowane nieuwierzytelnione komunikaty.  
  
 Identyfikator SID dołączony do wiadomości jest również używany do sprawdzania listy ACL kolejki docelowej, aby upewnić się, że klient ma uprawnienia do wysyłania komunikatów do kolejki.  
  
#### <a name="certificate-authentication-mode"></a>Tryb uwierzytelniania certyfikatu  

 Opcja używania trybu uwierzytelniania certyfikatów nie wymaga integracji Active Directory. W niektórych przypadkach, na przykład gdy usługa MSMQ jest zainstalowana w trybie grupy roboczej (bez integracji Active Directory) lub gdy do wysyłania komunikatów do kolejki jest używany protokół transferu protokołu niezawodnej obsługi komunikatów SOAP (SRMP), tylko <xref:System.ServiceModel.MsmqAuthenticationMode.Certificate> działa.  
  
 W przypadku wysyłania komunikatu programu WCF z programem <xref:System.ServiceModel.MsmqAuthenticationMode.Certificate> kanał WCF nie dołącza identyfikatora SID systemu Windows do wiadomości MSMQ. W związku z tym lista ACL kolejki docelowej musi zezwalać na `Anonymous` dostęp użytkowników do kolejki. Menedżer kolejki odbioru sprawdza, czy wiadomość MSMQ została podpisana przy użyciu certyfikatu, ale nie wykonuje żadnych operacji uwierzytelniania.  
  
 Certyfikat z informacjami o oświadczeniach i tożsamości jest wypełniany <xref:System.ServiceModel.ServiceSecurityContext> przez kanał transportowy w kolejce WCF. Usługa ta może używać tych informacji do wykonywania własnego uwierzytelniania nadawcy.  
  
### <a name="msmq-protection-level"></a>Poziom ochrony MSMQ  

 Poziom ochrony wskazuje, jak chronić komunikat usługi MSMQ, aby upewnić się, że nie został naruszony. Jest określony we <xref:System.ServiceModel.MsmqTransportSecurity.MsmqProtectionLevel%2A> właściwości. Wartość domyślna to <xref:System.Net.Security.ProtectionLevel.Sign>.  
  
#### <a name="sign-protection-level"></a>Podpisz poziom ochrony  

 Komunikat usługi MSMQ jest podpisywany przy użyciu wewnętrznie wygenerowanego certyfikatu podczas korzystania z `WindowsDomain` trybu uwierzytelniania lub certyfikatu wygenerowanego zewnętrznie podczas korzystania z `Certificate` trybu uwierzytelniania.  
  
#### <a name="sign-and-encrypt-protection-level"></a>Podpisywanie i szyfrowanie poziomu ochrony  

 Komunikat usługi MSMQ jest podpisywany przy użyciu wewnętrznego wygenerowanego certyfikatu podczas korzystania z `WindowsDomain` trybu uwierzytelniania lub certyfikatu wygenerowanego zewnętrznie podczas korzystania z `Certificate` trybu uwierzytelniania.  
  
 Oprócz podpisywania wiadomości komunikat usługi MSMQ jest szyfrowany przy użyciu klucza publicznego certyfikatu uzyskanego z Active Directory należącego do Menedżera kolejki odbioru, który hostuje kolejkę docelową. Menedżer kolejki wysyłania gwarantuje, że komunikat MSMQ jest szyfrowany podczas przesyłania. Menedżer kolejki odbioru odszyfrowuje komunikat usługi MSMQ przy użyciu klucza prywatnego jego certyfikatu wewnętrznego i zapisuje komunikat w kolejce (jeśli jest uwierzytelniany i autoryzowany) w postaci zwykłego tekstu.  
  
> [!NOTE]
> Aby zaszyfrować komunikat, wymagany jest Active Directory dostęp ( `UseActiveDirectory` Właściwość <xref:System.ServiceModel.NetMsmqBinding> musi być ustawiona na `true` ) i może być używana z obydwoma <xref:System.ServiceModel.MsmqAuthenticationMode.Certificate> i <xref:System.ServiceModel.MsmqAuthenticationMode.WindowsDomain> .  
  
#### <a name="none-protection-level"></a>Brak poziomu ochrony  

 Jest to implikowane <xref:System.ServiceModel.MsmqTransportSecurity.MsmqProtectionLevel%2A> , gdy jest ustawiony na <xref:System.Net.Security.ProtectionLevel.None> . Nie może to być prawidłowa wartość dla żadnych innych trybów uwierzytelniania.  
  
> [!NOTE]
> Jeśli komunikat usługi MSMQ jest podpisany, usługa MSMQ sprawdza, czy komunikat jest podpisany za pomocą dołączonego certyfikatu (wewnętrznego lub zewnętrznego) niezależnie od stanu kolejki, czyli kolejki uwierzytelnionej.  
  
### <a name="msmq-encryption-algorithm"></a>Algorytm szyfrowania usługi MSMQ  

 Algorytm szyfrowania określa algorytm używany do szyfrowania wiadomości MSMQ w sieci. Ta właściwość jest używana tylko wtedy <xref:System.ServiceModel.MsmqTransportSecurity.MsmqProtectionLevel%2A> , gdy jest ustawiona na <xref:System.Net.Security.ProtectionLevel.EncryptAndSign> .  
  
 Obsługiwane algorytmy to `RC4Stream` i `AES` i wartość domyślna to `RC4Stream` .  
  
 Algorytmu można używać `AES` tylko wtedy, gdy nadawca ma zainstalowaną usługę MSMQ 4,0. Ponadto kolejka docelowa musi być również hostowana w usłudze MSMQ 4,0.  
  
### <a name="msmq-hash-algorithm"></a>Algorytm wyznaczania wartości skrótu usługi MSMQ  

 Algorytm wyznaczania wartości skrótu określa algorytm używany do tworzenia podpisu cyfrowego wiadomości MSMQ. Menedżer kolejki odbioru używa tego samego algorytmu do uwierzytelniania wiadomości MSMQ. Ta właściwość jest używana tylko wtedy <xref:System.ServiceModel.MsmqTransportSecurity.MsmqProtectionLevel%2A> , gdy jest ustawiona na <xref:System.Net.Security.ProtectionLevel.Sign> lub <xref:System.Net.Security.ProtectionLevel.EncryptAndSign> .  
  
 Obsługiwane algorytmy to `MD5` , `SHA1` , `SHA256` i `SHA512` . Wartość domyślna to `SHA1`.

 Ze względu na kolizje problemów z algorytmem MD5/SHA1 firma Microsoft zaleca SHA256ą lub lepszą.
  
## <a name="see-also"></a>Zobacz też

- [Omówienie kolejek](queues-overview.md)
- [Pojęcia dotyczące zabezpieczeń](security-concepts.md)
- [Zabezpieczanie usług i klientów](securing-services-and-clients.md)
