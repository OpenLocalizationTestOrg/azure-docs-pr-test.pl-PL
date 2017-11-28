---
title: "Harmonogram wysokiej dostępności i niezawodności"
description: "Harmonogram wysokiej dostępności i niezawodności"
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 5ec78e60-a9b9-405a-91a8-f010f3872d50
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/16/2016
ms.author: deli
ms.openlocfilehash: 7e7fe49de7814b6058468d630f8638720e5864f3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="scheduler-high-availability-and-reliability"></a><span data-ttu-id="cdd4e-103">Harmonogram wysokiej dostępności i niezawodności</span><span class="sxs-lookup"><span data-stu-id="cdd4e-103">Scheduler High-Availability and Reliability</span></span>
## <a name="azure-scheduler-high-availability"></a><span data-ttu-id="cdd4e-104">Harmonogram systemu Azure wysokiej dostępności</span><span class="sxs-lookup"><span data-stu-id="cdd4e-104">Azure Scheduler High-Availability</span></span>
<span data-ttu-id="cdd4e-105">Jako podstawowa usługi platformy Azure Harmonogram systemu Azure zapewnia wysoką dostępność i zawiera zarówno wdrożenia usługi geograficznie nadmiarowego i regionalnych geo zadania replikacji.</span><span class="sxs-lookup"><span data-stu-id="cdd4e-105">As a core Azure platform service, Azure Scheduler is highly available and features both geo-redundant service deployment and geo-regional job replication.</span></span>

### <a name="geo-redundant-service-deployment"></a><span data-ttu-id="cdd4e-106">Wdrożenie usługi geograficznie nadmiarowego</span><span class="sxs-lookup"><span data-stu-id="cdd4e-106">Geo-redundant service deployment</span></span>
<span data-ttu-id="cdd4e-107">Harmonogram systemu Azure jest dostępna za pośrednictwem interfejsu użytkownika w niemal każdego regionu geograficznego, który jest obecnie na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="cdd4e-107">Azure Scheduler is available via the UI in almost every geo region that's in Azure today.</span></span> <span data-ttu-id="cdd4e-108">Lista regionów, które Harmonogram systemu Azure jest dostępna w [wymienione w tym miejscu](https://azure.microsoft.com/regions/#services).</span><span class="sxs-lookup"><span data-stu-id="cdd4e-108">The list of regions that Azure Scheduler is available in is [listed here](https://azure.microsoft.com/regions/#services).</span></span> <span data-ttu-id="cdd4e-109">Jeśli centrum danych w regionie hostowanej staje się niedostępny, możliwości trybu failover Harmonogram systemu Azure są taki sposób, że usługa jest dostępna z innej centrum danych.</span><span class="sxs-lookup"><span data-stu-id="cdd4e-109">If a data center in a hosted region is rendered unavailable, the failover capabilities of Azure Scheduler are such that the service is available from another data center.</span></span>

### <a name="geo-regional-job-replication"></a><span data-ttu-id="cdd4e-110">Replikacja geograficzna regionalne zadania</span><span class="sxs-lookup"><span data-stu-id="cdd4e-110">Geo-regional job replication</span></span>
<span data-ttu-id="cdd4e-111">Nie tylko słowo frontonu, dostępne dla żądań zarządzania, ale własne stanowisko jest również replikacją geograficzną Harmonogram systemu Azure.</span><span class="sxs-lookup"><span data-stu-id="cdd4e-111">Not only is the Azure Scheduler front-end available for management requests, but your own job is also geo-replicated.</span></span> <span data-ttu-id="cdd4e-112">Przypadku wystąpienia awarii w jeden region, harmonogram Azure awaryjnie i zapewnia, że zadanie jest uruchamiane z innym centrum danych w parach regionu geograficznego.</span><span class="sxs-lookup"><span data-stu-id="cdd4e-112">When there’s an outage in one region, Azure Scheduler fails over and ensures that the job is run from another data center in the paired geographic region.</span></span>

