---
title: My.Resources — Obiekt
ms.date: 07/20/2015
f1_keywords:
- My.Resources
- My.Resources.MyResources.ResourceManager
- My.Resources.MyResources.Culture
helpviewer_keywords:
- My.Resources object
ms.assetid: 34c3f2dc-7b87-432c-9d5f-17ea666bb266
ms.openlocfilehash: 3d12524706f680434d5b6d8da39c89042bea3281
ms.sourcegitcommit: d2db216e46323f73b32ae312c9e4135258e5d68e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/22/2020
ms.locfileid: "90867338"
---
# <a name="myresources-object"></a><span data-ttu-id="a568d-102">My.Resources — Obiekt</span><span class="sxs-lookup"><span data-stu-id="a568d-102">My.Resources Object</span></span>

<span data-ttu-id="a568d-103">Udostępnia właściwości i klasy do uzyskiwania dostępu do zasobów aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a568d-103">Provides properties and classes for accessing the application's resources.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="a568d-104">Uwagi</span><span class="sxs-lookup"><span data-stu-id="a568d-104">Remarks</span></span>  

 <span data-ttu-id="a568d-105">`My.Resources`Obiekt zapewnia dostęp do zasobów aplikacji i umożliwia dynamiczne pobieranie zasobów dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a568d-105">The `My.Resources` object provides access to the application's resources and lets you dynamically retrieve resources for your application.</span></span> <span data-ttu-id="a568d-106">Aby uzyskać więcej informacji, zobacz [Zarządzanie zasobami aplikacji (.NET)](/visualstudio/ide/managing-application-resources-dotnet).</span><span class="sxs-lookup"><span data-stu-id="a568d-106">For more information, see [Managing Application Resources (.NET)](/visualstudio/ide/managing-application-resources-dotnet).</span></span>  
  
 <span data-ttu-id="a568d-107">`My.Resources`Obiekt uwidacznia tylko zasoby globalne.</span><span class="sxs-lookup"><span data-stu-id="a568d-107">The `My.Resources` object exposes only global resources.</span></span> <span data-ttu-id="a568d-108">Nie zapewnia dostępu do plików zasobów skojarzonych z formularzami.</span><span class="sxs-lookup"><span data-stu-id="a568d-108">It does not provide access to resource files associated with forms.</span></span> <span data-ttu-id="a568d-109">Musisz uzyskać dostęp do zasobów formularza z formularza.</span><span class="sxs-lookup"><span data-stu-id="a568d-109">You must access the form resources from the form.</span></span>  
  
 <span data-ttu-id="a568d-110">Możesz uzyskać dostęp do plików zasobów specyficznych dla kultury aplikacji z `My.Resources` obiektu.</span><span class="sxs-lookup"><span data-stu-id="a568d-110">You can access the application's culture-specific resource files from the `My.Resources` object.</span></span> <span data-ttu-id="a568d-111">Domyślnie `My.Resources` obiekt wyszukuje zasoby z pliku zasobów, który jest zgodny z kulturą we <xref:Microsoft.VisualBasic.ApplicationServices.ApplicationBase.UICulture%2A> właściwości.</span><span class="sxs-lookup"><span data-stu-id="a568d-111">By default, the `My.Resources` object looks up resources from the resource file that matches the culture in the <xref:Microsoft.VisualBasic.ApplicationServices.ApplicationBase.UICulture%2A> property.</span></span> <span data-ttu-id="a568d-112">Można jednak zastąpić to zachowanie i określić określoną kulturę do użycia dla zasobów.</span><span class="sxs-lookup"><span data-stu-id="a568d-112">However, you can override this behavior and specify a particular culture to use for the resources.</span></span> <span data-ttu-id="a568d-113">Aby uzyskać więcej informacji, zobacz [zasoby w aplikacjach klasycznych](../../../framework/resources/index.md).</span><span class="sxs-lookup"><span data-stu-id="a568d-113">For more information, see [Resources in Desktop Apps](../../../framework/resources/index.md).</span></span>  
  
