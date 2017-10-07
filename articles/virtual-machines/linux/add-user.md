---
title: "aaaAdd tooa użytkownika maszyny Wirtualnej systemu Linux na platformie Azure | Dokumentacja firmy Microsoft"
description: "Dodaj użytkownika tooa maszyny Wirtualnej systemu Linux na platformie Azure."
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f8aa633b-8b75-45d7-b61d-11ac112cedd5
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/18/2016
ms.author: v-livech
ms.openlocfilehash: eed050154adf0cbed2c168e7aa675bd3ded85fcd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-user-tooan-azure-vm"></a>Dodaj użytkownika tooan maszyny Wirtualnej Azure
Jednym z pierwszego zadania hello na nowej maszyny Wirtualnej z systemem Linux jest toocreate nowego użytkownika.  W tym artykule, firma Microsoft przeprowadzenie Tworzenie konta użytkownika sudo, ustawienia hello hasła, dodawanie SSH kluczy publicznych, a na koniec użyj `visudo` sudo tooallow bez podania hasła.

Wymagania wstępne są: [konta platformy Azure](https://azure.microsoft.com/pricing/free-trial/), [kluczy publicznych i prywatnych SSH](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), grupy zasobów platformy Azure i hello Azure CLI zainstalowany i wyłączyć przy użyciu tryb usługi Resource Manager tooAzure `azure config mode arm`.

## <a name="quick-commands"></a>Szybkie polecenia
```bash
# Add a new user on RedHat family distros
sudo useradd -G wheel exampleUser

# Add a new user on Debian family distros
sudo useradd -G sudo exampleUser

# Set a password
sudo passwd exampleUser
Enter new UNIX password:
Retype new UNIX password:
passwd: password updated successfully

# Copy hello SSH Public Key toohello new user
ssh-copy-id -i ~/.ssh/id_rsa exampleuser@exampleserver

# Change sudoers tooallow no password
# Execute visudo as root tooedit hello /etc/sudoers file
visudo

# On RedHat family distros uncomment this line:
## Same thing without a password
# %wheel        ALL=(ALL)       NOPASSWD: ALL

# toothis
## Same thing without a password
%wheel        ALL=(ALL)       NOPASSWD: ALL

# On Debian family distros change this line:
# Allow members of group sudo tooexecute any command
%sudo   ALL=(ALL:ALL) ALL

# toothis
%sudo   ALL=(ALL) NOPASSWD:ALL

# Verify everything
# Verify hello SSH keys & User account
bill@slackware$ ssh -i ~/.ssh/id_rsa exampleuser@exampleserver

# Verify sudo access
sudo top
```

## <a name="detailed-walkthrough"></a>Szczegółowy przewodnik
### <a name="introduction"></a>Wprowadzenie
Jednym z hello pierwsze i najbardziej typowych zadań z nowym serwerze jest tooadd konta użytkownika.  Główny logowania powinny być wyłączone i nie należy używać konta głównego hello się z serwerem systemu Linux, tylko sudo.  Nadanie uprawnień przy użyciu funkcji sudo hello właściwy sposób tooadminister i użyj Linux eskalacji głównego użytkownika.

Za pomocą polecenia hello `useradd` dodajemy toohello konta użytkownika maszyny Wirtualnej systemu Linux.  Uruchomiona `useradd` modyfikuje `/etc/passwd`, `/etc/shadow`, `/etc/group`, i `/etc/gshadow`.  Dodajemy toohello flagi wiersza polecenia `useradd` polecenia tooalso dodać hello nowej toohello sudo odpowiednie grupy użytkowników w systemie Linux.  Nawet są jak `useradd` tworzy wejścia `/etc/passwd` nie daje hello nowego konta użytkownika hasła.  Tworzenie początkowej hasło dla nowego użytkownika hello przy użyciu prostego powitania `passwd` polecenia.  ostatni krok Hello jest toomodify hello sudo zasady tooallow polecenia tooexecute tego użytkownika z uprawnieniami sudo bez konieczności tooenter hasła dla każdego polecenia.  Zalogował się przy użyciu klucza prywatnego hello przyjęto, że konto użytkownika jest zabezpieczony przed nieupoważnione i będą tooallow sudo dostępu bez podania hasła.  

### <a name="adding-a-single-sudo-user-tooan-azure-vm"></a>Dodawanie tooan użytkownika sudo jednej maszyny Wirtualnej Azure
Zaloguj się za toohello maszyna wirtualna platformy Azure przy użyciu kluczy SSH.  Jeśli masz nie konfiguracji SSH publiczny dostęp do klucza, najpierw zostało wykonane w tym artykule [przy użyciu publicznego klucza uwierzytelniania za pomocą usługi Azure](http://link.to/article).  

Witaj `useradd` hello zadania po zakończeniu wykonywania polecenia:

* Utwórz nowe konto użytkownika
* Utwórz nową grupę użytkowników o hello samej nazwie
* Dodaj zbyt jest puste`/etc/passwd`
* Dodaj zbyt jest puste`/etc/gpasswd`

Witaj `-G` wiersza polecenia Flaga dodaje hello nowego konta toohello właściwego Linux grupy użytkowników nadanie hello nowego konta użytkownika uprawnień eskalacji głównego.

#### <a name="add-hello-user"></a>Dodaj użytkownika hello
```bash
# On RedHat family distros
sudo useradd -G wheel exampleUser

# On Debian family distros
sudo useradd -G sudo exampleUser
```

#### <a name="set-a-password"></a>Ustawienia hasła
Witaj `useradd` polecenie tworzy hello użytkownika i dodaje wpis tooboth `/etc/passwd` i `/etc/gpasswd` , ale faktycznie nie ustawia hasło hello.  Witaj hasło zostanie dodany wpis toohello przy użyciu hello `passwd` polecenia.

```bash
sudo passwd exampleUser
Enter new UNIX password:
Retype new UNIX password:
passwd: password updated successfully
```

Mamy teraz użytkownik z uprawnieniami sudo na powitania serwera.

### <a name="add-your-ssh-public-key-toohello-new-user-account"></a>Dodaj klucz publiczny SSH toohello nowe konto użytkownika
Na komputerze, użyj hello `ssh-copy-id` z hello nowe hasło.

```bash
ssh-copy-id -i ~/.ssh/id_rsa exampleuser@exampleserver
```

### <a name="using-visudo-tooallow-sudo-usage-without-a-password"></a>Użycie sudo tooallow visudo bez hasła
Przy użyciu `visudo` tooedit hello `/etc/sudoers` file dodaje kilka warstwy ochrony przed niepoprawnie modyfikowanie tego pliku ważne.  Podczas wykonywania `visudo`, hello `/etc/sudoers` plik jest zablokowany tooensure żaden inny użytkownik może wprowadzić zmiany, gdy jest aktywnie edytowany.  Witaj `/etc/sudoers` pliku jest również sprawdzane pod kątem błędów przez `visudo` podczas prób toosave lub zamknąć, więc nie można zapisać pliku sudoers przerwane.

Mamy już użytkowników w grupie poprawne hello dostępu sudo.  Teraz zamierzamy tooenable sudo toouse tych grup bez hasła.

```bash
# Execute visudo as root tooedit hello /etc/sudoers file
visudo

# On RedHat family distros uncomment this line:
## Same thing without a password
# %wheel        ALL=(ALL)       NOPASSWD: ALL

# toothis
## Same thing without a password
%wheel        ALL=(ALL)       NOPASSWD: ALL

# On Debian family distros change this line:
# Allow members of group sudo tooexecute any command
%sudo   ALL=(ALL:ALL) ALL

# toothis
%sudo   ALL=(ALL) NOPASSWD:ALL
```

### <a name="verify-hello-user-ssh-keys-and-sudo"></a>Sprawdź użytkownika hello ssh kluczy i operacji sudo
```bash
# Verify hello SSH keys & User account
ssh -i ~/.ssh/id_rsa exampleuser@exampleserver

# Verify sudo access
sudo top
```
