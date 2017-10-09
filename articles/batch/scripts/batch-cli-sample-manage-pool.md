---
title: "aaaAzure przykładowym skrypcie interfejsu wiersza polecenia — Zarządzanie pule w partii | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 6c9ca9515565aff42752231a080943be8e4c810b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-batch-pools-with-azure-cli"></a><span data-ttu-id="33183-103">Zarządzanie pule partii zadań Azure z wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="33183-103">Managing Azure Batch pools with Azure CLI</span></span>

<span data-ttu-id="33183-104">Te skrypt przedstawiono niektóre hello narzędzi dostępnych w ramach hello toocreate wiersza polecenia platformy Azure i Zarządzanie pulami węzłów obliczeniowych w hello usługi partia zadań Azure.</span><span class="sxs-lookup"><span data-stu-id="33183-104">These script demonstrates some of hello tools available in hello Azure CLI toocreate and manage pools of compute nodes in hello Azure Batch service.</span></span>

> [!NOTE]
> <span data-ttu-id="33183-105">polecenia Hello w tym przykładzie Tworzenie maszyn wirtualnych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="33183-105">hello commands in this sample create Azure virtual machines.</span></span> <span data-ttu-id="33183-106">Działających maszyn wirtualnych będą naliczane opłaty tooyour konta.</span><span class="sxs-lookup"><span data-stu-id="33183-106">Running VMs will accrue charges tooyour account.</span></span> <span data-ttu-id="33183-107">toominimize tych opłat, Usuń hello maszyn wirtualnych, po zakończeniu uruchomionych próbki hello.</span><span class="sxs-lookup"><span data-stu-id="33183-107">toominimize these charges, delete hello VMs once you're done running hello sample.</span></span> <span data-ttu-id="33183-108">Zobacz [wyczyścić pule](#clean-up-pools).</span><span class="sxs-lookup"><span data-stu-id="33183-108">See [Clean up pools](#clean-up-pools).</span></span>

<span data-ttu-id="33183-109">Pule partii można skonfigurować na dwa sposoby z konfiguracji usługi w chmurze (tylko system Windows) lub konfiguracji maszyny wirtualnej (z systemem Windows i Linux).</span><span class="sxs-lookup"><span data-stu-id="33183-109">Batch pools can be configured in two ways, either with a Cloud Services configuration (Windows only), or a Virtual Machine configuration (Windows and Linux).</span></span> <span data-ttu-id="33183-110">Przykładowe skrypty Hello poniżej pokazują, jak toocreate puli z obydwu konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="33183-110">hello sample scripts below show how toocreate pools with both configurations.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="33183-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="33183-111">Prerequisites</span></span>

- <span data-ttu-id="33183-112">Zainstaluj hello wiersza polecenia platformy Azure przy użyciu hello instrukcjami hello [Przewodnik instalacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/install-azure-cli), jeśli nie ma jeszcze zrobione.</span><span class="sxs-lookup"><span data-stu-id="33183-112">Install hello Azure CLI using hello instructions provided in hello [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), if you have not already done so.</span></span>
- <span data-ttu-id="33183-113">Tworzenie konta usługi partia zadań, jeśli nie został wcześniej.</span><span class="sxs-lookup"><span data-stu-id="33183-113">Create a Batch account if you don't already have one.</span></span> <span data-ttu-id="33183-114">Zobacz [Tworzenie konta usługi partia zadań z hello Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) przykładowego skryptu, który tworzy konto.</span><span class="sxs-lookup"><span data-stu-id="33183-114">See [Create a Batch account with hello Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) for a sample script that creates an account.</span></span>
- <span data-ttu-id="33183-115">Jeśli nie zostało to jeszcze zrobione, należy skonfigurować toorun aplikacji z zadania uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="33183-115">Configure an application toorun from a start task if you haven't yet done so.</span></span> <span data-ttu-id="33183-116">Zobacz [Dodawanie tooAzure aplikacji partii zadań z wiersza polecenia platformy Azure](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) przykładowego skryptu, który tworzy aplikację i przekazuje tooAzure pakietu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="33183-116">See [Adding applications tooAzure Batch with Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) for a sample script that creates an application and uploads an application package tooAzure.</span></span>

