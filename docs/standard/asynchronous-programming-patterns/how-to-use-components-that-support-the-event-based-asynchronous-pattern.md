---
title: 'Instrukcje: Używanie składników obsługujących wzorzec asynchroniczny oparty na zdarzeniach'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Event-based Asynchronous Pattern
- ProgressChangedEventArgs class
- BackgroundWorker component
- events [.NET Framework], asynchronous
- Asynchronous Pattern
- AsyncOperationManager class
- threading [.NET Framework], asynchronous features
- components [.NET Framework], asynchronous
- AsyncOperation class
- threading [Windows Forms], asynchronous features
- AsyncCompletedEventArgs class
ms.assetid: 35e9549c-1568-4768-ad07-17cc6dff11e1
ms.openlocfilehash: c41a695226068615efca5132985e50503060148b
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/15/2020
ms.locfileid: "90555669"
---
# <a name="how-to-use-components-that-support-the-event-based-asynchronous-pattern"></a><span data-ttu-id="0a22b-102">Instrukcje: Używanie składników obsługujących wzorzec asynchroniczny oparty na zdarzeniach</span><span class="sxs-lookup"><span data-stu-id="0a22b-102">How to: Use Components That Support the Event-based Asynchronous Pattern</span></span>
<span data-ttu-id="0a22b-103">Wiele składników oferuje możliwość wykonywania pracy asynchronicznie.</span><span class="sxs-lookup"><span data-stu-id="0a22b-103">Many components provide you with the option of performing their work asynchronously.</span></span> <span data-ttu-id="0a22b-104"><xref:System.Media.SoundPlayer>Składniki i <xref:System.Windows.Forms.PictureBox> umożliwiają na przykład ładowanie dźwięków i obrazów "w tle", podczas gdy główny wątek nadal działa bez przeszkód.</span><span class="sxs-lookup"><span data-stu-id="0a22b-104">The <xref:System.Media.SoundPlayer> and <xref:System.Windows.Forms.PictureBox> components, for example, enable you to load sounds and images "in the background" while your main thread continues running without interruption.</span></span>  
  
 <span data-ttu-id="0a22b-105">Korzystanie z metod asynchronicznych na klasie, która obsługuje [oparte na zdarzeniach](event-based-asynchronous-pattern-overview.md) , można jak równie łatwo dołączać obsługę zdarzeń do zdarzenia**ukończenia** _MethodName_przez składnik, podobnie jak w przypadku dowolnego innego zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="0a22b-105">Using asynchronous methods on a class that supports the [Event-based Asynchronous Pattern Overview](event-based-asynchronous-pattern-overview.md) can be as simple as attaching an event handler to the component's _MethodName_**Completed** event, just as you would for any other event.</span></span> <span data-ttu-id="0a22b-106">Po wywołaniu metody**asynchronicznej** _MethodName_aplikacja będzie kontynuowała pracę bez przeszkód do momentu zgłoszenia zdarzenia _MethodName_**ukończone** .</span><span class="sxs-lookup"><span data-stu-id="0a22b-106">When you call the _MethodName_**Async** method, your application will continue running without interruption until the _MethodName_**Completed** event is raised.</span></span> <span data-ttu-id="0a22b-107">W programie obsługi zdarzeń można sprawdzić <xref:System.ComponentModel.AsyncCompletedEventArgs> parametr, aby określić, czy operacja asynchroniczna została ukończona pomyślnie, czy też została anulowana.</span><span class="sxs-lookup"><span data-stu-id="0a22b-107">In your event handler, you can examine the <xref:System.ComponentModel.AsyncCompletedEventArgs> parameter to determine if the asynchronous operation successfully completed or if it was canceled.</span></span>  
  
 <span data-ttu-id="0a22b-108">Aby uzyskać więcej informacji o korzystaniu z programów obsługi zdarzeń, zobacz [Omówienie obsługi zdarzeń](/dotnet/desktop/winforms/event-handlers-overview-windows-forms).</span><span class="sxs-lookup"><span data-stu-id="0a22b-108">For more information about using event handlers, see [Event Handlers Overview](/dotnet/desktop/winforms/event-handlers-overview-windows-forms).</span></span>  
  
 <span data-ttu-id="0a22b-109">Poniższa procedura pokazuje, jak używać funkcji asynchronicznego ładowania obrazu <xref:System.Windows.Forms.PictureBox> formantu.</span><span class="sxs-lookup"><span data-stu-id="0a22b-109">The following procedure shows how to use the asynchronous image-loading capability of a <xref:System.Windows.Forms.PictureBox> control.</span></span>  
  
