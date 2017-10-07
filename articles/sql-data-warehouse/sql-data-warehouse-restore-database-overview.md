---
title: "Magazyn danych Azure — lokalnych i geograficznie nadmiarowego aaaRestore | Dokumentacja firmy Microsoft"
description: "Przegląd hello opcje przywracania bazy danych do przywrócenia bazy danych w magazynie danych SQL Azure."
services: sql-data-warehouse
documentationcenter: NA
author: Lakshmi1812
manager: jhubbard
editor: 
ms.assetid: 3e01c65c-6708-4fd7-82f5-4e1b5f61d304
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: backup-restore
ms.date: 10/31/2016
ms.author: lakshmir;barbkess
ms.openlocfilehash: a96b898372b29d420e1416ca93a172ff8af47fc7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="sql-data-warehouse-restore"></a>Przywrócenie magazynu danych SQL
> [!div class="op_single_selector"]
> * [Omówienie][Overview]
> * [Portal][Portal]
> * [Środowiska PowerShell][PowerShell]
> * [REST][REST]
> 
> 

Usługi SQL Data Warehouse umożliwia zarówno lokalnych, jak i geograficzne jego awarii magazynu danych w ramach odzyskiwania. Użyj toorestore przywracania tooa magazynu danych do punktu w regionie podstawowym hello, lub użyj innego regionu geograficznego geograficznie nadmiarowego kopii zapasowych toorestore tooa kopii zapasowych magazynu danych. W tym artykule opisano specyfice hello przywrócenie magazynu danych.

## <a name="what-is-a-data-warehouse-restore"></a>Co to jest przywrócenie magazynu danych?
Przywrócenie magazynu danych jest nowy magazyn danych, która jest tworzona na podstawie istniejącej kopii zapasowej lub usunięte dane magazynu. Magazyn danych przywróconej Hello ponownie tworzy hello magazynu kopii zapasowej danych w określonym czasie. Ponieważ Magazyn danych SQL to Rozproszony system, przywracania magazynu danych jest tworzony z wielu plików kopii zapasowej, które są przechowywane w obiektach blob Azure. 

Przywracanie bazy danych jest integralną część każdej strategii odzyskiwania biznesowych, jak ciągłości i odzyskiwaniem po awarii, ponieważ ponownie tworzy dane po przypadkowym uszkodzenia lub usunięcia.

Aby uzyskać więcej informacji, zobacz:

* [Tworzenie kopii zapasowych SQL Data Warehouse](sql-data-warehouse-backups.md)
* [Omówienie ciągłości działalności biznesowej](../sql-database/sql-database-business-continuity.md)

## <a name="data-warehouse-restore-points"></a>Punkty przywracania magazynu danych
Jako korzyścią z używania usługi Azure Premium Storage SQL Data Warehouse używa obiektu Blob magazynu Azure migawki toobackup hello danych podstawowych magazynu. Każda migawka ma punkt przywracania, który reprezentuje czas hello migawki hello uruchomiona. toorestore hurtowni danych, wybierz punkt przywracania i wydać polecenie restore.  

Usługi SQL Data Warehouse zawsze przywraca hello kopii zapasowej tooa nowego magazynu danych. Można albo Zachowaj hello przywróconych danych magazyn i hello bieżącą lub usuń jedno z nich. Jeśli chcesz tooreplace hello bieżąca data warehouse przy użyciu hello przywrócić magazynu danych, zmień jego nazwę.

Jeśli potrzebujesz toorestore hurtowni danych usuniętych lub wstrzymana, możesz [Utwórz bilet pomocy technicznej](sql-data-warehouse-get-started-create-support-ticket.md). 

<!-- 
### Can I restore a deleted data warehouse?

Yes, you can restore hello last available restore point.

Yes, for hello next seven calendar days. When you delete a data warehouse, SQL Data Warehouse actually keeps hello data warehouse and its snapshots for seven days just in case you need hello data. After seven days, you won't be able toorestore tooany of hello restore points. -->

## <a name="geo-redundant-restore"></a>Przywracanie geograficznie nadmiarowego
Można przywrócić obsługujący magazyn danych SQL Azure o takim samym poziomie wydajności wybranego regionu tooany magazynu danych. Należy pamiętać, że DWU 9000 i 18000 nie są obsługiwane we wszystkich regionach hello w wersji zapoznawczej.

> [!NOTE]
> Przywracanie tooperform geograficznie nadmiarowego, który musi nie rezygnujesz z tej funkcji.
> 
> 

## <a name="restore-timeline"></a>Przywróć osi czasu
Punkt przywracania dostępne tooany bazy danych w ramach hello można przywrócić w ostatnich siedmiu dni. Migawki Uruchom co cztery godziny tooeight i są dostępne na siedem dni. Gdy migawka jest starsza niż siedmiu dni, wygaśnie i jego punktu przywracania nie jest już dostępny.

## <a name="restore-costs"></a>Przywróć kosztów
jest on rozliczany Hello opłat magazynu dla magazynu danych przywróconych hello szybkością hello Azure Premium Storage. 

Jeśli magazynu przywróconych danych zostanie wstrzymana, są naliczane opłaty za magazyn szybkością hello Azure Premium Storage. Zaletą Hello wstrzymanie jest nie są naliczane opłaty dla zasobów obliczeniowych hello DWU.

Aby uzyskać więcej informacji na temat cen usługi SQL Data Warehouse, zobacz [cennik usługi SQL Data Warehouse](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).

## <a name="uses-for-restore"></a>Używa do odtworzenia
podstawowym zastosowaniem Hello przywracania magazynu danych jest toorecover danych po przypadkowej utraty danych lub uszkodzenia.

Umożliwia także tooretain przywracania magazynu danych kopii zapasowej przez ponad siedem dni. Po przywróceniu kopii zapasowej hello, masz hello magazynu danych online i można wstrzymać go przez nieograniczony czas toosave obliczeń kosztów. opłaty za magazyn szybkością hello Azure Premium Storage wiąże się z Hello wstrzymania bazy danych. 

## <a name="related-topics"></a>Powiązane tematy
### <a name="scenarios"></a>Scenariusze
* Omówienie ciągłości działalności, można zobaczyć [omówienie ciągłości działalności biznesowej](../sql-database/sql-database-business-continuity.md)

<!-- ### Tasks -->

tooperform hurtowni danych przywrócenie, przywracania przy użyciu:

* Azure portalu, zobacz [przywrócić hurtowni danych przy użyciu hello portalu Azure](sql-data-warehouse-restore-database-portal.md)
* Polecenia cmdlet programu PowerShell, zobacz [przywrócić hurtowni danych przy użyciu poleceń cmdlet programu PowerShell](sql-data-warehouse-restore-database-powershell.md)
* Interfejsy API REST, zobacz [przywrócić hurtowni danych przy użyciu hello interfejsów API REST](sql-data-warehouse-restore-database-rest-api.md)

<!-- ### Tutorials -->

<!--Image references-->

<!--Article references-->
[Azure SQL Database business continuity overview]: ../sql-database/sql-database-business-continuity.md
[Overview]: ./sql-data-warehouse-restore-database-overview.md
[Portal]: ./sql-data-warehouse-restore-database-portal.md
[PowerShell]: ./sql-data-warehouse-restore-database-powershell.md
[REST]: ./sql-data-warehouse-restore-database-rest-api.md

<!--MSDN references-->


<!--Other Web references-->
