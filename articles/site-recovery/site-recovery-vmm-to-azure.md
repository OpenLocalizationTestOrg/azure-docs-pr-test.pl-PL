---
title: aaaReplicate maszyn wirtualnych funkcji Hyper-V w programie VMM chmur tooAzure | Dokumentacja firmy Microsoft
description: "Organizowania replikacji, trybu failover i odzyskiwania maszyn wirtualnych funkcji Hyper-V zarządzane w tooAzure chmur programu System Center VMM"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: tysonn
ms.assetid: 8e7d868e-00f3-4e8b-9a9e-f23365abf6ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 06/14/2017
ms.author: raynew
ms.openlocfilehash: 84182fe4b63862ac7643208a22f236a7515a25a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooazure-using-site-recovery-in-hello-azure-portal"></a>Replikowanie maszyn wirtualnych funkcji Hyper-V w tooAzure chmur programu VMM przy użyciu usługi Site Recovery w portalu Azure hello
> [!div class="op_single_selector"]
> * [Witryna Azure Portal](site-recovery-vmm-to-azure.md)
> * [Klasyczny portal Azure](site-recovery-vmm-to-azure-classic.md)
> * [Program PowerShell — model usługi Resource Manager](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [PowerShell — model klasyczny](site-recovery-deploy-with-powershell.md)


W tym artykule opisano sposób tooreplicate lokalnych maszyn wirtualnych funkcji Hyper-V zarządzanych w tooAzure chmur programu System Center VMM, przy użyciu hello [usługi Azure Site Recovery](site-recovery-overview.md) w hello portalu Azure.

Po przeczytaniu tego artykułu, post wszelkie komentarze u dołu hello, lub na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

Jeśli chcesz toomigrate tooAzure maszyny (bez powrotu po awarii), zapoznaj się z [w tym artykule](site-recovery-migrate-to-azure.md).


## <a name="deployment-steps"></a>Kroki wdrażania

Wykonaj następujące kroki wdrażania toocomplete artykułu hello:


1. [Dowiedz się więcej](site-recovery-components.md) informacje o architekturze powitania dla tego wdrożenia. [Dowiedz się](site-recovery-hyper-v-azure-architecture.md) też, jak działa replikacja funkcji Hyper-V w usłudze Site Recovery.
2. Zweryfikuj wymagania wstępne i ograniczenia.
3. Skonfiguruj konta magazynu i sieć platformy Azure.
4. Przygotuj hello na lokalnym serwerze VMM i hosty funkcji Hyper-V.
5. Utwórz magazyn usługi Recovery Services. Magazyn Hello zawiera ustawienia konfiguracji i organizuje replikację.
6. Określ ustawienia źródła. Zarejestruj powitania serwera VMM w magazynie hello. Zainstaluj hello dostawcy usługi Azure Site Recovery na powitania serwera instalacji hello usług odzyskiwania Microsoft agenta VMM na hostach funkcji Hyper-V.
7. Skonfiguruj ustawienia replikacji i miejsca docelowe.
8. Włącz replikację hello maszyn wirtualnych.
9. Uruchom test toomake trybu failover, się, że wszystko działa zgodnie z oczekiwaniami.



## <a name="prerequisites"></a>Wymagania wstępne


**Wymaganie obsługi** | **Szczegóły**
--- | ---
**Azure** | Dowiedz się więcej na temat [wymagań platformy Azure](site-recovery-prereq.md#azure-requirements).
**Serwery lokalne** | [Dowiedz się więcej](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-in-vmm-clouds-to-azure) o wymaganiach dotyczących hello na lokalnym serwerze VMM i hosty funkcji Hyper-V.
**Lokalne maszyny wirtualne funkcji Hyper-V** | Maszyny wirtualne mają powinna być uruchomiona tooreplicate [obsługiwanym systemie operacyjnym](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)i być zgodne z [wymagania wstępne platformy Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).
**Adresy URL platformy Azure** | Serwer VMM Hello musi uzyskać dostęp do toothese adresów URL:<br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> Jeśli masz reguły zapory oparte na adresie IP, sprawdź, czy umożliwiają one tooAzure komunikacji.<br/></br> Zezwalaj na powitania [zakresów IP centrum danych Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653)i hello port HTTPS (port 443).<br/></br> Zezwalaj na zakresy adresów IP dla hello Azure regionie Twojej subskrypcji i zachodnie stany USA (używanych do kontroli dostępu i zarządzania tożsamościami).


## <a name="prepare-for-deployment"></a>Przygotowanie do wdrożenia
tooprepare wdrożenia, musisz:

1. [Skonfiguruj sieć platformy Azure](#set-up-an-azure-network), w której maszyny wirtualne Azure zostaną umieszczone po przejściu do trybu failover.
2. [Skonfiguruj konto usługi Azure Storage](#set-up-an-azure-storage-account) dla replikowanych danych.
3. [Przygotowanie serwera VMM hello](#prepare-the-vmm-server) do wdrażania usługi Site Recovery.
4. Przygotuj się do mapowania sieci. Skonfiguruj sieci, aby umożliwić skonfigurowanie mapowania sieci podczas wdrażania usługi Site Recovery.

### <a name="set-up-an-azure-network"></a>Konfiguracja sieci platformy Azure
Należy toowhich Azure sieci maszyn wirtualnych Azure utworzonych po połączy trybu failover.

* Witaj sieć powinna znajdować się w hello magazyn usług odzyskiwania i tym samym regionie co hello.
* W zależności od modelu zasobu hello ma toouse nie powiodła się na maszynach wirtualnych platformy Azure, skonfigurowaniu hello sieć platformy Azure [tryb usługi Resource Manager](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) lub [trybu klasycznego](../virtual-network/virtual-networks-create-vnet-classic-pportal.md).
* Zaleca się skonfigurowanie sieci przed rozpoczęciem dalszych działań. Jeśli nie, należy toodo go podczas wdrażania usługi Site Recovery.
Azure sieci używane przez usługę Site Recovery nie może być [przenieść](../azure-resource-manager/resource-group-move-resources.md) w hello samego, lub przez inne subskrypcje.

### <a name="set-up-an-azure-storage-account"></a>Konfigurowanie konta usługi Azure Storage
* Potrzebujesz standardowego/premium konta magazynu Azure toohold dane replikowane tooAzure. [Magazyn w warstwie premium](../storage/common/storage-premium-storage.md) służy do maszyn wirtualnych, które wymagają wysoką wydajność We/Wy i intensywnych obciążeń we/wy toohost małe opóźnienia. Jeśli chcesz, aby toouse toostore konta premium zreplikowanych danych, należy również konta magazynu w warstwie standardowa toostore dzienników replikacji przechwytywania trwającą zmienia się tooon lokalne dane. Witaj, konto musi być w hello magazyn usług odzyskiwania i tym samym regionie co hello.
* W zależności od modelu zasobu hello ma toouse nie powiodła się na maszynach wirtualnych platformy Azure, należy skonfigurować konto w [tryb usługi Resource Manager](../storage/common/storage-create-storage-account.md) lub [trybu klasycznego](../storage/common/storage-create-storage-account.md).
* Zalecamy skonfigurowanie konta przed rozpoczęciem dalszych działań. Jeśli nie, należy toodo go podczas wdrażania usługi Site Recovery.
- Należy pamiętać, że konta magazynu używane przez usługę Site Recovery nie może być [przenieść](../azure-resource-manager/resource-group-move-resources.md) w hello samego, lub przez inne subskrypcje.

### <a name="prepare-hello-vmm-server"></a>Przygotowanie serwera VMM hello
* Upewnij się, że ten serwer VMM hello jest zgodny z hello [wymagania wstępne](#prerequisites).
* Podczas wdrażania usługi Site Recovery można określić, że wszystkie chmury na serwerze VMM powinny być dostępne w hello portalu Azure. Jeśli chcesz tylko tooappear określonych chmur w portalu hello, można włączyć ustawienie hello chmury w konsoli administracyjnej programu VMM hello.

### <a name="prepare-for-network-mapping"></a>Przygotowanie do mapowania sieci
Podczas wdrażania usługi Site Recovery musisz skonfigurować mapowanie sieci. Mapowanie sieci działa między źródłowymi sieciami maszyny Wirtualnej programu VMM i docelowymi sieciami platformy Azure, hello tooenable następujące:

* Maszyny, które w tryb failover na powitania sam sieci można połączyć tooeach innych, nawet jeśli przeszły przez w hello sam sposób lub w hello tego samego planu odzyskiwania.
* Jeśli brama sieci jest skonfigurowana na powitania docelową sieć platformy Azure, maszyny wirtualne platformy Azure można połączyć tooon lokalne maszyny wirtualne.
* tooset mapowanie sieci, Oto co należy zrobić:

  * Upewnij się, że maszyny wirtualne w źródle powitania serwera hosta funkcji Hyper-V są tooa połączonych sieci maszyny Wirtualnej VMM. Ta sieć powinna być tooa połączone sieci logicznej, która jest skojarzona z chmurą hello.
  * Sieć platformy Azure zgodnie z [powyższym](#set-up-an-azure-network) opisem

## <a name="create-a-recovery-services-vault"></a>Tworzenie magazynu Usług odzyskiwania
1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).
2. Kliknij pozycję **Nowy** > **Monitorowanie i zarządzanie** > **Backup and Site Recovery (OMS)**.

    ![Nowy magazyn](./media/site-recovery-vmm-to-azure/new-vault3.png)
3. W **nazwa**, określ przyjazną nazwę tooidentify hello magazynu. Jeśli masz więcej niż jedną subskrypcję, wybierz jedną z nich.
4. [Utwórz grupę zasobów](../azure-resource-manager/resource-group-template-deploy-portal.md) lub wybierz istniejącą. Określ region platformy Azure. Maszyny będą replikowane toothis regionu. toocheck obsługiwane regiony, zobacz dotyczącą dostępności geograficznej w [szczegóły cennika usługi Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/)
5. Tooquickly dostępu hello magazynu z hello pulpitu nawigacyjnego, kliknij przycisk **toodashboard numeru Pin** > **Utwórz magazyn**.

    ![Nowy magazyn](./media/site-recovery-vmm-to-azure/new-vault.png)

na powitania pojawi się nowy magazyn Hello **pulpitu nawigacyjnego** > **wszystkie zasoby**, a na powitania głównego **Magazyny usług odzyskiwania** bloku.


## <a name="select-hello-protection-goal"></a>Wybierz cel ochrony hello

Wybierz, co ma tooreplicate, i miejsce tooreplicate do.

1. W **Magazyny usług odzyskiwania**, wybierz pozycję hello magazynu.
2. W sekcji **Wprowadzenie** kliknij pozycję **Site Recovery** > **Przygotowanie infrastruktury** > **Cel ochrony**.

    ![Wybieranie celów](./media/site-recovery-vmm-to-azure/choose-goals.png)
3. W **cel ochrony** wybierz **tooAzure**i wybierz **tak, z funkcją Hyper-V**. Wybierz **tak** tooconfirm używasz hostów funkcji Hyper-V toomanage programu VMM i hello odzyskiwania lokacji. Następnie kliknij przycisk **OK**.

## <a name="set-up-hello-source-environment"></a>Konfigurowanie środowiska źródłowego hello

Zainstaluj hello dostawcy usługi Azure Site Recovery na serwerze VMM hello i Zarejestruj serwer hello w magazynie hello. Zainstaluj agenta usług odzyskiwania Azure hello na hostach funkcji Hyper-V.

1. Kliknij pozycję **Przygotowanie infrastruktury** > **Źródło**.

    ![Konfiguracja źródła](./media/site-recovery-vmm-to-azure/set-source1.png)

2. W **Przygotuj źródło**, kliknij przycisk **+ VMM** tooadd serwera programu VMM.

    ![Konfiguracja źródła](./media/site-recovery-vmm-to-azure/set-source2.png)

3. W **Dodaj serwer**, sprawdź, czy **serwera programu System Center VMM** pojawia się w **typ serwera** , że serwer VMM hello spełnia hello [warunki wstępne i adres URL wymagania dotyczące](#prerequisites).
4. Pobierz plik instalacyjny dostawcy usługi Azure Site Recovery hello.
5. Pobierz klucz rejestracji hello. Będzie on potrzebny po uruchomieniu Instalatora. klucz Hello jest ważny przez pięć dni po jego wygenerowaniu.

    ![Konfiguracja źródła](./media/site-recovery-vmm-to-azure/set-source3.png)


## <a name="install-hello-provider-on-hello-vmm-server"></a>Zainstaluj na serwerze VMM hello hello dostawcy

1. Uruchom plik Instalatora dostawcy hello na powitania serwera VMM.
2. W usłudze **Microsoft Update** można włączyć aktualizacje, aby aktualizacje dostawcy były instalowane zgodnie z zasadami Microsoft Update.
3. W **instalacji**, Zaakceptuj lub zmodyfikuj hello domyślną lokalizację instalacji dostawcy i kliknij przycisk **zainstalować**.

    ![Lokalizacja instalacji](./media/site-recovery-vmm-to-azure/provider2.png)
4. Po zakończeniu instalacji kliknij przycisk **zarejestrować** tooregister hello menedżerem maszyny wirtualnej w magazynie hello.
5. W hello **ustawienia magazynu** kliknij przycisk **Przeglądaj** plik klucza tooselect hello magazynu. Określ subskrypcję usługi Azure Site Recovery hello i hello nazwę magazynu.

    ![Rejestracja serwera](./media/site-recovery-vmm-to-azure/provider10.PNG)
6. W **połączenia internetowego**, określ, jak dostawca uruchomiony na serwerze VMM hello łączą tooSite odzyskiwania przez hello hello internet.

   * Tooconnect dostawcy hello bezpośrednio, wybierz opcję **łączą się bezpośrednio tooAzure odzyskiwania lokacji bez serwera proxy**.
   * Jeśli istniejący serwer proxy wymaga uwierzytelniania lub chcesz toouse niestandardowego serwera proxy, zaznacz **połączyć tooAzure Przywracanie lokacji z użyciem serwera proxy**.
   * Jeśli używasz niestandardowego serwera proxy, określ adres hello, port oraz poświadczenia.
   * Jeśli używasz serwera proxy, możesz już zezwolono hello adresów URL opisanych w [wymagania wstępne](#on-premises-prerequisites).
   * Jeśli używasz niestandardowego serwera proxy konto Uruchom jako programu VMM (DRAProxyAccount) zostanie utworzony automatycznie za pomocą hello określone poświadczenia serwera proxy. Konfiguracja serwera proxy hello, dzięki czemu to konto mogło być pomyślnie uwierzytelnione. Ustawienia konta Uruchom jako programu VMM Hello można modyfikować w konsoli programu VMM hello. W **ustawienia**, rozwiń węzeł **zabezpieczeń** > **konta Uruchom jako**, a następnie zmodyfikuj hello hasło dla konta DRAProxyAccount. Usługa VMM hello toorestart należy tak, aby to ustawienie zostało zastosowane.

     ![Internet](./media/site-recovery-vmm-to-azure/provider13.PNG)
7. Zaakceptuj lub zmodyfikuj lokalizację hello certyfikat SSL, który jest automatycznie generowany do szyfrowania danych. Ten certyfikat jest używany, jeśli włączysz szyfrowanie danych dla chmury chronionej przez platformę Azure w portalu usługi Azure Site Recovery hello. Przechowuj ten certyfikat w bezpiecznym miejscu. Po uruchomieniu tooAzure trybu failover należy ją toodecrypt, jeśli jest włączone szyfrowanie danych.

    > [!NOTE]
    > Zalecane jest możliwość szyfrowania hello toouse dostarczany przez platformę Azure szyfrowanie danych magazynowanych zamiast opcji szyfrowania danych hello udostępniane przez usługi Azure Site Recovery. możliwość szyfrowania Hello dostarczany przez platformę Azure może być włączona dla magazynu > konta i pomaga osiągnąć lepszą wydajność, ponieważ hello szyfrowania i odszyfrowywania jest obsługiwany przez usługi Azure storage.
    > [Dowiedz się więcej o funkcji Szyfrowanie usługi Storage platformy Azure](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption).
    
8. W **nazwy serwera**, określ serwer VMM hello tooidentify przyjazną nazwę w magazynie hello. W konfiguracji klastra Określ nazwę roli klastra VMM hello.
9. Włącz **synchronizację metadanych chmury**, jeśli chcesz toosynchronize metadane dla wszystkich chmur na powitania serwera VMM w magazynie hello. Ta akcja wymaga tylko toohappen raz na każdym serwerze. Jeśli nie chcesz toosynchronize wszystkich chmur, można zaznaczać tego ustawienia i synchronizować poszczególne chmury indywidualnie WE hello właściwości chmury w konsoli programu VMM hello. Kliknij przycisk **zarejestrować** toocomplete hello procesu.

    ![Rejestracja serwera](./media/site-recovery-vmm-to-azure/provider16.PNG)
10. Rozpoczyna się rejestracja. Po zakończeniu rejestracji serwer hello jest wyświetlany w **infrastruktura usługi Site Recovery** > **serwery VMM**.


## <a name="install-hello-azure-recovery-services-agent-on-hyper-v-hosts"></a>Zainstaluj agenta usług odzyskiwania Azure hello na hostach funkcji Hyper-V

1. Po skonfigurowaniu hello dostawcy należy plik instalacyjny hello toodownload hello agenta usług odzyskiwania Azure. Uruchom Instalatora na każdym serwerze funkcji Hyper-V w chmurze VMM hello.

    ![Lokacje funkcji Hyper-V](./media/site-recovery-vmm-to-azure/hyperv-agent1.png)
2. W obszarze **Sprawdzanie wymagań wstępnych** kliknij przycisk **Dalej**. Wszystkie brakujące wymagania wstępne zostaną zainstalowane automatycznie.

    ![Wymagania wstępne dotyczące agenta Usług odzyskiwania](./media/site-recovery-vmm-to-azure/hyperv-agent2.png)
3. W **ustawienia instalacji**Zaakceptuj lub zmodyfikuj lokalizację instalacji hello i hello lokalizacji pamięci podręcznej. Witaj w pamięci podręcznej można skonfigurować na dysku, który ma co najmniej 5 GB miejsca do magazynowania, ale zalecamy dysk pamięci podręcznej z najmniej 600 GB wolnego miejsca. Następnie kliknij pozycję **Zainstaluj**.
4. Po zakończeniu instalacji kliknij przycisk **Zamknij** toofinish.

    ![Rejestracja agenta MARS](./media/site-recovery-vmm-to-azure/hyperv-agent3.png)

### <a name="command-line-installation"></a>Instalacja przy użyciu wiersza polecenia
Hello agenta usług odzyskiwania Microsoft Azure można zainstalować z wiersza polecenia przy użyciu hello następujące polecenie:

     marsagentinstaller.exe /q /nu

### <a name="set-up-internet-proxy-access-toosite-recovery-from-hyper-v-hosts"></a>Konfigurowanie internetowego serwera proxy dostępu tooSite odzyskiwania z hostów funkcji Hyper-V

agenta usług odzyskiwania Hello na hostach funkcji Hyper-V musi mieć tooAzure dostęp do Internetu w przypadku replikacji maszyny Wirtualnej. Jeśli uzyskujesz dostęp do Internetu hello za pośrednictwem serwera proxy, skonfiguruj go w następujący sposób:

1. Otwórz hello Microsoft Azure Backup przystawka programu MMC na hoście funkcji Hyper-V hello. Domyślnie skrót do usługi Kopia zapasowa Microsoft Azure jest dostępny na pulpicie hello, lub C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.
2. W przystawce hello, kliknij przycisk **Zmień właściwości**.
3. Na powitania **konfiguracji serwera Proxy** karcie, określ informacje dotyczące serwera proxy.

    ![Rejestracja agenta MARS](./media/site-recovery-vmm-to-azure/mars-proxy.png)
4. Sprawdź ten hello agent może osiągnąć adresy URL hello opisanego w hello [wymagania wstępne](#on-premises-prerequisites).

## <a name="set-up-hello-target-environment"></a>Konfigurowanie środowiska docelowego hello
Określ toobe konta magazynu Azure hello używanych w przypadku replikacji, a hello toowhich sieć platformy Azure, maszyny wirtualne Azure będą się łączyć po pracy awaryjnej.

1. Kliknij przycisk **przygotowanie infrastruktury** > **docelowego**, wybierz subskrypcję hello i hello grupy zasobów, w którym ma hello toocreate przejścia w tryb failover maszyny wirtualnej. Wybierz model wdrożenia hello, która ma toouse na platformie Azure (Zarządzanie zasobu lub classic) hello przejścia w tryb failover maszyny wirtualnej.

    ![Magazyn](./media/site-recovery-vmm-to-azure/enablerep3.png)

2. Usługa Site Recovery sprawdza, czy masz co najmniej jedno zgodne konto magazynu Azure i co najmniej jedną sieć platformy Azure.

    ![Magazyn](./media/site-recovery-vmm-to-azure/compatible-storage.png)

3. Jeśli nie utworzono konto magazynu, i chcesz toocreate jeden przy użyciu usługi Resource Manager, kliknij przycisk **+ konto magazynu** toodo tym miejscu.  Na powitania **utworzyć konto magazynu** bloku Określ nazwę konta, typ subskrypcji i lokalizacji. Witaj, konto musi należeć do hello tej samej lokalizacji co hello magazyn usług odzyskiwania.

   ![Magazyn](./media/site-recovery-vmm-to-azure/gs-createstorage.png)


   * Jeśli toocreate konto magazynu przy użyciu modelu klasycznego hello, należy to zrobić w hello portalu Azure. [Dowiedz się więcej](../storage/common/storage-create-storage-account.md)
   * Jeśli używasz konta magazynu w warstwie premium dla replikowanych danych, skonfiguruj dodatkowe konto magazynu, toostore dzienników replikacji, które przechwytują zachodzące zmiany lokalne tooon danych.
5. Jeśli nie utworzono sieci platformy Azure, i chcesz toocreate jeden przy użyciu usługi Resource Manager, kliknij przycisk **+ sieć** toodo tym miejscu. Na powitania **Utwórz sieć wirtualną** bloku określić nazwę sieciową, zakres adresów, szczegóły podsieci, subskrypcji i lokalizacji. Witaj sieć powinna znajdować się w hello tej samej lokalizacji co hello magazyn usług odzyskiwania.

   ![Sieć](./media/site-recovery-vmm-to-azure/gs-createnetwork.png)

   Jeśli toocreate sieci przy użyciu modelu klasycznego hello, należy to zrobić w hello portalu Azure. [Dowiedz się więcej](../virtual-network/virtual-networks-create-vnet-classic-pportal.md).

### <a name="configure-network-mapping"></a>Konfiguracja mapowania sieci

* [Przeczytaj](#prepare-for-network-mapping) szybkie omówienie funkcji mapowania sieci.
* Sprawdź, czy maszyny wirtualne na serwerze VMM hello tooa połączonych sieci maszyny Wirtualnej i czy utworzono przynajmniej jedną sieć wirtualną platformy Azure. Wiele sieci Vmnetwork może być zmapowane tooa pojedynczej sieci platformy Azure.

Skonfiguruj mapowanie w następujący sposób:

1. W **infrastruktura usługi Site Recovery** > **mapowania sieci** > **mapowanie sieci**, kliknij przycisk hello **+ mapowanie sieci**  ikony.

    ![Mapowanie sieci](./media/site-recovery-vmm-to-azure/network-mapping1.png)
2. W **Dodaj mapowanie sieci**, wybierz pozycję hello źródłowy serwer VMM i **Azure** jako cel hello.
3. Sprawdź hello subskrypcji i modelu wdrażania powitania po pracy awaryjnej.
4. W **Sieć źródłowa**, wybierz pozycję hello źródłowej lokalnej sieci maszyny Wirtualnej ma toomap z listy hello skojarzone z serwerem VMM hello.
5. W **Sieć docelowa**, wybierz hello sieć platformy Azure, w którym replika Azure zostaną umieszczone podczas są tworzone. Następnie kliknij przycisk **OK**.

    ![Mapowanie sieci](./media/site-recovery-vmm-to-azure/network-mapping2.png)

Oto, co się dzieje po rozpoczęciu mapowania sieci:

* Istniejące maszyny wirtualne w źródłowej sieci maszyny Wirtualnej hello są toohello połączonych sieci docelowej po rozpoczęciu mapowania. Nowych maszyn wirtualnych połączonych toohello źródłowej sieci maszyny Wirtualnej są połączone toohello mapowane sieć platformy Azure, podczas replikacji.
* Jeśli zmodyfikujesz istniejące mapowanie sieci maszyn wirtualnych repliki Połącz przy użyciu nowych ustawień hello.
* Jeśli hello Sieć docelowa ma wiele podsieci i jedna z tych podsieci ma hello znajduje się samą nazwę jak podsieć, w których hello źródłowej maszyny wirtualnej, a następnie maszyny wirtualnej repliki hello łączy toothat docelowej podsieci po pracy awaryjnej.
* Jeśli nie ma żadnych docelowa podsieć o pasującej nazwie, maszyna wirtualna hello łączy toohello pierwszej podsieci w sieci hello.

## <a name="configure-replication-settings"></a>Konfigurowanie ustawień replikacji
1. Kliknij przycisk toocreate nowe zasady replikacji, **przygotowanie infrastruktury** > **ustawienia replikacji** > **+ Utwórz i skojarz**.

    ![Sieć](./media/site-recovery-vmm-to-azure/gs-replication.png)
2. W obszarze **Utwórz i skojarz zasady** określ nazwę zasad.
3. W **częstotliwość kopiowania**, określić, jak często dane różnicowe tooreplicate po replikacji początkowej hello (co 30 sekund, 5 lub 15 minut).

    > [!NOTE]
    >  30 częstotliwość drugiego nie jest obsługiwane podczas replikowania toopremium magazynu. ograniczenie Hello jest określana przez hello liczby migawek dla obiekt blob (w 100) obsługiwane przez Magazyn w warstwie premium. [Dowiedz się więcej](../storage/common/storage-premium-storage.md#snapshots-and-copy-blob)

4. W **przechowywania punktu odzyskiwania**, określ w godzinach, jak długo będą hello okna przechowywania dla każdego punktu odzyskiwania. Chronione maszyny można odzyskać tooany punktu, w tym oknie.
5. W obszarze **Częstotliwość migawek spójności aplikacji** określ, jak często (1–12 godzin) będą tworzone punkty odzyskiwania zawierające migawki spójne z aplikacjami. Funkcja Hyper-V wykorzystuje dwa typy migawek — standardową migawkę, która jest przyrostową migawką całej maszyny wirtualnej hello i migawki spójne z aplikacją, która tworzy migawkę danych aplikacji hello wewnątrz maszyny wirtualnej hello punktu w czasie. Migawki spójne z aplikacjami Użyj tooensure usługi kopiowania woluminów w tle (VSS), które aplikacje są w spójnym stanie podczas hello migawki. Należy pamiętać, że po włączeniu migawek spójnych z aplikacją ma wpływ na powitania wydajność aplikacji uruchomionych na źródłowych maszynach wirtualnych. Upewnij się, że ustawiona wartość hello jest mniejsza niż liczba hello punktów odzyskiwania dodatkowe, które można skonfigurować.
6. W **czas rozpoczęcia replikacji początkowej**, wskazuje, kiedy toostart hello replikacji początkowej. Hello replikacja odbywa się za pośrednictwem przepustowości połączenia z Internetem, może być tooschedule ją poza najbardziej obciążonymi godzinami.
7. W **Szyfruj dane przechowywane na platformie Azure**, określ, czy tooencrypt dane w stanie spoczynku w magazynie Azure. Następnie kliknij przycisk **OK**.

    ![Zasady replikacji](./media/site-recovery-vmm-to-azure/gs-replication2.png)
8. Podczas tworzenia nowych zasad jest ona automatycznie skojarzona z hello chmury VMM. Kliknij przycisk **OK**. Dodatkowe chmury VMM (oraz hello maszyn wirtualnych w nich) można skojarzyć z zasadami replikacji w **replikacji** > nazwa_zasady > **Skojarz chmurę VMM**.

    ![Zasady replikacji](./media/site-recovery-vmm-to-azure/policy-associate.png)

## <a name="capacity-planning"></a>Planowanie pojemności

Teraz, po skonfigurowaniu podstawowej infrastruktury, pomyśl o planowaniu pojemności i zorientuj się, czy potrzebujesz dodatkowych zasobów.

Usługa Site Recovery zapewnia toohelp planowania pojemności przydzielić hello odpowiednich zasobów dotyczących środowiska źródłowego, składników usługi Site Recovery, sieci i magazynu. Hello planistę można uruchomić w trybie szybkim, aby uzyskać szacunkowe wartości oparte na średnich liczbach maszyn wirtualnych, dysków i pamięci masowej lub w trybie szczegółowym, w którym możesz wpisać dane na poziomie obciążenia hello. Przed rozpoczęciem:

* Zebrać informacje o środowisku replikacji, w tym o maszynach wirtualnych, liczbie dysków na maszynę wirtualną oraz pojemności dysków.
* Szacowana hello codziennych zmian (przenoszenia) szybkość będziesz mieć dla replikowanych danych. Można użyć hello [Capacity planner dla funkcji Hyper-V Replica](https://www.microsoft.com/download/details.aspx?id=39057) toohelp to zrobić.

1. Kliknij przycisk **Pobierz**, toodownload hello narzędzia, a następnie uruchom go. [Przeczytaj artykuł hello](site-recovery-capacity-planner.md) dołączony hello narzędzia.
2. Gdy wszystko będzie gotowe, wybierz **tak** w **zostało uruchomione hello Capacity Planner**?

   ![Planowanie pojemności](./media/site-recovery-vmm-to-azure/gs-capacity-planning.png)

   Więcej informacji na temat [sterowania przepustowością sieci](#network-bandwidth-considerations)




## <a name="enable-replication"></a>Włączanie replikacji

Przed rozpoczęciem należy upewnić się, że konto użytkownika usługi Azure ma hello wymagane [uprawnienia](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable replikację nowego tooAzure maszyny wirtualnej.

Teraz włącz replikację w następujący sposób:

1. Kliknij kolejno pozycje **Krok 2. Replikowanie aplikacji** > **Źródło**. Po włączeniu replikacji dla powitania po raz pierwszy, kliknij przycisk **+ Replikuj** w hello magazynu tooenable replikację dla dodatkowych maszyn.

    ![Włączanie replikacji](./media/site-recovery-vmm-to-azure/enable-replication1.png)
2. W hello **źródła** bloku, wybierz powitania serwera programu VMM i chmury hello w których hello funkcji Hyper-V znajdują się hosty. Następnie kliknij przycisk **OK**.

    ![Włączanie replikacji](./media/site-recovery-vmm-to-azure/enable-replication-source.png)
3. W **docelowego**, wybierz hello subskrypcję, model wdrożenia po pracy w trybie failover, i hello konto magazynu używane dla replikowanych danych.

    ![Włączanie replikacji](./media/site-recovery-vmm-to-azure/enable-replication-target.png)
4. Wybierz konto magazynu hello, które chcesz toouse. Jeśli chcesz toouse innego konta magazynu niż te, które masz, możesz [utworzyć](#set-up-an-azure-storage-account). Jeśli używasz konta magazynu w warstwie premium dla replikowanych danych, należy tooselect dodatkowego magazynu standardowego konta toostore dzienników replikacji które przechwytują zachodzące zmiany lokalne tooon data.toocreate konto magazynu przy użyciu modelu Resource Manager hello Kliknij przycisk **Utwórz nowy**. Jeśli toocreate konto magazynu przy użyciu modelu klasycznego hello, należy to zrobić [w portalu Azure hello](../storage/common/storage-create-storage-account.md). Następnie kliknij przycisk **OK**.
5. Wybierz hello Azure toowhich sieci i podsieci maszyn wirtualnych platformy Azure będą się łączyć, gdy są tworzone po pracy awaryjnej. Wybierz **Konfiguruj teraz dla wybranych maszyn**, tooapply hello sieci ustawienie tooall maszyn wybranych do ochrony. Wybierz **później skonfigurować**, hello tooselect sieć platformy Azure dla poszczególnych komputerów. Jeśli chcesz toouse inną sieć z tymi masz, możesz [utworzyć](#set-up-an-azure-network). toocreate sieci za pomocą funkcji hello modelu Resource Manager, kliknij przycisk **Utwórz nowy**. Jeśli toocreate sieci przy użyciu modelu klasycznego hello, należy to zrobić [w portalu Azure hello](../virtual-network/virtual-networks-create-vnet-classic-pportal.md). Wybierz podsieć, jeśli jest to konieczne. Następnie kliknij przycisk **OK**.
6. W **maszyn wirtualnych** > **wybierz maszyny wirtualne**, kliknij i zaznacz każdy komputer ma tooreplicate. Możesz wybrać tylko te maszyny, dla których można włączyć replikację. Następnie kliknij przycisk **OK**.

    ![Włączanie replikacji](./media/site-recovery-vmm-to-azure/enable-replication5.png)

7. W **właściwości** > **skonfigurować właściwości**, wybierz system operacyjny hello hello wybrane maszyn wirtualnych i hello dysku systemu operacyjnego.

    - Sprawdź, że hello maszyny Wirtualnej Azure nazwę (docelowy) jest zgodna z [wymagania maszyny wirtualnej platformy Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).   
    - Domyślnie wybrane są wszystkie dyski hello hello maszyny Wirtualnej replikacji, ale można wyczyścić tooexclude dysków je.

        - Możesz tooexclude dysków tooreduce replikacji przepustowości. Na przykład nie ma dysków tooreplicate o dane tymczasowe, lub dane, które ma odświeżane za każdym razem komputera lub aplikacje ponownego uruchomienia (na przykład pagefile.sys lub tempdb programu Microsoft SQL Server). Witaj dysku można wykluczyć z replikacji przez unselecting hello dysku.
        - Wykluczyć można tylko dyski podstawowe. Nie można wykluczyć dysków systemu operacyjnego.
        - Nie zalecamy wykluczania dysków dynamicznych. Wewnątrz maszyny wirtualnej gościa usługa Site Recovery nie może ustalić, czy wirtualny dysk twardy jest dyskiem podstawowym, czy dynamicznym. Wszystkie dyski woluminu dynamicznego zależnego nie są wykluczone, chronionego dysku dynamicznego hello wyświetli jako dysk nie powiodło się podczas hello maszyny Wirtualnej nie powiedzie się za pośrednictwem i dane hello na tym dysku nie będą dostępne.
        - Po włączeniu replikacji nie można dodawać ani usuwać dysków do replikacji. Tooadd lub wykluczyć dysk, wymagają ochrony toodisable dla hello maszyny Wirtualnej, a następnie włącz go ponownie.
        - Dyski tworzone ręcznie na platformie Azure nie mają możliwości powrotu po awarii. Na przykład jeśli się nie powieść ponad trzy dyski, a następnie utwórz dwa bezpośrednio w maszynie Wirtualnej platformy Azure, tylko te trzy dyski hello, które zostały przełączone do trybu failover nie powiedzie się z tooHyper Azure-V. Nie można dołączyć dyski utworzone ręcznie w przypadku powrotu po awarii lub w replikacji odwrotnej z tooAzure funkcji Hyper-V.
        - Jeśli dysk jest potrzebna dla toooperate aplikacji zostaną wykluczone, po tooAzure pracy awaryjnej należy toocreate, który można uruchomić go ręcznie na platformie Azure, tak że hello replikowane aplikacji. Alternatywnie można zintegrować usługi Automatyzacja Azure do planu odzyskiwania toocreate hello dysku podczas pracy awaryjnej hello maszyny.

    Kliknij przycisk **OK** toosave zmiany. Później możesz skonfigurować dodatkowe właściwości.

    ![Włączanie replikacji](./media/site-recovery-vmm-to-azure/enable-replication6-with-exclude-disk.png)

8. W **ustawienia replikacji** > **Konfigurowanie ustawień replikacji**, wybierz zasady replikacji hello ma tooapply hello chronionych maszyn wirtualnych. Następnie kliknij przycisk **OK**. Możesz zmodyfikować zasady replikacji hello w **zasady replikacji** > nazwa_zasady > **Edytuj ustawienia**. Zastosowane zmiany są używane dla obecnie replikowanych i nowych maszyn.

   ![Włączanie replikacji](./media/site-recovery-vmm-to-azure/enable-replication7.png)

Możesz śledzić postępy hello **Włącz ochronę** zadania w **zadania** > **zadania usługi Site Recovery**. Po hello **zakończenia ochrony** zadanie jest uruchamiane, hello maszyna jest gotowa do pracy awaryjnej.

### <a name="view-and-manage-vm-properties"></a>Wyświetlanie właściwości maszyny wirtualnej i zarządzanie nimi

Firma Microsoft zaleca sprawdzenie właściwości hello hello maszyny źródłowej. Pamiętaj o tej nazwie maszyny Wirtualnej Azure hello powinna być zgodna z [wymagania maszyny wirtualnej platformy Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).

1. W **chronione elementy**, kliknij przycisk **elementy replikowane**, i wybierz hello toosee maszyny jego szczegóły.

    ![Włączanie replikacji](./media/site-recovery-vmm-to-azure/vm-essentials.png)
2. W **właściwości**, można wyświetlić replikacji i trybu failover informacje dotyczące hello maszyny Wirtualnej.

    ![Włączanie replikacji](./media/site-recovery-vmm-to-azure/test-failover2.png)
3. W **obliczenia i sieć** > **właściwości obliczeń**, można określić rozmiaru maszyny Wirtualnej Azure hello nazwę i obiekt docelowy. Modyfikowanie hello nazwa toocomply z [wymagania dotyczące usługi Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) Jeśli potrzebujesz. Można również wyświetlać i modyfikować informacje dotyczące sieci docelowej hello, podsieci i hello adres IP, który jest przypisywany toohello maszyny Wirtualnej platformy Azure.
Należy pamiętać, że:

   * Można ustawić hello docelowy adres IP. Jeśli nie podasz adresu, hello maszyny przełączonej będzie używać protokołu DHCP. Jeśli ustawisz adres, który nie jest dostępna w trybie failover hello trybu failover zakończy się niepowodzeniem. Witaj, sam docelowy adres IP może być używane do testowania trybu failover, jeśli adres hello jest dostępny w testowej sieci trybu failover hello.
   * Hello liczbę kart sieciowych jest zależna hello rozmiar dla hello docelowej maszyny wirtualnej, w następujący sposób:

     * Jeśli hello liczbę kart sieciowych na maszynie źródłowej hello jest mniejsza lub równa toohello liczba kart dozwoloną dla rozmiaru maszyny docelowej hello, a następnie hello docelowa będzie mieć hello samą liczbę kart sieciowych jako źródło hello.
     * Jeśli przekracza hello liczbę kart sieciowych dla źródłowej maszyny wirtualnej hello dozwolona liczba hello hello rozmiaru docelowego, a następnie maksymalny rozmiar docelowy hello jest używany.
     * Na przykład jeśli maszyna źródłowa ma dwie karty sieciowe i rozmiaru maszyny docelowej hello obsługuje cztery karty, maszyna docelowa hello będzie mieć dwie karty sieciowe. Jeśli hello maszyna źródłowa ma dwie karty sieciowe, ale hello rozmiar docelowy obsługiwanych obsługuje tylko jedną, maszyna docelowa hello będzie mieć tylko jedną kartę.     
     * Jeśli hello maszyna wirtualna ma wiele kart sieciowych, wszystkie będą łączyć toohello tej samej sieci.

     ![Włączanie replikacji](./media/site-recovery-vmm-to-azure/test-failover4.png)

4. W **dysków** możesz wyświetlać hello systemu operacyjnego i dysków z danymi na powitania maszyny Wirtualnej, która będzie replikowana.

#### <a name="managed-disks"></a>Dyski zarządzane

W **obliczenia i sieć** > **właściwości obliczeń**, można ustawić "Użyj zarządzanego dysków" Ustawienie zbyt "tak" hello maszyny Wirtualnej, jeśli chcesz tooattach dysków zarządzanych tooyour maszyny na tooAzure migracji. Dyski zarządzane upraszcza zarządzanie dysku dla maszyn wirtualnych IaaS platformy Azure, zarządzając hello konta magazynu skojarzone z hello dysków maszyny Wirtualnej. [Dowiedz się więcej o dyskach zarządzanych](https://docs.microsoft.com/en-us/azure/storage/storage-managed-disks-overview).

   - Dyski zarządzane są maszyny wirtualnej toohello utworzony i dołączone tylko na tooAzure trybu failover. Po włączeniu ochrony, dane z lokalnych maszyn będzie tooreplicate toostorage kont.
   Dyski zarządzane mogą być tworzone tylko dla maszyn wirtualnych wdrożonych przy użyciu modelu wdrażania Menedżera zasobów hello.  

  > [!NOTE]
  > Powrotu po awarii w środowisku funkcji Hyper-V Azure tooon lokalne nie jest obecnie obsługiwany dla maszyn z dyskami zarządzanych. Ustaw "Użyj zarządzanego dysków" za "tak" tylko wtedy, gdy planujesz toomigrate tej maszyny do platformy Azure.

   - Po ustawieniu "Użyj zarządzanego dysków" za "tak", tylko zestawów dostępności w grupie zasobów hello z zestawem "Użyj zarządzanego dysków" za "tak" będzie dostępna do wyboru. Jest to spowodowane maszyn wirtualnych z dyskami zarządzanych może należeć tylko zestawów dostępności z zestawem właściwości "Użyj zarządzanego dyskami" za "Yes". Upewnij się, Utwórz zestawy dostępności z zestawem właściwości "Użyj zarządzanego dyskami" oparte na dyskach konwersji toouse zarządzane w tryb failover.  Podobnie w przypadku ustawienia "Użyj zarządzanego dysków" za "nie", tylko zestawy dostępności w grupie zasobów hello z właściwością "Użyj zarządzanego dysków" ustawiony za "nie" będzie dostępna do wyboru. [Dowiedz się więcej o dyskach zarządzanych i zestawach dostępności](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/manage-availability#use-managed-disks-for-vms-in-an-availability-set).

  > [!NOTE]
  > Jeśli konto magazynu hello używanych w przypadku replikacji została zaszyfrowana przy użyciu szyfrowania usługi magazynu w dowolnym momencie w czasie, tworzenie dysków zarządzanych w trybie failover zakończy się niepowodzeniem. Można ustawić "Użyj zarządzanego dysków" za "nie" i spróbuj ponownie pracy awaryjnej lub Wyłącz ochronę dla maszyny wirtualnej hello i chronić tooa konta magazynu, który nie był włączony w dowolnym momencie w czasie szyfrowanie usługi magazynu.
  > [Dowiedz się więcej o funkcji Szyfrowanie usługi Storage i dyskach zarządzanych](https://docs.microsoft.com/en-us/azure/storage/storage-managed-disks-overview#managed-disks-and-encryption).


## <a name="test-hello-deployment"></a>Testowe wdrożenie na powitania

Wdrażanie hello tootest możesz uruchomić test trybu failover dla jednej maszyny wirtualnej lub plan odzyskiwania, który zawiera co najmniej jednej maszyny wirtualnej.

### <a name="before-you-start"></a>Przed rozpoczęciem

 - Jeśli chcesz, aby tooAzure tooconnect maszyn wirtualnych za pomocą protokołu RDP po przejściu w tryb failover, zapoznaj się z [przygotowywanie tooconnect](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover).
 - test toofully należy toocopy usługi Active Directory i DNS w środowisku testowym. [Dowiedz się więcej](site-recovery-active-directory.md#test-failover-considerations).

### <a name="run-a-test-failover"></a>Wykonywanie próby przejścia w tryb failover

1. toofail za pośrednictwem jednej maszyny Wirtualnej w **elementy replikowane**, kliknij przycisk hello maszyny Wirtualnej > **+ testowy tryb Failover**.
2. Planowanie toofail za pośrednictwem odzyskiwania, **plany odzyskiwania**, kliknij prawym przyciskiem myszy hello planu > **testowy tryb Failover**. toocreate planu odzyskiwania [wykonaj te instrukcje](site-recovery-create-recovery-plans.md).
3. W **testowy tryb Failover**, wybierz opcję Połącz hello toowhich Azure sieci maszyn wirtualnych platformy Azure po pracy awaryjnej.
4. Kliknij przycisk **OK** toobegin hello w tryb failover. Możesz śledzić postępy, klikając na powitania wirtualna tooopen jego właściwości lub na powitania **testowy tryb Failover** zadania w **zadania usługi Site Recovery**.
5. Po zakończeniu pracy awaryjnej hello również powinno być możliwe toosee repliki hello Azure machine są wyświetlane w portalu Azure hello > **maszyn wirtualnych**. Należy upewnić się, że tej maszyny Wirtualnej hello jest hello odpowiedni rozmiar, że został podłączony toohello odpowiednią sieć i działa.
6. Przygotowanie do nawiązywania połączeń po pracy awaryjnej należy toohello tooconnect stanie maszyny Wirtualnej platformy Azure.
7. Gdy wszystko będzie gotowe, kliknij **oczyszczania testowy tryb failover** na powitania planu odzyskiwania. W **uwagi** zarejestrować i zapisać wszelkie obserwacje związane z hello testowy tryb failover. Spowoduje to usunięcie hello maszyn wirtualnych, które zostały utworzone podczas testowania trybu failover.

Aby uzyskać więcej informacji, przeczytaj hello [Test pracy awaryjnej tooAzure](site-recovery-test-failover-to-azure.md) artykułu.

## <a name="monitor-hello-deployment"></a>Monitor hello wdrożenia

Oto, jak można monitorować ustawienia konfiguracji, stanu i kondycji hello wdrażania usługi Site Recovery:

1. Polecenie hello tooaccess nazwa magazynu hello **Essentials** pulpitu nawigacyjnego. W tym pulpicie nawigacyjnym możesz wyświetlić zadania usługi Site Recovery, stan replikacji, plany odzyskiwania, kondycję serwera i zdarzenia.  Można dostosować **Essentials** tooshow hello Kafelki i układy, które są najbardziej przydatne tooyou, takich jak hello stan innych magazynów usługi Site Recovery i kopii zapasowej.

    ![Podstawy](./media/site-recovery-vmm-to-azure/essentials.png)
2. W **kondycji**, monitorowanie problemów na serwerach lokalnych (serwery VMM lub Konfiguracja) i hello zdarzenia wygenerowane przez usługę Site Recovery w hello ostatnich 24 godzin.
3. W hello **elementy replikowane**, **plany odzyskiwania**, i **zadania usługi Site Recovery** Kafelki można zarządzać i monitorować replikacji. Możesz przejść do szczegółów zadań w pozycji **Zadania** > **Zadania usługi Site Recovery**.

## <a name="command-line-installation-for-hello-azure-site-recovery-provider"></a>Instalacja wiersza polecenia dla hello dostawcy usługi Azure Site Recovery

Witaj dostawcy usługi Azure Site Recovery można zainstalować z hello wiersza polecenia. Ta metoda może być używana tooinstall hello dostawcy w rdzeniu serwera dla systemu Windows Server 2012 R2.

1. Pobierz hello dostawcy plików i rejestracji klucza tooa folder instalacji. Na przykład C:\ASR.
2. Z wiersza polecenia z podwyższonym poziomem uprawnień uruchom Instalatora dostawcy tych poleceń tooextract hello:

            C:\Windows\System32> CD C:\ASR
            C:\ASR> AzureSiteRecoveryProvider.exe /x:. /q
3. Uruchom to polecenie tooinstall hello składniki:

            C:\ASR> setupdr.exe /i
4. Następnie uruchom te polecenia, tooregister powitania serwera w magazynie hello:

        CD C:\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin
        C:\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin\> DRConfigurator.exe /r  /Friendlyname <friendly name of hello server> /Credentials <path of hello credentials file> /EncryptionEnabled <full file name toosave hello encryption certificate>       

Gdzie:

* **/ Credentials**: obowiązkowy parametr, który określa lokalizację pliku klucza rejestracji hello.  
* **/ FriendlyName**: obowiązkowy parametr dla nazwy powitania serwera hosta hello funkcji Hyper-V, która jest wyświetlana w portalu usługi Azure Site Recovery hello.
* * **/ EncryptionEnabled**: tooAzure chmur parametr opcjonalny w przypadku replikacji maszyn wirtualnych funkcji Hyper-V w programie VMM. Określ, czy tooencrypt maszynach wirtualnych platformy Azure (szyfrowanie danych w rest). Upewnij się, że hello ma nazwę pliku hello **PFX** rozszerzenia. Szyfrowanie jest domyślnie wyłączone.

    > [!NOTE]
    > Zalecane jest możliwość szyfrowania hello toouse dostarczany przez platformę Azure szyfrowanie danych magazynowanych zamiast hello szyfrowanie (opcja EncryptionEnabled) udostępniane przez usługi Azure Site Recovery. można włączyć możliwość szyfrowania Hello dostarczany przez platformę Azure dla konta magazynu i pomaga osiągnąć większą wydajność co hello szyfrowania i odszyfrowywania jest wykonywane przez platformę Azure  
    > Storage.
    > [Dowiedz się więcej o funkcji Szyfrowanie usługi Storage na platformie Azure](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption).
    
* **/ proxyaddress**: opcjonalny parametr określający adres hello powitania serwera proxy.
* **/ proxyport**: opcjonalny parametr określający port hello powitania serwera proxy.
* **/ proxyusername**: opcjonalny parametr określający nazwę użytkownika serwera proxy hello (Jeśli serwer proxy wymaga uwierzytelniania).
* **/ proxypassword**: opcjonalny parametr określający hello tooauthenticate hasła z serwera proxy (jeśli hello serwer proxy wymaga uwierzytelniania).


### <a name="network-bandwidth-considerations"></a>Zagadnienia dotyczące przepustowości sieci
Możesz użyć hello pojemności planner narzędzia toocalculate hello wymaganą przepustowość dla replikacji (Replikacja początkowa i przyrostowa). toocontrol hello ilość użycia przepustowości podczas replikacji, masz kilka opcji:

* **Ograniczanie przepustowości**: ruch funkcji Hyper-V, który replikuje tooa lokacji dodatkowej przechodzi przez konkretnego hosta funkcji Hyper-V. Można ograniczyć przepustowość na powitania serwera hosta.
* **Dostosowanie przepustowości**: możesz wywrzeć wpływ hello przepustowość dla replikacji przy użyciu kilku kluczy rejestru.

#### <a name="throttle-bandwidth"></a>Ograniczanie przepustowości
1. Otwórz hello Microsoft Azure Backup przystawka programu MMC na serwerze hosta funkcji Hyper-V hello. Domyślnie skrót do usługi Kopia zapasowa Microsoft Azure jest dostępny na pulpicie hello, lub C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.
2. W przystawce hello, kliknij przycisk **Zmień właściwości**.
3. Na powitania **ograniczania** wybierz opcję **włączyć użycia przepustowości połączenia internetowego do operacji tworzenia kopii zapasowej**i Ustaw limity hello do pracy oraz innych niż godziny pracy. Prawidłowe zakresy są od 512 KB/s too102 MB/s na sekundę.

    ![Ograniczanie przepustowości](./media/site-recovery-vmm-to-azure/throttle2.png)

Można również użyć hello [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) ograniczania tooset polecenia cmdlet. Oto przykład:

    $mon = [System.DayOfWeek]::Monday
    $tue = [System.DayOfWeek]::Tuesday
    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth  (512*1024) -NonWorkHourBandwidth (2048*1024)

**Set-OBMachineSetting -NoThrottle** wskazuje, że ograniczanie przepływności nie jest wymagane.

#### <a name="influence-network-bandwidth"></a>Wywieranie wpływu na przepustowość sieci
Witaj **UploadThreadsPerVM** formanty wartość rejestru hello liczba wątków, które są używane do transferu danych (Replikacja początkowa lub przyrostowa) dysku. Wyższa wartość zwiększa przepustowość sieci hello używanych w przypadku replikacji. Witaj **DownloadThreadsPerVM** wartość rejestru określa hello liczbę wątków używanych do transferu danych podczas powrotu po awarii.

1. W rejestrze hello Przejdź zbyt**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**.

   * Zmodyfikuj wartość hello **UploadThreadsPerVM** (lub Utwórz klucz hello, jeśli nie istnieje) toocontrol wątki używane podczas replikacji dysku.
   * Zmodyfikuj wartość hello **DownloadThreadsPerVM** (lub Utwórz klucz hello, jeśli nie istnieje) wątków toocontrol używany do ruchu powrotu po awarii z platformy Azure.
2. Witaj, wartość domyślna to 4. W sieci "o nadmiarowych zasobach" należy zmienić te klucze rejestru hello wartości domyślnych. Witaj maksymalna to 32. Monitorowanie ruchu toooptimize hello wartość.

## <a name="next-steps"></a>Następne kroki

Po zakończeniu replikacji początkowej i przetestowaniu hello wdrożenia, jak hello zajdzie taka potrzeba, można wywołać przechodzenia w tryb failover. [Dowiedz się więcej](site-recovery-failover.md) o różnych typach trybu failover i w jaki sposób toorun je.
