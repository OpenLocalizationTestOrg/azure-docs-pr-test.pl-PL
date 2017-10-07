---
title: aaaRestore magazyn danych SQL Azure (interfejsu API REST) | Dokumentacja firmy Microsoft
description: "Interfejs API REST zadania przywracania usługi Azure SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: Lakshmi1812
manager: jhubbard
editor: 
ms.assetid: fca922c6-b675-49c7-907e-5dcf26d451dd
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: backup-restore
ms.date: 10/31/2016
ms.author: lakshmir;barbkess
ms.openlocfilehash: cf6678d71aafff71b1ea715f447e41e25f20d1b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="restore-an-azure-sql-data-warehouse-rest-api"></a>Przywróć magazyn danych Azure SQL (interfejsu API REST)
> [!div class="op_single_selector"]
> * [Omówienie][Overview]
> * [Portal][Portal]
> * [Środowiska PowerShell][PowerShell]
> * [REST][REST]
> 
> 

W tym artykule dowiesz się, jak za pomocą usługi Azure SQL Data Warehouse toorestore hello interfejsu API REST.

## <a name="before-you-begin"></a>Przed rozpoczęciem
**Sprawdź, czy pojemność jednostek dtu w warstwie.** Każdy magazyn danych SQL jest obsługiwana przez serwer SQL (np. myserver.database.windows.net), który ma domyślnego przydziału jednostek dtu w warstwie.  Zanim będzie można przywrócić SQL Data Warehouse, sprawdź tego hello programu SQL server ma wystarczająco pozostałych limit przydziału jednostek DTU dla przywracanej hello w bazie danych. toolearn jak potrzebne toocalculate DTU lub toorequest więcej jednostek dtu w warstwie, zobacz [żądanie zmiany limitu przydziału jednostek dtu w warstwie][Request a DTU quota change].

## <a name="restore-an-active-or-paused-database"></a>Przywróć bazę danych aktywnej lub wstrzymana
toorestore bazy danych:

1. Pobierz listę hello przy użyciu operacji punkty przywracania bazy danych Get hello punkty przywracania bazy danych.
2. Rozpocznij przywracania przy użyciu hello [żądanie przywracania bazy danych utwórz] [ Create database restore request] operacji.
3. Śledzić stan hello przywracania za pomocą hello [operacji stan bazy danych] [ Database operation status] operacji.

> [!NOTE]
> Po ukończeniu przywracania hello można skonfigurować odzyskanej bazy danych, wykonując [konfiguracji bazy danych po odzyskaniu][Configure your database after recovery].
> 
> 

## <a name="restore-a-deleted-database"></a>Przywracanie usuniętej bazy danych
toorestore usuniętej bazy danych:

1. Lista wszystkich dostępnych usuniętych baz danych przy użyciu hello [listy dostępnych porzucić bazy danych] [ List restorable dropped databases] operacji.
2. Uzyskiwanie szczegółów hello hello usunięte bazy danych ma toorestore przy użyciu hello [Get dostępnych porzucić bazy danych] [ Get restorable dropped database] operacji.
3. Rozpocznij przywracania przy użyciu hello [żądanie przywracania bazy danych utwórz] [ Create database restore request] operacji.
4. Śledzić stan hello przywracania za pomocą hello [operacji stan bazy danych] [ Database operation status] operacji.

> [!NOTE]
> Zobacz bazy danych po zakończeniu przywracania hello tooconfigure [konfiguracji bazy danych po odzyskaniu][Configure your database after recovery].
> 
> 

## <a name="next-steps"></a>Następne kroki
toolearn o funkcjach ciągłości biznesowej hello wersji bazy danych SQL Azure, przeczytaj hello [omówienie ciągłości działalności biznesowej usługi Azure SQL Database][Azure SQL Database business continuity overview].

<!--Image references-->

<!--Article references-->
[Azure SQL Database business continuity overview]: ../sql-database/sql-database-business-continuity.md
[Request a DTU quota change]: ./sql-data-warehouse-get-started-create-support-ticket.md#request-quota-change
[Configure your database after recovery]: ../sql-database/sql-database-disaster-recovery.md#configure-your-database-after-recovery
[How tooinstall and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
[Overview]: ./sql-data-warehouse-restore-database-overview.md
[Portal]: ./sql-data-warehouse-restore-database-portal.md
[PowerShell]: ./sql-data-warehouse-restore-database-powershell.md
[REST]: ./sql-data-warehouse-restore-database-rest-api.md

<!--MSDN references-->
[Create database restore request]: https://msdn.microsoft.com/library/azure/dn509571.aspx
[Database operation status]: https://msdn.microsoft.com/library/azure/dn720371.aspx
[Get restorable dropped database]: https://msdn.microsoft.com/library/azure/dn509574.aspx
[List restorable dropped databases]: https://msdn.microsoft.com/library/azure/dn509562.aspx
[Restore-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt693390.aspx

<!--Other Web references-->
[Azure Portal]: https://portal.azure.com/
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
