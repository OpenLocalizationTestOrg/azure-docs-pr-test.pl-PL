---
title: "aaaReplicate maszyn wirtualnych funkcji Hyper-V w programie VMM z siecią SAN przy użyciu usługi Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób maszyn wirtualnych funkcji Hyper-V tooreplicate między dwiema lokacjami z usługi Azure Site Recovery przy użyciu replikacji SAN."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: eb480459-04d0-4c57-96c6-9b0829e96d65
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: raynew
ms.openlocfilehash: cee4ff519a8e9e7f29e17e923a9533fb339634b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-vms-in-vmm-clouds-tooa-secondary-site-with-azure-site-recovery-by-using-san"></a>Replikowanie maszyn wirtualnych funkcji Hyper-V w lokacji dodatkowej tooa chmur programu VMM z usługą Azure Site Recovery za pomocą sieci SAN


W tym artykule należy użyć, jeśli toodeploy [usługi Azure Site Recovery](site-recovery-overview.md) toomanage replikacji maszyn wirtualnych funkcji Hyper-V (zarządzane w chmurach programu System Center Virtual Machine Manager) tooa lokacja dodatkowa programu VMM, przy użyciu usługi Azure Site Recovery w portalu klasycznym hello. W tym scenariuszu nie jest dostępna w hello nowego portalu Azure.



