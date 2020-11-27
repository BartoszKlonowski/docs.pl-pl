---
title: invalidOverlappedToPinvoke MDA
description: Zapoznaj się z asystentem debugowania zarządzanego invalidOverlappedToPinvoke (MDA) w programie .NET, który może być aktywowany podczas awarii lub niewyjaśnionego uszkodzenia sterty.
ms.date: 03/30/2017
helpviewer_keywords:
- overlapped pointers
- managed debugging assistants (MDAs), overlapped pointers
- invalid overlapped pointer to platform invoke
- InvalidOverlappedToPinvoke MDA
- MDAs (managed debugging assistants), overlapped pointers
- pointers, overlapped
ms.assetid: 28876047-58bd-4fed-9452-c7da346d67c0
ms.openlocfilehash: 55b10af87130bd32410508cef2bc3e4e733549c0
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96281328"
---
# <a name="invalidoverlappedtopinvoke-mda"></a><span data-ttu-id="32895-103">invalidOverlappedToPinvoke MDA</span><span class="sxs-lookup"><span data-stu-id="32895-103">invalidOverlappedToPinvoke MDA</span></span>

<span data-ttu-id="32895-104">`invalidOverlappedToPinvoke`Asystent debugowania zarządzanego (MDA) jest uaktywniany, gdy nakładający się wskaźnik, który nie został utworzony na stercie wyrzucania elementów bezużytecznych, jest przesyłany do określonych funkcji Win32.</span><span class="sxs-lookup"><span data-stu-id="32895-104">The `invalidOverlappedToPinvoke` managed debugging assistant (MDA) is activated when an overlapped pointer that was not created on the garbage collection heap is passed to specific Win32 functions.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="32895-105">Domyślnie to zdarzenie MDA jest uaktywniane tylko wtedy, gdy wywołanie wywoływana przez platformę jest zdefiniowane w kodzie, a debuger raportuje stan JustMyCode każdej z tych metod.</span><span class="sxs-lookup"><span data-stu-id="32895-105">By default, this MDA is activated only if the platform invoke call is defined in your code and the debugger reports the JustMyCode status of each method.</span></span> <span data-ttu-id="32895-106">Debuger, który nie rozpoznaje JustMyCode (takich jak MDbg.exe bez rozszerzeń), nie aktywuje tego MDA.</span><span class="sxs-lookup"><span data-stu-id="32895-106">A debugger that does not understand JustMyCode (such as MDbg.exe with no extensions) will not activate this MDA.</span></span> <span data-ttu-id="32895-107">To zdarzenie MDA można włączyć dla tych debugerów przy użyciu pliku konfiguracji i jawnie wyraźnych `justMyCode="false"` w pliku .mda.config `(<invalidOverlappedToPinvoke enable="true" justMyCode="false"/>` ).</span><span class="sxs-lookup"><span data-stu-id="32895-107">This MDA can be enabled for those debuggers by using a configuration file and explicitly settting `justMyCode="false"` in the .mda.config file `(<invalidOverlappedToPinvoke enable="true" justMyCode="false"/>`).</span></span>  
  
## <a name="symptoms"></a><span data-ttu-id="32895-108">Objawy</span><span class="sxs-lookup"><span data-stu-id="32895-108">Symptoms</span></span>  

 <span data-ttu-id="32895-109">Awarie stosu lub niewyjaśnione uszkodzenia sterty.</span><span class="sxs-lookup"><span data-stu-id="32895-109">Crashes or unexplainable heap corruptions.</span></span>  
  
## <a name="cause"></a><span data-ttu-id="32895-110">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="32895-110">Cause</span></span>  

 <span data-ttu-id="32895-111">Nakładający się wskaźnik, który nie został utworzony na stercie wyrzucania elementów bezużytecznych, jest przesyłany do określonych funkcji systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="32895-111">An overlapped pointer that was not created on the garbage collection heap is passed to specific operating system functions.</span></span>  
  
 <span data-ttu-id="32895-112">W poniższej tabeli przedstawiono funkcje, które są śledzone przez to zdarzenie MDA.</span><span class="sxs-lookup"><span data-stu-id="32895-112">The following table shows the functions that this MDA tracks.</span></span>  
  
