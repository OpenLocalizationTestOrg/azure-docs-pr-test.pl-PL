---
title: "Program Azure PowerShell Menedżera zasobów na podstawie polecenia dla aplikacji sieci Web platformy Azure | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie użycia nowych poleceń na podstawie Menedżera zasobów Azure PowerShell do zarządzania aplikacjami sieci Web platformy Azure."
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: 4231fbba-61e5-4f92-b958-531c066fb87f
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/29/2016
ms.author: aelnably
ms.openlocfilehash: 8d574f051a327ba0409e6f25a5886af673d3d5e0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="using-azure-resource-manager-based-powershell-to-manage-azure-web-apps"></a><span data-ttu-id="41828-103">Przy użyciu zasobów platformy Azure na podstawie menedżera programu PowerShell do zarządzania aplikacjami sieci Web platformy Azure</span><span class="sxs-lookup"><span data-stu-id="41828-103">Using Azure Resource Manager-Based PowerShell to Manage Azure Web Apps</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="41828-104">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="41828-104">Azure CLI</span></span>](app-service-web-app-azure-resource-manager-xplat-cli.md)
> * [<span data-ttu-id="41828-105">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="41828-105">Azure PowerShell</span></span>](app-service-web-app-azure-resource-manager-powershell.md)
> 
> 

<span data-ttu-id="41828-106">Przy użyciu programu Microsoft Azure PowerShell w wersji 1.0.0 zostały dodane nowe polecenia, który dać użytkownikowi możliwość używania poleceń programu PowerShell z systemem Azure Resource Manager do zarządzania aplikacjami sieci Web.</span><span class="sxs-lookup"><span data-stu-id="41828-106">With Microsoft Azure PowerShell version 1.0.0 new commands have been added, that give the user the ability to use Azure Resource Manager-based PowerShell commands to manage Web Apps.</span></span>