## <a name="pool-with-cloud-service-configuration-sample-script"></a><span data-ttu-id="33183-117">Puli z skrypt przykładowy konfiguracji usługi chmury</span><span class="sxs-lookup"><span data-stu-id="33183-117">Pool with cloud service configuration sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/batch/manage-pool/manage-pool-windows.sh "Manage Cloud Services Pools")]

## <a name="pool-with-virtual-machine-configuration-sample-script"></a><span data-ttu-id="33183-118">Puli z skrypt przykładowy konfiguracji maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="33183-118">Pool with virtual machine configuration sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/batch/manage-pool/manage-pool-linux.sh "Manage Virtual Machine Pools")]

## <a name="clean-up-pools"></a><span data-ttu-id="33183-119">Oczyszczanie pul</span><span class="sxs-lookup"><span data-stu-id="33183-119">Clean up pools</span></span>

<span data-ttu-id="33183-120">Po uruchomieniu hello powyżej przykładowy skrypt należy uruchomić hello następujące polecenia toodelete hello pule.</span><span class="sxs-lookup"><span data-stu-id="33183-120">After you run hello above sample script, run hello following command toodelete hello pools.</span></span>
```azurecli
az batch pool delete --pool-id mypool-windows
az batch pool delete --pool-id mypool-linux
```

## <a name="script-explanation"></a><span data-ttu-id="33183-121">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="33183-121">Script explanation</span></span>

