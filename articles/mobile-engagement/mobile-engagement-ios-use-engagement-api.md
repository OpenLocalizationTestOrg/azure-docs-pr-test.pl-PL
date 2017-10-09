---
title: "aaaHow tooUse hello zaangażowania interfejsu API w systemie iOS"
description: "Najnowsze iOS SDK — jak tooUse hello zaangażowania interfejsu API w systemie iOS"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 1fb4509e-3804-46c1-949f-1cf727f91f9f
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 7fb9b95ad319cf3b1e2de81b5d6aee5b30266069
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-engagement-api-on-ios"></a><span data-ttu-id="28e5f-103">Jak tooUse hello zaangażowania interfejsu API w systemie iOS</span><span class="sxs-lookup"><span data-stu-id="28e5f-103">How tooUse hello Engagement API on iOS</span></span>
<span data-ttu-id="28e5f-104">Ten dokument jest dodatek toohello jak tooIntegrate zaangażowania w systemie iOS: dostarcza w głębokość szczegóły dotyczące sposobu toouse hello tooreport interfejsu API usługi Engagement statystyk aplikacji.</span><span class="sxs-lookup"><span data-stu-id="28e5f-104">This document is an add-on toohello document How tooIntegrate Engagement on iOS: it provides in depth details about how toouse hello Engagement API tooreport your application statistics.</span></span>

<span data-ttu-id="28e5f-105">Należy pamiętać, że jeśli mają tylko tooreport zaangażowania sesji aplikacji, działań, awarii (Crash) i informacje techniczne, następnie hello najprostszy sposób jest toomake wszystkie niestandardowe `UIViewController` obiekty dziedziczyć odpowiadającego hello `EngagementViewController` — klasa .</span><span class="sxs-lookup"><span data-stu-id="28e5f-105">Keep in mind that if you only want Engagement tooreport your application's sessions, activities, crashes and technical information, then hello simplest way is toomake all your custom `UIViewController` objects inherit from hello corresponding `EngagementViewController` class.</span></span>

<span data-ttu-id="28e5f-106">Jeśli chcesz, aby toodo więcej, na przykład, jeśli potrzebujesz tooreport aplikacji określonych zdarzeń, błędów i zadań, czy masz tooreport działania aplikacji w inny sposób niż jeden zaimplementowana w hello hello `EngagementViewController` klas, wówczas należy toouse hello Interfejs API usługi Engagement.</span><span class="sxs-lookup"><span data-stu-id="28e5f-106">If you want toodo more, for example if you need tooreport application specific events, errors and jobs, or if you have tooreport your application's activities in a different way than hello one implemented in hello `EngagementViewController` classes, then you need toouse hello Engagement API.</span></span>

<span data-ttu-id="28e5f-107">Hello zaangażowania interfejsu API jest zapewniana przez hello `EngagementAgent` klasy.</span><span class="sxs-lookup"><span data-stu-id="28e5f-107">hello Engagement API is provided by hello `EngagementAgent` class.</span></span> <span data-ttu-id="28e5f-108">Wystąpienie tej klasy może być pobierane przez wywołanie hello `[EngagementAgent shared]` metody statycznej (należy pamiętać, że hello `EngagementAgent` obiektu zwróconego jest pojedyncza).</span><span class="sxs-lookup"><span data-stu-id="28e5f-108">An instance of this class can be retrieved by calling hello `[EngagementAgent shared]` static method (note that hello `EngagementAgent` object returned is a singleton).</span></span>

<span data-ttu-id="28e5f-109">Zanim wszystkie wywołania interfejsu API, hello `EngagementAgent` obiekt musi zostać zainicjowany przez wywołanie metody hello`[EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];`</span><span class="sxs-lookup"><span data-stu-id="28e5f-109">Before any API calls, hello `EngagementAgent` object must be initialized by calling hello method `[EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];`</span></span>

