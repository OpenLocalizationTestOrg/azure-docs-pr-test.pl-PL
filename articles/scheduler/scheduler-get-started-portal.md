---
title: aaaGet wprowadzenie Harmonogram systemu Azure w portalu Azure | Dokumentacja firmy Microsoft
description: "Rozpoczynanie pracy z usługą Azure Scheduler w portalu Azure"
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: e69542ec-d10f-4f17-9b7a-2ee441ee7d68
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/10/2016
ms.author: deli
ms.openlocfilehash: 58255c0ad19da65932f8b1d36cb8fef1ff6e651b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-scheduler-in-azure-portal"></a><span data-ttu-id="6df14-103">Rozpoczynanie pracy z usługą Azure Scheduler w portalu Azure</span><span class="sxs-lookup"><span data-stu-id="6df14-103">Get started with Azure Scheduler in Azure portal</span></span>
<span data-ttu-id="6df14-104">Jest łatwy toocreate zaplanowane zadania w harmonogramie Azure.</span><span class="sxs-lookup"><span data-stu-id="6df14-104">It's easy toocreate scheduled jobs in Azure Scheduler.</span></span> <span data-ttu-id="6df14-105">W przypadku tego samouczka, dowiesz się, jak toocreate zadania.</span><span class="sxs-lookup"><span data-stu-id="6df14-105">In this tutorial, you'll learn how toocreate a job.</span></span> <span data-ttu-id="6df14-106">Są w nim zawarte także informacje na temat możliwości monitorowania oraz zarządzania, jakie oferuje usługa Scheduler.</span><span class="sxs-lookup"><span data-stu-id="6df14-106">You'll also learn Scheduler's monitoring and management capabilities.</span></span>

