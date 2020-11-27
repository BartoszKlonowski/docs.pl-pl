---
title: Wywoływanie walidacji działania
ms.date: 03/30/2017
ms.assetid: 22bef766-c505-4fd4-ac0f-7b363b238969
ms.openlocfilehash: 95e6b22fe9814133df080b1faadcc4be32b60bf9
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96279808"
---
# <a name="invoking-activity-validation"></a><span data-ttu-id="66747-102">Wywoływanie walidacji działania</span><span class="sxs-lookup"><span data-stu-id="66747-102">Invoking Activity Validation</span></span>

<span data-ttu-id="66747-103">Walidacja działań zapewnia metodę w celu identyfikowania i zgłaszania błędów w konfiguracji dowolnego działania przed jego wykonaniem.</span><span class="sxs-lookup"><span data-stu-id="66747-103">Activity validation provides a method to identify and report errors in any activity’s configuration prior to its execution.</span></span> <span data-ttu-id="66747-104">Walidacja występuje, gdy przepływ pracy jest modyfikowany w Projektancie przepływu pracy, a wszystkie błędy lub ostrzeżenia dotyczące walidacji są wyświetlane w Projektancie przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="66747-104">Validation occurs when a workflow is modified in the workflow designer and any validation errors or warnings are displayed in the workflow designer.</span></span> <span data-ttu-id="66747-105">Sprawdzanie poprawności występuje również w czasie wykonywania, gdy przepływ pracy jest wywoływany, a jeśli wystąpią błędy walidacji, <xref:System.Activities.InvalidWorkflowException> jest generowany przez domyślną logikę walidacji.</span><span class="sxs-lookup"><span data-stu-id="66747-105">Validation also occurs at run time when a workflow is invoked and if any validation errors occur, an <xref:System.Activities.InvalidWorkflowException> is thrown by the default validation logic.</span></span> <span data-ttu-id="66747-106">Windows Workflow Foundation (WF) zawiera <xref:System.Activities.Validation.ActivityValidationServices> klasę, która może być używana przez deweloperów aplikacji i narzędzi do pracy w celu jawnego sprawdzania poprawności działania.</span><span class="sxs-lookup"><span data-stu-id="66747-106">Windows Workflow Foundation (WF) provides the <xref:System.Activities.Validation.ActivityValidationServices> class that can be used by workflow application and tooling developers to explicitly validate an activity.</span></span> <span data-ttu-id="66747-107">W tym temacie opisano sposób użycia <xref:System.Activities.Validation.ActivityValidationServices> programu w celu przeprowadzenia walidacji działania.</span><span class="sxs-lookup"><span data-stu-id="66747-107">This topic describes how to use <xref:System.Activities.Validation.ActivityValidationServices> to perform activity validation.</span></span>  
  
## <a name="using-activityvalidationservices"></a><span data-ttu-id="66747-108">Korzystanie z ActivityValidationServices</span><span class="sxs-lookup"><span data-stu-id="66747-108">Using ActivityValidationServices</span></span>  

 <span data-ttu-id="66747-109"><xref:System.Activities.Validation.ActivityValidationServices> ma dwa <xref:System.Activities.Validation.ActivityValidationServices.Validate%2A> przeciążenia, które są używane do wywołania logiki walidacji działania.</span><span class="sxs-lookup"><span data-stu-id="66747-109"><xref:System.Activities.Validation.ActivityValidationServices> has two <xref:System.Activities.Validation.ActivityValidationServices.Validate%2A> overloads that are used to invoke an activity’s validation logic.</span></span> <span data-ttu-id="66747-110">Pierwsze Przeciążenie powoduje sprawdzenie poprawności działania głównego i zwrócenie kolekcji błędów i ostrzeżeń walidacji.</span><span class="sxs-lookup"><span data-stu-id="66747-110">The first overload takes the root activity to be validated and returns a collection of validation errors and warnings.</span></span> <span data-ttu-id="66747-111">W poniższym przykładzie `Add` użyto niestandardowego działania, które ma dwa wymagane argumenty.</span><span class="sxs-lookup"><span data-stu-id="66747-111">In the following example, a custom `Add` activity is used that has two required arguments.</span></span>  
  
