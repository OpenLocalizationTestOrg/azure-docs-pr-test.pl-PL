---
title: Seria aaaStorSimple 8000 jako miejsce docelowe kopii zapasowej z kopii zapasowej Exec | Dokumentacja firmy Microsoft
description: W tym artykule opisano hello StorSimple miejsce docelowe kopii zapasowej konfiguracji z kopii zapasowej Exec Veritas.
services: storsimple
documentationcenter: 
author: harshakirank
manager: matd
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/05/2016
ms.author: hkanna
ms.openlocfilehash: 270ad95e1f6b367e80048cad42beb936f205f69c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-as-a-backup-target-with-backup-exec"></a>StorSimple jako miejsce docelowe kopii zapasowej z kopii zapasowej Exec

## <a name="overview"></a>Omówienie

Azure StorSimple jest rozwiązania magazynu hybrydowego chmury firmy Microsoft. StorSimple adresy skomplikowane hello przyrostu wykładniczej danych przy użyciu konta magazynu platformy Azure jako rozszerzenia rozwiązania lokalnego hello i automatycznie warstw danych między lokalnymi magazynu i magazynu w chmurze.

W tym artykule omówiono StorSimple integracji z Veritas Backup Exec i najlepsze rozwiązania dotyczące integrowania oba rozwiązania. Możemy również zaleceń w sposób integrowania tooset zapasowych Backup Exec toobest z StorSimple. Firma Microsoft odroczenie tooVeritas najlepszych rozwiązań, tworzenia kopii zapasowej architektów i administratorów dla hello najlepsze sposób tooset Backup Exec toomeet indywidualnymi wymaganiami kopii zapasowej i umów dotyczących poziomu usług (SLA).

Mimo że firma Microsoft zilustrować czynności konfiguracyjne i podstawowe pojęcia, przewodnik krok po kroku konfiguracji lub instalacja jest w żadnym wypadku w tym artykule. Przyjęto założenie, że hello podstawowe składniki i infrastruktury znajdują się w stanie i gotowe toosupport hello pojęcia, które opisano.

### <a name="who-should-read-this"></a>Kto powinien przeczytać to?

Witaj informacje w tym artykule będzie najbardziej przydatne toobackup Administratorzy, administratorzy pamięci masowej i architektów magazynu, którzy korzystają z magazynu systemu Windows Server 2012 R2, Ethernet, usługi w chmurze i Exec kopii zapasowej.

## <a name="supported-versions"></a>Obsługiwane wersje

