---
title: aaaConvert Azure tooa zestawu skalowania maszyny wirtualnej | Dokumentacja firmy Microsoft
description: "Tworzenie i wdrażanie skali maszyny wirtualnej systemu Linux Azure ustawiony za pomocą hello Azure CLI."
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 04/05/2017
ms.author: adegeo
ms.openlocfilehash: e228282ac4855cef589b8500e74e9d461f9aed84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="convert-an-existing-azure-virtual-machine-tooa-scale-set"></a><span data-ttu-id="cf1fd-103">Konwertuj istniejącego zestawu skalowania maszyny wirtualnej platformy Azure tooa</span><span class="sxs-lookup"><span data-stu-id="cf1fd-103">Convert an existing Azure virtual machine tooa scale set</span></span>

<span data-ttu-id="cf1fd-104">Ten samouczek pokazuje, jak tooconvert toouse Azure CLI 2.0 tooa maszyny wirtualnej zestawu skalowania maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="cf1fd-104">This tutorial shows you how toouse Azure CLI 2.0 tooconvert a virtual machine tooa virtual machine scale set.</span></span> <span data-ttu-id="cf1fd-105">Możesz też dowiedzieć się, jak tooautomate hello hello maszyn wirtualnych w skali hello konfiguracja.</span><span class="sxs-lookup"><span data-stu-id="cf1fd-105">You also learn how tooautomate hello configuration of hello virtual machines in hello scale set.</span></span> <span data-ttu-id="cf1fd-106">Aby uzyskać więcej informacji na temat tooinstall Azure CLI 2.0, zobacz temat [wprowadzenie Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="cf1fd-106">For more information on how tooinstall Azure CLI 2.0, see [Getting Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md).</span></span> <span data-ttu-id="cf1fd-107">Aby uzyskać więcej informacji na temat zestawów skalowania, zobacz [zestawach skali maszyny wirtualnej](../../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="cf1fd-107">For more information about scale sets, see [Virtual Machine Scale Sets](../../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md).</span></span>

## <a name="step-1---deprovision-hello-vm"></a><span data-ttu-id="cf1fd-108">Krok 1 - Deprovision hello maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="cf1fd-108">Step 1 - Deprovision hello VM</span></span>

<span data-ttu-id="cf1fd-109">Użyj toohello tooconnect SSH maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="cf1fd-109">Use SSH tooconnect toohello VM.</span></span>

<span data-ttu-id="cf1fd-110">Witaj deprovision maszyny Wirtualnej przy użyciu hello Azure VM agent toodelete plików i danych.</span><span class="sxs-lookup"><span data-stu-id="cf1fd-110">Deprovision hello VM using hello Azure VM agent toodelete files and data.</span></span> <span data-ttu-id="cf1fd-111">Szczegółowe omówienie anulowania obsługi, zobacz [Przechwytywanie maszyny wirtualnej systemu Linux](capture-image.md).</span><span class="sxs-lookup"><span data-stu-id="cf1fd-111">For a detailed overview of deprovisioning, see [Capture a Linux virtual machine](capture-image.md).</span></span>

```bash
sudo waagent -deprovision+user -force
exit
```

## <a name="step-2---capture-an-image-of-hello-vm"></a><span data-ttu-id="cf1fd-112">Krok 2 — Przechwyć obraz powitania maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="cf1fd-112">Step 2 - Capture an image of hello VM</span></span>

<span data-ttu-id="cf1fd-113">Aby uzyskać szczegółowe omówienie rejestrowania, zobacz [Przechwytywanie maszyny wirtualnej systemu Linux](capture-image.md).</span><span class="sxs-lookup"><span data-stu-id="cf1fd-113">For a detailed overview of capturing, see [Capture a Linux virtual machine](capture-image.md).</span></span>

<span data-ttu-id="cf1fd-114">Cofnięcie przydziału hello maszyny Wirtualnej z [deallocate wirtualna az](/cli/azure/vm#deallocate):</span><span class="sxs-lookup"><span data-stu-id="cf1fd-114">Deallocate hello VM with [az vm deallocate](/cli/azure/vm#deallocate):</span></span>

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="cf1fd-115">Generalize hello maszyny Wirtualnej z [generalize wirtualna az](/cli/azure/vm#generalize):</span><span class="sxs-lookup"><span data-stu-id="cf1fd-115">Generalize hello VM with [az vm generalize](/cli/azure/vm#generalize):</span></span>

```azurecli
az vm generalize --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="cf1fd-116">Tworzenie obrazu na podstawie hello zasobu maszyny Wirtualnej z [tworzenia obrazu az](/cli/azure/image#create):</span><span class="sxs-lookup"><span data-stu-id="cf1fd-116">Create an image from hello VM resource with [az image create](/cli/azure/image#create):</span></span>

```azurecli
az image create --resource-group myResourceGroup --name myImage --source myVM
```

## <a name="step-3---create-hello-scale-set"></a><span data-ttu-id="cf1fd-117">Krok 3 — Tworzenie hello zestaw skali</span><span class="sxs-lookup"><span data-stu-id="cf1fd-117">Step 3 - Create hello scale set</span></span>

<span data-ttu-id="cf1fd-118">Pobierz hello **identyfikator** hello obrazu.</span><span class="sxs-lookup"><span data-stu-id="cf1fd-118">Get hello **id** of hello image.</span></span>

```azurecli
az image show --resource-group myResourceGroup --name myImage --query id
```

```json
"/subscriptions/afbdaf8b-9188-4651-bce1-9115dd57c98b/resourceGroups/vmtest/providers/Microsoft.Compute/images/myImage"
```

<span data-ttu-id="cf1fd-119">Utwórz maszynę Wirtualną z zasobu obrazu z [az vmss utworzyć](/cli/azure/vmss#create):</span><span class="sxs-lookup"><span data-stu-id="cf1fd-119">Create a VM from your image resource with [az vmss create](/cli/azure/vmss#create):</span></span>

```azurecli
az vmss create --resource-group myResourceGroup --name myScaleSet --image /subscriptions/afbdaf8b-9188-4651-bce1-9115dd57c98b/resourceGroups/vmtest/providers/Microsoft.Compute/images/myImage --upgrade-policy-mode automatic --vm-sku Standard_DS1_v2 --data-disk-sizes-gb 10 --admin-username azureuser --generate-ssh-keys
```

<span data-ttu-id="cf1fd-120">To polecenie również dołączyć dysku danych 10gb.</span><span class="sxs-lookup"><span data-stu-id="cf1fd-120">This command also attached a 10gb data disk.</span></span> <span data-ttu-id="cf1fd-121">Należy pamiętać, że w zależności od hello maszyny Wirtualnej wybrany rozmiar (użyliśmy **Standard_DS1_v2**), hello liczba dysków z danymi dozwolone jest różna.</span><span class="sxs-lookup"><span data-stu-id="cf1fd-121">Keep in mind that depending on hello VM size chosen (we used **Standard_DS1_v2**), hello number of data disks allowed is different.</span></span> <span data-ttu-id="cf1fd-122">Aby uzyskać więcej informacji, przejrzyj hello [rozmiarów maszyn wirtualnych](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="cf1fd-122">For more information, review hello [virtual machine sizes](sizes.md).</span></span>

<span data-ttu-id="cf1fd-123">Po zakończeniu zestawu skalowania hello, należy połączyć tooit.</span><span class="sxs-lookup"><span data-stu-id="cf1fd-123">Once hello scale set finishes, connect tooit.</span></span> <span data-ttu-id="cf1fd-124">Pobierz listę adresów IP dla wystąpień hello SSH z [az vmss listy--połączenia — informacje o wystąpieniu](/cli/azure/vmss#list-instance-connection-info):</span><span class="sxs-lookup"><span data-stu-id="cf1fd-124">Get a list of IP addresses for hello instances for SSH with [az vmss list-instance-connection-info](/cli/azure/vmss#list-instance-connection-info):</span></span>

```azurecli
az vmss list-instance-connection-info --resource-group myResourceGroup --name myScaleSet
```

```json
[
  "52.183.00.000:50000",
  "52.183.00.000:50003"
]
```

<span data-ttu-id="cf1fd-125">Teraz można podłączyć dysku danych hello wystąpienia tooinitialize toohello maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="cf1fd-125">Now you can connect toohello virtual machine instance tooinitialize hello data disk</span></span>

```bash
ssh -i ~/.ssh/id_rsa.pub -p 50000 azureuser@52.183.00.000
```

## <a name="step-4---initialize-hello-data-disk"></a><span data-ttu-id="cf1fd-126">Krok 4 — dysk danych hello inicjowania</span><span class="sxs-lookup"><span data-stu-id="cf1fd-126">Step 4 - Initialize hello data disk</span></span>

<span data-ttu-id="cf1fd-127">Podczas połączenia toohello maszyny wirtualnej, partycji dysku hello `fdisk`:</span><span class="sxs-lookup"><span data-stu-id="cf1fd-127">While connected toohello virtual machine, partition hello disk with `fdisk`:</span></span>

```bash
(echo n; echo p; echo 1; echo  ; echo  ; echo w) | sudo fdisk /dev/sdc
```

<span data-ttu-id="cf1fd-128">Zapis partycji toohello systemu plików z hello `mkfs` polecenia:</span><span class="sxs-lookup"><span data-stu-id="cf1fd-128">Write a file system toohello partition with hello `mkfs` command:</span></span>

```bash
sudo mkfs -t ext4 /dev/sdc1
```

<span data-ttu-id="cf1fd-129">Zainstaluj nowy dysk hello tak, aby była dostępna w systemie operacyjnym hello:</span><span class="sxs-lookup"><span data-stu-id="cf1fd-129">Mount hello new disk so that it is accessible in hello operating system:</span></span>

```bash
sudo mkdir /datadrive ; sudo mount /dev/sdc1 /datadrive
```

<span data-ttu-id="cf1fd-130">Witaj dysku może być teraz dostęp za pośrednictwem punktu instalacji datadrive hello, które można sprawdzić przy `ls /datadrive/`.</span><span class="sxs-lookup"><span data-stu-id="cf1fd-130">hello disk can now be accesses through hello datadrive mountpoint, which can be verified with `ls /datadrive/`.</span></span>

<span data-ttu-id="cf1fd-131">Zakończyć sesję SSH hello.</span><span class="sxs-lookup"><span data-stu-id="cf1fd-131">End hello SSH session.</span></span>


## <a name="step-5---configure-firewall"></a><span data-ttu-id="cf1fd-132">Krok 5 — Konfigurowanie zapory</span><span class="sxs-lookup"><span data-stu-id="cf1fd-132">Step 5 - Configure firewall</span></span>

<span data-ttu-id="cf1fd-133">Dziurkowanie przerw za pośrednictwem hello zapory toohello serwer sieci Web: obsługiwane przez zestaw skali hello.</span><span class="sxs-lookup"><span data-stu-id="cf1fd-133">Punch a hole through hello firewall toohello webserver hosted by hello scale set.</span></span> <span data-ttu-id="cf1fd-134">Podczas tworzenia zestawu skali hello, modułu równoważenia obciążenia została także utworzona i użyto go **SSH** toohello poszczególnych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="cf1fd-134">When hello scale set was created, a load balancer was also created, and you used it **SSH** toohello individual virtual machines.</span></span> <span data-ttu-id="cf1fd-135">tooopen portu, potrzebne informacje, którą można uzyskać przy użyciu wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="cf1fd-135">tooopen a port, you need two pieces of information, which you can get using Azure CLI.</span></span>

* <span data-ttu-id="cf1fd-136">**Pula adresów IP frontonu**</span><span class="sxs-lookup"><span data-stu-id="cf1fd-136">**Frontend IP address pool**</span></span>  
`az network lb show --resource-group myResourceGroup --name myScaleSetLB --output table --query frontendIpConfigurations[0].name`

* <span data-ttu-id="cf1fd-137">**Pula adresów IP zaplecza**</span><span class="sxs-lookup"><span data-stu-id="cf1fd-137">**Backend IP address pool**</span></span>  
`az network lb show --resource-group myResourceGroup --name myScaleSetLB --output table --query backendAddressPools[0].name`

<span data-ttu-id="cf1fd-138">Przy użyciu tych dwóch nazw, należy otworzyć port **80**.</span><span class="sxs-lookup"><span data-stu-id="cf1fd-138">With those two names, you can open port **80**.</span></span>

```azurecli
az network lb rule create --backend-pool-name myScaleSetLBBEPool --backend-port 80 --frontend-ip-name loadBalancerFrontEnd --frontend-port 80 --name webserver --protocol tcp --resource-group myResourceGroup --lb-name myScaleSetLB
```


## <a name="step-6---automate-configuration"></a><span data-ttu-id="cf1fd-139">Krok 6 — automatyzowania konfiguracji</span><span class="sxs-lookup"><span data-stu-id="cf1fd-139">Step 6 - Automate configuration</span></span>

<span data-ttu-id="cf1fd-140">Hello dysk danych wymaga toobe skonfigurowane na każde wystąpienie maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="cf1fd-140">hello data disk needs toobe configured on each virtual machine instance.</span></span> <span data-ttu-id="cf1fd-141">Firma Microsoft można zautomatyzować hello konfiguracji maszyny wirtualnej hello z hello **CustomScript** rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="cf1fd-141">We can automate hello configuration of hello virtual machine with hello **CustomScript** extension.</span></span>

<span data-ttu-id="cf1fd-142">Najpierw utwórz *SH* skryptu, który zawiera polecenia format dysku hello.</span><span class="sxs-lookup"><span data-stu-id="cf1fd-142">First, create a *.sh* script that includes hello disk format commands.</span></span>

```sh
#!/bin/bash

# Setup hello data disk
(echo n; echo p; echo 1; echo  ; echo  ; echo w) | fdisk /dev/sdc
fdisk /dev/sdc
mkfs -t ext4 /dev/sdc1
mkdir /datadrive
mount /dev/sdc1 /datadrive

exit 0
```

<span data-ttu-id="cf1fd-143">Następnie przekaż tego hello toowhere pliku skryptu **CustomScript** rozszerzenia do niego dostęp.</span><span class="sxs-lookup"><span data-stu-id="cf1fd-143">Next, upload that script file toowhere hello **CustomScript** extension can access it.</span></span> <span data-ttu-id="cf1fd-144">Jest dostępna kopia [tutaj](https://gist.githubusercontent.com/Thraka/ab1d8b78ac4b23722f3d3c1c03ac5df4).</span><span class="sxs-lookup"><span data-stu-id="cf1fd-144">A copy is available [here](https://gist.githubusercontent.com/Thraka/ab1d8b78ac4b23722f3d3c1c03ac5df4).</span></span>

<span data-ttu-id="cf1fd-145">Tworzenie pliku lokalnego o nazwie **settings.json** i put hello po bloku JSON w nim.</span><span class="sxs-lookup"><span data-stu-id="cf1fd-145">Create a local file named **settings.json** and put hello following JSON block in it.</span></span> <span data-ttu-id="cf1fd-146">Witaj `flieUris` można ustawić właściwości toowhere przekazany do pliku skryptu.</span><span class="sxs-lookup"><span data-stu-id="cf1fd-146">hello `flieUris` property should be set toowhere your script file was uploaded to.</span></span>

```json
{
  "fileUris": ["https://gist.githubusercontent.com/Thraka/ab1d8b78ac4b23722f3d3c1c03ac5df4/raw/3ac6e385010ac675e23ce583ce27b1a752f1b482/prep-vmss.sh"],
  "commandToExecute": "bash prep-vmss.sh" 
}
```

<span data-ttu-id="cf1fd-147">Wdrażanie tej skali tooyour polecenia ustawiony za pomocą hello **CustomScript** rozszerzenia odwołujące się do hello **settings.json** właśnie utworzony plik.</span><span class="sxs-lookup"><span data-stu-id="cf1fd-147">Deploy this command tooyour scale set with hello **CustomScript** extension, referencing hello **settings.json** file we just created.</span></span>

```azurecli
az vmss extension set --publisher Microsoft.Azure.Extensions --version 2.0 --name CustomScript --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

<span data-ttu-id="cf1fd-148">To rozszerzenie automatycznie wykorzystuje wszystkie bieżące wystąpienia i wystąpienia utworzone później przez skalowanie.</span><span class="sxs-lookup"><span data-stu-id="cf1fd-148">This extension automatically runs on all current instances, and any instances later created by scaling.</span></span>

## <a name="step-7---configure-autoscale-rules"></a><span data-ttu-id="cf1fd-149">Krok 7 — Konfigurowanie reguł automatycznego skalowania</span><span class="sxs-lookup"><span data-stu-id="cf1fd-149">Step 7 - Configure autoscale rules</span></span>

<span data-ttu-id="cf1fd-150">Obecnie reguł skalowania automatycznego nie można ustawić w wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="cf1fd-150">Currently, autoscale rules cannot be set in Azure CLI.</span></span> <span data-ttu-id="cf1fd-151">Użyj hello [portalu Azure](https://portal.azure.com) tooconfigure automatycznego skalowania.</span><span class="sxs-lookup"><span data-stu-id="cf1fd-151">Use hello [Azure portal](https://portal.azure.com) tooconfigure autoscale.</span></span>

## <a name="step-8---management-tasks"></a><span data-ttu-id="cf1fd-152">Krok 8 - zadania zarządzania</span><span class="sxs-lookup"><span data-stu-id="cf1fd-152">Step 8 - Management tasks</span></span>

<span data-ttu-id="cf1fd-153">W całym cyklu życia hello zestawu skali hello, może być konieczne toorun jednego lub więcej zadań zarządzania.</span><span class="sxs-lookup"><span data-stu-id="cf1fd-153">Throughout hello lifecycle of hello scale set, you may need toorun one or more management tasks.</span></span> <span data-ttu-id="cf1fd-154">Ponadto może ma skrypty toocreate, które automatyzują różnych zadań cyklu życia i hello interfejsu wiersza polecenia Azure udostępnia toodo szybko tych zadań.</span><span class="sxs-lookup"><span data-stu-id="cf1fd-154">Additionally, you may want toocreate scripts that automate various lifecycle-tasks, and hello Azure CLI provides a quick way toodo those tasks.</span></span> <span data-ttu-id="cf1fd-155">Poniżej przedstawiono kilka typowych zadań.</span><span class="sxs-lookup"><span data-stu-id="cf1fd-155">Here are a few common tasks.</span></span>

### <a name="get-connection-info"></a><span data-ttu-id="cf1fd-156">Pobierz informacje o połączeniu</span><span class="sxs-lookup"><span data-stu-id="cf1fd-156">Get connection info</span></span>

```azurecli
az vmss list-instance-connection-info --resource-group myResourceGroup --name myScaleSet
```

### <a name="set-instance-count-manual-scale"></a><span data-ttu-id="cf1fd-157">Ustaw liczbę wystąpień (Ręczne skala)</span><span class="sxs-lookup"><span data-stu-id="cf1fd-157">Set instance count (manual scale)</span></span>

```azurecli
az vmss scale --resource-group myResourceGroup --name myScaleSet --new-capacity 4
```

### <a name="delete-resource-group"></a><span data-ttu-id="cf1fd-158">Usuń grupę zasobów</span><span class="sxs-lookup"><span data-stu-id="cf1fd-158">Delete resource group</span></span>

<span data-ttu-id="cf1fd-159">Usunięcie grupy zasobów powoduje usunięcie wszystkie zasoby zawarte w ciągu.</span><span class="sxs-lookup"><span data-stu-id="cf1fd-159">Deleting a resource group also deletes all resources contained within.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="cf1fd-160">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="cf1fd-160">Next steps</span></span>
<span data-ttu-id="cf1fd-161">więcej informacji na temat niektórych hello skalowania maszyny wirtualnej ustawić funkcje wprowadzone w tym samouczku toolearn Zobacz hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="cf1fd-161">toolearn more about some of hello virtual machine scale set features introduced in this tutorial, see hello following information:</span></span>

- [<span data-ttu-id="cf1fd-162">Omówienie usługi Azure zestawy skalowania maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="cf1fd-162">Azure Virtual Machine Scale Sets overview</span></span>](../../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md)
- [<span data-ttu-id="cf1fd-163">Omówienie usługi Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="cf1fd-163">Azure Load Balancer overview</span></span>](../../load-balancer/load-balancer-overview.md)
- [<span data-ttu-id="cf1fd-164">Sterowaniu przepływem ruchu sieciowego z grup zabezpieczeń sieci</span><span class="sxs-lookup"><span data-stu-id="cf1fd-164">Control network traffic flow with network security groups</span></span>](../../virtual-network/virtual-networks-nsg.md)