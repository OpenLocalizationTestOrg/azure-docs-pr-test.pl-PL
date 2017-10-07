---
title: "tooback serwer kopii zapasowej Azure aaaUse zapasową obciążeń tooAzure klasyczny portal | Dokumentacja firmy Microsoft"
description: "Upewnij się, że środowisko jest poprawnie przygotowany tooback dużych obciążeń, za pomocą serwera usługi Kopia zapasowa Azure"
services: backup
documentationcenter: 
author: pvrk
manager: shivamg
editor: 
keywords: Serwer kopii zapasowej systemu Azure; Magazyn kopii zapasowych
ms.assetid: d86450e8-da63-4283-8fd7-2ee629fa14ab
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: masaran;trinadhk;pullabhk;markgal
ms.openlocfilehash: 7b574824c448096e0c0ba74a872ab8f2a434f6a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="preparing-tooback-up-workloads-using-azure-backup-server"></a>Przygotowywanie tooback dużych obciążeń, za pomocą serwera usługi Kopia zapasowa Azure
> [!div class="op_single_selector"]
> * [Azure Backup Server](backup-azure-microsoft-azure-backup.md)
> * [SCDPM](backup-azure-dpm-introduction.md)
> * [Serwer kopii zapasowej systemu Azure (klasyczne)](backup-azure-microsoft-azure-backup-classic.md)
> * [SCDPM (klasyczne)](backup-azure-dpm-introduction-classic.md)
>
>

Ten artykuł dotyczy przygotowanie Twojego środowiska tooback dużych obciążeń, za pomocą serwera usługi Kopia zapasowa Azure. Serwer kopii zapasowej Azure umożliwia ochronę obciążeń aplikacji, takich jak maszyn wirtualnych funkcji Hyper-V, programu Microsoft SQL Server, SharePoint Server, Microsoft Exchange i klientów systemu Windows z poziomu pojedynczej konsoli.

> [!WARNING]
> Serwer kopii zapasowej systemu Azure dziedziczy hello funkcjonalność programu Data Protection Manager (DPM) do utworzenia kopii zapasowej obciążeń. Wskaźniki można znaleźć tooDPM dokumentacji dla niektórych z tych funkcji. Jednak serwer kopii zapasowej Azure zapewnia ochronę na taśmie lub nie integracji z programem System Center.
>
>

## <a name="1-windows-server-machine"></a>1. Komputer z systemem Windows Server
![step1](./media/backup-azure-microsoft-azure-backup/step1.png)

pierwszym krokiem Hello kierunku uruchamianie hello Azure Utwórz kopię zapasową serwera w i przeprowadzanie jest toohave komputerze z systemem Windows Server.

