---
title: "tooback DPM aaaUse zapasową obciążeń tooAzure portal | Dokumentacja firmy Microsoft"
description: "Wprowadzenie toobacking zapasową serwerów DPM przy użyciu usługi Kopia zapasowa Azure hello"
services: backup
documentationcenter: 
author: adigan
manager: nkolli
editor: 
keywords: System Center Data Protection Manager, programu data protection manager, kopii zapasowych programu dpm
ms.assetid: c8c322cf-f5eb-422c-a34c-04a4801bfec7
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: adigan;giridham;jimpark;markgal;trinadhk
ms.openlocfilehash: 1dd988ae55012ac7dc485d2416458542c60b6ae3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="preparing-tooback-up-workloads-tooazure-with-dpm"></a>Przygotowywanie tooback się tooAzure obciążenia za pomocą programu DPM
> [!div class="op_single_selector"]
> * [Azure Backup Server](backup-azure-microsoft-azure-backup.md)
> * [SCDPM](backup-azure-dpm-introduction.md)
> * [Serwer kopii zapasowej systemu Azure (klasyczne)](backup-azure-microsoft-azure-backup-classic.md)
> * [SCDPM (klasyczne)](backup-azure-dpm-introduction-classic.md)
>
>

Ten artykuł zawiera wprowadzenie toousing kopia zapasowa Microsoft Azure tooprotect System Center Data Protection Manager (DPM) serwerów i obciążeń. Przeczytaj go, będzie zrozumieć:

* Jak działa kopii zapasowej serwera Azure DPM
* Witaj wymagania wstępne tooachieve smooth środowisko tworzenia kopii zapasowej
* Witaj typowych błędów napotkanych i w jaki sposób toodeal z nimi
* Obsługiwane scenariusze

> [!NOTE]
> Platforma Azure ma dwa modele wdrażania związane z tworzeniem i pracą z zasobami: [Resource Manager i Model Klasyczny](../azure-resource-manager/resource-manager-deployment-model.md). Ten artykuł zawiera hello informacje i procedury dotyczące przywracania maszyn wirtualnych wdrożonych przy użyciu hello modelu Resource Manager.
>
>

System Center DPM tworzy kopie zapasowe danych plików i aplikacji. TooDPM kopię zapasową danych można przechowywane na taśmie na dysku, lub kopię zapasową tooAzure w usłudze Kopia zapasowa Microsoft Azure. Program DPM współdziała z usługi Kopia zapasowa Azure w następujący sposób:

* **Program DPM wdrożony jako fizycznego serwera lub lokalnej maszyny wirtualnej** — Jeśli program DPM wdrożony jako serwera fizycznego lub lokalnej maszyny wirtualnej funkcji Hyper-V można tworzyć kopie zapasowe danych tooa usług odzyskiwania magazynu poza toodisk i tworzenia kopii zapasowej na taśmie.
* **Program DPM wdrożony jako maszyna wirtualna platformy Azure** — z programu System Center 2012 R2 z aktualizacją Update 3 programu DPM można wdrożyć jako maszynę wirtualną platformy Azure. Program DPM wdrożony jako maszyna wirtualna platformy Azure, które można wykonać kopię zapasową danych tooAzure dołączone dyski maszyny wirtualnej platformy Azure programu DPM toohello, czy można odciążyć magazyn danych hello dzięki tworzeniu kopii zapasowej tooa, które Magazyn usług odzyskiwania.

## <a name="why-backup-from-dpm-tooazure"></a>Dlaczego kopii zapasowej z programu DPM tooAzure?
korzyści biznesowe Hello przy użyciu usługi Kopia zapasowa Azure do wykonywania kopii zapasowych serwerów programu DPM obejmują:

* Lokalnego wdrożenia programu DPM Azure służy jako alternatywne termin toolong tootape wdrożenia.
* Dla wdrożeń programu DPM na platformie Azure kopia zapasowa Azure umożliwia toooffload magazynu z hello dysku platformy Azure, umożliwiając tooscale się starsze dane są przechowywane w magazynie usług odzyskiwania i nowych danych na dysku.