```csharp  
public sealed class Add : CodeActivity<int>  
{  
    [RequiredArgument]  
    public InArgument<int> Operand1 { get; set; }  
  
    [RequiredArgument]  
    public InArgument<int> Operand2 { get; set; }  
  
    protected override int Execute(CodeActivityContext context)  
    {  
        return Operand1.Get(context) + Operand2.Get(context);  
    }  
}  
```  
  
 <span data-ttu-id="66747-112">To `Add` działanie jest używane wewnątrz <xref:System.Activities.Statements.Sequence> , ale jego dwa wymagane argumenty nie są powiązane, jak pokazano w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="66747-112">The `Add` activity is used inside a <xref:System.Activities.Statements.Sequence>, but its two required arguments are not bound, as shown in the following example.</span></span>  
  
```csharp  
Variable<int> Operand1 = new Variable<int>{ Default = 10 };  
Variable<int> Operand2 = new Variable<int>{ Default = 15 };  
Variable<int> Result = new Variable<int>();  
  
Activity wf = new Sequence  
{  
    Variables = { Operand1, Operand2, Result },  
    Activities =
    {  
        new Add(),  
        new WriteLine  
        {  
            Text = new InArgument<string>(env => "The result is " + Result.Get(env))  
        }  
    }  
};  
```  
  
 <span data-ttu-id="66747-113">Ten przepływ pracy można zweryfikować, wywołując metodę <xref:System.Activities.Validation.ActivityValidationServices.Validate%2A> .</span><span class="sxs-lookup"><span data-stu-id="66747-113">This workflow can be validated by calling <xref:System.Activities.Validation.ActivityValidationServices.Validate%2A>.</span></span> <span data-ttu-id="66747-114"><xref:System.Activities.Validation.ActivityValidationServices.Validate%2A> Zwraca kolekcję błędów walidacji lub ostrzeżeń zawartych w działaniu i wszelkich elementów podrzędnych, jak pokazano w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="66747-114"><xref:System.Activities.Validation.ActivityValidationServices.Validate%2A> returns a collection of any validation errors or warnings contained by the activity and any children, as shown in the following example.</span></span>  
  
```csharp  
ValidationResults results = ActivityValidationServices.Validate(wf);  
  
if (results.Errors.Count == 0 && results.Warnings.Count == 0)  
{  
    Console.WriteLine("No warnings or errors");  
}  
else  
{  
    foreach (ValidationError error in results.Errors)  
    {  
        Console.WriteLine("Error: {0}", error.Message);  
    }  
    foreach (ValidationError warning in results.Warnings)  
    {  
        Console.WriteLine("Warning: {0}", warning.Message);  
    }  
}  
```  
  
 <span data-ttu-id="66747-115">Gdy <xref:System.Activities.Validation.ActivityValidationServices.Validate%2A> jest wywoływana dla tego przykładowego przepływu pracy, zwracane są dwa błędy walidacji.</span><span class="sxs-lookup"><span data-stu-id="66747-115">When <xref:System.Activities.Validation.ActivityValidationServices.Validate%2A> is called on this sample workflow, two validation errors are returned.</span></span>  
  
 <span data-ttu-id="66747-116">**Błąd: nie podano wartości dla wymaganego argumentu działania "Operand2".**</span><span class="sxs-lookup"><span data-stu-id="66747-116">**Error: Value for a required activity argument 'Operand2' was not supplied.**</span></span>  
<span data-ttu-id="66747-117">**Błąd: nie podano wartości dla wymaganego argumentu działania "Operand1".**</span><span class="sxs-lookup"><span data-stu-id="66747-117">**Error: Value for a required activity argument 'Operand1' was not supplied.**</span></span>  <span data-ttu-id="66747-118">Jeśli ten przepływ pracy został wywołany, <xref:System.Activities.InvalidWorkflowException> zostałby zgłoszony, jak pokazano w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="66747-118">If this workflow was invoked, an <xref:System.Activities.InvalidWorkflowException> would be thrown, as shown in the following example.</span></span>  
  
