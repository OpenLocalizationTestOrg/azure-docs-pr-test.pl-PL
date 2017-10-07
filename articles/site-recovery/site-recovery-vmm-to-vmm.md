---
title: "lokacja dodatkowa tooa maszyn wirtualnych funkcji Hyper-V aaaReplicate z usługi Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak tooreplicate maszyn wirtualnych funkcji Hyper-V w VMM chmur tooa dodatkowej VMM lokacji przy użyciu hello portalu Azure."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: b33a1922-aed6-4916-9209-0e257620fded
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: raynew
ms.openlocfilehash: e79dbdeab74266e843e5146298dc5aadfe66b5df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooa-secondary-vmm-site-using-hello-azure-portal"></a>Replikowanie maszyn wirtualnych funkcji Hyper-V w VMM chmur tooa lokacja dodatkowa programu VMM przy użyciu hello portalu Azure
> [!div class="op_single_selector"]
> * [Witryna Azure Portal](site-recovery-vmm-to-vmm.md)
> * [Portal klasyczny](site-recovery-vmm-to-vmm-classic.md)
> * [Program PowerShell — model usługi Resource Manager](site-recovery-vmm-to-vmm-powershell-resource-manager.md)
>
>

W tym artykule opisano sposób tooreplicate lokalnych maszyn wirtualnych funkcji Hyper-V zarządzane w chmurach programu System Center Virtual Machine Manager (VMM) przy użyciu lokacji dodatkowej tooa [usługi Azure Site Recovery](site-recovery-overview.md) w hello portalu Azure. Dowiedz się więcej na ten temat [architektura scenariusza](site-recovery-components.md).

Po przeczytaniu tego artykułu, post wszelkie komentarze u dołu hello, lub na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="prerequisites"></a>Wymagania wstępne

