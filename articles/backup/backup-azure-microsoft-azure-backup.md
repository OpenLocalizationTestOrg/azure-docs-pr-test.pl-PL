---
title: "tooback serwer kopii zapasowej Azure aaaUse zapasową obciążeń tooAzure | Dokumentacja firmy Microsoft"
description: "Użyj tooprotect serwer kopii zapasowej Azure lub utworzyć kopię zapasową obciążeń toohello portalu Azure."
services: backup
documentationcenter: 
author: PVRK
manager: shivamg
editor: 
keywords: "Serwer kopii zapasowej systemu Azure; chronić obciążenia; Tworzenie kopii zapasowej obciążeń"
ms.assetid: e7fb1907-9dc1-4ca1-8c61-50423d86540c
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/20/2017
ms.author: masaran;trinadhk;pullabhk;markgal
ms.openlocfilehash: a99b2919ffd44c6133960e3a935038a2bb1281c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="preparing-tooback-up-workloads-using-azure-backup-server"></a>Przygotowywanie tooback dużych obciążeń, za pomocą serwera usługi Kopia zapasowa Azure
> [!div class="op_single_selector"]
> * [Azure Backup Server](backup-azure-microsoft-azure-backup.md)
> * [SCDPM](backup-azure-dpm-introduction.md)
>
>

W tym artykule opisano sposób tooprepare tooback Twojego środowiska dużych obciążeń, za pomocą serwera usługi Kopia zapasowa Azure. Serwer kopii zapasowej Azure umożliwia ochronę obciążeń aplikacji, takich jak maszyn wirtualnych funkcji Hyper-V, programu Microsoft SQL Server, SharePoint Server, Microsoft Exchange i klientów systemu Windows z poziomu pojedynczej konsoli.

> [!NOTE]
> Serwer kopii zapasowej systemu Azure mogą teraz chronić maszyny wirtualne VMware i zapewnia lepsze zabezpieczenia możliwości. Zainstaluj produkt hello zgodnie z objaśnieniem w sekcjach hello poniżej; zastosowanie aktualizacji 1 i hello najnowsza wersja agenta kopii zapasowej Azure. toolearn więcej informacji na temat tworzenia kopii zapasowej serwerów VMware serwer kopii zapasowej Azure, zobacz artykuł hello [tooback serwer kopii zapasowej Azure Użyj serwera VMware](backup-azure-backup-server-vmware.md). toolearn o funkcjach zabezpieczeń, można znaleźć zbyt[dokumentacji funkcji zabezpieczeń kopii zapasowej platformy Azure](backup-azure-security-feature.md).
>
>

Można również chronić infrastrukturę jako obciążeń usługę (IaaS), takich jak maszyny wirtualne na platformie Azure.

> [!NOTE]
> Platforma Azure ma dwa modele wdrażania związane z tworzeniem i pracą z zasobami: [Resource Manager i Model Klasyczny](../azure-resource-manager/resource-manager-deployment-model.md). Ten artykuł zawiera hello informacje i procedury dotyczące przywracania maszyn wirtualnych wdrożonych przy użyciu hello modelu Resource Manager.
>
>

Serwer kopii zapasowej systemu Azure dziedziczy podobne funkcje tworzenia kopii zapasowej obciążeń hello z programu Data Protection Manager (DPM). W tym artykule łączy tooexplain dokumentacji tooDPM niektóre hello udostępnione funkcje. Jeśli serwer usługi Kopia zapasowa Azure udostępnia znacznie hello same funkcje co program DPM. Serwer kopii zapasowej systemu Azure nie obsługuje tworzenia kopii zapasowej tootape, ani nie jest zintegrowana z programem System Center.

## <a name="1-choose-an-installation-platform"></a>1. Wybierz platformy instalacji
pierwszym krokiem Hello kierunku uruchamianie hello Azure Utwórz kopię zapasową serwera w i przeprowadzanie jest tooset serwera systemu Windows. Serwer może być w Azure lub lokalnie.

### <a name="using-a-server-in-azure"></a>Przy użyciu serwera w systemie Azure
W przypadku wybierania serwera do uruchamiania serwera usługi Kopia zapasowa Azure, zalecane jest początkowo galerii systemu Windows Server 2012 R2 Datacenter. Artykuł Hello [tworzenie pierwszej maszyny wirtualnej systemu Windows w portalu Azure hello](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), zapewnia samouczek wprowadzenie hello zalecane maszyny wirtualnej platformy Azure, nawet jeśli nie znasz Azure przed. Witaj zalecane minimalne wymagania dla maszyny wirtualnej serwera hello (VM) powinny być: A2 standardowo dwa rdzenie i 3.5 GB pamięci RAM.

