---
title: "aaaReset dostępu tooan Azure maszyny Wirtualnej systemu Linux | Dokumentacja firmy Microsoft"
description: "Jak toomanage użytkowników i resetowania dostęp do maszyn wirtualnych systemu Linux przy użyciu rozszerzenia VMAccess hello i hello Azure CLI 2.0"
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 261a9646-1f93-407e-951e-0be7226b3064
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 08/04/2017
ms.author: danlep
ms.openlocfilehash: 2f8db01b9fac20bf547d8b1926e5c0b3c5d18280
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-users-ssh-and-check-or-repair-disks-on-linux-vms-using-hello-vmaccess-extension-with-hello-azure-cli-20"></a><span data-ttu-id="04e7d-103">Zarządzanie użytkownikami, SSH i wyboru lub naprawy dysków na maszynach wirtualnych systemu Linux przy użyciu hello rozszerzenia VMAccess z hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="04e7d-103">Manage users, SSH, and check or repair disks on Linux VMs using hello VMAccess Extension with hello Azure CLI 2.0</span></span>
<span data-ttu-id="04e7d-104">Witaj dysku na maszynie Wirtualnej systemu Linux są pokazywane błędy.</span><span class="sxs-lookup"><span data-stu-id="04e7d-104">hello disk on your Linux VM is showing errors.</span></span> <span data-ttu-id="04e7d-105">Jakiś sposób resetowania hasła użytkownika root hello dla maszyny Wirtualnej systemu Linux lub przypadkowo usunięty klucz prywatny SSH.</span><span class="sxs-lookup"><span data-stu-id="04e7d-105">You somehow reset hello root password for your Linux VM or accidentally deleted your SSH private key.</span></span> <span data-ttu-id="04e7d-106">Jeśli który wystąpił w dni hello hello centrum danych, będzie konieczne toodrive, a następnie otwórz tooget KVM hello na powitania serwera konsoli.</span><span class="sxs-lookup"><span data-stu-id="04e7d-106">If that happened back in hello days of hello datacenter, you would need toodrive there and then open hello KVM tooget at hello server console.</span></span> <span data-ttu-id="04e7d-107">Witaj rozszerzenia Azure VMAccess można traktować jako przełącznika KVM, które pozwala tooaccess hello konsoli tooreset dostępu tooLinux przeprowadzania konserwacji poziomu dysku.</span><span class="sxs-lookup"><span data-stu-id="04e7d-107">Think of hello Azure VMAccess extension as that KVM switch that allows you tooaccess hello console tooreset access tooLinux or perform disk level maintenance.</span></span>

