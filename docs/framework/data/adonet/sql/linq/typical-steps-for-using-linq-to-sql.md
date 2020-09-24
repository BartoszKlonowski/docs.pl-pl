---
title: Typowe kroki dotyczące korzystania z LINQ to SQL
ms.date: 03/30/2017
ms.assetid: 9a88bd51-bd74-48f7-a9b1-f650e8d55a3e
ms.openlocfilehash: dc8c4be1e895ee5c4c7947e6311e5bf71008490f
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91164263"
---
# <a name="typical-steps-for-using-linq-to-sql"></a><span data-ttu-id="29ee3-102">Typowe kroki dotyczące korzystania z LINQ to SQL</span><span class="sxs-lookup"><span data-stu-id="29ee3-102">Typical Steps for Using LINQ to SQL</span></span>

<span data-ttu-id="29ee3-103">Aby zaimplementować [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] aplikację, wykonaj kroki opisane w dalszej części tego tematu.</span><span class="sxs-lookup"><span data-stu-id="29ee3-103">To implement a [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] application, you follow the steps described later in this topic.</span></span> <span data-ttu-id="29ee3-104">Należy zauważyć, że wiele kroków jest opcjonalnych.</span><span class="sxs-lookup"><span data-stu-id="29ee3-104">Note that many steps are optional.</span></span> <span data-ttu-id="29ee3-105">Jest to bardzo możliwe, że można użyć modelu obiektów w stanie domyślnym.</span><span class="sxs-lookup"><span data-stu-id="29ee3-105">It is very possible that you can use your object model in its default state.</span></span>  
  
 <span data-ttu-id="29ee3-106">Aby szybko rozpocząć pracę, użyj Object Relational Designer, aby utworzyć model obiektów i rozpocząć kodowanie zapytań.</span><span class="sxs-lookup"><span data-stu-id="29ee3-106">For a really fast start, use the Object Relational Designer to create your object model and start coding your queries.</span></span>  
  
## <a name="creating-the-object-model"></a><span data-ttu-id="29ee3-107">Tworzenie modelu obiektu</span><span class="sxs-lookup"><span data-stu-id="29ee3-107">Creating the Object Model</span></span>  

 <span data-ttu-id="29ee3-108">Pierwszym krokiem jest utworzenie modelu obiektu na podstawie metadanych istniejącej relacyjnej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="29ee3-108">The first step is to create an object model from the metadata of an existing relational database.</span></span> <span data-ttu-id="29ee3-109">Model obiektów reprezentuje bazę danych zgodnie z językiem programowania dewelopera.</span><span class="sxs-lookup"><span data-stu-id="29ee3-109">The object model represents the database according to the programming language of the developer.</span></span> <span data-ttu-id="29ee3-110">Aby uzyskać więcej informacji, zobacz [model obiektów LINQ to SQL](the-linq-to-sql-object-model.md).</span><span class="sxs-lookup"><span data-stu-id="29ee3-110">For more information, see [The LINQ to SQL Object Model](the-linq-to-sql-object-model.md).</span></span>  
  
### <a name="1-select-a-tool-to-create-the-model"></a><span data-ttu-id="29ee3-111">1. Wybierz narzędzie, aby utworzyć model.</span><span class="sxs-lookup"><span data-stu-id="29ee3-111">1. Select a tool to create the model.</span></span>  

 <span data-ttu-id="29ee3-112">Do utworzenia modelu dostępne są trzy narzędzia.</span><span class="sxs-lookup"><span data-stu-id="29ee3-112">Three tools are available for creating the model.</span></span>  
  
