---
title: Konfigurowanie Internetowych usług informacyjnych 7.0 na potrzeby programu Windows Communication Foundation
ms.date: 03/30/2017
ms.assetid: 1050d395-092e-44d3-b4ba-66be3b039ffb
ms.openlocfilehash: 865e19d6626846481347274774d3ea59f2f7ecdd
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96284215"
---
# <a name="configuring-internet-information-services-70-for-windows-communication-foundation"></a><span data-ttu-id="defc7-102">Konfigurowanie Internetowych usług informacyjnych 7.0 na potrzeby programu Windows Communication Foundation</span><span class="sxs-lookup"><span data-stu-id="defc7-102">Configuring Internet Information Services 7.0 for Windows Communication Foundation</span></span>

<span data-ttu-id="defc7-103">Internet Information Services (IIS) 7,0 ma modularny projekt, który umożliwia selektywne instalowanie składników, które są wymagane.</span><span class="sxs-lookup"><span data-stu-id="defc7-103">Internet Information Services (IIS) 7.0 has a modular design that allows you to selectively install components that are required.</span></span> <span data-ttu-id="defc7-104">Ten projekt jest oparty na nowej technologii componentization opartej na manifestach wprowadzonej w systemie Windows Vista.</span><span class="sxs-lookup"><span data-stu-id="defc7-104">This design is based on the new manifest-driven componentization technology introduced in Windows Vista.</span></span> <span data-ttu-id="defc7-105">Istnieje ponad 40 autonomicznych składników funkcji usług IIS 7,0, które mogą być instalowane niezależnie.</span><span class="sxs-lookup"><span data-stu-id="defc7-105">There are more than 40 standalone feature components of IIS 7.0 that can be installed independently.</span></span> <span data-ttu-id="defc7-106">Dzięki temu specjaliści IT mogą łatwo dostosować instalację zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="defc7-106">This allows IT professionals to easily customize the installation as required.</span></span> <span data-ttu-id="defc7-107">W tym temacie omówiono sposób konfigurowania usług IIS 7,0 do użycia z programem Windows Communication Foundation (WCF) i określania, które składniki są wymagane.</span><span class="sxs-lookup"><span data-stu-id="defc7-107">This topic discusses how to configure IIS 7.0 for use with Windows Communication Foundation (WCF) and determine which components are required.</span></span>

## <a name="minimal-installation-installing-was"></a><span data-ttu-id="defc7-108">Minimalna instalacja: Instalacja została</span><span class="sxs-lookup"><span data-stu-id="defc7-108">Minimal Installation: Installing WAS</span></span>

 <span data-ttu-id="defc7-109">Minimalna instalacja całego pakietu usług IIS 7,0 to zainstalowanie usługi aktywacji procesów systemu Windows (WAS).</span><span class="sxs-lookup"><span data-stu-id="defc7-109">The minimal installation of the whole IIS 7.0 package is to install the Windows Process Activation Service (WAS).</span></span> <span data-ttu-id="defc7-110">BYŁA funkcją autonomiczną i jest jedyną funkcją z usług IIS 7,0, która jest dostępna dla wszystkich systemów operacyjnych Windows Vista (Home Basic, Home Premium, Business i Ultimate i Enterprise).</span><span class="sxs-lookup"><span data-stu-id="defc7-110">WAS is a standalone feature and it is the only feature from the IIS 7.0 that is available for all Windows Vista operating systems (Home Basic, Home Premium, Business, and Ultimate and Enterprise).</span></span>

 <span data-ttu-id="defc7-111">W panelu sterowania kliknij pozycję **programy** , a następnie kliknij pozycję **Włącz lub wyłącz funkcje systemu Windows** , które są wyświetlane w obszarze **programy i funkcje**, składnik został wyświetlony na liście tak jak na poniższej ilustracji.</span><span class="sxs-lookup"><span data-stu-id="defc7-111">From the Control Panel, click **Programs** and then click **Turn Windows features on or off** which is listed under **Programs and Features**, the WAS component is shown in the list as in the following illustration.</span></span>

 <span data-ttu-id="defc7-112">![Włącz lub wyłącz funkcje okna dialogowego](media/wcfc-turnfeaturesonoroffs.gif "wcfc_TurnFeaturesOnOrOffs")</span><span class="sxs-lookup"><span data-stu-id="defc7-112">![Turn Features On or Off Dialog](media/wcfc-turnfeaturesonoroffs.gif "wcfc_TurnFeaturesOnOrOffs")</span></span>

 <span data-ttu-id="defc7-113">Ta funkcja ma następujące składniki podrzędne:</span><span class="sxs-lookup"><span data-stu-id="defc7-113">This feature has the following sub-components:</span></span>

