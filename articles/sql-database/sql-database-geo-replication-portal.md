---
title: 'Portalu Azure: replikacja geograficzna bazy danych SQL | Dokumentacja firmy Microsoft'
description: "Skonfiguruj — replikacja geograficzna bazy danych SQL Azure w hello portalu Azure i zainicjuj tryb failover"
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
ms.openlocfilehash: 09cbbdb040f36c42593e3be87ce6db2238f36656
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-active-geo-replication-for-azure-sql-database-in-hello-azure-portal-and-initiate-failover"></a><span data-ttu-id="fcea6-103">Skonfiguruj aktywna replikacja geograficzna bazy danych SQL Azure w hello portalu Azure i zainicjuj tryb failover</span><span class="sxs-lookup"><span data-stu-id="fcea6-103">Configure active geo-replication for Azure SQL Database in hello Azure portal and initiate failover</span></span>

<span data-ttu-id="fcea6-104">W tym artykule opisano sposób tooconfigure aktywna replikacja geograficzna bazy danych SQL w hello [portalu Azure](http://portal.azure.com) i tooinitiate trybu failover.</span><span class="sxs-lookup"><span data-stu-id="fcea6-104">This article shows you how tooconfigure active geo-replication for SQL Database in hello [Azure portal](http://portal.azure.com) and tooinitiate failover.</span></span>

<span data-ttu-id="fcea6-105">tryb failover tooinitiate z hello portalu Azure, zobacz [zainicjować planowanego lub nieplanowanego trybu failover dla bazy danych SQL Azure z portalu Azure hello](sql-database-geo-replication-portal.md).</span><span class="sxs-lookup"><span data-stu-id="fcea6-105">tooinitiate failover with hello Azure portal, see [Initiate a planned or unplanned failover for Azure SQL Database with hello Azure portal](sql-database-geo-replication-portal.md).</span></span>

<span data-ttu-id="fcea6-106">tooconfigure aktywna replikacja geograficzna przy użyciu hello portalu Azure, należy hello następujących zasobów:</span><span class="sxs-lookup"><span data-stu-id="fcea6-106">tooconfigure active geo-replication by using hello Azure portal, you need hello following resource:</span></span>

* <span data-ttu-id="fcea6-107">Baza danych Azure SQL: podstawowej bazy danych hello, które mają tooreplicate tooa inny region geograficzny.</span><span class="sxs-lookup"><span data-stu-id="fcea6-107">An Azure SQL database: hello primary database that you want tooreplicate tooa different geographical region.</span></span>

> [!Note]
<span data-ttu-id="fcea6-108">Aktywna replikacja geograficzna musi należeć do zakresu od baz danych w hello tej samej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="fcea6-108">Active geo-replication must be between databases in hello same subscription.</span></span>

## <a name="add-a-secondary-database"></a><span data-ttu-id="fcea6-109">Dodać pomocniczą bazę danych</span><span class="sxs-lookup"><span data-stu-id="fcea6-109">Add a secondary database</span></span>
<span data-ttu-id="fcea6-110">Hello następujące kroki tworzenia nowego pomocniczej bazy danych współpracują — replikacja geograficzna.</span><span class="sxs-lookup"><span data-stu-id="fcea6-110">hello following steps create a new secondary database in a geo-replication partnership.</span></span>  

<span data-ttu-id="fcea6-111">tooadd pomocniczej bazy danych musi być właścicielem subskrypcji hello lub współwłaściciel.</span><span class="sxs-lookup"><span data-stu-id="fcea6-111">tooadd a secondary database, you must be hello subscription owner or co-owner.</span></span>

<span data-ttu-id="fcea6-112">Hello dodatkowej bazy danych ma takie same nazwy co podstawowa baza danych: hello hello i domyślnie ma hello tego samego poziomu usług.</span><span class="sxs-lookup"><span data-stu-id="fcea6-112">hello secondary database has hello same name as hello primary database and has, by default, hello same service level.</span></span> <span data-ttu-id="fcea6-113">Witaj dodatkowej bazy danych może być pojedynczą bazę danych lub bazę danych w puli elastycznej.</span><span class="sxs-lookup"><span data-stu-id="fcea6-113">hello secondary database can be a single database or a database in an elastic pool.</span></span> <span data-ttu-id="fcea6-114">Aby uzyskać więcej informacji, zobacz [warstw usług](sql-database-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="fcea6-114">For more information, see [Service tiers](sql-database-service-tiers.md).</span></span>
<span data-ttu-id="fcea6-115">Po utworzeniu i rozpoczęta hello dodatkowej, rozpoczyna się danych replikacji z hello podstawowej bazy danych toohello nowe pomocnicze bazy danych.</span><span class="sxs-lookup"><span data-stu-id="fcea6-115">After hello secondary is created and seeded, data begins replicating from hello primary database toohello new secondary database.</span></span>

> [!NOTE]
> <span data-ttu-id="fcea6-116">(Na przykład w wyniku zakończenia dotychczasowej relacji replikacji geograficznej) istnieje już baza danych partnera hello hello polecenie kończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="fcea6-116">If hello partner database already exists (for example, as a result of terminating a previous geo-replication relationship) hello command fails.</span></span>
> 

1. <span data-ttu-id="fcea6-117">W hello [portalu Azure](http://portal.azure.com), Przeglądaj toohello bazy danych, które mają tooset dla replikacji geograficznej.</span><span class="sxs-lookup"><span data-stu-id="fcea6-117">In hello [Azure portal](http://portal.azure.com), browse toohello database that you want tooset up for geo-replication.</span></span>
2. <span data-ttu-id="fcea6-118">Na stronie bazy danych SQL hello zaznacz **— replikacja geograficzna**, a następnie wybierz hello region toocreate hello dodatkowej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="fcea6-118">On hello SQL database page, select **geo-replication**, and then select hello region toocreate hello secondary database.</span></span> <span data-ttu-id="fcea6-119">Można wybrać dowolny region niż region hello hosting hello podstawowej bazy danych, ale zaleca się hello [sparowanego region](../best-practices-availability-paired-regions.md).</span><span class="sxs-lookup"><span data-stu-id="fcea6-119">You can select any region other than hello region hosting hello primary database, but we recommend hello [paired region](../best-practices-availability-paired-regions.md).</span></span>
   
    ![Konfigurowanie replikacji geograficznej](./media/sql-database-geo-replication-portal/configure-geo-replication.png)
3. <span data-ttu-id="fcea6-121">Wybierz lub skonfiguruj serwer hello i warstwę cenową dla hello pomocniczej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="fcea6-121">Select or configure hello server and pricing tier for hello secondary database.</span></span>
   
    ![Konfigurowanie dodatkowej](./media/sql-database-geo-replication-portal/create-secondary.png)
4. <span data-ttu-id="fcea6-123">Opcjonalnie można dodać puli elastycznej tooan dodatkowej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="fcea6-123">Optionally, you can add a secondary database tooan elastic pool.</span></span> <span data-ttu-id="fcea6-124">toocreate hello dodatkowej bazy danych w puli, kliknij przycisk **puli elastycznej** i wybierz pulę na powitania serwera docelowego.</span><span class="sxs-lookup"><span data-stu-id="fcea6-124">toocreate hello secondary database in a pool, click **elastic pool** and select a pool on hello target server.</span></span> <span data-ttu-id="fcea6-125">Pula musi już istnieć na serwerze docelowym hello.</span><span class="sxs-lookup"><span data-stu-id="fcea6-125">A pool must already exist on hello target server.</span></span> <span data-ttu-id="fcea6-126">Ten przepływ pracy nie powoduje utworzenia puli.</span><span class="sxs-lookup"><span data-stu-id="fcea6-126">This workflow does not create a pool.</span></span>
5. <span data-ttu-id="fcea6-127">Kliknij przycisk **Utwórz** tooadd hello dodatkowej.</span><span class="sxs-lookup"><span data-stu-id="fcea6-127">Click **Create** tooadd hello secondary.</span></span>
6. <span data-ttu-id="fcea6-128">Witaj dodatkowej baza danych została utworzona i rozpocznie się hello wstępne wypełnianie procesu.</span><span class="sxs-lookup"><span data-stu-id="fcea6-128">hello secondary database is created and hello seeding process begins.</span></span>
   
    ![Konfigurowanie dodatkowej](./media/sql-database-geo-replication-portal/seeding0.png)
7. <span data-ttu-id="fcea6-130">Po zakończeniu hello wstępne wypełnianie procesu hello dodatkowej bazy danych wyświetla jego stan.</span><span class="sxs-lookup"><span data-stu-id="fcea6-130">When hello seeding process is complete, hello secondary database displays its status.</span></span>
   
    ![Wstępne wypełnianie ukończone](./media/sql-database-geo-replication-portal/seeding-complete.png)

## <a name="initiate-a-failover"></a><span data-ttu-id="fcea6-132">Zainicjuj tryb failover</span><span class="sxs-lookup"><span data-stu-id="fcea6-132">Initiate a failover</span></span>

<span data-ttu-id="fcea6-133">Hello dodatkowej bazy danych mogą być wyłączone toobecome hello podstawowego.</span><span class="sxs-lookup"><span data-stu-id="fcea6-133">hello secondary database can be switched toobecome hello primary.</span></span>  

1. <span data-ttu-id="fcea6-134">W hello [portalu Azure](http://portal.azure.com), Przeglądaj toohello podstawowej bazy danych w partnerstwie — replikacja geograficzna hello.</span><span class="sxs-lookup"><span data-stu-id="fcea6-134">In hello [Azure portal](http://portal.azure.com), browse toohello primary database in hello geo-replication partnership.</span></span>
2. <span data-ttu-id="fcea6-135">W bloku bazy danych SQL hello, wybierz **wszystkie ustawienia** > **— replikacja geograficzna**.</span><span class="sxs-lookup"><span data-stu-id="fcea6-135">On hello SQL Database blade, select **All settings** > **geo-replication**.</span></span>
3. <span data-ttu-id="fcea6-136">W hello **pomocniczych** listy, wybierz opcję hello bazy danych ma toobecome hello nową podstawową, a następnie kliknij przycisk **pracy awaryjnej**.</span><span class="sxs-lookup"><span data-stu-id="fcea6-136">In hello **SECONDARIES** list, select hello database you want toobecome hello new primary and click **Failover**.</span></span>
   
    ![tryb failover](./media/sql-database-geo-replication-failover-portal/secondaries.png)
4. <span data-ttu-id="fcea6-138">Kliknij przycisk **tak** toobegin hello w tryb failover.</span><span class="sxs-lookup"><span data-stu-id="fcea6-138">Click **Yes** toobegin hello failover.</span></span>

<span data-ttu-id="fcea6-139">polecenie Hello natychmiast przełącza hello dodatkowej bazy danych do roli podstawowego hello.</span><span class="sxs-lookup"><span data-stu-id="fcea6-139">hello command immediately switches hello secondary database into hello primary role.</span></span> 

<span data-ttu-id="fcea6-140">Istnieje krótki okres, podczas którego obie bazy danych są niedostępne (w kolejności hello 0 sekund too25) podczas przełączania hello ról.</span><span class="sxs-lookup"><span data-stu-id="fcea6-140">There is a short period during which both databases are unavailable (on hello order of 0 too25 seconds) while hello roles are switched.</span></span> <span data-ttu-id="fcea6-141">Jeśli hello podstawowej bazy danych ma wiele baz danych w dodatkowej, polecenie hello automatycznie Rekonfiguruj hello innych pomocniczych tooconnect toohello nową podstawową.</span><span class="sxs-lookup"><span data-stu-id="fcea6-141">If hello primary database has multiple secondary databases, hello command automatically reconfigures hello other secondaries tooconnect toohello new primary.</span></span> <span data-ttu-id="fcea6-142">cała operacja Hello powinno zająć mniej niż minutę toocomplete w normalnych okolicznościach.</span><span class="sxs-lookup"><span data-stu-id="fcea6-142">hello entire operation should take less than a minute toocomplete under normal circumstances.</span></span> 

> [!NOTE]
> <span data-ttu-id="fcea6-143">To polecenie jest przeznaczona dla Szybkie odzyskiwanie bazy danych hello w razie awarii.</span><span class="sxs-lookup"><span data-stu-id="fcea6-143">This command is designed for quick recovery of hello database in case of an outage.</span></span> <span data-ttu-id="fcea6-144">Wyzwala trybu failover bez synchronizacji danych (wymuszone trybu failover).</span><span class="sxs-lookup"><span data-stu-id="fcea6-144">It triggers failover without data synchronization (forced failover).</span></span>  <span data-ttu-id="fcea6-145">Jeśli podstawowy hello jest w trybie online i zatwierdzania transakcji po wydaniu polecenia hello utratę danych mogą wystąpić.</span><span class="sxs-lookup"><span data-stu-id="fcea6-145">If hello primary is online and committing transactions when hello command is issued some data loss may occur.</span></span> 
> 
> 

## <a name="remove-secondary-database"></a><span data-ttu-id="fcea6-146">Usuń z dodatkowej bazy danych</span><span class="sxs-lookup"><span data-stu-id="fcea6-146">Remove secondary database</span></span>
<span data-ttu-id="fcea6-147">Ta operacja kończy trwale hello replikacji toohello dodatkowej bazy danych, i zmiany hello roli hello dodatkowej tooa zwykłej bazy danych do odczytu / zapisu.</span><span class="sxs-lookup"><span data-stu-id="fcea6-147">This operation permanently terminates hello replication toohello secondary database, and changes hello role of hello secondary tooa regular read-write database.</span></span> <span data-ttu-id="fcea6-148">Jeśli hello łączności toohello dodatkowej bazy danych jest uszkodzona, polecenie hello zakończy się pomyślnie, ale hello dodatkowej ma staje się odczytu i zapisu do po przywróceniu łączności.</span><span class="sxs-lookup"><span data-stu-id="fcea6-148">If hello connectivity toohello secondary database is broken, hello command succeeds but hello secondary does not become read-write until after connectivity is restored.</span></span>  

1. <span data-ttu-id="fcea6-149">W hello [portalu Azure](http://portal.azure.com), Przeglądaj toohello podstawowej bazy danych w partnerstwie — replikacja geograficzna hello.</span><span class="sxs-lookup"><span data-stu-id="fcea6-149">In hello [Azure portal](http://portal.azure.com), browse toohello primary database in hello geo-replication partnership.</span></span>
2. <span data-ttu-id="fcea6-150">Na stronie bazy danych SQL hello zaznacz **— replikacja geograficzna**.</span><span class="sxs-lookup"><span data-stu-id="fcea6-150">On hello SQL database page, select **geo-replication**.</span></span>
3. <span data-ttu-id="fcea6-151">W hello **pomocniczych** listy, wybierz hello bazy danych ma tooremove z hello — replikacja geograficzna powiązania.</span><span class="sxs-lookup"><span data-stu-id="fcea6-151">In hello **SECONDARIES** list, select hello database you want tooremove from hello geo-replication partnership.</span></span>
4. <span data-ttu-id="fcea6-152">Kliknij przycisk **Zatrzymaj replikację,**.</span><span class="sxs-lookup"><span data-stu-id="fcea6-152">Click **Stop Replication**.</span></span>
   
    ![Usuń pomocniczej](./media/sql-database-geo-replication-portal/remove-secondary.png)
5. <span data-ttu-id="fcea6-154">Zostanie wyświetlone okno potwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="fcea6-154">A confirmation window opens.</span></span> <span data-ttu-id="fcea6-155">Kliknij przycisk **tak** tooremove hello z bazy danych z hello — replikacja geograficzna powiązania.</span><span class="sxs-lookup"><span data-stu-id="fcea6-155">Click **Yes** tooremove hello database from hello geo-replication partnership.</span></span> <span data-ttu-id="fcea6-156">(Ustaw tooa Odczyt i zapis z bazy danych nie jest częścią replikacji.)</span><span class="sxs-lookup"><span data-stu-id="fcea6-156">(Set it tooa read-write database not part of any replication.)</span></span>

## <a name="next-steps"></a><span data-ttu-id="fcea6-157">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="fcea6-157">Next steps</span></span>
* <span data-ttu-id="fcea6-158">toolearn więcej informacji na temat aktywna replikacja geograficzna, zobacz [aktywna replikacja geograficzna](sql-database-geo-replication-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fcea6-158">toolearn more about active geo-replication, see [active geo-replication](sql-database-geo-replication-overview.md).</span></span>
* <span data-ttu-id="fcea6-159">Omówienie ciągłości działalności biznesowej i scenariuszy, zobacz [omówienie ciągłości działalności biznesowej](sql-database-business-continuity.md).</span><span class="sxs-lookup"><span data-stu-id="fcea6-159">For a business continuity overview and scenarios, see [Business continuity overview](sql-database-business-continuity.md).</span></span>

