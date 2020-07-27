---
title: Przegląd Autorstwo formantów
description: Rozszerzalność formantów Windows Presentation Foundation minimalizuje potrzebę tworzenia niestandardowych kontrolek. Dowiedz się, jak utworzyć nową kontrolkę, w razie potrzeby.
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- controls [WPF], authoring overview
- authoring overview for controls [WPF]
ms.assetid: 3d864748-cff0-4e63-9b23-d8e5a635b28f
ms.openlocfilehash: 600eb193613846d7eeeb626a6dfd317d2592f809
ms.sourcegitcommit: 87cfeb69226fef01acb17c56c86f978f4f4a13db
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/24/2020
ms.locfileid: "87166346"
---
# <a name="control-authoring-overview"></a>Przegląd tworzenia formantów

Rozszerzalność [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] modelu sterowania znacznie zmniejsza konieczność utworzenia nowej kontrolki. Jednak w niektórych przypadkach nadal może być konieczne utworzenie kontrolki niestandardowej. W tym temacie omówiono funkcje, które minimalizują potrzebę tworzenia kontrolek niestandardowych i różnych modeli tworzenia formantów w programie [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] . W tym temacie pokazano również, jak utworzyć nową kontrolkę.

<a name="when_to_write_a_new_control"></a>

## <a name="alternatives-to-writing-a-new-control"></a>Alternatywy do napisania nowej kontrolki

Historycznie, jeśli chcesz uzyskać dostosowane środowisko z istniejącej kontrolki, możesz zmienić standardowe właściwości kontrolki, takie jak kolor tła, Szerokość obramowania i rozmiar czcionki. Jeśli chcesz zwiększyć wygląd lub zachowanie kontrolki poza tymi wstępnie zdefiniowanymi parametrami, musisz utworzyć nową kontrolkę, zazwyczaj przez dziedziczenie z istniejącej kontrolki i zastępowanie metody odpowiedzialnej za rysowanie formantu.  Mimo że nadal jest to opcja, [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] umożliwia dostosowanie istniejących kontrolek przy użyciu rozbudowanego modelu zawartości, stylów, szablonów i wyzwalaczy. Poniższa lista zawiera przykłady zastosowania tych funkcji do tworzenia niestandardowych i spójnych środowisk bez konieczności tworzenia nowej kontrolki.

- **Zawartość rozbudowana.** Wiele standardowych [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] formantów obsługuje rozbudowaną zawartość. Na przykład właściwość content elementu <xref:System.Windows.Controls.Button> jest typu <xref:System.Object> , dlatego teoretycznie wszystko można wyświetlić na <xref:System.Windows.Controls.Button> .  Aby przycisk wyświetlał obraz i tekst, można dodać obraz i a <xref:System.Windows.Controls.TextBlock> do <xref:System.Windows.Controls.StackPanel> i przypisać <xref:System.Windows.Controls.StackPanel> do <xref:System.Windows.Controls.ContentControl.Content%2A> właściwości. Ponieważ kontrolki mogą wyświetlać [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] elementy wizualne i dowolne dane, trzeba utworzyć nową kontrolkę lub zmodyfikować istniejącą kontrolkę, aby obsługiwała złożoną wizualizację. Aby uzyskać więcej informacji na temat modelu zawartości dla <xref:System.Windows.Controls.Button> i innych modeli zawartości w programie [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] , zobacz [WPF content model](wpf-content-model.md).

- **Style.** A <xref:System.Windows.Style> to zbiór wartości, które reprezentują właściwości kontrolki. Za pomocą stylów można utworzyć reprezentację do wielokrotnego użytku dla żądanego wyglądu i zachowania kontrolki bez konieczności pisania nowej kontrolki. Załóżmy na przykład, że chcesz <xref:System.Windows.Controls.TextBlock> , aby wszystkie kontrolki miały czcionkę Red, Arial o rozmiarze 14. Styl można utworzyć jako zasób i odpowiednio ustawić odpowiednie właściwości. Następnie każde <xref:System.Windows.Controls.TextBlock> dodanie do aplikacji będzie miało taki sam wygląd.

- **Szablony danych.** A <xref:System.Windows.DataTemplate> umożliwia dostosowanie sposobu wyświetlania danych w formancie. Na przykład, <xref:System.Windows.DataTemplate> można użyć, aby określić, jak dane są wyświetlane w <xref:System.Windows.Controls.ListBox> .  Aby zapoznać się z przykładem, zobacz [tworzenia szablonów danych — omówienie](../data/data-templating-overview.md).  Oprócz dostosowywania wyglądu danych, <xref:System.Windows.DataTemplate> może obejmować elementy interfejsu użytkownika, co zapewnia dużą elastyczność w niestandardowym interfejsów użytkownika.  Na przykład przy użyciu <xref:System.Windows.DataTemplate> , można utworzyć, <xref:System.Windows.Controls.ComboBox> w którym każdy element zawiera pole wyboru.

