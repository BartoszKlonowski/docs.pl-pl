---
title: Niezapieczętowane klasy
ms.date: 10/22/2008
helpviewer_keywords:
- classes [.NET Framework], unsealed
- unsealed classes
- inheritance, classes
ms.assetid: 9a3bd505-90f5-4053-9f0d-3cf5fa3d3ebf
ms.openlocfilehash: b2e14b435aa567f231230da34307014210d46ccb
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/18/2020
ms.locfileid: "94828520"
---
# <a name="unsealed-classes"></a><span data-ttu-id="f00dd-102">Niezapieczętowane klasy</span><span class="sxs-lookup"><span data-stu-id="f00dd-102">Unsealed Classes</span></span>
<span data-ttu-id="f00dd-103">Klasy zapieczętowane nie mogą być dziedziczone z i uniemożliwiają rozszerzanie.</span><span class="sxs-lookup"><span data-stu-id="f00dd-103">Sealed classes cannot be inherited from, and they prevent extensibility.</span></span> <span data-ttu-id="f00dd-104">Z kolei klasy, które mogą być dziedziczone z, są nazywane niezapieczętowanymi klasami.</span><span class="sxs-lookup"><span data-stu-id="f00dd-104">In contrast, classes that can be inherited from are called unsealed classes.</span></span>

 <span data-ttu-id="f00dd-105">✔️ ROZWAŻYĆ użycie niezapieczętowanych klas bez dodanych wirtualnych lub chronionych elementów członkowskich jako doskonały sposób zapewnienia niedrogiej jeszcze bardziej łatwiejszej rozszerzalności na platformę.</span><span class="sxs-lookup"><span data-stu-id="f00dd-105">✔️ CONSIDER using unsealed classes with no added virtual or protected members as a great way to provide inexpensive yet much appreciated extensibility to a framework.</span></span>

 <span data-ttu-id="f00dd-106">Deweloperzy często chcą dziedziczyć z niezapieczętowanych klas, aby dodać wygodną składową, taką jak konstruktory niestandardowe, nowe metody lub przeciążenia metod.</span><span class="sxs-lookup"><span data-stu-id="f00dd-106">Developers often want to inherit from unsealed classes so as to add convenience members such as custom constructors, new methods, or method overloads.</span></span> <span data-ttu-id="f00dd-107">Na przykład,  `System.Messaging.MessageQueue` jest niezapieczętowany i w ten sposób umożliwia użytkownikom tworzenie kolejek niestandardowych, które są domyślne dla określonej ścieżki kolejki lub do dodawania metod niestandardowych, które upraszczają interfejs API dla konkretnych scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="f00dd-107">For example,  `System.Messaging.MessageQueue` is unsealed and thus allows users to create custom queues that default to a particular queue path or to add custom methods that simplify the API for specific scenarios.</span></span>

 <span data-ttu-id="f00dd-108">Klasy są domyślnie niezapieczętowane w większości języków programowania i jest to również zalecane domyślnie dla większości klas w strukturach.</span><span class="sxs-lookup"><span data-stu-id="f00dd-108">Classes are unsealed by default in most programming languages, and this is also the recommended default for most classes in frameworks.</span></span> <span data-ttu-id="f00dd-109">Rozszerzalność zapewniona przez niezapieczętowane typy jest znacznie doceniana przez użytkowników struktury i całkiem niedrogie, aby zapewnić z powodu stosunkowo niskich kosztów testów związanych z niezapieczętowanymi typami.</span><span class="sxs-lookup"><span data-stu-id="f00dd-109">The extensibility afforded by unsealed types is much appreciated by framework users and quite inexpensive to provide because of relatively low test costs associated with unsealed types.</span></span>

 <span data-ttu-id="f00dd-110">*Fragmenty © 2005, 2009 Microsoft Corporation. Wszelkie prawa zastrzeżone.*</span><span class="sxs-lookup"><span data-stu-id="f00dd-110">*Portions © 2005, 2009 Microsoft Corporation. All rights reserved.*</span></span>

 <span data-ttu-id="f00dd-111">*Ponownie Wydrukowano przez uprawnienie Pearson Education, Inc. z [wytycznych dotyczących projektowania platformy: konwencje, idiomy i wzorce dla bibliotek .NET do wielokrotnego użytku, 2. wydanie](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) przez Krzysztof Cwalina i Brad Abrams, opublikowane 22, 2008 przez Addison-Wesley Professional w ramach serii Microsoft Windows Development.*</span><span class="sxs-lookup"><span data-stu-id="f00dd-111">*Reprinted by permission of Pearson Education, Inc. from [Framework Design Guidelines: Conventions, Idioms, and Patterns for Reusable .NET Libraries, 2nd Edition](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) by Krzysztof Cwalina and Brad Abrams, published Oct 22, 2008 by Addison-Wesley Professional as part of the Microsoft Windows Development Series.*</span></span>

## <a name="see-also"></a><span data-ttu-id="f00dd-112">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="f00dd-112">See also</span></span>

- [<span data-ttu-id="f00dd-113">Wskazówki dotyczące projektowania struktury</span><span class="sxs-lookup"><span data-stu-id="f00dd-113">Framework Design Guidelines</span></span>](index.md)
- [<span data-ttu-id="f00dd-114">Projektowanie pod kątem rozszerzalności</span><span class="sxs-lookup"><span data-stu-id="f00dd-114">Designing for Extensibility</span></span>](designing-for-extensibility.md)
- [<span data-ttu-id="f00dd-115">Pieczętowanie</span><span class="sxs-lookup"><span data-stu-id="f00dd-115">Sealing</span></span>](sealing.md)
