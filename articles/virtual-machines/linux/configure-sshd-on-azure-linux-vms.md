---
title: Skonfiguruj SSHD na maszynach wirtualnych Azure Linux | Dokumentacja firmy Microsoft
description: "Skonfiguruj SSHD do najlepszych rozwiązań dotyczących zabezpieczeń i blokady SSH do maszyn wirtualnych systemu Linux platformy Azure."
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 11/21/2016
ms.author: v-livech
ms.openlocfilehash: 0195c385b00ab92b2b92ce8ff00983a0d91bf3a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="configure-sshd-on-azure-linux-vms"></a>Skonfiguruj SSHD na maszynach wirtualnych systemu Linux platformy Azure

W tym artykule opisano, jak do blokowania SSH serwera w systemie Linux, aby zapewnić najlepsze rozwiązania w zakresie zabezpieczeń, a także aby przyspieszyć proces logowania SSH przy użyciu protokołu SSH kluczy zamiast hasła.  Do kontynuowania blokady SSHD zamierzamy można wyłączyć użytkownika głównego mogli się zalogować, ograniczyć użytkowników, którzy mogą zalogować się za pomocą listy zatwierdzonych grup, wyłączenie protokołu SSH w wersji 1, minimalna bitowego klucza i Konfigurowanie automatycznego wylogowaniu bezczynnych użytkowników.  Wymagania dotyczące tego artykułu: konto platformy Azure ([Pobierz bezpłatną wersję próbną](https://azure.microsoft.com/pricing/free-trial/)) i [SSH publiczne i prywatne pliki klucza](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="quick-commands"></a>Szybkie polecenia

Konfigurowanie `/etc/ssh/sshd_config` z następującymi ustawieniami:

### <a name="disable-password-logins"></a>Wyłącz hasło logowania

```bash
PasswordAuthentication no
```

### <a name="disable-login-by-the-root-user"></a>Wyłącz logowanie przez użytkownika głównego

```bash
PermitRootLogin no
```

### <a name="allowed-groups-list"></a>Dozwolona lista grup

```bash
AllowGroups wheel
```

### <a name="allowed-users-list"></a>Lista dozwolonych użytkowników

```bash
AllowUsers ahmet ralph
```

### <a name="disable-ssh-protocol-version-1"></a>Wyłączanie protokołu SSH w wersji 1

```bash
Protocol 2
```

### <a name="minimum-key-bits"></a>Minimalna bitów klucza

```bash
ServerKeyBits 2048
```

### <a name="disconnect-idle-users"></a>Odłącz bezczynnych użytkowników

```bash
ClientAliveInterval 300
ClientAliveCountMax 0
```

## <a name="detailed-walkthrough"></a>Szczegółowy przewodnik

SSHD to SSH serwer, który działa na Maszynie wirtualnej systemu Linux.  SSH jest klienta z systemem Windows z powłoki na Twoje MacBook stacji roboczej systemu Linux lub Bash.  SSH jest również protokół używany do zabezpieczania i szyfrowania komunikacji między tą stacją roboczą a maszyny Wirtualnej systemu Linux wprowadzania SSH także sieci VPN (wirtualna sieć prywatna).

W tym artykule jest bardzo ważne jedno logowanie do maszyny Wirtualnej systemu Linux otwarte dla całego przewodnika.  Po nawiązaniu połączenia SSH pozostaje jako otwartą sesję tak długo, jak okno nie jest zamknięty.  Posiadanie jednego terminala do zalogowania się zezwala na zmiany wprowadzone do usługi SSHD bez są zablokowane Jeśli podziału zostaną zmienione.  Jeśli maszyny Wirtualnej systemu Linux przerwane konfiguracji SSHD pobrać zablokowane, platforma Azure oferuje możliwość resetowania przerwane konfiguracji SSHD o [rozszerzenia dostępu do maszyny Wirtualnej Azure](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Z tego powodu otworzyć dwóch terminale i SSH do maszyny Wirtualnej systemu Linux z obu z nich.  Firma Microsoft przy użyciu terminala pierwszy wprowadź zmiany w pliku konfiguracji SSHDs i ponownie uruchomić usługę SSHD.  Firma Microsoft przy użyciu terminala drugi do testowania te zmiany po ponownym uruchomieniu usługi.  Ponieważ firma Microsoft wyłączania hasła SSH i zależne ściśle kluczy SSH, jeśli klucze SSH nie są prawidłowe, a następnie zamknij połączenie z maszyną wirtualną, maszyna wirtualna zostanie trwale zablokowane i nie będzie można do niego zalogować się do niego wymaganiem go do usunięty i utworzony ponownie.

## <a name="disable-password-logins"></a>Wyłącz hasło logowania

Jest najszybszym sposobem na zapewnienie maszyny Wirtualnej systemu Linux można wyłączyć hasło logowania.  Po włączeniu hasła logowania robotów przeszukiwania sieci web zostanie natychmiast start próby siłowych odgadnąć hasło dla maszyny Wirtualnej systemu Linux przy użyciu protokołu SSH.  Całkowite wyłączenie hasło logowania, umożliwia serwerowi SSH Ignoruj wszystkie próby logowania hasła.

```bash
PasswordAuthentication no
```

## <a name="disable-login-by-the-root-user"></a>Wyłącz logowanie przez użytkownika głównego

Następujące najlepsze rozwiązania w systemie Linux, `root` użytkownika nigdy nie powinny być rejestrowane w za pośrednictwem protokołu SSH lub przy użyciu `sudo su`.  Wszystkie polecenia wymagające uprawnień na poziomie głównym powinna być uruchamiana zawsze za pośrednictwem `sudo` polecenia, które rejestruje wszystkie akcje dla przyszłych inspekcji.  Wyłączanie `root` użytkownikom możliwość logowania za pośrednictwem SSH jest zabezpieczeń najlepsze rozwiązania w zakresie krokiem, który zapewnia tylko autoryzowani użytkownicy będą mogli SSH.

```bash
PermitRootLogin no
```

## <a name="allowed-groups-list"></a>Dozwolona lista grup

SSH udostępnia metody ograniczyć użytkowników i grupy, który ma być dozwolony lub niedozwolony logowanie za pomocą protokołu SSH.  Ta funkcja używa list na zatwierdzenie lub odrzucenie logowania konkretnych użytkowników i grup.  Ustawienie grupy koło `AllowGroups` listy ogranicza zatwierdzonych logowania za pomocą protokołu SSH tylko konta użytkowników, które znajdują się w grupie kółka.

```bash
AllowGroups wheel
```

## <a name="allowed-users-list"></a>Lista dozwolonych użytkowników

Ograniczenie logowania SSH do użytkowników po prostu jest bardziej szczegółowe sposobem wykonywać takie same zadanie, które `AllowGroups` jest.  

```bash
AllowUsers ahmet ralph
```

## <a name="disable-ssh-protocol-version-1"></a>Wyłączanie protokołu SSH w wersji 1

Protokół SSH w wersji 1 jest niebezpieczne i powinny być wyłączone.  Protokół SSH w wersji 2 jest bieżącej wersji, która zapewnia bezpieczny sposób SSH na serwerze.  Wyłączanie protokołu SSH w wersji 1 nie zezwala na wszystkich klientów SSH, które próbują nawiązać połączenie z serwerem SSH, przy użyciu protokołu SSH w wersji 1.  Połączeń SSH tylko w wersji 2 są dozwolone w celu negocjowania połączenia z serwerem SSH.

```bash
Protocol 2
```

## <a name="minimum-key-bits"></a>Minimalna bitów klucza

Następujące najlepsze rozwiązania w zakresie zabezpieczeń hasło logowania SSH są wyłączone, a tylko klucze SSH mogą służyć do uwierzytelniania z serwerem SSH.  Te klucze SSH mogą być tworzone przy użyciu różne długości klucza, liczony w bitach.  Najlepsze praktyki stanów to minimalne dopuszczalne siłę klucza klucze o długości 2048 bitów.  Klucze mniej niż 2048 bitów teoretycznie może być uszkodzony.  Ustawienie `ServerKeyBits` do `2048` umożliwia połączeń przy użyciu kluczy 2048 bitów lub większej i odmowy połączeń mniej niż 2048 bitów.

```bash
ServerKeyBits 2048
```

## <a name="disconnect-idle-users"></a>Odłącz bezczynnych użytkowników

SSH ma możliwość odłączyć użytkowników, którzy mają otwarte połączenia, które po okresie bezczynności przez ponad Ustaw okres czasu w sekundach.  Utrzymywanie otwartych sesji do tych użytkowników, którzy są aktywni ogranicza ryzyko maszyny Wirtualnej systemu Linux.

```bash
ClientAliveInterval 300
ClientAliveCountMax 0
```

## <a name="restart-sshd"></a>Uruchom ponownie SSHD

Aby włączyć ustawienia w `/etc/ssh/sshd_config` ponownie uruchomić proces SSHD, co spowoduje ponowne uruchomienie serwera SSH.  Okno terminalu, używaną do ponownego uruchomienia serwera SSH pozostają otwarte, bez utraty otwartych sesji SSH.  Aby przetestować nowy SSH ustawienia serwera za pomocą drugiego okno terminalu lub kartę.  Używanie osobnych terminal do testowania połączenia SSH umożliwia Przejdź wstecz i wprowadzenia dodatkowych zmian `/etc/ssh/sshd_config` w pierwszym terminalu bez jest zablokowane przez istotne zmiany SSHD.  

### <a name="on-redhat-centos-and-fedora"></a>Redhat, Centos i Fedora

```bash
service sshd restart
```

### <a name="on-debian--ubuntu"></a>Na Debian i Ubuntu

```bash
service ssh restart
```

## <a name="reset-sshd-using-azure-reset-access"></a>Resetuj SSHD przy użyciu resetowania Azure — dostęp

Jeśli użytkownik jest zablokowany z istotne zmiany w konfiguracji SSHD służy rozszerzenia dostępu do maszyny Wirtualnej platformy Azure do zresetowania konfiguracji SSHD do oryginalnej konfiguracji.

Wszystkie nazwy przykład zastąpić własnymi.

```azurecli
azure vm reset-access \
--resource-group myResourceGroup \
--name myVM \
--reset-ssh
```

## <a name="install-fail2ban"></a>Zainstaluj Fail2ban

Zdecydowanie zaleca się zainstalować i skonfigurować aplikacji typu open source Fail2ban, która blokuje kolejnych nieudanych prób logowania do maszyny Wirtualnej systemu Linux za pomocą protokołu SSH za pomocą siłowych.  Fail2ban dzienniki powtarzane nieudane próby logowania za pomocą protokołu SSH, a następnie tworzy reguły zapory, aby zablokować adres IP, który prób pochodzą z.

* [Strona główna Fail2ban](http://www.fail2ban.org/wiki/index.php/Main_Page)

## <a name="next-steps"></a>Następne kroki

Po skonfigurowaniu i zablokowane serwer SSH na maszynie Wirtualnej systemu Linux czy dodatkowe zabezpieczenia najlepsze rozwiązania, możesz skorzystać z.  

* [Zarządzanie użytkownikami, SSH i wyboru lub napraw dyski na maszynach wirtualnych systemu Linux platformy Azure przy użyciu rozszerzenia VMAccess](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

* [Szyfrowanie dysków na Maszynę wirtualną systemu Linux przy użyciu wiersza polecenia platformy Azure](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

* [Dostęp i większe bezpieczeństwo w szablonach usługi Azure Resource Manager](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
