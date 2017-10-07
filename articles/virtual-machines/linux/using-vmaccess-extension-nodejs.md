---
title: "aaaReset dostępu na maszynach wirtualnych systemu Linux platformy Azure przy użyciu hello rozszerzenia VMAccess | Dokumentacja firmy Microsoft"
description: "Zresetuj dostęp na maszynach wirtualnych systemu Linux platformy Azure przy użyciu hello rozszerzenia VMAccess."
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 261a9646-1f93-407e-951e-0be7226b3064
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 10/25/2016
ms.author: v-livech
ms.openlocfilehash: 2636655f3f7d14ba30e1dc62c319e4e278521ead
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-users-ssh-and-check-or-repair-disks-on-azure-linux-vms-using-hello-vmaccess-extension-with-hello-azure-cli-10"></a><span data-ttu-id="4f321-103">Zarządzanie użytkownikami, SSH i wyboru lub naprawy dysków na maszynach wirtualnych systemu Linux platformy Azure przy użyciu hello rozszerzenia VMAccess z hello Azure CLI w wersji 1.0</span><span class="sxs-lookup"><span data-stu-id="4f321-103">Manage users, SSH, and check or repair disks on Azure Linux VMs using hello VMAccess Extension with hello Azure CLI 1.0</span></span>
<span data-ttu-id="4f321-104">W tym artykule opisano, jak toouse hello Azure VMAcesss rozszerzenia toocheck lub naprawiania dysku, zresetuj dostęp użytkownika, zarządzanie kontami użytkowników lub zresetuj konfigurację SSHD hello w systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="4f321-104">This article shows you how toouse hello Azure VMAcesss Extension toocheck or repair a disk, reset user access, manage user accounts, or reset hello SSHD configuration on Linux.</span></span> <span data-ttu-id="4f321-105">wymaga artykułu Hello:</span><span class="sxs-lookup"><span data-stu-id="4f321-105">hello article requires:</span></span>

