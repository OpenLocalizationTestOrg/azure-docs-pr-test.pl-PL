---
title: "Przykładowy skrypt Azure CLI — Zarządzanie pule w partii | Dokumentacja firmy Microsoft"
description: "Przykładowy skrypt Azure CLI — Zarządzanie pule w partii"
services: batch
documentationcenter: 
author: annatisch
manager: daryls
editor: tysonn
ms.assetid: 
ms.service: batch
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/02/2017
ms.author: antisch
ms.openlocfilehash: 2556b02459886390b803407c5cb828687229a44e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="managing-azure-batch-pools-with-azure-cli"></a><span data-ttu-id="a6279-103">Zarządzanie pule partii zadań Azure z wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="a6279-103">Managing Azure Batch pools with Azure CLI</span></span>

<span data-ttu-id="a6279-104">Te skryptu przedstawia niektóre z narzędzi dostępnych w ramach wiersza polecenia platformy Azure, aby utworzyć i Zarządzaj pulami węzłów obliczeniowych w usługi partia zadań Azure.</span><span class="sxs-lookup"><span data-stu-id="a6279-104">These script demonstrates some of the tools available in the Azure CLI to create and manage pools of compute nodes in the Azure Batch service.</span></span>

> [!NOTE]
> <span data-ttu-id="a6279-105">Polecenia w tym przykładzie Tworzenie maszyn wirtualnych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a6279-105">The commands in this sample create Azure virtual machines.</span></span> <span data-ttu-id="a6279-106">Działających maszyn wirtualnych będą naliczane opłaty do Twojego konta.</span><span class="sxs-lookup"><span data-stu-id="a6279-106">Running VMs will accrue charges to your account.</span></span> <span data-ttu-id="a6279-107">Aby zminimalizować tych opłat, Usuń maszyn wirtualnych po zakończeniu uruchamiania próbki.</span><span class="sxs-lookup"><span data-stu-id="a6279-107">To minimize these charges, delete the VMs once you're done running the sample.</span></span> <span data-ttu-id="a6279-108">Zobacz [wyczyścić pule](#clean-up-pools).</span><span class="sxs-lookup"><span data-stu-id="a6279-108">See [Clean up pools](#clean-up-pools).</span></span>

<span data-ttu-id="a6279-109">Pule partii można skonfigurować na dwa sposoby z konfiguracji usługi w chmurze (tylko system Windows) lub konfiguracji maszyny wirtualnej (z systemem Windows i Linux).</span><span class="sxs-lookup"><span data-stu-id="a6279-109">Batch pools can be configured in two ways, either with a Cloud Services configuration (Windows only), or a Virtual Machine configuration (Windows and Linux).</span></span> <span data-ttu-id="a6279-110">Przykładowe skrypty poniżej pokazano, jak utworzyć pule z obydwu konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="a6279-110">The sample scripts below show how to create pools with both configurations.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a6279-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="a6279-111">Prerequisites</span></span>

- <span data-ttu-id="a6279-112">Zainstaluj interfejs wiersza polecenia platformy Azure przy użyciu instrukcji w [Przewodnik instalacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/install-azure-cli), jeśli nie ma jeszcze zrobione.</span><span class="sxs-lookup"><span data-stu-id="a6279-112">Install the Azure CLI using the instructions provided in the [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), if you have not already done so.</span></span>
- <span data-ttu-id="a6279-113">Tworzenie konta usługi partia zadań, jeśli nie został wcześniej.</span><span class="sxs-lookup"><span data-stu-id="a6279-113">Create a Batch account if you don't already have one.</span></span> <span data-ttu-id="a6279-114">Zobacz [Tworzenie konta usługi partia zadań z wiersza polecenia platformy Azure](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) przykładowego skryptu, który tworzy konto.</span><span class="sxs-lookup"><span data-stu-id="a6279-114">See [Create a Batch account with the Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) for a sample script that creates an account.</span></span>
- <span data-ttu-id="a6279-115">Skonfigurować aplikację do uruchamiania z zadania uruchamiania, jeśli nie zostało to jeszcze zrobione.</span><span class="sxs-lookup"><span data-stu-id="a6279-115">Configure an application to run from a start task if you haven't yet done so.</span></span> <span data-ttu-id="a6279-116">Zobacz [Dodawanie aplikacji do partii zadań Azure z wiersza polecenia platformy Azure](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) przykładowego skryptu, który tworzy aplikację i przekazuje pakietu aplikacji do platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a6279-116">See [Adding applications to Azure Batch with Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) for a sample script that creates an application and uploads an application package to Azure.</span></span>

