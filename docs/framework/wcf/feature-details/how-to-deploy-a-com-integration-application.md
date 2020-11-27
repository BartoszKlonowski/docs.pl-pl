---
title: 'Instrukcje: wdrażanie aplikacji integracji modelu COM+'
ms.date: 03/30/2017
ms.assetid: 2e5a0510-db3c-4988-a09c-696285836650
ms.openlocfilehash: 5f2e64ed06b98db50259edf8ef307ce430b8be38
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96289792"
---
# <a name="how-to-deploy-a-com-integration-application"></a><span data-ttu-id="40551-102">Instrukcje: wdrażanie aplikacji integracji modelu COM+</span><span class="sxs-lookup"><span data-stu-id="40551-102">How to: Deploy a COM+ Integration Application</span></span>

<span data-ttu-id="40551-103">Po napisaniu aplikacji integracji modelu COM+ warto ją wdrożyć na innym komputerze.</span><span class="sxs-lookup"><span data-stu-id="40551-103">Once you have written a COM+ integration application, you may want to deploy it on another machine.</span></span> <span data-ttu-id="40551-104">W tym temacie opisano sposób przenoszenia aplikacji integracji modelu COM+ z jednego komputera na inny.</span><span class="sxs-lookup"><span data-stu-id="40551-104">This topic describes how to move a COM+ integration application from one machine to another.</span></span>  
  
### <a name="moving-a-com-hosted-integration-app"></a><span data-ttu-id="40551-105">Przemieszczanie hostowanej aplikacji integracji modelu COM+</span><span class="sxs-lookup"><span data-stu-id="40551-105">Moving a COM+ hosted Integration App</span></span>  
  
1. <span data-ttu-id="40551-106">Upewnij się, że platforma WCF jest zainstalowana na obu komputerach.</span><span class="sxs-lookup"><span data-stu-id="40551-106">Ensure that WCF is installed on both machines.</span></span>  
  
2. <span data-ttu-id="40551-107">Wyeksportuj aplikację z komputera A.</span><span class="sxs-lookup"><span data-stu-id="40551-107">Export the application from machine A.</span></span>  
  
3. <span data-ttu-id="40551-108">Zaimportuj aplikację na komputerze B.</span><span class="sxs-lookup"><span data-stu-id="40551-108">Import the application on machine B.</span></span>  
  
4. <span data-ttu-id="40551-109">Ustaw katalog główny aplikacji.</span><span class="sxs-lookup"><span data-stu-id="40551-109">Set the Application Root Directory.</span></span> <span data-ttu-id="40551-110">Zgodnie z Konwencją jest to% PROGRAMFILES%/ComPlus Applications/{AppGUID}.</span><span class="sxs-lookup"><span data-stu-id="40551-110">By convention, this is %PROGRAMFILES%/ComPlus Applications/{AppGUID}.</span></span>  
  
5. <span data-ttu-id="40551-111">Skopiuj pliki Application.config i Application. manifest z katalogu głównego aplikacji na komputerze A do katalogu głównego aplikacji na komputerze B.</span><span class="sxs-lookup"><span data-stu-id="40551-111">Copy the Application.config and Application.manifest files from the application root directory on machine A to the application root directory on machine B.</span></span>  
  
6. <span data-ttu-id="40551-112">Aby zidentyfikować odpowiednią maszynę, Edytuj adresy punktów końcowych usługi w pliku Application.config na komputerze B.</span><span class="sxs-lookup"><span data-stu-id="40551-112">Edit the service endpoint addresses in the Application.config file on machine B to identify the appropriate machine.</span></span> <span data-ttu-id="40551-113">Na przykład zmień `http://machineA/MyService` na `http://machineB/MyService` .</span><span class="sxs-lookup"><span data-stu-id="40551-113">For example, change `http://machineA/MyService` to `http://machineB/MyService`.</span></span>  
  
### <a name="moving-a-web-hosted-integration-application"></a><span data-ttu-id="40551-114">Przeniesienie aplikacji integracji hostowanej w sieci Web</span><span class="sxs-lookup"><span data-stu-id="40551-114">Moving a Web-hosted integration application</span></span>  
  
1. <span data-ttu-id="40551-115">Upewnij się, że platforma WCF jest zainstalowana na obu komputerach.</span><span class="sxs-lookup"><span data-stu-id="40551-115">Ensure that WCF is installed on both machines.</span></span>  
  
2. <span data-ttu-id="40551-116">Wyeksportuj aplikację z komputera A.</span><span class="sxs-lookup"><span data-stu-id="40551-116">Export the application from machine A.</span></span>  
  
3. <span data-ttu-id="40551-117">Zaimportuj aplikację na komputerze B.</span><span class="sxs-lookup"><span data-stu-id="40551-117">Import the application on machine B.</span></span>  
  
4. <span data-ttu-id="40551-118">Utwórz katalog główny usług IIS na komputerze B.</span><span class="sxs-lookup"><span data-stu-id="40551-118">Create an IIS vroot on machine B.</span></span>  
  
5. <span data-ttu-id="40551-119">Skopiuj plik SVC (ComponentName. svc) i plik Web.config z katalogu głównego na komputerze A do nowo utworzonego elementu głównego na komputerze B.</span><span class="sxs-lookup"><span data-stu-id="40551-119">Copy the .svc file (componentName.svc) and the Web.config file from the vroot on machine A to the newly created vroot on machine B.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="40551-120">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="40551-120">See also</span></span>

- [<span data-ttu-id="40551-121">Omówienie integracji z aplikacjami COM+</span><span class="sxs-lookup"><span data-stu-id="40551-121">Integrating with COM+ Applications Overview</span></span>](integrating-with-com-plus-applications-overview.md)
- [<span data-ttu-id="40551-122">Instrukcje: konfigurowanie ustawień usługi COM+</span><span class="sxs-lookup"><span data-stu-id="40551-122">How to: Configure COM+ Service Settings</span></span>](how-to-configure-com-service-settings.md)
- [<span data-ttu-id="40551-123">Instrukcje: używanie narzędzia konfiguracji modelu usług COM+</span><span class="sxs-lookup"><span data-stu-id="40551-123">How to: Use the COM+ Service Model Configuration Tool</span></span>](how-to-use-the-com-service-model-configuration-tool.md)