<span data-ttu-id="cdd4e-113">Na przykład jeśli po utworzeniu zadania w południowo-środkowe stany Harmonogram systemu Azure automatycznie replikuje tego zadania w północno-środkowe Stany.</span><span class="sxs-lookup"><span data-stu-id="cdd4e-113">For example, if you’ve created a job in South Central US, Azure Scheduler automatically replicates that job in North Central US.</span></span> <span data-ttu-id="cdd4e-114">Jeśli wystąpi awaria w południowo-środkowe stany, harmonogram systemu Azure zapewnia, że zadanie jest uruchamiane z północno-środkowe Stany.</span><span class="sxs-lookup"><span data-stu-id="cdd4e-114">When there’s a failure in South Central US, Azure Scheduler ensures that the job is run from North Central US.</span></span> 

![][1]

<span data-ttu-id="cdd4e-115">W związku z tym harmonogram systemu Azure zapewnia, że danych pozostaje w tym samym regionie geograficznym szerszych w razie awarii usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="cdd4e-115">As a result, Azure Scheduler ensures that your data stays within the same broader geographic region in case of an Azure failure.</span></span> <span data-ttu-id="cdd4e-116">W związku z tym nie wymagają zduplikowane zadanie tak, aby dodać wysokiej dostępności — Harmonogram systemu Azure automatycznie zapewnia funkcje wysokiej dostępności dla zadań.</span><span class="sxs-lookup"><span data-stu-id="cdd4e-116">As a result, you need not duplicate your job just to add high availability – Azure Scheduler automatically provides high-availability capabilities for your jobs.</span></span>

## <a name="azure-scheduler-reliability"></a><span data-ttu-id="cdd4e-117">Niezawodność Harmonogram systemu Azure</span><span class="sxs-lookup"><span data-stu-id="cdd4e-117">Azure Scheduler Reliability</span></span>
<span data-ttu-id="cdd4e-118">Harmonogram systemu Azure gwarancje własne wysokiej dostępności i mają inne podejście do zadań utworzonych przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="cdd4e-118">Azure Scheduler guarantees its own high-availability and takes a different approach to user-created jobs.</span></span> <span data-ttu-id="cdd4e-119">Na przykład zadanie może wywoływać punktu końcowego HTTP, która jest niedostępna.</span><span class="sxs-lookup"><span data-stu-id="cdd4e-119">For example, your job may invoke an HTTP endpoint that’s unavailable.</span></span> <span data-ttu-id="cdd4e-120">Niemniej jednak Azure harmonogramu próbuje wykonać swoją pracę pomyślnie, przez alternatywnych opcjami na wypadek awarii.</span><span class="sxs-lookup"><span data-stu-id="cdd4e-120">Azure Scheduler nonetheless tries to execute your job successfully, by giving you alternative options to deal with failure.</span></span> <span data-ttu-id="cdd4e-121">Harmonogram systemu Azure dzieje się tak na dwa sposoby:</span><span class="sxs-lookup"><span data-stu-id="cdd4e-121">Azure Scheduler does this in two ways:</span></span>

### <a name="configurable-retry-policy-via-retrypolicy"></a><span data-ttu-id="cdd4e-122">Można skonfigurować zasady spróbuj ponownie za pomocą "retryPolicy"</span><span class="sxs-lookup"><span data-stu-id="cdd4e-122">Configurable Retry Policy via “retryPolicy”</span></span>
<span data-ttu-id="cdd4e-123">Harmonogram systemu Azure pozwala skonfigurować zasady ponawiania.</span><span class="sxs-lookup"><span data-stu-id="cdd4e-123">Azure Scheduler allows you to configure a retry policy.</span></span> <span data-ttu-id="cdd4e-124">Domyślnie jeśli zadanie nie powiedzie się, harmonogram próbuje zadanie ponownie cztery razy więcej, w odstępach 30 sekund.</span><span class="sxs-lookup"><span data-stu-id="cdd4e-124">By default, if a job fails, Scheduler tries the job again four more times, at 30-second intervals.</span></span> <span data-ttu-id="cdd4e-125">Możesz ponownie skonfigurować tej zasady ponawiania być skuteczniejsze (na przykład dziesięć razy w odstępach 30 sekund) lub im (na przykład dwa razy codziennie.)</span><span class="sxs-lookup"><span data-stu-id="cdd4e-125">You may re-configure this retry policy to be more aggressive (for example, ten times, at 30-second intervals) or looser (for example, two times, at daily intervals.)</span></span>