```csharp  
try  
{  
    WorkflowInvoker.Invoke(wf);  
}  
catch (Exception ex)  
{  
    Console.WriteLine(ex);  
}  
```  
  
 <span data-ttu-id="66747-119">**System. Activities. InvalidWorkflowException:**</span><span class="sxs-lookup"><span data-stu-id="66747-119">**System.Activities.InvalidWorkflowException:**</span></span>  
<span data-ttu-id="66747-120">**Napotkano następujące błędy podczas przetwarzania drzewa przepływu pracy:** 
 **"Add": nie podano wartości dla wymaganego argumentu działania "Operand2".** 
 **"Add": nie podano wartości dla wymaganego argumentu działania "Operand1".**</span><span class="sxs-lookup"><span data-stu-id="66747-120">**The following errors were encountered while processing the workflow tree:**
 **'Add': Value for a required activity argument 'Operand2' was not supplied.**
 **'Add': Value for a required activity argument 'Operand1' was not supplied.**</span></span>  <span data-ttu-id="66747-121">Aby ten przykładowy przepływ pracy był prawidłowy, muszą być powiązane dwa wymagane argumenty `Add` działania.</span><span class="sxs-lookup"><span data-stu-id="66747-121">For this example workflow to be valid, the two required arguments of the `Add` activity must be bound.</span></span> <span data-ttu-id="66747-122">W poniższym przykładzie dwa wymagane argumenty są powiązane ze zmiennymi przepływu pracy wraz z wartością wyniku.</span><span class="sxs-lookup"><span data-stu-id="66747-122">In the following example, the two required arguments are bound to workflow variables along with the result value.</span></span> <span data-ttu-id="66747-123">W tym przykładzie <xref:System.Activities.Activity%601.Result%2A> argument jest powiązany wraz z dwoma wymaganymi argumentami.</span><span class="sxs-lookup"><span data-stu-id="66747-123">In this example the <xref:System.Activities.Activity%601.Result%2A> argument is bound along with the two required arguments.</span></span> <span data-ttu-id="66747-124"><xref:System.Activities.Activity%601.Result%2A>Argument nie musi być powiązany i nie powoduje błędu walidacji, jeśli nie jest.</span><span class="sxs-lookup"><span data-stu-id="66747-124">The <xref:System.Activities.Activity%601.Result%2A> argument is not required to be bound and does not cause a validation error if it is not.</span></span> <span data-ttu-id="66747-125">Jest odpowiedzialny za utworzenie powiązania przez autora przepływu pracy, <xref:System.Activities.Activity%601.Result%2A> jeśli jego wartość jest używana w innym miejscu w przepływie pracy.</span><span class="sxs-lookup"><span data-stu-id="66747-125">It is the responsibility of the workflow author to bind <xref:System.Activities.Activity%601.Result%2A> if its value is used elsewhere in the workflow.</span></span>  
  
```csharp  
new Add  
{  
    Operand1 = Operand1,  
    Operand2 = Operand2,  
    Result = Result  
}  
```  
  
### <a name="validating-required-arguments-on-the-root-activity"></a><span data-ttu-id="66747-126">Weryfikowanie wymaganych argumentów dla działania głównego</span><span class="sxs-lookup"><span data-stu-id="66747-126">Validating Required Arguments on the Root Activity</span></span>  

 <span data-ttu-id="66747-127">Jeśli działanie główne przepływu pracy ma argumenty, nie są one powiązane, dopóki przepływ pracy nie zostanie wywołany, a parametry są przekazane do przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="66747-127">If the root activity of a workflow has arguments, these are not bound until the workflow is invoked and parameters are passed to the workflow.</span></span> <span data-ttu-id="66747-128">Następujący przepływ pracy przeszedł sprawdzanie poprawności, ale jest generowany wyjątek, jeśli przepływ pracy jest wywoływany bez przekazywania w wymaganych argumentach, jak pokazano w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="66747-128">The following workflow passes validation, but an exception is thrown if the workflow is invoked without passing in the required arguments, as shown in the following example.</span></span>  
  
