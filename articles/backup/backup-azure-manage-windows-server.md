---
title: "usług odzyskiwania Azure aaaManage magazynami i serwerami | Dokumentacja firmy Microsoft"
description: "Użyj tego samouczka toolearn jak magazyny usług odzyskiwania Azure toomanage i serwerów."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: tysonn
ms.assetid: 4eea984b-7ed6-4600-ac60-99d2e9cb6d8a
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: markgal
ms.openlocfilehash: b4c35c86faa0828b3c63a13b85c095c0cbaba50e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-azure-recovery-services-vaults-and-servers-for-windows-machines"></a>Monitorowanie magazynów i serwerów usługi Azure Recovery Services i zarządzanie nimi dla maszyn z systemem Windows
> [!div class="op_single_selector"]
> * [Resource Manager](backup-azure-manage-windows-server.md)
> * [Wdrożenie klasyczne](backup-azure-manage-windows-server-classic.md)
>
>

W tym artykule znajdziesz omówienie hello zadania tworzenia kopii zapasowych monitorowanie i zarządzanie dostępne za pośrednictwem hello Azure portal i hello agenta kopii zapasowej Microsoft Azure. W tym artykule przyjęto założenie, już mieć subskrypcję platformy Azure i został utworzony co najmniej jeden magazyn usług odzyskiwania.

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-rm-include.md)]


## <a name="open-a-recovery-services-vault"></a>Otwórz magazyn usług odzyskiwania

pulpitem nawigacyjnym magazynu usług odzyskiwania Hello przedstawia szczegóły hello lub atrybuty z magazynu usług odzyskiwania.