## <a name="pool-with-cloud-service-configuration-sample-script"></a><span data-ttu-id="a6279-117">Puli z skrypt przykładowy konfiguracji usługi chmury</span><span class="sxs-lookup"><span data-stu-id="a6279-117">Pool with cloud service configuration sample script</span></span>

<span data-ttu-id="a6279-118">[!code-azurecli[główne](../../../cli_scripts/batch/manage-pool/manage-pool-windows.sh "Zarządzaj pulami usługi w chmurze")]</span><span class="sxs-lookup"><span data-stu-id="a6279-118">[!code-azurecli[main](../../../cli_scripts/batch/manage-pool/manage-pool-windows.sh "Manage Cloud Services Pools")]</span></span>

## <a name="pool-with-virtual-machine-configuration-sample-script"></a><span data-ttu-id="a6279-119">Puli z skrypt przykładowy konfiguracji maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="a6279-119">Pool with virtual machine configuration sample script</span></span>

<span data-ttu-id="a6279-120">[!code-azurecli[główne](../../../cli_scripts/batch/manage-pool/manage-pool-linux.sh "Zarządzaj pulami maszyny wirtualnej")]</span><span class="sxs-lookup"><span data-stu-id="a6279-120">[!code-azurecli[main](../../../cli_scripts/batch/manage-pool/manage-pool-linux.sh "Manage Virtual Machine Pools")]</span></span>

## <a name="clean-up-pools"></a><span data-ttu-id="a6279-121">Oczyszczanie pul</span><span class="sxs-lookup"><span data-stu-id="a6279-121">Clean up pools</span></span>

<span data-ttu-id="a6279-122">Po uruchomieniu powyższy skrypt przykładowy należy uruchomić następujące polecenie, aby usunąć pule.</span><span class="sxs-lookup"><span data-stu-id="a6279-122">After you run the above sample script, run the following command to delete the pools.</span></span>
```azurecli
az batch pool delete --pool-id mypool-windows
az batch pool delete --pool-id mypool-linux
```

## <a name="script-explanation"></a><span data-ttu-id="a6279-123">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="a6279-123">Script explanation</span></span>

