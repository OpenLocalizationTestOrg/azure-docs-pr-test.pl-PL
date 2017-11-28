---
title: Utworzenie kopii maszyny Wirtualnej systemu Linux z interfejsu wiersza polecenia platformy Azure w wersji 1.0 | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak utworzyć kopię maszyny wirtualnej systemu Linux platformy Azure z 1.0 interfejsu wiersza polecenia platformy Azure w modelu wdrażania usługi Resource Manager"
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
tags: azure-resource-manager
ms.assetid: 770569d2-23c1-4a5b-801e-cddcd1375164
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/22/2017
ms.author: cynthn
ms.openlocfilehash: 62ae54f3596c9383cbf3b401fcfdb42ecfdee63c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-copy-of-a-linux-virtual-machine-running-on-azure-with-the-azure-cli-10"></a><span data-ttu-id="6c141-103">Utworzenie kopii maszyny wirtualnej systemu Linux działających na platformie Azure z interfejsu wiersza polecenia platformy Azure w wersji 1.0</span><span class="sxs-lookup"><span data-stu-id="6c141-103">Create a copy of a Linux virtual machine running on Azure with the Azure CLI 1.0</span></span>
<span data-ttu-id="6c141-104">W tym artykule pokazano, jak utworzyć kopię Azure maszyny wirtualnej (VM) systemem Linux przy użyciu modelu wdrażania Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="6c141-104">This article shows you how to create a copy of your Azure virtual machine (VM) running Linux using the Resource Manager deployment model.</span></span> <span data-ttu-id="6c141-105">Najpierw skopiowaniu za pośrednictwem systemu operacyjnego i dysków z danymi do nowego kontenera, a następnie skonfigurować zasoby sieciowe i tworzenie nowej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6c141-105">First you copy over the operating system and data disks to a new container, then set up the network resources and create the new virtual machine.</span></span>