## <a name="properties"></a><span data-ttu-id="a568d-114">Właściwości</span><span class="sxs-lookup"><span data-stu-id="a568d-114">Properties</span></span>  

 <span data-ttu-id="a568d-115">Właściwości `My.Resources` obiektu zapewniają dostęp tylko do odczytu do zasobów aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a568d-115">The properties of the `My.Resources` object provide read-only access to your application's resources.</span></span> <span data-ttu-id="a568d-116">Aby dodać lub usunąć zasoby, użyj **projektanta projektu**.</span><span class="sxs-lookup"><span data-stu-id="a568d-116">To add or remove resources, use the **Project Designer**.</span></span> <span data-ttu-id="a568d-117">Dostęp do zasobów dodanych za pośrednictwem **projektanta projektu** można uzyskać za pomocą `My.Resources.` *resourceName*.</span><span class="sxs-lookup"><span data-stu-id="a568d-117">You can access resources added through the **Project Designer** by using `My.Resources.`*resourceName*.</span></span>  
  
 <span data-ttu-id="a568d-118">Możesz również dodać lub usunąć pliki zasobów, wybierając projekt w **Eksplorator rozwiązań** i klikając polecenie **Dodaj nowy element** lub **Dodaj istniejący element** z menu **projekt** .</span><span class="sxs-lookup"><span data-stu-id="a568d-118">You can also add or remove resource files by selecting your project in **Solution Explorer** and clicking **Add New Item** or **Add Existing Item** from the **Project** menu.</span></span> <span data-ttu-id="a568d-119">Dostęp do zasobów dodanych w ten sposób można uzyskać przy użyciu `My.Resources.` *resourceFileName* `.` *resourceName*nazwaplikuzasobów.</span><span class="sxs-lookup"><span data-stu-id="a568d-119">You can access resources added in this manner by using `My.Resources.`*resourceFileName*`.`*resourceName*.</span></span>  
  
 <span data-ttu-id="a568d-120">Każdy zasób ma nazwę, kategorię i wartość, a te ustawienia zasobów określają, w jaki sposób Właściwość uzyskiwania dostępu do zasobu jest wyświetlana w `My.Resources` obiekcie.</span><span class="sxs-lookup"><span data-stu-id="a568d-120">Each resource has a name, category, and value, and these resource settings determine how the property to access the resource appears in the `My.Resources` object.</span></span> <span data-ttu-id="a568d-121">Dla zasobów dodanych w **projektancie projektu**:</span><span class="sxs-lookup"><span data-stu-id="a568d-121">For resources added in the **Project Designer**:</span></span>  
  
- <span data-ttu-id="a568d-122">Nazwa Określa nazwę właściwości,</span><span class="sxs-lookup"><span data-stu-id="a568d-122">The name determines the name of the property,</span></span>  
  
- <span data-ttu-id="a568d-123">Dane zasobu to wartość właściwości,</span><span class="sxs-lookup"><span data-stu-id="a568d-123">The resource data is the value of the property,</span></span>  
  
- <span data-ttu-id="a568d-124">Kategoria określa typ właściwości:</span><span class="sxs-lookup"><span data-stu-id="a568d-124">The category determines the type of the property:</span></span>  
  
|<span data-ttu-id="a568d-125">Kategoria</span><span class="sxs-lookup"><span data-stu-id="a568d-125">Category</span></span>|<span data-ttu-id="a568d-126">Typ danych właściwości</span><span class="sxs-lookup"><span data-stu-id="a568d-126">Property data type</span></span>|  
|---|---|  
|<span data-ttu-id="a568d-127">**Ciągi**</span><span class="sxs-lookup"><span data-stu-id="a568d-127">**Strings**</span></span>|[<span data-ttu-id="a568d-128">Ciąg</span><span class="sxs-lookup"><span data-stu-id="a568d-128">String</span></span>](../data-types/string-data-type.md)|  
|<span data-ttu-id="a568d-129">**Obrazy**</span><span class="sxs-lookup"><span data-stu-id="a568d-129">**Images**</span></span>|<xref:System.Drawing.Bitmap>|  
|<span data-ttu-id="a568d-130">**Ikony**</span><span class="sxs-lookup"><span data-stu-id="a568d-130">**Icons**</span></span>|<xref:System.Drawing.Icon>|  
|<span data-ttu-id="a568d-131">**Audio**</span><span class="sxs-lookup"><span data-stu-id="a568d-131">**Audio**</span></span>|<xref:System.IO.UnmanagedMemoryStream><br /><br /> <span data-ttu-id="a568d-132"><xref:System.IO.UnmanagedMemoryStream>Klasa pochodzi od <xref:System.IO.Stream> klasy, więc może być używana z metodami, które pobierają strumienie, takie jak <xref:Microsoft.VisualBasic.Devices.Audio.Play%2A> Metoda.</span><span class="sxs-lookup"><span data-stu-id="a568d-132">The <xref:System.IO.UnmanagedMemoryStream> class derives from the <xref:System.IO.Stream> class, so it can be used with methods that take streams, such as the <xref:Microsoft.VisualBasic.Devices.Audio.Play%2A> method.</span></span>|  
|<span data-ttu-id="a568d-133">**Files**</span><span class="sxs-lookup"><span data-stu-id="a568d-133">**Files**</span></span>|<span data-ttu-id="a568d-134">-   [Ciąg](../data-types/string-data-type.md) dla plików tekstowych.</span><span class="sxs-lookup"><span data-stu-id="a568d-134">-   [String](../data-types/string-data-type.md) for text files.</span></span><br /><span data-ttu-id="a568d-135">-   <xref:System.Drawing.Bitmap> dla plików obrazów.</span><span class="sxs-lookup"><span data-stu-id="a568d-135">-   <xref:System.Drawing.Bitmap> for image files.</span></span><br /><span data-ttu-id="a568d-136">-   <xref:System.Drawing.Icon> dla plików ikon.</span><span class="sxs-lookup"><span data-stu-id="a568d-136">-   <xref:System.Drawing.Icon> for icon files.</span></span><br /><span data-ttu-id="a568d-137">-   <xref:System.IO.UnmanagedMemoryStream> dla plików dźwiękowych.</span><span class="sxs-lookup"><span data-stu-id="a568d-137">-   <xref:System.IO.UnmanagedMemoryStream> for sound files.</span></span>|  
|<span data-ttu-id="a568d-138">**Inne**</span><span class="sxs-lookup"><span data-stu-id="a568d-138">**Other**</span></span>|<span data-ttu-id="a568d-139">Określone przez informacje w kolumnie **Typ** projektanta.</span><span class="sxs-lookup"><span data-stu-id="a568d-139">Determined by the information in the designer's **Type** column.</span></span>|  
  
