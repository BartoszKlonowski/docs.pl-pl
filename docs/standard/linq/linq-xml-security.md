---
title: LINQ to XML zabezpieczenia — LINQ to XML
description: Dowiedz się więcej o rozwiązywaniu problemów z zabezpieczeniami LINQ to XML i sposobach ograniczenia zagrożeń bezpieczeństwa.
ms.date: 07/20/2015
ms.assetid: ef2c0dc9-ecf9-4c17-b24e-144184ab725f
ms.openlocfilehash: 72dd2bfe2a3f0edb69645daf4625ba24fb56732b
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/08/2020
ms.locfileid: "89553331"
---
# <a name="linq-to-xml-security"></a>Zabezpieczenia LINQ to XML

W tym artykule opisano problemy z zabezpieczeniami powiązane z LINQ to XML i przedstawiono wskazówki dotyczące ograniczania zagrożeń bezpieczeństwa.

## <a name="linq-to-xml-security-overview"></a>Omówienie zabezpieczeń LINQ to XML

LINQ to XML zaprojektowano więcej dla wygody programowania niż w przypadku aplikacji po stronie serwera z rygorystycznymi wymaganiami dotyczącymi bezpieczeństwa. Większość scenariuszy XML polega na przetwarzaniu zaufanych dokumentów XML, a nie przetwarzaniu niezaufanych dokumentów XML, które są przekazywane do serwera. LINQ to XML jest zoptymalizowany pod kątem tych scenariuszy.

Jeśli konieczne jest przetworzenie niezaufanych danych z nieznanych źródeł, firma Microsoft zaleca użycie wystąpienia <xref:System.Xml.XmlReader> klasy, która została skonfigurowana do filtrowania znanych ataków typu "odmowa usługi" (DOS).

Jeśli skonfigurowano <xref:System.Xml.XmlReader> , aby ograniczyć ataki typu "odmowa usługi", można użyć tego czytnika do wypełnienia drzewa LINQ to XML i nadal korzystać z ulepszeń programistycznych LINQ to XML. Wiele technik zaradczych wiąże się z tworzeniem czytników skonfigurowanych do ograniczania problemu zabezpieczeń, a następnie tworzenia wystąpienia drzewa XML za pomocą skonfigurowanego czytnika.

Język XML jest wewnętrznie narażony na ataki typu "odmowa usługi", ponieważ nie ma ograniczenia rozmiaru, głębokości, rozmiaru nazwy elementu i nie tylko. Bez względu na składnik używany do przetwarzania kodu XML, zawsze należy przygotować się do odtworzenia domeny aplikacji, jeśli używa nadmiernych zasobów.

## <a name="mitigation-of-xml-xsd-xpath-and-xslt-attacks"></a>Eliminowanie ataków XML, XSD, XPath i XSLT

LINQ to XML jest oparta na <xref:System.Xml.XmlReader> i <xref:System.Xml.XmlWriter> . LINQ to XML obsługuje XSD i XPath za pomocą metod rozszerzających <xref:System.Xml.Schema?displayProperty=nameWithType> w <xref:System.Xml.XPath?displayProperty=nameWithType> przestrzeniach nazw i. Korzystając z <xref:System.Xml.XmlReader> klas, <xref:System.Xml.XPath.XPathNavigator> , i <xref:System.Xml.XmlWriter> w połączeniu z LINQ to XML, można wywołać XSLT, aby przekształcić drzewa XML.

W przypadku korzystania z mniej bezpiecznego środowiska istnieje wiele problemów z zabezpieczeniami, które są skojarzone z językiem XML, i używania klas w <xref:System.Xml?displayProperty=nameWithType> ,, <xref:System.Xml.Schema?displayProperty=nameWithType> <xref:System.Xml.XPath?displayProperty=nameWithType> i <xref:System.Xml.Xsl?displayProperty=nameWithType> . Te problemy obejmują, ale nie są ograniczone do, następujące:

- XSD, XPath i XSLT są językami opartymi na ciągach, w których można określić operacje, które zużywają dużo czasu lub pamięci. W celu sprawdzenia, czy ciągi nie są złośliwe, czy też monitorowania i łagodzenia, że Ocena tych ciągów będzie powodować nadmierne użycie zasobów systemowych, należy wziąć pod uwagę Programiści aplikacji, którzy mają ciągi XSD, XPath lub XSLT z niezaufanych źródeł.
- Schematy XSD (w tym schematy wbudowane) są podatne na ataki typu "odmowa usługi"; nie należy akceptować schematów z niezaufanych źródeł.
- XSD i XSLT mogą zawierać odwołania do innych plików, a takie odwołania mogą powodować ataki między strefami i między domenami.
- Jednostki zewnętrzne w elementach DTD mogą powodować ataki między strefami i między domenami.
- Definicje DTD są podatne na ataki typu "odmowa usługi".
- Wyjątkowo głębokie dokumenty XML mogą powodować problemy z odmową usługi; może zajść potrzeba ograniczenia głębokości dokumentów XML.
- Nie Akceptuj składników pomocniczych, takich jak <xref:System.Xml.NameTable> , <xref:System.Xml.XmlNamespaceManager> i <xref:System.Xml.XmlResolver> obiektów, z niezaufanych zestawów.
- Odczytywanie danych w fragmentach w celu ograniczenia ataków na duże dokumenty.
- Bloki skryptów w arkuszach stylów XSLT mogą uwidaczniać wiele ataków.
- Uważnie sprawdzaj przed konstruowaniem dynamicznych wyrażeń XPath.

