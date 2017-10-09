---
title: aaaConfigure SSHD na maszynach wirtualnych systemu Linux platformy Azure | Dokumentacja firmy Microsoft
description: "Skonfiguruj SSHD najlepszych rozwiązań dotyczących zabezpieczeń i toolockdown SSH tooAzure maszyn wirtualnych systemu Linux."
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
ms.openlocfilehash: c2361be7199a24b129c06acfc899dd32f6e1d6fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-sshd-on-azure-linux-vms"></a>Skonfiguruj SSHD na maszynach wirtualnych systemu Linux platformy Azure

W tym artykule opisano, jak toolockdown hello serwera SSH w systemie Linux, tooprovide najlepsze rozwiązania w zakresie zabezpieczeń, a także toospeed proces logowania SSH hello przy użyciu kluczy SSH zamiast hasła.  blokady toofurther SSHD zamierzamy toodisable hello głównego użytkownika przed toologin można ograniczyć hello użytkowników, którzy mogą toologin za pośrednictwem listy zatwierdzonych grupy wyłączenie protokołu SSH w wersji 1, minimalna bitowego klucza i Konfigurowanie automatycznego wylogowaniu bezczynnych użytkowników.  wymagania Hello w tym artykule są: konto platformy Azure ([Pobierz bezpłatną wersję próbną](https://azure.microsoft.com/pricing/free-trial/)) i [SSH publiczne i prywatne pliki klucza](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="quick-commands"></a>Szybkie polecenia

Konfigurowanie `/etc/ssh/sshd_config` z hello następujące ustawienia:

### <a name="disable-password-logins"></a>Wyłącz hasło logowania

```bash
PasswordAuthentication no
```

### <a name="disable-login-by-hello-root-user"></a>Wyłącz logowanie przez użytkownika głównego hello

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

SSHD jest hello SSH serwera, który jest uruchamiany na powitania maszyny Wirtualnej systemu Linux.  SSH jest klienta z systemem Windows z powłoki na Twoje MacBook stacji roboczej systemu Linux lub Bash.  SSH jest również protokół hello używane toosecure i szyfrowania komunikacji hello między stacji roboczej i hello maszyny Wirtualnej systemu Linux wprowadzania SSH także sieci VPN (wirtualna sieć prywatna).

W tym artykule jest bardzo ważne tookeep jedno logowanie tooyour maszyny Wirtualnej systemu Linux Otwórz dla całego przewodnika hello.  Po nawiązaniu połączenia SSH pozostaje jako otwartą sesję tak długo, jak hello okno nie jest zamknięty.  Posiadanie jednego terminala zalogowany, umożliwia toohello toobe wprowadzone zmiany SSHD service bez są zablokowane, jeśli wprowadzono zmianę podziału.  Jeśli maszyny Wirtualnej systemu Linux przerwane konfiguracji SSHD pobrać zablokowane, platforma Azure oferuje tooreset możliwości hello przerwane konfiguracji SSHD z hello [rozszerzenia dostępu do maszyny Wirtualnej Azure](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Z tego powodu otworzyć dwóch terminale i toohello SSH maszyny Wirtualnej systemu Linux z obu z nich.  Firma Microsoft może Użyj hello pierwszy terminali toomake hello zmiany tooSSHDs pliku konfiguracji, a następnie ponownie uruchom usługę SSHD hello.  Używamy hello drugi tootest terminali te zmiany po ponownym uruchomieniu usługi hello.  Ponieważ firma Microsoft wyłączania hasła SSH i zależne ściśle kluczy SSH, jeśli klucze SSH nie są prawidłowe i zamknąć hello połączenia toohello maszyny Wirtualnej, hello maszyny Wirtualnej zostanie trwale zablokowane i nie będzie możliwe toologin tooit wymaganiem go toobe usunięty i utworzony ponownie.

## <a name="disable-password-logins"></a>Wyłącz hasło logowania

Witaj najszybszy sposób toosecure maszyny Wirtualnej systemu Linux jest toodisable hasło logowania.  Po włączeniu hasła logowania robotów przeszukiwania hello sieci web natychmiast rozpocznie się próba toobrute wymusić wynik hello hasła dla maszyny Wirtualnej systemu Linux przy użyciu protokołu SSH.  Wyłączenie całkowicie hasło logowania, włącza hello SSH serwera tooignore wszystkich prób logowania hasła.

```bash
PasswordAuthentication no
```

## <a name="disable-login-by-hello-root-user"></a>Wyłącz logowanie przez użytkownika głównego hello

Następujące najlepsze rozwiązania w systemie Linux, hello `root` użytkownika nigdy nie powinny być rejestrowane w za pośrednictwem protokołu SSH lub przy użyciu `sudo su`.  Wszystkie polecenia wymagające uprawnień na poziomie głównym powinna być uruchamiana zawsze za pośrednictwem hello `sudo` polecenia, które rejestruje wszystkie akcje dla przyszłych inspekcji.  Wyłączanie hello `root` użytkownikom możliwość logowania za pośrednictwem SSH jest zabezpieczeń najlepsze rozwiązania w zakresie krokiem, który zapewnia tooSSH mogą tylko autoryzowani użytkownicy.

```bash
PermitRootLogin no
```

## <a name="allowed-groups-list"></a>Dozwolona lista grup

SSH udostępnia metody ograniczyć użytkowników i grupy, który ma być dozwolony lub niedozwolony logowanie za pomocą protokołu SSH.  Ta funkcja korzysta z list tooapprove lub uniemożliwić logowanie konkretnych użytkowników i grup.  Ustawienie hello kółka grupy toohello `AllowGroups` listy ogranicza zatwierdzonych logowania za pośrednictwem SSH toojust użytkownika konta, które znajdują się w grupie kółka hello.

```bash
AllowGroups wheel
```

## <a name="allowed-users-list"></a>Lista dozwolonych użytkowników

Ograniczenie dostępu użytkowników toojust logowania SSH jest bardziej szczegółowe sposób tooaccomplish hello sam zadanie, które `AllowGroups` jest.  

```bash
AllowUsers ahmet ralph
```

## <a name="disable-ssh-protocol-version-1"></a>Wyłączanie protokołu SSH w wersji 1

Protokół SSH w wersji 1 jest niebezpieczne i powinny być wyłączone.  Protokołu SSH w wersji 2 jest hello bieżącej wersji, która udostępnia serwer tooyour tooSSH bezpieczny sposób.  Wyłączanie protokołu SSH w wersji 1 nie zezwala na wszystkich klientów SSH, które próbujesz tooestablish połączenie z serwerem SSH hello przy użyciu protokołu SSH w wersji 1.  Tylko połączeń SSH w wersji 2 są dozwolone toonegotiate połączenia z serwerem SSH hello.

```bash
Protocol 2
```

## <a name="minimum-key-bits"></a>Minimalna bitów klucza

Następujące najlepsze rozwiązania w zakresie zabezpieczeń hasło logowania SSH są wyłączone i tylko klucze SSH mogą toobe używanych tooauthenticate z serwerem SSH hello.  Te klucze SSH mogą być tworzone przy użyciu różne długości klucza, liczony w bitach.  Najlepsze praktyki stanów czy hello minimalną siłę klucza dopuszczalne klucze o długości 2048 bitów.  Klucze mniej niż 2048 bitów teoretycznie może być uszkodzony.  Ustawienie hello `ServerKeyBits` zbyt`2048` umożliwia połączeń przy użyciu kluczy 2048 bitów lub większej i odmowy połączeń mniej niż 2048 bitów.

```bash
ServerKeyBits 2048
```

## <a name="disconnect-idle-users"></a>Odłącz bezczynnych użytkowników

SSH ma hello możliwości toodisconnect użytkowników, którzy mają otwarte połączenia, które po okresie bezczynności przez ponad Ustaw okres czasu w sekundach.  Utrzymywanie otwartych sesji tooonly tych użytkowników, którzy są limity active narażenia hello hello maszyny Wirtualnej systemu Linux.

```bash
ClientAliveInterval 300
ClientAliveCountMax 0
```

## <a name="restart-sshd"></a>Uruchom ponownie SSHD

Ustawienia hello tooenable w `/etc/ssh/sshd_config` ponownie uruchomić proces SSHD hello, co spowoduje ponowne uruchomienie hello serwer SSH.  Okno terminalu Hello w przypadku używania serwera SSH hello toorestart pozostają otwarte, bez utraty hello otwartych sesji SSH.  tootest hello nowych ustawień serwera SSH za pomocą drugiego okno terminalu lub kartę.  Użycie hello oddzielnych tootest terminali połączenia SSH umożliwia toogo Wstecz i Utwórz dodatkowe zmiany toohello `/etc/ssh/sshd_config` w pierwszym terminal hello bez jest zablokowane przez istotne zmiany SSHD.  

### <a name="on-redhat-centos-and-fedora"></a>Redhat, Centos i Fedora

```bash
service sshd restart
```

### <a name="on-debian--ubuntu"></a>Na Debian i Ubuntu

```bash
service ssh restart
```

## <a name="reset-sshd-using-azure-reset-access"></a>Resetuj SSHD przy użyciu resetowania Azure — dostęp

Jeśli użytkownik jest zablokowany z najważniejszych zmian toohello SSHD konfiguracji można użyć hello rozszerzenia dostępu do maszyny Wirtualnej Azure tooreset hello SSHD konfiguracji wstecz toohello oryginalnej konfiguracji.

Wszystkie nazwy przykład zastąpić własnymi.

```azurecli
azure vm reset-access \
--resource-group myResourceGroup \
--name myVM \
--reset-ssh
```

## <a name="install-fail2ban"></a>Zainstaluj Fail2ban

Zalecane jest tooinstall i Instalator hello typu open source aplikacja Fail2ban, które bloki powtarzane próby toologin tooyour maszyny Wirtualnej systemu Linux za pomocą protokołu SSH za pomocą siłowych.  Dzienniki Fail2ban powtarzany nie powiodło się toologin prób za pomocą protokołu SSH, a następnie tworzy reguły zapory adres IP hello tooblock prób hello pochodzą z.

* [Strona główna Fail2ban](http://www.fail2ban.org/wiki/index.php/Main_Page)

## <a name="next-steps"></a>Następne kroki

Po skonfigurowaniu i zablokowane hello SSH serwera na maszynie Wirtualnej systemu Linux czy dodatkowe zabezpieczenia najlepsze rozwiązania, możesz skorzystać z.  

* [Zarządzanie użytkownikami, SSH i wyboru lub naprawy dysków na maszynach wirtualnych systemu Linux platformy Azure przy użyciu hello rozszerzenia VMAccess](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

* [Szyfrowanie dysków na Maszynę wirtualną systemu Linux przy użyciu hello wiersza polecenia platformy Azure](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

* [Dostęp i większe bezpieczeństwo w szablonach usługi Azure Resource Manager](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
