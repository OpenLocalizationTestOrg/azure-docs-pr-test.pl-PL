---
title: "aaaView i zarządzać zadaniami serii StorSimple 8000 | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano bloku zadania usługi Menedżer StorSimple urządzenia hello i w jaki sposób toouse on tootrack ostatnie, bieżących i zaplanowanych zadań tworzenia kopii zapasowej."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/29/2017
ms.author: alkohli
ms.openlocfilehash: a76acd67e2568478dd43d0fb16c1ae2dfb72a23d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-tooview-and-manage-jobs-update-3-and-later"></a><span data-ttu-id="0708c-103">Użyj tooview usługi Menedżer StorSimple urządzenia hello zadania i zarządzać nimi (Update 3 i nowsze)</span><span class="sxs-lookup"><span data-stu-id="0708c-103">Use hello StorSimple Device Manager service tooview and manage jobs (Update 3 and later)</span></span>

## <a name="overview"></a><span data-ttu-id="0708c-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="0708c-104">Overview</span></span>
<span data-ttu-id="0708c-105">Witaj **zadania** bloku zapewnia jednym portalu centralnej do wyświetlenia i zarządzanie zadaniami, które zostały uruchomione na urządzeniach połączone usługi Menedżer StorSimple urządzenia tooyour.</span><span class="sxs-lookup"><span data-stu-id="0708c-105">hello **Jobs** blade provides a single central portal for viewing and managing jobs that were started on devices connected tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="0708c-106">Można wyświetlić zadań zaplanowanych, uruchomionych, zakończone, anulowane i nie powiodło się dla wielu urządzeń.</span><span class="sxs-lookup"><span data-stu-id="0708c-106">You can view scheduled, running, completed, canceled, and failed jobs for multiple devices.</span></span> <span data-ttu-id="0708c-107">Wyniki są prezentowane w formie tabeli.</span><span class="sxs-lookup"><span data-stu-id="0708c-107">Results are presented in a tabular format.</span></span>

![Bloku zadań](./media/storsimple-8000-manage-jobs-u2/jobs1.png)

<span data-ttu-id="0708c-109">Można szybko znaleźć hello zadania, które są zainteresowani przez filtrowanie w polach, takich jak:</span><span class="sxs-lookup"><span data-stu-id="0708c-109">You can quickly find hello jobs you are interested in by filtering on fields such as:</span></span>

* <span data-ttu-id="0708c-110">**Stan** — zadania mogą być w toku, zakończyło się pomyślnie, anulowane, nie powiodło się, anulowanie lub zakończyło się pomyślnie z błędów.</span><span class="sxs-lookup"><span data-stu-id="0708c-110">**Status** – Jobs can be in progress, succeeded, canceled, failed, canceling, or succeeded with errors.</span></span>
* <span data-ttu-id="0708c-111">**Zakres czasu** — zadania mogą być filtrowane na podstawie hello zakres dat i godzin.</span><span class="sxs-lookup"><span data-stu-id="0708c-111">**Time range** – Jobs can be filtered based on hello date and time range.</span></span> <span data-ttu-id="0708c-112">zakresy Hello, dla których minął godzinę po 24 godzinach, ostatnie 7 dni, ostatnie 30 dni, ostatni rok lub Niestandardowa data.</span><span class="sxs-lookup"><span data-stu-id="0708c-112">hello ranges are past 1 hour, past 24 hours, past 7 days, past 30 days, past year, or custom date.</span></span>
* <span data-ttu-id="0708c-113">**Typ** — typ zadania hello można zaplanowanego tworzenia kopii zapasowej, ręcznego tworzenia kopii zapasowej i przywracania kopii zapasowej, Klonowanie woluminów, awaryjnie kontenery woluminów, utworzyć wolumin przypięty lokalnie, zmodyfikować woluminu, instalowania aktualizacji, zbierz dzienniki pomocy technicznej i utworzyć urządzenia chmury.</span><span class="sxs-lookup"><span data-stu-id="0708c-113">**Type** – hello job type can be scheduled backup, manual backup, restore backup, clone volume, fail over volume containers, create locally-pinned volume, modify volume, install updates, collect support logs and create cloud appliance.</span></span>
* <span data-ttu-id="0708c-114">**Urządzenia** — zadań są inicjowane na niektórych usługi tooyour podłączonych urządzeń.</span><span class="sxs-lookup"><span data-stu-id="0708c-114">**Devices** – Jobs are initiated on a certain device connected tooyour service.</span></span>
  