## <a name="engagement-concepts"></a><span data-ttu-id="28e5f-110">Pojęcia dotyczące usługi Engagement</span><span class="sxs-lookup"><span data-stu-id="28e5f-110">Engagement concepts</span></span>
<span data-ttu-id="28e5f-111">Hello następujące części uściślić hello wspólnej [Mobile Engagement pojęcia](mobile-engagement-concepts.md) dla platformy iOS hello.</span><span class="sxs-lookup"><span data-stu-id="28e5f-111">hello following parts refine hello common [Mobile Engagement Concepts](mobile-engagement-concepts.md) for hello iOS platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="28e5f-112">`Session` i `Activity`</span><span class="sxs-lookup"><span data-stu-id="28e5f-112">`Session` and `Activity`</span></span>
<span data-ttu-id="28e5f-113">*Działania* są zwykle skojarzone z jednego ekranu aplikacji hello, która jest toosay hello *działania* uruchamiana, gdy hello ekran jest wyświetlany i zatrzymuje po zamknięciu ekranu hello: hello jest przypadek, kiedy Witaj Engagement SDK jest zintegrowany przy użyciu hello `EngagementViewController` klasy.</span><span class="sxs-lookup"><span data-stu-id="28e5f-113">An *activity* is usually associated with one screen of hello application, that is toosay hello *activity* starts when hello screen is displayed and stops when hello screen is closed: this is hello case when hello Engagement SDK is integrated by using hello `EngagementViewController` classes.</span></span>

<span data-ttu-id="28e5f-114">Ale *działania* można sterować także ręcznie przy użyciu hello interfejsu API usługi Engagement.</span><span class="sxs-lookup"><span data-stu-id="28e5f-114">But *activities* can also be controlled manually by using hello Engagement API.</span></span> <span data-ttu-id="28e5f-115">Umożliwia to toosplit danego ekranu w kilku tooget części sub więcej szczegółów na temat hello użycia tego ekranu (na przykład częstotliwość tooknown i jak długo okna dialogowe są używane wewnątrz tego ekranu).</span><span class="sxs-lookup"><span data-stu-id="28e5f-115">This allows toosplit a given screen in several sub parts tooget more details about hello usage of this screen (for example tooknown how often and how long dialogs are used inside this screen).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="28e5f-116">Działania raportowania</span><span class="sxs-lookup"><span data-stu-id="28e5f-116">Reporting Activities</span></span>
### <a name="user-starts-a-new-activity"></a><span data-ttu-id="28e5f-117">Użytkownik uruchamia nowe działanie</span><span class="sxs-lookup"><span data-stu-id="28e5f-117">User starts a new Activity</span></span>
            [[EngagementAgent shared] startActivity:@"MyUserActivity" extras:nil];

<span data-ttu-id="28e5f-118">Należy toocall `startActivity()` każde działanie użytkownika hello czasu zmiany.</span><span class="sxs-lookup"><span data-stu-id="28e5f-118">You need toocall `startActivity()` each time hello user activity changes.</span></span> <span data-ttu-id="28e5f-119">Hello pierwszej wywołania funkcji toothis uruchamia nową sesję użytkownika.</span><span class="sxs-lookup"><span data-stu-id="28e5f-119">hello first call toothis function starts a new user session.</span></span>

### <a name="user-ends-his-current-activity"></a><span data-ttu-id="28e5f-120">Użytkownik kończy swoje bieżące działanie</span><span class="sxs-lookup"><span data-stu-id="28e5f-120">User ends his current Activity</span></span>
            [[EngagementAgent shared] endActivity];

> [!WARNING]
> <span data-ttu-id="28e5f-121">Należy **nigdy** wywołanie tej funkcji przez użytkownika, z wyjątkiem, jeśli chcesz, aby toosplit jedno użycie aplikacji na kilka sesji: wywołanie funkcji toothis spowodowałoby zakończenie hello bieżącej sesji, dlatego kolejne wywołanie za`startActivity()`czy Rozpocznij nową sesję.</span><span class="sxs-lookup"><span data-stu-id="28e5f-121">You should **NEVER** call this function by yourself, except if you want toosplit one use of your application into several sessions: a call toothis function would end hello current session immediately, so, a subsequent call too`startActivity()` would start a new session.</span></span> <span data-ttu-id="28e5f-122">Ta funkcja jest wywoływana automatycznie przez hello zestawu SDK, po zamknięciu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="28e5f-122">This function is automatically called by hello SDK when your application is closed.</span></span>
> 
> 

