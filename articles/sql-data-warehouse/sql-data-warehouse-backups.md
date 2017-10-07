---
title: "kopie zapasowe z usługi SQL Data Warehouse aaaAzure - migawki geograficznie nadmiarowego | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat kopii zapasowych wbudowaną bazą danych SQL Data Warehouse, umożliwiających toorestore punkt przywracania tooa magazyn danych SQL Azure lub inny region geograficzny."
services: sql-data-warehouse
documentationcenter: 
author: Lakshmi1812
manager: jhubbard
editor: 
ms.assetid: b5aff094-05b2-4578-acf3-ec456656febd
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.custom: backup-restore
ms.date: 10/31/2016
ms.author: lakshmir;barbkess
ms.openlocfilehash: 34659480485246f54a1490e185fc1b903fb2520d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="sql-data-warehouse-backups"></a>Tworzenie kopii zapasowych SQL Data Warehouse
Magazyn danych SQL oferuje zarówno lokalnych, jak i geograficzne kopii zapasowych w ramach jego możliwości tworzenia kopii zapasowych magazynu danych. Obejmują one migawki obiektu Blob magazynu Azure i Magazyn geograficznie nadmiarowy. Użyj danych magazynu kopii zapasowych toorestore przywracania tooa magazynu danych do punktu w regionie podstawowym hello, lub przywrócić tooa inny region geograficzny. W tym artykule opisano charakterystyki hello kopii zapasowych w usłudze SQL Data Warehouse.

## <a name="what-is-a-data-warehouse-backup"></a>Co to jest kopia zapasowa magazynu danych?
Kopia zapasowa magazynu danych jest hello danych, których można używać toorestore określonym czasie tooa magazynu danych.  Ponieważ Magazyn danych SQL to Rozproszony system, kopia zapasowa magazynu danych składa się z wielu plików, które są przechowywane w obiektach blob Azure. 

Kopie zapasowe bazy danych są integralną część każdej strategii odzyskiwania biznesowych, jak ciągłości i odzyskiwaniem po awarii, ponieważ ich ochronę danych przed przypadkowym uszkodzenia lub usunięcia. Aby uzyskać więcej informacji, zobacz [omówienie ciągłości działalności biznesowej](../sql-database/sql-database-business-continuity.md).

## <a name="data-redundancy"></a>Nadmiarowość danych
Usługa SQL Data Warehouse chroni dane przez zapisanie danych w magazyn lokalnie nadmiarowy (LRS) usługa Azure Premium Storage. Ta funkcja usługi Azure Storage przechowuje wiele synchronicznych kopii danych hello w hello dane lokalne centrum tooguarantee przezroczystą ochronę danych w przypadku zlokalizowanych awarii. Nadmiarowość danych zapewnia przełączniki problemów infrastruktury, takich jak awarii dysku danych. Nadmiarowość danych zapewnia ciągłość prowadzenia działalności biznesowej, odporność na uszkodzenia i wysokiej dostępności infrastruktury.

więcej informacji na temat toolearn:

