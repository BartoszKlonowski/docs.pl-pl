---
title: exceptionSwallowedOnCallFromCom MDA
description: Zapoznaj się z asystentem debugowania zarządzanego przez exceptionSwallowedOnCallFromCOM w programie .NET. To zdarzenie MDA występuje, jeśli wystąpił wyjątek, ale nie istnieje dobry sposób na zgłoszenie go.
ms.date: 03/30/2017
helpviewer_keywords:
- messages, informational
- informational messages
- managed debugging assistants (MDAs), exceptions
- exception handling, managed debugging assistants
- MDAs (managed debugging assistants), exceptions
- ExceptionSwallowedOnCallFromCOM MDA
ms.assetid: 55d6ab12-f251-4aab-aa64-aacbe9d9f974
ms.openlocfilehash: 11daccb4d1e757bf2fae25858d706eee5921c509
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96244356"
---
# <a name="exceptionswallowedoncallfromcom-mda"></a><span data-ttu-id="2876e-104">exceptionSwallowedOnCallFromCom MDA</span><span class="sxs-lookup"><span data-stu-id="2876e-104">exceptionSwallowedOnCallFromCom MDA</span></span>

<span data-ttu-id="2876e-105">`exceptionSwallowedOnCallFromCOM`Asystent debugowania zarządzanego (MDA) jest uaktywniany, gdy wyjątek jest zgłaszany z kodu środowiska uruchomieniowego języka wspólnego (CLR) wywoływanego z modelu COM za pomocą metody, która nie ma niezarządzanego zwracanego typu HRESULT.</span><span class="sxs-lookup"><span data-stu-id="2876e-105">The `exceptionSwallowedOnCallFromCOM` managed debugging assistant (MDA) is activated when an exception is thrown from common language runtime (CLR) code called from COM via a method that does not have an unmanaged HRESULT return type.</span></span>  
  
## <a name="symptoms"></a><span data-ttu-id="2876e-106">Objawy</span><span class="sxs-lookup"><span data-stu-id="2876e-106">Symptoms</span></span>  

 <span data-ttu-id="2876e-107">Wywołanie zarządzanego składnika z modelu COM zwraca wartość FALSE lub 0.</span><span class="sxs-lookup"><span data-stu-id="2876e-107">A call to a managed component from COM returns with a value of FALSE or 0.</span></span> <span data-ttu-id="2876e-108">Alternatywnie, jeśli metoda ma typ zwracany void, może nie być wskazywać, że wyjątek został zgłoszony podczas wykonywania metody.</span><span class="sxs-lookup"><span data-stu-id="2876e-108">Alternatively, if the method has a void return type, there may be no indication that an exception was thrown during the execution of the method.</span></span> <span data-ttu-id="2876e-109">W takim przypadku wyjątek zostanie przechwycony w trybie dyskretnym, a wykonywanie zwróci do obiektu wywołującego COM.</span><span class="sxs-lookup"><span data-stu-id="2876e-109">In this case, the exception will be silently caught and execution will return to the COM caller.</span></span>  
  
## <a name="cause"></a><span data-ttu-id="2876e-110">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="2876e-110">Cause</span></span>  

 <span data-ttu-id="2876e-111">Zgłoszono wyjątek, ale nie ma prawidłowego sposobu na jego raportowanie.</span><span class="sxs-lookup"><span data-stu-id="2876e-111">An exception was thrown, but there is no valid way to report it.</span></span>  
  
## <a name="resolution"></a><span data-ttu-id="2876e-112">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="2876e-112">Resolution</span></span>  

 <span data-ttu-id="2876e-113">Tylko informacyjne, niekoniecznie wskazujące usterkę.</span><span class="sxs-lookup"><span data-stu-id="2876e-113">Informational only, not necessarily indicative of a bug.</span></span>  
  
## <a name="effect-on-the-runtime"></a><span data-ttu-id="2876e-114">Wpływ na środowisko uruchomieniowe</span><span class="sxs-lookup"><span data-stu-id="2876e-114">Effect on the Runtime</span></span>  

 <span data-ttu-id="2876e-115">To zdarzenie MDA nie ma wpływu na środowisko CLR.</span><span class="sxs-lookup"><span data-stu-id="2876e-115">This MDA has no effect on the CLR.</span></span> <span data-ttu-id="2876e-116">Raport dotyczy tylko danych o przechwyconych dyskretnie wyjątkach.</span><span class="sxs-lookup"><span data-stu-id="2876e-116">It only reports data about silently caught exceptions.</span></span>  
  
## <a name="output"></a><span data-ttu-id="2876e-117">Dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="2876e-117">Output</span></span>  

 <span data-ttu-id="2876e-118">Komunikat informacyjny zawierający nazwę metody, nazwę typu i komunikat o wyjątku.</span><span class="sxs-lookup"><span data-stu-id="2876e-118">Informational message containing the method name, type name, and exception message.</span></span>  
  
## <a name="configuration"></a><span data-ttu-id="2876e-119">Konfigurowanie</span><span class="sxs-lookup"><span data-stu-id="2876e-119">Configuration</span></span>  
  
```xml  
<mdaConfig>  
  <assistants>  
    <exceptionSwallowedOnCallFromCom />  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="see-also"></a><span data-ttu-id="2876e-120">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="2876e-120">See also</span></span>

- <xref:System.Runtime.InteropServices.MarshalAsAttribute>
- [<span data-ttu-id="2876e-121">Diagnozowanie błędów przy użyciu asystentów zarządzanego debugowania</span><span class="sxs-lookup"><span data-stu-id="2876e-121">Diagnosing Errors with Managed Debugging Assistants</span></span>](diagnosing-errors-with-managed-debugging-assistants.md)
- [<span data-ttu-id="2876e-122">Organizowanie międzyoperacyjne</span><span class="sxs-lookup"><span data-stu-id="2876e-122">Interop Marshaling</span></span>](../interop/interop-marshaling.md)
