---
title: "aaaView tablicy wirtualnego StorSimple zadania i zarządzać nimi | Dokumentacja firmy Microsoft"
description: "Zawiera opis strony zadania usługi Menedżer StorSimple urządzenia hello i w jaki sposób toouse go tootrack ostatnie i bieżącego zadania dla hello tablicy wirtualne StorSimple."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 31879821-b599-4609-a7f4-d4b0f658a933
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 11/11/2016
ms.author: alkohli
ms.openlocfilehash: cf3f3e7bcdfff0ff2328b7354db2482286800e93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-tooview-jobs-for-hello-storsimple-virtual-array"></a><span data-ttu-id="eac9e-103">Zadania tooview usługi Menedżer StorSimple urządzenia hello na użytek hello tablicy wirtualnego StorSimple</span><span class="sxs-lookup"><span data-stu-id="eac9e-103">Use hello StorSimple Device Manager service tooview jobs for hello StorSimple Virtual Array</span></span>
## <a name="overview"></a><span data-ttu-id="eac9e-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="eac9e-104">Overview</span></span>
<span data-ttu-id="eac9e-105">Witaj **zadania** bloku udostępnia pojedynczy portal centralnej do przeglądania i zarządzania zadaniami, które są uruchamiane w tablicach wirtualnych, które są połączone tooyour usługi Menedżer StorSimple urządzenia.</span><span class="sxs-lookup"><span data-stu-id="eac9e-105">hello **Jobs** blade provides a single central portal for viewing and managing jobs that are started on virtual arrays that are connected tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="eac9e-106">Możesz wyświetlić zadania uruchomione, została zakończona i nie powiodło się dla wielu urządzeń wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="eac9e-106">You can view running, completed, and failed jobs for multiple virtual devices.</span></span> <span data-ttu-id="eac9e-107">Wyniki są prezentowane w formie tabeli.</span><span class="sxs-lookup"><span data-stu-id="eac9e-107">Results are presented in a tabular format.</span></span>

![Bloku zadań](./media/storsimple-virtual-array-manage-jobs/ova-jobs-blade.png)

<span data-ttu-id="eac9e-109">Można szybko znaleźć hello zadania, które są zainteresowani przez filtrowanie w polach, takich jak:</span><span class="sxs-lookup"><span data-stu-id="eac9e-109">You can quickly find hello jobs you are interested in by filtering on fields such as:</span></span>

* <span data-ttu-id="eac9e-110">**Zakres czasu** — zadania mogą być filtrowane na podstawie hello zakres dat i godzin.</span><span class="sxs-lookup"><span data-stu-id="eac9e-110">**Time range** – Jobs can be filtered based on hello date and time range.</span></span>
* <span data-ttu-id="eac9e-111">**Urządzenia** — zadań są inicjowane w usłudze tooyour określonego urządzenia połączone.</span><span class="sxs-lookup"><span data-stu-id="eac9e-111">**Devices** – Jobs are initiated on a specific device connected tooyour service.</span></span> <span data-ttu-id="eac9e-112">Witaj odfiltrowanych zadań następnie wyszczególniono w oparciu hello następujące atrybuty:</span><span class="sxs-lookup"><span data-stu-id="eac9e-112">hello filtered jobs are then tabulated based on hello following attributes:</span></span>
  
  * <span data-ttu-id="eac9e-113">**Nazwa** — Nazwa zadania hello może być **wszystkie**, **kopii zapasowej**, **klonowania**, **awaryjnie**, **pobierania aktualizacji** , lub **instalowania aktualizacji**.</span><span class="sxs-lookup"><span data-stu-id="eac9e-113">**Name** – hello job name can be **All**, **Backup**, **Clone**, **Fail over**, **Download updates**, or **Install updates**.</span></span>
  * <span data-ttu-id="eac9e-114">**Stan** — zadania mogą być **wszystkie**, **w toku**, **zakończyło się pomyślnie**, lub ****, lub **anulowane**.</span><span class="sxs-lookup"><span data-stu-id="eac9e-114">**Status** – Jobs can be **All**, **In progress**, **Succeeded**, or **Failed**, or **Canceled**.</span></span>
  * <span data-ttu-id="eac9e-115">**Jednostka** — Witaj zadań można skojarzyć z woluminu, udziału lub urządzenia.</span><span class="sxs-lookup"><span data-stu-id="eac9e-115">**Entity** – hello jobs can be associated with a volume, share, or device.</span></span>
  * <span data-ttu-id="eac9e-116">**Urządzenie** — Witaj nazwa hello urządzenia, na którym hello zadanie zostało uruchomione.</span><span class="sxs-lookup"><span data-stu-id="eac9e-116">**Device** – hello name of hello device on which hello job was started.</span></span>
  * <span data-ttu-id="eac9e-117">**Rozpoczęto w** — Witaj czas uruchomienia zadania hello.</span><span class="sxs-lookup"><span data-stu-id="eac9e-117">**Started on** – hello time when hello job was started.</span></span>
  * <span data-ttu-id="eac9e-118">**Czas trwania** — Witaj czas trwania na zadanie (job) hello zostało uruchomione.</span><span class="sxs-lookup"><span data-stu-id="eac9e-118">**Duration** – hello duration for on which hello job was run.</span></span>
