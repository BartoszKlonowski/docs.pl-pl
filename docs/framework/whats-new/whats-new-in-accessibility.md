---
title: Co nowego w ułatwieniach dostępu w .NET Framework
description: Zobacz, co nowego w programie .NET Accessibility, począwszy od .NET Framework 4.7.1. Funkcje ułatwień dostępu pozwalają aplikacji zapewnić odpowiednie środowisko dla użytkowników technologii pomocniczej.
ms.date: 04/18/2019
dev_langs:
- csharp
- vb
helpviewer_keywords:
- what's new [.NET Framework]
ms.openlocfilehash: df9188c4f7c2af77f5dc87309880a41724254c5c
ms.sourcegitcommit: 8bfeb5930ca48b2ee6053f16082dcaf24d46d221
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2020
ms.locfileid: "88558962"
---
# <a name="whats-new-in-accessibility-in-the-net-framework"></a>Co nowego w ułatwieniach dostępu w .NET Framework

.NET Framework ma na celu zwiększenie dostępności aplikacji dla użytkowników. Funkcje ułatwień dostępu umożliwiają aplikacji zapewnienie odpowiedniego środowiska dla użytkowników technologii pomocniczej. Począwszy od .NET Framework 4.7.1, .NET Framework obejmuje dużą liczbę ulepszeń ułatwień dostępu, które umożliwiają deweloperom tworzenie dostępnych aplikacji.

## <a name="accessibility-switches"></a>Przełączniki ułatwień dostępu

Można skonfigurować aplikację do korzystania z funkcji ułatwień dostępu, jeśli jest ona przeznaczona dla .NET Framework 4,7 lub wcześniejszej wersji, ale działa w systemie .NET Framework 4.7.1 lub nowszym. Możesz również skonfigurować aplikację tak, aby korzystała ze starszych funkcji (i nie korzystać z funkcji ułatwień dostępu), jeśli jest ona przeznaczona dla .NET Framework 4.7.1 lub nowszych. Każda wersja .NET Framework, która obejmuje funkcje ułatwień dostępu, ma przełącznik dostępności specyficzny dla wersji, który można dodać do [`<AppContextSwitchOverrides>`](../configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md) elementu w [`<runtime>`](../configure-apps/file-schema/runtime/index.md) sekcji pliku konfiguracyjnego aplikacji. Obsługiwane są następujące przełączniki:

|Wersja|Przełącznik|
|---|---|
|.NET Framework 4.7.1|"Switch. UseLegacyAccessibilityFeatures"|
| .NET Framework 4.7.2|"Switch. UseLegacyAccessibilityFeatures. 2"|
| .NET Framework 4.8|"Switch. UseLegacyAccessibilityFeatures. 3"|

### <a name="taking-advantage-of-accessibility-enhancements"></a>Korzystanie z ulepszeń ułatwień dostępu

Nowe funkcje ułatwień dostępu są domyślnie włączone dla aplikacji przeznaczonych .NET Framework 4.7.1 lub nowszych. Ponadto aplikacje przeznaczone dla starszej wersji .NET Framework ale działają na .NET Framework 4.7.1 lub nowszych mogą zrezygnować ze starszych zachowań dostępności (a tym samym korzystać z ulepszeń ułatwień dostępu) przez dodanie przełączników do [`<AppContextSwitchOverrides>`](../configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md) elementu w [`<runtime>`](../configure-apps/file-schema/runtime/index.md) sekcji pliku konfiguracji aplikacji i ustawienie ich wartości na `false` . Poniżej pokazano, jak wybrać ulepszenia ułatwień dostępu wprowadzone w .NET Framework 4.7.1:

```xml
<runtime>
    <!-- AppContextSwitchOverrides value attribute is in the form of 'key1=true|false;key2=true|false  -->
    <AppContextSwitchOverrides value="Switch.UseLegacyAccessibilityFeatures=false" />
</runtime>
```

W przypadku wybrania opcji ułatwienia dostępu w nowszej wersji .NET Framework należy również jawnie zadecydować o funkcjach wcześniejszych wersji .NET Framework. Skonfigurowanie aplikacji w taki sposób, aby korzystała z ulepszeń ułatwień dostępu zarówno w .NET Framework 4.7.1, jak i 4.7.2 wymaga następującego [`<AppContextSwitchOverrides>`](../configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md) elementu:

```xml
<runtime>
    <!-- AppContextSwitchOverrides value attribute is in the form of 'key1=true|false;key2=true|false  -->
    <AppContextSwitchOverrides value="Switch.UseLegacyAccessibilityFeatures=false;Switch.UseLegacyAccessibilityFeatures.2=false" />
</runtime>
```

Konfigurowanie aplikacji w celu skorzystania z ulepszeń ułatwień dostępu w .NET Framework 4.7.1, 4.7.2 i 4,8 wymaga następującego [`<AppContextSwitchOverrides>`](../configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md) elementu:

```xml
<runtime>
    <!-- AppContextSwitchOverrides value attribute is in the form of 'key1=true|false;key2=true|false  -->
    <AppContextSwitchOverrides value="Switch.UseLegacyAccessibilityFeatures=false;Switch.UseLegacyAccessibilityFeatures.2=false;Switch.UseLegacyAccessibilityFeatures.3=false" />
</runtime>
```

### <a name="restoring-legacy-behavior"></a>Przywracanie starszego zachowania

Aplikacje, które są przeznaczone dla wersji .NET Framework zaczynających się od 4.7.1, mogą wyłączyć funkcje ułatwień dostępu, dodając przełączniki do [`<AppContextSwitchOverrides>`](../configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md) elementu w [`<runtime>`](../configure-apps/file-schema/runtime/index.md) sekcji pliku konfiguracyjnego aplikacji i ustawiając ich wartość na `true` . Na przykład następujące czynności konfiguracyjne nie są związane z funkcjami ułatwień dostępu wprowadzonymi w .NET Framework 4.7.2:

```xml
<runtime>
    <!-- AppContextSwitchOverrides value attribute is in the form of 'key1=true|false;key2=true|false  -->
    <AppContextSwitchOverrides value="Switch.UseLegacyAccessibilityFeatures.2=true" />
</runtime>
```

## <a name="whats-new-in-accessibility-in-net-framework-48"></a>Nowości w ułatwieniach dostępu w .NET Framework 4,8

.NET Framework 4,8 zawiera nowe funkcje ułatwień dostępu w następujących obszarach:

- [Windows Forms](#winforms48)

- [Windows Presentation Foundation (WPF)](#wpf48)

- [Projektant przepływu pracy Windows Workflow Foundation (WF)](#wf48)

<a name="winforms48"></a>

### <a name="windows-forms"></a>Windows Forms

W .NET Framework 4,8 Windows Forms dodaje obsługę LiveRegions i zdarzeń powiadomień do wielu często używanych kontrolek. Dodaje również obsługę etykietek narzędzi, gdy użytkownik przechodzi do formantu przy użyciu klawiatury.

**UIA LiveRegions support w etykietach i StatusStrip**

UIA LiveRegions umożliwiają deweloperom aplikacji powiadamianie czytników ekranu o zmianie tekstu w kontrolce, która znajduje się poza lokalizacją, w której pracuje użytkownik. Jest to przydatne na przykład w przypadku <xref:System.Windows.Forms.StatusStrip> kontrolki wyświetlającej stan połączenia. Jeśli połączenie zostanie przerwane i stan zmieni się, deweloper może chcieć powiadomić czytnik ekranu.

Począwszy od .NET Framework 4,8, Windows Forms implementuje UIA LiveRegions dla <xref:System.Windows.Forms.Label> <xref:System.Windows.Forms.StatusStrip> formantów i. Na przykład poniższy kod używa LiveRegion w <xref:System.Windows.Forms.Label> kontrolce o nazwie `label1` :

```csharp
public Form1()
{
   InitializeComponent();
   label1.AutomationLiveSetting = AutomationLiveSetting.Polite;
}

…
Label1.Text = “Ready!”;
```

Narrator ogłasza "gotowe" niezależnie od tego, gdzie użytkownik jest w stanie korzystać z aplikacji.

Możesz również zaimplementować swój <xref:System.Windows.Forms.UserControl> element jako LiveRegion:

```csharp
using System;
using System.Windows.Forms;
using System.Windows.Forms.Automation;

namespace WindowsFormsApplication
{
   public partial class UserControl1 : UserControl, IAutomationLiveRegion
   {
      public UserControl1()
      {
         InitializeComponent();
      }

      public AutomationLiveSetting AutomationLiveSetting { get; set; }
      private AutomationLiveSetting IAutomationLiveRegion.GetLiveSetting()
      {
         return this.AutomationLiveSetting;
      }

      protected override void OnTextChanged(EventArgs e)
      {
         base.OnTextChanged(e);
         AutomationNotifications.UiaRaiseLiveRegionChangedEvent(this.AccessibilityObject);
      }
   }
}
```

**UIA zdarzenia powiadomień**

Zdarzenie powiadamiania UIA wprowadzone w ramach aktualizacji systemu Windows 10 z aktualizacją dla twórców pozwala aplikacji na zgłaszanie zdarzenia UIA, które prowadzi do Narratora w oparciu o tekst dostarczany wraz ze zdarzeniem, bez konieczności posiadania odpowiedniej kontrolki w interfejsie użytkownika. W niektórych scenariuszach jest to prosty sposób znacznie zwiększyć dostępność aplikacji. W programie może być również przydatne powiadamianie o postępie niektórych procesów, które mogą zająć dużo czasu. Aby uzyskać więcej informacji na temat zdarzeń powiadomień UIA, zobacz [czy aplikacja klasyczna korzysta z nowego zdarzenia powiadamiania o interfejsie użytkownika?](https://docs.microsoft.com/archive/blogs/winuiautomation/can-your-desktop-app-leverage-the-new-uia-notification-event-in-order-to-have-narrator-say-exactly-what-your-customers-need).

Poniższy przykład podnosi [zdarzenie powiadomienia](xref:System.Windows.Forms.AccessibleObject.RaiseAutomationNotification%2A):

```csharp
MethodInfo raiseMethod = typeof(AccessibleObject).GetMethod("RaiseAutomationNotification");
if (raiseMethod != null) {
   raiseMethod.Invoke(progressBar1.AccessibilityObject, new object[3] {/*Other*/ 4, /*All*/ 2, "The progress is 50%." });
}
```

**Etykietki narzędzi na dostępie z klawiatury**

W aplikacjach, które są przeznaczone .NET Framework 4.7.2 i starszych wersji, [etykietka narzędzia](xref:System.Windows.Forms.ToolTip) kontrolki może być wyzwalana tylko w celu przechodzenia do kontrolki. Począwszy od .NET Framework 4,8, użytkownik klawiatury może wyzwolić etykietkę narzędzia kontrolki za pomocą klawisza TAB lub klawiszy strzałek z klawiszami modyfikującymi lub bez. To konkretne ulepszenie ułatwień dostępu wymaga dodatkowego [przełącznika AppContext](../configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md):

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
   <startup>
      <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.6.1"/>
   </startup>
   <runtime>
      <!-- AppContextSwitchOverrides values are in the form of 'key1=true|false;key2=true|false  -->
      <!-- Please note that disabling Switch.UseLegacyAccessibilityFeatures, Switch.UseLegacyAccessibilityFeatures.2 and Switch.UseLegacyAccessibilityFeatures.3 is required to disable Switch.System.Windows.Forms.UseLegacyToolTipDisplay -->
      <AppContextSwitchOverrides value="Switch.UseLegacyAccessibilityFeatures=false;Switch.UseLegacyAccessibilityFeatures.2=false;Switch.UseLegacyAccessibilityFeatures.3=false;Switch.System.Windows.Forms.UseLegacyToolTipDisplay=false"/>
   </runtime>
</configuration>
```

Na poniższej ilustracji przedstawiono etykietkę narzędzia, gdy użytkownik wybierze przycisk z klawiaturą.

![Zrzut ekranu przedstawiający etykietkę narzędzia, gdy użytkownik nawiguje do przycisku przy użyciu klawiatury.](./media/whats-new-in-accessibility/select-tooltip-with-keyboard.png)

<a name="wpf48"></a>

### <a name="windows-presentation-foundation-wpf"></a>Windows Presentation Foundation (WPF)

Począwszy od .NET Framework 4,8, WPF obejmuje wiele ulepszeń ułatwień dostępu.

**Narratory ekranu nie ogłaszają już elementów z zwiniętym lub ukrytym widocznością**

Elementy z zwiniętym lub ukrytym widocznością nie są już anonsowane przez czytnik ekranu. Interfejsy użytkownika, które zawierają elementy z widocznością <xref:System.Windows.Visibility.Collapsed?displayProperty=nameWithType> lub <xref:System.Windows.Visibility.Hidden?displayProperty=nameWithType> mogą być reprezentowane przez czytniki ekranu, jeśli są ogłoszone dla użytkownika. Począwszy od .NET Framework 4,8, WPF nie obejmuje już elementów zwiniętych lub ukrytych w widoku sterowania drzewa UIAutomation, dzięki czemu czytniki zawartości ekranu nie będą już ogłaszać tych elementów.

**Właściwość SelectionTextBrush do użycia z zaznaczonym tekstem innym niż moduł definiowania układu**

W .NET Framework 4.7.2, WPF dodaliśmy możliwość rysowania <xref:System.Windows.Controls.TextBox> i <xref:System.Windows.Controls.PasswordBox> wybierania tekstu bez użycia warstwy modułu definiowania układu. Kolor pierwszego planu zaznaczonego tekstu w tym scenariuszu został podyktowany przez <xref:System.Windows.SystemColors.HighlightTextBrush?displayProperty=nameWithType> .

.NET Framework 4,8 dodaje nową właściwość, `SelectionTextBrush` która umożliwia deweloperom wybranie określonego pędzla dla zaznaczonego tekstu przy użyciu zaznaczonego tekstu. Ta właściwość działa tylko w <xref:System.Windows.Controls.Primitives.TextBoxBase> kontrolkach pochodnych i <xref:System.Windows.Controls.PasswordBox> formant w aplikacjach WPF z włączonym zaznaczeniem tekstu innym niż moduł definiowania układu. Nie działa on na <xref:System.Windows.Controls.RichTextBox> formancie. Jeśli wybór tekstu nie jest włączony, ta właściwość jest ignorowana.

Aby użyć tej właściwości, wystarczy dodać ją do kodu XAML i użyć odpowiedniego pędzla lub powiązania. Wynikowy wybór tekstu wygląda następująco:

![Zrzut ekranu aplikacji uruchomionej z wyrazami, Hello world zaznaczone.](./media/whats-new-in-accessibility/selectiontextbrush-property.png)

Można połączyć użycie `SelectionBrush` właściwości i, `SelectionTextBrush` Aby wygenerować wszelkie kombinacje kolorów tła i pierwszego planu, które są uważane za odpowiednie.

**Obsługa właściwości UIAutomation ControllerFor**

Właściwość UIAutomation `ControllerFor` zwraca tablicę elementów automatyzacji, które są manipulowane przez element automatyzacji, który obsługuje tę właściwość. Ta właściwość jest często używana do automatycznego sugerowania ułatwień dostępu. `ControllerFor` jest używany, gdy element automatyzacji ma wpływ na jeden lub więcej segmentów interfejsu użytkownika aplikacji lub pulpitu. W przeciwnym razie trudno jest powiązać wpływ operacji sterowania z elementami interfejsu użytkownika. Ta funkcja dodaje możliwość kontroli w celu udostępnienia wartości `ControllerFor` właściwości.

.NET Framework 4,8 dodaje nową metodę wirtualną, <xref:System.Windows.Automation.Peers.AutomationPeer.GetControlledPeersCore?displayProperty=nameWithType?displayProperty=nameWithType> . Aby podać wartość `ControllerFor` właściwości, wystarczy przesłonić tę metodę i zwrócić `List<AutomationPeer>` do kontrolek manipulowanych przez ten element <xref:System.Windows.Automation.Peers.AutomationPeer> :

```csharp
public class AutoSuggestTextBox: TextBox
{
   protected override AutomationPeer OnCreateAutomationPeer()
   {
      return new AutoSuggestTextBoxAutomationPeer(this);
   }

   public ListBox SuggestionListBox;
}

internal class AutoSuggestTextBoxAutomationPeer : TextBoxAutomationPeer
{
   public AutoSuggestTextBoxAutomationPeer(AutoSuggestTextBox owner) : base(owner)
   {
   }

   protected override List<AutomationPeer> GetControlledPeersCore()
   {
      List<AutomationPeer> controlledPeers = new List<AutomationPeer>();
      AutoSuggestTextBox owner = Owner as AutoSuggestTextBox;
      controlledPeers.Add(UIElementAutomationPeer.CreatePeerForElement(owner.SuggestionListBox));
      return controlledPeers;
   }
}
```

**Etykietki narzędzi na dostępie z klawiatury**

W .NET Framework 4.7.2 i starszych wersjach etykietki narzędzi są wyświetlane tylko wtedy, gdy użytkownik umieści kursor myszy nad kontrolką. W .NET Framework 4,8 etykietki narzędzi są również wyświetlane na nacisk klawiatury, a także za pomocą skrótu klawiaturowego.

Aby włączyć tę funkcję, aplikacja musi być ukierunkowana na .NET Framework 4,8 lub zadecydować przy użyciu `Switch.UseLegacyAccessibilityFeatures.3` `Switch.UseLegacyToolTipDisplay` przełączników i [AppContext](../configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md) . Poniżej znajduje się przykładowy plik konfiguracji aplikacji:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
   <startup>
      <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5" />
   </startup>
   <runtime>
      <AppContextSwitchOverrides value="Switch.UseLegacyAccessibilityFeatures=false;Switch.UseLegacyAccessibilityFeatures.2=false;Switch.UseLegacyAccessibilityFeatures.3=false;Switch.UseLegacyToolTipDisplay=false" />
   </runtime>
</configuration>
```

Po włączeniu wszystkie kontrolki zawierające etykietkę narzędzia wyświetlają ją, gdy kontrolka odbierze fokus klawiatury. Etykietka narzędzia może zostać odrzucona z upływem czasu lub po zmianie fokusu klawiatury. Użytkownicy mogą również odrzucić etykietkę narzędzia ręcznie przy użyciu nowego skrótu klawiaturowego, Ctrl + Shift + F10. Gdy etykietka narzędzia zostanie odrzucona, może być ponownie wyświetlana przy użyciu tego samego skrótu klawiaturowego.

> [!NOTE]
> [Etykietki narzędzi wstążki](xref:System.Windows.Controls.Ribbon.RibbonToolTip) na <xref:System.Windows.Controls.Ribbon.Ribbon> kontrolkach nie będą wyświetlane na fokusie klawiatury; są wyświetlane tylko za pomocą skrótu klawiaturowego.

**Dodano obsługę właściwości SizeOfSet i PositionInSet UIAutomation**

System Windows 10 wprowadził dwie nowe właściwości UIAutomation `SizeOfSet` , `PositionInSet` które są używane przez aplikacje do opisywania liczby elementów w zestawie. UIAutomation aplikacje klienckie, takie jak czytniki zawartości ekranu, mogą następnie wysyłać zapytania do aplikacji, aby ogłosić dokładną reprezentację interfejsu użytkownika aplikacji.

Począwszy od .NET Framework 4,8, WPF uwidacznia te dwie właściwości UIAutomation w aplikacjach WPF. Można to zrobić na dwa sposoby:

- Przy użyciu właściwości zależności.

  WPF dodaje dwie nowe właściwości zależności <xref:System.Windows.Automation.AutomationProperties.SizeOfSet?displayProperty=nameWithType> i <xref:System.Windows.Automation.AutomationProperties.PositionInSet?displayProperty=nameWithType> . Deweloper może użyć języka XAML, aby ustawić ich wartości:

  ```xaml
  <Button AutomationProperties.SizeOfSet="3"
    AutomationProperties.PositionInSet="1">Button 1</Button>

  <Button AutomationProperties.SizeOfSet="3"
    AutomationProperties.PositionInSet="2">Button 2</Button>

  <Button AutomationProperties.SizeOfSet="3"
    AutomationProperties.PositionInSet="3">Button 3</Button>
  ```

- Przez zastępowanie metod wirtualnych AutomationPeer.

  <xref:System.Windows.Automation.Peers.AutomationPeer.GetSizeOfSetCore>Metody i <xref:System.Windows.Automation.Peers.AutomationPeer.GetPositionInSetCore> wirtualne zostały dodane do klasy AutomationPeer. Deweloper może podać wartości dla `SizeOfSet` i, `PositionInSet` zastępując te metody, jak pokazano w następującym przykładzie:

  ```csharp
  public class MyButtonAutomationPeer : ButtonAutomationPeer
  {
    protected override int GetSizeOfSetCore()
    {
        // Call into your own logic to provide a value for SizeOfSet
        return CalculateSizeOfSet();
    }

    protected override int GetPositionInSetCore()
    {
        // Call into your own logic to provide a value for PositionInSet
        return CalculatePositionInSet();
    }
  }
  ```

Ponadto elementy w <xref:System.Windows.Controls.ItemsControl> wystąpieniach udostępniają wartość tych właściwości automatycznie bez dodatkowej akcji od dewelopera. Jeśli obiekt <xref:System.Windows.Controls.ItemsControl> jest zgrupowany, Kolekcja grup jest reprezentowana jako zestaw, a każda grupa jest traktowana jako oddzielny zestaw, przy czym każdy element wewnątrz tej grupy udostępnia swoją pozycję wewnątrz tej grupy, a także rozmiar grupy. Wirtualizacja nie ma wpływ na wartości automatyczne. Nawet jeśli element nie jest zrealizowany, nadal jest liczony do całkowitego rozmiaru zestawu i ma wpływ na pozycję w zestawie elementów równorzędnych.

Wartości automatyczne są dostępne tylko wtedy, gdy aplikacja jest docelowa .NET Framework 4,8. W przypadku aplikacji przeznaczonych dla starszej wersji .NET Framework można ustawić `Switch.UseLegacyAccessibilityFeatures.3` [przełącznik AppContext](../configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md), jak pokazano w następującym pliku App.config:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
   <startup>
      <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5" />
   </startup>
   <runtime>
      <AppContextSwitchOverrides value="Switch.UseLegacyAccessibilityFeatures=false;Switch.UseLegacyAccessibilityFeatures.2=false;Switch.UseLegacyAccessibilityFeatures.3=false" />
   </runtime>
</configuration>
```

<a name="wf48"></a>

### <a name="windows-workflow-foundation-wf-workflow-designer"></a>Projektant przepływu pracy Windows Workflow Foundation (WF)

Projektant przepływu pracy obejmuje następujące zmiany w .NET Framework 4,8:

- Użytkownicy korzystający z programu Narrator zobaczą ulepszenia w etykietach przypadków FlowSwitch.

- Użytkownicy korzystający z programu Narrator zobaczą ulepszenia w opisach przycisków.

- Użytkownicy, którzy wybierają duży kontrast motywy zobaczą ulepszenia widoczności Projektant przepływu pracy i jej kontrolek, takich jak lepsze współczynniki kontrastu między elementami i bardziej zauważalne pola wyboru używane na potrzeby elementów fokusu.

Jeśli aplikacja jest przeznaczona dla .NET Framework 4.7.2 lub starszej wersji, możesz zrezygnować z tych zmian, ustawiając `Switch.UseLegacyAccessibilityFeatures.3` [przełącznik AppContext](../configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md) `false` w pliku konfiguracyjnym aplikacji. Aby uzyskać więcej informacji, zobacz sekcję [Korzystanie z ulepszeń ułatwień dostępu](#taking-advantage-of-accessibility-enhancements) w tym artykule.

## <a name="whats-new-in-accessibility-in-net-framework-472"></a>Nowości w ułatwieniach dostępu w programie .NET Framework 4.7.2

Program .NET Framework 4.7.2 zawiera nowe funkcje ułatwień dostępu w następujących obszarach:

- [Windows Forms](#winforms472)

- [Windows Presentation Foundation (WPF)](#wpf472)

<a name="winforms472"></a>

### <a name="windows-forms"></a>Windows Forms

**Kolory zdefiniowane przez system operacyjny w duży kontrast motywy**

Począwszy od .NET Framework 4.7.2, Windows Forms używa kolorów zdefiniowanych przez system operacyjny w duży kontrast motywach. Ma to wpływ na następujące kontrolki:

- Strzałka listy rozwijanej <xref:System.Windows.Forms.ToolStripDropDownButton> kontrolki.

- <xref:System.Windows.Forms.Button> <xref:System.Windows.Forms.RadioButton> I <xref:System.Windows.Forms.CheckBox> kontrolek z <xref:System.Windows.Forms.ButtonBase.FlatStyle> ustawionym na <xref:System.Windows.Forms.FlatStyle.Flat?displayProperty=nameWithType> lub <xref:System.Windows.Forms.FlatStyle.Popup?displayProperty=nameWithType> . Wcześniej wybrane kolory tekstu i tła nie były kontrastowe i były trudne do odczytania.

- Kontrolki zawarte w elemencie <xref:System.Windows.Forms.GroupBox> , który ma <xref:System.Windows.Forms.Control.Enabled> Właściwość ustawioną na `false` .

- <xref:System.Windows.Forms.ToolStripButton> <xref:System.Windows.Forms.ToolStripComboBox> Kontrolki, i <xref:System.Windows.Forms.ToolStripDropDownButton> , które mają zwiększony stopień kontrastu jaskrawości w trybie duży kontrast.

- <xref:System.Windows.Forms.DataGridViewLinkCell.LinkColor>Właściwość <xref:System.Windows.Forms.DataGridViewLinkCell> .

**Ulepszenia Narratora**

Począwszy od .NET Framework 4.7.2, obsługa Narratora została ulepszona w następujący sposób:

- Anonsuje wartość właściwości przy zapowiadaniu <xref:System.Windows.Forms.ToolStripMenuItem.ShortcutKeys?displayProperty=nameWithType> tekstu <xref:System.Windows.Forms.ToolStripMenuItem> .

- Wskazuje, kiedy <xref:System.Windows.Forms.ToolStripMenuItem> <xref:System.Windows.Forms.Control.Enabled> Właściwość ma ustawioną wartość `false` .

- Przekazuje ona opinię na temat stanu pola wyboru, gdy <xref:System.Windows.Forms.ListView.CheckBoxes?displayProperty=nameWithType> Właściwość jest ustawiona na `true` .

- Kolejność fokusu trybu skanowania programu Narrator jest zgodna z kolejnością wizualizacji kontrolek w oknie dialogowym pobierania ClickOnce.

**Usprawnienia formantu DataGridView**

Począwszy od .NET Framework 4.7.2, <xref:System.Windows.Forms.DataGridView> formant wprowadził następujące udoskonalenia ułatwień dostępu:

- Wiersze można sortować przy użyciu klawiatury. Użytkownik może użyć klawisza F3, aby posortować według bieżącej kolumny.

- Gdy <xref:System.Windows.Forms.DataGridView.SelectionMode?displayProperty=nameWithType> jest ustawiona na <xref:System.Windows.Forms.DataGridViewSelectionMode.FullRowSelect?displayProperty=nameWithType> , nagłówek kolumny zmienia kolor, aby wskazać bieżącą kolumnę jako karty użytkownika przez komórki w bieżącym wierszu.

- <xref:System.Windows.Forms.AccessibleObject.Parent?displayProperty=nameWithType>Właściwość a <xref:System.Windows.Forms.DataGridViewLinkCell.DataGridViewLinkCellAccessibleObject?displayProperty=nameWithType> zwraca poprawną kontrolkę nadrzędną.

**Ulepszone podpowiedzi wizualne**

- <xref:System.Windows.Forms.RadioButton> <xref:System.Windows.Forms.CheckBox> Kontrolki i z pustą <xref:System.Windows.Forms.ButtonBase.Text> właściwością wyświetlają wskaźnik ostrości po otrzymaniu fokusu.

**Ulepszona obsługa siatki właściwości**

- <xref:System.Windows.Forms.PropertyGrid>Elementy podrzędne kontrolki zwracają teraz `true` do właściwości tylko wtedy, <xref:System.Windows.Automation.ValuePattern.IsReadOnlyProperty> gdy element PropertyGrid jest włączony.

- <xref:System.Windows.Forms.PropertyGrid>Elementy podrzędne formantu zwracają `false` dla <xref:System.Windows.Automation.AutomationElement.IsEnabledProperty> właściwości tylko wtedy, gdy element PropertyGrid może zostać zmieniony przez użytkownika.

**Ulepszone nawigowanie po klawiaturze**

- <xref:System.Windows.Forms.ToolStripButton>Formant umożliwia fokus, gdy jest zawarty w elemencie <xref:System.Windows.Forms.ToolStripPanel> , który ma <xref:System.Windows.Forms.ToolStripPanel.TabStop> Właściwość ustawioną na`true`

<a name="wpf472"></a>

### <a name="windows-presentation-foundation-wpf"></a>Windows Presentation Foundation (WPF)

**Zmiany w kontrolkach CheckBox i RadioButton**

W .NET Framework 4.7.1 i starszych wersjach, WPF <xref:System.Windows.Controls.CheckBox?displayProperty=nameWIthType> i <xref:System.Windows.Controls.RadioButton?displayProperty=nameWIthType> kontrolki są niespójne i w kompozycjach klasycznych i duży kontrast, nieprawidłowe wizualizacje fokusu.  Te problemy występują w przypadkach, gdy kontrolki nie mają żadnego zestawu zawartości.  Może to spowodować, że przejście między motywami jest mylące i wizualizacja fokusu będzie widoczna.

W .NET Framework 4.7.2 te wizualizacje są teraz bardziej spójne w różnych motywach i łatwiej widoczne w klasycznych i duży kontrast motywach.

**Kontrolki WinForms hostowane w aplikacji WPF**

W przypadku kontrolki WinForms hostowanej w aplikacji WPF w .NET Framework 4.7.1 i starszych wersjach użytkownicy nie mogli wystawić z warstwy WinForms, jeśli pierwszy lub ostatni formant w tej warstwie jest <xref:System.Windows.Forms.Integration.ElementHost> formantem WPF. W .NET Framework 4.7.2 Użytkownicy mogą teraz wystawić kartę z warstwy WinForms.

Jednak zautomatyzowane aplikacje, które opierają się na koncentracji, nigdy nie ucieczką warstwy WinForms, mogą przestać działać zgodnie z oczekiwaniami.

## <a name="whats-new-in-accessibility-in-net-framework-471"></a>Nowości w ułatwieniach dostępu w programie .NET Framework 4.7.1

Program .NET Framework 4.7.1 zawiera nowe funkcje ułatwień dostępu w następujących obszarach:

- [Windows Presentation Foundation (WPF)](#wpf471)

- [Windows Forms](#winforms471)

- [Kontrolki sieci Web ASP.NET](#aspnet471)

- [SDK Tools .NET](#tools471)

- [Projektant przepływu pracy Windows Workflow Foundation (WF)](#wf471)

<a name="wpf471"></a>

### <a name="windows-presentation-foundation-wpf"></a>Windows Presentation Foundation (WPF)

**Ulepszenia czytnika ekranu**

W przypadku włączenia ulepszeń ułatwień dostępu .NET Framework 4.7.1 obejmuje następujące udoskonalenia, które mają wpływ na czytniki zawartości ekranu:

- W .NET Framework 4,7 i wcześniejszych wersjach <xref:System.Windows.Controls.Expander> formanty zostały ogłoszone przez czytniki ekranu jako przyciski. Począwszy od .NET Framework 4.7.1, są one prawidłowo anonsowane jako rozwijane/zwijane grupy.

- W .NET Framework 4,7 i wcześniejszych wersjach <xref:System.Windows.Controls.DataGridCell> formanty zostały ogłoszone przez czytniki ekranu jako "niestandardowe". Począwszy od .NET Framework 4.7.1, są one teraz prawidłowo anonsowane jako komórka siatki danych (zlokalizowany).

- Począwszy od .NET Framework 4.7.1, czytniki ekranu anonsują nazwę edytowalną <xref:System.Windows.Controls.ComboBox> .

- W .NET Framework 4,7 i wcześniejszych wersjach, <xref:System.Windows.Controls.PasswordBox> formanty zostały ogłoszone jako "Brak elementów w widoku" lub w inny sposób nieprawidłowe zachowanie. Ten problem został rozwiązany, rozpoczynając od .NET Framework 4.7.1.

**Obsługa LiveRegion UIAutomation**

Czytniki ekranu, takie jak Narrator, ułatwiają osobom odczytywanie zawartości interfejsu użytkownika aplikacji, zazwyczaj przez zamianę tekstu na mowę dla zawartości interfejsu użytkownika, która ma fokus. Jeśli jednak element interfejsu użytkownika zmieni się i nie ma fokusu, użytkownik może nie zostać powiadomiony i może pominąć ważne informacje. Regiony na żywo mają na celu rozwiązanie tego problemu. Programista może użyć ich do informowania czytnika ekranu lub innego klienta UIAutomation o tym, że wprowadzono ważną zmianę w elemencie interfejsu użytkownika. Czytnik ekranu może następnie zdecydować, jak i kiedy należy poinformować użytkownika o tej zmianie.

Do obsługi regionów na żywo dodano następujące interfejsy API do platformy WPF:

- <xref:System.Windows.Automation.AutomationElementIdentifiers.LiveSettingProperty?displayProperty=nameWithType>Pola i <xref:System.Windows.Automation.AutomationElementIdentifiers.LiveRegionChangedEvent?displayProperty=nameWithType> , które identyfikują Właściwość **LiveSetting** i zdarzenie **LiveRegionChanged** . Można je ustawić przy użyciu języka XAML.

- Dołączona właściwość **AutomationProperties. LiveSetting** , która informuje czytnik ekranu o ważności zmiany interfejsu użytkownika.

- <xref:System.Windows.Automation.AutomationProperties.LiveSettingProperty?displayProperty=nameWithType>Właściwość, która identyfikuje załączoną Właściwość **AutomationProperties. LiveSetting** .

- <xref:System.Windows.Automation.Peers.AutomationPeer.GetLiveSettingCore%2A?displayProperty=nameWithType>Metoda, którą można zastąpić, aby zapewnić wartość **LiveSetting** .

- <xref:System.Windows.Automation.AutomationProperties.GetLiveSetting%2A?displayProperty=nameWithType>Metody i <xref:System.Windows.Automation.AutomationProperties.SetLiveSetting%2A?displayProperty=nameWithType> , które uzyskują i ustawiają wartość **LiveSetting** .

- <xref:System.Windows.Automation.AutomationLiveSetting?displayProperty=nameWithType>Wyliczenie, które definiuje następujące możliwe wartości **LiveSetting** :

  - <xref:System.Windows.Automation.AutomationLiveSetting.Off?displayProperty=nameWithType>. Element nie wysyła powiadomień, jeśli zawartość regionu aktywnego zmieniła się.
  - <xref:System.Windows.Automation.AutomationLiveSetting.Polite?displayProperty=nameWithType>. Element wysyła powiadomienia nieprzerwane, jeśli zawartość regionu aktywnego uległa zmianie.

  - <xref:System.Windows.Automation.AutomationLiveSetting.Assertive?displayProperty=nameWithType>. Element wysyła powiadomienia o przerwie, jeśli zawartość regionu aktywnego uległa zmianie.

Można utworzyć LiveRegion przez ustawienie właściwości **AutomationProperties. LiveSetting** dla elementu zainteresowania, jak pokazano w następującym przykładzie:

```xaml
<TextBlock Name="myTextBlock" AutomationProperties.LiveSetting="Assertive">announcement</TextBlock>
```

Gdy dane w regionie aktywnym zmieniają się i musisz poinformować czytnik ekranu, można jawnie zgłosić zdarzenie, jak pokazano w poniższym przykładzie.

```csharp
var peer = FrameworkElementAutomationPeer.FromElement(myTextBlock);

peer.RaiseAutomationEvent(AutomationEvents.LiveRegionChanged);
```

```vb
Dim peer = FrameworkElementAutomationPeer.FromElement(myTextBlock)
peer.RaiseAutomationEvent(AutomationEvents.LiveRegionChanged)

```

**High contrast** (Wysoki kontrast)

Począwszy od .NET Framework 4.7.1, wprowadzono ulepszenia w różnych kontrolkach WPF. Są one teraz widoczne po <xref:System.Windows.SystemParameters.HighContrast%2A> ustawieniu motywu. Należą do nich:

- <xref:System.Windows.Controls.Expander> kontroli

  Wizualizacja fokusu dla  <xref:System.Windows.Controls.Expander> kontrolki jest teraz widoczna. Wizualizacje klawiatury dla <xref:System.Windows.Controls.ComboBox> , <xref:System.Windows.Controls.ListBox> i <xref:System.Windows.Controls.RadioButton> kontrolki są również widoczne. Na przykład:

  Przed:

  ![Zrzut ekranu kontrolki ekspandera z fokusem i wizualizacja fokusu.](./media/whats-new-in-accessibility/expander-control-before.png)

  Po:

  ![Zrzut ekranu kontrolki ekspandera z fokusem pokazującą kropkowaną linię wokół tekstu kontrolki.](./media/whats-new-in-accessibility/expander-control-after.png)

- <xref:System.Windows.Controls.CheckBox> i <xref:System.Windows.Controls.RadioButton> kontrolki

  Tekst w <xref:System.Windows.Controls.CheckBox> <xref:System.Windows.Controls.RadioButton> kontrolkach i jest teraz łatwiejszy do sprawdzenia, gdy wybrane są motywy o dużym kontraście. Na przykład:

  Przed:

  ![Zrzut ekranu przycisków radiowych i kontrolek z niską widocznością tekstu w motywach o wysokim kontraście.](./media/whats-new-in-accessibility/high-contrast-radio-button-before.png)

  Po:

  ![Zrzut ekranu przycisków radiowych i kontrolek z lepszą widocznością tekstu w motywach o wysokim kontraście.](./media/whats-new-in-accessibility/high-contrast-radio-button-after.png)

- <xref:System.Windows.Controls.ComboBox> kontroli

  Począwszy od .NET Framework 4.7.1, obramowanie wyłączonej <xref:System.Windows.Controls.ComboBox> kontrolki ma taki sam kolor jak wyłączony tekst. Na przykład:

  Przed:

  ![Zrzut ekranu wyłączonego ComboBox z obramowaniem i tekstem kontrolki w różnych kolorach.](./media/whats-new-in-accessibility/combo-disabled-before.png)

  Po:

  ![Zrzut ekranu wyłączonego ComboBox z obramowaniem o taki sam kolor jak tekst kontrolki.](./media/whats-new-in-accessibility/combo-disabled-after.png)

  Ponadto przyciski wyłączone i priorytetowe używają poprawnego koloru motywu.

  Przed:

  ![Zrzut ekranu czarnego przycisku z szarym tekstem mówiący, aby skoncentrować się.](./media/whats-new-in-accessibility/button-theme-colors-before.png)

  Po:

  ![Zrzut ekranu przedstawiający niebieski przycisk z czarnym tekstem, który mówi mnie.](./media/whats-new-in-accessibility/button-theme-colors-after.png)

  Na koniec, w .NET Framework 4,7 i wcześniejszych wersjach, ustawienie <xref:System.Windows.Controls.ComboBox> stylu kontrolki tak, aby `Toolbar.ComboBoxStyleKey` powodowała, że strzałka listy rozwijanej ma być niewidoczna. Ten problem został rozwiązany, rozpoczynając od .NET Framework 4.7.1. Na przykład:

  Przed:

  ![Zrzut ekranu kontrolki ComboBox z niewidoczną strzałką listy rozwijanej.](./media/whats-new-in-accessibility/combo-box-style-key-before.png)

  Po:

  ![Zrzut ekranu przedstawiający formant ComboBox wyświetlający strzałkę listy rozwijanej.](./media/whats-new-in-accessibility/combo-box-style-key-after.png)

- <xref:System.Windows.Controls.DataGrid> kontroli

  Począwszy od .NET Framework 4.7.1, strzałka sortowania w <xref:System.Windows.Controls.DataGrid> kontrolkach używa teraz poprawnych kolorów motywu. Na przykład:

  Przed:

  ![Zrzut ekranu przedstawiający strzałkę wskaźnika sortowania przed ulepszeniami.](./media/whats-new-in-accessibility/sort-indicator-before.png)

  Po:

  ![Zrzut ekranu przedstawiający strzałkę wskaźnika sortowania po ulepszeniach.](./media/whats-new-in-accessibility/sort-indicator-after.png)

  Ponadto w .NET Framework 4,7 i wcześniejszych wersjach domyślny styl łącza został zmieniony na nieprawidłowy kolor na przycisku myszy nad trybem dużego kontrastu. Jest to rozwiązane, rozpoczynając od .NET Framework 4.7.1. Podobnie <xref:System.Windows.Controls.DataGrid> kolumny CheckBox używają oczekiwanych kolorów dla opinii o fokusie klawiatury, zaczynając od .NET Framework 4.7.1.

  Przed:

  ![Zrzut ekranu przedstawiający link mówiący o kliknięciu mnie! na czerwono.](./media/whats-new-in-accessibility/default-link-style-before.png)

  Po:

  ![Zrzut ekranu przedstawiający link mówiący o kliknięciu mnie! na żółto.](./media/whats-new-in-accessibility/default-link-style-after.png)

Aby uzyskać więcej informacji na temat ulepszeń ułatwień dostępu WPF w .NET Framework 4.7.1, zobacz [ulepszenia ułatwień dostępu w programie WPF](../migration-guide/retargeting/4.7-4.7.1.md#accessibility-improvements-in-wpf).

<a name="winforms471"></a>

### <a name="windows-forms-accessibility-improvements"></a>Ulepszenia ułatwień dostępu Windows Forms

W .NET Framework 4.7.1 Windows Forms (WinForms) obejmuje zmiany ułatwień dostępu w następujących obszarach.

**Udoskonalone wyświetlanie w trybie duży kontrast**

Począwszy od .NET Framework 4.7.1, różne kontrolki WinForm oferują ulepszone renderowanie w trybach HighContrast dostępnych w systemie operacyjnym. System Windows 10 zmienił wartości niektórych kolorów systemu o dużym kontraście, a Windows Forms jest oparty na strukturze Win32 systemu Windows 10. Aby uzyskać najlepsze środowisko, uruchom polecenie w najnowszej wersji systemu Windows i zapoznaj się z najnowszymi zmianami systemu operacyjnego przez dodanie pliku App. manifest do aplikacji testowej i odskomentuj wiersz systemu operacyjnego Windows 10, aby wyglądał następująco:

```xml
<!-- Windows 10 -->
<supportedOS Id="{8e0f7a12-bfb3-4fe8-b9a5-48fd50a15a9a}" />
```

Niektóre przykłady zmian wysokiego kontrastu obejmują:

- Zaznaczenia <xref:System.Windows.Forms.MenuStrip> elementów są łatwiejsze do wyświetlenia.

- Po wybraniu <xref:System.Windows.Forms.MenuStrip> elementy wyłączone są łatwiejsze do wyświetlenia.

- Tekst w wybranym <xref:System.Windows.Forms.Button> formancie różni się od koloru zaznaczenia.

- Wyłączony tekst jest łatwiejszy do odczytania. Na przykład:

  Przed:

  ![Zrzut ekranu aplikacji korzystającej z różnych kontrolek działających w trybie dużego kontrastu przed udoskonaleniami ułatwień dostępu.](./media/whats-new-in-accessibility/high-contrast-mode-menu-items-before.png)

  Po:

  ![Zrzut ekranu aplikacji korzystającej z różnych kontrolek uruchomionych w trybie dużego kontrastu po udoskonaleniu ułatwień dostępu.](./media/whats-new-in-accessibility/high-contrast-mode-menu-items-after.png)

- Ulepszenia dużego kontrastu w oknie dialogowym wyjątku wątku.

**Ulepszona obsługa Narratora**

Windows Forms w programie .NET Framework 4.7.1 zawierają następujące ulepszenia ułatwień dostępu dla programu Narrator:

- <xref:System.Windows.Forms.MonthCalendar>Dostęp do formantu można uzyskać za pomocą programu Narrator, a także innych narzędzi automatyzacji interfejsu użytkownika.

- <xref:System.Windows.Forms.CheckedListBox>Formant powiadamia program Narrator, gdy stan zaznaczenia elementu zmienił się, aby użytkownik był powiadomiony o zmianie wartości elementu listy.

- <xref:System.Windows.Forms.DataGridViewCell>Kontrolka raportuje poprawny stan tylko do odczytu w programie narrator.

- Narrator może teraz odczytywać wyłączony <xref:System.Windows.Forms.ToolStripMenuItem> tekst, podczas gdy wcześniej mógłby pominąć wyłączone elementy menu.

**Ulepszona obsługa wzorców dostępności UIAutomation**

Począwszy od .NET Framework 4.7.1, deweloperzy narzędzi technologii ułatwień dostępu mogą korzystać ze wspólnych wzorców dostępności interfejsu API i właściwości dla kilku kontrolek WinForms. Ulepszenia ułatwień dostępu obejmują:

- <xref:System.Windows.Forms.ComboBox>I <xref:System.Windows.Forms.ToolStripSplitButton> teraz obsługuje [wzorzec Rozwiń/Zwiń](../ui-automation/implementing-the-ui-automation-expandcollapse-control-pattern.md).

- <xref:System.Windows.Forms.DataGridViewCheckBoxCell>Obsługuje teraz [wzorzec przełączania](../ui-automation/implementing-the-ui-automation-toggle-control-pattern.md).

- <xref:System.Windows.Forms.ToolStripItem>Kontrolka obsługuje <xref:System.Windows.Automation.AutomationElement.AutomationElementInformation.Name> Właściwość oraz [wzorzec Rozwiń/Zwiń](../ui-automation/implementing-the-ui-automation-expandcollapse-control-pattern.md).

- <xref:System.Windows.Forms.NumericUpDown>Formanty i <xref:System.Windows.Forms.DomainUpDown> obsługują <xref:System.Windows.Automation.AutomationElement.AutomationElementInformation.Name> Właściwość.

**Ulepszone środowisko przeglądarki właściwości**

Począwszy od .NET Framework 4.7.1, Windows Forms obejmuje:

- Lepsza Nawigacja przy użyciu klawiatury w różnych oknach menu rozwijanego.
- Zmniejszenie niepotrzebnych tabulatorów.
- Lepsze raportowanie typów kontroli.
- Ulepszone zachowanie narratora.

<a name="aspnet471"></a>

### <a name="aspnet-web-controls"></a>Kontrolki sieci Web ASP.NET

Począwszy od .NET Framework 4.7.1 i programu Visual Studio 2017 w wersji 15,3, ASP.NET ulepsza, jak formanty sieci Web ASP.NET działają z technologią ułatwień dostępu w programie Visual Studio. Zmiany obejmują następujące elementy:

- Zmiany w celu zaimplementowania brakujących wzorców dostępności interfejsu użytkownika w kontrolkach, takich jak okno dialogowe **Dodawanie pola** w kreatorze **widoku szczegółów** lub okno dialogowe **Konfiguruj widok ListView** kreatora **ListView** .

- Zmiany w celu usprawnienia wyświetlania w trybie duży kontrast, takie jak **Edytor pól modułu stronicowania danych**.

- Zmiany w celu ulepszenia środowiska nawigacji klawiatury dla kontrolek, takich jak okno dialogowe **pola** w kreatorze **Edytuj pola modułu stronicowania** kontrolki formantu DataPager, okno dialogowe **Konfigurowanie obiektu ObjectContext** lub okno dialogowe **Konfigurowanie wyboru danych** kreatora **konfiguracji źródła danych** .

<a name="tools471"></a>

### <a name="net-sdk-tools"></a>SDK Tools .NET

[Narzędzie edytora konfiguracji (SvcConfigEditor.exe)](../wcf/configuration-editor-tool-svcconfigeditor-exe.md) i [narzędzie Podgląd śledzenia usług (SvcTraceViewer.exe)](../wcf/service-trace-viewer-tool-svctraceviewer-exe.md) zostały ulepszone, rozwiązując różne problemy z dostępnością. Większość z nich dotyczyła małych problemów, takich jak nazwa, która nie jest zdefiniowana lub niektóre wzorce automatyzacji interfejsu użytkownika nie są poprawnie zaimplementowane. Chociaż wielu użytkowników nie ma informacji o tych nieprawidłowych wartościach, klienci korzystający z technologii pomocniczych, takich jak czytniki zawartości ekranu, zobaczą więcej dostępnych narzędzi zestawu SDK.

Te udoskonalenia zmieniają niektóre poprzednie zachowania, na przykład kolejność fokusu klawiatury.

<a name="wf471"></a>

### <a name="windows-workflow-foundation-wf-workflow-designer"></a>Projektant przepływu pracy Windows Workflow Foundation (WF)

Zmiany ułatwień dostępu w Projektant przepływu pracy obejmują następujące elementy:

- Kolejność tabulacji zmieni się na od lewej do prawej i od góry do dołu w niektórych kontrolkach:

  - Okno inicjowania korelacji do ustawiania danych korelacji dla <xref:System.ServiceModel.Activities.InitializeCorrelation> działania.

  - Okno definicji zawartości dla <xref:System.ServiceModel.Activities.Receive> działań,, <xref:System.ServiceModel.Activities.Send> <xref:System.ServiceModel.Activities.SendReply> i <xref:System.ServiceModel.Activities.ReceiveReply> .

- Więcej funkcji jest dostępnych za pośrednictwem klawiatury:

  - Podczas edytowania właściwości działania grupy właściwości mogą być zwijane przez klawiaturę po raz pierwszy.

  - Ikony ostrzeżeń są dostępne na klawiaturze.

  - Przycisk **więcej właściwości** w oknie **Właściwości** jest dostępny na klawiaturze.

  - Użytkownicy klawiatury mogą uzyskać dostęp do elementów nagłówka w okienkach **argumenty** i **zmienne** Projektant przepływu pracy.

- Ulepszona widoczność elementów z fokusem, takich jak:

  - Dodawanie wierszy do siatek danych używanych przez Projektant przepływu pracy i projektantów działań.

  - Używanie tabulacji w polach w <xref:System.ServiceModel.Activities.ReceiveReply> <xref:System.ServiceModel.Activities.SendReply> działaniach i.

  - Ustawianie wartości domyślnych dla zmiennych lub argumentów

- Czytniki zawartości ekranu mogą teraz prawidłowo rozpoznać:

  - Punkty przerwania ustawione w Projektancie przepływu pracy.

  - <xref:System.Activities.Statements.FlowSwitch%601>Działania, <xref:System.Activities.Statements.FlowDecision> i <xref:System.ServiceModel.Activities.CorrelationScope> .
  - Zawartość <xref:System.ServiceModel.Activities.Receive> działania.

  - Typ docelowy dla <xref:System.Activities.Statements.InvokeMethod> działania.

  - Pole kombi wyjątku oraz sekcja finally w <xref:System.Activities.Statements.TryCatch> działaniu.

  - Pole kombi typ komunikatu, rozdzielacz w oknie Dodaj inicjatory korelacji, okno definicji zawartości i okno definicji CorrelatesOn w działaniach związanych z wiadomościami ( <xref:System.ServiceModel.Activities.Receive> , <xref:System.ServiceModel.Activities.Send> , <xref:System.ServiceModel.Activities.SendReply> i <xref:System.ServiceModel.Activities.ReceiveReply> ).

  - Przejścia komputera stanu i miejsca docelowe przejść.

  - Adnotacje i łączniki na <xref:System.Activities.Statements.FlowDecision> działaniach.

  - Menu kontekstowe (kliknij prawym przyciskiem myszy) dla działań.

  - Edytor wartości właściwości, przycisk Wyczyść wyszukiwanie, Kategoria według oraz alfabetyczne przyciski sortowania i okno dialogowe Edytor wyrażeń w siatce właściwości.

  - Procent powiększenia w Projektant przepływu pracy.

  - Separator w <xref:System.Activities.Statements.Parallel> <xref:System.Activities.Statements.Pick> działaniach i.

  - <xref:System.Activities.Statements.InvokeDelegate>Działanie.

  - Okno wybór typów dla działań słownika ( `Microsoft.Activities.AddToDictionary<TKey,TValue>` , `Microsoft.Activities.RemoveFromDictionary<TKey,TValue>` itp.).

  - Okno Przeglądaj i wybierz typ platformy .NET.

  - Struktura nawigacyjna w Projektant przepływu pracy.

- Użytkownicy, którzy wybierają duży kontrast motywy zobaczą wiele ulepszeń w zakresie widoczności Projektant przepływu pracy i jej kontrolek, takich jak lepsze współczynniki kontrastu między elementami i bardziej zauważalne pola wyboru używane do elementów fokusu.

## <a name="see-also"></a>Zobacz też

- [Co nowego w programie .NET Framework](index.md)
