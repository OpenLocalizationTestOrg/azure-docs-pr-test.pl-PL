---
title: tooFreeBSD aaaIntroduction na platformie Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się więcej o używaniu maszyn wirtualnych FreeBSD na platformie Azure"
services: virtual-machines-linux
documentationcenter: 
author: KylieLiang
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 32b87a5f-d024-4da0-8bf0-77e233d1422b
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/28/2017
ms.author: kyliel
ms.openlocfilehash: 43ba7a70ed21e7fb8b331f4a26db0426e098c4aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toofreebsd-on-azure"></a>Wprowadzenie tooFreeBSD na platformie Azure
Ten temat zawiera omówienie uruchomienie maszyny wirtualnej FreeBSD na platformie Azure.

## <a name="overview"></a>Omówienie
FreeBSD platformy Microsoft Azure jest zaawansowane systemu operacyjnego używany toopower nowoczesnych serwery, komputery stacjonarne i osadzone platform.

Microsoft Corporation jest udostępnianie obrazów FreeBSD na platformie Azure z hello [Agent gościa maszyny Wirtualnej Azure](https://github.com/Azure/WALinuxAgent/) wstępnie skonfigurowane. Obecnie hello następujące wersje FreeBSD mogą używać jako obrazy przez firmę Microsoft:

- FreeBSD 10.3-wersja
- FreeBSD 11.0-wersja

Hello agent jest odpowiedzialny za komunikację między hello FreeBSD maszyny Wirtualnej i hello Azure fabric dla operacji, takich jak inicjowanie obsługi administracyjnej hello maszyny Wirtualnej przy pierwszym użyciu (nazwa użytkownika, hasło lub klucz SSH, nazwy hosta, itp.) i włączenie funkcji selektywnego rozszerzeń maszyny Wirtualnej.

Podobnie jak w przypadku przyszłych wersji FreeBSD strategii hello jest toostay bieżącego i Udostępnij hello najnowsze wersje wkrótce po ich opublikowaniu przez zespół inżynieryjny hello FreeBSD wersji.

## <a name="deploying-a-freebsd-virtual-machine"></a>Wdrażanie maszyny wirtualnej FreeBSD
Wdrażanie maszyny wirtualnej FreeBSD jest dość proste przy użyciu obrazu z hello Azure Marketplace z hello portalu Azure:

- [10.3 FreeBSD na hello Azure Marketplace](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd103/)
- [11.0 FreeBSD na hello Azure Marketplace](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/)

### <a name="create-a-freebsd-vm-through-azure-cli-20-on-freebsd"></a>Tworzenie maszyny Wirtualnej FreeBSD za pośrednictwem interfejsu wiersza polecenia platformy Azure 2.0 na FreeBSD
Najpierw należy tooinstall [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) chociaż następujące polecenia na komputerze FreeBSD.

```bash 
curl -L https://aka.ms/InstallAzureCli | bash
```

Jeśli bash nie jest zainstalowany na tym komputerze FreeBSD, uruchom następujące polecenie przed rozpoczęciem powitalne instalacji. 

```bash
sudo pkg install bash
```

Jeśli python nie jest zainstalowany na tym komputerze FreeBSD, uruchom następujące polecenia przed rozpoczęciem powitalne instalacji. 

```bash
sudo pkg install python35
cd /usr/local/bin 
sudo rm /usr/local/bin/python 
sudo ln -s /usr/local/bin/python3.5 /usr/local/bin/python
```

Podczas instalacji hello prośba `Modify profile tooupdate your $PATH and enable shell/tab completion now? (Y/n)`. Jeśli wybierzesz odpowiedź `y` , a następnie wprowadź `/etc/rc.conf` jako `a path tooan rc file tooupdate`, może spełniać hello problem `ERROR: [Errno 13] Permission denied`. tooresolve ten problem, należy udzielić hello zapisu toocurrent prawo użytkownika w odniesieniu do pliku hello `etc/rc.conf`.

Teraz możesz zalogować się na platformie Azure i utworzyć FreeBSD maszyny Wirtualnej. Poniżej znajduje się przykład toocreate 11.0 FreeBSD maszyny Wirtualnej. Możesz także dodać parametr hello `--public-ip-address-dns-name` z globalnie unikatowej nazwy DNS dla nowo utworzonego publicznego adresu IP. 

```azurecli
az login 
az group create --name myResourceGroup --location eastus
az vm create --name myFreeBSD11 \
    --resource-group myResourceGroup \
    --image MicrosoftOSTC:FreeBSD:11.0:latest \
    --admin-username azureuser \
    --generate-ssh-keys
```

Następnie możesz zalogować się tooyour FreeBSD maszyny Wirtualnej za pośrednictwem adresu ip hello wydrukowania w hello powyższych danych wyjściowych z wdrożenia. 

```bash
ssh azureuser@xx.xx.xx.xx -i /etc/ssh/ssh_host_rsa_key
```   

## <a name="vm-extensions-for-freebsd"></a>Rozszerzenia maszyny Wirtualnej dla FreeBSD
Poniżej przedstawiono obsługiwane rozszerzeń maszyny Wirtualnej w FreeBSD.

### <a name="vmaccess"></a>Rozszerzenia VMAccess
Witaj [VMAccess](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess) rozszerzenia można:

* Resetowanie hasła hello hello oryginalnego sudo użytkownika.
* Utwórz nowego użytkownika sudo z hello hasło.
* Ustaw klucz publiczny hosta hello kluczem hello podane.
* Resetuj klucz publiczny hosta hello podane podczas obsługi, jeśli nie zostanie podany klucz hosta hello maszyny Wirtualnej.
* Otwórz hello portu SSH (22) i przywrócić hello sshd_config, jeśli reset_ssh ustawiono tootrue.
* Usuń hello istniejącego użytkownika.
* Sprawdź dyski.
* Napraw dodanych dysków.

### <a name="customscript"></a>CustomScript
Witaj [CustomScript](https://github.com/Azure/azure-linux-extensions/tree/master/CustomScript) rozszerzenia można:

* Jeśli zostanie podana, Pobierz skrypty hello dostosowane z usługi Azure Storage lub magazynu publicznego zewnętrznego (na przykład GitHub).
* Uruchom skrypt punktu wejścia hello.
* Obsługuje wbudowanego polecenia.
* Konwertuj automatycznie dopasuje styl systemu Windows w powłoki i skryptów języka Python.
* Automatycznie Usuń BOM powłoki i skryptów języka Python.
* Ochrona poufnych danych w CommandToExecute.

> [!NOTE]
> Maszyna wirtualna FreeBSD obsługuje tylko wersję CustomScript 1.x przez teraz.  

## <a name="authentication-user-names-passwords-and-ssh-keys"></a>Uwierzytelniania: nazwy użytkowników, hasła i klucze SSH
Podczas tworzenia maszyny wirtualnej FreeBSD przy użyciu hello portalu Azure, musisz podać nazwę użytkownika, hasło lub klucz publiczny SSH.
Nazwy użytkownika podczas wdrażania maszyny wirtualnej FreeBSD na platformie Azure nie muszą być zgodne nazwy kont systemowych (UID < 100) znajduje się już w hello maszyny wirtualnej ("root", na przykład).
Aktualnie obsługiwana jest tylko hello RSA klucza SSH. Wielowierszowy klucz SSH musi zaczynać się od `---- BEGIN SSH2 PUBLIC KEY ----` się i kończyć `---- END SSH2 PUBLIC KEY ----`.

## <a name="obtaining-superuser-privileges"></a>Uzyskanie uprawnień administratora
Witaj konta użytkownika, które określono podczas wdrażania wystąpienia maszyny wirtualnej na platformie Azure jest uprzywilejowanego konta. Witaj pakietu sudo został zainstalowany w hello opublikowane FreeBSD obrazu.
Po zalogowano się za pomocą tego konta użytkownika, możesz uruchamiać polecenia jako główny przy użyciu składni polecenia hello.

```
$ sudo <COMMAND>
```

Powłoka głównego Opcjonalnie można uzyskać za pomocą `sudo -s`.

## <a name="known-issues"></a>Znane problemy
Witaj [Agent gościa maszyny Wirtualnej Azure](https://github.com/Azure/WALinuxAgent/) wersji 2.2.2 ma [znany problem] (https://github.com/Azure/WALinuxAgent/pull/517), która powoduje niepowodzenie udostępniania hello dla maszyny Wirtualnej FreeBSD na platformie Azure. Witaj poprawka została przechwycona przez [Agent gościa maszyny Wirtualnej Azure](https://github.com/Azure/WALinuxAgent/) wersji 2.2.3 i jego nowszych wersjach. 

## <a name="next-steps"></a>Następne kroki
* Przejdź za[portalu Azure Marketplace](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/) toocreate FreeBSD maszyny Wirtualnej.
* Toobring własne tooAzure FreeBSD, zapoznaj się zbyt[tworzenie i przekazywanie wirtualnego dysku twardego FreeBSD tooAzure](classic/freebsd-create-upload-vhd.md).
