---
title: Zapewnianie integralności danych za pomocą wartości skrótu
description: Dowiedz się, jak zapewnić integralność danych przy użyciu kodów skrótu w programie .NET. Wartość skrótu to wartość liczbowa o stałej długości, która jednoznacznie identyfikuje dane.
ms.date: 07/14/2020
dev_langs:
- csharp
- vb
helpviewer_keywords:
- generating hash
- verifying hash codes
- cryptography [.NET], hash
- data integrity
- checking hash codes
- encryption [.NET], hash
- hash
ms.assetid: 33660f33-b70f-4dca-8c87-ab35cfc2961a
ms.openlocfilehash: 7f5e1d54efa3a5ccf28f2e0863a9bc9ccb80f894
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95689748"
---
# <a name="ensuring-data-integrity-with-hash-codes"></a><span data-ttu-id="6e42c-104">Zapewnianie integralności danych za pomocą wartości skrótu</span><span class="sxs-lookup"><span data-stu-id="6e42c-104">Ensuring Data Integrity with Hash Codes</span></span>

<span data-ttu-id="6e42c-105">Wartość skrótu to wartość liczbowa o stałej długości, która jednoznacznie identyfikuje dane.</span><span class="sxs-lookup"><span data-stu-id="6e42c-105">A hash value is a numeric value of a fixed length that uniquely identifies data.</span></span> <span data-ttu-id="6e42c-106">Wartości skrótu przedstawiają duże ilości danych jako dużo mniejsze wartości liczbowe, dlatego są używane z podpisami cyfrowymi.</span><span class="sxs-lookup"><span data-stu-id="6e42c-106">Hash values represent large amounts of data as much smaller numeric values, so they are used with digital signatures.</span></span> <span data-ttu-id="6e42c-107">Wartość skrótu można podpisywać bardziej wydajnie niż podpisywanie większej wartości.</span><span class="sxs-lookup"><span data-stu-id="6e42c-107">You can sign a hash value more efficiently than signing the larger value.</span></span> <span data-ttu-id="6e42c-108">Wartości skrótu są również przydatne do sprawdzania integralności danych wysyłanych za pomocą niezabezpieczonych kanałów.</span><span class="sxs-lookup"><span data-stu-id="6e42c-108">Hash values are also useful for verifying the integrity of data sent through insecure channels.</span></span> <span data-ttu-id="6e42c-109">Wartość skrótu odebranych danych może być porównywana z wartością skrótu danych, która została wysłana w celu określenia, czy dane zostały zmienione.</span><span class="sxs-lookup"><span data-stu-id="6e42c-109">The hash value of received data can be compared to the hash value of data as it was sent to determine whether the data was altered.</span></span>  
  
<span data-ttu-id="6e42c-110">W tym temacie opisano sposób generowania i weryfikowania kodów skrótów przy użyciu klas w <xref:System.Security.Cryptography> przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="6e42c-110">This topic describes how to generate and verify hash codes by using the classes in the <xref:System.Security.Cryptography> namespace.</span></span>  
  
