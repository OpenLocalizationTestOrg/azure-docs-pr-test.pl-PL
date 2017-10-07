---
title: "aaaDisable hasła SSH dla maszyny Wirtualnej systemu Linux przez skonfigurowanie SSHD | Dokumentacja firmy Microsoft"
description: "Zabezpieczenia sieci maszyny Wirtualnej systemu Linux na platformie Azure przez wyłączenie hasło logowania SSH."
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: 
ms.assetid: 46137640-a7d2-40e5-a1e9-9effef7eb190
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/26/2016
ms.author: v-livech
ms.openlocfilehash: fb67b2f5b8b3bf2ba214858940b04f2ea9013fb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="disable-ssh-passwords-on-your-linux-vm-by-configuring-sshd"></a>Wyłącz konfigurując SSHD haseł SSH dla maszyny Wirtualnej systemu Linux
Ten artykuł skupia się na temat toolock dół hello logowania zabezpieczeń maszyny wirtualnej systemu Linux.  Zaraz po otwarciu hello portu SSH 22 robotów world toohello start próby toologin przez odgadnięcie hasła.  Wykonamy w tym artykule jest, wyłącz hasło logowania za pomocą protokołu SSH.  Całkowicie usuwając możliwości hello hasła toouse hello maszyny Wirtualnej systemu Linux są chronione przez ten typ metodą siłową wymusić ataku.  dodane Hello jest podwyższenia będzie skonfigurowanie SSHD Linux tooonly Zezwalaj logowania za pomocą kluczy publicznych i prywatnych SSH, znacznie Witaj najbezpieczniejszą tooLinux toologin sposób.  Hello możliwych kombinacji go wymagają klucza prywatnego tooguess hello jest olbrzymie i w związku z tym odradza robotów z nawet bothering kluczy SSH w życie toobrute tootry.

## <a name="goals"></a>Cele
* Skonfiguruj SSHD toodisallow:
  * Hasło nazwy logowania
  * Dane logowania użytkownika głównego
  * Odpowiedź na żądanie uwierzytelniania
* Skonfiguruj SSHD tooallow:
  * tylko logowania klucza SSH
* Uruchom ponownie SSHD jest nadal zalogowany
* Nowa konfiguracja SSHD hello testu

