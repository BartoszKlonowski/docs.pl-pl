---
title: Strony, routing i układy
description: Dowiedz się, jak tworzyć strony w programie Blazor , korzystać z routingu po stronie klienta i zarządzać układami stron.
author: danroth27
ms.author: daroth
no-loc:
- Blazor
ms.date: 09/19/2019
ms.openlocfilehash: 714ba0be7c2014895a75250a47e6ce448863eb6c
ms.sourcegitcommit: 0100be20fcf23f61dab672deced70059ed71bb2e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/17/2020
ms.locfileid: "88267792"
---
# <a name="pages-routing-and-layouts"></a>Strony, routing i układy

Aplikacje ASP.NET Web Forms składają się ze stron zdefiniowanych w plikach *. aspx* . Adres każdej strony jest oparty na fizycznej ścieżce pliku w projekcie. Gdy przeglądarka wysyła żądanie do strony, zawartość strony jest dynamicznie renderowana na serwerze. Konta renderowania zarówno dla znacznika HTML strony, jak i jego formantów serwerowych.

W programie Blazor każda Strona w aplikacji jest składnikiem, zazwyczaj zdefiniowanym w pliku *. Razor* , z co najmniej jedną określoną trasą. Routing głównie odbywa się po stronie klienta bez udziału określonego żądania serwera. Przeglądarka najpierw wysyła żądanie do adresu głównego aplikacji. Składnik główny `Router` w aplikacji, Blazor a następnie obsługuje przechwycone żądania nawigacji i są do poprawnego składnika.

Blazor obsługuje również *głębokie łączenie*. Głębokie łączenie występuje, gdy przeglądarka wysyła żądanie do określonej trasy innej niż główna aplikacji. Żądania linków bezpośrednich wysyłanych do serwera są kierowane do Blazor aplikacji, która następnie kieruje żądanie po stronie klienta do właściwego składnika.

Prosta strona w formularzach sieci Web ASP.NET może zawierać następujące znaczniki:

*Nazwa. aspx*

```aspx-csharp
<%@ Page Title="Name" Language="C#" MasterPageFile="~/Site.Master" AutoEventWireup="true" CodeBehind="Name.aspx.cs" Inherits="WebApplication1.Name" %>

<asp:Content ID="BodyContent" ContentPlaceHolderID="MainContent" runat="server">
    <div>
        What is your name?<br />
        <asp:TextBox ID="TextBox1" runat="server"></asp:TextBox>
        <asp:Button ID="Button1" runat="server" Text="Submit" OnClick="Button1_Click" />
    </div>
    <div>
        <asp:Literal ID="Literal1" runat="server" />
    </div>
</asp:Content>
```

*Name.aspx.cs*

```csharp
public partial class Name : System.Web.UI.Page
{
    protected void Button1_Click1(object sender, EventArgs e)
    {
        Literal1.Text = "Hello " + TextBox1.Text;
    }
}
```

Odpowiednik strony w Blazor aplikacji będzie wyglądać następująco:

*Nazwa. Razor*

```razor
@page "/Name"
@layout MainLayout

<div>
    What is your name?<br />
    <input @bind="text" />
    <button @onclick="OnClick">Submit</button>
</div>
<div>
    @if (name != null)
    {
        @:Hello @name
    }
</div>

@code {
    string text;
    string name;

    void OnClick() {
        name = text;
    }
}
```

## <a name="create-pages"></a>Tworzenie stron

Aby utworzyć stronę w programie Blazor , Utwórz składnik i Dodaj `@page` dyrektywę Razor, aby określić trasę dla składnika. `@page`Dyrektywa przyjmuje jeden parametr, który jest szablonem trasy do dodania do tego składnika.

```razor
@page "/counter"
```

Wymagany jest parametr szablonu trasy. W przeciwieństwie do ASP.NET formularzy sieci Web, trasy do Blazor składnika *nie są* wywnioskowane z jego lokalizacji pliku (chociaż może to być funkcja dodana w przyszłości).

Składnia szablonu trasy jest tą samą składnią podstawową używaną do routingu w ASP.NET Web Forms. Parametry trasy są określone w szablonie za pomocą nawiasów klamrowych. Blazor spowoduje powiązanie wartości tras z parametrami składnika o tej samej nazwie (bez uwzględniania wielkości liter).

