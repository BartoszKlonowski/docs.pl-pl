---
title: Kompiluj składniki interfejsu użytkownika wielokrotnego użytku z Blazor
description: Dowiedz się, jak tworzyć składniki interfejsu użytkownika wielokrotnego użytku z Blazor i jak są one porównywane z kontrolkami formularzy Web Forms ASP.NET.
author: danroth27
ms.author: daroth
no-loc:
- Blazor
ms.date: 09/18/2019
ms.openlocfilehash: fd560c84c095dffc3718a7709af904d9ba722a18
ms.sourcegitcommit: d0990c1c1ab2f81908360f47eafa8db9aa165137
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/15/2020
ms.locfileid: "97512772"
---
# <a name="build-reusable-ui-components-with-no-locblazor"></a>Kompiluj składniki interfejsu użytkownika wielokrotnego użytku z Blazor

Jednym z atrakcyjnych elementów formularzy sieci Web ASP.NET jest to, jak umożliwia hermetyzację fragmentów kodu interfejsu użytkownika do wielokrotnego użytku. Niestandardowe kontrolki użytkownika można definiować w znacznikach przy użyciu plików *. ascx* . Można również tworzyć rozbudowane kontrolki serwera w kodzie za pomocą pełnego wsparcia projektanta.

Blazor obsługuje także hermetyzację interfejsu użytkownika za poorednictwem *składników*. Składnik:

- Jest samodzielnym fragmentem interfejsu użytkownika.
- Utrzymuje własny stan i logikę renderowania.
- Można zdefiniować procedury obsługi zdarzeń interfejsu użytkownika, powiązać dane wejściowe i zarządzać własnym cyklem życia.
- Jest zazwyczaj definiowana w pliku *Razor* przy użyciu składnia Razor.

## <a name="an-introduction-to-razor"></a>Wprowadzenie do Razor

Razor to lekki język tworzenia szablonów znaczników oparty na języku HTML i C#. Przy użyciu Razor można bezproblemowo przechodzić między znacznikami i kodem C# w celu zdefiniowania logiki renderowania składników. Po skompilowaniu pliku *Razor* logika renderowania jest przechwytywana w sposób uporządkowany w klasie .NET. Nazwa skompilowanej klasy jest pobierana z nazwy pliku *Razor* . Przestrzeń nazw jest pobierana z domyślnej przestrzeni nazw dla projektu i ścieżki folderu, lub można jawnie określić przestrzeń nazw za pomocą `@namespace` dyrektywy (więcej informacji na temat poniższych dyrektyw Razor).

Logika renderowania składnika jest utworzona przy użyciu standardowego znacznika HTML z dynamiczną logiką dodaną przy użyciu języka C#. `@`Znak jest używany do przejścia do języka C#. Razor jest zazwyczaj inteligentnym sposobem na ustalenie, kiedy przełączono z powrotem do formatu HTML. Na przykład poniższy składnik renderuje `<p>` tag z bieżącym czasem:

```razor
<p>@DateTime.Now</p>
```

Aby jawnie określić początkową i końcową wyrażenie języka C#, użyj nawiasów:

```razor
<p>@(DateTime.Now)</p>
```

Razor również ułatwia użycie przepływu sterowania języka C# w logice renderowania. Na przykład można warunkowo renderować niektóre HTML w następujący sposób:

```razor
@if (value % 2 == 0)
{
    <p>The value was even.</p>
}
```

Lub można wygenerować listę elementów przy użyciu normalnej pętli języka C# `foreach` podobnej do:

```razor
<ul>
@foreach (var item in items)
{
    <li>@item.Text</li>
}
</ul>
```

Dyrektywy Razor, podobnie jak dyrektywy w ASP.NET Web Forms, kontrolują wiele aspektów sposobu kompilowania składnika Razor. Przykłady obejmują:

- Przestrzeń nazw
- Klasa bazowa
- Zaimplementowane interfejsy
- Parametry ogólne
- Zaimportowane przestrzenie nazw
- Trasy

