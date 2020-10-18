---
title: Wartości typu „<typename1>” nie może zostać przekonwertowana na „<typename2>” (Odwołania do wielu plików)
ms.date: 07/20/2015
f1_keywords:
- vbc30961
- bc30961
helpviewer_keywords:
- BC30961
ms.assetid: 8be5aa0d-d236-4ac3-aa9c-5044f9f6562b
ms.openlocfilehash: 23c051e57014d7479d1c1c522b1a8da1ead52c19
ms.sourcegitcommit: ff5a4eb5cffbcac9521bc44a907a118cd7e8638d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/17/2020
ms.locfileid: "92161390"
---
# <a name="bc30961-value-of-type-typename1-cannot-be-converted-to-typename2-multiple-file-references"></a><span data-ttu-id="fe3eb-102">BC30961: \<typename1> nie można przekonwertować wartości typu "" na " \<typename2> " (odwołania do wielu plików)</span><span class="sxs-lookup"><span data-stu-id="fe3eb-102">BC30961: Value of type '\<typename1>' cannot be converted to '\<typename2>' (Multiple file references)</span></span>

<span data-ttu-id="fe3eb-103">\<typename1>Nie można przekonwertować wartości typu "" na " \<typename2> ".</span><span class="sxs-lookup"><span data-stu-id="fe3eb-103">Value of type '\<typename1>' cannot be converted to '\<typename2>'.</span></span> <span data-ttu-id="fe3eb-104">Niezgodność typów może być spowodowana mieszaniem odwołania do pliku " \<filepath1> " w projekcie " \<projectname1> " z odwołaniem do pliku " \<filepath2> " w projekcie " \<projectname2> ".</span><span class="sxs-lookup"><span data-stu-id="fe3eb-104">Type mismatch could be due to mixing a file reference to '\<filepath1>' in project '\<projectname1>' with a file reference to '\<filepath2>' in project '\<projectname2>'.</span></span> <span data-ttu-id="fe3eb-105">Jeśli oba zestawy są identyczne, spróbuj zastąpić te odwołania, aby oba odwołania były z tej samej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="fe3eb-105">If both assemblies are identical, try replacing these references so both references are from the same location.</span></span>

 <span data-ttu-id="fe3eb-106">W sytuacji, gdy projekt składa więcej niż jedno odwołanie do zestawu, kompilator nie może zagwarantować, że jeden typ może być konwertowany na inny.</span><span class="sxs-lookup"><span data-stu-id="fe3eb-106">In a situation where a project makes more than one file reference to an assembly, the compiler cannot guarantee that one type can be converted to another.</span></span>

 <span data-ttu-id="fe3eb-107">Każde odwołanie do pliku Określa ścieżkę i nazwę pliku wyjściowego projektu (zazwyczaj jest to plik DLL).</span><span class="sxs-lookup"><span data-stu-id="fe3eb-107">Each file reference specifies a file path and name for the output file of a project (typically a DLL file).</span></span> <span data-ttu-id="fe3eb-108">Kompilator nie może zagwarantować, że pliki wyjściowe pochodzą z tego samego źródła lub reprezentują te same wersje tego samego zestawu.</span><span class="sxs-lookup"><span data-stu-id="fe3eb-108">The compiler cannot guarantee that the output files come from the same source, or that they represent the same version of the same assembly.</span></span> <span data-ttu-id="fe3eb-109">W związku z tym nie może zagwarantować, że typy w różnych odwołaniach są tego samego typu, lub nawet że jeden z nich można przekonwertować na drugi.</span><span class="sxs-lookup"><span data-stu-id="fe3eb-109">Therefore, it cannot guarantee that the types in the different references are the same type, or even that one can be converted to the other.</span></span>

 <span data-ttu-id="fe3eb-110">Można użyć jednego odwołania do pliku, Jeśli wiesz, że zestawy, do których istnieją odwołania, mają tę samą tożsamość zestawu.</span><span class="sxs-lookup"><span data-stu-id="fe3eb-110">You can use a single file reference if you know that the referenced assemblies have the same assembly identity.</span></span> <span data-ttu-id="fe3eb-111">*Tożsamość zestawu* zawiera nazwę zestawu, wersję, klucz publiczny, jeśli istnieje, oraz kulturę.</span><span class="sxs-lookup"><span data-stu-id="fe3eb-111">The *assembly identity* includes the assembly's name, version, public key if any, and culture.</span></span> <span data-ttu-id="fe3eb-112">Te informacje jednoznacznie identyfikują zestaw.</span><span class="sxs-lookup"><span data-stu-id="fe3eb-112">This information uniquely identifies the assembly.</span></span>

 <span data-ttu-id="fe3eb-113">**Identyfikator błędu:** BC30961</span><span class="sxs-lookup"><span data-stu-id="fe3eb-113">**Error ID:** BC30961</span></span>

## <a name="to-correct-this-error"></a><span data-ttu-id="fe3eb-114">Aby poprawić ten błąd</span><span class="sxs-lookup"><span data-stu-id="fe3eb-114">To correct this error</span></span>

- <span data-ttu-id="fe3eb-115">Jeśli zestawy, do których się odwołuje, mają tę samą tożsamość zestawu, Usuń lub Zastąp jedno z odwołań do pliku, tak że istnieje tylko jedno odwołanie do pliku.</span><span class="sxs-lookup"><span data-stu-id="fe3eb-115">If the referenced assemblies have the same assembly identity, then remove or replace one of the file references so that there is only a single file reference.</span></span>

- <span data-ttu-id="fe3eb-116">Jeśli zestawy, do których się odwoływano, nie mają tej samej tożsamości zestawu, a następnie Zmień kod, tak aby nie próbował skonwertować typu w jeden do typu w drugim.</span><span class="sxs-lookup"><span data-stu-id="fe3eb-116">If the referenced assemblies do not have the same assembly identity, then change your code so that it does not attempt to convert a type in one to a type in the other.</span></span>

## <a name="see-also"></a><span data-ttu-id="fe3eb-117">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="fe3eb-117">See also</span></span>

- [<span data-ttu-id="fe3eb-118">Konwersje plików w Visual Basic</span><span class="sxs-lookup"><span data-stu-id="fe3eb-118">Type Conversions in Visual Basic</span></span>](../../programming-guide/language-features/data-types/type-conversions.md)
- [<span data-ttu-id="fe3eb-119">Zarządzanie odwołaniami w projekcie</span><span class="sxs-lookup"><span data-stu-id="fe3eb-119">Managing references in a project</span></span>](/visualstudio/ide/managing-references-in-a-project)