- **Szablony kontrolek.** Wiele kontrolek w [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] użyciu służy <xref:System.Windows.Controls.ControlTemplate> do definiowania struktury i wyglądu kontrolki, która oddziela wygląd formantu od funkcjonalności formantu. Można radykalnie zmienić wygląd kontrolki przez ponowne zdefiniowanie jej <xref:System.Windows.Controls.ControlTemplate> .  Załóżmy na przykład, że chcesz, aby formant wyglądał jak Sygnalizator uliczny. Ten formant ma prosty interfejs użytkownika i jego funkcje.  Kontrolka jest trzema kołami, tylko jeden z nich może być wciśnięty w czasie. Po pewnym odbiciu można się zastanowić, że <xref:System.Windows.Controls.RadioButton> oferuje funkcje tylko jednego z wybranych naraz, ale domyślny wygląd wyglądu <xref:System.Windows.Controls.RadioButton> nie wygląda tak jak sygnalizatory sygnalizatora ulicznego.  Ponieważ <xref:System.Windows.Controls.RadioButton> używa szablonu kontrolki do definiowania jego wyglądu, można łatwo zmienić jego definicję, <xref:System.Windows.Controls.ControlTemplate> Aby dopasować się do wymagań kontrolki, i użyć przycisków radiowych, aby utworzyć Wskaźnik sygnalizatora.

  > [!NOTE]
  > Chociaż <xref:System.Windows.Controls.RadioButton> może użyć elementu <xref:System.Windows.DataTemplate> , a <xref:System.Windows.DataTemplate> nie jest wystarczający w tym przykładzie.  <xref:System.Windows.DataTemplate>Definiuje wygląd zawartości kontrolki. W przypadku a <xref:System.Windows.Controls.RadioButton> , zawartość jest wyświetlana na prawo od okręgu, który wskazuje, czy <xref:System.Windows.Controls.RadioButton> jest zaznaczone.  W przykładzie sygnalizatora ulicznego przycisk radiowy musi być kółkiem, który może "rozjaśnić". Ponieważ wymagania dotyczące wyglądu dla sygnalizatora ulicznego różnią się od domyślnego wyglądu <xref:System.Windows.Controls.RadioButton> , należy ponownie zdefiniować <xref:System.Windows.Controls.ControlTemplate> .  Ogólnie rzecz <xref:System.Windows.DataTemplate> , jest używany do definiowania zawartości (lub danych) kontrolki i <xref:System.Windows.Controls.ControlTemplate> jest używany do definiowania sposobu, w jaki formant jest strukturalny.

- **Wyzwalacze.** A <xref:System.Windows.Trigger> pozwala dynamicznie zmieniać wygląd i zachowanie kontrolki bez tworzenia nowej kontrolki. Załóżmy na przykład, że masz wiele <xref:System.Windows.Controls.ListBox> kontrolek w aplikacji i chcesz, aby elementy w każdym <xref:System.Windows.Controls.ListBox> z nich były pogrubione i czerwone po zaznaczeniu. Pierwszym instinctem może być utworzenie klasy, która dziedziczy po <xref:System.Windows.Controls.ListBox> i przesłania <xref:System.Windows.Controls.Primitives.Selector.OnSelectionChanged%2A> metodę w celu zmiany wyglądu wybranego elementu, ale lepszym rozwiązaniem jest dodanie wyzwalacza do stylu <xref:System.Windows.Controls.ListBoxItem> , który zmienia wygląd wybranego elementu. Wyzwalacz pozwala zmieniać wartości właściwości lub podejmować działania na podstawie wartości właściwości. <xref:System.Windows.EventTrigger>Umożliwia podejmowanie akcji w przypadku wystąpienia zdarzenia.

Aby uzyskać więcej informacji na temat stylów, szablonów i wyzwalaczy, zobacz [Style i tworzenia szablonów](../../../desktop-wpf/fundamentals/styles-templates-overview.md).

Ogólnie rzecz biorąc, jeśli formant odzwierciedla funkcjonalność istniejącej kontrolki, ale chcesz, aby formant wyglądał inaczej, należy najpierw rozważyć, czy można użyć dowolnej metody omówionej w tej sekcji, aby zmienić wygląd istniejącej kontrolki.

<a name="models_for_control_authoring"></a>

## <a name="models-for-control-authoring"></a>Modele dla tworzenia formantów

Bogaty model zawartości, style, szablony i wyzwalacze minimalizują potrzebę tworzenia nowej kontrolki. Jeśli jednak trzeba utworzyć nową kontrolkę, ważne jest, aby zrozumieć różne modele tworzenia formantów w programie [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] . [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]Program udostępnia trzy ogólne modele do tworzenia kontrolki, z których każdy zapewnia inny zestaw funkcji i poziom elastyczności. Klasy bazowe dla trzech modeli to <xref:System.Windows.Controls.UserControl> , <xref:System.Windows.Controls.Control> i <xref:System.Windows.FrameworkElement> .

### <a name="deriving-from-usercontrol"></a>Wyprowadzanie z obiektu UserControl

Najprostszym sposobem utworzenia kontrolki w programie [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] jest uzyskanie od <xref:System.Windows.Controls.UserControl> . Podczas tworzenia kontrolki, która dziedziczy z <xref:System.Windows.Controls.UserControl> , należy dodać istniejące składniki do <xref:System.Windows.Controls.UserControl> , nazwy składników i obsługi zdarzeń odniesienia w [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] . Następnie można odwoływać się do nazwanych elementów i zdefiniować programy obsługi zdarzeń w kodzie. Ten model programistyczny jest bardzo podobny do modelu używanego do tworzenia aplikacji w programie [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] .

