---
author: dotpaul
ms.author: paulming
ms.date: 05/01/2019
ms.topic: include
ms.openlocfilehash: cf944ae9ca200d34a1f0f32e68bf3aee73a9500a
ms.sourcegitcommit: c04535ad05e374fb269fcfc6509217755fbc0d54
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/25/2020
ms.locfileid: "96586693"
---
- <span data-ttu-id="0b47f-101">Jeśli to możliwe, zamiast tego Użyj bezpiecznego serializatora i **nie Zezwalaj osobie atakującej na określenie dowolnego typu do deserializacji**.</span><span class="sxs-lookup"><span data-stu-id="0b47f-101">If possible, use a secure serializer instead, and **don't allow an attacker to specify an arbitrary type to deserialize**.</span></span> <span data-ttu-id="0b47f-102">Niektóre bezpieczniejsze serializacji obejmują:</span><span class="sxs-lookup"><span data-stu-id="0b47f-102">Some safer serializers include:</span></span>

  - <xref:System.Runtime.Serialization.DataContractSerializer?displayProperty=nameWithType>
  - <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer?displayProperty=nameWithType>
  - <span data-ttu-id="0b47f-103"><xref:System.Web.Script.Serialization.JavaScriptSerializer?displayProperty=nameWithType> — Nigdy nie używaj <xref:System.Web.Script.Serialization.SimpleTypeResolver?displayProperty=nameWithType> .</span><span class="sxs-lookup"><span data-stu-id="0b47f-103"><xref:System.Web.Script.Serialization.JavaScriptSerializer?displayProperty=nameWithType> - Never use <xref:System.Web.Script.Serialization.SimpleTypeResolver?displayProperty=nameWithType>.</span></span> <span data-ttu-id="0b47f-104">Jeśli musisz użyć mechanizmu rozpoznawania typów, Ogranicz typy deserializowane do oczekiwanej listy.</span><span class="sxs-lookup"><span data-stu-id="0b47f-104">If you must use a type resolver, restrict deserialized types to an expected list.</span></span>
  - <xref:System.Xml.Serialization.XmlSerializer?displayProperty=nameWithType>
  - <span data-ttu-id="0b47f-105">Newtonsoft Json.NET — Użyj TypeNameHandling. None.</span><span class="sxs-lookup"><span data-stu-id="0b47f-105">Newtonsoft Json.NET - Use TypeNameHandling.None.</span></span> <span data-ttu-id="0b47f-106">Jeśli musisz użyć innej wartości dla TypeNameHandling, Ogranicz typy deserializowane do oczekiwanej listy za pomocą niestandardowego ISerializationBinder.</span><span class="sxs-lookup"><span data-stu-id="0b47f-106">If you must use another value for TypeNameHandling, restrict deserialized types to an expected list with a custom ISerializationBinder.</span></span>
  - <span data-ttu-id="0b47f-107">Bufory protokołu</span><span class="sxs-lookup"><span data-stu-id="0b47f-107">Protocol Buffers</span></span>

- <span data-ttu-id="0b47f-108">Przekształć dane serializowane.</span><span class="sxs-lookup"><span data-stu-id="0b47f-108">Make the serialized data tamper-proof.</span></span> <span data-ttu-id="0b47f-109">Po serializacji należy kryptograficznie podpisywać serializowane dane.</span><span class="sxs-lookup"><span data-stu-id="0b47f-109">After serialization, cryptographically sign the serialized data.</span></span> <span data-ttu-id="0b47f-110">Przed deserializacji Sprawdź poprawność podpisu kryptograficznego.</span><span class="sxs-lookup"><span data-stu-id="0b47f-110">Before deserialization, validate the cryptographic signature.</span></span> <span data-ttu-id="0b47f-111">Ochrona klucza kryptograficznego przed ujawnieniem i projektowaniem na potrzeby rotacji kluczy.</span><span class="sxs-lookup"><span data-stu-id="0b47f-111">Protect the cryptographic key from being disclosed and design for key rotations.</span></span>
