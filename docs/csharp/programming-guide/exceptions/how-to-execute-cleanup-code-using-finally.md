---
title: Jak wykonać kod czyszczący za pomocą przewodnika programowania finally w języku C#
description: Dowiedz się, jak wykonać oczyszczanie kodu przy użyciu instrukcji "finally". Instrukcje finally zapewniają, że wszelkie niezbędne czyszczenie obiektów następuje natychmiast.
ms.date: 07/20/2015
helpviewer_keywords:
- try/finally blocks [C#]
- exceptions [C#], try/finally block
- exception handling [C#], try/finally block
ms.assetid: 1b1e5aef-3f32-4a88-9d39-b5fffb33bdaf
ms.openlocfilehash: 148c1f9fba67659a07c667bb15619d6f3f7c3b2f
ms.sourcegitcommit: 6f58a5f75ceeb936f8ee5b786e9adb81a9a3bee9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/28/2020
ms.locfileid: "87302025"
---
# <a name="how-to-execute-cleanup-code-using-finally-c-programming-guide"></a><span data-ttu-id="6bd44-104">Jak wykonać oczyszczanie kodu za pomocą finally (Przewodnik programowania w języku C#)</span><span class="sxs-lookup"><span data-stu-id="6bd44-104">How to execute cleanup code using finally (C# Programming Guide)</span></span>
<span data-ttu-id="6bd44-105">Celem `finally` instrukcji jest upewnienie się, że konieczne jest oczyszczenie obiektów, zwykle obiektów, które są zasobami zewnętrznymi, występuje natychmiast, nawet jeśli zostanie zgłoszony wyjątek.</span><span class="sxs-lookup"><span data-stu-id="6bd44-105">The purpose of a `finally` statement is to ensure that the necessary cleanup of objects, usually objects that are holding external resources, occurs immediately, even if an exception is thrown.</span></span> <span data-ttu-id="6bd44-106">Przykładem takiego oczyszczania jest wywoływanie <xref:System.IO.Stream.Close%2A> <xref:System.IO.FileStream> natychmiast po użyciu zamiast oczekiwania na odrzucanie obiektu przez środowisko uruchomieniowe języka wspólnego w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="6bd44-106">One example of such cleanup is calling <xref:System.IO.Stream.Close%2A> on a <xref:System.IO.FileStream> immediately after use instead of waiting for the object to be garbage collected by the common language runtime, as follows:</span></span>  
  
 [!code-csharp[csProgGuideExceptions#16](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideExceptions/CS/Exceptions.cs#16)]  
  
## <a name="example"></a><span data-ttu-id="6bd44-107">Przykład</span><span class="sxs-lookup"><span data-stu-id="6bd44-107">Example</span></span>  
 <span data-ttu-id="6bd44-108">Aby przekształcić poprzedni kod do `try-catch-finally` instrukcji, kod czyszczący jest oddzielony od kodu roboczego w następujący sposób.</span><span class="sxs-lookup"><span data-stu-id="6bd44-108">To turn the previous code into a `try-catch-finally` statement, the cleanup code is separated from the working code, as follows.</span></span>  
  
 [!code-csharp[csProgGuideExceptions#17](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideExceptions/CS/Exceptions.cs#17)]  
  
 <span data-ttu-id="6bd44-109">Ponieważ wyjątek może wystąpić w dowolnym momencie w `try` bloku przed `OpenWrite()` wywołaniem lub `OpenWrite()` samo wywołanie może się nie powieść, nie gwarantujemy, że plik jest otwarty, gdy spróbujemy go zamknąć.</span><span class="sxs-lookup"><span data-stu-id="6bd44-109">Because an exception can occur at any time within the `try` block before the `OpenWrite()` call, or the `OpenWrite()` call itself could fail, we are not guaranteed that the file is open when we try to close it.</span></span> <span data-ttu-id="6bd44-110">`finally`Blok dodaje zaznaczenie, aby upewnić się, że <xref:System.IO.FileStream> obiekt nie jest `null` przed wywołaniem <xref:System.IO.Stream.Close%2A> metody.</span><span class="sxs-lookup"><span data-stu-id="6bd44-110">The `finally` block adds a check to make sure that the <xref:System.IO.FileStream> object is not `null` before you call the <xref:System.IO.Stream.Close%2A> method.</span></span> <span data-ttu-id="6bd44-111">Bez `null` sprawdzania, `finally` blok może zgłosić swój własny <xref:System.NullReferenceException> , ale `finally` Jeśli jest to możliwe, należy unikać zgłaszania wyjątków w blokach.</span><span class="sxs-lookup"><span data-stu-id="6bd44-111">Without the `null` check, the `finally` block could throw its own <xref:System.NullReferenceException>, but throwing exceptions in `finally` blocks should be avoided if it is possible.</span></span>  
  
 <span data-ttu-id="6bd44-112">Połączenie z bazą danych jest kolejnym odpowiednim kandydatem do zamknięcia w `finally` bloku.</span><span class="sxs-lookup"><span data-stu-id="6bd44-112">A database connection is another good candidate for being closed in a `finally` block.</span></span> <span data-ttu-id="6bd44-113">Ponieważ liczba połączeń dozwolonych dla serwera bazy danych jest czasami ograniczona, należy zamknąć połączenia z bazą danych tak szybko, jak to możliwe.</span><span class="sxs-lookup"><span data-stu-id="6bd44-113">Because the number of connections allowed to a database server is sometimes limited, you should close database connections as quickly as possible.</span></span> <span data-ttu-id="6bd44-114">Jeśli wyjątek jest zgłaszany przed zamknięciem połączenia, jest to kolejny przypadek, w którym użycie `finally` bloku jest lepsze niż oczekiwanie na wyrzucanie elementów bezużytecznych.</span><span class="sxs-lookup"><span data-stu-id="6bd44-114">If an exception is thrown before you can close your connection, this is another case where using the `finally` block is better than waiting for garbage collection.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="6bd44-115">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="6bd44-115">See also</span></span>

- [<span data-ttu-id="6bd44-116">Przewodnik programowania w języku C#</span><span class="sxs-lookup"><span data-stu-id="6bd44-116">C# Programming Guide</span></span>](../index.md)
- [<span data-ttu-id="6bd44-117">Wyjątki i obsługa wyjątków</span><span class="sxs-lookup"><span data-stu-id="6bd44-117">Exceptions and Exception Handling</span></span>](./index.md)
- [<span data-ttu-id="6bd44-118">Obsługa wyjątków</span><span class="sxs-lookup"><span data-stu-id="6bd44-118">Exception Handling</span></span>](./exception-handling.md)
- [<span data-ttu-id="6bd44-119">using, instrukcja</span><span class="sxs-lookup"><span data-stu-id="6bd44-119">using Statement</span></span>](../../language-reference/keywords/using-statement.md)
- [<span data-ttu-id="6bd44-120">try-catch</span><span class="sxs-lookup"><span data-stu-id="6bd44-120">try-catch</span></span>](../../language-reference/keywords/try-catch.md)
- [<span data-ttu-id="6bd44-121">try-finally</span><span class="sxs-lookup"><span data-stu-id="6bd44-121">try-finally</span></span>](../../language-reference/keywords/try-finally.md)
- [<span data-ttu-id="6bd44-122">try-catch-finally</span><span class="sxs-lookup"><span data-stu-id="6bd44-122">try-catch-finally</span></span>](../../language-reference/keywords/try-catch-finally.md)
