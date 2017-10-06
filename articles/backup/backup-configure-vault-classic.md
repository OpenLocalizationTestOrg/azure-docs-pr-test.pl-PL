---
title: "aaaBack zapasową systemu Windows server lub stacji roboczej tooAzure (modelu klasycznego) | Dokumentacja firmy Microsoft"
description: "Kopia zapasowa systemu Windows serwery lub klientów tooa magazynu kopii zapasowych na platformie Azure. Za pomocą agenta usługi Kopia zapasowa Azure hello przejść przez podstawowe informacje dotyczące ochrony plików i folderów tooa magazyn kopii zapasowych."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: Magazyn kopii zapasowych; Tworzenie kopii zapasowej systemu Windows server; Kopia zapasowa systemu windows;
ms.assetid: 3b543bfd-8978-4f11-816a-0498fe14a8ba
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: c8f2a9bed1e5885f5c272c65b9282ededc05850a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-a-windows-server-or-workstation-tooazure-using-hello-classic-portal"></a>Tworzenie kopii zapasowej systemu Windows server lub stacji roboczej tooAzure przy użyciu klasycznego portalu hello
> [!div class="op_single_selector"]
> * [Portal klasyczny](backup-configure-vault-classic.md)
> * [Witryna Azure Portal](backup-configure-vault.md)
>
>

W tym artykule przedstawiono procedury hello muszą toofollow tooprepare środowiska, a następnie wykonaj kopię zapasową tooAzure systemu Windows server (lub stacji roboczej). Obejmuje ona również zagadnienia dotyczące wdrażania rozwiązania do tworzenia kopii zapasowej. Jeśli interesuje Cię w trakcie tworzenia kopii zapasowej Azure dla powitania po raz pierwszy, w tym artykule szybko przeprowadzi Cię przez proces hello.

Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: Resource Manager i model klasyczny. W tym artykule omówiono przy użyciu hello klasycznego modelu wdrażania. Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager.

