---
title: Ostrzeżenie SYSLIB0001
description: Dowiedz się więcej o Obsoletions, które generują ostrzeżenie SYSLIB0001 w czasie kompilacji.
ms.topic: reference
ms.date: 10/20/2020
ms.openlocfilehash: d275717e22b260d9ceff4fe94993e9a0e6996cf0
ms.sourcegitcommit: 721c3e4bdbb1ea0bb420818ec944c538fe5c513a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/01/2020
ms.locfileid: "96437847"
---
# <a name="syslib0001-the-utf-7-encoding-is-insecure"></a><span data-ttu-id="860a5-103">SYSLIB0001: kodowanie UTF-7 jest niezabezpieczone</span><span class="sxs-lookup"><span data-stu-id="860a5-103">SYSLIB0001: The UTF-7 encoding is insecure</span></span>

<span data-ttu-id="860a5-104">Kodowanie UTF-7 nie jest już używane między aplikacjami, a wiele specyfikacji już [zabroni jego użycia](https://security.stackexchange.com/a/68609/3573) w wymianie.</span><span class="sxs-lookup"><span data-stu-id="860a5-104">The UTF-7 encoding is no longer in wide use among applications, and many specs now [forbid its use](https://security.stackexchange.com/a/68609/3573) in interchange.</span></span> <span data-ttu-id="860a5-105">Jest to również sporadycznie [używane jako wektor ataku](https://cve.mitre.org/cgi-bin/cvekey.cgi?keyword=utf-7) w aplikacjach, które nie przewidziano do napotkania danych zakodowanych w formacie UTF-7.</span><span class="sxs-lookup"><span data-stu-id="860a5-105">It's also occasionally [used as an attack vector](https://cve.mitre.org/cgi-bin/cvekey.cgi?keyword=utf-7) in applications that don't anticipate encountering UTF-7-encoded data.</span></span> <span data-ttu-id="860a5-106">Firma Microsoft ostrzega przed użyciem, <xref:System.Text.UTF7Encoding?displayProperty=nameWithType> ponieważ nie zapewnia wykrywania błędów.</span><span class="sxs-lookup"><span data-stu-id="860a5-106">Microsoft warns against use of <xref:System.Text.UTF7Encoding?displayProperty=nameWithType> because it doesn't provide error detection.</span></span>

<span data-ttu-id="860a5-107">W związku z tym następujące interfejsy API są oznaczone jako przestarzałe, począwszy od platformy .NET 5,0.</span><span class="sxs-lookup"><span data-stu-id="860a5-107">Consequently, the following APIs are marked obsolete, starting in .NET 5.0.</span></span> <span data-ttu-id="860a5-108">Użycie tych interfejsów API generuje ostrzeżenie `SYSLIB0001` w czasie kompilacji.</span><span class="sxs-lookup"><span data-stu-id="860a5-108">Use of these APIs generates warning `SYSLIB0001` at compile time.</span></span>

- <span data-ttu-id="860a5-109"><xref:System.Text.Encoding.UTF7?displayProperty=nameWithType> wartość</span><span class="sxs-lookup"><span data-stu-id="860a5-109"><xref:System.Text.Encoding.UTF7?displayProperty=nameWithType> property</span></span>
- <span data-ttu-id="860a5-110"><xref:System.Text.UTF7Encoding.%23ctor%2A> Konstruktor</span><span class="sxs-lookup"><span data-stu-id="860a5-110"><xref:System.Text.UTF7Encoding.%23ctor%2A> constructors</span></span>

## <a name="workarounds"></a><span data-ttu-id="860a5-111">Obejścia</span><span class="sxs-lookup"><span data-stu-id="860a5-111">Workarounds</span></span>

- <span data-ttu-id="860a5-112">W przypadku korzystania z programu <xref:System.Text.Encoding.UTF7?displayProperty=nameWithType> lub <xref:System.Text.UTF7Encoding> w ramach własnego protokołu lub formatu pliku:</span><span class="sxs-lookup"><span data-stu-id="860a5-112">If you're using <xref:System.Text.Encoding.UTF7?displayProperty=nameWithType> or <xref:System.Text.UTF7Encoding> within your own protocol or file format:</span></span>

  <span data-ttu-id="860a5-113">Przełącz się do korzystania z <xref:System.Text.Encoding.UTF8?displayProperty=nameWithType> lub <xref:System.Text.UTF8Encoding> .</span><span class="sxs-lookup"><span data-stu-id="860a5-113">Switch to using <xref:System.Text.Encoding.UTF8?displayProperty=nameWithType> or <xref:System.Text.UTF8Encoding>.</span></span> <span data-ttu-id="860a5-114">UTF-8 jest standardem branżowym i jest szeroko obsługiwany w różnych językach, systemach operacyjnych i w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="860a5-114">UTF-8 is an industry standard and is widely supported across languages, operating systems, and runtimes.</span></span> <span data-ttu-id="860a5-115">Użycie UTF-8 ułatwia przyszłą konserwację kodu i sprawia, że jest to bardziej obsługiwane w pozostałej części ekosystemu.</span><span class="sxs-lookup"><span data-stu-id="860a5-115">Using UTF-8 eases future maintenance of your code and makes it more interoperable with the rest of the ecosystem.</span></span>

- <span data-ttu-id="860a5-116">Jeśli porównujesz <xref:System.Text.Encoding> wystąpienie z <xref:System.Text.Encoding.UTF7?displayProperty=nameWithType> :</span><span class="sxs-lookup"><span data-stu-id="860a5-116">If you're comparing an <xref:System.Text.Encoding> instance against <xref:System.Text.Encoding.UTF7?displayProperty=nameWithType>:</span></span>

  <span data-ttu-id="860a5-117">Zamiast tego należy rozważyć przeprowadzenie sprawdzenia względem dobrze znanej strony kodowej UTF-7, która jest `65000` .</span><span class="sxs-lookup"><span data-stu-id="860a5-117">Instead, consider performing a check against the well-known UTF-7 code page, which is `65000`.</span></span> <span data-ttu-id="860a5-118">Porównując względem strony kodowej, można uniknąć ostrzeżenia, a także obsłużyć niektóre przypadki brzegowe, na przykład jeśli ktoś wywołał `new UTF7Encoding()` lub podklasy typ.</span><span class="sxs-lookup"><span data-stu-id="860a5-118">By comparing against the code page, you avoid the warning and also handle some edge cases, such as if somebody called `new UTF7Encoding()` or subclassed the type.</span></span>

  ```csharp
  void DoSomething(Encoding enc)
  {
      // Don't perform the check this way.
      // It produces a warning and misses some edge cases.
      if (enc == Encoding.UTF7)
      {
          // Encoding is UTF-7.
      }

      // Instead, perform the check this way.
      if (enc != null && enc.CodePage == 65000)
      {
          // Encoding is UTF-7.
      }
  }
  ```

[!INCLUDE [suppress-syslib-warning](../../../includes/suppress-syslib-warning.md)]

## <a name="see-also"></a><span data-ttu-id="860a5-119">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="860a5-119">See also</span></span>

- [<span data-ttu-id="860a5-120">Ścieżki kodu UTF-7 są przestarzałe</span><span class="sxs-lookup"><span data-stu-id="860a5-120">UTF-7 code paths are obsolete</span></span>](core-libraries/5.0/utf-7-code-paths-obsolete.md)
