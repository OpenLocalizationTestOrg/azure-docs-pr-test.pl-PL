---
title: "aaaView StorSimple zadania i zarządzać nimi | Dokumentacja firmy Microsoft"
description: "Zawiera opis strony zadania usługi Menedżer StorSimple hello i w jaki sposób toouse on tootrack ostatnie, bieżących i zaplanowanych zadań tworzenia kopii zapasowej."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 55922cd0-d490-48eb-938a-012a67c1c09e
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: b7341270e37a9f2530a8da1fb7c54f6b699c699c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-tooview-and-manage-storsimple-jobs"></a><span data-ttu-id="30e3b-103">Użyj tooview usługi Menedżer StorSimple hello zadania i zarządzać nimi StorSimple</span><span class="sxs-lookup"><span data-stu-id="30e3b-103">Use hello StorSimple Manager service tooview and manage StorSimple jobs</span></span>
[!INCLUDE [storsimple-version-selector-manage-jobs](../../includes/storsimple-version-selector-manage-jobs.md)]

## <a name="overview"></a><span data-ttu-id="30e3b-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="30e3b-104">Overview</span></span>
<span data-ttu-id="30e3b-105">Witaj **zadania** strona zawiera pojedynczy portalu centralnej do przeglądania i zarządzania zadaniami, które zostały uruchomione na urządzeniach podłączony tooyour usługi Menedżer StorSimple.</span><span class="sxs-lookup"><span data-stu-id="30e3b-105">hello **Jobs** page provides a single central portal for viewing and managing jobs that were started on devices connected tooyour StorSimple Manager service.</span></span> <span data-ttu-id="30e3b-106">Można wyświetlić zadań zaplanowanych, uruchomionych, została zakończona i nie powiodło się dla wielu urządzeń.</span><span class="sxs-lookup"><span data-stu-id="30e3b-106">You can view scheduled, running, completed, and failed jobs for multiple devices.</span></span> <span data-ttu-id="30e3b-107">Wyniki są prezentowane w formie tabeli.</span><span class="sxs-lookup"><span data-stu-id="30e3b-107">Results are presented in a tabular format.</span></span> 

![Strona zadania](./media/storsimple-manage-jobs/HCS_JobsPage.png)

<span data-ttu-id="30e3b-109">Można szybko znaleźć hello zadania, które są zainteresowani przez filtrowanie w polach, takich jak:</span><span class="sxs-lookup"><span data-stu-id="30e3b-109">You can quickly find hello jobs you are interested in by filtering on fields such as:</span></span>

* <span data-ttu-id="30e3b-110">**Stan** — zadania może być uruchomiony, zaplanowane, nie powiodło się, ukończonych, anulowanie lub anulowane.</span><span class="sxs-lookup"><span data-stu-id="30e3b-110">**Status** – Jobs can be running, scheduled, failed, completed, canceling, or canceled.</span></span>
* <span data-ttu-id="30e3b-111">**Typ** — zadania mogą być tworzone w wyniku zaplanowanego lub kopii zapasowej na żądanie (**wykonać kopii zapasowej**), klonowanie, przywracania urządzenia lub operacji aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="30e3b-111">**Type** – Jobs can be created as a result of a scheduled or an on-demand backup (**Take Backup**), cloning, a device restore, or an update operation.</span></span>
* <span data-ttu-id="30e3b-112">**Urządzenia** — zadań są inicjowane na niektórych usługi tooyour podłączonych urządzeń.</span><span class="sxs-lookup"><span data-stu-id="30e3b-112">**Devices** – Jobs are initiated on a certain device connected tooyour service.</span></span>
* <span data-ttu-id="30e3b-113">**Od i do** — zadania mogą być filtrowane na podstawie hello zakres dat i godzin.</span><span class="sxs-lookup"><span data-stu-id="30e3b-113">**From and To** – Jobs can be filtered based on hello date and time range.</span></span>

<span data-ttu-id="30e3b-114">Witaj odfiltrowanych zadań następnie wyszczególniono na podstawie hello hello następujące atrybuty:</span><span class="sxs-lookup"><span data-stu-id="30e3b-114">hello filtered jobs are then tabulated on hello basis of hello following attributes:</span></span>