## <a name="prerequisites"></a>Wymagania wstępne
Przygotuj tooback kopia zapasowa Azure zapasowej danych programu DPM w następujący sposób:

1. **Tworzenie magazynu usług odzyskiwania** — Tworzenie magazynu w portalu Azure.
2. **Pobierz poświadczenia magazynu** — Pobierz hello poświadczenia, które używają tooregister hello programu DPM serwera tooRecovery magazyn usług.
3. **Zainstaluj hello Azure Backup Agent** — z usługi Kopia zapasowa Azure, zainstaluj agenta hello na każdym serwerze DPM.
4. **Zarejestruj serwer hello** — magazyn usług tooRecovery serwera programu DPM hello rejestru.

### <a name="1-create-a-recovery-services-vault"></a>1. Tworzenie magazynu usługi Recovery Services
toocreate odzyskiwania usług magazynu:

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com/).
2. W menu Centrum powitania kliknij **Przeglądaj** i hello listy zasobów, wpisz **usług odzyskiwania**. Po rozpoczęciu wpisywania, spowoduje odfiltrowanie listy hello oparte na dane wejściowe. Kliknij opcję **Magazyn Usług odzyskiwania**.

    ![Tworzenie magazynu usługi Recovery Services — krok 1](./media/backup-azure-dpm-introduction/open-recovery-services-vault.png)

    zostanie wyświetlona lista Hello Magazyny usług odzyskiwania.
3. Na powitania **Magazyny usług odzyskiwania** menu, kliknij przycisk **Dodaj**.

    ![Tworzenie magazynu Usług odzyskiwania — krok 2](./media/backup-azure-dpm-introduction/rs-vault-menu.png)

    Usługi odzyskiwania Hello zostanie otwarty blok magazyn monitem tooprovide **nazwa**, **subskrypcji**, **grupy zasobów**, i **lokalizacji**.

    ![Tworzenie magazynu Usług odzyskiwania — krok 5](./media/backup-azure-dpm-introduction/rs-vault-attributes.png)
4. Aby uzyskać **nazwa**, wprowadź przyjazną nazwę tooidentify hello magazynu. Nazwa Hello musi toobe unikatowy dla hello subskrypcji platformy Azure. Wpisz nazwę o długości od 2 do 50 znaków. Musi ona rozpoczynać się od litery i może zawierać tylko litery, cyfry i łączniki.
5. Kliknij przycisk **subskrypcji** toosee hello listę dostępnych subskrypcji. Jeśli nie masz pewności, który toouse subskrypcji, użyj domyślnej hello (lub sugerowane) subskrypcji. Większa liczba opcji do wyboru będzie dostępna tylko w przypadku, gdy konto organizacji jest skojarzone z wieloma subskrypcjami platformy Azure.
6. Kliknij przycisk **grupy zasobów** toosee hello listę dostępnych grup zasobów, lub kliknij przycisk **nowy** toocreate nową grupę zasobów. Pełne informacje na temat grup zasobów można znaleźć w temacie [Omówienie usługi Azure Resource Manager](../azure-resource-manager/resource-group-overview.md)
7. Kliknij przycisk **lokalizacji** tooselect hello region geograficzny magazynu hello.
8. Kliknij przycisk **Utwórz**. Może upłynąć trochę czasu zanim hello toobe utworzony magazyn usług odzyskiwania. Monitoruje powiadomienia o stanie hello hello górnym obszarze po prawej stronie w portalu hello.
   Po utworzeniu magazynu zostanie otwarty w portalu hello.

