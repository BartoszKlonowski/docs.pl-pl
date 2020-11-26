---
title: Używanie synchronicznego gniazda klienta
description: W tym przykładzie pokazano synchroniczne gniazdo klienta w .NET Framework, które wstrzymuje program aplikacji podczas kończenia operacji sieciowej.
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- application protocols, sockets
- sending data, sockets
- data requests, sockets
- requesting data from Internet, sockets
- synchronous client sockets
- Socket class, synchronous client sockets
- receiving data, sockets
- sockets, synchronous client sockets
- protocols, sockets
- Internet, sockets
- client sockets
ms.assetid: 945d00c6-7202-466c-9df9-140b84156d43
ms.openlocfilehash: f198f283f2acfdcfbafed25baecb02a64e9d1e26
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96236315"
---
# <a name="using-a-synchronous-client-socket"></a><span data-ttu-id="1e4e4-103">Używanie synchronicznego gniazda klienta</span><span class="sxs-lookup"><span data-stu-id="1e4e4-103">Using a Synchronous Client Socket</span></span>

<span data-ttu-id="1e4e4-104">Synchroniczne gniazdo klienta zawiesza program aplikacji podczas kończenia operacji sieciowej.</span><span class="sxs-lookup"><span data-stu-id="1e4e4-104">A synchronous client socket suspends the application program while the network operation completes.</span></span> <span data-ttu-id="1e4e4-105">Gniazda synchroniczne nie są odpowiednie dla aplikacji, które intensywnie wykorzystują sieć do ich obsługi, ale mogą zapewnić prosty dostęp do usług sieciowych dla innych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1e4e4-105">Synchronous sockets are not suitable for applications that make heavy use of the network for their operation, but they can enable simple access to network services for other applications.</span></span>  
  
 <span data-ttu-id="1e4e4-106">Aby wysłać dane, Przekaż tablicę bajtową do jednej z <xref:System.Net.Sockets.Socket> metod wysyłania danych klasy ( <xref:System.Net.Sockets.Socket.Send%2A> i <xref:System.Net.Sockets.Socket.SendTo%2A> ).</span><span class="sxs-lookup"><span data-stu-id="1e4e4-106">To send data, pass a byte array to one of the <xref:System.Net.Sockets.Socket> class's send-data methods (<xref:System.Net.Sockets.Socket.Send%2A> and <xref:System.Net.Sockets.Socket.SendTo%2A>).</span></span> <span data-ttu-id="1e4e4-107">Poniższy przykład koduje ciąg w buforze tablicy bajtów przy użyciu <xref:System.Text.Encoding.ASCII%2A?displayProperty=nameWithType> właściwości, a następnie przesyła bufor do urządzenia sieciowego przy użyciu metody **send** .</span><span class="sxs-lookup"><span data-stu-id="1e4e4-107">The following example encodes a string into a byte array buffer using the <xref:System.Text.Encoding.ASCII%2A?displayProperty=nameWithType> property and then transmits the buffer to the network device using the **Send** method.</span></span> <span data-ttu-id="1e4e4-108">Metoda **send** zwraca liczbę bajtów wysłanych do urządzenia sieciowego.</span><span class="sxs-lookup"><span data-stu-id="1e4e4-108">The **Send** method returns the number of bytes sent to the network device.</span></span>  
  
```vb  
Dim msg As Byte() = _  
    System.Text.Encoding.ASCII.GetBytes("This is a test.")  
Dim bytesSent As Integer = s.Send(msg)  
```  
  
