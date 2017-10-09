---
title: aaaMonitor maszyn wirtualnych systemu Linux na platformie Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toomonitor rozruchu diagnostyki i metryki wydajności na maszynie wirtualnej systemu Linux na platformie Azure"
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
ms.openlocfilehash: 282da0f03ab0bf37bd44750c22813ca8d1c89560
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomonitor-a-linux-virtual-machine-in-azure"></a><span data-ttu-id="ab0a0-103">Jak toomonitor maszyny wirtualnej systemu Linux na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="ab0a0-103">How toomonitor a Linux virtual machine in Azure</span></span>

<span data-ttu-id="ab0a0-104">tooensure maszyn wirtualnych (VM) na platformie Azure działają poprawnie, można przejrzeć diagnostyki rozruchu i metryki wydajności.</span><span class="sxs-lookup"><span data-stu-id="ab0a0-104">tooensure your virtual machines (VMs) in Azure are running correctly, you can review boot diagnostics and performance metrics.</span></span> <span data-ttu-id="ab0a0-105">Ten samouczek zawiera informacje na temat wykonywania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="ab0a0-105">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ab0a0-106">Włącz diagnostykę rozruchu na powitania maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="ab0a0-106">Enable boot diagnostics on hello VM</span></span>
> * <span data-ttu-id="ab0a0-107">Wyświetlanie diagnostyki rozruchu</span><span class="sxs-lookup"><span data-stu-id="ab0a0-107">View boot diagnostics</span></span>
> * <span data-ttu-id="ab0a0-108">Wyświetlaj metryki hosta</span><span class="sxs-lookup"><span data-stu-id="ab0a0-108">View host metrics</span></span>
> * <span data-ttu-id="ab0a0-109">Włącz rozszerzenia diagnostyki na powitania maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="ab0a0-109">Enable diagnostics extension on hello VM</span></span>
> * <span data-ttu-id="ab0a0-110">Wyświetlaj metryki maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="ab0a0-110">View VM metrics</span></span>
> * <span data-ttu-id="ab0a0-111">Tworzenie alertów w oparciu metryki diagnostycznych</span><span class="sxs-lookup"><span data-stu-id="ab0a0-111">Create alerts based on diagnostic metrics</span></span>
> * <span data-ttu-id="ab0a0-112">Skonfiguruj zaawansowane monitorowanie</span><span class="sxs-lookup"><span data-stu-id="ab0a0-112">Set up advanced monitoring</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="ab0a0-113">Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym samouczku wymaga działają hello Azure CLI w wersji 2.0.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="ab0a0-113">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="ab0a0-114">Uruchom `az --version` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="ab0a0-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="ab0a0-115">Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="ab0a0-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-vm"></a><span data-ttu-id="ab0a0-116">Tworzenie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="ab0a0-116">Create VM</span></span>

<span data-ttu-id="ab0a0-117">Diagnostyka toosee i metryki w akcji, należy maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ab0a0-117">toosee diagnostics and metrics in action, you need a VM.</span></span> <span data-ttu-id="ab0a0-118">Najpierw utwórz nową grupę zasobów o [Tworzenie grupy az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="ab0a0-118">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="ab0a0-119">Witaj poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroupMonitor* w hello *eastus* lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="ab0a0-119">hello following example creates a resource group named *myResourceGroupMonitor* in hello *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroupMonitor --location eastus
```

<span data-ttu-id="ab0a0-120">Teraz Utwórz maszynę Wirtualną z [tworzenia maszyny wirtualnej az](https://docs.microsoft.com/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="ab0a0-120">Now create a VM with [az vm create](https://docs.microsoft.com/cli/azure/vm#create).</span></span> <span data-ttu-id="ab0a0-121">Witaj poniższy przykład tworzy Maszynę wirtualną o nazwie *myVM*:</span><span class="sxs-lookup"><span data-stu-id="ab0a0-121">hello following example creates a VM named *myVM*:</span></span>

```azurecli-interactive 
az vm create \
  --resource-group myResourceGroupMonitor \
  --name myVM \
  --image UbuntuLTS \
  --admin-username azureuser \
  --generate-ssh-keys
