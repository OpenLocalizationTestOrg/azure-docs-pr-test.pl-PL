---
title: "magazynami kopii zapasowych Azure aaaManage i hello klasycznego modelu wdrażania przy użyciu serwerów Azure | Dokumentacja firmy Microsoft"
description: "Użyj tego samouczka toolearn jak magazyny toomanage kopia zapasowa Azure i serwerów."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: tysonn
ms.assetid: f175eb12-0905-437f-91fd-eaee03ab6e81
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: markgal;
ms.openlocfilehash: 6c38b04f4a76604bfd639a9b2d58237ce44e2386
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-backup-vaults-and-servers-using-hello-classic-deployment-model"></a>Zarządzanie magazynami kopia zapasowa Azure i serwerami przy użyciu hello klasycznego modelu wdrażania
> [!div class="op_single_selector"]
> * [Resource Manager](backup-azure-manage-windows-server.md)
> * [Wdrożenie klasyczne](backup-azure-manage-windows-server-classic.md)
>
>

W tym artykule znajdziesz Przegląd zadań zarządzania kopiami zapasowymi hello dostępne za pośrednictwem hello klasycznego portalu Azure i hello agenta kopii zapasowej Microsoft Azure.

> [!IMPORTANT]
> Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../azure-resource-manager/resource-manager-deployment-model.md). W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia hello. Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager.

> [!IMPORTANT]
> Teraz można uaktualnić Twoje Magazyny usług tooRecovery magazynów kopii zapasowych. Aby uzyskać więcej informacji, zobacz artykuł hello [uaktualnienia tooa magazynu kopii zapasowej, Magazyn usług odzyskiwania i](backup-azure-upgrade-backup-to-recovery-services.md). Firma Microsoft zachęca tooupgrade Magazyny usług tooRecovery magazyny kopii zapasowych.<br/> Po 15 października 2017 nie można użyć magazyny kopii zapasowych toocreate środowiska PowerShell. **Do 1 listopada 2017 r.**:
>- Wszystkie pozostałe magazyny kopii zapasowych zostanie automatycznie uaktualniony tooRecovery Magazyny usług.
>- Użytkownik nie będzie możliwe tooaccess danych kopii zapasowych w portalu klasycznym hello. Zamiast tego użyj hello Azure tooaccess portalu tej kopii zapasowej w Magazyny usług odzyskiwania.
>

