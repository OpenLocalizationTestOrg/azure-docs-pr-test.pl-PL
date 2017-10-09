---
title: "aaaMigrate magazynu toopremium magazynu istniejących danych Azure | Dokumentacja firmy Microsoft"
description: "Instrukcje dotyczące migracji istniejącego magazynu toopremium magazynu danych"
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: barbkess
editor: 
ms.assetid: 04b05dea-c066-44a0-9751-0774eb84c689
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 11/29/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: 145199c2da1f6f1fb8898626cd04886c42d82204
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-data-warehouse-toopremium-storage"></a><span data-ttu-id="8ee82-103">Migracja magazynu toopremium magazynu danych</span><span class="sxs-lookup"><span data-stu-id="8ee82-103">Migrate your data warehouse toopremium storage</span></span>
<span data-ttu-id="8ee82-104">Usługa Azure SQL Data Warehouse niedawno wprowadzone [magazyn w warstwie premium dla większej wydajności przewidywalności][premium storage for greater performance predictability].</span><span class="sxs-lookup"><span data-stu-id="8ee82-104">Azure SQL Data Warehouse recently introduced [premium storage for greater performance predictability][premium storage for greater performance predictability].</span></span> <span data-ttu-id="8ee82-105">Istniejące dane, które można teraz magazynów obecnie magazynu w warstwie standardowa migracji toopremium magazynu.</span><span class="sxs-lookup"><span data-stu-id="8ee82-105">Existing data warehouses currently on standard storage can now be migrated toopremium storage.</span></span> <span data-ttu-id="8ee82-106">Możesz korzystać z automatycznych migracji, lub jeśli wolisz toocontrol podczas toomigrate (które obejmują przestój), możesz zrobić samodzielnie hello migracji.</span><span class="sxs-lookup"><span data-stu-id="8ee82-106">You can take advantage of automatic migration, or if you prefer toocontrol when toomigrate (which does involve some downtime), you can do hello migration yourself.</span></span>

<span data-ttu-id="8ee82-107">Jeśli masz więcej niż jeden magazyn danych, użyj hello [harmonogramu automatycznej migracji] [ automatic migration schedule] toodetermine podczas również zostaną poddane migracji.</span><span class="sxs-lookup"><span data-stu-id="8ee82-107">If you have more than one data warehouse, use hello [automatic migration schedule][automatic migration schedule] toodetermine when it will also be migrated.</span></span>

## <a name="determine-storage-type"></a><span data-ttu-id="8ee82-108">Określanie typu magazynu</span><span class="sxs-lookup"><span data-stu-id="8ee82-108">Determine storage type</span></span>
<span data-ttu-id="8ee82-109">Jeśli utworzono hurtowni danych przed powitania po daty są aktualnie używa magazynu w warstwie standardowa.</span><span class="sxs-lookup"><span data-stu-id="8ee82-109">If you created a data warehouse before hello following dates, you are currently using standard storage.</span></span>

