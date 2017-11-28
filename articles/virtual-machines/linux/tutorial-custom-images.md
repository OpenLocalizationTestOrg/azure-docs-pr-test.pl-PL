---
title: "aaaCreate niestandardowych obrazów maszyn wirtualnych z hello Azure CLI | Dokumentacja firmy Microsoft"
description: "Samouczek — Tworzenie niestandardowego obrazu maszyny Wirtualnej przy użyciu hello wiersza polecenia platformy Azure."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/21/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 217a993c0c1d48939b74108ac6c5f7a1a619416c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-of-an-azure-vm-using-hello-cli"></a><span data-ttu-id="1de13-103">Tworzenie niestandardowego obrazu maszyny Wirtualnej platformy Azure przy użyciu hello interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="1de13-103">Create a custom image of an Azure VM using hello CLI</span></span>

<span data-ttu-id="1de13-104">Niestandardowe obrazy są takie jak obrazy marketplace, ale można je utworzyć samodzielnie.</span><span class="sxs-lookup"><span data-stu-id="1de13-104">Custom images are like marketplace images, but you create them yourself.</span></span> <span data-ttu-id="1de13-105">Niestandardowe obrazy mogą być używane toobootstrap konfiguracje, takie jak wstępnego ładowania aplikacji, konfiguracji aplikacji i inne konfiguracje systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="1de13-105">Custom images can be used toobootstrap configurations such as preloading applications, application configurations, and other OS configurations.</span></span> <span data-ttu-id="1de13-106">W tym samouczku utworzysz własnego niestandardowego obrazu maszyny wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1de13-106">In this tutorial, you create your own custom image of an Azure virtual machine.</span></span> <span data-ttu-id="1de13-107">Omawiane kwestie:</span><span class="sxs-lookup"><span data-stu-id="1de13-107">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1de13-108">Anulowanie zastrzeżenia i generalize maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="1de13-108">Deprovision and generalize VMs</span></span>
> * <span data-ttu-id="1de13-109">Tworzenie obrazu niestandardowego</span><span class="sxs-lookup"><span data-stu-id="1de13-109">Create a custom image</span></span>
> * <span data-ttu-id="1de13-110">Utwórz maszynę Wirtualną z obrazu niestandardowego</span><span class="sxs-lookup"><span data-stu-id="1de13-110">Create a VM from a custom image</span></span>
> * <span data-ttu-id="1de13-111">Wyświetlanie listy wszystkich obrazów hello w ramach subskrypcji</span><span class="sxs-lookup"><span data-stu-id="1de13-111">List all hello images in your subscription</span></span>
> * <span data-ttu-id="1de13-112">Usuń obraz</span><span class="sxs-lookup"><span data-stu-id="1de13-112">Delete an image</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="1de13-113">Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym samouczku wymaga działają hello Azure CLI w wersji 2.0.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="1de13-113">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="1de13-114">Uruchom `az --version` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="1de13-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="1de13-115">Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="1de13-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="1de13-116">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="1de13-116">Before you begin</span></span>

<span data-ttu-id="1de13-117">Poniższe kroki Hello szczegółowo tootake istniejącej maszyny Wirtualnej i włącz go do wielokrotnego użytku niestandardowego obrazu, który służy toocreate nowych wystąpień maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1de13-117">hello steps below detail how tootake an existing VM and turn it into a re-usable custom image that you can use toocreate new VM instances.</span></span>

<span data-ttu-id="1de13-118">przykład Witaj toocomplete w tym samouczku, musi mieć istniejącej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1de13-118">toocomplete hello example in this tutorial, you must have an existing virtual machine.</span></span> <span data-ttu-id="1de13-119">Jeśli to konieczne, to [przykładowym skrypcie](../scripts/virtual-machines-linux-cli-sample-create-vm-nginx.md) można utworzyć.</span><span class="sxs-lookup"><span data-stu-id="1de13-119">If needed, this [script sample](../scripts/virtual-machines-linux-cli-sample-create-vm-nginx.md) can create one for you.</span></span> <span data-ttu-id="1de13-120">Podczas pracy nad hello samouczek, Zastąp maszyny Wirtualnej i grupy zasobów hello nazwy w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="1de13-120">When working through hello tutorial, replace hello resource group and VM names where needed.</span></span>

