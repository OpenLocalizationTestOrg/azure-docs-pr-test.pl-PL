---
title: "aaaAzure narzędzi wiersza polecenia Menedżera zasobów na podstawie między platformami dla aplikacji sieci Web platformy Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse hello nowe toomanage opartej na usłudze Azure Resource Manager narzędzi wiersza polecenia i platform aplikacji sieci Web platformy Azure."
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: d415b195-4262-416f-b59f-7e1aef200054
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/29/2016
ms.author: aelnably
ms.openlocfilehash: 5f5e03edcb01154aef3bd220cd27358f69656ef4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-resource-manager-based-xplat-cli-for-azure-app-service"></a><span data-ttu-id="e3431-103">Przy użyciu wiersza polecenia XPlat na podstawie Menedżera zasobów Azure dla usługi aplikacji Azure</span><span class="sxs-lookup"><span data-stu-id="e3431-103">Using Azure Resource Manager-Based XPlat CLI for Azure App Service</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e3431-104">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="e3431-104">Azure CLI</span></span>](app-service-web-app-azure-resource-manager-xplat-cli.md)
> * [<span data-ttu-id="e3431-105">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="e3431-105">Azure PowerShell</span></span>](app-service-web-app-azure-resource-manager-powershell.md)

<span data-ttu-id="e3431-106">Hello wydanej wersji narzędzi wiersza polecenia usługi Microsoft Azure i platform 0.10.5 zostały dodane nowe polecenia.</span><span class="sxs-lookup"><span data-stu-id="e3431-106">With hello release of Microsoft Azure Cross-platform Command-Line Tools version 0.10.5, new commands have been added.</span></span> <span data-ttu-id="e3431-107">Te polecenia nadaj hello użytkownika hello możliwości toouse PowerShell usługi Azure Resource Manager na podstawie polecenia toomanage usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e3431-107">These commands give hello user hello ability toouse Azure Resource Manager-based PowerShell commands toomanage App Service.</span></span>

