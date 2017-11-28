---
title: aaaCapture obrazu maszyny wirtualnej systemu Linux | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toocapture obraz opartych na systemie Linux Azure maszynę wirtualną (VM) utworzony z hello klasycznego modelu wdrażania."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 17d7ffee-a58e-4290-9de1-64c3cf1ddc05
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: iainfou
ms.openlocfilehash: 33c4059d5bb919a86bdc3492abca540750f365ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocapture-a-classic-linux-virtual-machine-as-an-image"></a><span data-ttu-id="6b223-103">Jak toocapture klasyczne maszyny wirtualnej systemu Linux jako obrazu</span><span class="sxs-lookup"><span data-stu-id="6b223-103">How toocapture a classic Linux virtual machine as an image</span></span>
> [!IMPORTANT]
> <span data-ttu-id="6b223-104">Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="6b223-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="6b223-105">W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia hello.</span><span class="sxs-lookup"><span data-stu-id="6b223-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="6b223-106">Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="6b223-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="6b223-107">Dowiedz się, jak za[wykonaj te czynności przy użyciu modelu Resource Manager hello](../capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6b223-107">Learn how too[perform these steps using hello Resource Manager model](../capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="6b223-108">W tym artykule opisano sposób toocapture klasycznego Azure maszynę wirtualną (VM) systemem Linux jako obrazu toocreate innych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="6b223-108">This article shows you how toocapture a classic Azure virtual machine (VM) running Linux as an image toocreate other virtual machines.</span></span> <span data-ttu-id="6b223-109">Ten obraz zawiera hello dysku systemu operacyjnego i dysków z danymi dołączone toohello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6b223-109">This image includes hello OS disk and data disks attached toohello VM.</span></span> <span data-ttu-id="6b223-110">Nie ma wśród nich konfiguracji sieci, więc należy tooconfigure które po utworzeniu hello inne maszyny Wirtualnej z obrazu hello.</span><span class="sxs-lookup"><span data-stu-id="6b223-110">It doesn't include networking configuration, so you need tooconfigure that when you create hello other VM from hello image.</span></span>

<span data-ttu-id="6b223-111">Magazyny Azure hello obrazu w obszarze **obrazów**, oraz wszystkie obrazy zostały przekazane.</span><span class="sxs-lookup"><span data-stu-id="6b223-111">Azure stores hello image under **Images**, along with any images you've uploaded.</span></span> <span data-ttu-id="6b223-112">Aby uzyskać więcej informacji na temat obrazów, zobacz [o obrazy maszyny wirtualnej na platformie Azure][About Virtual Machine Images in Azure].</span><span class="sxs-lookup"><span data-stu-id="6b223-112">For more information about images, see [About Virtual Machine Images in Azure][About Virtual Machine Images in Azure].</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="6b223-113">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="6b223-113">Before you begin</span></span>
<span data-ttu-id="6b223-114">Tych krokach przyjęto założenie, że zostało już utworzone przy użyciu klasycznego modelu wdrożenia hello i hello skonfigurowanego systemu operacyjnego, dołączanie wszystkich dysków danych maszyny Wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6b223-114">These steps assume that you've already created an Azure VM using hello Classic deployment model and configured hello operating system, including attaching any data disks.</span></span> <span data-ttu-id="6b223-115">Toocreate maszyny Wirtualnej, należy przeczytać [jak tooCreate maszyny wirtualnej systemu Linux][How tooCreate a Linux Virtual Machine].</span><span class="sxs-lookup"><span data-stu-id="6b223-115">If you need toocreate a VM, read [How tooCreate a Linux Virtual Machine][How tooCreate a Linux Virtual Machine].</span></span>

## <a name="capture-hello-virtual-machine"></a><span data-ttu-id="6b223-116">Przechwytywanie maszyny wirtualnej hello</span><span class="sxs-lookup"><span data-stu-id="6b223-116">Capture hello virtual machine</span></span>
1. <span data-ttu-id="6b223-117">[Połącz toohello wirtualna](../mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) przy użyciu klienta SSH wybranych przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="6b223-117">[Connect toohello VM](../mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) using an SSH client of your choice.</span></span>
2. <span data-ttu-id="6b223-118">W oknie SSH hello wpisz następujące polecenie hello.</span><span class="sxs-lookup"><span data-stu-id="6b223-118">In hello SSH window, type hello following command.</span></span> <span data-ttu-id="6b223-119">Witaj dane wyjściowe z `waagent` mogą się nieco różnić w zależności od wersji hello tego narzędzia:</span><span class="sxs-lookup"><span data-stu-id="6b223-119">hello output from `waagent` may vary slightly depending on hello version of this utility:</span></span>

    ```bash
    sudo waagent -deprovision+user
    ```

    <span data-ttu-id="6b223-120">Witaj poprzednie polecenie prób tooclean hello system i nie była odpowiednia dla reprovisioning.</span><span class="sxs-lookup"><span data-stu-id="6b223-120">hello preceding command attempts tooclean hello system and make it suitable for reprovisioning.</span></span> <span data-ttu-id="6b223-121">Tę operację wykonuje hello następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="6b223-121">This operation performs hello following tasks:</span></span>

   * <span data-ttu-id="6b223-122">Usuwa kluczy SSH hosta (jeśli Provisioning.RegenerateSshHostKeyPair "y" w pliku konfiguracyjnym hello)</span><span class="sxs-lookup"><span data-stu-id="6b223-122">Removes SSH host keys (if Provisioning.RegenerateSshHostKeyPair is 'y' in hello configuration file)</span></span>
   * <span data-ttu-id="6b223-123">Czyści konfiguracji serwera nazw w /etc/resolv.conf</span><span class="sxs-lookup"><span data-stu-id="6b223-123">Clears nameserver configuration in /etc/resolv.conf</span></span>
   * <span data-ttu-id="6b223-124">Usuwa hello `root` hasło użytkownika w tle/etc / (jeśli Provisioning.DeleteRootPassword "y" w pliku konfiguracyjnym hello)</span><span class="sxs-lookup"><span data-stu-id="6b223-124">Removes hello `root` user password from /etc/shadow (if Provisioning.DeleteRootPassword is 'y' in hello configuration file)</span></span>
   * <span data-ttu-id="6b223-125">Usunięcie buforowanych dzierżaw klientów DHCP</span><span class="sxs-lookup"><span data-stu-id="6b223-125">Removes cached DHCP client leases</span></span>
   * <span data-ttu-id="6b223-126">Resetuje hosta toolocalhost.localdomain nazwy</span><span class="sxs-lookup"><span data-stu-id="6b223-126">Resets host name toolocalhost.localdomain</span></span>
   * <span data-ttu-id="6b223-127">Usuwa hello ostatnie konto użytkownika elastycznie (uzyskane z /var/lib/waagent) **i skojarzone dane**.</span><span class="sxs-lookup"><span data-stu-id="6b223-127">Deletes hello last provisioned user account (obtained from /var/lib/waagent) **and associated data**.</span></span>

     > [!NOTE]
     > <span data-ttu-id="6b223-128">Cofanie zastrzegania usuwa pliki i dane za "generalize" hello obrazu.</span><span class="sxs-lookup"><span data-stu-id="6b223-128">Deprovisioning deletes files and data too"generalize" hello image.</span></span> <span data-ttu-id="6b223-129">Tylko Uruchom to polecenie na maszynie Wirtualnej, który ma toocapture jako nowy szablon obrazu.</span><span class="sxs-lookup"><span data-stu-id="6b223-129">Only run this command on a VM that you intend toocapture as a new image template.</span></span> <span data-ttu-id="6b223-130">Nie gwarantuje obrazu hello jest brany pod uwagę wszystkie informacje poufne lub nadaje się do strony toothird ponownej dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="6b223-130">It does not guarantee that hello image is cleared of all sensitive information or is suitable for redistribution toothird parties.</span></span>

3. <span data-ttu-id="6b223-131">Typ **y** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="6b223-131">Type **y** toocontinue.</span></span> <span data-ttu-id="6b223-132">Możesz dodać hello `-force` tooavoid parametr ten krok potwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="6b223-132">You can add hello `-force` parameter tooavoid this confirmation step.</span></span>
4. <span data-ttu-id="6b223-133">Typ **zakończenia** tooclose hello SSH klienta.</span><span class="sxs-lookup"><span data-stu-id="6b223-133">Type **Exit** tooclose hello SSH client.</span></span>

   > [!NOTE]
   > <span data-ttu-id="6b223-134">Witaj pozostałych kroków założono, że masz już [zainstalowane hello Azure CLI](../../../cli-install-nodejs.md) na komputerze klienckim.</span><span class="sxs-lookup"><span data-stu-id="6b223-134">hello remaining steps assume you have already [installed hello Azure CLI](../../../cli-install-nodejs.md) on your client computer.</span></span> <span data-ttu-id="6b223-135">Można również wykonać wszystkie hello następujące kroki w hello [portalu Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6b223-135">All hello following steps can also be done in hello [Azure portal](http://portal.azure.com).</span></span>

5. <span data-ttu-id="6b223-136">Na swoim komputerze klienckim otwórz okno wiersza polecenia platformy Azure i tooyour logowania subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6b223-136">From your client computer, open Azure CLI and login tooyour Azure subscription.</span></span> <span data-ttu-id="6b223-137">Aby uzyskać więcej informacji, przeczytaj [połączyć tooan subskrypcji platformy Azure z hello Azure CLI](../../../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="6b223-137">For details, read [Connect tooan Azure subscription from hello Azure CLI](../../../xplat-cli-connect.md).</span></span>

   > [!NOTE]
   > <span data-ttu-id="6b223-138">W portalu Azure hello Zaloguj się w portalu toohello.</span><span class="sxs-lookup"><span data-stu-id="6b223-138">In hello Azure portal, log in toohello portal.</span></span>

6. <span data-ttu-id="6b223-139">Upewnij się, że jesteś w trybie zarządzania usługami:</span><span class="sxs-lookup"><span data-stu-id="6b223-139">Make sure you are in Service Management mode:</span></span>

    ```azurecli
    azure config mode asm
    ```

7. <span data-ttu-id="6b223-140">Zamknij maszynę Wirtualną, która jest już anulowana hello.</span><span class="sxs-lookup"><span data-stu-id="6b223-140">Shut down hello VM that is already deprovisioned.</span></span> <span data-ttu-id="6b223-141">Witaj poniższy przykład zamyka hello maszyny Wirtualnej o nazwie `myVM`:</span><span class="sxs-lookup"><span data-stu-id="6b223-141">hello following example shuts down hello VM named `myVM`:</span></span>

    ```azurecli
    azure vm shutdown myVM
    ```
   <span data-ttu-id="6b223-142">Jeśli to konieczne, można wyświetlić listę hello wszystkie maszyny wirtualne utworzone w ramach subskrypcji przy użyciu`azure vm list`</span><span class="sxs-lookup"><span data-stu-id="6b223-142">If needed, you can view a list all hello VMs created in your subscription by using `azure vm list`</span></span>

   > [!NOTE]
   > <span data-ttu-id="6b223-143">Jeśli używasz hello portalu Azure wybierz hello maszyny Wirtualnej i kliknij przycisk **zatrzymać** zamknie hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6b223-143">If you're using hello Azure portal, select hello VM and click **Stop** to shut down hello VM.</span></span>

8. <span data-ttu-id="6b223-144">Po zatrzymaniu hello maszyny Wirtualnej Przechwyć obraz powitania.</span><span class="sxs-lookup"><span data-stu-id="6b223-144">When hello VM is stopped, capture hello image.</span></span> <span data-ttu-id="6b223-145">następujące przechwytywania przykład Hello hello maszyny Wirtualnej o nazwie `myVM` i tworzy uogólniony obraz o nazwie `myNewVM`:</span><span class="sxs-lookup"><span data-stu-id="6b223-145">hello following example captures hello VM named `myVM` and creates a generalized image named `myNewVM`:</span></span>

    ```azurecli
    azure vm capture -t myVM myNewVM
    ```

    <span data-ttu-id="6b223-146">Witaj `-t` podpolecenia usuwa hello oryginalna maszyna wirtualna.</span><span class="sxs-lookup"><span data-stu-id="6b223-146">hello `-t` subcommand deletes hello original virtual machine.</span></span>

    > [!NOTE]
    > <span data-ttu-id="6b223-147">W portalu Azure hello, można przechwycić obraz, wybierając **obrazu** menu hello koncentratora.</span><span class="sxs-lookup"><span data-stu-id="6b223-147">In hello Azure portal, you can capture an image by selecting **Image** from hello hub menu.</span></span> <span data-ttu-id="6b223-148">Potrzebujesz następujących informacji o obrazie hello hello toosupply: Nazwa grupy zasobów, lokalizacji, typu systemu operacyjnego i ścieżki do magazynu obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="6b223-148">You need toosupply hello following information for hello image: name, resource group, location, operating system type, and storage blob path.</span></span>

9. <span data-ttu-id="6b223-149">Nowy obraz powitania jest teraz dostępna w hello listy obrazów, które mogą być tooconfigure używanej żadnej nowej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6b223-149">hello new image is now available in hello list of images that can be used tooconfigure any new VM.</span></span> <span data-ttu-id="6b223-150">Możesz je wyświetlić przy użyciu polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="6b223-150">You can view it with hello command:</span></span>

   ```azurecli
   azure vm image list
   ```

   <span data-ttu-id="6b223-151">Na powitania [portalu Azure](http://portal.azure.com), w hello pojawi się nowy obraz powitania **obrazów maszyn wirtualnych (klasyczne)** należący toohello **obliczeniowe** usług.</span><span class="sxs-lookup"><span data-stu-id="6b223-151">On hello [Azure portal](http://portal.azure.com), hello new image appears in hello **VM images (classic)** that belongs toohello **Compute** services.</span></span> <span data-ttu-id="6b223-152">Dostęp można uzyskać **obrazów maszyn wirtualnych (klasyczne)** klikając _więcej usług_ u dołu hello hello Azure Usługa listy, a następnie sprawdzając w hello **obliczeniowe** usług.</span><span class="sxs-lookup"><span data-stu-id="6b223-152">You can access **VM images (classic)** by clicking _More services_ at hello bottom of hello Azure service list, and then looking in hello **Compute** services.</span></span>   

   ![Pomyślne przechwytywania obrazu](./media/capture-image/VMCapturedImageAvailable.png)

## <a name="next-steps"></a><span data-ttu-id="6b223-154">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6b223-154">Next steps</span></span>
<span data-ttu-id="6b223-155">Obraz powitania jest gotowy toobe używane toocreate maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="6b223-155">hello image is ready toobe used toocreate VMs.</span></span> <span data-ttu-id="6b223-156">Możesz użyć polecenia interfejsu wiersza polecenia Azure hello `azure vm create` i nazwa obrazu hello dostaw został utworzony.</span><span class="sxs-lookup"><span data-stu-id="6b223-156">You can use hello Azure CLI command `azure vm create` and supply hello image name you created.</span></span> <span data-ttu-id="6b223-157">Aby uzyskać więcej informacji, zobacz [hello Using Azure CLI z klasycznego modelu wdrożenia](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="6b223-157">For more information, see [Using hello Azure CLI with Classic deployment model](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span>

<span data-ttu-id="6b223-158">Można również użyć hello [portalu Azure](http://portal.azure.com) toocreate niestandardowych maszyny Wirtualnej za pomocą hello **obrazu** — metoda i wybierając hello obrazu utworzonego.</span><span class="sxs-lookup"><span data-stu-id="6b223-158">Alternatively, use hello [Azure portal](http://portal.azure.com) toocreate a custom VM by using hello **Image** method and selecting hello image you created.</span></span> <span data-ttu-id="6b223-159">Aby uzyskać więcej informacji, zobacz [jak tooCreate wirtualna niestandardowe][How tooCreate a Custom Virtual Machine].</span><span class="sxs-lookup"><span data-stu-id="6b223-159">For more information, see [How tooCreate a Custom VM][How tooCreate a Custom Virtual Machine].</span></span>

<span data-ttu-id="6b223-160">**Zobacz też:** [Podręcznik użytkownika Azure agenta systemu Linux](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="6b223-160">**See also:** [Azure Linux Agent User Guide](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

[About Virtual Machine Images in Azure]:../../virtual-machines-linux-classic-about-images.md
[How tooCreate a Custom Virtual Machine]:create-custom.md
[How tooAttach a Data Disk tooa Virtual Machine]:attach-disk.md
[How tooCreate a Linux Virtual Machine]:create-custom.md
