---
title: "aaaBack się tooAzure stanu systemu Windows | Dokumentacja firmy Microsoft"
description: "Dowiedz się tooback hello stanu systemu Windows Server i/lub tooAzure komputerów z systemem Windows."
services: backup
documentationcenter: 
author: saurabhsensharma
manager: carmonm
editor: 
keywords: "jak toobackup; jak tooback; kopii zapasowej plików i folderów"
ms.assetid: 5b15ebf1-2214-4722-b937-96e2be8872bb
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: saurse;markgal
ms.openlocfilehash: be5d4be81af981c10de82add9fe962a730753cf5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-windows-system-state-in-resource-manager-deployment"></a>Wykonaj kopię zapasową stanu systemu Windows podczas wdrażania usługi Resource Manager
W tym artykule opisano, jak stan tooAzure: tooback systemu Windows Server. Jest samouczek toowalk danego użytkownika przez proces hello podstawy.

Więcej informacji na temat tworzenia kopii zapasowej Azure tooknow należy przeczytać ten tekst [omówienie](backup-introduction-to-azure-backup.md).

Jeśli nie masz subskrypcji platformy Azure, utwórz [bezpłatne konto](https://azure.microsoft.com/free/) umożliwiające dostęp do dowolnej usługi Azure.

## <a name="create-a-recovery-services-vault"></a>Tworzenie magazynu usługi Recovery Services
tooback zapasową plików i folderów, należy toocreate magazynu usług odzyskiwania w regionie hello miejscu toostore hello danych. Należy również toodetermine sposób replikowania magazynu.

### <a name="toocreate-a-recovery-services-vault"></a>toocreate magazynu usług odzyskiwania
1. Jeśli jeszcze tego nie zrobiono, zaloguj się w toohello [Azure Portal](https://portal.azure.com/) przy użyciu subskrypcji platformy Azure.
2. W menu Centrum powitania kliknij **więcej usług** i hello listy zasobów, wpisz **usług odzyskiwania** i kliknij przycisk **Magazyny usług odzyskiwania**.

    ![Tworzenie magazynu usługi Recovery Services — krok 1](./media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    Jeśli występują Magazyny usług odzyskiwania w ramach subskrypcji hello, magazynów hello są wyświetlane.
3. Na powitania **Magazyny usług odzyskiwania** menu, kliknij przycisk **Dodaj**.

    ![Tworzenie magazynu Usług odzyskiwania — krok 2](./media/backup-try-azure-backup-in-10-mins/rs-vault-menu.png)

    Usługi odzyskiwania Hello zostanie otwarty blok magazyn monitem tooprovide **nazwa**, **subskrypcji**, **grupy zasobów**, i **lokalizacji**.

    ![Tworzenie magazynu usługi Recovery Services — krok 3](./media/backup-try-azure-backup-in-10-mins/rs-vault-step-3.png)

4. Aby uzyskać **nazwa**, wprowadź przyjazną nazwę tooidentify hello magazynu. Nazwa Hello musi toobe unikatowy dla hello subskrypcji platformy Azure. Wpisz nazwę o długości od 2 do 50 znaków. Musi ona rozpoczynać się od litery i może zawierać tylko litery, cyfry i łączniki.

5. W hello **subskrypcji** Użyj hello menu rozwijanego toochoose hello subskrypcji platformy Azure. Jeśli używasz tylko jedną subskrypcję, wyświetlonym subskrypcji i toohello następny krok można pominąć. Jeśli nie masz pewności, który toouse subskrypcji, użyj domyślnej hello (lub sugerowane) subskrypcji. Większa liczba opcji do wyboru jest dostępna tylko w przypadku, gdy konto organizacji jest skojarzone z wieloma subskrypcjami platformy Azure.

6. W hello **grupy zasobów** sekcji:

    * Wybierz **Utwórz nowy** Jeśli toocreate grupę zasobów.
    Lub
    * Wybierz **Użyj istniejącego** i kliknij przycisk hello menu rozwijanego toosee hello listę dostępnych grup zasobów.

  Aby uzyskać pełne informacje na temat grup zasobów, zobacz hello [Omówienie usługi Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).

7. Kliknij przycisk **lokalizacji** tooselect hello region geograficzny magazynu hello. Ten wybór Określa region geograficzny hello wysyłania danych kopii zapasowych.

8. U dołu hello blok magazyn usług odzyskiwania hello, kliknij przycisk **Utwórz**.

    Może upłynąć kilka minut hello toobe utworzony magazyn usług odzyskiwania. Monitor stanu hello powiadomienia w górnym obszarze po prawej stronie powitania hello portalu. Po utworzeniu magazynu zostanie wyświetlony hello listę magazynów usług odzyskiwania. Jeśli po kilku minutach nie widzisz swojego magazynu, kliknij pozycję **Odśwież**.

    ![Klikanie pozycji Odśwież](./media/backup-try-azure-backup-in-10-mins/refresh-button.png)</br>

    Przeanalizowanie magazynu na liście hello magazynów usług odzyskiwania jest nadmiarowość magazynu hello tooset gotowe.

### <a name="set-storage-redundancy-for-hello-vault"></a>Ustaw nadmiarowość magazynu dla magazynu hello
Podczas tworzenia magazynu usług odzyskiwania, upewnij się, że sposób skonfigurowanych hello jest nadmiarowość magazynu.

1. Z hello **Magazyny usług odzyskiwania** bloku, kliknij przycisk Nowy magazyn hello.

    ![Wybierz nowy magazyn hello z listy hello magazynu usług odzyskiwania](./media/backup-try-azure-backup-in-10-mins/rs-vault-list.png)

    Po wybraniu magazynu hello hello **magazyn usług odzyskiwania i** narrows bloku oraz blok ustawień hello (*mającego nazwę hello magazynu hello u góry hello*) i hello magazynu szczegóły blok otwarte.

    ![Widok konfiguracji magazynu hello nowy magazyn](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration-2.png)
2. W bloku ustawienia hello nowy magazyn, użyj tooscroll pionowy slajdów hello dół toohello sekcji Zarządzaj, a następnie kliknij przycisk **infrastruktura kopii zapasowej**.
    zostanie otwarty blok infrastruktura kopii zapasowej Hello.
3. W bloku infrastruktura kopii zapasowej powitania kliknij **konfiguracji kopii zapasowej** tooopen hello **konfiguracji kopii zapasowej** bloku.

    ![Ustaw hello konfigurację magazynu dla nowego magazynu](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration.png)
4. Wybierz hello odpowiednią opcję replikacji dla magazynu.

    ![Opcje konfiguracji usługi Storage](./media/backup-try-azure-backup-in-10-mins/choose-storage-configuration.png)

    Domyślnie magazyn jest nadmiarowy geograficznie. Jeśli używasz platformy Azure jako punktu końcowego podstawowego magazynu kopii zapasowych nadal toouse **geograficznie nadmiarowego**. Jeśli nie używasz Azure jako punktu końcowego podstawowego magazynu kopii zapasowych, należy wybrać **lokalnie nadmiarowego**, co zmniejsza koszty usługi Azure storage hello. Więcej informacji o opcjach magazynu [geograficznie nadmiarowego](../storage/common/storage-redundancy.md#geo-redundant-storage) i [lokalnie nadmiarowego](../storage/common/storage-redundancy.md#locally-redundant-storage) można znaleźć w tym [omówieniu nadmiarowości magazynu](../storage/common/storage-redundancy.md).

Teraz, po utworzeniu magazynu, należy go skonfigurować do tworzenia kopii zapasowej stanu systemu Windows.

## <a name="configure-hello-vault"></a>Konfigurowanie magazynu hello
1. Na hello bloku magazyn usług odzyskiwania (dla hello właśnie utworzony magazyn), w sekcji wprowadzenie hello, kliknij przycisk **kopii zapasowej**, następnie na powitania **wprowadzenie do korzystania z kopii zapasowej** bloku, wybierz  **Celem tworzenia kopii zapasowej**.

    ![Otwieranie bloku celu kopii zapasowej](./media/backup-try-azure-backup-in-10-mins/open-backup-settings.png)

    Witaj **cel kopii zapasowej** zostanie otwarty blok.

    ![Otwieranie bloku celu kopii zapasowej](./media/backup-try-azure-backup-in-10-mins/backup-goal-blade.png)

2. Z hello **gdzie działa Twoje obciążenie?** menu rozwijanego wybierz **lokalnymi**.

    Pozycję **Lokalnie** trzeba wybrać, ponieważ Twój serwer lub komputer z systemem Windows jest maszyną fizyczną spoza platformy Azure.

3. Z hello **co chcesz toobackup?** menu, wybierz opcję **stanu systemu**i kliknij przycisk **OK**.

    ![Konfigurowanie plików i folderów](./media/backup-azure-system-state/backup-goal-system-state.png)

    Po kliknięciu przycisku OK znacznik wyboru pojawia się dalej zbyt**cel kopii zapasowej**i hello **przygotowanie infrastruktury** zostanie otwarty blok.

    ![Cel kopii zapasowej został skonfigurowany, następnym krokiem jest przygotowanie infrastruktury](./media/backup-try-azure-backup-in-10-mins/backup-goal-configed.png)

4. Na powitania **przygotowanie infrastruktury** bloku, kliknij przycisk **Pobierz agenta dla systemu Windows Server lub klienta systemu Windows**.

    ![Przygotowywanie infrastruktury](./media/backup-try-azure-backup-in-10-mins/choose-agent-for-server-client.png)

    Jeśli używasz systemu Windows Server podstawowych, a następnie wybierz pozycję toodownload hello agenta dla systemu Windows Server podstawowych. Menu podręczne monit toorun lub zapisać MARSAgentInstaller.exe.

    ![Okno dialogowe MARSAgentInstaller](./media/backup-try-azure-backup-in-10-mins/mars-installer-run-save.png)

5. W menu podręcznym pobierania hello, kliknij przycisk **zapisać**.

    Domyślnie program hello **MARSagentinstaller.exe** plik jest zapisywany w folderze pobrane tooyour. Po zakończeniu działania Instalatora hello, pojawi się okno podręczne, jeśli Instalator hello toorun lub Otwórz hello folder.

    ![Przygotowywanie infrastruktury](./media/backup-try-azure-backup-in-10-mins/mars-installer-complete.png)

    Nie należy jeszcze tooinstall hello agenta. Można zainstalować agenta hello pobrane hello poświadczenia magazynu.

6. Na powitania **przygotowanie infrastruktury** bloku, kliknij przycisk **Pobierz**.

    ![Pobieranie poświadczeń magazynu](./media/backup-try-azure-backup-in-10-mins/download-vault-credentials.png)

    poświadczenia magazynu Hello Pobierz tooyour folderze pobrane. Po poświadczenia magazynu hello zakończyć pobieranie, zostanie wyświetlony okno podręczne, jeśli chcesz tooopen lub Zapisz hello poświadczenia. Kliknij pozycję **Zapisz**. Jeśli przypadkowo kliknij **Otwórz**, let okno dialogowe hello prób poświadczenia magazynu hello tooopen, zakończyć się niepowodzeniem. Nie można otworzyć hello poświadczenia magazynu. Kontynuować toohello następnego kroku. poświadczenia magazynu Hello znajdują się w folderze pobrane hello.   

    ![Zakończenie pobierania poświadczeń magazynu](./media/backup-try-azure-backup-in-10-mins/vault-credentials-downloaded.png)

## <a name="install-and-register-hello-agent"></a>Zainstaluj i zarejestruj hello agenta

> [!NOTE]
> Włączenie kopii zapasowej za pomocą portalu Azure hello nie jest jeszcze dostępna. Użyj tooback agenta usług odzyskiwania Microsoft Azure hello stanu systemu Windows Server.
>

1. Zlokalizuj i kliknij dwukrotnie hello **MARSagentinstaller.exe** z hello pobieranie folderu (lub innej lokalizacji).

    Instalator Hello zapewnia szereg wiadomości, ponieważ wyodrębnia on, instaluje i rejestruje hello agenta usług odzyskiwania.

    ![Uruchamianie Instalatora agenta usługi Recovery Services — poświadczenia](./media/backup-try-azure-backup-in-10-mins/mars-installer-registration.png)

2. Ukończyć powitalnych Kreatora instalacji agenta usług odzyskiwania Microsoft Azure. Kreator hello toocomplete, musisz:

   * Wybierz lokalizację dla folderu instalacji i pamięci podręcznej hello.
   * Podaj informacje o serwerze proxy, jeśli używasz toohello tooconnect serwera proxy internet.
   * Podaj swoją nazwę użytkownika i hasło, jeśli korzystasz z uwierzytelnionego serwera proxy.
   * Podaj poświadczenia magazynu pobrane hello
   * Zapisz hasło szyfrowania hello w bezpiecznej lokalizacji.

     > [!NOTE]
     > Jeśli użytkownik zapomni hasła hello, Microsoft nie może odzyskać hello dane kopii zapasowej. Zapisz plik hello w bezpiecznej lokalizacji. Jest wymagane toorestore kopii zapasowej.
     >
     >

Hello agent jest teraz zainstalowany i komputera jest zarejestrowaną toohello magazynu. Wszystko gotowe tooconfigure i Planowanie tworzenia kopii zapasowej.

## <a name="back-up-windows-server-system-state-preview"></a>Wykonaj kopię zapasową stanu systemu Windows Server (wersja zapoznawcza)
Witaj początkowa kopia zapasowa obejmuje trzy zadania:

* Włącz kopii zapasowej stanu systemu przy użyciu hello agenta usługi Kopia zapasowa Azure
* Witaj harmonogram tworzenia kopii zapasowych
* Tworzenie kopii zapasowej plików i folderów na powitania po raz pierwszy

toocomplete hello początkowa kopia zapasowa, agent usług odzyskiwania Microsoft Azure hello użycia.

### <a name="tooenable-system-state-backup-using-hello-azure-backup-agent"></a>tooenable kopii zapasowej stanu systemu przy użyciu hello agenta usługi Kopia zapasowa Azure

1. W sesji programu PowerShell Uruchom hello następujące polecenia toostop hello kopia zapasowa Azure aparatu.

  ```
  PS C:\> Net stop obengine
  ```

2. Otwórz hello rejestru systemu Windows.

  ```
  PS C:\> regedit.exe
  ```

3. Dodaj następującego klucza rejestru o hello hello określona wartość typu DWord.

  | Ścieżka rejestru | Klucz rejestru | Wartość DWord |
  |---------------|--------------|-------------|
  | HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider | TurnOffSSBFeature | 2 |

4. Uruchom ponownie Aparat kopii zapasowej hello, wykonując następujące polecenie w wierszu polecenia z pełnymi uprawnieniami hello.

  ```
  PS C:\> Net start obengine
  ```

### <a name="tooschedule-hello-backup-job"></a>zadanie tworzenia kopii zapasowej hello tooschedule

1. Otwórz agenta usług odzyskiwania Microsoft Azure hello. Aby go znaleźć, wyszukaj na maszynie łańcuch **Microsoft Azure Backup**.

    ![Uruchamianie agenta usług odzyskiwania Azure hello](./media/backup-try-azure-backup-in-10-mins/snap-in-search.png)

2. W agencie usług odzyskiwania hello, kliknij przycisk **harmonogram tworzenia kopii zapasowych**.

    ![Planowanie tworzenia kopii zapasowej systemu Windows Server](./media/backup-try-azure-backup-in-10-mins/schedule-first-backup.png)

3. Na powitania wprowadzenie strony hello Kreatora harmonogramu kopii zapasowej, kliknij przycisk **dalej**.

4. Na stronie tooBackup wybierz elementy powitania kliknij **Dodaj elementy**.

5. Wybierz **stanu systemu** , a następnie kliknij przycisk **OK**.

6. Kliknij przycisk **Dalej**.

7. Witaj harmonogramu kopii zapasowej stanu systemu i przechowywania zostanie automatycznie ustawione tooback się każdą niedzielę o 21:00:00 czasu lokalnego, i okresu przechowywania hello jest ustawiony too60 dni.

   > [!NOTE]
   > Automatycznie skonfigurowano zasad przechowywania i kopii zapasowych stanu systemu. Po utworzeniu kopii zapasowej plików i folderów oprócz toohello systemu Windows Server System stanu, określ tylko hello kopii zapasowej i przechowywania zasady kopii zapasowych pliku z hello kreatora. 
   >

8. Na stronie potwierdzenia hello, przejrzyj informacje hello, a następnie kliknij przycisk **Zakończ**.

9. Po zakończeniu pracy Kreatora hello tworzenie hello harmonogram tworzenia kopii zapasowych, kliknij przycisk **Zamknij**.

### <a name="tooback-up-windows-server-system-state-for-hello-first-time"></a>tooback zapasowa stanu systemu Windows Server dla powitania po raz pierwszy

1. Upewnij się, że nie ma żadnych oczekujących aktualizacji dla systemu Windows Server, które wymagają ponownego uruchomienia.

2. W agencie usług odzyskiwania hello, kliknij przycisk **wykonaj kopię zapasową teraz** hello toocomplete początkowe umieszczanie za pośrednictwem sieci hello.

    ![Natychmiastowe tworzenie kopii zapasowej systemu Windows Server](./media/backup-try-azure-backup-in-10-mins/backup-now.png)

3. Na stronie potwierdzenia hello Przejrzyj hello ustawień, które Witaj ponownie teraz Kreatora konfigurowania użyje tooback hello maszyny. Następnie kliknij pozycję **Utwórz kopię zapasową**.

4. Kliknij przycisk **Zamknij** tooclose hello kreatora. Jeśli zamkniesz Kreatora hello przed zakończeniem procesu tworzenia kopii zapasowej hello, Kreator hello nadal toorun w tle hello.

5. Po utworzeniu kopii zapasowej plików i folderów na serwerze, także stan systemu serwera Windows toohello, kreator Utwórz kopię zapasową teraz hello tylko wykona kopię zapasową plików. tooperform ad hoc stanu systemu wykonaj kopię zapasową, użyj następującego polecenia programu PowerShell hello:

    ```
    PS C:\> Start-OBSystemStateBackup
    ```

  Po zakończeniu tworzenia początkowej kopii zapasowej hello hello **zadanie zostało ukończone** stan zostanie wyświetlony w konsoli usługi Backup hello.

  ![Początkowa replikacja została zakończona](./media/backup-try-azure-backup-in-10-mins/ircomplete.png)

## <a name="frequently-asked-questions"></a>Często zadawane pytania

Witaj następujące pytania i odpowiedzi zawierają dodatkowe informacje.

### <a name="what-is-hello-staging-volume"></a>Co to jest hello przemieszczania woluminu?

Witaj woluminu przemieszczania reprezentuje lokalizację pośrednich hello gdzie hello natywnie dostępna kopia zapasowa systemu Windows Server przygotuje hello kopii zapasowej stanu systemu. Agent usługi Kopia zapasowa Azure, a następnie kompresuje i szyfruje pośredniego kopia zapasowa i wysyła on za pośrednictwem bezpiecznego protokołu HTTPS toohello skonfigurowany magazyn usług odzyskiwania. **Stanowczo zaleca się, że ustanowić hello woluminu tymczasowe na woluminie z systemem innym niż systemu Windows. Jeśli zauważysz problemy z kopii zapasowych stanu systemu Sprawdzanie lokalizacji hello woluminu przemieszczania jest hello pierwszy krok rozwiązywania problemów.** 

### <a name="how-can-i-change-hello-staging-volume-path-specified-in-hello-azure-backup-agent"></a>Jak zmienić hello przemieszczania woluminu ścieżce określonej w hello agenta usługi Kopia zapasowa Azure?

Witaj woluminu przemieszczania znajduje się w folderu pamięci podręcznej hello domyślnie. 

1. toochange tej lokalizacji hello Użyj następującego polecenia (w wierszu polecenia z podwyższonym poziomem uprawnień):
  ```
  PS C:\> Net stop obengine
  ```

2. Następnie zaktualizuj hello następujące wpisy rejestru z hello ścieżki toohello nowego woluminu przemieszczania folderu.

  |Ścieżka rejestru|Klucz rejestru|Wartość|
  |-------------|------------|-----|
  |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider | SSBStagingPath | Nowa lokalizacja woluminu przemieszczania |

Hello ścieżki tymczasowej jest rozróżniana wielkość liter i muszą być dokładnie odpowiadać tej samej hello jej co istnieje na serwerze hello. 

3. Po zmianie ścieżki woluminu przemieszczania hello ponownego uruchomienia aparatu kopii zapasowej hello:
  ```
  PS C:\> Net start obengine
  ```
4. toopick hello zmieniona ścieżka, hello Otwórz agenta usług odzyskiwania Microsoft Azure i wyzwalacza ad hoc kopii zapasowej stanu systemu.

### <a name="why-is-hello-system-state-default-retention-set-too60-days"></a>Dlaczego jest stan systemu hello przechowywania domyślne ustawić dni too60?

Witaj użytkowania kopii zapasowej stanu systemu jest hello taki sam jak ustawienie hello "okresu istnienia reliktu" hello roli usługi Active Directory systemu Windows Server. Wartość domyślna Hello wpis okresu istnienia reliktu hello wynosi 60 dni. Tę wartość można ustawić dla obiektu konfiguracji usługi Directory (NTDS) hello.

### <a name="how-do-i-change-hello-default-backup-and-retention-policy-for-system-state"></a>Jak zmienić domyślne hello kopii zapasowej i zasad przechowywania dla stanu systemu?

domyślne hello toochange kopii zapasowej i zasad przechowywania dla stanu systemu:
1. Zatrzymaj hello Aparat kopii zapasowej. Uruchom następujące polecenie w wierszu polecenia z podwyższonym poziomem uprawnień, hello.

  ```
  PS C:\> Net stop obengine
  ```

2. Dodaj lub zaktualizuj hello następujące wpisy klucza rejestru HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider.

  |Nazwa rejestru|Opis|Wartość|
  |-------------|-----------|-----|
  |SSBScheduleTime|Używane tooconfigure hello hello kopii zapasowej. Domyślna to 21: 00 czasu lokalnego.|DWord: Format hh: mm (dziesiętna) na przykład 2130 dla 21:30:00 czasu lokalnego|
  |SSBScheduleDays|Dni hello tooconfigure używane podczas tworzenia kopii zapasowej stanu systemu należy przeprowadzić na powitania określony czas. Poszczególnych cyfr określ dni tygodnia hello. 0 oznacza niedzielę, 1 oznacza poniedziałek, i tak dalej. Dzień domyślny dla kopii zapasowej oznacza niedzielę.|DWord: dni hello tygodnia toorun tworzenia kopii zapasowej (dziesiętna), na przykład 1230 harmonogramy tworzenia kopii zapasowych w poniedziałek, Wtorek, środę i niedzielę.|
  |SSBRetentionDays|Używane tooconfigure hello dni tooretain kopii zapasowej. Wartość domyślna to 60. Maksymalna dozwolona wartość to 180.|DWord: Dni tooretain kopii zapasowej (dziesiętne).|

3. Hello Użyj następującego polecenia toorestart hello kopii zapasowej aparatu.
    ```
    PS C:\> Net start obengine
    ```

4. Otwórz agenta usług odzyskiwania Microsoft hello.

5. Kliknij przycisk **harmonogram tworzenia kopii zapasowych** , a następnie kliknij przycisk **dalej** do momentu wyświetlenia hello zmiany zostaną uwzględnione.

6. Kliknij przycisk **Zakończ** tooapply hello zmiany.


## <a name="questions"></a>Pytania?
Jeśli masz pytania lub w przypadku dowolnej funkcji, które chcesz toosee uwzględnione, [Prześlij nam opinię](http://aka.ms/azurebackup_feedback).

## <a name="next-steps"></a>Następne kroki
* Dowiedz się więcej o [tworzeniu kopii zapasowej maszyn z systemem Windows](backup-configure-vault.md).
* Teraz, gdy utworzono kopię zapasową plików i folderów, możesz [zarządzać swoimi magazynami i serwerami](backup-azure-manage-windows-server.md).
* Toorestore kopii zapasowej, należy użyć w tym artykule zbyt[przywrócenia plików tooa systemu Windows maszyny](backup-azure-restore-windows-server.md).
