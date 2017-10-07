---
title: toouse aaaHow PerfInsights na platformie Microsoft Azure | Dokumentacja firmy Microsoft
description: "Uzyskuje informacje o sposobie toouse PerfInsights tootroubleshoot maszyny Wirtualnej systemu Windows wydajności problemów."
services: virtual-machines-windows'
documentationcenter: 
author: genlin
manager: cshepard
editor: na
tags: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: genli
ms.openlocfilehash: f23ff7708c0c63bd02674b1bdc07753e8a89d9be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-perfinsights"></a>Jak toouse PerfInsights 

[PerfInsights](http://aka.ms/perfinsightsdownload) jest automatyczne skrypt, który gromadzi informacje przydatne informacje diagnostyczne, działa obciążenia We/Wy obciążenia i zapewnia toohelp raportu analizy Rozwiązywanie problemów z problemów z wydajnością maszyny Wirtualnej systemu Windows w systemie Microsoft Azure. 

Firma Microsoft zaleca uruchomienie tego skryptu przed otwarciem biletu pomocy technicznej w firmie Microsoft problemy z wydajnością maszyny Wirtualnej.

## <a name="supported-troubleshooting-scenarios"></a>Obsługiwane scenariusze rozwiązywania problemów

PerfInsights można zbierać i analizować kilka rodzajów informacji, które są zgrupowane w scenariuszach unikatowy.

### <a name="collect-disk-configuration"></a>Zbierz dane o konfiguracji dysku 

W tym scenariuszu zbiera hello konfiguracji dysku i inne ważne informacje, w tym hello następujące elementy:

-   Dzienniki zdarzeń

-   Stan sieci dla wszystkich połączeń przychodzących i wychodzących

-   Ustawienia konfiguracji sieci i zapory

-   Listy zadań dla wszystkich aplikacji, które są aktualnie uruchomione w systemie hello

-   Informacje o pliku utworzonego przez msinfo32 hello maszyny wirtualnej (VM)

-   Ustawienia konfiguracji bazy danych programu Microsoft SQL Server (jeśli hello maszyna wirtualna została zidentyfikowana jako serwer, na którym działa program SQL Server)

-   Liczniki niezawodności magazynu

-   Ważne poprawki systemu Windows

-   Sterowniki filtrów zainstalowany

To jest pasywny zbiór informacje, które nie powinny mieć wpływ na hello system. 

>[!Note]
>Ten scenariusz jest automatycznie uwzględnione w poszczególnych hello następujące scenariusze.

### <a name="benchmarkstorage-performance-test"></a>Test wydajności testu porównawczego/magazynu

W tym scenariuszu uruchamia hello [diskspd](https://github.com/Microsoft/diskspd) testu wydajności testu (IOPS i MB/s) dla wszystkich dysków, które są dołączone toohello maszyny Wirtualnej. 

> [!Note]
> W tym scenariuszu może mieć wpływ na hello system i nie powinny być uruchamiane na komputerze produkcyjnym. Jeśli to konieczne, uruchom ten scenariusz w tooavoid okna obsługi dedykowanych problemów. Większe obciążenie jest spowodowane testu śledzenia lub testu porównawczego może negatywnie wpłynąć na wydajność hello maszyny wirtualnej.
>

### <a name="general-vm-slow-analysis"></a>Analiza ogólne wolno maszyny Wirtualnej 

W tym scenariuszu uruchamia [licznika wydajności](https://msdn.microsoft.com/library/windows/desktop/aa373083(v=vs.85).aspx) śledzenia przy użyciu hello liczniki, które są określone w pliku Generalcounters.txt hello. Jeśli hello maszyna wirtualna została zidentyfikowana jako serwer, na którym działa program SQL Server, uruchamia śledzenia licznika wydajności przy użyciu hello liczniki, które znajdują się w pliku Sqlcounters.txt hello. Zawiera również dane diagnostyczne wydajności.

### <a name="vm-slow-analysis-and-benchmark"></a>Analiza powoli maszyny Wirtualnej i wzorzec

W tym scenariuszu uruchamia [licznika wydajności](https://msdn.microsoft.com/library/windows/desktop/aa373083(v=vs.85).aspx) śledzenia, w którym następuje [diskspd](https://github.com/Microsoft/diskspd) testu. 

> [!Note]
> W tym scenariuszu może mieć wpływ na hello system i nie powinny być uruchamiane na komputerze produkcyjnym. Jeśli to konieczne, uruchom ten scenariusz w tooavoid okna obsługi dedykowanych problemów. Większe obciążenie jest spowodowane testu śledzenia lub testu porównawczego może negatywnie wpłynąć na wydajność hello maszyny wirtualnej.
>

### <a name="azure-files-analysis"></a>Azure analizy plików 

W tym scenariuszu uruchamia przechwytywania licznika wydajności specjalne wraz z śledzenia ścieżek połączeń sieciowych. Przechwytywanie obejmuje wszystkie liczniki "Udziały SMB klienta" hello. Witaj poniżej przedstawiono niektóre kluczowe klienta udziału liczniki wydajności protokołu SMB należących do przechwytywania hello:

| **Typ**     | **Licznik udziałów klienta protokołu SMB** |
|--------------|-------------------------------|
| Operacje wejścia/wyjścia         | Dane żądania/s             |
|              | Liczba żądań odczytu/s             |
|              | Zapisu żądania/s            |
| Opóźnienie      | Średnia liczba żądań danych/s         |
|              | Średni czas odczytu s                 |
|              | Średni czas zapisu s                |
| Rozmiar operacji We/Wy      | Średni Bajty/danych żądania       |
|              | Średni Bajty odczytu               |
|              | Średni Bajty/zapisu              |
| Przepływność   | Dane bajty/s                |
|              | Odczytu dysku/s                |
|              | Bajty zapisane/s               |
| Długość kolejki | Średni Długość kolejki odczytu        |
|              | Średni Długość kolejki zapisu       |
|              | Średni Długość kolejki danych        |

### <a name="custom-configuration"></a>Konfiguracja niestandardowa 

Podczas wykonywania niestandardowej konfiguracji używasz wszystkie ślady (Diagnostyka wydajności, dane licznika wydajności, program xperf, sieci, storport) równolegle, zależności, jak wiele różnych dane śledzenia są wybrane. Po zakończeniu śledzenie hello narzędzie jest uruchamiane hello testu narzędzia diskspd, jeśli jest zaznaczone. 

> [!Note]
> W tym scenariuszu może mieć wpływ na hello system i nie powinny być uruchamiane na komputerze produkcyjnym. Jeśli to konieczne, uruchom ten scenariusz w tooavoid okna obsługi dedykowanych problemów. Większe obciążenie jest spowodowane testu śledzenia lub testu porównawczego może negatywnie wpłynąć na wydajność hello maszyny wirtualnej.
>

## <a name="what-kind-of-information-is-collected-by-hello-script"></a>Jakie informacje są zbierane za pomocą skryptu hello?

Informacje dotyczące maszyny Wirtualnej systemu Windows, dyski lub magazynu konfiguracji do puli, liczniki wydajności, dzienników i różne dane śledzenia są zbierane w zależności od scenariusza wydajności hello używanego:

|Zebrane dane                              |  |  | Scenariusze wydajności |  |  | |
|----------------------------------|----------------------------|------------------------------------|--------------------------|--------------------------------|----------------------|----------------------|
|                              | Zbieraj konfiguracja dysków | Test wydajności testu porównawczego i magazynowania | Analiza ogólne wolno maszyny Wirtualnej | Analiza powoli maszyny Wirtualnej i wzorzec | Azure analizy plików | Konfiguracja niestandardowa |
| Informacje z dzienników zdarzeń      | Tak                        | Tak                                | Tak                      | Tak                            | Tak                  | Tak                  |
| Informacje o systemie               | Tak                        | Tak                                | Tak                      | Tak                            | Tak                  | Tak                  |
| Mapa woluminu                       | Tak                        | Tak                                | Tak                      | Tak                            | Tak                  | Tak                  |
| Mapy dysku                         | Tak                        | Tak                                | Tak                      | Tak                            | Tak                  | Tak                  |
| Uruchomione zadania                    | Tak                        | Tak                                | Tak                      | Tak                            | Tak                  | Tak                  |
| Liczniki niezawodności magazynu     | Tak                        | Tak                                | Tak                      | Tak                            | Tak                  | Tak                  |
| Informacje o magazynu              | Tak                        | Tak                                | Tak                      | Tak                            | Tak                  | Tak                  |
| Dane wyjściowe fsutil                    | Tak                        | Tak                                | Tak                      | Tak                            | Tak                  | Tak                  |
| Informacje dotyczące sterownik filtru               | Tak                        | Tak                                | Tak                      | Tak                            | Tak                  | Tak                  |
| Dane wyjściowe polecenia netstat                   | Tak                        | Tak                                | Tak                      | Tak                            | Tak                  | Tak                  |
| Konfiguracja sieci            | Tak                        | Tak                                | Tak                      | Tak                            | Tak                  | Tak                  |
| Konfiguracja zapory           | Tak                        | Tak                                | Tak                      | Tak                            | Tak                  | Tak                  |
| Konfiguracja programu SQL Server         | Tak                        | Tak                                | Tak                      | Tak                            | Tak                  | Tak                  |
| Dane wydajności diagnostyki śledzenia * |                            |                                    | Tak                      |                                |                      | Tak                  |
| Licznik wydajności śledzenia **     |                            |                                    |                          |                                |                      | Tak                  |
| Licznik SMB śledzenia **             |                            |                                    |                          |                                | Tak                  |                      |
| SQL Server licznika śledzenia **      |                            |                                    |                          |                                |                      | Tak                  |
| Program XPerf śledzenia                      |                            |                                    |                          |                                |                      | Tak                  |
| StorPort śledzenia                   |                            |                                    |                          |                                |                      | Tak                  |
| Śledzenie sieci                    |                            |                                    |                          |                                | Tak                  | Tak                  |
| Śledzenia testu narzędzia Diskspd ***      |                            | Tak                                |                          | Tak                            |                      |                      |
|       |                            |                         |                                                   |                      |                      |

### <a name="performance-diagnostics-trace-"></a>Wydajności diagnostyki śledzenia (*)

Działa to aparat oparty na regułach w hello tła toocollect danych i diagnozowanie problemów stałej wydajności. obecnie obsługiwane są następujące reguły Hello:

- Reguła HighCpuUsage: wykrywa wysokiej okresów użycia Procesora i przedstawia hello pakiety najwięcej użycia procesora CPU podczas tych okresów.
- Reguła HighDiskUsage: wykrywa okresów użycia dysku na dyskach fizycznych i zawiera dysk hello konsumentów użycia tych okresach.
- Reguła HighResolutionDiskMetric: Pokazuje IOPS, przepływności i metryki opóźnienia we/wy na 50 milisekund dla każdego dysku fizycznego. Pomaga tooquickly zidentyfikować dysku ograniczania okresów.
- Reguła HighMemoryUsage: wykrywa okresów użycia pamięci wysokiej i przedstawia pamięci górnej hello konsumentów użycia tych okresach.

> [!NOTE] 
> Obecnie są obsługiwane wersje systemu Windows, obejmujących hello .NET Framework 3.5 lub nowszy.

### <a name="performance-counter-trace-"></a>Śledzenia licznik wydajności (*)

Zbiera hello następujące liczniki wydajności:

- \Process, \Processor, \Memory, \Thread, \PhysicalDisk, \LogicalDisk
- \Server\Pool stron, \Cache\Lazy zapisu opróżnienia/s, \Cache\Dirty niestronicowanej, błędy, błędy \Server\Pool stronicowanej
- Wybrane liczniki w obszarze \Network interfejsu, \IPv4\Datagrams, \IPv6\Datagrams, \TCPv4\Segments, \TCPv6\Segments, \Network karty, \WFPv4\Packets, \WFPv6\Packets, \UDPv4\Datagrams, \UDPv6\Datagrams, \TCPv4\Connection, \TCPv6\Connection, \ Sieci Winsock \Microsoft QoS Policy\Packets, \Per procesora interfejsu karty działań w sieci, podstawowego dostawcy

#### <a name="for-sql-server-instances"></a>Dla wystąpienia programu SQL Server
- Menedżer serwera: bufor \SQL, Statystyka puli \SQLServer:Resource, \SQLServer:SQL Statistics\
- \SQLServer:Locks, \SQLServer:General, statystyki
- Metody \SQLServer:Access

#### <a name="for-azure-files"></a>W przypadku plików platformy Azure
Udziały klient \SMB

### <a name="diskspd-benchmark-trace-"></a>Testu narzędzia Diskspd śledzenia (*)
Testy obciążenia We/Wy Diskspd [dysk systemu operacyjnego (zapis) oraz dyski puli (odczyt/zapis)]

## <a name="run-hello-perfinsights-on-your-vm"></a>Uruchom hello PerfInsights na maszynie Wirtualnej

### <a name="what-do-i-have-tooknow-before-i-run-hello-script"></a>Co to są dostępne tooknow przed I Uruchom skrypt hello? 

**Wymagania dotyczące skryptu**

1.  Ten skrypt należy uruchomić na powitania maszynę Wirtualną, która ma problem z wydajnością hello. 

2.  Witaj, obsługiwane są następujące systemy operacyjne: Windows Server 2008 R2, 2012, 2012 R2, 2016; Windows 8.1 i Windows 10.

**Możliwe problemy podczas uruchamiania skryptu hello na maszynach wirtualnych w środowisku produkcyjnym:**

1.  skrypt Hello może niekorzystnie wpłynąć na wydajność hello hello wirtualna stosowania oraz scenariusz "Testu" lub "Custom" hello, który jest skonfigurowany przy użyciu narzędzia XPerf lub narzędzia DiskSpd. Uruchom skrypt hello w środowisku produkcyjnym, należy zachować ostrożność.

2.  Możesz użyć skryptu hello oraz scenariusz "Testu" lub "Custom" hello, który jest skonfigurowany przy użyciu narzędzia DiskSpd, upewnij się, że nie inne operacje w tle zakłóca hello obciążenia We/Wy na dyskach hello przetestowane.

3.  Domyślnie program hello skrypt używa hello magazyn tymczasowy dysku toocollect danych. Jeśli śledzenie pozostaje włączona przez dłuższy czas, może być odpowiednie hello ilość zbieranych danych. Może to zmniejszyć hello dostępność miejsca na dysku tymczasowym hello, w związku z tym wpływających na dowolnej aplikacji, która opiera się na tym dysku.

### <a name="how-do-i-run-perfinsights"></a>Jak uruchomić PerfInsights? 

toorun hello skryptu, wykonaj następujące kroki:

1. Pobierz [PerfInsights.zip](http://aka.ms/perfinsightsdownload).

2. Odblokować plik PerfInsights.zip hello. toodo to plik PerfInsights.zip powitania kliknij prawym przyciskiem myszy, wybierz **właściwości**. W hello **ogólne** wybierz opcję **Odblokuj** , a następnie wybierz **OK**. Będzie to upewnij się, że hello skrypt jest uruchamiany bez dodatkowych zabezpieczeń monity.  

    ![Plik zip hello odblokowywania](media/how-to-use-perfInsights/unlock-file.png)

3.  Rozwiń plik PerfInsights.zip hello skompresowane w napędzie tymczasowe (domyślnie zazwyczaj jest to dysk hello D). Witaj skompresowany plik powinien zawierać następujące hello plików i folderów:

    ![pliki z folderu zip hello](media/how-to-use-perfInsights/file-folder.png)

4.  Otwórz program Windows PowerShell jako administrator, a następnie uruchom skrypt PerfInsights.ps1 hello.

    ```
    cd <hello path of PerfInsights folder >
    Powershell.exe -ExecutionPolicy UnRestricted -NoProfile -File .\\PerfInsights.ps1
    ```

    Może być tooenter "y" tooif masz pytanie, tooconfirm że zasady wykonywania hello toochange.

    Okno dialogowe zastrzeżenie hello są podane informacje diagnostyczne tooshare opcji hello z Support firmy Microsoft. Toocontinue umowy licencyjnej toohello również musi wyrazić zgodę. Wybierz odpowiednie opcje, a następnie kliknij przycisk **Uruchom skrypt**.

    ![Pole zrzeczenie odpowiedzialności](media/how-to-use-perfInsights/disclaimer.png)

5.  Przedstawia liczbę przypadków hello, jeśli jest dostępne po uruchomieniu skryptu hello (jest to naszych statystyki). Następnie kliknij przycisk **OK**.
    
    ![Wprowadź identyfikator pomocy technicznej](media/how-to-use-perfInsights/enter-support-number.png)

6.  Wybierz dysk magazynu tymczasowego. Hello skryptu można wykryć automatycznie hello litera dysku hello. W razie wystąpienia problemów w tym etapie, może być monit tooselect hello dysku (dysk domyślny hello jest D). Wygenerowane dzienniki są przechowywane w tym miejscu w dzienniku hello\_folder kolekcji. Po wprowadzeniu lub zaakceptować hello literę dysku, kliknij przycisk **OK**.

    ![Wprowadź dysku](media/how-to-use-perfInsights/enter-drive.png)

7.  Wybierz scenariusz rozwiązywania problemów z hello liście.

       ![Wybierz scenariusze pomocy technicznej](media/how-to-use-perfInsights/select-scenarios.png)

8.  Można również uruchomić PerfInsights bez interfejsu użytkownika.

    Hello następujące polecenie uruchamia hello "Wolno wirtualna ogólne analizy" Rozwiązywanie problemów z scenariusz bez monitowania interfejsu użytkownika lub przechwycenia danych dla 30 sekund. Monit tooconsent toohello tych samych zastrzeżenie i umowy licencyjnej, które są wymienione w kroku 4.

        powershell.exe -ExecutionPolicy UnRestricted -NoProfile -Command ".\\PerfInsights.ps1 -NoGui -Scenario vmslow -TracingDuration 30"

    Jeśli chcesz PerfInsights toorun w trybie dyskretnym, użyj **- AcceptDisclaimerAndShareDiagnostics** parametru. Na przykład użyć hello następujące polecenie:

        powershell.exe -ExecutionPolicy UnRestricted -NoProfile -Command ".\\PerfInsights.ps1 -NoGui -Scenario vmslow -TracingDuration 30 -AcceptDisclaimerAndShareDiagnostics"

### <a name="how-do-i-troubleshoot-issues-while-running-hello-script"></a>Jak rozwiązywać problemy podczas uruchamiania skryptu hello?

Jeśli skrypt hello nieprawidłowo kończy działanie, możesz wyczyścić niespójna, uruchamiając skrypt hello razem z hello — przełącznik oczyszczania w następujący sposób:

    powershell.exe -ExecutionPolicy UnRestricted -NoProfile -Command ".\\PerfInsights.ps1 -Cleanup"

Ewentualnych problemów podczas automatycznego wykrywania hello hello tymczasowego dysku może być monitowany tooselect hello dysku (dysk domyślny hello jest D).

![Wprowadź dysku](media/how-to-use-perfInsights/enter-drive.png)

skrypt Hello odinstalowuje hello narzędzia i usuwa folderów tymczasowych.

### <a name="troubleshooting-other-script-issues"></a>Rozwiązywanie problemów z innych problemów skryptu 

Ewentualnych problemów po uruchomieniu skryptu hello, naciśnij klawisz wykonywanie skryptu hello toointerrupt klawisze Ctrl + C. obiekty tymczasowe tooremove, zobacz sekcję "Oczyszczanie po zakończeniu nietypowe" hello.

Jeśli będziesz kontynuować błędu skryptu tooexperience mimo kilku prób, firma Microsoft zaleca Uruchom skrypt hello w "tryb debugowania" przy użyciu hello "-debugowania" opcja parametru podczas uruchamiania.

Po awarii hello występuje kopiowania hello pełne dane wyjściowe konsoli programu PowerShell hello, a następnie wysłać je toohello Microsoft Support agenta, który jest pomoc w przypadku toohelp rozwiązywanie problemu hello.

### <a name="how-do-i-run-hello-script-in-custom-configuration-mode"></a>Jak uruchomić skrypt hello w trybie niestandardowej konfiguracji?

Wybierając hello **niestandardowy** konfiguracji, można włączyć kilka śladów równoległe (Użyj zaznacz toomulti klawiszem Shift):

![Wybierz scenariuszy](media/how-to-use-perfInsights/select-scenario.png)

Po wybraniu hello Diagnostyka wydajności, śledzenia licznika wydajności, śledzenia programu XPerf, śledzenia sieci lub śledzenia Storport scenariuszy, wykonaj te instrukcje hello hello okien dialogowych, a następnie spróbuj tooreproduce hello rozwiązującą problem z wydajnością, po uruchomieniu hello śladów.

Witaj następujące okno dialogowe umożliwia uruchamianie śledzenia:

![Rozpocznij śledzenie](media/how-to-use-perfInsights/start-trace-message.png)

ślady hello toostop, ma tooconfirm hello polecenie w oknie dialogowym drugiego.

![Zatrzymaj śledzenie](media/how-to-use-perfInsights/stop-trace-message.png)
![Zatrzymaj śledzenie](media/how-to-use-perfInsights/ok-trace-message.png)

Gdy hello śladów lub wykonywane są operacje, nowy plik jest generowany w D:\\dziennika\_kolekcji (lub hello tymczasowej stacji) o nazwie **CollectedData\_RRRR MM-dd\_hh\_mm \_ss.zip.** Możesz wysłać ten plik toohello obsługi agent do analizy.

## <a name="review-hello-diagnostics-report-created-by-perfinsights"></a>Przejrzyj raport diagnostyczny hello utworzone przez PerfInsights

W ramach hello **CollectedData\_RRRR MM-dd\_hh\_mm\_pliku ss.zip** generowany przez PerfInsights, można znaleźć raport HTML ze szczegółami hello wyników PerfInsights. tooreview hello raportu, a następnie rozwiń hello **CollectedData\_RRRR MM-dd\_hh\_mm\_ss.zip** pliku, a następnie otwórz hello **PerfInsights Report.html**pliku.

Wybierz hello **ustalenia** kartę.

![Znajdź kartę](media/how-to-use-perfInsights/findingtab.png)

**Uwagi**

-   Wiadomości na czerwono znane problemy konfiguracji, które mogą powodować problemy z wydajnością.

-   Komunikaty w żółty są ostrzeżenia, które reprezentują-optymalne konfiguracje, które nie muszą powodować problemy z wydajnością.

-   Wiadomości na niebiesko są tylko szczegółowych instrukcji.

Przejrzyj hello łącza HTTP dla wszystkich komunikatów o błędach w czerwonym tooget bardziej szczegółowe informacje o ustalenia hello i ich wpływu na wydajność hello lub najlepszych rozwiązań dotyczących konfiguracji zoptymalizowana pod kątem wydajności.

### <a name="disk-configuration-tab"></a>Karta Konfiguracja dysku

Witaj **omówienie** sekcja wyświetla różne widoki hello magazynu konfiguracji, w tym informacje z narzędzia Diskpart i miejsca do magazynowania

Witaj **DiskMap** i **VolumeMap** sekcjach opisano na podwójną perspektywy jak logicznej woluminów i dysków fizycznych są powiązane tooeach innych.

W hello perspektywy dysk fizyczny (DiskMap) hello tabeli przedstawiono wszystkie woluminy logiczne, które są uruchomione na dysku hello. W hello poniższy przykład PhysicalDrive2 uruchamia 2 logicznej woluminy tworzone na wielu partycjach (J i H):

![Karta dane](media/how-to-use-perfInsights/disktab.png)

W hello perspektywy woluminu (*VolumeMap*), hello tabelach przedstawiono wszystkie dyski fizyczne hello w obszarze każdego woluminu logicznego. Zwróć uwagę, że dla dysków dynamicznych/RAID, mogą zostać uruchomione logicznej woluminu na wiele dysków fizycznych. W następujące przykładowe hello *C:\\instalacji* jest punkt_instalacji, skonfigurowany jako *SpannedDisk* na PhysicalDisks \#2 i \#3:

![Karta woluminu](media/how-to-use-perfInsights/volumetab.png)

### <a name="sql-server-tab"></a>Karta programu SQL Server

Jeśli hello docelowej maszyny Wirtualnej obsługuje wszystkie wystąpienia programu SQL Server, zostanie wyświetlony dodatkowe karty w raporcie hello, o nazwie **programu SQL Server**:

![Karta SQL](media/how-to-use-perfInsights/sqltab.png)

Ta sekcja zawiera "Przegląd" oraz dodatkowe sub kart dla poszczególnych wystąpień programu SQL Server hello hostowanych na powitania maszyny Wirtualnej.

sekcja "Informacje" Hello zawiera przydatne tabelę, która znajduje się podsumowanie wszystkich hello dyski fizyczne (dysków systemowych i danych) z systemem, które zawierają pliki danych i pliki dziennika transakcji.

W hello poniższy przykład *PhysicalDrive0* (uruchomionego hello C dysku) jest wyświetlany, ponieważ zarówno hello *modeldev* i *modellog* pliki znajdują się na dysku hello C i są one różnych typów (takich jak plik danych i dziennika transakcji, odpowiednio):

![LogInfo](media/how-to-use-perfInsights/loginfo.png)

karty danego wystąpienia programu SQL Server Hello zawierają ogólne sekcja, która zawiera podstawowe informacje o wybranym wystąpieniu hello i dodatkowe sekcje zaawansowane informacje, w tym ustawienia, konfiguracje i opcje użytkownika.

## <a name="references-toohello-external-tools-used"></a>Odwołuje się do narzędzia zewnętrznego toohello używane

### <a name="diskspd"></a>Narzędzia Diskspd

DISKSPD jest magazynu obciążenia generator wydajności testu narzędziem hello systemu Windows i Windows Server i infrastrukturą serwera chmury engineering zespołów. Aby uzyskać więcej informacji, zobacz [Diskspd](https://github.com/Microsoft/diskspd).

### <a name="xperf"></a>Program XPerf

Program XPerf jest śladów toocapture narzędzia wiersza polecenia, z zestawu narzędzi wydajności systemu Windows hello.

Aby uzyskać więcej informacji, zobacz [Toolkit wydajności systemu Windows — program Xperf](https://blogs.msdn.microsoft.com/ntdebugging/2008/04/03/windows-performance-toolkit-xperf/).

## <a name="next-steps"></a>Następne kroki

### <a name="upload-diagnostics-logs-and-reports-toomicrosoft-support-for-further-review"></a>Przekaż diagnostycznych dzienników i raportów tooMicrosoft pomocy technicznej do dalszej analizy

Podczas pracy z hello personelu Support firmy Microsoft, może być żądane tootransmit hello wygenerowanej przez hello tooassist PerfInsights proces rozwiązywania problemów.

Hello przedstawiciel pomocy technicznej utworzy DTM obszaru roboczego dla Ciebie, a otrzymasz wiadomość e-mail zawierającą link toohello [DTM portal (https://filetransfer.support.microsoft.com/EFTClient/Account/Login.htm) oraz identyfikator unikatowy użytkownika i hasła.

Ta wiadomość zostanie wysłana z **usługi diagnostyki automatycznego CTS** (ctsadiag@microsoft.com).

![Przykładowe wiadomość hello](media/how-to-use-perfInsights/supportemail.png)

Aby dodatkowo zwiększyć bezpieczeństwo, będzie wymagany toochange hasła na pierwszym użyciu.

Po zalogowaniu tooDTM znajdziesz hello tooupload okno dialogowe **CollectedData\_RRRR MM-dd\_hh\_mm\_ss.zip** pliku, który został zebrany przez PerfInsights.