| <span data-ttu-id="8ee82-110">**Region**</span><span class="sxs-lookup"><span data-stu-id="8ee82-110">**Region**</span></span> | <span data-ttu-id="8ee82-111">**Utworzone przed tą datą magazynu danych**</span><span class="sxs-lookup"><span data-stu-id="8ee82-111">**Data warehouse created before this date**</span></span> |
|:--- |:--- |
| <span data-ttu-id="8ee82-112">Australia Wschodnia</span><span class="sxs-lookup"><span data-stu-id="8ee82-112">Australia East</span></span> |<span data-ttu-id="8ee82-113">Magazyn w warstwie Premium nie są jeszcze dostępne</span><span class="sxs-lookup"><span data-stu-id="8ee82-113">Premium storage not yet available</span></span> |
| <span data-ttu-id="8ee82-114">Chiny Wschodnie</span><span class="sxs-lookup"><span data-stu-id="8ee82-114">China East</span></span> |<span data-ttu-id="8ee82-115">1 listopada 2016 r.</span><span class="sxs-lookup"><span data-stu-id="8ee82-115">November 1, 2016</span></span> |
| <span data-ttu-id="8ee82-116">Chiny Północne</span><span class="sxs-lookup"><span data-stu-id="8ee82-116">China North</span></span> |<span data-ttu-id="8ee82-117">1 listopada 2016 r.</span><span class="sxs-lookup"><span data-stu-id="8ee82-117">November 1, 2016</span></span> |
| <span data-ttu-id="8ee82-118">Niemcy Środkowe</span><span class="sxs-lookup"><span data-stu-id="8ee82-118">Germany Central</span></span> |<span data-ttu-id="8ee82-119">1 listopada 2016 r.</span><span class="sxs-lookup"><span data-stu-id="8ee82-119">November 1, 2016</span></span> |
| <span data-ttu-id="8ee82-120">Niemcy Północno-Wschodnie</span><span class="sxs-lookup"><span data-stu-id="8ee82-120">Germany Northeast</span></span> |<span data-ttu-id="8ee82-121">1 listopada 2016 r.</span><span class="sxs-lookup"><span data-stu-id="8ee82-121">November 1, 2016</span></span> |
| <span data-ttu-id="8ee82-122">Indie Zachodnie</span><span class="sxs-lookup"><span data-stu-id="8ee82-122">India West</span></span> |<span data-ttu-id="8ee82-123">Magazyn w warstwie Premium nie są jeszcze dostępne</span><span class="sxs-lookup"><span data-stu-id="8ee82-123">Premium storage not yet available</span></span> |
| <span data-ttu-id="8ee82-124">Japonia Zachodnia</span><span class="sxs-lookup"><span data-stu-id="8ee82-124">Japan West</span></span> |<span data-ttu-id="8ee82-125">Magazyn w warstwie Premium nie są jeszcze dostępne</span><span class="sxs-lookup"><span data-stu-id="8ee82-125">Premium storage not yet available</span></span> |
| <span data-ttu-id="8ee82-126">Środkowo-północne stany USA</span><span class="sxs-lookup"><span data-stu-id="8ee82-126">North Central US</span></span> |<span data-ttu-id="8ee82-127">10 listopada 2016 r.</span><span class="sxs-lookup"><span data-stu-id="8ee82-127">November 10, 2016</span></span> |

## <a name="automatic-migration-details"></a><span data-ttu-id="8ee82-128">Szczegóły automatycznej migracji</span><span class="sxs-lookup"><span data-stu-id="8ee82-128">Automatic migration details</span></span>
<span data-ttu-id="8ee82-129">Domyślnie, przeprowadzimy migrację bazy danych dla Ciebie między 6:00 a 6:00:00 czasu lokalnego w Twoim regionie podczas hello [harmonogramu automatycznej migracji][automatic migration schedule].</span><span class="sxs-lookup"><span data-stu-id="8ee82-129">By default, we will migrate your database for you between 6:00 PM and 6:00 AM in your region's local time during hello [automatic migration schedule][automatic migration schedule].</span></span> <span data-ttu-id="8ee82-130">Podczas migracji hello będzie można jej używać istniejącego magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="8ee82-130">Your existing data warehouse will be unusable during hello migration.</span></span> <span data-ttu-id="8ee82-131">Witaj migracji zajmie około jednej godziny na terabajt magazynu na magazyn danych.</span><span class="sxs-lookup"><span data-stu-id="8ee82-131">hello migration will take approximately one hour per terabyte of storage per data warehouse.</span></span> <span data-ttu-id="8ee82-132">Nie zostanie obciążona podczas jakiejkolwiek jego części hello automatyczną migrację.</span><span class="sxs-lookup"><span data-stu-id="8ee82-132">You will not be charged during any portion of hello automatic migration.</span></span>

> [!NOTE]
> <span data-ttu-id="8ee82-133">Po zakończeniu migracji hello magazynu danych będzie ponownie online i można go użyć.</span><span class="sxs-lookup"><span data-stu-id="8ee82-133">When hello migration is complete, your data warehouse will be back online and usable.</span></span>
>
>