## <a name="introduction"></a>Wprowadzenie
[Definicja SSH](https://en.wikipedia.org/wiki/Secure_Shell)

SSHD jest hello SSH serwera, który jest uruchamiany na powitania maszyny Wirtualnej systemu Linux.  SSH jest klienta, który jest uruchamiany z powłoki na stacji roboczej MacBook lub Linux.  SSH jest również protokół hello używane toosecure i szyfrowania komunikacji hello między stacji roboczej i hello maszyny Wirtualnej systemu Linux.

W tym artykule jest bardzo ważne tookeep jeden tooyour logowania przeprowadzenie otwarte dla hello całej maszyny Wirtualnej systemu Linux.  Z tego powodu z obu z nich zostanie otwarty dwóch terminale i toohello SSH maszyny Wirtualnej systemu Linux.  Firma Microsoft będzie Użyj hello pierwszy terminali toomake hello zmiany tooSSHDs pliku konfiguracji i ponownie uruchom usługę SSHD hello.  Używamy hello drugi tootest terminali te zmiany po ponownym uruchomieniu usługi hello.  Ponieważ firma Microsoft wyłączania hasła SSH i zależne ściśle kluczy SSH, jeśli klucze SSH nie są prawidłowe i zamknąć hello połączenia toohello maszyny Wirtualnej, hello maszyny Wirtualnej zostanie trwale zablokowane i nie będzie możliwe toologin tooit wymaganiem go toobe usunięty i utworzony ponownie.

## <a name="prerequisites"></a>Wymagania wstępne
* [Tworzenie kluczy SSH w systemie Linux i komputerów Mac dla maszyn wirtualnych systemu Linux na platformie Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* Konto platformy Azure
  * [zakładania wersji próbnej](https://azure.microsoft.com/pricing/free-trial/)
  * [Witryna Azure Portal](http://portal.azure.com)
* Maszyny Wirtualnej systemu Linux działających na platformie azure
* SSH publicznych i prywatnych pary kluczy w`~/.ssh/`
* Klucz publiczny SSH w `~/.ssh/authorized_keys` na powitania maszyny Wirtualnej systemu Linux
* Prawa Sudo na powitania maszyny Wirtualnej
* Port 22 otwarte

## <a name="quick-commands"></a>Szybkie polecenia
*Indywidualny Administratorzy systemu Linux, po prostu chcących hello TLDR wersji zacznij tutaj.  Szczegółowy opis i krokach związanych z dla wszystkich pozostałych użytkowników, który chce hello pominąć tę sekcję.*

```bash
sudo vim /etc/ssh/sshd_config
```

Edytowanie pliku konfiguracji hello w następujący sposób:

```sh
# Change PasswordAuthentication toothis:
PasswordAuthentication no

# Change PubkeyAuthentication toothis:
PubkeyAuthentication yes

# Change PermitRootLogin toothis:
PermitRootLogin no

# Change ChallengeResponseAuthentication toothis:
ChallengeResponseAuthentication no
```

Uruchom ponownie usługę SSHD hello. Na podstawie Debian dystrybucjach:

```bash
sudo service ssh restart
```

Na podstawie Red Hat dystrybucjach:

```bash
sudo service sshd restart
```

## <a name="detailed-walk-through"></a>Szczegółowe krokach związanych z
Logowania toohello maszyny Wirtualnej systemu Linux na terminalu 1 (T1).  Logowania toohello maszyny Wirtualnej systemu Linux na terminalu 2 (T2).

Na T2 zamierzamy tooedit hello SSHD konfiguracji pliku.  

```bash
sudo vim /etc/ssh/sshd_config
```

W tym miejscu możemy edytować tylko hello ustawienia toodisable hasła i włączyć logowania do klucza SSH.  Istnieje wiele ustawień w tym pliku należy badania i zmienić toomake Linux & SSH jako bezpieczne, zgodnie z potrzebami.

#### <a name="disable-password-logins"></a>Wyłącz hasło logowania

```sh
# Change PasswordAuthentication toothis:
PasswordAuthentication no
```

#### <a name="enable-public-key-authentication"></a>Włącz uwierzytelnianie klucza publicznego

```sh
# Change PubkeyAuthentication toothis:
PubkeyAuthentication yes
```

#### <a name="disable-root-login"></a>Wyłącz logowanie głównego

```sh
# Change PermitRootLogin toothis:
PermitRootLogin no
```

#### <a name="disable-challenge-response-authentication"></a>Wyłącz uwierzytelnianie odpowiedź na żądanie
```sh
# Change ChallengeResponseAuthentication toothis:
ChallengeResponseAuthentication no
```

### <a name="restart-sshd"></a>Uruchom ponownie SSHD
Z powłoki hello T1 upewnij się, możesz nadal są rejestrowane w.  Jest to krytycznych, dlatego możesz nie być blokowane z maszyny Wirtualnej Jeśli klucze SSH nie są prawidłowe, ponieważ hasła są obecnie wyłączone.  Jeśli wszystkie ustawienia są niepoprawne na maszynie Wirtualnej systemu Linux można użyć T1 toofix sshd_config, nadal będziesz się logować i SSH będzie podtrzymywania połączenia hello podczas hello SSHD service ponownie.

Z T2 Uruchom:

##### <a name="on-hello-debian-family"></a>Na powitania Debian rodziny
```bash
sudo service ssh restart
```

##### <a name="on-hello-redhat-family"></a>Na powitania rodziny RedHat
```bash
sudo service sshd restart
```

Hasła są teraz wyłączone na chronić je przed prób logowania siłowych hasła maszyny Wirtualnej.  Z tylko SSH klucze dozwolone będą mogli toologin szybsze i bardziej bezpieczne.

