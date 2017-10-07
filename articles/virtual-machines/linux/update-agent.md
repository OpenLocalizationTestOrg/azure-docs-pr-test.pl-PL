---
title: "Witaj aaaUpdate agenta systemu Linux platformy Azure z usługi GitHub | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooupdate agenta systemu Linux platformy Azure dla maszyny Wirtualnej systemu Linux w najnowszej wersji Azure toohello z usługi GitHub"
services: virtual-machines-linux
documentationcenter: 
author: SuperScottz
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: f1f19300-987d-4f29-9393-9aba866f049c
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: mingzhan
ms.openlocfilehash: 4ce7c56efc1e6563e6415f7687573f9fb9e7b4c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooupdate-hello-azure-linux-agent-on-a-vm"></a>Jak tooupdate hello Azure agenta systemu Linux na maszynie Wirtualnej

tooupdate Twojego [agenta systemu Linux Azure](https://github.com/Azure/WALinuxAgent) na Maszynę wirtualną systemu Linux na platformie Azure, należy wcześniej:

- Uruchomionej maszyny Wirtualnej systemu Linux na platformie Azure.
- Toothat połączenia maszyny Wirtualnej systemu Linux przy użyciu protokołu SSH.

Należy zawsze sprawdzić, czy pakiet w repozytorium distro Linux hello najpierw. Możliwe jest dostępny pakiet hello nie może być hello najnowszej wersji, jednak włączenie autoupdate zapewnia hello agenta systemu Linux będzie zawsze uzyskać hello najnowszej aktualizacji. Czy ma problemy z instalacją hello menedżerów pakietu, należy zwrócić wsparciu hello distro dostawcy.

## <a name="updating-hello-azure-linux-agent"></a>Aktualizowanie hello Azure agenta systemu Linux

## <a name="ubuntu"></a>Ubuntu

#### <a name="check-your-current-package-version"></a>Sprawdź bieżącą wersję pakietu

```bash
apt list --installed | grep walinuxagent
```

#### <a name="update-package-cache"></a>Pamięć podręczną pakietów aktualizacji

```bash
sudo apt-get -qq update
```

#### <a name="install-hello-latest-package-version"></a>Zainstaluj najnowszą wersję pakietu hello

```bash
sudo apt-get install walinuxagent
```

#### <a name="ensure-auto-update-is-enabled"></a>Upewnij się, że jest włączone automatyczne aktualizacje

Najpierw należy sprawdzić toosee, jeśli jest włączona:

```bash
cat /etc/waagent.conf
```

Znajdź "AutoUpdate.Enabled". Jeśli to pole wyboru jest wyświetlane, jest włączona:

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

tooenable Uruchom:

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a>Uruchom ponownie usługę agenta waagent hello

#### <a name="restart-agent-for-1404"></a>Uruchom ponownie agenta dla 14.04

```bash
initctl restart walinuxagent
```

#### <a name="restart-agent-for-1604--1704"></a>Uruchom ponownie agenta dla 16.04 / 17.04

```bash
systemctl restart walinuxagent.service
```

## <a name="debian"></a>Debian

### <a name="debian-7-wheezy"></a>Debian 7 "Wheezy"

#### <a name="check-your-current-package-version"></a>Sprawdź bieżącą wersję pakietu

```bash
dpkg -l | grep waagent
```

#### <a name="update-package-cache"></a>Pamięć podręczną pakietów aktualizacji

```bash
sudo apt-get -qq update
```

#### <a name="install-hello-latest-package-version"></a>Zainstaluj najnowszą wersję pakietu hello

```bash
sudo apt-get install waagent
```

#### <a name="enable-agent-auto-update"></a>Włącz Aktualizacje automatyczne agenta
Ta wersja Debian nie ma wersji > = 2.0.16, dlatego aktualizacje automatyczne jest niedostępna dla niego. dane wyjściowe Hello hello powyżej polecenie wyświetli, jeśli pakietów hello jest aktualny.

### <a name="debian-8-jessie--debian-9-stretch"></a>Debian 8 "Joasia" / Debian 9 "Stretch"

#### <a name="check-your-current-package-version"></a>Sprawdź bieżącą wersję pakietu

```bash
apt list --installed | grep walinuxagent
```

#### <a name="update-package-cache"></a>Pamięć podręczną pakietów aktualizacji

```bash
sudo apt-get -qq update
```

#### <a name="install-hello-latest-package-version"></a>Zainstaluj najnowszą wersję pakietu hello

```bash
sudo apt-get install waagent
```
#### <a name="ensure-auto-update-is-enabled"></a>Upewnij się, że jest włączone automatyczne aktualizacje 

Najpierw należy sprawdzić toosee, jeśli jest włączona:

```bash
cat /etc/waagent.conf
```

Znajdź "AutoUpdate.Enabled". Jeśli to pole wyboru jest wyświetlane, jest włączona:

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

tooenable Uruchom:

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a>Uruchom ponownie usługę agenta waagent hello

```
sudo systemctl restart walinuxagent.service
```

## <a name="redhat--centos"></a>RedHat / CentOS

### <a name="rhelcentos-6"></a>RHEL/CentOS 6

#### <a name="check-your-current-package-version"></a>Sprawdź bieżącą wersję pakietu

```bash
sudo yum list WALinuxAgent
```

#### <a name="check-available-updates"></a>Sprawdzanie dostępności aktualizacji

```bash
sudo yum check-update WALinuxAgent
```

#### <a name="install-hello-latest-package-version"></a>Zainstaluj najnowszą wersję pakietu hello

```bash
sudo yum install WALinuxAgent
```

#### <a name="ensure-auto-update-is-enabled"></a>Upewnij się, że jest włączone automatyczne aktualizacje 

Najpierw należy sprawdzić toosee, jeśli jest włączona:

```bash
cat /etc/waagent.conf
```

Znajdź "AutoUpdate.Enabled". Jeśli to pole wyboru jest wyświetlane, jest włączona:

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

tooenable Uruchom:

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a>Uruchom ponownie usługę agenta waagent hello

```
sudo service waagent restart
```

### <a name="rhelcentos-7"></a>RHEL/CentOS 7

#### <a name="check-your-current-package-version"></a>Sprawdź bieżącą wersję pakietu

```bash
sudo yum list WALinuxAgent
```

#### <a name="check-available-updates"></a>Sprawdzanie dostępności aktualizacji

```bash
sudo yum check-update WALinuxAgent
```

#### <a name="install-hello-latest-package-version"></a>Zainstaluj najnowszą wersję pakietu hello

```bash
sudo yum install WALinuxAgent  
```

#### <a name="ensure-auto-update-is-enabled"></a>Upewnij się, że jest włączone automatyczne aktualizacje 

Najpierw należy sprawdzić toosee, jeśli jest włączona:

```bash
cat /etc/waagent.conf
```

Znajdź "AutoUpdate.Enabled". Jeśli to pole wyboru jest wyświetlane, jest włączona:

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

tooenable Uruchom:

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a>Uruchom ponownie usługę agenta waagent hello

```bash
sudo systemctl restart waagent.service
```

## <a name="suse-sles"></a>SUSE SLES

### <a name="suse-sles-11-sp4"></a>SUSE SLES 11 Z DODATKIEM SP4

#### <a name="check-your-current-package-version"></a>Sprawdź bieżącą wersję pakietu

```bash
zypper info python-azure-agent
```

#### <a name="check-available-updates"></a>Sprawdzanie dostępności aktualizacji

Hello powyżej dane wyjściowe wyświetli, jeśli pakiet hello działa toodate.

#### <a name="install-hello-latest-package-version"></a>Zainstaluj najnowszą wersję pakietu hello

```bash
sudo zypper install python-azure-agent
```

#### <a name="ensure-auto-update-is-enabled"></a>Upewnij się, że jest włączone automatyczne aktualizacje 

Najpierw należy sprawdzić toosee, jeśli jest włączona:

```bash
cat /etc/waagent.conf
```

Znajdź "AutoUpdate.Enabled". Jeśli to pole wyboru jest wyświetlane, jest włączona:

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

tooenable Uruchom:

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a>Uruchom ponownie usługę agenta waagent hello

```bash
sudo /etc/init.d/waagent restart
```

### <a name="suse-sles-12-sp2"></a>SUSE SLES 12 Z DODATKIEM SP2

#### <a name="check-your-current-package-version"></a>Sprawdź bieżącą wersję pakietu

```bash
zypper info python-azure-agent
```

#### <a name="check-available-updates"></a>Sprawdzanie dostępności aktualizacji

W danych wyjściowych hello z hello powyżej spowoduje to wyświetlenie Jeśli pakietów hello jest maksymalnie daty.

#### <a name="install-hello-latest-package-version"></a>Zainstaluj najnowszą wersję pakietu hello

```bash
sudo zypper install python-azure-agent
```

#### <a name="ensure-auto-update-is-enabled"></a>Upewnij się, że jest włączone automatyczne aktualizacje 

Najpierw należy sprawdzić toosee, jeśli jest włączona:

```bash
cat /etc/waagent.conf
```

Znajdź "AutoUpdate.Enabled". Jeśli to pole wyboru jest wyświetlane, jest włączona:

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

tooenable Uruchom:

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a>Uruchom ponownie usługę agenta waagent hello

```bash
sudo systemctl restart waagent.service
```

## <a name="oracle-6-and-7"></a>Oracle 6 i 7

Oracle Linux, upewnij się, że hello `Addons` repozytorium jest włączona. Wybierz plik hello tooedit `/etc/yum.repos.d/public-yum-ol6.repo`(Oracle Linux 6) lub `/etc/yum.repos.d/public-yum-ol7.repo`(Oracle Linux) i zmień wiersz hello `enabled=0` za`enabled=1` w obszarze **[ol6_addons]** lub **[ol7_addons]** w tym pliku.

Następnie tooinstall hello najnowszą wersję hello Azure agenta systemu Linux, wpisz:

```bash
sudo yum install WALinuxAgent
```

Jeśli nie znajdziesz hello dodatek repozytorium można po prostu dodać te wiersze na końcu pliku .repo zgodnie z wersji Oracle Linux tooyour hello:

W przypadku maszyn wirtualnych Oracle Linux 6:

```sh
[ol6_addons]
name=Add-Ons for Oracle Linux $releasever ($basearch)
baseurl=http://public-yum.oracle.com/repo/OracleLinux/OL6/addons/x86_64
gpgkey=http://public-yum.oracle.com/RPM-GPG-KEY-oracle-ol6
gpgcheck=1
enabled=1
```

Oracle Linux 7 maszyn wirtualnych:

```sh
[ol7_addons]
name=Oracle Linux $releasever Add ons ($basearch)
baseurl=http://public-yum.oracle.com/repo/OracleLinux/OL7/addons/$basearch/
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-oracle
gpgcheck=1
enabled=0
```

Następnie wpisz:

```bash
sudo yum update WALinuxAgent
```

Zazwyczaj jest wymagany, ale z jakiegoś powodu potrzebne tooinstall z https://github.com bezpośrednio, użyj hello następujące kroki.


## <a name="update-hello-linux-agent-when-no-agent-package-exists-for-distribution"></a>Zaktualizuj hello agenta systemu Linux, gdy pakiet agenta, nie istnieje dla dystrybucji

Zainstaluj wget (istnieją pewne dystrybucjach, który nie należy instalować go domyślnie, takie jak wersje Redhat, CentOS i Oracle Linux 6.4 i 6.5) przez wpisanie `sudo yum install wget` hello w wierszu polecenia.

### <a name="1-download-hello-latest-version"></a>1. Pobieranie najnowszej wersji hello
Otwórz [hello wersji agenta systemu Linux platformy Azure w serwisie GitHub](https://github.com/Azure/WALinuxAgent/releases) strony sieci web, i sprawdź numer hello najnowszej wersji. (Można znaleźć wersji bieżącej, wpisując `waagent --version`.)

#### <a name="for-version-22x-or-later-type"></a>Dla wersji 2.2.x lub później, wpisz:
```bash
wget https://github.com/Azure/WALinuxAgent/archive/v2.2.x.zip
unzip v2.2.x.zip.zip
cd WALinuxAgent-2.2.x
```

Witaj następujący wiersz jest używana wersja 2.2.0 na przykład:

```bash
wget https://github.com/Azure/WALinuxAgent/archive/v2.2.14.zip
unzip v2.2.14.zip  
cd WALinuxAgent-2.2.14
```

### <a name="2-install-hello-azure-linux-agent"></a>2. Zainstaluj hello Azure agenta systemu Linux

#### <a name="for-version-22x-use"></a>Dla wersji 2.2.x, użyj:
Może być konieczne pakietu hello tooinstall `setuptools` najpierw — zobacz [tutaj](https://pypi.python.org/pypi/setuptools). Następnie uruchom polecenie:

```bash
sudo python setup.py install
```

#### <a name="ensure-auto-update-is-enabled"></a>Upewnij się, że jest włączone automatyczne aktualizacje

Najpierw należy sprawdzić toosee, jeśli jest włączona:

```bash
cat /etc/waagent.conf
```

Znajdź "AutoUpdate.Enabled". Jeśli to pole wyboru jest wyświetlane, jest włączona:

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

tooenable Uruchom:

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="3-restart-hello-waagent-service"></a>3. Uruchom ponownie usługę agenta waagent hello
Dla większości dystrybucjach systemu Linux:

```bash
sudo service waagent restart
```

Ubuntu użyć:

```bash
sudo service walinuxagent restart
```

Dla CoreOS użyj polecenia:

```bash
sudo systemctl restart waagent
```

### <a name="4-confirm-hello-azure-linux-agent-version"></a>4. Potwierdzenie hello wersji agenta systemu Linux platformy Azure
    
```bash
waagent -version
```

Dla CoreOS hello powyżej polecenie może nie działać.

Pojawi się, że tego hello agenta systemu Linux Azure wersji został zaktualizowany toohello nowej wersji.

Aby uzyskać więcej informacji dotyczących hello agenta systemu Linux platformy Azure, zobacz [README agenta systemu Linux Azure](https://github.com/Azure/WALinuxAgent).
