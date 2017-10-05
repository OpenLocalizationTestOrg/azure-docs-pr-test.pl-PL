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
# <a name="manage-users-ssh-and-check-or-repair-disks-on-linux-vms-using-the-vmaccess-extension-with-the-azure-cli-20"></a>Zarządzanie użytkownikami, SSH i wyboru lub napraw dyski na maszynach wirtualnych systemu Linux przy użyciu rozszerzenia VMAccess 2.0 interfejsu wiersza polecenia platformy Azure
Dysk na maszynie Wirtualnej systemu Linux są pokazywane błędy. Jakiś sposób resetowania hasła głównego dla maszyny Wirtualnej systemu Linux lub przypadkowo usunięty klucz prywatny SSH. Jeśli które miały miejsce w ciągu dni centrum danych, konieczne będzie dysk istnieje, a następnie otwórz KVM można uzyskać za pomocą konsoli serwera. Rozszerzenia Azure VMAccess można traktować jako przełącznika KVM, które umożliwia dostęp do konsoli zresetować dostępu do systemu Linux lub przeprowadź obsługę poziomu dysku.

W tym artykule przedstawiono sposób rozszerzenia VMAccess Azure umożliwia sprawdzanie lub naprawiania dysku, zresetuj dostęp użytkownika, zarządzanie kontami użytkowników, zresetuj konfigurację protokołu SSH w systemie Linux. Czynności te można również wykonać przy użyciu [interfejsu wiersza polecenia platformy Azure w wersji 1.0](using-vmaccess-extension-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).


## <a name="ways-to-use-the-vmaccess-extension"></a>Sposoby używania rozszerzenia VMAccess
Istnieją dwa sposoby, że można użyć rozszerzenia VMAccess na maszyny wirtualne systemu Linux:

* Użyj interfejsu wiersza polecenia platformy Azure w wersji 2.0 i wymaganych parametrów.
* [Użyj nieprzetworzone pliki w formacie JSON, które przetwarzają rozszerzenia VMAccess](#use-json-files-and-the-vmaccess-extension) i działa na.

W poniższych przykładach użyto [użytkownika maszyny wirtualnej az](/cli/azure/vm/user) poleceń. Aby wykonać te kroki, należy najnowszej [Azure CLI 2.0](/cli/azure/install-az-cli2) zainstalowane i zalogowany do konta platformy Azure przy użyciu [logowania az](/cli/azure/#login).

## <a name="reset-ssh-key"></a>Resetuj klucz SSH
Poniższy przykład resetuje klucza SSH dla użytkownika `azureuser` na Maszynie wirtualnej o nazwie `myVM`:

```azurecli
az vm user update \
  --resource-group myResourceGroup \
  --name myVM \
  --username azureuser \
  --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="reset-password"></a>Resetowanie hasła
Poniższy przykład resetuje hasło użytkownika `azureuser` na Maszynie wirtualnej o nazwie `myVM`:

```azurecli
az vm user update \
  --resource-group myResourceGroup \
  --name myVM \
  --username azureuser \
  --password myNewPassword
```

## <a name="restart-ssh"></a>Uruchom ponownie SSH
W poniższym przykładzie uruchomieniu demon SSH i zresetowanie konfiguracji SSH do wartości domyślnych na maszynie Wirtualnej o nazwie `myVM`:

```azurecli
az vm user reset-ssh \
  --resource-group myResourceGroup \
  --name myVM
```

## <a name="create-a-user"></a>Utwórz użytkownika
Poniższy przykład tworzy użytkownika o nazwie `myNewUser` przy użyciu klucza SSH do uwierzytelniania na Maszynie wirtualnej o nazwie `myVM`:

```azurecli
az vm user update \
  --resource-group myResourceGroup \
  --name myVM \
  --username myNewUser \
  --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="delete-a-user"></a>Usuń użytkownika
W następującym przykładzie użytkownik o nazwie `myNewUser` na Maszynie wirtualnej o nazwie `myVM`:

```azurecli
az vm user delete \
  --resource-group myResourceGroup \
  --name myVM \
  --username myNewUser
```


## <a name="use-json-files-and-the-vmaccess-extension"></a>Pliki w formacie JSON i rozszerzenia VMAccess
W poniższych przykładach użyto nieprzetworzone pliki w formacie JSON. Użyj [zestaw rozszerzenia maszyny wirtualnej az](/cli/azure/vm/extension#set) następnie wywołać pliki w formacie JSON. Te pliki w formacie JSON również może być wywołana z szablonów platformy Azure. 

### <a name="reset-user-access"></a>Zresetuj dostęp użytkownika
W przypadku utraty dostępu do katalogu głównego na maszynie Wirtualnej systemu Linux, możesz uruchomić skrypt rozszerzenia VMAccess do zresetowania hasła lub klucza SSH użytkownika.

Aby zresetować klucz publiczny SSH użytkownika, Utwórz plik o nazwie `reset_ssh_key.json` i dodaj ustawienia w następującym formacie. Podstaw wartości dla `username` i `ssh_key` parametry:

```json
{
  "username":"azureuser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNGxxxxxx2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7xxxxxxwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5wxxtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== azureuser@myVM"
}
```

Wykonanie skryptu VMAccess:

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings reset_ssh_key.json
```

Aby zresetować hasło użytkownika, Utwórz plik o nazwie `reset_user_password.json` i dodaj ustawienia w następującym formacie. Podstaw wartości dla `username` i `password` parametry:

```json
{
  "username":"azureuser",
  "password":"myNewPassword" 
}
```

Wykonanie skryptu VMAccess:

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
Aby uruchomić ponownie demon SSH i zresetowanie konfiguracji SSH do wartości domyślnych, Utwórz plik o nazwie `reset_sshd.json`. Dodaj następującą zawartość:

```json
{
  "reset_ssh": true
}
```

Wykonanie skryptu VMAccess:

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

Aby utworzyć użytkownika, który używa klucza SSH do uwierzytelniania, Utwórz plik o nazwie `create_new_user.json` i dodaj ustawienia w następującym formacie. Podstaw wartości dla `username` i `ssh_key` parametry:

```json
{
  "username":"myNewUser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNG1vHY7P2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7iUo5IdwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5woYtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== myNewUser@myVM",
  "password":"myNewUserPassword"
}
```

Wykonanie skryptu VMAccess:

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings create_new_user.json
```

Aby usunąć użytkownika, Utwórz plik o nazwie `delete_user.json` i dodaj następującą zawartość. Zastąp wartość dla `remove_user` parametru:

```json
{
  "remove_user":"myNewUser"
}
```

Wykonanie skryptu VMAccess:

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings delete_user.json
```

### <a name="check-or-repair-the-disk"></a>Sprawdź i napraw dysk
Użyć rozszerzenia VMAccess można również Sprawdź i napraw dysku, który został dodany do maszyny Wirtualnej systemu Linux.

Sprawdź, a następnie napraw dysku, Utwórz plik o nazwie `disk_check_repair.json` i dodaj ustawienia w następującym formacie. Zastąp wartość dla nazwy `repair_disk`:

```json
{
  "check_disk": "true",
  "repair_disk": "true, mydiskname"
}
```

Wykonanie skryptu VMAccess:

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
Aktualizowanie systemu Linux przy użyciu rozszerzenia VMAccess Azure jest jedną metodę, aby wprowadzić zmiany w uruchomionej maszyny Wirtualnej systemu Linux. Aby zmodyfikować maszyny Wirtualnej systemu Linux na rozruch umożliwia także narzędzia, takie jak szablony usługi Azure Resource Manager i init chmury.

[Rozszerzenia maszyn wirtualnych i funkcji w systemie Linux](extensions-features.md)

[Tworzenie szablonów usługi Azure Resource Manager z rozszerzeniami maszyny Wirtualnej systemu Linux](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[Dostosowywanie maszyny Wirtualnej systemu Linux podczas tworzenia za pomocą init chmury](using-cloud-init.md)

