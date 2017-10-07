---
title: "dyski aaaExclude z ochrony za pomocą usługi Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "Opisuje, dlaczego i w jaki sposób tooexclude maszyny Wirtualnej dyski z replikacji w scenariuszach VMware tooAzure i tooAzure funkcji Hyper-V."
services: site-recovery
documentationcenter: 
author: nsoneji
manager: garavd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 06/05/2017
ms.author: nisoneji
ms.openlocfilehash: f47146bc57aeab3fce90123d0894fa86dde93417
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="exclude-disks-from-replication"></a>Wykluczanie dysków z replikacji
W tym artykule opisano, jak tooexclude dyski z replikacji. To wykluczenie można zoptymalizować przepustowości replikacji hello używane lub optymalizacji zasobów po stronie docelowej hello, które korzystają z tych dysków. Funkcja Hello jest obsługiwana w scenariuszach VMware tooAzure i tooAzure funkcji Hyper-V.

## <a name="prerequisites"></a>Wymagania wstępne

Domyślnie wszystkie dyski na maszynie są replikowane. tooexclude dysku z replikacji należy ręcznie zainstalować hello usługi mobilności na maszynie hello przed włączeniem replikacji w przypadku replikowania VMware tooAzure.


## <a name="why-exclude-disks-from-replication"></a>Dlaczego wykluczać dyski z replikacji?
Wykluczenie dysków z replikacji jest często konieczne, ponieważ:

- dane Hello jest churned na dysku hello wykluczone nie są ważne lub nie wymaga toobe replikowane.

- Ma toosave magazynu i zasobów sieciowych przez ten zmian nie będą replikowane.

## <a name="what-are-hello-typical-scenarios"></a>Jakie są typowe scenariusze hello?
Możliwe jest wskazanie konkretnych przykładów zmian danych, które świetnie nadają się do wykluczenia. Przykłady może obejmować zapisuje plik stronicowania tooa (pagefile.sys) i zapisuje plik bazy danych tempdb toohello programu Microsoft SQL Server. W zależności od obciążenia hello i podsystemu magazynowania hello pliku stronicowania hello można zarejestrować znaczną ilość danych churn. Jednak replikacji tych danych ze hello tooAzure lokacji głównej będzie wymagać wielu zasobów. W związku z tym program hello następujące kroki toooptimize replikacji maszyny wirtualnej z jednego dysk wirtualny, który ma zarówno hello systemu operacyjnego, jak i plik stronicowania hello:

1. Podziel hello jednego dysku wirtualnego na dwa dyski wirtualne. Jeden dysk wirtualny ma hello systemu operacyjnego, a hello innych ma hello pliku stronicowania.
2. Wykluczanie dysku z plikiem stronicowania hello z replikacji.

Podobnie można użyć hello następujące kroki toooptimize dysku, który ma zarówno tempdb programu Microsoft SQL Server hello pole i hello plik systemowej bazy danych:

1. Zachowaj hello systemowej bazy danych i bazy danych tempdb na dwóch różnych dyskach.
2. Wykluczanie dysku bazy danych tempdb hello z replikacji.

## <a name="how-tooexclude-disks-from-replication"></a>Jak tooexclude dyski z replikacji?

### <a name="vmware-tooazure"></a>VMware tooAzure
Wykonaj hello [włączyć replikację](site-recovery-vmware-to-azure.md) tooprotect przepływu pracy maszyny wirtualnej z portalu usługi Azure Site Recovery hello. W hello czwarty krok hello przepływu pracy, użyj hello **tooREPLICATE dysku** dysków tooexclude kolumny z replikacji. Domyślnie do replikacji są wybierane wszystkie dyski. Wyczyść pole wyboru hello dysków, które mają tooexclude z replikacji, a następnie pełne hello kroki tooenable replikacji.

![Wyklucz z replikacji dyski i włączyć replikację VMware tooAzure powrotu po awarii](./media/site-recovery-exclude-disk/v2a-enable-replication-exclude-disk1.png)


