---
title: aaaInstall serwer kopii zapasowej Azure w wersji 2 | Dokumentacja firmy Microsoft
description: "Azure v2 Utwórz kopię zapasową serwera udostępnia udoskonalone funkcje tworzenia kopii zapasowej ochrony maszyn wirtualnych, plików i folderów oraz obciążeń. Dowiedz się, jak tooAzure tooinstall lub uaktualnienia Utwórz kopię zapasową serwera v2."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
ms.assetid: 
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: masaran;markgal
ms.openlocfilehash: 5b1699dadd3a173f1c0ef91a1a600bc5e12f20ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="install-azure-backup-server-v2"></a>Zainstaluj serwer kopii zapasowej systemu Azure w wersji 2

Serwer kopii zapasowej systemu Azure pomaga w ochronie maszyn wirtualnych (VM), obciążenia, pliki i foldery i więcej. Azure v2 Utwórz kopię zapasową serwera oparty na serwer kopii zapasowej Azure w wersji 1 i udostępnia nowe funkcje, które nie są dostępne w wersji 1. Porównanie funkcji między v1 i v2, zobacz [macierzy ochrona serwer kopii zapasowej Azure](backup-mabs-protection-matrix.md). 

uaktualnienie z wersji 1 Utwórz kopię zapasową serwera nie są Hello dodatkowe funkcje w wersji 2 Utwórz kopię zapasową serwera. Jednak v1 Utwórz kopię zapasową serwera nie jest wymagane w przypadku instalowania serwera kopii zapasowej w wersji 2. Jeśli tooupgrade z kopii zapasowej serwera v1 tooBackup Server v2, należy zainstalować v2 Utwórz kopię zapasową serwera na powitania kopii zapasowej ochrony serwera. Istniejących ustawień serwera kopii zapasowej pozostaną nienaruszone.