<span data-ttu-id="33183-122">Ten skrypt używa powitania po toocreate poleceń i manipulowania pule partii.</span><span class="sxs-lookup"><span data-stu-id="33183-122">This script uses hello following commands toocreate and manipulate Batch pools.</span></span>
<span data-ttu-id="33183-123">Każde polecenie w dokumentacji konkretnego toocommand łącza tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="33183-123">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="33183-124">Polecenie</span><span class="sxs-lookup"><span data-stu-id="33183-124">Command</span></span> | <span data-ttu-id="33183-125">Uwagi</span><span class="sxs-lookup"><span data-stu-id="33183-125">Notes</span></span> |
|---|---|
| [<span data-ttu-id="33183-126">AZ logowanie się na koncie usługi partia zadań</span><span class="sxs-lookup"><span data-stu-id="33183-126">az batch account login</span></span>](https://docs.microsoft.com/cli/azure/batch/account#login) | <span data-ttu-id="33183-127">Uwierzytelnić konta usługi partia zadań.</span><span class="sxs-lookup"><span data-stu-id="33183-127">Authenticate against a Batch account.</span></span>  |
| [<span data-ttu-id="33183-128">Lista zbiorcza az partii aplikacji</span><span class="sxs-lookup"><span data-stu-id="33183-128">az batch application summary list</span></span>](https://docs.microsoft.com/cli/azure/batch/application/summary#list) | <span data-ttu-id="33183-129">Lista dostępnych aplikacji hello w hello konta usługi partia zadań.</span><span class="sxs-lookup"><span data-stu-id="33183-129">List hello available applications in hello Batch account.</span></span>  |
| [<span data-ttu-id="33183-130">Tworzenie puli partii az</span><span class="sxs-lookup"><span data-stu-id="33183-130">az batch pool create</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#create) | <span data-ttu-id="33183-131">Tworzenie puli maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="33183-131">Create a pool of VMs.</span></span>  |
| [<span data-ttu-id="33183-132">zestaw puli partii az</span><span class="sxs-lookup"><span data-stu-id="33183-132">az batch pool set</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#set) | <span data-ttu-id="33183-133">Zaktualizuj właściwości puli.</span><span class="sxs-lookup"><span data-stu-id="33183-133">Update properties of a pool.</span></span>  |
| [<span data-ttu-id="33183-134">Lista węzła — agent-jednostki SKU puli partii az</span><span class="sxs-lookup"><span data-stu-id="33183-134">az batch pool node-agent-skus list</span></span>](https://docs.microsoft.com/cli/azure/batch/pool/node-agent-skus#list) | <span data-ttu-id="33183-135">Agent dostępnego węzła listy jednostki SKU i informacje o obrazie.</span><span class="sxs-lookup"><span data-stu-id="33183-135">List available node agent SKUs and image information.</span></span>  |
| [<span data-ttu-id="33183-136">Zmiana rozmiaru puli partii az</span><span class="sxs-lookup"><span data-stu-id="33183-136">az batch pool resize</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#resize) | <span data-ttu-id="33183-137">Podana liczba hello zmiany rozmiaru działających maszyn wirtualnych w hello puli.</span><span class="sxs-lookup"><span data-stu-id="33183-137">Resize hello number of running VMs in hello specified pool.</span></span>  |
| [<span data-ttu-id="33183-138">Pokaż puli partii az</span><span class="sxs-lookup"><span data-stu-id="33183-138">az batch pool show</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#show) | <span data-ttu-id="33183-139">Wyświetl właściwości hello puli.</span><span class="sxs-lookup"><span data-stu-id="33183-139">Display hello properties of a pool.</span></span>  |
| [<span data-ttu-id="33183-140">Usuwanie puli partii az</span><span class="sxs-lookup"><span data-stu-id="33183-140">az batch pool delete</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#delete) | <span data-ttu-id="33183-141">Usuń hello określonej puli.</span><span class="sxs-lookup"><span data-stu-id="33183-141">Delete hello specified pool.</span></span>  |
| [<span data-ttu-id="33183-142">Włączanie automatycznego skalowania puli partii az</span><span class="sxs-lookup"><span data-stu-id="33183-142">az batch pool autoscale enable</span></span>](https://docs.microsoft.com/cli/azure/batch/pool/autoscale#enable) | <span data-ttu-id="33183-143">Włącz automatyczne skalowanie w puli i zastosować formułę.</span><span class="sxs-lookup"><span data-stu-id="33183-143">Enable auto-scaling on a pool and apply a formula.</span></span>  |
| [<span data-ttu-id="33183-144">wyłączanie automatycznego skalowania puli partii az</span><span class="sxs-lookup"><span data-stu-id="33183-144">az batch pool autoscale disable</span></span>](https://docs.microsoft.com/cli/azure/batch/pool/autoscale#disable) | <span data-ttu-id="33183-145">Wyłącz automatyczne skalowanie w puli.</span><span class="sxs-lookup"><span data-stu-id="33183-145">Disable auto-scaling on a pool.</span></span>  |
| [<span data-ttu-id="33183-146">AZ partii węzła listy</span><span class="sxs-lookup"><span data-stu-id="33183-146">az batch node list</span></span>](https://docs.microsoft.com/cli/azure/batch/node#list) | <span data-ttu-id="33183-147">Lista wszystkich hello węźle obliczeń w hello określonej puli.</span><span class="sxs-lookup"><span data-stu-id="33183-147">List all hello compute node in hello specified pool.</span></span>  |
| [<span data-ttu-id="33183-148">ponowny rozruch węzła partii az</span><span class="sxs-lookup"><span data-stu-id="33183-148">az batch node reboot</span></span>](https://docs.microsoft.com/cli/azure/batch/node#reboot) | <span data-ttu-id="33183-149">Ponowny rozruch węzła obliczeniowego określonego hello.</span><span class="sxs-lookup"><span data-stu-id="33183-149">Reboot hello specified compute node.</span></span>  |
| [<span data-ttu-id="33183-150">Usuń węzeł partii az</span><span class="sxs-lookup"><span data-stu-id="33183-150">az batch node delete</span></span>](https://docs.microsoft.com/cli/azure/batch/node#delete) | <span data-ttu-id="33183-151">Usuń węzły hello wymienione z hello określone puli.</span><span class="sxs-lookup"><span data-stu-id="33183-151">Delete hello listed nodes from hello specified pool.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="33183-152">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="33183-152">Next steps</span></span>

<span data-ttu-id="33183-153">Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="33183-153">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="33183-154">Dodatkowe przykłady skryptów partii interfejsu wiersza polecenia można znaleźć w hello [dokumentacji interfejsu wiersza polecenia Azure partii](../batch-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="33183-154">Additional Batch CLI script samples can be found in hello [Azure Batch CLI documentation](../batch-cli-samples.md).</span></span>

