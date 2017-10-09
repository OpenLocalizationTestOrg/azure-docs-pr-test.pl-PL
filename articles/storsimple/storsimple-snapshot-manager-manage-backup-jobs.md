---
title: zadania tworzenia kopii zapasowej Snapshot Manager aaaStorSimple | Dokumentacja firmy Microsoft
description: "Opisuje sposób toouse hello tooview przystawki MMC programu StorSimple Snapshot Manager i zarządzanie nimi zaplanowane, uruchomione i zakończonych zadań tworzenia kopii zapasowej."
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: bf4dcff6-c819-4766-b9d9-9922831cb200
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: 3dba0a2aa527d17d67130f537bcdce5722b05a76
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-tooview-and-manage-backup-jobs"></a><span data-ttu-id="6951d-103">Użyj tooview StorSimple Snapshot Manager i zarządzanie nimi zadania tworzenia kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="6951d-103">Use StorSimple Snapshot Manager tooview and manage backup jobs</span></span>

## <a name="overview"></a><span data-ttu-id="6951d-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="6951d-104">Overview</span></span>
<span data-ttu-id="6951d-105">Hello **zadania** węzła w hello **zakres** w okienku zostaną wyświetlone powitalne **zaplanowane**, **ostatnich 24 godzin**, i **systemem**kopii zapasowej zadania, które inicjowane interakcyjnego lub skonfigurowanymi zasadami.</span><span class="sxs-lookup"><span data-stu-id="6951d-105">hello **Jobs** node in hello **Scope** pane shows hello **Scheduled**, **Last 24 hours**, and **Running** backup tasks that you initiated interactively or by a configured policy.</span></span> 

<span data-ttu-id="6951d-106">W tym samouczku opisano, jak używasz hello **zadania** węzła toodisplay informacji na temat zaplanowane, ostatnie i aktualnie uruchomionych zadań tworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="6951d-106">This tutorial explains how you can use hello **Jobs** node toodisplay information about scheduled, recent, and currently running backup jobs.</span></span> <span data-ttu-id="6951d-107">(Lista hello zadania i informacji znajduje się na powitania **wyniki** okienko.) Ponadto można kliknij prawym przyciskiem myszy wymienionych zadań i zobacz menu kontekstowego, który zawiera listę dostępnych akcji.</span><span class="sxs-lookup"><span data-stu-id="6951d-107">(hello list of jobs and corresponding information appears in hello **Results** pane.) Additionally, you can right-click a listed job and see a context menu that lists available actions.</span></span>

## <a name="view-scheduled-jobs"></a><span data-ttu-id="6951d-108">Wyświetl zaplanowane zadania</span><span class="sxs-lookup"><span data-stu-id="6951d-108">View scheduled jobs</span></span>
<span data-ttu-id="6951d-109">Witaj użyj następującej procedury tooview zaplanowanych zadań tworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="6951d-109">Use hello following procedure tooview scheduled backup jobs.</span></span>