### <a name="set-storage-replication"></a>Konfigurowanie replikacji magazynu
opcji replikacji magazynu Hello umożliwia toochoose między magazynu geograficznie nadmiarowego i lokalnie nadmiarowego magazynu. Domyślnie magazyn jest nadmiarowy geograficznie. Pozostaw hello opcji set toogeo nadmiarowego magazynu, jeśli jest to Twoja podstawowa kopia zapasowa. Wybierz magazyn lokalnie nadmiarowy, jeśli chcesz skorzystać z tańszej, ale mniej trwałej opcji. Przeczytaj więcej na temat [geograficznie nadmiarowego](../storage/common/storage-redundancy.md#geo-redundant-storage) i [magazyn lokalnie nadmiarowy](../storage/common/storage-redundancy.md#locally-redundant-storage) opcje magazynu w hello [Omówienie replikacji usługi Azure Storage](../storage/common/storage-redundancy.md).

ustawienia replikacji magazynu hello tooedit:

1. Wybierz magazyn tooopen hello magazynu w pulpicie nawigacyjnym i hello bloku ustawienia. Jeśli hello **ustawienia** nie otwarcie bloku, kliknij przycisk **wszystkie ustawienia** hello magazynu w pulpicie nawigacyjnym.
2. Na powitania **ustawienia** bloku, kliknij przycisk **infrastruktura kopii zapasowej** > **konfiguracji kopii zapasowej** tooopen hello **konfiguracji kopii zapasowej** bloku. Na powitania **konfiguracji kopii zapasowej** bloku, wybierz hello opcji replikacji magazynu dla magazynu.

    ![Lista magazynów kopii zapasowych](./media/backup-azure-vms-first-look-arm/choose-storage-configuration-rs-vault.png)

    Po wybraniu opcji magazynu powitania dla magazynu, wszystko jest gotowe tooassociate hello maszyn wirtualnych z magazynem hello. toobegin hello skojarzenia, należy odnaleźć i zarejestrować hello maszyn wirtualnych platformy Azure.

### <a name="2-download-vault-credentials"></a>2. Pobieranie poświadczeń magazynu
Plik poświadczeń magazynu Hello jest certyfikatem generowane przez portal powitania dla każdego magazynu kopii zapasowych. Hello portal przekazuje następnie hello toohello klucza publicznego usługi kontroli dostępu (ACS). Hello klucza prywatnego certyfikatu hello stają się dostępne toohello użytkownika jako część przepływu pracy hello, które jest podawana jako dane wejściowe w hello maszyny rejestracji w przepływie pracy. To jest uwierzytelniany hello maszyny toosend dane kopii zapasowej tooan zidentyfikowane magazynu w hello usługi Kopia zapasowa Azure.

poświadczenia magazynu Hello jest używany tylko podczas rejestracji hello w przepływie pracy. Jest tooensure odpowiedzialność hello użytkownika, który hello pliku nie zostaną ujawnione poświadczenia magazynu. Jeśli znajduje się w ręce hello dowolny złośliwy użytkownik, plik poświadczeń magazynu hello może być używane tooregister inne maszyny przed hello tego samego magazynu. Jednak ponieważ hello dane kopii zapasowej jest zaszyfrowany przy użyciu hasła, który należy toohello klienta, dane kopii zapasowej nie zostaną ujawnione. toomitigate tego problemu, poświadczenia magazynu ustawiono tooexpire w 48hrs. Możesz pobrać hello poświadczenia magazynu usług odzyskiwania dowolną liczbę razy —, ale podczas przepływu pracy rejestracji hello dotyczy tylko hello najnowszy plik poświadczeń magazynu.

Plik poświadczeń magazynu Hello jest pobierana za pośrednictwem bezpiecznego kanału z hello portalu Azure. Witaj usługi Azure Backup nie rozpoznaje hello klucza prywatnego certyfikatu hello i w portalu hello lub usługi hello hello klucz prywatny nie jest trwały. Użyj hello następujące kroki toodownload hello magazynu poświadczeń pliku tooa komputera lokalnego.

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com/).
2. Otwórz usług odzyskiwania magazynu toowhich toowhich ma tooregister maszyny DPM.
3. Blok ustawień jest otwierany domyślnie. Jeśli jest zamknięty, kliknij polecenie **ustawienia** w bloku ustawień hello tooopen pulpitu nawigacyjnego magazynu. W bloku ustawienia, kliknij polecenie **właściwości**.

    ![Otwarcie bloku magazynu](./media/backup-azure-dpm-introduction/vault-settings-dpm.png)
