---
title: "aaaCreate SSH parę kluczy dla maszyn wirtualnych systemu Linux na platformie Azure | Dokumentacja firmy Microsoft"
description: "Bezpiecznie utwórz parę kluczy SSH, prywatny i publiczny, dla maszyn wirtualnych z systemem Linux."
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: 
ms.assetid: 34ae9482-da3e-4b2d-9d0d-9d672aa42498
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/08/2017
ms.author: rasquill
ms.openlocfilehash: c4c7cec77c9b48295f2a28c8179b30a4dc38a555
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-ssh-public-and-private-key-pair-for-linux-vms"></a>Tworzenie pary kluczy prywatnych i publicznych SSH dla maszyn wirtualnych z systemem Linux

W tym artykule opisano, jak toogenerate protocol w wersji 2 RSA publicznego i prywatnego klucza SSH pliku toouse pary maszyn wirtualnych systemu Linux.  Para kluczy SSH umożliwia tworzenie maszyn wirtualnych na platformie Azure, która domyślne toousing kluczy SSH do uwierzytelnienia, eliminując konieczność hello toolog haseł w.  Hasła można złamać, a następnie otwórz maszyn wirtualnych się tooguess atakami siłowymi toorelentless hasła. Maszyny wirtualne utworzone z szablonami platformy Azure lub hello `azure-cli` może zawierać klucz publiczny SSH jako część wdrożenia hello, usuwanie krok konfiguracji wdrożenia post wyłączenia hasło logowania SSH.

## <a name="quick-commands"></a>Szybkie polecenia

Uruchom hello poniższych poleceń z powłoki Bash, zastępując przykłady hello własne wyborów.

Domyślnie plik klucza publicznego SSH jest tworzony w folderze `~/.ssh/id_rsa.pub`. Po wyświetleniu monitu, za pomocą następującego polecenia hello, należy utworzyć toosecure "hasło" klucz prywatny. (hello hasło jest używane hasło tooencrypt klucz prywatny.)

```bash
ssh-keygen -t rsa -b 2048 
```

Dodaj klucz hello nowo utworzone za`ssh-agent`:

```bash
ssh-add ~/.ssh/id_rsa
```

> [!IMPORTANT] 
> Witaj powyżej pracy poleceń w systemach operacyjnych Linux prawie wszystkie dystrybucji, ale nie działać w kontenerach, jak hello środowiska może znacząco ograniczone. 

## <a name="detailed-walkthrough"></a>Szczegółowy przewodnik