```

## <a name="enable-boot-diagnostics"></a><span data-ttu-id="ab0a0-122">Włącz diagnostykę rozruchu</span><span class="sxs-lookup"><span data-stu-id="ab0a0-122">Enable boot diagnostics</span></span>

<span data-ttu-id="ab0a0-123">Jak rozruchu maszyn wirtualnych systemu Linux, rozszerzenia diagnostyki rozruchu hello przechwytuje dane wyjściowe rozruchu i zapisuje go w magazynie Azure.</span><span class="sxs-lookup"><span data-stu-id="ab0a0-123">As Linux VMs boot, hello boot diagnostic extension captures boot output and stores it in Azure storage.</span></span> <span data-ttu-id="ab0a0-124">Może to być problemy rozruchu maszyny Wirtualnej tootroubleshoot używane.</span><span class="sxs-lookup"><span data-stu-id="ab0a0-124">This data can be used tootroubleshoot VM boot issues.</span></span> <span data-ttu-id="ab0a0-125">Diagnostyki rozruchu nie są automatycznie włączone, podczas tworzenia maszyny Wirtualnej systemu Linux przy użyciu hello wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ab0a0-125">Boot diagnostics are not automatically enabled when you create a Linux VM using hello Azure CLI.</span></span>

<span data-ttu-id="ab0a0-126">Przed włączeniem diagnostyki rozruchu, konto magazynu na potrzeby toobe utworzony do przechowywania dzienników rozruchu.</span><span class="sxs-lookup"><span data-stu-id="ab0a0-126">Before enabling boot diagnostics, a storage account needs toobe created for storing boot logs.</span></span> <span data-ttu-id="ab0a0-127">Konta magazynu musi mieć globalnie unikatowej nazwy należeć do zakresu od 3 do 24 znaków i musi zawierać tylko cyfry i małe litery.</span><span class="sxs-lookup"><span data-stu-id="ab0a0-127">Storage accounts must have a globally unique name, be between 3 and 24 characters, and must contain only numbers and lowercase letters.</span></span> <span data-ttu-id="ab0a0-128">Utwórz konto magazynu z hello [Tworzenie konta magazynu az](/cli/azure/storage/account#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="ab0a0-128">Create a storage account with hello [az storage account create](/cli/azure/storage/account#create) command.</span></span> <span data-ttu-id="ab0a0-129">W tym przykładzie losowy ciąg jest używany toocreate nazwy konta magazynu unikatowy.</span><span class="sxs-lookup"><span data-stu-id="ab0a0-129">In this example, a random string is used toocreate a unique storage account name.</span></span> 

```azurecli-interactive 
storageacct=mydiagdata$RANDOM

az storage account create \
  --resource-group myResourceGroupMonitor \
  --name $storageacct \
  --sku Standard_LRS \
  --location eastus