## <a name="create-a-custom-image"></a><span data-ttu-id="1de13-121">Tworzenie obrazu niestandardowego</span><span class="sxs-lookup"><span data-stu-id="1de13-121">Create a custom image</span></span>

<span data-ttu-id="1de13-122">toocreate obrazu maszyny wirtualnej, należy tooprepare hello wirtualna anulowania obsługi, dealokowanie, a następnie oznaczenie hello źródłowej maszyny Wirtualnej, ponieważ uogólniony.</span><span class="sxs-lookup"><span data-stu-id="1de13-122">toocreate an image of a virtual machine, you need tooprepare hello VM by deprovisioning, deallocating, and then marking hello source VM as generalized.</span></span> <span data-ttu-id="1de13-123">Raz hello, który został przygotowany maszyny Wirtualnej, można utworzyć obrazu.</span><span class="sxs-lookup"><span data-stu-id="1de13-123">Once hello VM has been prepared, you can create an image.</span></span>

### <a name="deprovision-hello-vm"></a><span data-ttu-id="1de13-124">Anulowanie zastrzeżenia hello maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="1de13-124">Deprovision hello VM</span></span> 

<span data-ttu-id="1de13-125">Cofanie zastrzegania stanowi uogólnienie hello maszyny Wirtualnej przez usunięcie informacji na temat określonego komputera.</span><span class="sxs-lookup"><span data-stu-id="1de13-125">Deprovisioning generalizes hello VM by removing machine-specific information.</span></span> <span data-ttu-id="1de13-126">To generalizacji ułatwia toodeploy możliwych wiele maszyn wirtualnych za pomocą pojedynczego obrazu.</span><span class="sxs-lookup"><span data-stu-id="1de13-126">This generalization makes it possible toodeploy many VMs from a single image.</span></span> <span data-ttu-id="1de13-127">Podczas anulowania obsługi, nazwa hosta hello jest resetowany zbyt*localhost.localdomain*.</span><span class="sxs-lookup"><span data-stu-id="1de13-127">During deprovisioning, hello host name is reset too*localhost.localdomain*.</span></span> <span data-ttu-id="1de13-128">Klucze hosta SSH, konfiguracje wskazują hasła głównego i buforowanych dzierżaw DHCP również są usuwane.</span><span class="sxs-lookup"><span data-stu-id="1de13-128">SSH host keys, nameserver configurations, root password, and cached DHCP leases are also deleted.</span></span>

<span data-ttu-id="1de13-129">Witaj toodeprovision maszyny Wirtualnej, użyj agenta maszyny Wirtualnej Azure hello (agenta waagent).</span><span class="sxs-lookup"><span data-stu-id="1de13-129">toodeprovision hello VM, use hello Azure VM agent (waagent).</span></span> <span data-ttu-id="1de13-130">agent maszyny Wirtualnej Azure Hello jest zainstalowany na powitania maszyny Wirtualnej i zarządza interakcji z hello Kontroler sieci szkieletowej Azure i udostępniania.</span><span class="sxs-lookup"><span data-stu-id="1de13-130">hello Azure VM agent is installed on hello VM and manages provisioning and interacting with hello Azure Fabric Controller.</span></span> <span data-ttu-id="1de13-131">Aby uzyskać więcej informacji, zobacz hello [Podręcznik użytkownika agenta systemu Linux Azure](agent-user-guide.md).</span><span class="sxs-lookup"><span data-stu-id="1de13-131">For more information, see hello [Azure Linux Agent user guide](agent-user-guide.md).</span></span>

