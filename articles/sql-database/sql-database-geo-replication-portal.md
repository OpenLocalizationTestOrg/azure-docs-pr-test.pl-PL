---
title: 'Portalu Azure: replikacja geograficzna bazy danych SQL | Dokumentacja firmy Microsoft'
description: "Skonfiguruj — replikacja geograficzna bazy danych SQL Azure w portalu Azure i zainicjuj tryb failover"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: d0b29822-714f-4633-a5ab-fb1a09d43ced
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/06/2016
ms.author: carlrab
ms.openlocfilehash: db90fad2fe397f0c8466db6bdc1bd8c8d1cf8f15
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="configure-active-geo-replication-for-azure-sql-database-in-the-azure-portal-and-initiate-failover"></a><span data-ttu-id="9e338-103">Skonfiguruj aktywna replikacja geograficzna bazy danych SQL Azure w portalu Azure i zainicjuj tryb failover</span><span class="sxs-lookup"><span data-stu-id="9e338-103">Configure active geo-replication for Azure SQL Database in the Azure portal and initiate failover</span></span>

<span data-ttu-id="9e338-104">W tym artykule przedstawiono sposób konfigurowania bazy danych SQL w aktywna replikacja geograficzna [portalu Azure](http://portal.azure.com) i rozpoczęcie pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="9e338-104">This article shows you how to configure active geo-replication for SQL Database in the [Azure portal](http://portal.azure.com) and to initiate failover.</span></span>

<span data-ttu-id="9e338-105">Aby zainicjować trybu failover przy użyciu portalu Azure, zobacz [zainicjowanie planowanego lub nieplanowanego trybu failover dla bazy danych SQL Azure przy użyciu portalu Azure](sql-database-geo-replication-portal.md).</span><span class="sxs-lookup"><span data-stu-id="9e338-105">To initiate failover with the Azure portal, see [Initiate a planned or unplanned failover for Azure SQL Database with the Azure portal](sql-database-geo-replication-portal.md).</span></span>

<span data-ttu-id="9e338-106">Aktywna replikacja geograficzna należy skonfigurować przy użyciu portalu Azure, potrzebne są następujące zasoby:</span><span class="sxs-lookup"><span data-stu-id="9e338-106">To configure active geo-replication by using the Azure portal, you need the following resource:</span></span>

* <span data-ttu-id="9e338-107">Baza danych Azure SQL: podstawowej bazy danych, które mają być replikowane w innym regionie geograficznym.</span><span class="sxs-lookup"><span data-stu-id="9e338-107">An Azure SQL database: The primary database that you want to replicate to a different geographical region.</span></span>

> [!Note]
<span data-ttu-id="9e338-108">Aktywna replikacja geograficzna musi należeć do zakresu od bazy danych w tej samej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="9e338-108">Active geo-replication must be between databases in the same subscription.</span></span>

## <a name="add-a-secondary-database"></a><span data-ttu-id="9e338-109">Dodać pomocniczą bazę danych</span><span class="sxs-lookup"><span data-stu-id="9e338-109">Add a secondary database</span></span>
<span data-ttu-id="9e338-110">Następujące kroki tworzenia nowego pomocniczej bazy danych współpracują — replikacja geograficzna.</span><span class="sxs-lookup"><span data-stu-id="9e338-110">The following steps create a new secondary database in a geo-replication partnership.</span></span>  

<span data-ttu-id="9e338-111">Aby dodać pomocniczą bazę danych, musi być właścicielem subskrypcji lub współwłaściciel.</span><span class="sxs-lookup"><span data-stu-id="9e338-111">To add a secondary database, you must be the subscription owner or co-owner.</span></span>

<span data-ttu-id="9e338-112">Dodatkowej bazy danych ma taką samą nazwę co podstawowa baza danych i ma domyślnie na tym samym poziomie usługi.</span><span class="sxs-lookup"><span data-stu-id="9e338-112">The secondary database has the same name as the primary database and has, by default, the same service level.</span></span> <span data-ttu-id="9e338-113">Dodatkowej bazy danych może być pojedynczą bazę danych lub bazy danych w puli elastycznej.</span><span class="sxs-lookup"><span data-stu-id="9e338-113">The secondary database can be a single database or a database in an elastic pool.</span></span> <span data-ttu-id="9e338-114">Aby uzyskać więcej informacji, zobacz [warstw usług](sql-database-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="9e338-114">For more information, see [Service tiers](sql-database-service-tiers.md).</span></span>
<span data-ttu-id="9e338-115">Po utworzeniu i rozpoczęta pomocniczej, danych rozpoczyna replikację z podstawowej bazy danych do nowej dodatkowej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="9e338-115">After the secondary is created and seeded, data begins replicating from the primary database to the new secondary database.</span></span>

> [!NOTE]
> <span data-ttu-id="9e338-116">Jeśli baza danych partnera już istnieje (na przykład w wyniku zakończenia dotychczasowej relacji replikacji geograficznej) polecenie kończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="9e338-116">If the partner database already exists (for example, as a result of terminating a previous geo-replication relationship) the command fails.</span></span>
> 

1. <span data-ttu-id="9e338-117">W [portalu Azure](http://portal.azure.com), przejdź do bazy danych, który ma zostać skonfigurowany do replikacji geograficznej.</span><span class="sxs-lookup"><span data-stu-id="9e338-117">In the [Azure portal](http://portal.azure.com), browse to the database that you want to set up for geo-replication.</span></span>
2. <span data-ttu-id="9e338-118">Na stronie bazy danych SQL, wybierz **— replikacja geograficzna**, a następnie wybierz region do tworzenia pomocniczej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="9e338-118">On the SQL database page, select **geo-replication**, and then select the region to create the secondary database.</span></span> <span data-ttu-id="9e338-119">Można wybrać dowolny region inny niż region podstawowy bazę danych, ale zaleca się [sparowanego region](../best-practices-availability-paired-regions.md).</span><span class="sxs-lookup"><span data-stu-id="9e338-119">You can select any region other than the region hosting the primary database, but we recommend the [paired region](../best-practices-availability-paired-regions.md).</span></span>
   
    ![Konfigurowanie replikacji geograficznej](./media/sql-database-geo-replication-portal/configure-geo-replication.png)
3. <span data-ttu-id="9e338-121">Wybierz i skonfiguruj serwer i warstwę cenową dla pomocniczej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="9e338-121">Select or configure the server and pricing tier for the secondary database.</span></span>
   
    ![Konfigurowanie dodatkowej](./media/sql-database-geo-replication-portal/create-secondary.png)
4. <span data-ttu-id="9e338-123">Opcjonalnie można dodać pomocniczą bazę danych z puli elastycznej.</span><span class="sxs-lookup"><span data-stu-id="9e338-123">Optionally, you can add a secondary database to an elastic pool.</span></span> <span data-ttu-id="9e338-124">Aby utworzyć dodatkowej bazy danych w puli, kliknij przycisk **puli elastycznej** i wybierz pulę na serwerze docelowym.</span><span class="sxs-lookup"><span data-stu-id="9e338-124">To create the secondary database in a pool, click **elastic pool** and select a pool on the target server.</span></span> <span data-ttu-id="9e338-125">Pula musi już istnieć na serwerze docelowym.</span><span class="sxs-lookup"><span data-stu-id="9e338-125">A pool must already exist on the target server.</span></span> <span data-ttu-id="9e338-126">Ten przepływ pracy nie powoduje utworzenia puli.</span><span class="sxs-lookup"><span data-stu-id="9e338-126">This workflow does not create a pool.</span></span>
5. <span data-ttu-id="9e338-127">Kliknij przycisk **Utwórz** można dodać pomocniczy.</span><span class="sxs-lookup"><span data-stu-id="9e338-127">Click **Create** to add the secondary.</span></span>
6. <span data-ttu-id="9e338-128">Utworzono dodatkowej bazy danych i rozpocznie się proces rozmieszczania.</span><span class="sxs-lookup"><span data-stu-id="9e338-128">The secondary database is created and the seeding process begins.</span></span>
   
    ![Konfigurowanie dodatkowej](./media/sql-database-geo-replication-portal/seeding0.png)
7. <span data-ttu-id="9e338-130">Po zakończeniu procesu rozmieszczania dodatkowej bazy danych wyświetla jego stan.</span><span class="sxs-lookup"><span data-stu-id="9e338-130">When the seeding process is complete, the secondary database displays its status.</span></span>
   
    ![Wstępne wypełnianie ukończone](./media/sql-database-geo-replication-portal/seeding-complete.png)

## <a name="initiate-a-failover"></a><span data-ttu-id="9e338-132">Zainicjuj tryb failover</span><span class="sxs-lookup"><span data-stu-id="9e338-132">Initiate a failover</span></span>

<span data-ttu-id="9e338-133">Dodatkowej bazy danych mogą być przełączane do stają się serwerem podstawowym.</span><span class="sxs-lookup"><span data-stu-id="9e338-133">The secondary database can be switched to become the primary.</span></span>  

1. <span data-ttu-id="9e338-134">W [portalu Azure](http://portal.azure.com), przejdź do podstawowej bazy danych — replikacja geograficzna wspólnie.</span><span class="sxs-lookup"><span data-stu-id="9e338-134">In the [Azure portal](http://portal.azure.com), browse to the primary database in the geo-replication partnership.</span></span>
2. <span data-ttu-id="9e338-135">W bloku bazy danych SQL, wybierz **wszystkie ustawienia** > **— replikacja geograficzna**.</span><span class="sxs-lookup"><span data-stu-id="9e338-135">On the SQL Database blade, select **All settings** > **geo-replication**.</span></span>
3. <span data-ttu-id="9e338-136">W **pomocniczych** listy, wybierz bazę danych, aby stać się nową podstawową, a następnie kliknij przycisk **pracy awaryjnej**.</span><span class="sxs-lookup"><span data-stu-id="9e338-136">In the **SECONDARIES** list, select the database you want to become the new primary and click **Failover**.</span></span>
   
    ![tryb failover](./media/sql-database-geo-replication-failover-portal/secondaries.png)
4. <span data-ttu-id="9e338-138">Kliknij przycisk **tak** do rozpoczęcia pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="9e338-138">Click **Yes** to begin the failover.</span></span>

<span data-ttu-id="9e338-139">Polecenie natychmiast zmienia dodatkowej bazy danych do roli podstawowego.</span><span class="sxs-lookup"><span data-stu-id="9e338-139">The command immediately switches the secondary database into the primary role.</span></span> 

<span data-ttu-id="9e338-140">Istnieje krótki okres, podczas którego obie bazy danych są niedostępne (rzędu 0 do 25 sekund), podczas przełączania ról.</span><span class="sxs-lookup"><span data-stu-id="9e338-140">There is a short period during which both databases are unavailable (on the order of 0 to 25 seconds) while the roles are switched.</span></span> <span data-ttu-id="9e338-141">Jeśli podstawowa baza danych ma wiele baz danych w dodatkowej, polecenie automatycznie skonfiguruje replik pomocniczych do nawiązania połączenia nową podstawową.</span><span class="sxs-lookup"><span data-stu-id="9e338-141">If the primary database has multiple secondary databases, the command automatically reconfigures the other secondaries to connect to the new primary.</span></span> <span data-ttu-id="9e338-142">Cała operacja powinny zająć mniej niż minutę w normalnych okolicznościach.</span><span class="sxs-lookup"><span data-stu-id="9e338-142">The entire operation should take less than a minute to complete under normal circumstances.</span></span> 

> [!NOTE]
> <span data-ttu-id="9e338-143">To polecenie jest przeznaczona dla Szybkie odzyskiwanie bazy danych w przypadku awarii.</span><span class="sxs-lookup"><span data-stu-id="9e338-143">This command is designed for quick recovery of the database in case of an outage.</span></span> <span data-ttu-id="9e338-144">Wyzwala trybu failover bez synchronizacji danych (wymuszone trybu failover).</span><span class="sxs-lookup"><span data-stu-id="9e338-144">It triggers failover without data synchronization (forced failover).</span></span>  <span data-ttu-id="9e338-145">Jeśli podstawowy jest w trybie online i może wystąpić, zatwierdzania transakcji, gdy wydano polecenie utratę danych.</span><span class="sxs-lookup"><span data-stu-id="9e338-145">If the primary is online and committing transactions when the command is issued some data loss may occur.</span></span> 
> 
> 

## <a name="remove-secondary-database"></a><span data-ttu-id="9e338-146">Usuń z dodatkowej bazy danych</span><span class="sxs-lookup"><span data-stu-id="9e338-146">Remove secondary database</span></span>
<span data-ttu-id="9e338-147">Ta operacja trwale kończy replikację do dodatkowej bazy danych i zmiany roli pomocniczej zwykłej odczytu i zapisu bazy danych.</span><span class="sxs-lookup"><span data-stu-id="9e338-147">This operation permanently terminates the replication to the secondary database, and changes the role of the secondary to a regular read-write database.</span></span> <span data-ttu-id="9e338-148">Łączność z dodatkowej bazy danych jest uszkodzona, polecenie powiedzie się, ale ma dodatkowej, staje się odczytu i zapisu, dopóki łączność zostanie przywrócona.</span><span class="sxs-lookup"><span data-stu-id="9e338-148">If the connectivity to the secondary database is broken, the command succeeds but the secondary does not become read-write until after connectivity is restored.</span></span>  

1. <span data-ttu-id="9e338-149">W [portalu Azure](http://portal.azure.com), przejdź do podstawowej bazy danych — replikacja geograficzna wspólnie.</span><span class="sxs-lookup"><span data-stu-id="9e338-149">In the [Azure portal](http://portal.azure.com), browse to the primary database in the geo-replication partnership.</span></span>
2. <span data-ttu-id="9e338-150">Na stronie bazy danych SQL, wybierz **— replikacja geograficzna**.</span><span class="sxs-lookup"><span data-stu-id="9e338-150">On the SQL database page, select **geo-replication**.</span></span>
3. <span data-ttu-id="9e338-151">W **pomocniczych** listy, wybierz bazę danych, aby usunąć z powiązania — replikacja geograficzna.</span><span class="sxs-lookup"><span data-stu-id="9e338-151">In the **SECONDARIES** list, select the database you want to remove from the geo-replication partnership.</span></span>
4. <span data-ttu-id="9e338-152">Kliknij przycisk **Zatrzymaj replikację,**.</span><span class="sxs-lookup"><span data-stu-id="9e338-152">Click **Stop Replication**.</span></span>
   
    ![Usuń pomocniczej](./media/sql-database-geo-replication-portal/remove-secondary.png)
5. <span data-ttu-id="9e338-154">Zostanie wyświetlone okno potwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="9e338-154">A confirmation window opens.</span></span> <span data-ttu-id="9e338-155">Kliknij przycisk **tak** usunąć bazę danych z powiązania — replikacja geograficzna.</span><span class="sxs-lookup"><span data-stu-id="9e338-155">Click **Yes** to remove the database from the geo-replication partnership.</span></span> <span data-ttu-id="9e338-156">(Ustawia go do odczytu i zapisu bazy danych nie jest częścią replikacji).</span><span class="sxs-lookup"><span data-stu-id="9e338-156">(Set it to a read-write database not part of any replication.)</span></span>

## <a name="next-steps"></a><span data-ttu-id="9e338-157">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9e338-157">Next steps</span></span>
* <span data-ttu-id="9e338-158">Aby dowiedzieć się więcej na temat aktywna replikacja geograficzna, zobacz [aktywna replikacja geograficzna](sql-database-geo-replication-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9e338-158">To learn more about active geo-replication, see [active geo-replication](sql-database-geo-replication-overview.md).</span></span>
* <span data-ttu-id="9e338-159">Omówienie ciągłości działalności biznesowej i scenariuszy, zobacz [omówienie ciągłości działalności biznesowej](sql-database-business-continuity.md).</span><span class="sxs-lookup"><span data-stu-id="9e338-159">For a business continuity overview and scenarios, see [Business continuity overview](sql-database-business-continuity.md).</span></span>