- <span data-ttu-id="29ee3-113">Object Relational Designer</span><span class="sxs-lookup"><span data-stu-id="29ee3-113">The Object Relational Designer</span></span>  
  
     <span data-ttu-id="29ee3-114">Ten Projektant udostępnia rozbudowany interfejs użytkownika służący do tworzenia modelu obiektów z istniejącej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="29ee3-114">This designer provides a rich user interface for creating an object model from an existing database.</span></span> <span data-ttu-id="29ee3-115">To narzędzie jest częścią środowiska IDE programu Visual Studio i najlepiej jest dostosowane do małych i średnich baz danych.</span><span class="sxs-lookup"><span data-stu-id="29ee3-115">This tool is part of the Visual Studio IDE, and is best suited to small or medium databases.</span></span>  
  
- <span data-ttu-id="29ee3-116">Narzędzie do generowania kodu SQLMetal</span><span class="sxs-lookup"><span data-stu-id="29ee3-116">The SQLMetal code-generation tool</span></span>  
  
     <span data-ttu-id="29ee3-117">To narzędzie wiersza polecenia zapewnia nieco inny zestaw opcji z projektanta O/R.</span><span class="sxs-lookup"><span data-stu-id="29ee3-117">This command-line utility provides a slightly different set of options from the O/R Designer.</span></span> <span data-ttu-id="29ee3-118">Modelowanie dużych baz danych jest najlepszym rozwiązaniem przy użyciu tego narzędzia.</span><span class="sxs-lookup"><span data-stu-id="29ee3-118">Modeling large databases is best done by using this tool.</span></span> <span data-ttu-id="29ee3-119">Aby uzyskać więcej informacji, zobacz [SqlMetal.exe (Narzędzie generowania kodu)](../../../../tools/sqlmetal-exe-code-generation-tool.md).</span><span class="sxs-lookup"><span data-stu-id="29ee3-119">For more information, see [SqlMetal.exe (Code Generation Tool)](../../../../tools/sqlmetal-exe-code-generation-tool.md).</span></span>  
  
- <span data-ttu-id="29ee3-120">Edytor kodu</span><span class="sxs-lookup"><span data-stu-id="29ee3-120">A code editor</span></span>  
  
     <span data-ttu-id="29ee3-121">Swój własny kod można napisać przy użyciu edytora kodu programu Visual Studio lub innego edytora.</span><span class="sxs-lookup"><span data-stu-id="29ee3-121">You can write your own code by using either the Visual Studio code editor or another editor.</span></span> <span data-ttu-id="29ee3-122">Firma Microsoft nie zaleca tego podejścia, które może być podatne na błędy, gdy istnieje istniejąca baza danych i może korzystać z projektanta O/R lub narzędzia SQLMetal.</span><span class="sxs-lookup"><span data-stu-id="29ee3-122">We do not recommend this approach, which can be prone to errors, when you have an existing database and can use either the O/R Designer or the SQLMetal tool.</span></span> <span data-ttu-id="29ee3-123">Jednak Edytor kodu może być cenny dla rafinacji lub modyfikacji kodu, który został już wygenerowany przy użyciu innych narzędzi.</span><span class="sxs-lookup"><span data-stu-id="29ee3-123">However, the code editor can be valuable for refining or modifying code you have already generated by using other tools.</span></span> <span data-ttu-id="29ee3-124">Aby uzyskać więcej informacji, zobacz [How to: Dostosowywanie klas jednostek przy użyciu edytora kodu](how-to-customize-entity-classes-by-using-the-code-editor.md).</span><span class="sxs-lookup"><span data-stu-id="29ee3-124">For more information, see [How to: Customize Entity Classes by Using the Code Editor](how-to-customize-entity-classes-by-using-the-code-editor.md).</span></span>  
  
### <a name="2-select-the-kind-of-code-you-want-to-generate"></a><span data-ttu-id="29ee3-125">2. Wybierz rodzaj kodu, który chcesz wygenerować.</span><span class="sxs-lookup"><span data-stu-id="29ee3-125">2. Select the kind of code you want to generate.</span></span>  
  