## <a name="before-you-start"></a>Przed rozpoczęciem
tooback serwera lub klienta tooAzure, potrzebne jest konto platformy Azure. Jeśli nie masz, możesz utworzyć [bezpłatne konto](https://azure.microsoft.com/free/) w zaledwie kilka minut.

## <a name="create-a-backup-vault"></a>Tworzenie magazynu kopii zapasowych
tooback zapasowe plików i folderów z serwera lub klienta, należy toocreate magazynu kopii zapasowych w regionie geograficznym hello miejscu toostore hello danych.

> [!IMPORTANT]
> Uruchamianie 2017 marca, można dłużej korzystać magazyny kopii zapasowych w klasycznym portalu toocreate hello.
>
> Teraz można uaktualnić Twoje Magazyny usług tooRecovery magazynów kopii zapasowych. Aby uzyskać więcej informacji, zobacz artykuł hello [uaktualnienia tooa magazynu kopii zapasowej, Magazyn usług odzyskiwania i](backup-azure-upgrade-backup-to-recovery-services.md). Firma Microsoft zachęca tooupgrade Magazyny usług tooRecovery magazyny kopii zapasowych.<br/> **15 października 2017**, użytkownik nie będzie już magazyny kopii zapasowych toocreate PowerShell toouse stanie. <br/> **Od 1 listopada 2017 roku**:
>- Wszystkie pozostałe magazyny kopii zapasowych zostanie automatycznie uaktualniony tooRecovery Magazyny usług.
>- Użytkownik nie będzie możliwe tooaccess danych kopii zapasowych w portalu klasycznym hello. Zamiast tego użyj hello Azure tooaccess portalu tej kopii zapasowej w Magazyny usług odzyskiwania.
>


## <a name="download-hello-vault-credential-file"></a>Pobierz plik poświadczeń magazynu hello
Witaj na lokalnej maszynie musi toobe, aby go może tworzyć kopie zapasowe danych tooAzure uwierzytelnienie z magazynu kopii zapasowych. Witaj uwierzytelnianie odbywa się za pośrednictwem *magazynu poświadczeń*. Plik poświadczeń magazynu Hello jest pobierana za pośrednictwem bezpiecznego kanału z portalu klasycznego hello. klucz prywatny certyfikatu Hello nie zmieniają się w portalu hello lub hello usługi.

### <a name="toodownload-hello-vault-credential-file-tooa-local-machine"></a>toodownload hello magazynu poświadczeń pliku tooa komputera lokalnego
1. W okienku nawigacji po lewej stronie powitania kliknij **usług odzyskiwania**, a następnie wybierz hello magazynu kopii zapasowych, który został utworzony.

    ![Początkowa replikacja została zakończona](./media/backup-configure-vault-classic/rs-left-nav.png)
2. Na stronie Szybki Start powitania kliknij **poświadczenia magazynu pobierania**.

   klasyczny portal Hello generuje poświadczenia magazynu przy użyciu kombinacji nazwy magazynu hello i hello bieżącą datę. Plik poświadczeń magazynu Hello jest używany tylko podczas rejestracji hello w przepływie pracy i wygasa po 48 godzin.

   Plik poświadczeń magazynu Hello można pobrać z portalu hello.
3. Kliknij przycisk **zapisać** toodownload hello magazynu poświadczeń pliku toohello folderze pobrane hello konta lokalnego. Możesz też wybrać **Zapisz jako** z hello **zapisać** toospecify menu Plik poświadczeń magazynu hello lokalizację.

   > [!NOTE]
   > Upewnij się, że plik poświadczeń magazynu hello jest zapisany w lokalizacji dostępnej z komputera. Jeśli jest on przechowywany w bloku komunikatów udziale lub na serwerze plików, należy sprawdzić, czy tooaccess uprawnienia hello go.
   >
   >

## <a name="download-install-and-register-hello-backup-agent"></a>Pobieranie, instalowanie i rejestrowanie agenta usługi Kopia zapasowa hello
Po utworzeniu magazynu kopii zapasowych hello i plik poświadczeń magazynu hello pobierania agenta musi być zainstalowany na wszystkich maszynach w systemie Windows.

### <a name="toodownload-install-and-register-hello-agent"></a>toodownload, zainstaluj i zarejestruj hello agenta
1. Kliknij przycisk **usług odzyskiwania**, a następnie wybierz hello magazynu kopii zapasowych, które mają tooregister z serwerem.
2. Na stronie Szybki Start powitania kliknij agenta hello **agenta dla systemu Windows Server lub klienta programu System Center Data Protection Manager lub Windows**. Następnie kliknij przycisk **Save** (Zapisz).

    ![Zapisz agenta](./media/backup-configure-vault-classic/agent.png)
3. Po pobraniu pliku MARSagentinstaller.exe powitania kliknij **Uruchom** (lub kliknij dwukrotnie **MARSAgentInstaller.exe** z lokalizacji hello zapisany).
4. Wybierz folder instalacji hello i folderu pamięci podręcznej, która jest wymagana dla hello agenta, a następnie kliknij przycisk **dalej**. lokalizacji pamięci podręcznej Hello musi mieć co najmniej 5 procent danych kopii zapasowej hello tooat równy wolnego miejsca.
5. Można kontynuować tooconnect toohello Internet za pośrednictwem hello domyślnych ustawień serwera proxy.             Jeśli używasz serwera proxy toohello tooconnect serwera Internet, na stronie Konfiguracja serwera Proxy hello wybierz hello **użyć niestandardowych ustawień serwera proxy** pole wyboru, a następnie wprowadź szczegóły serwera proxy hello. Jeśli korzystasz z uwierzytelnionego serwera proxy, wprowadź szczegóły użytkownika hello nazwę i hasło, a następnie kliknij **dalej**.
6. Kliknij przycisk **zainstalować** instalacji agenta hello toobegin. agent usługi Kopia zapasowa Hello instaluje program .NET Framework 4.5 i programu Windows PowerShell (Jeśli to nie jest jeszcze zainstalowana) toocomplete hello instalacji.
7. Po zainstalowaniu agenta powitania kliknij **kontynuować tooRegistration** toocontinue z hello przepływu pracy.
8. Na stronie magazyn identyfikacji hello Przejrzyj plik poświadczeń magazynu wybierz hello tooand, który został wcześniej pobrany.

    Plik poświadczeń magazynu Hello jest prawidłowy tylko 48 godzin po pobraniu jej z hello portalu. Jeśli wystąpi błąd na tej stronie (np. "poświadczenia magazynu wygasł podany plik"), zaloguj się w portalu toohello i ponownie Pobierz plik poświadczeń magazynu hello.

    Upewnij się, że ten plik poświadczeń magazynu hello jest dostępny w lokalizacji, która hello instalacji aplikacji można uzyskać dostępu do. Jeśli wystąpią błędy dotyczące dostępu, skopiuj hello magazynu poświadczeń pliku tooa tymczasowej lokalizacji na powitania sam komputera i ponów próbę wykonania operacji hello.

    Jeśli wystąpi błąd poświadczeń magazynu, takich jak "magazynu nieprawidłowe poświadczenia podane", plik hello jest uszkodzony lub nie ma hello najnowszych poświadczeń skojarzonych z usługą odzyskiwania hello. Ponów operację powitania po pobraniu nowego pliku poświadczeń magazynu z portalu hello. Ten błąd może wystąpić, gdy użytkownik kliknie hello **poświadczenia magazynu pobierania** opcję wiele razy pod rząd szybkie. W takim przypadku tylko hello ostatni plik poświadczeń magazynu jest nieprawidłowa.
9. Na stronie ustawienie szyfrowania hello można wygenerować hasło lub podać hasło (z co najmniej 16 znaków). Należy pamiętać, toosave hello hasła w bezpiecznym miejscu.
10. Kliknij przycisk **Zakończ**. Hello kreatora rejestrowania serwera rejestruje powitania serwera z kopii zapasowej.

    > [!WARNING]
    > Jeśli utracisz lub zapomnisz hasło hello, Microsoft nie może pomóc w odzyskiwaniu hello dane kopii zapasowej. Jesteś właścicielem hello hasło szyfrowania i Microsoft nie ma wgląd w hello hasło, którego używasz. Zapisz plik hello w bezpiecznej lokalizacji, ponieważ będzie wymagane podczas operacji odzyskiwania.
    >
    >

11. Po ustawieniu klucza szyfrowania hello pozostaw hello **uruchamianie agenta usług odzyskiwania Azure Microsoft** zaznaczone pole wyboru, a następnie kliknij przycisk **Zamknij**.

## <a name="complete-hello-initial-backup"></a>Zakończenie hello początkowa kopia zapasowa
Witaj początkowa kopia zapasowa obejmuje dwa kluczowe zadania:

* Tworzenie harmonogramu tworzenia kopii zapasowych hello
* Tworzenie kopii zapasowej plików i folderów na powitania po raz pierwszy

Po zakończeniu tworzenia początkowej kopii zapasowej hello hello zasad tworzenia kopii zapasowej powoduje utworzenie punktów kopii zapasowych, których można użyć, jeśli potrzebujesz toorecover hello danych. zasady tworzenia kopii zapasowej Hello dzieje się tak na podstawie harmonogramu hello, który należy zdefiniować.

### <a name="tooschedule-hello-backup"></a>Kopia zapasowa hello tooschedule
1. Otwórz hello agenta usługi Kopia zapasowa Microsoft Azure. (Zostanie otwarty automatycznie, gdy zostanie pozostawiony hello **uruchamianie agenta usług odzyskiwania Azure Microsoft** pole wyboru jest zaznaczone, po zamknięciu kreatora rejestrowania serwera hello.) Aby go znaleźć, wyszukaj na maszynie łańcuch **Microsoft Azure Backup**.

    ![Uruchamianie agenta usługi Kopia zapasowa Azure hello](./media/backup-configure-vault-classic/snap-in-search.png)
2. Witaj agenta kopii zapasowej, kliknij przycisk **harmonogram tworzenia kopii zapasowych**.

    ![Planowanie tworzenia kopii zapasowej systemu Windows Server](./media/backup-configure-vault-classic/schedule-backup-close.png)
3. Na powitania wprowadzenie strony hello Kreatora harmonogramu kopii zapasowej, kliknij przycisk **dalej**.
4. Na stronie tooBackup wybierz elementy powitania kliknij **Dodaj elementy**.
5. Wybierz hello pliki i foldery, które mają tooback w górę, a następnie kliknij przycisk **OK**.
6. Kliknij przycisk **Dalej**.
7. Na powitania **Określanie harmonogramu tworzenia kopii zapasowej** Określ hello **harmonogram tworzenia kopii zapasowych** i kliknij przycisk **dalej**.

    Można zaplanować tworzenie kopii zapasowych codziennie (maksymalnie trzy razy) lub co tydzień.

    ![Elementy związane z tworzeniem kopii zapasowej systemu Windows Server](./media/backup-configure-vault-classic/specify-backup-schedule-close.png)

   > [!NOTE]
   > Aby uzyskać więcej informacji o sposobie toospecify hello harmonogram tworzenia kopii zapasowych, zobacz artykuł hello [tooreplace kopia zapasowa Azure użycie infrastruktury taśmy](backup-azure-backup-cloud-as-tape.md).
   >
   >

8. Na powitania **Wybieranie zasady przechowywania** strona, wybierz hello **zasady przechowywania** dla hello kopii zapasowej.

    zasady przechowywania Hello określa hello okres czasu, dla której będą przechowywane hello kopii zapasowej. Zamiast określać "wspólne zasady" dla wszystkich punktów kopii zapasowej, można określić różne zasady przechowywania na podstawie hello tworzenia kopii zapasowej. Można zmodyfikować toomeet zasady przechowywania codziennie, co tydzień, miesięcznych i rocznych hello potrzeb.
9. Na stronie Wybieranie typu początkowej kopii zapasowej hello wybierz typ początkowej kopii zapasowej hello. Pozostaw opcję hello **automatycznie przez sieć hello** zaznaczone, a następnie kliknij przycisk **dalej**.

    Można tworzyć kopie zapasowe automatycznie przez sieć hello, lub w trybie offline, można tworzyć kopie zapasowe. Witaj dalszej części tego artykułu opisano proces hello automatycznego tworzenia kopii zapasowych. Jeśli wolisz toodo kopię zapasową offline, przejrzyj artykuł hello [w trybie Offline kopii zapasowej przepływu pracy w usłudze Kopia zapasowa Azure](backup-azure-backup-import-export.md) Aby uzyskać dodatkowe informacje.
10. Na stronie potwierdzenia hello, przejrzyj informacje hello, a następnie kliknij przycisk **Zakończ**.
11. Po zakończeniu pracy Kreatora hello tworzenie hello harmonogram tworzenia kopii zapasowych, kliknij przycisk **Zamknij**.

### <a name="enable-network-throttling-optional"></a>Włącz ograniczanie przepustowości sieci (opcjonalnie)
agent usługi Kopia zapasowa Hello zapewnia ograniczanie przepustowości sieci. Ograniczanie kontrolek z wykorzystaniem przepustowości sieci podczas transferu danych. Ten formant może być przydatne, gdy konieczne tooback zapasową danych poza godzinami pracy, ale nie chcesz hello toointerfere procesu tworzenia kopii zapasowej z innych ruch internetowy. Ograniczanie stosuje tooback zapasowej i przywracanie działania.

**Ograniczanie przepustowości sieci tooenable**

1. Witaj agenta kopii zapasowej, kliknij przycisk **Zmień właściwości**.

    ![Zmień właściwości](./media/backup-configure-vault-classic/change-properties.png)
2. Na powitania **ograniczania** kartę, zaznacz hello **włączyć użycia przepustowości połączenia internetowego do operacji tworzenia kopii zapasowej** pole wyboru.

    ![Ograniczanie przepustowości sieci](./media/backup-configure-vault-classic/throttling-dialog.png)
3. Po włączeniu ograniczenia przepustowości, określ hello dozwolone przepustowości dla transferu danych kopii zapasowej podczas **godzin pracy** i **godziny wolne**.

    wartości przepustowości Hello rozpocząć 512 kilobitów na sekundę (KB/s) i można przejść w górę too1, 023 MB na sekundę (MB/s). Można również wyznaczyć hello rozpoczęcia i zakończenia **godzin pracy**, i dni tygodnia hello są uważane dniach. Godziny poza wyznaczonych są traktowane jako godzin pracy z systemem innym niż godziny pracy.
4. Kliknij przycisk **OK**.

### <a name="tooback-up-now"></a>tooback zapasową teraz
1. Witaj agenta kopii zapasowej, kliknij przycisk **wykonaj kopię zapasową teraz** hello toocomplete początkowe umieszczanie za pośrednictwem sieci hello.

    ![Natychmiastowe tworzenie kopii zapasowej systemu Windows Server](./media/backup-configure-vault-classic/backup-now.png)
2. Na stronie potwierdzenia hello Przejrzyj hello ustawień, które Witaj ponownie teraz Kreatora konfigurowania użyje tooback hello maszyny. Następnie kliknij pozycję **Utwórz kopię zapasową**.
3. Kliknij przycisk **Zamknij** tooclose hello kreatora. Jeśli zrobisz to przed zakończeniem procesu tworzenia kopii zapasowej hello, Kreator hello nadal toorun w tle hello.

Po zakończeniu tworzenia początkowej kopii zapasowej hello hello **zadanie zostało ukończone** stan zostanie wyświetlony w konsoli usługi Backup hello.

![Początkowa replikacja została zakończona](./media/backup-configure-vault-classic/ircomplete.png)

## <a name="next-steps"></a>Następne kroki
* Zaloguj się do [bezpłatne konto platformy Azure](https://azure.microsoft.com/free/).

Aby uzyskać dodatkowe informacje na temat tworzenia kopii zapasowych maszyn wirtualnych lub innych obciążeń zobacz:

* [Tworzenie kopii zapasowych maszyn wirtualnych IaaS](backup-azure-vms-prepare.md)
* [Tworzenie kopii zapasowej obciążeń tooAzure serwer kopii zapasowej Microsoft Azure](backup-azure-microsoft-azure-backup.md)
* [Tworzenie kopii zapasowej obciążeń tooAzure za pomocą programu DPM](backup-azure-dpm-introduction.md)
