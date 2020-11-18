---
title: Rozszerzanie metadanych za pomocą atrybutów
description: Dowiedz się, jak zwiększyć liczbę metadanych przy użyciu atrybutów w programie .NET. Atrybuty są opisowymi deklaracjami słów kluczowych, aby dodawać adnotacje do elementów programowania, takich jak typy i pola.
ms.date: 10/14/2020
helpviewer_keywords:
- metadata, extending
- attributes [.NET], metadata
- elements [.NET], attributes
- common language runtime, attributes
- annotating programming elements
- keyword-like descriptive declarations
- runtime, attributes
- extending metadata
ms.assetid: 30386922-1e00-4602-9ebf-526b271a8b87
ms.openlocfilehash: e41299b83ae451117ab6829eee928b0d2306be19
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/18/2020
ms.locfileid: "94829079"
---
# <a name="extend-metadata-using-attributes"></a>Rozszerzanie metadanych przy użyciu atrybutów

Środowisko uruchomieniowe języka wspólnego umożliwia dodawanie opisowych deklaracji słów kluczowych, takich jak atrybuty, do elementów programistycznych, takich jak typy, pola, metody i właściwości. Podczas kompilowania kodu środowiska uruchomieniowego jest on konwertowany do języka pośredniego firmy Microsoft (MSIL) i umieszczony wewnątrz przenośnego pliku wykonywalnego (PE) wraz z metadanymi generowanymi przez kompilator. Atrybuty umożliwiają umieszczanie w metadanych dodatkowych informacji opisowych, które można wyodrębnić przy użyciu usług odbicia środowiska uruchomieniowego. Kompilator tworzy atrybuty przy deklarowaniu wystąpień klas specjalnych, które pochodzą z <xref:System.Attribute?displayProperty=nameWithType> .

Platforma .NET używa atrybutów z różnych powodów i rozwiązywania wielu problemów. Atrybuty opisują sposób serializacji danych, określają cechy, które są używane do wymuszania zabezpieczeń i ograniczają optymalizacje przez kompilator just-in-Time (JIT), dzięki czemu kod pozostaje łatwy do debugowania. Atrybuty mogą również rejestrować nazwę pliku lub autora kodu lub kontrolować widoczność formantów i członków podczas opracowywania formularzy.

## <a name="related-articles"></a>Pokrewne artykuły:

|Tytuł|Opis|
|-----------|-----------------|
|[Stosowanie atrybutów](applying-attributes.md)|Opisuje sposób zastosowania atrybutu do elementu kodu.|
|[Wpisywanie atrybutów niestandardowych](writing-custom-attributes.md)|Opisuje sposób projektowania klas atrybutów niestandardowych.|
|[Pobieranie informacji przechowywanych w atrybutach](retrieving-information-stored-in-attributes.md)|Opisuje sposób pobierania atrybutów niestandardowych dla kodu, który jest ładowany do kontekstu wykonywania.|
|[Metadane i składniki Self-Describing](../metadata-and-self-describing-components.md)|Zawiera omówienie metadanych i opis sposobu ich implementacji w przenośnym pliku wykonywalnym (PE) platformy .NET.|
|[Instrukcje: Ładowanie zestawów do kontekstu Reflection-Only](../../framework/reflection-and-codedom/how-to-load-assemblies-into-the-reflection-only-context.md)|Wyjaśnia, jak pobrać informacje o atrybutach niestandardowych w kontekście tylko odbicia.|

## <a name="reference"></a>Tematy pomocy

- <xref:System.Attribute?displayProperty=nameWithType>