<span data-ttu-id="0708c-115">Witaj odfiltrowanych zadań następnie wyszczególniono na podstawie hello hello następujące atrybuty:</span><span class="sxs-lookup"><span data-stu-id="0708c-115">hello filtered jobs are then tabulated on hello basis of hello following attributes:</span></span>
  
* <span data-ttu-id="0708c-116">**Nazwa** — zaplanowanego tworzenia kopii zapasowej, ręcznego tworzenia kopii zapasowych, przywracania kopii zapasowej woluminu w klonowania, tryb failover kontenery woluminów tworzenia woluminu przypiętego lokalnie, zmodyfikować woluminu, instalowania aktualizacji, zbierz dzienniki pomocy technicznej lub utworzyć urządzenia chmury.</span><span class="sxs-lookup"><span data-stu-id="0708c-116">**Name** – scheduled backup, manual backup, restore backup, clone volume, fail over volume containers, create locally pinned volume, modify volume, install updates, collect support logs, or create cloud appliance.</span></span>
* <span data-ttu-id="0708c-117">**Stan** — uruchomiona, zakończone, anulowane, nie powiodło się, anulowanie lub ukończone z błędami.</span><span class="sxs-lookup"><span data-stu-id="0708c-117">**Status** – running, completed, canceled, failed, canceling, or completed with errors.</span></span>
* <span data-ttu-id="0708c-118">**Jednostka** — hello zadań można skojarzyć z woluminu, zasad tworzenia kopii zapasowej lub urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="0708c-118">**Entity** – hello jobs can be associated with a volume, a backup policy, or a device.</span></span> <span data-ttu-id="0708c-119">Na przykład zadanie klonowania jest skojarzony z woluminem, zaplanowane zadanie tworzenia kopii zapasowej jest skojarzone z zasadami tworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="0708c-119">For example, a clone job is associated with a volume, whereas a scheduled backup job is associated with a backup policy.</span></span> <span data-ttu-id="0708c-120">Zadania urządzenia jest tworzony w wyniku odzyskiwania awaryjnego (DR) lub operacji przywracania.</span><span class="sxs-lookup"><span data-stu-id="0708c-120">A device job is created as a result of a disaster recovery (DR) or a restore operation.</span></span>
* <span data-ttu-id="0708c-121">**Urządzenie** — Witaj nazwa hello urządzenia, na którym hello zadanie zostało uruchomione.</span><span class="sxs-lookup"><span data-stu-id="0708c-121">**Device** – hello name of hello device on which hello job was started.</span></span>
* <span data-ttu-id="0708c-122">**Rozpoczęto w** — Witaj czas uruchomienia zadania hello.</span><span class="sxs-lookup"><span data-stu-id="0708c-122">**Started on** – hello time when hello job was started.</span></span>
* <span data-ttu-id="0708c-123">**Czas trwania** — hello czasu wymaganego toocomplete hello zadania.</span><span class="sxs-lookup"><span data-stu-id="0708c-123">**Duration** – hello time required toocomplete hello job.</span></span>

<span data-ttu-id="0708c-124">Witaj listy zadań są odświeżane co 30 sekund.</span><span class="sxs-lookup"><span data-stu-id="0708c-124">hello list of jobs is refreshed every 30 seconds.</span></span>

<span data-ttu-id="0708c-125">Można wykonywać następujące zadania związane z akcji na tej stronie powitania:</span><span class="sxs-lookup"><span data-stu-id="0708c-125">You can perform hello following job-related actions on this page:</span></span>

* <span data-ttu-id="0708c-126">Wyświetlanie szczegółów zadania</span><span class="sxs-lookup"><span data-stu-id="0708c-126">View job details</span></span>
* <span data-ttu-id="0708c-127">Anulowanie zadania</span><span class="sxs-lookup"><span data-stu-id="0708c-127">Cancel a job</span></span>

## <a name="view-job-details"></a><span data-ttu-id="0708c-128">Wyświetlanie szczegółów zadania</span><span class="sxs-lookup"><span data-stu-id="0708c-128">View job details</span></span>
<span data-ttu-id="0708c-129">Wykonaj hello poniższe kroki tooview hello informacje wszystkie zadania.</span><span class="sxs-lookup"><span data-stu-id="0708c-129">Perform hello following steps tooview hello details of any job.</span></span>

#### <a name="tooview-job-details"></a><span data-ttu-id="0708c-130">Szczegóły zadania tooview</span><span class="sxs-lookup"><span data-stu-id="0708c-130">tooview job details</span></span>
1. <span data-ttu-id="0708c-131">Przejdź tooyour usługi Menedżer urządzeń StorSimple, a następnie kliknij przycisk **zadania**.</span><span class="sxs-lookup"><span data-stu-id="0708c-131">Go tooyour StorSimple Device Manager service and then click **Jobs**.</span></span>