Dyrektywy Razor zaczynają się od `@` znaku i są zwykle używane na początku nowego wiersza na początku pliku. Na przykład `@namespace` dyrektywa definiuje przestrzeń nazw składnika:

```razor
@namespace MyComponentNamespace
```

W poniższej tabeli zestawiono różne dyrektywy Razor używane w programie Blazor i ich ekwiwalenty formularzy sieci Web ASP.NET, jeśli istnieją.

|Dyrektywę    |Opis|Przykład|Odpowiednik formularzy sieci Web|
|-------------|-----------|-------|--------------------|
|`@attribute` |Dodaje atrybut Level klasy do składnika|`@attribute [Authorize]`|Brak|
|`@code`      |Dodaje składowe klasy do składnika|`@code { ... }`|`<script runat="server">...</script>`|
|`@implements`|Implementuje określony interfejs|`@implements IDisposable`|Użyj kodu|
|`@inherits`  |Dziedziczy z określonej klasy bazowej|`@inherits MyComponentBase`|`<%@ Control Inherits="MyUserControlBase" %>`|
|`@inject`    |Wprowadza usługę do składnika|`@inject IJSRuntime JS`|Brak|
|`@layout`    |Określa składnik układu dla składnika|`@layout MainLayout`|`<%@ Page MasterPageFile="~/Site.Master" %>`|
|`@namespace` |Ustawia przestrzeń nazw dla składnika|`@namespace MyNamespace`|Brak|
|`@page`      |Określa trasę dla składnika|`@page "/product/{id}"`|`<%@ Page %>`|
|`@typeparam` |Określa parametr typu ogólnego dla składnika|`@typeparam TItem`|Użyj kodu|
|`@using`     |Określa przestrzeń nazw do dołączenia do zakresu|`@using MyComponentNamespace`|Dodaj przestrzeń nazw w *web.config*|

Składniki Razor również dzielą użycie *atrybutów dyrektywy* dla elementów w celu kontrolowania różnych aspektów kompilowania składników (obsługa zdarzeń, powiązanie danych, składnik & odwołań elementów itp.). Atrybuty dyrektywy All są zgodne ze wspólną składnią ogólną, w której wartości w nawiasach są opcjonalne:

```razor
@directive(-suffix(:name))(="value")
```

Poniższa tabela zawiera podsumowanie różnych atrybutów dyrektyw Razor używanych w programie Blazor .

|Atrybut    |Opis|Przykład|
|-------------|-----------|-------|
|`@attributes`|Renderuje słownik atrybutów|`<input @attributes="ExtraAttributes" />`|
|`@bind`      |Tworzy dwukierunkowe powiązanie danych    |`<input @bind="username" @bind:event="oninput" />`|
|`@on{event}` |Dodaje program obsługi zdarzeń dla określonego zdarzenia|`<button @onclick="IncrementCount">Click me!</button>`|
|`@key`       |Określa klucz, który ma być używany przez algorytm porównujący do zachowywania elementów w kolekcji|`<DetailsEditor @key="person" Details="person.Details" />`|
|`@ref`       |Przechwytuje odwołanie do składnika lub elementu HTML|`<MyDialog @ref="myDialog" />`|

Różne atrybuty dyrektywy używane przez Blazor ( `@onclick` , `@bind` , `@ref` , i tak dalej) zostały omówione w poniższych sekcjach i w dalszej części rozdziałów.

Wiele składni używanych w plikach *. aspx* i *. ascx* ma składnie równoległe w Razor. Poniżej znajduje się proste porównanie składni dla ASP.NET Web Forms i Razor.