<span data-ttu-id="a6279-124">Ten skrypt używa następujących poleceń do tworzenia i modyfikowania pule partii.</span><span class="sxs-lookup"><span data-stu-id="a6279-124">This script uses the following commands to create and manipulate Batch pools.</span></span>
<span data-ttu-id="a6279-125">Każde polecenie w tabeli łącza do dokumentacji specyficzne dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="a6279-125">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="a6279-126">Polecenie</span><span class="sxs-lookup"><span data-stu-id="a6279-126">Command</span></span> | <span data-ttu-id="a6279-127">Uwagi</span><span class="sxs-lookup"><span data-stu-id="a6279-127">Notes</span></span> |
|---|---|
| [<span data-ttu-id="a6279-128">AZ logowanie się na koncie usługi partia zadań</span><span class="sxs-lookup"><span data-stu-id="a6279-128">az batch account login</span></span>](https://docs.microsoft.com/cli/azure/batch/account#login) | <span data-ttu-id="a6279-129">Uwierzytelnić konta usługi partia zadań.</span><span class="sxs-lookup"><span data-stu-id="a6279-129">Authenticate against a Batch account.</span></span>  |
| [<span data-ttu-id="a6279-130">Lista zbiorcza az partii aplikacji</span><span class="sxs-lookup"><span data-stu-id="a6279-130">az batch application summary list</span></span>](https://docs.microsoft.com/cli/azure/batch/application/summary#list) | <span data-ttu-id="a6279-131">Lista dostępnych aplikacji w ramach konta usługi partia zadań.</span><span class="sxs-lookup"><span data-stu-id="a6279-131">List the available applications in the Batch account.</span></span>  |
| [<span data-ttu-id="a6279-132">Tworzenie puli partii az</span><span class="sxs-lookup"><span data-stu-id="a6279-132">az batch pool create</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#create) | <span data-ttu-id="a6279-133">Tworzenie puli maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="a6279-133">Create a pool of VMs.</span></span>  |
| [<span data-ttu-id="a6279-134">zestaw puli partii az</span><span class="sxs-lookup"><span data-stu-id="a6279-134">az batch pool set</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#set) | <span data-ttu-id="a6279-135">Zaktualizuj właściwości puli.</span><span class="sxs-lookup"><span data-stu-id="a6279-135">Update properties of a pool.</span></span>  |
| [<span data-ttu-id="a6279-136">Lista węzła — agent-jednostki SKU puli partii az</span><span class="sxs-lookup"><span data-stu-id="a6279-136">az batch pool node-agent-skus list</span></span>](https://docs.microsoft.com/cli/azure/batch/pool/node-agent-skus#list) | <span data-ttu-id="a6279-137">Agent dostępnego węzła listy jednostki SKU i informacje o obrazie.</span><span class="sxs-lookup"><span data-stu-id="a6279-137">List available node agent SKUs and image information.</span></span>  |
| [<span data-ttu-id="a6279-138">Zmiana rozmiaru puli partii az</span><span class="sxs-lookup"><span data-stu-id="a6279-138">az batch pool resize</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#resize) | <span data-ttu-id="a6279-139">Zmień rozmiar liczba uruchomionych maszyn wirtualnych w określonej puli.</span><span class="sxs-lookup"><span data-stu-id="a6279-139">Resize the number of running VMs in the specified pool.</span></span>  |
| [<span data-ttu-id="a6279-140">Pokaż puli partii az</span><span class="sxs-lookup"><span data-stu-id="a6279-140">az batch pool show</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#show) | <span data-ttu-id="a6279-141">Wyświetl właściwości puli.</span><span class="sxs-lookup"><span data-stu-id="a6279-141">Display the properties of a pool.</span></span>  |
| [<span data-ttu-id="a6279-142">Usuwanie puli partii az</span><span class="sxs-lookup"><span data-stu-id="a6279-142">az batch pool delete</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#delete) | <span data-ttu-id="a6279-143">Usuń określoną pulę.</span><span class="sxs-lookup"><span data-stu-id="a6279-143">Delete the specified pool.</span></span>  |
| [<span data-ttu-id="a6279-144">Włączanie automatycznego skalowania puli partii az</span><span class="sxs-lookup"><span data-stu-id="a6279-144">az batch pool autoscale enable</span></span>](https://docs.microsoft.com/cli/azure/batch/pool/autoscale#enable) | <span data-ttu-id="a6279-145">Włącz automatyczne skalowanie w puli i zastosować formułę.</span><span class="sxs-lookup"><span data-stu-id="a6279-145">Enable auto-scaling on a pool and apply a formula.</span></span>  |
| [<span data-ttu-id="a6279-146">wyłączanie automatycznego skalowania puli partii az</span><span class="sxs-lookup"><span data-stu-id="a6279-146">az batch pool autoscale disable</span></span>](https://docs.microsoft.com/cli/azure/batch/pool/autoscale#disable) | <span data-ttu-id="a6279-147">Wyłącz automatyczne skalowanie w puli.</span><span class="sxs-lookup"><span data-stu-id="a6279-147">Disable auto-scaling on a pool.</span></span>  |
| [<span data-ttu-id="a6279-148">AZ partii węzła listy</span><span class="sxs-lookup"><span data-stu-id="a6279-148">az batch node list</span></span>](https://docs.microsoft.com/cli/azure/batch/node#list) | <span data-ttu-id="a6279-149">Wyświetl listę wszystkich węźle obliczeń w określonej puli.</span><span class="sxs-lookup"><span data-stu-id="a6279-149">List all the compute node in the specified pool.</span></span>  |
| [<span data-ttu-id="a6279-150">ponowny rozruch węzła partii az</span><span class="sxs-lookup"><span data-stu-id="a6279-150">az batch node reboot</span></span>](https://docs.microsoft.com/cli/azure/batch/node#reboot) | <span data-ttu-id="a6279-151">Ponowny rozruch węzła obliczeniowego określony.</span><span class="sxs-lookup"><span data-stu-id="a6279-151">Reboot the specified compute node.</span></span>  |
| [<span data-ttu-id="a6279-152">Usuń węzeł partii az</span><span class="sxs-lookup"><span data-stu-id="a6279-152">az batch node delete</span></span>](https://docs.microsoft.com/cli/azure/batch/node#delete) | <span data-ttu-id="a6279-153">Usuń węzły wymienionych z określonej puli.</span><span class="sxs-lookup"><span data-stu-id="a6279-153">Delete the listed nodes from the specified pool.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="a6279-154">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a6279-154">Next steps</span></span>

<span data-ttu-id="a6279-155">Aby uzyskać więcej informacji dotyczących interfejsu wiersza polecenia Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a6279-155">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="a6279-156">Dodatkowe przykłady skryptów partii interfejsu wiersza polecenia można znaleźć w [dokumentacji interfejsu wiersza polecenia Azure partii](../batch-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="a6279-156">Additional Batch CLI script samples can be found in the [Azure Batch CLI documentation](../batch-cli-samples.md).</span></span>

