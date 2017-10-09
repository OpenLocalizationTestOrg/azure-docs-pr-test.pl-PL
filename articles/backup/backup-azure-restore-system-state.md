---
title: 'Kopia zapasowa Azure: Tooa Przywracanie stanu systemu Windows Server | Dokumentacja firmy Microsoft'
description: "Krok wyjaśnienie krok przywracania stanu systemu Windows Server z kopii zapasowej na platformie Azure."
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: 
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/18/2017
ms.author: saurse;trinadhk;markgal;
ms.openlocfilehash: a45506507f53e2744350d3b6b2e52f1db415de4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="restore-system-state-toowindows-server"></a>Przywracanie stanu systemu tooWindows serwera

W tym artykule opisano, jak magazyn kopii zapasowych stanu systemu Windows Server toorestore z usług odzyskiwania Azure. toorestore stanu systemu, musi mieć kopię zapasową stanu systemu (utworzone za pomocą instrukcji hello w [Utwórz kopię zapasową stanu systemu](backup-azure-system-state.md#back-up-windows-server-system-state-preview)) i upewnij się, że zainstalowano hello [najnowszą wersję programu Microsoft Azure Recovery hello Agent usług (MARS)](http://aka.ms/azurebackup_agent). Odzyskiwanie stanu systemu Windows Server danych z magazynu usług odzyskiwania Azure jest procesem dwuetapowym:

1. Przywróć stan systemu jako pliki kopii zapasowej Azure. Podczas przywracania stanu systemu plików z kopii zapasowej Azure, można wykonać jedną z następujących czynności:
  * Przywracanie stanu systemu toohello tym samym serwerze, na których wykonano kopie zapasowe hello, lub
  * Przywracanie stanu systemu tooan alternatywny serwer plików.

2. Zastosuj hello przywrócić stan systemu plików tooa systemu Windows Server.


## <a name="recover-system-state-files-toohello-same-server"></a>Odzyskać stan systemu plików toohello tym samym serwerze
Witaj, wykonaj czynności wyjaśniają, jak tooroll kopii programu Windows Server konfiguracji tooa poprzedniego stanu. Wycofanie serwera konfiguracji tooa wstecz znane stabilności, może być bardzo istotne. Witaj poniższych stan systemu serwera kroków przywracania hello z magazynu usług odzyskiwania. 

1. Otwórz hello **kopia zapasowa Microsoft Azure** przystawki. Jeśli nie wiadomo, w którym zainstalowano przystawkę hello, wyszukaj hello komputerze lub serwerze dla **kopia zapasowa Microsoft Azure**.

    Aplikacja klasyczna Hello powinny być wyświetlane w wynikach wyszukiwania hello.

2. Kliknij przycisk **odzyskać dane** toostart hello kreatora.

    ![Odzyskiwanie danych](./media/backup-azure-restore-windows-server/recover.png)

3. Na powitania **wprowadzenie** okienka, toorestore hello danych toohello tego samego serwera lub komputera, wybierz **tego serwera (`<server name>`)** i kliknij przycisk **dalej**.

    ![Wybierz ten serwer opcja toorestore hello danych toohello tym samym komputerze](./media/backup-azure-restore-system-state/samemachine.png)

4. Na powitania **wybierz tryb odzyskiwania** okienku wybierz **stanu systemu** , a następnie kliknij przycisk **dalej**.

    ![Przeglądanie plików](./media/backup-azure-restore-system-state/recover-type-selection.png)

5. W kalendarzu hello w **Wybierz wolumin i data** punktu okienku, wybierz odzyskiwania. 

    Można przywrócić z dowolnego punktu odzyskiwania w czasie. Daty w **bold** wskazać hello dostępności co najmniej jeden punkt odzyskiwania. Po wybraniu Data, jeśli dostępnych jest wiele punktów odzyskiwania, wybierz hello określony punkt odzyskiwania z hello **czasu** menu rozwijanego.

    ![Data i woluminu](./media/backup-azure-restore-system-state/select-date.png)

6. Po wybraniu toorestore punktu odzyskiwania powitania kliknij **dalej**.

    Kopia zapasowa Azure instaluje punkt odzyskiwania lokalne powitania i używa go jako wolumin odzyskiwania.

7. W okienku dalej hello, określ lokalizację docelową hello hello odzyskać stan systemu plików, a następnie kliknij przycisk **Przeglądaj** tooopen Eksploratora Windows i Znajdź hello pliki i foldery mają. Witaj opcji **kopie tak, aby obie wersje**, tworzy kopie poszczególnych plików w istniejącego archiwum pliku stanu systemu zamiast tworzenia kopii hello hello całe archiwum stanu systemu.

    ![Opcje odzyskiwania](./media/backup-azure-restore-system-state/recover-as-files.png)

8. Sprawdź szczegóły hello odzyskiwania na powitania **potwierdzenie** okienko i kliknij przycisk **odzyskać**.

   ![Kliknij przycisk Odzyskaj tooacknowledge hello Odzyskaj akcji](./media/backup-azure-restore-system-state/confirm-recovery.png)

9. Kopiuj hello *WindowsImageBackup* katalogu w hello niekrytyczne woluminu tooa miejsce docelowe odzyskiwania powitania serwera. Zwykle woluminu systemu operacyjnego Windows hello jest hello wolumin krytyczny.

10. Po hello odzyskiwania zakończy się pomyślnie, wykonaj kroki hello w sekcji hello [Zastosuj przywrócić stan systemu plików toohello systemu Windows Server](backup-azure-restore-system-state.md#apply-restored-system-state-files-to-the-windows-server), hello toocomplete proces odzyskiwania stanu systemu.

## <a name="recover-system-state-files-tooan-alternate-server"></a>Alternatywny serwer tooan pliki odzyskać stan systemu

Jeśli serwera z systemem Windows jest uszkodzony lub jest niedostępny, i chcesz toorestore on tooa stabilności przez odzyskiwanie hello stanu systemu Windows Server, można przywrócić stan systemu serwera uszkodzony hello z innego serwera. Użyj hello następujące kroki toohello Przywracanie stanu systemu na osobnym serwerze.  

obejmuje Hello terminologią używaną w następujące kroki:

- *Maszyna źródłowa* — podjęto hello oryginalnego komputera z kopii zapasowej które hello i który jest obecnie niedostępny.
- *Maszyna docelowa* — Witaj maszyny toowhich hello dane są odzyskiwane.
- *Przykładowe magazynu* — hello toowhich magazyn usług odzyskiwania hello *maszyny źródłowej* i *maszyny docelowej* są rejestrowane. <br/>

> [!NOTE]
> Kopie zapasowe wykonane z jednego komputera nie może być tooa przywróconej maszyny ze starszą wersją systemu operacyjnego hello. Na przykład kopii zapasowych wykonanych z systemem Windows Server 2016 maszyny nie może być przywrócona tooWindows Server 2012 R2. Jednak odwrotność hello jest możliwe. Możesz użyć kopii zapasowych z toorestore systemu Windows Server 2012 R2, Windows Server 2016.
>

1. Otwórz hello **kopia zapasowa Microsoft Azure** przystawki na powitania *maszyny docelowej*.
2. Upewnij się, że hello *maszyny docelowej* i hello *maszyny źródłowej* są zarejestrowane toohello magazyn usług odzyskiwania tego samego.
3. Kliknij przycisk **odzyskać dane** tooinitiate hello w przepływie pracy.

    ![Odzyskiwanie danych](./media/backup-azure-restore-windows-server-classic/recover.png)

4. Wybierz **innego serwera**

    ![Inny serwer](./media/backup-azure-restore-system-state/anotherserver.png)

5. Podaj plik poświadczeń magazynu hello, która odpowiada toohello *magazynu próbki*. Jeśli plik poświadczeń magazynu hello jest nieprawidłowa (lub wygasła), Pobierz plik poświadczeń magazynu z hello *magazynu próbki* w hello portalu Azure. Po podany plik poświadczeń magazynu hello hello magazyn usług odzyskiwania skojarzonych z plik poświadczeń magazynu hello zostanie wyświetlony.

6. W okienku wybierz pozycję Utwórz kopię zapasową serwera hello wybierz hello *maszyny źródłowej* z listy hello wyświetlanych maszyn.

    ![Lista komputerów](./media/backup-azure-restore-windows-server-classic/machinelist.png)

7. W okienku wybierz tryb odzyskiwania hello, wybierz **stanu systemu** i kliknij przycisk **dalej**. 

    ![Wyszukiwanie](./media/backup-azure-restore-system-state/recover-type-selection.png)

8. Na powitania kalendarza w hello **Wybierz wolumin i data** punktu okienku, wybierz odzyskiwania. Można przywrócić z dowolnego punktu odzyskiwania w czasie. Daty w **bold** wskazać hello dostępności co najmniej jeden punkt odzyskiwania. Po wybraniu Data, jeśli dostępnych jest wiele punktów odzyskiwania, wybierz hello określony punkt odzyskiwania z hello **czasu** menu rozwijanego. 

    ![Wyszukiwanie elementów](./media/backup-azure-restore-system-state/select-date.png)

9. Po wybraniu toorestore punktu odzyskiwania powitania kliknij **dalej**.

10. Na powitania **wybierz tryb odzyskiwania stanu systemu** okienka, określ docelowy hello miejscu toobe odzyskane pliki stanu systemu, a następnie kliknij **dalej**.

    ![Szyfrowanie](./media/backup-azure-restore-system-state/recover-as-files.png)

    Witaj opcji **kopie tak, aby obie wersje**, tworzy kopie poszczególnych plików w istniejącego archiwum pliku stanu systemu zamiast tworzenia kopii hello hello całe archiwum stanu systemu.

11. Sprawdź szczegóły hello odzyskiwania w okienku potwierdzenie hello, a następnie kliknij przycisk **odzyskać**. 

    ![proces odzyskiwania hello tooconfirm przycisk Odzyskaj powitania kliknij](./media/backup-azure-restore-system-state/confirm-recovery.png)

12. Kopiuj hello *WindowsImageBackup* katalogu tooa niekrytyczne woluminu powitania serwera (na przykład D:\). Wolumin systemu operacyjnego Windows hello jest zazwyczaj hello wolumin krytyczny.

13. proces odzyskiwania hello toocomplete, użyj następujących hello sekcji zbyt[zastosować hello przywrócić stan systemu plików w systemie Windows Server](backup-azure-restore-system-state.md#apply-restored-system-state-on-a-windows-server).




## <a name="apply-restored-system-state-on-a-windows-server"></a>Zastosuj przywróconego stanu systemu w systemie Windows Server

Po odzyskały stan systemu jako plików za pomocą agenta usług odzyskiwania Azure, użyj hello kopia zapasowa systemu Windows Server narzędzie tooapply hello odzyskać tooWindows stanu systemu serwera. Witaj narzędzie Kopia zapasowa systemu Windows Server jest już dostępny na powitania serwera. Hello następujące kroki opisano, jak tooapply hello odzyskać stan systemu.

1. Użyj następujących hello polecenia tooreboot serwera w *trybie naprawy usług katalogowych*. W wierszu polecenia z podwyższonym poziomem uprawnień:

    ```
    PS C:\> Bcdedit /set safeboot dsrepair
    PS C:\> Shutdown /r /t 0
    ```

2. Po ponownym uruchomieniu hello Otwórz przystawkę narzędzia Kopia zapasowa systemu Windows Server hello. Jeśli nie wiadomo, w którym zainstalowano przystawkę hello, wyszukaj hello komputerze lub serwerze dla **kopia zapasowa systemu Windows Server**.

    Aplikacja klasyczna Hello pojawia się w wynikach wyszukiwania hello.

3. W przystawce hello, wybierz **lokalna kopia zapasowa**.

    ![Wybierz z tego miejsca toorestore lokalna kopia zapasowa](./media/backup-azure-restore-system-state/win-server-backup-local-backup.png)

4. Na powitania lokalna kopia zapasowa w konsoli hello **okienka Akcje**, kliknij przycisk **odzyskać** hello tooopen Kreatora odzyskiwania.

5. Wybierz opcję hello **kopia zapasowa jest przechowywana w innej lokalizacji**i kliknij przycisk **dalej**.

   ![Wybierz inny serwer tooa toorecover](./media/backup-azure-restore-system-state/backup-stored-in-diff-location.png)

6. Podczas określania typu lokalizacji hello, wybierz **zdalnego folderu udostępnionego** Jeśli kopia zapasowa stanu systemu serwera tooanother odzyskane. Jeśli stan systemu został odzyskany lokalnie, następnie wybierz **dyski lokalne**. 

    ![Wybierz czy toorecovery z serwera lokalnego lub innego](./media/backup-azure-restore-system-state/ss-recovery-remote-shared-folder.png)

7. Wprowadź hello ścieżki toohello *WindowsImageBackup* katalogu, lub wybrać dysk lokalne powitania zawierający ten katalog (na przykład D:\WindowsImageBackup) odzyskiwane podczas odzyskiwania pliki stanu systemu hello za pomocą odzyskiwania Azure Usługi agenta i kliknij przycisk **dalej**.

    ![Ścieżka toohello udostępnionych plików](./media/backup-azure-restore-system-state/ss-recovery-remote-folder.png)

8. Wybierz hello stanu systemu wersji mają toorestore i kliknij przycisk **dalej**.

9. Wybierz w okienku Wybieranie typu odzyskiwania hello **stanu systemu** i kliknij przycisk **dalej**.

10. Dla lokalizacji hello hello odzyskiwania stanu systemu, wybierz **oryginalnej lokalizacji**i kliknij przycisk **dalej**.

11. Przejrzyj szczegóły potwierdzenie hello, sprawdź ustawienia ponowny rozruch hello, a następnie kliknij przycisk **odzyskać** tooapplly hello przywrócić stan systemu plików.

    ![hello uruchamiania Przywracanie stanu systemu plików](./media/backup-azure-restore-system-state/launch-ss-recovery.png)

## <a name="special-considerations-for-system-state-recovery-on-active-directory-server"></a>Uwagi dotyczące odzyskiwania stanu systemu na serwerze usługi Active Directory

Kopia zapasowa stanu systemu zawiera danych usługi Active Directory. Użyj hello poniższych kroków toorestore usług domenowych w usłudze Active Directory (AD DS) z jego bieżącym stanie tooa poprzedniego stanu.

1. Uruchom ponownie kontroler domeny hello w trybie przywracania usług katalogowych (DSRM).
2. Wykonaj kroki hello [tutaj](https://technet.microsoft.com/en-us/library/cc794755(v=ws.10).aspx) toorecover poleceń cmdlet narzędzia Kopia zapasowa systemu Windows Server toouse usług AD DS.


## <a name="troubleshoot-failed-system-state-restore"></a>Rozwiązywanie problemów z niepowodzeniem Przywracanie stanu systemu

Jeśli hello poprzedniego procesu stosowania stan systemu nie zakończy się pomyślnie, należy użyć toorecover środowisko odzyskiwania systemu Windows (Windows RE) powitania serwera z systemem Windows. Witaj poniższych krokach opisano sposób toorecover przy użyciu środowiska Windows RE. Użyj tej opcji tylko wtedy, gdy system Windows Server nie normalny rozruch po przywróceniu stanu systemu. powitania po procesie powoduje usunięcie danych z systemem innym niż system, ostrożność. 

1. Przeprowadź rozruch serwera z systemem Windows w hello środowisko odzyskiwania systemu Windows (Windows RE).

2. Wybierz Rozwiązywanie problemów z trzech dostępnych opcji hello.

    ![Otwieranie menu](./media/backup-azure-restore-system-state/winre-1.png)

3. Z hello **zaawansowane opcje** ekranu wybierz **wiersza polecenia** i podaj nazwę użytkownika administratora serwera hello i hasło.

   ![Otwieranie menu](./media/backup-azure-restore-system-state/winre-2.png)

4. Podaj nazwę użytkownika administratora serwera hello i hasło.

    ![Otwieranie menu](./media/backup-azure-restore-system-state/winre-3.png)

5. Po otwarciu hello wiersza polecenia w trybie administratora, uruchom następujące polecenie tooget hello stanu systemu kopii zapasowych.

    ```
    Wbadmin get versions -backuptarget:<Volume where WindowsImageBackup folder is copied>:
    ```
    ![Pobieranie wersji kopii zapasowej stanu systemu](./media/backup-azure-restore-system-state/winre-4.png)

6. Uruchom następujące polecenie tooget hello wszystkich woluminów dostępnych w programie Kopia zapasowa hello.

    ```
    Wbadmin get items -version:<copy version from above step> -backuptarget:<Backup volume>
    ```

    ![Pobieranie wersji kopii zapasowej stanu systemu](./media/backup-azure-restore-system-state/winre-5.png)

7. Witaj następujące polecenie przywraca wszystkie woluminy, które są częścią hello kopii zapasowej stanu systemu. Należy pamiętać, że ten krok umożliwia odzyskiwanie tylko hello woluminów krytycznych, które są częścią hello stanu systemu. Wszystkie dane z systemem innym niż System jest usunięte.

    ```
    Wbadmin start recovery -items:C: -itemtype:Volume -version:<Backupversion> -backuptarget:<backup target volume>
    ```
     ![Pobieranie wersji kopii zapasowej stanu systemu](./media/backup-azure-restore-system-state/winre-6.png)



## <a name="next-steps"></a>Następne kroki
* Teraz, gdy zostały odzyskane pliki i foldery, możesz [Zarządzanie kopii zapasowych](backup-azure-manage-windows-server.md).
