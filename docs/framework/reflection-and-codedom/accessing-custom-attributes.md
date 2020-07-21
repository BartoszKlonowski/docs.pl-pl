---
title: Uzyskiwanie dostępu do atrybutów niestandardowych
description: Dostęp do atrybutów niestandardowych w programie .NET. Po skojarzeniu atrybutów z elementami programu można użyć odbicia, aby zbadać ich istnienie i wartości.
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- custom attributes, accessibility
- attributes [.NET Framework], accessing
- reflection, custom attributes
ms.assetid: 1d8e3398-00d8-47d5-a084-214f9859d3d7
ms.openlocfilehash: 1197fc5149e144d293deda1173e82ca2dadeda7d
ms.sourcegitcommit: cf5a800a33de64d0aad6d115ffcc935f32375164
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/20/2020
ms.locfileid: "86475141"
---
# <a name="accessing-custom-attributes"></a>Uzyskiwanie dostępu do atrybutów niestandardowych
Po skojarzeniu atrybutów z elementami programu odbicie może służyć do wykonywania zapytań o ich istnienie i wartości. W .NET Framework w wersji 1,0 i 1,1 atrybuty niestandardowe są badane w kontekście wykonania. .NET Framework w wersji 2,0 udostępnia nowy kontekst ładowania, kontekst tylko odbicia, który może służyć do badania kodu, którego nie można załadować do wykonania.  
  
## <a name="the-reflection-only-context"></a>Kontekst tylko odbicie  
 Nie można wykonać kodu załadowanego do kontekstu tylko odbicie. Oznacza to, że nie można utworzyć wystąpień atrybutów niestandardowych, ponieważ wymagałoby to wykonania konstruktorów. Aby załadować i przejrzeć atrybuty niestandardowe w kontekście tylko odbicia, użyj <xref:System.Reflection.CustomAttributeData> klasy. Wystąpienia tej klasy można uzyskać przy użyciu odpowiedniego przeciążenia metody statycznej <xref:System.Reflection.CustomAttributeData.GetCustomAttributes%2A?displayProperty=nameWithType> . Zobacz [instrukcje: ładowanie zestawów do kontekstu tylko odbicie](how-to-load-assemblies-into-the-reflection-only-context.md).  
  
## <a name="the-execution-context"></a>Kontekst wykonywania  
 Główne metody odbicia w celu zbadania atrybutów w kontekście wykonywania są <xref:System.Reflection.MemberInfo.GetCustomAttributes%2A?displayProperty=nameWithType> i <xref:System.Attribute.GetCustomAttributes%2A?displayProperty=nameWithType> .  
  
 Dostępność atrybutu niestandardowego jest sprawdzana w odniesieniu do zestawu, w którym jest dołączony. Jest to równoznaczne z sprawdzeniem, czy metoda na typie w zestawie, do którego jest dołączony atrybut niestandardowy, może wywołać konstruktora atrybutu niestandardowego.  
  
 Metody, takie jak <xref:System.Reflection.Assembly.GetCustomAttributes%28System.Boolean%29?displayProperty=nameWithType> Sprawdzanie widoczności i dostępności argumentu typu. Tylko kod w zestawie, który zawiera typ zdefiniowany przez użytkownika, może pobrać atrybut niestandardowy tego typu za pomocą **GetCustomAttributes —**.  
  
 Poniższy przykład kodu w języku C# jest typowym wzorcem projektowania atrybutów niestandardowych. Ilustruje on model odbicia niestandardowego atrybutu środowiska uruchomieniowego.  
  
```csharp
System.DLL  
public class DescriptionAttribute : Attribute  
{  
}  
  
System.Web.DLL  
internal class MyDescriptionAttribute : DescriptionAttribute  
{  
}  
  
public class LocalizationExtenderProvider  
{  
    [MyDescriptionAttribute(...)]  
    public CultureInfo GetLanguage(...)  
    {  
    }  
}  
```  
  
 Jeśli środowisko uruchomieniowe próbuje pobrać atrybuty niestandardowe dla publicznego typu atrybutu niestandardowego <xref:System.ComponentModel.DescriptionAttribute> dołączonego do metody **GetLanguage** , wykonuje następujące czynności:  
  
1. Środowisko uruchomieniowe sprawdza, czy argument typu **DescriptionAttribute** do **typu. GetCustomAttributes —**( *Typ typu) jest*publiczny i dlatego jest widoczny i dostępny.  
  
2. Środowisko uruchomieniowe sprawdza, czy zdefiniowany przez użytkownika typ **WebDescriptionAttribute** , który pochodzi od **DescriptionAttribute** , jest widoczny i dostępny w ramach zestawu **System.Web.DLL** , do którego jest dołączany do metody **GetLanguage**().  
  
3. Środowisko uruchomieniowe sprawdza, czy Konstruktor elementu **WebDescriptionAttribute** jest widoczny i dostępny w ramach zestawu **System.Web.DLL** .  
  
4. Środowisko uruchomieniowe wywołuje konstruktora elementu **WebDescriptionAttribute** z parametrami atrybutu niestandardowego i zwraca nowy obiekt do obiektu wywołującego.  
  
 Model odbicia atrybutów niestandardowych może wyciekować wystąpienia typów zdefiniowanych przez użytkownika poza zestawem, w którym jest zdefiniowany typ. Nie różni się to od elementów członkowskich w bibliotece systemowej środowiska uruchomieniowego, które zwracają wystąpienia typów zdefiniowanych przez użytkownika, takich jak <xref:System.Type.GetMethods%2A?displayProperty=nameWithType> zwracanie tablicy obiektów **RuntimeMethodInfo** . Aby zapobiec odnajdywaniu przez klienta informacji o typie atrybutu niestandardowego zdefiniowanym przez użytkownika, należy zdefiniować członków typu jako niepubliczny.  
  
 Poniższy przykład ilustruje podstawowy sposób używania odbicia w celu uzyskania dostępu do atrybutów niestandardowych.  
  
 [!code-cpp[CustomAttributeData#2](../../../samples/snippets/cpp/VS_Snippets_CLR/CustomAttributeData/CPP/source2.cpp#2)]
 [!code-csharp[CustomAttributeData#2](../../../samples/snippets/csharp/VS_Snippets_CLR/CustomAttributeData/CS/source2.cs#2)]
 [!code-vb[CustomAttributeData#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CustomAttributeData/VB/source2.vb#2)]  
  
## <a name="see-also"></a>Zobacz także

- <xref:System.Reflection.MemberInfo.GetCustomAttributes%2A?displayProperty=nameWithType>
- <xref:System.Attribute.GetCustomAttributes%2A?displayProperty=nameWithType>
- [Wyświetlanie informacji o typie](viewing-type-information.md)
- [Zagadnienia dotyczące zabezpieczeń dla odbicia](security-considerations-for-reflection.md)
