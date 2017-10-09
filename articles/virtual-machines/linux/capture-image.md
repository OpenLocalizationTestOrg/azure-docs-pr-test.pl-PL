---
title: "Obraz maszyny wirtualnej systemu Linux na platformie Azure przy użyciu interfejsu wiersza polecenia 2.0 aaaCapture | Dokumentacja firmy Microsoft"
description: "Przechwyć obraz maszyny Wirtualnej Azure toouse wdrożeń masowej przy użyciu hello Azure CLI 2.0."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: e608116f-f478-41be-b787-c2ad91b5a802
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 07/10/2017
ms.author: cynthn
ms.openlocfilehash: 9558332a86186b282775097428df462709373012
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-an-image-of-a-virtual-machine-or-vhd"></a><span data-ttu-id="1b041-103">Jak toocreate obraz maszyny wirtualnej lub wirtualnego dysku twardego</span><span class="sxs-lookup"><span data-stu-id="1b041-103">How toocreate an image of a virtual machine or VHD</span></span>

<!-- generalize, image - extended version of hello tutorial-->

<span data-ttu-id="1b041-104">toocreate wiele kopii toouse maszyny wirtualnej (VM) na platformie Azure, przechwytywania obrazu hello maszyny Wirtualnej lub hello wirtualnego dysku twardego systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="1b041-104">toocreate multiple copies of a virtual machine (VM) toouse in Azure, capture an image of hello VM or hello OS VHD.</span></span> <span data-ttu-id="1b041-105">toocreate obrazu, należy usunąć informacje osobiste konto, dzięki czemu bezpieczniejsze toodeploy wiele razy.</span><span class="sxs-lookup"><span data-stu-id="1b041-105">toocreate an image, you need remove personal account information which makes it safer toodeploy multiple times.</span></span> <span data-ttu-id="1b041-106">W hello następujące kroki, anulowanie zastrzeżenia istniejącej maszyny Wirtualnej, deallocate i tworzenie obrazu.</span><span class="sxs-lookup"><span data-stu-id="1b041-106">In hello following steps you deprovision an existing VM, deallocate and create an image.</span></span> <span data-ttu-id="1b041-107">Można użyć tego obrazu toocreate maszyn wirtualnych w dowolnej grupie zasobów w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="1b041-107">You can use this image toocreate VMs across any resource group within your subscription.</span></span>

<span data-ttu-id="1b041-108">Jeśli chcesz toocreate kopię istniejącej maszyny Wirtualnej systemu Linux tworzenia kopii zapasowej i debugowania lub przekazanie specjalne dysku VHD systemu Linux z lokalnej maszyny Wirtualnej, zobacz [przekazywanie i Utwórz Maszynę wirtualną systemu Linux na podstawie obrazu niestandardowego dysku](upload-vhd.md).</span><span class="sxs-lookup"><span data-stu-id="1b041-108">If you want toocreate a copy of your existing Linux VM for backup or debugging, or upload a specialized Linux VHD from an on-premises VM, see [Upload and create a Linux VM from custom disk image](upload-vhd.md).</span></span>  

<span data-ttu-id="1b041-109">Można również użyć **pakujący** toocreate konfiguracji niestandardowej.</span><span class="sxs-lookup"><span data-stu-id="1b041-109">You can also use **Packer** toocreate your custom configuration.</span></span> <span data-ttu-id="1b041-110">Aby uzyskać więcej informacji na temat używania pakujący, zobacz [jak obrazy maszyny wirtualnej systemu Linux toocreate pakujący toouse w programie Azure](build-image-with-packer.md).</span><span class="sxs-lookup"><span data-stu-id="1b041-110">For more information on using Packer, see [How toouse Packer toocreate Linux virtual machine images in Azure](build-image-with-packer.md).</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="1b041-111">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="1b041-111">Before you begin</span></span>
<span data-ttu-id="1b041-112">Upewnij się, czy zostały spełnione następujące wymagania wstępne hello:</span><span class="sxs-lookup"><span data-stu-id="1b041-112">Ensure that you meet hello following prerequisites:</span></span>

