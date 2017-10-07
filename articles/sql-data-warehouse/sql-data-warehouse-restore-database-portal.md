---
title: aaaRestore Azure SQL Data Warehouse (Azure portal) | Dokumentacja firmy Microsoft
description: Azure portalu zadania przywracania magazyn danych SQL Azure.
services: sql-data-warehouse
documentationcenter: NA
author: Lakshmi1812
manager: barbkess
editor: 
ms.assetid: b0aef539-7657-4b0e-9899-74098f5c21bc
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: backup-restore
ms.date: 09/21/2016
ms.author: lakshmir;barbkess
ms.openlocfilehash: cb225d2a21b61acab70a51b69c266f8d3ffacc9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="restore-azure-sql-data-warehouse-portal"></a>Przywracanie usługi Azure SQL Data Warehouse (portal)
> [!div class="op_single_selector"]
> * [Omówienie][Overview]
> * [Portal][Portal]
> * [Środowiska PowerShell][PowerShell]
> * [REST][REST]
>
>
W tym artykule dowiesz się, jak toorestore Azure SQL Data Warehouse przy użyciu hello portalu Azure.

## <a name="before-you-begin"></a>Przed rozpoczęciem
**Sprawdź, czy pojemność jednostek dtu w warstwie.** Każde wystąpienie usługi SQL Data Warehouse jest hostowana przez serwer SQL (na przykład myserver.database.windows.net), który ma domyślnego przydziału (bazy danych DTU) jednostki przepływności danych. Zanim będzie można przywrócić SQL Data Warehouse, sprawdź, czy program SQL server ma wystarczająco pozostałych limit przydziału jednostek DTU dla hello bazy danych, które są przywracane. toolearn limit przydziału jednostek DTU toocalculate lub toorequest Dtu więcej, zobacz temat [żądanie zmiany limitu przydziału jednostek dtu w warstwie][Request a DTU quota change].

## <a name="restore-an-active-or-paused-database"></a>Przywróć bazę danych aktywnej lub wstrzymana
toorestore bazy danych:

1. Zaloguj się toohello [portalu Azure][Azure portal].
2. Wybierz w okienku po lewej stronie powitania **Przeglądaj**, a następnie wybierz **serwerów SQL**.

    ![Wybierz opcję Przeglądaj > serwery SQL](./media/sql-data-warehouse-restore-database-portal/01-browse-for-sql-server.png)
3. Znajdź serwer, a następnie wybierz go.

    ![Wybierz serwer](./media/sql-data-warehouse-restore-database-portal/01-select-server.png)
4. Znajdź wystąpienie hello usługi SQL Data Warehouse, mają toorestore z, a następnie zaznacz go.

    ![Wybierz wystąpienie hello toorestore SQL Data Warehouse](./media/sql-data-warehouse-restore-database-portal/01-select-active-dw.png)
5. U góry hello hello bloku hurtowni danych, zaznacz pole wyboru **przywrócić**.

    ![Wybierz przywracania](./media/sql-data-warehouse-restore-database-portal/01-select-restore-from-active.png)
6. Określ nowy **Nazwa bazy danych**.
7. Wybierz hello najnowszych **punkt przywracania**.

   Upewnij się, że możesz wybrać hello najnowszy punkt przywracania. Ponieważ punkty przywracania są wyświetlane w uniwersalnego czasu koordynowanego (UTC), opcja domyślna hello może nie być hello najnowszy punkt przywracania.

      ![Wybierz punkt przywracania](./media/sql-data-warehouse-restore-database-portal/01-restore-blade-from-active.png)
8. Kliknij przycisk **OK**.
9. rozpocznie się proces przywracania bazy danych Hello i można użyć **powiadomienia** toomonitor hello procesu.

> [!NOTE]
> Po zakończeniu przywracania hello można skonfigurować odzyskanej bazy danych, wykonując [konfiguracji bazy danych po odzyskaniu][Configure your database after recovery].
>
>

## <a name="restore-a-deleted-database"></a>Przywracanie usuniętej bazy danych
toorestore usuniętej bazy danych:

1. Zaloguj się toohello [portalu Azure][Azure portal].
2. Wybierz w okienku po lewej stronie powitania **Przeglądaj**, a następnie wybierz **serwerów SQL**.

    ![Wybierz opcję Przeglądaj > serwery SQL](./media/sql-data-warehouse-restore-database-portal/01-browse-for-sql-server.png)
3. Znajdź serwer, a następnie wybierz go.

    ![Wybierz serwer](./media/sql-data-warehouse-restore-database-portal/02-select-server.png)
4. Przewiń w dół toohello **operacji** sekcji w bloku serwera.
5. Wybierz hello **usunięte bazy danych** kafelka.

    ![Wybierz hello usuniętych baz danych kafelków](./media/sql-data-warehouse-restore-database-portal/02-select-deleted-dws.png)
6. Wybierz hello usunąć bazę danych, które mają toorestore.

    ![Wybierz toorestore bazy danych](./media/sql-data-warehouse-restore-database-portal/02-select-deleted-dw.png)
7. Określ nowy **Nazwa bazy danych**.

    ![Dodaj nazwę hello bazy danych](./media/sql-data-warehouse-restore-database-portal/02-restore-blade-from-deleted.png)
8. Kliknij przycisk **OK**.
9. rozpocznie się proces przywracania bazy danych Hello i można użyć **powiadomienia** toomonitor hello procesu.

> [!NOTE]
> Zobacz bazy danych po zakończeniu przywracania hello tooconfigure [konfiguracji bazy danych po odzyskaniu][Configure your database after recovery].
>
>

## <a name="next-steps"></a>Następne kroki
toolearn o funkcjach ciągłości biznesowej hello wersji bazy danych SQL Azure, przeczytaj hello [omówienie ciągłości działalności biznesowej usługi Azure SQL Database][Azure SQL Database business continuity overview].

<!--Image references-->

<!--Article references-->
[Azure SQL Database business continuity overview]: ../sql-database/sql-database-business-continuity.md
[Overview]: ./sql-data-warehouse-restore-database-overview.md
[Portal]: ./sql-data-warehouse-restore-database-portal.md
[PowerShell]: ./sql-data-warehouse-restore-database-powershell.md
[REST]: ./sql-data-warehouse-restore-database-rest-api.md
[Configure your database after recovery]: ../sql-database/sql-database-disaster-recovery.md#configure-your-database-after-recovery
[Request a DTU quota change]: ./sql-data-warehouse-get-started-create-support-ticket.md#request-quota-change

<!--MSDN references-->

<!--Blog references-->

<!--Other Web references-->
[Azure portal]: https://portal.azure.com/