W przypadku poprawnego działania programu można skorzystać z zalet <xref:System.Windows.Controls.UserControl> bogatej zawartości, stylów i wyzwalaczy. Jeśli jednak kontrolka dziedziczy od <xref:System.Windows.Controls.UserControl> , osoby, które korzystają z Twojego formantu, nie będą mogły użyć <xref:System.Windows.DataTemplate> ani <xref:System.Windows.Controls.ControlTemplate> dostosować wyglądu.  Konieczne jest wyjęcie z <xref:System.Windows.Controls.Control> klasy lub jednej z jej klas pochodnych (poza <xref:System.Windows.Controls.UserControl> ), aby utworzyć kontrolkę niestandardową, która obsługuje szablony.

#### <a name="benefits-of-deriving-from-usercontrol"></a>Zalety wyprowadzania z elementu UserControl

Należy rozważyć, <xref:System.Windows.Controls.UserControl> czy zostały spełnione wszystkie następujące warunki:

- Chcesz utworzyć kontrolkę podobnie jak w przypadku kompilowania aplikacji.

- Kontrolka składa się tylko z istniejących składników.

- Nie musisz obsługiwać złożonych dostosowań.

### <a name="deriving-from-control"></a>Wyprowadzanie z kontroli

Wyprowadzanie z <xref:System.Windows.Controls.Control> klasy jest modelem używanym przez większość istniejących [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] kontrolek. Podczas tworzenia kontrolki, która dziedziczy z <xref:System.Windows.Controls.Control> klasy, definiuje się jej wygląd przy użyciu szablonów. Dzięki temu można oddzielić logikę operacyjną od reprezentacji wizualnej. Można także zapewnić oddzielenie interfejsu użytkownika i logiki przy użyciu poleceń i powiązań zamiast zdarzeń i unikania elementów odwołujących się w <xref:System.Windows.Controls.ControlTemplate> przypadku, gdy jest to możliwe.  Jeśli interfejs użytkownika i logika kontrolki są prawidłowo oddzielone, użytkownik formantu może ponownie zdefiniować formant, <xref:System.Windows.Controls.ControlTemplate> Aby dostosować jego wygląd. Chociaż Kompilowanie niestandardowe <xref:System.Windows.Controls.Control> nie jest tak proste jak Kompilowanie <xref:System.Windows.Controls.UserControl> , niestandardowa <xref:System.Windows.Controls.Control> zapewnia największą elastyczność.

#### <a name="benefits-of-deriving-from-control"></a>Zalety wynikające z kontroli

Należy rozważyć wyprowadzanie z <xref:System.Windows.Controls.Control> zamiast używać <xref:System.Windows.Controls.UserControl> klasy, jeśli istnieją następujące zastosowania:

- Chcesz, aby wygląd kontrolki był dostosowywany za pośrednictwem <xref:System.Windows.Controls.ControlTemplate> .

- Chcesz, aby formant obsługiwał różne motywy.

### <a name="deriving-from-frameworkelement"></a>Wyprowadzanie z FrameworkElement

Kontrolki, które pochodzą z <xref:System.Windows.Controls.UserControl> lub <xref:System.Windows.Controls.Control> polegają na tworzeniu istniejących elementów. W przypadku wielu scenariuszy jest to akceptowalne rozwiązanie, ponieważ każdy obiekt, który dziedziczy z, <xref:System.Windows.FrameworkElement> może znajdować się w <xref:System.Windows.Controls.ControlTemplate> . Jednak istnieją sytuacje, w których wygląd kontrolki wymaga więcej niż funkcjonalności prostej składowej elementu. Dla tych scenariuszy bazowa <xref:System.Windows.FrameworkElement> wybór polega na tym, że składnik jest w tej chwili wybrany.

Istnieją dwie standardowe metody dla <xref:System.Windows.FrameworkElement> składników opartych na kompilowaniu: Render bezpośredni i kompozycja elementów niestandardowych. Renderowanie bezpośrednie polega na zastępowaniu <xref:System.Windows.UIElement.OnRender%2A> metody <xref:System.Windows.FrameworkElement> i udostępnianiu <xref:System.Windows.Media.DrawingContext> operacji, które jawnie definiują wizualizacje składnika. Jest to metoda używana przez <xref:System.Windows.Controls.Image> i <xref:System.Windows.Controls.Border> . Kompozycja elementu niestandardowego obejmuje użycie obiektów typu <xref:System.Windows.Media.Visual> w celu zredagowania wyglądu składnika. Aby zapoznać się z przykładem, zobacz [Używanie obiektów użycie DrawingVisual](../graphics-multimedia/using-drawingvisual-objects.md). <xref:System.Windows.Controls.Primitives.Track>to przykład kontrolki w programie [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] , która używa niestandardowego składu elementu. Istnieje również możliwość mieszania bezpośredniego renderowania i niestandardowego kompozycji elementów w tej samej kontrolce.

#### <a name="benefits-of-deriving-from-frameworkelement"></a>Korzyści wynikające z wytworzenia z elementu FrameworkElement

Należy rozważyć, <xref:System.Windows.FrameworkElement> czy istnieją następujące zastosowania:

- Chcesz mieć precyzyjną kontrolę nad wyglądem kontrolki poza tym, co jest obsługiwane przez prostą kompozycję elementów.

