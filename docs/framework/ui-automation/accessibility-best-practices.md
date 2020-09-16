---
title: Najlepsze praktyki dotyczące ułatwień dostępu
description: Poznaj najlepsze rozwiązania dotyczące ułatwień dostępu w programie .NET. Eksploruj dostęp programistyczny, ustawienia użytkownika, Visual graficzny projekt interfejsu użytkownika, nawigację i interfejsy Multimodal.
ms.date: 03/30/2017
helpviewer_keywords:
- best practices for accessibility
- accessibility, best practices for
ms.assetid: e6d5cd98-21a3-4b01-999c-fb953556d0e6
ms.openlocfilehash: 1c01cfe8fdfb285ee5cbc586cc0c549365ef72ee
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/15/2020
ms.locfileid: "90543150"
---
# <a name="accessibility-best-practices"></a>Najlepsze rozwiązania dotyczące ułatwień dostępu

> [!NOTE]
> Ten artykuł jest przeznaczony .NET Framework dla deweloperów, którzy chcą korzystać z klas automatyzacji zarządzanego interfejsu użytkownika zdefiniowanych w <xref:System.Windows.Automation> przestrzeni nazw. Najnowsze informacje o automatyzacji interfejsu użytkownika znajdują się w temacie [Windows Automation API: Automatyzacja interfejsu użytkownika](/windows/win32/winauto/entry-uiauto-win32).  
  
 Wdrożenie następujących najlepszych rozwiązań w zakresie kontroli lub aplikacji poprawi ich dostępność dla osób korzystających z urządzeń z technologią pomocniczą. Wiele z tych najlepszych rozwiązań koncentruje się na dobrym projekcie interfejsu użytkownika. Każde najlepsze rozwiązanie obejmuje informacje o implementacji dla formantów i aplikacji Windows Presentation Foundation (WPF). W wielu przypadkach pracy, która spełnia te najlepsze rozwiązania, jest już zawarty w kontrolkach WPF.  
  
<a name="Programmatic_Access"></a>
## <a name="programmatic-access"></a>Dostęp programowy  
 Dostęp programistyczny polega na zapewnieniu, że wszystkie elementy interfejsu użytkownika są oznaczone etykietami, wartości właściwości są ujawniane i wywoływane są odpowiednie zdarzenia. W przypadku standardowych formantów WPF większość tej pracy jest już wykonywana przez program <xref:System.Windows.Automation.Peers.AutomationPeer> . Niestandardowe kontrolki wymagają dodatkowej pracy, aby zapewnić, że dostęp programistyczny jest prawidłowo zaimplementowany.  
  
<a name="Enable_Programmatic_Access_to_all_UI_Elements_and_Text"></a>
### <a name="enable-programmatic-access-to-all-ui-elements-and-text"></a>Włącz dostęp programistyczny do wszystkich elementów interfejsu użytkownika i tekstu  
 Elementy interfejsu użytkownika powinny włączać dostęp programistyczny. Jeśli interfejs użytkownika jest standardową kontrolką WPF, obsługa dostępu programowego jest zawarta w kontrolce. Jeśli formant jest formantem niestandardowym — formantem, który został poddany do podklasy ze wspólnej kontrolki lub kontrolki, która została poddana kontroli, należy sprawdzić <xref:System.Windows.Automation.Peers.AutomationPeer> implementację obszarów, które mogą wymagać modyfikacji.  
  
 Zgodnie z tym najlepszym rozwiązaniem dostawcy technologii pomocniczej mogą identyfikować elementy interfejsu użytkownika produktu i manipulować nimi.  
  
<a name="Place_Names__Titles_and_Descriptions_on_UI_Objects_"></a>
### <a name="place-names-titles-and-descriptions-on-ui-objects-frames-and-pages"></a>Umieszczaj nazwy, tytuły i opisy dotyczące obiektów, ramek i stron interfejsu użytkownika  
 Technologie pomocnicze, zwłaszcza czytniki ekranu, wykorzystują tytuł, aby zrozumieć lokalizację ramki, obiektu lub strony w schemacie nawigacji. W związku z tym tytuł musi być opisowy. Na przykład tytuł strony sieci Web "Strona sieci Web firmy Microsoft" jest bezużyteczny, jeśli użytkownik przejdzie głęboko do określonego obszaru. Opisowy tytuł ma krytyczne znaczenie dla użytkowników niewidomych i niezależnych od czytników zawartości ekranu. Podobnie w przypadku formantów WPF <xref:System.Windows.Automation.AutomationProperties.NameProperty> i <xref:System.Windows.Automation.AutomationProperties.HelpTextProperty> są ważne w przypadku urządzeń z technologią pomocniczą.  
  
 Korzystając z tej najlepszej wskazówki, można używać technologii pomocniczych do identyfikowania i manipulowania interfejsem użytkownika w przykładowych formantach i aplikacjach.  
  
