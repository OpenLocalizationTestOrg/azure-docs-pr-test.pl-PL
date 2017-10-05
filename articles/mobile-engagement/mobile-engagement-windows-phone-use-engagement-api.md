---
title: "Jak zaangażowania interfejsu API w systemie Windows Phone Silverlight"
description: "Jak zaangażowania interfejsu API w systemie Windows Phone Silverlight"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: ae2ba2e8-f75b-4dee-a164-a7dd65d35a23
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: ec8b6c13ea052c8063dfde4321cdd286ab6cb817
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-the-engagement-api-on-windows-phone-silverlight"></a><span data-ttu-id="a8f06-103">Jak zaangażowania interfejsu API w systemie Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="a8f06-103">How to Use the Engagement API on Windows Phone Silverlight</span></span>
<span data-ttu-id="a8f06-104">Ten dokument jest dodatkiem do dokumentu [jak zintegrowana usługa Mobile Engagement w aplikacji Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md).</span><span class="sxs-lookup"><span data-stu-id="a8f06-104">This document is an add-on to the document [How to integrate Mobile Engagement in your Windows Phone Silverlight app](mobile-engagement-windows-phone-integrate-engagement.md).</span></span> <span data-ttu-id="a8f06-105">Zapewnia on głębokość szczegółowe informacje dotyczące raportu statystyk aplikacji za pomocą interfejsu API usługi Engagement.</span><span class="sxs-lookup"><span data-stu-id="a8f06-105">It provides in depth details about how to use the Engagement API to report your application statistics.</span></span>

<span data-ttu-id="a8f06-106">Jeśli mają zaangażowania do raportów aplikacji sesji, działania, awarii (Crash) i informacje techniczne, a następnie Najłatwiejszą metodą jest zapewnienie wszystkie Twoje `PhoneApplicationPage` klasy podrzędne dziedziczą `EngagementPage` klasy.</span><span class="sxs-lookup"><span data-stu-id="a8f06-106">If you only want Engagement to report your application's sessions, activities, crashes and technical information, then the simplest way is to make all your `PhoneApplicationPage` sub-classes inherit from the `EngagementPage` class.</span></span>

<span data-ttu-id="a8f06-107">Jeśli chcesz zrobić więcej, na przykład, jeśli zachodzi konieczność raportów aplikacji określonych zdarzeń, błędów i zadań, lub jeśli zajdzie potrzeba raportu działania aplikacji w inny sposób niż jeden zaimplementowana w `EngagementPage` klasy, a następnie należy użyć interfejsu API usługi Engagement.</span><span class="sxs-lookup"><span data-stu-id="a8f06-107">If you want to do more, for example if you need to report application specific events, errors and jobs, or if you have to report your application's activities in a different way than the one implemented in the `EngagementPage` classes, then you need to use the Engagement API.</span></span>

<span data-ttu-id="a8f06-108">Interfejsu API programu zaangażowania jest zapewniana przez `EngagementAgent` klasy.</span><span class="sxs-lookup"><span data-stu-id="a8f06-108">The Engagement API is provided by the `EngagementAgent` class.</span></span> <span data-ttu-id="a8f06-109">Można dostęp do tych metod, za pomocą `EngagementAgent.Instance`.</span><span class="sxs-lookup"><span data-stu-id="a8f06-109">You can access to those methods through `EngagementAgent.Instance`.</span></span>

<span data-ttu-id="a8f06-110">Nawet wtedy, gdy moduł agenta nie została zainicjowana, każde wywołanie interfejsu API jest opóźniona i zostanie wykonana ponownie gdy agent nie jest dostępny.</span><span class="sxs-lookup"><span data-stu-id="a8f06-110">Even if the agent module has not been initialized, each call to the API is deferred, and will be executed again when the agent is available.</span></span>

## <a name="engagement-concepts"></a><span data-ttu-id="a8f06-111">Pojęcia dotyczące usługi Engagement</span><span class="sxs-lookup"><span data-stu-id="a8f06-111">Engagement concepts</span></span>
<span data-ttu-id="a8f06-112">Następujące części uściślić pojęcia Mobile Engagement dla platformy Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="a8f06-112">The following parts refine the Mobile Engagement Concepts for the Windows Phone platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="a8f06-113">`Session` i `Activity`</span><span class="sxs-lookup"><span data-stu-id="a8f06-113">`Session` and `Activity`</span></span>
<span data-ttu-id="a8f06-114">*Działania* jest zazwyczaj skojarzony z jedną stronę aplikacji, to znaczy *działania* rozpoczyna się, gdy strona jest wyświetlana i zatrzymywana, gdy strona zostanie zamknięty: dotyczy to sytuacji, gdy zestaw SDK Engagement jest zintegrowany przy użyciu `EngagementPage` klasy.</span><span class="sxs-lookup"><span data-stu-id="a8f06-114">An *activity* is usually associated with one page of the application, that is to say the *activity* starts when the page is displayed and stops when the page is closed: this is the case when the Engagement SDK is integrated by using the `EngagementPage` class.</span></span>

