---
title: Reguły dotyczące zbędnego kodu
description: Dowiedz się więcej o niepotrzebnych regułach kodu analizy kodu
ms.date: 09/30/2020
ms.topic: reference
author: gewarren
ms.author: gewarren
dev_langs:
- CSharp
- VB
ms.openlocfilehash: 16c4ba0e4bee2388736bf9813a3e8290d8d4da32
ms.sourcegitcommit: 48466b8fb7332ececff5dc388f19f6b3ff503dd4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/05/2020
ms.locfileid: "96589868"
---
# <a name="unnecessary-code-rules"></a><span data-ttu-id="82fb7-103">Reguły dotyczące zbędnego kodu</span><span class="sxs-lookup"><span data-stu-id="82fb7-103">Unnecessary code rules</span></span>

<span data-ttu-id="82fb7-104">Niepotrzebne reguły kodu identyfikują różne części bazy kodu, które są zbędne i mogą być refaktoryzacjne lub usuwane.</span><span class="sxs-lookup"><span data-stu-id="82fb7-104">Unnecessary code rules identify different parts of the code base that are unnecessary and can be refactored or removed.</span></span> <span data-ttu-id="82fb7-105">Obecność niepotrzebnego kodu wskazuje jeden z następujących problemów:</span><span class="sxs-lookup"><span data-stu-id="82fb7-105">The presence of unnecessary code indicates one of more of the following problems:</span></span>

- <span data-ttu-id="82fb7-106">Czytelność: kod, który jest niekoniecznie obniżać czytelność.</span><span class="sxs-lookup"><span data-stu-id="82fb7-106">Readability: Code that is unnecessarily degrading readability.</span></span> <span data-ttu-id="82fb7-107">Na przykład flagi [IDE0001](ide0001.md) niepotrzebne kwalifikacje nazw typów.</span><span class="sxs-lookup"><span data-stu-id="82fb7-107">For example, [IDE0001](ide0001.md) flags unnecessary type-name qualifications.</span></span>
- <span data-ttu-id="82fb7-108">Łatwość konserwacji: kod, który nie jest już używany po refaktoryzacji i jest niepotrzebny.</span><span class="sxs-lookup"><span data-stu-id="82fb7-108">Maintainability: Code that is no longer used after refactoring and is unnecessarily being maintained.</span></span> <span data-ttu-id="82fb7-109">Na przykład flagi [IDE0051](ide0051.md) nieużywające prywatnych pól, właściwości, zdarzeń i metod.</span><span class="sxs-lookup"><span data-stu-id="82fb7-109">For example, [IDE0051](ide0051.md) flags unused private fields, properties, events, and methods.</span></span>
- <span data-ttu-id="82fb7-110">Wydajność: niepotrzebne obliczenie, które nie ma efektów ubocznych i prowadzi do niepotrzebnych obciążeń związanych z wydajnością.</span><span class="sxs-lookup"><span data-stu-id="82fb7-110">Performance: Unnecessary computation that has no side effects and leads to unnecessary performance overhead.</span></span> <span data-ttu-id="82fb7-111">Na przykład flagi [IDE0059](ide0059.md) nieużywane przypisania wartości, gdzie wyrażenie służące do obliczania wartości nie ma żadnych efektów ubocznych.</span><span class="sxs-lookup"><span data-stu-id="82fb7-111">For example, [IDE0059](ide0059.md) flags unused value assignments where the expression to compute a value has no side effects.</span></span>
- <span data-ttu-id="82fb7-112">Funkcja: problem funkcjonalny w kodzie prowadzący do wymaganego kodu, który jest renderowany jako nadmiarowy.</span><span class="sxs-lookup"><span data-stu-id="82fb7-112">Functionality: Functional issue in code leading to required code being rendered redundant.</span></span> <span data-ttu-id="82fb7-113">Na przykład flagi [IDE0060](ide0060.md) nieużywane parametry, w których Metoda przypadkowo ignoruje parametr wejściowy.</span><span class="sxs-lookup"><span data-stu-id="82fb7-113">For example, [IDE0060](ide0060.md) flags unused parameters where the method accidentally ignores an input parameter.</span></span>

<span data-ttu-id="82fb7-114">Reguły w tej sekcji dotyczą następujących niepotrzebnych reguł kodu:</span><span class="sxs-lookup"><span data-stu-id="82fb7-114">The rules in this section concern the following unnecessary code rules:</span></span>

