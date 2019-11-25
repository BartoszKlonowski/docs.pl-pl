---
title: Informacje o obiekcie wywołującym
description: Opisuje sposób używania atrybutów argumentów informacji o wywołującym do uzyskiwania informacji o wywołującym z metody.
ms.date: 11/04/2019
ms.openlocfilehash: d995b37149277b7c7d1b6217ee484d3c90a7f8b3
ms.sourcegitcommit: f348c84443380a1959294cdf12babcb804cfa987
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/12/2019
ms.locfileid: "73976798"
---
# <a name="caller-information"></a><span data-ttu-id="d6727-103">Informacje o obiekcie wywołującym</span><span class="sxs-lookup"><span data-stu-id="d6727-103">Caller information</span></span>

<span data-ttu-id="d6727-104">Przy użyciu atrybutów informacji o obiekcie wywołującym można uzyskać informacje o obiekcie wywołującym metodę.</span><span class="sxs-lookup"><span data-stu-id="d6727-104">By using Caller Info attributes, you can obtain information about the caller to a method.</span></span> <span data-ttu-id="d6727-105">Można uzyskać ścieżkę pliku kodu źródłowego, numer wiersza kodu źródłowego i nazwę elementu członkowskiego obiektu wywołującego.</span><span class="sxs-lookup"><span data-stu-id="d6727-105">You can obtain file path of the source code, the line number in the source code, and the member name of the caller.</span></span> <span data-ttu-id="d6727-106">Te informacje są przydatne do śledzenia, debugowania i tworzenia narzędzi diagnostycznych.</span><span class="sxs-lookup"><span data-stu-id="d6727-106">This information is helpful for tracing, debugging, and creating diagnostic tools.</span></span>

<span data-ttu-id="d6727-107">Aby uzyskać te informacje, należy użyć atrybutów stosowanych do opcjonalnych parametrów, z których każdy ma wartość domyślną.</span><span class="sxs-lookup"><span data-stu-id="d6727-107">To obtain this information, you use attributes that are applied to optional parameters, each of which has a default value.</span></span> <span data-ttu-id="d6727-108">W poniższej tabeli wymieniono atrybuty informacji o wywołującym, które są zdefiniowane w przestrzeni nazw [System. Runtime. CompilerServices](/dotnet/api/system.runtime.compilerservices) :</span><span class="sxs-lookup"><span data-stu-id="d6727-108">The following table lists the Caller Info attributes that are defined in the [System.Runtime.CompilerServices](/dotnet/api/system.runtime.compilerservices) namespace:</span></span>

|<span data-ttu-id="d6727-109">Atrybut</span><span class="sxs-lookup"><span data-stu-id="d6727-109">Attribute</span></span>|<span data-ttu-id="d6727-110">Opis</span><span class="sxs-lookup"><span data-stu-id="d6727-110">Description</span></span>|<span data-ttu-id="d6727-111">Typ</span><span class="sxs-lookup"><span data-stu-id="d6727-111">Type</span></span>|
|---------|-----------|----|
|[<span data-ttu-id="d6727-112">CallerFilePath</span><span class="sxs-lookup"><span data-stu-id="d6727-112">CallerFilePath</span></span>](/dotnet/api/system.runtime.compilerservices.callerfilepathattribute)|<span data-ttu-id="d6727-113">Pełna ścieżka pliku źródłowego zawierającego obiekt wywołujący.</span><span class="sxs-lookup"><span data-stu-id="d6727-113">Full path of the source file that contains the caller.</span></span> <span data-ttu-id="d6727-114">Jest to ścieżka pliku w czasie kompilacji.</span><span class="sxs-lookup"><span data-stu-id="d6727-114">This is the file path at compile time.</span></span>|`String`
|[<span data-ttu-id="d6727-115">CallerLineNumber</span><span class="sxs-lookup"><span data-stu-id="d6727-115">CallerLineNumber</span></span>](/dotnet/api/system.runtime.compilerservices.callerlinenumberattribute)|<span data-ttu-id="d6727-116">Numer wiersza w pliku źródłowym, w którym to wierszu jest wywoływana metoda.</span><span class="sxs-lookup"><span data-stu-id="d6727-116">Line number in the source file at which the method is called.</span></span>|`Integer`|
|[<span data-ttu-id="d6727-117">CallerMemberName</span><span class="sxs-lookup"><span data-stu-id="d6727-117">CallerMemberName</span></span>](/dotnet/api/system.runtime.compilerservices.callermembernameattribute)|<span data-ttu-id="d6727-118">Nazwa metody lub właściwości obiektu wywołującego.</span><span class="sxs-lookup"><span data-stu-id="d6727-118">Method or property name of the caller.</span></span> <span data-ttu-id="d6727-119">Zobacz sekcję nazwy elementów członkowskich w dalszej części tego tematu.</span><span class="sxs-lookup"><span data-stu-id="d6727-119">See the Member Names section later in this topic.</span></span>|`String`|

