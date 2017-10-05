---
title: "Przechwyć obraz maszyny wirtualnej systemu Linux | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie przechwytywania obrazu opartych na systemie Linux Azure maszyny wirtualnej (VM) utworzone za pomocą klasycznym modelu wdrażania."
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
ms.openlocfilehash: ecde5dd3211bfbb290e6910d7d55136d079c6cf3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-capture-a-classic-linux-virtual-machine-as-an-image"></a><span data-ttu-id="ac93a-103">Jak przechwycić klasyczną maszynę wirtualną z systemem Linux jako obraz</span><span class="sxs-lookup"><span data-stu-id="ac93a-103">How to capture a classic Linux virtual machine as an image</span></span>
> [!IMPORTANT]
> <span data-ttu-id="ac93a-104">Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="ac93a-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="ac93a-105">W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="ac93a-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="ac93a-106">Firma Microsoft zaleca, aby w przypadku większości nowych wdrożeń korzystać z modelu opartego na programie Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ac93a-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="ac93a-107">Dowiedz się, jak [wykonać te kroki przy użyciu modelu usługi Resource Manager](../capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ac93a-107">Learn how to [perform these steps using the Resource Manager model](../capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="ac93a-108">W tym artykule przedstawiono sposób Przechwytywanie klasycznego Azure maszyny wirtualnej (VM) systemem Linux jako obrazu, aby utworzyć pozostałe maszyny wirtualne.</span><span class="sxs-lookup"><span data-stu-id="ac93a-108">This article shows you how to capture a classic Azure virtual machine (VM) running Linux as an image to create other virtual machines.</span></span> <span data-ttu-id="ac93a-109">Ten obraz zawiera dysku systemu operacyjnego i dyskach danych dołączonych do maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ac93a-109">This image includes the OS disk and data disks attached to the VM.</span></span> <span data-ttu-id="ac93a-110">Nie ma wśród nich konfiguracji sieci, dlatego należy skonfigurować, które po utworzeniu maszyny Wirtualnej z obrazu.</span><span class="sxs-lookup"><span data-stu-id="ac93a-110">It doesn't include networking configuration, so you need to configure that when you create the other VM from the image.</span></span>

<span data-ttu-id="ac93a-111">Azure zapisuje obraz w obszarze **obrazów**, oraz wszystkie obrazy zostały przekazane.</span><span class="sxs-lookup"><span data-stu-id="ac93a-111">Azure stores the image under **Images**, along with any images you've uploaded.</span></span> <span data-ttu-id="ac93a-112">Aby uzyskać więcej informacji na temat obrazów, zobacz [o obrazy maszyny wirtualnej na platformie Azure][About Virtual Machine Images in Azure].</span><span class="sxs-lookup"><span data-stu-id="ac93a-112">For more information about images, see [About Virtual Machine Images in Azure][About Virtual Machine Images in Azure].</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="ac93a-113">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="ac93a-113">Before you begin</span></span>
<span data-ttu-id="ac93a-114">Tych krokach przyjęto założenie, że już utworzone przy użyciu klasycznego modelu wdrożenia maszyny Wirtualnej platformy Azure i skonfigurować systemu operacyjnego, w tym dołączanie dowolnego dysku z danymi.</span><span class="sxs-lookup"><span data-stu-id="ac93a-114">These steps assume that you've already created an Azure VM using the Classic deployment model and configured the operating system, including attaching any data disks.</span></span> <span data-ttu-id="ac93a-115">Jeśli musisz utworzyć Maszynę wirtualną, przeczytaj [tworzenie maszyny wirtualnej systemu Linux][How to Create a Linux Virtual Machine].</span><span class="sxs-lookup"><span data-stu-id="ac93a-115">If you need to create a VM, read [How to Create a Linux Virtual Machine][How to Create a Linux Virtual Machine].</span></span>

## <a name="capture-the-virtual-machine"></a><span data-ttu-id="ac93a-116">Przechwytywanie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="ac93a-116">Capture the virtual machine</span></span>
1. <span data-ttu-id="ac93a-117">[Połączenie z maszyną Wirtualną](../mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) przy użyciu klienta SSH wybranych przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ac93a-117">[Connect to the VM](../mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) using an SSH client of your choice.</span></span>
2. <span data-ttu-id="ac93a-118">W oknie SSH wpisz następujące polecenie.</span><span class="sxs-lookup"><span data-stu-id="ac93a-118">In the SSH window, type the following command.</span></span> <span data-ttu-id="ac93a-119">Dane wyjściowe z `waagent` mogą się nieco różnić w zależności od wersji tego narzędzia:</span><span class="sxs-lookup"><span data-stu-id="ac93a-119">The output from `waagent` may vary slightly depending on the version of this utility:</span></span>

    ```bash
    sudo waagent -deprovision+user
    ```

    <span data-ttu-id="ac93a-120">Poprzednie polecenie próbuje wyczyścić systemu i zapewnić ich odpowiednie dla reprovisioning.</span><span class="sxs-lookup"><span data-stu-id="ac93a-120">The preceding command attempts to clean the system and make it suitable for reprovisioning.</span></span> <span data-ttu-id="ac93a-121">Tę operację wykonuje następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="ac93a-121">This operation performs the following tasks:</span></span>

   * <span data-ttu-id="ac93a-122">Usuwa kluczy SSH hosta (jeśli Provisioning.RegenerateSshHostKeyPair "y" w pliku konfiguracji)</span><span class="sxs-lookup"><span data-stu-id="ac93a-122">Removes SSH host keys (if Provisioning.RegenerateSshHostKeyPair is 'y' in the configuration file)</span></span>
   * <span data-ttu-id="ac93a-123">Czyści konfiguracji serwera nazw w /etc/resolv.conf</span><span class="sxs-lookup"><span data-stu-id="ac93a-123">Clears nameserver configuration in /etc/resolv.conf</span></span>
   * <span data-ttu-id="ac93a-124">Usuwa `root` hasło użytkownika w tle/etc / (jeśli Provisioning.DeleteRootPassword "y" w pliku konfiguracji)</span><span class="sxs-lookup"><span data-stu-id="ac93a-124">Removes the `root` user password from /etc/shadow (if Provisioning.DeleteRootPassword is 'y' in the configuration file)</span></span>
   * <span data-ttu-id="ac93a-125">Usunięcie buforowanych dzierżaw klientów DHCP</span><span class="sxs-lookup"><span data-stu-id="ac93a-125">Removes cached DHCP client leases</span></span>
   * <span data-ttu-id="ac93a-126">Zresetowanie nazwy hosta na wartość localhost.localdomain</span><span class="sxs-lookup"><span data-stu-id="ac93a-126">Resets host name to localhost.localdomain</span></span>
   * <span data-ttu-id="ac93a-127">Usuwa konto użytkownika (uzyskane z /var/lib/waagent) udostępniane przez ostatnie **i skojarzone dane**.</span><span class="sxs-lookup"><span data-stu-id="ac93a-127">Deletes the last provisioned user account (obtained from /var/lib/waagent) **and associated data**.</span></span>

     > [!NOTE]
     > <span data-ttu-id="ac93a-128">Cofanie zastrzegania usuwa pliki i dane do "generalize" obrazu.</span><span class="sxs-lookup"><span data-stu-id="ac93a-128">Deprovisioning deletes files and data to "generalize" the image.</span></span> <span data-ttu-id="ac93a-129">To polecenie należy uruchamiać tylko na maszynie Wirtualnej, który ma zostać przechwytywania jako nowy szablon obrazu.</span><span class="sxs-lookup"><span data-stu-id="ac93a-129">Only run this command on a VM that you intend to capture as a new image template.</span></span> <span data-ttu-id="ac93a-130">Nie gwarantuje, że obraz jest wyczyszczone wszystkie informacje poufne lub nadaje się do ponownej dystrybucji osobom trzecim.</span><span class="sxs-lookup"><span data-stu-id="ac93a-130">It does not guarantee that the image is cleared of all sensitive information or is suitable for redistribution to third parties.</span></span>

3. <span data-ttu-id="ac93a-131">Typ **y** aby kontynuować.</span><span class="sxs-lookup"><span data-stu-id="ac93a-131">Type **y** to continue.</span></span> <span data-ttu-id="ac93a-132">Możesz dodać `-force` parametr, aby uniknąć tego kroku potwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="ac93a-132">You can add the `-force` parameter to avoid this confirmation step.</span></span>
4. <span data-ttu-id="ac93a-133">Typ **zakończenia** zamykania klienta SSH.</span><span class="sxs-lookup"><span data-stu-id="ac93a-133">Type **Exit** to close the SSH client.</span></span>

   > [!NOTE]
   > <span data-ttu-id="ac93a-134">Pozostałe kroki założono, że masz już [zainstalowane interfejsu wiersza polecenia Azure](../../../cli-install-nodejs.md) na komputerze klienckim.</span><span class="sxs-lookup"><span data-stu-id="ac93a-134">The remaining steps assume you have already [installed the Azure CLI](../../../cli-install-nodejs.md) on your client computer.</span></span> <span data-ttu-id="ac93a-135">Można również wykonać następujące kroki [portalu Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ac93a-135">All the following steps can also be done in the [Azure portal](http://portal.azure.com).</span></span>

5. <span data-ttu-id="ac93a-136">Na komputerze klienckim otwórz wiersza polecenia platformy Azure i zaloguj się do subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ac93a-136">From your client computer, open Azure CLI and login to your Azure subscription.</span></span> <span data-ttu-id="ac93a-137">Aby uzyskać więcej informacji, przeczytaj [połączenie z subskrypcją platformy Azure z wiersza polecenia platformy Azure](../../../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="ac93a-137">For details, read [Connect to an Azure subscription from the Azure CLI](../../../xplat-cli-connect.md).</span></span>

   > [!NOTE]
   > <span data-ttu-id="ac93a-138">W portalu Azure należy zalogować się do portalu.</span><span class="sxs-lookup"><span data-stu-id="ac93a-138">In the Azure portal, log in to the portal.</span></span>

6. <span data-ttu-id="ac93a-139">Upewnij się, że jesteś w trybie zarządzania usługami:</span><span class="sxs-lookup"><span data-stu-id="ac93a-139">Make sure you are in Service Management mode:</span></span>

    ```azurecli
    azure config mode asm
    ```

7. <span data-ttu-id="ac93a-140">Zamknij maszynę Wirtualną, która jest już anulowana.</span><span class="sxs-lookup"><span data-stu-id="ac93a-140">Shut down the VM that is already deprovisioned.</span></span> <span data-ttu-id="ac93a-141">Poniższy przykład wyłączania maszyny Wirtualnej o nazwie `myVM`:</span><span class="sxs-lookup"><span data-stu-id="ac93a-141">The following example shuts down the VM named `myVM`:</span></span>

    ```azurecli
    azure vm shutdown myVM
    ```
   <span data-ttu-id="ac93a-142">Jeśli to konieczne, można wyświetlić listę wszystkich maszyny wirtualne utworzone w ramach subskrypcji przy użyciu`azure vm list`</span><span class="sxs-lookup"><span data-stu-id="ac93a-142">If needed, you can view a list all the VMs created in your subscription by using `azure vm list`</span></span>

   > [!NOTE]
   > <span data-ttu-id="ac93a-143">Jeśli używasz portalu Azure, wybierz maszynę Wirtualną i kliknij przycisk **zatrzymać** można zamknąć maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ac93a-143">If you're using the Azure portal, select the VM and click **Stop** to shut down the VM.</span></span>

8. <span data-ttu-id="ac93a-144">Po zatrzymaniu maszyny Wirtualnej Przechwyć obraz.</span><span class="sxs-lookup"><span data-stu-id="ac93a-144">When the VM is stopped, capture the image.</span></span> <span data-ttu-id="ac93a-145">Poniższy przykład przechwytuje maszynę Wirtualną o nazwie `myVM` i tworzy uogólniony obraz o nazwie `myNewVM`:</span><span class="sxs-lookup"><span data-stu-id="ac93a-145">The following example captures the VM named `myVM` and creates a generalized image named `myNewVM`:</span></span>

    ```azurecli
    azure vm capture -t myVM myNewVM
    ```

    <span data-ttu-id="ac93a-146">`-t` Podpolecenia Usuwa oryginalny maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ac93a-146">The `-t` subcommand deletes the original virtual machine.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ac93a-147">W portalu Azure, można przechwycić obraz, wybierając **obrazu** w menu Centrum.</span><span class="sxs-lookup"><span data-stu-id="ac93a-147">In the Azure portal, you can capture an image by selecting **Image** from the hub menu.</span></span> <span data-ttu-id="ac93a-148">Należy podać następujące informacje dotyczące obrazu: Nazwa grupy zasobów, lokalizacji, typu systemu operacyjnego i ścieżki do magazynu obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="ac93a-148">You need to supply the following information for the image: name, resource group, location, operating system type, and storage blob path.</span></span>

9. <span data-ttu-id="ac93a-149">Nowy obraz jest teraz dostępny na liście obrazów, które mogą służyć do konfigurowania żadnych nowej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ac93a-149">The new image is now available in the list of images that can be used to configure any new VM.</span></span> <span data-ttu-id="ac93a-150">Możesz je wyświetlić przy użyciu polecenia:</span><span class="sxs-lookup"><span data-stu-id="ac93a-150">You can view it with the command:</span></span>

   ```azurecli
   azure vm image list
   ```

   <span data-ttu-id="ac93a-151">Na [portalu Azure](http://portal.azure.com), nowy obraz zostanie wyświetlony w **obrazów maszyn wirtualnych (klasyczne)** należący do **obliczeniowe** usług.</span><span class="sxs-lookup"><span data-stu-id="ac93a-151">On the [Azure portal](http://portal.azure.com), the new image appears in the **VM images (classic)** that belongs to the **Compute** services.</span></span> <span data-ttu-id="ac93a-152">Dostęp można uzyskać **obrazów maszyn wirtualnych (klasyczne)** , klikając _więcej usług_ w dolnej części platformy Azure Usługa listy, a następnie sprawdzając **obliczeniowe** usług.</span><span class="sxs-lookup"><span data-stu-id="ac93a-152">You can access **VM images (classic)** by clicking _More services_ at the bottom of the Azure service list, and then looking in the **Compute** services.</span></span>   

   ![Pomyślne przechwytywania obrazu](./media/capture-image/VMCapturedImageAvailable.png)

## <a name="next-steps"></a><span data-ttu-id="ac93a-154">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ac93a-154">Next steps</span></span>
<span data-ttu-id="ac93a-155">Obraz jest gotowy do użycia do tworzenia maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="ac93a-155">The image is ready to be used to create VMs.</span></span> <span data-ttu-id="ac93a-156">Możesz użyć polecenia interfejsu wiersza polecenia Azure `azure vm create` i podaj nazwę obraz został utworzony.</span><span class="sxs-lookup"><span data-stu-id="ac93a-156">You can use the Azure CLI command `azure vm create` and supply the image name you created.</span></span> <span data-ttu-id="ac93a-157">Aby uzyskać więcej informacji, zobacz [z klasycznego modelu wdrażania przy użyciu interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="ac93a-157">For more information, see [Using the Azure CLI with Classic deployment model](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span>

<span data-ttu-id="ac93a-158">Można również użyć [portalu Azure](http://portal.azure.com) Tworzenie niestandardowych maszyny Wirtualnej za pomocą **obrazu** — metoda i wybierając obraz został utworzony.</span><span class="sxs-lookup"><span data-stu-id="ac93a-158">Alternatively, use the [Azure portal](http://portal.azure.com) to create a custom VM by using the **Image** method and selecting the image you created.</span></span> <span data-ttu-id="ac93a-159">Aby uzyskać więcej informacji, zobacz [tworzenie maszyny Wirtualnej niestandardowe][How to Create a Custom Virtual Machine].</span><span class="sxs-lookup"><span data-stu-id="ac93a-159">For more information, see [How to Create a Custom VM][How to Create a Custom Virtual Machine].</span></span>

<span data-ttu-id="ac93a-160">**Zobacz też:** [Podręcznik użytkownika Azure agenta systemu Linux](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="ac93a-160">**See also:** [Azure Linux Agent User Guide](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

[About Virtual Machine Images in Azure]:../../virtual-machines-linux-classic-about-images.md
[How to Create a Custom Virtual Machine]:create-custom.md
[How to Attach a Data Disk to a Virtual Machine]:attach-disk.md
[How to Create a Linux Virtual Machine]:create-custom.md
