---
title: Organizowanie domyślne dotyczące tablic
description: Zrozumienie domyślnego kierowania dla tablic. Zapoznaj się z tablicami zarządzanymi, niezarządzanymi tablicami, przekazywaniem parametrów tablicy do kodu .NET i przekazywaniem tablic do modelu COM.
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- interop marshaling, arrays
- arrays, interop marshaling
ms.assetid: 8a3cca8b-dd94-4e3d-ad9a-9ee7590654bc
ms.openlocfilehash: 6bfe95576a6460efac75fd392e24acf42e36f2de
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "90555266"
---
# <a name="default-marshaling-for-arrays"></a><span data-ttu-id="6f668-104">Organizowanie domyślne dotyczące tablic</span><span class="sxs-lookup"><span data-stu-id="6f668-104">Default Marshaling for Arrays</span></span>
<span data-ttu-id="6f668-105">W aplikacji składającej się wyłącznie z kodu zarządzanego środowisko uruchomieniowe języka wspólnego przekazuje typy tablicy jako parametry wejściowe/out.</span><span class="sxs-lookup"><span data-stu-id="6f668-105">In an application consisting entirely of managed code, the common language runtime passes array types as In/Out parameters.</span></span> <span data-ttu-id="6f668-106">W przeciwieństwie do organizatora międzyoperacyjności domyślnie przekazuje tablicę w postaci parametrów.</span><span class="sxs-lookup"><span data-stu-id="6f668-106">In contrast, the interop marshaler passes an array as In parameters by default.</span></span>  
  
 <span data-ttu-id="6f668-107">Dzięki [przypinaniu optymalizacji](copying-and-pinning.md)Tablica danych kopiowalnych może być wyświetlana jako parametr in/out podczas korzystania z obiektów w tym samym elemencie Apartment.</span><span class="sxs-lookup"><span data-stu-id="6f668-107">With [pinning optimization](copying-and-pinning.md), a blittable array can appear to operate as an In/Out parameter when interacting with objects in the same apartment.</span></span> <span data-ttu-id="6f668-108">Jednak w przypadku późniejszego wyeksportowania kodu do biblioteki typów użytej do wygenerowania serwera proxy międzymaszynowego, a ta biblioteka jest używana do organizowania wywołań w ramach apartamentach, wywołania mogą przywrócić wartość true w zachowaniu parametrów.</span><span class="sxs-lookup"><span data-stu-id="6f668-108">However, if you later export the code to a type library used to generate the cross-machine proxy, and that library is used to marshal your calls across apartments, the calls can revert to true In parameter behavior.</span></span>  
  
 <span data-ttu-id="6f668-109">Tablice są złożone z natury, a różnice między zarządzanymi i niezarządzanymi tablicami gwarantują więcej informacji niż w przypadku innych typów innych niż danych kopiowalnych.</span><span class="sxs-lookup"><span data-stu-id="6f668-109">Arrays are complex by nature, and the distinctions between managed and unmanaged arrays warrant more information than other non-blittable types.</span></span>  
  
## <a name="managed-arrays"></a><span data-ttu-id="6f668-110">Zarządzane tablice</span><span class="sxs-lookup"><span data-stu-id="6f668-110">Managed Arrays</span></span>  
 <span data-ttu-id="6f668-111">Zarządzane typy tablic mogą się różnić; jednak <xref:System.Array?displayProperty=nameWithType> Klasa jest klasą bazową wszystkich typów tablicowych.</span><span class="sxs-lookup"><span data-stu-id="6f668-111">Managed array types can vary; however, the <xref:System.Array?displayProperty=nameWithType> class is the base class of all array types.</span></span> <span data-ttu-id="6f668-112">Klasa **System. Array** ma właściwości do określania rangi, długości i dolnych i górnych granic tablicy, a także metod uzyskiwania dostępu do, sortowania, wyszukiwania, kopiowania i tworzenia tablic.</span><span class="sxs-lookup"><span data-stu-id="6f668-112">The **System.Array** class has properties for determining the rank, length, and lower and upper bounds of an array, as well as methods for accessing, sorting, searching, copying, and creating arrays.</span></span>  
  
 <span data-ttu-id="6f668-113">Te typy tablic są dynamiczne i nie mają odpowiedniego typu statycznego zdefiniowanego w bibliotece klas bazowych.</span><span class="sxs-lookup"><span data-stu-id="6f668-113">These array types are dynamic and do not have a corresponding static type defined in the base class library.</span></span> <span data-ttu-id="6f668-114">Wygodnie jest myśleć o każdej kombinacji typu elementu i rangi jako odrębny typ tablicy.</span><span class="sxs-lookup"><span data-stu-id="6f668-114">It is convenient to think of each combination of element type and rank as a distinct type of array.</span></span> <span data-ttu-id="6f668-115">W związku z tym, Jednowymiarowa tablica liczb całkowitych jest innego typu niż Jednowymiarowa tablica podwójnych typów.</span><span class="sxs-lookup"><span data-stu-id="6f668-115">Therefore, a one-dimensional array of integers is of a different type than a one-dimensional array of double types.</span></span> <span data-ttu-id="6f668-116">Podobnie Dwuwymiarowa tablica liczb całkowitych różni się od jednowymiarowej tablicy liczb całkowitych.</span><span class="sxs-lookup"><span data-stu-id="6f668-116">Similarly a two-dimensional array of integers is different from a one-dimensional array of integers.</span></span> <span data-ttu-id="6f668-117">Granice tablicy nie są brane pod uwagę podczas porównywania typów.</span><span class="sxs-lookup"><span data-stu-id="6f668-117">The bounds of the array are not considered when comparing types.</span></span>  
  
 <span data-ttu-id="6f668-118">Jak przedstawiono w poniższej tabeli, każde wystąpienie tablicy zarządzanej musi mieć określony typ elementu, rangę i dolną granicę.</span><span class="sxs-lookup"><span data-stu-id="6f668-118">As the following table shows, any instance of a managed array must be of a specific element type, rank, and lower bound.</span></span>  
  