|Cechy                      |Formularze sieci Web           |Składnia               |Razor         |Składnia |
|-----------------------------|--------------------|---------------------|--------------|-------|
|Dyrektyw                   |`<%@ [directive] %>`|`<%@ Page %>`        |`@[directive]`|`@page`|
|Bloki kodu                  |`<% %>`             |`<% int x = 123; %>` |`@{ }`        |`@{ int x = 123; }`|
|Wyrażenia<br>(Kodowane HTML)|`<%: %>`            |`<%:DateTime.Now %>` |Konwersja `@`<br>Wprost `@()`|`@DateTime.Now`<br>`@(DateTime.Now)`|
|Komentarze                     |`<%-- --%>`         |`<%-- Commented --%>`|`@* *@`       |`@* Commented *@`|
|Powiązanie danych                 |`<%# %>`            |`<%# Bind("Name") %>`|`@bind`       |`<input @bind="username" />`|

Aby dodać elementy członkowskie do klasy składnika Razor, użyj `@code` dyrektywy. Ta technika jest podobna do użycia `<script runat="server">...</script>` bloku w kontrolce użytkownika lub stronie formularzy sieci Web ASP.NET.

```razor
@code {
    int count = 0;

    void IncrementCount()
    {
        count++;
    }
}
```

Ponieważ Razor jest oparta na języku C#, musi być skompilowana z poziomu projektu C# (*. csproj*). Nie można kompilować plików *Razor* z projektu Visual Basic (*. vbproj*). Nadal możesz odwoływać się do Visual Basic projektów z Blazor projektu. Przeciwieństwo jest również prawdziwe.

Aby uzyskać pełne informacje dotyczące składnia Razor, zobacz [składnia Razor Reference for ASP.NET Core](/aspnet/core/mvc/views/razor).

## <a name="use-components"></a>Używanie składników

Oprócz normalnego HTML składniki mogą również używać innych składników jako części logiki renderowania. Składnia służąca do używania składnika w Razor jest podobna do użycia kontrolki użytkownika w aplikacji ASP.NET Web Forms. Składniki są określane przy użyciu tagu elementu, który jest zgodny z nazwą typu składnika. Na przykład można dodać `Counter` składnik podobny do tego:

```razor
<Counter />
```

W przeciwieństwie do ASP.NET formularzy sieci Web, składniki w Blazor :

- Nie używaj prefiksu elementu (na przykład `asp:` ).
- Nie wymagaj rejestracji na stronie ani w *web.config*.

Należy wziąć pod uwagę składniki Razor, takie jak typy .NET, ponieważ dokładnie te elementy są. Jeśli zestaw zawierający składnik jest przywoływany, składnik jest dostępny do użycia. Aby przenieść przestrzeń nazw składnika do zakresu, Zastosuj `@using` dyrektywę:

```razor
@using MyComponentLib

<Counter />
```

Jak widać w projektach domyślnych Blazor , często należy umieścić `@using` dyrektywy w pliku *_Imports. Razor* , aby zostały zaimportowane do wszystkich plików *. Razor* w tym samym katalogu i w katalogach podrzędnych.

Jeśli przestrzeń nazw składnika nie znajduje się w zakresie, można określić składnik przy użyciu pełnej nazwy typu, jak w języku C#:

```razor
<MyComponentLib.Counter />
```

## <a name="component-parameters"></a>Parametry składnika

W formularzach sieci Web ASP.NET można przepływać parametry i dane do kontrolek przy użyciu właściwości publicznych. Te właściwości można ustawić w znacznikach przy użyciu atrybutów lub ustawionych bezpośrednio w kodzie. Blazor składniki działają w podobny sposób, chociaż właściwości składnika również muszą być oznaczone `[Parameter]` atrybutem, który ma być traktowany jako parametry składnika.

Poniższy `Counter` składnik definiuje parametr składnika o nazwie `IncrementAmount` , który może służyć do określenia kwoty, którą `Counter` należy zwiększyć przy każdym kliknięciu przycisku.

```razor
<h1>Counter</h1>

<p>Current count: @currentCount</p>

<button class="btn btn-primary" @onclick="IncrementCount">Click me</button>

@code {
    int currentCount = 0;

    [Parameter]
    public int IncrementAmount { get; set; } = 1;

    void IncrementCount()
    {
        currentCount+=IncrementAmount;
    }
}
```

