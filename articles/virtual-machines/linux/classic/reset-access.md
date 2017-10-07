---
title: "aaaReset hasła maszyny Wirtualnej systemu Linux i SSH klucz z hello interfejsu wiersza polecenia | Dokumentacja firmy Microsoft"
description: "Jak hello toouse rozszerzenia VMAccess z hello Azure interfejsu wiersza polecenia (CLI) tooreset maszyny Wirtualnej systemu Linux hasła lub klucza SSH, popraw konfigurację SSH hello i sprawdzanie spójności dysku"
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: d975eb70-5ff1-40d1-a634-8dd2646dcd17
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 11/16/2016
ms.author: cynthn
ms.openlocfilehash: 1650ad64fb982627ae9f90b1a8209bb56bac7004
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-a-linux-vm-password-or-ssh-key-fix-hello-ssh-configuration-and-check-disk-consistency-using-hello-vmaccess-extension"></a>Jak tooreset maszyny Wirtualnej systemu Linux hasła lub klucza SSH, popraw konfigurację SSH hello i sprawdzanie spójności dysku przy użyciu rozszerzenia VMAccess hello
Jeśli nie możesz połączyć tooa maszyny wirtualnej systemu Linux na platformie Azure z powodu zapomniane hasło, nieprawidłowy klucz Secure Shell (SSH) lub na problem z konfiguracją SSH hello, hello rozszerzenia VMAccessForLinux za pomocą hello Azure CLI tooreset hello hasła lub klucza SSH, napraw Witaj konfiguracji SSH i sprawdzanie spójności dysku. 

> [!IMPORTANT] 
> Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../resource-manager-deployment-model.md). W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia hello. Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager. Dowiedz się, jak za[wykonaj te czynności przy użyciu modelu Resource Manager hello](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess).

Hello wiersza polecenia platformy Azure, możesz za pomocą hello **zestaw rozszerzenia maszyny wirtualnej azure** polecenie poleceniach tooaccess interfejsu wiersza polecenia (Bash, terminali, wiersza polecenia). Uruchom **zestaw rozszerzenia maszyny wirtualnej azure pomocy** użycia szczegółowe rozszerzenia.

Z hello wiersza polecenia platformy Azure, możesz wykonać hello następujących zadań:

* [Resetowanie hasła hello](#pwresetcli)
* [Resetuj klucz SSH hello](#sshkeyresetcli)
* [Resetuj hello hasła i hello klucza SSH](#resetbothcli)
* [Utwórz nowe konto użytkownika sudo](#createnewsudocli)
* [Zresetuj konfigurację protokołu SSH hello](#sshconfigresetcli)
* [Usuń użytkownika](#deletecli)
* [Wyświetl stan hello hello rozszerzenia VMAccess](#statuscli)
* [Sprawdzanie spójności dodanych dysków](#checkdisk)
* [Napraw dodane dyski na maszynie Wirtualnej systemu Linux](#repairdisk)

## <a name="prerequisites"></a>Wymagania wstępne
Potrzebne są następujące hello toodo:

* Konieczne będzie zbyt[zainstalować hello Azure CLI](../../../cli-install-nodejs.md) i [połączenia subskrypcji tooyour](../../../xplat-cli-connect.md) toouse Azure zasoby skojarzone z Twoim kontem.
* Ustaw hello poprawny tryb hello klasycznego modelu wdrażania, wpisując hello następujące polecenie w wierszu polecenia hello:
    ``` 
        azure config mode asm
    ```
* Jeśli chcesz, aby tooreset jedną mają nowe hasło lub zestawu kluczy SSH. Jeśli konfiguracja protokołu SSH hello tooreset nie trzeba je.

## <a name="pwresetcli"></a>Resetowanie hasła hello
1. Utwórz plik na komputerze o nazwie PrivateConf.json z tych wierszy. Zastąp **myUserName** i  **myP@ssW0rd**  z własną nazwę użytkownika i hasło i ustawić własne datę wygaśnięcia.

    ```   
        {
        "username":"myUserName",
        "password":"myP@ssW0rd",
        "expiration":"2020-01-01"
        }
    ```
        
2. Uruchom to polecenie, zastępując nazwę hello maszyny wirtualnej dla **myVM**.

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* –-private-config-path PrivateConf.json
    ```

## <a name="sshkeyresetcli"></a>Resetuj klucz SSH hello
1. Utwórz plik o nazwie PrivateConf.json z tych zawartości. Zastąp hello **myUserName** i **mySSHKey** wartościami odpowiednimi informacjami.

    ```   
        {
        "username":"myUserName",
        "ssh_key":"mySSHKey"
        }
    ```
2. Uruchom to polecenie, zastępując nazwę hello maszyny wirtualnej dla **myVM**.
   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json

## <a name="resetbothcli"></a>Zresetuj zarówno hello hasła i hello klucza SSH
1. Utwórz plik o nazwie PrivateConf.json z tych zawartości. Zastąp hello **myUserName**, **mySSHKey** i  **myP@ssW0rd**  wartościami odpowiednimi informacjami.

    ``` 
        {
        "username":"myUserName",
        "ssh_key":"mySSHKey",
        "password":"myP@ssW0rd"
        }
    ```

2. Uruchom to polecenie, zastępując nazwę hello maszyny wirtualnej dla **myVM**.

    ```   
        azure vm extension set MyVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json
    ```

## <a name="createnewsudocli"></a>Utwórz nowe konto użytkownika sudo

Jeśli zapomnisz swoją nazwę użytkownika, można użyć rozszerzenia VMAccess toocreate nową z urzędem sudo hello. W takim przypadku hello istniejącej nazwy użytkownika i hasło nie zostaną zmodyfikowane.

toocreate nowego użytkownika sudo z dostępem do hasła, użyj skryptu hello w [resetowania hasła hello](#pwresetcli) i określić nową nazwę użytkownika hello.

toocreate nowego użytkownika sudo z dostępem klucza SSH, użyj skryptu hello w [klucza SSH hello resetowania](#sshkeyresetcli) i określić nową nazwę użytkownika hello.

Można również użyć [resetowania hasła hello i klucz SSH hello](#resetbothcli) toocreate nowego użytkownika z jednocześnie hasło i dostęp do klucza SSH.

## <a name="sshconfigresetcli"></a>Zresetuj konfigurację protokołu SSH hello
Jeśli konfiguracji SSH hello jest w stanie niepożądane, może również utracić toohello dostęp do maszyny Wirtualnej. Możesz użyć hello VMAccess rozszerzenia tooreset hello konfiguracji tooits domyślny stan. toodo tak, wystarczy, że klucz "reset_ssh" hello tooset zbyt "True". rozszerzenia Hello Uruchom ponownie serwer SSH hello, otwórz port SSH hello na maszynie Wirtualnej i zresetuj wartości toodefault konfiguracji SSH hello. konto użytkownika Hello (nazwa, hasło lub kluczy SSH) nie zostaną zmienione.

> [!NOTE]
> plik konfiguracji SSH Hello pobiera zresetować znajduje się w /etc/ssh/sshd_config.
> 
> 

1. Utwórz plik o nazwie PrivateConf.json z tą zawartością.

    ```   
        {
        "reset_ssh":"True"
        }
    ```

2. Uruchom to polecenie, zastępując nazwę hello maszyny wirtualnej dla **myVM**. 

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json
    ```

## <a name="deletecli"></a>Usuń użytkownika
Jeśli chcesz toodelete konto użytkownika, bez logowania do maszyny Wirtualnej toohello bezpośrednio, można użyć tego skryptu.

1. Utwórz plik o nazwie PrivateConf.json z tej zawartości, zastępując hello użytkownika nazwa tooremove dla **removeUserName**. 

    ```   
        {
        "remove_user":"removeUserName"
        }
    ```

2. Uruchom to polecenie, zastępując nazwę hello maszyny wirtualnej dla **myVM**. 

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json
    ```

## <a name="statuscli"></a>Wyświetl stan hello hello rozszerzenia VMAccess
Stan hello toodisplay hello rozszerzenia VMAccess, uruchom to polecenie.

```
        azure vm extension get
```

## <a name='checkdisk'></a>Sprawdzanie spójności dodanych dysków
fsck toorun na wszystkich dyskach na maszynie wirtualnej systemu Linux, potrzebne są następujące hello toodo:

1. Utwórz plik o nazwie PublicConf.json z tą zawartością. Sprawdź, czy dysk przyjmuje wartość typu boolean dla czy toocheck do niej dołączone dyski maszyny wirtualnej tooyour lub nie. 

    ```   
        {   
        "check_disk": "true"
        }
    ```

2. Uruchom ten tooexecute polecenie, zastępując nazwę hello maszyny wirtualnej dla **myVM**.

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --public-config-path PublicConf.json 
    ```

## <a name='repairdisk'></a>Napraw dyski
toorepair dysków, które nie są Instalowanie lub błędy konfiguracji instalacji, użyj hello VMAccess rozszerzenia tooreset hello instalacji konfiguracji na maszynie wirtualnej systemu Linux. Zastępowanie hello nazwę dysku dla **myDisk**.

1. Utwórz plik o nazwie PublicConf.json z tą zawartością. 

    ```   
        {
        "repair_disk":"true",
        "disk_name":"myDisk"
        }
    ```

2. Uruchom ten tooexecute polecenie, zastępując nazwę hello maszyny wirtualnej dla **myVM**.

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --public-config-path PublicConf.json
    ```

## <a name="next-steps"></a>Następne kroki
* Jeśli chcesz poleceń cmdlet programu Azure PowerShell toouse lub usługi Azure Resource Manager szablony tooreset hello hasła lub klucza SSH, popraw konfigurację SSH hello i sprawdzanie spójności dysku, zobacz hello [dokumentacją dotyczącą rozszerzenia VMAccess w serwisie GitHub](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess). 
* Można również użyć hello [portalu Azure](https://portal.azure.com) tooreset hello hasła lub klucza SSH maszyny wirtualnej systemu Linux wdrożonych w hello klasycznego modelu wdrażania. Nie można aktualnie użyć hello toothis portalu dla maszyny Wirtualnej systemu Linux wdrożonych w modelu wdrażania usługi Resource Manager hello.
* Zobacz [o rozszerzenia maszyny wirtualnej i funkcjach](../extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) więcej informacji o przy użyciu rozszerzeń maszyny Wirtualnej dla maszyn wirtualnych platformy Azure.