* <span data-ttu-id="eac9e-119">**Stan** — możesz wyszukać wszystkie zadania uruchomione, zakończone lub nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="eac9e-119">**Status** – You can search for all, running, completed, or failed jobs.</span></span>
* <span data-ttu-id="eac9e-120">**Typ zadania** — typ zadania hello mogą być wszystkie, tworzenia kopii zapasowych, przywracania, trybu failover, Pobierz aktualizacje lub instalowania aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="eac9e-120">**Job type** – hello job type can be all, backup, restore, failover, download updates, or install updates.</span></span>

<span data-ttu-id="eac9e-121">Witaj listy zadań są odświeżane co 30 sekund.</span><span class="sxs-lookup"><span data-stu-id="eac9e-121">hello list of jobs is refreshed every 30 seconds.</span></span>

## <a name="view-job-details"></a><span data-ttu-id="eac9e-122">Wyświetlanie szczegółów zadania</span><span class="sxs-lookup"><span data-stu-id="eac9e-122">View job details</span></span>
<span data-ttu-id="eac9e-123">Wykonaj hello poniższe kroki tooview hello informacje wszystkie zadania.</span><span class="sxs-lookup"><span data-stu-id="eac9e-123">Perform hello following steps tooview hello details of any job.</span></span>

#### <a name="tooview-job-details"></a><span data-ttu-id="eac9e-124">Szczegóły zadania tooview</span><span class="sxs-lookup"><span data-stu-id="eac9e-124">tooview job details</span></span>
1. <span data-ttu-id="eac9e-125">Na powitania **zadania** bloku, wyświetlania zadań hello są zainteresowani, uruchamiając zapytanie o odpowiednie filtry.</span><span class="sxs-lookup"><span data-stu-id="eac9e-125">On hello **Jobs** blade, display hello job(s) you are interested in by running a query with appropriate filters.</span></span> <span data-ttu-id="eac9e-126">Można wyszukiwać zadania zakończone lub nie działają.</span><span class="sxs-lookup"><span data-stu-id="eac9e-126">You can search for completed or running jobs.</span></span>
2. <span data-ttu-id="eac9e-127">Wybierz zadanie z hello tabelarycznej listę zadań.</span><span class="sxs-lookup"><span data-stu-id="eac9e-127">Select a job from hello tabular list of jobs.</span></span>
   
    ![Blok zadania](./media/storsimple-virtual-array-manage-jobs/ova-jobs-blade.png)
3. <span data-ttu-id="eac9e-129">U dołu hello hello strony, kliknij przycisk **szczegóły**.</span><span class="sxs-lookup"><span data-stu-id="eac9e-129">At hello bottom of hello page, click **Details**.</span></span>
4. <span data-ttu-id="eac9e-130">W hello **szczegóły** okno dialogowe, można wyświetlić stan, szczegóły i statystyk czasu.</span><span class="sxs-lookup"><span data-stu-id="eac9e-130">In hello **Details** dialog box, you can view status, details, and time statistics.</span></span> <span data-ttu-id="eac9e-131">Witaj poniższej ilustracji przedstawiono przykład hello **szczegóły zadania tworzenia kopii zapasowej** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="eac9e-131">hello following illustration shows an example of hello **Backup Job Details** dialog box.</span></span>
   
    ![Szczegóły zadania](./media/storsimple-virtual-array-manage-jobs/ova-jobs-details.png)