<span data-ttu-id="04e7d-108">W tym artykule opisano, jak toouse hello Azure rozszerzenia VMAccess toocheck lub naprawiania dysku, zresetuj dostęp użytkownika, zarządzanie kontami użytkowników lub zresetowanie konfiguracji SSH hello w systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="04e7d-108">This article shows you how toouse hello Azure VMAccess Extension toocheck or repair a disk, reset user access, manage user accounts, or reset hello SSH configuration on Linux.</span></span> <span data-ttu-id="04e7d-109">Można również wykonać te kroki hello [Azure CLI 1.0](using-vmaccess-extension-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="04e7d-109">You can also perform these steps with hello [Azure CLI 1.0](using-vmaccess-extension-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="ways-toouse-hello-vmaccess-extension"></a><span data-ttu-id="04e7d-110">Sposoby toouse hello rozszerzenia VMAccess</span><span class="sxs-lookup"><span data-stu-id="04e7d-110">Ways toouse hello VMAccess Extension</span></span>
<span data-ttu-id="04e7d-111">Istnieją dwa sposoby, w których można używać hello rozszerzenia VMAccess na maszyny wirtualne systemu Linux:</span><span class="sxs-lookup"><span data-stu-id="04e7d-111">There are two ways that you can use hello VMAccess Extension on your Linux VMs:</span></span>

* <span data-ttu-id="04e7d-112">Użyj hello Azure CLI 2.0 i hello wymaganych parametrów.</span><span class="sxs-lookup"><span data-stu-id="04e7d-112">Use hello Azure CLI 2.0 and hello required parameters.</span></span>
* <span data-ttu-id="04e7d-113">[Użyj nieprzetworzone dane JSON pliki tego procesu rozszerzenia VMAccess hello](#use-json-files-and-the-vmaccess-extension) i działa na.</span><span class="sxs-lookup"><span data-stu-id="04e7d-113">[Use raw JSON files that hello VMAccess Extension process](#use-json-files-and-the-vmaccess-extension) and then act on.</span></span>

<span data-ttu-id="04e7d-114">Witaj, następujące przykłady użycia [użytkownika maszyny wirtualnej az](/cli/azure/vm/user) poleceń.</span><span class="sxs-lookup"><span data-stu-id="04e7d-114">hello following examples use [az vm user](/cli/azure/vm/user) commands.</span></span> <span data-ttu-id="04e7d-115">tooperform tych kroków, należy hello najnowszych [Azure CLI 2.0](/cli/azure/install-az-cli2) zainstalowane i zarejestrowane za pomocą konta Azure tooan [logowania az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="04e7d-115">tooperform these steps, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

## <a name="reset-ssh-key"></a><span data-ttu-id="04e7d-116">Resetuj klucz SSH</span><span class="sxs-lookup"><span data-stu-id="04e7d-116">Reset SSH key</span></span>
<span data-ttu-id="04e7d-117">Witaj poniższy przykład resetuje hello klucza SSH dla użytkownika hello `azureuser` na powitania maszyny Wirtualnej o nazwie `myVM`:</span><span class="sxs-lookup"><span data-stu-id="04e7d-117">hello following example resets hello SSH key for hello user `azureuser` on hello VM named `myVM`:</span></span>

```azurecli
az vm user update \
  --resource-group myResourceGroup \
  --name myVM \
  --username azureuser \
  --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="reset-password"></a><span data-ttu-id="04e7d-118">Resetowanie hasła</span><span class="sxs-lookup"><span data-stu-id="04e7d-118">Reset password</span></span>
<span data-ttu-id="04e7d-119">Witaj poniższy przykład resetuje hello hasło dla użytkownika hello `azureuser` na powitania maszyny Wirtualnej o nazwie `myVM`:</span><span class="sxs-lookup"><span data-stu-id="04e7d-119">hello following example resets hello password for hello user `azureuser` on hello VM named `myVM`:</span></span>

```azurecli
az vm user update \
  --resource-group myResourceGroup \
  --name myVM \
  --username azureuser \
  --password myNewPassword
```

## <a name="restart-ssh"></a><span data-ttu-id="04e7d-120">Uruchom ponownie SSH</span><span class="sxs-lookup"><span data-stu-id="04e7d-120">Restart SSH</span></span>
<span data-ttu-id="04e7d-121">Witaj poniższym przykładzie zostanie ponownie uruchomiony demon SSH hello i resetuje hello wartości toodefault konfiguracji SSH maszyny wirtualnej o nazwie `myVM`:</span><span class="sxs-lookup"><span data-stu-id="04e7d-121">hello following example restarts hello SSH daemon and resets hello SSH configuration toodefault values on a VM named `myVM`:</span></span>

```azurecli
az vm user reset-ssh \
  --resource-group myResourceGroup \
  --name myVM
```

## <a name="create-a-user"></a><span data-ttu-id="04e7d-122">Utwórz użytkownika</span><span class="sxs-lookup"><span data-stu-id="04e7d-122">Create a user</span></span>
<span data-ttu-id="04e7d-123">Witaj poniższy przykład tworzy użytkownika o nazwie `myNewUser` przy użyciu klucza SSH do uwierzytelniania na powitania maszyny Wirtualnej o nazwie `myVM`:</span><span class="sxs-lookup"><span data-stu-id="04e7d-123">hello following example creates a user named `myNewUser` using an SSH key for authentication on hello VM named `myVM`:</span></span>

```azurecli
az vm user update \
  --resource-group myResourceGroup \
  --name myVM \
  --username myNewUser \
  --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="delete-a-user"></a><span data-ttu-id="04e7d-124">Usuń użytkownika</span><span class="sxs-lookup"><span data-stu-id="04e7d-124">Delete a user</span></span>
<span data-ttu-id="04e7d-125">Witaj poniższy przykład powoduje usunięcie użytkownika o nazwie `myNewUser` na powitania maszyny Wirtualnej o nazwie `myVM`:</span><span class="sxs-lookup"><span data-stu-id="04e7d-125">hello following example deletes a user named `myNewUser` on hello VM named `myVM`:</span></span>

```azurecli
az vm user delete \
  --resource-group myResourceGroup \
  --name myVM \
  --username myNewUser
```


## <a name="use-json-files-and-hello-vmaccess-extension"></a><span data-ttu-id="04e7d-126">Użyj pliki w formacie JSON i hello rozszerzenia VMAccess</span><span class="sxs-lookup"><span data-stu-id="04e7d-126">Use JSON files and hello VMAccess Extension</span></span>
<span data-ttu-id="04e7d-127">Następujące przykłady Hello Użyj nieprzetworzone pliki w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="04e7d-127">hello following examples use raw JSON files.</span></span> <span data-ttu-id="04e7d-128">Użyj [zestaw rozszerzenia maszyny wirtualnej az](/cli/azure/vm/extension#set) toothen wywołać pliki w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="04e7d-128">Use [az vm extension set](/cli/azure/vm/extension#set) toothen call your JSON files.</span></span> <span data-ttu-id="04e7d-129">Te pliki w formacie JSON również może być wywołana z szablonów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="04e7d-129">These JSON files can also be called from Azure templates.</span></span> 

### <a name="reset-user-access"></a><span data-ttu-id="04e7d-130">Zresetuj dostęp użytkownika</span><span class="sxs-lookup"><span data-stu-id="04e7d-130">Reset user access</span></span>
<span data-ttu-id="04e7d-131">W przypadku utraty dostępu tooroot na maszynie Wirtualnej systemu Linux, możesz uruchomić tooreset skryptu VMAccess klucza SSH użytkownika lub hasło.</span><span class="sxs-lookup"><span data-stu-id="04e7d-131">If you have lost access tooroot on your Linux VM, you can launch a VMAccess script tooreset a user's SSH key or password.</span></span>

<span data-ttu-id="04e7d-132">klucz publiczny SSH hello tooreset użytkownika, Utwórz plik o nazwie `reset_ssh_key.json` i dodać ustawienia hello zgodny z formatem.</span><span class="sxs-lookup"><span data-stu-id="04e7d-132">tooreset hello SSH public key of a user, create a file named `reset_ssh_key.json` and add settings in hello following format.</span></span> <span data-ttu-id="04e7d-133">Podstaw wartości dla hello `username` i `ssh_key` parametry:</span><span class="sxs-lookup"><span data-stu-id="04e7d-133">Substitute your own values for hello `username` and `ssh_key` parameters:</span></span>

```json
{
  "username":"azureuser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNGxxxxxx2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7xxxxxxwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5wxxtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== azureuser@myVM"
}
```

<span data-ttu-id="04e7d-134">Wykonanie skryptu VMAccess hello:</span><span class="sxs-lookup"><span data-stu-id="04e7d-134">Execute hello VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings reset_ssh_key.json
```

<span data-ttu-id="04e7d-135">tooreset hasło użytkownika, Utwórz plik o nazwie `reset_user_password.json` i dodać ustawienia hello zgodny z formatem.</span><span class="sxs-lookup"><span data-stu-id="04e7d-135">tooreset a user password, create a file named `reset_user_password.json` and add settings in hello following format.</span></span> <span data-ttu-id="04e7d-136">Podstaw wartości dla hello `username` i `password` parametry:</span><span class="sxs-lookup"><span data-stu-id="04e7d-136">Substitute your own values for hello `username` and `password` parameters:</span></span>

```json
{
  "username":"azureuser",
  "password":"myNewPassword" 
}
```

<span data-ttu-id="04e7d-137">Wykonanie skryptu VMAccess hello:</span><span class="sxs-lookup"><span data-stu-id="04e7d-137">Execute hello VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings reset_user_password.json
```

### <a name="restart-ssh"></a><span data-ttu-id="04e7d-138">Uruchom ponownie SSH</span><span class="sxs-lookup"><span data-stu-id="04e7d-138">Restart SSH</span></span>
<span data-ttu-id="04e7d-139">toorestart hello demon SSH i resetowania wartości toodefault konfiguracji SSH hello, Utwórz plik o nazwie `reset_sshd.json`.</span><span class="sxs-lookup"><span data-stu-id="04e7d-139">toorestart hello SSH daemon and reset hello SSH configuration toodefault values, create a file named `reset_sshd.json`.</span></span> <span data-ttu-id="04e7d-140">Dodaj hello następującej zawartości:</span><span class="sxs-lookup"><span data-stu-id="04e7d-140">Add hello following content:</span></span>

```json
{
  "reset_ssh": true
}
```

<span data-ttu-id="04e7d-141">Wykonanie skryptu VMAccess hello:</span><span class="sxs-lookup"><span data-stu-id="04e7d-141">Execute hello VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings reset_sshd.json
```

### <a name="manage-users"></a><span data-ttu-id="04e7d-142">Zarządzanie użytkownikami</span><span class="sxs-lookup"><span data-stu-id="04e7d-142">Manage users</span></span>

<span data-ttu-id="04e7d-143">toocreate użytkownika, który używa klucza SSH do uwierzytelnienia, Utwórz plik o nazwie `create_new_user.json` i dodać ustawienia hello zgodny z formatem.</span><span class="sxs-lookup"><span data-stu-id="04e7d-143">toocreate a user that uses an SSH key for authentication, create a file named `create_new_user.json` and add settings in hello following format.</span></span> <span data-ttu-id="04e7d-144">Podstaw wartości dla hello `username` i `ssh_key` parametry:</span><span class="sxs-lookup"><span data-stu-id="04e7d-144">Substitute your own values for hello `username` and `ssh_key` parameters:</span></span>

```json
{
  "username":"myNewUser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNG1vHY7P2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7iUo5IdwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5woYtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== myNewUser@myVM",
  "password":"myNewUserPassword"
}
```

<span data-ttu-id="04e7d-145">Wykonanie skryptu VMAccess hello:</span><span class="sxs-lookup"><span data-stu-id="04e7d-145">Execute hello VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings create_new_user.json
```

<span data-ttu-id="04e7d-146">toodelete użytkownika, Utwórz plik o nazwie `delete_user.json` i Dodaj powitania po zawartości.</span><span class="sxs-lookup"><span data-stu-id="04e7d-146">toodelete a user, create a file named `delete_user.json` and add hello following content.</span></span> <span data-ttu-id="04e7d-147">Zastąp wartość dla hello `remove_user` parametru:</span><span class="sxs-lookup"><span data-stu-id="04e7d-147">Substitute your own value for hello `remove_user` parameter:</span></span>

```json
{
  "remove_user":"myNewUser"
}
```

<span data-ttu-id="04e7d-148">Wykonanie skryptu VMAccess hello:</span><span class="sxs-lookup"><span data-stu-id="04e7d-148">Execute hello VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings delete_user.json
```

### <a name="check-or-repair-hello-disk"></a><span data-ttu-id="04e7d-149">Sprawdź lub napraw program hello dysku</span><span class="sxs-lookup"><span data-stu-id="04e7d-149">Check or repair hello disk</span></span>
<span data-ttu-id="04e7d-150">Użyć rozszerzenia VMAccess można również sprawdzić i naprawiania dysku dodania toohello maszyny Wirtualnej systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="04e7d-150">Using VMAccess you can also check and repair a disk that you added toohello Linux VM.</span></span>

<span data-ttu-id="04e7d-151">toocheck, a następnie napraw hello dysku, Utwórz plik o nazwie `disk_check_repair.json` i dodać ustawienia hello zgodny z formatem.</span><span class="sxs-lookup"><span data-stu-id="04e7d-151">toocheck and then repair hello disk, create a file named `disk_check_repair.json` and add settings in hello following format.</span></span> <span data-ttu-id="04e7d-152">Zastąp wartość dla nazwy hello `repair_disk`:</span><span class="sxs-lookup"><span data-stu-id="04e7d-152">Substitute your own value for hello name of `repair_disk`:</span></span>

```json
{
  "check_disk": "true",
  "repair_disk": "true, mydiskname"
}
```

<span data-ttu-id="04e7d-153">Wykonanie skryptu VMAccess hello:</span><span class="sxs-lookup"><span data-stu-id="04e7d-153">Execute hello VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings disk_check_repair.json
```

## <a name="next-steps"></a><span data-ttu-id="04e7d-154">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="04e7d-154">Next steps</span></span>
<span data-ttu-id="04e7d-155">Aktualizowanie systemu Linux przy użyciu hello Azure rozszerzenia VMAccess jest jeden zmian toomake metody na uruchomionej maszyny Wirtualnej systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="04e7d-155">Updating Linux using hello Azure VMAccess Extension is one method toomake changes on a running Linux VM.</span></span> <span data-ttu-id="04e7d-156">Umożliwia także narzędzi, takich jak chmury init i toomodify szablonów usługi Azure Resource Manager z maszyny Wirtualnej systemu Linux na rozruchu.</span><span class="sxs-lookup"><span data-stu-id="04e7d-156">You can also use tools like cloud-init and Azure Resource Manager templates toomodify your Linux VM on boot.</span></span>

[<span data-ttu-id="04e7d-157">Rozszerzenia maszyn wirtualnych i funkcji w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="04e7d-157">Virtual machine extensions and features for Linux</span></span>](extensions-features.md)

[<span data-ttu-id="04e7d-158">Tworzenie szablonów usługi Azure Resource Manager z rozszerzeniami maszyny Wirtualnej systemu Linux</span><span class="sxs-lookup"><span data-stu-id="04e7d-158">Authoring Azure Resource Manager templates with Linux VM extensions</span></span>](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="04e7d-159">Podczas tworzenia przy użyciu chmury init toocustomize Maszynę wirtualną systemu Linux</span><span class="sxs-lookup"><span data-stu-id="04e7d-159">Using cloud-init toocustomize a Linux VM during creation</span></span>](using-cloud-init.md)

