---
title: "Migrowanie do Menedżera zasobów przy użyciu programu PowerShell | Dokumentacja firmy Microsoft"
description: "W tym artykule przedstawiono w trakcie migracji obsługiwane przez platformę IaaS zasobów, takich jak maszynach wirtualnych (VM), sieci wirtualnych (sieci wirtualne) oraz kont magazynu ze środowiska klasycznego do usługi Azure Resource Manager (ARM) za pomocą poleceń programu PowerShell systemu Azure"
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 2b3dff9b-2e99-4556-acc5-d75ef234af9c
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: kasing
ms.openlocfilehash: 489e6cc6bd3c5b36635f5f7e398d08fed681d2e7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="migrate-iaas-resources-from-classic-to-azure-resource-manager-by-using-azure-powershell"></a><span data-ttu-id="2ff7b-103">Migracja zasobów IaaS ze środowiska klasycznego do usługi Azure Resource Manager przy użyciu programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="2ff7b-103">Migrate IaaS resources from classic to Azure Resource Manager by using Azure PowerShell</span></span>
<span data-ttu-id="2ff7b-104">Te kroki pokazują, jak używać poleceń programu Azure PowerShell do migracji infrastruktury jako zasoby usługi (IaaS) z klasycznym modelu wdrażania modelu wdrażania usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="2ff7b-104">These steps show you how to use Azure PowerShell commands to migrate infrastructure as a service (IaaS) resources from the classic deployment model to the Azure Resource Manager deployment model.</span></span>

<span data-ttu-id="2ff7b-105">Należy również przeprowadzić migrację zasobów za pomocą [interfejsu wiersza polecenia platformy Azure (Azure CLI)](../linux/migration-classic-resource-manager-cli.md).</span><span class="sxs-lookup"><span data-stu-id="2ff7b-105">If you want, you can also migrate resources by using the [Azure Command Line Interface (Azure CLI)](../linux/migration-classic-resource-manager-cli.md).</span></span>

