---
title: aaaAzure serwera kopii zapasowej stanu systemu chroni i przywraca systemu operacyjnego toobare | Dokumentacja firmy Microsoft
description: "Użyj serwera usługi Kopia zapasowa Azure tooback stanu systemu i zapewniają ochronę odzyskiwania kompletnego stanu systemu od zera (BMR)."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
keywords: 
ms.assetid: 
ms.service: backup
ms.workload: storage-backup-recovery
ms.targetplatform: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: markgal,masaran
ms.openlocfilehash: d34c8bbdc7cc24c905f81ceaf199698c1ee923db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-system-state-and-restore-toobare-metal-with-azure-backup-server"></a>Wykonaj kopię zapasową stanu systemu i przywracanie toobare systemu operacyjnego z serwera usługi Kopia zapasowa Azure

Serwer kopii zapasowej systemu Azure wykonuje kopię zapasową stanu systemu i zapewnia ochronę odzyskiwania zera (BMR).

*   **Kopia zapasowa stanu systemu**: tworzy kopie zapasowe plików systemu operacyjnego, więc można odzyskać, gdy komputer jest uruchamiany, ale system plików i rejestru hello zostaną utracone. Kopię zapasową stanu systemu zawiera:
    * Element członkowski domeny: rozruch plików, COM + baza danych rejestracji klasy, rejestru
    * Kontroler domeny: rozruchu systemu Windows Server Active Directory (NTDS), plików, COM + baza danych rejestracji klasy, rejestru, wolumin systemowy (SYSVOL)
    * Komputer z uruchomioną usług klastrowania: metadanych serwera klastra
    * Komputer z uruchomioną usług certyfikatów: certyfikat danych
* **Kopia zapasowa bez systemu operacyjnego**: tworzy kopie zapasowe plików systemu operacyjnego i wszystkich danych na woluminach krytycznych (z wyjątkiem danych użytkownika). Zgodnie z definicją kopia zapasowa BMR obejmuje kopię zapasową stanu systemu. Kiedy komputer nie uruchamia się i masz toorecover wszystko, zapewnia ochronę.

Hello w poniższej tabeli podsumowano, co można wykonać kopię zapasową i odzyskiwanie. Aby uzyskać szczegółowe informacje o wersji aplikacji, które mogą być chronione przy użyciu stanu systemu i BMR, zobacz [czego serwer kopii zapasowej Azure Utwórz kopię zapasową?](backup-mabs-protection-matrix.md).

