---
title: aaaReplicate tooAzure maszyn wirtualnych funkcji Hyper-V w portalu klasycznym hello | Dokumentacja firmy Microsoft
description: "W tym artykule opisano, jak tooreplicate wirtualnego funkcji Hyper-V maszyny tooAzure, gdy komputery nie są zarządzane w chmurach programu VMM."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 3f4c4483-e3dd-495a-bd02-c16e9e28c88d
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 02/21/2017
ms.author: raynew
ms.openlocfilehash: 12d08d950a79e956436cb03ffc87ab40e86c589e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-between-on-premises-hyper-v-virtual-machines-and-azure-without-vmm-with-azure-site-recovery"></a>Replikowanie między maszynami wirtualnymi funkcji Hyper-V lokalnymi i Azure (bez VMM) z usługą Azure Site Recovery
> [!div class="op_single_selector"]
> * [Azure Portal](site-recovery-hyper-v-site-to-azure.md)
> * [Program PowerShell — model usługi Resource Manager](site-recovery-deploy-with-powershell-resource-manager.md)
> * [Klasyczny portal](site-recovery-hyper-v-site-to-azure-classic.md)
>
>

W tym artykule opisano sposób tooreplicate lokalnymi tooAzure maszyn wirtualnych funkcji Hyper-V, za pomocą hello [usługi Azure Site Recovery](site-recovery-overview.md) usługi w hello portalu Azure. W tym scenariuszu serwery funkcji Hyper-V nie są zarządzane w chmurach programu VMM.

Po przeczytaniu tego artykułu, post wszelkie komentarze u dołu hello, lub zadać pytania techniczne na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="site-recovery-in-hello-azure-portal"></a>Odzyskiwanie lokacji w hello portalu Azure

Platforma Azure ma dwa różne [modele wdrażania](../resource-manager-deployment-model.md) związane z tworzeniem zasobów i pracą z nimi — model usługi Azure Resource Manager i model klasyczny. Azure ma dwa portale — hello klasycznego portalu Azure i hello portalu Azure.

W tym artykule opisano sposób toodeploy w portalu klasycznym hello. Hello klasyczny portal może być używane toomaintain istniejących magazynów. Nie można utworzyć nowego magazynów, przy użyciu klasycznego portalu hello.

## <a name="site-recovery-in-your-business"></a>Usługa Site Recovery w Twojej firmie

Organizacje wymagają strategii BCDR, która określa, jak aplikacje i dane pozostają uruchomione i dostępne podczas planowanych lub nieplanowanych przestojów i odzyskać toonormal warunków roboczych możliwie jak. Usługa Site Recovery ma następujące możliwości:

* Ochrona poza siedzibą w przypadku aplikacji biznesowych działających na maszynach wirtualnych funkcji Hyper-V.
* Tooset pojedynczej lokalizacji, zarządzanie i monitorowanie replikacji, trybu failover i odzyskiwania.
* TooAzure proste trybu failover i powrotu po awarii (odzyskać) z serwerami hosta Azure tooHyper-V w lokacji lokalnej.
* Plany odzyskiwania obejmujące wiele maszyn wirtualnych, dzięki którym obciążenia aplikacji w tych samych warstwach przechodzą razem do trybu failover.

