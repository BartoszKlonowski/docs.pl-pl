---
title: Nazwy zestawów i bibliotek DLL
description: Poznaj wskazówki dotyczące nazewnictwa zestawów i bibliotek dołączanych dynamicznie (dll). Zestaw może obejmować jeden lub więcej plików, ale zwykle mapuje jeden do jednego z biblioteką DLL.
ms.date: 10/22/2008
helpviewer_keywords:
- names [.NET Framework], DLLs
- names [.NET Framework], assemblies
- assemblies [.NET Framework], names
- DLLs, names
ms.assetid: e800b610-31b4-4949-9c14-cb60e9f254be
ms.openlocfilehash: 2d1484889eb7db537de970c31109f26a6d61ad8d
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/18/2020
ms.locfileid: "94830054"
---
# <a name="names-of-assemblies-and-dlls"></a><span data-ttu-id="881b2-104">Nazwy zestawów i bibliotek DLL</span><span class="sxs-lookup"><span data-stu-id="881b2-104">Names of Assemblies and DLLs</span></span>
<span data-ttu-id="881b2-105">Zestaw jest jednostką wdrożenia i tożsamością dla programów kodu zarządzanego.</span><span class="sxs-lookup"><span data-stu-id="881b2-105">An assembly is the unit of deployment and identity for managed code programs.</span></span> <span data-ttu-id="881b2-106">Chociaż zestawy mogą obejmować jeden lub więcej plików, zazwyczaj zestaw mapuje jeden do jednego z biblioteką DLL.</span><span class="sxs-lookup"><span data-stu-id="881b2-106">Although assemblies can span one or more files, typically an assembly maps one-to-one with a DLL.</span></span> <span data-ttu-id="881b2-107">W związku z tym, w tej sekcji opisano tylko konwencje nazewnictwa bibliotek DLL, które następnie można mapować na konwencje nazewnictwa zestawów.</span><span class="sxs-lookup"><span data-stu-id="881b2-107">Therefore, this section describes only DLL naming conventions, which then can be mapped to assembly naming conventions.</span></span>

 <span data-ttu-id="881b2-108">✔️ Wybierz nazwy bibliotek DLL zestawu, które sugerują duże fragmenty funkcjonalności, takich jak system. Data.</span><span class="sxs-lookup"><span data-stu-id="881b2-108">✔️ DO choose names for your assembly DLLs that suggest large chunks of functionality, such as System.Data.</span></span>

 <span data-ttu-id="881b2-109">Nazwy zestawów i bibliotek DLL nie muszą odpowiadać nazwom przestrzeni nazw, ale podczas określania nazw zestawów można przestrzegać nazwy przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="881b2-109">Assembly and DLL names don’t have to correspond to namespace names, but it is reasonable to follow the namespace name when naming assemblies.</span></span> <span data-ttu-id="881b2-110">Dobrą regułą dla kciuka jest nazwa biblioteki DLL na podstawie wspólnego prefiksu przestrzeni nazw zawartych w zestawie.</span><span class="sxs-lookup"><span data-stu-id="881b2-110">A good rule of thumb is to name the DLL based on the common prefix of the namespaces contained in the assembly.</span></span> <span data-ttu-id="881b2-111">Na przykład zestaw z dwoma przestrzeniami nazw `MyCompany.MyTechnology.FirstFeature` i `MyCompany.MyTechnology.SecondFeature` , można wywołać `MyCompany.MyTechnology.dll` .</span><span class="sxs-lookup"><span data-stu-id="881b2-111">For example, an assembly with two namespaces, `MyCompany.MyTechnology.FirstFeature` and `MyCompany.MyTechnology.SecondFeature`, could be called `MyCompany.MyTechnology.dll`.</span></span>

 <span data-ttu-id="881b2-112">✔️ ROZWAŻYĆ nazewnictwa bibliotek DLL zgodnie z poniższym wzorcem:</span><span class="sxs-lookup"><span data-stu-id="881b2-112">✔️ CONSIDER naming DLLs according to the following pattern:</span></span>

 `<Company>.<Component>.dll`

 <span data-ttu-id="881b2-113">gdzie `<Component>` zawiera jedną lub więcej klauzul rozdzielonych kropkami.</span><span class="sxs-lookup"><span data-stu-id="881b2-113">where `<Component>` contains one or more dot-separated clauses.</span></span> <span data-ttu-id="881b2-114">Przykład:</span><span class="sxs-lookup"><span data-stu-id="881b2-114">For example:</span></span>

 <span data-ttu-id="881b2-115">`Litware.Controls.dll`.</span><span class="sxs-lookup"><span data-stu-id="881b2-115">`Litware.Controls.dll`.</span></span>

 <span data-ttu-id="881b2-116">*Fragmenty © 2005, 2009 Microsoft Corporation. Wszelkie prawa zastrzeżone.*</span><span class="sxs-lookup"><span data-stu-id="881b2-116">*Portions © 2005, 2009 Microsoft Corporation. All rights reserved.*</span></span>

 <span data-ttu-id="881b2-117">*Ponownie Wydrukowano przez uprawnienie Pearson Education, Inc. z [wytycznych dotyczących projektowania platformy: konwencje, idiomy i wzorce dla bibliotek .NET do wielokrotnego użytku, 2. wydanie](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) przez Krzysztof Cwalina i Brad Abrams, opublikowane 22, 2008 przez Addison-Wesley Professional w ramach serii Microsoft Windows Development.*</span><span class="sxs-lookup"><span data-stu-id="881b2-117">*Reprinted by permission of Pearson Education, Inc. from [Framework Design Guidelines: Conventions, Idioms, and Patterns for Reusable .NET Libraries, 2nd Edition](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) by Krzysztof Cwalina and Brad Abrams, published Oct 22, 2008 by Addison-Wesley Professional as part of the Microsoft Windows Development Series.*</span></span>

## <a name="see-also"></a><span data-ttu-id="881b2-118">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="881b2-118">See also</span></span>

- [<span data-ttu-id="881b2-119">Wskazówki dotyczące projektowania struktury</span><span class="sxs-lookup"><span data-stu-id="881b2-119">Framework Design Guidelines</span></span>](index.md)
- [<span data-ttu-id="881b2-120">Wskazówki dotyczące nazewnictwa</span><span class="sxs-lookup"><span data-stu-id="881b2-120">Naming Guidelines</span></span>](naming-guidelines.md)
