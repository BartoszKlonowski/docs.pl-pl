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
<span data-ttu-id="ea5b2-101">Niezabezpieczone deserializatory są narażone na deserializacja niezaufanych danych.</span><span class="sxs-lookup"><span data-stu-id="ea5b2-101">Insecure deserializers are vulnerable when deserializing untrusted data.</span></span> <span data-ttu-id="ea5b2-102">Osoba atakująca może zmodyfikować serializowane dane w celu uwzględnienia nieoczekiwanych typów, aby wstrzyknąć obiekty ze złośliwymi efektami ubocznymi.</span><span class="sxs-lookup"><span data-stu-id="ea5b2-102">An attacker could modify the serialized data to include unexpected types to inject objects with malicious side effects.</span></span> <span data-ttu-id="ea5b2-103">Atak na niezabezpieczony Deserializator może na przykład wykonywać polecenia w podstawowym systemie operacyjnym, komunikować się przez sieć lub usuwać pliki.</span><span class="sxs-lookup"><span data-stu-id="ea5b2-103">An attack against an insecure deserializer could, for example, execute commands on the underlying operating system, communicate over the network, or delete files.</span></span>