```csharp  
Activity wf = new Add();  
  
ValidationResults results = ActivityValidationServices.Validate(wf);  
// results has no errors or warnings, but when the workflow  
// is invoked, an InvalidWorkflowException is thrown.  
try  
{  
    WorkflowInvoker.Invoke(wf);  
}  
catch (Exception ex)  
{  
    Console.WriteLine(ex);  
}  
```  
  
 <span data-ttu-id="66747-129">**System. ArgumentException: Ustawienia argumentu działania głównego są nieprawidłowe.**</span><span class="sxs-lookup"><span data-stu-id="66747-129">**System.ArgumentException: The root activity's argument settings are incorrect.**</span></span>  
<span data-ttu-id="66747-130">**Popraw definicję przepływu pracy lub podaj wartości wejściowe, aby naprawić te błędy:** 
 **"Add": nie podano wartości dla wymaganego argumentu działania "Operand2".** 
 **"Add": nie podano wartości dla wymaganego argumentu działania "Operand1".**</span><span class="sxs-lookup"><span data-stu-id="66747-130">**Either fix the workflow definition or supply input values to fix these errors:**
 **'Add': Value for a required activity argument 'Operand2' was not supplied.**
 **'Add': Value for a required activity argument 'Operand1' was not supplied.**</span></span>  <span data-ttu-id="66747-131">Po przekazaniu prawidłowych argumentów przepływ pracy zakończy się pomyślnie, jak pokazano w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="66747-131">After the correct arguments are passed, the workflow completes successfully, as shown in the following example.</span></span>  
  
```csharp  
Add wf = new Add();  
  
ValidationResults results = ActivityValidationServices.Validate(wf);  
// results has no errors or warnings, and the workflow completes  
// successfully because the required arguments were passed.  
try  
{  
    Dictionary<string, object> wfparams = new Dictionary<string, object>  
    {  
        { "Operand1", 10 },  
        { "Operand2", 15 }  
    };  
  
    int result = WorkflowInvoker.Invoke(wf, wfparams);  
    Console.WriteLine("Result: {0}", result);  
}  
catch (Exception ex)  
{  
    Console.WriteLine(ex);  
}  
```  
  
> [!NOTE]
> <span data-ttu-id="66747-132">W tym przykładzie działanie główne zostało zadeklarowane jako `Add` zamiast `Activity` tak jak w poprzednim przykładzie.</span><span class="sxs-lookup"><span data-stu-id="66747-132">In this example, the root activity was declared as `Add` instead of `Activity` as in the previous example.</span></span> <span data-ttu-id="66747-133">Dzięki temu `WorkflowInvoker.Invoke` Metoda zwraca pojedynczą liczbę całkowitą, która reprezentuje wyniki `Add` działania zamiast słownika `out` argumentów.</span><span class="sxs-lookup"><span data-stu-id="66747-133">This allows the `WorkflowInvoker.Invoke` method to return a single integer that represents the results of the `Add` activity instead of a dictionary of `out` arguments.</span></span> <span data-ttu-id="66747-134">Zmienna `wf` mogła być również zadeklarowana jako `Activity<int>` .</span><span class="sxs-lookup"><span data-stu-id="66747-134">The variable `wf` could also have been declared as `Activity<int>`.</span></span>  
  
 <span data-ttu-id="66747-135">Podczas sprawdzania poprawności argumentów głównych jest odpowiedzialna aplikacja hosta, aby upewnić się, że wszystkie wymagane argumenty są przekazane po wywołaniu przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="66747-135">When validating root arguments, it is the responsibility of the host application to ensure that all required arguments are passed when the workflow is invoked.</span></span>  
  
### <a name="invoking-imperative-code-based-validation"></a><span data-ttu-id="66747-136">Wywoływanie bezwzględnej Code-Based walidacji</span><span class="sxs-lookup"><span data-stu-id="66747-136">Invoking Imperative Code-Based Validation</span></span>

