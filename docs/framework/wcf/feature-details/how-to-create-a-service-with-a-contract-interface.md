---
title: 'Instrukcje: tworzenie usługi przy użyciu interfejsu kontraktu'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 7b6803f6-d6f9-4cc2-9f1b-6f4c920475d5
ms.openlocfilehash: 2234e6fe8d0ee2e0029a061ba96ef84f840f0c9b
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96286347"
---
# <a name="how-to-create-a-service-with-a-contract-interface"></a>Instrukcje: tworzenie usługi przy użyciu interfejsu kontraktu

Preferowanym sposobem utworzenia kontraktu Windows Communication Foundation (WCF) jest użycie interfejsu. Ta umowa określa zbieranie i strukturę komunikatów wymaganych do uzyskania dostępu do operacji oferowanych przez usługę. Ten interfejs definiuje typy wejściowe i wyjściowe przez zastosowanie <xref:System.ServiceModel.ServiceContractAttribute> klasy do interfejsu i <xref:System.ServiceModel.OperationContractAttribute> klasy do metod, które mają zostać ujawnione.  
  
 Aby uzyskać więcej informacji na temat umów dotyczących usług, zobacz [Projektowanie kontraktów usług](../designing-service-contracts.md).  
  
### <a name="creating-a-wcf-contract-with-an-interface"></a>Tworzenie kontraktu WCF z interfejsem  
  
1. Utwórz nowy interfejs przy użyciu Visual Basic, C# lub dowolnego innego języka środowiska uruchomieniowego języka wspólnego.  
  
2. Zastosuj <xref:System.ServiceModel.ServiceContractAttribute> klasę do interfejsu.  
  
3. Zdefiniuj metody w interfejsie.  
  
4. Zastosuj <xref:System.ServiceModel.OperationContractAttribute> klasę do każdej metody, która musi być ujawniona w ramach publicznego kontraktu WCF.  
  
## <a name="example"></a>Przykład  

 Poniższy przykład kodu przedstawia interfejs, który definiuje kontrakt usługi.  
  
 [!code-csharp[c_HowTo_CreateContractWithInterface#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_createcontractwithinterface/cs/source.cs#1)]
 [!code-vb[c_HowTo_CreateContractWithInterface#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_createcontractwithinterface/vb/source.vb#1)]  
  
 Metody, do których <xref:System.ServiceModel.OperationContractAttribute> zastosowano klasę, domyślnie używają wzorca komunikatów żądanie-odpowiedź. Aby uzyskać więcej informacji na temat tego wzorca wiadomości, zobacz [How to: Create a Request-Reply Contract](how-to-create-a-request-reply-contract.md). Można również tworzyć i używać innych wzorców komunikatów przez ustawienie właściwości atrybutu. Aby uzyskać więcej przykładów, zobacz [How to: Create a One-Way Contract](how-to-create-a-one-way-contract.md) i [How to: Create a Duplex kontraktu](how-to-create-a-duplex-contract.md).  
  
## <a name="see-also"></a>Zobacz też

- <xref:System.ServiceModel.ServiceContractAttribute>
- <xref:System.ServiceModel.OperationContractAttribute>
