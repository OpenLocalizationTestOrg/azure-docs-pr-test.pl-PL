---
title: "tooback agenta usługi Kopia zapasowa Azure aaaUse zapasowe plików i folderów | Dokumentacja firmy Microsoft"
description: "Użyj tooback agenta usługi Kopia zapasowa Microsoft Azure hello się tooAzure plików i folderów systemu Windows. Tworzenie magazynu usług odzyskiwania, zainstalować agenta kopii zapasowej hello Definiowanie zasad tworzenia kopii zapasowej hello i uruchomić hello początkowa kopia zapasowa na powitania pliki i foldery."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: Magazyn kopii zapasowych; Tworzenie kopii zapasowej systemu Windows server; Kopia zapasowa systemu windows;
ms.assetid: 7f5b1943-b3c1-4ddb-8fb7-3560533c68d5
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/15/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: be203c24841971872b5c6e7cf260a2fa5c58ac47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-a-windows-server-or-client-tooazure-using-hello-resource-manager-deployment-model"></a>Tworzenie kopii zapasowej systemu Windows Server lub klienta tooAzure, przy użyciu modelu wdrażania usługi Resource Manager hello
> [!div class="op_single_selector"]
> * [Witryna Azure Portal](backup-configure-vault.md)
> * [Portal klasyczny](backup-configure-vault-classic.md)
>
>

W tym artykule opisano, jak pliki i foldery tooAzure tooback systemu Windows Server (lub klienta systemu Windows) z usługi Kopia zapasowa Azure przy użyciu hello modelu wdrażania usługi Resource Manager.

[!INCLUDE [learn-about-deployment-models](../../includes/backup-deployment-models.md)]

![Kroki procesu tworzenia kopii zapasowej](./media/backup-configure-vault/initial-backup-process.png)