- <span data-ttu-id="29ee3-126">Plik kodu źródłowego C# lub Visual Basic dla mapowania opartego na atrybutach.</span><span class="sxs-lookup"><span data-stu-id="29ee3-126">A C# or Visual Basic source code file for attribute-based mapping.</span></span>  
  
     <span data-ttu-id="29ee3-127">Następnie można dołączyć ten plik kodu do projektu programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="29ee3-127">You then include this code file in your Visual Studio project.</span></span> <span data-ttu-id="29ee3-128">Aby uzyskać więcej informacji, zobacz [Mapowanie oparte na atrybutach](attribute-based-mapping.md).</span><span class="sxs-lookup"><span data-stu-id="29ee3-128">For more information, see [Attribute-Based Mapping](attribute-based-mapping.md).</span></span>  
  
- <span data-ttu-id="29ee3-129">Plik XML dla mapowania zewnętrznego.</span><span class="sxs-lookup"><span data-stu-id="29ee3-129">An XML file for external mapping.</span></span>  
  
     <span data-ttu-id="29ee3-130">Korzystając z tej metody, można zachować metadane mapowania z kodu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="29ee3-130">By using this approach, you can keep the mapping metadata out of your application code.</span></span> <span data-ttu-id="29ee3-131">Aby uzyskać więcej informacji, zobacz [Mapowanie zewnętrzne](external-mapping.md).</span><span class="sxs-lookup"><span data-stu-id="29ee3-131">For more information, see [External Mapping](external-mapping.md).</span></span>  
  
    > [!NOTE]
    > <span data-ttu-id="29ee3-132">Projektant O/R nie obsługuje generowania plików mapowania zewnętrznego.</span><span class="sxs-lookup"><span data-stu-id="29ee3-132">The O/R Designer does not support the generation of external mapping files.</span></span> <span data-ttu-id="29ee3-133">Aby zaimplementować tę funkcję, należy użyć narzędzia SQLMetal.</span><span class="sxs-lookup"><span data-stu-id="29ee3-133">You must use the SQLMetal tool to implement this feature.</span></span>  
  
- <span data-ttu-id="29ee3-134">Plik DBML, który można modyfikować przed wygenerowaniem końcowego pliku kodu.</span><span class="sxs-lookup"><span data-stu-id="29ee3-134">A DBML file, which you can modify before generating a final code file.</span></span>  
  
     <span data-ttu-id="29ee3-135">Jest to funkcja zaawansowana.</span><span class="sxs-lookup"><span data-stu-id="29ee3-135">This is an advanced feature.</span></span>  
  
### <a name="3-refine-the-code-file-to-reflect-the-needs-of-your-application"></a><span data-ttu-id="29ee3-136">3. Uściślij plik kodu w celu odzwierciedlenia potrzeb aplikacji.</span><span class="sxs-lookup"><span data-stu-id="29ee3-136">3. Refine the code file to reflect the needs of your application.</span></span>  

 <span data-ttu-id="29ee3-137">W tym celu można użyć projektanta O/R lub edytora kodu.</span><span class="sxs-lookup"><span data-stu-id="29ee3-137">For this purpose, you can use either the O/R Designer or the code editor.</span></span>  
  