## <a name="classes"></a><span data-ttu-id="a568d-140">Klasy</span><span class="sxs-lookup"><span data-stu-id="a568d-140">Classes</span></span>  

 <span data-ttu-id="a568d-141">`My.Resources`Obiekt uwidacznia każdy plik zasobów jako klasę z właściwościami udostępnionymi.</span><span class="sxs-lookup"><span data-stu-id="a568d-141">The `My.Resources` object exposes each resource file as a class with shared properties.</span></span> <span data-ttu-id="a568d-142">Nazwa klasy jest taka sama jak nazwa pliku zasobu.</span><span class="sxs-lookup"><span data-stu-id="a568d-142">The class name is the same as the name of the resource file.</span></span> <span data-ttu-id="a568d-143">Zgodnie z opisem w poprzedniej sekcji zasoby w pliku zasobów są ujawniane jako właściwości w klasie.</span><span class="sxs-lookup"><span data-stu-id="a568d-143">As described in the previous section, the resources in a resource file are exposed as properties in the class.</span></span>  
  
## <a name="example"></a><span data-ttu-id="a568d-144">Przykład</span><span class="sxs-lookup"><span data-stu-id="a568d-144">Example</span></span>  

 <span data-ttu-id="a568d-145">Ten przykład ustawia tytuł formularza na zasób ciągu o nazwie `Form1Title` w pliku zasobów aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a568d-145">This example sets the title of a form to the string resource named `Form1Title` in the application resource file.</span></span> <span data-ttu-id="a568d-146">Aby przykład działał, aplikacja musi mieć ciąg o nazwie `Form1Title` w pliku zasobów.</span><span class="sxs-lookup"><span data-stu-id="a568d-146">For the example to work, the application must have a string named `Form1Title` in its resource file.</span></span>  
  
 [!code-vb[VbVbalrMyResources#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyResources/VB/Form1.vb#1)]  
  
## <a name="example"></a><span data-ttu-id="a568d-147">Przykład</span><span class="sxs-lookup"><span data-stu-id="a568d-147">Example</span></span>  

 <span data-ttu-id="a568d-148">Ten przykład ustawia ikonę formularza na ikonę o nazwie `Form1Icon` , która jest przechowywana w pliku zasobów aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a568d-148">This example sets the icon of the form to the icon named `Form1Icon` that is stored in the application's resource file.</span></span> <span data-ttu-id="a568d-149">Aby przykład działał, aplikacja musi mieć ikonę o nazwie `Form1Icon` w pliku zasobów.</span><span class="sxs-lookup"><span data-stu-id="a568d-149">For the example to work, the application must have an icon named `Form1Icon` in its resource file.</span></span>  
  
 [!code-vb[VbVbalrMyResources#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyResources/VB/Form1.vb#2)]  
  
## <a name="example"></a><span data-ttu-id="a568d-150">Przykład</span><span class="sxs-lookup"><span data-stu-id="a568d-150">Example</span></span>  

 <span data-ttu-id="a568d-151">Ten przykład służy do ustawiania obrazu tła formularza do zasobu obrazu o nazwie `Form1Background` , który znajduje się w pliku zasobów aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a568d-151">This example sets the background image of a form to the image resource named `Form1Background`, which is in the application resource file.</span></span> <span data-ttu-id="a568d-152">Aby ten przykład działał, aplikacja musi mieć zasób obrazu o nazwie `Form1Background` w pliku zasobów.</span><span class="sxs-lookup"><span data-stu-id="a568d-152">For this example to work, the application must have an image resource named `Form1Background` in its resource file.</span></span>  
  
 [!code-vb[VbVbalrMyResources#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyResources/VB/Form1.vb#3)]  
  
## <a name="example"></a><span data-ttu-id="a568d-153">Przykład</span><span class="sxs-lookup"><span data-stu-id="a568d-153">Example</span></span>  

 <span data-ttu-id="a568d-154">Ten przykład odtwarza dźwięk zapisany jako zasób audio o nazwie `Form1Greeting` w pliku zasobów aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a568d-154">This example plays the sound that is stored as an audio resource named `Form1Greeting` in the application's resource file.</span></span> <span data-ttu-id="a568d-155">Aby przykład działał, aplikacja musi mieć zasób audio o nazwie `Form1Greeting` w pliku zasobów.</span><span class="sxs-lookup"><span data-stu-id="a568d-155">For the example to work, the application must have an audio resource named `Form1Greeting` in its resource file.</span></span> <span data-ttu-id="a568d-156">Ta `My.Computer.Audio.Play` Metoda jest dostępna tylko dla aplikacji Windows Forms.</span><span class="sxs-lookup"><span data-stu-id="a568d-156">The `My.Computer.Audio.Play` method is available only for Windows Forms applications.</span></span>  
  
 [!code-vb[VbVbalrMyResources#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyResources/VB/Form1.vb#4)]  
  
## <a name="example"></a><span data-ttu-id="a568d-157">Przykład</span><span class="sxs-lookup"><span data-stu-id="a568d-157">Example</span></span>  

 <span data-ttu-id="a568d-158">Ten przykład Pobiera wersję kultury języka francuskiego dla zasobu ciągu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a568d-158">This example retrieves the French-culture version of a  string resource of the application.</span></span> <span data-ttu-id="a568d-159">Zasób ma nazwę `Message` .</span><span class="sxs-lookup"><span data-stu-id="a568d-159">The resource is named `Message`.</span></span> <span data-ttu-id="a568d-160">Aby zmienić kulturę `My.Resources` używaną przez obiekt, użyjemy przykładu <xref:Microsoft.VisualBasic.ApplicationServices.ApplicationBase.ChangeUICulture%2A> .</span><span class="sxs-lookup"><span data-stu-id="a568d-160">To change the culture that the `My.Resources` object uses, the example uses <xref:Microsoft.VisualBasic.ApplicationServices.ApplicationBase.ChangeUICulture%2A>.</span></span>  
  
 <span data-ttu-id="a568d-161">Aby ten przykład działał, aplikacja musi mieć ciąg o nazwie `Message` w pliku zasobów, a aplikacja powinna mieć wersję kultury języka francuskiego tego pliku zasobów Resources.fr-fr. resx.</span><span class="sxs-lookup"><span data-stu-id="a568d-161">For this example to work, the application must have a string named `Message` in its resource file, and the application should have the French-culture version of that resource file, Resources.fr-FR.resx.</span></span> <span data-ttu-id="a568d-162">Jeśli aplikacja nie ma wersji pliku zasobów w języku francuskim, `My.Resource` obiekt pobiera zasób z pliku zasobów kultury domyślnej.</span><span class="sxs-lookup"><span data-stu-id="a568d-162">If the application does not have the French-culture version of the resource file, the `My.Resource` object retrieves the resource from the default-culture resource file.</span></span>  
  
 [!code-vb[VbVbalrMyResources#10](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyResources/VB/Form1.vb#10)]  
  
## <a name="see-also"></a><span data-ttu-id="a568d-163">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="a568d-163">See also</span></span>

- [<span data-ttu-id="a568d-164">Zarządzanie zasobami aplikacji (.NET)</span><span class="sxs-lookup"><span data-stu-id="a568d-164">Managing Application Resources (.NET)</span></span>](/visualstudio/ide/managing-application-resources-dotnet)
- [<span data-ttu-id="a568d-165">Zasoby w aplikacjach klasycznych</span><span class="sxs-lookup"><span data-stu-id="a568d-165">Resources in Desktop Apps</span></span>](../../../framework/resources/index.md)