* <span data-ttu-id="30e3b-115">**Typ** — kopii zapasowej, sklonowany, przywracania, pracy awaryjnej lub aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="30e3b-115">**Type** – Backup, clone, restore, failover, or update.</span></span>
* <span data-ttu-id="30e3b-116">**Stan** — uruchomiona, zaplanowane, nie powiodło się, ukończone, anulowanie lub anulowane.</span><span class="sxs-lookup"><span data-stu-id="30e3b-116">**Status** – Running, scheduled, failed, completed, canceling, or canceled.</span></span>
* <span data-ttu-id="30e3b-117">**Jednostka** — hello zadań można skojarzyć z woluminu, zasad tworzenia kopii zapasowej lub urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="30e3b-117">**Entity** – hello jobs can be associated with a volume, a backup policy, or a device.</span></span> <span data-ttu-id="30e3b-118">Zadanie klonowania jest skojarzony z woluminem, zaplanowane zadanie tworzenia kopii zapasowej jest skojarzone z zasadami tworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="30e3b-118">A clone job is associated with a volume, whereas a scheduled backup job is associated with a backup policy.</span></span> <span data-ttu-id="30e3b-119">Zadania urządzenia jest tworzony w wyniku odzyskiwania awaryjnego (DR) lub operacji przywracania.</span><span class="sxs-lookup"><span data-stu-id="30e3b-119">A device job is created as a result of a disaster recovery (DR) or a restore operation.</span></span>
* <span data-ttu-id="30e3b-120">**Urządzenie** — Witaj nazwa hello urządzenia, na którym hello zadanie zostało uruchomione.</span><span class="sxs-lookup"><span data-stu-id="30e3b-120">**Device** – hello name of hello device on which hello job was started.</span></span>
* <span data-ttu-id="30e3b-121">**Rozpoczęto na** — Witaj czas uruchomienia zadania hello.</span><span class="sxs-lookup"><span data-stu-id="30e3b-121">**Started On** – hello time when hello job was started.</span></span>
* <span data-ttu-id="30e3b-122">**Postęp** — Witaj procentu ukończenia uruchomionego zadania.</span><span class="sxs-lookup"><span data-stu-id="30e3b-122">**Progress** – hello percentage completion of a running job.</span></span> <span data-ttu-id="30e3b-123">Zadanie zostało ukończone, aby uzyskać to zawsze być 100%.</span><span class="sxs-lookup"><span data-stu-id="30e3b-123">For a completed job, this should always be 100%.</span></span>

<span data-ttu-id="30e3b-124">Witaj listy zadań są odświeżane co 30 sekund.</span><span class="sxs-lookup"><span data-stu-id="30e3b-124">hello list of jobs is refreshed every 30 seconds.</span></span>

<span data-ttu-id="30e3b-125">Można wykonywać następujące zadania związane z akcji na tej stronie powitania:</span><span class="sxs-lookup"><span data-stu-id="30e3b-125">You can perform hello following job-related actions on this page:</span></span>

* <span data-ttu-id="30e3b-126">Wyświetlanie szczegółów zadania</span><span class="sxs-lookup"><span data-stu-id="30e3b-126">View job details</span></span>
* <span data-ttu-id="30e3b-127">Anulowanie zadania</span><span class="sxs-lookup"><span data-stu-id="30e3b-127">Cancel a job</span></span>

## <a name="view-job-details"></a><span data-ttu-id="30e3b-128">Wyświetlanie szczegółów zadania</span><span class="sxs-lookup"><span data-stu-id="30e3b-128">View job details</span></span>
<span data-ttu-id="30e3b-129">Wykonaj hello poniższe kroki tooview hello informacje wszystkie zadania.</span><span class="sxs-lookup"><span data-stu-id="30e3b-129">Perform hello following steps tooview hello details of any job.</span></span>