|<span data-ttu-id="6f668-119">Typ tablicy zarządzanej</span><span class="sxs-lookup"><span data-stu-id="6f668-119">Managed array type</span></span>|<span data-ttu-id="6f668-120">Typ elementu</span><span class="sxs-lookup"><span data-stu-id="6f668-120">Element type</span></span>|<span data-ttu-id="6f668-121">Ranga</span><span class="sxs-lookup"><span data-stu-id="6f668-121">Rank</span></span>|<span data-ttu-id="6f668-122">Dolna granica</span><span class="sxs-lookup"><span data-stu-id="6f668-122">Lower bound</span></span>|<span data-ttu-id="6f668-123">Notacja podpisu</span><span class="sxs-lookup"><span data-stu-id="6f668-123">Signature notation</span></span>|  
|------------------------|------------------|----------|-----------------|------------------------|  
|<span data-ttu-id="6f668-124">**ELEMENT_TYPE_ARRAY**</span><span class="sxs-lookup"><span data-stu-id="6f668-124">**ELEMENT_TYPE_ARRAY**</span></span>|<span data-ttu-id="6f668-125">Określony przez typ.</span><span class="sxs-lookup"><span data-stu-id="6f668-125">Specified by type.</span></span>|<span data-ttu-id="6f668-126">Określone przez rangę.</span><span class="sxs-lookup"><span data-stu-id="6f668-126">Specified by rank.</span></span>|<span data-ttu-id="6f668-127">Opcjonalnie określone przez granice.</span><span class="sxs-lookup"><span data-stu-id="6f668-127">Optionally specified by bounds.</span></span>|<span data-ttu-id="6f668-128">*Typ* **[** *n*,*m* **]**</span><span class="sxs-lookup"><span data-stu-id="6f668-128">*type* **[** *n*,*m* **]**</span></span>|  
|<span data-ttu-id="6f668-129">**ELEMENT_TYPE_CLASS**</span><span class="sxs-lookup"><span data-stu-id="6f668-129">**ELEMENT_TYPE_CLASS**</span></span>|<span data-ttu-id="6f668-130">Nieznane</span><span class="sxs-lookup"><span data-stu-id="6f668-130">Unknown</span></span>|<span data-ttu-id="6f668-131">Nieznane</span><span class="sxs-lookup"><span data-stu-id="6f668-131">Unknown</span></span>|<span data-ttu-id="6f668-132">Nieznane</span><span class="sxs-lookup"><span data-stu-id="6f668-132">Unknown</span></span>|<span data-ttu-id="6f668-133">**System. Array**</span><span class="sxs-lookup"><span data-stu-id="6f668-133">**System.Array**</span></span>|  
|<span data-ttu-id="6f668-134">**ELEMENT_TYPE_SZARRAY**</span><span class="sxs-lookup"><span data-stu-id="6f668-134">**ELEMENT_TYPE_SZARRAY**</span></span>|<span data-ttu-id="6f668-135">Określony przez typ.</span><span class="sxs-lookup"><span data-stu-id="6f668-135">Specified by type.</span></span>|<span data-ttu-id="6f668-136">1</span><span class="sxs-lookup"><span data-stu-id="6f668-136">1</span></span>|<span data-ttu-id="6f668-137">0</span><span class="sxs-lookup"><span data-stu-id="6f668-137">0</span></span>|<span data-ttu-id="6f668-138">*Typ* **[** *n* **]**</span><span class="sxs-lookup"><span data-stu-id="6f668-138">*type* **[** *n* **]**</span></span>|  
  
## <a name="unmanaged-arrays"></a><span data-ttu-id="6f668-139">Tablice niezarządzane</span><span class="sxs-lookup"><span data-stu-id="6f668-139">Unmanaged Arrays</span></span>  
 <span data-ttu-id="6f668-140">Tablice niezarządzane są tablicami bezpiecznymi w stylu COM lub tablicami w stylu C ze stałą lub zmienną długością.</span><span class="sxs-lookup"><span data-stu-id="6f668-140">Unmanaged arrays are either COM-style safe arrays or C-style arrays with fixed or variable length.</span></span> <span data-ttu-id="6f668-141">Bezpieczne tablice to samoopisujące się tablice, które zawierają typ, rangę i granice skojarzonych danych tablicy.</span><span class="sxs-lookup"><span data-stu-id="6f668-141">Safe arrays are self-describing arrays that carry the type, rank, and bounds of the associated array data.</span></span> <span data-ttu-id="6f668-142">Tablice w stylu C to jednowymiarowe tablice z ustaloną dolną granicą 0.</span><span class="sxs-lookup"><span data-stu-id="6f668-142">C-style arrays are one-dimensional typed arrays with a fixed lower bound of 0.</span></span> <span data-ttu-id="6f668-143">Usługa Marshaling ma ograniczoną obsługę obu typów tablic.</span><span class="sxs-lookup"><span data-stu-id="6f668-143">The marshaling service has limited support for both types of arrays.</span></span>  
  
## <a name="passing-array-parameters-to-net-code"></a><span data-ttu-id="6f668-144">Przekazywanie parametrów tablicy do kodu platformy .NET</span><span class="sxs-lookup"><span data-stu-id="6f668-144">Passing Array Parameters to .NET Code</span></span>  
 <span data-ttu-id="6f668-145">Zarówno tablice w stylu C, jak i bezpieczne tablice można przesłać do kodu platformy .NET z niezarządzanego kodu jako tablicę bezpieczną lub tablicę w stylu języka C.</span><span class="sxs-lookup"><span data-stu-id="6f668-145">Both C-style arrays and safe arrays can be passed to .NET code from unmanaged code as either a safe array or a C-style array.</span></span> <span data-ttu-id="6f668-146">W poniższej tabeli przedstawiono wartość typu niezarządzanego i typ zaimportowany.</span><span class="sxs-lookup"><span data-stu-id="6f668-146">The following table shows the unmanaged type value and the imported type.</span></span>  
  
|<span data-ttu-id="6f668-147">Typ niezarządzany</span><span class="sxs-lookup"><span data-stu-id="6f668-147">Unmanaged type</span></span>|<span data-ttu-id="6f668-148">Typ zaimportowany</span><span class="sxs-lookup"><span data-stu-id="6f668-148">Imported type</span></span>|  
|--------------------|-------------------|  
|<span data-ttu-id="6f668-149">**SAFEARRAY (** *Typ* **)**</span><span class="sxs-lookup"><span data-stu-id="6f668-149">**SafeArray(** *Type* **)**</span></span>|<span data-ttu-id="6f668-150">**ELEMENT_TYPE_SZARRAY\*\*\*\*\<** *ConvertedType* **>**</span><span class="sxs-lookup"><span data-stu-id="6f668-150">**ELEMENT_TYPE_SZARRAY** **\<** *ConvertedType* **>**</span></span><br /><br /> <span data-ttu-id="6f668-151">Ranga = 1, Dolna granica = 0.</span><span class="sxs-lookup"><span data-stu-id="6f668-151">Rank = 1, lower bound = 0.</span></span> <span data-ttu-id="6f668-152">Rozmiar jest znany tylko wtedy, gdy jest podany w podpisie zarządzanym.</span><span class="sxs-lookup"><span data-stu-id="6f668-152">Size is known only if provided in the managed signature.</span></span> <span data-ttu-id="6f668-153">Tablic bezpiecznych, które nie mają rangi = 1 lub dolnego powiązania = 0, nie mogą być organizowane jako **SZARRAY**.</span><span class="sxs-lookup"><span data-stu-id="6f668-153">Safe arrays that are not rank = 1 or lower bound = 0 cannot be marshaled as **SZARRAY**.</span></span>|  
|<span data-ttu-id="6f668-154">*Typ*  **[]**</span><span class="sxs-lookup"><span data-stu-id="6f668-154">*Type*  **[]**</span></span>|<span data-ttu-id="6f668-155">**ELEMENT_TYPE_SZARRAY\*\*\*\*\<** *ConvertedType* **>**</span><span class="sxs-lookup"><span data-stu-id="6f668-155">**ELEMENT_TYPE_SZARRAY** **\<** *ConvertedType* **>**</span></span><br /><br /> <span data-ttu-id="6f668-156">Ranga = 1, Dolna granica = 0.</span><span class="sxs-lookup"><span data-stu-id="6f668-156">Rank = 1, lower bound = 0.</span></span> <span data-ttu-id="6f668-157">Rozmiar jest znany tylko wtedy, gdy jest podany w podpisie zarządzanym.</span><span class="sxs-lookup"><span data-stu-id="6f668-157">Size is known only if provided in the managed signature.</span></span>|  
  
