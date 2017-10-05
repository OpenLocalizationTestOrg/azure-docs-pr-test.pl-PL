---
title: "Przywracanie usługi Azure SQL Data Warehouse (Azure portal) | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: f6bc8671410dc7015a8d2a4bea1ba11f9ae526c3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="restore-azure-sql-data-warehouse-portal"></a><span data-ttu-id="f6b21-103">Przywracanie usługi Azure SQL Data Warehouse (portal)</span><span class="sxs-lookup"><span data-stu-id="f6b21-103">Restore Azure SQL Data Warehouse (portal)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="f6b21-104">[Omówienie][Overview]</span><span class="sxs-lookup"><span data-stu-id="f6b21-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="f6b21-105">[Portal][Portal]</span><span class="sxs-lookup"><span data-stu-id="f6b21-105">[Portal][Portal]</span></span>
> * <span data-ttu-id="f6b21-106">[Środowiska PowerShell][PowerShell]</span><span class="sxs-lookup"><span data-stu-id="f6b21-106">[PowerShell][PowerShell]</span></span>
> * <span data-ttu-id="f6b21-107">[REST][REST]</span><span class="sxs-lookup"><span data-stu-id="f6b21-107">[REST][REST]</span></span>
>
>
<span data-ttu-id="f6b21-108">W tym artykule dowiesz się, jak przywrócić Azure SQL Data Warehouse przy użyciu portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="f6b21-108">In this article, you will learn how to restore Azure SQL Data Warehouse by using the Azure portal.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="f6b21-109">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="f6b21-109">Before you begin</span></span>
<span data-ttu-id="f6b21-110">**Sprawdź, czy pojemność jednostek dtu w warstwie.**</span><span class="sxs-lookup"><span data-stu-id="f6b21-110">**Verify your DTU capacity.**</span></span> <span data-ttu-id="f6b21-111">Każde wystąpienie usługi SQL Data Warehouse jest hostowana przez serwer SQL (na przykład myserver.database.windows.net), który ma domyślnego przydziału (bazy danych DTU) jednostki przepływności danych.</span><span class="sxs-lookup"><span data-stu-id="f6b21-111">Each instance of SQL Data Warehouse is hosted by a SQL server (for example, myserver.database.windows.net) which has a default data throughput unit (DTU) quota.</span></span> <span data-ttu-id="f6b21-112">Zanim będzie można przywrócić SQL Data Warehouse, sprawdź, czy program SQL server ma wystarczająco pozostałych limit przydziału jednostek DTU w przypadku przywracania bazy danych.</span><span class="sxs-lookup"><span data-stu-id="f6b21-112">Before you can restore SQL Data Warehouse, verify that your SQL server has enough remaining DTU quota for the database that you're restoring.</span></span> <span data-ttu-id="f6b21-113">Aby dowiedzieć się jak obliczyć limit przydziału jednostek DTU lub zażądać więcej jednostek Dtu, zobacz [żądanie zmiany limitu przydziału jednostek dtu w warstwie][Request a DTU quota change].</span><span class="sxs-lookup"><span data-stu-id="f6b21-113">To learn how to calculate DTU quota or to request more DTUs, see [Request a DTU quota change][Request a DTU quota change].</span></span>

## <a name="restore-an-active-or-paused-database"></a><span data-ttu-id="f6b21-114">Przywróć bazę danych aktywnej lub wstrzymana</span><span class="sxs-lookup"><span data-stu-id="f6b21-114">Restore an active or paused database</span></span>
<span data-ttu-id="f6b21-115">Przywracanie bazy danych:</span><span class="sxs-lookup"><span data-stu-id="f6b21-115">To restore a database:</span></span>

