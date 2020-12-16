---
title: Ostrzeżenie SYSLIB0004
description: Dowiedz się więcej o Obsoletions, które generują ostrzeżenie SYSLIB0004 w czasie kompilacji.
ms.topic: reference
ms.date: 10/20/2020
ms.openlocfilehash: 03be8bb54f71f74ed94ee2c3f8489397ae1e99b5
ms.sourcegitcommit: e301979e3049ce412d19b094c60ed95b316a8f8c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/16/2020
ms.locfileid: "97596560"
---
# <a name="syslib0004-the-constrained-execution-region-cer-feature-is-not-supported"></a><span data-ttu-id="94bd0-103">SYSLIB0004: funkcja ograniczonego regionu wykonywania (CER) nie jest obsługiwana</span><span class="sxs-lookup"><span data-stu-id="94bd0-103">SYSLIB0004: The constrained execution region (CER) feature is not supported</span></span>

<span data-ttu-id="94bd0-104">Funkcja [ograniczone regiony wykonywania (CER)](../../../framework/performance/constrained-execution-regions.md) jest obsługiwana tylko w .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="94bd0-104">The [Constrained execution regions (CER)](../../../framework/performance/constrained-execution-regions.md) feature is supported only in .NET Framework.</span></span> <span data-ttu-id="94bd0-105">W związku z tym różne interfejsy API związane z programem CER są oznaczane jako przestarzałe, począwszy od platformy .NET 5,0.</span><span class="sxs-lookup"><span data-stu-id="94bd0-105">As such, various CER-related APIs are marked obsolete, starting in .NET 5.0.</span></span> <span data-ttu-id="94bd0-106">Użycie tych interfejsów API generuje ostrzeżenie `SYSLIB0004` w czasie kompilacji.</span><span class="sxs-lookup"><span data-stu-id="94bd0-106">Using these APIs generates warning `SYSLIB0004` at compile time.</span></span>

<span data-ttu-id="94bd0-107">Następujące interfejsy API związane z programem CER są przestarzałe:</span><span class="sxs-lookup"><span data-stu-id="94bd0-107">The following CER-related APIs are obsolete:</span></span>

- <xref:System.Runtime.CompilerServices.RuntimeHelpers.ExecuteCodeWithGuaranteedCleanup(System.Runtime.CompilerServices.RuntimeHelpers.TryCode,System.Runtime.CompilerServices.RuntimeHelpers.CleanupCode,System.Object)?displayProperty=nameWithType>
- <xref:System.Runtime.CompilerServices.RuntimeHelpers.PrepareConstrainedRegions?displayProperty=nameWithType>
- <xref:System.Runtime.CompilerServices.RuntimeHelpers.PrepareConstrainedRegionsNoOP?displayProperty=nameWithType>
- <xref:System.Runtime.CompilerServices.RuntimeHelpers.PrepareContractedDelegate(System.Delegate)?displayProperty=nameWithType>
- <xref:System.Runtime.CompilerServices.RuntimeHelpers.ProbeForSufficientStack?displayProperty=nameWithType>
- <xref:System.Runtime.ConstrainedExecution.Cer?displayProperty=nameWithType>
- <xref:System.Runtime.ConstrainedExecution.Consistency?displayProperty=nameWithType>
- <xref:System.Runtime.ConstrainedExecution.PrePrepareMethodAttribute?displayProperty=nameWithType>
- <xref:System.Runtime.ConstrainedExecution.ReliabilityContractAttribute?displayProperty=nameWithType>

## <a name="workarounds"></a><span data-ttu-id="94bd0-108">Obejścia</span><span class="sxs-lookup"><span data-stu-id="94bd0-108">Workarounds</span></span>

