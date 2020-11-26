---
title: 'Usługa: Błędy walidacji i uwierzytelniania'
ms.date: 03/30/2017
ms.assetid: 55c98268-b1ad-459d-851b-25ef52248187
ms.openlocfilehash: d89419d7d579d29a1c57370d61eefb8b26333a40
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96236861"
---
# <a name="service-security-validation-and-authentication-failures"></a><span data-ttu-id="046f2-102">Usługa: Błędy walidacji i uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="046f2-102">Service: Security Validation and Authentication Failures</span></span>

<span data-ttu-id="046f2-103">Nazwa licznika: Błędy walidacji zabezpieczeń i uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="046f2-103">Counter name: Security Validation and Authentication Failures</span></span>  
  
## <a name="description"></a><span data-ttu-id="046f2-104">Opis</span><span class="sxs-lookup"><span data-stu-id="046f2-104">Description</span></span>  

 <span data-ttu-id="046f2-105">Ten licznik jest zwiększany za każdym razem, gdy komunikat zostanie odrzucony z powodu problemu z zabezpieczeniami, którego nie dotyczy licznik "wywołania zabezpieczeń bez autoryzacji".</span><span class="sxs-lookup"><span data-stu-id="046f2-105">This counter is incremented whenever a message is rejected due to a security problem not covered by the "Security Calls Not Authorized" counter.</span></span> <span data-ttu-id="046f2-106">Takie problemy obejmują:</span><span class="sxs-lookup"><span data-stu-id="046f2-106">Such problems include:</span></span>  
  
- <span data-ttu-id="046f2-107">Nie można odczytać z komunikatu tokenu klienta.</span><span class="sxs-lookup"><span data-stu-id="046f2-107">Client token cannot be read from the message.</span></span>  
  
- <span data-ttu-id="046f2-108">Uwierzytelnianie tokenu klienta nie powiodło się (na przykład złe hasło).</span><span class="sxs-lookup"><span data-stu-id="046f2-108">Client token has failed authentication (for example, bad password).</span></span>  
  
- <span data-ttu-id="046f2-109">Weryfikacja podpisu nie powiodła się (na przykład komunikat został naruszony).</span><span class="sxs-lookup"><span data-stu-id="046f2-109">Signature verification has failed (for example, the message has been tampered).</span></span>  
  
- <span data-ttu-id="046f2-110">Komunikat jest duplikatem z poprzedniego, który może wystąpić podczas ataku metodą powtórzeń.</span><span class="sxs-lookup"><span data-stu-id="046f2-110">The message is a duplicate from a previous one, which can happen during a replay attack.</span></span>  
  
- <span data-ttu-id="046f2-111">Wystąpił błąd odszyfrowywania.</span><span class="sxs-lookup"><span data-stu-id="046f2-111">A decryption failure has occurred.</span></span>  
  
- <span data-ttu-id="046f2-112">W komunikacie brakuje niektórych wymaganych elementów (na przykład braku sygnatury czasowej lub zaszyfrowanego bloku danych).</span><span class="sxs-lookup"><span data-stu-id="046f2-112">Some required elements (for example, missing timestamp or encrypted data block) are missing from the message.</span></span>  
  
- <span data-ttu-id="046f2-113">Wystąpiły błędy podczas uzgadniania TLSNEGO/SPNEGO.</span><span class="sxs-lookup"><span data-stu-id="046f2-113">Errors have occurred during TLSNEGO/SPNEGO handshake.</span></span>