<span data-ttu-id="cdd4e-126">Jako przykład kiedy może to ułatwić może utworzyć zadania uruchamiane raz w tygodniu, który wywołuje punkt końcowy HTTP.</span><span class="sxs-lookup"><span data-stu-id="cdd4e-126">As an example of when this may help, you may create a job that runs once a week and invokes an HTTP endpoint.</span></span> <span data-ttu-id="cdd4e-127">Jeśli punkt końcowy HTTP działa przez kilka godzin po uruchomieniu zadania, może nie chcesz czekać tydzień więcej zadania uruchamiać ponownie, ponieważ nawet domyślne zasady ponawiania zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="cdd4e-127">If the HTTP endpoint is down for a few hours when your job runs, you may not want to wait one more week for the job to run again since even the default retry policy will fail.</span></span> <span data-ttu-id="cdd4e-128">W takich przypadkach mogą ponownie skonfigurować zasady ponawiania standard, aby ponowić próbę co trzy godziny (na przykład) zamiast co 30 sekund.</span><span class="sxs-lookup"><span data-stu-id="cdd4e-128">In such cases, you may reconfigure the standard retry policy to retry every three hours (for example) instead of every 30 seconds.</span></span>

<span data-ttu-id="cdd4e-129">Aby dowiedzieć się, jak skonfigurować zasady ponawiania, zajrzyj do [retryPolicy](scheduler-concepts-terms.md#retrypolicy).</span><span class="sxs-lookup"><span data-stu-id="cdd4e-129">To learn how to configure a retry policy, refer to [retryPolicy](scheduler-concepts-terms.md#retrypolicy).</span></span>

### <a name="alternate-endpoint-configurability-via-erroraction"></a><span data-ttu-id="cdd4e-130">Alternatywne konfigurowalne punktu końcowego za pośrednictwem "errorAction"</span><span class="sxs-lookup"><span data-stu-id="cdd4e-130">Alternate Endpoint Configurability via “errorAction”</span></span>
<span data-ttu-id="cdd4e-131">Jeśli punkt końcowy docelowego dla zadania harmonogramu Azure pozostaje jest nieosiągalny, harmonogram systemu Azure powraca do punkcie końcowym alternate obsługi błędów po wykonaniu jej zasady ponawiania.</span><span class="sxs-lookup"><span data-stu-id="cdd4e-131">If the target endpoint for your Azure Scheduler job remains unreachable, Azure Scheduler falls back to the alternate error-handling endpoint after following its retry policy.</span></span> <span data-ttu-id="cdd4e-132">Jeśli skonfigurowano punkcie końcowym alternate obsługi błędów, harmonogram systemu Azure wywołuje go.</span><span class="sxs-lookup"><span data-stu-id="cdd4e-132">If an alternate error-handling endpoint is configured, Azure Scheduler invokes it.</span></span> <span data-ttu-id="cdd4e-133">Z punktem końcowym alternatywne własne zadania są wysokiej dostępności w wypadku awarii.</span><span class="sxs-lookup"><span data-stu-id="cdd4e-133">With an alternate endpoint, your own jobs are highly available in the face of failure.</span></span>

<span data-ttu-id="cdd4e-134">Na przykład w diagramie poniżej Harmonogram systemu Azure wynika, jego zasady ponawiania trafienie usługi sieci web w Nowym Jorku.</span><span class="sxs-lookup"><span data-stu-id="cdd4e-134">As an example, in the diagram below, Azure Scheduler follows its retry policy to hit a New York web service.</span></span> <span data-ttu-id="cdd4e-135">Po awarii ponownych prób, sprawdza, czy jest alternatywny.</span><span class="sxs-lookup"><span data-stu-id="cdd4e-135">After the retries fail, it checks if there's an alternate.</span></span> <span data-ttu-id="cdd4e-136">Następnie przejdzie do przodu i uruchamia wysyłania żądań do alternatywnego z tej samej zasady ponawiania.</span><span class="sxs-lookup"><span data-stu-id="cdd4e-136">It then goes ahead and starts making requests to the alternate with the same retry policy.</span></span>

![][2]

<span data-ttu-id="cdd4e-137">Należy pamiętać, że te same zasady ponawiania dotyczą zarówno oryginalnej operacji, jak i akcja błędu alternatywny.</span><span class="sxs-lookup"><span data-stu-id="cdd4e-137">Note that the same retry policy applies to both the original action and the alternate error action.</span></span> <span data-ttu-id="cdd4e-138">Istnieje również możliwość Akcja alternatywny błędu akcji typ jest inny niż typ działania głównego akcji.</span><span class="sxs-lookup"><span data-stu-id="cdd4e-138">It’s also possible to have the alternate error action’s action type be different from the main action’s action type.</span></span> <span data-ttu-id="cdd4e-139">Na przykład podczas działania głównego może wywołaniem punktu końcowego HTTP, akcja błędu zamiast tego można kolejki magazynu, kolejką usługi service bus lub Akcja temat magistrali usługi, który wykonuje rejestrowanie błędów.</span><span class="sxs-lookup"><span data-stu-id="cdd4e-139">For example, while the main action may be invoking an HTTP endpoint, the error action may instead be a storage queue, service bus queue, or service bus topic action that does error-logging.</span></span>

<span data-ttu-id="cdd4e-140">Aby dowiedzieć się, jak skonfigurować alternatywne punktu końcowego, zapoznaj się [errorAction](scheduler-concepts-terms.md#action-and-erroraction).</span><span class="sxs-lookup"><span data-stu-id="cdd4e-140">To learn how to configure an alternate endpoint, refer to [errorAction](scheduler-concepts-terms.md#action-and-erroraction).</span></span>

## <a name="see-also"></a><span data-ttu-id="cdd4e-141">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="cdd4e-141">See Also</span></span>
 [<span data-ttu-id="cdd4e-142">Co to jest Scheduler?</span><span class="sxs-lookup"><span data-stu-id="cdd4e-142">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="cdd4e-143">Pojęcia i terminologia dotyczące usługi Azure Scheduler oraz hierarchia jednostek</span><span class="sxs-lookup"><span data-stu-id="cdd4e-143">Azure Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="cdd4e-144">Rozpoczynanie pracy z usługą Scheduler w witrynie Azure Portal</span><span class="sxs-lookup"><span data-stu-id="cdd4e-144">Get started using Scheduler in the Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="cdd4e-145">Plany i rozliczenia w usłudze Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="cdd4e-145">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="cdd4e-146">Tworzenie złożonych harmonogramów i zaawansowanych cykli z użyciem usługi Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="cdd4e-146">How to build complex schedules and advanced recurrence with Azure Scheduler</span></span>](scheduler-advanced-complexity.md)

 [<span data-ttu-id="cdd4e-147">Dokumentacja interfejsu API REST usługi Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="cdd4e-147">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="cdd4e-148">Dokumentacja poleceń cmdlet programu PowerShell dla usługi Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="cdd4e-148">Azure Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="cdd4e-149">Limity, wartości domyślne i kody błędów usługi Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="cdd4e-149">Azure Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)

 [<span data-ttu-id="cdd4e-150">Uwierzytelnianie połączeń wychodzących usługi Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="cdd4e-150">Azure Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

[1]: ./media/scheduler-high-availability-reliability/scheduler-high-availability-reliability-image1.png

[2]: ./media/scheduler-high-availability-reliability/scheduler-high-availability-reliability-image2.png