|<span data-ttu-id="32895-113">Moduł</span><span class="sxs-lookup"><span data-stu-id="32895-113">Module</span></span>|<span data-ttu-id="32895-114">Funkcja</span><span class="sxs-lookup"><span data-stu-id="32895-114">Function</span></span>|  
|------------|--------------|  
|<span data-ttu-id="32895-115">HttpApi.dll</span><span class="sxs-lookup"><span data-stu-id="32895-115">HttpApi.dll</span></span>|`HttpReceiveHttpRequest`|  
|<span data-ttu-id="32895-116">IpHlpApi.dll</span><span class="sxs-lookup"><span data-stu-id="32895-116">IpHlpApi.dll</span></span>|`NotifyAddrChange`|  
|<span data-ttu-id="32895-117">kernel32.dll</span><span class="sxs-lookup"><span data-stu-id="32895-117">kernel32.dll</span></span>|`ReadFile`|  
|<span data-ttu-id="32895-118">kernel32.dll</span><span class="sxs-lookup"><span data-stu-id="32895-118">kernel32.dll</span></span>|`ReadFileEx`|  
|<span data-ttu-id="32895-119">kernel32.dll</span><span class="sxs-lookup"><span data-stu-id="32895-119">kernel32.dll</span></span>|`WriteFile`|  
|<span data-ttu-id="32895-120">kernel32.dll</span><span class="sxs-lookup"><span data-stu-id="32895-120">kernel32.dll</span></span>|`WriteFileEx`|  
|<span data-ttu-id="32895-121">kernel32.dll</span><span class="sxs-lookup"><span data-stu-id="32895-121">kernel32.dll</span></span>|`ReadDirectoryChangesW`|  
|<span data-ttu-id="32895-122">kernel32.dll</span><span class="sxs-lookup"><span data-stu-id="32895-122">kernel32.dll</span></span>|`PostQueuedCompletionStatus`|  
|<span data-ttu-id="32895-123">MSWSock.dll</span><span class="sxs-lookup"><span data-stu-id="32895-123">MSWSock.dll</span></span>|`ConnectEx`|  
|<span data-ttu-id="32895-124">WS2_32.dll</span><span class="sxs-lookup"><span data-stu-id="32895-124">WS2_32.dll</span></span>|`WSASend`|  
|<span data-ttu-id="32895-125">WS2_32.dll</span><span class="sxs-lookup"><span data-stu-id="32895-125">WS2_32.dll</span></span>|`WSASendTo`|  
|<span data-ttu-id="32895-126">WS2_32.dll</span><span class="sxs-lookup"><span data-stu-id="32895-126">WS2_32.dll</span></span>|`WSARecv`|  
|<span data-ttu-id="32895-127">WS2_32.dll</span><span class="sxs-lookup"><span data-stu-id="32895-127">WS2_32.dll</span></span>|`WSARecvFrom`|  
|<span data-ttu-id="32895-128">MQRT.dll</span><span class="sxs-lookup"><span data-stu-id="32895-128">MQRT.dll</span></span>|`MQReceiveMessage`|  
  
 <span data-ttu-id="32895-129">Prawdopodobieństwo uszkodzenia sterty jest wysokie dla tego warunku, ponieważ <xref:System.AppDomain> wywołanie może zostać zwolnione.</span><span class="sxs-lookup"><span data-stu-id="32895-129">The potential for heap corruption is high for this condition because the <xref:System.AppDomain> making the call might unload.</span></span> <span data-ttu-id="32895-130">Jeśli zwalnia <xref:System.AppDomain> , kod aplikacji zwalnia pamięć dla nakładającego się wskaźnika, powodując uszkodzenie po zakończeniu operacji lub kod przecieka pamięć, co spowoduje problemy później.</span><span class="sxs-lookup"><span data-stu-id="32895-130">If the <xref:System.AppDomain> unloads, the application code will either free the memory for the overlapped pointer, causing corruption when the operation finishes, or the code will leak the memory, causing difficulties later.</span></span>  
  
## <a name="resolution"></a><span data-ttu-id="32895-131">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="32895-131">Resolution</span></span>  

 <span data-ttu-id="32895-132">Użyj <xref:System.Threading.Overlapped> obiektu, wywołując metodę, <xref:System.Threading.Overlapped.Pack%2A> Aby uzyskać <xref:System.Threading.NativeOverlapped> strukturę, która może zostać przeniesiona do funkcji.</span><span class="sxs-lookup"><span data-stu-id="32895-132">Use an <xref:System.Threading.Overlapped> object, calling the <xref:System.Threading.Overlapped.Pack%2A> method to get a <xref:System.Threading.NativeOverlapped> structure that can be passed to the function.</span></span> <span data-ttu-id="32895-133">Jeśli zwalnia <xref:System.AppDomain> , CLR czeka na zakończenie operacji asynchronicznej przed zwolnieniem wskaźnika.</span><span class="sxs-lookup"><span data-stu-id="32895-133">If the <xref:System.AppDomain> unloads, the CLR waits until the asynchronous operation completes before freeing the pointer.</span></span>  
  
## <a name="effect-on-the-runtime"></a><span data-ttu-id="32895-134">Wpływ na środowisko uruchomieniowe</span><span class="sxs-lookup"><span data-stu-id="32895-134">Effect on the Runtime</span></span>  

 <span data-ttu-id="32895-135">To zdarzenie MDA nie ma wpływu na środowisko CLR.</span><span class="sxs-lookup"><span data-stu-id="32895-135">This MDA had no effect on the CLR.</span></span>  
  
## <a name="output"></a><span data-ttu-id="32895-136">Dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="32895-136">Output</span></span>  

 <span data-ttu-id="32895-137">Poniżej znajduje się przykład danych wyjściowych z tego MDA.</span><span class="sxs-lookup"><span data-stu-id="32895-137">The following is an example of output from this MDA.</span></span>  
  
 `An overlapped pointer (0x00ea3430) that was not allocated on the GC heap was passed via Pinvoke to the Win32 function 'WriteFile' in module 'KERNEL32.DLL'. If the AppDomain is shut down, this can cause heap corruption when the async I/O completes. The best solution is to pass a NativeOverlapped structure retrieved from a call to System.Threading.Overlapped.Pack(). If the AppDomain exits, the CLR will keep this structure alive and pinned until the I/O completes.`  
  
## <a name="configuration"></a><span data-ttu-id="32895-138">Konfigurowanie</span><span class="sxs-lookup"><span data-stu-id="32895-138">Configuration</span></span>  
  
```xml  
<mdaConfig>  
  <assistants>  
    <invalidOverlappedToPinvoke/>  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="see-also"></a><span data-ttu-id="32895-139">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="32895-139">See also</span></span>

- <xref:System.Runtime.InteropServices.MarshalAsAttribute>
- [<span data-ttu-id="32895-140">Diagnozowanie błędów przy użyciu asystentów zarządzanego debugowania</span><span class="sxs-lookup"><span data-stu-id="32895-140">Diagnosing Errors with Managed Debugging Assistants</span></span>](diagnosing-errors-with-managed-debugging-assistants.md)
- [<span data-ttu-id="32895-141">Organizowanie międzyoperacyjne</span><span class="sxs-lookup"><span data-stu-id="32895-141">Interop Marshaling</span></span>](../interop/interop-marshaling.md)
