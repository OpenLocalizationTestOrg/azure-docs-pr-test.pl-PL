---
title: "aaaView StorSimple zadania i zarządzać nimi | Dokumentacja firmy Microsoft"
description: "Zawiera opis strony zadania usługi Menedżer StorSimple hello i w jaki sposób toouse on tootrack ostatnie, bieżących i zaplanowanych zadań tworzenia kopii zapasowej."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: cdd3e9e8-7ccd-40a3-8c07-0ab1338c0e59
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: d6ecdcbc3d8a4757c2328303f268e51c8ce26b65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-tooview-and-manage-storsimple-jobs-update-2"></a><span data-ttu-id="ccc4c-103">Użyj tooview usługi Menedżer StorSimple hello zadania i zarządzać nimi StorSimple (aktualizacja Update 2)</span><span class="sxs-lookup"><span data-stu-id="ccc4c-103">Use hello StorSimple Manager service tooview and manage StorSimple jobs (Update 2)</span></span>
[!INCLUDE [storsimple-version-selector-manage-jobs](../../includes/storsimple-version-selector-manage-jobs.md)]

## <a name="overview"></a><span data-ttu-id="ccc4c-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="ccc4c-104">Overview</span></span>
<span data-ttu-id="ccc4c-105">Witaj **zadania** strona zawiera pojedynczy portalu centralnej do przeglądania i zarządzania zadaniami, które zostały uruchomione na urządzeniach podłączony tooyour usługi Menedżer StorSimple.</span><span class="sxs-lookup"><span data-stu-id="ccc4c-105">hello **Jobs** page provides a single central portal for viewing and managing jobs that were started on devices connected tooyour StorSimple Manager service.</span></span> <span data-ttu-id="ccc4c-106">Można wyświetlić zadań zaplanowanych, uruchomionych, zakończone, anulowane i nie powiodło się dla wielu urządzeń.</span><span class="sxs-lookup"><span data-stu-id="ccc4c-106">You can view scheduled, running, completed, canceled, and failed jobs for multiple devices.</span></span> <span data-ttu-id="ccc4c-107">Wyniki są prezentowane w formie tabeli.</span><span class="sxs-lookup"><span data-stu-id="ccc4c-107">Results are presented in a tabular format.</span></span> 

![Strona zadania](./media/storsimple-manage-jobs-u2/jobs.png)

<span data-ttu-id="ccc4c-109">Można szybko znaleźć hello zadania, które są zainteresowani przez filtrowanie w polach, takich jak:</span><span class="sxs-lookup"><span data-stu-id="ccc4c-109">You can quickly find hello jobs you are interested in by filtering on fields such as:</span></span>