4. Na stronie właściwości powitania kliknij **Pobierz** w obszarze **kopię zapasową poświadczeń**. Hello portal generuje plik poświadczeń magazynu hello, który ma zostać udostępnione do pobrania.

    ![Do pobrania](./media/backup-azure-dpm-introduction/vault-credentials.png)

Hello portal wygeneruje poświadczenie magazynu przy użyciu kombinacji nazwy magazynu hello i hello bieżącą datę. Kliknij przycisk **zapisać** toodownload hello magazynu poświadczeń toohello lokalnego konta pobiera folderu lub wybierz Zapisz jako z hello zapisać menu toospecify lokalizację hello poświadczenia magazynu. Zajmuje minutę tooa toobe pliku hello wygenerowany.

### <a name="note"></a>Uwaga
* Upewnij się, że ten plik poświadczeń magazynu hello jest zapisywany w lokalizacji, w których może uzyskać dostęp z komputera. Jeśli jest on przechowywany w udziale plików/SMB, sprawdź, czy uprawnienia dostępu hello.
* Plik poświadczeń magazynu Hello jest używany tylko podczas rejestracji hello w przepływie pracy.
* Plik poświadczeń magazynu Hello wygasa po 48hrs i może zostać pobrany z portalu hello.

### <a name="3-install-backup-agent"></a>3. Zainstaluj agenta kopii zapasowej
Po utworzeniu magazynu usługi Kopia zapasowa Azure hello, powinien być zainstalowany agent na wszystkich maszynach systemu Windows (Windows Server, klienta systemu Windows, serwer System Center Data Protection Manager lub serwer kopii zapasowej Azure machine), które umożliwia wykonywanie kopii zapasowych danych i aplikacji tooAzure.

1. Otwórz usług odzyskiwania magazynu toowhich toowhich ma tooregister maszyny DPM.
2. Blok ustawień jest otwierany domyślnie. Jeśli jest zamknięty, kliknij polecenie **ustawienia** tooopen hello ustawienia bloku. W bloku ustawienia, kliknij polecenie **właściwości**.

    ![Otwarcie bloku magazynu](./media/backup-azure-dpm-introduction/vault-settings-dpm.png)
3. Na stronie Ustawienia powitania kliknij **Pobierz** w obszarze **Agent usługi Kopia zapasowa Azure**.

    ![Do pobrania](./media/backup-azure-dpm-introduction/azure-backup-agent.png)

   Pobrany hello agenta, kliknij dwukrotnie MARSAgentInstaller.exe toolaunch hello instalacji agenta usługi Kopia zapasowa Azure hello. Wybierz folder instalacji hello i pliki tymczasowe folderu wymagane dla hello agenta. Określona lokalizacja pamięci podręcznej Hello musi mieć wolnego miejsca, czyli co najmniej 5% hello dane kopii zapasowej.
4. Jeśli używasz toohello tooconnect serwera proxy internet w hello **konfiguracji serwera Proxy** ekranu, wprowadź szczegóły serwera proxy hello. Jeśli korzystasz z uwierzytelnionego serwera proxy, wprowadź szczegóły nazwy i hasła użytkownika hello na tym ekranie.
5. agent usługi Kopia zapasowa Azure Hello instaluje .NET Framework 4.5 i programu Windows PowerShell (Jeśli nie jest dostępna) toocomplete hello instalację.
6. Po zainstalowaniu agenta hello **Zamknij** hello okna.

   ![Zamknij](../../includes/media/backup-install-agent/dpm_FinishInstallation.png)