## <a name="example"></a><span data-ttu-id="d6727-120">Przykład</span><span class="sxs-lookup"><span data-stu-id="d6727-120">Example</span></span>

<span data-ttu-id="d6727-121">Poniższy przykład pokazuje, jak można użyć tych atrybutów do śledzenia obiektu wywołującego.</span><span class="sxs-lookup"><span data-stu-id="d6727-121">The following example shows how you might use these attributes to trace a caller.</span></span>

```fsharp
open System.Diagnostics
open System.Runtime.CompilerServices
open System.Runtime.InteropServices

type Tracer() =
    member _.DoTrace(message: string,
                      [<CallerMemberName; Optional; DefaultParameterValue("")>] memberName: string,
                      [<CallerFilePath; Optional; DefaultParameterValue("")>] path: string,
                      [<CallerLineNumber; Optional; DefaultParameterValue(0)>] line: int) =
        Trace.WriteLine(sprintf "Message: %s" message)
        Trace.WriteLine(sprintf "Member name: %s" memberName)
        Trace.WriteLine(sprintf "Source file path: %s" path)
        Trace.WriteLine(sprintf "Source line number: %d" line)
```

## <a name="remarks"></a><span data-ttu-id="d6727-122">Uwagi</span><span class="sxs-lookup"><span data-stu-id="d6727-122">Remarks</span></span>

<span data-ttu-id="d6727-123">Atrybuty informacji o wywołującym mogą być stosowane tylko do parametrów opcjonalnych.</span><span class="sxs-lookup"><span data-stu-id="d6727-123">Caller Info attributes can only be applied to optional parameters.</span></span> <span data-ttu-id="d6727-124">Atrybuty informacji o wywołującym powodują, że kompilator zapisuje odpowiednią wartość dla każdego opcjonalnego parametru uzupełnionego atrybutem informacje o wywołującym.</span><span class="sxs-lookup"><span data-stu-id="d6727-124">The Caller Info attributes cause the compiler to write the proper value for each optional parameter decorated with a Caller Info attribute.</span></span>

<span data-ttu-id="d6727-125">Wartości informacji o obiekcie wywołującym są emitowane jako literały do języka pośredniego (IL, Intermediate Language) w czasie kompilacji.</span><span class="sxs-lookup"><span data-stu-id="d6727-125">Caller Info values are emitted as literals into the Intermediate Language (IL) at compile time.</span></span> <span data-ttu-id="d6727-126">W przeciwieństwie do wyników właściwości [ślad stosu](/dotnet/api/system.diagnostics.stacktrace) dla wyjątków, nie ma to wpływu na wyniki.</span><span class="sxs-lookup"><span data-stu-id="d6727-126">Unlike the results of the [StackTrace](/dotnet/api/system.diagnostics.stacktrace) property for exceptions, the results aren't affected by obfuscation.</span></span>