```

<span data-ttu-id="ab0a0-130">Podczas włączania diagnostyki rozruchu, wymagany jest kontener magazynu obiektów blob toohello URI hello.</span><span class="sxs-lookup"><span data-stu-id="ab0a0-130">When enabling boot diagnostics, hello URI toohello blob storage container is needed.</span></span> <span data-ttu-id="ab0a0-131">Witaj następujące kwerendy polecenia hello tooreturn konta magazynu tego identyfikatora URI.</span><span class="sxs-lookup"><span data-stu-id="ab0a0-131">hello following command queries hello storage account tooreturn this URI.</span></span> <span data-ttu-id="ab0a0-132">Witaj wartość identyfikatora URI jest przechowywany w nazwach zmiennych *bloburi*, która jest używana w hello następnego kroku.</span><span class="sxs-lookup"><span data-stu-id="ab0a0-132">hello URI value is stored in a variable names *bloburi*, which is used in hello next step.</span></span>

```azurecli-interactive 
bloburi=$(az storage account show --resource-group myResourceGroupMonitor --name $storageacct --query 'primaryEndpoints.blob' -o tsv)
```

<span data-ttu-id="ab0a0-133">Teraz Włącz diagnostyki rozruchu z [włączyć diagnostyki rozruchu az wirtualna](https://docs.microsoft.com/cli/azure/vm/boot-diagnostics#enable).</span><span class="sxs-lookup"><span data-stu-id="ab0a0-133">Now enable boot diagnostics with [az vm boot-diagnostics enable](https://docs.microsoft.com/cli/azure/vm/boot-diagnostics#enable).</span></span> <span data-ttu-id="ab0a0-134">Witaj `--storage` wartość jest hello obiektu blob identyfikatora URI zebrane w poprzednim kroku hello.</span><span class="sxs-lookup"><span data-stu-id="ab0a0-134">hello `--storage` value is hello blob URI collected in hello previous step.</span></span>

```azurecli-interactive 
az vm boot-diagnostics enable \
  --resource-group myResourceGroupMonitor \
  --name myVM \
  --storage $bloburi
