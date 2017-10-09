---
title: "Witaj tooUse aaaHow API zaangażowania na uniwersalnych systemu Windows"
description: "Jak tooUse hello API zaangażowania na uniwersalnych systemu Windows"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: bb501fca-9cfe-4495-81df-b5efd6e0137b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 0256b839c28e4ef6c530106408d744038fa711ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-engagement-api-on-windows-universal"></a><span data-ttu-id="620ab-103">Jak tooUse hello API zaangażowania na uniwersalnych systemu Windows</span><span class="sxs-lookup"><span data-stu-id="620ab-103">How tooUse hello Engagement API on Windows Universal</span></span>
<span data-ttu-id="620ab-104">Ten dokument jest dodatek toohello [jak tooIntegrate zaangażowania na uniwersalnych systemu Windows](mobile-engagement-windows-store-integrate-engagement.md): dostarcza w głębokość szczegóły dotyczące sposobu toouse hello tooreport interfejsu API usługi Engagement statystyk aplikacji.</span><span class="sxs-lookup"><span data-stu-id="620ab-104">This document is an add-on toohello document [How tooIntegrate Engagement on Windows Universal](mobile-engagement-windows-store-integrate-engagement.md): it provides in depth details about how toouse hello Engagement API tooreport your application statistics.</span></span>

<span data-ttu-id="620ab-105">Należy pamiętać, że jeśli mają tylko tooreport zaangażowania sesji aplikacji, działań, awarii (Crash) i informacje techniczne, następnie hello Najprostszym sposobem jest toomake wszystkie Twoje `Page` klasy podrzędne dziedziczą hello `EngagementPage` klasy.</span><span class="sxs-lookup"><span data-stu-id="620ab-105">Keep in mind that if you only want Engagement tooreport your application's sessions, activities, crashes and technical information, then hello simplest way is toomake all your `Page` sub-classes inherit from hello `EngagementPage` class.</span></span>

<span data-ttu-id="620ab-106">Jeśli chcesz, aby toodo więcej, na przykład, jeśli potrzebujesz tooreport aplikacji określonych zdarzeń, błędów i zadań, czy masz tooreport działania aplikacji w inny sposób niż jeden zaimplementowana w hello hello `EngagementPage` klas, wówczas należy toouse hello Interfejs API usługi Engagement.</span><span class="sxs-lookup"><span data-stu-id="620ab-106">If you want toodo more, for example if you need tooreport application specific events, errors and jobs, or if you have tooreport your application's activities in a different way than hello one implemented in hello `EngagementPage` classes, then you need toouse hello Engagement API.</span></span>

<span data-ttu-id="620ab-107">Hello zaangażowania interfejsu API jest zapewniana przez hello `EngagementAgent` klasy.</span><span class="sxs-lookup"><span data-stu-id="620ab-107">hello Engagement API is provided by hello `EngagementAgent` class.</span></span> <span data-ttu-id="620ab-108">Można uzyskać dostępu do metody toothose za pośrednictwem `EngagementAgent.Instance`.</span><span class="sxs-lookup"><span data-stu-id="620ab-108">You can access toothose methods through `EngagementAgent.Instance`.</span></span>

<span data-ttu-id="620ab-109">Nawet wtedy, gdy hello agenta modułu nie została zainicjowana, interfejsu API każdego wywołania toohello została odroczona i zostanie wykonana ponownie gdy hello agent jest dostępna.</span><span class="sxs-lookup"><span data-stu-id="620ab-109">Even if hello agent module has not been initialized, each call toohello API is deferred, and will be executed again when hello agent is available.</span></span>