<span data-ttu-id="d6727-127">Można jawnie dostarczyć opcjonalne argumenty do sterowania informacjami o obiekcie wywołującym lub ukryć te informacje.</span><span class="sxs-lookup"><span data-stu-id="d6727-127">You can explicitly supply the optional arguments to control the caller information or to hide caller information.</span></span>

## <a name="member-names"></a><span data-ttu-id="d6727-128">Nazwy elementów członkowskich</span><span class="sxs-lookup"><span data-stu-id="d6727-128">Member names</span></span>

<span data-ttu-id="d6727-129">Można użyć atrybutu [`CallerMemberName`](/dotnet/api/system.runtime.compilerservices.callermembernameattribute) , aby uniknąć określania nazwy elementu członkowskiego jako argumentu `String` dla wywoływanej metody.</span><span class="sxs-lookup"><span data-stu-id="d6727-129">You can use the [`CallerMemberName`](/dotnet/api/system.runtime.compilerservices.callermembernameattribute) attribute to avoid specifying the member name as a `String` argument to the called method.</span></span> <span data-ttu-id="d6727-130">Korzystając z tej techniki, można uniknąć problemu, którego Refaktoryzacja zmiany nazwy nie zmienia wartości `String`.</span><span class="sxs-lookup"><span data-stu-id="d6727-130">By using this technique, you avoid the problem that Rename Refactoring doesn't change the `String` values.</span></span> <span data-ttu-id="d6727-131">Jest to szczególnie przydatne w następujących zadaniach:</span><span class="sxs-lookup"><span data-stu-id="d6727-131">This benefit is especially useful for the following tasks:</span></span>

- <span data-ttu-id="d6727-132">Używanie procedur do śledzenia i diagnostycznych.</span><span class="sxs-lookup"><span data-stu-id="d6727-132">Using tracing and diagnostic routines.</span></span>
- <span data-ttu-id="d6727-133">Implementowanie interfejsu [INotifyPropertyChanged](/dotnet/api/system.componentmodel.inotifypropertychanged) podczas wiązania danych.</span><span class="sxs-lookup"><span data-stu-id="d6727-133">Implementing the [INotifyPropertyChanged](/dotnet/api/system.componentmodel.inotifypropertychanged) interface when binding data.</span></span> <span data-ttu-id="d6727-134">Ten interfejs umożliwia właściwości obiektu powiadamianie powiązanego formantu, że właściwość zmieniła się, dzięki czemu formant może wyświetlić zaktualizowane informacje.</span><span class="sxs-lookup"><span data-stu-id="d6727-134">This interface allows the property of an object to notify a bound control that the property has changed, so that the control can display the updated information.</span></span> <span data-ttu-id="d6727-135">Bez atrybutu [`CallerMemberName`](/dotnet/api/system.runtime.compilerservices.callermembernameattribute) należy określić nazwę właściwości jako literału.</span><span class="sxs-lookup"><span data-stu-id="d6727-135">Without the [`CallerMemberName`](/dotnet/api/system.runtime.compilerservices.callermembernameattribute) attribute, you must specify the property name as a literal.</span></span>

<span data-ttu-id="d6727-136">Poniższy wykres pokazuje nazwy elementów członkowskich, które są zwracane w przypadku używania atrybutu CallerMemberName.</span><span class="sxs-lookup"><span data-stu-id="d6727-136">The following chart shows the member names that are returned when you use the CallerMemberName attribute.</span></span>

