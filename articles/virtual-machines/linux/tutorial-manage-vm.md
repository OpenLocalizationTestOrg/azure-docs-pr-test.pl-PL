---
title: "aaaCreate i zarządzanie maszyn wirtualnych systemu Linux z hello Azure CLI | Dokumentacja firmy Microsoft"
description: "Samouczek — tworzenie i zarządzanie maszyn wirtualnych systemu Linux z hello wiersza polecenia platformy Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 05f7c1cf860f809bc13f110778d3bddd619ac6f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-linux-vms-with-hello-azure-cli"></a><span data-ttu-id="f9106-103">Tworzenie i zarządzanie maszyn wirtualnych systemu Linux z hello wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="f9106-103">Create and Manage Linux VMs with hello Azure CLI</span></span>

<span data-ttu-id="f9106-104">Maszyny wirtualne platformy Azure zawierają w pełni konfigurowalne i elastyczne środowiska komputerowego.</span><span class="sxs-lookup"><span data-stu-id="f9106-104">Azure virtual machines provide a fully configurable and flexible computing environment.</span></span> <span data-ttu-id="f9106-105">Ten samouczek obejmuje elementów wdrożenia podstawowej maszyny wirtualnej platformy Azure, takich jak rozmiar maszyny Wirtualnej, wybierając obrazu maszyny Wirtualnej i wdrażanie maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f9106-105">This tutorial covers basic Azure virtual machine deployment items such as selecting a VM size, selecting a VM image, and deploying a VM.</span></span> <span data-ttu-id="f9106-106">Omawiane kwestie:</span><span class="sxs-lookup"><span data-stu-id="f9106-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f9106-107">Tworzenie i łączenie tooa maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="f9106-107">Create and connect tooa VM</span></span>
> * <span data-ttu-id="f9106-108">Wybierz i używać obrazów maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="f9106-108">Select and use VM images</span></span>
> * <span data-ttu-id="f9106-109">Wyświetlanie i używanie określonych rozmiarów maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="f9106-109">View and use specific VM sizes</span></span>
> * <span data-ttu-id="f9106-110">Zmienianie rozmiaru maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="f9106-110">Resize a VM</span></span>
> * <span data-ttu-id="f9106-111">Wyświetlanie i zrozumienie stanu maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="f9106-111">View and understand VM state</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="f9106-112">Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym samouczku wymaga działają hello Azure CLI w wersji 2.0.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="f9106-112">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="f9106-113">Uruchom `az --version` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="f9106-113">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="f9106-114">Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="f9106-114">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-resource-group"></a><span data-ttu-id="f9106-115">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="f9106-115">Create resource group</span></span>

