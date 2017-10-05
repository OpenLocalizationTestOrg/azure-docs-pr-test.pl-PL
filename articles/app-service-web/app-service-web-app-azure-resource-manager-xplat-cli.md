---
title: "Aplikacja sieci Web narzędzia Azure wiersza polecenia i platform opartych na Menedżera zasobów Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak użycie nowych narzędzi wiersza polecenia na podstawie usługi Azure Resource Manager i platform do zarządzania aplikacjami sieci Web platformy Azure."
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
ms.openlocfilehash: 7a03e1417617453c43edcc3787da10d171359757
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="using-azure-resource-manager-based-xplat-cli-for-azure-app-service"></a><span data-ttu-id="d1e5e-103">Przy użyciu wiersza polecenia XPlat na podstawie Menedżera zasobów Azure dla usługi aplikacji Azure</span><span class="sxs-lookup"><span data-stu-id="d1e5e-103">Using Azure Resource Manager-Based XPlat CLI for Azure App Service</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d1e5e-104">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="d1e5e-104">Azure CLI</span></span>](app-service-web-app-azure-resource-manager-xplat-cli.md)
> * [<span data-ttu-id="d1e5e-105">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="d1e5e-105">Azure PowerShell</span></span>](app-service-web-app-azure-resource-manager-powershell.md)

<span data-ttu-id="d1e5e-106">Wraz z wydaniem wersji narzędzi wiersza polecenia usługi Microsoft Azure i platform 0.10.5 zostały dodane nowe polecenia.</span><span class="sxs-lookup"><span data-stu-id="d1e5e-106">With the release of Microsoft Azure Cross-platform Command-Line Tools version 0.10.5, new commands have been added.</span></span> <span data-ttu-id="d1e5e-107">Tych poleceń przyznać użytkownikowi możliwość używania poleceń programu PowerShell z systemem Azure Resource Manager do zarządzania z usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d1e5e-107">These commands give the user the ability to use Azure Resource Manager-based PowerShell commands to manage App Service.</span></span>