## <a name="reporting-events"></a><span data-ttu-id="28e5f-123">Zdarzenia raportowania</span><span class="sxs-lookup"><span data-stu-id="28e5f-123">Reporting Events</span></span>
### <a name="session-events"></a><span data-ttu-id="28e5f-124">Zdarzenia sesji</span><span class="sxs-lookup"><span data-stu-id="28e5f-124">Session events</span></span>
<span data-ttu-id="28e5f-125">Zdarzenia sesji są zazwyczaj używane tooreport hello akcje wykonywane przez użytkownika podczas jego sesji.</span><span class="sxs-lookup"><span data-stu-id="28e5f-125">Session events are usually used tooreport hello actions performed by a user during his session.</span></span>

<span data-ttu-id="28e5f-126">**Przykład bez dodatkowe dane:**</span><span class="sxs-lookup"><span data-stu-id="28e5f-126">**Example without extra data:**</span></span>

    @implementation MyViewController {
       [...]
       - (void)willRotateToInterfaceOrientation:(UIInterfaceOrientation)toInterfaceOrientation duration:(NSTimeInterval)duration
       {
        [super willRotateToInterfaceOrientation:toInterfaceOrientation duration:duration];
            ...
        [[EngagementAgent shared] sendSessionEvent:@"will_rotate" extras:nil];
            ...
       }
       [...]
    }

<span data-ttu-id="28e5f-127">**Przykład: dodatkowe dane:**</span><span class="sxs-lookup"><span data-stu-id="28e5f-127">**Example with extra data:**</span></span>

    @implementation MyViewController {
       [...]
       - (void)willRotateToInterfaceOrientation:(UIInterfaceOrientation)toInterfaceOrientation duration:(NSTimeInterval)duration
       {
        [super willRotateToInterfaceOrientation:toInterfaceOrientation duration:duration];
            ...
        NSMutableDictionary* extras = [NSMutableDictionary dictionary];
        [extras setObject:[NSNumber numberWithInt:toInterfaceOrientation] forKey:@"to_orientation_id"];
        [extras setObject:[NSNumber numberWithDouble:duration] forKey:@"duration"];
        [[EngagementAgent shared] sendSessionEvent:@"will_rotate" extras:extras];
            ...
       }
       [...]
    }

### <a name="standalone-events"></a><span data-ttu-id="28e5f-128">Autonomiczny zdarzenia</span><span class="sxs-lookup"><span data-stu-id="28e5f-128">Standalone events</span></span>
<span data-ttu-id="28e5f-129">Zdarzenia toosession inaczej, zdarzenia autonomiczny można poza hello kontekstu sesji.</span><span class="sxs-lookup"><span data-stu-id="28e5f-129">Contrary toosession events, standalone events can be used outside of hello context of a session.</span></span>

<span data-ttu-id="28e5f-130">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="28e5f-130">**Example:**</span></span>

    [[EngagementAgent shared] sendEvent:@"received_notification" extras:nil];

## <a name="reporting-errors"></a><span data-ttu-id="28e5f-131">Raportowanie błędów</span><span class="sxs-lookup"><span data-stu-id="28e5f-131">Reporting Errors</span></span>
### <a name="session-errors"></a><span data-ttu-id="28e5f-132">Błędy sesji</span><span class="sxs-lookup"><span data-stu-id="28e5f-132">Session errors</span></span>
<span data-ttu-id="28e5f-133">Błędy sesji są błędy hello zwykle używanych tooreport wpływające na powitania użytkownika podczas jego sesji.</span><span class="sxs-lookup"><span data-stu-id="28e5f-133">Session errors are usually used tooreport hello errors impacting hello user during his session.</span></span>

<span data-ttu-id="28e5f-134">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="28e5f-134">**Example:**</span></span>

    /** hello user has entered invalid data in a form */
    @implementation MyViewController {
      [...]
      -(void)onMyFormSubmitted:(MyForm*)form {
        [...]
        /* hello user has entered an invalid email address */
        [[EngagementAgent shared] sendSessionError:@"sign_up_email" extras:nil]
        [...]
      }
      [...]
    }

### <a name="standalone-errors"></a><span data-ttu-id="28e5f-135">Błędy autonomiczny</span><span class="sxs-lookup"><span data-stu-id="28e5f-135">Standalone errors</span></span>
<span data-ttu-id="28e5f-136">Sprzeczne toosession błędy, błędy autonomiczny mogła być używana poza hello kontekstu sesji.</span><span class="sxs-lookup"><span data-stu-id="28e5f-136">Contrary toosession errors, standalone errors can be used outside of hello context of a session.</span></span>