- <span data-ttu-id="94bd0-109">Jeśli zastosowano atrybut CER do metody, Usuń atrybut.</span><span class="sxs-lookup"><span data-stu-id="94bd0-109">If you have applied a CER attribute to a method, remove the attribute.</span></span> <span data-ttu-id="94bd0-110">Te atrybuty nie mają wpływu na program .NET 5,0 i jego nowsze wersje.</span><span class="sxs-lookup"><span data-stu-id="94bd0-110">These attributes have no effect in .NET 5.0 and later versions.</span></span>

  ```csharp
  // REMOVE the attribute below.
  [ReliabilityContract(Consistency.WillNotCorruptState, Cer.Success)]
  public void DoSomething()
  {
  }

  // REMOVE the attribute below.
  [PrePrepareMethod]
  public void DoSomething()
  {
  }
  ```

- <span data-ttu-id="94bd0-111">Jeśli wywołujesz `RuntimeHelpers.ProbeForSufficientStack` lub `RuntimeHelpers.PrepareContractedDelegate` , Usuń wywołanie.</span><span class="sxs-lookup"><span data-stu-id="94bd0-111">If you are calling `RuntimeHelpers.ProbeForSufficientStack` or `RuntimeHelpers.PrepareContractedDelegate`, remove the call.</span></span> <span data-ttu-id="94bd0-112">Te wywołania nie działają w programie .NET 5,0 i jego nowszych wersjach.</span><span class="sxs-lookup"><span data-stu-id="94bd0-112">These calls have no effect in .NET 5.0 and later versions.</span></span>

  ```csharp
  public void DoSomething()
  {
      // REMOVE the call below.
      RuntimeHelpers.ProbeForSufficientStack();

      // (Remainder of your method logic here.)
  }
  ```

- <span data-ttu-id="94bd0-113">Jeśli wywołujesz `RuntimeHelpers.PrepareConstrainedRegions` , Usuń wywołanie.</span><span class="sxs-lookup"><span data-stu-id="94bd0-113">If you are calling `RuntimeHelpers.PrepareConstrainedRegions`, remove the call.</span></span> <span data-ttu-id="94bd0-114">To wywołanie nie działa w programie .NET 5,0 i jego nowszych wersjach.</span><span class="sxs-lookup"><span data-stu-id="94bd0-114">This call has no effect in .NET 5.0 and later versions.</span></span>

  ```csharp
  public void DoSomething_Old()
  {
      // REMOVE the call below.
      RuntimeHelpers.PrepareConstrainedRegions();
      try
      {
          // try code
      }
      finally
      {
          // cleanup code
      }
  }

  public void DoSomething_Corrected()
  {
      // There is no call to PrepareConstrainedRegions. It's a normal try / finally block.

      try
      {
          // try code
      }
      finally
      {
          // cleanup code
      }
  }
  ```

- <span data-ttu-id="94bd0-115">Jeśli wywołujesz `RuntimeHelpers.ExecuteCodeWithGuaranteedCleanup` , Zastąp wywołanie przy użyciu standardowego bloku _try/catch/finally_ .</span><span class="sxs-lookup"><span data-stu-id="94bd0-115">If you are calling `RuntimeHelpers.ExecuteCodeWithGuaranteedCleanup`, replace the call with a standard _try / catch / finally_ block.</span></span>

  ```csharp
  // The sample below produces warning SYSLIB0004.
  public void DoSomething_Old()
  {
      RuntimeHelpers.ExecuteCodeWithGuaranteedCleanup(MyTryCode, MyCleanupCode, null);
  }
  public void MyTryCode(object state) { /* try code */ }
  public void MyCleanupCode(object state, bool exceptionThrown) { /* cleanup code */ }

  // The corrected sample below does not produce warning SYSLIB0004.
  public void DoSomething_Corrected()
  {
      try
      {
          // try code
      }
      catch (Exception ex)
      {
          // exception handling code
      }
      finally
      {
          // cleanup code
      }
  }
  ```

[!INCLUDE [suppress-syslib-warning](../../../../includes/suppress-syslib-warning.md)]

## <a name="see-also"></a><span data-ttu-id="94bd0-116">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="94bd0-116">See also</span></span>

- [<span data-ttu-id="94bd0-117">Ograniczone regiony wykonywania</span><span class="sxs-lookup"><span data-stu-id="94bd0-117">Constrained execution regions</span></span>](../../../framework/performance/constrained-execution-regions.md)