| Lokalizacja | Minimalne wymagania | Dodatkowe instrukcje |
| --- | --- | --- |
| Azure |Maszyny wirtualne IaaS platformy Azure<br><br>A2 Standard: 2 rdzenie, 3.5GB pamięci RAM |Można uruchomić przy użyciu prostego galerii obrazu systemu Windows Server 2012 R2 Datacenter. [Ochrona za pomocą serwera kopii zapasowej Azure (DPM) obciążenia IaaS](https://technet.microsoft.com/library/jj852163.aspx) ma wiele wszystkie szczegóły. Upewnij się, przeczytaj artykuł hello całkowicie przed wdrożeniem hello maszyny. |
| Lokalnie |Maszyna wirtualna funkcji Hyper-V,<br> Maszyna wirtualna oprogramowania VMWare,<br> lub hosta fizycznego.<br><br>2 rdzenie i 4GB pamięci RAM |Można deduplikacja magazynu programu DPM hello, za pomocą deduplikacji serwera systemu Windows. Dowiedz się więcej na temat [programu DPM i deduplikacji](https://technet.microsoft.com/library/dn891438.aspx) współpracują ze sobą po wdrożeniu na maszynach wirtualnych funkcji Hyper-V. |

> [!NOTE]
> Zalecane jest zainstalowanie serwera usługi Kopia zapasowa Azure na komputerze z systemem Windows Server 2012 R2 Datacenter. Wiele wymagań wstępnych hello automatycznie są objęte hello najnowszej wersji systemu operacyjnego Windows hello.
>
>

Jeśli planujesz toojoin serwer kopii zapasowej Azure tooa domeny, zaleca się przyłączyć serwer fizyczny hello lub domeny toohello maszyny wirtualnej przed zainstalowaniem oprogramowania serwer kopii zapasowej Azure hello. Przenoszenie serwera usługi Kopia zapasowa Azure tooa nowej domeny, po wdrożeniu jest *nieobsługiwane*.

## <a name="2-backup-vault"></a>2. Magazyn kopii zapasowych
![step2](./media/backup-azure-microsoft-azure-backup/step2.png)

Czy wysyłać dane kopii zapasowej tooAzure lub schowaj lokalnie, powitania serwera kopii zapasowej Azure musi być zarejestrowany tooa magazynu. Jeśli dla nowych użytkowników kopia zapasowa Azure i mają toouse serwer kopii zapasowej Azure, zobacz hello Azure portalu wersja tego artykułu - [przygotowanie tooback dużych obciążeń, za pomocą serwera usługi Kopia zapasowa Azure](backup-azure-microsoft-azure-backup.md).

> [!IMPORTANT]
> Uruchamianie 2017 marca, można dłużej korzystać magazyny kopii zapasowych w klasycznym portalu toocreate hello.
> Teraz można uaktualnić Twoje Magazyny usług tooRecovery magazynów kopii zapasowych. Aby uzyskać więcej informacji, zobacz artykuł hello [uaktualnienia tooa magazynu kopii zapasowej, Magazyn usług odzyskiwania i](backup-azure-upgrade-backup-to-recovery-services.md). Firma Microsoft zachęca tooupgrade Magazyny usług tooRecovery magazyny kopii zapasowych.<br/> Po 15 października 2017 nie można użyć magazyny kopii zapasowych toocreate środowiska PowerShell. **Do 1 listopada 2017 r.**:
>- Wszystkie pozostałe magazyny kopii zapasowych zostanie automatycznie uaktualniony tooRecovery Magazyny usług.
>- Użytkownik nie będzie możliwe tooaccess danych kopii zapasowych w portalu klasycznym hello. Zamiast tego użyj hello Azure tooaccess portalu tej kopii zapasowej w Magazyny usług odzyskiwania.
>



## <a name="3-software-package"></a>3. Pakiet oprogramowania
![krok 3](./media/backup-azure-microsoft-azure-backup/step3.png)

### <a name="downloading-hello-software-package"></a>Pobieranie pakietu oprogramowania hello
Podobne toovault poświadczeń, można pobrać kopia zapasowa Microsoft Azure dla obciążeń aplikacji z hello **strony Szybki Start** hello magazynu kopii zapasowych.

1. Kliknij przycisk **dla obciążeń aplikacji (tooCloud tooDisk dysku)**. Spowoduje to przejście toohello strony Centrum pobierania, z której można pobrać pakiet oprogramowania hello.

    ![Ekran powitalny kopia zapasowa Microsoft Azure](./media/backup-azure-microsoft-azure-backup/dpm-venus1.png)
2. Kliknij pozycję **Pobierz**.

    ![Pobierz center 1](./media/backup-azure-microsoft-azure-backup/downloadcenter1.png)
3. Zaznacz wszystkie pliki hello, a następnie kliknij przycisk **dalej**. Pobieranie hello wszystkie pliki pochodzące strony pobierania hello kopia zapasowa Microsoft Azure i miejscem, w którym hello wszystkie pliki w hello tym samym folderze.
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
2. Na ekranie powitalnym powitania kliknij hello **dalej** przycisku. Powoduje to przejście toohello *wymagań wstępnych sprawdza* sekcji. Na tym ekranie kliknij hello **Sprawdź** przycisk toodetermine spełnieniu hello sprzętowe i programowe wymagania wstępne dotyczące serwera usługi Kopia zapasowa Azure. Jeśli wszystkie hello są wymagania wstępne zostały spełnione pomyślnie, pojawi się komunikat wskazujący, że na tej maszynie hello spełnia wymagania hello. Polecenie hello **dalej** przycisku.

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

    Witaj następnym krokiem jest hello tooconfigure agenta usług odzyskiwania Microsoft Azure. W ramach konfiguracji hello konieczne będzie tooprovide Twojego hello magazynu poświadczeń tooregister hello maszyny toohello magazynu kopii zapasowych. Zostanie również podać hasło tooencrypt/odszyfrowywania hello dane przesyłane między Azure i lokalnej. Można automatycznie wygenerować hasło lub podać własne minimalna hasło 16 znaków. Kontynuacja za pomocą Kreatora hello hello agent został skonfigurowany.

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
![step4](./media/backup-azure-microsoft-azure-backup/step4.png)

Serwer kopii zapasowej systemu Azure wymaga łączności usługi Kopia zapasowa Azure toohello dla toowork produktu hello pomyślnie. toovalidate, czy maszyna hello ma tooAzure łączności hello, używać hello ```Get-DPMCloudConnection``` w konsoli programu PowerShell serwera kopii zapasowej Azure hello apletu polecenia. Jeśli hello dane wyjściowe polecenia hello ma wartość PRAWDA, a następnie istnieje połączenie, #else nie ma żadnej łączności.

Na powitania w tym samym czasie, hello subskrypcji platformy Azure musi toobe w dobrej kondycji. toofind hello stanu subskrypcji i toomanage go logowania toohello [portal subskrypcji](https://account.windowsazure.com/Subscriptions).

Znając stanu hello hello Azure łączności i hello subskrypcji platformy Azure, można użyć tabeli hello poniżej toofind limit hello wpływ na powitania funkcji wykonywania kopii zapasowej i przywracania.

| Stan łączności | Subskrypcja platformy Azure | TooAzure kopii zapasowej | Toodisk kopii zapasowej | Przywróć z platformy Azure | Przywróć z dysku |
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
