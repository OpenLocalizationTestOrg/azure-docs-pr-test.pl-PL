---
title: "Wyświetl zadania i zarządzać nimi tablicy wirtualnego StorSimple | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano na stronie zadań usługi Menedżer StorSimple urządzenia i jak z niego korzystać, aby śledzić najnowsze i bieżącego zadania dla tablicy wirtualnego StorSimple."
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
ms.openlocfilehash: 3fd1c262a8ce94d8e98f2b066a8028d974b15b1d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-device-manager-service-to-view-jobs-for-the-storsimple-virtual-array"></a><span data-ttu-id="6d5d8-103">Użyj usługi Menedżer StorSimple urządzenia do wyświetlania zadań dla tablicy wirtualnego StorSimple</span><span class="sxs-lookup"><span data-stu-id="6d5d8-103">Use the StorSimple Device Manager service to view jobs for the StorSimple Virtual Array</span></span>
## <a name="overview"></a><span data-ttu-id="6d5d8-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="6d5d8-104">Overview</span></span>
<span data-ttu-id="6d5d8-105">**Zadania** bloku udostępnia pojedynczy portal centralnej do przeglądania i zarządzania zadaniami, które są uruchamiane w tablicach wirtualnych, które są połączone z usługą Menedżera urządzeń StorSimple.</span><span class="sxs-lookup"><span data-stu-id="6d5d8-105">The **Jobs** blade provides a single central portal for viewing and managing jobs that are started on virtual arrays that are connected to your StorSimple Device Manager service.</span></span> <span data-ttu-id="6d5d8-106">Możesz wyświetlić zadania uruchomione, została zakończona i nie powiodło się dla wielu urządzeń wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="6d5d8-106">You can view running, completed, and failed jobs for multiple virtual devices.</span></span> <span data-ttu-id="6d5d8-107">Wyniki są prezentowane w formie tabeli.</span><span class="sxs-lookup"><span data-stu-id="6d5d8-107">Results are presented in a tabular format.</span></span>

![Bloku zadań](./media/storsimple-virtual-array-manage-jobs/ova-jobs-blade.png)

<span data-ttu-id="6d5d8-109">Można szybko znaleźć zadania, które są zainteresowani przez filtrowanie w polach, takich jak:</span><span class="sxs-lookup"><span data-stu-id="6d5d8-109">You can quickly find the jobs you are interested in by filtering on fields such as:</span></span>

* <span data-ttu-id="6d5d8-110">**Zakres czasu** — zadania mogą być filtrowane w oparciu o zakres dat i godzin.</span><span class="sxs-lookup"><span data-stu-id="6d5d8-110">**Time range** – Jobs can be filtered based on the date and time range.</span></span>
* <span data-ttu-id="6d5d8-111">**Urządzenia** — zadań są inicjowane na określonym urządzeniu połączona z usługą.</span><span class="sxs-lookup"><span data-stu-id="6d5d8-111">**Devices** – Jobs are initiated on a specific device connected to your service.</span></span> <span data-ttu-id="6d5d8-112">Odfiltrowanych zadań następnie wyszczególniono w oparciu o następujące atrybuty:</span><span class="sxs-lookup"><span data-stu-id="6d5d8-112">The filtered jobs are then tabulated based on the following attributes:</span></span>
  
  * <span data-ttu-id="6d5d8-113">**Nazwa** — Nazwa zadania może być **wszystkie**, **kopii zapasowej**, **klonowania**, **awaryjnie**, **pobieranie aktualizacji**, lub **instalowania aktualizacji**.</span><span class="sxs-lookup"><span data-stu-id="6d5d8-113">**Name** – The job name can be **All**, **Backup**, **Clone**, **Fail over**, **Download updates**, or **Install updates**.</span></span>
  * <span data-ttu-id="6d5d8-114">**Stan** — zadania mogą być **wszystkie**, **w toku**, **zakończyło się pomyślnie**, lub ****, lub **anulowane**.</span><span class="sxs-lookup"><span data-stu-id="6d5d8-114">**Status** – Jobs can be **All**, **In progress**, **Succeeded**, or **Failed**, or **Canceled**.</span></span>
  * <span data-ttu-id="6d5d8-115">**Jednostka** — zadania może być skojarzony z woluminu, udziału lub urządzenia.</span><span class="sxs-lookup"><span data-stu-id="6d5d8-115">**Entity** – The jobs can be associated with a volume, share, or device.</span></span>
  * <span data-ttu-id="6d5d8-116">**Urządzenie** — nazwa urządzenia, na którym zadanie zostało uruchomione.</span><span class="sxs-lookup"><span data-stu-id="6d5d8-116">**Device** – The name of the device on which the job was started.</span></span>
  * <span data-ttu-id="6d5d8-117">**Rozpoczęto w** — czas uruchomienia zadania.</span><span class="sxs-lookup"><span data-stu-id="6d5d8-117">**Started on** – The time when the job was started.</span></span>
  * <span data-ttu-id="6d5d8-118">**Czas trwania** — czas trwania na zostało uruchomione zadanie.</span><span class="sxs-lookup"><span data-stu-id="6d5d8-118">**Duration** – The duration for on which the job was run.</span></span>