7. zbyt**hello rejestrowania serwera DPM** toohello magazynu, w hello **zarządzania** karcie, kliknij na **Online**. Następnie wybierz opcję **zarejestrować**. Zostanie otwarty hello zarejestrować Kreatora instalacji.
8. Jeśli używasz toohello tooconnect serwera proxy internet w hello **konfiguracji serwera Proxy** ekranu, wprowadź szczegóły serwera proxy hello. Jeśli korzystasz z uwierzytelnionego serwera proxy, wprowadź szczegóły nazwy i hasła użytkownika hello na tym ekranie.

    ![Konfiguracja serwera proxy](../../includes/media/backup-install-agent/DPM_SetupOnlineBackup_Proxy.png)
9. Na ekranie poświadczenia magazynu hello Przeglądaj plik poświadczeń magazynu wybierz hello tooand, który został wcześniej pobrany.

    ![Poświadczenia magazynu](../../includes/media/backup-install-agent/DPM_SetupOnlineBackup_Credentials.jpg)

    Plik poświadczeń magazynu Hello jest prawidłowa tylko dla 48 godzin (po jej pobraniu, z portalu hello). W razie wystąpienia błędu w tym ekranu (na przykład "Wygasła udostępniony plik poświadczeń magazynu"), toohello logowania Azure portal i pobrać hello plik poświadczeń magazynu ponownie.

    Upewnij się, że ten plik poświadczeń magazynu hello jest dostępna w lokalizacji, którą można uzyskać, sprawdzając hello instalacji aplikacji. Jeśli wystąpią błędy powiązane, poświadczenia magazynu hello kopii pliku tooa lokalizacji tymczasowej na tej maszynie i ponów próbę wykonania operacji hello.

    Jeśli wystąpi błąd poświadczeń nieprawidłowy magazynu (na przykład "magazynu nieprawidłowe poświadczenia podane") hello plik jest uszkodzony lub nie ma hello najnowszych poświadczeń skojarzonych z usługą odzyskiwania hello. Ponów operację powitania po pobraniu nowego pliku poświadczeń magazynu z portalu hello. Ten błąd zazwyczaj występuje Jeśli hello użytkownik kliknie hello **poświadczenia magazynu pobierania** opcję hello portalu Azure, szybkie naciśnięcie. W takim przypadku tylko hello drugi plik poświadczeń magazynu jest nieprawidłowa.
10. toocontrol hello wykorzystanie przepustowości sieci podczas pracy oraz godzin nieroboczych w hello **ustawienia ograniczania** ekranu, można ustawić limity użycia przepustowości hello i zdefiniuj hello pracy oraz innych niż godziny pracy.

    ![Ustawienie ograniczenia przepustowości](../../includes/media/backup-install-agent/DPM_SetupOnlineBackup_Throttling.png)
11. W hello **ustawienia folderu odzyskiwania** ekranu, przejdź do folderu hello gdzie hello pliki pobierane z usługi Azure zostanie przemieszczony tymczasowo.

    ![Ustawienia folderu odzyskiwania](../../includes/media/backup-install-agent/DPM_SetupOnlineBackup_RecoveryFolder.png)
12. W hello **ustawienie szyfrowania** ekranu, można wygenerować hasło lub podać hasło (co najmniej 16 znaków). Należy pamiętać, toosave hello hasła w bezpiecznym miejscu.

    ![Szyfrowanie](../../includes/media/backup-install-agent/DPM_SetupOnlineBackup_Encryption.png)

    > [!WARNING]
    > Jeśli hello zgubienia lub zapomnienia hasła; Microsoft nie może pomóc w odzyskiwaniu danych kopii zapasowej hello. użytkownik końcowy Hello jest właścicielem hello hasło szyfrowania i Microsoft nie ma wgląd w hello hasło używane przez użytkownika końcowego hello. Zapisz plik hello w bezpiecznej lokalizacji, zgodnie z wymaganiami podczas operacji odzyskiwania.
    >
    >
