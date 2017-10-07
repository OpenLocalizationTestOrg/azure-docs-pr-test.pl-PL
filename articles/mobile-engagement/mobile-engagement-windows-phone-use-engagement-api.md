---
title: "Witaj tooUse aaaHow API zaangażowania na Windows Phone Silverlight"
description: "Jak tooUse hello API zaangażowania na Windows Phone Silverlight"
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
ms.openlocfilehash: 1e84be95cc910be7f1227b4ae60eb483a1939284
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-engagement-api-on-windows-phone-silverlight"></a><span data-ttu-id="89778-103">Jak tooUse hello API zaangażowania na Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="89778-103">How tooUse hello Engagement API on Windows Phone Silverlight</span></span>
<span data-ttu-id="89778-104">Ten dokument jest dodatek toohello [jak toointegrate Mobile Engagement w aplikacji Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md).</span><span class="sxs-lookup"><span data-stu-id="89778-104">This document is an add-on toohello document [How toointegrate Mobile Engagement in your Windows Phone Silverlight app](mobile-engagement-windows-phone-integrate-engagement.md).</span></span> <span data-ttu-id="89778-105">Zapewnia on głębokość szczegóły dotyczące sposobu toouse hello tooreport interfejsu API usługi Engagement statystyk aplikacji.</span><span class="sxs-lookup"><span data-stu-id="89778-105">It provides in depth details about how toouse hello Engagement API tooreport your application statistics.</span></span>

<span data-ttu-id="89778-106">Jeśli mają tooreport zaangażowania sesji aplikacji, działań, awarii (Crash) i informacje techniczne, a następnie hello najprostszą metodą jest toomake wszystkie Twoje `PhoneApplicationPage` klasy podrzędne dziedziczą hello `EngagementPage` klasy.</span><span class="sxs-lookup"><span data-stu-id="89778-106">If you only want Engagement tooreport your application's sessions, activities, crashes and technical information, then hello simplest way is toomake all your `PhoneApplicationPage` sub-classes inherit from hello `EngagementPage` class.</span></span>

<span data-ttu-id="89778-107">Jeśli chcesz, aby toodo więcej, na przykład, jeśli potrzebujesz tooreport aplikacji określonych zdarzeń, błędów i zadań, czy masz tooreport działania aplikacji w inny sposób niż jeden zaimplementowana w hello hello `EngagementPage` klas, wówczas należy toouse hello Interfejs API usługi Engagement.</span><span class="sxs-lookup"><span data-stu-id="89778-107">If you want toodo more, for example if you need tooreport application specific events, errors and jobs, or if you have tooreport your application's activities in a different way than hello one implemented in hello `EngagementPage` classes, then you need toouse hello Engagement API.</span></span>

<span data-ttu-id="89778-108">Hello zaangażowania interfejsu API jest zapewniana przez hello `EngagementAgent` klasy.</span><span class="sxs-lookup"><span data-stu-id="89778-108">hello Engagement API is provided by hello `EngagementAgent` class.</span></span> <span data-ttu-id="89778-109">Można uzyskać dostępu do metody toothose za pośrednictwem `EngagementAgent.Instance`.</span><span class="sxs-lookup"><span data-stu-id="89778-109">You can access toothose methods through `EngagementAgent.Instance`.</span></span>

<span data-ttu-id="89778-110">Nawet wtedy, gdy hello agenta modułu nie została zainicjowana, interfejsu API każdego wywołania toohello została odroczona i zostanie wykonana ponownie gdy hello agent jest dostępna.</span><span class="sxs-lookup"><span data-stu-id="89778-110">Even if hello agent module has not been initialized, each call toohello API is deferred, and will be executed again when hello agent is available.</span></span>