|Tworzenie kopii zapasowych|Problem|Odzyskiwanie z kopii zapasowej serwera kopii zapasowej Azure|Odzyskiwanie z kopii zapasowej stanu systemu|ODZYSKIWANIA SYSTEMU OD ZERA|
|----------|---------|---------------------------|------------------------------------|-------|
|**Plik danych**<br /><br />Regularnego tworzenia kopii zapasowych<br /><br />Kopii zapasowej BMR/system stanu|Utraconych danych|Tak|N|N|
|**Plik danych**<br /><br />Kopia zapasowa Azure serwera kopii zapasowej danych plików<br /><br />Kopii zapasowej BMR/system stanu|Utraconego lub uszkodzonego systemu operacyjnego|N|Tak|Tak|
|**Plik danych**<br /><br />Kopia zapasowa Azure serwera kopii zapasowej danych plików<br /><br />Kopii zapasowej BMR/system stanu|Utracony serwer (nieuszkodzone woluminy danych)|N|N|Tak|
|**Plik danych**<br /><br />Kopia zapasowa Azure serwera kopii zapasowej danych plików<br /><br />Kopii zapasowej BMR/system stanu|Utracony serwer (utracone woluminy danych)|Tak|Nie|Tak (BMR, następuje zwykłe odzyskiwanie kopii zapasowej pliku danych)|
|**Dane programu SharePoint**:<br /><br />Utwórz kopię zapasową serwera kopii zapasowej systemu Azure danych farmy<br /><br />Kopii zapasowej BMR/system stanu|Utracone witryny, listy, elementy listy, dokumentów|Tak|N|N|
|**Dane programu SharePoint**:<br /><br />Utwórz kopię zapasową serwera kopii zapasowej systemu Azure danych farmy<br /><br />Kopii zapasowej BMR/system stanu|Utraconego lub uszkodzonego systemu operacyjnego|N|Tak|Tak|
|**Dane programu SharePoint**:<br /><br />Utwórz kopię zapasową serwera kopii zapasowej systemu Azure danych farmy<br /><br />Kopii zapasowej BMR/system stanu|Odzyskiwanie po awarii|N|N|N|
|Windows Server 2012 R2 Hyper-V<br /><br />Utwórz kopię zapasową serwera kopii zapasowej systemu Azure hosta funkcji Hyper-V lub gościa<br /><br />Kopia zapasowa stanu BMR/systemu hosta|Utracone maszyny Wirtualnej|Tak|N|N|
|Funkcja Hyper-V<br /><br />Utwórz kopię zapasową serwera kopii zapasowej systemu Azure hosta funkcji Hyper-V lub gościa<br /><br />Kopia zapasowa stanu BMR/systemu hosta|Utraconego lub uszkodzonego systemu operacyjnego|N|Tak|Tak|
|Funkcja Hyper-V<br /><br />Utwórz kopię zapasową serwera kopii zapasowej systemu Azure hosta funkcji Hyper-V lub gościa<br /><br />Kopia zapasowa stanu BMR/systemu hosta|Utracone hosta funkcji Hyper-V (nieuszkodzone VMs)|N|N|Tak|
|Funkcja Hyper-V<br /><br />Utwórz kopię zapasową serwera kopii zapasowej systemu Azure hosta funkcji Hyper-V lub gościa<br /><br />Kopia zapasowa stanu BMR/systemu hosta|Utracone hosta funkcji Hyper-V (utracone maszyny wirtualne)|N|N|Tak<br /><br />Odzyskiwania systemu od ZERA, następuje zwykłe odzyskiwanie serwera usługi Kopia zapasowa Azure|
|Wymiana serwer SQL<br /><br />Utwórz kopię zapasową serwera aplikacji usługa Kopia zapasowa Azure<br /><br />Kopii zapasowej BMR/system stanu|Dane aplikacji utracone|Tak|N|N|
|Wymiana serwer SQL<br /><br />Utwórz kopię zapasową serwera aplikacji usługa Kopia zapasowa Azure<br /><br />Kopii zapasowej BMR/system stanu|Utraconego lub uszkodzonego systemu operacyjnego|N|Y|Tak|
|Wymiana serwer SQL<br /><br />Utwórz kopię zapasową serwera aplikacji usługa Kopia zapasowa Azure<br /><br />Kopii zapasowej BMR/system stanu|Utracony serwer (nieuszkodzone dzienniki transakcji/bazy danych)|N|N|Tak|
|Wymiana serwer SQL<br /><br />Utwórz kopię zapasową serwera aplikacji usługa Kopia zapasowa Azure<br /><br />Kopii zapasowej BMR/system stanu|Utracony serwer (utracone dzienniki transakcji/bazy danych)|N|N|Tak<br /><br />Odzyskiwania systemu od ZERA, następuje zwykłe odzyskiwanie serwera usługi Kopia zapasowa Azure|

## <a name="how-system-state-backup-works"></a>Jak działa kopii zapasowej stanu systemu

Po uruchomieniu kopii zapasowej stanu systemu, Utwórz kopię zapasową serwera komunikuje się z toorequest kopia zapasowa systemu Windows Server za kopii zapasowej stanu systemu serwera hello. Utwórz kopię zapasową serwera i kopia zapasowa systemu Windows Server domyślnie używają hello dysk, który ma hello największą ilość wolnego miejsca. Informacje o dysku są zapisywane w pliku PSDataSourceConfig.xml hello. Jest to dysk hello, która kopia zapasowa systemu Windows Server używa kopii zapasowych.