### <a name="safe-arrays"></a><span data-ttu-id="6f668-158">Bezpieczne tablice</span><span class="sxs-lookup"><span data-stu-id="6f668-158">Safe Arrays</span></span>  
 <span data-ttu-id="6f668-159">Gdy bezpieczna tablica jest importowana z biblioteki typów do zestawu .NET, tablica jest konwertowana na tablicę jednowymiarową znanego typu (na przykład **int**).</span><span class="sxs-lookup"><span data-stu-id="6f668-159">When a safe array is imported from a type library to a .NET assembly, the array is converted to a one-dimensional array of a known type (such as **int**).</span></span> <span data-ttu-id="6f668-160">Te same reguły konwersji typów, które mają zastosowanie do parametrów, mają zastosowanie także do elementów tablicy.</span><span class="sxs-lookup"><span data-stu-id="6f668-160">The same type conversion rules that apply to parameters also apply to array elements.</span></span> <span data-ttu-id="6f668-161">Na przykład bezpieczna tablica typów **BSTR** jest zarządzaną tablicą ciągów, a bezpieczna tablica wariantów jest zarządzaną tablicą obiektów.</span><span class="sxs-lookup"><span data-stu-id="6f668-161">For example, a safe array of **BSTR** types becomes a managed array of strings and a safe array of variants becomes a managed array of objects.</span></span> <span data-ttu-id="6f668-162">Typ elementu **SAFEARRAY** jest przechwytywany z biblioteki typów i zapisywany w wartości **SAFEARRAY** <xref:System.Runtime.InteropServices.UnmanagedType> wyliczenia.</span><span class="sxs-lookup"><span data-stu-id="6f668-162">The **SAFEARRAY** element type is captured from the type library and saved in the **SAFEARRAY** value of the <xref:System.Runtime.InteropServices.UnmanagedType> enumeration.</span></span>  
  
 <span data-ttu-id="6f668-163">Ponieważ ranga i granice tablicy bezpiecznej nie można ustalić na podstawie biblioteki typów, przyjmuje się, że ranga jest równa 1, a dolna granica jest przyjmowana jako równa 0.</span><span class="sxs-lookup"><span data-stu-id="6f668-163">Because the rank and bounds of the safe array cannot be determined from the type library, the rank is assumed to equal 1 and the lower bound is assumed to equal 0.</span></span> <span data-ttu-id="6f668-164">Ranga i granice muszą być zdefiniowane w zarządzanym podpisie wygenerowanym przez [importera biblioteki typów (Tlbimp.exe)](../tools/tlbimp-exe-type-library-importer.md).</span><span class="sxs-lookup"><span data-stu-id="6f668-164">The rank and bounds must be defined in the managed signature produced by the [Type Library Importer (Tlbimp.exe)](../tools/tlbimp-exe-type-library-importer.md).</span></span> <span data-ttu-id="6f668-165">Jeśli ranga przeniesiona do metody w czasie wykonywania różni się od, <xref:System.Runtime.InteropServices.SafeArrayRankMismatchException> jest generowany.</span><span class="sxs-lookup"><span data-stu-id="6f668-165">If the rank passed to the method at run time differs, a <xref:System.Runtime.InteropServices.SafeArrayRankMismatchException> is thrown.</span></span> <span data-ttu-id="6f668-166">Jeśli typ tablicy przeszedł w czasie wykonywania różni się, <xref:System.Runtime.InteropServices.SafeArrayTypeMismatchException> zostanie zgłoszony.</span><span class="sxs-lookup"><span data-stu-id="6f668-166">If the type of the array passed at run time differs, a <xref:System.Runtime.InteropServices.SafeArrayTypeMismatchException> is thrown.</span></span> <span data-ttu-id="6f668-167">W poniższym przykładzie przedstawiono bezpieczne tablice w kodzie zarządzanym i niezarządzanym.</span><span class="sxs-lookup"><span data-stu-id="6f668-167">The following example shows safe arrays in managed and unmanaged code.</span></span>  
  
 <span data-ttu-id="6f668-168">**Niezarządzany podpis**</span><span class="sxs-lookup"><span data-stu-id="6f668-168">**Unmanaged signature**</span></span>  
  
```cpp
HRESULT New1([in] SAFEARRAY( int ) ar);  
HRESULT New2([in] SAFEARRAY( DATE ) ar);  
HRESULT New3([in, out] SAFEARRAY( BSTR ) *ar);  
```  
  
 <span data-ttu-id="6f668-169">**Sygnatura zarządzana**</span><span class="sxs-lookup"><span data-stu-id="6f668-169">**Managed signature**</span></span>  
  
```vb  
Sub New1(<MarshalAs(UnmanagedType.SafeArray, SafeArraySubType:=VT_I4)> _  
   ar() As Integer)  
Sub New2(<MarshalAs(UnmanagedType.SafeArray, SafeArraySubType:=VT_DATE)> _
   ar() As DateTime)  
Sub New3(ByRef <MarshalAs(UnmanagedType.SafeArray, SafeArraySubType:=VT_BSTR)> _
   ar() As String)  
```  
  
```csharp  
void New1([MarshalAs(UnmanagedType.SafeArray, SafeArraySubType=VT_I4)] int[] ar) ;  
void New2([MarshalAs(UnmanagedType.SafeArray, SafeArraySubType=VT_DATE)]
   DateTime[] ar);  
void New3([MarshalAs(UnmanagedType.SafeArray, SafeArraySubType=VT_BSTR)]
   ref String[] ar);  
```  
  
 <span data-ttu-id="6f668-170">Wielowymiarowe lub niezerowe powiązane tablice mogą być organizowane w kodzie zarządzanym, jeśli sygnatura metody utworzona przez Tlbimp.exe jest modyfikowana w celu wskazania typu elementu **ELEMENT_TYPE_ARRAY** zamiast **ELEMENT_TYPE_SZARRAY**.</span><span class="sxs-lookup"><span data-stu-id="6f668-170">Multidimensional, or nonzero-bound safe arrays, can be marshaled into managed code if the method signature produced by Tlbimp.exe is modified to indicate an element type of **ELEMENT_TYPE_ARRAY** instead of **ELEMENT_TYPE_SZARRAY**.</span></span> <span data-ttu-id="6f668-171">Alternatywnie można użyć przełącznika **/sysarray** z Tlbimp.exe, aby zaimportować wszystkie tablice jako <xref:System.Array?displayProperty=nameWithType> obiekty.</span><span class="sxs-lookup"><span data-stu-id="6f668-171">Alternatively, you can use the **/sysarray** switch with Tlbimp.exe to import all arrays as <xref:System.Array?displayProperty=nameWithType> objects.</span></span> <span data-ttu-id="6f668-172">W przypadku, gdy przenoszona tablica jest nazywana wielowymiarową, można edytować kod języka pośredniego firmy Microsoft (MSIL) utworzony przez Tlbimp.exe i ponownie go skompilować.</span><span class="sxs-lookup"><span data-stu-id="6f668-172">In cases where the array being passed is known to be multidimensional, you can edit the Microsoft intermediate language (MSIL) code produced by Tlbimp.exe and then recompile it.</span></span> <span data-ttu-id="6f668-173">Aby uzyskać szczegółowe informacje na temat modyfikowania kodu MSIL, zobacz Dostosowywanie wywoływanych [otok środowiska uruchomieniowego](/previous-versions/dotnet/netframework-4.0/e753eftz(v=vs.100)).</span><span class="sxs-lookup"><span data-stu-id="6f668-173">For details about how to modify MSIL code, see [Customizing Runtime Callable Wrappers](/previous-versions/dotnet/netframework-4.0/e753eftz(v=vs.100)).</span></span>  
  
