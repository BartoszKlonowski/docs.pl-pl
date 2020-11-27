---
title: 'Prognozowanie wdrożeń programu Windows Communication Foundation: ułatwianie integracji w przyszłości'
ms.date: 03/30/2017
ms.assetid: 3028bba8-6355-4ee0-9ecd-c56e614cb474
ms.openlocfilehash: ead28354a3687bcca22a1a0eb5ccc9f15f0c69d2
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96266574"
---
# <a name="anticipating-adopting-the-windows-communication-foundation-easing-future-integration"></a><span data-ttu-id="13401-102">Prognozowanie wdrożeń programu Windows Communication Foundation: ułatwianie integracji w przyszłości</span><span class="sxs-lookup"><span data-stu-id="13401-102">Anticipating Adopting the Windows Communication Foundation: Easing Future Integration</span></span>

<span data-ttu-id="13401-103">Jeśli używasz usługi ASP.NET już dzisiaj i przewidujesz korzystanie z programu WCF w przyszłości, w tym temacie znajdują się wskazówki pozwalające zapewnić zgodność nowych usług sieci Web ASP.NET ze wszystkimi aplikacjami WCF.</span><span class="sxs-lookup"><span data-stu-id="13401-103">If you use ASP.NET today, and anticipate using WCF in the future, this topic provides guidance to ensure that new ASP.NET Web services will work well together with WCF applications.</span></span>  
  
## <a name="general-recommendations"></a><span data-ttu-id="13401-104">Ogólne zalecenia</span><span class="sxs-lookup"><span data-stu-id="13401-104">General Recommendations</span></span>  

 <span data-ttu-id="13401-105">Przyjmij ASP.NET 2,0 dla nowych usług.</span><span class="sxs-lookup"><span data-stu-id="13401-105">Adopt ASP.NET 2.0 for any new services.</span></span> <span data-ttu-id="13401-106">Pozwoli to zapewnić dostęp do ulepszeń i ulepszeń nowej wersji.</span><span class="sxs-lookup"><span data-stu-id="13401-106">Doing so will provide access to the improvements and enhancements of the new version.</span></span> <span data-ttu-id="13401-107">Jednak umożliwi to również możliwość korzystania ze składników ASP.NET 2,0 ze składnikami WCF w tej samej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="13401-107">However, it will also allow for the possibility of using ASP.NET 2.0 components together with WCF components in the same application.</span></span>  
  
## <a name="protocols"></a><span data-ttu-id="13401-108">Protokoły</span><span class="sxs-lookup"><span data-stu-id="13401-108">Protocols</span></span>  

 <span data-ttu-id="13401-109">Użyj nowej funkcji ASP.NET 2.0 do sprawdzania zgodności z profilem Basic WS-I 1,1:</span><span class="sxs-lookup"><span data-stu-id="13401-109">Use ASP.NET 2.0’s new facility for validating conformity to the WS-I Basic Profile 1.1:</span></span>  
  
```csharp  
[WebService(Namespace = "http://tempuri.org/")]  
[WebServiceBinding(  
     ConformsTo = WsiProfiles.BasicProfile1_1,  
     EmitConformanceClaims=true)]  
public interface IEcho  
```  
  
 <span data-ttu-id="13401-110">Usługi sieci Web ASP.NET zgodne ze standardem WS-I Basic Profile 1,1 będą współdziałać z klientami WCF przy użyciu wstępnie zdefiniowanych powiązań programu WCF <xref:System.ServiceModel.BasicHttpBinding> .</span><span class="sxs-lookup"><span data-stu-id="13401-110">ASP.NET Web services that conform to WS-I Basic Profile 1.1 will be interoperable with WCF clients by using WCF predefined binding, <xref:System.ServiceModel.BasicHttpBinding>.</span></span>  
  
## <a name="service-development"></a><span data-ttu-id="13401-111">Opracowywanie usług</span><span class="sxs-lookup"><span data-stu-id="13401-111">Service Development</span></span>  

 <span data-ttu-id="13401-112">Należy unikać używania <xref:System.Web.Services.Protocols.SoapDocumentServiceAttribute> atrybutu, aby komunikaty były kierowane do metod opartych na w pełni kwalifikowanej nazwie elementu treści komunikatu protokołu SOAP, a nie w nagłówku HTTP SoapAction.</span><span class="sxs-lookup"><span data-stu-id="13401-112">Avoid using the <xref:System.Web.Services.Protocols.SoapDocumentServiceAttribute> attribute to have messages routed to methods based on the fully-qualified name of the body element of the SOAP message rather than the SOAPAction HTTP header.</span></span> <span data-ttu-id="13401-113">Funkcja WCF używa nagłówka HTTP SOAPAction dla komunikatów routingu.</span><span class="sxs-lookup"><span data-stu-id="13401-113">WCF uses the SOAPAction HTTP header for routing messages.</span></span>  
  
