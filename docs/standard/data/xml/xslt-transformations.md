---
title: Przekształcenia XSLT
ms.date: 03/30/2017
ms.assetid: 202f8820-224c-494f-b61e-cd127eac6e03
ms.openlocfilehash: b87768b402f92e0e59279aab0f0062e510fda2e6
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/18/2020
ms.locfileid: "94818196"
---
# <a name="xslt-transformations"></a><span data-ttu-id="232cc-102">Przekształcenia XSLT</span><span class="sxs-lookup"><span data-stu-id="232cc-102">XSLT Transformations</span></span>
<span data-ttu-id="232cc-103">Extensible Stylesheet Language Transformation (XSLT) umożliwia przekształcanie zawartości źródłowego dokumentu XML w inny dokument, który jest inny niż format lub struktura.</span><span class="sxs-lookup"><span data-stu-id="232cc-103">The Extensible Stylesheet Language Transformation (XSLT) lets you transform the content of a source XML document into another document that is different in format or structure.</span></span> <span data-ttu-id="232cc-104">Na przykład można użyć XSLT do przekształcenia XML w HTML do użycia w witrynie sieci Web lub przekształcenia go w dokument zawierający tylko pola wymagane przez aplikację.</span><span class="sxs-lookup"><span data-stu-id="232cc-104">For example, you can use XSLT to transform XML into HTML for use on a Web site or to transform it into a document that contains only the fields required by an application.</span></span> <span data-ttu-id="232cc-105">Ten proces transformacji jest określany na podstawie [zalecenia 1,0 w formacie W3C XSL Transformation (XSLT)](https://www.w3.org/TR/xslt-10/).</span><span class="sxs-lookup"><span data-stu-id="232cc-105">This transformation process is specified by the [W3C XSL Transformations (XSLT) Version 1.0 recommendation](https://www.w3.org/TR/xslt-10/).</span></span>  
  
 <span data-ttu-id="232cc-106"><xref:System.Xml.Xsl.XslCompiledTransform>Klasa to procesor XSLT w środowisku .NET.</span><span class="sxs-lookup"><span data-stu-id="232cc-106">The <xref:System.Xml.Xsl.XslCompiledTransform> class is the XSLT processor in .NET.</span></span> <span data-ttu-id="232cc-107"><xref:System.Xml.Xsl.XslCompiledTransform>Klasa obsługuje zalecenie dotyczące [W3C XSLT 1,0](https://www.w3.org/TR/xslt-10/).</span><span class="sxs-lookup"><span data-stu-id="232cc-107">The <xref:System.Xml.Xsl.XslCompiledTransform> class supports the [W3C XSLT 1.0 recommendation](https://www.w3.org/TR/xslt-10/).</span></span>  
  
> [!NOTE]
> <span data-ttu-id="232cc-108"><xref:System.Xml.Xsl.XslTransform>Klasa jest przestarzała w .NET Framework w wersji 2,0.</span><span class="sxs-lookup"><span data-stu-id="232cc-108">The <xref:System.Xml.Xsl.XslTransform> class is obsolete in .NET Framework version 2.0.</span></span> <span data-ttu-id="232cc-109"><xref:System.Xml.Xsl.XslCompiledTransform>Klasa jest nową implementacją aparatu XSLT.</span><span class="sxs-lookup"><span data-stu-id="232cc-109">The <xref:System.Xml.Xsl.XslCompiledTransform> class is a new implementation of the XSLT engine.</span></span> <span data-ttu-id="232cc-110">Obejmuje to ulepszenia wydajności i nowe funkcje zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="232cc-110">It includes performance improvements and new security features.</span></span> <span data-ttu-id="232cc-111">Zalecanym sposobem jest utworzenie aplikacji XSLT przy użyciu <xref:System.Xml.Xsl.XslCompiledTransform> klasy.</span><span class="sxs-lookup"><span data-stu-id="232cc-111">The recommended practice is to create XSLT applications using the <xref:System.Xml.Xsl.XslCompiledTransform> class.</span></span>  
  
## <a name="in-this-section"></a><span data-ttu-id="232cc-112">W tej sekcji</span><span class="sxs-lookup"><span data-stu-id="232cc-112">In This Section</span></span>  
 [<span data-ttu-id="232cc-113">Używanie klasy XslCompiledTransform</span><span class="sxs-lookup"><span data-stu-id="232cc-113">Using the XslCompiledTransform Class</span></span>](using-the-xslcompiledtransform-class.md)  
 <span data-ttu-id="232cc-114">Zawiera informacje o korzystaniu z <xref:System.Xml.Xsl.XslCompiledTransform> klasy.</span><span class="sxs-lookup"><span data-stu-id="232cc-114">Provides information on using the <xref:System.Xml.Xsl.XslCompiledTransform> class.</span></span>  
  
 [<span data-ttu-id="232cc-115">Migrowanie z klasy XslTransform</span><span class="sxs-lookup"><span data-stu-id="232cc-115">Migrating From the XslTransform Class</span></span>](migrating-from-the-xsltransform-class.md)  
 <span data-ttu-id="232cc-116">W tym artykule omówiono sposób migrowania kodu z <xref:System.Xml.Xsl.XslTransform> klasy.</span><span class="sxs-lookup"><span data-stu-id="232cc-116">Discusses how to migrate code from the <xref:System.Xml.Xsl.XslTransform> class.</span></span>  
  
 [<span data-ttu-id="232cc-117">Kompilator XSLT (xsltc.exe)</span><span class="sxs-lookup"><span data-stu-id="232cc-117">XSLT Compiler (xsltc.exe)</span></span>](xslt-compiler-xsltc-exe.md)  
 <span data-ttu-id="232cc-118">Zawiera informacje o korzystaniu z kompilatora XSLT.</span><span class="sxs-lookup"><span data-stu-id="232cc-118">Provides information on using the XSLT compiler.</span></span>  
  
 [<span data-ttu-id="232cc-119">Przekształcenia XSLT przy użyciu klasy XslTransform</span><span class="sxs-lookup"><span data-stu-id="232cc-119">XSLT Transformations with the XslTransform Class</span></span>](xslt-transformations-with-the-xsltransform-class.md)  
 <span data-ttu-id="232cc-120">Zawiera informacje o korzystaniu z <xref:System.Xml.Xsl.XslTransform> klasy.</span><span class="sxs-lookup"><span data-stu-id="232cc-120">Provides information on using the <xref:System.Xml.Xsl.XslTransform> class.</span></span>  
  
## <a name="reference"></a><span data-ttu-id="232cc-121">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="232cc-121">Reference</span></span>  
 <xref:System.Xml.Xsl.XslCompiledTransform>  
 <xref:System.Xml.Xsl.XsltArgumentList>  
 <xref:System.Xml.Xsl.XsltSettings>  
  
## <a name="related-sections"></a><span data-ttu-id="232cc-122">Sekcje pokrewne</span><span class="sxs-lookup"><span data-stu-id="232cc-122">Related Sections</span></span>  
 [<span data-ttu-id="232cc-123">Dokumenty i dane XML</span><span class="sxs-lookup"><span data-stu-id="232cc-123">XML Documents and Data</span></span>](index.md)
