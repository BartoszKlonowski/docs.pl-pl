---
title: Nieobsługiwane interfejsy API w oprogramowaniu .NET Core i .NET 5 +
titleSuffix: ''
description: Dowiedz się, które interfejsy API platformy .NET zawsze zgłaszają wyjątek w oprogramowaniu .NET Core i .NET 5,0 i nowszych wersjach.
ms.date: 10/13/2020
ms.openlocfilehash: 1bd41192d0d6752d2b659da9fb6387dac321b2c3
ms.sourcegitcommit: e301979e3049ce412d19b094c60ed95b316a8f8c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/16/2020
ms.locfileid: "97593269"
---
# <a name="apis-that-always-throw-exceptions-on-net-core-and-net-5"></a><span data-ttu-id="4c3a6-103">Interfejsy API, które zawsze generują wyjątki w oprogramowaniu .NET Core i .NET 5 +</span><span class="sxs-lookup"><span data-stu-id="4c3a6-103">APIs that always throw exceptions on .NET Core and .NET 5+</span></span>

<span data-ttu-id="4c3a6-104">Następujące interfejsy API zawsze będą zgłaszać <xref:System.PlatformNotSupportedException> na platformie .net 5,0 i nowszych wersjach (łącznie ze wszystkimi wersjami programu .NET Core) na wszystkich lub podzestawach platform.</span><span class="sxs-lookup"><span data-stu-id="4c3a6-104">The following APIs will always throw a <xref:System.PlatformNotSupportedException> on .NET 5.0 and later versions (including all versions of .NET Core) on all or a subset of platforms.</span></span>

<span data-ttu-id="4c3a6-105">Ten artykuł organizuje interfejsy API, których to dotyczy, według przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="4c3a6-105">This article organizes the affected APIs by namespace.</span></span>