<span data-ttu-id="1de13-132">Połącz tooyour maszyny Wirtualnej przy użyciu protokołu SSH i hello Uruchom polecenie toodeprovision hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1de13-132">Connect tooyour VM using SSH and run hello command toodeprovision hello VM.</span></span> <span data-ttu-id="1de13-133">Z hello `+user` argument, hello ostatnie konto użytkownika elastycznie i wszelkie powiązane dane, również zostaną usunięte.</span><span class="sxs-lookup"><span data-stu-id="1de13-133">With hello `+user` argument, hello last provisioned user account and any associated data are also deleted.</span></span> <span data-ttu-id="1de13-134">Zamień adres IP przykład hello hello publicznego adresu IP maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1de13-134">Replace hello example IP address with hello public IP address of your VM.</span></span>

<span data-ttu-id="1de13-135">Toohello SSH maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1de13-135">SSH toohello VM.</span></span>
```bash
ssh azureuser@52.174.34.95
```
<span data-ttu-id="1de13-136">Anulowanie zastrzeżenia hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1de13-136">Deprovision hello VM.</span></span>

```bash
sudo waagent -deprovision+user -force
```
<span data-ttu-id="1de13-137">Zamknij sesję SSH hello.</span><span class="sxs-lookup"><span data-stu-id="1de13-137">Close hello SSH session.</span></span>

```bash
exit
```

### <a name="deallocate-and-mark-hello-vm-as-generalized"></a><span data-ttu-id="1de13-138">Cofnięcie przydziału i oznacz hello maszyny Wirtualnej, ponieważ uogólniony</span><span class="sxs-lookup"><span data-stu-id="1de13-138">Deallocate and mark hello VM as generalized</span></span>

