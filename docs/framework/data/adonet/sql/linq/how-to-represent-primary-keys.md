---
title: 'Instrukcje: Reprezentacja kluczy podstawowych'
ms.date: 03/30/2017
ms.assetid: 63c65289-6539-42b2-8493-891c232018fa
ms.openlocfilehash: 02570176c8aef5cfdc7ba09fd6976f430900e8df
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91166238"
---
# <a name="how-to-represent-primary-keys"></a><span data-ttu-id="40116-102">Instrukcje: Reprezentacja kluczy podstawowych</span><span class="sxs-lookup"><span data-stu-id="40116-102">How to: Represent Primary Keys</span></span>

<span data-ttu-id="40116-103">Użyj [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] <xref:System.Data.Linq.Mapping.ColumnAttribute.IsPrimaryKey%2A> właściwości w atrybucie, <xref:System.Data.Linq.Mapping.ColumnAttribute> Aby wyznaczyć właściwość lub pole reprezentujące klucz podstawowy dla kolumny bazy danych.</span><span class="sxs-lookup"><span data-stu-id="40116-103">Use the [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] <xref:System.Data.Linq.Mapping.ColumnAttribute.IsPrimaryKey%2A> property on the <xref:System.Data.Linq.Mapping.ColumnAttribute> attribute to designate a property or field to represent the primary key for a database column.</span></span>  
  
 <span data-ttu-id="40116-104">Aby zapoznać się z przykładami kodu, zobacz <xref:System.Data.Linq.Mapping.ColumnAttribute.IsPrimaryKey%2A> .</span><span class="sxs-lookup"><span data-stu-id="40116-104">For code examples, see <xref:System.Data.Linq.Mapping.ColumnAttribute.IsPrimaryKey%2A>.</span></span>  
  
> [!NOTE]
> [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] <span data-ttu-id="40116-105">Program nie obsługuje kolumn obliczanych jako kluczy podstawowych.</span><span class="sxs-lookup"><span data-stu-id="40116-105">does not support computed columns as primary keys.</span></span>  
  
### <a name="to-designate-a-property-or-field-as-a-primary-key"></a><span data-ttu-id="40116-106">Aby wyznaczyć właściwość lub pole jako klucz podstawowy</span><span class="sxs-lookup"><span data-stu-id="40116-106">To designate a property or field as a primary key</span></span>  
  
1. <span data-ttu-id="40116-107">Dodaj <xref:System.Data.Linq.Mapping.ColumnAttribute.IsPrimaryKey%2A> Właściwość do <xref:System.Data.Linq.Mapping.ColumnAttribute> atrybutu.</span><span class="sxs-lookup"><span data-stu-id="40116-107">Add the <xref:System.Data.Linq.Mapping.ColumnAttribute.IsPrimaryKey%2A> property to the <xref:System.Data.Linq.Mapping.ColumnAttribute> attribute.</span></span>  
  
2. <span data-ttu-id="40116-108">Określ wartość jako `true` .</span><span class="sxs-lookup"><span data-stu-id="40116-108">Specify the value as `true`.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="40116-109">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="40116-109">See also</span></span>

- [<span data-ttu-id="40116-110">Model obiektu LINQ to SQL</span><span class="sxs-lookup"><span data-stu-id="40116-110">The LINQ to SQL Object Model</span></span>](the-linq-to-sql-object-model.md)
- [<span data-ttu-id="40116-111">Instrukcje: Dostosowywanie klas jednostek za pomocą edytora kodu</span><span class="sxs-lookup"><span data-stu-id="40116-111">How to: Customize Entity Classes by Using the Code Editor</span></span>](how-to-customize-entity-classes-by-using-the-code-editor.md)