Aby określić parametr składnika w Blazor , Użyj atrybutu tak jak w ASP.NET Web Forms:

```razor
<Counter IncrementAmount="10" />
```

## <a name="event-handlers"></a>Procedury obsługi zdarzeń

Zarówno ASP.NET Web Forms, jak i Blazor oferują oparty na zdarzeniach model programowania do obsługi zdarzeń interfejsu użytkownika. Przykłady takich zdarzeń obejmują kliknięcia przycisku i wprowadzanie tekstu. W formularzach sieci Web ASP.NET używasz kontrolek serwera HTML do obsługi zdarzeń interfejsu użytkownika uwidocznionych przez DOM lub można obsługiwać zdarzenia udostępniane przez formanty serwera sieci Web. Zdarzenia są nakierowane na serwer za pomocą żądań post-Back. Rozważmy poniższy przycisk formularzy sieci Web, a następnie kliknij przycisk przykład:

*Counter. ascx*

```aspx-csharp
<asp:Button ID="ClickMeButton" runat="server" Text="Click me!" OnClick="ClickMeButton_Click" />
```

*Counter.ascx.cs*

```csharp
public partial class Counter : System.Web.UI.UserControl
{
    protected void ClickMeButton_Click(object sender, EventArgs e)
    {
        Console.WriteLine("The button was clicked!");
    }
}
```

W programie Blazor można rejestrować procedury obsługi zdarzeń interfejsu użytkownika dom bezpośrednio przy użyciu atrybutów dyrektywy formularza `@on{event}` . `{event}`Symbol zastępczy reprezentuje nazwę zdarzenia. Na przykład można nasłuchiwać przycisku w następujący sposób:

```razor
<button @onclick="OnClick">Click me!</button>

@code {
    void OnClick()
    {
        Console.WriteLine("The button was clicked!);
    }
}
```

Procedury obsługi zdarzeń mogą akceptować opcjonalny, specyficzny dla zdarzenia argument, aby uzyskać więcej informacji o zdarzeniu. Na przykład zdarzenia myszy mogą przyjmować `MouseEventArgs` argument, ale nie jest to wymagane.

```razor
<button @onclick="OnClick">Click me!</button>

@code {
    void OnClick(MouseEventArgs e)
    {
        Console.WriteLine($"Mouse clicked at {e.ScreenX}, {e.ScreenY}.");
    }
}
```

Zamiast odwoływać się do grupy metod programu obsługi zdarzeń, można użyć wyrażenia lambda. Wyrażenie lambda umożliwia zamknięcie innych wartości w zakresie.

```razor
@foreach (var buttonLabel in buttonLabels)
{
    <button @onclick="() => Console.WriteLine($"The {buttonLabel} button was clicked!")">@buttonLabel</button>
}
```

Procedury obsługi zdarzeń mogą być wykonywane synchronicznie lub asynchronicznie. Na przykład następująca `OnClick` procedura obsługi zdarzeń wykonuje asynchronicznie:

```razor
<button @onclick="OnClick">Click me!</button>

@code {
    async Task OnClick()
    {
        var result = await Http.GetAsync("api/values");
    }
}
```

Po obsłudze zdarzenia składnik jest renderowany w celu uwzględnienia zmian stanu składnika. W przypadku obsługi zdarzeń asynchronicznych składnik jest renderowany natychmiast po zakończeniu wykonywania procedury obsługi. Składnik jest renderowany *ponownie* po asynchronicznym `Task` zakończeniu. Ten asynchroniczny tryb wykonywania umożliwia renderowanie niektórych odpowiednich interfejsów użytkownika, podczas gdy asynchroniczne `Task` jest nadal w toku.

```razor
<button @onclick="ShowMessage">Get message</button>

@if (showMessage)
{
    @if (message == null)
    {
        <p><em>Loading...</em></p>
    }
    else
    {
        <p>The message is: @message</p>
    }
}

@code
{
    bool showMessage = false;
    string message;

    public async Task ShowMessage()
    {
        showMessage = true;
        message = await MessageService.GetMessageAsync();
    }
}
```