## <a name="engagement-concepts"></a><span data-ttu-id="89778-111">Pojęcia dotyczące usługi Engagement</span><span class="sxs-lookup"><span data-stu-id="89778-111">Engagement concepts</span></span>
<span data-ttu-id="89778-112">Hello następujące części uściślić pojęcia dotyczące usługi Engagement Mobile hello hello platformy Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="89778-112">hello following parts refine hello Mobile Engagement Concepts for hello Windows Phone platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="89778-113">`Session` i `Activity`</span><span class="sxs-lookup"><span data-stu-id="89778-113">`Session` and `Activity`</span></span>
<span data-ttu-id="89778-114">*Działania* są zwykle skojarzone z jednej strony aplikacji hello, która jest toosay hello *działania* uruchamiana, gdy strona hello jest wyświetlany i zatrzymuje po zamknięciu strony hello: hello w przypadku gdy hello Engagement SDK jest zintegrowany przy użyciu hello `EngagementPage` klasy.</span><span class="sxs-lookup"><span data-stu-id="89778-114">An *activity* is usually associated with one page of hello application, that is toosay hello *activity* starts when hello page is displayed and stops when hello page is closed: this is hello case when hello Engagement SDK is integrated by using hello `EngagementPage` class.</span></span>

<span data-ttu-id="89778-115">Ale *działania* można sterować także ręcznie przy użyciu hello interfejsu API usługi Engagement.</span><span class="sxs-lookup"><span data-stu-id="89778-115">But *activities* can also be controlled manually by using hello Engagement API.</span></span> <span data-ttu-id="89778-116">Umożliwia to toosplit danej strony w kilku tooget części sub więcej szczegółów na temat hello użycia tej strony (na przykład częstotliwość tooknown i jak długo okna dialogowe są używane wewnątrz tej strony).</span><span class="sxs-lookup"><span data-stu-id="89778-116">This allows toosplit a given page in several sub parts tooget more details about hello usage of this page (for example tooknown how often and how long dialogs are used inside this page).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="89778-117">Działania raportowania</span><span class="sxs-lookup"><span data-stu-id="89778-117">Reporting Activities</span></span>
### <a name="user-starts-a-new-activity"></a><span data-ttu-id="89778-118">Użytkownik uruchamia nowe działanie</span><span class="sxs-lookup"><span data-stu-id="89778-118">User starts a new Activity</span></span>
#### <a name="reference"></a><span data-ttu-id="89778-119">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="89778-119">Reference</span></span>
            void StartActivity(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="89778-120">Należy toocall `StartActivity()` każde działanie użytkownika hello czasu zmiany.</span><span class="sxs-lookup"><span data-stu-id="89778-120">You need toocall `StartActivity()` each time hello user activity changes.</span></span> <span data-ttu-id="89778-121">Hello pierwszej wywołania funkcji toothis uruchamia nową sesję użytkownika.</span><span class="sxs-lookup"><span data-stu-id="89778-121">hello first call toothis function starts a new user session.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="89778-122">Witaj SDK automatycznie wywołać metodę EndActivity hello, po zamknięciu aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="89778-122">hello SDK automatically call hello EndActivity method when hello application is closed.</span></span> <span data-ttu-id="89778-123">W związku z tym zaleca toocall hello StartActivity metody zawsze, gdy Zakończono działanie hello hello użytkownika zmian i wywołania tooNEVER hello metody EndActivity, ponieważ wywołanie tej metody wymusza hello toobe bieżącej sesji.</span><span class="sxs-lookup"><span data-stu-id="89778-123">Thus, it is HIGHLY recommended toocall hello StartActivity method whenever hello activity of hello user change, and tooNEVER call hello EndActivity method, since calling this method forces hello current session toobe ended.</span></span>
> 
> 

#### <a name="example"></a><span data-ttu-id="89778-124">Przykład</span><span class="sxs-lookup"><span data-stu-id="89778-124">Example</span></span>
            EngagementAgent.Instance.StartActivity("main", new Dictionary<object, object>() {{"example", "data"}});

### <a name="user-ends-his-current-activity"></a><span data-ttu-id="89778-125">Użytkownik kończy swoje bieżące działanie</span><span class="sxs-lookup"><span data-stu-id="89778-125">User ends his current Activity</span></span>
#### <a name="reference"></a><span data-ttu-id="89778-126">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="89778-126">Reference</span></span>
            void EndActivity()

<span data-ttu-id="89778-127">Należy toocall `EndActivity()` co najmniej raz, gdy użytkownik hello kończy swoje ostatnie działanie.</span><span class="sxs-lookup"><span data-stu-id="89778-127">You need toocall `EndActivity()` at least once when hello user finishes his last activity.</span></span> <span data-ttu-id="89778-128">Informuje hello Engagement SDK hello użytkownik jest obecnie w stanie bezczynności, czy że sesji użytkownika hello muszą toobe zamknąć raz limit czasu sesji hello wygaśnie (jeśli wywołujesz `StartActivity()` przed upłynięciem limitu czasu sesji hello, sesji hello jest kontynuowane po prostu).</span><span class="sxs-lookup"><span data-stu-id="89778-128">This informs hello Engagement SDK that hello user is currently idle, and that hello user session need toobe closed once hello session timeout will expire (if you call `StartActivity()` before hello session timeout expires, hello session is simply continued).</span></span>

#### <a name="example"></a><span data-ttu-id="89778-129">Przykład</span><span class="sxs-lookup"><span data-stu-id="89778-129">Example</span></span>
            EngagementAgent.Instance.EndActivity();

## <a name="reporting-jobs"></a><span data-ttu-id="89778-130">Zadania raportowania</span><span class="sxs-lookup"><span data-stu-id="89778-130">Reporting Jobs</span></span>
### <a name="start-a-job"></a><span data-ttu-id="89778-131">Uruchom zadanie</span><span class="sxs-lookup"><span data-stu-id="89778-131">Start a job</span></span>
#### <a name="reference"></a><span data-ttu-id="89778-132">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="89778-132">Reference</span></span>
            void StartJob(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="89778-133">Podaje tootrack zadania hello można użyć w danym okresie czasu.</span><span class="sxs-lookup"><span data-stu-id="89778-133">You can use hello job tootrack certains tasks over a period of time.</span></span>

#### <a name="example"></a><span data-ttu-id="89778-134">Przykład</span><span class="sxs-lookup"><span data-stu-id="89778-134">Example</span></span>
            // An upload begins...

            // Set hello extras
            var extras = new Dictionary<object, object>();
            extras.Add("title", "avatar");
            extras.Add("type", "image");

            EngagementAgent.Instance.StartJob("uploadData", extras);

### <a name="end-a-job"></a><span data-ttu-id="89778-135">Zakończenia zadania</span><span class="sxs-lookup"><span data-stu-id="89778-135">End a job</span></span>
#### <a name="reference"></a><span data-ttu-id="89778-136">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="89778-136">Reference</span></span>
            void EndJob(string name)

<span data-ttu-id="89778-137">Jak zadanie śledzone przez zadanie zostało zakończone, powinien wywoływać metodę EndJob powitania dla tego zadania, podając nazwę zadania hello.</span><span class="sxs-lookup"><span data-stu-id="89778-137">As soon as a task tracked by a job has been terminated, you should call hello EndJob method for this job, by supplying hello job name.</span></span>

#### <a name="example"></a><span data-ttu-id="89778-138">Przykład</span><span class="sxs-lookup"><span data-stu-id="89778-138">Example</span></span>
            // In hello previous section, we started an upload tracking with a job
            // Then, hello upload ends

            EngagementAgent.Instance.EndJob("uploadData");

## <a name="reporting-events"></a><span data-ttu-id="89778-139">Zdarzenia raportowania</span><span class="sxs-lookup"><span data-stu-id="89778-139">Reporting Events</span></span>
<span data-ttu-id="89778-140">Brak trzy typy zdarzeń:</span><span class="sxs-lookup"><span data-stu-id="89778-140">There is three types of events :</span></span>

* <span data-ttu-id="89778-141">Autonomiczny zdarzenia</span><span class="sxs-lookup"><span data-stu-id="89778-141">Standalone events</span></span>
* <span data-ttu-id="89778-142">Zdarzenia sesji</span><span class="sxs-lookup"><span data-stu-id="89778-142">Session events</span></span>
* <span data-ttu-id="89778-143">Zdarzenia zadań</span><span class="sxs-lookup"><span data-stu-id="89778-143">Job events</span></span>

### <a name="standalone-events"></a><span data-ttu-id="89778-144">Autonomiczny zdarzenia</span><span class="sxs-lookup"><span data-stu-id="89778-144">Standalone Events</span></span>
#### <a name="reference"></a><span data-ttu-id="89778-145">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="89778-145">Reference</span></span>
            void SendEvent(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="89778-146">Autonomiczny zdarzeń może wystąpić poza hello kontekstu sesji.</span><span class="sxs-lookup"><span data-stu-id="89778-146">Standalone events can occur outside of hello context of a session.</span></span>

#### <a name="example"></a><span data-ttu-id="89778-147">Przykład</span><span class="sxs-lookup"><span data-stu-id="89778-147">Example</span></span>
            EngagementAgent.Instance.SendEvent("event", extra);

### <a name="session-events"></a><span data-ttu-id="89778-148">Zdarzenia sesji</span><span class="sxs-lookup"><span data-stu-id="89778-148">Session events</span></span>
#### <a name="reference"></a><span data-ttu-id="89778-149">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="89778-149">Reference</span></span>
            void SendSessionEvent(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="89778-150">Zdarzenia sesji są zazwyczaj używane tooreport hello akcje wykonywane przez użytkownika podczas jego sesji.</span><span class="sxs-lookup"><span data-stu-id="89778-150">Session events are usually used tooreport hello actions performed by a user during his session.</span></span>

#### <a name="example"></a><span data-ttu-id="89778-151">Przykład</span><span class="sxs-lookup"><span data-stu-id="89778-151">Example</span></span>
<span data-ttu-id="89778-152">**Bez danych:**</span><span class="sxs-lookup"><span data-stu-id="89778-152">**Without data :**</span></span>

            EngagementAgent.Instance.SendSessionEvent("sessionEvent");

            // or

            EngagementAgent.Instance.SendSessionEvent("sessionEvent", null);

<span data-ttu-id="89778-153">**Z danymi:**</span><span class="sxs-lookup"><span data-stu-id="89778-153">**With data :**</span></span>

            Dictionary<object, object> extras = new Dictionary<object,object>();
            extras.Add("name", "data");
            EngagementAgent.Instance.SendSessionEvent("sessionEvent", extras);

### <a name="job-events"></a><span data-ttu-id="89778-154">Zdarzenia zadań</span><span class="sxs-lookup"><span data-stu-id="89778-154">Job Events</span></span>
#### <a name="reference"></a><span data-ttu-id="89778-155">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="89778-155">Reference</span></span>
            void SendJobEvent(string eventName, string jobName, Dictionary<object, object> extras = null)

<span data-ttu-id="89778-156">Zdarzenia zadania są zazwyczaj używane tooreport hello akcje wykonywane przez użytkownika podczas wykonywania zadania.</span><span class="sxs-lookup"><span data-stu-id="89778-156">Job events are usually used tooreport hello actions performed by a user during a Job.</span></span>

#### <a name="example"></a><span data-ttu-id="89778-157">Przykład</span><span class="sxs-lookup"><span data-stu-id="89778-157">Example</span></span>
            EngagementAgent.Instance.SendJobEvent("eventName", "jobName", extras);

## <a name="reporting-errors"></a><span data-ttu-id="89778-158">Raportowanie błędów</span><span class="sxs-lookup"><span data-stu-id="89778-158">Reporting Errors</span></span>
<span data-ttu-id="89778-159">Brak trzy typy błędów:</span><span class="sxs-lookup"><span data-stu-id="89778-159">There is three types of errors :</span></span>

* <span data-ttu-id="89778-160">Błędy autonomiczny</span><span class="sxs-lookup"><span data-stu-id="89778-160">Standalone errors</span></span>
* <span data-ttu-id="89778-161">Błędy sesji</span><span class="sxs-lookup"><span data-stu-id="89778-161">Session errors</span></span>
* <span data-ttu-id="89778-162">Błędy zadań</span><span class="sxs-lookup"><span data-stu-id="89778-162">Job errors</span></span>

### <a name="standalone-errors"></a><span data-ttu-id="89778-163">Błędy autonomiczny</span><span class="sxs-lookup"><span data-stu-id="89778-163">Standalone errors</span></span>
#### <a name="reference"></a><span data-ttu-id="89778-164">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="89778-164">Reference</span></span>
            void SendError(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="89778-165">Błędy sprzeczne toosession poza hello kontekstu sesji mogą wystąpić błędy autonomicznych.</span><span class="sxs-lookup"><span data-stu-id="89778-165">Contrary toosession errors, standalone errors can occur outside of hello context of a session.</span></span>

#### <a name="example"></a><span data-ttu-id="89778-166">Przykład</span><span class="sxs-lookup"><span data-stu-id="89778-166">Example</span></span>
            EngagementAgent.Instance.SendError("errorName", extras);

### <a name="session-errors"></a><span data-ttu-id="89778-167">Błędy sesji</span><span class="sxs-lookup"><span data-stu-id="89778-167">Session errors</span></span>
#### <a name="reference"></a><span data-ttu-id="89778-168">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="89778-168">Reference</span></span>
            void SendSessionError(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="89778-169">Błędy sesji są błędy hello zwykle używanych tooreport wpływające na powitania użytkownika podczas jego sesji.</span><span class="sxs-lookup"><span data-stu-id="89778-169">Session errors are usually used tooreport hello errors impacting hello user during his session.</span></span>

#### <a name="example"></a><span data-ttu-id="89778-170">Przykład</span><span class="sxs-lookup"><span data-stu-id="89778-170">Example</span></span>
            EngagementAgent.Instance.SendSessionError("errorName", extra);

### <a name="job-errors"></a><span data-ttu-id="89778-171">Błędy zadań</span><span class="sxs-lookup"><span data-stu-id="89778-171">Job Errors</span></span>
#### <a name="reference"></a><span data-ttu-id="89778-172">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="89778-172">Reference</span></span>
            void SendJobError(string errorName, string jobName, Dictionary<object, object> extras = null)

<span data-ttu-id="89778-173">Błędy mogą być powiązane tooa uruchomienia zadania zamiast powiązane toohello bieżącą sesję użytkownika.</span><span class="sxs-lookup"><span data-stu-id="89778-173">Errors can be related tooa running job instead of being related toohello current user session.</span></span>

#### <a name="example"></a><span data-ttu-id="89778-174">Przykład</span><span class="sxs-lookup"><span data-stu-id="89778-174">Example</span></span>
            EngagementAgent.Instance.SendJobError("errorName", "jobname", extra);

## <a name="reporting-crashes"></a><span data-ttu-id="89778-175">Raportowanie awarii (Crash)</span><span class="sxs-lookup"><span data-stu-id="89778-175">Reporting Crashes</span></span>
<span data-ttu-id="89778-176">Hello agent dostarcza dwóch metod toodeal awarii (Crash).</span><span class="sxs-lookup"><span data-stu-id="89778-176">hello agent provides two methods toodeal with crashes.</span></span>

### <a name="send-an-exception"></a><span data-ttu-id="89778-177">Wyślij Wystąpił wyjątek</span><span class="sxs-lookup"><span data-stu-id="89778-177">Send an exception</span></span>
#### <a name="reference"></a><span data-ttu-id="89778-178">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="89778-178">Reference</span></span>
            void SendCrash(Exception e, bool terminateSession = false)

#### <a name="example"></a><span data-ttu-id="89778-179">Przykład</span><span class="sxs-lookup"><span data-stu-id="89778-179">Example</span></span>
<span data-ttu-id="89778-180">Wystąpił wyjątek w dowolnym momencie możesz wysłać przez wywołanie metody:</span><span class="sxs-lookup"><span data-stu-id="89778-180">You can send an exception at any time by calling :</span></span>

            EngagementAgent.Instance.SendCrash(aCatchedException);

<span data-ttu-id="89778-181">Umożliwia także opcjonalny parametr tooterminate hello zaangażowania sesji na powitania tym samym czasie niż wysyłanie hello awarii.</span><span class="sxs-lookup"><span data-stu-id="89778-181">You can also use an optional parameter tooterminate hello engagement session at hello same time than sending hello crash.</span></span> <span data-ttu-id="89778-182">toodo tak, wywołania:</span><span class="sxs-lookup"><span data-stu-id="89778-182">toodo so, call :</span></span>

            EngagementAgent.Instance.SendCrash(new Exception("example"), terminateSession: true);

<span data-ttu-id="89778-183">Jeśli możesz to zrobić, zadania i hello sesji zostanie zamknięte zaraz po awarii hello wysyłania.</span><span class="sxs-lookup"><span data-stu-id="89778-183">If you do that, hello session and jobs will be closed just after sending hello crash.</span></span>

### <a name="send-an-unhandled-exception"></a><span data-ttu-id="89778-184">Wyślij nieobsługiwany wyjątek</span><span class="sxs-lookup"><span data-stu-id="89778-184">Send an unhandled exception</span></span>
#### <a name="reference"></a><span data-ttu-id="89778-185">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="89778-185">Reference</span></span>
            void SendCrash(ApplicationUnhandledExceptionEventArgs e)

<span data-ttu-id="89778-186">Engagement udostępnia również wyjątki toosend nieobsługiwany metody.</span><span class="sxs-lookup"><span data-stu-id="89778-186">Engagement also provides a method toosend unhandled exceptions.</span></span> <span data-ttu-id="89778-187">Jest to szczególnie przydatne, gdy jest używany wewnątrz obsługi zdarzeń UnhandledException silverlight hello.</span><span class="sxs-lookup"><span data-stu-id="89778-187">This is especially useful when used inside hello silverlight UnhandledException event handler.</span></span>

<span data-ttu-id="89778-188">Ta metoda będzie **zawsze** przerwanie hello zaangażowania sesji i zadania po wywołaniu.</span><span class="sxs-lookup"><span data-stu-id="89778-188">This method will **ALWAYS** terminate hello engagement session and jobs after being called.</span></span>

#### <a name="example"></a><span data-ttu-id="89778-189">Przykład</span><span class="sxs-lookup"><span data-stu-id="89778-189">Example</span></span>
<span data-ttu-id="89778-190">Można użyć tooimplement własne obsługi UnhandledException (zwłaszcza, jeśli wyłączono hello awarii automatyczne funkcję zaangażowania raportowania).</span><span class="sxs-lookup"><span data-stu-id="89778-190">You can use it tooimplement your own UnhandledException handler (especially if you have disabled hello automatic crash reporting feature of Engagement).</span></span> <span data-ttu-id="89778-191">Na przykład w hello `Application_UnhandledException` metody hello `App.xaml.cs` pliku:</span><span class="sxs-lookup"><span data-stu-id="89778-191">For example, in hello `Application_UnhandledException` method of hello `App.xaml.cs` file :</span></span>

            // In your App.xaml.cs file

            // Code tooexecute on Unhandled Exceptions
            private void Application_UnhandledException(object sender, ApplicationUnhandledExceptionEventArgs e)
            {
              // your own code

              EngagementAgent.Instance.SendCrash(e);
            }

## <a name="onactivated"></a><span data-ttu-id="89778-192">OnActivated</span><span class="sxs-lookup"><span data-stu-id="89778-192">OnActivated</span></span>
### <a name="reference"></a><span data-ttu-id="89778-193">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="89778-193">Reference</span></span>
            void OnActivated(ActivatedEventArgs e)

<span data-ttu-id="89778-194">Gdy hello użytkownik przechodzi do przodu, od aplikacji, po hello dezaktywowane zdarzenie jest zgłaszane, systemu operacyjnego hello podejmie aplikacji hello tooput stan nieaktywni.</span><span class="sxs-lookup"><span data-stu-id="89778-194">When hello user navigates forward, away from an application, after hello Deactivated event is raised, hello operating system will attempt tooput hello application into a dormant state.</span></span> <span data-ttu-id="89778-195">Następnie aplikacja hello jest chowanie.</span><span class="sxs-lookup"><span data-stu-id="89778-195">Then, hello application is Tombstoning.</span></span> <span data-ttu-id="89778-196">W tym procesie aplikacja zostanie zakończona, ale niektóre dane o stanie hello aplikacji hello i hello poszczególnych stron w aplikacji hello są zachowywane.</span><span class="sxs-lookup"><span data-stu-id="89778-196">In this process an application is terminated but some data about hello state of hello application and hello individual pages within hello application is preserved.</span></span>

<span data-ttu-id="89778-197">Masz tooinsert `EngagementAgent.Instance.OnActivated(e)` w hello `Application_Activated` metody z hello App.xaml.cs pliku tooreset hello agenta zaangażowania, gdy aplikacja hello została schowany.</span><span class="sxs-lookup"><span data-stu-id="89778-197">You have tooinsert `EngagementAgent.Instance.OnActivated(e)` in hello `Application_Activated` method from hello App.xaml.cs file tooreset hello Engagement Agent when hello application has been Tombstoned.</span></span>

### <a name="example"></a><span data-ttu-id="89778-198">Przykład</span><span class="sxs-lookup"><span data-stu-id="89778-198">Example</span></span>
            // Inside your App.xaml.cs file

            // Code tooexecute when hello application is activated (brought tooforeground)
            // This code will not execute when hello application is first launched
            private void Application_Activated(object sender, ActivatedEventArgs e)
            {
              EngagementAgent.Instance.OnActivated(e);
            }

## <a name="device-id"></a><span data-ttu-id="89778-199">Identyfikator urządzenia</span><span class="sxs-lookup"><span data-stu-id="89778-199">Device Id</span></span>
            String GetDeviceId()

<span data-ttu-id="89778-200">Identyfikator urządzenia usługi engagement hello można uzyskać przez wywołanie tej metody.</span><span class="sxs-lookup"><span data-stu-id="89778-200">You can get hello engagement device id by calling this method.</span></span>

## <a name="extras-parameters"></a><span data-ttu-id="89778-201">Dodatkowe parametry</span><span class="sxs-lookup"><span data-stu-id="89778-201">Extras parameters</span></span>
<span data-ttu-id="89778-202">Dowolne dane można zdarzeń dołączonych tooan, błąd, działania lub zadania.</span><span class="sxs-lookup"><span data-stu-id="89778-202">Arbitrary data can be attached tooan event, an error, an activity or a job.</span></span> <span data-ttu-id="89778-203">Dane te mogą być elementami struktury, za pomocą słownika.</span><span class="sxs-lookup"><span data-stu-id="89778-203">These data can be structured using a dictionary.</span></span> <span data-ttu-id="89778-204">Klucze i wartości mogą być dowolnego typu.</span><span class="sxs-lookup"><span data-stu-id="89778-204">Keys and values can be of any type.</span></span>

<span data-ttu-id="89778-205">Dodatkowe dane są serializowane, więc jeśli chcesz tooinsert własne typu w dodatki masz tooadd kontraktu danych dla tego typu.</span><span class="sxs-lookup"><span data-stu-id="89778-205">Extras data are serialized so if you want tooinsert your own type in extras you have tooadd a data contract for this type.</span></span>

### <a name="example"></a><span data-ttu-id="89778-206">Przykład</span><span class="sxs-lookup"><span data-stu-id="89778-206">Example</span></span>
<span data-ttu-id="89778-207">Utworzymy nową klasę "Osoby".</span><span class="sxs-lookup"><span data-stu-id="89778-207">We create a new class "Person".</span></span>

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

<span data-ttu-id="89778-208">Następnie dodamy `Person` dodatkowe tooan wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="89778-208">Then, we will add a `Person` instance tooan extra.</span></span>

            Person person = new Person("Engagement Haddock", 51);
            var extras = new Dictionary<object, object>();
            extras.Add("people", person);

            EngagementAgent.Instance.SendEvent("Event", extras);

> [!WARNING]
> <span data-ttu-id="89778-209">Jeśli inne typy obiektów, upewnij się, że ich metodę ToString() jest implementowane tooreturn człowieka czytelnych ciągów.</span><span class="sxs-lookup"><span data-stu-id="89778-209">If you put other types of objects, make sure their ToString() method is implemented tooreturn a human readable string.</span></span>
> 
> 

### <a name="limits"></a><span data-ttu-id="89778-210">Limity</span><span class="sxs-lookup"><span data-stu-id="89778-210">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="89778-211">Klucze</span><span class="sxs-lookup"><span data-stu-id="89778-211">Keys</span></span>
<span data-ttu-id="89778-212">Każdy klucz w obiekcie hello musi odpowiadać hello następującego wyrażenia regularnego:</span><span class="sxs-lookup"><span data-stu-id="89778-212">Each key in hello object must match hello following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*$`

<span data-ttu-id="89778-213">Oznacza to, że klucze musi rozpoczynać się od co najmniej jedną literą, następują litery, cyfry i znaki podkreślenia (\_).</span><span class="sxs-lookup"><span data-stu-id="89778-213">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="89778-214">Rozmiar</span><span class="sxs-lookup"><span data-stu-id="89778-214">Size</span></span>
<span data-ttu-id="89778-215">Dodatki są zbyt ograniczone**1024** znaków w wywołaniu.</span><span class="sxs-lookup"><span data-stu-id="89778-215">Extras are limited too**1024** characters per call.</span></span>

## <a name="reporting-application-information"></a><span data-ttu-id="89778-216">Raportowanie informacji o aplikacji</span><span class="sxs-lookup"><span data-stu-id="89778-216">Reporting Application Information</span></span>
### <a name="reference"></a><span data-ttu-id="89778-217">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="89778-217">Reference</span></span>
            void SendAppInfo(Dictionary<object, object> appInfos)

<span data-ttu-id="89778-218">Można ręcznie raportu śledzenia informacji (lub innych aplikacji szczegółowych informacji) przy użyciu funkcji SendAppInfo() hello.</span><span class="sxs-lookup"><span data-stu-id="89778-218">You can manually report tracking information (or any other application specific information) using hello SendAppInfo() function.</span></span>

<span data-ttu-id="89778-219">Należy pamiętać, że te informacje mogą zostać przesłane przyrostowo: tylko hello wartość najnowszej dla danego klucza zostaną zachowane dla danego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="89778-219">Note that these information can be sent incrementally: only hello latest value for a given key will be kept for a given device.</span></span> <span data-ttu-id="89778-220">Podobnie jak dodatkowe zdarzenia użycie słownika\<obiektu, obiekt\> tooattach informacje.</span><span class="sxs-lookup"><span data-stu-id="89778-220">Like event extras, use a Dictionary\<object, object\> tooattach informations.</span></span>

### <a name="example"></a><span data-ttu-id="89778-221">Przykład</span><span class="sxs-lookup"><span data-stu-id="89778-221">Example</span></span>
            Dictionary<object, object> appInfo = new Dictionary<object, object>()
            {
               {"subscription", "2013-12-07"},
               {"premium", "true"}
            };

            EngagementAgent.Instance.SendAppInfo(appInfo);

### <a name="limits"></a><span data-ttu-id="89778-222">Limity</span><span class="sxs-lookup"><span data-stu-id="89778-222">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="89778-223">Klucze</span><span class="sxs-lookup"><span data-stu-id="89778-223">Keys</span></span>
<span data-ttu-id="89778-224">Każdy klucz w obiekcie hello musi odpowiadać hello następującego wyrażenia regularnego:</span><span class="sxs-lookup"><span data-stu-id="89778-224">Each key in hello object must match hello following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*$`

<span data-ttu-id="89778-225">Oznacza to, że klucze musi rozpoczynać się od co najmniej jedną literą, następują litery, cyfry i znaki podkreślenia (\_).</span><span class="sxs-lookup"><span data-stu-id="89778-225">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="89778-226">Rozmiar</span><span class="sxs-lookup"><span data-stu-id="89778-226">Size</span></span>
<span data-ttu-id="89778-227">Informacje o aplikacji są zbyt ograniczone**1024** znaków w wywołaniu.</span><span class="sxs-lookup"><span data-stu-id="89778-227">Application information are limited too**1024** characters per call.</span></span>

<span data-ttu-id="89778-228">W hello poprzedni przykład, hello JSON wysyłane toohello serwera jest 44 znaków:</span><span class="sxs-lookup"><span data-stu-id="89778-228">In hello previous example, hello JSON sent toohello server is 44 characters long:</span></span>

            {"subscription":"2013-12-07","premium":"true"}

## <a name="logging"></a><span data-ttu-id="89778-229">Rejestrowanie</span><span class="sxs-lookup"><span data-stu-id="89778-229">Logging</span></span>
### <a name="enable-logging"></a><span data-ttu-id="89778-230">Włączanie rejestrowania</span><span class="sxs-lookup"><span data-stu-id="89778-230">Enable Logging</span></span>
<span data-ttu-id="89778-231">Hello SDK może być skonfigurowany tooproduce dzienników testu w konsoli środowiska IDE hello.</span><span class="sxs-lookup"><span data-stu-id="89778-231">hello SDK can be configured tooproduce test logs in hello IDE console.</span></span>
<span data-ttu-id="89778-232">Dzienniki te nie są uaktywnione domyślnie.</span><span class="sxs-lookup"><span data-stu-id="89778-232">These logs are not activated by default.</span></span> <span data-ttu-id="89778-233">toocustomize ta, właściwość hello aktualizacji `EngagementAgent.Instance.TestLogEnabled` tooone hello wartość dostępna hello `EngagementTestLogLevel` wyliczenia, na przykład:</span><span class="sxs-lookup"><span data-stu-id="89778-233">toocustomize this, update hello property `EngagementAgent.Instance.TestLogEnabled` tooone of hello value available from hello `EngagementTestLogLevel` enumeration, for instance:</span></span>

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();