* Usługa Azure Premium storage, zobacz [tooAzure wprowadzenie magazyn w warstwie Premium](../storage/common/storage-premium-storage.md).
* Magazyn lokalnie nadmiarowy, zobacz [replikacja usługi Azure Storage](../storage/common/storage-redundancy.md#locally-redundant-storage).

## <a name="azure-storage-blob-snapshots"></a>Migawki obiektu Blob magazynu Azure
Jako korzyścią z używania usługi Azure Premium Storage SQL Data Warehouse używa magazynu danych hello toobackup migawki obiektu Blob magazynu Azure lokalnie. Można przywrócić punkt przywracania migawki tooa magazynu danych. Migawki Uruchom co najmniej co 8 godzin i są dostępne na siedem dni.  

więcej informacji na temat toolearn:

* Migawki obiektów blob platformy Azure, zobacz [utworzenia migawki obiektu blob](../storage/blobs/storage-blob-snapshots.md).

## <a name="geo-redundant-backups"></a>Kopie zapasowe geograficznie nadmiarowego
Co 24 godziny, SQL Data Warehouse przechowuje hello magazynu danych w magazynu w warstwie standardowa. Witaj magazynu danych jest tworzony toomatch hello czasu hello ostatnia migawka. Witaj magazynu w warstwie standardowa należy tooa magazynu geograficznie nadmiarowego konta z dostępem do odczytu (RA-GRS). Funkcja magazynu Azure RA-GRS Hello replikuje tooa pliki kopii zapasowej hello [centrum danych sparowanego](../best-practices-availability-paired-regions.md). Replikacja geograficzna gwarantuje, że w przypadku, gdy nie można uzyskać dostępu hello migawki w danym regionie podstawowym, można przywrócić magazynu danych. 

Ta funkcja jest domyślnie. Jeśli nie chcesz toouse geograficznie nadmiarowego kopii zapasowych, możesz [zrezygnować z niego] (https://docs.microsoft.com/powershell/resourcemanager/Azurerm.sql/v2.1.0/Set-AzureRmSqlDatabaseGeoBackupPolicy?redirectedfrom=msdn). 

> [!NOTE]
> W magazynie Azure określenie hello *replikacji* odnosi się toocopying plików z jednej lokalizacji tooanother. SQL do *replikacji bazy danych* odwołuje się tookeeping toomultiple pomocniczej bazy danych synchronizowane z podstawowej bazy danych. 
> 
> 

> [!NOTE]
> Nie można zrezygnować z magazynu geograficznie nadmiarowego kopii zapasowych z DWU 9000 i DWU 18000. 
>
> 

więcej informacji na temat toolearn:

* Magazyn geograficznie nadmiarowy, zobacz [replikacja usługi Azure Storage](../storage/common/storage-redundancy.md).
* RA-GRS magazynu, zobacz [dostęp do odczytu magazynu geograficznie nadmiarowego](../storage/common/storage-redundancy.md#read-access-geo-redundant-storage).

## <a name="data-warehouse-backup-schedule-and-retention-period"></a>Harmonogram tworzenia kopii zapasowych i okres przechowywania magazynu danych
Usługi SQL Data Warehouse tworzy migawek w magazynie danych w trybie online, co cztery godziny tooeight dzięki temu każda migawki na siedem dni. Z bazy danych online tooone punktów przywracania hello w hello można przywrócić w ciągu ostatnich siedmiu dni. 

toosee rozpoczęcie hello ostatnia migawka, uruchom to zapytanie na online SQL Data Warehouse. 

```sql
select top 1 *
from sys.pdw_loader_backup_runs 
order by run_id desc;
```

Jeśli potrzebujesz tooretain migawki przez ponad siedem dni, można przywrócić przywracania tooa punktu nowy magazyn danych. Po zakończeniu operacji przywracania hello SQL Data Warehouse rozpoczyna tworzenie migawek na powitania nowego magazynu danych. Jeśli nie wprowadzisz zmian toohello nowy magazyn danych, migawek hello pozostać pusta i w związku z tym koszt migawki hello jest minimalny. Można również wstrzymać hello tookeep bazy danych magazynu danych SQL z tworzenia migawki.

### <a name="what-happens-toomy-backup-retention-while-my-data-warehouse-is-paused"></a>Co się stanie toomy przechowywania kopii zapasowych, gdy mój hurtowni danych zostało wstrzymane?
Usługi SQL Data Warehouse nie tworzy migawki i nie wygasa migawek, podczas gdy magazyn danych jest wstrzymana. wiek migawki Hello nie zmienić magazyn danych hello jest wstrzymana. Przechowywania migawki jest oparta na powitania liczbę dni ważności hello magazynu danych jest w trybie online nie dni kalendarzowych.

Na przykład migawki rozpoczyna się października 1 na 4 pm hello hurtowni danych zostało wstrzymane 3 października po 16: 00, migawka hello jest dwóch dni. Zawsze, gdy magazyn danych hello wraca do trybu online migawki hello jest dwóch dni. Jeśli magazyn danych hello przejściu do trybu online 5 października godzinie 4, migawki hello jest dwa dni i pozostaje pięć dni.

Gdy magazyn danych hello wraca do trybu online, SQL Data Warehouse wznawia nowych migawek i wygasa migawek, gdy mają one danych ponad siedem dni.

### <a name="how-long-is-hello-retention-period-for-a-dropped-data-warehouse"></a>Jak długo trwa hello okres przechowywania danych w magazynie porzuconych?
Po upuszczeniu hurtowni danych, hello magazynu danych i migawek hello są zapisywane na siedem dni i następnie usuwane. Można przywrócić tooany magazynu danych hello punktów przywracania hello zapisane.

> [!IMPORTANT]
> Usunięcie logicznej wystąpienia programu SQL server, wszystkich baz danych należących do wystąpienia toohello również zostaną usunięte i nie może zostać odzyskany. Nie można przywrócić usuniętego serwera.
> 
> 

## <a name="data-warehouse-backup-costs"></a>Koszty kopii zapasowych magazynu danych
Witaj całkowity koszt dla magazynu danych podstawowych i siedem dni migawek obiektów Blob platformy Azure jest zaokrąglony toohello najbliższej TB. Na przykład jeśli magazyn danych jest 1,5 TB i hello migawki używają 100 GB, są rozliczane za 2 TB danych stawkami Azure Premium Storage. 

> [!NOTE]
> Każda migawka jest początkowo pusta i zwiększa się w miarę wprowadzania zmian toohello danych podstawowych magazynu. Wszystkie migawki wzrost rozmiaru jako hello danych magazynu zmiany. W związku z tym kosztów magazynowania hello migawek wzrostu zgodnie z toohello szybkość zmian.
> 
> 

Jeśli korzystasz z magazynu geograficznie nadmiarowego, pojawi się opłat oddzielnie. Magazyn geograficznie nadmiarowy Hello jest on rozliczany według hello standardowe stawki dostęp do odczytu geograficznie magazynu geograficznie nadmiarowego (RA-GRS).

Aby uzyskać więcej informacji na temat cen usługi SQL Data Warehouse, zobacz [cennik usługi SQL Data Warehouse](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).

## <a name="using-database-backups"></a>Za pomocą kopii zapasowej bazy danych
podstawowym zastosowaniem Hello kopii zapasowych magazynu danych SQL jest toorestore hello danych magazynu tooone punktów przywracania hello w okresie przechowywania hello.  

* toorestore SQL data warehouse, zobacz [przywrócić SQL data warehouse](sql-data-warehouse-restore-database-overview.md).

## <a name="related-topics"></a>Powiązane tematy
### <a name="scenarios"></a>Scenariusze
* Omówienie ciągłości działalności, można zobaczyć [omówienie ciągłości działalności biznesowej](../sql-database/sql-database-business-continuity.md)

<!-- ### Tasks -->

* Zobacz toorestore hurtowni danych [przywrócić magazyn danych SQL](sql-data-warehouse-restore-database-overview.md)

<!-- ### Tutorials -->