<span data-ttu-id="a8f06-115">Ale *działania* mogą również być kontrolowane ręcznie przy użyciu interfejsu API usługi Engagement.</span><span class="sxs-lookup"><span data-stu-id="a8f06-115">But *activities* can also be controlled manually by using the Engagement API.</span></span> <span data-ttu-id="a8f06-116">Dzięki temu można podzielić na daną stronę w kilku części sub, aby uzyskać więcej informacji o korzystaniu z tej strony (na przykład aby częstotliwość znane i jak długo okna dialogowe są używane wewnątrz tej strony).</span><span class="sxs-lookup"><span data-stu-id="a8f06-116">This allows to split a given page in several sub parts to get more details about the usage of this page (for example to known how often and how long dialogs are used inside this page).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="a8f06-117">Działania raportowania</span><span class="sxs-lookup"><span data-stu-id="a8f06-117">Reporting Activities</span></span>
### <a name="user-starts-a-new-activity"></a><span data-ttu-id="a8f06-118">Użytkownik uruchamia nowe działanie</span><span class="sxs-lookup"><span data-stu-id="a8f06-118">User starts a new Activity</span></span>
#### <a name="reference"></a><span data-ttu-id="a8f06-119">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="a8f06-119">Reference</span></span>
            void StartActivity(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="a8f06-120">Należy wywołać `StartActivity()` każdej zmianie działania użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a8f06-120">You need to call `StartActivity()` each time the user activity changes.</span></span> <span data-ttu-id="a8f06-121">W pierwszym wywołaniu tej funkcji uruchamia nową sesję użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a8f06-121">The first call to this function starts a new user session.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a8f06-122">Zestaw SDK automatycznie Wywołaj metodę EndActivity po zamknięciu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a8f06-122">The SDK automatically call the EndActivity method when the application is closed.</span></span> <span data-ttu-id="a8f06-123">W związku z tym zaleca do wywoływania metody StartActivity zawsze, gdy działanie zmiany użytkowników i nigdy Wywołaj metodę EndActivity, ponieważ wywołanie tej metody wymusza bieżącej sesji, aby zostać zakończona.</span><span class="sxs-lookup"><span data-stu-id="a8f06-123">Thus, it is HIGHLY recommended to call the StartActivity method whenever the activity of the user change, and to NEVER call the EndActivity method, since calling this method forces the current session to be ended.</span></span>
> 
> 

#### <a name="example"></a><span data-ttu-id="a8f06-124">Przykład</span><span class="sxs-lookup"><span data-stu-id="a8f06-124">Example</span></span>
            EngagementAgent.Instance.StartActivity("main", new Dictionary<object, object>() {{"example", "data"}});

### <a name="user-ends-his-current-activity"></a><span data-ttu-id="a8f06-125">Użytkownik kończy swoje bieżące działanie</span><span class="sxs-lookup"><span data-stu-id="a8f06-125">User ends his current Activity</span></span>
#### <a name="reference"></a><span data-ttu-id="a8f06-126">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="a8f06-126">Reference</span></span>
            void EndActivity()

<span data-ttu-id="a8f06-127">Należy wywołać `EndActivity()` co najmniej raz, gdy użytkownik kończy swoje ostatnie działanie.</span><span class="sxs-lookup"><span data-stu-id="a8f06-127">You need to call `EndActivity()` at least once when the user finishes his last activity.</span></span> <span data-ttu-id="a8f06-128">Informuje Engagement SDK, że użytkownik jest obecnie w stanie bezczynności i sesji użytkownika muszą być zamknięte raz limit czasu sesji wygaśnie (jeśli wywołujesz `StartActivity()` przed upłynięciem limitu czasu sesji, sesja jest kontynuowane po prostu).</span><span class="sxs-lookup"><span data-stu-id="a8f06-128">This informs the Engagement SDK that the user is currently idle, and that the user session need to be closed once the session timeout will expire (if you call `StartActivity()` before the session timeout expires, the session is simply continued).</span></span>

#### <a name="example"></a><span data-ttu-id="a8f06-129">Przykład</span><span class="sxs-lookup"><span data-stu-id="a8f06-129">Example</span></span>
            EngagementAgent.Instance.EndActivity();

## <a name="reporting-jobs"></a><span data-ttu-id="a8f06-130">Zadania raportowania</span><span class="sxs-lookup"><span data-stu-id="a8f06-130">Reporting Jobs</span></span>
### <a name="start-a-job"></a><span data-ttu-id="a8f06-131">Uruchom zadanie</span><span class="sxs-lookup"><span data-stu-id="a8f06-131">Start a job</span></span>
#### <a name="reference"></a><span data-ttu-id="a8f06-132">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="a8f06-132">Reference</span></span>
            void StartJob(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="a8f06-133">To zadanie służy do śledzenia zadań podaje w danym okresie czasu.</span><span class="sxs-lookup"><span data-stu-id="a8f06-133">You can use the job to track certains tasks over a period of time.</span></span>

#### <a name="example"></a><span data-ttu-id="a8f06-134">Przykład</span><span class="sxs-lookup"><span data-stu-id="a8f06-134">Example</span></span>
            // An upload begins...

            // Set the extras
            var extras = new Dictionary<object, object>();
            extras.Add("title", "avatar");
            extras.Add("type", "image");

            EngagementAgent.Instance.StartJob("uploadData", extras);

### <a name="end-a-job"></a><span data-ttu-id="a8f06-135">Zakończenia zadania</span><span class="sxs-lookup"><span data-stu-id="a8f06-135">End a job</span></span>
#### <a name="reference"></a><span data-ttu-id="a8f06-136">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="a8f06-136">Reference</span></span>
            void EndJob(string name)

<span data-ttu-id="a8f06-137">Jak zadanie śledzone przez zadanie zostało zakończone, należy wywołać metodę EndJob dla tego zadania, podając nazwę zadania.</span><span class="sxs-lookup"><span data-stu-id="a8f06-137">As soon as a task tracked by a job has been terminated, you should call the EndJob method for this job, by supplying the job name.</span></span>

#### <a name="example"></a><span data-ttu-id="a8f06-138">Przykład</span><span class="sxs-lookup"><span data-stu-id="a8f06-138">Example</span></span>
            // In the previous section, we started an upload tracking with a job
            // Then, the upload ends

            EngagementAgent.Instance.EndJob("uploadData");

## <a name="reporting-events"></a><span data-ttu-id="a8f06-139">Zdarzenia raportowania</span><span class="sxs-lookup"><span data-stu-id="a8f06-139">Reporting Events</span></span>
<span data-ttu-id="a8f06-140">Brak trzy typy zdarzeń:</span><span class="sxs-lookup"><span data-stu-id="a8f06-140">There is three types of events :</span></span>

* <span data-ttu-id="a8f06-141">Autonomiczny zdarzenia</span><span class="sxs-lookup"><span data-stu-id="a8f06-141">Standalone events</span></span>
* <span data-ttu-id="a8f06-142">Zdarzenia sesji</span><span class="sxs-lookup"><span data-stu-id="a8f06-142">Session events</span></span>
* <span data-ttu-id="a8f06-143">Zdarzenia zadań</span><span class="sxs-lookup"><span data-stu-id="a8f06-143">Job events</span></span>

### <a name="standalone-events"></a><span data-ttu-id="a8f06-144">Autonomiczny zdarzenia</span><span class="sxs-lookup"><span data-stu-id="a8f06-144">Standalone Events</span></span>
#### <a name="reference"></a><span data-ttu-id="a8f06-145">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="a8f06-145">Reference</span></span>
            void SendEvent(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="a8f06-146">Autonomiczny zdarzeń może wystąpić poza kontekstem sesji.</span><span class="sxs-lookup"><span data-stu-id="a8f06-146">Standalone events can occur outside of the context of a session.</span></span>

#### <a name="example"></a><span data-ttu-id="a8f06-147">Przykład</span><span class="sxs-lookup"><span data-stu-id="a8f06-147">Example</span></span>
            EngagementAgent.Instance.SendEvent("event", extra);

### <a name="session-events"></a><span data-ttu-id="a8f06-148">Zdarzenia sesji</span><span class="sxs-lookup"><span data-stu-id="a8f06-148">Session events</span></span>
#### <a name="reference"></a><span data-ttu-id="a8f06-149">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="a8f06-149">Reference</span></span>
            void SendSessionEvent(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="a8f06-150">Zdarzenia sesji są zwykle używane do zgłaszania akcji wykonywanych przez użytkownika podczas jego sesji.</span><span class="sxs-lookup"><span data-stu-id="a8f06-150">Session events are usually used to report the actions performed by a user during his session.</span></span>

#### <a name="example"></a><span data-ttu-id="a8f06-151">Przykład</span><span class="sxs-lookup"><span data-stu-id="a8f06-151">Example</span></span>
<span data-ttu-id="a8f06-152">**Bez danych:**</span><span class="sxs-lookup"><span data-stu-id="a8f06-152">**Without data :**</span></span>

            EngagementAgent.Instance.SendSessionEvent("sessionEvent");

            // or

            EngagementAgent.Instance.SendSessionEvent("sessionEvent", null);

<span data-ttu-id="a8f06-153">**Z danymi:**</span><span class="sxs-lookup"><span data-stu-id="a8f06-153">**With data :**</span></span>

            Dictionary<object, object> extras = new Dictionary<object,object>();
            extras.Add("name", "data");
            EngagementAgent.Instance.SendSessionEvent("sessionEvent", extras);

### <a name="job-events"></a><span data-ttu-id="a8f06-154">Zdarzenia zadań</span><span class="sxs-lookup"><span data-stu-id="a8f06-154">Job Events</span></span>
#### <a name="reference"></a><span data-ttu-id="a8f06-155">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="a8f06-155">Reference</span></span>
            void SendJobEvent(string eventName, string jobName, Dictionary<object, object> extras = null)

<span data-ttu-id="a8f06-156">Zdarzenia zadania są zazwyczaj używane do zgłaszania akcji wykonywanych przez użytkownika podczas wykonywania zadania.</span><span class="sxs-lookup"><span data-stu-id="a8f06-156">Job events are usually used to report the actions performed by a user during a Job.</span></span>

#### <a name="example"></a><span data-ttu-id="a8f06-157">Przykład</span><span class="sxs-lookup"><span data-stu-id="a8f06-157">Example</span></span>
            EngagementAgent.Instance.SendJobEvent("eventName", "jobName", extras);

## <a name="reporting-errors"></a><span data-ttu-id="a8f06-158">Raportowanie błędów</span><span class="sxs-lookup"><span data-stu-id="a8f06-158">Reporting Errors</span></span>
<span data-ttu-id="a8f06-159">Brak trzy typy błędów:</span><span class="sxs-lookup"><span data-stu-id="a8f06-159">There is three types of errors :</span></span>

* <span data-ttu-id="a8f06-160">Błędy autonomiczny</span><span class="sxs-lookup"><span data-stu-id="a8f06-160">Standalone errors</span></span>
* <span data-ttu-id="a8f06-161">Błędy sesji</span><span class="sxs-lookup"><span data-stu-id="a8f06-161">Session errors</span></span>
* <span data-ttu-id="a8f06-162">Błędy zadań</span><span class="sxs-lookup"><span data-stu-id="a8f06-162">Job errors</span></span>

### <a name="standalone-errors"></a><span data-ttu-id="a8f06-163">Błędy autonomiczny</span><span class="sxs-lookup"><span data-stu-id="a8f06-163">Standalone errors</span></span>
#### <a name="reference"></a><span data-ttu-id="a8f06-164">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="a8f06-164">Reference</span></span>
            void SendError(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="a8f06-165">Sprzecznie błędy sesji mogą wystąpić błędy autonomiczny poza kontekstem sesji.</span><span class="sxs-lookup"><span data-stu-id="a8f06-165">Contrary to session errors, standalone errors can occur outside of the context of a session.</span></span>

#### <a name="example"></a><span data-ttu-id="a8f06-166">Przykład</span><span class="sxs-lookup"><span data-stu-id="a8f06-166">Example</span></span>
            EngagementAgent.Instance.SendError("errorName", extras);

### <a name="session-errors"></a><span data-ttu-id="a8f06-167">Błędy sesji</span><span class="sxs-lookup"><span data-stu-id="a8f06-167">Session errors</span></span>
#### <a name="reference"></a><span data-ttu-id="a8f06-168">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="a8f06-168">Reference</span></span>
            void SendSessionError(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="a8f06-169">Błędy sesji są zwykle używane do raportów o błędach podczas sesji jego wpływu na użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a8f06-169">Session errors are usually used to report the errors impacting the user during his session.</span></span>

#### <a name="example"></a><span data-ttu-id="a8f06-170">Przykład</span><span class="sxs-lookup"><span data-stu-id="a8f06-170">Example</span></span>
            EngagementAgent.Instance.SendSessionError("errorName", extra);

### <a name="job-errors"></a><span data-ttu-id="a8f06-171">Błędy zadań</span><span class="sxs-lookup"><span data-stu-id="a8f06-171">Job Errors</span></span>
#### <a name="reference"></a><span data-ttu-id="a8f06-172">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="a8f06-172">Reference</span></span>
            void SendJobError(string errorName, string jobName, Dictionary<object, object> extras = null)

<span data-ttu-id="a8f06-173">Błędy może być powiązane z uruchomionym zadaniem zamiast związany z bieżącą sesją użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a8f06-173">Errors can be related to a running job instead of being related to the current user session.</span></span>

#### <a name="example"></a><span data-ttu-id="a8f06-174">Przykład</span><span class="sxs-lookup"><span data-stu-id="a8f06-174">Example</span></span>
            EngagementAgent.Instance.SendJobError("errorName", "jobname", extra);

## <a name="reporting-crashes"></a><span data-ttu-id="a8f06-175">Raportowanie awarii (Crash)</span><span class="sxs-lookup"><span data-stu-id="a8f06-175">Reporting Crashes</span></span>
<span data-ttu-id="a8f06-176">Agent udostępnia dwie metody na wypadek awarii.</span><span class="sxs-lookup"><span data-stu-id="a8f06-176">The agent provides two methods to deal with crashes.</span></span>

### <a name="send-an-exception"></a><span data-ttu-id="a8f06-177">Wyślij Wystąpił wyjątek</span><span class="sxs-lookup"><span data-stu-id="a8f06-177">Send an exception</span></span>
#### <a name="reference"></a><span data-ttu-id="a8f06-178">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="a8f06-178">Reference</span></span>
            void SendCrash(Exception e, bool terminateSession = false)

#### <a name="example"></a><span data-ttu-id="a8f06-179">Przykład</span><span class="sxs-lookup"><span data-stu-id="a8f06-179">Example</span></span>
<span data-ttu-id="a8f06-180">Wystąpił wyjątek w dowolnym momencie możesz wysłać przez wywołanie metody:</span><span class="sxs-lookup"><span data-stu-id="a8f06-180">You can send an exception at any time by calling :</span></span>

            EngagementAgent.Instance.SendCrash(aCatchedException);

<span data-ttu-id="a8f06-181">Opcjonalny parametr umożliwia również zakończyć sesję zaangażowania w tym samym czasie niż przy użyciu tej awarii.</span><span class="sxs-lookup"><span data-stu-id="a8f06-181">You can also use an optional parameter to terminate the engagement session at the same time than sending the crash.</span></span> <span data-ttu-id="a8f06-182">Aby to zrobić, należy wywołać:</span><span class="sxs-lookup"><span data-stu-id="a8f06-182">To do so, call :</span></span>

            EngagementAgent.Instance.SendCrash(new Exception("example"), terminateSession: true);

<span data-ttu-id="a8f06-183">Jeśli możesz to zrobić, zadania i sesji zostanie zamknięte zaraz po awarii wysyłania.</span><span class="sxs-lookup"><span data-stu-id="a8f06-183">If you do that, the session and jobs will be closed just after sending the crash.</span></span>

### <a name="send-an-unhandled-exception"></a><span data-ttu-id="a8f06-184">Wyślij nieobsługiwany wyjątek</span><span class="sxs-lookup"><span data-stu-id="a8f06-184">Send an unhandled exception</span></span>
#### <a name="reference"></a><span data-ttu-id="a8f06-185">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="a8f06-185">Reference</span></span>
            void SendCrash(ApplicationUnhandledExceptionEventArgs e)

<span data-ttu-id="a8f06-186">Engagement udostępnia również metody do wysyłania nieobsługiwanych wyjątków.</span><span class="sxs-lookup"><span data-stu-id="a8f06-186">Engagement also provides a method to send unhandled exceptions.</span></span> <span data-ttu-id="a8f06-187">Jest to szczególnie przydatne, gdy jest używany wewnątrz obsługi zdarzeń UnhandledException silverlight.</span><span class="sxs-lookup"><span data-stu-id="a8f06-187">This is especially useful when used inside the silverlight UnhandledException event handler.</span></span>

<span data-ttu-id="a8f06-188">Ta metoda będzie **zawsze** przerwanie zaangażowania sesji i zadania po wywołaniu.</span><span class="sxs-lookup"><span data-stu-id="a8f06-188">This method will **ALWAYS** terminate the engagement session and jobs after being called.</span></span>

#### <a name="example"></a><span data-ttu-id="a8f06-189">Przykład</span><span class="sxs-lookup"><span data-stu-id="a8f06-189">Example</span></span>
<span data-ttu-id="a8f06-190">Służy on do implementowania obsługi własnych UnhandledException (zwłaszcza, jeśli wyłączono automatyczne awarii, funkcję zaangażowania raportowania).</span><span class="sxs-lookup"><span data-stu-id="a8f06-190">You can use it to implement your own UnhandledException handler (especially if you have disabled the automatic crash reporting feature of Engagement).</span></span> <span data-ttu-id="a8f06-191">Na przykład w `Application_UnhandledException` metody `App.xaml.cs` pliku:</span><span class="sxs-lookup"><span data-stu-id="a8f06-191">For example, in the `Application_UnhandledException` method of the `App.xaml.cs` file :</span></span>

            // In your App.xaml.cs file

            // Code to execute on Unhandled Exceptions
            private void Application_UnhandledException(object sender, ApplicationUnhandledExceptionEventArgs e)
            {
              // your own code

              EngagementAgent.Instance.SendCrash(e);
            }

## <a name="onactivated"></a><span data-ttu-id="a8f06-192">OnActivated</span><span class="sxs-lookup"><span data-stu-id="a8f06-192">OnActivated</span></span>
### <a name="reference"></a><span data-ttu-id="a8f06-193">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="a8f06-193">Reference</span></span>
            void OnActivated(ActivatedEventArgs e)

<span data-ttu-id="a8f06-194">Gdy użytkownik przechodzi do przodu, od aplikacji, po wywołaniu zdarzenia dezaktywowane, system operacyjny spróbuje ponownie przełączyć aplikację do stanu nieaktywni.</span><span class="sxs-lookup"><span data-stu-id="a8f06-194">When the user navigates forward, away from an application, after the Deactivated event is raised, the operating system will attempt to put the application into a dormant state.</span></span> <span data-ttu-id="a8f06-195">Następnie aplikacja jest chowanie.</span><span class="sxs-lookup"><span data-stu-id="a8f06-195">Then, the application is Tombstoning.</span></span> <span data-ttu-id="a8f06-196">W tym procesie aplikacja zostanie zakończona, ale niektóre dane o stanie aplikacji i poszczególnych stron w aplikacji zostaną zachowane.</span><span class="sxs-lookup"><span data-stu-id="a8f06-196">In this process an application is terminated but some data about the state of the application and the individual pages within the application is preserved.</span></span>

<span data-ttu-id="a8f06-197">Należy wstawić `EngagementAgent.Instance.OnActivated(e)` w `Application_Activated` metody plik App.xaml.cs, aby zresetować agenta zaangażowania, gdy aplikacja została schowany.</span><span class="sxs-lookup"><span data-stu-id="a8f06-197">You have to insert `EngagementAgent.Instance.OnActivated(e)` in the `Application_Activated` method from the App.xaml.cs file to reset the Engagement Agent when the application has been Tombstoned.</span></span>

### <a name="example"></a><span data-ttu-id="a8f06-198">Przykład</span><span class="sxs-lookup"><span data-stu-id="a8f06-198">Example</span></span>
            // Inside your App.xaml.cs file

            // Code to execute when the application is activated (brought to foreground)
            // This code will not execute when the application is first launched
            private void Application_Activated(object sender, ActivatedEventArgs e)
            {
              EngagementAgent.Instance.OnActivated(e);
            }

## <a name="device-id"></a><span data-ttu-id="a8f06-199">Identyfikator urządzenia</span><span class="sxs-lookup"><span data-stu-id="a8f06-199">Device Id</span></span>
            String GetDeviceId()

<span data-ttu-id="a8f06-200">Identyfikator urządzenia zaangażowania można uzyskać przez wywołanie tej metody.</span><span class="sxs-lookup"><span data-stu-id="a8f06-200">You can get the engagement device id by calling this method.</span></span>

## <a name="extras-parameters"></a><span data-ttu-id="a8f06-201">Dodatkowe parametry</span><span class="sxs-lookup"><span data-stu-id="a8f06-201">Extras parameters</span></span>
<span data-ttu-id="a8f06-202">Dowolne dane można dołączyć do zdarzenia, błąd, działania lub zadania.</span><span class="sxs-lookup"><span data-stu-id="a8f06-202">Arbitrary data can be attached to an event, an error, an activity or a job.</span></span> <span data-ttu-id="a8f06-203">Dane te mogą być elementami struktury, za pomocą słownika.</span><span class="sxs-lookup"><span data-stu-id="a8f06-203">These data can be structured using a dictionary.</span></span> <span data-ttu-id="a8f06-204">Klucze i wartości mogą być dowolnego typu.</span><span class="sxs-lookup"><span data-stu-id="a8f06-204">Keys and values can be of any type.</span></span>

<span data-ttu-id="a8f06-205">Dodatkowe dane są serializowane, tak aby wstawić własne typu dodatki należy dodać kontraktu danych dla tego typu.</span><span class="sxs-lookup"><span data-stu-id="a8f06-205">Extras data are serialized so if you want to insert your own type in extras you have to add a data contract for this type.</span></span>

### <a name="example"></a><span data-ttu-id="a8f06-206">Przykład</span><span class="sxs-lookup"><span data-stu-id="a8f06-206">Example</span></span>
<span data-ttu-id="a8f06-207">Utworzymy nową klasę "Osoby".</span><span class="sxs-lookup"><span data-stu-id="a8f06-207">We create a new class "Person".</span></span>

            using System.Runtime.Serialization;

            namespace Engagement.Agent
            {
              [DataContract]
              public class Person
              {
                public Person(string name, int age)
                {
                  Age = age;
                  Name = name;
                }

                // Properties

                [DataMember]
                public int Age
                {
                  get;
                  set;
                }

                [DataMember]
                public string Name
                {
                  get;
                  set; 
                }
              }
            }

<span data-ttu-id="a8f06-208">Następnie dodamy `Person` wystąpienia dodatkową.</span><span class="sxs-lookup"><span data-stu-id="a8f06-208">Then, we will add a `Person` instance to an extra.</span></span>

            Person person = new Person("Engagement Haddock", 51);
            var extras = new Dictionary<object, object>();
            extras.Add("people", person);

            EngagementAgent.Instance.SendEvent("Event", extras);

> [!WARNING]
> <span data-ttu-id="a8f06-209">Jeśli inne typy obiektów, upewnij się, że ich metodę ToString() jest zaimplementowana do zwrócenia człowieka czytelnych ciągów.</span><span class="sxs-lookup"><span data-stu-id="a8f06-209">If you put other types of objects, make sure their ToString() method is implemented to return a human readable string.</span></span>
> 
> 

### <a name="limits"></a><span data-ttu-id="a8f06-210">Limity</span><span class="sxs-lookup"><span data-stu-id="a8f06-210">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="a8f06-211">Klucze</span><span class="sxs-lookup"><span data-stu-id="a8f06-211">Keys</span></span>
<span data-ttu-id="a8f06-212">Każdy klucz w obiekcie musi odpowiadać następującym wyrażeniem regularnym:</span><span class="sxs-lookup"><span data-stu-id="a8f06-212">Each key in the object must match the following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*$`

<span data-ttu-id="a8f06-213">Oznacza to, że klucze musi rozpoczynać się od co najmniej jedną literą, następują litery, cyfry i znaki podkreślenia (\_).</span><span class="sxs-lookup"><span data-stu-id="a8f06-213">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="a8f06-214">Rozmiar</span><span class="sxs-lookup"><span data-stu-id="a8f06-214">Size</span></span>
<span data-ttu-id="a8f06-215">Dodatki są ograniczone do **1024** znaków w wywołaniu.</span><span class="sxs-lookup"><span data-stu-id="a8f06-215">Extras are limited to **1024** characters per call.</span></span>

## <a name="reporting-application-information"></a><span data-ttu-id="a8f06-216">Raportowanie informacji o aplikacji</span><span class="sxs-lookup"><span data-stu-id="a8f06-216">Reporting Application Information</span></span>
### <a name="reference"></a><span data-ttu-id="a8f06-217">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="a8f06-217">Reference</span></span>
            void SendAppInfo(Dictionary<object, object> appInfos)

<span data-ttu-id="a8f06-218">Funkcja śledzenia informacji (lub innych aplikacji szczegółowych informacji) przy użyciu SendAppInfo() ręcznie może raportować.</span><span class="sxs-lookup"><span data-stu-id="a8f06-218">You can manually report tracking information (or any other application specific information) using the SendAppInfo() function.</span></span>

<span data-ttu-id="a8f06-219">Należy pamiętać, że te informacje mogą zostać przesłane przyrostowo: tylko najnowszą wartość dla danego klucza zostaną zachowane dla danego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="a8f06-219">Note that these information can be sent incrementally: only the latest value for a given key will be kept for a given device.</span></span> <span data-ttu-id="a8f06-220">Podobnie jak dodatkowe zdarzenia użycie słownika\<obiektu, obiekt\> dołączyć informacje.</span><span class="sxs-lookup"><span data-stu-id="a8f06-220">Like event extras, use a Dictionary\<object, object\> to attach informations.</span></span>

### <a name="example"></a><span data-ttu-id="a8f06-221">Przykład</span><span class="sxs-lookup"><span data-stu-id="a8f06-221">Example</span></span>
            Dictionary<object, object> appInfo = new Dictionary<object, object>()
            {
               {"subscription", "2013-12-07"},
               {"premium", "true"}
            };

            EngagementAgent.Instance.SendAppInfo(appInfo);

### <a name="limits"></a><span data-ttu-id="a8f06-222">Limity</span><span class="sxs-lookup"><span data-stu-id="a8f06-222">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="a8f06-223">Klucze</span><span class="sxs-lookup"><span data-stu-id="a8f06-223">Keys</span></span>
<span data-ttu-id="a8f06-224">Każdy klucz w obiekcie musi odpowiadać następującym wyrażeniem regularnym:</span><span class="sxs-lookup"><span data-stu-id="a8f06-224">Each key in the object must match the following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*$`

<span data-ttu-id="a8f06-225">Oznacza to, że klucze musi rozpoczynać się od co najmniej jedną literą, następują litery, cyfry i znaki podkreślenia (\_).</span><span class="sxs-lookup"><span data-stu-id="a8f06-225">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="a8f06-226">Rozmiar</span><span class="sxs-lookup"><span data-stu-id="a8f06-226">Size</span></span>
<span data-ttu-id="a8f06-227">Informacje o aplikacji są ograniczone do **1024** znaków w wywołaniu.</span><span class="sxs-lookup"><span data-stu-id="a8f06-227">Application information are limited to **1024** characters per call.</span></span>

<span data-ttu-id="a8f06-228">W poprzednim przykładzie JSON na serwer wysyłane jest 44 znaków:</span><span class="sxs-lookup"><span data-stu-id="a8f06-228">In the previous example, the JSON sent to the server is 44 characters long:</span></span>

            {"subscription":"2013-12-07","premium":"true"}

## <a name="logging"></a><span data-ttu-id="a8f06-229">Rejestrowanie</span><span class="sxs-lookup"><span data-stu-id="a8f06-229">Logging</span></span>
### <a name="enable-logging"></a><span data-ttu-id="a8f06-230">Włączanie rejestrowania</span><span class="sxs-lookup"><span data-stu-id="a8f06-230">Enable Logging</span></span>
<span data-ttu-id="a8f06-231">Można skonfigurować zestaw SDK do tworzenia dzienników testu w konsoli środowiska IDE.</span><span class="sxs-lookup"><span data-stu-id="a8f06-231">The SDK can be configured to produce test logs in the IDE console.</span></span>
<span data-ttu-id="a8f06-232">Dzienniki te nie są uaktywnione domyślnie.</span><span class="sxs-lookup"><span data-stu-id="a8f06-232">These logs are not activated by default.</span></span> <span data-ttu-id="a8f06-233">Aby dostosować to, zaktualizuj właściwość `EngagementAgent.Instance.TestLogEnabled` do jednej z dostępnych wartości `EngagementTestLogLevel` wyliczenia, na przykład:</span><span class="sxs-lookup"><span data-stu-id="a8f06-233">To customize this, update the property `EngagementAgent.Instance.TestLogEnabled` to one of the value available from the `EngagementTestLogLevel` enumeration, for instance:</span></span>

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();