#### <a name="tooview-job-details"></a><span data-ttu-id="30e3b-130">Szczegóły zadania tooview</span><span class="sxs-lookup"><span data-stu-id="30e3b-130">tooview job details</span></span>
1. <span data-ttu-id="30e3b-131">Na powitania **zadania** strony, wyświetlania zadań hello są zainteresowani, uruchamiając zapytanie o odpowiednie filtry.</span><span class="sxs-lookup"><span data-stu-id="30e3b-131">On hello **Jobs** page, display hello job(s) you are interested in by running a query with appropriate filters.</span></span> <span data-ttu-id="30e3b-132">Można wyszukiwać ukończone, uruchomiona lub anulowane zadania.</span><span class="sxs-lookup"><span data-stu-id="30e3b-132">You can search for completed, running, or canceled jobs.</span></span>
2. <span data-ttu-id="30e3b-133">Wybierz zadanie.</span><span class="sxs-lookup"><span data-stu-id="30e3b-133">Select a job.</span></span>
3. <span data-ttu-id="30e3b-134">U dołu hello hello strony, kliknij przycisk **szczegóły**.</span><span class="sxs-lookup"><span data-stu-id="30e3b-134">At hello bottom of hello page, click **Details**.</span></span>
4. <span data-ttu-id="30e3b-135">W hello **szczegóły zadania tworzenia kopii zapasowej** okno dialogowe, można wyświetlić stan hello, szczegóły statystyk czasu i statystyki danych.</span><span class="sxs-lookup"><span data-stu-id="30e3b-135">In hello **Backup Job Details** dialog box, you can view hello status, details, time statistics, and data statistics.</span></span>

## <a name="cancel-a-job"></a><span data-ttu-id="30e3b-136">Anulowanie zadania</span><span class="sxs-lookup"><span data-stu-id="30e3b-136">Cancel a job</span></span>
<span data-ttu-id="30e3b-137">Wykonaj następujące kroki toocancel wykonywanym zadaniem hello.</span><span class="sxs-lookup"><span data-stu-id="30e3b-137">Perform hello following steps toocancel a running job.</span></span>

### <a name="toocancel-a-job"></a><span data-ttu-id="30e3b-138">toocancel zadania</span><span class="sxs-lookup"><span data-stu-id="30e3b-138">toocancel a job</span></span>
1. <span data-ttu-id="30e3b-139">Na powitania **zadania** strony, wyświetlania zadań uruchomionych hello mają toocancel, uruchamiając zapytanie o odpowiednie filtry.</span><span class="sxs-lookup"><span data-stu-id="30e3b-139">On hello **Jobs** page, display hello running job(s) that you want toocancel by running a query with appropriate filters.</span></span>
2. <span data-ttu-id="30e3b-140">Wybierz zadanie hello.</span><span class="sxs-lookup"><span data-stu-id="30e3b-140">Select hello job.</span></span>
3. <span data-ttu-id="30e3b-141">U dołu hello hello strony, kliknij przycisk **anulować**.</span><span class="sxs-lookup"><span data-stu-id="30e3b-141">At hello bottom of hello page, click **Cancel**.</span></span>
4. <span data-ttu-id="30e3b-142">Po wyświetleniu monitu o potwierdzenie kliknij przycisk **Tak**.</span><span class="sxs-lookup"><span data-stu-id="30e3b-142">When prompted for confirmation, click **Yes**.</span></span>

<span data-ttu-id="30e3b-143">To zadanie jest teraz anulowane.</span><span class="sxs-lookup"><span data-stu-id="30e3b-143">This job is now canceled.</span></span>

## <a name="next-steps"></a><span data-ttu-id="30e3b-144">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="30e3b-144">Next steps</span></span>
* <span data-ttu-id="30e3b-145">Dowiedz się, jak za[Zarządzanie zasadami tworzenia kopii zapasowej StorSimple](storsimple-manage-backup-policies.md).</span><span class="sxs-lookup"><span data-stu-id="30e3b-145">Learn how too[manage your StorSimple backup policies](storsimple-manage-backup-policies.md).</span></span>
* <span data-ttu-id="30e3b-146">Dowiedz się, jak za[Użyj hello tooadminister usługi Menedżer StorSimple, urządzenia StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="30e3b-146">Learn how too[use hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

