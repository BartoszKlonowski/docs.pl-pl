---
title: Mapowanie ograniczeń key schematu XML (XSD) na ograniczenia elementu DataSet
ms.date: 03/30/2017
ms.assetid: 22664196-f270-4ebc-a169-70e16a83dfa1
ms.openlocfilehash: b55b232faa01bf36788276caaf8bc2e97dddf697
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91172791"
---
# <a name="map-key-xml-schema-xsd-constraints-to-dataset-constraints"></a><span data-ttu-id="db41d-102">Mapowanie ograniczeń key schematu XML (XSD) na ograniczenia elementu DataSet</span><span class="sxs-lookup"><span data-stu-id="db41d-102">Map key XML Schema (XSD) Constraints to DataSet Constraints</span></span>

<span data-ttu-id="db41d-103">W schemacie można określić ograniczenie klucza dla elementu lub atrybutu przy użyciu elementu **klucza** .</span><span class="sxs-lookup"><span data-stu-id="db41d-103">In a schema, you can specify a key constraint on an element or attribute using the **key** element.</span></span> <span data-ttu-id="db41d-104">Element lub atrybut, w którym określono ograniczenie klucza, muszą mieć unikatowe wartości w dowolnym wystąpieniu schematu i nie może mieć wartości null.</span><span class="sxs-lookup"><span data-stu-id="db41d-104">The element or attribute on which a key constraint is specified must have unique values in any schema instance, and cannot have null values.</span></span>  
  
 <span data-ttu-id="db41d-105">Ograniczenie klucza jest podobne do ograniczenia UNIQUE, z tą różnicą, że kolumna, w której zdefiniowano ograniczenie klucza nie może mieć wartości null.</span><span class="sxs-lookup"><span data-stu-id="db41d-105">The key constraint is similar to the unique constraint, except that the column on which a key constraint is defined cannot have null values.</span></span>  
  
 <span data-ttu-id="db41d-106">Poniższa tabela zawiera opis atrybutów **msdata** , które można określić w elemencie **Key** .</span><span class="sxs-lookup"><span data-stu-id="db41d-106">The following table outlines the **msdata** attributes that you can specify in the **key** element.</span></span>  
  
|<span data-ttu-id="db41d-107">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="db41d-107">Attribute name</span></span>|<span data-ttu-id="db41d-108">Opis</span><span class="sxs-lookup"><span data-stu-id="db41d-108">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="db41d-109">**msdata: ConstraintName**</span><span class="sxs-lookup"><span data-stu-id="db41d-109">**msdata:ConstraintName**</span></span>|<span data-ttu-id="db41d-110">Jeśli ten atrybut jest określony, jego wartość jest używana jako nazwa ograniczenia.</span><span class="sxs-lookup"><span data-stu-id="db41d-110">If this attribute is specified, its value is used as the constraint name.</span></span> <span data-ttu-id="db41d-111">W przeciwnym razie atrybut **name** zawiera wartość nazwy ograniczenia.</span><span class="sxs-lookup"><span data-stu-id="db41d-111">Otherwise, the **name** attribute provides the value of the constraint name.</span></span>|  
|<span data-ttu-id="db41d-112">**msdata: PrimaryKey**</span><span class="sxs-lookup"><span data-stu-id="db41d-112">**msdata:PrimaryKey**</span></span>|<span data-ttu-id="db41d-113">Jeśli `PrimaryKey="true"` jest obecny, właściwość ograniczenia **IsPrimaryKey** jest ustawiona na **wartość true**, co oznacza, że jest kluczem podstawowym.</span><span class="sxs-lookup"><span data-stu-id="db41d-113">If `PrimaryKey="true"` is present, the **IsPrimaryKey** constraint property is set to **true**, thus making it a primary key.</span></span> <span data-ttu-id="db41d-114">Właściwość Column **AllowDBNull** ma wartość **false**, ponieważ klucze podstawowe nie mogą mieć wartości null.</span><span class="sxs-lookup"><span data-stu-id="db41d-114">The **AllowDBNull** column property is set to **false**, because primary keys cannot have null values.</span></span>|  
  
 <span data-ttu-id="db41d-115">W przypadku konwertowania schematu, w którym jest określone ograniczenie klucza, proces mapowania tworzy unikatowe ograniczenie dla tabeli z właściwością Column **AllowDBNull** ustawioną na **wartość false** dla każdej kolumny ograniczenia.</span><span class="sxs-lookup"><span data-stu-id="db41d-115">In converting schema in which a key constraint is specified, the mapping process creates a unique constraint on the table with the **AllowDBNull** column property set to **false** for each column in the constraint.</span></span> <span data-ttu-id="db41d-116">Właściwość **IsPrimaryKey** ograniczenia UNIQUE jest również ustawiona na **wartość false** , chyba że określono `msdata:PrimaryKey="true"` element **Key** .</span><span class="sxs-lookup"><span data-stu-id="db41d-116">The **IsPrimaryKey** property of the unique constraint is also set to **false** unless you have specified `msdata:PrimaryKey="true"` on the **key** element.</span></span> <span data-ttu-id="db41d-117">Jest to identyczne z ograniczeniami unikatowymi w schemacie, w którym `PrimaryKey="true"` .</span><span class="sxs-lookup"><span data-stu-id="db41d-117">This is identical to a unique constraint in the schema in which `PrimaryKey="true"`.</span></span>  
  
 <span data-ttu-id="db41d-118">W poniższym przykładzie schematu element **klucza** określa ograniczenie klucza elementu **CustomerID** .</span><span class="sxs-lookup"><span data-stu-id="db41d-118">In the following schema example, the **key** element specifies the key constraint on the **CustomerID** element.</span></span>  
  