1. <span data-ttu-id="f6b21-116">Zaloguj się w witrynie [Azure Portal][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="f6b21-116">Sign in to the [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="f6b21-117">W okienku po lewej stronie wybierz **Przeglądaj**, a następnie wybierz **serwerów SQL**.</span><span class="sxs-lookup"><span data-stu-id="f6b21-117">In the left pane, select **Browse**, and then select **SQL servers**.</span></span>

    ![Wybierz opcję Przeglądaj > serwery SQL](./media/sql-data-warehouse-restore-database-portal/01-browse-for-sql-server.png)
3. <span data-ttu-id="f6b21-119">Znajdź serwer, a następnie wybierz go.</span><span class="sxs-lookup"><span data-stu-id="f6b21-119">Find your server, and then select it.</span></span>

    ![Wybierz serwer](./media/sql-data-warehouse-restore-database-portal/01-select-server.png)
4. <span data-ttu-id="f6b21-121">Znajdź wystąpienie programu SQL Data Warehouse, który chcesz przywrócić z, a następnie wybierz go.</span><span class="sxs-lookup"><span data-stu-id="f6b21-121">Find the instance of SQL Data Warehouse that you want to restore from, and then select it.</span></span>

    ![Wybierz wystąpienie programu SQL magazynu danych do przywrócenia](./media/sql-data-warehouse-restore-database-portal/01-select-active-dw.png)
5. <span data-ttu-id="f6b21-123">W górnej części bloku hurtowni danych, wybierz **przywrócić**.</span><span class="sxs-lookup"><span data-stu-id="f6b21-123">At the top of the Data Warehouse blade, select **Restore**.</span></span>

    ![Wybierz przywracania](./media/sql-data-warehouse-restore-database-portal/01-select-restore-from-active.png)
6. <span data-ttu-id="f6b21-125">Określ nowy **Nazwa bazy danych**.</span><span class="sxs-lookup"><span data-stu-id="f6b21-125">Specify a new **Database name**.</span></span>
7. <span data-ttu-id="f6b21-126">Wybierz najnowszą **punkt przywracania**.</span><span class="sxs-lookup"><span data-stu-id="f6b21-126">Select the latest **Restore point**.</span></span>

   <span data-ttu-id="f6b21-127">Upewnij się, że została wybrana do ostatniego punktu przywracania.</span><span class="sxs-lookup"><span data-stu-id="f6b21-127">Make sure you choose the latest restore point.</span></span> <span data-ttu-id="f6b21-128">Ponieważ punkty przywracania są wyświetlane w uniwersalnego czasu koordynowanego (UTC), opcją domyślną może nie być do ostatniego punktu przywracania.</span><span class="sxs-lookup"><span data-stu-id="f6b21-128">Because restore points are shown in Coordinated Universal Time (UTC), the default option might not be the latest restore point.</span></span>

      ![Wybierz punkt przywracania](./media/sql-data-warehouse-restore-database-portal/01-restore-blade-from-active.png)
8. <span data-ttu-id="f6b21-130">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="f6b21-130">Select **OK**.</span></span>
9. <span data-ttu-id="f6b21-131">Rozpocznie się proces przywracania bazy danych, a następnie można użyć **powiadomienia** do monitorowania procesu.</span><span class="sxs-lookup"><span data-stu-id="f6b21-131">The database restore process will begin, and you can use **NOTIFICATIONS** to monitor the process.</span></span>

> [!NOTE]
> <span data-ttu-id="f6b21-132">Po zakończeniu przywracania, można skonfigurować odzyskanej bazy danych, wykonując [konfiguracji bazy danych po odzyskaniu][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="f6b21-132">After the restore has finished, you can configure your recovered database by following [Configure your database after recovery][Configure your database after recovery].</span></span>
>
>

## <a name="restore-a-deleted-database"></a><span data-ttu-id="f6b21-133">Przywracanie usuniętej bazy danych</span><span class="sxs-lookup"><span data-stu-id="f6b21-133">Restore a deleted database</span></span>
<span data-ttu-id="f6b21-134">Aby przywrócić usunięte bazy danych:</span><span class="sxs-lookup"><span data-stu-id="f6b21-134">To restore a deleted database:</span></span>

1. <span data-ttu-id="f6b21-135">Zaloguj się w witrynie [Azure Portal][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="f6b21-135">Sign in to the [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="f6b21-136">W okienku po lewej stronie wybierz **Przeglądaj**, a następnie wybierz **serwerów SQL**.</span><span class="sxs-lookup"><span data-stu-id="f6b21-136">In the left pane, select **Browse**, and then select **SQL servers**.</span></span>

    ![Wybierz opcję Przeglądaj > serwery SQL](./media/sql-data-warehouse-restore-database-portal/01-browse-for-sql-server.png)
3. <span data-ttu-id="f6b21-138">Znajdź serwer, a następnie wybierz go.</span><span class="sxs-lookup"><span data-stu-id="f6b21-138">Find your server, and then select it.</span></span>

    ![Wybierz serwer](./media/sql-data-warehouse-restore-database-portal/02-select-server.png)
4. <span data-ttu-id="f6b21-140">Przewiń w dół do **operacji** sekcji w bloku serwera.</span><span class="sxs-lookup"><span data-stu-id="f6b21-140">Scroll down to the **Operations** section on your server's blade.</span></span>
5. <span data-ttu-id="f6b21-141">Wybierz **usunięte bazy danych** kafelka.</span><span class="sxs-lookup"><span data-stu-id="f6b21-141">Select the **Deleted databases** tile.</span></span>

    ![Wybierz Kafelek usunięte bazy danych](./media/sql-data-warehouse-restore-database-portal/02-select-deleted-dws.png)
6. <span data-ttu-id="f6b21-143">Wybierz usuniętej bazy danych, który chcesz przywrócić.</span><span class="sxs-lookup"><span data-stu-id="f6b21-143">Select the deleted database that you want to restore.</span></span>

    ![Wybierz bazę danych do przywrócenia](./media/sql-data-warehouse-restore-database-portal/02-select-deleted-dw.png)
7. <span data-ttu-id="f6b21-145">Określ nowy **Nazwa bazy danych**.</span><span class="sxs-lookup"><span data-stu-id="f6b21-145">Specify a new **Database name**.</span></span>

    ![Dodaj nazwę bazy danych](./media/sql-data-warehouse-restore-database-portal/02-restore-blade-from-deleted.png)
8. <span data-ttu-id="f6b21-147">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="f6b21-147">Select **OK**.</span></span>
9. <span data-ttu-id="f6b21-148">Rozpocznie się proces przywracania bazy danych, a następnie można użyć **powiadomienia** do monitorowania procesu.</span><span class="sxs-lookup"><span data-stu-id="f6b21-148">The database restore process will begin, and you can use **NOTIFICATIONS** to monitor the process.</span></span>

> [!NOTE]
> <span data-ttu-id="f6b21-149">Aby skonfigurować bazę danych, po zakończeniu przywracania, zobacz [konfiguracji bazy danych po odzyskaniu][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="f6b21-149">To configure your database after the restore has finished, see [Configure your database after recovery][Configure your database after recovery].</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="f6b21-150">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f6b21-150">Next steps</span></span>
<span data-ttu-id="f6b21-151">Aby dowiedzieć się więcej o funkcjach ciągłości biznesowej wersji bazy danych SQL Azure, przeczytaj [omówienie ciągłości działalności biznesowej usługi Azure SQL Database][Azure SQL Database business continuity overview].</span><span class="sxs-lookup"><span data-stu-id="f6b21-151">To learn about the business continuity features of Azure SQL Database editions, read the [Azure SQL Database business continuity overview][Azure SQL Database business continuity overview].</span></span>

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
