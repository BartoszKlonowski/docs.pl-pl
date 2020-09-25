---
title: Relacje i ograniczenia schematu XML
ms.date: 03/30/2017
ms.assetid: 165bc2bc-60a1-40e0-9b89-7c68ef979079
ms.openlocfilehash: 5861386e42defa189aaa50a3af0bd95d7e9257fd
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91173708"
---
# <a name="xml-schema-constraints-and-relationships"></a>Relacje i ograniczenia schematu XML

W schemacie języka definicji schematu XML (XSD) można określić ograniczenia (ograniczenia UNIQUE, Key i keyref) oraz relacje (przy użyciu adnotacji **msdata: Relationship** ). W tym temacie wyjaśniono, jak są interpretowane ograniczenia i relacje określone w schemacie XML w celu wygenerowania <xref:System.Data.DataSet> .  
  
 Ogólnie rzecz biorąc, w schemacie XML należy określić adnotację **msdata: Relationship** , jeśli chcesz wygenerować tylko relacje w **zestawie danych**. Aby uzyskać więcej informacji, zobacz [generowanie relacji zestawu danych z schematu XML (XSD)](generating-dataset-relations-from-xml-schema-xsd.md). Należy określić ograniczenia (unikatowy, klucz i keyref), jeśli chcesz wygenerować ograniczenia w **zestawie danych**. Należy zauważyć, że ograniczenia Key i keyref są również używane do generowania relacji, jak wyjaśniono w dalszej części tego tematu.  
  
## <a name="generating-a-relationship-from-key-and-keyref-constraints"></a>Generowanie relacji z ograniczeniami Key i keyref  

 Zamiast określania adnotacji **msdata: Relationship** , można określić ograniczenia Key i keyref, które są używane podczas procesu mapowania schematu XML do generowania nie tylko ograniczenia, ale również relacji w **zestawie danych**. Jeśli jednak określisz `msdata:ConstraintOnly="true"` w elemencie **keyref** , **zestaw danych** będzie zawierać tylko ograniczenia i nie będzie uwzględniać relacji.  
  
 W poniższym przykładzie przedstawiono schemat XML, który zawiera elementy **Order** i **OrderDetail** , które nie są zagnieżdżone. Schemat określa również ograniczenia klucza i elementu keyref.  
  
```xml  
<xs:schema id="MyDataSet" xmlns=""
            xmlns:xs="http://www.w3.org/2001/XMLSchema"
            xmlns:msdata="urn:schemas-microsoft-com:xml-msdata">  
  
 <xs:element name="MyDataSet" msdata:IsDataSet="true">  
  <xs:complexType>  
    <xs:choice maxOccurs="unbounded">  
      <xs:element name="OrderDetail">  
       <xs:complexType>  
         <xs:sequence>  
           <xs:element name="OrderNo" type="xs:integer" />  
           <xs:element name="ItemNo" type="xs:string" />  
         </xs:sequence>  
       </xs:complexType>  
      </xs:element>  
      <xs:element name="Order">  
        <xs:complexType>  
          <xs:sequence>  
            <xs:element name="OrderNumber" type="xs:integer" />  
            <xs:element name="EmpNumber" type="xs:integer" />  
          </xs:sequence>  
        </xs:complexType>  
      </xs:element>  
    </xs:choice>  
  </xs:complexType>  
  
  <xs:key name="OrderNumberKey"  >  
    <xs:selector xpath=".//Order" />  
    <xs:field xpath="OrderNumber" />  
  </xs:key>  
  
  <xs:keyref name="OrderNoRef" refer="OrderNumberKey">  
    <xs:selector xpath=".//OrderDetail" />  
    <xs:field xpath="OrderNo" />  
  </xs:keyref>  
 </xs:element>  
</xs:schema>  
```  
  
 **Zestaw danych** , który jest generowany podczas procesu mapowania schematu XML, zawiera tabele **Order** i **OrderDetail** . Ponadto **zestaw danych** zawiera relacje i ograniczenia. W poniższym przykładzie przedstawiono relacje i ograniczenia. Należy zauważyć, że schemat nie określa adnotacji **msdata: Relationship** ; Zamiast tego ograniczenia Key i keyref są używane do generowania relacji.  
  