```


## <a name="view-boot-diagnostics"></a><span data-ttu-id="ab0a0-135">Wyświetlanie diagnostyki rozruchu</span><span class="sxs-lookup"><span data-stu-id="ab0a0-135">View boot diagnostics</span></span>

<span data-ttu-id="ab0a0-136">Po włączeniu diagnostyki rozruchu zawsze zatrzymywania i uruchamiania hello maszyny Wirtualnej, informacje na temat procesu rozruchu hello są zapisywane tooa pliku dziennika.</span><span class="sxs-lookup"><span data-stu-id="ab0a0-136">When boot diagnostics are enabled, each time you stop and start hello VM, information about hello boot process is written tooa log file.</span></span> <span data-ttu-id="ab0a0-137">W tym przykładzie najpierw cofnąć hello maszyny Wirtualnej z hello [deallocate wirtualna az](/cli/azure/vm#deallocate) polecenia w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="ab0a0-137">For this example, first deallocate hello VM with hello [az vm deallocate](/cli/azure/vm#deallocate) command as follows:</span></span>

```azurecli-interactive 
az vm deallocate --resource-group myResourceGroupMonitor --name myVM
```

<span data-ttu-id="ab0a0-138">Teraz uruchomić hello maszyny Wirtualnej z hello [uruchomienia maszyny wirtualnej az]( /cli/azure/vm#stop) polecenia w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="ab0a0-138">Now start hello VM with hello [az vm start]( /cli/azure/vm#stop) command as follows:</span></span>

```azurecli-interactive 
az vm start --resource-group myResourceGroupMonitor --name myVM
```

<span data-ttu-id="ab0a0-139">Można uzyskać hello danych diagnostyki rozruchu dla *myVM* z hello [az maszyny wirtualnej diagnostyki rozruchu get rozruchu — dziennik](https://docs.microsoft.com/cli/azure/vm/boot-diagnostics#get-boot-log) polecenia w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="ab0a0-139">You can get hello boot diagnostic data for *myVM* with hello [az vm boot-diagnostics get-boot-log](https://docs.microsoft.com/cli/azure/vm/boot-diagnostics#get-boot-log) command as follows:</span></span>

```azurecli-interactive 
az vm boot-diagnostics get-boot-log --resource-group myResourceGroupMonitor --name myVM
```


## <a name="view-host-metrics"></a><span data-ttu-id="ab0a0-140">Wyświetlaj metryki hosta</span><span class="sxs-lookup"><span data-stu-id="ab0a0-140">View host metrics</span></span>

<span data-ttu-id="ab0a0-141">Maszynę wirtualną systemu Linux zawiera dedykowany hosta na platformie Azure, która współdziała ona z.</span><span class="sxs-lookup"><span data-stu-id="ab0a0-141">A Linux VM has a dedicated host in Azure that it interacts with.</span></span> <span data-ttu-id="ab0a0-142">Metryki są automatycznie pobierane hello hosta i mogą być wyświetlane w portalu Azure hello w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="ab0a0-142">Metrics are automatically collected for hello host and can be viewed in hello Azure portal as follows:</span></span>

1. <span data-ttu-id="ab0a0-143">W hello portalu Azure, kliknij przycisk **grup zasobów**, wybierz pozycję **myResourceGroupMonitor**, a następnie wybierz **myVM** hello listy zasobów.</span><span class="sxs-lookup"><span data-stu-id="ab0a0-143">In hello Azure portal, click **Resource Groups**, select **myResourceGroupMonitor**, and then select **myVM** in hello resource list.</span></span>
1. <span data-ttu-id="ab0a0-144">toosee wykonuje hello hosta maszyny Wirtualnej, kliknij **metryki** na powitania bloku maszyny Wirtualnej, następnie wybierz jedno z hello *[Host]* metryki w obszarze **dostępne metryki**.</span><span class="sxs-lookup"><span data-stu-id="ab0a0-144">toosee how hello host VM is performing, click **Metrics** on hello VM blade, then select any of hello *[Host]* metrics under **Available metrics**.</span></span>

    ![Wyświetlaj metryki hosta](./media/tutorial-monitoring/monitor-host-metrics.png)


## <a name="install-diagnostics-extension"></a><span data-ttu-id="ab0a0-146">Zainstaluj rozszerzenie diagnostyki</span><span class="sxs-lookup"><span data-stu-id="ab0a0-146">Install diagnostics extension</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ab0a0-147">Ten dokument zawiera opis wersji 2.3 hello diagnostycznych rozszerzenia systemu Linux, która została wycofana.</span><span class="sxs-lookup"><span data-stu-id="ab0a0-147">This document describes version 2.3 of hello Linux Diagnostic Extension, which has been deprecated.</span></span> <span data-ttu-id="ab0a0-148">Wersja 2.3 będzie obsługiwana do 30 czerwca 2018.</span><span class="sxs-lookup"><span data-stu-id="ab0a0-148">Version 2.3 will be supported until June 30, 2018.</span></span>
>
> <span data-ttu-id="ab0a0-149">Zamiast tego można włączyć w wersji 3.0 hello rozszerzenia diagnostyczne systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="ab0a0-149">Version 3.0 of hello Linux Diagnostic Extension can be enabled instead.</span></span> <span data-ttu-id="ab0a0-150">Aby uzyskać więcej informacji, zobacz [hello dokumentacji](./diagnostic-extension.md).</span><span class="sxs-lookup"><span data-stu-id="ab0a0-150">For more information, see [hello documentation](./diagnostic-extension.md).</span></span>

<span data-ttu-id="ab0a0-151">Witaj hosta podstawowe metryki są dostępne, ale toosee bardziej szczegółowe i metryki specyficzne dla maszyny Wirtualnej, możesz tooneed tooinstall hello Azure diagnostics rozszerzenia na powitania maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ab0a0-151">hello basic host metrics are available, but toosee more granular and VM-specific metrics, you tooneed tooinstall hello Azure diagnostics extension on hello VM.</span></span> <span data-ttu-id="ab0a0-152">Witaj rozszerzenia diagnostyki Azure umożliwia dodatkowe funkcje monitorowania i diagnostyki toobe dane pobrane z hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ab0a0-152">hello Azure diagnostics extension allows additional monitoring and diagnostics data toobe retrieved from hello VM.</span></span> <span data-ttu-id="ab0a0-153">Możesz wyświetlić te metryki wydajności i tworzyć alerty oparte na sposób wykonywania hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ab0a0-153">You can view these performance metrics and create alerts based on how hello VM performs.</span></span> <span data-ttu-id="ab0a0-154">rozszerzenie diagnostycznych Hello jest instalowany za pośrednictwem portalu Azure hello:</span><span class="sxs-lookup"><span data-stu-id="ab0a0-154">hello diagnostic extension is installed through hello Azure portal as follows:</span></span>

1. <span data-ttu-id="ab0a0-155">W hello portalu Azure, kliknij przycisk **grup zasobów**, wybierz pozycję **myResourceGroup**, a następnie wybierz **myVM** hello listy zasobów.</span><span class="sxs-lookup"><span data-stu-id="ab0a0-155">In hello Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in hello resource list.</span></span>
1. <span data-ttu-id="ab0a0-156">Kliknij przycisk **ustawienia diagnostyki**.</span><span class="sxs-lookup"><span data-stu-id="ab0a0-156">Click **Diagnosis settings**.</span></span> <span data-ttu-id="ab0a0-157">Lista Hello wskazuje, że *diagnostyki rozruchu* są już włączone w poprzedniej sekcji hello.</span><span class="sxs-lookup"><span data-stu-id="ab0a0-157">hello list shows that *Boot diagnostics* are already enabled from hello previous section.</span></span> <span data-ttu-id="ab0a0-158">Kliknij pole wyboru hello *podstawowe metryki*.</span><span class="sxs-lookup"><span data-stu-id="ab0a0-158">Click hello check box for *Basic metrics*.</span></span>
1. <span data-ttu-id="ab0a0-159">W hello *konta magazynu* Przejdź hello wybierz tooand *mydiagdata [1234]* konto utworzone w poprzedniej sekcji hello.</span><span class="sxs-lookup"><span data-stu-id="ab0a0-159">In hello *Storage account* section, browse tooand select hello *mydiagdata[1234]* account created in hello previous section.</span></span>
1. <span data-ttu-id="ab0a0-160">Kliknij przycisk hello **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="ab0a0-160">Click hello **Save** button.</span></span>

    ![Wyświetlaj metryki diagnostycznych](./media/tutorial-monitoring/enable-diagnostics-extension.png)


## <a name="view-vm-metrics"></a><span data-ttu-id="ab0a0-162">Wyświetlaj metryki maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="ab0a0-162">View VM metrics</span></span>

<span data-ttu-id="ab0a0-163">Witaj metryki maszyny Wirtualnej można wyświetlić w hello taki sam sposób, aby wyświetlić metryki maszyny Wirtualnej hosta hello:</span><span class="sxs-lookup"><span data-stu-id="ab0a0-163">You can view hello VM metrics in hello same way that you viewed hello host VM metrics:</span></span>

1. <span data-ttu-id="ab0a0-164">W hello portalu Azure, kliknij przycisk **grup zasobów**, wybierz pozycję **myResourceGroup**, a następnie wybierz **myVM** hello listy zasobów.</span><span class="sxs-lookup"><span data-stu-id="ab0a0-164">In hello Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in hello resource list.</span></span>
1. <span data-ttu-id="ab0a0-165">toosee wykonuje hello maszyny Wirtualnej, kliknij **metryki** na hello bloku maszyny Wirtualnej, a następnie wybierz dowolną hello diagnostyki metryki w obszarze **dostępne metryki**.</span><span class="sxs-lookup"><span data-stu-id="ab0a0-165">toosee how hello VM is performing, click **Metrics** on hello VM blade, and then select any of hello diagnostics metrics under **Available metrics**.</span></span>

    ![Wyświetlaj metryki maszyny Wirtualnej](./media/tutorial-monitoring/monitor-vm-metrics.png)


## <a name="create-alerts"></a><span data-ttu-id="ab0a0-167">Tworzenie alertów</span><span class="sxs-lookup"><span data-stu-id="ab0a0-167">Create alerts</span></span>

<span data-ttu-id="ab0a0-168">Można tworzyć alertów w oparciu metryki dotyczące wydajności.</span><span class="sxs-lookup"><span data-stu-id="ab0a0-168">You can create alerts based on specific performance metrics.</span></span> <span data-ttu-id="ab0a0-169">Alerty można używane toonotify, który podczas średniego użycia procesora CPU przekracza określonego progu lub wolnego miejsca na dysku spada poniżej pewnego, np.</span><span class="sxs-lookup"><span data-stu-id="ab0a0-169">Alerts can be used toonotify you when average CPU usage exceeds a certain threshold or available free disk space drops below a certain amount, for example.</span></span> <span data-ttu-id="ab0a0-170">Alerty są wyświetlane w portalu Azure hello lub mogą być wysyłane za pośrednictwem poczty e-mail.</span><span class="sxs-lookup"><span data-stu-id="ab0a0-170">Alerts are displayed in hello Azure portal or can be sent via email.</span></span> <span data-ttu-id="ab0a0-171">W odpowiedzi tooalerts generowaną może także wyzwolić elementu runbook usługi Automatyzacja Azure lub usługi Azure Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="ab0a0-171">You can also trigger Azure Automation runbooks or Azure Logic Apps in response tooalerts being generated.</span></span>

<span data-ttu-id="ab0a0-172">Witaj poniższy przykład tworzy alert dla średniego użycia procesora CPU.</span><span class="sxs-lookup"><span data-stu-id="ab0a0-172">hello following example creates an alert for average CPU usage.</span></span>

1. <span data-ttu-id="ab0a0-173">W hello portalu Azure, kliknij przycisk **grup zasobów**, wybierz pozycję **myResourceGroup**, a następnie wybierz **myVM** hello listy zasobów.</span><span class="sxs-lookup"><span data-stu-id="ab0a0-173">In hello Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in hello resource list.</span></span>
2. <span data-ttu-id="ab0a0-174">Kliknij przycisk **reguły alertów** na powitania bloku maszyny Wirtualnej, następnie kliknij przycisk **Dodaj alert metryki** hello górze hello blok alerty.</span><span class="sxs-lookup"><span data-stu-id="ab0a0-174">Click **Alert rules** on hello VM blade, then click **Add metric alert** across hello top of hello alerts blade.</span></span>
4. <span data-ttu-id="ab0a0-175">Podaj **nazwa** alertu, takie jak *myAlertRule*</span><span class="sxs-lookup"><span data-stu-id="ab0a0-175">Provide a **Name** for your alert, such as *myAlertRule*</span></span>
5. <span data-ttu-id="ab0a0-176">tootrigger alert, gdy procent użycia procesora CPU przekracza 1.0 przez pięć minut, pozostaw hello wszystkich innych wartości domyślnych wybrane.</span><span class="sxs-lookup"><span data-stu-id="ab0a0-176">tootrigger an alert when CPU percentage exceeds 1.0 for five minutes, leave all hello other defaults selected.</span></span>
6. <span data-ttu-id="ab0a0-177">Opcjonalnie, zaznacz pole hello *E-mail właściciele, współautorzy i czytelnicy* toosend powiadomienia e-mail.</span><span class="sxs-lookup"><span data-stu-id="ab0a0-177">Optionally, check hello box for *Email owners, contributors, and readers* toosend email notification.</span></span> <span data-ttu-id="ab0a0-178">Akcja domyślna Hello jest toopresent powiadomienia w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="ab0a0-178">hello default action is toopresent a notification in hello portal.</span></span>
7. <span data-ttu-id="ab0a0-179">Kliknij przycisk hello **OK** przycisku.</span><span class="sxs-lookup"><span data-stu-id="ab0a0-179">Click hello **OK** button.</span></span>


## <a name="advanced-monitoring"></a><span data-ttu-id="ab0a0-180">Zaawansowane monitorowanie</span><span class="sxs-lookup"><span data-stu-id="ab0a0-180">Advanced monitoring</span></span> 

<span data-ttu-id="ab0a0-181">Możliwość bardziej zaawansowane monitorowanie maszyny wirtualnej za pomocą [Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview).</span><span class="sxs-lookup"><span data-stu-id="ab0a0-181">You can do more advanced monitoring of your VM by using [Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview).</span></span> <span data-ttu-id="ab0a0-182">Jeśli nie zostało to jeszcze zrobione, należy zarejestrować się w celu [bezpłatnej wersji próbnej](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial) programu Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="ab0a0-182">If you haven't already done so, you can sign up for a [free trial](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial) of Operations Management Suite.</span></span>

<span data-ttu-id="ab0a0-183">Jeśli masz portalu OMS toohello dostępu można znaleźć identyfikator obszaru roboczego hello klucza i obszar roboczy w bloku ustawień hello.</span><span class="sxs-lookup"><span data-stu-id="ab0a0-183">When you have access toohello OMS portal, you can find hello workspace key and workspace identifier on hello Settings blade.</span></span> <span data-ttu-id="ab0a0-184">Zastąp < klucz obszaru roboczego > i < identyfikator obszaru roboczego > z wartościami hello z Twojej OMS można użyć obszaru roboczego, a następnie możesz **zestaw rozszerzenia maszyny wirtualnej az** tooadd hello OMS rozszerzenia toohello maszyny Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="ab0a0-184">Replace <workspace-key> and <workspace-id> with hello values for from your OMS workspace and then you can use **az vm extension set** tooadd hello OMS extension toohello VM:</span></span>

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

<span data-ttu-id="ab0a0-185">W bloku dziennika wyszukiwania hello portalu OMS hello, powinien zostać wyświetlony *myVM* takich jak co przedstawiono na poniższej ilustracji hello:</span><span class="sxs-lookup"><span data-stu-id="ab0a0-185">On hello Log Search blade of hello OMS portal, you should see *myVM* such as what is shown in hello following picture:</span></span>

![Blok OMS](./media/tutorial-monitoring/tutorial-monitor-oms.png)

## <a name="next-steps"></a><span data-ttu-id="ab0a0-187">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ab0a0-187">Next steps</span></span>

<span data-ttu-id="ab0a0-188">W tym samouczku został skonfigurowany i przejrzeć maszyn wirtualnych w Centrum zabezpieczeń Azure.</span><span class="sxs-lookup"><span data-stu-id="ab0a0-188">In this tutorial, you configured and reviewed VMs with Azure Security Center.</span></span> <span data-ttu-id="ab0a0-189">W tym samouczku omówiono:</span><span class="sxs-lookup"><span data-stu-id="ab0a0-189">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ab0a0-190">Włącz diagnostykę rozruchu na powitania maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="ab0a0-190">Enable boot diagnostics on hello VM</span></span>
> * <span data-ttu-id="ab0a0-191">Wyświetlanie diagnostyki rozruchu</span><span class="sxs-lookup"><span data-stu-id="ab0a0-191">View boot diagnostics</span></span>
> * <span data-ttu-id="ab0a0-192">Wyświetlaj metryki hosta</span><span class="sxs-lookup"><span data-stu-id="ab0a0-192">View host metrics</span></span>
> * <span data-ttu-id="ab0a0-193">Włącz rozszerzenia diagnostyki na powitania maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="ab0a0-193">Enable diagnostics extension on hello VM</span></span>
> * <span data-ttu-id="ab0a0-194">Wyświetlaj metryki maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="ab0a0-194">View VM metrics</span></span>
> * <span data-ttu-id="ab0a0-195">Tworzenie alertów w oparciu metryki diagnostycznych</span><span class="sxs-lookup"><span data-stu-id="ab0a0-195">Create alerts based on diagnostic metrics</span></span>
> * <span data-ttu-id="ab0a0-196">Skonfiguruj zaawansowane monitorowanie</span><span class="sxs-lookup"><span data-stu-id="ab0a0-196">Set up advanced monitoring</span></span>

<span data-ttu-id="ab0a0-197">Przejdź dalej toolearn samouczka toohello temat Centrum zabezpieczeń Azure.</span><span class="sxs-lookup"><span data-stu-id="ab0a0-197">Advance toohello next tutorial toolearn about Azure security center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ab0a0-198">Zarządzanie zabezpieczeniami maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="ab0a0-198">Manage VM security</span></span>](./tutorial-azure-security.md)