### <a name="c-style-arrays"></a><span data-ttu-id="6f668-174">Tablice w stylu języka C</span><span class="sxs-lookup"><span data-stu-id="6f668-174">C-Style Arrays</span></span>  
 <span data-ttu-id="6f668-175">Gdy tablica w stylu C jest importowana z biblioteki typów do zestawu .NET, tablica jest konwertowana na **ELEMENT_TYPE_SZARRAY**.</span><span class="sxs-lookup"><span data-stu-id="6f668-175">When a C-style array is imported from a type library to a .NET assembly, the array is converted to **ELEMENT_TYPE_SZARRAY**.</span></span>  
  
 <span data-ttu-id="6f668-176">Typ elementu tablicy jest określany na podstawie biblioteki typów i zachowywany podczas importowania.</span><span class="sxs-lookup"><span data-stu-id="6f668-176">The array element type is determined from the type library and preserved during the import.</span></span> <span data-ttu-id="6f668-177">Te same reguły konwersji, które mają zastosowanie do parametrów, mają zastosowanie także do elementów tablicy.</span><span class="sxs-lookup"><span data-stu-id="6f668-177">The same conversion rules that apply to parameters also apply to array elements.</span></span> <span data-ttu-id="6f668-178">Na przykład Tablica typów **LPSTR** jest tablicą typów **ciągów** .</span><span class="sxs-lookup"><span data-stu-id="6f668-178">For example, an array of **LPStr** types becomes an array of **String** types.</span></span> <span data-ttu-id="6f668-179">Tlbimp.exe przechwytuje typ elementu tablicy i stosuje <xref:System.Runtime.InteropServices.MarshalAsAttribute> atrybut do parametru.</span><span class="sxs-lookup"><span data-stu-id="6f668-179">Tlbimp.exe captures the array element type and applies the <xref:System.Runtime.InteropServices.MarshalAsAttribute> attribute to the parameter.</span></span>  
  
 <span data-ttu-id="6f668-180">Przyjmuje się, że ranga tablicy jest równa 1.</span><span class="sxs-lookup"><span data-stu-id="6f668-180">The array rank is assumed to equal 1.</span></span> <span data-ttu-id="6f668-181">Jeśli ranga jest większa niż 1, tablica jest organizowana jako tablica Jednowymiarowa w kolejności kolumny — główna.</span><span class="sxs-lookup"><span data-stu-id="6f668-181">If the rank is greater than 1, the array is marshaled as a one-dimensional array in column-major order.</span></span> <span data-ttu-id="6f668-182">Dolna granica zawsze jest równa 0.</span><span class="sxs-lookup"><span data-stu-id="6f668-182">The lower bound always equals 0.</span></span>  
  
 <span data-ttu-id="6f668-183">Biblioteki typów mogą zawierać tablice o stałej lub zmiennej długości.</span><span class="sxs-lookup"><span data-stu-id="6f668-183">Type libraries can contain arrays of fixed or variable length.</span></span> <span data-ttu-id="6f668-184">Tlbimp.exe może importować tylko tablice o stałej długości z bibliotek typów, ponieważ biblioteki typów nie zawierają informacji wymaganych do organizowania tablic o zmiennej długości.</span><span class="sxs-lookup"><span data-stu-id="6f668-184">Tlbimp.exe can import only fixed-length arrays from type libraries because type libraries lack the information needed to marshal variable-length arrays.</span></span> <span data-ttu-id="6f668-185">W przypadku tablic o stałej długości rozmiar jest zaimportowany z biblioteki typów i przechwytywany w elemencie **MarshalAsAttribute** , który jest stosowany do parametru.</span><span class="sxs-lookup"><span data-stu-id="6f668-185">With fixed-length arrays, the size is imported from the type library and captured in the **MarshalAsAttribute** that is applied to the parameter.</span></span>  
  
 <span data-ttu-id="6f668-186">Należy ręcznie zdefiniować biblioteki typów zawierające tablice o zmiennej długości, jak pokazano w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="6f668-186">You must manually define type libraries containing variable-length arrays, as shown in the following example.</span></span>  
  
 <span data-ttu-id="6f668-187">**Niezarządzany podpis**</span><span class="sxs-lookup"><span data-stu-id="6f668-187">**Unmanaged signature**</span></span>  
  
```cpp
HRESULT New1(int ar[10]);  
HRESULT New2(double ar[10][20]);  
HRESULT New3(LPWStr ar[10]);  
```  
  
 <span data-ttu-id="6f668-188">**Sygnatura zarządzana**</span><span class="sxs-lookup"><span data-stu-id="6f668-188">**Managed signature**</span></span>  
  
```vb  
Sub New1(<MarshalAs(UnmanagedType.LPArray, SizeConst=10)> _  
   ar() As Integer)  
Sub New2(<MarshalAs(UnmanagedType.LPArray, SizeConst=200)> _  
   ar() As Double)  
Sub New2(<MarshalAs(UnmanagedType.LPArray, _  
   ArraySubType=UnmanagedType.LPWStr, SizeConst=10)> _  
   ar() As String)  
```  
  
```csharp  
void New1([MarshalAs(UnmanagedType.LPArray, SizeConst=10)] int[] ar);  
void New2([MarshalAs(UnmanagedType.LPArray, SizeConst=200)] double[] ar);  
void New2([MarshalAs(UnmanagedType.LPArray,
   ArraySubType=UnmanagedType.LPWStr, SizeConst=10)] String[] ar);  
```  
  
 <span data-ttu-id="6f668-189">Chociaż atrybuty **size_is** lub **length_is** można zastosować do tablicy źródła w języku definicji interfejsu (IDL), aby przekazać rozmiar do klienta, kompilator Microsoft Interface Definition Language (MIDL) nie propaguje tych informacji do biblioteki typów.</span><span class="sxs-lookup"><span data-stu-id="6f668-189">Although you can apply the **size_is** or **length_is** attributes to an array in Interface Definition Language (IDL) source to convey the size to a client, the Microsoft Interface Definition Language (MIDL) compiler does not propagate that information to the type library.</span></span> <span data-ttu-id="6f668-190">Bez znajomości rozmiaru usługa Marshaling Interop nie może zorganizować elementów tablicy.</span><span class="sxs-lookup"><span data-stu-id="6f668-190">Without knowing the size, the interop marshaling service cannot marshal the array elements.</span></span> <span data-ttu-id="6f668-191">W związku z tym tablice o zmiennej długości są importowane jako argumenty odwołania.</span><span class="sxs-lookup"><span data-stu-id="6f668-191">Consequently, variable-length arrays are imported as reference arguments.</span></span> <span data-ttu-id="6f668-192">Przykład:</span><span class="sxs-lookup"><span data-stu-id="6f668-192">For example:</span></span>  
  
 <span data-ttu-id="6f668-193">**Niezarządzany podpis**</span><span class="sxs-lookup"><span data-stu-id="6f668-193">**Unmanaged signature**</span></span>  
  
