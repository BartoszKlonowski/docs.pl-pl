---
title: 'Porady: implementowanie obserwatora'
description: Zaimplementuj obserwatora w programie .NET. Wzorzec projektowy obserwatora wymaga podziału między obserwatorem, który rejestruje powiadomienia i dostawcę.
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- observers [.NET], observer design pattern
- observer design pattern [.NET], implementing observers
ms.assetid: 8ecfa9f5-b500-473d-bcf0-5652ffb1e53d
ms.openlocfilehash: bfd595cec8e499b760f75f614bd0a61b031eb207
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/18/2020
ms.locfileid: "94828338"
---
# <a name="how-to-implement-an-observer"></a><span data-ttu-id="2d3f7-104">Porady: implementowanie obserwatora</span><span class="sxs-lookup"><span data-stu-id="2d3f7-104">How to: Implement an Observer</span></span>
<span data-ttu-id="2d3f7-105">Wzorzec projektowy obserwatora wymaga podziału między obserwatorem, który rejestruje powiadomienia i dostawca, który monitoruje dane i wysyła powiadomienia do jednego lub kilku obserwatorów.</span><span class="sxs-lookup"><span data-stu-id="2d3f7-105">The observer design pattern requires a division between an observer, which registers for notifications, and a provider, which monitors data and sends notifications to one or more observers.</span></span> <span data-ttu-id="2d3f7-106">W tym temacie omówiono sposób tworzenia obserwatora.</span><span class="sxs-lookup"><span data-stu-id="2d3f7-106">This topic discusses how to create an observer.</span></span> <span data-ttu-id="2d3f7-107">Pokrewny temat, [jak: implementowanie dostawcy](how-to-implement-a-provider.md), omawia sposób tworzenia dostawcy.</span><span class="sxs-lookup"><span data-stu-id="2d3f7-107">A related topic, [How to: Implement a Provider](how-to-implement-a-provider.md), discusses how to create an provider.</span></span>  
  
### <a name="to-create-an-observer"></a><span data-ttu-id="2d3f7-108">Aby utworzyć obserwatora</span><span class="sxs-lookup"><span data-stu-id="2d3f7-108">To create an observer</span></span>  
  