```xml  
<xs:schema id="cod"  
            xmlns:xs="http://www.w3.org/2001/XMLSchema"
            xmlns:msdata="urn:schemas-microsoft-com:xml-msdata">  
  <xs:element name="Customers">  
    <xs:complexType>  
      <xs:sequence>  
        <xs:element name="CustomerID" type="xs:string" minOccurs="0" />  
        <xs:element name="CompanyName" type="xs:string" minOccurs="0" />  
       <xs:element name="Phone" type="xs:string" />  
     </xs:sequence>  
   </xs:complexType>  
 </xs:element>  
<xs:element name="MyDataSet" msdata:IsDataSet="true">  
  <xs:complexType>  
    <xs:choice maxOccurs="unbounded">  
      <xs:element ref="Customers" />  
    </xs:choice>  
  </xs:complexType>  
   <xs:key  msdata:PrimaryKey="true"  
       msdata:ConstraintName="KeyCustID"  
          name="KeyConstCustomerID" >  
     <xs:selector xpath=".//Customers" />  
     <xs:field xpath="CustomerID" />  
    </xs:key>  
 </xs:element>  
</xs:schema>
```  
  
 <span data-ttu-id="db41d-119">Element **klucza** określa, że wartości elementu podrzędnego **IDKlienta** elementu **Customers** muszą mieć unikatowe wartości i nie może zawierać wartości null.</span><span class="sxs-lookup"><span data-stu-id="db41d-119">The **key** element specifies that the values of the **CustomerID** child element of the **Customers** element must have unique values and cannot have null values.</span></span> <span data-ttu-id="db41d-120">W przypadku tłumaczenia schematu języka definicji schematu XML (XSD) proces mapowania tworzy poniższą tabelę:</span><span class="sxs-lookup"><span data-stu-id="db41d-120">In translating the XML Schema definition language (XSD) schema, the mapping process creates the following table:</span></span>  
  
```text  
Customers(CustomerID, CompanyName, Phone)  
```  
  
 <span data-ttu-id="db41d-121">Mapowanie schematu XML tworzy również **UniqueConstraint** w kolumnie **IDKlienta** , jak pokazano w poniższej tabeli <xref:System.Data.DataSet> .</span><span class="sxs-lookup"><span data-stu-id="db41d-121">The XML Schema mapping also creates a **UniqueConstraint** on the **CustomerID** column, as shown in the following <xref:System.Data.DataSet>.</span></span> <span data-ttu-id="db41d-122">(Dla uproszczenia są wyświetlane tylko odpowiednie właściwości.)</span><span class="sxs-lookup"><span data-stu-id="db41d-122">(For simplicity, only relevant properties are shown.)</span></span>  
  
```text  
      DataSetName: MyDataSet  
TableName: customers  
  ColumnName: CustomerID  
      AllowDBNull: False  
      Unique: True  
  ConstraintName: KeyCustID  
      Table: customers  
      Columns: CustomerID
      IsPrimaryKey: True  
```  
  
 <span data-ttu-id="db41d-123">W wygenerowanym **zestawie danych** Właściwość **IsPrimaryKey** elementu **UniqueConstraint** ma **wartość true** , ponieważ schemat określa `msdata:PrimaryKey="true"` element **Key** .</span><span class="sxs-lookup"><span data-stu-id="db41d-123">In the **DataSet** that is generated, the **IsPrimaryKey** property of the **UniqueConstraint** is set to **true** because the schema specifies `msdata:PrimaryKey="true"` in the **key** element.</span></span>  
  
 <span data-ttu-id="db41d-124">Wartość właściwości **ConstraintName** **UniqueConstraint** w **zestawie danych** jest wartością atrybutu **msdata: ConstraintName** określonego w elemencie **Key** w schemacie.</span><span class="sxs-lookup"><span data-stu-id="db41d-124">The value of the **ConstraintName** property of the **UniqueConstraint** in the **DataSet** is the value of the **msdata:ConstraintName** attribute specified in the **key** element in the schema.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="db41d-125">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="db41d-125">See also</span></span>

- [<span data-ttu-id="db41d-126">Mapowanie ograniczeń schematu XML (XSD) na ograniczenia elementu DataSet</span><span class="sxs-lookup"><span data-stu-id="db41d-126">Mapping XML Schema (XSD) Constraints to DataSet Constraints</span></span>](mapping-xml-schema-xsd-constraints-to-dataset-constraints.md)
- [<span data-ttu-id="db41d-127">Generowanie relacji elementu DataSet na podstawie schematu XML (XSD)</span><span class="sxs-lookup"><span data-stu-id="db41d-127">Generating DataSet Relations from XML Schema (XSD)</span></span>](generating-dataset-relations-from-xml-schema-xsd.md)
- [<span data-ttu-id="db41d-128">Omówienie ADO.NET</span><span class="sxs-lookup"><span data-stu-id="db41d-128">ADO.NET Overview</span></span>](../ado-net-overview.md)