#### <a name="tooview-scheduled-jobs"></a><span data-ttu-id="6951d-110">tooview zaplanowane zadania</span><span class="sxs-lookup"><span data-stu-id="6951d-110">tooview scheduled jobs</span></span>
1. <span data-ttu-id="6951d-111">Kliknij przycisk hello ikony pulpitu toostart StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="6951d-111">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span> 
2. <span data-ttu-id="6951d-112">W hello **zakres** okienku rozwiń hello **zadania** węzeł, a następnie kliknij przycisk **zaplanowane**.</span><span class="sxs-lookup"><span data-stu-id="6951d-112">In hello **Scope** pane, expand hello **Jobs** node, and click **Scheduled**.</span></span> <span data-ttu-id="6951d-113">Hello następujące informacje są wyświetlane w hello **wyniki** okienka:</span><span class="sxs-lookup"><span data-stu-id="6951d-113">hello following information appears in hello **Results** pane:</span></span>
   
   * <span data-ttu-id="6951d-114">**Nazwa** — Witaj nazwa hello zaplanowaną migawkę</span><span class="sxs-lookup"><span data-stu-id="6951d-114">**Name** – hello name of hello scheduled snapshot</span></span>
   * <span data-ttu-id="6951d-115">**Uruchom** — hello Data i godzina hello następną zaplanowaną migawkę</span><span class="sxs-lookup"><span data-stu-id="6951d-115">**Next Run** – hello date and time of hello next scheduled snapshot</span></span>
   * <span data-ttu-id="6951d-116">**Ostatnie uruchomienie** — hello Data i godzina ostatniej zaplanowanej migawki hello</span><span class="sxs-lookup"><span data-stu-id="6951d-116">**Last Run** – hello date and time of hello most recent scheduled snapshot</span></span>
     
     > [!NOTE]
     > <span data-ttu-id="6951d-117">Jednorazowe tylko migawek, hello **następnego uruchomienia** i **ostatnie uruchomienie** będzie hello takie same.</span><span class="sxs-lookup"><span data-stu-id="6951d-117">For one-time only snapshots, hello **Next Run** and **Last Run** will be hello same.</span></span>
     
     ![Zaplanowanych zadań kopii zapasowej](./media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_scheduled.png) 
3. <span data-ttu-id="6951d-119">tooperform dodatkowe akcje w konkretnym zadaniu, kliknij prawym przyciskiem myszy nazwę zadania hello w hello **wyniki** okienka, a następnie zaznacz opcje menu hello.</span><span class="sxs-lookup"><span data-stu-id="6951d-119">tooperform additional actions on a specific job, right-click hello job name in hello **Results** pane and select from hello menu options.</span></span>

## <a name="view-recent-jobs"></a><span data-ttu-id="6951d-120">Wyświetl ostatnie zadania</span><span class="sxs-lookup"><span data-stu-id="6951d-120">View recent jobs</span></span>
<span data-ttu-id="6951d-121">Użyj powitania po tooview procedury tworzenia kopii zapasowej i przywracania zadania, które zostały ukończone w hello ostatnich 24 godzin.</span><span class="sxs-lookup"><span data-stu-id="6951d-121">Use hello following procedure tooview backup and restore jobs that were completed in hello last 24 hours.</span></span>