Utwórz kopię zapasową serwera v2 można zainstalować w systemie Windows Server 2012 R2 lub Windows Server 2016. tootake korzystać z nowych funkcji, takich jak System Center 2016 ochrony Menedżera Modern kopii zapasowej pamięci masowej, v2 kopii zapasowej serwera należy zainstalować w systemie Windows Server 2016. Przed uaktualnieniem instalacji tooor v2 Utwórz kopię zapasową serwera, przeczytaj o hello [wymagania wstępne instalacji](https://docs.microsoft.com/system-center/dpm/install-dpm#setup-prerequisites).

> [!NOTE]
> Serwer kopii zapasowej systemu Azure ma hello tego samego kodu podstawowej jako System Center Data Protection Manager. V1 serwera kopii zapasowej jest równoważne tooData Protection Manager 2012 R2, a v2 Utwórz kopię zapasową serwera jest równoważne tooData Protection Manager 2016. W tym artykule odwołuje się od czasu do czasu hello dokumentacji programu Data Protection Manager.
>
>

## <a name="upgrade-backup-server-toov2"></a>Uaktualnij toov2 kopii zapasowej serwera
tooupgrade z kopii zapasowej serwera v1 tooBackup Server v2, upewnij się, że instalacja ma hello wymagane aktualizacje:

- [Aktualizowanie agentów ochrony hello](backup-mabs-upgrade-to-v2.md#update-the-dpm-protection-agent) na powitania chronionymi serwerami.
- Uaktualnienie systemu Windows Server 2012 R2 tooWindows Server 2016.
- Uaktualnij administratora zdalnego serwera kopii zapasowej platformy Azure na wszystkich serwerach produkcyjnych.
- Upewnij się, że kopie zapasowe są ustawione toocontinue bez ponownego uruchomienia serwera produkcyjnego.


### <a name="upgrade-steps-for-backup-server-v2"></a>Kroki uaktualniania dla kopii zapasowej serwera w wersji 2

1. W Centrum pobierania hello [Pobierz Instalator uaktualnienia hello](https://go.microsoft.com/fwlink/?LinkId=626082).

2. Po wyodrębnieniu hello Kreatora instalacji upewnij się, że **wykonania setup.exe** jest wybrany, a następnie wybierz **Zakończ**.

  ![Instalator Instalatora — należy uruchomić Instalator](./media/backup-mabs-upgrade-to-v2/run-setup.png)

3. W Kreatorze hello serwer kopii zapasowej Microsoft Azure w obszarze **zainstalować**, wybierz pozycję **serwer kopii zapasowej Microsoft Azure**.

  ![Instalator Instalatora — wybierz opcję instalacji](./media/backup-mabs-upgrade-to-v2/mabs-installer-s1.png)

4. Na powitania **powitalnej** Przejrzyj hello ostrzeżenia, a następnie wybierz **dalej**.

  ![Instalator Instalatora - strony powitalnej](./media/backup-mabs-upgrade-to-v2/mabs-installer-s2.png)

5. Kreator instalacji Hello wykonuje sprawdzanie wymagań wstępnych toomake się, że w środowisku można uaktualnić. Na powitania **wymagań wstępnych sprawdza** wybierz pozycję **Sprawdź**.

  ![Instalator — strona kontroli wymagań wstępnych Instalatora](./media/backup-mabs-upgrade-to-v2/mabs-installer-s3-perform-checks.png)

6. Środowisko musi przejść pomyślnie hello wymagań wstępnych. Jeśli w środowisku nie przeszły pomyślnie testu hello, zanotuj hello problemy, a następnie naprawione. Następnie wybierz opcję **Sprawdź ponownie**. Po przekazujesz hello wymagań wstępnych, wybierz **dalej**.

  ![Instalator Instalatora — przycisk Sprawdź ponownie](./media/backup-mabs-upgrade-to-v2/mabs-installer-s4-pass-checks.png)

7. Na powitania **ustawienia SQL** , wybierz odpowiednią opcję hello do instalacji programu SQL, a następnie wybierz **Sprawdź i zainstaluj**.

  ![Instalator Instalatora — strona ustawień SQL](./media/backup-mabs-upgrade-to-v2/mabs-installer-s5-sql-settings.png)

  Sprawdzanie Hello może potrwać kilka minut. Kiedy kontroli hello są gotowe, wybierz pozycję **dalej**.

  ![Instalator Instalatora — Sprawdź ustawienia SQL i przycisk Zainstaluj](./media/backup-mabs-upgrade-to-v2/mabs-installer-s5a-check-and fix-settings.png)

8. Na powitania **ustawienia instalacji** pozycję dowolnej lokalizacji toohello zmiany, których zainstalowano Utwórz kopię zapasową serwera lub toohello lokalizacji przechowywania plików tymczasowych. Wybierz **dalej**.

  ![Instalator Instalatora — strona Ustawienia instalacji](./media/backup-mabs-upgrade-to-v2/mabs-installer-s6-installation-settings.png)

9. toofinish hello Kreatora instalacji, wybierz opcję **Zakończ**.

  ![Instalator Instalatora — zakończenie](./media/backup-mabs-upgrade-to-v2/run-setup.png)



## <a name="add-storage-for-modern-backup-storage"></a>Dodawanie magazynu dla nowoczesnych magazynu kopii zapasowej

wydajność magazynu kopii zapasowej tooimprove, v2 Utwórz kopię zapasową serwera dodaje obsługę woluminów. Jak serwer zapasowy v1 v2 Utwórz kopię zapasową serwera obsługuje dyski.

### <a name="add-volumes-and-disks"></a>Dodaj do woluminów i dysków
Po uruchomieniu v2 Utwórz kopię zapasową serwera w systemie Windows Server 2016 można użyć woluminów toostore kopii zapasowej danych. Woluminy oferują oszczędności pojemności magazynu i szybsze tworzenie kopii zapasowych. Ponieważ woluminy są tooBackup nowego serwera, należy je dodać. 

Po dodaniu tooBackup woluminu serwera można nadać woluminu hello przyjazną nazwę. Kliknij przycisk hello **przyjazną nazwę** kolumny woluminu hello ma tooname. Nazwa hello można zmienić później, jeśli to konieczne. Możesz również użyć programu PowerShell tooadd lub zmienić przyjazne nazwy dla woluminów.

tooadd woluminu w hello Konsola administratora:

1. W konsoli administratora serwera kopii zapasowej Azure hello, wybierz **zarządzania** > **Magazyn dyskowy** > **Dodaj**.

    ![Otwórz hello kreatora Dodawanie magazynu dyskowego](./media//backup-mabs-upgrade-to-v2/open-add-disk-storage-wizard.png)

    Spowoduje to otwarcie kreatora Dodawanie magazynu dyskowego hello.

2. Na powitania **dodać magazyn dyskowy** strony w hello **dostępnych woluminów** , wybierz wolumin, a następnie wybierz **Dodaj**.
3. W hello **wybrane woluminy** Wprowadź przyjazną nazwę dla woluminu hello, a następnie wybierz **OK**.

      ![Magazyn dyskowy Kreator dodawania — Dodawanie woluminu](./media/backup-mabs-upgrade-to-v2/add-volume.png)

  Jeśli chcesz tooadd dysku, dysku hello muszą należeć tooa grupy ochrony, która ma starszej wersji magazynu. Te dyski mogą być używane tylko dla tych grup ochrony. Jeśli serwer zapasowy nie ma źródeł, które mają ochronę za pomocą starszej wersji, nie ma na liście hello dysku.

  Aby uzyskać więcej informacji na temat dodawania dysków, zobacz [Dodawanie magazynu starszych tooincrease dysków](http://docs.microsoft.com/system-center/dpm/upgrade-to-dpm-2016#adding-disks-to-increase-legacy-storage). Nie można nadać przyjazną nazwę dysku.


### <a name="assign-workloads-toovolumes"></a>Przypisz toovolumes obciążeń

Utwórz kopię zapasową serwera, należy określić w obciążeń, które są przypisane toowhich woluminów. Na przykład można ustawić kosztowne woluminów, które obsługują dużej liczby operacji wejścia/wyjścia na drugim (IOPS) toostore tylko obciążeń, które wymagają częstego, dużej liczby kopii zapasowych. Przykładem jest program SQL Server z dzienników transakcji.

#### <a name="update-dpmdiskstorage"></a>DPMDiskStorage aktualizacji

właściwości hello tooupdate woluminu w puli magazynu hello w kopii zapasowej serwera, użyj polecenia cmdlet programu PowerShell hello DPMDiskStorage aktualizacji.

Składnia:

`Parameter Set: Volume`

```
Update-DPMDiskStorage [-Volume] <Volume> [[-FriendlyName] <String> ] [[-DatasourceType] <VolumeTag[]> ] [-Confirm] [-WhatIf] [ <CommonParameters>]
```

Wszystkie zmiany wprowadzone przy użyciu programu PowerShell są odzwierciedlane w hello interfejsu użytkownika.


## <a name="protect-data-sources"></a>Ochrona źródeł danych
toobegin ochrona źródeł danych, Utwórz grupę ochrony. Witaj następujące kroki Wyróżnij zmiany lub dodatki toohello Kreatora nowej grupy ochrony.

toocreate grupy ochrony:

1. W konsoli administratora serwera kopii zapasowej hello, wybierz **ochrony**.

2. Na wstążce narzędzi hello, wybierz **nowy**.

    Spowoduje to otwarcie Kreatora tworzenia nowej grupy ochrony hello.

  ![Kreator tworzenia nowej grupy ochrony](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-1.png)

3. Na powitania **powitalnej** wybierz pozycję **dalej**.
4. Na powitania **wybierz typ grupy ochrony** wybierz typ grupy ochrony mają toocreate, a następnie wybierz hello **dalej**.

  ![Strona Typ wybierz grupę ochrony](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-2.png)

5. Na powitania **Wybierz członków grupy** strony w hello **dostępni członkowie** okienka, hello członków z ochrony agenci są wyświetlane. Na przykład wybierz wolumin D:\ i E:\ i dodaj je toohello **wybranych składników** okienka. Wybierz **dalej**.

  ![Wybierz grupy elementów członkowskich strony](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-3.png)

6. Na powitania **wybierz metodę ochrony danych** wprowadź **Nazwa grupy ochrony**, wybierz metodę ochrony hello, a następnie wybierz **dalej**. Jeśli chcesz uzyskać krótkoterminową ochronę, musisz wybrać hello **dysku** kopii zapasowej metody.

  ![Wybierz metodę ochrony danych strony](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-4.png)

7. Na powitania **Określ cele krótkoterminowe** strony szczegółów wybierz hello **zakres przechowywania** i **częstotliwość synchronizacji**. Następnie wybierz opcję **dalej**. Opcjonalnie toochange hello harmonogram gdy punkty odzyskiwania są podejmowane, wybierz pozycję **Modyfikuj**.

  ![Określ cele krótkoterminowe strony](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-5.png)

8. Na powitania **Przejrzyj przydział magazynu dyskowego** Przejrzyj szczegóły dotyczące wybranych źródeł danych hello, rozmiar i wartości dla toobe miejsca hello zainicjowano obsługę administracyjną i hello woluminu magazynu docelowego.

  ![Przejrzyj przydział magazynu dyskowego strony](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-6.png)

  Woluminy magazynu są oparte na alokacji woluminu obciążenia hello (Ustaw przy użyciu programu PowerShell) i hello dostępny magazyn. Woluminy magazynu hello można zmienić, wybierając w menu rozwijanym hello inne woluminy. W przypadku zmiany wartości hello **docelowy magazyn**, hello wartość **magazynu dostępnego dysku** dynamicznie zmiany wartości tooreflect **wolnego miejsca** i **Underprovisioned miejsca**.

  Jeśli źródeł danych hello wzrostu zgodnie z planem, hello wartość hello **Underprovisioned miejsca** kolumny w **magazynu dostępnego dysku** odzwierciedla hello ilość dodatkowego magazynu, które ma potrzebne. Użyj tego planu toohelp wartość magazynu musi smooth kopii zapasowych. Jeśli hello wartość wynosi zero, nie ma żadnych potencjalnych problemów z magazynem, w najbliższej przyszłości hello. Jeśli wartość hello jest liczbą różne od zera, nie ma wystarczającej ilości miejsca przydzielone (oparte na sieci ochrony zasad i hello rozmiar danych z chronionych elementów członkowskich).

  ![Magazyn dyskowy niedostatecznej alokacji](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-7.png)

   toofinish Tworzenie kreatora hello pełną, grupy ochrony.

## <a name="migrate-legacy-storage-toomodern-backup-storage"></a>Migrowanie starszych magazynu tooModern magazynu kopii zapasowej
Po przeprowadzeniu uaktualnienia instalacji tooor Utwórz kopię zapasową serwera v2 i hello uaktualnienia systemu operacyjnego tooWindows Server 2016, należy zaktualizować toouse grupy z ochrony nowoczesnych magazynu kopii zapasowej. Domyślnie nie są zmieniane grup ochrony. Nadal toofunction jako początkowo zostały ustawione. 

Aktualizowanie toouse grup ochrony nowoczesnych magazynu kopii zapasowej jest opcjonalna. tooupdate hello grupy ochrony, Zatrzymaj ochronę wszystkich źródeł danych za pomocą hello zachować opcji danych. Następnie należy dodać hello danych źródeł tooa nowej grupy ochrony.

1. W konsoli administratora hello, wybierz hello **ochrony** funkcji. W hello **członka grupy ochrony** listy, kliknij prawym przyciskiem myszy element członkowski hello, a następnie wybierz **Zatrzymaj ochronę członka**.

  ![Zatrzymaj ochronę członka](http://docs.microsoft.com/system-center/dpm/media/upgrade-to-dpm-2016/dpm-2016-stop-protection1.png)

2. W hello **Usuń z grupy** okno dialogowe, przejrzyj hello używane miejsce na dysku i hello dostępne wolne miejsce w puli magazynów hello. domyślne Hello jest punktów odzyskiwania hello tooleave na powitania dysku i zezwolić im tooexpire na skojarzonych zasad przechowywania. Kliknij przycisk **OK**.

  Puli magazynu wolnego toohello miejsca tooimmediately zwracany hello używane dysku, wybierz opcję hello **Usuń replikę z dysku** pole wyboru toodelete hello kopii zapasowej danych (i punktów odzyskiwania) skojarzone z tym członkiem.

  ![Usuń z grupy, okno dialogowe](http://docs.microsoft.com/system-center/dpm/media/upgrade-to-dpm-2016/dpm-2016-retain-data.png)

3. Utwórz grupę ochrony, która używa nowoczesnej magazynu kopii zapasowej. Zawierają hello bez ochrony źródeł danych.


## <a name="add-disks-tooincrease-legacy-storage"></a>Dodawanie dysków tooincrease starszych magazynu

Toouse starszej wersji magazynu z kopii zapasowej serwera należy może być konieczne tooadd dysków tooincrease starszej wersji magazynu. 

Magazyn dyskowy tooadd:

1. W konsoli administratora hello, wybierz **zarządzania** > **Magazyn dyskowy** > **Dodaj**.

    ![Magazyn dyskowy okno dialogowe Dodawanie](http://docs.microsoft.com/system-center/dpm/media/upgrade-to-dpm-2016/dpm-2016-add-disk-storage.png)

4. W hello **dodać magazyn dyskowy** okno dialogowe, wybierz opcję **Dodaj dyski**.

5. Hello listy dostępnych dysków, wybierz hello dyski, które chcesz tooadd, wybierz opcję **Dodaj**, a następnie wybierz **OK**.

## <a name="update-hello-data-protection-manager-protection-agent"></a>Zaktualizuj agenta ochrony programu Data Protection Manager hello

Utwórz kopię zapasową serwera używa hello System Center Data Protection Manager protection agent aktualizacji. Jeśli przeprowadzasz uaktualnienie agenta ochrony, który nie jest połączony toohello sieci, nie można użyć hello toocomplete Data Protection Manager Administrator Console uaktualnienia podłączonego agenta. Należy uaktualnić agenta ochrony hello w środowisku domeny nieaktywny. Dopóki hello komputer kliencki jest połączony toohello sieci, powitalne Data Protection Manager Administrator Console pokazuje tej aktualizacji agenta ochrony hello jest w stanie oczekiwania.

Witaj poniższych sekcjach opisano sposób tooupdate agentów ochrony dla komputerów klienckich, które są połączone i komputery klienckie, które nie są połączone.

### <a name="update-a-protection-agent-for-a-connected-client-computer"></a>Zaktualizuj agenta ochrony na podłączonym komputerze klienckim

1. W konsoli administratora serwera kopii zapasowej hello, wybierz **zarządzania** > **agentów**.

2. W okienku wyświetlania hello wybierz komputery klienckie hello, dla których ma agenta ochrony hello tooupdate.

  > [!NOTE]
  > Witaj **aktualizacji agenta** kolumna wskazuje, kiedy aktualizacji agenta ochrony jest dostępne dla każdego komputera chronionego. W hello **akcje** okienka, hello **aktualizacji** akcja jest dostępna tylko wtedy, gdy komputer chroniony jest zaznaczony i są dostępne aktualizacje.
  >
  >

3. tooinstall aktualizacji agentów ochrony na komputerach hello wybrane w hello **akcje** okienku wybierz **aktualizacji**.

### <a name="update-a-protection-agent-on-a-client-computer-that-is-not-connected"></a>Zaktualizuj agenta ochrony na komputerze klienckim, który nie jest połączony

1. W konsoli administratora serwera kopii zapasowej hello, wybierz **zarządzania** > **agentów**.

2. W okienku wyświetlania hello wybierz komputery klienckie hello, dla których ma agenta ochrony hello tooupdate.

  > [!NOTE]
   > Witaj **aktualizacji agenta** kolumna wskazuje, kiedy aktualizacji agenta ochrony jest dostępne dla każdego komputera chronionego. W hello **akcje** okienka, hello **aktualizacji** akcja jest niedostępna, gdy komputer chroniony jest zaznaczony, chyba że są dostępne aktualizacje.
  >
  >

3. tooinstall aktualizacji agentów ochrony na komputerach hello wybrana, wybierz opcję **aktualizacji**.

4. Dla komputera klienckiego, który nie jest połączonych sieci toohello, dopóki hello komputer jest połączony toohello sieci, hello **stan agenta** kolumna zawiera stan **oczekująca aktualizacja**.

  Komputer kliencki po sieci połączonych toohello hello **aktualizacji agenta** kolumny dla komputera klienckiego hello wskazuje stan **aktualizacji**.
  
### <a name="move-legacy-protection-groups-from-old-version-and-sync-hello-new-version-with-azure"></a>Przenieść starszych grup ochrony z starszą wersję i synchronizacji hello nowej wersji przy użyciu platformy Azure

Gdy aktualizacji są zarówno serwer kopii zapasowej Azure i hello systemu operacyjnego, jest gotowy tooprotect nowych źródeł danych przy użyciu nowoczesnych magazynu kopii zapasowej. Jednak już chronione źródła danych będą nadal toobe chronione w starszej wersji hello sposób, jak były na serwerze kopii zapasowej Azure, ale wszystkie nowe ochrony będzie używać nowoczesnych magazynu kopii zapasowej.

Następujące czynności są toomigrate źródeł danych z magazynu kopii zapasowych tooModern ochrony starszej wersji trybu.

• Dodaj hello nowych woluminów toohello puli magazynów programu DPM i przypisz przyjazną tagi źródła danych i nazwy, w razie potrzeby.
• Dla każdego źródła danych, która jest w trybie starszej wersji, Zatrzymaj ochronę źródła danych hello i "Zachowaj chronione dane".  Pozwoli to odzyskiwania starych punktów odzyskiwania po migracji.

• Utwórz nowy PG i wybierz hello źródeł danych, które są toobe przechowywane przy użyciu nowego formatu.
• Program DPM wykona kopia repliki z magazynu kopii zapasowych starszych hello do hello lokalnie nowoczesnych magazynu kopii zapasowej woluminu.
Uwaga: To będą widoczne jako • zadania po odzyskiwaniu operacji wszystkie nowe synchronizacji i punktów odzyskiwania będą następnie przechowywane w nowoczesnych magazynu kopii zapasowej.
• Stare punkty odzyskiwania będą usuwane limit wygaśnie i ostatecznie wolnego miejsca na dysku hello.
• Po wszystkich woluminów starszych hello są usuwane z hello starego magazynu, dysk hello można usunąć z platformy Azure i hello kopii zapasowych systemu.
• Wykonaj kopię zapasową programu hello Azure DPMDB.

Część 2:-ważne elementy > hello nowego serwera należy toobe o nazwie takie same jak hello oryginalny serwer usługi Kopia zapasowa Azure. Nie można zmienić nazwy hello hello nowego serwera kopii zapasowej Azure, jeśli chcesz toouse starego pulę magazynu i punkty odzyskiwania tooretain DPMDB — musi mieć kopię zapasową bazy danych dpmdb należy przywrócić toobe

1) Zamknięcie hello oryginalny serwer kopii zapasowej platformy Azure lub wyłączanie przewodowy hello.
2) Resetuj hello konta komputera w usłudze active directory.
3) Zainstaluj Server 2016 na nowej maszyny i nazwy jej hello tej samej nazwy komputera jako hello oryginalny serwer usługi Kopia zapasowa Azure.
4) Dołącz hello domeny
5) Zainstaluj serwer usługi Kopia zapasowa Azure w wersji 2 (dyski puli magazynów DPM przenieść ze starego serwera, a następnie zaimportuj)
6) Przywróć hello DPMDB pobranych z końcem część 2
7) Dołącz hello magazynu z hello oryginalny serwer zapasowy toohello nowego serwera.
8) Z hello SQL przywracania bazy danych DPMDB
9) Z wiersza polecenia administratora na nowy serwer tooMicrosoft cd kopia zapasowa Azure Zainstaluj lokalizacji i otworzyć folder bin