```cpp
HRESULT New1(int ar[]);  
HRESULT New2(int ArSize, [size_is(ArSize)] double ar[]);  
HRESULT New3(int ElemCnt, [length_is(ElemCnt)] LPStr ar[]);  
```  
  
 <span data-ttu-id="6f668-194">**Sygnatura zarządzana**</span><span class="sxs-lookup"><span data-stu-id="6f668-194">**Managed signature**</span></span>  
  
```vb  
Sub New1(ByRef ar As Integer)  
Sub New2(ByRef ar As Double)  
Sub New3(ByRef ar As String)  
```  
  
```csharp  
void New1(ref int ar);
void New2(ref double ar);
void New3(ref String ar);
```  
  
 <span data-ttu-id="6f668-195">Można przekazać Organizatorowi rozmiar tablicy, edytując kod języka pośredniego firmy Microsoft (MSIL) utworzony przez Tlbimp.exe, a następnie ponownie go skompilować.</span><span class="sxs-lookup"><span data-stu-id="6f668-195">You can provide the marshaler with the array size by editing the Microsoft intermediate language (MSIL) code produced by Tlbimp.exe and then recompiling it.</span></span> <span data-ttu-id="6f668-196">Aby uzyskać szczegółowe informacje na temat modyfikowania kodu MSIL, zobacz Dostosowywanie wywoływanych [otok środowiska uruchomieniowego](/previous-versions/dotnet/netframework-4.0/e753eftz(v=vs.100)).</span><span class="sxs-lookup"><span data-stu-id="6f668-196">For details about how to modify MSIL code, see [Customizing Runtime Callable Wrappers](/previous-versions/dotnet/netframework-4.0/e753eftz(v=vs.100)).</span></span> <span data-ttu-id="6f668-197">Aby wskazać liczbę elementów w tablicy, Zastosuj <xref:System.Runtime.InteropServices.MarshalAsAttribute> Typ do parametru array definicji metody zarządzanej w jeden z następujących sposobów:</span><span class="sxs-lookup"><span data-stu-id="6f668-197">To indicate the number of elements in the array, apply the <xref:System.Runtime.InteropServices.MarshalAsAttribute> type to the array parameter of the managed method definition in one of the following ways:</span></span>  
  
- <span data-ttu-id="6f668-198">Zidentyfikuj inny parametr zawierający liczbę elementów w tablicy.</span><span class="sxs-lookup"><span data-stu-id="6f668-198">Identify another parameter that contains the number of elements in the array.</span></span> <span data-ttu-id="6f668-199">Parametry są identyfikowane według pozycji, rozpoczynając od pierwszego parametru jako numer 0.</span><span class="sxs-lookup"><span data-stu-id="6f668-199">The parameters are identified by position, starting with the first parameter as number 0.</span></span>
  
    ```vb  
    Sub [New](ElemCnt As Integer, _  
       \<MarshalAs(UnmanagedType.LPArray, SizeParamIndex:=1)> _  
       ar() As Integer)  
    ```  
  
    ```csharp  
    void New(  
       int ElemCnt,
       [MarshalAs(UnmanagedType.LPArray, SizeParamIndex=0)] int[] ar );  
    ```  
  
- <span data-ttu-id="6f668-200">Zdefiniuj rozmiar tablicy jako stałą.</span><span class="sxs-lookup"><span data-stu-id="6f668-200">Define the size of the array as a constant.</span></span> <span data-ttu-id="6f668-201">Przykład:</span><span class="sxs-lookup"><span data-stu-id="6f668-201">For example:</span></span>  
  
    ```vb  
    Sub [New](\<MarshalAs(UnmanagedType.LPArray, SizeConst:=128)> _  
       ar() As Integer)  
    ```  
  
    ```csharp  
    void New(  
       [MarshalAs(UnmanagedType.LPArray, SizeConst=128)] int[] ar );  
    ```  
  
 <span data-ttu-id="6f668-202">Podczas organizowania tablic z niezarządzanego kodu do kodu zarządzanego Organizator sprawdza, czy atrybut **MarshalAsAttribute** skojarzony z parametrem, aby określić rozmiar tablicy.</span><span class="sxs-lookup"><span data-stu-id="6f668-202">When marshaling arrays from unmanaged code to managed code, the marshaler checks the **MarshalAsAttribute** associated with the parameter to determine the array size.</span></span> <span data-ttu-id="6f668-203">Jeśli rozmiar tablicy nie zostanie określony, tylko jeden element jest zorganizowany.</span><span class="sxs-lookup"><span data-stu-id="6f668-203">If the array size is not specified, only one element is marshaled.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="6f668-204">Wartość **MarshalAsAttribute** nie ma wpływu na kierowanie tablic zarządzanych do kodu niezarządzanego.</span><span class="sxs-lookup"><span data-stu-id="6f668-204">The **MarshalAsAttribute** has no effect on marshaling managed arrays to unmanaged code.</span></span> <span data-ttu-id="6f668-205">W tym kierunku rozmiar tablicy jest określany przez badanie.</span><span class="sxs-lookup"><span data-stu-id="6f668-205">In that direction, the array size is determined by examination.</span></span> <span data-ttu-id="6f668-206">Nie istnieje sposób organizowania podzestawu zarządzanej tablicy.</span><span class="sxs-lookup"><span data-stu-id="6f668-206">There is no way to marshal a subset of a managed array.</span></span>  
  
 <span data-ttu-id="6f668-207">Organizator międzyoperacyjny używa metod **CoTaskMemAlloc** i **CoTaskMemFree** do przydzielania i pobierania pamięci.</span><span class="sxs-lookup"><span data-stu-id="6f668-207">The interop marshaler uses the **CoTaskMemAlloc** and **CoTaskMemFree** methods to allocate and retrieve memory.</span></span> <span data-ttu-id="6f668-208">Alokacja pamięci wykonywana przez kod niezarządzany również musi używać tych metod.</span><span class="sxs-lookup"><span data-stu-id="6f668-208">Memory allocation performed by unmanaged code must also use these methods.</span></span>  
  
## <a name="passing-arrays-to-com"></a><span data-ttu-id="6f668-209">Przekazywanie tablic do modelu COM</span><span class="sxs-lookup"><span data-stu-id="6f668-209">Passing Arrays to COM</span></span>  
 <span data-ttu-id="6f668-210">Wszystkie typy tablicy zarządzanej mogą być przesyłane do niezarządzanego kodu z kodu zarządzanego.</span><span class="sxs-lookup"><span data-stu-id="6f668-210">All managed array types can be passed to unmanaged code from managed code.</span></span> <span data-ttu-id="6f668-211">W zależności od typu zarządzanego i zastosowanych do niego atrybutów tablica może być dostępna jako bezpieczna tablica lub tablica w stylu C, jak pokazano w poniższej tabeli.</span><span class="sxs-lookup"><span data-stu-id="6f668-211">Depending on the managed type and the attributes applied to it, the array can be accessed as a safe array or a C-style array, as shown in the following table.</span></span>  
  