Po wszelkie komentarze na końcu hello w tym artykule. Uzyskaj odpowiedzi na pytania tootechnical w hello [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="why-replicate-with-san-and-site-recovery"></a>Dlaczego replikacji z sieci SAN i Site Recovery?

* Sieci SAN stanowi rozwiązanie replikacji na poziomie przedsiębiorstwa, skalowalnej, dzięki czemu lokację główną, zawierający funkcji Hyper-V z siecią SAN można replikować lokacja dodatkowa tooa jednostek LUN z sieci SAN. Magazyn jest zarządzany przez program VMM i replikacji i trybu failover jest zorkiestrowana z usługą Site Recovery.
* Usługa Site Recovery współpracuje z kilku [partnerów magazynu SAN](http://social.technet.microsoft.com/wiki/contents/articles/28317.deploying-azure-site-recovery-with-vmm-and-san-supported-storage-arrays.aspx) tooprovide replikacja za pośrednictwem protokołu Fibre Channel i iSCSI magazynu.  
* Użyj istniejącej sieci SAN infrastruktury tooprotect krytycznym aplikacje wdrożone w klastrach funkcji Hyper-V. Maszyny wirtualne mogą być replikowane jako grupa, dzięki czemu aplikacje warstwowe można pracować w trybie Failover spójnie.
* Replikacja sieci SAN zapewnia spójność replikacji między różnych warstw aplikacji przy użyciu replikacji zsynchronizowane niski RTO i cel punktu odzyskiwania, a asynchronicznego replikacji wysokiej elastyczność (w zależności od możliwości tablicy magazynu).  
* Można zarządzać magazynem sieci SAN w hello sieci szkieletowej VMM i używać SMI-S w istniejącym magazynie toodiscover programu VMM.  

Należy pamiętać, że:
- Replikacji do lokacji za pomocą sieci SAN nie jest dostępna w hello portalu Azure. Jest on dostępny tylko w portalu klasycznym hello. Nie można utworzyć nowego magazynów w portalu klasycznym hello. Istniejące magazynów, mogą być obsługiwane.
- Replikacja z tooAzure sieci SAN nie jest obsługiwana.
- Nie można zreplikować udostępnionymi dyskami Vhdx, lub jednostek logicznych (LUN), które są bezpośrednio podłączone tooVMs za pośrednictwem protokołu Fibre Channel lub iSCSI. Klastry gościa mogą być replikowane.


## <a name="architecture"></a>Architektura

![Architektura sieci SAN](./media/site-recovery-vmm-san/architecture.png)

- **Azure**: Konfigurowanie w magazynie usługi Site Recovery w portalu Azure hello.
- **Magazyn sieci SAN**: Magazyn sieci SAN jest zarządzana w hello sieci szkieletowej VMM. Dodaj dostawcę magazynu hello, utworzyć klasyfikacje magazynu i konfigurowanie pul magazynów.
- **Program VMM i funkcji Hyper-V**: zaleca się serwer programu VMM w każdej lokacji. Konfigurowanie chmur prywatnych programu VMM i umieszczenie klastrów funkcji Hyper-V w tych chmurach. Podczas wdrażania hello dostawcy usługi Azure Site Recovery jest zainstalowany na każdym serwerze programu VMM, a serwer hello jest zarejestrowany w magazynie hello. Witaj dostawca komunikuje się z replikacja toomanage usługi Site Recovery hello, trybu failover i powrotu po awarii.
- **Replikacja**: po skonfigurowaniu magazynu w programie VMM i skonfigurować replikację w usłudze Site Recovery, zachodzi replikacja między hello głównej i dodatkowej pamięci masowej. Żadne dane nie replikacji jest wysyłane tooSite odzyskiwania.
- **Tryb failover**: Włącz tryb failover w portalu usługi Site Recovery hello. Brak zerowej utraty danych w trybie failover, ponieważ replikacja jest synchroniczne.
- **Powrót po awarii**: Wstecz toofail włączyć zmiany różnicowe tootransfer replikacji odwrotnej z lokacji głównej toohello hello lokacji dodatkowej. Po ukończeniu replikacji odwrotnej można uruchomić planowanego trybu failover z tooprimary dodatkowej. Ten planowany tryb failover zatrzymuje hello repliki maszyn wirtualnych w lokacji dodatkowej hello i można je uruchomić w lokacji głównej hello.


## <a name="before-you-start"></a>Przed rozpoczęciem


**Wymagania wstępne** | **Szczegóły**
--- | ---
**Azure** |Potrzebujesz konta platformy [Microsoft Azure](https://azure.microsoft.com/). Możesz rozpocząć od [bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/). [Dowiedz się więcej](https://azure.microsoft.com/pricing/details/site-recovery/) o cenach usługi Site Recovery. Utwórz tooconfigure magazynu usługi Azure Site Recovery i Zarządzaj replikacji i trybu failover.
**VMM** | Można użyć pojedynczego serwera programu VMM i replikacji między różne chmury, ale zaleca się jeden programu VMM w lokacji głównej hello i jeden w lokacji dodatkowej hello. Przez program VMM można wdrożyć jako fizyczny lub wirtualny serwer autonomiczny lub jako klaster. <br/><br/>Serwer VMM Hello powinna działać System Center 2012 R2 lub nowszym z hello najnowszymi aktualizacjami zbiorczymi.<br/><br/> Należy co najmniej jednej chmury skonfigurowanej na powitania tooprotect i jednej chmury skonfigurowanej na serwerze VMM dodatkowej hello podstawowy serwer VMM ma toouse dla trybu failover.<br/><br/> Chmura źródłowa Hello musi zawierać co najmniej jedną grupę hostów programu VMM.<br/><br/> Wszystkie chmury VMM musi mieć zestawu profilu pojemności funkcji Hyper-V hello.<br/><br/> Aby uzyskać więcej informacji na temat konfigurowania chmur programu VMM, zobacz [wdrożenia chmury prywatnej wirtualna](https://technet.microsoft.com/en-us/system-center-docs/vmm/scenario/cloud-overview).
**Funkcja Hyper-V** | Należy co najmniej jeden klaster funkcji Hyper-V w głównych i dodatkowych chmurach VMM.<br/><br/> klaster funkcji Hyper-V źródła Hello musi zawierać co najmniej jednej maszyny wirtualnej.<br/><br/> Witaj grupę hostów programu VMM w lokacjach głównych i dodatkowych hello musi zawierać co najmniej jeden hello klastrów funkcji Hyper-V.<br/><br/>serwery funkcji Hyper-V Hello źródłowa i docelowa musi działać system Windows Server 2012 lub nowszym z hello funkcji Hyper-V roli i hello najnowsze aktualizacje zainstalowane.<br/><br/> Jeśli pracujesz w funkcji Hyper-V w klastrze i statyczne klaster oparte na adresie IP, broker klastra nie jest tworzone automatycznie. Musisz skonfigurować go ręcznie. Aby uzyskać więcej informacji, zobacz [przygotowywanie klastrów hostów funkcji Hyper-V replica](https://www.petri.com/use-hyper-v-replica-broker-prepare-host-clusters).
**Magazyn sieci SAN** | Można replikować maszyny wirtualne w klastrze gościa z magazynem channel lub iSCSI lub przy użyciu udostępnionych wirtualnych dysków twardych (vhdx).<br/><br/> Należy dwóch różnych macierzy sieci SAN: jeden w lokacji głównej hello i hello w jednej lokacji dodatkowej.<br/><br/> Infrastruktura sieciowa powinny zostać skonfigurowane między macierzami hello. Można skonfigurować komunikację równorzędną i replikacji. Licencje replikacji powinny zostać skonfigurowane zgodnie z wymaganiami tablicy magazynu hello.<br/><br/>Konfigurowanie sieci między serwerami hosta hello funkcji Hyper-V, a macierz magazynowa hello tak, aby hosty mogą się komunikować z magazynem jednostek LUN za pomocą protokołu Fibre Channel lub iSCSI.<br/><br/> Sprawdź [obsługiwanych tablic magazynowych](http://social.technet.microsoft.com/wiki/contents/articles/28317.deploying-azure-site-recovery-with-vmm-and-san-supported-storage-arrays.aspx).<br/><br/> Należy zainstalować dostawców SMI-S od producentów tablicy magazynu i hello macierzami sieci SAN mają być zarządzane przez dostawcę hello. Konfigurowanie zgodnie z instrukcjami toomanufacturer hello dostawcy.<br/><br/>Upewnij się, że tablica hello dostawcy SMI-S jest na serwerze tej hello VMM serwera mogą uzyskiwać dostęp do sieci hello przy użyciu adresu IP lub FQDN.<br/><br/> Każdej macierzy SAN powinien mieć co najmniej jeden dostępne pule magazynów.<br/><br/> Hello podstawowy serwer VMM ma zarządzać hello głównej tablicy i hello pomocniczy serwer programu VMM należy zarządzać hello dodatkowej tablicy.
**Mapowanie sieci** | Skonfiguruj mapowanie sieci, dzięki czemu replikowanych maszyn wirtualnych optymalnie są umieszczane na serwerach hostów funkcji Hyper-V dodatkowej po pracy awaryjnej i, dzięki czemu są one połączone tooappropriate sieci maszyny Wirtualnej. Jeśli nie skonfigurujesz mapowania sieci, repliki maszyn wirtualnych będzie sieci połączonych tooany po pracy awaryjnej.<br/><br/> Upewnij się, że sieci VMM są poprawnie skonfigurowane, dzięki czemu możesz skonfigurować mapowanie sieci podczas wdrażania usługi Site Recovery. W programie VMM hello maszyn wirtualnych na hoście funkcji Hyper-V źródłowym hello powinna być tooa połączonych sieci maszyny Wirtualnej programu VMM. Ta sieć powinna być tooa połączone sieci logicznej, która jest skojarzona z chmurą hello.<br/><br/> Chmura docelowa Hello powinny mieć odpowiedni sieci maszyny Wirtualnej i należy go tooa połączonego odpowiednie sieci logicznej, która jest skojarzona z hello chmurę docelową z kolei.<br/><br/>.

## <a name="step-1-prepare-hello-vmm-infrastructure"></a>Krok 1: Przygotowanie infrastruktury VMM hello
tooprepare infrastruktury programu VMM należy:

1. Sprawdź chmur programu VMM.
2. Integracja i ich klasyfikację magazynu sieci SAN w programie VMM.
3. Utwórz jednostki LUN i przydzielania magazynu.
4. Utwórz grupy replikacji.
5. Skonfiguruj sieci maszyn wirtualnych.

### <a name="verify-vmm-clouds"></a>Sprawdź chmur programu VMM

Upewnij się, że Twoje chmur programu VMM zostały ustawione prawidłowo przed rozpoczęciem wdrażania usługi Site Recovery.

### <a name="integrate-and-classify-san-storage-in-hello-vmm-fabric"></a>Integracja i ich klasyfikację magazynu sieci SAN w hello sieci szkieletowej VMM

1. W konsoli programu VMM hello Przejdź zbyt**sieci szkieletowej** > **magazynu** > **Dodaj zasoby** > **urządzeń magazynujących**.
2. W hello **dodawania urządzeń magazynujących** kreatora wybierz **wybierz typ dostawcy magazynu** i wybierz **sieci SAN i NAS oddnalezione i zarządzane przez dostawcę SMI-S**.

    ![Typ dostawcy](./media/site-recovery-vmm-san/provider-type.png)

3. Na powitania **Określ protokół i adres dostawcy SMI-S magazynu hello** wybierz pozycję **CIMXML SMI-S** i określ ustawienia hello łączącego toohello dostawcy.
4. W **dostawcy IP lub nazwa FQDN** i **portu TCP/IP**, określ ustawienia hello łączącego toohello dostawcy. Połączenie SSL można użyć tylko dla CIMXML SMI-S.

    ![Połącz dostawcy](./media/site-recovery-vmm-san/connect-settings.png)
5. W **konto Uruchom jako**, określ konto Uruchom jako programu VMM, który można uzyskać dostępu do dostawcy hello lub utworzyć konto.
6. Na powitania **Zbierz informacje** strony, program VMM spróbuje automatycznie toodiscover, a następnie zaimportuj hello informacje o urządzeniu magazynu. tooretry odnajdywania, kliknij przycisk **dostawca skanowania**. Jeśli proces odnajdywania hello zakończy się powodzeniem, czy tablic magazynowych, pule magazynu, producenta, model i pojemność są wyświetlane na stronie powitania odnalezionymi hello.

    ![Odnajdywanie magazynu](./media/site-recovery-vmm-san/discover.png)
7. W **wybierz tooplace pule magazynu w obszarze Zarządzanie i przypisz klasyfikację**, wybierz pule magazynów hello, czy program VMM zarządzania i przypisz klasyfikację. Informacje o jednostce LUN zostaną zaimportowane z pul magazynów hello. Tworzenie jednostki LUN na podstawie na aplikacji hello należy tooprotect, ich wymagania dotyczące pojemności i wymagań dla siebie niezbędne tooreplicate.

    ![Klasyfikowanie magazynu](./media/site-recovery-vmm-san/classify.png)

### <a name="create-luns-and-allocate-storage"></a>Tworzenie jednostek LUN i przydzielania magazynu

Tworzenie jednostki LUN na podstawie na aplikacji hello należy tooprotect, wymagania dotyczące pojemności i wymagań dla siebie niezbędne tooreplicate.

1. Po wyświetleniu magazynu hello hello sieci szkieletowej VMM, możesz [udostępniania jednostek LUN](https://technet.microsoft.com/en-us/system-center-docs/vmm/manage/manage-storage-host-groups#create-a-lun-in-vmm).

     > [!NOTE]
     > Nie dodawaj dysków VHD dla maszyny Wirtualnej, które zostały włączone dla replikacji tooLUNs hello. Jeśli w lokacji odzyskiwania grupy replikacji nie ma tych jednostek LUN, nie zostanie wykryty przez usługę Site Recovery.
     >

2. Przydziel klastra hostów funkcji Hyper-V toohello pojemności magazynu, aby program VMM można wdrożyć magazyn toohello udostępniane dane maszyny wirtualnej:

   * Przed przydzielania magazynu toohello klastra, należy tooallocate go toohello VMM grupy hostów na które hello klastra. Aby uzyskać więcej informacji, zobacz [jak grupy w programie VMM hostów tooa jednostki logiczne magazynu tooallocate](https://technet.microsoft.com/library/gg610686.aspx) i [jak tooa grupy hostów w programie VMM do puli magazynu tooallocate](https://technet.microsoft.com/library/gg610635.aspx).
   * Przydziel klastra toohello pojemności magazynu, zgodnie z opisem w [jak klastra tooconfigure magazynu na hoście funkcji Hyper-V w programie VMM](https://technet.microsoft.com/library/gg610692.aspx).

    ![Typ dostawcy](./media/site-recovery-vmm-san/provider-type.png)
3. W **Określ protokół i adres dostawcy SMI-S magazynu hello**, wybierz pozycję **CIMXML SMI-S**. Określ ustawienia hello podłączania toohello dostawcy. Połączenie SSL można użyć tylko w przypadku CIMXML SMI-S.

    ![Połącz dostawcy](./media/site-recovery-vmm-san/connect-settings.png)
4. W **konto Uruchom jako**, określ konto Uruchom jako programu VMM, który można uzyskać dostępu do dostawcy hello lub utworzyć konto.
5. W **Zbierz informacje**, program VMM spróbuje automatycznie toodiscover, a następnie zaimportuj hello informacje o urządzeniu magazynu. Jeśli potrzebujesz tooretry kliknij **dostawca skanowania**. Gdy proces odnajdywania hello zakończy się powodzeniem, tablic magazynowych hello, pule magazynów, producenta, model i pojemność są wyświetlane na stronie powitania.

    ![Odnajdywanie magazynu](./media/site-recovery-vmm-san/discover.png)
7. W **wybierz tooplace pule magazynu w obszarze Zarządzanie i przypisz klasyfikację**, wybierz pule magazynów hello, czy program VMM zarządzać i przypisz klasyfikację. Informacje o jednostce LUN zostaną zaimportowane z pul magazynów hello.

    ![Klasyfikowanie magazynu](./media/site-recovery-vmm-san/classify.png)


### <a name="create-replication-groups"></a>Utwórz grupy replikacji

Utwórz grupę replikacji, która zawiera wszystkie jednostki LUN hello, które będą potrzebne tooreplicate ze sobą.

1. W konsoli programu VMM hello Otwórz hello **grup replikacji** kartę właściwości tablicy magazynu hello, a następnie kliknij przycisk **nowy**.
2. Utwórz grupę replikacji hello.

    ![Grupa replikacji sieci SAN](./media/site-recovery-vmm-san/rep-group.png)

### <a name="set-up-networks"></a>Konfigurowanie sieci

Jeśli chcesz mapowania sieci tooconfigure hello następujące:

1. Zobacz Mapowanie sieci usługi Site Recovery.
2. Przygotuj sieci maszyn wirtualnych w programie VMM:

   * [Skonfiguruj sieci logiczne](https://technet.microsoft.com/en-us/system-center-docs/vmm/manage/manage-network-logical-networks).
   * [Skonfiguruj sieci maszyn wirtualnych](https://technet.microsoft.com/en-us/system-center-docs/vmm/manage/manage-network-vm-networks).


## <a name="step-2-create-a-vault"></a>Krok 2: Tworzenie magazynu

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com) z serwera VMM hello ma tooregister w magazynie hello.
2. Rozwiń węzeł **usług danych** > **usług odzyskiwania**, a następnie kliknij przycisk **magazynie usługi Site Recovery**.
3. Kliknij pozycje **Utwórz nowe** > **Szybkie tworzenie**.
4. W **nazwa**, wprowadź przyjazną nazwę tooidentify hello magazynu.
5. W **Region**, wybierz hello region geograficzny magazynu hello. toocheck obsługiwane regiony, zobacz [szczegóły cennika usługi Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).
6. Kliknij pozycję **Utwórz magazyn**.

    ![Nowy magazyn](./media/site-recovery-vmm-san/create-vault.png)

Sprawdź, czy hello tooconfirm paska stanu, który hello magazynu został pomyślnie utworzony. Witaj magazyn będzie wyświetlany jako **Active** na powitania głównego **usług odzyskiwania** strony.

### <a name="register-hello-vmm-servers"></a>Rejestrowanie serwerów VMM hello

1. Otwórz hello **Szybki Start** strony z hello **usług odzyskiwania** strony. Szybki Start można również otworzyć w dowolnym momencie, wybierając ikonę hello.

    ![Ikona Szybki start](./media/site-recovery-vmm-san/quick-start-icon.png)
2. W polu listy rozwijanej hello, wybierz **między funkcją Hyper-V lokalnej lokacji przy użyciu replikacji tablicy**.

    ![Klucz rejestracji](./media/site-recovery-vmm-san/select-san.png)
3. W **Przygotowanie serwerów programu VMM**, Pobierz najnowszą wersję pliku instalacyjnego dostawcy usługi Azure Site Recovery hello hello.
4. Uruchom ten plik na źródłowym serwerze programu VMM hello. Jeśli program VMM jest wdrożony w klastrze i instalujesz hello dostawcy dla powitania po raz pierwszy, zainstaluj hello dostawcy na aktywnym węźle i Zakończ hello instalacji tooregister hello serwer VMM w magazynie hello. Następnie zainstaluj hello dostawcy na powitania innych węzłów. Jeśli uaktualniasz hello dostawcy należy tooupgrade we wszystkich węzłach, dzięki czemu mają one hello sama wersja dostawcy.
5. Witaj Instalator sprawdza wymagania i żądania uprawnień toostop hello Instalatora dostawcy toobegin usługi VMM. Usługa Hello zostanie automatycznie uruchomiona po zakończeniu instalacji. W klastrze programu VMM będzie roli klastra zostanie wyświetlony monit o toostop hello.
6. W **Microsoft Update**, można włączyć aktualizacje i aktualizacje dostawcy będą instalowane zgodnie z zasadami Microsoft Update tooyour.

    ![Usługa Microsoft Updates](./media/site-recovery-vmm-san/ms-update.png)

7. Domyślnie jest lokalizacja instalacji hello hello dostawcy <SystemDrive>\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin. Kliknij przycisk **zainstalować** toobegin.

    ![Lokalizacja instalacji](./media/site-recovery-vmm-san/install-location.png)

8. Po zainstalowaniu dostawcy powitania kliknij **zarejestrować** tooregister hello menedżerem maszyny wirtualnej w magazynie hello.

    ![Instalacja ukończona](./media/site-recovery-vmm-san/install-complete.png)

9. W **połączenia internetowego**, określ, jak hello dostawcy łączy toohello Internet. Wybierz **Użyj domyślnych ustawień serwera proxy systemu** Jeśli chcesz toouse hello domyślnych ustawień połączenia internetowego na powitania serwera.

    ![Ustawienia internetowe](./media/site-recovery-vmm-san/proxy-details.png)

   * Jeśli toouse niestandardowego serwera proxy, należy je skonfigurować przed zainstalowaniem hello dostawcy. Podczas konfigurowania niestandardowych ustawień serwera proxy połączenia serwera proxy hello toocheck uruchomienia testów.
   * Jeśli używasz niestandardowego serwera proxy lub domyślny serwer proxy wymaga uwierzytelniania, należy wprowadź szczegóły serwera proxy hello, w tym hello adres i port.
   * Witaj wymagane adresy URL powinien być dostępny z serwera VMM hello.
   * Jeśli używasz niestandardowego serwera proxy konto Uruchom jako programu VMM (DRAProxyAccount) jest tworzona automatycznie przy użyciu hello określonych poświadczeń serwera proxy. Skonfiguruj serwer proxy hello, aby mógł uwierzytelnić tego konta. Można zmodyfikować hello Uruchom jako ustawienia konta w konsoli programu VMM hello (**ustawienia** > **zabezpieczeń** > **konta Uruchom jako**  >  **Konta DRAProxyAccount**). Należy ponownie uruchomić usługę VMM hello hello zmiany tootake efektu.
10. W **klucz rejestracji**, wybierz pozycję hello klucza, który został pobrany z serwera VMM w portalu i skopiowanego toohello hello.
11. W **nazwę magazynu**, sprawdź nazwę hello hello magazynu, w którym hello serwer zostanie zarejestrowany.

    ![Rejestracja serwera](./media/site-recovery-vmm-san/vault-creds.png)
12. ustawienie szyfrowania Hello jest używana tylko dla programu VMM tooAzure replikacji. Można je zignorować.

    ![Rejestracja serwera](./media/site-recovery-vmm-san/encrypt.png)
13. W **nazwy serwera**, określ serwer VMM hello tooidentify przyjazną nazwę w magazynie hello. W konfiguracji klastra Określ nazwę roli klastra VMM hello.
14. W **synchronizacja metadanych chmury początkowego**, wybierz, czy dla wszystkich chmur na serwerze VMM hello toosynchronize metadanych. Ta akcja wymaga tylko toohappen raz na każdym serwerze. Jeśli nie chcesz toosynchronize wszystkich chmur, można zaznaczać tego ustawienia i synchronizować poszczególne chmury indywidualnie WE hello właściwości chmury w konsoli programu VMM hello.

    ![Rejestracja serwera](./media/site-recovery-vmm-san/friendly-name.png)

15. Kliknij przycisk **dalej** toocomplete hello procesu. Po rejestracji metadane z serwera VMM hello są pobierane przez usługę Azure Site Recovery. Serwer Hello jest wyświetlany w **serwerów** > **serwery VMM** w magazynie hello.

### <a name="command-line-installation"></a>Instalacja wiersza polecenia

Witaj dostawcy usługi Azure Site Recovery można również zainstalować przy użyciu hello następującego wiersza polecenia. Ta metoda może być używana tooinstall hello dostawcy w rdzeniu serwera dla systemu Windows Server 2012 R2.

1. Pobierz hello dostawcy plików i rejestracji klucza tooa folder instalacji. Na przykład C:\ASR.
2. Zatrzymaj usługę VMM hello.
3. Wyodrębnij Instalatora dostawcy hello. Uruchom następujące polecenia jako administrator:

        C:\Windows\System32> CD C:\ASR
        C:\ASR> AzureSiteRecoveryProvider.exe /x:. /q
4. Zainstaluj hello dostawcy:

        C:\ASR> setupdr.exe /i
5. Zarejestruj hello dostawcy:

        CD C:\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin
        C:\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin\> DRConfigurator.exe /r  /Friendlyname <friendly name of hello server> /Credentials <path of hello credentials file> /EncryptionEnabled <full file name toosave hello encryption certificate>         

Parametry:

* **/ Credentials**: wymagany parametr hello lokalizacji, w których hello znajduje się plik klucza rejestracji.  
* **/ FriendlyName**: wymagany parametr dla nazwy powitania serwera hosta hello funkcji Hyper-V, która jest wyświetlana w portalu usługi Azure Site Recovery hello.
* **/ EncryptionEnabled**: parametr opcjonalny używany tylko podczas replikowania z tooAzure programu VMM.
* **/ proxyaddress**: opcjonalny parametr określający adres hello powitania serwera proxy.
* **/ proxyport**: opcjonalny parametr określający port hello powitania serwera proxy.
* **/ proxyusername**: opcjonalny parametr określający nazwę użytkownika serwera proxy hello (jeśli hello serwer proxy wymaga uwierzytelniania).
* **/ proxypassword**: opcjonalny parametr określający hasło hello w celu uwierzytelniania z serwerem proxy hello (jeśli hello serwer proxy wymaga uwierzytelniania).

## <a name="step-3-map-storage-arrays-and-pools"></a>Krok 3: Mapowanie tablic magazynowych i pule

Które puli magazynów pomocniczego odbiera dane replikacji z puli głównej hello toospecify tablice podstawowych i pomocniczych mapy. Mapy magazynu, przed skonfigurowaniem replikacji, ponieważ informacje o mapowaniu hello jest używany po włączeniu ochrony dla grupy replikacji.

Przed rozpoczęciem należy sprawdzić, czy chmur programu VMM są wyświetlane w magazynie hello. Chmury są wykrywane po zsynchronizowaniu wszystkich chmur podczas instalacji dostawcy lub podczas synchronizacji w konsoli programu VMM hello określonej chmury.

1. Kliknij przycisk **zasobów** > **magazynu serwera** > **mapy źródłowej i docelowej tablic**.
    ![Rejestracja serwera](./media/site-recovery-vmm-san/storage-map.png)

2. Wybierz macierze magazynowe hello w lokacji głównej hello i zamapowania ich tablice toostorage w lokacji dodatkowej hello. W **pule magazynów**, wybierz źródło i docelowych toomap puli magazynu.

    ![Rejestracja serwera](./media/site-recovery-vmm-san/storage-map-pool.png)

## <a name="step-4-configure-replication-settings"></a>Krok 4: Konfigurowanie ustawień replikacji

Po zarejestrowanych serwerów programu VMM, należy skonfigurować ustawienia ochrony chmury.

1. Na powitania **Szybki Start** kliknij przycisk **Konfigurowanie ochrony dla chmur programu VMM**.
2. Na powitania **chronione elementy** , a następnie wybierz chmury hello **konfiguracji**.
3. W **docelowej**, wybierz pozycję **VMM**.
4. W **lokalizacja docelowa**, wybierz pozycję powitania serwera VMM, który zarządza hello chmurę toouse odzyskiwania.
5. W **Target chmury**, wybierz chmurę docelową hello mają toouse dla trybu failover maszyny Wirtualnej.
   * Zaleca się, że wybierz chmurę docelową, który spełnia wymagania odzyskiwania hello maszyn wirtualnych, które można chronić.
   * Chmury mogą należeć tylko pary chmur pojedynczego tooa — jako podstawowego lub chmurę docelową.
6. Usługa Site Recovery sprawdza, czy chmur mają dostęp do magazynu tooSAN i tego magazynu hello tablice są zamapowane.
7. Jeśli weryfikacja zakończy się pomyślnie, w **typ replikacji**, wybierz pozycję **SAN**.

Po zapisaniu ustawień hello utworzono zadanie, która może być monitorowane na powitania **zadania** kartę. Ustawienia można zmodyfikować na powitania **Konfiguruj** kartę. Chcąc lokalizacji docelowej hello toomodify lub docelowej chmury, musisz usunąć konfiguracji chmury hello i ponownie skonfigurować chmurę hello.

## <a name="step-5-enable-network-mapping"></a>Krok 5: Włączanie mapowania sieci

1. Na powitania **Szybki Start** kliknij przycisk **Mapuj sieci**.
2. Wybierz hello źródłowym serwerze programu VMM, a następnie wybierz hello docelowy VMM toowhich powitania serwera sieci zostanie zamapowana. Lista Hello źródła sieci i ich skojarzonych docelowego są wyświetlane. Wartość pusta jest wyświetlany w sieciach, które nie są zamapowane. Kliknij przycisk hello informacji ikona dalej toohello źródłowa i docelowa nazwy tooview hello podsieci dla każdej sieci.
3. Wybierz sieć w **sieci w źródle**, a następnie kliknij przycisk **mapy**. Usługa Hello hello sieci maszyn wirtualnych na serwerze docelowym hello wykrywa i wyświetla je.

    ![Architektura sieci SAN](./media/site-recovery-vmm-san/network-map1.png)
4. Wybierz jedną z sieci maszyny Wirtualnej hello z hello docelowym serwerze VMM.

    ![Architektura sieci SAN](./media/site-recovery-vmm-san/network-map2.png)

5. Po wybraniu Sieć docelowa hello liczba chronionych chmur używających Sieć źródłowa hello są wyświetlane. Wyświetlana jest również dostępnych sieci. Zaleca się, że wybrano sieci docelowej, która jest dostępna tooall hello chmur, używaną do replikacji.
6. Kliknij przycisk hello — proces mapowania hello toocomplete znacznik wyboru. Uruchomienia zadania, który śledzi postęp. Możesz je wyświetlić na powitania **zadania** kartę.

## <a name="step-6-enable-replication-for-replication-groups"></a>Krok 6: Włączanie replikacji dla grupy replikacji

Aby włączyć ochronę maszyn wirtualnych, należy tooenable replikacji dla grupy replikacji magazynu.

1. Na powitania **właściwości** strony hello chmury podstawowej w portalu usługi Site Recovery hello, otwórz hello **maszyn wirtualnych** i kliknij polecenie **Dodaj grupę replikacji**.
2. Wybierz co najmniej jedną grupę replikacji programu VMM, skojarzonych z chmurą hello Sprawdź hello tablice źródłowa i docelowa, a następnie wybierz częstotliwość replikacji hello.

Usługa Site Recovery, VMM i dostawców SMI-S hello udostępnić hello numerów LUN magazynu lokacji docelowej i Włącz replikacji magazynu. Jeśli został już zreplikowany hello grupy replikacji, Site Recovery ponownie używa hello istniejącej relacji replikacji i aktualizacje hello informacji.

## <a name="step-7-enable-protection-for-virtual-machines"></a>Krok 7: Włączanie ochrony dla maszyn wirtualnych


Podczas replikowania jest grupą magazynów, należy włączyć ochronę maszyn wirtualnych w konsoli programu VMM hello z jedną z następujących metod hello:

* **Nowa maszyna wirtualna**: podczas tworzenia maszyny Wirtualnej, Włącz replikację i skojarzyć z grupą replikacji hello hello maszyny Wirtualnej.
  Po wybraniu tej opcji program VMM używa magazynu maszyny Wirtualnej hello inteligentnego umieszczania toooptimally miejsce na jednostkach LUN hello hello grupy replikacji. Usługa Site Recovery organizuje hello tworzenia maszyny Wirtualnej w lokacji dodatkowej hello cienia i przydziela pojemności, dzięki czemu będzie można uruchomić repliki maszyn wirtualnych po pracy awaryjnej.
* **Istniejącej maszyny wirtualnej**: Jeśli maszyna wirtualna została już wdrożona w programie VMM, można włączyć replikację i wykonywać grupą replikacji tooa magazynu migracji. Po zakończenia, program VMM i Usługa Site Recovery wykryć hello nowej maszyny Wirtualnej i rozpocząć zarządzanie go w usłudze Site Recovery. Cienia w lokacji dodatkowej hello zostanie utworzona maszyna wirtualna, a miejsce jest przydzielane, więc ta replika hello maszyna wirtualna może zostać uruchomiona po pracy awaryjnej.

![Włączanie ochrony](./media/site-recovery-vmm-san/enable-protect.png)

Po włączeniu replikacji maszyn wirtualnych są wyświetlane w konsoli usługi Site Recovery hello. Można wyświetlić właściwości maszyny Wirtualnej, śledzić stan i śledzić trybu failover grupy replikacji, które zawierają wiele maszyn wirtualnych. W ramach replikacji sieci SAN wszystkich maszyn wirtualnych, które skojarzono z grupą replikacji musi przełączyć razem. Jest to spowodowane pracy awaryjnej w warstwie magazynu hello najpierw. Jest ważne toogroup Twojego replikacji grupy poprawnie i umieścić tylko maszyny wirtualne skojarzony ze sobą.

> [!NOTE]
> Po włączeniu replikacji dla maszyny Wirtualnej, nie dodawaj tooLUNs jej wirtualne dyski twarde, chyba że znajdują się w grupie replikacji usługi Site Recovery. Wirtualne dyski twarde zostanie wykryty przez usługę Site Recovery tylko, jeśli znajdują się w grupie replikacji usługi Site Recovery.
>
>

Możesz śledzić postępy, w tym hello replikacji początkowej na powitania **zadania** kartę. Po uruchomieniu zadania zakończenia ochrony hello hello maszyna wirtualna jest gotowa do pracy awaryjnej.

![Zadanie ochrony maszyny wirtualnej](./media/site-recovery-vmm-san/job-props.png)

## <a name="step-8-test-hello-deployment"></a>Krok 8: Testowanie wdrożenia hello

Testowanie sieci toomake wdrożenia się powyżej zgodnie z oczekiwaniami niepowodzenie maszyn wirtualnych. toodo, to utworzyć plan odzyskiwania i testować tryb failover.

1. Na powitania **plany odzyskiwania** , kliknij pozycję **Utwórz Plan odzyskiwania**.
2. Określ nazwę hello planu odzyskiwania, a następnie wybierz serwerach VMM źródłowych i docelowych. Serwer źródłowy Hello musi mieć maszyn wirtualnych, które są włączone dla trybu failover i odzyskiwania. Wybierz **SAN** tooview tylko chmury, które są skonfigurowane do replikacji sieci SAN.

    ![Tworzenie planu odzyskiwania](./media/site-recovery-vmm-san/r-plan.png)

3. W **wybierz maszyny wirtualne**, wybierz grupy replikacji. Wszystkie maszyny wirtualne skojarzone z grupą hello są dodawane toohello planu odzyskiwania. Te maszyny wirtualne są dodawane toohello odzyskiwania planu domyślnej grupy (Grupa 1). W razie potrzeby można dodać więcej grup. Po replikacji maszyny wirtualne są numerowane według kolejności toohello grup hello planu odzyskiwania.

    ![Wybierz maszyny wirtualne](./media/site-recovery-vmm-san/r-plan-vm.png)
4. Po utworzeniu planu odzyskiwania hello pojawia się na liście hello na powitania **plany odzyskiwania** kartę. Wybierz hello plan, a **testowy tryb Failover**.
5. Na powitania **potwierdzić testowy tryb Failover** wybierz pozycję **Brak**. Po włączeniu tej opcji hello przejścia w tryb failover maszyn wirtualnych replik nie będzie tooany połączonych sieci. Testuje tego powitalne maszyn wirtualnych w tryb failover zgodnie z oczekiwaniami, ale nie sprawdza hello środowiska sieciowego. Aby uzyskać więcej informacji na temat innych opcji sieciowych, zobacz [trybu failover Usługa Site Recovery](site-recovery-failover.md).

    ![Wybierz test sieci](./media/site-recovery-vmm-san/test-fail1.png)

6. Hello testowej maszyny Wirtualnej jest tworzona na powitania sam hosta jako hello hosta, na którym replika hello znajduje się maszyna wirtualna. Chmura toohello, w których hello znajduje się maszyna wirtualna repliki nie jest dodawany.
2. Po replikacji hello repliki maszyny Wirtualnej ma inny adres IP niż hello podstawowej maszyny wirtualnej. Jeśli adresy wystawiania z serwera DHCP, zostaną automatycznie zaktualizowane. Jeśli nie używasz protokołu DHCP, hello same adresy, należy toorun kilka skryptów.
3. Uruchom ten skrypt tooretrieve hello adres IP:

       $vm = Get-SCVirtualMachine -Name <VM_NAME>
       $na = $vm[0].VirtualNetworkAdapters>
       $ip = Get-SCIPAddress -GrantToObjectID $na[0].id
       $ip.address  

4. Uruchom ten przykładowy skrypt tooupdate DNS. Określ adres IP hello, który można pobrać.

       [string]$Zone,
       [string]$name,
       [string]$IP
       )
       $Record = Get-DnsServerResourceRecord -ZoneName $zone -Name $name
       $newrecord = $record.clone()
       $newrecord.RecordData[0].IPv4Address  =  $IP
       Set-DnsServerResourceRecord -zonename $zone -OldInputObject $record -NewInputObject $Newrecord


## <a name="next-steps"></a>Następne kroki

Po uruchomieniu testu toocheck trybu failover, czy działa środowisko zgodnie z oczekiwaniami, zobacz [trybu failover Usługa Site Recovery](site-recovery-failover.md) toolearn o różnych typach trybu failover.