<span data-ttu-id="28e5f-137">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="28e5f-137">**Example:**</span></span>

    [[EngagementAgent shared] sendError:@"something_failed" extras:nil];

## <a name="reporting-jobs"></a><span data-ttu-id="28e5f-138">Zadania raportowania</span><span class="sxs-lookup"><span data-stu-id="28e5f-138">Reporting Jobs</span></span>
<span data-ttu-id="28e5f-139">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="28e5f-139">**Example:**</span></span>

<span data-ttu-id="28e5f-140">Załóżmy, że chcesz tooreport hello czas trwania procesu logowania:</span><span class="sxs-lookup"><span data-stu-id="28e5f-140">Suppose you want tooreport hello duration of your login process:</span></span>

    [...]
    -(void)signIn
    {
      /* Start job */
      [[EngagementAgent shared] startJob:@"sign_in" extras:nil];

      [... sign in ...]

      /* End job */
      [[EngagementAgent shared] endJob:@"sign_in"];
    }
    [...]

### <a name="report-errors-during-a-job"></a><span data-ttu-id="28e5f-141">Zgłoś błędy podczas wykonywania zadania</span><span class="sxs-lookup"><span data-stu-id="28e5f-141">Report Errors during a Job</span></span>
<span data-ttu-id="28e5f-142">Błędy mogą być powiązane tooa uruchomienia zadania zamiast powiązane toohello bieżącą sesję użytkownika.</span><span class="sxs-lookup"><span data-stu-id="28e5f-142">Errors can be related tooa running job instead of being related toohello current user session.</span></span>

<span data-ttu-id="28e5f-143">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="28e5f-143">**Example:**</span></span>

<span data-ttu-id="28e5f-144">Załóżmy, że chcesz tooreport wystąpił błąd podczas procesu logowania:</span><span class="sxs-lookup"><span data-stu-id="28e5f-144">Suppose you want tooreport an error during your login process:</span></span>

    [...]
    -(void)signin
    {
      /* Start job */
      [[EngagementAgent shared] startJob:@"sign_in" extras:nil];

      BOOL success = NO;
      while (!success) {
        /* Try toosign in */
        NSError* error = nil;
        [self trySigin:&error];
        success = error == nil;

        /* If an error occured report it */
        if(!success)
        {
          [[EngagementAgent shared] sendJobError:@"sign_in_error"
                         jobName:@"sign_in"
                          extras:[NSDictionary dictionaryWithObject:[error localizedDescription] forKey:@"error"]];

          /* Retry after a moment */
          [NSThread sleepForTimeInterval:20];
        }
      }

      /* End job */
      [[EngagementAgent shared] endJob:@"sign_in"];
    };
    [...]

### <a name="events-during-a-job"></a><span data-ttu-id="28e5f-145">Zdarzenia podczas wykonywania zadania</span><span class="sxs-lookup"><span data-stu-id="28e5f-145">Events during a job</span></span>
<span data-ttu-id="28e5f-146">Zdarzenia mogą być powiązane tooa uruchomienia zadania zamiast powiązane toohello bieżącą sesję użytkownika.</span><span class="sxs-lookup"><span data-stu-id="28e5f-146">Events can be related tooa running job instead of being related toohello current user session.</span></span>

<span data-ttu-id="28e5f-147">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="28e5f-147">**Example:**</span></span>

<span data-ttu-id="28e5f-148">Załóżmy, że mamy sieci społecznościowych i używamy zadania tooreport hello całkowity czas podczas którego hello użytkownika jest serwer połączony toohello.</span><span class="sxs-lookup"><span data-stu-id="28e5f-148">Suppose we have a social network, and we use a job tooreport hello total time during which hello user is connected toohello server.</span></span> <span data-ttu-id="28e5f-149">Witaj użytkownika mogą odbierać komunikaty z jego znajomych, to zdarzenia zadania.</span><span class="sxs-lookup"><span data-stu-id="28e5f-149">hello user can receive messages from his friends, this is a job event.</span></span>

    [...]
    - (void) signin
    {
      [...Sign in code...]
      [[EngagementAgent shared] startJob:@"connection" extras:nil];
    }
    [...]
    - (void) signout
    {
      [...Sign out code...]
      [[EngagementAgent shared] endJob:@"connection"];
    }
    [...]
    - (void) onMessageReceived
    {
      [...Notify user...]
      [[EngagementAgent shared] sendJobEvent:@"connection" jobName:@"message_received" extras:nil];
    }
    [...]