<span data-ttu-id="66747-137">Bezwzględna Walidacja oparta na kodzie zapewnia prosty sposób, aby działanie zapewniało jego weryfikację i jest dostępne dla działań, które pochodzą z <xref:System.Activities.CodeActivity> , <xref:System.Activities.AsyncCodeActivity> i <xref:System.Activities.NativeActivity> .</span><span class="sxs-lookup"><span data-stu-id="66747-137">Imperative code-based validation provides a simple way for an activity to provide validation about itself, and is available for activities that derive from <xref:System.Activities.CodeActivity>, <xref:System.Activities.AsyncCodeActivity>, and <xref:System.Activities.NativeActivity>.</span></span> <span data-ttu-id="66747-138">Kod sprawdzania poprawności, który określa wszelkie błędy walidacji lub ostrzeżenia są dodawane do działania.</span><span class="sxs-lookup"><span data-stu-id="66747-138">Validation code that determines any validation errors or warnings is added to the activity.</span></span> <span data-ttu-id="66747-139">Po wywołaniu walidacji dla działania te ostrzeżenia lub błędy są zawarte w kolekcji zwróconej przez wywołanie metody <xref:System.Activities.Validation.ActivityValidationServices.Validate%2A> .</span><span class="sxs-lookup"><span data-stu-id="66747-139">When validation is invoked on the activity, these warnings or errors are contained in the collection returned by the call to <xref:System.Activities.Validation.ActivityValidationServices.Validate%2A>.</span></span> <span data-ttu-id="66747-140">W poniższym przykładzie `CreateProduct` zdefiniowano działanie.</span><span class="sxs-lookup"><span data-stu-id="66747-140">In the following example, a `CreateProduct` activity is defined.</span></span> <span data-ttu-id="66747-141">Jeśli wartość `Cost` jest większa niż `Price` , do metadanych w przesłonięciu zostanie dodany błąd walidacji <xref:System.Activities.CodeActivity.CacheMetadata%2A> .</span><span class="sxs-lookup"><span data-stu-id="66747-141">If the `Cost` is greater than the `Price`, a validation error is added to the metadata in the <xref:System.Activities.CodeActivity.CacheMetadata%2A> override.</span></span>  
  
```csharp  
public sealed class CreateProduct : CodeActivity  
{  
    public double Price { get; set; }  
    public double Cost { get; set; }  
  
    // [RequiredArgument] attribute will generate a validation error
    // if the Description argument is not set.  
    [RequiredArgument]  
    public InArgument<string> Description { get; set; }  
  
    protected override void CacheMetadata(CodeActivityMetadata metadata)  
    {  
        base.CacheMetadata(metadata);  
        // Determine when the activity has been configured in an invalid way.  
        if (this.Cost > this.Price)  
        {  
            // Add a validation error with a custom message.  
            metadata.AddValidationError("The Cost must be less than or equal to the Price.");  
        }  
    }  
  
    protected override void Execute(CodeActivityContext context)  
    {  
        // Not needed for the sample.  
    }  
}  
```  
  
 <span data-ttu-id="66747-142">W tym przykładzie przepływ pracy jest konfigurowany za pomocą `CreateProduct` działania.</span><span class="sxs-lookup"><span data-stu-id="66747-142">In this example, a workflow is configured using the `CreateProduct` activity.</span></span> <span data-ttu-id="66747-143">W tym przepływie pracy `Cost` jest większy niż `Price` , a wymagany `Description` argument nie jest ustawiony.</span><span class="sxs-lookup"><span data-stu-id="66747-143">In this workflow, the `Cost` is greater than the `Price`, and the required `Description` argument is not set.</span></span> <span data-ttu-id="66747-144">Po wywołaniu walidacji zwracane są następujące błędy.</span><span class="sxs-lookup"><span data-stu-id="66747-144">When validation is invoked, the following errors are returned.</span></span>  
  
```csharp  
Activity wf = new Sequence  
{  
    Activities =
    {  
        new CreateProduct  
        {  
            Cost = 75.00,  
            Price = 55.00  
            // Cost > Price and required Description argument not set.  
        },  
        new WriteLine  
        {  
            Text = "Product added."  
        }  
    }  
};  
  
ValidationResults results = ActivityValidationServices.Validate(wf);  
  
if (results.Errors.Count == 0 && results.Warnings.Count == 0)  
{  
    Console.WriteLine("No warnings or errors");  
}  
else  
{  
    foreach (ValidationError error in results.Errors)  
    {  
        Console.WriteLine("Error: {0}", error.Message);  
    }  
    foreach (ValidationError warning in results.Warnings)  
    {  
        Console.WriteLine("Warning: {0}", warning.Message);  
    }  
}  
```  
  
 <span data-ttu-id="66747-145">**Błąd: koszt nie może być większy niż cena.**</span><span class="sxs-lookup"><span data-stu-id="66747-145">**Error: The Cost must be less than or equal to the Price.**</span></span>  
