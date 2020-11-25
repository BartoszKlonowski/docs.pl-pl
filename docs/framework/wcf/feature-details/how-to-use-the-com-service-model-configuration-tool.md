---
title: 'Instrukcje: używanie narzędzia konfiguracji modelu usług COM+'
ms.date: 03/30/2017
helpviewer_keywords:
- COM+ [WCF], using service model configuration tool
ms.assetid: 7e68cd8d-5fda-4641-b92f-290db874376e
ms.openlocfilehash: 2d21ec8ccf84a7c9af235af8e0afd444044cf81b
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95729390"
---
# <a name="how-to-use-the-com-service-model-configuration-tool"></a><span data-ttu-id="734e0-102">Instrukcje: używanie narzędzia konfiguracji modelu usług COM+</span><span class="sxs-lookup"><span data-stu-id="734e0-102">How to: Use the COM+ Service Model Configuration Tool</span></span>

<span data-ttu-id="734e0-103">Po wybraniu odpowiedniego trybu hostingu Użyj narzędzia wiersza polecenia konfiguracji modelu usług modelu COM+ (ComSvcConfig.exe), aby skonfigurować interfejsy aplikacji, które będą udostępniane jako usługi sieci Web.</span><span class="sxs-lookup"><span data-stu-id="734e0-103">Once you have selected an appropriate hosting mode, use the COM+ Service Model Configuration command-line tool (ComSvcConfig.exe) to configure the application interfaces that will be exposed as Web services.</span></span>

> [!NOTE]
> <span data-ttu-id="734e0-104">Aby wykonać dowolne z następujących zadań, musisz być administratorem na komputerze.</span><span class="sxs-lookup"><span data-stu-id="734e0-104">You must be an administrator on the machine to perform any of the following tasks.</span></span>

 <span data-ttu-id="734e0-105">W przypadku korzystania z ComSvcConfig.exe na komputerze z systemem Windows 7 w celu skonfigurowania usługi sieci Web do korzystania z najnowszej wersji modelu usług (obecnie v 4.5) wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="734e0-105">When using ComSvcConfig.exe on a Windows 7 machine to configure a web service to use the latest service model version (currently v4.5), perform the following steps:</span></span>

1. <span data-ttu-id="734e0-106">Ustaw klucz rejestru  `[HKEY_LOCAL_COMPUTER\SOFTWARE\Microsoft\.NETFramework]\OnlyUseLatestCLR` na wartość typu DWORD 0x00000001</span><span class="sxs-lookup"><span data-stu-id="734e0-106">Set the registry key  `[HKEY_LOCAL_COMPUTER\SOFTWARE\Microsoft\.NETFramework]\OnlyUseLatestCLR` to a DWORD value of 0x00000001</span></span>

2. <span data-ttu-id="734e0-107">Uruchom comsvcconfig.exe</span><span class="sxs-lookup"><span data-stu-id="734e0-107">Run comsvcconfig.exe</span></span>

3. <span data-ttu-id="734e0-108">Przywróć pierwotną wartość klucza rejestru, który został dodany w kroku 1, lub usuń go, jeśli nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="734e0-108">Revert the registry key added in step 1 back to its original value, or delete it if did not exist.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="734e0-109">Przywrócenie tego klucza rejestru jest ważne.</span><span class="sxs-lookup"><span data-stu-id="734e0-109">Reverting this registry key is important.</span></span> <span data-ttu-id="734e0-110">Jest to klucz zgodności.</span><span class="sxs-lookup"><span data-stu-id="734e0-110">This is a compatibility key.</span></span> <span data-ttu-id="734e0-111">Przywrócenie tej zmiany może spowodować problemy z innymi aplikacjami .NET uruchomionymi na komputerze.</span><span class="sxs-lookup"><span data-stu-id="734e0-111">Not reverting this change may cause issues with other .NET applications running on the machine).</span></span>