13. Po kliknięciu hello **zarejestrować** przycisku, hello maszyna zarejestrowana pomyślnie toohello magazynu i są teraz gotowe toostart tworzenie kopii zapasowej tooMicrosoft Azure.
14. Podczas korzystania z programu Data Protection Manager, można zmodyfikować ustawienia hello określony podczas przepływu pracy rejestracji hello klikając hello **Konfiguruj** opcję, wybierając **Online** w obszarze hello  **Zarządzanie** kartę.

## <a name="requirements-and-limitations"></a>Wymagania (i ograniczenia)
* Program DPM może działać jako serwer fizyczny lub maszyny wirtualnej funkcji Hyper-V zainstalowanych w programie System Center 2012 SP1 lub System Center 2012 R2. Mogą również działać jako maszyna wirtualna platformy Azure z programu System Center 2012 R2 z co najmniej programu DPM 2012 R2 Update Rollup 3 lub maszyny wirtualnej systemu Windows w środowisku programu VMWare na nim uruchomione w programie System Center 2012 R2 z pakietem zbiorczym aktualizacji 5.
* Jeśli używasz programu DPM z programu System Center 2012 z dodatkiem SP1 należy zainstalować aktualizacji Przywróć zapasowej 2 dla programu System Center Data Protection Manager z dodatkiem SP1. Jest to wymagane, aby można było zainstalować hello Azure Backup Agent.
* Serwer programu DPM Hello powinien mieć programu Windows PowerShell i .net Framework 4.5 zainstalowane.
* Program DPM można utworzyć kopię zapasową większości obciążeń tooAzure kopii zapasowej. Pełną listę, co ma obsługiwane Zobacz hello kopia zapasowa Azure obsługuje poniższe elementy.
* Nie można odzyskać danych przechowywanych w usłudze Kopia zapasowa Azure z opcją "Kopiuj tootape" hello.
* Konieczne będzie konto platformy Azure z włączoną funkcją kopia zapasowa Azure hello. Jeśli go nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut. Przeczytaj informacje o [cennikiem usługi Kopia zapasowa Azure](https://azure.microsoft.com/pricing/details/backup/).
* Za pomocą usługi Kopia zapasowa Azure wymaga hello Azure Backup Agent toobe zainstalowanych na serwerach hello, który ma tooback w górę. Każdy serwer musi mieć co najmniej 5% hello rozmiar danych hello, która jest tworzona kopia zapasowa, dostępne jako wolnego miejsca w magazynie lokalnym. Na przykład tworzenie kopii zapasowej 100 GB danych wymaga co najmniej 5 GB wolnego miejsca w lokalizacji pliki tymczasowe hello.
* Dane będą przechowywane w hello magazynu magazynu Azure. Nie ma limit nie toohello ilość danych, które można tworzyć kopie zapasowe tooan magazynu usługi Kopia zapasowa Azure, ale rozmiar hello źródła danych (na przykład maszyny wirtualnej lub bazy danych) nie powinna przekraczać 54400 GB.

Kopia zapasowa tooAzure obsługuje następujące typy plików:

* Zaszyfrowane (tylko pełne kopie zapasowe)
* Skompresowane (obsługą przyrostowych kopii zapasowych)
* Rozrzedzone (obsługą przyrostowych kopii zapasowych)
* Skompresowane i rozrzedzone (traktowane jako rozrzedzone)

I te nie są obsługiwane:

* Serwery w systemach plików z uwzględnieniem wielkości liter nie są obsługiwane.
* Twarde linki (pomijane)
* (Pomijane) punkty ponownej analizy
* Zaszyfrowane i skompresowane (pomijane)
* Zaszyfrowane i rozrzedzone (pomijane)
* Skompresowany strumień
* Rozrzedzony strumień

> [!NOTE]
> Od w System Center 2012 DPM z dodatkiem SP1 lub nowszym można tworzyć kopie zapasowe dużych obciążeń chronionych przez tooAzure programu DPM za pomocą usługi Microsoft Azure Backup.
>
>