## <a name="create-a-job"></a><span data-ttu-id="6df14-107">Tworzenie zadania</span><span class="sxs-lookup"><span data-stu-id="6df14-107">Create a job</span></span>
1. <span data-ttu-id="6df14-108">Zaloguj się za[portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="6df14-108">Sign in too[Azure portal](https://portal.azure.com/).</span></span>  
2. <span data-ttu-id="6df14-109">Kliknij przycisk **+ nowy** > typ *harmonogramu* w polu wyszukiwania hello > Wybierz **harmonogramu** w wynikach > kliknij **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="6df14-109">Click **+New** > type *Scheduler* in hello search box >  select **Scheduler** in results > click **Create**.</span></span>
   
    ![][marketplace-create]
3. <span data-ttu-id="6df14-110">Utwórzmy zadanie, które spowoduje przesłanie żądania GET do witryny http://www.microsoft.com/.</span><span class="sxs-lookup"><span data-stu-id="6df14-110">Let’s create a job that simply hits http://www.microsoft.com/ with a GET request.</span></span> <span data-ttu-id="6df14-111">W hello **zadania harmonogramu** ekranu, wprowadź hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="6df14-111">In hello **Scheduler Job** screen, enter hello following information:</span></span>
   
   1. <span data-ttu-id="6df14-112">**Nazwa:** `getmicrosoft`</span><span class="sxs-lookup"><span data-stu-id="6df14-112">**Name:** `getmicrosoft`</span></span>  
   2. <span data-ttu-id="6df14-113">**Subskrypcja:** subskrypcja usługi Azure użytkownika</span><span class="sxs-lookup"><span data-stu-id="6df14-113">**Subscription:** Your Azure subscription</span></span>   
   3. <span data-ttu-id="6df14-114">**Kolekcja zadań:** wybierz istniejącą kolekcję zadań lub kliknij przycisk **Utwórz nową** > wprowadź nazwę.</span><span class="sxs-lookup"><span data-stu-id="6df14-114">**Job Collection:** Select an existing job collection, or click **Create New** > enter a name.</span></span>
4. <span data-ttu-id="6df14-115">Następnie w **ustawienia akcji**, zdefiniuj hello następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="6df14-115">Next, in **Action Settings**, define hello following values:</span></span>
   
   1. <span data-ttu-id="6df14-116">**Typ akcji:** ` HTTP`</span><span class="sxs-lookup"><span data-stu-id="6df14-116">**Action Type:** ` HTTP`</span></span>  
   2. <span data-ttu-id="6df14-117">**Metoda:** `GET`</span><span class="sxs-lookup"><span data-stu-id="6df14-117">**Method:** `GET`</span></span>  
   3. <span data-ttu-id="6df14-118">**Adres URL:** ` http://www.microsoft.com`</span><span class="sxs-lookup"><span data-stu-id="6df14-118">**URL:** ` http://www.microsoft.com`</span></span>  
      
      ![][action-settings]
5. <span data-ttu-id="6df14-119">Ostatnią czynnością jest zdefiniowanie harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="6df14-119">Finally, let's define a schedule.</span></span> <span data-ttu-id="6df14-120">Witaj zadania można określić jako zadanie wykonywane, ale umożliwia pobranie harmonogram cyklu:</span><span class="sxs-lookup"><span data-stu-id="6df14-120">hello job could be defined as a one-time job, but let’s pick a recurrence schedule:</span></span>
   
   1. <span data-ttu-id="6df14-121">**Cykl**: `Recurring`</span><span class="sxs-lookup"><span data-stu-id="6df14-121">**Recurrence**: `Recurring`</span></span>
   2. <span data-ttu-id="6df14-122">**Uruchom**: dzisiejsza data</span><span class="sxs-lookup"><span data-stu-id="6df14-122">**Start**: Today's date</span></span>
   3. <span data-ttu-id="6df14-123">**Powtarzaj co**: `12 Hours`</span><span class="sxs-lookup"><span data-stu-id="6df14-123">**Recur every**: `12 Hours`</span></span>
   4. <span data-ttu-id="6df14-124">**Zakończ**: dwa dni od dnia dzisiejszego</span><span class="sxs-lookup"><span data-stu-id="6df14-124">**End by**: Two days from today's date</span></span>  
      
      ![][recurrence-schedule]
6. <span data-ttu-id="6df14-125">Kliknij przycisk **Utwórz**</span><span class="sxs-lookup"><span data-stu-id="6df14-125">Click **Create**</span></span>

## <a name="manage-and-monitor-jobs"></a><span data-ttu-id="6df14-126">Zarządzanie i monitorowanie zadań</span><span class="sxs-lookup"><span data-stu-id="6df14-126">Manage and monitor jobs</span></span>
<span data-ttu-id="6df14-127">Po utworzeniu zadania zostanie wyświetlona hello pulpitu nawigacyjnego Azure głównego.</span><span class="sxs-lookup"><span data-stu-id="6df14-127">Once a job is created, it appears in hello main Azure dashboard.</span></span> <span data-ttu-id="6df14-128">Kliknij zadanie hello i nowy zostanie otwarte okno z hello następujące karty:</span><span class="sxs-lookup"><span data-stu-id="6df14-128">Click hello job and a new window opens with hello following tabs:</span></span>

1. <span data-ttu-id="6df14-129">Właściwości</span><span class="sxs-lookup"><span data-stu-id="6df14-129">Properties</span></span>  
2. <span data-ttu-id="6df14-130">Ustawienia akcji</span><span class="sxs-lookup"><span data-stu-id="6df14-130">Action Settings</span></span>  
3. <span data-ttu-id="6df14-131">Harmonogram</span><span class="sxs-lookup"><span data-stu-id="6df14-131">Schedule</span></span>  
4. <span data-ttu-id="6df14-132">Historia</span><span class="sxs-lookup"><span data-stu-id="6df14-132">History</span></span>
5. <span data-ttu-id="6df14-133">Użytkownicy</span><span class="sxs-lookup"><span data-stu-id="6df14-133">Users</span></span>
   
   ![][job-overview]

### <a name="properties"></a><span data-ttu-id="6df14-134">Właściwości</span><span class="sxs-lookup"><span data-stu-id="6df14-134">Properties</span></span>
<span data-ttu-id="6df14-135">Te właściwości tylko do odczytu opisują metadanych zarządzania hello hello harmonogram zadania.</span><span class="sxs-lookup"><span data-stu-id="6df14-135">These read-only properties describe hello management metadata for hello Scheduler job.</span></span>

   ![][job-properties]

### <a name="action-settings"></a><span data-ttu-id="6df14-136">Ustawienia akcji</span><span class="sxs-lookup"><span data-stu-id="6df14-136">Action settings</span></span>
<span data-ttu-id="6df14-137">Kliknięcie zadania w hello **zadania** ekran umożliwia tooconfigure zadania.</span><span class="sxs-lookup"><span data-stu-id="6df14-137">Clicking on a job in hello **Jobs** screen allows you tooconfigure that job.</span></span> <span data-ttu-id="6df14-138">Dzięki temu można skonfigurować ustawienia zaawansowane, jeśli nie możesz skonfigurować je w hello szybkie — tworzenie kreatora.</span><span class="sxs-lookup"><span data-stu-id="6df14-138">This lets you configure advanced settings, if you didn't configure them in hello quick-create wizard.</span></span>

<span data-ttu-id="6df14-139">Dla wszystkich typów akcji może zmienić zasady ponawiania hello i hello akcji błędu.</span><span class="sxs-lookup"><span data-stu-id="6df14-139">For all action types, you may change hello retry policy and hello error action.</span></span>

<span data-ttu-id="6df14-140">Dla typów akcji zadania HTTP i HTTPS mogą ulec zmianie tooany metody hello dozwolone zlecenie HTTP.</span><span class="sxs-lookup"><span data-stu-id="6df14-140">For HTTP and HTTPS job action types, you may change hello method tooany allowed HTTP verb.</span></span> <span data-ttu-id="6df14-141">Mogą również dodać, usunąć lub zmienić informacje uwierzytelniania podstawowego lub hello nagłówków.</span><span class="sxs-lookup"><span data-stu-id="6df14-141">You may also add, delete, or change hello headers and basic authentication information.</span></span>

<span data-ttu-id="6df14-142">Dla typów akcji kolejki magazynu możesz zmienić hello konta magazynu, nazwę kolejki tokenu sygnatury dostępu Współdzielonego i treść.</span><span class="sxs-lookup"><span data-stu-id="6df14-142">For storage queue action types, you may change hello storage account, queue name, SAS token, and body.</span></span>

<span data-ttu-id="6df14-143">Dla typów akcji magistrali usług możesz zmienić hello przestrzeni nazw, ścieżki tematu/kolejki, ustawienia uwierzytelniania, typem transportu, właściwości wiadomości i treści wiadomości.</span><span class="sxs-lookup"><span data-stu-id="6df14-143">For service bus action types, you may change hello namespace, topic/queue path, authentication settings, transport type, message properties, and message body.</span></span>

   ![][job-action-settings]

### <a name="schedule"></a><span data-ttu-id="6df14-144">Harmonogram</span><span class="sxs-lookup"><span data-stu-id="6df14-144">Schedule</span></span>
<span data-ttu-id="6df14-145">Dzięki temu można skonfigurować harmonogram hello, jeśli chcesz toochange hello harmonogram, który został utworzony w hello szybkie — tworzenie kreatora.</span><span class="sxs-lookup"><span data-stu-id="6df14-145">This lets you reconfigure hello schedule, if you'd like toochange hello schedule you created in hello quick-create wizard.</span></span>

<span data-ttu-id="6df14-146">Jest to toobuild możliwości [harmonogramy złożone i zaawansowane cyklu w zadanie](scheduler-advanced-complexity.md)</span><span class="sxs-lookup"><span data-stu-id="6df14-146">This is an opportunity toobuild [complex schedules and advanced recurrence in your job](scheduler-advanced-complexity.md)</span></span>

<span data-ttu-id="6df14-147">Możesz zmienić hello Data rozpoczęcia i czas, w przypadku harmonogramu powtarzającego i hello Data zakończenia i czasu (Jeśli zadanie hello jest cykliczny.)</span><span class="sxs-lookup"><span data-stu-id="6df14-147">You may change hello start date and time, recurrence schedule, and hello end date and time (if hello job is recurring.)</span></span>

   ![][job-schedule]

### <a name="history"></a><span data-ttu-id="6df14-148">Historia</span><span class="sxs-lookup"><span data-stu-id="6df14-148">History</span></span>
<span data-ttu-id="6df14-149">Witaj **historii** karcie są wyświetlane wybrane metryki dla każdego wykonania zadania w systemie hello hello wybranego zadania.</span><span class="sxs-lookup"><span data-stu-id="6df14-149">hello **History** tab displays selected metrics for every job execution in hello system for hello selected job.</span></span> <span data-ttu-id="6df14-150">Te metryki Podaj wartości w czasie rzeczywistym dotyczące kondycji hello użytkownika harmonogramu:</span><span class="sxs-lookup"><span data-stu-id="6df14-150">These metrics provide real-time values regarding hello health of your Scheduler:</span></span>

1. <span data-ttu-id="6df14-151">Stan</span><span class="sxs-lookup"><span data-stu-id="6df14-151">Status</span></span>  
2. <span data-ttu-id="6df14-152">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="6df14-152">Details</span></span>  
3. <span data-ttu-id="6df14-153">Liczba ponownych prób</span><span class="sxs-lookup"><span data-stu-id="6df14-153">Retry attempts</span></span>
4. <span data-ttu-id="6df14-154">Wystąpienie: 1., 2., 3. itp.</span><span class="sxs-lookup"><span data-stu-id="6df14-154">Occurrence: 1st, 2nd, 3rd, etc.</span></span>
5. <span data-ttu-id="6df14-155">Godzina rozpoczęcia wykonywania</span><span class="sxs-lookup"><span data-stu-id="6df14-155">Start time of execution</span></span>  
6. <span data-ttu-id="6df14-156">Godzina zakończenia wykonywania</span><span class="sxs-lookup"><span data-stu-id="6df14-156">End time of execution</span></span>
   
   ![][job-history]

<span data-ttu-id="6df14-157">Możesz kliknąć opcję wykonywania tooview jego **szczegóły historii**, tym hello całej odpowiedzi dla każdego wykonania.</span><span class="sxs-lookup"><span data-stu-id="6df14-157">You can click on a run tooview its **History Details**, including hello whole response for every execution.</span></span> <span data-ttu-id="6df14-158">To okno dialogowe umożliwia również toocopy hello odpowiedzi toohello Schowka.</span><span class="sxs-lookup"><span data-stu-id="6df14-158">This dialog box also allows you toocopy hello response toohello clipboard.</span></span>

   ![][job-history-details]

### <a name="users"></a><span data-ttu-id="6df14-159">Użytkownicy</span><span class="sxs-lookup"><span data-stu-id="6df14-159">Users</span></span>
<span data-ttu-id="6df14-160">Kontrola dostępu oparta na rolach (Role-Based Access Control, RBAC) na platformie Azure umożliwia precyzyjne zarządzanie dostępem dla usługi Azure Scheduler.</span><span class="sxs-lookup"><span data-stu-id="6df14-160">Azure Role-Based Access Control (RBAC) enables fine-grained access management for Azure Scheduler.</span></span> <span data-ttu-id="6df14-161">toolearn jak hello toouse kartę Użytkownicy, można znaleźć zbyt[kontroli dostępu](../active-directory/role-based-access-control-configure.md)</span><span class="sxs-lookup"><span data-stu-id="6df14-161">toolearn how toouse hello Users tab, refer too[Azure Role-Based Access Control](../active-directory/role-based-access-control-configure.md)</span></span>

## <a name="see-also"></a><span data-ttu-id="6df14-162">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="6df14-162">See also</span></span>
 [<span data-ttu-id="6df14-163">Co to jest usługa Scheduler?</span><span class="sxs-lookup"><span data-stu-id="6df14-163">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="6df14-164">Pojęcia i terminologia dotyczące usługi Scheduler oraz hierarchia jednostek</span><span class="sxs-lookup"><span data-stu-id="6df14-164">Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="6df14-165">Plany i rozliczenia w usłudze Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="6df14-165">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="6df14-166">Jak planuje toobuild złożone i zaawansowane cyklu z Harmonogram systemu Azure</span><span class="sxs-lookup"><span data-stu-id="6df14-166">How toobuild complex schedules and advanced recurrence with Azure Scheduler</span></span>](scheduler-advanced-complexity.md)

 [<span data-ttu-id="6df14-167">Dokumentacja interfejsu API REST usługi Scheduler</span><span class="sxs-lookup"><span data-stu-id="6df14-167">Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="6df14-168">Dokumentacja poleceń cmdlet programu PowerShell dla usługi Scheduler</span><span class="sxs-lookup"><span data-stu-id="6df14-168">Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="6df14-169">Wysoka dostępność i niezawodność usługi Scheduler</span><span class="sxs-lookup"><span data-stu-id="6df14-169">Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="6df14-170">Limity, wartości domyślne i kody błędów usługi Scheduler</span><span class="sxs-lookup"><span data-stu-id="6df14-170">Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)

 [<span data-ttu-id="6df14-171">Uwierzytelnianie połączeń wychodzących usługi Scheduler</span><span class="sxs-lookup"><span data-stu-id="6df14-171">Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

[marketplace-create]: ./media/scheduler-get-started-portal/scheduler-v2-portal-marketplace-create.png
[action-settings]: ./media/scheduler-get-started-portal/scheduler-v2-portal-action-settings.png
[recurrence-schedule]: ./media/scheduler-get-started-portal/scheduler-v2-portal-recurrence-schedule.png
[job-properties]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-properties.png
[job-overview]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-overview-1.png
[job-action-settings]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-action-settings.png
[job-schedule]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-schedule.png
[job-history]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-history.png
[job-history-details]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-history-details.png


[1]: ./media/scheduler-get-started-portal/scheduler-get-started-portal001.png
[2]: ./media/scheduler-get-started-portal/scheduler-get-started-portal002.png
[3]: ./media/scheduler-get-started-portal/scheduler-get-started-portal003.png
[4]: ./media/scheduler-get-started-portal/scheduler-get-started-portal004.png
[5]: ./media/scheduler-get-started-portal/scheduler-get-started-portal005.png
[6]: ./media/scheduler-get-started-portal/scheduler-get-started-portal006.png
[7]: ./media/scheduler-get-started-portal/scheduler-get-started-portal007.png
[8]: ./media/scheduler-get-started-portal/scheduler-get-started-portal008.png
[9]: ./media/scheduler-get-started-portal/scheduler-get-started-portal009.png
[10]: ./media/scheduler-get-started-portal/scheduler-get-started-portal010.png
[11]: ./media/scheduler-get-started-portal/scheduler-get-started-portal011.png
[12]: ./media/scheduler-get-started-portal/scheduler-get-started-portal012.png
[13]: ./media/scheduler-get-started-portal/scheduler-get-started-portal013.png
[14]: ./media/scheduler-get-started-portal/scheduler-get-started-portal014.png
[15]: ./media/scheduler-get-started-portal/scheduler-get-started-portal015.png