## <a name="data-representation"></a><span data-ttu-id="13401-114">Reprezentacja danych</span><span class="sxs-lookup"><span data-stu-id="13401-114">Data Representation</span></span>  

 <span data-ttu-id="13401-115">KOD XML, do którego <xref:System.Xml.Serialization.XmlSerializer> serializowany jest typ domyślnie jest semantycznie identyczny z XML, do którego jest <xref:System.Runtime.Serialization.DataContractSerializer> serializowany typ, pod warunkiem, że przestrzeń nazw dla kodu XML jest jawnie zdefiniowana.</span><span class="sxs-lookup"><span data-stu-id="13401-115">The XML into which <xref:System.Xml.Serialization.XmlSerializer> serializes a type by default is semantically identical to the XML into which the <xref:System.Runtime.Serialization.DataContractSerializer> serializes a type, provided the namespace for the XML is explicitly defined.</span></span> <span data-ttu-id="13401-116">Podczas definiowania typu danych do użycia z usługami sieci Web ASP.NET w celu przewidzenia wdrożenia WCF w przyszłości wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="13401-116">When defining a data type for use with ASP.NET Web services in anticipation of adopting WCF in the future, do the following:</span></span>  
  
1. <span data-ttu-id="13401-117">Zdefiniuj typ przy użyciu klas .NET Framework, a nie schematu XML.</span><span class="sxs-lookup"><span data-stu-id="13401-117">Define the type using .NET Framework classes rather than XML Schema.</span></span>  
  
2. <span data-ttu-id="13401-118">Dodaj tylko <xref:System.SerializableAttribute> i <xref:System.Xml.Serialization.XmlRootAttribute> do klasy, używając tej ostatniej, aby jawnie zdefiniować przestrzeń nazw dla tego typu.</span><span class="sxs-lookup"><span data-stu-id="13401-118">Add only the <xref:System.SerializableAttribute> and the <xref:System.Xml.Serialization.XmlRootAttribute> to the class, using the latter to explicitly define the namespace for the type.</span></span> <span data-ttu-id="13401-119">Nie dodawaj dodatkowych atrybutów z <xref:System.Xml.Serialization> przestrzeni nazw, aby kontrolować sposób tłumaczenia klasy .NET Framework na XML.</span><span class="sxs-lookup"><span data-stu-id="13401-119">Do no add additional attributes from the <xref:System.Xml.Serialization> namespace to control how the .NET Framework class is to be translated into XML.</span></span>  
  
 <span data-ttu-id="13401-120">Przyjmując takie podejście, powinno być możliwe późniejsze przekazanie klas .NET do kontraktów danych z dodaniem <xref:System.Runtime.Serialization.DataContractAttribute> i <xref:System.Runtime.Serialization.DataMemberAttribute> bez znacząco zmiany kodu XML, do którego klasy są serializowane do transmisji.</span><span class="sxs-lookup"><span data-stu-id="13401-120">By adopting this approach, you should be able to later make the .NET classes into data contracts with the addition of the <xref:System.Runtime.Serialization.DataContractAttribute> and <xref:System.Runtime.Serialization.DataMemberAttribute> without significantly altering the XML into which the classes are serialized for transmission.</span></span> <span data-ttu-id="13401-121">Typy używane w komunikatach przez usługi sieci Web ASP.NET będą mogły być przetwarzane jako Kontrakty danych przez aplikacje WCF, a wśród innych korzyści, lepsza wydajność aplikacji WCF.</span><span class="sxs-lookup"><span data-stu-id="13401-121">The types used in messages by ASP.NET Web services will be able to be processed as data contracts by WCF applications, yielding, amongst other benefits, better performance in WCF applications.</span></span>  
  
## <a name="security"></a><span data-ttu-id="13401-122">Zabezpieczenia</span><span class="sxs-lookup"><span data-stu-id="13401-122">Security</span></span>  

 <span data-ttu-id="13401-123">Należy unikać używania opcji uwierzytelniania zapewnianych przez Internet Information Services (IIS).</span><span class="sxs-lookup"><span data-stu-id="13401-123">Avoid using the authentication options provided by Internet Information Services (IIS).</span></span> <span data-ttu-id="13401-124">Klienci WCF nie obsługują tych funkcji.</span><span class="sxs-lookup"><span data-stu-id="13401-124">WCF clients do not support them.</span></span> <span data-ttu-id="13401-125">Jeśli usługa musi być zabezpieczona, użyj opcji dostarczonych przez program WCF, ponieważ te opcje są bogatsze i są oparte na protokołach standardowych.</span><span class="sxs-lookup"><span data-stu-id="13401-125">If a service needs to be secured, use the options provided by WCF, because these options are richer and are based on standard protocols.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="13401-126">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="13401-126">See also</span></span>

- [<span data-ttu-id="13401-127">Prognozowanie wdrożeń programu Windows Communication Foundation: ułatwianie migracji w przyszłości</span><span class="sxs-lookup"><span data-stu-id="13401-127">Anticipating Adopting the Windows Communication Foundation: Easing Future Migration</span></span>](anticipating-adopting-wcf-migration.md)