Składniki mogą także definiować własne zdarzenia przez zdefiniowanie parametru składnika typu `EventCallback<TValue>` . Wywołania zwrotne zdarzeń obsługują wszystkie odmiany programów obsługi zdarzeń interfejsu użytkownika DOM: argumenty opcjonalne, synchroniczne lub asynchroniczne, grupy metod lub wyrażenia lambda.

```razor
<button class="btn btn-primary" @onclick="OnClick">Click me!</button>

@code {
    [Parameter]
    public EventCallback<MouseEventArgs> OnClick { get; set; }
}
```

## <a name="data-binding"></a>Powiązanie danych

Blazor zapewnia prosty mechanizm wiązania danych ze składnika interfejsu użytkownika ze stanem składnika. Takie podejście różni się od funkcji w formularzach sieci Web ASP.NET w celu powiązania danych ze źródeł danych z kontrolkami interfejsu użytkownika. Będziemy odkrywać dane obsługi z różnych źródeł danych w sekcji [dotyczącej danych](data.md) .

Aby utworzyć dwukierunkowe powiązanie danych ze składnika interfejsu użytkownika ze stanem składnika, użyj `@bind` atrybutu dyrektywy. W poniższym przykładzie wartość pola wyboru jest powiązana z `isChecked` polem.

```razor
<input type="checkbox" @bind="isChecked" />

@code {
    bool isChecked;
}
```

Gdy składnik jest renderowany, wartość pola wyboru jest ustawiana na wartość w `isChecked` polu. Gdy użytkownik przełącza pole wyboru, `onchange` zdarzenie jest wywoływane, a `isChecked` pole jest ustawione na nową wartość. `@bind`Składnia w tym przypadku jest równoważna następującym znacznikiem:

```razor
<input value="@isChecked" @onchange="(UIChangeEventArgs e) => isChecked = e.Value" />
```

Aby zmienić zdarzenie używane dla powiązania, użyj `@bind:event` atrybutu.

```razor
<input @bind="text" @bind:event="oninput" />
<p>@text</p>

@code {
    string text;
}
```

Składniki mogą również obsługiwać powiązanie danych z parametrami. Aby powiązać dane, zdefiniuj parametr wywołania zwrotnego zdarzenia o takiej samej nazwie jak parametr możliwy do powiązania. Sufiks "zmieniony" został dodany do nazwy.

*PasswordBox. Razor*

```razor
Password: <input
    value="@Password"
    @oninput="OnPasswordChanged"
    type="@(showPassword ? "text" : "password")" />

<label><input type="checkbox" @bind="showPassword" />Show password</label>

@code {
    private bool showPassword;

    [Parameter]
    public string Password { get; set; }

    [Parameter]
    public EventCallback<string> PasswordChanged { get; set; }

    private Task OnPasswordChanged(ChangeEventArgs e)
    {
        Password = e.Value.ToString();
        return PasswordChanged.InvokeAsync(Password);
    }
}
```

Aby połączyć dane z podstawowym elementem interfejsu użytkownika, należy ustawić wartość i obsłużyć zdarzenie bezpośrednio dla elementu interfejsu użytkownika zamiast używać `@bind` atrybutu.

Aby powiązać z parametrem składnika, użyj `@bind-{Parameter}` atrybutu, aby określić parametr, do którego chcesz utworzyć powiązanie.

```razor
<PasswordBox @bind-Password="password" />

@code {
    string password;
}
```

## <a name="state-changes"></a>Zmiany stanu

Jeśli stan składnika uległ zmianie poza normalnym zdarzeniem interfejsu użytkownika lub wywołaniem zwrotnym zdarzenia, składnik musi ręcznie sygnalizować, że musi być renderowany ponownie. Aby sygnalizować zmianę stanu składnika, wywołaj `StateHasChanged` metodę w składniku.

