---
title: "aaaMigrate tooResource maszyn wirtualnych Menedżera przy użyciu wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule przedstawiono hello obsługiwane platformy migracji zasobów z klasycznym tooAzure Resource Manager przy użyciu wiersza polecenia platformy Azure"
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d6f5a877-05b6-4127-a545-3f5bede4e479
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: kasing
ms.openlocfilehash: 0b11f4bb1b4658b3e88bf7629147ed953b678556
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-iaas-resources-from-classic-tooazure-resource-manager-by-using-azure-cli"></a><span data-ttu-id="71651-103">Migracja zasobów IaaS z klasycznym tooAzure Menedżera zasobów przy użyciu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="71651-103">Migrate IaaS resources from classic tooAzure Resource Manager by using Azure CLI</span></span>
<span data-ttu-id="71651-104">Te kroki pokazują, jak toouse Azure interfejsu wiersza polecenia (CLI) polecenia toomigrate infrastruktura jako usługa (IaaS) zasoby z modelu wdrażania usługi Azure Resource Manager toohello hello wdrażania klasycznego modelu.</span><span class="sxs-lookup"><span data-stu-id="71651-104">These steps show you how toouse Azure command-line interface (CLI) commands toomigrate infrastructure as a service (IaaS) resources from hello classic deployment model toohello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="71651-105">Artykuł Hello wymaga hello [interfejsu wiersza polecenia Azure](../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="71651-105">hello article requires hello [Azure CLI](../../cli-install-nodejs.md).</span></span>

> [!NOTE]
> <span data-ttu-id="71651-106">Wszystkie operacje hello opisane w tym miejscu są idempotentności.</span><span class="sxs-lookup"><span data-stu-id="71651-106">All hello operations described here are idempotent.</span></span> <span data-ttu-id="71651-107">Jeśli masz problem niż nieobsługiwanej funkcji lub błąd konfiguracji, zalecamy możesz ponowić próbę hello przygotowanie, przerwania lub przekazania operacji.</span><span class="sxs-lookup"><span data-stu-id="71651-107">If you have a problem other than an unsupported feature or a configuration error, we recommend that you retry hello prepare, abort, or commit operation.</span></span> <span data-ttu-id="71651-108">Platforma Hello spróbuj hello akcję ponownie.</span><span class="sxs-lookup"><span data-stu-id="71651-108">hello platform will then try hello action again.</span></span>
> 
> 

<br>
<span data-ttu-id="71651-109">Poniżej przedstawiono kolejność hello tooidentify schemat blokowy, w którym kroki należy wykonać podczas procesu migracji toobe</span><span class="sxs-lookup"><span data-stu-id="71651-109">Here is a flowchart tooidentify hello order in which steps need toobe executed during a migration process</span></span>

![Zrzut ekranu pokazujący hello kroków migracji](../windows/media/migration-classic-resource-manager/migration-flow.png)

## <a name="step-1-prepare-for-migration"></a><span data-ttu-id="71651-111">Krok 1: Przygotowanie do migracji</span><span class="sxs-lookup"><span data-stu-id="71651-111">Step 1: Prepare for migration</span></span>
<span data-ttu-id="71651-112">Poniżej przedstawiono kilka najlepsze rozwiązania, które firma Microsoft zaleca jako ocenić migracji zasobów IaaS z klasycznym tooResource Menedżera:</span><span class="sxs-lookup"><span data-stu-id="71651-112">Here are a few best practices that we recommend as you evaluate migrating IaaS resources from classic tooResource Manager:</span></span>

* <span data-ttu-id="71651-113">Zapoznaj się z artykułem hello [lista nieobsługiwanych konfiguracji lub funkcji](../windows/migration-classic-resource-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="71651-113">Read through hello [list of unsupported configurations or features](../windows/migration-classic-resource-manager-overview.md).</span></span> <span data-ttu-id="71651-114">Jeśli masz maszyn wirtualnych, które używają nieobsługiwane konfiguracje i funkcje, firma Microsoft zaleca, poczekaj toobe obsługi funkcji/konfiguracji hello anonsowania.</span><span class="sxs-lookup"><span data-stu-id="71651-114">If you have virtual machines that use unsupported configurations or features, we recommend that you wait for hello feature/configuration support toobe announced.</span></span> <span data-ttu-id="71651-115">Alternatywnie można usunąć tej funkcji lub wychodzenia z tej konfiguracji tooenable migracji, jeśli go odpowiada Twoim potrzebom.</span><span class="sxs-lookup"><span data-stu-id="71651-115">Alternatively, you can remove that feature or move out of that configuration tooenable migration if it suits your needs.</span></span>
* <span data-ttu-id="71651-116">Jeśli mają automatyczny skrypty, które obecnie wdrażanie infrastruktury i aplikacji, spróbuj toocreate podobnych konfiguracji testu przy użyciu tych skryptów do migracji.</span><span class="sxs-lookup"><span data-stu-id="71651-116">If you have automated scripts that deploy your infrastructure and applications today, try toocreate a similar test setup by using those scripts for migration.</span></span> <span data-ttu-id="71651-117">Można też skonfigurować próbkę środowiskami przy użyciu hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="71651-117">Alternatively, you can set up sample environments by using hello Azure portal.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="71651-118">Migracji z klasycznym tooResource Menedżera bramy aplikacji nie są obecnie obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="71651-118">Application Gateways are not currently supported for migration from classic tooResource Manager.</span></span> <span data-ttu-id="71651-119">toomigrate klasycznej sieci wirtualnej z bramy aplikacji usunąć bramę hello przed uruchomieniem operacji Prepare toomove hello sieci.</span><span class="sxs-lookup"><span data-stu-id="71651-119">toomigrate a classic virtual network with an Application gateway, remove hello gateway before running a Prepare operation toomove hello network.</span></span> <span data-ttu-id="71651-120">Po zakończeniu migracji hello ponownie hello bramy w usłudze Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="71651-120">After you complete hello migration, reconnect hello gateway in Azure Resource Manager.</span></span> 
>
><span data-ttu-id="71651-121">Łączenie obwody tooExpressRoute w innej subskrypcji bram usługi ExpressRoute nie może być migrowane automatycznie.</span><span class="sxs-lookup"><span data-stu-id="71651-121">ExpressRoute gateways connecting tooExpressRoute circuits in another subscription cannot be migrated automatically.</span></span> <span data-ttu-id="71651-122">W takiej sytuacji należy usunąć bramę usługi ExpressRoute hello, migrację sieci wirtualnej hello i Utwórz ponownie hello bramy.</span><span class="sxs-lookup"><span data-stu-id="71651-122">In such cases, remove hello ExpressRoute gateway, migrate hello virtual network and recreate hello gateway.</span></span> <span data-ttu-id="71651-123">Zobacz [ExpressRoute migracji obwody i skojarzone sieci wirtualne od modelu wdrażania Menedżera zasobów klasycznych toohello hello](../../expressroute/expressroute-migration-classic-resource-manager.md) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="71651-123">Please see [Migrate ExpressRoute circuits and associated virtual networks from hello classic toohello Resource Manager deployment model](../../expressroute/expressroute-migration-classic-resource-manager.md) for more information.</span></span>
> 
> 

## <a name="step-2-set-your-subscription-and-register-hello-provider"></a><span data-ttu-id="71651-124">Krok 2: Ustaw swoją subskrypcję i zarejestrować dostawcę hello</span><span class="sxs-lookup"><span data-stu-id="71651-124">Step 2: Set your subscription and register hello provider</span></span>
<span data-ttu-id="71651-125">Scenariusze migracji należy tooset Twojego środowiska dla obu classic i Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="71651-125">For migration scenarios, you need tooset up your environment for both classic and Resource Manager.</span></span> <span data-ttu-id="71651-126">[Zainstaluj interfejs wiersza polecenia Azure](../../cli-install-nodejs.md) i [Wybierz subskrypcję](../../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="71651-126">[Install Azure CLI](../../cli-install-nodejs.md) and [select your subscription](../../xplat-cli-connect.md).</span></span>

<span data-ttu-id="71651-127">Konto logowania tooyour.</span><span class="sxs-lookup"><span data-stu-id="71651-127">Sign-in tooyour account.</span></span>

    azure login

<span data-ttu-id="71651-128">Wybierz hello subskrypcji platformy Azure przy użyciu następującego polecenia hello.</span><span class="sxs-lookup"><span data-stu-id="71651-128">Select hello Azure subscription by using hello following command.</span></span>

    azure account set "<azure-subscription-name>"

> [!NOTE]
> <span data-ttu-id="71651-129">Rejestracja jest jeden raz krok jednak wymaga toobe wykonywane raz, przed podjęciem próby wykonania migracji.</span><span class="sxs-lookup"><span data-stu-id="71651-129">Registration is a one time step but it needs toobe done once before attempting migration.</span></span> <span data-ttu-id="71651-130">Bez rejestracji zostanie wyświetlony następujący komunikat o błędzie hello</span><span class="sxs-lookup"><span data-stu-id="71651-130">Without registering you'll see hello following error message</span></span> 
> 
> <span data-ttu-id="71651-131">*Element BadRequest: Subskrypcja nie jest zarejestrowana do migracji.*</span><span class="sxs-lookup"><span data-stu-id="71651-131">*BadRequest : Subscription is not registered for migration.*</span></span> 
> 
> 

<span data-ttu-id="71651-132">Zarejestruj się w dostawcy zasobów hello migracji za pomocą następującego polecenia hello.</span><span class="sxs-lookup"><span data-stu-id="71651-132">Register with hello migration resource provider by using hello following command.</span></span> <span data-ttu-id="71651-133">Należy pamiętać, że w niektórych przypadkach to polecenie upłynie limit czasu. Jednak hello będzie można pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="71651-133">Note that in some cases, this command times out. However, hello registration will be successful.</span></span>

    azure provider register Microsoft.ClassicInfrastructureMigrate

<span data-ttu-id="71651-134">Poczekaj pięć minut hello toofinish rejestracji.</span><span class="sxs-lookup"><span data-stu-id="71651-134">Please wait five minutes for hello registration toofinish.</span></span> <span data-ttu-id="71651-135">Za pomocą następującego polecenia hello można sprawdzić stan hello hello zatwierdzania.</span><span class="sxs-lookup"><span data-stu-id="71651-135">You can check hello status of hello approval by using hello following command.</span></span> <span data-ttu-id="71651-136">Upewnij się, że jest RegistrationState `Registered` przed kontynuowaniem.</span><span class="sxs-lookup"><span data-stu-id="71651-136">Make sure that RegistrationState is `Registered` before you proceed.</span></span>

    azure provider show Microsoft.ClassicInfrastructureMigrate

<span data-ttu-id="71651-137">Teraz przełącznik CLI toohello `asm` tryb.</span><span class="sxs-lookup"><span data-stu-id="71651-137">Now switch CLI toohello `asm` mode.</span></span>

    azure config mode asm

## <a name="step-3-make-sure-you-have-enough-azure-resource-manager-virtual-machine-cores-in-hello-azure-region-of-your-current-deployment-or-vnet"></a><span data-ttu-id="71651-138">Krok 3: Upewnij się, że masz wystarczająco dużo rdzeni maszyny wirtualnej Azure Resource Manager w hello region platformy Azure dla bieżącego wdrożenia lub sieci Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="71651-138">Step 3: Make sure you have enough Azure Resource Manager Virtual Machine cores in hello Azure region of your current deployment or VNET</span></span>
<span data-ttu-id="71651-139">W tym kroku musisz tooswitch zbyt`arm` tryb.</span><span class="sxs-lookup"><span data-stu-id="71651-139">For this step you'll need tooswitch too`arm` mode.</span></span> <span data-ttu-id="71651-140">W tym z hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="71651-140">Do this with hello following command.</span></span>

```
azure config mode arm
```

<span data-ttu-id="71651-141">Możesz użyć powitania po interfejsu wiersza polecenia polecenie toocheck hello Bieżąca ilość rdzeni, do których masz usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="71651-141">You can use hello following CLI command toocheck hello current amount of cores you have in Azure Resource Manager.</span></span> <span data-ttu-id="71651-142">toolearn więcej informacji na temat przydziały core, zobacz [limity i hello Azure Resource Manager](../../azure-subscription-service-limits.md#limits-and-the-azure-resource-manager)</span><span class="sxs-lookup"><span data-stu-id="71651-142">toolearn more about core quotas, see [Limits and hello Azure Resource Manager](../../azure-subscription-service-limits.md#limits-and-the-azure-resource-manager)</span></span>

```
azure vm list-usage -l "<Your VNET or Deployment's Azure region"
```

<span data-ttu-id="71651-143">Po zakończeniu sprawdzenia tego kroku, możesz przełączyć ponownie zbyt`asm` tryb.</span><span class="sxs-lookup"><span data-stu-id="71651-143">Once you're done verifying this step, you can switch back too`asm` mode.</span></span>

    azure config mode asm


## <a name="step-4-option-1---migrate-virtual-machines-in-a-cloud-service"></a><span data-ttu-id="71651-144">Krok 4: Opcja 1 — migracji maszyn wirtualnych w usłudze w chmurze</span><span class="sxs-lookup"><span data-stu-id="71651-144">Step 4: Option 1 - Migrate virtual machines in a cloud service</span></span>
<span data-ttu-id="71651-145">Pobranie listy hello usługi w chmurze przy użyciu hello następujące polecenie, a następnie usługa w chmurze hello pobrania, które mają toomigrate.</span><span class="sxs-lookup"><span data-stu-id="71651-145">Get hello list of cloud services by using hello following command, and then pick hello cloud service that you want toomigrate.</span></span> <span data-ttu-id="71651-146">Należy pamiętać, że jeśli hello maszyn wirtualnych w usłudze w chmurze hello znajdują się w sieci wirtualnej lub mają one role sieć web/proces roboczy, zostanie wyświetlony komunikat o błędzie.</span><span class="sxs-lookup"><span data-stu-id="71651-146">Note that if hello VMs in hello cloud service are in a virtual network or if they have web/worker roles, you will get an error message.</span></span>

    azure service list

<span data-ttu-id="71651-147">Witaj uruchom następujące polecenie Nazwa wdrożenia hello tooget dla usługi w chmurze hello z hello pełne dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="71651-147">Run hello following command tooget hello deployment name for hello cloud service from hello verbose output.</span></span> <span data-ttu-id="71651-148">W większości przypadków hello Nazwa wdrożenia jest hello taka sama jak nazwa usługi w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="71651-148">In most cases, hello deployment name is hello same as hello cloud service name.</span></span>

    azure service show <serviceName> -vv

<span data-ttu-id="71651-149">Po pierwsze sprawdzanie poprawności w przypadku migrowania usługi w chmurze hello za pomocą następującego polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="71651-149">First, validate if you can migrate hello cloud service using hello following commands:</span></span>

```shell
azure service deployment validate-migration <serviceName> <deploymentName> new "" "" ""
```

<span data-ttu-id="71651-150">Przygotuj maszyny wirtualne hello hello w usłudze w chmurze do migracji.</span><span class="sxs-lookup"><span data-stu-id="71651-150">Prepare hello virtual machines in hello cloud service for migration.</span></span> <span data-ttu-id="71651-151">Masz dwie opcje toochoose z.</span><span class="sxs-lookup"><span data-stu-id="71651-151">You have two options toochoose from.</span></span>

<span data-ttu-id="71651-152">Toomigrate hello maszyn wirtualnych tooa utworzone platformy sieci wirtualnej firmy, należy użyć hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="71651-152">If you want toomigrate hello VMs tooa platform-created virtual network, use hello following command.</span></span>

    azure service deployment prepare-migration <serviceName> <deploymentName> new "" "" ""

<span data-ttu-id="71651-153">Tooan toomigrate istniejącej sieci wirtualnej w modelu wdrażania usługi Resource Manager hello firmy, należy użyć hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="71651-153">If you want toomigrate tooan existing virtual network in hello Resource Manager deployment model, use hello following command.</span></span>

    azure service deployment prepare-migration <serviceName> <deploymentName> existing <destinationVNETResourceGroupName> <subnetName> <vnetName>

<span data-ttu-id="71651-154">Po przygotowanie hello operacja się powiodła, można przeglądać hello pełne dane wyjściowe tooget hello migracji stanu hello maszyn wirtualnych i upewnij się, że są one hello `Prepared` stanu.</span><span class="sxs-lookup"><span data-stu-id="71651-154">After hello prepare operation is successful, you can look through hello verbose output tooget hello migration state of hello VMs and ensure that they are in hello `Prepared` state.</span></span>

    azure vm show <vmName> -vv

<span data-ttu-id="71651-155">Sprawdź konfigurację hello hello przygotowany zasobów przy użyciu interfejsu wiersza polecenia lub hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="71651-155">Check hello configuration for hello prepared resources by using either CLI or hello Azure portal.</span></span> <span data-ttu-id="71651-156">Jeśli nie jest jeszcze gotowa do migracji i ma toogo toohello wstecz poprzedni stan, użyj hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="71651-156">If you are not ready for migration and you want toogo back toohello old state, use hello following command.</span></span>

    azure service deployment abort-migration <serviceName> <deploymentName>

<span data-ttu-id="71651-157">Jeśli hello przygotowane Konfiguracja wygląda dobrze, można przejść do przodu i zatwierdzić hello zasobów za pomocą następującego polecenia hello.</span><span class="sxs-lookup"><span data-stu-id="71651-157">If hello prepared configuration looks good, you can move forward and commit hello resources by using hello following command.</span></span>

    azure service deployment commit-migration <serviceName> <deploymentName>



## <a name="step-4-option-2----migrate-virtual-machines-in-a-virtual-network"></a><span data-ttu-id="71651-158">Krok 4: Opcja 2 — migracji maszyn wirtualnych w sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="71651-158">Step 4: Option 2 -  Migrate virtual machines in a virtual network</span></span>
<span data-ttu-id="71651-159">Pobranie hello sieci wirtualnej, które mają toomigrate.</span><span class="sxs-lookup"><span data-stu-id="71651-159">Pick hello virtual network that you want toomigrate.</span></span> <span data-ttu-id="71651-160">Należy pamiętać, że jeśli hello sieć wirtualna zawiera role sieć web/proces roboczy lub maszyn wirtualnych z nieobsługiwaną konfiguracją, otrzymasz komunikat o błędzie weryfikacji.</span><span class="sxs-lookup"><span data-stu-id="71651-160">Note that if hello virtual network contains web/worker roles or VMs with unsupported configurations, you will get a validation error message.</span></span>

<span data-ttu-id="71651-161">Pobierz wszystkie sieci wirtualne hello w subskrypcji hello za pomocą następującego polecenia hello.</span><span class="sxs-lookup"><span data-stu-id="71651-161">Get all hello virtual networks in hello subscription by using hello following command.</span></span>

    azure network vnet list

<span data-ttu-id="71651-162">Witaj dane wyjściowe będą wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="71651-162">hello output will look something like this:</span></span>

![Zrzut ekranu przedstawiający hello wiersza polecenia o nazwie całej sieci wirtualnej hello wyróżnione.](../media/virtual-machines-linux-cli-migration-classic-resource-manager/vnet.png)

<span data-ttu-id="71651-164">W hello powyżej przykładzie, hello **virtualNetworkName** jest hello całą nazwę **"Classicubuntu16 classicubuntu16 grupy"**.</span><span class="sxs-lookup"><span data-stu-id="71651-164">In hello above example, hello **virtualNetworkName** is hello entire name **"Group classicubuntu16 classicubuntu16"**.</span></span>

<span data-ttu-id="71651-165">Po pierwsze sprawdzanie poprawności w przypadku migrowania hello sieci wirtualnej przy użyciu hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="71651-165">First, validate if you can migrate hello virtual network using hello following command:</span></span>

```shell
azure network vnet validate-migration <virtualNetworkName>
```

<span data-ttu-id="71651-166">Przygotowania do migracji sieci wirtualnej hello wybranych przez użytkownika, za pomocą następującego polecenia hello.</span><span class="sxs-lookup"><span data-stu-id="71651-166">Prepare hello virtual network of your choice for migration by using hello following command.</span></span>

    azure network vnet prepare-migration <virtualNetworkName>

<span data-ttu-id="71651-167">Sprawdź konfigurację hello hello przygotowany maszyn wirtualnych przy użyciu interfejsu wiersza polecenia lub hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="71651-167">Check hello configuration for hello prepared virtual machines by using either CLI or hello Azure portal.</span></span> <span data-ttu-id="71651-168">Jeśli nie jest jeszcze gotowa do migracji i ma toogo toohello wstecz poprzedni stan, użyj hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="71651-168">If you are not ready for migration and you want toogo back toohello old state, use hello following command.</span></span>

    azure network vnet abort-migration <virtualNetworkName>

<span data-ttu-id="71651-169">Jeśli hello przygotowane Konfiguracja wygląda dobrze, można przejść do przodu i zatwierdzić hello zasobów za pomocą następującego polecenia hello.</span><span class="sxs-lookup"><span data-stu-id="71651-169">If hello prepared configuration looks good, you can move forward and commit hello resources by using hello following command.</span></span>

    azure network vnet commit-migration <virtualNetworkName>

## <a name="step-5-migrate-a-storage-account"></a><span data-ttu-id="71651-170">Krok 5: Migrowanie konta magazynu</span><span class="sxs-lookup"><span data-stu-id="71651-170">Step 5: Migrate a storage account</span></span>
<span data-ttu-id="71651-171">Po zakończeniu migracji maszyn wirtualnych hello, zaleca się migrowanie hello konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="71651-171">Once you're done migrating hello virtual machines, we recommend you migrate hello storage account.</span></span>

<span data-ttu-id="71651-172">Przygotuj hello konta magazynu do migracji za pomocą następującego polecenia hello</span><span class="sxs-lookup"><span data-stu-id="71651-172">Prepare hello storage account for migration by using hello following command</span></span>

    azure storage account prepare-migration <storageAccountName>

<span data-ttu-id="71651-173">Sprawdź konfigurację hello hello przygotowane konta magazynu przy użyciu interfejsu wiersza polecenia lub hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="71651-173">Check hello configuration for hello prepared storage account by using either CLI or hello Azure portal.</span></span> <span data-ttu-id="71651-174">Jeśli nie jest jeszcze gotowa do migracji i ma toogo toohello wstecz poprzedni stan, użyj hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="71651-174">If you are not ready for migration and you want toogo back toohello old state, use hello following command.</span></span>

    azure storage account abort-migration <storageAccountName>

<span data-ttu-id="71651-175">Jeśli hello przygotowane Konfiguracja wygląda dobrze, można przejść do przodu i zatwierdzić hello zasobów za pomocą następującego polecenia hello.</span><span class="sxs-lookup"><span data-stu-id="71651-175">If hello prepared configuration looks good, you can move forward and commit hello resources by using hello following command.</span></span>

    azure storage account commit-migration <storageAccountName>

## <a name="next-steps"></a><span data-ttu-id="71651-176">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="71651-176">Next steps</span></span>

* [<span data-ttu-id="71651-177">Omówienie migracji zasobów IaaS z klasycznym tooAzure Resource Manager obsługiwane platformy</span><span class="sxs-lookup"><span data-stu-id="71651-177">Overview of platform-supported migration of IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="71651-178">Techniczne szczegółowe informacje na temat migracji z obsługiwanych platform z klasycznym tooAzure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="71651-178">Technical deep dive on platform-supported migration from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="71651-179">Planowanie migracji zasobów IaaS z klasycznym tooAzure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="71651-179">Planning for migration of IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="71651-180">Użyj programu PowerShell toomigrate IaaS zasobów z klasycznym tooAzure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="71651-180">Use PowerShell toomigrate IaaS resources from classic tooAzure Resource Manager</span></span>](../windows/migration-classic-resource-manager-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="71651-181">Narzędzia z migracji zasobów IaaS z klasycznym tooAzure Menedżera zasobów społeczności</span><span class="sxs-lookup"><span data-stu-id="71651-181">Community tools for assisting with migration of IaaS resources from classic tooAzure Resource Manager</span></span>](../windows/migration-classic-resource-manager-community-tools.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="71651-182">Przegląd najbardziej typowych błędów migracji</span><span class="sxs-lookup"><span data-stu-id="71651-182">Review most common migration errors</span></span>](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="71651-183">Hello przeglądu najczęściej zadawane pytania dotyczące migracji zasobów IaaS z klasycznym tooAzure Menedżera zasobów</span><span class="sxs-lookup"><span data-stu-id="71651-183">Review hello most frequently asked questions about migrating IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
