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
# <a name="restore-azure-sql-data-warehouse-portal"></a><span data-ttu-id="6e975-103">Przywracanie usługi Azure SQL Data Warehouse (portal)</span><span class="sxs-lookup"><span data-stu-id="6e975-103">Restore Azure SQL Data Warehouse (portal)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="6e975-104">[Omówienie][Overview]</span><span class="sxs-lookup"><span data-stu-id="6e975-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="6e975-105">[Portal][Portal]</span><span class="sxs-lookup"><span data-stu-id="6e975-105">[Portal][Portal]</span></span>
> * <span data-ttu-id="6e975-106">[Środowiska PowerShell][PowerShell]</span><span class="sxs-lookup"><span data-stu-id="6e975-106">[PowerShell][PowerShell]</span></span>
> * <span data-ttu-id="6e975-107">[REST][REST]</span><span class="sxs-lookup"><span data-stu-id="6e975-107">[REST][REST]</span></span>
>
>
<span data-ttu-id="6e975-108">W tym artykule dowiesz się, jak toorestore Azure SQL Data Warehouse przy użyciu hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="6e975-108">In this article, you will learn how toorestore Azure SQL Data Warehouse by using hello Azure portal.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="6e975-109">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="6e975-109">Before you begin</span></span>
<span data-ttu-id="6e975-110">**Sprawdź, czy pojemność jednostek dtu w warstwie.**</span><span class="sxs-lookup"><span data-stu-id="6e975-110">**Verify your DTU capacity.**</span></span> <span data-ttu-id="6e975-111">Każde wystąpienie usługi SQL Data Warehouse jest hostowana przez serwer SQL (na przykład myserver.database.windows.net), który ma domyślnego przydziału (bazy danych DTU) jednostki przepływności danych.</span><span class="sxs-lookup"><span data-stu-id="6e975-111">Each instance of SQL Data Warehouse is hosted by a SQL server (for example, myserver.database.windows.net) which has a default data throughput unit (DTU) quota.</span></span> <span data-ttu-id="6e975-112">Zanim będzie można przywrócić SQL Data Warehouse, sprawdź, czy program SQL server ma wystarczająco pozostałych limit przydziału jednostek DTU dla hello bazy danych, które są przywracane.</span><span class="sxs-lookup"><span data-stu-id="6e975-112">Before you can restore SQL Data Warehouse, verify that your SQL server has enough remaining DTU quota for hello database that you're restoring.</span></span> <span data-ttu-id="6e975-113">toolearn limit przydziału jednostek DTU toocalculate lub toorequest Dtu więcej, zobacz temat [żądanie zmiany limitu przydziału jednostek dtu w warstwie][Request a DTU quota change].</span><span class="sxs-lookup"><span data-stu-id="6e975-113">toolearn how toocalculate DTU quota or toorequest more DTUs, see [Request a DTU quota change][Request a DTU quota change].</span></span>

## <a name="restore-an-active-or-paused-database"></a><span data-ttu-id="6e975-114">Przywróć bazę danych aktywnej lub wstrzymana</span><span class="sxs-lookup"><span data-stu-id="6e975-114">Restore an active or paused database</span></span>
<span data-ttu-id="6e975-115">toorestore bazy danych:</span><span class="sxs-lookup"><span data-stu-id="6e975-115">toorestore a database:</span></span>