#### <a name="job-failures-when-hello-virtual-machine-is-paused-in-hello-hypervisor"></a><span data-ttu-id="eac9e-133">Wykonanie zadań po hello maszyna wirtualna jest wstrzymana w funkcji hypervisor hello</span><span class="sxs-lookup"><span data-stu-id="eac9e-133">Job failures when hello virtual machine is paused in hello hypervisor</span></span>
<span data-ttu-id="eac9e-134">Gdy zadanie jest w postęp na tablicy wirtualnego StorSimple i hello urządzenia (udostępniane w ramach funkcji hypervisor maszyny wirtualnej) jest wstrzymana na więcej niż 15 minut, zadanie hello zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="eac9e-134">When a job is in progress on your StorSimple Virtual Array and hello device (virtual machine provisioned in hypervisor) is paused for greater than 15 minutes, hello job fails.</span></span> <span data-ttu-id="eac9e-135">To jest powodu tooyour tablicy wirtualnego StorSimple czasu są zsynchronizowane z czasem Microsoft Azure hello.</span><span class="sxs-lookup"><span data-stu-id="eac9e-135">This is due tooyour StorSimple Virtual Array time being out of sync with hello Microsoft Azure time.</span></span> 

<span data-ttu-id="eac9e-136">Zobaczysz hello następujący błąd: "Godzina na urządzeniu jest zsynchronizowany z czasem Microsoft Azure hello przez ponad 15 minut.</span><span class="sxs-lookup"><span data-stu-id="eac9e-136">You will see hello following error: "Your device time is out of sync with hello Microsoft Azure time by more than 15 minutes.</span></span> <span data-ttu-id="eac9e-137">Upewnij się, że hello funkcji hypervisor i hello godzin urządzenia są synchronizowane z serwer NTP.</span><span class="sxs-lookup"><span data-stu-id="eac9e-137">Ensure that hello hypervisor and hello device times are synchronized with an NTP servier.</span></span> <span data-ttu-id="eac9e-138">Sprawdź, czy nie ma żadnych problemów łączności.</span><span class="sxs-lookup"><span data-stu-id="eac9e-138">Verify that there are no connectivity issues.</span></span> <span data-ttu-id="eac9e-139">problemy z łącznością tootroubleshoot, uruchamiania testów diagnostycznych z lokalne powitania interfejsu użytkownika urządzenia wirtualnego sieci web."</span><span class="sxs-lookup"><span data-stu-id="eac9e-139">tootroubleshoot connectivity issues, run diagnostic tests from hello local web UI of your virtual device."</span></span>

<span data-ttu-id="eac9e-140">Te błędy się zadania toobackup, przywracania, aktualizacji i pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="eac9e-140">These failures apply toobackup, restore, update, and failover jobs.</span></span> <span data-ttu-id="eac9e-141">Maszyny wirtualnej jest obsługiwana w funkcji Hyper-V, maszyny hello ostatecznie synchronizuje czas z Twojej funkcji hypervisor.</span><span class="sxs-lookup"><span data-stu-id="eac9e-141">If your virtual machine is provisioned in Hyper-V, hello machine eventually synchronizes time with your hypervisor.</span></span> <span data-ttu-id="eac9e-142">Gdy tak się stanie, można ponownie uruchomić zadanie.</span><span class="sxs-lookup"><span data-stu-id="eac9e-142">Once that happens, you can restart your job.</span></span>

## <a name="next-steps"></a><span data-ttu-id="eac9e-143">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="eac9e-143">Next steps</span></span>
<span data-ttu-id="eac9e-144">[Dowiedz się, jak toouse hello tooadminister interfejsu użytkownika sieci web lokalnego tablica wirtualnego StorSimple](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="eac9e-144">[Learn how toouse hello local web UI tooadminister your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

