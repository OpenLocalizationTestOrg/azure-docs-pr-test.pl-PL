---
title: "aaaHigh wydajności magazyn w warstwie Premium i Azure zarządzane dyski dla maszyn wirtualnych | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o wysokiej wydajności Premium Storage i dysków zarządzanych w maszynach wirtualnych Azure. Azure serii DS, DSv2 serii, serie GS i maszyn wirtualnych serii Fs obsługuje usługi Premium Storage."
services: storage
documentationcenter: 
author: ramankumarlive
manager: aungoo-msft
editor: tysonn
ms.assetid: e2a20625-6224-4187-8401-abadc8f1de91
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: ramankum
ms.openlocfilehash: 5f08e615869ed59a9d80d798ec191dd4d3abc3e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="high-performance-premium-storage-and-managed-disks-for-vms"></a>Magazyn w warstwie Premium wysokiej wydajności i zarządzane dyski dla maszyn wirtualnych
Usługa Azure Premium Storage oferuje obsługę dysków o wysokiej wydajności i małych opóźnieniach maszynach wirtualnych (VM) z wejścia/wyjścia (We/Wy)-intensywnych obciążeń. Dyski maszyn wirtualnych, które używają magazyn w warstwie Premium przechowywania danych na dyskach półprzewodnikowych (SSD). Zaletą tootake hello szybkości i wydajności dysków w warstwie premium magazynu można przeprowadzić migrację istniejącej maszyny Wirtualnej tooPremium dyski magazynu.

Na platformie Azure możesz dołączyć kilka premium magazynu dysków tooa maszyny Wirtualnej. Za pomocą wielu dysków daje aplikacji zapasowej too256 TB magazynu dla maszyny Wirtualnej. Z magazyn w warstwie Premium aplikacje można osiągnąć 80 000 operacji We/Wy na sekundę (IOPS) dla maszyny Wirtualnej i przepustowości dysków zapasowych too2, 000 MB na sekundę (MB/s) dla maszyny Wirtualnej. Operacje odczytu zapewniają bardzo małych opóźnień.

Z magazyn w warstwie Premium Azure oferuje możliwości hello tootruly przyrostu shift wymagających przedsiębiorstwa aplikacjach, takich jak chmury toohello farm Dynamics AX, Dynamics CRM, Exchange Server, SAP Business pakietu i programu SharePoint. Można uruchomić obciążeń intensywnie wydajności bazy danych w aplikacjach, takich jak SQL Server, Oracle, bazy danych MongoDB, MySQL i pamięci podręcznej Redis, wymagających wysoką wydajność i małe opóźnienia.

> [!NOTE]
> W hello najlepszą wydajność aplikacji zaleca się przeprowadzenie migracji dysku maszyny Wirtualnej, który wymaga wysokiej tooPremium IOPS magazynu. Jeśli dysk nie wymaga wysokiej IOPS, może pomóc limit kosztów, przechowując go w usłudze Azure standard Storage. W magazynie standardowa maszyna wirtualna dysku dane są przechowywane na dysków twardych (HDD) zamiast na dyskach SSD.
> 

Azure oferuje dwa sposoby dyski magazynu premium toocreate dla maszyn wirtualnych:

* **Dyski niezarządzane**

    Metoda oryginalnego Hello jest dysków toouse niezarządzanych. Niezarządzane dysku możesz zarządzać hello kont magazynu, aby używać toostore hello wirtualnego dysku twardego (VHD) plików, które odpowiadają tooyour dysków maszyny Wirtualnej. Pliki VHD są przechowywane jako stronicowe obiekty BLOB na kontach magazynu Azure. 

* **Dyski zarządzane**

    Po wybraniu [dysków zarządzanych Azure](../../virtual-machines/windows/managed-disks-overview.md), Azure zarządza kontami magazynu hello, których używasz dla dysków maszyny Wirtualnej. Należy określić typ dysku hello (Premium lub Standard) i hello rozmiar dysku hello, które są potrzebne. Azure tworzy i którymi zarządza hello dysku dla Ciebie. Nie masz tooworry o umieszczenie hello dysków w wielu tooensure kont magazynu pozostać w limity skalowalności dla kont magazynu. Azure obsługuje który dla Ciebie.

Zaleca się wybranie dysków zarządzanych, tootake zalety ich wielu funkcji.