Można dostosować hello dysk, który używa serwera zapasowego hello kopii zapasowej stanu systemu. Na serwerze hello chronione Przejdź tooC:\Program Files\Microsoft Manager\MABS\Datasources ochrony danych. Otwórz plik PSDataSourceConfig.xml hello do edycji. Zmień hello \<FilesToProtect\> wartość hello literę dysku. Zapisz i zamknij plik hello. Jeśli istnieje tooprotect hello stan systemu komputera hello zestawu grup ochrony, uruchom sprawdzanie spójności. Jeśli alert jest generowany, wybierz **Modyfikuj grupę ochrony** w hello alert, a następnie pełne hello kreatora. Następnie uruchom kolejną kontrolę spójności.

Należy pamiętać, że jeśli serwer ochrony hello jest w klastrze, możliwe, że dysk klastra zostanie wybrany jako dysk hello z hello największej ilości wolnego miejsca. Własności tego dysku zostało wyłączone tooanother węzła i uruchomienia kopii zapasowej stanu systemu, hello dysku nie jest dostępna i hello kopii zapasowej nie powiedzie się. W tym scenariuszu należy zmodyfikować PSDataSourceConfig.xml toopoint tooa dysku.

Następnie kopia zapasowa systemu Windows Server tworzy folder o nazwie w głównym hello hello przywracania folder WindowsImageBackup. Jak Kopia zapasowa systemu Windows Server tworzy kopię zapasową hello, wszystkie dane hello jest umieszczony w tym folderze. Po zakończeniu operacji tworzenia kopii zapasowej hello pliku hello jest przekazanych toohello komputera serwera kopii zapasowej. Należy zwrócić uwagę hello następujących informacji:

* Ten folder i jego zawartość nie wyczyszczono po zakończeniu operacji transferu lub kopii zapasowej hello. Hello najlepsze sposób toothink tego jest, że hello miejsce pozostaje zarezerwowane dla hello następnej kopii zapasowej zostało zakończone.
* Hello folder jest tworzony za każdym razem, gdy kopia zapasowa ma zostać. Witaj datą i godziną odzwierciedlają hello godzina ostatniej kopii zapasowej stanu systemu.

## <a name="bmr-backup"></a>Kopii zapasowej BMR

Odzyskiwania systemu od zera (łącznie z kopii zapasowej stanu systemu) zadanie tworzenia kopii zapasowej hello jest zapisywany bezpośrednio tooa udziału na komputerze serwera kopii zapasowej hello. Tooa folder nie jest zapisywana na serwerze hello chronione.

Utwórz kopię zapasową serwera wywołuje kopia zapasowa systemu Windows Server i udostępni hello woluminu repliki dla kopii zapasowej BMR. W takim przypadku program nie nakazuje dysku hello toouse kopia zapasowa systemu Windows Server z hello największej ilości wolnego miejsca. Zamiast tego używa udziału hello, który został utworzony dla zadania hello.

Po zakończeniu operacji tworzenia kopii zapasowej hello pliku hello jest przekazanych toohello komputera serwera kopii zapasowej. Dzienniki są przechowywane w C:\Windows\Logs\WindowsServerBackup.

## <a name="prerequisites-and-limitations"></a>Wymagania wstępne i ograniczenia

-   Odzyskiwania systemu od ZERA nie jest obsługiwana dla komputerów z systemem Windows Server 2003 lub na komputerach z systemem operacyjnym klienta.

-   Nie można włączyć ochrony BMR i systemu stanu dla hello sam komputer w różnych grupach ochrony.

-   Komputer Utwórz kopię zapasową serwera nie może chronić siebie samego przy odzyskiwania systemu od ZERA.

-   Krótkoterminowe tootape ochrony (dysk taśma lub D2T) nie jest obsługiwana dla odzyskiwania systemu od ZERA. Długoterminowe tootape magazynu (dysk do dysk taśma lub D2D2T) jest obsługiwana.

-   W przypadku ochrony BMR kopia zapasowa systemu Windows Server musi być zainstalowany na komputerze hello chronione.