* <span data-ttu-id="ccc4c-110">**Stan** — zadania może być uruchomiony, zakończone, anulowane, nie powiodło się, anulowanie lub ukończone z błędami.</span><span class="sxs-lookup"><span data-stu-id="ccc4c-110">**Status** – Jobs can be running, completed, canceled, failed, canceling, or completed with errors.</span></span>
* <span data-ttu-id="ccc4c-111">**Od i do** — zadania mogą być filtrowane na podstawie hello zakres dat i godzin.</span><span class="sxs-lookup"><span data-stu-id="ccc4c-111">**From and To** – Jobs can be filtered based on hello date and time range.</span></span>
* <span data-ttu-id="ccc4c-112">**Typ** — typ zadania hello może być kopii zapasowej, ręcznego wykonywania kopii zapasowej, przywracania, klonowania, tryb failover urządzeń, tworzenia woluminu przypiętego lokalnie, zmodyfikować woluminu, aktualizowanie i obsługuje pakiet lub inicjowania obsługi urządzenia wirtualnego.</span><span class="sxs-lookup"><span data-stu-id="ccc4c-112">**Type** – hello job type can be backup, manual backup, restore, clone, device failover, create locally pinned volume, modify volume, update, support package, or virtual device provisioning.</span></span>
* <span data-ttu-id="ccc4c-113">**Urządzenia** — zadań są inicjowane na niektórych usługi tooyour podłączonych urządzeń.</span><span class="sxs-lookup"><span data-stu-id="ccc4c-113">**Devices** – Jobs are initiated on a certain device connected tooyour service.</span></span>
  <span data-ttu-id="ccc4c-114">Witaj odfiltrowanych zadań następnie wyszczególniono na podstawie hello hello następujące atrybuty:</span><span class="sxs-lookup"><span data-stu-id="ccc4c-114">hello filtered jobs are then tabulated on hello basis of hello following attributes:</span></span>
  
  * <span data-ttu-id="ccc4c-115">**Typ** — kopia zapasowa, ręcznego wykonywania kopii zapasowej, przywracania, klonowania, tryb failover urządzeń, tworzenia woluminu przypiętego lokalnie, zmodyfikować woluminu, aktualizowanie i obsługuje pakiet lub inicjowania obsługi urządzenia wirtualnego.</span><span class="sxs-lookup"><span data-stu-id="ccc4c-115">**Type** – backup, manual backup, restore, clone, device failover, create locally pinned volume, modify volume, update, support package, or virtual device provisioning.</span></span>
  * <span data-ttu-id="ccc4c-116">**Stan** — uruchomiona, zakończone, anulowane, nie powiodło się, anulowanie lub ukończone z błędami.</span><span class="sxs-lookup"><span data-stu-id="ccc4c-116">**Status** – running, completed, canceled, failed, canceling, or completed with errors.</span></span>
  * <span data-ttu-id="ccc4c-117">**Jednostka** — hello zadań można skojarzyć z woluminu, zasad tworzenia kopii zapasowej lub urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="ccc4c-117">**Entity** – hello jobs can be associated with a volume, a backup policy, or a device.</span></span> <span data-ttu-id="ccc4c-118">Na przykład zadanie klonowania jest skojarzony z woluminem, zaplanowane zadanie tworzenia kopii zapasowej jest skojarzone z zasadami tworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="ccc4c-118">For example, a clone job is associated with a volume, whereas a scheduled backup job is associated with a backup policy.</span></span> <span data-ttu-id="ccc4c-119">Zadania urządzenia jest tworzony w wyniku odzyskiwania awaryjnego (DR) lub operacji przywracania.</span><span class="sxs-lookup"><span data-stu-id="ccc4c-119">A device job is created as a result of a disaster recovery (DR) or a restore operation.</span></span>
  * <span data-ttu-id="ccc4c-120">**Urządzenie** — Witaj nazwa hello urządzenia, na którym hello zadanie zostało uruchomione.</span><span class="sxs-lookup"><span data-stu-id="ccc4c-120">**Device** – hello name of hello device on which hello job was started.</span></span>
  * <span data-ttu-id="ccc4c-121">**Rozpoczęto w** — Witaj czas uruchomienia zadania hello.</span><span class="sxs-lookup"><span data-stu-id="ccc4c-121">**Started on** – hello time when hello job was started.</span></span>
  * <span data-ttu-id="ccc4c-122">**Postęp** — Witaj procentu ukończenia uruchomionego zadania.</span><span class="sxs-lookup"><span data-stu-id="ccc4c-122">**Progress** – hello percentage completion of a running job.</span></span> <span data-ttu-id="ccc4c-123">Zadanie zostało ukończone, aby uzyskać to zawsze być 100%.</span><span class="sxs-lookup"><span data-stu-id="ccc4c-123">For a completed job, this should always be 100%.</span></span>

<span data-ttu-id="ccc4c-124">Witaj listy zadań są odświeżane co 30 sekund.</span><span class="sxs-lookup"><span data-stu-id="ccc4c-124">hello list of jobs is refreshed every 30 seconds.</span></span>

<span data-ttu-id="ccc4c-125">Można wykonywać następujące zadania związane z akcji na tej stronie powitania:</span><span class="sxs-lookup"><span data-stu-id="ccc4c-125">You can perform hello following job-related actions on this page:</span></span>

* <span data-ttu-id="ccc4c-126">Wyświetlanie szczegółów zadania</span><span class="sxs-lookup"><span data-stu-id="ccc4c-126">View job details</span></span>
* <span data-ttu-id="ccc4c-127">Anulowanie zadania</span><span class="sxs-lookup"><span data-stu-id="ccc4c-127">Cancel a job</span></span>

## <a name="view-job-details"></a><span data-ttu-id="ccc4c-128">Wyświetlanie szczegółów zadania</span><span class="sxs-lookup"><span data-stu-id="ccc4c-128">View job details</span></span>
<span data-ttu-id="ccc4c-129">Wykonaj hello poniższe kroki tooview hello informacje wszystkie zadania.</span><span class="sxs-lookup"><span data-stu-id="ccc4c-129">Perform hello following steps tooview hello details of any job.</span></span>

