---
title: Typ „<typename>” nie jest zdefiniowany
ms.date: 07/20/2015
f1_keywords:
- vbc30002
- bc30002
helpviewer_keywords:
- BC30002
ms.assetid: b0faf204-57fd-44de-8c05-9db027eea663
ms.openlocfilehash: 195e749e29494d438dbd052e8e308250f4cce1ca
ms.sourcegitcommit: ff5a4eb5cffbcac9521bc44a907a118cd7e8638d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/17/2020
ms.locfileid: "92161897"
---
# <a name="bc30002-type-typename-is-not-defined"></a><span data-ttu-id="ad0ff-102">BC30002: \<typename> nie zdefiniowano typu ""</span><span class="sxs-lookup"><span data-stu-id="ad0ff-102">BC30002: Type '\<typename>' is not defined</span></span>

<span data-ttu-id="ad0ff-103">Instrukcja utworzyła odwołanie do typu, który nie został zdefiniowany.</span><span class="sxs-lookup"><span data-stu-id="ad0ff-103">The statement has made reference to a type that has not been defined.</span></span> <span data-ttu-id="ad0ff-104">Można zdefiniować typ w instrukcji deklaracji, takiej jak,, `Enum` `Structure` `Class` , lub `Interface` .</span><span class="sxs-lookup"><span data-stu-id="ad0ff-104">You can define a type in a declaration statement such as `Enum`, `Structure`, `Class`, or `Interface`.</span></span>

 <span data-ttu-id="ad0ff-105">**Identyfikator błędu:** BC30002</span><span class="sxs-lookup"><span data-stu-id="ad0ff-105">**Error ID:** BC30002</span></span>

## <a name="to-correct-this-error"></a><span data-ttu-id="ad0ff-106">Aby poprawić ten błąd</span><span class="sxs-lookup"><span data-stu-id="ad0ff-106">To correct this error</span></span>

- <span data-ttu-id="ad0ff-107">Upewnij się, że definicja typu i jego odwołanie używają tej samej pisowni.</span><span class="sxs-lookup"><span data-stu-id="ad0ff-107">Ensure that the type definition and its reference both use the same spelling.</span></span>

- <span data-ttu-id="ad0ff-108">Upewnij się, że definicja typu jest dostępna dla odwołania.</span><span class="sxs-lookup"><span data-stu-id="ad0ff-108">Ensure that the type definition is accessible to the reference.</span></span> <span data-ttu-id="ad0ff-109">Na przykład, jeśli typ znajduje się w innym module i został zadeklarowany `Private` , Przenieś definicję typu do modułu odwołującego lub Zadeklaruj go `Public` .</span><span class="sxs-lookup"><span data-stu-id="ad0ff-109">For example, if the type is in another module and has been declared `Private`, move the type definition to the referencing module or declare it `Public`.</span></span>

- <span data-ttu-id="ad0ff-110">Upewnij się, że przestrzeń nazw typu nie jest ponownie zdefiniowana w ramach projektu.</span><span class="sxs-lookup"><span data-stu-id="ad0ff-110">Ensure that the namespace of the type is not redefined within your project.</span></span> <span data-ttu-id="ad0ff-111">Jeśli jest, użyj `Global` słowa kluczowego, aby w pełni zakwalifikować nazwę typu.</span><span class="sxs-lookup"><span data-stu-id="ad0ff-111">If it is, use the `Global` keyword to fully qualify the type name.</span></span> <span data-ttu-id="ad0ff-112">Na przykład jeśli projekt definiuje przestrzeń nazw o nazwie `System` , nie można <xref:System.Object?displayProperty=nameWithType> uzyskać dostępu do typu, chyba że jest on w pełni kwalifikowany za pomocą `Global` słowa kluczowego: `Global.System.Object` .</span><span class="sxs-lookup"><span data-stu-id="ad0ff-112">For example, if a project defines a namespace named `System`, the <xref:System.Object?displayProperty=nameWithType> type cannot be accessed unless it is fully qualified with the `Global` keyword: `Global.System.Object`.</span></span>

- <span data-ttu-id="ad0ff-113">Jeśli typ jest zdefiniowany, ale Biblioteka obiektów lub biblioteka typów, w której jest zdefiniowana, nie jest zarejestrowana w Visual Basic, kliknij przycisk **Dodaj odwołanie** w menu **projekt** , a następnie wybierz odpowiednią bibliotekę obiektów lub bibliotekę typów.</span><span class="sxs-lookup"><span data-stu-id="ad0ff-113">If the type is defined, but the object library or type library in which it is defined is not registered in Visual Basic, click **Add Reference** on the **Project** menu, and then select the appropriate object library or type library.</span></span>

- <span data-ttu-id="ad0ff-114">Upewnij się, że typ znajduje się w zestawie, który jest częścią profilowania .NET Framework profilu.</span><span class="sxs-lookup"><span data-stu-id="ad0ff-114">Ensure that the type is in an assembly that is part of the targeted .NET Framework profile.</span></span> <span data-ttu-id="ad0ff-115">Aby uzyskać więcej informacji, zobacz [Rozwiązywanie problemów .NET Framework określania błędów](/visualstudio/msbuild/troubleshooting-dotnet-framework-targeting-errors).</span><span class="sxs-lookup"><span data-stu-id="ad0ff-115">For more information, see [Troubleshooting .NET Framework Targeting Errors](/visualstudio/msbuild/troubleshooting-dotnet-framework-targeting-errors).</span></span>

## <a name="see-also"></a><span data-ttu-id="ad0ff-116">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="ad0ff-116">See also</span></span>

- [<span data-ttu-id="ad0ff-117">Przestrzenie nazw w Visual Basic</span><span class="sxs-lookup"><span data-stu-id="ad0ff-117">Namespaces in Visual Basic</span></span>](../../programming-guide/program-structure/namespaces.md)
- [<span data-ttu-id="ad0ff-118">Enum, instrukcja</span><span class="sxs-lookup"><span data-stu-id="ad0ff-118">Enum Statement</span></span>](../statements/enum-statement.md)
- [<span data-ttu-id="ad0ff-119">Structure — Instrukcja</span><span class="sxs-lookup"><span data-stu-id="ad0ff-119">Structure Statement</span></span>](../statements/structure-statement.md)
- [<span data-ttu-id="ad0ff-120">Class, instrukcja</span><span class="sxs-lookup"><span data-stu-id="ad0ff-120">Class Statement</span></span>](../statements/class-statement.md)
- [<span data-ttu-id="ad0ff-121">Interface, instrukcja</span><span class="sxs-lookup"><span data-stu-id="ad0ff-121">Interface Statement</span></span>](../statements/interface-statement.md)
- [<span data-ttu-id="ad0ff-122">Zarządzanie odwołaniami w projekcie</span><span class="sxs-lookup"><span data-stu-id="ad0ff-122">Managing references in a project</span></span>](/visualstudio/ide/managing-references-in-a-project)