<span data-ttu-id="66747-146">**Błąd: nie podano wartości dla wymaganego argumentu działania "Description".**</span><span class="sxs-lookup"><span data-stu-id="66747-146">**Error: Value for a required activity argument 'Description' was not supplied.**</span></span>
> [!NOTE]
> <span data-ttu-id="66747-147">Autorzy działań niestandardowych mogą zapewnić logikę walidacji w <xref:System.Activities.CodeActivity.CacheMetadata%2A> przesłonięciu działania.</span><span class="sxs-lookup"><span data-stu-id="66747-147">Custom activity authors can provide validation logic in an activity's <xref:System.Activities.CodeActivity.CacheMetadata%2A> override.</span></span> <span data-ttu-id="66747-148">Wszystkie wyjątki zgłoszone przez <xref:System.Activities.CodeActivity.CacheMetadata%2A> nie są traktowane jako błędy walidacji.</span><span class="sxs-lookup"><span data-stu-id="66747-148">Any exceptions that are thrown from <xref:System.Activities.CodeActivity.CacheMetadata%2A> are not treated as validation errors.</span></span> <span data-ttu-id="66747-149">Te wyjątki spowodują wyjście z wywołania <xref:System.Activities.Validation.ActivityValidationServices.Validate%2A> i muszą być obsługiwane przez wywołującego.</span><span class="sxs-lookup"><span data-stu-id="66747-149">These exceptions will escape from the call to <xref:System.Activities.Validation.ActivityValidationServices.Validate%2A> and must be handled by the caller.</span></span>  
  