### <a name="to-enable-a-picturebox-control-to-asynchronously-load-an-image"></a><span data-ttu-id="0a22b-110">Aby włączyć formant PictureBox do asynchronicznego ładowania obrazu</span><span class="sxs-lookup"><span data-stu-id="0a22b-110">To enable a PictureBox control to asynchronously load an image</span></span>  
  
1. <span data-ttu-id="0a22b-111">Utwórz wystąpienie <xref:System.Windows.Forms.PictureBox> składnika w formularzu.</span><span class="sxs-lookup"><span data-stu-id="0a22b-111">Create an instance of the <xref:System.Windows.Forms.PictureBox> component in your form.</span></span>  
  
2. <span data-ttu-id="0a22b-112">Przypisz do zdarzenia procedurę obsługi zdarzeń <xref:System.Windows.Forms.PictureBox.LoadCompleted> .</span><span class="sxs-lookup"><span data-stu-id="0a22b-112">Assign an event handler to the <xref:System.Windows.Forms.PictureBox.LoadCompleted> event.</span></span>  
  
     <span data-ttu-id="0a22b-113">Sprawdź pod kątem błędów, które mogły wystąpić podczas pobierania asynchronicznego w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="0a22b-113">Check for any errors that may have occurred during the asynchronous download here.</span></span> <span data-ttu-id="0a22b-114">Jest to również miejsce, w którym można sprawdzić, czy jest to możliwe.</span><span class="sxs-lookup"><span data-stu-id="0a22b-114">This is also where you check for cancellation.</span></span>  
  
     [!code-csharp[System.Windows.Forms.PictureBox.LoadAsync#2](snippets/component-that-supports-the-event-based-asynchronous-pattern/csharp/Form1.cs#2)]
     [!code-vb[System.Windows.Forms.PictureBox.LoadAsync#2](snippets/component-that-supports-the-event-based-asynchronous-pattern/vb/Form1.vb#2)]  
  
     [!code-csharp[System.Windows.Forms.PictureBox.LoadAsync#5](snippets/component-that-supports-the-event-based-asynchronous-pattern/csharp/Form1.cs#5)]
     [!code-vb[System.Windows.Forms.PictureBox.LoadAsync#5](snippets/component-that-supports-the-event-based-asynchronous-pattern/vb/Form1.vb#5)]  
  
3. <span data-ttu-id="0a22b-115">Dodaj dwa przyciski, nazywane `loadButton` i `cancelLoadButton` , do formularza.</span><span class="sxs-lookup"><span data-stu-id="0a22b-115">Add two buttons, called `loadButton` and `cancelLoadButton`, to your form.</span></span> <span data-ttu-id="0a22b-116">Dodaj <xref:System.Windows.Forms.Control.Click> programy obsługi zdarzeń, aby rozpocząć i anulować pobieranie.</span><span class="sxs-lookup"><span data-stu-id="0a22b-116">Add <xref:System.Windows.Forms.Control.Click> event handlers to start and cancel the download.</span></span>  
  
     [!code-csharp[System.Windows.Forms.PictureBox.LoadAsync#3](snippets/component-that-supports-the-event-based-asynchronous-pattern/csharp/Form1.cs#3)]
     [!code-vb[System.Windows.Forms.PictureBox.LoadAsync#3](snippets/component-that-supports-the-event-based-asynchronous-pattern/vb/Form1.vb#3)]  
  
     [!code-csharp[System.Windows.Forms.PictureBox.LoadAsync#4](snippets/component-that-supports-the-event-based-asynchronous-pattern/csharp/Form1.cs#4)]
     [!code-vb[System.Windows.Forms.PictureBox.LoadAsync#4](snippets/component-that-supports-the-event-based-asynchronous-pattern/vb/Form1.vb#4)]  
  
4. <span data-ttu-id="0a22b-117">Uruchom aplikację.</span><span class="sxs-lookup"><span data-stu-id="0a22b-117">Run your application.</span></span>  
  
     <span data-ttu-id="0a22b-118">Po pobraniu obrazu będzie można swobodnie przenieść formularz, zminimalizować go i zmaksymalizować.</span><span class="sxs-lookup"><span data-stu-id="0a22b-118">As the image download proceeds, you can move the form freely, minimize it, and maximize it.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="0a22b-119">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="0a22b-119">See also</span></span>

- [<span data-ttu-id="0a22b-120">Instrukcje: uruchamianie operacji w tle</span><span class="sxs-lookup"><span data-stu-id="0a22b-120">How to: Run an Operation in the Background</span></span>](/dotnet/desktop/winforms/controls/how-to-run-an-operation-in-the-background)
- [<span data-ttu-id="0a22b-121">Asynchroniczny wzorzec oparty na zdarzeniach — przegląd</span><span class="sxs-lookup"><span data-stu-id="0a22b-121">Event-based Asynchronous Pattern Overview</span></span>](event-based-asynchronous-pattern-overview.md)