W poniższym przykładzie składnik wyświetla komunikat z `AppState` usługi, którą można zaktualizować za pomocą innych części aplikacji. Składnik rejestruje `StateHasChanged` metodę ze `AppState.OnChange` zdarzeniem, aby składnik był renderowany za każdym razem, gdy komunikat zostanie zaktualizowany.

```csharp
public class AppState
{
    public string Message { get; }

    // Lets components receive change notifications
    public event Action OnChange;

    public void UpdateMessage(string message)
    {
        Message = message;
        NotifyStateChanged();
    }

    private void NotifyStateChanged() => OnChange?.Invoke();
}
```

```razor
@inject AppState AppState

<p>App message: @AppState.Message</p>

@code {
    protected override void OnInitialized()
    {
        AppState.OnChange += StateHasChanged
    }
}
```

## <a name="component-lifecycle"></a>Cykl życia składnika

Struktura formularzy sieci Web ASP.NET ma dobrze zdefiniowane metody cyklu życia dla modułów, stron i kontrolek. Na przykład poniższy formant implementuje programy obsługi zdarzeń dla `Init` `Load` zdarzeń, i `UnLoad` cyklu życia:

*Counter.ascx.cs*

```csharp
public partial class Counter : System.Web.UI.UserControl
{
    protected void Page_Init(object sender, EventArgs e) { ... }
    protected void Page_Load(object sender, EventArgs e) { ... }
    protected void Page_UnLoad(object sender, EventArgs e) { ... }
}
```

Blazor składniki mają również dobrze zdefiniowany cykl życia. Cykl życia składnika może służyć do inicjowania stanu składnika i implementowania zaawansowanych zachowań składników.

Wszystkie Blazor metody cyklu życia składników są dostępne zarówno w wersji synchronicznej, jak i asynchronicznej. Renderowanie składnika jest synchroniczne. Nie można uruchomić logiki asynchronicznej jako części renderowania składnika. Wszystkie logiki asynchroniczne muszą zostać wykonane w ramach `async` metody cyklu życia.

### <a name="oninitialized"></a>OnInitialized

`OnInitialized`Metody i `OnInitializedAsync` są używane do inicjowania składnika. Składnik jest zazwyczaj inicjowany po pierwszym renderowaniu. Po zainicjowaniu składnika można go renderować wiele razy, zanim zostanie ostatecznie usunięty. `OnInitialized`Metoda jest podobna do `Page_Load` zdarzenia na stronach i formantach formularzy sieci Web ASP.NET.

```csharp
protected override void OnInitialized() { ... }
protected override async Task OnInitializedAsync() { await ... }
```

### <a name="onparametersset"></a>OnParametersSet

`OnParametersSet`Metody i `OnParametersSetAsync` są wywoływane, gdy składnik otrzymał parametry z jego elementu nadrzędnego, a wartość jest przypisana do właściwości. Te metody są wykonywane po zainicjowaniu składnika i za *każdym razem, gdy składnik jest renderowany*.

```csharp
protected override void OnParametersSet() { ... }
protected override async Task OnParametersSetAsync() { await ... }
```

### <a name="onafterrender"></a>OnAfterRender

`OnAfterRender`Metody i `OnAfterRenderAsync` są wywoływane po zakończeniu renderowania składnika. Odwołania do elementów i składników są wypełniane w tym punkcie (więcej informacji znajduje się poniżej). W tym momencie jest włączona funkcja interaktywność z przeglądarką. Interakcje z obsługą DOM i wykonanie kodu JavaScript mogą być bezpiecznie wykonywane.

```csharp
protected override void OnAfterRender(bool firstRender)
{
    if (firstRender)
    {
        ...
    }
}
protected override async Task OnAfterRenderAsync(bool firstRender)
{
    if (firstRender)
    {
        await ...
    }
}
```

`OnAfterRender` i `OnAfterRenderAsync` *nie są wywoływane podczas renderowania na serwerze*.

`firstRender`Parametr jest `true` przy pierwszym renderowaniu składnika; w przeciwnym razie jego wartość to `false` .