## <a name="linq-to-xml-security-issues"></a>LINQ to XML problemy z zabezpieczeniami

Problemy z bezpieczeństwem w tym artykule nie są wyświetlane w żadnej określonej kolejności. Wszystkie problemy są ważne i powinny być odpowiednio rozwiązane.

Pomyślne podniesienie uprawnień ataku daje złośliwemu zestawowi większą kontrolę nad jego środowiskiem. Pomyślne podniesienie uprawnień ataku może spowodować ujawnienie danych, odmowa usługi i nie tylko.

Aplikacje nie powinny ujawniać danych użytkownikom, którzy nie mają uprawnień do wyświetlania tych danych.

Ataki typu "odmowa usługi" powodują, że analizator XML lub LINQ to XML zużywa nadmierne ilości pamięci lub czasu procesora CPU. Ataki typu "odmowa usługi" są uważane za mniej surowe niż podniesienie uprawnień lub ujawnienie danych. Jednak są ważne w scenariuszu, w którym serwer musi przetwarzać dokumenty XML z niezaufanych źródeł.

### <a name="dont-expose-error-messages-to-untrusted-callers"></a>Nie ujawniaj komunikatów o błędach niezaufanym wywołującym

Opis błędu może ujawnić dane, takie jak dane, które są przekształcane, nazwy plików lub szczegóły implementacji. Komunikaty o błędach nie powinny być ujawnione dla wywołujących, które nie są zaufane. Należy wychwycić wszystkie błędy i zgłosić błędy przy użyciu własnych niestandardowych komunikatów o błędach.

### <a name="dont-call-codeaccesspermissionsassert-in-an-event-handler"></a>Nie wywołuj metody CodeAccessPermissions. Assert w obsłudze zdarzeń

Zestaw może mieć mniejsze lub większe uprawnienia. Zestaw, który ma większe uprawnienia, ma większą kontrolę nad komputerem i jego środowiskami.

Jeśli kod w zestawie z większą liczbą uprawnień jest wywoływany <xref:System.Security.CodeAccessPermission.Assert%2A?displayProperty=nameWithType> w programie obsługi zdarzeń, a następnie drzewo XML zostanie przesłane do złośliwego zestawu z ograniczonymi uprawnieniami, złośliwy zestaw może spowodować podniesienie poziomu zdarzenia. Ponieważ zdarzenie uruchamia kod, który znajduje się w zestawie z większymi uprawnieniami, złośliwy zestaw będzie działać z podwyższonym poziomem uprawnień.

Firma Microsoft zaleca, aby nie wywoływać <xref:System.Security.CodeAccessPermission.Assert%2A?displayProperty=nameWithType> w programie obsługi zdarzeń.

### <a name="dont-accept-dtds-from-untrusted-sources"></a>Nie Akceptuj elementów DTD z niezaufanych źródeł

Jednostki w elementach DTD są z natury niebezpieczne. Istnieje możliwość złośliwego dokumentu XML zawierającego DTD, który może spowodować, że analizator będzie używał całej pamięci i czasu procesora, powodując atak typu "odmowa usługi". W związku z tym w LINQ to XML przetwarzanie DTD jest domyślnie wyłączone. Nie należy akceptować elementów DTD z niezaufanych źródeł.

Przykładem akceptowania elementów DTD z niezaufanych źródeł jest aplikacja sieci Web, która umożliwia użytkownikom sieci Web przekazywanie pliku XML, który odwołuje się do pliku DTD i DTD. Po sprawdzeniu poprawności pliku złośliwy element DTD może wykonać atak typu "odmowa usługi" na serwerze. Innym przykładem akceptowania elementów DTD z niezaufanych źródeł jest odwołanie do elementu DTD w udziale sieciowym, który umożliwia także anonimowy dostęp do FTP.

### <a name="avoid-excessive-buffer-allocation"></a>Unikaj nadmiernej alokacji buforu

Deweloperzy aplikacji powinni mieć świadomość, że wyjątkowo duże źródła danych mogą prowadzić do wyczerpania zasobów i ataków typu "odmowa usługi".

Jeśli złośliwy użytkownik przesyła lub przekaże bardzo duży dokument XML, może to spowodować, że LINQ to XML zużywa nadmierne zasoby systemowe. Może to stanowić atak typu "odmowa usługi". Aby tego uniknąć, można ustawić <xref:System.Xml.XmlReaderSettings.MaxCharactersInDocument%2A?displayProperty=nameWithType> Właściwość i utworzyć czytnik, który jest następnie ograniczony w rozmiarze dokumentu, który może zostać załadowany. Następnie należy użyć czytnika, aby utworzyć drzewo XML.

