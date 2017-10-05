---
title: Testowanie odzyskiwania po awarii bazy danych SQL | Dokumentacja firmy Microsoft
description: "Dowiedz się, wskazówki i najlepsze rozwiązania dotyczące korzystania z bazy danych SQL Azure przeprowadzić testowanie odzyskiwania po awarii, aby chronić Twoje misji krytycznych aplikacji LOB odporność na awarie i awarie."
services: sql-database
documentationcenter: 
author: anosov1960
manager: jhubbard
editor: monicar
ms.assetid: b44a269c-fe2a-404f-b013-290030860bd1
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 07/31/2016
ms.author: sashan
ms.openlocfilehash: 1b1d65a41a794a566287dcffe3581ac58e2a965f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="performing-disaster-recovery-drill"></a><span data-ttu-id="af99e-103">Wykonywanie wyszczególniania odzyskiwania po awarii</span><span class="sxs-lookup"><span data-stu-id="af99e-103">Performing Disaster Recovery Drill</span></span>
<span data-ttu-id="af99e-104">Zalecane jest okresowo wykonywać weryfikacji aplikacja jest gotowa do przepływu pracy odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="af99e-104">It is recommended that validation of application readiness for recovery workflow is performed periodically.</span></span> <span data-ttu-id="af99e-105">Weryfikowanie zachowanie aplikacji oraz wpływ utraty danych i/lub przerw w działaniu obejmuje czy tryb failover jest dobrym rozwiązaniem engineering.</span><span class="sxs-lookup"><span data-stu-id="af99e-105">Verifying the application behavior and implications of data loss and/or the disruption that failover involves is a good engineering practice.</span></span> <span data-ttu-id="af99e-106">Również jest wymagane przez większość standardy branżowe w ramach certyfikacji ciągłości biznesowej.</span><span class="sxs-lookup"><span data-stu-id="af99e-106">It is also a requirement by most industry standards as part of business continuity certification.</span></span>

<span data-ttu-id="af99e-107">Obejmuje wykonywania wyszczególniania odzyskiwania po awarii:</span><span class="sxs-lookup"><span data-stu-id="af99e-107">Performing a disaster recovery drill consists of:</span></span>

* <span data-ttu-id="af99e-108">Symulowanie symulacje awarii warstwy danych</span><span class="sxs-lookup"><span data-stu-id="af99e-108">Simulating data tier outage</span></span>
* <span data-ttu-id="af99e-109">Odzyskiwanie</span><span class="sxs-lookup"><span data-stu-id="af99e-109">Recovering</span></span>
* <span data-ttu-id="af99e-110">Sprawdź poprawność odzyskiwania post integralności aplikacji</span><span class="sxs-lookup"><span data-stu-id="af99e-110">Validate application integrity post recovery</span></span>

<span data-ttu-id="af99e-111">W zależności od tego, jak możesz [przeznaczony dla ciągłość prowadzenia działalności biznesowej aplikacji](sql-database-business-continuity.md), przepływu pracy można wykonać drążenie może się różnić.</span><span class="sxs-lookup"><span data-stu-id="af99e-111">Depending on how you [designed your application for business continuity](sql-database-business-continuity.md), the workflow to execute the drill can vary.</span></span> <span data-ttu-id="af99e-112">Poniżej opisano najważniejsze wskazówki przeprowadzenie wyszczególniania odzyskiwania po awarii, w kontekście bazy danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="af99e-112">Below we describe the best practices conducting a disaster recovery drill in the context of Azure SQL Database.</span></span>

## <a name="geo-restore"></a><span data-ttu-id="af99e-113">Przywracanie geograficzne</span><span class="sxs-lookup"><span data-stu-id="af99e-113">Geo-restore</span></span>
<span data-ttu-id="af99e-114">Aby zapobiec utracie danych podczas przeprowadzania wyszczególniania odzyskiwania po awarii, zaleca się przeprowadzania Przechodzenie do szczegółów, tworząc kopię w środowisku produkcyjnym i użycie go do sprawdzenia przepływu pracy awaryjnej aplikacji przy użyciu środowiska testowego.</span><span class="sxs-lookup"><span data-stu-id="af99e-114">To prevent the potential data loss when conducting a disaster recovery drill, we recommend performing the drill using a test environment by creating a copy of the production environment and using it to verify the application’s failover workflow.</span></span>

