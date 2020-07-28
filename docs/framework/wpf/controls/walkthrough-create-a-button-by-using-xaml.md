---
title: 'Wskazówki: Tworzenie przycisku przy użyciu XAML'
description: Skorzystaj z tego przewodnika, aby dowiedzieć się, jak utworzyć animowany przycisk do użycia w aplikacji Windows Presentation Foundation przy użyciu języka XAML.
ms.date: 03/30/2017
helpviewer_keywords:
- buttons [WPF]
ms.assetid: 138c41c4-1759-4bbf-8d77-77031a06a8a0
ms.openlocfilehash: 136d1ad5d6fefd70f0d977e5287ae75f06c52d36
ms.sourcegitcommit: 87cfeb69226fef01acb17c56c86f978f4f4a13db
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/24/2020
ms.locfileid: "87164848"
---
# <a name="walkthrough-create-a-button-by-using-xaml"></a><span data-ttu-id="83a11-103">Wskazówki: Tworzenie przycisku przy użyciu XAML</span><span class="sxs-lookup"><span data-stu-id="83a11-103">Walkthrough: Create a Button by Using XAML</span></span>

<span data-ttu-id="83a11-104">Celem tego instruktażu jest nauczenie się, jak utworzyć animowany przycisk do użycia w aplikacji Windows Presentation Foundation (WPF).</span><span class="sxs-lookup"><span data-stu-id="83a11-104">The objective of this walkthrough is to learn how to create an animated button for use in a Windows Presentation Foundation (WPF) application.</span></span> <span data-ttu-id="83a11-105">W tym instruktażu zastosowano style i szablon w celu utworzenia niestandardowego zasobu przycisku, który umożliwia ponowne użycie kodu i rozdzielenie logiki przycisku z deklaracji przycisku.</span><span class="sxs-lookup"><span data-stu-id="83a11-105">This walkthrough uses styles and a template to create a customized button resource that allows reuse of code and separation of button logic from the button declaration.</span></span> <span data-ttu-id="83a11-106">Ten Instruktaż jest zapisywana w całości w [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] .</span><span class="sxs-lookup"><span data-stu-id="83a11-106">This walkthrough is written entirely in [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="83a11-107">Ten przewodnik przeprowadzi Cię przez kroki tworzenia aplikacji przez wpisanie lub skopiowanie i wklejenie [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] do programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="83a11-107">This walkthrough guides you through the steps for creating the application by typing or copying and pasting [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] into Visual Studio.</span></span> <span data-ttu-id="83a11-108">Jeśli wolisz dowiedzieć się, jak używać projektanta do tworzenia tej samej aplikacji, zobacz [Tworzenie przycisku przy użyciu programu Microsoft Expression Blend](walkthrough-create-a-button-by-using-microsoft-expression-blend.md).</span><span class="sxs-lookup"><span data-stu-id="83a11-108">If you would prefer to learn how to use a designer to create the same application, see [Create a Button by Using Microsoft Expression Blend](walkthrough-create-a-button-by-using-microsoft-expression-blend.md).</span></span>

<span data-ttu-id="83a11-109">Na poniższej ilustracji przedstawiono gotowe przyciski.</span><span class="sxs-lookup"><span data-stu-id="83a11-109">The following figure shows the finished buttons.</span></span>

<span data-ttu-id="83a11-110">![Przyciski niestandardowe, które zostały utworzone przy użyciu języka XAML](./media/custom-button-animatedbutton-5.gif "custom_button_AnimatedButton_5")</span><span class="sxs-lookup"><span data-stu-id="83a11-110">![Custom buttons that were created by using XAML](./media/custom-button-animatedbutton-5.gif "custom_button_AnimatedButton_5")</span></span>

## <a name="create-basic-buttons"></a><span data-ttu-id="83a11-111">Utwórz podstawowe przyciski</span><span class="sxs-lookup"><span data-stu-id="83a11-111">Create Basic Buttons</span></span>

<span data-ttu-id="83a11-112">Zacznijmy od utworzenia nowego projektu i dodania do okna kilku przycisków.</span><span class="sxs-lookup"><span data-stu-id="83a11-112">Let's start by creating a new project and adding a few buttons to the window.</span></span>

### <a name="to-create-a-new-wpf-project-and-add-buttons-to-the-window"></a><span data-ttu-id="83a11-113">Aby utworzyć nowy projekt WPF i dodać przyciski do okna</span><span class="sxs-lookup"><span data-stu-id="83a11-113">To create a new WPF project and add buttons to the window</span></span>

1. <span data-ttu-id="83a11-114">Uruchom program Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="83a11-114">Start Visual Studio.</span></span>

2. <span data-ttu-id="83a11-115">**Utwórz nowy projekt WPF:** W menu **plik** wskaż polecenie **Nowy**, a następnie kliknij pozycję **projekt**.</span><span class="sxs-lookup"><span data-stu-id="83a11-115">**Create a new WPF project:** On the **File** menu, point to **New**, and then click **Project**.</span></span> <span data-ttu-id="83a11-116">Znajdź szablon **aplikacji systemu Windows (WPF)** i Nadaj projektowi nazwę "AnimatedButton".</span><span class="sxs-lookup"><span data-stu-id="83a11-116">Find the **Windows Application (WPF)** template and name the project "AnimatedButton".</span></span> <span data-ttu-id="83a11-117">Spowoduje to utworzenie szkieletu dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="83a11-117">This will create the skeleton for the application.</span></span>

3. <span data-ttu-id="83a11-118">**Dodaj podstawowe przyciski domyślne:** Wszystkie pliki potrzebne do tego przewodnika są udostępniane przez szablon.</span><span class="sxs-lookup"><span data-stu-id="83a11-118">**Add basic default buttons:** All the files you need for this walkthrough are provided by the template.</span></span> <span data-ttu-id="83a11-119">Otwórz plik window1. XAML, klikając go dwukrotnie w Eksplorator rozwiązań.</span><span class="sxs-lookup"><span data-stu-id="83a11-119">Open the Window1.xaml file by double clicking it in Solution Explorer.</span></span> <span data-ttu-id="83a11-120">Domyślnie istnieje <xref:System.Windows.Controls.Grid> element w window1. XAML.</span><span class="sxs-lookup"><span data-stu-id="83a11-120">By default, there is a <xref:System.Windows.Controls.Grid> element in Window1.xaml.</span></span> <span data-ttu-id="83a11-121">Usuń <xref:System.Windows.Controls.Grid> element i Dodaj do strony kilka przycisków [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] , wpisując lub kopiując i wklejając następujący wyróżniony kod do window1. XAML:</span><span class="sxs-lookup"><span data-stu-id="83a11-121">Remove the <xref:System.Windows.Controls.Grid> element and add a few buttons to the [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] page by typing or copy and pasting the following highlighted code to Window1.xaml:</span></span>

    ```xaml
    <Window x:Class="AnimatedButton.Window1"
      xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
      xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
      Title="AnimatedButton" Height="300" Width="300"
      Background="Black">
      <!-- Buttons arranged vertically inside a StackPanel. -->
      <StackPanel HorizontalAlignment="Left">
          <Button>Button 1</Button>
          <Button>Button 2</Button>
          <Button>Button 3</Button>
      </StackPanel>
    </Window>
    ```

     <span data-ttu-id="83a11-122">Naciśnij klawisz F5, aby uruchomić aplikację. powinien pojawić się zestaw przycisków, które wyglądają jak na poniższej ilustracji.</span><span class="sxs-lookup"><span data-stu-id="83a11-122">Press F5 to run the application; you should see a set of buttons that looks like the following figure.</span></span>

     <span data-ttu-id="83a11-123">![Trzy podstawowe przyciski](./media/custom-button-animatedbutton-1.gif "custom_button_AnimatedButton_1")</span><span class="sxs-lookup"><span data-stu-id="83a11-123">![Three basic buttons](./media/custom-button-animatedbutton-1.gif "custom_button_AnimatedButton_1")</span></span>

     <span data-ttu-id="83a11-124">Teraz, gdy utworzono podstawowe przyciski, zakończysz pracę w pliku window1. XAML.</span><span class="sxs-lookup"><span data-stu-id="83a11-124">Now that you have created the basic buttons, you are finished working in the Window1.xaml file.</span></span> <span data-ttu-id="83a11-125">Pozostała część przewodnika koncentruje się na pliku App. XAML, definiowaniu stylów i szablonie przycisków.</span><span class="sxs-lookup"><span data-stu-id="83a11-125">The rest of the walkthrough focuses on the app.xaml file, defining styles and a template for the buttons.</span></span>

## <a name="set-basic-properties"></a><span data-ttu-id="83a11-126">Ustaw właściwości podstawowe</span><span class="sxs-lookup"><span data-stu-id="83a11-126">Set Basic Properties</span></span>

<span data-ttu-id="83a11-127">Następnie Skonfigurujmy niektóre właściwości na tych przyciskach, aby kontrolować wygląd i układ przycisku.</span><span class="sxs-lookup"><span data-stu-id="83a11-127">Next, let's set some properties on these buttons to control the button appearance and layout.</span></span> <span data-ttu-id="83a11-128">Zamiast ustawiania właściwości na przyciskach indywidualnie, użyjesz zasobów do definiowania właściwości przycisku dla całej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="83a11-128">Rather than setting properties on the buttons individually, you will use resources to define button properties for the entire application.</span></span> <span data-ttu-id="83a11-129">Zasoby aplikacji są koncepcyjnie podobne do zewnętrznych kaskadowe arkusze stylów (CSS) dla stron sieci Web; jednak zasoby są znacznie bardziej wydajne niż kaskadowe arkusze stylów (CSS), jak widać na końcu tego instruktażu.</span><span class="sxs-lookup"><span data-stu-id="83a11-129">Application resources are conceptually similar to external Cascading Style Sheets (CSS) for Web pages; however, resources are much more powerful than Cascading Style Sheets (CSS), as you will see by the end of this walkthrough.</span></span> <span data-ttu-id="83a11-130">Aby dowiedzieć się więcej o zasobach, zobacz [zasoby XAML](../../../desktop-wpf/fundamentals/xaml-resources-define.md).</span><span class="sxs-lookup"><span data-stu-id="83a11-130">To learn more about resources, see [XAML Resources](../../../desktop-wpf/fundamentals/xaml-resources-define.md).</span></span>

### <a name="to-use-styles-to-set-basic-properties-on-the-buttons"></a><span data-ttu-id="83a11-131">Aby użyć stylów do ustawiania podstawowych właściwości na przyciskach</span><span class="sxs-lookup"><span data-stu-id="83a11-131">To use styles to set basic properties on the buttons</span></span>

1. <span data-ttu-id="83a11-132">**Zdefiniuj blok Application. Resources:** Otwórz plik App. XAML i Dodaj następujące wyróżnione znaczniki, jeśli jeszcze tego nie zrobiono:</span><span class="sxs-lookup"><span data-stu-id="83a11-132">**Define an Application.Resources block:** Open app.xaml and add the following highlighted markup if it is not already there:</span></span>

    ```xaml
    <Application x:Class="AnimatedButton.App"
      xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
      xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
      StartupUri="Window1.xaml"
      >
      <Application.Resources>
        <!-- Resources for the entire application can be defined here. -->
      </Application.Resources>
    </Application>
    ```

     <span data-ttu-id="83a11-133">Zakres zasobów jest określany na podstawie tego, gdzie definiujesz zasób.</span><span class="sxs-lookup"><span data-stu-id="83a11-133">Resource scope is determined by where you define the resource.</span></span> <span data-ttu-id="83a11-134">Zdefiniowanie zasobów w `Application.Resources` pliku App. XAML umożliwia użycie zasobu z dowolnego miejsca w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="83a11-134">Defining resources in `Application.Resources` in the app.xaml file enables the resource to be used from anywhere in the application.</span></span> <span data-ttu-id="83a11-135">Aby dowiedzieć się więcej o definiowaniu zakresu zasobów, zobacz [zasoby XAML](../../../desktop-wpf/fundamentals/xaml-resources-define.md).</span><span class="sxs-lookup"><span data-stu-id="83a11-135">To learn more about defining the scope of your resources, see [XAML Resources](../../../desktop-wpf/fundamentals/xaml-resources-define.md).</span></span>

2. <span data-ttu-id="83a11-136">**Utwórz styl i Zdefiniuj dla niego podstawowe wartości właściwości:** Dodaj następujący znacznik do `Application.Resources` bloku.</span><span class="sxs-lookup"><span data-stu-id="83a11-136">**Create a style and define basic property values with it:** Add the following markup to the `Application.Resources` block.</span></span> <span data-ttu-id="83a11-137">Ten znacznik tworzy obiekt <xref:System.Windows.Style> , który dotyczy wszystkich przycisków w aplikacji, ustawienie <xref:System.Windows.FrameworkElement.Width%2A> przycisków na 90 i <xref:System.Windows.FrameworkElement.Margin%2A> do 10:</span><span class="sxs-lookup"><span data-stu-id="83a11-137">This markup creates a <xref:System.Windows.Style> that applies to all buttons in the application, setting the <xref:System.Windows.FrameworkElement.Width%2A> of the buttons to 90 and the <xref:System.Windows.FrameworkElement.Margin%2A> to 10:</span></span>

    ```xaml
    <Application.Resources>
      <Style TargetType="Button">
        <Setter Property="Width" Value="90" />
        <Setter Property="Margin" Value="10" />
      </Style>
    </Application.Resources>
    ```

     <span data-ttu-id="83a11-138"><xref:System.Windows.Style.TargetType%2A>Właściwość określa, że styl dotyczy wszystkich obiektów typu <xref:System.Windows.Controls.Button> .</span><span class="sxs-lookup"><span data-stu-id="83a11-138">The <xref:System.Windows.Style.TargetType%2A> property specifies that the style applies to all objects of type <xref:System.Windows.Controls.Button>.</span></span> <span data-ttu-id="83a11-139">Każda <xref:System.Windows.Setter> z nich ustawia inną wartość właściwości dla <xref:System.Windows.Style> .</span><span class="sxs-lookup"><span data-stu-id="83a11-139">Each <xref:System.Windows.Setter> sets a different property value for the <xref:System.Windows.Style>.</span></span> <span data-ttu-id="83a11-140">W związku z tym, w tym momencie każdy przycisk w aplikacji ma szerokość 90 i margines 10.</span><span class="sxs-lookup"><span data-stu-id="83a11-140">Therefore, at this point every button in the application has a width of 90 and a margin of 10.</span></span>  <span data-ttu-id="83a11-141">Jeśli naciśniesz klawisz F5, aby uruchomić aplikację, zobaczysz następujące okno.</span><span class="sxs-lookup"><span data-stu-id="83a11-141">If you press F5 to run the application, you see the following window.</span></span>

     <span data-ttu-id="83a11-142">![Przyciski o szerokości 90 i marginesie 10](./media/custom-button-animatedbutton-2.gif "custom_button_AnimatedButton_2")</span><span class="sxs-lookup"><span data-stu-id="83a11-142">![Buttons with a width of 90 and a margin of 10](./media/custom-button-animatedbutton-2.gif "custom_button_AnimatedButton_2")</span></span>

     <span data-ttu-id="83a11-143">Istnieje dużo więcej możliwości z stylami, w tym różne sposoby dostosowania obiektów do celów, określania złożonych wartości właściwości, a nawet style jako dane wejściowe dla innych stylów.</span><span class="sxs-lookup"><span data-stu-id="83a11-143">There is much more you can do with styles, including a variety of ways to fine-tune what objects are targeted, specifying complex property values, and even using styles as input for other styles.</span></span> <span data-ttu-id="83a11-144">Aby uzyskać więcej informacji, zobacz [Style i tworzenia szablonów](../../../desktop-wpf/fundamentals/styles-templates-overview.md).</span><span class="sxs-lookup"><span data-stu-id="83a11-144">For more information, see [Styling and Templating](../../../desktop-wpf/fundamentals/styles-templates-overview.md).</span></span>

3. <span data-ttu-id="83a11-145">**Ustaw wartość właściwości styl na zasób:** Zasoby umożliwiają proste użycie często zdefiniowanych obiektów i wartości.</span><span class="sxs-lookup"><span data-stu-id="83a11-145">**Set a style property value to a resource:** Resources enable a simple way to reuse commonly defined objects and values.</span></span> <span data-ttu-id="83a11-146">Jest to szczególnie przydatne do definiowania złożonych wartości przy użyciu zasobów, aby kod był bardziej modularny.</span><span class="sxs-lookup"><span data-stu-id="83a11-146">It is especially useful to define complex values using resources to make your code more modular.</span></span> <span data-ttu-id="83a11-147">Dodaj następujące wyróżnione znaczniki do pliku App. XAML.</span><span class="sxs-lookup"><span data-stu-id="83a11-147">Add the following highlighted markup to app.xaml.</span></span>

    ```xaml
    <Application.Resources>
      <LinearGradientBrush x:Key="GrayBlueGradientBrush" StartPoint="0,0" EndPoint="1,1">
        <GradientStop Color="DarkGray" Offset="0" />
        <GradientStop Color="#CCCCFF" Offset="0.5" />
        <GradientStop Color="DarkGray" Offset="1" />
      </LinearGradientBrush>
      <Style TargetType="{x:Type Button}">
        <Setter Property="Background" Value="{StaticResource GrayBlueGradientBrush}" />
        <Setter Property="Width" Value="80" />
        <Setter Property="Margin" Value="10" />
      </Style>
    </Application.Resources>
    ```

     <span data-ttu-id="83a11-148">Bezpośrednio pod `Application.Resources` blokiem został utworzony zasób o nazwie "GrayBlueGradientBrush".</span><span class="sxs-lookup"><span data-stu-id="83a11-148">Directly under the `Application.Resources` block, you created a resource called "GrayBlueGradientBrush".</span></span> <span data-ttu-id="83a11-149">Ten zasób definiuje gradient poziomy.</span><span class="sxs-lookup"><span data-stu-id="83a11-149">This resource defines a horizontal gradient.</span></span> <span data-ttu-id="83a11-150">Tego zasobu można używać jako wartości właściwości z dowolnego miejsca w aplikacji, w tym do metody ustawiającej style przycisku dla <xref:System.Windows.Controls.Control.Background%2A> właściwości.</span><span class="sxs-lookup"><span data-stu-id="83a11-150">This resource can be used as a property value from anywhere in the application, including inside the button style setter for the <xref:System.Windows.Controls.Control.Background%2A> property.</span></span> <span data-ttu-id="83a11-151">Teraz wszystkie przyciski mają <xref:System.Windows.Controls.Control.Background%2A> wartość właściwości tego gradientu.</span><span class="sxs-lookup"><span data-stu-id="83a11-151">Now, all the buttons have a <xref:System.Windows.Controls.Control.Background%2A> property value of this gradient.</span></span>

     <span data-ttu-id="83a11-152">Naciśnij klawisz F5, aby uruchomić aplikację.</span><span class="sxs-lookup"><span data-stu-id="83a11-152">Press F5 to run the application.</span></span> <span data-ttu-id="83a11-153">Powinien wyglądać podobnie do poniższego.</span><span class="sxs-lookup"><span data-stu-id="83a11-153">It should look like the following.</span></span>

     <span data-ttu-id="83a11-154">![Przyciski z tłem gradientowym](./media/custom-button-animatedbutton-3.gif "custom_button_AnimatedButton_3")</span><span class="sxs-lookup"><span data-stu-id="83a11-154">![Buttons with a gradient background](./media/custom-button-animatedbutton-3.gif "custom_button_AnimatedButton_3")</span></span>

## <a name="create-a-template-that-defines-the-look-of-the-button"></a><span data-ttu-id="83a11-155">Utwórz szablon definiujący wygląd przycisku</span><span class="sxs-lookup"><span data-stu-id="83a11-155">Create a Template That Defines the Look of the Button</span></span>

<span data-ttu-id="83a11-156">W tej sekcji utworzysz szablon, który dostosowuje wygląd przycisku.</span><span class="sxs-lookup"><span data-stu-id="83a11-156">In this section, you create a template that customizes the appearance (presentation) of the button.</span></span> <span data-ttu-id="83a11-157">Prezentacja przycisku składa się z kilku obiektów, w tym prostokątów i innych składników, aby nadać przyciskowi unikatowy wygląd.</span><span class="sxs-lookup"><span data-stu-id="83a11-157">The button presentation is made up of several objects including rectangles and other components to give the button a unique look.</span></span>

<span data-ttu-id="83a11-158">Do tej pory kontrolka wyglądu przycisków w aplikacji została ograniczona do zmiany właściwości przycisku.</span><span class="sxs-lookup"><span data-stu-id="83a11-158">So far, the control of how buttons look in the application has been confined to changing properties of the button.</span></span> <span data-ttu-id="83a11-159">Co zrobić, jeśli chcesz wprowadzić bardziej podstawowe zmiany wyglądu przycisku?</span><span class="sxs-lookup"><span data-stu-id="83a11-159">What if you want to make more radical changes to the button's appearance?</span></span> <span data-ttu-id="83a11-160">Szablony umożliwiają zaawansowaną kontrolę nad prezentacją obiektu.</span><span class="sxs-lookup"><span data-stu-id="83a11-160">Templates enable powerful control over the presentation of an object.</span></span> <span data-ttu-id="83a11-161">Ponieważ szablony mogą być używane w ramach stylów, można zastosować szablon do wszystkich obiektów, do których odnosi się ten styl (w tym instruktażu przycisk).</span><span class="sxs-lookup"><span data-stu-id="83a11-161">Because templates can be used within styles, you can apply a template to all objects that the style applies to (in this walkthrough, the button).</span></span>

### <a name="to-use-the-template-to-define-the-look-of-the-button"></a><span data-ttu-id="83a11-162">Aby użyć szablonu do zdefiniowania wyglądu przycisku</span><span class="sxs-lookup"><span data-stu-id="83a11-162">To use the template to define the look of the button</span></span>

1. <span data-ttu-id="83a11-163">**Skonfiguruj szablon:** Ponieważ formanty takie jak <xref:System.Windows.Controls.Button> ma <xref:System.Windows.Controls.Control.Template%2A> Właściwość, można zdefiniować wartość właściwości szablonu, podobnie jak inne wartości właściwości, które zostały ustawione w <xref:System.Windows.Style> <xref:System.Windows.Setter> .</span><span class="sxs-lookup"><span data-stu-id="83a11-163">**Set up the template:** Because controls like <xref:System.Windows.Controls.Button> have a <xref:System.Windows.Controls.Control.Template%2A> property, you can define the template property value just like the other property values we have set in a <xref:System.Windows.Style> using a <xref:System.Windows.Setter>.</span></span> <span data-ttu-id="83a11-164">Dodaj następujący wyróżniony znacznik do stylu przycisku.</span><span class="sxs-lookup"><span data-stu-id="83a11-164">Add the following highlighted markup to your button style.</span></span>

    ```xaml
    <Application.Resources>
      <LinearGradientBrush x:Key="GrayBlueGradientBrush"
        StartPoint="0,0" EndPoint="1,1">
        <GradientStop Color="DarkGray" Offset="0" />
        <GradientStop Color="#CCCCFF" Offset="0.5" />
        <GradientStop Color="DarkGray" Offset="1" />
      </LinearGradientBrush>
      <Style TargetType="{x:Type Button}">
        <Setter Property="Background" Value="{StaticResource GrayBlueGradientBrush}" />
        <Setter Property="Width" Value="80" />
        <Setter Property="Margin" Value="10" />
        <Setter Property="Template">
          <Setter.Value>
            <!-- The button template is defined here. -->
          </Setter.Value>
        </Setter>
      </Style>
    </Application.Resources>
    ```

2. <span data-ttu-id="83a11-165">**Zmień prezentację przycisku:** W tym momencie należy zdefiniować szablon.</span><span class="sxs-lookup"><span data-stu-id="83a11-165">**Alter button presentation:** At this point, you need to define the template.</span></span> <span data-ttu-id="83a11-166">Dodaj następujący wyróżniony znacznik.</span><span class="sxs-lookup"><span data-stu-id="83a11-166">Add the following highlighted markup.</span></span> <span data-ttu-id="83a11-167">Ten znacznik określa dwa <xref:System.Windows.Shapes.Rectangle> elementy z zaokrąglonymi krawędziami, po których następuje <xref:System.Windows.Controls.DockPanel> .</span><span class="sxs-lookup"><span data-stu-id="83a11-167">This markup specifies two <xref:System.Windows.Shapes.Rectangle> elements with rounded edges, followed by a <xref:System.Windows.Controls.DockPanel>.</span></span> <span data-ttu-id="83a11-168"><xref:System.Windows.Controls.DockPanel>Służy do hostowania <xref:System.Windows.Controls.ContentPresenter> przycisku.</span><span class="sxs-lookup"><span data-stu-id="83a11-168">The <xref:System.Windows.Controls.DockPanel> is used to host the <xref:System.Windows.Controls.ContentPresenter> of the button.</span></span> <span data-ttu-id="83a11-169">A <xref:System.Windows.Controls.ContentPresenter> wyświetla zawartość przycisku.</span><span class="sxs-lookup"><span data-stu-id="83a11-169">A <xref:System.Windows.Controls.ContentPresenter> displays the content of the button.</span></span> <span data-ttu-id="83a11-170">W tym instruktażu zawartość jest tekstem ("Button 1", "Button 2", "Button 3").</span><span class="sxs-lookup"><span data-stu-id="83a11-170">In this walkthrough, the content is text ("Button 1", "Button 2", "Button 3").</span></span> <span data-ttu-id="83a11-171">Wszystkie składniki szablonu (prostokąty i <xref:System.Windows.Controls.DockPanel> ) są określone w obrębie <xref:System.Windows.Controls.Grid> .</span><span class="sxs-lookup"><span data-stu-id="83a11-171">All of the template components (the rectangles and the <xref:System.Windows.Controls.DockPanel>) are laid out inside of a <xref:System.Windows.Controls.Grid>.</span></span>

    ```xaml
    <Setter.Value>
      <ControlTemplate TargetType="Button">
        <Grid Width="{TemplateBinding Width}" Height="{TemplateBinding Height}" ClipToBounds="True">
          <!-- Outer Rectangle with rounded corners. -->
          <Rectangle x:Name="outerRectangle" HorizontalAlignment="Stretch" VerticalAlignment="Stretch" Stroke="{TemplateBinding Background}" RadiusX="20" RadiusY="20" StrokeThickness="5" Fill="Transparent" />
          <!-- Inner Rectangle with rounded corners. -->
          <Rectangle x:Name="innerRectangle" HorizontalAlignment="Stretch" VerticalAlignment="Stretch" Stroke="Transparent" StrokeThickness="20" Fill="{TemplateBinding Background}" RadiusX="20" RadiusY="20" />
          <!-- Present Content (text) of the button. -->
          <DockPanel Name="myContentPresenterDockPanel">
            <ContentPresenter x:Name="myContentPresenter" Margin="20" Content="{TemplateBinding  Content}" TextBlock.Foreground="Black" />
          </DockPanel>
        </Grid>
      </ControlTemplate>
    </Setter.Value>
    ```

     <span data-ttu-id="83a11-172">Naciśnij klawisz F5, aby uruchomić aplikację.</span><span class="sxs-lookup"><span data-stu-id="83a11-172">Press F5 to run the application.</span></span> <span data-ttu-id="83a11-173">Powinien wyglądać podobnie do poniższego.</span><span class="sxs-lookup"><span data-stu-id="83a11-173">It should look like the following.</span></span>

     ![Okno z 3 przyciskami](./media/custom-button-animatedbutton-4.gif)

3. <span data-ttu-id="83a11-175">**Dodaj GlassEffect do szablonu:** Następnie dodasz szklaną.</span><span class="sxs-lookup"><span data-stu-id="83a11-175">**Add a glasseffect to the template:** Next you will add the glass.</span></span> <span data-ttu-id="83a11-176">Najpierw należy utworzyć zasoby, które tworzą efekt gradientu szkła.</span><span class="sxs-lookup"><span data-stu-id="83a11-176">First you create some resources that create a glass gradient effect.</span></span> <span data-ttu-id="83a11-177">Dodaj te zasoby gradientu w dowolnym miejscu w `Application.Resources` bloku:</span><span class="sxs-lookup"><span data-stu-id="83a11-177">Add these gradient resources anywhere within the `Application.Resources` block:</span></span>

    ```xaml
    <Application.Resources>
      <GradientStopCollection x:Key="MyGlassGradientStopsResource">
        <GradientStop Color="WhiteSmoke" Offset="0.2" />
        <GradientStop Color="Transparent" Offset="0.4" />
        <GradientStop Color="WhiteSmoke" Offset="0.5" />
        <GradientStop Color="Transparent" Offset="0.75" />
        <GradientStop Color="WhiteSmoke" Offset="0.9" />
        <GradientStop Color="Transparent" Offset="1" />
      </GradientStopCollection>
      <LinearGradientBrush x:Key="MyGlassBrushResource"
        StartPoint="0,0" EndPoint="1,1" Opacity="0.75"
        GradientStops="{StaticResource MyGlassGradientStopsResource}" />
    <!-- Styles and other resources below here. -->
    ```

     <span data-ttu-id="83a11-178">Te zasoby są używane jako <xref:System.Windows.Shapes.Shape.Fill%2A> dla prostokąta, który został wstawiony do <xref:System.Windows.Controls.Grid> szablonu przycisku.</span><span class="sxs-lookup"><span data-stu-id="83a11-178">These resources are used as the <xref:System.Windows.Shapes.Shape.Fill%2A> for a rectangle that we insert into the <xref:System.Windows.Controls.Grid> of the button template.</span></span> <span data-ttu-id="83a11-179">Dodaj następujący wyróżniony znacznik do szablonu.</span><span class="sxs-lookup"><span data-stu-id="83a11-179">Add the following highlighted markup to the template.</span></span>

    ```xaml
    <Setter.Value>
      <ControlTemplate TargetType="{x:Type Button}">
        <Grid Width="{TemplateBinding Width}" Height="{TemplateBinding Height}"
          ClipToBounds="True">

        <!-- Outer Rectangle with rounded corners. -->
        <Rectangle x:Name="outerRectangle" HorizontalAlignment="Stretch"
          VerticalAlignment="Stretch" Stroke="{TemplateBinding Background}"
          RadiusX="20" RadiusY="20" StrokeThickness="5" Fill="Transparent" />

        <!-- Inner Rectangle with rounded corners. -->
        <Rectangle x:Name="innerRectangle" HorizontalAlignment="Stretch"
          VerticalAlignment="Stretch" Stroke="Transparent" StrokeThickness="20"
          Fill="{TemplateBinding Background}" RadiusX="20" RadiusY="20" />

        <!-- Glass Rectangle -->
        <Rectangle x:Name="glassCube" HorizontalAlignment="Stretch"
          VerticalAlignment="Stretch"
          StrokeThickness="2" RadiusX="10" RadiusY="10" Opacity="0"
          Fill="{StaticResource MyGlassBrushResource}"
          RenderTransformOrigin="0.5,0.5">
          <Rectangle.Stroke>
            <LinearGradientBrush StartPoint="0.5,0" EndPoint="0.5,1">
              <LinearGradientBrush.GradientStops>
                <GradientStop Offset="0.0" Color="LightBlue" />
                <GradientStop Offset="1.0" Color="Gray" />
              </LinearGradientBrush.GradientStops>
            </LinearGradientBrush>
          </Rectangle.Stroke>
          <!-- These transforms have no effect as they are declared here.
          The reason the transforms are included is to be targets
          for animation (see later). -->
          <Rectangle.RenderTransform>
            <TransformGroup>
              <ScaleTransform />
              <RotateTransform />
            </TransformGroup>
          </Rectangle.RenderTransform>
          <!-- A BevelBitmapEffect is applied to give the button a "Beveled" look. -->
          <Rectangle.BitmapEffect>
            <BevelBitmapEffect />
          </Rectangle.BitmapEffect>
        </Rectangle>

        <!-- Present Text of the button. -->
        <DockPanel Name="myContentPresenterDockPanel">
          <ContentPresenter x:Name="myContentPresenter" Margin="20"
            Content="{TemplateBinding  Content}" TextBlock.Foreground="Black" />
        </DockPanel>
      </Grid>
    </ControlTemplate>
    </Setter.Value>
    ```

     <span data-ttu-id="83a11-180">Należy zauważyć, że <xref:System.Windows.UIElement.Opacity%2A> prostokąt z `x:Name` właściwością "glassCube" ma wartość 0, więc po uruchomieniu przykładu nie jest wyświetlany prostokąt szklany umieszczony na górze.</span><span class="sxs-lookup"><span data-stu-id="83a11-180">Notice that the <xref:System.Windows.UIElement.Opacity%2A> of the rectangle with the `x:Name` property of "glassCube" is 0, so when you run the sample, you do not see the glass rectangle overlaid on top.</span></span> <span data-ttu-id="83a11-181">Dzieje się tak dlatego, że później dodamy wyzwalacze do szablonu, gdy użytkownik będzie współdziałać z przyciskiem.</span><span class="sxs-lookup"><span data-stu-id="83a11-181">This is because we will later add triggers to the template for when the user interacts with the button.</span></span> <span data-ttu-id="83a11-182">Można jednak zobaczyć, jak wygląda przycisk teraz, zmieniając <xref:System.Windows.UIElement.Opacity%2A> wartość na 1 i uruchamiając aplikację.</span><span class="sxs-lookup"><span data-stu-id="83a11-182">However, you can see what the button looks like now by changing the <xref:System.Windows.UIElement.Opacity%2A> value to 1 and running the application.</span></span> <span data-ttu-id="83a11-183">Zobacz poniższą ilustrację.</span><span class="sxs-lookup"><span data-stu-id="83a11-183">See the following figure.</span></span> <span data-ttu-id="83a11-184">Przed przejściem do następnego kroku Zmień wartość <xref:System.Windows.UIElement.Opacity%2A> z powrotem na 0.</span><span class="sxs-lookup"><span data-stu-id="83a11-184">Before proceeding to the next step, change the <xref:System.Windows.UIElement.Opacity%2A> back to 0.</span></span>

     <span data-ttu-id="83a11-185">![Przyciski niestandardowe, które zostały utworzone przy użyciu języka XAML](./media/custom-button-animatedbutton-5.gif "custom_button_AnimatedButton_5")</span><span class="sxs-lookup"><span data-stu-id="83a11-185">![Custom buttons that were created by using XAML](./media/custom-button-animatedbutton-5.gif "custom_button_AnimatedButton_5")</span></span>

## <a name="create-button-interactivity"></a><span data-ttu-id="83a11-186">Utwórz interaktywny przycisk</span><span class="sxs-lookup"><span data-stu-id="83a11-186">Create Button Interactivity</span></span>

<span data-ttu-id="83a11-187">W tej sekcji utworzysz wyzwalacze właściwości i wyzwalacze zdarzeń, aby zmienić wartości właściwości i uruchamiać animacje w odpowiedzi na akcje użytkownika, takie jak przesuwanie wskaźnika myszy nad przyciskiem i klikanie.</span><span class="sxs-lookup"><span data-stu-id="83a11-187">In this section, you will create property triggers and event triggers to change property values and run animations in response to user actions such as moving the mouse pointer over the button and clicking.</span></span>

<span data-ttu-id="83a11-188">Prosty sposób na dodanie interaktywności (przesuwanie myszą, wyjście myszy, kliknięcie itd.) polega na zdefiniowaniu wyzwalaczy w szablonie lub stylu.</span><span class="sxs-lookup"><span data-stu-id="83a11-188">An easy way to add interactivity (mouse-over, mouse-leave, click, and so on) is to define triggers within your template or style.</span></span> <span data-ttu-id="83a11-189">Aby utworzyć <xref:System.Windows.Trigger> , należy zdefiniować Właściwość "warunek", taką jak: <xref:System.Windows.UIElement.IsMouseOver%2A> wartość właściwości Button jest równa `true` .</span><span class="sxs-lookup"><span data-stu-id="83a11-189">To create a <xref:System.Windows.Trigger>, you define a property "condition" such as: The button <xref:System.Windows.UIElement.IsMouseOver%2A> property value is equal to `true`.</span></span> <span data-ttu-id="83a11-190">Następnie definiuje się metody ustawiające (akcje), które mają miejsce, gdy warunek wyzwalacza ma wartość true.</span><span class="sxs-lookup"><span data-stu-id="83a11-190">You then define setters (actions) that take place when the trigger condition is true.</span></span>

### <a name="to-create-button-interactivity"></a><span data-ttu-id="83a11-191">Aby utworzyć interaktywny przycisk</span><span class="sxs-lookup"><span data-stu-id="83a11-191">To create button interactivity</span></span>

1. <span data-ttu-id="83a11-192">**Dodaj wyzwalacze szablonu:** Dodaj wyróżnione adiustacje do szablonu.</span><span class="sxs-lookup"><span data-stu-id="83a11-192">**Add template triggers:** Add the highlighted markup to your template.</span></span>

    ```xaml
    <Setter.Value>
      <ControlTemplate TargetType="{x:Type Button}">
        <Grid Width="{TemplateBinding Width}"
          Height="{TemplateBinding Height}" ClipToBounds="True">

          <!-- Outer Rectangle with rounded corners. -->
          <Rectangle x:Name="outerRectangle" HorizontalAlignment="Stretch"
          VerticalAlignment="Stretch" Stroke="{TemplateBinding Background}"
          RadiusX="20" RadiusY="20" StrokeThickness="5" Fill="Transparent" />

          <!-- Inner Rectangle with rounded corners. -->
          <Rectangle x:Name="innerRectangle" HorizontalAlignment="Stretch"
            VerticalAlignment="Stretch" Stroke="Transparent"
            StrokeThickness="20"
            Fill="{TemplateBinding Background}" RadiusX="20" RadiusY="20"
          />

          <!-- Glass Rectangle -->
          <Rectangle x:Name="glassCube" HorizontalAlignment="Stretch"
            VerticalAlignment="Stretch"
            StrokeThickness="2" RadiusX="10" RadiusY="10" Opacity="0"
            Fill="{StaticResource MyGlassBrushResource}"
            RenderTransformOrigin="0.5,0.5">
            <Rectangle.Stroke>
              <LinearGradientBrush StartPoint="0.5,0" EndPoint="0.5,1">
                <LinearGradientBrush.GradientStops>
                  <GradientStop Offset="0.0" Color="LightBlue" />
                  <GradientStop Offset="1.0" Color="Gray" />
                </LinearGradientBrush.GradientStops>
              </LinearGradientBrush>
            </Rectangle.Stroke>

            <!-- These transforms have no effect as they
                 are declared here.
                 The reason the transforms are included is to be targets
                 for animation (see later). -->
            <Rectangle.RenderTransform>
              <TransformGroup>
                <ScaleTransform />
                <RotateTransform />
              </TransformGroup>
            </Rectangle.RenderTransform>

              <!-- A BevelBitmapEffect is applied to give the button a
                   "Beveled" look. -->
            <Rectangle.BitmapEffect>
              <BevelBitmapEffect />
            </Rectangle.BitmapEffect>
          </Rectangle>

          <!-- Present Text of the button. -->
          <DockPanel Name="myContentPresenterDockPanel">
            <ContentPresenter x:Name="myContentPresenter" Margin="20"
              Content="{TemplateBinding  Content}" TextBlock.Foreground="Black" />
          </DockPanel>
        </Grid>

        <ControlTemplate.Triggers>       <!-- Set action triggers for the buttons and define            what the button does in response to those triggers. -->     </ControlTemplate.Triggers>
      </ControlTemplate>
    </Setter.Value>
    ```

2. <span data-ttu-id="83a11-193">**Dodaj wyzwalacze właściwości:** Dodaj wyróżnione znaczniki do `ControlTemplate.Triggers` bloku:</span><span class="sxs-lookup"><span data-stu-id="83a11-193">**Add property triggers:** Add the highlighted markup to the `ControlTemplate.Triggers` block:</span></span>

    ```xaml
    <ControlTemplate.Triggers>

      <!-- Set properties when mouse pointer is over the button. -->   <Trigger Property="IsMouseOver" Value="True">     <!-- Below are three property settings that occur when the           condition is met (user mouses over button).  -->     <!-- Change the color of the outer rectangle when user           mouses over it. -->     <Setter Property ="Rectangle.Stroke" TargetName="outerRectangle"       Value="{DynamicResource {x:Static SystemColors.HighlightBrushKey}}" />     <!-- Sets the glass opacity to 1, therefore, the           glass "appears" when user mouses over it. -->     <Setter Property="Rectangle.Opacity" Value="1" TargetName="glassCube" />     <!-- Makes the text slightly blurry as though you           were looking at it through blurry glass. -->     <Setter Property="ContentPresenter.BitmapEffect"        TargetName="myContentPresenter">       <Setter.Value>         <BlurBitmapEffect Radius="1" />       </Setter.Value>     </Setter>   </Trigger>

    <ControlTemplate.Triggers/>
    ```

     <span data-ttu-id="83a11-194">Naciśnij klawisz F5, aby uruchomić aplikację i zobaczyć efekt podczas uruchamiania wskaźnika myszy nad przyciskami.</span><span class="sxs-lookup"><span data-stu-id="83a11-194">Press F5 to run the application and see the effect as you run the mouse pointer over the buttons.</span></span>

3. <span data-ttu-id="83a11-195">**Dodaj wyzwalacz fokusu:** Następnie dodamy kilka podobnych metod ustawiających, aby obsłużyć przypadek, gdy przycisk ma fokus (na przykład po kliknięciu przez użytkownika).</span><span class="sxs-lookup"><span data-stu-id="83a11-195">**Add a focus trigger:** Next, we'll add some similar setters to handle the case when the button has focus (for example, after the user clicks it).</span></span>

    ```xaml
    <ControlTemplate.Triggers>

      <!-- Set properties when mouse pointer is over the button. -->
      <Trigger Property="IsMouseOver" Value="True">

        <!-- Below are three property settings that occur when the
             condition is met (user mouses over button).  -->
        <!-- Change the color of the outer rectangle when user          mouses over it. -->
        <Setter Property ="Rectangle.Stroke" TargetName="outerRectangle"
          Value="{DynamicResource {x:Static SystemColors.HighlightBrushKey}}" />

        <!-- Sets the glass opacity to 1, therefore, the          glass "appears" when user mouses over it. -->
        <Setter Property="Rectangle.Opacity" Value="1"       TargetName="glassCube" />

        <!-- Makes the text slightly blurry as though you were          looking at it through blurry glass. -->
        <Setter Property="ContentPresenter.BitmapEffect"       TargetName="myContentPresenter">
          <Setter.Value>
            <BlurBitmapEffect Radius="1" />
          </Setter.Value>
        </Setter>
      </Trigger>
      <!-- Set properties when button has focus. -->   <Trigger Property="IsFocused" Value="true">     <Setter Property="Rectangle.Opacity" Value="1"       TargetName="glassCube" />     <Setter Property="Rectangle.Stroke" TargetName="outerRectangle"       Value="{DynamicResource {x:Static SystemColors.HighlightBrushKey}}" />     <Setter Property="Rectangle.Opacity" Value="1" TargetName="glassCube" />   </Trigger>

    </ControlTemplate.Triggers>
    ```

     <span data-ttu-id="83a11-196">Naciśnij klawisz F5, aby uruchomić aplikację, a następnie kliknij jeden z przycisków.</span><span class="sxs-lookup"><span data-stu-id="83a11-196">Press F5 to run the application and click on one of the buttons.</span></span> <span data-ttu-id="83a11-197">Zauważ, że przycisk pozostaje wyróżniony po kliknięciu go, ponieważ nadal ma fokus.</span><span class="sxs-lookup"><span data-stu-id="83a11-197">Notice that the button stays highlighted after you click it because it still has focus.</span></span> <span data-ttu-id="83a11-198">Jeśli klikniesz inny przycisk, nowy przycisk stanie się fokusem, a ostatni z nich utraci.</span><span class="sxs-lookup"><span data-stu-id="83a11-198">If you click another button, the new button gains focus while the last one loses it.</span></span>

4. <span data-ttu-id="83a11-199">**Dodaj animacje dla** <xref:System.Windows.UIElement.MouseEnter> **i** <xref:System.Windows.UIElement.MouseLeave> **:** Następnie dodamy kilka animacji do wyzwalaczy.  </span><span class="sxs-lookup"><span data-stu-id="83a11-199">**Add animations for**  <xref:System.Windows.UIElement.MouseEnter> **and** <xref:System.Windows.UIElement.MouseLeave> **:** Next we add some animations to the triggers.</span></span> <span data-ttu-id="83a11-200">Dodaj następujący znacznik w dowolnym miejscu wewnątrz `ControlTemplate.Triggers` bloku.</span><span class="sxs-lookup"><span data-stu-id="83a11-200">Add the following markup anywhere inside of the `ControlTemplate.Triggers` block.</span></span>

    ```xaml
    <!-- Animations that start when mouse enters and leaves button. -->
    <EventTrigger RoutedEvent="Mouse.MouseEnter">
      <EventTrigger.Actions>
        <BeginStoryboard Name="mouseEnterBeginStoryboard">
          <Storyboard>
          <!-- This animation makes the glass rectangle shrink in the X direction. -->
            <DoubleAnimation Storyboard.TargetName="glassCube"
              Storyboard.TargetProperty=
              "(Rectangle.RenderTransform).(TransformGroup.Children)[0].(ScaleTransform.ScaleX)"
              By="-0.1" Duration="0:0:0.5" />
            <!-- This animation makes the glass rectangle shrink in the Y direction. -->
            <DoubleAnimation
            Storyboard.TargetName="glassCube"
              Storyboard.TargetProperty=
              "(Rectangle.RenderTransform).(TransformGroup.Children)[0].(ScaleTransform.ScaleY)"
              By="-0.1" Duration="0:0:0.5" />
          </Storyboard>
        </BeginStoryboard>
      </EventTrigger.Actions>
    </EventTrigger>
    <EventTrigger RoutedEvent="Mouse.MouseLeave">
      <EventTrigger.Actions>
        <!-- Stopping the storyboard sets all animated properties back to default. -->
        <StopStoryboard BeginStoryboardName="mouseEnterBeginStoryboard" />
      </EventTrigger.Actions>
    </EventTrigger>
    ```

     <span data-ttu-id="83a11-201">Prostokąt szklany zmniejsza się, gdy wskaźnik myszy przesuwa się nad przycisk i wraca do normalnego rozmiaru przy opuszczaniu wskaźnika.</span><span class="sxs-lookup"><span data-stu-id="83a11-201">The glass rectangle shrinks when the mouse pointer moves over the button and returns back to normal size when the pointer leaves.</span></span>

     <span data-ttu-id="83a11-202">Istnieją dwie animacje wyzwalane, gdy wskaźnik myszy znajduje się nad przyciskiem ( <xref:System.Windows.UIElement.MouseEnter> zdarzenie jest zgłaszane).</span><span class="sxs-lookup"><span data-stu-id="83a11-202">There are two animations that are triggered when the pointer goes over the button (<xref:System.Windows.UIElement.MouseEnter> event is raised).</span></span> <span data-ttu-id="83a11-203">Te animacje zmniejszają prostokąt szklany wzdłuż osi X i Y.</span><span class="sxs-lookup"><span data-stu-id="83a11-203">These animations shrink the glass rectangle along the X and Y axis.</span></span> <span data-ttu-id="83a11-204">Zwróć uwagę na właściwości <xref:System.Windows.Media.Animation.DoubleAnimation> elementów — <xref:System.Windows.Media.Animation.Timeline.Duration%2A> i <xref:System.Windows.Media.Animation.DoubleAnimation.By%2A> .</span><span class="sxs-lookup"><span data-stu-id="83a11-204">Notice the properties on the <xref:System.Windows.Media.Animation.DoubleAnimation> elements — <xref:System.Windows.Media.Animation.Timeline.Duration%2A> and <xref:System.Windows.Media.Animation.DoubleAnimation.By%2A>.</span></span> <span data-ttu-id="83a11-205"><xref:System.Windows.Media.Animation.Timeline.Duration%2A>Określa, że animacja występuje w ciągu pół sekundy i <xref:System.Windows.Media.Animation.DoubleAnimation.By%2A> określa, że szkło zmniejsza się o 10%.</span><span class="sxs-lookup"><span data-stu-id="83a11-205">The <xref:System.Windows.Media.Animation.Timeline.Duration%2A> specifies that the animation occurs over half a second, and <xref:System.Windows.Media.Animation.DoubleAnimation.By%2A> specifies that the glass shrinks by 10%.</span></span>

     <span data-ttu-id="83a11-206">Drugi wyzwalacz zdarzenia ( <xref:System.Windows.UIElement.MouseLeave> ) po prostu kończy pierwszy.</span><span class="sxs-lookup"><span data-stu-id="83a11-206">The second event trigger (<xref:System.Windows.UIElement.MouseLeave>) simply stops the first one.</span></span> <span data-ttu-id="83a11-207">Po zatrzymaniu elementu <xref:System.Windows.Media.Animation.Storyboard> wszystkie animowane właściwości są przywracane do wartości domyślnych.</span><span class="sxs-lookup"><span data-stu-id="83a11-207">When you stop a <xref:System.Windows.Media.Animation.Storyboard>, all the animated properties return to their default values.</span></span> <span data-ttu-id="83a11-208">W związku z tym, gdy użytkownik przesuwa wskaźnik poza przycisk, po przesunięciu wskaźnika myszy nad przycisk przechodzi do końca.</span><span class="sxs-lookup"><span data-stu-id="83a11-208">Therefore, when the user moves the pointer off the button, the button goes back to the way it was before the mouse pointer moved over the button.</span></span> <span data-ttu-id="83a11-209">Aby uzyskać więcej informacji na temat animacji, zobacz [Omówienie animacji](../graphics-multimedia/animation-overview.md).</span><span class="sxs-lookup"><span data-stu-id="83a11-209">For more information about animations, see [Animation Overview](../graphics-multimedia/animation-overview.md).</span></span>

5. <span data-ttu-id="83a11-210">**Dodaj animację dla momentu kliknięcia przycisku:** Ostatnim krokiem jest dodanie wyzwalacza, gdy użytkownik kliknie przycisk.</span><span class="sxs-lookup"><span data-stu-id="83a11-210">**Add an animation for when the button is clicked:** The final step is to add a trigger for when the user clicks the button.</span></span> <span data-ttu-id="83a11-211">Dodaj następujący znacznik w dowolnym miejscu wewnątrz `ControlTemplate.Triggers` bloku:</span><span class="sxs-lookup"><span data-stu-id="83a11-211">Add the following markup anywhere inside of the `ControlTemplate.Triggers` block:</span></span>

    ```xaml
    <!-- Animation fires when button is clicked, causing glass to spin.  -->
    <EventTrigger RoutedEvent="Button.Click">
      <EventTrigger.Actions>
        <BeginStoryboard>
          <Storyboard>
            <DoubleAnimation Storyboard.TargetName="glassCube"
              Storyboard.TargetProperty=
              "(Rectangle.RenderTransform).(TransformGroup.Children)[1].(RotateTransform.Angle)"
              By="360" Duration="0:0:0.5" />
          </Storyboard>
        </BeginStoryboard>
      </EventTrigger.Actions>
    </EventTrigger>
    ```

     <span data-ttu-id="83a11-212">Naciśnij klawisz F5, aby uruchomić aplikację, a następnie kliknij jeden z przycisków.</span><span class="sxs-lookup"><span data-stu-id="83a11-212">Press F5 to run the application, and click one of the buttons.</span></span> <span data-ttu-id="83a11-213">Po kliknięciu przycisku, prostokąt szklany obraca się wokół siebie.</span><span class="sxs-lookup"><span data-stu-id="83a11-213">When you click a button, the glass rectangle spins around.</span></span>

## <a name="summary"></a><span data-ttu-id="83a11-214">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="83a11-214">Summary</span></span>
 <span data-ttu-id="83a11-215">W tym instruktażu wykonasz następujące ćwiczenia:</span><span class="sxs-lookup"><span data-stu-id="83a11-215">In this walkthrough, you performed the following exercises:</span></span>

- <span data-ttu-id="83a11-216">Nakierowany a <xref:System.Windows.Style> do typu obiektu ( <xref:System.Windows.Controls.Button> ).</span><span class="sxs-lookup"><span data-stu-id="83a11-216">Targeted a <xref:System.Windows.Style> to an object type (<xref:System.Windows.Controls.Button>).</span></span>

- <span data-ttu-id="83a11-217">Kontrolowane podstawowe właściwości przycisków w całej aplikacji przy użyciu <xref:System.Windows.Style> .</span><span class="sxs-lookup"><span data-stu-id="83a11-217">Controlled basic properties of the buttons in the entire application using the <xref:System.Windows.Style>.</span></span>

- <span data-ttu-id="83a11-218">Utworzone zasoby, takie jak gradienty, które mają być używane dla wartości właściwości metod <xref:System.Windows.Style> ustawiających.</span><span class="sxs-lookup"><span data-stu-id="83a11-218">Created resources like gradients to use for property values of the <xref:System.Windows.Style> setters.</span></span>

- <span data-ttu-id="83a11-219">Dostosowany wygląd przycisków w całej aplikacji przez zastosowanie szablonu do przycisków.</span><span class="sxs-lookup"><span data-stu-id="83a11-219">Customized the look of buttons in the entire application by applying a template to the buttons.</span></span>

- <span data-ttu-id="83a11-220">Dostosowane zachowanie przycisków w odpowiedzi na akcje użytkownika (takie jak <xref:System.Windows.UIElement.MouseEnter> , <xref:System.Windows.UIElement.MouseLeave> i <xref:System.Windows.Controls.Primitives.ButtonBase.Click> ), które uwzględniają efekty animacji.</span><span class="sxs-lookup"><span data-stu-id="83a11-220">Customized behavior for the buttons in response to user actions (such as <xref:System.Windows.UIElement.MouseEnter>, <xref:System.Windows.UIElement.MouseLeave>, and <xref:System.Windows.Controls.Primitives.ButtonBase.Click>) that included animation effects.</span></span>

## <a name="see-also"></a><span data-ttu-id="83a11-221">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="83a11-221">See also</span></span>

- [<span data-ttu-id="83a11-222">Tworzenie przycisku przy użyciu programu Microsoft Expression Blend</span><span class="sxs-lookup"><span data-stu-id="83a11-222">Create a Button by Using Microsoft Expression Blend</span></span>](walkthrough-create-a-button-by-using-microsoft-expression-blend.md)
- [<span data-ttu-id="83a11-223">Tworzenie szablonów i stylów</span><span class="sxs-lookup"><span data-stu-id="83a11-223">Styling and Templating</span></span>](../../../desktop-wpf/fundamentals/styles-templates-overview.md)
- [<span data-ttu-id="83a11-224">Przegląd Animacja</span><span class="sxs-lookup"><span data-stu-id="83a11-224">Animation Overview</span></span>](../graphics-multimedia/animation-overview.md)
- [<span data-ttu-id="83a11-225">Przegląd Malowanie jednolitymi kolorami i gradientami</span><span class="sxs-lookup"><span data-stu-id="83a11-225">Painting with Solid Colors and Gradients Overview</span></span>](../graphics-multimedia/painting-with-solid-colors-and-gradients-overview.md)
- [<span data-ttu-id="83a11-226">Przegląd Efekty mapy bitowej</span><span class="sxs-lookup"><span data-stu-id="83a11-226">Bitmap Effects Overview</span></span>](../graphics-multimedia/bitmap-effects-overview.md)
