---
title: aaaReplicate maszyn wirtualnych funkcji Hyper-V w lokacji dodatkowej VMM tooa (klasyczny Portal Azure) | Dokumentacja firmy Microsoft
description: "W tym artykule opisano, jak tooreplicate maszyn wirtualnych funkcji Hyper-V w programie VMM chmur tooa dodatkowej lokacji programu VMM z usługą Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: a63acba3-8fb3-4926-aa29-b1e64a765681
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: raynew
ms.openlocfilehash: fe551e1f741579044f540ea0e50a6e36d48133ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooa-secondary-vmm-site"></a>Replikowanie maszyn wirtualnych funkcji Hyper-V w VMM chmur tooa lokacja dodatkowa programu VMM
> [!div class="op_single_selector"]
> * [Witryna Azure Portal](site-recovery-vmm-to-vmm.md)
> * [Portal klasyczny](site-recovery-vmm-to-vmm-classic.md)
> * [Program PowerShell — model usługi Resource Manager](site-recovery-vmm-to-vmm-powershell-resource-manager.md)
>
>

Witaj usługi Azure Site Recovery przyczynia się tooyour ciągłość i strategia odzyskiwania (BCDR) poprzez organizowanie replikacji, trybu failover i odzyskiwania maszyn wirtualnych i serwerów fizycznych. Maszyny można replikowanych tooAzure lub tooa dodatkowej w lokalnym centrum danych. Aby zapoznać się z szybkim omówieniem, przeczytaj temat [Co to jest usługa Azure Site Recovery?](site-recovery-overview.md)

## <a name="overview"></a>Omówienie
W tym artykule opisano, jak serwery, zarządzane przez program VMM chmur toosecondary lokacji programu VMM przy użyciu usługi Azure Site Recovery hosta funkcji Hyper-V tooreplicate maszyn wirtualnych w funkcji Hyper-V.

Hello artykuł zawiera wymagania wstępne, pokazuje sposób instalacji tooset się w magazynie usługi Site Recovery hello dostawcy usługi Azure Site Recovery na źródłowym i VMM serwery docelowe, zarejestrować serwery hello w magazynie hello, skonfiguruj ustawienia ochrony dla chmur programu VMM i włączeniu Ochrona maszyn wirtualnych funkcji Hyper-V. Aby zakończyć, testowania hello trybu failover toomake się, że wszystko działa zgodnie z oczekiwaniami.

Zamieść wszelkie komentarze lub pytania u dołu hello w tym artykule, albo na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="architecture"></a>Architektura
Obraz powitania poniżej przedstawia kanałów komunikacyjnych różnych hello i porty używane przez usługę Azure Site Recovery do aranżacji i replikacji

![Topologia E2E](./media/site-recovery-vmm-to-vmm-classic/e2e-topology.png)

## <a name="before-you-start"></a>Przed rozpoczęciem
Upewnij się, że te wymagania wstępne zostały spełnione:

| **Wymagania wstępne** | **Szczegóły** |
| --- | --- |
| **Azure** |Potrzebujesz konta platformy [Microsoft Azure](https://azure.microsoft.com/). Możesz rozpocząć od [bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/). [Dowiedz się więcej](https://azure.microsoft.com/pricing/details/site-recovery/) o cenach usługi Site Recovery. |
| **VMM** |Należy co najmniej jeden serwer programu VMM.<br/><br/>Serwer VMM Hello powinna być uruchomiona co najmniej System Center 2012 SP1 z hello najnowszymi aktualizacjami zbiorczymi.<br/><br/>Jeśli chcesz tooset konfiguracji ochrony za pomocą jednego serwera programu VMM, należy co najmniej dwóch chmur skonfigurowane na serwerze hello.<br/><br/>Jeśli chcesz toodeploy ochrony z dwoma serwerami VMM każdy serwer musi mieć co najmniej jednej chmury skonfigurowanej na powitania tooprotect i jednej chmury skonfigurowanej na serwerze VMM dodatkowej hello podstawowy serwer VMM ma toouse dla ochrony i odzyskiwania<br/><br/>Wszystkie chmury VMM musi mieć ustawić profil funkcji Hyper-V hello.<br/><br/>Chmura źródłowa Hello, które mają tooprotect musi zawierać co najmniej jedną grupę hostów programu VMM. |
| **Funkcja Hyper-V** |Wymaga co najmniej jeden serwer hosta funkcji Hyper-V w hello podstawowych i pomocniczych grupę hostów programu VMM i co najmniej jednej maszyny wirtualnej na każdym serwerze hosta funkcji Hyper-V.<br/><br/>Witaj źródłowa i docelowa serwerów funkcji Hyper-V musi działać co najmniej Windows Server 2012 z rolą funkcji Hyper-V hello i mieć hello zainstalowane najnowsze aktualizacje.<br/><br/>Dowolnego serwera funkcji Hyper-V zawierające maszyny wirtualne mają tooprotect musi znajdować się w chmurze VMM.<br/><br/>Jeśli używasz funkcji Hyper-V w klastrze, należy pamiętać, że broker klastra nie jest tworzony automatycznie w przypadku statycznej klastra oparte na adresie IP. Należy ręcznie tooconfigure hello brokera. Aby [dowiedzieć się więcej](https://www.petri.com/use-hyper-v-replica-broker-prepare-host-clusters), zobacz wpis na blogu Aidana Finna. |
| **Mapowanie sieci** |Można skonfigurować, aby się upewnić, czy replikowane maszyny wirtualne optymalnie są umieszczane na serwerach hostów funkcji Hyper-V dodatkowej po pracy awaryjnej i czy można połączyć się sieci maszyn wirtualnych tooappropriate toomake mapowania sieci. Jeśli nie skonfigurujesz mapowania sieci, repliki maszyn wirtualnych będzie sieci połączonych tooany po pracy awaryjnej.<br/><br/>tooset mapowanie sieci podczas wdrażania, upewnij się, że hello maszyny wirtualne na serwerze hosta funkcji Hyper-V źródła hello są tooa połączonych sieci maszyny Wirtualnej VMM. Ta sieć powinna być tooa połączone sieci logicznej, która jest skojarzona z hello chmury. < br /<br/>Chmura docelowa Hello na powitania pomocniczy serwer VMM używanego do odzyskiwania powinny mieć skonfigurowane odpowiednie sieci maszyny Wirtualnej, a z kolei powinien być połączony tooa odpowiadającego sieci logicznej, która jest skojarzona z hello chmura docelowa. |
| **Mapowanie magazynu** |Domyślnie podczas replikacji maszyny wirtualnej w funkcji Hyper-V host serwera tooa docelowy funkcji Hyper-V hosta serwera źródłowego, replikowane dane są przechowywane w hello domyślnej lokalizacji określonej dla hosta funkcji Hyper-V docelowego hello w Menedżerze funkcji Hyper-V. Aby uzyskać większą kontrolę nad przechowywania replikowanych danych można skonfigurować mapowania magazynu<br/><br/> Magazyn tooconfigure mapowania, należy tooset się klasyfikacji magazynu na powitania źródła i VMM serwery docelowe, przed rozpoczęciem wdrażania. |

## <a name="step-1-create-a-site-recovery-vault"></a>Krok 1. Tworzenie magazynu usługi Site Recovery
1. Zaloguj się toohello [portalu zarządzania](https://portal.azure.com) z serwera VMM hello ma tooregister.
2. Rozwiń węzeł **usług danych** > **usług odzyskiwania** i kliknij przycisk **magazynie usługi Site Recovery**.
3. Kliknij pozycje **Utwórz nowe** > **Szybkie tworzenie**.
4. W **nazwa**, wprowadź przyjazną nazwę tooidentify hello magazynu.
5. W **Region** wybierz hello region geograficzny magazynu hello. toocheck obsługiwane regiony, zobacz dotyczącą dostępności geograficznej w [szczegóły cennika usługi Azure Site Recovery](http://go.microsoft.com/fwlink/?LinkId=389880).
6. Kliknij pozycję **Utwórz magazyn**.

    ![Tworzenie magazynu](./media/site-recovery-vmm-to-vmm-classic/create-vault.png)

Sprawdź stan hello paska tego magazynu hello został utworzony. Witaj magazyn będzie wyświetlany jako **Active** na powitania głównej strony usług odzyskiwania.

## <a name="step-2-generate-a-vault-registration-key"></a>Krok 2. Generowanie klucza rejestracji magazynu
Wygeneruj klucz rejestracji w magazynie hello. Po pobraniu hello dostawcy usługi Azure Site Recovery i zainstaluj go na serwerze VMM hello, użyjesz tego serwera VMM hello tooregister kluczy w magazynie hello.

1. W hello **usług odzyskiwania** strony Szybki Start hello tooopen magazynu powitania kliknij pozycję. Szybki Start można również otworzyć w dowolnym momencie, korzystając z ikony hello.

    ![Ikona Szybki start](./media/site-recovery-vmm-to-vmm-classic/quick-start-icon.png)
2. Z listy rozwijanej hello wybierz **między dwiema lokacjami VMM lokalnymi**.
3. W **Przygotowanie serwerów programu VMM**, kliknij przycisk **Wygeneruj plik klucza rejestracji**. Plik klucza Hello jest generowany automatycznie i jest ważny przez 5 dni po jego wygenerowaniu. Jeśli nie używasz hello portalu Azure z serwerem VMM hello należy toocopy tego serwera toohello plików.

    ![Klucz rejestracji](./media/site-recovery-vmm-to-vmm-classic/register-key.png)

## <a name="step-3-install-hello-azure-site-recovery-provider"></a>Krok 3: Instalowanie hello dostawcy usługi Azure Site Recovery
1. Na powitania **Szybki Start** strony w **Przygotowanie serwerów programu VMM**, kliknij przycisk **Pobierz Microsoft dostawcy Azure Site Recovery do instalacji na serwerach VMM** tooobtain hello najnowsza wersja Wersja pliku instalacyjnego dostawcy hello.
2. Uruchom ten plik na źródłowym serwerze programu VMM hello.

   > [!NOTE]
   > Jeśli program VMM jest wdrożony w klastrze i instalujesz hello dostawcy dla powitania po raz pierwszy go zainstalować na aktywnym węźle i Zakończ hello instalacji tooregister hello serwer VMM w magazynie hello. Następnie zainstaluj hello dostawcy na powitania innych węzłów. Należy pamiętać, że Jeśli uaktualniasz hello dostawcy należy tooupgrade we wszystkich węzłach, ponieważ wszystkie powinny być uruchomione hello sama wersja dostawcy.
   >
   >
3. Instalator Hello jest kilka **Sprawdzanie wymagań wstępnych** żądania uprawnień toostop hello VMM usługi Instalatora dostawcy toobegin i. Witaj usługi programu VMM zostanie automatycznie uruchomiona po zakończeniu instalacji. Jeśli przeprowadzasz instalację na klastra VMM, który będzie wyświetlony monit o roli klastra hello toostop.
4. W usłudze **Microsoft Update** można włączyć aktualizacje. To ustawienie jest włączone aktualizacje dostawcy będą instalowane zgodnie z zasadami Microsoft Update tooyour.

    ![Usługa Microsoft Updates](./media/site-recovery-vmm-to-vmm-classic/ms-update.png)
5. Lokalizacja instalacji Hello ustawiono zbyt**<SystemDrive>\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin**. Polecenie hello toostart przycisk Zainstaluj instalowanie hello dostawcy.

    ![InstallLocation](./media/site-recovery-vmm-to-vmm-classic/install-location.png)
6. Po hello jest zainstalowany dostawca kliknij **zarejestrować** tooregister powitania serwera w magazynie hello.

    ![InstallComplete](./media/site-recovery-vmm-to-vmm-classic/install-complete.png)
7. W **nazwę magazynu**, sprawdź nazwę hello hello magazynu, w którym hello serwer zostanie zarejestrowany. Kliknij przycisk *Dalej*.

    ![Rejestracja serwera](./media/site-recovery-vmm-to-vmm-classic/vaultcred.PNG)
8. W **połączenia internetowego** Określ hello jak dostawca uruchomiony na powitania VMM łączy serwer toohello Internet. Wybierz **Połącz przy użyciu istniejących ustawień serwera proxy** toouse hello domyślnych ustawień połączenia internetowego skonfigurowane na powitania serwera.

    ![Ustawienia internetowe](./media/site-recovery-vmm-to-vmm-classic/proxydetails.PNG)

   * Jeśli chcesz, aby toouse niestandardowego serwera proxy należy skonfigurować go przed zainstalowaniem hello dostawcy. Podczas konfigurowania niestandardowych ustawień serwera proxy wykonywany jest test w toocheck hello proxy połączenia.
   * Jeśli używasz niestandardowego serwera proxy lub domyślny serwer proxy wymaga uwierzytelniania należy tooenter hello proxy szczegółów, w tym hello adres i port proxy.
   * Następujące adresy URL powinien być dostępny hello serwer VMM i hosty funkcji Hyper-v hello
     * *.hypervrecoverymanager.windowsazure.com
     * *.accesscontrol.windows.net
     * *.backup.windowsazure.com
     * *.blob.core.windows.net
     * *.store.core.windows.net
   * Zezwalaj na adresy IP hello opisanego w [zakresów IP centrum danych Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653) i protokół HTTPS (port 443). Trzeba toowhite listą zakresów IP hello region platformy Azure, możesz zaplanować toouse i zachodnie stany USA.
   * Jeśli używasz niestandardowego serwera proxy konto Uruchom jako programu VMM (DRAProxyAccount) zostanie utworzony automatycznie za pomocą hello określonych poświadczeń serwera proxy. Konfiguracja serwera proxy hello, dzięki czemu to konto mogło być pomyślnie uwierzytelnione. Ustawienia konta Uruchom jako programu VMM Hello można modyfikować w konsoli programu VMM hello. toodo, otwórz hello **ustawienia** obszaru roboczego, rozwiń węzeł **zabezpieczeń**, kliknij przycisk **konta Uruchom jako**, a następnie zmodyfikować hello hasło dla konta DRAProxyAccount. Usługa VMM hello toorestart należy tak, aby to ustawienie zostało zastosowane.
9. W **klucz rejestracji**, zaznacz klucz hello pobrany z usługi Azure Site Recovery, a następnie skopiować toohello serwera VMM.
10. ustawienie szyfrowania Hello jest używana tylko w przypadku replikacji maszyn wirtualnych funkcji Hyper-V w tooAzure chmur programu VMM. Jeśli replikujesz tooa lokacji dodatkowej nie jest używane.
11. W **nazwy serwera**, określ serwer VMM hello tooidentify przyjazną nazwę w magazynie hello. W konfiguracji klastra Określ nazwę roli klastra VMM hello.
12. W **Synchronizuj metadane chmury** wybierz, czy dla wszystkich chmur na powitania serwera VMM w magazynie hello toosynchronize metadanych. Ta akcja wymaga tylko toohappen raz na każdym serwerze. Jeśli nie chcesz toosynchronize wszystkich chmur, można zaznaczać tego ustawienia i synchronizować poszczególne chmury indywidualnie WE hello właściwości chmury w konsoli programu VMM hello.
13. Kliknij przycisk **dalej** toocomplete hello procesu. Po rejestracji metadane z serwera VMM hello są pobierane przez usługę Azure Site Recovery. Serwer Hello jest wyświetlany w **serwery VMM** > **serwerów** w magazynie hello.

    ![Serwery](./media/site-recovery-vmm-to-vmm-classic/provider13.PNG)

### <a name="command-line-installation"></a>Instalacja przy użyciu wiersza polecenia
Witaj dostawcy usługi Azure Site Recovery można również zainstalować z wiersza polecenia hello. Ta metoda może być używana tooinstall hello dostawcy w RDZENIU serwera dla systemu Windows Server 2012 R2.

1. Pobierz hello dostawcy plików i rejestracji klucza tooa folder instalacji. Na przykład C:\ASR.
2. Zatrzymaj hello Usługa System Center Virtual Machine Manager
3. Wyodrębnij Instalatora dostawcy hello, uruchamiając następujące polecenia z wiersza polecenia, używając **administratora** uprawnienia:

        C:\Windows\System32> CD C:\ASR
        C:\ASR> AzureSiteRecoveryProvider.exe /x:. /q
4. Zainstaluj dostawcę hello uruchamiając:

        C:\ASR> setupdr.exe /i
5. Zarejestruj dostawcę hello uruchamiając:

        CD C:\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin
        C:\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin\> DRConfigurator.exe /r  /Friendlyname <friendly name of hello server> /Credentials <path of hello credentials file> /EncryptionEnabled <full file name toosave hello encryption certificate>     

Gdy parametry hello są:

* **/ Credentials**: obowiązkowy parametr, który określa lokalizację hello, w których hello znajduje się plik klucza rejestracji  
* **/ FriendlyName**: obowiązkowy parametr dla nazwy powitania serwera hosta hello funkcji Hyper-V, która jest wyświetlana w portalu usługi Azure Site Recovery hello.
* **/ EncryptionEnabled**: opcjonalny parametr należy toouse tylko w tooAzure VMM hello scenariusz, jeśli potrzebujesz szyfrowania maszyn wirtualnych przechowywanych na platformie Azure. Sprawdź, czy nazwa hello tego pliku hello podasz ma **PFX** rozszerzenia.
* **/ proxyaddress**: opcjonalny parametr określający adres hello powitania serwera proxy.
* **/ proxyport**: opcjonalny parametr określający port hello powitania serwera proxy.
* **/ proxyusername**: opcjonalny parametr określający nazwę użytkownika serwera Proxy hello (Jeśli serwer proxy wymaga uwierzytelniania).
* **/ proxypassword**: opcjonalny parametr określający hello hasła w celu uwierzytelniania z serwerem proxy hello (Jeśli serwer proxy wymaga uwierzytelniania).  

## <a name="step-4-configure-cloud-protection-settings"></a>Krok 4: Konfigurowanie chmury ustawienia ochrony
Po zarejestrowanych serwerów programu VMM, można skonfigurować ustawienia ochrony chmury. Jeśli włączona opcja hello **Synchronizuj dane chmury z magazynem hello** podczas instalowania dostawcy hello więc wszystkich chmur na serwerze VMM hello pojawią się w hello **chronione elementy** kartę w magazynie hello. Jeśli użytkownik nie można zsynchronizować z usługą Azure Site Recovery określonej chmury w hello **ogólne** karty hello strony właściwości chmury w konsoli programu VMM hello.

![Opublikowana chmura](./media/site-recovery-vmm-to-vmm-classic/clouds-list.png)

1. Na stronie Szybki Start powitania kliknij **Konfigurowanie ochrony dla chmur programu VMM**.
2. Na powitania **chmur programu VMM** , a następnie wybierz chmury hello chcesz tooconfigure, a następnie przejdź toohello **konfiguracji** kartę.
3. W **docelowej**, wybierz pozycję **VMM**.
4. W **lokalizacja docelowa**, wybierz hello na miejscu serwera VMM, który zarządza hello chmurę toouse odzyskiwania.
5. W **Target chmury**, wybierz chmurę docelową hello ma toouse pracy awaryjnej maszyn wirtualnych w chmurze źródło hello. Należy pamiętać, że:

   * Zaleca się, że wybierz chmurę docelową, który spełnia wymagania odzyskiwania hello maszyn wirtualnych, które będą chronić.
   * Chmury mogą należeć tylko pary chmur pojedynczego tooa — jako podstawowego lub chmurę docelową.
6. W **częstotliwość kopiowania**, określ, jak często dane mają być synchronizowane między 5he lokalizacja źródłowa i docelowa. Należy pamiętać, że to ustawienie działa tylko po hello hosta funkcji Hyper-V jest uruchomiony system Windows Server 2012 R2. Dla innych serwerów używane domyślne ustawienia pięciu minut.
7. W **dodatkowych punktów odzyskiwania**, określ, czy toocreate dodatkowe punkty. Wartość domyślna zero Hello wskazuje, że tylko hello najnowszy punkt odzyskiwania dla podstawowej maszyny wirtualnej jest przechowywany na serwerze hosta repliki. Należy pamiętać, że włączenie wiele punktów odzyskiwania wymaga dodatkowego miejsca do magazynowania dla hello migawek, które są przechowywane w każdym punkcie odzyskiwania. Domyślnie punkty odzyskiwania są tworzone co godzinę, dzięki czemu każdy punkt odzyskiwania zawiera wartość godziny danych. wartość punktu odzyskiwania Hello przypisany do maszyny wirtualnej hello w konsoli programu VMM hello nie powinna być mniejsza niż wartość hello przypisać w konsoli usługi Azure Site Recovery hello.
8. W **częstotliwość migawek spójnych z aplikacją**, określ, jak często toocreate migawki spójne z aplikacjami. Funkcja Hyper-V wykorzystuje dwa typy migawek — standardową migawkę, która jest przyrostową migawką całej maszyny wirtualnej hello i migawki spójne z aplikacją, która tworzy migawkę danych aplikacji hello wewnątrz maszyny wirtualnej hello punktu w czasie. Migawki spójne z aplikacjami Użyj tooensure usługi kopiowania woluminów w tle (VSS), które aplikacje są w spójnym stanie podczas hello migawki. Należy pamiętać, że po włączeniu migawek spójnych z aplikacją ma wpływ na powitania wydajność aplikacji uruchomionych na źródłowych maszynach wirtualnych. Upewnij się, że ustawiona wartość hello jest mniejsza niż liczba hello punktów odzyskiwania dodatkowe, które można skonfigurować.

    ![Skonfiguruj ustawienia ochrony](./media/site-recovery-vmm-to-vmm-classic/cloud-settings.png)
9. W **kompresję transferu danych**, określ, czy można kompresować replikowane dane przesyłane.
10. W **uwierzytelniania**, określ, jak uwierzytelnianie ruchu między hello podstawowego i serwery hosta funkcji Hyper-V odzyskiwania. Należy wybrać protokół HTTPS, chyba że masz działającego środowiska Kerberos skonfigurowane. Usługa Azure Site Recovery automatycznie skonfiguruje certyfikatów do uwierzytelniania protokołu HTTPS. Nie jest wymagana żadna konfiguracja ręczna. W przypadku wybrania protokołu Kerberos, biletu protokołu Kerberos będzie używany do wzajemnego uwierzytelniania hello serwerów hosta. Domyślnie port 8083 i 8084 (dla certyfikatów) będą otwierane w hello zapory systemu Windows na serwerach hostów funkcji Hyper-V hello. Należy pamiętać, że to ustawienie dotyczy tylko serwerów hosta funkcji Hyper-V z systemem Windows Server 2012 R2.
11. W **portu**, zmodyfikuj hello numer portu, na których źródło hello i docelowych komputerów hostów nasłuchuje ruchu związanego z replikacją. Na przykład możesz zmodyfikować hello ustawienie, jeśli chcesz, aby tooapply jakości usług (QoS) sieci przepustowości dla ruchu replikacji. Sprawdź, czy hello port nie jest używany przez inną aplikację i Otwórz w ustawieniach zapory hello.
12. W **metodę replikacji**, określ sposób hello początkowej replikacji danych z lokalizacji tootarget źródła obsługi, przed rozpoczęciem replikacji regularne:

    * **Za pośrednictwem sieci**— kopiowanie danych za pośrednictwem sieci hello może być czasochłonne i użyciem zasobów. Firma Microsoft zaleca, możesz użyć tej opcji hello chmura zawiera maszyny wirtualne z stosunkowo mały wirtualne dyski twarde, a lokacja główna hello jest toohello podłączonej lokacji dodatkowej za pośrednictwem połączenia z szeroką przepustowości. Można określić, że kopia hello powinien natychmiast rozpocząć lub wybierz godzinę. Replikacji sieci zaleca się zaplanowanie poza godzinami szczytu.
    * **W trybie offline**— ta metoda określa, czy Replikacja początkowa hello zostanie wykonane przy użyciu nośnika zewnętrznego. Jest przydatne, jeśli chcesz, aby tooavoid spadek wydajności sieci lub lokalizacji geograficznie zdalnych. toouse tej metody Określ lokalizację eksportu hello na powitania chmura źródłowa i lokalizacja importu hello na chmurę docelową hello. Po włączeniu ochrony dla maszyny wirtualnej, wirtualny dysk twardy hello jest skopiowany toohello określona lokalizacja eksportu. Przesyła toohello lokacji docelowej, a następnie skopiuj go toohello importu lokalizacji. Witaj Witaj kopii systemu zaimportowane maszyn wirtualnych repliki toohello informacji.
13. Wybierz **usunąć maszyny wirtualnej repliki** toospecify, który hello maszyny wirtualnej repliki powinien zostać usunięty, jeśli użytkownik zaprzestanie ochrony maszyny wirtualnej hello wybierając hello **Usuń ochronę dla maszyny wirtualnej hello**  opcji na karcie maszyn wirtualnych hello hello właściwości chmury. To ustawienie jest włączone, po wyłączeniu maszyny wirtualnej ochrona powitalnych zostanie usunięty z usługi Azure Site Recovery, hello ustawień usługi Site Recovery dla maszyny wirtualnej hello są w konsoli programu VMM hello, i hello repliki zostaną usunięte.

    ![Skonfiguruj ustawienia ochrony](./media/site-recovery-vmm-to-vmm-classic/cloud-settings-replica.png)

Po zapisaniu ustawień hello zadania zostanie utworzone i mogą być monitorowane na powitania **zadania** kartę. Wszystkie serwery hosta funkcji Hyper-V w hello chmura źródłowa programu VMM zostaną skonfigurowane do replikacji. Ustawienia chmury można modyfikować na powitania **Konfiguruj** kartę. Jeśli chcesz toomodify hello lokalizacji lub docelową chmurę docelową należy usunąć hello konfiguracji chmury, a następnie zmień konfigurację chmury hello.

### <a name="prepare-for-offline-initial-replication"></a>Przygotuj się do początkowej replikacji offline
Potrzebne są następujące akcje tooprepare początkowej replikacji offline hello toodo:

* Na serwerze źródłowym hello należy wskazać lokalizacji, z których hello eksportu danych będą miały miejsce. Pełna kontrola przypisać uprawnienia NTFS i udziału toohello usługi VMM w ścieżce eksportu hello. Na serwerze docelowym hello użytkownik będzie określić lokalizacji, z której zaimportować hello danych zostanie przeprowadzona. Przypisz hello te same uprawnienia, w tym ścieżki importu.
* Jeśli hello importowania lub eksportowania, ścieżka jest udostępniana, przypisz członkostwo w grupie administratora, użytkownik zaawansowany, Operator drukowania lub Operator serwera na powitania konto usługi VMM na komputerze zdalnym hello na które hello udostępnionych znajduje się.
* Jeśli używasz Uruchom jako konta tooadd hosty, na powitania zaimportować i wyeksportuj ścieżki, przypisz odczytu Odczyt i zapis toohello konta Uruchom jako w programie VMM.
* Witaj importowanie i eksportowanie udziałów nie powinien znajdować się na dowolnym komputerze używany jako serwer hosta funkcji Hyper-V, ponieważ konfiguracja ze sprzężeniem zwrotnym nie jest obsługiwana przez funkcję Hyper-V.
* W usłudze Active Directory na każdym serwerze hosta funkcji Hyper-V, który zawiera maszyny wirtualne tooprotect, włączyć i skonfigurować delegowanie ograniczone tootrust hello komputerami zdalnymi na które hello importowanie i eksportowanie ścieżek znajdują się, w następujący sposób:
  1. Na kontrolerze domeny hello Otwórz **użytkownicy usługi Active Directory i komputery**.
  2. W drzewie konsoli powitania kliknij **DomainName** > **komputerów**.
  3. Nazwa serwera hosta funkcji Hyper-V powitania kliknij prawym przyciskiem myszy > **właściwości**.
  4. Na powitania **delegowania** T kliknij kartę**Rdza tego komputera w celu delegowania toospecified tylko usług**.
  5. Kliknij przycisk **Użyj dowolnego protokołu uwierzytelniania**.
  6. Kliknij przycisk **dodać** > **użytkownicy i komputery**.
  7. Nazwa typu hello hello komputerze, który obsługuje ścieżkę eksportu hello > **OK**. Z listy dostępnych usług hello, naciśnij i przytrzymaj klawisz CTRL hello, a następnie kliknij przycisk **cifs** > **OK**. Powtórz hello nazwę komputera hello tej ścieżki importu hello hostów. Powtórz w razie potrzeby dodatkowe serwery hosta funkcji Hyper-V.

## <a name="step-5-configure-network-mapping"></a>Krok 5: Konfigurowanie mapowania sieci
1. Na stronie Szybki Start powitania kliknij **Mapuj sieci**.
2. Wybierz hello źródłowym serwerze programu VMM z którego chcesz toomap sieci, a następnie hello powitania toowhich serwera VMM docelowej, sieci zostanie zamapowana. Lista Hello źródła sieci i ich skojarzonych docelowego są wyświetlane. Wartość pusta jest wyświetlany dla sieci, które nie są obecnie mapowane.
3. Wybierz sieć w **sieci w źródle** > **mapy**. Usługa Hello hello sieci maszyn wirtualnych na serwerze docelowym hello wykrywa i wyświetla je. Kliknij przycisk hello informacji ikona dalej toohello źródłowa i docelowa nazwy tooview hello podsieci dla każdej sieci.

    ![Konfiguracja mapowania sieci](./media/site-recovery-vmm-to-vmm-classic/network-mapping1.png)
4. W oknie dialogowym hello wybierz jedną z sieci maszyny Wirtualnej hello z hello docelowym serwerze VMM.

    ![Wybieranie sieci docelowej](./media/site-recovery-vmm-to-vmm-classic/network-mapping2.png)
5. Po wybraniu Sieć docelowa hello liczba chronionych chmur używających Sieć źródłowa hello są wyświetlane. Wyświetlane są również dostępne docelowych sieci, które są skojarzone z chmury hello używany na potrzeby ochrony. Firma Microsoft zaleca, wybierz opcję sieci docelowej, która jest dostępne tooall hello chmur, używanego do ochrony. Lub można również przejść toohello serwer VMM i modyfikować hello chmury właściwości tooadd hello sieci logicznej odpowiadającego toohello sieci maszyn wirtualnych, które mają toochoose.
6. Kliknij przycisk hello — proces mapowania hello toocomplete znacznik wyboru. Postęp mapowania hello tootrack uruchomienia zadania. Możesz je wyświetlić na powitania **zadania** kartę.

## <a name="step-6-configure-storage-mapping"></a>Krok 6: Konfigurowanie mapowania magazynu
Domyślnie podczas replikacji maszyny wirtualnej w funkcji Hyper-V host serwera tooa docelowy funkcji Hyper-V hosta serwera źródłowego, replikowane dane są przechowywane w hello domyślnej lokalizacji określonej dla hosta funkcji Hyper-V docelowego hello w Menedżerze funkcji Hyper-V. Uzyskać większą kontrolę nad przechowywania replikowanych danych można skonfigurować mapowania magazynu w następujący sposób:

1. Zdefiniuj klasyfikacje magazynu dla obu źródła hello i VMM serwery docelowe. [Dowiedz się więcej](https://technet.microsoft.com/library/gg610685.aspx). Klasyfikacje musi być toohello dostępne serwery hosta funkcji Hyper-V w chmurach źródłowym i docelowym. Nie ma potrzeby klasyfikacje toohave hello tego samego typu magazynu. Na przykład można mapować Klasyfikacja źródła, która zawiera klasyfikacji docelowego tooa udziałów SMB, zawierający udostępnionych woluminów klastra.
2. Po klasyfikacje są na miejscu, można utworzyć mapowania. toodo to na powitania **Szybki Start** strony > **mapy magazynu**.
3. Kliknij przycisk hello **magazynu** kartę > **mapowania klasyfikacji magazynu**.
4. Na powitania **mapowania klasyfikacji magazynu** , wybierz klasyfikacje na serwerze źródłowym hello i VMM serwery docelowe. Zapisz ustawienia.

    ![Wybieranie sieci docelowej](./media/site-recovery-vmm-to-vmm-classic/storage-mapping.png)

## <a name="step-7-enable-virtual-machine-protection"></a>Krok 7: Włączanie ochrony maszyny wirtualnej
Po serwerów, chmur i sieci są skonfigurowane poprawnie, można włączyć ochrony dla maszyn wirtualnych w chmurze hello.

1. Na powitania **maszyn wirtualnych** w chmurze hello, w których hello znajduje się maszyny wirtualnej, kliknij pozycję **Włącz ochronę** > **Dodawanie maszyn wirtualnych**.
2. Z listy hello maszyn wirtualnych w chmurze hello wybierz hello, co ma tooprotect.

    ![Włączanie ochrony maszyny wirtualnej](./media/site-recovery-vmm-to-vmm-classic/enable-protection.png)
3. Śledzenie postępu hello akcji włączania ochrony w hello **zadania** kartę, w tym hello replikacji początkowej. Po hello zadanie zakończenia ochrony maszyna wirtualna działa hello jest gotowy do trybu failover. Po włączeniu ochrony i zreplikowaniu maszyn wirtualnych, będziesz w stanie tooview je na platformie Azure.

    ![Zadanie ochrony maszyny wirtualnej](./media/site-recovery-vmm-to-vmm-classic/vm-jobs.png)

> [!NOTE]
> Można również włączyć ochronę maszyn wirtualnych w konsoli programu VMM hello. Kliknij przycisk **Włącz ochronę** na powitania narzędzi hello **usługi Azure Site Recovery** hello właściwości maszyny wirtualnej.
>
>

### <a name="on-board-existing-virtual-machines"></a>Lokalnego istniejące maszyny wirtualne
Jeśli masz istniejące maszyny wirtualne w programie VMM, które są replikowane z funkcji Hyper-V Replica potrzebujesz tooonboard ich do ochrony Azure Site Recovery w następujący sposób:

1. Sprawdź, czy masz głównych i dodatkowych chmurach. Upewnij się, że serwer hello funkcji Hyper-V hosting hello istniejącej maszyny wirtualnej znajduje się w chmurze podstawowej hello i tego serwera funkcji Hyper-V hello obsługującego maszyny wirtualnej repliki hello znajduje się w chmurze dodatkowej hello. Upewnij się, że skonfigurowano ustawienia ochrony chmury hello. Ustawienia Hello powinna odpowiadać tych aktualnie skonfigurowanych dla funkcji Hyper-V Replica. W przeciwnym razie replikację maszyny wirtualnej może nie działać zgodnie z oczekiwaniami.
2. Następnie włącz ochronę hello podstawowej maszyny wirtualnej. Azure Site Recovery i VMM zapewnia, że hello tego samego hosta repliki i maszyny wirtualnej jest wykrywane i usługi Azure Site Recovery spowoduje ponowne użycie i ponownie ustanowić replikację przy użyciu ustawień hello skonfigurowane podczas konfigurowania chmury.

## <a name="test-your-deployment"></a>Testowanie wdrożenia
Planowanie wdrożenia możesz uruchomić test trybu failover dla jednej maszyny wirtualnej, lub utworzyć plan odzyskiwania składające się z wielu maszyn wirtualnych i uruchomić test trybu failover dla hello tootest.  Próba przejścia w tryb failover symuluje mechanizm pracy awaryjnej i odzyskiwania w sieci izolowanej.

### <a name="create-a-recovery-plan"></a>Tworzenie planu odzyskiwania
1. Na powitania **plany odzyskiwania** , kliknij pozycję **Utwórz Plan odzyskiwania**.
2. Określ nazwę dla planu odzyskiwania hello i serwerach VMM źródłowych i docelowych. Serwer źródłowy Hello musi mieć maszyn wirtualnych, które są włączone dla trybu failover i odzyskiwania. Wybierz **funkcji Hyper-V** tooview tylko chmury, które są skonfigurowane do replikacji funkcji Hyper-V.

    ![Tworzenie planu odzyskiwania](./media/site-recovery-vmm-to-vmm-classic/recovery-plan1.png)
3. W **Wybieranie maszyny wirtualnej**, wybierz grupy replikacji. Wszystkie maszyny wirtualne powiązane z grupy replikacji hello będzie można wybrać i dodać toohello planu odzyskiwania. Te maszyny wirtualne są dodawane planu odzyskiwania toohello grupy domyślnej — Grupa 1. w razie potrzeby można dodać więcej grup. Należy pamiętać, że po replikacji maszyny wirtualnej rozpocznie zgodnie z kolejnością hello grup hello planu odzyskiwania.

    ![Dodaj maszyny wirtualne](./media/site-recovery-vmm-to-vmm-classic/recovery-plan2.png)

Po utworzeniu planu odzyskiwania, zostanie wyświetlony na liście hello na powitania **plany odzyskiwania** kartę.

### <a name="run-a-test-failover"></a>Wykonywanie próby przejścia w tryb failover
1. Na powitania **plany odzyskiwania** , a następnie wybierz hello plan i kliknij przycisk **testowy tryb Failover**.
2. Na powitania **potwierdzić testowy tryb Failover** wybierz pozycję **Brak**. Należy pamiętać, że włączeniu tej opcji hello przejścia w tryb failover maszyny wirtualnej repliki nie będzie tooany połączenia sieciowego. Spowoduje to przetestowanie ponad zgodnie z oczekiwaniami hello maszyny wirtualnej kończy się niepowodzeniem, ale nie sprawdza środowiska sieciowego replikacji. Zobacz, jak za[testować tryb failover](site-recovery-failover.md) Aby uzyskać więcej informacji o tym, jak toouse różnych opcji sieciowych.
3. Witaj testowej maszyny wirtualnej zostanie utworzona na powitania sam hosta jako hello hosta, na które hello istnieje maszyny wirtualnej repliki. Jest ona dodawana toohello tej samej chmury, w których hello znajduje się maszyna wirtualna repliki.

### <a name="run-a-recovery-plan"></a>Uruchom planu odzyskiwania
Po replikacji hello repliki maszyny wirtualnej może nie mieć adres IP, który jest hello sam, jak adres IP hello hello podstawowej maszyny wirtualnej. Maszyny wirtualne zaktualizuje hello serwera DNS, które używają po rozpoczęciu. Istnieje również możliwość dodania skryptów tooupdate powitania serwera DNS tooensure terminowo aktualizacji.

#### <a name="script-tooretrieve-hello-ip-address"></a>Adres IP hello tooretrieve skryptu
Uruchom ten adres IP hello tooretrieve przykładowy skrypt.

        $vm = Get-SCVirtualMachine -Name <VM_NAME>
        $na = $vm[0].VirtualNetworkAdapters>
        $ip = Get-SCIPAddress -GrantToObjectID $na[0].id
        $ip.address  

#### <a name="script-tooupdate-dns"></a>Skrypt tooupdate DNS
Uruchom ten przykładowy skrypt tooupdate DNS określenie adresu IP hello pobrać za pomocą hello poprzedniej przykładowy skrypt.

        string]$Zone,
        [string]$name,
        [string]$IP
        )
        $Record = Get-DnsServerResourceRecord -ZoneName $zone -Name $name
        $newrecord = $record.clone()
        $newrecord.RecordData[0].IPv4Address  =  $IP
        Set-DnsServerResourceRecord -zonename $zone -OldInputObject $record -NewInputObject $Newrecord



## <a name="privacy-information-for-site-recovery"></a>Informacje o ochronie prywatności dla usługi Site Recovery
Ta sekcja zawiera informacje o dodatkowych prywatności dotyczące hello usługi Microsoft Azure Site Recovery ("Usługa"). tooview hello — zasady zachowania poufności usługi Microsoft Azure, zobacz [Microsoft Azure — zasady zachowania poufności informacji](http://go.microsoft.com/fwlink/?LinkId=324899)

**Funkcja: rejestracji**

* **Jaką pełni funkcję**: rejestruje serwer z usługą, dzięki czemu mogą być chronione maszyny wirtualne
* **Informacje zebrane**: po zarejestrowaniu hello usługi służy do zbierania, procesów i przesyła informacje o certyfikacie zarządzania z serwera VMM Witaj wyznaczone tooprovide odzyskiwania po awarii przy użyciu nazwy usługi hello powitania serwera VMM, i nazwa hello chmur maszyn wirtualnych na serwerze programu VMM.
* **Korzystanie z informacji o**:

  * Certyfikat zarządzania — służy to toohelp identyfikację i uwierzytelnienie hello zarejestrowano serwer VMM do toohello dostępu do usługi. Witaj usługi używa hello publicznej części klucza o toosecure certyfikatu hello token, który tylko hello zarejestrowany uzyskać dostęp do serwera programu VMM. Serwer Hello musi toouse funkcji usługi toohello to toogain tokenu dostępu.
  * Nazwa serwera VMM hello — nazwa serwera VMM hello jest wymagana tooidentify i komunikować się z hello odpowiedni serwer programu VMM na powitania, które znajdują się chmury.
  * Chmury nazw z serwera VMM hello — wymagana jest nazwa chmury hello, korzystając z chmury usługi hello parowanie rozłączania funkcji opisanych poniżej. W przypadku podjęcia decyzji toopair chmury z centrum danych pierwotnych z innej chmury w centrum danych odzyskiwania hello hello nazwy wszystkich chmur hello z centrum danych odzyskiwania hello są prezentowane.
* **Wybór**: te informacje są integralną część hello procesu rejestracji usługi, ponieważ ułatwia i hello usługi tooidentify powitania serwera VMM dla której ma zostać tooprovide ochrony Azure Site Recovery, a także tooidentify hello poprawne zarejestrowanego serwera programu VMM. Jeśli nie chcesz toosend toohello tej informacji usługi, nie należy używać tej usługi. Jeśli zarejestrować serwer, a następnie chcesz toounregister, możesz to zrobić przez usunięcie informacji o serwerze programu VMM hello z portalu hello (która jest hello portalu Azure).

**Funkcja: Włączanie usługi Azure Site Recovery**

* **Jaką pełni funkcję**: hello Azure dostawcy usługi Site Recovery zainstalowana na serwerze VMM hello jest hello kanał komunikacji z hello usługi. Witaj dostawcy jest biblioteki dołączanej (dynamicznie DLL), hostowana w procesie VMM hello. Funkcja "Odzyskiwania centrum danych" hello pobiera włączane po powitalne dostawca jest zainstalowany, w konsoli administratora programu VMM hello. Żadnych nowych lub istniejących maszyn wirtualnych w chmurze, można włączyć właściwość o nazwie "Odzyskiwania centrum danych" toohelp ochrona powitalnych maszyny wirtualnej. Gdy ta właściwość jest ustawiona, hello dostawcy wysyła hello nazwy i Identyfikatora hello toohello maszyny wirtualnej usługi. Witaj wirtualnego jest chroniona przez technologię replikacji systemu Windows Server 2012 lub Windows Server 2012 R2 Hyper-V. Witaj danych maszyny wirtualnej pobiera replikowane z jednego tooanother hosta funkcji Hyper-V (zazwyczaj znajduje się w centrum danych różnych "odzyskiwania").
* **Informacje zebrane**: hello usługi służy do zbierania, procesów i przesyła metadanych dla hello maszynę wirtualną, która zawiera nazwę hello, identyfikator sieci wirtualnej i nazwa hello hello chmury do której on należy.
* **Korzystanie z informacji o**: hello usługi używa hello powyżej maszyny wirtualnej hello toopopulate informacji w portalu usługi.
* **Wybór**: to jest integralną część usługi hello i nie można jej wyłączyć. Jeśli nie chcesz, aby te informacje wysyłane toohello usługi, nie włączaj ochrony Azure Site Recovery żadnych maszyn wirtualnych. Należy pamiętać, że wszystkie dane przesyłane przez hello toohello dostawcy usługi są przesyłane za pośrednictwem protokołu HTTPS.

**Funkcji: Plan odzyskiwania**

* **Jaką pełni funkcję**: Ta funkcja pomaga toobuild plan aranżacji centrum danych "odzyskiwania" hello. Można określić kolejność hello, w których hello maszyn wirtualnych lub grupy maszyn wirtualnych powinny być uruchamiane w lokacji odzyskiwania hello. Można również określić wszelkie toobe zautomatyzowanych skryptów Uruchom lub dowolnego toobe ręczne działania podjęte w czasie hello odzyskiwania dla każdej maszyny wirtualnej. Trybu failover (opisane w następnej sekcji hello) jest zwykle wyzwalane na powitania Plan odzyskiwania na poziomie skoordynowany sposób odzyskiwania.
* **Informacje zebrane**: hello usługi służy do zbierania, procesów i przesyła metadanych dla planu odzyskiwania hello, w tym metadanych maszyny wirtualnej, a metadane wszelkich skryptów automatyzacji oraz zawiera informacje o akcji ręcznej.
* **Korzystanie z informacji o**: metadane hello opisany powyżej jest plan odzyskiwania hello toobuild używanych w portalu usługi.
* **Wybór**: to jest integralną część usługi hello i nie można jej wyłączyć. Jeśli nie chcesz tego informacje wysyłane toohello usługi kompilacji nie plany odzyskiwania w tej usłudze.

**Funkcja: Mapowanie sieci**

* **Jaką pełni funkcję**: Ta funkcja umożliwia toomap informacje o sieci z centrum danych odzyskiwania Centrum toohello hello danych podstawowych. W przypadku maszyn wirtualnych hello są odzyskiwane w lokacji odzyskiwania hello, to mapowanie ułatwia ustanowienia połączenia sieciowego dla nich.
* **Informacje zebrane**: W ramach funkcji mapowania sieci hello, hello usługi służy do zbierania, procesów i przesyła metadanych hello hello sieci logicznych dla każdej lokacji (podstawowe i datacenter).
* **Korzystanie z informacji o**: hello usługi używa toopopulate metadanych hello portalem usługi gdzie możesz mapować hello informacje o sieci.
* **Wybór**: to jest integralną część hello usługi i nie można jej wyłączyć. Jeśli nie chcesz, aby te informacje wysyłane toohello usługi, nie używaj funkcji mapowania sieci hello.

**Funkcja: Tryb Failover - planowane, niezaplanowanego testów**

* **Jaką pełni funkcję**: Ta funkcja pomaga trybu failover maszyny wirtualnej z jednego centrum danych zarządzanych przez program VMM tooanother centrum danych zarządzanych przez program VMM. Akcja trybu failover Hello jest wyzwalany przez użytkownika hello na ich portalu. Możliwe przyczyny trybu failover obejmują nieplanowanego zdarzenia (na przykład w przypadku hello disaster0 fizycznych; to zdarzenie planowane (na przykład datacenter równoważenia obciążenia); test trybu failover (na przykład odzyskiwania planu próba).

Witaj dostawcy na serwerze VMM hello pobiera powiadamianym o zdarzeniu hello z hello usługi i wykonuje działania trybu failover na hoście funkcji Hyper-V hello za pośrednictwem interfejsów VMM. Rzeczywista praca w trybie failover hello maszynę wirtualną z jednego tooanother hosta funkcji Hyper-V (zwykle działających w centrum danych różnych "odzyskiwania") jest obsługiwane przez technologię replikacji hello systemu Windows Server 2012 lub Windows Server 2012 R2 Hyper-V. Po zakończeniu pracy awaryjnej hello hello dostawcy zainstalowanego na serwerze VMM hello centrum danych "odzyskiwania" hello wysyła hello Powodzenie informacji toohello usługi.

* **Informacje zebrane**: hello usługi używa hello powyżej informacji toopopulate hello stan hello trybu failover akcji informacji w portalu usługi.
* **Korzystanie z informacji o**: hello usługi używa hello powyżej informacji w następujący sposób:

  * Certyfikat zarządzania — służy to toohelp identyfikację i uwierzytelnienie hello zarejestrowano serwer VMM do toohello dostępu do usługi. Witaj usługi używa hello publicznej części klucza o toosecure certyfikatu hello token, który tylko hello zarejestrowany uzyskać dostęp do serwera programu VMM. Serwer Hello musi toouse funkcji usługi toohello to toogain tokenu dostępu.
  * Nazwa serwera VMM hello — nazwa serwera VMM hello jest wymagana tooidentify i komunikować się z hello odpowiedni serwer programu VMM na powitania, które znajdują się chmury.
  * Chmury nazw z serwera VMM hello — wymagana jest nazwa chmury hello, korzystając z chmury usługi hello parowanie rozłączania funkcji opisanych poniżej. W przypadku podjęcia decyzji toopair chmury z centrum danych pierwotnych z innej chmury w centrum danych odzyskiwania hello hello nazwy wszystkich chmur hello z centrum danych odzyskiwania hello są prezentowane.
* **Wybór**: to jest integralną część usługi hello i nie można jej wyłączyć. Jeśli nie chcesz, aby te informacje wysyłane toohello usługi, nie należy używać tej usługi.

## <a name="next-steps"></a>Następne kroki
Po uruchomieniu testu toocheck trybu failover, środowisku działa zgodnie z oczekiwaniami, [Dowiedz się więcej o](site-recovery-failover.md) różnego rodzaju przechodzenia w tryb failover.
