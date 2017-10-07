---
title: "Szybki Start: Instalacja ręczna pojedynczym wystąpieniem SAP HANA na maszynach wirtualnych platformy Azure | Dokumentacja firmy Microsoft"
description: "Przewodnik Szybki start dotyczący instalacji ręcznej z pojedynczym wystąpieniem SAP HANA na maszynach wirtualnych platformy Azure"
services: virtual-machines-linux
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: c51a2a06-6e97-429b-a346-b433a785c9f0
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 09/15/2016
ms.author: hermannd
ms.openlocfilehash: 57b58b8e07379eed5641f5f89d55b38f52c69e44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-manual-installation-of-single-instance-sap-hana-on-azure-vms"></a>Szybki Start: Instalacja ręczna pojedynczym wystąpieniem SAP HANA na maszynach wirtualnych Azure
## <a name="introduction"></a>Wprowadzenie
Ten przewodnik pomaga skonfigurować pojedynczym wystąpieniem SAP HANA na maszynach wirtualnych platformy Azure (VM), instalując SAP NetWeaver 7.5 i SAP HANA 1.0 SP12 ręcznie. Hello ten przewodnik koncentruje się na temat wdrażania SAP HANA na platformie Azure. Nie zastępuje dokumentacji SAP. 

>[!Note]
>Ten przewodnik zawiera opis wdrożenia SAP HANA na maszynach wirtualnych platformy Azure. Informacji o wdrażaniu SAP HANA do wystąpień dużych HANA, zobacz [przy użyciu programu SAP na maszynach wirtualnych platformy Azure (VM)](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/get-started).
 
## <a name="prerequisites"></a>Wymagania wstępne
W tym przewodniku założono, że czytelnik zna takie infrastruktury jako podstawy usługi (IaaS), jako:
 * Jak toodeploy maszyny wirtualne lub sieci wirtualnych za pośrednictwem hello portalu Azure lub programu PowerShell.
 * Hello Azure i platform interfejsu wiersza polecenia (CLI), w tym hello opcja toouse JavaScript Object Notation (JSON) szablony.

W tym przewodniku założono również, że czytelnik zna:
* SAP HANA i SAP NetWeaver i w jaki sposób tooinstall ich lokalnymi.
* Instalowanie i SAP HANA i SAP wystąpień aplikacji na platformie Azure.
* Witaj następujących koncepcje i procedury:
   * Planowanie wdrożenia SAP na platformie Azure, w tym planowania sieci wirtualnej platformy Azure i użycia usługi Azure Storage. Zobacz [SAP NetWeaver na maszynach wirtualnych Azure (VM) — przewodnik dotyczący planowania i implementacji](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/planning-guide).
   * Wdrożenie zasad i sposoby toodeploy maszyn wirtualnych na platformie Azure. Zobacz [wdrażania maszyn wirtualnych platformy Azure dla programu SAP](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/deployment-guide).
   * Wysoka dostępność dla programu SAP NetWeaver ASCS (ABAP SAP centralnej usługi), SCS (SAP centralnej usługi) i Wywołujących (obliczone rozliczenie) na platformie Azure. Zobacz [wysoka dostępność dla programu SAP NetWeaver na maszynach wirtualnych Azure](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/high-availability-guide).
   * Więcej informacji na temat wydajności tooimprove dzięki wykorzystaniu instalacji wielu SID ASCS/SCS na platformie Azure. Zobacz [tworzenia konfiguracji wielu SID SAP NetWeaver](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/high-availability-multi-sid). 
   * Zasady uruchamiania programu SAP NetWeaver oparte na maszynach opartych na systemie Linux na platformie Azure. Zobacz [uruchomione na maszynach wirtualnych programu Microsoft Azure SUSE Linux SAP NetWeaver](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/suse-quickstart). Ten przewodnik zawiera ustawienia specyficzne dla systemu Linux w maszynach wirtualnych platformy Azure i uzyskać szczegółowe informacje dotyczące jak tooproperly dołączać tooLinux dyski magazynu Azure maszyn wirtualnych.

W tej chwili maszynach wirtualnych platformy Azure certyfikowanych przez SAP SAP HANA skalowanie w pionie tylko konfiguracji. Konfiguracje skalowalnego w poziomie z obciążeniami SAP HANA nie są jeszcze obsługiwane. SAP HANA wysokiej dostępności w przypadku konfiguracji skalowania w górę, zobacz [wysoką dostępność SAP HANA na maszynach wirtualnych platformy Azure (VM)](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/sap-hana-high-availability).