<span data-ttu-id="f9106-116">Utwórz grupę zasobów o hello [Tworzenie grupy az](https://docs.microsoft.com/cli/azure/group#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="f9106-116">Create a resource group with hello [az group create](https://docs.microsoft.com/cli/azure/group#create) command.</span></span> 

<span data-ttu-id="f9106-117">Grupa zasobów platformy Azure to logiczny kontener przeznaczony do wdrażania zasobów platformy Azure i zarządzania nimi.</span><span class="sxs-lookup"><span data-stu-id="f9106-117">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="f9106-118">Grupy zasobów musi zostać utworzone przed maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f9106-118">A resource group must be created before a virtual machine.</span></span> <span data-ttu-id="f9106-119">W tym przykładzie grupy zasobów o nazwie *myResourceGroupVM* jest tworzony w hello *eastus* regionu.</span><span class="sxs-lookup"><span data-stu-id="f9106-119">In this example, a resource group named *myResourceGroupVM* is created in hello *eastus* region.</span></span> 

```azurecli-interactive 
az group create --name myResourceGroupVM --location eastus
```

<span data-ttu-id="f9106-120">Grupa zasobów Hello jest określony, podczas tworzenia lub modyfikowania maszyn wirtualnych, które są widoczne w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="f9106-120">hello resource group is specified when creating or modifying a VM, which can be seen throughout this tutorial.</span></span>

## <a name="create-virtual-machine"></a><span data-ttu-id="f9106-121">Tworzenie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="f9106-121">Create virtual machine</span></span>

<span data-ttu-id="f9106-122">Utwórz maszynę wirtualną z hello [tworzenia maszyny wirtualnej az](https://docs.microsoft.com/cli/azure/vm#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="f9106-122">Create a virtual machine with hello [az vm create](https://docs.microsoft.com/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="f9106-123">Podczas tworzenia maszyny wirtualnej, takich jak obraz systemu operacyjnego, dysku zmiany rozmiaru i administracyjnych poświadczeń jest kilka opcji.</span><span class="sxs-lookup"><span data-stu-id="f9106-123">When creating a virtual machine, several options are available such as operating system image, disk sizing, and administrative credentials.</span></span> <span data-ttu-id="f9106-124">W tym przykładzie utworzono maszynę wirtualną o nazwie *myVM* systemem Ubuntu Server.</span><span class="sxs-lookup"><span data-stu-id="f9106-124">In this example, a virtual machine is created with a name of *myVM* running Ubuntu Server.</span></span> 

```azurecli-interactive 
az vm create --resource-group myResourceGroupVM --name myVM --image UbuntuLTS --generate-ssh-keys
```

<span data-ttu-id="f9106-125">Raz hello utworzenia maszyny Wirtualnej, hello Azure CLI generuje informacje o hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f9106-125">Once hello VM has been created, hello Azure CLI outputs information about hello VM.</span></span> <span data-ttu-id="f9106-126">Zwróć uwagę na powitania `publicIpAddress`, ten adres może być maszyny wirtualnej hello używane tooaccess...</span><span class="sxs-lookup"><span data-stu-id="f9106-126">Take note of hello `publicIpAddress`, this address can be used tooaccess hello virtual machine..</span></span> 

```azurecli-interactive 
{
  "fqdns": "",
  "id": "/subscriptions/d5b9d4b7-6fc1-0000-0000-000000000000/resourceGroups/myResourceGroupVM/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "52.174.34.95",
  "resourceGroup": "myResourceGroupVM"
}
```

## <a name="connect-toovm"></a><span data-ttu-id="f9106-127">Połącz tooVM</span><span class="sxs-lookup"><span data-stu-id="f9106-127">Connect tooVM</span></span>

<span data-ttu-id="f9106-128">Teraz można podłączyć toohello maszyny Wirtualnej przy użyciu protokołu SSH.</span><span class="sxs-lookup"><span data-stu-id="f9106-128">You can now connect toohello VM using SSH.</span></span> <span data-ttu-id="f9106-129">Zamień adres IP przykład hello hello `publicIpAddress` zanotowanym w poprzednim kroku hello.</span><span class="sxs-lookup"><span data-stu-id="f9106-129">Replace hello example IP address with hello `publicIpAddress` noted in hello previous step.</span></span>

```bash
ssh 52.174.34.95
```

<span data-ttu-id="f9106-130">Po zakończeniu hello maszyny Wirtualnej, należy zamknąć sesję SSH hello.</span><span class="sxs-lookup"><span data-stu-id="f9106-130">Once finished with hello VM, close hello SSH session.</span></span> 

```bash
exit
```

## <a name="understand-vm-images"></a><span data-ttu-id="f9106-131">Zrozumienie obrazów maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="f9106-131">Understand VM images</span></span>

<span data-ttu-id="f9106-132">Hello Azure marketplace zawiera wiele obrazów, które mogą być używane toocreate maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="f9106-132">hello Azure marketplace includes many images that can be used toocreate VMs.</span></span> <span data-ttu-id="f9106-133">W poprzednich krokach hello maszyna wirtualna została utworzona przy użyciu obrazu Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="f9106-133">In hello previous steps, a virtual machine was created using an Ubuntu image.</span></span> <span data-ttu-id="f9106-134">W tym kroku powitalne wiersza polecenia platformy Azure jest używane toosearch hello marketplace obrazu CentOS, który jest następnie używany toodeploy drugiej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f9106-134">In this step, hello Azure CLI is used toosearch hello marketplace for a CentOS image, which is then used toodeploy a second virtual machine.</span></span>  

<span data-ttu-id="f9106-135">toosee listę hello najczęściej używane obrazów, użyj hello [listy obrazów maszyny wirtualnej az](/cli/azure/vm/image#list) polecenia.</span><span class="sxs-lookup"><span data-stu-id="f9106-135">toosee a list of hello most commonly used images, use hello [az vm image list](/cli/azure/vm/image#list) command.</span></span>

```azurecli-interactive 
az vm image list --output table
```

<span data-ttu-id="f9106-136">dane wyjściowe polecenia Hello zwraca hello najpopularniejszych obrazów maszyn wirtualnych na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="f9106-136">hello command output returns hello most popular VM images on Azure.</span></span>

```bash
Offer          Publisher               Sku                 Urn                                                             UrnAlias             Version
-------------  ----------------------  ------------------  --------------------------------------------------------------  -------------------  ---------
WindowsServer  MicrosoftWindowsServer  2016-Datacenter     MicrosoftWindowsServer:WindowsServer:2016-Datacenter:latest     Win2016Datacenter    latest
WindowsServer  MicrosoftWindowsServer  2012-R2-Datacenter  MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest  Win2012R2Datacenter  latest
WindowsServer  MicrosoftWindowsServer  2008-R2-SP1         MicrosoftWindowsServer:WindowsServer:2008-R2-SP1:latest         Win2008R2SP1         latest
WindowsServer  MicrosoftWindowsServer  2012-Datacenter     MicrosoftWindowsServer:WindowsServer:2012-Datacenter:latest     Win2012Datacenter    latest
UbuntuServer   Canonical               16.04-LTS           Canonical:UbuntuServer:16.04-LTS:latest                         UbuntuLTS            latest
CentOS         OpenLogic               7.3                 OpenLogic:CentOS:7.3:latest                                     CentOS               latest
openSUSE-Leap  SUSE                    42.2                SUSE:openSUSE-Leap:42.2:latest                                  openSUSE-Leap        latest
RHEL           RedHat                  7.3                 RedHat:RHEL:7.3:latest                                          RHEL                 latest
SLES           SUSE                    12-SP2              SUSE:SLES:12-SP2:latest                                         SLES                 latest
Debian         credativ                8                   credativ:Debian:8:latest                                        Debian               latest
CoreOS         CoreOS                  Stable              CoreOS:CoreOS:Stable:latest                                     CoreOS               latest
```

<span data-ttu-id="f9106-137">Pełna lista, można wyświetlić, dodając hello `--all` argumentu.</span><span class="sxs-lookup"><span data-stu-id="f9106-137">A full list can be seen by adding hello `--all` argument.</span></span> <span data-ttu-id="f9106-138">listy obrazów Hello można również filtrować według `--publisher` lub `–-offer`.</span><span class="sxs-lookup"><span data-stu-id="f9106-138">hello image list can also be filtered by `--publisher` or `–-offer`.</span></span> <span data-ttu-id="f9106-139">W tym przykładzie hello lista jest przefiltrowana pod kątem wszystkich obrazów z ofertą, który pasuje *CentOS*.</span><span class="sxs-lookup"><span data-stu-id="f9106-139">In this example, hello list is filtered for all images with an offer that matches *CentOS*.</span></span> 

```azurecli-interactive 
az vm image list --offer CentOS --all --output table
```

<span data-ttu-id="f9106-140">Częściowe dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="f9106-140">Partial output:</span></span>

```azurecli-interactive 
Offer             Publisher         Sku   Urn                                     Version
----------------  ----------------  ----  --------------------------------------  -----------
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.201501         6.5.201501
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.201503         6.5.201503
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.201506         6.5.201506
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.20150904       6.5.20150904
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.20160309       6.5.20160309
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.20170207       6.5.20170207
```

<span data-ttu-id="f9106-141">toodeploy Maszynę wirtualną przy użyciu określonego obrazu, zanotuj wartość hello w hello *Urn* kolumny.</span><span class="sxs-lookup"><span data-stu-id="f9106-141">toodeploy a VM using a specific image, take note of hello value in hello *Urn* column.</span></span> <span data-ttu-id="f9106-142">Podczas określania obraz powitania, numer wersji obrazu hello można zastąpić "najnowszej", który wybiera hello najnowszą wersję hello dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="f9106-142">When specifying hello image, hello image version number can be replaced with “latest”, which selects hello latest version of hello distribution.</span></span> <span data-ttu-id="f9106-143">W tym przykładzie hello `--image` argument jest używany toospecify hello najnowszej wersji obrazu CentOS 6.5.</span><span class="sxs-lookup"><span data-stu-id="f9106-143">In this example, hello `--image` argument is used toospecify hello latest version of a CentOS 6.5 image.</span></span>  

```azurecli-interactive 
az vm create --resource-group myResourceGroupVM --name myVM2 --image OpenLogic:CentOS:6.5:latest --generate-ssh-keys
```

## <a name="understand-vm-sizes"></a><span data-ttu-id="f9106-144">Zrozumienie rozmiarów maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="f9106-144">Understand VM sizes</span></span>

<span data-ttu-id="f9106-145">Rozmiar maszyny wirtualnej określa hello zasobów obliczeniowych, takich jak Procesora GPU i pamięci wprowadzone toohello dostępne maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f9106-145">A virtual machine size determines hello amount of compute resources such as CPU, GPU, and memory that are made available toohello virtual machine.</span></span> <span data-ttu-id="f9106-146">Maszyny wirtualne muszą toobe rozmiary hello oczekiwano obciążenia pracą.</span><span class="sxs-lookup"><span data-stu-id="f9106-146">Virtual machines need toobe sized appropriately for hello expected work load.</span></span> <span data-ttu-id="f9106-147">Jeśli zwiększa obciążenie, można zmienić rozmiar istniejącej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f9106-147">If workload increases, an existing virtual machine can be resized.</span></span>

### <a name="vm-sizes"></a><span data-ttu-id="f9106-148">Rozmiary maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="f9106-148">VM Sizes</span></span>

<span data-ttu-id="f9106-149">w poniższej tabeli Hello kategoryzuje rozmiary do przypadków użycia.</span><span class="sxs-lookup"><span data-stu-id="f9106-149">hello following table categorizes sizes into use cases.</span></span>  

| <span data-ttu-id="f9106-150">Typ</span><span class="sxs-lookup"><span data-stu-id="f9106-150">Type</span></span>                     | <span data-ttu-id="f9106-151">Rozmiary</span><span class="sxs-lookup"><span data-stu-id="f9106-151">Sizes</span></span>           |    <span data-ttu-id="f9106-152">Opis</span><span class="sxs-lookup"><span data-stu-id="f9106-152">Description</span></span>       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| [<span data-ttu-id="f9106-153">Zastosowania ogólne</span><span class="sxs-lookup"><span data-stu-id="f9106-153">General purpose</span></span>](sizes-general.md)         |<span data-ttu-id="f9106-154">Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0 7</span><span class="sxs-lookup"><span data-stu-id="f9106-154">Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7</span></span>| <span data-ttu-id="f9106-155">Zrównoważonym Procesora do pamięci.</span><span class="sxs-lookup"><span data-stu-id="f9106-155">Balanced CPU-to-memory.</span></span> <span data-ttu-id="f9106-156">Nadaje się doskonale dla deweloperów / testu i małych toomedium rozwiązania aplikacji i danych.</span><span class="sxs-lookup"><span data-stu-id="f9106-156">Ideal for dev / test and small toomedium applications and data solutions.</span></span>  |
| [<span data-ttu-id="f9106-157">Optymalizacja pod kątem obliczeń</span><span class="sxs-lookup"><span data-stu-id="f9106-157">Compute optimized</span></span>](sizes-compute.md)   | <span data-ttu-id="f9106-158">FS, F</span><span class="sxs-lookup"><span data-stu-id="f9106-158">Fs, F</span></span>             | <span data-ttu-id="f9106-159">Wysoka Procesora do pamięci.</span><span class="sxs-lookup"><span data-stu-id="f9106-159">High CPU-to-memory.</span></span> <span data-ttu-id="f9106-160">Nadaje się do aplikacji średnia ruchu, urządzeń sieciowych i procesów wsadowych.</span><span class="sxs-lookup"><span data-stu-id="f9106-160">Good for medium traffic applications, network appliances, and batch processes.</span></span>        |
| [<span data-ttu-id="f9106-161">Optymalizacja pod kątem pamięci</span><span class="sxs-lookup"><span data-stu-id="f9106-161">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md)    | <span data-ttu-id="f9106-162">Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D</span><span class="sxs-lookup"><span data-stu-id="f9106-162">Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D</span></span>   | <span data-ttu-id="f9106-163">Wysoka pamięci do core.</span><span class="sxs-lookup"><span data-stu-id="f9106-163">High memory-to-core.</span></span> <span data-ttu-id="f9106-164">Doskonałe rozwiązanie dla relacyjnych baz danych, pamięci podręcznych średnia toolarge i analiza w pamięci.</span><span class="sxs-lookup"><span data-stu-id="f9106-164">Great for relational databases, medium toolarge caches, and in-memory analytics.</span></span>                 |
| [<span data-ttu-id="f9106-165">Optymalizacja pod kątem magazynu</span><span class="sxs-lookup"><span data-stu-id="f9106-165">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md)      | <span data-ttu-id="f9106-166">Ls</span><span class="sxs-lookup"><span data-stu-id="f9106-166">Ls</span></span>                | <span data-ttu-id="f9106-167">Wysoka przepływność dysku i operacje we/wy.</span><span class="sxs-lookup"><span data-stu-id="f9106-167">High disk throughput and IO.</span></span> <span data-ttu-id="f9106-168">Idealne rozwiązanie w przypadku danych big data oraz baz danych SQL i NoSQL.</span><span class="sxs-lookup"><span data-stu-id="f9106-168">Ideal for Big Data, SQL, and NoSQL databases.</span></span>                                                         |
| [<span data-ttu-id="f9106-169">Procesor GPU</span><span class="sxs-lookup"><span data-stu-id="f9106-169">GPU</span></span>](sizes-gpu.md)          | <span data-ttu-id="f9106-170">WIRTUALIZACJĄ SIECI, NC</span><span class="sxs-lookup"><span data-stu-id="f9106-170">NV, NC</span></span>            | <span data-ttu-id="f9106-171">Celem duże Renderowanie grafiki i wideo edycji specjalne maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="f9106-171">Specialized VMs targeted for heavy graphic rendering and video editing.</span></span>       |
| [<span data-ttu-id="f9106-172">Wysoka wydajność</span><span class="sxs-lookup"><span data-stu-id="f9106-172">High performance</span></span>](sizes-hpc.md) | <span data-ttu-id="f9106-173">H-A8 11</span><span class="sxs-lookup"><span data-stu-id="f9106-173">H, A8-11</span></span>          | <span data-ttu-id="f9106-174">Nasze najbardziej zaawansowanych Procesora maszyny wirtualne z interfejsami opcjonalne wysokiej przepustowości sieci (RDMA).</span><span class="sxs-lookup"><span data-stu-id="f9106-174">Our most powerful CPU VMs with optional high-throughput network interfaces (RDMA).</span></span> 


### <a name="find-available-vm-sizes"></a><span data-ttu-id="f9106-175">Znajdowanie dostępnych rozmiarów maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="f9106-175">Find available VM sizes</span></span>

<span data-ttu-id="f9106-176">toosee listę maszyn wirtualnych rozmiarów dostępnych w określonym regionie, użyj hello [listy rozmiarów maszyn wirtualnych az](/cli/azure/vm#list-sizes) polecenia.</span><span class="sxs-lookup"><span data-stu-id="f9106-176">toosee a list of VM sizes available in a particular region, use hello [az vm list-sizes](/cli/azure/vm#list-sizes) command.</span></span> 

```azurecli-interactive 
az vm list-sizes --location eastus --output table
```

<span data-ttu-id="f9106-177">Częściowe dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="f9106-177">Partial output:</span></span>

```azurecli-interactive 
  MaxDataDiskCount    MemoryInMb  Name                      NumberOfCores    OsDiskSizeInMb    ResourceDiskSizeInMb
------------------  ------------  ----------------------  ---------------  ----------------  ----------------------
                 2          3584  Standard_DS1                          1           1047552                    7168
                 4          7168  Standard_DS2                          2           1047552                   14336
                 8         14336  Standard_DS3                          4           1047552                   28672
                16         28672  Standard_DS4                          8           1047552                   57344
                 4         14336  Standard_DS11                         2           1047552                   28672
                 8         28672  Standard_DS12                         4           1047552                   57344
                16         57344  Standard_DS13                         8           1047552                  114688
                32        114688  Standard_DS14                        16           1047552                  229376
                 1           768  Standard_A0                           1           1047552                   20480
                 2          1792  Standard_A1                           1           1047552                   71680
                 4          3584  Standard_A2                           2           1047552                  138240
                 8          7168  Standard_A3                           4           1047552                  291840
                 4         14336  Standard_A5                           2           1047552                  138240
                16         14336  Standard_A4                           8           1047552                  619520
                 8         28672  Standard_A6                           4           1047552                  291840
                16         57344  Standard_A7                           8           1047552                  619520
```

### <a name="create-vm-with-specific-size"></a><span data-ttu-id="f9106-178">Tworzenie maszyny Wirtualnej o określonym rozmiarze</span><span class="sxs-lookup"><span data-stu-id="f9106-178">Create VM with specific size</span></span>

<span data-ttu-id="f9106-179">Witaj poprzedniego przykładu tworzenia maszyny Wirtualnej o rozmiarze nie podano, której wynikiem jest domyślny rozmiar.</span><span class="sxs-lookup"><span data-stu-id="f9106-179">In hello previous VM creation example, a size was not provided, which results in a default size.</span></span> <span data-ttu-id="f9106-180">Można wybrać rozmiar maszyny Wirtualnej za pomocą czasu tworzenia [tworzenia maszyny wirtualnej az](/cli/azure/vm#create) i hello `--size` argumentu.</span><span class="sxs-lookup"><span data-stu-id="f9106-180">A VM size can be selected at creation time using [az vm create](/cli/azure/vm#create) and hello `--size` argument.</span></span> 

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroupVM \
    --name myVM3 \
    --image UbuntuLTS \
    --size Standard_F4s \
    --generate-ssh-keys
```

### <a name="resize-a-vm"></a><span data-ttu-id="f9106-181">Zmienianie rozmiaru maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="f9106-181">Resize a VM</span></span>

<span data-ttu-id="f9106-182">Po wdrożeniu maszyny Wirtualnej można tooincrease po zmianie rozmiaru lub zmniejszenia alokacji zasobów.</span><span class="sxs-lookup"><span data-stu-id="f9106-182">After a VM has been deployed, it can be resized tooincrease or decrease resource allocation.</span></span>

<span data-ttu-id="f9106-183">Przed zmianą rozmiaru maszyny Wirtualnej, sprawdź, czy hello wymagany rozmiar w klastrze jest dostępny hello bieżącej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f9106-183">Before resizing a VM, check if hello desired size is available on hello current Azure cluster.</span></span> <span data-ttu-id="f9106-184">Witaj [az maszyny wirtualnej-vm — zmiany rozmiaru — opcje listy](/cli/azure/vm#list-vm-resize-options) polecenie zwraca hello listę rozmiarów.</span><span class="sxs-lookup"><span data-stu-id="f9106-184">hello [az vm list-vm-resize-options](/cli/azure/vm#list-vm-resize-options) command returns hello list of sizes.</span></span> 

```azurecli-interactive 
az vm list-vm-resize-options --resource-group myResourceGroupVM --name myVM --query [].name
```
<span data-ttu-id="f9106-185">W razie potrzeby hello się, że rozmiar jest dostępny hello maszyny Wirtualnej można zmienić rozmiar ze stanu zasilania na, jednak podczas hello operacji ponownego rozruchu.</span><span class="sxs-lookup"><span data-stu-id="f9106-185">If hello desired size is available, hello VM can be resized from a powered-on state, however it is rebooted during hello operation.</span></span> <span data-ttu-id="f9106-186">Użyj hello [Zmień rozmiar maszyny wirtualnej az]( /cli/azure/vm#resize) zmiany rozmiaru hello tooperform polecenia.</span><span class="sxs-lookup"><span data-stu-id="f9106-186">Use hello [az vm resize]( /cli/azure/vm#resize) command tooperform hello resize.</span></span>

```azurecli-interactive 
az vm resize --resource-group myResourceGroupVM --name myVM --size Standard_DS4_v2
```

<span data-ttu-id="f9106-187">Jeśli hello żądany rozmiar nie jest na powitania bieżący klaster hello wirtualna potrzeb, może wystąpić toobe alokację przed hello operacja zmiany rozmiaru.</span><span class="sxs-lookup"><span data-stu-id="f9106-187">If hello desired size is not on hello current cluster, hello VM needs toobe deallocated before hello resize operation can occur.</span></span> <span data-ttu-id="f9106-188">Użyj hello [deallocate wirtualna az]( /cli/azure/vm#deallocate) polecenia toostop i cofnięcia przydzielenia hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f9106-188">Use hello [az vm deallocate]( /cli/azure/vm#deallocate) command toostop and deallocate hello VM.</span></span> <span data-ttu-id="f9106-189">Uwaga: w przypadku hello maszyny Wirtualnej jest włączona ponownie, wszystkie dane na dysku tymczasowym hello mogą zostać usunięte.</span><span class="sxs-lookup"><span data-stu-id="f9106-189">Note, when hello VM is powered back on, any data on hello temp disk may be removed.</span></span> <span data-ttu-id="f9106-190">Hello publiczny adres IP także zmianę, chyba że używana jest statyczny adres IP.</span><span class="sxs-lookup"><span data-stu-id="f9106-190">hello public IP address also changes unless a static IP address is being used.</span></span> 

```azurecli-interactive 
az vm deallocate --resource-group myResourceGroupVM --name myVM
```

<span data-ttu-id="f9106-191">Po cofnięciu przydziału, może wystąpić hello zmiany rozmiaru.</span><span class="sxs-lookup"><span data-stu-id="f9106-191">Once deallocated, hello resize can occur.</span></span> 

```azurecli-interactive 
az vm resize --resource-group myResourceGroupVM --name myVM --size Standard_GS1
```

<span data-ttu-id="f9106-192">Po hello rozmiaru, można uruchomić hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f9106-192">After hello resize, hello VM can be started.</span></span>

```azurecli-interactive 
az vm start --resource-group myResourceGroupVM --name myVM
```

## <a name="vm-power-states"></a><span data-ttu-id="f9106-193">Stany zasilania maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="f9106-193">VM power states</span></span>

<span data-ttu-id="f9106-194">Maszyny Wirtualnej platformy Azure może mieć jedną z wielu stany zasilania.</span><span class="sxs-lookup"><span data-stu-id="f9106-194">An Azure VM can have one of many power states.</span></span> <span data-ttu-id="f9106-195">Ten stan reprezentuje hello bieżący stan hello maszyny Wirtualnej z punktu widzenia hello hello funkcji hypervisor.</span><span class="sxs-lookup"><span data-stu-id="f9106-195">This state represents hello current state of hello VM from hello standpoint of hello hypervisor.</span></span> 

### <a name="power-states"></a><span data-ttu-id="f9106-196">Stany zasilania</span><span class="sxs-lookup"><span data-stu-id="f9106-196">Power states</span></span>

| <span data-ttu-id="f9106-197">Stan zasilania</span><span class="sxs-lookup"><span data-stu-id="f9106-197">Power State</span></span> | <span data-ttu-id="f9106-198">Opis</span><span class="sxs-lookup"><span data-stu-id="f9106-198">Description</span></span>
|----|----|
| <span data-ttu-id="f9106-199">Uruchamianie</span><span class="sxs-lookup"><span data-stu-id="f9106-199">Starting</span></span> | <span data-ttu-id="f9106-200">Wskazuje, że jest uruchamiana hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f9106-200">Indicates hello virtual machine is being started.</span></span> |
| <span data-ttu-id="f9106-201">Działanie</span><span class="sxs-lookup"><span data-stu-id="f9106-201">Running</span></span> | <span data-ttu-id="f9106-202">Wskazuje, że działa hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f9106-202">Indicates that hello virtual machine is running.</span></span> |
| <span data-ttu-id="f9106-203">Zatrzymywanie</span><span class="sxs-lookup"><span data-stu-id="f9106-203">Stopping</span></span> | <span data-ttu-id="f9106-204">Wskazuje, że tej maszyny wirtualnej hello jest zatrzymywana.</span><span class="sxs-lookup"><span data-stu-id="f9106-204">Indicates that hello virtual machine is being stopped.</span></span> | 
| <span data-ttu-id="f9106-205">Zatrzymane</span><span class="sxs-lookup"><span data-stu-id="f9106-205">Stopped</span></span> | <span data-ttu-id="f9106-206">Wskazuje, że tej maszyny wirtualnej hello jest zatrzymana.</span><span class="sxs-lookup"><span data-stu-id="f9106-206">Indicates that hello virtual machine is stopped.</span></span> <span data-ttu-id="f9106-207">Maszyny wirtualne w stanie hello zatrzymana nadal naliczenie opłat za obliczenia.</span><span class="sxs-lookup"><span data-stu-id="f9106-207">Virtual machines in hello stopped state still incur compute charges.</span></span>  |
| <span data-ttu-id="f9106-208">Cofanie przydziału</span><span class="sxs-lookup"><span data-stu-id="f9106-208">Deallocating</span></span> | <span data-ttu-id="f9106-209">Wskazuje, że cofana jest hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f9106-209">Indicates that hello virtual machine is being deallocated.</span></span> |
| <span data-ttu-id="f9106-210">Cofnięcie przydziału</span><span class="sxs-lookup"><span data-stu-id="f9106-210">Deallocated</span></span> | <span data-ttu-id="f9106-211">Oznacza, że hello maszyny wirtualnej zostanie usunięty z hello funkcji hypervisor, ale nadal dostępne w płaszczyźnie kontroli hello.</span><span class="sxs-lookup"><span data-stu-id="f9106-211">Indicates that hello virtual machine is removed from hello hypervisor but still available in hello control plane.</span></span> <span data-ttu-id="f9106-212">Maszyny wirtualne w stanie Deallocated hello nie naliczenie opłat za obliczenia.</span><span class="sxs-lookup"><span data-stu-id="f9106-212">Virtual machines in hello Deallocated state do not incur compute charges.</span></span> |
| - | <span data-ttu-id="f9106-213">Wskazuje, że stan zasilania hello hello maszyny wirtualnej jest nieznany.</span><span class="sxs-lookup"><span data-stu-id="f9106-213">Indicates that hello power state of hello virtual machine is unknown.</span></span> |

### <a name="find-power-state"></a><span data-ttu-id="f9106-214">Znajdź stan zasilania</span><span class="sxs-lookup"><span data-stu-id="f9106-214">Find power state</span></span>

<span data-ttu-id="f9106-215">Stan hello tooretrieve określonej maszyny wirtualnej, użyj hello [wirtualna az Pobierz widok wystąpienia](/cli/azure/vm#get-instance-view) polecenia.</span><span class="sxs-lookup"><span data-stu-id="f9106-215">tooretrieve hello state of a particular VM, use hello [az vm get instance-view](/cli/azure/vm#get-instance-view) command.</span></span> <span data-ttu-id="f9106-216">Należy się toospecify poprawną nazwę maszyny wirtualnej i grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="f9106-216">Be sure toospecify a valid name for a virtual machine and resource group.</span></span> 

```azurecli-interactive 
az vm get-instance-view \
    --name myVM \
    --resource-group myResourceGroupVM \
    --query instanceView.statuses[1] --output table
```

<span data-ttu-id="f9106-217">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="f9106-217">Output:</span></span>

```azurecli-interactive 
ode                DisplayStatus    Level
------------------  ---------------  -------
PowerState/running  VM running       Info
```

## <a name="management-tasks"></a><span data-ttu-id="f9106-218">Zadania zarządzania</span><span class="sxs-lookup"><span data-stu-id="f9106-218">Management tasks</span></span>

<span data-ttu-id="f9106-219">Podczas hello cyklu maszyny wirtualnej może być toorun zadań zarządzania, takich jak uruchamianie, zatrzymywanie lub usuwanie maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f9106-219">During hello life-cycle of a virtual machine, you may want toorun management tasks such as starting, stopping, or deleting a virtual machine.</span></span> <span data-ttu-id="f9106-220">Ponadto można toocreate skrypty tooautomate powtarzających się lub złożonych zadań.</span><span class="sxs-lookup"><span data-stu-id="f9106-220">Additionally, you may want toocreate scripts tooautomate repetitive or complex tasks.</span></span> <span data-ttu-id="f9106-221">Przy użyciu hello Azure CLI, wiele typowych zadań zarządzania można uruchomić z wiersza polecenia hello lub w skryptach.</span><span class="sxs-lookup"><span data-stu-id="f9106-221">Using hello Azure CLI, many common management tasks can be run from hello command line or in scripts.</span></span> 

### <a name="get-ip-address"></a><span data-ttu-id="f9106-222">Pobierz adres IP</span><span class="sxs-lookup"><span data-stu-id="f9106-222">Get IP address</span></span>

<span data-ttu-id="f9106-223">To polecenie zwraca hello prywatnych i publicznych adresów IP maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f9106-223">This command returns hello private and public IP addresses of a virtual machine.</span></span>  

```azurecli-interactive 
az vm list-ip-addresses --resource-group myResourceGroupVM --name myVM --output table
```

### <a name="stop-virtual-machine"></a><span data-ttu-id="f9106-224">Zatrzymaj maszynę wirtualną</span><span class="sxs-lookup"><span data-stu-id="f9106-224">Stop virtual machine</span></span>

```azurecli-interactive 
az vm stop --resource-group myResourceGroupVM --name myVM
```

### <a name="start-virtual-machine"></a><span data-ttu-id="f9106-225">Uruchom maszynę wirtualną</span><span class="sxs-lookup"><span data-stu-id="f9106-225">Start virtual machine</span></span>

```azurecli-interactive 
az vm start --resource-group myResourceGroupVM --name myVM
```

### <a name="delete-resource-group"></a><span data-ttu-id="f9106-226">Usuń grupę zasobów</span><span class="sxs-lookup"><span data-stu-id="f9106-226">Delete resource group</span></span>

<span data-ttu-id="f9106-227">Usunięcie grupy zasobów powoduje usunięcie wszystkie zasoby zawarte w ciągu.</span><span class="sxs-lookup"><span data-stu-id="f9106-227">Deleting a resource group also deletes all resources contained within.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroupVM --no-wait --yes
```

## <a name="next-steps"></a><span data-ttu-id="f9106-228">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f9106-228">Next steps</span></span>

<span data-ttu-id="f9106-229">W tym samouczku poznanie podstawowych tworzenia maszyny Wirtualnej i zarządzania, np.:</span><span class="sxs-lookup"><span data-stu-id="f9106-229">In this tutorial, you learned about basic VM creation and management such as how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f9106-230">Tworzenie i łączenie tooa maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="f9106-230">Create and connect tooa VM</span></span>
> * <span data-ttu-id="f9106-231">Wybierz i używać obrazów maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="f9106-231">Select and use VM images</span></span>
> * <span data-ttu-id="f9106-232">Wyświetlanie i używanie określonych rozmiarów maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="f9106-232">View and use specific VM sizes</span></span>
> * <span data-ttu-id="f9106-233">Zmienianie rozmiaru maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="f9106-233">Resize a VM</span></span>
> * <span data-ttu-id="f9106-234">Wyświetlanie i zrozumienie stanu maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="f9106-234">View and understand VM state</span></span>

<span data-ttu-id="f9106-235">Przejdź dalej toolearn samouczka toohello dysków maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f9106-235">Advance toohello next tutorial toolearn about VM disks.</span></span>  

> [!div class="nextstepaction"]
> [<span data-ttu-id="f9106-236">Utwórz i Zarządzaj maszyny Wirtualnej dyski</span><span class="sxs-lookup"><span data-stu-id="f9106-236">Create and Manage VM disks</span></span>](./tutorial-manage-disks.md)