-   W przypadku ochrony BMR w przeciwieństwie do ochrony stanu systemu, Utwórz kopię zapasową serwera nie ma żadnych wymagań dotyczących miejsca na powitania chronionego komputera. Kopia zapasowa systemu Windows Server bezpośrednio przesyła kopie zapasowe toohello kopii zapasowej serwera. zadanie tworzenia kopii zapasowej transferu Hello nie pojawia się na powitania Utwórz kopię zapasową serwera **zadania** widoku.

-   Utwórz kopię zapasową serwera rezerwuje 30 GB miejsca na woluminie repliki hello odzyskiwania systemu od zera. Można to zmienić na powitania **przydział dysku** stronie powitania Kreatora modyfikacji grupy ochrony lub przy użyciu polecenia cmdlet Get-DatasourceDiskAllocation i Set-DatasourceDiskAllocation w środowisku PowerShell hello. Na woluminie punktu odzyskiwania hello ochrona BMR wymaga około 6 GB do przechowywania danych przez pięć dni.
    * Należy pamiętać, że nie można zmniejszyć hello repliki woluminu rozmiar tooless niż 15 GB.
    * Utwórz kopię zapasową serwera nie oblicza rozmiaru źródła danych BMR hello hello. Zakłada się 30 GB dla wszystkich serwerów. Zmień wartość hello na podstawie rozmiaru hello kopii zapasowych BMR, które mogą pojawić się w danym środowisku. rozmiar kopii zapasowej BMR Hello około obliczany jako suma miejsca używanego hello na wszystkie woluminy krytyczne. Woluminy krytyczne = wolumin rozruchowy + wolumin systemowy + wolumin obsługujący dane o stanie systemu, takie jak Active Directory.

-   W przypadku zmiany z ochrony tooBMR ochrony stanu systemu, ochrona BMR wymaga mniej miejsca na powitania *woluminu punktu odzyskiwania*. Jednak hello dodatkowe miejsce na woluminie hello jest nie odzyskana. Można ręcznie zmniejszyć rozmiar woluminu hello na powitania **modyfikowanie przydziału dysku** hello kreatora modyfikacji grupy ochrony lub przy użyciu polecenia cmdlet Get-DatasourceDiskAllocation i Set-DatasourceDiskAllocation w środowisku PowerShell hello.

    W przypadku zmiany z ochrony tooBMR ochrony stanu systemu, ochrona BMR wymaga więcej miejsca na powitania *woluminu repliki*. Witaj wolumin zostanie automatycznie rozszerzony. Jeśli chcesz toochange hello domyślne alokacje miejsca, użyj polecenia cmdlet programu PowerShell Modify-DiskAllocation hello.

-   W przypadku zmiany z ochrony stanu toosystem ochrony BMR, potrzebujesz więcej miejsca na woluminie punktu odzyskiwania hello. Utwórz kopię zapasową serwera spróbować tooautomatically wzrost hello woluminu. Jeśli w puli magazynu hello jest za mało miejsca, występuje błąd.

    W przypadku zmiany z ochrony stanu toosystem ochrony BMR, należy miejsca na powitania chronionego komputera. Jest tak, ponieważ Ochrona stanu systemu najpierw zapisuje hello komputera lokalnego toohello repliki, a następnie przekazuje ją toohello kopii zapasowej serwera.

## <a name="before-you-begin"></a>Przed rozpoczęciem