|<span data-ttu-id="6f668-212">Typ tablicy zarządzanej</span><span class="sxs-lookup"><span data-stu-id="6f668-212">Managed array type</span></span>|<span data-ttu-id="6f668-213">Wyeksportowany jako</span><span class="sxs-lookup"><span data-stu-id="6f668-213">Exported as</span></span>|  
|------------------------|-----------------|  
|<span data-ttu-id="6f668-214">**ELEMENT_TYPE_SZARRAY\*\*\*\*\<** *type* **>**</span><span class="sxs-lookup"><span data-stu-id="6f668-214">**ELEMENT_TYPE_SZARRAY** **\<** *type* **>**</span></span>|<span data-ttu-id="6f668-215"><xref:System.Runtime.InteropServices.UnmanagedType>**. SafeArray (** *Typ* **)**</span><span class="sxs-lookup"><span data-stu-id="6f668-215"><xref:System.Runtime.InteropServices.UnmanagedType> **.SafeArray(** *type* **)**</span></span><br /><br /> <span data-ttu-id="6f668-216">**UnmanagedType. LPArray**</span><span class="sxs-lookup"><span data-stu-id="6f668-216">**UnmanagedType.LPArray**</span></span><br /><br /> <span data-ttu-id="6f668-217">Typ jest podany w podpisie.</span><span class="sxs-lookup"><span data-stu-id="6f668-217">Type is provided in the signature.</span></span> <span data-ttu-id="6f668-218">Ranga jest zawsze 1, Dolna granica jest zawsze równa 0.</span><span class="sxs-lookup"><span data-stu-id="6f668-218">Rank is always 1, lower bound is always 0.</span></span> <span data-ttu-id="6f668-219">Rozmiar jest zawsze znany w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="6f668-219">Size is always known at run time.</span></span>|  
|<span data-ttu-id="6f668-220">**ELEMENT_TYPE_ARRAY** **\<** *type* **>** **\<** *rank* **>**[**\<** *bounds* **>**]</span><span class="sxs-lookup"><span data-stu-id="6f668-220">**ELEMENT_TYPE_ARRAY** **\<** *type* **>** **\<** *rank* **>**[**\<** *bounds* **>**]</span></span>|<span data-ttu-id="6f668-221">**UnmanagedType. SAFEARRAY (** *Typ* **)**</span><span class="sxs-lookup"><span data-stu-id="6f668-221">**UnmanagedType.SafeArray(** *type* **)**</span></span><br /><br /> <span data-ttu-id="6f668-222">**UnmanagedType. LPArray**</span><span class="sxs-lookup"><span data-stu-id="6f668-222">**UnmanagedType.LPArray**</span></span><br /><br /> <span data-ttu-id="6f668-223">Typ, ranga, granice są podane w podpisie.</span><span class="sxs-lookup"><span data-stu-id="6f668-223">Type, rank, bounds are provided in the signature.</span></span> <span data-ttu-id="6f668-224">Rozmiar jest zawsze znany w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="6f668-224">Size is always known at run time.</span></span>|  
|<span data-ttu-id="6f668-225">**ELEMENT_TYPE_CLASS\*\*\*\*\<**<xref:System.Array?displayProperty=nameWithType>**>\*\*</span><span class="sxs-lookup"><span data-stu-id="6f668-225">**ELEMENT_TYPE_CLASS** **\<**<xref:System.Array?displayProperty=nameWithType>**>\*\*</span></span>|<span data-ttu-id="6f668-226">**UT_Interface**</span><span class="sxs-lookup"><span data-stu-id="6f668-226">**UT_Interface**</span></span><br /><br /> <span data-ttu-id="6f668-227">**UnmanagedType. SAFEARRAY (** *Typ* **)**</span><span class="sxs-lookup"><span data-stu-id="6f668-227">**UnmanagedType.SafeArray(** *type* **)**</span></span><br /><br /> <span data-ttu-id="6f668-228">Typ, ranga, granice i rozmiar są zawsze znane w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="6f668-228">Type, rank, bounds, and size are always known at run time.</span></span>|  
  
 <span data-ttu-id="6f668-229">Istnieje ograniczenie dotyczące automatyzacji OLE odnoszące się do tablic struktur, które zawierają LPSTR lub LPWSTR.</span><span class="sxs-lookup"><span data-stu-id="6f668-229">There is a limitation in OLE Automation relating to arrays of structures that contain LPSTR or LPWSTR.</span></span>  <span data-ttu-id="6f668-230">W związku z tym pola **String** muszą być organizowane jako **UnmanagedType. BSTR**.</span><span class="sxs-lookup"><span data-stu-id="6f668-230">Therefore, **String** fields have to be marshaled as **UnmanagedType.BSTR**.</span></span> <span data-ttu-id="6f668-231">W przeciwnym razie zostanie zgłoszony wyjątek.</span><span class="sxs-lookup"><span data-stu-id="6f668-231">Otherwise, an exception will be thrown.</span></span>  
  
### <a name="element_type_szarray"></a><span data-ttu-id="6f668-232">ELEMENT_TYPE_SZARRAY</span><span class="sxs-lookup"><span data-stu-id="6f668-232">ELEMENT_TYPE_SZARRAY</span></span>  
 <span data-ttu-id="6f668-233">Gdy metoda zawierająca parametr **ELEMENT_TYPE_SZARRAY** (tablica Jednowymiarowa) jest eksportowana z zestawu .NET do biblioteki typów, parametr array jest konwertowany na typ **SAFEARRAY** danego typu.</span><span class="sxs-lookup"><span data-stu-id="6f668-233">When a method containing an **ELEMENT_TYPE_SZARRAY** parameter (one-dimensional array) is exported from a .NET assembly to a type library, the array parameter is converted to a **SAFEARRAY** of a given type.</span></span> <span data-ttu-id="6f668-234">Te same reguły konwersji mają zastosowanie do typów elementów tablicy.</span><span class="sxs-lookup"><span data-stu-id="6f668-234">The same conversion rules apply to the array element types.</span></span> <span data-ttu-id="6f668-235">Zawartość tablicy zarządzanej jest automatycznie kopiowana z pamięci zarządzanej do elementu **SAFEARRAY**.</span><span class="sxs-lookup"><span data-stu-id="6f668-235">The contents of the managed array are automatically copied from managed memory into the **SAFEARRAY**.</span></span> <span data-ttu-id="6f668-236">Przykład:</span><span class="sxs-lookup"><span data-stu-id="6f668-236">For example:</span></span>  
  
#### <a name="managed-signature"></a><span data-ttu-id="6f668-237">Sygnatura zarządzana</span><span class="sxs-lookup"><span data-stu-id="6f668-237">Managed signature</span></span>  
  
```vb  
Sub [New](ar() As Long)  
Sub [New](ar() As String)  
```  
  
```csharp  
void New(long[] ar );  
void New(String[] ar );  
```  
  
#### <a name="unmanaged-signature"></a><span data-ttu-id="6f668-238">Niezarządzany podpis</span><span class="sxs-lookup"><span data-stu-id="6f668-238">Unmanaged signature</span></span>  
  
```cpp
HRESULT New([in] SAFEARRAY( long ) ar);
HRESULT New([in] SAFEARRAY( BSTR ) ar);  
```  
  
 <span data-ttu-id="6f668-239">Ranga tablic bezpiecznych jest zawsze 1, a dolna granica jest zawsze równa 0.</span><span class="sxs-lookup"><span data-stu-id="6f668-239">The rank of the safe arrays is always 1 and the lower bound is always 0.</span></span> <span data-ttu-id="6f668-240">Rozmiar jest określany w czasie wykonywania przez rozmiar przesyłanej tablicy zarządzanej.</span><span class="sxs-lookup"><span data-stu-id="6f668-240">The size is determined at run time by the size of the managed array being passed.</span></span>  
  
 <span data-ttu-id="6f668-241">Tablica może być również organizowana jako tablica w stylu C przy użyciu <xref:System.Runtime.InteropServices.MarshalAsAttribute> atrybutu.</span><span class="sxs-lookup"><span data-stu-id="6f668-241">The array can also be marshaled as a C-style array by using the <xref:System.Runtime.InteropServices.MarshalAsAttribute> attribute.</span></span> <span data-ttu-id="6f668-242">Przykład:</span><span class="sxs-lookup"><span data-stu-id="6f668-242">For example:</span></span>  
  