1. Zaloguj się toohello [Azure Portal](https://portal.azure.com/) przy użyciu subskrypcji platformy Azure.
2. W menu Centrum powitania kliknij **więcej usług**.

    ![Otwórz listę magazynów usług odzyskiwania — krok 1](./media/backup-azure-manage-windows-server/open-rs-vault-list.png) <br/>

3. Ma tooopen magazynu usług odzyskiwania. Okno dialogowe hello, zacznij pisać **usług odzyskiwania**. Po rozpoczęciu wpisywania, spowoduje odfiltrowanie listy hello oparte na dane wejściowe. Kliknij przycisk **Magazyny usług odzyskiwania** magazyny toodisplay hello listę usług odzyskiwania w ramach subskrypcji.

    ![Tworzenie magazynu usługi Recovery Services — krok 1](./media/backup-azure-manage-windows-server/browse-to-rs-vaults-2.png) <br/>

    Otwiera Hello listę magazynów usług odzyskiwania.

    ![Tworzenie magazynu usługi Recovery Services — krok 1](./media/backup-azure-manage-windows-server/list-of-rs-vaults.png) <br/>

4. Z listy hello magazynów wybierz nazwę hello hello ma tooopen magazyn usług odzyskiwania. zostanie otwarty blok pulpitu nawigacyjnego magazynu usług odzyskiwania Hello.

    ![pulpitem nawigacyjnym magazynu usług odzyskiwania](./media/backup-azure-manage-windows-server/rs-vault-blade.png) <br/>

    Po otwarciu magazyn usług odzyskiwania hello wypróbować hello zadań monitorowania lub zarządzania.

## <a name="monitor-backup-jobs-and-alerts"></a>Monitorowanie zadań tworzenia kopii zapasowej i alerty

Monitoruj zadania i alerty z hello magazyn usług odzyskiwania i pulpitu nawigacyjnego, której występuje:

* Szczegóły alerty kopii zapasowej
* Pliki i foldery, a także chroniona w chmurze hello maszyn wirtualnych platformy Azure
* Całkowita ilość miejsca zużyte na platformie Azure
* Stan zadania tworzenia kopii zapasowej

![Zadania tworzenia kopii zapasowej pulpitu nawigacyjnego](./media/backup-azure-manage-windows-server/dashboard-tiles.png)

Kliknięcie przycisku hello informacji w każdym z tych kafelków spowoduje otwarcie bloku skojarzone hello, w których zarządzasz powiązanych zadań.

Z góry hello hello pulpitu nawigacyjnego:

* Ustawienia zapewnia dostęp dostępnych zadań tworzenia kopii zapasowej.
* Magazyn kopii zapasowych — umożliwia wykonanie kopii zapasowej nowe pliki i foldery (lub maszyn wirtualnych platformy Azure) toohello usług odzyskiwania.
* Delete — Jeśli magazyn usług odzyskiwania jest już używana, można usunąć toofree miejsca do magazynowania. DELETE jest włączona tylko po usunięciu wszystkich chronionych serwerach z hello magazynu.

![Zadania tworzenia kopii zapasowej pulpitu nawigacyjnego](./media/backup-azure-manage-windows-server/dashboard-tasks.png)

## <a name="alerts-for-backups-using-azure-backup-agent"></a>Alerty kopii zapasowych za pomocą agenta kopii zapasowej systemu Azure:
| Poziom alertu | Wysyłania alertów |
| --- | --- |
| Krytyczne |Niepowodzenia wykonywania kopii zapasowej, niepowodzenia odzyskiwania |
| Ostrzeżenie |Kopia zapasowa zakończona z ostrzeżeniami (jeśli jest mniej niż sto nie kopii zapasowej plików powodu toocorruption problemów i pomyślnie kopii zapasowej plików ponad milion) |
| Informacyjny |Brak |

## <a name="manage-backup-alerts"></a>Zarządzanie alertami kopii zapasowej
Kliknij przycisk hello **alerty kopii zapasowej** hello tooopen kafelka **alerty kopii zapasowej** blok alerty i zarządzaj nimi.

![Alerty kopii zapasowej](./media/backup-azure-manage-windows-server/manage-backup-alerts.png)

Witaj alerty kopii zapasowej kafelka pokazuje hello liczba:

* alerty krytyczne nierozpoznane w ostatnich 24 godzinach
* alerty ostrzegawcze nierozpoznane w ostatnich 24 godzinach

Kliknięcie na każdym z tych łączy powoduje toohello **alerty kopii zapasowej** bloku filtrowany widok alertów (krytyczna lub poważna).

W bloku hello alerty kopii zapasowej możesz:

* Wybierz hello tooinclude odpowiednie informacje o alerty.

    ![Wybierz kolumny](./media/backup-azure-manage-windows-server/choose-alerts-colunms.png)
* Filtrowanie alertów na czas ważności, stanu i rozpoczęcia i zakończenia.

    ![Filtrowanie alertów](./media/backup-azure-manage-windows-server/filter-alerts.png)
* Konfigurowanie powiadomień o ważności, częstotliwości i adresatów, a także włączyć alerty lub wyłączyć.

    ![Filtrowanie alertów](./media/backup-azure-manage-windows-server/configure-notifications.png)

Jeśli **na alertu** został wybrany jako hello **powiadamiania** częstotliwość nie grupowania lub zmniejszenia w wiadomościach e-mail. Każdy alert powoduje 1 powiadomień. To jest ustawienie domyślne hello i hello rozpoznawania e-mail jest również wysyłane natychmiast.

Jeśli **co godzinę szyfrowanego** został wybrany jako hello **powiadamiania** częstotliwość jeden adres e-mail jest wysyłana użytkownika toohello informacją, które istnieją nierozwiązane nowe alerty wygenerowane w hello ostatniej godziny. Wiadomość e-mail z rozwiązania jest wysyłane na końcu hello hello godzinę.

Alerty mogą być wysyłane do hello następujące poziomy ważności:

* Krytyczne
* Ostrzeżenie
* Informacje

Dezaktywuj alert hello z hello **Dezaktywuj** przycisku na powitania zadania szczegóły blok. Po kliknięciu Dezaktywuj, możesz podać informacje o rozdzielczości.

Wybierz kolumny hello ma tooappear jako część hello alertu o hello **wybierz kolumny** przycisku.

> [!NOTE]
> Z hello **ustawienia** bloku Zarządzanie alerty kopii zapasowej przez zaznaczenie **monitorowanie i Raporty > Alerty i zdarzenia > Alerty kopii zapasowej** , a następnie klikając polecenie **filtru** lub  **Konfigurowanie powiadomień**.
>
>

## <a name="manage-backup-items"></a>Zarządzaj elementami kopii zapasowej
Zarządzanie lokalnymi kopiami zapasowymi jest teraz dostępna w portalu zarządzania hello. W sekcji kopii zapasowej hello pulpitu nawigacyjnego hello hello **elementów kopii zapasowych** kafelka zawiera hello liczbę elementów kopii zapasowych chronionych toohello magazynu.

Kliknij przycisk **folderów plików** w hello kafelka elementy kopii zapasowej.

![Kafelek elementów kopii zapasowych](./media/backup-azure-manage-windows-server/backup-items-tile.png)

Hello elementów kopii zapasowych, który zostanie otwarty blok z hello filtrować tooFile zestaw folderów, której występuje każdej kopii zapasowej elementów na liście.

![Elementy kopii zapasowej](./media/backup-azure-manage-windows-server/backup-item-list.png)

W przypadku wybrania określonego elementu kopii zapasowej z listy hello widzisz hello niezbędne szczegóły dla tego elementu.

> [!NOTE]
> Z hello **ustawienia** bloku zarządzania plikami i folderami wybierając **chronione elementy > kopii zapasowej elementów** , a następnie wybierając **folderów plików** z hello menu rozwijanym.
>
>

![Elementy kopii zapasowej z ustawień](./media/backup-azure-manage-windows-server/backup-files-and-folders.png)

## <a name="manage-backup-jobs"></a>Zarządzanie zadaniami kopii zapasowej
Zadania tworzenia kopii zapasowej zarówno na lokalnym (Jeśli serwer lokalne powitania wykonuje kopię zapasową tooAzure), jak i kopii zapasowych Azure są widoczne na pulpicie nawigacyjnym hello.

W hello kopii zapasowej części pulpitu nawigacyjnego hello kafelka zadania tworzenia kopii zapasowej hello pokazuje hello liczbę zadań:

* w toku
* Wystąpił błąd na powitania ostatnich 24 godzin.

toomanage zadań kopii zapasowych, kliknij przycisk hello **zadania tworzenia kopii zapasowej** kafelka, która otwiera blok zadań tworzenia kopii zapasowej hello.

![Elementy kopii zapasowej z ustawień](./media/backup-azure-manage-windows-server/backup-jobs.png)

Modyfikowanie hello informacje są dostępne w bloku zadania tworzenia kopii zapasowej hello z hello **wybierz kolumny** przycisk u góry hello hello strony.

Użyj hello **filtru** tooselect przycisk między plików i folderów z kopii zapasowej maszyny wirtualnej platformy Azure.

Jeśli nie widzisz z kopii zapasowej plików i folderów, kliknij przycisk **filtru** u góry hello hello strony i wybierz **pliki i foldery** hello typu elementu menu.

> [!NOTE]
> Z hello **ustawienia** bloku Zarządzanie zadania tworzenia kopii zapasowej przez zaznaczenie **monitorowanie i Raporty > zadania > zadań tworzenia kopii zapasowej** , a następnie wybierając **folderów plików** z listy hello menu.
>
>

## <a name="monitor-backup-usage"></a>Monitorowanie użycia kopii zapasowej
W kopii zapasowej części pulpitu nawigacyjnego hello hello Kafelek użycie kopii zapasowej hello pokazuje magazynu hello zużyte na platformie Azure. Użycie magazynu jest dostępne:

* Użycie magazynu LRS skojarzony z magazynem hello w chmurze
* Użycie magazynu GRS skojarzony z magazynem hello w chmurze

## <a name="manage-your-production-servers"></a>Zarządzanie serwerami produkcji
toomanage serwerów produkcyjnych, kliknij przycisk **ustawienia**.

W obszarze Zarządzanie kliknij **infrastruktura kopii zapasowej > serwerów produkcyjnych**.

Witaj list bloku serwerów produkcyjnych serwerów produkcyjnych. Kliknij serwer w szczegóły hello listy tooopen powitania serwera.

![Elementy chronione](./media/backup-azure-manage-windows-server/production-server-list.png)


## <a name="open-hello-azure-backup-agent"></a>Otwórz hello agenta usługi Kopia zapasowa Azure
Otwórz hello **agenta usługi Kopia zapasowa Microsoft Azure** (można go znaleźć, wyszukaj komputer dla *kopia zapasowa Microsoft Azure*).

![Planowanie kopii zapasowych serwera systemu Windows](./media/backup-azure-manage-windows-server/snap-in-search.png)

Z hello **akcje** dostępne pod adresem hello rogu konsoli agenta kopii zapasowej hello, należy wykonać następujące zadania zarządzania hello:

* Zarejestruj serwer
* Harmonogram tworzenia kopii zapasowych
* Wykonaj kopię zapasową teraz
* Zmień właściwości

![Akcje konsoli agenta usługi Kopia zapasowa Microsoft Azure](./media/backup-azure-manage-windows-server/console-actions.png)

> [!NOTE]
> zbyt**odzyskać dane**, zobacz [przywrócić pliki tooa systemu Windows server lub komputer kliencki z systemem Windows](backup-azure-restore-windows-server.md).
>
>

## <a name="modify-hello-backup-schedule"></a>Zmodyfikuj harmonogram kopii zapasowych hello
1. W agencie kopia zapasowa Microsoft Azure powitania kliknij **harmonogram tworzenia kopii zapasowych**.

    ![Planowanie kopii zapasowych serwera systemu Windows](./media/backup-azure-manage-windows-server/schedule-backup.png)
2. W hello **Kreatora harmonogramu kopii zapasowej** pozostaw hello **wprowadzanie zmian elementów toobackup lub razy** zaznaczono opcję i kliknij przycisk **dalej**.

    ![Planowanie kopii zapasowych serwera systemu Windows](./media/backup-azure-manage-windows-server/modify-or-stop-a-scheduled-backup.png)
3. Jeśli chcesz tooadd lub zmienić elementy na powitania **tooBackup wybierz elementy** ekranu kliknij **Dodaj elementy**.

    Można również ustawić **ustawienia wykluczania** na tej stronie kreatora hello. Jeśli pliki tooexclude lub typów plików odczytu hello procedurę dodawania [ustawienia wykluczania](#manage-exclusion-settings).
4. Wybierz hello pliki i foldery mają tooback w górę i kliknij przycisk **OK**.

    ![Planowanie kopii zapasowych serwera systemu Windows](./media/backup-azure-manage-windows-server/add-items-modify.png)
5. Określ hello **harmonogram tworzenia kopii zapasowych** i kliknij przycisk **dalej**.

    Można zaplanować codziennie (maksymalnie 3 razy dziennie) lub cotygodniowe kopie zapasowe.

    ![Elementy związane z tworzeniem kopii zapasowej systemu Windows Server](./media/backup-azure-manage-windows-server/specify-backup-schedule-modify-close.png)

   > [!NOTE]
   > Określanie harmonogramu tworzenia kopii zapasowych hello omówiono szczegółowo w tym [artykułu](backup-azure-backup-cloud-as-tape.md).
   >

6. Wybierz hello **zasady przechowywania** hello kopii zapasowej, a następnie kliknij przycisk **dalej**.

    ![Elementy związane z tworzeniem kopii zapasowej systemu Windows Server](./media/backup-azure-manage-windows-server/select-retention-policy-modify.png)
7. Na powitania **potwierdzenie** ekran Przegląd hello informacji i kliknij przycisk **Zakończ**.
8. Gdy Kreator hello zakończy tworzenie hello **harmonogram tworzenia kopii zapasowych**, kliknij przycisk **Zamknij**.

    Po zmodyfikowaniu ochrony, można potwierdzić poprawnie wyzwalają kopii zapasowych przez przejście toohello **zadania** kartę i potwierdzenie, że zmiany zostaną odzwierciedlone w hello kopii zapasowej zadania.

## <a name="enable-network-throttling"></a>Włącz ograniczanie przepustowości sieci

agent usługi Kopia zapasowa Azure Hello zawiera kartę ograniczenia przepustowości, co pozwala toocontrol wykorzystaniem przepustowości sieci podczas transferu danych. Ten formant może być przydatne, gdy konieczne tooback zapasową danych poza godzinami pracy, ale nie chcesz hello toointerfere procesu tworzenia kopii zapasowej z innych ruch internetowy. Ograniczanie danych transfer stosuje tooback zapasową i przywrócić działań.  

Ograniczanie tooenable:

1. W hello **agent usługi Kopia zapasowa**, kliknij przycisk **Zmień właściwości**.
2. Na powitania ** ograniczania kartę, zaznacz **włączyć użycia przepustowości połączenia internetowego do operacji tworzenia kopii zapasowej**.

    ![Ograniczanie przepustowości sieci](./media/backup-azure-manage-windows-server/throttling-dialog.png)

    Po włączeniu ograniczenia przepustowości, określ hello dozwolone przepustowości dla transferu danych kopii zapasowej podczas **godzin pracy** i **godziny wolne**.

    wartości przepustowości Hello rozpoczynały 512 kilobajtach na sekundę (KB/s) i można przejść w górę too1023 MB na sekundę (MB/s). Można również wyznaczyć hello rozpoczęcia i zakończenia **godzin pracy**, i dni tygodnia hello są traktowane jako pracy dni. czas Hello poza Witaj wyznaczone godzin pracy jest godzin wolnych toobe rozważenia.
3. Kliknij przycisk **OK**.

## <a name="manage-exclusion-settings"></a>Zarządzanie ustawieniami wykluczeń
1. Otwórz hello **agenta usługi Kopia zapasowa Microsoft Azure** (można go znaleźć, wyszukaj na maszynie łańcuch *kopia zapasowa Microsoft Azure*).

    ![Planowanie kopii zapasowych serwera systemu Windows](./media/backup-azure-manage-windows-server/snap-in-search.png)
2. W agencie kopia zapasowa Microsoft Azure powitania kliknij **harmonogram tworzenia kopii zapasowych**.

    ![Planowanie kopii zapasowych serwera systemu Windows](./media/backup-azure-manage-windows-server/schedule-backup.png)
3. W hello Kreatora harmonogramu kopii zapasowej pozostaw hello **wprowadzanie zmian elementów toobackup lub razy** zaznaczono opcję i kliknij przycisk **dalej**.

    ![Planowanie kopii zapasowych serwera systemu Windows](./media/backup-azure-manage-windows-server/modify-or-stop-a-scheduled-backup.png)
4. Kliknij przycisk **ustawienia wykluczenia**.

    ![Planowanie kopii zapasowych serwera systemu Windows](./media/backup-azure-manage-windows-server/exclusion-settings.png)
5. Kliknij przycisk **Dodaj wykluczenia**.

    ![Planowanie kopii zapasowych serwera systemu Windows](./media/backup-azure-manage-windows-server/add-exclusion.png)
6. Wybierz lokalizację hello, a następnie kliknij przycisk **OK**.

    ![Planowanie kopii zapasowych serwera systemu Windows](./media/backup-azure-manage-windows-server/exclusion-location.png)
7. Dodaj rozszerzenie pliku hello w hello **typ pliku** pola.

    ![Planowanie kopii zapasowych serwera systemu Windows](./media/backup-azure-manage-windows-server/exclude-file-type.png)

    Dodawanie rozszerzenia MP3

    ![Planowanie kopii zapasowych serwera systemu Windows](./media/backup-azure-manage-windows-server/exclude-mp3.png)

    tooadd inne rozszerzenie, kliknij przycisk **Dodawanie wykluczenia** i wprowadź inne rozszerzenie typu pliku (Dodawanie rozszerzenia .jpeg).

    ![Planowanie kopii zapasowych serwera systemu Windows](./media/backup-azure-manage-windows-server/exclude-jpg.png)
8. Po dodaniu wszystkich rozszerzeń powitania kliknij **OK**.
9. Kontynuuj hello Kreatora harmonogramu kopii zapasowej, klikając **dalej** do hello **stronę potwierdzenia**, następnie kliknij przycisk **Zakończ**.

    ![Planowanie kopii zapasowych serwera systemu Windows](./media/backup-azure-manage-windows-server/finish-exclusions.png)

## <a name="frequently-asked-questions"></a>Często zadawane pytania
**1. Stan zadania tworzenia kopii zapasowej Hello jest wyświetlana jako zakończone hello Azure agenta kopii zapasowej, dlaczego nie go pobrać natychmiast odzwierciedlone w portalu?**

Odpowiedź 1. Jest w Maksymalne opóźnienie 15 minutach między hello stan zadania tworzenia kopii zapasowej zostaną uwzględnione w hello agenta kopii zapasowej systemu Azure i hello portalu Azure.

**Q.2, gdy zadanie tworzenia kopii zapasowej nie powiedzie się, jak długo trwa tooraise alert?**

A.2 alert jest uruchamiany w ciągu 20 minutach hello Azure niepowodzenia wykonywania kopii zapasowej.

**K3. Jest przypadek, w którym nie będzie wysyłana wiadomość e-mail, jeśli skonfigurowano powiadomienia?**

Odpowiedź 3. Poniżej przedstawiono hello przypadków podczas hello powiadomienia nie będą wysyłane w kolejności tooreduce hello alertu szumu:

* Jeśli powiadomienia są skonfigurowane co godzinę, a alert jest uruchamiany rozwiązane w ciągu godziny hello
* Zadanie zostało anulowane.
* Drugi zadanie tworzenia kopii zapasowej nie powiodło się, ponieważ oryginalne zadanie tworzenia kopii zapasowej jest w toku.

## <a name="troubleshooting-monitoring-issues"></a>Rozwiązywanie problemów monitorowania
**Problem:** zadania i/lub alerty z hello Azure Backup agent nie są wyświetlane w portalu hello.

**Kroki rozwiązywania problemów:** hello procesu ```OBRecoveryServicesManagementAgent```, wysyła hello zadania i alert toohello danych usługi Azure Backup. Czasami ten proces może zostać wstrzymana lub zamknięcie.

1. proces hello tooverify nie jest uruchomiony, otwórz **Menedżera zadań** i sprawdź, czy hello ```OBRecoveryServicesManagementAgent``` proces jest uruchomiony.
2. Przy założeniu, że proces hello nie jest uruchomiony, otwórz **Panelu sterowania** i Przeglądaj hello Lista usług. Uruchom lub uruchom ponownie **agenta usług odzyskiwania Microsoft Azure w zarządzania**.

    Aby uzyskać więcej informacji Przejdź dzienniki hello na:<br/>
   `<AzureBackup_agent_install_folder>\Microsoft Azure Recovery Services Agent\Temp\GatewayProvider*`Na przykład:<br/>
   `C:\Program Files\Microsoft Azure Recovery Services Agent\Temp\GatewayProvider0.errlog`

## <a name="next-steps"></a>Następne kroki
* [Przywracanie systemu Windows Server lub klienta systemu Windows z platformy Azure](backup-azure-restore-windows-server.md)
* toolearn więcej informacji na temat usługi Kopia zapasowa Azure, zobacz [Omówienie programu Kopia zapasowa Azure](backup-introduction-to-azure-backup.md)
* Odwiedź hello [Forum kopia zapasowa Azure](http://go.microsoft.com/fwlink/p/?LinkId=290933)
