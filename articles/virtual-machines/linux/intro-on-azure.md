---
title: Wprowadzenie do systemu Linux na platformie Azure | Dokumentacja firmy Microsoft
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
ms.openlocfilehash: 7bd0c5549a2e1f592681760d5ef464b9570ca4ab
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-linux-on-azure"></a>Wprowadzenie do systemu Linux na platformie Azure
Ten temat zawiera omówienie niektórych aspektów przy użyciu maszyn wirtualnych systemu Linux w chmurze Azure. Wdrażanie maszyny wirtualnej systemu Linux jest dość proste przy użyciu obrazu z galerii.

## <a name="authentication-usernames-passwords-and-ssh-keys"></a>Uwierzytelniania: Nazwy użytkowników, hasła i klucze SSH
Podczas tworzenia maszyny wirtualnej systemu Linux przy użyciu portalu Azure, konieczne jest podanie albo nazwa użytkownika i hasło lub klucz publiczny SSH. Wybór nazwy użytkownika podczas wdrażania maszyny wirtualnej systemu Linux na platformie Azure podlega następujące ograniczenia: nazwy kont systemowych (UID < 100) już istnieje na maszynie wirtualnej nie są dozwolone, "root" na przykład.

* Zobacz [Utwórz maszynę wirtualną z systemem Linux](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* Zobacz [sposobu korzystania z protokołu SSH z systemem Linux na platformie Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="obtaining-superuser-privileges-using-sudo"></a>Uzyskiwanie przy użyciu uprawnień administratora`sudo`
Konto użytkownika, które określono podczas wdrażania wystąpienia maszyny wirtualnej na platformie Azure jest uprzywilejowanego konta. To konto jest skonfigurowane przez agenta systemu Linux Azure, aby można było podniesienia uprawnień przy użyciu głównego (konto administratora) `sudo` narzędzia. Po zalogowaniu się przy użyciu tego konta użytkownika, można uruchomić poleceń jako główny przy użyciu składni polecenia:

    # sudo <COMMAND>

Opcjonalnie można uzyskać powłoki głównego przy użyciu **sudo -s**.

* Zobacz [przy użyciu uprawnień głównego na maszynach wirtualnych systemu Linux na platformie Azure](use-root-privileges.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="firewall-configuration"></a>Konfiguracja zapory
Platforma Azure udostępnia pakietów przychodzących filtr, który ogranicza możliwość użycia połączenia do porty określone w portalu Azure. Domyślnie tylko port dozwolonych jest SSH. Możesz otworzyć dostępu do dodatkowych portów na maszynie wirtualnej systemu Linux przez skonfigurowanie punktów końcowych w portalu Azure:

* Zobacz: [sposobu konfigurowania punktów końcowych do maszyny wirtualnej](../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

Nie należy włączać Linux obrazów w galerii Azure *iptables* zapory domyślnie. W razie potrzeby można skonfigurować zapory zapewnienie dodatkowych filtrowania.

## <a name="hostname-changes"></a>Zmiany nazwy hosta
Po początkowym wdrożeniu wystąpienia obrazu systemu Linux, należy podać nazwę hosta dla maszyny wirtualnej. Po uruchomieniu maszyny wirtualnej, dzięki czemu wiele maszyn wirtualnych, połączone ze sobą przeprowadzać wyszukiwania adres IP przy użyciu nazwy hostów ta nazwa hosta jest publikowany na serwerach DNS platformy.

Jeśli nazwa hosta zmiany są potrzebne, po wdrożeniu maszyny wirtualnej, użyj polecenia

    # sudo hostname <newname>

Agent systemu Linux Azure udostępnia funkcję automatycznie wykrywa tę zmianę nazwy i odpowiednio skonfigurować maszynę wirtualną, aby zachować tę zmianę i publikowania tej zmiany na serwerach DNS platformy.

* [Podręcznik użytkownika Azure agenta systemu Linux](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="cloud-init"></a>Init chmury
**Ubuntu** i **CoreOS** obrazów korzystanie z inicjowaniem chmurze na platformie Azure, która zapewnia dodatkowe funkcje do inicjalizacji maszyny wirtualnej.

* [Jak można wstawić danych niestandardowych](../windows/classic/inject-custom-data.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [Niestandardowe dane i inicjowania chmurze na platformie Microsoft Azure](https://azure.microsoft.com/blog/2014/04/21/custom-data-and-cloud-init-on-windows-azure/)
* [Tworzenie partycji wymiany Azure przy użyciu inicjowania chmury](https://wiki.ubuntu.com/AzureSwapPartitions)
* [Jak używać CoreOS na platformie Azure](https://coreos.com/os/docs/latest/booting-on-azure.html)

## <a name="virtual-machine-image-capture"></a>Przechwyć obraz maszyny wirtualnej
Platforma Azure oferuje możliwość przechwytywania stanu z istniejącej maszyny wirtualnej do obrazu, który następnie można wdrożyć dodatkowe maszyny wirtualnej wystąpień. Agent systemu Linux platformy Azure może być używany do wycofania, niektóre dostosowania, na który została wykonana podczas procesu inicjowania obsługi administracyjnej. Może wykonaj poniższe kroki, aby przechwycić maszynę wirtualną jako obrazu:

1. Uruchom **agenta waagent-deprovision** cofnąć dostosowania inicjowania obsługi administracyjnej. Lub **agenta waagent-deprovision + użytkownika** można opcjonalnie usunąć konto użytkownika określone podczas inicjowania obsługi i wszystkie skojarzone dane.
2. Zamknij dół/Wyłącz maszynę wirtualną.
3. Kliknij przycisk **przechwytywania** w portalu Azure lub użyj programu PowerShell lub interfejsu wiersza polecenia narzędzia Przechwytywanie maszyny wirtualnej jako obraz.
   
   * Zobacz: [Przechwytywanie maszyny wirtualnej systemu Linux w celu użycia jako szablon](classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

## <a name="attaching-disks"></a>Dołączanie dysków
Każda maszyna wirtualna ma tymczasowej lokalnego *zasobu dysku* dołączony. Ponieważ dane na dysku zasobu nie może być trwałe między ponownymi uruchomieniami komputera jest często używany przez aplikacje i procesów uruchomionych na maszynie wirtualnej dla przejściowy i **tymczasowego** magazynu danych. Służy również do przechowywania strony lub zamienić pliki systemu operacyjnego.

W systemie Linux, dysk zasobów jest zwykle zarządzane przez agenta systemu Linux platformy Azure i automatycznie zainstalowany **/mnt/zasobu** (lub **katalogu/mnt** na obrazach Ubuntu).

> [!NOTE]
> Należy zauważyć, że zasób dysku **tymczasowego** na dysku i może być usunięty i ponownie sformatowany po ponownym uruchomieniu maszyny Wirtualnej.
> 
> 

W systemie Linux dysku danych może mieć nazwę przez jądro jako `/dev/sdc`, a użytkownicy będą musieli partycji, formatowanie i zainstalowania tego zasobu. Ten temat znajdują się instrukcje w samouczku: [jak dołączyć dysku danych do maszyny wirtualnej](../windows/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

* **Zobacz też:** [należy skonfigurować oprogramowanie RAID w systemie Linux](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) & [skonfigurować LVM na Maszynę wirtualną systemu Linux na platformie Azure](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

