---
title: tooLinux aaaIntroduction na platformie Azure | Dokumentacja firmy Microsoft
description: "Informacje o używaniu maszyn wirtualnych systemu Linux na platformie Azure."
services: virtual-machines-linux
documentationcenter: python
author: szarkos
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: b13bf305-87bf-4df3-815e-e8f6337aa6ea
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: szark
ms.openlocfilehash: 3a931447ee23ce7000174ca314c3e10abc6b8e74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toolinux-on-azure"></a>Wprowadzenie tooLinux na platformie Azure
W tym temacie omówiono niektóre aspekty w hello chmury Azure przy użyciu maszyn wirtualnych systemu Linux. Wdrażanie maszyny wirtualnej systemu Linux jest dość proste z galerii hello przy użyciu obrazu.

## <a name="authentication-usernames-passwords-and-ssh-keys"></a>Uwierzytelniania: Nazwy użytkowników, hasła i klucze SSH
Podczas tworzenia maszyny wirtualnej systemu Linux przy użyciu hello portalu Azure, zostanie wyświetlona prośba tooprovide albo nazwa użytkownika i hasło lub klucz publiczny SSH. Witaj wybór nazwy użytkownika podczas wdrażania maszyny wirtualnej systemu Linux na platformie Azure jest toohello podmiotu następujące ograniczenia: nazwy kont systemowych (UID < 100) znajduje się już w hello maszyny wirtualnej nie są dozwolone, "root" na przykład.

* Zobacz [Utwórz maszynę wirtualną z systemem Linux](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* Zobacz [jak tooUse SSH z systemem Linux na platformie Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="obtaining-superuser-privileges-using-sudo"></a>Uzyskiwanie przy użyciu uprawnień administratora`sudo`
Witaj konta użytkownika, które określono podczas wdrażania wystąpienia maszyny wirtualnej na platformie Azure jest uprzywilejowanego konta. To konto jest konfigurowana przy użyciu hello hello agenta systemu Linux platformy Azure toobe stanie tooelevate uprawnienia tooroot (konto administratora) `sudo` narzędzia. Po zalogowaniu się przy użyciu tego konta użytkownika, będą mogli toorun poleceń jako główny przy użyciu składni polecenia hello:

    # sudo <COMMAND>

Opcjonalnie można uzyskać powłoki głównego przy użyciu **sudo -s**.

* Zobacz [przy użyciu uprawnień głównego na maszynach wirtualnych systemu Linux na platformie Azure](use-root-privileges.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="firewall-configuration"></a>Konfiguracja zapory
Platforma Azure udostępnia pakietów przychodzących filtr, który ogranicza tooports łączności określone w hello portalu Azure. Domyślnie program hello tylko dozwolonych port jest SSH. Może otwarcia portów tooadditional dostępu na maszynie wirtualnej systemu Linux przez skonfigurowanie punktów końcowych w hello portalu Azure:

* Zobacz: [jak tooSet się punkty końcowe tooa maszyny wirtualnej](../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

Hello Linux obrazów w galerii Azure hello nie należy włączać hello *iptables* zapory domyślnie. W razie potrzeby można skonfigurować zapory hello tooprovide dodatkowe filtrowania.

## <a name="hostname-changes"></a>Zmiany nazwy hosta
Po początkowym wdrożeniu wystąpienia obrazu systemu Linux, jest wymagana tooprovide nazwę hosta dla maszyny wirtualnej hello. Po uruchomieniu maszyny wirtualnej hello, ta nazwa hosta jest serwerów DNS platformy opublikowanych toohello tak, aby wiele tooeach maszyny wirtualne podłączone, inne mogą wykonywać wyszukiwania adres IP przy użyciu nazwy hostów.

Jeśli nazwa hosta zmiany są potrzebne, po wdrożeniu maszyny wirtualnej, użyj polecenia hello

    # sudo hostname <newname>

Hello Azure agenta systemu Linux zawiera funkcje tooautomatically wykrycia tej zmiany nazwy i odpowiednio Konfiguracja toopersist maszyny wirtualnej hello tę zmianę i publikowanie serwerów DNS tej zmiany toohello platformy.

* [Podręcznik użytkownika Azure agenta systemu Linux](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="cloud-init"></a>Init chmury
**Ubuntu** i **CoreOS** obrazów korzystanie z inicjowaniem chmurze na platformie Azure, która zapewnia dodatkowe funkcje do inicjalizacji maszyny wirtualnej.

* [Jak tooInject danych niestandardowych](../windows/classic/inject-custom-data.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [Niestandardowe dane i inicjowania chmurze na platformie Microsoft Azure](https://azure.microsoft.com/blog/2014/04/21/custom-data-and-cloud-init-on-windows-azure/)
* [Tworzenie partycji wymiany Azure przy użyciu inicjowania chmury](https://wiki.ubuntu.com/AzureSwapPartitions)
* [Jak tooUse CoreOS na platformie Azure](https://coreos.com/os/docs/latest/booting-on-azure.html)

## <a name="virtual-machine-image-capture"></a>Przechwyć obraz maszyny wirtualnej
Platforma Azure udostępnia hello możliwości toocapture hello stan istniejącej maszyny wirtualnej do obrazu, który może być następnie używane toodeploy wystąpień dodatkowych maszyn wirtualnych. Hello agenta systemu Linux platformy Azure mogą być używane toorollback niektóre hello dostosowania, które zostało wykonane podczas procesu udostępniania hello. Jako obrazu, może wykonaj kroki hello poniżej toocapture maszyny wirtualnej:

1. Uruchom **agenta waagent-deprovision** tooundo inicjowania obsługi administracyjnej dostosowania. Lub **agenta waagent-deprovision + użytkownika** toooptionally usunąć konto użytkownika hello określone podczas inicjowania obsługi i wszystkie skojarzone dane.
2. Zamknij dół/wyłączyć hello maszyny wirtualnej.
3. Kliknij przycisk **przechwytywania** w hello Azure hello portalu lub użyj programu PowerShell lub interfejsu wiersza polecenia narzędzia maszyny wirtualnej hello toocapture jako obraz.
   
   * Zobacz: [jak tooCapture tooUse maszyny wirtualnej systemu Linux jako szablon](classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

## <a name="attaching-disks"></a>Dołączanie dysków
Każda maszyna wirtualna ma tymczasowej lokalnego *zasobu dysku* dołączony. Ponieważ dane na dysku zasobu nie może być trwałe między ponownymi uruchomieniami komputera jest często używany przez aplikacje i procesów uruchomionych na maszynie wirtualnej powitania dla przejściowy i **tymczasowego** magazynu danych. Możliwe jest również używane toostore pliki strony lub wymiany hello systemu operacyjnego hello.

W systemie Linux hello zasobu dysk jest zwykle zarządzane przez agenta systemu Linux Azure hello i automatycznie instalowane za**/mnt/zasobu** (lub **katalogu/mnt** na obrazach Ubuntu).

> [!NOTE]
> Ten dysk zasobów hello jest **tymczasowego** na dysku i może być usunięty i ponownie sformatowany podczas hello wirtualna rozruchu komputera.
> 
> 

W systemie Linux hello dysku danych może mieć nazwę przez jądro hello jako `/dev/sdc`, a użytkownicy muszą toopartition, formatowanie i zainstaluj tego zasobu. Ten temat znajdują się instrukcje w samouczku hello: [jak tooAttach tooa dysku danych maszyny wirtualnej](../windows/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

* **Zobacz też:** [należy skonfigurować oprogramowanie RAID w systemie Linux](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) & [skonfigurować LVM na Maszynę wirtualną systemu Linux na platformie Azure](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