#### <a name="tooview-job-details"></a><span data-ttu-id="ccc4c-130">Szczegóły zadania tooview</span><span class="sxs-lookup"><span data-stu-id="ccc4c-130">tooview job details</span></span>
1. <span data-ttu-id="ccc4c-131">Na powitania **zadania** strony, wyświetlania zadań hello są zainteresowani, uruchamiając zapytanie o odpowiednie filtry.</span><span class="sxs-lookup"><span data-stu-id="ccc4c-131">On hello **Jobs** page, display hello job(s) you are interested in by running a query with appropriate filters.</span></span> <span data-ttu-id="ccc4c-132">Można wyszukiwać ukończone, uruchomiona lub anulowane zadania.</span><span class="sxs-lookup"><span data-stu-id="ccc4c-132">You can search for completed, running, or canceled jobs.</span></span>
2. <span data-ttu-id="ccc4c-133">Wybierz zadanie.</span><span class="sxs-lookup"><span data-stu-id="ccc4c-133">Select a job.</span></span>
3. <span data-ttu-id="ccc4c-134">U dołu hello hello strony, kliknij przycisk **szczegóły**.</span><span class="sxs-lookup"><span data-stu-id="ccc4c-134">At hello bottom of hello page, click **Details**.</span></span>
4. <span data-ttu-id="ccc4c-135">W hello **szczegóły zadania tworzenia kopii zapasowej** okno dialogowe, można wyświetlić stan hello, szczegóły statystyk czasu i statystyki danych.</span><span class="sxs-lookup"><span data-stu-id="ccc4c-135">In hello **Backup Job Details** dialog box, you can view hello status, details, time statistics, and data statistics.</span></span>
   
    ![Strona szczegółów zadania](./media/storsimple-manage-jobs-u2/JobDetails.png)

## <a name="cancel-a-job"></a><span data-ttu-id="ccc4c-137">Anulowanie zadania</span><span class="sxs-lookup"><span data-stu-id="ccc4c-137">Cancel a job</span></span>
<span data-ttu-id="ccc4c-138">Wykonaj następujące kroki toocancel wykonywanym zadaniem hello.</span><span class="sxs-lookup"><span data-stu-id="ccc4c-138">Perform hello following steps toocancel a running job.</span></span>

> [!NOTE]
> <span data-ttu-id="ccc4c-139">Niektóre zadania, takie jak modyfikowanie woluminu toochange hello woluminie, którego typ lub rozszerzenie woluminu, nie można anulować.</span><span class="sxs-lookup"><span data-stu-id="ccc4c-139">Some jobs, such as modifying a volume toochange hello volume type or expanding a volume, cannot be canceled.</span></span>
> 
> 

### <a name="toocancel-a-job"></a><span data-ttu-id="ccc4c-140">toocancel zadania</span><span class="sxs-lookup"><span data-stu-id="ccc4c-140">toocancel a job</span></span>
1. <span data-ttu-id="ccc4c-141">Na powitania **zadania** strony, wyświetlania zadań uruchomionych hello mają toocancel, uruchamiając zapytanie o odpowiednie filtry.</span><span class="sxs-lookup"><span data-stu-id="ccc4c-141">On hello **Jobs** page, display hello running job(s) that you want toocancel by running a query with appropriate filters.</span></span>
2. <span data-ttu-id="ccc4c-142">Wybierz zadanie hello.</span><span class="sxs-lookup"><span data-stu-id="ccc4c-142">Select hello job.</span></span>
3. <span data-ttu-id="ccc4c-143">U dołu hello hello strony, kliknij przycisk **anulować**.</span><span class="sxs-lookup"><span data-stu-id="ccc4c-143">At hello bottom of hello page, click **Cancel**.</span></span>
4. <span data-ttu-id="ccc4c-144">Po wyświetleniu monitu o potwierdzenie kliknij przycisk **Tak**.</span><span class="sxs-lookup"><span data-stu-id="ccc4c-144">When prompted for confirmation, click **Yes**.</span></span>

<span data-ttu-id="ccc4c-145">To zadanie jest teraz anulowane.</span><span class="sxs-lookup"><span data-stu-id="ccc4c-145">This job is now canceled.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ccc4c-146">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ccc4c-146">Next steps</span></span>
* <span data-ttu-id="ccc4c-147">Dowiedz się, jak za[Zarządzanie zasadami tworzenia kopii zapasowej StorSimple](storsimple-manage-backup-policies.md).</span><span class="sxs-lookup"><span data-stu-id="ccc4c-147">Learn how too[manage your StorSimple backup policies](storsimple-manage-backup-policies.md).</span></span>
* <span data-ttu-id="ccc4c-148">Dowiedz się, jak za[Użyj hello tooadminister usługi Menedżer StorSimple, urządzenia StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="ccc4c-148">Learn how too[use hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

