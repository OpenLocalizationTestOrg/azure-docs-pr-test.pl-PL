---
title: "aaaPrerequisites dla tooAzure replikacji przy użyciu usługi Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o wymaganiach wstępnych hello replikowania maszyn wirtualnych i maszyn fizycznych tooAzure za pomocą usługi Azure Site Recovery hello."
services: site-recovery
documentationcenter: 
author: rajani-janaki-ram
manager: jwhit
editor: tysonn
ms.assetid: e24eea6c-50a7-4cd5-aab4-2c5c4d72ee2d
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/23/2017
ms.author: rajanaki
ms.openlocfilehash: 0e32ab7cd7c65a3f67ffa2f2c15af189c15b6f49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
#  <a name="prerequisites-for-replication-from-on-premises-tooazure-by-using-site-recovery"></a>Wymagania wstępne dotyczące replikacji z lokalnych tooAzure przy użyciu usługi Site Recovery

> [!div class="op_single_selector"]
> * [Replikacja między Azure tooAzure](site-recovery-azure-to-azure-prereq.md)
> * [Replikacja między lokalnymi tooAzure](site-recovery-prereq.md)

Usługa Azure Site Recovery może pomóc obsługuje ciągłości i odzyskiwaniem po awarii (BCDR) odzyskiwania strategią biznesową poprzez organizowanie replikacji maszyny wirtualnej platformy Azure (VM) tooanother region platformy Azure. Odzyskiwanie lokacji są replikowane, na lokalnych serwerów fizycznych i maszyn wirtualnych toohello chmury (Azure) lub tooa dodatkowego centrum danych. W przypadku wystąpienia awarii w lokalizacji głównej, można przełączyć tooa dodatkowej lokalizacji tookeep aplikacji i obciążeń dostępne. Po powrocie z lokalizacji podstawowej hello operacji toonormal może zakończyć się niepowodzeniem wstecz tooyour lokalizacji głównej. Aby uzyskać więcej informacji na temat odzyskiwania lokacji, zobacz [co to jest usługa Site Recovery?](site-recovery-overview.md).

W tym artykule firma Microsoft podsumowanie jakiegoś hello rozpoczyna replikację usługi Site Recovery z tooAzure komputera lokalnego.