- <span data-ttu-id="defc7-114">Środowisko .NET</span><span class="sxs-lookup"><span data-stu-id="defc7-114">.NET Environment</span></span>

- <span data-ttu-id="defc7-115">Interfejsy API konfiguracji</span><span class="sxs-lookup"><span data-stu-id="defc7-115">Configuration APIs</span></span>

- <span data-ttu-id="defc7-116">Model procesów</span><span class="sxs-lookup"><span data-stu-id="defc7-116">Process Model</span></span>

 <span data-ttu-id="defc7-117">W przypadku wybrania węzła głównego elementu, domyślnie sprawdzany jest tylko podrzędny węzeł **modelu procesu** .</span><span class="sxs-lookup"><span data-stu-id="defc7-117">If you select the root node of WAS, only the **Process Model** sub-node is checked by default.</span></span> <span data-ttu-id="defc7-118">Należy pamiętać, że instalacja jest przeprowadzana tylko w przypadku instalacji, ponieważ nie ma żadnych obsługi dla serwera sieci Web.</span><span class="sxs-lookup"><span data-stu-id="defc7-118">Please note that with this installation you are only installing WAS, because there is no support for a Web server.</span></span>

 <span data-ttu-id="defc7-119">Aby program WCF lub dowolna aplikacja ASP.NET działała, zaznacz pole wyboru **środowisko .NET** .</span><span class="sxs-lookup"><span data-stu-id="defc7-119">To make WCF or any ASP.NET application work, check the **.NET Environment** checkbox.</span></span> <span data-ttu-id="defc7-120">Oznacza to, że wszystkie składniki były wymagane do poprawnego działania usług WCF i ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="defc7-120">This means that all of WAS components are required to make WCF and ASP.NET to work well.</span></span> <span data-ttu-id="defc7-121">Są one automatycznie sprawdzane po zainstalowaniu któregokolwiek z tych składników.</span><span class="sxs-lookup"><span data-stu-id="defc7-121">These are automatically checked once you install any of those components.</span></span>

## <a name="iis-70-default-installation"></a><span data-ttu-id="defc7-122">IIS 7,0: Instalacja domyślna</span><span class="sxs-lookup"><span data-stu-id="defc7-122">IIS 7.0: Default Installation</span></span>

 <span data-ttu-id="defc7-123">Sprawdzając funkcję **Internet Information Services** , niektóre węzły podrzędne są automatycznie sprawdzane, jak pokazano na poniższej ilustracji.</span><span class="sxs-lookup"><span data-stu-id="defc7-123">By checking the **Internet Information Services** feature, some of the sub-nodes are automatically checked as shown in the following illustration.</span></span>

 <span data-ttu-id="defc7-124">![Ustawienia domyślne dla funkcji usług IIS 7,0](media/wcfc-turningfeaturesonoroff2.gif "wcfc_TurningFeaturesOnOrOff2")</span><span class="sxs-lookup"><span data-stu-id="defc7-124">![Default settings for IIS 7.0 features](media/wcfc-turningfeaturesonoroff2.gif "wcfc_TurningFeaturesOnOrOff2")</span></span>

 <span data-ttu-id="defc7-125">Jest to domyślna instalacja usług IIS 7,0.</span><span class="sxs-lookup"><span data-stu-id="defc7-125">This is the default installation of IIS 7.0.</span></span> <span data-ttu-id="defc7-126">Za pomocą tej instalacji można używać usług IIS 7,0 do obsługi zawartości statycznej (takiej jak strony HTML i inna zawartość).</span><span class="sxs-lookup"><span data-stu-id="defc7-126">With this installation, you can use IIS 7.0 to service static content (such as HTML pages and other content).</span></span> <span data-ttu-id="defc7-127">Nie można jednak uruchamiać aplikacji ASP.NET ani CGI ani hostować usług WCF.</span><span class="sxs-lookup"><span data-stu-id="defc7-127">However, you cannot run ASP.NET or CGI applications or host WCF services.</span></span>