## <a name="using-the-object-model"></a><span data-ttu-id="29ee3-138">Korzystanie z modelu obiektów</span><span class="sxs-lookup"><span data-stu-id="29ee3-138">Using the Object Model</span></span>  

 <span data-ttu-id="29ee3-139">Na poniższej ilustracji przedstawiono relacje między deweloperem a danymi w scenariuszu dwuwarstwowym.</span><span class="sxs-lookup"><span data-stu-id="29ee3-139">The following illustration shows the relationship between the developer and the data in a two-tier scenario.</span></span> <span data-ttu-id="29ee3-140">W przypadku innych scenariuszy zobacz [aplikacje N-warstwowe i zdalne za pomocą LINQ to SQL](n-tier-and-remote-applications-with-linq-to-sql.md).</span><span class="sxs-lookup"><span data-stu-id="29ee3-140">For other scenarios, see [N-Tier and Remote Applications with LINQ to SQL](n-tier-and-remote-applications-with-linq-to-sql.md).</span></span>  
  
 ![Zrzut ekranu pokazujący model obiektów LINQ.](./media/the-linq-to-sql-object-model/linq-object-model-two-tier.png)  
  
 <span data-ttu-id="29ee3-142">Teraz, gdy masz już model obiektów, opiszemy żądania informacji i manipulowanie danymi w tym modelu.</span><span class="sxs-lookup"><span data-stu-id="29ee3-142">Now that you have the object model, you describe information requests and manipulate data within that model.</span></span> <span data-ttu-id="29ee3-143">Myślisz o obiektach i właściwościach w modelu obiektów, a nie w odniesieniu do wierszy i kolumn bazy danych.</span><span class="sxs-lookup"><span data-stu-id="29ee3-143">You think in terms of the objects and properties in your object model and not in terms of the rows and columns of the database.</span></span> <span data-ttu-id="29ee3-144">Nie można bezpośrednio obsłużyć bazy danych.</span><span class="sxs-lookup"><span data-stu-id="29ee3-144">You do not deal directly with the database.</span></span>  
  
 <span data-ttu-id="29ee3-145">Gdy użytkownik instruuje [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] wykonać zapytanie, które zostało opisane lub wywołało `SubmitChanges()` dane, które były manipulowane, [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] komunikuje się z bazą danych w języku bazy danych.</span><span class="sxs-lookup"><span data-stu-id="29ee3-145">When you instruct [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] to either execute a query that you have described or call `SubmitChanges()` on data that you have manipulated, [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] communicates with the database in the language of the database.</span></span>  
  
 <span data-ttu-id="29ee3-146">Poniżej przedstawiono typowe kroki dotyczące użycia modelu obiektów, który został utworzony.</span><span class="sxs-lookup"><span data-stu-id="29ee3-146">The following represents typical steps for using the object model that you have created.</span></span>  
  
### <a name="1-create-queries-to-retrieve-information-from-the-database"></a><span data-ttu-id="29ee3-147">1. Utwórz zapytania, aby pobrać informacje z bazy danych.</span><span class="sxs-lookup"><span data-stu-id="29ee3-147">1. Create queries to retrieve information from the database.</span></span>  

 <span data-ttu-id="29ee3-148">Aby uzyskać więcej informacji, zobacz [pojęcia dotyczące zapytań](query-concepts.md) i [przykłady zapytań](query-examples.md).</span><span class="sxs-lookup"><span data-stu-id="29ee3-148">For more information, see [Query Concepts](query-concepts.md) and [Query Examples](query-examples.md).</span></span>  
  
### <a name="2-override-default-behaviors-for-insert-update-and-delete"></a><span data-ttu-id="29ee3-149">2. Przesłoń domyślne zachowania dla operacji INSERT, Update i DELETE.</span><span class="sxs-lookup"><span data-stu-id="29ee3-149">2. Override default behaviors for Insert, Update, and Delete.</span></span>  

 <span data-ttu-id="29ee3-150">Ta czynność jest opcjonalna.</span><span class="sxs-lookup"><span data-stu-id="29ee3-150">This step is optional.</span></span> <span data-ttu-id="29ee3-151">Aby uzyskać więcej informacji, zobacz [Dostosowywanie operacji wstawiania, aktualizowania i usuwania](customizing-insert-update-and-delete-operations.md).</span><span class="sxs-lookup"><span data-stu-id="29ee3-151">For more information, see [Customizing Insert, Update, and Delete Operations](customizing-insert-update-and-delete-operations.md).</span></span>  
  
