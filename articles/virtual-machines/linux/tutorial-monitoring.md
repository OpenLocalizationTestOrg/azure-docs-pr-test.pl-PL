---
title: Monitorowanie maszyn wirtualnych systemu Linux na platformie Azure | Dokumentacja firmy Microsoft
description: "Informacje o sposobie monitorowania diagnostyki rozruchu i metryki wydajności na maszynie wirtualnej systemu Linux na platformie Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/08/2017
ms.author: davidmu
ms.custom: mvc
ms.openlocfilehash: 3fe8390e88e609b57a462e066f972346f8e8730e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-monitor-a-linux-virtual-machine-in-azure"></a><span data-ttu-id="9f759-103">Jak monitorować maszyny wirtualnej systemu Linux na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="9f759-103">How to monitor a Linux virtual machine in Azure</span></span>

<span data-ttu-id="9f759-104">Aby zapewnić, że działają poprawnie maszyn wirtualnych (VM) na platformie Azure, możesz przejrzeć diagnostyki rozruchu i metryk wydajności.</span><span class="sxs-lookup"><span data-stu-id="9f759-104">To ensure your virtual machines (VMs) in Azure are running correctly, you can review boot diagnostics and performance metrics.</span></span> <span data-ttu-id="9f759-105">Ten samouczek zawiera informacje na temat wykonywania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="9f759-105">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9f759-106">Włącz diagnostykę rozruchu na maszynie Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="9f759-106">Enable boot diagnostics on the VM</span></span>
> * <span data-ttu-id="9f759-107">Wyświetlanie diagnostyki rozruchu</span><span class="sxs-lookup"><span data-stu-id="9f759-107">View boot diagnostics</span></span>
> * <span data-ttu-id="9f759-108">Wyświetlaj metryki hosta</span><span class="sxs-lookup"><span data-stu-id="9f759-108">View host metrics</span></span>
> * <span data-ttu-id="9f759-109">Włącz diagnostykę rozszerzenie na maszynie Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="9f759-109">Enable diagnostics extension on the VM</span></span>
> * <span data-ttu-id="9f759-110">Wyświetlaj metryki maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="9f759-110">View VM metrics</span></span>
> * <span data-ttu-id="9f759-111">Tworzenie alertów w oparciu metryki diagnostycznych</span><span class="sxs-lookup"><span data-stu-id="9f759-111">Create alerts based on diagnostic metrics</span></span>
> * <span data-ttu-id="9f759-112">Skonfiguruj zaawansowane monitorowanie</span><span class="sxs-lookup"><span data-stu-id="9f759-112">Set up advanced monitoring</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="9f759-113">Jeśli wybierzesz do zainstalowania i używania interfejsu wiersza polecenia lokalnie, w tym samouczku wymaga używasz interfejsu wiersza polecenia Azure w wersji 2.0.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="9f759-113">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="9f759-114">Uruchom polecenie `az --version`, aby dowiedzieć się, jaka wersja jest używana.</span><span class="sxs-lookup"><span data-stu-id="9f759-114">Run `az --version` to find the version.</span></span> <span data-ttu-id="9f759-115">Jeśli konieczna będzie instalacja lub uaktualnienie, zobacz [Instalowanie interfejsu wiersza polecenia platformy Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="9f759-115">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-vm"></a><span data-ttu-id="9f759-116">Tworzenie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="9f759-116">Create VM</span></span>

<span data-ttu-id="9f759-117">Aby wyświetlić dane diagnostyczne i metryki w akcji, należy maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="9f759-117">To see diagnostics and metrics in action, you need a VM.</span></span> <span data-ttu-id="9f759-118">Najpierw utwórz nową grupę zasobów o [Tworzenie grupy az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="9f759-118">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="9f759-119">Poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroupMonitor* w *eastus* lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="9f759-119">The following example creates a resource group named *myResourceGroupMonitor* in the *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroupMonitor --location eastus
```

<span data-ttu-id="9f759-120">Teraz Utwórz maszynę Wirtualną z [tworzenia maszyny wirtualnej az](https://docs.microsoft.com/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="9f759-120">Now create a VM with [az vm create](https://docs.microsoft.com/cli/azure/vm#create).</span></span> <span data-ttu-id="9f759-121">Poniższy przykład tworzy Maszynę wirtualną o nazwie *myVM*:</span><span class="sxs-lookup"><span data-stu-id="9f759-121">The following example creates a VM named *myVM*:</span></span>

```azurecli-interactive 
az vm create \
  --resource-group myResourceGroupMonitor \
  --name myVM \
  --image UbuntuLTS \
  --admin-username azureuser \
  --generate-ssh-keys
```

## <a name="enable-boot-diagnostics"></a><span data-ttu-id="9f759-122">Włącz diagnostykę rozruchu</span><span class="sxs-lookup"><span data-stu-id="9f759-122">Enable boot diagnostics</span></span>

<span data-ttu-id="9f759-123">Jak rozruchu maszyn wirtualnych systemu Linux, rozszerzenia diagnostyki rozruchu przechwytuje dane wyjściowe rozruchu i zapisuje go w magazynie Azure.</span><span class="sxs-lookup"><span data-stu-id="9f759-123">As Linux VMs boot, the boot diagnostic extension captures boot output and stores it in Azure storage.</span></span> <span data-ttu-id="9f759-124">Te dane mogą służyć do rozwiązywania problemów rozruchu maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="9f759-124">This data can be used to troubleshoot VM boot issues.</span></span> <span data-ttu-id="9f759-125">Diagnostyki rozruchu nie są automatycznie włączone, podczas tworzenia maszyny Wirtualnej systemu Linux przy użyciu wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9f759-125">Boot diagnostics are not automatically enabled when you create a Linux VM using the Azure CLI.</span></span>

<span data-ttu-id="9f759-126">Przed włączeniem diagnostyki rozruchu, konta magazynu musi być utworzony do przechowywania dzienników rozruchu.</span><span class="sxs-lookup"><span data-stu-id="9f759-126">Before enabling boot diagnostics, a storage account needs to be created for storing boot logs.</span></span> <span data-ttu-id="9f759-127">Konta magazynu musi mieć globalnie unikatowej nazwy należeć do zakresu od 3 do 24 znaków i musi zawierać tylko cyfry i małe litery.</span><span class="sxs-lookup"><span data-stu-id="9f759-127">Storage accounts must have a globally unique name, be between 3 and 24 characters, and must contain only numbers and lowercase letters.</span></span> <span data-ttu-id="9f759-128">Utwórz konto magazynu z [Tworzenie konta magazynu az](/cli/azure/storage/account#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="9f759-128">Create a storage account with the [az storage account create](/cli/azure/storage/account#create) command.</span></span> <span data-ttu-id="9f759-129">W tym przykładzie losowy ciąg służy do tworzenia nazwy konta magazynu unikatowy.</span><span class="sxs-lookup"><span data-stu-id="9f759-129">In this example, a random string is used to create a unique storage account name.</span></span> 

```azurecli-interactive 
storageacct=mydiagdata$RANDOM

az storage account create \
  --resource-group myResourceGroupMonitor \
  --name $storageacct \
  --sku Standard_LRS \
  --location eastus
```

<span data-ttu-id="9f759-130">Podczas włączania diagnostyki rozruchu, wymagany jest identyfikator URI do kontenera magazynu obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="9f759-130">When enabling boot diagnostics, the URI to the blob storage container is needed.</span></span> <span data-ttu-id="9f759-131">Polecenie wysyła zapytanie do konta magazynu, aby powrócić do tego identyfikatora URI.</span><span class="sxs-lookup"><span data-stu-id="9f759-131">The following command queries the storage account to return this URI.</span></span> <span data-ttu-id="9f759-132">Wartość identyfikatora URI jest przechowywana w nazwach zmiennych *bloburi*, która jest używana w następnym kroku.</span><span class="sxs-lookup"><span data-stu-id="9f759-132">The URI value is stored in a variable names *bloburi*, which is used in the next step.</span></span>

```azurecli-interactive 
bloburi=$(az storage account show --resource-group myResourceGroupMonitor --name $storageacct --query 'primaryEndpoints.blob' -o tsv)
```

<span data-ttu-id="9f759-133">Teraz Włącz diagnostyki rozruchu z [włączyć diagnostyki rozruchu az wirtualna](https://docs.microsoft.com/cli/azure/vm/boot-diagnostics#enable).</span><span class="sxs-lookup"><span data-stu-id="9f759-133">Now enable boot diagnostics with [az vm boot-diagnostics enable](https://docs.microsoft.com/cli/azure/vm/boot-diagnostics#enable).</span></span> <span data-ttu-id="9f759-134">`--storage` Wartość jest obiektu blob identyfikatora URI zebrane w poprzednim kroku.</span><span class="sxs-lookup"><span data-stu-id="9f759-134">The `--storage` value is the blob URI collected in the previous step.</span></span>

```azurecli-interactive 
az vm boot-diagnostics enable \
  --resource-group myResourceGroupMonitor \
  --name myVM \
  --storage $bloburi
```


## <a name="view-boot-diagnostics"></a><span data-ttu-id="9f759-135">Wyświetlanie diagnostyki rozruchu</span><span class="sxs-lookup"><span data-stu-id="9f759-135">View boot diagnostics</span></span>

<span data-ttu-id="9f759-136">Po włączeniu diagnostyki rozruchu zawsze zatrzymać i uruchomić maszynę Wirtualną, informacje na temat procesu rozruchu są zapisywane w pliku dziennika.</span><span class="sxs-lookup"><span data-stu-id="9f759-136">When boot diagnostics are enabled, each time you stop and start the VM, information about the boot process is written to a log file.</span></span> <span data-ttu-id="9f759-137">W tym przykładzie najpierw cofnąć maszyny Wirtualnej z [deallocate wirtualna az](/cli/azure/vm#deallocate) polecenia w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="9f759-137">For this example, first deallocate the VM with the [az vm deallocate](/cli/azure/vm#deallocate) command as follows:</span></span>

```azurecli-interactive 
az vm deallocate --resource-group myResourceGroupMonitor --name myVM
```

<span data-ttu-id="9f759-138">Teraz uruchom maszynę Wirtualną z [uruchomienia maszyny wirtualnej az]( /cli/azure/vm#stop) polecenia w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="9f759-138">Now start the VM with the [az vm start]( /cli/azure/vm#stop) command as follows:</span></span>

```azurecli-interactive 
az vm start --resource-group myResourceGroupMonitor --name myVM
```

<span data-ttu-id="9f759-139">Można uzyskać danych diagnostyki rozruchu dla *myVM* z [az maszyny wirtualnej diagnostyki rozruchu get rozruchu — dziennik](https://docs.microsoft.com/cli/azure/vm/boot-diagnostics#get-boot-log) polecenia w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="9f759-139">You can get the boot diagnostic data for *myVM* with the [az vm boot-diagnostics get-boot-log](https://docs.microsoft.com/cli/azure/vm/boot-diagnostics#get-boot-log) command as follows:</span></span>

```azurecli-interactive 
az vm boot-diagnostics get-boot-log --resource-group myResourceGroupMonitor --name myVM
```


## <a name="view-host-metrics"></a><span data-ttu-id="9f759-140">Wyświetlaj metryki hosta</span><span class="sxs-lookup"><span data-stu-id="9f759-140">View host metrics</span></span>

<span data-ttu-id="9f759-141">Maszynę wirtualną systemu Linux zawiera dedykowany hosta na platformie Azure, która współdziała ona z.</span><span class="sxs-lookup"><span data-stu-id="9f759-141">A Linux VM has a dedicated host in Azure that it interacts with.</span></span> <span data-ttu-id="9f759-142">Metryki są automatycznie pobierane dla hosta i mogą być wyświetlane w portalu Azure w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="9f759-142">Metrics are automatically collected for the host and can be viewed in the Azure portal as follows:</span></span>

1. <span data-ttu-id="9f759-143">W portalu Azure kliknij **grup zasobów**, wybierz pozycję **myResourceGroupMonitor**, a następnie wybierz **myVM** na liście zasobów.</span><span class="sxs-lookup"><span data-stu-id="9f759-143">In the Azure portal, click **Resource Groups**, select **myResourceGroupMonitor**, and then select **myVM** in the resource list.</span></span>
1. <span data-ttu-id="9f759-144">Aby zobaczyć, jak działa hosta maszyny Wirtualnej, kliknij **metryki** w bloku maszyny Wirtualnej, następnie wybierz jedno z *[Host]* metryki w obszarze **dostępne metryki**.</span><span class="sxs-lookup"><span data-stu-id="9f759-144">To see how the host VM is performing, click **Metrics** on the VM blade, then select any of the *[Host]* metrics under **Available metrics**.</span></span>

    ![Wyświetlaj metryki hosta](./media/tutorial-monitoring/monitor-host-metrics.png)


## <a name="install-diagnostics-extension"></a><span data-ttu-id="9f759-146">Zainstaluj rozszerzenie diagnostyki</span><span class="sxs-lookup"><span data-stu-id="9f759-146">Install diagnostics extension</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9f759-147">Ten dokument zawiera opis wersji 2.3 rozszerzenia diagnostyczne systemu Linux, która została wycofana.</span><span class="sxs-lookup"><span data-stu-id="9f759-147">This document describes version 2.3 of the Linux Diagnostic Extension, which has been deprecated.</span></span> <span data-ttu-id="9f759-148">Wersja 2.3 będzie obsługiwana do 30 czerwca 2018.</span><span class="sxs-lookup"><span data-stu-id="9f759-148">Version 2.3 will be supported until June 30, 2018.</span></span>
>
> <span data-ttu-id="9f759-149">Zamiast tego można włączyć w wersji 3.0 rozszerzenia diagnostyczne systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="9f759-149">Version 3.0 of the Linux Diagnostic Extension can be enabled instead.</span></span> <span data-ttu-id="9f759-150">Aby uzyskać więcej informacji, zobacz [dokumentacji](./diagnostic-extension.md).</span><span class="sxs-lookup"><span data-stu-id="9f759-150">For more information, see [the documentation](./diagnostic-extension.md).</span></span>

<span data-ttu-id="9f759-151">Metryki podstawowych hostów są dostępne, ale bardziej szczegółowe i metryki specyficzne dla maszyny Wirtualnej, można, należy zainstalować rozszerzenie diagnostycznych platformy Azure na maszynie Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="9f759-151">The basic host metrics are available, but to see more granular and VM-specific metrics, you to need to install the Azure diagnostics extension on the VM.</span></span> <span data-ttu-id="9f759-152">Rozszerzenia diagnostyki Azure umożliwia dodatkowe funkcje monitorowania i dane diagnostyczne mają zostać pobrane z maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="9f759-152">The Azure diagnostics extension allows additional monitoring and diagnostics data to be retrieved from the VM.</span></span> <span data-ttu-id="9f759-153">Możesz wyświetlić te metryki wydajności i tworzyć alerty oparte na sposób wykonywania maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="9f759-153">You can view these performance metrics and create alerts based on how the VM performs.</span></span> <span data-ttu-id="9f759-154">Rozszerzenia diagnostycznych jest zainstalowany za pośrednictwem portalu Azure w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="9f759-154">The diagnostic extension is installed through the Azure portal as follows:</span></span>

1. <span data-ttu-id="9f759-155">W portalu Azure kliknij **grup zasobów**, wybierz pozycję **myResourceGroup**, a następnie wybierz **myVM** na liście zasobów.</span><span class="sxs-lookup"><span data-stu-id="9f759-155">In the Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in the resource list.</span></span>
1. <span data-ttu-id="9f759-156">Kliknij przycisk **ustawienia diagnostyki**.</span><span class="sxs-lookup"><span data-stu-id="9f759-156">Click **Diagnosis settings**.</span></span> <span data-ttu-id="9f759-157">Lista wskazuje, że *diagnostyki rozruchu* są już włączone w poprzedniej sekcji.</span><span class="sxs-lookup"><span data-stu-id="9f759-157">The list shows that *Boot diagnostics* are already enabled from the previous section.</span></span> <span data-ttu-id="9f759-158">Kliknij pole wyboru dla *podstawowe metryki*.</span><span class="sxs-lookup"><span data-stu-id="9f759-158">Click the check box for *Basic metrics*.</span></span>
1. <span data-ttu-id="9f759-159">W *konta magazynu* sekcji, wyszukaj i wybierz *mydiagdata [1234]* konto utworzone w poprzedniej sekcji.</span><span class="sxs-lookup"><span data-stu-id="9f759-159">In the *Storage account* section, browse to and select the *mydiagdata[1234]* account created in the previous section.</span></span>
1. <span data-ttu-id="9f759-160">Kliknij przycisk **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="9f759-160">Click the **Save** button.</span></span>

    ![Wyświetlaj metryki diagnostycznych](./media/tutorial-monitoring/enable-diagnostics-extension.png)


## <a name="view-vm-metrics"></a><span data-ttu-id="9f759-162">Wyświetlaj metryki maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="9f759-162">View VM metrics</span></span>

<span data-ttu-id="9f759-163">Metryki maszyny Wirtualnej można wyświetlać w taki sam sposób, aby wyświetlić hosta metryki maszyny Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="9f759-163">You can view the VM metrics in the same way that you viewed the host VM metrics:</span></span>

1. <span data-ttu-id="9f759-164">W portalu Azure kliknij **grup zasobów**, wybierz pozycję **myResourceGroup**, a następnie wybierz **myVM** na liście zasobów.</span><span class="sxs-lookup"><span data-stu-id="9f759-164">In the Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in the resource list.</span></span>
1. <span data-ttu-id="9f759-165">Aby zobaczyć, jak działa maszyny Wirtualnej, kliknij **metryki** w bloku maszyny Wirtualnej, a następnie wybierz jedno z metryki diagnostyki w obszarze **dostępne metryki**.</span><span class="sxs-lookup"><span data-stu-id="9f759-165">To see how the VM is performing, click **Metrics** on the VM blade, and then select any of the diagnostics metrics under **Available metrics**.</span></span>

    ![Wyświetlaj metryki maszyny Wirtualnej](./media/tutorial-monitoring/monitor-vm-metrics.png)


## <a name="create-alerts"></a><span data-ttu-id="9f759-167">Tworzenie alertów</span><span class="sxs-lookup"><span data-stu-id="9f759-167">Create alerts</span></span>

<span data-ttu-id="9f759-168">Można tworzyć alertów w oparciu metryki dotyczące wydajności.</span><span class="sxs-lookup"><span data-stu-id="9f759-168">You can create alerts based on specific performance metrics.</span></span> <span data-ttu-id="9f759-169">Alerty można powiadomić o, gdy średniego użycia procesora CPU przekracza określonego progu lub wolnego miejsca na dysku spada poniżej pewnego, np.</span><span class="sxs-lookup"><span data-stu-id="9f759-169">Alerts can be used to notify you when average CPU usage exceeds a certain threshold or available free disk space drops below a certain amount, for example.</span></span> <span data-ttu-id="9f759-170">Alerty są wyświetlane w portalu Azure lub mogą być wysyłane za pośrednictwem poczty e-mail.</span><span class="sxs-lookup"><span data-stu-id="9f759-170">Alerts are displayed in the Azure portal or can be sent via email.</span></span> <span data-ttu-id="9f759-171">W odpowiedzi na alerty generowane może także wyzwolić elementu runbook usługi Automatyzacja Azure lub usługi Azure Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="9f759-171">You can also trigger Azure Automation runbooks or Azure Logic Apps in response to alerts being generated.</span></span>

<span data-ttu-id="9f759-172">Poniższy przykład tworzy alert dla średniego użycia procesora CPU.</span><span class="sxs-lookup"><span data-stu-id="9f759-172">The following example creates an alert for average CPU usage.</span></span>

1. <span data-ttu-id="9f759-173">W portalu Azure kliknij **grup zasobów**, wybierz pozycję **myResourceGroup**, a następnie wybierz **myVM** na liście zasobów.</span><span class="sxs-lookup"><span data-stu-id="9f759-173">In the Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in the resource list.</span></span>
2. <span data-ttu-id="9f759-174">Kliknij przycisk **reguły alertów** w bloku maszyny Wirtualnej, następnie kliknij polecenie **Dodaj alert metryki** w górnej części bloku alerty.</span><span class="sxs-lookup"><span data-stu-id="9f759-174">Click **Alert rules** on the VM blade, then click **Add metric alert** across the top of the alerts blade.</span></span>
4. <span data-ttu-id="9f759-175">Podaj **nazwa** alertu, takie jak *myAlertRule*</span><span class="sxs-lookup"><span data-stu-id="9f759-175">Provide a **Name** for your alert, such as *myAlertRule*</span></span>
5. <span data-ttu-id="9f759-176">Do wyzwolenia alertu, gdy procent użycia procesora CPU przekracza 1.0 przez pięć minut, pozostaw wszystkie inne wartości domyślne wybrane.</span><span class="sxs-lookup"><span data-stu-id="9f759-176">To trigger an alert when CPU percentage exceeds 1.0 for five minutes, leave all the other defaults selected.</span></span>
6. <span data-ttu-id="9f759-177">Opcjonalnie zaznacz pole wyboru, aby uzyskać *E-mail właściciele, współautorzy i czytelnicy* do wysyłania powiadomień e-mail.</span><span class="sxs-lookup"><span data-stu-id="9f759-177">Optionally, check the box for *Email owners, contributors, and readers* to send email notification.</span></span> <span data-ttu-id="9f759-178">Domyślne działanie jest obecne powiadomienia w portalu.</span><span class="sxs-lookup"><span data-stu-id="9f759-178">The default action is to present a notification in the portal.</span></span>
7. <span data-ttu-id="9f759-179">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="9f759-179">Click the **OK** button.</span></span>


## <a name="advanced-monitoring"></a><span data-ttu-id="9f759-180">Zaawansowane monitorowanie</span><span class="sxs-lookup"><span data-stu-id="9f759-180">Advanced monitoring</span></span> 

<span data-ttu-id="9f759-181">Możliwość bardziej zaawansowane monitorowanie maszyny wirtualnej za pomocą [Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview).</span><span class="sxs-lookup"><span data-stu-id="9f759-181">You can do more advanced monitoring of your VM by using [Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview).</span></span> <span data-ttu-id="9f759-182">Jeśli nie zostało to jeszcze zrobione, należy zarejestrować się w celu [bezpłatnej wersji próbnej](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial) programu Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="9f759-182">If you haven't already done so, you can sign up for a [free trial](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial) of Operations Management Suite.</span></span>

<span data-ttu-id="9f759-183">Jeśli masz dostęp do portalu OMS klucz obszaru roboczego i identyfikator obszaru roboczego można znaleźć w bloku ustawień.</span><span class="sxs-lookup"><span data-stu-id="9f759-183">When you have access to the OMS portal, you can find the workspace key and workspace identifier on the Settings blade.</span></span> <span data-ttu-id="9f759-184">Zastąp < klucz obszaru roboczego > i < identyfikator obszaru roboczego > wartościami dla z Twojej OMS można użyć obszaru roboczego, a następnie możesz **zestaw rozszerzenia maszyny wirtualnej az** można dodać rozszerzenia OMS do maszyny Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="9f759-184">Replace <workspace-key> and <workspace-id> with the values for from your OMS workspace and then you can use **az vm extension set** to add the OMS extension to the VM:</span></span>

```azurecli-interactive 
az vm extension set \
  --resource-group myResourceGroupMonitor \
  --vm-name myVM \
  --name OmsAgentForLinux \
  --publisher Microsoft.EnterpriseCloud.Monitoring \
  --version 1.3 \
  --protected-settings '{"workspaceKey": "<workspace-key>"}' \
  --settings '{"workspaceId": "<workspace-id>"}'
```

<span data-ttu-id="9f759-185">W bloku dziennika wyszukiwania portalu OMS, powinna zostać wyświetlona *myVM* takich jak co przedstawiono na poniższej ilustracji:</span><span class="sxs-lookup"><span data-stu-id="9f759-185">On the Log Search blade of the OMS portal, you should see *myVM* such as what is shown in the following picture:</span></span>

![Blok OMS](./media/tutorial-monitoring/tutorial-monitor-oms.png)

## <a name="next-steps"></a><span data-ttu-id="9f759-187">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9f759-187">Next steps</span></span>

<span data-ttu-id="9f759-188">W tym samouczku został skonfigurowany i przejrzeć maszyn wirtualnych w Centrum zabezpieczeń Azure.</span><span class="sxs-lookup"><span data-stu-id="9f759-188">In this tutorial, you configured and reviewed VMs with Azure Security Center.</span></span> <span data-ttu-id="9f759-189">Możesz przedstawiono sposób do:</span><span class="sxs-lookup"><span data-stu-id="9f759-189">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9f759-190">Włącz diagnostykę rozruchu na maszynie Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="9f759-190">Enable boot diagnostics on the VM</span></span>
> * <span data-ttu-id="9f759-191">Wyświetlanie diagnostyki rozruchu</span><span class="sxs-lookup"><span data-stu-id="9f759-191">View boot diagnostics</span></span>
> * <span data-ttu-id="9f759-192">Wyświetlaj metryki hosta</span><span class="sxs-lookup"><span data-stu-id="9f759-192">View host metrics</span></span>
> * <span data-ttu-id="9f759-193">Włącz diagnostykę rozszerzenie na maszynie Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="9f759-193">Enable diagnostics extension on the VM</span></span>
> * <span data-ttu-id="9f759-194">Wyświetlaj metryki maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="9f759-194">View VM metrics</span></span>
> * <span data-ttu-id="9f759-195">Tworzenie alertów w oparciu metryki diagnostycznych</span><span class="sxs-lookup"><span data-stu-id="9f759-195">Create alerts based on diagnostic metrics</span></span>
> * <span data-ttu-id="9f759-196">Skonfiguruj zaawansowane monitorowanie</span><span class="sxs-lookup"><span data-stu-id="9f759-196">Set up advanced monitoring</span></span>

<span data-ttu-id="9f759-197">Przejdź do następnego samouczka, aby dowiedzieć się więcej na temat Centrum zabezpieczeń Azure.</span><span class="sxs-lookup"><span data-stu-id="9f759-197">Advance to the next tutorial to learn about Azure security center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9f759-198">Zarządzanie zabezpieczeniami maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="9f759-198">Manage VM security</span></span>](./tutorial-azure-security.md)