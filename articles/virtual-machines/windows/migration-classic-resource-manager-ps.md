---
title: "tooResource aaaMigrate Manager przy użyciu programu PowerShell | Dokumentacja firmy Microsoft"
description: "W tym artykule przedstawiono hello obsługiwane platformy migracji zasobów IaaS, takich jak maszynach wirtualnych (VM), sieci wirtualnych (sieci wirtualne) oraz kont magazynu z klasycznym tooAzure Resource Manager (ARM) za pomocą poleceń programu PowerShell systemu Azure"
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
ms.openlocfilehash: b5b2987da292f1c241be71a354b0c2e1a96a07c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-iaas-resources-from-classic-tooazure-resource-manager-by-using-azure-powershell"></a><span data-ttu-id="7e2ae-103">Migracja zasobów IaaS z klasycznym tooAzure Resource Manager przy użyciu programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="7e2ae-103">Migrate IaaS resources from classic tooAzure Resource Manager by using Azure PowerShell</span></span>
<span data-ttu-id="7e2ae-104">Te kroki pokazują, jak toouse programu Azure PowerShell poleceń toomigrate infrastruktura jako usługa (IaaS) zasoby z modelu wdrażania usługi Azure Resource Manager toohello hello wdrażania klasycznego modelu.</span><span class="sxs-lookup"><span data-stu-id="7e2ae-104">These steps show you how toouse Azure PowerShell commands toomigrate infrastructure as a service (IaaS) resources from hello classic deployment model toohello Azure Resource Manager deployment model.</span></span>

<span data-ttu-id="7e2ae-105">Należy również przeprowadzić migrację zasobów za pomocą hello [interfejsu wiersza polecenia platformy Azure (Azure CLI)](../linux/migration-classic-resource-manager-cli.md).</span><span class="sxs-lookup"><span data-stu-id="7e2ae-105">If you want, you can also migrate resources by using hello [Azure Command Line Interface (Azure CLI)](../linux/migration-classic-resource-manager-cli.md).</span></span>