<span data-ttu-id="41828-107">Aby dowiedzieć się więcej o zarządzaniu grupami zasobów, zobacz [przy użyciu programu Azure PowerShell z usługą Azure Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="41828-107">To learn about managing Resource Groups, see [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span> 

<span data-ttu-id="41828-108">Aby zapoznać się z pełną listą parametrów i opcje dla polecenia cmdlet programu PowerShell, zobacz [pełne odwołania do polecenia Cmdlet oparte na sieci Web aplikacji usługi Azure Resource Manager poleceń cmdlet programu PowerShell](https://msdn.microsoft.com/library/mt619237.aspx)</span><span class="sxs-lookup"><span data-stu-id="41828-108">To learn about the full list of parameters and options for the PowerShell cmdlets, see the [full Cmdlet Reference of Web App Azure Resource Manager-based PowerShell Cmdlets](https://msdn.microsoft.com/library/mt619237.aspx)</span></span>

## <a name="managing-app-service-plans"></a><span data-ttu-id="41828-109">Plany zarządzania z usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="41828-109">Managing App Service Plans</span></span>
### <a name="create-an-app-service-plan"></a><span data-ttu-id="41828-110">Tworzenie planu usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="41828-110">Create an App Service Plan</span></span>
<span data-ttu-id="41828-111">Aby utworzyć plan usługi aplikacji, użyj **AzureRmAppServicePlan nowy** polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="41828-111">To create an app service plan, use the **New-AzureRmAppServicePlan** cmdlet.</span></span>

<span data-ttu-id="41828-112">Poniżej przedstawiono opisy różnych parametrów:</span><span class="sxs-lookup"><span data-stu-id="41828-112">Following are descriptions of the different parameters:</span></span>

* <span data-ttu-id="41828-113">**Nazwa**: Nazwa planu usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="41828-113">**Name**: name of the app service plan.</span></span>
* <span data-ttu-id="41828-114">**Lokalizacja**: usługa lokalizacji planu.</span><span class="sxs-lookup"><span data-stu-id="41828-114">**Location**: service plan location.</span></span>
* <span data-ttu-id="41828-115">**ResourceGroupName**: grupy zasobów, która zawiera plan usługi aplikacji nowo utworzony.</span><span class="sxs-lookup"><span data-stu-id="41828-115">**ResourceGroupName**: resource group that includes the newly created app service plan.</span></span>
* <span data-ttu-id="41828-116">**Warstwa**: żądanej warstwy cenowej (domyślna to bezpłatna, inne opcje są współużytkowane, podstawowa, standardowa i Premium).</span><span class="sxs-lookup"><span data-stu-id="41828-116">**Tier**:  the desired pricing tier (Default is Free, other options are Shared, Basic, Standard, and Premium.)</span></span>
* <span data-ttu-id="41828-117">**WorkerSize**: rozmiar pracowników (wartość domyślna to mały, jeśli określono parametr warstwy jako podstawowa, standardowa lub Premium.</span><span class="sxs-lookup"><span data-stu-id="41828-117">**WorkerSize**: the size of workers (Default is small if the Tier parameter was specified as Basic, Standard, or Premium.</span></span> <span data-ttu-id="41828-118">Inne opcje są średni i duży).</span><span class="sxs-lookup"><span data-stu-id="41828-118">Other options are Medium, and Large.)</span></span>
* <span data-ttu-id="41828-119">**NumberofWorkers**: liczba pracowników w aplikacji usługi plan (wartość domyślna to 1).</span><span class="sxs-lookup"><span data-stu-id="41828-119">**NumberofWorkers**: the number of workers in the app service plan (Default value is 1).</span></span> 

<span data-ttu-id="41828-120">Przykład można używać tego polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="41828-120">Example to use this cmdlet:</span></span>

    New-AzureRmAppServicePlan -Name ContosoAppServicePlan -Location "South Central US" -ResourceGroupName ContosoAzureResourceGroup -Tier Premium -WorkerSize Large -NumberofWorkers 10

### <a name="create-an-app-service-plan-in-an-app-service-environment"></a><span data-ttu-id="41828-121">Tworzenie planu usługi aplikacji w środowisku usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="41828-121">Create an App Service Plan in an App Service Environment</span></span>
<span data-ttu-id="41828-122">Aby utworzyć plan usługi aplikacji w środowisku usługi aplikacji, użyj tego samego polecenia **AzureRmAppServicePlan nowy** z dodatkowe parametry, aby określić nazwę ASE i nazwa grupy zasobów w ASE.</span><span class="sxs-lookup"><span data-stu-id="41828-122">To create an app service plan in an app service environment, use the same command **New-AzureRmAppServicePlan** command with extra parameters to specify the ASE's name and ASE's resource group name.</span></span>

<span data-ttu-id="41828-123">Przykład można używać tego polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="41828-123">Example to use this cmdlet:</span></span>

    New-AzureRmAppServicePlan -Name ContosoAppServicePlan -Location "South Central US" -ResourceGroupName ContosoAzureResourceGroup -AseName constosoASE -AseResourceGroupName contosoASERG -Tier Premium -WorkerSize Large -NumberofWorkers 10

<span data-ttu-id="41828-124">Aby dowiedzieć się więcej na temat środowiska usługi aplikacji, sprawdź [wprowadzenie do środowiska usługi aplikacji](app-service-app-service-environment-intro.md)</span><span class="sxs-lookup"><span data-stu-id="41828-124">To learn more about app service environment, check [Introduction to App Service Environment](app-service-app-service-environment-intro.md)</span></span>

### <a name="list-existing-app-service-plans"></a><span data-ttu-id="41828-125">Lista istniejących planów usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="41828-125">List Existing App Service Plans</span></span>
<span data-ttu-id="41828-126">Aby wyświetlić listę istniejących planów usługi aplikacji, należy użyć **Get-AzureRmAppServicePlan** polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="41828-126">To list the existing app service plans, use **Get-AzureRmAppServicePlan** cmdlet.</span></span>

<span data-ttu-id="41828-127">Aby wyświetlić listę wszystkich planów usługi aplikacji w ramach Twojej subskrypcji, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="41828-127">To list all app service plans under your subscription, use:</span></span> 

    Get-AzureRmAppServicePlan

<span data-ttu-id="41828-128">Aby wyświetlić listę wszystkich planów usługi aplikacji w obszarze określonej grupy zasobów, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="41828-128">To list all app service plans under a specific resource group, use:</span></span>

    Get-AzureRmAppServicePlan -ResourceGroupname ContosoAzureResourceGroup

<span data-ttu-id="41828-129">Aby uzyskać plan usługi specyficzne dla aplikacji, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="41828-129">To get a specific app service plan, use:</span></span>

    Get-AzureRmAppServicePlan -Name ContosoAppServicePlan


### <a name="configure-an-existing-app-service-plan"></a><span data-ttu-id="41828-130">Skonfiguruj istniejący Plan usługi App Service</span><span class="sxs-lookup"><span data-stu-id="41828-130">Configure an existing App Service Plan</span></span>
<span data-ttu-id="41828-131">Aby zmienić ustawienia dla istniejącego planu usługi aplikacji, należy użyć **AzureRmAppServicePlan zestaw** polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="41828-131">To change the settings for an existing app service plan, use the **Set-AzureRmAppServicePlan** cmdlet.</span></span> <span data-ttu-id="41828-132">Możesz zmienić warstwę, rozmiar procesu roboczego oraz liczbę procesów roboczych</span><span class="sxs-lookup"><span data-stu-id="41828-132">You can change the tier, worker size, and the number of workers</span></span> 

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Tier Standard -WorkerSize Medium -NumberofWorkers 9

#### <a name="scaling-an-app-service-plan"></a><span data-ttu-id="41828-133">Skalowanie planu usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="41828-133">Scaling an App Service Plan</span></span>
<span data-ttu-id="41828-134">Aby skalować istniejący Plan usługi App Service, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="41828-134">To scale an existing App Service Plan, use:</span></span>

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -NumberofWorkers 9

#### <a name="changing-the-worker-size-of-an-app-service-plan"></a><span data-ttu-id="41828-135">Zmiana rozmiaru procesu roboczego planu usługi App Service</span><span class="sxs-lookup"><span data-stu-id="41828-135">Changing the worker size of an App Service Plan</span></span>
<span data-ttu-id="41828-136">Aby zmienić rozmiar pracowników w istniejący Plan usługi App Service, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="41828-136">To change the size of workers in an existing App Service Plan, use:</span></span>

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -WorkerSize Medium

#### <a name="changing-the-tier-of-an-app-service-plan"></a><span data-ttu-id="41828-137">Zmiana warstwy Plan usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="41828-137">Changing the Tier of an App Service Plan</span></span>
<span data-ttu-id="41828-138">Aby zmienić warstwę z istniejącego planu usługi App Service, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="41828-138">To change the tier of an existing App Service Plan, use:</span></span>

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Tier Standard

### <a name="delete-an-existing-app-service-plan"></a><span data-ttu-id="41828-139">Usuń istniejący Plan usługi App Service</span><span class="sxs-lookup"><span data-stu-id="41828-139">Delete an existing App Service Plan</span></span>
<span data-ttu-id="41828-140">Aby usunąć istniejący plan usługi aplikacji, wszystkie aplikacje sieci web przypisanej należy przenieść lub usunięciem.</span><span class="sxs-lookup"><span data-stu-id="41828-140">To delete an existing app service plan, all assigned web apps need to be moved or deleted first.</span></span> <span data-ttu-id="41828-141">Następnie przy użyciu **AzureRmAppServicePlan Usuń** polecenia cmdlet można usunąć planu usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="41828-141">Then using the **Remove-AzureRmAppServicePlan** cmdlet you can delete the app service plan.</span></span>

    Remove-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup

## <a name="managing-app-service-web-apps"></a><span data-ttu-id="41828-142">Zarządzanie aplikacjami sieci Web usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="41828-142">Managing App Service Web Apps</span></span>
### <a name="create-a-web-app"></a><span data-ttu-id="41828-143">Tworzenie aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="41828-143">Create a Web App</span></span>
<span data-ttu-id="41828-144">Aby utworzyć aplikację sieci web, użyj **AzureRmWebApp nowy** polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="41828-144">To create a web app, use the **New-AzureRmWebApp** cmdlet.</span></span>

<span data-ttu-id="41828-145">Poniżej przedstawiono opisy różnych parametrów:</span><span class="sxs-lookup"><span data-stu-id="41828-145">Following are descriptions of the different parameters:</span></span>

* <span data-ttu-id="41828-146">**Nazwa**: Nazwa aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="41828-146">**Name**: name for the web app.</span></span>
* <span data-ttu-id="41828-147">**AppServicePlan**: Nazwa planu usługi używany do obsługi aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="41828-147">**AppServicePlan**: name for the service plan used to host the web app.</span></span>
* <span data-ttu-id="41828-148">**ResourceGroupName**: grupę zasobów, która obsługuje plan usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="41828-148">**ResourceGroupName**: resource group that hosts the App service plan.</span></span>
* <span data-ttu-id="41828-149">**Lokalizacja**: Lokalizacja aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="41828-149">**Location**: the web app location.</span></span>

<span data-ttu-id="41828-150">Przykład można używać tego polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="41828-150">Example to use this cmdlet:</span></span>

    New-AzureRmWebApp -Name ContosoWebApp -AppServicePlan ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Location "South Central US"

### <a name="create-a-web-app-in-an-app-service-environment"></a><span data-ttu-id="41828-151">Tworzenie aplikacji sieci Web w środowisku usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="41828-151">Create a Web App in an App Service Environment</span></span>
<span data-ttu-id="41828-152">Aby utworzyć aplikację sieci web w środowisku aplikacji (ASE).</span><span class="sxs-lookup"><span data-stu-id="41828-152">To create a web app in an App Service Environment (ASE).</span></span> <span data-ttu-id="41828-153">Używać tego samego **AzureRmWebApp nowy** polecenie z dodatkowych parametrów, aby określić nazwę ASE i grupy zasobów nazw, które ASE należy.</span><span class="sxs-lookup"><span data-stu-id="41828-153">Use the same **New-AzureRmWebApp** command with extra parameters to specify the ASE name and the resource group name that the ASE belongs to.</span></span>

    New-AzureRmWebApp -Name ContosoWebApp -AppServicePlan ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Location "South Central US"  -ASEName ContosoASEName -ASEResourceGroupName ContosoASEResourceGroupName

<span data-ttu-id="41828-154">Aby dowiedzieć się więcej na temat środowiska usługi aplikacji, sprawdź [wprowadzenie do środowiska usługi aplikacji](app-service-app-service-environment-intro.md)</span><span class="sxs-lookup"><span data-stu-id="41828-154">To learn more about app service environment, check [Introduction to App Service Environment](app-service-app-service-environment-intro.md)</span></span>

### <a name="delete-an-existing-web-app"></a><span data-ttu-id="41828-155">Usuń istniejącą aplikację sieci Web</span><span class="sxs-lookup"><span data-stu-id="41828-155">Delete an existing Web App</span></span>
<span data-ttu-id="41828-156">Aby usunąć istniejącą aplikację sieci web można użyć **AzureRmWebApp Usuń** polecenia cmdlet, należy określić nazwę aplikacji sieci web i nazwa grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="41828-156">To delete an existing web app you can use the **Remove-AzureRmWebApp** cmdlet, you need to specify the name of the web app and the resource group name.</span></span>

    Remove-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup


### <a name="list-existing-web-apps"></a><span data-ttu-id="41828-157">Listy istniejących aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="41828-157">List existing Web Apps</span></span>
<span data-ttu-id="41828-158">Aby wyświetlić listę istniejących aplikacji sieci web, należy użyć **Get-AzureRmWebApp** polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="41828-158">To list the existing web apps, use the **Get-AzureRmWebApp** cmdlet.</span></span>

<span data-ttu-id="41828-159">Aby wyświetlić listę wszystkich aplikacji sieci web w ramach Twojej subskrypcji, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="41828-159">To list all web apps under your subscription, use:</span></span>

    Get-AzureRmWebApp

<span data-ttu-id="41828-160">Aby wyświetlić listę wszystkich aplikacji sieci web w obszarze określonej grupy zasobów, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="41828-160">To list all web apps under a specific resource group, use:</span></span>

    Get-AzureRmWebApp -ResourceGroupname ContosoAzureResourceGroup

<span data-ttu-id="41828-161">Aby uzyskać aplikację sieci web określonych, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="41828-161">To get a specific web app, use:</span></span>

    Get-AzureRmWebApp -Name ContosoWebApp

### <a name="configure-an-existing-web-app"></a><span data-ttu-id="41828-162">Konfigurowanie istniejącej aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="41828-162">Configure an existing Web App</span></span>
<span data-ttu-id="41828-163">Aby zmienić ustawienia i konfiguracje dla istniejącej aplikacji sieci web, użyj **AzureRmWebApp zestaw** polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="41828-163">To change the settings and configurations for an existing web app, use the **Set-AzureRmWebApp** cmdlet.</span></span> <span data-ttu-id="41828-164">Aby uzyskać pełną listę parametrów, sprawdź [polecenia Cmdlet opis łącza](https://msdn.microsoft.com/library/mt652487.aspx)</span><span class="sxs-lookup"><span data-stu-id="41828-164">For a full list of parameters, check the [Cmdlet reference link](https://msdn.microsoft.com/library/mt652487.aspx)</span></span>

<span data-ttu-id="41828-165">Przykład (1): Użyj tego polecenia cmdlet, aby zmienić parametry połączenia</span><span class="sxs-lookup"><span data-stu-id="41828-165">Example (1): use this cmdlet to change connection strings</span></span>

    $connectionstrings = @{ ContosoConn1 = @{ Type = “MySql”; Value = “MySqlConn”}; ContosoConn2 = @{ Type = “SQLAzure”; Value = “SQLAzureConn”} }
    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -ConnectionStrings $connectionstrings

<span data-ttu-id="41828-166">Przykład (2): Dodawanie lub zmienianie ustawień aplikacji</span><span class="sxs-lookup"><span data-stu-id="41828-166">Example (2): add or change app settings</span></span>

    $appsettings = @{appsetting1 = "appsetting1value"; appsetting2 = "appsetting2value"}
    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -AppSettings $appsettings


<span data-ttu-id="41828-167">Przykład (3): Ustaw aplikacji sieci web do uruchamiania w trybie 64-bitowym</span><span class="sxs-lookup"><span data-stu-id="41828-167">Example (3):  set the web app to run in 64-bit mode</span></span>

    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -Use32BitWorkerProcess $False

### <a name="change-the-state-of-an-existing-web-app"></a><span data-ttu-id="41828-168">Zmień stan istniejącej aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="41828-168">Change the state of an existing Web App</span></span>
#### <a name="restart-a-web-app"></a><span data-ttu-id="41828-169">Ponowne uruchomienie aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="41828-169">Restart a web app</span></span>
<span data-ttu-id="41828-170">Aby ponownie uruchomić aplikacji sieci web, należy określić nazwę i zasobów Grupa aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="41828-170">To restart a web app, you must specify the name and resource group of the web app.</span></span>

    Restart-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

#### <a name="stop-a-web-app"></a><span data-ttu-id="41828-171">Zatrzymać aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="41828-171">Stop a web app</span></span>
<span data-ttu-id="41828-172">Aby zatrzymać aplikacji sieci web, należy określić nazwę i zasobów Grupa aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="41828-172">To stop a web app, you must specify the name and resource group of the web app.</span></span>

    Stop-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

#### <a name="start-a-web-app"></a><span data-ttu-id="41828-173">Uruchamiają aplikację sieci web</span><span class="sxs-lookup"><span data-stu-id="41828-173">Start a web app</span></span>
<span data-ttu-id="41828-174">Aby uruchomić aplikację sieci web, należy określić nazwę i zasobów Grupa aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="41828-174">To start a web app, you must specify the name and resource group of the web app.</span></span>

    Start-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

### <a name="manage-web-app-publishing-profiles"></a><span data-ttu-id="41828-175">Zarządzanie profilami publikowania aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="41828-175">Manage Web App Publishing profiles</span></span>
<span data-ttu-id="41828-176">Każda aplikacja sieci web ma profil publikowania, który może być używana do publikowania aplikacji, można wykonać kilka czynności dla profilów publikowania.</span><span class="sxs-lookup"><span data-stu-id="41828-176">Each web app has a publishing profile that can be used to publish your apps, several operations can be executed on publishing profiles.</span></span>

#### <a name="get-publishing-profile"></a><span data-ttu-id="41828-177">Pobierz publikowania profilu</span><span class="sxs-lookup"><span data-stu-id="41828-177">Get Publishing Profile</span></span>
<span data-ttu-id="41828-178">Aby pobrać profilu publikowania dla aplikacji sieci web, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="41828-178">To get the publishing profile for a web app, use:</span></span>

    Get-AzureRmWebAppPublishingProfile -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -OutputFile .\publishingprofile.txt

<span data-ttu-id="41828-179">To polecenie zwraca profilu publikowania do wiersza polecenia, jak również wyjściowych profilu publikowania do pliku tekstowego.</span><span class="sxs-lookup"><span data-stu-id="41828-179">This command echoes the publishing profile to the command line as well output the publishing profile to a text file.</span></span>

#### <a name="reset-publishing-profile"></a><span data-ttu-id="41828-180">Resetowanie profilu publikowania</span><span class="sxs-lookup"><span data-stu-id="41828-180">Reset Publishing Profile</span></span>
<span data-ttu-id="41828-181">Aby zresetować zarówno publikowania hasło dla sieci web i FTP wdrażania dla aplikacji sieci web, użyj:</span><span class="sxs-lookup"><span data-stu-id="41828-181">To reset both the publishing password for FTP and web deploy for a web app, use:</span></span>

    Reset-AzureRmWebAppPublishingProfile -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

### <a name="manage-web-app-certificates"></a><span data-ttu-id="41828-182">Zarządzanie certyfikatami aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="41828-182">Manage Web App Certificates</span></span>
<span data-ttu-id="41828-183">Aby dowiedzieć się więcej o zarządzaniu certyfikatów aplikacji sieci web, zobacz [powiązania certyfikatów SSL przy użyciu programu PowerShell](app-service-web-app-powershell-ssl-binding.md)</span><span class="sxs-lookup"><span data-stu-id="41828-183">To learn about how to manage web app certificates, see [SSL Certificates binding using PowerShell](app-service-web-app-powershell-ssl-binding.md)</span></span>

### <a name="next-steps"></a><span data-ttu-id="41828-184">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="41828-184">Next Steps</span></span>
* <span data-ttu-id="41828-185">Aby dowiedzieć się więcej o obsłudze programu PowerShell usługi Azure Resource Manager, zobacz [przy użyciu programu Azure PowerShell z usługą Azure Resource Manager.](../powershell-azure-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="41828-185">To learn about Azure Resource Manager PowerShell support, see [Using Azure PowerShell with Azure Resource Manager.](../powershell-azure-resource-manager.md)</span></span>
* <span data-ttu-id="41828-186">Aby dowiedzieć się więcej na temat środowiska usługi App Service, zobacz [wprowadzenie do środowiska usługi aplikacji.](app-service-app-service-environment-intro.md)</span><span class="sxs-lookup"><span data-stu-id="41828-186">To learn about App Service Environments, see [Introduction to App Service Environment.](app-service-app-service-environment-intro.md)</span></span>
* <span data-ttu-id="41828-187">Aby dowiedzieć się więcej o zarządzaniu certyfikatami SSL usługi aplikacji przy użyciu programu PowerShell, zobacz [powiązania certyfikatów SSL przy użyciu programu PowerShell.](app-service-web-app-powershell-ssl-binding.md)</span><span class="sxs-lookup"><span data-stu-id="41828-187">To learn about managing App Service SSL certificates using PowerShell, see [SSL Certificates binding using PowerShell.](app-service-web-app-powershell-ssl-binding.md)</span></span>
* <span data-ttu-id="41828-188">Aby zapoznać się z pełną listą poleceń cmdlet programu PowerShell usługi Azure Resource Manager na podstawie dla aplikacji sieci Web platformy Azure, zobacz [referencyjnej poleceń Cmdlet Azure poleceń cmdlet programu PowerShell Menedżera zasobów Azure aplikacje sieci Web.](https://msdn.microsoft.com/library/mt619237.aspx)</span><span class="sxs-lookup"><span data-stu-id="41828-188">To learn about the full list of Azure Resource Manager-based PowerShell cmdlets for Azure Web Apps, see [Azure Cmdlet Reference of Web Apps Azure Resource Manager PowerShell Cmdlets.](https://msdn.microsoft.com/library/mt619237.aspx)</span></span>
* * <span data-ttu-id="41828-189">Aby dowiedzieć się więcej o zarządzaniu App Service przy użyciu interfejsu wiersza polecenia, zobacz [wiersza polecenia XPlat Using Azure Resource Manager-Based dla aplikacji sieci Web platformy Azure.](app-service-web-app-azure-resource-manager-xplat-cli.md)</span><span class="sxs-lookup"><span data-stu-id="41828-189">To learn about managing App Service using CLI, see [Using Azure Resource Manager-Based XPlat CLI for Azure Web App.](app-service-web-app-azure-resource-manager-xplat-cli.md)</span></span>