> [!NOTE]
>
> - <span data-ttu-id="4c3a6-106">Ten artykuł jest pracą w toku.</span><span class="sxs-lookup"><span data-stu-id="4c3a6-106">This article is a work-in-progress.</span></span> <span data-ttu-id="4c3a6-107">Nie jest to kompletna lista interfejsów API, które generują wyjątki w programie .NET 5 lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="4c3a6-107">It is not a complete list of APIs that throw exceptions on .NET 5+.</span></span>
> - <span data-ttu-id="4c3a6-108">Ten artykuł nie zawiera jawnych implementacji interfejsu dla serializacji binarnej, która jest zgłaszana w programie .NET 5 lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="4c3a6-108">This article does not include the explicit interface implementations for binary serialization that throw on .NET 5+.</span></span> <span data-ttu-id="4c3a6-109">Aby uzyskać więcej informacji, zobacz [Serializacja binarna w programie .NET Core](../../standard/serialization/binary-serialization.md#net-core).</span><span class="sxs-lookup"><span data-stu-id="4c3a6-109">For more information, see [Binary serialization in .NET Core](../../standard/serialization/binary-serialization.md#net-core).</span></span>

## <a name="system"></a><span data-ttu-id="4c3a6-110">System</span><span class="sxs-lookup"><span data-stu-id="4c3a6-110">System</span></span>

| <span data-ttu-id="4c3a6-111">Członek</span><span class="sxs-lookup"><span data-stu-id="4c3a6-111">Member</span></span> | <span data-ttu-id="4c3a6-112">Platformy, które generują</span><span class="sxs-lookup"><span data-stu-id="4c3a6-112">Platforms that throw</span></span> |
| - | - |
| <xref:System.AppDomain.CreateDomain%2A?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-113">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-113">All</span></span> |
| <xref:System.AppDomain.ExecuteAssembly(System.String,System.String[],System.Byte[],System.Configuration.Assemblies.AssemblyHashAlgorithm)?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-114">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-114">All</span></span> |
| <xref:System.Console.CapsLock?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-115">Linux i macOS</span><span class="sxs-lookup"><span data-stu-id="4c3a6-115">Linux and macOS</span></span> |
| <xref:System.Console.NumberLock?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-116">Linux i macOS</span><span class="sxs-lookup"><span data-stu-id="4c3a6-116">Linux and macOS</span></span> |
| <xref:System.Delegate.GetObjectData(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-117">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-117">All</span></span> |
| <xref:System.Exception.SerializeObjectState?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-118">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-118">All</span></span> |
| <xref:System.MarshalByRefObject.GetLifetimeService?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-119">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-119">All</span></span> |
| <xref:System.MarshalByRefObject.InitializeLifetimeService?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-120">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-120">All</span></span> |
| <xref:System.OperatingSystem.GetObjectData(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-121">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-121">All</span></span> |
| <xref:System.Type.ReflectionOnlyGetType(System.String,System.Boolean,System.Boolean)?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-122">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-122">All</span></span> |

## <a name="systemcodedomcompiler"></a><span data-ttu-id="4c3a6-123">System. CodeDom. Compiler</span><span class="sxs-lookup"><span data-stu-id="4c3a6-123">System.CodeDom.Compiler</span></span>

| <span data-ttu-id="4c3a6-124">Członek</span><span class="sxs-lookup"><span data-stu-id="4c3a6-124">Member</span></span> | <span data-ttu-id="4c3a6-125">Platformy, które generują</span><span class="sxs-lookup"><span data-stu-id="4c3a6-125">Platforms that throw</span></span> |
| - | - |
| <xref:System.CodeDom.Compiler.CodeDomProvider.CompileAssemblyFromDom%2A?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-126">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-126">All</span></span> |
| <xref:System.CodeDom.Compiler.CodeDomProvider.CompileAssemblyFromFile%2A?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-127">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-127">All</span></span> |
| <xref:System.CodeDom.Compiler.CodeDomProvider.CompileAssemblyFromSource%2A?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-128">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-128">All</span></span> |

## <a name="systemcollectionsspecialized"></a><span data-ttu-id="4c3a6-129">System. Collections. specjalizowane</span><span class="sxs-lookup"><span data-stu-id="4c3a6-129">System.Collections.Specialized</span></span>

| <span data-ttu-id="4c3a6-130">Członek</span><span class="sxs-lookup"><span data-stu-id="4c3a6-130">Member</span></span> | <span data-ttu-id="4c3a6-131">Platformy, które generują</span><span class="sxs-lookup"><span data-stu-id="4c3a6-131">Platforms that throw</span></span> |
| - | - |
| <xref:System.Collections.Specialized.NameObjectCollectionBase.%23ctor(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)> | <span data-ttu-id="4c3a6-132">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-132">All</span></span> |
| <xref:System.Collections.Specialized.NameObjectCollectionBase.GetObjectData(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-133">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-133">All</span></span> |
| <xref:System.Collections.Specialized.NameObjectCollectionBase.OnDeserialization(System.Object)?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-134">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-134">All</span></span> |

## <a name="systemconfiguration"></a><span data-ttu-id="4c3a6-135">System.Configwersja</span><span class="sxs-lookup"><span data-stu-id="4c3a6-135">System.Configuration</span></span>

| <span data-ttu-id="4c3a6-136">Członek</span><span class="sxs-lookup"><span data-stu-id="4c3a6-136">Member</span></span> | <span data-ttu-id="4c3a6-137">Platformy, które generują</span><span class="sxs-lookup"><span data-stu-id="4c3a6-137">Platforms that throw</span></span> |
| - | - |
| <span data-ttu-id="4c3a6-138"><xref:System.Configuration.RsaProtectedConfigurationProvider?displayProperty=nameWithType> (wszystkie elementy członkowskie)</span><span class="sxs-lookup"><span data-stu-id="4c3a6-138"><xref:System.Configuration.RsaProtectedConfigurationProvider?displayProperty=nameWithType> (all members)</span></span> | <span data-ttu-id="4c3a6-139">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-139">All</span></span> |

## <a name="systemconsole"></a><span data-ttu-id="4c3a6-140">System.Console</span><span class="sxs-lookup"><span data-stu-id="4c3a6-140">System.Console</span></span>

| <span data-ttu-id="4c3a6-141">Członek</span><span class="sxs-lookup"><span data-stu-id="4c3a6-141">Member</span></span> | <span data-ttu-id="4c3a6-142">Platformy, które generują</span><span class="sxs-lookup"><span data-stu-id="4c3a6-142">Platforms that throw</span></span> |
| - | - |
| <xref:System.Console.Beep?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-143">Linux i macOS</span><span class="sxs-lookup"><span data-stu-id="4c3a6-143">Linux and macOS</span></span> |
| <span data-ttu-id="4c3a6-144"><xref:System.Console.BufferHeight?displayProperty=nameWithType> (tylko ustaw)</span><span class="sxs-lookup"><span data-stu-id="4c3a6-144"><xref:System.Console.BufferHeight?displayProperty=nameWithType> (set only)</span></span> | <span data-ttu-id="4c3a6-145">Linux i macOS</span><span class="sxs-lookup"><span data-stu-id="4c3a6-145">Linux and macOS</span></span> |
| <span data-ttu-id="4c3a6-146"><xref:System.Console.BufferWidth?displayProperty=nameWithType> (tylko ustaw)</span><span class="sxs-lookup"><span data-stu-id="4c3a6-146"><xref:System.Console.BufferWidth?displayProperty=nameWithType> (set only)</span></span> | <span data-ttu-id="4c3a6-147">Linux i macOS</span><span class="sxs-lookup"><span data-stu-id="4c3a6-147">Linux and macOS</span></span> |
| <span data-ttu-id="4c3a6-148"><xref:System.Console.CursorSize?displayProperty=nameWithType> (tylko ustaw)</span><span class="sxs-lookup"><span data-stu-id="4c3a6-148"><xref:System.Console.CursorSize?displayProperty=nameWithType> (set only)</span></span> | <span data-ttu-id="4c3a6-149">Linux i macOS</span><span class="sxs-lookup"><span data-stu-id="4c3a6-149">Linux and macOS</span></span> |
| <span data-ttu-id="4c3a6-150"><xref:System.Console.CursorVisible?displayProperty=nameWithType> (tylko pobieranie)</span><span class="sxs-lookup"><span data-stu-id="4c3a6-150"><xref:System.Console.CursorVisible?displayProperty=nameWithType> (get only)</span></span> | <span data-ttu-id="4c3a6-151">Linux i macOS</span><span class="sxs-lookup"><span data-stu-id="4c3a6-151">Linux and macOS</span></span> |
| <xref:System.Console.MoveBufferArea%2A?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-152">Linux i macOS</span><span class="sxs-lookup"><span data-stu-id="4c3a6-152">Linux and macOS</span></span> |
| <xref:System.Console.SetWindowPosition%2A?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-153">Linux i macOS</span><span class="sxs-lookup"><span data-stu-id="4c3a6-153">Linux and macOS</span></span> |
| <xref:System.Console.SetWindowSize%2A?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-154">Linux i macOS</span><span class="sxs-lookup"><span data-stu-id="4c3a6-154">Linux and macOS</span></span> |
| <span data-ttu-id="4c3a6-155"><xref:System.Console.Title?displayProperty=nameWithType> (tylko pobieranie)</span><span class="sxs-lookup"><span data-stu-id="4c3a6-155"><xref:System.Console.Title?displayProperty=nameWithType> (get only)</span></span> | <span data-ttu-id="4c3a6-156">Linux i macOS</span><span class="sxs-lookup"><span data-stu-id="4c3a6-156">Linux and macOS</span></span> |
| <span data-ttu-id="4c3a6-157"><xref:System.Console.WindowHeight?displayProperty=nameWithType> (tylko ustaw)</span><span class="sxs-lookup"><span data-stu-id="4c3a6-157"><xref:System.Console.WindowHeight?displayProperty=nameWithType> (set only)</span></span> | <span data-ttu-id="4c3a6-158">Linux i macOS</span><span class="sxs-lookup"><span data-stu-id="4c3a6-158">Linux and macOS</span></span> |
| <span data-ttu-id="4c3a6-159"><xref:System.Console.WindowLeft?displayProperty=nameWithType> (tylko ustaw)</span><span class="sxs-lookup"><span data-stu-id="4c3a6-159"><xref:System.Console.WindowLeft?displayProperty=nameWithType> (set only)</span></span> | <span data-ttu-id="4c3a6-160">Linux i macOS</span><span class="sxs-lookup"><span data-stu-id="4c3a6-160">Linux and macOS</span></span> |
| <span data-ttu-id="4c3a6-161"><xref:System.Console.WindowTop?displayProperty=nameWithType> (tylko ustaw)</span><span class="sxs-lookup"><span data-stu-id="4c3a6-161"><xref:System.Console.WindowTop?displayProperty=nameWithType> (set only)</span></span> | <span data-ttu-id="4c3a6-162">Linux i macOS</span><span class="sxs-lookup"><span data-stu-id="4c3a6-162">Linux and macOS</span></span> |
| <span data-ttu-id="4c3a6-163"><xref:System.Console.WindowWidth?displayProperty=nameWithType> (tylko ustaw)</span><span class="sxs-lookup"><span data-stu-id="4c3a6-163"><xref:System.Console.WindowWidth?displayProperty=nameWithType> (set only)</span></span> | <span data-ttu-id="4c3a6-164">Linux i macOS</span><span class="sxs-lookup"><span data-stu-id="4c3a6-164">Linux and macOS</span></span> |

## <a name="systemdatacommon"></a><span data-ttu-id="4c3a6-165">System. Data. Common</span><span class="sxs-lookup"><span data-stu-id="4c3a6-165">System.Data.Common</span></span>

| <span data-ttu-id="4c3a6-166">Członek</span><span class="sxs-lookup"><span data-stu-id="4c3a6-166">Member</span></span> | <span data-ttu-id="4c3a6-167">Platformy, które generują</span><span class="sxs-lookup"><span data-stu-id="4c3a6-167">Platforms that throw</span></span> |
| - | - |
| <span data-ttu-id="4c3a6-168"><xref:System.Data.Common.DbDataReader.GetSchemaTable%2A?displayProperty=nameWithType> (zgłasza <xref:System.NotSupportedException> )</span><span class="sxs-lookup"><span data-stu-id="4c3a6-168"><xref:System.Data.Common.DbDataReader.GetSchemaTable%2A?displayProperty=nameWithType> (throws <xref:System.NotSupportedException>)</span></span> | <span data-ttu-id="4c3a6-169">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-169">All</span></span> |

## <a name="systemdiagnosticsprocess"></a><span data-ttu-id="4c3a6-170">System. Diagnostics. Process</span><span class="sxs-lookup"><span data-stu-id="4c3a6-170">System.Diagnostics.Process</span></span>

| <span data-ttu-id="4c3a6-171">Członek</span><span class="sxs-lookup"><span data-stu-id="4c3a6-171">Member</span></span> | <span data-ttu-id="4c3a6-172">Platformy, które generują</span><span class="sxs-lookup"><span data-stu-id="4c3a6-172">Platforms that throw</span></span> |
| - | - |
| <span data-ttu-id="4c3a6-173"><xref:System.Diagnostics.Process.MaxWorkingSet?displayProperty=nameWithType> (tylko ustaw)</span><span class="sxs-lookup"><span data-stu-id="4c3a6-173"><xref:System.Diagnostics.Process.MaxWorkingSet?displayProperty=nameWithType> (set only)</span></span> | <span data-ttu-id="4c3a6-174">Linux</span><span class="sxs-lookup"><span data-stu-id="4c3a6-174">Linux</span></span> |
| <span data-ttu-id="4c3a6-175"><xref:System.Diagnostics.Process.MinWorkingSet?displayProperty=nameWithType> (tylko ustaw)</span><span class="sxs-lookup"><span data-stu-id="4c3a6-175"><xref:System.Diagnostics.Process.MinWorkingSet?displayProperty=nameWithType> (set only)</span></span> | <span data-ttu-id="4c3a6-176">Linux</span><span class="sxs-lookup"><span data-stu-id="4c3a6-176">Linux</span></span> |
| <xref:System.Diagnostics.Process.ProcessorAffinity?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-177">macOS</span><span class="sxs-lookup"><span data-stu-id="4c3a6-177">macOS</span></span> |
| <xref:System.Diagnostics.Process.MainWindowHandle?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-178">Linux i macOS</span><span class="sxs-lookup"><span data-stu-id="4c3a6-178">Linux and macOS</span></span> |
| <xref:System.Diagnostics.Process.Start(System.String,System.String,System.String,System.Security.SecureString,System.String)?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-179">Linux i macOS</span><span class="sxs-lookup"><span data-stu-id="4c3a6-179">Linux and macOS</span></span> |
| <xref:System.Diagnostics.Process.Start(System.String,System.String,System.Security.SecureString,System.String)?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-180">Linux i macOS</span><span class="sxs-lookup"><span data-stu-id="4c3a6-180">Linux and macOS</span></span> |
| <xref:System.Diagnostics.ProcessStartInfo.UserName?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-181">Linux i macOS</span><span class="sxs-lookup"><span data-stu-id="4c3a6-181">Linux and macOS</span></span> |
| <xref:System.Diagnostics.ProcessStartInfo.PasswordInClearText?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-182">Linux i macOS</span><span class="sxs-lookup"><span data-stu-id="4c3a6-182">Linux and macOS</span></span> |
| <xref:System.Diagnostics.ProcessStartInfo.Domain?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-183">Linux i macOS</span><span class="sxs-lookup"><span data-stu-id="4c3a6-183">Linux and macOS</span></span> |
| <xref:System.Diagnostics.ProcessStartInfo.LoadUserProfile?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-184">Linux i macOS</span><span class="sxs-lookup"><span data-stu-id="4c3a6-184">Linux and macOS</span></span> |
| <span data-ttu-id="4c3a6-185"><xref:System.Diagnostics.ProcessThread.BasePriority?displayProperty=nameWithType> (tylko ustaw)</span><span class="sxs-lookup"><span data-stu-id="4c3a6-185"><xref:System.Diagnostics.ProcessThread.BasePriority?displayProperty=nameWithType> (set only)</span></span> | <span data-ttu-id="4c3a6-186">Linux i macOS</span><span class="sxs-lookup"><span data-stu-id="4c3a6-186">Linux and macOS</span></span> |
| <span data-ttu-id="4c3a6-187"><xref:System.Diagnostics.ProcessThread.BasePriority?displayProperty=nameWithType> (tylko pobieranie)</span><span class="sxs-lookup"><span data-stu-id="4c3a6-187"><xref:System.Diagnostics.ProcessThread.BasePriority?displayProperty=nameWithType> (get only)</span></span> | <span data-ttu-id="4c3a6-188">macOS</span><span class="sxs-lookup"><span data-stu-id="4c3a6-188">macOS</span></span> |
| <span data-ttu-id="4c3a6-189"><xref:System.Diagnostics.ProcessThread.ProcessorAffinity?displayProperty=nameWithType> (tylko ustaw)</span><span class="sxs-lookup"><span data-stu-id="4c3a6-189"><xref:System.Diagnostics.ProcessThread.ProcessorAffinity?displayProperty=nameWithType> (set only)</span></span> | <span data-ttu-id="4c3a6-190">Linux i macOS</span><span class="sxs-lookup"><span data-stu-id="4c3a6-190">Linux and macOS</span></span> |

## <a name="systemio"></a><span data-ttu-id="4c3a6-191">System.IO</span><span class="sxs-lookup"><span data-stu-id="4c3a6-191">System.IO</span></span>

| <span data-ttu-id="4c3a6-192">Członek</span><span class="sxs-lookup"><span data-stu-id="4c3a6-192">Member</span></span> | <span data-ttu-id="4c3a6-193">Platformy, które generują</span><span class="sxs-lookup"><span data-stu-id="4c3a6-193">Platforms that throw</span></span> |
| - | - |
| <xref:System.IO.FileSystemInfo.%23ctor(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)> | <span data-ttu-id="4c3a6-194">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-194">All</span></span> |
| <xref:System.IO.FileSystemInfo.GetObjectData(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-195">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-195">All</span></span> |

## <a name="systemiopipes"></a><span data-ttu-id="4c3a6-196">System. IO. Pipes</span><span class="sxs-lookup"><span data-stu-id="4c3a6-196">System.IO.Pipes</span></span>

| <span data-ttu-id="4c3a6-197">Członek</span><span class="sxs-lookup"><span data-stu-id="4c3a6-197">Member</span></span> | <span data-ttu-id="4c3a6-198">Platformy, które generują</span><span class="sxs-lookup"><span data-stu-id="4c3a6-198">Platforms that throw</span></span> |
| - | - |
| <xref:System.IO.Pipes.NamedPipeClientStream.NumberOfServerInstances?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-199">Linux i macOS</span><span class="sxs-lookup"><span data-stu-id="4c3a6-199">Linux and macOS</span></span> |
| <xref:System.IO.Pipes.NamedPipeServerStream.GetImpersonationUserName?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-200">Linux i macOS</span><span class="sxs-lookup"><span data-stu-id="4c3a6-200">Linux and macOS</span></span> |
| <xref:System.IO.Pipes.PipeStream.InBufferSize?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-201">Linux i macOS</span><span class="sxs-lookup"><span data-stu-id="4c3a6-201">Linux and macOS</span></span> |
| <xref:System.IO.Pipes.PipeStream.OutBufferSize?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-202">Linux i macOS</span><span class="sxs-lookup"><span data-stu-id="4c3a6-202">Linux and macOS</span></span> |
| <span data-ttu-id="4c3a6-203"><xref:System.IO.Pipes.PipeStream.ReadMode?displayProperty=nameWithType> (tylko ustaw)</span><span class="sxs-lookup"><span data-stu-id="4c3a6-203"><xref:System.IO.Pipes.PipeStream.ReadMode?displayProperty=nameWithType> (set only)</span></span> | <span data-ttu-id="4c3a6-204">Linux i macOS</span><span class="sxs-lookup"><span data-stu-id="4c3a6-204">Linux and macOS</span></span> |
| <xref:System.IO.Pipes.PipeStream.WaitForPipeDrain?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-205">Linux i macOS</span><span class="sxs-lookup"><span data-stu-id="4c3a6-205">Linux and macOS</span></span> |

## <a name="systemmedia"></a><span data-ttu-id="4c3a6-206">System. Media</span><span class="sxs-lookup"><span data-stu-id="4c3a6-206">System.Media</span></span>

| <span data-ttu-id="4c3a6-207">Członek</span><span class="sxs-lookup"><span data-stu-id="4c3a6-207">Member</span></span> | <span data-ttu-id="4c3a6-208">Platformy, które generują</span><span class="sxs-lookup"><span data-stu-id="4c3a6-208">Platforms that throw</span></span> |
| - | - |
| <xref:System.Media.SoundPlayer.%23ctor(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)> | <span data-ttu-id="4c3a6-209">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-209">All</span></span> |

## <a name="systemnet"></a><span data-ttu-id="4c3a6-210">System.Net</span><span class="sxs-lookup"><span data-stu-id="4c3a6-210">System.Net</span></span>

| <span data-ttu-id="4c3a6-211">Członek</span><span class="sxs-lookup"><span data-stu-id="4c3a6-211">Member</span></span> | <span data-ttu-id="4c3a6-212">Platformy, które generują</span><span class="sxs-lookup"><span data-stu-id="4c3a6-212">Platforms that throw</span></span> |
| - | - |
| <xref:System.Net.AuthenticationManager.Authenticate(System.String,System.Net.WebRequest,System.Net.ICredentials)?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-213">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-213">All</span></span> |
| <xref:System.Net.AuthenticationManager.PreAuthenticate(System.Net.WebRequest,System.Net.ICredentials)?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-214">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-214">All</span></span> |
| <xref:System.Net.FileWebRequest.%23ctor(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)> | <span data-ttu-id="4c3a6-215">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-215">All</span></span> |
| <xref:System.Net.FileWebRequest.GetObjectData(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-216">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-216">All</span></span> |
| <xref:System.Net.FileWebResponse.%23ctor(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)> | <span data-ttu-id="4c3a6-217">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-217">All</span></span> |
| <xref:System.Net.FileWebResponse.GetObjectData(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-218">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-218">All</span></span> |
| <xref:System.Net.HttpWebRequest.%23ctor(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)> | <span data-ttu-id="4c3a6-219">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-219">All</span></span> |
| <xref:System.Net.HttpWebRequest.GetObjectData(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-220">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-220">All</span></span> |
| <xref:System.Net.HttpWebResponse.%23ctor(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)> | <span data-ttu-id="4c3a6-221">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-221">All</span></span> |
| <xref:System.Net.HttpWebResponse.GetObjectData(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-222">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-222">All</span></span> |
| <xref:System.Net.WebProxy.%23ctor(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)> | <span data-ttu-id="4c3a6-223">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-223">All</span></span> |
| <xref:System.Net.WebProxy.GetDefaultProxy?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-224">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-224">All</span></span> |
| <xref:System.Net.WebProxy.GetObjectData%2A?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-225">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-225">All</span></span> |
| <xref:System.Net.WebRequest.%23ctor(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)> | <span data-ttu-id="4c3a6-226">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-226">All</span></span> |
| <xref:System.Net.WebRequest.GetObjectData(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-227">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-227">All</span></span> |
| <xref:System.Net.WebResponse.%23ctor(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)> | <span data-ttu-id="4c3a6-228">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-228">All</span></span> |
| <xref:System.Net.WebResponse.GetObjectData(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-229">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-229">All</span></span> |

## <a name="systemnetnetworkinformation"></a><span data-ttu-id="4c3a6-230">System .NET. NetworkInformation</span><span class="sxs-lookup"><span data-stu-id="4c3a6-230">System.Net.NetworkInformation</span></span>

| <span data-ttu-id="4c3a6-231">Członek</span><span class="sxs-lookup"><span data-stu-id="4c3a6-231">Member</span></span> | <span data-ttu-id="4c3a6-232">Platformy, które generują</span><span class="sxs-lookup"><span data-stu-id="4c3a6-232">Platforms that throw</span></span> |
| - | - |
| <xref:System.Net.NetworkInformation.Ping.Send%2A?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-233">Windows (platformy UWP)</span><span class="sxs-lookup"><span data-stu-id="4c3a6-233">Windows (UWP)</span></span> |

## <a name="systemnetsockets"></a><span data-ttu-id="4c3a6-234">System .NET. Sockets</span><span class="sxs-lookup"><span data-stu-id="4c3a6-234">System.Net.Sockets</span></span>

| <span data-ttu-id="4c3a6-235">Członek</span><span class="sxs-lookup"><span data-stu-id="4c3a6-235">Member</span></span> | <span data-ttu-id="4c3a6-236">Platformy, które generują</span><span class="sxs-lookup"><span data-stu-id="4c3a6-236">Platforms that throw</span></span> |
| - | - |
| <xref:System.Net.Sockets.Socket.%23ctor(System.Net.Sockets.SocketInformation)> | <span data-ttu-id="4c3a6-237">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-237">All</span></span> |
| <xref:System.Net.Sockets.Socket.DuplicateAndClose(System.Int32)?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-238">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-238">All</span></span> |

## <a name="systemnetwebsockets"></a><span data-ttu-id="4c3a6-239">System .NET. WebSockets</span><span class="sxs-lookup"><span data-stu-id="4c3a6-239">System.Net.WebSockets</span></span>

| <span data-ttu-id="4c3a6-240">Członek</span><span class="sxs-lookup"><span data-stu-id="4c3a6-240">Member</span></span> | <span data-ttu-id="4c3a6-241">Platformy, które generują</span><span class="sxs-lookup"><span data-stu-id="4c3a6-241">Platforms that throw</span></span> |
| - | - |
| <xref:System.Net.WebSockets.WebSocket.RegisterPrefixes?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-242">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-242">All</span></span> |

## <a name="systemreflection"></a><span data-ttu-id="4c3a6-243">System. odbicie</span><span class="sxs-lookup"><span data-stu-id="4c3a6-243">System.Reflection</span></span>

| <span data-ttu-id="4c3a6-244">Członek</span><span class="sxs-lookup"><span data-stu-id="4c3a6-244">Member</span></span> | <span data-ttu-id="4c3a6-245">Platformy, które generują</span><span class="sxs-lookup"><span data-stu-id="4c3a6-245">Platforms that throw</span></span> |
| - | - |
| <xref:System.Reflection.Assembly.ReflectionOnlyLoad%2A?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-246">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-246">All</span></span> |
| <xref:System.Reflection.Assembly.ReflectionOnlyLoadFrom(System.String)?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-247">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-247">All</span></span> |
| <xref:System.Reflection.AssemblyName.GetObjectData(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-248">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-248">All</span></span> |
| <xref:System.Reflection.AssemblyName.OnDeserialization(System.Object)?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-249">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-249">All</span></span> |
| <xref:System.Reflection.StrongNameKeyPair.%23ctor(System.String)> | <span data-ttu-id="4c3a6-250">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-250">All</span></span> |
| <xref:System.Reflection.StrongNameKeyPair.%23ctor(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)> | <span data-ttu-id="4c3a6-251">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-251">All</span></span> |
| <xref:System.Reflection.StrongNameKeyPair.PublicKey?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-252">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-252">All</span></span> |

## <a name="systemruntimecompilerservices"></a><span data-ttu-id="4c3a6-253">System. Runtime. CompilerServices</span><span class="sxs-lookup"><span data-stu-id="4c3a6-253">System.Runtime.CompilerServices</span></span>

| <span data-ttu-id="4c3a6-254">Członek</span><span class="sxs-lookup"><span data-stu-id="4c3a6-254">Member</span></span> | <span data-ttu-id="4c3a6-255">Platformy, które generują</span><span class="sxs-lookup"><span data-stu-id="4c3a6-255">Platforms that throw</span></span> |
| - | - |
| <xref:System.Runtime.CompilerServices.DebugInfoGenerator.CreatePdbGenerator?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-256">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-256">All</span></span> |

## <a name="systemruntimeinteropservices"></a><span data-ttu-id="4c3a6-257">System. Runtime. InteropServices</span><span class="sxs-lookup"><span data-stu-id="4c3a6-257">System.Runtime.InteropServices</span></span>

| <span data-ttu-id="4c3a6-258">Członek</span><span class="sxs-lookup"><span data-stu-id="4c3a6-258">Member</span></span> | <span data-ttu-id="4c3a6-259">Platformy, które generują</span><span class="sxs-lookup"><span data-stu-id="4c3a6-259">Platforms that throw</span></span> |
| - | - |
| <xref:System.Runtime.InteropServices.Marshal.GetIDispatchForObject(System.Object)?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-260">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-260">All</span></span> |
| <xref:System.Runtime.InteropServices.RuntimeEnvironment.SystemConfigurationFile?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-261">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-261">All</span></span> |
| <xref:System.Runtime.InteropServices.RuntimeEnvironment.GetRuntimeInterfaceAsIntPtr(System.Guid,System.Guid)?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-262">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-262">All</span></span> |
| <xref:System.Runtime.InteropServices.RuntimeEnvironment.GetRuntimeInterfaceAsObject(System.Guid,System.Guid)?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-263">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-263">All</span></span> |
| <xref:System.Runtime.InteropServices.WindowsRuntime.WindowsRuntimeMarshal.StringToHString(System.String)?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-264">Linux i macOS</span><span class="sxs-lookup"><span data-stu-id="4c3a6-264">Linux and macOS</span></span> |
| <xref:System.Runtime.InteropServices.WindowsRuntime.WindowsRuntimeMarshal.PtrToStringHString(System.IntPtr)?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-265">Linux i macOS</span><span class="sxs-lookup"><span data-stu-id="4c3a6-265">Linux and macOS</span></span> |
| <xref:System.Runtime.InteropServices.WindowsRuntime.WindowsRuntimeMarshal.FreeHString(System.IntPtr)?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-266">Linux i macOS</span><span class="sxs-lookup"><span data-stu-id="4c3a6-266">Linux and macOS</span></span> |

## <a name="systemruntimeserialization"></a><span data-ttu-id="4c3a6-267">System.Runtime.Serialization</span><span class="sxs-lookup"><span data-stu-id="4c3a6-267">System.Runtime.Serialization</span></span>

| <span data-ttu-id="4c3a6-268">Członek</span><span class="sxs-lookup"><span data-stu-id="4c3a6-268">Member</span></span> | <span data-ttu-id="4c3a6-269">Platformy, które generują</span><span class="sxs-lookup"><span data-stu-id="4c3a6-269">Platforms that throw</span></span> |
| - | - |
| <xref:System.Runtime.Serialization.XsdDataContractExporter.Schemas?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-270">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-270">All</span></span> |

## <a name="systemsecurity"></a><span data-ttu-id="4c3a6-271">System. Security</span><span class="sxs-lookup"><span data-stu-id="4c3a6-271">System.Security</span></span>

| <span data-ttu-id="4c3a6-272">Członek</span><span class="sxs-lookup"><span data-stu-id="4c3a6-272">Member</span></span> | <span data-ttu-id="4c3a6-273">Platformy, które generują</span><span class="sxs-lookup"><span data-stu-id="4c3a6-273">Platforms that throw</span></span> |
| - | - |
| <xref:System.Security.CodeAccessPermission.Deny?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-274">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-274">All</span></span> |
| <xref:System.Security.CodeAccessPermission.PermitOnly?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-275">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-275">All</span></span> |
| <xref:System.Security.PermissionSet.ConvertPermissionSet(System.String,System.Byte[],System.String)?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-276">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-276">All</span></span> |
| <xref:System.Security.PermissionSet.Deny?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-277">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-277">All</span></span> |
| <xref:System.Security.PermissionSet.PermitOnly?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-278">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-278">All</span></span> |
| <xref:System.Security.SecurityContext.Capture?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-279">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-279">All</span></span> |
| <xref:System.Security.SecurityContext.CreateCopy?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-280">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-280">All</span></span> |
| <xref:System.Security.SecurityContext.Dispose?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-281">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-281">All</span></span> |
| <xref:System.Security.SecurityContext.IsFlowSuppressed?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-282">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-282">All</span></span> |
| <xref:System.Security.SecurityContext.IsWindowsIdentityFlowSuppressed?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-283">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-283">All</span></span> |
| <xref:System.Security.SecurityContext.RestoreFlow?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-284">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-284">All</span></span> |
| <xref:System.Security.SecurityContext.Run(System.Security.SecurityContext,System.Threading.ContextCallback,System.Object)?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-285">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-285">All</span></span> |
| <xref:System.Security.SecurityContext.SuppressFlow?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-286">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-286">All</span></span> |
| <xref:System.Security.SecurityContext.SuppressFlowWindowsIdentity?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-287">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-287">All</span></span> |

## <a name="systemsecurityclaims"></a><span data-ttu-id="4c3a6-288">System. Security. Claims</span><span class="sxs-lookup"><span data-stu-id="4c3a6-288">System.Security.Claims</span></span>

| <span data-ttu-id="4c3a6-289">Członek</span><span class="sxs-lookup"><span data-stu-id="4c3a6-289">Member</span></span> | <span data-ttu-id="4c3a6-290">Platformy, które generują</span><span class="sxs-lookup"><span data-stu-id="4c3a6-290">Platforms that throw</span></span> |
| - | - |
| <xref:System.Security.Claims.ClaimsPrincipal.%23ctor(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)> | <span data-ttu-id="4c3a6-291">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-291">All</span></span> |
| <xref:System.Security.Claims.ClaimsPrincipal.GetObjectData(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-292">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-292">All</span></span> |
| <xref:System.Security.Claims.ClaimsIdentity.%23ctor(System.Runtime.Serialization.SerializationInfo)> | <span data-ttu-id="4c3a6-293">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-293">All</span></span> |
| <xref:System.Security.Claims.ClaimsIdentity.%23ctor(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)> | <span data-ttu-id="4c3a6-294">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-294">All</span></span> |
| <xref:System.Security.Claims.ClaimsIdentity.GetObjectData(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-295">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-295">All</span></span> |

## <a name="systemsecuritycryptography"></a><span data-ttu-id="4c3a6-296">System. Security. Cryptography</span><span class="sxs-lookup"><span data-stu-id="4c3a6-296">System.Security.Cryptography</span></span>

| <span data-ttu-id="4c3a6-297">Członek</span><span class="sxs-lookup"><span data-stu-id="4c3a6-297">Member</span></span> | <span data-ttu-id="4c3a6-298">Platformy, które generują</span><span class="sxs-lookup"><span data-stu-id="4c3a6-298">Platforms that throw</span></span> |
| - | - |
| <xref:System.Security.Cryptography.AsymmetricAlgorithm.Create(System.String)?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-299">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-299">All</span></span> |
| <xref:System.Security.Cryptography.CspKeyContainerInfo.%23ctor%2A> | <span data-ttu-id="4c3a6-300">Linux i macOS</span><span class="sxs-lookup"><span data-stu-id="4c3a6-300">Linux and macOS</span></span> |
| <xref:System.Security.Cryptography.CspKeyContainerInfo.Accessible?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-301">Linux i macOS</span><span class="sxs-lookup"><span data-stu-id="4c3a6-301">Linux and macOS</span></span> |
| <xref:System.Security.Cryptography.CspKeyContainerInfo.Exportable?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-302">Linux i macOS</span><span class="sxs-lookup"><span data-stu-id="4c3a6-302">Linux and macOS</span></span> |
| <xref:System.Security.Cryptography.CspKeyContainerInfo.HardwareDevice?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-303">Linux i macOS</span><span class="sxs-lookup"><span data-stu-id="4c3a6-303">Linux and macOS</span></span> |
| <xref:System.Security.Cryptography.CspKeyContainerInfo.KeyContainerName?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-304">Linux i macOS</span><span class="sxs-lookup"><span data-stu-id="4c3a6-304">Linux and macOS</span></span> |
| <xref:System.Security.Cryptography.CspKeyContainerInfo.KeyNumber?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-305">Linux i macOS</span><span class="sxs-lookup"><span data-stu-id="4c3a6-305">Linux and macOS</span></span> |
| <xref:System.Security.Cryptography.CspKeyContainerInfo.MachineKeyStore?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-306">Linux i macOS</span><span class="sxs-lookup"><span data-stu-id="4c3a6-306">Linux and macOS</span></span> |
| <xref:System.Security.Cryptography.CspKeyContainerInfo.Protected?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-307">Linux i macOS</span><span class="sxs-lookup"><span data-stu-id="4c3a6-307">Linux and macOS</span></span> |
| <xref:System.Security.Cryptography.CspKeyContainerInfo.ProviderName?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-308">Linux i macOS</span><span class="sxs-lookup"><span data-stu-id="4c3a6-308">Linux and macOS</span></span> |
| <xref:System.Security.Cryptography.CspKeyContainerInfo.ProviderType?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-309">Linux i macOS</span><span class="sxs-lookup"><span data-stu-id="4c3a6-309">Linux and macOS</span></span> |
| <xref:System.Security.Cryptography.CspKeyContainerInfo.RandomlyGenerated?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-310">Linux i macOS</span><span class="sxs-lookup"><span data-stu-id="4c3a6-310">Linux and macOS</span></span> |
| <xref:System.Security.Cryptography.CspKeyContainerInfo.Removable?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-311">Linux i macOS</span><span class="sxs-lookup"><span data-stu-id="4c3a6-311">Linux and macOS</span></span> |
| <xref:System.Security.Cryptography.CspKeyContainerInfo.UniqueKeyContainerName?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-312">Linux i macOS</span><span class="sxs-lookup"><span data-stu-id="4c3a6-312">Linux and macOS</span></span> |
| <xref:System.Security.Cryptography.HashAlgorithm.Create?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-313">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-313">All</span></span> |
| <xref:System.Security.Cryptography.HMAC.Create?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-314">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-314">All</span></span> |
| <xref:System.Security.Cryptography.HMAC.Create(System.String)?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-315">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-315">All</span></span> |
| <xref:System.Security.Cryptography.HMAC.HashCore%2A?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-316">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-316">All</span></span> |
| <xref:System.Security.Cryptography.HMAC.HashFinal%2A?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-317">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-317">All</span></span> |
| <xref:System.Security.Cryptography.HMAC.Initialize%2A?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-318">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-318">All</span></span> |
| <xref:System.Security.Cryptography.KeyedHashAlgorithm.Create?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-319">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-319">All</span></span> |
| <xref:System.Security.Cryptography.KeyedHashAlgorithm.Create(System.String)?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-320">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-320">All</span></span> |
| <xref:System.Security.Cryptography.ProtectedData.Protect%2A?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-321">Linux i macOS</span><span class="sxs-lookup"><span data-stu-id="4c3a6-321">Linux and macOS</span></span> |
| <xref:System.Security.Cryptography.ProtectedData.Unprotect%2A?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-322">Linux i macOS</span><span class="sxs-lookup"><span data-stu-id="4c3a6-322">Linux and macOS</span></span> |
| <xref:System.Security.Cryptography.RSA.FromXmlString%2A?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-323">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-323">All</span></span> |
| <xref:System.Security.Cryptography.RSA.ToXmlString%2A?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-324">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-324">All</span></span> |
| <xref:System.Security.Cryptography.SymmetricAlgorithm.Create?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-325">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-325">All</span></span> |
| <xref:System.Security.Cryptography.SymmetricAlgorithm.Create(System.String)?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-326">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-326">All</span></span> |

## <a name="systemsecuritycryptographypkcs"></a><span data-ttu-id="4c3a6-327">System. Security. Cryptography. PKCS</span><span class="sxs-lookup"><span data-stu-id="4c3a6-327">System.Security.Cryptography.Pkcs</span></span>

| <span data-ttu-id="4c3a6-328">Członek</span><span class="sxs-lookup"><span data-stu-id="4c3a6-328">Member</span></span> | <span data-ttu-id="4c3a6-329">Platformy, które generują</span><span class="sxs-lookup"><span data-stu-id="4c3a6-329">Platforms that throw</span></span> |
| - | - |
| <xref:System.Security.Cryptography.Pkcs.CmsSigner.%23ctor(System.Security.Cryptography.CspParameters)> | <span data-ttu-id="4c3a6-330">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-330">All</span></span> |
| <xref:System.Security.Cryptography.Pkcs.SignerInfo.ComputeCounterSignature?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-331">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-331">All</span></span> |

## <a name="systemsecuritycryptographyx509certificates"></a><span data-ttu-id="4c3a6-332">System. Security. Cryptography. x509</span><span class="sxs-lookup"><span data-stu-id="4c3a6-332">System.Security.Cryptography.X509Certificates</span></span>

| <span data-ttu-id="4c3a6-333">Członek</span><span class="sxs-lookup"><span data-stu-id="4c3a6-333">Member</span></span> | <span data-ttu-id="4c3a6-334">Platformy, które generują</span><span class="sxs-lookup"><span data-stu-id="4c3a6-334">Platforms that throw</span></span> |
| - | - |
| <xref:System.Security.Cryptography.X509Certificates.X509Certificate.%23ctor(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)> | <span data-ttu-id="4c3a6-335">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-335">All</span></span> |
| <xref:System.Security.Cryptography.X509Certificates.X509Certificate.Import%2A?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-336">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-336">All</span></span> |
| <xref:System.Security.Cryptography.X509Certificates.X509Certificate2.%23ctor(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)> | <span data-ttu-id="4c3a6-337">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-337">All</span></span> |
| <span data-ttu-id="4c3a6-338"><xref:System.Security.Cryptography.X509Certificates.X509Certificate2.PrivateKey?displayProperty=nameWithType> (tylko ustaw)</span><span class="sxs-lookup"><span data-stu-id="4c3a6-338"><xref:System.Security.Cryptography.X509Certificates.X509Certificate2.PrivateKey?displayProperty=nameWithType> (set only)</span></span> | <span data-ttu-id="4c3a6-339">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-339">All</span></span> |

## <a name="systemsecurityauthenticationextendedprotection"></a><span data-ttu-id="4c3a6-340">System. Security. Authentication. Kiedy</span><span class="sxs-lookup"><span data-stu-id="4c3a6-340">System.Security.Authentication.ExtendedProtection</span></span>

| <span data-ttu-id="4c3a6-341">Członek</span><span class="sxs-lookup"><span data-stu-id="4c3a6-341">Member</span></span> | <span data-ttu-id="4c3a6-342">Platformy, które generują</span><span class="sxs-lookup"><span data-stu-id="4c3a6-342">Platforms that throw</span></span> |
| - | - |
| <xref:System.Security.Authentication.ExtendedProtection.ExtendedProtectionPolicy.%23ctor(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)> | <span data-ttu-id="4c3a6-343">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-343">All</span></span> |

## <a name="systemsecuritypolicy"></a><span data-ttu-id="4c3a6-344">System. Security. Policy</span><span class="sxs-lookup"><span data-stu-id="4c3a6-344">System.Security.Policy</span></span>

| <span data-ttu-id="4c3a6-345">Członek</span><span class="sxs-lookup"><span data-stu-id="4c3a6-345">Member</span></span> | <span data-ttu-id="4c3a6-346">Platformy, które generują</span><span class="sxs-lookup"><span data-stu-id="4c3a6-346">Platforms that throw</span></span> |
| - | - |
| <xref:System.Security.Policy.Hash.GetObjectData(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-347">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-347">All</span></span> |

## <a name="systemserviceprocessservicecontroller"></a><span data-ttu-id="4c3a6-348">System. ServiceProcess. ServiceController</span><span class="sxs-lookup"><span data-stu-id="4c3a6-348">System.ServiceProcess.ServiceController</span></span>

| <span data-ttu-id="4c3a6-349">Członek</span><span class="sxs-lookup"><span data-stu-id="4c3a6-349">Member</span></span> | <span data-ttu-id="4c3a6-350">Platformy, które generują</span><span class="sxs-lookup"><span data-stu-id="4c3a6-350">Platforms that throw</span></span> |
| - | - |
| <xref:System.ServiceProcess.TimeoutException.%23ctor(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)> | <span data-ttu-id="4c3a6-351">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-351">All</span></span> |

## <a name="systemtextregularexpressions"></a><span data-ttu-id="4c3a6-352">System.Text.RegularExpressions</span><span class="sxs-lookup"><span data-stu-id="4c3a6-352">System.Text.RegularExpressions</span></span>

| <span data-ttu-id="4c3a6-353">Członek</span><span class="sxs-lookup"><span data-stu-id="4c3a6-353">Member</span></span> | <span data-ttu-id="4c3a6-354">Platformy, które generują</span><span class="sxs-lookup"><span data-stu-id="4c3a6-354">Platforms that throw</span></span> |
| - | - |
| <xref:System.Text.RegularExpressions.Regex.CompileToAssembly%2A?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-355">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-355">All</span></span> |

## <a name="systemthreading"></a><span data-ttu-id="4c3a6-356">System. Threading</span><span class="sxs-lookup"><span data-stu-id="4c3a6-356">System.Threading</span></span>

| <span data-ttu-id="4c3a6-357">Członek</span><span class="sxs-lookup"><span data-stu-id="4c3a6-357">Member</span></span> | <span data-ttu-id="4c3a6-358">Platformy, które generują</span><span class="sxs-lookup"><span data-stu-id="4c3a6-358">Platforms that throw</span></span> |
| - | - |
| <xref:System.Threading.CompressedStack.GetObjectData(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-359">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-359">All</span></span> |
| <xref:System.Threading.ExecutionContext.GetObjectData(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-360">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-360">All</span></span> |
| <xref:System.Threading.Thread.Abort%2A?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-361">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-361">All</span></span> |
| <xref:System.Threading.Thread.ResetAbort?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-362">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-362">All</span></span> |
| <xref:System.Threading.Thread.Resume?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-363">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-363">All</span></span> |
| <xref:System.Threading.Thread.Suspend?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-364">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-364">All</span></span> |

## <a name="systemxml"></a><span data-ttu-id="4c3a6-365">System.Xml</span><span class="sxs-lookup"><span data-stu-id="4c3a6-365">System.Xml</span></span>

| <span data-ttu-id="4c3a6-366">Członek</span><span class="sxs-lookup"><span data-stu-id="4c3a6-366">Member</span></span> | <span data-ttu-id="4c3a6-367">Platformy, które generują</span><span class="sxs-lookup"><span data-stu-id="4c3a6-367">Platforms that throw</span></span> |
| - | - |
| <xref:System.Xml.XmlDictionaryReader.CreateMtomReader(System.Byte[],System.Int32,System.Int32,System.Text.Encoding[],System.String,System.Xml.XmlDictionaryReaderQuotas,System.Int32,System.Xml.OnXmlDictionaryReaderClose)?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-368">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-368">All</span></span> |
| <xref:System.Xml.XmlDictionaryReader.CreateMtomReader(System.IO.Stream,System.Text.Encoding[],System.String,System.Xml.XmlDictionaryReaderQuotas,System.Int32,System.Xml.OnXmlDictionaryReaderClose)?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-369">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-369">All</span></span> |
| <xref:System.Xml.XmlDictionaryWriter.CreateMtomWriter(System.IO.Stream,System.Text.Encoding,System.Int32,System.String,System.String,System.String,System.Boolean,System.Boolean)?displayProperty=nameWithType> | <span data-ttu-id="4c3a6-370">Wszystko</span><span class="sxs-lookup"><span data-stu-id="4c3a6-370">All</span></span> |

## <a name="see-also"></a><span data-ttu-id="4c3a6-371">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="4c3a6-371">See also</span></span>

- [<span data-ttu-id="4c3a6-372">Istotne zmiany dotyczące migracji z .NET Framework do platformy .NET Core</span><span class="sxs-lookup"><span data-stu-id="4c3a6-372">Breaking changes for migration from .NET Framework to .NET Core</span></span>](fx-core.md)
- [<span data-ttu-id="4c3a6-373">Serializacja binarna w programie .NET Core</span><span class="sxs-lookup"><span data-stu-id="4c3a6-373">Binary serialization in .NET Core</span></span>](../../standard/serialization/binary-serialization.md#net-core)
- [<span data-ttu-id="4c3a6-374">Analizator przenośności platformy .NET</span><span class="sxs-lookup"><span data-stu-id="4c3a6-374">.NET portability analyzer</span></span>](../../standard/analyzers/portability-analyzer.md)
