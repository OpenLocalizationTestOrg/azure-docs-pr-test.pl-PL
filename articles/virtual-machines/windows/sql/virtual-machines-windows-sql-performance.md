---
title: "aaaPerformance najlepsze rozwiązania dotyczące programu SQL Server na platformie Azure | Dokumentacja firmy Microsoft"
description: "Zawiera najlepsze rozwiązania dla optymalizacji wydajności programu SQL Server na maszynach wirtualnych Microsoft Azure."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: a0c85092-2113-4982-b73a-4e80160bac36
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 06/27/2017
ms.author: jroth
ms.openlocfilehash: 42ec9fbeb2dec3a654b93bbd08d666369835ee73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="performance-best-practices-for-sql-server-in-azure-virtual-machines"></a>Najlepsze rozwiązania w zakresie wydajności dla programu SQL Server w usłudze Azure Virtual Machines

## <a name="overview"></a>Omówienie

Ten temat zawiera najlepsze rozwiązania dotyczące optymalizacji wydajności programu SQL Server w maszynie wirtualnej platformy Azure firmy Microsoft. Podczas uruchamiania programu SQL Server w maszynach wirtualnych platformy Azure, zaleca się kontynuować przy użyciu hello opcje, które są stosowane tooSQL serwera w środowisku serwera lokalnego dostrajania wydajności bazy danych. Jednak wydajność hello relacyjnej bazy danych w chmurze publicznej zależy od wielu czynników, takich jak rozmiar hello maszyny wirtualnej oraz konfiguracji hello hello dysków danych.

Podczas tworzenia obrazów programu SQL Server [należy wziąć pod uwagę inicjowania obsługi administracyjnej maszyn wirtualnych w portalu Azure hello](virtual-machines-windows-portal-sql-server-provision.md). Udostępnione w hello Portal za pomocą Menedżera zasobów serwera SQL w maszynach wirtualnych implementuje wszystkie następujące najlepsze rozwiązania, w tym hello konfiguracji magazynu.

Ten artykuł koncentruje się na pobieranie hello *najlepsze* wydajności programu SQL Server na maszynach wirtualnych Azure. Jeżeli obciążenie jest mniej wymagająca, nie mogą wymagać co optymalizacji wymienionych poniżej. Twoje potrzeby w zakresie wydajności i obciążenia wzorce wziąć pod uwagę oceny tych zaleceń.

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="quick-check-list"></a>Szybkie sprawdzenie listy

Witaj poniżej znajduje się lista szybkie sprawdzenie do uzyskania optymalnej wydajności programu SQL Server na maszynach wirtualnych platformy Azure:

| Obszar | Optymalizacje |
| --- | --- |
| [Rozmiar maszyny Wirtualnej](#vm-size-guidance) |[DS3](../../virtual-machines-windows-sizes-memory.md) lub nowszej wersji Enterprise programu SQL.<br/><br/>[DS2](../../virtual-machines-windows-sizes-memory.md) lub nowszej wersji Standard programu SQL i sieci Web. |
| [Storage](#storage-guidance) |Użyj [magazyn w warstwie Premium](../../../storage/common/storage-premium-storage.md). Magazynu w warstwie standardowa zaleca się tylko do programowania i testowania.<br/><br/>Zachowaj hello [konta magazynu](../../../storage/common/storage-create-storage-account.md) i maszyna wirtualna w hello SQL Server tego samego regionu.<br/><br/>Wyłącz Azure [magazynu geograficznie nadmiarowego](../../../storage/common/storage-redundancy.md) (replikacja geograficzna) na koncie magazynu hello. |
| [Dyski](#disks-guidance) |Użyj co najmniej 2 [dysków P30](../../../storage/common/storage-premium-storage.md#scalability-and-performance-targets) (1 dla plików dziennika; 1 dla danych plików i TempDB).<br/><br/>Unikaj używania systemu operacyjnego lub dysków tymczasowego magazynu bazy danych lub rejestrowania.<br/><br/>Włącz buforowanie odczytu na dyskach hello hosting hello pliki danych i bazy danych TempDB.<br/><br/>Nie należy włączać buforowanie na dyskach hosting hello pliku dziennika.<br/><br/>Ważne: Zatrzymywanie usługi programu SQL Server hello, w przypadku zmiany ustawień pamięci podręcznej hello dysku maszyny Wirtualnej platformy Azure.<br/><br/>Paskowych wielu danych Azure dysków tooget zwiększyć przepływność we/wy.<br/><br/>Format z opisem rozmiarów alokacji. |
| [WE/WY](#io-guidance) |Włączanie kompresji strony bazy danych.<br/><br/>Włącz inicjowanie błyskawicznych plików dla danych plików.<br/><br/>Ogranicz lub wyłącz automatyczne zwiększanie hello bazy danych.<br/><br/>Wyłącz autoshrink na powitania bazy danych.<br/><br/>Przenieś wszystkie dyski toodata baz danych, w tym systemowych baz danych.<br/><br/>Przenieś programu SQL Server błąd dziennika i śledzenia katalogów toodata dyski z plikami.<br/><br/>Ustawienia domyślne lokalizacje plików kopii zapasowej i bazy danych.<br/><br/>Włącz zablokowanych stron.<br/><br/>Zastosuj poprawki wydajności programu SQL Server. |
| [Funkcja unikatowe](#feature-specific-guidance) |Utwórz kopię zapasową bezpośrednio tooblob magazynu. |

Aby uzyskać więcej informacji na temat *jak* i *Dlaczego* toomake te optymalizacje, przejrzyj szczegóły hello i wskazówki zamieszczone w poniższych sekcjach.

## <a name="vm-size-guidance"></a>Wskazówki dotyczące rozmiaru maszyny Wirtualnej

W przypadku aplikacji poufnych wydajności zaleca się użycie następujących hello [rozmiary maszyn wirtualnych](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json):

* **SQL Server Enterprise Edition**: DS3 lub nowszej
* **SQL Server Standard i Web Edition**: DS2 lub nowszej

## <a name="storage-guidance"></a>Wskazówki dotyczące magazynu

Obsługa maszyn wirtualnych: seria DS (wraz z serii DSv2 i GS-series) [magazyn w warstwie Premium](../../../storage/common/storage-premium-storage.md). Magazyn w warstwie Premium jest zalecana dla wszystkich obciążeń produkcyjnych.

> [!WARNING]
> Standard Storage ma różnych opóźnienia i przepustowości i jest zalecane tylko dla obciążeń i testowania. Obciążeń produkcyjnych należy używać magazyn w warstwie Premium.

Ponadto zaleca się utworzenie konta magazynu Azure w hello tym samym centrum danych jako programu SQL Server maszyn wirtualnych tooreduce transfer opóźnienia. Podczas tworzenia konta magazynu, należy wyłączyć — replikacja geograficzna jako kolejność spójne zapisu na wielu dyskach nie jest gwarantowana. Zamiast tego należy wziąć pod uwagę konfigurowania technologii odzyskiwania po awarii programu SQL Server, między dwiema danych Azure. Aby uzyskać więcej informacji, zobacz [wysokiej dostępności i odzyskiwania po awarii dla programu SQL Server w usłudze Azure Virtual Machines](virtual-machines-windows-sql-high-availability-dr.md).

## <a name="disks-guidance"></a>Wskazówki dotyczące dysków

Istnieją trzy typy głównego dysku na maszynie Wirtualnej platformy Azure:

* **Dysk systemu operacyjnego**: podczas tworzenia maszyny wirtualnej platformy Azure, platforma hello dołączą co najmniej jednego dysku (oznaczone jako hello **C** dysku) toohello maszyny Wirtualnej dla dysku systemu operacyjnego. Ten dysk jest plik VHD przechowywany jako stronicowy obiekt blob w magazynie.
* **Dysku tymczasowym**: maszyny wirtualne Azure zawiera inny dysk o nazwie dysku tymczasowym hello (oznaczone jako hello **D**: dysku). Jest to dysk na węźle hello, który może służyć do miejsce na pliki tymczasowe.
* **Dyski danych**: można także dołączyć jako dyski danych maszyny wirtualnej tooyour dodatkowych dysków i będą one przechowywane w magazynie jako stronicowych obiektów blob.

Witaj poniższych sekcjach opisano zalecenia dotyczące używania tych dyskach.

### <a name="operating-system-disk"></a>Dysk systemu operacyjnego

Dysk systemu operacyjnego jest wirtualnego dysku twardego, który można rozruchu i instalacji uruchomiona wersja systemu operacyjnego i jest oznaczony jako **C** dysku.

Domyślnie buforowanie zasad na dysku systemu operacyjnego hello **odczytu/zapisu**. W przypadku aplikacji poufnych wydajności zalecane jest użycie dysków z danymi zamiast hello dysku systemu operacyjnego. Zobacz sekcję hello na dyskach danych poniżej.

### <a name="temporary-disk"></a>Tymczasowe dysku

Witaj dysku magazyn tymczasowy, oznaczone jako hello **D**: dysk, nie jest utrwalona tooAzure magazynu obiektów blob. Nie należy przechowywać plików bazy danych użytkownika lub pliki dziennika transakcji użytkownika na powitania **D**: dysku.

D-series, Dv2 serii i G serii maszyn wirtualnych jest hello tymczasowej stacji na tych maszynach wirtualnych na dyskach SSD. Jeżeli obciążenie intensywnie korzysta z bazy danych TempDB (np. obiekty tymczasowe lub złożonych sprzężeń), przechowywania bazy danych TempDB na powitania **D** dysku może spowodować wyższej przepustowości TempDB i zmniejszyć opóźnienia bazy danych TempDB.

Dla maszyn wirtualnych, które obsługują magazyn w warstwie Premium (serii DS, DSv2 serii i serii GS) zalecamy przechowywanie bazy danych TempDB na dysku, który obsługuje magazyn w warstwie Premium z buforowaniem odczytu włączona. Istnieje jeden wyjątek toothis zalecenia; Jeśli użycie bazy danych TempDB jest intensywnie wykonujących operacje zapisu, można osiągnąć większą wydajność dzięki przechowywaniu bazy danych TempDB na lokalne powitania **D** dysk, który jest również na dyskach SSD na rozmiary maszyny.

### <a name="data-disks"></a>Dyski danych

* **Użyć dysków danych dla plików danych i dziennika**: co najmniej, użyj 2 magazyn w warstwie Premium [dysków P30](../../../storage/common/storage-premium-storage.md#scalability-and-performance-targets) gdzie jeden dysk zawiera pliki dziennika hello a hello innych hello dane i pliki bazy danych TempDB. Każdy dysk magazyn w warstwie Premium zawiera pewną liczbę IOPs i przepustowości (MB/s) w zależności od rozmiaru, zgodnie z opisem w hello poniższego artykułu: [przy użyciu magazyn w warstwie Premium dla dysków](../../../storage/common/storage-premium-storage.md).

* **Rozkładanie**: więcej przepustowości, można dodać dodatkowego dysku z danymi i używać rozkładanie. toodetermine hello liczba dysków danych, należy tooanalyze hello liczbę IOPS i przepustowość wymagana Twoje pliki dziennika i dane i pliki bazy danych TempDB. Zwróć uwagę, że różne rozmiary maszyny Wirtualnej mają różne limity hello liczby IOPs, jak i przepustowość obsługiwane, zobacz tabele hello na IOPS na [rozmiar maszyny Wirtualnej](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Użyj hello następujące wytyczne:

  * Dla systemu Windows 8/Windows Server 2012 lub nowszym, użyj [miejsca do magazynowania](https://technet.microsoft.com/library/hh831739.aspx) z hello następujące wytyczne:

      1. Zestaw hello interleave (rozmiar przeplotu) too64 KB (65536 bajtów) dla obciążeń OLTP i 256 KB (262 144 bajty) dotyczących magazynów wpływ na wydajność obciążeń tooavoid powodu toopartition niespójność danych. To musi być ustawiona przy użyciu programu PowerShell.
      1. Ustaw liczbę kolumn = Liczba dysków fizycznych. W przypadku konfigurowania więcej niż 8 dysków (nie interfejsu użytkownika Menedżera serwera) za pomocą programu PowerShell. 

    Na przykład hello następującego środowiska PowerShell tworzy nowy rozmiar too64 KB i hello liczbę kolumn too2 interleave puli magazynu z hello:

    ```powershell
    $PoolCount = Get-PhysicalDisk -CanPool $True
    $PhysicalDisks = Get-PhysicalDisk | Where-Object {$_.FriendlyName -like "*2" -or $_.FriendlyName -like "*3"}

    New-StoragePool -FriendlyName "DataFiles" -StorageSubsystemFriendlyName "Storage Spaces*" -PhysicalDisks $PhysicalDisks | New-VirtualDisk -FriendlyName "DataFiles" -Interleave 65536 -NumberOfColumns 2 -ResiliencySettingName simple –UseMaximumSize |Initialize-Disk -PartitionStyle GPT -PassThru |New-Partition -AssignDriveLetter -UseMaximumSize |Format-Volume -FileSystem NTFS -NewFileSystemLabel "DataDisks" -AllocationUnitSize 65536 -Confirm:$false 
    ```

  * Dla systemu Windows 2008 R2 lub starszym można używać dysków dynamicznych (woluminy rozłożone systemu operacyjnego) oraz rozmiar przeplotu hello jest zawsze 64 KB. Należy pamiętać, że ta opcja jest przestarzały począwszy od systemu Windows 8/Windows Server 2012. Informacje, zobacz hello obsługi instrukcji w [usługi dysków wirtualnych przechodzi tooWindows interfejsu API zarządzania magazynami](https://msdn.microsoft.com/library/windows/desktop/hh848071.aspx).

  * Jeśli obciążenie nie dziennika znacznym i nie wymaga dedykowanego IOPs, można skonfigurować tylko jedną pulę magazynu. W przeciwnym razie utwórz dwie pule magazynu, jeden dla plików dziennika hello i innej puli magazynu dla hello plików danych i bazy danych TempDB. Określ numer hello dysków skojarzone z każdym pula magazynów oparta na Twoich oczekiwań obciążenia. Należy pamiętać, że różne rozmiary maszyn wirtualnych pozwala różne liczby dysków dołączonych danych. Aby uzyskać więcej informacji, zobacz [rozmiary maszyn wirtualnych](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

  * Jeśli nie używasz magazyn w warstwie Premium (wszystkie scenariusze tworzenia/testowania), zalecane hello jest tooadd hello maksymalna liczba dysków danych obsługiwane przez użytkownika [rozmiar maszyny Wirtualnej](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) i użyj rozkładanie.

* **Buforowanie zasad**: dysków z danymi dla magazyn w warstwie Premium, Włącz buforowanie odczytu dla dysków z danymi hello hosting tylko danych plików i bazy danych TempDB. Jeśli nie używasz magazyn w warstwie Premium, nie należy włączać buforowania na wszelkich dyskach danych. Instrukcje dotyczące konfigurowania dysku buforowania, można znaleźć hello następujące tematy: [AzureOSDisk zestaw](https://msdn.microsoft.com/library/azure/jj152847) i [AzureDataDisk zestawu](https://msdn.microsoft.com/library/azure/jj152851.aspx).

  > [!WARNING]
  > Zatrzymywanie usługi programu SQL Server hello, zmieniając ustawienie pamięci podręcznej hello Azure VM dysków tooavoid hello możliwości ewentualne uszkodzenia bazy danych.

* **Rozmiar jednostki alokacji systemu plików NTFS**: podczas formatowania dysku danych hello, zaleca się użyć rozmiar jednostki alokacji 64 KB danych i plików dziennika, jak również w bazie danych TempDB.

* **Najlepsze rozwiązania dotyczące zarządzania dysku**: podczas wpisywania usunięcie dysku danych lub zmiana jego pamięci podręcznej, Zatrzymaj usługę programu SQL Server hello podczas zmiany hello. Jeśli ustawienia buforowania hello są zmienione na dysku systemu operacyjnego hello Azure zatrzymuje hello maszyny Wirtualnej, zmiany hello typ pamięci podręcznej i uruchamia ponownie hello maszyny Wirtualnej. Po zmianie ustawień pamięci podręcznej hello dysku danych, hello maszyny Wirtualnej nie został on zatrzymany, ale dysk danych hello jest odłączony od hello maszyny Wirtualnej podczas hello zmienić, a następnie ponownie nałożona.

  > [!WARNING]
  > Błąd toostop hello usługi SQL Server podczas tych czynności może spowodować uszkodzenie bazy danych.

## <a name="io-guidance"></a>Wskazówki dotyczące operacji We/Wy

* najbardziej efektywne Hello magazyn w warstwie Premium są uzyskuje, gdy parallelize żądań i aplikacji. Magazyn w warstwie Premium jest przeznaczony do scenariuszy, których głębokość kolejki we/wy hello jest większa niż 1, dlatego niewielkiego lub żadnego wzrost wydajności jednowątkowe serial żądań (nawet jeśli są one znacznym magazynu). Na przykład to może mieć wpływ na wyniki testu jednowątkowe hello narzędzia analizy wydajności, takich jak SQLIO.

* Należy rozważyć użycie [bazy danych kompresji strony](https://msdn.microsoft.com/library/cc280449.aspx) jak może pomóc zwiększyć wydajność obciążeń intensywnie korzystających z operacji We/Wy. Jednak hello kompresji danych może zwiększyć użycie procesora CPU hello na powitania serwera bazy danych.

* Rozważ włączenie błyskawicznych plik inicjowania tooreduce hello czas wymagany do przydzielenia pierwszy plik. Zaletą tootake inicjowania błyskawicznych pliku Przyznawanie kontu usługi SQL Server (MSSQLSERVER) hello z SE_MANAGE_VOLUME_NAME i dodaj go toohello **wykonywać zadania konserwacji woluminów** zasady zabezpieczeń. Jeśli używasz obrazu platformy programu SQL Server na platformie Azure, hello domyślnego konta usługi (NT Service\MSSQLSERVER) nie jest dodawany toohello **wykonywać zadania konserwacji woluminów** zasady zabezpieczeń. Innymi słowy inicjowanie błyskawicznych plików nie jest włączona w obrazie platformy Azure serwera SQL. Po dodaniu toohello konta usługi programu SQL Server hello **wykonywać zadania konserwacji woluminów** zasady zabezpieczeń, usługi SQL Server hello ponownego uruchomienia. Może to być zagadnienia dotyczące zabezpieczeń dla tej funkcji. Aby uzyskać więcej informacji, zobacz [Inicjowanie plików bazy danych](https://msdn.microsoft.com/library/ms175935.aspx).

* **Automatyczne zwiększanie** jest uznawany za toobe jedynie awaryjnych nieoczekiwany wzrost. Nie zarządzania rozwojem danych i dziennika na podstawie bieżącego z automatycznego przyrostu. Jeśli używane jest automatyczne zwiększanie, wstępnie rosnąć hello pliku za pomocą przełącznika rozmiar hello.

* Upewnij się, że **autoshrink** jest zmniejszenie niepotrzebnych tooavoid wyłączone, który może negatywnie wpłynąć na wydajność.

* Przenieś wszystkie dyski toodata baz danych, w tym systemowych baz danych. Aby uzyskać więcej informacji, zobacz [przenoszenia baz danych systemu](https://msdn.microsoft.com/library/ms345408.aspx).

* Przenieś programu SQL Server błąd dziennika i śledzenia katalogów toodata dyski z plikami. Można to zrobić w programie SQL Server Configuration Manager przez kliknięcie prawym przyciskiem myszy wystąpienie programu SQL Server i wybierz opcję Właściwości. Witaj ustawienia pliku dziennika i śledzenia błędów można zmienić w programie hello **Parametry uruchamiania** hello kartę w hello określono katalog zrzutu **zaawansowane** hello kartę po zrzut ekranu przedstawia where toolook dla parametr uruchamiania Hello błędu dziennika.

    ![Zrzut ekranu dziennik błędów programu SQL](./media/virtual-machines-windows-sql-performance/sql_server_error_log_location.png)

* Ustawienia domyślne lokalizacje plików kopii zapasowej i bazy danych. Użyj hello zalecenia w tym temacie, a zmiany hello w oknie właściwości powitania serwera. Aby uzyskać instrukcje, zobacz [hello Wyświetl lub zmień domyślne lokalizacje dla danych i plików dziennika (SQL Server Management Studio)](https://msdn.microsoft.com/library/dd206993.aspx). Witaj Poniższy zrzut ekranu pokazuje, gdzie toomake tych zmian.

    ![Pliki dziennika danych SQL i tworzenie kopii zapasowych](./media/virtual-machines-windows-sql-performance/sql_server_default_data_log_backup_locations.png)
* Włącz zablokowany tooreduce stron we/wy i żadnych działań stronicowania. Aby uzyskać więcej informacji, zobacz [włączyć hello blokowanie stron w pamięci (system Windows) — opcja](https://msdn.microsoft.com/library/ms190730.aspx).

* Jeśli używasz programu SQL Server 2012, należy zainstalować Service Pack 1 aktualizacją zbiorczą 10. Ta aktualizacja zawiera poprawkę hello niską wydajność We/Wy podczas wykonywania wybierz w instrukcji tabeli tymczasowej w programie SQL Server 2012. Aby uzyskać informacje, zobacz [artykułu bazy wiedzy](http://support.microsoft.com/kb/2958012).

* Należy rozważyć kompresowania wszystkie pliki danych podczas przesyłania We/Wy systemu Azure.

## <a name="feature-specific-guidance"></a>Funkcja dokładne wskazówki

Niektóre wdrożenia może osiągnięcia korzyści dodatkowe wydajności za pomocą bardziej zaawansowanych technik konfiguracji. Witaj poniżej prezentuje niektóre funkcje programu SQL Server, które mogą pomóc Ci lepszą wydajność tooachieve:

* **Kopia zapasowa magazynu tooAzure**: podczas wykonywania kopii zapasowych programu SQL Server uruchomionego na maszynach wirtualnych Azure, można użyć [tooURL kopii zapasowej programu SQL Server](https://msdn.microsoft.com/library/dn435916.aspx). Ta funkcja jest dostępnych w programie SQL Server 2012 z dodatkiem SP1 CU2 i zalecane do wykonywania kopii zapasowych dysków z danymi toohello dołączony. Gdy możesz wykonywania kopii zapasowej/przywracania do/z magazynu Azure, wykonaj zalecenia hello zawarte w [kopii zapasowej serwera SQL tooURL najlepsze rozwiązania i rozwiązywanie problemów i przywracanie z kopii zapasowych przechowywanych w magazynie Azure](https://msdn.microsoft.com/library/jj919149.aspx). Można również zautomatyzować te kopie zapasowe przy użyciu [automatyczna usługa Backup dla programu SQL Server w usłudze Azure Virtual Machines](virtual-machines-windows-sql-automated-backup.md).

    Wcześniejsze tooSQL Server 2012, można użyć [tooAzure kopii zapasowej programu SQL Server narzędzia](https://www.microsoft.com/download/details.aspx?id=40740). To narzędzie ułatwia tooincrease przepustowość kopii zapasowej za pomocą wielu cele stripe kopii zapasowej.

* **Pliki danych programu SQL Server na platformie Azure**: Ta nowa funkcja [plików danych programu SQL Server na platformie Azure](https://msdn.microsoft.com/library/dn385720.aspx), jest dostępnych w programie SQL Server 2014. Programem SQL Server z plików danych na platformie Azure przedstawiono charakterystyki wydajności można porównywać pod względem jako za pomocą dysków danych Azure.

## <a name="next-steps"></a>Następne kroki

Aby uzyskać najlepsze rozwiązania w zakresie zabezpieczeń, zobacz [zagadnienia dotyczące zabezpieczeń dla programu SQL Server w usłudze Azure Virtual Machines](virtual-machines-windows-sql-security.md).

Przejrzyj inne tematy maszyny wirtualnej programu SQL Server na [programu SQL Server na omówienia maszyn wirtualnych Azure](virtual-machines-windows-sql-server-iaas-overview.md).
