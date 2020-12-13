---
title: Zmiany w bibliotece .NET
description: Wyświetla listę istotnych zmian w podstawowych bibliotekach .NET dla platformy .NET Core w wersji 1.0-3.0.
ms.date: 07/27/2020
ms.openlocfilehash: 092ff36a5e07c9e226fe2a67d5e7cfd391e9d16b
ms.sourcegitcommit: fcbe432482464b1639decad78cc4dc8387c6269e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/12/2020
ms.locfileid: "97366876"
---
# <a name="core-net-libraries-breaking-changes-in-net-core-10-30"></a><span data-ttu-id="a06b7-103">Podstawowe biblioteki .NET istotne zmiany w programie .NET Core 1.0 — 3.0</span><span class="sxs-lookup"><span data-stu-id="a06b7-103">Core .NET libraries breaking changes in .NET Core 1.0-3.0</span></span>

<span data-ttu-id="a06b7-104">Podstawowe biblioteki .NET zapewniają pierwotne i inne typy ogólne używane przez platformę .NET Core.</span><span class="sxs-lookup"><span data-stu-id="a06b7-104">The core .NET libraries provide the primitives and other general types used by .NET Core.</span></span>

<span data-ttu-id="a06b7-105">Następujące istotne zmiany zostały udokumentowane na tej stronie:</span><span class="sxs-lookup"><span data-stu-id="a06b7-105">The following breaking changes are documented on this page:</span></span>