- Chcesz zdefiniować wygląd formantu przez zdefiniowanie własnej logiki renderowania.

- Chcesz tworzyć istniejące elementy w taki sposób, aby przekroczyć możliwości programu <xref:System.Windows.Controls.UserControl> i <xref:System.Windows.Controls.Control> .

<a name="control_authoring_basics"></a>

## <a name="control-authoring-basics"></a>Podstawowe informacje dotyczące tworzenia formantów

Jak wspomniano wcześniej, jedną z najbardziej zaawansowanych funkcji programu [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] jest możliwość przekroczenia ustawień podstawowych właściwości kontrolki, aby zmienić jej wygląd i zachowanie, a mimo to nie trzeba tworzyć kontrolki niestandardowej. Opcje stylów, powiązań danych i wyzwalacza są możliwe przez [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] system właściwości i [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] system zdarzeń. W poniższych sekcjach opisano niektóre praktyki, które należy wykonać, niezależnie od modelu używanego do tworzenia kontrolki niestandardowej, tak aby użytkownicy kontrolki niestandardowej mogli korzystać z tych funkcji w taki sam sposób jak w przypadku kontrolki dołączonej do programu [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] .

### <a name="use-dependency-properties"></a>Użyj właściwości zależności

Gdy właściwość jest właściwością zależności, można wykonać następujące czynności:

- Ustaw właściwość w stylu.

- Powiąż Właściwość ze źródłem danych.

- Użyj zasobu dynamicznego jako wartości właściwości.

- Animuj właściwość.

Jeśli chcesz, aby właściwość kontrolki obsługiwała jakąkolwiek z tych funkcji, należy zaimplementować ją jako właściwość zależności. W poniższym przykładzie zdefiniowano właściwość zależności o nazwie `Value` , wykonując następujące czynności:

- Zdefiniuj <xref:System.Windows.DependencyProperty> Identyfikator o nazwie `ValueProperty` jako `public` `static` `readonly` pole.

- Zarejestruj nazwę właściwości w systemie właściwości, wywołując metodę <xref:System.Windows.DependencyProperty.Register%2A?displayProperty=nameWithType> , aby określić następujące elementy:

  - Nazwa właściwości.

  - Typ właściwości.

  - Typ, który jest właścicielem właściwości.

  - Metadane właściwości. Metadane zawierają wartość domyślną właściwości, <xref:System.Windows.CoerceValueCallback> a i <xref:System.Windows.PropertyChangedCallback> .

- Zdefiniuj właściwość otoki CLR o nazwie `Value` , która jest taka sama jak nazwa, która jest używana do rejestrowania właściwości zależności, przez implementację właściwości `get` i `set` metod dostępu. Należy zauważyć, `get` że `set` metody dostępu i są tylko wywoływane <xref:System.Windows.DependencyObject.GetValue%2A> i <xref:System.Windows.DependencyObject.SetValue%2A> odpowiednio. Zaleca się, aby metody dostępu do właściwości zależności nie zawierały dodatkowej logiki, ponieważ klienci i [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] mogą ominąć metod dostępu i <xref:System.Windows.DependencyObject.GetValue%2A> <xref:System.Windows.DependencyObject.SetValue%2A> bezpośrednio. Na przykład gdy właściwość jest powiązana ze źródłem danych, `set` akcesor właściwości nie jest wywoływany.  Zamiast dodawać dodatkową logikę do metod dostępu get i Set, użyj <xref:System.Windows.ValidateValueCallback> <xref:System.Windows.CoerceValueCallback> delegatów, i, <xref:System.Windows.PropertyChangedCallback> Aby odpowiedzieć na lub sprawdź wartość podczas zmiany.  Aby uzyskać więcej informacji na temat tych wywołań zwrotnych, zobacz [wywołania zwrotne właściwości zależności i walidacja](../advanced/dependency-property-callbacks-and-validation.md).

- Zdefiniuj metodę dla <xref:System.Windows.CoerceValueCallback> nazwy `CoerceValue` . `CoerceValue`zapewnia, że `Value` jest większa lub równa `MinValue` i mniejsza lub równa `MaxValue` .

- Zdefiniuj metodę dla elementu <xref:System.Windows.PropertyChangedCallback> o nazwie `OnValueChanged` . `OnValueChanged`tworzy <xref:System.Windows.RoutedPropertyChangedEventArgs%601> obiekt i przygotowuje się do podniesienia poziomu `ValueChanged` zdarzenia kierowanego. Zdarzenia kierowane zostały omówione w następnej sekcji.