<span data-ttu-id="8ee82-134">Microsoft trwa powitania po migracji hello toocomplete czynności (te nie wymagają żadnych zaangażowania ze strony użytkownika).</span><span class="sxs-lookup"><span data-stu-id="8ee82-134">Microsoft is taking hello following steps toocomplete hello migration (these do not require any involvement on your part).</span></span> <span data-ttu-id="8ee82-135">W tym przykładzie załóżmy, że istniejącego magazynu danych na magazynu w warstwie standardowa aktualnie ma nazwę "MyDW."</span><span class="sxs-lookup"><span data-stu-id="8ee82-135">In this example, imagine that your existing data warehouse on standard storage is currently named “MyDW.”</span></span>

1. <span data-ttu-id="8ee82-136">Microsoft zmienia "MyDW" za "MyDW_DO_NOT_USE_ [sygnatury czasowej]".</span><span class="sxs-lookup"><span data-stu-id="8ee82-136">Microsoft renames “MyDW” too“MyDW_DO_NOT_USE_[Timestamp].”</span></span>
2. <span data-ttu-id="8ee82-137">Microsoft wstrzymuje "MyDW_DO_NOT_USE_ [sygnatury czasowej]".</span><span class="sxs-lookup"><span data-stu-id="8ee82-137">Microsoft pauses “MyDW_DO_NOT_USE_[Timestamp].”</span></span> <span data-ttu-id="8ee82-138">W tym czasie wykonywana jest kopia zapasowa.</span><span class="sxs-lookup"><span data-stu-id="8ee82-138">During this time, a backup is taken.</span></span> <span data-ttu-id="8ee82-139">Wiele pauzy i wznawia mogą pojawić się firma Microsoft napotkania problemów podczas tego procesu.</span><span class="sxs-lookup"><span data-stu-id="8ee82-139">You may see multiple pauses and resumes if we encounter any issues during this process.</span></span>
3. <span data-ttu-id="8ee82-140">Microsoft tworzy nowy magazyn danych o nazwie "MyDW" na magazyn w warstwie premium z kopii zapasowej hello w kroku 2.</span><span class="sxs-lookup"><span data-stu-id="8ee82-140">Microsoft creates a new data warehouse named “MyDW” on premium storage from hello backup taken in step 2.</span></span> <span data-ttu-id="8ee82-141">"MyDW" pojawią się dopiero po zakończeniu przywracania hello.</span><span class="sxs-lookup"><span data-stu-id="8ee82-141">“MyDW” will not appear until after hello restore is complete.</span></span>
4. <span data-ttu-id="8ee82-142">Po zakończeniu przywracania hello "MyDW" zwraca toohello tych samych danych jednostek magazynu i stan (wstrzymana lub aktywnym), który był przed migracją hello.</span><span class="sxs-lookup"><span data-stu-id="8ee82-142">After hello restore is complete, “MyDW” returns toohello same data warehouse units and state (paused or active) that it was before hello migration.</span></span>
5. <span data-ttu-id="8ee82-143">Po zakończeniu migracji hello Microsoft usuwa "MyDW_DO_NOT_USE_ [sygnatury czasowej]".</span><span class="sxs-lookup"><span data-stu-id="8ee82-143">After hello migration is complete, Microsoft deletes “MyDW_DO_NOT_USE_[Timestamp]”.</span></span>

> [!NOTE]
> <span data-ttu-id="8ee82-144">Witaj poniższe ustawienia nie jest przenoszone w ramach migracji hello:</span><span class="sxs-lookup"><span data-stu-id="8ee82-144">hello following settings do not carry over as part of hello migration:</span></span>
>
> * <span data-ttu-id="8ee82-145">Inspekcji na poziomie bazy danych hello musi toobe ponownie włączona.</span><span class="sxs-lookup"><span data-stu-id="8ee82-145">Auditing at hello database level needs toobe re-enabled.</span></span>
> * <span data-ttu-id="8ee82-146">Reguły zapory na poziomie bazy danych hello muszą toobe ponownie dodane.</span><span class="sxs-lookup"><span data-stu-id="8ee82-146">Firewall rules at hello database level need toobe re-added.</span></span> <span data-ttu-id="8ee82-147">Reguły zapory na poziomie serwera hello nie dotyczy.</span><span class="sxs-lookup"><span data-stu-id="8ee82-147">Firewall rules at hello server level are not affected.</span></span>
>
>