Możesz zamieścić wszelkie komentarze u dołu hello hello artykułu. Również można zadawać pytania techniczne w hello [forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="azure-requirements"></a>Wymagania systemu Azure

**Wymaganie** | **Szczegóły**
--- | ---
**Konto platformy Azure** | A [konta Microsoft Azure](http://azure.microsoft.com/). Możesz rozpocząć od [bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).
**Usługa Site Recovery** | Aby uzyskać więcej informacji na temat cen dla hello usługi Azure Site Recovery, zobacz [cenach usługi Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/). |
**Azure Storage** | Należy toostore replikowane dane konta usługi Azure Storage. Konto magazynu Hello musi znajdować się w hello magazyn usług odzyskiwania Azure i tym samym regionie co hello. Maszyny wirtualne platformy Azure są tworzone podczas pracy awaryjnej.<br/><br/> W zależności od modelu zasobu hello ma toouse dla trybu failover maszyny Wirtualnej platformy Azure, można skonfigurować konto, za pomocą hello [modelu wdrażania usługi Azure Resource Manager](../storage/common/storage-create-storage-account.md) lub hello [klasycznego modelu wdrażania](../storage/common/storage-create-storage-account.md).<br/><br/>Możesz używać [magazynu geograficznie nadmiarowego](../storage/common/storage-redundancy.md#geo-redundant-storage) lub magazynu lokalnie nadmiarowego. Zalecamy magazyn geograficznie nadmiarowy. Z magazynu geograficznie nadmiarowego dane są odporne w przypadku regionalnej awarii lub jeśli nie można odzyskać regionu podstawowego hello.<br/><br/> Można używać konta standardowe magazynu Azure, lub skorzystać z usługi Azure Premium Storage. [Magazyn w warstwie Premium](https://docs.microsoft.com/azure/storage/storage-premium-storage) zazwyczaj jest używana w przypadku maszyn wirtualnych, które wymagają wysoką wydajność We/Wy i małe opóźnienia. Z magazyn w warstwie premium maszyna wirtualna może obsługiwać/O wykonujących obciążeń. Jeśli używasz usługi Premium Storage do przechowywania replikowanych danych, potrzebujesz też standardowego konta magazynu. Konta standard storage przechowuje dzienników replikacji, które przechwytują zachodzące zmiany lokalne tooon danych.<br/><br/>
**Ograniczenia magazynu** | Nie można przenieść konta magazynu, używane w lokacji odzyskiwania tooa innej grupie zasobów lub Przenieś użycia tooor z innej subskrypcji.<br/><br/> Obecnie usługa replikacji konta magazynu toopremium w Indie środkowe i Indie Południowe nie jest dostępna.
**Sieć platformy Azure** | Potrzebujesz sieci platformy Azure, maszyny wirtualne Azure toowhich Połącz po pracy awaryjnej. Hello Azure sieć musi znajdować się w hello magazyn usług odzyskiwania i tym samym regionie co hello.<br/><br/> W hello portalu Azure, można utworzyć sieci platformy Azure przy użyciu hello [modelu wdrażania usługi Resource Manager](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) lub hello [klasycznego modelu wdrażania](../virtual-network/virtual-networks-create-vnet-classic-pportal.md).<br/><br/> Jeśli replikujesz z tooAzure System Center Virtual Machine Manager (VMM), należy skonfigurować mapowanie sieci między sieciami maszyn wirtualnych VMM i sieci platformy Azure. Dzięki temu, że maszyny wirtualne Azure łączenia sieci tooappropriate po pracy awaryjnej.
**Ograniczenia dotyczące sieci** | Nie można przenieść kont sieci, używane w lokacji odzyskiwania tooa innej grupie zasobów lub Przenieś użycia tooor z innej subskrypcji.
**Mapowanie sieci** | Jeśli replikujesz maszyny wirtualne funkcji Hyper-V firmy Microsoft w chmurach programu VMM, należy skonfigurować mapowanie sieci. Dzięki temu, że maszynach wirtualnych platformy Azure są tworzone po pracy awaryjnej, połączyć tooappropriate sieci.

> [!NOTE]
> Witaj poniższych sekcjach opisano wymagania wstępne hello różne składniki powitania klienta środowiska. Aby uzyskać więcej informacji na temat obsługi dla określonej konfiguracji, zobacz hello [macierz obsługi](site-recovery-support-matrix.md).
>

## <a name="disaster-recovery-of-vmware-vms-or-physical-windows-or-linux-servers-tooazure"></a>Odzyskiwanie po awarii maszyn wirtualnych VMware lub fizycznych tooAzure serwerów z systemem Windows lub Linux
Witaj następujące składniki są wymagane podczas odzyskiwania po awarii maszyn wirtualnych VMware lub serwerach fizycznych systemu Windows lub Linux. Ponadto są toohello takich, które opisano w [wymagania dotyczące usługi Azure](#azure-requirements).


### <a name="configuration-server-or-additional-process-server"></a>Konfiguracja serwera lub serwera dodatkowych procesów

Konfigurowanie komputera lokalnego jako hello konfiguracji serwera tooorchestrate komunikacji między hello lokalną lokacją a platformą Azure. Witaj na lokalnej maszynie zarządza także replikacji danych. <br/></br>

*   **VMware vCenter lub vSphere wymagania wstępne dotyczące hosta**

    | **Składnik** | **Wymagania** |
    | --- | --- |
    | **vSphere** | Musi mieć co najmniej jeden VMware funkcji hypervisor vSphere..<br/><br/>Funkcji hypervisor musi być uruchomiona vSphere w wersji 6.0, 5.5 lub 5.1 z hello najnowsze aktualizacje.<br/><br/>Zaleca się, że hostami vSphere i serwery vCenter się znajdować w hello sam sieciowe jako serwera przetwarzania hello. Jeśli nie skonfigurowano serwera dedykowanego procesu jest sieci hello, w którym znajduje się serwer konfiguracji hello. |
    | **vCenter** | Firma Microsoft zaleca hostach vSphere można wdrożyć toomanage VMware vCenter server. Musi ona być uruchomiona vCenter w wersji 6.0 lub 5.5, z hello najnowsze aktualizacje.<br/><br/>**Ograniczenie**: Usługa Site Recovery nie obsługuje replikacji między wystąpieniami vCenter vMotion. Magazyn usługi rejestracji urządzeń i Storage vMotion również nie są obsługiwane w głównym celu maszyny Wirtualnej po zakończeniu operacji ponownej ochrony.||

* **Wymagania wstępne dotyczące replikowane maszyny**

    | **Składnik** | **Wymagania** |
    | --- | --- |
    | **Maszyny lokalne** (maszyny wirtualne VMware) | Replikowane maszyny wirtualne muszą być narzędzia VMware zainstalowany i uruchomiony.<br/><br/> Maszyny wirtualne muszą spełniać [wymagania wstępne platformy Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) do tworzenia maszyny Wirtualnej platformy Azure.<br/><br/>Pojemność dysku na każdym chronionym komputerze nie może być więcej niż 1,023 GB. <br/><br/>Minimalna 2 GB wolnego miejsca na dysku instalacyjnym hello jest wymagany do instalacji składnika.<br/><br/>Jeśli chcesz tooenable spójności wielu maszyn wirtualnych, należy otworzyć port 20004 zaporę lokalne powitania maszyny Wirtualnej.<br/><br/>Nazwy komputerów musi wynosić od 1 do 63 znaków (należy użyć litery, cyfry i łączniki). Witaj nazwa musi zaczynać się literą lub cyfrą i kończyć literą lub cyfrą. <br/><br/>Po włączeniu replikacji dla maszyny, można zmodyfikować hello nazwa platformy Azure.<br/><br/> |
    | **Komputery z systemem Windows** (fizycznej lub VMware) | Witaj maszyny musi być uruchomiona jedna z następujących hello obsługiwane 64-bitowe systemy operacyjne: <br/>— Windows Server 2012 R2<br/>— Windows Server 2012<br/>— Windows Server 2008 R2 z dodatkiem SP1 lub nowszej wersji.<br/><br/> Witaj system operacyjny musi być zainstalowany na dysku systemu operacyjnego hello dysku C. musi być dyskiem podstawowym z systemem Windows, a nie dynamiczny. Witaj dysku danych może być dynamiczny.<br/><br/>|
    | **Maszyny z systemem Linux** (fizycznej lub VMware) | Witaj maszyny musi być uruchomiona jedna z następujących hello obsługiwane 64-bitowe systemy operacyjne: <br/>-Red Hat Enterprise Linux 7.2, 7.1, 6.8 lub 6.7<br/>-Centos 7.2, 7.1, 7.0, 6.8, 6.7, 6.6 lub 6.5<br/>-Serwer Ubuntu 14.04 LTS (listę obsługiwanych jądra wersje Ubuntu, zobacz [obsługiwanych systemów operacyjnych](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions))<br/>— Oracle Enterprise Linux 6.5 lub 6.4, systemem albo hello Red Hat zgodny jądra lub podzielenie Enterprise jądra wersji 3 (UEK3)<br/>-SUSE Linux Enterprise Server 11 z dodatkiem SP4 lub SUSE Linux Enterprise Server 11 z dodatkiem SP3<br/><br/>Pliki/etc/hosts na chronionych komputerach musi mieć wpisów, które mapują hello hosta lokalnego nazwa tooIP skojarzonego z wszystkich kart sieciowych.<br/><br/>Po przejściu w tryb failover Chcąc tooan tooconnect maszyny Wirtualnej platformy Azure z systemem Linux przy użyciu klienta Secure Shell (SSH), sprawdź, czy usługa SSH hello na powitania chronione maszyny jest ustawiony toostart automatycznie po uruchomieniu systemu. Upewnij się, również reguły zapory zezwalają na maszynie toohello chronione połączenia SSH.<br/><br/>Nazwa hosta Hello, punkty instalacji, nazwy urządzenia i ścieżki systemu Linux i nazwy pliku (na przykład/etc / i usr) muszą być tylko w języku angielskim.<br/><br/>Witaj następujących katalogów (jeśli skonfigurowany jako osobne partycje lub systemu plików) wszystkie muszą być na powitania samego dysku (dysk systemu operacyjnego hello) na serwerze źródłowym hello:<br/>- / (root)<br/>- / rozruchu<br/>-usr<br/>-/ usr/lokalnego<br/>-/var<br/>- / itp<br/><br/>Obecnie XFS v5 funkcje, takie jak metadanych sumy kontrolnej, nie są obsługiwane przez usługę Site Recovery na XFS systemów plików. Upewnij się, że XFS systemów plików nie są użyciem dowolnej funkcji v5. Można użyć hello xfs_info narzędzie toocheck hello XFS superblock hello partycji. Jeśli **ftype** ustawiono zbyt**1**, XFS v5 funkcje są używane.<br/><br/>Na serwerach Red Hat Enterprise Linux 7 i CentOS 7 narzędzie lsof hello musi być zainstalowany i dostępny.<br/><br/>


## <a name="disaster-recovery-of-hyper-v-vms-tooazure-no-vmm"></a>Odzyskiwanie po awarii tooAzure maszyn wirtualnych funkcji Hyper-V (bez VMM)

Witaj następujące składniki są wymagane podczas odzyskiwania po awarii maszyn wirtualnych funkcji Hyper-V w chmurach programu VMM. Ponadto są toohello takich, które opisano w [wymagania dotyczące usługi Azure](#azure-requirements).

| **Wymagania wstępne** | **Szczegóły** |
| --- | --- |
| **Host funkcji Hyper-V** |Jeden lub więcej serwerów lokalnych musi działać system Windows Server 2012 R2 z hello najnowsze aktualizacje i włączonej roli Hyper-V hello lub Microsoft Hyper-V Server 2012 R2.<br/><br/>Serwery funkcji Hyper-V musi mieć przynajmniej jednej maszyny wirtualnej.<br/><br/>Serwery funkcji Hyper-V musi być połączony toohello Internetu, bezpośrednio lub za pośrednictwem serwera proxy.<br/><br/>Serwery funkcji Hyper-V muszą mieć hello poprawki opisanej w artykule bazy wiedzy Knowledge Base hello [2961977](https://support.microsoft.com/kb/2961977) zainstalowane.
|**Dostawca i agent**| Podczas wdrażania usługi Site Recovery instaluje się dostawcę usługi Azure Site Recovery hello. instalację dostawcy Hello instaluje również hello agenta usług odzyskiwania Azure na każdym serwerze funkcji Hyper-V, na którym jest zainstalowany maszyn wirtualnych, który ma zostać tooprotect. <br/><br/>Wszystkie serwery funkcji Hyper-V w usłudze Site Recovery magazynu musi mieć hello hello dostawca i hello agent tej samej wersji.<br/><br/>Dostawca Hello musi tooconnect tooSite odzyskiwania za pośrednictwem hello Internet. Może zostać wysłany ruch, bezpośrednio lub za pośrednictwem serwera proxy. Serwer proxy oparty na HTTPS nie jest obsługiwane. Serwer proxy Hello muszą zezwalać toohello dostępu następujące adresy URL:<br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/>Jeśli masz reguły zapory oparte na adresie IP na serwerze hello, upewnij się, hello reguły Zezwalaj na komunikację tooAzure.<br/><br/> Zezwalaj na powitania [zakresy IP centrum danych Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653)i HTTPS (port 443).<br/><br/> Zezwalaj na zakresy adresów IP dla hello Azure regionie Twojej subskrypcji i hello zachodnie stany USA (używanych do zarządzania tożsamości i kontroli dostępu).


## <a name="disaster-recovery-of-hyper-v-vms-in-vmm-clouds-tooazure"></a>Odzyskiwanie po awarii maszyn wirtualnych funkcji Hyper-V w tooAzure chmury VMM

Witaj następujące składniki są wymagane podczas odzyskiwania po awarii maszyn wirtualnych funkcji Hyper-V w chmurach programu VMM. Ponadto są toohello takich, które opisano w [wymagania dotyczące usługi Azure](#azure-requirements).

| **Wymagania wstępne** | **Szczegóły** |
| --- | --- |
| **Program Virtual Machine Manager** |Musi mieć co najmniej jeden serwer programu VMM uruchomiony w programie System Center 2012 R2 lub nowszy. Każdy serwer VMM musi mieć co najmniej jedną chmurę skonfigurowane. <br/><br/>Chmury muszą mieć:<br/>-Co najmniej jedną grupę hostów programu VMM.<br/>— Serwery hosta funkcji Hyper-V lub klastry w każdej grupie hostów.<br/><br/>Aby uzyskać więcej informacji na temat konfigurowania chmur programu VMM, zobacz [jak toocreate chmury w programie Virtual Machine Manager 2012](http://social.technet.microsoft.com/wiki/contents/articles/2729.how-to-create-a-cloud-in-vmm-2012.aspx). |
| **Funkcja Hyper-V** |Serwery hosta funkcji Hyper-V musi działać co najmniej Windows Server 2012 R2 z włączonej roli Hyper-V hello lub Microsoft Hyper-V Server 2012 R2. musi być zainstalowana Hello najnowsze aktualizacje.<br/><br/> Serwer funkcji Hyper-V musi mieć przynajmniej jednej maszyny wirtualnej.<br/><br/> Serwer hosta funkcji Hyper-V lub klastra, który zawiera maszyny wirtualne, które mają tooreplicate muszą być zarządzane w chmurze VMM.<br/><br/>Serwery funkcji Hyper-V musi być połączony toohello Internetu, bezpośrednio lub za pośrednictwem serwera proxy.<br/><br/>Serwery funkcji Hyper-V muszą mieć hello poprawki opisanej w artykule bazy wiedzy Knowledge Base hello [2961977](https://support.microsoft.com/kb/2961977) zainstalowane.<br/><br/>Serwery hosta funkcji Hyper-V wymagają dostępu do Internetu dla tooAzure replikacji danych. |
| **Dostawca i agent** |Podczas wdrażania usługi Azure Site Recovery Zainstaluj dostawcę usługi Azure Site Recovery na serwerze VMM hello. Zainstaluj agenta usług odzyskiwania na hostach funkcji Hyper-V. Witaj dostawca i agent muszą tooconnect tooAzure bezpośrednio przez hello Internet lub za pośrednictwem serwera proxy. Serwer proxy oparty na protokole HTTPS nie jest obsługiwany. Serwer proxy Hello na powitania serwera programu VMM i hosty funkcji Hyper-V należy zezwolić na dostęp do: <br/><br/>[!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)] <br/><br/>Jeśli masz reguły zapory oparte na adresie IP na serwerze VMM hello, upewnij się, czy hello reguły zezwalają na komunikację tooAzure.<br/><br/> Zezwalaj na powitania [zakresy IP centrum danych Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653) i HTTPS (port 443).<br/><br/>Zezwalaj na zakresy adresów IP dla hello region platformy Azure dla subskrypcji i zachodnie stany USA hello (używanych do zarządzania tożsamości i kontroli dostępu).<br/><br/> |

### <a name="replicated-machine-prerequisites"></a>Wymagania wstępne dotyczące replikowane maszyny

| **Składnik** | **Szczegóły** |
| --- | --- |
| **Chronione maszyny wirtualne** | Usługa Site Recovery obsługuje wszystkich systemów operacyjnych, które są obsługiwane przez [Azure](https://technet.microsoft.com/library/cc794868%28v=ws.10%29.aspx).<br/><br/>Maszyny wirtualne muszą spełniać hello [wymagania wstępne platformy Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) do tworzenia maszyny Wirtualnej platformy Azure. Nazwy komputerów musi wynosić od 1 do 63 znaków (należy użyć litery, cyfry i łączniki). Witaj nazwa musi zaczynać się literą lub cyfrą i kończyć literą lub cyfrą. <br/><br/>Nazwa maszyny Wirtualnej hello można zmodyfikować po włączeniu replikacji dla maszyny Wirtualnej hello. <br/><br/> Pojemność dysku dla każdego chronionego komputera nie może być więcej niż 1,023 GB. Maszyna wirtualna może zawierać maksymalnie too16 dysków (w górę too16 TB).<br/><br/>


## <a name="disaster-recovery-of-hyper-v-vms-in-vmm-clouds-tooa-customer-owned-site"></a>Odzyskiwanie po awarii maszyn wirtualnych funkcji Hyper-V w lokacji należące do klientów tooa chmur programu VMM

Witaj następujące składniki są wymagane podczas odzyskiwania po awarii maszyn wirtualnych funkcji Hyper-V w lokacji należące do klientów tooa chmur programu VMM. Ponadto są toohello takich, które opisano w [wymagania dotyczące usługi Azure](#azure-requirements).

| **Składnik** | **Szczegóły** |
| --- | --- |
| **Program Virtual Machine Manager** |  Zaleca się wdrożenie serwera programu VMM na powitania lokacji głównej i hello lokacji dodatkowej.<br/><br/> Możesz [replikacji między chmurami na jednym serwerze VMM](site-recovery-vmm-to-vmm.md#prepare-for-single-server-deployment). tooreplicate między chmurami na jednym serwerze programu VMM, należy co najmniej dwóch chmur skonfigurowane na serwerze VMM hello.<br/><br/> Serwery programu VMM musi działać co najmniej System Center 2012 SP1 z najnowszymi aktualizacjami hello.<br/><br/> Każdy serwer VMM musi mieć co najmniej jedną chmurę. Wszystkie chmury musi mieć powitalne zbioru profilów pojemności funkcji Hyper-V. <br/><br/>Chmury muszą mieć co najmniej jedną grupę hostów programu VMM. Aby uzyskać więcej informacji na temat konfigurowania chmur programu VMM, zobacz [przygotowanie do wdrożenia usługi Azure Site Recovery](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric). |
| **Funkcja Hyper-V** | Serwery funkcji Hyper-V musi działać co najmniej Windows Server 2012 z rolą funkcji Hyper-V hello włączony i ma hello zainstalowane najnowsze aktualizacje.<br/><br/> Serwer funkcji Hyper-V musi mieć przynajmniej jednej maszyny wirtualnej.<br/><br/>  Serwery hosta funkcji Hyper-V muszą znajdować się w grupach hostów w hello głównych i dodatkowych chmurach VMM.<br/><br/> Po uruchomieniu funkcji Hyper-V w klastrze systemu Windows Server 2012 R2, zaleca się zainstalowanie hello aktualizację opisaną w artykule bazy wiedzy [2961977](https://support.microsoft.com/kb/2961977).<br/><br/> Jeśli uruchamianie funkcji Hyper-V w klastrze, w systemie Windows Server 2012 i statyczne klaster oparte na adresie IP, broker klastra nie jest tworzone automatycznie. Należy ręcznie skonfigurować hello brokera klastra. Aby uzyskać więcej informacji na temat brokera klastra hello zobacz [rolę brokera repliki hello Konfigurowanie replikacji do klastra](http://social.technet.microsoft.com/wiki/contents/articles/18792.configure-replica-broker-role-cluster-to-cluster-replication.aspx). |
| **Dostawca** | Podczas wdrażania usługi Site Recovery Zainstaluj dostawcę usługi Azure Site Recovery hello na serwerach VMM. Dostawca Hello komunikuje się z usługą Site Recovery za pośrednictwem protokołu HTTPS (port 443) tooorchestrate replikacji. Dane replikacji między hello podstawowych i pomocniczych serwerów Hyper-V za pośrednictwem hello sieci LAN lub za pośrednictwem połączenia sieci VPN.<br/><br/> Witaj dostawcy, który jest uruchomiony na serwerze VMM hello musi uzyskać dostęp do toohello następujące adresy URL:<br/><br/>[!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)] <br/><br/>dostawcy usługi Site Recovery Hello muszą zezwalać na komunikację zapory z toohello serwery VMM hello [zakresy IP centrum danych Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653)i umożliwić hello protokołu HTTPS (port 443). |


## <a name="url-access"></a>Dostęp do adresu URL
Te adresy URL muszą być dostępne z Serwery hosta funkcji Hyper-V, VMware i VMM:

|**ADRES URL** | **Program VMM tooVMM** | **Program VMM tooAzure** | **TooAzure funkcji Hyper-V** | **VMware tooAzure** |
|--- | --- | --- | --- | --- |
|``*.accesscontrol.windows.net`` | Zezwalaj | Zezwalaj | Zezwalaj | Zezwalaj |
|``*.backup.windowsazure.com`` | Niewymagane | Zezwalaj | Zezwalaj | Zezwalaj |
|``*.hypervrecoverymanager.windowsazure.com`` | Zezwalaj | Zezwalaj | Zezwalaj | Zezwalaj |
|``*.store.core.windows.net`` | Zezwalaj | Zezwalaj | Zezwalaj | Zezwalaj |
|``*.blob.core.windows.net`` | Niewymagane | Zezwalaj | Zezwalaj | Zezwalaj |
|``https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi`` | Niewymagane | Niewymagane | Niewymagane | Zezwalaj na pobieranie programu SQL |
|``time.windows.com`` | Zezwalaj | Zezwalaj | Zezwalaj | Zezwalaj|
|``time.nist.gov`` | Zezwalaj | Zezwalaj | Zezwalaj | Zezwalaj |