* <span data-ttu-id="1b041-113">Należy maszyny Wirtualnej platformy Azure utworzonych w modelu wdrażania usługi Resource Manager hello za pomocą dysków zarządzanych.</span><span class="sxs-lookup"><span data-stu-id="1b041-113">You need an Azure VM created in hello Resource Manager deployment model using managed disks.</span></span> <span data-ttu-id="1b041-114">Jeśli nie utworzono Maszynę wirtualną systemu Linux, możesz użyć hello [portal](quick-create-portal.md), hello [interfejsu wiersza polecenia Azure](quick-create-cli.md), lub [szablonów Resource Manager](create-ssh-secured-vm-from-template.md).</span><span class="sxs-lookup"><span data-stu-id="1b041-114">If you haven't created a Linux VM, you can use hello [portal](quick-create-portal.md), hello [Azure CLI](quick-create-cli.md), or [Resource Manager templates](create-ssh-secured-vm-from-template.md).</span></span> <span data-ttu-id="1b041-115">Skonfiguruj hello maszyny Wirtualnej, zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="1b041-115">Configure hello VM as needed.</span></span> <span data-ttu-id="1b041-116">Na przykład [Dodaj dyski danych](add-disk.md), stosowania aktualizacji i zainstalować aplikacje.</span><span class="sxs-lookup"><span data-stu-id="1b041-116">For example, [add data disks](add-disk.md), apply updates, and install applications.</span></span> 