-   [Tworzenie kopii zapasowych Exec 16 i nowszych wersjach](http://backupexec.com/compatibility)
-   [StorSimple Update 3 i nowszych wersji](storsimple-overview.md#storsimple-workload-summary)


## <a name="why-storsimple-as-a-backup-target"></a>Dlaczego StorSimple jako miejsce docelowe kopii zapasowej?

StorSimple jest dobrym rozwiązaniem w przypadku miejsce docelowe kopii zapasowej, ponieważ:

-   Zapewnia on standardowe, lokalnego magazynu toouse aplikacjom kopii zapasowych jako protokół fast miejsce docelowe kopii zapasowej, bez wprowadzania żadnych zmian. Można też użyć StorSimple do szybkiego przywrócenia ostatnie kopii zapasowych.
-   Jego chmury warstwy jest w pełni zintegrowana z toouse konta magazynu Azure cloud ekonomicznego magazynowania Azure.
-   Udostępnia automatycznie przechowywania poza siedzibą odzyskiwania po awarii.

## <a name="key-concepts"></a>Kluczowe pojęcia

Podobnie jak w przypadku dowolnego pamięci masowej, zachować ostrożność podczas oceny wydajności magazynu hello rozwiązania, umów SLA, szybkość zmian i wymagań wzrost wydajności jest toosuccess krytyczne. główny pomysł Hello jest, że dzięki zastosowaniu warstwy chmury, chmury toohello godziny dostępu i produktywność odgrywają podstawowych rolę hello zdolności StorSimple toodo swojego zadania.

StorSimple jest zaprojektowana tooprovide tooapplications magazynu, które działają na dobrze zdefiniowany zestaw roboczy danych (gorących danych). W tym modelu zestaw roboczy hello danych są przechowywane w warstwach lokalne powitania i hello pozostałe wolne/chłodni/zarchiwizowane zestaw danych jest toohello warstwowych chmury. Ten model jest reprezentowany w powitania po rysunku. wiersz Hello niemal płaskiej zielony reprezentuje hello danych przechowywanych w warstwach lokalnych hello hello urządzenia StorSimple. Witaj czerwona linia reprezentuje hello łączną ilość danych przechowywanych na powitania rozwiązania StorSimple przez wszystkie warstwy. Witaj odstęp między hello płaskim zielony wiersza i hello krzywej red reprezentuje hello łączną ilość danych przechowywanych w chmurze hello.

**Obsługa poziomów StorSimple**
![StorSimple diagramów warstw](./media/storsimple-configure-backup-target-using-backup-exec/image1.jpg)

Taka architektura na uwadze znajdziesz czy StorSimple, jest idealnym rozwiązaniem toooperate jako miejsce docelowe kopii zapasowej. Możesz użyć StorSimple do:
-   Wykonaj z najczęściej wykonywanych operacji przywracania z hello lokalnego zestaw roboczy danych.
-   Użyj hello chmury odzyskiwania po awarii poza siedzibą firmy i starszych danych, gdzie są dłuższe interwały przywracania.

## <a name="storsimple-benefits"></a>Korzyści StorSimple

StorSimple zapewnia rozwiązanie lokalne, które jest w pełni zintegrowana z Microsoft Azure, dzięki wykorzystaniu bezproblemowy dostęp do lokalnych tooon i magazynu w chmurze.

StorSimple używa automatycznego tworzenia warstw między hello lokalnego urządzenia, którego urządzenia półprzewodnikowych (SSD) i magistrali serial attached SCSI (SAS) magazynu, a Magazyn Azure. Automatyczne warstw utrzymuje często używane dane lokalne na hello warstwy dysków SSD i dysków SAS. Powoduje przeniesienie tooAzure rzadko używane dane magazynu.

StorSimple oferuje następujące korzyści:

-   Unikatowy kompresji i deduplikacji algorytmów hello chmury tooachieve Niespotykana deduplikacji poziomy
-   Wysoka dostępność
-   Replikacja geograficzna przy użyciu platformy Azure — replikacja geograficzna
-   Integracja Azure
-   Szyfrowanie danych w chmurze hello
-   Ulepszonych funkcji odzyskiwania i zgodność

Chociaż StorSimple zasadniczo przedstawia dwa scenariusze wdrażania głównego (miejsce docelowe kopii zapasowej głównej i dodatkowej miejsce docelowe kopii zapasowej), jest zwykły, urządzeniem magazynu blokowego. StorSimple wszystkie hello kompresji i deduplikacji. Bezproblemowo wysyła i pobiera dane między chmurą hello i aplikacji hello i systemie plików.

Aby uzyskać więcej informacji o StorSimple, zobacz [z serii StorSimple 8000: rozwiązanie magazynu w chmurze hybrydowej](storsimple-overview.md). Ponadto można przejrzeć hello [techniczne serii StorSimple 8000](storsimple-technical-specifications-and-compliance.md).

> [!IMPORTANT]
> Używanie StorSimple urządzenia jako miejsce docelowe kopii zapasowej jest obsługiwane tylko w przypadku StorSimple 8000 z aktualizacją Update 3 i nowszych wersjach.

## <a name="architecture-overview"></a>Omówienie architektury

Witaj poniższych tabelach przedstawiono wskazówki dotyczące hello urządzeń modelu do architektury początkowej.

**Możliwości StorSimple dla lokalnych i magazynu w chmurze**

| Pojemność magazynu       | 8100          | 8600            |
|------------------------|---------------|-----------------|
| Pojemność magazynu lokalnego | &lt;10 TiB\*  | &lt;20 TiB\*  |
| Pojemność magazynu w chmurze | &gt;200 TiB\* | &gt;500 TiB\* |
\*Rozmiar magazynu nie przyjmuje żadnych deduplikacji ani kompresji.

**StorSimple pojemności dla głównych i dodatkowych kopii zapasowych**

| Scenariusz tworzenia kopii zapasowej  | Pojemność magazynu lokalnego  | Pojemność magazynu w chmurze  |
|---|---|---|
| Podstawowa kopia zapasowa  | Ostatnie kopie zapasowe przechowywane w magazynie lokalnym na szybkie odzyskiwanie toomeet cel punktu odzyskiwania (RPO) | Historia kopii zapasowych (RPO), który pasuje do pojemności chmury |
| Dodatkowej kopii zapasowej | Dodatkowej kopii kopii zapasowej danych mogą być przechowywane w chmurze pojemności  | Nie dotyczy  |

## <a name="storsimple-as-a-primary-backup-target"></a>StorSimple jako miejsce docelowe kopii zapasowej głównej

W tym scenariuszu woluminów StorSimple są prezentowane toohello aplikacji kopii zapasowej jako jedynego repozytorium hello kopii zapasowych. powitania po rysunek przedstawia architektury rozwiązania, w którym wszystkie kopie zapasowe Użyj StorSimple warstwowej woluminów na potrzeby tworzenia kopii zapasowych i przywracania.

![StorSimple jako miejsce docelowe kopii zapasowej głównej diagram logiczny](./media/storsimple-configure-backup-target-using-backup-exec/primarybackuptargetlogicaldiagram.png)

### <a name="primary-target-backup-logical-steps"></a>Etapy logiczne kopii zapasowej głównej docelowej

1.  Kontakty Utwórz kopię zapasową serwera Hello hello docelowego agenta kopii zapasowej, a agent usługi Kopia zapasowa hello przesyła dane toohello Utwórz kopię zapasową serwera.
2.  Utwórz kopię zapasową serwera Hello zapisuje dane woluminami warstwowymi toohello StorSimple.
3.  Witaj, Utwórz kopię zapasową serwera aktualizuje bazę danych katalogu hello, a następnie kończy zadanie tworzenia kopii zapasowej hello.
4.  Skrypt migawki wyzwala hello chmury migawki Menedżer StorSimple (start lub usunięcie).
5.  Utwórz kopię zapasową serwera Hello Usuwa wygasłe kopii zapasowych na podstawie zasad przechowywania.


### <a name="primary-target-restore-logical-steps"></a>Etapy logiczne przywracania głównej docelowej

1.  Witaj, Utwórz kopię zapasową serwera uruchamia przywracania hello odpowiednie dane z repozytorium magazynu hello.
2.  agent usługi Kopia zapasowa Hello odbiera dane hello z hello kopii zapasowej serwera.
3.  Serwer kopii zapasowej Hello zakończy hello zadanie przywracania.

## <a name="storsimple-as-a-secondary-backup-target"></a>StorSimple jako dodatkowej miejsce docelowe kopii zapasowej

W tym scenariuszu woluminów StorSimple głównie służą do przechowywania długoterminowego i archiwizacji.

Witaj poniższej ilustracji przedstawiono architekturę, w których początkowej kopii zapasowych i przywraca wolumin docelowy wysokiej wydajności. Te kopie zapasowe są kopiowane i archiwizowane tooa StorSimple do warstwy woluminu zgodnie z ustalonym harmonogramem.

Jego jest ważne toosize woluminu wysokiej wydajności, dzięki czemu może obsłużyć zasad przechowywania wymagań pojemność i wydajność.

![StorSimple jako miejsce docelowe kopii zapasowej dodatkowej diagram logiczny](./media/storsimple-configure-backup-target-using-backup-exec/secondarybackuptargetlogicaldiagram.png)

### <a name="secondary-target-backup-logical-steps"></a>Dodatkowej docelowy kopii zapasowej etapy logiczne

1.  Kontakty Utwórz kopię zapasową serwera Hello hello docelowego agenta kopii zapasowej, a agent usługi Kopia zapasowa hello przesyła dane toohello Utwórz kopię zapasową serwera.
2.  Utwórz kopię zapasową serwera Hello zapisuje toohigh wydajności pamięci masowej.
3.  Witaj, Utwórz kopię zapasową serwera aktualizuje bazę danych katalogu hello, a następnie kończy zadanie tworzenia kopii zapasowej hello.
4.  Utwórz kopię zapasową serwera Hello kopiuje tooStorSimple kopii zapasowych na podstawie zasad przechowywania.
5.  Skrypt migawki wyzwala hello chmury migawki Menedżer StorSimple (start lub usunięcie).
6.  Utwórz kopię zapasową serwera Hello Usuwa wygasłe kopii zapasowych na podstawie zasad przechowywania.

### <a name="secondary-target-restore-logical-steps"></a>Etapy logiczne przywracania dodatkowej docelowego

1.  Witaj, Utwórz kopię zapasową serwera uruchamia przywracania hello odpowiednie dane z repozytorium magazynu hello.
2.  agent usługi Kopia zapasowa Hello odbiera dane hello z hello kopii zapasowej serwera.
3.  Serwer kopii zapasowej Hello zakończy hello zadanie przywracania.

## <a name="deploy-hello-solution"></a>Wdrażanie rozwiązania hello

Wdrażanie rozwiązania hello wymaga trzy kroki:
1. Przygotowanie infrastruktury sieci hello.
2. Wdrażanie urządzenia StorSimple jako miejsce docelowe kopii zapasowej.
3. Wdróż Exec kopii zapasowej.

Każdy krok została omówiona szczegółowo w hello następujące sekcje.

### <a name="set-up-hello-network"></a>Konfigurowanie sieci hello

Ponieważ StorSimple to rozwiązanie, które jest zintegrowany z hello chmury Azure, StorSimple wymaga toohello active i pracy połączenia chmury Azure. To połączenie jest używana do operacje, takie jak migawki w chmurze, zarządzania, transfer metadanych i magazynu w chmurze tooAzure tootier starszej, mniej używanych danych.

Tooperform rozwiązania hello optymalnie, zaleca się przestrzeganie tych sieci najlepsze rozwiązania:

-   Hello łącza, które łączy z warstw tooAzure StorSimple musi spełniać wymagania przepustowości. tooachieve, zastosuj hello niezbędne jakości usług (QoS) poziomu tooyour infrastruktury przełączników toomatch Twojego RPO i odzyskiwania czasu SLA cel (RTO).
-   Maksymalna opóźnienia dostępu do magazynu obiektów Blob platformy Azure powinna być około 80 ms.

### <a name="deploy-storsimple"></a>Wdrażanie StorSimple

Aby uzyskać szczegółowe instrukcje wdrożenia StorSimple, zobacz [wdrażanie lokalnego urządzenia StorSimple](storsimple-deployment-walkthrough-u2.md).

### <a name="deploy-backup-exec"></a>Wdrażanie Exec kopii zapasowej

Dla kopii zapasowej Exec najlepsze rozwiązania dotyczące instalacji, zobacz [najlepszych rozwiązań dotyczących instalacji Backup Exec](https://www.veritas.com/support/en_US/article.000068207).

## <a name="set-up-hello-solution"></a>Konfigurowanie rozwiązania hello

W tej sekcji przedstawiony przykłady konfiguracji. Witaj następujące przykłady i zalecenia ilustrują hello najbardziej podstawowa i podstawowych implementacji. Ta implementacja może nie mieć zastosowania bezpośrednio tooyour specyficznych wymagań kopii zapasowej.

### <a name="set-up-storsimple"></a>Konfigurowanie StorSimple

| Zadania wdrażania StorSimple  | Dodatkowe uwagi |
|---|---|
| Wdrażanie lokalnego urządzenia StorSimple. | Obsługiwane wersje: Aktualizacja 3 i jego nowsze wersje. |
| Włącz hello miejsce docelowe kopii zapasowej. | Użyj tych tooturn poleceń na lub wyłącz tryb miejsce docelowe kopii zapasowej i stan tooget. Aby uzyskać więcej informacji, zobacz [połączyć się zdalnie urządzenia StorSimple tooa](storsimple-remote-connect.md).</br> tooturn na tryb tworzenia kopii zapasowych: `Set-HCSBackupApplianceMode -enable`. </br> tooturn off trybu tworzenia kopii zapasowych: `Set-HCSBackupApplianceMode -disable`. </br> bieżący stan hello tooget ustawień trybu tworzenia kopii zapasowych: `Get-HCSBackupApplianceMode`. |
| Utwórz kontener woluminów typowe dla woluminu, który przechowuje dane kopii zapasowej hello. Wszystkie dane w kontenerze wolumin jest deduplikowany. | Kontenery woluminów StorSimple Definiowanie domen deduplikacji.  |
| Utwórz woluminy StorSimple. | Utwórz woluminy o rozmiarze jako Zamknij toohello zakładano użycia, jak to możliwe, ponieważ chmura migawki czas trwania wpływa na rozmiar woluminu. Aby uzyskać informacje na temat toosize woluminu, przeczytaj o [zasady przechowywania](#retention-policies).</br> </br> Użyj StorSimple do warstwy woluminy i wybierz hello **Użyj tego woluminu w przypadku rzadziej używanych danych archiwalnych** pole wyboru. </br> Używanie tylko przypięty lokalnie woluminów nie jest obsługiwane. |
| Utwórz unikatowy StorSimple zasady tworzenia kopii zapasowych wszystkich woluminów miejsce docelowe kopii zapasowej hello. | Zasady tworzenia kopii zapasowej StorSimple definiuje hello woluminu spójności grupy. |
| Wyłącz harmonogram hello jako migawki hello wygaśnie. | Migawki są wyzwalane jako operację przetwarzania końcowego. |

### <a name="set-up-hello-host-backup-server-storage"></a>Konfigurowanie magazynu kopii zapasowej serwera hosta hello

Konfigurowanie magazynu kopii zapasowej serwera hosta hello zgodnie z wytycznymi toothese:  

- Nie używaj woluminy łączone (utworzonego przez Zarządzanie dyskami systemu Windows). Dyski łączone nie są obsługiwane.
- Formatowanie woluminów o rozmiarze 64 KB alokacji w systemie plików NTFS.
- Mapuje woluminy StorSimple hello bezpośrednio toohello Exec kopii zapasowej serwera.
    - Użyj iSCSI dla serwerów fizycznych.
    - Dyski przekazujące na użytek serwerów wirtualnych.

## <a name="best-practices-for-storsimple-and-backup-exec"></a>Najlepsze rozwiązania dotyczące StorSimple i Exec kopii zapasowej

Konfigurowanie rozwiązania zgodnie z wytycznymi toohello w hello następujące sekcje.

### <a name="operating-system-best-practices"></a>Najlepsze rozwiązania w zakresie systemu operacyjnego

-   Wyłącz szyfrowanie systemu Windows Server i deduplikacji systemu plików NTFS hello.
-   Wyłącz defragmentacji systemu Windows Server na powitania woluminów StorSimple.
-   Wyłącz indeksowanie na powitania woluminów StorSimple w systemie Windows Server.
-   Uruchom skanowanie za pomocą oprogramowania antywirusowego na hoście źródłowym hello (nie dla woluminów StorSimple hello).
-   Wyłącz domyślne hello [konserwacji systemu Windows Server](https://msdn.microsoft.com/library/windows/desktop/hh848037.aspx) w Menedżerze zadań. Wykonaj następujące czynności w jednym z hello następujące sposoby:
   - Wyłącz hello konfiguratora konserwacji w harmonogramu zadań systemu Windows.
   - Pobierz [PsExec](https://technet.microsoft.com/sysinternals/bb897553.aspx) Windows Sysinternals. Po pobraniu narzędzia PsExec, uruchom program Azure PowerShell jako administrator i wpisz:
      ```powershell
      psexec \\%computername% -s schtasks /change /tn “MicrosoftWindowsTaskSchedulerMaintenance Configurator" /disable
      ```

### <a name="storsimple-best-practices"></a>Najlepsze rozwiązania StorSimple

  -   Pamiętaj, że urządzenia StorSimple hello jest aktualizowany za[aktualizacji 3 lub nowszym](storsimple-install-update-3.md).
  -   Odizolowanego ruchu iSCSI i chmury. Użyj iSCSI dedykowanych połączeń dla ruchu między StorSimple i hello Utwórz kopię zapasową serwera.
  -   Pamiętaj, że urządzenie StorSimple jest dedykowany miejsce docelowe kopii zapasowej. Mieszane obciążeń nie są obsługiwane, ponieważ wpływają na Twoje RTO i cel punktu odzyskiwania.

### <a name="backup-exec-best-practices"></a>Kopia zapasowa Exec najlepszych rozwiązań.

-   Exec kopii zapasowej musi być zainstalowany na lokalnym dysku powitania serwera, a nie na woluminu StorSimple.
-   Ustaw magazynu kopii zapasowej Exec hello **równoczesnych operacji zapisu** toohello maksymalny dozwolony.
    -   Ustaw magazynu kopii zapasowej Exec hello **rozmiar bloku i buforu** too512 KB.
    -   Włączanie magazynu kopii zapasowej Exec **buforowane Odczyt i zapis**.
-   StorSimple obsługuje Backup Exec pełne i przyrostowe kopie zapasowe. Zaleca się nie używać syntetyczne i różnicowych kopii zapasowych.
-   Plik kopii zapasowej danych powinien zawierać tylko dane dotyczące określonego zadania. Na przykład dołącza bez nośnika przez różne zadania są dozwolone.
-   Wyłącz zadanie weryfikacji. W razie potrzeby weryfikacji powinny zostać zaplanowane po hello najnowszego zadania tworzenia kopii zapasowej. Jest ważne toounderstand, że to zadanie dotyczy kopii zapasowych.
-   Wybierz **magazynu** > **dysku** > **szczegóły** > **właściwości**. Wyłącz **wstępnie przydzielić miejsca na dysku**.

Aby uzyskać najnowsze ustawienia kopii zapasowej Exec hello i najlepsze rozwiązania dotyczące wdrażania tych wymagań, zobacz [hello Veritas witryny sieci Web](https://www.veritas.com).

## <a name="retention-policies"></a>Zasady przechowywania

Jeden z typów zasad przechowywania kopii zapasowych najczęściej hello są to zasady dziadek, ojciec i syn (GFS). W zasadzie GFS przyrostowej kopii zapasowej jest wykonywane codziennie i pełne kopie zapasowe są wykonywane co tydzień i co miesiąc. Powoduje to zasady sześć StorSimple woluminami warstwowymi. Jeden wolumin zawiera pełne kopie zapasowe hello co tydzień, miesięcznych i rocznych. Witaj inne woluminy pięć przechowywania codziennych przyrostowych kopii zapasowych.

Poniższy przykład hello używamy obrotu GFS. przykład Witaj założono hello następujące czynności:

-   Deduplikacją nie lub skompresowane dane są używane.
-   Pełne kopie zapasowe są 1 TiB.
-   Codzienne przyrostowe kopie zapasowe są 500 GiB.
-   Cztery cotygodniowe kopie zapasowe są przechowywane przez miesiąc.
-   Dwanaście comiesięczne kopie zapasowe są przechowywane przez rok.
-   Jeden corocznej kopii zapasowej jest przechowywana na 10 lat.

Oparte na powitania poprzedzających założeń, Utwórz 26-TiB pełne kopie zapasowe hello miesięcznych i rocznych wolumin warstwowy StorSimple. Tworzenie 5-TiB StorSimple do warstwy woluminu dla każdego hello przyrostowych codziennych kopii zapasowych.

| Typ kopii zapasowej przechowywania | Rozmiar (TiB) | Mnożnik GFS\* | Łączna pojemność (TiB)  |
|---|---|---|---|
| Pełne co tydzień | 1 | 4  | 4 |
| Codzienne przyrostowe | 0.5 | 20 (cykle równy liczbie tygodni miesięcznie) | 12 (2 dla dodatkowych przydziału) |
| Miesięczne pełny | 1 | 12 | 12 |
| Pełne roczne | 1  | 10 | 10 |
| Wymaganie GFS |   | 38 |   |
| Dodatkowego limitu przydziału  | 4  |   | 42 całkowita wymaganie GFS  |
\*Witaj GFS mnożnik jest hello liczba kopii musi tooprotect i zachować toomeet wymagań zasad tworzenia kopii zapasowej.

## <a name="set-up-backup-exec-storage"></a>Konfigurowanie magazynu kopii zapasowej Exec

### <a name="tooset-up-backup-exec-storage"></a>tooset magazynie Exec kopii zapasowej

1.  W konsoli zarządzania Backup Exec hello, wybierz **magazynu** > **konfigurowania magazynu** > **Magazyn dyskowy**  >   **Następny**.

    ![Kopia zapasowa Exec konsoli zarządzania, skonfiguruj strony składowania](./media/storsimple-configure-backup-target-using-backup-exec/image4.png)

2.  Wybierz **Magazyn dyskowy**, a następnie wybierz **dalej**.

    ![Konsola zarządzania Exec kopii zapasowej, strony wybierz magazynu](./media/storsimple-configure-backup-target-using-backup-exec/image5.png)

3.  Na przykład, wprowadź nazwę reprezentatywny **sobota pełna**oraz opis. Wybierz **dalej**.

    ![Kopii zapasowej Exec management console, nazwę i opis strony](./media/storsimple-configure-backup-target-using-backup-exec/image7.png)

4.  Wybierz hello dysku, gdzie chcesz toocreate hello dysku magazynu urządzenie, a następnie wybierz **dalej**.

    ![Konsola zarządzania Exec kopii zapasowej, strona wyboru dysku magazynu](./media/storsimple-configure-backup-target-using-backup-exec/image9.png)

5.  Zwiększenie zbyt hello liczbę operacji zapisu**16**, a następnie wybierz **dalej**.

    ![Kopia zapasowa Exec konsoli zarządzania równoczesnych zapisu operacji ustawienia strony](./media/storsimple-configure-backup-target-using-backup-exec/image10.png)

6.  Przejrzyj ustawienia hello, a następnie wybierz **Zakończ**.

    ![Konsola zarządzania Exec kopii zapasowej, strona podsumowania konfiguracji magazynu](./media/storsimple-configure-backup-target-using-backup-exec/image11.png)

7.  Na końcu hello przypisanie poszczególnych woluminów, zmień hello magazynu urządzenia ustawienia toomatch tych zalecane w [najlepsze rozwiązania dotyczące StorSimple i Backup Exec](#best-practices-for-storsimple-and-backup-exec).

    ![Konsola zarządzania Exec kopii zapasowej, strony ustawień urządzenia pamięci masowej](./media/storsimple-configure-backup-target-using-backup-exec/image12.png)

8.  Powtórz kroki od 1 do 7, aż zakończysz przypisywanie sieci tooBackup woluminów StorSimple Exec.

## <a name="set-up-storsimple-as-a-primary-backup-target"></a>Konfigurowanie StorSimple jako miejsce docelowe kopii zapasowej głównej

> [!NOTE]
> Przywróć dane z kopii zapasowej, która została chmury warstwowych toohello występuje szybkością chmury.

Witaj poniższej ilustracji przedstawiono mapowanie hello typowe woluminu tooa zadania tworzenia kopii zapasowej. W takim przypadku wszystkie cotygodniowe kopie zapasowe hello mapy toohello sobota zapełniony dysk, a przyrostowe kopie zapasowe hello mapowania dysków przyrostowe tooMonday piątek. Witaj wszystkich kopii zapasowych i przywracania są z StorSimple do warstwy woluminu.

![Diagram logiczny konfiguracji podstawowej miejsce docelowe kopii zapasowej](./media/storsimple-configure-backup-target-using-backup-exec/primarybackuptargetdiagram.png)

### <a name="storsimple-as-a-primary-backup-target-gfs-schedule-example"></a>Przykład zaplanować StorSimple jako miejsce docelowe kopii zapasowej głównej GFS

Oto przykład harmonogramu obrotu GFS cztery tygodnie miesięcznych i rocznych:

| Typ częstotliwości lub tworzenia kopii zapasowej | Pełne | Przyrostowe (1-5 dni)  |   
|---|---|---|
| Co tydzień (1 – 4 tygodnie) | Sobota | Poniedziałek — piątek |
| Miesięczne  | Sobota  |   |
| Co rok | Sobota  |   |   |


### <a name="assign-storsimple-volumes-tooa-backup-exec-backup-job"></a>Przypisz zadanie tworzenia kopii zapasowej Backup Exec tooa woluminów StorSimple

Witaj następująca sekwencja przyjęto założenie, że ten host docelowy Exec kopii zapasowej i hello są skonfigurowane zgodnie z wytycznymi agenta kopii zapasowej Exec hello.

#### <a name="tooassign-storsimple-volumes-tooa-backup-exec-backup-job"></a>tooassign StorSimple woluminów tooa Backup Exec kopii zapasowej zadania

1.  W konsoli zarządzania Backup Exec hello, wybierz **hosta** > **kopii zapasowej** > **tooDisk kopii zapasowej**.

    ![Kopia zapasowa Exec konsoli zarządzania, wybierz hosta, toodisk i kopii zapasowej](./media/storsimple-configure-backup-target-using-backup-exec/image14.png)

2.  W hello **kopii zapasowych: właściwości definicji** okna dialogowego, w obszarze **kopii zapasowej**, wybierz pozycję **Edytuj**.

    ![Konsola zarządzania Exec kopii zapasowej, okno dialogowe Właściwości definicji kopii zapasowej](./media/storsimple-configure-backup-target-using-backup-exec/image15.png)

3.  Skonfiguruj kopie zapasowe pełne i przyrostowe, aby mogli zgodnie z wymaganiami RPO i RTO i jest zgodna z tooVeritas najlepszych rozwiązań.

4.  W hello **opcje kopii zapasowej** okno dialogowe, wybierz opcję **magazynu**.

    ![Konsola zarządzania Exec kopii zapasowej, okno dialogowe Opcje usługi Magazyn kopii zapasowych](./media/storsimple-configure-backup-target-using-backup-exec/image16.png)

5.  Przypisz odpowiedni StorSimple woluminów tooyour harmonogram tworzenia kopii zapasowych.

    > [!NOTE]
    > **Kompresja** i **typ szyfrowania** są ustawiane za**Brak**.

6.  W obszarze **Sprawdź**, wybierz pozycję hello **nie sprawdzaj poprawności danych dla tego zadania** pole wyboru. Użycie tej opcji może wpłynąć na obsługę poziomów StorSimple.

    > [!NOTE]
    > Defragmentacji, indeksowanie i weryfikacji tła negatywnie wpłynąć na powitania StorSimple warstwy.

    ![Konsola zarządzania Exec kopii zapasowej, opcje kopii zapasowej, sprawdź ustawienia](./media/storsimple-configure-backup-target-using-backup-exec/image17.png)

7.  Po skonfigurowaniu hello reszty toomeet Twojego opcje tworzenia kopii zapasowej z wymaganiami, wybierz **OK** toofinish.

## <a name="set-up-storsimple-as-a-secondary-backup-target"></a>Konfigurowanie StorSimple jako dodatkowej miejsce docelowe kopii zapasowej

> [!NOTE]
>Przywraca dane z kopii zapasowej, która została chmury warstwowych toohello wystąpić szybkością chmury.

W tym modelu musi mieć tooserve nośnika (inne niż StorSimple) magazynu jako tymczasowy pamięci podręcznej. Na przykład można użyć dublowanej macierzy niezależnych dysków (RAID) wolumin tooaccommodate miejsca, wejścia/wyjścia (We/Wy) i przepustowości. Firma Microsoft zaleca używanie RAID 5, 50 i 10.

Witaj rysunku poniżej przedstawiono typowe krótkoterminowego przechowywania lokalnego (toohello serwera) woluminy i długoterminowego przechowywania archiwa woluminów. W tym scenariuszu wszystkie kopie zapasowe uruchamiane na lokalne powitania (serwer toohello) woluminu RAID. Te kopie zapasowe są okresowo zduplikowane i archiwizowane tooan archiwa woluminu. Jego jest ważne toosize lokalne (serwer toohello) woluminu RAID, dzięki czemu może obsłużyć krótkoterminowego przechowywania pojemność i wydajność wymagań.

### <a name="storsimple-as-a-secondary-backup-target-gfs-example"></a>StorSimple jako przykład GFS dodatkowej miejsce docelowe kopii zapasowej

![StorSimple jako miejsce docelowe kopii zapasowej dodatkowej diagram logiczny](./media/storsimple-configure-backup-target-using-backup-exec/secondarybackuptargetdiagram.png)

Witaj poniższej tabeli przedstawiono sposób tooset się toorun kopii zapasowych na lokalne powitania i dyski StorSimple. Zawiera wymagania dotyczące poszczególnych i całkowitej pojemności.

### <a name="backup-configuration-and-capacity-requirements"></a>Wymagania dotyczące pojemności i konfiguracji kopii zapasowej

| Typ kopii zapasowej i przechowywania | Skonfigurowany magazyn | Rozmiar (TiB) | Mnożnik GFS | Łączna pojemność\* (TiB) |
|---|---|---|---|---|
| Tydzień, 1 (pełne i przyrostowe) |Dysk lokalny (krótkoterminowych)| 1 | 1 | 1 |
| Tygodnie StorSimple 2-4 |Dysk StorSimple (długoterminowej) | 1 | 4 | 4 |
| Miesięczne pełny |Dysk StorSimple (długoterminowej) | 1 | 12 | 12 |
| Pełne roczne |Dysk StorSimple (długoterminowej) | 1 | 1 | 1 |
|Wymagany rozmiar woluminów GFS |  |  |  | 18*|
\*Łączna pojemność obejmuje 17 dyski TiB StorSimple i 1 TiB woluminu RAID.


### <a name="gfs-example-schedule-gfs-rotation-weekly-monthly-and-yearly-schedule"></a>Harmonogram przykład GFS: obracanie GFS harmonogram tygodniowy, miesięcznych i rocznych

| Tydzień | Pełne | Przyrostowe dnia 1 | Dzień przyrostowe 2 | Dzień przyrostowe 3 | Dzień przyrostowe 4 | Dzień przyrostowe 5 |
|---|---|---|---|---|---|---|
| 1 tydzień | Lokalne woluminu RAID  | Lokalne woluminu RAID | Lokalne woluminu RAID | Lokalne woluminu RAID | Lokalne woluminu RAID | Lokalne woluminu RAID |
| Tydzień 2 | Tygodnie StorSimple 2-4 |   |   |   |   |   |
| Tydzień 3 | Tygodnie StorSimple 2-4 |   |   |   |   |   |
| Tydzień 4 | Tygodnie StorSimple 2-4 |   |   |   |   |   |
| Miesięczne | Co miesiąc StorSimple |   |   |   |   |   |
| Co rok | Co rok StorSimple  |   |   |   |   |   |   |


### <a name="assign-storsimple-volumes-tooa-backup-exec-archive-and-deduplication-job"></a>Przypisz StorSimple woluminów tooa Backup Exec archiwum i deduplikacji zadania

#### <a name="tooassign-storsimple-volumes-tooa-backup-exec-archive-and-duplication-job"></a>tooassign StorSimple woluminów tooa Backup Exec archiwum i powielania zadania

1.  W konsoli zarządzania Backup Exec hello, kliknij prawym przyciskiem myszy zadanie hello mają woluminu StorSimple tooa tooarchive, a następnie wybierz **kopii zapasowych: właściwości definicji** > **Edytuj**.

    ![Konsola zarządzania Exec kopii zapasowej, karta Właściwości definicji kopii zapasowej](./media/storsimple-configure-backup-target-using-backup-exec/image19.png)

2.  Wybierz **Dodaj etap** > **zduplikowane tooDisk** > **Edytuj**.

    ![Kopia zapasowa konsoli zarządzania Exec, Dodaj etap](./media/storsimple-configure-backup-target-using-backup-exec/image20.png)

3.  W hello **zduplikowane opcje** okno dialogowe, wybierz hello wartości, które mają toouse dla **źródła** i **harmonogram**.

    ![Tworzenie kopii zapasowych Exec konsoli zarządzania, tworzenia kopii zapasowej definicji właściwości i opcje zduplikowane](./media/storsimple-configure-backup-target-using-backup-exec/image21.png)

4.  W hello **magazynu** listy rozwijanej, wybierz hello woluminu StorSimple, w którym ma hello archiwum zadania toostore hello danych.

    ![Tworzenie kopii zapasowych Exec konsoli zarządzania, tworzenia kopii zapasowej definicji właściwości i opcje zduplikowane](./media/storsimple-configure-backup-target-using-backup-exec/image22.png)

5.  Wybierz **Sprawdź**, a następnie wybierz hello **nie sprawdzaj poprawności danych dla tego zadania** pole wyboru.

    ![Tworzenie kopii zapasowych Exec konsoli zarządzania, tworzenia kopii zapasowej definicji właściwości i opcje zduplikowane](./media/storsimple-configure-backup-target-using-backup-exec/image23.png)

6.  Kliknij przycisk **OK**.

    ![Tworzenie kopii zapasowych Exec konsoli zarządzania, tworzenia kopii zapasowej definicji właściwości i opcje zduplikowane](./media/storsimple-configure-backup-target-using-backup-exec/image24.png)

7.  W hello **kopii zapasowej** kolumny, Dodaj nowy etap. Dla źródła hello, użyj **przyrostowe**. Dla celu hello wybierz hello woluminu StorSimple, gdzie hello zadanie tworzenia przyrostowej kopii zapasowej zostaną zarchiwizowane. Powtórz kroki od 1 do 6.

## <a name="storsimple-cloud-snapshots"></a>Migawki StorSimple w chmurze

Migawki StorSimple w chmurze w ochronie danych hello, która znajduje się w urządzeniu StorSimple. Tworzenie migawka w chmurze jest równoważne tooshipping lokalnej kopii zapasowej taśmy tooan poza siedzibą firmy zakładzie. Użycie magazynu geograficznie nadmiarowego Azure, jest utworzenie migawkę chmury odpowiednik tooshipping taśm kopii zapasowych toomultiple witryn. Jeśli potrzebujesz toorestore urządzenia po awarii może doprowadzić online innego urządzenia StorSimple i tryb failover. Po hello w tryb failover będzie możliwe tooaccess hello danych (szybkością chmury) z hello najnowszych migawka w chmurze.

powitania po sekcji opisano, jak toocreate toostart krótkich skryptu i delete StorSimple w chmurze migawki podczas tworzenia kopii zapasowej przetwarzania końcowego.

> [!NOTE]
> Migawki tworzone ręcznie lub programowo nie wykonuj hello StorSimple snapshot wygaśnięcia zasad. Te migawki, należy ręcznie lub programowo usunąć.

### <a name="start-and-delete-cloud-snapshots-by-using-a-script"></a>Uruchom i Usuń migawki w chmurze za pomocą skryptu

> [!NOTE]
> Dokładnie oceń hello zgodności i następstwa przechowywania danych przed usunięciem migawki StorSimple. Aby uzyskać więcej informacji o tym, jak toorun skryptu po wykonaniu kopii zapasowej, zobacz hello [dokumentacji Backup Exec](https://www.veritas.com/support/en_US/15047.html).

### <a name="backup-lifecycle"></a>Cykl życia tworzenia kopii zapasowej

![Diagram cyklu życia tworzenia kopii zapasowej](./media/storsimple-configure-backup-target-using-backup-exec/backuplifecycle.png)

### <a name="requirements"></a>Wymagania

-   powitania serwera, który uruchamia skrypt hello musi mieć dostęp do zasobów w chmurze tooAzure.
-   Witaj, konto użytkownika musi mieć hello niezbędne uprawnienia.
-   Zasady tworzenia kopii zapasowej StorSimple z hello skojarzone StorSimple woluminów musi być zdefiniowane, ale nie jest włączona.
-   Będziesz potrzebować hello Nazwa zasobu StorSimple, klucz rejestracji, nazwa urządzenia i identyfikator zasad tworzenia kopii zapasowej.

### <a name="toostart-or-delete-a-cloud-snapshot"></a>toostart lub usuń migawka w chmurze

1.  [Zainstalowanie programu Azure PowerShell](/powershell/azure/overview).
2.  [Pobieranie i importowanie publikowania ustawienia i informacje o subskrypcji](https://msdn.microsoft.com/library/dn385850.aspx).
3.  W hello klasycznego portalu Azure, uzyskać nazwę zasobu hello i [klucz rejestracji usługi Menedżer StorSimple](storsimple-deployment-walkthrough-u2.md#step-2-get-the-service-registration-key).
4.  Na powitania serwera, który uruchamia skrypt hello Uruchom program PowerShell jako administrator. Wpisz następujące polecenie:

    `Get-AzureStorSimpleDeviceBackupPolicy –DeviceName <device name>`

    Identyfikator Uwaga hello zasad tworzenia kopii zapasowej.
5.  W programie Notatnik Utwórz nowy skrypt programu PowerShell przy użyciu następującego kodu hello.

    Skopiuj i wklej następujący fragment kodu:
    ```powershell
    Import-AzurePublishSettingsFile "c:\\CloudSnapshot Snapshot\\myAzureSettings.publishsettings"
    Disable-AzureDataCollection
    $ApplianceName = <myStorSimpleApplianceName>
    $RetentionInDays = 20
    $RetentionInDays = -$RetentionInDays
    $Today = Get-Date
    $ExpirationDate = $Today.AddDays($RetentionInDays)
    Select-AzureStorSimpleResource -ResourceName "myResource" –RegistrationKey
    Start-AzureStorSimpleDeviceBackupJob –DeviceName $ApplianceName -BackupType CloudSnapshot -BackupPolicyId <BackupId> -Verbose
    $CompletedSnapshots =@()
    $CompletedSnapshots = Get-AzureStorSimpleDeviceBackup -DeviceName $ApplianceName
    Write-Host "hello Expiration date is " $ExpirationDate
    Write-Host

    ForEach ($SnapShot in $CompletedSnapshots)
    {
        $SnapshotStartTimeStamp = $Snapshot.CreatedOn
        if ($SnapshotStartTimeStamp -lt $ExpirationDate)

        {
            $SnapShotInstanceID = $SnapShot.InstanceId
            Write-Host "This snpashotdate was created on " $SnapshotStartTimeStamp.Date.ToShortDateString()
            Write-Host "Instance ID " $SnapShotInstanceID
            Write-Host "This snpashotdate is older and needs toobe deleted"
            Write-host "\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#"
            Remove-AzureStorSimpleDeviceBackup -DeviceName $ApplianceName -BackupId $SnapShotInstanceID -Force -Verbose
        }
    }
    ```
      Zapisz toohello skrypt programu PowerShell hello ustawień publikowania tej samej lokalizacji, w której zapisano platformy Azure. Na przykład Zapisz jako C:\CloudSnapshot\StorSimpleCloudSnapshot.ps1.
6.  Dodaj zadanie tworzenia kopii zapasowej tooyour skryptu hello w kopii zapasowej Exec edytując przetwarzanie wstępne Opcje zadania tworzenia kopii zapasowej Exec i przetwarzania końcowego poleceń.

    ![Wykonaj kopię zapasową Exec konsoli, opcje tworzenia kopii zapasowej, karta poleceń pre-i przetwarzanie końcowe](./media/storsimple-configure-backup-target-using-backup-exec/image25.png)

> [!NOTE]
> Zaleca się uruchomić StorSimple chmury migawki zasad tworzenia kopii zapasowej jako przetwarzanie końcowe skrypt na końcu hello codzienne zadania kopii zapasowej. Aby uzyskać więcej informacji na temat sposobu tooback zapasowej i przywracania toohelp środowiska aplikacji kopii zapasowej, użytkownika spełnia Twoje RPO i RTO, skontaktuj się z Twojego architektów kopii zapasowej.

## <a name="storsimple-as-a-restore-source"></a>StorSimple jako źródło przywracania

Przywraca z pracy urządzenia StorSimple, takich jak przywracanie z dowolnym urządzeniem magazynu blokowego. Przywraca dane warstwowych toohello chmurze występuje szybkością chmury. Dla danych lokalnych przywraca wystąpić na szybkość dysku lokalnym hello hello urządzenia. Aby uzyskać informacje na temat tooperform przywracania, zobacz dokumentację Backup Exec hello. Zalecane jest zgodna z tooBackup Exec przywracania najlepszych rozwiązań.

## <a name="storsimple-failover-and-disaster-recovery"></a>StorSimple trybu failover i odzyskiwanie po awarii

> [!NOTE]
> Dla scenariuszy miejsce docelowe kopii zapasowej urządzenia chmury StorSimple nie jest obsługiwany jako miejsce docelowe przywracania.

Awarii może wpływać wiele czynników. Witaj w poniższej tabeli wymieniono typowe scenariusze odzyskiwania po awarii.

| Scenariusz | Wpływ | Jak toorecover | Uwagi |
|---|---|---|---|
| Niepowodzenie urządzenia StorSimple | Operacje tworzenia kopii zapasowej i przywracania są przerywane. | Zastąp hello urządzenia nie powiodło się i wykonywać [StorSimple trybu failover i odzyskiwania po awarii](storsimple-device-failover-disaster-recovery.md). | Tooperform przywracania po odzyskaniu urządzenia, należy zestawów roboczych pełne dane są pobierane z hello chmury toohello nowego urządzenia. Wszystkie operacje są szybkością chmury. Witaj indeksowanie i skatalogowania ponowne skanowanie proces może spowodować wszystkie zestawy kopii zapasowych toobe skanowania i pobierane z hello warstwy toohello urządzenia lokalnego poziomów w chmurze, która może być czasochłonne. |
| Exec — błąd serwera kopii zapasowej | Operacje tworzenia kopii zapasowej i przywracania są przerywane. | Odbudowanie powitania serwera kopii zapasowej i przywracania bazy danych zgodnie z opisem w [sposób ręcznego tworzenia kopii zapasowej i przywracanie z kopii zapasowej Exec (BEDB) bazy danych toodo](http://www.veritas.com/docs/000041083). | Należy odbudować ani przywrócić hello Exec kopii zapasowej serwera w lokacji odzyskiwania po awarii hello. Witaj bazy danych toohello ostatniego punktu przywracania. Jeśli hello przywrócić Exec kopii zapasowej bazy danych nie jest zsynchronizowana z najnowszego zadania tworzenia kopii zapasowej, indeksowanie i katalogowanie jest wymagane. Ten indeks i ponowne skanowanie procesu katalogu może spowodować wszystkie zestawy kopii zapasowych toobe skanowania i pobierane z hello chmury warstwy toohello urządzenia lokalnego warstwy. Dzięki temu dalsze intensywnie czasu. |
| Awaria lokacji, która powoduje utratę hello hello kopii zapasowych serwera i StorSimple | Operacje tworzenia kopii zapasowej i przywracania są przerywane. | Najpierw przywrócić StorSimple, a następnie przywróć kopię zapasową Exec. | Najpierw przywrócić StorSimple, a następnie przywróć kopię zapasową Exec. Tooperform przywracania po odzyskaniu urządzenia, należy zestawów roboczych hello pełne dane są pobierane z hello chmury toohello nowego urządzenia. Wszystkie operacje są szybkością chmury. |

## <a name="references"></a>Dokumentacja

Witaj następujące dokumenty zostały odwołanie do tego artykułu:

- [StorSimple Wielościeżkowe We/Wy Instalatora](storsimple-configure-mpio-windows-server.md)
- [Scenariusze magazynu: alokowanie elastyczne](http://msdn.microsoft.com/library/windows/hardware/dn265487.aspx)
- [Przy użyciu GPT dysków](http://msdn.microsoft.com/windows/hardware/gg463524.aspx#EHD)
- [Konfigurowanie kopii w tle dla folderów udostępnionych](http://technet.microsoft.com/library/cc771893.aspx)

## <a name="next-steps"></a>Następne kroki

- Dowiedz się więcej o tym, jak za[przywrócenie z zestawu kopii zapasowych](storsimple-restore-from-backup-set-u2.md).
- Dowiedz się więcej na temat tooperform [urządzenia trybu failover i odzyskiwania po awarii](storsimple-device-failover-disaster-recovery.md).