* <span data-ttu-id="6d5d8-119">**Stan** — możesz wyszukać wszystkie zadania uruchomione, zakończone lub nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="6d5d8-119">**Status** – You can search for all, running, completed, or failed jobs.</span></span>
* <span data-ttu-id="6d5d8-120">**Typ zadania** — typ zadania mogą być wszystkie, tworzenia kopii zapasowych, przywracania, trybu failover, Pobierz aktualizacje lub instalowania aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="6d5d8-120">**Job type** – The job type can be all, backup, restore, failover, download updates, or install updates.</span></span>

<span data-ttu-id="6d5d8-121">Lista zadań są odświeżane co 30 sekund.</span><span class="sxs-lookup"><span data-stu-id="6d5d8-121">The list of jobs is refreshed every 30 seconds.</span></span>

## <a name="view-job-details"></a><span data-ttu-id="6d5d8-122">Wyświetl szczegóły zadania</span><span class="sxs-lookup"><span data-stu-id="6d5d8-122">View job details</span></span>
<span data-ttu-id="6d5d8-123">Wykonaj poniższe kroki, aby wyświetlić szczegóły wszystkie zadania.</span><span class="sxs-lookup"><span data-stu-id="6d5d8-123">Perform the following steps to view the details of any job.</span></span>

#### <a name="to-view-job-details"></a><span data-ttu-id="6d5d8-124">Aby wyświetlić szczegóły zadania</span><span class="sxs-lookup"><span data-stu-id="6d5d8-124">To view job details</span></span>
1. <span data-ttu-id="6d5d8-125">Na **zadania** bloku wyświetlania zadań są zainteresowani, uruchamiając zapytanie o odpowiednie filtry.</span><span class="sxs-lookup"><span data-stu-id="6d5d8-125">On the **Jobs** blade, display the job(s) you are interested in by running a query with appropriate filters.</span></span> <span data-ttu-id="6d5d8-126">Można wyszukiwać zadania zakończone lub nie działają.</span><span class="sxs-lookup"><span data-stu-id="6d5d8-126">You can search for completed or running jobs.</span></span>
2. <span data-ttu-id="6d5d8-127">Wybierz zadanie z tabelarycznej listę zadań.</span><span class="sxs-lookup"><span data-stu-id="6d5d8-127">Select a job from the tabular list of jobs.</span></span>
   
    ![Blok zadania](./media/storsimple-virtual-array-manage-jobs/ova-jobs-blade.png)
3. <span data-ttu-id="6d5d8-129">W dolnej części strony kliknij **szczegóły**.</span><span class="sxs-lookup"><span data-stu-id="6d5d8-129">At the bottom of the page, click **Details**.</span></span>
4. <span data-ttu-id="6d5d8-130">W **szczegóły** okno dialogowe, można wyświetlić stan, szczegóły i statystyk czasu.</span><span class="sxs-lookup"><span data-stu-id="6d5d8-130">In the **Details** dialog box, you can view status, details, and time statistics.</span></span> <span data-ttu-id="6d5d8-131">Na poniższej ilustracji przedstawiono przykład **szczegóły zadania tworzenia kopii zapasowej** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="6d5d8-131">The following illustration shows an example of the **Backup Job Details** dialog box.</span></span>
   
    ![Szczegóły zadania](./media/storsimple-virtual-array-manage-jobs/ova-jobs-details.png)