* <span data-ttu-id="7e2ae-106">Aby uzyskać podstawowe informacje dotyczące obsługiwanych scenariuszy migracji, zobacz [obsługiwane platformy migracji zasobów IaaS z klasycznym tooAzure Resource Manager](migration-classic-resource-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7e2ae-106">For background on supported migration scenarios, see [Platform-supported migration of IaaS resources from classic tooAzure Resource Manager](migration-classic-resource-manager-overview.md).</span></span>
* <span data-ttu-id="7e2ae-107">Aby uzyskać szczegółowe wskazówki i Przewodnik migracji, zobacz [techniczne szczegółowe informacje na temat migracji z obsługiwanych platform z klasycznym tooAzure Resource Manager](migration-classic-resource-manager-deep-dive.md).</span><span class="sxs-lookup"><span data-stu-id="7e2ae-107">For detailed guidance and a migration walkthrough, see [Technical deep dive on platform-supported migration from classic tooAzure Resource Manager](migration-classic-resource-manager-deep-dive.md).</span></span>
* [<span data-ttu-id="7e2ae-108">Przegląd najbardziej typowych błędów migracji</span><span class="sxs-lookup"><span data-stu-id="7e2ae-108">Review most common migration errors</span></span>](migration-classic-resource-manager-errors.md)

<br>
<span data-ttu-id="7e2ae-109">Poniżej przedstawiono kolejność hello tooidentify schemat blokowy, w którym kroki należy wykonać podczas procesu migracji toobe</span><span class="sxs-lookup"><span data-stu-id="7e2ae-109">Here is a flowchart tooidentify hello order in which steps need toobe executed during a migration process</span></span>

![Zrzut ekranu pokazujący hello kroków migracji](media/migration-classic-resource-manager/migration-flow.png)

## <a name="step-1-plan-for-migration"></a><span data-ttu-id="7e2ae-111">Krok 1: Planowanie migracji</span><span class="sxs-lookup"><span data-stu-id="7e2ae-111">Step 1: Plan for migration</span></span>
<span data-ttu-id="7e2ae-112">Poniżej przedstawiono kilka najlepsze rozwiązania, które firma Microsoft zaleca jako ocenić migracji zasobów IaaS z klasycznym tooResource Menedżera:</span><span class="sxs-lookup"><span data-stu-id="7e2ae-112">Here are a few best practices that we recommend as you evaluate migrating IaaS resources from classic tooResource Manager:</span></span>

* <span data-ttu-id="7e2ae-113">Zapoznaj się z artykułem hello [obsługiwane i nieobsługiwane funkcje i konfiguracje](migration-classic-resource-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7e2ae-113">Read through hello [supported and unsupported features and configurations](migration-classic-resource-manager-overview.md).</span></span> <span data-ttu-id="7e2ae-114">Jeśli masz maszyn wirtualnych, które używają nieobsługiwane konfiguracje i funkcje, firma Microsoft zaleca, poczekaj toobe obsługi funkcji/Konfiguracja hello anonsowania.</span><span class="sxs-lookup"><span data-stu-id="7e2ae-114">If you have virtual machines that use unsupported configurations or features, we recommend that you wait for hello configuration/feature support toobe announced.</span></span> <span data-ttu-id="7e2ae-115">Jeśli zgodnie z potrzebami, Usuń tej funkcji lub przenieść poza migracji tooenable tej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="7e2ae-115">Alternatively, if it suits your needs, remove that feature or move out of that configuration tooenable migration.</span></span>
* <span data-ttu-id="7e2ae-116">Jeśli mają automatyczny skrypty, które obecnie wdrażanie infrastruktury i aplikacji, spróbuj toocreate podobnych konfiguracji testu przy użyciu tych skryptów do migracji.</span><span class="sxs-lookup"><span data-stu-id="7e2ae-116">If you have automated scripts that deploy your infrastructure and applications today, try toocreate a similar test setup by using those scripts for migration.</span></span> <span data-ttu-id="7e2ae-117">Można też skonfigurować próbkę środowiskami przy użyciu hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="7e2ae-117">Alternatively, you can set up sample environments by using hello Azure portal.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7e2ae-118">Migracji z klasycznym tooResource Menedżera bramy aplikacji nie są obecnie obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="7e2ae-118">Application Gateways are not currently supported for migration from classic tooResource Manager.</span></span> <span data-ttu-id="7e2ae-119">toomigrate klasycznej sieci wirtualnej z bramy aplikacji usunąć bramę hello przed uruchomieniem operacji Prepare toomove hello sieci.</span><span class="sxs-lookup"><span data-stu-id="7e2ae-119">toomigrate a classic virtual network with an Application gateway, remove hello gateway before running a Prepare operation toomove hello network.</span></span> <span data-ttu-id="7e2ae-120">Po zakończeniu migracji hello ponownie hello bramy w usłudze Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7e2ae-120">After you complete hello migration, reconnect hello gateway in Azure Resource Manager.</span></span>
>
><span data-ttu-id="7e2ae-121">Łączenie obwody tooExpressRoute w innej subskrypcji bram usługi ExpressRoute nie może być migrowane automatycznie.</span><span class="sxs-lookup"><span data-stu-id="7e2ae-121">ExpressRoute gateways connecting tooExpressRoute circuits in another subscription cannot be migrated automatically.</span></span> <span data-ttu-id="7e2ae-122">W takiej sytuacji należy usunąć bramę usługi ExpressRoute hello, migrację sieci wirtualnej hello i Utwórz ponownie hello bramy.</span><span class="sxs-lookup"><span data-stu-id="7e2ae-122">In such cases, remove hello ExpressRoute gateway, migrate hello virtual network and recreate hello gateway.</span></span> <span data-ttu-id="7e2ae-123">Zobacz [ExpressRoute migracji obwody i skojarzone sieci wirtualne od modelu wdrażania Menedżera zasobów klasycznych toohello hello](../../expressroute/expressroute-migration-classic-resource-manager.md) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="7e2ae-123">Please see [Migrate ExpressRoute circuits and associated virtual networks from hello classic toohello Resource Manager deployment model](../../expressroute/expressroute-migration-classic-resource-manager.md) for more information.</span></span>
>
>

## <a name="step-2-install-hello-latest-version-of-azure-powershell"></a><span data-ttu-id="7e2ae-124">Krok 2: Zainstaluj najnowszą wersję hello programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="7e2ae-124">Step 2: Install hello latest version of Azure PowerShell</span></span>
<span data-ttu-id="7e2ae-125">Istnieją dwa główne opcje tooinstall programu Azure PowerShell: [galerii programu PowerShell](https://www.powershellgallery.com/profiles/azure-sdk/) lub [Instalatora platformy sieci Web (WebPI)](http://aka.ms/webpi-azps).</span><span class="sxs-lookup"><span data-stu-id="7e2ae-125">There are two main options tooinstall Azure PowerShell: [PowerShell Gallery](https://www.powershellgallery.com/profiles/azure-sdk/) or [Web Platform Installer (WebPI)](http://aka.ms/webpi-azps).</span></span> <span data-ttu-id="7e2ae-126">WebPI odbiera comiesięcznych aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="7e2ae-126">WebPI receives monthly updates.</span></span> <span data-ttu-id="7e2ae-127">Galerii programu PowerShell odbiera aktualizacje w sposób ciągły.</span><span class="sxs-lookup"><span data-stu-id="7e2ae-127">PowerShell Gallery receives updates on a continuous basis.</span></span> <span data-ttu-id="7e2ae-128">W tym artykule jest oparta na program Azure PowerShell w wersji 2.1.0.</span><span class="sxs-lookup"><span data-stu-id="7e2ae-128">This article is based on Azure PowerShell version 2.1.0.</span></span>

<span data-ttu-id="7e2ae-129">Aby uzyskać instrukcje instalacji, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7e2ae-129">For installation instructions, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<br>

## <a name="step-3-ensure-that-you-are-an-administrator-for-hello-subscription-in-azure-portal"></a><span data-ttu-id="7e2ae-130">Krok 3: Upewnij się, że jesteś administratorem subskrypcji hello w portalu Azure</span><span class="sxs-lookup"><span data-stu-id="7e2ae-130">Step 3: Ensure that you are an administrator for hello subscription in Azure portal</span></span>
<span data-ttu-id="7e2ae-131">tooperform tej migracji, musi zostać dodany jako współadministrator subskrypcji hello w hello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7e2ae-131">tooperform this migration, you must be added as a co-administrator for hello subscription in hello [Azure portal](https://portal.azure.com).</span></span>

1. <span data-ttu-id="7e2ae-132">Zaloguj się na powitania [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7e2ae-132">Sign into hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="7e2ae-133">W menu Centrum hello wybierz **subskrypcji**.</span><span class="sxs-lookup"><span data-stu-id="7e2ae-133">On hello Hub menu, select **Subscription**.</span></span> <span data-ttu-id="7e2ae-134">Jeśli nie widzisz, wybierz **więcej usług**.</span><span class="sxs-lookup"><span data-stu-id="7e2ae-134">If you don't see it, select **More services**.</span></span>
3. <span data-ttu-id="7e2ae-135">Znajdź hello subskrypcji odpowiedni wpis, a następnie przyjrzeć się hello **Moje roli** pola.</span><span class="sxs-lookup"><span data-stu-id="7e2ae-135">Find hello appropriate subscription entry, then look at hello **MY ROLE** field.</span></span> <span data-ttu-id="7e2ae-136">Dla administratora współpracującego, hello wartość powinna być _administrator konta_.</span><span class="sxs-lookup"><span data-stu-id="7e2ae-136">For a co-administrator, hello value should be _Account admin_.</span></span>

<span data-ttu-id="7e2ae-137">Jeśli nie jest możliwe tooadd współadministratorem, następnie skontaktuj się z administratorem usługi ani współadministratorem tooget subskrypcji hello dodane przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="7e2ae-137">If you are not able tooadd a co-administrator, then contact a service administrator or co-administrator for hello subscription tooget yourself added.</span></span>   

## <a name="step-4-set-your-subscription-and-sign-up-for-migration"></a><span data-ttu-id="7e2ae-138">Krok 4: Ustaw subskrypcji i zaloguj do migracji</span><span class="sxs-lookup"><span data-stu-id="7e2ae-138">Step 4: Set your subscription and sign up for migration</span></span>
<span data-ttu-id="7e2ae-139">Najpierw należy uruchomić wiersz programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7e2ae-139">First, start a PowerShell prompt.</span></span> <span data-ttu-id="7e2ae-140">W przypadku migracji należy tooset Twojego środowiska dla obu classic i Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="7e2ae-140">For migration, you need tooset up your environment for both classic and Resource Manager.</span></span>

<span data-ttu-id="7e2ae-141">Zaloguj się konta tooyour hello modelu Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7e2ae-141">Sign in tooyour account for hello Resource Manager model.</span></span>

```powershell
    Login-AzureRmAccount
```

<span data-ttu-id="7e2ae-142">Uzyskiwanie hello dostępnych subskrypcji przy użyciu hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="7e2ae-142">Get hello available subscriptions by using hello following command:</span></span>

```powershell
    Get-AzureRMSubscription | Sort Name | Select Name
```

<span data-ttu-id="7e2ae-143">Ustaw subskrypcji platformy Azure dla hello bieżącej sesji.</span><span class="sxs-lookup"><span data-stu-id="7e2ae-143">Set your Azure subscription for hello current session.</span></span> <span data-ttu-id="7e2ae-144">W tym przykładzie ustawia domyślną nazwę subskrypcji hello zbyt**moją subskrypcję Azure**.</span><span class="sxs-lookup"><span data-stu-id="7e2ae-144">This example sets hello default subscription name too**My Azure Subscription**.</span></span> <span data-ttu-id="7e2ae-145">Zamień nazwę subskrypcji przykład hello własne.</span><span class="sxs-lookup"><span data-stu-id="7e2ae-145">Replace hello example subscription name with your own.</span></span>

```powershell
    Select-AzureRmSubscription –SubscriptionName "My Azure Subscription"
```

> [!NOTE]
> <span data-ttu-id="7e2ae-146">Rejestracja jest jednorazowe krok, ale należy to robić raz przed próbą wykonania migracji.</span><span class="sxs-lookup"><span data-stu-id="7e2ae-146">Registration is a one-time step, but you must do it once before attempting migration.</span></span> <span data-ttu-id="7e2ae-147">Bez rejestrowania, zobacz temat hello następujący komunikat o błędzie:</span><span class="sxs-lookup"><span data-stu-id="7e2ae-147">Without registering, you see hello following error message:</span></span>
>
> <span data-ttu-id="7e2ae-148">*Element BadRequest: Subskrypcja nie jest zarejestrowana do migracji.*</span><span class="sxs-lookup"><span data-stu-id="7e2ae-148">*BadRequest : Subscription is not registered for migration.*</span></span>
>
>

<span data-ttu-id="7e2ae-149">Rejestracja dostawcy zasobów migracji hello za pomocą następującego polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="7e2ae-149">Register with hello migration resource provider by using hello following command:</span></span>

```powershell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
```

<span data-ttu-id="7e2ae-150">Poczekaj pięć minut hello toofinish rejestracji.</span><span class="sxs-lookup"><span data-stu-id="7e2ae-150">Please wait five minutes for hello registration toofinish.</span></span> <span data-ttu-id="7e2ae-151">Stan hello zatwierdzenia hello można sprawdzić za pomocą następującego polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="7e2ae-151">You can check hello status of hello approval by using hello following command:</span></span>

```powershell
    Get-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
```

<span data-ttu-id="7e2ae-152">Upewnij się, że jest RegistrationState `Registered` przed kontynuowaniem.</span><span class="sxs-lookup"><span data-stu-id="7e2ae-152">Make sure that RegistrationState is `Registered` before you proceed.</span></span>

<span data-ttu-id="7e2ae-153">Teraz Zaloguj się na koncie tooyour hello klasycznego modelu.</span><span class="sxs-lookup"><span data-stu-id="7e2ae-153">Now sign in tooyour account for hello classic model.</span></span>

```powershell
    Add-AzureAccount
```

<span data-ttu-id="7e2ae-154">Uzyskiwanie hello dostępnych subskrypcji przy użyciu hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="7e2ae-154">Get hello available subscriptions by using hello following command:</span></span>

```powershell
    Get-AzureSubscription | Sort SubscriptionName | Select SubscriptionName
```

<span data-ttu-id="7e2ae-155">Ustaw subskrypcji platformy Azure dla hello bieżącej sesji.</span><span class="sxs-lookup"><span data-stu-id="7e2ae-155">Set your Azure subscription for hello current session.</span></span> <span data-ttu-id="7e2ae-156">W tym przykładzie subskrypcji domyślne hello zbyt**moją subskrypcję Azure**.</span><span class="sxs-lookup"><span data-stu-id="7e2ae-156">This example sets hello default subscription too**My Azure Subscription**.</span></span> <span data-ttu-id="7e2ae-157">Zamień nazwę subskrypcji przykład hello własne.</span><span class="sxs-lookup"><span data-stu-id="7e2ae-157">Replace hello example subscription name with your own.</span></span>

```powershell
    Select-AzureSubscription –SubscriptionName "My Azure Subscription"
```

<br>

## <a name="step-5-make-sure-you-have-enough-azure-resource-manager-virtual-machine-cores-in-hello-azure-region-of-your-current-deployment-or-vnet"></a><span data-ttu-id="7e2ae-158">Krok 5: Upewnij się, że masz wystarczająco dużo rdzeni maszyny wirtualnej Azure Resource Manager w hello region platformy Azure dla bieżącego wdrożenia lub sieci Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="7e2ae-158">Step 5: Make sure you have enough Azure Resource Manager Virtual Machine cores in hello Azure region of your current deployment or VNET</span></span>
<span data-ttu-id="7e2ae-159">Możesz użyć hello następującego środowiska PowerShell polecenie toocheck hello bieżąca liczba rdzeni, do których masz usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7e2ae-159">You can use hello following PowerShell command toocheck hello current number of cores you have in Azure Resource Manager.</span></span> <span data-ttu-id="7e2ae-160">toolearn więcej informacji na temat przydziały core, zobacz [limity i hello Azure Resource Manager](../../azure-subscription-service-limits.md#limits-and-the-azure-resource-manager).</span><span class="sxs-lookup"><span data-stu-id="7e2ae-160">toolearn more about core quotas, see [Limits and hello Azure Resource Manager](../../azure-subscription-service-limits.md#limits-and-the-azure-resource-manager).</span></span>

<span data-ttu-id="7e2ae-161">W tym przykładzie służy do sprawdzania dostępności hello hello **zachodnie stany USA** regionu.</span><span class="sxs-lookup"><span data-stu-id="7e2ae-161">This example checks hello availability in hello **West US** region.</span></span> <span data-ttu-id="7e2ae-162">Zamień nazwę regionu przykład hello własne.</span><span class="sxs-lookup"><span data-stu-id="7e2ae-162">Replace hello example region name with your own.</span></span>

```powershell
Get-AzureRmVMUsage -Location "West US"
```

## <a name="step-6-run-commands-toomigrate-your-iaas-resources"></a><span data-ttu-id="7e2ae-163">Krok 6: Uruchamianie poleceń toomigrate zasobów IaaS</span><span class="sxs-lookup"><span data-stu-id="7e2ae-163">Step 6: Run commands toomigrate your IaaS resources</span></span>
> [!NOTE]
> <span data-ttu-id="7e2ae-164">Wszystkie operacje hello opisane w tym miejscu są idempotentności.</span><span class="sxs-lookup"><span data-stu-id="7e2ae-164">All hello operations described here are idempotent.</span></span> <span data-ttu-id="7e2ae-165">Jeśli masz problem niż nieobsługiwanej funkcji lub błąd konfiguracji, zalecamy możesz ponowić próbę hello przygotowanie, przerwania lub przekazania operacji.</span><span class="sxs-lookup"><span data-stu-id="7e2ae-165">If you have a problem other than an unsupported feature or a configuration error, we recommend that you retry hello prepare, abort, or commit operation.</span></span> <span data-ttu-id="7e2ae-166">Platforma Hello próbuje hello akcję ponownie.</span><span class="sxs-lookup"><span data-stu-id="7e2ae-166">hello platform then tries hello action again.</span></span>
>
>

## <a name="step-61-option-1---migrate-virtual-machines-in-a-cloud-service-not-in-a-virtual-network"></a><span data-ttu-id="7e2ae-167">Krok 6.1: Opcja 1 — migracji maszyn wirtualnych w usłudze w chmurze (nie w sieci wirtualnej)</span><span class="sxs-lookup"><span data-stu-id="7e2ae-167">Step 6.1: Option 1 - Migrate virtual machines in a cloud service (not in a virtual network)</span></span>
<span data-ttu-id="7e2ae-168">Pobranie listy hello usługi w chmurze przy użyciu hello następujące polecenie, a następnie usługa w chmurze hello pobrania, które mają toomigrate.</span><span class="sxs-lookup"><span data-stu-id="7e2ae-168">Get hello list of cloud services by using hello following command, and then pick hello cloud service that you want toomigrate.</span></span> <span data-ttu-id="7e2ae-169">Jeśli hello maszyn wirtualnych w usłudze w chmurze hello znajdują się w sieci wirtualnej lub mają one role sieci web lub procesu roboczego, hello polecenie zwróci komunikat o błędzie.</span><span class="sxs-lookup"><span data-stu-id="7e2ae-169">If hello VMs in hello cloud service are in a virtual network or if they have web or worker roles, hello command returns an error message.</span></span>

```powershell
    Get-AzureService | ft Servicename
```

<span data-ttu-id="7e2ae-170">Pobierz hello Nazwa wdrożenia dla usługi w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="7e2ae-170">Get hello deployment name for hello cloud service.</span></span> <span data-ttu-id="7e2ae-171">W tym przykładzie nazwa usługi hello jest **Moje usługi**.</span><span class="sxs-lookup"><span data-stu-id="7e2ae-171">In this example, hello service name is **My Service**.</span></span> <span data-ttu-id="7e2ae-172">Nazwa usługi przykład hello należy zastąpić nazwę usługi.</span><span class="sxs-lookup"><span data-stu-id="7e2ae-172">Replace hello example service name with your own service name.</span></span>

```powershell
    $serviceName = "My Service"
    $deployment = Get-AzureDeployment -ServiceName $serviceName
    $deploymentName = $deployment.DeploymentName
```

<span data-ttu-id="7e2ae-173">Przygotuj maszyny wirtualne hello hello w usłudze w chmurze do migracji.</span><span class="sxs-lookup"><span data-stu-id="7e2ae-173">Prepare hello virtual machines in hello cloud service for migration.</span></span> <span data-ttu-id="7e2ae-174">Masz dwie opcje toochoose z.</span><span class="sxs-lookup"><span data-stu-id="7e2ae-174">You have two options toochoose from.</span></span>

* <span data-ttu-id="7e2ae-175">**Opcja 1. Migrowanie hello maszyn wirtualnych tooa utworzone platformy sieci wirtualnej**</span><span class="sxs-lookup"><span data-stu-id="7e2ae-175">**Option 1. Migrate hello VMs tooa platform-created virtual network**</span></span>

    <span data-ttu-id="7e2ae-176">Po pierwsze sprawdzanie poprawności w przypadku migrowania usługi w chmurze hello za pomocą następującego polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="7e2ae-176">First, validate if you can migrate hello cloud service using hello following commands:</span></span>

    ```powershell
    $validate = Move-AzureService -Validate -ServiceName $serviceName `
        -DeploymentName $deploymentName -CreateNewVirtualNetwork
    $validate.ValidationMessages
    ```

    <span data-ttu-id="7e2ae-177">Witaj poprzednie polecenie wyświetla wszystkie ostrzeżenia i błędy, które blokują migracji.</span><span class="sxs-lookup"><span data-stu-id="7e2ae-177">hello preceding command displays any warnings and errors that block migration.</span></span> <span data-ttu-id="7e2ae-178">Jeśli weryfikacja zakończy się pomyślnie, a następnie można przenieść na toohello **Prepare** krok:</span><span class="sxs-lookup"><span data-stu-id="7e2ae-178">If validation is successful, then you can move on toohello **Prepare** step:</span></span>

    ```powershell
    Move-AzureService -Prepare -ServiceName $serviceName `
        -DeploymentName $deploymentName -CreateNewVirtualNetwork
    ```
* <span data-ttu-id="7e2ae-179">**Opcja 2. Migrowanie tooan istniejącej sieci wirtualnej w modelu wdrażania usługi Resource Manager hello**</span><span class="sxs-lookup"><span data-stu-id="7e2ae-179">**Option 2. Migrate tooan existing virtual network in hello Resource Manager deployment model**</span></span>

    <span data-ttu-id="7e2ae-180">W tym przykładzie zestawy hello Nazwa grupy zasobów zbyt**myResourceGroup**, zbyt hello wirtualnej nazwy sieciowej**myVirtualNetwork** i hello nazwy podsieci za**mySubNet**.</span><span class="sxs-lookup"><span data-stu-id="7e2ae-180">This example sets hello resource group name too**myResourceGroup**, hello virtual network name too**myVirtualNetwork** and hello subnet name too**mySubNet**.</span></span> <span data-ttu-id="7e2ae-181">Zamień nazwy hello w przykładzie hello hello nazw własnych zasobów.</span><span class="sxs-lookup"><span data-stu-id="7e2ae-181">Replace hello names in hello example with hello names of your own resources.</span></span>

    ```powershell
    $existingVnetRGName = "myResourceGroup"
    $vnetName = "myVirtualNetwork"
    $subnetName = "mySubNet"
    ```

    <span data-ttu-id="7e2ae-182">Po pierwsze sprawdzanie poprawności w przypadku migrowania hello sieci wirtualnej przy użyciu hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="7e2ae-182">First, validate if you can migrate hello virtual network using hello following command:</span></span>

    ```powershell
    $validate = Move-AzureService -Validate -ServiceName $serviceName `
        -DeploymentName $deploymentName -UseExistingVirtualNetwork -VirtualNetworkResourceGroupName $existingVnetRGName -VirtualNetworkName $vnetName -SubnetName $subnetName
    $validate.ValidationMessages
    ```

    <span data-ttu-id="7e2ae-183">Witaj poprzednie polecenie wyświetla wszystkie ostrzeżenia i błędy, które blokują migracji.</span><span class="sxs-lookup"><span data-stu-id="7e2ae-183">hello preceding command displays any warnings and errors that block migration.</span></span> <span data-ttu-id="7e2ae-184">Jeśli weryfikacja zakończy się pomyślnie, można przejść z powitania po kroku:</span><span class="sxs-lookup"><span data-stu-id="7e2ae-184">If validation is successful, then you can proceed with hello following Prepare step:</span></span>

    ```powershell
        Move-AzureService -Prepare -ServiceName $serviceName -DeploymentName $deploymentName `
        -UseExistingVirtualNetwork -VirtualNetworkResourceGroupName $existingVnetRGName `
        -VirtualNetworkName $vnetName -SubnetName $subnetName
    ```

<span data-ttu-id="7e2ae-185">Po hello operacji Prepare powiedzie się przy użyciu jednej z hello poprzedzających opcji, należy zbadać stanu migracji hello hello maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="7e2ae-185">After hello Prepare operation succeeds with either of hello preceding options, query hello migration state of hello VMs.</span></span> <span data-ttu-id="7e2ae-186">Upewnij się, że są one hello `Prepared` stanu.</span><span class="sxs-lookup"><span data-stu-id="7e2ae-186">Ensure that they are in hello `Prepared` state.</span></span>

<span data-ttu-id="7e2ae-187">W tym przykładzie zestawy hello nazwę maszyny Wirtualnej za**myVM**.</span><span class="sxs-lookup"><span data-stu-id="7e2ae-187">This example sets hello VM name too**myVM**.</span></span> <span data-ttu-id="7e2ae-188">Zastąp nazwę przykład hello nazwę maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="7e2ae-188">Replace hello example name with your own VM name.</span></span>

```powershell
    $vmName = "myVM"
    $vm = Get-AzureVM -ServiceName $serviceName -Name $vmName
    $vm.VM.MigrationState
```

<span data-ttu-id="7e2ae-189">Sprawdź konfigurację hello hello przygotowany zasobów przy użyciu programu PowerShell lub hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="7e2ae-189">Check hello configuration for hello prepared resources by using either PowerShell or hello Azure portal.</span></span> <span data-ttu-id="7e2ae-190">Jeśli nie jest jeszcze gotowa do migracji i ma toogo toohello wstecz poprzedni stan, użyj hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="7e2ae-190">If you are not ready for migration and you want toogo back toohello old state, use hello following command:</span></span>

```powershell
    Move-AzureService -Abort -ServiceName $serviceName -DeploymentName $deploymentName
```

<span data-ttu-id="7e2ae-191">Jeśli hello przygotowane Konfiguracja wygląda dobrze, możesz przejść do przodu i zatwierdzić hello zasobów za pomocą następującego polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="7e2ae-191">If hello prepared configuration looks good, you can move forward and commit hello resources by using hello following command:</span></span>

```powershell
    Move-AzureService -Commit -ServiceName $serviceName -DeploymentName $deploymentName
```

## <a name="step-61-option-2---migrate-virtual-machines-in-a-virtual-network"></a><span data-ttu-id="7e2ae-192">Krok 6.1: Opcja 2 — migracji maszyn wirtualnych w sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="7e2ae-192">Step 6.1: Option 2 - Migrate virtual machines in a virtual network</span></span>

<span data-ttu-id="7e2ae-193">maszyny wirtualne toomigrate w sieci wirtualnej, migracja hello sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="7e2ae-193">toomigrate virtual machines in a virtual network, you migrate hello virtual network.</span></span> <span data-ttu-id="7e2ae-194">maszyny wirtualne Hello automatycznie migracji z hello sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="7e2ae-194">hello virtual machines automatically migrate with hello virtual network.</span></span> <span data-ttu-id="7e2ae-195">Pobranie hello sieci wirtualnej, które mają toomigrate.</span><span class="sxs-lookup"><span data-stu-id="7e2ae-195">Pick hello virtual network that you want toomigrate.</span></span>
> [!NOTE]
> <span data-ttu-id="7e2ae-196">[Przeprowadź migrację jednej maszyny wirtualnej klasycznego](migrate-single-classic-to-resource-manager.md) przez utworzenie nowej maszyny wirtualnej usługi Resource Manager z dyskami zarządzane przy użyciu hello plików (systemu operacyjnego i danych) wirtualnego dysku twardego hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="7e2ae-196">[Migrate single classic virtual machine](migrate-single-classic-to-resource-manager.md) by creating a new Resource Manager virtual machine with Managed Disks using hello VHD (OS and data) files of hello virtual machine.</span></span>
<br>

> [!NOTE]
> <span data-ttu-id="7e2ae-197">Nazwa sieci wirtualnej Hello mogą się różnić od co przedstawiono na powitania nowego portalu.</span><span class="sxs-lookup"><span data-stu-id="7e2ae-197">hello virtual network name might be different from what is shown in hello new Portal.</span></span> <span data-ttu-id="7e2ae-198">Witaj nowego portalu Azure Wyświetla hello nazwę jako `[vnet-name]` , ale nazwa rzeczywista sieci wirtualnej hello jest typu `Group [resource-group-name] [vnet-name]`.</span><span class="sxs-lookup"><span data-stu-id="7e2ae-198">hello new Azure Portal displays hello name as `[vnet-name]` but hello actual virtual network name is of type `Group [resource-group-name] [vnet-name]`.</span></span> <span data-ttu-id="7e2ae-199">Przed migracją wyszukiwania hello rzeczywiste wirtualnej nazwy sieciowej przy użyciu polecenia hello `Get-AzureVnetSite | Select -Property Name` lub wyświetlania w hello starego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="7e2ae-199">Before migrating, lookup hello actual virtual network name using hello command `Get-AzureVnetSite | Select -Property Name` or view it in hello old Azure Portal.</span></span> 

<span data-ttu-id="7e2ae-200">W tym przykładzie zestawy hello wirtualnej nazwy sieciowej zbyt**myVnet**.</span><span class="sxs-lookup"><span data-stu-id="7e2ae-200">This example sets hello virtual network name too**myVnet**.</span></span> <span data-ttu-id="7e2ae-201">Zamień nazwę sieci wirtualnej przykład hello własne.</span><span class="sxs-lookup"><span data-stu-id="7e2ae-201">Replace hello example virtual network name with your own.</span></span>

```powershell
    $vnetName = "myVnet"
```

> [!NOTE]
> <span data-ttu-id="7e2ae-202">Jeśli sieć wirtualna hello zawiera sieci web lub roli proces roboczy lub maszyn wirtualnych z nieobsługiwaną konfiguracją, otrzymasz komunikat o błędzie weryfikacji.</span><span class="sxs-lookup"><span data-stu-id="7e2ae-202">If hello virtual network contains web or worker roles, or VMs with unsupported configurations, you get a validation error message.</span></span>
>
>

<span data-ttu-id="7e2ae-203">Po pierwsze sprawdzanie poprawności w przypadku migrowania hello sieci wirtualnej przy użyciu następującego polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="7e2ae-203">First, validate if you can migrate hello virtual network by using hello following command:</span></span>

```powershell
    Move-AzureVirtualNetwork -Validate -VirtualNetworkName $vnetName
```

<span data-ttu-id="7e2ae-204">Witaj poprzednie polecenie wyświetla wszystkie ostrzeżenia i błędy, które blokują migracji.</span><span class="sxs-lookup"><span data-stu-id="7e2ae-204">hello preceding command displays any warnings and errors that block migration.</span></span> <span data-ttu-id="7e2ae-205">Jeśli weryfikacja zakończy się pomyślnie, można przejść z powitania po kroku:</span><span class="sxs-lookup"><span data-stu-id="7e2ae-205">If validation is successful, then you can proceed with hello following Prepare step:</span></span>

```powershell
    Move-AzureVirtualNetwork -Prepare -VirtualNetworkName $vnetName
```

<span data-ttu-id="7e2ae-206">Sprawdź konfigurację hello hello przygotowany maszyn wirtualnych przy użyciu programu Azure PowerShell lub hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="7e2ae-206">Check hello configuration for hello prepared virtual machines by using either Azure PowerShell or hello Azure portal.</span></span> <span data-ttu-id="7e2ae-207">Jeśli nie jest jeszcze gotowa do migracji i ma toogo toohello wstecz poprzedni stan, użyj hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="7e2ae-207">If you are not ready for migration and you want toogo back toohello old state, use hello following command:</span></span>

```powershell
    Move-AzureVirtualNetwork -Abort -VirtualNetworkName $vnetName
```

<span data-ttu-id="7e2ae-208">Jeśli hello przygotowane Konfiguracja wygląda dobrze, możesz przejść do przodu i zatwierdzić hello zasobów za pomocą następującego polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="7e2ae-208">If hello prepared configuration looks good, you can move forward and commit hello resources by using hello following command:</span></span>

```powershell
    Move-AzureVirtualNetwork -Commit -VirtualNetworkName $vnetName
```

## <a name="step-62-migrate-a-storage-account"></a><span data-ttu-id="7e2ae-209">Krok 6.2 migracji konta magazynu</span><span class="sxs-lookup"><span data-stu-id="7e2ae-209">Step 6.2 Migrate a storage account</span></span>
<span data-ttu-id="7e2ae-210">Po zakończeniu migracji maszyn wirtualnych hello, zaleca się migrowanie hello kont magazynu.</span><span class="sxs-lookup"><span data-stu-id="7e2ae-210">Once you're done migrating hello virtual machines, we recommend you migrate hello storage accounts.</span></span>

<span data-ttu-id="7e2ae-211">Przed przeprowadzeniem migracji konta magazynu hello, należy wykonać przed wymagań wstępnych:</span><span class="sxs-lookup"><span data-stu-id="7e2ae-211">Before you migrate hello storage account, please perform preceding prerequisite checks:</span></span>

* <span data-ttu-id="7e2ae-212">**Migrowanie klasycznych maszyn wirtualnych, których dyski są przechowywane na koncie magazynu hello**</span><span class="sxs-lookup"><span data-stu-id="7e2ae-212">**Migrate classic virtual machines whose disks are stored in hello storage account**</span></span>

    <span data-ttu-id="7e2ae-213">Poprzedzających polecenie zwraca RoleName i DiskName właściwości wszystkich dysków maszyny Wirtualnej z klasycznym hello hello konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="7e2ae-213">Preceding command returns RoleName and DiskName properties of all hello classic VM disks in hello storage account.</span></span> <span data-ttu-id="7e2ae-214">RoleName jest nazwa hello hello toowhich maszynę wirtualną, której jest dołączona dysku.</span><span class="sxs-lookup"><span data-stu-id="7e2ae-214">RoleName is hello name of hello virtual machine toowhich a disk is attached.</span></span> <span data-ttu-id="7e2ae-215">Jeśli poprzedzających polecenie zwraca dysków upewnij się, że toowhich maszyny wirtualne są dołączone dyski te są migrowane przed migracją hello konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="7e2ae-215">If preceding command returns disks then ensure that virtual machines toowhich these disks are attached are migrated before migrating hello storage account.</span></span>
    ```powershell
     $storageAccountName = 'yourStorageAccountName'
      Get-AzureDisk | where-Object {$_.MediaLink.Host.Contains($storageAccountName)} | Select-Object -ExpandProperty AttachedTo -Property `
      DiskName | Format-List -Property RoleName, DiskName

    ```
* <span data-ttu-id="7e2ae-216">**Usuń przechowywane na koncie magazynu hello niedołączonej klasycznego dysków maszyny Wirtualnej**</span><span class="sxs-lookup"><span data-stu-id="7e2ae-216">**Delete unattached classic VM disks stored in hello storage account**</span></span>

    <span data-ttu-id="7e2ae-217">Find niedołączonej klasycznego dysków maszyny Wirtualnej w magazynie hello konta przy użyciu następujących poleceń:</span><span class="sxs-lookup"><span data-stu-id="7e2ae-217">Find unattached classic VM disks in hello storage account using following command:</span></span>

    ```powershell
        $storageAccountName = 'yourStorageAccountName'
        Get-AzureDisk | where-Object {$_.MediaLink.Host.Contains($storageAccountName)} | Where-Object -Property AttachedTo -EQ $null | Format-List -Property DiskName  

    ```
    <span data-ttu-id="7e2ae-218">Jeśli powyżej polecenie zwraca dysków Usuń te dyski za pomocą następujących poleceń:</span><span class="sxs-lookup"><span data-stu-id="7e2ae-218">If above command returns disks then delete these disks using following command:</span></span>

    ```powershell
       Remove-AzureDisk -DiskName 'yourDiskName'
    ```
* <span data-ttu-id="7e2ae-219">**Usuń maszyny Wirtualnej obrazy przechowywane na koncie magazynu hello**</span><span class="sxs-lookup"><span data-stu-id="7e2ae-219">**Delete VM images stored in hello storage account**</span></span>

    <span data-ttu-id="7e2ae-220">Poprzedzających polecenie zwraca wszystkie obrazy maszyny Wirtualnej hello dysku systemu operacyjnego przechowywanego w hello konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="7e2ae-220">Preceding command returns all hello VM images with OS disk stored in hello storage account.</span></span>
     ```powershell
        Get-AzureVmImage | Where-Object { $_.OSDiskConfiguration.MediaLink -ne $null -and $_.OSDiskConfiguration.MediaLink.Host.Contains($storageAccountName)`
                                } | Select-Object -Property ImageName, ImageLabel
     ```
     <span data-ttu-id="7e2ae-221">Poprzedzających polecenie zwraca wszystkie obrazy maszyny Wirtualnej hello z dyskami danych przechowywane na koncie magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="7e2ae-221">Preceding command returns all hello VM images with data disks stored in hello storage account.</span></span>
     ```powershell

        Get-AzureVmImage | Where-Object {$_.DataDiskConfigurations -ne $null `
                                         -and ($_.DataDiskConfigurations | Where-Object {$_.MediaLink -ne $null -and $_.MediaLink.Host.Contains($storageAccountName)}).Count -gt 0 `
                                        } | Select-Object -Property ImageName, ImageLabel
     ```
    <span data-ttu-id="7e2ae-222">Usuń wszystkie obrazy maszyny Wirtualnej hello zwrócony przez powyżej poleceń przy użyciu poprzedniego polecenia:</span><span class="sxs-lookup"><span data-stu-id="7e2ae-222">Delete all hello VM images returned by above commands using preceding command:</span></span>
    ```powershell
    Remove-AzureVMImage -ImageName 'yourImageName'
    ```

<span data-ttu-id="7e2ae-223">Sprawdzanie poprawności każdego konta magazynu dla migracji za pomocą hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="7e2ae-223">Validate each storage account for migration by using hello following command.</span></span> <span data-ttu-id="7e2ae-224">W tym przykładzie nazwa konta magazynu hello jest **Mojekontomagazynu**.</span><span class="sxs-lookup"><span data-stu-id="7e2ae-224">In this example, hello storage account name is **myStorageAccount**.</span></span> <span data-ttu-id="7e2ae-225">Zamień hello Przykładowa nazwa hello nazwę konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="7e2ae-225">Replace hello example name with hello name of your own storage account.</span></span>

```powershell
    $storageAccountName = "myStorageAccount"
    Move-AzureStorageAccount -Validate -StorageAccountName $storageAccountName
```

<span data-ttu-id="7e2ae-226">Następnym krokiem jest tooPrepare hello konto magazynu na potrzeby migracji</span><span class="sxs-lookup"><span data-stu-id="7e2ae-226">Next step is tooPrepare hello storage account for migration</span></span>

```powershell
    $storageAccountName = "myStorageAccount"
    Move-AzureStorageAccount -Prepare -StorageAccountName $storageAccountName
```

<span data-ttu-id="7e2ae-227">Sprawdź konfigurację hello hello przygotowane konta magazynu przy użyciu programu Azure PowerShell lub hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="7e2ae-227">Check hello configuration for hello prepared storage account by using either Azure PowerShell or hello Azure portal.</span></span> <span data-ttu-id="7e2ae-228">Jeśli nie jest jeszcze gotowa do migracji i ma toogo toohello wstecz poprzedni stan, użyj hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="7e2ae-228">If you are not ready for migration and you want toogo back toohello old state, use hello following command:</span></span>

```powershell
    Move-AzureStorageAccount -Abort -StorageAccountName $storageAccountName
```

<span data-ttu-id="7e2ae-229">Jeśli hello przygotowane Konfiguracja wygląda dobrze, możesz przejść do przodu i zatwierdzić hello zasobów za pomocą następującego polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="7e2ae-229">If hello prepared configuration looks good, you can move forward and commit hello resources by using hello following command:</span></span>

```powershell
    Move-AzureStorageAccount -Commit -StorageAccountName $storageAccountName
```

## <a name="next-steps"></a><span data-ttu-id="7e2ae-230">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7e2ae-230">Next steps</span></span>
* [<span data-ttu-id="7e2ae-231">Omówienie migracji zasobów IaaS z klasycznym tooAzure Resource Manager obsługiwane platformy</span><span class="sxs-lookup"><span data-stu-id="7e2ae-231">Overview of platform-supported migration of IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="7e2ae-232">Techniczne szczegółowe informacje na temat migracji z obsługiwanych platform z klasycznym tooAzure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7e2ae-232">Technical deep dive on platform-supported migration from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="7e2ae-233">Planowanie migracji zasobów IaaS z klasycznym tooAzure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7e2ae-233">Planning for migration of IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="7e2ae-234">Użyj interfejsu wiersza polecenia toomigrate IaaS zasobów z klasycznym tooAzure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7e2ae-234">Use CLI toomigrate IaaS resources from classic tooAzure Resource Manager</span></span>](../linux/migration-classic-resource-manager-cli.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="7e2ae-235">Narzędzia z migracji zasobów IaaS z klasycznym tooAzure Menedżera zasobów społeczności</span><span class="sxs-lookup"><span data-stu-id="7e2ae-235">Community tools for assisting with migration of IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-community-tools.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="7e2ae-236">Przegląd najbardziej typowych błędów migracji</span><span class="sxs-lookup"><span data-stu-id="7e2ae-236">Review most common migration errors</span></span>](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="7e2ae-237">Hello przeglądu najczęściej zadawane pytania dotyczące migracji zasobów IaaS z klasycznym tooAzure Menedżera zasobów</span><span class="sxs-lookup"><span data-stu-id="7e2ae-237">Review hello most frequently asked questions about migrating IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