#### <a name="tooview-recent-jobs"></a><span data-ttu-id="6951d-122">tooview ostatnich zadań</span><span class="sxs-lookup"><span data-stu-id="6951d-122">tooview recent jobs</span></span>
1. <span data-ttu-id="6951d-123">Kliknij przycisk hello ikony pulpitu toostart StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="6951d-123">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="6951d-124">W hello **zakres** okienku rozwiń hello **zadania** węzeł, a następnie kliknij przycisk **ostatnich 24 godzin**.</span><span class="sxs-lookup"><span data-stu-id="6951d-124">In hello **Scope** pane, expand hello **Jobs** node, and click **Last 24 hours**.</span></span> <span data-ttu-id="6951d-125">Witaj **wyniki** w okienku zostaną wyświetlone zadania tworzenia kopii zapasowej hello w ostatnich 24 godzinach (maksymalnie tooa 64 zadania).</span><span class="sxs-lookup"><span data-stu-id="6951d-125">hello **Results** pane shows backup jobs for hello last 24 hours (tooa maximum of 64 jobs).</span></span> <span data-ttu-id="6951d-126">Hello następujące informacje są wyświetlane w hello **wyniki** okienko, w zależności od hello **widoku** możesz określić opcje:</span><span class="sxs-lookup"><span data-stu-id="6951d-126">hello following information appears in hello **Results** pane, depending on hello **View** options you specify:</span></span>
   
   * <span data-ttu-id="6951d-127">**Nazwa** — Witaj nazwa hello zaplanowaną migawkę.</span><span class="sxs-lookup"><span data-stu-id="6951d-127">**Name** – hello name of hello scheduled snapshot.</span></span>
   * <span data-ttu-id="6951d-128">**Rozpoczęto** — hello Data i godzina rozpoczęcia hello migawki.</span><span class="sxs-lookup"><span data-stu-id="6951d-128">**Started** – hello date and time when hello snapshot began.</span></span>
   * <span data-ttu-id="6951d-129">**Zatrzymano** — Data hello i migawki hello zakończono lub zostało przerwane.</span><span class="sxs-lookup"><span data-stu-id="6951d-129">**Stopped** – hello date and time when hello snapshot finished or was terminated.</span></span>
   * <span data-ttu-id="6951d-130">**Upłynął** — Witaj ilość czasu między hello **uruchomiono** i **zatrzymane** razy.</span><span class="sxs-lookup"><span data-stu-id="6951d-130">**Elapsed** – hello amount of time between hello **Started** and **Stopped** times.</span></span>
   * <span data-ttu-id="6951d-131">**Stan** — Witaj stan hello niedawno ukończoną zadania.</span><span class="sxs-lookup"><span data-stu-id="6951d-131">**Status** – hello state of hello recently completed job.</span></span> <span data-ttu-id="6951d-132">**Powodzenie** wskazuje hello kopii zapasowej został utworzony pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="6951d-132">**Success** indicates that hello backup was created successfully.</span></span> <span data-ttu-id="6951d-133">**Nie powiodło się** wskazuje hello zadania nie zostało uruchomione pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="6951d-133">**Failed** indicates that hello job did not run successfully.</span></span>
   * <span data-ttu-id="6951d-134">**Informacje o** — Witaj Przyczyna niepowodzenia hello.</span><span class="sxs-lookup"><span data-stu-id="6951d-134">**Information** – hello reason for hello failure.</span></span>
   * <span data-ttu-id="6951d-135">**Bajty przetwarzane (MB)** — Witaj ilości danych z grupy hello woluminu, który był przetwarzany (w MB).</span><span class="sxs-lookup"><span data-stu-id="6951d-135">**Bytes processed (MB)** – hello amount of data from hello volume group that was processed (in MBs).</span></span> 
     
     ![Zadania, które były uruchamiane w hello w ostatnich 24 godzinach](./media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_Last_24_hours.png) 
3. <span data-ttu-id="6951d-137">tooperform dodatkowe akcje w konkretnym zadaniu, kliknij prawym przyciskiem myszy nazwę zadania hello w hello **wyniki** okienka, a następnie zaznacz opcje menu hello.</span><span class="sxs-lookup"><span data-stu-id="6951d-137">tooperform additional actions on a specific job, right-click hello job name in hello **Results** pane and select from hello menu options.</span></span>
   
    ![Usuwanie zadania](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Delete_backup.png)

## <a name="view-currently-running-jobs"></a><span data-ttu-id="6951d-139">Wyświetl uruchomione zadania</span><span class="sxs-lookup"><span data-stu-id="6951d-139">View currently running jobs</span></span>
<span data-ttu-id="6951d-140">Witaj użyj następującej procedury tooview zadania, które są aktualnie uruchomione.</span><span class="sxs-lookup"><span data-stu-id="6951d-140">Use hello following procedure tooview jobs that are currently running.</span></span>