>[!NOTE]
>
> * Można wykluczyć tylko dyski, które już zostały zainstalowane usługi mobilności hello. Należy toomanually instalacji usługi mobilności hello, ponieważ hello usługa mobilności jest instalowany tylko przy użyciu mechanizmu wypychania powitania po włączeniu replikacji.
> * Tylko dyski podstawowe można wyłączyć z replikacji. Nie możesz wykluczać dysków systemu operacyjnego ani dysków dynamicznych.
> * Po włączeniu replikacji nie możesz dodawać dysków do replikacji ani ich usuwać. Tooadd lub wykluczyć dysk, wymagają ochrony toodisable hello maszyny i włącz ją ponownie.
> * Jeśli można wykluczyć dysku, który jest potrzebna dla toooperate aplikacji po tooAzure trybu failover, konieczne będzie toocreate hello dysk ręcznie w systemie Azure, co umożliwia uruchamianie aplikacji hello replikowane. Alternatywnie można zintegrować usługi Automatyzacja Azure dysku hello toocreate planu odzyskiwania w trybie failover hello maszyny.
> * Maszyna wirtualna z systemem Windows: Dyski utworzone ręcznie na platformie Azure nie mają możliwości powrotu po awarii. Jeśli na przykład przełączysz w tryb failover trzy dyski i utworzysz dwa bezpośrednio w usłudze Azure Virtual Machines, powrót po awarii nastąpi tylko dla trzech dysków przełączonych w tryb failover. Nie można dołączyć dyski, które zostały utworzone ręcznie w przypadku powrotu po awarii lub ponownej ochrony z lokalnymi tooAzure.
> * Maszyna wirtualna z systemem Linux: Dyski utworzone ręcznie na platformie Azure są uwzględniane podczas powrotu po awarii. Jeśli na przykład przełączysz w tryb failover trzy dyski i utworzysz dwa bezpośrednio w usłudze Azure Virtual Machines, powrót po awarii nastąpi dla wszystkich pięciu dysków. Dysków utworzonych ręcznie nie możesz wykluczyć z powrotu po awarii.
>

### <a name="hyper-v-tooazure"></a>TooAzure funkcji Hyper-V
Wykonaj hello [włączyć replikację](site-recovery-hyper-v-site-to-azure.md) tooprotect przepływu pracy maszyny wirtualnej z portalu usługi Azure Site Recovery hello. W hello czwarty krok hello przepływu pracy, użyj hello **tooREPLICATE dysku** dysków tooexclude kolumny z replikacji. Domyślnie do replikacji są wybierane wszystkie dyski. Wyczyść pole wyboru hello dysków, które mają tooexclude z replikacji, a następnie pełne hello kroki tooenable replikacji.

![Wyklucz z replikacji dyski i włączyć replikację funkcji Hyper-V tooAzure powrotu po awarii](./media/site-recovery-vmm-to-azure/enable-replication6-with-exclude-disk.png)

>[!NOTE]
>
> * Z replikacji możesz wykluczyć tylko dyski podstawowe. Nie możesz wykluczać dysków systemu operacyjnego. Nie zalecamy wykluczania dysków dynamicznych. Usługa Azure Site Recovery nie może zidentyfikować, który wirtualny dysk twardy (VHD) jest podstawowych lub dynamicznych w maszynie wirtualnej typu Gość hello.  Jeśli wszystkie dyski woluminu dynamicznego zależnego nie są wyłączone, chroniony dysk dynamiczny hello staje się uszkodzony dysk na maszynie wirtualnej trybu failover i hello danych na tym dysku nie jest dostępny.
> * Po włączeniu replikacji nie możesz dodawać dysków do replikacji ani ich usuwać. Tooadd lub wykluczyć dysk, wymagają ochrony toodisable hello maszyny wirtualnej i włącz ją ponownie.
> * Jeśli dysk jest potrzebna dla toooperate aplikacji zostaną wykluczone, po tooAzure pracy awaryjnej należy toocreate hello dysk ręcznie w systemie Azure, co umożliwia uruchamianie aplikacji hello replikowane. Alternatywnie można zintegrować usługi Automatyzacja Azure dysku hello toocreate planu odzyskiwania w trybie failover hello maszyny.
> * Dyski utworzone ręcznie na platformie Azure nie mają możliwości powrotu po awarii. Na przykład jeśli się nie powieść ponad trzy dyski i utworzyć dwa dyski bezpośrednio w usłudze Azure Virtual Machines, tylko trzy dyski, które zostały przełączone do trybu failover nie powiedzie się z tooHyper Azure-V. Nie można dołączyć dyski, które zostały utworzone ręcznie w przypadku powrotu po awarii lub replikacji odwrotnej z tooAzure funkcji Hyper-V.