#### <a name="managed-signature"></a><span data-ttu-id="6f668-243">Sygnatura zarządzana</span><span class="sxs-lookup"><span data-stu-id="6f668-243">Managed signature</span></span>  
  
```vb  
Sub [New](<MarshalAs(UnmanagedType.LPArray, SizeParamIndex:=1)> _  
   ar() As Long, size as Integer)  
Sub [New](<MarshalAs(UnmanagedType.LPArray, SizeParamIndex:=1)> _  
   ar() As String, size as Integer)  
Sub [New](<MarshalAs(UnmanagedType.LPArray, _  
   ArraySubType= UnmanagedType.LPStr, SizeParamIndex:=1)> _  
   ar() As String, size as Integer)  
```  
  
```csharp  
void New([MarshalAs(UnmanagedType.LPArray, SizeParamIndex=1)]
   long [] ar, int size );  
void New([MarshalAs(UnmanagedType.LPArray, SizeParamIndex=1)]
   String [] ar, int size );  
void New([MarshalAs(UnmanagedType.LPArray, ArraySubType=
   UnmanagedType.LPStr, SizeParamIndex=1)]
   String [] ar, int size );  
```  
  
#### <a name="unmanaged-signature"></a><span data-ttu-id="6f668-244">Niezarządzany podpis</span><span class="sxs-lookup"><span data-stu-id="6f668-244">Unmanaged signature</span></span>  
  
```cpp
HRESULT New(long ar[]);
HRESULT New(BSTR ar[]);
HRESULT New(LPStr ar[]);  
```  
  
 <span data-ttu-id="6f668-245">Chociaż Organizator ma informacje o długości wymaganej do zorganizowania tablicy, Długość tablicy jest zwykle przekazywany jako oddzielny argument, aby przekazać długość do elementu wywoływanego.</span><span class="sxs-lookup"><span data-stu-id="6f668-245">Although the marshaler has the length information needed to marshal the array, the array length is usually passed as a separate argument to convey the length to the callee.</span></span>  
  
### <a name="element_type_array"></a><span data-ttu-id="6f668-246">ELEMENT_TYPE_ARRAY</span><span class="sxs-lookup"><span data-stu-id="6f668-246">ELEMENT_TYPE_ARRAY</span></span>  
 <span data-ttu-id="6f668-247">Gdy metoda zawierająca parametr **ELEMENT_TYPE_ARRAY** zostanie wyeksportowana z zestawu .NET do biblioteki typów, parametr array jest konwertowany na typ **SAFEARRAY** danego typu.</span><span class="sxs-lookup"><span data-stu-id="6f668-247">When a method containing an **ELEMENT_TYPE_ARRAY** parameter is exported from a .NET assembly to a type library, the array parameter is converted to a **SAFEARRAY** of a given type.</span></span> <span data-ttu-id="6f668-248">Zawartość tablicy zarządzanej jest automatycznie kopiowana z pamięci zarządzanej do elementu **SAFEARRAY**.</span><span class="sxs-lookup"><span data-stu-id="6f668-248">The contents of the managed array are automatically copied from managed memory into the **SAFEARRAY**.</span></span> <span data-ttu-id="6f668-249">Przykład:</span><span class="sxs-lookup"><span data-stu-id="6f668-249">For example:</span></span>  
  
#### <a name="managed-signature"></a><span data-ttu-id="6f668-250">Sygnatura zarządzana</span><span class="sxs-lookup"><span data-stu-id="6f668-250">Managed signature</span></span>  
  
```vb  
Sub [New](ar(,) As Long)  
Sub [New](ar(,) As String)  
```  
  
```csharp  
void New( long [,] ar );  
void New( String [,] ar );  
```  
  
#### <a name="unmanaged-signature"></a><span data-ttu-id="6f668-251">Niezarządzany podpis</span><span class="sxs-lookup"><span data-stu-id="6f668-251">Unmanaged signature</span></span>  
  
```cpp
HRESULT New([in] SAFEARRAY( long ) ar);
HRESULT New([in] SAFEARRAY( BSTR ) ar);  
```  
  
 <span data-ttu-id="6f668-252">Ranga, rozmiar i granice bezpiecznych tablic są określane w czasie wykonywania przez charakterystykę zarządzanej tablicy.</span><span class="sxs-lookup"><span data-stu-id="6f668-252">The rank, size, and bounds of the safe arrays are determined at run time by the characteristics of the managed array.</span></span>  
  
 <span data-ttu-id="6f668-253">Tablica może być również organizowana jako tablica w stylu C przez zastosowanie <xref:System.Runtime.InteropServices.MarshalAsAttribute> atrybutu.</span><span class="sxs-lookup"><span data-stu-id="6f668-253">The array can also be marshaled as a C-style array by applying the <xref:System.Runtime.InteropServices.MarshalAsAttribute> attribute.</span></span> <span data-ttu-id="6f668-254">Przykład:</span><span class="sxs-lookup"><span data-stu-id="6f668-254">For example:</span></span>  
  
#### <a name="managed-signature"></a><span data-ttu-id="6f668-255">Sygnatura zarządzana</span><span class="sxs-lookup"><span data-stu-id="6f668-255">Managed signature</span></span>  
  
```vb  
Sub [New](<MarshalAs(UnmanagedType.LPARRAY, SizeParamIndex:=1)> _  
   ar(,) As Long, size As Integer)  
Sub [New](<MarshalAs(UnmanagedType.LPARRAY, _  
   ArraySubType:=UnmanagedType.LPStr, SizeParamIndex:=1)> _  
   ar(,) As String, size As Integer)  
```  
  
```csharp  
void New([MarshalAs(UnmanagedType.LPARRAY, SizeParamIndex=1)]
   long [,] ar, int size );  
void New([MarshalAs(UnmanagedType.LPARRAY,
   ArraySubType= UnmanagedType.LPStr, SizeParamIndex=1)]
   String [,] ar, int size );  
```  
  
#### <a name="unmanaged-signature"></a><span data-ttu-id="6f668-256">Niezarządzany podpis</span><span class="sxs-lookup"><span data-stu-id="6f668-256">Unmanaged signature</span></span>  
  
```cpp
HRESULT New(long ar[]);
HRESULT New(LPStr ar[]);  
```  
  
 <span data-ttu-id="6f668-257">Nie można zorganizować tablic zagnieżdżonych.</span><span class="sxs-lookup"><span data-stu-id="6f668-257">Nested arrays cannot be marshaled.</span></span> <span data-ttu-id="6f668-258">Na przykład następujący podpis generuje błąd podczas eksportowania z [eksporterem biblioteki typów (Tlbexp.exe)](../tools/tlbexp-exe-type-library-exporter.md).</span><span class="sxs-lookup"><span data-stu-id="6f668-258">For example, the following signature generates an error when exported with the [Type Library Exporter (Tlbexp.exe)](../tools/tlbexp-exe-type-library-exporter.md).</span></span>  
  