**Wymagania wstępne** | **Szczegóły**
--- | ---
**Azure** | Potrzebujesz konta platformy [Microsoft Azure](http://azure.microsoft.com/). Możesz rozpocząć od [bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/). [Dowiedz się więcej](https://azure.microsoft.com/pricing/details/site-recovery/) o cenach usługi Site Recovery.
**Program VMM lokalnej** | Firma Microsoft zaleca się, że masz dwoma serwerami VMM, w lokacji głównej hello i jeden w hello dodatkowej.<br/><br/> Umożliwia replikację między chmurami na jednym serwerze programu VMM.<br/><br/> Serwery VMM powinna być uruchomiona co najmniej System Center 2012 SP1 z najnowszymi aktualizacjami hello.<br/><br/> Serwery VMM wymagają dostępu do Internetu.
**Chmury VMM** | Każdy serwer VMM musi dysponować co najmniej jedną chmurę, a wszystkie chmury musi mieć zestawu profilu pojemności funkcji Hyper-V hello. <br/><br/>Chmury muszą zawierać co najmniej jedną grupę hostów programu VMM.<br/><br/> Jeśli masz tylko jeden serwer VMM, wymaga co najmniej dwa chmur, tooact jako podstawowego i pomocniczego.
**Funkcja Hyper-V** | Serwery funkcji Hyper-V musi działać co najmniej Windows Server 2012 z rolą hello funkcji Hyper-V, i mieć hello zainstalowane najnowsze aktualizacje.<br/><br/> Serwer funkcji Hyper-V powinien zawierać co najmniej jedną maszynę wirtualną.<br/><br/>  Serwery hosta funkcji Hyper-V powinien znajdować się w grupach hostów w hello głównych i dodatkowych chmurach VMM.<br/><br/> Po uruchomieniu funkcji Hyper-V w klastrze systemu Windows Server 2012 R2 zainstaluj [zaktualizować 2961977](https://support.microsoft.com/kb/2961977)<br/><br/> Po uruchomieniu w systemie Windows Server 2012 Hyper-V w klastrze, broker klastra nie jest tworzony automatycznie w przypadku statycznej klastra oparte na adresie IP. Należy ręcznie skonfigurować hello brokera klastra. [Dowiedz się więcej](http://social.technet.microsoft.com/wiki/contents/articles/18792.configure-replica-broker-role-cluster-to-cluster-replication.aspx).<br/><br/> Serwery funkcji Hyper-V wymagają dostępu do Internetu.
**Adresy URL** | Serwery VMM i hosty funkcji Hyper-V powinny być możliwe tooreach tych adresów URL:<br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]

## <a name="deployment-steps"></a>Kroki wdrażania

Oto, co należy zrobić:

1. Sprawdź wymagania wstępne.
2. Przygotuj hello serwer VMM i hosty funkcji Hyper-V.
3. Utwórz magazyn usługi Recovery Services. Magazyn Hello zawiera ustawienia konfiguracji i organizuje replikację.
4. Określ ustawienia źródła i celu oraz replikacji.
5. Wdrażanie hello usługi mobilności na maszynach wirtualnych, które mają tooreplicate.
6. Przygotowanie do replikacji, a następnie włączyć replikację dla maszyn wirtualnych funkcji Hyper-V.
7. Uruchom test toomake trybu failover, się, że wszystko działa zgodnie z oczekiwaniami.

## <a name="prepare-vmm-servers-and-hyper-v-hosts"></a>Przygotowanie serwerów programu VMM i hosty funkcji Hyper-V

tooprepare wdrożenia:

1. Sprawdź, czy serwer VMM hello i hosty funkcji Hyper-V są zgodne z hello wymagania wstępne opisane powyżej i może osiągnąć adresy URL hello wymagane.
2. Konfigurowanie sieci programu VMM, dzięki czemu można skonfigurować [mapowania sieci](#network-mapping-overview).

    - Upewnij się, że maszyny wirtualne w źródle powitania serwera hosta funkcji Hyper-V są tooa połączonych sieci maszyny Wirtualnej VMM. Ta sieć powinna być tooa połączone sieci logicznej, która jest skojarzona z chmurą hello.
    Sprawdź, czy chmura dodatkowej hello używanego do odzyskiwania ma skonfigurowane odpowiednie sieci maszyny Wirtualnej. Ta sieć maszyn wirtualnych powinny być tooa połączone sieci logicznej, która ma powiązanego z chmurą dodatkowej hello.

3. Przygotowanie do [pojedynczy serwer wdrażania](#single-vmm-server-deployment), jeśli chcesz, aby maszyny wirtualne tooreplicate między chmurami na powitania tego samego serwera VMM.

## <a name="create-a-recovery-services-vault"></a>Tworzenie magazynu Usług odzyskiwania
1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).
2. Kliknij kolejno pozycje **Nowy** > **Zarządzanie** > **Usługi odzyskiwania**.
3. W **nazwa**, określ przyjazną nazwę tooidentify hello magazynu. Jeśli masz więcej niż jedną subskrypcję, wybierz jedną z nich.
4. [Utwórz grupę zasobów](../azure-resource-manager/resource-group-template-deploy-portal.md) lub wybierz istniejącą. Określ region platformy Azure. Komputery są replikowane toothis regionu. toocheck obsługiwane regiony, zobacz dotyczącą dostępności geograficznej w [szczegóły cennika usługi Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/)
5. Tooquickly dostępu hello magazynu z hello pulpitu nawigacyjnego, kliknij przycisk **toodashboard numeru Pin** > **Utwórz magazyn**.

    ![Nowy magazyn](./media/site-recovery-vmm-to-vmm/new-vault-settings.png)

na powitania pojawi się nowy magazyn Hello **pulpitu nawigacyjnego**w **wszystkie zasoby**, a na powitania głównego **Magazyny usług odzyskiwania** bloku.


## <a name="choose-a-protection-goal"></a>Wybierz cel ochrony

Wybierz, co ma tooreplicate i miejscu tooreplicate do.

2. Kliknij przycisk **usługi Site Recovery** > **krok 1: Przygotowanie infrastruktury** > **cel ochrony**.
3. Wybierz **lokacji toorecovery**i wybierz **tak, z funkcją Hyper-V**.
4. Wybierz **tak** tooindicate używasz hostów funkcji Hyper-V hello toomanage programu VMM.
5. Wybierz **tak** Jeśli pomocniczy serwer programu VMM. Jeśli wdrażasz replikacji między chmurami na jednym serwerze programu VMM, kliknij przycisk **nr**. Następnie kliknij przycisk **OK**.

    ![Wybieranie celów](./media/site-recovery-vmm-to-vmm/choose-goals.png)

## <a name="set-up-hello-source-environment"></a>Konfigurowanie środowiska źródłowego hello

Zainstalować hello dostawcy usługi Azure Site Recovery na serwerach VMM i Odnajdź i Zarejestruj serwer w magazynie hello.

1. Kliknij przycisk **krok 1: Przygotowanie infrastruktury** > **źródła**.

    ![Konfiguracja źródła](./media/site-recovery-vmm-to-vmm/goals-source.png)
2. W **Przygotuj źródło**, kliknij przycisk **+ VMM** tooadd serwera programu VMM.

    ![Konfiguracja źródła](./media/site-recovery-vmm-to-vmm/set-source1.png)
3. W **Dodaj serwer**, sprawdź, czy **serwera programu System Center VMM** pojawia się w **typ serwera** , że serwer VMM hello spełnia hello [wymagania wstępne](#prerequisites).
4. Pobierz plik instalacyjny dostawcy usługi Azure Site Recovery hello.
5. Pobierz klucz rejestracji hello. Będzie on potrzebny po uruchomieniu Instalatora. klucz Hello jest ważny przez pięć dni po jego wygenerowaniu.

    ![Konfiguracja źródła](./media/site-recovery-vmm-to-vmm/set-source3.png)
6. Zainstaluj hello dostawcy usługi Azure Site Recovery na serwerze VMM hello. Nie ma potrzeby tooexplicitly należy już nic instalować na serwerach hostów funkcji Hyper-V.


### <a name="install-hello-azure-site-recovery-provider"></a>Zainstaluj hello dostawcy usługi Azure Site Recovery

1. Uruchom plik Instalatora dostawcy hello na każdym serwerze programu VMM. Jeśli program VMM jest wdrożony w klastrze, wykonaj powitania po pierwszym instalowanym hello:
    -  Zainstaluj dostawcę hello na aktywnym węźle i Zakończ hello instalacji tooregister hello serwer VMM w magazynie hello.
    - Następnie należy zainstalować hello dostawcy na powitania innych węzłów. Węzły klastra należy uruchomić hello tę samą wersję programu hello dostawcy.
2. Instalator uruchamia kilka wymagań wstępnych i żądania usługi VMM hello toostop uprawnienia. Witaj usługi programu VMM zostanie automatycznie uruchomiona po zakończeniu instalacji. Po zainstalowaniu na klastrze programu VMM, możesz roli klastra hello toostop zostanie wyświetlony monit o.
3. W **Microsoft Update**, można włączyć toospecify czy aktualizacje dostawcy były instalowane zgodnie z zasadami Microsoft Update.
4. W **instalacji**, Zaakceptuj lub zmodyfikuj hello domyślna lokalizacja instalacji, a następnie kliknij przycisk **zainstalować**.

    ![Lokalizacja instalacji](./media/site-recovery-vmm-to-vmm/provider-location.png)
5. Po zakończeniu instalacji kliknij przycisk **zarejestrować** tooregister powitania serwera w magazynie hello.

    ![Lokalizacja instalacji](./media/site-recovery-vmm-to-vmm/provider-register.png)
6. W **nazwę magazynu**, sprawdź nazwę hello hello magazynu, w którym hello serwer zostanie zarejestrowany. Kliknij przycisk *Dalej*.

    ![Rejestracja serwera](./media/site-recovery-vmm-to-vmm-classic/vaultcred.PNG)
7. W **połączenia internetowego**, określ, jak dostawca hello uruchomiony na serwerze VMM hello łączy tooAzure.

    ![Ustawienia internetowe](./media/site-recovery-vmm-to-vmm-classic/proxydetails.PNG)

   - Można określić, tego dostawcy hello należy łączyć bezpośrednio toohello internet, lub za pośrednictwem serwera proxy.
   - Określ ustawienia serwera proxy, jeśli to konieczne.
   - Jeśli używasz serwera proxy konto Uruchom jako programu VMM (DRAProxyAccount) jest tworzony automatycznie przy użyciu hello określonych poświadczeń serwera proxy. Konfiguracja serwera proxy hello, dzięki czemu to konto mogło być pomyślnie uwierzytelnione. Witaj ustawienia konta Uruchom jako można modyfikować w konsoli programu VMM hello > **ustawienia** > **zabezpieczeń** > **konta Uruchom jako**. Uruchom ponownie zmiany tooupdate usługi VMM hello.
8. W **klucz rejestracji**, zaznacz klucz hello pobrany z usługi Azure Site Recovery, a następnie skopiować toohello serwera VMM.
9. ustawienie szyfrowania Hello jest używana tylko w przypadku replikacji maszyn wirtualnych funkcji Hyper-V w tooAzure chmur programu VMM. Jeśli replikujesz tooa lokacji dodatkowej nie jest używane.
10. W **nazwy serwera**, określ serwer VMM hello tooidentify przyjazną nazwę w magazynie hello. W konfiguracji klastra Określ nazwę roli klastra VMM hello.
11. W **Synchronizuj metadane chmury**, wybierz, czy dla wszystkich chmur na powitania serwera VMM w magazynie hello toosynchronize metadanych. Ta akcja wymaga tylko toohappen raz na każdym serwerze. Jeśli nie chcesz toosynchronize wszystkich chmur, można zaznaczać tego ustawienia i synchronizować poszczególne chmury indywidualnie WE hello właściwości chmury w konsoli programu VMM hello.
12. Kliknij przycisk **dalej** toocomplete hello procesu. Po rejestracji metadane z serwera VMM hello są pobierane przez usługę Azure Site Recovery. Serwer Hello jest wyświetlany na powitania **serwery VMM** kartę na powitania **serwerów** strony w magazynie hello.

    ![Serwer](./media/site-recovery-vmm-to-vmm-classic/provider13.PNG)
13. Po hello serwer jest dostępny w konsoli usługi Site Recovery hello w **źródła** > **Przygotuj źródło** wybierz serwer VMM hello i wybierz hello chmury, w których hello funkcji Hyper-V znajduje się host. Następnie kliknij przycisk **OK**.

Dostawca hello można także zainstalować z wiersza polecenia hello:

[!INCLUDE [site-recovery-rw-provider-command-line](../../includes/site-recovery-rw-provider-command-line.md)]


## <a name="set-up-hello-target-environment"></a>Konfigurowanie środowiska docelowego hello

Wybierz hello docelowym serwerze VMM i w chmurze.

1. Kliknij przycisk **przygotowanie infrastruktury** > **docelowego**i wybierz hello docelowym serwerze VMM ma toouse.
2. Pojawi się na serwerze hello chmury, które są synchronizowane z usługą Site Recovery. Wybierz chmurę docelową hello.

   ![docelowy](./media/site-recovery-vmm-to-vmm/target-vmm.png)

## <a name="set-up-replication-settings"></a>Konfigurowanie ustawień replikacji

- Po utworzeniu zasad replikacji wszystkich hosta za pomocą zasad hello musi mieć hello sam system operacyjny. Witaj chmury VMM może zawierać hosty funkcji Hyper-V z różnymi wersjami systemu Windows Server, ale w takim przypadku należy wielu skojarzeń zasad replikacji.
- Można wykonywać hello o początkowej replikacji w trybie offline. [Dowiedz się więcej](#prepare-for-initial-offline-replication)

1. Kliknij przycisk toocreate nowe zasady replikacji **przygotowanie infrastruktury** > **ustawienia replikacji** > **+ Utwórz i skojarz**.

    ![Sieć](./media/site-recovery-vmm-to-vmm/gs-replication.png)
2. W obszarze **Utwórz i skojarz zasady** określ nazwę zasad. Witaj źródłowy i docelowy typ powinien być **funkcji Hyper-V**.
3. W **host funkcji Hyper-V w wersji**, wybierz system operacyjny jest uruchomiona na hoście hello.
4. W **typ uwierzytelniania** i **port uwierzytelniania**, określ, jak uwierzytelnianie ruchu między hello podstawowego i serwery hosta funkcji Hyper-V odzyskiwania. Wybierz **certyfikatu** w przypadku braku działającego środowiska protokołu Kerberos. Usługa Azure Site Recovery automatycznie skonfiguruje certyfikatów do uwierzytelniania protokołu HTTPS. Nie trzeba toodo niczego ręcznie. Domyślnie port 8083 i 8084 (dla certyfikatów) będą otwierane w hello zapory systemu Windows na serwerach hostów funkcji Hyper-V hello. Jeśli wybierzesz **Kerberos**, biletu protokołu Kerberos będzie używany do wzajemnego uwierzytelniania hello serwerów hosta. Należy pamiętać, że to ustawienie dotyczy tylko serwerów hosta funkcji Hyper-V z systemem Windows Server 2012 R2.
5. W **częstotliwość kopiowania**, określić, jak często dane różnicowe tooreplicate po replikacji początkowej hello (co 30 sekund, 5 lub 15 minut).
6. W **przechowywania punktu odzyskiwania**, określ w godzinach, jak długo będą hello okna przechowywania dla każdego punktu odzyskiwania. Chronione maszyny można odzyskać tooany punktu, w tym oknie.
7. W **częstotliwość migawek spójności aplikacji**, określ, jak często (1 – 12 godzin) punkty odzyskiwania zawierające migawki spójne z aplikacjami są tworzone. Funkcja Hyper-V wykorzystuje dwa typy migawek — standardową migawkę, która jest przyrostową migawką całej maszyny wirtualnej hello i migawki spójne z aplikacją, która tworzy migawkę danych aplikacji hello wewnątrz maszyny wirtualnej hello punktu w czasie. Migawki spójne z aplikacjami Użyj tooensure usługi kopiowania woluminów w tle (VSS), które aplikacje są w spójnym stanie podczas hello migawki. Włącz migawki spójne z aplikacjami, wpłynie na powitania wydajność aplikacji uruchomionych na źródłowych maszynach wirtualnych. Upewnij się, że ustawiona wartość hello jest mniejsza niż liczba hello punktów odzyskiwania dodatkowe, które można skonfigurować.
8. W **kompresję transferu danych**, określ, czy można kompresować replikowane dane przesyłane.
9. Wybierz **Usuń replikę maszyny Wirtualnej**, powinien zostać usunięty toospecify, który hello maszyny wirtualnej repliki, Jeśli wyłączysz ochrona powitalnych źródłowej maszyny Wirtualnej. Jeśli to ustawienie zostanie włączone po wyłączeniu ochrony dla źródła hello maszyny Wirtualnej zostanie usunięte z konsoli usługi Site Recovery hello, ustawienia usługi Site Recovery dla hello VMM z konsoli programu VMM hello, i repliki hello jest usunięte.
10. W **metodę replikacji początkowej**, jeśli przeprowadzasz replikację za pośrednictwem sieci hello, określ, czy toostart hello replikacji początkowej lub zaplanowania jej. toosave przepustowość sieci, może być tooschedule ją poza najbardziej obciążonymi godzinami. Następnie kliknij przycisk **OK**.

     ![Zasady replikacji](./media/site-recovery-vmm-to-vmm/gs-replication2.png)
11. Podczas tworzenia nowych zasad jest ona automatycznie skojarzona z hello chmury VMM. W **zasad replikacji**, kliknij przycisk **OK**. Dodatkowe chmury VMM (oraz hello maszyn wirtualnych w nich) można skojarzyć z zasadami replikacji w **replikacji** > nazwa_zasady > **Skojarz chmurę VMM**.

     ![Zasady replikacji](./media/site-recovery-vmm-to-vmm/policy-associate.png)


### <a name="configure-network-mapping"></a>Konfiguracja mapowania sieci

- Dowiedz się więcej o [mapowania sieci](#prepare-for-network-mapping) przed jego uruchomieniem.
- Sprawdź, czy maszyny wirtualne na serwerach VMM są połączone tooa sieci maszyny Wirtualnej.


1. W **infrastruktura usługi Site Recovery** > **mapowanie sieci** > **mapowania sieci**, kliknij przycisk **+ mapowanie sieci**.

    ![Mapowanie sieci](./media/site-recovery-vmm-to-azure/network-mapping1.png)
2. W **Dodaj mapowanie sieci** , wybierz źródło hello i VMM serwery docelowe. Witaj sieci maszyny Wirtualnej skojarzone z serwerów VMM hello są pobierane.
3. W **Sieć źródłowa**, wybierz sieć hello ma toouse z listy hello sieci maszyny Wirtualnej skojarzone z hello podstawowy serwer VMM.
4. W **Sieć docelowa**, wybierz sieć hello ma toouse na powitania pomocniczy serwer programu VMM. Następnie kliknij przycisk **OK**.

    ![Mapowanie sieci](./media/site-recovery-vmm-to-vmm/network-mapping2.png)

Oto, co się dzieje po rozpoczęciu mapowania sieci:

* Wszystkie istniejące maszyny wirtualne repliki odpowiadające źródłowej sieci maszyny Wirtualnej toohello będzie sieć maszyny Wirtualnej podłączonej toohello docelowej.
* Nowe maszyny wirtualne, które są połączone toohello źródłowej sieci maszyny Wirtualnej będzie mapowanej sieci docelowej połączonych toohello po replikacji.
* Jeśli zmodyfikujesz istniejące mapowanie, uwzględniając nową sieć maszyn wirtualnych repliki zostaną podłączone z wykorzystaniem nowych ustawień hello.
* Jeśli hello Sieć docelowa ma wiele podsieci i jedna z tych podsieci ma hello znajduje się samą nazwę jak podsieć, w których hello źródłowej maszyny wirtualnej, a następnie hello repliki maszyny wirtualnej zostaną połączone toothat docelowej podsieci po pracy awaryjnej. Jeśli nie ma żadnych docelowa podsieć o pasującej nazwie, maszyna wirtualna hello będzie toohello połączonych pierwszej podsieci w sieci hello.

### <a name="configure-storage-mapping"></a>Skonfiguruj mapowanie pamięci masowej.

[Mapowanie magazynu](#prepare-for-storage-mapping) nie jest obsługiwany w hello nowego portalu Azure. Jednak można ją włączyć, przy użyciu programu Powershell. [Dowiedz się więcej](site-recovery-vmm-to-vmm-powershell-resource-manager.md#step-7-configure-storage-mapping).

## <a name="step-5-capacity-planning"></a>Krok 5. Planowanie pojemności

Teraz, po skonfigurowaniu podstawowej infrastruktury, pomyśl o planowaniu pojemności i zorientuj się, czy potrzebujesz dodatkowych zasobów.

- Pobierz i uruchom hello [Azure Site Recovery Capacity planner](site-recovery-capacity-planner.md), toogather informacji o środowisku replikacji, w tym o maszynach wirtualnych, dysków dla maszyny Wirtualnej i magazynu dla każdego dysku.
- Po zostały zebrane informacje o replikacji w czasie rzeczywistym, można zmodyfikować hello NetQos zasad toocontrol replikacji przepustowości dla maszyn wirtualnych. Przeczytaj więcej na temat [ograniczania ruchu repliki funkcji Hyper-V](http://www.thomasmaurer.ch/2013/12/throttling-hyper-v-replica-traffic/), na blogu Thomasa Maurer blogu. Uzyskaj więcej informacji o hello [polecenia cmdlet New-NetQosPolicy](https://technet.microsoft.com/library/hh967468.aspx.).

## <a name="enable-replication"></a>Włączanie replikacji

1. Kliknij kolejno pozycje **Krok 2. Replikowanie aplikacji** > **Źródło**. Po włączeniu replikacji dla powitania po raz pierwszy, kliknij **+ Replikuj** w hello magazynu tooenable replikację dla dodatkowych maszyn.

    ![Włączanie replikacji](./media/site-recovery-vmm-to-vmm/enable-replication1.png)
2. W **źródła**, wybierz serwer VMM hello i hello chmury, w których hello znajdują się hosty funkcji Hyper-V ma tooreplicate. Następnie kliknij przycisk **OK**.

    ![Włączanie replikacji](./media/site-recovery-vmm-to-vmm/enable-replication2.png)
3. W **docelowego**, sprawdź hello pomocniczy serwer programu VMM i w chmurze.
4. W **maszyn wirtualnych**, wybierz hello maszyny wirtualne mają tooprotect z listy hello.

    ![Włączanie ochrony maszyny wirtualnej](./media/site-recovery-vmm-to-vmm/enable-replication5.png)

Możesz śledzić postępy hello **Włącz ochronę** akcji w **zadania** > **zadania usługi Site Recovery**. Po hello **zakończenia ochrony** zadanie zostało ukończone, maszyna wirtualna hello jest gotowa do pracy awaryjnej.

Należy pamiętać, że:

- Można również włączyć ochronę maszyn wirtualnych w konsoli programu VMM hello. Kliknij przycisk **Włącz ochronę** na pasku narzędzi hello we właściwościach maszyny wirtualnej hello > **usługi Azure Site Recovery** kartę.
- Po włączeniu replikacji można wyświetlić właściwości hello maszyny Wirtualnej w **elementy replikowane**. Na powitania **Essentials** pulpitu nawigacyjnego, wyświetlane są informacje dotyczące zasad replikacji hello hello maszyny Wirtualnej i jej stan. Kliknij przycisk **właściwości** więcej szczegółów.

### <a name="onboard-existing-virtual-machines"></a>Dodaj istniejące maszyny wirtualne
Jeśli masz istniejące maszyny wirtualne w programie VMM, które są replikowane z funkcji Hyper-V Replica, możesz dołączyć je do replikacji usługi Azure Site Recovery w następujący sposób:

1. Upewnij się, że serwer hello funkcji Hyper-V hosting hello istniejącej maszyny Wirtualnej znajduje się w chmurze podstawowej hello oraz tego serwera funkcji Hyper-V hello obsługującego maszyny wirtualnej repliki hello znajduje się w chmurze dodatkowej hello.
2. Upewnij się, że skonfigurowano zasady replikacji dla chmury VMM podstawowej hello.
3. Włącz replikację hello podstawowej maszyny wirtualnej. Azure Site Recovery i VMM upewnij się, że hello tego samego hosta repliki i maszyny wirtualnej zostanie wykryte i będzie używał usługi Azure Site Recovery i ponownie ustanowić replikację przy użyciu hello określonych ustawień.

## <a name="test-your-deployment"></a>Testowanie wdrożenia

tootest wdrożenia, możesz uruchomić [testowanie trybu failover](site-recovery-test-failover-vmm-to-vmm.md) dla jednej maszyny wirtualnej, lub [Tworzenie planu odzyskiwania](site-recovery-create-recovery-plans.md) zawiera co najmniej jednej maszyny wirtualnej.



## <a name="prepare-for-offline-initial-replication"></a>Przygotuj się do początkowej replikacji offline

Możesz to zrobić hello kopii początkowe dane replikacji w trybie offline. Można to przygotować w następujący sposób:

* Na powitania serwera źródłowego można określić lokalizacji, z których hello odbędzie się eksportowania danych. Pełna kontrola przypisać uprawnienia NTFS i udziału toohello usługi VMM w ścieżce eksportu hello. Na serwerze docelowym hello można określić lokalizacji, z której zaimportować hello danych zostanie przeprowadzona. Przypisz hello te same uprawnienia, w tym ścieżki importu.
* Jeśli hello importowania lub eksportowania, ścieżka jest udostępniana, przypisz członkostwo w grupie administratora, użytkownik zaawansowany, Operator drukowania lub Operator serwera na powitania konto usługi VMM na komputerze zdalnym hello na które hello udostępnionych znajduje się.
* Jeśli używasz Uruchom jako konta tooadd hosty, na powitania zaimportować i wyeksportuj ścieżki, przypisz odczytu Odczyt i zapis toohello konta Uruchom jako w programie VMM.
* Witaj importowanie i eksportowanie udziałów nie powinien znajdować się na dowolnym komputerze używany jako serwer hosta funkcji Hyper-V, ponieważ konfiguracja ze sprzężeniem zwrotnym nie jest obsługiwana przez funkcję Hyper-V.
* W usłudze Active Directory na każdym serwerze hosta funkcji Hyper-V, który zawiera maszyny wirtualne tooprotect, włączyć i skonfigurować delegowanie ograniczone tootrust hello komputerami zdalnymi na które hello importowanie i eksportowanie ścieżek znajdują się, w następujący sposób:
  1. Na kontrolerze domeny hello Otwórz **użytkownicy usługi Active Directory i komputery**.
  2. W drzewie konsoli powitania kliknij **DomainName** > **komputerów**.
  3. Nazwa serwera hosta funkcji Hyper-V powitania kliknij prawym przyciskiem myszy > **właściwości**.
  4. Na powitania **delegowania** , kliknij pozycję **Ufaj temu komputerowi w delegowania toospecified tylko usług**.
  5. Kliknij przycisk **Użyj dowolnego protokołu uwierzytelniania**.
  6. Kliknij przycisk **dodać** > **użytkownicy i komputery**.
  7. Nazwa typu hello hello komputerze, który obsługuje ścieżkę eksportu hello > **OK**. Z listy dostępnych usług hello, naciśnij i przytrzymaj klawisz CTRL hello, a następnie kliknij przycisk **cifs** > **OK**. Powtórz hello nazwę komputera hello tej ścieżki importu hello hostów. Powtórz w razie potrzeby dodatkowe serwery hosta funkcji Hyper-V.



## <a name="prepare-for-network-mapping"></a>Przygotowanie do mapowania sieci
Mapowanie sieci działa między sieciami maszyn wirtualnych VMM na powitania podstawowym i pomocniczym serwerze programu VMM do:

* Optymalnie umieścić po pracy awaryjnej maszyn wirtualnych repliki dodatkowej hosty funkcji Hyper-V.
* Łączenie sieci maszyn wirtualnych tooappropriate maszyn wirtualnych repliki po pracy awaryjnej.

Należy pamiętać, że:
- Mapowanie sieci można skonfigurować między sieciami maszyn wirtualnych na dwóch serwerach VMM, lub na jednym serwerze programu VMM, gdy dwie lokacje są zarządzane przez hello sam serwer.
- W przypadku mapowania jest poprawnie skonfigurowany i replikacja jest włączona, maszyny Wirtualnej w lokalizacji głównej hello będzie tooa połączonych sieci i jej replika w lokalizacji docelowej hello zostaną podłączone tooits mapowane sieci.
- Jeśli sieci są skonfigurowane poprawnie w programie VMM po wybraniu opcji sieć maszyny Wirtualnej docelową podczas mapowania sieci, hello VMM źródła chmur używających hello źródłowej sieci maszyny Wirtualnej zostanie wyświetlony, wraz z sieci maszyn wirtualnych dostępnych hello na powitania docelowej chmury, które są używane do ochrona.
- Jeśli hello Sieć docelowa ma wiele podsieci i jedna z tych podsieci ma tej samej nazwy jak hello podsieci, w których hello znajduje źródłowej maszyny wirtualnej, następnie hello hello maszyny wirtualnej repliki zostaną połączone toothat docelowej podsieci po pracy awaryjnej. Jeśli nie ma żadnych docelowa podsieć o pasującej nazwie, maszyna wirtualna hello będzie toohello połączonych pierwszej podsieci w sieci hello.


Oto przykład tooillustrate ten mechanizm. Spójrzmy organizacji z dwóch lokalizacji w Nowym Jorku i Chicago.

| **Lokalizacja** | **Serwer VMM** | **Sieci maszyn wirtualnych** | **Mapowane na** |
| --- | --- | --- | --- |
| Nowy Jork |Program VMM NowyJork |NowyJork VMNetwork1 |Zmapowane Chicago tooVMNetwork1 |
| NowyJork VMNetwork2 |Nie zostały zamapowane | | |
| Chicago |Program VMM Chicago |VMNetwork1 Chicago |Zmapowane NowyJork tooVMNetwork1 |
| VMNetwork2 Chicago |Nie zostały zamapowane | | |

Z tym przykładem:

* Po utworzeniu maszyny wirtualnej repliki dla żadnej maszyny wirtualnej, który jest połączony NowyJork tooVMNetwork1 będą połączone Chicago tooVMNetwork1.
* Po utworzeniu maszyny wirtualnej repliki dla NowyJork VMNetwork2 lub VMNetwork2 Chicago nie będzie tooany połączenia sieciowego.

Oto, jak chmur programu VMM są zainstalowane w naszym przykładzie organizacji, a także hello sieci logiczne skojarzone z chmury hello.

### <a name="cloud-protection-settings"></a>Ustawienia ochrony chmury
| **Chronionej chmurze** | **Ochrona chmury** | **Sieć logiczna (Nowy Jork)** |
| --- | --- | --- |
| GoldCloud1 |GoldCloud2 | |
| SilverCloud1 |SilverCloud2 | |
| GoldCloud2 |<p>Nie dotyczy</p><p></p> |<p>NowyJork LogicalNetwork1</p><p>LogicalNetwork1 Chicago</p> |
| SilverCloud2 |<p>Nie dotyczy</p><p></p> |<p>NowyJork LogicalNetwork1</p><p>LogicalNetwork1 Chicago</p> |

### <a name="logical-and-vm-network-settings"></a>Ustawienia sieci logicznych, jak i maszyny Wirtualnej
| **Lokalizacja** | **Sieć logiczna** | **Skojarzone sieci maszyny Wirtualnej** |
| --- | --- | --- |
| Nowy Jork |NowyJork LogicalNetwork1 |NowyJork VMNetwork1 |
| Chicago |LogicalNetwork1 Chicago |VMNetwork1 Chicago |
| LogicalNetwork2Chicago |VMNetwork2 Chicago | |

### <a name="target-networks"></a>Sieci docelowych
Na podstawie tych ustawień, gdy wybrana sieć wirtualna docelowa hello, hello w poniższej tabeli przedstawiono opcje hello, które będą dostępne.

| **Wybierz** | **Chronionej chmurze** | **Ochrona chmury** | **Sieć docelowa jest dostępna** |
| --- | --- | --- | --- |
| VMNetwork1 Chicago |SilverCloud1 |SilverCloud2 |Dostępna |
| GoldCloud1 |GoldCloud2 |Dostępna | |
| VMNetwork2 Chicago |SilverCloud1 |SilverCloud2 |Niedostępne |
| GoldCloud1 |GoldCloud2 |Dostępna | |


### <a name="failback"></a>Powrót po awarii
co się stanie w przypadku powrotu po awarii (replikacja odwrotna) hello toosee Załóżmy, że NowyJork VMNetwork1 jest mapowanych tooVMNetwork1-Chicago, z hello następujące ustawienia.

| **Maszyny wirtualne** | **TooVM połączonych sieci** |
| --- | --- |
| VM1 |VMNetwork1 sieci |
| Maszyny VM2 (repliki VM1) |VMNetwork1 Chicago |

Przy użyciu tych ustawień umożliwia przeglądanie, co dzieje się w kilku możliwych scenariuszach.

| **Scenariusz** | **Wynik** |
| --- | --- |
| Brak zmian w hello właściwości sieci maszyny Wirtualnej 2 po pracy awaryjnej. |1 maszyna wirtualna pozostaje Sieć źródłowa toohello połączonych. |
| Właściwości sieci maszyny Wirtualnej 2 są zmieniane po pracy awaryjnej i jest odłączony. |1 maszyna wirtualna jest odłączony. |
| Właściwości sieci maszyny Wirtualnej 2 są zmieniane po pracy awaryjnej i jest połączony Chicago tooVMNetwork2. |Jeśli nie jest zamapowana VMNetwork2 Chicago, 1 maszyna wirtualna zostanie odłączony. |
| Mapowanie sieci VMNetwork1 Chicago zostanie zmieniona. |1 maszyna wirtualna będzie toohello połączonych sieci obecnie mapowane tooVMNetwork1-Chicago. |


## <a name="prepare-for-single-server-deployment"></a>Przygotowanie do wdrożenia pojedynczego serwera


Jeśli masz tylko jeden serwer VMM, można replikować maszyny wirtualne na hostach funkcji Hyper-V w chmurze VMM hello zbyt[Azure](site-recovery-vmm-to-azure.md) lub tooa dodatkowej chmury VMM. Firma Microsoft zaleca hello pierwsza opcja, ponieważ replikacja między chmurami nie ma łatwego. Jeśli chcesz tooreplicate między chmurami może replikować z jednym autonomicznym serwerem VMM lub za pomocą jednego serwera VMM wdrożone w klastrze rozciągnięty systemu Windows

### <a name="standalone-vmm-server"></a>Serwer VMM autonomiczny

W tym scenariuszu podczas wdrażania pojedynczego serwera VMM hello jako maszyny wirtualnej w lokacji głównej hello, a replikowanie tej maszyny Wirtualnej tooa dodatkowej lokacji przy użyciu usługi Site Recovery i funkcji Hyper-V Replica.

1. **Konfigurowanie programu VMM na maszynie Wirtualnej funkcji Hyper-V**. Zalecamy, aby przekazać hello wystąpienia programu SQL Server używany przez program VMM na powitania tej samej maszyny Wirtualnej. Zaoszczędzić czas, jak tylko jedna maszyna wirtualna ma toobe utworzony. Jeśli chcesz toouse zdalnego wystąpienia programu SQL Server i wystąpienia awarii, należy toorecover danego wystąpienia zanim będzie można odzyskać VMM.
2. **Upewnij się, serwer VMM hello ma co najmniej dwa skonfigurowaną chmurę**. Jedna chmura zawiera maszyny wirtualne mają tooreplicate i hello innych chmurze będzie służyć jako lokalizacja dodatkowa hello powitalne. Witaj w chmurze, która zawiera hello maszyny wirtualne mają tooprotect powinny być zgodne z [wymagania wstępne](#prerequisites).
3. Konfigurowanie usługi Site Recovery, zgodnie z opisem w tym artykule. Utwórz i zarejestruj hello serwer VMM w magazynie, skonfigurować zasady replikacji i włączyć replikację. nazwy VMM Hello źródłowa i docelowa będzie hello w tej samej. Określ, że początkowa replikacja odbywa się za pośrednictwem sieci hello.
4. Po skonfigurowaniu mapowania sieci należy mapować hello sieci maszyny Wirtualnej dla sieci maszyny Wirtualnej toohello chmury podstawowej hello hello dodatkowej chmury.
5. W konsoli Menedżera funkcji Hyper-V hello Włącz repliki funkcji Hyper-V na hoście funkcji Hyper-V hello, który zawiera hello maszyny Wirtualnej programu VMM i włączyć replikację na powitania maszyny Wirtualnej. Upewnij się, że nie dodawaj tooclouds maszyny wirtualnej VMM hello, które są chronione przez usługę Site Recovery, tooensure, że ustawienia funkcji Hyper-V Replica nie są zastępowane przez usługę Site Recovery.
6. W przypadku utworzenia plany odzyskiwania dla trybu failover, którego używasz hello na tym samym serwerze programu VMM dla źródła i docelowych.
7. Zakończenie przestoju służy do pracy awaryjnej i odzyskać w następujący sposób:

   1. Uruchomić nieplanowany tryb failover w konsoli Menedżera funkcji Hyper-V hello w lokacji dodatkowej hello, toofail za pośrednictwem hello podstawowej maszyny Wirtualnej VMM toohello dodatkowej lokacji.
   2. Sprawdź powitalne tej maszyny Wirtualnej VMM jest uruchomiony i działa prawidłowo, a w magazynie hello Uruchom toofail nieplanowanego trybu failover za pośrednictwem hello maszyn wirtualnych z podstawowego toosecondary chmur. Przekaż hello trybu failover, a następnie wybierz alternatywny punkt odzyskiwania, jeśli jest wymagana.
   3. Po hello nieplanowanego trybu failover, wszystkie zasoby są dostępne z lokacji głównej hello ponownie.
   4. Po udostępnieniu ponownie, w konsoli Menedżera funkcji Hyper-V hello w lokacji dodatkowej hello hello lokacji głównej, należy włączyć replikację odwrotną dla maszyny Wirtualnej VMM hello. Spowoduje to uruchomienie replikacji dla maszyny Wirtualnej hello z tooprimary dodatkowej.
   5. Uruchom planowanego trybu failover w konsoli Menedżera funkcji Hyper-V hello w lokacji dodatkowej hello, toofail za pośrednictwem hello lokacji głównej toohello maszyny Wirtualnej VMM. Zatwierdź hello trybu failover. Następnie należy włączyć replikację odwrotną, dzięki czemu hello maszyny Wirtualnej VMM replikacja odbywa się ponownie z toosecondary głównej.
   6. W magazynie usług odzyskiwania hello Włącz replikację odwrotną dla hello obciążenia maszyn wirtualnych, toostart replikować je z tooprimary dodatkowej.
   7. W magazynie usług odzyskiwania hello, uruchom planowany tryb failover toofail wstecz hello obciążenia maszyn wirtualnych toohello lokacji głównej. Zatwierdź toocomplete pracy awaryjnej hello go. Włącz replikację odwrotną toostart replikacji hello obciążenia maszyn wirtualnych z podstawowego toosecondary.

### <a name="stretched-vmm-cluster"></a>Rozciągnięty klastra VMM

Zamiast wdrażać autonomiczny serwer programu VMM jako maszynę Wirtualną, która replikuje tooa lokacji dodatkowej, możesz wprowadzić VMM wysokiej dostępności przez wdrożenie jej jako maszyny Wirtualnej w klastrze pracy awaryjnej systemu Windows. Zapewnia to odporność obsługi obciążeń i ochrony przed awariami sprzętu. toodeploy z hello lokacji odzyskiwania maszyny Wirtualnej VMM powinny zostać wdrożone w klastrze stretch między lokacjami geograficznie. toodo to:

1. Zainstaluj program VMM na maszynie wirtualnej w klastrze pracy awaryjnej systemu Windows i wybierz hello opcja toorun powitania serwera jako o wysokiej dostępności podczas instalacji.
2. Hello wystąpienia programu SQL Server, który jest używany przez program VMM powinny być replikowane z grupami dostępności AlwaysOn programu SQL Server, aby była repliki bazy danych hello w lokacji dodatkowej hello.
3. Postępuj zgodnie z instrukcjami hello w tym artykule toocreate magazynu, Zarejestruj serwer hello i skonfiguruj ochronę. Należy tooregister każdy serwer VMM w hello klastra w powitalne magazyn usług odzyskiwania. toodo, zainstaluj hello dostawcy na aktywnym węźle i Zarejestruj serwer VMM hello. Następnie należy zainstalować hello dostawcy na innych węzłach.
4. Po awarii, serwer programu VMM hello jego odpowiednia baza danych programu SQL Server przełączone do trybu failover i uzyskać dostęp z lokacji dodatkowej hello.



## <a name="prepare-for-storage-mapping"></a>Przygotowanie do mapowania magazynu


Konfigurowanie magazynu mapowania przez mapowania klasyfikacji magazynu w źródle i docelowa następujące hello toodo serwery VMM:

  * **Identyfikowanie docelowy magazyn dla maszyny wirtualnej repliki**— na dysku twardym maszyny Wirtualnej źródłowego zostaną zreplikowane magazynu toohello, określony (udział SMB lub klastra udostępnione woluminy (CSV)) w miejscu docelowym hello.
  * **Umieszczania maszyn wirtualnych repliki**— mapowanie magazynu jest toooptimally używanych maszyn wirtualnych repliki miejscu na serwerach hostów funkcji Hyper-V. Maszyny wirtualne repliki zostaną umieszczone na hostach, które mogą uzyskiwać dostęp do klasyfikacji magazynu hello zamapowane.
  * **Brak mapowania magazynu**— Jeśli nie skonfigurujesz mapowania przechowywania maszyny wirtualne będą replikowane toohello domyślną lokalizację przechowywania określonych na serwerze hosta funkcji Hyper-V hello skojarzoną z maszyną wirtualną hello repliki.

Należy pamiętać, że:
- Można skonfigurować mapowanie między dwoma chmur programu VMM na jednym serwerze.
- Klasyfikacje magazynu musi być toohello dostępnych grup hostów znajduje się w chmurach źródłowe i docelowe.
- Nie ma potrzeby klasyfikacje toohave hello tego samego typu magazynu. Na przykład można mapować Klasyfikacja źródła, która zawiera klasyfikacji docelowego tooa udziałów SMB, zawierający udostępnionych woluminów klastra.

### <a name="example"></a>Przykład
Jeśli klasyfikacje są poprawnie skonfigurowane w programie VMM po wybraniu hello źródłowy i docelowy serwer programu VMM podczas mapowania pamięci masowej, pojawi się hello klasyfikacje źródłowe i docelowe. Oto przykład udziałów plików magazynu i klasyfikacji dla organizacji z dwóch lokalizacji w Nowym Jorku i Chicago.

| **Lokalizacja** | **Serwer VMM** | **Udziału plików (źródło)** | **Klasyfikacja (źródło)** | **Mapowane na** | **Udziału plików (docelowy)** |
| --- | --- | --- | --- | --- | --- |
| Nowy Jork |VMM_Source |SourceShare1 |GOLD |GOLD_TARGET |TargetShare1 |
| SourceShare2 |SREBRNY |SILVER_TARGET |TargetShare2 | | |
| SourceShare3 |BRĄZOWY |BRONZE_TARGET |TargetShare3 | | |
| Chicago |VMM_Target | |GOLD_TARGET |Nie zostały zamapowane | |
|  |SILVER_TARGET |Nie zostały zamapowane | | | |
|  |BRONZE_TARGET |Nie zostały zamapowane | | | |

Z tym przykładem:

* Po utworzeniu maszyny wirtualnej repliki dla żadnej maszyny wirtualnej w magazynie ZŁOTA (SourceShare1) będą replikowane tooa GOLD_TARGET magazynu (TargetShare1).
* Po utworzeniu maszyny wirtualnej repliki dla żadnej maszyny wirtualnej w magazynie SREBRNY (SourceShare2) zostanie ono tooa replikowanego magazynu SILVER_TARGET (TargetShare2) i tak dalej.

### <a name="multiple-storage-locations"></a>Wiele lokalizacji magazynu
Przydzielenia klasyfikacji docelowy hello toomultiple SMB udziały lub woluminy CSV lokalizacji magazynu optymalne hello zostaną automatycznie zaznaczone, po hello maszyna wirtualna jest chroniona. Jeśli brak odpowiedniego elementu docelowego magazynu jest dostępny z hello określona klasyfikacji, hello domyślnej lokalizacji magazynu określony na hoście funkcji Hyper-V hello jest używany tooplace hello replik wirtualnych dysków twardych.

Hello w poniższej tabeli przedstawiono, jak klasyfikacji magazynu i udostępnionych woluminów klastra są skonfigurowane w naszym przykładzie.

| **Lokalizacja** | **Klasyfikacja** | **Skojarzone magazynu** |
| --- | --- | --- |
| Nowy Jork |GOLD |<p>C:\ClusterStorage\SourceVolume1</p><p>\\FileServer\SourceShare1</p> |
| SREBRNY |<p>C:\ClusterStorage\SourceVolume2</p><p>\\FileServer\SourceShare2</p> | |
| Chicago |GOLD_TARGET |<p>C:\ClusterStorage\TargetVolume1</p><p>\\FileServer\TargetShare1</p> |
| SILVER_TARGET |<p>C:\ClusterStorage\TargetVolume2</p><p>\\FileServer\TargetShare2</p> | |

Ta tabela zawiera podsumowanie hello zachowanie po włączeniu ochrony dla maszyn wirtualnych (VM1 - VM5) w tym przykładzie środowisku.

| **Maszyny wirtualne** | **Źródłowy magazyn** | **Klasyfikacja źródła** | **Zmapowane docelowy magazyn** |
| --- | --- | --- | --- |
| VM1 |C:\ClusterStorage\SourceVolume1 |GOLD |<p>C:\ClusterStorage\SourceVolume1</p><p>\\\FileServer\SourceShare1</p><p>Zarówno GOLD_TARGET</p> |
| MASZYNY VM2 |\\FileServer\SourceShare1 |GOLD |<p>C:\ClusterStorage\SourceVolume1</p><p>\\FileServer\SourceShare1</p> <p>Zarówno GOLD_TARGET</p> |
| VM3 |C:\ClusterStorage\SourceVolume2 |SREBRNY |<p>C:\ClusterStorage\SourceVolume2</p><p>\FileServer\SourceShare2</p> |
| VM4 |\FileServer\SourceShare2 |SREBRNY |<p>C:\ClusterStorage\SourceVolume2</p><p>\\FileServer\SourceShare2</p><p>Zarówno SILVER_TARGET</p> |
| VM5 |C:\ClusterStorage\SourceVolume3 |Nie dotyczy |Brak mapowania, więc hello domyślną lokalizację przechowywania hosta funkcji Hyper-V hello jest używany |



### <a name="data-privacy-overview"></a>Omówienie prywatności danych

Ta tabela zawiera podsumowanie sposobu przechowywania danych w tym scenariuszu:

- - -
| Akcja | **Szczegóły** | **Zebrane dane** | **Korzystanie** | **Wymagane** |
| --- | --- | --- | --- | --- |
| **Rejestracja** | Należy zarejestrować serwer VMM w magazynie usług odzyskiwania. Jeśli chcesz później toounregister serwera, możesz to zrobić przez usunięcie informacji o serwerze hello z hello portalu Azure. | Po zarejestrowaniu serwera VMM lokacji odzyskiwania zbiera procesów i przenosi metadane dotyczące hello serwer VMM i nazwy hello chmur VMM hello wykryta przez usługę Site Recovery. | danych Hello jest używany tooidentify i komunikacji z serwerem VMM odpowiednie hello i skonfiguruj ustawienia dla odpowiednich chmur programu VMM. | Ta funkcja jest wymagana. Jeśli nie chcesz toosend tego tooSite informacje odzyskiwania nie można używać usługi Site Recovery hello. |
| **Włączanie replikacji** | Hello dostawcy usługi Azure Site Recovery jest zainstalowany na serwerze VMM hello i jest hello kanał do komunikacji z hello usługi Site Recovery. Witaj dostawcy jest biblioteki dołączanej (dynamicznie DLL), hostowana w procesie VMM hello. Funkcja "Odzyskiwania centrum danych" hello pobiera włączane po powitalne dostawca jest zainstalowany, w konsoli administratora programu VMM hello. Nowych i istniejących maszyn wirtualnych można włączyć ochrony tooenable tej funkcji dla maszyny Wirtualnej. |Z tego zestawu właściwości hello dostawcy wysyła hello nazwy i Identyfikatora hello tooSite maszyny Wirtualnej odzyskiwania.  Replikacja jest włączona w systemie Windows Server 2012 lub Windows Server 2012 R2 Hyper-V Replica. Witaj danych maszyny wirtualnej pobiera replikowane z jednego tooanother hosta funkcji Hyper-V (zazwyczaj znajduje się w centrum danych różnych "odzyskiwania"). |Usługi Site Recovery używa wirtualna hello metadane toopopulate hello hello portalu Azure. | Ta funkcja jest integralną część usługi hello i nie można jej wyłączyć. Jeśli nie chcesz toosend te informacje, nie należy włączyć ochronę usługi Site Recovery maszyn wirtualnych. Należy pamiętać, że wszystkie dane przesyłane przez tooSite dostawcy hello odzyskiwania są przesyłane za pośrednictwem protokołu HTTPS. |
| **Plan odzyskiwania** | Plany odzyskiwania pomocne w tworzeniu planu aranżacji centrum danych hello odzyskiwania. Można określić kolejność hello, w którym maszyny wirtualne lub grupy maszyn wirtualnych powinny być uruchamiane w lokacji odzyskiwania hello. Można również określić wszelkie toobe zautomatyzowanych skryptów Uruchom lub dowolnego toobe ręczne działania podjęte w czasie hello odzyskiwania dla każdej maszyny Wirtualnej. Zwykle wyzwoleniu trybu failover na poziomie planu odzyskiwania hello skoordynowany sposób odzyskiwania. | Usługa Site Recovery zbiera, przetwarza i przesyła metadanych dla planu odzyskiwania hello, w tym metadanych maszyny wirtualnej, a metadane wszelkich skryptów automatyzacji oraz zawiera informacje o akcji ręcznej. |metadane Hello jest plan odzyskiwania hello toobuild używanych w hello portalu Azure. |Ta funkcja jest integralną część usługi hello i nie można jej wyłączyć. Jeśli nie chcesz toosend tooSite tej informacji odzyskiwania, nie należy tworzyć planów odzyskiwania. |
| **Mapowanie sieci** | Mapy sieci informacji z centrum danych odzyskiwania Centrum toohello hello danych podstawowych. Gdy maszyny wirtualne są odzyskiwane w lokacji odzyskiwania hello, mapowanie sieci ułatwia ustanowienia połączenia sieciowego. |Usługa Site Recovery zbiera, przetwarza i przesyła metadanych hello hello sieci logicznych dla każdej lokacji (podstawowe i datacenter). |metadane Hello jest toopopulate używanych ustawień sieci, dzięki czemu można mapować hello informacje o sieci. | Ta funkcja jest integralną część usługi hello i nie można jej wyłączyć. Jeśli nie chcesz toosend tooSite tej informacji odzyskiwania, nie używaj mapowania sieci. |
| **Tryb failover (planowane/nieplanowane/testowanie oprogramowania)** | Trybu failover nie powiedzie się za pośrednictwem maszyn wirtualnych z jednego danych zarządzanych przez program VMM tooanother center. Akcja trybu failover Hello jest wyzwalana ręcznie w hello portalu Azure. |Witaj dostawcy na serwerze VMM hello jest powiadamiany hello zdarzenia trybu failover za pomocą usługi Site Recovery i uruchamia działanie trybu failover na hoście funkcji Hyper-V hello za pośrednictwem interfejsów VMM. Rzeczywistego uruchamiania trybu failover maszyny wirtualnej z jednego tooanother hosta funkcji Hyper-V i obsługiwane przez system Windows Server 2012 lub Windows Server 2012 R2 Hyper-V Replica. Tylnym usługi Site Recovery używa informacji hello wysyłane stan hello toopopulate informacje o akcji trybu failover hello hello portalu Azure. | Ta funkcja jest integralną część usługi hello i nie można jej wyłączyć. Jeśli nie chcesz toosend tooSite tej informacji odzyskiwania, nie należy używać trybu failover. |

## <a name="next-steps"></a>Następne kroki

Po przetestowaniu wdrożenia hello więcej informacji na temat innych typów [trybu failover](site-recovery-failover.md)