<a name="Ensure_Programmatic_Events_are_Triggered_by_all_UI"></a>
### <a name="ensure-programmatic-events-are-triggered-by-all-ui-activities"></a>Upewnij się, że zdarzenia programistyczne są wyzwalane przez wszystkie działania interfejsu użytkownika  
 Zgodnie z tym najlepszym rozwiązaniem, technologie wspomagające umożliwiają nasłuchiwanie zmian w interfejsie użytkownika i powiadamianie użytkownika o tych zmianach.  
  
<a name="User_Settings"></a>
## <a name="user-settings"></a>Ustawienia użytkownika  
 Najlepszym rozwiązaniem w tej sekcji jest zagwarantowanie, że formanty lub aplikacje nie zastępują ustawień użytkownika.  
  
<a name="Respect_all_System_Wide_Settings_and_do_not_Interfere"></a>
### <a name="respect-all-system-wide-settings-and-do-not-interfere-with-accessibility-functions"></a>Uwzględnij wszystkie ustawienia systemowe i nie zakłócaj działania funkcji ułatwień dostępu  
 Użytkownicy mogą używać panelu sterowania do ustawiania niektórych flag dla całego systemu; inne flagi można ustawić programowo. Tych ustawień nie należy zmieniać przez kontrolki ani aplikacje. Ponadto aplikacje muszą obsługiwać ustawienia ułatwień dostępu dla swojego systemu operacyjnego hosta.  
  
 Zgodnie z tym najlepszym rozwiązaniem użytkownicy mogą ustawiać ustawienia ułatwień dostępu i wiedzieć, że te ustawienia nie zostaną zmienione przez aplikacje.  
  
<a name="Visual_UI_Design"></a>
## <a name="visual-ui-design"></a>Projekt wizualnego interfejsu użytkownika  
 Najlepsze rozwiązania w tej sekcji zapewniają, że kontrolki lub aplikacje wykorzystują kolor i obrazy efektywnie i mogą być używane przez technologie pomocnicze.  
  
<a name="Don_t_Hard_Code_Colors"></a>
### <a name="dont-hard-code-colors"></a>Nie należy trwale kodować kolorów  
 Osoby, które są w kolorze niewidomym, mają słabą wizję lub używają czerni i białych ekranów, mogą nie być w stanie używać aplikacji z ustalonymi kolorami.  
  
 Zgodnie z tym najlepszym rozwiązaniem użytkownicy dostosowują kombinacje kolorów na podstawie indywidualnych potrzeb.  
  
<a name="Support_High_Contrast_and_all_System_Display_Attributes"></a>
### <a name="support-high-contrast-and-all-system-display-attributes"></a>Obsługa duży kontrast i wszystkie atrybuty wyświetlania systemu  
 Aplikacje nie powinny zakłócać ani wyłączać wybranych przez użytkownika ustawień kontrastu systemu, kolorów ani opcji wyświetlania w całym systemie. Ustawienia dotyczące całego systemu przyjęte przez użytkownika rozszerzają dostępność aplikacji, dlatego nie powinny być wyłączone ani nieuznawane przez aplikacje. Kolor powinien być używany w odpowiedniej kombinacji pierwszego planu w tle, aby zapewnić odpowiedni kontrast. Nie mieszaj niepowiązanych kolorów i nie odwracaj kolorów.  
  
 Wielu użytkowników wymaga określonych kombinacji o wysokim kontraście, takich jak biały tekst na czarnym tle. Rysowanie odpisano, jako czarny tekst na białym tle powoduje, że tło spada na pierwszy plan i może utrudnić odczyt dla niektórych użytkowników.  
  
<a name="Ensure_all_UI_Correctly_Scales_by_any_DPI_Setting"></a>
### <a name="ensure-all-ui-correctly-scales-by-any-dpi-setting"></a>Upewnij się, że wszystkie elementy interfejsu użytkownika są prawidłowo skalowane według dowolnego ustawienia DPI  
 Upewnij się, że wszystkie elementy interfejsu użytkownika mogą być prawidłowo skalowane przy użyciu dowolnego ustawienia DPI. Upewnij się również, że elementy interfejsu użytkownika mieszczą się na ekranie 1024 x 768 z 120 kropkami na cal (dpi).  
  
<a name="Navigation"></a>
## <a name="navigation"></a>Nawigacja  
 Najlepsze rozwiązania w tej sekcji zapewniają, że nawigacja została zastosowana w przypadku formantów i aplikacji.  
  
<a name="Provide_Keyboard_Interface_for_all_UI_Elements"></a>
### <a name="provide-keyboard-interface-for-all-ui-elements"></a>Zapewnianie interfejsu klawiatury dla wszystkich elementów interfejsu użytkownika  
 Tabulatory, szczególnie w przypadku starannego planowania, umożliwiają użytkownikom innym sposobem nawigowania po interfejsie użytkownika.  
  
 Aplikacje powinny udostępniać następujące interfejsy klawiatury:  
  
- tabulatory dla wszystkich kontrolek, z którymi użytkownik może korzystać, takich jak przyciski, linki lub pola listy  
  
- kolejność tabulacji logicznej  
  
