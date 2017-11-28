---
title: aaaCapture toouse Azure maszyny Wirtualnej systemu Linux jako szablon | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toocapture i obraz opartych na systemie Linux Azure maszynę wirtualną (VM) utworzone za pomocą modelu wdrażania usługi Azure Resource Manager hello."
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
ms.openlocfilehash: 877eee5c842bebe80e755c2240cdaaef4ade6ff5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="capture-a-linux-virtual-machine-running-on-azure"></a><span data-ttu-id="b255a-103">Przechwytywanie maszyny wirtualnej systemu Linux działających na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="b255a-103">Capture a Linux virtual machine running on Azure</span></span>
<span data-ttu-id="b255a-104">Wykonaj kroki hello w tym artykule toogeneralize i przechwycenia maszyny wirtualnej systemu Linux platformy Azure (VM) w modelu wdrażania usługi Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="b255a-104">Follow hello steps in this article toogeneralize and capture your Azure Linux virtual machine (VM) in hello Resource Manager deployment model.</span></span> <span data-ttu-id="b255a-105">Uogólnienie hello maszyny Wirtualnej, Usuń konto osobiste informacje i przygotować toobe wirtualna hello użyty jako obraz.</span><span class="sxs-lookup"><span data-stu-id="b255a-105">When you generalize hello VM, you remove personal account information and prepare hello VM toobe used as an image.</span></span> <span data-ttu-id="b255a-106">Można następnie przechwytywania obrazów uogólniony wirtualny dysk twardy (VHD) do hello systemu operacyjnego, dysków VHD dla dysków dołączonych danych i [szablonu usługi Resource Manager](../../azure-resource-manager/resource-group-overview.md) o nowych wdrożeniach maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b255a-106">You then capture a generalized virtual hard disk (VHD) image for hello OS, VHDs for attached data disks, and a [Resource Manager template](../../azure-resource-manager/resource-group-overview.md) for new VM deployments.</span></span> <span data-ttu-id="b255a-107">W tym artykule szczegółowo sposób obrazu toocapture maszyny Wirtualnej o hello Azure CLI 1.0 dla maszyny Wirtualnej za pomocą niezarządzanych dysków.</span><span class="sxs-lookup"><span data-stu-id="b255a-107">This article details how toocapture a VM image with hello Azure CLI 1.0 for a VM using unmanaged disks.</span></span> <span data-ttu-id="b255a-108">Możesz również [Przechwytywanie maszyny Wirtualnej za pomocą dysków zarządzanych Azure z hello Azure CLI 2.0](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b255a-108">You can also [capture a VM using Azure Managed Disks with hello Azure CLI 2.0](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="b255a-109">Zarządzane dyski są obsługiwane przez hello platformy Azure i nie wymagają żadnych toostore przygotowania lub lokalizacji je.</span><span class="sxs-lookup"><span data-stu-id="b255a-109">Managed disks are handled by hello Azure platform and do not require any preparation or location toostore them.</span></span> <span data-ttu-id="b255a-110">Aby uzyskać więcej informacji, zobacz temat [Omówienie usługi Azure Managed Disks](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b255a-110">For more information, see [Azure Managed Disks overview](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 

<span data-ttu-id="b255a-111">toocreate maszyn wirtualnych przy użyciu obrazu hello, skonfiguruj zasobów sieciowych dla każdej nowej maszyny Wirtualnej i użyj hello toodeploy szablonu (pliku notacji obiektu JavaScript lub formatu JSON,) z hello przechwyconych obrazów dysków VHD.</span><span class="sxs-lookup"><span data-stu-id="b255a-111">toocreate VMs using hello image, set up network resources for each new VM, and use hello template (a JavaScript Object Notation, or JSON, file) toodeploy it from hello captured VHD images.</span></span> <span data-ttu-id="b255a-112">W ten sposób można replikować maszyny Wirtualnej z bieżącej konfiguracji oprogramowania, podobnie toohello używać obrazów w hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="b255a-112">In this way, you can replicate a VM with its current software configuration, similar toohello way you use images in hello Azure Marketplace.</span></span>

> [!TIP]
> <span data-ttu-id="b255a-113">Jeśli toocreate kopię istniejącej maszyny Wirtualnej systemu Linux jej stanem specjalne tworzenia kopii zapasowej i debugowania, zobacz [utworzenie kopii maszyny wirtualnej systemu Linux działających na platformie Azure](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b255a-113">If you want toocreate a copy of your existing Linux VM with its specialized state for backup or debugging, see [Create a copy of a Linux virtual machine running on Azure](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="b255a-114">I tooupload wirtualnego dysku twardego z lokalnej maszyny Wirtualnej systemu Linux, zobacz [przekazywanie i Utwórz Maszynę wirtualną systemu Linux na podstawie obrazu niestandardowego dysku](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b255a-114">And if you want tooupload a Linux VHD from an on-premises VM, see [Upload and create a Linux VM from custom disk image](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>  

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="b255a-115">Zadanie hello toocomplete wersje interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="b255a-115">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="b255a-116">Można ukończyć powitalnych zadań przy użyciu jednej z hello następujące wersje interfejsu wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="b255a-116">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="b255a-117">[Azure CLI 1.0](#before-you-begin) — nasze interfejsu wiersza polecenia dla hello classic i zasobów zarządzania wdrażania modeli (w tym artykule)</span><span class="sxs-lookup"><span data-stu-id="b255a-117">[Azure CLI 1.0](#before-you-begin) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="b255a-118">[Azure CLI 2.0](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -naszej nowej generacji interfejsu wiersza polecenia dla modelu wdrażania zarządzania zasobów hello</span><span class="sxs-lookup"><span data-stu-id="b255a-118">[Azure CLI 2.0](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="b255a-119">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="b255a-119">Before you begin</span></span>
<span data-ttu-id="b255a-120">Upewnij się, czy zostały spełnione następujące wymagania wstępne hello:</span><span class="sxs-lookup"><span data-stu-id="b255a-120">Ensure that you meet hello following prerequisites:</span></span>

* <span data-ttu-id="b255a-121">**Maszyna wirtualna platformy Azure utworzonych w modelu wdrażania usługi Resource Manager hello** — Jeśli nie utworzono Maszynę wirtualną systemu Linux, możesz użyć hello [portalu](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), hello [interfejsu wiersza polecenia Azure](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), lub [Resource Manager szablony](create-ssh-secured-vm-from-template.md).</span><span class="sxs-lookup"><span data-stu-id="b255a-121">**Azure VM created in hello Resource Manager deployment model** - If you haven't created a Linux VM, you can use hello [portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), hello [Azure CLI](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), or [Resource Manager templates](create-ssh-secured-vm-from-template.md).</span></span> 
  
    <span data-ttu-id="b255a-122">Skonfiguruj hello maszyny Wirtualnej, zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="b255a-122">Configure hello VM as needed.</span></span> <span data-ttu-id="b255a-123">Na przykład [Dodaj dyski danych](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), stosowania aktualizacji i zainstalować aplikacje.</span><span class="sxs-lookup"><span data-stu-id="b255a-123">For example, [add data disks](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), apply updates, and install applications.</span></span> 
* <span data-ttu-id="b255a-124">**Azure CLI** -Install hello [interfejsu wiersza polecenia Azure](../../cli-install-nodejs.md) na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="b255a-124">**Azure CLI** - Install hello [Azure CLI](../../cli-install-nodejs.md) on a local computer.</span></span>

## <a name="step-1-remove-hello-azure-linux-agent"></a><span data-ttu-id="b255a-125">Krok 1: Usuń agenta systemu Linux Azure hello</span><span class="sxs-lookup"><span data-stu-id="b255a-125">Step 1: Remove hello Azure Linux agent</span></span>
<span data-ttu-id="b255a-126">Najpierw uruchom hello **agenta waagent** z hello **deprovision** parametru na powitania maszyny Wirtualnej systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="b255a-126">First, run hello **waagent** command with hello **deprovision** parameter on hello Linux VM.</span></span> <span data-ttu-id="b255a-127">To polecenie usuwa pliki i hello toomake danych gotowe do uogólnianie maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b255a-127">This command deletes files and data toomake hello VM ready for generalizing.</span></span> <span data-ttu-id="b255a-128">Aby uzyskać więcej informacji, zobacz hello [Podręcznik użytkownika agenta systemu Linux Azure](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b255a-128">For details, see hello [Azure Linux Agent user guide](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

1. <span data-ttu-id="b255a-129">Połącz tooyour maszyny Wirtualnej systemu Linux przy użyciu klienta SSH.</span><span class="sxs-lookup"><span data-stu-id="b255a-129">Connect tooyour Linux VM using an SSH client.</span></span>
2. <span data-ttu-id="b255a-130">W oknie SSH hello wpisz następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="b255a-130">In hello SSH window, type hello following command:</span></span>
   
    ```bash
    sudo waagent -deprovision+user
    ```
   > [!NOTE]
   > <span data-ttu-id="b255a-131">Tylko Uruchom to polecenie na maszynie Wirtualnej, który ma toocapture jako obraz.</span><span class="sxs-lookup"><span data-stu-id="b255a-131">Only run this command on a VM that you intend toocapture as an image.</span></span> <span data-ttu-id="b255a-132">Nie gwarantuje obrazu hello jest brany pod uwagę wszystkie informacje poufne lub nadaje się do ponownej dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="b255a-132">It does not guarantee that hello image is cleared of all sensitive information or is suitable for redistribution.</span></span>
 
3. <span data-ttu-id="b255a-133">Typ **y** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="b255a-133">Type **y** toocontinue.</span></span> <span data-ttu-id="b255a-134">Możesz dodać hello **-wymusić** tooavoid parametr ten krok potwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="b255a-134">You can add hello **-force** parameter tooavoid this confirmation step.</span></span>
4. <span data-ttu-id="b255a-135">Po zakończeniu wykonywania polecenia hello wpisz **zakończyć**.</span><span class="sxs-lookup"><span data-stu-id="b255a-135">After hello command completes, type **exit**.</span></span> <span data-ttu-id="b255a-136">Ten krok powoduje zamknięcie powitania klienta SSH.</span><span class="sxs-lookup"><span data-stu-id="b255a-136">This step closes hello SSH client.</span></span>

## <a name="step-2-capture-hello-vm"></a><span data-ttu-id="b255a-137">Krok 2: Przechwytywanie hello maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="b255a-137">Step 2: Capture hello VM</span></span>
<span data-ttu-id="b255a-138">Użyj hello toogeneralize wiersza polecenia platformy Azure i przechwytywania hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b255a-138">Use hello Azure CLI toogeneralize and capture hello VM.</span></span> <span data-ttu-id="b255a-139">Poniższe przykłady w hello Zastąp przykładowe nazwy parametrów własne wartości.</span><span class="sxs-lookup"><span data-stu-id="b255a-139">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="b255a-140">Przykład nazwy parametru zawierają **myResourceGroup**, **myVnet**, i **myVM**.</span><span class="sxs-lookup"><span data-stu-id="b255a-140">Example parameter names include **myResourceGroup**, **myVnet**, and **myVM**.</span></span>

1. <span data-ttu-id="b255a-141">Z komputera lokalnego, otwórz hello wiersza polecenia platformy Azure i [tooyour logowania subskrypcji platformy Azure](../../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="b255a-141">From your local computer, open hello Azure CLI and [login tooyour Azure subscription](../../xplat-cli-connect.md).</span></span> 
2. <span data-ttu-id="b255a-142">Upewnij się, że jesteś w trybie Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="b255a-142">Make sure you are in Resource Manager mode.</span></span>
   
    ```azurecli
    azure config mode arm
    ```
3. <span data-ttu-id="b255a-143">Zamknij maszynę Wirtualną, która już anulowana za pomocą następującego polecenia hello hello:</span><span class="sxs-lookup"><span data-stu-id="b255a-143">Shut down hello VM that you already deprovisioned by using hello following command:</span></span>
   
    ```azurecli
    azure vm deallocate -g myResourceGroup -n myVM
    ```
4. <span data-ttu-id="b255a-144">Generalize hello maszyny Wirtualnej z hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="b255a-144">Generalize hello VM with hello following command:</span></span>
   
    ```azurecli
    azure vm generalize -g myResourceGroup -n myVM
    ```
5. <span data-ttu-id="b255a-145">Teraz uruchom hello **przechwytywania maszyna wirtualna platformy azure** polecenia, które przechwytywania hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b255a-145">Now run hello **azure vm capture** command, which captures hello VM.</span></span> <span data-ttu-id="b255a-146">W hello poniższy przykład, wirtualne dyski twarde są przechwytywane z obrazu hello nazwy zaczyna się od **MyVHDNamePrefix**i hello **-t** opcja określa szablon toohello ścieżki **MyTemplate.json**.</span><span class="sxs-lookup"><span data-stu-id="b255a-146">In hello following example, hello image VHDs are captured with names beginning with **MyVHDNamePrefix**, and hello **-t** option specifies a path toohello template **MyTemplate.json**.</span></span> 
   
    ```azurecli
    azure vm capture -g myResourceGroup -n myVM -p myVHDNamePrefix -t myTemplate.json
    ```
   
   > [!IMPORTANT]
   > <span data-ttu-id="b255a-147">pliki VHD obrazu Hello tworzone domyślnie hello używać tego samego konta magazynu, który hello oryginalna maszyna wirtualna.</span><span class="sxs-lookup"><span data-stu-id="b255a-147">hello image VHD files get created by default in hello same storage account that hello original VM used.</span></span> <span data-ttu-id="b255a-148">Użyj hello *tego samego konta magazynu* hello toostore wirtualne dyski twarde dla wszelkie nowe maszyny wirtualne, Utwórz hello obrazu.</span><span class="sxs-lookup"><span data-stu-id="b255a-148">Use hello *same storage account* toostore hello VHDs for any new VMs you create from hello image.</span></span> 

6. <span data-ttu-id="b255a-149">Lokalizacja hello toofind przechwyconego obrazu szablonu JSON hello otwarty w edytorze tekstów.</span><span class="sxs-lookup"><span data-stu-id="b255a-149">toofind hello location of a captured image, open hello JSON template in a text editor.</span></span> <span data-ttu-id="b255a-150">W hello **storageProfile**, Znajdź hello **uri** z hello **obrazu** znajduje się w hello **systemu** kontenera.</span><span class="sxs-lookup"><span data-stu-id="b255a-150">In hello **storageProfile**, find hello **uri** of hello **image** located in hello **system** container.</span></span> <span data-ttu-id="b255a-151">Na przykład hello identyfikatora URI obrazu dysku systemu operacyjnego hello przypomina zbyt`https://xxxxxxxxxxxxxx.blob.core.windows.net/system/Microsoft.Compute/Images/vhds/MyVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`</span><span class="sxs-lookup"><span data-stu-id="b255a-151">For example, hello URI of hello OS disk image is similar too`https://xxxxxxxxxxxxxx.blob.core.windows.net/system/Microsoft.Compute/Images/vhds/MyVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`</span></span>

## <a name="step-3-create-a-vm-from-hello-captured-image"></a><span data-ttu-id="b255a-152">Krok 3: Tworzenie maszyny Wirtualnej z hello przechwycony obraz</span><span class="sxs-lookup"><span data-stu-id="b255a-152">Step 3: Create a VM from hello captured image</span></span>
<span data-ttu-id="b255a-153">Teraz za pomocą obrazu hello toocreate szablonu maszyny Wirtualnej systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="b255a-153">Now use hello image with a template toocreate a Linux VM.</span></span> <span data-ttu-id="b255a-154">Te kroki pokazują, jak toouse hello wiersza polecenia platformy Azure i hello szablon pliku JSON przechwycone toocreate hello maszyny Wirtualnej w nowej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b255a-154">These steps show you how toouse hello Azure CLI and hello JSON file template you captured toocreate hello VM in a new virtual network.</span></span>

### <a name="create-network-resources"></a><span data-ttu-id="b255a-155">Utwórz zasoby sieciowe</span><span class="sxs-lookup"><span data-stu-id="b255a-155">Create network resources</span></span>
<span data-ttu-id="b255a-156">Szablon hello toouse, należy najpierw tooset sieci wirtualnej i karty Sieciowej dla nowej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b255a-156">toouse hello template, you first need tooset up a virtual network and NIC for your new VM.</span></span> <span data-ttu-id="b255a-157">Zaleca się tworzenie grupy zasobów dla tych zasobów w hello miejsce przechowywania obrazu maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b255a-157">We recommend you create a resource group for these resources in hello location where your VM image is stored.</span></span> <span data-ttu-id="b255a-158">Uruchom polecenia podobne toohello po, zastępując nazwy zasobów i odpowiednie lokalizacji platformy Azure ("centralus" w tych poleceniach):</span><span class="sxs-lookup"><span data-stu-id="b255a-158">Run commands similar toohello following, substituting names for your resources and an appropriate Azure location ("centralus" in these commands):</span></span>

```azurecli
azure group create myResourceGroup1 -l "centralus"

azure network vnet create myResourceGroup1 myVnet -l "centralus"

azure network vnet subnet create myResourceGroup1 myVnet mySubnet

azure network public-ip create myResourceGroup1 myPublicIP -l "centralus"

azure network nic create myResourceGroup1 myNIC -k mySubnet -m myVnet -p myPublicIP -l "centralus"
```

### <a name="get-hello-id-of-hello-nic"></a><span data-ttu-id="b255a-159">Pobierz hello identyfikator hello karty Sieciowej</span><span class="sxs-lookup"><span data-stu-id="b255a-159">Get hello Id of hello NIC</span></span>
<span data-ttu-id="b255a-160">toodeploy maszyny Wirtualnej z obrazu hello przy użyciu hello JSON zapisane podczas przechwytywania, należy hello identyfikator hello karty sieciowej.</span><span class="sxs-lookup"><span data-stu-id="b255a-160">toodeploy a VM from hello image by using hello JSON you saved during capture, you need hello Id of hello NIC.</span></span> <span data-ttu-id="b255a-161">Go uzyskać, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="b255a-161">Obtain it by running hello following command:</span></span>

```azurecli
azure network nic show myResourceGroup1 myNIC
```

<span data-ttu-id="b255a-162">Witaj **identyfikator** w hello dane wyjściowe są podobne zbyt`/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/MyResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic`</span><span class="sxs-lookup"><span data-stu-id="b255a-162">hello **Id** in hello output is similar too`/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/MyResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic`</span></span>

### <a name="create-a-vm"></a><span data-ttu-id="b255a-163">Tworzenie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="b255a-163">Create a VM</span></span>
<span data-ttu-id="b255a-164">Teraz hello uruchom następujące polecenie toocreate maszyny Wirtualnej z hello przechwycony obraz maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b255a-164">Now run hello following command toocreate your VM from hello captured VM image.</span></span> <span data-ttu-id="b255a-165">Użyj hello **-f** szablon toohello ścieżki hello toospecify parametru JSON plik zostanie zapisany.</span><span class="sxs-lookup"><span data-stu-id="b255a-165">Use hello **-f** parameter toospecify hello path toohello template JSON file you saved.</span></span>

```azurecli
azure group deployment create myResourceGroup1 MyDeployment -f MyTemplate.json
```

<span data-ttu-id="b255a-166">W danych wyjściowych polecenia hello są toosupply zostanie wyświetlony monit o nowe nazwę maszyny Wirtualnej, nazwa użytkownika administratora hello i hasło, a hello identyfikator hello karty Sieciowej, którą utworzono wcześniej.</span><span class="sxs-lookup"><span data-stu-id="b255a-166">In hello command output, you are prompted toosupply a new VM name, hello admin user name and password, and hello Id of hello NIC you created previously.</span></span>

```bash
info:    Executing command group deployment create
info:    Supply values for hello following parameters
vmName: myNewVM
adminUserName: myAdminuser
adminPassword: ********
networkInterfaceId: /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resource Groups/myResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic
```

<span data-ttu-id="b255a-167">następujące przykładowe Hello pokazuje, zobacz pomyślne wdrożenie:</span><span class="sxs-lookup"><span data-stu-id="b255a-167">hello following sample shows what you see for a successful deployment:</span></span>

```bash
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment xxxxxxx
+ Waiting for deployment toocomplete
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

### <a name="verify-hello-deployment"></a><span data-ttu-id="b255a-168">Sprawdź hello wdrożenia</span><span class="sxs-lookup"><span data-stu-id="b255a-168">Verify hello deployment</span></span>
<span data-ttu-id="b255a-169">Teraz SSH toohello maszyny wirtualnej utworzone tooverify hello wdrażania i uruchamiania przy użyciu hello nowej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b255a-169">Now SSH toohello virtual machine you created tooverify hello deployment and start using hello new VM.</span></span> <span data-ttu-id="b255a-170">tooconnect za pośrednictwem protokołu SSH, znaleźć adres IP hello hello maszyny Wirtualnej utworzonej, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="b255a-170">tooconnect via SSH, find hello IP address of hello VM you created by running hello following command:</span></span>

```azurecli
azure network public-ip show myResourceGroup1 myPublicIP
```

<span data-ttu-id="b255a-171">Hello publiczny adres IP jest wyświetlany w danych wyjściowych polecenia hello.</span><span class="sxs-lookup"><span data-stu-id="b255a-171">hello public IP address is listed in hello command output.</span></span> <span data-ttu-id="b255a-172">Domyślnie połączenie toohello maszyny Wirtualnej systemu Linux przez SSH na port 22.</span><span class="sxs-lookup"><span data-stu-id="b255a-172">By default you connect toohello Linux VM by SSH on port 22.</span></span>

## <a name="create-additional-vms"></a><span data-ttu-id="b255a-173">Utwórz dodatkowe maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="b255a-173">Create additional VMs</span></span>
<span data-ttu-id="b255a-174">Użyj hello przechwycone toodeploy obrazu i szablon dodatkowe maszyny wirtualne, wykonując kroki hello w powyższej sekcji hello.</span><span class="sxs-lookup"><span data-stu-id="b255a-174">Use hello captured image and template toodeploy additional VMs using hello steps in hello preceding section.</span></span> <span data-ttu-id="b255a-175">Inne opcje toocreate maszyn wirtualnych z obrazu hello obejmują przy użyciu szablonu Szybki Start lub uruchomione hello **tworzenia maszyny wirtualnej azure** polecenia.</span><span class="sxs-lookup"><span data-stu-id="b255a-175">Other options toocreate VMs from hello image include using a quickstart template or running hello **azure vm create** command.</span></span>

### <a name="use-hello-captured-template"></a><span data-ttu-id="b255a-176">Użyj szablonu przechwyconych hello</span><span class="sxs-lookup"><span data-stu-id="b255a-176">Use hello captured template</span></span>
<span data-ttu-id="b255a-177">toouse hello przechwycony obraz i szablonu, wykonaj następujące kroki, (szczegóły w powyższej sekcji hello):</span><span class="sxs-lookup"><span data-stu-id="b255a-177">toouse hello captured image and template, follow these steps (detailed in hello preceding section):</span></span>

* <span data-ttu-id="b255a-178">Upewnij się, że obraz maszyny Wirtualnej jest w hello tego samego konta magazynu, który jest hostem wirtualnego dysku twardego maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b255a-178">Ensure that your VM image is in hello same storage account that hosts your VM's VHD.</span></span>
* <span data-ttu-id="b255a-179">Skopiuj plik JSON szablonu hello i określ unikatową nazwę dysku systemu operacyjnego hello hello nowej maszyny Wirtualnej wirtualnego dysku twardego (lub wirtualne dyski twarde).</span><span class="sxs-lookup"><span data-stu-id="b255a-179">Copy hello template JSON file and specify a unique name for hello OS disk of hello new VM's VHD (or VHDs).</span></span> <span data-ttu-id="b255a-180">Na przykład w hello **storageProfile**w obszarze **wirtualnego dysku twardego**w **uri**, określ unikatową nazwę dla hello **osDisk** wirtualnego dysku twardego, podobne zbyt`https://xxxxxxxxxxxxxx.blob.core.windows.net/vhds/MyNewVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`</span><span class="sxs-lookup"><span data-stu-id="b255a-180">For example, in hello **storageProfile**, under **vhd**, in **uri**, specify a unique name for hello **osDisk** VHD, similar too`https://xxxxxxxxxxxxxx.blob.core.windows.net/vhds/MyNewVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`</span></span>
* <span data-ttu-id="b255a-181">Utwórz kartę Sieciową w obu hello tej samej lub innej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b255a-181">Create a NIC in either hello same or a different virtual network.</span></span>
* <span data-ttu-id="b255a-182">Przy użyciu pliku JSON hello zmodyfikować szablon, Utwórz wdrożenie w grupie zasobów hello, w którym zdefiniować hello sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b255a-182">Using hello modified template JSON file, create a deployment in hello resource group in which you set up hello virtual network.</span></span>

### <a name="use-a-quickstart-template"></a><span data-ttu-id="b255a-183">Szablon szybkiego startu</span><span class="sxs-lookup"><span data-stu-id="b255a-183">Use a quickstart template</span></span>
<span data-ttu-id="b255a-184">Jeśli chcesz skonfigurować automatycznie po utworzeniu maszyny Wirtualnej z obrazu hello sieci hello tych zasobów można określić w szablonie.</span><span class="sxs-lookup"><span data-stu-id="b255a-184">If you want hello network set up automatically when you create a VM from hello image, you can specify those resources in a template.</span></span> <span data-ttu-id="b255a-185">Na przykład, zobacz hello [101 maszyny wirtualnej użytkownika obrazu z szablonu](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) z usługi GitHub.</span><span class="sxs-lookup"><span data-stu-id="b255a-185">For example, see hello [101-vm-from-user-image template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) from GitHub.</span></span> <span data-ttu-id="b255a-186">Ten szablon tworzy Maszynę wirtualną z obrazu niestandardowego i hello niezbędne sieci wirtualnej, publiczny adres IP i zasobów kart interfejsu Sieciowego.</span><span class="sxs-lookup"><span data-stu-id="b255a-186">This template creates a VM from your custom image and hello necessary virtual network, public IP address, and NIC resources.</span></span> <span data-ttu-id="b255a-187">Przewodnik przy użyciu szablonu hello hello portalu Azure, zobacz [jak toocreate maszynę wirtualną z obrazu niestandardowego za pomocą szablonu usługi Resource Manager](http://codeisahighway.com/how-to-create-a-virtual-machine-from-a-custom-image-using-an-arm-template/).</span><span class="sxs-lookup"><span data-stu-id="b255a-187">For a walkthrough of using hello template in hello Azure portal, see [How toocreate a virtual machine from a custom image using a Resource Manager template](http://codeisahighway.com/how-to-create-a-virtual-machine-from-a-custom-image-using-an-arm-template/).</span></span>

### <a name="use-hello-azure-vm-create-command"></a><span data-ttu-id="b255a-188">Użyj hello azure vm Utwórz polecenie</span><span class="sxs-lookup"><span data-stu-id="b255a-188">Use hello azure vm create command</span></span>
<span data-ttu-id="b255a-189">Zazwyczaj jest najprostszym toouse toocreate szablon Menedżera zasobów maszyny Wirtualnej z obrazu hello.</span><span class="sxs-lookup"><span data-stu-id="b255a-189">Usually it's easiest toouse a Resource Manager template toocreate a VM from hello image.</span></span> <span data-ttu-id="b255a-190">Można jednak utworzyć hello wirtualna *imperatively* przy użyciu hello **tworzenia maszyny wirtualnej platformy azure** z hello **-Q** (**— urn obrazu**) parametru .</span><span class="sxs-lookup"><span data-stu-id="b255a-190">However, you can create hello VM *imperatively* by using hello **azure vm create** command with hello **-Q** (**--image-urn**) parameter.</span></span> <span data-ttu-id="b255a-191">Jeśli ta metoda również przekazać hello **-d** (**systemu operacyjnego —-dysk-dysk vhd**) parametru toospecify hello lokalizację pliku VHD hello systemu operacyjnego dla hello nowej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b255a-191">If you use this method, you also pass hello **-d** (**--os-disk-vhd**) parameter toospecify hello location of hello OS .vhd file for hello new VM.</span></span> <span data-ttu-id="b255a-192">Ten plik musi znajdować się w kontenerze wirtualne dyski twarde hello hello konta magazynu, którym jest przechowywany plik wirtualnego dysku twardego obraz powitania.</span><span class="sxs-lookup"><span data-stu-id="b255a-192">This file must be in hello vhds container of hello storage account where hello image VHD file is stored.</span></span> <span data-ttu-id="b255a-193">Witaj polecenia kopie hello wirtualnego dysku twardego dla hello nowej maszyny Wirtualnej automatycznie toohello **wirtualne dyski twarde** kontenera.</span><span class="sxs-lookup"><span data-stu-id="b255a-193">hello command copies hello VHD for hello new VM automatically toohello **vhds** container.</span></span>

<span data-ttu-id="b255a-194">Przed uruchomieniem **tworzenia maszyny wirtualnej azure** z obrazem hello ukończyć hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="b255a-194">Before running **azure vm create** with hello image, complete hello following steps:</span></span>

1. <span data-ttu-id="b255a-195">Utwórz grupę zasobów lub istniejącej grupy zasobów dla wdrożenia hello zidentyfikować.</span><span class="sxs-lookup"><span data-stu-id="b255a-195">Create a resource group, or identify an existing resource group for hello deployment.</span></span>
2. <span data-ttu-id="b255a-196">Utwórz publiczny zasobu adresu IP i zasobu kart hello nowej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b255a-196">Create a public IP address resource and a NIC resource for hello new VM.</span></span> <span data-ttu-id="b255a-197">Kroki toocreate sieci wirtualnej publiczny adres IP i kart przy użyciu interfejsu wiersza polecenia, hello uzyskać wcześniej w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="b255a-197">For steps toocreate a virtual network, public IP address, and NIC by using hello CLI, see earlier in this article.</span></span> <span data-ttu-id="b255a-198">(**tworzenia maszyny wirtualnej azure** można również utworzyć karty Sieciowej, ale należy toopass dodatkowe parametry dla sieci wirtualnej i podsieci.)</span><span class="sxs-lookup"><span data-stu-id="b255a-198">(**azure vm create** can also create a NIC, but you need toopass additional parameters for a virtual network and subnet.)</span></span>

<span data-ttu-id="b255a-199">Następnie uruchom polecenie, które przekazuje identyfikatorów URI tooboth hello nowego pliku wirtualnego dysku twardego systemu operacyjnego i hello istniejącego obrazu.</span><span class="sxs-lookup"><span data-stu-id="b255a-199">Then run a command that passes URIs tooboth hello new OS VHD file and hello existing image.</span></span> <span data-ttu-id="b255a-200">W tym przykładzie rozmiar Standard_A1 zostanie utworzona maszyna wirtualna w regionie wschodnie stany USA hello.</span><span class="sxs-lookup"><span data-stu-id="b255a-200">In this example, a size Standard_A1 VM is created in hello East US region.</span></span>

```azurecli
azure vm create -g myResourceGroup1 -n myNewVM -l eastus -y Linux \
-z Standard_A1 -u myAdminname -p myPassword -f myNIC \
-d "https://xxxxxxxxxxxxxx.blob.core.windows.net/vhds/MyNewVHDNamePrefix.vhd" \
-Q "https://xxxxxxxxxxxxxx.blob.core.windows.net/system/Microsoft.Compute/Images/vhds/MyVHDNamePrefix-osDisk.vhd"
```

<span data-ttu-id="b255a-201">Opcje dodatkowe polecenia, można uruchomić `azure help vm create`.</span><span class="sxs-lookup"><span data-stu-id="b255a-201">For additional command options, run `azure help vm create`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b255a-202">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b255a-202">Next steps</span></span>
<span data-ttu-id="b255a-203">toomanage maszyn wirtualnych z hello interfejsu wiersza polecenia, zobacz zadań hello w [wdrażania i zarządzania maszynami wirtualnymi przy użyciu szablonów usługi Azure Resource Manager i hello Azure CLI](create-ssh-secured-vm-from-template.md).</span><span class="sxs-lookup"><span data-stu-id="b255a-203">toomanage your VMs with hello CLI, see hello tasks in [Deploy and manage virtual machines by using Azure Resource Manager templates and hello Azure CLI](create-ssh-secured-vm-from-template.md).</span></span>

