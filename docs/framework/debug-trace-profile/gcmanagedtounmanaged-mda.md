---
title: gcManagedToUnmanaged MDA
description: Zapoznaj się z asystentem debugowania zarządzanego przez gcManagedToUnmanaged. To zdarzenie MDA może zostać aktywowane z powodu przedwcześnie wyrzucania elementów bezużytecznych podczas przejścia do kodu niezarządzanego.
ms.date: 03/30/2017
helpviewer_keywords:
- MDAs (managed debugging assistants), garbage collection
- GcManagedToUnmanaged MDA
- GC managed to unmanaged
- transitioning threads managed to unmanaged code
- threading [.NET Framework], garbage collection
- managed to unmanaged garbage collection
- managed debugging assistants (MDAs), garbage collection
- threading [.NET Framework], managed debugging assistants
- garbage collection, run-time errors
ms.assetid: 7417f837-805e-4fed-a430-ca919c8421dc
ms.openlocfilehash: 668b06109e59f1239cd2b3e3017aeee1916ce69e
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96244239"
---
# <a name="gcmanagedtounmanaged-mda"></a><span data-ttu-id="c7882-104">gcManagedToUnmanaged MDA</span><span class="sxs-lookup"><span data-stu-id="c7882-104">gcManagedToUnmanaged MDA</span></span>

<span data-ttu-id="c7882-105">`gcManagedToUnmanaged`Asystent debugowania zarządzanego (MDA) powoduje wyrzucanie elementów bezużytecznych za każdym razem, gdy wątek przechodzi z zarządzanego do niezarządzanego kodu.</span><span class="sxs-lookup"><span data-stu-id="c7882-105">The `gcManagedToUnmanaged` managed debugging assistant (MDA) causes a garbage collection whenever a thread transitions from managed to unmanaged code.</span></span>  
  
## <a name="symptoms"></a><span data-ttu-id="c7882-106">Objawy</span><span class="sxs-lookup"><span data-stu-id="c7882-106">Symptoms</span></span>  

 <span data-ttu-id="c7882-107">Niezarządzany składnik użytkownika zgłasza naruszenie zasad dostępu podczas próby użycia zarządzanego obiektu, który został ujawniony w modelu COM.</span><span class="sxs-lookup"><span data-stu-id="c7882-107">An unmanaged user component throws an access violation when trying to use a managed object that had been exposed to COM.</span></span> <span data-ttu-id="c7882-108">Obiekt COM wydaje się być wystawiony.</span><span class="sxs-lookup"><span data-stu-id="c7882-108">The COM object appears to have been released.</span></span> <span data-ttu-id="c7882-109">Naruszenie zasad dostępu jest niejednoznaczne.</span><span class="sxs-lookup"><span data-stu-id="c7882-109">The access violation is nondeterministic.</span></span>  
  
## <a name="cause"></a><span data-ttu-id="c7882-110">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="c7882-110">Cause</span></span>  

 <span data-ttu-id="c7882-111">Jeśli składnik niezarządzany nie odwołuje się prawidłowo do prawidłowego zliczania zarządzanego obiektu COM, środowisko uruchomieniowe może zebrać obiekt zarządzany uwidoczniony do modelu COM, gdy składnik niezarządzany nadal utrzymuje odwołanie do obiektu.</span><span class="sxs-lookup"><span data-stu-id="c7882-111">If an unmanaged component is not reference counting a managed COM object correctly, then the runtime could collect a managed object exposed to COM when the unmanaged component still holds a reference to the object.</span></span> <span data-ttu-id="c7882-112">Środowisko uruchomieniowe wywołuje <xref:System.Runtime.InteropServices.Marshal.Release%2A> podczas odzyskiwania pamięci, więc jeśli składnik użytkownika używa obiektu przed wystąpieniem bezużyteczności, wówczas nie został jeszcze zebrany.</span><span class="sxs-lookup"><span data-stu-id="c7882-112">The runtime calls <xref:System.Runtime.InteropServices.Marshal.Release%2A> during garbage collections, so if the user component uses the object before the garbage collection occurs, then it will not yet have been collected.</span></span> <span data-ttu-id="c7882-113">To jest źródło nieustalenia.</span><span class="sxs-lookup"><span data-stu-id="c7882-113">This is the source of the nondeterminism.</span></span>  
  
## <a name="resolution"></a><span data-ttu-id="c7882-114">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="c7882-114">Resolution</span></span>  

 <span data-ttu-id="c7882-115">Włączenie tego asystenta skraca czas od momentu, gdy obiekt kwalifikuje się do kolekcji i <xref:System.Runtime.InteropServices.Marshal.Release%2A> jest wywoływany, ułatwiając śledzenie, który składnik niezarządzany najpierw próbuje uzyskać dostęp do zebranego obiektu.</span><span class="sxs-lookup"><span data-stu-id="c7882-115">Enabling this assistant reduces the time between when the object is eligible for collection and <xref:System.Runtime.InteropServices.Marshal.Release%2A> is called, helping to track down which unmanaged component first tries to access the collected object.</span></span>  
  
## <a name="effect-on-the-runtime"></a><span data-ttu-id="c7882-116">Wpływ na środowisko uruchomieniowe</span><span class="sxs-lookup"><span data-stu-id="c7882-116">Effect on the Runtime</span></span>  

 <span data-ttu-id="c7882-117">Powoduje wyrzucanie elementów bezużytecznych po każdym przejścia wątku z zarządzanego do niezarządzanego kodu.</span><span class="sxs-lookup"><span data-stu-id="c7882-117">Causes a garbage collection whenever a thread transitions from managed to unmanaged code.</span></span>  
  
## <a name="output"></a><span data-ttu-id="c7882-118">Dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="c7882-118">Output</span></span>  

 <span data-ttu-id="c7882-119">To zdarzenie MDA nie generuje danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="c7882-119">This MDA produces no output.</span></span>  
  
## <a name="configuration"></a><span data-ttu-id="c7882-120">Konfigurowanie</span><span class="sxs-lookup"><span data-stu-id="c7882-120">Configuration</span></span>  
  
```xml  
<mdaConfig>  
  <assistants>  
    <gcManagedToUnmanaged/>  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="see-also"></a><span data-ttu-id="c7882-121">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="c7882-121">See also</span></span>

- <xref:System.Runtime.InteropServices.MarshalAsAttribute>
- [<span data-ttu-id="c7882-122">Diagnozowanie błędów przy użyciu asystentów zarządzanego debugowania</span><span class="sxs-lookup"><span data-stu-id="c7882-122">Diagnosing Errors with Managed Debugging Assistants</span></span>](diagnosing-errors-with-managed-debugging-assistants.md)
- [<span data-ttu-id="c7882-123">Organizowanie międzyoperacyjne</span><span class="sxs-lookup"><span data-stu-id="c7882-123">Interop Marshaling</span></span>](../interop/interop-marshaling.md)
- [<span data-ttu-id="c7882-124">gcUnmanagedToManaged</span><span class="sxs-lookup"><span data-stu-id="c7882-124">gcUnmanagedToManaged</span></span>](gcunmanagedtomanaged-mda.md)