<a name="Show_the_Keyboard_Focus"></a>
### <a name="show-the-keyboard-focus"></a>Pokaż fokus klawiatury  
 Użytkownicy muszą wiedzieć, który obiekt ma fokus klawiatury, aby można było przewidzieć efekt ich naciśnięć klawiszy. Aby wyróżnić fokus klawiatury, Użyj kolorów, czcionek lub grafiki, takich jak prostokąty lub powiększenia. Aby audibly wyróżnić fokus klawiatury, Zmień głośność, gęstość lub jakość tonalną.  
  
 Aby uniknąć pomyłek, aplikacje powinny ukrywać wszystkie wskaźniki fokusu wizualnego i przyciemniać zaznaczenia, które znajdują się w nieaktywnym systemie Windows (lub okienka).  
  
 Aplikacje powinny wykonać następujące czynności z fokusem klawiatury:  
  
- jeden element powinien zawsze mieć fokus klawiatury  
  
- fokus klawiatury powinien być widoczny i oczywisty  
  
- Wybory i/lub elementy skoncentrowane powinny być wyróżnione wizualnie  
  
<a name="Support_Navigation_Standards_and_Powerful_Navigation"></a>
### <a name="support-navigation-standards-and-powerful-navigation-schemes"></a>Obsługuj standardy nawigacji i zaawansowane schematy nawigacji  
 Różne aspekty nawigacji klawiaturowej zapewniają różne sposoby nawigowania po interfejsie użytkownika.  
  
 Aplikacje powinny udostępniać następujące interfejsy klawiatury:  
  
- klawisze skrótów i podkreślone klawisze dostępu dla wszystkich poleceń, menu i kontrolek  
  
- skróty klawiaturowe do ważnych linków  
  
- wszystkie elementy menu mają klucz dostępu; wszystkie przyciski mają klawisze skrótów, a wszystkie polecenia mają klawisz akceleratora.  
  
<a name="Do_not_let_Mouse_Location_Interfere_with_Keyboard"></a>
### <a name="do-not-let-mouse-location-interfere-with-keyboard-navigation"></a>Nie Zezwalaj na zakłócanie lokalizacji myszy przy użyciu klawiatury  
 Lokalizacja myszy nie powinna zakłócać nawigowania po klawiaturze. Jeśli na przykład mysz jest umieszczona w pewnym miejscu i użytkownik przechodzi przy użyciu klawiatury, kliknięcie myszą nie powinno nastąpić, chyba że zostanie zainicjowany przez użytkownika.  
  
<a name="Multimodal_Interface"></a>
## <a name="multimodal-interface"></a>Multimodal, interfejs  
 Najlepsze rozwiązania w tej sekcji zapewniają, że interfejs użytkownika aplikacji zawiera alternatywy dla elementów wizualizacji.  
  
<a name="Provide_User_Selectable_Equivalents_for_Non_Text"></a>
### <a name="provide-user-selectable-equivalents-for-non-text-elements"></a>Zapewnianie odpowiedników wybieranych przez użytkownika dla elementów innych niż tekstowe  
 Dla każdego elementu nie będącego tekstem, należy wybrać odpowiedni dla użytkownika tekst, transkrypcje lub opisy audio, takie jak tekst alternatywny, napisy lub wizualne Opinie.  
  
 Elementy inne niż tekstowe obejmują szeroką gamę elementów interfejsu użytkownika, takich jak obrazy, regiony mapy obrazu, animacje, applety, ramki, skrypty, przyciski graficzne, dźwięki, autonomiczne pliki audio i wideo. Elementy inne niż tekstowe są ważne, gdy zawierają informacje wizualne, mowę lub ogólne informacje o dźwięku, do których użytkownik potrzebuje dostępu, aby zrozumieć zawartość interfejsu użytkownika.  
  
<a name="Use_Color_but_also_Provide_Alternatives_to_Color"></a>
### <a name="use-color-but-also-provide-alternatives-to-color"></a>Użyj koloru, ale również Podaj alternatywy dla koloru  
 Użyj koloru, aby ulepszyć, wyróżnić lub powtórzyć powtarzanie informacji, które są wyświetlane w inny sposób, ale nie Komunikuj się z informacjami przy użyciu samego koloru. Użytkownicy, którzy są kolorami niewidomymi lub mają wyświetlacz monochromatyczny, potrzebują alternatywy do kolorowania.  
  
<a name="Use_Standard_Input_APIs_with_Devices_Independent"></a>
### <a name="use-standard-input-apis-with-device-independent-calls"></a>Używanie standardowych interfejsów API wejścia z wywołaniami niezależnymi od urządzenia  
 Wywołania niezależne od urządzenia zapewniają równość funkcji klawiatury i myszy, a jednocześnie zapewniają technologię pomocniczą z wymaganymi informacjami o interfejsie użytkownika.  
  
## <a name="see-also"></a>Zobacz także

- <xref:System.Windows.Automation.Peers>
- [NumericUpDown kontrolkę niestandardową z motywem i przykładem obsługi automatyzacji interfejsu użytkownika](/previous-versions/dotnet/netframework-3.5/ms771573(v=vs.90))
- [Wskazówki dotyczące projektowania interfejsu użytkownika klawiatury](/previous-versions/windows/desktop/dnacc/guidelines-for-keyboard-user-interface-design)
