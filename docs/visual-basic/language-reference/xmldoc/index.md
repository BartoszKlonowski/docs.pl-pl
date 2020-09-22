---
title: Zalecane tagi XML dla komentarzy do dokumentacji
ms.date: 07/20/2015
f1_keywords:
- vb.XmlDocComment
helpviewer_keywords:
- tags, XML
- XML comments, recommended tags [Visual Basic]
- comments, recommended XML tags
ms.assetid: 294e0736-ff1e-498e-af83-6db71ed41a72
ms.openlocfilehash: 9f877ee3fc9d616dc1e946293489a8aab96ac2e1
ms.sourcegitcommit: d2db216e46323f73b32ae312c9e4135258e5d68e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/22/2020
ms.locfileid: "90872791"
---
# <a name="recommended-xml-tags-for-documentation-comments-visual-basic"></a><span data-ttu-id="b7b80-102">Zalecane tagi XML dla komentarzy dokumentacji (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="b7b80-102">Recommended XML Tags for Documentation Comments (Visual Basic)</span></span>

<span data-ttu-id="b7b80-103">Kompilator Visual Basic może przetwarzać komentarze dokumentacji w kodzie do pliku XML.</span><span class="sxs-lookup"><span data-stu-id="b7b80-103">The Visual Basic compiler can process documentation comments in your code to an XML file.</span></span> <span data-ttu-id="b7b80-104">Możesz użyć dodatkowych narzędzi do przetworzenia pliku XML w dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="b7b80-104">You can use additional tools to process the XML file into documentation.</span></span>  
  
 <span data-ttu-id="b7b80-105">Komentarze XML są dozwolone w konstrukcjach kodu, takich jak typy i elementy członkowskie typu.</span><span class="sxs-lookup"><span data-stu-id="b7b80-105">XML comments are allowed on code constructs such as types and type members.</span></span> <span data-ttu-id="b7b80-106">W przypadku typów częściowych tylko jedna część typu może zawierać komentarze XML, chociaż nie ma żadnych ograniczeń dotyczących komentowania jej elementów członkowskich.</span><span class="sxs-lookup"><span data-stu-id="b7b80-106">For partial types, only one part of the type can have XML comments, although there is no restriction on commenting its members.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="b7b80-107">Komentarzy do dokumentacji nie można stosować do przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="b7b80-107">Documentation comments cannot be applied to namespaces.</span></span> <span data-ttu-id="b7b80-108">Przyczyną jest to, że jedna przestrzeń nazw może obejmować kilka zestawów, a nie wszystkie zestawy muszą być ładowane w tym samym czasie.</span><span class="sxs-lookup"><span data-stu-id="b7b80-108">The reason is that one namespace can span several assemblies, and not all assemblies have to be loaded at the same time.</span></span>  
  
 <span data-ttu-id="b7b80-109">Kompilator przetwarza dowolny tag, który jest prawidłowym kodem XML.</span><span class="sxs-lookup"><span data-stu-id="b7b80-109">The compiler processes any tag that is valid XML.</span></span> <span data-ttu-id="b7b80-110">Poniższe Tagi zapewniają powszechnie używane funkcje w dokumentacji użytkownika.</span><span class="sxs-lookup"><span data-stu-id="b7b80-110">The following tags provide commonly used functionality in user documentation.</span></span>  
  
||||  
|---|---|---|  
|[\<c>](c.md)|[\<code>](code.md)|[\<example>](example.md)|  
|<span data-ttu-id="b7b80-111">[\<exception>](exception.md)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="b7b80-111">[\<exception>](exception.md) <sup>1</sup></span></span>|<span data-ttu-id="b7b80-112">[\<include>](include.md)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="b7b80-112">[\<include>](include.md) <sup>1</sup></span></span>|[\<list>](list.md)|  
|[\<para>](para.md)|<span data-ttu-id="b7b80-113">[\<param>](param.md)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="b7b80-113">[\<param>](param.md) <sup>1</sup></span></span>|[\<paramref>](paramref.md)|  
|<span data-ttu-id="b7b80-114">[\<permission>](permission.md)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="b7b80-114">[\<permission>](permission.md) <sup>1</sup></span></span>|[\<remarks>](remarks.md)|[\<returns>](returns.md)|  
|<span data-ttu-id="b7b80-115">[\<see>](see.md)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="b7b80-115">[\<see>](see.md) <sup>1</sup></span></span>|<span data-ttu-id="b7b80-116">[\<seealso>](seealso.md)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="b7b80-116">[\<seealso>](seealso.md) <sup>1</sup></span></span>|[\<summary>](summary.md)|  
|<span data-ttu-id="b7b80-117">[\<typeparam>](typeparam.md)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="b7b80-117">[\<typeparam>](typeparam.md) <sup>1</sup></span></span>|[\<value>](value.md)||  
  
 <span data-ttu-id="b7b80-118">(<sup>1</sup> kompilator weryfikuje składnię).</span><span class="sxs-lookup"><span data-stu-id="b7b80-118">(<sup>1</sup> The compiler verifies syntax.)</span></span>  
  
> [!NOTE]
> <span data-ttu-id="b7b80-119">Jeśli chcesz, aby w tekście komentarza do dokumentacji pojawiły się nawiasy kątowe, użyj `&lt;` i `&gt;` .</span><span class="sxs-lookup"><span data-stu-id="b7b80-119">If you want angle brackets to appear in the text of a documentation comment, use `&lt;` and `&gt;`.</span></span> <span data-ttu-id="b7b80-120">Na przykład ciąg `"&lt;text in angle brackets&gt;"` będzie wyświetlany jako `<text in angle brackets>` .</span><span class="sxs-lookup"><span data-stu-id="b7b80-120">For example, the string `"&lt;text in angle brackets&gt;"` will appear as `<text in angle brackets>`.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="b7b80-121">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="b7b80-121">See also</span></span>

- [<span data-ttu-id="b7b80-122">Dokumentowanie kodu za pomocą XML</span><span class="sxs-lookup"><span data-stu-id="b7b80-122">Documenting Your Code with XML</span></span>](../../programming-guide/program-structure/documenting-your-code-with-xml.md)
- [<span data-ttu-id="b7b80-123">-doc</span><span class="sxs-lookup"><span data-stu-id="b7b80-123">-doc</span></span>](../../reference/command-line-compiler/doc.md)
- [<span data-ttu-id="b7b80-124">Instrukcje: tworzenie dokumentacji XML</span><span class="sxs-lookup"><span data-stu-id="b7b80-124">How to: Create XML Documentation</span></span>](../../programming-guide/program-structure/how-to-create-xml-documentation.md)