## <a name="using-validationsettings"></a><span data-ttu-id="66747-150">Korzystanie z Właściwość</span><span class="sxs-lookup"><span data-stu-id="66747-150">Using ValidationSettings</span></span>  

 <span data-ttu-id="66747-151">Domyślnie wszystkie działania w drzewie aktywności są oceniane, gdy Walidacja jest wywoływana przez <xref:System.Activities.Validation.ActivityValidationServices> .</span><span class="sxs-lookup"><span data-stu-id="66747-151">By default, all activities in the activity tree are evaluated when validation is invoked by <xref:System.Activities.Validation.ActivityValidationServices>.</span></span> <span data-ttu-id="66747-152"><xref:System.Activities.Validation.ValidationSettings> umożliwia dostosowanie walidacji na kilka różnych sposobów przez skonfigurowanie jej trzech właściwości.</span><span class="sxs-lookup"><span data-stu-id="66747-152"><xref:System.Activities.Validation.ValidationSettings> allows the validation to be customized in several different ways by configuring its three properties.</span></span> <span data-ttu-id="66747-153"><xref:System.Activities.Validation.ValidationSettings.SingleLevel%2A> Określa, czy moduł walidacji ma przewidzieć całe drzewo aktywności, czy ma zastosowanie tylko logiki walidacji do podanego działania.</span><span class="sxs-lookup"><span data-stu-id="66747-153"><xref:System.Activities.Validation.ValidationSettings.SingleLevel%2A> specifies whether the validator should walk the entire activity tree or only apply validation logic to the supplied activity.</span></span> <span data-ttu-id="66747-154">Wartością domyślną tego ustawienia jest `false` .</span><span class="sxs-lookup"><span data-stu-id="66747-154">The default for this value is `false`.</span></span> <span data-ttu-id="66747-155"><xref:System.Activities.Validation.ValidationSettings.AdditionalConstraints%2A> określa dodatkowe mapowanie ograniczeń z typu do listy ograniczeń.</span><span class="sxs-lookup"><span data-stu-id="66747-155"><xref:System.Activities.Validation.ValidationSettings.AdditionalConstraints%2A> specifies additional constraint mapping from a type to a list of constraints.</span></span> <span data-ttu-id="66747-156">W przypadku typu podstawowego każdego działania w drzewie aktywności jest wyszukiwany <xref:System.Activities.Validation.ValidationSettings.AdditionalConstraints%2A> .</span><span class="sxs-lookup"><span data-stu-id="66747-156">For the base type of each activity in the activity tree being validated there is a lookup into <xref:System.Activities.Validation.ValidationSettings.AdditionalConstraints%2A>.</span></span> <span data-ttu-id="66747-157">Jeśli zostanie znaleziona zgodna lista ograniczeń, wszystkie ograniczenia na liście są oceniane dla działania.</span><span class="sxs-lookup"><span data-stu-id="66747-157">If a matching constraint list is found, all constraints in the list are evaluated for the activity.</span></span> <span data-ttu-id="66747-158"><xref:System.Activities.Validation.ValidationSettings.OnlyUseAdditionalConstraints%2A> Określa, czy moduł walidacji ma oszacować wszystkie ograniczenia, czy tylko te określone w <xref:System.Activities.Validation.ValidationSettings.AdditionalConstraints%2A> .</span><span class="sxs-lookup"><span data-stu-id="66747-158"><xref:System.Activities.Validation.ValidationSettings.OnlyUseAdditionalConstraints%2A> specifies whether the validator should evaluate all constraints or only those specified in <xref:System.Activities.Validation.ValidationSettings.AdditionalConstraints%2A>.</span></span> <span data-ttu-id="66747-159">Wartość domyślna to `false`.</span><span class="sxs-lookup"><span data-stu-id="66747-159">The default value is `false`.</span></span> <span data-ttu-id="66747-160"><xref:System.Activities.Validation.ValidationSettings.AdditionalConstraints%2A> i <xref:System.Activities.Validation.ValidationSettings.OnlyUseAdditionalConstraints%2A> są przydatne dla autorów hostów przepływu pracy do dodawania dodatkowej weryfikacji dla przepływów pracy, takich jak ograniczenia zasad dla narzędzi, takich jak FxCop.</span><span class="sxs-lookup"><span data-stu-id="66747-160"><xref:System.Activities.Validation.ValidationSettings.AdditionalConstraints%2A> and <xref:System.Activities.Validation.ValidationSettings.OnlyUseAdditionalConstraints%2A> are useful for workflow host authors to add additional validation for workflows, such as policy constraints for tools such as FxCop.</span></span> <span data-ttu-id="66747-161">Aby uzyskać więcej informacji o ograniczeniach, zobacz [ograniczenia deklaratywne](declarative-constraints.md).</span><span class="sxs-lookup"><span data-stu-id="66747-161">For more information about constraints, see [Declarative Constraints](declarative-constraints.md).</span></span>  
  
 <span data-ttu-id="66747-162">Aby użyć <xref:System.Activities.Validation.ValidationSettings> , skonfiguruj żądane właściwości, a następnie Przekaż je w wywołaniu <xref:System.Activities.Validation.ActivityValidationServices.Validate%2A> .</span><span class="sxs-lookup"><span data-stu-id="66747-162">To use <xref:System.Activities.Validation.ValidationSettings>, configure the desired properties, and then pass it in the call to <xref:System.Activities.Validation.ActivityValidationServices.Validate%2A>.</span></span> <span data-ttu-id="66747-163">W tym przykładzie zostanie zweryfikowany przepływ pracy, który składa się <xref:System.Activities.Statements.Sequence> z niestandardowym `Add` działaniem.</span><span class="sxs-lookup"><span data-stu-id="66747-163">In this example, a workflow that consists of a <xref:System.Activities.Statements.Sequence> with a custom `Add` activity is validated.</span></span> <span data-ttu-id="66747-164">`Add`Działanie ma dwa wymagane argumenty.</span><span class="sxs-lookup"><span data-stu-id="66747-164">The `Add` activity has two required arguments.</span></span>  
  
```csharp  
public sealed class Add : CodeActivity<int>  
{  
    [RequiredArgument]  
    public InArgument<int> Operand1 { get; set; }  
  
    [RequiredArgument]  
    public InArgument<int> Operand2 { get; set; }  
  
    protected override int Execute(CodeActivityContext context)  
    {  
        return Operand1.Get(context) + Operand2.Get(context);  
    }  
}  
```  
  
 <span data-ttu-id="66747-165">Poniższe `Add` działanie jest używane w <xref:System.Activities.Statements.Sequence> , ale jego dwa wymagane argumenty nie są powiązane.</span><span class="sxs-lookup"><span data-stu-id="66747-165">The following `Add` activity is used in a <xref:System.Activities.Statements.Sequence>, but its two required arguments are not bound.</span></span>  
  
