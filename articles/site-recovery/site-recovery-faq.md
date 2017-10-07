---
title: "Usługa Azure Site Recovery: Często zadawane pytania | Dokumentacja firmy Microsoft"
description: "W tym artykule omówiono popularnych pytania dotyczące usługi Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 5cdc4bcd-b4fe-48c7-8be1-1db39bd9c078
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/22/2017
ms.author: raynew
ms.openlocfilehash: 6d0bd2475466e5745e1f084bd2267d954d624ebd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-site-recovery-frequently-asked-questions-faq"></a>Azure Site Recovery: często zadawane pytania (FAQ)
Ten artykuł zawiera często zadawane pytania dotyczące usługi Azure Site Recovery. Jeśli masz pytania po przeczytaniu tego artykułu, opublikuj je na hello [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/Forums/azure/home?forum=hypervrecovmgr).

## <a name="general"></a>Ogólne
### <a name="what-does-site-recovery-do"></a>Do czego służy usługa Site Recovery?
Usługi Site Recovery przyczynia się tooyour ciągłość oraz strategia odzyskiwania (BCDR), poprzez organizowanie i automatyzowanie replikacji maszyn wirtualnych Azure między regionami, lokalnych maszyn wirtualnych i serwerów fizycznych tooAzure i tooa maszyny lokalne dodatkowego centrum danych. [Dowiedz się więcej](site-recovery-overview.md).

### <a name="what-can-site-recovery-protect"></a>Co może chronić Usługa Site Recovery?
* **Maszyny wirtualne platformy Azure**: Usługa Site Recovery może replikować dowolne obciążenia uruchomione na obsługiwanej maszynie Wirtualnej Azure
* **Maszyny wirtualne funkcji Hyper-V**: Usługa Site Recovery może chronić dowolne obciążenia uruchomione na maszynie Wirtualnej funkcji Hyper-V.
* **Serwery fizyczne**: Usługa Site Recovery może chronić serwery fizyczne z systemem Windows lub Linux.
* **Maszyny wirtualne VMware**: Usługa Site Recovery może chronić dowolne obciążenia uruchomione na maszynie wirtualnej VMware.

### <a name="does-site-recovery-support-hello-azure-resource-manager-model"></a>Usługa Site Recovery obsługuje modelu usługi Azure Resource Manager hello?
Usługa Site Recovery jest dostępna w hello portalu Azure z obsługą dla Menedżera zasobów. Usługa Site Recovery obsługuje starszych wdrożeń w hello klasycznego portalu Azure. Nie można utworzyć nowego magazynu w portalu klasycznym hello i nowe funkcje nie są obsługiwane.

### <a name="can-i-replicate-azure-vms"></a>Czy można replikować maszyny wirtualne Azure?
Tak, obsługiwanych maszynach wirtualnych platformy Azure można replikować między regiony platformy Azure. [Dowiedz się więcej](site-recovery-azure-to-azure.md).

### <a name="what-do-i-need-in-hyper-v-tooorchestrate-replication-with-site-recovery"></a>Czego potrzebuję w funkcji Hyper-V tooorchestrate replikacji z usługą Site Recovery?
Serwer hosta funkcji Hyper-V hello potrzebnych zależy od scenariusza wdrażania hello. Wyewidencjonuj hello wymagania wstępne funkcji Hyper-V w:

* [Replikowanie maszyn wirtualnych funkcji Hyper-V (bez VMM) tooAzure](site-recovery-hyper-v-site-to-azure.md)
* [Replikowanie maszyn wirtualnych funkcji Hyper-V (w programie VMM) tooAzure](site-recovery-vmm-to-azure.md)
* [Replikowanie maszyn wirtualnych funkcji Hyper-V tooa dodatkowego centrum danych](site-recovery-vmm-to-vmm.md)
* Jeśli replikujesz tooa pomocniczego centrum danych, przeczytaj o [obsługiwane systemy operacyjne gościa dla maszyn wirtualnych funkcji Hyper-V](https://technet.microsoft.com/library/mt126277.aspx).
* Jeśli replikujesz tooAzure Usługa Site Recovery obsługuje wszystkie hello systemów operacyjnych gościa, które są [obsługiwany przez platformę Azure](https://technet.microsoft.com/library/cc794868%28v=ws.10%29.aspx).

### <a name="can-i-protect-vms-when-hyper-v-is-running-on-a-client-operating-system"></a>Maszyny wirtualne można chronić po funkcji Hyper-V działa w systemie operacyjnym klienta?
Nie. Maszyny wirtualne muszą znajdować się na serwerze hosta funkcji Hyper-V, który jest uruchomiony na serwerze z obsługiwanym systemem Windows. Jeśli potrzebujesz tooprotect komputer kliencki, możesz replikować go jako maszynę fizyczną za[Azure](site-recovery-vmware-to-azure.md) lub [dodatkowego centrum danych](site-recovery-vmware-to-vmware.md).

### <a name="what-workloads-can-i-protect-with-site-recovery"></a>Jakie obciążenia mogę chronić za pomocą usługi Site Recovery?
Można użyć usługi Site Recovery tooprotect większość obciążenia uruchomione na obsługiwanej maszynie Wirtualnej lub serwerze fizycznym. Site Recovery zapewnia wsparcie dla replikacji obsługującej, dzięki czemu aplikacje mogą być odzyskiwane tooan inteligentnego stanu. Integruje się z aplikacjami firmy Microsoft, takich jak SharePoint, Exchange, Dynamics, SQL Server i usługi Active Directory i ściśle współpracuje z wiodącymi dostawcami oprogramowania, w tym Oracle, SAP, IBM i Red Hat. [Dowiedz się więcej](site-recovery-workload.md) o ochronie obciążeń.

### <a name="do-hyper-v-hosts-need-toobe-in-vmm-clouds"></a>Czy hosty funkcji Hyper-V muszą toobe w chmurach programu VMM?
Jeśli chcesz tooreplicate tooa dodatkowego centrum danych, a następnie maszyn wirtualnych funkcji Hyper-V muszą znajdować się na funkcji Hyper-V obsługuje serwery znajdujące się w chmurze VMM. Jeśli chcesz tooreplicate tooAzure można replikować maszyny wirtualne na serwerach hostów funkcji Hyper-V z chmur VMM lub bez. [Dowiedz się więcej](site-recovery-hyper-v-site-to-azure.md).

### <a name="can-i-deploy-site-recovery-with-vmm-if-i-only-have-one-vmm-server"></a>Czy mogę wdrożyć usługę Site Recovery z programem VMM, jeśli mam tylko jeden serwer VMM?

Tak. Możesz replikować maszyny wirtualne na serwerach funkcji Hyper-V w tooAzure chmury VMM hello lub replikować je między chmurami VMM na powitania sam serwer. Lokalnymi tooon lokalnej replikacji zalecamy posiadanie serwera VMM w obu lokacjach podstawowych i pomocniczych hello.  

### <a name="what-physical-servers-can-i-protect"></a>Jakie serwery fizyczne mogę chronić?
Można replikować fizycznych serwerów z systemem Windows i Linux tooAzure lub tooa lokacji dodatkowej. [Dowiedz się więcej o](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) wymagania dotyczące systemu operacyjnego.  Witaj, te same wymagania dotyczą czy replikujesz tooAzure serwerów fizycznych lub tooa lokacji dodatkowej.


Należy pamiętać, że serwery fizyczne będzie uruchamiany jako maszyn wirtualnych na platformie Azure, jeśli spadnie do serwera lokalnego. Tooan powrotu po awarii w lokalnym serwerze fizycznym nie jest obecnie obsługiwany. Dla komputera chronionego jak fizyczną można tylko powrotu po awarii tooa maszyny wirtualnej VMware.

### <a name="what-vmware-vms-can-i-protect"></a>Jakie maszyny wirtualne VMware mogę chronić?

maszyny wirtualne VMware tooprotect należy vSphere hypervisor i maszyny wirtualne z uruchomionymi narzędziami VMware. Zalecane jest również, czy masz vCenter server toomanage hello funkcjami hypervisor VMware. [Dowiedz się więcej](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) o dokładnych wymaganiach dotyczących replikacji serwerów VMware i maszyn wirtualnych tooAzure lub tooa lokacji dodatkowej.


### <a name="can-i-manage-disaster-recovery-for-my-branch-offices-with-site-recovery"></a>Czy mogę zarządzać odzyskiwaniem po awarii dla oddziałów firmy przy użyciu usługi Site Recovery?
Tak. Gdy używasz usługi Site Recovery tooorchestrate replikacji i trybu failover w biurach oddziałów, uzyskasz ujednoliconego aranżacji i widoku wszystkie obciążenia oddziałów w centralnej lokalizacji. Można łatwo uruchomić tryb failover i administrować odzyskiwania po awarii wszystkich oddziałów z siedziby, bez konieczności przechodzenia hello gałęzi.

## <a name="pricing"></a>Cennik

### <a name="what-charges-do-i-incur-while-using-azure-site-recovery"></a>Co opłaty są naliczane podczas korzystania z usługi Azure Site Recovery?
Gdy używasz usługi Site Recovery wiąże się z opłatami hello licencji usługi Site Recovery, magazynu Azure, transakcji magazynu i transfer danych wychodzących. [Dowiedz się więcej](https://azure.microsoft.com/pricing/details/site-recovery).

Licencja usługi Site Recovery Hello jest dla każdego wystąpienia chronionych, w przypadku wystąpienia maszyny Wirtualnej lub serwerze fizycznym.

- Jeśli dysk maszyny Wirtualnej są replikowane tooa konta standard storage, hello opłat magazynu platformy Azure jest wykorzystania magazynu hello. Na przykład jeśli rozmiar dysku źródłowego hello jest 1 TB i 400 GB jest używany, Usługa Site Recovery tworzy 1 TB wirtualnego dysku twardego na platformie Azure, ale magazynu hello naliczona opłata jest 400 GB (oraz hello ilość miejsca używanego dla dzienników replikacji).
- Jeśli dysk maszyny Wirtualnej są replikowane konta magazynu premium tooa, hello opłat magazynu platformy Azure jest dla rozmiaru magazynu hello zainicjowano obsługę administracyjną, zaokrąglone dla hello najbliższej opcji dysku magazynu premium. Na przykład jeśli rozmiar dysku źródłowego hello jest 50 GB, Usługa Site Recovery tworzy dysk 50 GB na platformie Azure oraz Azure mapuje ten toohello najbliższej dysku magazynu premium (P10).  Koszty są obliczane na P10, a nie na rozmiar dysku hello 50 GB.  [Dowiedz się więcej](https://aka.ms/premium-storage-pricing).  Jeśli używasz magazyn w warstwie premium, konto magazynu w warstwie standardowa dla rejestrowania replikacji jest również wymagany i hello ilość miejsca magazynu w warstwie standardowa dla dzienników również jest on rozliczany.
- Dyski nie są tworzone do testowania trybu failover lub awarię. Stan replikacji hello, magazynu opłaty kategorii hello "stronicowych obiektów blob i dysku" zgodnie z harmonogramem hello [Kalkulator cen magazynu](https://azure.microsoft.com/en-in/pricing/calculator/) poniesione. Opłaty te są oparte na powitania typ magazynu premium/standard i hello nadmiarowości danych wpisz - LRS, GRS, RA-GRS itp.
- Toouse opcja hello zarządzane dyski w tryb failover zaznaczenie, [opłat za dysków zarządzanych](https://azure.microsoft.com/en-in/pricing/details/managed-disks/) po przejściu w tryb failover trybu failover i testowanie. Zarządzane dyski, które opłaty nie są stosowane podczas replikacji.
- Jeśli nie wybrano hello opcja toouse zarządzane dyski w tryb failover, magazynu opłaty kategorii hello "stronicowych obiektów blob i dysku" zgodnie z harmonogramem hello [Kalkulator cen magazynu](https://azure.microsoft.com/en-in/pricing/calculator/) poniesionych po pracy awaryjnej. Opłaty te są oparte na powitania typ magazynu premium/standard i hello nadmiarowości danych wpisz - LRS, GRS, RA-GRS itp.
- Transakcje magazynu są naliczane podczas replikacji stabilnego i regularnych operacji maszyny Wirtualnej po przejściu w tryb failover i testowania trybu failover. Ale opłaty te są bez znaczenia.

Podczas testowania trybu failover, w których zostaną zastosowane koszty transakcji maszyny Wirtualnej, magazynowania, transfer danych wychodzących i magazynu hello są również poniesione koszty.



## <a name="security"></a>Bezpieczeństwo
### <a name="is-replication-data-sent-toohello-site-recovery-service"></a>Dane replikacji są wysyłane toohello usługi Site Recovery?
Nie, Usługa Site Recovery nie przechwytuje replikowanych danych, nie ma żadnych informacji o co działa na maszynach wirtualnych lub serwerach fizycznych.
Dane replikacji są wymieniane między lokalnymi hostami funkcji Hyper-V, funkcjami hypervisor VMware lub serwerami fizycznymi i usługą Azure Storage lub lokacją dodatkową. Usługa Site Recovery ma toointercept nie możliwości danych. Tylko metadane hello potrzebne tooorchestrate replikacji i trybu failover są wysyłane toohello usługi Site Recovery.  

Usługa Site Recovery jest ISO 27001: 2013, 27018, HIPAA, DPA i w procesie hello ocen SOC2 i FedRAMP JAB.

### <a name="for-compliance-reasons-even-our-on-premises-metadata-must-remain-within-hello-same-geographic-region-can-site-recovery-help-us"></a>Ze względu na zgodność nawet naszych lokalnych metadanych muszą pozostać w hello tym samym regionie geograficznym. Usługa Site Recovery pomaga nam?
Tak. Po utworzeniu magazynu usługi Site Recovery w regionie, Upewniamy się, że wszystkie metadane, które firma Microsoft muszą tooenable i organizowania replikacji i trybu failover pozostaje w tym regionie obiektu geograficznego granic.

### <a name="does-site-recovery-encrypt-replication"></a>Czy usługa Site Recovery szyfruje replikację?
Dla maszyn wirtualnych i serwerów fizycznych replikacji między lokalnymi witryn szyfrowania podczas przesyłania danych jest obsługiwane. Dla maszyn wirtualnych i serwerów fizycznych replikowanie tooAzure, zarówno szyfrowanie podczas przesyłania danych i [szyfrowania na rest (na platformie Azure)](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption) są obsługiwane.

## <a name="replication"></a>Replikacja

### <a name="can-i-replicate-over-a-site-to-site-vpn-tooazure"></a>Można replikować za pośrednictwem tooAzure sieci VPN typu lokacja lokacja?
Usługa Azure Site Recovery replikuje dane tooan kontem magazynu platformy Azure, za pośrednictwem publicznego punktu końcowego. Replikacja nie jest za pośrednictwem sieci VPN lokacja lokacja. Można utworzyć sieci VPN lokacja lokacja z sieci wirtualnej platformy Azure. To nie zakłóca replikacji usługi Site Recovery.

### <a name="can-i-use-expressroute-tooreplicate-virtual-machines-tooazure"></a>Można użyć tooAzure maszyn wirtualnych tooreplicate ExpressRoute?
Tak, ExpressRoute mogą być używane tooreplicate tooAzure maszyn wirtualnych. Usługa Azure Site Recovery replikuje dane tooan konta magazynu Azure za pośrednictwem publicznego punktu końcowego. Należy tooset się [publicznej komunikacji równorzędnej](../expressroute/expressroute-circuit-peerings.md#public-peering) toouse ExpressRoute replikacji usługi Site Recovery. Po hello maszyny wirtualne zostały awaryjnie tooan sieci wirtualnej platformy Azure będą dostępne za pomocą hello [prywatnej komunikacji równorzędnej](../expressroute/expressroute-circuit-peerings.md#private-peering) Instalatorowi hello sieci wirtualnej platformy Azure.

### <a name="are-there-any-prerequisites-for-replicating-virtual-machines-tooazure"></a>Czy istnieją wymagania wstępne związane z replikowanie maszyn wirtualnych tooAzure?
Maszyny wirtualne mają tooreplicate tooAzure powinny być zgodne z [wymagania dotyczące usługi Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).

Twoje konto użytkownika systemu Azure wymaga toohave niektórych [uprawnienia](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable replikację nowego tooAzure maszyny wirtualnej.

### <a name="can-i-replicate-hyper-v-generation-2-virtual-machines-tooazure"></a>Czy można replikować tooAzure 2 maszyn wirtualnych generacji w funkcji Hyper-V?
Tak. Usługa Site Recovery konwertuje z generacji 2 toogeneration 1 podczas pracy awaryjnej. W przypadku powrotu po awarii maszyna hello jest przekonwertowanego toogeneration wstecz 2. [Dowiedz się więcej](http://azure.microsoft.com/blog/2015/04/28/disaster-recovery-to-azure-enhanced-and-were-listening/).

### <a name="if-i-replicate-tooazure-how-do-i-pay-for-azure-vms"></a>W przypadku replikacji tooAzure, jak będę płacić za maszyny wirtualne Azure?
Podczas regularnej replikacji dane są replikowane toogeo nadmiarowego magazynu Azure i nie ma potrzeby toopay opłaty maszyny wirtualne IaaS platformy Azure, zapewniając znaczących korzyści. Po uruchomieniu tooAzure trybu failover, Usługa Site Recovery automatycznie tworzy maszyny wirtualne IaaS platformy Azure, a po tym zostaną naliczone hello zasobów obliczeniowych, które zostaną zużyte na platformie Azure.

### <a name="can-i-automate-site-recovery-scenarios-with-an-sdk"></a>Czy można zautomatyzować scenariuszy odzyskiwania lokacji przy użyciu zestawu SDK?
Tak. Można automatyzować przepływy pracy usługi Site Recovery przy użyciu hello interfejsu API Rest, programu PowerShell lub hello Azure SDK. Aktualnie obsługiwanych scenariuszach wdrażania usługi Site Recovery przy użyciu programu PowerShell:

* [Replikowanie maszyn wirtualnych funkcji Hyper-V w VMMs tooAzure chmur programu PowerShell Menedżera zasobów](site-recovery-vmm-to-azure-powershell-resource-manager.md)
* [Replikowanie maszyn wirtualnych funkcji Hyper-V bez tooAzure VMM PowerShell Resource Manager](site-recovery-deploy-with-powershell-resource-manager.md)

### <a name="if-i-replicate-tooazure-what-kind-of-storage-account-do-i-need"></a>W przypadku replikacji tooAzure jakiego konta magazynu potrzebuję?
* **Klasyczny portal Azure**: w przypadku instalowania usługi Site Recovery w hello klasycznego portalu Azure, konieczne będzie [konta standardowe magazynu geograficznie nadmiarowego](../storage/common/storage-redundancy.md#geo-redundant-storage). Usługa Premium Storage nie jest obecnie obsługiwana. Witaj, konto musi być w hello tym samym regionie co magazyn usługi Site Recovery hello.
* **Azure portal**: w przypadku instalowania usługi Site Recovery w portalu Azure hello, potrzebujesz konta magazynu LRS lub GRS. Zalecamy użycie konta GRS, dzięki czemu dane są odporne w przypadku regionalnej awarii lub jeśli nie można odzyskać regionu podstawowego hello. Witaj, konto musi być w hello magazyn usług odzyskiwania i tym samym regionie co hello. Magazyn w warstwie Premium jest teraz obsługiwana dla maszyny Wirtualnej VMware, maszyna wirtualna funkcji Hyper-V i replikacji serwera fizycznego, podczas wdrażania usługi Site Recovery w portalu Azure hello.

### <a name="how-often-can-i-replicate-data"></a>Jak często mogę replikować dane?
* **Funkcja Hyper-V:** maszyn wirtualnych funkcji Hyper-V mogą być replikowane co 30 sekund (z wyjątkiem magazyn w warstwie premium), 5 minut lub 15 minut. Jeśli po skonfigurowaniu replikacji sieci SAN replikacja jest synchroniczne.
* **Maszyny wirtualne VMware i serwery fizyczne:** częstotliwość replikacji nie jest tutaj istotna. Replikacja jest ciągły.

### <a name="can-i-extend-replication-from-existing-recovery-site-tooanother-tertiary-site"></a>Czy mogę rozszerzyć replikację z istniejącej witryny tooanother trzeciorzędny lokacji odzyskiwania?
Replikacja rozszerzona lub łańcuchowa nie jest obsługiwana. Żądanie tę funkcję w [forum opinii](http://feedback.azure.com/forums/256299-site-recovery/suggestions/6097959-support-for-exisiting-extended-replication).

### <a name="can-i-do-an-offline-replication-hello-first-time-i-replicate-tooazure"></a>Możliwości replikacji w trybie offline powitania po raz pierwszy replikacji tooAzure?
Ta funkcja nie jest obsługiwana. Żądanie tę funkcję w hello [forum opinii](http://feedback.azure.com/forums/256299-site-recovery/suggestions/6227386-support-for-offline-replication-data-transfer-from).

### <a name="can-i-exclude-specific-disks-from-replication"></a>Czy z replikacji można wykluczyć określone dyski?
Jest to obsługiwane, gdy jesteś [replikowanie maszyn wirtualnych VMware i maszyn wirtualnych funkcji Hyper-V](site-recovery-exclude-disk.md) tooAzure przy użyciu hello portalu Azure.

### <a name="can-i-replicate-virtual-machines-with-dynamic-disks"></a>Czy można replikować maszyny wirtualne z dyskami dynamicznymi?
Dyski dynamiczne są obsługiwane w przypadku replikacji maszyn wirtualnych funkcji Hyper-V. Są one również obsługiwane podczas replikowania maszyn wirtualnych VMware i maszyn fizycznych tooAzure. dysk systemu operacyjnego Hello musi być dyskiem podstawowym.

### <a name="can-i-add-a-new-machine-tooan-existing-replication-group"></a>Można dodać nowego tooan istniejącą grupę replikacji maszyny?
Dodawanie nowej grupy replikacji tooexisting maszyny jest obsługiwane. toodo tak, wybierz grupę replikacji hello (za pomocą bloku "Zreplikowane elementy") i kliknij prawym przyciskiem myszy wybierz menu kontekstowe w grupie replikacji hello i wybierz odpowiednią opcję hello.

![Dodaj grupę tooreplication](./media/site-recovery-faq/add-server-replication-group.png)

### <a name="can-i-throttle-bandwidth-allotted-for-hyper-v-replication-traffic"></a>Czy mogę ograniczyć przepustowość przydzieloną dla ruchu replikacji funkcji Hyper-V?
Tak. Możesz przeczytać więcej na temat ograniczania przepustowości w hello wdrażania:

* [Planowanie wydajności dla replikowanie maszyn wirtualnych VMware oraz serwerach fizycznych](site-recovery-plan-capacity-vmware.md)
* [Planowanie wydajności dla replikowanie maszyn wirtualnych funkcji Hyper-V w chmurach programu VMM](site-recovery-vmm-to-azure.md#capacity-planning)
* [Planowanie wydajności dla replikowanie maszyn wirtualnych funkcji Hyper-V bez programu VMM](site-recovery-hyper-v-site-to-azure.md)

## <a name="failover"></a>Tryb failover
### <a name="if-im-failing-over-tooazure-how-do-i-access-hello-azure-virtual-machines-after-failover"></a>Jeśli używam awaryjne tooAzure, jak uzyskać dostęp hello Azure maszyn wirtualnych po pracy awaryjnej?
Można uzyskać dostępu do hello maszynach wirtualnych platformy Azure za pośrednictwem bezpiecznego połączenia internetowego, za pośrednictwem sieci VPN lokacja lokacja lub za pośrednictwem usługi Azure ExpressRoute. Liczba elementów w kolejności tooconnect tooprepare jest potrzebny. [Dowiedz się więcej](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover)


### <a name="if-i-fail-over-tooazure-how-does-azure-make-sure-my-data-is-resilient"></a>Jeśli I pracy awaryjnej tooAzure jak Azure upewnij się, że moje dane są odporne?
Platforma Azure została zaprojektowana z myślą o odporności danych. Usługa Site Recovery jest już zaprojektowana z myślą o pracy awaryjnej tooa pomocniczego centrum danych Azure, zgodnie z warunkami umowy SLA platformy Azure, jeśli potrzebujesz hello powstaje powitalne. Jeśli tak się stanie, Upewniamy metadane i magazyny pozostają w hello tym samym regionie geograficznym, który został wybrany dla magazynu.  

### <a name="if-im-replicating-between-two-datacenters-what-happens-if-my-primary-datacenter-experiences-an-unexpected-outage"></a>Jeśli Przeprowadzam replikację między dwoma centrami danych co się stanie w przypadku awarii napotka Moje podstawowego centrum danych?
Możesz wyzwolić nieplanowany tryb failover z lokacji dodatkowej hello. Usługa Site Recovery nie wymaga łączności z hello lokacji głównej tooperform hello w tryb failover.

### <a name="is-failover-automatic"></a>Czy tryb failover jest automatyczny?
Tryb failover nie jest automatyczny. Zainicjuj tryb failover z jednym kliknięciem w portalu hello, lub można użyć [PowerShell odzyskiwania lokacji](/powershell/module/azurerm.siterecovery) tootrigger trybu failover. Niepowodzenie wstecz jest proste działania w portalu usługi Site Recovery hello.

tooautomate, których można użyć lokalnego narzędzia Orchestrator lub programu Operations Manager toodetect awarii maszyny wirtualnej, a następnie użyć trybu failover hello wyzwalacza hello zestawu SDK.

* [Dowiedz się więcej](site-recovery-create-recovery-plans.md) o planach odzyskiwania.
* [Dowiedz się więcej](site-recovery-failover.md) o pracy awaryjnej.
* [Dowiedz się więcej](site-recovery-failback-azure-to-vmware.md) o niepowodzeniu kopię maszyn wirtualnych VMware oraz serwerach fizycznych

### <a name="if-my-on-premises-host-is-not-responding-or-crashed-can-i-failover-back-tooa-different-host"></a>Jeśli host Moje lokalnymi nie jest nieodpowiadający lub awaria, czy można trybu failover wstecz tooa innego hosta?
Tak, można użyć hello alternatywną lokalizację odzyskiwania toofailback tooa inny host z platformy Azure. Dowiedz się więcej o opcjach hello hello poniższych łączy dla maszyn wirtualnych VMware i funkcji Hyper-v.

* [W przypadku maszyn wirtualnych VMware](site-recovery-how-to-failback-azure-to-vmware.md#fail-back-to-the-original-or-alternate-location)
* [W przypadku maszyn wirtualnych funkcji Hyper-v](site-recovery-failback-from-azure-to-hyper-v.md#failback-to-an-alternate-location)

## <a name="service-providers"></a>Dostawcy usług
### <a name="im-a-service-provider-does-site-recovery-work-for-dedicated-and-shared-infrastructure-models"></a>Jestem dostawcą usług. Usługa Site Recovery działa dla modeli opartych na infrastrukturze dedykowanej i współdzielonej?
Tak. Usługa Site Recovery obsługuje modele oparte na infrastrukturze dedykowanej i współdzielonej.

### <a name="for-a-service-provider-is-hello-identity-of-my-tenant-shared-with-hello-site-recovery-service"></a>Dla dostawcy usług jest hello tożsamość mojej dzierżawy jest udostępniana usłudze Site Recovery hello?
Nie. Tożsamość dzierżawcy pozostaje anonimowy. Twoje dzierżawy nie wymagają portalu usługi Site Recovery toohello dostępu. Tylko hello administrator dostawcy usług współdziała z hello portalu.

### <a name="will-tenant-application-data-ever-go-tooazure"></a>Dane aplikacji dzierżawy kiedykolwiek przejdzie tooAzure?
Podczas replikacji między lokacjami należącymi do dostawcy usług, dane aplikacji nigdy nie trafiają tooAzure. Dane są szyfrowane podczas przesyłania i replikowane bezpośrednio między lokacjami dostawcy usług hello.

Jeśli replikujesz tooAzure dane aplikacji są wysyłane tooAzure magazynu, ale nie toohello usługi Site Recovery. Dane są szyfrowane podczas przesyłania i pozostają zaszyfrowane na platformie Azure.

### <a name="will-my-tenants-receive-a-bill-for-any-azure-services"></a>Czy moje dzierżawy otrzymają rachunek za jakiekolwiek usługi platformy Azure?
Nie. Relacja rozliczeń platformy Azure jest bezpośrednio z dostawcą usług hello. Dostawcy usług są odpowiedzialni za generowanie konkretnych rachunków dla swoich dzierżaw.

### <a name="if-im-replicating-tooazure-do-we-need-toorun-virtual-machines-in-azure-at-all-times"></a>Jeśli Przeprowadzam replikację tooAzure, potrzebujemy toorun maszyn wirtualnych na platformie Azure przez cały czas?
Nie, dane są replikowane tooan kontem magazynu platformy Azure w ramach subskrypcji. Podczas testowego (test odzyskiwania po awarii) lub rzeczywistego uruchamiania trybu failover usługa Site Recovery automatycznie tworzy maszyny wirtualne w ramach subskrypcji.

### <a name="do-you-ensure-tenant-level-isolation-when-i-replicate-tooazure"></a>Zapewnić izolacja na poziomie dzierżawy podczas replikacji tooAzure?
Tak.

### <a name="what-platforms-do-you-currently-support"></a>Jakie platformy są obecnie obsługiwane?
Firma Microsoft obsługuje pakietu Azure Pack, systemie Cloud Platform System i wdrażania (2012 i nowsze) opartego na programie System Center. [Dowiedz się więcej](https://technet.microsoft.com/library/dn850370.aspx) o integracji pakietu Azure Pack i Site Recovery.

### <a name="do-you-support-single-azure-pack-and-single-vmm-server-deployments"></a>Czy są obsługiwane wdrożenia oparte na jednym pakiecie Azure Pack i jednym serwerze VMM?
Tak, można replikować tooAzure maszyn wirtualnych funkcji Hyper-V, lub między lokacjami dostawcy usług.  Należy pamiętać, że Jeśli replikujesz między lokacjami dostawcy usług integracji elementów runbook platformy Azure jest niedostępna.

## <a name="next-steps"></a>Następne kroki
* Witaj odczytu [omówieniem usługi Site Recovery](site-recovery-overview.md)
* Dowiedz się więcej o [architekturze usługi Site Recovery](site-recovery-components.md)  