### <a name="idisposable"></a>IDisposable

Blazor składniki można zaimplementować `IDisposable` do usuwania zasobów, gdy składnik zostanie usunięty z interfejsu użytkownika. Składnik Razor można zaimplementować przy `IDispose` użyciu `@implements` dyrektywy:

```razor
@using System
@implements IDisposable

...

@code {
    public void Dispose()
    {
        ...
    }
}
```

## <a name="capture-component-references"></a>Przechwyć odwołania do składników

W programie ASP.NET Web Forms często można manipulować wystąpieniem formantu bezpośrednio w kodzie, odwołując się do jego identyfikatora. W programie Blazor możliwe jest również przechwytywanie i manipulowanie odwołaniem do składnika, chociaż jest to znacznie mniej typowe.

Aby przechwycić odwołanie do składnika w programie Blazor , należy użyć `@ref` atrybutu dyrektywy. Wartość atrybutu powinna być zgodna z nazwą pola settable o tym samym typie co składnik, do którego się odwołuje.

```razor
<MyLoginDialog @ref="loginDialog" ... />

@code {
    MyLoginDialog loginDialog;

    void OnSomething()
    {
        loginDialog.Show();
    }
}
```

Gdy składnik nadrzędny jest renderowany, pole zostanie wypełnione wystąpieniem składnika podrzędnego. Następnie można wywołać metody lub w inny sposób manipulować wystąpieniem składnika.

Manipulowanie stanem składnika bezpośrednio przy użyciu odwołań do składników nie jest zalecane. Uniemożliwia to automatyczne renderowanie składnika w prawidłowym czasie.

## <a name="capture-element-references"></a>Przechwyć odwołania do elementów

Blazor składniki mogą przechwytywać odwołania do elementu. W przeciwieństwie do kontrolek serwera HTML w formularzach sieci Web ASP.NET nie można manipulować modelem DOM bezpośrednio przy użyciu odwołania do elementu w Blazor . Blazor obsługuje większość interakcji z modelem DOM przy użyciu algorytmu różnicowania modelu DOM. Przechwycone odwołania do elementów w programie Blazor są nieprzezroczyste. Są one jednak używane do przekazywania określonego odwołania do elementu w wywołaniu JavaScript Interop. Aby uzyskać więcej informacji na temat międzyoperacyjności języka JavaScript, zobacz [ASP.NET Core Blazor międzyoperacyjności JavaScript](/aspnet/core/blazor/javascript-interop).

## <a name="templated-components"></a>Składniki z szablonami

W formularzach sieci Web ASP.NET można tworzyć *kontrolki z szablonami*. Kontrolki z szablonami umożliwiają deweloperowi określenie fragmentu kodu HTML służącego do renderowania kontrolki kontenera. Mechanics kompilowania formantów serwera są złożone, ale zapewniają zaawansowane scenariusze renderowania danych w sposób dostosowywalny przez użytkownika. Przykłady formantów z szablonami obejmują `Repeater` i `DataList` .

Blazor składniki można także definiować za pomocą definiowania parametrów składnika typu `RenderFragment` lub `RenderFragment<T>` . `RenderFragment`Reprezentuje fragment znacznika Razor, który będzie następnie renderowany przez składnik. A `RenderFragment<T>` to fragment znacznika Razor, który przyjmuje parametr, który można określić podczas renderowania fragmentu renderowania.

### <a name="child-content"></a>Zawartość podrzędna

Blazor składniki mogą przechwytywać zawartość podrzędną jako `RenderFragment` i renderować tę zawartość w ramach renderowania składników. Aby przechwycić zawartość podrzędną, zdefiniuj parametr składnika typu `RenderFragment` i nadaj mu nazwę `ChildContent` .

*ChildContentComponent. Razor*

```razor
<h1>Component with child content</h1>

<div>@ChildContent</div>

@code {
    [Parameter]
    public RenderFragment ChildContent { get; set; }
}
```

Składnik nadrzędny może następnie dostarczyć zawartość podrzędną przy użyciu normalnego składnia Razor.

