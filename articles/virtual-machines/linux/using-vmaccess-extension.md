---
title: "Zresetuj dostęp do maszyny Wirtualnej systemu Linux na platformie Azure | Dokumentacja firmy Microsoft"
description: "Jak zarządzać użytkownikami i zresetuj dostęp na maszynach wirtualnych systemu Linux przy użyciu rozszerzenia VMAccess i 2.0 interfejsu wiersza polecenia platformy Azure"
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
ms.openlocfilehash: 587c73278a9a92776276a811c5c4c8d3db773de3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="manage-users-ssh-and-check-or-repair-disks-on-linux-vms-using-the-vmaccess-extension-with-the-azure-cli-20"></a><span data-ttu-id="95719-103">Zarządzanie użytkownikami, SSH i wyboru lub napraw dyski na maszynach wirtualnych systemu Linux przy użyciu rozszerzenia VMAccess 2.0 interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="95719-103">Manage users, SSH, and check or repair disks on Linux VMs using the VMAccess Extension with the Azure CLI 2.0</span></span>
<span data-ttu-id="95719-104">Dysk na maszynie Wirtualnej systemu Linux są pokazywane błędy.</span><span class="sxs-lookup"><span data-stu-id="95719-104">The disk on your Linux VM is showing errors.</span></span> <span data-ttu-id="95719-105">Jakiś sposób resetowania hasła głównego dla maszyny Wirtualnej systemu Linux lub przypadkowo usunięty klucz prywatny SSH.</span><span class="sxs-lookup"><span data-stu-id="95719-105">You somehow reset the root password for your Linux VM or accidentally deleted your SSH private key.</span></span> <span data-ttu-id="95719-106">Jeśli które miały miejsce w ciągu dni centrum danych, konieczne będzie dysk istnieje, a następnie otwórz KVM można uzyskać za pomocą konsoli serwera.</span><span class="sxs-lookup"><span data-stu-id="95719-106">If that happened back in the days of the datacenter, you would need to drive there and then open the KVM to get at the server console.</span></span> <span data-ttu-id="95719-107">Rozszerzenia Azure VMAccess można traktować jako przełącznika KVM, które umożliwia dostęp do konsoli zresetować dostępu do systemu Linux lub przeprowadź obsługę poziomu dysku.</span><span class="sxs-lookup"><span data-stu-id="95719-107">Think of the Azure VMAccess extension as that KVM switch that allows you to access the console to reset access to Linux or perform disk level maintenance.</span></span>

