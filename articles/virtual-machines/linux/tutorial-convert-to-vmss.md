---
title: Konwertuj zestaw skali maszyny Wirtualnej platformy Azure | Dokumentacja firmy Microsoft
description: "Tworzenie i wdrażanie skali maszyny wirtualnej systemu Linux Azure ustawiony za pomocą wiersza polecenia platformy Azure."
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
ms.openlocfilehash: 8d3376d2791b1349298db618d475ce5573083702
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="convert-an-existing-azure-virtual-machine-to-a-scale-set"></a><span data-ttu-id="25488-103">Konwertuj istniejącą maszynę wirtualną platformy Azure na zestaw skali</span><span class="sxs-lookup"><span data-stu-id="25488-103">Convert an existing Azure virtual machine to a scale set</span></span>

<span data-ttu-id="25488-104">W tym samouczku przedstawiono sposób używać Azure CLI 2.0 w celu konwertowania maszyny wirtualnej do zestawu skalowania maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="25488-104">This tutorial shows you how to use Azure CLI 2.0 to convert a virtual machine to a virtual machine scale set.</span></span> <span data-ttu-id="25488-105">Możesz również sposób automatyzowania konfiguracji maszyn wirtualnych w zestawie skalowania.</span><span class="sxs-lookup"><span data-stu-id="25488-105">You also learn how to automate the configuration of the virtual machines in the scale set.</span></span> <span data-ttu-id="25488-106">Aby uzyskać więcej informacji na temat sposobu instalowania 2.0 interfejsu wiersza polecenia Azure, zobacz [wprowadzenie Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="25488-106">For more information on how to install Azure CLI 2.0, see [Getting Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md).</span></span> <span data-ttu-id="25488-107">Aby uzyskać więcej informacji na temat zestawów skalowania, zobacz [zestawach skali maszyny wirtualnej](../../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="25488-107">For more information about scale sets, see [Virtual Machine Scale Sets](../../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md).</span></span>

## <a name="step-1---deprovision-the-vm"></a><span data-ttu-id="25488-108">Krok 1 — anulowanie zastrzeżenia maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="25488-108">Step 1 - Deprovision the VM</span></span>

<span data-ttu-id="25488-109">Używanie protokołu SSH, aby nawiązać połączenie z maszyną Wirtualną.</span><span class="sxs-lookup"><span data-stu-id="25488-109">Use SSH to connect to the VM.</span></span>

<span data-ttu-id="25488-110">Anulowanie zastrzeżenia maszyny Wirtualnej, aby usunąć pliki i dane przy użyciu agenta maszyny Wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="25488-110">Deprovision the VM using the Azure VM agent to delete files and data.</span></span> <span data-ttu-id="25488-111">Szczegółowe omówienie anulowania obsługi, zobacz [Przechwytywanie maszyny wirtualnej systemu Linux](capture-image.md).</span><span class="sxs-lookup"><span data-stu-id="25488-111">For a detailed overview of deprovisioning, see [Capture a Linux virtual machine](capture-image.md).</span></span>

```bash
sudo waagent -deprovision+user -force
exit
```

## <a name="step-2---capture-an-image-of-the-vm"></a><span data-ttu-id="25488-112">Krok 2 — przechwytywania obrazu maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="25488-112">Step 2 - Capture an image of the VM</span></span>

<span data-ttu-id="25488-113">Aby uzyskać szczegółowe omówienie rejestrowania, zobacz [Przechwytywanie maszyny wirtualnej systemu Linux](capture-image.md).</span><span class="sxs-lookup"><span data-stu-id="25488-113">For a detailed overview of capturing, see [Capture a Linux virtual machine](capture-image.md).</span></span>

<span data-ttu-id="25488-114">Cofnięcie przydziału maszyny Wirtualnej z [deallocate wirtualna az](/cli/azure/vm#deallocate):</span><span class="sxs-lookup"><span data-stu-id="25488-114">Deallocate the VM with [az vm deallocate](/cli/azure/vm#deallocate):</span></span>

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="25488-115">Generalize maszyny Wirtualnej z [generalize wirtualna az](/cli/azure/vm#generalize):</span><span class="sxs-lookup"><span data-stu-id="25488-115">Generalize the VM with [az vm generalize](/cli/azure/vm#generalize):</span></span>

```azurecli
az vm generalize --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="25488-116">Tworzenie obrazu na podstawie zasobu maszyny Wirtualnej z [tworzenia obrazu az](/cli/azure/image#create):</span><span class="sxs-lookup"><span data-stu-id="25488-116">Create an image from the VM resource with [az image create](/cli/azure/image#create):</span></span>

```azurecli
az image create --resource-group myResourceGroup --name myImage --source myVM
```

## <a name="step-3---create-the-scale-set"></a><span data-ttu-id="25488-117">Krok 3 — Utwórz zestaw skali</span><span class="sxs-lookup"><span data-stu-id="25488-117">Step 3 - Create the scale set</span></span>

<span data-ttu-id="25488-118">Pobierz **identyfikator** obrazu.</span><span class="sxs-lookup"><span data-stu-id="25488-118">Get the **id** of the image.</span></span>

```azurecli
az image show --resource-group myResourceGroup --name myImage --query id
```

```json
"/subscriptions/afbdaf8b-9188-4651-bce1-9115dd57c98b/resourceGroups/vmtest/providers/Microsoft.Compute/images/myImage"
```

<span data-ttu-id="25488-119">Utwórz maszynę Wirtualną z zasobu obrazu z [az vmss utworzyć](/cli/azure/vmss#create):</span><span class="sxs-lookup"><span data-stu-id="25488-119">Create a VM from your image resource with [az vmss create](/cli/azure/vmss#create):</span></span>

```azurecli
az vmss create --resource-group myResourceGroup --name myScaleSet --image /subscriptions/afbdaf8b-9188-4651-bce1-9115dd57c98b/resourceGroups/vmtest/providers/Microsoft.Compute/images/myImage --upgrade-policy-mode automatic --vm-sku Standard_DS1_v2 --data-disk-sizes-gb 10 --admin-username azureuser --generate-ssh-keys
```

<span data-ttu-id="25488-120">To polecenie również dołączyć dysku danych 10gb.</span><span class="sxs-lookup"><span data-stu-id="25488-120">This command also attached a 10gb data disk.</span></span> <span data-ttu-id="25488-121">Należy pamiętać, że w zależności od maszyny Wirtualnej wybrany rozmiar (użyliśmy **Standard_DS1_v2**), liczba dysków z danymi dozwolone, jest inny.</span><span class="sxs-lookup"><span data-stu-id="25488-121">Keep in mind that depending on the VM size chosen (we used **Standard_DS1_v2**), the number of data disks allowed is different.</span></span> <span data-ttu-id="25488-122">Aby uzyskać więcej informacji, przejrzyj [rozmiarów maszyn wirtualnych](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="25488-122">For more information, review the [virtual machine sizes](sizes.md).</span></span>

<span data-ttu-id="25488-123">Po zakończeniu skali się z nim połączyć.</span><span class="sxs-lookup"><span data-stu-id="25488-123">Once the scale set finishes, connect to it.</span></span> <span data-ttu-id="25488-124">Pobierz listę adresów IP dla wystąpień SSH z [az vmss listy--połączenia — informacje o wystąpieniu](/cli/azure/vmss#list-instance-connection-info):</span><span class="sxs-lookup"><span data-stu-id="25488-124">Get a list of IP addresses for the instances for SSH with [az vmss list-instance-connection-info](/cli/azure/vmss#list-instance-connection-info):</span></span>

```azurecli
az vmss list-instance-connection-info --resource-group myResourceGroup --name myScaleSet
```

```json
[
  "52.183.00.000:50000",
  "52.183.00.000:50003"
]
```

<span data-ttu-id="25488-125">Teraz możesz nawiązać połączenie wystąpienie maszyny wirtualnej, aby zainicjalizować dysk danych</span><span class="sxs-lookup"><span data-stu-id="25488-125">Now you can connect to the virtual machine instance to initialize the data disk</span></span>

```bash
ssh -i ~/.ssh/id_rsa.pub -p 50000 azureuser@52.183.00.000
```

## <a name="step-4---initialize-the-data-disk"></a><span data-ttu-id="25488-126">Krok 4 — zainicjalizować dysk danych</span><span class="sxs-lookup"><span data-stu-id="25488-126">Step 4 - Initialize the data disk</span></span>

<span data-ttu-id="25488-127">Podczas połączenia z maszyną wirtualną, partycji dysku z `fdisk`:</span><span class="sxs-lookup"><span data-stu-id="25488-127">While connected to the virtual machine, partition the disk with `fdisk`:</span></span>

```bash
(echo n; echo p; echo 1; echo  ; echo  ; echo w) | sudo fdisk /dev/sdc
```

<span data-ttu-id="25488-128">Zapis systemu plików z partycją `mkfs` polecenia:</span><span class="sxs-lookup"><span data-stu-id="25488-128">Write a file system to the partition with the `mkfs` command:</span></span>

```bash
sudo mkfs -t ext4 /dev/sdc1
```

<span data-ttu-id="25488-129">Zainstaluj nowy dysk, tak aby była dostępna w systemie operacyjnym:</span><span class="sxs-lookup"><span data-stu-id="25488-129">Mount the new disk so that it is accessible in the operating system:</span></span>

```bash
sudo mkdir /datadrive ; sudo mount /dev/sdc1 /datadrive
```

<span data-ttu-id="25488-130">Dysk można teraz dostęp za pośrednictwem datadrive punktu instalacji, który można sprawdzić przy `ls /datadrive/`.</span><span class="sxs-lookup"><span data-stu-id="25488-130">The disk can now be accesses through the datadrive mountpoint, which can be verified with `ls /datadrive/`.</span></span>

<span data-ttu-id="25488-131">Zakończyć sesję SSH.</span><span class="sxs-lookup"><span data-stu-id="25488-131">End the SSH session.</span></span>


## <a name="step-5---configure-firewall"></a><span data-ttu-id="25488-132">Krok 5 — Konfigurowanie zapory</span><span class="sxs-lookup"><span data-stu-id="25488-132">Step 5 - Configure firewall</span></span>

<span data-ttu-id="25488-133">Dziurkowanie przerw za pośrednictwem zapory, serwer sieci Web obsługiwane przez zestaw skali.</span><span class="sxs-lookup"><span data-stu-id="25488-133">Punch a hole through the firewall to the webserver hosted by the scale set.</span></span> <span data-ttu-id="25488-134">Podczas tworzenia zestawu skali, usługi równoważenia obciążenia została także utworzona i użyto go **SSH** do poszczególnych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="25488-134">When the scale set was created, a load balancer was also created, and you used it **SSH** to the individual virtual machines.</span></span> <span data-ttu-id="25488-135">Aby otworzyć port, potrzebne informacje, którą można uzyskać przy użyciu wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="25488-135">To open a port, you need two pieces of information, which you can get using Azure CLI.</span></span>

* <span data-ttu-id="25488-136">**Pula adresów IP frontonu**</span><span class="sxs-lookup"><span data-stu-id="25488-136">**Frontend IP address pool**</span></span>  
`az network lb show --resource-group myResourceGroup --name myScaleSetLB --output table --query frontendIpConfigurations[0].name`

* <span data-ttu-id="25488-137">**Pula adresów IP zaplecza**</span><span class="sxs-lookup"><span data-stu-id="25488-137">**Backend IP address pool**</span></span>  
`az network lb show --resource-group myResourceGroup --name myScaleSetLB --output table --query backendAddressPools[0].name`

<span data-ttu-id="25488-138">Przy użyciu tych dwóch nazw, należy otworzyć port **80**.</span><span class="sxs-lookup"><span data-stu-id="25488-138">With those two names, you can open port **80**.</span></span>

```azurecli
az network lb rule create --backend-pool-name myScaleSetLBBEPool --backend-port 80 --frontend-ip-name loadBalancerFrontEnd --frontend-port 80 --name webserver --protocol tcp --resource-group myResourceGroup --lb-name myScaleSetLB
```


## <a name="step-6---automate-configuration"></a><span data-ttu-id="25488-139">Krok 6 — automatyzowania konfiguracji</span><span class="sxs-lookup"><span data-stu-id="25488-139">Step 6 - Automate configuration</span></span>

<span data-ttu-id="25488-140">Dysk z danymi musi zostać skonfigurowane na każde wystąpienie maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="25488-140">The data disk needs to be configured on each virtual machine instance.</span></span> <span data-ttu-id="25488-141">Firma Microsoft można zautomatyzować konfigurację maszyny wirtualnej o **CustomScript** rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="25488-141">We can automate the configuration of the virtual machine with the **CustomScript** extension.</span></span>

<span data-ttu-id="25488-142">Najpierw utwórz *SH* skryptu, który zawiera polecenia format dysku.</span><span class="sxs-lookup"><span data-stu-id="25488-142">First, create a *.sh* script that includes the disk format commands.</span></span>

```sh
#!/bin/bash

# Setup the data disk
(echo n; echo p; echo 1; echo  ; echo  ; echo w) | fdisk /dev/sdc
fdisk /dev/sdc
mkfs -t ext4 /dev/sdc1
mkdir /datadrive
mount /dev/sdc1 /datadrive

exit 0
```

<span data-ttu-id="25488-143">Następnie przekazywanie tego pliku skryptu do where **CustomScript** rozszerzenia do niego dostęp.</span><span class="sxs-lookup"><span data-stu-id="25488-143">Next, upload that script file to where the **CustomScript** extension can access it.</span></span> <span data-ttu-id="25488-144">Jest dostępna kopia [tutaj](https://gist.githubusercontent.com/Thraka/ab1d8b78ac4b23722f3d3c1c03ac5df4).</span><span class="sxs-lookup"><span data-stu-id="25488-144">A copy is available [here](https://gist.githubusercontent.com/Thraka/ab1d8b78ac4b23722f3d3c1c03ac5df4).</span></span>

<span data-ttu-id="25488-145">Tworzenie pliku lokalnego o nazwie **settings.json** i umieszcza w nim następujący blok JSON.</span><span class="sxs-lookup"><span data-stu-id="25488-145">Create a local file named **settings.json** and put the following JSON block in it.</span></span> <span data-ttu-id="25488-146">`flieUris` Właściwość powinna być ustawiona, gdy plik skryptu została przekazana do.</span><span class="sxs-lookup"><span data-stu-id="25488-146">The `flieUris` property should be set to where your script file was uploaded to.</span></span>

```json
{
  "fileUris": ["https://gist.githubusercontent.com/Thraka/ab1d8b78ac4b23722f3d3c1c03ac5df4/raw/3ac6e385010ac675e23ce583ce27b1a752f1b482/prep-vmss.sh"],
  "commandToExecute": "bash prep-vmss.sh" 
}
```

<span data-ttu-id="25488-147">Wdrożyć na skalę ustawiony za pomocą tego polecenia **CustomScript** rozszerzenia, odwołuje się do **settings.json** właśnie utworzony plik.</span><span class="sxs-lookup"><span data-stu-id="25488-147">Deploy this command to your scale set with the **CustomScript** extension, referencing the **settings.json** file we just created.</span></span>

```azurecli
az vmss extension set --publisher Microsoft.Azure.Extensions --version 2.0 --name CustomScript --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

<span data-ttu-id="25488-148">To rozszerzenie automatycznie wykorzystuje wszystkie bieżące wystąpienia i wystąpienia utworzone później przez skalowanie.</span><span class="sxs-lookup"><span data-stu-id="25488-148">This extension automatically runs on all current instances, and any instances later created by scaling.</span></span>

## <a name="step-7---configure-autoscale-rules"></a><span data-ttu-id="25488-149">Krok 7 — Konfigurowanie reguł automatycznego skalowania</span><span class="sxs-lookup"><span data-stu-id="25488-149">Step 7 - Configure autoscale rules</span></span>

<span data-ttu-id="25488-150">Obecnie reguł skalowania automatycznego nie można ustawić w wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="25488-150">Currently, autoscale rules cannot be set in Azure CLI.</span></span> <span data-ttu-id="25488-151">Użyj [portalu Azure](https://portal.azure.com) skonfigurowanie automatycznego skalowania.</span><span class="sxs-lookup"><span data-stu-id="25488-151">Use the [Azure portal](https://portal.azure.com) to configure autoscale.</span></span>

## <a name="step-8---management-tasks"></a><span data-ttu-id="25488-152">Krok 8 - zadania zarządzania</span><span class="sxs-lookup"><span data-stu-id="25488-152">Step 8 - Management tasks</span></span>

<span data-ttu-id="25488-153">W całym cyklu życia zestawu skalowania konieczne może być Uruchom jedno lub więcej zadań zarządzania.</span><span class="sxs-lookup"><span data-stu-id="25488-153">Throughout the lifecycle of the scale set, you may need to run one or more management tasks.</span></span> <span data-ttu-id="25488-154">Ponadto może zajść potrzeba tworzenia skryptów automatyzujących różnych zadań cykl życia i interfejsu wiersza polecenia Azure zapewnia szybki sposób wykonywania tych zadań.</span><span class="sxs-lookup"><span data-stu-id="25488-154">Additionally, you may want to create scripts that automate various lifecycle-tasks, and the Azure CLI provides a quick way to do those tasks.</span></span> <span data-ttu-id="25488-155">Poniżej przedstawiono kilka typowych zadań.</span><span class="sxs-lookup"><span data-stu-id="25488-155">Here are a few common tasks.</span></span>

### <a name="get-connection-info"></a><span data-ttu-id="25488-156">Pobierz informacje o połączeniu</span><span class="sxs-lookup"><span data-stu-id="25488-156">Get connection info</span></span>

```azurecli
az vmss list-instance-connection-info --resource-group myResourceGroup --name myScaleSet
```

### <a name="set-instance-count-manual-scale"></a><span data-ttu-id="25488-157">Ustaw liczbę wystąpień (Ręczne skala)</span><span class="sxs-lookup"><span data-stu-id="25488-157">Set instance count (manual scale)</span></span>

```azurecli
az vmss scale --resource-group myResourceGroup --name myScaleSet --new-capacity 4
```

### <a name="delete-resource-group"></a><span data-ttu-id="25488-158">Usuń grupę zasobów</span><span class="sxs-lookup"><span data-stu-id="25488-158">Delete resource group</span></span>

<span data-ttu-id="25488-159">Usunięcie grupy zasobów powoduje usunięcie wszystkie zasoby zawarte w ciągu.</span><span class="sxs-lookup"><span data-stu-id="25488-159">Deleting a resource group also deletes all resources contained within.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="25488-160">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="25488-160">Next steps</span></span>
<span data-ttu-id="25488-161">Aby dowiedzieć się więcej na temat niektóre funkcje zestawu skali maszyny wirtualnej, wprowadzone w tym samouczku, zobacz następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="25488-161">To learn more about some of the virtual machine scale set features introduced in this tutorial, see the following information:</span></span>

- [<span data-ttu-id="25488-162">Omówienie usługi Azure zestawy skalowania maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="25488-162">Azure Virtual Machine Scale Sets overview</span></span>](../../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md)
- [<span data-ttu-id="25488-163">Omówienie usługi Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="25488-163">Azure Load Balancer overview</span></span>](../../load-balancer/load-balancer-overview.md)
- [<span data-ttu-id="25488-164">Sterowaniu przepływem ruchu sieciowego z grup zabezpieczeń sieci</span><span class="sxs-lookup"><span data-stu-id="25488-164">Control network traffic flow with network security groups</span></span>](../../virtual-network/virtual-networks-nsg.md)