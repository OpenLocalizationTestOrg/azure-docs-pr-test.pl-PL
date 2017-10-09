---
title: "aaaCreate kopię maszyny Wirtualnej systemu Linux z hello Azure CLI 1.0 | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate kopia maszyny wirtualnej systemu Linux platformy Azure z hello Azure CLI 1.0 w modelu wdrażania usługi Resource Manager hello"
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
ms.openlocfilehash: 997a2c8109e7083ececd76fd1013e9ed4d3e6afd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-copy-of-a-linux-virtual-machine-running-on-azure-with-hello-azure-cli-10"></a><span data-ttu-id="e0cd2-103">Utworzenie kopii maszyny wirtualnej systemu Linux działających na platformie Azure z hello Azure CLI w wersji 1.0</span><span class="sxs-lookup"><span data-stu-id="e0cd2-103">Create a copy of a Linux virtual machine running on Azure with hello Azure CLI 1.0</span></span>
<span data-ttu-id="e0cd2-104">W tym artykule opisano, jak toocreate kopię sieci maszyny wirtualnej platformy Azure (VM) uruchomionego systemu Linux przy użyciu hello modelu wdrażania usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e0cd2-104">This article shows you how toocreate a copy of your Azure virtual machine (VM) running Linux using hello Resource Manager deployment model.</span></span> <span data-ttu-id="e0cd2-105">Najpierw skopiować hello systemu operacyjnego i dysków tooa nowy kontener danych, a następnie skonfigurowaniu hello zasobów sieciowych i tworzenie nowej maszyny wirtualnej hello.</span><span class="sxs-lookup"><span data-stu-id="e0cd2-105">First you copy over hello operating system and data disks tooa new container, then set up hello network resources and create hello new virtual machine.</span></span>

