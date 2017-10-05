---
title: "Wyświetl zadania i zarządzać nimi StorSimple | Dokumentacja firmy Microsoft"
description: "Opis strony zadania usługi Menedżer StorSimple oraz używać go do śledzenia ostatnie, bieżących i zaplanowanych zadań tworzenia kopii zapasowej."
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
ms.openlocfilehash: 7d9377bb8f3cb8c587823c2d71d61dfb9b50f52f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-manager-service-to-view-and-manage-storsimple-jobs"></a><span data-ttu-id="63145-103">Użyj usługi Menedżer StorSimple, aby wyświetlić zadania i zarządzać nimi StorSimple</span><span class="sxs-lookup"><span data-stu-id="63145-103">Use the StorSimple Manager service to view and manage StorSimple jobs</span></span>
[!INCLUDE [storsimple-version-selector-manage-jobs](../../includes/storsimple-version-selector-manage-jobs.md)]

## <a name="overview"></a><span data-ttu-id="63145-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="63145-104">Overview</span></span>
<span data-ttu-id="63145-105">**Zadania** strony zapewnia jednym portalu centralnej do przeglądania i zarządzania zadaniami, które zostały uruchomione na urządzeniach połączona z usługą Menedżer StorSimple.</span><span class="sxs-lookup"><span data-stu-id="63145-105">The **Jobs** page provides a single central portal for viewing and managing jobs that were started on devices connected to your StorSimple Manager service.</span></span> <span data-ttu-id="63145-106">Można wyświetlić zadań zaplanowanych, uruchomionych, została zakończona i nie powiodło się dla wielu urządzeń.</span><span class="sxs-lookup"><span data-stu-id="63145-106">You can view scheduled, running, completed, and failed jobs for multiple devices.</span></span> <span data-ttu-id="63145-107">Wyniki są prezentowane w formie tabeli.</span><span class="sxs-lookup"><span data-stu-id="63145-107">Results are presented in a tabular format.</span></span> 

![Strona zadania](./media/storsimple-manage-jobs/HCS_JobsPage.png)

<span data-ttu-id="63145-109">Można szybko znaleźć zadania, które są zainteresowani przez filtrowanie w polach, takich jak:</span><span class="sxs-lookup"><span data-stu-id="63145-109">You can quickly find the jobs you are interested in by filtering on fields such as:</span></span>

* <span data-ttu-id="63145-110">**Stan** — zadania może być uruchomiony, zaplanowane, nie powiodło się, ukończonych, anulowanie lub anulowane.</span><span class="sxs-lookup"><span data-stu-id="63145-110">**Status** – Jobs can be running, scheduled, failed, completed, canceling, or canceled.</span></span>
* <span data-ttu-id="63145-111">**Typ** — zadania mogą być tworzone w wyniku zaplanowanego lub kopii zapasowej na żądanie (**wykonać kopii zapasowej**), klonowanie, przywracania urządzenia lub operacji aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="63145-111">**Type** – Jobs can be created as a result of a scheduled or an on-demand backup (**Take Backup**), cloning, a device restore, or an update operation.</span></span>
* <span data-ttu-id="63145-112">**Urządzenia** — zadań są inicjowane na niektórych urządzeniach połączona z usługą.</span><span class="sxs-lookup"><span data-stu-id="63145-112">**Devices** – Jobs are initiated on a certain device connected to your service.</span></span>
* <span data-ttu-id="63145-113">**Od i do** — zadania mogą być filtrowane w oparciu o zakres dat i godzin.</span><span class="sxs-lookup"><span data-stu-id="63145-113">**From and To** – Jobs can be filtered based on the date and time range.</span></span>

<span data-ttu-id="63145-114">Następnie wyszczególniono odfiltrowanych zadań na podstawie następujących atrybutów:</span><span class="sxs-lookup"><span data-stu-id="63145-114">The filtered jobs are then tabulated on the basis of the following attributes:</span></span>

* <span data-ttu-id="63145-115">**Typ** — kopii zapasowej, sklonowany, przywracania, pracy awaryjnej lub aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="63145-115">**Type** – Backup, clone, restore, failover, or update.</span></span>
* <span data-ttu-id="63145-116">**Stan** — uruchomiona, zaplanowane, nie powiodło się, ukończone, anulowanie lub anulowane.</span><span class="sxs-lookup"><span data-stu-id="63145-116">**Status** – Running, scheduled, failed, completed, canceling, or canceled.</span></span>
* <span data-ttu-id="63145-117">**Jednostka** — zadania może być skojarzony z woluminu, zasad tworzenia kopii zapasowej lub urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="63145-117">**Entity** – The jobs can be associated with a volume, a backup policy, or a device.</span></span> <span data-ttu-id="63145-118">Zadanie klonowania jest skojarzony z woluminem, zaplanowane zadanie tworzenia kopii zapasowej jest skojarzone z zasadami tworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="63145-118">A clone job is associated with a volume, whereas a scheduled backup job is associated with a backup policy.</span></span> <span data-ttu-id="63145-119">Zadania urządzenia jest tworzony w wyniku odzyskiwania awaryjnego (DR) lub operacji przywracania.</span><span class="sxs-lookup"><span data-stu-id="63145-119">A device job is created as a result of a disaster recovery (DR) or a restore operation.</span></span>
* <span data-ttu-id="63145-120">**Urządzenie** — nazwa urządzenia, na którym zadanie zostało uruchomione.</span><span class="sxs-lookup"><span data-stu-id="63145-120">**Device** – The name of the device on which the job was started.</span></span>
* <span data-ttu-id="63145-121">**Rozpoczęto na** — czas uruchomienia zadania.</span><span class="sxs-lookup"><span data-stu-id="63145-121">**Started On** – The time when the job was started.</span></span>
* <span data-ttu-id="63145-122">**Postęp** — zakończenia procent uruchomionego zadania.</span><span class="sxs-lookup"><span data-stu-id="63145-122">**Progress** – The percentage completion of a running job.</span></span> <span data-ttu-id="63145-123">Zadanie zostało ukończone, aby uzyskać to zawsze być 100%.</span><span class="sxs-lookup"><span data-stu-id="63145-123">For a completed job, this should always be 100%.</span></span>

