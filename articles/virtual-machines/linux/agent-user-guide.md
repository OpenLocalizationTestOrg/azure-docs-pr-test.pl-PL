---
title: "aaaAzure omówienie agenta maszyny Wirtualnej systemu Linux | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooinstall i konfigurowanie maszyny wirtualnej interakcji z kontrolerem sieci szkieletowej Azure toomanage agenta systemu Linux (agenta waagent)."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: e41de979-6d56-40b0-8916-895bf215ded6
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 10/17/2016
ms.author: szark
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 4e08c84d9205f4db7aae6fd1568ec1f15fba395c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-and-using-hello-azure-linux-agent"></a>Opis i przy użyciu hello Azure agenta systemu Linux
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="introduction"></a>Wprowadzenie
Witaj Linux Agent usługi Microsoft Azure (agenta waagent) zarządza systemu Linux i FreeBSD inicjowania obsługi administracyjnej i maszyny Wirtualnej interakcji z hello Azure kontrolera sieci szkieletowej. Udostępnia ona następujące funkcje dla wdrożenia systemu Linux i FreeBSD IaaS hello:

> [!NOTE]
> Zobacz agenta systemu Linux Azure hello [README](https://github.com/Azure/WALinuxAgent/blob/master/README.md) dodatkowe szczegóły.
> 
> 

* **Inicjowanie obsługi obrazu**
  
  * Tworzenie konta użytkownika
  * Konfigurowanie typów uwierzytelniania SSH
  * Wdrożenie par kluczy i kluczy publicznych SSH
  * Nazwa hosta hello ustawienia
  * Platforma toohello nazwy hosta hello publikowania DNS
  * Platforma toohello klucza odcisk palca hosta raportowania SSH
  * Zarządzanie zasobami dysku
  * Formatowanie i instalowania hello zasobu dysku
  * Konfigurowanie obszaru wymiany
* **Sieć**
  
  * Zarządza tras tooimprove zgodność z serwerami DHCP platformy
  * Zapewnia stabilność hello Nazwa interfejsu sieciowego hello
* **Jądra**
  
  * Konfiguruje wirtualną architekturę NUMA (Wyłącz dla jądra < 2.6.37)
  * Wykorzystuje entropii funkcji Hyper-V dla /dev/random
  * Konfiguruje SCSI przekroczeń limitu czasu dla urządzenia głównego hello, (który może być zdalne)
* **Diagnostyka**
  
  * Port szeregowy toohello przekierowania konsoli
* **Wdrożenia programu SCVMM**
  
  * Wykrywa i używa do ładowania agenta VMM hello Linux podczas uruchamiania w środowisku programu System Center Virtual Machine Manager 2012 R2
* **Rozszerzenia maszyny Wirtualnej**
  
  * Wstaw składnik utworzone przez firmę Microsoft i partnerów do automatyzacji oprogramowania i konfiguracji tooenable maszyny Wirtualnej systemu Linux (IaaS)
  * Implementacja odwołanie rozszerzenia maszyny Wirtualnej na [https://github.com/Azure/azure-linux-extensions](https://github.com/Azure/azure-linux-extensions)

## <a name="communication"></a>Komunikacja
przepływ informacji Hello hello platformy toohello agenta odbywa się za pośrednictwem dwóch kanałów:

* Czas rozruchu dołączonych dysków DVD do wdrożenia IaaS. Ten dysk DVD zawiera zgodne OVF pliku konfiguracji, który zawiera wszystkie informacje o udostępnianiu niż rzeczywista keypairs SSH hello.
* Punkt końcowy protokołu TCP udostępnianie interfejsu API REST używany tooobtain wdrażanie i Konfigurowanie topologii.

## <a name="requirements"></a>Wymagania
Witaj następujących systemów zostały przetestowane i są znane toowork z hello Azure agenta systemu Linux:

> [!NOTE]
> Ta lista może się różnić od hello oficjalnego listę obsługiwanych systemów na powitania platformie Microsoft Azure, zgodnie z opisem w tym miejscu: [http://support.microsoft.com/kb/2805216](http://support.microsoft.com/kb/2805216)
> 
> 

* CoreOS
* CentOS 6.3 +
* Red Hat Enterprise Linux 6.7 +
* Debian 7.0 +
* Ubuntu 12.04 +
* openSUSE 12.3 +
* SLES 11 Z DODATKIEM SP3 +
* Oracle Linux 6.4 +

Inne obsługiwane systemy:

* FreeBSD 10 + (Azure agenta systemu Linux v2.0.10 +)

agenta systemu Linux Hello jest zależna od niektórych pakietów systemu w kolejności toofunction prawidłowo:

* Python 2.6 +
* Biblioteki OpenSSL 1.0 +
* OpenSSH 5.3 +
* Narzędzia systemu plików: ulec sfdisk fdisk, mkfs,
* Narzędzia hasło: chpasswd, sudo
* Narzędzia do edycji tekstu: mniejszyć, grep
* Narzędzia sieci: trasy ip
* Obsługuje jądra służący do instalowania funkcji zdefiniowanej przez użytkownika, systemy plików.

## <a name="installation"></a>Instalacja
Instalacja przy użyciu obr. / min lub pakietu DEB z repozytorium pakietów programu dystrybucji jest hello preferowana metoda Instalowanie i uaktualnianie hello Azure agenta systemu Linux. Wszystkie hello [zatwierdzone dostawców dystrybucji](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) zintegrować pakiet agenta platformy Azure Linux hello repozytoriami i obrazów.

Zapoznaj się z dokumentacją toohello w hello [repozytorium agenta systemu Linux platformy Azure w serwisie GitHub](https://github.com/Azure/WALinuxAgent) dla zaawansowane opcje instalacji, takich jak instalowanie z lokalizacji źródłowej lub toocustom lub prefiksów.

## <a name="command-line-options"></a>Opcje wiersza polecenia
### <a name="flags"></a>Flagi
* verbose: Zwiększ poziom szczegółowości określonego polecenia
* Wymuś: Pomiń interakcyjne potwierdzenie dla niektórych poleceń

### <a name="commands"></a>Polecenia
* Pomoc: Wyświetla listę poleceń hello obsługiwane i flagi.
* deprovision: próba tooclean hello systemu i zapewnić ich nadające się do ponownego inicjowania obsługi administracyjnej. Ta operacja usunięte hello następujące czynności:
  
  * Wszystkie klucze hosta SSH (jeśli Provisioning.RegenerateSshHostKeyPair "y" w pliku konfiguracyjnym hello)
  * Konfiguracja serwera nazw w /etc/resolv.conf
  * Hasła głównego z /etc/shadow (jeśli Provisioning.DeleteRootPassword "y" w pliku konfiguracyjnym hello)
  * Buforowane dzierżawy klientów DHCP
  * Resetuje hosta toolocalhost.localdomain nazwy

> [!WARNING]
> Cofanie zastrzegania nie gwarantuje, że ten obraz powitania jest wyczyszczone wszystkie informacje poufne i odpowiedni w przypadku ponownej dystrybucji.
> 
> 

* deprovision + użytkownika: wykonuje wszystkie elementy w obszarze - deprovision (powyżej) i również usuwa hello ostatnie konto użytkownika elastycznie (uzyskane z /var/lib/waagent) i skojarzone dane. Ten parametr jest podczas usuwania inicjowania obsługi administracyjnej z obrazem, który został wcześniej inicjowania obsługi administracyjnej na platformie Azure, mogą być przechwytywane i ponownego użycia.
* Wersja: Wyświetla hello wersji agenta waagent
* serialconsole: konfiguruje ttyS0 toomark CHODNIKÓW (hello pierwszego portu szeregowego) jako hello rozruchowe konsoli. Dzięki temu jądra rozruchu dzienniki są wysyłane do portu szeregowego toothe, a udostępnione do debugowania.
* demon: uruchomiono agenta waagent jako demon toomanage interakcji z platformą hello. Ten argument jest toowaagent określonego w skrypcie inicjowania agenta waagent hello.
* Rozpocznij: uruchomiono agenta waagent jako proces w tle

## <a name="configuration"></a>Konfiguracja
Plik konfiguracji (/ etc/waagent.conf) kontrolki hello agenta waagent akcje. Poniżej przedstawiono przykładowy plik konfiguracji:

    Provisioning.Enabled=y
    Provisioning.DeleteRootPassword=n
    Provisioning.RegenerateSshHostKeyPair=y
    Provisioning.SshHostKeyPairType=rsa
    Provisioning.MonitorHostName=y
    Provisioning.DecodeCustomData=n
    Provisioning.ExecuteCustomData=n
    Provisioning.PasswordCryptId=6
    Provisioning.PasswordCryptSaltLength=10
    ResourceDisk.Format=y
    ResourceDisk.Filesystem=ext4
    ResourceDisk.MountPoint=/mnt/resource
    ResourceDisk.MountOptions=None
    ResourceDisk.EnableSwap=n
    ResourceDisk.SwapSizeMB=0
    LBProbeResponder=y
    Logs.Verbose=n
    OS.RootDeviceScsiTimeout=300
    OS.OpensslPath=None
    HttpProxy.Host=None
    HttpProxy.Port=None

powitalne różne opcje konfiguracji są szczegółowo opisana poniżej. Opcje konfiguracji są trzy typy; Wartość logiczna, String lub Integer. Opcje konfiguracji logiczna Hello można określić jako "y" lub "n". Witaj specjalne — słowo kluczowe "None" mogą być używane w przypadku niektórych ciąg typu konfiguracji wpisów zgodnie z opisem poniżej.

**Provisioning.Enabled:**  
Typ: wartość logiczna  
Domyślne: y

To umożliwia tooenable użytkownika hello lub wyłącz hello inicjowania obsługi funkcji hello agenta. Prawidłowe wartości to "y" lub "n". Jeśli Inicjowanie obsługi administracyjnej jest wyłączone, hosta i użytkownika kluczy SSH w obrazie hello są zachowywane i określona w hello Azure API inicjowania obsługi administracyjnej konfiguracja jest ignorowana.

> [!NOTE]
> Witaj `Provisioning.Enabled` zbyt "n" na Ubuntu chmury obrazów użyj init chmury w celu obsługi domyślne wartości parametrów.
> 
> 

**Provisioning.DeleteRootPassword:**  
Typ: wartość logiczna  
Domyślne: n

Jeśli zestaw, hello hasła użytkownika root w hello/etc/pliku w tle zostanie wymazane podczas hello procesu inicjowania obsługi administracyjnej.

**Provisioning.RegenerateSshHostKeyPair:**  
Typ: wartość logiczna  
Domyślne: y

Jeśli zestawu i wszystkich hostów par kluczy SSH (ecdsa, dsa i rsa) zostaną usunięte podczas procesu z/etc/ssh/udostępniania hello. I generowany jest jeden świeże pary kluczy.

Typ szyfrowania Hello hello świeże pary kluczy jest konfigurowane przez hello Provisioning.SshHostKeyPairType wpisu. Należy pamiętać, że niektórych dystrybucji zostaną ponownie utworzone par kluczy SSH dla wszystkich Brak typów szyfrowania, po ponownym uruchomieniu demon SSH hello (na przykład po ponownym rozruchu).

**Provisioning.SshHostKeyPairType:**  
Typ: ciąg  
Domyślne: rsa

Typ algorytmu szyfrowania tooan, który jest obsługiwany przez hello demon SSH na maszynie wirtualnej hello można go ustawić. Hello zwykle obsługiwane wartości to "rsa", "dsa" i "ecdsa". Należy pamiętać, że "putty.exe" w systemie Windows nie obsługuje "ecdsa". Tak Jeśli planujesz toouse putty.exe na tooa tooconnect Windows wdrożenia systemu Linux, użyj "rsa" lub "dsa".

**Provisioning.MonitorHostName:**  
Typ: wartość logiczna  
Domyślne: y

Jeśli ustawiona, agenta waagent monitorujący maszyny wirtualnej systemu Linux hello zmiany nazwy hosta (jak zwracany przez polecenie "Nazwa hosta" hello) i automatycznie Aktualizuj hello konfiguracji sieci w przypadku zmiany hello tooreflect obraz powitania. W nazwie hello toopush kolejności zmienić toohello serwerów DNS, sieci zostanie uruchomiona ponownie w hello maszyny wirtualnej. Spowoduje to w skrócie utratę łączności z Internetem.

**Provisioning.DecodeCustomData**  
Typ: wartość logiczna  
Domyślne: n

Jeśli zostanie ustawiona, agenta waagent dekodowania CustomData z formatu Base64.

**Provisioning.ExecuteCustomData**  
Typ: wartość logiczna  
Domyślne: n

Jeśli ustawiona, agenta waagent wykona CustomData po zainicjowaniu obsługi administracyjnej.

**Provisioning.PasswordCryptId**  
Typ: ciąg  
Domyślne: 6

Algorytm używany przez crypt podczas generowania skrótu hasła.  
 1 - MD5  
 2a - Blowfish  
 5 - ALGORYTMU SHA-256  
 6 - SHA-512  

**Provisioning.PasswordCryptSaltLength**  
Typ: ciąg  
Domyślny: 10

Długość losowe soli używana podczas generowania skrótu hasła.

**ResourceDisk.Format:**  
Typ: wartość logiczna  
Domyślne: y

Jeśli ustawiona, dysk zasobów hello dostarczony przez platformę hello jest formatowany i zainstalowanych w wyniku agenta waagent, jeśli typ filesystem hello żądany przez użytkownika hello w "ResourceDisk.Filesystem" jest inna niż "ntfs". Jednej partycji typu systemu Linux (83) są udostępniane na powitania dysku. Należy pamiętać, że ta partycja nie zostanie sformatowana Jeśli można zainstalować pomyślnie.

**ResourceDisk.Filesystem:**  
Typ: ciąg  
Domyślne: ext4

To określa typ plików hello hello zasobu dysku. Obsługiwane wartości różnią się dystrybucji systemu Linux. Jeśli ciąg hello jest X, następnie mkfs. X powinny znajdować się na powitania Linux obrazu. SLES 11 obrazów zwykle należy użyć "ext3". Obrazy FreeBSD należy użyć "ufs2" w tym miejscu.

**ResourceDisk.MountPoint:**  
Typ: ciąg  
Wartość domyślna: / mnt/zasobu 

Określa ścieżkę hello jaką hello zasobu dysk jest zainstalowany. Ten dysk zasobów hello jest *tymczasowego* na dysku i może opróżnić po anulowaną aprowizacją hello maszyny Wirtualnej.

**ResourceDisk.MountOptions**  
Typ: ciąg  
Domyślnie: Brak

Określa opcje instalacji dysku toobe przekazany polecenie -o instalacji toohello. Jest to rozdzielana przecinkami lista wartości, np. "nodev, nosuid". Zobacz mount(8), aby uzyskać szczegółowe informacje.

**ResourceDisk.EnableSwap:**  
Typ: wartość logiczna  
Domyślne: n

Jeśli ustawiona, plik wymiany (/ swapfile) jest tworzony na powitania zasobu dysku i dodać obszar wymiany toohello systemu.

**ResourceDisk.SwapSizeMB:**  
Typ: liczba całkowita  
Domyślna: 0

rozmiar Hello hello pliku wymiany w megabajtach.

**Logs.Verbose:**  
Typ: wartość logiczna  
Domyślne: n

Jeśli jest boosted zestawu, szczegółowości dziennika. Agenta Waagent dzienniki too/var/log/waagent.log i wykorzystuje hello systemu logrotate funkcji toorotate dzienniki.

**SYSTEM OPERACYJNY. EnableRDMA**  
Typ: wartość logiczna  
Domyślne: n

Jeśli ustawiona, hello agent będą podejmować tooinstall, a następnie załadować sterownik jądra RDMA, odpowiadający hello wersji oprogramowania układowego hello na powitania podstawowy sprzęt.

**SYSTEM OPERACYJNY. RootDeviceScsiTimeout:**  
Typ: liczba całkowita  
Domyślne: 300

Spowoduje to skonfigurowanie hello SCSI przekroczenia limitu czasu w sekundach na dyskach dysku i danych hello systemu operacyjnego. Jeśli nie jest ustawiona, system hello, które będą używane wartości domyślne.

**SYSTEM OPERACYJNY. OpensslPath:**  
Typ: ciąg  
Domyślnie: Brak

Może to być toospecify używane ścieżki alternatywnej dla hello toouse binarnych biblioteki openssl dla operacji kryptograficznych.

**HttpProxy.Host, HttpProxy.Port**  
Typ: ciąg  
Domyślnie: Brak

Jeśli ustawiona, hello agent użyje tego serwera proxy internet hello tooaccess serwera. 

## <a name="ubuntu-cloud-images"></a>Obrazy Ubuntu chmury
Należy pamiętać, że korzystanie z obrazów chmury Ubuntu [init chmury](https://launchpad.net/ubuntu/+source/cloud-init) tooperform wiele zadań konfiguracyjnych, które w przeciwnym razie mogłyby być zarządzane przez hello agenta systemu Linux platformy Azure.  Należy pamiętać, hello następujące różnice:

* **Provisioning.Enabled** zbyt "n" na obrazów chmury Ubuntu tooperform chmury inicjowania obsługi zadań Użyj ustawień domyślnych.
* Witaj następujące parametry konfiguracji nie mają wpływu na obrazy chmury Ubuntu, używanego init chmury toomanage hello zasobów dysku i zamiany miejsca:
  
  * **ResourceDisk.Format**
  * **ResourceDisk.Filesystem**
  * **ResourceDisk.MountPoint**
  * **ResourceDisk.EnableSwap**
  * **ResourceDisk.SwapSizeMB**
* Zobacz hello następującego punktu instalacji zasobów tooconfigure hello zasobów dysku i Zamień miejsce na obrazy chmury Ubuntu podczas inicjowania obsługi:
  
  * [Ubuntu Witryna typu Wiki: Konfigurowanie partycji wymiany](http://go.microsoft.com/fwlink/?LinkID=532955&clcid=0x409)
  * [Wstrzykiwania niestandardowe dane do maszyny wirtualnej platformy Azure](../windows/classic/inject-custom-data.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

