---
title: Reguły dokumentacji (analiza kodu)
description: Poznaj reguły dokumentacji dotyczącej reguł analizy kodu
ms.date: 09/16/2019
ms.topic: reference
f1_keywords:
- vs.codeanalysis.documentationrules
helpviewer_keywords:
- documentation rules
- managed code analysis rules, documentation rules
- warnings, documentation
author: mavasani
ms.author: mavasani
ms.openlocfilehash: 29d1734eec29bd00d456b4b00c48c2e8ef223441
ms.sourcegitcommit: 2e4adc490c1d2a705a0592b295d606b10b9f51f1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/25/2020
ms.locfileid: "96587220"
---
# <a name="documentation-rules"></a><span data-ttu-id="13edc-103">Reguły dokumentacji</span><span class="sxs-lookup"><span data-stu-id="13edc-103">Documentation rules</span></span>

<span data-ttu-id="13edc-104">Reguły dokumentacji obsługują pisanie dobrze udokumentowanych bibliotek poprzez poprawne użycie [komentarzy dokumentacji XML](../../../csharp/codedoc.md) dla widocznych na zewnątrz interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="13edc-104">Documentation rules support writing well-documented libraries through the correct use of [XML documentation comments](../../../csharp/codedoc.md) for externally visible APIs.</span></span>

## <a name="in-this-section"></a><span data-ttu-id="13edc-105">W tej sekcji</span><span class="sxs-lookup"><span data-stu-id="13edc-105">In this section</span></span>

| <span data-ttu-id="13edc-106">Reguła</span><span class="sxs-lookup"><span data-stu-id="13edc-106">Rule</span></span> | <span data-ttu-id="13edc-107">Opis</span><span class="sxs-lookup"><span data-stu-id="13edc-107">Description</span></span> |
| - | - |
| [<span data-ttu-id="13edc-108">CA1200: Unikaj używania tagów cref z prefiksem</span><span class="sxs-lookup"><span data-stu-id="13edc-108">CA1200: Avoid using cref tags with a prefix</span></span>](ca1200.md) | <span data-ttu-id="13edc-109">Atrybut [cref](../../../csharp/programming-guide/xmldoc/cref-attribute.md) w tagu dokumentacji XML oznacza "odwołanie do kodu".</span><span class="sxs-lookup"><span data-stu-id="13edc-109">The [cref](../../../csharp/programming-guide/xmldoc/cref-attribute.md) attribute in an XML documentation tag means "code reference".</span></span> <span data-ttu-id="13edc-110">Określa, że wewnętrznym tekstem znacznika jest element kodu, taki jak typ, metoda lub właściwość.</span><span class="sxs-lookup"><span data-stu-id="13edc-110">It specifies that the inner text of the tag is a code element, such as a type, method, or property.</span></span> <span data-ttu-id="13edc-111">Należy unikać używania `cref` tagów z prefiksami, ponieważ uniemożliwia kompilatorowi Weryfikowanie odwołań.</span><span class="sxs-lookup"><span data-stu-id="13edc-111">Avoid using `cref` tags with prefixes, because it prevents the compiler from verifying references.</span></span> <span data-ttu-id="13edc-112">Uniemożliwia również znajdowanie i aktualizowanie tych odwołań do tych symboli podczas refaktoryzacji przez program Visual Studio Integrated Development Environment (IDE).</span><span class="sxs-lookup"><span data-stu-id="13edc-112">It also prevents the Visual Studio integrated development environment (IDE) from finding and updating these symbol references during refactorings.</span></span> |