#### <a name="outage-simulation"></a><span data-ttu-id="af99e-115">Symulacji awarii</span><span class="sxs-lookup"><span data-stu-id="af99e-115">Outage simulation</span></span>
<span data-ttu-id="af99e-116">Aby symulować awarii, można usunąć lub zmienić nazwy źródłowej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="af99e-116">To simulate the outage, you can delete or rename the source database.</span></span> <span data-ttu-id="af99e-117">Powoduje to błędów łączności aplikacji.</span><span class="sxs-lookup"><span data-stu-id="af99e-117">This causes application connectivity failures.</span></span>

#### <a name="recovery"></a><span data-ttu-id="af99e-118">Odzyskiwanie</span><span class="sxs-lookup"><span data-stu-id="af99e-118">Recovery</span></span>
* <span data-ttu-id="af99e-119">Wykonać geograficznie przywracania bazy danych na innym serwerze, zgodnie z opisem [tutaj](sql-database-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="af99e-119">Perform the geo-restore of the database into a different server as described [here](sql-database-disaster-recovery.md).</span></span>
* <span data-ttu-id="af99e-120">Zmień konfigurację aplikacji, aby nawiązać połączenie odzyskanej bazy danych i postępuj zgodnie z [skonfigurować bazę danych po odzyskaniu](sql-database-disaster-recovery.md) przewodniku, aby zakończyć odzyskiwanie.</span><span class="sxs-lookup"><span data-stu-id="af99e-120">Change the application configuration to connect to the recovered database and follow the [Configure a database after recovery](sql-database-disaster-recovery.md) guide to complete the recovery.</span></span>

#### <a name="validation"></a><span data-ttu-id="af99e-121">Walidacja</span><span class="sxs-lookup"><span data-stu-id="af99e-121">Validation</span></span>
* <span data-ttu-id="af99e-122">Zakończ Drąż weryfikowanie odzyskiwania post integralności aplikacji (w tym parametry połączenia, logowania, podstawowych funkcji testowania lub innych operacji sprawdzania poprawności część procedur signoffs standardowej aplikacji).</span><span class="sxs-lookup"><span data-stu-id="af99e-122">Complete the drill by verifying the application integrity post recovery (including connection strings, logins, basic functionality testing or other validations part of standard application signoffs procedures).</span></span>

## <a name="geo-replication"></a><span data-ttu-id="af99e-123">Replikacja geograficzna</span><span class="sxs-lookup"><span data-stu-id="af99e-123">Geo-replication</span></span>
<span data-ttu-id="af99e-124">Dla bazy danych, który jest chroniony za pomocą — replikacja geograficzna wykonywania Przechodzenie do szczegółów obejmuje planowany tryb failover na dodatkowej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="af99e-124">For a database that is protected using geo-replication the drill exercise involves planned failover to the secondary database.</span></span> <span data-ttu-id="af99e-125">Planowany tryb failover zapewnia, że podstawowej i pomocniczej bazy danych pozostają zsynchronizowane podczas przełączania ról.</span><span class="sxs-lookup"><span data-stu-id="af99e-125">The planned failover ensures that the primary and the secondary databases remain in sync when the roles are switched.</span></span> <span data-ttu-id="af99e-126">Inaczej niż w przypadku nieplanowanego trybu failover ta operacja nie powoduje utraty danych, więc Drąż mogą być wykonywane w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="af99e-126">Unlike the unplanned failover, this operation does not result in data loss, so the drill can be performed in the production environment.</span></span>

#### <a name="outage-simulation"></a><span data-ttu-id="af99e-127">Symulacji awarii</span><span class="sxs-lookup"><span data-stu-id="af99e-127">Outage simulation</span></span>
<span data-ttu-id="af99e-128">Aby symulować awarii, można wyłączyć maszyny wirtualnej, połączony z bazą danych lub aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="af99e-128">To simulate the outage, you can disable the web application or virtual machine connected to the database.</span></span> <span data-ttu-id="af99e-129">W efekcie awarie połączenia dla klientów sieci web.</span><span class="sxs-lookup"><span data-stu-id="af99e-129">This results in the connectivity failures for the web clients.</span></span>

#### <a name="recovery"></a><span data-ttu-id="af99e-130">Odzyskiwanie</span><span class="sxs-lookup"><span data-stu-id="af99e-130">Recovery</span></span>
* <span data-ttu-id="af99e-131">Upewnij się, Konfiguracja aplikacji w regionie DR wskazuje była dodatkowej, która staje się dostępny w pełni nową podstawową.</span><span class="sxs-lookup"><span data-stu-id="af99e-131">Make sure the application configuration in the DR region points to the former secondary which becomes the fully accessible new primary.</span></span>
* <span data-ttu-id="af99e-132">Wykonaj [planowanego trybu failover](scripts/sql-database-setup-geodr-and-failover-database-powershell.md) dokonanie pomocniczej bazie danych nowego podstawowego</span><span class="sxs-lookup"><span data-stu-id="af99e-132">Perform [planned failover](scripts/sql-database-setup-geodr-and-failover-database-powershell.md) to make the secondary database a new primary</span></span>
* <span data-ttu-id="af99e-133">Postępuj zgodnie z [skonfigurować bazę danych po odzyskaniu](sql-database-disaster-recovery.md) przewodniku, aby zakończyć odzyskiwanie.</span><span class="sxs-lookup"><span data-stu-id="af99e-133">Follow the [Configure a database after recovery](sql-database-disaster-recovery.md) guide to complete the recovery.</span></span>

#### <a name="validation"></a><span data-ttu-id="af99e-134">Walidacja</span><span class="sxs-lookup"><span data-stu-id="af99e-134">Validation</span></span>
* <span data-ttu-id="af99e-135">Zakończ Drąż weryfikowanie odzyskiwania post integralności aplikacji (w tym parametry połączenia, logowania, podstawowych funkcji testowania lub innych operacji sprawdzania poprawności część procedur signoffs standardowej aplikacji).</span><span class="sxs-lookup"><span data-stu-id="af99e-135">Complete the drill by verifying the application integrity post recovery (including connection strings, logins, basic functionality testing or other validations part of standard application signoffs procedures).</span></span>

## <a name="next-steps"></a><span data-ttu-id="af99e-136">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="af99e-136">Next steps</span></span>
* <span data-ttu-id="af99e-137">Aby dowiedzieć się więcej o scenariuszach ciągłości biznesowej, zobacz [ciągłości scenariuszy](sql-database-business-continuity.md)</span><span class="sxs-lookup"><span data-stu-id="af99e-137">To learn about business continuity scenarios, see [Continuity scenarios](sql-database-business-continuity.md)</span></span>
* <span data-ttu-id="af99e-138">Aby dowiedzieć się więcej na temat usługi Azure SQL bazy danych automatycznego tworzenia kopii zapasowych, zobacz [bazy danych SQL automatycznego tworzenia kopii zapasowych](sql-database-automated-backups.md)</span><span class="sxs-lookup"><span data-stu-id="af99e-138">To learn about Azure SQL Database automated backups, see [SQL Database automated backups](sql-database-automated-backups.md)</span></span>
* <span data-ttu-id="af99e-139">Aby dowiedzieć się więcej o używaniu kopie zapasowe automatycznego odzyskiwania, zobacz [przywrócić bazę danych z kopii zapasowych inicjowane przez usługę](sql-database-recovery-using-backups.md)</span><span class="sxs-lookup"><span data-stu-id="af99e-139">To learn about using automated backups for recovery, see [restore a database from the service-initiated backups](sql-database-recovery-using-backups.md)</span></span>
* <span data-ttu-id="af99e-140">Informacje na temat opcji odzyskiwania szybsze, zobacz [aktywna replikacja geograficzna](sql-database-geo-replication-overview.md)</span><span class="sxs-lookup"><span data-stu-id="af99e-140">To learn about faster recovery options, see [active geo-replication](sql-database-geo-replication-overview.md)</span></span>  