<span data-ttu-id="e3431-108">toolearn o zarządzaniu grupami zasobów, zobacz [Użyj toomanage interfejsu wiersza polecenia Azure hello Azure zasobów i grup zasobów](../azure-resource-manager/xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="e3431-108">toolearn about managing Resource Groups, see [Use hello Azure CLI toomanage Azure resources and resource groups](../azure-resource-manager/xplat-cli-azure-resource-manager.md).</span></span> 

> [!NOTE] 
> <span data-ttu-id="e3431-109">Ponadto wypróbowanie [Azure CLI 2.0](https://github.com/Azure/azure-cli), napisany w języku Python dla modelu wdrażania zarządzania zasobów hello infrastruktury CLI nowej generacji.</span><span class="sxs-lookup"><span data-stu-id="e3431-109">Also, try out [Azure CLI 2.0](https://github.com/Azure/azure-cli), a next-generation CLI written in Python for hello resource management deployment model.</span></span>
>
>

## <a name="managing-app-service-plans"></a><span data-ttu-id="e3431-110">Plany zarządzania z usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="e3431-110">Managing App Service Plans</span></span>
### <a name="create-an-app-service-plan"></a><span data-ttu-id="e3431-111">Tworzenie planu usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="e3431-111">Create an App Service Plan</span></span>
<span data-ttu-id="e3431-112">toocreate plan usługi aplikacji, użyj hello **utworzyć azure appserviceplan** polecenia.</span><span class="sxs-lookup"><span data-stu-id="e3431-112">toocreate an app service plan, use hello **azure appserviceplan create** command.</span></span>

<span data-ttu-id="e3431-113">Poniżej przedstawiono opisy różnych parametrów hello:</span><span class="sxs-lookup"><span data-stu-id="e3431-113">Following are descriptions of hello different parameters:</span></span>

* <span data-ttu-id="e3431-114">**--grupy zasobów**: grupy zasobów, która zawiera plan usługi aplikacji hello nowo utworzona.</span><span class="sxs-lookup"><span data-stu-id="e3431-114">**--resource-group**: resource group that includes hello newly created app service plan.</span></span>
* <span data-ttu-id="e3431-115">**--name**: Nazwa planu usługi aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="e3431-115">**--name**: name of hello app service plan.</span></span>
* <span data-ttu-id="e3431-116">**--lokalizacji**: Lokalizacja planu usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e3431-116">**--location**: app service plan location.</span></span>
* <span data-ttu-id="e3431-117">**Jednostka sku —**: hello potrzeby cenową jednostki sku (Opcje hello są: F1 (bezpłatnie).</span><span class="sxs-lookup"><span data-stu-id="e3431-117">**--sku**:  hello desired pricing sku (hello options are: F1 (Free).</span></span> <span data-ttu-id="e3431-118">D1 (wspólna).</span><span class="sxs-lookup"><span data-stu-id="e3431-118">D1 (Shared).</span></span> <span data-ttu-id="e3431-119">B1 (podstawowe mała liczba godzin), B2 (podstawowa średnia liczba godzin) i B3 (Basic duże).</span><span class="sxs-lookup"><span data-stu-id="e3431-119">B1 (Basic Small), B2 (Basic Medium), and B3 (Basic Large).</span></span> <span data-ttu-id="e3431-120">S1 (standardowa mała liczba godzin), S2 (standardowa średnia liczba godzin) i S3 (Standard duże).</span><span class="sxs-lookup"><span data-stu-id="e3431-120">S1 (Standard Small), S2 (Standard Medium), and S3 (Standard Large).</span></span> <span data-ttu-id="e3431-121">P1 (mały Premium), P2 (średnia Premium), a P3 (duże Premium).)</span><span class="sxs-lookup"><span data-stu-id="e3431-121">P1 (Premium Small), P2 (Premium Medium), and P3 (Premium Large).)</span></span>
* <span data-ttu-id="e3431-122">**--wystąpień**: hello liczbę procesów roboczych w planie usługi aplikacji hello (wartość domyślna to 1).</span><span class="sxs-lookup"><span data-stu-id="e3431-122">**--instances**: hello number of workers in hello app service plan (Default value is 1).</span></span>

<span data-ttu-id="e3431-123">Przykład toouse tego polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="e3431-123">Example toouse this cmdlet:</span></span>

    azure appserviceplan create --name ContosoAppServicePlan --location "South Central US" --resource-group ContosoAzureResourceGroup --sku P1 --instances 10

#### <a name="create-a-linux-app-service-plan"></a><span data-ttu-id="e3431-124">Tworzenie planu usługi aplikacji w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="e3431-124">Create a Linux App Service Plan</span></span>

<span data-ttu-id="e3431-125">Przy użyciu hello sam **utworzyć azure appserviceplan** polecenia z hello dodatkowy parametr **true islinux —**.</span><span class="sxs-lookup"><span data-stu-id="e3431-125">Using hello same **azure appserviceplan create** command, with hello extra parameter **--islinux true**.</span></span> <span data-ttu-id="e3431-126">Zanotuj hello ograniczenia i regiony opisane w [tooApp wprowadzenie usługi w systemie Linux](app-service-linux-intro.md)</span><span class="sxs-lookup"><span data-stu-id="e3431-126">Note hello restrictions and regions outlined in [Introduction tooApp Service on Linux](app-service-linux-intro.md)</span></span>

### <a name="list-existing-app-service-plans"></a><span data-ttu-id="e3431-127">Lista istniejących planów usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="e3431-127">List Existing App Service Plans</span></span>
<span data-ttu-id="e3431-128">toolist hello istniejących planów usługi aplikacji, użyj **listy azure appserviceplan** polecenia.</span><span class="sxs-lookup"><span data-stu-id="e3431-128">toolist hello existing app service plans, use **azure appserviceplan list** command.</span></span>

<span data-ttu-id="e3431-129">toolist wszystkich planów usługi aplikacji w obszarze określonej grupy zasobów, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="e3431-129">toolist all app service plans under a specific resource group, use:</span></span>

    azure appserviceplan list --resource-group ContosoAzureResourceGroup

<span data-ttu-id="e3431-130">Użyj tooget planu usługi aplikacji określonych **Pokaż azure appserviceplan** polecenia:</span><span class="sxs-lookup"><span data-stu-id="e3431-130">tooget a specific app service plan, use **azure appserviceplan show** command:</span></span>

    azure appserviceplan show --name ContosoAppServicePlan --resource-group southeastasia

### <a name="configure-an-existing-app-service-plan"></a><span data-ttu-id="e3431-131">Skonfiguruj istniejący Plan usługi App Service</span><span class="sxs-lookup"><span data-stu-id="e3431-131">Configure an existing App Service Plan</span></span>
<span data-ttu-id="e3431-132">toochange hello ustawień dla istniejącego planu usługi aplikacji, użyj hello **azure appserviceplan config** polecenia.</span><span class="sxs-lookup"><span data-stu-id="e3431-132">toochange hello settings for an existing app service plan, use hello **azure appserviceplan config** command.</span></span> <span data-ttu-id="e3431-133">Możesz zmienić hello jednostki sku i hello liczbę procesów roboczych</span><span class="sxs-lookup"><span data-stu-id="e3431-133">You can change hello sku, and hello number of workers</span></span> 

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --sku S1 --instances 9

#### <a name="scaling-an-app-service-plan"></a><span data-ttu-id="e3431-134">Skalowanie planu usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="e3431-134">Scaling an App Service Plan</span></span>
<span data-ttu-id="e3431-135">Użyj istniejącego planu usługi App Service, tooscale:</span><span class="sxs-lookup"><span data-stu-id="e3431-135">tooscale an existing App Service Plan, use:</span></span>

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --instances 9

#### <a name="changing-hello-sku-of-an-app-service-plan"></a><span data-ttu-id="e3431-136">Zmiana hello jednostki SKU planu usługi App Service</span><span class="sxs-lookup"><span data-stu-id="e3431-136">Changing hello SKU of an App Service Plan</span></span>
<span data-ttu-id="e3431-137">numer hello toochange istniejący Plan usługi App Service, użyj:</span><span class="sxs-lookup"><span data-stu-id="e3431-137">toochange hello sku of an existing App Service Plan, use:</span></span>

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --sku S1


### <a name="delete-an-existing-app-service-plan"></a><span data-ttu-id="e3431-138">Usuń istniejący Plan usługi App Service</span><span class="sxs-lookup"><span data-stu-id="e3431-138">Delete an existing App Service Plan</span></span>
<span data-ttu-id="e3431-139">toodelete istniejący plan usługi aplikacji, wszystkie przypisane aplikacje muszą toobe przeniesiono lub usunięto najpierw.</span><span class="sxs-lookup"><span data-stu-id="e3431-139">toodelete an existing app service plan, all assigned apps need toobe moved or deleted first.</span></span> <span data-ttu-id="e3431-140">Przy użyciu hello **usunąć aplikacji sieci Web azure** polecenia, można usunąć planu usługi aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="e3431-140">Then using hello **azure webapp delete** command you can delete hello app service plan.</span></span>

    azure appserviceplan delete --name ContosoAppServicePlan --resource-group southeastasia

## <a name="managing-app-service-apps"></a><span data-ttu-id="e3431-141">Zarządzanie aplikacjami usługi App Service</span><span class="sxs-lookup"><span data-stu-id="e3431-141">Managing App Service apps</span></span>
### <a name="create-a-web-app"></a><span data-ttu-id="e3431-142">Tworzenie aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="e3431-142">Create a web app</span></span>
<span data-ttu-id="e3431-143">toocreate aplikacji sieci web, użyj hello **tworzenie aplikacji sieci Web azure** polecenia.</span><span class="sxs-lookup"><span data-stu-id="e3431-143">toocreate a web app, use hello **azure webapp create** command.</span></span>

<span data-ttu-id="e3431-144">Poniżej przedstawiono opisy różnych parametrów hello:</span><span class="sxs-lookup"><span data-stu-id="e3431-144">Following are descriptions of hello different parameters:</span></span>

* <span data-ttu-id="e3431-145">**--name**: Nazwa aplikacji sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="e3431-145">**--name**: name for hello web app.</span></span>
* <span data-ttu-id="e3431-146">**--planu**: nazwa dla hello planu usługi aplikacji sieci web hello toohost.</span><span class="sxs-lookup"><span data-stu-id="e3431-146">**--plan**: name for hello service plan used toohost hello web app.</span></span>
* <span data-ttu-id="e3431-147">**--grupy zasobów**: grupy zasobów, który jest hostem plan usługi aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="e3431-147">**--resource-group**: resource group that hosts hello App service plan.</span></span>
* <span data-ttu-id="e3431-148">**--lokalizacji**: hello lokalizacji aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="e3431-148">**--location**: hello web app location.</span></span>

<span data-ttu-id="e3431-149">Przykład toouse tego polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="e3431-149">Example toouse this cmdlet:</span></span>

    azure webapp create --name ContosoWebApp --resource-group ContosoAzureResourceGroup --plan ContosoAppServicePlan --location "South Central US"

### <a name="delete-an-existing-app"></a><span data-ttu-id="e3431-150">Usuń istniejącą aplikację</span><span class="sxs-lookup"><span data-stu-id="e3431-150">Delete an existing app</span></span>
<span data-ttu-id="e3431-151">toodelete istniejącej aplikacji, można użyć hello **usunąć aplikacji sieci Web azure** polecenia.</span><span class="sxs-lookup"><span data-stu-id="e3431-151">toodelete an existing app, you can use hello **azure webapp delete** command.</span></span> <span data-ttu-id="e3431-152">Należy toospecify hello nazwę aplikacji hello oraz nazwę grupy zasobów hello.</span><span class="sxs-lookup"><span data-stu-id="e3431-152">You need toospecify hello name of hello app and hello resource group name.</span></span>

    azure webapp delete --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="list-existing-apps"></a><span data-ttu-id="e3431-153">Listy istniejących aplikacji</span><span class="sxs-lookup"><span data-stu-id="e3431-153">List existing apps</span></span>
<span data-ttu-id="e3431-154">toolist hello istniejących aplikacji, użyj hello **listy aplikacji sieci Web azure** polecenia.</span><span class="sxs-lookup"><span data-stu-id="e3431-154">toolist hello existing apps, use hello **azure webapp list** command.</span></span>

<span data-ttu-id="e3431-155">toolist wszystkie aplikacje w określonej grupy zasobów, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="e3431-155">toolist all apps in a specific resource group, use:</span></span>

    azure webapp list --resource-group ContosoAzureResourceGroup

<span data-ttu-id="e3431-156">tooget określonej aplikacji, użyj hello **Pokaż aplikacji sieci Web azure** polecenia.</span><span class="sxs-lookup"><span data-stu-id="e3431-156">tooget a specific app, use hello **azure webapp show** command.</span></span>

    azure webapp show --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="configure-an-existing-app"></a><span data-ttu-id="e3431-157">Konfigurowanie istniejącej aplikacji</span><span class="sxs-lookup"><span data-stu-id="e3431-157">Configure an existing app</span></span>
<span data-ttu-id="e3431-158">toochange hello ustawienia i konfiguracje dla istniejącej aplikacji, użyj hello **aplikacji sieci Web azure config set** polecenia.</span><span class="sxs-lookup"><span data-stu-id="e3431-158">toochange hello settings and configurations for an existing app, use hello **azure webapp config set** command.</span></span>

<span data-ttu-id="e3431-159">Przykład (1): Zmień wersję php hello aplikacji</span><span class="sxs-lookup"><span data-stu-id="e3431-159">Example (1): change hello php version of a app</span></span> 

    azure webapp config set --name ContosoWebApp --resource-group ContosoAzureResourceGroup --phpversion 5.6

<span data-ttu-id="e3431-160">Przykład (2): Dodawanie lub zmienianie ustawień aplikacji</span><span class="sxs-lookup"><span data-stu-id="e3431-160">Example (2): add or change app settings</span></span>

    webapp config appsettings set --name ContosoWebApp --resource-group ContosoAzureResourceGroup appsetting1=appsetting1value,appsetting2=appsetting2value

<span data-ttu-id="e3431-161">tooknow, jakie inne konfigurację można zmienić, użyj hello **konfiguracji aplikacji sieci Web azure wartości -h** polecenia.</span><span class="sxs-lookup"><span data-stu-id="e3431-161">tooknow what other configuration can be changed, use hello **azure webapp config set -h** command.</span></span>

### <a name="change-hello-state-of-an-existing-app"></a><span data-ttu-id="e3431-162">Zmiana stanu hello istniejącej aplikacji</span><span class="sxs-lookup"><span data-stu-id="e3431-162">Change hello state of an existing app</span></span>
#### <a name="restart-an-app"></a><span data-ttu-id="e3431-163">Uruchom ponownie aplikację</span><span class="sxs-lookup"><span data-stu-id="e3431-163">Restart an app</span></span>
<span data-ttu-id="e3431-164">toorestart usługi aplikacji, należy określić nazwę i zasobów grupę hello aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="e3431-164">toorestart an app, you must specify hello name and resource group of hello app.</span></span>

    azure webapp restart --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="stop-an-app"></a><span data-ttu-id="e3431-165">Zatrzymaj aplikację</span><span class="sxs-lookup"><span data-stu-id="e3431-165">Stop an app</span></span>
<span data-ttu-id="e3431-166">toostop usługi aplikacji, należy określić nazwę i zasobów grupę hello aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="e3431-166">toostop an app, you must specify hello name and resource group of hello app.</span></span>

    azure webapp stop --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="start-an-app"></a><span data-ttu-id="e3431-167">Uruchamiają aplikację</span><span class="sxs-lookup"><span data-stu-id="e3431-167">Start an app</span></span>
<span data-ttu-id="e3431-168">toostart usługi aplikacji, należy określić nazwę i zasobów grupę hello aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="e3431-168">toostart an app, you must specify hello name and resource group of hello app.</span></span>

    azure webapp start --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="manage-publishing-profiles-of-an-app"></a><span data-ttu-id="e3431-169">Zarządzanie profilami publikowania aplikacji</span><span class="sxs-lookup"><span data-stu-id="e3431-169">Manage publishing profiles of an app</span></span>
<span data-ttu-id="e3431-170">Każda aplikacja ma profil publikowania, które mogą być używane toopublish kodu.</span><span class="sxs-lookup"><span data-stu-id="e3431-170">Each app has a publishing profile that can be used toopublish your code.</span></span>

#### <a name="get-publishing-profile"></a><span data-ttu-id="e3431-171">Pobierz publikowania profilu</span><span class="sxs-lookup"><span data-stu-id="e3431-171">Get Publishing Profile</span></span>
<span data-ttu-id="e3431-172">Publikowanie aplikacji, Użyj profilu hello tooget:</span><span class="sxs-lookup"><span data-stu-id="e3431-172">tooget hello publishing profile for a app, use:</span></span>

    azure webapp publishingprofile --name ContosoWebApp --resource-group ContosoAzureResourceGroup

<span data-ttu-id="e3431-173">To polecenie zwraca hello publikowania profilu użytkownika i hasło toohello wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="e3431-173">This command echoes hello publishing profile username and password toohello command line.</span></span>

### <a name="manage-app-hostnames"></a><span data-ttu-id="e3431-174">Zarządzanie nazwy hostów aplikacji</span><span class="sxs-lookup"><span data-stu-id="e3431-174">Manage app hostnames</span></span>
<span data-ttu-id="e3431-175">toomanage powiązań z nazwami hostów dla aplikacji, użyj hello **hostnames konfiguracji aplikacji sieci Web azure** polecenia</span><span class="sxs-lookup"><span data-stu-id="e3431-175">toomanage hostname bindings for your app, use hello **azure webapp config hostnames** command</span></span>  

#### <a name="list-hostname-bindings"></a><span data-ttu-id="e3431-176">Lista powiązań z nazwami hostów</span><span class="sxs-lookup"><span data-stu-id="e3431-176">List hostname bindings</span></span>
<span data-ttu-id="e3431-177">tooget hello bieżącego powiązań z nazwami hostów dla aplikacji, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="e3431-177">tooget hello current hostname bindings for an app, use:</span></span>

    azure webapp config hostnames list --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="add-hostname-bindings"></a><span data-ttu-id="e3431-178">Dodawanie powiązań z nazwami hostów</span><span class="sxs-lookup"><span data-stu-id="e3431-178">Add hostname bindings</span></span>
<span data-ttu-id="e3431-179">tooadd hostname powiązania tooan aplikacji, użyj:</span><span class="sxs-lookup"><span data-stu-id="e3431-179">tooadd hostname bindings tooan app, use:</span></span>

    azure webapp config hostnames add --name ContosoWebApp --resource-group ContosoAzureResourceGroup --hostname www.contoso.com

#### <a name="delete-hostname-bindings"></a><span data-ttu-id="e3431-180">Usuń powiązań z nazwami hostów</span><span class="sxs-lookup"><span data-stu-id="e3431-180">Delete hostname bindings</span></span>
<span data-ttu-id="e3431-181">toodelete powiązań z nazwami hostów, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="e3431-181">toodelete hostname bindings, use:</span></span>

    azure webapp config hostnames delete --name ContosoWebApp --resource-group ContosoAzureResourceGroup --hostname www.contoso.com

## <a name="next-steps"></a><span data-ttu-id="e3431-182">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e3431-182">Next Steps</span></span>
* <span data-ttu-id="e3431-183">toolearn dotyczące obsługi interfejsu wiersza polecenia Menedżera zasobów Azure, zobacz [Użyj toomanage interfejsu wiersza polecenia Azure hello Azure zasobów i grup zasobów.](../azure-resource-manager/xplat-cli-azure-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="e3431-183">toolearn about Azure Resource Manager CLI support, see [Use hello Azure CLI toomanage Azure resources and resource groups.](../azure-resource-manager/xplat-cli-azure-resource-manager.md)</span></span>
* <span data-ttu-id="e3431-184">toolearn o zarządzaniu App Service przy użyciu programu PowerShell, zobacz [tooManage Using Azure Resource Manager-Based programu PowerShell Azure Web Apps.](app-service-web-app-azure-resource-manager-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="e3431-184">toolearn about managing App Service using PowerShell, see [Using Azure Resource Manager-Based PowerShell tooManage Azure Web Apps.](app-service-web-app-azure-resource-manager-powershell.md)</span></span>
* <span data-ttu-id="e3431-185">toolearn o usłudze Azure App Service w systemie Linux, zobacz [tooApp wprowadzenie usługi w systemie Linux](app-service-linux-intro.md)</span><span class="sxs-lookup"><span data-stu-id="e3431-185">toolearn about Azure App Service on Linux, see [Introduction tooApp Service on Linux](app-service-linux-intro.md)</span></span>