1. <span data-ttu-id="6e975-116">Zaloguj się toohello [portalu Azure][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="6e975-116">Sign in toohello [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="6e975-117">Wybierz w okienku po lewej stronie powitania **Przeglądaj**, a następnie wybierz **serwerów SQL**.</span><span class="sxs-lookup"><span data-stu-id="6e975-117">In hello left pane, select **Browse**, and then select **SQL servers**.</span></span>

    ![Wybierz opcję Przeglądaj > serwery SQL](./media/sql-data-warehouse-restore-database-portal/01-browse-for-sql-server.png)
3. <span data-ttu-id="6e975-119">Znajdź serwer, a następnie wybierz go.</span><span class="sxs-lookup"><span data-stu-id="6e975-119">Find your server, and then select it.</span></span>

    ![Wybierz serwer](./media/sql-data-warehouse-restore-database-portal/01-select-server.png)
4. <span data-ttu-id="6e975-121">Znajdź wystąpienie hello usługi SQL Data Warehouse, mają toorestore z, a następnie zaznacz go.</span><span class="sxs-lookup"><span data-stu-id="6e975-121">Find hello instance of SQL Data Warehouse that you want toorestore from, and then select it.</span></span>

    ![Wybierz wystąpienie hello toorestore SQL Data Warehouse](./media/sql-data-warehouse-restore-database-portal/01-select-active-dw.png)
5. <span data-ttu-id="6e975-123">U góry hello hello bloku hurtowni danych, zaznacz pole wyboru **przywrócić**.</span><span class="sxs-lookup"><span data-stu-id="6e975-123">At hello top of hello Data Warehouse blade, select **Restore**.</span></span>

    ![Wybierz przywracania](./media/sql-data-warehouse-restore-database-portal/01-select-restore-from-active.png)
6. <span data-ttu-id="6e975-125">Określ nowy **Nazwa bazy danych**.</span><span class="sxs-lookup"><span data-stu-id="6e975-125">Specify a new **Database name**.</span></span>
7. <span data-ttu-id="6e975-126">Wybierz hello najnowszych **punkt przywracania**.</span><span class="sxs-lookup"><span data-stu-id="6e975-126">Select hello latest **Restore point**.</span></span>

   <span data-ttu-id="6e975-127">Upewnij się, że możesz wybrać hello najnowszy punkt przywracania.</span><span class="sxs-lookup"><span data-stu-id="6e975-127">Make sure you choose hello latest restore point.</span></span> <span data-ttu-id="6e975-128">Ponieważ punkty przywracania są wyświetlane w uniwersalnego czasu koordynowanego (UTC), opcja domyślna hello może nie być hello najnowszy punkt przywracania.</span><span class="sxs-lookup"><span data-stu-id="6e975-128">Because restore points are shown in Coordinated Universal Time (UTC), hello default option might not be hello latest restore point.</span></span>

      ![Wybierz punkt przywracania](./media/sql-data-warehouse-restore-database-portal/01-restore-blade-from-active.png)
8. <span data-ttu-id="6e975-130">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="6e975-130">Select **OK**.</span></span>
9. <span data-ttu-id="6e975-131">rozpocznie się proces przywracania bazy danych Hello i można użyć **powiadomienia** toomonitor hello procesu.</span><span class="sxs-lookup"><span data-stu-id="6e975-131">hello database restore process will begin, and you can use **NOTIFICATIONS** toomonitor hello process.</span></span>

> [!NOTE]
> <span data-ttu-id="6e975-132">Po zakończeniu przywracania hello można skonfigurować odzyskanej bazy danych, wykonując [konfiguracji bazy danych po odzyskaniu][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="6e975-132">After hello restore has finished, you can configure your recovered database by following [Configure your database after recovery][Configure your database after recovery].</span></span>
>
>

## <a name="restore-a-deleted-database"></a><span data-ttu-id="6e975-133">Przywracanie usuniętej bazy danych</span><span class="sxs-lookup"><span data-stu-id="6e975-133">Restore a deleted database</span></span>
<span data-ttu-id="6e975-134">toorestore usuniętej bazy danych:</span><span class="sxs-lookup"><span data-stu-id="6e975-134">toorestore a deleted database:</span></span>

1. <span data-ttu-id="6e975-135">Zaloguj się toohello [portalu Azure][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="6e975-135">Sign in toohello [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="6e975-136">Wybierz w okienku po lewej stronie powitania **Przeglądaj**, a następnie wybierz **serwerów SQL**.</span><span class="sxs-lookup"><span data-stu-id="6e975-136">In hello left pane, select **Browse**, and then select **SQL servers**.</span></span>

    ![Wybierz opcję Przeglądaj > serwery SQL](./media/sql-data-warehouse-restore-database-portal/01-browse-for-sql-server.png)
3. <span data-ttu-id="6e975-138">Znajdź serwer, a następnie wybierz go.</span><span class="sxs-lookup"><span data-stu-id="6e975-138">Find your server, and then select it.</span></span>

    ![Wybierz serwer](./media/sql-data-warehouse-restore-database-portal/02-select-server.png)
4. <span data-ttu-id="6e975-140">Przewiń w dół toohello **operacji** sekcji w bloku serwera.</span><span class="sxs-lookup"><span data-stu-id="6e975-140">Scroll down toohello **Operations** section on your server's blade.</span></span>
5. <span data-ttu-id="6e975-141">Wybierz hello **usunięte bazy danych** kafelka.</span><span class="sxs-lookup"><span data-stu-id="6e975-141">Select hello **Deleted databases** tile.</span></span>

    ![Wybierz hello usuniętych baz danych kafelków](./media/sql-data-warehouse-restore-database-portal/02-select-deleted-dws.png)
6. <span data-ttu-id="6e975-143">Wybierz hello usunąć bazę danych, które mają toorestore.</span><span class="sxs-lookup"><span data-stu-id="6e975-143">Select hello deleted database that you want toorestore.</span></span>

    ![Wybierz toorestore bazy danych](./media/sql-data-warehouse-restore-database-portal/02-select-deleted-dw.png)
7. <span data-ttu-id="6e975-145">Określ nowy **Nazwa bazy danych**.</span><span class="sxs-lookup"><span data-stu-id="6e975-145">Specify a new **Database name**.</span></span>

    ![Dodaj nazwę hello bazy danych](./media/sql-data-warehouse-restore-database-portal/02-restore-blade-from-deleted.png)
8. <span data-ttu-id="6e975-147">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="6e975-147">Select **OK**.</span></span>
9. <span data-ttu-id="6e975-148">rozpocznie się proces przywracania bazy danych Hello i można użyć **powiadomienia** toomonitor hello procesu.</span><span class="sxs-lookup"><span data-stu-id="6e975-148">hello database restore process will begin, and you can use **NOTIFICATIONS** toomonitor hello process.</span></span>

> [!NOTE]
> <span data-ttu-id="6e975-149">Zobacz bazy danych po zakończeniu przywracania hello tooconfigure [konfiguracji bazy danych po odzyskaniu][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="6e975-149">tooconfigure your database after hello restore has finished, see [Configure your database after recovery][Configure your database after recovery].</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="6e975-150">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6e975-150">Next steps</span></span>
<span data-ttu-id="6e975-151">toolearn o funkcjach ciągłości biznesowej hello wersji bazy danych SQL Azure, przeczytaj hello [omówienie ciągłości działalności biznesowej usługi Azure SQL Database][Azure SQL Database business continuity overview].</span><span class="sxs-lookup"><span data-stu-id="6e975-151">toolearn about hello business continuity features of Azure SQL Database editions, read hello [Azure SQL Database business continuity overview][Azure SQL Database business continuity overview].</span></span>

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