### <a name="automatic-migration-schedule"></a><span data-ttu-id="8ee82-148">Automatyczna migracja harmonogramu</span><span class="sxs-lookup"><span data-stu-id="8ee82-148">Automatic migration schedule</span></span>
<span data-ttu-id="8ee82-149">Migracje automatyczne występują między 6:00 a 6:00:00 (czas lokalny dla regionu) podczas hello według harmonogramu awarii.</span><span class="sxs-lookup"><span data-stu-id="8ee82-149">Automatic migrations occur between 6:00 PM and 6:00 AM (local time per region) during hello following outage schedule.</span></span>

| <span data-ttu-id="8ee82-150">**Region**</span><span class="sxs-lookup"><span data-stu-id="8ee82-150">**Region**</span></span> | <span data-ttu-id="8ee82-151">**Szacowana data rozpoczęcia**</span><span class="sxs-lookup"><span data-stu-id="8ee82-151">**Estimated start date**</span></span> | <span data-ttu-id="8ee82-152">**Szacowana data końcowa**</span><span class="sxs-lookup"><span data-stu-id="8ee82-152">**Estimated end date**</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="8ee82-153">Australia Wschodnia</span><span class="sxs-lookup"><span data-stu-id="8ee82-153">Australia East</span></span> |<span data-ttu-id="8ee82-154">Nie można ustalić jeszcze</span><span class="sxs-lookup"><span data-stu-id="8ee82-154">Not determined yet</span></span> |<span data-ttu-id="8ee82-155">Nie można ustalić jeszcze</span><span class="sxs-lookup"><span data-stu-id="8ee82-155">Not determined yet</span></span> |
| <span data-ttu-id="8ee82-156">Chiny Wschodnie</span><span class="sxs-lookup"><span data-stu-id="8ee82-156">China East</span></span> |<span data-ttu-id="8ee82-157">9 stycznia 2017 r.</span><span class="sxs-lookup"><span data-stu-id="8ee82-157">January 9, 2017</span></span> |<span data-ttu-id="8ee82-158">13 stycznia 2017 r.</span><span class="sxs-lookup"><span data-stu-id="8ee82-158">January 13, 2017</span></span> |
| <span data-ttu-id="8ee82-159">Chiny Północne</span><span class="sxs-lookup"><span data-stu-id="8ee82-159">China North</span></span> |<span data-ttu-id="8ee82-160">9 stycznia 2017 r.</span><span class="sxs-lookup"><span data-stu-id="8ee82-160">January 9, 2017</span></span> |<span data-ttu-id="8ee82-161">13 stycznia 2017 r.</span><span class="sxs-lookup"><span data-stu-id="8ee82-161">January 13, 2017</span></span> |
| <span data-ttu-id="8ee82-162">Niemcy Środkowe</span><span class="sxs-lookup"><span data-stu-id="8ee82-162">Germany Central</span></span> |<span data-ttu-id="8ee82-163">9 stycznia 2017 r.</span><span class="sxs-lookup"><span data-stu-id="8ee82-163">January 9, 2017</span></span> |<span data-ttu-id="8ee82-164">13 stycznia 2017 r.</span><span class="sxs-lookup"><span data-stu-id="8ee82-164">January 13, 2017</span></span> |
| <span data-ttu-id="8ee82-165">Niemcy Północno-Wschodnie</span><span class="sxs-lookup"><span data-stu-id="8ee82-165">Germany Northeast</span></span> |<span data-ttu-id="8ee82-166">9 stycznia 2017 r.</span><span class="sxs-lookup"><span data-stu-id="8ee82-166">January 9, 2017</span></span> |<span data-ttu-id="8ee82-167">13 stycznia 2017 r.</span><span class="sxs-lookup"><span data-stu-id="8ee82-167">January 13, 2017</span></span> |
| <span data-ttu-id="8ee82-168">Indie Zachodnie</span><span class="sxs-lookup"><span data-stu-id="8ee82-168">India West</span></span> |<span data-ttu-id="8ee82-169">Nie można ustalić jeszcze</span><span class="sxs-lookup"><span data-stu-id="8ee82-169">Not determined yet</span></span> |<span data-ttu-id="8ee82-170">Nie można ustalić jeszcze</span><span class="sxs-lookup"><span data-stu-id="8ee82-170">Not determined yet</span></span> |
| <span data-ttu-id="8ee82-171">Japonia Zachodnia</span><span class="sxs-lookup"><span data-stu-id="8ee82-171">Japan West</span></span> |<span data-ttu-id="8ee82-172">Nie można ustalić jeszcze</span><span class="sxs-lookup"><span data-stu-id="8ee82-172">Not determined yet</span></span> |<span data-ttu-id="8ee82-173">Nie można ustalić jeszcze</span><span class="sxs-lookup"><span data-stu-id="8ee82-173">Not determined yet</span></span> |
| <span data-ttu-id="8ee82-174">Środkowo-północne stany USA</span><span class="sxs-lookup"><span data-stu-id="8ee82-174">North Central US</span></span> |<span data-ttu-id="8ee82-175">9 stycznia 2017 r.</span><span class="sxs-lookup"><span data-stu-id="8ee82-175">January 9, 2017</span></span> |<span data-ttu-id="8ee82-176">13 stycznia 2017 r.</span><span class="sxs-lookup"><span data-stu-id="8ee82-176">January 13, 2017</span></span> |

