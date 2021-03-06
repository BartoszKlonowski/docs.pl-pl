---
title: Jak My zależy od typu projektu
ms.date: 07/20/2015
helpviewer_keywords:
- _MYTYPE
ms.assetid: c188b38e-bd9d-4121-9983-41ea6a94d28e
ms.openlocfilehash: 740185d8030c09e8813bc7680b451f6326588593
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/04/2020
ms.locfileid: "84411717"
---
# <a name="how-my-depends-on-project-type-visual-basic"></a>Jak My zależy od typu projektu (Visual Basic)

`My`uwidacznia tylko te obiekty, które są wymagane przez określony typ projektu. Na przykład `My.Forms` obiekt jest dostępny w aplikacji Windows Forms, ale nie jest dostępny w aplikacji konsolowej. W tym temacie opisano, które `My` obiekty są dostępne w różnych typach projektów.  
  
## <a name="my-in-windows-applications-and-web-sites"></a>Moje w aplikacjach i witrynach sieci Web systemu Windows  

 `My`uwidacznia tylko obiekty, które są przydatne w bieżącym typie projektu; pomija obiekty, które nie są stosowane. Na przykład na poniższej ilustracji przedstawiono `My` model obiektów w projekcie Windows Forms.  
  
 ![Diagram pokazujący model my Object w aplikacji Windows Forms.](./media/how-my-depends-on-project-type/my-object-model-windows-forms.png)  
  
 W projekcie witryny sieci Web `My` udostępnia obiekty, które mają zastosowanie do deweloperów sieci Web (takich jak `My.Request` obiekty i `My.Response` ) przy jednoczesnym pomijaniu obiektów, które nie są istotne (takie jak `My.Forms` obiekt). Na poniższej ilustracji przedstawiono `My` model obiektów w projekcie witryny sieci Web:  
  
 ![Diagram przedstawiający mój model obiektów w aplikacji sieci Web.](./media/how-my-depends-on-project-type/my-object-model-web.png)  
  
## <a name="project-details"></a>Szczegóły projektu  

 W poniższej tabeli przedstawiono, które `My` obiekty są domyślnie włączone dla ośmiu typów projektów: aplikacji systemu Windows, biblioteki klas, aplikacji konsolowej, biblioteki formantów systemu Windows, biblioteki formantów sieci Web, usługi systemu Windows, pustej i witryny sieci Web.  
  
 Istnieją trzy wersje obiektu `My.Application` , dwie wersje `My.Computer` obiektu i dwie wersje `My.User` obiektu; szczegóły dotyczące tych wersji są podane w przypisach po tabeli.  
  
|Mój obiekt|Aplikacja systemu Windows|Biblioteka klas|Aplikacja konsoli|Biblioteka formantów systemu Windows|Biblioteka formantów sieci Web|Usługa systemu Windows|Pusty|Witryna sieci Web|  
|---|---|---|---|---|---|---|---|---|  
|`My.Application`|**Tak** <sup>1</sup>|**Tak** <sup>2</sup>|**Tak** <sup>3</sup>|**Tak** <sup>2</sup>|Nie|**Tak** <sup>3</sup>|Nie|Nie|  
|`My.Computer`|**Tak** <sup>4</sup>|**Tak** <sup>4</sup>|**Tak** <sup>4</sup>|**Tak** <sup>4</sup>|**Tak** <sup>5</sup>|**Tak** <sup>4</sup>|Nie|**Tak** <sup>5</sup>|  
|`My.Forms`|**Tak**|Nie|Nie|**Tak**|Nie|Nie|Nie|Nie|  
|`My.Log`|Nie|Nie|Nie|Nie|Nie|Nie|Nie|**Tak**|  
|`My.Request`|Nie|Nie|Nie|Nie|Nie|Nie|Nie|**Tak**|  
|`My.Resources`|**Tak**|**Tak**|**Tak**|**Tak**|**Tak**|**Tak**|Nie|Nie|  
|`My.Response`|Nie|Nie|Nie|Nie|Nie|Nie|Nie|**Tak**|  
|`My.Settings`|**Tak**|**Tak**|**Tak**|**Tak**|**Tak**|**Tak**|Nie|Nie|  
|`My.User`|**Tak** <sup>6</sup>|**Tak** <sup>6</sup>|**Tak** <sup>6</sup>|**Tak** <sup>6</sup>|**Tak** <sup>7</sup>|**Tak** <sup>6</sup>|Nie|**Tak** <sup>7</sup>|  
|`My.WebServices`|**Tak**|**Tak**|**Tak**|**Tak**|**Tak**|**Tak**|Nie|Nie|  
  
 <sup>1</sup> Windows Forms wersja programu `My.Application` . Pochodzi z wersji konsoli (patrz adnotacja 3); dodaje obsługę współpracy z oknami aplikacji i udostępnia model aplikacji Visual Basic.  
  
 <sup>2</sup> wersja biblioteki programu `My.Application` . Zapewnia podstawowe funkcje, które są konieczne przez aplikację: umożliwia członkom zapisywanie w dzienniku aplikacji i uzyskiwanie dostępu do informacji o aplikacji.  
  
 <sup>3</sup> wersja konsoli programu `My.Application` . Pochodzi z wersji biblioteki (patrz adnotacja 2) i dodaje dodatkowych członków do uzyskiwania dostępu do argumentów wiersza polecenia i informacji o wdrożeniu technologii ClickOnce.  
  
 <sup>4</sup> wersja systemu Windows `My.Computer` . Pochodzi z wersji serwera (patrz adnotacja 5) i zapewnia dostęp do przydatnych obiektów na komputerze klienckim, takich jak klawiatura, ekran i mysz.  
  
 <sup>5</sup> wersja serwera programu `My.Computer` . Zawiera podstawowe informacje o komputerze, takie jak nazwa, dostęp do zegara i tak dalej.  
  
 <sup>6</sup> wersja systemu Windows `My.User` . Ten obiekt jest skojarzony z bieżącą tożsamością wątku.  
  
 <sup>7</sup> wersja sieci Web programu `My.User` . Ten obiekt jest skojarzony z tożsamością użytkownika bieżącego żądania HTTP.  
  
## <a name="see-also"></a>Zobacz też

- <xref:Microsoft.VisualBasic.ApplicationServices.ApplicationBase>
- <xref:Microsoft.VisualBasic.Devices.Computer>
- <xref:Microsoft.VisualBasic.Logging.Log>
- <xref:Microsoft.VisualBasic.ApplicationServices.User>
- [Dostosowywanie, które obiekty są dostępne w My](../customizing-extending-my/customizing-which-objects-are-available-in-my.md)
- [Kompilacja warunkowa](../../programming-guide/program-structure/conditional-compilation.md)
- [-Definiuj (Visual Basic)](../../reference/command-line-compiler/define.md)
- [My.Forms — Obiekt](../../language-reference/objects/my-forms-object.md)
- [My.Request — Obiekt](../../language-reference/objects/my-request-object.md)
- [My.Response — Obiekt](../../language-reference/objects/my-response-object.md)
- [My.WebServices — Obiekt](../../language-reference/objects/my-webservices-object.md)
