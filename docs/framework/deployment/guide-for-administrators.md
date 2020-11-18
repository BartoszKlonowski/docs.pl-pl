---
title: .NET Framework — Przewodnik wdrażania dla administratorów
description: Zapoznaj się z przewodnikiem wdrażania platformy .NET dla administratorów. Te informacje służą do wdrażania programu .NET w wersji 4,5 i jej zależności systemowych w sieci.
ms.date: 04/10/2018
helpviewer_keywords:
- administrator's guide, deploying .NET Framework
- deployment [.NET Framework], administrator's guide
ms.assetid: bee14036-0436-44e8-89f5-4bc61317977a
ms.openlocfilehash: 12076334d3ede0c8ab9b618ba2018f23c9fc6ae4
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/18/2020
ms.locfileid: "94817097"
---
# <a name="net-framework-deployment-guide-for-administrators"></a><span data-ttu-id="dd07c-104">.NET Framework — Przewodnik wdrażania dla administratorów</span><span class="sxs-lookup"><span data-stu-id="dd07c-104">.NET Framework Deployment Guide for Administrators</span></span>

<span data-ttu-id="dd07c-105">W tym artykule krok po kroku opisano, jak administrator systemu może wdrożyć .NET Framework 4,5 i zależności systemu w sieci za pomocą usługi Microsoft Endpoint Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="dd07c-105">This step-by-step article describes how a system administrator can deploy .NET Framework 4.5 and its system dependencies across a network by using Microsoft Endpoint Configuration Manager.</span></span> <span data-ttu-id="dd07c-106">W tym artykule przyjęto założenie, że wszystkie docelowe komputery klienckie spełniają minimalne wymagania dotyczące .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="dd07c-106">This article assumes that all target client computers meet the minimum requirements for .NET Framework.</span></span> <span data-ttu-id="dd07c-107">Aby uzyskać listę wymagań dotyczących oprogramowania i sprzętu dla instalacji .NET Framework 4,5, zobacz [wymagania systemowe](../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="dd07c-107">For a list of the software and hardware requirements for installing .NET Framework 4.5, see [System Requirements](../get-started/system-requirements.md).</span></span>

> [!NOTE]
> <span data-ttu-id="dd07c-108">Oprogramowanie przywoływane w tym dokumencie, w tym, bez ograniczenia, .NET Framework 4,5, Configuration Manager i Active Directory, podlega postanowieniom licencyjnym.</span><span class="sxs-lookup"><span data-stu-id="dd07c-108">The software referenced in this document, including, without limitation, .NET Framework 4.5, Configuration Manager, and Active Directory, are each subject to license terms and conditions.</span></span> <span data-ttu-id="dd07c-109">W tych instrukcjach przyjęto założenie, że takie postanowienia licencyjne i warunki zostały przejrzane i zaakceptowane przez właściwych licencjobiorców oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="dd07c-109">These instructions assume that such license terms and conditions have been reviewed and accepted by the appropriate licensees of the software.</span></span> <span data-ttu-id="dd07c-110">Te instrukcje nie unieważniają żadnego postanowienia tych umów licencyjnych.</span><span class="sxs-lookup"><span data-stu-id="dd07c-110">These instructions do not waive any of the terms and conditions of such license agreements.</span></span>
>
> <span data-ttu-id="dd07c-111">Aby uzyskać informacje na temat pomocy technicznej dla .NET Framework, zobacz [.NET Framework oficjalne zasady pomocy technicznej](https://dotnet.microsoft.com/platform/support/policy/dotnet-framework) w witrynie sieci Web Pomoc techniczna firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="dd07c-111">For information about support for .NET Framework, see [.NET Framework official support policy](https://dotnet.microsoft.com/platform/support/policy/dotnet-framework) on the Microsoft Support website.</span></span>

<span data-ttu-id="dd07c-112">Ten temat zawiera następujące sekcje:</span><span class="sxs-lookup"><span data-stu-id="dd07c-112">This topic contains the following sections:</span></span>

- [<span data-ttu-id="dd07c-113">Proces wdrażania</span><span class="sxs-lookup"><span data-stu-id="dd07c-113">The deployment process</span></span>](#the_deployment_process)
- [<span data-ttu-id="dd07c-114">Wdrażanie .NET Framework</span><span class="sxs-lookup"><span data-stu-id="dd07c-114">Deploying .NET Framework</span></span>](#deploying_in_a_test_environment)
- [<span data-ttu-id="dd07c-115">Tworzenie kolekcji</span><span class="sxs-lookup"><span data-stu-id="dd07c-115">Create a collection</span></span>](#creating_a_collection)
- [<span data-ttu-id="dd07c-116">Tworzenie pakietu i programu</span><span class="sxs-lookup"><span data-stu-id="dd07c-116">Create a package and program</span></span>](#creating_a_package)
- [<span data-ttu-id="dd07c-117">Wybieranie punktu dystrybucji</span><span class="sxs-lookup"><span data-stu-id="dd07c-117">Select a distribution point</span></span>](#select_dist_point)
- [<span data-ttu-id="dd07c-118">Wdrażanie pakietu</span><span class="sxs-lookup"><span data-stu-id="dd07c-118">Deploy the package</span></span>](#deploying_package)
- [<span data-ttu-id="dd07c-119">Zasoby</span><span class="sxs-lookup"><span data-stu-id="dd07c-119">Resources</span></span>](#resources)
- [<span data-ttu-id="dd07c-120">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="dd07c-120">Troubleshooting</span></span>](#troubleshooting)

<a name="the_deployment_process"></a>

## <a name="the-deployment-process"></a><span data-ttu-id="dd07c-121">Proces wdrażania</span><span class="sxs-lookup"><span data-stu-id="dd07c-121">The deployment process</span></span>

<span data-ttu-id="dd07c-122">W przypadku korzystania z infrastruktury obsługiwanej przez program Configuration Manager można wdrożyć pakiet redystrybucyjny .NET Framework na komputerach w sieci.</span><span class="sxs-lookup"><span data-stu-id="dd07c-122">When you have the supporting infrastructure in place, you use Configuration Manager to deploy the .NET Framework redistributable package to computers on the network.</span></span> <span data-ttu-id="dd07c-123">Tworzenie infrastruktury obejmuje utworzenie i zdefiniowanie pięciu podstawowych obszarów: kolekcji, pakietu i programu dla oprogramowania, punktów dystrybucji i wdrożeń.</span><span class="sxs-lookup"><span data-stu-id="dd07c-123">Building the infrastructure involves creating and defining five primary areas: collections, a package and program for the software, distribution points, and deployments.</span></span>

- <span data-ttu-id="dd07c-124">**Kolekcje** to grupy zasobów Configuration Manager, takie jak użytkownicy, grupy użytkowników lub komputery, na które .NET Framework wdrożone.</span><span class="sxs-lookup"><span data-stu-id="dd07c-124">**Collections** are groups of Configuration Manager resources, such as users, user groups, or computers, to which .NET Framework is deployed.</span></span> <span data-ttu-id="dd07c-125">Aby uzyskać więcej informacji, zobacz [wprowadzenie do kolekcji w Configuration Manager](/configmgr/core/clients/manage/collections/introduction-to-collections) w bibliotece dokumentacji Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="dd07c-125">For more information, see [Introduction to collections in Configuration Manager](/configmgr/core/clients/manage/collections/introduction-to-collections) in the Configuration Manager documentation library.</span></span>

- <span data-ttu-id="dd07c-126">**Pakiety i programy** zwykle reprezentują aplikacje, które mają być zainstalowane na komputerze klienckim, ale mogą również zawierać pojedyncze pliki, aktualizacje lub nawet poszczególne polecenia.</span><span class="sxs-lookup"><span data-stu-id="dd07c-126">**Packages and programs** typically represent software applications to be installed on a client computer, but they might also contain individual files, updates, or even individual commands.</span></span> <span data-ttu-id="dd07c-127">Aby uzyskać więcej informacji, zobacz [pakiety i programy w Configuration Manager](/configmgr/apps/deploy-use/packages-and-programs) w bibliotece dokumentacji Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="dd07c-127">For more information, see [Packages and programs in Configuration Manager](/configmgr/apps/deploy-use/packages-and-programs) in the Configuration Manager documentation library.</span></span>

- <span data-ttu-id="dd07c-128">**Punkty dystrybucji** są Configuration Manager ról systemu lokacji, które przechowują pliki wymagane do uruchamiania oprogramowania na komputerach klienckich.</span><span class="sxs-lookup"><span data-stu-id="dd07c-128">**Distribution points** are Configuration Manager site system roles that store files required for software to run on client computers.</span></span> <span data-ttu-id="dd07c-129">Gdy klient programu Configuration Manager odbiera i przetwarza wdrożenie oprogramowania, kontaktuje się z punktem dystrybucji w celu pobrania zawartości skojarzonej z oprogramowaniem i rozpoczęcia procesu instalacji.</span><span class="sxs-lookup"><span data-stu-id="dd07c-129">When the Configuration Manager client receives and processes a software deployment, it contacts a distribution point to download the content associated with the software and to start the installation process.</span></span> <span data-ttu-id="dd07c-130">Aby uzyskać więcej informacji, zobacz [podstawowe pojęcia związane z zarządzaniem zawartością w programie Configuration Manager](/configmgr/core/plan-design/hierarchy/fundamental-concepts-for-content-management) w bibliotece dokumentacji Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="dd07c-130">For more information, see [Fundamental concepts for content management in Configuration Manager](/configmgr/core/plan-design/hierarchy/fundamental-concepts-for-content-management) in the Configuration Manager documentation library.</span></span>

- <span data-ttu-id="dd07c-131">**Wdrożenia** instruują odpowiednich członków określonej kolekcji docelowej w celu zainstalowania pakietu oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="dd07c-131">**Deployments** instruct applicable members of the specified target collection to install the software package.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dd07c-132">Procedury opisane w tym temacie zawierają typowe ustawienia służące do tworzenia i wdrażania pakietu oraz programu i mogą nie obejmować wszystkich możliwych ustawień.</span><span class="sxs-lookup"><span data-stu-id="dd07c-132">The procedures in this topic contain typical settings for creating and deploying a package and program, and might not cover all possible settings.</span></span> <span data-ttu-id="dd07c-133">Inne Configuration Manager opcje wdrażania można znaleźć w [bibliotece dokumentacji Configuration Manager](/previous-versions/system-center/system-center-2012-R2/gg682041(v=technet.10)).</span><span class="sxs-lookup"><span data-stu-id="dd07c-133">For other Configuration Manager deployment options, see the [Configuration Manager Documentation Library](/previous-versions/system-center/system-center-2012-R2/gg682041(v=technet.10)).</span></span>

<a name="deploying_in_a_test_environment"></a>

## <a name="deploying-net-framework"></a><span data-ttu-id="dd07c-134">Wdrażanie .NET Framework</span><span class="sxs-lookup"><span data-stu-id="dd07c-134">Deploying .NET Framework</span></span>

<span data-ttu-id="dd07c-135">Za pomocą Configuration Manager można wdrożyć instalację dyskretną .NET Framework 4,5, w której użytkownicy nie współpracują z procesem instalacji.</span><span class="sxs-lookup"><span data-stu-id="dd07c-135">You can use Configuration Manager to deploy a silent installation of .NET Framework 4.5, where the users do not interact with the installation process.</span></span> <span data-ttu-id="dd07c-136">Wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="dd07c-136">Follow these steps:</span></span>

1. <span data-ttu-id="dd07c-137">[Utwórz kolekcję](#creating_a_collection).</span><span class="sxs-lookup"><span data-stu-id="dd07c-137">[Create a collection](#creating_a_collection).</span></span>

2. <span data-ttu-id="dd07c-138">[Utwórz pakiet i program dla .NET Framework pakiet redystrybucyjny](#creating_a_package).</span><span class="sxs-lookup"><span data-stu-id="dd07c-138">[Create a package and program for the .NET Framework redistributable](#creating_a_package).</span></span>

3. <span data-ttu-id="dd07c-139">[Wybierz punkt dystrybucji](#select_dist_point).</span><span class="sxs-lookup"><span data-stu-id="dd07c-139">[Select a distribution point](#select_dist_point).</span></span>

4. <span data-ttu-id="dd07c-140">[Wdróż pakiet](#deploying_package).</span><span class="sxs-lookup"><span data-stu-id="dd07c-140">[Deploy the package](#deploying_package).</span></span>

<a name="creating_a_collection"></a>

### <a name="create-a-collection"></a><span data-ttu-id="dd07c-141">Tworzenie kolekcji</span><span class="sxs-lookup"><span data-stu-id="dd07c-141">Create a collection</span></span>

<span data-ttu-id="dd07c-142">W tym kroku należy wybrać komputery, na których będzie wdrażany pakiet i program, i zgrupować je w kolekcji urządzeń.</span><span class="sxs-lookup"><span data-stu-id="dd07c-142">In this step, you select the computers to which you will deploy the package and program, and group them into a device collection.</span></span> <span data-ttu-id="dd07c-143">Aby utworzyć kolekcję w programie Configuration Manager, można użyć bezpośrednich reguł członkostwa (elementy członkowskie kolekcji są określane ręcznie) lub reguł zapytań (program Configuration Manager określa elementy członkowskie kolekcji na podstawie określonych kryteriów).</span><span class="sxs-lookup"><span data-stu-id="dd07c-143">To create a collection in Configuration Manager, you can use direct membership rules (where you manually specify the collection members) or query rules (where Configuration Manager determines the collection members based on criteria you specify).</span></span> <span data-ttu-id="dd07c-144">Aby uzyskać więcej informacji na temat reguł członkostwa, w tym zapytań i reguł bezpośrednich, zobacz [wprowadzenie do kolekcji w Configuration Manager](/configmgr/core/clients/manage/collections/introduction-to-collections) w bibliotece dokumentacji Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="dd07c-144">For more information about membership rules, including queries and direct rules, see [Introduction to collections in Configuration Manager](/configmgr/core/clients/manage/collections/introduction-to-collections) in the Configuration Manager Documentation Library.</span></span>

<span data-ttu-id="dd07c-145">Aby utworzyć kolekcję:</span><span class="sxs-lookup"><span data-stu-id="dd07c-145">To create a collection:</span></span>

1. <span data-ttu-id="dd07c-146">W konsoli Configuration Manager wybierz pozycję **zasoby i zgodność**.</span><span class="sxs-lookup"><span data-stu-id="dd07c-146">In the Configuration Manager console, choose **Assets and Compliance**.</span></span>

2. <span data-ttu-id="dd07c-147">W obszarze roboczym **zasoby i zgodność** wybierz pozycję **Kolekcje urządzeń**.</span><span class="sxs-lookup"><span data-stu-id="dd07c-147">In the **Assets and Compliance** workspace, choose **Device Collections**.</span></span>

3. <span data-ttu-id="dd07c-148">Na karcie **Narzędzia główne** w grupie **Tworzenie** wybierz pozycję **Utwórz kolekcję urządzeń**.</span><span class="sxs-lookup"><span data-stu-id="dd07c-148">On the **Home** tab in the **Create** group, choose **Create Device Collection**.</span></span>

4. <span data-ttu-id="dd07c-149">Na stronie **Ogólne** **Kreatora tworzenia kolekcji urządzeń** wprowadź nazwę kolekcji.</span><span class="sxs-lookup"><span data-stu-id="dd07c-149">On the **General** page of the **Create Device Collection Wizard**, enter a name for the collection.</span></span>

5. <span data-ttu-id="dd07c-150">Wybierz pozycję **Przeglądaj** , aby określić kolekcję ograniczającą.</span><span class="sxs-lookup"><span data-stu-id="dd07c-150">Choose **Browse** to specify a limiting collection.</span></span>

6. <span data-ttu-id="dd07c-151">Na stronie **reguły członkostwa** wybierz pozycję **Dodaj regułę**, a następnie wybierz pozycję **reguła bezpośrednia** , aby otworzyć **Kreatora tworzenia reguły członkostwa bezpośredniego**.</span><span class="sxs-lookup"><span data-stu-id="dd07c-151">On the **Membership Rules** page, choose **Add Rule**, and then choose **Direct Rule** to open the **Create Direct Membership Rule Wizard**.</span></span> <span data-ttu-id="dd07c-152">Wybierz pozycję **Next** (Dalej).</span><span class="sxs-lookup"><span data-stu-id="dd07c-152">Choose **Next**.</span></span>

7. <span data-ttu-id="dd07c-153">Na stronie **Wyszukiwanie zasobów** na liście **Klasa zasobów** wybierz pozycję **zasób systemowy**.</span><span class="sxs-lookup"><span data-stu-id="dd07c-153">On the **Search for Resources** page, in the **Resource class** list, choose **System Resource**.</span></span> <span data-ttu-id="dd07c-154">Na liście **nazwa atrybutu** wybierz pozycję **Nazwa**.</span><span class="sxs-lookup"><span data-stu-id="dd07c-154">In the **Attribute name** list, choose **Name**.</span></span> <span data-ttu-id="dd07c-155">W polu **wartość** wprowadź `%` , a następnie wybierz przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="dd07c-155">In the **Value** field, enter `%`, and then choose **Next**.</span></span>

8. <span data-ttu-id="dd07c-156">Na stronie **Wybierz zasoby** zaznacz pole wyboru obok każdego komputera, na którym chcesz wdrożyć .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="dd07c-156">On the **Select Resources** page, select the check box for each computer that you want to deploy the .NET Framework to.</span></span> <span data-ttu-id="dd07c-157">Wybierz pozycję **dalej**, a następnie Zakończ pracę kreatora.</span><span class="sxs-lookup"><span data-stu-id="dd07c-157">Choose **Next**, and then complete the wizard.</span></span>

9. <span data-ttu-id="dd07c-158">Na stronie **reguły członkostwa** **Kreatora tworzenia kolekcji urządzeń** wybierz **dalej**, a następnie Ukończ pracę kreatora.</span><span class="sxs-lookup"><span data-stu-id="dd07c-158">On the **Membership Rules** page of the **Create Device Collection Wizard**, choose **Next**, and then complete the wizard.</span></span>

<a name="creating_a_package"></a>

### <a name="create-a-package-and-program-for-the-net-framework-redistributable-package"></a><span data-ttu-id="dd07c-159">Tworzenie pakietu i programu dla redystrybucyjnego pakietu programu .NET Framework</span><span class="sxs-lookup"><span data-stu-id="dd07c-159">Create a package and program for the .NET Framework redistributable package</span></span>

<span data-ttu-id="dd07c-160">Wykonanie poniższych kroków umożliwia ręczne utworzenie pakietu redystrybucyjnego programu .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="dd07c-160">The following steps create a package for the .NET Framework redistributable manually.</span></span> <span data-ttu-id="dd07c-161">Pakiet zawiera określone parametry instalacji .NET Framework i lokalizację, z której pakiet będzie dystrybuowany do komputerów docelowych.</span><span class="sxs-lookup"><span data-stu-id="dd07c-161">The package contains the specified parameters for installing .NET Framework and the location from where the package will be distributed to the target computers.</span></span>

<span data-ttu-id="dd07c-162">Aby utworzyć pakiet:</span><span class="sxs-lookup"><span data-stu-id="dd07c-162">To create a package:</span></span>

1. <span data-ttu-id="dd07c-163">W konsoli Configuration Manager wybierz pozycję **Biblioteka oprogramowania**.</span><span class="sxs-lookup"><span data-stu-id="dd07c-163">In the Configuration Manager console, choose **Software Library**.</span></span>

2. <span data-ttu-id="dd07c-164">W obszarze roboczym **Biblioteka oprogramowania** rozwiń węzeł **Zarządzanie aplikacjami**, a następnie wybierz pozycję **pakiety**.</span><span class="sxs-lookup"><span data-stu-id="dd07c-164">In the **Software Library** workspace, expand **Application Management**, and then choose **Packages**.</span></span>

3. <span data-ttu-id="dd07c-165">Na karcie **Narzędzia główne** w grupie **Tworzenie** wybierz pozycję **Utwórz pakiet**.</span><span class="sxs-lookup"><span data-stu-id="dd07c-165">On the **Home** tab, in the **Create** group, choose **Create Package**.</span></span>

4. <span data-ttu-id="dd07c-166">Na stronie **pakiet** **Kreatora tworzenia pakietu i programu** wprowadź następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="dd07c-166">On the **Package** page of the **Create Package and Program Wizard**, enter the following information:</span></span>

    - <span data-ttu-id="dd07c-167">Nazwa: `.NET Framework 4.5`</span><span class="sxs-lookup"><span data-stu-id="dd07c-167">Name: `.NET Framework 4.5`</span></span>

    - <span data-ttu-id="dd07c-168">Instrukcj `Microsoft`</span><span class="sxs-lookup"><span data-stu-id="dd07c-168">Manufacturer: `Microsoft`</span></span>

    - <span data-ttu-id="dd07c-169">Język.</span><span class="sxs-lookup"><span data-stu-id="dd07c-169">Language.</span></span> `English (US)`

5. <span data-ttu-id="dd07c-170">Wybierz opcję **ten pakiet zawiera pliki źródłowe**, a następnie wybierz pozycję **Przeglądaj** , aby wybrać folder lokalny lub sieciowy zawierający pliki instalacyjne .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="dd07c-170">Choose **This package contains source files**, and then choose **Browse** to select the local or network folder that contains the .NET Framework installation files.</span></span> <span data-ttu-id="dd07c-171">Po wybraniu folderu wybierz **przycisk OK**, a następnie wybierz przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="dd07c-171">When you have selected the folder, choose **OK**, and then choose **Next**.</span></span>

6. <span data-ttu-id="dd07c-172">Na stronie **Typ programu** kreatora wybierz pozycję **program standardowy**, a następnie wybierz przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="dd07c-172">On the **Program Type** page of the wizard, choose **Standard Program**, and then choose **Next**.</span></span>

7. <span data-ttu-id="dd07c-173">Na stronie **program** w **Kreatorze tworzenia pakietu i programu** wprowadź następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="dd07c-173">On the **Program** page of the **Create Package and Program Wizard**, enter the following information:</span></span>

    1. <span data-ttu-id="dd07c-174">**Nazwa:**`.NET Framework 4.5`</span><span class="sxs-lookup"><span data-stu-id="dd07c-174">**Name:** `.NET Framework 4.5`</span></span>

    2. <span data-ttu-id="dd07c-175">**Wiersz polecenia:** `dotNetFx45_Full_x86_x64.exe /q /norestart /ChainingPackage ADMINDEPLOYMENT` (Opcje wiersza polecenia są opisane w tabeli po wykonaniu tych kroków)</span><span class="sxs-lookup"><span data-stu-id="dd07c-175">**Command line:** `dotNetFx45_Full_x86_x64.exe /q /norestart /ChainingPackage ADMINDEPLOYMENT` (command-line options are described in the table after these steps)</span></span>

    3. <span data-ttu-id="dd07c-176">**Uruchom:** Wybierz **Ukryj**.</span><span class="sxs-lookup"><span data-stu-id="dd07c-176">**Run:** Choose **Hidden**.</span></span>

    4. <span data-ttu-id="dd07c-177">**Program może zostać uruchomiony:** Wybierz opcję, która określa, że program może być uruchamiany niezależnie od tego, czy użytkownik jest zalogowany.</span><span class="sxs-lookup"><span data-stu-id="dd07c-177">**Program can run:** Choose the option that specifies that the program can run regardless of whether a user is logged on.</span></span>

8. <span data-ttu-id="dd07c-178">Na stronie **wymagania** wybierz pozycję **dalej** , aby zaakceptować wartości domyślne, a następnie Ukończ pracę kreatora.</span><span class="sxs-lookup"><span data-stu-id="dd07c-178">On the **Requirements** page, choose **Next** to accept the default values, and then complete the wizard.</span></span>

<span data-ttu-id="dd07c-179">W poniższej tabeli opisano opcje wiersza polecenia określone w kroku 7.</span><span class="sxs-lookup"><span data-stu-id="dd07c-179">The following table describes the command-line options specified in step 7.</span></span>

|<span data-ttu-id="dd07c-180">Opcja</span><span class="sxs-lookup"><span data-stu-id="dd07c-180">Option</span></span>|<span data-ttu-id="dd07c-181">Opis</span><span class="sxs-lookup"><span data-stu-id="dd07c-181">Description</span></span>|
|------------|-----------------|
|<span data-ttu-id="dd07c-182">**parametru**</span><span class="sxs-lookup"><span data-stu-id="dd07c-182">**/q**</span></span>|<span data-ttu-id="dd07c-183">Ustawia tryb cichy.</span><span class="sxs-lookup"><span data-stu-id="dd07c-183">Sets quiet mode.</span></span> <span data-ttu-id="dd07c-184">Nie jest wymagane wprowadzanie danych przez użytkownika i nie są wyświetlane dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="dd07c-184">No user input is required, and no output is shown.</span></span>|
|<span data-ttu-id="dd07c-185">**/norestart**</span><span class="sxs-lookup"><span data-stu-id="dd07c-185">**/norestart**</span></span>|<span data-ttu-id="dd07c-186">Uniemożliwia Instalatorowi automatyczne wykonywanie ponownego rozruchu.</span><span class="sxs-lookup"><span data-stu-id="dd07c-186">Prevents the Setup program from rebooting automatically.</span></span> <span data-ttu-id="dd07c-187">Użycie tej opcji spowoduje, że program Configuration Manager będzie musiał obsługiwać ponowne uruchamianie komputera.</span><span class="sxs-lookup"><span data-stu-id="dd07c-187">If you use this option, Configuration Manager must handle the computer restart.</span></span>|
|<span data-ttu-id="dd07c-188">**/chainingpackage** *pakietname*</span><span class="sxs-lookup"><span data-stu-id="dd07c-188">**/chainingpackage** *PackageName*</span></span>|<span data-ttu-id="dd07c-189">Określa nazwę pakietu, który tworzy łańcuch.</span><span class="sxs-lookup"><span data-stu-id="dd07c-189">Specifies the name of the package that is doing the chaining.</span></span> <span data-ttu-id="dd07c-190">Te informacje są zgłaszane z innymi informacjami sesji instalacji dla tych, którzy zarejestrowali się w programie Microsoft Program poprawy jakości obsługi klienta (CEIP).</span><span class="sxs-lookup"><span data-stu-id="dd07c-190">This information is reported with other installation session information for those who have signed up for the Microsoft Customer Experience Improvement Program (CEIP).</span></span> <span data-ttu-id="dd07c-191">Jeśli nazwa pakietu zawiera spacje, użyj podwójnych cudzysłowów jako ograniczników; na przykład: **/chainingpackage "iloczyn łańcucha"**.</span><span class="sxs-lookup"><span data-stu-id="dd07c-191">If the package name includes spaces, use double quotation marks as delimiters; for example: **/chainingpackage "Chaining Product"**.</span></span>|

<span data-ttu-id="dd07c-192">Wykonanie tych kroków spowoduje utworzenie pakietu o nazwie .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="dd07c-192">These steps create a package named .NET Framework 4.5.</span></span> <span data-ttu-id="dd07c-193">Program wdraża instalację dyskretną .NET Framework 4,5.</span><span class="sxs-lookup"><span data-stu-id="dd07c-193">The program deploys a silent installation of .NET Framework 4.5.</span></span> <span data-ttu-id="dd07c-194">W przypadku instalacji dyskretnej użytkownicy nie pracują z procesem instalacji, a aplikacja łańcucha musi przechwycić kod powrotny i obsłużyć ponowne uruchomienie. Zobacz [Uzyskiwanie informacji o postępie z pakietu instalacyjnego](/previous-versions/cc825975(v=vs.100)).</span><span class="sxs-lookup"><span data-stu-id="dd07c-194">In a silent installation, users do not interact with the installation process, and the chaining application has to capture the return code and handle rebooting; see [Getting Progress Information from an Installation Package](/previous-versions/cc825975(v=vs.100)).</span></span>

<a name="select_dist_point"></a>

### <a name="select-a-distribution-point"></a><span data-ttu-id="dd07c-195">Wybieranie punktu dystrybucji</span><span class="sxs-lookup"><span data-stu-id="dd07c-195">Select a distribution point</span></span>

<span data-ttu-id="dd07c-196">Aby dystrybuować pakiet i program na komputery klienckie z serwera, należy najpierw wyznaczyć system lokacji jako punkt dystrybucji, a następnie dystrybuować pakiet do punktu dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="dd07c-196">To distribute the package and program to client computers from a server, you must first designate a site system as a distribution point and then distribute the package to the distribution point.</span></span>

<span data-ttu-id="dd07c-197">Wykonując poniższe kroki, można wybrać punkt dystrybucji dla pakietu programu .NET Framework 4.5 utworzonego w poprzedniej sekcji:</span><span class="sxs-lookup"><span data-stu-id="dd07c-197">Use the following steps to select a distribution point for the .NET Framework 4.5 package you created in the previous section:</span></span>

1. <span data-ttu-id="dd07c-198">W konsoli Configuration Manager wybierz pozycję **Biblioteka oprogramowania**.</span><span class="sxs-lookup"><span data-stu-id="dd07c-198">In the Configuration Manager console, choose **Software Library**.</span></span>

2. <span data-ttu-id="dd07c-199">W obszarze roboczym **Biblioteka oprogramowania** rozwiń węzeł **Zarządzanie aplikacjami**, a następnie wybierz pozycję **pakiety**.</span><span class="sxs-lookup"><span data-stu-id="dd07c-199">In the **Software Library** workspace, expand **Application Management**, and then choose **Packages**.</span></span>

3. <span data-ttu-id="dd07c-200">Z listy pakietów wybierz pakiet **.NET Framework 4,5** , który został utworzony w poprzedniej sekcji.</span><span class="sxs-lookup"><span data-stu-id="dd07c-200">From the list of packages, select the package **.NET Framework 4.5** that you created in the previous section.</span></span>

4. <span data-ttu-id="dd07c-201">Na karcie **Narzędzia główne** w grupie **wdrożenie** wybierz pozycję **Dystrybuuj zawartość**.</span><span class="sxs-lookup"><span data-stu-id="dd07c-201">On the **Home** tab, in the **Deployment** group, choose **Distribute Content**.</span></span>

5. <span data-ttu-id="dd07c-202">Na karcie **Ogólne** w **Kreatorze dystrybucji zawartości** wybierz pozycję **dalej**.</span><span class="sxs-lookup"><span data-stu-id="dd07c-202">On the **General** tab of the **Distribute Content Wizard**, choose **Next**.</span></span>

6. <span data-ttu-id="dd07c-203">Na stronie **miejsce docelowe zawartości** kreatora wybierz pozycję **Dodaj**, a następnie wybierz pozycję **punkt dystrybucji**.</span><span class="sxs-lookup"><span data-stu-id="dd07c-203">On the **Content Destination** page of the wizard, choose **Add**, and then choose **Distribution Point**.</span></span>

7. <span data-ttu-id="dd07c-204">W oknie dialogowym **Dodawanie punktów dystrybucji** wybierz punkty dystrybucji, które będą obsługiwać pakiet i program, a następnie wybierz **przycisk OK**.</span><span class="sxs-lookup"><span data-stu-id="dd07c-204">In the **Add Distribution Points** dialog box, select the distribution point(s) that will host the package and program, and then choose **OK**.</span></span>

8. <span data-ttu-id="dd07c-205">Wykonaj kroki kreatora.</span><span class="sxs-lookup"><span data-stu-id="dd07c-205">Complete the wizard.</span></span>

<span data-ttu-id="dd07c-206">Pakiet zawiera teraz wszystkie informacje potrzebne do dyskretnego wdrożenia .NET Framework 4,5.</span><span class="sxs-lookup"><span data-stu-id="dd07c-206">The package now contains all the information you need to silently deploy .NET Framework 4.5.</span></span> <span data-ttu-id="dd07c-207">Przed wdrożeniem pakietu i programu należy się upewnić, że został on zainstalowany w punkcie dystrybucji. Zobacz sekcję "Monitorowanie stanu zawartości" tematu [monitorowanie zawartości dystrybuowanej za pomocą Configuration Manager](/configmgr/core/servers/deploy/configure/monitor-content-you-have-distributed) w bibliotece Configuration Manager dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="dd07c-207">Before you deploy the package and program, verify that it was installed on the distribution point; see the "Content status monitoring" section of [Monitor content you distribute with Configuration Manager](/configmgr/core/servers/deploy/configure/monitor-content-you-have-distributed) in the Configuration Manager Documentation Library.</span></span>

<a name="deploying_package"></a>

### <a name="deploy-the-package"></a><span data-ttu-id="dd07c-208">Wdrażanie pakietu</span><span class="sxs-lookup"><span data-stu-id="dd07c-208">Deploy the package</span></span>

<span data-ttu-id="dd07c-209">Aby wdrożyć pakiet i program .NET Framework 4.5:</span><span class="sxs-lookup"><span data-stu-id="dd07c-209">To deploy the .NET Framework 4.5 package and program:</span></span>

1. <span data-ttu-id="dd07c-210">W konsoli Configuration Manager wybierz pozycję **Biblioteka oprogramowania**.</span><span class="sxs-lookup"><span data-stu-id="dd07c-210">In the Configuration Manager console, choose **Software Library**.</span></span>

2. <span data-ttu-id="dd07c-211">W obszarze roboczym **Biblioteka oprogramowania** rozwiń węzeł **Zarządzanie aplikacjami**, a następnie wybierz pozycję **pakiety**.</span><span class="sxs-lookup"><span data-stu-id="dd07c-211">In the **Software Library** workspace, expand **Application Management**, and then choose **Packages**.</span></span>

3. <span data-ttu-id="dd07c-212">Z listy pakietów wybierz utworzony pakiet o nazwie **.NET Framework 4,5**.</span><span class="sxs-lookup"><span data-stu-id="dd07c-212">From the list of packages, select the package you created named **.NET Framework 4.5**.</span></span>

4. <span data-ttu-id="dd07c-213">Na karcie **Narzędzia główne** w grupie **wdrożenie** wybierz pozycję **Wdróż**.</span><span class="sxs-lookup"><span data-stu-id="dd07c-213">On the **Home** tab, in the **Deployment** group, choose **Deploy**.</span></span>

5. <span data-ttu-id="dd07c-214">Na stronie **Ogólne** **Kreatora wdrażania oprogramowania** wybierz pozycję **Przeglądaj**, a następnie wybierz utworzoną wcześniej kolekcję.</span><span class="sxs-lookup"><span data-stu-id="dd07c-214">On the **General** page of the **Deploy Software Wizard**, choose **Browse**, and then select the collection that you created earlier.</span></span> <span data-ttu-id="dd07c-215">Wybierz pozycję **Next** (Dalej).</span><span class="sxs-lookup"><span data-stu-id="dd07c-215">Choose **Next**.</span></span>

6. <span data-ttu-id="dd07c-216">Na stronie **zawartość** kreatora sprawdź, czy jest wyświetlany punkt, z którego ma zostać rozdystrybuowane oprogramowanie, a następnie wybierz przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="dd07c-216">On the **Content** page of the wizard, verify that the point from which you want to distribute the software is displayed, and then choose **Next**.</span></span>

7. <span data-ttu-id="dd07c-217">Na stronie **Ustawienia wdrożenia** w Kreatorze upewnij się, że **Akcja** jest ustawiona na **Zainstaluj**, a **cel** jest ustawiony na wartość **wymagane**.</span><span class="sxs-lookup"><span data-stu-id="dd07c-217">On the **Deployment Settings** page of the wizard, confirm that **Action** is set to **Install**, and **Purpose** is set to **Required**.</span></span> <span data-ttu-id="dd07c-218">Te wartości ustawień gwarantują, że pakiet oprogramowania będzie obowiązkowo instalowany na komputerach docelowych.</span><span class="sxs-lookup"><span data-stu-id="dd07c-218">This ensures that the software package will be a mandatory installation on the targeted computers.</span></span> <span data-ttu-id="dd07c-219">Wybierz pozycję **Next** (Dalej).</span><span class="sxs-lookup"><span data-stu-id="dd07c-219">Choose **Next**.</span></span>

8. <span data-ttu-id="dd07c-220">Na stronie **Planowanie** w Kreatorze Określ, kiedy mają być instalowane .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="dd07c-220">On the **Scheduling** page of the wizard, specify when you want .NET Framework to be installed.</span></span> <span data-ttu-id="dd07c-221">Możesz wybrać opcję **Nowy** , aby przypisać czas instalacji lub poinstruować oprogramowanie, które ma zostać zainstalowane, gdy użytkownik się zaloguje lub wyłączy lub najszybciej, jak to możliwe.</span><span class="sxs-lookup"><span data-stu-id="dd07c-221">You can choose **New** to assign an installation time, or instruct the software to install when the user logs on or off, or as soon as possible.</span></span> <span data-ttu-id="dd07c-222">Wybierz pozycję **Next** (Dalej).</span><span class="sxs-lookup"><span data-stu-id="dd07c-222">Choose **Next**.</span></span>

9. <span data-ttu-id="dd07c-223">Na stronie **środowisko użytkownika** kreatora Użyj wartości domyślnych i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="dd07c-223">On the **User Experience** page of the wizard, use the default values and choose **Next**.</span></span>

    > [!WARNING]
    > <span data-ttu-id="dd07c-224">W środowisku produkcyjnym mogą obowiązywać zasady wymagające wybrania innych ustawień harmonogramu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="dd07c-224">Your production environment might have policies that require different selections for the deployment schedule.</span></span>

10. <span data-ttu-id="dd07c-225">Na stronie **punkty dystrybucji** kreatora Użyj wartości domyślnych i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="dd07c-225">On the **Distribution Points** page of the wizard, use the default values and choose **Next**.</span></span>

11. <span data-ttu-id="dd07c-226">Wykonaj kroki kreatora.</span><span class="sxs-lookup"><span data-stu-id="dd07c-226">Complete the wizard.</span></span> <span data-ttu-id="dd07c-227">Postęp wdrożenia można monitorować w węźle **wdrożenia** obszaru roboczego **monitorowanie** .</span><span class="sxs-lookup"><span data-stu-id="dd07c-227">You can monitor the progress of the deployment in the **Deployments** node of the **Monitoring** workspace.</span></span>

<span data-ttu-id="dd07c-228">Teraz pakiet zostanie wdrożony w kolekcji docelowej i rozpocznie się dyskretna instalacja programu .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="dd07c-228">The package will now be deployed to the targeted collection and the silent installation of .NET Framework 4.5 will begin.</span></span> <span data-ttu-id="dd07c-229">Informacje o kodach błędów instalacji .NET Framework 4,5 znajdują się w sekcji [kody powrotne](#return_codes) w dalszej części tego tematu.</span><span class="sxs-lookup"><span data-stu-id="dd07c-229">For information about .NET Framework 4.5 installation error codes, see the [Return Codes](#return_codes) section later in this topic.</span></span>

<a name="resources"></a>

## <a name="resources"></a><span data-ttu-id="dd07c-230">Zasoby</span><span class="sxs-lookup"><span data-stu-id="dd07c-230">Resources</span></span>

<span data-ttu-id="dd07c-231">Aby uzyskać więcej informacji na temat infrastruktury testowania wdrożenia pakietu redystrybucyjnego .NET Framework 4,5, zobacz następujące zasoby.</span><span class="sxs-lookup"><span data-stu-id="dd07c-231">For more information about the infrastructure for testing the deployment of the .NET Framework 4.5 redistributable package, see the following resources.</span></span>

<span data-ttu-id="dd07c-232">**Active Directory, DNS, DHCP:**</span><span class="sxs-lookup"><span data-stu-id="dd07c-232">**Active Directory, DNS, DHCP:**</span></span>

- [<span data-ttu-id="dd07c-233">Active Directory Domain Services</span><span class="sxs-lookup"><span data-stu-id="dd07c-233">Active Directory Domain Services</span></span>](/windows/desktop/ad/active-directory-domain-services)

- [<span data-ttu-id="dd07c-234">System nazw domen (DNS)</span><span class="sxs-lookup"><span data-stu-id="dd07c-234">Domain Name System (DNS)</span></span>](/windows-server/networking/dns/dns-top)

- [<span data-ttu-id="dd07c-235">Protokół DHCP</span><span class="sxs-lookup"><span data-stu-id="dd07c-235">Dynamic Host Configuration Protocol (DHCP)</span></span>](/windows-server/networking/technologies/dhcp/dhcp-top)

<span data-ttu-id="dd07c-236">**SQL Server 2008:**</span><span class="sxs-lookup"><span data-stu-id="dd07c-236">**SQL Server 2008:**</span></span>

- <span data-ttu-id="dd07c-237">[Instalowanie SQL Server 2008 (SQL Server wideo)](/previous-versions/sql/sql-server-2008/dd299415(v=sql.100))</span><span class="sxs-lookup"><span data-stu-id="dd07c-237">[Installing SQL Server 2008 (SQL Server Video)](/previous-versions/sql/sql-server-2008/dd299415(v=sql.100))</span></span>

- [<span data-ttu-id="dd07c-238">SQL Server 2008 — Omówienie zabezpieczeń dla administratorów bazy danych</span><span class="sxs-lookup"><span data-stu-id="dd07c-238">SQL Server 2008 Security Overview for Database Administrators</span></span>](https://download.microsoft.com/download/a/c/d/acd8e043-d69b-4f09-bc9e-4168b65aaa71/SQL2008SecurityOverviewforAdmins.docx)

<span data-ttu-id="dd07c-239">**Configuration Manager programu System Center 2012 (punkt zarządzania, punkt dystrybucji):**</span><span class="sxs-lookup"><span data-stu-id="dd07c-239">**System Center 2012 Configuration Manager (Management Point, Distribution Point):**</span></span>

- <span data-ttu-id="dd07c-240">[Administrowanie lokacją dla programu System Center 2012 Configuration Manager](/previous-versions/system-center/system-center-2012-R2/gg681983(v=technet.10))</span><span class="sxs-lookup"><span data-stu-id="dd07c-240">[Site Administration for System Center 2012 Configuration Manager](/previous-versions/system-center/system-center-2012-R2/gg681983(v=technet.10))</span></span>

<span data-ttu-id="dd07c-241">**Klient programu System Center 2012 Configuration Manager dla komputerów z systemem Windows:**</span><span class="sxs-lookup"><span data-stu-id="dd07c-241">**System Center 2012 Configuration Manager client for Windows computers:**</span></span>

- <span data-ttu-id="dd07c-242">[Wdrażanie klientów dla programu System Center 2012 Configuration Manager](/previous-versions/system-center/system-center-2012-R2/gg699391(v=technet.10))</span><span class="sxs-lookup"><span data-stu-id="dd07c-242">[Deploying Clients for System Center 2012 Configuration Manager](/previous-versions/system-center/system-center-2012-R2/gg699391(v=technet.10))</span></span>

<a name="troubleshooting"></a>

## <a name="troubleshooting"></a><span data-ttu-id="dd07c-243">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="dd07c-243">Troubleshooting</span></span>

### <a name="log-file-locations"></a><span data-ttu-id="dd07c-244">Lokalizacje plików dziennika</span><span class="sxs-lookup"><span data-stu-id="dd07c-244">Log file locations</span></span>

<span data-ttu-id="dd07c-245">Podczas instalacji .NET Framework są generowane następujące pliki dziennika:</span><span class="sxs-lookup"><span data-stu-id="dd07c-245">The following log files are generated during .NET Framework setup:</span></span>

- <span data-ttu-id="dd07c-246">%temp%\Microsoft .NET Framework *wersja* \* . txt</span><span class="sxs-lookup"><span data-stu-id="dd07c-246">%temp%\Microsoft .NET Framework *version*\*.txt</span></span>
- <span data-ttu-id="dd07c-247">%temp%\Microsoft .NET Framework *wersja* \* . html</span><span class="sxs-lookup"><span data-stu-id="dd07c-247">%temp%\Microsoft .NET Framework *version*\*.html</span></span>

<span data-ttu-id="dd07c-248">*wersja* , w której jest instalowana wersja .NET Framework, na przykład 4,5 lub 4.7.2.</span><span class="sxs-lookup"><span data-stu-id="dd07c-248">where *version* is the version of .NET Framework that you're installing, such as 4.5 or 4.7.2.</span></span>

<span data-ttu-id="dd07c-249">Możesz również określić katalog, w którym zapisywane są pliki dziennika przy użyciu `/log` opcji wiersza polecenia w .NET Framework polecenie instalacji.</span><span class="sxs-lookup"><span data-stu-id="dd07c-249">You can also specify the directory to which log files are written by using the `/log` command-line option in the .NET Framework installation command.</span></span> <span data-ttu-id="dd07c-250">Aby uzyskać więcej informacji, zobacz [.NET Framework Przewodnik wdrażania dla deweloperów](deployment-guide-for-developers.md#command-line-options).</span><span class="sxs-lookup"><span data-stu-id="dd07c-250">For more information, see [.NET Framework deployment guide for developers](deployment-guide-for-developers.md#command-line-options).</span></span>

<span data-ttu-id="dd07c-251">Za pomocą narzędzia do [zbierania dzienników](https://www.microsoft.com/download/details.aspx?id=12493) można zbierać pliki dziennika .NET Framework i utworzyć skompresowany plik Cabinet (CAB), który zmniejsza rozmiar plików.</span><span class="sxs-lookup"><span data-stu-id="dd07c-251">You can use the [log collection tool](https://www.microsoft.com/download/details.aspx?id=12493) to collect the .NET Framework log files and to create a compressed cabinet (.cab) file that reduces the size of the files.</span></span>

<a name="return_codes"></a>

### <a name="return-codes"></a><span data-ttu-id="dd07c-252">Kody powrotne</span><span class="sxs-lookup"><span data-stu-id="dd07c-252">Return codes</span></span>

<span data-ttu-id="dd07c-253">W poniższej tabeli wymieniono najbardziej typowe kody powrotu z programu instalacyjnego pakietu redystrybucyjnego .NET Framework 4,5.</span><span class="sxs-lookup"><span data-stu-id="dd07c-253">The following table lists the most common return codes from the .NET Framework 4.5 redistributable installation program.</span></span> <span data-ttu-id="dd07c-254">Kody powrotne są takie same dla wszystkich wersji instalatora.</span><span class="sxs-lookup"><span data-stu-id="dd07c-254">The return codes are the same for all versions of the installer.</span></span>

<span data-ttu-id="dd07c-255">Aby uzyskać linki do szczegółowych informacji, zobacz następną sekcję, [pobieranie kodów błędów](#additional_error_codes).</span><span class="sxs-lookup"><span data-stu-id="dd07c-255">For links to detailed information, see the next section, [Download error codes](#additional_error_codes).</span></span>

|<span data-ttu-id="dd07c-256">Kod powrotu</span><span class="sxs-lookup"><span data-stu-id="dd07c-256">Return code</span></span>|<span data-ttu-id="dd07c-257">Opis</span><span class="sxs-lookup"><span data-stu-id="dd07c-257">Description</span></span>|
|-----------------|-----------------|
|<span data-ttu-id="dd07c-258">0</span><span class="sxs-lookup"><span data-stu-id="dd07c-258">0</span></span>|<span data-ttu-id="dd07c-259">Instalacja została zakończona pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="dd07c-259">Installation completed successfully.</span></span>|
|<span data-ttu-id="dd07c-260">1602</span><span class="sxs-lookup"><span data-stu-id="dd07c-260">1602</span></span>|<span data-ttu-id="dd07c-261">Użytkownik anulował instalację.</span><span class="sxs-lookup"><span data-stu-id="dd07c-261">The user canceled installation.</span></span>|
|<span data-ttu-id="dd07c-262">1603</span><span class="sxs-lookup"><span data-stu-id="dd07c-262">1603</span></span>|<span data-ttu-id="dd07c-263">Podczas instalacji wystąpił błąd krytyczny.</span><span class="sxs-lookup"><span data-stu-id="dd07c-263">A fatal error occurred during installation.</span></span>|
|<span data-ttu-id="dd07c-264">1641</span><span class="sxs-lookup"><span data-stu-id="dd07c-264">1641</span></span>|<span data-ttu-id="dd07c-265">Do ukończenia instalacji wymagane jest ponowne uruchomienie komputera.</span><span class="sxs-lookup"><span data-stu-id="dd07c-265">A restart is required to complete the installation.</span></span> <span data-ttu-id="dd07c-266">Ten komunikat oznacza sukces.</span><span class="sxs-lookup"><span data-stu-id="dd07c-266">This message indicates success.</span></span>|
|<span data-ttu-id="dd07c-267">3010</span><span class="sxs-lookup"><span data-stu-id="dd07c-267">3010</span></span>|<span data-ttu-id="dd07c-268">Do ukończenia instalacji wymagane jest ponowne uruchomienie komputera.</span><span class="sxs-lookup"><span data-stu-id="dd07c-268">A restart is required to complete the installation.</span></span> <span data-ttu-id="dd07c-269">Ten komunikat oznacza sukces.</span><span class="sxs-lookup"><span data-stu-id="dd07c-269">This message indicates success.</span></span>|
|<span data-ttu-id="dd07c-270">5100</span><span class="sxs-lookup"><span data-stu-id="dd07c-270">5100</span></span>|<span data-ttu-id="dd07c-271">Komputer użytkownika nie spełnia wymagań systemowych.</span><span class="sxs-lookup"><span data-stu-id="dd07c-271">The user's computer does not meet system requirements.</span></span>|

<a name="additional_error_codes"></a>

### <a name="download-error-codes"></a><span data-ttu-id="dd07c-272">Kody błędów pobierania</span><span class="sxs-lookup"><span data-stu-id="dd07c-272">Download error codes</span></span>

- [<span data-ttu-id="dd07c-273">Kody błędów Usługa inteligentnego transferu w tle (bity)</span><span class="sxs-lookup"><span data-stu-id="dd07c-273">Background Intelligent Transfer Service (BITS) error codes</span></span>](/windows/desktop/Bits/bits-return-values)

- <span data-ttu-id="dd07c-274">[Kody błędów monikera adresu URL](/previous-versions/windows/internet-explorer/ie-developer/platform-apis/ms775145(v=vs.85))</span><span class="sxs-lookup"><span data-stu-id="dd07c-274">[URL moniker error codes](/previous-versions/windows/internet-explorer/ie-developer/platform-apis/ms775145(v=vs.85))</span></span>

- [<span data-ttu-id="dd07c-275">Kody błędów usługi WinHttp</span><span class="sxs-lookup"><span data-stu-id="dd07c-275">WinHttp error codes</span></span>](/windows/desktop/WinHttp/error-messages)

<span data-ttu-id="dd07c-276">Inne kody błędów:</span><span class="sxs-lookup"><span data-stu-id="dd07c-276">Other error codes:</span></span>

- [<span data-ttu-id="dd07c-277">Instalator Windows kody błędów</span><span class="sxs-lookup"><span data-stu-id="dd07c-277">Windows Installer error codes</span></span>](/windows/desktop/msi/error-codes)

- <span data-ttu-id="dd07c-278">[Kody wyników agenta Windows Update](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc720442(v=ws.10))</span><span class="sxs-lookup"><span data-stu-id="dd07c-278">[Windows Update Agent result codes](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc720442(v=ws.10))</span></span>

## <a name="see-also"></a><span data-ttu-id="dd07c-279">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="dd07c-279">See also</span></span>

- [<span data-ttu-id="dd07c-280">Przewodnik wdrażania dla deweloperów</span><span class="sxs-lookup"><span data-stu-id="dd07c-280">Deployment Guide for Developers</span></span>](deployment-guide-for-developers.md)
- [<span data-ttu-id="dd07c-281">Wymagania systemowe</span><span class="sxs-lookup"><span data-stu-id="dd07c-281">System Requirements</span></span>](../get-started/system-requirements.md)
