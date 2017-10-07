---
title: aaaSQL testowanie odzyskiwania po awarii bazy danych | Dokumentacja firmy Microsoft
description: "Uczyć się wskazówki i najlepsze rozwiązania dotyczące korzystania z bazy danych SQL Azure tooperform awaryjnego odzyskiwania ćwiczenia toohelp Zachowaj toofailures odporność aplikacji krytycznym znaczeniu dla firmy misji i awarie."
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
ms.openlocfilehash: bf17857a19fdebddf0d4f55e4db3a1b33efb4e8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="performing-disaster-recovery-drill"></a><span data-ttu-id="c55de-103">Wykonywanie wyszczególniania odzyskiwania po awarii</span><span class="sxs-lookup"><span data-stu-id="c55de-103">Performing Disaster Recovery Drill</span></span>
<span data-ttu-id="c55de-104">Zalecane jest okresowo wykonywać weryfikacji aplikacja jest gotowa do przepływu pracy odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="c55de-104">It is recommended that validation of application readiness for recovery workflow is performed periodically.</span></span> <span data-ttu-id="c55de-105">Weryfikowanie, czy zachowanie aplikacji hello i zagadnień dotyczących danych utraty i/lub hello przerw w działaniu obejmuje czy tryb failover jest dobrym rozwiązaniem engineering.</span><span class="sxs-lookup"><span data-stu-id="c55de-105">Verifying hello application behavior and implications of data loss and/or hello disruption that failover involves is a good engineering practice.</span></span> <span data-ttu-id="c55de-106">Również jest wymagane przez większość standardy branżowe w ramach certyfikacji ciągłości biznesowej.</span><span class="sxs-lookup"><span data-stu-id="c55de-106">It is also a requirement by most industry standards as part of business continuity certification.</span></span>

<span data-ttu-id="c55de-107">Obejmuje wykonywania wyszczególniania odzyskiwania po awarii:</span><span class="sxs-lookup"><span data-stu-id="c55de-107">Performing a disaster recovery drill consists of:</span></span>

* <span data-ttu-id="c55de-108">Symulowanie symulacje awarii warstwy danych</span><span class="sxs-lookup"><span data-stu-id="c55de-108">Simulating data tier outage</span></span>
* <span data-ttu-id="c55de-109">Odzyskiwanie</span><span class="sxs-lookup"><span data-stu-id="c55de-109">Recovering</span></span>
* <span data-ttu-id="c55de-110">Sprawdź poprawność odzyskiwania post integralności aplikacji</span><span class="sxs-lookup"><span data-stu-id="c55de-110">Validate application integrity post recovery</span></span>

<span data-ttu-id="c55de-111">W zależności od tego, jak możesz [przeznaczony dla ciągłość prowadzenia działalności biznesowej aplikacji](sql-database-business-continuity.md), hello przepływu pracy tooexecute hello Przechodzenie do szczegółów mogą się różnić.</span><span class="sxs-lookup"><span data-stu-id="c55de-111">Depending on how you [designed your application for business continuity](sql-database-business-continuity.md), hello workflow tooexecute hello drill can vary.</span></span> <span data-ttu-id="c55de-112">Poniżej opisano najważniejsze wskazówki hello przeprowadzenie wyszczególniania odzyskiwania po awarii, w kontekście hello bazy danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="c55de-112">Below we describe hello best practices conducting a disaster recovery drill in hello context of Azure SQL Database.</span></span>

## <a name="geo-restore"></a><span data-ttu-id="c55de-113">Przywracanie geograficzne</span><span class="sxs-lookup"><span data-stu-id="c55de-113">Geo-restore</span></span>
<span data-ttu-id="c55de-114">tooprevent hello utracie danych podczas przeprowadzania wyszczególniania odzyskiwania po awarii, zaleca się przeprowadzania hello Przechodzenie do szczegółów, tworząc kopię hello środowiska produkcyjnego i używa go przy użyciu środowiska testowego aplikacji hello tooverify przepływu pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="c55de-114">tooprevent hello potential data loss when conducting a disaster recovery drill, we recommend performing hello drill using a test environment by creating a copy of hello production environment and using it tooverify hello application’s failover workflow.</span></span>

