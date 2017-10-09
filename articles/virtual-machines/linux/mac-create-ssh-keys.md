---
title: "aaaCreate i używanie SSH parę kluczy dla maszyn wirtualnych systemu Linux na platformie Azure | Dokumentacja firmy Microsoft"
description: "Jak toocreate i używanie SSH publiczne i prywatne parę kluczy dla maszyn wirtualnych systemu Linux w Azure tooimprove hello zabezpieczeń hello procesu uwierzytelniania."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 34ae9482-da3e-4b2d-9d0d-9d672aa42498
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/14/2017
ms.author: iainfou
ms.openlocfilehash: 7fb94841d34d5bc006f3134adf91102ddce5f174
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-use-an-ssh-public-and-private-key-pair-for-linux-vms-in-azure"></a>Jak skojarzyć toocreate i użyj klucz publiczny i prywatny SSH dla maszyn wirtualnych systemu Linux na platformie Azure
Z pary kluczy bezpiecznej powłoki (SSH) można utworzyć na platformie Azure, która używania kluczy SSH w celu uwierzytelniania, eliminując konieczność hello toolog haseł w maszynach wirtualnych (VM). W tym artykule opisano, jak tooquickly Generowanie i używanie parę pliku klucza publicznego i prywatnego RSA w wersji 2 protokołu SSH dla maszyn wirtualnych systemu Linux. Aby uzyskać bardziej szczegółowe kroki i dodatkowe przykłady, zobacz [szczegółowe kroki par kluczy SSH toocreate i certyfikaty](create-ssh-keys-detailed.md).

## <a name="create-an-ssh-key-pair"></a>Tworzenie pary kluczy SSH
Użyj hello `ssh-keygen` polecenia toocreate SSH publicznego i prywatnego klucza pliki, które są domyślnie tworzone w hello `~/.ssh` katalogu, ale można określić inną lokalizację i hasło dodatkowe (hasło tooaccess hello plik klucza prywatnego) po zostanie wyświetlony monit. Uruchom następujące polecenie z powłoki Bash hello, udzielenie odpowiedzi na powitania monity z odpowiednimi informacjami.

```bash
ssh-keygen -t rsa -b 2048
```

## <a name="use-hello-ssh-key-pair"></a>Para kluczy SSH hello
Witaj klucz publiczny, który można umieścić na maszynie Wirtualnej systemu Linux na platformie Azure są domyślnie przechowywane w `~/.ssh/id_rsa.pub`, chyba że zostaną zmienione lokalizacji powitania po ich utworzeniu. Jeśli używasz hello [Azure CLI 2.0](/cli/azure) toocreate maszyny Wirtualnej, określ lokalizację hello tego klucza publicznego, gdy używasz hello [tworzenia maszyny wirtualnej az](/cli/azure/vm#create) z hello `--ssh-key-path` — opcja. Jeśli skopiuj i Wklej zawartość hello hello toouse pliku klucza publicznego w hello portalu Azure lub w szablonie usługi Resource Manager, upewnij się, że nie należy skopiować wszystkie dodatkowe odstępu. Na przykład, jeśli używasz OS X, można przekazać pliku klucza publicznego hello (domyślnie **~/.ssh/id_rsa.pub**) zbyt**pbcopy** toocopy hello zawartość (istnieją inne programy systemu Linux, które hello samo, takich jak `xclip`).

Jeśli nie znasz kluczy publicznych SSH, możesz wyświetlić swój klucz publiczny, uruchamiając polecenie `cat` w następujący sposób i zastępując ścieżkę `~/.ssh/id_rsa.pub` lokalizacją własnego pliku klucza publicznego:

```bash
cat ~/.ssh/id_rsa.pub
```

Z użyciem klucza publicznego hello na maszynie Wirtualnej Azure, SSH tooyour maszynę Wirtualną przy użyciu hello adres IP lub nazwę DNS maszyny wirtualnej (Pamiętaj tooreplace `azureuser` i `myvm.westus.cloudapp.azure.com` poniżej z hello nazwa użytkownika i nazwy FQDN hello--lub adres IP adresów):

```bash
ssh azureuser@myvm.westus.cloudapp.azure.com
```

Jeśli podano hasło podczas tworzenia Twojej parę kluczy, wprowadź hasło powitania po wyświetleniu monitu w procesie logowania hello. (hello serwer jest dodawany tooyour `~/.ssh/known_hosts` folderu, a nie będzie pytany tooconnect ponownie do czasu klucza publicznego hello na zmiany maszyny Wirtualnej platformy Azure lub nazwa serwera hello jest usuwany z `~/.ssh/known_hosts`.)

## <a name="next-steps"></a>Następne kroki

Maszyny wirtualne utworzone za pomocą kluczy SSH są domyślnie skonfigurowane przy użyciu haseł wyłączone, toomake metodą siłową odgadnięcie prób znacznie droższe i w związku z tym trudne. W tym temacie opisano tworzenie prostej pary kluczy SSH do szybkiego używania. Jeśli potrzebujesz więcej pomocy podczas tworzenia Twojej pary kluczy SSH, lub wymagać dodatkowych certyfikatów, zobacz [szczegółowe kroki par kluczy SSH toocreate i certyfikaty](create-ssh-keys-detailed.md).

Można tworzyć maszyn wirtualnych korzystających z pary kluczy SSH za pomocą hello portalu Azure, interfejsu wiersza polecenia i szablony:

* [Tworzenie bezpiecznej maszyny Wirtualnej systemu Linux przy użyciu hello portalu Azure](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Tworzenie bezpiecznej maszyny Wirtualnej systemu Linux przy użyciu hello Azure CLI 2.0)](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Tworzenie bezpiecznej maszyny wirtualnej systemu Linux przy użyciu szablonu platformy Azure](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