- [<span data-ttu-id="82fb7-115">Uprość nazwę (IDE0001)</span><span class="sxs-lookup"><span data-stu-id="82fb7-115">Simplify name (IDE0001)</span></span>](ide0001.md)
- [<span data-ttu-id="82fb7-116">Uprość dostęp do składowych (IDE0002)</span><span class="sxs-lookup"><span data-stu-id="82fb7-116">Simplify member access (IDE0002)</span></span>](ide0002.md)
- [<span data-ttu-id="82fb7-117">Usuń niepotrzebne rzutowanie (IDE0004)</span><span class="sxs-lookup"><span data-stu-id="82fb7-117">Remove unnecessary cast (IDE0004)</span></span>](ide0004.md)
- [<span data-ttu-id="82fb7-118">Usuń niepotrzebne Importy (IDE0005)</span><span class="sxs-lookup"><span data-stu-id="82fb7-118">Remove unnecessary import (IDE0005)</span></span>](ide0005.md)
- [<span data-ttu-id="82fb7-119">Usuń nieosiągalny kod (IDE0035)</span><span class="sxs-lookup"><span data-stu-id="82fb7-119">Remove unreachable code (IDE0035)</span></span>](ide0035.md)
- [<span data-ttu-id="82fb7-120">Usuń nieużywany prywatny element członkowski (IDE0051)</span><span class="sxs-lookup"><span data-stu-id="82fb7-120">Remove unused private member (IDE0051)</span></span>](ide0051.md)
- [<span data-ttu-id="82fb7-121">Usuń odczytanie prywatnego elementu członkowskiego (IDE0052)</span><span class="sxs-lookup"><span data-stu-id="82fb7-121">Remove unread private member (IDE0052)</span></span>](ide0052.md)
- [<span data-ttu-id="82fb7-122">Usuń nieużywaną wartość wyrażenia (IDE0058)</span><span class="sxs-lookup"><span data-stu-id="82fb7-122">Remove unused expression value (IDE0058)</span></span>](ide0058.md)
- [<span data-ttu-id="82fb7-123">Usuń niepotrzebne przypisanie wartości (IDE0059)</span><span class="sxs-lookup"><span data-stu-id="82fb7-123">Remove unnecessary value assignment (IDE0059)</span></span>](ide0059.md)
- [<span data-ttu-id="82fb7-124">Usuń nieużywany parametr (IDE0060)</span><span class="sxs-lookup"><span data-stu-id="82fb7-124">Remove unused parameter (IDE0060)</span></span>](ide0060.md)
- [<span data-ttu-id="82fb7-125">Usuń niepotrzebne pomijanie (IDE0079)</span><span class="sxs-lookup"><span data-stu-id="82fb7-125">Remove unnecessary suppression (IDE0079)</span></span>](ide0079.md)
- <span data-ttu-id="82fb7-126">[Usuń niezbędny operator pomijania (IDE0080)](ide0080.md) — tylko język C#.</span><span class="sxs-lookup"><span data-stu-id="82fb7-126">[Remove unnecessary suppression operator (IDE0080)](ide0080.md) - C# only.</span></span>
- <span data-ttu-id="82fb7-127">[Usuń element "ByVal" (IDE0081)](ide0081.md) — tylko Visual Basic.</span><span class="sxs-lookup"><span data-stu-id="82fb7-127">[Remove 'ByVal' (IDE0081)](ide0081.md) - Visual Basic only.</span></span>
- [<span data-ttu-id="82fb7-128">Usuń niezbędny operator równości (IDE0100)</span><span class="sxs-lookup"><span data-stu-id="82fb7-128">Remove unnecessary equality operator (IDE0100)</span></span>](ide0100.md)
- <span data-ttu-id="82fb7-129">[Usuń niepotrzebne odrzucanie (IDE0110)](ide0110.md) — tylko w języku C#.</span><span class="sxs-lookup"><span data-stu-id="82fb7-129">[Remove unnecessary discard (IDE0110)](ide0110.md) - C# only.</span></span>

<span data-ttu-id="82fb7-130">Niektóre z tych reguł mają opcje konfigurowania zachowania reguły:</span><span class="sxs-lookup"><span data-stu-id="82fb7-130">Some of these rules have options to configure the rule behavior:</span></span>

- [<span data-ttu-id="82fb7-131">csharp_style_unused_value_expression_statement_preference (IDE0058)</span><span class="sxs-lookup"><span data-stu-id="82fb7-131">csharp_style_unused_value_expression_statement_preference (IDE0058)</span></span>](ide0058.md#csharp_style_unused_value_expression_statement_preference)
- [<span data-ttu-id="82fb7-132">visual_basic_style_unused_value_expression_statement_preference (IDE0058)</span><span class="sxs-lookup"><span data-stu-id="82fb7-132">visual_basic_style_unused_value_expression_statement_preference (IDE0058)</span></span>](ide0058.md#visual_basic_style_unused_value_expression_statement_preference)
- [<span data-ttu-id="82fb7-133">csharp_style_unused_value_assignment_preference (IDE0059)</span><span class="sxs-lookup"><span data-stu-id="82fb7-133">csharp_style_unused_value_assignment_preference (IDE0059)</span></span>](ide0059.md#csharp_style_unused_value_assignment_preference)
- [<span data-ttu-id="82fb7-134">visual_basic_style_unused_value_assignment_preference (IDE0059)</span><span class="sxs-lookup"><span data-stu-id="82fb7-134">visual_basic_style_unused_value_assignment_preference (IDE0059)</span></span>](ide0059.md#visual_basic_style_unused_value_assignment_preference)
- [<span data-ttu-id="82fb7-135">dotnet_code_quality_unused_parameters (IDE0060)</span><span class="sxs-lookup"><span data-stu-id="82fb7-135">dotnet_code_quality_unused_parameters (IDE0060)</span></span>](ide0060.md#dotnet_code_quality_unused_parameters)
- [<span data-ttu-id="82fb7-136">dotnet_remove_unnecessary_suppression_exclusions (IDE0079)</span><span class="sxs-lookup"><span data-stu-id="82fb7-136">dotnet_remove_unnecessary_suppression_exclusions (IDE0079)</span></span>](ide0079.md#dotnet_remove_unnecessary_suppression_exclusions)

## <a name="see-also"></a><span data-ttu-id="82fb7-137">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="82fb7-137">See also</span></span>

- [<span data-ttu-id="82fb7-138">Reguły języka stylu kodu</span><span class="sxs-lookup"><span data-stu-id="82fb7-138">Code style language rules</span></span>](language-rules.md)
- [<span data-ttu-id="82fb7-139">Dokumentacja reguł stylu kodu</span><span class="sxs-lookup"><span data-stu-id="82fb7-139">Code style rules reference</span></span>](index.md)