### <a name="3-set-appropriate-options-to-detect-and-report-concurrency-conflicts"></a><span data-ttu-id="29ee3-152">3. Ustaw odpowiednie opcje wykrywania i zgłaszania konfliktów współbieżności.</span><span class="sxs-lookup"><span data-stu-id="29ee3-152">3. Set appropriate options to detect and report concurrency conflicts.</span></span>  

 <span data-ttu-id="29ee3-153">Możesz pozostawić model z wartościami domyślnymi do obsługi konfliktów współbieżności lub można go zmienić zgodnie z własnymi potrzebami.</span><span class="sxs-lookup"><span data-stu-id="29ee3-153">You can leave your model with its default values for handling concurrency conflicts, or you can change it to suit your purposes.</span></span> <span data-ttu-id="29ee3-154">Aby uzyskać więcej informacji, zobacz [How to: Określanie, które elementy członkowskie są testowane pod kątem konfliktów współbieżności](how-to-specify-which-members-are-tested-for-concurrency-conflicts.md) , i [instrukcje: Określanie, kiedy są zgłaszane wyjątki współbieżności](how-to-specify-when-concurrency-exceptions-are-thrown.md).</span><span class="sxs-lookup"><span data-stu-id="29ee3-154">For more information, see [How to: Specify Which Members are Tested for Concurrency Conflicts](how-to-specify-which-members-are-tested-for-concurrency-conflicts.md) and [How to: Specify When Concurrency Exceptions are Thrown](how-to-specify-when-concurrency-exceptions-are-thrown.md).</span></span>  
  
### <a name="4-establish-an-inheritance-hierarchy"></a><span data-ttu-id="29ee3-155">4. Ustanów hierarchię dziedziczenia.</span><span class="sxs-lookup"><span data-stu-id="29ee3-155">4. Establish an inheritance hierarchy.</span></span>  

 <span data-ttu-id="29ee3-156">Ta czynność jest opcjonalna.</span><span class="sxs-lookup"><span data-stu-id="29ee3-156">This step is optional.</span></span> <span data-ttu-id="29ee3-157">Aby uzyskać więcej informacji, zobacz [Obsługa dziedziczenia](inheritance-support.md).</span><span class="sxs-lookup"><span data-stu-id="29ee3-157">For more information, see [Inheritance Support](inheritance-support.md).</span></span>  
  
### <a name="5-provide-an-appropriate-user-interface"></a><span data-ttu-id="29ee3-158">5. Podaj odpowiedni interfejs użytkownika.</span><span class="sxs-lookup"><span data-stu-id="29ee3-158">5. Provide an appropriate user interface.</span></span>  

 <span data-ttu-id="29ee3-159">Ten krok jest opcjonalny i zależy od tego, w jaki sposób aplikacja zostanie użyta.</span><span class="sxs-lookup"><span data-stu-id="29ee3-159">This step is optional, and depends on how your application will be used.</span></span>  
  
### <a name="6-debug-and-test-your-application"></a><span data-ttu-id="29ee3-160">6. Debuguj i przetestuj aplikację.</span><span class="sxs-lookup"><span data-stu-id="29ee3-160">6. Debug and test your application.</span></span>  

 <span data-ttu-id="29ee3-161">Aby uzyskać więcej informacji, zobacz [obsługa debugowania](debugging-support.md).</span><span class="sxs-lookup"><span data-stu-id="29ee3-161">For more information, see [Debugging Support](debugging-support.md).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="29ee3-162">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="29ee3-162">See also</span></span>

- [<span data-ttu-id="29ee3-163">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="29ee3-163">Getting Started</span></span>](getting-started.md)
- [<span data-ttu-id="29ee3-164">Tworzenie modelu obiektu</span><span class="sxs-lookup"><span data-stu-id="29ee3-164">Creating the Object Model</span></span>](creating-the-object-model.md)
- [<span data-ttu-id="29ee3-165">Procedury składowane</span><span class="sxs-lookup"><span data-stu-id="29ee3-165">Stored Procedures</span></span>](stored-procedures.md)