<span data-ttu-id="6c141-106">Możesz również [przekazywanie i tworzenie maszyny Wirtualnej z obrazu niestandardowego dysku](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6c141-106">You can also [upload and create a VM from custom disk image](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="6c141-107">Wersje interfejsu wiersza polecenia umożliwiające wykonanie zadania</span><span class="sxs-lookup"><span data-stu-id="6c141-107">CLI versions to complete the task</span></span>
<span data-ttu-id="6c141-108">Zadanie można wykonać przy użyciu jednej z następujących wersji interfejsu wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="6c141-108">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="6c141-109">Interfejs wiersza polecenia platformy Azure w wersji 1.0 — nasz interfejs wiersza polecenia dla klasycznego modelu wdrażania i modelu wdrażania na potrzeby zarządzania zasobami (w tym artykule)</span><span class="sxs-lookup"><span data-stu-id="6c141-109">Azure CLI 1.0 – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="6c141-110">[Interfejs wiersza polecenia platformy Azure w wersji 2.0](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) — nasz interfejs wiersza polecenia nowej generacji dla modelu wdrażania na potrzeby zarządzania zasobami</span><span class="sxs-lookup"><span data-stu-id="6c141-110">[Azure CLI 2.0](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="6c141-111">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="6c141-111">Before you begin</span></span>
<span data-ttu-id="6c141-112">Upewnij się, spełnia następujące wymagania wstępne, przed rozpoczęciem kroków:</span><span class="sxs-lookup"><span data-stu-id="6c141-112">Ensure that you meet the following prerequisites before you start the steps:</span></span>

* <span data-ttu-id="6c141-113">Masz [interfejsu wiersza polecenia Azure](../../cli-install-nodejs.md) pobrane i zainstalowane na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="6c141-113">You have the [Azure CLI](../../cli-install-nodejs.md) downloaded and installed on your machine.</span></span> 
* <span data-ttu-id="6c141-114">Należy również pewne informacje o istniejącej maszyny Wirtualnej systemu Linux platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="6c141-114">You also need some information about your existing Azure Linux VM:</span></span>

| <span data-ttu-id="6c141-115">Informacje o źródle maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="6c141-115">Source VM information</span></span> | <span data-ttu-id="6c141-116">Skąd uzyskać</span><span class="sxs-lookup"><span data-stu-id="6c141-116">Where to get it</span></span> |
| --- | --- |
| <span data-ttu-id="6c141-117">Nazwa maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="6c141-117">VM name</span></span> |`azure vm list` |
| <span data-ttu-id="6c141-118">Nazwa grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="6c141-118">Resource Group name</span></span> |`azure vm list` |
| <span data-ttu-id="6c141-119">Lokalizacja</span><span class="sxs-lookup"><span data-stu-id="6c141-119">Location</span></span> |`azure vm list` |
| <span data-ttu-id="6c141-120">Nazwa konta magazynu</span><span class="sxs-lookup"><span data-stu-id="6c141-120">Storage Account name</span></span> |`azure storage account list -g <resourceGroup>` |
| <span data-ttu-id="6c141-121">Nazwa kontenera</span><span class="sxs-lookup"><span data-stu-id="6c141-121">Container name</span></span> |`azure storage container list -a <sourcestorageaccountname>` |
| <span data-ttu-id="6c141-122">Nazwa pliku wirtualnego dysku twardego maszyny Wirtualnej źródłowego</span><span class="sxs-lookup"><span data-stu-id="6c141-122">Source VM VHD file name</span></span> |`azure storage blob list --container <containerName>` |

* <span data-ttu-id="6c141-123">Należy zmienić kilka opcji dotyczących nowej maszyny Wirtualnej:   </span><span class="sxs-lookup"><span data-stu-id="6c141-123">You will need to make some choices about your new VM:    </span></span><br> <span data-ttu-id="6c141-124">-Nazwa kontenera   </span><span class="sxs-lookup"><span data-stu-id="6c141-124">-Container name    </span></span><br> <span data-ttu-id="6c141-125">-Nazwa maszyny Wirtualnej   </span><span class="sxs-lookup"><span data-stu-id="6c141-125">-VM name    </span></span><br> <span data-ttu-id="6c141-126">Rozmiar maszyny Wirtualnej —   </span><span class="sxs-lookup"><span data-stu-id="6c141-126">-VM size    </span></span><br> <span data-ttu-id="6c141-127">Nazwa sieci wirtualnej-   </span><span class="sxs-lookup"><span data-stu-id="6c141-127">-vNet name    </span></span><br> <span data-ttu-id="6c141-128">-Nazwa podsieci   </span><span class="sxs-lookup"><span data-stu-id="6c141-128">-SubNet name    </span></span><br> <span data-ttu-id="6c141-129">Nazwa - IP   </span><span class="sxs-lookup"><span data-stu-id="6c141-129">-IP Name    </span></span><br> <span data-ttu-id="6c141-130">Nazwa - NIC</span><span class="sxs-lookup"><span data-stu-id="6c141-130">-NIC name</span></span>

## <a name="login-and-set-your-subscription"></a><span data-ttu-id="6c141-131">Logowania i ustaw swoją subskrypcję</span><span class="sxs-lookup"><span data-stu-id="6c141-131">Login and set your subscription</span></span>
1. <span data-ttu-id="6c141-132">Zaloguj się do interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="6c141-132">Login to the CLI.</span></span>

    ```azurecli
    azure login
    ```
2. <span data-ttu-id="6c141-133">Upewnij się, że jesteś w trybie Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="6c141-133">Make sure you are in Resource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```
3. <span data-ttu-id="6c141-134">Ustaw poprawną subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="6c141-134">Set the correct subscription.</span></span> <span data-ttu-id="6c141-135">"Lista konto platformy azure" można użyć do wyświetlenia wszystkich subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="6c141-135">You can use 'azure account list' to see all of your subscriptions.</span></span>

    ```azurecli
    azure account set mySubscriptionID
    ```

## <a name="stop-the-vm"></a><span data-ttu-id="6c141-136">Zatrzymywanie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="6c141-136">Stop the VM</span></span>
<span data-ttu-id="6c141-137">Zatrzymaj i cofnięcia przydzielenia źródłowej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6c141-137">Stop and deallocate the source VM.</span></span> <span data-ttu-id="6c141-138">"Lista maszyna wirtualna platformy azure" można użyć w celu uzyskania listy wszystkich maszyn wirtualnych w Twojej subskrypcji i zasobu ich nazwy grup.</span><span class="sxs-lookup"><span data-stu-id="6c141-138">You can use 'azure vm list' to get a list of all of the VMs in your subscription and their resource group names.</span></span>

```azurecli
azure vm stop myResourceGroup myVM
azure vm deallocate myResourceGroup MyVM
```


## <a name="copy-the-vhd"></a><span data-ttu-id="6c141-139">Skopiuj wirtualny dysk twardy</span><span class="sxs-lookup"><span data-stu-id="6c141-139">Copy the VHD</span></span>
<span data-ttu-id="6c141-140">Możesz skopiować wirtualny dysk twardy z magazynu źródłowego do docelowego przy użyciu `azure storage blob copy start`.</span><span class="sxs-lookup"><span data-stu-id="6c141-140">You can copy the VHD from the source storage to the destination using the `azure storage blob copy start`.</span></span> <span data-ttu-id="6c141-141">W tym przykładzie zamierzamy Skopiuj wirtualny dysk twardy do tego samego konta magazynu, ale różnych kontenerów.</span><span class="sxs-lookup"><span data-stu-id="6c141-141">In this example, we are going to copy the VHD to the same storage account, but a different container.</span></span>

<span data-ttu-id="6c141-142">Aby skopiować dysk VHD do innego kontenera, w tym samym koncie magazynu, wpisz:</span><span class="sxs-lookup"><span data-stu-id="6c141-142">To copy the VHD to another container in the same storage account, type:</span></span>

```azurecli
azure storage blob copy start \
        https://mystorageaccountname.blob.core.windows.net:8080/mycontainername/myVHD.vhd \
        myNewContainerName
```

## <a name="set-up-the-virtual-network-for-your-new-vm"></a><span data-ttu-id="6c141-143">Konfigurowanie sieci wirtualnej dla nowej maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="6c141-143">Set up the virtual network for your new VM</span></span>
<span data-ttu-id="6c141-144">Konfigurowanie sieci wirtualnej i karty Sieciowej dla nowej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6c141-144">Set up a virtual network and NIC for your new VM.</span></span> 

```azurecli
azure network vnet create myResourceGroup myVnet -l myLocation

azure network vnet subnet create -a <address.prefix.in.CIDR/format> myResourceGroup myVnet mySubnet

azure network public-ip create myResourceGroup myPublicIP -l myLocation

azure network nic create myResourceGroup myNic -k mySubnet -m myVnet -p myPublicIP -l myLocation
```


## <a name="create-the-new-vm"></a><span data-ttu-id="6c141-145">Tworzenie nowej maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="6c141-145">Create the new VM</span></span>
<span data-ttu-id="6c141-146">Teraz można utworzyć maszyny Wirtualnej z dysku wirtualnego przekazane [przy użyciu szablonu usługi resource manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd) lub za pomocą interfejsu wiersza polecenia, określając identyfikator URI do skopiowanego dysku, wpisując:</span><span class="sxs-lookup"><span data-stu-id="6c141-146">You can now create a VM from your uploaded virtual disk [using a resource manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd) or through the CLI by specifying the URI to your copied disk by typing:</span></span>

```azurecli
azure vm create -n myVM -l myLocation -g myResourceGroup -f myNic \
        -z Standard_DS1_v2 -y Linux \
        https://mystorageaccountname.blob.core.windows.net:8080/mycontainername/myVHD.vhd 
```



## <a name="next-steps"></a><span data-ttu-id="6c141-147">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6c141-147">Next steps</span></span>
<span data-ttu-id="6c141-148">Aby dowiedzieć się, jak zarządzać nowej maszyny wirtualnej za pomocą wiersza polecenia platformy Azure, zobacz [polecenia wiersza polecenia platformy Azure dla Menedżera zasobów Azure](../azure-cli-arm-commands.md).</span><span class="sxs-lookup"><span data-stu-id="6c141-148">To learn how to use Azure CLI to manage your new virtual machine, see [Azure CLI commands for the Azure Resource Manager](../azure-cli-arm-commands.md).</span></span>