<span data-ttu-id="95719-108">W tym artykule przedstawiono sposób rozszerzenia VMAccess Azure umożliwia sprawdzanie lub naprawiania dysku, zresetuj dostęp użytkownika, zarządzanie kontami użytkowników, zresetuj konfigurację protokołu SSH w systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="95719-108">This article shows you how to use the Azure VMAccess Extension to check or repair a disk, reset user access, manage user accounts, or reset the SSH configuration on Linux.</span></span> <span data-ttu-id="95719-109">Czynności te można również wykonać przy użyciu [interfejsu wiersza polecenia platformy Azure w wersji 1.0](using-vmaccess-extension-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="95719-109">You can also perform these steps with the [Azure CLI 1.0](using-vmaccess-extension-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="ways-to-use-the-vmaccess-extension"></a><span data-ttu-id="95719-110">Sposoby używania rozszerzenia VMAccess</span><span class="sxs-lookup"><span data-stu-id="95719-110">Ways to use the VMAccess Extension</span></span>
<span data-ttu-id="95719-111">Istnieją dwa sposoby, że można użyć rozszerzenia VMAccess na maszyny wirtualne systemu Linux:</span><span class="sxs-lookup"><span data-stu-id="95719-111">There are two ways that you can use the VMAccess Extension on your Linux VMs:</span></span>

* <span data-ttu-id="95719-112">Użyj interfejsu wiersza polecenia platformy Azure w wersji 2.0 i wymaganych parametrów.</span><span class="sxs-lookup"><span data-stu-id="95719-112">Use the Azure CLI 2.0 and the required parameters.</span></span>
* <span data-ttu-id="95719-113">[Użyj nieprzetworzone pliki w formacie JSON, które przetwarzają rozszerzenia VMAccess](#use-json-files-and-the-vmaccess-extension) i działa na.</span><span class="sxs-lookup"><span data-stu-id="95719-113">[Use raw JSON files that the VMAccess Extension process](#use-json-files-and-the-vmaccess-extension) and then act on.</span></span>

<span data-ttu-id="95719-114">W poniższych przykładach użyto [użytkownika maszyny wirtualnej az](/cli/azure/vm/user) poleceń.</span><span class="sxs-lookup"><span data-stu-id="95719-114">The following examples use [az vm user](/cli/azure/vm/user) commands.</span></span> <span data-ttu-id="95719-115">Aby wykonać te kroki, należy najnowszej [Azure CLI 2.0](/cli/azure/install-az-cli2) zainstalowane i zalogowany do konta platformy Azure przy użyciu [logowania az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="95719-115">To perform these steps, you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

## <a name="reset-ssh-key"></a><span data-ttu-id="95719-116">Resetuj klucz SSH</span><span class="sxs-lookup"><span data-stu-id="95719-116">Reset SSH key</span></span>
<span data-ttu-id="95719-117">Poniższy przykład resetuje klucza SSH dla użytkownika `azureuser` na Maszynie wirtualnej o nazwie `myVM`:</span><span class="sxs-lookup"><span data-stu-id="95719-117">The following example resets the SSH key for the user `azureuser` on the VM named `myVM`:</span></span>

```azurecli
az vm user update \
  --resource-group myResourceGroup \
  --name myVM \
  --username azureuser \
  --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="reset-password"></a><span data-ttu-id="95719-118">Resetowanie hasła</span><span class="sxs-lookup"><span data-stu-id="95719-118">Reset password</span></span>
<span data-ttu-id="95719-119">Poniższy przykład resetuje hasło użytkownika `azureuser` na Maszynie wirtualnej o nazwie `myVM`:</span><span class="sxs-lookup"><span data-stu-id="95719-119">The following example resets the password for the user `azureuser` on the VM named `myVM`:</span></span>

```azurecli
az vm user update \
  --resource-group myResourceGroup \
  --name myVM \
  --username azureuser \
  --password myNewPassword
```

## <a name="restart-ssh"></a><span data-ttu-id="95719-120">Uruchom ponownie SSH</span><span class="sxs-lookup"><span data-stu-id="95719-120">Restart SSH</span></span>
<span data-ttu-id="95719-121">W poniższym przykładzie uruchomieniu demon SSH i zresetowanie konfiguracji SSH do wartości domyślnych na maszynie Wirtualnej o nazwie `myVM`:</span><span class="sxs-lookup"><span data-stu-id="95719-121">The following example restarts the SSH daemon and resets the SSH configuration to default values on a VM named `myVM`:</span></span>

```azurecli
az vm user reset-ssh \
  --resource-group myResourceGroup \
  --name myVM
```

## <a name="create-a-user"></a><span data-ttu-id="95719-122">Utwórz użytkownika</span><span class="sxs-lookup"><span data-stu-id="95719-122">Create a user</span></span>
<span data-ttu-id="95719-123">Poniższy przykład tworzy użytkownika o nazwie `myNewUser` przy użyciu klucza SSH do uwierzytelniania na Maszynie wirtualnej o nazwie `myVM`:</span><span class="sxs-lookup"><span data-stu-id="95719-123">The following example creates a user named `myNewUser` using an SSH key for authentication on the VM named `myVM`:</span></span>

```azurecli
az vm user update \
  --resource-group myResourceGroup \
  --name myVM \
  --username myNewUser \
  --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="delete-a-user"></a><span data-ttu-id="95719-124">Usuń użytkownika</span><span class="sxs-lookup"><span data-stu-id="95719-124">Delete a user</span></span>
<span data-ttu-id="95719-125">W następującym przykładzie użytkownik o nazwie `myNewUser` na Maszynie wirtualnej o nazwie `myVM`:</span><span class="sxs-lookup"><span data-stu-id="95719-125">The following example deletes a user named `myNewUser` on the VM named `myVM`:</span></span>

```azurecli
az vm user delete \
  --resource-group myResourceGroup \
  --name myVM \
  --username myNewUser
```


## <a name="use-json-files-and-the-vmaccess-extension"></a><span data-ttu-id="95719-126">Pliki w formacie JSON i rozszerzenia VMAccess</span><span class="sxs-lookup"><span data-stu-id="95719-126">Use JSON files and the VMAccess Extension</span></span>
<span data-ttu-id="95719-127">W poniższych przykładach użyto nieprzetworzone pliki w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="95719-127">The following examples use raw JSON files.</span></span> <span data-ttu-id="95719-128">Użyj [zestaw rozszerzenia maszyny wirtualnej az](/cli/azure/vm/extension#set) następnie wywołać pliki w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="95719-128">Use [az vm extension set](/cli/azure/vm/extension#set) to then call your JSON files.</span></span> <span data-ttu-id="95719-129">Te pliki w formacie JSON również może być wywołana z szablonów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="95719-129">These JSON files can also be called from Azure templates.</span></span> 

### <a name="reset-user-access"></a><span data-ttu-id="95719-130">Zresetuj dostęp użytkownika</span><span class="sxs-lookup"><span data-stu-id="95719-130">Reset user access</span></span>
<span data-ttu-id="95719-131">W przypadku utraty dostępu do katalogu głównego na maszynie Wirtualnej systemu Linux, możesz uruchomić skrypt rozszerzenia VMAccess do zresetowania hasła lub klucza SSH użytkownika.</span><span class="sxs-lookup"><span data-stu-id="95719-131">If you have lost access to root on your Linux VM, you can launch a VMAccess script to reset a user's SSH key or password.</span></span>

<span data-ttu-id="95719-132">Aby zresetować klucz publiczny SSH użytkownika, Utwórz plik o nazwie `reset_ssh_key.json` i dodaj ustawienia w następującym formacie.</span><span class="sxs-lookup"><span data-stu-id="95719-132">To reset the SSH public key of a user, create a file named `reset_ssh_key.json` and add settings in the following format.</span></span> <span data-ttu-id="95719-133">Podstaw wartości dla `username` i `ssh_key` parametry:</span><span class="sxs-lookup"><span data-stu-id="95719-133">Substitute your own values for the `username` and `ssh_key` parameters:</span></span>

```json
{
  "username":"azureuser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNGxxxxxx2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7xxxxxxwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5wxxtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== azureuser@myVM"
}
```

<span data-ttu-id="95719-134">Wykonanie skryptu VMAccess:</span><span class="sxs-lookup"><span data-stu-id="95719-134">Execute the VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings reset_ssh_key.json
```

<span data-ttu-id="95719-135">Aby zresetować hasło użytkownika, Utwórz plik o nazwie `reset_user_password.json` i dodaj ustawienia w następującym formacie.</span><span class="sxs-lookup"><span data-stu-id="95719-135">To reset a user password, create a file named `reset_user_password.json` and add settings in the following format.</span></span> <span data-ttu-id="95719-136">Podstaw wartości dla `username` i `password` parametry:</span><span class="sxs-lookup"><span data-stu-id="95719-136">Substitute your own values for the `username` and `password` parameters:</span></span>

```json
{
  "username":"azureuser",
  "password":"myNewPassword" 
}
```

<span data-ttu-id="95719-137">Wykonanie skryptu VMAccess:</span><span class="sxs-lookup"><span data-stu-id="95719-137">Execute the VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings reset_user_password.json
```

### <a name="restart-ssh"></a><span data-ttu-id="95719-138">Uruchom ponownie SSH</span><span class="sxs-lookup"><span data-stu-id="95719-138">Restart SSH</span></span>
<span data-ttu-id="95719-139">Aby uruchomić ponownie demon SSH i zresetowanie konfiguracji SSH do wartości domyślnych, Utwórz plik o nazwie `reset_sshd.json`.</span><span class="sxs-lookup"><span data-stu-id="95719-139">To restart the SSH daemon and reset the SSH configuration to default values, create a file named `reset_sshd.json`.</span></span> <span data-ttu-id="95719-140">Dodaj następującą zawartość:</span><span class="sxs-lookup"><span data-stu-id="95719-140">Add the following content:</span></span>

```json
{
  "reset_ssh": true
}
```

<span data-ttu-id="95719-141">Wykonanie skryptu VMAccess:</span><span class="sxs-lookup"><span data-stu-id="95719-141">Execute the VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings reset_sshd.json
```

### <a name="manage-users"></a><span data-ttu-id="95719-142">Zarządzanie użytkownikami</span><span class="sxs-lookup"><span data-stu-id="95719-142">Manage users</span></span>

<span data-ttu-id="95719-143">Aby utworzyć użytkownika, który używa klucza SSH do uwierzytelniania, Utwórz plik o nazwie `create_new_user.json` i dodaj ustawienia w następującym formacie.</span><span class="sxs-lookup"><span data-stu-id="95719-143">To create a user that uses an SSH key for authentication, create a file named `create_new_user.json` and add settings in the following format.</span></span> <span data-ttu-id="95719-144">Podstaw wartości dla `username` i `ssh_key` parametry:</span><span class="sxs-lookup"><span data-stu-id="95719-144">Substitute your own values for the `username` and `ssh_key` parameters:</span></span>

```json
{
  "username":"myNewUser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNG1vHY7P2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7iUo5IdwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5woYtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== myNewUser@myVM",
  "password":"myNewUserPassword"
}
```

<span data-ttu-id="95719-145">Wykonanie skryptu VMAccess:</span><span class="sxs-lookup"><span data-stu-id="95719-145">Execute the VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings create_new_user.json
```

<span data-ttu-id="95719-146">Aby usunąć użytkownika, Utwórz plik o nazwie `delete_user.json` i dodaj następującą zawartość.</span><span class="sxs-lookup"><span data-stu-id="95719-146">To delete a user, create a file named `delete_user.json` and add the following content.</span></span> <span data-ttu-id="95719-147">Zastąp wartość dla `remove_user` parametru:</span><span class="sxs-lookup"><span data-stu-id="95719-147">Substitute your own value for the `remove_user` parameter:</span></span>

```json
{
  "remove_user":"myNewUser"
}
```

<span data-ttu-id="95719-148">Wykonanie skryptu VMAccess:</span><span class="sxs-lookup"><span data-stu-id="95719-148">Execute the VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings delete_user.json
```

### <a name="check-or-repair-the-disk"></a><span data-ttu-id="95719-149">Sprawdź i napraw dysk</span><span class="sxs-lookup"><span data-stu-id="95719-149">Check or repair the disk</span></span>
<span data-ttu-id="95719-150">Użyć rozszerzenia VMAccess można również Sprawdź i napraw dysku, który został dodany do maszyny Wirtualnej systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="95719-150">Using VMAccess you can also check and repair a disk that you added to the Linux VM.</span></span>

<span data-ttu-id="95719-151">Sprawdź, a następnie napraw dysku, Utwórz plik o nazwie `disk_check_repair.json` i dodaj ustawienia w następującym formacie.</span><span class="sxs-lookup"><span data-stu-id="95719-151">To check and then repair the disk, create a file named `disk_check_repair.json` and add settings in the following format.</span></span> <span data-ttu-id="95719-152">Zastąp wartość dla nazwy `repair_disk`:</span><span class="sxs-lookup"><span data-stu-id="95719-152">Substitute your own value for the name of `repair_disk`:</span></span>

```json
{
  "check_disk": "true",
  "repair_disk": "true, mydiskname"
}
```

<span data-ttu-id="95719-153">Wykonanie skryptu VMAccess:</span><span class="sxs-lookup"><span data-stu-id="95719-153">Execute the VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings disk_check_repair.json
```

## <a name="next-steps"></a><span data-ttu-id="95719-154">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="95719-154">Next steps</span></span>
<span data-ttu-id="95719-155">Aktualizowanie systemu Linux przy użyciu rozszerzenia VMAccess Azure jest jedną metodę, aby wprowadzić zmiany w uruchomionej maszyny Wirtualnej systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="95719-155">Updating Linux using the Azure VMAccess Extension is one method to make changes on a running Linux VM.</span></span> <span data-ttu-id="95719-156">Aby zmodyfikować maszyny Wirtualnej systemu Linux na rozruch umożliwia także narzędzia, takie jak szablony usługi Azure Resource Manager i init chmury.</span><span class="sxs-lookup"><span data-stu-id="95719-156">You can also use tools like cloud-init and Azure Resource Manager templates to modify your Linux VM on boot.</span></span>

[<span data-ttu-id="95719-157">Rozszerzenia maszyn wirtualnych i funkcji w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="95719-157">Virtual machine extensions and features for Linux</span></span>](extensions-features.md)

[<span data-ttu-id="95719-158">Tworzenie szablonów usługi Azure Resource Manager z rozszerzeniami maszyny Wirtualnej systemu Linux</span><span class="sxs-lookup"><span data-stu-id="95719-158">Authoring Azure Resource Manager templates with Linux VM extensions</span></span>](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="95719-159">Dostosowywanie maszyny Wirtualnej systemu Linux podczas tworzenia za pomocą init chmury</span><span class="sxs-lookup"><span data-stu-id="95719-159">Using cloud-init to customize a Linux VM during creation</span></span>](using-cloud-init.md)