1.  **Wdrażanie serwera kopii zapasowej Azure**. Upewnij się, że Utwórz kopię zapasową serwera jest prawidłowo wdrożony. Aby uzyskać więcej informacji, zobacz:
    * [Wymagania systemowe dla serwera usługi Kopia zapasowa Azure](http://docs.microsoft.com/system-center/dpm/install-dpm#setup-prerequisites)
    * [Kopii zapasowej macierzy ochrony serwera](backup-mabs-protection-matrix.md)

2.  **Konfigurowanie magazynu**. Można przechowywać dane kopii zapasowej na dysku, na taśmie i w chmurze hello z platformy Azure. Aby uzyskać więcej informacji, zobacz [Przygotuj magazyn danych](https://docs.microsoft.com/system-center/dpm/plan-long-and-short-term-data-storage).

3.  **Skonfiguruj agenta ochrony hello**. Zainstaluj agenta ochrony hello na komputerze hello, który chcesz tooback zapasowe. Aby uzyskać więcej informacji, zobacz [agenta ochrony DPM hello Wdróż](http://docs.microsoft.com/system-center/dpm/deploy-dpm-protection-agent).

## <a name="back-up-system-state-and-bare-metal"></a>Wykonaj kopię zapasową stanu systemu i od zera
Konfigurowanie grupy ochrony zgodnie z opisem w [wdrażanie grup ochrony](http://docs.microsoft.com/system-center/dpm/create-dpm-protection-groups). Nie można włączyć ochrony BMR i systemu stanu dla hello sam komputer w różnych grupach. Po wybraniu funkcji BMR, stan systemu jest automatycznie włączone.


1.  Kreator tworzenia nowej grupy ochrony hello tooopen w hello konsoli administratora serwera kopii zapasowej, wybierz **ochrony** > **akcje** > **utworzyć ochrony Grupy**.

2.  Na powitania **wybierz typ grupy ochrony** wybierz **serwerów**, a następnie wybierz **dalej**.

3.  Na powitania **Wybierz członków grupy** strony, rozwiń hello komputera, a następnie wybierz opcję **BMR** lub **stanu systemu**.

    Należy pamiętać, że nie można chronić zarówno BMR i stanu systemu dla hello komputera znajdującego się w różnych grupach. Po wybraniu funkcji BMR, stan systemu jest automatycznie włączone. Aby uzyskać więcej informacji, zobacz [wdrażanie grup ochrony](http://docs.microsoft.com/system-center/dpm/create-dpm-protection-groups).

4.  Na powitania **wybierz metodę ochrony danych** wybierz sposób toohandle krótko- i długoterminowej kopii zapasowej. Tworzenie krótkoterminowej kopii zapasowej jest zawsze toodisk najpierw, hello opcji tworzenia kopii zapasowych z toohello dysku hello Azure w chmurze za pomocą usługi Kopia zapasowa Azure (krótkoterminowej lub długoterminowej). Alternatywne termin toolong chmura toohello kopii zapasowej jest tooset się długoterminowej kopii zapasowej tooa autonomiczny taśm lub urządzenia biblioteką taśm został podłączony tooBackup serwera.

5.  Na powitania **Wybierz cele krótkoterminowe** wybierz sposób tooback zapasowych terminu tooshort magazynu na dysku:
    1. Aby uzyskać **zakres przechowywania**, wybierz, jak długo mają tookeep hello danych na dysku. 
    2. Aby uzyskać **częstotliwość synchronizacji**, wybierz, jak często ma toorun przyrostowej kopii zapasowej toodisk. Jeśli nie chcesz tooset interwał wykonywania kopii zapasowej, można sprawdzić hello **zaraz przed punktem odzyskiwania** opcji. Utwórz kopię zapasową serwera zostanie uruchomiony ekspresowej pełnej kopii zapasowej, tuż przed każdym punktu odzyskiwania zaplanowano.

6.  Jeśli chcesz toostore danych na taśmie do przechowywania długoterminowego na powitania **Określ cele długoterminowe** wybierz, jak długo mają tookeep danych na taśmie (1 – 99 lat). 
    1. Aby uzyskać **częstotliwość wykonywania kopii zapasowych**, wybierz częstotliwość tworzenia kopii zapasowej tootape powinno być ono uruchomione. częstotliwość Hello opiera się na zakres przechowywania hello, wybrane:
        * Gdy hello zakres przechowywania wynosi 1 – 99 lat, możesz wybrać toooccur kopii zapasowych codziennie, co tydzień, co dwa tygodnie, miesięczne, co kwartał, co pół roku lub rocznego.
        * Gdy hello zakres przechowywania wynosi 1-11 miesięcy, możesz wybrać toooccur kopii zapasowych codziennie, co tydzień, co dwa tygodnie lub co miesiąc.
        * Jeśli hello zakres przechowywania wynosi 1 – 4 tygodnie, można wybrać toooccur kopii zapasowych codziennie lub co tydzień.

    2. Na powitania **szczegółów zaznacz taśmy i biblioteki** strona, wybierz hello toouse taśmy i biblioteki, oraz czy skompresowane i zaszyfrowanych danych.

7.  Na powitania **Przejrzyj przydział dysku** Przejrzyj hello magazynu puli miejsca na dysku przydzielonego dla grupy ochrony hello.

    1. **Całkowity rozmiar danych** hello rozmiar danych hello ma tooback w górę.
    2. **Udostępnione na serwerze kopii zapasowej Azure toobe miejsca na dysku** miejsca hello, zalecane dla grupy ochrony hello Utwórz kopię zapasową serwera. Utwórz kopię zapasową serwera wybiera hello idealne wolumin kopii zapasowej na podstawie ustawień hello. Jednak możesz edytować opcje tworzenia kopii zapasowej woluminu hello w **szczegóły alokacji dysku**. 
    3. W przypadku obciążeń w menu rozwijanym hello, wybierz preferowany hello magazynu. Zmiany wprowadzone zmiany wartości hello **całkowita ilość miejsca** i **wolnego miejsca w magazynie** w hello **dostępny Magazyn dyskowy** okienka. Underprovisioned miejsca jest hello ilości miejsca, Utwórz kopię zapasową serwera sugestią, dodać toohello woluminu, tooensure smooth kopii zapasowych.

8.  Na powitania **wybierz metodę tworzenia repliki** wybierz sposób toohandle hello początkowej pełnej replikacji danych. Jeśli wybierzesz tooreplicate za pośrednictwem sieci hello, zaleca się wybranie poza godzinami szczytu. W przypadku dużych ilości danych lub warunków sieciowych, które są optymalne należy wziąć pod uwagę replikowanie danych hello w trybie offline przy użyciu nośnika wymiennego.

9. Na powitania **wybierz opcje sprawdzania spójności** wybierz sposób tooautomate sprawdzenie spójności. Możesz toorun kontroli tylko wtedy, gdy dane repliki staje się niespójna, lub zgodnie z harmonogramem. Jeśli nie chcesz tooconfigure automatycznego sprawdzania spójności, można uruchomić sprawdzanie ręczne w dowolnym momencie. Sprawdzanie ręczne, w hello toorun **ochrony** obszaru hello konsoli administratora serwera kopii zapasowej, kliknij prawym przyciskiem myszy ochrona powitalnych grupy, a następnie wybierz **Przeprowadź Sprawdzanie spójności**.

10. Jeśli wybrano tooback się toohello chmury za pomocą usługi Kopia zapasowa Azure, na powitania **Określ dane chronione Online** strony, upewnij się, że wybrana hello zadania, które mają tooback się tooAzure.

11. Na powitania **Określanie harmonogramu tworzenia kopii zapasowej Online** wybierz częstotliwość przyrostowe kopie zapasowe tooAzure zostanie przeprowadzona. Można zaplanować tworzenie kopii zapasowych toorun każdego dnia, tygodnia, miesiąca i roku i wybierz hello Data i godzina na tym, które powinno być ono uruchomione. Tworzenie kopii zapasowych może wystąpić się tootwice dziennie. Kopii zapasowej, punkt odzyskiwania danych jest tworzony w Azure z hello kopii danych kopii zapasowej hello przechowywane na dysku, Utwórz kopię zapasową serwera hello.

12. Na powitania **Określanie zasad przechowywania Online** wybierz sposób hello punktów odzyskiwania, które są tworzone z kopii zapasowej codziennie, co tydzień, miesięcznych i rocznych hello są przechowywane na platformie Azure.

13. Na powitania **wybierz replikacji Online** wybierz sposób występuje hello Pełna replikacja początkowa danych. Można replikować za pośrednictwem sieci hello lub wykonaj w trybie offline kopii zapasowej (obsługi w trybie offline). Kopia zapasowa offline używa hello Azure importu funkcji. Aby uzyskać więcej informacji, zobacz [w trybie Offline kopii zapasowej przepływu pracy w usłudze Kopia zapasowa Azure](backup-azure-backup-import-export.md).

14. Na powitania **Podsumowanie** Przejrzyj ustawienia. Po wybraniu **Utwórz grupę**, następuje Replikacja początkowa danych hello. Po zakończeniu replikacji danych, na powitania **stan** strona, stan grupy ochrony hello jest **OK**. Kopia zapasowa następnie odbywa się na ochrona powitalnych ustawienia grupy.

## <a name="recover-system-state-or-bmr"></a>Odzyskiwanie stanu systemu lub odzyskiwania systemu od ZERA
Można odzyskać, lokalizacji sieciowej tooa stanu systemu lub odzyskiwania systemu od ZERA. Jeśli utworzono kopię zapasową BMR, użyj środowiska odzyskiwania systemu Windows (WinRE) toostart system i połącz go toohello sieci. Następnie należy użyć toorecover kopia zapasowa systemu Windows Server z lokalizacji sieciowej hello. Jeśli utworzono kopię zapasową stanu systemu, wystarczy użyć toorecover kopia zapasowa systemu Windows Server z lokalizacji sieciowej hello.

### <a name="restore-bmr"></a>Przywróć odzyskiwania systemu od ZERA
Uruchamianie odzyskiwania na powitania serwera kopii zapasowej komputera:

1.  W hello **odzyskiwania** okienka, Znajdź hello komputer toorecover, a następnie wybrać **odzyskiwaniu bez systemu operacyjnego**.

2.  Dostępne punkty odzyskiwania są pogrubione w kalendarzu hello. Wybierz hello datę i godzinę dla punktu odzyskiwania hello, które mają toouse.

3.  Na powitania **Wybieranie typu odzyskiwania** wybierz **folderu sieciowego tooa kopiowania.**

4.  Na powitania **określ miejsce docelowe** wybierz, gdzie chcesz toocopy hello dane. Należy pamiętać, że zaznaczone miejsce docelowe tego hello musi toohave wystarczająco dużo miejsca. Firma Microsoft zaleca, aby utworzyć nowy folder.

5.  Na powitania **Określanie opcji odzyskiwania** strony, tooapply ustawienia zabezpieczeń wybierz hello. Następnie wybierz, czy sieci magazynowania (SAN) toouse — na podstawie migawki sprzętowe szybciej odzyskiwać dane. (Jest to opcja tylko wtedy, gdy sieci SAN z tej funkcji, które są dostępne i hello toocreate możliwości i podziału toomake klonowania go zapisywalny. In Addition, hello komputera chronionego i serwera kopii zapasowej komputera musi być połączony toohello tej samej sieci.)

6.  Skonfiguruj opcje powiadamiania. Na powitania **potwierdzenie** wybierz pozycję **odzyskać**.

Skonfiguruj lokalizację udziału hello:

1.  W lokalizacji przywracania hello Przejdź toohello folderu, który ma hello kopii zapasowej.

2.  Udostępnij folder hello, który jest o jeden poziom wyżej WindowsImageBackup, tak aby hello głównym folderu udostępnionego hello jest hello WindowsImageBackup folder. Jeśli nie zrobisz, przywracania nie odnajdzie hello kopii zapasowej. tooconnect przy użyciu środowiska odzyskiwania systemu Windows (WinRE), należy udziału, w której będziesz mieć dostęp ze środowiska WinRE hello poprawny adres IP i poświadczeń.

Przywróć hello system:

1.  Start hello komputera, na którym ma toorestore hello obrazu przy użyciu dysku DVD systemu Windows hello dla systemu hello są przywracane.

2.  Na pierwszej stronie powitania Sprawdź ustawienia języka i ustawienia regionalne. Na powitania **zainstalować** wybierz pozycję **Napraw komputer**.

3.  Na powitania **opcje odzyskiwania systemu** wybierz pozycję **Przywróć komputer przy użyciu utworzonego wcześniej obrazu systemu**.

4.  Na powitania **Wybierz kopię zapasową obrazu systemu** wybierz **wybierz obraz systemu** > **zaawansowane** > **wyszukiwania dla systemu Obraz powitania sieci**. Jeśli zostanie wyświetlone ostrzeżenie, wybierz **tak**. Przejdź do ścieżki udziału toohello, wprowadź poświadczenia hello, a następnie wybierz punkt odzyskiwania hello. To skanowanie w poszukiwaniu określonych kopii zapasowych, które są dostępne w tym punkcie odzyskiwania. Wybierz punkt odzyskiwania hello, które mają toouse.

5.  Na powitania **wybrać sposób tworzenia kopii zapasowej hello toorestore** wybierz pozycję **Format i ponownie podziel na partycje dysków**. Na następnej stronie powitania Sprawdź ustawienia. 

6.  Przywracanie hello toobegin, wybierz opcję **Zakończ**. Wymagane jest ponowne uruchomienie.

### <a name="restore-system-state"></a>Przywracanie stanu systemu

Uruchom odzyskiwanie z kopii zapasowej serwera:

1.  W hello **odzyskiwania** okienku Znajdź hello komputer ma toorecover, a następnie wybierz **odzyskiwaniu bez systemu operacyjnego**.

2.  Dostępne punkty odzyskiwania są pogrubione w kalendarzu hello. Wybierz hello datę i godzinę dla punktu odzyskiwania hello, które mają toouse.

3.  Na powitania **Wybieranie typu odzyskiwania** wybierz **folderu sieciowego tooa kopiowania**.

4.  Na powitania **określ miejsce docelowe** wybierz, gdzie chcesz toocopy hello danych. Należy pamiętać, że wybranego miejsca docelowego tej hello musi wystarczająco dużo miejsca. Firma Microsoft zaleca, aby utworzyć nowy folder.

5.  Na powitania **Określanie opcji odzyskiwania** strony, tooapply ustawienia zabezpieczeń wybierz hello. Następnie wybierz, czy migawek sprzętowych opartych na sieci SAN toouse szybciej odzyskiwać dane. (Jest to opcja tylko wtedy, gdy sieci SAN z tej funkcji i hello toocreate możliwości i podziału toomake klonowania go zapisywalny. In Addition, hello komputerze chronionym i kopii zapasowej serwera musi być połączony toohello tej samej sieci.)

6.  Skonfiguruj opcje powiadamiania. Na powitania **potwierdzenie** wybierz pozycję **odzyskać**.

Uruchom narzędzie Kopia zapasowa systemu Windows Server:

1.  Wybierz **akcje** > **odzyskać** > **tego serwera** > **dalej**.

2.  Wybierz **innego serwera**, wybierz pozycję hello **Określ typ lokalizacji** , a następnie wybierz **zdalnego folderu udostępnionego**. Wprowadź hello ścieżki toohello folderu, który zawiera hello punktu odzyskiwania.

3.  Na powitania **Wybieranie typu odzyskiwania** wybierz **stanu systemu**. 

4. Na powitania **Wybieranie lokalizacji dla odzyskiwania stanu systemu** wybierz **oryginalnej lokalizacji**.

5.  Na powitania **potwierdzenie** wybierz pozycję **odzyskać**. Po przywróceniu hello Uruchom ponownie serwer hello.

6.  Można również uruchomić Przywracanie stanu systemu hello w wierszu polecenia. toodo tego uruchomienia narzędzia Kopia zapasowa systemu Windows Server na komputerze hello ma toorecover. Identyfikator wersji hello tooget, w wierszu polecenia, wpisz:```wbadmin get versions -backuptarget \<servername\sharename\>```

    Użyj identyfikatora wersji hello toostart Przywracanie stanu systemu hello. Witaj wiersza polecenia wpisz:```wbadmin start systemstaterecovery -version:<versionidentified> -backuptarget:<servername\sharename>```

    Upewnij się, że chcesz toostart hello odzyskiwania. Proces hello w oknie wiersza polecenia hello jest widoczny. Tworzony jest dziennik przywracania. Po przywróceniu hello Uruchom ponownie serwer hello.