```csharp  
byte[] msg = System.Text.Encoding.ASCII.GetBytes("This is a test");  
int bytesSent = s.Send(msg);  
```  
  
 <span data-ttu-id="1e4e4-109">Metoda **send** usuwa bajty z buforu i kolejkuje je za pomocą interfejsu sieciowego do wysłania do urządzenia sieciowego.</span><span class="sxs-lookup"><span data-stu-id="1e4e4-109">The **Send** method removes the bytes from the buffer and queues them with the network interface to be sent to the network device.</span></span> <span data-ttu-id="1e4e4-110">Interfejs sieciowy może nie wysłać danych natychmiast, ale zostanie on wysłany ostatecznie, o ile połączenie zostanie normalnie zamknięte przy użyciu <xref:System.Net.Sockets.Socket.Shutdown%2A> metody.</span><span class="sxs-lookup"><span data-stu-id="1e4e4-110">The network interface might not send the data immediately, but it will send it eventually, as long as the connection is closed normally with the <xref:System.Net.Sockets.Socket.Shutdown%2A> method.</span></span>  
  
 <span data-ttu-id="1e4e4-111">Aby odbierać dane z urządzenia sieciowego, należy przekazać bufor do jednej z metod odbioru danych klasy **gniazda** ( <xref:System.Net.Sockets.Socket.Receive%2A> i <xref:System.Net.Sockets.Socket.ReceiveFrom%2A> ).</span><span class="sxs-lookup"><span data-stu-id="1e4e4-111">To receive data from a network device, pass a buffer to one of the **Socket** class's receive-data methods (<xref:System.Net.Sockets.Socket.Receive%2A> and <xref:System.Net.Sockets.Socket.ReceiveFrom%2A>).</span></span> <span data-ttu-id="1e4e4-112">Gniazda synchroniczne zawieszają aplikację do momentu odebrania bajtów z sieci lub do momentu zamknięcia gniazda.</span><span class="sxs-lookup"><span data-stu-id="1e4e4-112">Synchronous sockets will suspend the application until bytes are received from the network or until the socket is closed.</span></span> <span data-ttu-id="1e4e4-113">Poniższy przykład odbiera dane z sieci, a następnie wyświetla je w konsoli programu.</span><span class="sxs-lookup"><span data-stu-id="1e4e4-113">The following example receives data from the network and then displays it on the console.</span></span> <span data-ttu-id="1e4e4-114">W przykładzie założono, że dane pochodzące z sieci są tekstem zakodowanym w formacie ASCII.</span><span class="sxs-lookup"><span data-stu-id="1e4e4-114">The example assumes that the data coming from the network is ASCII-encoded text.</span></span> <span data-ttu-id="1e4e4-115">Metoda **Receive** zwraca liczbę bajtów odebranych z sieci.</span><span class="sxs-lookup"><span data-stu-id="1e4e4-115">The **Receive** method returns the number of bytes received from the network.</span></span>  
  
```vb  
Dim bytes(1024) As Byte  
Dim bytesRec = s.Receive(bytes)  
Console.WriteLine("Echoed text = {0}", _  
    System.Text.Encoding.ASCII.GetString(bytes, 0, bytesRec))  
```  
  
```csharp  
byte[] bytes = new byte[1024];  
int bytesRec = s.Receive(bytes);  
Console.WriteLine("Echoed text = {0}",  
    System.Text.Encoding.ASCII.GetString(bytes, 0, bytesRec));  
```  
  
 <span data-ttu-id="1e4e4-116">Gdy gniazdo nie jest już potrzebne, należy je zwolnić, wywołując <xref:System.Net.Sockets.Socket.Shutdown%2A> metodę, a następnie wywołując metodę **Close** .</span><span class="sxs-lookup"><span data-stu-id="1e4e4-116">When the socket is no longer needed, you need to release it by calling the <xref:System.Net.Sockets.Socket.Shutdown%2A> method and then calling the **Close** method.</span></span> <span data-ttu-id="1e4e4-117">Poniższy przykład zwalnia **gniazdo**.</span><span class="sxs-lookup"><span data-stu-id="1e4e4-117">The following example releases a **Socket**.</span></span> <span data-ttu-id="1e4e4-118"><xref:System.Net.Sockets.SocketShutdown>Wyliczenie definiuje stałe wskazujące, czy gniazdo powinno być zamknięte do wysłania, do odbioru lub dla obu.</span><span class="sxs-lookup"><span data-stu-id="1e4e4-118">The <xref:System.Net.Sockets.SocketShutdown> enumeration defines constants that indicate whether the socket should be closed for sending, for receiving, or for both.</span></span>  
  
```vb  
s.Shutdown(SocketShutdown.Both)  
s.Close()  
```  
  
```csharp  
s.Shutdown(SocketShutdown.Both);  
s.Close();  
```  
  
## <a name="see-also"></a><span data-ttu-id="1e4e4-119">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="1e4e4-119">See also</span></span>

- [<span data-ttu-id="1e4e4-120">Używanie asynchronicznego gniazda klienta</span><span class="sxs-lookup"><span data-stu-id="1e4e4-120">Using an Asynchronous Client Socket</span></span>](using-an-asynchronous-client-socket.md)
- [<span data-ttu-id="1e4e4-121">Nasłuchiwanie przy użyciu gniazd</span><span class="sxs-lookup"><span data-stu-id="1e4e4-121">Listening with Sockets</span></span>](listening-with-sockets.md)
- [<span data-ttu-id="1e4e4-122">Przykład synchronicznego gniazda klienta</span><span class="sxs-lookup"><span data-stu-id="1e4e4-122">Synchronous Client Socket Example</span></span>](synchronous-client-socket-example.md)