* <span data-ttu-id="1b041-117">Należy również toohave hello najnowszych [Azure CLI 2.0](/cli/azure/install-az-cli2) zainstalowane i zalogować się przy użyciu konta Azure tooan [logowania az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="1b041-117">You also need toohave hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and be logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

## <a name="quick-commands"></a><span data-ttu-id="1b041-118">Szybkie polecenia</span><span class="sxs-lookup"><span data-stu-id="1b041-118">Quick commands</span></span>

<span data-ttu-id="1b041-119">Uproszczona wersja tego tematu, testowania, obliczenia lub informacje o maszynach wirtualnych na platformie Azure, dla [utworzyć niestandardowy obraz maszyny Wirtualnej platformy Azure przy użyciu interfejsu wiersza polecenia hello](tutorial-custom-images.md).</span><span class="sxs-lookup"><span data-stu-id="1b041-119">For a simplified version of this topic, for testing, evaluating or learning about VMs in Azure, see [Create a custom image of an Azure VM using hello CLI](tutorial-custom-images.md).</span></span>


## <a name="step-1-deprovision-hello-vm"></a><span data-ttu-id="1b041-120">Krok 1: Hello Deprovision maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="1b041-120">Step 1: Deprovision hello VM</span></span>
<span data-ttu-id="1b041-121">Możesz anulowanie zastrzeżenia hello maszyny Wirtualnej za pomocą agenta maszyny Wirtualnej Azure hello, toodelete maszyny określonych plików i danych.</span><span class="sxs-lookup"><span data-stu-id="1b041-121">You deprovision hello VM, using hello Azure VM agent, toodelete machine specific files and data.</span></span> <span data-ttu-id="1b041-122">Użyj hello `waagent` z hello *-deprovision + użytkownika* parametru w źródle maszyny Wirtualnej systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="1b041-122">Use hello `waagent` command with hello *-deprovision+user* parameter on your source Linux VM.</span></span> <span data-ttu-id="1b041-123">Aby uzyskać więcej informacji, zobacz hello [Podręcznik użytkownika agenta systemu Linux Azure](../windows/agent-user-guide.md).</span><span class="sxs-lookup"><span data-stu-id="1b041-123">For more information, see hello [Azure Linux Agent user guide](../windows/agent-user-guide.md).</span></span>

1. <span data-ttu-id="1b041-124">Połącz tooyour maszyny Wirtualnej systemu Linux przy użyciu klienta SSH.</span><span class="sxs-lookup"><span data-stu-id="1b041-124">Connect tooyour Linux VM using an SSH client.</span></span>
2. <span data-ttu-id="1b041-125">W oknie SSH hello wpisz następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="1b041-125">In hello SSH window, type hello following command:</span></span>
   
    ```bash
    sudo waagent -deprovision+user
    ```
<br>
   > [!NOTE]
   > <span data-ttu-id="1b041-126">Tylko Uruchom to polecenie na maszynie Wirtualnej, który ma toocapture jako obraz.</span><span class="sxs-lookup"><span data-stu-id="1b041-126">Only run this command on a VM that you intend toocapture as an image.</span></span> <span data-ttu-id="1b041-127">Nie gwarantuje obrazu hello jest brany pod uwagę wszystkie informacje poufne lub nadaje się do ponownej dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="1b041-127">It does not guarantee that hello image is cleared of all sensitive information or is suitable for redistribution.</span></span> <span data-ttu-id="1b041-128">Witaj *+ użytkownika* parametru spowoduje również usunięcie hello ostatnie konto użytkownika elastycznie.</span><span class="sxs-lookup"><span data-stu-id="1b041-128">hello *+user* parameter also removes hello last provisioned user account.</span></span> <span data-ttu-id="1b041-129">Jeśli poświadczenia konta tookeep w hello maszyny Wirtualnej, należy użyć *-deprovision* tooleave hello konta w miejscu.</span><span class="sxs-lookup"><span data-stu-id="1b041-129">If you want tookeep account credentials in hello VM, just use *-deprovision* tooleave hello user account in place.</span></span>
 
3. <span data-ttu-id="1b041-130">Typ **y** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="1b041-130">Type **y** toocontinue.</span></span> <span data-ttu-id="1b041-131">Możesz dodać hello **-wymusić** tooavoid parametr ten krok potwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="1b041-131">You can add hello **-force** parameter tooavoid this confirmation step.</span></span>
4. <span data-ttu-id="1b041-132">Po zakończeniu wykonywania polecenia hello wpisz **zakończyć**.</span><span class="sxs-lookup"><span data-stu-id="1b041-132">After hello command completes, type **exit**.</span></span> <span data-ttu-id="1b041-133">Ten krok powoduje zamknięcie powitania klienta SSH.</span><span class="sxs-lookup"><span data-stu-id="1b041-133">This step closes hello SSH client.</span></span>

## <a name="step-2-create-vm-image"></a><span data-ttu-id="1b041-134">Krok 2: Tworzenie obrazu maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="1b041-134">Step 2: Create VM image</span></span>
<span data-ttu-id="1b041-135">Jak uogólniony przy użyciu hello Azure CLI 2.0 toomark hello maszyny Wirtualnej, a następnie przechwycić obraz powitania.</span><span class="sxs-lookup"><span data-stu-id="1b041-135">Use hello Azure CLI 2.0 toomark hello VM as generalized and capture hello image.</span></span> <span data-ttu-id="1b041-136">Poniższe przykłady w hello Zastąp przykładowe nazwy parametrów własne wartości.</span><span class="sxs-lookup"><span data-stu-id="1b041-136">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="1b041-137">Przykład nazwy parametru zawierają *myResourceGroup*, *myVnet*, i *myVM*.</span><span class="sxs-lookup"><span data-stu-id="1b041-137">Example parameter names include *myResourceGroup*, *myVnet*, and *myVM*.</span></span>

1. <span data-ttu-id="1b041-138">Cofnięcie przydziału hello maszynę Wirtualną, która anulowana z [deallocate wirtualna az](/cli//azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="1b041-138">Deallocate hello VM that you deprovisioned with [az vm deallocate](/cli//azure/vm#deallocate).</span></span> <span data-ttu-id="1b041-139">Witaj poniższy przykład cofa alokację hello maszyny Wirtualnej o nazwie *myVM* hello grupy zasobów o nazwie *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="1b041-139">hello following example deallocates hello VM named *myVM* in hello resource group named *myResourceGroup*:</span></span>
   
    ```azurecli
    az vm deallocate \
      --resource-group myResourceGroup \
      --name myVM
    ```

2. <span data-ttu-id="1b041-140">Znacznik hello maszyny Wirtualnej, ponieważ uogólniony z [generalize wirtualna az](/cli//azure/vm#generalize).</span><span class="sxs-lookup"><span data-stu-id="1b041-140">Mark hello VM as generalized with [az vm generalize](/cli//azure/vm#generalize).</span></span> <span data-ttu-id="1b041-141">Witaj następujący przykład znaczniki Witaj Witaj maszyny Wirtualnej o nazwie *myVM* hello grupy zasobów o nazwie *myResourceGroup* jako uogólniony:</span><span class="sxs-lookup"><span data-stu-id="1b041-141">hello following example marks hello hello VM named *myVM* in hello resource group named *myResourceGroup* as generalized:</span></span>
   
    ```azurecli
    az vm generalize \
      --resource-group myResourceGroup \
      --name myVM
    ```

3. <span data-ttu-id="1b041-142">Teraz utworzyć obraz powitania zasobu maszyny Wirtualnej z [tworzenia obrazu az](/cli//azure/image#create).</span><span class="sxs-lookup"><span data-stu-id="1b041-142">Now create an image of hello VM resource with [az image create](/cli//azure/image#create).</span></span> <span data-ttu-id="1b041-143">Witaj poniższy przykład tworzy obraz o nazwie *myImage* hello grupy zasobów o nazwie *myResourceGroup* przy użyciu hello zasobu maszyny Wirtualnej o nazwie *myVM*:</span><span class="sxs-lookup"><span data-stu-id="1b041-143">hello following example creates an image named *myImage* in hello resource group named *myResourceGroup* using hello VM resource named *myVM*:</span></span>
   
    ```azurecli
    az image create \
      --resource-group myResourceGroup \
      --name myImage --source myVM
    ```
   
   > [!NOTE]
   > <span data-ttu-id="1b041-144">Witaj obrazu jest tworzony w hello same grupy zasobów jako źródło maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1b041-144">hello image is created in hello same resource group as your source VM.</span></span> <span data-ttu-id="1b041-145">Maszyny wirtualne można tworzyć w dowolnej grupie zasobów w ramach subskrypcji z tego obrazu.</span><span class="sxs-lookup"><span data-stu-id="1b041-145">You can create VMs in any resource group within your subscription from this image.</span></span> <span data-ttu-id="1b041-146">Z punktu widzenia zarządzania możesz toocreate grupy zasobów dla określonych zasobów maszyny Wirtualnej i obrazów.</span><span class="sxs-lookup"><span data-stu-id="1b041-146">From a management perspective, you may wish toocreate a specific resource group for your VM resources and images.</span></span>

## <a name="step-3-create-a-vm-from-hello-captured-image"></a><span data-ttu-id="1b041-147">Krok 3: Tworzenie maszyny Wirtualnej z hello przechwycony obraz</span><span class="sxs-lookup"><span data-stu-id="1b041-147">Step 3: Create a VM from hello captured image</span></span>
<span data-ttu-id="1b041-148">Utwórz maszynę Wirtualną przy użyciu obrazu hello zostały utworzone z [tworzenia maszyny wirtualnej az](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="1b041-148">Create a VM using hello image you created with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="1b041-149">Witaj poniższy przykład tworzy Maszynę wirtualną o nazwie *myVMDeployed* z obrazu hello o nazwie *myImage*:</span><span class="sxs-lookup"><span data-stu-id="1b041-149">hello following example creates a VM named *myVMDeployed* from hello image named *myImage*:</span></span>

```azurecli
az vm create \
   --resource-group myResourceGroup \
   --name myVMDeployed \
   --image myImage\
   --admin-username azureuser \
   --ssh-key-value ~/.ssh/id_rsa.pub
```

### <a name="creating-hello-vm-in-another-resource-group"></a><span data-ttu-id="1b041-150">Tworzenie hello maszyny Wirtualnej w innej grupie zasobów</span><span class="sxs-lookup"><span data-stu-id="1b041-150">Creating hello VM in another resource group</span></span> 

<span data-ttu-id="1b041-151">Maszyny wirtualne można utworzyć na podstawie obrazu w dowolnej grupie zasobów w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="1b041-151">You can create VMs from an image in any resource group within your subscription.</span></span> <span data-ttu-id="1b041-152">toocreate Maszynę wirtualną w innej grupie zasobów niż obraz powitania Określ hello zasobów pełny identyfikator tooyour obrazu.</span><span class="sxs-lookup"><span data-stu-id="1b041-152">toocreate a VM in a different resource group than hello image, specify hello full resource ID tooyour image.</span></span> <span data-ttu-id="1b041-153">Użyj [listy obrazów az](/cli/azure/image#list) tooview listy obrazów.</span><span class="sxs-lookup"><span data-stu-id="1b041-153">Use [az image list](/cli/azure/image#list) tooview a list of images.</span></span> <span data-ttu-id="1b041-154">Witaj danych wyjściowych jest toohello podobnie poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="1b041-154">hello output is similar toohello following example:</span></span>

```json
"id": "/subscriptions/guid/resourceGroups/MYRESOURCEGROUP/providers/Microsoft.Compute/images/myImage",
   "location": "westus",
   "name": "myImage",
```

<span data-ttu-id="1b041-155">Witaj poniższym przykładzie użyto [tworzenia maszyny wirtualnej az](/cli/azure/vm#create) toocreate Maszynę wirtualną w innej grupie zasobów niż obraz źródłowy hello, określając identyfikator zasobu obrazu hello:</span><span class="sxs-lookup"><span data-stu-id="1b041-155">hello following example uses [az vm create](/cli/azure/vm#create) toocreate a VM in a different resource group than hello source image by specifying hello image resource ID:</span></span>

```azurecli
az vm create \
   --resource-group myOtherResourceGroup \
   --name myOtherVMDeployed \
   --image "/subscriptions/guid/resourceGroups/MYRESOURCEGROUP/providers/Microsoft.Compute/images/myImage" \
   --admin-username azureuser \
   --ssh-key-value ~/.ssh/id_rsa.pub
```


## <a name="step-4-verify-hello-deployment"></a><span data-ttu-id="1b041-156">Krok 4: Weryfikowanie wdrażania hello</span><span class="sxs-lookup"><span data-stu-id="1b041-156">Step 4: Verify hello deployment</span></span>

<span data-ttu-id="1b041-157">Teraz SSH toohello maszyny wirtualnej utworzone tooverify hello wdrażania i uruchamiania przy użyciu hello nowej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1b041-157">Now SSH toohello virtual machine you created tooverify hello deployment and start using hello new VM.</span></span> <span data-ttu-id="1b041-158">tooconnect za pośrednictwem protokołu SSH, Znajdź hello adres IP lub nazwa FQDN maszyny wirtualnej z [az maszyny wirtualnej pokazu](/cli/azure/vm#show):</span><span class="sxs-lookup"><span data-stu-id="1b041-158">tooconnect via SSH, find hello IP address or FQDN of your VM with [az vm show](/cli/azure/vm#show):</span></span>

```azurecli
az vm show \
   --resource-group myResourceGroup \
   --name myVMDeployed \
   --show-details
```

## <a name="next-steps"></a><span data-ttu-id="1b041-159">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1b041-159">Next steps</span></span>
<span data-ttu-id="1b041-160">Możesz utworzyć wiele maszyn wirtualnych z obrazu maszyny Wirtualnej źródłowego.</span><span class="sxs-lookup"><span data-stu-id="1b041-160">You can create multiple VMs from your source VM image.</span></span> <span data-ttu-id="1b041-161">Jeśli potrzebujesz toomake zmiany tooyour obrazu:</span><span class="sxs-lookup"><span data-stu-id="1b041-161">If you need toomake changes tooyour image:</span></span> 

- <span data-ttu-id="1b041-162">Utwórz maszynę Wirtualną z obrazu.</span><span class="sxs-lookup"><span data-stu-id="1b041-162">Create a VM from your image.</span></span>
- <span data-ttu-id="1b041-163">Upewnij się, wszystkie aktualizacje i zmiany konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="1b041-163">Make any updates or configuration changes.</span></span>
- <span data-ttu-id="1b041-164">Wykonaj hello ponownie kroki toodeprovision, deallocate generalize i tworzenie obrazu.</span><span class="sxs-lookup"><span data-stu-id="1b041-164">Follow hello steps again toodeprovision, deallocate, generalize, and create an image.</span></span>
- <span data-ttu-id="1b041-165">Skorzystaj z tego nowego obrazu dla przyszłych wdrożeń.</span><span class="sxs-lookup"><span data-stu-id="1b041-165">Use this new image for future deployments.</span></span> <span data-ttu-id="1b041-166">W razie potrzeby usuń hello oryginalnego obrazu.</span><span class="sxs-lookup"><span data-stu-id="1b041-166">If desired, delete hello original image.</span></span>

<span data-ttu-id="1b041-167">Aby uzyskać więcej informacji na temat zarządzania maszyn wirtualnych z hello interfejsu wiersza polecenia, zobacz [Azure CLI 2.0](/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="1b041-167">For more information on managing your VMs with hello CLI, see [Azure CLI 2.0](/cli/azure/overview).</span></span>