```csharp  
Variable<int> Operand1 = new Variable<int> { Default = 10 };  
Variable<int> Operand2 = new Variable<int> { Default = 15 };  
Variable<int> Result = new Variable<int>();  
  
Activity wf = new Sequence  
{  
    Variables = { Operand1, Operand2, Result },  
    Activities =
    {  
        new Add(),  
        new WriteLine  
        {  
            Text = new InArgument<string>(env => "The result is " + Result.Get(env))  
        }  
    }  
};  
```  
  
 <span data-ttu-id="66747-166">W poniższym przykładzie Walidacja jest wykonywana z <xref:System.Activities.Validation.ValidationSettings.SingleLevel%2A> ustawioną na `true` , więc <xref:System.Activities.Statements.Sequence> sprawdzane jest tylko działanie główne.</span><span class="sxs-lookup"><span data-stu-id="66747-166">For the following example, validation is performed with <xref:System.Activities.Validation.ValidationSettings.SingleLevel%2A> set to `true`, so only the root <xref:System.Activities.Statements.Sequence> activity is validated.</span></span>  
  
```csharp  
ValidationSettings settings = new ValidationSettings  
{  
    SingleLevel = true  
};  
  
ValidationResults results = ActivityValidationServices.Validate(wf, settings);  
  
if (results.Errors.Count == 0 && results.Warnings.Count == 0)  
{  
    Console.WriteLine("No warnings or errors");  
}  
else  
{  
    foreach (ValidationError error in results.Errors)  
    {  
        Console.WriteLine("Error: {0}", error.Message);  
    }  
    foreach (ValidationError warning in results.Warnings)  
    {  
        Console.WriteLine("Warning: {0}", warning.Message);  
    }  
}  
```  
  
 <span data-ttu-id="66747-167">Ten kod wyświetla następujące dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="66747-167">This code displays the following output:</span></span>  
  
 <span data-ttu-id="66747-168">**Brak ostrzeżeń lub błędów** Mimo `Add` że działanie ma wymagane argumenty, które nie są powiązane, walidacja zakończyła się pomyślnie, ponieważ oceniane jest tylko działanie główne.</span><span class="sxs-lookup"><span data-stu-id="66747-168">**No warnings or errors** Even though the `Add` activity has required arguments that are not bound, validation is successful because only the root activity is evaluated.</span></span> <span data-ttu-id="66747-169">Ten typ weryfikacji jest przydatny do sprawdzania poprawności tylko określonych elementów w drzewie aktywności, takich jak walidacja zmiany właściwości pojedynczego działania w projektancie.</span><span class="sxs-lookup"><span data-stu-id="66747-169">This type of validation is useful for validating only specific elements in an activity tree, such as validation of a property change of a single activity in a designer.</span></span> <span data-ttu-id="66747-170">Należy pamiętać, że w przypadku wywołania tego przepływu pracy jest oceniana pełna Walidacja skonfigurowana w przepływie pracy i <xref:System.Activities.InvalidWorkflowException> zostałaby zgłoszona.</span><span class="sxs-lookup"><span data-stu-id="66747-170">Note that if this workflow is invoked, the full validation configured in the workflow is evaluated and an <xref:System.Activities.InvalidWorkflowException> would be thrown.</span></span> <span data-ttu-id="66747-171"><xref:System.Activities.Validation.ActivityValidationServices> i <xref:System.Activities.Validation.ValidationSettings> skonfigurować wyłącznie sprawdzanie poprawności wywoływane przez hosta, a nie sprawdzanie poprawności, które występuje po wywołaniu przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="66747-171"><xref:System.Activities.Validation.ActivityValidationServices> and <xref:System.Activities.Validation.ValidationSettings> configure only validation explicitly invoked by the host, and not the validation that occurs when a workflow is invoked.</span></span>
