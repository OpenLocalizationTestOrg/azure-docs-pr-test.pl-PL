---
title: "aaaUse fabryki danych Azure z usługą Magazyn danych SQL | Dokumentacja firmy Microsoft"
description: "Porady dotyczące przy użyciu fabryki danych Azure (ADF) w usłudze Azure SQL Data Warehouse związane z opracowywaniem rozwiązań."
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
ms.assetid: 492de762-c7a2-4cdb-943f-3135230e94f1
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: d40a547830f9681504253d39ae3066800a955c04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-data-factory-with-sql-data-warehouse"></a>Użyj fabryki danych Azure z usługą Magazyn danych SQL
Fabryka danych Azure zapewnia pełni zarządzanego metodę organizowanie hello transferu danych i wykonywania procedur składowanych na magazyn danych SQL.  Pozwoli to toomore łatwo Konfiguracja i harmonogram złożony wyodrębniania, przekształcania i ładowania (ETL) procedur z usługą Magazyn danych SQL. Aby uzyskać bardziej szczegółowy przegląd fabryki danych Azure, zobacz hello [dokumentacji fabryki danych Azure][Azure Data Factory documentation].

## <a name="data-movement"></a>Przenoszenie danych
Fabryka danych Azure umożliwia przenoszenie danych między zarówno lokalnych źródeł i różnych usług platformy Azure.  Ogólne, bieżący integracji z fabryką danych Azure obsługuje tooand przeniesienia danych z hello następujących lokalizacji:

* Magazyn obiektów blob platformy Azure
* Usługa Azure SQL Database
* Lokalny serwer SQL
* Program SQL Server na IaaS

Informacje dotyczące jak aktywność kopiowania tooset zapasowych sekcji [skopiować dane z fabryką danych Azure][Copy data with Azure Data Factory]

## <a name="stored-procedures"></a>Procedury składowane
 W hello sam sposób można też używać tooschedule transferu danych, fabryki danych Azure mogą być używane tooorchestrate hello wykonywania procedur składowanych.  Umożliwia bardziej złożonych toobe potoki utworzone i rozszerza fabryki danych Azure możliwości tooleverage hello moc obliczeniową usługi SQL Data Warehouse.

## <a name="next-steps"></a>Następne kroki
Omówienie integracji, zobacz [Omówienie integracji usługi SQL Data Warehouse][SQL Data Warehouse integration overview].
Więcej porad dla deweloperów znajduje się w artykule [Omówienie programowania w usłudze SQL Data Warehouse][SQL Data Warehouse development overview].

<!--Image references-->

<!--Article references-->

[Copy data with Azure Data Factory]: ../data-factory/data-factory-data-movement-activities.md
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
[SQL Data Warehouse integration overview]: ./sql-data-warehouse-overview-integrate.md

<!--MSDN references-->

<!--Other Web references-->
[Azure Data Factory documentation]:https://azure.microsoft.com/documentation/services/data-factory/