## <a name="end-to-end-scenarios-of-exclude-disks"></a>Kompleksowe scenariusze wykluczania dysków
Teraz należy wziąć pod uwagę dwa scenariusze toounderstand hello Wyklucz dysku funkcji:

- Dysk bazy danych tempdb programu SQL Server
- Dysk pliku stronicowania (pagefile.sys)

### <a name="exclude-hello-sql-server-tempdb-disk"></a>Wykluczanie dysku bazy danych tempdb serwera SQL hello
Rozważmy maszynę wirtualną programu SQL Server z bazą danych tempdb, którą można wykluczyć.

Nazwa Hello hello dysku wirtualnego jest SalesDB.

Dyski na powitania źródłowej maszyny wirtualnej są następujące:


**Nazwa dysku** | **Nr dysku systemu operacyjnego gościa** | **Litera dysku** | **Typ danych na dysku hello**
--- | --- | --- | ---
DB-Disk0-OS | DYSK0 | C:\ | Dysk systemu operacyjnego
DB-Disk1| Dysk1 | D:\ | Systemowa baza danych SQL i baza danych użytkownika 1
DB — Disk2 (dysk hello wykluczone z ochrony) | Dysk2 | E:\ | Pliki tymczasowe
DB — Disk3 (dysk hello wykluczone z ochrony) | Dysk3 | F:\ | Baza danych SQL bazy danych tempdb (ścieżka folderu (F:\MSSQL\Data\) < /br/>< /br/>, Zanotuj ścieżkę folderu hello przed trybu failover.
DB-Disk4 | Dysk4 |G:\ |Baza danych użytkownika 2

Przenoszenie danych na dwóch dysków maszyny wirtualnej hello jest tymczasowy, podczas ochrony maszyny wirtualnej SalesDB hello, Disk2 i Disk3 można wykluczyć z replikacji. Usługa Azure Site Recovery nie będzie replikować tych dysków. W tryb failover tych dysków nie będą obecne na maszynie wirtualnej trybu failover hello na platformie Azure.

Dyski na powitania maszyny wirtualnej platformy Azure po trybu failover są następujące:

**Nr dysku systemu operacyjnego gościa** | **Litera dysku** | **Typ danych na dysku hello**
--- | --- | ---
DYSK0 | C:\ | Dysk systemu operacyjnego
Dysk1 | E:\ | Magazyn tymczasowy < /br / >< /br / > Azure dodaje ten dysk i przypisuje hello pierwszą dostępną literę dysku.
Dysk2 | D:\ | Systemowa baza danych SQL i baza danych użytkownika 1
Dysk3 | G:\ | Baza danych użytkownika 2

Ponieważ Disk2 i Disk3 zostały wykluczone z maszyny wirtualnej SalesDB hello, E: jest hello pierwszą literę dysku z listy dostępnych hello. Azure przypisuje woluminie magazynu tymczasowego toohello E:. Dla wszystkich dysków hello replikowane pozostają litery dysku hello hello takie same.

Disk3, która była hello SQL bazy danych tempdb dysku (ścieżka folderu bazy danych tempdb F:\MSSQL\Data\), został wykluczony z replikacji. Witaj dysk nie jest dostępne na maszynie wirtualnej hello trybu failover. W związku z tym hello usługi SQL jest w stanie zatrzymania, i musi hello F:\MSSQL\Data ścieżki.

Istnieją dwa sposoby toocreate tej ścieżki:

- Dodaj nowy dysk i przypisz ścieżkę folderu bazy danych tempdb.
- Użyj istniejącego dysku magazynu tymczasowego dla ścieżki folderu hello bazy danych tempdb.

#### <a name="add-a-new-disk"></a>Dodaj nowy dysk:

1. Zapisz ścieżek hello SQL tempdb.mdf oraz tempdb.ldf przed trybu failover.
2. Z hello portalu Azure Dodaj nowy dysk toohello trybu failover maszyny wirtualnej z hello tej samej lub więcej rozmiar jak hello źródła SQL bazy danych tempdb dysku (Disk3).
3. Zaloguj się toohello maszyny wirtualnej platformy Azure. Za pomocą konsoli zarządzania (diskmgmt.msc) dysku hello inicjowanie i formatowanie hello nowo dodanych dysków.
4. Przypisz hello sama litera użytej przez hello SQL bazy danych tempdb dysku (F:).
5. Utwórz folder bazy danych tempdb na powitania woluminu F: (F:\MSSQL\Data).
6. Uruchom usługę SQL hello z konsoli usługi hello.

#### <a name="use-an-existing-temporary-storage-disk-for-hello-sql-tempdb-folder-path"></a>Użyj istniejącego dysku magazynu tymczasowego dla ścieżki folderu bazy danych tempdb SQL hello:

1. Otwórz wiersz polecenia.
2. Uruchom program SQL Server w trybie odzyskiwania, w wierszu polecenia hello.

        Net start MSSQLSERVER /f / T3608

3. Uruchom hello następujące narzędzia sqlcmd toochange hello tempdb ścieżki toohello nowej ścieżki.

        sqlcmd -A -S SalesDB        **Use your SQL DBname**
        USE master;     
        GO      
        ALTER DATABASE tempdb       
        MODIFY FILE (NAME = tempdev, FILENAME = 'E:\MSSQL\tempdata\tempdb.mdf');
        GO      
        ALTER DATABASE tempdb       
        MODIFY FILE (NAME = templog, FILENAME = 'E:\MSSQL\tempdata\templog.ldf');       
        GO


4. Zatrzymać hello usług Microsoft SQL Server.

        Net stop MSSQLSERVER
5. Uruchom usługę Microsoft SQL Server hello.

        Net start MSSQLSERVER

Można znaleźć toohello następujące wytyczne Azure dla dysku magazynu tymczasowego:

* [Przy użyciu dysków SSD w maszynach wirtualnych platformy Azure toostore TempDB serwera SQL i rozszerzenia puli buforów](https://blogs.technet.microsoft.com/dataplatforminsider/2014/09/25/using-ssds-in-azure-vms-to-store-sql-server-tempdb-and-buffer-pool-extensions/)
* [Najlepsze rozwiązania w zakresie wydajności dla programu SQL Server w usłudze Azure Virtual Machines](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-performance)

### <a name="failback-from-azure-tooan-on-premises-host"></a>Powrót po awarii (z hosta lokalnego Azure tooan)
Teraz Przyjrzyjmy się hello dysków, które są replikowane w trybie failover z lokalnymi Azure tooyour hosta VMware lub funkcji Hyper-V. Dyski utworzone ręcznie na platformie Azure nie będą replikowane. Jeśli na przykład przełączysz w tryb failover trzy dyski i utworzysz dwa bezpośrednio w usłudze Azure Virtual Machines, powrót po awarii nastąpi tylko dla trzech dysków przełączonych w tryb failover. Nie można dołączyć dyski, które zostały utworzone ręcznie w przypadku powrotu po awarii lub ponownej ochrony z lokalnymi tooAzure. On również nie jest replikowany hello magazyn tymczasowy dysku lokalnego tooon hostów.

#### <a name="failback-toooriginal-location-recovery"></a>Odzyskiwanie do lokalizacji toooriginal powrotu po awarii

W poprzednim przykładzie hello konfigurację dysku maszyny wirtualnej platformy Azure hello jest następujący:

**Nr dysku systemu operacyjnego gościa** | **Litera dysku** | **Typ danych na dysku hello**
--- | --- | ---
DYSK0 | C:\ | Dysk systemu operacyjnego
Dysk1 | E:\ | Magazyn tymczasowy < /br / >< /br / > Azure dodaje ten dysk i przypisuje hello pierwszą dostępną literę dysku.
Dysk2 | D:\ | Systemowa baza danych SQL i baza danych użytkownika 1
Dysk3 | G:\ | Baza danych użytkownika 2


#### <a name="vmware-tooazure"></a>VMware tooAzure
Po zakończeniu powrotu po awarii toohello oryginalnej lokalizacji konfigurację dysku maszyny wirtualnej na powrót po awarii hello nie ma dysków. Dyski, które zostały wykluczone z VMware tooAzure nie będą dostępne na maszynie wirtualnej hello powrotu po awarii.

Po planowanego trybu failover z Azure lokalnych tooon VMware dyski na maszynie wirtualnej VMWare hello (oryginalnej lokalizacji) są następujące:

**Nr dysku systemu operacyjnego gościa** | **Litera dysku** | **Typ danych na dysku hello**
--- | --- | ---
DYSK0 | C:\ | Dysk systemu operacyjnego
Dysk1 | D:\ | Systemowa baza danych SQL i baza danych użytkownika 1
Dysk2 | G:\ | Baza danych użytkownika 2

#### <a name="hyper-v-tooazure"></a>TooAzure funkcji Hyper-V
W przypadku powrotu po awarii jest toohello oryginalnej lokalizacji, hello powrotu po awarii maszyny wirtualnej dysku konfiguracji pozostaje hello takie same jak oryginalną konfigurację dysku maszyny wirtualnej funkcji Hyper-v. Dyski, które zostały wykluczone z tooAzure lokacji funkcji Hyper-V są dostępne na maszynie wirtualnej hello powrotu po awarii.

Po zaplanowanym tryb failover z Azure tooon lokalnym funkcji Hyper-V dyski na maszynie wirtualnej funkcji Hyper-V hello (oryginalnej lokalizacji) są następujące:

**Nazwa dysku** | **Nr dysku systemu operacyjnego gościa** | **Litera dysku** | **Typ danych na dysku hello**
--- | --- | --- | ---
DB-Disk0-OS | DYSK0 |   C:\ | Dysk systemu operacyjnego
DB-Disk1 | Dysk1 | D:\ | Systemowa baza danych SQL i baza danych użytkownika 1
DB-Disk2 (dysk wykluczony) | Dysk2 | E:\ | Pliki tymczasowe
DB-Disk3 (dysk wykluczony) | Dysk3 | F:\ | Baza danych SQL tempdb — ścieżka folderu (F:\MSSQL\Data\)
DB-Disk4 | Dysk4 | G:\ | Baza danych użytkownika 2


#### <a name="exclude-hello-paging-file-pagefilesys-disk"></a>Wyklucz hello stronicowania na dysku z plikiem (pagefile.sys)

Rozważmy maszynę wirtualną zawierającą dysk z plikiem stronicowania, który można wykluczyć.
Są dwa przypadki.

#### <a name="case-1-hello-paging-file-is-configured-on-hello-d-drive"></a>Przypadek 1: plik stronicowania hello jest skonfigurowany na powitania dysku D:
W tym miejscu jest konfiguracja dysków hello:


**Nazwa dysku** | **Nr dysku systemu operacyjnego gościa** | **Litera dysku** | **Typ danych na dysku hello**
--- | --- | --- | ---
DB-Disk0-OS | DYSK0 | C:\ | Dysk systemu operacyjnego
Dysk bazy danych — 1 (dysk hello wykluczone z ochrony hello) | Dysk1 | D:\ | pagefile.sys
DB-Disk2 | Dysk2 | E:\ | Dane użytkowników 1
DB-Disk3 | Dysk3 | F:\ | Dane użytkowników 2

Poniżej przedstawiono hello rozmiaru pliku stronicowania na powitania źródłowej maszyny wirtualnej:

![Ustawienia pliku stronicowania na źródłowej maszynie wirtualnej](./media/site-recovery-exclude-disk/pagefile-on-d-drive-sourceVM.png)


Po pracy w trybie failover hello maszynę wirtualną z VMware tooAzure lub tooAzure funkcji Hyper-V dyski na powitania maszyny wirtualnej platformy Azure są następujące:

**Nazwa dysku** | **Nr dysku systemu operacyjnego gościa** | **Litera dysku** | **Typ danych na dysku hello**
--- | --- | --- | ---
DB-Disk0-OS | DYSK0 | C:\ | Dysk systemu operacyjnego
DB-Disk1 | Dysk1 | D:\ | Magazyn tymczasowy</br /> </br />pagefile.sys
DB-Disk2 | Dysk2 | E:\ | Dane użytkowników 1
DB-Disk3 | Dysk3 | F:\ | Dane użytkowników 2

Ponieważ dysk 1 (D:) został wykluczony, D: jest hello pierwszą literę dysku z listy dostępnych hello. Azure przypisuje woluminie magazynu tymczasowego toohello D:. Ponieważ D: jest dostępna na powitania maszyny wirtualnej platformy Azure, hello ustawienia rozmiaru pliku stronicowania pozostaje maszyny wirtualnej hello hello takie same.

Poniżej przedstawiono hello rozmiaru pliku stronicowania na powitania maszyny wirtualnej platformy Azure:

![Ustawienia pliku stronicowania na maszynie wirtualnej platformy Azure](./media/site-recovery-exclude-disk/pagefile-on-Azure-vm-after-failover.png)

#### <a name="case-2-hello-paging-file-is-configured-on-another-drive-other-than-d-drive"></a>Przypadek 2: plik stronicowania hello jest skonfigurowany na innym dysku (innym niż dysk D:)

Poniżej przedstawiono konfigurację dysku maszyny wirtualnej źródłowego hello:

**Nazwa dysku** | **Nr dysku systemu operacyjnego gościa** | **Litera dysku** | **Typ danych na dysku hello**
--- | --- | --- | ---
DB-Disk0-OS | DYSK0 | C:\ | Dysk systemu operacyjnego
Dysk bazy danych — 1 (dysk hello wykluczone z ochrony) | Dysk1 | G:\ | pagefile.sys
DB-Disk2 | Dysk2 | E:\ | Dane użytkowników 1
DB-Disk3 | Dysk3 | F:\ | Dane użytkowników 2

Poniżej przedstawiono hello rozmiaru pliku stronicowania na powitania na lokalnej maszynie wirtualnej:

![Ustawienia pliku na maszynie wirtualnej lokalne powitania stronicowania](./media/site-recovery-exclude-disk/pagefile-on-g-drive-sourceVM.png)

Po pracy w trybie failover maszyny wirtualnej hello z tooAzure VMware/funkcji Hyper-V dyski na powitania maszyny wirtualnej platformy Azure są następujące:

**Nazwa dysku**| **Nr dysku systemu operacyjnego gościa**| **Litera dysku** | **Typ danych na dysku hello**
--- | --- | --- | ---
DB-Disk0-OS | DYSK0  |C:\ |Dysk systemu operacyjnego
DB-Disk1 | Dysk1 | D:\ | Magazyn tymczasowy</br /> </br />pagefile.sys
DB-Disk2 | Dysk2 | E:\ | Dane użytkowników 1
DB-Disk3 | Dysk3 | F:\ | Dane użytkowników 2

Ponieważ D: hello pierwszą literę dysku z listy dostępnych hello, Azure przypisuje woluminie magazynu tymczasowego toohello D:. Dla wszystkich dysków hello replikowane pozostaje litery dysku hello hello takie same. Ponieważ hello G: dysku nie jest dostępna, hello system będzie używać dysku C: hello hello plik stronicowania.

Poniżej przedstawiono hello rozmiaru pliku stronicowania na powitania maszyny wirtualnej platformy Azure:

![Ustawienia pliku stronicowania na maszynie wirtualnej platformy Azure](./media/site-recovery-exclude-disk/pagefile-on-Azure-vm-after-failover-2.png)

## <a name="next-steps"></a>Następne kroki
Po skonfigurowaniu i uruchomieniu wdrożenia [dowiedz się więcej](site-recovery-failover.md) o różnych typach trybu failover.