## <a name="extra-parameters"></a><span data-ttu-id="28e5f-150">Dodatkowe parametry</span><span class="sxs-lookup"><span data-stu-id="28e5f-150">Extra parameters</span></span>
<span data-ttu-id="28e5f-151">Dowolne dane mogą być dołączone tooevents, błędów, działań i zadań.</span><span class="sxs-lookup"><span data-stu-id="28e5f-151">Arbitrary data can be attached tooevents, errors, activities and jobs.</span></span>

<span data-ttu-id="28e5f-152">Te dane mogą być elementami struktury, używa klasy NSDictionary dla systemu iOS.</span><span class="sxs-lookup"><span data-stu-id="28e5f-152">This data can be structured, it uses iOS's NSDictionary class.</span></span>

<span data-ttu-id="28e5f-153">Należy pamiętać, że może zawierać dodatkowe `arrays(NSArray, NSMutableArray)`, `numbers(NSNumber class)`, `strings(NSString, NSMutableString)`, `urls(NSURL)`, `data(NSData, NSMutableData)` lub innych `NSDictionary` wystąpień.</span><span class="sxs-lookup"><span data-stu-id="28e5f-153">Note that extras can contain `arrays(NSArray, NSMutableArray)`, `numbers(NSNumber class)`, `strings(NSString, NSMutableString)`, `urls(NSURL)`, `data(NSData, NSMutableData)` or other `NSDictionary` instances.</span></span>

> [!NOTE]
> <span data-ttu-id="28e5f-154">Witaj dodatkowy parametr jest serializowany w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="28e5f-154">hello extra parameter is serialized in JSON.</span></span> <span data-ttu-id="28e5f-155">Jeśli chcesz toopass różnych obiektów niż hello opisane powyżej, musi implementować następujące metody w klasie hello:</span><span class="sxs-lookup"><span data-stu-id="28e5f-155">If you want toopass different objects than hello ones described above, you must implement hello following method in your class:</span></span>
> 
> <span data-ttu-id="28e5f-156">-(NSString*) JSONRepresentation;</span><span class="sxs-lookup"><span data-stu-id="28e5f-156">-(NSString*)JSONRepresentation;</span></span>
> 
> <span data-ttu-id="28e5f-157">Metoda Hello powinna zwrócić reprezentację obiektu w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="28e5f-157">hello method should return a JSON representation of your object.</span></span>
> 
> 

### <a name="example"></a><span data-ttu-id="28e5f-158">Przykład</span><span class="sxs-lookup"><span data-stu-id="28e5f-158">Example</span></span>
    NSMutableDictionary* extras = [NSMutableDictionary dictionaryWithCapacity:2];
    [extras setObject:[NSNumber numberWithInt:123] forKey:@"video_id"];
    [extras setObject:@"http://foobar.com/blog" forKey:@"ref_click"];
    [[EngagementAgent shared] sendEvent:@"video_clicked" extras:extras];