| <span data-ttu-id="a06b7-106">Zmiana podziału</span><span class="sxs-lookup"><span data-stu-id="a06b7-106">Breaking change</span></span> | <span data-ttu-id="a06b7-107">Wprowadzona wersja</span><span class="sxs-lookup"><span data-stu-id="a06b7-107">Version introduced</span></span> |
| - | :-: |
| [<span data-ttu-id="a06b7-108">Przekazanie grupy GroupCollection do metod rozszerzających, które \<T> wymagają uściślania</span><span class="sxs-lookup"><span data-stu-id="a06b7-108">Passing GroupCollection to extension methods taking IEnumerable\<T> requires disambiguation</span></span>](#passing-groupcollection-to-extension-methods-taking-ienumerablet-requires-disambiguation) | <span data-ttu-id="a06b7-109">3.0</span><span class="sxs-lookup"><span data-stu-id="a06b7-109">3.0</span></span> |
| [<span data-ttu-id="a06b7-110">Interfejsy API służące do raportowania wersji teraz produktu i nie wersji</span><span class="sxs-lookup"><span data-stu-id="a06b7-110">APIs that report version now report product and not file version</span></span>](#apis-that-report-version-now-report-product-and-not-file-version) | <span data-ttu-id="a06b7-111">3.0</span><span class="sxs-lookup"><span data-stu-id="a06b7-111">3.0</span></span> |
| [<span data-ttu-id="a06b7-112">Niestandardowe wystąpienia EncoderFallbackBuffer nie mogą podlegać rekursywnie</span><span class="sxs-lookup"><span data-stu-id="a06b7-112">Custom EncoderFallbackBuffer instances cannot fall back recursively</span></span>](#custom-encoderfallbackbuffer-instances-cannot-fall-back-recursively) | <span data-ttu-id="a06b7-113">3.0</span><span class="sxs-lookup"><span data-stu-id="a06b7-113">3.0</span></span> |
| [<span data-ttu-id="a06b7-114">Zmiany zachowań formatowania zmiennoprzecinkowego i analizowania</span><span class="sxs-lookup"><span data-stu-id="a06b7-114">Floating point formatting and parsing behavior changes</span></span>](#floating-point-formatting-and-parsing-behavior-changed) | <span data-ttu-id="a06b7-115">3.0</span><span class="sxs-lookup"><span data-stu-id="a06b7-115">3.0</span></span> |
| [<span data-ttu-id="a06b7-116">Operacje analizowania zmiennoprzecinkowe nie będą już kończyć się niepowodzeniem lub nie generują wyjątku overflow</span><span class="sxs-lookup"><span data-stu-id="a06b7-116">Floating-point parsing operations no longer fail or throw an OverflowException</span></span>](#floating-point-parsing-operations-no-longer-fail-or-throw-an-overflowexception) | <span data-ttu-id="a06b7-117">3.0</span><span class="sxs-lookup"><span data-stu-id="a06b7-117">3.0</span></span> |
| [<span data-ttu-id="a06b7-118">InvalidAsynchronousStateException — przeniesiony do innego zestawu</span><span class="sxs-lookup"><span data-stu-id="a06b7-118">InvalidAsynchronousStateException moved to another assembly</span></span>](#invalidasynchronousstateexception-moved-to-another-assembly) | <span data-ttu-id="a06b7-119">3.0</span><span class="sxs-lookup"><span data-stu-id="a06b7-119">3.0</span></span> |
| [<span data-ttu-id="a06b7-120">Zastępowanie źle sformułowanych sekwencji bajtów w formacie UTF-8 następuje po wskazówkach dotyczących standardu Unicode</span><span class="sxs-lookup"><span data-stu-id="a06b7-120">Replacing ill-formed UTF-8 byte sequences follows Unicode guidelines</span></span>](#replacing-ill-formed-utf-8-byte-sequences-follows-unicode-guidelines) | <span data-ttu-id="a06b7-121">3.0</span><span class="sxs-lookup"><span data-stu-id="a06b7-121">3.0</span></span> |
| [<span data-ttu-id="a06b7-122">TypeDescriptionProviderAttribute przeniesiony do innego zestawu</span><span class="sxs-lookup"><span data-stu-id="a06b7-122">TypeDescriptionProviderAttribute moved to another assembly</span></span>](#typedescriptionproviderattribute-moved-to-another-assembly) | <span data-ttu-id="a06b7-123">3.0</span><span class="sxs-lookup"><span data-stu-id="a06b7-123">3.0</span></span> |
| [<span data-ttu-id="a06b7-124">Element ZipArchiveEntry nie obsługuje już archiwów z niespójnymi rozmiarami wpisów</span><span class="sxs-lookup"><span data-stu-id="a06b7-124">ZipArchiveEntry no longer handles archives with inconsistent entry sizes</span></span>](#ziparchiveentry-no-longer-handles-archives-with-inconsistent-entry-sizes) | <span data-ttu-id="a06b7-125">3.0</span><span class="sxs-lookup"><span data-stu-id="a06b7-125">3.0</span></span> |
| [<span data-ttu-id="a06b7-126">Element FieldInfo. SetValue zgłasza wyjątek dla pól static, tylko init</span><span class="sxs-lookup"><span data-stu-id="a06b7-126">FieldInfo.SetValue throws exception for static, init-only fields</span></span>](#fieldinfosetvalue-throws-exception-for-static-init-only-fields) | <span data-ttu-id="a06b7-127">3.0</span><span class="sxs-lookup"><span data-stu-id="a06b7-127">3.0</span></span> |
| [<span data-ttu-id="a06b7-128">Pola prywatne dodane do wbudowanych typów struktur</span><span class="sxs-lookup"><span data-stu-id="a06b7-128">Private fields added to built-in struct types</span></span>](#private-fields-added-to-built-in-struct-types) | <span data-ttu-id="a06b7-129">2.1</span><span class="sxs-lookup"><span data-stu-id="a06b7-129">2.1</span></span> |
| [<span data-ttu-id="a06b7-130">Zmień wartość domyślną UseShellExecute</span><span class="sxs-lookup"><span data-stu-id="a06b7-130">Change in default value of UseShellExecute</span></span>](#change-in-default-value-of-useshellexecute) | <span data-ttu-id="a06b7-131">2.1</span><span class="sxs-lookup"><span data-stu-id="a06b7-131">2.1</span></span> |
| [<span data-ttu-id="a06b7-132">Wersje OpenSSL na macOS</span><span class="sxs-lookup"><span data-stu-id="a06b7-132">OpenSSL versions on macOS</span></span>](#openssl-versions-on-macos) | <span data-ttu-id="a06b7-133">2.1</span><span class="sxs-lookup"><span data-stu-id="a06b7-133">2.1</span></span> |
| [<span data-ttu-id="a06b7-134">UnauthorizedAccessException zgłoszone przez FileSystemInfo. Attributes</span><span class="sxs-lookup"><span data-stu-id="a06b7-134">UnauthorizedAccessException thrown by FileSystemInfo.Attributes</span></span>](#unauthorizedaccessexception-thrown-by-filesysteminfoattributes) | <span data-ttu-id="a06b7-135">1.0</span><span class="sxs-lookup"><span data-stu-id="a06b7-135">1.0</span></span> |
| [<span data-ttu-id="a06b7-136">Obsługa wyjątków uszkodzonego stanu procesu nie jest obsługiwana</span><span class="sxs-lookup"><span data-stu-id="a06b7-136">Handling corrupted-process-state exceptions is not supported</span></span>](#handling-corrupted-state-exceptions-is-not-supported) | <span data-ttu-id="a06b7-137">1.0</span><span class="sxs-lookup"><span data-stu-id="a06b7-137">1.0</span></span> |
| [<span data-ttu-id="a06b7-138">Właściwości UriBuilder nie dołączają już znaków wiodących</span><span class="sxs-lookup"><span data-stu-id="a06b7-138">UriBuilder properties no longer prepend leading characters</span></span>](#uribuilder-properties-no-longer-prepend-leading-characters) | <span data-ttu-id="a06b7-139">1.0</span><span class="sxs-lookup"><span data-stu-id="a06b7-139">1.0</span></span> |
| [<span data-ttu-id="a06b7-140">Proces. element StartInfo zgłasza InvalidOperationException dla procesów, które nie zostały uruchomione</span><span class="sxs-lookup"><span data-stu-id="a06b7-140">Process.StartInfo throws InvalidOperationException for processes you didn't start</span></span>](#processstartinfo-throws-invalidoperationexception-for-processes-you-didnt-start) | <span data-ttu-id="a06b7-141">1.0</span><span class="sxs-lookup"><span data-stu-id="a06b7-141">1.0</span></span> |

## <a name="net-core-30"></a><span data-ttu-id="a06b7-142">.NET Core 3.0</span><span class="sxs-lookup"><span data-stu-id="a06b7-142">.NET Core 3.0</span></span>

[!INCLUDE [disambiguate-generic-type-for-groupcollection](../../../includes/core-changes/corefx/3.0/disambiguate-generic-type-for-groupcollection.md)]

***

[!INCLUDE[APIs that report version now report product and not file version](~/includes/core-changes/corefx/3.0/version-information-changes.md)]

<span data-ttu-id="a06b7-143">\*\*_</span><span class="sxs-lookup"><span data-stu-id="a06b7-143">\*\*_</span></span>

[!INCLUDE[Custom EncoderFallbackBuffer instances cannot fall back recursively](~/includes/core-changes/corefx/3.0/custom-encoderfallbackbuffer-cannot-be-recursive.md)]

_*_

[!INCLUDE[Floating point formatting and parsing behavior changes](~/includes/core-changes/corefx/3.0/floating-point-changes.md)]

_*_

[!INCLUDE[Floating-point parsing operations no longer fail or throw an OverflowException](~/includes/core-changes/corefx/3.0/floating-point-parsing-does-not-overflow.md)]

_*_

[!INCLUDE[InvalidAsynchronousStateException moved to another assembly](~/includes/core-changes/corefx/3.0/move-invalidasynchronousstateexception.md)]

_*_

[!INCLUDE[NET Core 3.0 follows Unicode best practices when replacing ill-formed UTF-8 byte sequences](~/includes/core-changes/corefx/3.0/net-core-3-0-follows-unicode-utf8-best-practices.md)]

_*_

[!INCLUDE[TypeDescriptionProviderAttribute moved to another assembly](~/includes/core-changes/corefx/3.0/move-typedescriptionproviderattribute.md)]

_*_

[!INCLUDE[ZipArchiveEntry no longer handles archives with inconsistent entry sizes](~/includes/core-changes/corefx/3.0/ziparchiveentry-and-inconsistent-entry-sizes.md)]

_*_

[!INCLUDE [FieldInfo.SetValue throws exception for static, init-only fields](~/includes/core-changes/corefx/3.0/fieldinfo-setvalue-exception.md)]

_*_

## <a name="net-core-21"></a><span data-ttu-id="a06b7-144">.NET Core 2.1</span><span class="sxs-lookup"><span data-stu-id="a06b7-144">.NET Core 2.1</span></span>

[!INCLUDE[Private fields added to built-in struct types](~/includes/core-changes/corefx/2.1/instantiate-struct.md)]

_*_

[!INCLUDE[Change in default value of UseShellExecute](~/includes/core-changes/corefx/2.1/process-start-changes.md)]

_*_

[!INCLUDE [OpenSSL versions on macOS](../../../includes/core-changes/corefx/openssl-dependencies-macos.md)]

_*_

## <a name="net-core-10"></a><span data-ttu-id="a06b7-145">.NET Core 1,0</span><span class="sxs-lookup"><span data-stu-id="a06b7-145">.NET Core 1.0</span></span>

[!INCLUDE [UnauthorizedAccessException thrown by FileSystemInfo.Attributes](~/includes/core-changes/corefx/1.0/filesysteminfo-attributes-exceptions.md)]

_*_

[!INCLUDE [corrupted-state-exceptions](~/includes/core-changes/corefx/1.0/corrupted-state-exceptions.md)]

_*_

[!INCLUDE [uribuilder-behavior-changes](../../../includes/core-changes/corefx/1.0/uribuilder-behavior-changes.md)]

_*_

[!INCLUDE [startinfo-throws-exception](../../../includes/core-changes/corefx/1.0/startinfo-throws-exception.md)]

<span data-ttu-id="a06b7-146">_\*\*</span><span class="sxs-lookup"><span data-stu-id="a06b7-146">_\*\*</span></span>