#### <a name="outage-simulation"></a><span data-ttu-id="c55de-115">Symulacji awarii</span><span class="sxs-lookup"><span data-stu-id="c55de-115">Outage simulation</span></span>
<span data-ttu-id="c55de-116">toosimulate hello awarii, można usunąć ani zmienić nazwy hello źródłowej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="c55de-116">toosimulate hello outage, you can delete or rename hello source database.</span></span> <span data-ttu-id="c55de-117">Powoduje to błędów łączności aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c55de-117">This causes application connectivity failures.</span></span>

#### <a name="recovery"></a><span data-ttu-id="c55de-118">Odzyskiwanie</span><span class="sxs-lookup"><span data-stu-id="c55de-118">Recovery</span></span>
* <span data-ttu-id="c55de-119">Wykonać przywracaniem geograficznym hello hello bazy danych na innym serwerze, zgodnie z opisem [tutaj](sql-database-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="c55de-119">Perform hello geo-restore of hello database into a different server as described [here](sql-database-disaster-recovery.md).</span></span>
* <span data-ttu-id="c55de-120">Zmień hello aplikacji konfiguracji tooconnect toohello odzyskanej bazy danych i wykonaj hello [skonfigurować bazę danych po odzyskaniu](sql-database-disaster-recovery.md) przewodnik toocomplete hello odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="c55de-120">Change hello application configuration tooconnect toohello recovered database and follow hello [Configure a database after recovery](sql-database-disaster-recovery.md) guide toocomplete hello recovery.</span></span>

#### <a name="validation"></a><span data-ttu-id="c55de-121">Walidacja</span><span class="sxs-lookup"><span data-stu-id="c55de-121">Validation</span></span>
* <span data-ttu-id="c55de-122">Zakończenie hello Przechodzenie do szczegółów weryfikując aplikacji hello integralności post odzyskiwania (w tym parametry połączenia, logowania, podstawowych funkcji testowania lub innych operacji sprawdzania poprawności część procedur signoffs standardowej aplikacji).</span><span class="sxs-lookup"><span data-stu-id="c55de-122">Complete hello drill by verifying hello application integrity post recovery (including connection strings, logins, basic functionality testing or other validations part of standard application signoffs procedures).</span></span>

## <a name="geo-replication"></a><span data-ttu-id="c55de-123">Replikacja geograficzna</span><span class="sxs-lookup"><span data-stu-id="c55de-123">Geo-replication</span></span>
<span data-ttu-id="c55de-124">Dla bazy danych, która jest chroniony za pomocą Przechodzenie do szczegółów — replikacja geograficzna hello wykonywania obejmuje planowany tryb failover toohello dodatkowej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="c55de-124">For a database that is protected using geo-replication hello drill exercise involves planned failover toohello secondary database.</span></span> <span data-ttu-id="c55de-125">Hello planowany tryb failover zapewnia, że hello głównej i pomocniczej bazy danych hello pozostają zsynchronizowane podczas przełączania ról hello.</span><span class="sxs-lookup"><span data-stu-id="c55de-125">hello planned failover ensures that hello primary and hello secondary databases remain in sync when hello roles are switched.</span></span> <span data-ttu-id="c55de-126">W odróżnieniu od hello nieplanowanego trybu failover, ta operacja nie powoduje utraty danych, więc hello Przechodzenie do szczegółów mogą być wykonywane w środowisku produkcyjnym hello.</span><span class="sxs-lookup"><span data-stu-id="c55de-126">Unlike hello unplanned failover, this operation does not result in data loss, so hello drill can be performed in hello production environment.</span></span>

#### <a name="outage-simulation"></a><span data-ttu-id="c55de-127">Symulacji awarii</span><span class="sxs-lookup"><span data-stu-id="c55de-127">Outage simulation</span></span>
<span data-ttu-id="c55de-128">toosimulate hello awarii, można wyłączyć aplikacji sieci web hello lub maszyny wirtualnej podłączone toohello w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="c55de-128">toosimulate hello outage, you can disable hello web application or virtual machine connected toohello database.</span></span> <span data-ttu-id="c55de-129">W efekcie hello połączeniami dla klientów sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="c55de-129">This results in hello connectivity failures for hello web clients.</span></span>

#### <a name="recovery"></a><span data-ttu-id="c55de-130">Odzyskiwanie</span><span class="sxs-lookup"><span data-stu-id="c55de-130">Recovery</span></span>
* <span data-ttu-id="c55de-131">Upewnij się, że konfiguracja aplikacji hello w hello DR region punktów toohello była dodatkowej która staje się hello pełni dostępny nową podstawową.</span><span class="sxs-lookup"><span data-stu-id="c55de-131">Make sure hello application configuration in hello DR region points toohello former secondary which becomes hello fully accessible new primary.</span></span>
* <span data-ttu-id="c55de-132">Wykonaj [planowanego trybu failover](scripts/sql-database-setup-geodr-and-failover-database-powershell.md) toomake hello pomocniczej bazy danych nowego podstawowego</span><span class="sxs-lookup"><span data-stu-id="c55de-132">Perform [planned failover](scripts/sql-database-setup-geodr-and-failover-database-powershell.md) toomake hello secondary database a new primary</span></span>
* <span data-ttu-id="c55de-133">Wykonaj hello [skonfigurować bazę danych po odzyskaniu](sql-database-disaster-recovery.md) przewodnik toocomplete hello odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="c55de-133">Follow hello [Configure a database after recovery](sql-database-disaster-recovery.md) guide toocomplete hello recovery.</span></span>

#### <a name="validation"></a><span data-ttu-id="c55de-134">Walidacja</span><span class="sxs-lookup"><span data-stu-id="c55de-134">Validation</span></span>
* <span data-ttu-id="c55de-135">Zakończenie hello Przechodzenie do szczegółów weryfikując aplikacji hello integralności post odzyskiwania (w tym parametry połączenia, logowania, podstawowych funkcji testowania lub innych operacji sprawdzania poprawności część procedur signoffs standardowej aplikacji).</span><span class="sxs-lookup"><span data-stu-id="c55de-135">Complete hello drill by verifying hello application integrity post recovery (including connection strings, logins, basic functionality testing or other validations part of standard application signoffs procedures).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c55de-136">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c55de-136">Next steps</span></span>
* <span data-ttu-id="c55de-137">toolearn o scenariuszach ciągłości biznesowej, zobacz [ciągłości scenariuszy](sql-database-business-continuity.md)</span><span class="sxs-lookup"><span data-stu-id="c55de-137">toolearn about business continuity scenarios, see [Continuity scenarios](sql-database-business-continuity.md)</span></span>
* <span data-ttu-id="c55de-138">toolearn o bazy danych SQL Azure automatycznego tworzenia kopii zapasowych, zobacz [bazy danych SQL automatycznego tworzenia kopii zapasowych](sql-database-automated-backups.md)</span><span class="sxs-lookup"><span data-stu-id="c55de-138">toolearn about Azure SQL Database automated backups, see [SQL Database automated backups](sql-database-automated-backups.md)</span></span>
* <span data-ttu-id="c55de-139">toolearn o za pomocą kopie zapasowe automatycznego odzyskiwania, zobacz [przywrócić bazę danych z kopii zapasowych hello inicjowane przez usługę](sql-database-recovery-using-backups.md)</span><span class="sxs-lookup"><span data-stu-id="c55de-139">toolearn about using automated backups for recovery, see [restore a database from hello service-initiated backups](sql-database-recovery-using-backups.md)</span></span>
* <span data-ttu-id="c55de-140">toolearn o szybsze opcje odzyskiwania, zobacz [aktywna replikacja geograficzna](sql-database-geo-replication-overview.md)</span><span class="sxs-lookup"><span data-stu-id="c55de-140">toolearn about faster recovery options, see [active geo-replication](sql-database-geo-replication-overview.md)</span></span>  
