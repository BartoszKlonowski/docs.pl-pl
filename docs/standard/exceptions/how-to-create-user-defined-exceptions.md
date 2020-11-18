---
title: 'Porady: tworzenie wyjątków zdefiniowanych przez użytkownika'
description: Dowiedz się, jak utworzyć wyjątki zdefiniowane przez użytkownika, które są alternatywą dla hierarchii klas wyjątków pochodzących z klasy podstawowej wyjątku w programie .NET.
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- user-defined exceptions
- exceptions, examples
- exceptions, user-defined
ms.assetid: 25819a5a-f915-4fc8-b924-a76915674e04
ms.openlocfilehash: b0a8549c9bacf322a0685c7b505185ab1d1101f6
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/18/2020
ms.locfileid: "94828130"
---
# <a name="how-to-create-user-defined-exceptions"></a><span data-ttu-id="dc189-103">Jak utworzyć wyjątki zdefiniowane przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="dc189-103">How to create user-defined exceptions</span></span>

<span data-ttu-id="dc189-104">Platforma .NET udostępnia hierarchię klas wyjątków ostatecznie pochodnych od klasy bazowej <xref:System.Exception> .</span><span class="sxs-lookup"><span data-stu-id="dc189-104">.NET provides a hierarchy of exception classes ultimately derived from the base class <xref:System.Exception>.</span></span> <span data-ttu-id="dc189-105">Jeśli jednak żaden ze wstępnie zdefiniowanych wyjątków nie spełnia Twoich potrzeb, można utworzyć własne klasy wyjątków, wyprowadzając je z <xref:System.Exception> klasy.</span><span class="sxs-lookup"><span data-stu-id="dc189-105">However, if none of the predefined exceptions meets your needs, you can create your own exception classes by deriving from the <xref:System.Exception> class.</span></span>

<span data-ttu-id="dc189-106">Podczas tworzenia własnych wyjątków, należy zakończyć nazwę klasy wyjątku zdefiniowanego przez użytkownika z wyrazem "Exception" i zaimplementować trzy typowe konstruktory, jak pokazano w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="dc189-106">When creating your own exceptions, end the class name of the user-defined exception with the word "Exception", and implement the three common constructors, as shown in the following example.</span></span> <span data-ttu-id="dc189-107">W przykładzie zdefiniowano nową klasę wyjątku o nazwie `EmployeeListNotFoundException` .</span><span class="sxs-lookup"><span data-stu-id="dc189-107">The example defines a new exception class named `EmployeeListNotFoundException`.</span></span> <span data-ttu-id="dc189-108">Klasa pochodzi od <xref:System.Exception> i zawiera trzy konstruktory.</span><span class="sxs-lookup"><span data-stu-id="dc189-108">The class is derived from <xref:System.Exception> and includes three constructors.</span></span>

[!code-cpp[dg_exceptionDesign#14](../../../samples/snippets/cpp/VS_Snippets_CLR/dg_exceptionDesign/cpp/example2.cpp#14)]
[!code-csharp[dg_exceptionDesign#14](../../../samples/snippets/csharp/VS_Snippets_CLR/dg_exceptionDesign/cs/example2.cs#14)]
[!code-vb[dg_exceptionDesign#14](../../../samples/snippets/visualbasic/VS_Snippets_CLR/dg_exceptionDesign/vb/example2.vb#14)]  

> [!NOTE]
> <span data-ttu-id="dc189-109">W sytuacjach, gdy używasz komunikacji zdalnej, należy upewnić się, że metadane dla wszystkich wyjątków zdefiniowanych przez użytkownika są dostępne na serwerze (wywoływanym) i na kliencie (obiekt serwera proxy lub wywołujący).</span><span class="sxs-lookup"><span data-stu-id="dc189-109">In situations where you are using remoting, you must ensure that the metadata for any user-defined exceptions is available at the server (callee) and to the client (the proxy object or caller).</span></span> <span data-ttu-id="dc189-110">Aby uzyskać więcej informacji, zobacz [najlepsze rozwiązania dotyczące wyjątków](best-practices-for-exceptions.md).</span><span class="sxs-lookup"><span data-stu-id="dc189-110">For more information, see [Best practices for exceptions](best-practices-for-exceptions.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="dc189-111">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="dc189-111">See also</span></span>

- [<span data-ttu-id="dc189-112">Wyjątki</span><span class="sxs-lookup"><span data-stu-id="dc189-112">Exceptions</span></span>](index.md)
