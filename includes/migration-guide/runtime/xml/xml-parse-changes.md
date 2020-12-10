---
ms.openlocfilehash: dfa8235fcfd868b80d3a610bddb492899519e289
ms.sourcegitcommit: 81f1bba2c97a67b5ca76bcc57b37333ffca60c7b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/10/2020
ms.locfileid: "97009071"
---
### <a name="xml-parsing-changes"></a>Zmiany analizy XML

| Nazwa    | Wartość   |
|:--------|:--------|
| Zakres   | Mały   |
| Wersja | 4.5.2   |
| Typ    | Środowisko uruchomieniowe |

#### <a name="details"></a>Szczegóły

Ze względów bezpieczeństwa wprowadzono następujące zmiany w interfejsach API analizy XML:

- <xref:System.Xml.XmlReaderSettings.MaxCharactersFromEntities?displayProperty=nameWithType> jest ustawiony na 10 000 000, gdy <xref:System.Xml.XmlReaderSettings> jest zainicjowany.
- <xref:System.Xml.XmlReaderSettings.XmlResolver?displayProperty=nameWithType> jest domyślnie ustawiony na wartość `null` .

> [!NOTE]
> <xref:System.Xml.XmlReaderSettings> jest używany przez wszystkie parsery XML, więc podczas gdy ta zmiana pomaga w <xref:System.Xml.XmlReader> przypadku, ma także wpływ na inne scenariusze.

#### <a name="suggestion"></a>Sugestia

Aby przywrócić poprzednie zachowanie, można ustawić wartość w rejestrze. Dodaj wartość DWORD o nazwie `EnableLegacyXmlSettings` do `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\XML` klucza rejestru i ustaw jej wartość na `1` . Zamiast tego można także dodać wartość rejestru do HKEY_CURRENT_USER Hive.

#### <a name="affected-apis"></a>Dotyczy interfejsów API

- <xref:System.Xml.XmlReaderSettings.MaxCharactersFromEntities?displayProperty=fullName>
- <xref:System.Xml.XmlReaderSettings.XmlResolver?displayProperty=fullName>

Ponadto dotyczy to wszystkich interfejsów API XML, które są zależne od <xref:System.Xml.XmlResolver> programu (bezpośrednio lub pośrednio).

<!--

#### Affected APIs

- `P:System.Xml.XmlReaderSettings.MaxCharactersFromEntities`
- `P:System.Xml.XmlReaderSettings.XmlResolver`

-->
