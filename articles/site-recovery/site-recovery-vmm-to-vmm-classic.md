---
title: Replikowanie maszyn wirtualnych funkcji Hyper-V w programie VMM do lokacji dodatkowej (klasyczny Portal Azure) | Dokumentacja firmy Microsoft
description: "W tym artykule opisano sposób replikowania maszyn wirtualnych funkcji Hyper-V w chmurach VMM do dodatkowej lokacji programu VMM z usługą Azure Site Recovery."
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
ms.openlocfilehash: 6814f62f73bad272229205f4768dcce5947117d1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-to-a-secondary-vmm-site"></a>Replikowanie maszyn wirtualnych funkcji Hyper-V w chmurach VMM do dodatkowej lokacji programu VMM
> [!div class="op_single_selector"]
> * [Witryna Azure Portal](site-recovery-vmm-to-vmm.md)
> * [Portal klasyczny](site-recovery-vmm-to-vmm-classic.md)
> * [Program PowerShell — model usługi Resource Manager](site-recovery-vmm-to-vmm-powershell-resource-manager.md)
>
>

Usługa Azure Site Recovery przyczynia się do strategii związanej z ciągłością biznesową i odzyskiwaniem po awarii (BCDR, business continuity and disaster recovery) poprzez organizowanie replikacji, pracy w trybie failover i odzyskiwania maszyn wirtualnych oraz serwerów fizycznych. Maszyny można replikować do platformy Azure lub lokalnego pomocniczego centrum danych. Aby zapoznać się z szybkim omówieniem, przeczytaj temat [Co to jest usługa Azure Site Recovery?](site-recovery-overview.md)

## <a name="overview"></a>Omówienie
W tym artykule opisano sposób replikowania maszyn wirtualnych funkcji Hyper-V na serwerach hostów funkcji Hyper-V, które są zarządzane w chmurach VMM do dodatkowej lokacji programu VMM przy użyciu usługi Azure Site Recovery.

Artykuł zawiera wymagania wstępne, przedstawiono sposób konfigurowania magazynu usługi Site Recovery Zainstaluj dostawcę usługi Azure Site Recovery na źródłowym i VMM serwery docelowe, Zarejestruj serwer w magazynie, skonfigurować ustawienia ochrony dla chmur programu VMM i następnie włącz ochronę maszyn wirtualnych funkcji Hyper-V. Aby zakończyć, przetestuj tryb failover w celu sprawdzenia, czy wszystko działa zgodnie z oczekiwaniami.

