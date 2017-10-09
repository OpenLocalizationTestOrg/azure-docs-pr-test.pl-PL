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
# <a name="manage-users-ssh-and-check-or-repair-disks-on-linux-vms-using-hello-vmaccess-extension-with-hello-azure-cli-20"></a>Zarządzanie użytkownikami, SSH i wyboru lub naprawy dysków na maszynach wirtualnych systemu Linux przy użyciu hello rozszerzenia VMAccess z hello Azure CLI 2.0
Witaj dysku na maszynie Wirtualnej systemu Linux są pokazywane błędy. Jakiś sposób resetowania hasła użytkownika root hello dla maszyny Wirtualnej systemu Linux lub przypadkowo usunięty klucz prywatny SSH. Jeśli który wystąpił w dni hello hello centrum danych, będzie konieczne toodrive, a następnie otwórz tooget KVM hello na powitania serwera konsoli. Witaj rozszerzenia Azure VMAccess można traktować jako przełącznika KVM, które pozwala tooaccess hello konsoli tooreset dostępu tooLinux przeprowadzania konserwacji poziomu dysku.

W tym artykule opisano, jak toouse hello Azure rozszerzenia VMAccess toocheck lub naprawiania dysku, zresetuj dostęp użytkownika, zarządzanie kontami użytkowników lub zresetowanie konfiguracji SSH hello w systemie Linux. Można również wykonać te kroki hello [Azure CLI 1.0](using-vmaccess-extension-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).


## <a name="ways-toouse-hello-vmaccess-extension"></a>Sposoby toouse hello rozszerzenia VMAccess
Istnieją dwa sposoby, w których można używać hello rozszerzenia VMAccess na maszyny wirtualne systemu Linux:

* Użyj hello Azure CLI 2.0 i hello wymaganych parametrów.
* [Użyj nieprzetworzone dane JSON pliki tego procesu rozszerzenia VMAccess hello](#use-json-files-and-the-vmaccess-extension) i działa na.

Witaj, następujące przykłady użycia [użytkownika maszyny wirtualnej az](/cli/azure/vm/user) poleceń. tooperform tych kroków, należy hello najnowszych [Azure CLI 2.0](/cli/azure/install-az-cli2) zainstalowane i zarejestrowane za pomocą konta Azure tooan [logowania az](/cli/azure/#login).

## <a name="reset-ssh-key"></a>Resetuj klucz SSH
Witaj poniższy przykład resetuje hello klucza SSH dla użytkownika hello `azureuser` na powitania maszyny Wirtualnej o nazwie `myVM`:

```azurecli
az vm user update \
  --resource-group myResourceGroup \
  --name myVM \
  --username azureuser \
  --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="reset-password"></a>Resetowanie hasła
Witaj poniższy przykład resetuje hello hasło dla użytkownika hello `azureuser` na powitania maszyny Wirtualnej o nazwie `myVM`:

```azurecli
az vm user update \
  --resource-group myResourceGroup \
  --name myVM \
  --username azureuser \
  --password myNewPassword
```

## <a name="restart-ssh"></a>Uruchom ponownie SSH
Witaj poniższym przykładzie zostanie ponownie uruchomiony demon SSH hello i resetuje hello wartości toodefault konfiguracji SSH maszyny wirtualnej o nazwie `myVM`:

```azurecli
az vm user reset-ssh \
  --resource-group myResourceGroup \
  --name myVM
```

## <a name="create-a-user"></a>Utwórz użytkownika
Witaj poniższy przykład tworzy użytkownika o nazwie `myNewUser` przy użyciu klucza SSH do uwierzytelniania na powitania maszyny Wirtualnej o nazwie `myVM`:

```azurecli
az vm user update \
  --resource-group myResourceGroup \
  --name myVM \
  --username myNewUser \
  --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="delete-a-user"></a>Usuń użytkownika
Witaj poniższy przykład powoduje usunięcie użytkownika o nazwie `myNewUser` na powitania maszyny Wirtualnej o nazwie `myVM`:

```azurecli
az vm user delete \
  --resource-group myResourceGroup \
  --name myVM \
  --username myNewUser
```


## <a name="use-json-files-and-hello-vmaccess-extension"></a>Użyj pliki w formacie JSON i hello rozszerzenia VMAccess
Następujące przykłady Hello Użyj nieprzetworzone pliki w formacie JSON. Użyj [zestaw rozszerzenia maszyny wirtualnej az](/cli/azure/vm/extension#set) toothen wywołać pliki w formacie JSON. Te pliki w formacie JSON również może być wywołana z szablonów platformy Azure. 

### <a name="reset-user-access"></a>Zresetuj dostęp użytkownika
W przypadku utraty dostępu tooroot na maszynie Wirtualnej systemu Linux, możesz uruchomić tooreset skryptu VMAccess klucza SSH użytkownika lub hasło.

klucz publiczny SSH hello tooreset użytkownika, Utwórz plik o nazwie `reset_ssh_key.json` i dodać ustawienia hello zgodny z formatem. Podstaw wartości dla hello `username` i `ssh_key` parametry:

```json
{
  "username":"azureuser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNGxxxxxx2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7xxxxxxwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5wxxtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== azureuser@myVM"
}
```

Wykonanie skryptu VMAccess hello:

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings reset_ssh_key.json
```

tooreset hasło użytkownika, Utwórz plik o nazwie `reset_user_password.json` i dodać ustawienia hello zgodny z formatem. Podstaw wartości dla hello `username` i `password` parametry:

```json
{
  "username":"azureuser",
  "password":"myNewPassword" 
}
```

Wykonanie skryptu VMAccess hello:

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings reset_user_password.json
```

### <a name="restart-ssh"></a>Uruchom ponownie SSH
toorestart hello demon SSH i resetowania wartości toodefault konfiguracji SSH hello, Utwórz plik o nazwie `reset_sshd.json`. Dodaj hello następującej zawartości:

```json
{
  "reset_ssh": true
}
```

Wykonanie skryptu VMAccess hello:

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings reset_sshd.json
```

### <a name="manage-users"></a>Zarządzanie użytkownikami

toocreate użytkownika, który używa klucza SSH do uwierzytelnienia, Utwórz plik o nazwie `create_new_user.json` i dodać ustawienia hello zgodny z formatem. Podstaw wartości dla hello `username` i `ssh_key` parametry:

```json
{
  "username":"myNewUser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNG1vHY7P2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7iUo5IdwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5woYtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== myNewUser@myVM",
  "password":"myNewUserPassword"
}
```

Wykonanie skryptu VMAccess hello:

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings create_new_user.json
```

toodelete użytkownika, Utwórz plik o nazwie `delete_user.json` i Dodaj powitania po zawartości. Zastąp wartość dla hello `remove_user` parametru:

```json
{
  "remove_user":"myNewUser"
}
```

Wykonanie skryptu VMAccess hello:

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings delete_user.json
```

### <a name="check-or-repair-hello-disk"></a>Sprawdź lub napraw program hello dysku
Użyć rozszerzenia VMAccess można również sprawdzić i naprawiania dysku dodania toohello maszyny Wirtualnej systemu Linux.

toocheck, a następnie napraw hello dysku, Utwórz plik o nazwie `disk_check_repair.json` i dodać ustawienia hello zgodny z formatem. Zastąp wartość dla nazwy hello `repair_disk`:

```json
{
  "check_disk": "true",
  "repair_disk": "true, mydiskname"
}
```

Wykonanie skryptu VMAccess hello:

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings disk_check_repair.json
```

## <a name="next-steps"></a>Następne kroki
Aktualizowanie systemu Linux przy użyciu hello Azure rozszerzenia VMAccess jest jeden zmian toomake metody na uruchomionej maszyny Wirtualnej systemu Linux. Umożliwia także narzędzi, takich jak chmury init i toomodify szablonów usługi Azure Resource Manager z maszyny Wirtualnej systemu Linux na rozruchu.

[Rozszerzenia maszyn wirtualnych i funkcji w systemie Linux](extensions-features.md)

[Tworzenie szablonów usługi Azure Resource Manager z rozszerzeniami maszyny Wirtualnej systemu Linux](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[Podczas tworzenia przy użyciu chmury init toocustomize Maszynę wirtualną systemu Linux](using-cloud-init.md)