<span data-ttu-id="e0cd2-106">Możesz również [przekazywanie i tworzenie maszyny Wirtualnej z obrazu niestandardowego dysku](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e0cd2-106">You can also [upload and create a VM from custom disk image](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="e0cd2-107">Zadanie hello toocomplete wersje interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="e0cd2-107">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="e0cd2-108">Można ukończyć powitalnych zadań przy użyciu jednej z hello następujące wersje interfejsu wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="e0cd2-108">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="e0cd2-109">Azure CLI 1.0 — nasze interfejsu wiersza polecenia dla hello classic i zasobów zarządzania wdrażania modeli (w tym artykule)</span><span class="sxs-lookup"><span data-stu-id="e0cd2-109">Azure CLI 1.0 – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="e0cd2-110">[Azure CLI 2.0](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -naszej nowej generacji interfejsu wiersza polecenia dla modelu wdrażania zarządzania zasobów hello</span><span class="sxs-lookup"><span data-stu-id="e0cd2-110">[Azure CLI 2.0](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="e0cd2-111">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="e0cd2-111">Before you begin</span></span>
<span data-ttu-id="e0cd2-112">Upewnij się, czy zostały spełnione następujące wymagania wstępne, przed rozpoczęciem powitalne kroki hello:</span><span class="sxs-lookup"><span data-stu-id="e0cd2-112">Ensure that you meet hello following prerequisites before you start hello steps:</span></span>

* <span data-ttu-id="e0cd2-113">Masz hello [interfejsu wiersza polecenia Azure](../../cli-install-nodejs.md) pobrane i zainstalowane na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="e0cd2-113">You have hello [Azure CLI](../../cli-install-nodejs.md) downloaded and installed on your machine.</span></span> 
* <span data-ttu-id="e0cd2-114">Należy również pewne informacje o istniejącej maszyny Wirtualnej systemu Linux platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="e0cd2-114">You also need some information about your existing Azure Linux VM:</span></span>

| <span data-ttu-id="e0cd2-115">Informacje o źródle maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="e0cd2-115">Source VM information</span></span> | <span data-ttu-id="e0cd2-116">Gdzie tooget go</span><span class="sxs-lookup"><span data-stu-id="e0cd2-116">Where tooget it</span></span> |
| --- | --- |
| <span data-ttu-id="e0cd2-117">Nazwa maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="e0cd2-117">VM name</span></span> |`azure vm list` |
| <span data-ttu-id="e0cd2-118">Nazwa grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="e0cd2-118">Resource Group name</span></span> |`azure vm list` |
| <span data-ttu-id="e0cd2-119">Lokalizacja</span><span class="sxs-lookup"><span data-stu-id="e0cd2-119">Location</span></span> |`azure vm list` |
| <span data-ttu-id="e0cd2-120">Nazwa konta magazynu</span><span class="sxs-lookup"><span data-stu-id="e0cd2-120">Storage Account name</span></span> |`azure storage account list -g <resourceGroup>` |
| <span data-ttu-id="e0cd2-121">Nazwa kontenera</span><span class="sxs-lookup"><span data-stu-id="e0cd2-121">Container name</span></span> |`azure storage container list -a <sourcestorageaccountname>` |
| <span data-ttu-id="e0cd2-122">Nazwa pliku wirtualnego dysku twardego maszyny Wirtualnej źródłowego</span><span class="sxs-lookup"><span data-stu-id="e0cd2-122">Source VM VHD file name</span></span> |`azure storage blob list --container <containerName>` |

* <span data-ttu-id="e0cd2-123">Konieczne będzie toomake kilka opcji dotyczących nowej maszyny Wirtualnej:   </span><span class="sxs-lookup"><span data-stu-id="e0cd2-123">You will need toomake some choices about your new VM:    </span></span><br> <span data-ttu-id="e0cd2-124">-Nazwa kontenera   </span><span class="sxs-lookup"><span data-stu-id="e0cd2-124">-Container name    </span></span><br> <span data-ttu-id="e0cd2-125">-Nazwa maszyny Wirtualnej   </span><span class="sxs-lookup"><span data-stu-id="e0cd2-125">-VM name    </span></span><br> <span data-ttu-id="e0cd2-126">Rozmiar maszyny Wirtualnej —   </span><span class="sxs-lookup"><span data-stu-id="e0cd2-126">-VM size    </span></span><br> <span data-ttu-id="e0cd2-127">Nazwa sieci wirtualnej-   </span><span class="sxs-lookup"><span data-stu-id="e0cd2-127">-vNet name    </span></span><br> <span data-ttu-id="e0cd2-128">-Nazwa podsieci   </span><span class="sxs-lookup"><span data-stu-id="e0cd2-128">-SubNet name    </span></span><br> <span data-ttu-id="e0cd2-129">Nazwa - IP   </span><span class="sxs-lookup"><span data-stu-id="e0cd2-129">-IP Name    </span></span><br> <span data-ttu-id="e0cd2-130">Nazwa - NIC</span><span class="sxs-lookup"><span data-stu-id="e0cd2-130">-NIC name</span></span>

## <a name="login-and-set-your-subscription"></a><span data-ttu-id="e0cd2-131">Logowania i ustaw swoją subskrypcję</span><span class="sxs-lookup"><span data-stu-id="e0cd2-131">Login and set your subscription</span></span>
1. <span data-ttu-id="e0cd2-132">Toohello logowania interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="e0cd2-132">Login toohello CLI.</span></span>

    ```azurecli
    azure login
    ```
2. <span data-ttu-id="e0cd2-133">Upewnij się, że jesteś w trybie Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="e0cd2-133">Make sure you are in Resource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```
3. <span data-ttu-id="e0cd2-134">Ustaw hello poprawną subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="e0cd2-134">Set hello correct subscription.</span></span> <span data-ttu-id="e0cd2-135">Można użyć "Lista konto platformy azure" toosee wszystkich subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="e0cd2-135">You can use 'azure account list' toosee all of your subscriptions.</span></span>

    ```azurecli
    azure account set mySubscriptionID
    ```

## <a name="stop-hello-vm"></a><span data-ttu-id="e0cd2-136">Zatrzymaj hello maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="e0cd2-136">Stop hello VM</span></span>
<span data-ttu-id="e0cd2-137">Zatrzymaj i cofnięcia przydzielenia hello źródłowej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e0cd2-137">Stop and deallocate hello source VM.</span></span> <span data-ttu-id="e0cd2-138">Można użyć "Lista maszyna wirtualna platformy azure" tooget listę wszystkich hello maszyn wirtualnych w subskrypcji i ich nazwy grup zasobów.</span><span class="sxs-lookup"><span data-stu-id="e0cd2-138">You can use 'azure vm list' tooget a list of all of hello VMs in your subscription and their resource group names.</span></span>

```azurecli
azure vm stop myResourceGroup myVM
azure vm deallocate myResourceGroup MyVM
```


## <a name="copy-hello-vhd"></a><span data-ttu-id="e0cd2-139">Skopiuj hello wirtualnego dysku twardego</span><span class="sxs-lookup"><span data-stu-id="e0cd2-139">Copy hello VHD</span></span>
<span data-ttu-id="e0cd2-140">Możesz skopiować hello wirtualnego dysku twardego z hello źródła toohello miejscem docelowym magazynu przy użyciu hello `azure storage blob copy start`.</span><span class="sxs-lookup"><span data-stu-id="e0cd2-140">You can copy hello VHD from hello source storage toohello destination using hello `azure storage blob copy start`.</span></span> <span data-ttu-id="e0cd2-141">W tym przykładzie zamierzamy toocopy hello wirtualnego dysku twardego toohello tego samego konta magazynu, ale różnych kontenerów.</span><span class="sxs-lookup"><span data-stu-id="e0cd2-141">In this example, we are going toocopy hello VHD toohello same storage account, but a different container.</span></span>

<span data-ttu-id="e0cd2-142">kontener tooanother toocopy hello wirtualnego dysku twardego w hello tego samego konta magazynu, wpisz:</span><span class="sxs-lookup"><span data-stu-id="e0cd2-142">toocopy hello VHD tooanother container in hello same storage account, type:</span></span>

```azurecli
azure storage blob copy start \
        https://mystorageaccountname.blob.core.windows.net:8080/mycontainername/myVHD.vhd \
        myNewContainerName
```

## <a name="set-up-hello-virtual-network-for-your-new-vm"></a><span data-ttu-id="e0cd2-143">Konfigurowanie sieci wirtualnej hello dla nowej maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="e0cd2-143">Set up hello virtual network for your new VM</span></span>
<span data-ttu-id="e0cd2-144">Konfigurowanie sieci wirtualnej i karty Sieciowej dla nowej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e0cd2-144">Set up a virtual network and NIC for your new VM.</span></span> 

```azurecli
azure network vnet create myResourceGroup myVnet -l myLocation

azure network vnet subnet create -a <address.prefix.in.CIDR/format> myResourceGroup myVnet mySubnet

azure network public-ip create myResourceGroup myPublicIP -l myLocation

azure network nic create myResourceGroup myNic -k mySubnet -m myVnet -p myPublicIP -l myLocation
```


## <a name="create-hello-new-vm"></a><span data-ttu-id="e0cd2-145">Utwórz hello nowej maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="e0cd2-145">Create hello new VM</span></span>
<span data-ttu-id="e0cd2-146">Teraz można utworzyć maszyny Wirtualnej z dysku wirtualnego przekazane [przy użyciu szablonu usługi resource manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd) lub za pośrednictwem hello interfejsu wiersza polecenia, określając hello URI tooyour skopiowanych dysku, wpisując:</span><span class="sxs-lookup"><span data-stu-id="e0cd2-146">You can now create a VM from your uploaded virtual disk [using a resource manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd) or through hello CLI by specifying hello URI tooyour copied disk by typing:</span></span>

```azurecli
azure vm create -n myVM -l myLocation -g myResourceGroup -f myNic \
        -z Standard_DS1_v2 -y Linux \
        https://mystorageaccountname.blob.core.windows.net:8080/mycontainername/myVHD.vhd 
```



## <a name="next-steps"></a><span data-ttu-id="e0cd2-147">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e0cd2-147">Next steps</span></span>
<span data-ttu-id="e0cd2-148">toolearn jak toomanage interfejsu wiersza polecenia Azure toouse nowej maszyny wirtualnej, zobacz [polecenia wiersza polecenia platformy Azure dla usługi Azure Resource Manager hello](../azure-cli-arm-commands.md).</span><span class="sxs-lookup"><span data-stu-id="e0cd2-148">toolearn how toouse Azure CLI toomanage your new virtual machine, see [Azure CLI commands for hello Azure Resource Manager](../azure-cli-arm-commands.md).</span></span>