* <span data-ttu-id="4f321-106">konta platformy Azure ([skorzystaj z bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/));</span><span class="sxs-lookup"><span data-stu-id="4f321-106">an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)).</span></span>
* <span data-ttu-id="4f321-107">Witaj [interfejsu wiersza polecenia Azure](../../cli-install-nodejs.md) logowania `azure login`.</span><span class="sxs-lookup"><span data-stu-id="4f321-107">hello [Azure CLI](../../cli-install-nodejs.md) logged in with `azure login`.</span></span>
* <span data-ttu-id="4f321-108">Hello Azure CLI *musi znajdować się w* tryb usługi Azure Resource Manager `azure config mode arm`.</span><span class="sxs-lookup"><span data-stu-id="4f321-108">hello Azure CLI *must be in* Azure Resource Manager mode `azure config mode arm`.</span></span>


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="4f321-109">Zadanie hello toocomplete wersje interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="4f321-109">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="4f321-110">Można ukończyć powitalnych zadań przy użyciu jednej z hello następujące wersje interfejsu wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="4f321-110">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="4f321-111">[Azure CLI 1.0](#quick-commands)— nasze interfejsu wiersza polecenia dla hello classic i zasobów zarządzania wdrażania modeli (w tym artykule)</span><span class="sxs-lookup"><span data-stu-id="4f321-111">[Azure CLI 1.0](#quick-commands)– our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="4f321-112">[Azure CLI 2.0](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -naszej nowej generacji interfejsu wiersza polecenia dla modelu wdrażania zarządzania zasobów hello</span><span class="sxs-lookup"><span data-stu-id="4f321-112">[Azure CLI 2.0](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="4f321-113">Szybkie polecenia</span><span class="sxs-lookup"><span data-stu-id="4f321-113">Quick commands</span></span>
<span data-ttu-id="4f321-114">Istnieją dwa sposoby toouse VMAccess na maszyny wirtualne systemu Linux:</span><span class="sxs-lookup"><span data-stu-id="4f321-114">There are two ways toouse VMAccess on your Linux VMs:</span></span>

* <span data-ttu-id="4f321-115">Przy użyciu hello Azure CLI 1.0 i hello wymagane parametry.</span><span class="sxs-lookup"><span data-stu-id="4f321-115">Using hello Azure CLI 1.0 and hello required parameters.</span></span>
* <span data-ttu-id="4f321-116">Przy użyciu nieprzetworzone pliki w formacie JSON, które rozszerzenia VMAccess przetwarza i działa na.</span><span class="sxs-lookup"><span data-stu-id="4f321-116">Using raw JSON files that VMAccess processes and then act on.</span></span>

<span data-ttu-id="4f321-117">W sekcji szybkich poleceń hello, zamierzamy toouse hello Azure CLI 1.0 `azure vm reset-access` metody.</span><span class="sxs-lookup"><span data-stu-id="4f321-117">For hello quick command section, we are going toouse hello Azure CLI 1.0 `azure vm reset-access` method.</span></span> <span data-ttu-id="4f321-118">W hello poniższych przykładach poleceń Zastąp wartości hello, zawierających "przykładu" hello wartościami z własnego środowiska.</span><span class="sxs-lookup"><span data-stu-id="4f321-118">In hello following command examples, replace hello values that contain "example" with hello values from your own environment.</span></span>

## <a name="create-a-resource-group-and-linux-vm"></a><span data-ttu-id="4f321-119">Tworzenie grupy zasobów i maszyny Wirtualnej systemu Linux</span><span class="sxs-lookup"><span data-stu-id="4f321-119">Create a Resource Group and Linux VM</span></span>
```bash
azure group create myResourceGroup westus
```

## <a name="create-a-debian-vm"></a><span data-ttu-id="4f321-120">Tworzenie Debian maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="4f321-120">Create a Debian VM</span></span>
```azurecli
azure vm quick-create \
  -M ~/.ssh/id_rsa.pub \
  -u myAdminUser \
  -g myResourceGroup \
  -l westus \
  -y Linux \
  -n myVM \
  -Q Debian
```

## <a name="reset-root-password"></a><span data-ttu-id="4f321-121">Resetowanie hasła głównego</span><span class="sxs-lookup"><span data-stu-id="4f321-121">Reset root password</span></span>
<span data-ttu-id="4f321-122">hasła głównego hello tooreset:</span><span class="sxs-lookup"><span data-stu-id="4f321-122">tooreset hello root password:</span></span>

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -u root \
  -p myNewPassword
```

## <a name="ssh-key-reset"></a><span data-ttu-id="4f321-123">Resetowanie klucza SSH</span><span class="sxs-lookup"><span data-stu-id="4f321-123">SSH key reset</span></span>
<span data-ttu-id="4f321-124">klucz SSH hello tooreset użytkownika innego niż główny:</span><span class="sxs-lookup"><span data-stu-id="4f321-124">tooreset hello SSH key of a non-root user:</span></span>

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -u myAdminUser \
  -M ~/.ssh/id_rsa.pub
```

## <a name="create-a-user"></a><span data-ttu-id="4f321-125">Utwórz użytkownika</span><span class="sxs-lookup"><span data-stu-id="4f321-125">Create a user</span></span>
<span data-ttu-id="4f321-126">toocreate użytkownika:</span><span class="sxs-lookup"><span data-stu-id="4f321-126">toocreate a user:</span></span>

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -u myAdminUser \
  -p myAdminUserPassword
```

## <a name="remove-a-user"></a><span data-ttu-id="4f321-127">Usuwanie użytkownika</span><span class="sxs-lookup"><span data-stu-id="4f321-127">Remove a user</span></span>
```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -R myRemovedUser
```

## <a name="reset-sshd"></a><span data-ttu-id="4f321-128">Resetuj SSHD</span><span class="sxs-lookup"><span data-stu-id="4f321-128">Reset SSHD</span></span>
<span data-ttu-id="4f321-129">Konfiguracja SSHD hello tooreset:</span><span class="sxs-lookup"><span data-stu-id="4f321-129">tooreset hello SSHD configuration:</span></span>

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM
  -r
```


## <a name="detailed-walkthrough"></a><span data-ttu-id="4f321-130">Szczegółowy przewodnik</span><span class="sxs-lookup"><span data-stu-id="4f321-130">Detailed walkthrough</span></span>
### <a name="vmaccess-defined"></a><span data-ttu-id="4f321-131">Rozszerzenia VMAccess zdefiniowane:</span><span class="sxs-lookup"><span data-stu-id="4f321-131">VMAccess defined:</span></span>
<span data-ttu-id="4f321-132">Witaj dysku na maszynie Wirtualnej systemu Linux są pokazywane błędy.</span><span class="sxs-lookup"><span data-stu-id="4f321-132">hello disk on your Linux VM is showing errors.</span></span> <span data-ttu-id="4f321-133">Jakiś sposób resetowania hasła użytkownika root hello dla maszyny Wirtualnej systemu Linux lub przypadkowo usunięty klucz prywatny SSH.</span><span class="sxs-lookup"><span data-stu-id="4f321-133">You somehow reset hello root password for your Linux VM or accidentally deleted your SSH private key.</span></span> <span data-ttu-id="4f321-134">Jeśli który wystąpił w dni hello hello centrum danych, będzie konieczne toodrive, a następnie otwórz tooget KVM hello na powitania serwera konsoli.</span><span class="sxs-lookup"><span data-stu-id="4f321-134">If that happened back in hello days of hello datacenter, you would need toodrive there and then open hello KVM tooget at hello server console.</span></span> <span data-ttu-id="4f321-135">Witaj rozszerzenia Azure VMAccess można traktować jako przełącznika KVM, które pozwala tooaccess hello konsoli tooreset dostępu tooLinux przeprowadzania konserwacji poziomu dysku.</span><span class="sxs-lookup"><span data-stu-id="4f321-135">Think of hello Azure VMAccess extension as that KVM switch that allows you tooaccess hello console tooreset access tooLinux or perform disk level maintenance.</span></span>

<span data-ttu-id="4f321-136">Aby hello uzyskać szczegółowe wskazówki, zamierzamy toouse hello długą formę rozszerzenia VMAccess, który używa nieprzetworzone pliki w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="4f321-136">For hello detailed walkthrough, we are going toouse hello long form of VMAccess, which uses raw JSON files.</span></span>  <span data-ttu-id="4f321-137">Te pliki JSON rozszerzenia VMAccess również może być wywołana z szablonów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4f321-137">These VMAccess JSON files can also be called from Azure templates.</span></span>

### <a name="using-vmaccess-toocheck-or-repair-hello-disk-of-a-linux-vm"></a><span data-ttu-id="4f321-138">Przy użyciu rozszerzenia VMAccess toocheck lub naprawy dysku hello maszyny wirtualnej systemu Linux</span><span class="sxs-lookup"><span data-stu-id="4f321-138">Using VMAccess toocheck or repair hello disk of a Linux VM</span></span>
<span data-ttu-id="4f321-139">Za pomocą rozszerzenia VMAccess można wykonać fsck Uruchom na powitania dysku w obszarze maszyny Wirtualnej systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="4f321-139">Using VMAccess you can do a fsck run on hello disk under your Linux VM.</span></span>  <span data-ttu-id="4f321-140">Można także zrobić wyboru dysku i naprawy dysku przy użyciu rozszerzenia VMAccess.</span><span class="sxs-lookup"><span data-stu-id="4f321-140">You can also do a disk check and a disk repair using a VMAccess.</span></span>

<span data-ttu-id="4f321-141">toocheck, a następnie napraw hello dysku należy użyć tego rozszerzenia VMAccess skryptu:</span><span class="sxs-lookup"><span data-stu-id="4f321-141">toocheck, and then repair hello disk use this VMAccess script:</span></span>

`disk_check_repair.json`

```json
{
  "check_disk": "true",
  "repair_disk": "true, user-disk-name"
}
```

<span data-ttu-id="4f321-142">Wykonanie skryptu VMAccess hello:</span><span class="sxs-lookup"><span data-stu-id="4f321-142">Execute hello VMAccess script with:</span></span>

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path disk_check_repair.json
```

### <a name="using-vmaccess-tooreset-user-access-toolinux"></a><span data-ttu-id="4f321-143">Przy użyciu rozszerzenia VMAccess tooreset użytkownika dostępu tooLinux</span><span class="sxs-lookup"><span data-stu-id="4f321-143">Using VMAccess tooreset user access tooLinux</span></span>
<span data-ttu-id="4f321-144">W przypadku utraty dostępu tooroot na maszynie Wirtualnej systemu Linux, można uruchomić rozszerzenia VMAccess skryptu tooreset hello głównego hasła.</span><span class="sxs-lookup"><span data-stu-id="4f321-144">If you have lost access tooroot on your Linux VM, you can launch a VMAccess script tooreset hello root password.</span></span>

<span data-ttu-id="4f321-145">hasła głównego hello tooreset, użyj tego skryptu VMAccess:</span><span class="sxs-lookup"><span data-stu-id="4f321-145">tooreset hello root password, use this VMAccess script:</span></span>

`reset_root_password.json`

```json
{
  "username":"root",
  "password":"myNewPassword"
}
```

<span data-ttu-id="4f321-146">Wykonanie skryptu VMAccess hello:</span><span class="sxs-lookup"><span data-stu-id="4f321-146">Execute hello VMAccess script with:</span></span>

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path reset_root_password.json
```

<span data-ttu-id="4f321-147">klucz SSH hello tooreset użytkownika innego niż główny, użyj tego skryptu VMAccess:</span><span class="sxs-lookup"><span data-stu-id="4f321-147">tooreset hello SSH key of a non-root user, use this VMAccess script:</span></span>

`reset_ssh_key.json`

```json
{
  "username":"myAdminUser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNG1vHY7P2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7iUo5IdwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5woYtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== myAdminUser@myVM" 
}
```

<span data-ttu-id="4f321-148">Wykonanie skryptu VMAccess hello:</span><span class="sxs-lookup"><span data-stu-id="4f321-148">Execute hello VMAccess script with:</span></span>

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path reset_ssh_key.json
```

### <a name="using-vmaccess-toomanage-user-accounts-on-linux"></a><span data-ttu-id="4f321-149">Przy użyciu kont użytkowników toomanage VMAccess w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="4f321-149">Using VMAccess toomanage user accounts on Linux</span></span>
<span data-ttu-id="4f321-150">Rozszerzenia VMAccess jest skrypt w języku Python, które mogą być używane toomanage użytkowników na maszynie Wirtualnej systemu Linux bez logowania i przy użyciu sudo lub hello konta głównego.</span><span class="sxs-lookup"><span data-stu-id="4f321-150">VMAccess is a Python script that can be used toomanage users on your Linux VM without logging in and using sudo or hello root account.</span></span>

<span data-ttu-id="4f321-151">toocreate użytkownika, użyj tego skryptu VMAccess:</span><span class="sxs-lookup"><span data-stu-id="4f321-151">toocreate a user, use this VMAccess script:</span></span>

`create_new_user.json`

```json
{
  "username":"myNewUser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNG1vHY7P2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7iUo5IdwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5woYtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== myNewUser@myVM",
  "password":"myNewUserPassword"
}
```

<span data-ttu-id="4f321-152">Wykonanie skryptu VMAccess hello:</span><span class="sxs-lookup"><span data-stu-id="4f321-152">Execute hello VMAccess script with:</span></span>

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path create_new_user.json
```

<span data-ttu-id="4f321-153">toodelete użytkownika, użyj tego skryptu VMAccess:</span><span class="sxs-lookup"><span data-stu-id="4f321-153">toodelete a user, use this VMAccess script:</span></span>

`remove_user.json`

```json
{
  "remove_user":"myDeletedUser"
}
```

<span data-ttu-id="4f321-154">Wykonanie skryptu VMAccess hello:</span><span class="sxs-lookup"><span data-stu-id="4f321-154">Execute hello VMAccess script with:</span></span>

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path remove_user.json
```

### <a name="using-vmaccess-tooreset-hello-sshd-configuration"></a><span data-ttu-id="4f321-155">Za pomocą rozszerzenia VMAccess tooreset hello SSHD konfiguracji</span><span class="sxs-lookup"><span data-stu-id="4f321-155">Using VMAccess tooreset hello SSHD configuration</span></span>
<span data-ttu-id="4f321-156">Jeśli konfiguracja SSHD maszyn wirtualnych systemu Linux toohello zmiany i zamknij hello połączenia SSH przed zweryfikowaniem hello zmian, użytkownik może uniemożliwić SSH'ing ponownie.</span><span class="sxs-lookup"><span data-stu-id="4f321-156">If you make changes toohello Linux VMs SSHD configuration and close hello SSH connection before verifying hello changes, you may be prevented from SSH'ing back in.</span></span>  <span data-ttu-id="4f321-157">Rozszerzenia VMAccess mogą być używane tooreset hello SSHD konfiguracji wstecz tooa znanej dobrej konfiguracji bez konieczności logowania się za pomocą protokołu SSH.</span><span class="sxs-lookup"><span data-stu-id="4f321-157">VMAccess can be used tooreset hello SSHD configuration back tooa known good configuration without being logged in over SSH.</span></span>

<span data-ttu-id="4f321-158">tooreset hello SSHD konfiguracji, użyj tego skryptu VMAccess:</span><span class="sxs-lookup"><span data-stu-id="4f321-158">tooreset hello SSHD configuration use this VMAccess script:</span></span>

`reset_sshd.json`

```json
{
  "reset_ssh": true
}
```

<span data-ttu-id="4f321-159">Wykonanie skryptu VMAccess hello:</span><span class="sxs-lookup"><span data-stu-id="4f321-159">Execute hello VMAccess script with:</span></span>

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path reset_sshd.json
```

## <a name="next-steps"></a><span data-ttu-id="4f321-160">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4f321-160">Next steps</span></span>
<span data-ttu-id="4f321-161">Aktualizowanie systemu Linux przy użyciu rozszerzenia VMAccess Azure jest jeden zmian toomake metody na uruchomionej maszyny Wirtualnej systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="4f321-161">Updating Linux using Azure VMAccess Extensions is one method toomake changes on a running Linux VM.</span></span>  <span data-ttu-id="4f321-162">Umożliwia także takich narzędzi jak init chmury i toomodify szablonów Azure maszyny Wirtualnej systemu Linux na rozruchu.</span><span class="sxs-lookup"><span data-stu-id="4f321-162">You can also use tools like cloud-init and Azure Templates toomodify your Linux VM on boot.</span></span>

[<span data-ttu-id="4f321-163">Temat funkcji i rozszerzeń maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="4f321-163">About virtual machine extensions and features</span></span>](../windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="4f321-164">Tworzenie szablonów usługi Azure Resource Manager z rozszerzeniami maszyny Wirtualnej systemu Linux</span><span class="sxs-lookup"><span data-stu-id="4f321-164">Authoring Azure Resource Manager templates with Linux VM extensions</span></span>](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="4f321-165">Podczas tworzenia przy użyciu chmury init toocustomize Maszynę wirtualną systemu Linux</span><span class="sxs-lookup"><span data-stu-id="4f321-165">Using cloud-init toocustomize a Linux VM during creation</span></span>](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