Przykład ścieżki: C:\windows\system32 > cd "c:\Program Files\Microsoft Azure Backup\DPM\DPM\bin\
Kopia zapasowa tooAzure wykonaj polecenie DPMSYNC-SYNC

10) Uruchom polecenie DPMSYNC-SYNC Uwaga Po dodaniu nowej puli magazynu programu DPM toohello dysków zamiast przenoszenia hello stare, następnie uruchom polecenie DPMSYNC - Reallocatereplica

## <a name="new-powershell-cmdlets-in-v2"></a>Nowe polecenia cmdlet programu PowerShell w wersji 2

Po zainstalowaniu serwera usługi Kopia zapasowa Azure w wersji 2, dostępne są dwa nowe polecenia cmdlet: 
* [DPMRecoveryPoint instalacji](https://technet.microsoft.com/library/mt787159.aspx)
* [Odinstalowywanie DPMRecoveryPoint](https://technet.microsoft.com/library/mt787158.aspx)

## <a name="next-steps"></a>Następne kroki

Dowiedz się, jak tooprepare serwera lub Włącz ochronę obciążenia:
- [Przygotowanie serwera kopii zapasowej obciążeń](backup-azure-microsoft-azure-backup.md)
- [Użyj tooback serwera kopii zapasowej serwera VMware](backup-azure-backup-server-vmware.md)
- [Użyj tooback serwera kopii zapasowej serwera SQL](backup-azure-sql-mabs.md)
- [Nowoczesne magazynu kopii zapasowej za pomocą kopii zapasowej serwera](backup-mabs-add-storage.md)