Przy użyciu kluczy publicznych i prywatnych SSH jest hello Najprostszym sposobem toolog w tooyour serwerów z systemem Linux. [Kryptografia klucza publicznego](https://en.wikipedia.org/wiki/Public-key_cryptography) zapewnia znacznie bezpieczniejsze toolog sposób w tooyour Linux lub BSD wirtualna na platformie Azure niż hasła, które może być metodą siłową znacznie łatwiej.

> [!IMPORTANT]
> Klucz publiczny można udostępniać wszystkim, ale tylko Ty (lub lokalna infrastruktura zabezpieczeń) posiadasz klucz prywatny.  powinien mieć klucz prywatny SSH Hello [bardzo bezpieczne hasło](https://www.xkcd.com/936/) (źródło:[xkcd.com](https://xkcd.com)) toosafeguard go.  To hasło jest klucz prywatny SSH hello tylko tooaccess i **nie jest** hello hasło do konta użytkownika.  Po dodaniu klucza SSH tooyour Hasło szyfruje hello klucza prywatnego za pomocą 128-bitowego szyfrowania AES, dzięki czemu hello klucz prywatny jest bezużyteczny bez toodecrypt hasło hello go.  Jeśli osoba atakująca kraść klucz prywatny i że klucz nie ma hasła, będą mogli toouse to prywatnego klucza toolog w tooany serwerów, które mają hello odpowiadającym mu kluczem publicznym.  Zabezpieczenie klucza prywatnego hasłem zapewnia dodatkową warstwę ochronną dla infrastruktury na platformie Azure, a osoba niepowołana nie może go użyć.

W tym artykule tworzy protokołu SSH w wersji 2 RSA publicznego i prywatnego klucza pliki, które są zalecane w przypadku wdrożeń na powitania Menedżera zasobów.  *SSH-rsa* klucze są wymagane na powitania [portal](https://portal.azure.com) dla wdrożenia usługi Resource Manager i klasycznym.

## <a name="disable-ssh-passwords-by-using-ssh-keys"></a>Wyłączanie haseł SSH przy użyciu kluczy SSH

Platforma Azure wymaga, aby klucz publiczny i prywatny miały długość co najmniej 2048 bitów oraz format ssh-rsa. użycie kluczy toocreate hello `ssh-keygen`, która najpierw zadaje szereg pytań, a następnie zapisuje klucz prywatny i dopasowany klucz publiczny. Po utworzeniu maszyny Wirtualnej platformy Azure klucza publicznego hello jest kopiowana za`~/.ssh/authorized_keys`.  Kluczy SSH w `~/.ssh/authorized_keys` są używane toochallenge powitania klienta toomatch hello odpowiedni klucz prywatny na połączenia logowania SSH.  Po utworzeniu maszyny Wirtualnej systemu Linux na platformie Azure przy użyciu kluczy SSH do uwierzytelniania Azure konfiguruje hello SSHD toonot serwera Zezwalaj na hasło logowania, tylko kluczy SSH.  W związku z tym tworząc maszyn wirtualnych systemu Linux platformy Azure z kluczy SSH, można ułatwić hello bezpiecznego wdrażania maszyny Wirtualnej i zapisać samodzielnie hello typowej konfiguracji po wdrożeniu kroku wyłączenie hasła w pliku konfiguracyjnym sshd_config hello.

## <a name="using-ssh-keygen"></a>Korzystanie z programu ssh-keygen

To polecenie umożliwia utworzenie zabezpieczonej (zaszyfrowanej) pary kluczy SSH przy użyciu RSA 2048-bitowego i jest oznaczone jako tooeasily go zidentyfikować.  

SSH klucze są domyślnie przechowywane w hello `~/.ssh` katalogu.  Jeśli nie masz `~/.ssh` katalogu, hello `ssh-keygen` polecenie tworzy go dla Ciebie hello odpowiednie uprawnienia.

```bash
ssh-keygen \
-t rsa \
-b 2048 
```

*Opis polecenia*

`ssh-keygen`= hello program używany toocreate hello kluczy

`-t rsa`= Typ klucza toocreate, czyli formacie RSA hello [](https://en.wikipedia.org/Wiki/RSA_(cryptosystem) wikipedia

`-b 2048`= Liczba bitów klucza hello


## <a name="classic-portal-and-x509-certs"></a>Portal klasyczny i certyfikaty X.509

Jeśli używasz hello Azure [klasyczny portal](https://manage.windowsazure.com/), wymaga certyfikatów X.509 hello kluczy SSH.  Nie są dozwolone żadne inne typy publicznych kluczy SSH — *muszą* to być certyfikaty X.509.

toocreate certyfikatu X.509 z istniejącego klucza prywatnego SSH-RSA:

```bash
openssl req -x509 \
-key ~/.ssh/id_rsa \
-nodes \
-days 365 \
-newkey rsa:2048 \
-out ~/.ssh/id_rsa.pem
```

## <a name="classic-deploy-using-asm"></a>Wdrażanie klasyczne przy użyciu programu `asm`

Jeśli używasz klasycznego hello wdrożyć model (Zarządzanie usługą Azure CLI `asm`), można użyć klucza publicznego SSH-RSA lub sformatowany RFC4716 klucza w **PEM** kontenera.  klucz publiczny SSH-RSA Hello jest co został utworzony we wcześniejszej części tego artykułu przy użyciu `ssh-keygen`.

toocreate RFC4716 sformatowany klucza z istniejącego klucza publicznego SSH:

```bash
ssh-keygen \
-f ~/.ssh/id_rsa.pub \
-e \
-m RFC4716 > ~/.ssh/id_ssh2.pem
```

## <a name="example-of-ssh-keygen"></a>Przykład polecenia ssh-keygen

```bash
ssh-keygen -t rsa -b 2048 -C "ahmet@myserver"
Generating public/private rsa key pair.
Enter file in which toosave hello key (/home/ahmet/.ssh/id_rsa): 
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/ahmet/.ssh/id_rsa.
Your public key has been saved in /home/ahmet/.ssh/id_rsa.pub.
hello key fingerprint is:
14:a3:cb:3e:78:ad:25:cc:55:e9:0c:08:e5:d1:a9:08 ahmet@myserver
hello keys randomart image is:
+--[ RSA 2048]----+
|        o o. .   |
|      E. = .o    |
|      ..o...     |
|     . o....     |
|      o S =      |
|     . + O       |
|      + = =      |
|       o +       |
|        .        |
+-----------------+
```

Zapisane pliki klucza:

`Enter file in which toosave hello key (/home/ahmet/.ssh/id_rsa): ~/.ssh/id_rsa`

Nazwa pary kluczy Hello tego artykułu.  Para kluczy o nazwie **id_rsa** jest domyślnym hello i niektóre narzędzia mogą wymagać hello **id_rsa** nazwę pliku klucza prywatnego, dobrym pomysłem jest o jeden. katalog Hello `~/.ssh/` jest hello domyślna lokalizacja dla par kluczy SSH i pliku konfiguracyjnego SSH hello.  Jeśli nie zostanie określony z pełną ścieżką `ssh-keygen` będzie utworzyć klucze hello w hello bieżący katalog roboczy, nie hello domyślne `~/.ssh`.

Lista hello `~/.ssh` katalogu.

```bash
ls -al ~/.ssh
-rw------- 1 ahmet staff  1675 Aug 25 18:04 id_rsa
-rw-r--r-- 1 ahmet staff   410 Aug 25 18:04 rsa.pub
```

Hasło klucza:

`Enter passphrase (empty for no passphrase):`

`ssh-keygen`odwołuje się klucz prywatny tooencrypt hello tooa hasło używane jako "hasło".  Jest *silnie* zalecane tooadd pary kluczy tooyour hasło. Bez hasła ochrona powitalnych klucz prywatny każda osoba mająca hello plik klucza może być używany toolog w tooany serwera, który ma hello odpowiadającym mu kluczem publicznym. Dodawanie hasło oferuje lepszą ochronę w przypadku, gdy osoba niepowołana jest w stanie toogain dostępu tooyour pliku klucza prywatnego, umożliwiając czasu toochange hello klucze tooauthenticate użytkownik.

## <a name="using-ssh-agent-toostore-your-private-key-password"></a>Przy użyciu hasła klucza prywatnego ssh-agent toostore

hasło pliku tooavoid wpisanie klucza prywatnego przy każdym logowaniu przez protokół SSH, można użyć `ssh-agent` toocache hasło pliku klucza prywatnego. Jeśli używasz Mac hello łańcucha kluczy systemu OS x przechowuje bezpiecznego hasła do klucza prywatnego powitania po wywołaniu `ssh-agent`.

Sprawdź i użyj `ssh-agent` i `ssh-add` tooinform hello systemu SSH o hello pliki klucza, aby hasło hello nie będzie używane w trybie interakcyjnym toobe.

```bash
eval "$(ssh-agent -s)"
```

Teraz Dodaj klucz prywatny hello zbyt`ssh-agent` za pomocą polecenia hello `ssh-add`.

```bash
ssh-add ~/.ssh/id_rsa
```

hasło klucza prywatnego Hello są obecnie przechowywane w `ssh-agent`.

## <a name="using-ssh-copy-id-tooinstall-hello-new-key"></a>Przy użyciu `ssh-copy-id` tooinstall hello nowego klucza
Jeśli utworzono już Maszynę wirtualną można zainstalować z hello następujące polecenie, zastępując hello maszyny Wirtualnej użytkownika i adres serwera hello własne wartości hello nowe SSH publicznego klucza tooyour maszyny Wirtualnej systemu Linux:

```bash
ssh-copy-id -i ~/.ssh/id_rsa.pub ahmet@myserver
```

## <a name="create-and-configure-an-ssh-config-file"></a>Tworzenie i konfigurowanie pliku konfiguracyjnego SSH

Jest najlepszym toocreate praktyki i skonfigurować `~/.ssh/config` toospeed pliku na górę logowania i optymalizacji Twoje zachowanie klienta SSH.

Poniższy przykład Hello pokazano standardową konfigurację.

### <a name="create-hello-file"></a>Utwórz plik hello

```bash
touch ~/.ssh/config
```

### <a name="edit-hello-file-tooadd-hello-new-ssh-configuration"></a>Edytuj hello pliku tooadd hello nową konfigurację SSH:

```bash
vim ~/.ssh/config
```

### <a name="example-sshconfig-file"></a>Przykład pliku `~/.ssh/config`:

```bash
# Azure Keys
Host fedora22
  Hostname 102.160.203.241
  User ahmet
# ./Azure Keys
# Default Settings
Host *
  PubkeyAuthentication=yes
  IdentitiesOnly=yes
  ServerAliveInterval=60
  ServerAliveCountMax=30
  ControlMaster auto
  ControlPath ~/.ssh/SSHConnections/ssh-%r@%h:%p
  ControlPersist 4h
  IdentityFile ~/.ssh/id_rsa
```

To konfiguracji SSH umożliwia możesz sekcje dla każdego serwera tooenable każdego toohave własnej pary kluczy. Witaj ustawienia domyślne (`Host *`) są przeznaczone dla wszystkich hostach, które nie należy do żadnej hello określonych hostach w górę w pliku konfiguracyjnym hello.

### <a name="config-file-explained"></a>Opis pliku konfiguracji

`Host`= Nazwa hello hello hosta wywołanego na powitania w terminalu.  `ssh fedora22`Określa, że `SSH` toouse hello wartości w bloku ustawienia hello etykietą `Host fedora22` Uwaga: Host może być jakakolwiek etykieta jest dla Ciebie, który nie reprezentuje hello rzeczywiste nazwą hosta żadnego serwera.

`Hostname 102.160.203.241`= hello adres IP lub nazwa DNS serwera hello.

`User ahmet`= toouse konta użytkownika zdalnego hello podczas logowania się na serwerze toohello.

`PubKeyAuthentication yes`= informuje protokół SSH, mają toouse toolog klucza SSH.

`IdentityFile /home/ahmet/.ssh/id_id_rsa`= klucza prywatnego SSH hello i odpowiednie toouse klucza publicznego dla uwierzytelniania.

## <a name="ssh-into-linux-without-a-password"></a>Korzystanie z protokołu SSH w systemie Linux bez użycia hasła

Teraz, gdy masz parę kluczy SSH i skonfigurowany plik konfiguracji SSH są możliwe toolog w tooyour maszyny Wirtualnej systemu Linux szybkie i bezpieczne. powitania po raz pierwszy logujesz się tooa serwera przy użyciu hello klucza SSH polecenie monituje możesz dla hello hasło dla tego pliku klucza.

```bash
ssh fedora22
```

### <a name="command-explained"></a>Opis polecenia

Gdy `ssh fedora22` jest wykonywany SSH najpierw lokalizuje i ładuje wszystkie ustawienia z hello `Host fedora22` bloku, a następnie obciążeń hello wszystkie pozostałe ustawienia z ostatniego bloku hello `Host *`.

## <a name="next-steps"></a>Następne kroki

Następnie się jest toocreate maszyn wirtualnych systemu Linux platformy Azure przy użyciu nowego klucza publicznego hello SSH.  Maszyny wirtualne platformy Azure utworzonych za pomocą klucza publicznego SSH jako hello logowania są lepiej zabezpieczone niż maszyny wirtualne utworzone przy użyciu metody logowania hello domyślne hasła.  W domyślnej konfiguracji maszyn wirtualnych platformy Azure utworzonych przy użyciu kluczy SSH hasła są wyłączone, aby uniknąć prób odgadnięcia hasła za pomocą ataków siłowych. Jeśli potrzebujesz więcej pomocy podczas tworzenia Twojej pary kluczy SSH, lub wymagać dodatkowych certyfikatów, takie jak w przypadku użycia z klasycznego portalu hello, zobacz [szczegółowe kroki par kluczy SSH toocreate i certyfikaty](create-ssh-keys-detailed.md).

* [Tworzenie bezpiecznej maszyny wirtualnej systemu Linux przy użyciu szablonu platformy Azure](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Tworzenie bezpiecznej maszyny Wirtualnej systemu Linux przy użyciu hello portalu Azure](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Tworzenie bezpiecznej maszyny Wirtualnej systemu Linux przy użyciu hello wiersza polecenia platformy Azure](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