### <a name="limits"></a><span data-ttu-id="28e5f-159">Limity</span><span class="sxs-lookup"><span data-stu-id="28e5f-159">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="28e5f-160">Klucze</span><span class="sxs-lookup"><span data-stu-id="28e5f-160">Keys</span></span>
<span data-ttu-id="28e5f-161">Każdy klucz w hello `NSDictionary` musi odpowiadać hello następującego wyrażenia regularnego:</span><span class="sxs-lookup"><span data-stu-id="28e5f-161">Each key in hello `NSDictionary` must match hello following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*`

<span data-ttu-id="28e5f-162">Oznacza to, że klucze musi rozpoczynać się od co najmniej jedną literą, następują litery, cyfry i znaki podkreślenia (\_).</span><span class="sxs-lookup"><span data-stu-id="28e5f-162">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="28e5f-163">Rozmiar</span><span class="sxs-lookup"><span data-stu-id="28e5f-163">Size</span></span>
<span data-ttu-id="28e5f-164">Dodatki są zbyt ograniczone**1024** znaków na wywołanie (po zakodowaniu w formacie JSON przez agenta zaangażowania hello).</span><span class="sxs-lookup"><span data-stu-id="28e5f-164">Extras are limited too**1024** characters per call (once encoded in JSON by hello Engagement agent).</span></span>

<span data-ttu-id="28e5f-165">W hello poprzedni przykład, hello JSON wysyłane toohello serwera jest 58 znaków:</span><span class="sxs-lookup"><span data-stu-id="28e5f-165">In hello previous example, hello JSON sent toohello server is 58 characters long:</span></span>

    {"ref_click":"http:\/\/foobar.com\/blog","video_id":"123"}

## <a name="reporting-application-information"></a><span data-ttu-id="28e5f-166">Raportowanie informacji o aplikacji</span><span class="sxs-lookup"><span data-stu-id="28e5f-166">Reporting Application Information</span></span>
<span data-ttu-id="28e5f-167">Można ręcznie raportu śledzenia informacji (lub innych aplikacji szczegółowych informacji) przy użyciu hello `sendAppInfo:` funkcji.</span><span class="sxs-lookup"><span data-stu-id="28e5f-167">You can manually report tracking information (or any other application specific information) using hello `sendAppInfo:` function.</span></span>

<span data-ttu-id="28e5f-168">Należy pamiętać, że te informacje mogą zostać przesłane przyrostowo: tylko hello wartość najnowszej dla danego klucza zostaną zachowane dla danego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="28e5f-168">Note that these information can be sent incrementally: only hello latest value for a given key will be kept for a given device.</span></span>

<span data-ttu-id="28e5f-169">Takich jak dodatkowe zdarzenia hello `NSDictionary` klasa jest używana tooabstract informacje o aplikacji, należy pamiętać, że stałych lub słowników podrzędnej będzie traktowany jako płaska ciągów (za pomocą serializacji JSON).</span><span class="sxs-lookup"><span data-stu-id="28e5f-169">Like event extras, hello `NSDictionary` class is used tooabstract application information, note that arrays or sub-dictionaries will be treated as flat strings (using JSON serialization).</span></span>

<span data-ttu-id="28e5f-170">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="28e5f-170">**Example:**</span></span>

    NSMutableDictionary* appInfo = [NSMutableDictionary dictionaryWithCapacity:2];
    [appInfo setObject:@"female" forKey:@"gender"];
    [appInfo setObject:@"1983-12-07" forKey:@"birthdate"]; // December 7th 1983
    [[EngagementAgent shared] sendAppInfo:appInfo];

### <a name="limits"></a><span data-ttu-id="28e5f-171">Limity</span><span class="sxs-lookup"><span data-stu-id="28e5f-171">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="28e5f-172">Klucze</span><span class="sxs-lookup"><span data-stu-id="28e5f-172">Keys</span></span>
<span data-ttu-id="28e5f-173">Każdy klucz w hello `NSDictionary` musi odpowiadać hello następującego wyrażenia regularnego:</span><span class="sxs-lookup"><span data-stu-id="28e5f-173">Each key in hello `NSDictionary` must match hello following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*`

<span data-ttu-id="28e5f-174">Oznacza to, że klucze musi rozpoczynać się od co najmniej jedną literą, następują litery, cyfry i znaki podkreślenia (\_).</span><span class="sxs-lookup"><span data-stu-id="28e5f-174">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="28e5f-175">Rozmiar</span><span class="sxs-lookup"><span data-stu-id="28e5f-175">Size</span></span>
<span data-ttu-id="28e5f-176">Informacje o aplikacji są zbyt ograniczone**1024** znaków na wywołanie (po zakodowaniu w formacie JSON przez agenta zaangażowania hello).</span><span class="sxs-lookup"><span data-stu-id="28e5f-176">Application information are limited too**1024** characters per call (once encoded in JSON by hello Engagement agent).</span></span>

<span data-ttu-id="28e5f-177">W hello poprzedni przykład, hello JSON wysyłane toohello serwera jest 44 znaków:</span><span class="sxs-lookup"><span data-stu-id="28e5f-177">In hello previous example, hello JSON sent toohello server is 44 characters long:</span></span>

    {"birthdate":"1983-12-07","gender":"female"}