## <a name="iis-70-installation-with-aspnet-support"></a><span data-ttu-id="defc7-128">IIS 7,0: Instalacja z obsługą ASP.NET</span><span class="sxs-lookup"><span data-stu-id="defc7-128">IIS 7.0: Installation with ASP.NET Support</span></span>

 <span data-ttu-id="defc7-129">Aby ASP.NET działały w usługach IIS 7,0, należy zainstalować ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="defc7-129">You must install ASP.NET to make ASP.NET work on IIS 7.0.</span></span> <span data-ttu-id="defc7-130">Po sprawdzeniu **ASP.NET** ekran powinien wyglądać jak na poniższej ilustracji.</span><span class="sxs-lookup"><span data-stu-id="defc7-130">After checking **ASP.NET**, your screen should look like the following illustration.</span></span>

 <span data-ttu-id="defc7-131">![Asp.NET wymagane ustawienia](media/wcfc-trunfeaturesonoroff3s.gif "wcfc_TrunFeaturesOnOrOFf3s")</span><span class="sxs-lookup"><span data-stu-id="defc7-131">![Asp.NET required settings](media/wcfc-trunfeaturesonoroff3s.gif "wcfc_TrunFeaturesOnOrOFf3s")</span></span>

 <span data-ttu-id="defc7-132">Jest to minimalne środowisko dla aplikacji WCF i ASP.NET, które działają w usługach IIS 7,0.</span><span class="sxs-lookup"><span data-stu-id="defc7-132">This is the minimal environment for both WCF and ASP.NET applications to work in IIS 7.0.</span></span>

## <a name="iis-70-installation-with-iis-60-compatibility-components"></a><span data-ttu-id="defc7-133">IIS 7,0: Instalacja ze składnikami zgodności usług IIS 6,0</span><span class="sxs-lookup"><span data-stu-id="defc7-133">IIS 7.0: Installation with IIS 6.0 Compatibility Components</span></span>

 <span data-ttu-id="defc7-134">Podczas instalowania usług IIS 7,0 w systemie przy użyciu programu Visual Studio 2005 lub innych skryptów lub narzędzi do automatyzacji (takich jak Adsutil.vbs), które konfigurują aplikacje wirtualne korzystające z interfejsu API metabazy usług IIS 6,0, upewnij się, że zaznaczono **Narzędzia do obsługi skryptów** 6,0 IIS.</span><span class="sxs-lookup"><span data-stu-id="defc7-134">When installing IIS 7.0 on a system with Visual Studio 2005 or some other automation scripts or tools (such as Adsutil.vbs) that configure virtual applications that use IIS 6.0 Metabase API, ensure that you check the IIS 6.0 **Scripting Tools**.</span></span> <span data-ttu-id="defc7-135">Spowoduje to automatyczne sprawdzenie innych podrzędnych węzłów **zgodności zarządzania** usług IIS 6,0.</span><span class="sxs-lookup"><span data-stu-id="defc7-135">This automatically checks the other sub-nodes of IIS 6.0 **Management Compatibility**.</span></span> <span data-ttu-id="defc7-136">Na poniższej ilustracji przedstawiono ekran po wykonaniu tej czynności:</span><span class="sxs-lookup"><span data-stu-id="defc7-136">The following illustration shows the screen after this is done:</span></span>

 <span data-ttu-id="defc7-137">![Ustawienia zgodności zarządzania usługami IIS 6,0](media/scfc-turnfeaturesonoroff5s.gif "scfc_TurnFeaturesOnOrOff5s")</span><span class="sxs-lookup"><span data-stu-id="defc7-137">![IIS 6.0 Management Compatibility Settings](media/scfc-turnfeaturesonoroff5s.gif "scfc_TurnFeaturesOnOrOff5s")</span></span>

 <span data-ttu-id="defc7-138">W przypadku tej instalacji masz wszystko, co jest wymagane do korzystania z usług IIS 7,0, ASP.NET i funkcji WCF oraz przykładów dostępnych w sieci Web.</span><span class="sxs-lookup"><span data-stu-id="defc7-138">With this installation, you have everything required to use IIS 7.0, ASP.NET and WCF features and samples available on the Web.</span></span>