* <span data-ttu-id="2ff7b-106">Aby uzyskać podstawowe informacje dotyczące obsługiwanych scenariuszy migracji, zobacz [obsługiwane platformy migracji zasobów IaaS ze środowiska klasycznego do usługi Azure Resource Manager](migration-classic-resource-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2ff7b-106">For background on supported migration scenarios, see [Platform-supported migration of IaaS resources from classic to Azure Resource Manager](migration-classic-resource-manager-overview.md).</span></span>
* <span data-ttu-id="2ff7b-107">Aby uzyskać szczegółowe wskazówki i Przewodnik migracji, zobacz [techniczne szczegółowe informacje na temat obsługiwanych platform migracji ze środowiska klasycznego do usługi Azure Resource Manager](migration-classic-resource-manager-deep-dive.md).</span><span class="sxs-lookup"><span data-stu-id="2ff7b-107">For detailed guidance and a migration walkthrough, see [Technical deep dive on platform-supported migration from classic to Azure Resource Manager](migration-classic-resource-manager-deep-dive.md).</span></span>
* [<span data-ttu-id="2ff7b-108">Przegląd najbardziej typowych błędów migracji</span><span class="sxs-lookup"><span data-stu-id="2ff7b-108">Review most common migration errors</span></span>](migration-classic-resource-manager-errors.md)

<br>
<span data-ttu-id="2ff7b-109">Oto schemat blokowy, aby określić kolejność kroków muszą być wykonywane podczas procesu migracji</span><span class="sxs-lookup"><span data-stu-id="2ff7b-109">Here is a flowchart to identify the order in which steps need to be executed during a migration process</span></span>

![Zrzut ekranu przedstawiający kroki migracji](media/migration-classic-resource-manager/migration-flow.png)

## <a name="step-1-plan-for-migration"></a><span data-ttu-id="2ff7b-111">Krok 1: Planowanie migracji</span><span class="sxs-lookup"><span data-stu-id="2ff7b-111">Step 1: Plan for migration</span></span>
<span data-ttu-id="2ff7b-112">Poniżej przedstawiono kilka najlepsze rozwiązania, które są zalecane jako ocenić Migrowanie zasobów IaaS z klasycznego do Menedżera zasobów:</span><span class="sxs-lookup"><span data-stu-id="2ff7b-112">Here are a few best practices that we recommend as you evaluate migrating IaaS resources from classic to Resource Manager:</span></span>

* <span data-ttu-id="2ff7b-113">Zapoznaj się z artykułem [obsługiwane i nieobsługiwane funkcje i konfiguracje](migration-classic-resource-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2ff7b-113">Read through the [supported and unsupported features and configurations](migration-classic-resource-manager-overview.md).</span></span> <span data-ttu-id="2ff7b-114">Jeśli masz maszyn wirtualnych, które używają nieobsługiwane konfiguracje i funkcje, zaleca się poczekać do obsługi funkcji/konfiguracji zostaną ogłoszone.</span><span class="sxs-lookup"><span data-stu-id="2ff7b-114">If you have virtual machines that use unsupported configurations or features, we recommend that you wait for the configuration/feature support to be announced.</span></span> <span data-ttu-id="2ff7b-115">Jeśli zgodnie z potrzebami, Usuń tej funkcji lub wychodzenia takiej konfiguracji, aby umożliwić migrację.</span><span class="sxs-lookup"><span data-stu-id="2ff7b-115">Alternatively, if it suits your needs, remove that feature or move out of that configuration to enable migration.</span></span>
* <span data-ttu-id="2ff7b-116">Jeśli mają automatyczny skrypty, które obecnie wdrażanie infrastruktury i aplikacji, spróbuj utworzyć podobnych konfiguracji testu przy użyciu tych skryptów do migracji.</span><span class="sxs-lookup"><span data-stu-id="2ff7b-116">If you have automated scripts that deploy your infrastructure and applications today, try to create a similar test setup by using those scripts for migration.</span></span> <span data-ttu-id="2ff7b-117">Można też skonfigurować próbkę środowiskami przy użyciu portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="2ff7b-117">Alternatively, you can set up sample environments by using the Azure portal.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2ff7b-118">Bramy aplikacji nie są obecnie obsługiwane dla migracji ze środowiska klasycznego do Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="2ff7b-118">Application Gateways are not currently supported for migration from classic to Resource Manager.</span></span> <span data-ttu-id="2ff7b-119">Aby przeprowadzić migrację z bramy aplikacji klasycznej sieci wirtualnej, należy usunąć bramę, przed uruchomieniem operacji Prepare, aby przenieść sieć.</span><span class="sxs-lookup"><span data-stu-id="2ff7b-119">To migrate a classic virtual network with an Application gateway, remove the gateway before running a Prepare operation to move the network.</span></span> <span data-ttu-id="2ff7b-120">Po zakończeniu migracji należy ponownie podłączyć bramy w usłudze Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="2ff7b-120">After you complete the migration, reconnect the gateway in Azure Resource Manager.</span></span>
>
><span data-ttu-id="2ff7b-121">Bram usługi ExpressRoute nawiązywania obwody usługi ExpressRoute w innej subskrypcji nie może być migrowane automatycznie.</span><span class="sxs-lookup"><span data-stu-id="2ff7b-121">ExpressRoute gateways connecting to ExpressRoute circuits in another subscription cannot be migrated automatically.</span></span> <span data-ttu-id="2ff7b-122">W takiej sytuacji należy usunąć bramę usługi ExpressRoute, migrację sieci wirtualnej i Utwórz ponownie bramę.</span><span class="sxs-lookup"><span data-stu-id="2ff7b-122">In such cases, remove the ExpressRoute gateway, migrate the virtual network and recreate the gateway.</span></span> <span data-ttu-id="2ff7b-123">Zobacz [ExpressRoute migracji obwody i skojarzone sieci wirtualne z klasycznego modelu wdrażania usługi Resource Manager](../../expressroute/expressroute-migration-classic-resource-manager.md) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="2ff7b-123">Please see [Migrate ExpressRoute circuits and associated virtual networks from the classic to the Resource Manager deployment model](../../expressroute/expressroute-migration-classic-resource-manager.md) for more information.</span></span>
>
>

## <a name="step-2-install-the-latest-version-of-azure-powershell"></a><span data-ttu-id="2ff7b-124">Krok 2: Zainstaluj najnowszą wersję programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="2ff7b-124">Step 2: Install the latest version of Azure PowerShell</span></span>
<span data-ttu-id="2ff7b-125">Istnieją dwie główne opcje instalacji programu Azure PowerShell: [galerii programu PowerShell](https://www.powershellgallery.com/profiles/azure-sdk/) lub [Instalatora platformy sieci Web (WebPI)](http://aka.ms/webpi-azps).</span><span class="sxs-lookup"><span data-stu-id="2ff7b-125">There are two main options to install Azure PowerShell: [PowerShell Gallery](https://www.powershellgallery.com/profiles/azure-sdk/) or [Web Platform Installer (WebPI)](http://aka.ms/webpi-azps).</span></span> <span data-ttu-id="2ff7b-126">WebPI odbiera comiesięcznych aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="2ff7b-126">WebPI receives monthly updates.</span></span> <span data-ttu-id="2ff7b-127">Galerii programu PowerShell odbiera aktualizacje w sposób ciągły.</span><span class="sxs-lookup"><span data-stu-id="2ff7b-127">PowerShell Gallery receives updates on a continuous basis.</span></span> <span data-ttu-id="2ff7b-128">W tym artykule jest oparta na program Azure PowerShell w wersji 2.1.0.</span><span class="sxs-lookup"><span data-stu-id="2ff7b-128">This article is based on Azure PowerShell version 2.1.0.</span></span>

<span data-ttu-id="2ff7b-129">Aby uzyskać instrukcje instalacji, zobacz [jak instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2ff7b-129">For installation instructions, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<br>

## <a name="step-3-ensure-that-you-are-an-administrator-for-the-subscription-in-azure-portal"></a><span data-ttu-id="2ff7b-130">Krok 3: Upewnij się, że jesteś administratorem subskrypcji w portalu Azure</span><span class="sxs-lookup"><span data-stu-id="2ff7b-130">Step 3: Ensure that you are an administrator for the subscription in Azure portal</span></span>
<span data-ttu-id="2ff7b-131">Do przeprowadzania migracji, możesz muszą zostać dodane jako współadministrator subskrypcji w [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2ff7b-131">To perform this migration, you must be added as a co-administrator for the subscription in the [Azure portal](https://portal.azure.com).</span></span>

1. <span data-ttu-id="2ff7b-132">Zaloguj się do [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2ff7b-132">Sign into the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="2ff7b-133">W menu Centrum wybierz **subskrypcji**.</span><span class="sxs-lookup"><span data-stu-id="2ff7b-133">On the Hub menu, select **Subscription**.</span></span> <span data-ttu-id="2ff7b-134">Jeśli nie widzisz, wybierz **więcej usług**.</span><span class="sxs-lookup"><span data-stu-id="2ff7b-134">If you don't see it, select **More services**.</span></span>
3. <span data-ttu-id="2ff7b-135">Znajdź pozycję odpowiednie subskrypcji, a następnie przyjrzeć się **Moje roli** pola.</span><span class="sxs-lookup"><span data-stu-id="2ff7b-135">Find the appropriate subscription entry, then look at the **MY ROLE** field.</span></span> <span data-ttu-id="2ff7b-136">Dla administratora współpracującego, wartość powinna być _administrator konta_.</span><span class="sxs-lookup"><span data-stu-id="2ff7b-136">For a co-administrator, the value should be _Account admin_.</span></span>

<span data-ttu-id="2ff7b-137">Jeśli nie jest możliwe dodać administratora współpracującego, następnie skontaktuj się z administratorem usługi ani współadministratorem subskrypcji można pobrać samodzielnie dodane.</span><span class="sxs-lookup"><span data-stu-id="2ff7b-137">If you are not able to add a co-administrator, then contact a service administrator or co-administrator for the subscription to get yourself added.</span></span>   

## <a name="step-4-set-your-subscription-and-sign-up-for-migration"></a><span data-ttu-id="2ff7b-138">Krok 4: Ustaw subskrypcji i zaloguj do migracji</span><span class="sxs-lookup"><span data-stu-id="2ff7b-138">Step 4: Set your subscription and sign up for migration</span></span>
<span data-ttu-id="2ff7b-139">Najpierw należy uruchomić wiersz programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2ff7b-139">First, start a PowerShell prompt.</span></span> <span data-ttu-id="2ff7b-140">W przypadku migracji należy skonfigurować środowisko dla obu classic i Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="2ff7b-140">For migration, you need to set up your environment for both classic and Resource Manager.</span></span>

<span data-ttu-id="2ff7b-141">Zaloguj się do swojego konta dla modelu Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="2ff7b-141">Sign in to your account for the Resource Manager model.</span></span>

```powershell
    Login-AzureRmAccount
```

<span data-ttu-id="2ff7b-142">Uzyskiwanie dostępnych subskrypcji przy użyciu następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="2ff7b-142">Get the available subscriptions by using the following command:</span></span>

```powershell
    Get-AzureRMSubscription | Sort Name | Select Name
```

<span data-ttu-id="2ff7b-143">Ustaw subskrypcji platformy Azure dla bieżącej sesji.</span><span class="sxs-lookup"><span data-stu-id="2ff7b-143">Set your Azure subscription for the current session.</span></span> <span data-ttu-id="2ff7b-144">W tym przykładzie ustawia domyślną nazwę subskrypcji **moją subskrypcję Azure**.</span><span class="sxs-lookup"><span data-stu-id="2ff7b-144">This example sets the default subscription name to **My Azure Subscription**.</span></span> <span data-ttu-id="2ff7b-145">Przykładowa nazwa subskrypcji należy zastąpić własnymi.</span><span class="sxs-lookup"><span data-stu-id="2ff7b-145">Replace the example subscription name with your own.</span></span>

```powershell
    Select-AzureRmSubscription –SubscriptionName "My Azure Subscription"
```

> [!NOTE]
> <span data-ttu-id="2ff7b-146">Rejestracja jest jednorazowe krok, ale należy to robić raz przed próbą wykonania migracji.</span><span class="sxs-lookup"><span data-stu-id="2ff7b-146">Registration is a one-time step, but you must do it once before attempting migration.</span></span> <span data-ttu-id="2ff7b-147">Bez rejestrowania, zobacz się następujący komunikat o błędzie:</span><span class="sxs-lookup"><span data-stu-id="2ff7b-147">Without registering, you see the following error message:</span></span>
>
> <span data-ttu-id="2ff7b-148">*Element BadRequest: Subskrypcja nie jest zarejestrowana do migracji.*</span><span class="sxs-lookup"><span data-stu-id="2ff7b-148">*BadRequest : Subscription is not registered for migration.*</span></span>
>
>

<span data-ttu-id="2ff7b-149">Rejestracja dostawcy zasobów migracji za pomocą następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="2ff7b-149">Register with the migration resource provider by using the following command:</span></span>

```powershell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
```

<span data-ttu-id="2ff7b-150">Poczekaj pięć minut dla rejestracji zakończyć.</span><span class="sxs-lookup"><span data-stu-id="2ff7b-150">Please wait five minutes for the registration to finish.</span></span> <span data-ttu-id="2ff7b-151">Można sprawdzić stan zatwierdzenia za pomocą następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="2ff7b-151">You can check the status of the approval by using the following command:</span></span>

```powershell
    Get-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
```

<span data-ttu-id="2ff7b-152">Upewnij się, że jest RegistrationState `Registered` przed kontynuowaniem.</span><span class="sxs-lookup"><span data-stu-id="2ff7b-152">Make sure that RegistrationState is `Registered` before you proceed.</span></span>

<span data-ttu-id="2ff7b-153">Teraz logować się do swojego konta w przypadku modelu klasycznego.</span><span class="sxs-lookup"><span data-stu-id="2ff7b-153">Now sign in to your account for the classic model.</span></span>

```powershell
    Add-AzureAccount
```

<span data-ttu-id="2ff7b-154">Uzyskiwanie dostępnych subskrypcji przy użyciu następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="2ff7b-154">Get the available subscriptions by using the following command:</span></span>

```powershell
    Get-AzureSubscription | Sort SubscriptionName | Select SubscriptionName
```

<span data-ttu-id="2ff7b-155">Ustaw subskrypcji platformy Azure dla bieżącej sesji.</span><span class="sxs-lookup"><span data-stu-id="2ff7b-155">Set your Azure subscription for the current session.</span></span> <span data-ttu-id="2ff7b-156">W tym przykładzie subskrypcji domyślne **moją subskrypcję Azure**.</span><span class="sxs-lookup"><span data-stu-id="2ff7b-156">This example sets the default subscription to **My Azure Subscription**.</span></span> <span data-ttu-id="2ff7b-157">Przykładowa nazwa subskrypcji należy zastąpić własnymi.</span><span class="sxs-lookup"><span data-stu-id="2ff7b-157">Replace the example subscription name with your own.</span></span>

```powershell
    Select-AzureSubscription –SubscriptionName "My Azure Subscription"
```

<br>

## <a name="step-5-make-sure-you-have-enough-azure-resource-manager-virtual-machine-cores-in-the-azure-region-of-your-current-deployment-or-vnet"></a><span data-ttu-id="2ff7b-158">Krok 5: Upewnij się, że masz wystarczająco dużo rdzeni maszyny wirtualnej Azure Resource Manager w regionie Azure bieżącego wdrożenia lub sieci Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="2ff7b-158">Step 5: Make sure you have enough Azure Resource Manager Virtual Machine cores in the Azure region of your current deployment or VNET</span></span>
<span data-ttu-id="2ff7b-159">Aby sprawdzić bieżącą liczbę rdzeni, do których masz usługi Azure Resource Manager służy następującego polecenia programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2ff7b-159">You can use the following PowerShell command to check the current number of cores you have in Azure Resource Manager.</span></span> <span data-ttu-id="2ff7b-160">Aby dowiedzieć się więcej o przydziały core, zobacz [limity i usługi Azure Resource Manager](../../azure-subscription-service-limits.md#limits-and-the-azure-resource-manager).</span><span class="sxs-lookup"><span data-stu-id="2ff7b-160">To learn more about core quotas, see [Limits and the Azure Resource Manager](../../azure-subscription-service-limits.md#limits-and-the-azure-resource-manager).</span></span>

<span data-ttu-id="2ff7b-161">W tym przykładzie sprawdza dostępność **zachodnie stany USA** regionu.</span><span class="sxs-lookup"><span data-stu-id="2ff7b-161">This example checks the availability in the **West US** region.</span></span> <span data-ttu-id="2ff7b-162">Przykładowa nazwa regionu zastąpić własnym.</span><span class="sxs-lookup"><span data-stu-id="2ff7b-162">Replace the example region name with your own.</span></span>

```powershell
Get-AzureRmVMUsage -Location "West US"
```

## <a name="step-6-run-commands-to-migrate-your-iaas-resources"></a><span data-ttu-id="2ff7b-163">Krok 6: Uruchamianie poleceń, aby przeprowadzić migrację zasobów IaaS</span><span class="sxs-lookup"><span data-stu-id="2ff7b-163">Step 6: Run commands to migrate your IaaS resources</span></span>
> [!NOTE]
> <span data-ttu-id="2ff7b-164">Wszystkie czynności opisane w tym miejscu są idempotentności.</span><span class="sxs-lookup"><span data-stu-id="2ff7b-164">All the operations described here are idempotent.</span></span> <span data-ttu-id="2ff7b-165">Jeśli masz problem niż nieobsługiwanej funkcji lub błąd konfiguracji, zalecamy możesz ponowić próbę o przygotowaniu przerwania lub przekazania operacji.</span><span class="sxs-lookup"><span data-stu-id="2ff7b-165">If you have a problem other than an unsupported feature or a configuration error, we recommend that you retry the prepare, abort, or commit operation.</span></span> <span data-ttu-id="2ff7b-166">Platforma próbuje wykonać akcję ponownie.</span><span class="sxs-lookup"><span data-stu-id="2ff7b-166">The platform then tries the action again.</span></span>
>
>

## <a name="step-61-option-1---migrate-virtual-machines-in-a-cloud-service-not-in-a-virtual-network"></a><span data-ttu-id="2ff7b-167">Krok 6.1: Opcja 1 — migracji maszyn wirtualnych w usłudze w chmurze (nie w sieci wirtualnej)</span><span class="sxs-lookup"><span data-stu-id="2ff7b-167">Step 6.1: Option 1 - Migrate virtual machines in a cloud service (not in a virtual network)</span></span>
<span data-ttu-id="2ff7b-168">Pobierz listę usług w chmurze za pomocą następującego polecenia, a następnie wybierz usługę w chmurze, które chcesz migrować.</span><span class="sxs-lookup"><span data-stu-id="2ff7b-168">Get the list of cloud services by using the following command, and then pick the cloud service that you want to migrate.</span></span> <span data-ttu-id="2ff7b-169">Jeśli w sieci wirtualnej maszyn wirtualnych w usłudze w chmurze lub mają one role sieci web lub procesu roboczego, polecenie zwróci komunikat o błędzie.</span><span class="sxs-lookup"><span data-stu-id="2ff7b-169">If the VMs in the cloud service are in a virtual network or if they have web or worker roles, the command returns an error message.</span></span>

```powershell
    Get-AzureService | ft Servicename
```

<span data-ttu-id="2ff7b-170">Pobierz nazwę wdrożenia usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="2ff7b-170">Get the deployment name for the cloud service.</span></span> <span data-ttu-id="2ff7b-171">W tym przykładzie nazwa usługi jest **Moje usługi**.</span><span class="sxs-lookup"><span data-stu-id="2ff7b-171">In this example, the service name is **My Service**.</span></span> <span data-ttu-id="2ff7b-172">Przykładowa nazwa usługi należy zastąpić nazwę usługi.</span><span class="sxs-lookup"><span data-stu-id="2ff7b-172">Replace the example service name with your own service name.</span></span>

```powershell
    $serviceName = "My Service"
    $deployment = Get-AzureDeployment -ServiceName $serviceName
    $deploymentName = $deployment.DeploymentName
```

<span data-ttu-id="2ff7b-173">Przygotuj maszyny wirtualne w usłudze w chmurze do migracji.</span><span class="sxs-lookup"><span data-stu-id="2ff7b-173">Prepare the virtual machines in the cloud service for migration.</span></span> <span data-ttu-id="2ff7b-174">Dostępne są dwie opcje do wyboru.</span><span class="sxs-lookup"><span data-stu-id="2ff7b-174">You have two options to choose from.</span></span>

* <span data-ttu-id="2ff7b-175">**Opcja 1. Migrowanie maszyn wirtualnych do sieci wirtualnej utworzone platformy**</span><span class="sxs-lookup"><span data-stu-id="2ff7b-175">**Option 1. Migrate the VMs to a platform-created virtual network**</span></span>

    <span data-ttu-id="2ff7b-176">Po pierwsze sprawdzanie poprawności w przypadku migrowania usługi w chmurze przy użyciu następujących poleceń:</span><span class="sxs-lookup"><span data-stu-id="2ff7b-176">First, validate if you can migrate the cloud service using the following commands:</span></span>

    ```powershell
    $validate = Move-AzureService -Validate -ServiceName $serviceName `
        -DeploymentName $deploymentName -CreateNewVirtualNetwork
    $validate.ValidationMessages
    ```

    <span data-ttu-id="2ff7b-177">Poprzednie polecenie wyświetla wszystkie ostrzeżenia i błędy, które blokują migracji.</span><span class="sxs-lookup"><span data-stu-id="2ff7b-177">The preceding command displays any warnings and errors that block migration.</span></span> <span data-ttu-id="2ff7b-178">Jeśli weryfikacja zakończy się pomyślnie, a następnie można przenieść na **Prepare** krok:</span><span class="sxs-lookup"><span data-stu-id="2ff7b-178">If validation is successful, then you can move on to the **Prepare** step:</span></span>

    ```powershell
    Move-AzureService -Prepare -ServiceName $serviceName `
        -DeploymentName $deploymentName -CreateNewVirtualNetwork
    ```
* <span data-ttu-id="2ff7b-179">**Opcja 2. Migrowanie do istniejącej sieci wirtualnej w modelu wdrażania usługi Resource Manager**</span><span class="sxs-lookup"><span data-stu-id="2ff7b-179">**Option 2. Migrate to an existing virtual network in the Resource Manager deployment model**</span></span>

    <span data-ttu-id="2ff7b-180">W tym przykładzie nazwa grupy zasobów **myResourceGroup**, nazwa sieci wirtualnej do **myVirtualNetwork** i nazwy podsieci **mySubNet**.</span><span class="sxs-lookup"><span data-stu-id="2ff7b-180">This example sets the resource group name to **myResourceGroup**, the virtual network name to **myVirtualNetwork** and the subnet name to **mySubNet**.</span></span> <span data-ttu-id="2ff7b-181">Zamień nazwy w tym przykładzie nazwy własnych zasobów.</span><span class="sxs-lookup"><span data-stu-id="2ff7b-181">Replace the names in the example with the names of your own resources.</span></span>

    ```powershell
    $existingVnetRGName = "myResourceGroup"
    $vnetName = "myVirtualNetwork"
    $subnetName = "mySubNet"
    ```

    <span data-ttu-id="2ff7b-182">Po pierwsze sprawdzanie poprawności w przypadku migrowania sieci wirtualnej przy użyciu następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="2ff7b-182">First, validate if you can migrate the virtual network using the following command:</span></span>

    ```powershell
    $validate = Move-AzureService -Validate -ServiceName $serviceName `
        -DeploymentName $deploymentName -UseExistingVirtualNetwork -VirtualNetworkResourceGroupName $existingVnetRGName -VirtualNetworkName $vnetName -SubnetName $subnetName
    $validate.ValidationMessages
    ```

    <span data-ttu-id="2ff7b-183">Poprzednie polecenie wyświetla wszystkie ostrzeżenia i błędy, które blokują migracji.</span><span class="sxs-lookup"><span data-stu-id="2ff7b-183">The preceding command displays any warnings and errors that block migration.</span></span> <span data-ttu-id="2ff7b-184">Jeśli weryfikacja zakończy się pomyślnie, można przejść z następujący krok przygotowania:</span><span class="sxs-lookup"><span data-stu-id="2ff7b-184">If validation is successful, then you can proceed with the following Prepare step:</span></span>

    ```powershell
        Move-AzureService -Prepare -ServiceName $serviceName -DeploymentName $deploymentName `
        -UseExistingVirtualNetwork -VirtualNetworkResourceGroupName $existingVnetRGName `
        -VirtualNetworkName $vnetName -SubnetName $subnetName
    ```

<span data-ttu-id="2ff7b-185">Po operacji Prepare powiedzie się przy użyciu jednej z tych opcji, sprawdzania stanu migracji maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="2ff7b-185">After the Prepare operation succeeds with either of the preceding options, query the migration state of the VMs.</span></span> <span data-ttu-id="2ff7b-186">Upewnij się, że są one `Prepared` stanu.</span><span class="sxs-lookup"><span data-stu-id="2ff7b-186">Ensure that they are in the `Prepared` state.</span></span>

<span data-ttu-id="2ff7b-187">W tym przykładzie nazwa maszyny Wirtualnej **myVM**.</span><span class="sxs-lookup"><span data-stu-id="2ff7b-187">This example sets the VM name to **myVM**.</span></span> <span data-ttu-id="2ff7b-188">Przykładowa nazwa należy zastąpić nazwę maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2ff7b-188">Replace the example name with your own VM name.</span></span>

```powershell
    $vmName = "myVM"
    $vm = Get-AzureVM -ServiceName $serviceName -Name $vmName
    $vm.VM.MigrationState
```

<span data-ttu-id="2ff7b-189">Sprawdź konfigurację dla zasobów przygotowanego przy użyciu programu PowerShell lub w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="2ff7b-189">Check the configuration for the prepared resources by using either PowerShell or the Azure portal.</span></span> <span data-ttu-id="2ff7b-190">Jeśli chcesz powrócić do poprzedni stan nie jest jeszcze gotowa do migracji, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="2ff7b-190">If you are not ready for migration and you want to go back to the old state, use the following command:</span></span>

```powershell
    Move-AzureService -Abort -ServiceName $serviceName -DeploymentName $deploymentName
```

<span data-ttu-id="2ff7b-191">Jeśli przygotowane Konfiguracja wygląda dobrze, możesz przejść do przodu i zatwierdzić zasobów za pomocą następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="2ff7b-191">If the prepared configuration looks good, you can move forward and commit the resources by using the following command:</span></span>

```powershell
    Move-AzureService -Commit -ServiceName $serviceName -DeploymentName $deploymentName
```

## <a name="step-61-option-2---migrate-virtual-machines-in-a-virtual-network"></a><span data-ttu-id="2ff7b-192">Krok 6.1: Opcja 2 — migracji maszyn wirtualnych w sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="2ff7b-192">Step 6.1: Option 2 - Migrate virtual machines in a virtual network</span></span>

<span data-ttu-id="2ff7b-193">Aby dokonać migracji maszyn wirtualnych w sieci wirtualnej, należy przeprowadzić migrację sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2ff7b-193">To migrate virtual machines in a virtual network, you migrate the virtual network.</span></span> <span data-ttu-id="2ff7b-194">Maszyny wirtualne są automatycznie migracji z siecią wirtualną.</span><span class="sxs-lookup"><span data-stu-id="2ff7b-194">The virtual machines automatically migrate with the virtual network.</span></span> <span data-ttu-id="2ff7b-195">Wybierz sieć wirtualną, która mają zostać zmigrowane.</span><span class="sxs-lookup"><span data-stu-id="2ff7b-195">Pick the virtual network that you want to migrate.</span></span>
> [!NOTE]
> <span data-ttu-id="2ff7b-196">[Przeprowadź migrację jednej maszyny wirtualnej klasycznego](migrate-single-classic-to-resource-manager.md) przez utworzenie nowej maszyny wirtualnej usługi Resource Manager z dyskami zarządzane przy użyciu plików wirtualnego dysku twardego (systemu operacyjnego i danych) maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2ff7b-196">[Migrate single classic virtual machine](migrate-single-classic-to-resource-manager.md) by creating a new Resource Manager virtual machine with Managed Disks using the VHD (OS and data) files of the virtual machine.</span></span>
<br>

> [!NOTE]
> <span data-ttu-id="2ff7b-197">Nazwa sieci wirtualnej mogą się różnić od przedstawionego w nowego portalu.</span><span class="sxs-lookup"><span data-stu-id="2ff7b-197">The virtual network name might be different from what is shown in the new Portal.</span></span> <span data-ttu-id="2ff7b-198">Nowy Portal Azure zawiera nazwę jako `[vnet-name]` , ale nazwa rzeczywista sieci wirtualnej jest typu `Group [resource-group-name] [vnet-name]`.</span><span class="sxs-lookup"><span data-stu-id="2ff7b-198">The new Azure Portal displays the name as `[vnet-name]` but the actual virtual network name is of type `Group [resource-group-name] [vnet-name]`.</span></span> <span data-ttu-id="2ff7b-199">Przed migracją, wyszukiwanie nazwy sieci wirtualnych za pomocą polecenia `Get-AzureVnetSite | Select -Property Name` lub wyświetlić w portalu Azure stary.</span><span class="sxs-lookup"><span data-stu-id="2ff7b-199">Before migrating, lookup the actual virtual network name using the command `Get-AzureVnetSite | Select -Property Name` or view it in the old Azure Portal.</span></span> 

<span data-ttu-id="2ff7b-200">W tym przykładzie nazwa sieci wirtualnej **myVnet**.</span><span class="sxs-lookup"><span data-stu-id="2ff7b-200">This example sets the virtual network name to **myVnet**.</span></span> <span data-ttu-id="2ff7b-201">Przykładowa nazwa sieci wirtualnej należy zastąpić własnymi.</span><span class="sxs-lookup"><span data-stu-id="2ff7b-201">Replace the example virtual network name with your own.</span></span>

```powershell
    $vnetName = "myVnet"
```

> [!NOTE]
> <span data-ttu-id="2ff7b-202">Jeśli sieć wirtualna zawiera sieci web lub roli proces roboczy lub maszyn wirtualnych z nieobsługiwaną konfiguracją, otrzymasz komunikat o błędzie weryfikacji.</span><span class="sxs-lookup"><span data-stu-id="2ff7b-202">If the virtual network contains web or worker roles, or VMs with unsupported configurations, you get a validation error message.</span></span>
>
>

<span data-ttu-id="2ff7b-203">Po pierwsze sprawdzanie poprawności w przypadku migrowania sieci wirtualnej przy użyciu następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="2ff7b-203">First, validate if you can migrate the virtual network by using the following command:</span></span>

```powershell
    Move-AzureVirtualNetwork -Validate -VirtualNetworkName $vnetName
```

<span data-ttu-id="2ff7b-204">Poprzednie polecenie wyświetla wszystkie ostrzeżenia i błędy, które blokują migracji.</span><span class="sxs-lookup"><span data-stu-id="2ff7b-204">The preceding command displays any warnings and errors that block migration.</span></span> <span data-ttu-id="2ff7b-205">Jeśli weryfikacja zakończy się pomyślnie, można przejść z następujący krok przygotowania:</span><span class="sxs-lookup"><span data-stu-id="2ff7b-205">If validation is successful, then you can proceed with the following Prepare step:</span></span>

```powershell
    Move-AzureVirtualNetwork -Prepare -VirtualNetworkName $vnetName
```

<span data-ttu-id="2ff7b-206">Sprawdź konfigurację przygotować maszyn wirtualnych przy użyciu programu Azure PowerShell lub w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="2ff7b-206">Check the configuration for the prepared virtual machines by using either Azure PowerShell or the Azure portal.</span></span> <span data-ttu-id="2ff7b-207">Jeśli chcesz powrócić do poprzedni stan nie jest jeszcze gotowa do migracji, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="2ff7b-207">If you are not ready for migration and you want to go back to the old state, use the following command:</span></span>

```powershell
    Move-AzureVirtualNetwork -Abort -VirtualNetworkName $vnetName
```

<span data-ttu-id="2ff7b-208">Jeśli przygotowane Konfiguracja wygląda dobrze, możesz przejść do przodu i zatwierdzić zasobów za pomocą następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="2ff7b-208">If the prepared configuration looks good, you can move forward and commit the resources by using the following command:</span></span>

```powershell
    Move-AzureVirtualNetwork -Commit -VirtualNetworkName $vnetName
```

## <a name="step-62-migrate-a-storage-account"></a><span data-ttu-id="2ff7b-209">Krok 6.2 migracji konta magazynu</span><span class="sxs-lookup"><span data-stu-id="2ff7b-209">Step 6.2 Migrate a storage account</span></span>
<span data-ttu-id="2ff7b-210">Po zakończeniu migracji maszyn wirtualnych, firma Microsoft zaleca migracji kont magazynu.</span><span class="sxs-lookup"><span data-stu-id="2ff7b-210">Once you're done migrating the virtual machines, we recommend you migrate the storage accounts.</span></span>

<span data-ttu-id="2ff7b-211">Przed przeprowadzeniem migracji konta magazynu, należy wykonać przed wymagań wstępnych:</span><span class="sxs-lookup"><span data-stu-id="2ff7b-211">Before you migrate the storage account, please perform preceding prerequisite checks:</span></span>

* <span data-ttu-id="2ff7b-212">**Migrowanie klasycznych maszyn wirtualnych, których dyski są przechowywane na koncie magazynu**</span><span class="sxs-lookup"><span data-stu-id="2ff7b-212">**Migrate classic virtual machines whose disks are stored in the storage account**</span></span>

    <span data-ttu-id="2ff7b-213">Poprzedzających polecenie zwraca RoleName i DiskName właściwości wszystkich klasycznego dysków maszyny Wirtualnej na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="2ff7b-213">Preceding command returns RoleName and DiskName properties of all the classic VM disks in the storage account.</span></span> <span data-ttu-id="2ff7b-214">RoleName jest nazwa maszyny wirtualnej, do której jest dołączona dysku.</span><span class="sxs-lookup"><span data-stu-id="2ff7b-214">RoleName is the name of the virtual machine to which a disk is attached.</span></span> <span data-ttu-id="2ff7b-215">Jeśli poprzedzających polecenie zwraca dysków następnie upewnij się, że maszyn wirtualnych, do których są dołączone dyski te są migrowane przed przeprowadzeniem migracji konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="2ff7b-215">If preceding command returns disks then ensure that virtual machines to which these disks are attached are migrated before migrating the storage account.</span></span>
    ```powershell
     $storageAccountName = 'yourStorageAccountName'
      Get-AzureDisk | where-Object {$_.MediaLink.Host.Contains($storageAccountName)} | Select-Object -ExpandProperty AttachedTo -Property `
      DiskName | Format-List -Property RoleName, DiskName

    ```
* <span data-ttu-id="2ff7b-216">**Usuń niedołączonej klasycznego dyski maszyn wirtualnych przechowywanych w ramach konta magazynu**</span><span class="sxs-lookup"><span data-stu-id="2ff7b-216">**Delete unattached classic VM disks stored in the storage account**</span></span>

    <span data-ttu-id="2ff7b-217">Find niedołączonej klasycznego dysków maszyny Wirtualnej w magazynie konta przy użyciu następujących poleceń:</span><span class="sxs-lookup"><span data-stu-id="2ff7b-217">Find unattached classic VM disks in the storage account using following command:</span></span>

    ```powershell
        $storageAccountName = 'yourStorageAccountName'
        Get-AzureDisk | where-Object {$_.MediaLink.Host.Contains($storageAccountName)} | Where-Object -Property AttachedTo -EQ $null | Format-List -Property DiskName  

    ```
    <span data-ttu-id="2ff7b-218">Jeśli powyżej polecenie zwraca dysków Usuń te dyski za pomocą następujących poleceń:</span><span class="sxs-lookup"><span data-stu-id="2ff7b-218">If above command returns disks then delete these disks using following command:</span></span>

    ```powershell
       Remove-AzureDisk -DiskName 'yourDiskName'
    ```
* <span data-ttu-id="2ff7b-219">**Usuwanie obrazów maszyn wirtualnych przechowywanych w ramach konta magazynu**</span><span class="sxs-lookup"><span data-stu-id="2ff7b-219">**Delete VM images stored in the storage account**</span></span>

    <span data-ttu-id="2ff7b-220">Poprzedzających polecenie zwraca wszystkie obrazy maszyny Wirtualnej z dyskiem systemu operacyjnego przechowywane na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="2ff7b-220">Preceding command returns all the VM images with OS disk stored in the storage account.</span></span>
     ```powershell
        Get-AzureVmImage | Where-Object { $_.OSDiskConfiguration.MediaLink -ne $null -and $_.OSDiskConfiguration.MediaLink.Host.Contains($storageAccountName)`
                                } | Select-Object -Property ImageName, ImageLabel
     ```
     <span data-ttu-id="2ff7b-221">Poprzedzających polecenie zwraca wszystkie obrazy maszyny Wirtualnej z dyskami danych przechowywanych w ramach konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="2ff7b-221">Preceding command returns all the VM images with data disks stored in the storage account.</span></span>
     ```powershell

        Get-AzureVmImage | Where-Object {$_.DataDiskConfigurations -ne $null `
                                         -and ($_.DataDiskConfigurations | Where-Object {$_.MediaLink -ne $null -and $_.MediaLink.Host.Contains($storageAccountName)}).Count -gt 0 `
                                        } | Select-Object -Property ImageName, ImageLabel
     ```
    <span data-ttu-id="2ff7b-222">Usuń wszystkie obrazy maszyny Wirtualnej zwrócony przez powyżej poleceń przy użyciu poprzedniego polecenia:</span><span class="sxs-lookup"><span data-stu-id="2ff7b-222">Delete all the VM images returned by above commands using preceding command:</span></span>
    ```powershell
    Remove-AzureVMImage -ImageName 'yourImageName'
    ```

<span data-ttu-id="2ff7b-223">Sprawdzanie poprawności każdego konta magazynu, migracji za pomocą następującego polecenia.</span><span class="sxs-lookup"><span data-stu-id="2ff7b-223">Validate each storage account for migration by using the following command.</span></span> <span data-ttu-id="2ff7b-224">W tym przykładzie nazwa konta magazynu jest **Mojekontomagazynu**.</span><span class="sxs-lookup"><span data-stu-id="2ff7b-224">In this example, the storage account name is **myStorageAccount**.</span></span> <span data-ttu-id="2ff7b-225">Przykładowa nazwa należy zastąpić nazwę konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="2ff7b-225">Replace the example name with the name of your own storage account.</span></span>

```powershell
    $storageAccountName = "myStorageAccount"
    Move-AzureStorageAccount -Validate -StorageAccountName $storageAccountName
```

<span data-ttu-id="2ff7b-226">Następnym krokiem jest przygotowania do migracji konta magazynu</span><span class="sxs-lookup"><span data-stu-id="2ff7b-226">Next step is to Prepare the storage account for migration</span></span>

```powershell
    $storageAccountName = "myStorageAccount"
    Move-AzureStorageAccount -Prepare -StorageAccountName $storageAccountName
```

<span data-ttu-id="2ff7b-227">Sprawdź konfigurację dla konta magazynu przygotowanego przy użyciu programu Azure PowerShell lub w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="2ff7b-227">Check the configuration for the prepared storage account by using either Azure PowerShell or the Azure portal.</span></span> <span data-ttu-id="2ff7b-228">Jeśli chcesz powrócić do poprzedni stan nie jest jeszcze gotowa do migracji, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="2ff7b-228">If you are not ready for migration and you want to go back to the old state, use the following command:</span></span>

```powershell
    Move-AzureStorageAccount -Abort -StorageAccountName $storageAccountName
```

<span data-ttu-id="2ff7b-229">Jeśli przygotowane Konfiguracja wygląda dobrze, możesz przejść do przodu i zatwierdzić zasobów za pomocą następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="2ff7b-229">If the prepared configuration looks good, you can move forward and commit the resources by using the following command:</span></span>

```powershell
    Move-AzureStorageAccount -Commit -StorageAccountName $storageAccountName
```

## <a name="next-steps"></a><span data-ttu-id="2ff7b-230">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2ff7b-230">Next steps</span></span>
* [<span data-ttu-id="2ff7b-231">Omówienie migracji zasobów IaaS ze środowiska klasycznego do usługi Azure Resource Manager obsługiwane platformy</span><span class="sxs-lookup"><span data-stu-id="2ff7b-231">Overview of platform-supported migration of IaaS resources from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="2ff7b-232">Techniczne szczegółowe informacje na temat obsługiwanych platform migracji ze środowiska klasycznego do usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2ff7b-232">Technical deep dive on platform-supported migration from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="2ff7b-233">Planowanie migracji zasobów rozwiązania IaaS z wdrożenia klasycznego do usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2ff7b-233">Planning for migration of IaaS resources from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="2ff7b-234">Migracja zasobów IaaS ze środowiska klasycznego do usługi Azure Resource Manager za pomocą interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="2ff7b-234">Use CLI to migrate IaaS resources from classic to Azure Resource Manager</span></span>](../linux/migration-classic-resource-manager-cli.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="2ff7b-235">Narzędzia społeczności z migracji zasobów IaaS ze środowiska klasycznego do usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2ff7b-235">Community tools for assisting with migration of IaaS resources from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-community-tools.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="2ff7b-236">Przegląd najbardziej typowych błędów migracji</span><span class="sxs-lookup"><span data-stu-id="2ff7b-236">Review most common migration errors</span></span>](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="2ff7b-237">Przejrzyj najczęściej zadawane pytania dotyczące migrowania zasobów IaaS ze środowiska klasycznego do usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2ff7b-237">Review the most frequently asked questions about migrating IaaS resources from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
