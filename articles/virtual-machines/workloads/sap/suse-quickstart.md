---
title: aaaTesting SAP NetWeaver na maszynach wirtualnych programu Microsoft Azure SUSE Linux | Dokumentacja firmy Microsoft
description: "Testowanie środowiska SAP NetWeaver na maszynach wirtualnych systemu SUSE Linux na platformie Microsoft Azure"
services: virtual-machines-linux
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 645e358b-3ca1-4d3d-bf70-b0f287498d7a
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/14/2017
ms.author: hermannd
ms.openlocfilehash: 0e3faab05417a1a15541e2b79aa7eddacda44611
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="running-sap-netweaver-on-microsoft-azure-suse-linux-vms"></a>Uruchamianie środowiska SAP NetWeaver na maszynach wirtualnych systemu SUSE Linux na platformie Microsoft Azure
W tym artykule opisano różne rzeczy tooconsider po uruchomieniu programu SAP NetWeaver na maszynach wirtualnych Microsoft Azure SUSE Linux (VM). Począwszy od maj 2016 19 SAP NetWeaver jest oficjalnie obsługiwana na SUSE maszyn wirtualnych systemu Linux na platformie Azure. Wszystkie szczegóły dotyczące wersji systemu Linux, wersje jądra SAP i tak dalej znajduje się w 1928533 Uwaga SAP "aplikacje SAP na platformie Azure: obsługiwanych produktach i typy maszyna wirtualna platformy Azure".
Dalsze dokumentację dotyczącą SAP na maszynach wirtualnych systemu Linux można znaleźć tutaj: [przy użyciu programu SAP na maszynach wirtualnych systemu Linux (VM)](get-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Witaj następujących informacji powinny pomóc w uniknięciu niektórych potencjalne pułapki związane.

## <a name="suse-images-on-azure-for-running-sap"></a>Obrazy SUSE na platformie Azure do uruchamiania programu SAP
Dla programu SAP NetWeaver działających na platformie Azure, użyj tylko SUSE Linux Enterprise Server SLES 12 (SPx) — Zobacz też Uwaga SAP 1928533. Specjalne obrazu SUSE jest hello Azure Marketplace ("SLES 11 z dodatkiem SP3 na SAP CAL"), ale to nie jest przeznaczony do użytku ogólnego. Nie należy używać tego obrazu, ponieważ jest on zarezerwowany dla hello [biblioteki urządzenia chmury SAP](https://cal.sap.com/) rozwiązania.  

Dla wszystkich nowych testów i instalacji na platformie Azure, należy użyć Menedżera zasobów Azure. toolook dla obrazów SUSE SLES i wersji przy użyciu programu Azure PowerShell lub hello Azure interfejsu wiersza polecenia (CLI) hello Użyj następującego polecenia. Następnie można hello wyjścia, na przykład toodefine hello obrazu systemu operacyjnego w szablonie do wdrażania nowej maszyny Wirtualnej systemu Linux SUSE JSON.
Te polecenia programu PowerShell są prawidłowe dla programu Azure PowerShell w wersji 1.0.1 i nowszym.

Gdy jest nadal możliwe toouse hello standardowych SLES obrazów instalacji SAP zalecane jest użycie toomake hello SLES nowe dla obrazów SAP, które są dostępne obecnie na hello Azure obrazem galerii. Można znaleźć więcej informacji na temat tych obrazów na powitania odpowiadającego [strony portalu Azure Marketplace]( https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SUSE.SLES-SAP ) lub hello [strony sieci web SUSE — często zadawane pytania dotyczące SLES dla SAP]( https://www.suse.com/products/sles-for-sap/frequently-asked-questions/ ).


* Wyszukaj istniejących wydawców w tym SUSE:
  
   ```
   PS  : Get-AzureRmVMImagePublisher -Location "West Europe"  | where-object { $_.publishername -like "*US*"  }
   CLI : azure vm image list-publishers westeurope | grep "US"
   ```
* Wyszukaj istniejących ofert z SUSE:
  
   ```
   PS  : Get-AzureRmVMImageOffer -Location "West Europe" -Publisher "SUSE"
   CLI : azure vm image list-offers westeurope SUSE
   ```
* Wyszukaj ofert SUSE SLES:
  
   ```
   PS  : Get-AzureRmVMImageSku -Location "West Europe" -Publisher "SUSE" -Offer "SLES"
   PS  : Get-AzureRmVMImageSku -Location "West Europe" -Publisher "SUSE" -Offer "SLES-SAP"
   CLI : azure vm image list-skus westeurope SUSE SLES
   CLI : azure vm image list-skus westeurope SUSE SLES-SAP
   ```
* Wygląd dla określonej wersji SLES SKU:
  
   ```
   PS  : Get-AzureRmVMImage -Location "West Europe" -Publisher "SUSE" -Offer "SLES" -skus "12-SP2"
   PS  : Get-AzureRmVMImage -Location "West Europe" -Publisher "SUSE" -Offer "SLES-SAP" -skus "12-SP2"
   CLI : azure vm image list westeurope SUSE SLES 12-SP2
   CLI : azure vm image list westeurope SUSE SLES-SAP 12-SP2
   ```

## <a name="installing-walinuxagent-in-a-suse-vm"></a>Instalowanie na maszynie wirtualnej SUSE WALinuxAgent
Witaj agenta o nazwie WALinuxAgent jest częścią hello SLES obrazów w hello Azure Marketplace. Informacje o instalowaniu go ręcznie (na przykład podczas przekazywania SLES OS wirtualny dysk twardy (VHD) z lokalnymi) zobacz:

* [OpenSUSE](http://software.opensuse.org/package/WALinuxAgent)
* [Azure](../../linux/endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [SUSE](https://www.suse.com/communities/blog/suse-linux-enterprise-server-configuration-for-windows-azure/)

## <a name="sap-enhanced-monitoring"></a>SAP "rozszerzonego monitorowania"
SAP "rozszerzonego monitorowania" jest obowiązkowy toorun wymagań wstępnych SAP na platformie Azure. Sprawdź, czy szczegóły SAP Pamiętaj 2191498 "SAP na Linux z: rozszerzonego monitorowania Azure".

## <a name="attaching-azure-data-disks-tooan-azure-linux-vm"></a>Dołączanie danych Azure tooan dysków maszyny Wirtualnej systemu Linux platformy Azure
Należy nigdy nie Zainstaluj tooan dysków danych Azure maszyny Wirtualnej systemu Linux platformy Azure przy użyciu identyfikatora hello urządzenia. Zamiast tego należy użyć hello unikatowym identyfikatorem (UUID). W przypadku używania narzędzi graficznych toomount danych Azure dysków, na przykład, należy zachować ostrożność. Sprawdź wpisy hello w /etc/fstab.

Hello problem z Identyfikatorem urządzenia hello jest, że może go zmienić, a następnie hello maszyny Wirtualnej platformy Azure może Odłóż hello procesu rozruchu. toomitigate hello problem, można dodać parametr nofail hello w /etc/fstab. Jednak należy zachować ostrożność przy nofail ponieważ aplikacji może użyć punktu instalacji hello jako przed i może zapisać do systemu plików hello głównego, w przypadku, gdy dysk danych zewnętrznych Azure nie został zainstalowany podczas rozruchu hello.

toomounting jedynym wyjątkiem Hello za pomocą identyfikatora UUID jest dołączanie dysku systemu operacyjnego w celu rozwiązywania problemów, zgodnie z opisem w hello następujących sekcji.

## <a name="troubleshooting-a-suse-vm-that-isnt-accessible-anymore"></a>Rozwiązywanie problemów z SUSE maszynę Wirtualną, która nie jest już dostępny
Mogą wystąpić sytuacje, w którym SUSE maszyny Wirtualnej na platformie Azure, zawiesza się hello procesu rozruchu (na przykład z powodu błędu związane z instalowania dysków). Ten problem można sprawdzić za pomocą funkcji diagnostyki rozruchu powitania dla maszyn wirtualnych platformy Azure w wersji 2 w hello portalu Azure. Aby uzyskać więcej informacji, zobacz [diagnostyki rozruchu](https://azure.microsoft.com/blog/boot-diagnostics-for-virtual-machines-v2/).

Jednym ze sposobów toosolve hello problem jest dysk systemu operacyjnego hello tooattach z hello uszkodzony tooanother maszyny Wirtualnej VM SUSE na platformie Azure. Następnie wprowadź odpowiednie zmiany, takie jak /etc/fstab edytowanie lub usuwanie reguł udev sieci, zgodnie z opisem w następnej sekcji hello.

Brak jednego tooconsider ważne. Wdrażanie kilka SUSE maszyn wirtualnych z takiego samego obrazu w portalu Azure Marketplace, (na przykład SLES 11 z dodatkiem SP4) powoduje, że hello hello OS tooalways dysku go zainstalować hello sam identyfikator UUID. W związku z tym przy użyciu hello tooattach identyfikatora UUID dysku systemu operacyjnego z inną maszynę Wirtualną, która została wdrożona przy użyciu hello takiego samego obrazu portalu Azure Marketplace spowoduje dwóch UUID nie są identyczne. To powoduje występowanie problemów i może oznaczać, że hello przeznaczony do rozwiązywania maszyny Wirtualnej w rzeczywistości zostanie uruchomiony z hello dołączony, a uszkodzonego dysku systemu operacyjnego zamiast hello oryginału.

Istnieją dwa sposoby tooavoid to:

* Użyj innego obrazu portalu Azure Marketplace dla hello Rozwiązywanie problemów z maszyny Wirtualnej (na przykład SLES 11 SPx zamiast SLES 12).
* Nie należy dołączyć hello uszkodzony dysk systemu operacyjnego z inną maszynę Wirtualną przy użyciu identyfikatora UUID--Użyj coś innego.

## <a name="uploading-a-suse-vm-from-on-premises-tooazure"></a>Przekazywanie SUSE maszyny Wirtualnej z lokalnymi tooAzure
Opis tooupload kroki hello SUSE maszyny Wirtualnej z lokalnymi tooAzure, zobacz [przygotowanie SLES lub openSUSE maszyny wirtualnej na platformie Azure](../../linux/suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Tooupload Maszynę wirtualną bez hello deprovision krok na końcu hello (na przykład tookeep istniejącą instalację programu SAP, a także nazwę hosta hello), sprawdzić hello następujące elementy:

* Upewnij się, że ten dysk systemu operacyjnego hello został zainstalowany przy użyciu identyfikatora UUID ani nie hello identyfikator urządzenia. Zmiana tooUUID tylko w /etc/fstab jest niewystarczający hello dysku systemu operacyjnego. Ponadto nie zapomnij tooadapt hello rozruchowym za pośrednictwem YaST lub edytując /boot/grub/menu.lst.
* Jeśli używasz hello formatu VHDX dla dysku systemu operacyjnego SUSE hello i przekonwertować go tooVHD o przekazywaniu tooAzure, jest bardzo prawdopodobne, urządzenie sieci hello ulegnie zmianie z eth0 tooeth1. tooavoid problemów, gdy jest uruchamiany na platformie Azure później, zmień tooeth0 Wstecz, zgodnie z opisem w [ustalania eth0 w sklonować SLES 11 VMware](https://dartron.wordpress.com/2013/09/27/fixing-eth1-in-cloned-sles-11-vmware/).

Ponadto w toowhat opisaną w artykule hello, firma Microsoft zaleca, Usuń to:

   /lib/udev/rules.d/75-persistent-NET-Generator.Rules

Można także zainstalować hello toohelp agenta systemu Linux platformy Azure (agenta waagent) można uniknąć potencjalnych problemów, tak długo, jak wiele kart sieciowych nie istnieją.

## <a name="deploying-a-suse-vm-on-azure"></a>Wdrażanie SUSE maszyny Wirtualnej na platformie Azure
Należy utworzyć nowe SUSE maszyn wirtualnych przy użyciu plików szablonu JSON w hello nowy model usługi Azure Resource Manager. Po utworzeniu pliku szablonu JSON hello hello maszyny Wirtualnej można wdrożyć przy użyciu następującego polecenia interfejsu wiersza polecenia, jako alternatywnej tooPowerShell hello:

   ```
   azure group deployment create "<deployment name>" -g "<resource group name>" --template-file "<../../filename.json>"

   ```
Aby uzyskać więcej informacji o plikach szablonu JSON, zobacz [szablonów Authoring Azure Resource Manager](../../../resource-group-authoring-templates.md) i [szablonów Szybki Start Azure](https://azure.microsoft.com/documentation/templates/).

Aby uzyskać więcej informacji dotyczących interfejsu wiersza polecenia i usługi Azure Resource Manager, zobacz [Użyj hello Azure CLI for Mac, Linux i Windows za pomocą Menedżera zasobów Azure](../../../xplat-cli-azure-resource-manager.md).

## <a name="sap-license-and-hardware-key"></a>Klucz sprzętu i licencji SAP
Hello SAP Azure kwalifikację nowego mechanizmu zostało wprowadzone toocalculate hello SAP sprzętu klucz, który jest używany dla hello SAP licencji. jądra SAP Hello miał toobe dostosowane użycie toomake to. Wcześniejsze wersje jądra SAP dla systemu Linux nie zawiera tej zmiany kodu. Dlatego w niektórych sytuacjach (na przykład maszyny Wirtualnej Azure zmiany rozmiaru), zmienić hello SAP sprzętu klucza i hello SAP licencji zostało nie będzie już prawidłowy. Jest to rozwiązanie w hello najnowsze jądra systemu Linux SAP. Aby uzyskać więcej informacji można znaleźć Uwaga SAP 1928533.

## <a name="suse-sapconf-package--tuned-adm"></a>Pakiet sapconf SUSE / adm dopasowane
SUSE zawiera pakiet o nazwie "sapconf", która zarządza zestawem ustawienia specyficzne dla programu SAP. Więcej informacji na temat jakie ten pakiet jest i jak tooinstall i użyj go, zobacz [przy użyciu sapconf tooprepare systemów SAP toorun SUSE Linux Enterprise Server](https://www.suse.com/communities/blog/using-sapconf-to-prepare-suse-linux-enterprise-server-to-run-sap-systems/) i [co to jest sapconf lub jak tooprepare SUSE Linux Enterprise Serwer z systemami SAP? ](http://scn.sap.com/community/linux/blog/2014/03/31/what-is-sapconf-or-how-to-prepare-a-suse-linux-enterprise-server-for-running-sap-systems).

Witaj międzyczasie ma nowego narzędzia, która zastępuje sapconf - dopasowane adm. Co można znaleźć więcej informacji o tym narzędziu po hello dwa łącza poniżej.

SLES dokumentację dotyczącą profilu dopasowane adm sap-hana można znaleźć [tutaj](https://www.suse.com/documentation/sles-for-sap-12/book_s4s/data/sec_s4s_configure_sapconf.html) 

Systemy dostrajania dla obciążeń SAP z dopasowane adm — można znaleźć [tutaj](https://www.suse.com/documentation/sles-for-sap-12/pdfdoc/book_s4s/book_s4s.pdf) w rozdziale 6.2

## <a name="nfs-share-in-distributed-sap-installations"></a>W instalacji programu SAP rozproszonych udziału NFS
Jeśli masz instalacją rozproszoną — na przykład, gdzie mają tooinstall hello w bazie danych i przy hello SAP aplikacji serwerów w oddzielnych maszyn wirtualnych — można udostępnić katalogu /sapmnt hello za pośrednictwem sieciowego systemu plików (NFS). Jeśli masz problemy z hello kroki instalacji po utworzeniu udziału NFS dla /sapmnt powitalne, sprawdź toosee, jeśli ustawiono "no_root_squash" hello udziału.

## <a name="logical-volumes"></a>Woluminy logiczne
W przeszłości hello ile wymagane dużą logiczne na wielu dyskach danych Azure (na przykład w przypadku hello bazy danych SAP), został zalecane toouse mdadm lvm pełni nie został jeszcze zatwierdzonych na platformie Azure. toolearn tooset się RAID systemu Linux na platformie Azure przy użyciu mdadm, zobacz temat [należy skonfigurować oprogramowanie RAID w systemie Linux](../../linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). W hello tego czasu od początku maja 2016 również lvm jest w pełni obsługiwany na platformie Azure i mogą być używane jako alternatywne toomdadm. Aby uzyskać dodatkowe informacje dotyczące lvm na platformie Azure, zobacz [skonfigurować LVM na maszynie Wirtualnej systemu Linux na platformie Azure](../../linux/configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="azure-suse-repository"></a>Azure SUSE repozytorium
Jeśli masz problem z repozytorium Azure SUSE standardowe toohello dostępu, możesz użyć tooreset prostego polecenia go. Może się to zdarzyć, jeśli tworzenie prywatnych obrazu systemu operacyjnego w regionie Azure, a następnie kopiowania hello obrazu tooa innym regionie, w którym ma toodeploy nowych maszyn wirtualnych, które są oparte na tym prywatnej obrazu systemu operacyjnego. Uruchom hello następujące polecenia wewnątrz hello maszyny Wirtualnej:

   ```
   service guestregister restart
   ```

## <a name="gnome-desktop"></a>Gnome pulpitu
Toouse hello Gnome pulpitu tooinstall całego systemu pokaz SAP w jednej maszyny Wirtualnej — łącznie z graficznym interfejsem użytkownika SAP, przeglądarki i konsoli zarządzania programu SAP — należy użyć tego tooinstall wskazówki na hello Azure SLES obrazów:

   Dla SLES 11:

   ```
   zypper in -t pattern gnome
   ```

   Dla SLES 12:

   ```
   zypper in -t pattern gnome-basic
   ```

## <a name="sap-support-for-oracle-on-linux-in-hello-cloud"></a>Obsługa Oracle w systemie Linux w chmurze hello SAP
Brak ograniczeń pomocy technicznej z programem Oracle w systemie Linux w zwirtualizowanych środowiskach. Chociaż nie jest to tematu specyficzne dla platformy Azure, jest ważne toounderstand. W systemie SUSE lub Red Hat w chmurze publicznej, takich jak Azure SAP nie obsługuje Oracle. toodiscuss w tym temacie, skontaktuj się bezpośrednio z programu Oracle.