> [!WARNING]
> <span data-ttu-id="734e0-112">W przypadku korzystania z ComSvcConfig.exe/Install na komputerze z systemem Windows 8 zostanie wyświetlone okno dialogowe informujące o tym, że aplikacja na komputerze wymaga następującej funkcji systemu Windows: .NET Framework 3,5 (w tym .NET 2,0 i .NET 3,0 "Jeśli .NET Framework 3,5 nie jest zainstalowana.</span><span class="sxs-lookup"><span data-stu-id="734e0-112">When using ComSvcConfig.exe  /install on a Windows 8 machine, a dialog is displayed stating "An app on your PC needs the following Windows feature: .NET Framework 3.5 (includes .NET 2.0 and .NET 3.0" if .NET Framework 3.5 is not installed.</span></span> <span data-ttu-id="734e0-113">To okno dialogowe może być ignorowane.</span><span class="sxs-lookup"><span data-stu-id="734e0-113">This dialog may be ignored.</span></span> <span data-ttu-id="734e0-114">Alternatywnie można przyOnlyUseLatestCLR klucz rejestru do wartości DWORD 0x00000001</span><span class="sxs-lookup"><span data-stu-id="734e0-114">Alternatively you can sed the OnlyUseLatestCLR registry key to a DWORD value of 0x00000001</span></span>

## <a name="add-an-interface-using-the-com-hosting-mode"></a><span data-ttu-id="734e0-115">Dodawanie interfejsu przy użyciu trybu hostingu modelu COM+</span><span class="sxs-lookup"><span data-stu-id="734e0-115">Add an interface using the COM+ hosting mode</span></span>

- <span data-ttu-id="734e0-116">Uruchom ComSvcConfig przy użyciu `/install` `/hosting:complus` opcji i, jak pokazano w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="734e0-116">Run ComSvcConfig using the `/install` and `/hosting:complus` options, as shown in the following example.</span></span>

    ```console
    ComSvcConfig.exe /install /application:OnlineStore /contract:ItemOrders.Financial,IFinances /hosting:complus /verbose
    ```

     <span data-ttu-id="734e0-117">Polecenie dodaje `IFinances` Interfejs `ItemOrders.IFinancial` składnika (z aplikacji OnlineStore com+) do zestawu interfejsów, które będą uwidocznione jako usługi sieci Web.</span><span class="sxs-lookup"><span data-stu-id="734e0-117">The command adds the `IFinances` interface of the `ItemOrders.IFinancial` component (from the OnlineStore COM+ application) to the set of interfaces that will be exposed as Web services.</span></span> <span data-ttu-id="734e0-118">Usługa używa trybu hostingu modelu COM+ i w związku z tym wymaga jawnej aktywacji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="734e0-118">The service uses the COM+ hosting mode and therefore requires explicit application activation.</span></span>

     <span data-ttu-id="734e0-119">Chociaż symbol wieloznaczny gwiazdka ( \* ) może być używany dla składnika i interfejsu, należy unikać używania go, ponieważ może być konieczne uwidocznienie tylko wybranych funkcji jako usługi sieci Web.</span><span class="sxs-lookup"><span data-stu-id="734e0-119">While the wildcard asterisk (\*) character can be used for the component and the interface, avoid using it because you might want to expose only selected functionality as a Web service.</span></span> <span data-ttu-id="734e0-120">Jeśli jest uruchamiany z przyszłą wersją tego składnika, użycie symbolu wieloznacznego może przypadkowo ujawnić interfejsy, które mogą nie być obecne podczas określania składni konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="734e0-120">If run with a future version of this component, using the wildcard may unintentionally expose interfaces that may not have been present when the configuration syntax was determined.</span></span>

     <span data-ttu-id="734e0-121">Opcja/verbose nakazuje narzędziu wyświetlanie ostrzeżeń oprócz błędów.</span><span class="sxs-lookup"><span data-stu-id="734e0-121">The /verbose option instructs the tool to display warnings in addition to any errors.</span></span>

     <span data-ttu-id="734e0-122">Kontrakt dla uwidocznionej usługi będzie zawierać wszystkie metody z `IFinances` interfejsu.</span><span class="sxs-lookup"><span data-stu-id="734e0-122">The contract for the exposed service will contain all of the methods from the `IFinances` interface.</span></span>

## <a name="add-specific-methods-from-an-interface-using-the-com-hosting-mode"></a><span data-ttu-id="734e0-123">Dodawanie określonych metod z interfejsu przy użyciu trybu hostingu modelu COM+</span><span class="sxs-lookup"><span data-stu-id="734e0-123">Add specific methods from an interface using the COM+ hosting mode</span></span>

- <span data-ttu-id="734e0-124">Uruchom ComSvcConfig przy użyciu `/install` `/hosting:complus` opcji i z jawnym nazewnictwem wymaganych metod, jak pokazano w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="734e0-124">Run ComSvcConfig using the `/install` and `/hosting:complus` options with explicit naming of the required methods, as shown in the following example.</span></span>

    ```console
    ComSvcConfig.exe /install /application:OnlineStore /contract:ItemOrders.Financial,IFinances.{Credit,Debit} /hosting:complus /verbose
    ```

     <span data-ttu-id="734e0-125">Polecenie dodaje tylko `Credit` `Debit` metody i z `IFinances` interfejsu jako operacje do umowy uwidocznionej usługi.</span><span class="sxs-lookup"><span data-stu-id="734e0-125">The command adds only the `Credit` and `Debit` methods from the `IFinances` interface as operations to the exposed service contract.</span></span> <span data-ttu-id="734e0-126">Wszystkie inne metody interfejsu zostaną pominięte z kontraktu i nie zostaną wywołane przez klientów usługi sieci Web.</span><span class="sxs-lookup"><span data-stu-id="734e0-126">All other methods on the interface will be omitted from the contract and will not be callable from Web service clients.</span></span>

## <a name="add-an-interface-using-the-web-hosting-mode"></a><span data-ttu-id="734e0-127">Dodawanie interfejsu przy użyciu trybu hostingu w sieci Web</span><span class="sxs-lookup"><span data-stu-id="734e0-127">Add an interface using the Web hosting mode</span></span>

- <span data-ttu-id="734e0-128">Uruchom ComSvcConfig przy użyciu `/install` opcji i `/hosting:was` opcji, jak pokazano w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="734e0-128">Run ComSvcConfig using the `/install` option and the `/hosting:was` option, as shown in the following example.</span></span>

    ```console
    ComSvcConfig.exe /install /application:OnlineWarehouse /contract:ItemInventory.Warehouse,IStockLevels /hosting:was /webDirectory:root/OnlineWarehouse /mex /verbose
    ```

     <span data-ttu-id="734e0-129">Polecenie dodaje interfejs do `IStockLevels` `ItemInventory.Warehouse` składnika (z aplikacji OnlineWarehouse com+) do zestawu interfejsów, które będą udostępniane jako usługi sieci Web.</span><span class="sxs-lookup"><span data-stu-id="734e0-129">The command adds the `IStockLevels` interface on the `ItemInventory.Warehouse` component (from the OnlineWarehouse COM+ application) to the set of interfaces that will be exposed as Web services.</span></span> <span data-ttu-id="734e0-130">Usługa jest w sieci Web hostowana w katalogu wirtualnym usługi IIS OnlineWarehouse, a nie w modelu COM+, a więc aplikacja jest automatycznie uaktywniana zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="734e0-130">The service is Web hosted in the OnlineWarehouse virtual directory of IIS rather than in COM+, and thus the application is automatically activated as required.</span></span>

     <span data-ttu-id="734e0-131">Aby można było korzystać z konfiguracji w procesie hostowanym w sieci Web, aplikacja COM+ musi być skonfigurowana do uruchamiania jako aplikacja biblioteki, a nie aplikacja serwera przy użyciu konsoli administracyjnej usług składowych.</span><span class="sxs-lookup"><span data-stu-id="734e0-131">To use the Web-hosted in-process configuration, the COM+ application must be configured to run as a Library application rather than a Server application using the Component Services administration console.</span></span> <span data-ttu-id="734e0-132">Aplikacje skonfigurowane jako aplikacje serwera używają standardowego trybu hostowanego w sieci Web i ponoszą przeskok procesu, aby przetwarzać każde żądanie.</span><span class="sxs-lookup"><span data-stu-id="734e0-132">Applications configured as Server applications use the standard Web-hosted mode and incur a process hop to process each request.</span></span>

     <span data-ttu-id="734e0-133">`/mex`Opcja dodaje dodatkowy punkt końcowy usługi wymiany metadanych (Mex), który używa tego samego transportu co punkt końcowy usługi aplikacji do obsługi klientów, którzy chcą pobrać definicję kontraktu z usługi.</span><span class="sxs-lookup"><span data-stu-id="734e0-133">The `/mex` option adds an additional Metadata Exchange (MEX) service endpoint that uses the same transport as the application's service endpoint to support clients that want to retrieve a contract definition from the service.</span></span>

## <a name="remove-a-web-service-for-a-specified-interface"></a><span data-ttu-id="734e0-134">Usuwanie usługi sieci Web dla określonego interfejsu</span><span class="sxs-lookup"><span data-stu-id="734e0-134">Remove a Web service for a specified interface</span></span>

- <span data-ttu-id="734e0-135">Uruchom ComSvcConfig przy użyciu `/uninstall` opcji, jak pokazano w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="734e0-135">Run ComSvcConfig using the `/uninstall` option, as shown in the following example.</span></span>

    ```console
    ComSvcConfig.exe /uninstall /application:OnlineStore /contract:ItemOrders.Financial,IFinances /hosting:complus
    ```

     <span data-ttu-id="734e0-136">Polecenie usuwa `IFinances` interfejs na `ItemOrders.Financial` składniku programu (z aplikacji OnlineStore com+).</span><span class="sxs-lookup"><span data-stu-id="734e0-136">The command removes the `IFinances` interface on the `ItemOrders.Financial` component (from the OnlineStore COM+ application).</span></span>

## <a name="list-currently-exposed-interfaces"></a><span data-ttu-id="734e0-137">Wyświetl listę aktualnie uwidocznionych interfejsów</span><span class="sxs-lookup"><span data-stu-id="734e0-137">List currently exposed interfaces</span></span>

- <span data-ttu-id="734e0-138">Uruchom ComSvcConfig przy użyciu `/list` opcji, jak pokazano w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="734e0-138">Run ComSvcConfig using the `/list` option, as shown in the following example.</span></span>

    ```console
    ComSvcConfig.exe /list
    ```

     <span data-ttu-id="734e0-139">Polecenie wyświetla listę aktualnie uwidocznionych interfejsów wraz z odpowiednim adresem i szczegółami powiązania, które należą do zakresu komputera lokalnego.</span><span class="sxs-lookup"><span data-stu-id="734e0-139">The command lists the currently exposed interfaces, along with the corresponding address and binding details, scoped to the local machine.</span></span>

## <a name="list-specific-currently-exposed-interfaces"></a><span data-ttu-id="734e0-140">Wyświetlanie listy określonych aktualnie uwidocznionych interfejsów</span><span class="sxs-lookup"><span data-stu-id="734e0-140">List specific currently exposed interfaces</span></span>

- <span data-ttu-id="734e0-141">Uruchom ComSvcConfig przy użyciu `/list` opcji, jak pokazano w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="734e0-141">Run ComSvcConfig using the `/list` option, as shown in the following example.</span></span>

    ```console
    ComSvcConfig.exe /list /application:OnlineStore /hosting:complus
    ```

     <span data-ttu-id="734e0-142">Polecenie wyświetla aktualnie uwidocznione interfejsy obsługiwane przez model COM+ oraz odpowiednie adresy i szczegóły dotyczące powiązań dla aplikacji OnlineStore COM+ na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="734e0-142">The command lists currently exposed COM+-hosted interfaces, along with the corresponding address and binding details, for the OnlineStore COM+ application on the local machine.</span></span>

## <a name="display-help-for-options"></a><span data-ttu-id="734e0-143">Wyświetl pomoc dla opcji</span><span class="sxs-lookup"><span data-stu-id="734e0-143">Display help for options</span></span>

- <span data-ttu-id="734e0-144">Uruchom ComSvcConfig przy użyciu/?</span><span class="sxs-lookup"><span data-stu-id="734e0-144">Run ComSvcConfig using the /?</span></span> <span data-ttu-id="734e0-145">opcja, jak pokazano w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="734e0-145">option, as shown in the following example.</span></span>

    ```console
    ComSvcConfig.exe /?
    ```

## <a name="see-also"></a><span data-ttu-id="734e0-146">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="734e0-146">See also</span></span>

- [<span data-ttu-id="734e0-147">Omówienie integracji z aplikacjami COM+</span><span class="sxs-lookup"><span data-stu-id="734e0-147">Integrating with COM+ Applications Overview</span></span>](integrating-with-com-plus-applications-overview.md)