<span data-ttu-id="d1e5e-108">Aby dowiedzieć się więcej o zarządzaniu grupami zasobów, zobacz [użyć wiersza polecenia platformy Azure do zarządzania zasobami Azure i grup zasobów](../azure-resource-manager/xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="d1e5e-108">To learn about managing Resource Groups, see [Use the Azure CLI to manage Azure resources and resource groups](../azure-resource-manager/xplat-cli-azure-resource-manager.md).</span></span> 

> [!NOTE] 
> <span data-ttu-id="d1e5e-109">Ponadto wypróbowanie [Azure CLI 2.0](https://github.com/Azure/azure-cli), napisanych w języku Python dla zarządzania model wdrażania zasobów nowej generacji infrastruktury CLI.</span><span class="sxs-lookup"><span data-stu-id="d1e5e-109">Also, try out [Azure CLI 2.0](https://github.com/Azure/azure-cli), a next-generation CLI written in Python for the resource management deployment model.</span></span>
>
>

## <a name="managing-app-service-plans"></a><span data-ttu-id="d1e5e-110">Plany zarządzania z usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="d1e5e-110">Managing App Service Plans</span></span>
### <a name="create-an-app-service-plan"></a><span data-ttu-id="d1e5e-111">Tworzenie planu usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="d1e5e-111">Create an App Service Plan</span></span>
<span data-ttu-id="d1e5e-112">Aby utworzyć plan usługi aplikacji, użyj **utworzyć azure appserviceplan** polecenia.</span><span class="sxs-lookup"><span data-stu-id="d1e5e-112">To create an app service plan, use the **azure appserviceplan create** command.</span></span>

<span data-ttu-id="d1e5e-113">Poniżej przedstawiono opisy różnych parametrów:</span><span class="sxs-lookup"><span data-stu-id="d1e5e-113">Following are descriptions of the different parameters:</span></span>

* <span data-ttu-id="d1e5e-114">**--grupy zasobów**: grupy zasobów, która zawiera plan usługi aplikacji nowo utworzony.</span><span class="sxs-lookup"><span data-stu-id="d1e5e-114">**--resource-group**: resource group that includes the newly created app service plan.</span></span>
* <span data-ttu-id="d1e5e-115">**--name**: Nazwa planu usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d1e5e-115">**--name**: name of the app service plan.</span></span>
* <span data-ttu-id="d1e5e-116">**--lokalizacji**: Lokalizacja planu usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d1e5e-116">**--location**: app service plan location.</span></span>
* <span data-ttu-id="d1e5e-117">**Jednostka sku —**: żądany cenową jednostki sku (dostępne są następujące opcje: F1 (bezpłatnie).</span><span class="sxs-lookup"><span data-stu-id="d1e5e-117">**--sku**:  the desired pricing sku (The options are: F1 (Free).</span></span> <span data-ttu-id="d1e5e-118">D1 (wspólna).</span><span class="sxs-lookup"><span data-stu-id="d1e5e-118">D1 (Shared).</span></span> <span data-ttu-id="d1e5e-119">B1 (podstawowe mała liczba godzin), B2 (podstawowa średnia liczba godzin) i B3 (Basic duże).</span><span class="sxs-lookup"><span data-stu-id="d1e5e-119">B1 (Basic Small), B2 (Basic Medium), and B3 (Basic Large).</span></span> <span data-ttu-id="d1e5e-120">S1 (standardowa mała liczba godzin), S2 (standardowa średnia liczba godzin) i S3 (Standard duże).</span><span class="sxs-lookup"><span data-stu-id="d1e5e-120">S1 (Standard Small), S2 (Standard Medium), and S3 (Standard Large).</span></span> <span data-ttu-id="d1e5e-121">P1 (mały Premium), P2 (średnia Premium), a P3 (duże Premium).)</span><span class="sxs-lookup"><span data-stu-id="d1e5e-121">P1 (Premium Small), P2 (Premium Medium), and P3 (Premium Large).)</span></span>
* <span data-ttu-id="d1e5e-122">**--wystąpień**: liczba pracowników w aplikacji usługi plan (wartość domyślna to 1).</span><span class="sxs-lookup"><span data-stu-id="d1e5e-122">**--instances**: the number of workers in the app service plan (Default value is 1).</span></span>

<span data-ttu-id="d1e5e-123">Przykład można używać tego polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="d1e5e-123">Example to use this cmdlet:</span></span>

    azure appserviceplan create --name ContosoAppServicePlan --location "South Central US" --resource-group ContosoAzureResourceGroup --sku P1 --instances 10

#### <a name="create-a-linux-app-service-plan"></a><span data-ttu-id="d1e5e-124">Tworzenie planu usługi aplikacji w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="d1e5e-124">Create a Linux App Service Plan</span></span>

<span data-ttu-id="d1e5e-125">Korzystającej z tego samego **utworzyć azure appserviceplan** polecenia z dodatkowym parametrem **true--islinux**.</span><span class="sxs-lookup"><span data-stu-id="d1e5e-125">Using the same **azure appserviceplan create** command, with the extra parameter **--islinux true**.</span></span> <span data-ttu-id="d1e5e-126">Należy pamiętać, ograniczenia i regiony opisane w temacie [wprowadzenie do usługi App Service w systemie Linux](app-service-linux-intro.md)</span><span class="sxs-lookup"><span data-stu-id="d1e5e-126">Note the restrictions and regions outlined in [Introduction to App Service on Linux](app-service-linux-intro.md)</span></span>

### <a name="list-existing-app-service-plans"></a><span data-ttu-id="d1e5e-127">Lista istniejących planów usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="d1e5e-127">List Existing App Service Plans</span></span>
<span data-ttu-id="d1e5e-128">Aby wyświetlić listę istniejących planów usługi aplikacji, należy użyć **listy azure appserviceplan** polecenia.</span><span class="sxs-lookup"><span data-stu-id="d1e5e-128">To list the existing app service plans, use **azure appserviceplan list** command.</span></span>

<span data-ttu-id="d1e5e-129">Aby wyświetlić listę wszystkich planów usługi aplikacji w obszarze określonej grupy zasobów, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="d1e5e-129">To list all app service plans under a specific resource group, use:</span></span>

    azure appserviceplan list --resource-group ContosoAzureResourceGroup

<span data-ttu-id="d1e5e-130">Aby uzyskać plan usługi specyficzne dla aplikacji, należy użyć **Pokaż azure appserviceplan** polecenia:</span><span class="sxs-lookup"><span data-stu-id="d1e5e-130">To get a specific app service plan, use **azure appserviceplan show** command:</span></span>

    azure appserviceplan show --name ContosoAppServicePlan --resource-group southeastasia

### <a name="configure-an-existing-app-service-plan"></a><span data-ttu-id="d1e5e-131">Skonfiguruj istniejący Plan usługi App Service</span><span class="sxs-lookup"><span data-stu-id="d1e5e-131">Configure an existing App Service Plan</span></span>
<span data-ttu-id="d1e5e-132">Aby zmienić ustawienia dla istniejącego planu usługi aplikacji, należy użyć **azure appserviceplan config** polecenia.</span><span class="sxs-lookup"><span data-stu-id="d1e5e-132">To change the settings for an existing app service plan, use the **azure appserviceplan config** command.</span></span> <span data-ttu-id="d1e5e-133">Można zmienić jednostki sku i liczbę procesów roboczych</span><span class="sxs-lookup"><span data-stu-id="d1e5e-133">You can change the sku, and the number of workers</span></span> 

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --sku S1 --instances 9

#### <a name="scaling-an-app-service-plan"></a><span data-ttu-id="d1e5e-134">Skalowanie planu usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="d1e5e-134">Scaling an App Service Plan</span></span>
<span data-ttu-id="d1e5e-135">Aby skalować istniejący Plan usługi App Service, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="d1e5e-135">To scale an existing App Service Plan, use:</span></span>

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --instances 9

#### <a name="changing-the-sku-of-an-app-service-plan"></a><span data-ttu-id="d1e5e-136">Zmiana jednostki SKU planu usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="d1e5e-136">Changing the SKU of an App Service Plan</span></span>
<span data-ttu-id="d1e5e-137">Aby zmienić numer istniejący Plan usługi App Service, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="d1e5e-137">To change the sku of an existing App Service Plan, use:</span></span>

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --sku S1


### <a name="delete-an-existing-app-service-plan"></a><span data-ttu-id="d1e5e-138">Usuń istniejący Plan usługi App Service</span><span class="sxs-lookup"><span data-stu-id="d1e5e-138">Delete an existing App Service Plan</span></span>
<span data-ttu-id="d1e5e-139">Aby usunąć istniejący plan usługi aplikacji, wszystkie aplikacje przypisanej muszą zostać przeniesiony lub usunięciem.</span><span class="sxs-lookup"><span data-stu-id="d1e5e-139">To delete an existing app service plan, all assigned apps need to be moved or deleted first.</span></span> <span data-ttu-id="d1e5e-140">Następnie przy użyciu **usunąć aplikacji sieci Web azure** polecenia, można usunąć planu usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d1e5e-140">Then using the **azure webapp delete** command you can delete the app service plan.</span></span>

    azure appserviceplan delete --name ContosoAppServicePlan --resource-group southeastasia

## <a name="managing-app-service-apps"></a><span data-ttu-id="d1e5e-141">Zarządzanie aplikacjami usługi App Service</span><span class="sxs-lookup"><span data-stu-id="d1e5e-141">Managing App Service apps</span></span>
### <a name="create-a-web-app"></a><span data-ttu-id="d1e5e-142">Tworzenie aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="d1e5e-142">Create a web app</span></span>
<span data-ttu-id="d1e5e-143">Aby utworzyć aplikację sieci web, użyj **tworzenie aplikacji sieci Web azure** polecenia.</span><span class="sxs-lookup"><span data-stu-id="d1e5e-143">To create a web app, use the **azure webapp create** command.</span></span>

<span data-ttu-id="d1e5e-144">Poniżej przedstawiono opisy różnych parametrów:</span><span class="sxs-lookup"><span data-stu-id="d1e5e-144">Following are descriptions of the different parameters:</span></span>

* <span data-ttu-id="d1e5e-145">**--name**: Nazwa aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="d1e5e-145">**--name**: name for the web app.</span></span>
* <span data-ttu-id="d1e5e-146">**--planu**: Nazwa planu usługi używany do obsługi aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="d1e5e-146">**--plan**: name for the service plan used to host the web app.</span></span>
* <span data-ttu-id="d1e5e-147">**--grupy zasobów**: grupę zasobów, która obsługuje plan usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d1e5e-147">**--resource-group**: resource group that hosts the App service plan.</span></span>
* <span data-ttu-id="d1e5e-148">**--lokalizacji**: Lokalizacja aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="d1e5e-148">**--location**: the web app location.</span></span>

<span data-ttu-id="d1e5e-149">Przykład można używać tego polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="d1e5e-149">Example to use this cmdlet:</span></span>

    azure webapp create --name ContosoWebApp --resource-group ContosoAzureResourceGroup --plan ContosoAppServicePlan --location "South Central US"

### <a name="delete-an-existing-app"></a><span data-ttu-id="d1e5e-150">Usuń istniejącą aplikację</span><span class="sxs-lookup"><span data-stu-id="d1e5e-150">Delete an existing app</span></span>
<span data-ttu-id="d1e5e-151">Aby usunąć istniejącą aplikację, można użyć **usunąć aplikacji sieci Web azure** polecenia.</span><span class="sxs-lookup"><span data-stu-id="d1e5e-151">To delete an existing app, you can use the **azure webapp delete** command.</span></span> <span data-ttu-id="d1e5e-152">Należy określić nazwę aplikacji i nazwę grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="d1e5e-152">You need to specify the name of the app and the resource group name.</span></span>

    azure webapp delete --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="list-existing-apps"></a><span data-ttu-id="d1e5e-153">Listy istniejących aplikacji</span><span class="sxs-lookup"><span data-stu-id="d1e5e-153">List existing apps</span></span>
<span data-ttu-id="d1e5e-154">Aby wyświetlić listę istniejących aplikacji, należy użyć **listy aplikacji sieci Web azure** polecenia.</span><span class="sxs-lookup"><span data-stu-id="d1e5e-154">To list the existing apps, use the **azure webapp list** command.</span></span>

<span data-ttu-id="d1e5e-155">Aby wyświetlić listę wszystkich aplikacji w określonej grupy zasobów, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="d1e5e-155">To list all apps in a specific resource group, use:</span></span>

    azure webapp list --resource-group ContosoAzureResourceGroup

<span data-ttu-id="d1e5e-156">Aby uzyskać konkretną aplikację, należy użyć **Pokaż aplikacji sieci Web azure** polecenia.</span><span class="sxs-lookup"><span data-stu-id="d1e5e-156">To get a specific app, use the **azure webapp show** command.</span></span>

    azure webapp show --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="configure-an-existing-app"></a><span data-ttu-id="d1e5e-157">Konfigurowanie istniejącej aplikacji</span><span class="sxs-lookup"><span data-stu-id="d1e5e-157">Configure an existing app</span></span>
<span data-ttu-id="d1e5e-158">Aby zmienić ustawienia i konfiguracje dla istniejącej aplikacji, użyj **aplikacji sieci Web azure config set** polecenia.</span><span class="sxs-lookup"><span data-stu-id="d1e5e-158">To change the settings and configurations for an existing app, use the **azure webapp config set** command.</span></span>

<span data-ttu-id="d1e5e-159">Przykład (1): Zmień wersję php aplikacji</span><span class="sxs-lookup"><span data-stu-id="d1e5e-159">Example (1): change the php version of a app</span></span> 

    azure webapp config set --name ContosoWebApp --resource-group ContosoAzureResourceGroup --phpversion 5.6

<span data-ttu-id="d1e5e-160">Przykład (2): Dodawanie lub zmienianie ustawień aplikacji</span><span class="sxs-lookup"><span data-stu-id="d1e5e-160">Example (2): add or change app settings</span></span>

    webapp config appsettings set --name ContosoWebApp --resource-group ContosoAzureResourceGroup appsetting1=appsetting1value,appsetting2=appsetting2value

<span data-ttu-id="d1e5e-161">Wiedzieć, co inna konfiguracja może być zmieniona, użyj **konfiguracji aplikacji sieci Web azure wartości -h** polecenia.</span><span class="sxs-lookup"><span data-stu-id="d1e5e-161">To know what other configuration can be changed, use the **azure webapp config set -h** command.</span></span>

### <a name="change-the-state-of-an-existing-app"></a><span data-ttu-id="d1e5e-162">Zmień stan istniejącej aplikacji</span><span class="sxs-lookup"><span data-stu-id="d1e5e-162">Change the state of an existing app</span></span>
#### <a name="restart-an-app"></a><span data-ttu-id="d1e5e-163">Uruchom ponownie aplikację</span><span class="sxs-lookup"><span data-stu-id="d1e5e-163">Restart an app</span></span>
<span data-ttu-id="d1e5e-164">Aby ponownie uruchomić aplikację, należy określić nazwę i zasobów grupy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d1e5e-164">To restart an app, you must specify the name and resource group of the app.</span></span>

    azure webapp restart --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="stop-an-app"></a><span data-ttu-id="d1e5e-165">Zatrzymaj aplikację</span><span class="sxs-lookup"><span data-stu-id="d1e5e-165">Stop an app</span></span>
<span data-ttu-id="d1e5e-166">Aby zatrzymać aplikację, należy określić nazwę i zasobów grupy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d1e5e-166">To stop an app, you must specify the name and resource group of the app.</span></span>

    azure webapp stop --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="start-an-app"></a><span data-ttu-id="d1e5e-167">Uruchamiają aplikację</span><span class="sxs-lookup"><span data-stu-id="d1e5e-167">Start an app</span></span>
<span data-ttu-id="d1e5e-168">Aby uruchomić aplikację, należy określić nazwę i zasobów grupy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d1e5e-168">To start an app, you must specify the name and resource group of the app.</span></span>

    azure webapp start --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="manage-publishing-profiles-of-an-app"></a><span data-ttu-id="d1e5e-169">Zarządzanie profilami publikowania aplikacji</span><span class="sxs-lookup"><span data-stu-id="d1e5e-169">Manage publishing profiles of an app</span></span>
<span data-ttu-id="d1e5e-170">Każda aplikacja ma profil publikowania, który może być używana do publikowania kodu.</span><span class="sxs-lookup"><span data-stu-id="d1e5e-170">Each app has a publishing profile that can be used to publish your code.</span></span>

#### <a name="get-publishing-profile"></a><span data-ttu-id="d1e5e-171">Pobierz publikowania profilu</span><span class="sxs-lookup"><span data-stu-id="d1e5e-171">Get Publishing Profile</span></span>
<span data-ttu-id="d1e5e-172">Aby pobrać profilu publikowania aplikacji, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="d1e5e-172">To get the publishing profile for a app, use:</span></span>

    azure webapp publishingprofile --name ContosoWebApp --resource-group ContosoAzureResourceGroup

<span data-ttu-id="d1e5e-173">To polecenie zwraca publikowania profilu nazwy użytkownika i hasło w wierszu polecenia.</span><span class="sxs-lookup"><span data-stu-id="d1e5e-173">This command echoes the publishing profile username and password to the command line.</span></span>

### <a name="manage-app-hostnames"></a><span data-ttu-id="d1e5e-174">Zarządzanie nazwy hostów aplikacji</span><span class="sxs-lookup"><span data-stu-id="d1e5e-174">Manage app hostnames</span></span>
<span data-ttu-id="d1e5e-175">Aby zarządzać powiązań z nazwami hostów dla aplikacji, należy użyć **hostnames konfiguracji aplikacji sieci Web azure** polecenia</span><span class="sxs-lookup"><span data-stu-id="d1e5e-175">To manage hostname bindings for your app, use the **azure webapp config hostnames** command</span></span>  

#### <a name="list-hostname-bindings"></a><span data-ttu-id="d1e5e-176">Lista powiązań z nazwami hostów</span><span class="sxs-lookup"><span data-stu-id="d1e5e-176">List hostname bindings</span></span>
<span data-ttu-id="d1e5e-177">Aby uzyskać bieżące powiązań z nazwami hostów, dla aplikacji, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="d1e5e-177">To get the current hostname bindings for an app, use:</span></span>

    azure webapp config hostnames list --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="add-hostname-bindings"></a><span data-ttu-id="d1e5e-178">Dodawanie powiązań z nazwami hostów</span><span class="sxs-lookup"><span data-stu-id="d1e5e-178">Add hostname bindings</span></span>
<span data-ttu-id="d1e5e-179">Aby dodać powiązań z nazwami hostów do aplikacji, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="d1e5e-179">To add hostname bindings to an app, use:</span></span>

    azure webapp config hostnames add --name ContosoWebApp --resource-group ContosoAzureResourceGroup --hostname www.contoso.com

#### <a name="delete-hostname-bindings"></a><span data-ttu-id="d1e5e-180">Usuń powiązań z nazwami hostów</span><span class="sxs-lookup"><span data-stu-id="d1e5e-180">Delete hostname bindings</span></span>
<span data-ttu-id="d1e5e-181">Aby usunąć powiązań z nazwami hostów, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="d1e5e-181">To delete hostname bindings, use:</span></span>

    azure webapp config hostnames delete --name ContosoWebApp --resource-group ContosoAzureResourceGroup --hostname www.contoso.com

## <a name="next-steps"></a><span data-ttu-id="d1e5e-182">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d1e5e-182">Next Steps</span></span>
* <span data-ttu-id="d1e5e-183">Aby dowiedzieć się więcej na temat obsługi interfejsu wiersza polecenia Menedżera zasobów Azure, zobacz [użyć wiersza polecenia platformy Azure do zarządzania zasobami Azure i grup zasobów.](../azure-resource-manager/xplat-cli-azure-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="d1e5e-183">To learn about Azure Resource Manager CLI support, see [Use the Azure CLI to manage Azure resources and resource groups.](../azure-resource-manager/xplat-cli-azure-resource-manager.md)</span></span>
* <span data-ttu-id="d1e5e-184">Aby dowiedzieć się więcej o zarządzaniu App Service przy użyciu programu PowerShell, zobacz [Using Azure Resource Manager-Based PowerShell do zarządzania aplikacji sieci Web platformy Azure.](app-service-web-app-azure-resource-manager-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="d1e5e-184">To learn about managing App Service using PowerShell, see [Using Azure Resource Manager-Based PowerShell to Manage Azure Web Apps.](app-service-web-app-azure-resource-manager-powershell.md)</span></span>
* <span data-ttu-id="d1e5e-185">Aby dowiedzieć się więcej o usłudze Azure App Service w systemie Linux, zobacz [wprowadzenie do usługi App Service w systemie Linux](app-service-linux-intro.md)</span><span class="sxs-lookup"><span data-stu-id="d1e5e-185">To learn about Azure App Service on Linux, see [Introduction to App Service on Linux](app-service-linux-intro.md)</span></span>