Na przykład jeśli wiesz, że maksymalny oczekiwany rozmiar dokumentów XML pochodzących z niezaufanego źródła będzie mniejszy niż 50 000 bajtów, ustaw wartość <xref:System.Xml.XmlReaderSettings.MaxCharactersInDocument%2A?displayProperty=nameWithType> na 100 000. Nie będzie to encumber przetwarzania dokumentów XML i w tym samym czasie będzie ograniczać zagrożenia odmowy usługi, w przypadku których można przekazać dokumenty, które mogą zużywać duże ilości pamięci.

### <a name="avoid-excess-entity-expansion"></a>Unikaj nadmiernego rozszerzania jednostek

Jednym z znanych ataków typu "odmowa usługi" w przypadku korzystania z DTD jest dokument, który powoduje nadmierne rozwinięcie jednostek. Aby tego uniknąć, można ustawić <xref:System.Xml.XmlReaderSettings.MaxCharactersFromEntities%2A?displayProperty=nameWithType> Właściwość i utworzyć czytnik, który jest następnie ograniczony w liczbie znaków będących wynikiem rozwinięcia jednostki. Następnie należy użyć czytnika, aby utworzyć drzewo XML.

### <a name="limit-the-depth-of-the-xml-hierarchy"></a>Ograniczanie głębokości hierarchii XML

Jednym z możliwych ataków typu "odmowa usługi" jest przesłanie dokumentu, który ma nadmierną Głębokość hierarchii. Aby tego uniknąć, można otoczyć obiekt <xref:System.Xml.XmlReader> we własnej klasie, która zlicza elementy. Jeśli głębokość przekracza wstępnie określony poziom, można przerwać przetwarzanie złośliwego dokumentu.

### <a name="protect-against-untrusted-xmlreader-or-xmlwriter-implementations"></a>Ochrona przed niezaufanymi implementacjami elementu XmlReader lub XmlWriter

Administratorzy powinni upewnić się, że wszystkie dostarczone zewnętrznie <xref:System.Xml.XmlReader> lub <xref:System.Xml.XmlWriter> implementacje mają silne nazwy i zostały zarejestrowane w konfiguracji maszyny. Zapobiega to załadowaniu złośliwego kodu jako czytnika lub składnika zapisywania.

### <a name="periodically-free-objects-that-reference-xname"></a>Okresowe bezpłatne obiekty odwołujące się do XName

Aby chronić przed niektórymi atakami, programiści aplikacji powinny bezpłatnie zwolnić wszystkie obiekty, które odwołują się do <xref:System.Xml.Linq.XName> obiektu w domenie aplikacji.

### <a name="protect-against-random-xml-names"></a>Ochrona przed przypadkowymi nazwami XML

Aplikacje, które pobierają dane z niezaufanych źródeł, powinny rozważyć użycie <xref:System.Xml.XmlReader> zawiniętego w kodzie niestandardowym w celu sprawdzenia możliwości losowych nazw XML i przestrzeni nazw. Jeśli zostaną wykryte takie losowe nazwy XML i przestrzenie nazw, aplikacja będzie mogła przerwać przetwarzanie złośliwego dokumentu.

Możesz chcieć ograniczyć liczbę nazw w danej przestrzeni nazw (łącznie z nazwami w obszarze brak przestrzeni nazw) do rozsądnego limitu.

### <a name="serialize-linq-to-xml-objects-to-xml-text-before-passing-the-data-to-an-untrusted-component"></a>Serializacja LINQ to XML obiektów do tekstu XML przed przekazaniem danych do niezaufanego składnika

LINQ to XML może służyć do tworzenia potoków przetwarzania, w których różne składniki aplikacji ładują, weryfikują, wykonują zapytania, Przekształć, aktualizują i zapisują dane XML przesyłane między składnikami jako drzewa XML. Może to pomóc zoptymalizować wydajność, ponieważ obciążenie związane z ładowaniem i serializowaniem obiektów do tekstu XML odbywa się tylko na końcach potoku. Deweloperzy muszą mieć jednak świadomość, że wszystkie adnotacje i programy obsługi zdarzeń utworzone przez jeden składnik są dostępne dla innych składników. Może to spowodować powstanie kilku luk w zabezpieczeniach, jeśli składniki mają różne poziomy zaufania. Aby utworzyć bezpieczne potoki w mniej zaufanych składnikach, należy serializować LINQ to XML obiektów do tekstu XML przed przekazaniem danych do niezaufanego składnika.

Niektóre zabezpieczenia są udostępniane przez środowisko uruchomieniowe języka wspólnego (CLR). Na przykład, składnik, który nie zawiera klasy prywatnej, nie może uzyskać dostępu do adnotacji, które są określone przez tę klasę. Jednakże adnotacje mogą być usuwane przez składniki, które nie mogą ich odczytać. Może to być przyczyną naruszenia ataku.

## <a name="see-also"></a>Zobacz też

- [Przegląd LINQ to XML](linq-xml-overview.md)