|<span data-ttu-id="d6727-137">Wywołanie ma miejsce w</span><span class="sxs-lookup"><span data-stu-id="d6727-137">Calls occurs within</span></span>|<span data-ttu-id="d6727-138">Wynikowa nazwa elementu członkowskiego</span><span class="sxs-lookup"><span data-stu-id="d6727-138">Member name result</span></span>|
|-------------------|------------------|
|<span data-ttu-id="d6727-139">Metoda, właściwość lub zdarzenie</span><span class="sxs-lookup"><span data-stu-id="d6727-139">Method, property, or event</span></span>|<span data-ttu-id="d6727-140">Nazwa metody, właściwości lub zdarzenia, gdzie zainicjowane było wywołanie.</span><span class="sxs-lookup"><span data-stu-id="d6727-140">The name of the method, property, or event from which the call originated.</span></span>|
|<span data-ttu-id="d6727-141">Konstruktor</span><span class="sxs-lookup"><span data-stu-id="d6727-141">Constructor</span></span>|<span data-ttu-id="d6727-142">Ciąg „.ctor”</span><span class="sxs-lookup"><span data-stu-id="d6727-142">The string ".ctor"</span></span>|
|<span data-ttu-id="d6727-143">Statyczny konstruktor</span><span class="sxs-lookup"><span data-stu-id="d6727-143">Static constructor</span></span>|<span data-ttu-id="d6727-144">Ciąg „.cctor”</span><span class="sxs-lookup"><span data-stu-id="d6727-144">The string ".cctor"</span></span>|
|<span data-ttu-id="d6727-145">Destruktor</span><span class="sxs-lookup"><span data-stu-id="d6727-145">Destructor</span></span>|<span data-ttu-id="d6727-146">Ciąg „Finalize”.</span><span class="sxs-lookup"><span data-stu-id="d6727-146">The string "Finalize"</span></span>|
|<span data-ttu-id="d6727-147">Zdefiniowane przez użytkownika operatory lub konwersje</span><span class="sxs-lookup"><span data-stu-id="d6727-147">User-defined operators or conversions</span></span>|<span data-ttu-id="d6727-148">Nazwa wygenerowana dla elementu członkowskiego, na przykład „op_Addition”.</span><span class="sxs-lookup"><span data-stu-id="d6727-148">The generated name for the member, for example, "op_Addition".</span></span>|
|<span data-ttu-id="d6727-149">Konstruktor atrybutu</span><span class="sxs-lookup"><span data-stu-id="d6727-149">Attribute constructor</span></span>|<span data-ttu-id="d6727-150">Nazwa elementu członkowskiego, do którego został zastosowany atrybut.</span><span class="sxs-lookup"><span data-stu-id="d6727-150">The name of the member to which the attribute is applied.</span></span> <span data-ttu-id="d6727-151">Jeśli atrybut jest dowolnym elementem elementu członkowskiego (takim jak parametr, wartość zwracana lub parametr typu ogólnego), to wynikiem jest nazwa elementu członkowskiego, który jest skojarzony z tym elementem.</span><span class="sxs-lookup"><span data-stu-id="d6727-151">If the attribute is any element within a member (such as a parameter, a return value, or a generic type parameter), this result is the name of the member that's associated with that element.</span></span>|
|<span data-ttu-id="d6727-152">Brak nadrzędnego elementu członkowskiego (na przykład poziom zestawu lub atrybuty, które są stosowane do typów)</span><span class="sxs-lookup"><span data-stu-id="d6727-152">No containing member (for example, assembly-level or attributes that are applied to types)</span></span>|<span data-ttu-id="d6727-153">Wartość domyślna opcjonalnego parametru.</span><span class="sxs-lookup"><span data-stu-id="d6727-153">The default value of the optional parameter.</span></span>|

## <a name="see-also"></a><span data-ttu-id="d6727-154">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="d6727-154">See also</span></span>

- [<span data-ttu-id="d6727-155">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="d6727-155">Attributes</span></span>](attributes.md)
- [<span data-ttu-id="d6727-156">Nazwane argumenty</span><span class="sxs-lookup"><span data-stu-id="d6727-156">Named arguments</span></span>](parameters-and-arguments.md#named-arguments)
- [<span data-ttu-id="d6727-157">Parametry opcjonalne</span><span class="sxs-lookup"><span data-stu-id="d6727-157">Optional parameters</span></span>](parameters-and-arguments.md#optional-parameters)