```text
....ConstraintName: OrderNumberKey  
....Type: UniqueConstraint  
....Table: Order  
....Columns: OrderNumber  
....IsPrimaryKey: False  
  
....ConstraintName: OrderNoRef  
....Type: ForeignKeyConstraint  
....Table: OrderDetail  
....Columns: OrderNo  
....RelatedTable: Order  
....RelatedColumns: OrderNumber  
  
..RelationName: OrderNoRef  
..ParentTable: Order  
..ParentColumns: OrderNumber  
..ChildTable: OrderDetail  
..ChildColumns: OrderNo  
..ParentKeyConstraint: OrderNumberKey  
..ChildKeyConstraint: OrderNoRef  
..Nested: False  
```  
  
 W poprzednim przykładzie schematu elementy **Order** i **OrderDetail** nie są zagnieżdżone. W poniższym przykładzie schematu te elementy są zagnieżdżone. Jednak nie **msdata:** adnotacja relacji jest określona; w związku z tym założono niejawną relację. Aby uzyskać więcej informacji, zobacz [Mapowanie niejawnych relacji między zagnieżdżonymi elementami schematu](map-implicit-relations-between-nested-schema-elements.md). Schemat określa również ograniczenia klucza i elementu keyref.  
  
```xml  
<xs:schema id="MyDataSet" xmlns=""
            xmlns:xs="http://www.w3.org/2001/XMLSchema"
            xmlns:msdata="urn:schemas-microsoft-com:xml-msdata">  
  
 <xs:element name="MyDataSet" msdata:IsDataSet="true">  
  <xs:complexType>  
    <xs:choice maxOccurs="unbounded">  
  
      <xs:element name="Order">  
        <xs:complexType>  
          <xs:sequence>  
            <xs:element name="OrderNumber" type="xs:integer" />  
            <xs:element name="EmpNumber" type="xs:integer" />  
  
            <xs:element name="OrderDetail">  
              <xs:complexType>  
                <xs:sequence>  
                  <xs:element name="OrderNo" type="xs:integer" />  
                  <xs:element name="ItemNo" type="xs:string" />  
                </xs:sequence>  
              </xs:complexType>  
            </xs:element>  
          </xs:sequence>  
        </xs:complexType>  
      </xs:element>  
    </xs:choice>  
  </xs:complexType>  
  
  <xs:key name="OrderNumberKey"  >  
    <xs:selector xpath=".//Order" />  
    <xs:field xpath="OrderNumber" />  
  </xs:key>  
  
  <xs:keyref name="OrderNoRef" refer="OrderNumberKey">  
    <xs:selector xpath=".//OrderDetail" />  
    <xs:field xpath="OrderNo" />  
  </xs:keyref>  
 </xs:element>  
</xs:schema>  
```  
  
 **Zestaw danych** wynikający z procesu mapowania schematu XML obejmuje dwie tabele:  
  
```text  
Order(OrderNumber, EmpNumber, Order_Id)  
OrderDetail(OrderNumber, ItemNumber, Order_Id)  
```  
  
 **Zestaw danych** zawiera również dwie relacje (jedna oparta na **msdata:** adnotacja relacji i inne na podstawie ograniczeń klucza i elementu keyref) i różne ograniczenia. W poniższym przykładzie przedstawiono relacje i ograniczenia.  
  
```text
..RelationName: Order_OrderDetail  
..ParentTable: Order  
..ParentColumns: Order_Id  
..ChildTable: OrderDetail  
..ChildColumns: Order_Id  
..ParentKeyConstraint: Constraint1  
..ChildKeyConstraint: Order_OrderDetail  
..Nested: True  
  
..RelationName: OrderNoRef  
..ParentTable: Order  
..ParentColumns: OrderNumber  
..ChildTable: OrderDetail  
..ChildColumns: OrderNo  
..ParentKeyConstraint: OrderNumberKey  
..ChildKeyConstraint: OrderNoRef  
..Nested: False  
  
..ConstraintName: OrderNumberKey  
..Type: UniqueConstraint  
..Table: Order  
..Columns: OrderNumber  
..IsPrimaryKey: False  
  
..ConstraintName: Constraint1  
..Type: UniqueConstraint  
..Table: Order  
..Columns: Order_Id  
..IsPrimaryKey: True  
  
..ConstraintName: Order_OrderDetail  
..Type: ForeignKeyConstraint  
..Table: OrderDetail  
..Columns: Order_Id  
..RelatedTable: Order  
..RelatedColumns: Order_Id  
  
..ConstraintName: OrderNoRef  
..Type: ForeignKeyConstraint  
..Table: OrderDetail  
..Columns: OrderNo  
..RelatedTable: Order  
..RelatedColumns: OrderNumber  
```  
  
 Jeśli ograniczenie elementu keyref odwołujące się do zagnieżdżonej tabeli zawiera adnotację **msdata: Isnested = "true"** , **zestaw danych** utworzy pojedynczą relację zagnieżdżoną opartą na ograniczeniu keyref i powiązanym ograniczeniu UNIQUE/Key.  
  
## <a name="see-also"></a>Zobacz też

- [Pobieranie relacyjnej struktury elementu DataSet ze schematu XML (XSD)](deriving-dataset-relational-structure-from-xml-schema-xsd.md)
- [Omówienie ADO.NET](../ado-net-overview.md)
