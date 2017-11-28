---
title: "polecenia aaaAzure PowerShell oparte na Menedżera zasobów dla aplikacji sieci Web platformy Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse hello nowe toomanage polecenia PowerShell usługi Azure Resource Manager na podstawie aplikacji sieci Web platformy Azure."
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
ms.openlocfilehash: bbb821e89daa315280436e84e11316217bb644d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-resource-manager-based-powershell-toomanage-azure-web-apps"></a><span data-ttu-id="b76fb-103">Przy użyciu programu PowerShell Azure Resource Manager-Based tooManage Azure Web Apps</span><span class="sxs-lookup"><span data-stu-id="b76fb-103">Using Azure Resource Manager-Based PowerShell tooManage Azure Web Apps</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b76fb-104">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="b76fb-104">Azure CLI</span></span>](app-service-web-app-azure-resource-manager-xplat-cli.md)
> * [<span data-ttu-id="b76fb-105">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b76fb-105">Azure PowerShell</span></span>](app-service-web-app-azure-resource-manager-powershell.md)
> 
> 

<span data-ttu-id="b76fb-106">Przy użyciu programu Microsoft Azure PowerShell w wersji 1.0.0 zostały dodane nowe polecenia, które powodują hello użytkownika hello możliwości toouse PowerShell usługi Azure Resource Manager na podstawie polecenia toomanage aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="b76fb-106">With Microsoft Azure PowerShell version 1.0.0 new commands have been added, that give hello user hello ability toouse Azure Resource Manager-based PowerShell commands toomanage Web Apps.</span></span>

<span data-ttu-id="b76fb-107">toolearn o zarządzaniu grupami zasobów, zobacz [przy użyciu programu Azure PowerShell z usługą Azure Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="b76fb-107">toolearn about managing Resource Groups, see [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span> 

<span data-ttu-id="b76fb-108">toolearn o hello pełną listę parametrów i opcje dotyczące hello poleceń cmdlet programu PowerShell, zobacz hello [pełne odwołania do polecenia Cmdlet oparte na sieci Web aplikacji usługi Azure Resource Manager poleceń cmdlet programu PowerShell](https://msdn.microsoft.com/library/mt619237.aspx)</span><span class="sxs-lookup"><span data-stu-id="b76fb-108">toolearn about hello full list of parameters and options for hello PowerShell cmdlets, see hello [full Cmdlet Reference of Web App Azure Resource Manager-based PowerShell Cmdlets](https://msdn.microsoft.com/library/mt619237.aspx)</span></span>

## <a name="managing-app-service-plans"></a><span data-ttu-id="b76fb-109">Plany zarządzania z usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="b76fb-109">Managing App Service Plans</span></span>
### <a name="create-an-app-service-plan"></a><span data-ttu-id="b76fb-110">Tworzenie planu usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="b76fb-110">Create an App Service Plan</span></span>
<span data-ttu-id="b76fb-111">toocreate plan usługi aplikacji, użyj hello **AzureRmAppServicePlan nowy** polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b76fb-111">toocreate an app service plan, use hello **New-AzureRmAppServicePlan** cmdlet.</span></span>

<span data-ttu-id="b76fb-112">Poniżej przedstawiono opisy różnych parametrów hello:</span><span class="sxs-lookup"><span data-stu-id="b76fb-112">Following are descriptions of hello different parameters:</span></span>

* <span data-ttu-id="b76fb-113">**Nazwa**: Nazwa planu usługi aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="b76fb-113">**Name**: name of hello app service plan.</span></span>
* <span data-ttu-id="b76fb-114">**Lokalizacja**: usługa lokalizacji planu.</span><span class="sxs-lookup"><span data-stu-id="b76fb-114">**Location**: service plan location.</span></span>
* <span data-ttu-id="b76fb-115">**ResourceGroupName**: grupy zasobów, która zawiera plan usługi aplikacji hello nowo utworzona.</span><span class="sxs-lookup"><span data-stu-id="b76fb-115">**ResourceGroupName**: resource group that includes hello newly created app service plan.</span></span>
* <span data-ttu-id="b76fb-116">**Warstwa**: hello żądaną warstwę cenową (domyślna to bezpłatna, inne opcje są współużytkowane, podstawowa, standardowa i Premium).</span><span class="sxs-lookup"><span data-stu-id="b76fb-116">**Tier**:  hello desired pricing tier (Default is Free, other options are Shared, Basic, Standard, and Premium.)</span></span>
* <span data-ttu-id="b76fb-117">**WorkerSize**: hello rozmiar pracowników (wartość domyślna to mały, jeśli określono parametr warstwy hello jako podstawowa, standardowa lub Premium.</span><span class="sxs-lookup"><span data-stu-id="b76fb-117">**WorkerSize**: hello size of workers (Default is small if hello Tier parameter was specified as Basic, Standard, or Premium.</span></span> <span data-ttu-id="b76fb-118">Inne opcje są średni i duży).</span><span class="sxs-lookup"><span data-stu-id="b76fb-118">Other options are Medium, and Large.)</span></span>
* <span data-ttu-id="b76fb-119">**NumberofWorkers**: hello liczbę procesów roboczych w planie usługi aplikacji hello (wartość domyślna to 1).</span><span class="sxs-lookup"><span data-stu-id="b76fb-119">**NumberofWorkers**: hello number of workers in hello app service plan (Default value is 1).</span></span> 

<span data-ttu-id="b76fb-120">Przykład toouse tego polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="b76fb-120">Example toouse this cmdlet:</span></span>

    New-AzureRmAppServicePlan -Name ContosoAppServicePlan -Location "South Central US" -ResourceGroupName ContosoAzureResourceGroup -Tier Premium -WorkerSize Large -NumberofWorkers 10

### <a name="create-an-app-service-plan-in-an-app-service-environment"></a><span data-ttu-id="b76fb-121">Tworzenie planu usługi aplikacji w środowisku usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="b76fb-121">Create an App Service Plan in an App Service Environment</span></span>
<span data-ttu-id="b76fb-122">toocreate planie usługi aplikacji w środowisku usługi aplikacji, użyj hello same polecenie **AzureRmAppServicePlan nowy** polecenia o nazwie dodatkowe parametry toospecify hello w ASE i nazwa grupy zasobów w ASE.</span><span class="sxs-lookup"><span data-stu-id="b76fb-122">toocreate an app service plan in an app service environment, use hello same command **New-AzureRmAppServicePlan** command with extra parameters toospecify hello ASE's name and ASE's resource group name.</span></span>

<span data-ttu-id="b76fb-123">Przykład toouse tego polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="b76fb-123">Example toouse this cmdlet:</span></span>

    New-AzureRmAppServicePlan -Name ContosoAppServicePlan -Location "South Central US" -ResourceGroupName ContosoAzureResourceGroup -AseName constosoASE -AseResourceGroupName contosoASERG -Tier Premium -WorkerSize Large -NumberofWorkers 10

<span data-ttu-id="b76fb-124">więcej informacji na temat środowiska usługi aplikacji, sprawdź toolearn [tooApp wprowadzenie środowiska usługi](app-service-app-service-environment-intro.md)</span><span class="sxs-lookup"><span data-stu-id="b76fb-124">toolearn more about app service environment, check [Introduction tooApp Service Environment](app-service-app-service-environment-intro.md)</span></span>

### <a name="list-existing-app-service-plans"></a><span data-ttu-id="b76fb-125">Lista istniejących planów usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="b76fb-125">List Existing App Service Plans</span></span>
<span data-ttu-id="b76fb-126">toolist hello istniejących planów usługi aplikacji, użyj **Get-AzureRmAppServicePlan** polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b76fb-126">toolist hello existing app service plans, use **Get-AzureRmAppServicePlan** cmdlet.</span></span>

<span data-ttu-id="b76fb-127">Użyj toolist wszystkich planów usługi aplikacji w ramach Twojej subskrypcji:</span><span class="sxs-lookup"><span data-stu-id="b76fb-127">toolist all app service plans under your subscription, use:</span></span> 

    Get-AzureRmAppServicePlan

<span data-ttu-id="b76fb-128">toolist wszystkich planów usługi aplikacji w obszarze określonej grupy zasobów, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="b76fb-128">toolist all app service plans under a specific resource group, use:</span></span>

    Get-AzureRmAppServicePlan -ResourceGroupname ContosoAzureResourceGroup

<span data-ttu-id="b76fb-129">Użyj tooget planu usługi specyficzne dla aplikacji:</span><span class="sxs-lookup"><span data-stu-id="b76fb-129">tooget a specific app service plan, use:</span></span>

    Get-AzureRmAppServicePlan -Name ContosoAppServicePlan


### <a name="configure-an-existing-app-service-plan"></a><span data-ttu-id="b76fb-130">Skonfiguruj istniejący Plan usługi App Service</span><span class="sxs-lookup"><span data-stu-id="b76fb-130">Configure an existing App Service Plan</span></span>
<span data-ttu-id="b76fb-131">toochange hello ustawień dla istniejącego planu usługi aplikacji, użyj hello **AzureRmAppServicePlan zestaw** polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b76fb-131">toochange hello settings for an existing app service plan, use hello **Set-AzureRmAppServicePlan** cmdlet.</span></span> <span data-ttu-id="b76fb-132">Można zmienić warstwy hello, rozmiar procesu roboczego i hello liczbę procesów roboczych</span><span class="sxs-lookup"><span data-stu-id="b76fb-132">You can change hello tier, worker size, and hello number of workers</span></span> 

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Tier Standard -WorkerSize Medium -NumberofWorkers 9

#### <a name="scaling-an-app-service-plan"></a><span data-ttu-id="b76fb-133">Skalowanie planu usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="b76fb-133">Scaling an App Service Plan</span></span>
<span data-ttu-id="b76fb-134">Użyj istniejącego planu usługi App Service, tooscale:</span><span class="sxs-lookup"><span data-stu-id="b76fb-134">tooscale an existing App Service Plan, use:</span></span>

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -NumberofWorkers 9

#### <a name="changing-hello-worker-size-of-an-app-service-plan"></a><span data-ttu-id="b76fb-135">Zmienianie rozmiaru procesu roboczego hello planu usługi App Service</span><span class="sxs-lookup"><span data-stu-id="b76fb-135">Changing hello worker size of an App Service Plan</span></span>
<span data-ttu-id="b76fb-136">rozmiar hello toochange pracowników w istniejący Plan usługi App Service, użyj:</span><span class="sxs-lookup"><span data-stu-id="b76fb-136">toochange hello size of workers in an existing App Service Plan, use:</span></span>

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -WorkerSize Medium

#### <a name="changing-hello-tier-of-an-app-service-plan"></a><span data-ttu-id="b76fb-137">Zmiana hello warstwy planu usługi App Service</span><span class="sxs-lookup"><span data-stu-id="b76fb-137">Changing hello Tier of an App Service Plan</span></span>
<span data-ttu-id="b76fb-138">warstwy hello toochange istniejący Plan usługi App Service, użyj:</span><span class="sxs-lookup"><span data-stu-id="b76fb-138">toochange hello tier of an existing App Service Plan, use:</span></span>

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Tier Standard

### <a name="delete-an-existing-app-service-plan"></a><span data-ttu-id="b76fb-139">Usuń istniejący Plan usługi App Service</span><span class="sxs-lookup"><span data-stu-id="b76fb-139">Delete an existing App Service Plan</span></span>
<span data-ttu-id="b76fb-140">toodelete istniejący plan usługi aplikacji, wszystkie przypisane toobe przeniesiony lub usunięty, najpierw należy aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="b76fb-140">toodelete an existing app service plan, all assigned web apps need toobe moved or deleted first.</span></span> <span data-ttu-id="b76fb-141">Przy użyciu hello **AzureRmAppServicePlan Usuń** polecenia cmdlet można usunąć planu usługi aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="b76fb-141">Then using hello **Remove-AzureRmAppServicePlan** cmdlet you can delete hello app service plan.</span></span>

    Remove-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup

## <a name="managing-app-service-web-apps"></a><span data-ttu-id="b76fb-142">Zarządzanie aplikacjami sieci Web usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="b76fb-142">Managing App Service Web Apps</span></span>
### <a name="create-a-web-app"></a><span data-ttu-id="b76fb-143">Tworzenie aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="b76fb-143">Create a Web App</span></span>
<span data-ttu-id="b76fb-144">toocreate aplikacji sieci web, użyj hello **AzureRmWebApp nowy** polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b76fb-144">toocreate a web app, use hello **New-AzureRmWebApp** cmdlet.</span></span>

<span data-ttu-id="b76fb-145">Poniżej przedstawiono opisy różnych parametrów hello:</span><span class="sxs-lookup"><span data-stu-id="b76fb-145">Following are descriptions of hello different parameters:</span></span>

* <span data-ttu-id="b76fb-146">**Nazwa**: Nazwa aplikacji sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="b76fb-146">**Name**: name for hello web app.</span></span>
* <span data-ttu-id="b76fb-147">**AppServicePlan**: nazwa dla hello planu usługi aplikacji sieci web hello toohost.</span><span class="sxs-lookup"><span data-stu-id="b76fb-147">**AppServicePlan**: name for hello service plan used toohost hello web app.</span></span>
* <span data-ttu-id="b76fb-148">**ResourceGroupName**: grupy zasobów, który jest hostem plan usługi aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="b76fb-148">**ResourceGroupName**: resource group that hosts hello App service plan.</span></span>
* <span data-ttu-id="b76fb-149">**Lokalizacja**: hello lokalizacji aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="b76fb-149">**Location**: hello web app location.</span></span>

<span data-ttu-id="b76fb-150">Przykład toouse tego polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="b76fb-150">Example toouse this cmdlet:</span></span>

    New-AzureRmWebApp -Name ContosoWebApp -AppServicePlan ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Location "South Central US"

### <a name="create-a-web-app-in-an-app-service-environment"></a><span data-ttu-id="b76fb-151">Tworzenie aplikacji sieci Web w środowisku usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="b76fb-151">Create a Web App in an App Service Environment</span></span>
<span data-ttu-id="b76fb-152">toocreate aplikacji sieci web w środowisku aplikacji (ASE).</span><span class="sxs-lookup"><span data-stu-id="b76fb-152">toocreate a web app in an App Service Environment (ASE).</span></span> <span data-ttu-id="b76fb-153">Użyj hello sam **AzureRmWebApp nowy** polecenia o nazwie hello ASE toospecify dodatkowe parametry i nazwa grupy zasobów hello hello ASE należącą do.</span><span class="sxs-lookup"><span data-stu-id="b76fb-153">Use hello same **New-AzureRmWebApp** command with extra parameters toospecify hello ASE name and hello resource group name that hello ASE belongs to.</span></span>

    New-AzureRmWebApp -Name ContosoWebApp -AppServicePlan ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Location "South Central US"  -ASEName ContosoASEName -ASEResourceGroupName ContosoASEResourceGroupName

<span data-ttu-id="b76fb-154">więcej informacji na temat środowiska usługi aplikacji, sprawdź toolearn [tooApp wprowadzenie środowiska usługi](app-service-app-service-environment-intro.md)</span><span class="sxs-lookup"><span data-stu-id="b76fb-154">toolearn more about app service environment, check [Introduction tooApp Service Environment](app-service-app-service-environment-intro.md)</span></span>

### <a name="delete-an-existing-web-app"></a><span data-ttu-id="b76fb-155">Usuń istniejącą aplikację sieci Web</span><span class="sxs-lookup"><span data-stu-id="b76fb-155">Delete an existing Web App</span></span>
<span data-ttu-id="b76fb-156">toodelete istniejącej aplikacji sieci web, można użyć hello **AzureRmWebApp Usuń** polecenia cmdlet, potrzebna nazwa hello toospecify hello aplikacji sieci web i nazwa grupy zasobów hello.</span><span class="sxs-lookup"><span data-stu-id="b76fb-156">toodelete an existing web app you can use hello **Remove-AzureRmWebApp** cmdlet, you need toospecify hello name of hello web app and hello resource group name.</span></span>

    Remove-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup


### <a name="list-existing-web-apps"></a><span data-ttu-id="b76fb-157">Listy istniejących aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="b76fb-157">List existing Web Apps</span></span>
<span data-ttu-id="b76fb-158">toolist hello istniejących aplikacji sieci web, użyj hello **Get-AzureRmWebApp** polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b76fb-158">toolist hello existing web apps, use hello **Get-AzureRmWebApp** cmdlet.</span></span>

<span data-ttu-id="b76fb-159">Użyj toolist wszystkie aplikacje sieci web w ramach Twojej subskrypcji:</span><span class="sxs-lookup"><span data-stu-id="b76fb-159">toolist all web apps under your subscription, use:</span></span>

    Get-AzureRmWebApp

<span data-ttu-id="b76fb-160">toolist wszystkie aplikacje sieci web w obszarze określonej grupy zasobów, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="b76fb-160">toolist all web apps under a specific resource group, use:</span></span>

    Get-AzureRmWebApp -ResourceGroupname ContosoAzureResourceGroup

<span data-ttu-id="b76fb-161">Użyj aplikacji sieci web określonego tooget:</span><span class="sxs-lookup"><span data-stu-id="b76fb-161">tooget a specific web app, use:</span></span>

    Get-AzureRmWebApp -Name ContosoWebApp

### <a name="configure-an-existing-web-app"></a><span data-ttu-id="b76fb-162">Konfigurowanie istniejącej aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="b76fb-162">Configure an existing Web App</span></span>
<span data-ttu-id="b76fb-163">toochange hello ustawienia i konfiguracje dla istniejącej aplikacji sieci web, użyj hello **AzureRmWebApp zestaw** polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b76fb-163">toochange hello settings and configurations for an existing web app, use hello **Set-AzureRmWebApp** cmdlet.</span></span> <span data-ttu-id="b76fb-164">Aby uzyskać pełną listę parametrów, sprawdź hello [polecenia Cmdlet opis łącza](https://msdn.microsoft.com/library/mt652487.aspx)</span><span class="sxs-lookup"><span data-stu-id="b76fb-164">For a full list of parameters, check hello [Cmdlet reference link](https://msdn.microsoft.com/library/mt652487.aspx)</span></span>

<span data-ttu-id="b76fb-165">Przykład (1): Użyj parametrów połączenia toochange tego polecenia cmdlet</span><span class="sxs-lookup"><span data-stu-id="b76fb-165">Example (1): use this cmdlet toochange connection strings</span></span>

    $connectionstrings = @{ ContosoConn1 = @{ Type = “MySql”; Value = “MySqlConn”}; ContosoConn2 = @{ Type = “SQLAzure”; Value = “SQLAzureConn”} }
    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -ConnectionStrings $connectionstrings

<span data-ttu-id="b76fb-166">Przykład (2): Dodawanie lub zmienianie ustawień aplikacji</span><span class="sxs-lookup"><span data-stu-id="b76fb-166">Example (2): add or change app settings</span></span>

    $appsettings = @{appsetting1 = "appsetting1value"; appsetting2 = "appsetting2value"}
    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -AppSettings $appsettings


<span data-ttu-id="b76fb-167">Przykład (3): Ustaw toorun aplikacji sieci web hello w trybie 64-bitowym</span><span class="sxs-lookup"><span data-stu-id="b76fb-167">Example (3):  set hello web app toorun in 64-bit mode</span></span>

    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -Use32BitWorkerProcess $False

### <a name="change-hello-state-of-an-existing-web-app"></a><span data-ttu-id="b76fb-168">Zmiana stanu hello istniejącej aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="b76fb-168">Change hello state of an existing Web App</span></span>
#### <a name="restart-a-web-app"></a><span data-ttu-id="b76fb-169">Ponowne uruchomienie aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="b76fb-169">Restart a web app</span></span>
<span data-ttu-id="b76fb-170">toorestart aplikacji sieci web, należy określić nazwę i zasobów grupę hello hello aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="b76fb-170">toorestart a web app, you must specify hello name and resource group of hello web app.</span></span>

    Restart-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

#### <a name="stop-a-web-app"></a><span data-ttu-id="b76fb-171">Zatrzymać aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="b76fb-171">Stop a web app</span></span>
<span data-ttu-id="b76fb-172">toostop aplikacji sieci web, należy określić nazwę i zasobów grupę hello hello aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="b76fb-172">toostop a web app, you must specify hello name and resource group of hello web app.</span></span>

    Stop-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

#### <a name="start-a-web-app"></a><span data-ttu-id="b76fb-173">Uruchamiają aplikację sieci web</span><span class="sxs-lookup"><span data-stu-id="b76fb-173">Start a web app</span></span>
<span data-ttu-id="b76fb-174">toostart aplikacji sieci web, należy określić nazwę i zasobów grupę hello hello aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="b76fb-174">toostart a web app, you must specify hello name and resource group of hello web app.</span></span>

    Start-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

### <a name="manage-web-app-publishing-profiles"></a><span data-ttu-id="b76fb-175">Zarządzanie profilami publikowania aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="b76fb-175">Manage Web App Publishing profiles</span></span>
<span data-ttu-id="b76fb-176">Każda aplikacja sieci web ma profil publikowania, które mogą być używane toopublish aplikacji, można wykonać kilka czynności dla profilów publikowania.</span><span class="sxs-lookup"><span data-stu-id="b76fb-176">Each web app has a publishing profile that can be used toopublish your apps, several operations can be executed on publishing profiles.</span></span>

#### <a name="get-publishing-profile"></a><span data-ttu-id="b76fb-177">Pobierz publikowania profilu</span><span class="sxs-lookup"><span data-stu-id="b76fb-177">Get Publishing Profile</span></span>
<span data-ttu-id="b76fb-178">Publikowanie aplikacji sieci web, Użyj profilu hello tooget:</span><span class="sxs-lookup"><span data-stu-id="b76fb-178">tooget hello publishing profile for a web app, use:</span></span>

    Get-AzureRmWebAppPublishingProfile -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -OutputFile .\publishingprofile.txt

<span data-ttu-id="b76fb-179">To polecenie informujące, że hello również wiersza polecenia toohello profilu publikowania danych wyjściowych hello pliku tekstowego tooa profilu publikowania.</span><span class="sxs-lookup"><span data-stu-id="b76fb-179">This command echoes hello publishing profile toohello command line as well output hello publishing profile tooa text file.</span></span>

#### <a name="reset-publishing-profile"></a><span data-ttu-id="b76fb-180">Resetowanie profilu publikowania</span><span class="sxs-lookup"><span data-stu-id="b76fb-180">Reset Publishing Profile</span></span>
<span data-ttu-id="b76fb-181">tooreset zarówno hello publikowania hasło, dla sieci web i FTP, wdrożenia dla aplikacji sieci web, użyj:</span><span class="sxs-lookup"><span data-stu-id="b76fb-181">tooreset both hello publishing password for FTP and web deploy for a web app, use:</span></span>

    Reset-AzureRmWebAppPublishingProfile -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

### <a name="manage-web-app-certificates"></a><span data-ttu-id="b76fb-182">Zarządzanie certyfikatami aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="b76fb-182">Manage Web App Certificates</span></span>
<span data-ttu-id="b76fb-183">Zobacz toolearn o jak certyfikatów aplikacji sieci web na toomanage [powiązania certyfikatów SSL przy użyciu programu PowerShell](app-service-web-app-powershell-ssl-binding.md)</span><span class="sxs-lookup"><span data-stu-id="b76fb-183">toolearn about how toomanage web app certificates, see [SSL Certificates binding using PowerShell](app-service-web-app-powershell-ssl-binding.md)</span></span>

### <a name="next-steps"></a><span data-ttu-id="b76fb-184">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b76fb-184">Next Steps</span></span>
* <span data-ttu-id="b76fb-185">toolearn o obsłudze programu PowerShell usługi Azure Resource Manager, zobacz [przy użyciu programu Azure PowerShell z usługą Azure Resource Manager.](../powershell-azure-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="b76fb-185">toolearn about Azure Resource Manager PowerShell support, see [Using Azure PowerShell with Azure Resource Manager.](../powershell-azure-resource-manager.md)</span></span>
* <span data-ttu-id="b76fb-186">toolearn o środowiska usługi App Service, zobacz [tooApp wprowadzenie środowiska usługi.](app-service-app-service-environment-intro.md)</span><span class="sxs-lookup"><span data-stu-id="b76fb-186">toolearn about App Service Environments, see [Introduction tooApp Service Environment.](app-service-app-service-environment-intro.md)</span></span>
* <span data-ttu-id="b76fb-187">toolearn o zarządzaniu certyfikatami SSL usługi aplikacji przy użyciu programu PowerShell, zobacz [powiązania certyfikatów SSL przy użyciu programu PowerShell.](app-service-web-app-powershell-ssl-binding.md)</span><span class="sxs-lookup"><span data-stu-id="b76fb-187">toolearn about managing App Service SSL certificates using PowerShell, see [SSL Certificates binding using PowerShell.](app-service-web-app-powershell-ssl-binding.md)</span></span>
* <span data-ttu-id="b76fb-188">toolearn o hello pełną listę na podstawie usługi Azure Resource Manager poleceń cmdlet programu PowerShell dla aplikacji sieci Web platformy Azure, zobacz [referencyjnej poleceń Cmdlet Azure poleceń cmdlet programu PowerShell Menedżera zasobów Azure aplikacje sieci Web.](https://msdn.microsoft.com/library/mt619237.aspx)</span><span class="sxs-lookup"><span data-stu-id="b76fb-188">toolearn about hello full list of Azure Resource Manager-based PowerShell cmdlets for Azure Web Apps, see [Azure Cmdlet Reference of Web Apps Azure Resource Manager PowerShell Cmdlets.](https://msdn.microsoft.com/library/mt619237.aspx)</span></span>
* * <span data-ttu-id="b76fb-189">toolearn o zarządzaniu App Service przy użyciu interfejsu wiersza polecenia, zobacz [wiersza polecenia XPlat Using Azure Resource Manager-Based dla aplikacji sieci Web platformy Azure.](app-service-web-app-azure-resource-manager-xplat-cli.md)</span><span class="sxs-lookup"><span data-stu-id="b76fb-189">toolearn about managing App Service using CLI, see [Using Azure Resource Manager-Based XPlat CLI for Azure Web App.](app-service-web-app-azure-resource-manager-xplat-cli.md)</span></span>