<span data-ttu-id="63145-124">Lista zadań są odświeżane co 30 sekund.</span><span class="sxs-lookup"><span data-stu-id="63145-124">The list of jobs is refreshed every 30 seconds.</span></span>

<span data-ttu-id="63145-125">Na tej stronie można wykonywać następujące czynności związanych z pracą:</span><span class="sxs-lookup"><span data-stu-id="63145-125">You can perform the following job-related actions on this page:</span></span>

* <span data-ttu-id="63145-126">Wyświetl szczegóły zadania</span><span class="sxs-lookup"><span data-stu-id="63145-126">View job details</span></span>
* <span data-ttu-id="63145-127">Anulowanie zadania</span><span class="sxs-lookup"><span data-stu-id="63145-127">Cancel a job</span></span>

## <a name="view-job-details"></a><span data-ttu-id="63145-128">Wyświetl szczegóły zadania</span><span class="sxs-lookup"><span data-stu-id="63145-128">View job details</span></span>
<span data-ttu-id="63145-129">Wykonaj poniższe kroki, aby wyświetlić szczegóły wszystkie zadania.</span><span class="sxs-lookup"><span data-stu-id="63145-129">Perform the following steps to view the details of any job.</span></span>

#### <a name="to-view-job-details"></a><span data-ttu-id="63145-130">Aby wyświetlić szczegóły zadania</span><span class="sxs-lookup"><span data-stu-id="63145-130">To view job details</span></span>
1. <span data-ttu-id="63145-131">Na **zadania** strony, wyświetlania zadań są zainteresowani, uruchamiając zapytanie o odpowiednie filtry.</span><span class="sxs-lookup"><span data-stu-id="63145-131">On the **Jobs** page, display the job(s) you are interested in by running a query with appropriate filters.</span></span> <span data-ttu-id="63145-132">Można wyszukiwać ukończone, uruchomiona lub anulowane zadania.</span><span class="sxs-lookup"><span data-stu-id="63145-132">You can search for completed, running, or canceled jobs.</span></span>
2. <span data-ttu-id="63145-133">Wybierz zadanie.</span><span class="sxs-lookup"><span data-stu-id="63145-133">Select a job.</span></span>
3. <span data-ttu-id="63145-134">W dolnej części strony kliknij **szczegóły**.</span><span class="sxs-lookup"><span data-stu-id="63145-134">At the bottom of the page, click **Details**.</span></span>
4. <span data-ttu-id="63145-135">W **szczegóły zadania tworzenia kopii zapasowej** okno dialogowe, można wyświetlić stan, szczegóły, statystyk czasu i statystyki danych.</span><span class="sxs-lookup"><span data-stu-id="63145-135">In the **Backup Job Details** dialog box, you can view the status, details, time statistics, and data statistics.</span></span>

## <a name="cancel-a-job"></a><span data-ttu-id="63145-136">Anulowanie zadania</span><span class="sxs-lookup"><span data-stu-id="63145-136">Cancel a job</span></span>
<span data-ttu-id="63145-137">Wykonaj poniższe kroki, aby anulować zadanie uruchomione.</span><span class="sxs-lookup"><span data-stu-id="63145-137">Perform the following steps to cancel a running job.</span></span>

### <a name="to-cancel-a-job"></a><span data-ttu-id="63145-138">Aby anulować zadanie</span><span class="sxs-lookup"><span data-stu-id="63145-138">To cancel a job</span></span>
1. <span data-ttu-id="63145-139">Na **zadania** pozycję Wyświetl uruchomione zadania, które chcesz anulować, uruchamiając zapytanie z filtrami odpowiednie.</span><span class="sxs-lookup"><span data-stu-id="63145-139">On the **Jobs** page, display the running job(s) that you want to cancel by running a query with appropriate filters.</span></span>
2. <span data-ttu-id="63145-140">Wybierz zadanie.</span><span class="sxs-lookup"><span data-stu-id="63145-140">Select the job.</span></span>
3. <span data-ttu-id="63145-141">W dolnej części strony kliknij **anulować**.</span><span class="sxs-lookup"><span data-stu-id="63145-141">At the bottom of the page, click **Cancel**.</span></span>
4. <span data-ttu-id="63145-142">Po wyświetleniu monitu o potwierdzenie kliknij przycisk **Tak**.</span><span class="sxs-lookup"><span data-stu-id="63145-142">When prompted for confirmation, click **Yes**.</span></span>

<span data-ttu-id="63145-143">To zadanie jest teraz anulowane.</span><span class="sxs-lookup"><span data-stu-id="63145-143">This job is now canceled.</span></span>

## <a name="next-steps"></a><span data-ttu-id="63145-144">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="63145-144">Next steps</span></span>
* <span data-ttu-id="63145-145">Dowiedz się, jak [Zarządzanie zasadami tworzenia kopii zapasowej StorSimple](storsimple-manage-backup-policies.md).</span><span class="sxs-lookup"><span data-stu-id="63145-145">Learn how to [manage your StorSimple backup policies](storsimple-manage-backup-policies.md).</span></span>
* <span data-ttu-id="63145-146">Dowiedz się, jak [zarządzać urządzenia StorSimple przy użyciu usługi Menedżer StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="63145-146">Learn how to [use the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