```razor
@page "/product/{id}"

<h1>Product @Id</h1>

@code {
    [Parameter]
    public string Id { get; set; }
}
```

Można również określić ograniczenia dotyczące wartości parametru trasy. Na przykład, aby ograniczyć identyfikator produktu do `int` :

```razor
@page "/product/{id:int}"

<h1>Product @Id</h1>

@code {
    [Parameter]
    public int Id { get; set; }
}
```

Pełną listę ograniczeń trasy obsługiwanych przez Blazor program można znaleźć w temacie [ograniczenia trasy](/aspnet/core/blazor/routing#route-constraints).

## <a name="router-component"></a>Składnik routera

Routing w programie Blazor jest obsługiwany przez `Router` składnik. `Router`Składnik jest zazwyczaj używany w głównym składniku aplikacji (*App. Razor*).

```razor
<Router AppAssembly="@typeof(Program).Assembly">
    <Found Context="routeData">
        <RouteView RouteData="@routeData" DefaultLayout="@typeof(MainLayout)" />
    </Found>
    <NotFound>
        <LayoutView Layout="@typeof(MainLayout)">
            <p>Sorry, there's nothing at this address.</p>
        </LayoutView>
    </NotFound>
</Router>
```

`Router`Składnik odnajduje składniki routingu w określonym `AppAssembly` i opcjonalnie określony `AdditionalAssemblies` . Gdy przeglądarka nawiguje, `Router` przechwytuje nawigację i renderuje zawartość `Found` parametru z wyodrębnionym, `RouteData` Jeśli trasa pasuje do adresu, w przeciwnym razie `Router` renderuje swój `NotFound` parametr.

`RouteView`Składnik obsługuje renderowanie dopasowanego składnika określonego przez `RouteData` jego układ, jeśli go zawiera. Jeśli dopasowany składnik nie ma układu, `DefaultLayout` jest używany opcjonalnie określony.

`LayoutView`Składnik renderuje jego zawartość podrzędną w ramach określonego układu. W dalszej części tego rozdziału przejdziemy do bardziej szczegółowych informacji o układach.

## <a name="navigation"></a>Nawigacja

W formularzach sieci Web ASP.NET można wyzwolić nawigację do innej strony, zwracając odpowiedź przekierowania do przeglądarki. Na przykład:

```csharp
protected void NavigateButton_Click(object sender, EventArgs e)
{
    Response.Redirect("Counter");
}
```

Zwracanie odpowiedzi przekierowania nie jest zazwyczaj możliwe w Blazor . Blazor nie używa modelu żądanie-odpowiedź. Można jednak bezpośrednio wyzwalać nawigację przeglądarki, podobnie jak w przypadku języka JavaScript.

Blazor zapewnia `NavigationManager` usługę, która może służyć do:

- Pobierz bieżący adres przeglądarki
- Pobierz adres podstawowy
- Wywołaj nawigację
- Otrzymuj powiadomienia o zmianie adresu

Aby przejść do innego adresu, użyj `NavigateTo` metody:

```razor
@page "/"
@inject NavigationManager NavigationManager

<button @onclick="Navigate">Navigate</button>

@code {
    void Navigate() {
        NavigationManager.NavigateTo("counter");
    }
}
```

Aby uzyskać opis wszystkich `NavigationManager` członków, zobacz [identyfikatory URI i pomocnika stanu nawigacji](/aspnet/core/blazor/routing#uri-and-navigation-state-helpers).

## <a name="base-urls"></a>Podstawowe adresy URL

Jeśli Blazor aplikacja jest wdrażana w ścieżce podstawowej, należy określić podstawowy adres URL w metadanych strony przy użyciu `<base>` tagu dla właściwości Routing do Work. Jeśli strona hosta dla aplikacji jest renderowana na serwerze przy użyciu Razor, można użyć `~/` składni, aby określić adres podstawowy aplikacji. Jeśli strona hosta jest statycznym kodem HTML, należy jawnie określić podstawowy adres URL.

```html
<base href="~/" />
```

## <a name="page-layout"></a>Układ strony

Układ strony w formularzach sieci Web ASP.NET jest obsługiwany przez strony główne. Strony wzorcowe definiują szablon z co najmniej jednym symbolem zastępczym zawartości, który może zostać dostarczony przez poszczególne strony. Strony wzorcowe są zdefiniowane w plikach *. Master* i zaczynają się od `<%@ Master %>` dyrektywy. Zawartość plików *. Master* jest zakodowana w taki sam sposób, jak na stronie *. aspx* , ale przy dodawaniu `<asp:ContentPlaceHolder>` kontrolek do oznaczania, gdzie strony mogą dostarczać zawartość.

*Site.master*

```aspx-csharp
<%@ Master Language="C#" AutoEventWireup="true" CodeBehind="Site.master.cs" Inherits="WebApplication1.SiteMaster" %>

<!DOCTYPE html>
<html lang="en">
<head runat="server">
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title><%: Page.Title %> - My ASP.NET Application</title>
    <link href="~/favicon.ico" rel="shortcut icon" type="image/x-icon" />
</head>
<body>
    <form runat="server">
        <div class="container body-content">
            <asp:ContentPlaceHolder ID="MainContent" runat="server">
            </asp:ContentPlaceHolder>
            <hr />
            <footer>
                <p>&copy; <%: DateTime.Now.Year %> - My ASP.NET Application</p>
            </footer>
        </div>
    </form>
</body>
</html>
```

W programie Blazor Obsługa układu strony przy użyciu składników układu. Składniki układu dziedziczą z `LayoutComponentBase` , który definiuje pojedynczą `Body` Właściwość typu `RenderFragment` , która może służyć do renderowania zawartości strony.

*MainLayout. Razor*

```razor
@inherits LayoutComponentBase
<h1>Main layout</h1>
<div>
    @Body
</div>
```

Gdy jest renderowany Strona z układem, strona jest renderowana w obrębie zawartości określonego układu w lokalizacji, w której układ renderuje swoją `Body` Właściwość.

Aby zastosować układ do strony, użyj `@layout` dyrektywy:

```razor
@layout MainLayout
```

Można określić układ wszystkich składników w folderze i podfolderach przy użyciu pliku *_Imports. Razor* . Możesz również określić układ domyślny dla wszystkich stron przy użyciu [składnika routera](#router-component).

Strony wzorcowe mogą definiować wiele symboli zastępczych zawartości, ale układy w programie Blazor mają tylko jedną `Body` Właściwość. To ograniczenie Blazor komponentów układu będzie miejmy nadzieję w przyszłej wersji.

Strony wzorcowe w formularzach sieci Web ASP.NET mogą być zagnieżdżane. Oznacza to, że strona wzorcowa może również korzystać z strony wzorcowej. Składniki układu w programie Blazor mogą być również zagnieżdżone. Można zastosować składnik układu do składnika układu. Zawartość układu wewnętrznego będzie renderowana w układzie zewnętrznym.

*ChildLayout. Razor*

```razor
@layout MainLayout
<h2>Child layout</h2>
<div>
    @Body
</div>
```

*Index. Razor*

```razor
@page "/"
@layout ChildLayout
<p>I'm in a nested layout!</p>
```

Wyrenderowane dane wyjściowe dla strony byłyby następujące:

```html
<h1>Main layout</h1>
<div>
    <h2>Child layout</h2>
    <div>
        <p>I'm in a nested layout!</p>
    </div>
</div>
```

Układy w programie Blazor nie definiują zwykle elementów głównych HTML dla strony ( `<html>` , `<body>` ,, itd `<head>` .). Elementy głównego pliku HTML są definiowane na Blazor stronie hosta aplikacji, która jest używana do renderowania początkowej zawartości HTML dla aplikacji (zobacz [Bootstrap Blazor ](project-structure.md#bootstrap-blazor)). Na stronie hosta można renderować wiele składników głównych aplikacji z otaczającym znacznikiem.

Składniki programu Blazor , w tym strony, nie mogą renderować `<script>` tagów. To ograniczenie renderowania istnieje `<script>` , ponieważ Tagi są ładowane jednokrotnie, a następnie nie można ich zmienić. Jeśli spróbujesz renderować Tagi dynamicznie przy użyciu składnia Razor, może wystąpić nieoczekiwane zachowanie. Zamiast tego należy `<script>` dodać wszystkie Tagi do strony hosta aplikacji.

>[!div class="step-by-step"]
>[Poprzedni](components.md) 
> [Dalej](state-management.md)