#### <a name="job-failures-when-the-virtual-machine-is-paused-in-the-hypervisor"></a><span data-ttu-id="6d5d8-133">Błędy zadań, gdy maszyna wirtualna jest wstrzymana w funkcji hypervisor</span><span class="sxs-lookup"><span data-stu-id="6d5d8-133">Job failures when the virtual machine is paused in the hypervisor</span></span>
<span data-ttu-id="6d5d8-134">Gdy zadanie jest w postępu tablica wirtualnego StorSimple oraz urządzenia (udostępnione w funkcji hypervisor, maszyna wirtualna) jest wstrzymana na więcej niż 15 minut, zadanie nie powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="6d5d8-134">When a job is in progress on your StorSimple Virtual Array and the device (virtual machine provisioned in hypervisor) is paused for greater than 15 minutes, the job fails.</span></span> <span data-ttu-id="6d5d8-135">To jest z powodu czasu tablicy wirtualnego StorSimple są zsynchronizowane z czasem Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="6d5d8-135">This is due to your StorSimple Virtual Array time being out of sync with the Microsoft Azure time.</span></span> 

<span data-ttu-id="6d5d8-136">Zostanie wyświetlony następujący błąd: "Godzina na urządzeniu jest zsynchronizowany z czasem Microsoft Azure przez ponad 15 minut.</span><span class="sxs-lookup"><span data-stu-id="6d5d8-136">You will see the following error: "Your device time is out of sync with the Microsoft Azure time by more than 15 minutes.</span></span> <span data-ttu-id="6d5d8-137">Sprawdź, czy funkcja hypervisor i urządzenie, które czasy są zsynchronizowane z serwer NTP.</span><span class="sxs-lookup"><span data-stu-id="6d5d8-137">Ensure that the hypervisor and the device times are synchronized with an NTP servier.</span></span> <span data-ttu-id="6d5d8-138">Sprawdź, czy nie ma żadnych problemów łączności.</span><span class="sxs-lookup"><span data-stu-id="6d5d8-138">Verify that there are no connectivity issues.</span></span> <span data-ttu-id="6d5d8-139">Aby rozwiązać problemy z łącznością, uruchom testów diagnostycznych z lokalnej sieci web interfejsu użytkownika z urządzeniem wirtualnym."</span><span class="sxs-lookup"><span data-stu-id="6d5d8-139">To troubleshoot connectivity issues, run diagnostic tests from the local web UI of your virtual device."</span></span>

<span data-ttu-id="6d5d8-140">Błędy te dotyczą zadań kopii zapasowych, przywracania, aktualizacji i pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="6d5d8-140">These failures apply to backup, restore, update, and failover jobs.</span></span> <span data-ttu-id="6d5d8-141">Jeśli zainicjowaniu obsługi maszyny wirtualnej w funkcji Hyper-V, maszyny ostatecznie synchronizuje czas z funkcji hypervisor.</span><span class="sxs-lookup"><span data-stu-id="6d5d8-141">If your virtual machine is provisioned in Hyper-V, the machine eventually synchronizes time with your hypervisor.</span></span> <span data-ttu-id="6d5d8-142">Gdy tak się stanie, można ponownie uruchomić zadanie.</span><span class="sxs-lookup"><span data-stu-id="6d5d8-142">Once that happens, you can restart your job.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6d5d8-143">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6d5d8-143">Next steps</span></span>
<span data-ttu-id="6d5d8-144">[Dowiedz się, jak używać lokalnego interfejsu użytkownika sieci web do administrowania tablica wirtualnego StorSimple](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="6d5d8-144">[Learn how to use the local web UI to administer your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