## <a name="generating-a-hash"></a><span data-ttu-id="6e42c-111">Generowanie skrótu</span><span class="sxs-lookup"><span data-stu-id="6e42c-111">Generating a Hash</span></span>

 <span data-ttu-id="6e42c-112">Zarządzane klasy skrótów mogą mieszać tablicę bajtów lub obiekt strumienia zarządzanego.</span><span class="sxs-lookup"><span data-stu-id="6e42c-112">The managed hash classes can hash either an array of bytes or a managed stream object.</span></span> <span data-ttu-id="6e42c-113">W poniższym przykładzie jest używany algorytm skrótu SHA1 do tworzenia wartości skrótu dla ciągu.</span><span class="sxs-lookup"><span data-stu-id="6e42c-113">The following example uses the SHA1 hash algorithm to create a hash value for a string.</span></span> <span data-ttu-id="6e42c-114">W przykładzie użyto <xref:System.Text.UnicodeEncoding> klasy do przekonwertowania ciągu na tablicę bajtów, które są zmieszane przy użyciu <xref:System.Security.Cryptography.SHA256> klasy.</span><span class="sxs-lookup"><span data-stu-id="6e42c-114">The example uses the <xref:System.Text.UnicodeEncoding> class to convert the string into an array of bytes that are hashed by using the <xref:System.Security.Cryptography.SHA256> class.</span></span> <span data-ttu-id="6e42c-115">Wartość skrótu zostanie następnie wyświetlona w konsoli programu.</span><span class="sxs-lookup"><span data-stu-id="6e42c-115">The hash value is then displayed to the console.</span></span>  

 [!code-csharp[GeneratingAHash#1](../../../samples/snippets/csharp/VS_Snippets_CLR/generatingahash/cs/program.cs#1)]
 [!code-vb[GeneratingAHash#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/generatingahash/vb/program.vb#1)]  
  
 <span data-ttu-id="6e42c-116">Ten kod będzie wyświetlał następujący ciąg do konsoli:</span><span class="sxs-lookup"><span data-stu-id="6e42c-116">This code will display the following string to the console:</span></span>  
  
 `185 203 236 22 3 228 27 130 87 23 244 15 87 88 14 43 37 61 106 224 81 172 224 211 104 85 194 197 194 25 120 217`  
  
## <a name="verifying-a-hash"></a><span data-ttu-id="6e42c-117">Weryfikowanie skrótu</span><span class="sxs-lookup"><span data-stu-id="6e42c-117">Verifying a Hash</span></span>

 <span data-ttu-id="6e42c-118">Dane można porównać do wartości skrótu, aby określić jej integralność.</span><span class="sxs-lookup"><span data-stu-id="6e42c-118">Data can be compared to a hash value to determine its integrity.</span></span> <span data-ttu-id="6e42c-119">Zwykle dane są zmieszane w określonym czasie, a wartość skrótu jest chroniona w jakiś sposób.</span><span class="sxs-lookup"><span data-stu-id="6e42c-119">Usually, data is hashed at a certain time and the hash value is protected in some way.</span></span> <span data-ttu-id="6e42c-120">Później można ponownie wykonać mieszanie danych i porównywać ją z wartością chronioną.</span><span class="sxs-lookup"><span data-stu-id="6e42c-120">At a later time, the data can be hashed again and compared to the protected value.</span></span> <span data-ttu-id="6e42c-121">W przypadku dopasowania wartości skrótu dane nie zostały zmienione.</span><span class="sxs-lookup"><span data-stu-id="6e42c-121">If the hash values match, the data has not been altered.</span></span> <span data-ttu-id="6e42c-122">Jeśli wartości nie są zgodne, dane zostały uszkodzone.</span><span class="sxs-lookup"><span data-stu-id="6e42c-122">If the values do not match, the data has been corrupted.</span></span> <span data-ttu-id="6e42c-123">Aby ten system działał, chroniony skrót musi być zaszyfrowany lub przechowywany jako wpis tajny ze wszystkich niezaufanych stron.</span><span class="sxs-lookup"><span data-stu-id="6e42c-123">For this system to work, the protected hash must be encrypted or kept secret from all untrusted parties.</span></span>  
  
 <span data-ttu-id="6e42c-124">Poniższy przykład porównuje poprzednią wartość skrótu ciągu z nową wartością skrótu.</span><span class="sxs-lookup"><span data-stu-id="6e42c-124">The following example compares the previous hash value of a string to a new hash value.</span></span> <span data-ttu-id="6e42c-125">Ten przykład powoduje pętlę przez każdy bajt wartości skrótu i wykonuje porównanie.</span><span class="sxs-lookup"><span data-stu-id="6e42c-125">This example loops through each byte of the hash values and makes a comparison.</span></span>  
  
 [!code-csharp[VerifyingAHash#1](../../../samples/snippets/csharp/VS_Snippets_CLR/verifyingahash/cs/program.cs#1)]
 [!code-vb[VerifyingAHash#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/verifyingahash/vb/program.vb#1)]  
  
 <span data-ttu-id="6e42c-126">Jeśli dwie wartości skrótów są zgodne, ten kod wyświetla następujące polecenie w konsoli programu:</span><span class="sxs-lookup"><span data-stu-id="6e42c-126">If the two hash values match, this code displays the following to the console:</span></span>  
  
```console  
The hash codes match.  
```  
  
 <span data-ttu-id="6e42c-127">Jeśli nie są zgodne, kod wyświetla następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="6e42c-127">If they do not match, the code displays the following:</span></span>  
  
```console  
The hash codes do not match.  
```  
  
## <a name="see-also"></a><span data-ttu-id="6e42c-128">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="6e42c-128">See also</span></span>

- [<span data-ttu-id="6e42c-129">Model kryptografii</span><span class="sxs-lookup"><span data-stu-id="6e42c-129">Cryptography Model</span></span>](cryptography-model.md)
- [<span data-ttu-id="6e42c-130">Usługi kryptograficzne</span><span class="sxs-lookup"><span data-stu-id="6e42c-130">Cryptographic Services</span></span>](cryptographic-services.md)
- [<span data-ttu-id="6e42c-131">Kryptografia międzyplatformowa</span><span class="sxs-lookup"><span data-stu-id="6e42c-131">Cross-Platform Cryptography</span></span>](cross-platform-cryptography.md)
- [<span data-ttu-id="6e42c-132">Ochrona danych ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="6e42c-132">ASP.NET Core Data Protection</span></span>](/aspnet/core/security/data-protection/introduction)