## <a name="request-limits"></a><span data-ttu-id="defc7-139">Limity żądań</span><span class="sxs-lookup"><span data-stu-id="defc7-139">Request Limits</span></span>

 <span data-ttu-id="defc7-140">W systemie Windows Vista z usługami IIS 7 wartość domyślna `maxUri` ustawień i `maxQueryStringSize` została zmieniona.</span><span class="sxs-lookup"><span data-stu-id="defc7-140">On Windows Vista with IIS 7 the default value of the `maxUri` and `maxQueryStringSize` settings have been changed.</span></span> <span data-ttu-id="defc7-141">Domyślnie Filtrowanie żądań w usługach IIS 7,0 zezwala na długość adresu URL 4096 znaków i długość ciągu zapytania wynoszącą 2048 znaków.</span><span class="sxs-lookup"><span data-stu-id="defc7-141">By default, request filtering in IIS 7.0 allows a URL length of 4096 characters and a query string length of 2048 characters.</span></span> <span data-ttu-id="defc7-142">Aby zmienić te ustawienia domyślne, Dodaj następujący kod XML do pliku App.config.</span><span class="sxs-lookup"><span data-stu-id="defc7-142">To change these defaults add the following XML to your App.config file.</span></span>

```xml
 <system.webServer>
    <security>
        <requestFiltering>
            <requestLimits maxUrl="8192" maxQueryString="8192" />
        </requestFiltering>
    </security>
 </system.webServer>
 ```

## <a name="see-also"></a><span data-ttu-id="defc7-143">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="defc7-143">See also</span></span>

- [<span data-ttu-id="defc7-144">Architektura aktywacji WAS</span><span class="sxs-lookup"><span data-stu-id="defc7-144">WAS Activation Architecture</span></span>](was-activation-architecture.md)
- [<span data-ttu-id="defc7-145">Konfigurowanie usługi WAS do użycia z programem WCF</span><span class="sxs-lookup"><span data-stu-id="defc7-145">Configuring WAS for Use with WCF</span></span>](configuring-the-wpa--service-for-use-with-wcf.md)
- [<span data-ttu-id="defc7-146">Instrukcje: instalowanie i konfigurowanie składników aktywacji programu WCF</span><span class="sxs-lookup"><span data-stu-id="defc7-146">How to: Install and Configure WCF Activation Components</span></span>](how-to-install-and-configure-wcf-activation-components.md)
- <span data-ttu-id="defc7-147">[Funkcje hostingu sieci szkieletowej aplikacji systemu Windows Server](/previous-versions/appfabric/ee677189(v=azure.10))</span><span class="sxs-lookup"><span data-stu-id="defc7-147">[Windows Server App Fabric Hosting Features](/previous-versions/appfabric/ee677189(v=azure.10))</span></span>