## <a name="before-you-start"></a>Przed rozpoczęciem
tooback serwera lub klienta tooAzure, potrzebne jest konto platformy Azure. Jeśli nie masz, możesz utworzyć [bezpłatne konto](https://azure.microsoft.com/free/) w zaledwie kilka minut.

## <a name="create-a-recovery-services-vault"></a>Tworzenie magazynu Usług odzyskiwania
Magazyn usług odzyskiwania jest jednostka, która przechowuje wszystkie hello kopie zapasowe i punkty odzyskiwania, tworzonych w czasie. Magazyn usług odzyskiwania Hello zawiera także hello zasad tworzenia kopii zapasowych stosowane toohello chronione pliki i foldery. Podczas tworzenia magazynu usług odzyskiwania należy również wybrać opcji nadmiarowość magazynu odpowiednie hello.

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

    * Wybierz **Utwórz nowy** Jeśli chcesz toocreate nową grupę zasobów.
    Lub
    * Wybierz **Użyj istniejącego** i kliknij przycisk hello menu rozwijanego toosee hello listę dostępnych grup zasobów.

  Aby uzyskać pełne informacje na temat grup zasobów, zobacz hello [Omówienie usługi Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).

7. Kliknij przycisk **lokalizacji** tooselect hello region geograficzny magazynu hello. Ten wybór Określa region geograficzny hello wysyłania danych kopii zapasowych.

8. U dołu hello blok magazyn usług odzyskiwania hello, kliknij przycisk **Utwórz**.

  Może upłynąć kilka minut hello toobe utworzony magazyn usług odzyskiwania. Monitor stanu hello powiadomienia w górnym obszarze po prawej stronie powitania hello portalu. Po utworzeniu magazynu zostanie wyświetlony hello listę magazynów usług odzyskiwania. Jeśli po kilku minutach nie widzisz swojego magazynu, kliknij pozycję **Odśwież**.

  ![Klikanie pozycji Odśwież](./media/backup-try-azure-backup-in-10-mins/refresh-button.png)</br>

  Przeanalizowanie magazynu na liście hello magazynów usług odzyskiwania jest nadmiarowość magazynu hello tooset gotowe.


### <a name="set-storage-redundancy"></a>Nadmiarowość magazynu zestawu
Podczas tworzenia magazynu usługi Recovery Services określany jest sposób replikowania magazynu.

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

Teraz, po utworzeniu magazynu, pobieranie i instalowanie agenta usług odzyskiwania Microsoft Azure hello, pobierając poświadczenia magazynu i przy użyciu tych poświadczeń tooregister hello agenta z przygotowanie tooback Twojego infrastruktury zapasowe plików i folderów Magazyn Hello.

## <a name="configure-hello-vault"></a>Konfigurowanie magazynu hello

1. Na hello bloku magazyn usług odzyskiwania (dla hello właśnie utworzony magazyn), w sekcji wprowadzenie hello, kliknij przycisk **kopii zapasowej**, następnie na powitania **wprowadzenie do korzystania z kopii zapasowej** bloku, wybierz  **Celem tworzenia kopii zapasowej**.

  ![Otwieranie bloku celu kopii zapasowej](./media/backup-try-azure-backup-in-10-mins/open-backup-settings.png)

  Witaj **cel kopii zapasowej** zostanie otwarty blok. Jeśli wcześniej skonfigurowano hello magazyn usług odzyskiwania i następnie hello **cel kopii zapasowej** kliknięcie powoduje otwarcie bloków **kopii zapasowej** na powitania usług odzyskiwania magazynu bloku.

  ![Otwieranie bloku celu kopii zapasowej](./media/backup-try-azure-backup-in-10-mins/backup-goal-blade.png)

2. Z hello **gdzie działa Twoje obciążenie?** menu rozwijanego wybierz **lokalnymi**.

  Pozycję **Lokalnie** trzeba wybrać, ponieważ Twój serwer lub komputer z systemem Windows jest maszyną fizyczną spoza platformy Azure.

3. Z hello **co chcesz toobackup?** menu, wybierz opcję **pliki i foldery**i kliknij przycisk **OK**.

  ![Konfigurowanie plików i folderów](./media/backup-try-azure-backup-in-10-mins/set-file-folder.png)

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
> Włączenie kopii zapasowej za pomocą portalu Azure hello nie jest jeszcze dostępna. Użyj tooback agenta usług odzyskiwania Microsoft Azure hello zapasową plików i folderów.
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

## <a name="network-and-connectivity-requirements"></a>Wymagania dotyczące sieci i łączności

Machine/serwera proxy został ograniczony dostęp do Internetu, upewnij się, że ustawienia zapory na komputerze hello/serwera proxy są hello tooallow skonfigurowane następujące adresy URL: <br>
    1. www.msftncsi.com
    2. *.Microsoft.com
    3. *.WindowsAzure.com
    4. *.microsoftonline.com
    5. *.windows.ne


## <a name="create-hello-backup-policy"></a>Tworzenie zasad tworzenia kopii zapasowej hello
Hello zasad tworzenia kopii zapasowej jest harmonogram hello, gdy punkty odzyskiwania są pobierane i hello czas hello punkty odzyskiwania zostaną zachowane. Przy użyciu zasad tworzenia kopii zapasowej hello kopia zapasowa Microsoft Azure agenta toocreate hello pliki i foldery.

### <a name="toocreate-a-backup-schedule"></a>toocreate harmonogram tworzenia kopii zapasowych
1. Otwórz hello agenta usługi Kopia zapasowa Microsoft Azure. Aby go znaleźć, wyszukaj na maszynie łańcuch **Microsoft Azure Backup**.

    ![Uruchamianie agenta usługi Kopia zapasowa Azure hello](./media/backup-configure-vault/snap-in-search.png)
2. W agencie kopii zapasowej hello **akcje** okienku, kliknij przycisk **harmonogram tworzenia kopii zapasowych** hello toolaunch Kreatora harmonogramu kopii zapasowej.

    ![Planowanie tworzenia kopii zapasowej systemu Windows Server](./media/backup-configure-vault/schedule-first-backup.png)

3. Na powitania **wprowadzenie** strony hello Kreatora harmonogramu kopii zapasowej, kliknij przycisk **dalej**.
4. Na powitania **tooBackup wybierz elementy** kliknij przycisk **Dodaj elementy**.

  zostanie otwarte okno dialogowe Wybieranie elementów Hello.

5. Wybierz hello pliki i foldery mają tooprotect, a następnie kliknij przycisk **OK**.
6. W hello **tooBackup wybierz elementy** kliknij przycisk **dalej**.
7. Na powitania **Określanie harmonogramu tworzenia kopii zapasowej** Określ harmonogram tworzenia kopii zapasowych hello i kliknij przycisk **dalej**.

    Można zaplanować tworzenie kopii zapasowych codziennie (maksymalnie trzy razy) lub co tydzień.

    ![Elementy związane z tworzeniem kopii zapasowej systemu Windows Server](./media/backup-configure-vault/specify-backup-schedule-close.png)

   > [!NOTE]
   > Aby uzyskać więcej informacji o sposobie toospecify hello harmonogram tworzenia kopii zapasowych, zobacz artykuł hello [tooreplace kopia zapasowa Azure użycie infrastruktury taśmy](backup-azure-backup-cloud-as-tape.md).
   >
   >

8. Na powitania **Wybieranie zasady przechowywania** , wybierz hello zasad przechowywania określonych powitania dla kopii zapasowej hello i kliknij przycisk **dalej**.

    zasady przechowywania Hello określa hello okres czasu, który hello kopia zapasowa jest przechowywana. Zamiast określać "wspólne zasady" dla wszystkich punktów kopii zapasowej, można określić różne zasady przechowywania na podstawie hello tworzenia kopii zapasowej. Można zmodyfikować toomeet zasady przechowywania codziennie, co tydzień, miesięcznych i rocznych hello potrzeb.
9. Na stronie Wybieranie typu początkowej kopii zapasowej hello wybierz typ początkowej kopii zapasowej hello. Pozostaw opcję hello **automatycznie przez sieć hello** zaznaczone, a następnie kliknij przycisk **dalej**.

    Można tworzyć kopie zapasowe automatycznie przez sieć hello, lub w trybie offline, można tworzyć kopie zapasowe. Witaj dalszej części tego artykułu opisano proces hello automatycznego tworzenia kopii zapasowych. Jeśli wolisz toodo kopię zapasową offline, przejrzyj artykuł hello [w trybie Offline kopii zapasowej przepływu pracy w usłudze Kopia zapasowa Azure](backup-azure-backup-import-export.md) Aby uzyskać dodatkowe informacje.
10. Na stronie potwierdzenia hello, przejrzyj informacje hello, a następnie kliknij przycisk **Zakończ**.
11. Po zakończeniu pracy Kreatora hello tworzenie hello harmonogram tworzenia kopii zapasowych, kliknij przycisk **Zamknij**.

### <a name="enable-network-throttling"></a>Włącz ograniczanie przepustowości sieci
agent usługi Kopia zapasowa Microsoft Azure Hello zapewnia ograniczanie przepustowości sieci. Ograniczanie kontrolek z wykorzystaniem przepustowości sieci podczas transferu danych. Ten formant może być przydatne, gdy konieczne tooback zapasową danych poza godzinami pracy, ale nie chcesz hello toointerfere procesu tworzenia kopii zapasowej z innych ruch internetowy. Ograniczanie stosuje tooback zapasowej i przywracanie działania.

> [!NOTE]
> Ograniczanie przepustowości sieci nie jest dostępne w systemu Windows Server 2008 R2 z dodatkiem SP1, Windows Server 2008 z dodatkiem SP2 lub Windows 7 (dodatków service pack). funkcji ograniczania sieci kopia zapasowa Azure Hello angażujący jakości usług (QoS) w systemie operacyjnym lokalne powitania. Jeśli kopia zapasowa Azure może chronić tych systemów operacyjnych, wersji hello QoS dostępne na tych platformach nie działa z ograniczanie przepustowości sieci usługi Kopia zapasowa Azure. Ograniczanie przepustowości sieci można używać na wszystkich innych [obsługiwanych systemów operacyjnych](backup-azure-backup-faq.md).
>
>

**Ograniczanie przepustowości sieci tooenable**

1. W agencie kopia zapasowa Microsoft Azure hello, kliknij przycisk **Zmień właściwości**.

    ![Zmień właściwości](./media/backup-configure-vault/change-properties.png)
2. Na powitania **ograniczania** kartę, zaznacz hello **włączyć użycia przepustowości połączenia internetowego do operacji tworzenia kopii zapasowej** pole wyboru.

    ![Ograniczanie przepustowości sieci](./media/backup-configure-vault/throttling-dialog.png)
3. Po włączeniu ograniczenia przepustowości, określ hello dozwolone przepustowości dla transferu danych kopii zapasowej podczas **godzin pracy** i **godziny wolne**.

    wartości przepustowości Hello rozpocząć 512 kilobitów na sekundę (KB/s) i można przejść w górę too1, 023 MB na sekundę (MB/s). Można również wyznaczyć hello rozpoczęcia i zakończenia **godzin pracy**, i dni tygodnia hello są uważane dniach. Godziny poza wyznaczonych są traktowane jako godzin pracy z systemem innym niż godziny pracy.
4. Kliknij przycisk **OK**.

### <a name="tooback-up-files-and-folders-for-hello-first-time"></a>tooback zapasowe plików i folderów na powitania po raz pierwszy
1. W hello agenta kopii zapasowej, kliknij przycisk **wykonaj kopię zapasową teraz** hello toocomplete początkowe umieszczanie za pośrednictwem sieci hello.

    ![Natychmiastowe tworzenie kopii zapasowej systemu Windows Server](./media/backup-configure-vault/backup-now.png)
2. Na stronie potwierdzenia hello Przejrzyj hello ustawień, które Witaj ponownie teraz Kreatora konfigurowania użyje tooback hello maszyny. Następnie kliknij pozycję **Utwórz kopię zapasową**.
3. Kliknij przycisk **Zamknij** tooclose hello kreatora. Jeśli zrobisz to przed zakończeniem procesu tworzenia kopii zapasowej hello, Kreator hello nadal toorun w tle hello.

Po zakończeniu tworzenia początkowej kopii zapasowej hello hello **zadanie zostało ukończone** stan zostanie wyświetlony w konsoli usługi Backup hello.

![Początkowa replikacja została zakończona](./media/backup-configure-vault/ircomplete.png)

## <a name="questions"></a>Pytania?
Jeśli masz pytania lub w przypadku dowolnej funkcji, które chcesz toosee uwzględnione, [Prześlij nam opinię](http://aka.ms/azurebackup_feedback).

## <a name="next-steps"></a>Następne kroki
Aby uzyskać dodatkowe informacje na temat tworzenia kopii zapasowych maszyn wirtualnych lub innych obciążeń zobacz:

* Teraz, gdy utworzono kopię zapasową plików i folderów, możesz [zarządzać swoimi magazynami i serwerami](backup-azure-manage-windows-server.md).
* Toorestore kopii zapasowej, należy użyć w tym artykule zbyt[przywrócenia plików tooa systemu Windows maszyny](backup-azure-restore-windows-server.md).