#### <a name="managed-signature"></a><span data-ttu-id="6f668-259">Sygnatura zarządzana</span><span class="sxs-lookup"><span data-stu-id="6f668-259">Managed signature</span></span>  
  
```vb  
Sub [New](ar()()() As Long)  
```  
  
```csharp  
void New(long [][][] ar );  
```  
  
### <a name="element_type_class-systemarray"></a><span data-ttu-id="6f668-260">ELEMENT_TYPE_CLASS \<System.Array></span><span class="sxs-lookup"><span data-stu-id="6f668-260">ELEMENT_TYPE_CLASS \<System.Array></span></span>  
 <span data-ttu-id="6f668-261">Gdy metoda zawierająca <xref:System.Array?displayProperty=nameWithType> parametr zostanie wyeksportowana z zestawu .NET do biblioteki typów, parametr array jest konwertowany na interfejs **_Array** .</span><span class="sxs-lookup"><span data-stu-id="6f668-261">When a method containing a <xref:System.Array?displayProperty=nameWithType> parameter is exported from a .NET assembly to a type library, the array parameter is converted to an **_Array** interface.</span></span> <span data-ttu-id="6f668-262">Zawartość tablicy zarządzanej jest dostępna tylko za pomocą metod i właściwości interfejsu **_Array** .</span><span class="sxs-lookup"><span data-stu-id="6f668-262">The contents of the managed array are accessible only through the methods and properties of the **_Array** interface.</span></span> <span data-ttu-id="6f668-263">Element **System. Array** może być również zorganizowany jako **SAFEARRAY** przy użyciu <xref:System.Runtime.InteropServices.MarshalAsAttribute> atrybutu.</span><span class="sxs-lookup"><span data-stu-id="6f668-263">**System.Array** can also be marshaled as a **SAFEARRAY** by using the <xref:System.Runtime.InteropServices.MarshalAsAttribute> attribute.</span></span> <span data-ttu-id="6f668-264">Gdy jest zorganizowany jako bezpieczna tablica, elementy tablicy są organizowane jako warianty.</span><span class="sxs-lookup"><span data-stu-id="6f668-264">When marshaled as a safe array, the array elements are marshaled as variants.</span></span> <span data-ttu-id="6f668-265">Przykład:</span><span class="sxs-lookup"><span data-stu-id="6f668-265">For example:</span></span>  
  
#### <a name="managed-signature"></a><span data-ttu-id="6f668-266">Sygnatura zarządzana</span><span class="sxs-lookup"><span data-stu-id="6f668-266">Managed signature</span></span>  
  
```vb  
Sub New1( ar As System.Array )  
Sub New2( <MarshalAs(UnmanagedType.Safe array)> ar As System.Array )  
```  
  
```csharp  
void New1( System.Array ar );  
void New2( [MarshalAs(UnmanagedType.Safe array)] System.Array ar );  
```  
  
#### <a name="unmanaged-signature"></a><span data-ttu-id="6f668-267">Niezarządzany podpis</span><span class="sxs-lookup"><span data-stu-id="6f668-267">Unmanaged signature</span></span>  
  
```cpp
HRESULT New([in] _Array *ar);
HRESULT New([in] SAFEARRAY(VARIANT) ar);  
```  
  
### <a name="arrays-within-structures"></a><span data-ttu-id="6f668-268">Tablice w strukturach</span><span class="sxs-lookup"><span data-stu-id="6f668-268">Arrays within Structures</span></span>  
 <span data-ttu-id="6f668-269">Struktury niezarządzane mogą zawierać osadzone tablice.</span><span class="sxs-lookup"><span data-stu-id="6f668-269">Unmanaged structures can contain embedded arrays.</span></span> <span data-ttu-id="6f668-270">Domyślnie te osadzone pola tablicy są organizowane jako SAFEARRAY.</span><span class="sxs-lookup"><span data-stu-id="6f668-270">By default, these embedded array fields are marshaled as a SAFEARRAY.</span></span> <span data-ttu-id="6f668-271">W poniższym przykładzie `s1` jest osadzoną tablicą przydzieloną bezpośrednio w samej strukturze.</span><span class="sxs-lookup"><span data-stu-id="6f668-271">In the following example, `s1` is an embedded array that is allocated directly within the structure itself.</span></span>  
  
#### <a name="unmanaged-representation"></a><span data-ttu-id="6f668-272">Reprezentacja niezarządzana</span><span class="sxs-lookup"><span data-stu-id="6f668-272">Unmanaged representation</span></span>  
  
```cpp
struct MyStruct {  
    short s1[128];  
}  
```  
  
 <span data-ttu-id="6f668-273">Tablice mogą być organizowane jako <xref:System.Runtime.InteropServices.UnmanagedType> , co wymaga ustawienia <xref:System.Runtime.InteropServices.MarshalAsAttribute> pola.</span><span class="sxs-lookup"><span data-stu-id="6f668-273">Arrays can be marshaled as <xref:System.Runtime.InteropServices.UnmanagedType>, which requires you to set the <xref:System.Runtime.InteropServices.MarshalAsAttribute> field.</span></span> <span data-ttu-id="6f668-274">Rozmiar można ustawić tylko jako stała.</span><span class="sxs-lookup"><span data-stu-id="6f668-274">The size can be set only as a constant.</span></span> <span data-ttu-id="6f668-275">Poniższy kod pokazuje odpowiadającą zarządzane definicje `MyStruct` .</span><span class="sxs-lookup"><span data-stu-id="6f668-275">The following code shows the corresponding managed definition of `MyStruct`.</span></span>  
  
```vb  
Public Structure <StructLayout(LayoutKind.Sequential)> MyStruct  
   Public <MarshalAs(UnmanagedType.ByValArray, SizeConst := 128)> _  
     s1() As Short  
End Structure  
```  
  
```csharp  
[StructLayout(LayoutKind.Sequential)]  
public struct MyStruct {  
   [MarshalAs(UnmanagedType.ByValArray, SizeConst=128)] public short[] s1;  
}  
```  
  
## <a name="see-also"></a><span data-ttu-id="6f668-276">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="6f668-276">See also</span></span>

- [<span data-ttu-id="6f668-277">Domyślne zachowanie marshalingu</span><span class="sxs-lookup"><span data-stu-id="6f668-277">Default Marshaling Behavior</span></span>](default-marshaling-behavior.md)
- [<span data-ttu-id="6f668-278">Typy kopiowalne i niekopiowalne</span><span class="sxs-lookup"><span data-stu-id="6f668-278">Blittable and Non-Blittable Types</span></span>](blittable-and-non-blittable-types.md)
- <span data-ttu-id="6f668-279">[Atrybuty kierunkowe](/previous-versions/dotnet/netframework-4.0/77e6taeh(v=vs.100))</span><span class="sxs-lookup"><span data-stu-id="6f668-279">[Directional Attributes](/previous-versions/dotnet/netframework-4.0/77e6taeh(v=vs.100))</span></span>
- [<span data-ttu-id="6f668-280">Kopiowanie i przypinanie</span><span class="sxs-lookup"><span data-stu-id="6f668-280">Copying and Pinning</span></span>](copying-and-pinning.md)
