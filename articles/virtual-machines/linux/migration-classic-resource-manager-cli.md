---
title: "Migrowanie maszyn wirtualnych do Menedżera zasobów przy użyciu wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule przedstawiono za pośrednictwem obsługiwanych platform migracji zasobów z klasycznego do usługi Azure Resource Manager przy użyciu wiersza polecenia platformy Azure"
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
ms.openlocfilehash: a63d758570b09b37b8e51c639267f729521d9ae0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="migrate-iaas-resources-from-classic-to-azure-resource-manager-by-using-azure-cli"></a><span data-ttu-id="fec47-103">Migracja zasobów IaaS ze środowiska klasycznego do usługi Azure Resource Manager przy użyciu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="fec47-103">Migrate IaaS resources from classic to Azure Resource Manager by using Azure CLI</span></span>
<span data-ttu-id="fec47-104">Te kroki pokazują, jak używać poleceń Azure interfejsu wiersza polecenia (CLI), aby migrować infrastruktury jako zasoby usługi (IaaS) z klasycznym modelu wdrażania modelu wdrażania usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="fec47-104">These steps show you how to use Azure command-line interface (CLI) commands to migrate infrastructure as a service (IaaS) resources from the classic deployment model to the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="fec47-105">Wymaga artykułu [interfejsu wiersza polecenia Azure](../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="fec47-105">The article requires the [Azure CLI](../../cli-install-nodejs.md).</span></span>

> [!NOTE]
> <span data-ttu-id="fec47-106">Wszystkie czynności opisane w tym miejscu są idempotentności.</span><span class="sxs-lookup"><span data-stu-id="fec47-106">All the operations described here are idempotent.</span></span> <span data-ttu-id="fec47-107">Jeśli masz problem niż nieobsługiwanej funkcji lub błąd konfiguracji, zalecamy możesz ponowić próbę o przygotowaniu przerwania lub przekazania operacji.</span><span class="sxs-lookup"><span data-stu-id="fec47-107">If you have a problem other than an unsupported feature or a configuration error, we recommend that you retry the prepare, abort, or commit operation.</span></span> <span data-ttu-id="fec47-108">Platforma spróbuj wykonać akcję ponownie.</span><span class="sxs-lookup"><span data-stu-id="fec47-108">The platform will then try the action again.</span></span>
> 
> 

<br>
<span data-ttu-id="fec47-109">Oto schemat blokowy, aby określić kolejność kroków muszą być wykonywane podczas procesu migracji</span><span class="sxs-lookup"><span data-stu-id="fec47-109">Here is a flowchart to identify the order in which steps need to be executed during a migration process</span></span>

![Zrzut ekranu przedstawiający kroki migracji](../windows/media/migration-classic-resource-manager/migration-flow.png)

## <a name="step-1-prepare-for-migration"></a><span data-ttu-id="fec47-111">Krok 1: Przygotowanie do migracji</span><span class="sxs-lookup"><span data-stu-id="fec47-111">Step 1: Prepare for migration</span></span>
<span data-ttu-id="fec47-112">Poniżej przedstawiono kilka najlepsze rozwiązania, które są zalecane jako ocenić Migrowanie zasobów IaaS z klasycznego do Menedżera zasobów:</span><span class="sxs-lookup"><span data-stu-id="fec47-112">Here are a few best practices that we recommend as you evaluate migrating IaaS resources from classic to Resource Manager:</span></span>

* <span data-ttu-id="fec47-113">Zapoznaj się z artykułem [lista nieobsługiwanych konfiguracji lub funkcji](../windows/migration-classic-resource-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fec47-113">Read through the [list of unsupported configurations or features](../windows/migration-classic-resource-manager-overview.md).</span></span> <span data-ttu-id="fec47-114">Jeśli masz maszyn wirtualnych, które używają nieobsługiwane konfiguracje i funkcje, zaleca się poczekać do obsługi funkcji/konfiguracji zostaną ogłoszone.</span><span class="sxs-lookup"><span data-stu-id="fec47-114">If you have virtual machines that use unsupported configurations or features, we recommend that you wait for the feature/configuration support to be announced.</span></span> <span data-ttu-id="fec47-115">Alternatywnie można usunąć tej funkcji lub wychodzenia tej konfiguracji, aby umożliwić migrację, jeśli go odpowiada Twoim potrzebom.</span><span class="sxs-lookup"><span data-stu-id="fec47-115">Alternatively, you can remove that feature or move out of that configuration to enable migration if it suits your needs.</span></span>
* <span data-ttu-id="fec47-116">Jeśli mają automatyczny skrypty, które obecnie wdrażanie infrastruktury i aplikacji, spróbuj utworzyć podobnych konfiguracji testu przy użyciu tych skryptów do migracji.</span><span class="sxs-lookup"><span data-stu-id="fec47-116">If you have automated scripts that deploy your infrastructure and applications today, try to create a similar test setup by using those scripts for migration.</span></span> <span data-ttu-id="fec47-117">Można też skonfigurować próbkę środowiskami przy użyciu portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="fec47-117">Alternatively, you can set up sample environments by using the Azure portal.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fec47-118">Bramy aplikacji nie są obecnie obsługiwane dla migracji ze środowiska klasycznego do Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="fec47-118">Application Gateways are not currently supported for migration from classic to Resource Manager.</span></span> <span data-ttu-id="fec47-119">Aby przeprowadzić migrację z bramy aplikacji klasycznej sieci wirtualnej, należy usunąć bramę, przed uruchomieniem operacji Prepare, aby przenieść sieć.</span><span class="sxs-lookup"><span data-stu-id="fec47-119">To migrate a classic virtual network with an Application gateway, remove the gateway before running a Prepare operation to move the network.</span></span> <span data-ttu-id="fec47-120">Po zakończeniu migracji należy ponownie podłączyć bramy w usłudze Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="fec47-120">After you complete the migration, reconnect the gateway in Azure Resource Manager.</span></span> 
>
><span data-ttu-id="fec47-121">Bram usługi ExpressRoute nawiązywania obwody usługi ExpressRoute w innej subskrypcji nie może być migrowane automatycznie.</span><span class="sxs-lookup"><span data-stu-id="fec47-121">ExpressRoute gateways connecting to ExpressRoute circuits in another subscription cannot be migrated automatically.</span></span> <span data-ttu-id="fec47-122">W takiej sytuacji należy usunąć bramę usługi ExpressRoute, migrację sieci wirtualnej i Utwórz ponownie bramę.</span><span class="sxs-lookup"><span data-stu-id="fec47-122">In such cases, remove the ExpressRoute gateway, migrate the virtual network and recreate the gateway.</span></span> <span data-ttu-id="fec47-123">Zobacz [ExpressRoute migracji obwody i skojarzone sieci wirtualne z klasycznego modelu wdrażania usługi Resource Manager](../../expressroute/expressroute-migration-classic-resource-manager.md) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="fec47-123">Please see [Migrate ExpressRoute circuits and associated virtual networks from the classic to the Resource Manager deployment model](../../expressroute/expressroute-migration-classic-resource-manager.md) for more information.</span></span>
> 
> 

## <a name="step-2-set-your-subscription-and-register-the-provider"></a><span data-ttu-id="fec47-124">Krok 2: Ustaw swoją subskrypcję i zarejestrować dostawcę</span><span class="sxs-lookup"><span data-stu-id="fec47-124">Step 2: Set your subscription and register the provider</span></span>
<span data-ttu-id="fec47-125">Scenariusze migracji należy skonfigurować środowisko dla obu classic i Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="fec47-125">For migration scenarios, you need to set up your environment for both classic and Resource Manager.</span></span> <span data-ttu-id="fec47-126">[Zainstaluj interfejs wiersza polecenia Azure](../../cli-install-nodejs.md) i [Wybierz subskrypcję](../../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="fec47-126">[Install Azure CLI](../../cli-install-nodejs.md) and [select your subscription](../../xplat-cli-connect.md).</span></span>

<span data-ttu-id="fec47-127">Zaloguj się do swojego konta.</span><span class="sxs-lookup"><span data-stu-id="fec47-127">Sign-in to your account.</span></span>

    azure login

<span data-ttu-id="fec47-128">Wybierz subskrypcję platformy Azure przy użyciu następującego polecenia.</span><span class="sxs-lookup"><span data-stu-id="fec47-128">Select the Azure subscription by using the following command.</span></span>

    azure account set "<azure-subscription-name>"

> [!NOTE]
> <span data-ttu-id="fec47-129">Rejestracja jest relacją jeden krok czasu, ale należy jednak wykonać jeden raz, przed podjęciem próby wykonania migracji.</span><span class="sxs-lookup"><span data-stu-id="fec47-129">Registration is a one time step but it needs to be done once before attempting migration.</span></span> <span data-ttu-id="fec47-130">Bez rejestrowania pojawi się następujący komunikat o błędzie</span><span class="sxs-lookup"><span data-stu-id="fec47-130">Without registering you'll see the following error message</span></span> 
> 
> <span data-ttu-id="fec47-131">*Element BadRequest: Subskrypcja nie jest zarejestrowana do migracji.*</span><span class="sxs-lookup"><span data-stu-id="fec47-131">*BadRequest : Subscription is not registered for migration.*</span></span> 
> 
> 

<span data-ttu-id="fec47-132">Zarejestruj się w dostawcy zasobów migracji za pomocą następującego polecenia.</span><span class="sxs-lookup"><span data-stu-id="fec47-132">Register with the migration resource provider by using the following command.</span></span> <span data-ttu-id="fec47-133">Należy pamiętać, że w niektórych przypadkach to polecenie upłynie limit czasu.</span><span class="sxs-lookup"><span data-stu-id="fec47-133">Note that in some cases, this command times out.</span></span> <span data-ttu-id="fec47-134">Jednak powiedzie się rejestracji.</span><span class="sxs-lookup"><span data-stu-id="fec47-134">However, the registration will be successful.</span></span>

    azure provider register Microsoft.ClassicInfrastructureMigrate

<span data-ttu-id="fec47-135">Poczekaj pięć minut dla rejestracji zakończyć.</span><span class="sxs-lookup"><span data-stu-id="fec47-135">Please wait five minutes for the registration to finish.</span></span> <span data-ttu-id="fec47-136">Za pomocą następującego polecenia można sprawdzić stan zatwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="fec47-136">You can check the status of the approval by using the following command.</span></span> <span data-ttu-id="fec47-137">Upewnij się, że jest RegistrationState `Registered` przed kontynuowaniem.</span><span class="sxs-lookup"><span data-stu-id="fec47-137">Make sure that RegistrationState is `Registered` before you proceed.</span></span>

    azure provider show Microsoft.ClassicInfrastructureMigrate

<span data-ttu-id="fec47-138">Teraz przełącznik interfejsu wiersza polecenia do `asm` tryb.</span><span class="sxs-lookup"><span data-stu-id="fec47-138">Now switch CLI to the `asm` mode.</span></span>

    azure config mode asm

## <a name="step-3-make-sure-you-have-enough-azure-resource-manager-virtual-machine-cores-in-the-azure-region-of-your-current-deployment-or-vnet"></a><span data-ttu-id="fec47-139">Krok 3: Upewnij się, że masz wystarczająco dużo rdzeni maszyny wirtualnej Azure Resource Manager w regionie Azure bieżącego wdrożenia lub sieci Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="fec47-139">Step 3: Make sure you have enough Azure Resource Manager Virtual Machine cores in the Azure region of your current deployment or VNET</span></span>
<span data-ttu-id="fec47-140">W tym kroku musisz przełączyć się do `arm` tryb.</span><span class="sxs-lookup"><span data-stu-id="fec47-140">For this step you'll need to switch to `arm` mode.</span></span> <span data-ttu-id="fec47-141">To zrobić przy użyciu następującego polecenia.</span><span class="sxs-lookup"><span data-stu-id="fec47-141">Do this with the following command.</span></span>

```
azure config mode arm
```

<span data-ttu-id="fec47-142">Interfejs wiersza polecenia następujące polecenie służy do sprawdzania Bieżąca ilość rdzeni, do których masz usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="fec47-142">You can use the following CLI command to check the current amount of cores you have in Azure Resource Manager.</span></span> <span data-ttu-id="fec47-143">Aby dowiedzieć się więcej o przydziały core, zobacz [limity i usługi Azure Resource Manager](../../azure-subscription-service-limits.md#limits-and-the-azure-resource-manager)</span><span class="sxs-lookup"><span data-stu-id="fec47-143">To learn more about core quotas, see [Limits and the Azure Resource Manager](../../azure-subscription-service-limits.md#limits-and-the-azure-resource-manager)</span></span>

```
azure vm list-usage -l "<Your VNET or Deployment's Azure region"
```

<span data-ttu-id="fec47-144">Po zakończeniu sprawdzenia tego kroku, możesz przełączyć do `asm` tryb.</span><span class="sxs-lookup"><span data-stu-id="fec47-144">Once you're done verifying this step, you can switch back to `asm` mode.</span></span>

    azure config mode asm


## <a name="step-4-option-1---migrate-virtual-machines-in-a-cloud-service"></a><span data-ttu-id="fec47-145">Krok 4: Opcja 1 — migracji maszyn wirtualnych w usłudze w chmurze</span><span class="sxs-lookup"><span data-stu-id="fec47-145">Step 4: Option 1 - Migrate virtual machines in a cloud service</span></span>
<span data-ttu-id="fec47-146">Pobierz listę usług w chmurze za pomocą następującego polecenia, a następnie wybierz usługę w chmurze, które chcesz migrować.</span><span class="sxs-lookup"><span data-stu-id="fec47-146">Get the list of cloud services by using the following command, and then pick the cloud service that you want to migrate.</span></span> <span data-ttu-id="fec47-147">Należy pamiętać, że jeśli maszyny wirtualne w usłudze w chmurze znajdują się w sieci wirtualnej, lub jeśli dysponują role sieć web/proces roboczy zostanie wyświetlony komunikat o błędzie.</span><span class="sxs-lookup"><span data-stu-id="fec47-147">Note that if the VMs in the cloud service are in a virtual network or if they have web/worker roles, you will get an error message.</span></span>

    azure service list

<span data-ttu-id="fec47-148">Uruchom następujące polecenie, aby uzyskać nazwę wdrożenia usługi w chmurze z pełne dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="fec47-148">Run the following command to get the deployment name for the cloud service from the verbose output.</span></span> <span data-ttu-id="fec47-149">W większości przypadków nazwa wdrożenia jest taka sama jak nazwa usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="fec47-149">In most cases, the deployment name is the same as the cloud service name.</span></span>

    azure service show <serviceName> -vv

<span data-ttu-id="fec47-150">Po pierwsze sprawdzanie poprawności w przypadku migrowania usługi w chmurze przy użyciu następujących poleceń:</span><span class="sxs-lookup"><span data-stu-id="fec47-150">First, validate if you can migrate the cloud service using the following commands:</span></span>

```shell
azure service deployment validate-migration <serviceName> <deploymentName> new "" "" ""
```

<span data-ttu-id="fec47-151">Przygotuj maszyny wirtualne w usłudze w chmurze do migracji.</span><span class="sxs-lookup"><span data-stu-id="fec47-151">Prepare the virtual machines in the cloud service for migration.</span></span> <span data-ttu-id="fec47-152">Dostępne są dwie opcje do wyboru.</span><span class="sxs-lookup"><span data-stu-id="fec47-152">You have two options to choose from.</span></span>

<span data-ttu-id="fec47-153">Jeśli chcesz przeprowadzić migrację maszyn wirtualnych do sieci wirtualnych utworzonych przez platformę, użyj następującego polecenia.</span><span class="sxs-lookup"><span data-stu-id="fec47-153">If you want to migrate the VMs to a platform-created virtual network, use the following command.</span></span>

    azure service deployment prepare-migration <serviceName> <deploymentName> new "" "" ""

<span data-ttu-id="fec47-154">Jeśli chcesz przeprowadzić migrację do istniejącej sieci wirtualnej w modelu wdrażania usługi Resource Manager, użyj następującego polecenia.</span><span class="sxs-lookup"><span data-stu-id="fec47-154">If you want to migrate to an existing virtual network in the Resource Manager deployment model, use the following command.</span></span>

    azure service deployment prepare-migration <serviceName> <deploymentName> existing <destinationVNETResourceGroupName> <subnetName> <vnetName>

<span data-ttu-id="fec47-155">Po operacji prepare zakończy się pomyślnie, można sprawdzić za pomocą pełne dane wyjściowe do pobrania stanu migracji maszyn wirtualnych i upewnij się, że są one `Prepared` stanu.</span><span class="sxs-lookup"><span data-stu-id="fec47-155">After the prepare operation is successful, you can look through the verbose output to get the migration state of the VMs and ensure that they are in the `Prepared` state.</span></span>

    azure vm show <vmName> -vv

<span data-ttu-id="fec47-156">Sprawdź konfigurację dla zasobów przygotowanego przy użyciu interfejsu wiersza polecenia lub w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="fec47-156">Check the configuration for the prepared resources by using either CLI or the Azure portal.</span></span> <span data-ttu-id="fec47-157">Jeśli chcesz powrócić do poprzedni stan nie jest jeszcze gotowa do migracji, użyj następującego polecenia.</span><span class="sxs-lookup"><span data-stu-id="fec47-157">If you are not ready for migration and you want to go back to the old state, use the following command.</span></span>

    azure service deployment abort-migration <serviceName> <deploymentName>

<span data-ttu-id="fec47-158">Jeśli przygotowane Konfiguracja wygląda dobrze, można przejść do przodu i zatwierdzić zasobów za pomocą następującego polecenia.</span><span class="sxs-lookup"><span data-stu-id="fec47-158">If the prepared configuration looks good, you can move forward and commit the resources by using the following command.</span></span>

    azure service deployment commit-migration <serviceName> <deploymentName>



## <a name="step-4-option-2----migrate-virtual-machines-in-a-virtual-network"></a><span data-ttu-id="fec47-159">Krok 4: Opcja 2 — migracji maszyn wirtualnych w sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="fec47-159">Step 4: Option 2 -  Migrate virtual machines in a virtual network</span></span>
<span data-ttu-id="fec47-160">Wybierz sieć wirtualną, która mają zostać zmigrowane.</span><span class="sxs-lookup"><span data-stu-id="fec47-160">Pick the virtual network that you want to migrate.</span></span> <span data-ttu-id="fec47-161">Należy pamiętać, że jeśli sieć wirtualna zawiera role sieć web/proces roboczy lub maszyn wirtualnych z nieobsługiwaną konfiguracją, otrzymasz komunikat o błędzie weryfikacji.</span><span class="sxs-lookup"><span data-stu-id="fec47-161">Note that if the virtual network contains web/worker roles or VMs with unsupported configurations, you will get a validation error message.</span></span>

<span data-ttu-id="fec47-162">Pobierz wszystkie sieci wirtualne w subskrypcji przy użyciu następującego polecenia.</span><span class="sxs-lookup"><span data-stu-id="fec47-162">Get all the virtual networks in the subscription by using the following command.</span></span>

    azure network vnet list

<span data-ttu-id="fec47-163">Dane wyjściowe będą wyglądać mniej więcej tak:</span><span class="sxs-lookup"><span data-stu-id="fec47-163">The output will look something like this:</span></span>

![Zrzut ekranu przedstawiający wiersza polecenia o nazwie całej sieci wirtualnej wyróżnione.](../media/virtual-machines-linux-cli-migration-classic-resource-manager/vnet.png)

<span data-ttu-id="fec47-165">W powyższym przykładzie **virtualNetworkName** jest całą nazwę **"Classicubuntu16 classicubuntu16 grupy"**.</span><span class="sxs-lookup"><span data-stu-id="fec47-165">In the above example, the **virtualNetworkName** is the entire name **"Group classicubuntu16 classicubuntu16"**.</span></span>

<span data-ttu-id="fec47-166">Po pierwsze sprawdzanie poprawności w przypadku migrowania sieci wirtualnej przy użyciu następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="fec47-166">First, validate if you can migrate the virtual network using the following command:</span></span>

```shell
azure network vnet validate-migration <virtualNetworkName>
```

<span data-ttu-id="fec47-167">Przygotowania do migracji sieci wirtualnej wybranych przez użytkownika, za pomocą następującego polecenia.</span><span class="sxs-lookup"><span data-stu-id="fec47-167">Prepare the virtual network of your choice for migration by using the following command.</span></span>

    azure network vnet prepare-migration <virtualNetworkName>

<span data-ttu-id="fec47-168">Sprawdź konfigurację przygotować maszyn wirtualnych przy użyciu interfejsu wiersza polecenia lub w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="fec47-168">Check the configuration for the prepared virtual machines by using either CLI or the Azure portal.</span></span> <span data-ttu-id="fec47-169">Jeśli chcesz powrócić do poprzedni stan nie jest jeszcze gotowa do migracji, użyj następującego polecenia.</span><span class="sxs-lookup"><span data-stu-id="fec47-169">If you are not ready for migration and you want to go back to the old state, use the following command.</span></span>

    azure network vnet abort-migration <virtualNetworkName>

<span data-ttu-id="fec47-170">Jeśli przygotowane Konfiguracja wygląda dobrze, można przejść do przodu i zatwierdzić zasobów za pomocą następującego polecenia.</span><span class="sxs-lookup"><span data-stu-id="fec47-170">If the prepared configuration looks good, you can move forward and commit the resources by using the following command.</span></span>

    azure network vnet commit-migration <virtualNetworkName>

## <a name="step-5-migrate-a-storage-account"></a><span data-ttu-id="fec47-171">Krok 5: Migrowanie konta magazynu</span><span class="sxs-lookup"><span data-stu-id="fec47-171">Step 5: Migrate a storage account</span></span>
<span data-ttu-id="fec47-172">Po zakończeniu migracji maszyn wirtualnych, firma Microsoft zaleca migracji konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="fec47-172">Once you're done migrating the virtual machines, we recommend you migrate the storage account.</span></span>

<span data-ttu-id="fec47-173">Przygotowanie konta magazynu dla migracji za pomocą następującego polecenia</span><span class="sxs-lookup"><span data-stu-id="fec47-173">Prepare the storage account for migration by using the following command</span></span>

    azure storage account prepare-migration <storageAccountName>

<span data-ttu-id="fec47-174">Sprawdź konfigurację dla konta magazynu przygotowanego przy użyciu interfejsu wiersza polecenia lub w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="fec47-174">Check the configuration for the prepared storage account by using either CLI or the Azure portal.</span></span> <span data-ttu-id="fec47-175">Jeśli chcesz powrócić do poprzedni stan nie jest jeszcze gotowa do migracji, użyj następującego polecenia.</span><span class="sxs-lookup"><span data-stu-id="fec47-175">If you are not ready for migration and you want to go back to the old state, use the following command.</span></span>

    azure storage account abort-migration <storageAccountName>

<span data-ttu-id="fec47-176">Jeśli przygotowane Konfiguracja wygląda dobrze, można przejść do przodu i zatwierdzić zasobów za pomocą następującego polecenia.</span><span class="sxs-lookup"><span data-stu-id="fec47-176">If the prepared configuration looks good, you can move forward and commit the resources by using the following command.</span></span>

    azure storage account commit-migration <storageAccountName>

## <a name="next-steps"></a><span data-ttu-id="fec47-177">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="fec47-177">Next steps</span></span>

* [<span data-ttu-id="fec47-178">Omówienie migracji zasobów IaaS ze środowiska klasycznego do usługi Azure Resource Manager obsługiwane platformy</span><span class="sxs-lookup"><span data-stu-id="fec47-178">Overview of platform-supported migration of IaaS resources from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="fec47-179">Techniczne szczegółowe informacje na temat obsługiwanych platform migracji ze środowiska klasycznego do usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="fec47-179">Technical deep dive on platform-supported migration from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="fec47-180">Planowanie migracji zasobów rozwiązania IaaS z wdrożenia klasycznego do usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="fec47-180">Planning for migration of IaaS resources from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="fec47-181">Migracja zasobów IaaS ze środowiska klasycznego do usługi Azure Resource Manager przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="fec47-181">Use PowerShell to migrate IaaS resources from classic to Azure Resource Manager</span></span>](../windows/migration-classic-resource-manager-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="fec47-182">Narzędzia społeczności z migracji zasobów IaaS ze środowiska klasycznego do usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="fec47-182">Community tools for assisting with migration of IaaS resources from classic to Azure Resource Manager</span></span>](../windows/migration-classic-resource-manager-community-tools.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="fec47-183">Przegląd najbardziej typowych błędów migracji</span><span class="sxs-lookup"><span data-stu-id="fec47-183">Review most common migration errors</span></span>](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="fec47-184">Przejrzyj najczęściej zadawane pytania dotyczące migrowania zasobów IaaS ze środowiska klasycznego do usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="fec47-184">Review the most frequently asked questions about migrating IaaS resources from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
