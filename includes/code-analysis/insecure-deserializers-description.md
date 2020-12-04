---
author: dotpaul
ms.author: paulming
ms.date: 04/05/2019
ms.topic: include
ms.openlocfilehash: 9235f1bcda7529b71aef542d3a49da08a9d4b59e
ms.sourcegitcommit: c04535ad05e374fb269fcfc6509217755fbc0d54
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/25/2020
ms.locfileid: "96586681"
---
Niezabezpieczone deserializatory są narażone na deserializacja niezaufanych danych. Osoba atakująca może zmodyfikować serializowane dane w celu uwzględnienia nieoczekiwanych typów, aby wstrzyknąć obiekty ze złośliwymi efektami ubocznymi. Atak na niezabezpieczony Deserializator może na przykład wykonywać polecenia w podstawowym systemie operacyjnym, komunikować się przez sieć lub usuwać pliki.