## <a name="self-migration-toopremium-storage"></a><span data-ttu-id="8ee82-177">Samodzielna migracji toopremium magazynu</span><span class="sxs-lookup"><span data-stu-id="8ee82-177">Self-migration toopremium storage</span></span>
<span data-ttu-id="8ee82-178">Jeśli chcesz toocontrol, gdy nastąpi z przestoju, można użyć hello następujące kroki toomigrate istniejącego magazynu danych w magazynie toopremium magazynu w warstwie standardowa.</span><span class="sxs-lookup"><span data-stu-id="8ee82-178">If you want toocontrol when your downtime will occur, you can use hello following steps toomigrate an existing data warehouse on standard storage toopremium storage.</span></span> <span data-ttu-id="8ee82-179">Jeśli wybierzesz tę opcję, należy wykonać migracji własny hello przed rozpoczęciem powitalne automatycznej migracji w tym regionie.</span><span class="sxs-lookup"><span data-stu-id="8ee82-179">If you choose this option, you must complete hello self-migration before hello automatic migration begins in that region.</span></span> <span data-ttu-id="8ee82-180">Dzięki temu, że uniknąć ryzyka hello automatycznej migracji powoduje konflikt (zobacz toohello [harmonogramu automatycznej migracji][automatic migration schedule]).</span><span class="sxs-lookup"><span data-stu-id="8ee82-180">This ensures that you avoid any risk of hello automatic migration causing a conflict (refer toohello [automatic migration schedule][automatic migration schedule]).</span></span>