## <a name="azure-prerequisites"></a>Wymagania wstępne platformy Azure
* Potrzebujesz konta platformy [Microsoft Azure](https://azure.microsoft.com/). Możesz rozpocząć od [bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).
* Należy toostore replikowane dane konta magazynu platformy Azure. Konto Hello musi włączyć replikację geograficzną. Należy go w tym samym regionie co magazyn usługi Azure Site Recovery hello hello i skojarzone z hello tej samej subskrypcji. [Dowiedz się więcej na temat usługi Azure storage](../storage/common/storage-introduction.md). Należy pamiętać, że nie obsługujemy Przenoszenie konta magazynu utworzone za pomocą hello [nowego portalu Azure](../storage/common/storage-create-storage-account.md) między grupami zasobów.
* Tak, aby maszyny wirtualne platformy Azure tooa połączonych sieci podczas przejścia w tryb failover z lokacji głównej należy sieci wirtualnej platformy Azure.

## <a name="hyper-v-prerequisites"></a>Wymagania wstępne funkcji Hyper-V
* W lokacji lokalnej źródła hello będziesz potrzebować co najmniej jeden serwer z systemem **systemu Windows Server 2012 R2** z zainstalowaną rolą funkcji Hyper-V hello lub **Microsoft Hyper-V Server 2012 R2**. Ten serwer należy:
* Zawiera co najmniej jednej maszyny wirtualnej.
* Być połączone toohello Internetu, bezpośrednio lub za pośrednictwem serwera proxy.
* Działać poprawki hello opisaną w artykule KB [2961977](https://support.microsoft.com/en-us/kb/2961977 "KB2961977").

## <a name="virtual-machine-prerequisites"></a>Wymagania wstępne dotyczące maszyny wirtualnej
Maszyny wirtualne mają tooprotect powinna być zgodna z [wymagania maszyny wirtualnej platformy Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).

## <a name="provider-and-agent-prerequisites"></a>Dostawca i agent wymagania wstępne
Jako część wdrożenia usługi Azure Site Recovery możesz zainstalować hello dostawcy usługi Azure Site Recovery i hello agenta usług odzyskiwania Azure na każdym serwerze funkcji Hyper-V. Należy pamiętać, że:

* Zalecamy zawsze uruchamiaj hello najnowsze wersje hello dostawca i agent. Są one dostępne w portalu usługi Site Recovery hello.
* Wszystkie serwery funkcji Hyper-V w magazynie powinny mieć hello tej samej wersji hello dostawca i agent.
* Witaj dostawca uruchomiony na serwerze hello łączy tooSite odzyskiwania za pośrednictwem hello internet. Można to zrobić bez serwera proxy, ustawienia serwera proxy hello obecnie skonfigurowany na serwerze funkcji Hyper-V hello lub niestandardowych ustawień serwera proxy konfigurowanych podczas instalacji dostawcy. Należy upewnić się, czy ten serwer proxy hello ma toouse mogą uzyskiwać dostęp do tych adresów URL hello podłączania tooAzure toomake:

  * *.accesscontrol.windows.net
  * *.backup.windowsazure.com
  * *.hypervrecoverymanager.windowsazure.com
  * *.store.core.windows.net      
  * *.blob.core.windows.net
  - https://www.msftncsi.com/ncsi.txt
  - time.windows.com
  - time.nist.gov
* Ponadto Zezwalaj hello adresy IP, opisane w [zakresów IP centrum danych Azure](https://www.microsoft.com/download/details.aspx?id=41653) i protokół HTTPS (port 443). Masz zakresów IP hello tooallow hello region platformy Azure, możesz zaplanować toouse i zachodnie stany USA.

Ta grafika przedstawia kanałów komunikacyjnych różnych hello i porty używane przez usługę Site Recovery do aranżacji i replikacji

![Topologia B2A](./media/site-recovery-hyper-v-site-to-azure-classic/b2a-topology.png)

## <a name="step-1-create-a-vault"></a>Krok 1: Tworzenie magazynu
1. Zaloguj się toohello [portalu zarządzania](https://portal.azure.com).
2. Rozwiń węzeł **usług danych** > **usług odzyskiwania** i kliknij przycisk **magazynie usługi Site Recovery**.
3. Kliknij pozycje **Utwórz nowe** > **Szybkie tworzenie**.
4. W **nazwa**, wprowadź przyjazną nazwę tooidentify hello magazynu.
5. W **Region**, wybierz hello region geograficzny magazynu hello. toocheck obsługiwane regiony, zobacz dotyczącą dostępności geograficznej w [szczegóły cennika usługi Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).
6. Kliknij pozycję **Utwórz magazyn**.

    ![Nowy magazyn](./media/site-recovery-hyper-v-site-to-azure-classic/vault.png)

Sprawdź, czy hello tooconfirm paska stanu, który hello magazynu został pomyślnie utworzony. Witaj magazyn będzie wyświetlany jako **Active** na powitania głównej strony usług odzyskiwania.

## <a name="step-2-create-a-hyper-v-site"></a>Krok 2: Tworzenie lokacji funkcji Hyper-V
1. Na stronie powitania usług odzyskiwania kliknij strony Szybki Start hello tooopen magazynu hello. Szybki Start można również otworzyć w dowolnym momencie, korzystając z ikony hello.

    ![Szybki start](./media/site-recovery-hyper-v-site-to-azure-classic/quick-start-icon.png)
2. Z listy rozwijanej hello wybierz **między lokalną lokacją funkcji Hyper-V i platformą Azure**.

    ![Scenariusz lokacji funkcji Hyper-V](./media/site-recovery-hyper-v-site-to-azure-classic/select-scenario.png)
3. W **tworzenia lokacji funkcji Hyper-V** kliknij **lokacji funkcji Hyper-V Utwórz**. Określ nazwę lokacji i Zapisz.

    ![Lokacja funkcji Hyper-V](./media/site-recovery-hyper-v-site-to-azure-classic/create-site.png)

## <a name="step-3-install-hello-provider-and-agent"></a>Krok 3: Instalowanie hello dostawca i agent
Zainstaluj hello dostawca i agent na każdym serwerze funkcji Hyper-V, który ma tooprotect maszyny wirtualne.

Jeśli instalujesz w klastrze funkcji Hyper-V, wykonuje kroki 5-11 na każdym węźle klastra trybu failover hello. Po wszystkie węzły są zarejestrowane i jest chroniony, nawet w przypadku migrowania między węzłami w klastrze hello będą chronione maszyny wirtualne.

1. W **serwerów funkcji Hyper-V przygotowanie**, kliknij przycisk **Pobierz klucz rejestracji** pliku.
2. Na powitania **Pobierz klucz rejestracji** kliknij przycisk **Pobierz** dalej toohello lokacji. Pobierz hello tooa kluczy bezpiecznej lokalizacji, która mogą łatwo uzyskiwać hello funkcji Hyper-V server. klucz Hello jest ważny przez 5 dni po jego wygenerowaniu.

    ![Klucz rejestracji](./media/site-recovery-hyper-v-site-to-azure-classic/download-key.png)
3. Kliknij przycisk **hello pobierania dostawcy** tooobtain hello najnowszej wersji.
4. Uruchom plik hello na każdym serwerze funkcji Hyper-V, które mają tooregister w magazynie hello. Plik Hello instaluje dwa składniki:
   * **Dostawca usługi Azure Site Recovery**— obsługuje komunikację i aranżacji między serwerem hello funkcji Hyper-V i hello portalu usługi Azure Site Recovery.
   * **Agent usług odzyskiwania Azure**— obsługuje transportu danych między maszynami wirtualnymi na powitania serwera źródłowego funkcji Hyper-V i Magazyn Azure.
5. W usłudze **Microsoft Update** można włączyć aktualizacje. To ustawienie jest włączone, dostawca i Agent aktualizacje będą instalowane zgodnie z zasadami Microsoft Update tooyour.

    ![Usługa Microsoft Updates](./media/site-recovery-hyper-v-site-to-azure-classic/provider1.png)
6. W **instalacji** określić, gdzie hello tooinstall dostawca i Agent na hello serwera funkcji Hyper-V.

    ![Lokalizacja instalacji](./media/site-recovery-hyper-v-site-to-azure-classic/provider2.png)
7. Po zakończeniu instalacji kontynuuj Instalator tooregister powitania serwera w magazynie hello.
8. Na powitania **ustawienia magazynu** kliknij przycisk **Przeglądaj** pliku klucza hello tooselect. Określ subskrypcję usługi Azure Site Recovery hello, hello nazwę magazynu, i należy serwer hello funkcji Hyper-V toowhich hello funkcji Hyper-V w lokacji.

    ![Rejestracja serwera](./media/site-recovery-hyper-v-site-to-azure-classic/provider8.PNG)
9. Na powitania **połączenia internetowego** strony, należy określić, jak hello dostawcy łączy tooAzure usługi Site Recovery. Wybierz **Użyj domyślnych ustawień serwera proxy systemu** toouse hello domyślnych ustawień połączenia internetowego skonfigurowane na powitania serwera. Jeśli nie określisz wartości domyślne hello, ustawienia będą stosowane.

   ![Ustawienia internetowe](./media/site-recovery-hyper-v-site-to-azure-classic/provider7.PNG)
10. Rozpoczyna się rejestracja tooregister powitania serwera w magazynie hello.

    ![Rejestracja serwera](./media/site-recovery-hyper-v-site-to-azure-classic/provider15.PNG)
11. Po zakończeniu rejestracji metadane z hello funkcji Hyper-V server są pobierane przez usługę Azure Site Recovery i serwer hello jest wyświetlany na powitania **Lokacje funkcji Hyper-V** kartę na powitania **serwerów** strony w magazynie hello.

### <a name="install-hello-provider-from-hello-command-line"></a>Zainstaluj z wiersza polecenia hello hello dostawcy
Jako alternatywę można zainstalować z wiersza polecenia hello hello dostawcy usługi Azure Site Recovery. Należy używać tej metody, jeśli chcesz, aby tooinstall hello dostawcy na komputerze z systemem Windows Server Core 2012 R2. Uruchom z wiersza polecenia hello w następujący sposób:

1. Pobierz hello dostawcy plików i rejestracji klucza tooa folder instalacji. Na przykład C:\ASR.
2. Uruchom wiersz polecenia jako Administrator i wpisz:

        C:\Windows\System32> CD C:\ASR
        C:\ASR> AzureSiteRecoveryProvider.exe /x:. /q
3. Następnie zainstaluj hello dostawcy, uruchamiając:

        C:\ASR> setupdr.exe /i
4. Uruchom po zarejestrowaniu toocomplete hello:

        CD C:\Program Files\Microsoft Azure Site Recovery Provider
        C:\Program Files\Microsoft Azure Site Recovery Provider\> DRConfigurator.exe /r  /Friendlyname <friendly name of hello server> /Credentials <path of hello credentials file> /EncryptionEnabled <full file name toosave hello encryption certificate>         

Gdzie parametry obejmują:

* **/ Credentials**: Określ lokalizację hello hello klucza rejestracji pobrany.
* **/ FriendlyName**: Określ serwer hosta funkcji Hyper-V hello tooidentify nazwa. Ta nazwa będzie wyświetlana w portalu hello
* **/ EncryptionEnabled**: opcjonalne. Określ, czy tooencrypt maszyn wirtualnych repliki na platformie Azure (szyfrowanie danych w rest).
* **/ proxyaddress**; **/proxyport**; **/proxyusername**; **/proxypassword**: opcjonalne. Określ parametry serwera proxy, jeśli chcesz toouse niestandardowego serwera proxy lub istniejący serwer proxy wymaga uwierzytelniania.

## <a name="step-4-create-an-azure-storage-account"></a>Krok 4. Tworzenie konta magazynu platformy Azure
* W **przygotowanie zasobów** wybierz **Utwórz konto magazynu** toocreate konta magazynu Azure, jeśli nie masz. Witaj, konto musi mieć włączoną replikacją geograficzną. Należy go w tym samym regionie co magazyn usługi Azure Site Recovery hello hello i skojarzone z hello tej samej subskrypcji.

    ![Tworzenie konta magazynu](./media/site-recovery-hyper-v-site-to-azure-classic/create-resources.png)

> [!NOTE]
> 1. Firma Microsoft nie obsługuje przenoszenia hello kont magazynu utworzonych przy użyciu hello [nowego portalu Azure](../storage/common/storage-create-storage-account.md) między grupami zasobów.
> 2. [Migracji kont magazynu](../azure-resource-manager/resource-group-move-resources.md) między zasobów grup poziomu hello tej samej subskrypcji lub różnych subskrypcji nie jest obsługiwana dla konta magazynu służące do wdrażania usługi Site Recovery.
>

## <a name="step-5-create-and-configure-protection-groups"></a>Krok 5: Tworzenie i konfigurowanie grup ochrony
Logiczne grupowanie są grupy ochrony za pomocą tooprotect hello maszyn wirtualnych, które mają takie same ustawienia ochrony. Zastosuj grupy ochrony tooa ustawienia ochrony, a te ustawienia są stosowane tooall maszyn wirtualnych, dodanie toohello grupy.

1. W **Utwórz i skonfiguruj grupy ochrony** kliknij **Utwórz grupę ochrony**. Jeśli wszystkie wymagania wstępne nie są stosowane wydawane wiadomości, można kliknąć **wyświetlić szczegóły** Aby uzyskać więcej informacji.
2. W hello **grup ochrony** Dodaj grupę ochrony. Określ nazwę, hello lokacji źródłowej funkcji Hyper-V i docelowy hello **Azure**, Nazwa subskrypcji usługi Azure Site Recovery i hello kontem magazynu platformy Azure.

    ![Grupy ochrony](./media/site-recovery-hyper-v-site-to-azure-classic/protection-group.png)
3. W **ustawienia replikacji** hello zestaw **częstotliwość kopiowania** toospecify częstotliwość hello przyrost danych mają być synchronizowane między hello źródłowe i docelowe. Można ustawić too30 sekund, 5 minut lub 15 minut.
4. W **Zachowaj punkty odzyskiwania** Określ, ile godzin historii odzyskiwania powinny być przechowywane.
5. W **częstotliwość migawek spójnych z aplikacją** można określić, czy migawki tootake wykorzystujące tooensure usługi kopiowania woluminów w tle (VSS), które aplikacje są w spójnym stanie podczas hello migawki. Domyślnie nie są one uwzględnione. Upewnij się, że ta wartość jest ustawiana tooless niż hello liczba punktów odzyskiwania dodatkowe, które można skonfigurować. To ustawienie jest obsługiwane tylko, jeśli maszyna wirtualna hello jest uruchomiona w systemie operacyjnym Windows.
6. W **czas rozpoczęcia replikacji początkowej** Określ, kiedy początkowej replikacji maszyn wirtualnych w grupie ochrony hello mają być wysyłane tooAzure.

    ![Grupy ochrony](./media/site-recovery-hyper-v-site-to-azure-classic/protection-group2.png)

## <a name="step-6-enable-virtual-machine-protection"></a>Krok 6: Włączanie ochrony maszyny wirtualnej
Dodaj maszyny wirtualne tooa ochrony grupy tooenable ich ochronę.

> [!NOTE]
> Ochrona maszyn wirtualnych z systemem Linux ze statycznym adresem IP nie jest obsługiwana.
>
>

1. Na powitania **maszyny** grupy dla grupy ochrony hello, kliknij przycisk ** Dodaj maszyny wirtualne tooprotection tooenable ochrony **.
2. Na powitania **Włącz ochronę maszyny wirtualnej** hello wybierz maszyny wirtualne mają tooprotect strony.

    ![Włączanie ochrony maszyny wirtualnej](./media/site-recovery-hyper-v-site-to-azure-classic/add-vm.png)

    rozpoczyna się zadania ochrony włączyć Hello. Możesz śledzić postępy na powitania **zadania** kartę. Po hello zadanie zakończenia ochrony maszyna wirtualna działa hello jest gotowy do trybu failover.
3. Po ochrony jest konfigurowanie można wykonywać następujące czynności:

   * Wyświetl maszyn wirtualnych w **chronione elementy** > **grup ochrony** > *protectiongroup_name*  >  **Maszyn wirtualnych** można przejść do szczegółów w dół szczegóły toomachine w hello **właściwości** kartę...
   * Skonfiguruj właściwości trybu failover powitania dla maszyn wirtualnych, w **chronione elementy** > **grup ochrony** > *protectiongroup_name*  >  **Maszyn wirtualnych** *virtual_machine_name* > **Konfiguruj**. Można skonfigurować:

     * **Nazwa**: Nazwa hello hello maszyny wirtualnej na platformie Azure.
     * **Rozmiar**: hello rozmiar docelowy hello maszyny wirtualnej, który zakończy się niepowodzeniem przez.

       ![Skonfiguruj właściwości maszyny wirtualnej](./media/site-recovery-hyper-v-site-to-azure-classic/vm-properties.png)
   * Skonfiguruj ustawienia dodatkowe maszyny wirtualnej w *chronione elementy** > **grup ochrony** > *protectiongroup_name* > **maszyn wirtualnych** *virtual_machine_name* > **Konfiguruj**, takie jak:

     * **Karty sieciowe**: hello liczbę kart sieciowych jest zależna hello rozmiaru określonego dla docelowej maszyny wirtualnej hello. Sprawdź [specyfikacje rozmiaru maszyny wirtualnej](../virtual-machines/linux/sizes.md) hello liczbę kart sieciowych obsługiwanych przez hello rozmiar maszyny wirtualnej.

       Podczas modyfikowania hello rozmiar maszyny wirtualnej i Zapisz ustawienia hello hello numer karty sieciowej ulegnie zmianie po otwarciu **Konfiguruj** hello stronę następnym razem. Hello liczbę kart sieciowych docelowych maszyn wirtualnych jest minimalną hello liczbę kart sieciowych na źródłowej maszynie wirtualnej i maksymalną liczbę kart sieciowych obsługiwanych przez rozmiar hello hello maszyny wirtualnej. Objaśniono poniżej:

       * Jeśli hello liczbę kart sieciowych na maszynie źródłowej hello jest mniejsza lub równa toohello liczba kart dozwoloną dla rozmiaru maszyny docelowej hello, a następnie hello docelowa będzie mieć hello samą liczbę kart sieciowych jako źródło hello.
       * Jeśli hello liczbę kart sieciowych dla źródłowej maszyny wirtualnej hello przekracza liczbę hello dozwoloną dla hello rozmiar docelowy, a następnie maksymalny rozmiar docelowy hello będą używane.
       * Na przykład jeśli maszyna źródłowa ma dwie karty sieciowe i rozmiaru maszyny docelowej hello obsługuje cztery karty, maszyna docelowa hello będzie mieć dwie karty sieciowe. Jeśli hello maszyna źródłowa ma dwie karty sieciowe, ale hello rozmiar docelowy obsługiwanych obsługuje tylko jedną maszyna docelowa hello będzie mieć tylko jedną kartę.

     * **Sieć platformy Azure**: Określ maszyny wirtualnej hello toowhich sieci hello w trybie Failover. Jeśli maszyna wirtualna hello ma wiele kart sieciowych wszystkich kart powinien toohello połączonych tej samej sieci platformy Azure.
     * **Podsieci** dla każdej karty sieciowej na maszynie wirtualnej hello podsieci wybierz hello hello sieć platformy Azure toowhich hello maszynie należy łączyć po pracy awaryjnej.
     * **Docelowy adres IP**: Jeśli hello karta sieciowa źródłowej maszyny wirtualnej jest skonfigurowany toouse statycznych adresów IP, następnie można określić hello adresu IP dla docelowej maszyny wirtualnej tooensure hello, który hello maszyny ma hello tego samego adresu IP po trybu failover .  Jeśli nie określisz adresu IP dowolny dostępny adres zostanie przypisana w momencie hello pracy awaryjnej. Określ adres, który jest używany następnie trybu failover zakończy się niepowodzeniem.

     > [!NOTE]
     > [Migracja sieci](../azure-resource-manager/resource-group-move-resources.md) między zasobów grup poziomu hello tej samej subskrypcji lub różnych subskrypcji nie jest obsługiwana dla sieci używane do wdrażania usługi Site Recovery.
     >

     ![Skonfiguruj właściwości maszyny wirtualnej](./media/site-recovery-hyper-v-site-to-azure-classic/multiple-nic.png)




## <a name="step-7-create-a-recovery-plan"></a>Krok 7: Tworzenie planu odzyskiwania
W kolejności tootest hello wdrożenia możesz uruchomić test trybu failover dla jednej maszyny wirtualnej lub plan odzyskiwania, który zawiera co najmniej jednej maszyny wirtualnej. [Dowiedz się więcej](site-recovery-create-recovery-plans.md) o tworzeniu planu odzyskiwania.

## <a name="step-8-test-hello-deployment"></a>Krok 8: Testowanie wdrożenia hello
Istnieją dwa sposoby toorun tooAzure pracy awaryjnej testu.

* **Testowanie trybu failover bez sieci platformy Azure**— ten test trybu failover sprawdza, czy maszyna wirtualna hello funkcjonuje poprawnie na platformie Azure. Witaj maszyny wirtualnej nie będzie tooany połączonych sieci platformy Azure po pracy awaryjnej.
* **Testowanie trybu failover z siecią platformy Azure**— tego typu kontrole trybu failover, które hello całe środowisko replikacji funkcjonuje zgodnie z oczekiwaniami i tryb failover maszyny wirtualne hello łączy toohello określonego docelową sieć platformy Azure. Należy pamiętać, że do testowania trybu failover podsieci hello hello testowej maszyny wirtualnej będzie można znalezienia oparty na powitania podsieci maszyny wirtualnej repliki hello. Jest to inny tooregular replikacji, gdy hello podsieci maszyny wirtualnej repliki jest oparta na podsieci hello hello źródłowej maszyny wirtualnej.

Jeśli chcesz toorun test trybu failover bez określenia sieci platformy Azure nie trzeba tooprepare żadnych czynności.

toorun test trybu failover z docelową siecią platformy Azure, konieczne będzie toocreate nowej sieci platformy Azure, która jest odizolowana od sieci platformy Azure środowiska produkcyjnego (domyślne zachowanie podczas tworzenia nowej sieci na platformie Azure). Odczyt [testować tryb failover](site-recovery-failover.md) więcej szczegółów.

toofully przetestować wdrożenie replikacji i sieci należy tooset się hello infrastruktury, więc ten hello replikowane toowork maszyny wirtualnej, zgodnie z oczekiwaniami. Jednym ze sposobów wykonywania tootooset tej maszyny wirtualnej jako kontroler domeny z serwerem DNS i replikować go tooAzure przy użyciu usługi Site Recovery toocreate go w teście hello sieci, uruchamiając test trybu failover.  [Dowiedz się więcej](site-recovery-active-directory.md#test-failover-considerations) dotyczących testu pracy awaryjnej dla usługi Active Directory.

Uruchom hello testowy tryb failover w następujący sposób:

> [!NOTE]
> tooget hello najlepszą wydajność po wykonaniu tooAzure trybu failover, upewnij się, czy zostały zainstalowane hello Azure agenta hello chronione maszyny. Ułatwia do szybsze uruchamianie i diagnozowanie w przypadku wystąpienia problemów. Agenta systemu Linux można znaleźć [tutaj](https://github.com/Azure/WALinuxAgent), a agenta systemu Windows można znaleźć [tutaj](http://go.microsoft.com/fwlink/?LinkID=394789).
>
>

1. Na powitania **plany odzyskiwania** , a następnie wybierz hello plan i kliknij przycisk **testowy tryb Failover**.
2. Na powitania **potwierdzić testowy tryb Failover** wybierz **Brak** lub określoną sieć platformy Azure.  Należy pamiętać, że w przypadku wybrania **Brak** hello testowy tryb failover sprawdzi hello maszyny wirtualnej została zreplikowana poprawnie tooAzure, ale nie Sprawdzanie konfiguracji sieci replikacji.

    ![Testowanie trybu failover](./media/site-recovery-hyper-v-site-to-azure-classic/test-nonetwork.png)
3. Na powitania **zadania** można śledzić postęp trybu failover. Należy także stanie toosee hello testowa replika maszyny wirtualnej w hello portalu Azure. Jeśli ustawisz zapasowych tooaccess maszyn wirtualnych z sieci lokalnej można zainicjować maszyny wirtualnej toohello połączenia pulpitu zdalnego.
4. Gdy hello w tryb failover osiągnie hello **Ukończ testowanie** fazy, kliknij przycisk **Zakończ Test** toofinish się hello testowy tryb failover. Użytkownik może przejść do szczegółów toohello **zadania** karcie tootrack postęp trybu failover, a stan i tooperform wszystkie akcje, które są potrzebne.
5. Po pracy awaryjnej będziesz w stanie toosee hello testowa replika maszyny wirtualnej w portalu Azure hello. Jeśli ustawisz zapasowych tooaccess maszyn wirtualnych z sieci lokalnej można zainicjować maszyny wirtualnej toohello połączenia pulpitu zdalnego.

   1. Sprawdź pomyślnie uruchomić hello maszyn wirtualnych.
   2. Maszyna wirtualna toohello tooconnect na platformie Azure przy użyciu pulpitu zdalnego po hello w tryb failover, należy włączyć Podłączanie pulpitu zdalnego na maszynie wirtualnej hello przed rozpoczęciem powitalne testowy tryb failover. Należy również tooadd punkt końcowy protokołu RDP na maszynie wirtualnej hello. Można wykorzystać [runbook usługi Automatyzacja Azure](site-recovery-runbook-automation.md) toodo który.
   3. Po pracy awaryjnej Jeśli używasz publicznego adresu IP address tooconnect toohello maszynę wirtualną na platformie Azure przy użyciu pulpitu zdalnego, upewnij się, nie masz żadnych zasad domeny, które uniemożliwiają połączenie tooa maszyny wirtualnej przy użyciu adresu publicznego.
6. Po zakończeniu testowania hello hello następujące:

   * Kliknij przycisk **hello testu przejścia w tryb failover**. Czyszczenie hello test środowiska tooautomatically zasilania poza i Usuń hello testowe maszyny wirtualne.
   * Kliknij przycisk **uwagi** toorecord i zapisać wszelkie obserwacje związane z hello testowy tryb failover.
7. Gdy hello w tryb failover osiągnie hello **Ukończ testowanie** fazy zakończenia weryfikacji hello w następujący sposób:
   1. Widok hello maszyny wirtualnej repliki w hello portalu Azure. Sprawdź, czy hello maszyny wirtualnej zostanie uruchomiony pomyślnie.
   2. Jeśli ustawisz zapasowych tooaccess maszyn wirtualnych z sieci lokalnej można zainicjować maszyny wirtualnej toohello połączenia pulpitu zdalnego.
   3. Kliknij przycisk **hello pełny test** toofinish go.
   4. Kliknij przycisk **uwagi** toorecord i zapisać wszelkie obserwacje związane z hello testowy tryb failover.
   5. Kliknij przycisk **hello testu przejścia w tryb failover**. Czyszczenie hello test środowiska tooautomatically zasilania poza i Usuń hello testowej maszyny wirtualnej.

## <a name="next-steps"></a>Następne kroki
Po skonfigurowaniu i uruchomieniu wdrożenia [dowiedz się więcej](site-recovery-failover.md) o trybie failover.