```razor
<ChildContentComponent>
    <ChildContent>
        <p>The time is @DateTime.Now</p>
    </ChildContent>
</ChildContentComponent>
```

### <a name="template-parameters"></a>Parametry szablonu

BlazorSkładnik szablonu może również definiować wiele parametrów składnika typu `RenderFragment` lub `RenderFragment<T>` . Parametr dla elementu `RenderFragment<T>` można określić, gdy jest wywoływany. Aby określić parametr typu ogólnego dla składnika, użyj `@typeparam` dyrektywy Razor.

*SimpleListView. Razor*

```razor
@typeparam TItem

@Heading

<ul>
@foreach (var item in Items)
{
    <li>@ItemTemplate(item)</li>
}
</ul>

@code {
    [Parameter]
    public RenderFragment Heading { get; set; }

    [Parameter]
    public RenderFragment<TItem> ItemTemplate { get; set; }

    [Parameter]
    public IEnumerable<TItem> Items { get; set; }
}
```

W przypadku korzystania z składnika z szablonem parametry szablonu można określić za pomocą elementów podrzędnych, które pasują do nazw parametrów. Argumenty składnika typu `RenderFragment<T>` przekazane jako elementy mają niejawny parametr o nazwie `context` . Nazwę tego parametru implementacji można zmienić przy użyciu `Context` atrybutu elementu podrzędnego. Wszystkie parametry typu ogólnego można określić przy użyciu atrybutu, który jest zgodny z nazwą parametru typu. Parametr typu zostanie wywnioskowany, jeśli jest to możliwe:

```razor
<SimpleListView Items="messages" TItem="string">
    <Heading>
        <h1>My list</h1>
    </Heading>
    <ItemTemplate Context="message">
        <p>The message is: @message</p>
    </ItemTemplate>
</SimpleListView>
```

Dane wyjściowe tego składnika wyglądają następująco:

```html
<h1>My list</h1>
<ul>
    <li><p>The message is: message1</p></li>
    <li><p>The message is: message2</p></li>
<ul>
```

## <a name="code-behind"></a>Związane z kodem

BlazorSkładnik jest zwykle tworzony w jednym pliku *Razor* . Można jednak również oddzielić kod i znaczniki przy użyciu pliku związanego z kodem. Aby użyć pliku składnika, Dodaj plik C#, który jest zgodny z nazwą pliku składnika, ale z dodaniem rozszerzenia *CS* (*Counter.Razor.cs*). Użyj pliku C#, aby zdefiniować klasę bazową dla składnika. Można nazwać klasę bazową w dowolnym celu, ale jest ona wspólna dla nazwy klasy, która jest taka sama jak Klasa składnika, ale z `Base` dodanym rozszerzeniem ( `CounterBase` ). Klasa oparta na składnikach musi również pochodzić od `ComponentBase` . Następnie w pliku składnika Razor Dodaj `@inherits` dyrektywę, aby określić klasę bazową składnika ( `@inherits CounterBase` ).

*Counter. Razor*

```razor
@inherits CounterBase

<h1>Counter</h1>

<p>Current count: @currentCount</p>

<button @onclick="IncrementCount">Click me</button>
```

*Counter.razor.cs*

```csharp
public class CounterBase : ComponentBase
{
    protected int currentCount = 0;

    protected void IncrementCount()
    {
        currentCount++;
    }
}
```

Widoczność elementów członkowskich składnika w klasie bazowej musi być `protected` lub `public` widoczna dla klasy składnika.

## <a name="additional-resources"></a>Zasoby dodatkowe

Powyższe nie jest wyczerpujące dla wszystkich aspektów Blazor składników. Aby uzyskać więcej informacji na temat [tworzenia i używania ASP.NET Core składników Razor](/aspnet/core/blazor/components), zobacz Blazor dokumentację.

>[!div class="step-by-step"]
>[Poprzedni](app-startup.md) 
> [Dalej](pages-routing-layouts.md)
