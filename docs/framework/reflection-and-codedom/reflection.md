---
title: Odbicie w programie .NET
description: Odbicie przeglądowe w programie .NET. Uzyskaj informacje o załadowanych zestawach i typach zdefiniowanych w nich, takich jak klasy, interfejsy, struktury i wyliczenia.
ms.date: 03/30/2017
helpviewer_keywords:
- assemblies [.NET], reflection
- EventInfo class, reflection
- common language runtime, reflection
- FieldInfo class, reflection
- ParameterInfo class, reflection
- ConstructorInfo class, reflection
- Assembly class, reflection
- value types, reflection
- reflection, about reflection
- modules, reflection
- runtime, reflection
- Module class, reflection
- MethodInfo class, reflection
- PropertyInfo class, reflection
- type browsers
- reflection
- discovering type information at run time
- type system, reflection
ms.assetid: d1a58e7f-fb39-4d50-bf84-e3b8f9bf9775
ms.openlocfilehash: 46c67595126af2c62b28d29983775943586a0b90
ms.sourcegitcommit: 3d84eac0818099c9949035feb96bbe0346358504
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/21/2020
ms.locfileid: "86865284"
---
# <a name="reflection-in-net"></a>Odbicie w programie .NET

Klasy w <xref:System.Reflection> przestrzeni nazw, w połączeniu z <xref:System.Type?displayProperty=nameWithType> , umożliwiają uzyskanie informacji o załadowanych [zestawach](../../standard/assembly/index.md) i typach zdefiniowanych w nich, takich jak [klasy](../../standard/base-types/common-type-system.md#classes), [interfejsy](../../standard/base-types/common-type-system.md#interfaces)i typy wartości (czyli [struktury](../../standard/base-types/common-type-system.md#structures) i [wyliczenia](../../standard/base-types/common-type-system.md#enumerations)). Można również użyć odbicia do tworzenia wystąpień typów w czasie wykonywania oraz do wywoływania i uzyskiwania dostępu do nich. Aby zapoznać się z tematami dotyczącymi konkretnych aspektów odbicia, zobacz [Tematy pokrewne](#related_topics) na końcu tego omówienia.
  
Moduł ładujący [środowiska uruchomieniowego języka wspólnego](../../standard/clr.md) zarządza [domenami aplikacji](../app-domains/application-domains.md), które stanowią zdefiniowane granice wokół obiektów, które mają ten sam zakres aplikacji. Zarządzanie obejmuje ładowanie każdego zestawu do odpowiedniej domeny aplikacji i sterowanie układem pamięci hierarchii typów w ramach każdego zestawu.  
  
[Zestawy](../app-domains/index.md) zawierają moduły, moduły zawierają typy, a typy zawierają elementy członkowskie. Odbicie zawiera obiekty, które hermetyzują zestawy, moduły i typy. Możesz użyć odbicia, aby dynamicznie utworzyć wystąpienie typu, powiązać typ z istniejącym obiektem lub uzyskać typ z istniejącego obiektu. Następnie można wywołać metody typu lub uzyskać dostęp do jego pól i właściwości. Typowe zastosowania odbicia obejmują następujące elementy:  
  
- Użyj <xref:System.Reflection.Assembly> , aby definiować i ładować zestawy, ładować moduły, które są wymienione w manifeście zestawu, i zlokalizować typ z tego zestawu i utworzyć jego wystąpienie.  
  
- Służy <xref:System.Reflection.Module> do odnajdywania informacji, takich jak zestaw, który zawiera moduł i klasy w module. Można również uzyskać wszystkie metody globalne lub inne określone, nieglobalne metody zdefiniowane w module.  
  
- Służy <xref:System.Reflection.ConstructorInfo> do odnajdywania informacji, takich jak nazwa, parametry, Modyfikatory dostępu (takie jak `public` lub `private` ), oraz szczegóły implementacji (takie jak `abstract` lub `virtual` ) konstruktora. Użyj <xref:System.Type.GetConstructors%2A> metody lub, <xref:System.Type.GetConstructor%2A> <xref:System.Type> Aby wywołać określony Konstruktor.  
  
- Służy <xref:System.Reflection.MethodInfo> do odnajdywania informacji, takich jak nazwa, zwracany typ, parametry, Modyfikatory dostępu (takie jak `public` lub `private` ), oraz szczegóły implementacji (takie jak `abstract` lub `virtual` ) metody. Użyj <xref:System.Type.GetMethods%2A> metody lub, <xref:System.Type.GetMethod%2A> <xref:System.Type> Aby wywołać konkretną metodę.  
  
- Służy <xref:System.Reflection.FieldInfo> do odnajdywania informacji, takich jak nazwa, Modyfikatory dostępu (takie jak `public` lub `private` ) i szczegóły implementacji (takie jak `static` ) pola, oraz pobierania lub ustawiania wartości pól.  
  
- Służy <xref:System.Reflection.EventInfo> do odnajdywania informacji, takich jak nazwa, typ danych programu obsługi zdarzeń, atrybuty niestandardowe, typ deklarujący i typ odbicia zdarzenia oraz dodawanie lub usuwanie programów obsługi zdarzeń.  
  
- Służy <xref:System.Reflection.PropertyInfo> do odnajdywania informacji, takich jak nazwa, typ danych, typ deklarujący, typ odbicia i stan tylko do odczytu lub do zapisu właściwości, oraz do pobierania lub ustawiania wartości właściwości.  
  
- Służy <xref:System.Reflection.ParameterInfo> do odnajdywania informacji, takich jak nazwa parametru, typ danych, czy parametr jest parametrem wejściowym lub wyjściowym, oraz pozycja parametru w podpisie metody.  
  
- Służy <xref:System.Reflection.CustomAttributeData> do odnajdywania informacji o atrybutach niestandardowych podczas pracy w kontekście tylko odbicia w domenie aplikacji. <xref:System.Reflection.CustomAttributeData>umożliwia badanie atrybutów bez tworzenia wystąpień.  
  
Klasy <xref:System.Reflection.Emit> przestrzeni nazw zapewniają wyspecjalizowaną postać odbicia, która umożliwia kompilowanie typów w czasie wykonywania.  
  
Odbicie może również służyć do tworzenia aplikacji nazywanych przeglądarkami typu, które umożliwiają użytkownikom wybieranie typów, a następnie wyświetlanie informacji o tych typach.  
  
Istnieją inne zastosowania do odbicia. Kompilatory dla języków takich jak JScript używają odbicia do konstruowania tabel symboli. Klasy w <xref:System.Runtime.Serialization> przestrzeni nazw używają odbicia, aby uzyskać dostęp do danych i określić, które pola mają być utrwalane. Klasy w <xref:System.Runtime.Remoting> przestrzeni nazw używają odbicia pośrednio przy użyciu serializacji.  
  
## <a name="runtime-types-in-reflection"></a>Typy środowiska uruchomieniowego w odbiciu  
Odbicie zawiera klasy, takie jak <xref:System.Type> i <xref:System.Reflection.MethodInfo> , do reprezentowania typów, elementów członkowskich, parametrów i innych jednostek kodu. Jednak w przypadku używania odbicia nie można bezpośrednio korzystać z tych klas, z których większość jest abstrakcyjna ( `MustInherit` w Visual Basic). Zamiast tego pracujesz z typami dostarczanymi przez środowisko uruchomieniowe języka wspólnego (CLR).  
  
Na przykład w przypadku używania operatora języka C# `typeof` ( `GetType` w Visual Basic) do uzyskania obiektu obiekt <xref:System.Type> jest naprawdę a `RuntimeType` . `RuntimeType`pochodzi z <xref:System.Type> i zapewnia implementacje wszystkich metod abstrakcyjnych.  
  
Te klasy środowiska uruchomieniowego są `internal` ( `Friend` w Visual Basic). Nie są one udokumentowane niezależnie od ich klas bazowych, ponieważ ich zachowanie zostało opisane w dokumentacji klasy bazowej.  
  
<a name="related_topics"></a>

## <a name="related-topics"></a>Tematy pokrewne  
  
|Tytuł|Opis|  
|-----------|-----------------|  
|[Wyświetlanie informacji o typie](viewing-type-information.md)|Opisuje <xref:System.Type> klasę i zawiera przykłady kodu, które ilustrują sposób użycia <xref:System.Type> kilku klas odbicia w celu uzyskania informacji na temat konstruktorów, metod, pól, właściwości i zdarzeń.|  
|[Odbicie i typy ogólne](reflection-and-generic-types.md)|Wyjaśnia, jak odbicie obsługuje parametry typu i argumenty typu rodzajowego i metod ogólnych.|  
|[Zagadnienia dotyczące zabezpieczeń dla odbicia](security-considerations-for-reflection.md)|Opisuje reguły, które określają, w jakim stopniu odbicie może być używane do wykrywania informacji o typie i typów dostępu.|  
|[Dynamiczne ładowanie i używanie typów](dynamically-loading-and-using-types.md)|Opisuje interfejs powiązania niestandardowego odbicia obsługujący późne wiązanie.|  
|[Instrukcje: Ładowanie zestawów do kontekstu Reflection-Only](how-to-load-assemblies-into-the-reflection-only-context.md)|Opisuje kontekst ładowania tylko odbicie. Pokazuje, jak załadować zestaw, jak przetestować kontekst i jak sprawdzać atrybuty zastosowane do zestawu w kontekście tylko odbicie.|  
|[Uzyskiwanie dostępu do atrybutów niestandardowych](accessing-custom-attributes.md)|Demonstruje użycie odbicia w celu uzyskania atrybutu i jego wartości.|  
|[Określanie w pełni kwalifikowanych nazw typów](specifying-fully-qualified-type-names.md)|Opisuje format w pełni kwalifikowanych nazw typów w warunkach Naura (BNF) i składni wymaganej do określenia znaków specjalnych, nazw zestawów, wskaźników, odwołań i tablic.|  
|[Instrukcje: Podłączanie delegata za pomocą odbicia](how-to-hook-up-a-delegate-using-reflection.md)|Wyjaśnia, jak utworzyć delegata dla metody i podłączyć delegata do zdarzenia. Wyjaśnia, jak utworzyć metodę obsługi zdarzeń w czasie wykonywania przy użyciu <xref:System.Reflection.Emit.DynamicMethod> .|  
|[Emitowanie dynamicznych metod i zestawów](emitting-dynamic-methods-and-assemblies.md)|Wyjaśnia, jak generować dynamiczne zestawy i metody dynamiczne.|  
  
## <a name="reference"></a>Tematy pomocy  

<xref:System.Type?displayProperty=nameWithType>  
  
<xref:System.Reflection>  
  
<xref:System.Reflection.Emit>  