Jeśli szukają tooget wystąpieniem SAP HANA lub S/4HANA lub system BW/4HANA wdrożona w czasie bardzo szybko, należy rozważyć użycie hello [biblioteki urządzenia chmury SAP](http://cal.sap.com). Możesz znaleźć dokumentację dotyczącą wdrażania, na przykład S/4HANA systemu za pośrednictwem SAP CAL na platformie Azure w [w tym przewodniku](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/cal-s4h). Toohave wystarczy subskrypcji platformy Azure i użytkownika SAP, który może być zarejestrowane przy użyciu biblioteki urządzenia chmury SAP.

## <a name="additional-resources"></a>Dodatkowe zasoby
### <a name="sap-hana-backup"></a>Kopia zapasowa SAP HANA
Aby uzyskać informacji na temat tworzenia kopii zapasowej bazy danych SAP HANA na maszynach wirtualnych Azure zobacz:
* [Podręcznik tworzenia kopii zapasowej programu SAP HANA na maszynach wirtualnych platformy Azure](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/sap-hana-backup-guide)
* [SAP HANA Azure Backup na poziomie plików](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/sap-hana-backup-file-level)
* [SAP HANA kopię zapasową pamięci masowej migawki](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/sap-hana-backup-storage-snapshots)

### <a name="sap-cloud-appliance-library"></a>Biblioteka urządzenia chmury SAP
Aby uzyskać informacje na temat używania biblioteki urządzenia chmury SAP toodeploy S/4HANA lub BW/4HANA, zobacz [wdrożenia SAP S/4HANA lub BW/4HANA w systemie Microsoft Azure](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/cal-s4h).

### <a name="sap-hana-supported-operating-systems"></a>SAP HANA obsługiwanych systemów operacyjnych
Aby uzyskać informacje na systemy operacyjne obsługiwane SAP HANA, zobacz [SAP Obsługa Uwaga #2235581 - SAP HANA: systemy operacyjne obsługiwane](https://launchpad.support.sap.com/#/notes/2235581/E). Maszyny wirtualne platformy Azure obsługuje tylko podzbiór tych systemów operacyjnych. Witaj następujące systemy operacyjne są obsługiwane toodeploy SAP HANA na platformie Azure: 

* SUSE Linux Enterprise Server 12.x
* Red Hat Enterprise Linux 7.2

Dodatkową dokumentację SAP SAP HANA o różnych systemów operacyjnych Linux zobacz:

* [Uwaga Obsługa SAP &#171356; - oprogramowania SAP w systemie Linux: informacje ogólne](https://launchpad.support.sap.com/#/notes/1984787)
* [Obsługa Uwaga &#1944799; - SAP HANA wskazówki dotyczące instalacji systemu operacyjnego SLES SAP](http://go.sap.com/documents/2016/05/e8705aae-717c-0010-82c7-eda71af511fa.html)
* [Uwaga Obsługa SAP #2205917 - SAP HANA DB zalecane ustawienia systemu operacyjnego dla SLES 12 aplikacje SAP](https://launchpad.support.sap.com/#/notes/2205917/E)
* [Uwaga Obsługa SAP &#1984787; - SUSE Linux Enterprise Server 12: Informacje o instalacji](https://launchpad.support.sap.com/#/notes/1984787)
* [Uwaga Obsługa SAP &#1391070; - rozwiązań UUID systemu Linux](https://launchpad.support.sap.com/#/notes/1391070)
* [SAP Uwaga Obsługa &#2009879; - SAP HANA wytyczne dotyczące systemu operacyjnego systemu Red Hat Enterprise Linux (RHEL)](https://launchpad.support.sap.com/#/notes/2009879)
* [2292690 - SAP HANA DB: OS zalecane ustawienia dla systemów RHEL 7](https://launchpad.support.sap.com/#/notes/2292690/E)

### <a name="sap-monitoring-in-azure"></a>SAP monitorowania na platformie Azure
Aby uzyskać informacji na temat SAP monitorowania na platformie Azure zobacz:

* [Uwaga SAP 2191498](https://launchpad.support.sap.com/#/notes/2191498/E). Ta uwaga omówiono SAP "rozszerzonego monitorowania" z maszyn wirtualnych systemu Linux na platformie Azure. 
* [Uwaga SAP 1102124](https://launchpad.support.sap.com/#/notes/1102124/E). Ta uwaga omówiono SAPOSCOL w systemie Linux. 
* [Uwaga SAP 2178632](https://launchpad.support.sap.com/#/notes/2178632/E). Ta uwaga omówiono kluczowe metryki monitorowania dla programu SAP w systemie Microsoft Azure.

### <a name="azure-vm-types"></a>Typy maszyny Wirtualnej platformy Azure
Typy maszyny Wirtualnej platformy Azure i scenariusze obsługiwane SAP obciążenia używane z SAP HANA są udokumentowane w artykule [IaaS platformy certyfikat SAP](https://www.sap.com/dmc/exp/2014-09-02-hana-hardware/enEN/iaas.html). 

Azure typy maszyn wirtualnych, które certyfikowanych przez SAP dla programu SAP NetWeaver lub hello S/4HANA warstwy aplikacji są udokumentowane w artykule [1928533 Uwaga SAP — aplikacje SAP na platformie Azure: typy obsługiwanych produktów i maszyny Wirtualnej Azure](https://launchpad.support.sap.com/#/notes/1928533/E).

>[!Note]
>Integracja SAP Linux Azure jest obsługiwana tylko w usłudze Azure Resource Manager i nie hello klasycznego modelu wdrażania. 

## <a name="manual-installation-of-sap-hana"></a>Instalacja ręczna SAP HANA
W tym przewodniku opisano, jak toomanually zainstalować SAP HANA na maszynach wirtualnych platformy Azure na dwa sposoby:

* Za pomocą Menedżera inicjowania obsługi oprogramowania SAP (SWPM) jako część instalacji rozproszonej NetWeaver w kroku "zainstalować wystąpienie bazy danych" hello
* Za pomocą hello SAP HANA bazy danych narzędzie Menedżer cyklu życia, HDBLCM, a następnie zainstaluj NetWeaver

Umożliwia także SWPM tooinstall wszystkich składników (SAP HANA, serwer aplikacji hello SAP i hello ASCS wystąpienia) w jedną maszynę Wirtualną z jednej, zgodnie z opisem w tym [anonsu blogu SAP HANA](https://blogs.saphana.com/2013/12/31/announcement-sap-hana-and-sap-netweaver-as-abap-deployed-on-one-server-is-generally-available/). Ta opcja nie jest opisane w tym przewodniku Szybki Start, ale hello są problemy, które należy wziąć pod uwagę hello takie same.

Przed rozpoczęciem instalacji, zaleca się przeczytanie hello "Preparing Azure maszyn wirtualnych dla ręcznej instalacji SAP HANA" dalszej części tego przewodnika. Dzięki temu można zapobiec kilka podstawowych błędów, które mogą wystąpić, gdy używasz tylko domyślną konfigurację maszyny Wirtualnej platformy Azure.

## <a name="key-steps-for-sap-hana-installation-when-you-use-sap-swpm"></a>Klucza kroki instalacji SAP HANA używania SAP SWPM
Ta sekcja zawiera listę kluczy kroki ręczne, jednego wystąpienia instalacji SAP HANA hello realizując instalację tooperform rozproszonej SAP NetWeaver w wersji 7.5 SAP SWPM. poszczególne kroki Hello są szczegółowo w zrzutach ekranu w dalszej części tego przewodnika.

1. Tworzenie sieci wirtualnej platformy Azure, zawierającą testu dwóch maszyn wirtualnych.
2. Wdróż hello dwóch maszyn wirtualnych platformy Azure z systemami operacyjnymi (w naszym przykładzie SUSE Linux Enterprise Server (SLES) i SLES dla dodatku SP1 dla programu SAP aplikacji 12), zgodnie z toohello modelu usługi Azure Resource Manager.
3. Dołącz dwa standardowe Azure lub serwera aplikacji toohello dysków (na przykład dysków 75 GB lub 500 GB) magazynu premium maszyny Wirtualnej.
4. Dołącz serwer bazy danych HANA toohello dyski magazynu premium maszyny Wirtualnej. Aby uzyskać więcej informacji zobacz sekcję "Dysk instalacji" hello później w tym przewodniku.
5. W zależności od wymagań dotyczących rozmiaru lub przepływności dołączyć wiele dysków, a następnie utwórz woluminy rozłożone przy użyciu zarządzania woluminu logicznego lub narzędzia administracyjnego wielu urządzeń (MDADM) na poziomie systemu operacyjnego hello wewnątrz hello maszyny Wirtualnej.
6. Utwórz XFS systemów plików na powitania dołączone dyski lub woluminy logiczne.
7. Zainstaluj hello nowych XFS pliku systemów na poziomie hello systemu operacyjnego. Użyj jednego systemu plików dla całego oprogramowania SAP hello. Użyj hello innych systemu plików dla katalogu /sapmnt hello i kopii zapasowych, np. Na serwerze bazy danych programu SAP HANA hello należy zainstalować systemów plików XFS hello na dyski magazynu premium hello jako /hana i /usr/sap. Ten proces jest konieczne tooprevent hello głównego pliku system, który jest zbyt na maszynach wirtualnych Azure Linux, z zapełnia się.
8. Wprowadź hello lokalnych adresów IP testu hello maszyn wirtualnych w pliku hello/etc/hosts.
9. Wprowadź hello **nofail** parametru w hello/etc/fstab pliku.
10. Ustaw parametry jądra systemu Linux zgodnie z wersji systemu operacyjnego Linux toohello, którego używasz. Aby uzyskać więcej informacji zobacz hello odpowiednie SAP uwag HANA i hello sekcji "Jądra parametry" w tym przewodniku.
11. Zwiększ obszar wymiany.
12. Opcjonalnie zainstalować graficznego pulpitu na powitania testu maszyn wirtualnych. W przeciwnym razie użyj SAPinst instalacji zdalnej.
13. Pobranie oprogramowania SAP hello z hello Marketplace usługi SAP.
14. Zainstaluj wystąpienie SAP ASCS hello na serwerze aplikacji hello maszyny Wirtualnej.
15. Katalog /sapmnt hello między hello test maszyn wirtualnych przy użyciu systemu plików NFS. Serwer aplikacji Hello maszyny Wirtualnej jest powitania serwera systemu plików NFS.
16. Zainstaluj wystąpienie bazy danych hello, w tym HANA, przy użyciu SWPM na serwerze bazy danych hello maszyny Wirtualnej.
17. Zainstaluj serwer podstawowy aplikacji hello (adresy) na serwerze aplikacji hello maszyny Wirtualnej.
18. Uruchom konsolę zarządzania SAP (SAP MC). Na przykład połączyć się z graficznym interfejsem użytkownika SAP lub HANA Studio.

## <a name="key-steps-for-sap-hana-installation-when-you-use-hdblcm"></a>Klucza kroki instalacji SAP HANA używania HDBLCM
Ta sekcja zawiera listę kluczy kroki ręczne, jednego wystąpienia instalacji SAP HANA hello realizując instalację tooperform rozproszonej SAP NetWeaver w wersji 7.5 SAP HDBLCM. poszczególne kroki Hello są szczegółowo w zrzutach ekranu w tym przewodniku.

1. Tworzenie sieci wirtualnej platformy Azure, zawierającą testu dwóch maszyn wirtualnych.
2. Wdrażanie dwóch maszyn wirtualnych platformy Azure z systemami operacyjnymi (w naszym przykładzie SLES i SLES SAP aplikacji 12 z dodatkiem SP1) zgodnie z toohello modelu usługi Azure Resource Manager.
3. Dołącz dwa standardowe Azure lub serwera aplikacji toohello dysków (na przykład dysków 75 GB lub 500 GB) magazynu premium maszyny Wirtualnej.
4. Dołącz serwer bazy danych HANA toohello dyski magazynu premium maszyny Wirtualnej. Aby uzyskać więcej informacji zobacz sekcję "Dysk instalacji" hello później w tym przewodniku.
5. W zależności od wymagań dotyczących rozmiaru lub przepływności Dołącz wiele dysków i utworzyć woluminy rozłożone za pomocą zarządzania woluminu logicznego lub narzędzia administracyjnego wielu urządzeń (MDADM) na poziomie systemu operacyjnego hello wewnątrz hello maszyny Wirtualnej.
6. Utwórz XFS systemów plików na powitania dołączone dyski lub woluminy logiczne.
7. Zainstaluj hello nowych XFS pliku systemów na poziomie hello systemu operacyjnego. Jeden system plików przy użyciu oprogramowania SAP hello, a użycie hello drugi hello /sapmnt katalogu i kopii zapasowych, na przykład. Na serwerze bazy danych programu SAP HANA hello należy zainstalować systemów plików XFS hello na dyski magazynu premium hello jako /hana i /usr/sap. Ten proces jest konieczne toohelp zapobiec przepełnieniu hello głównego pliku system, który jest zbyt na maszynach wirtualnych systemu Linux platformy Azure,.
8. Wprowadź hello lokalnych adresów IP testu hello maszyn wirtualnych w pliku hello/etc/hosts.
9. Wprowadź hello **nofail** parametru w hello/etc/fstab pliku.
10. Ustaw parametry jądra zgodnie z wersji systemu operacyjnego Linux toohello, którego używasz. Aby uzyskać więcej informacji zobacz hello odpowiednie SAP uwag HANA i hello sekcji "Jądra parametry" w tym przewodniku.
11. Zwiększ obszar wymiany.
12. Opcjonalnie zainstalować graficznego pulpitu na powitania testu maszyn wirtualnych. W przeciwnym razie użyj SAPinst instalacji zdalnej.
13. Pobranie oprogramowania SAP hello z hello Marketplace usługi SAP.
14. Utwórz grupę, sapsys, z grupą 1001 identyfikator na serwerze bazy danych HANA hello maszyny Wirtualnej.
15. Zainstaluj SAP HANA na powitania serwera bazy danych maszyny Wirtualnej za pomocą HANA bazy danych Lifecycle Manager (HDBLCM).
16. Zainstaluj wystąpienie SAP ASCS hello na serwerze aplikacji hello maszyny Wirtualnej.
17. Katalog /sapmnt hello między hello test maszyn wirtualnych przy użyciu systemu plików NFS. Serwer aplikacji Hello maszyny Wirtualnej jest powitania serwera systemu plików NFS.
18. Zainstaluj wystąpienie bazy danych hello, w tym HANA, przy użyciu SWPM na serwerze bazy danych HANA hello maszyny Wirtualnej.
19. Zainstaluj serwer podstawowy aplikacji hello (adresy) na serwerze aplikacji hello maszyny Wirtualnej.
20. Uruchom SAP MC. Połącz za pomocą interfejsu GUI SAP lub HANA Studio.

## <a name="preparing-azure-vms-for-a-manual-installation-of-sap-hana"></a>Przygotowywanie maszyn wirtualnych platformy Azure do ręcznego instalowania SAP HANA
W tej sekcji omówiono hello następujące tematy:

* Aktualizacje systemu operacyjnego
* Konfiguracja dysków
* Parametry jądra
* systemy plików
* Plik Hello/etc/hosts
* Hello/etc/fstab pliku

### <a name="os-updates"></a>Aktualizacje systemu operacyjnego
Sprawdź, czy system operacyjny Linux aktualizacje i poprawki przed zainstalowaniem dodatkowego oprogramowania. Instalując poprawkę, może być możliwe tooavoid technicznej toohello wywołania.

Upewnij się, że używasz:
* SUSE Linux Enterprise Server dla programu SAP aplikacji.
* Red Hat Enterprise Linux dla aplikacje SAP lub Red Hat Enterprise Linux dla programu SAP HANA. 

Jeśli nie jest jeszcze zarejestrować hello wdrożenia systemu operacyjnego z subskrypcji Linux hello Linux dostawcy. Należy pamiętać, że SUSE ma obrazów systemu operacyjnego dla aplikacje SAP, które już zawierają usług i które są zarejestrowane automatycznie.

Oto przykład sprawdzania dostępnych poprawek dla systemu SUSE Linux przy użyciu hello **zypper** polecenia:

 `sudo zypper list-patches`

W zależności od rodzaju hello problem poprawki są klasyfikowane według kategorii i ważności. Są często używane wartości dla kategorii: **zabezpieczeń**, **zalecane**, **opcjonalne**, **funkcji**, **dokumentu**, lub **yast**.
Są często używane wartości ważności: **krytyczne**, **ważne**, **umiarkowane**, **niski**, lub **nieokreślony**.

Witaj **zypper** polecenia jest wyszukiwany tylko hello aktualizacji, które wymagają zainstalowanych pakietów. Na przykład można użyć tego polecenia:

`sudo zypper patch  --category=security,recommended --severity=critical,important`

Możesz dodać parametr hello `--dry-run` tootest hello aktualizacji bez aktualizowania faktycznie hello systemu.


### <a name="disk-setup"></a>Konfiguracja dysków
system plików głównego Hello w Maszynę wirtualną systemu Linux na platformie Azure obowiązuje ograniczenie rozmiaru. Dlatego jest konieczne tooattach dodatkowy dysk miejsca tooan maszyny Wirtualnej platformy Azure do uruchamiania programu SAP. Dla serwera aplikacji SAP maszynach wirtualnych platformy Azure hello użycie usługi Azure standard storage dysku może być wystarczające. Jednak dla SAP HANA DBMS maszynach wirtualnych platformy Azure, użyj hello Azure Premium Storage dysków dla wdrożenia produkcyjnego i nieprodukcyjnych jest obowiązkowe.

Oparte na powitania [SAP HANA TDI przestrzeni dyskowej jest potrzebne](https://www.sap.com/documents/2015/03/74cdb554-5a7c-0010-82c7-eda71af511fa.html), widoczną powitania po konfiguracji usługi Azure Premium Storage: 

| JEDNOSTKA SKU MASZYNY WIRTUALNEJ | Pamięć RAM |  / hana/danych i dziennika/hana / <br /> paski LVM lub MDADM | / hana/udostępnionych | wolumin/root | / usr/sap |
| --- | --- | --- | --- | --- | --- |
| GS5 | 448 GB | 2 x P30 | 1 x P20 | 1 x P10 | 1 x P10 | 

W konfiguracji dysków sugerowane hello ilość danych HANA hello i wolumin dziennika są umieszczane na powitania sam zestaw dysków magazynu Azure premium, które są rozkładane LVM lub MDADM. Nie jest konieczne toodefine żadnych nadmiarowość RAID poziomu, ponieważ usługa Azure Premium Storage przechowuje trzy obrazy dysków hello w celu zapewnienia nadmiarowości. toomake konieczne jest skonfigurowanie niewystarczającego miejsca w magazynie, zapoznaj się hello [SAP HANA TDI przestrzeni dyskowej jest potrzebne](https://www.sap.com/documents/2015/03/74cdb554-5a7c-0010-82c7-eda71af511fa.html) i [przewodnik aktualizacji i instalacji serwera SAP HANA](http://help.sap.com/saphelp_hanaplatform/helpdata/en/4c/24d332a37b4a3caad3e634f9900a45/frameset.htm). Należy również rozważyć hello innego wirtualnego dysku twardego (VHD) przepływność ilości hello dyski magazynu różnych Azure premium zgodnie z opisem w [zarządzanych dysków dla maszyny wirtualne i Magazyn w warstwie Premium wysokiej wydajności](https://docs.microsoft.com/azure/storage/storage-premium-storage). 

Można dodać więcej magazyn w warstwie premium dyski maszyn wirtualnych systemu DBMS HANA toohello do przechowywania kopii zapasowych dziennika bazy danych lub transakcji.

Aby uzyskać więcej informacji na temat Witaj dwie główne narzędzia używane tooconfigure stosowanie Zobacz hello następujące artykuły:

* [Należy skonfigurować oprogramowanie RAID w systemie Linux](../../linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Skonfiguruj LVM na Maszynę wirtualną systemu Linux na platformie Azure](../../linux/configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

Aby uzyskać więcej informacji na temat dołączania dyski maszyn wirtualnych tooAzure systemem Linux jako system operacyjny gościa, zobacz [dodać tooa dysku maszyny Wirtualnej systemu Linux](../../linux/add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Usługa Azure Premium Storage umożliwia toodefine dyskowej pamięci podręcznej trybów. Dla zestawu hello rozkładane /hana/data i /hana/log powinny być wyłączone buforowanie dysku. Dla hello inne woluminy (dysków) hello buforowanie trybu powinna być ustawiona zbyt**tylko do odczytu**.

Aby uzyskać więcej informacji, zobacz [magazyn w warstwie Premium: magazyn o wysokiej wydajności dla obciążeń maszyny wirtualnej Azure](../../../storage/common/storage-premium-storage.md).

Szablony JSON próbki toofind do tworzenia maszyn wirtualnych, przejdź zbyt[szablonów Szybki Start Azure](https://github.com/Azure/azure-quickstart-templates).
Szablon maszyny wirtualnej — prosty sles Hello jest podstawowy szablon. Obejmuje on sekcji magazynu, przy użyciu dysku dodatkowe 100 GB danych. Ten szablon może służyć jako podstawa. Istnieje możliwość dostosowania hello szablonu tooyour określonej konfiguracji.

>[!Note]
>Jest ważne tooattach hello magazynu Azure dysku przy użyciu identyfikatora UUID, zgodnie z opisem w [systemem SAP NetWeaver na maszynach wirtualnych programu Microsoft Azure SUSE Linux](suse-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

W środowisku testowym hello dwa dyski standardowe magazynu Azure zostały dołączone toohello SAP aplikacji serwera maszyny Wirtualnej, pokazane na powitania po zrzut ekranu. Jeden dysk dla instalacji są przechowywane wszystkie oprogramowania SAP hello (w tym NetWeaver 7.5 SAP graficznego interfejsu użytkownika i SAP HANA). Witaj drugiego dysku zapewnić wystarczającą ilością wolnego miejsca, będzie dostępna dla dodatkowych wymagań (na przykład dane kopii zapasowej i testowych), a dla toobe katalogu (to znaczy SAP profilów) /sapmnt hello współdzielona przez wszystkie maszyny wirtualne, które należą toohello poziomą tego samego SAP.

![Wyświetlanie danych dwóch dysków i ich rozmiary SAP HANA aplikacji serwera dyski okna](./media/hana-get-started/image003.jpg)


### <a name="kernel-parameters"></a>Parametry jądra
SAP HANA wymaga określonych ustawień jądra systemu Linux, które nie są częścią hello standardowe Azure galerii obrazów i musi być ustawiony ręcznie. W zależności od tego, czy używasz SUSE lub Red Hat parametry hello mogą się różnić. Uwagi SAP Hello wymienione wcześniej zapewniają informacje o tych parametrów. Zrzuty ekranu hello jest wyświetlane użyto SUSE Linux 12 z dodatkiem SP1. 

SLES dla GA 12 aplikacje SAP i SLES dla dodatku SP1 dla programu SAP aplikacji 12 mają nowe narzędzie **dopasowane adm**, że zastępuje hello starego **sapconf** narzędzia. Jest dostępna dla profilu specjalnego SAP HANA **dopasowane adm**. tootune hello systemu SAP HANA, wprowadź następujące hello jako użytkownik główny:

   `tuned-adm profile sap-hana`

Aby uzyskać więcej informacji na temat **dopasowane adm**, zobacz hello [SUSE dokumentację dotyczącą dopasowane adm](https://www.suse.com/documentation/sles-for-sap-12/pdfdoc/sles-for-sap-12-sp1.zip).

Widać hello następującego zrzutu ekranu, jak **dopasowane adm** zmienione hello `transparent_hugepage` i `numa_balancing` wartości, zgodnie z toohello wymagane ustawienia SAP HANA.

![Narzędzie dopasowane adm Hello zmiany wartości zgodnie z ustawieniami SAP HANA toorequired](./media/hana-get-started/image005.jpg)

Użyj trwałe, ustawienia jądra SAP HANA hello toomake **grub2** na SLES 12. Aby uzyskać więcej informacji na temat **grub2**, przejdź toohello [struktury plików konfiguracji](https://www.suse.com/documentation/sles-for-sap-12/pdfdoc/sles-for-sap-12-sp1.zip) sekcji hello SUSE dokumentacji.

Witaj Poniższy zrzut ekranu przedstawia sposób hello jądra ustawienia zostały zmienione w pliku konfiguracyjnym hello i następnie skompilować przy użyciu **grub2 mkconfig**:

![Ustawienia jądra zmienić w pliku konfiguracyjnym hello i skompilowanych przy użyciu grub2 mkconfig](./media/hana-get-started/image006.jpg)

Innym rozwiązaniem jest toochange hello ustawienia za pomocą YaST i hello **moduł ładujący rozruchu** > **parametry jądra** ustawienia:

![Karta Ustawienia parametrów jądra Hello w moduł ładujący rozruchu YaST](./media/hana-get-started/image007.jpg)

### <a name="file-systems"></a>systemy plików
Witaj Poniższy zrzut ekranu przedstawia dwa systemy plików, które zostały utworzone na serwerze aplikacji programu SAP hello maszyny Wirtualnej na powitania dwóch dysków dołączonych standardowego magazynu Azure. Systemów plików typu XFS i są zainstalowane zbyt/sapdata i /sapsoftware.

Jego jest nie jest to konieczne toostructure Twojego systemów plików w ten sposób. Masz inne opcje struktury hello miejsca na dysku. Witaj najbardziej ważnym zagadnieniem jest system plików tooprevent hello głównego z brakiem wolnego miejsca.

![Dwa systemy plików utworzony na serwerze aplikacji hello SAP maszyny Wirtualnej](./media/hana-get-started/image008.jpg)

Dotyczące hello SAP HANA DB maszyny Wirtualnej, podczas instalacji bazy danych, korzystając z SAPinst (SWPM) oraz hello **typowe** opcji instalacji, wszystko jest zainstalowane w ramach /hana i /usr/sap. Domyślna lokalizacja kopii zapasowej dziennika SAP HANA hello Hello podlega /usr/sap. Ponownie ponieważ jest ważne tooprevent hello głównego pliku system z brakiem miejsca do magazynowania, upewnij się, brak wystarczającej ilości wolnego miejsca w obszarze /hana i /usr/sap przed rozpoczęciem instalacji przy użyciu SWPM SAP HANA.

Opis układ standardowy system plików hello SAP HANA, zobacz hello [przewodnik aktualizacji i instalacji serwera SAP HANA](http://help.sap.com/saphelp_hanaplatform/helpdata/en/4c/24d332a37b4a3caad3e634f9900a45/frameset.htm).

![Systemy plików dodatkowe utworzony na serwerze aplikacji hello SAP maszyny Wirtualnej](./media/hana-get-started/image009.jpg)

Po zainstalowaniu programu SAP NetWeaver na standardowe SLES/SLES obrazu galerii Azure 12 aplikacje SAP, zostanie wyświetlony komunikat z informacją, że brakuje miejsca wymiany, jak pokazano w powitania po zrzut ekranu. toodismiss tego komunikatu, można ręcznie dodać za pomocą pliku wymiany **dd**, **mkswap**, i **swapon**. jak to zrobić, wyszukaj toolearn "Plik wymiany ręczne dodawanie" w hello [hello Using Partycjonera YaST](https://www.suse.com/documentation/sles-for-sap-12/pdfdoc/sles-for-sap-12-sp1.zip) sekcji hello dokumentacji SUSE.

Innym rozwiązaniem jest obszar wymiany tooconfigure przy użyciu hello agenta maszyny Wirtualnej systemu Linux. Aby uzyskać więcej informacji, zobacz hello [Podręcznik użytkownika agenta systemu Linux Azure](../../linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

![Udzielanie porad jest obszar wymiany niewystarczające komunikat podręczny](./media/hana-get-started/image010.jpg)


### <a name="hello-etchosts-file"></a>Plik Hello/etc/hosts
Przed rozpoczęciem tooinstall SAP, upewnij się, że zawierają hello nazw hostów i adresy IP hello SAP maszyn wirtualnych w pliku/etc/hosts hello. Wdrażanie wszystkich maszyn wirtualnych SAP hello w ramach jednej sieci wirtualnej platformy Azure, a następnie użyj hello adresów IP, jak pokazano poniżej:

![Nazwy hosta i adresy IP maszyn wirtualnych SAP hello wymienione w pliku/etc/hosts hello](./media/hana-get-started/image011.jpg)

### <a name="hello-etcfstab-file"></a>Hello/etc/fstab pliku

Jest przydatne tooadd hello **nofail** pliku fstab toohello parametrów. W ten sposób, jeśli wystąpią problemy z dyskami hello hello maszyny Wirtualnej nie wykraczać hello procesu rozruchu. Jednak pamiętać, że nie mogą być dostępne dodatkowe miejsce na dysku i procesów może zapełnić hello głównym systemie plików. Jeśli brakuje /hana, nie można uruchomić SAP HANA.

![Dodaj hello nofail parametru toohello fstab plik](./media/hana-get-started/image000c.jpg)

## <a name="graphical-gnome-desktop-on-sles-12sles-for-sap-applications-12"></a>Graficzny GNOME pulpitu na SLES 12/SLES dla 12 aplikacje SAP
W tej sekcji omówiono hello następujące tematy:

* Instalowanie hello GNOME pulpitu i xrdp na SLES 12/SLES dla 12 aplikacje SAP
* Uruchomiona opartych na języku Java MC SAP przy użyciu przeglądarki Firefox na SLES 12/SLES 12 aplikacje SAP

Można również użyć rozwiązań alternatywnych, takich jak Xterminal lub VNC (nie opisano w tym przewodniku).

### <a name="installing-hello-gnome-desktop-and-xrdp-on-sles-12sles-for-sap-applications-12"></a>Instalowanie hello GNOME pulpitu i xrdp na SLES 12/SLES dla 12 aplikacje SAP
Jeśli masz tła systemu Windows można łatwo za pomocą graficznego pulpitu bezpośrednio z poziomu hello maszyn wirtualnych systemu Linux SAP toorun Firefox, SAPinst, SAP graficznego interfejsu użytkownika, SAP MC lub HANA Studio i połącz toohello maszyny Wirtualnej za pomocą protokołu RDP (Remote Desktop) hello, komputer z systemem Windows. Zależne od zasadami w firmie o dodawaniu graficzne interfejsy użytkownika tooproduction i nieprodukcyjnych systemów opartymi na systemie Linux, można tooinstall GNOME na serwerze. tooinstall hello GNOME pulpitu na Azure SLES 12/SLES dla maszyny Wirtualnej 12 aplikacje SAP:

1. Zainstaluj hello GNOME pulpitu, wprowadzając następujące polecenie (na przykład w oknie programu PuTTY) hello:

   `zypper in -t pattern gnome-basic`

2. Zainstaluj tooallow xrdp toohello połączenia maszyny Wirtualnej za pośrednictwem protokołu RDP:

   `zypper in xrdp`

3. Edytuj /etc/sysconfig/windowmanager i ustaw hello domyślne okna Menedżera tooGNOME:

   `DEFAULT_WM="gnome"`

4. Uruchom **chkconfig** toomake się upewnić, że xrdp jest uruchamiany automatycznie po ponownym uruchomieniu:

   `chkconfig -level 3 xrdp on`

5. Jeśli masz problem z hello połączenie RDP, spróbuj toorestart (z okna programu PuTTY, na przykład):

   `/etc/xrdp/xrdp.sh restart`

6. Jeśli ponowne uruchomienie xrdp wymienionych w poprzednim hello krok nie działa, sprawdź plik .pid:

   `check /var/run` 

   Wyszukaj `xrdp.pid`. Jeśli możesz znaleźć, usuń go i spróbuj ponownie toorestart.

### <a name="starting-sap-mc"></a>Uruchamianie SAP MC
Po zainstalowaniu pulpitu GNOME hello uruchamianie hello graficznego opartych na języku Java MC SAP z Firefox podczas pracy w usłudze Azure SLES 12/SLES dla maszyny Wirtualnej 12 aplikacje SAP może być wyświetlany błąd ze względu na brak Java — dodatek plug-in dla przeglądarki hello.

Witaj toostart adres URL Hello jest SAP MC `<server>:5<instance_number>13`.

Aby uzyskać więcej informacji, zobacz [hello uruchamianie opartych na sieci Web Konsola zarządzania SAP](https://help.sap.com/saphelp_nwce10/helpdata/en/48/6b7c6178dc4f93e10000000a42189d/frameset.htm).

Witaj Poniższy zrzut ekranu przedstawia hello komunikat o błędzie jest wyświetlany, gdy brak hello Java — dodatek plug-in dla przeglądarki:

![Komunikat o błędzie wskazujący brak Java — dodatek plug-in dla przeglądarki](./media/hana-get-started/image013.jpg)

Jednym ze sposobów toosolve hello problem jest hello tooinstall Brak wtyczki za pomocą YaST, jak pokazano w powitania po zrzut ekranu:

![Przy użyciu tooinstall YaST Brak wtyczki](./media/hana-get-started/image014.jpg)

Po wprowadzeniu ponownie hello adres URL konsoli zarządzania programu SAP, pojawi się komunikat pytaniem, czy użytkownik tooactivate hello wtyczki:

![Okno dialogowe, które żądają aktywacji wtyczki](./media/hana-get-started/image015.jpg)

Może również pojawi się komunikat o błędzie dotyczący brakującego pliku javafx.properties. To wymaganie toohello powiązane programu Oracle Java 1.8 dla programu SAP 7.4 graficznego interfejsu użytkownika. (Zobacz [Uwaga SAP 2059429](https://launchpad.support.sap.com/#/notes/2059424).) Hello wersję IBM Java ani pakietu openjdk hello dostarczone z SLES/SLES dla 12 aplikacje SAP obejmuje hello javafx.properties wymaganych plików. rozwiązanie Hello jest toodownload i zainstalować Java SE 8 z programu Oracle.

Wątek dyskusji hello uzyskać informacji dotyczących podobnego problemu z openjdk na openSUSE, [Leap Java 7.4 SAPGui dla openSUSE 42.1](https://scn.sap.com/thread/3908306).

## <a name="manual-installation-of-sap-hana-swpm"></a>Instalacja ręczna SAP HANA: SWPM
Seria Hello zrzuty ekranu w tej sekcji przedstawiono hello klucza kroki dotyczące instalowania programu SAP NetWeaver 7.5 i SAP HANA SP12 używania SWPM (SAPinst). W ramach instalacji NetWeaver 7.5, SWPM również hello HANA bazę danych można zainstalować jako jedno wystąpienie.

W środowisku testowym próbki zainstalowano tylko jeden serwer aplikacji zaawansowane biznesowych aplikacji programowania (ABAP). Jak pokazano na powitania po zrzut ekranu, użyliśmy hello **rozproszony System** opcji tooinstall hello ASCS i wystąpień serwera aplikacji głównej w jednej maszynie Wirtualnej platformy Azure i SAP HANA jako hello system bazy danych w innej maszynie Wirtualnej platformy Azure.

![ASCS i wystąpień serwera aplikacji głównej instalowany przy użyciu opcji rozproszony System hello](./media/hana-get-started/image012.jpg)

Po wystąpieniu ASCS hello jest zainstalowany na serwerze aplikacji hello maszyny Wirtualnej i ustaw zbyt "zielone" hello SAP Management Console (wyświetlone czcionką powitania po zrzut ekranu), hello /sapmnt katalogu (w tym katalogu profilu SAP hello) musi być udostępniona z serwerem SAP HANA DB hello maszyny Wirtualnej. Hello DB kroku instalacji potrzebuje dostępu do informacji toothis. Witaj najlepszy sposób tooprovide dostęp jest toouse systemu plików NFS, w którym można skonfigurować przy użyciu YaST.

![SAP konsoli zarządzania przedstawiający hello ASCS wystąpienia zainstalowany na serwerze aplikacji hello maszyny Wirtualnej i ustaw zbyt "zielony"](./media/hana-get-started/image016.jpg)

Na serwerze aplikacji hello wirtualna hello/sapmnt directory należy go udostępniać za pomocą systemu plików NFS przy użyciu hello **rw** i **no_root_squash** opcje. Witaj domyślne to **ro** i **root_squash**, które mogą spowodować tooproblems po zainstalowaniu hello wystąpienie bazy danych.

![Udostępnianie hello /sapmnt katalogu za pomocą systemu plików NFS przy użyciu opcji rw i no_root_squash hello](./media/hana-get-started/image017b.jpg)

Jak hello dalej zrzut ekranu pokazuje, hello /sapmnt udział z serwera aplikacji hello maszyny Wirtualnej musi być skonfigurowane na serwerze SAP HANA DB hello maszyny Wirtualnej przy użyciu **klient systemu plików NFS** (i YaST).

![udział /sapmnt Hello skonfigurowane za pomocą klienta systemu plików NFS](./media/hana-get-started/image018b.jpg)

Instalacja rozproszonej 7.5 NetWeaver tooperform (**wystąpienie bazy danych**), jak pokazano hello następującego zrzutu ekranu, zaloguj się na serwerze bazy danych programu SAP HANA toohello maszyny Wirtualnej i uruchom SWPM.

![Instalowanie wystąpienia bazy danych, rejestrując się serwera SAP HANA DB toohello maszyny Wirtualnej i uruchamianie SWPM](./media/hana-get-started/image019.jpg)

Po wybraniu **typowe** instalacji i hello nośnika instalacyjnego toohello ścieżki, wprowadź identyfikator SID bazy danych, nazwy hosta hello, liczby wystąpień hello i hasła administratora systemu hello bazy danych.

![Strona Hello SAP HANA bazy danych systemu administratora logowania](./media/hana-get-started/image035b.jpg)

Wprowadź hasło hello schematu DBACOCKPIT hello:

![pole wprowadzenia hasła Hello hello DBACOCKPIT schematu](./media/hana-get-started/image036b.jpg)

Wprowadź pytanie o hasło schematu SAPABAP1 hello:

![Wprowadź pytanie o hasło schematu SAPABAP1 hello](./media/hana-get-started/image037b.jpg)

Po zakończeniu każdego zadania zielony znacznik wyboru jest wyświetlane następnej fazy tooeach hello procesu instalacji bazy danych. wiadomości powitania "wykonywania... Baza danych została ukończona wystąpienia"jest wyświetlany.

![Zadanie zakończone okna komunikat](./media/hana-get-started/image023.jpg)

Po pomyślnej instalacji hello konsoli zarządzania programu SAP powinno również Pokaż hello wystąpienie bazy danych jako "green" i wyświetlenie hello pełną listę procesów SAP HANA (hdbindexserver, hdbcompileserver i tak dalej).

![Okno konsoli zarządzania programu SAP z listą procesów SAP HANA](./media/hana-get-started/image024.jpg)

Witaj Poniższy zrzut ekranu przedstawia hello części hello struktury plików w katalogu /hana/shared hello, który SWPM utworzony podczas instalacji HANA hello. Ponieważ nie istnieje żadne toospecify opcji inną ścieżkę, jest ważne toomount dodatkowe miejsce na dysku w katalogu /hana hello przed hello SAP HANA instalacji przy użyciu SWPM. System plików głównego hello zapobiega wyczerpaniu wolnego miejsca.

![Witaj /hana/shared katalogu struktury plików utworzony podczas instalacji HANA](./media/hana-get-started/image025.jpg)

Ten zrzut ekranu przedstawia struktury plików hello hello /usr/sap katalogu:

![Struktura pliku katalogu /usr/sap Hello](./media/hana-get-started/image026.jpg)

Ostatnim krokiem Hello hello rozproszonych ABAP instalacji jest wystąpienie serwera podstawowego aplikacji hello tooinstall:

![Wystąpienie serwera ABAP instalacji przedstawiający głównej aplikacji jako ostatni krok hello](./media/hana-get-started/image027b.jpg)

Po zainstalowaniu wystąpienie serwera podstawowego aplikacji hello i SAP graficznego interfejsu użytkownika, użyj hello **Panelu sterowania DBA** tooconfirm transakcji, które hello SAP HANA instalacji została ukończona poprawnie:

![Okno Panel sterowania DBA potwierdzenia pomyślnej instalacji](./media/hana-get-started/image028b.jpg)

Jako ostatni krok może chcesz zainstalować toofirst HANA Studio w serwera aplikacji hello SAP maszyny Wirtualnej, a następnie połącz wystąpienie SAP HANA toohello, czy jest uruchomiona na serwerze bazy danych hello maszyny Wirtualnej:

![Instalowanie programu SAP HANA Studio serwera aplikacji hello SAP maszyny Wirtualnej](./media/hana-get-started/image038b.jpg)

## <a name="manual-installation-of-sap-hana-hdblcm"></a>Instalacja ręczna SAP HANA: HDBLCM
W dodatku tooinstalling SAP HANA jako część instalacji rozproszonych za pomocą SWPM hello HANA autonomicznych można zainstalować najpierw, za pomocą HDBLCM. Na przykład można zainstalować programu SAP NetWeaver 7.5 lub. zrzuty ekranu Hello w tej sekcji przedstawiono, jak działa ten proces.

Aby uzyskać więcej informacji na temat hello HANA HDBLCM narzędzia Zobacz:

* [Po wybraniu hello Popraw SAP HANA HDBLCM Your zadania](https://help.sap.com/saphelp_hanaplatform/helpdata/en/68/5cff570bb745d48c0ab6d50123ca60/content.htm)
* [Narzędzia do zarządzania cyklem życia SAP HANA](http://saphanatutorial.com/sap-hana-lifecycle-management-tools/)
* [Przewodnik dotyczący aktualizacji i instalacji serwera SAP HANA](http://help.sap.com/hana/SAP_HANA_Server_Installation_Guide_en.pdf)

Ustawienie identyfikator dla hello grupy tooavoid problemy z domyślną `\<HANA SID\>adm user` (utworzonego przez narzędzie HDBLCM hello), zdefiniuj nową grupę o nazwie `sapsys` przy użyciu Identyfikatora grupy `1001` przed zainstalowaniem SAP HANA za pośrednictwem HDBLCM:

![Nowe grupy "sapsys" zdefiniowane przy użyciu grupy o identyfikatorze 1001](./media/hana-get-started/image030.jpg)

Po uruchomieniu HDBLCM hello po raz pierwszy, zostanie wyświetlony menu start proste. Wybierz element 1, **zainstalować nowy system**, jak pokazano w powitania po zrzut ekranu:

![Opcja "Zainstaluj nowego systemu" hello HDBLCM rozpoczęcia okna](./media/hana-get-started/image031.jpg)

Witaj Poniższy zrzut ekranu przedstawia wszystkie opcje klucza hello, które wcześniej wybrano.

> [!IMPORTANT]
> Katalogi, które są nazywane HANA dziennika i woluminów danych, a także hello ścieżki instalacji (/ hana/udostępnione w tym przykładzie) i /usr/sap, nie powinien być częścią hello głównego pliku systemu. Te katalogi należy toohello dysków danych Azure, które zostały dołączone toohello maszyny Wirtualnej (opisanej w sekcji hello "dysk instalacji"). Takie podejście zapobiega system plików głównego hello wyczerpaniu miejsca. W hello następującego zrzutu ekranu, widać, czy administrator systemu HANA hello ma identyfikator użytkownika `1005` i jest częścią hello `sapsys` grupy (identyfikator `1001`) która została zdefiniowana przed rozpoczęciem powitalne instalacji.

![Lista wszystkich najważniejsze składniki SAP HANA wcześniej wybrany](./media/hana-get-started/image032.jpg)

Możesz sprawdzić hello `\<HANA SID\>adm user` (`azdadm` w powitania po zrzut ekranu) szczegółowe informacje w katalogu hello/etc/haseł:

![HANA \<HANA SID\>adm szczegóły użytkownika na liście hello/etc/haseł katalogu](./media/hana-get-started/image033.jpg)

Po zainstalowaniu SAP HANA przy użyciu HDBLCM widać hello struktury plików w systemie SAP HANA Studio pokazane na powitania po zrzut ekranu. Witaj SAPABAP1 schemat, który zawiera wszystkie tabele SAP NetWeaver hello, nie jest jeszcze dostępna.

![Struktura pliku SAP HANA w SAP HANA Studio](./media/hana-get-started/image034.jpg)

Po zainstalowaniu SAP HANA SAP NetWeaver można zainstalować na nim. Jak pokazano hello następującego zrzutu ekranu instalacja hello została przeprowadzona jako instalacją rozproszoną przy użyciu SWPM (zgodnie z opisem w poprzedniej sekcji hello). Po zainstalowaniu hello wystąpienie bazy danych przy użyciu SWPM wprowadź hello tych samych danych za pomocą HDBLCM (na przykład nazwy hosta, identyfikator SID HANA i liczby wystąpień). Następnie SWPM korzysta z istniejącej instalacji HANA hello i dodaje więcej schematów.

![Przeprowadzane przy użyciu SWPM instalacją rozproszoną](./media/hana-get-started/image035b.jpg)

Witaj Poniższy zrzut ekranu przedstawia kroku instalacji SWPM hello gdzie wprowadź dane dotyczące schematu DBACOCKPIT hello:

![krok instalacji SWPM Hello gdzie wprowadzeniu DBACOCKPIT schemat danych](./media/hana-get-started/image036b.jpg)

Wprowadź dane dotyczące schematu SAPABAP1 hello:

![Wprowadzanie danych o hello SAPABAP1 schematu](./media/hana-get-started/image037b.jpg)

Po zakończeniu instalacji wystąpienia bazy danych SWPM hello można wyświetlić hello SAPABAP1 schematu w SAP HANA Studio:

![Schemat Hello SAPABAP1 w SAP HANA Studio](./media/hana-get-started/image038b.jpg)

Na koniec, po ukończeniu serwera aplikacji hello SAP i instalacji graficznego interfejsu użytkownika programu SAP można zweryfikować hello HANA DB wystąpienia, korzystając z hello **Panelu sterowania DBA** transakcji:

![wystąpienie bazy danych HANA Hello zweryfikować hello transakcji DBA w Panelu sterowania](./media/hana-get-started/image039b.jpg)


## <a name="sap-software-downloads"></a>Pobieranie oprogramowania SAP
Oprogramowanie można pobrać z hello Marketplace usługi SAP, jak pokazano w powitania po zrzuty ekranu.

Pobierz NetWeaver w wersji 7.5 dla systemu Linux/HANA:

 ![Okno SAP usługi instalacji i uaktualniania pobierania NetWeaver 7.5](./media/hana-get-started/image001.jpg)

Pobierz wersję platformy SP12 HANA:

 ![Okno SAP usługi instalacji i uaktualniania wersji platformy SP12 HANA pobierania](./media/hana-get-started/image002.jpg)