### <a name="self-migration-instructions"></a><span data-ttu-id="8ee82-181">Instrukcje dotyczące migracji samodzielnej</span><span class="sxs-lookup"><span data-stu-id="8ee82-181">Self-migration instructions</span></span>
<span data-ttu-id="8ee82-182">toomigrate danych magazynu samodzielnie, użyj hello kopii zapasowej i przywracania funkcji.</span><span class="sxs-lookup"><span data-stu-id="8ee82-182">toomigrate your data warehouse yourself, use hello backup and restore features.</span></span> <span data-ttu-id="8ee82-183">Hello przywracania część migracji hello jest oczekiwany tootake około jednej godziny na terabajt magazynu na magazyn danych.</span><span class="sxs-lookup"><span data-stu-id="8ee82-183">hello restore portion of hello migration is expected tootake around one hour per terabyte of storage per data warehouse.</span></span> <span data-ttu-id="8ee82-184">Witaj tookeep takie same nazwy, po zakończeniu migracji, należy wykonać hello [toorename kroki podczas migracji][steps toorename during migration].</span><span class="sxs-lookup"><span data-stu-id="8ee82-184">If you want tookeep hello same name after migration is complete, follow hello [steps toorename during migration][steps toorename during migration].</span></span>

1. <span data-ttu-id="8ee82-185">[Wstrzymaj] [ Pause] magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="8ee82-185">[Pause][Pause] your data warehouse.</span></span> <span data-ttu-id="8ee82-186">Kliknięcie tej pozycji spowoduje automatyczne kopie zapasowe.</span><span class="sxs-lookup"><span data-stu-id="8ee82-186">This takes an automatic backup.</span></span>
2. <span data-ttu-id="8ee82-187">[Przywróć] [ Restore] z najnowszych migawki.</span><span class="sxs-lookup"><span data-stu-id="8ee82-187">[Restore][Restore] from your most recent snapshot.</span></span>
3. <span data-ttu-id="8ee82-188">Usuwanie istniejącego magazynu danych na magazynu w warstwie standardowa.</span><span class="sxs-lookup"><span data-stu-id="8ee82-188">Delete your existing data warehouse on standard storage.</span></span> <span data-ttu-id="8ee82-189">**Jeśli nie toodo ten krok zostanie naliczona opłata dla obu magazynów danych.**</span><span class="sxs-lookup"><span data-stu-id="8ee82-189">**If you fail toodo this step, you will be charged for both data warehouses.**</span></span>

> [!NOTE]
> <span data-ttu-id="8ee82-190">Witaj poniższe ustawienia nie jest przenoszone w ramach migracji hello:</span><span class="sxs-lookup"><span data-stu-id="8ee82-190">hello following settings do not carry over as part of hello migration:</span></span>
>
> * <span data-ttu-id="8ee82-191">Inspekcji na poziomie bazy danych hello musi toobe ponownie włączona.</span><span class="sxs-lookup"><span data-stu-id="8ee82-191">Auditing at hello database level needs toobe re-enabled.</span></span>
> * <span data-ttu-id="8ee82-192">Reguły zapory na poziomie bazy danych hello muszą toobe ponownie dodane.</span><span class="sxs-lookup"><span data-stu-id="8ee82-192">Firewall rules at hello database level need toobe re-added.</span></span> <span data-ttu-id="8ee82-193">Reguły zapory na poziomie serwera hello nie dotyczy.</span><span class="sxs-lookup"><span data-stu-id="8ee82-193">Firewall rules at hello server level are not affected.</span></span>
>
>

#### <a name="rename-data-warehouse-during-migration-optional"></a><span data-ttu-id="8ee82-194">Zmień nazwę magazynu danych podczas migracji (opcjonalnie)</span><span class="sxs-lookup"><span data-stu-id="8ee82-194">Rename data warehouse during migration (optional)</span></span>
<span data-ttu-id="8ee82-195">Dwie bazy danych na powitania nie może być tym samym serwerze logicznym hello tej samej nazwy.</span><span class="sxs-lookup"><span data-stu-id="8ee82-195">Two databases on hello same logical server cannot have hello same name.</span></span> <span data-ttu-id="8ee82-196">Magazyn danych SQL obsługuje teraz hello toorename możliwości magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="8ee82-196">SQL Data Warehouse now supports hello ability toorename a data warehouse.</span></span>

<span data-ttu-id="8ee82-197">W tym przykładzie załóżmy, że istniejącego magazynu danych na magazynu w warstwie standardowa aktualnie ma nazwę "MyDW."</span><span class="sxs-lookup"><span data-stu-id="8ee82-197">In this example, imagine that your existing data warehouse on standard storage is currently named “MyDW.”</span></span>

