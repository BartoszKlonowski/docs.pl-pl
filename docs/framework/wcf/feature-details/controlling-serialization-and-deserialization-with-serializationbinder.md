---
title: Kontrolowanie serializacji i deserializacji za pomocą elementu SerializationBinder
ms.date: 07/14/2020
ms.assetid: ba8dcecf-acc7-467c-939d-021bbac797d4
ms.openlocfilehash: be4068411e2154db53a9616df6cf4d83803954e6
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96293744"
---
# <a name="controlling-serialization-and-deserialization-with-serializationbinder"></a>Kontrolowanie serializacji i deserializacji za pomocą elementu SerializationBinder

> [!WARNING]
> <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> nie jest zabezpieczony i ***nie*** może być zabezpieczony. Aby uzyskać więcej informacji, zobacz [Przewodnik po zabezpieczeniach BinaryFormatter](../../../standard/serialization/binaryformatter-security-guide.md).

Podczas serializacji, program formatujący przesyła informacje wymagane do utworzenia wystąpienia obiektu o poprawnym typie i wersji. Te informacje zazwyczaj obejmują pełną nazwę typu i nazwę zestawu obiektu. Domyślnie deserializacja używa tych informacji do utworzenia wystąpienia identycznego obiektu. Niektórzy użytkownicy mogą potrzebować kontroli klasy do serializacji i deserializacji, ponieważ oryginalna Klasa może nie istnieć na maszynie wykonującej deserializacji, Oryginalna klasa została przeniesiona między zestawami lub na serwerze i kliencie musi być wymagana inna wersja klasy. Aby uzyskać więcej informacji, zobacz [użycie spinacza serializacji](../samples/usage-of-serialization-binder.md).  
  
> [!WARNING]
> Ta funkcja jest dostępna tylko w przypadku korzystania z programu <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> lub <xref:System.Runtime.Serialization.NetDataContractSerializer> .  
  
## <a name="using-serializationbinder"></a>Korzystanie z pomocą elementu SerializationBinder  

 <xref:System.Runtime.Serialization.SerializationBinder> jest klasą abstrakcyjną służącą do kontrolowania rzeczywistych typów używanych podczas serializacji i deserializacji. Aby kontrolować typy używane podczas serializacji i deserializacji, należy utworzyć klasę z <xref:System.Runtime.Serialization.SerializationBinder> i zastąpić <xref:System.Runtime.Serialization.SerializationBinder.BindToName(System.Type,System.String@,System.String@)> <xref:System.Runtime.Serialization.SerializationBinder.BindToType(System.String,System.String)> metody i. <xref:System.Runtime.Serialization.SerializationBinder.BindToName(System.Type,System.String@,System.String@)>Metoda przyjmuje <xref:System.Type> i zwraca zestaw i nazwę typu. <xref:System.Runtime.Serialization.SerializationBinder.BindToType(System.String,System.String)>Metoda przyjmuje zestaw i nazwę typu i zwraca <xref:System.Type> .  
  
## <a name="see-also"></a>Zobacz też

- [Serializacja i deserializacja](serialization-and-deserialization.md)
- [Używanie obiektu wiążącego serializacji](../samples/usage-of-serialization-binder.md)