tooget pracy z magazynem Premium [utworzyć bezpłatne konto platformy Azure](https://azure.microsoft.com/pricing/free-trial/). 

Informacji o migracji istniejącej tooPremium maszyn wirtualnych magazynu, zobacz [Konwertuj Maszynę wirtualną systemu Windows z dysków toomanaged niezarządzane dysków](../../virtual-machines/windows/convert-unmanaged-to-managed-disks.md) lub [Konwertuj Maszynę wirtualną systemu Linux z dysków toomanaged niezarządzane dysków](../../virtual-machines/linux/convert-unmanaged-to-managed-disks.md).

> [!NOTE]
> Magazyn w warstwie Premium jest dostępna w większości regionów. Hello lista dostępnych regionów w [usług Azure według regionu](https://azure.microsoft.com/regions/#services), obejrzyj hello regionów, w których obsługiwane maszyny wirtualne z serii rozmiar pomocy technicznej Premium (serii DS, DSV2 serii GS-series i Fs serii maszyn wirtualnych) są obsługiwane.
> 

## <a name="features"></a>Funkcje

Poniżej przedstawiono niektóre funkcje hello magazyn w warstwie Premium:

* **Dyski magazynu w warstwie Premium**

    Dyski maszyny Wirtualnej obsługuje magazynu Premium, które można dołączyć toospecific rozmiar serii maszyn wirtualnych. Magazyn w warstwie Premium obsługuje serii DS, DSv2 serii GS-serii, serie Ls i Fs serii maszyn wirtualnych. Masz do wyboru rozmiary dysków siedem: P4 (32GB) P6 (64GB), P10 (128 MB), P20 (512GB), P30 (1024GB), P40 (2048GB), P50 (4095GB). P4 i rozmiary dysków P6 są jeszcze obsługiwane tylko w przypadku dysków zarządzanych. Rozmiar każdego dysku ma specyfikacjami wydajności. W zależności od wymagań aplikacji można dołączyć co najmniej jeden tooyour dysków maszyny Wirtualnej. Przedstawione specyfikacje hello bardziej szczegółowo w [magazyn w warstwie Premium cele wydajności i skalowalności](#scalability-and-performance-targets).

* **Stronicowe — wersja Premium**

    Magazyn w warstwie Premium obsługuje stronicowych obiektów blob. Użyj stronicowe obiekty BLOB toostore trwałe niezarządzane dysków dla maszyn wirtualnych w warstwie Premium Storage. W przeciwieństwie do standardowego magazynu Azure magazyn w warstwie Premium nie obsługuje blokowe obiekty BLOB, Dołącz obiektów blob, plików, tabel lub kolejek. Stronicowe Premium obsługuje sześciu rozmiary P10 tooP50 i P60 (8191GiB). P60 Premium stronicowych obiektów blob nie jest obsługiwane toobe dołączone jako dyski maszyny Wirtualnej. 

    Dowolny obiekt umieszczony na koncie magazynu premium będzie stronicowych obiektów blob. Witaj stronicowych obiektów blob przyciąganie tooone hello obsługiwane rozmiary elastycznie. Jest to, dlaczego konto magazynu w warstwie premium nie jest przeznaczona toobe używanych toostore niewielki rozmiar obiektów blob.

* **Konto magazynu w warstwie Premium**

    toostart przy użyciu magazyn w warstwie Premium, Utwórz konto magazynu premium dla niezarządzanego dysków. W hello [portalu Azure](https://portal.azure.com), toocreate premium konta magazynu, wybierz hello **Premium** warstwę wydajności. Wybierz hello **magazyn lokalnie nadmiarowy (LRS)** opcji replikacji. Można również tworzyć konta magazynu premium przez ustawienie typu hello zbyt**Premium_LRS** w jednym z następujących lokalizacji hello:
    * [Interfejs API REST magazynu](https://docs.microsoft.com/rest/api/storageservices/Azure-Storage-Services-REST-API-Reference) (wersji 2014-02-14 lub nowszy)
    * [Interfejs API REST zarządzania usługami](http://msdn.microsoft.com/library/azure/ee460799.aspx) (w wersji 2014-10-01 lub nowszej wersji dla platformy Azure w przypadku wdrożeń klasycznych)
    * [Azure API REST dostawcy zasobów magazynu](https://docs.microsoft.com/rest/api/storagerp) (w przypadku wdrożenia usługi Azure Resource Manager)
    * [Program Azure PowerShell](/powershell/azureps-cmdlets-docs.md) (wersja 0.8.10 lub nowszy)

    toolearn temat limitów konta magazynu premium, zobacz [magazyn w warstwie Premium cele wydajności i skalowalności](#premium-storage-scalability-and-performance-targets).

* **Magazyn lokalnie nadmiarowy — wersja Premium**

    Konto magazynu premium obsługuje tylko lokalnie nadmiarowego magazynu jako hello opcji replikacji. Magazyn lokalnie nadmiarowy przechowuje trzy kopie danych hello w pojedynczym regionie. Regionalnej awarii, musisz należy wykonać kopię zapasową dysków maszyny Wirtualnej w innym regionie przy użyciu [kopia zapasowa Azure](../../backup/backup-introduction-to-azure-backup.md). Możesz również użyć konta magazynu geograficznie nadmiarowego (GRS) jako hello magazynu kopii zapasowych. 

    Azure używa konta magazynu jako kontener dla niezarządzanego dysków. Podczas tworzenia Azure serii DS, DSv2 serii GS-series lub serii Fs maszynę Wirtualną za pomocą dysków niezarządzane, a wybierz konto magazynu premium, systemu operacyjnego i dyski danych są przechowywane na tym koncie magazynu.

## <a name="supported-vms"></a>Obsługiwane maszyny wirtualne
Magazyn w warstwie Premium obsługuje serii DS, DSv2 serii GS-serii, serie Ls i Fs serii maszyn wirtualnych. Z tych typów maszyny Wirtualnej służy dyski magazynu standard i premium. Nie można używać dysków premium magazynu serii maszyn wirtualnych, które nie są Premium zgodnych z magazynu.

Aby uzyskać informacje o typach maszyn wirtualnych i rozmiary Azure dla systemu Windows, zobacz [rozmiarów maszyn wirtualnych systemu Windows](../../virtual-machines/virtual-machines-windows-sizes-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Aby uzyskać informacje o typach maszyn wirtualnych i rozmiary na platformie Azure dla systemu Linux, zobacz [rozmiarów maszyn wirtualnych systemu Linux](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Oto niektóre funkcje hello hello: seria DS, DSv2 serii GS-series, Ls serii i Fs serii maszyn wirtualnych:

* **Usługi w chmurze**

    Można dodać maszyny wirtualne z serii DS tooa usługi w chmurze tylko maszyny wirtualne serii DS. Nie należy dodawać maszyny wirtualne z serii DS tooan istniejącą usługę w chmurze o typie innym niż maszyny wirtualne z serii DS. Można migrować istniejące wirtualne dyski twarde tooa nowej usługi w chmurze uruchamiana tylko maszyny wirtualne serii DS. Jeśli chcesz toouse hello tego samego wirtualnego adresu IP dla hello nową usługę w chmurze hostujący maszyny wirtualne z serii DS, użyj [zastrzeżonych adresów IP](../../virtual-network/virtual-networks-instance-level-public-ip.md). GS-series maszyny wirtualne można dodać tooan istniejącej usługi chmury tylko GS-series maszyn wirtualnych.

* **Dysk systemu operacyjnego**

    Można skonfigurować toouse Twojego Premium magazynu z maszyny Wirtualnej — wersja premium lub dysku standardowym systemie operacyjnym. Witaj najlepsze wyniki zaleca się, przy użyciu dysku systemu operacyjnego magazyn w warstwie Premium.

* **Dyski danych**

    Można użyć premium i standardowych dysków w hello tej samej maszyny Wirtualnej z magazynu Premium. Magazyn w warstwie Premium możesz udostępnić Maszynę wirtualną i dołączyć kilka toohello dysków danych maszyny Wirtualnej. W razie potrzeby tooincrease hello pojemność i wydajność woluminu hello można paskowych na dyskach.

    > [!NOTE]
    > Jeśli paskowych dysków w warstwie premium magazynu danych przy użyciu [miejsca do magazynowania](http://technet.microsoft.com/library/hh831739.aspx), skonfiguruj miejsca do magazynowania za pomocą 1 kolumny dla każdego dysku, którego używasz. W przeciwnym razie ogólnej wydajności hello rozkładane woluminu może być mniejsza niż oczekiwano z powodu nierówna Dystrybucja ruchu między dyskami hello. Domyślnie w Menedżerze serwera można skonfigurować kolumn dla zapasowe too8 dysków. Jeśli masz więcej niż 8 dysków, użyj programu PowerShell toocreate hello woluminu. Ręcznie określ hello liczbę kolumn. W przeciwnym razie hello interfejsu użytkownika Menedżera serwera nadal toouse 8 kolumn, nawet jeśli masz więcej dysków. Na przykład jeśli masz 32 dysków w jednej rozłożony określić 32 kolumny. toospecify hello liczbę kolumn hello używa dysku wirtualnego, w hello [New-VirtualDisk](http://technet.microsoft.com/library/hh848643.aspx) polecenia cmdlet programu PowerShell, użyj hello *NumberOfColumns* parametru. Aby uzyskać więcej informacji, zobacz [omówienie funkcji miejsca do magazynowania](http://technet.microsoft.com/library/hh831739.aspx) i [miejsca do magazynowania — często zadawane pytania](http://social.technet.microsoft.com/wiki/contents/articles/11382.storage-spaces-frequently-asked-questions-faq.aspx).
    >
    > 

* **Pamięć podręczna**

    Maszyny wirtualne w hello rozmiar serii, która obsługuje usługi Premium Storage ma unikatowy możliwość buforowania wysokiej przepustowości i opóźnień. Witaj, możliwość buforowania przekracza podstawowej wydajności dysku magazynu premium. Można ustawić dysku hello buforowanie zasad na dyski magazynu premium za**tylko do odczytu**, **ReadWrite**, lub **Brak**. dysk domyślny Hello zasad buforowania jest **tylko do odczytu** dla wszystkich dysków danych — warstwa premium i **ReadWrite** dysków systemu operacyjnego. Aby uzyskać optymalną wydajność aplikacji użyj hello poprawne ustawienie pamięci podręcznej. Na przykład dla dysków z danymi ciężki odczytu lub w trybie tylko do odczytu, takich jak pliki danych programu SQL Server, ustaw dysku hello zasad buforowania zbyt**tylko do odczytu**. Dla danych intensywnie zapisu lub w trybie tylko do zapisu dysków, takich jak pliki dziennika programu SQL Server, ustaw dysku hello zasad buforowania zbyt**Brak**. toolearn więcej informacji na temat optymalizacji projektu z magazyn w warstwie Premium, zobacz [projektu dla wydajności z magazyn w warstwie Premium](storage-premium-storage-performance.md).

* **Analiza**

    wydajność maszyny Wirtualnej tooanalyze przy użyciu dysków w warstwie Premium Storage, Włącz diagnostyki maszyny Wirtualnej w hello [portalu Azure](https://portal.azure.com). Aby uzyskać więcej informacji, zobacz [maszyny Wirtualnej Azure monitorowania z rozszerzeniem diagnostyki Azure](https://azure.microsoft.com/blog/2014/09/02/windows-azure-virtual-machine-monitoring-with-wad-extension/). 

    toosee wydajności dysku, użyj narzędzi systemu operacyjnego, takich jak [Monitor wydajności systemu Windows](https://technet.microsoft.com/library/cc749249.aspx) dla maszyn wirtualnych systemu Windows i hello [iostat](http://linux.die.net/man/1/iostat) polecenia dla maszyn wirtualnych systemu Linux.

* **Limity skalowania maszyny Wirtualnej i wydajność**

    Każdy magazyn w warstwie Premium, obsługiwany rozmiar maszyny Wirtualnej ma limity skalowania i wydajności specyfikacje IOPS, przepustowości i hello liczba dysków, które można dołączyć dla maszyny Wirtualnej. Użycie dysków w warstwie premium magazynu maszyn wirtualnych, upewnij się, że istnieje wystarczająca IOPS i przepustowości ruchu dysku toodrive maszyny Wirtualnej.

    Na przykład STANDARD_DS1 maszyny Wirtualnej ma dedykowany przepustowości 32 MB/s dla ruchu dysku magazynu premium. Dysk magazynu premium P10 zapewniają przepustowości 100 MB/s. Jeśli dysk magazynu premium P10 toothis dołączona maszyna wirtualna, tylko można przejść się too32 MB/s. Witaj, które zapewniają maksymalną 100 MB/s tego dysku P10 hello nie może używać.

    Witaj największy maszyny Wirtualnej w ramach hello serii DS jest obecnie hello Standard_DS15_v2. Witaj Standard_DS15_v2 można przygotować too960 MB/s na wszystkich dyskach. Witaj największy maszyny Wirtualnej w ramach hello GS-series jest hello Standard_GS5. Witaj Standard_GS5 można przygotować too2, 000 MB/s na wszystkich dyskach.

    Należy zauważyć, że te limity dysku tylko dla ruchu. Ograniczenia te nie zawierają trafień w pamięci podręcznej i ruchu sieciowego. Oddzielne przepustowości dostępnej dla ruchu sieciowego maszyn wirtualnych. Przepustowości dla ruchu sieciowego różni się od hello dedykowanego przepustowość wykorzystywaną przez dyski magazynu premium.

    Aby hello najbardziej aktualne informacje o maksymalne IOPS i przepływności (przepustowość) dla maszyn wirtualnych, obsługiwane przez Magazyn w warstwie Premium, zobacz [rozmiarów maszyn wirtualnych systemu Windows](/azure/virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) lub [rozmiarów maszyn wirtualnych systemu Linux](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

    Aby uzyskać więcej informacji o dyski magazynu premium i limity ich IOPS i przepływność zobacz tabelę hello w następnej sekcji hello.

## <a name="scalability-and-performance-targets"></a>Cele dotyczące skalowalności i wydajności
W tej sekcji opisano tooconsider cele wydajności i skalowalności hello używania magazyn w warstwie Premium.

Konta Premium magazynu są następujące wartości docelowe skalowalności hello:

| Konto łączna pojemność | Przepustowość konto magazyn lokalnie nadmiarowy |
| --- | --- | 
| Pojemność dysku: 35 TB <br>Migawki pojemności: 10 TB | Zapasowej too50 gigabity na sekundę dla ruchu przychodzącego<sup>1</sup> + wychodzących<sup>2</sup> |

<sup>1</sup> wszystkich danych (liczba żądań), które są wysyłane tooa konta magazynu

<sup>2</sup> wszystkich danych (odpowiedzi), które są odbierane z konta magazynu

Aby uzyskać więcej informacji, zobacz [elementy docelowe skalowalności i wydajności usługi Azure Storage](storage-scalability-targets.md).

Jeśli używasz konta premium magazynu dla niezarządzanego dysków i aplikacji przekracza hello wartości docelowe skalowalności konta jednego magazynu, można toomigrate toomanaged dysków. Jeśli nie chcesz toomigrate toomanaged dysków, tworzenie wielu kont magazynu toouse Twojej aplikacji. Następnie partycji danych przez tych kont magazynu. Na przykład jeśli chcesz tooattach 51 TB dysków między wieloma maszynami wirtualnymi, rozłożyć je na dwóch kont magazynu. 35 TB jest ograniczona hello pojedynczego premium konta magazynu. Upewnij się, że konto magazynu premium pojedynczego nigdy nie ma ponad 35 TB elastycznie dyski.

### <a name="premium-storage-disk-limits"></a>Limity dysku magazynu Premium
Podczas udostępniania dysku magazynu premium hello rozmiar dysku hello określa hello maksymalne IOPS i przepływności (przepustowość). Platforma Azure oferuje siedem typów dysków w warstwie premium magazynu: P4 P6 (zarządzane tylko dysków), (zarządzane tylko dysków), P10, P20 P30, P40 i P50. Każdy typ dysku magazynu premium ma określone limity IOPS i przepływności. W hello w poniższej tabeli opisano limity dla typów dysków hello:

| Typ dysków Premium  | P4    | P6    | P10   | P20   | P30   | P40   | P50   | 
|---------------------|-------|-------|-------|-------|-------|-------|-------|
| Rozmiar dysku           | 32 GB| 64 GB| 128 GB| 512 GB            | 1024 GB (1 TB)    | 2048 GB (2 TB)    | 4095 GB (4 TB)    | 
| Liczba operacji wejścia/wyjścia na sekundę na dysk       | 120   | 240   | 500   | 2300              | 5000              | 7500              | 7500              | 
| Przepływność na dysk | 25 MB na sekundę  | 50 MB / s  | 100 MB na sekundę | 150 MB na sekundę | 200 MB / s | 250 MB na sekundę | 250 MB na sekundę | 

> [!NOTE]
> Upewnij się, że wystarczającą przepustowość znajduje się na dysku ruchu toodrive maszyny Wirtualnej, zgodnie z opisem w [obsługiwane magazyn w warstwie Premium maszyn wirtualnych](#premium-storage-supported-vms). W przeciwnym razie Twoje przepływność dysku i IOPS są ograniczone toolower wartości. Maksymalna przepustowość i IOPS są oparte na powitania maszyny Wirtualnej limity, nie opisano w powyższej tabeli hello limity dysku hello.  
> 
> 

Poniżej przedstawiono niektóre tooknow ważnych rzeczy, o cele wydajności i skalowalności magazyn w warstwie Premium:

* **Udostępnione pojemność i wydajność**

    Podczas obsługi administracyjnej dysku magazynu premium, w przeciwieństwie do standardowego magazynu ma gwarancji hello pojemności, IOPS i przepływności tego dysku. Na przykład w przypadku tworzenia dysku P50 Azure udostępnia 4,095 GB pojemności, 7500 IOPS i 250 MB/s przepustowości dla tego dysku. Aplikacja może używać całość lub część hello pojemność i wydajność.

* **Rozmiar dysku**

    Azure mapy hello toohello (zaokrąglona w górę) rozmiar dysku najbliższej opcji dysku magazynu premium, jak określono w tabeli hello w powyższej sekcji hello. Na przykład rozmiar 100 GB na dysku jest sklasyfikowany jako opcja P10. Może wykonywać się too500 IOPS z zapasowej too100 MB/s przepustowości. Podobnie dysk 400 GB jest sklasyfikowany jako P20 rozmiar. Może wykonywać się too2, 300 IOPS, o 150 MB/s przepustowości.
    
    > [!NOTE]
    > Można łatwo zwiększyć rozmiar hello istniejących dysków. Na przykład można tooincrease hello rozmiar dysku 30 GB too128 GB lub TB nawet too1. Można też tooconvert dysku tooa P30 dysku P20 ponieważ potrzebujesz większej pojemności lub więcej IOPS i przepustowość. 
    > 
 
* **Rozmiar operacji We/Wy**

    rozmiar Hello operacji We/Wy jest 256 KB. Jeśli przesyłane dane hello jest mniejsza niż 256 KB, jest uznawane za 1 jednostka we/wy. Większe rozmiary We/Wy są liczone jako wiele operacji We/Wy o rozmiarze 256 KB. Na przykład 1100 KB we/wy jest liczony jako 5 jednostki we/wy.

* **Przepływność**

    limit przepustowości Hello zawiera zapisy toohello dysku i zawiera operacji odczytu na dysku, które nie są obsługiwane z pamięci podręcznej hello. Na przykład dysk P10 ma 100 MB/s przepustowości dla każdego dysku. W hello w poniższej tabeli przedstawiono przykładowe prawidłowe przepływności dysku P10:

    | Maksymalna przepustowość dla każdego dysku P10 | Pamięć podręczna nie odczytuje z dysku | Pamięć podręczna nie zapisuje toodisk |
    | --- | --- | --- |
    | 100 MB/s | 100 MB/s | 0 |
    | 100 MB/s | 0 | 100 MB/s |
    | 100 MB/s | 60 MB/s | 40 MB/s |

* **Trafień w pamięci podręcznej**

    Trafień w pamięci podręcznej nie są ograniczone przez hello przydzielone IOPS lub przepływności hello dysku. Na przykład, jeśli używasz dysku danych o **tylko do odczytu** ustawienia pamięci podręcznej na maszynie Wirtualnej, która jest obsługiwana przez Magazyn w warstwie Premium, odczytów, które są obsługiwane z pamięci podręcznej hello nie są toohello podmiotu IOPS i ograniczyć przepustowość hello dysku. Jeśli obciążenie hello dysku jest głównie operacje odczytu i może spowodować, że bardzo wysokiej przepływności. Witaj w pamięci podręcznej jest tooseparate podmiotu IOPS i ograniczenia przepływności na powitania poziom maszyny Wirtualnej, oparte na powitania rozmiar maszyny Wirtualnej. Maszyny wirtualne z serii DS mają około 4000 IOPS i 33 przepływności MB/s na podstawowe dla lokalnych dysków SSD operacji We/Wy i pamięci podręcznej. Maszyny wirtualne z serii GS mają limit 5000 IOPS i 50 MB/s przepustowości na podstawowe dla lokalnych dysków SSD operacji We/Wy i pamięci podręcznej. 

## <a name="throttling"></a>Ograniczanie przepływności
Ograniczanie mogą wystąpić, jeśli aplikacji IOPS lub przepływności przekracza limity hello przydzielone dla dysku magazynu premium. Również ograniczanie może wystąpić, jeśli ruchu dysku na wszystkich dyskach na powitania maszyny Wirtualnej przekracza limit przepustowości dysku hello dostępne dla hello maszyny Wirtualnej. Ograniczanie tooavoid, zalecamy ograniczenie hello liczba oczekujących żądań We/Wy dysku hello. Użyj limit na podstawie celów skalowalność i wydajność dysku hello, które zostały udostępnione, a hello dysku przepustowości dostępnej toohello maszyny Wirtualnej.  

Aplikację można osiągnąć hello można uzyskać najmniejsze opóźnienia, gdy jest on przeznaczony tooavoid ograniczania. Jednak jeśli hello liczba oczekujących żądań We/Wy dysku hello jest za mały, aplikacji nie może korzystać z hello maksymalną poziomów IOPS i przepływność, które są dostępne toohello dysku.

Witaj następujące przykłady pokazują, jak ograniczanie toocalculate poziomy. Wszystkie obliczenia są oparte na rozmiar jednostki we/wy 256 KB.

### <a name="example-1"></a>Przykład 1
Aplikacja została przetworzona 495 jednostki we/wy o rozmiarze 16 KB w jednej sekundy na dysku P10. jednostki we/wy Hello są liczone jako 495 IOPS. Jeśli spróbujesz 2 MB we/wy w hello sam drugi, hello całkowitej liczby operacji We/Wy jednostki jest równy too495 + 8 IOPS. Jest to spowodowane We/Wy 2 MB = jednostki 2048 KB / 256 KB = 8 we/wy, gdy hello rozmiar jednostki we/wy jest 256 KB. Ponieważ hello sumę 495 8 limit hello 500 IOPS dla dysku hello, ograniczanie występuje.

### <a name="example-2"></a>Przykład 2
Aplikacja została przetworzona 400 jednostek o rozmiarze 256 KB na dysku P10 we/wy. Witaj całkowitej przepustowości jest (400 &#215; 256) / 1024 KB = 100 MB/s. Dysk P10 ma limit przepustowości 100 MB/s. Jeśli aplikacja próbuje tooperform więcej operacji We/Wy w tym sekundy, jest to ograniczenie, ponieważ przekracza limit hello przydzielone.

### <a name="example-3"></a>Przykład 3
Masz DS4 maszyny Wirtualnej z dwóch dysków P30 dołączony. Każdy dysk P30 jest zdolny do 200 MB/s przepustowości. Jednak DS4 maszyny Wirtualnej ma pojemność dysku przepustowości 256 MB/s. Nie może obsłużyć zarówno dołączonych dysków toohello maksymalną przepustowość na tej maszynie Wirtualnej DS4 na powitania tym samym czasie. tooresolve, może wytrzymać ruchu 200 MB/s na jednym dysku i 56 MB/s na innym dysku hello. Jeśli hello sumę ruchu dysku odbywa się za pośrednictwem 256 MB/s, jest ograniczany ruch sieciowy dysku.

> [!NOTE]
> Jeśli ruchu dysku przede wszystkim składa się z małych rozmiarów we/wy, prawdopodobnie aplikacji będzie osiągnął limit IOPS hello przed hello limit przepływności. Jednak jeśli ruch dysku hello składa się przede wszystkim wielkości we/wy, prawdopodobnie aplikacji będzie osiągnęła limit przepływności hello najpierw zamiast limitu IOPS hello. Można zmaksymalizować IOPS aplikacji i przepustowości przy użyciu optymalny rozmiar operacji We/Wy. Ponadto można ograniczyć hello liczba oczekujących żądań We/Wy dysku.
> 

Zobacz toolearn więcej informacji na temat projektowania o wysokiej wydajności przy użyciu magazynu Premium [projektu dla wydajności z magazyn w warstwie Premium](storage-premium-storage-performance.md).

## <a name="snapshots-and-copy-blob"></a>Migawki i kopii obiektu Blob

toohello plik wirtualnego dysku twardego hello magazynu usługi jest stronicowych obiektów blob. Twórz migawki stronicowe obiekty BLOB i skopiuj je tooanother lokalizacji, takiej jak tooa innego konta magazynu.

### <a name="unmanaged-disks"></a>Dyski niezarządzane

Utwórz [przyrostowe migawki](../../virtual-machines/windows/incremental-snapshots.md) dla dysków premium niezarządzane hello sam sposobu korzystania z magazynu w warstwie standardowa migawki. Magazyn w warstwie Premium obsługuje tylko lokalnie nadmiarowego magazynu jako hello opcji replikacji. Zaleca się, że tworzenie migawki, a następnie skopiuj hello migawki tooa standardowy magazyn geograficznie nadmiarowy konta. Aby uzyskać więcej informacji, zobacz [opcje nadmiarowość magazynu Azure](storage-redundancy.md).

Jeśli dysk jest dołączona tooa maszyny Wirtualnej, niektóre operacje interfejsu API na powitania dysku nie są dozwolone. Na przykład nie można wykonać [kopiowania obiektu Blob](/rest/api/storageservices/Copy-Blob) operacji dla tego obiektu blob, jeśli dysk hello jest dołączony tooa maszyny Wirtualnej. Zamiast tego należy najpierw utworzyć migawkę tego obiektu blob przy użyciu hello [migawki obiektu Blob](/rest/api/storageservices/Snapshot-Blob) interfejsu API REST. Następnie należy wykonać hello [kopiowania obiektu Blob](/rest/api/storageservices/Copy-Blob) z hello migawki toocopy hello dołączono dysk. Alternatywnie można odłączyć dysku hello, a następnie wykonaj wszystkie niezbędne operacje.

Witaj następujące limity Zastosuj toopremium magazynu obiektów blob migawki:

| Limit magazynu w warstwie Premium | Wartość |
| --- | --- |
| Maksymalna liczba migawek na obiektów blob | 100 |
| Pojemności konta magazynu dla migawki<br>(Dotyczy danych tylko migawki. Nie zawiera danych w podstawowej obiektu blob.) | 10 TB |
| Minimalny czas między kolejnymi migawki | 10 minut |

toomaintain geograficznie nadmiarowego kopie z migawki, możesz skopiować migawki z konta magazynu geograficznie nadmiarowego w warstwie standardowa tooa konta premium magazynu przy użyciu narzędzia AzCopy lub kopiowania obiektu Blob. Aby uzyskać więcej informacji, zobacz [transferu danych za pomocą narzędzia wiersza polecenia AzCopy hello](storage-use-azcopy.md) i [kopiowania obiektu Blob](/rest/api/storageservices/Copy-Blob).

Aby uzyskać szczegółowe informacje dotyczące operacji REST względem stronicowe obiekty BLOB na koncie magazynu premium, zobacz [obiektu Blob operacji usługi z usługą Azure Premium Storage](http://go.microsoft.com/fwlink/?LinkId=521969).

### <a name="managed-disks"></a>Dyski zarządzane

Migawek dla dysków zarządzanych jest kopię hello zarządzanego dysku tylko do odczytu. Witaj migawka jest przechowywana jako standardowych dysków zarządzanych. Obecnie [przyrostowe migawki](../../virtual-machines/windows/incremental-snapshots.md) nie są obsługiwane w przypadku dysków zarządzanych. toolearn tootake migawek dla dysków zarządzanych, zobacz temat [Utwórz kopię plik VHD przechowywany jako zarządzany Azure dysku przy użyciu migawek zarządzane w systemie Windows](../../virtual-machines/windows/snapshot-copy-managed-disk.md) lub [Utwórz kopię plik VHD przechowywany jako zarządzany Azure dysku przy użyciu zarządzanego migawek w systemie Linux](../../virtual-machines/linux/snapshot-copy-managed-disk.md).

Jeśli dysków zarządzanych jest dołączona tooa maszyny Wirtualnej, niektóre operacje interfejsu API na dysku hello są niedozwolone. Na przykład nie można wygenerować tooperform sygnatury dostępu Współdzielonego dostępu współdzielonego operacji kopiowania zablokowaniu dysku hello dołączonych tooa maszyny Wirtualnej. Zamiast tego należy najpierw Utwórz migawkę hello dysku, a następnie wykonaj kopię hello hello migawki. Alternatywnie można odłączyć dysku hello, a następnie wygeneruj operacji kopiowania hello tooperform sygnatury dostępu Współdzielonego.


## <a name="premium-storage-for-linux-vms"></a>Magazyn w warstwie Premium dla maszyn wirtualnych systemu Linux
Program hello następujące informacje toohelp, skonfigurowanych maszyn wirtualnych systemu Linux w magazyn w warstwie Premium:

skalowalność tooachieve elementów docelowych w magazynie Premium dla wszystkich dysków w warstwie premium magazynu z buforowania zestawu zbyt**tylko do odczytu** lub **Brak**, należy wyłączyć "bariery" w przypadku zainstalowania hello systemu plików. Ponieważ hello zapisuje się, że dyski magazynu toopremium są trwałe dla tych ustawień pamięci podręcznej nie jest konieczne bariery w tym scenariuszu. Po pomyślnym zakończeniu hello zapisu żądania, danych zostało zapisanych toohello magazynu trwałego. toodisable "bariery", użyj jednej z następujących metod hello. Wybierz hello, jeden dla systemu plików:
  
* Dla **reiserFS**, toodisable bariery, użyj hello `barrier=none` opcji instalacji. (Użyj bariery tooenable `barrier=flush`.)
* Dla **ext3/ext4**, toodisable bariery, użyj hello `barrier=0` opcji instalacji. (Użyj bariery tooenable `barrier=1`.)
* Dla **XFS**, toodisable bariery, użyj hello `nobarrier` opcji instalacji. (Użyj bariery tooenable `barrier`.)
* Premium magazynu dysków przy użyciu pamięci podręcznej ustawić także**ReadWrite**, Włącz bariery dla zapisu trwałości.
* Dla toopersist etykiety woluminu po ponownym uruchomieniu hello maszyny Wirtualnej, należy zaktualizować /etc/fstab z dyskami toohello odwołuje się do unikatowego identyfikatora uniwersalnego (UUID) hello. Aby uzyskać więcej informacji, zobacz [dodać tooa dysków zarządzanych w maszyny Wirtualnej systemu Linux](../../virtual-machines/linux/add-disk.md).

Hello dystrybucje systemu Linux po sprawdzeniu poprawności dla usługi Azure Premium Storage. Lepszą wydajność i stabilności magazyn w warstwie Premium, zaleca się uaktualnienie tooone sieci maszyn wirtualnych z tych wersji, co najmniej (lub tooa nowszej wersji). Niektóre wersje wymagają powitalne hello najnowsze Linux integracji usług (LIS), wersja 4.0, dla platformy Azure. toodownload i zainstaluj dystrybucji łącza hello na liście hello w poniższej tabeli. Listy obrazów toohello możemy dodać podczas wykonywania sprawdzania poprawności. Należy pamiętać, że naszego operacje sprawdzania poprawności, Pokaż, że wydajność może być różna dla każdego obrazu. Wydajność zależy od obciążenia właściwości i ustawienia obrazu. Obrazy różnych dostosowanych do różnych rodzajów obciążeń.

| Dystrybucja | Wersja | Obsługiwane jądra | Szczegóły |
| --- | --- | --- | --- |
| Ubuntu | 12.04 | 3.2.0-75.110+ | Ubuntu-12_04_5-LTS-AMD64-Server-20150119-en-us-30GB |
| Ubuntu | 14.04 | 3.13.0-44.73+ | Ubuntu-14_04_1-LTS-AMD64-Server-20150123-en-us-30GB |
| Debian | 7.x, 8.x | 3.16.7-ckt4-1+ | &nbsp; |
| SUSE | SLES 12| 3.12.36-38.1+| SUSE-sles-12-priorytet v20150213 <br> SUSE-sles-12-v20150213 |
| SUSE | SLES 11 Z DODATKIEM SP4 | 3.0.101-0.63.1+ | &nbsp; |
| CoreOS | 584.0.0+| 3.18.4+ | CoreOS 584.0.0 |
| CentOS | 6.5, 6.6, 6.7, 7.0 | &nbsp; | [LIS4 wymagane](http://go.microsoft.com/fwlink/?LinkID=403033&clcid=0x409) <br> *Patrz Uwaga w następnej sekcji hello* |
| CentOS | 7.1+ | 3.10.0-229.1.2.el7+ | [LIS4 zalecane](http://go.microsoft.com/fwlink/?LinkID=403033&clcid=0x409) <br> *Patrz Uwaga w następnej sekcji hello* |
| Red Hat Enterprise Linux (RHEL) | 6.8+, 7.2+ | &nbsp; | &nbsp; |
| Oracle | 6.0+, 7.2+ | &nbsp; | UEK4 lub RHCK |
| Oracle | 7.0-7.1 | &nbsp; | UEK4 lub RHCK z[LIS 4.1 +](http://go.microsoft.com/fwlink/?LinkID=403033&clcid=0x409) |
| Oracle | 6.4-6.7 | &nbsp; | UEK4 lub RHCK z[LIS 4.1 +](http://go.microsoft.com/fwlink/?LinkID=403033&clcid=0x409) |


### <a name="lis-drivers-for-openlogic-centos"></a>Sterowniki LIS OpenLogic CentOS

Jeśli korzystasz z maszyny wirtualnej CentOS OpenLogic, uruchom następujące polecenie tooinstall hello najnowsze sterowniki hello:

```
sudo rpm -e hypervkvpd  ## (Might return an error if not installed. That's OK.)
sudo yum install microsoft-hyper-v
```

tooactivate hello nowe sterowniki, uruchom ponownie komputer hello.

## <a name="pricing-and-billing"></a>Cennik i rozliczenia

Użycie magazyn w warstwie Premium, zastosuj następujące zagadnienia dotyczące rozliczeń hello:

* **Rozmiar dysku i obiektów blob magazynu Premium**

    Rozliczeń dla dysku magazynu premium lub obiektu blob zależy od rozmiaru hello elastycznie hello dysku lub obiektu blob. Azure mapy hello toohello elastycznie rozmiaru (zaokrąglona w górę) najbliższej opcji dysku magazynu premium. Aby uzyskać więcej informacji, zobacz tabelę hello w [magazyn w warstwie Premium cele wydajności i skalowalności](#premium-storage-scalability-and-performance-targets). Każdy tooa mapy dysku obsługiwane udostępniane rozmiar dysku, a następnie jest on rozliczany odpowiednio. Rozliczeń dla dowolnego dysku inicjowana jest proporcjonalna co godzinę przy użyciu hello miesięcznej cenie hello oferta magazyn w warstwie Premium. Na przykład jeśli elastycznie dysk P10 i usunięto go po 20 godzin, są rozliczane za hello P10 oferty proporcjonalnie too20 godzin. Jest to niezależnie od hello ilość danych rzeczywistych zapisywane toohello dysku lub hello IOPS i przepływności używane.

* **Premium niezarządzane dysków migawek**

    Migawki na dyski premium niezarządzanych są rozliczane hello dodatkowej pojemności używanych przez hello migawki. Aby uzyskać więcej informacji na temat migawek, zobacz [utworzenia migawki obiektu blob](/rest/api/storageservices/Snapshot-Blob).

* **Migawek dysków zarządzanych w warstwie Premium**

    Migawki dysków zarządzanych jest tylko do odczytu kopię hello dysku. dysk Hello jest przechowywana jako standardowych dysków zarządzanych. Koszty migawki hello sam jako standard zarządzany dysku. Na przykład jeśli migawki z dysków zarządzanych w warstwie premium 128 GB koszt hello migawki hello jest tooa równoważne 128 GB standardowych dysków zarządzanych w.  

* **Transfer danych wychodzących**

    [Transfer danych wychodzących](https://azure.microsoft.com/pricing/details/data-transfers/) (danych wychodzących z centrach danych platformy Azure) powodują Naliczanie opłat za zużycie przepustowości.

Aby uzyskać szczegółowe informacje o cenach dla magazyn w warstwie Premium, obsługiwane przez Magazyn w warstwie Premium maszyn wirtualnych i dysków zarządzanych zobacz następujące artykuły:

* [Cennik usługi Azure Storage](https://azure.microsoft.com/pricing/details/storage/)
* [Cennik maszyn wirtualnych](https://azure.microsoft.com/pricing/details/virtual-machines/)
* [Dyski zarządzane ceny](https://azure.microsoft.com/pricing/details/managed-disks/)

## <a name="azure-backup-support"></a>Obsługa kopii zapasowej systemu Azure 

Regionalnej awarii, musisz należy wykonać kopię zapasową dysków maszyny Wirtualnej w innym regionie przy użyciu [kopia zapasowa Azure](../../backup/backup-introduction-to-azure-backup.md) i konto magazynu GRS jako magazyn kopii zapasowych.

toocreate zadania tworzenia kopii zapasowej na podstawie czasu tworzenia kopii zapasowych, łatwe przywrócenie maszyny Wirtualnej i zasady przechowywania kopii zapasowych, użyj kopii zapasowej Azure. Narzędzie Kopia zapasowa służy zarówno z dyskami niezarządzane i zarządzane. Aby uzyskać więcej informacji, zobacz [kopia zapasowa Azure dla maszyn wirtualnych z dyskami niezarządzane](../../backup/backup-azure-vms-first-look-arm.md) i [kopia zapasowa Azure dla maszyn wirtualnych z dyskami zarządzanych](../../backup/backup-introduction-to-azure-backup.md#using-managed-disk-vms-with-azure-backup). 

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji na temat magazyn w warstwie Premium zobacz następujące artykuły hello.

### <a name="design-and-implement-with-premium-storage"></a>Projektowanie i implementowanie z magazyn w warstwie Premium
* [Projektować pod kątem wydajności przy użyciu magazyn w warstwie Premium](storage-premium-storage-performance.md)
* [Operacje magazynu obiektów blob z magazyn w warstwie Premium](http://go.microsoft.com/fwlink/?LinkId=521969)

### <a name="operational-guidance"></a>Wskazówki dotyczące obsługi
* [Migrowanie tooAzure magazyn w warstwie Premium](../common/storage-migration-to-premium-storage.md)

### <a name="blog-posts"></a>Wpisy na blogach
* [Usługa Azure Premium Storage ogólnie dostępna](https://azure.microsoft.com/blog/azure-premium-storage-now-generally-available-2/)
* [Anonsowanie hello GS-series: Dodawanie toohello pomocy technicznej Premium Storage największy maszyn wirtualnych w hello chmury publicznej](https://azure.microsoft.com/blog/azure-has-the-most-powerful-vms-in-the-public-cloud/)
