---
title: 'Instrukcje: ustawianie zasad pamięci podręcznej dla żądania'
description: Dowiedz się, jak ustawić zasady pamięci podręcznej dla żądania w .NET Framework. Te zasady pamięci podręcznej umożliwiają użycie zasobu z pamięci podręcznej przez maksymalnie dobę.
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- request cache policies
ms.assetid: 39c15e40-586b-4ac9-9cce-146f74b7e545
ms.openlocfilehash: cbb8f2eaf618cb9faaca1375d829478a645962a7
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96253417"
---
# <a name="how-to-set-cache-policy-for-a-request"></a><span data-ttu-id="601d3-104">Instrukcje: ustawianie zasad pamięci podręcznej dla żądania</span><span class="sxs-lookup"><span data-stu-id="601d3-104">How to: Set Cache Policy for a Request</span></span>

<span data-ttu-id="601d3-105">W poniższym przykładzie pokazano, jak ustawić zasady pamięci podręcznej dla żądania.</span><span class="sxs-lookup"><span data-stu-id="601d3-105">The following example demonstrates setting a cache policy for a request.</span></span> <span data-ttu-id="601d3-106">Przykładowe dane wejściowe to identyfikator URI, taki jak `http://www.contoso.com/` .</span><span class="sxs-lookup"><span data-stu-id="601d3-106">The example input is a URI such as `http://www.contoso.com/`.</span></span>  
  
## <a name="example"></a><span data-ttu-id="601d3-107">Przykład</span><span class="sxs-lookup"><span data-stu-id="601d3-107">Example</span></span>  

 <span data-ttu-id="601d3-108">Poniższy przykład kodu tworzy zasady pamięci podręcznej, które umożliwiają użycie żądanego zasobu z pamięci podręcznej, jeśli nie było w pamięci podręcznej dłużej niż jeden dzień.</span><span class="sxs-lookup"><span data-stu-id="601d3-108">The following code example creates a cache policy that allows the requested resource to be used from the cache if it has not been in the cache for longer than one day.</span></span> <span data-ttu-id="601d3-109">Przykład wyświetla komunikat wskazujący, czy zasób został użyty z pamięci podręcznej, na przykład,, `"The response was retrieved from the cache : False."` a następnie wyświetla zasób.</span><span class="sxs-lookup"><span data-stu-id="601d3-109">The example displays a message that indicates whether the resource was used from the cache—for example, `"The response was retrieved from the cache : False."`—and then displays the resource.</span></span> <span data-ttu-id="601d3-110">Żądanie może być spełnione przez dowolną pamięć podręczną między klientem i serwerem.</span><span class="sxs-lookup"><span data-stu-id="601d3-110">A request can be fulfilled by any cache between the client and server.</span></span>  
  
```csharp  
using System;  
using System.Net;  
using System.Net.Cache;  
using System.IO;  
  
namespace Examples.System.Net.Cache  
{  
    public class CacheExample  
    {
        public static void UseCacheForOneDay(Uri resource)  
        {  
            // Create a policy that allows items in the cache  
            // to be used if they have been cached one day or less.  
            HttpRequestCachePolicy requestPolicy =
                new HttpRequestCachePolicy (HttpCacheAgeControl.MaxAge,  
                TimeSpan.FromDays(1));  
  
            WebRequest request = WebRequest.Create (resource);  
            // Set the policy for this request only.  
            request.CachePolicy = requestPolicy;  
            HttpWebResponse response = (HttpWebResponse)request.GetResponse();  
            // Determine whether the response was retrieved from the cache.  
            Console.WriteLine ("The response was retrieved from the cache : {0}.",  
               response.IsFromCache);  
            Stream s = response.GetResponseStream ();  
            StreamReader reader = new StreamReader (s);  
            // Display the requested resource.  
            Console.WriteLine(reader.ReadToEnd());  
            reader.Close ();  
            s.Close();  
            response.Close();  
        }  
        public static void Main(string[] args)  
        {  
            if (args == null || args.Length != 1)  
            {  
                Console.WriteLine ("You must specify the URI to retrieve.");  
                return;  
            }  
            UseCacheForOneDay (new Uri(args[0]));  
        }  
    }  
}  
```  
  
```vb  
Imports System  
Imports System.Net  
Imports System.Net.Cache  
Imports System.IO  
Namespace Examples.System.Net.Cache  
    Public Class CacheExample  
        Public Shared Sub UseCacheForOneDay(ByVal resource As Uri)  
            ' Create a policy that allows items in the cache  
            ' to be used if they have been cached one day or less.  
            Dim requestPolicy As New HttpRequestCachePolicy _  
                  (HttpCacheAgeControl.MaxAge, TimeSpan.FromDays(1))  
            Dim request As WebRequest = WebRequest.Create(resource)  
            ' Set the policy for this request only.  
            request.CachePolicy = requestPolicy  
            Dim response As HttpWebResponse = _  
             CType(request.GetResponse(), HttpWebResponse)  
            ' Determine whether the response was retrieved from the cache.  
            Console.WriteLine("The response was retrieved from the cache : {0}.", _  
                response.IsFromCache)  
            Dim s As Stream = response.GetResponseStream()  
            Dim reader As New StreamReader(s)  
            ' Display the requested resource.  
            Console.WriteLine(reader.ReadToEnd())  
            reader.Close()  
            s.Close()  
            response.Close()  
        End Sub  
        Public Shared Sub Main(ByVal args() As String)  
            If args Is Nothing OrElse args.Length <> 1 Then  
                Console.WriteLine("You must specify the URI to retrieve.")  
                Return  
            End If  
            UseCacheForOneDay(New Uri(args(0)))  
        End Sub  
    End Class  
End Namespace  
```  
  
## <a name="see-also"></a><span data-ttu-id="601d3-111">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="601d3-111">See also</span></span>

- [<span data-ttu-id="601d3-112">Zarządzanie pamięcią podręczną dla aplikacji sieciowych</span><span class="sxs-lookup"><span data-stu-id="601d3-112">Cache Management for Network Applications</span></span>](cache-management-for-network-applications.md)
- [<span data-ttu-id="601d3-113">Zasady pamięci podręcznej</span><span class="sxs-lookup"><span data-stu-id="601d3-113">Cache Policy</span></span>](cache-policy.md)
- [<span data-ttu-id="601d3-114">Zasady pamięci podręcznej oparte na lokalizacji</span><span class="sxs-lookup"><span data-stu-id="601d3-114">Location-Based Cache Policies</span></span>](location-based-cache-policies.md)
- [<span data-ttu-id="601d3-115">Zasady pamięci podręcznej oparte na czasie</span><span class="sxs-lookup"><span data-stu-id="601d3-115">Time-Based Cache Policies</span></span>](time-based-cache-policies.md)
- [<span data-ttu-id="601d3-116">\<requestCaching> — Element (Ustawienia sieci)</span><span class="sxs-lookup"><span data-stu-id="601d3-116">\<requestCaching> Element (Network Settings)</span></span>](../configure-apps/file-schema/network/requestcaching-element-network-settings.md)