2. <span data-ttu-id="0708c-132">W hello **zadania** bloku, wyświetlania zadań hello są zainteresowani, uruchamiając zapytanie o odpowiednie filtry.</span><span class="sxs-lookup"><span data-stu-id="0708c-132">In hello **Jobs** blade, display hello job(s) you are interested in by running a query with appropriate filters.</span></span> <span data-ttu-id="0708c-133">Można wyszukiwać ukończone, uruchomiona lub anulowane zadania.</span><span class="sxs-lookup"><span data-stu-id="0708c-133">You can search for completed, running, or canceled jobs.</span></span>

    ![Blok zadania](./media/storsimple-8000-manage-jobs-u2/jobs1.png)

2. <span data-ttu-id="0708c-135">Wybierz, a następnie kliknij zadanie.</span><span class="sxs-lookup"><span data-stu-id="0708c-135">Select and click a job.</span></span>

    ![Blok zadania](./media/storsimple-8000-manage-jobs-u2/jobs3.png)

3. <span data-ttu-id="0708c-137">W bloku szczegóły zadania hello można wyświetlić stan hello, szczegóły statystyk czasu i statystyki danych.</span><span class="sxs-lookup"><span data-stu-id="0708c-137">In hello job details blade, you can view hello status, details, time statistics, and data statistics.</span></span>
   
    ![Szczegóły zadania](./media/storsimple-8000-manage-jobs-u2/jobs4.png)

## <a name="cancel-a-job"></a><span data-ttu-id="0708c-139">Anulowanie zadania</span><span class="sxs-lookup"><span data-stu-id="0708c-139">Cancel a job</span></span>
<span data-ttu-id="0708c-140">Wykonaj następujące kroki toocancel wykonywanym zadaniem hello.</span><span class="sxs-lookup"><span data-stu-id="0708c-140">Perform hello following steps toocancel a running job.</span></span>

> [!NOTE]
> <span data-ttu-id="0708c-141">Niektóre zadania, takie jak modyfikowanie woluminu toochange hello woluminie, którego typ lub rozszerzenie woluminu, nie można anulować.</span><span class="sxs-lookup"><span data-stu-id="0708c-141">Some jobs, such as modifying a volume toochange hello volume type or expanding a volume, cannot be canceled.</span></span>


### <a name="toocancel-a-job"></a><span data-ttu-id="0708c-142">toocancel zadania</span><span class="sxs-lookup"><span data-stu-id="0708c-142">toocancel a job</span></span>
1. <span data-ttu-id="0708c-143">Na powitania **zadania** strony, wyświetlania zadań uruchomionych hello mają toocancel, uruchamiając zapytanie o odpowiednie filtry.</span><span class="sxs-lookup"><span data-stu-id="0708c-143">On hello **Jobs** page, display hello running job(s) that you want toocancel by running a query with appropriate filters.</span></span> <span data-ttu-id="0708c-144">Wybierz zadanie hello.</span><span class="sxs-lookup"><span data-stu-id="0708c-144">Select hello job.</span></span>

2. <span data-ttu-id="0708c-145">Kliknij prawym przyciskiem myszy, w menu kontekstowym hello hello wybranego zadania tooinvoke, a następnie kliknij przycisk **anulować**.</span><span class="sxs-lookup"><span data-stu-id="0708c-145">Right-click on hello selected job tooinvoke hello context menu and click **Cancel**.</span></span>

    ![Szczegóły zadania](./media/storsimple-8000-manage-jobs-u2/jobs2.png)

3. <span data-ttu-id="0708c-147">Po wyświetleniu monitu o potwierdzenie kliknij przycisk **Tak**.</span><span class="sxs-lookup"><span data-stu-id="0708c-147">When prompted for confirmation, click **Yes**.</span></span> <span data-ttu-id="0708c-148">To zadanie jest teraz anulowane.</span><span class="sxs-lookup"><span data-stu-id="0708c-148">This job is now canceled.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0708c-149">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0708c-149">Next steps</span></span>
* <span data-ttu-id="0708c-150">Dowiedz się, jak za[Zarządzanie zasadami tworzenia kopii zapasowej StorSimple](storsimple-8000-manage-backup-policies-u2.md).</span><span class="sxs-lookup"><span data-stu-id="0708c-150">Learn how too[manage your StorSimple backup policies](storsimple-8000-manage-backup-policies-u2.md).</span></span>
* <span data-ttu-id="0708c-151">Dowiedz się, jak za[Użyj hello tooadminister usługi Menedżera urządzeń StorSimple, urządzenia StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="0708c-151">Learn how too[use hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