Ochrona obciążenia za pomocą serwera usługi Kopia zapasowa Azure ma wiele wszystkie szczegóły. Artykuł Hello [zainstalować program DPM jako maszyny wirtualnej platformy Azure](https://technet.microsoft.com/library/jj852163.aspx), pomaga opisano te wszystkie szczegóły. Przed wdrożeniem maszyny hello, całkowicie odczytane w tym artykule.

### <a name="using-an-on-premises-server"></a>Za pomocą lokalnego serwera
Jeśli nie chcesz, aby toorun powitania serwera podstawowego na platformie Azure, można uruchomić serwera hello na maszynie Wirtualnej funkcji Hyper-V, maszyny Wirtualnej VMware lub hosta fizycznego. Witaj zalecane minimalne wymagania dotyczące sprzętu serwera hello są dwa rdzenie i 4 GB pamięci RAM. w hello w poniższej tabeli przedstawiono Hello obsługiwane systemy operacyjne:

| System operacyjny | Platforma | SKU |
|:--- | --- |:--- |
| Windows Server 2012 R2 i najnowsze dodatki Service Pack |64-bitowa |Standard, Datacenter, Foundation |
| Windows Server 2012 i najnowsze dodatki Service Pack |64-bitowa |Datacenter, Foundation, Standard |
| Windows Storage Server 2012 R2 i najnowsze dodatki Service Pack |64-bitowa |Standard, Workgroup |
| Windows Storage Server 2012 i najnowsze dodatki Service Pack |64-bitowa |Standard, Workgroup |

Można deduplikacja magazynu programu DPM hello, za pomocą deduplikacji serwera systemu Windows. Dowiedz się więcej na temat [programu DPM i deduplikacji](https://technet.microsoft.com/library/dn891438.aspx) współpracują ze sobą po wdrożeniu na maszynach wirtualnych funkcji Hyper-V.

> [!NOTE]
> Serwer kopii zapasowej systemu Azure jest zaprojektowana toorun na dedykowanym serwerze jednozadaniowych. Nie można zainstalować serwer kopii zapasowej Azure na:
> - Komputer działa jako kontroler domeny
> - Komputer, na których serwer aplikacji hello jest zainstalowana rola
> - Na komputerze będącym serwerem zarządzania programu System Center Operations Manager
> - Komputer, na którym jest uruchomiony program Exchange Server
> - Komputer, który jest węzłem klastra

Zawsze przyłączyć do domeny tooa serwer kopii zapasowej Azure. Jeśli planujesz toomove powitania serwera tooa innej domeny, zaleca się przyłączyć powitania serwera toohello nowej domeny przed instalacją serwera kopii zapasowej Azure. Przenoszenie istniejącego serwera kopii zapasowej Azure maszyny tooa nowej domeny, po wdrożenia *nieobsługiwane*.

## <a name="2-recovery-services-vault"></a>2. Magazyn usługi Recovery Services
Wyślij dane kopii zapasowej tooAzure lub schowaj lokalnie, oprogramowania hello musi tooAzure toobe połączony. toobe dokładniej, komputer serwera usługi Kopia zapasowa Azure hello musi mieć toobe zarejestrowany w magazynie usług odzyskiwania.

toocreate odzyskiwania usług magazynu:

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com/).
2. W menu Centrum powitania kliknij **Przeglądaj** i hello listy zasobów, wpisz **usług odzyskiwania**. Po rozpoczęciu wpisywania, hello listy filtry oparte na dane wejściowe. Kliknij opcję **Magazyn Usług odzyskiwania**.

    ![Tworzenie magazynu usługi Recovery Services — krok 1](./media/backup-azure-microsoft-azure-backup/open-recovery-services-vault.png) <br/>

    zostanie wyświetlona lista Hello Magazyny usług odzyskiwania.
3. Na powitania **Magazyny usług odzyskiwania** menu, kliknij przycisk **Dodaj**.

    ![Tworzenie magazynu Usług odzyskiwania — krok 2](./media/backup-azure-microsoft-azure-backup/rs-vault-menu.png)

    Usługi odzyskiwania Hello zostanie otwarty blok magazyn monitem tooprovide **nazwa**, **subskrypcji**, **grupy zasobów**, i **lokalizacji**.

    ![Tworzenie magazynu Usług odzyskiwania — krok 5](./media/backup-azure-microsoft-azure-backup/rs-vault-attributes.png)
4. Aby uzyskać **nazwa**, wprowadź przyjazną nazwę tooidentify hello magazynu. Nazwa Hello musi toobe unikatowy dla hello subskrypcji platformy Azure. Wpisz nazwę o długości od 2 do 50 znaków. Musi ona rozpoczynać się od litery i może zawierać tylko litery, cyfry i łączniki.
5. Kliknij przycisk **subskrypcji** toosee hello listę dostępnych subskrypcji. Jeśli nie masz pewności, który toouse subskrypcji, użyj domyślnej hello (lub sugerowane) subskrypcji. Większa liczba opcji do wyboru jest dostępna tylko w przypadku, gdy konto organizacji jest skojarzone z wieloma subskrypcjami platformy Azure.
6. Kliknij przycisk **grupy zasobów** toosee hello listę dostępnych grup zasobów, lub kliknij przycisk **nowy** toocreate nową grupę zasobów. Pełne informacje na temat grup zasobów można znaleźć w temacie [Omówienie usługi Azure Resource Manager](../azure-resource-manager/resource-group-overview.md)
7. Kliknij przycisk **lokalizacji** tooselect hello region geograficzny magazynu hello.
8. Kliknij przycisk **Utwórz**. Może upłynąć trochę czasu zanim hello toobe utworzony magazyn usług odzyskiwania. Monitoruje powiadomienia o stanie hello hello górnym obszarze po prawej stronie w portalu hello.
   Po utworzeniu magazynu zostanie otwarty w portalu hello.

### <a name="set-storage-replication"></a>Konfigurowanie replikacji magazynu
opcji replikacji magazynu Hello umożliwia toochoose między magazynu geograficznie nadmiarowego i lokalnie nadmiarowego magazynu. Domyślnie magazyn jest nadmiarowy geograficznie. Jeśli ten magazyn jest podstawowym magazynu, pozostaw magazynu geograficznie nadmiarowego toogeo zestaw opcji magazynu hello. Wybierz magazyn lokalnie nadmiarowy, jeśli chcesz skorzystać z tańszej, ale mniej trwałej opcji. Przeczytaj więcej na temat [geograficznie nadmiarowego](../storage/common/storage-redundancy.md#geo-redundant-storage) i [magazyn lokalnie nadmiarowy](../storage/common/storage-redundancy.md#locally-redundant-storage) opcje magazynu w hello [Omówienie replikacji usługi Azure Storage](../storage/common/storage-redundancy.md).

ustawienia replikacji magazynu hello tooedit:

1. Wybierz magazyn tooopen hello magazynu w pulpicie nawigacyjnym i hello bloku ustawienia. Jeśli hello **ustawienia** nie otwarcie bloku, kliknij przycisk **wszystkie ustawienia** hello magazynu w pulpicie nawigacyjnym.
2. Na powitania **ustawienia** bloku, kliknij przycisk **infrastruktura kopii zapasowej** > **konfiguracji kopii zapasowej** tooopen hello **konfiguracji kopii zapasowej** bloku. Na powitania **konfiguracji kopii zapasowej** bloku, wybierz hello opcji replikacji magazynu dla magazynu.

    ![Lista magazynów kopii zapasowych](./media/backup-azure-vms-first-look-arm/choose-storage-configuration-rs-vault.png)

    Po wybraniu opcji magazynu powitania dla magazynu, wszystko jest gotowe tooassociate hello maszyn wirtualnych z magazynem hello. toobegin hello skojarzenia, należy odnaleźć i zarejestrować hello maszyn wirtualnych platformy Azure.

## <a name="3-software-package"></a>3. Pakiet oprogramowania
### <a name="downloading-hello-software-package"></a>Pobieranie pakietu oprogramowania hello
1. Zaloguj się toohello [portalu Azure](https://portal.azure.com/).
2. Jeśli masz już magazyn usług odzyskiwania, Otwórz, przejdź toostep 3. Jeśli nie masz otwarte magazyn usług odzyskiwania, ale znajdują się w portalu Azure, w menu centralnym hello hello kliknij **Przeglądaj**.

   * Na liście hello zasobów, wpisz **usług odzyskiwania**.
   * Po rozpoczęciu wpisywania, spowoduje odfiltrowanie listy hello oparte na dane wejściowe. Po wyświetleniu pozycji **Magazyny Usług odzyskiwania** kliknij ją.

     ![Tworzenie magazynu usługi Recovery Services — krok 1](./media/backup-azure-microsoft-azure-backup/open-recovery-services-vault.png)

     zostanie wyświetlona lista Hello Magazyny usług odzyskiwania.
   * Z listy hello Magazyny usług odzyskiwania wybierz magazyn.

     Otwiera Hello wybranego magazynu z pulpitu nawigacyjnego.

     ![Otwarcie bloku magazynu](./media/backup-azure-microsoft-azure-backup/vault-dashboard.png)
3. Witaj **ustawienia** zostanie otwarty blok domyślnie. Jeśli jest zamknięty, kliknij polecenie **ustawienia** tooopen hello ustawienia bloku.

    ![Otwarcie bloku magazynu](./media/backup-azure-microsoft-azure-backup/vault-setting.png)
4. Kliknij przycisk **kopii zapasowej** Kreator wprowadzenie hello tooopen.

    ![Wprowadzenie do kopii zapasowej](./media/backup-azure-microsoft-azure-backup/getting-started-backup.png)

    W hello **wprowadzenie do korzystania z kopii zapasowej** bloku, który zostanie otwarty, **celów tworzenia kopii zapasowej** zostanie wybrana automatycznie.

    ![Kopia zapasowa cele — domyślna otwieranych](./media/backup-azure-microsoft-azure-backup/getting-started.png)

5. W hello **cel kopii zapasowej** bloku z hello **gdzie działa Twoje obciążenie** menu, wybierz opcję **lokalnymi**.

    ![lokalne i obciążeń, gdy cele](./media/backup-azure-microsoft-azure-backup/backup-goals-azure-backup-server.png)

    Z hello **co chcesz toobackup?** menu rozwijanego, wybierz hello obciążeń mają tooprotect za pomocą serwera usługi Kopia zapasowa Azure, a następnie kliknij przycisk **OK**.

    Hello **wprowadzenie do korzystania z kopii zapasowej** hello przełączniki kreatora **przygotowanie infrastruktury** tooback opcji się tooAzure obciążeń.

   > [!NOTE]
   > Jeśli chcesz tylko tooback zapasowe plików i folderów, zaleca się przy użyciu agenta usługi Kopia zapasowa Azure hello i następujące wskazówki hello w artykule hello [Pierwsze spojrzenie: tworzenie kopii zapasowej plików i folderów](backup-try-azure-backup-in-10-mins.md). Jeśli zamierzasz tooprotect więcej niż pliki i foldery lub użytkownik jest planowana ochrona powitalnych tooexpand musi w przyszłości hello, wybierz tych obciążeń.
   >
   >

    ![Wprowadzenie zmian kreatora wprowadzenie](./media/backup-azure-microsoft-azure-backup/getting-started-prep-infra.png)

6. W hello **przygotowanie infrastruktury** bloku, że zostanie otwarty, kliknij polecenie hello **Pobierz** łącza, aby zainstalować serwer kopii zapasowej Azure i pobierania poświadczeń magazynu. Korzystanie z poświadczeń magazynu hello podczas rejestracji magazynu usług odzyskiwania toohello serwer kopii zapasowej Azure. Witaj łącza prowadzą toohello gdzie hello pakiet oprogramowania można pobrać Centrum pobierania.

    ![Przygotowanie infrastruktury dla serwera usługi Kopia zapasowa Azure](./media/backup-azure-microsoft-azure-backup/azure-backup-server-prep-infra.png)

7. Zaznacz wszystkie pliki hello, a następnie kliknij przycisk **dalej**. Pobieranie hello wszystkie pliki pochodzące strony pobierania hello kopia zapasowa Microsoft Azure i miejscem, w którym hello wszystkie pliki w hello tym samym folderze.

    ![Pobierz center 1](./media/backup-azure-microsoft-azure-backup/downloadcenter.png)

    Ponieważ hello pobierania rozmiar wszystkich plików hello razem > sieci 3G, minut hello na łącze pobierania 10 MB/s, który może potrwać too60 pobrać toocomplete.

### <a name="extracting-hello-software-package"></a>Wyodrębnianie hello pakietu oprogramowania
Po pobraniu wszystkich plików powitania kliknij **MicrosoftAzureBackupInstaller.exe**. Spowoduje to uruchomienie hello **Kreatora instalacji programu Microsoft Azure Backup** tooextract hello instalacji plików lokalizacji tooa określonego przez użytkownika. Kontynuuj pracę kreatora hello i kliknij na powitania **wyodrębnić** przycisk proces wyodrębniania hello toobegin.

> [!WARNING]
> Co najmniej 4GB wolnego miejsca jest pliki instalacyjne wymagane tooextract hello.
>
>

![Kreator tworzenia kopii zapasowej Microsoft Azure](./media/backup-azure-microsoft-azure-backup/extract/03.png)

Raz proces wyodrębniania hello pełną wyboru hello pole toolaunch hello świeżo wyodrębnione *setup.exe* toobegin instalowania serwer kopii zapasowej Microsoft Azure i kliknij na powitania **Zakończ** przycisku.

### <a name="installing-hello-software-package"></a>Instalowanie pakietu oprogramowania hello
1. Kliknij przycisk **kopia zapasowa Microsoft Azure** toolaunch hello Kreator.

    ![Kreator tworzenia kopii zapasowej Microsoft Azure](./media/backup-azure-microsoft-azure-backup/launch-screen2.png)
2. Na ekranie powitalnym powitania kliknij hello **dalej** przycisku. Powoduje to przejście toohello *wymagań wstępnych sprawdza* sekcji. Na tym ekranie kliknij **Sprawdź** toodetermine spełnieniu hello sprzętowe i programowe wymagania wstępne dotyczące serwera usługi Kopia zapasowa Azure. Jeśli pomyślnie zostały spełnione wszystkie wymagania wstępne, pojawi się komunikat wskazujący, że na tej maszynie hello spełnia wymagania hello. Polecenie hello **dalej** przycisku.

    ![Sprawdź serwera kopii zapasowej Azure — Zapraszamy i wymagania wstępne](./media/backup-azure-microsoft-azure-backup/prereq/prereq-screen2.png)
3. Serwer kopii zapasowej Microsoft Azure wymaga programu SQL Server Standard, a pakiet instalacyjny serwera usługi Kopia zapasowa Azure hello jest dostarczany powiązane z hello odpowiedniego programu SQL Server plików binarnych potrzebne. Przy uruchamianiu nową instalację serwera usługi Kopia zapasowa Azure, należy wybrać opcję hello **zainstalować nowe wystąpienie programu SQL Server w przypadku takiej konfiguracji** i kliknij przycisk hello **Sprawdź i zainstaluj** przycisku. Po pomyślnym zainstalowaniu hello wymagania wstępne, kliknij **dalej**.

    ![Serwera kopii zapasowej Azure — sprawdzenie programu SQL Server](./media/backup-azure-microsoft-azure-backup/sql/01.png)

    Jeśli wystąpi błąd z maszyną hello toorestart zalecenie, to zrobić i kliknij przycisk **Sprawdź ponownie**.

   > [!NOTE]
   > Serwer kopii zapasowej systemu Azure nie będzie działać przy użyciu zdalnego wystąpienia programu SQL Server. wystąpienie Hello jest używany przez serwer kopii zapasowej Azure musi toobe lokalnego.
   >
   >
4. Podaj lokalizację instalacji hello kopia zapasowa Microsoft Azure serwera plików, a następnie kliknij przycisk **dalej**.

    ![PreReq2 kopia zapasowa Microsoft Azure](./media/backup-azure-microsoft-azure-backup/space-screen.png)

    pliki tymczasowe lokalizacji Hello jest wymagana do tworzenia kopii zapasowych tooAzure. Upewnij się, że pliki tymczasowe lokalizacja hello jest co najmniej 5% danych hello planowane toobe kopii zapasowej toohello chmury. W przypadku ochrony dysku oddzielnych dyskach musi toobe skonfigurowany po zakończeniu instalacji hello. Aby uzyskać więcej informacji na temat pul magazynów, zobacz [Konfigurowanie pul magazynów i dysku magazynu](https://technet.microsoft.com/library/hh758075.aspx).
5. Podaj silne hasło dla kont użytkowników lokalnych z ograniczeniami, a następnie kliknij przycisk **dalej**.

    ![PreReq2 kopia zapasowa Microsoft Azure](./media/backup-azure-microsoft-azure-backup/security-screen.png)
6. Wybierz, czy toouse *Microsoft Update* toocheck aktualizacji i kliknij przycisk **dalej**.

   > [!NOTE]
   > Zaleca się o przekierowania tooMicrosoft aktualizacji, co zapewnia bezpieczeństwo i ważne aktualizacje systemu Windows i innych produktów, takich jak Microsoft Azure Utwórz kopię zapasową serwera usługi Windows Update.
   >
   >

    ![PreReq2 kopia zapasowa Microsoft Azure](./media/backup-azure-microsoft-azure-backup/update-opt-screen2.png)
7. Przejrzyj hello *Podsumowanie ustawień* i kliknij przycisk **zainstalować**.

    ![PreReq2 kopia zapasowa Microsoft Azure](./media/backup-azure-microsoft-azure-backup/summary-screen.png)
8. Instalacja Hello odbywa się w fazach. W hello pierwszego etap hello na powitania serwera zainstalowano agenta usług odzyskiwania Microsoft Azure. Kreator Hello sprawdza również połączenie z Internetem. Jeśli dostępny jest połączenie z Internetem można kontynuować instalacji, jeśli nie, należy tooprovide proxy szczegóły tooconnect toohello Internet.

    Witaj następnym krokiem jest hello tooconfigure agenta usług odzyskiwania Microsoft Azure. W ramach konfiguracji hello, konieczne będzie tooprovide Twojego magazynu poświadczeń tooregister hello maszyny toohello usług odzyskiwania magazynu. Zostanie również podać hasło tooencrypt/odszyfrowywania hello dane przesyłane między Azure i lokalnej. Można automatycznie wygenerować hasło lub podać własne minimalna hasło 16 znaków. Kontynuacja za pomocą Kreatora hello hello agent został skonfigurowany.

    ![Azure PreReq2 Server kopii zapasowej](./media/backup-azure-microsoft-azure-backup/mars/04.png)
9. Po pomyślnym zakończeniu rejestracji powitania serwera kopia zapasowa Microsoft Azure, hello ogólną Kreator instalacji będzie kontynuowana toohello instalacji i konfiguracji programu SQL Server i składniki serwera kopii zapasowej Azure hello. Po zakończeniu hello instalacji składników programu SQL Server, hello serwer kopii zapasowej Azure składniki są zainstalowane.

    ![Azure Backup Server](./media/backup-azure-microsoft-azure-backup/final-install/venus-installation-screen.png)

Po ukończeniu kroku instalacji hello hello ikony pulpitu produktu będzie utworzono również. Wystarczy kliknąć dwukrotnie hello ikona toolaunch hello produktu.

### <a name="add-backup-storage"></a>Dodawanie magazynu kopii zapasowej
Hello pierwszej kopii zapasowej jest przechowywany w magazynie dołączonym toohello maszyny serwera kopii zapasowej Azure. Aby uzyskać więcej informacji na temat dodawania dysków, zobacz [Konfigurowanie pul magazynów i dysku magazynu](https://technet.microsoft.com/library/hh758075.aspx).

> [!NOTE]
> Należy korzystać z magazynu kopii zapasowych tooadd nawet wtedy, gdy planujesz toosend tooAzure danych. W bieżącej architektury hello Azure kopii zapasowej serwera, magazynu usługi Kopia zapasowa Azure hello posiada hello *drugi* kopię danych hello na czas lokalny magazyn hello przechowuje hello pierwszy (i obowiązkowe) kopii zapasowej.
>
>

## <a name="4-network-connectivity"></a>4. Połączenie sieciowe
Serwer kopii zapasowej systemu Azure wymaga łączności usługi Kopia zapasowa Azure toohello dla toowork produktu hello pomyślnie. toovalidate, czy maszyna hello ma tooAzure łączności hello, używać hello ```Get-DPMCloudConnection``` polecenia cmdlet w konsoli programu PowerShell serwera kopii zapasowej Azure hello. Jeśli hello dane wyjściowe polecenia cmdlet hello ma wartość PRAWDA, a następnie istnieje połączenie, #else nie ma żadnej łączności.

Na powitania w tym samym czasie, hello subskrypcji platformy Azure musi toobe w dobrej kondycji. toofind hello stanu subskrypcji i toomanage go logowania toohello [portal subskrypcji](https://account.windowsazure.com/Subscriptions).

Znając stanu hello hello Azure łączności i hello subskrypcji platformy Azure, można użyć tabeli hello poniżej toofind limit hello wpływ na powitania funkcji wykonywania kopii zapasowej i przywracania.

| Stan łączności | Subskrypcja platformy Azure | Wykonaj kopię zapasową tooAzure | Wykonaj kopię zapasową toodisk | Przywróć z platformy Azure | Przywróć z dysku |
| --- | --- | --- | --- | --- | --- |
| połączone |Aktywne |Dozwolone |Dozwolone |Dozwolone |Dozwolone |
| połączone |Ważność |Zatrzymane |Zatrzymane |Dozwolone |Dozwolone |
| połączone |Anulowana |Zatrzymane |Zatrzymane |Punkty odzyskiwania zatrzymane, a Azure usunięte |Zatrzymane |
| Utratą połączenia > 15 dni |Aktywne |Zatrzymane |Zatrzymane |Dozwolone |Dozwolone |
| Utratą połączenia > 15 dni |Ważność |Zatrzymane |Zatrzymane |Dozwolone |Dozwolone |
| Utratą połączenia > 15 dni |Anulowana |Zatrzymane |Zatrzymane |Punkty odzyskiwania zatrzymane, a Azure usunięte |Zatrzymane |

### <a name="recovering-from-loss-of-connectivity"></a>Odzyskiwanie z utraty połączenia
Jeśli zapora lub serwer proxy, który uniemożliwia tooAzure dostępu, należy hello toowhitelist następujące adresy domeny w profilu zapory i proxy hello:

* www.msftncsi.com
* \*.Microsoft.com
* \*.WindowsAzure.com
* \*.microsoftonline.com
* \*.windows.net

Po tooAzure łączność została przywrócona toohello serwer kopii zapasowej Azure maszyny, hello operacje, które mogą być wykonywane są określane przez hello stanu subskrypcji platformy Azure. powyższej tabeli Hello zawiera szczegółowe informacje o operacjach hello dozwolona po maszyny hello jest "połączenia".

### <a name="handling-subscription-states"></a>Obsługa stany subskrypcji
Jest możliwe tootake subskrypcji platformy Azure z *wygasłe* lub *Deprovisioned* toohello stanu *Active* stanu. Jednak ma wpływ na niektóre na zachowanie produktu hello podczas hello stanu nie jest *Active*:

* A *Deprovisioned* subskrypcji utraci funkcje hello okres, który jest ona anulowana. Na włączanie *Active*, hello produktu funkcji wykonywania kopii zapasowej i przywracania jest przywrócona. można również pobrać Hello dane kopii zapasowej na dysku lokalnym hello Jeśli znajdowały się od okresu przechowywania wystarczająco duża. Jednak hello kopii zapasowej danych na platformie Azure po nieodwracalnie subskrypcji hello wprowadza hello *Deprovisioned* stanu.
* *Wygasłe* subskrypcji tylko utraci funkcje dla dopóki umożliwiono jego *Active* ponownie. Zostało żadnych kopii zapasowych zaplanowanych dla okresu hello które subskrypcji hello *wygasłe* nie zostaną uruchomione.

## <a name="troubleshooting"></a>Rozwiązywanie problemów
Jeśli kopia zapasowa Microsoft Azure serwera zakończy się niepowodzeniem z błędami hello fazy instalacji (lub kopii zapasowej lub przywracania), zapoznaj się z pomocą techniczną firmy toothis [dokumentu kody błędów](https://support.microsoft.com/kb/3041338) Aby uzyskać więcej informacji.
Można także odwoływać się zbyt[— często zadawane pytania dotyczące usługi Kopia zapasowa Azure](backup-azure-backup-faq.md)

## <a name="next-steps"></a>Następne kroki
Aby wyświetlić szczegółowe informacje dotyczące [przygotowywanie środowiska dla programu DPM](https://technet.microsoft.com/library/hh758176.aspx) w witrynie Microsoft TechNet hello. Zawiera informacje o obsługiwanych konfiguracjach, na których można wdrożyć i używany serwer kopii zapasowej Azure.

Możesz użyć tych artykułów toogain lepiej zrozumieć ochrony obciążenia przy użyciu serwera kopia zapasowa Microsoft Azure.

* [Kopia zapasowa programu SQL Server](backup-azure-backup-sql.md)
* [Kopia zapasowa programu SharePoint server](backup-azure-backup-sharepoint.md)
* [Alternatywny serwer kopii zapasowej](backup-azure-alternate-dpm-server.md)
