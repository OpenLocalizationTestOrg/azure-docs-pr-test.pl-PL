---
title: "aaaPause, wznowić, skalować T-SQL w usłudze Azure SQL Data Warehouse | Dokumentacja firmy Microsoft"
description: "Transact-SQL (T-SQL) zadań poza tooscale wydajności przez dostosowanie wartości dwu. Zmniejszyć koszty przez skalowanie w trakcie godziny poza szczytem."
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
ms.assetid: a970d939-2adf-4856-8a78-d4fe8ab2cceb
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 03/30/2017
ms.author: elbutter;barbkess
ms.openlocfilehash: 84c6868acb673221d8853319ac9a05bb98b2b7c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-t-sql"></a>Zarządzanie moc obliczeniową w usłudze Azure SQL Data Warehouse (T-SQL)
> [!div class="op_single_selector"]
> * [Omówienie](sql-data-warehouse-manage-compute-overview.md)
> * [Portal](sql-data-warehouse-manage-compute-portal.md)
> * [PowerShell](sql-data-warehouse-manage-compute-powershell.md)
> * [REST](sql-data-warehouse-manage-compute-rest-api.md)
> * [TSQL](sql-data-warehouse-manage-compute-tsql.md)
>
>

<a name="current-dwu-bk"></a>

## <a name="view-current-dwu-settings"></a>Wyświetl bieżące ustawienia Jednostka DWU
tooview hello bieżącej wartości DWU ustawienia dla baz danych:

1. Otwórz Eksplorator obiektów SQL Server w programie Visual Studio.
2. Połączenie skojarzone z serwera logicznego bazy danych SQL hello bazy danych master toohello.
3. Wybierz z hello sys.database_service_objectives dynamiczny widok zarządzania. Oto przykład: 

```sql
SELECT
    db.name [Database]
,   ds.edition [Edition]
,   ds.service_objective [Service Objective]
FROM
    sys.database_service_objectives ds
JOIN
    sys.databases db ON ds.database_id = db.database_id
```

<a name="scale-dwu-bk"></a>
<a name="scale-compute-bk"></a>

## <a name="scale-compute"></a>Skalowanie możliwości obliczeniowych
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

Witaj toochange jednostek dwu:

1. Połączenie skojarzone z serwera logicznego bazy danych SQL bazy danych master toohello.
2. Użyj hello [ALTER DATABASE] [ ALTER DATABASE] instrukcji TSQL. Witaj poniższy przykład przedstawia hello usługi poziomu celu tooDW1000 dla bazy danych hello MySQLDW. 

```Sql
ALTER DATABASE MySQLDW
MODIFY (SERVICE_OBJECTIVE = 'DW1000')
;
```

<a name="check-database-state-bk"></a>

## <a name="check-database-state-and-operation-progress"></a>Sprawdzić postęp stanu oraz operacji bazy danych

1. Połączenie skojarzone z serwera logicznego bazy danych SQL bazy danych master toohello.
2. Przedstawia stan bazy danych toocheck zapytania

```sql
SELECT *
FROM
sys.databases
```

3. Przedstawia stan toocheck zapytania operacji

```sql
SELECT *
FROM
    sys.dm_operation_status
WHERE
    resource_type_desc = 'Database'
AND 
    major_resource_id = 'MySQLDW'
```

Ten widok DMV zwraca informacje o różnych operacji zarządzania na usługą SQL Data Warehouse, takich jak stan operacji i hello hello hello operacja, która będzie IN_PROGRESS lub UKOŃCZONA.



<a name="next-steps-bk"></a>

## <a name="next-steps"></a>Następne kroki
Inne zadania zarządzania, zobacz [omówienie zarządzania][Management overview].

<!--Image references-->

<!--Article references-->
[Service capacity limits]: ./sql-data-warehouse-service-capacity-limits.md
[Management overview]: ./sql-data-warehouse-overview-manage.md
[Manage compute power overview]: ./sql-data-warehouse-manage-compute-overview.md

<!--MSDN references-->

[ALTER DATABASE]: https://msdn.microsoft.com/library/mt204042.aspx


<!--Other Web references-->

[Azure portal]: http://portal.azure.com/
