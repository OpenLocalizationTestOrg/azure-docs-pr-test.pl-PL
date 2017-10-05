---
title: "Przechwytywanie maszyny Wirtualnej systemu Linux platformy Azure do użycia jako szablon | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie przechwytywania i obraz opartych na systemie Linux Azure maszynę wirtualną (VM) utworzone za pomocą modelu wdrażania usługi Azure Resource Manager."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: e608116f-f478-41be-b787-c2ad91b5a802
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: b1164fbd816eea5189786850f096438e32f8f802
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="capture-a-linux-virtual-machine-running-on-azure"></a><span data-ttu-id="898b0-103">Przechwytywanie maszyny wirtualnej systemu Linux działających na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="898b0-103">Capture a Linux virtual machine running on Azure</span></span>
<span data-ttu-id="898b0-104">Wykonaj kroki opisane w tym artykule, aby Uogólnij i Przechwyć maszyny wirtualnej systemu Linux platformy Azure (VM) w modelu wdrażania Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="898b0-104">Follow the steps in this article to generalize and capture your Azure Linux virtual machine (VM) in the Resource Manager deployment model.</span></span> <span data-ttu-id="898b0-105">Uogólnienie maszynę Wirtualną, Usuń konto osobiste informacje i przygotowanie wirtualna do użycia jako obraz.</span><span class="sxs-lookup"><span data-stu-id="898b0-105">When you generalize the VM, you remove personal account information and prepare the VM to be used as an image.</span></span> <span data-ttu-id="898b0-106">Można następnie przechwytywania obrazu uogólniony wirtualny dysk twardy (VHD) dla systemu operacyjnego, dysków VHD dla dysków dołączonych danych i [szablonu usługi Resource Manager](../../azure-resource-manager/resource-group-overview.md) o nowych wdrożeniach maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="898b0-106">You then capture a generalized virtual hard disk (VHD) image for the OS, VHDs for attached data disks, and a [Resource Manager template](../../azure-resource-manager/resource-group-overview.md) for new VM deployments.</span></span> <span data-ttu-id="898b0-107">Ten artykuł zawiera szczegóły dotyczące sposobu przechwytywania obrazu maszyny Wirtualnej z interfejsu wiersza polecenia platformy Azure w wersji 1.0 za pomocą niezarządzanych dysków maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="898b0-107">This article details how to capture a VM image with the Azure CLI 1.0 for a VM using unmanaged disks.</span></span> <span data-ttu-id="898b0-108">Możesz również [Przechwytywanie maszyny Wirtualnej za pomocą dysków zarządzanych Azure 2.0 interfejsu wiersza polecenia Azure](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="898b0-108">You can also [capture a VM using Azure Managed Disks with the Azure CLI 2.0](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="898b0-109">Dyski zarządzane są obsługiwane przez platformę Azure i nie wymagają wszystkie lub lokalizację do przechowywania ich.</span><span class="sxs-lookup"><span data-stu-id="898b0-109">Managed disks are handled by the Azure platform and do not require any preparation or location to store them.</span></span> <span data-ttu-id="898b0-110">Aby uzyskać więcej informacji, zobacz temat [Omówienie usługi Azure Managed Disks](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="898b0-110">For more information, see [Azure Managed Disks overview](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 

<span data-ttu-id="898b0-111">Do tworzenia maszyn wirtualnych przy użyciu obrazu, konfigurowanie zasobów sieciowych dla każdej nowej maszyny Wirtualnej, a następnie wdrożyć go z przechwyconych obrazów wirtualnego dysku twardego przy użyciu szablonu (plik JavaScript Object Notation lub formatu JSON,).</span><span class="sxs-lookup"><span data-stu-id="898b0-111">To create VMs using the image, set up network resources for each new VM, and use the template (a JavaScript Object Notation, or JSON, file) to deploy it from the captured VHD images.</span></span> <span data-ttu-id="898b0-112">W ten sposób można replikować maszyny Wirtualnej z bieżącej konfiguracji oprogramowania, podobnie jak używać obrazów w portalu Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="898b0-112">In this way, you can replicate a VM with its current software configuration, similar to the way you use images in the Azure Marketplace.</span></span>

> [!TIP]
> <span data-ttu-id="898b0-113">Jeśli chcesz utworzyć kopię istniejącej maszyny Wirtualnej systemu Linux jej stanem specjalne tworzenia kopii zapasowej i debugowania, zobacz [utworzenie kopii maszyny wirtualnej systemu Linux działających na platformie Azure](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="898b0-113">If you want to create a copy of your existing Linux VM with its specialized state for backup or debugging, see [Create a copy of a Linux virtual machine running on Azure](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="898b0-114">A jeśli chcesz przekazać wirtualnego dysku twardego z lokalnej maszyny Wirtualnej systemu Linux, zobacz [przekazywanie i Utwórz Maszynę wirtualną systemu Linux na podstawie obrazu niestandardowego dysku](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="898b0-114">And if you want to upload a Linux VHD from an on-premises VM, see [Upload and create a Linux VM from custom disk image](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>  

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="898b0-115">Wersje interfejsu wiersza polecenia umożliwiające wykonanie zadania</span><span class="sxs-lookup"><span data-stu-id="898b0-115">CLI versions to complete the task</span></span>
<span data-ttu-id="898b0-116">Zadanie można wykonać przy użyciu jednej z następujących wersji interfejsu wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="898b0-116">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="898b0-117">[Azure CLI 1.0](#before-you-begin) — nasze interfejsu wiersza polecenia dla klasycznego i zasobów zarządzania wdrażania modeli (w tym artykule)</span><span class="sxs-lookup"><span data-stu-id="898b0-117">[Azure CLI 1.0](#before-you-begin) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="898b0-118">[Interfejs wiersza polecenia platformy Azure w wersji 2.0](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) — nasz interfejs wiersza polecenia nowej generacji dla modelu wdrażania na potrzeby zarządzania zasobami</span><span class="sxs-lookup"><span data-stu-id="898b0-118">[Azure CLI 2.0](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="898b0-119">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="898b0-119">Before you begin</span></span>
<span data-ttu-id="898b0-120">Upewnij się, że zostały spełnione następujące wymagania wstępne:</span><span class="sxs-lookup"><span data-stu-id="898b0-120">Ensure that you meet the following prerequisites:</span></span>

* <span data-ttu-id="898b0-121">**Maszyna wirtualna platformy Azure utworzonych w modelu wdrażania usługi Resource Manager** — Jeśli nie utworzono Maszynę wirtualną systemu Linux, możesz użyć [portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), [interfejsu wiersza polecenia Azure](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), lub [szablony Menedżera zasobów](create-ssh-secured-vm-from-template.md).</span><span class="sxs-lookup"><span data-stu-id="898b0-121">**Azure VM created in the Resource Manager deployment model** - If you haven't created a Linux VM, you can use the [portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), the [Azure CLI](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), or [Resource Manager templates](create-ssh-secured-vm-from-template.md).</span></span> 
  
    <span data-ttu-id="898b0-122">Konfigurowanie maszyny Wirtualnej, zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="898b0-122">Configure the VM as needed.</span></span> <span data-ttu-id="898b0-123">Na przykład [Dodaj dyski danych](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), stosowania aktualizacji i zainstalować aplikacje.</span><span class="sxs-lookup"><span data-stu-id="898b0-123">For example, [add data disks](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), apply updates, and install applications.</span></span> 
* <span data-ttu-id="898b0-124">**Azure CLI** -Zainstaluj [interfejsu wiersza polecenia Azure](../../cli-install-nodejs.md) na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="898b0-124">**Azure CLI** - Install the [Azure CLI](../../cli-install-nodejs.md) on a local computer.</span></span>

## <a name="step-1-remove-the-azure-linux-agent"></a><span data-ttu-id="898b0-125">Krok 1: Usuń agenta systemu Linux platformy Azure</span><span class="sxs-lookup"><span data-stu-id="898b0-125">Step 1: Remove the Azure Linux agent</span></span>
<span data-ttu-id="898b0-126">Najpierw uruchom **agenta waagent** z **deprovision** parametru na Maszynie wirtualnej systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="898b0-126">First, run the **waagent** command with the **deprovision** parameter on the Linux VM.</span></span> <span data-ttu-id="898b0-127">To polecenie usuwa pliki i dane w celu przygotowania do uogólnianie maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="898b0-127">This command deletes files and data to make the VM ready for generalizing.</span></span> <span data-ttu-id="898b0-128">Aby uzyskać więcej informacji, zobacz [Podręcznik użytkownika agenta systemu Linux Azure](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="898b0-128">For details, see the [Azure Linux Agent user guide](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

1. <span data-ttu-id="898b0-129">Podłącz do sieci maszyny Wirtualnej systemu Linux przy użyciu klienta SSH.</span><span class="sxs-lookup"><span data-stu-id="898b0-129">Connect to your Linux VM using an SSH client.</span></span>
2. <span data-ttu-id="898b0-130">W oknie SSH wpisz następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="898b0-130">In the SSH window, type the following command:</span></span>
   
    ```bash
    sudo waagent -deprovision+user
    ```
   > [!NOTE]
   > <span data-ttu-id="898b0-131">To polecenie można uruchamiać tylko na maszynie Wirtualnej, który ma zostać przechwytywanie w formie obrazu.</span><span class="sxs-lookup"><span data-stu-id="898b0-131">Only run this command on a VM that you intend to capture as an image.</span></span> <span data-ttu-id="898b0-132">Nie gwarantuje, że obraz jest wyczyszczone wszystkie informacje poufne lub nadaje się do ponownej dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="898b0-132">It does not guarantee that the image is cleared of all sensitive information or is suitable for redistribution.</span></span>
 
3. <span data-ttu-id="898b0-133">Typ **y** aby kontynuować.</span><span class="sxs-lookup"><span data-stu-id="898b0-133">Type **y** to continue.</span></span> <span data-ttu-id="898b0-134">Możesz dodać **-force** parametr, aby uniknąć tego kroku potwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="898b0-134">You can add the **-force** parameter to avoid this confirmation step.</span></span>
4. <span data-ttu-id="898b0-135">Po zakończeniu wykonywania polecenia, wpisz **zakończyć**.</span><span class="sxs-lookup"><span data-stu-id="898b0-135">After the command completes, type **exit**.</span></span> <span data-ttu-id="898b0-136">Ten krok powoduje zamknięcie klienta SSH.</span><span class="sxs-lookup"><span data-stu-id="898b0-136">This step closes the SSH client.</span></span>

## <a name="step-2-capture-the-vm"></a><span data-ttu-id="898b0-137">Krok 2: Przechwytywanie maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="898b0-137">Step 2: Capture the VM</span></span>
<span data-ttu-id="898b0-138">Użyj interfejsu wiersza polecenia Azure, aby Uogólnij i Przechwyć maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="898b0-138">Use the Azure CLI to generalize and capture the VM.</span></span> <span data-ttu-id="898b0-139">W poniższych przykładach Zastąp przykładowe nazwy parametrów własne wartości.</span><span class="sxs-lookup"><span data-stu-id="898b0-139">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="898b0-140">Przykład nazwy parametru zawierają **myResourceGroup**, **myVnet**, i **myVM**.</span><span class="sxs-lookup"><span data-stu-id="898b0-140">Example parameter names include **myResourceGroup**, **myVnet**, and **myVM**.</span></span>

1. <span data-ttu-id="898b0-141">Na komputerze lokalnym, Otwórz wiersza polecenia platformy Azure i [logowania do subskrypcji platformy Azure](../../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="898b0-141">From your local computer, open the Azure CLI and [login to your Azure subscription](../../xplat-cli-connect.md).</span></span> 
2. <span data-ttu-id="898b0-142">Upewnij się, że jesteś w trybie Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="898b0-142">Make sure you are in Resource Manager mode.</span></span>
   
    ```azurecli
    azure config mode arm
    ```
3. <span data-ttu-id="898b0-143">Zamknij maszynę Wirtualną, która już anulowana za pomocą następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="898b0-143">Shut down the VM that you already deprovisioned by using the following command:</span></span>
   
    ```azurecli
    azure vm deallocate -g myResourceGroup -n myVM
    ```
4. <span data-ttu-id="898b0-144">Generalize maszyny Wirtualnej za pomocą następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="898b0-144">Generalize the VM with the following command:</span></span>
   
    ```azurecli
    azure vm generalize -g myResourceGroup -n myVM
    ```
5. <span data-ttu-id="898b0-145">Teraz uruchom **przechwytywania maszyna wirtualna platformy azure** polecenia, które znajdują się maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="898b0-145">Now run the **azure vm capture** command, which captures the VM.</span></span> <span data-ttu-id="898b0-146">W poniższym przykładzie obrazu wirtualne dyski twarde są przechwytywane z nazwy, począwszy od **MyVHDNamePrefix**i **-t** opcja określa ścieżkę do szablonu **MyTemplate.json**.</span><span class="sxs-lookup"><span data-stu-id="898b0-146">In the following example, the image VHDs are captured with names beginning with **MyVHDNamePrefix**, and the **-t** option specifies a path to the template **MyTemplate.json**.</span></span> 
   
    ```azurecli
    azure vm capture -g myResourceGroup -n myVM -p myVHDNamePrefix -t myTemplate.json
    ```
   
   > [!IMPORTANT]
   > <span data-ttu-id="898b0-147">Pliki VHD obrazu tworzone domyślnie na tym samym koncie magazynu, która używana oryginalna maszyna wirtualna.</span><span class="sxs-lookup"><span data-stu-id="898b0-147">The image VHD files get created by default in the same storage account that the original VM used.</span></span> <span data-ttu-id="898b0-148">Użyj *tego samego konta magazynu* do przechowywania dysków VHD dla wszelkie nowe maszyny wirtualne utworzysz z obrazu.</span><span class="sxs-lookup"><span data-stu-id="898b0-148">Use the *same storage account* to store the VHDs for any new VMs you create from the image.</span></span> 

6. <span data-ttu-id="898b0-149">Aby znaleźć lokalizację przechwycony obraz, otwórz szablon JSON w edytorze tekstów.</span><span class="sxs-lookup"><span data-stu-id="898b0-149">To find the location of a captured image, open the JSON template in a text editor.</span></span> <span data-ttu-id="898b0-150">W **storageProfile**, Znajdź **uri** z **obrazu** znajduje się w **systemu** kontenera.</span><span class="sxs-lookup"><span data-stu-id="898b0-150">In the **storageProfile**, find the **uri** of the **image** located in the **system** container.</span></span> <span data-ttu-id="898b0-151">Na przykład jest podobny do identyfikatora URI obrazu dysku systemu operacyjnego`https://xxxxxxxxxxxxxx.blob.core.windows.net/system/Microsoft.Compute/Images/vhds/MyVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`</span><span class="sxs-lookup"><span data-stu-id="898b0-151">For example, the URI of the OS disk image is similar to `https://xxxxxxxxxxxxxx.blob.core.windows.net/system/Microsoft.Compute/Images/vhds/MyVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`</span></span>

## <a name="step-3-create-a-vm-from-the-captured-image"></a><span data-ttu-id="898b0-152">Krok 3: Tworzenie maszyny Wirtualnej z przechwyconego obrazu</span><span class="sxs-lookup"><span data-stu-id="898b0-152">Step 3: Create a VM from the captured image</span></span>
<span data-ttu-id="898b0-153">Teraz należy użyć obrazu przy użyciu szablonu, aby utworzyć Maszynę wirtualną systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="898b0-153">Now use the image with a template to create a Linux VM.</span></span> <span data-ttu-id="898b0-154">Te kroki pokazują, jak użyć wiersza polecenia platformy Azure i szablon pliku JSON, przechwyconych w celu utworzenia maszyny Wirtualnej w nowej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="898b0-154">These steps show you how to use the Azure CLI and the JSON file template you captured to create the VM in a new virtual network.</span></span>

### <a name="create-network-resources"></a><span data-ttu-id="898b0-155">Utwórz zasoby sieciowe</span><span class="sxs-lookup"><span data-stu-id="898b0-155">Create network resources</span></span>
<span data-ttu-id="898b0-156">Aby użyć szablonu, należy najpierw skonfigurować sieć wirtualną i karty Sieciowej dla nowej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="898b0-156">To use the template, you first need to set up a virtual network and NIC for your new VM.</span></span> <span data-ttu-id="898b0-157">Zaleca się tworzenie grupy zasobów dla tych zasobów w lokalizacji przechowywania obrazu maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="898b0-157">We recommend you create a resource group for these resources in the location where your VM image is stored.</span></span> <span data-ttu-id="898b0-158">Uruchom polecenia podobne do następujących, zastępując nazwy zasobów i odpowiednie lokalizacji platformy Azure ("centralus" w tych poleceniach):</span><span class="sxs-lookup"><span data-stu-id="898b0-158">Run commands similar to the following, substituting names for your resources and an appropriate Azure location ("centralus" in these commands):</span></span>

```azurecli
azure group create myResourceGroup1 -l "centralus"

azure network vnet create myResourceGroup1 myVnet -l "centralus"

azure network vnet subnet create myResourceGroup1 myVnet mySubnet

azure network public-ip create myResourceGroup1 myPublicIP -l "centralus"

azure network nic create myResourceGroup1 myNIC -k mySubnet -m myVnet -p myPublicIP -l "centralus"
```

### <a name="get-the-id-of-the-nic"></a><span data-ttu-id="898b0-159">Pobierz identyfikator karty Sieciowej</span><span class="sxs-lookup"><span data-stu-id="898b0-159">Get the Id of the NIC</span></span>
<span data-ttu-id="898b0-160">Aby wdrożyć Maszynę wirtualną z obrazu przy użyciu JSON zapisane podczas przechwytywania, potrzebny jest identyfikator karty sieciowej.</span><span class="sxs-lookup"><span data-stu-id="898b0-160">To deploy a VM from the image by using the JSON you saved during capture, you need the Id of the NIC.</span></span> <span data-ttu-id="898b0-161">Go uzyskać, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="898b0-161">Obtain it by running the following command:</span></span>

```azurecli
azure network nic show myResourceGroup1 myNIC
```

<span data-ttu-id="898b0-162">**Identyfikator** w danych wyjściowych jest podobny do`/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/MyResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic`</span><span class="sxs-lookup"><span data-stu-id="898b0-162">The **Id** in the output is similar to `/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/MyResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic`</span></span>

### <a name="create-a-vm"></a><span data-ttu-id="898b0-163">Tworzenie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="898b0-163">Create a VM</span></span>
<span data-ttu-id="898b0-164">Teraz uruchom następujące polecenie w celu utworzenia maszyny Wirtualnej z przechwyconego obrazu maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="898b0-164">Now run the following command to create your VM from the captured VM image.</span></span> <span data-ttu-id="898b0-165">Użyj **-f** parametr, aby określić ścieżkę do pliku JSON szablonu został zapisany.</span><span class="sxs-lookup"><span data-stu-id="898b0-165">Use the **-f** parameter to specify the path to the template JSON file you saved.</span></span>

```azurecli
azure group deployment create myResourceGroup1 MyDeployment -f MyTemplate.json
```

<span data-ttu-id="898b0-166">W danych wyjściowych polecenia zostanie wyświetlony monit podaj nową nazwę maszyny Wirtualnej, nazwa użytkownika administratora i hasła oraz identyfikator karty Sieciowej, którą utworzono wcześniej.</span><span class="sxs-lookup"><span data-stu-id="898b0-166">In the command output, you are prompted to supply a new VM name, the admin user name and password, and the Id of the NIC you created previously.</span></span>

```bash
info:    Executing command group deployment create
info:    Supply values for the following parameters
vmName: myNewVM
adminUserName: myAdminuser
adminPassword: ********
networkInterfaceId: /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resource Groups/myResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic
```

<span data-ttu-id="898b0-167">Poniższy przykład pokazuje, zobacz pomyślne wdrożenie:</span><span class="sxs-lookup"><span data-stu-id="898b0-167">The following sample shows what you see for a successful deployment:</span></span>

```bash
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment xxxxxxx
+ Waiting for deployment to complete
data:    DeploymentName     : MyDeployment
data:    ResourceGroupName  : MyResourceGroup1
data:    ProvisioningState  : Succeeded
data:    Timestamp          : xxxxxxx
data:    Mode               : Incremental
data:    Name                Type          Value

data:    ------------------  ------------  -------------------------------------

data:    vmName              String        myNewVM

data:    vmSize              String        Standard_D1

data:    adminUserName       String        myAdminuser

data:    adminPassword       SecureString  undefined

data:    networkInterfaceId  String        /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/MyResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic
info:    group deployment create command OK
```

### <a name="verify-the-deployment"></a><span data-ttu-id="898b0-168">Weryfikacja wdrażania</span><span class="sxs-lookup"><span data-stu-id="898b0-168">Verify the deployment</span></span>
<span data-ttu-id="898b0-169">Teraz SSH dla maszyny wirtualnej utworzonej do weryfikowania wdrożenia i rozpocząć korzystanie z nowej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="898b0-169">Now SSH to the virtual machine you created to verify the deployment and start using the new VM.</span></span> <span data-ttu-id="898b0-170">Aby połączyć się za pośrednictwem protokołu SSH, znaleźć adres IP maszyny wirtualnej został utworzony za pomocą następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="898b0-170">To connect via SSH, find the IP address of the VM you created by running the following command:</span></span>

```azurecli
azure network public-ip show myResourceGroup1 myPublicIP
```

<span data-ttu-id="898b0-171">Publiczny adres IP znajduje się w danych wyjściowych polecenia.</span><span class="sxs-lookup"><span data-stu-id="898b0-171">The public IP address is listed in the command output.</span></span> <span data-ttu-id="898b0-172">Domyślnie można podłączyć się do maszyny Wirtualnej systemu Linux przez SSH na port 22.</span><span class="sxs-lookup"><span data-stu-id="898b0-172">By default you connect to the Linux VM by SSH on port 22.</span></span>

## <a name="create-additional-vms"></a><span data-ttu-id="898b0-173">Utwórz dodatkowe maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="898b0-173">Create additional VMs</span></span>
<span data-ttu-id="898b0-174">Skorzystaj z przechwyconego obrazu i szablonu można wdrożyć dodatkowe maszyny wirtualne, korzystając z procedury w poprzedniej sekcji.</span><span class="sxs-lookup"><span data-stu-id="898b0-174">Use the captured image and template to deploy additional VMs using the steps in the preceding section.</span></span> <span data-ttu-id="898b0-175">Inne opcje do tworzenia maszyn wirtualnych z obrazu obejmują przy użyciu szablonu Szybki Start lub systemem **tworzenia maszyny wirtualnej azure** polecenia.</span><span class="sxs-lookup"><span data-stu-id="898b0-175">Other options to create VMs from the image include using a quickstart template or running the **azure vm create** command.</span></span>

### <a name="use-the-captured-template"></a><span data-ttu-id="898b0-176">Użyj szablonu przechwycony</span><span class="sxs-lookup"><span data-stu-id="898b0-176">Use the captured template</span></span>
<span data-ttu-id="898b0-177">Aby użyć przechwyconego obrazu szablonu, wykonaj następujące kroki, (szczegóły w poprzedniej sekcji):</span><span class="sxs-lookup"><span data-stu-id="898b0-177">To use the captured image and template, follow these steps (detailed in the preceding section):</span></span>

* <span data-ttu-id="898b0-178">Upewnij się, że obraz maszyny Wirtualnej ma na tym samym koncie magazynu, który jest hostem wirtualnego dysku twardego maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="898b0-178">Ensure that your VM image is in the same storage account that hosts your VM's VHD.</span></span>
* <span data-ttu-id="898b0-179">Skopiuj plik JSON szablonu i określ unikatową nazwę dysku systemu operacyjnego, dysku VHD nowej maszyny Wirtualnej (lub wirtualne dyski twarde).</span><span class="sxs-lookup"><span data-stu-id="898b0-179">Copy the template JSON file and specify a unique name for the OS disk of the new VM's VHD (or VHDs).</span></span> <span data-ttu-id="898b0-180">Na przykład w **storageProfile**w obszarze **wirtualnego dysku twardego**w **uri**, określ unikatową nazwę dla **osDisk** wirtualnego dysku twardego, podobnie jak`https://xxxxxxxxxxxxxx.blob.core.windows.net/vhds/MyNewVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`</span><span class="sxs-lookup"><span data-stu-id="898b0-180">For example, in the **storageProfile**, under **vhd**, in **uri**, specify a unique name for the **osDisk** VHD, similar to `https://xxxxxxxxxxxxxx.blob.core.windows.net/vhds/MyNewVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`</span></span>
* <span data-ttu-id="898b0-181">Utwórz kartę Sieciową, w tym samym lub różnych sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="898b0-181">Create a NIC in either the same or a different virtual network.</span></span>
* <span data-ttu-id="898b0-182">Przy użyciu pliku JSON zmodyfikowany szablon, Utwórz wdrożenie w grupie zasobów, w którym Konfigurowanie sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="898b0-182">Using the modified template JSON file, create a deployment in the resource group in which you set up the virtual network.</span></span>

### <a name="use-a-quickstart-template"></a><span data-ttu-id="898b0-183">Szablon szybkiego startu</span><span class="sxs-lookup"><span data-stu-id="898b0-183">Use a quickstart template</span></span>
<span data-ttu-id="898b0-184">Jeśli chcesz skonfigurować automatycznie po utworzeniu maszyny Wirtualnej z obrazu sieci, można określić te zasoby w szablonie.</span><span class="sxs-lookup"><span data-stu-id="898b0-184">If you want the network set up automatically when you create a VM from the image, you can specify those resources in a template.</span></span> <span data-ttu-id="898b0-185">Na przykład, zobacz [101 maszyny wirtualnej użytkownika obrazu z szablonu](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) z usługi GitHub.</span><span class="sxs-lookup"><span data-stu-id="898b0-185">For example, see the [101-vm-from-user-image template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) from GitHub.</span></span> <span data-ttu-id="898b0-186">Ten szablon tworzy Maszynę wirtualną z niestandardowego obrazu i niezbędne sieci wirtualnej, publiczny adres IP i zasobów kart interfejsu Sieciowego.</span><span class="sxs-lookup"><span data-stu-id="898b0-186">This template creates a VM from your custom image and the necessary virtual network, public IP address, and NIC resources.</span></span> <span data-ttu-id="898b0-187">Przewodnik przy użyciu szablonu w portalu Azure, zobacz [tworzenia maszyny wirtualnej z obrazu niestandardowego za pomocą szablonu usługi Resource Manager](http://codeisahighway.com/how-to-create-a-virtual-machine-from-a-custom-image-using-an-arm-template/).</span><span class="sxs-lookup"><span data-stu-id="898b0-187">For a walkthrough of using the template in the Azure portal, see [How to create a virtual machine from a custom image using a Resource Manager template](http://codeisahighway.com/how-to-create-a-virtual-machine-from-a-custom-image-using-an-arm-template/).</span></span>

### <a name="use-the-azure-vm-create-command"></a><span data-ttu-id="898b0-188">Polecenie utworzenia Użyj maszyna wirtualna platformy azure</span><span class="sxs-lookup"><span data-stu-id="898b0-188">Use the azure vm create command</span></span>
<span data-ttu-id="898b0-189">Zazwyczaj łatwiej jest utworzyć Maszynę wirtualną z obrazu za pomocą szablonu usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="898b0-189">Usually it's easiest to use a Resource Manager template to create a VM from the image.</span></span> <span data-ttu-id="898b0-190">Można jednak utworzyć maszyny Wirtualnej *imperatively* przy użyciu **tworzenia maszyny wirtualnej azure** z **-Q** (**— urn obrazu**) parametru.</span><span class="sxs-lookup"><span data-stu-id="898b0-190">However, you can create the VM *imperatively* by using the **azure vm create** command with the **-Q** (**--image-urn**) parameter.</span></span> <span data-ttu-id="898b0-191">Jeśli używasz tej metody należy również przekazać **-d** (**systemu operacyjnego —-dysk-dysk vhd**) parametr, aby określić lokalizację pliku VHD systemu operacyjnego dla nowej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="898b0-191">If you use this method, you also pass the **-d** (**--os-disk-vhd**) parameter to specify the location of the OS .vhd file for the new VM.</span></span> <span data-ttu-id="898b0-192">Ten plik musi znajdować się w kontenerze wirtualne dyski twarde konta magazynu, w którym jest przechowywany plik VHD obrazu.</span><span class="sxs-lookup"><span data-stu-id="898b0-192">This file must be in the vhds container of the storage account where the image VHD file is stored.</span></span> <span data-ttu-id="898b0-193">Polecenie kopiuje dysk VHD dla nowej maszyny Wirtualnej automatycznie **wirtualne dyski twarde** kontenera.</span><span class="sxs-lookup"><span data-stu-id="898b0-193">The command copies the VHD for the new VM automatically to the **vhds** container.</span></span>

<span data-ttu-id="898b0-194">Przed uruchomieniem **tworzenia maszyny wirtualnej azure** przy użyciu obrazu, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="898b0-194">Before running **azure vm create** with the image, complete the following steps:</span></span>

1. <span data-ttu-id="898b0-195">Utwórz grupę zasobów lub zidentyfikować istniejącą grupę zasobów dla wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="898b0-195">Create a resource group, or identify an existing resource group for the deployment.</span></span>
2. <span data-ttu-id="898b0-196">Utwórz zasób publiczny adres IP i zasobów kart interfejsu Sieciowego dla nowej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="898b0-196">Create a public IP address resource and a NIC resource for the new VM.</span></span> <span data-ttu-id="898b0-197">Aby uzyskać kroki, aby utworzyć sieć wirtualną, publiczny adres IP i kart przy użyciu interfejsu wiersza polecenia Zobacz wcześniej w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="898b0-197">For steps to create a virtual network, public IP address, and NIC by using the CLI, see earlier in this article.</span></span> <span data-ttu-id="898b0-198">(**tworzenia maszyny wirtualnej azure** można również utworzyć karty Sieciowej, ale należy przekazywać dodatkowych parametrów dla sieci wirtualnej i podsieci.)</span><span class="sxs-lookup"><span data-stu-id="898b0-198">(**azure vm create** can also create a NIC, but you need to pass additional parameters for a virtual network and subnet.)</span></span>

<span data-ttu-id="898b0-199">Następnie uruchom polecenie, które przekazuje identyfikatorów URI do nowego pliku wirtualnego dysku twardego systemu operacyjnego i istniejącego obrazu.</span><span class="sxs-lookup"><span data-stu-id="898b0-199">Then run a command that passes URIs to both the new OS VHD file and the existing image.</span></span> <span data-ttu-id="898b0-200">W tym przykładzie rozmiar Standard_A1 maszyna wirtualna jest utworzona w regionie wschodnie stany USA.</span><span class="sxs-lookup"><span data-stu-id="898b0-200">In this example, a size Standard_A1 VM is created in the East US region.</span></span>

```azurecli
azure vm create -g myResourceGroup1 -n myNewVM -l eastus -y Linux \
-z Standard_A1 -u myAdminname -p myPassword -f myNIC \
-d "https://xxxxxxxxxxxxxx.blob.core.windows.net/vhds/MyNewVHDNamePrefix.vhd" \
-Q "https://xxxxxxxxxxxxxx.blob.core.windows.net/system/Microsoft.Compute/Images/vhds/MyVHDNamePrefix-osDisk.vhd"
```

<span data-ttu-id="898b0-201">Opcje dodatkowe polecenia, można uruchomić `azure help vm create`.</span><span class="sxs-lookup"><span data-stu-id="898b0-201">For additional command options, run `azure help vm create`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="898b0-202">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="898b0-202">Next steps</span></span>
<span data-ttu-id="898b0-203">Aby zarządzać maszyn wirtualnych z poziomu interfejsu wiersza polecenia, zobacz zadań w [wdrażania i zarządzania maszynami wirtualnymi przy użyciu szablonów usługi Azure Resource Manager i interfejsu wiersza polecenia Azure](create-ssh-secured-vm-from-template.md).</span><span class="sxs-lookup"><span data-stu-id="898b0-203">To manage your VMs with the CLI, see the tasks in [Deploy and manage virtual machines by using Azure Resource Manager templates and the Azure CLI](create-ssh-secured-vm-from-template.md).</span></span>