[!code-csharp[UserControlNumericUpDown#DependencyProperty](~/samples/snippets/csharp/VS_Snippets_Wpf/UserControlNumericUpDown/CSharp/NumericUpDown.xaml.cs#dependencyproperty)]
[!code-vb[UserControlNumericUpDown#DependencyProperty](~/samples/snippets/visualbasic/VS_Snippets_Wpf/UserControlNumericUpDown/visualbasic/numericupdown.xaml.vb#dependencyproperty)]

Aby uzyskać więcej informacji, zobacz [niestandardowe właściwości zależności](../advanced/custom-dependency-properties.md).

### <a name="use-routed-events"></a>Korzystanie z zdarzeń kierowanych

Podobnie jak właściwości zależności zwiększają koncepcję właściwości CLR z dodatkową funkcjonalnością, zdarzenia kierowane zwiększają koncepcję standardowych zdarzeń CLR. Podczas tworzenia nowej [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] kontrolki dobrym sposobem jest zaimplementowanie zdarzenia jako zdarzenia kierowanego, ponieważ routowane zdarzenie obsługuje następujące zachowanie:

- Zdarzenia mogą być obsługiwane na obiekcie nadrzędnym wielu kontrolek. Jeśli zdarzenie jest zdarzeniem propagacji, jeden element nadrzędny w drzewie elementu może subskrybować zdarzenie. Następnie autorzy aplikacji mogą używać jednego programu obsługi, aby odpowiedzieć na zdarzenie wielu kontrolek. Na przykład, Jeśli kontrolka jest częścią każdego elementu w <xref:System.Windows.Controls.ListBox> (ponieważ jest zawarta w <xref:System.Windows.DataTemplate> ), Deweloper aplikacji może zdefiniować program obsługi zdarzeń dla zdarzenia kontrolki na <xref:System.Windows.Controls.ListBox> . Za każdym razem, gdy wystąpi zdarzenie na dowolnym z formantów, wywoływana jest procedura obsługi zdarzeń.

- Zdarzenia trasowane mogą być używane w programie <xref:System.Windows.EventSetter> , co umożliwia deweloperom aplikacji określenie obsługi zdarzenia w ramach stylu.

- Zdarzenia trasowane mogą być używane w <xref:System.Windows.EventTrigger> , co jest przydatne w przypadku animowania właściwości przy użyciu [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] . Aby uzyskać więcej informacji, zobacz [Omówienie animacji](../graphics-multimedia/animation-overview.md).

W poniższym przykładzie zdefiniowano zdarzenie trasowane, wykonując następujące czynności:

- Zdefiniuj <xref:System.Windows.RoutedEvent> Identyfikator o nazwie `ValueChangedEvent` jako `public` `static` `readonly` pole.

- Zarejestruj zdarzenie trasowane przez wywołanie <xref:System.Windows.EventManager.RegisterRoutedEvent%2A?displayProperty=nameWithType> metody. W przykładzie określono następujące informacje podczas wywoływania <xref:System.Windows.EventManager.RegisterRoutedEvent%2A> :

  - Nazwa zdarzenia to `ValueChanged` .

  - Strategia routingu to <xref:System.Windows.RoutingStrategy.Bubble> , co oznacza, że program obsługi zdarzeń na źródle (obiekt, który wywołuje zdarzenie) jest wywoływany jako pierwszy, a następnie procedury obsługi zdarzeń w elementach nadrzędnych źródła są wywoływane po powodzeniu, rozpoczynając od programu obsługi zdarzeń na najbliższym elemencie nadrzędnym.

  - Typ procedury obsługi zdarzeń jest <xref:System.Windows.RoutedPropertyChangedEventHandler%601> zbudowany z <xref:System.Decimal> typem.

  - Typem właściciela zdarzenia jest `NumericUpDown` .

- Zadeklaruj zdarzenie publiczne o nazwie `ValueChanged` i zawiera deklaracje metody dostępu zdarzenia. Przykład wywołuje <xref:System.Windows.UIElement.AddHandler%2A> w `add` deklaracji akcesora i <xref:System.Windows.UIElement.RemoveHandler%2A> w `remove` deklaracji metody dostępu do korzystania z [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] usług zdarzeń.

- Utwórz chronioną metodę wirtualną o nazwie `OnValueChanged` , która wywołuje `ValueChanged` zdarzenie.

[!code-csharp[UserControlNumericUpDown#RoutedEvent](~/samples/snippets/csharp/VS_Snippets_Wpf/UserControlNumericUpDown/CSharp/NumericUpDown.xaml.cs#routedevent)]
[!code-vb[UserControlNumericUpDown#RoutedEvent](~/samples/snippets/visualbasic/VS_Snippets_Wpf/UserControlNumericUpDown/visualbasic/numericupdown.xaml.vb#routedevent)]

Aby uzyskać więcej informacji, zobacz [Omówienie zdarzeń kierowanych](../advanced/routed-events-overview.md) i [Tworzenie niestandardowego zdarzenia kierowanego](../advanced/how-to-create-a-custom-routed-event.md).

### <a name="use-binding"></a>Użyj powiązania

Aby oddzielić interfejs użytkownika formantu od jego logiki, należy rozważyć użycie powiązania danych. Jest to szczególnie ważne w przypadku definiowania wyglądu kontrolki przy użyciu <xref:System.Windows.Controls.ControlTemplate> . W przypadku używania powiązania danych można wyeliminować konieczność odwoływania się do określonych części interfejsu użytkownika z kodu. Dobrym pomysłem jest uniknięcie odwoływania się do elementów, które znajdują się w, <xref:System.Windows.Controls.ControlTemplate> ponieważ gdy kod odwołuje się do elementów, które znajdują się w <xref:System.Windows.Controls.ControlTemplate> i <xref:System.Windows.Controls.ControlTemplate> zostaje zmieniony, element, do którego się odwoływano, musi być uwzględniony w nowym <xref:System.Windows.Controls.ControlTemplate> .

Poniższy przykład aktualizuje <xref:System.Windows.Controls.TextBlock> `NumericUpDown` kontrolkę, przypisując do niej nazwę i odwołujący się do pola tekstowego według nazwy w kodzie.

[!code-xaml[UserControlNumericUpDownSimple#UIRefMarkup](~/samples/snippets/csharp/VS_Snippets_Wpf/UserControlNumericUpDownSimple/CSharp/NumericUpDown.xaml#uirefmarkup)]

[!code-csharp[UserControlNumericUpDownSimple#UIRefCode](~/samples/snippets/csharp/VS_Snippets_Wpf/UserControlNumericUpDownSimple/CSharp/NumericUpDown.xaml.cs#uirefcode)]
[!code-vb[UserControlNumericUpDownSimple#UIRefCode](~/samples/snippets/visualbasic/VS_Snippets_Wpf/UserControlNumericUpDownSimple/VisualBasic/NumericUpDown.xaml.vb#uirefcode)]

Poniższy przykład używa powiązania, aby wykonać to samo.

[!code-xaml[UserControlNumericUpDown#Binding](~/samples/snippets/csharp/VS_Snippets_Wpf/UserControlNumericUpDown/CSharp/NumericUpDown.xaml#binding)]

Aby uzyskać więcej informacji na temat powiązania danych, zobacz temat [powiązanie danych — omówienie](../../../desktop-wpf/data/data-binding-overview.md).

### <a name="design-for-designers"></a>Projektowanie dla projektantów

Aby uzyskać pomoc techniczną dla formantów WPF w programie WPF Designer dla programu Visual Studio (na przykład edytowania właściwości z okno Właściwości), postępuj zgodnie z poniższymi wskazówkami.  Aby uzyskać więcej informacji na temat programowania dla projektanta WPF, zobacz [Design XAML w programie Visual Studio](/visualstudio/xaml-tools/designing-xaml-in-visual-studio).

#### <a name="dependency-properties"></a>Właściwości zależności

Upewnij się, że wdrożono środowisko CLR i metody dostępu zgodnie z `get` `set` wcześniejszym opisem w artykule "Używanie właściwości zależności". Projektanci mogą używać otoki do wykrywania obecności właściwości zależności, ale tak jak [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] i klientów kontrolki, nie muszą wywoływać metod dostępu podczas pobierania lub ustawiania właściwości.

#### <a name="attached-properties"></a>Dołączone właściwości

Załączone właściwości należy zaimplementować w niestandardowych kontrolkach, korzystając z następujących wskazówek:

- Ma `public` `static` `readonly` <xref:System.Windows.DependencyProperty> metodę *PropertyName* , `Property` która została utworzona przy użyciu <xref:System.Windows.DependencyProperty.RegisterAttached%2A> metody. Nazwa właściwości, która jest przesyłana do <xref:System.Windows.DependencyProperty.RegisterAttached%2A> musi być zgodna z parametrem *PropertyName*.

- Zaimplementuj parę `public` `static` metod CLR o nazwie `Set` *PropertyName* i `Get` *PropertyName*. Obie metody powinny akceptować klasę pochodną <xref:System.Windows.DependencyProperty> jako pierwszy argument. Metoda `Set` *PropertyName* akceptuje również argument, którego typ jest zgodny z typem danych zarejestrowanych dla właściwości. Metoda `Get` *PropertyName* powinna zwracać wartość tego samego typu. Jeśli `Set` brakuje metody *PropertyName* , właściwość jest oznaczona jako tylko do odczytu.

- `Set`Funkcja *PropertyName* i `Get` *PropertyName* musi bezpośrednio kierować do <xref:System.Windows.DependencyObject.GetValue%2A> <xref:System.Windows.DependencyObject.SetValue%2A> metod i w docelowym obiekcie zależności. Projektanci mogą uzyskać dostęp do dołączonej właściwości, wywołując przez otokę metody lub wykonując bezpośrednie wywołanie do docelowego obiektu zależności.

Aby uzyskać więcej informacji o dołączanych właściwościach, zobacz temat [dołączone właściwości przegląd](../advanced/attached-properties-overview.md).

### <a name="define-and-use-shared-resources"></a>Definiowanie i używanie zasobów udostępnionych

Możesz dołączyć swój formant w tym samym zestawie, w którym znajduje się aplikacja, lub spakować formant w osobnym zestawie, który może być używany w wielu aplikacjach. W większości przypadków informacje omówione w tym temacie dotyczą niezależnie od używanej metody.  Należy jednak pamiętać o jednej różnicy.  Po umieszczeniu formantu w tym samym zestawie, w którym znajduje się aplikacja, możesz dodać zasoby globalne do pliku App. XAML. Ale zestaw, który zawiera tylko kontrolki, nie ma <xref:System.Windows.Application> skojarzonego z nim obiektu, więc plik App. XAML nie jest dostępny.

Gdy aplikacja szuka zasobu, sprawdza trzy poziomy w następującej kolejności:

1. Poziom elementu.

   System rozpoczyna się od elementu, który odwołuje się do zasobu, a następnie przeszukuje zasoby logicznego elementu nadrzędnego i tak dalej, aż do osiągnięcia elementu głównego.

2. Poziom aplikacji.

   Zasoby zdefiniowane przez <xref:System.Windows.Application> obiekt.

3. Poziom motywu.

   Słowniki na poziomie motywu są przechowywane w podfolderze o nazwie motywy.  Pliki w folderze motywy odpowiadają kompozycjom.  Na przykład możesz mieć interfejs Aero. NormalColor. XAML, Luna. NormalColor. XAML, Royale. NormalColor. XAML i tak dalej.  Można również mieć plik o nazwie Generic. XAML.  Gdy system wyszukuje zasób na poziomie motywów, najpierw szuka go w pliku specyficznym dla motywu, a następnie szuka go w ogólnym języku XAML.

Gdy formant znajduje się w zestawie, który jest oddzielony od aplikacji, należy umieścić zasoby globalne na poziomie elementu lub na poziomie motywu. Obie metody mają swoje zalety.

#### <a name="defining-resources-at-the-element-level"></a>Definiowanie zasobów na poziomie elementu

Zasoby udostępnione można definiować na poziomie elementu przez utworzenie niestandardowego słownika zasobów i scalenie go ze słownikiem zasobów formantu.  Korzystając z tej metody, można nazwać dowolny plik zasobów i może znajdować się w tym samym folderze co kontrolki. Zasoby na poziomie elementu mogą również używać prostych ciągów jako kluczy. Poniższy przykład tworzy <xref:System.Windows.Media.LinearGradientBrush> plik zasobów o nazwie Dictionary1. XAML.

[!code-xaml[SharedResources#1](~/samples/snippets/csharp/VS_Snippets_Wpf/SharedResources/CS/Dictionary1.xaml#1)]

Po zdefiniowaniu słownika należy go scalić z słownikiem zasobów formantu.  Można to zrobić za pomocą programu [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] lub kodu.

Poniższy przykład Scala słownik zasobów przy użyciu programu [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] .

[!code-xaml[SharedResources#2](~/samples/snippets/csharp/VS_Snippets_Wpf/SharedResources/CS/ShapeResizer.xaml#2)]

Wadą tego podejścia jest to, że <xref:System.Windows.ResourceDictionary> obiekt jest tworzony przy każdym odwoływaniu się do niego.  Na przykład jeśli masz 10 niestandardowych kontrolek w bibliotece i Scal udostępnione słowniki zasobów dla każdej kontrolki przy użyciu języka XAML, tworzysz 10 identycznych <xref:System.Windows.ResourceDictionary> obiektów.  Można tego uniknąć, tworząc klasę statyczną, która scala zasoby w kodzie i zwraca wynik <xref:System.Windows.ResourceDictionary> .

Poniższy przykład tworzy klasę, która zwraca współużytkowany <xref:System.Windows.ResourceDictionary> .

[!code-csharp[SharedResources#3](~/samples/snippets/csharp/VS_Snippets_Wpf/SharedResources/CS/SharedDictionaryManager.cs#3)]

Poniższy przykład Scala zasób udostępniony z zasobami kontrolki niestandardowej w konstruktorze formantu przed wywołaniem `InitializeComponent` .  Ponieważ `SharedDictionaryManager.SharedDictionary` jest to właściwość statyczna, <xref:System.Windows.ResourceDictionary> jest tworzona tylko raz. Ze względu na to, że słownik zasobów został wcześniej scalony `InitializeComponent` , zasoby są dostępne dla formantu w jego [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] pliku.

[!code-csharp[SharedResources#4](~/samples/snippets/csharp/VS_Snippets_Wpf/SharedResources/CS/ShapeResizer.xaml.cs#4)]

#### <a name="defining-resources-at-the-theme-level"></a>Definiowanie zasobów na poziomie motywu

[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]umożliwia tworzenie zasobów dla różnych motywów systemu Windows.  Jako autor kontrolki możesz zdefiniować zasób dla określonego motywu, aby zmienić wygląd formantu w zależności od tego, jaki motyw jest używany. Na przykład wygląd elementu <xref:System.Windows.Controls.Button> w klasycznym motywie systemu Windows (motyw domyślny dla systemu windows 2000) różni się od programu <xref:System.Windows.Controls.Button> w motywie Luna systemu Windows (motyw domyślny dla systemu Windows XP), ponieważ <xref:System.Windows.Controls.Button> używa innego <xref:System.Windows.Controls.ControlTemplate> dla każdego motywu.

Zasoby specyficzne dla motywu są przechowywane w słowniku zasobów z określoną nazwą pliku. Te pliki muszą znajdować się w folderze o nazwie `Themes` , który jest podfolderem folderu, który zawiera kontrolkę. W poniższej tabeli wymieniono pliki słownika zasobów i motyw, które są skojarzone z każdym plikiem:

|Nazwa pliku słownika zasobów|Motyw systemu Windows|
|-----------------------------------|-------------------|
|`Classic.xaml`|Klasyczne systemy Windows 9X/2000 Szukaj w systemie Windows XP|
|`Luna.NormalColor.xaml`|Domyślny niebieski motyw w systemie Windows XP|
|`Luna.Homestead.xaml`|Motyw oliwy w systemie Windows XP|
|`Luna.Metallic.xaml`|Motyw Silver w systemie Windows XP|
|`Royale.NormalColor.xaml`|Motyw domyślny w systemie Windows XP Media Center Edition|
|`Aero.NormalColor.xaml`|Motyw domyślny w systemie Windows Vista|

Nie trzeba definiować zasobów dla każdego motywu. Jeśli zasób nie jest zdefiniowany dla określonego motywu, formant sprawdza `Classic.xaml` dla zasobu. Jeśli zasób nie jest zdefiniowany w pliku, który odnosi się do bieżącego motywu lub w programie `Classic.xaml` , formant używa zasobu generycznego, który znajduje się w pliku słownika zasobów o nazwie `generic.xaml` .  Plik znajduje się `generic.xaml` w tym samym folderze co pliki słowników zasobów specyficznych dla motywu. Chociaż nie `generic.xaml` odpowiada określonemu motywowi systemu Windows, nadal jest słownikiem poziomu motywu.

Kontrolka niestandardowa [C#](https://github.com/dotnet/docs/tree/master/samples/snippets/csharp/VS_Snippets_Wpf/CustomControlNumericUpDown/CSharp) lub [Visual Basic](https://github.com/dotnet/docs/tree/master/samples/snippets/visualbasic/VS_Snippets_Wpf/CustomControlNumericUpDown/visualbasic) NumericUpDown z motywem i obsługą automatyzacji interfejsu użytkownika zawiera dwa słowniki zasobów dla `NumericUpDown` kontrolki: jeden jest w pliku Generic. XAML, a drugi to w Luna. NormalColor. XAML.

Po umieszczeniu <xref:System.Windows.Controls.ControlTemplate> w dowolnym pliku słownika zasobów specyficznych dla motywu należy utworzyć statyczny Konstruktor dla kontrolki i wywołać <xref:System.Windows.DependencyProperty.OverrideMetadata%28System.Type%2CSystem.Windows.PropertyMetadata%29> metodę na <xref:System.Windows.FrameworkElement.DefaultStyleKey%2A> , jak pokazano w poniższym przykładzie.

[!code-csharp[CustomControlNumericUpDownOneProject#StaticConstructor](~/samples/snippets/csharp/VS_Snippets_Wpf/CustomControlNumericUpDownOneProject/CSharp/NumericUpDown.cs#staticconstructor)]
[!code-vb[CustomControlNumericUpDownOneProject#StaticConstructor](~/samples/snippets/visualbasic/VS_Snippets_Wpf/CustomControlNumericUpDownOneProject/visualbasic/numericupdown.vb#staticconstructor)]

##### <a name="defining-and-referencing-keys-for-theme-resources"></a>Definiowanie i odwoływanie się do kluczy dla zasobów motywu

Podczas definiowania zasobu na poziomie elementu można przypisać ciąg jako klucz i uzyskać dostęp do zasobu za pośrednictwem ciągu. Podczas definiowania zasobu na poziomie motywu należy użyć <xref:System.Windows.ComponentResourceKey> jako klucza.  W poniższym przykładzie zdefiniowano zasób w pliku Generic. XAML.

[!code-xaml[ThemeResourcesControlLibrary#5](~/samples/snippets/csharp/VS_Snippets_Wpf/ThemeResourcesControlLibrary/CS/Themes/generic.xaml#5)]

Poniższy przykład odwołuje się do zasobu przez określenie <xref:System.Windows.ComponentResourceKey> jako klucza.

[!code-xaml[ThemeResourcesControlLibrary#6](~/samples/snippets/csharp/VS_Snippets_Wpf/ThemeResourcesControlLibrary/CS/NumericUpDown.xaml#6)]

##### <a name="specifying-the-location-of-theme-resources"></a>Określanie lokalizacji zasobów motywu

Aby znaleźć zasoby dla kontrolki, aplikacja hostingu musi wiedzieć, że zestaw zawiera zasoby dotyczące kontroli. Można to zrobić, dodając <xref:System.Windows.ThemeInfoAttribute> do zestawu, który zawiera kontrolkę. <xref:System.Windows.ThemeInfoAttribute>Zawiera <xref:System.Windows.ThemeInfoAttribute.GenericDictionaryLocation%2A> Właściwość, która określa lokalizację zasobów ogólnych, oraz <xref:System.Windows.ThemeInfoAttribute.ThemeDictionaryLocation%2A> Właściwość, która określa lokalizację zasobów specyficznych dla motywu.

Poniższy przykład ustawia <xref:System.Windows.ThemeInfoAttribute.GenericDictionaryLocation%2A> <xref:System.Windows.ThemeInfoAttribute.ThemeDictionaryLocation%2A> właściwości i na <xref:System.Windows.ResourceDictionaryLocation.SourceAssembly> , aby określić, że ogólne i charakterystyczne dla motywu zasoby znajdują się w tym samym zestawie co formant.

[!code-csharp[CustomControlNumericUpDown#ThemesSection](~/samples/snippets/csharp/VS_Snippets_Wpf/CustomControlNumericUpDown/CSharp/CustomControlLibrary/Properties/AssemblyInfo.cs#themessection)]
[!code-vb[CustomControlNumericUpDown#ThemesSection](~/samples/snippets/visualbasic/VS_Snippets_Wpf/CustomControlNumericUpDown/visualbasic/customcontrollibrary/my project/assemblyinfo.vb#themessection)]

## <a name="see-also"></a>Zobacz także

- [Projektowanie XAML w programie Visual Studio](/visualstudio/xaml-tools/designing-xaml-in-visual-studio)
- [Pakuj URI w WPF](../app-development/pack-uris-in-wpf.md)
- [Niestandardowe dostosowywanie formantu](control-customization.md)
