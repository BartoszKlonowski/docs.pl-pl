---
title: Jak skonwertować tablicę bajtową na Przewodnik programowania int-C#
description: Dowiedz się, jak skonwertować tablicę bajtową na liczbę całkowitą. Zobacz przykłady kodu i Wyświetl dodatkowe dostępne zasoby.
ms.date: 07/20/2015
helpviewer_keywords:
- conversions [C#], byte array to int
- byte arrays [C#], converting to int
ms.topic: how-to
ms.custom: contperf-fy21q2
ms.assetid: d6ac20e2-448e-4aea-99b9-faf04c6f1e79
ms.openlocfilehash: f6fb6ad907ecd668d59ca95b19218c19d378d83e
ms.sourcegitcommit: d0990c1c1ab2f81908360f47eafa8db9aa165137
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/15/2020
ms.locfileid: "97513253"
---
# <a name="how-to-convert-a-byte-array-to-an-int-c-programming-guide"></a><span data-ttu-id="ea900-103">Jak skonwertować tablicę bajtową na liczbę całkowitą (Przewodnik programowania w języku C#)</span><span class="sxs-lookup"><span data-stu-id="ea900-103">How to convert a byte array to an int (C# Programming Guide)</span></span>

<span data-ttu-id="ea900-104">W tym przykładzie pokazano, jak użyć <xref:System.BitConverter> klasy do konwersji tablicy bajtów na [int](../../language-reference/builtin-types/integral-numeric-types.md) i z powrotem do tablicy bajtów.</span><span class="sxs-lookup"><span data-stu-id="ea900-104">This example shows you how to use the <xref:System.BitConverter> class to convert an array of bytes to an [int](../../language-reference/builtin-types/integral-numeric-types.md) and back to an array of bytes.</span></span> <span data-ttu-id="ea900-105">Może być konieczne przekonwertowanie z bajtów na typ danych wbudowanych po odczytaniu bajtów z sieci, na przykład.</span><span class="sxs-lookup"><span data-stu-id="ea900-105">You may have to convert from bytes to a built-in data type after you read bytes off the network, for example.</span></span> <span data-ttu-id="ea900-106">Oprócz metody [ToInt32 — (Byte \[ \] , Int32)](xref:System.BitConverter.ToInt32(System.Byte[],System.Int32)) w przykładzie Poniższa tabela zawiera listę metod w <xref:System.BitConverter> klasie, które konwertują bajty (z tablicy bajtów) na inne typy wbudowane.</span><span class="sxs-lookup"><span data-stu-id="ea900-106">In addition to the [ToInt32(Byte\[\], Int32)](xref:System.BitConverter.ToInt32(System.Byte[],System.Int32)) method in the example, the following table lists methods in the <xref:System.BitConverter> class that convert bytes (from an array of bytes) to other built-in types.</span></span>

|<span data-ttu-id="ea900-107">Zwrócony typ</span><span class="sxs-lookup"><span data-stu-id="ea900-107">Type returned</span></span>|<span data-ttu-id="ea900-108">Metoda</span><span class="sxs-lookup"><span data-stu-id="ea900-108">Method</span></span>|
|-------------------|------------|
|`bool`|<span data-ttu-id="ea900-109">[ToBoolean (Byte \[ \] , Int32)](xref:System.BitConverter.ToBoolean(System.Byte[],System.Int32))</span><span class="sxs-lookup"><span data-stu-id="ea900-109">[ToBoolean(Byte\[\], Int32)](xref:System.BitConverter.ToBoolean(System.Byte[],System.Int32))</span></span>|
|`char`|<span data-ttu-id="ea900-110">[ToChar — (Byte \[ \] , Int32)](xref:System.BitConverter.ToChar(System.Byte[],System.Int32))</span><span class="sxs-lookup"><span data-stu-id="ea900-110">[ToChar(Byte\[\], Int32)](xref:System.BitConverter.ToChar(System.Byte[],System.Int32))</span></span>|
|`double`|<span data-ttu-id="ea900-111">[ToDouble — (Byte \[ \] , Int32)](xref:System.BitConverter.ToDouble(System.Byte[],System.Int32))</span><span class="sxs-lookup"><span data-stu-id="ea900-111">[ToDouble(Byte\[\], Int32)](xref:System.BitConverter.ToDouble(System.Byte[],System.Int32))</span></span>|
|`short`|<span data-ttu-id="ea900-112">[Toint16 — (Byte \[ \] , Int32)](xref:System.BitConverter.ToInt16(System.Byte[],System.Int32))</span><span class="sxs-lookup"><span data-stu-id="ea900-112">[ToInt16(Byte\[\], Int32)](xref:System.BitConverter.ToInt16(System.Byte[],System.Int32))</span></span>|
|`int`|<span data-ttu-id="ea900-113">[Toint32 — (Byte \[ \] , Int32)](xref:System.BitConverter.ToInt32(System.Byte[],System.Int32))</span><span class="sxs-lookup"><span data-stu-id="ea900-113">[ToInt32(Byte\[\], Int32)](xref:System.BitConverter.ToInt32(System.Byte[],System.Int32))</span></span>|
|`long`|<span data-ttu-id="ea900-114">[Toint64 — (Byte \[ \] , Int32)](xref:System.BitConverter.ToInt64(System.Byte[],System.Int32))</span><span class="sxs-lookup"><span data-stu-id="ea900-114">[ToInt64(Byte\[\], Int32)](xref:System.BitConverter.ToInt64(System.Byte[],System.Int32))</span></span>|
|`float`|<span data-ttu-id="ea900-115">[ToSingle — (Byte \[ \] , Int32)](xref:System.BitConverter.ToSingle(System.Byte[],System.Int32))</span><span class="sxs-lookup"><span data-stu-id="ea900-115">[ToSingle(Byte\[\], Int32)](xref:System.BitConverter.ToSingle(System.Byte[],System.Int32))</span></span>|
|`ushort`|<span data-ttu-id="ea900-116">[Touint16 — (Byte \[ \] , Int32)](xref:System.BitConverter.ToUInt16(System.Byte[],System.Int32))</span><span class="sxs-lookup"><span data-stu-id="ea900-116">[ToUInt16(Byte\[\], Int32)](xref:System.BitConverter.ToUInt16(System.Byte[],System.Int32))</span></span>|
|`uint`|<span data-ttu-id="ea900-117">[Touint32 — (Byte \[ \] , Int32)](xref:System.BitConverter.ToUInt32(System.Byte[],System.Int32))</span><span class="sxs-lookup"><span data-stu-id="ea900-117">[ToUInt32(Byte\[\], Int32)](xref:System.BitConverter.ToUInt32(System.Byte[],System.Int32))</span></span>|
|`ulong`|<span data-ttu-id="ea900-118">[Touint64 — (Byte \[ \] , Int32)](xref:System.BitConverter.ToUInt64(System.Byte[],System.Int32))</span><span class="sxs-lookup"><span data-stu-id="ea900-118">[ToUInt64(Byte\[\], Int32)](xref:System.BitConverter.ToUInt64(System.Byte[],System.Int32))</span></span>|

## <a name="example"></a><span data-ttu-id="ea900-119">Przykład</span><span class="sxs-lookup"><span data-stu-id="ea900-119">Example</span></span>

<span data-ttu-id="ea900-120">Ten przykład Inicjuje tablicę bajtów, odwraca tablicę, jeśli architektura komputera jest w stanie little-endian (to znaczy najmniej znaczący bajt jest zapisywany jako pierwszy), a następnie wywołuje metodę [ToInt32 — (Byte \[ \] , Int32)](xref:System.BitConverter.ToInt32(System.Byte[],System.Int32)) , aby przekonwertować cztery bajty w tablicy na `int` .</span><span class="sxs-lookup"><span data-stu-id="ea900-120">This example initializes an array of bytes, reverses the array if the computer architecture is little-endian (that is, the least significant byte is stored first), and then calls the [ToInt32(Byte\[\], Int32)](xref:System.BitConverter.ToInt32(System.Byte[],System.Int32)) method to convert four bytes in the array to an `int`.</span></span> <span data-ttu-id="ea900-121">Drugi argument [ToInt32 — (Byte \[ \] , Int32)](xref:System.BitConverter.ToInt32(System.Byte[],System.Int32)) określa początkowy indeks tablicy bajtów.</span><span class="sxs-lookup"><span data-stu-id="ea900-121">The second argument to [ToInt32(Byte\[\], Int32)](xref:System.BitConverter.ToInt32(System.Byte[],System.Int32)) specifies the start index of the array of bytes.</span></span>

> [!NOTE]
> <span data-ttu-id="ea900-122">Dane wyjściowe mogą się różnić w zależności od liczby bajtów architektury komputera.</span><span class="sxs-lookup"><span data-stu-id="ea900-122">The output may differ depending on the endianness of your computer's architecture.</span></span>

[!code-csharp[csProgGuideTypes#22](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsProgGuideTypes/CS/Class1.cs#22)]

## <a name="example"></a><span data-ttu-id="ea900-123">Przykład</span><span class="sxs-lookup"><span data-stu-id="ea900-123">Example</span></span>

<span data-ttu-id="ea900-124">W tym przykładzie <xref:System.BitConverter.GetBytes%28System.Int32%29> Metoda <xref:System.BitConverter> klasy jest wywoływana w celu przekonwertowania `int` na tablicę bajtów.</span><span class="sxs-lookup"><span data-stu-id="ea900-124">In this example, the <xref:System.BitConverter.GetBytes%28System.Int32%29> method of the <xref:System.BitConverter> class is called to convert an `int` to an array of bytes.</span></span>

> [!NOTE]
> <span data-ttu-id="ea900-125">Dane wyjściowe mogą się różnić w zależności od liczby bajtów architektury komputera.</span><span class="sxs-lookup"><span data-stu-id="ea900-125">The output may differ depending on the endianness of your computer's architecture.</span></span>

[!code-csharp[csProgGuideTypes#23](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsProgGuideTypes/CS/Class1.cs#23)]

## <a name="see-also"></a><span data-ttu-id="ea900-126">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="ea900-126">See also</span></span>

- <xref:System.BitConverter>
- <xref:System.BitConverter.IsLittleEndian>
- [<span data-ttu-id="ea900-127">Typy</span><span class="sxs-lookup"><span data-stu-id="ea900-127">Types</span></span>](./index.md)