<span data-ttu-id="1de13-139">toocreate obraz powitania maszyny Wirtualnej musi toobe alokację.</span><span class="sxs-lookup"><span data-stu-id="1de13-139">toocreate an image, hello VM needs toobe deallocated.</span></span> <span data-ttu-id="1de13-140">Cofnięcie przydziału hello maszynę Wirtualną przy użyciu [deallocate wirtualna az](/cli//azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="1de13-140">Deallocate hello VM using [az vm deallocate](/cli//azure/vm#deallocate).</span></span> 
   
```azurecli-interactive 
az vm deallocate --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="1de13-141">Wreszcie, Ustaw stan hello hello maszyny Wirtualnej jako uogólniony z [generalize wirtualna az](/cli//azure/vm#generalize) wówczas hello platformy Azure traktował hello maszyny Wirtualnej został uogólniony.</span><span class="sxs-lookup"><span data-stu-id="1de13-141">Finally, set hello state of hello VM as generalized with [az vm generalize](/cli//azure/vm#generalize) so hello Azure platform knows hello VM has been generalized.</span></span> <span data-ttu-id="1de13-142">Można tworzyć tylko obraz z ogólnych maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1de13-142">You can only create an image from a generalized VM.</span></span>
   
```azurecli-interactive 
az vm generalize --resource-group myResourceGroup --name myVM
```

### <a name="create-hello-image"></a><span data-ttu-id="1de13-143">Utworzyć obraz powitania</span><span class="sxs-lookup"><span data-stu-id="1de13-143">Create hello image</span></span>

<span data-ttu-id="1de13-144">Teraz można utworzyć obraz powitania maszyny Wirtualnej za pomocą [tworzenia obrazu az](/cli//azure/image#create).</span><span class="sxs-lookup"><span data-stu-id="1de13-144">Now you can create an image of hello VM by using [az image create](/cli//azure/image#create).</span></span> <span data-ttu-id="1de13-145">Witaj poniższy przykład tworzy obraz o nazwie *myImage* z maszyny Wirtualnej o nazwie *myVM*.</span><span class="sxs-lookup"><span data-stu-id="1de13-145">hello following example creates an image named *myImage* from a VM named *myVM*.</span></span>
   
```azurecli-interactive 
az image create \
    --resource-group myResourceGroup \
    --name myImage \
    --source myVM
```
 
## <a name="create-vms-from-hello-image"></a><span data-ttu-id="1de13-146">Tworzenie maszyn wirtualnych z hello obrazu</span><span class="sxs-lookup"><span data-stu-id="1de13-146">Create VMs from hello image</span></span>

<span data-ttu-id="1de13-147">Teraz, gdy masz obrazu można utworzyć jeden lub więcej nowych maszyn wirtualnych na podstawie hello obrazu przy użyciu [tworzenia maszyny wirtualnej az](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="1de13-147">Now that you have an image, you can create one or more new VMs from hello image using [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="1de13-148">Witaj poniższy przykład tworzy Maszynę wirtualną o nazwie *myVMfromImage* z obrazu hello o nazwie *myImage*.</span><span class="sxs-lookup"><span data-stu-id="1de13-148">hello following example creates a VM named *myVMfromImage* from hello image named *myImage*.</span></span>

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroup \
    --name myVMfromImage \
    --image myImage \
    --admin-username azureuser \
    --generate-ssh-keys
```

## <a name="image-management"></a><span data-ttu-id="1de13-149">Zarządzanie obrazami</span><span class="sxs-lookup"><span data-stu-id="1de13-149">Image management</span></span> 

<span data-ttu-id="1de13-150">Oto kilka przykładów typowych zadań zarządzania obrazu i w jaki sposób toocomplete ich przy użyciu hello wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1de13-150">Here are some examples of common image management tasks and how toocomplete them using hello Azure CLI.</span></span>

<span data-ttu-id="1de13-151">Wyświetl listę wszystkich obrazów według nazwy w formacie tabeli.</span><span class="sxs-lookup"><span data-stu-id="1de13-151">List all images by name in a table format.</span></span>

```azurecli-interactive 
az image list \
  --resource-group myResourceGroup
```

<span data-ttu-id="1de13-152">Usuń obraz.</span><span class="sxs-lookup"><span data-stu-id="1de13-152">Delete an image.</span></span> <span data-ttu-id="1de13-153">W tym przykładzie usuwa hello obrazu o nazwie *myOldImage* z hello *myResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="1de13-153">This example deletes hello image named *myOldImage* from hello *myResourceGroup*.</span></span>

```azurecli-interactive 
az image delete \
    --name myOldImage \
    --resource-group myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="1de13-154">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1de13-154">Next steps</span></span>

<span data-ttu-id="1de13-155">W tym samouczku utworzony niestandardowy obraz maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1de13-155">In this tutorial, you created a custom VM image.</span></span> <span data-ttu-id="1de13-156">W tym samouczku omówiono:</span><span class="sxs-lookup"><span data-stu-id="1de13-156">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1de13-157">Anulowanie zastrzeżenia i generalize maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="1de13-157">Deprovision and generalize VMs</span></span>
> * <span data-ttu-id="1de13-158">Tworzenie obrazu niestandardowego</span><span class="sxs-lookup"><span data-stu-id="1de13-158">Create a custom image</span></span>
> * <span data-ttu-id="1de13-159">Utwórz maszynę Wirtualną z obrazu niestandardowego</span><span class="sxs-lookup"><span data-stu-id="1de13-159">Create a VM from a custom image</span></span>
> * <span data-ttu-id="1de13-160">Wyświetlanie listy wszystkich obrazów hello w ramach subskrypcji</span><span class="sxs-lookup"><span data-stu-id="1de13-160">List all hello images in your subscription</span></span>
> * <span data-ttu-id="1de13-161">Usuń obraz</span><span class="sxs-lookup"><span data-stu-id="1de13-161">Delete an image</span></span>

<span data-ttu-id="1de13-162">Przejdź dalej toolearn samouczka toohello o wysokiej dostępności maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1de13-162">Advance toohello next tutorial toolearn about highly available virtual machines.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="1de13-163">[Tworzenie maszyn wirtualnych wysokiej dostępności](tutorial-availability-sets.md).</span><span class="sxs-lookup"><span data-stu-id="1de13-163">[Create highly available VMs](tutorial-availability-sets.md).</span></span>

