---
title: "aaaCopy Maszynę wirtualną systemu Linux przy użyciu interfejsu wiersza polecenia platformy Azure w wersji 2.0 | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate kopię maszyny Wirtualnej systemu Linux platformy Azure przy użyciu interfejsu wiersza polecenia platformy Azure w wersji 2.0 i dysków zarządzanych."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
tags: azure-resource-manager
ms.assetid: 770569d2-23c1-4a5b-801e-cddcd1375164
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 03/10/2017
ms.author: cynthn
ms.openlocfilehash: ee34a4259dd0c1e7bf49312fe3fe3ba809bf69e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-copy-of-a-linux-vm-by-using-azure-cli-20-and-managed-disks"></a><span data-ttu-id="b792e-103">Utworzenie kopii maszyny wirtualnej systemu Linux przy użyciu interfejsu wiersza polecenia platformy Azure w wersji 2.0 i dysków zarządzanych</span><span class="sxs-lookup"><span data-stu-id="b792e-103">Create a copy of a Linux VM by using Azure CLI 2.0 and Managed Disks</span></span>


<span data-ttu-id="b792e-104">W tym artykule opisano, jak toocreate kopię Azure maszyny wirtualnej (VM) systemem Linux przy użyciu hello Azure CLI w wersji 2.0 i modelu wdrażania usługi Azure Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="b792e-104">This article shows you how toocreate a copy of your Azure virtual machine (VM) running Linux using hello Azure CLI 2.0 and hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="b792e-105">Można również wykonać te kroki hello [Azure CLI 1.0](copy-vm-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b792e-105">You can also perform these steps with hello [Azure CLI 1.0](copy-vm-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="b792e-106">Możesz również [przekazywanie i tworzenie maszyny Wirtualnej z dysku VHD](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b792e-106">You can also [upload and create a VM from a VHD](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b792e-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="b792e-107">Prerequisites</span></span>


-   <span data-ttu-id="b792e-108">Zainstaluj [Azure CLI 2.0](/cli/azure/install-az-cli2)</span><span class="sxs-lookup"><span data-stu-id="b792e-108">Install [Azure CLI 2.0](/cli/azure/install-az-cli2)</span></span>

-   <span data-ttu-id="b792e-109">Zaloguj się tooan konto platformy Azure z [logowania az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="b792e-109">Sign in tooan Azure account with [az login](/cli/azure/#login).</span></span>

-   <span data-ttu-id="b792e-110">Ma toouse maszyny Wirtualnej platformy Azure jako hello źródła dla tej kopii.</span><span class="sxs-lookup"><span data-stu-id="b792e-110">Have an Azure VM toouse as hello source for your copy.</span></span>

## <a name="step-1-stop-hello-source-vm"></a><span data-ttu-id="b792e-111">Krok 1: Zatrzymaj hello źródłowej maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="b792e-111">Step 1: Stop hello source VM</span></span>


<span data-ttu-id="b792e-112">Cofnięcie przydziału hello źródłowej maszyny Wirtualnej za pomocą [deallocate wirtualna az](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="b792e-112">Deallocate hello source VM by using [az vm deallocate](/cli/azure/vm#deallocate).</span></span>
<span data-ttu-id="b792e-113">Witaj poniższy przykład cofa alokację hello maszyny Wirtualnej o nazwie **myVM** w grupie zasobów hello **myResourceGroup**:</span><span class="sxs-lookup"><span data-stu-id="b792e-113">hello following example deallocates hello VM named **myVM** in hello resource group **myResourceGroup**:</span></span>

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

## <a name="step-2-copy-hello-source-vm"></a><span data-ttu-id="b792e-114">Krok 2: Kopiowanie hello źródłowej maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="b792e-114">Step 2: Copy hello source VM</span></span>


<span data-ttu-id="b792e-115">toocopy Maszynę wirtualną, Utwórz kopię hello podstawowych dysków wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="b792e-115">toocopy a VM, you create a copy of hello underlying virtual hard disk.</span></span> <span data-ttu-id="b792e-116">Ten proces tworzy specjalne wirtualnego dysku twardego jako zarządzane dysk zawierający hello tej samej konfiguracji i ustawień, jak hello źródłowej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b792e-116">This process creates a specialized VHD as a Managed Disk that contains hello same configuration and settings as hello source VM.</span></span>

<span data-ttu-id="b792e-117">Aby uzyskać więcej informacji o dyskach Azure Managed Disks, zobacz [Omówienie usługi Azure Managed Disks](../windows/managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b792e-117">For more information about Azure Managed Disks, see [Azure Managed Disks overview](../windows/managed-disks-overview.md).</span></span> 

1.  <span data-ttu-id="b792e-118">Każda nazwa maszyny Wirtualnej i hello jej dysk systemu operacyjnego z [listy wirtualna az](/cli/azure/vm#list).</span><span class="sxs-lookup"><span data-stu-id="b792e-118">List each VM and hello name of its OS disk with [az vm list](/cli/azure/vm#list).</span></span> <span data-ttu-id="b792e-119">Witaj poniższy przykład zawiera listę wszystkich maszyn wirtualnych w grupie zasobów o nazwie **myResourceGroup**:</span><span class="sxs-lookup"><span data-stu-id="b792e-119">hello following example lists all VMs in the resource group named **myResourceGroup**:</span></span>
    
    ```azurecli
    az vm list -g myTestRG --query '[].{Name:name,DiskName:storageProfile.osDisk.name}' --output table
    ```

    <span data-ttu-id="b792e-120">Witaj danych wyjściowych jest toohello podobnie poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="b792e-120">hello output is similar toohello following example:</span></span>

    ```azurecli
    Name    DiskName
    ------  --------
    myVM    myDisk
    ```

1.  <span data-ttu-id="b792e-121">Kopiuj hello dysk, tworząc nowe zarządzane przy użyciu dysku [Tworzenie dysku az](/cli/azure/disk#create).</span><span class="sxs-lookup"><span data-stu-id="b792e-121">Copy hello disk by creating a new managed disk using [az disk create](/cli/azure/disk#create).</span></span> <span data-ttu-id="b792e-122">Witaj poniższy przykład tworzy dysk o nazwie **myCopiedDisk** z hello zarządzane dysku o nazwie **myDisk**:</span><span class="sxs-lookup"><span data-stu-id="b792e-122">hello following example creates a disk named **myCopiedDisk** from hello managed disk named **myDisk**:</span></span>

    ```azurecli
    az disk create --resource-group myResourceGroup --name myCopiedDisk --source myDisk
    ``` 

1.  <span data-ttu-id="b792e-123">Sprawdź hello zarządzane dysków w grupie zasobów za pomocą [Lista dysków az](/cli/azure/disk#list).</span><span class="sxs-lookup"><span data-stu-id="b792e-123">Verify hello managed disks now in your resource group by using [az disk list](/cli/azure/disk#list).</span></span> <span data-ttu-id="b792e-124">Hello poniższy przykład zawiera listę dysków hello zarządzane w hello grupy zasobów o nazwie **myResourceGroup**:</span><span class="sxs-lookup"><span data-stu-id="b792e-124">hello following example lists hello managed disks in hello resource group named **myResourceGroup**:</span></span>

    ```azurecli
    az disk list --resource-group myResourceGroup --output table
    ```

1.  <span data-ttu-id="b792e-125">Pomiń zbyt["krok 3: Konfigurowanie sieci wirtualnej"](#step-3-set-up-a-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="b792e-125">Skip too["Step 3: Set up a virtual network"](#step-3-set-up-a-virtual-network).</span></span>


## <a name="step-3-set-up-a-virtual-network"></a><span data-ttu-id="b792e-126">Krok 3: Konfigurowanie sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="b792e-126">Step 3: Set up a virtual network</span></span>


<span data-ttu-id="b792e-127">Witaj następujące opcjonalne kroki tworzenia nowej sieci wirtualnej, podsieci, publiczny adres IP i sieć wirtualna karta sieciowa (NIC).</span><span class="sxs-lookup"><span data-stu-id="b792e-127">hello following optional steps create a new virtual network, subnet, public IP address, and virtual network interface card (NIC).</span></span>

<span data-ttu-id="b792e-128">Jeśli kopiujesz Maszynę wirtualną do rozwiązywania problemów z celów lub dodatkowe wdrożenia, nie może być toouse maszyny Wirtualnej w ramach istniejącej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b792e-128">If you are copying a VM for troubleshooting purposes or additional deployments, you might not want toouse a VM in an existing virtual network.</span></span>

<span data-ttu-id="b792e-129">Jeśli chcesz toocreate infrastruktury sieci wirtualnej dla maszyn wirtualnych skopiowanych wykonaj hello obok kilku kroków.</span><span class="sxs-lookup"><span data-stu-id="b792e-129">If you want toocreate a virtual network infrastructure for your copied VMs, follow hello next few steps.</span></span> <span data-ttu-id="b792e-130">Jeśli nie chcesz toocreate sieci wirtualnej, Pomiń zbyt[krok 4: tworzenie maszyny Wirtualnej](#step-4-create-a-vm).</span><span class="sxs-lookup"><span data-stu-id="b792e-130">If you don't want toocreate a virtual network, skip too[Step 4: Create a VM](#step-4-create-a-vm).</span></span>

1.  <span data-ttu-id="b792e-131">Utwórz sieć wirtualną hello przy użyciu [tworzenie sieci wirtualnej sieci az](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="b792e-131">Create hello virtual network by using [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="b792e-132">Witaj poniższy przykład tworzy sieć wirtualną o nazwie **myVnet** i podsieć o nazwie **mySubnet**:</span><span class="sxs-lookup"><span data-stu-id="b792e-132">hello following example creates a virtual network named **myVnet** and a subnet named **mySubnet**:</span></span>

    ```azurecli
    az network vnet create --resource-group myResourceGroup --location westus --name myVnet \
        --address-prefix 192.168.0.0/16 --subnet-name mySubnet --subnet-prefix 192.168.1.0/24
    ```

1.  <span data-ttu-id="b792e-133">Tworzenie publicznego adresu IP za pomocą [utworzyć az sieci publicznej ip](/cli/azure/network/public-ip#create).</span><span class="sxs-lookup"><span data-stu-id="b792e-133">Create a public IP by using [az network public-ip create](/cli/azure/network/public-ip#create).</span></span> <span data-ttu-id="b792e-134">Witaj poniższy przykład tworzy publicznego adresu IP o nazwie **myPublicIP** o nazwie DNS hello **mypublicdns**.</span><span class="sxs-lookup"><span data-stu-id="b792e-134">hello following example creates a public IP named **myPublicIP** with hello DNS name of **mypublicdns**.</span></span> <span data-ttu-id="b792e-135">(nazwa DNS hello musi być unikatowa, więc Podaj unikatową nazwę.)</span><span class="sxs-lookup"><span data-stu-id="b792e-135">(hello DNS name must be unique, so provide a unique name.)</span></span>

    ```azurecli
    az network public-ip create --resource-group myResourceGroup --location westus \
        --name myPublicIP --dns-name mypublicdns --allocation-method static --idle-timeout 4
    ```

1.  <span data-ttu-id="b792e-136">Tworzenie przy użyciu kart hello [tworzenie kart interfejsu sieciowego az](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="b792e-136">Create hello NIC using [az network nic create](/cli/azure/network/nic#create).</span></span>
    <span data-ttu-id="b792e-137">Witaj poniższy przykład tworzy karty Sieciowej o nazwie **myNic** to jest dołączona toothe **mySubnet** podsieci:</span><span class="sxs-lookup"><span data-stu-id="b792e-137">hello following example creates a NIC named **myNic** that's attached toothe **mySubnet** subnet:</span></span>

    ```azurecli
    az network nic create --resource-group myResourceGroup --location westus --name myNic \
        --vnet-name myVnet --subnet mySubnet --public-ip-address myPublicIP
    ```

## <a name="step-4-create-a-vm"></a><span data-ttu-id="b792e-138">Krok 4: Tworzenie maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="b792e-138">Step 4: Create a VM</span></span>

<span data-ttu-id="b792e-139">Można teraz utworzyć Maszynę wirtualną za pomocą [tworzenia maszyny wirtualnej az](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="b792e-139">You can now create a VM by using [az vm create](/cli/azure/vm#create).</span></span>

<span data-ttu-id="b792e-140">Określ hello skopiowane toouse dysków zarządzanych jako dysk systemu operacyjnego hello (--attach-os-disk) w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="b792e-140">Specify hello copied managed disk toouse as hello OS disk (--attach-os-disk), as follows:</span></span>

```azurecli
az vm create --resource-group myResourceGroup --name myCopiedVM \
    --admin-username azureuser --ssh-key-value ~/.ssh/id_rsa.pub \
    --nics myNic --size Standard_DS1_v2 --os-type Linux \
    --attach-os-disk myCopiedDisk
```

## <a name="next-steps"></a><span data-ttu-id="b792e-141">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b792e-141">Next steps</span></span>

<span data-ttu-id="b792e-142">toolearn jak toomanage interfejsu wiersza polecenia Azure toouse nowej maszyny Wirtualnej, zobacz [polecenia wiersza polecenia platformy Azure dla usługi Azure Resource Manager hello](../azure-cli-arm-commands.md).</span><span class="sxs-lookup"><span data-stu-id="b792e-142">toolearn how toouse Azure CLI toomanage your new VM, see [Azure CLI commands for hello Azure Resource Manager](../azure-cli-arm-commands.md).</span></span>