## <a name="engagement-concepts"></a><span data-ttu-id="620ab-110">Pojęcia dotyczące usługi Engagement</span><span class="sxs-lookup"><span data-stu-id="620ab-110">Engagement concepts</span></span>
<span data-ttu-id="620ab-111">Hello następujące części uściślić hello wspólnej [Mobile Engagement pojęcia](mobile-engagement-concepts.md) dla platformy uniwersalnej systemu Windows hello.</span><span class="sxs-lookup"><span data-stu-id="620ab-111">hello following parts refine hello common [Mobile Engagement Concepts](mobile-engagement-concepts.md) for hello Windows Universal platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="620ab-112">`Session` i `Activity`</span><span class="sxs-lookup"><span data-stu-id="620ab-112">`Session` and `Activity`</span></span>
<span data-ttu-id="620ab-113">*Działania* są zwykle skojarzone z jednej strony aplikacji hello, która jest toosay hello *działania* uruchamiana, gdy strona hello jest wyświetlany i zatrzymuje po zamknięciu strony hello: hello w przypadku gdy hello Engagement SDK jest zintegrowany przy użyciu hello `EngagementPage` klasy.</span><span class="sxs-lookup"><span data-stu-id="620ab-113">An *activity* is usually associated with one page of hello application, that is toosay hello *activity* starts when hello page is displayed and stops when hello page is closed: this is hello case when hello Engagement SDK is integrated by using hello `EngagementPage` class.</span></span>