1. <span data-ttu-id="8ee82-198">Zmień nazwę "MyDW" za pomocą następującego polecenia ALTER DATABASE hello.</span><span class="sxs-lookup"><span data-stu-id="8ee82-198">Rename "MyDW" by using hello following ALTER DATABASE command.</span></span> <span data-ttu-id="8ee82-199">(W tym przykładzie firma Microsoft będzie zmień jego nazwę "MyDW_BeforeMigration.")  To polecenie zatrzymania wszystkich istniejących transakcji i musi zostać wykonane w hello toosucceed bazy danych master.</span><span class="sxs-lookup"><span data-stu-id="8ee82-199">(In this example, we'll rename it "MyDW_BeforeMigration.")  This command stops all existing transactions, and must be done in hello master database toosucceed.</span></span>
   ```
   ALTER DATABASE CurrentDatabasename MODIFY NAME = NewDatabaseName;
   ```
2. <span data-ttu-id="8ee82-200">[Wstrzymaj] [ Pause] "MyDW_BeforeMigration."</span><span class="sxs-lookup"><span data-stu-id="8ee82-200">[Pause][Pause] "MyDW_BeforeMigration."</span></span> <span data-ttu-id="8ee82-201">Kliknięcie tej pozycji spowoduje automatyczne kopie zapasowe.</span><span class="sxs-lookup"><span data-stu-id="8ee82-201">This takes an automatic backup.</span></span>
3. <span data-ttu-id="8ee82-202">[Przywróć] [ Restore] z najnowszych migawki nową bazę danych o nazwie hello on toobe (na przykład "MyDW").</span><span class="sxs-lookup"><span data-stu-id="8ee82-202">[Restore][Restore] from your most recent snapshot a new database with hello name it used toobe (for example, "MyDW").</span></span>
4. <span data-ttu-id="8ee82-203">Usuń "MyDW_BeforeMigration."</span><span class="sxs-lookup"><span data-stu-id="8ee82-203">Delete "MyDW_BeforeMigration."</span></span> <span data-ttu-id="8ee82-204">**Jeśli nie toodo ten krok zostanie naliczona opłata dla obu magazynów danych.**</span><span class="sxs-lookup"><span data-stu-id="8ee82-204">**If you fail toodo this step, you will be charged for both data warehouses.**</span></span>


## <a name="next-steps"></a><span data-ttu-id="8ee82-205">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8ee82-205">Next steps</span></span>
<span data-ttu-id="8ee82-206">Bez hello zmienić toopremium magazynu, należy również zwiększonej liczby plików bazy danych obiektów blob w hello podstawowej architektury magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="8ee82-206">With hello change toopremium storage, you also have an increased number of database blob files in hello underlying architecture of your data warehouse.</span></span> <span data-ttu-id="8ee82-207">zwiększenia wydajności hello toomaximize tę zmianę, Odbuduj Twojej klastrowane indeksy magazynu kolumn za pomocą następującego skryptu hello.</span><span class="sxs-lookup"><span data-stu-id="8ee82-207">toomaximize hello performance benefits of this change, rebuild your clustered columnstore indexes by using hello following script.</span></span> <span data-ttu-id="8ee82-208">skrypt Hello działa, powodując, że niektóre istniejące dane toohello dodatkowe obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="8ee82-208">hello script works by forcing some of your existing data toohello additional blobs.</span></span> <span data-ttu-id="8ee82-209">Jeśli nie podejmiesz żadnych działań, danych hello naturalnie zostanie ponownie rozesłać wraz z upływem czasu, ponieważ załadowanie większej ilości danych w tabelach.</span><span class="sxs-lookup"><span data-stu-id="8ee82-209">If you take no action, hello data will naturally redistribute over time as you load more data into your tables.</span></span>

<span data-ttu-id="8ee82-210">**Wymagania wstępne:**</span><span class="sxs-lookup"><span data-stu-id="8ee82-210">**Prerequisites:**</span></span>

- <span data-ttu-id="8ee82-211">Witaj magazynu danych należy uruchamiać z jednostki magazynu danych 1000 lub nowszą (zobacz [mocy obliczeniowej skali][scale compute power]).</span><span class="sxs-lookup"><span data-stu-id="8ee82-211">hello data warehouse should run with 1,000 data warehouse units or higher (see [scale compute power][scale compute power]).</span></span>
- <span data-ttu-id="8ee82-212">Witaj wykonywania skryptu hello użytkownika powinna mieć hello [roli mediumrc] [ mediumrc role] lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="8ee82-212">hello user executing hello script should be in hello [mediumrc role][mediumrc role] or higher.</span></span> <span data-ttu-id="8ee82-213">tooadd toothis roli użytkownika, wykonaj następujące hello:````EXEC sp_addrolemember 'xlargerc', 'MyUser'````</span><span class="sxs-lookup"><span data-stu-id="8ee82-213">tooadd a user toothis role, execute hello following: ````EXEC sp_addrolemember 'xlargerc', 'MyUser'````</span></span>

````sql
-------------------------------------------------------------------------------
-- Step 1: Create table toocontrol index rebuild
-- Run as user in mediumrc or higher
--------------------------------------------------------------------------------
create table sql_statements
WITH (distribution = round_robin)
as select
    'alter index all on ' + s.name + '.' + t.NAME + ' rebuild;' as statement,
    row_number() over (order by s.name, t.name) as sequence
from
    sys.schemas s
    inner join sys.tables t
        on s.schema_id = t.schema_id
where
    is_external = 0
;
go

--------------------------------------------------------------------------------
-- Step 2: Execute index rebuilds. If script fails, hello below can be re-run toorestart where last left off.
-- Run as user in mediumrc or higher
--------------------------------------------------------------------------------

declare @nbr_statements int = (select count(*) from sql_statements)
declare @i int = 1
while(@i <= @nbr_statements)
begin
      declare @statement nvarchar(1000)= (select statement from sql_statements where sequence = @i)
      print cast(getdate() as nvarchar(1000)) + ' Executing... ' + @statement
      exec (@statement)
      delete from sql_statements where sequence = @i
      set @i += 1
end;
go
-------------------------------------------------------------------------------
-- Step 3: Clean up table created in Step 1
--------------------------------------------------------------------------------
drop table sql_statements;
go
````

<span data-ttu-id="8ee82-214">Jeśli wystąpią problemy z magazynem danych, [Utwórz bilet pomocy technicznej] [ create a support ticket] i referencyjne "Magazyn toopremium migracji" jako hello z możliwych przyczyn.</span><span class="sxs-lookup"><span data-stu-id="8ee82-214">If you encounter any issues with your data warehouse, [create a support ticket][create a support ticket] and reference “migration toopremium storage” as hello possible cause.</span></span>

<!--Image references-->

<!--Article references-->
[automatic migration schedule]: #automatic-migration-schedule
[self-migration tooPremium Storage]: #self-migration-to-premium-storage
[create a support ticket]: sql-data-warehouse-get-started-create-support-ticket.md
[Azure paired region]: best-practices-availability-paired-regions.md
[main documentation site]: services/sql-data-warehouse.md
[Pause]: sql-data-warehouse-manage-compute-portal.md#pause-compute
[Restore]: sql-data-warehouse-restore-database-portal.md
[steps toorename during migration]: #optional-steps-to-rename-during-migration
[scale compute power]: sql-data-warehouse-manage-compute-portal.md#scale-compute-power
[mediumrc role]: sql-data-warehouse-develop-concurrency.md

<!--MSDN references-->


<!--Other Web references-->
[Premium Storage for greater performance predictability]: https://azure.microsoft.com/en-us/blog/azure-sql-data-warehouse-introduces-premium-storage-for-greater-performance/
[Azure Portal]: https://portal.azure.com