Zamieść wszelkie komentarze lub pytania pod tym artykułem lub na [forum Usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="architecture"></a>Architektura
Na rysunku poniżej przedstawiono kanałów komunikacyjnych różnych i porty używane przez usługę Azure Site Recovery do aranżacji i replikacji

![Topologia E2E](./media/site-recovery-vmm-to-vmm-classic/e2e-topology.png)

## <a name="before-you-start"></a>Przed rozpoczęciem
Upewnij się, że te wymagania wstępne zostały spełnione:

| **Wymagania wstępne** | **Szczegóły** |
| --- | --- |
| **Azure** |Potrzebujesz konta platformy [Microsoft Azure](https://azure.microsoft.com/). Możesz rozpocząć od [bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/). [Dowiedz się więcej](https://azure.microsoft.com/pricing/details/site-recovery/) o cenach usługi Site Recovery. |
| **VMM** |Należy co najmniej jeden serwer programu VMM.<br/><br/>Na serwerze VMM powinny być uruchomiona co najmniej System Center 2012 SP1 z najnowszymi aktualizacjami zbiorczymi.<br/><br/>Jeśli chcesz skonfigurować ochronę za pomocą jednego serwera programu VMM, należy co najmniej dwóch chmur skonfigurowane na serwerze.<br/><br/>Jeśli chcesz wdrożyć ochrony przy użyciu dwóch serwerów programu VMM, każdy serwer musi mieć co najmniej jednej chmury skonfigurowanej na podstawowym serwerze programu VMM, który chcesz chronić, a jednej chmury skonfigurowanej na pomocniczym serwerze programu VMM, który ma być używany do ochrony i odzyskiwania<br/><br/>Wszystkie chmury VMM musi mieć ustawić profil funkcji Hyper-V.<br/><br/>Chmura źródłowa, którą chcesz chronić, musi zawierać co najmniej jedną grupę hostów programu VMM. |
| **Funkcja Hyper-V** |Wymaga co najmniej jeden serwer hosta funkcji Hyper-V w głównych i dodatkowych grup hostów programu VMM i co najmniej jednej maszyny wirtualnej na każdym serwerze hosta funkcji Hyper-V.<br/><br/>Serwery funkcji Hyper-V źródłowa i docelowa musi działać co najmniej Windows Server 2012 z rolą funkcji Hyper-V i mieć zainstalowane najnowsze aktualizacje.<br/><br/>Serwer funkcji Hyper-V zawierający maszyny wirtualne, które chcesz chronić, musi znajdować się w chmurze programu VMM.<br/><br/>Jeśli używasz funkcji Hyper-V w klastrze, należy pamiętać, że broker klastra nie jest tworzony automatycznie w przypadku statycznej klastra oparte na adresie IP. Należy ręcznie skonfigurować brokera klastra. Aby [dowiedzieć się więcej](https://www.petri.com/use-hyper-v-replica-broker-prepare-host-clusters), zobacz wpis na blogu Aidana Finna. |
| **Mapowanie sieci** |Można skonfigurować mapowanie sieci, aby upewnić się, że replikowanych maszyn wirtualnych optymalnie są umieszczane na serwerach hostów funkcji Hyper-V dodatkowej po pracy awaryjnej i czy można nawiązać odpowiednie sieci maszyny Wirtualnej. Jeśli nie skonfigurujesz mapowania sieci, repliki maszyn wirtualnych nie będzie połączona z żadną siecią po pracy awaryjnej.<br/><br/>Aby skonfigurować mapowanie sieci podczas wdrażania, upewnij się, że maszyny wirtualne na serwerze hosta funkcji Hyper-V źródła są połączone z siecią maszyny Wirtualnej programu VMM. Ta sieć powinna połączona z siecią logiczną, która jest skojarzona z chmurą. < br /<br/>Chmura docelowa na pomocniczym serwerze programu VMM używanego do odzyskiwania powinny mieć skonfigurowane odpowiednie sieci maszyny Wirtualnej, a następnie go z kolei powinna być łączona z odpowiedniego sieć logiczną, która jest skojarzona z chmurą docelowej. |
| **Mapowanie magazynu** |Domyślnie podczas replikacji maszyny wirtualnej na serwerze hosta funkcji Hyper-V źródłowego do docelowego serwera hosta funkcji Hyper-V, replikowane dane są przechowywane w lokalizacji domyślnej, określony dla docelowego hosta funkcji Hyper-V w Menedżerze funkcji Hyper-V. Aby uzyskać większą kontrolę nad przechowywania replikowanych danych można skonfigurować mapowania magazynu<br/><br/> Aby skonfigurować mapowanie magazynu, należy skonfigurować klasyfikacje magazynów w źródle i VMM serwery docelowe, przed rozpoczęciem wdrażania. |

## <a name="step-1-create-a-site-recovery-vault"></a>Krok 1. Tworzenie magazynu usługi Site Recovery
1. Zaloguj się do [portalu zarządzania](https://portal.azure.com) z serwera programu VMM, który chcesz zarejestrować.
2. Rozwiń węzeł **usług danych** > **usług odzyskiwania** i kliknij przycisk **magazynie usługi Site Recovery**.
3. Kliknij pozycje **Utwórz nowe** > **Szybkie tworzenie**.
4. W polu **Nazwa** wprowadź przyjazną nazwę identyfikującą magazyn.
5. W **Region** wybierz region geograficzny magazynu. Aby sprawdzić obsługiwane regiony, zobacz sekcję dotyczącą dostępności geograficznej w temacie [Szczegóły cennika usługi Azure Site Recovery](http://go.microsoft.com/fwlink/?LinkId=389880).
6. Kliknij pozycję **Utwórz magazyn**.

    ![Tworzenie magazynu](./media/site-recovery-vmm-to-vmm-classic/create-vault.png)

Na pasku stanu Sprawdź, czy magazyn został utworzony. Magazyn będzie wyświetlany jako **Aktywny** na stronie głównej Usług odzyskiwania.

## <a name="step-2-generate-a-vault-registration-key"></a>Krok 2. Generowanie klucza rejestracji magazynu
Wygeneruj klucz rejestracji magazynu. Po pobraniu dostawcy usługi Azure Site Recovery i zainstalowaniu go na serwerze programu VMM użyjesz tego klucza do zarejestrowania serwera programu VMM w magazynie.

1. Na stronie **Usługi odzyskiwania** kliknij magazyn, aby otworzyć stronę Szybki start. Stronę Szybki start można również otworzyć w dowolnym momencie przy użyciu ikony.

    ![Ikona Szybki start](./media/site-recovery-vmm-to-vmm-classic/quick-start-icon.png)
2. Na liście rozwijanej wybierz **między dwiema lokacjami VMM lokalnymi**.
3. W **Przygotowanie serwerów programu VMM**, kliknij przycisk **Wygeneruj plik klucza rejestracji**. Plik klucza jest generowany automatycznie i ważny przez 5 dni po jego wygenerowaniu. Jeśli nie uzyskujesz dostęp do portalu Azure, z serwera programu VMM, należy skopiować ten plik do serwera.

    ![Klucz rejestracji](./media/site-recovery-vmm-to-vmm-classic/register-key.png)

## <a name="step-3-install-the-azure-site-recovery-provider"></a>Krok 3. Instalowanie dostawcy usługi Azure Site Recovery
1. Na **Szybki Start** strony w **Przygotowanie serwerów programu VMM**, kliknij przycisk **Pobierz Microsoft dostawcy Azure Site Recovery do instalacji na serwerach VMM** Aby uzyskać najnowszą wersję pliku instalacyjnego dostawcy.
2. Uruchom ten plik na źródłowym serwerze programu VMM.

   > [!NOTE]
   > Jeśli program VMM jest wdrożony w klastrze i instalujesz dostawcę po raz pierwszy, zainstaluj go w aktywnym węźle i ukończ instalację, aby zarejestrować serwer programu VMM w magazynie. Następnie zainstaluj dostawcę w pozostałych węzłach. Należy pamiętać, że Jeśli uaktualniasz dostawcę należy uaktualnić we wszystkich węzłach, ponieważ ich powinien wszystkie być uruchomiona ta sama wersja dostawcy.
   >
   >
3. Instalator jest kilka **Sprawdzanie wymagań wstępnych** i żąda uprawnienia do zatrzymania usługi programu VMM w celu rozpoczęcia instalacji dostawcy. Usługa programu VMM zostanie automatycznie ponownie uruchomiona po zakończeniu instalacji. Jeśli instalujesz w klastrze programu VMM, zostanie wyświetlony monit o zatrzymanie roli klastra.
4. W usłudze **Microsoft Update** można włączyć aktualizacje. Po włączeniu tego ustawienia aktualizacje dostawcy będą instalowane zgodnie z zasadami usługi Microsoft Update.

    ![Usługa Microsoft Updates](./media/site-recovery-vmm-to-vmm-classic/ms-update.png)
5. Lokalizacja instalacji jest ustawiona na  **<SystemDrive>\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin**. Kliknij przycisk Zainstaluj, aby rozpocząć instalowanie dostawcy.

    ![InstallLocation](./media/site-recovery-vmm-to-vmm-classic/install-location.png)
6. Po zainstalowaniu dostawcy kliknij pozycję **Zarejestruj**, aby zarejestrować serwer w magazynie.

    ![InstallComplete](./media/site-recovery-vmm-to-vmm-classic/install-complete.png)
7. Zweryfikuj, że w polu **Nazwa magazynu** jest wpisana nazwa magazynu, w którym serwer zostanie zarejestrowany. Kliknij przycisk *Dalej*.

    ![Rejestracja serwera](./media/site-recovery-vmm-to-vmm-classic/vaultcred.PNG)
8. W obszarze **Połączenie internetowe** określ, jak dostawca uruchomiony na serwerze programu VMM łączy się z Internetem. Wybierz pozycję **Połącz z istniejącymi ustawieniami serwera proxy**, aby użyć domyślnych ustawień połączenia internetowego skonfigurowanych na serwerze.

    ![Ustawienia internetowe](./media/site-recovery-vmm-to-vmm-classic/proxydetails.PNG)

   * Jeśli chcesz użyć niestandardowego serwera proxy, należy skonfigurować go przed zainstalowaniem dostawcy. Podczas konfigurowania niestandardowych ustawień serwera proxy wykonywany jest test w celu sprawdzenia połączenia serwera proxy.
   * Jeśli używasz niestandardowego serwera proxy lub domyślny serwer proxy wymaga uwierzytelniania, musisz wprowadzić szczegóły serwera proxy, łącznie z adresem i portem.
   * Następujące adresy URL powinny być dostępne z serwera programu VMM i hostów funkcji Hyper-V
     * *.hypervrecoverymanager.windowsazure.com
     * *.accesscontrol.windows.net
     * *.backup.windowsazure.com
     * *.blob.core.windows.net
     * *.store.core.windows.net
   * Zezwól na adresy IP, opisane w temacie [Azure Datacenter IP Ranges](https://www.microsoft.com/download/confirmation.aspx?id=41653) (Zakresy adresów IP centrum danych Azure), i protokół HTTPS (port 443). Należy również umieścić na liście dozwolonych zakresy adresów IP regionu Azure, który będzie używany, i regionu Zachodnie stany USA.
   * W przypadku użycia niestandardowego serwera proxy konto Uruchom jako programu VMM (DRAProxyAccount) zostanie automatycznie utworzone przy użyciu określonych poświadczeń serwera proxy. Skonfiguruj serwer proxy tak, aby to konto mogło być pomyślnie uwierzytelnione. Ustawienia konta Uruchom jako programu VMM można zmodyfikować w konsoli programu VMM. Aby to zrobić, otwórz obszar roboczy **Ustawienia**, rozwiń pozycję **Zabezpieczenia**, kliknij pozycję **Konta Uruchom jako**, a następnie zmodyfikuj hasło dla konta DRAProxyAccount. Aby to ustawienie zostało zastosowane, należy ponownie uruchomić usługę programu VMM.
9. W oknie **Klucz rejestracji** wybierz klucz, aby potwierdzić, że klucz został pobrany z usługi Azure Site Recovery i skopiowany na serwer programu VMM.
10. Ustawienie szyfrowania jest używane tylko w przypadku replikacji maszyn wirtualnych funkcji Hyper-V w chmurach VMM do platformy Azure. Ustawienie nie jest używane w przypadku replikowania do lokacji dodatkowej.
11. W polu **Nazwa serwera** wprowadź przyjazną nazwę identyfikującą serwer VMM w magazynie. W konfiguracji klastra określ nazwę roli klastra VMM.
12. W oknie **Synchronizacja metadanych chmury** określ, czy chcesz synchronizować metadane dla wszystkich chmur na serwerze programu VMM z magazynem. To działanie ma miejsce tylko raz na każdym serwerze. Jeśli nie chcesz synchronizować wszystkich chmur, możesz nie zaznaczać tego ustawienia i synchronizować poszczególne chmury indywidualnie we właściwościach chmury w konsoli programu VMM.
13. Kliknij przycisk **Dalej**, aby ukończyć proces. Po rejestracji metadane z serwera programu VMM są pobierane przez usługę Azure Site Recovery. Serwer jest wyświetlany w **serwery VMM** > **serwerów** w magazynie.

    ![Serwery](./media/site-recovery-vmm-to-vmm-classic/provider13.PNG)

### <a name="command-line-installation"></a>Instalacja przy użyciu wiersza polecenia
Dostawcy usługi Azure Site Recovery można również zainstalować z poziomu wiersza polecenia. Ta metoda może służyć do zainstalowania dostawcy w RDZENIU serwera dla systemu Windows Server 2012 R2.

1. Pobierz plik instalacyjny dostawcy i klucz rejestracji do folderu. Na przykład C:\ASR.
2. Zatrzymaj usługę programu System Center Virtual Machine Manager
3. Wyodrębnij Instalatora dostawcy, uruchamiając następujące polecenia z wiersza polecenia, używając **administratora** uprawnienia:

        C:\Windows\System32> CD C:\ASR
        C:\ASR> AzureSiteRecoveryProvider.exe /x:. /q
4. Zainstaluj dostawcę, uruchamiając:

        C:\ASR> setupdr.exe /i
5. Zarejestruj dostawcę, uruchamiając:

        CD C:\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin
        C:\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin\> DRConfigurator.exe /r  /Friendlyname <friendly name of the server> /Credentials <path of the credentials file> /EncryptionEnabled <full file name to save the encryption certificate>     

Gdzie parametry są:

* **/ Credentials**: obowiązkowy parametr, który określa lokalizację, w którym znajduje się plik klucza rejestracji  
* **/FriendlyName**: obowiązkowy parametr dla nazwy serwera hosta funkcji Hyper-V, która będzie wyświetlana w portalu usługi Azure Site Recovery.
* **/ EncryptionEnabled**: opcjonalny parametr, który należy użyć tylko w przypadku programu VMM do scenariusza Azure, jeśli potrzebujesz szyfrowania maszyn wirtualnych przechowywanych na platformie Azure. Upewnij się, że nazwa pliku, musisz podać ma **PFX** rozszerzenia.
* **/proxyAddress**: opcjonalny parametr określający adres serwera proxy.
* **/proxyport**: opcjonalny parametr określający port serwera proxy.
* **/ proxyusername**: opcjonalny parametr określający nazwę użytkownika serwera Proxy (Jeśli serwer proxy wymaga uwierzytelniania).
* **/ proxypassword**: opcjonalny parametr określający hasło do uwierzytelniania przy użyciu serwera proxy (Jeśli serwer proxy wymaga uwierzytelniania).  

## <a name="step-4-configure-cloud-protection-settings"></a>Krok 4: Konfigurowanie chmury ustawienia ochrony
Po zarejestrowanych serwerów programu VMM, można skonfigurować ustawienia ochrony chmury. Jeśli włączono opcję **Synchronizuj dane chmury z magazynem** podczas instalowania dostawcy wszystkich chmur na serwerze programu VMM będzie wyświetlane w **chronione elementy** w magazynie. Jeśli użytkownik nie mogą wykonywać synchronizację z usługą Azure Site Recovery w określonej chmurze **ogólne** kartę stronie Właściwości chmury w konsoli programu VMM.

![Opublikowana chmura](./media/site-recovery-vmm-to-vmm-classic/clouds-list.png)

1. Na stronie Szybki start kliknij pozycję **Skonfiguruj ochronę dla chmur programu VMM**.
2. Na **chmur programu VMM** , a następnie wybierz chmurę, który chcesz skonfigurować, a następnie przejdź do **konfiguracji** kartę.
3. W **docelowej**, wybierz pozycję **VMM**.
4. W **lokalizacja docelowa**, wybierz serwer programu VMM na miejscu, który zarządza chmury, którego chcesz użyć do odzyskania.
5. W **Target chmury**, wybierz chmurę docelową, którego chcesz użyć w trybie failover maszyny wirtualnej w chmurze źródło. Należy pamiętać, że:

   * Zaleca się, że wybierz chmurę docelową, który spełnia wymagania odzyskiwania dla maszyn wirtualnych, które będą chronić.
   * Chmury mogą należeć tylko do pary pojedyncza chmura — jako podstawowego lub chmurę docelową.
6. W **częstotliwość kopiowania**, określ, jak często dane mają być synchronizowane między 5he lokalizacja źródłowa i docelowa. Należy pamiętać, że to ustawienie działa tylko po na hoście funkcji Hyper-V działa system Windows Server 2012 R2. Dla innych serwerów używane domyślne ustawienia pięciu minut.
7. W **dodatkowych punktów odzyskiwania**, określ, czy chcesz utworzyć dodatkowe punkty. Wartość domyślna 0 wskazuje, że tylko najnowszy punkt odzyskiwania dla podstawowej maszyny wirtualnej jest przechowywany na serwerze hosta repliki. Należy pamiętać, że włączenie wiele punktów odzyskiwania wymaga dodatkowego magazynu migawek, które są przechowywane w każdym punkcie odzyskiwania. Domyślnie punkty odzyskiwania są tworzone co godzinę, dzięki czemu każdy punkt odzyskiwania zawiera wartość godziny danych. Wartość punktu odzyskiwania, przypisany do maszyny wirtualnej w konsoli programu VMM nie powinna być mniejsza niż wartość przypisać w konsoli usługi Azure Site Recovery.
8. W **częstotliwość migawek spójnych z aplikacją**, określ, jak często mają być tworzone migawki spójne z aplikacjami. Funkcja Hyper-V wykorzystuje dwa typy migawek — standardową migawkę, która jest przyrostową migawką całej maszyny wirtualnej oraz migawkę spójności aplikacji, która wykonuje migawkę danych aplikacji wewnątrz maszyny wirtualnej w danym punkcie w czasie. Migawki spójne z aplikacjami używają usługi Volume Shadow Copy (VSS), aby zapewnić, że aplikacje są w spójnym stanie podczas wykonywania migawki. Należy pamiętać, że jeśli migawki spójne z aplikacjami zostaną włączone, będzie to miało wpływ na wydajność aplikacji uruchomionych na źródłowych maszynach wirtualnych. Upewnij się, że ustawiona wartość jest mniejsza od liczby skonfigurowanych dodatkowych punktów odzyskiwania.

    ![Skonfiguruj ustawienia ochrony](./media/site-recovery-vmm-to-vmm-classic/cloud-settings.png)
9. W **kompresję transferu danych**, określ, czy można kompresować replikowane dane przesyłane.
10. W **uwierzytelniania**, określ, jak uwierzytelnianie ruchu między serwerami hosta funkcji Hyper-V podstawowymi i odzyskiwania. Należy wybrać protokół HTTPS, chyba że masz działającego środowiska Kerberos skonfigurowane. Usługa Azure Site Recovery automatycznie skonfiguruje certyfikatów do uwierzytelniania protokołu HTTPS. Nie jest wymagana żadna konfiguracja ręczna. W przypadku wybrania protokołu Kerberos, biletu protokołu Kerberos będzie używany do wzajemnego uwierzytelniania serwerów hosta. Domyślnie port 8083 i 8084 (dla certyfikatów) zostanie otwarty w Zaporze systemu Windows na serwerach hostów funkcji Hyper-V. Należy pamiętać, że to ustawienie dotyczy tylko serwerów hosta funkcji Hyper-V z systemem Windows Server 2012 R2.
11. W **portu**, zmodyfikuj numer portu, na którym komputery host źródłowy i docelowy nasłuchiwać ruch związany z replikacją. Na przykład zmodyfikuj ustawienie, jeśli chcesz zastosować jakości usług (QoS) sieci przepustowości dla ruchu replikacji. Sprawdź, czy port nie jest używany przez inną aplikację i że jest on otwarty w ustawieniach zapory.
12. W **metodę replikacji**, określ sposób replikacji początkowej danych ze źródła do lokalizacji docelowej obsługi, przed rozpoczęciem replikacji regularne:

    * **Za pośrednictwem sieci**— kopiowanie danych za pośrednictwem sieci może być czasochłonne i użyciem zasobów. Firma Microsoft zaleca, użyj tej opcji, jeśli chmura zawiera maszyny wirtualne z stosunkowo mały wirtualne dyski twarde, a Jeśli lokacja główna jest podłączona do lokacji dodatkowej za pośrednictwem połączenia z szeroką przepustowości. Można określić, że kopia powinien natychmiast rozpocząć lub wybierz godzinę. Replikacji sieci zaleca się zaplanowanie poza godzinami szczytu.
    * **W trybie offline**— ta metoda określa, czy Replikacja początkowa zostanie wykonane przy użyciu nośnika zewnętrznego. Jest przydatne, jeśli chcesz zapobiec spadkowi wydajności sieci lub lokalizacji geograficznie zdalnych. Aby użyć tej metody określeniu lokalizacji plików eksportu w chmurze źródło i lokalizację importu na chmurę docelową. Po włączeniu ochrony dla maszyny wirtualnej, wirtualny dysk twardy jest kopiowany do lokalizacji określonej dla eksportu. Wyślij go do lokacji docelowej, a następnie skopiuj go do lokalizacji importowania. Zaimportowane informacje o jest kopiowany do maszyny wirtualnej repliki.
13. Wybierz **usunąć maszyny wirtualnej repliki** do określenia, czy maszyna wirtualna repliki powinien zostać usunięty, jeśli użytkownik zaprzestanie ochrony maszyny wirtualnej, wybierając **Usuń ochronę dla maszyny wirtualnej** opcji na karcie maszyn wirtualnych właściwości chmury. To ustawienie jest włączone, po wyłączeniu ochrony maszyny wirtualnej zostanie usunięty z usługi Azure Site Recovery, ustawienia usługi Site Recovery dla maszyny wirtualnej są w konsoli programu VMM, i repliki zostaną usunięte.

    ![Skonfiguruj ustawienia ochrony](./media/site-recovery-vmm-to-vmm-classic/cloud-settings-replica.png)

Po zapisaniu ustawień zostanie utworzone zadanie, które można monitorować na karcie **Zadania**. Wszystkie serwery hostów funkcji Hyper-V w źródłowej chmurze programu VMM zostaną skonfigurowane do replikacji. Ustawienia chmury można modyfikować na **Konfiguruj** kartę. Jeśli chcesz zmodyfikować lokalizacji lub docelową chmurę docelową należy usunąć konfigurację chmury, a ponownie skonfigurować chmurę.

### <a name="prepare-for-offline-initial-replication"></a>Przygotuj się do początkowej replikacji offline
Musisz wykonać następujące czynności, aby przygotować się do początkowej replikacji w trybie offline:

* Na serwerze źródłowym można wskazać lokalizacji, z którego eksportu danych będą miały miejsce. Pełna kontrola należy przypisać uprawnienia NTFS i udziału do usługi VMM w ścieżce eksportu. Na serwerze docelowym należy wskazać lokalizacji, z której nastąpi importowania danych. Przypisz te same uprawnienia, w tym ścieżki importu.
* Jeśli ścieżki importu lub eksportu jest udostępniony, należy przypisać administratora, użytkownik zaawansowany, Operator drukowania lub Operator serwera członkostwa grupy dla konta usługi programu VMM na komputerze zdalnym, na którym udostępniony znajduje się.
* Jeśli używasz wszystkich kont Uruchom jako, aby dodać hosty, na ścieżek importu i eksportu, przypisz odczytu Odczyt i zapis do konta Uruchom jako w programie VMM.
* Importowanie i eksportowanie udziałów, nie powinien znajdować się na dowolnym komputerze używanym jako serwer hosta funkcji Hyper-V, ponieważ konfiguracja ze sprzężeniem zwrotnym nie jest obsługiwana przez funkcję Hyper-V.
* W usłudze Active Directory w każdej funkcji Hyper-V serwera hosta, który zawiera maszyny wirtualne, które chcesz chronić, włączyć i skonfigurować delegowanie ograniczone zaufania do komputerów zdalnych, na których ścieżek importu i eksportu znajdują się, w następujący sposób:
  1. Na kontrolerze domeny otwórz **użytkownicy usługi Active Directory i komputery**.
  2. W drzewie konsoli kliknij **DomainName** > **komputerów**.
  3. Kliknij prawym przyciskiem myszy nazwę serwera hosta funkcji Hyper-V > **właściwości**.
  4. Na **delegowania** T kliknij kartę**Rdza temu komputerowi w delegowaniu tylko do określonych usług**.
  5. Kliknij przycisk **Użyj dowolnego protokołu uwierzytelniania**.
  6. Kliknij przycisk **dodać** > **użytkownicy i komputery**.
  7. Wpisz nazwę komputera, który obsługuje ścieżkę eksportu > **OK**. Z listy dostępnych usług, naciśnij i przytrzymaj klawisz CTRL, a następnie kliknij przycisk **cifs** > **OK**. Powtórz dla nazwy komputera, który obsługuje ścieżkę importu. Powtórz w razie potrzeby dodatkowe serwery hosta funkcji Hyper-V.

## <a name="step-5-configure-network-mapping"></a>Krok 5: Konfigurowanie mapowania sieci
1. Na stronie Szybki start kliknij pozycję **Mapuj sieci**.
2. Wybierz źródłowy serwer VMM, z którego chcesz mapowanie sieci, a następnie docelowym serwerze VMM, do którego zostanie zamapowane sieci. Lista źródła sieci i ich sieci docelowej skojarzone są wyświetlane. Wartość pusta jest wyświetlany dla sieci, które nie są obecnie mapowane.
3. Wybierz sieć w **sieci w źródle** > **mapy**. Usługa wykrywa wszystkie sieci maszyny Wirtualnej na serwerze docelowym i wyświetla je. Kliknij ikonę informacji obok nazwy sieciowe źródłowe i docelowe, aby wyświetlić podsieci dla wszystkich sieci.

    ![Konfiguracja mapowania sieci](./media/site-recovery-vmm-to-vmm-classic/network-mapping1.png)
4. W oknie dialogowym wybierz jedną z sieci maszyny Wirtualnej z docelowym serwerze VMM.

    ![Wybieranie sieci docelowej](./media/site-recovery-vmm-to-vmm-classic/network-mapping2.png)
5. Po wybraniu Sieć docelowa liczba chronionych chmur, korzystających z źródłowej sieci są wyświetlane. Wyświetlane są również dostępne docelowych sieci, które są skojarzone z chmury używana na potrzeby ochrony. Zaleca się, że wybrano sieci docelowej, która jest dostępna dla wszystkich chmur, którego używasz do ochrony. Lub można również przejść do serwera programu VMM i modyfikować właściwości chmury w celu dodania sieci logicznej odpowiadający sieci maszyny wirtualnej, który chcesz wybrać.
6. Kliknij znacznik wyboru, aby ukończyć proces mapowania. Zadanie zacznie śledzić postęp mapowania. Umożliwia on **zadania** kartę.

## <a name="step-6-configure-storage-mapping"></a>Krok 6: Konfigurowanie mapowania magazynu
Domyślnie podczas replikacji maszyny wirtualnej na serwerze hosta funkcji Hyper-V źródłowego do docelowego serwera hosta funkcji Hyper-V, replikowane dane są przechowywane w lokalizacji domyślnej, określony dla docelowego hosta funkcji Hyper-V w Menedżerze funkcji Hyper-V. Uzyskać większą kontrolę nad przechowywania replikowanych danych można skonfigurować mapowania magazynu w następujący sposób:

1. Zdefiniuj klasyfikacji magazynu na serwerach VMM źródłowych i docelowych. [Dowiedz się więcej](https://technet.microsoft.com/library/gg610685.aspx). Klasyfikacje muszą być dostępne dla serwerów hostów funkcji Hyper-V w chmurach źródłowym i docelowym. Klasyfikacje nie muszą mieć ten sam typ magazynu. Na przykład można mapować Klasyfikacja źródła, która zawiera udziały SMB w celu Klasyfikacja docelowej, która zawiera udostępnionych woluminów klastra.
2. Po klasyfikacje są na miejscu, można utworzyć mapowania. Aby to zrobić, na **Szybki Start** strony > **mapy magazynu**.
3. Kliknij przycisk **magazynu** kartę > **mapowania klasyfikacji magazynu**.
4. Na **mapowania klasyfikacji magazynu** , wybierz klasyfikacje w źródle i VMM serwery docelowe. Zapisz ustawienia.

    ![Wybieranie sieci docelowej](./media/site-recovery-vmm-to-vmm-classic/storage-mapping.png)

## <a name="step-7-enable-virtual-machine-protection"></a>Krok 7: Włączanie ochrony maszyny wirtualnej
Po poprawnym skonfigurowaniu serwerów, chmur i sieci można włączyć ochronę dla maszyn wirtualnych w chmurze.

1. Na **maszyn wirtualnych** w chmurze, w którym znajduje się maszyny wirtualnej, kliknij pozycję **Włącz ochronę** > **Dodawanie maszyn wirtualnych**.
2. Z listy maszyn wirtualnych w chmurze wybierz maszynę, którą chcesz chronić.

    ![Włączanie ochrony maszyny wirtualnej](./media/site-recovery-vmm-to-vmm-classic/enable-protection.png)
3. Śledzić postęp akcji włączania ochrony w **zadania** kartę, łącznie z replikacją początkową. Po uruchomieniu zadania zakończenia ochrony maszyna wirtualna jest gotowa do pracy awaryjnej. Po włączeniu ochrony i zreplikowaniu maszyn wirtualnych będą one widoczne na platformie Azure.

    ![Zadanie ochrony maszyny wirtualnej](./media/site-recovery-vmm-to-vmm-classic/vm-jobs.png)

> [!NOTE]
> Można również włączyć ochronę maszyn wirtualnych w konsoli programu VMM. Kliknij przycisk **Włącz ochronę** na pasku narzędzi w **usługi Azure Site Recovery** we właściwościach maszyny wirtualnej.
>
>

### <a name="on-board-existing-virtual-machines"></a>Lokalnego istniejące maszyny wirtualne
Jeśli masz istniejące maszyny wirtualne w programie VMM, które są replikowane z funkcji Hyper-V Replica należy dołączyć je do ochrony Azure Site Recovery w następujący sposób:

1. Sprawdź, czy masz głównych i dodatkowych chmurach. Upewnij się, że serwer funkcji Hyper-V hosting istniejącej maszyny wirtualnej znajduje się w chmurze podstawowej i że serwera funkcji Hyper-V obsługującego maszyny wirtualnej repliki znajduje się w chmurze dodatkowej. Upewnij się, że skonfigurowano ustawienia ochrony chmury. Ustawienia powinna odpowiadać tych aktualnie skonfigurowanych dla funkcji Hyper-V Replica. W przeciwnym razie replikację maszyny wirtualnej może nie działać zgodnie z oczekiwaniami.
2. Następnie włącz ochronę na podstawowej maszynie wirtualnej. Azure Site Recovery i VMM zapewnia, że wykrycia tego samego hosta repliki i maszyny wirtualne i usługi Azure Site Recovery spowoduje ponowne użycie i ponownie ustanowić replikację przy użyciu ustawienia skonfigurowane podczas konfigurowania chmury.

## <a name="test-your-deployment"></a>Testowanie wdrożenia
Aby przetestować wdrożenie można uruchomić test trybu failover dla jednej maszyny wirtualnej, lub utworzyć plan odzyskiwania uwzględniający wiele maszyn wirtualnych i testować tryb failover planu.  Próba przejścia w tryb failover symuluje mechanizm pracy awaryjnej i odzyskiwania w sieci izolowanej.

### <a name="create-a-recovery-plan"></a>Tworzenie planu odzyskiwania
1. Na **plany odzyskiwania** , kliknij pozycję **Utwórz Plan odzyskiwania**.
2. Określ nazwę dla planu odzyskiwania i serwerach VMM źródłowych i docelowych. Na serwerze źródłowym musi być maszyn wirtualnych, które są włączone dla trybu failover i odzyskiwania. Wybierz **funkcji Hyper-V** Aby wyświetlić tylko chmury, które są skonfigurowane do replikacji funkcji Hyper-V.

    ![Tworzenie planu odzyskiwania](./media/site-recovery-vmm-to-vmm-classic/recovery-plan1.png)
3. W **Wybieranie maszyny wirtualnej**, wybierz grupy replikacji. Wszystkie maszyny wirtualne powiązane z grupą replikacji zostanie wybrane i dodane do planu odzyskiwania. Te maszyny wirtualne są dodawane do planu odzyskiwania grupy domyślnej — Grupa 1. w razie potrzeby można dodać więcej grup. Należy pamiętać, że po replikacji maszyny wirtualnej rozpocznie zgodnie z kolejnością grup planu odzyskiwania.

    ![Dodaj maszyny wirtualne](./media/site-recovery-vmm-to-vmm-classic/recovery-plan2.png)

Po utworzeniu planu odzyskiwania wygląda na to, na liście na **plany odzyskiwania** kartę.

### <a name="run-a-test-failover"></a>Wykonywanie próby przejścia w tryb failover
1. Na karcie **Plany odzyskiwania** wybierz plan i kliknij pozycję **Test pracy w trybie failover**.
2. Na **potwierdzić testowy tryb Failover** wybierz pozycję **Brak**. Należy pamiętać, że ta opcja włączone nieudane maszyn wirtualnych replik nie będzie podłączona do żadnej sieci. Spowoduje to przetestowanie, że maszyna wirtualna awaryjnie zgodnie z oczekiwaniami, ale nie sprawdza środowiska sieciowego replikacji. Zobacz, jak [testować tryb failover](site-recovery-failover.md) Aby uzyskać więcej informacji o sposobie używania różnych opcji sieciowych.
3. Testowa maszyna wirtualna zostanie utworzona na tym samym hoście jako hosta, na którym znajduje się maszyna wirtualna repliki. Jest ona dodawana do tej samej chmury, w którym znajduje się maszyna wirtualna repliki.

### <a name="run-a-recovery-plan"></a>Uruchom planu odzyskiwania
Po replikacji maszyny wirtualnej repliki nie może być adres IP, który jest taki sam jak adres IP podstawowej maszyny wirtualnej. Maszyny wirtualne spowoduje zaktualizowanie serwera DNS, które używają po rozpoczęciu. Można również dodać skrypt, aby zaktualizować serwer DNS w celu zapewnienia aktualnych aktualizacji.

#### <a name="script-to-retrieve-the-ip-address"></a>Skrypt można pobrać adresu IP
Uruchom ten przykładowy skrypt można pobrać adresu IP.

        $vm = Get-SCVirtualMachine -Name <VM_NAME>
        $na = $vm[0].VirtualNetworkAdapters>
        $ip = Get-SCIPAddress -GrantToObjectID $na[0].id
        $ip.address  

#### <a name="script-to-update-dns"></a>Skrypt w celu zaktualizowania DNS
Uruchom ten przykładowy skrypt, aby zaktualizować usługę DNS, określając adres IP, który można pobrać przy użyciu poprzedniej przykładowy skrypt.

        string]$Zone,
        [string]$name,
        [string]$IP
        )
        $Record = Get-DnsServerResourceRecord -ZoneName $zone -Name $name
        $newrecord = $record.clone()
        $newrecord.RecordData[0].IPv4Address  =  $IP
        Set-DnsServerResourceRecord -zonename $zone -OldInputObject $record -NewInputObject $Newrecord



## <a name="privacy-information-for-site-recovery"></a>Informacje o ochronie prywatności dla usługi Site Recovery
Ta sekcja zawiera informacje o dodatkowych prywatności dla usługi Microsoft Azure Site Recovery ("Usługa"). Aby wyświetlić zasady zachowania poufności informacji dotyczące usług Microsoft Azure, zobacz [Microsoft Azure — zasady zachowania poufności informacji](http://go.microsoft.com/fwlink/?LinkId=324899)

**Funkcja: rejestracji**

* **Jaką pełni funkcję**: rejestruje serwer z usługą, dzięki czemu mogą być chronione maszyny wirtualne
* **Informacje zebrane**: po rejestracji usługa zbiera przetwarza i przesyła informacje o certyfikacie zarządzania z serwera VMM, który ma wyznaczonych do dostarczenia przy użyciu nazwę usługi serwera VMM, a nazwa chmur maszyn wirtualnych na serwerze programu VMM odzyskiwania po awarii.
* **Korzystanie z informacji o**:

  * Certyfikat zarządzania — służy do identyfikacji i uwierzytelniania zarejestrowanego serwera programu VMM w celu uzyskania dostępu do usługi. Usługa używa publicznej części klucza certyfikatu do zabezpieczenia tokenu, który tylko zarejestrowanego serwera programu VMM może uzyskać dostęp do. Serwer musi używać ten token do uzyskiwania dostępu do funkcji usługi.
  * Nazwa serwera programu VMM — nazwa serwera programu VMM jest wymagany do identyfikowania i komunikacji z serwerem VMM odpowiednie, na którym znajdują się chmury.
  * Nazwy z serwera programu VMM w chmurze — wymagana jest nazwa chmury, korzystając z usługi chmury parowanie rozłączania funkcji opisanych poniżej. W przypadku podjęcia decyzji parę z innej chmury odzyskiwania centrum danych chmury z centrum danych podstawowych, są prezentowane nazwy wszystkich chmur z centrum danych odzyskiwania.
* **Wybór**: te informacje są integralną część procesu rejestracji usługi, ponieważ użytkownik i usługi do identyfikowania serwera VMM, dla którego chcesz podać ochrony Azure Site Recovery, a także aby zidentyfikować poprawne zarejestrowanego serwera programu VMM. Jeśli nie chcesz wysyłać tych informacji do usługi, nie należy używać tej usługi. Jeśli zarejestrować serwer, a później chcesz ją wyrejestrować, możesz to zrobić przez usunięcie informacji o serwerze VMM za pomocą portalu usługi, (czyli portalu Azure).

**Funkcja: Włączanie usługi Azure Site Recovery**

* **Jaką pełni funkcję**: dostawcy usługi Azure Site Recovery, zainstalowane na serwerze programu VMM jest kanał komunikacji z usługą. Dostawca jest biblioteki dołączanej (dynamicznie DLL), hostowana w procesie programu VMM. Po zainstalowaniu dostawcy, funkcja "Odzyskiwania centrum danych" pobiera włączona w konsoli administratora programu VMM. Żadnych nowych lub istniejących maszyn wirtualnych w chmurze, można włączyć właściwość o nazwie "Odzyskiwania centrum danych", aby chronić maszyny wirtualnej. Gdy ta właściwość jest ustawiona, dostawca wysyła nazwę i identyfikator maszyny wirtualnej z usługą. Wirtualny jest chroniona przez technologię replikacji systemu Windows Server 2012 lub Windows Server 2012 R2 Hyper-V. Dane maszyny wirtualnej pobiera replikowane z jednego hosta funkcji Hyper-V na inny (zazwyczaj znajduje się w centrum danych różnych "odzyskiwania").
* **Informacje zebrane**: usługa zbiera, procesów i przesyła metadanych dla maszyny wirtualnej, w tym nazwa, identyfikator sieci wirtualnej i nazwę chmury do której on należy.
* **Korzystanie z informacji o**: Usługa powyższe informacje są używane do wypełniania informacji o maszynie wirtualnej w portalu usługi.
* **Wybór**: to jest integralną część usługi i nie można jej wyłączyć. Jeśli nie chcesz, aby te informacje wysyłane do usługi, nie włączaj ochrony Azure Site Recovery żadnych maszyn wirtualnych. Należy pamiętać, że wszystkie dane przesyłane przez dostawcę do usługi są przesyłane za pośrednictwem protokołu HTTPS.

**Funkcji: Plan odzyskiwania**

* **Jaką pełni funkcję**: Ta funkcja pomaga utworzyć plan aranżacji centrum danych "odzyskiwania". Można określić kolejność, w której maszyny wirtualne lub grupy maszyn wirtualnych powinny być uruchamiane w lokacji odzyskiwania. Można również określić wszelkie zautomatyzowanych skryptów do uruchomienia lub any ręczne działania podejmowane w momencie odzyskiwania dla każdej maszyny wirtualnej można. Na poziomie Plan odzyskiwania skoordynowany sposób odzyskiwania zwykle wyzwoleniu pracy awaryjnej (opisane w następnej sekcji).
* **Informacje zebrane**: usługa zbiera, procesów i przesyła metadanych dla planu odzyskiwania, w tym metadanych maszyny wirtualnej, a metadane wszelkich skryptów automatyzacji oraz zawiera informacje o akcji ręcznej.
* **Korzystanie z informacji o**: metadane opisany powyżej jest używany do tworzenia planu odzyskiwania w portalu usługi.
* **Wybór**: to jest integralną część usługi i nie można jej wyłączyć. Jeśli nie chcesz, aby te informacje wysyłane do usługi, nie tworzyć plany odzyskiwania w tej usłudze.

**Funkcja: Mapowanie sieci**

* **Jaką pełni funkcję**: Ta funkcja służy do mapowania informacji o sieci z centrum danych podstawowych odzyskiwania centrum danych. Jeśli maszyny wirtualne są odzyskiwane w lokacji odzyskiwania, to mapowanie pomaga w ustanowienia połączenia sieciowego dla nich.
* **Informacje zebrane**: jako część funkcji mapowania sieci, usługa zbiera przetwarza i przesyła metadanych sieci logiczne dla każdej lokacji (podstawowe i datacenter).
* **Korzystanie z informacji o**: usługa używa metadanych do wypełnienia portalem usługi gdzie możesz mapować informacje o sieci.
* **Wybór**: to jest integralną część usługi i nie można jej wyłączyć. Jeśli nie chcesz, aby te informacje wysyłane do usługi, nie używaj funkcji mapowania sieci.

**Funkcja: Tryb Failover - planowane, niezaplanowanego testów**

* **Jaką pełni funkcję**: funkcja ta umożliwia pracę awaryjną maszyny wirtualnej z jednego centrum danych zarządzanych przez program VMM innego centrum danych zarządzanych przez program VMM. Akcja trybu failover jest wyzwalany przez użytkowników na ich portalu. Możliwe przyczyny trybu failover obejmują nieplanowanego zdarzenia (na przykład w przypadku fizycznych disaster0; to zdarzenie planowane (na przykład datacenter równoważenia obciążenia); test trybu failover (na przykład odzyskiwania planu próba).

Dostawcy na serwerze programu VMM pobiera powiadomienia o zdarzeniu na podstawie usługi, a następnie wykonuje działania trybu failover na hoście funkcji Hyper-V za pośrednictwem interfejsów VMM. Rzeczywista praca w trybie failover maszyny wirtualnej z jednego hosta funkcji Hyper-V na inny (zwykle działających w centrum danych różnych "odzyskiwania") jest obsługiwane przez technologię replikacji w systemie Windows Server 2012 lub Windows Server 2012 R2 Hyper-V. Po zakończeniu pracy awaryjnej dostawcy zainstalowanego na serwerze programu VMM w centrum danych "odzyskiwania" wysyła informacje Powodzenie z usługą.

* **Informacje zebrane**: Usługa użyje powyższe informacje, aby wypełnić stan informacji działania trybu failover w portalu usługi.
* **Korzystanie z informacji o**: usługa korzysta z powyższych informacji w następujący sposób:

  * Certyfikat zarządzania — służy do identyfikacji i uwierzytelniania zarejestrowanego serwera programu VMM w celu uzyskania dostępu do usługi. Usługa używa publicznej części klucza certyfikatu do zabezpieczenia tokenu, który tylko zarejestrowanego serwera programu VMM może uzyskać dostęp do. Serwer musi używać ten token do uzyskiwania dostępu do funkcji usługi.
  * Nazwa serwera programu VMM — nazwa serwera programu VMM jest wymagany do identyfikowania i komunikacji z serwerem VMM odpowiednie, na którym znajdują się chmury.
  * Nazwy z serwera programu VMM w chmurze — wymagana jest nazwa chmury, korzystając z usługi chmury parowanie rozłączania funkcji opisanych poniżej. W przypadku podjęcia decyzji parę z innej chmury odzyskiwania centrum danych chmury z centrum danych podstawowych, są prezentowane nazwy wszystkich chmur z centrum danych odzyskiwania.
* **Wybór**: to jest integralną część usługi i nie można jej wyłączyć. Jeśli nie chcesz, aby te informacje wysyłane do usługi, nie należy używać tej usługi.

## <a name="next-steps"></a>Następne kroki
Po uruchomieniu testowy tryb failover Sprawdź środowisko działa zgodnie z oczekiwaniami, [Dowiedz się więcej o](site-recovery-failover.md) różnego rodzaju przechodzenia w tryb failover.
