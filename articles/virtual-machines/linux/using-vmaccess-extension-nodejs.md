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
# <a name="manage-users-ssh-and-check-or-repair-disks-on-azure-linux-vms-using-hello-vmaccess-extension-with-hello-azure-cli-10"></a>Zarządzanie użytkownikami, SSH i wyboru lub naprawy dysków na maszynach wirtualnych systemu Linux platformy Azure przy użyciu hello rozszerzenia VMAccess z hello Azure CLI w wersji 1.0
W tym artykule opisano, jak toouse hello Azure VMAcesss rozszerzenia toocheck lub naprawiania dysku, zresetuj dostęp użytkownika, zarządzanie kontami użytkowników lub zresetuj konfigurację SSHD hello w systemie Linux. wymaga artykułu Hello:

* konta platformy Azure ([skorzystaj z bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/));
* Witaj [interfejsu wiersza polecenia Azure](../../cli-install-nodejs.md) logowania `azure login`.
* Hello Azure CLI *musi znajdować się w* tryb usługi Azure Resource Manager `azure config mode arm`.


## <a name="cli-versions-toocomplete-hello-task"></a>Zadanie hello toocomplete wersje interfejsu wiersza polecenia
Można ukończyć powitalnych zadań przy użyciu jednej z hello następujące wersje interfejsu wiersza polecenia:

- [Azure CLI 1.0](#quick-commands)— nasze interfejsu wiersza polecenia dla hello classic i zasobów zarządzania wdrażania modeli (w tym artykule)
- [Azure CLI 2.0](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -naszej nowej generacji interfejsu wiersza polecenia dla modelu wdrażania zarządzania zasobów hello


## <a name="quick-commands"></a>Szybkie polecenia
Istnieją dwa sposoby toouse VMAccess na maszyny wirtualne systemu Linux:

* Przy użyciu hello Azure CLI 1.0 i hello wymagane parametry.
* Przy użyciu nieprzetworzone pliki w formacie JSON, które rozszerzenia VMAccess przetwarza i działa na.

W sekcji szybkich poleceń hello, zamierzamy toouse hello Azure CLI 1.0 `azure vm reset-access` metody. W hello poniższych przykładach poleceń Zastąp wartości hello, zawierających "przykładu" hello wartościami z własnego środowiska.

## <a name="create-a-resource-group-and-linux-vm"></a>Tworzenie grupy zasobów i maszyny Wirtualnej systemu Linux
```bash
azure group create myResourceGroup westus
```

## <a name="create-a-debian-vm"></a>Tworzenie Debian maszyny Wirtualnej
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

## <a name="reset-root-password"></a>Resetowanie hasła głównego
hasła głównego hello tooreset:

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -u root \
  -p myNewPassword
```

## <a name="ssh-key-reset"></a>Resetowanie klucza SSH
klucz SSH hello tooreset użytkownika innego niż główny:

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -u myAdminUser \
  -M ~/.ssh/id_rsa.pub
```

## <a name="create-a-user"></a>Utwórz użytkownika
toocreate użytkownika:

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -u myAdminUser \
  -p myAdminUserPassword
```

## <a name="remove-a-user"></a>Usuwanie użytkownika
```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -R myRemovedUser
```

## <a name="reset-sshd"></a>Resetuj SSHD
Konfiguracja SSHD hello tooreset:

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM
  -r
```


## <a name="detailed-walkthrough"></a>Szczegółowy przewodnik
### <a name="vmaccess-defined"></a>Rozszerzenia VMAccess zdefiniowane:
Witaj dysku na maszynie Wirtualnej systemu Linux są pokazywane błędy. Jakiś sposób resetowania hasła użytkownika root hello dla maszyny Wirtualnej systemu Linux lub przypadkowo usunięty klucz prywatny SSH. Jeśli który wystąpił w dni hello hello centrum danych, będzie konieczne toodrive, a następnie otwórz tooget KVM hello na powitania serwera konsoli. Witaj rozszerzenia Azure VMAccess można traktować jako przełącznika KVM, które pozwala tooaccess hello konsoli tooreset dostępu tooLinux przeprowadzania konserwacji poziomu dysku.

Aby hello uzyskać szczegółowe wskazówki, zamierzamy toouse hello długą formę rozszerzenia VMAccess, który używa nieprzetworzone pliki w formacie JSON.  Te pliki JSON rozszerzenia VMAccess również może być wywołana z szablonów platformy Azure.

### <a name="using-vmaccess-toocheck-or-repair-hello-disk-of-a-linux-vm"></a>Przy użyciu rozszerzenia VMAccess toocheck lub naprawy dysku hello maszyny wirtualnej systemu Linux
Za pomocą rozszerzenia VMAccess można wykonać fsck Uruchom na powitania dysku w obszarze maszyny Wirtualnej systemu Linux.  Można także zrobić wyboru dysku i naprawy dysku przy użyciu rozszerzenia VMAccess.

toocheck, a następnie napraw hello dysku należy użyć tego rozszerzenia VMAccess skryptu:

`disk_check_repair.json`

```json
{
  "check_disk": "true",
  "repair_disk": "true, user-disk-name"
}
```

Wykonanie skryptu VMAccess hello:

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path disk_check_repair.json
```

### <a name="using-vmaccess-tooreset-user-access-toolinux"></a>Przy użyciu rozszerzenia VMAccess tooreset użytkownika dostępu tooLinux
W przypadku utraty dostępu tooroot na maszynie Wirtualnej systemu Linux, można uruchomić rozszerzenia VMAccess skryptu tooreset hello głównego hasła.

hasła głównego hello tooreset, użyj tego skryptu VMAccess:

`reset_root_password.json`

```json
{
  "username":"root",
  "password":"myNewPassword"
}
```

Wykonanie skryptu VMAccess hello:

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path reset_root_password.json
```

klucz SSH hello tooreset użytkownika innego niż główny, użyj tego skryptu VMAccess:

`reset_ssh_key.json`

```json
{
  "username":"myAdminUser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNG1vHY7P2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7iUo5IdwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5woYtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== myAdminUser@myVM" 
}
```

Wykonanie skryptu VMAccess hello:

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path reset_ssh_key.json
```

### <a name="using-vmaccess-toomanage-user-accounts-on-linux"></a>Przy użyciu kont użytkowników toomanage VMAccess w systemie Linux
Rozszerzenia VMAccess jest skrypt w języku Python, które mogą być używane toomanage użytkowników na maszynie Wirtualnej systemu Linux bez logowania i przy użyciu sudo lub hello konta głównego.

toocreate użytkownika, użyj tego skryptu VMAccess:

`create_new_user.json`

```json
{
  "username":"myNewUser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNG1vHY7P2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7iUo5IdwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5woYtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== myNewUser@myVM",
  "password":"myNewUserPassword"
}
```

Wykonanie skryptu VMAccess hello:

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path create_new_user.json
```

toodelete użytkownika, użyj tego skryptu VMAccess:

`remove_user.json`

```json
{
  "remove_user":"myDeletedUser"
}
```

Wykonanie skryptu VMAccess hello:

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path remove_user.json
```

### <a name="using-vmaccess-tooreset-hello-sshd-configuration"></a>Za pomocą rozszerzenia VMAccess tooreset hello SSHD konfiguracji
Jeśli konfiguracja SSHD maszyn wirtualnych systemu Linux toohello zmiany i zamknij hello połączenia SSH przed zweryfikowaniem hello zmian, użytkownik może uniemożliwić SSH'ing ponownie.  Rozszerzenia VMAccess mogą być używane tooreset hello SSHD konfiguracji wstecz tooa znanej dobrej konfiguracji bez konieczności logowania się za pomocą protokołu SSH.

tooreset hello SSHD konfiguracji, użyj tego skryptu VMAccess:

`reset_sshd.json`

```json
{
  "reset_ssh": true
}
```

Wykonanie skryptu VMAccess hello:

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path reset_sshd.json
```

## <a name="next-steps"></a>Następne kroki
Aktualizowanie systemu Linux przy użyciu rozszerzenia VMAccess Azure jest jeden zmian toomake metody na uruchomionej maszyny Wirtualnej systemu Linux.  Umożliwia także takich narzędzi jak init chmury i toomodify szablonów Azure maszyny Wirtualnej systemu Linux na rozruchu.

[Temat funkcji i rozszerzeń maszyny wirtualnej](../windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[Tworzenie szablonów usługi Azure Resource Manager z rozszerzeniami maszyny Wirtualnej systemu Linux](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[Podczas tworzenia przy użyciu chmury init toocustomize Maszynę wirtualną systemu Linux](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