#### <a name="tooview-currently-running-jobs"></a><span data-ttu-id="6951d-141">tooview aktualnie uruchomionych zadań</span><span class="sxs-lookup"><span data-stu-id="6951d-141">tooview currently running jobs</span></span>
1. <span data-ttu-id="6951d-142">Kliknij przycisk hello ikony pulpitu toostart StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="6951d-142">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="6951d-143">W hello **zakres** okienku rozwiń hello **zadania** węzeł, a następnie kliknij przycisk **systemem**.</span><span class="sxs-lookup"><span data-stu-id="6951d-143">In hello **Scope** pane, expand hello **Jobs** node, and click **Running**.</span></span> <span data-ttu-id="6951d-144">W zależności od hello **widoku** opcje określisz, hello następujących informacji jest wyświetlana w hello **wyniki** okienka:</span><span class="sxs-lookup"><span data-stu-id="6951d-144">Depending on hello **View** options you specify, hello following information appears in hello **Results** pane:</span></span>
   
   * <span data-ttu-id="6951d-145">**Nazwa** — Witaj nazwa hello zaplanowaną migawkę.</span><span class="sxs-lookup"><span data-stu-id="6951d-145">**Name** – hello name of hello scheduled snapshot.</span></span>
   * <span data-ttu-id="6951d-146">**Rozpoczęto** — hello Data i godzina rozpoczęcia hello migawki.</span><span class="sxs-lookup"><span data-stu-id="6951d-146">**Started** – hello date and time when hello snapshot began.</span></span>
   * <span data-ttu-id="6951d-147">**Punkt kontrolny** — Witaj bieżącej akcji hello kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="6951d-147">**Checkpoint** – hello current action of hello backup.</span></span>
   * <span data-ttu-id="6951d-148">**Stan** — Witaj procentu ukończenia.</span><span class="sxs-lookup"><span data-stu-id="6951d-148">**Status** – hello percentage of completion.</span></span>
   * <span data-ttu-id="6951d-149">**Upłynął** — Witaj ilość czasu, jaki upłynął od chwili rozpoczęcia tworzenia kopii zapasowej hello.</span><span class="sxs-lookup"><span data-stu-id="6951d-149">**Elapsed** – hello amount of time that has passed since hello backup began.</span></span> 
   * <span data-ttu-id="6951d-150">**Średnia przepływność (MB)** — współczynnik łączna liczba bajtów danych przetwarzanych toothat łączny czas poświęcony na przetwarzanie (MB).</span><span class="sxs-lookup"><span data-stu-id="6951d-150">**Average throughput (MB)** – ratio of total bytes of data processed toothat of total time taken for processing (MBs).</span></span>
   * <span data-ttu-id="6951d-151">**Bajty przetwarzane (MB)** — łączna liczba bajtów dane przetworzone (w MB).</span><span class="sxs-lookup"><span data-stu-id="6951d-151">**Bytes processed (MB)** – total bytes of data processed (in MBs).</span></span>
   * <span data-ttu-id="6951d-152">**Bajty zapisane (MB)** — łączna liczba bajtów danych (w MB).</span><span class="sxs-lookup"><span data-stu-id="6951d-152">**Bytes written (MB)** – total bytes of data written (in MBs).</span></span> <span data-ttu-id="6951d-153">Ona zawiera hello danych, a także hello metadanych i dlatego zazwyczaj większe niż hello przetwarzane bajtów.</span><span class="sxs-lookup"><span data-stu-id="6951d-153">It includes hello data as well as hello metadata and hence is typically greater than hello Bytes Processed.</span></span>
     
     ![Obecnie uruchomionych zadań](./media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_running.png)
3. <span data-ttu-id="6951d-155">tooperform dodatkowe akcje w konkretnym zadaniu, kliknij prawym przyciskiem myszy nazwę zadania hello w hello **wyniki** okienka, a następnie zaznacz opcje menu hello.</span><span class="sxs-lookup"><span data-stu-id="6951d-155">tooperform additional actions on a specific job, right-click hello job name in hello **Results** pane and select from hello menu options.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6951d-156">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6951d-156">Next steps</span></span>
* <span data-ttu-id="6951d-157">Dowiedz się, jak za[użyć tooadminister StorSimple Snapshot Manager rozwiązania StorSimple](storsimple-snapshot-manager-admin.md).</span><span class="sxs-lookup"><span data-stu-id="6951d-157">Learn how too[use StorSimple Snapshot Manager tooadminister your StorSimple solution](storsimple-snapshot-manager-admin.md).</span></span>
* <span data-ttu-id="6951d-158">Dowiedz się, jak za[używać katalogu kopii zapasowej hello toomanage StorSimple Snapshot Manager](storsimple-snapshot-manager-manage-backup-catalog.md).</span><span class="sxs-lookup"><span data-stu-id="6951d-158">Learn how too[use StorSimple Snapshot Manager toomanage hello backup catalog](storsimple-snapshot-manager-manage-backup-catalog.md).</span></span>