## <a name="management-portal-tasks"></a>Zadania portalu zarządzania
1. Zaloguj się toohello [portalu zarządzania](https://manage.windowsazure.com).
2. Kliknij przycisk **usług odzyskiwania**, następnie kliknij nazwę magazynu kopii zapasowych strony Szybki Start hello tooview hello.

    ![Usługi odzyskiwania](./media/backup-azure-manage-windows-server-classic/rs-left-nav.png)

Wybierając opcje hello u góry strony Szybki Start hello hello widać hello dostępnych zadań zarządzania.

![Zarządzanie karty](./media/backup-azure-manage-windows-server-classic/qs-page.png)

### <a name="dashboard"></a>Pulpit nawigacyjny
Wybierz **pulpitu nawigacyjnego** przegląd wykorzystania hello toosee powitania serwera. Witaj **przegląd wykorzystania** obejmuje:

* toocloud zarejestrowany Hello liczby serwerów systemu Windows
* Witaj liczbę maszyn wirtualnych platformy Azure chroniona w chmurze
* Całkowita ilość miejsca Hello zużyte na platformie Azure
* Witaj stan ostatnich zadań

U dołu hello hello pulpit nawigacyjny umożliwia wykonywanie hello następujące zadania:

* **Zarządzanie certyfikatami** — Jeśli certyfikat został użyty tooregister powitania serwera, a następnie użycie tego certyfikatu hello tooupdate. Jeśli używane są poświadczenia magazynu, nie używaj **Zarządzaj certyfikatem**.
* **Usuń** — usuwa hello bieżącego magazynu kopii zapasowych. Jeśli magazyn kopii zapasowych jest już używana, można usunąć toofree miejsca do magazynowania. **Usuń** jest włączona tylko po wszystkie zarejestrowane serwery zostały usunięte z magazynu hello.

![Zadania tworzenia kopii zapasowej pulpitu nawigacyjnego](./media/backup-azure-manage-windows-server-classic/dashboard-tasks.png)

## <a name="registered-items"></a>Zarejestrowanych elementów
Wybierz **zarejestrowane elementy** nazwy hello tooview hello serwerów, które są zarejestrowane toothis magazynu.

![Zarejestrowanych elementów](./media/backup-azure-manage-windows-server-classic/registered-items.png)

Witaj **typu** filtru domyślne tooAzure maszyny wirtualnej. nazwy hello tooview hello serwerów, które są zarejestrowane toothis magazynu, wybierz **systemu Windows server** z hello menu rozwijanym.

W tym miejscu można wykonywać następujące zadania hello:

* **Zezwalaj na ponowną rejestrację** — po wybraniu tej opcji można użyć serwera hello **Kreatora rejestracji** hello lokalnymi kopia zapasowa Microsoft Azure agenta tooregister hello Server z magazynem kopii zapasowych powitania po raz drugi . Może być konieczne toore rejestru ze względu na błąd tooan hello certyfikatu lub jeśli serwer ma toobe odbudowane.
* **Usuń** — usuwa serwer z magazynu kopii zapasowych hello. Wszystkie hello przechowywane dane skojarzone z serwerem hello zostaną natychmiast usunięte.

    ![Zarejestrowanych elementów zadań](./media/backup-azure-manage-windows-server-classic/registered-items-tasks.png)

## <a name="protected-items"></a>Elementy chronione
Wybierz **chronione elementy** tooview hello elementy, które kopii zapasowej z hello serwerów.

![Elementy chronione](./media/backup-azure-manage-windows-server-classic/protected-items.png)

## <a name="configure"></a>Konfigurowanie
Z hello **Konfiguruj** karcie można wybrać opcję nadmiarowość magazynu odpowiednie hello. Hello najlepszym czasu tooselect hello magazynu nadmiarowość rozwiązaniem jest bezpośrednio po utworzenie magazynu i przed tooit zarejestrowane są wszystkie maszyny.

> [!WARNING]
> Po powiązaniu elementu z magazynu zarejestrowanych toohello opcji nadmiarowość magazynu hello jest zablokowany i nie może być modyfikowany.
>
>

![Konfigurowanie](./media/backup-azure-manage-windows-server-classic/configure.png)

Zobacz ten artykuł, aby uzyskać więcej informacji [nadmiarowość magazynu](../storage/common/storage-redundancy.md).

## <a name="microsoft-azure-backup-agent-tasks"></a>Zadania agenta usługi Kopia zapasowa Microsoft Azure
### <a name="console"></a>Konsola
Otwórz hello **agenta usługi Kopia zapasowa Microsoft Azure** (można go znaleźć, wyszukaj na maszynie łańcuch *kopia zapasowa Microsoft Azure*).

![Agent usługi Kopia zapasowa](./media/backup-azure-manage-windows-server-classic/snap-in-search.png)

Z hello **akcje** dostępne pod adresem hello rogu konsoli agenta kopii zapasowej hello można wykonywać na powitania następujące zadania związane z zarządzaniem:

* Zarejestruj serwer
* Harmonogram tworzenia kopii zapasowych
* Wykonaj kopię zapasową teraz
* Zmień właściwości

![Akcje konsoli agentów.](./media/backup-azure-manage-windows-server-classic/console-actions.png)

> [!NOTE]
> zbyt**odzyskać dane**, zobacz [przywrócić pliki tooa systemu Windows server lub komputer kliencki z systemem Windows](backup-azure-restore-windows-server.md).
>
>

### <a name="modify-an-existing-backup"></a>Modyfikowanie istniejącej kopii zapasowej
1. W agencie kopia zapasowa Microsoft Azure powitania kliknij **harmonogram tworzenia kopii zapasowych**.

    ![Planowanie kopii zapasowych serwera systemu Windows](./media/backup-azure-manage-windows-server-classic/schedule-backup.png)
2. W hello **Kreatora harmonogramu kopii zapasowej** pozostaw hello **wprowadzanie zmian elementów toobackup lub razy** zaznaczono opcję i kliknij przycisk **dalej**.

    ![Modyfikowanie zaplanowanego tworzenia kopii zapasowej](./media/backup-azure-manage-windows-server-classic/modify-or-stop-a-scheduled-backup.png)
3. Jeśli chcesz tooadd lub zmienić elementy na powitania **tooBackup wybierz elementy** ekranu kliknij **Dodaj elementy**.

    Można również ustawić **ustawienia wykluczania** na tej stronie kreatora hello. Jeśli pliki tooexclude lub typów plików odczytu hello procedurę dodawania [ustawienia wykluczania](#exclusion-settings).
4. Wybierz hello pliki i foldery mają tooback w górę i kliknij przycisk **OK**.

    ![Dodaj elementy](./media/backup-azure-manage-windows-server-classic/add-items-modify.png)
5. Określ hello **harmonogram tworzenia kopii zapasowych** i kliknij przycisk **dalej**.

    Można zaplanować codziennie (maksymalnie 3 razy dziennie) lub cotygodniowe kopie zapasowe.

    ![Określ harmonogram tworzenia kopii zapasowej](./media/backup-azure-manage-windows-server-classic/specify-backup-schedule-modify-close.png)

   > [!NOTE]
   > Określanie harmonogramu tworzenia kopii zapasowych hello omówiono szczegółowo w tym [artykułu](backup-azure-backup-cloud-as-tape.md).
   >
   >
6. Wybierz hello **zasady przechowywania** hello kopii zapasowej, a następnie kliknij przycisk **dalej**.

    ![Wybierz zasady przechowywania](./media/backup-azure-manage-windows-server-classic/select-retention-policy-modify.png)
7. Na powitania **potwierdzenie** ekran Przegląd hello informacji i kliknij przycisk **Zakończ**.
8. Gdy Kreator hello zakończy tworzenie hello **harmonogram tworzenia kopii zapasowych**, kliknij przycisk **Zamknij**.

    Po zmodyfikowaniu ochrony, można potwierdzić poprawnie wyzwalają kopii zapasowych przez przejście toohello **zadania** kartę i potwierdzenie, że zmiany zostaną odzwierciedlone w hello kopii zapasowej zadania.

### <a name="enable-network-throttling"></a>Włącz ograniczanie przepustowości sieci
agent usługi Kopia zapasowa Azure Hello zawiera kartę ograniczenia przepustowości, co pozwala toocontrol wykorzystaniem przepustowości sieci podczas transferu danych. Ten formant może być przydatne, gdy konieczne tooback zapasową danych poza godzinami pracy, ale nie chcesz hello toointerfere procesu tworzenia kopii zapasowej z innych ruch internetowy. Ograniczanie danych transfer stosuje tooback zapasową i przywrócić działań.  

Ograniczanie tooenable:

1. W hello **agent usługi Kopia zapasowa**, kliknij przycisk **Zmień właściwości**.
2. Wybierz hello **włączyć użycia przepustowości połączenia internetowego do operacji tworzenia kopii zapasowej** wyboru.

    ![Ograniczanie przepustowości sieci](./media/backup-azure-manage-windows-server-classic/throttling-dialog.png)
3. Po włączeniu ograniczenia przepustowości, określ hello dozwolone przepustowości dla transferu danych kopii zapasowej podczas **godzin pracy** i **godziny wolne**.

    wartości przepustowości Hello rozpoczynały 512 kilobajtach na sekundę (KB/s) i można przejść w górę too1023 MB na sekundę (MB/s). Można również wyznaczyć hello rozpoczęcia i zakończenia **godzin pracy**, i dni tygodnia hello są traktowane jako pracy dni. czas Hello poza Witaj wyznaczone godzin pracy jest godzin wolnych toobe rozważenia.
4. Kliknij przycisk **OK**.

## <a name="exclusion-settings"></a>Ustawienia wykluczania
1. Otwórz hello **agenta usługi Kopia zapasowa Microsoft Azure** (można go znaleźć, wyszukaj na maszynie łańcuch *kopia zapasowa Microsoft Azure*).

    ![Otwórz agenta kopii zapasowej](./media/backup-azure-manage-windows-server-classic/snap-in-search.png)
2. W agencie kopia zapasowa Microsoft Azure powitania kliknij **harmonogram tworzenia kopii zapasowych**.

    ![Planowanie kopii zapasowych serwera systemu Windows](./media/backup-azure-manage-windows-server-classic/schedule-backup.png)
3. W hello Kreatora harmonogramu kopii zapasowej pozostaw hello **wprowadzanie zmian elementów toobackup lub razy** zaznaczono opcję i kliknij przycisk **dalej**.

    ![Modyfikowanie harmonogramu](./media/backup-azure-manage-windows-server-classic/modify-or-stop-a-scheduled-backup.png)
4. Kliknij przycisk **ustawienia wykluczenia**.

    ![Wybierz elementy tooexclude](./media/backup-azure-manage-windows-server-classic/exclusion-settings.png)
5. Kliknij przycisk **Dodaj wykluczenia**.

    ![Dodaj wykluczenia](./media/backup-azure-manage-windows-server-classic/add-exclusion.png)
6. Wybierz lokalizację hello, a następnie kliknij przycisk **OK**.

    ![Wybierz lokalizację do wykluczenia](./media/backup-azure-manage-windows-server-classic/exclusion-location.png)
7. Dodaj rozszerzenie pliku hello w hello **typ pliku** pola.

    ![Wyklucz według typu pliku](./media/backup-azure-manage-windows-server-classic/exclude-file-type.png)

    Dodawanie rozszerzenia MP3

    ![Przykład typu pliku](./media/backup-azure-manage-windows-server-classic/exclude-mp3.png)

    tooadd inne rozszerzenie, kliknij przycisk **Dodawanie wykluczenia** i wprowadź inne rozszerzenie typu pliku (Dodawanie rozszerzenia .jpeg).

    ![Innym przykładem typu pliku](./media/backup-azure-manage-windows-server-classic/exclude-jpg.png)
8. Po dodaniu wszystkich rozszerzeń powitania kliknij **OK**.
9. Kontynuuj hello Kreatora harmonogramu kopii zapasowej, klikając **dalej** do hello **stronę potwierdzenia**, następnie kliknij przycisk **Zakończ**.

    ![Potwierdzenie wyłączenia](./media/backup-azure-manage-windows-server-classic/finish-exclusions.png)

## <a name="next-steps"></a>Następne kroki
* [Przywracanie systemu Windows Server lub klienta systemu Windows z platformy Azure](backup-azure-restore-windows-server.md)
* toolearn więcej informacji na temat usługi Kopia zapasowa Azure, zobacz [Omówienie programu Kopia zapasowa Azure](backup-introduction-to-azure-backup.md)
* Odwiedź hello [Forum kopia zapasowa Azure](http://go.microsoft.com/fwlink/p/?LinkId=290933)