<span data-ttu-id="620ab-114">Ale *działania* można sterować także ręcznie przy użyciu hello interfejsu API usługi Engagement.</span><span class="sxs-lookup"><span data-stu-id="620ab-114">But *activities* can also be controlled manually by using hello Engagement API.</span></span> <span data-ttu-id="620ab-115">Dzięki temu toosplit daną stronę w kilku sub tooget części więcej szczegółów na temat użycia hello tej strony (na przykład częstotliwość tooknow i jak długo okna dialogowe są używane wewnątrz tej strony).</span><span class="sxs-lookup"><span data-stu-id="620ab-115">This allows you toosplit a given page in several sub parts tooget more details about hello usage of this page (for example tooknow how often and how long dialogs are used inside this page).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="620ab-116">Działania raportowania</span><span class="sxs-lookup"><span data-stu-id="620ab-116">Reporting Activities</span></span>
### <a name="user-starts-a-new-activity"></a><span data-ttu-id="620ab-117">Użytkownik uruchamia nowe działanie</span><span class="sxs-lookup"><span data-stu-id="620ab-117">User starts a new Activity</span></span>
#### <a name="reference"></a><span data-ttu-id="620ab-118">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="620ab-118">Reference</span></span>
            void StartActivity(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="620ab-119">Należy toocall `StartActivity()` każde działanie użytkownika hello czasu zmiany.</span><span class="sxs-lookup"><span data-stu-id="620ab-119">You need toocall `StartActivity()` each time hello user activity changes.</span></span> <span data-ttu-id="620ab-120">Hello pierwszej wywołania funkcji toothis uruchamia nową sesję użytkownika.</span><span class="sxs-lookup"><span data-stu-id="620ab-120">hello first call toothis function starts a new user session.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="620ab-121">Hello SDK automatycznie wywołuje metodę EndActivity hello, gdy aplikacja hello jest zamknięty.</span><span class="sxs-lookup"><span data-stu-id="620ab-121">hello SDK automatically calls hello EndActivity method when hello application is closed.</span></span> <span data-ttu-id="620ab-122">W związku z tym zaleca toocall hello StartActivity metody podczas zmiany w natężeniu działań hello hello użytkownika i wywołania tooNEVER hello metody EndActivity, ponieważ wywołanie tej metody wymusza hello toobe bieżąca sesja została zakończona.</span><span class="sxs-lookup"><span data-stu-id="620ab-122">Thus, it is HIGHLY recommended toocall hello StartActivity method whenever hello activity of hello user changes, and tooNEVER call hello EndActivity method, since calling this method forces hello current session toobe ended.</span></span>
> 
> 

#### <a name="example"></a><span data-ttu-id="620ab-123">Przykład</span><span class="sxs-lookup"><span data-stu-id="620ab-123">Example</span></span>
            EngagementAgent.Instance.StartActivity("main", new Dictionary<object, object>() {{"example", "data"}});

### <a name="user-ends-his-current-activity"></a><span data-ttu-id="620ab-124">Użytkownik kończy swoje bieżące działanie</span><span class="sxs-lookup"><span data-stu-id="620ab-124">User ends his current Activity</span></span>
#### <a name="reference"></a><span data-ttu-id="620ab-125">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="620ab-125">Reference</span></span>
            void EndActivity()

<span data-ttu-id="620ab-126">Kończy działanie hello i hello sesji.</span><span class="sxs-lookup"><span data-stu-id="620ab-126">This ends hello activity and hello session.</span></span> <span data-ttu-id="620ab-127">Nie należy wywołać tej metody, znając naprawdę wykonywanych czynności.</span><span class="sxs-lookup"><span data-stu-id="620ab-127">You should not call this method unless you really know what you're doing.</span></span>

#### <a name="example"></a><span data-ttu-id="620ab-128">Przykład</span><span class="sxs-lookup"><span data-stu-id="620ab-128">Example</span></span>
            EngagementAgent.Instance.EndActivity();

## <a name="reporting-jobs"></a><span data-ttu-id="620ab-129">Zadania raportowania</span><span class="sxs-lookup"><span data-stu-id="620ab-129">Reporting Jobs</span></span>
### <a name="start-a-job"></a><span data-ttu-id="620ab-130">Uruchom zadanie</span><span class="sxs-lookup"><span data-stu-id="620ab-130">Start a job</span></span>
#### <a name="reference"></a><span data-ttu-id="620ab-131">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="620ab-131">Reference</span></span>
            void StartJob(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="620ab-132">Podaje tootrack zadania hello można użyć w danym okresie czasu.</span><span class="sxs-lookup"><span data-stu-id="620ab-132">You can use hello job tootrack certains tasks over a period of time.</span></span>

#### <a name="example"></a><span data-ttu-id="620ab-133">Przykład</span><span class="sxs-lookup"><span data-stu-id="620ab-133">Example</span></span>
            // An upload begins...

            // Set hello extras
            var extras = new Dictionary<object, object>();
            extras.Add("title", "avatar");
            extras.Add("type", "image");

            EngagementAgent.Instance.StartJob("uploadData", extras);

### <a name="end-a-job"></a><span data-ttu-id="620ab-134">Zakończenia zadania</span><span class="sxs-lookup"><span data-stu-id="620ab-134">End a job</span></span>
#### <a name="reference"></a><span data-ttu-id="620ab-135">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="620ab-135">Reference</span></span>
            void EndJob(string name)

<span data-ttu-id="620ab-136">Jak zadanie śledzone przez zadanie zostało zakończone, powinien wywoływać metodę EndJob powitania dla tego zadania, podając nazwę zadania hello.</span><span class="sxs-lookup"><span data-stu-id="620ab-136">As soon as a task tracked by a job has been terminated, you should call hello EndJob method for this job, by supplying hello job name.</span></span>

#### <a name="example"></a><span data-ttu-id="620ab-137">Przykład</span><span class="sxs-lookup"><span data-stu-id="620ab-137">Example</span></span>
            // In hello previous section, we started an upload tracking with a job
            // Then, hello upload ends

            EngagementAgent.Instance.EndJob("uploadData");

## <a name="reporting-events"></a><span data-ttu-id="620ab-138">Zdarzenia raportowania</span><span class="sxs-lookup"><span data-stu-id="620ab-138">Reporting Events</span></span>
<span data-ttu-id="620ab-139">Brak trzy typy zdarzeń:</span><span class="sxs-lookup"><span data-stu-id="620ab-139">There is three types of events :</span></span>

* <span data-ttu-id="620ab-140">Autonomiczny zdarzenia</span><span class="sxs-lookup"><span data-stu-id="620ab-140">Standalone events</span></span>
* <span data-ttu-id="620ab-141">Zdarzenia sesji</span><span class="sxs-lookup"><span data-stu-id="620ab-141">Session events</span></span>
* <span data-ttu-id="620ab-142">Zdarzenia zadań</span><span class="sxs-lookup"><span data-stu-id="620ab-142">Job events</span></span>

### <a name="standalone-events"></a><span data-ttu-id="620ab-143">Autonomiczny zdarzenia</span><span class="sxs-lookup"><span data-stu-id="620ab-143">Standalone Events</span></span>
#### <a name="reference"></a><span data-ttu-id="620ab-144">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="620ab-144">Reference</span></span>
            void SendEvent(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="620ab-145">Autonomiczny zdarzeń może wystąpić poza hello kontekstu sesji.</span><span class="sxs-lookup"><span data-stu-id="620ab-145">Standalone events can occur outside of hello context of a session.</span></span>

#### <a name="example"></a><span data-ttu-id="620ab-146">Przykład</span><span class="sxs-lookup"><span data-stu-id="620ab-146">Example</span></span>
            EngagementAgent.Instance.SendEvent("event", extra);

### <a name="session-events"></a><span data-ttu-id="620ab-147">Zdarzenia sesji</span><span class="sxs-lookup"><span data-stu-id="620ab-147">Session events</span></span>
#### <a name="reference"></a><span data-ttu-id="620ab-148">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="620ab-148">Reference</span></span>
            void SendSessionEvent(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="620ab-149">Zdarzenia sesji są zazwyczaj używane tooreport hello akcje wykonywane przez użytkownika podczas jego sesji.</span><span class="sxs-lookup"><span data-stu-id="620ab-149">Session events are usually used tooreport hello actions performed by a user during his session.</span></span>

#### <a name="example"></a><span data-ttu-id="620ab-150">Przykład</span><span class="sxs-lookup"><span data-stu-id="620ab-150">Example</span></span>
<span data-ttu-id="620ab-151">**Bez danych:**</span><span class="sxs-lookup"><span data-stu-id="620ab-151">**Without data :**</span></span>

            EngagementAgent.Instance.SendSessionEvent("sessionEvent");

            // or

            EngagementAgent.Instance.SendSessionEvent("sessionEvent", null);

<span data-ttu-id="620ab-152">**Z danymi:**</span><span class="sxs-lookup"><span data-stu-id="620ab-152">**With data :**</span></span>

            Dictionary<object, object> extras = new Dictionary<object,object>();
            extras.Add("name", "data");
            EngagementAgent.Instance.SendSessionEvent("sessionEvent", extras);

### <a name="job-events"></a><span data-ttu-id="620ab-153">Zdarzenia zadań</span><span class="sxs-lookup"><span data-stu-id="620ab-153">Job Events</span></span>
#### <a name="reference"></a><span data-ttu-id="620ab-154">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="620ab-154">Reference</span></span>
            void SendJobEvent(string eventName, string jobName, Dictionary<object, object> extras = null)

<span data-ttu-id="620ab-155">Zdarzenia zadania są zazwyczaj używane tooreport hello akcje wykonywane przez użytkownika podczas wykonywania zadania.</span><span class="sxs-lookup"><span data-stu-id="620ab-155">Job events are usually used tooreport hello actions performed by a user during a Job.</span></span>

#### <a name="example"></a><span data-ttu-id="620ab-156">Przykład</span><span class="sxs-lookup"><span data-stu-id="620ab-156">Example</span></span>
            EngagementAgent.Instance.SendJobEvent("eventName", "jobName", extras);

## <a name="reporting-errors"></a><span data-ttu-id="620ab-157">Raportowanie błędów</span><span class="sxs-lookup"><span data-stu-id="620ab-157">Reporting Errors</span></span>
<span data-ttu-id="620ab-158">Istnieją trzy typy błędów:</span><span class="sxs-lookup"><span data-stu-id="620ab-158">There are three types of errors :</span></span>

* <span data-ttu-id="620ab-159">Błędy autonomiczny</span><span class="sxs-lookup"><span data-stu-id="620ab-159">Standalone errors</span></span>
* <span data-ttu-id="620ab-160">Błędy sesji</span><span class="sxs-lookup"><span data-stu-id="620ab-160">Session errors</span></span>
* <span data-ttu-id="620ab-161">Błędy zadań</span><span class="sxs-lookup"><span data-stu-id="620ab-161">Job errors</span></span>

### <a name="standalone-errors"></a><span data-ttu-id="620ab-162">Błędy autonomiczny</span><span class="sxs-lookup"><span data-stu-id="620ab-162">Standalone errors</span></span>
#### <a name="reference"></a><span data-ttu-id="620ab-163">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="620ab-163">Reference</span></span>
            void SendError(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="620ab-164">Błędy sprzeczne toosession poza hello kontekstu sesji mogą wystąpić błędy autonomicznych.</span><span class="sxs-lookup"><span data-stu-id="620ab-164">Contrary toosession errors, standalone errors can occur outside of hello context of a session.</span></span>

#### <a name="example"></a><span data-ttu-id="620ab-165">Przykład</span><span class="sxs-lookup"><span data-stu-id="620ab-165">Example</span></span>
            EngagementAgent.Instance.SendError("errorName", extras);

### <a name="session-errors"></a><span data-ttu-id="620ab-166">Błędy sesji</span><span class="sxs-lookup"><span data-stu-id="620ab-166">Session errors</span></span>
#### <a name="reference"></a><span data-ttu-id="620ab-167">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="620ab-167">Reference</span></span>
            void SendSessionError(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="620ab-168">Błędy sesji są błędy hello zwykle używanych tooreport wpływające na powitania użytkownika podczas jego sesji.</span><span class="sxs-lookup"><span data-stu-id="620ab-168">Session errors are usually used tooreport hello errors impacting hello user during his session.</span></span>

#### <a name="example"></a><span data-ttu-id="620ab-169">Przykład</span><span class="sxs-lookup"><span data-stu-id="620ab-169">Example</span></span>
            EngagementAgent.Instance.SendSessionError("errorName", extra);

### <a name="job-errors"></a><span data-ttu-id="620ab-170">Błędy zadań</span><span class="sxs-lookup"><span data-stu-id="620ab-170">Job Errors</span></span>
#### <a name="reference"></a><span data-ttu-id="620ab-171">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="620ab-171">Reference</span></span>
            void SendJobError(string errorName, string jobName, Dictionary<object, object> extras = null)

<span data-ttu-id="620ab-172">Błędy mogą być powiązane tooa uruchomienia zadania zamiast powiązane toohello bieżącą sesję użytkownika.</span><span class="sxs-lookup"><span data-stu-id="620ab-172">Errors can be related tooa running job instead of being related toohello current user session.</span></span>

#### <a name="example"></a><span data-ttu-id="620ab-173">Przykład</span><span class="sxs-lookup"><span data-stu-id="620ab-173">Example</span></span>
            EngagementAgent.Instance.SendJobError("errorName", "jobname", extra);

## <a name="reporting-crashes"></a><span data-ttu-id="620ab-174">Raportowanie awarii (Crash)</span><span class="sxs-lookup"><span data-stu-id="620ab-174">Reporting Crashes</span></span>
<span data-ttu-id="620ab-175">Hello agent dostarcza dwóch metod toodeal awarii (Crash).</span><span class="sxs-lookup"><span data-stu-id="620ab-175">hello agent provides two methods toodeal with crashes.</span></span>

### <a name="send-an-exception"></a><span data-ttu-id="620ab-176">Wyślij Wystąpił wyjątek</span><span class="sxs-lookup"><span data-stu-id="620ab-176">Send an exception</span></span>
#### <a name="reference"></a><span data-ttu-id="620ab-177">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="620ab-177">Reference</span></span>
            void SendCrash(Exception e, bool terminateSession = false)

#### <a name="example"></a><span data-ttu-id="620ab-178">Przykład</span><span class="sxs-lookup"><span data-stu-id="620ab-178">Example</span></span>
<span data-ttu-id="620ab-179">Wystąpił wyjątek w dowolnym momencie możesz wysłać przez wywołanie metody:</span><span class="sxs-lookup"><span data-stu-id="620ab-179">You can send an exception at any time by calling :</span></span>

            EngagementAgent.Instance.SendCrash(aCatchedException);

<span data-ttu-id="620ab-180">Umożliwia także opcjonalny parametr tooterminate hello zaangażowania sesji na powitania tym samym czasie niż wysyłanie hello awarii.</span><span class="sxs-lookup"><span data-stu-id="620ab-180">You can also use an optional parameter tooterminate hello engagement session at hello same time than sending hello crash.</span></span> <span data-ttu-id="620ab-181">toodo tak, wywołania:</span><span class="sxs-lookup"><span data-stu-id="620ab-181">toodo so, call :</span></span>

            EngagementAgent.Instance.SendCrash(new Exception("example"), terminateSession: true);

<span data-ttu-id="620ab-182">Jeśli możesz to zrobić, zadania i hello sesji zostanie zamknięte zaraz po awarii hello wysyłania.</span><span class="sxs-lookup"><span data-stu-id="620ab-182">If you do that, hello session and jobs will be closed just after sending hello crash.</span></span>

### <a name="send-an-unhandled-exception"></a><span data-ttu-id="620ab-183">Wyślij nieobsługiwany wyjątek</span><span class="sxs-lookup"><span data-stu-id="620ab-183">Send an unhandled exception</span></span>
#### <a name="reference"></a><span data-ttu-id="620ab-184">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="620ab-184">Reference</span></span>
            void SendCrash(Exception e)

<span data-ttu-id="620ab-185">Jeśli masz zaangażowania również zapewnia wyjątki toosend nieobsługiwany — metoda **wyłączone** automatyczne zaangażowania **awarii** raportowania.</span><span class="sxs-lookup"><span data-stu-id="620ab-185">Engagement also provides a method toosend unhandled exceptions if you have **DISABLED** Engagement automatic **crash** reporting.</span></span> <span data-ttu-id="620ab-186">Jest to szczególnie przydatne, gdy jest używany wewnątrz obsługi zdarzeń UnhandledException aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="620ab-186">This is especially useful when used inside hello application UnhandledException event handler.</span></span>

<span data-ttu-id="620ab-187">Ta metoda będzie **zawsze** przerwanie hello zaangażowania sesji i zadania po wywołaniu.</span><span class="sxs-lookup"><span data-stu-id="620ab-187">This method will **ALWAYS** terminate hello engagement session and jobs after being called.</span></span>

#### <a name="example"></a><span data-ttu-id="620ab-188">Przykład</span><span class="sxs-lookup"><span data-stu-id="620ab-188">Example</span></span>
<span data-ttu-id="620ab-189">Można użyć tooimplement własne UnhandledExceptionEventArgs programu obsługi.</span><span class="sxs-lookup"><span data-stu-id="620ab-189">You can use it tooimplement your own UnhandledExceptionEventArgs handler.</span></span> <span data-ttu-id="620ab-190">Na przykład dodać hello `Current_UnhandledException` metody hello `App.xaml.cs` pliku:</span><span class="sxs-lookup"><span data-stu-id="620ab-190">For example, add hello `Current_UnhandledException` method of hello `App.xaml.cs` file :</span></span>

            // In your App.xaml.cs file

            // Code tooexecute on Unhandled Exceptions
            void Current_UnhandledException(object sender, UnhandledExceptionEventArgs e)
            {
               EngagementAgent.Instance.SendCrash(e.Exception,false);
            }

<span data-ttu-id="620ab-191">W pliku App.xaml.cs "Publicznego App() {}" należy dodać:</span><span class="sxs-lookup"><span data-stu-id="620ab-191">In App.xaml.cs in "Public App(){}" add:</span></span>

            Application.Current.UnhandledException += Current_UnhandledException;

## <a name="device-id"></a><span data-ttu-id="620ab-192">Identyfikator urządzenia</span><span class="sxs-lookup"><span data-stu-id="620ab-192">Device Id</span></span>
            String EngagementAgent.Instance.GetDeviceId()

<span data-ttu-id="620ab-193">Identyfikator urządzenia usługi engagement hello można uzyskać przez wywołanie tej metody.</span><span class="sxs-lookup"><span data-stu-id="620ab-193">You can get hello engagement device id by calling this method.</span></span>

## <a name="extras-parameters"></a><span data-ttu-id="620ab-194">Dodatkowe parametry</span><span class="sxs-lookup"><span data-stu-id="620ab-194">Extras parameters</span></span>
<span data-ttu-id="620ab-195">Dowolne dane można zdarzeń dołączonych tooan, błąd, działania lub zadania.</span><span class="sxs-lookup"><span data-stu-id="620ab-195">Arbitrary data can be attached tooan event, an error, an activity or a job.</span></span> <span data-ttu-id="620ab-196">Dane te mogą być elementami struktury, za pomocą słownika.</span><span class="sxs-lookup"><span data-stu-id="620ab-196">These data can be structured using a dictionary.</span></span> <span data-ttu-id="620ab-197">Klucze i wartości mogą być dowolnego typu.</span><span class="sxs-lookup"><span data-stu-id="620ab-197">Keys and values can be of any type.</span></span>

<span data-ttu-id="620ab-198">Dodatkowe dane są serializowane, więc jeśli chcesz tooinsert własne typu w dodatki masz tooadd kontraktu danych dla tego typu.</span><span class="sxs-lookup"><span data-stu-id="620ab-198">Extras data are serialized so if you want tooinsert your own type in extras you have tooadd a data contract for this type.</span></span>

### <a name="example"></a><span data-ttu-id="620ab-199">Przykład</span><span class="sxs-lookup"><span data-stu-id="620ab-199">Example</span></span>
<span data-ttu-id="620ab-200">Utworzymy nową klasę "Osoby".</span><span class="sxs-lookup"><span data-stu-id="620ab-200">We create a new class "Person".</span></span>

            using System.Runtime.Serialization;

            namespace Microsoft.Azure.Engagement
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

<span data-ttu-id="620ab-201">Następnie dodamy `Person` dodatkowe tooan wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="620ab-201">Then, we will add a `Person` instance tooan extra.</span></span>

            Person person = new Person("Engagement Haddock", 51);
            var extras = new Dictionary<object, object>();
            extras.Add("people", person);

            EngagementAgent.Instance.SendEvent("Event", extras);

> [!WARNING]
> <span data-ttu-id="620ab-202">Jeśli inne typy obiektów, upewnij się, że ich metodę ToString() jest implementowane tooreturn człowieka czytelnych ciągów.</span><span class="sxs-lookup"><span data-stu-id="620ab-202">If you put other types of objects, make sure their ToString() method is implemented tooreturn a human readable string.</span></span>
> 
> 

### <a name="limits"></a><span data-ttu-id="620ab-203">Limity</span><span class="sxs-lookup"><span data-stu-id="620ab-203">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="620ab-204">Klucze</span><span class="sxs-lookup"><span data-stu-id="620ab-204">Keys</span></span>
<span data-ttu-id="620ab-205">Każdy klucz w obiekcie hello musi odpowiadać hello następującego wyrażenia regularnego:</span><span class="sxs-lookup"><span data-stu-id="620ab-205">Each key in hello object must match hello following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*$`

<span data-ttu-id="620ab-206">Oznacza to, że klucze musi rozpoczynać się od co najmniej jedną literą, następują litery, cyfry i znaki podkreślenia (\_).</span><span class="sxs-lookup"><span data-stu-id="620ab-206">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="620ab-207">Rozmiar</span><span class="sxs-lookup"><span data-stu-id="620ab-207">Size</span></span>
<span data-ttu-id="620ab-208">Dodatki są zbyt ograniczone**1024** znaków w wywołaniu.</span><span class="sxs-lookup"><span data-stu-id="620ab-208">Extras are limited too**1024** characters per call.</span></span>

## <a name="reporting-application-information"></a><span data-ttu-id="620ab-209">Raportowanie informacji o aplikacji</span><span class="sxs-lookup"><span data-stu-id="620ab-209">Reporting Application Information</span></span>
### <a name="reference"></a><span data-ttu-id="620ab-210">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="620ab-210">Reference</span></span>
            void SendAppInfo(Dictionary<object, object> appInfos)

<span data-ttu-id="620ab-211">Można ręcznie raportu śledzenia informacji (lub innych aplikacji szczegółowych informacji) przy użyciu funkcji SendAppInfo() hello.</span><span class="sxs-lookup"><span data-stu-id="620ab-211">You can manually report tracking information (or any other application specific information) using hello SendAppInfo() function.</span></span>

<span data-ttu-id="620ab-212">Należy pamiętać, że te dane mogą być wysyłane przyrostowo: tylko hello wartość najnowszej dla danego klucza zostaną zachowane dla danego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="620ab-212">Note that this data can be sent incrementally: only hello latest value for a given key will be kept for a given device.</span></span> <span data-ttu-id="620ab-213">Podobnie jak dodatkowe zdarzenia użycie słownika\<obiektu, obiekt\> tooattach danych.</span><span class="sxs-lookup"><span data-stu-id="620ab-213">Like event extras, use a Dictionary\<object, object\> tooattach data.</span></span>

### <a name="example"></a><span data-ttu-id="620ab-214">Przykład</span><span class="sxs-lookup"><span data-stu-id="620ab-214">Example</span></span>
            Dictionary<object, object> appInfo = new Dictionary<object, object>()
              {
                {"birthdate", "1983-12-07"},
                {"gender", "female"}
              };

            EngagementAgent.Instance.SendAppInfo(appInfo);

### <a name="limits"></a><span data-ttu-id="620ab-215">Limity</span><span class="sxs-lookup"><span data-stu-id="620ab-215">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="620ab-216">Klucze</span><span class="sxs-lookup"><span data-stu-id="620ab-216">Keys</span></span>
<span data-ttu-id="620ab-217">Każdy klucz w obiekcie hello musi odpowiadać hello następującego wyrażenia regularnego:</span><span class="sxs-lookup"><span data-stu-id="620ab-217">Each key in hello object must match hello following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*$`

<span data-ttu-id="620ab-218">Oznacza to, że klucze musi rozpoczynać się od co najmniej jedną literą, następują litery, cyfry i znaki podkreślenia (\_).</span><span class="sxs-lookup"><span data-stu-id="620ab-218">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="620ab-219">Rozmiar</span><span class="sxs-lookup"><span data-stu-id="620ab-219">Size</span></span>
<span data-ttu-id="620ab-220">Informacje o aplikacji są zbyt ograniczone**1024** znaków w wywołaniu.</span><span class="sxs-lookup"><span data-stu-id="620ab-220">Application information is limited too**1024** characters per call.</span></span>

<span data-ttu-id="620ab-221">W hello poprzedni przykład, hello JSON wysyłane toohello serwera jest 44 znaków:</span><span class="sxs-lookup"><span data-stu-id="620ab-221">In hello previous example, hello JSON sent toohello server is 44 characters long:</span></span>

            {"birthdate":"1983-12-07","gender":"female"}

## <a name="logging"></a><span data-ttu-id="620ab-222">Rejestrowanie</span><span class="sxs-lookup"><span data-stu-id="620ab-222">Logging</span></span>
### <a name="enable-logging"></a><span data-ttu-id="620ab-223">Włączanie rejestrowania</span><span class="sxs-lookup"><span data-stu-id="620ab-223">Enable Logging</span></span>
<span data-ttu-id="620ab-224">Hello SDK może być skonfigurowany tooproduce dzienników testu w konsoli środowiska IDE hello.</span><span class="sxs-lookup"><span data-stu-id="620ab-224">hello SDK can be configured tooproduce test logs in hello IDE console.</span></span>
<span data-ttu-id="620ab-225">Dzienniki te nie są uaktywnione domyślnie.</span><span class="sxs-lookup"><span data-stu-id="620ab-225">These logs are not activated by default.</span></span> <span data-ttu-id="620ab-226">toocustomize ta, właściwość hello aktualizacji `EngagementAgent.Instance.TestLogEnabled` tooone hello wartość dostępna hello `EngagementTestLogLevel` wyliczenia, na przykład:</span><span class="sxs-lookup"><span data-stu-id="620ab-226">toocustomize this, update hello property `EngagementAgent.Instance.TestLogEnabled` tooone of hello value available from hello `EngagementTestLogLevel` enumeration, for instance:</span></span>

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

