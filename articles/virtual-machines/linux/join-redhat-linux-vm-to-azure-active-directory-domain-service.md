---
title: aaaJoin tooan maszyny Wirtualnej systemu Linux RedHat Azure Active Directory DS | Dokumentacja firmy Microsoft
description: "Jak toojoin tooan istniejącej maszyny Wirtualnej z RedHat Enterprise Linux 7 usługi Azure Active Directory domeny."
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: vlivech
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/14/2016
ms.author: v-livech
ms.openlocfilehash: f3ba3c764e253191753f1cc5fc8c3b85c53818af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="join-a-redhat-linux-vm-tooan-azure-active-directory-domain-service"></a>Dołącz do maszyny Wirtualnej systemu Linux RedHat tooan usług domenowych Azure Active Directory

W tym artykule opisano sposób toojoin tooan maszyny wirtualnej Red Hat Enterprise Linux (RHEL) 7 interfejsów Azure Active Directory domeny usług (AADDS) zarządzania domeny.  wymagania dotyczące Hello są:

- [Konto platformy Azure](https://azure.microsoft.com/pricing/free-trial/)

- [Pliki kluczy publicznych i prywatnych SSH](mac-create-ssh-keys.md)

- [Azure Active Directory Domain Services kontrolera domeny](../../active-directory-domain-services/active-directory-ds-getting-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="quick-commands"></a>Szybkie polecenia

_Przykładami należy zastąpić własnymi ustawieniami._

### <a name="switch-hello-azure-cli-tooclassic-deployment-mode"></a>Przełącznik wiersza polecenia platformy azure hello tooclassic wdrożeń w trybie

```azurecli
azure config mode asm
```

### <a name="search-for-a-rhel-version-and-image"></a>Wyszukaj RHEL wersji i obrazów

```azurecli
azure vm image list | grep "Red Hat"
```

### <a name="create-a-redhat-linux-vm"></a>Utwórz Redhat Linux VM

```azurecli
azure vm create myVM \
-o a879bbefc56a43abb0ce65052aac09f3__RHEL_7_2_Standard_Azure_RHUI-20161026220742 \
-g ahmet \
-p myPassword \
-e 22 \
-t "~/.ssh/id_rsa.pub" \
-z "Small" \
-l "West US"
```

### <a name="ssh-toohello-vm"></a>Toohello SSH maszyny Wirtualnej

```bash
ssh -i ~/.ssh/id_rsa ahmet@myVM
```

### <a name="update-yum-packages"></a>YUM pakietów aktualizacji

```bash
sudo yum update
```

### <a name="install-packages-needed"></a>Zainstaluj wymagane pakiety

```bash
sudo yum -y install realmd sssd krb5-workstation krb5-libs
```

Obecnie pakiety hello wymagane są zainstalowane na maszynie wirtualnej systemu Linux hello, następne zadanie hello jest domeny zarządzanej toohello toojoin hello maszyny wirtualnej.

### <a name="discover-hello-aad-domain-services-managed-domain"></a>Odnajdywanie domeny zarządzanej usług domenowych w usłudze AAD hello

```bash
sudo realm discover mydomain.com
```

### <a name="initialize-kerberos"></a>Inicjowanie protokołu kerberos

Upewnij się, że podajesz użytkownik, który należy toohello "AAD kontrolera domeny" Administratorzy. Tylko ci użytkownicy można przyłączyć do domeny zarządzanej toohello komputerów.

```bash
kinit ahmet@mydomain.com
```

### <a name="join-hello-machine-toohello-domain"></a>Dołącz do domeny toohello maszyny hello

```bash
sudo realm join --verbose mydomain.com -U 'ahmet@mydomain.com'
```

### <a name="verify-hello-machine-is-joined-toohello-domain"></a>Sprawdź, czy komputer hello jest toohello przyłączone do domeny

```bash
ssh -l ahmet@mydomain.com mydomain.cloudapp.net
```

## <a name="next-steps"></a>Następne kroki

* [Red Hat aktualizacji infrastruktury (RHUI) na żądanie Red Hat Enterprise Linux w maszynach wirtualnych na platformie Azure](update-infrastructure-redhat.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Konfigurowanie magazynu kluczy dla maszyn wirtualnych w usłudze Azure Resource Manager](key-vault-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Wdrażanie i zarządzanie maszynami wirtualnymi przy użyciu szablonów usługi Azure Resource Manager i hello wiersza polecenia platformy Azure](../linux/create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