1. <span data-ttu-id="2d3f7-109">Zdefiniuj obserwatora, który jest typem, który implementuje <xref:System.IObserver%601?displayProperty=nameWithType> interfejs.</span><span class="sxs-lookup"><span data-stu-id="2d3f7-109">Define the observer, which is a type that implements the <xref:System.IObserver%601?displayProperty=nameWithType> interface.</span></span> <span data-ttu-id="2d3f7-110">Na przykład poniższy kod definiuje typ o nazwie `TemperatureReporter` , który jest konstruowaną <xref:System.IObserver%601?displayProperty=nameWithType> implementacją z argumentem typu ogólnego `Temperature` .</span><span class="sxs-lookup"><span data-stu-id="2d3f7-110">For example, the following code defines a type named `TemperatureReporter` that is a constructed <xref:System.IObserver%601?displayProperty=nameWithType> implementation with a generic type argument of `Temperature`.</span></span>  
  
     [!code-csharp[Conceptual.ObserverDesign.HowTo#8](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.observerdesign.howto/cs/observer.cs#8)]
     [!code-vb[Conceptual.ObserverDesign.HowTo#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.observerdesign.howto/vb/observer.vb#8)]  
  
2. <span data-ttu-id="2d3f7-111">Jeśli obserwator może zrezygnować z otrzymywania powiadomień, zanim dostawca wywoła jego <xref:System.IObserver%601.OnCompleted%2A?displayProperty=nameWithType> implementację, zdefiniuj zmienną prywatną, która będzie przechowywać <xref:System.IDisposable> implementację zwróconą przez <xref:System.IObservable%601.Subscribe%2A?displayProperty=nameWithType> metodę dostawcy.</span><span class="sxs-lookup"><span data-stu-id="2d3f7-111">If the observer can stop receiving notifications before the provider calls its <xref:System.IObserver%601.OnCompleted%2A?displayProperty=nameWithType> implementation, define a private variable that will hold the <xref:System.IDisposable> implementation returned by the provider's <xref:System.IObservable%601.Subscribe%2A?displayProperty=nameWithType> method.</span></span> <span data-ttu-id="2d3f7-112">Należy również zdefiniować metodę subskrypcji, która wywołuje <xref:System.IObservable%601.Subscribe%2A> metodę dostawcy i zapisuje zwracany <xref:System.IDisposable> obiekt.</span><span class="sxs-lookup"><span data-stu-id="2d3f7-112">You should also define a subscription method that calls the provider's <xref:System.IObservable%601.Subscribe%2A> method and stores the returned <xref:System.IDisposable> object.</span></span> <span data-ttu-id="2d3f7-113">Na przykład poniższy kod definiuje zmienną prywatną o nazwie `unsubscriber` i definiuje `Subscribe` metodę, która wywołuje <xref:System.IObservable%601.Subscribe%2A> metodę dostawcy i przypisuje zwracany obiekt do `unsubscriber` zmiennej.</span><span class="sxs-lookup"><span data-stu-id="2d3f7-113">For example, the following code defines a private variable named `unsubscriber` and defines a `Subscribe` method that calls the provider's <xref:System.IObservable%601.Subscribe%2A> method and assigns the returned object to the `unsubscriber` variable.</span></span>  
  
     [!code-csharp[Conceptual.ObserverDesign.HowTo#9](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.observerdesign.howto/cs/observer.cs#9)]
     [!code-vb[Conceptual.ObserverDesign.HowTo#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.observerdesign.howto/vb/observer.vb#9)]  
  
3. <span data-ttu-id="2d3f7-114">Zdefiniuj metodę, która umożliwia obserwatorowi zatrzymanie otrzymywania powiadomień, zanim dostawca wywoła jego <xref:System.IObserver%601.OnCompleted%2A?displayProperty=nameWithType> implementację, jeśli ta funkcja jest wymagana.</span><span class="sxs-lookup"><span data-stu-id="2d3f7-114">Define a method that enables the observer to stop receiving notifications before the provider calls its <xref:System.IObserver%601.OnCompleted%2A?displayProperty=nameWithType> implementation, if this feature is required.</span></span> <span data-ttu-id="2d3f7-115">W poniższym przykładzie zdefiniowano `Unsubscribe` metodę.</span><span class="sxs-lookup"><span data-stu-id="2d3f7-115">The following example defines an `Unsubscribe` method.</span></span>  
  
     [!code-csharp[Conceptual.ObserverDesign.HowTo#10](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.observerdesign.howto/cs/observer.cs#10)]
     [!code-vb[Conceptual.ObserverDesign.HowTo#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.observerdesign.howto/vb/observer.vb#10)]  
  
4. <span data-ttu-id="2d3f7-116">Podaj implementacje trzech metod zdefiniowanych przez <xref:System.IObserver%601> Interfejs: <xref:System.IObserver%601.OnNext%2A?displayProperty=nameWithType> , <xref:System.IObserver%601.OnError%2A?displayProperty=nameWithType> , i <xref:System.IObserver%601.OnCompleted%2A?displayProperty=nameWithType> .</span><span class="sxs-lookup"><span data-stu-id="2d3f7-116">Provide implementations of the three methods defined by the <xref:System.IObserver%601> interface: <xref:System.IObserver%601.OnNext%2A?displayProperty=nameWithType>, <xref:System.IObserver%601.OnError%2A?displayProperty=nameWithType>, and <xref:System.IObserver%601.OnCompleted%2A?displayProperty=nameWithType>.</span></span> <span data-ttu-id="2d3f7-117">W zależności od dostawcy i potrzeb aplikacji <xref:System.IObserver%601.OnError%2A> <xref:System.IObserver%601.OnCompleted%2A> metody i mogą być implementacjami zastępczymi.</span><span class="sxs-lookup"><span data-stu-id="2d3f7-117">Depending on the provider and the needs of the application, the <xref:System.IObserver%601.OnError%2A> and <xref:System.IObserver%601.OnCompleted%2A> methods can be stub implementations.</span></span> <span data-ttu-id="2d3f7-118">Należy zauważyć, że <xref:System.IObserver%601.OnError%2A> Metoda nie powinna obsłużyć pożądanego <xref:System.Exception> obiektu jako wyjątek, a <xref:System.IObserver%601.OnCompleted%2A> Metoda jest bezpłatna do wywołania <xref:System.IDisposable.Dispose%2A?displayProperty=nameWithType> implementacji dostawcy.</span><span class="sxs-lookup"><span data-stu-id="2d3f7-118">Note that the <xref:System.IObserver%601.OnError%2A> method should not handle the passed <xref:System.Exception> object as an exception, and the <xref:System.IObserver%601.OnCompleted%2A> method is free to call the provider's <xref:System.IDisposable.Dispose%2A?displayProperty=nameWithType> implementation.</span></span> <span data-ttu-id="2d3f7-119">W poniższym przykładzie przedstawiono <xref:System.IObserver%601> implementację `TemperatureReporter` klasy.</span><span class="sxs-lookup"><span data-stu-id="2d3f7-119">The following example shows the <xref:System.IObserver%601> implementation of the `TemperatureReporter` class.</span></span>  
  
     [!code-csharp[Conceptual.ObserverDesign.HowTo#11](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.observerdesign.howto/cs/observer.cs#11)]
     [!code-vb[Conceptual.ObserverDesign.HowTo#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.observerdesign.howto/vb/observer.vb#11)]  
  
## <a name="example"></a><span data-ttu-id="2d3f7-120">Przykład</span><span class="sxs-lookup"><span data-stu-id="2d3f7-120">Example</span></span>  
 <span data-ttu-id="2d3f7-121">Poniższy przykład zawiera kompletny kod źródłowy dla `TemperatureReporter` klasy, który zapewnia <xref:System.IObserver%601> implementację aplikacji monitorującej temperatury.</span><span class="sxs-lookup"><span data-stu-id="2d3f7-121">The following example contains the complete source code for the `TemperatureReporter` class, which provides the <xref:System.IObserver%601> implementation for a temperature monitoring application.</span></span>  
  
 [!code-csharp[Conceptual.ObserverDesign.HowTo#12](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.observerdesign.howto/cs/observer.cs#12)]
 [!code-vb[Conceptual.ObserverDesign.HowTo#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.observerdesign.howto/vb/observer.vb#12)]  
  
## <a name="see-also"></a><span data-ttu-id="2d3f7-122">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="2d3f7-122">See also</span></span>

- <xref:System.IObserver%601>
- [<span data-ttu-id="2d3f7-123">Wzorzec projektowy obserwatora</span><span class="sxs-lookup"><span data-stu-id="2d3f7-123">Observer Design Pattern</span></span>](observer-design-pattern.md)
- [<span data-ttu-id="2d3f7-124">Instrukcje: implementowanie dostawcy</span><span class="sxs-lookup"><span data-stu-id="2d3f7-124">How to: Implement a Provider</span></span>](how-to-implement-a-provider.md)
- [<span data-ttu-id="2d3f7-125">Wzorzec projektowy obserwatora — Najlepsze praktyki</span><span class="sxs-lookup"><span data-stu-id="2d3f7-125">Observer Design Pattern Best Practices</span></span>](observer-design-pattern-best-practices.md)
