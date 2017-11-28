---
title: "Sposób użycia interfejsu API programu zaangażowania w systemie iOS"
description: "Najnowsze iOS SDK — sposób użycia interfejsu API programu zaangażowania w systemie iOS"
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
ms.openlocfilehash: a31424da98205e97bdf57010cccfd044360f03dd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-the-engagement-api-on-ios"></a><span data-ttu-id="2e2ae-103">Sposób użycia interfejsu API programu zaangażowania w systemie iOS</span><span class="sxs-lookup"><span data-stu-id="2e2ae-103">How to Use the Engagement API on iOS</span></span>
<span data-ttu-id="2e2ae-104">Ten dokument jest dodatkiem do dokumentu jak zintegrować zaangażowania w systemie iOS: dostarcza w głębokość szczegółowe informacje dotyczące raportu statystyk aplikacji za pomocą interfejsu API usługi Engagement.</span><span class="sxs-lookup"><span data-stu-id="2e2ae-104">This document is an add-on to the document How to Integrate Engagement on iOS: it provides in depth details about how to use the Engagement API to report your application statistics.</span></span>

<span data-ttu-id="2e2ae-105">Należy pamiętać, że jeśli chcesz tylko zaangażowania do raportów aplikacji sesji, działania, awarii (Crash) i informacje techniczne, następnie Najłatwiejszą metodą jest zapewnienie wszystkie niestandardowe `UIViewController` obiekty dziedziczyć odpowiadającego `EngagementViewController` klasy.</span><span class="sxs-lookup"><span data-stu-id="2e2ae-105">Keep in mind that if you only want Engagement to report your application's sessions, activities, crashes and technical information, then the simplest way is to make all your custom `UIViewController` objects inherit from the corresponding `EngagementViewController` class.</span></span>

<span data-ttu-id="2e2ae-106">Jeśli chcesz zrobić więcej, na przykład, jeśli zachodzi konieczność raportów aplikacji określonych zdarzeń, błędów i zadań, lub jeśli zajdzie potrzeba raportu działania aplikacji w inny sposób niż jeden zaimplementowana w `EngagementViewController` klasy, a następnie należy użyć interfejsu API usługi Engagement.</span><span class="sxs-lookup"><span data-stu-id="2e2ae-106">If you want to do more, for example if you need to report application specific events, errors and jobs, or if you have to report your application's activities in a different way than the one implemented in the `EngagementViewController` classes, then you need to use the Engagement API.</span></span>

<span data-ttu-id="2e2ae-107">Interfejsu API programu zaangażowania jest zapewniana przez `EngagementAgent` klasy.</span><span class="sxs-lookup"><span data-stu-id="2e2ae-107">The Engagement API is provided by the `EngagementAgent` class.</span></span> <span data-ttu-id="2e2ae-108">Wystąpienie tej klasy można pobrać przez wywołanie metody `[EngagementAgent shared]` metody statycznej (należy pamiętać, że `EngagementAgent` obiektu zwróconego jest pojedyncza).</span><span class="sxs-lookup"><span data-stu-id="2e2ae-108">An instance of this class can be retrieved by calling the `[EngagementAgent shared]` static method (note that the `EngagementAgent` object returned is a singleton).</span></span>

<span data-ttu-id="2e2ae-109">Przed wszystkie wywołania interfejsu API `EngagementAgent` obiekt musi zostać zainicjowany przez wywołanie metody`[EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];`</span><span class="sxs-lookup"><span data-stu-id="2e2ae-109">Before any API calls, the `EngagementAgent` object must be initialized by calling the method `[EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];`</span></span>

## <a name="engagement-concepts"></a><span data-ttu-id="2e2ae-110">Pojęcia dotyczące usługi Engagement</span><span class="sxs-lookup"><span data-stu-id="2e2ae-110">Engagement concepts</span></span>
<span data-ttu-id="2e2ae-111">Następujące części uściślić typowe [Mobile Engagement pojęcia](mobile-engagement-concepts.md) dla platformy iOS.</span><span class="sxs-lookup"><span data-stu-id="2e2ae-111">The following parts refine the common [Mobile Engagement Concepts](mobile-engagement-concepts.md) for the iOS platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="2e2ae-112">`Session` i `Activity`</span><span class="sxs-lookup"><span data-stu-id="2e2ae-112">`Session` and `Activity`</span></span>
<span data-ttu-id="2e2ae-113">*Działania* są zwykle skojarzone z jednego ekranu aplikacji, to znaczy *działania* uruchamiana, gdy ekran jest wyświetlany i zatrzymuje po zamknięciu ekranu: dotyczy to sytuacji, gdy zestaw SDK Engagement jest zintegrowany przy użyciu `EngagementViewController` klasy.</span><span class="sxs-lookup"><span data-stu-id="2e2ae-113">An *activity* is usually associated with one screen of the application, that is to say the *activity* starts when the screen is displayed and stops when the screen is closed: this is the case when the Engagement SDK is integrated by using the `EngagementViewController` classes.</span></span>

<span data-ttu-id="2e2ae-114">Ale *działania* mogą również być kontrolowane ręcznie przy użyciu interfejsu API usługi Engagement.</span><span class="sxs-lookup"><span data-stu-id="2e2ae-114">But *activities* can also be controlled manually by using the Engagement API.</span></span> <span data-ttu-id="2e2ae-115">Dzięki temu podzielenie danej ekranu w kilku części sub, aby uzyskać więcej informacji na temat użycia tego ekranu (na przykład aby częstotliwość znane i jak długo okna dialogowe są używane wewnątrz tego ekranu).</span><span class="sxs-lookup"><span data-stu-id="2e2ae-115">This allows to split a given screen in several sub parts to get more details about the usage of this screen (for example to known how often and how long dialogs are used inside this screen).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="2e2ae-116">Działania raportowania</span><span class="sxs-lookup"><span data-stu-id="2e2ae-116">Reporting Activities</span></span>
### <a name="user-starts-a-new-activity"></a><span data-ttu-id="2e2ae-117">Użytkownik uruchamia nowe działanie</span><span class="sxs-lookup"><span data-stu-id="2e2ae-117">User starts a new Activity</span></span>
            [[EngagementAgent shared] startActivity:@"MyUserActivity" extras:nil];

<span data-ttu-id="2e2ae-118">Należy wywołać `startActivity()` każdej zmianie działania użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2e2ae-118">You need to call `startActivity()` each time the user activity changes.</span></span> <span data-ttu-id="2e2ae-119">W pierwszym wywołaniu tej funkcji uruchamia nową sesję użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2e2ae-119">The first call to this function starts a new user session.</span></span>

### <a name="user-ends-his-current-activity"></a><span data-ttu-id="2e2ae-120">Użytkownik kończy swoje bieżące działanie</span><span class="sxs-lookup"><span data-stu-id="2e2ae-120">User ends his current Activity</span></span>
            [[EngagementAgent shared] endActivity];

> [!WARNING]
> <span data-ttu-id="2e2ae-121">Należy **nigdy** wywołanie tej funkcji przez użytkownika, z wyjątkiem, jeśli chcesz podzielić jedno użycie aplikacji na kilka sesji: wywołanie tej funkcji spowodowałoby zakończenie bieżącej sesji, więc, kolejne wywołanie `startActivity()` Czy uruchomić nową sesję.</span><span class="sxs-lookup"><span data-stu-id="2e2ae-121">You should **NEVER** call this function by yourself, except if you want to split one use of your application into several sessions: a call to this function would end the current session immediately, so, a subsequent call to `startActivity()` would start a new session.</span></span> <span data-ttu-id="2e2ae-122">Ta funkcja jest wywoływana przez zestaw SDK automatycznie, gdy aplikacja jest zamknięty.</span><span class="sxs-lookup"><span data-stu-id="2e2ae-122">This function is automatically called by the SDK when your application is closed.</span></span>
> 
> 

## <a name="reporting-events"></a><span data-ttu-id="2e2ae-123">Zdarzenia raportowania</span><span class="sxs-lookup"><span data-stu-id="2e2ae-123">Reporting Events</span></span>
### <a name="session-events"></a><span data-ttu-id="2e2ae-124">Zdarzenia sesji</span><span class="sxs-lookup"><span data-stu-id="2e2ae-124">Session events</span></span>
<span data-ttu-id="2e2ae-125">Zdarzenia sesji są zwykle używane do zgłaszania akcji wykonywanych przez użytkownika podczas jego sesji.</span><span class="sxs-lookup"><span data-stu-id="2e2ae-125">Session events are usually used to report the actions performed by a user during his session.</span></span>

<span data-ttu-id="2e2ae-126">**Przykład bez dodatkowe dane:**</span><span class="sxs-lookup"><span data-stu-id="2e2ae-126">**Example without extra data:**</span></span>

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

<span data-ttu-id="2e2ae-127">**Przykład: dodatkowe dane:**</span><span class="sxs-lookup"><span data-stu-id="2e2ae-127">**Example with extra data:**</span></span>

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

### <a name="standalone-events"></a><span data-ttu-id="2e2ae-128">Autonomiczny zdarzenia</span><span class="sxs-lookup"><span data-stu-id="2e2ae-128">Standalone events</span></span>
<span data-ttu-id="2e2ae-129">Sprzecznie zdarzenia sesji zdarzeń autonomicznego może służyć poza kontekstem sesji.</span><span class="sxs-lookup"><span data-stu-id="2e2ae-129">Contrary to session events, standalone events can be used outside of the context of a session.</span></span>

<span data-ttu-id="2e2ae-130">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="2e2ae-130">**Example:**</span></span>

    [[EngagementAgent shared] sendEvent:@"received_notification" extras:nil];

## <a name="reporting-errors"></a><span data-ttu-id="2e2ae-131">Raportowanie błędów</span><span class="sxs-lookup"><span data-stu-id="2e2ae-131">Reporting Errors</span></span>
### <a name="session-errors"></a><span data-ttu-id="2e2ae-132">Błędy sesji</span><span class="sxs-lookup"><span data-stu-id="2e2ae-132">Session errors</span></span>
<span data-ttu-id="2e2ae-133">Błędy sesji są zwykle używane do raportów o błędach podczas sesji jego wpływu na użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2e2ae-133">Session errors are usually used to report the errors impacting the user during his session.</span></span>

<span data-ttu-id="2e2ae-134">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="2e2ae-134">**Example:**</span></span>

    /** The user has entered invalid data in a form */
    @implementation MyViewController {
      [...]
      -(void)onMyFormSubmitted:(MyForm*)form {
        [...]
        /* The user has entered an invalid email address */
        [[EngagementAgent shared] sendSessionError:@"sign_up_email" extras:nil]
        [...]
      }
      [...]
    }

### <a name="standalone-errors"></a><span data-ttu-id="2e2ae-135">Błędy autonomiczny</span><span class="sxs-lookup"><span data-stu-id="2e2ae-135">Standalone errors</span></span>
<span data-ttu-id="2e2ae-136">Sprzeczności z sesji błędy błędy autonomiczny może służyć poza kontekstem sesji.</span><span class="sxs-lookup"><span data-stu-id="2e2ae-136">Contrary to session errors, standalone errors can be used outside of the context of a session.</span></span>

<span data-ttu-id="2e2ae-137">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="2e2ae-137">**Example:**</span></span>

    [[EngagementAgent shared] sendError:@"something_failed" extras:nil];

## <a name="reporting-jobs"></a><span data-ttu-id="2e2ae-138">Zadania raportowania</span><span class="sxs-lookup"><span data-stu-id="2e2ae-138">Reporting Jobs</span></span>
<span data-ttu-id="2e2ae-139">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="2e2ae-139">**Example:**</span></span>

<span data-ttu-id="2e2ae-140">Załóżmy, że chcesz zgłosić w czasie trwania procesu logowania:</span><span class="sxs-lookup"><span data-stu-id="2e2ae-140">Suppose you want to report the duration of your login process:</span></span>

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

### <a name="report-errors-during-a-job"></a><span data-ttu-id="2e2ae-141">Zgłoś błędy podczas wykonywania zadania</span><span class="sxs-lookup"><span data-stu-id="2e2ae-141">Report Errors during a Job</span></span>
<span data-ttu-id="2e2ae-142">Błędy może być powiązane z uruchomionym zadaniem zamiast związany z bieżącą sesją użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2e2ae-142">Errors can be related to a running job instead of being related to the current user session.</span></span>

<span data-ttu-id="2e2ae-143">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="2e2ae-143">**Example:**</span></span>

<span data-ttu-id="2e2ae-144">Załóżmy, że chcesz zgłosić błąd podczas procesu logowania:</span><span class="sxs-lookup"><span data-stu-id="2e2ae-144">Suppose you want to report an error during your login process:</span></span>

    [...]
    -(void)signin
    {
      /* Start job */
      [[EngagementAgent shared] startJob:@"sign_in" extras:nil];

      BOOL success = NO;
      while (!success) {
        /* Try to sign in */
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

### <a name="events-during-a-job"></a><span data-ttu-id="2e2ae-145">Zdarzenia podczas wykonywania zadania</span><span class="sxs-lookup"><span data-stu-id="2e2ae-145">Events during a job</span></span>
<span data-ttu-id="2e2ae-146">Zdarzenia może być powiązane z uruchomionym zadaniem zamiast związany z bieżącą sesją użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2e2ae-146">Events can be related to a running job instead of being related to the current user session.</span></span>

<span data-ttu-id="2e2ae-147">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="2e2ae-147">**Example:**</span></span>

<span data-ttu-id="2e2ae-148">Załóżmy, że mamy sieci społecznościowych i używamy zadania do raportu całkowity czas, w którym użytkownik jest połączony z serwerem.</span><span class="sxs-lookup"><span data-stu-id="2e2ae-148">Suppose we have a social network, and we use a job to report the total time during which the user is connected to the server.</span></span> <span data-ttu-id="2e2ae-149">Użytkownik może odbierać komunikaty z jego znajomych, to zdarzenia zadania.</span><span class="sxs-lookup"><span data-stu-id="2e2ae-149">The user can receive messages from his friends, this is a job event.</span></span>

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

## <a name="extra-parameters"></a><span data-ttu-id="2e2ae-150">Dodatkowe parametry</span><span class="sxs-lookup"><span data-stu-id="2e2ae-150">Extra parameters</span></span>
<span data-ttu-id="2e2ae-151">Dowolne dane, może zostać dołączona do zdarzeń, błędów, działań i zadań.</span><span class="sxs-lookup"><span data-stu-id="2e2ae-151">Arbitrary data can be attached to events, errors, activities and jobs.</span></span>

<span data-ttu-id="2e2ae-152">Te dane mogą być elementami struktury, używa klasy NSDictionary dla systemu iOS.</span><span class="sxs-lookup"><span data-stu-id="2e2ae-152">This data can be structured, it uses iOS's NSDictionary class.</span></span>

<span data-ttu-id="2e2ae-153">Należy pamiętać, że może zawierać dodatkowe `arrays(NSArray, NSMutableArray)`, `numbers(NSNumber class)`, `strings(NSString, NSMutableString)`, `urls(NSURL)`, `data(NSData, NSMutableData)` lub innych `NSDictionary` wystąpień.</span><span class="sxs-lookup"><span data-stu-id="2e2ae-153">Note that extras can contain `arrays(NSArray, NSMutableArray)`, `numbers(NSNumber class)`, `strings(NSString, NSMutableString)`, `urls(NSURL)`, `data(NSData, NSMutableData)` or other `NSDictionary` instances.</span></span>

> [!NOTE]
> <span data-ttu-id="2e2ae-154">Dodatkowy parametr jest serializowany w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="2e2ae-154">The extra parameter is serialized in JSON.</span></span> <span data-ttu-id="2e2ae-155">Jeśli chcesz przekazać różnych obiektów niż opisane powyżej, musisz zaimplementować następującą metodę w klasie:</span><span class="sxs-lookup"><span data-stu-id="2e2ae-155">If you want to pass different objects than the ones described above, you must implement the following method in your class:</span></span>
> 
> <span data-ttu-id="2e2ae-156">-(NSString*) JSONRepresentation;</span><span class="sxs-lookup"><span data-stu-id="2e2ae-156">-(NSString*)JSONRepresentation;</span></span>
> 
> <span data-ttu-id="2e2ae-157">Metoda powinna zwracać reprezentację obiektu w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="2e2ae-157">The method should return a JSON representation of your object.</span></span>
> 
> 

### <a name="example"></a><span data-ttu-id="2e2ae-158">Przykład</span><span class="sxs-lookup"><span data-stu-id="2e2ae-158">Example</span></span>
    NSMutableDictionary* extras = [NSMutableDictionary dictionaryWithCapacity:2];
    [extras setObject:[NSNumber numberWithInt:123] forKey:@"video_id"];
    [extras setObject:@"http://foobar.com/blog" forKey:@"ref_click"];
    [[EngagementAgent shared] sendEvent:@"video_clicked" extras:extras];

### <a name="limits"></a><span data-ttu-id="2e2ae-159">Limity</span><span class="sxs-lookup"><span data-stu-id="2e2ae-159">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="2e2ae-160">Klucze</span><span class="sxs-lookup"><span data-stu-id="2e2ae-160">Keys</span></span>
<span data-ttu-id="2e2ae-161">Każdy klucz w `NSDictionary` musi być zgodna z następującym wyrażeniem regularnym:</span><span class="sxs-lookup"><span data-stu-id="2e2ae-161">Each key in the `NSDictionary` must match the following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*`

<span data-ttu-id="2e2ae-162">Oznacza to, że klucze musi rozpoczynać się od co najmniej jedną literą, następują litery, cyfry i znaki podkreślenia (\_).</span><span class="sxs-lookup"><span data-stu-id="2e2ae-162">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="2e2ae-163">Rozmiar</span><span class="sxs-lookup"><span data-stu-id="2e2ae-163">Size</span></span>
<span data-ttu-id="2e2ae-164">Dodatki są ograniczone do **1024** znaków na wywołanie (po zakodowaniu w formacie JSON przez agenta Engagement).</span><span class="sxs-lookup"><span data-stu-id="2e2ae-164">Extras are limited to **1024** characters per call (once encoded in JSON by the Engagement agent).</span></span>

<span data-ttu-id="2e2ae-165">W poprzednim przykładzie JSON na serwer wysyłane jest 58 znaków:</span><span class="sxs-lookup"><span data-stu-id="2e2ae-165">In the previous example, the JSON sent to the server is 58 characters long:</span></span>

    {"ref_click":"http:\/\/foobar.com\/blog","video_id":"123"}

## <a name="reporting-application-information"></a><span data-ttu-id="2e2ae-166">Raportowanie informacji o aplikacji</span><span class="sxs-lookup"><span data-stu-id="2e2ae-166">Reporting Application Information</span></span>
<span data-ttu-id="2e2ae-167">Można ręcznie raportu śledzenia informacji (lub innych aplikacji szczegółowych informacji) przy użyciu `sendAppInfo:` funkcji.</span><span class="sxs-lookup"><span data-stu-id="2e2ae-167">You can manually report tracking information (or any other application specific information) using the `sendAppInfo:` function.</span></span>

<span data-ttu-id="2e2ae-168">Należy pamiętać, że te informacje mogą zostać przesłane przyrostowo: tylko najnowszą wartość dla danego klucza zostaną zachowane dla danego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="2e2ae-168">Note that these information can be sent incrementally: only the latest value for a given key will be kept for a given device.</span></span>

<span data-ttu-id="2e2ae-169">Dodatki zdarzeń, takich jak `NSDictionary` klasa jest używana do abstrakcyjnej informacje o aplikacji, należy pamiętać, że tablice lub słowników podrzędne będzie traktowany jako płaska ciągów (za pomocą serializacji JSON).</span><span class="sxs-lookup"><span data-stu-id="2e2ae-169">Like event extras, the `NSDictionary` class is used to abstract application information, note that arrays or sub-dictionaries will be treated as flat strings (using JSON serialization).</span></span>

<span data-ttu-id="2e2ae-170">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="2e2ae-170">**Example:**</span></span>

    NSMutableDictionary* appInfo = [NSMutableDictionary dictionaryWithCapacity:2];
    [appInfo setObject:@"female" forKey:@"gender"];
    [appInfo setObject:@"1983-12-07" forKey:@"birthdate"]; // December 7th 1983
    [[EngagementAgent shared] sendAppInfo:appInfo];

### <a name="limits"></a><span data-ttu-id="2e2ae-171">Limity</span><span class="sxs-lookup"><span data-stu-id="2e2ae-171">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="2e2ae-172">Klucze</span><span class="sxs-lookup"><span data-stu-id="2e2ae-172">Keys</span></span>
<span data-ttu-id="2e2ae-173">Każdy klucz w `NSDictionary` musi być zgodna z następującym wyrażeniem regularnym:</span><span class="sxs-lookup"><span data-stu-id="2e2ae-173">Each key in the `NSDictionary` must match the following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*`

<span data-ttu-id="2e2ae-174">Oznacza to, że klucze musi rozpoczynać się od co najmniej jedną literą, następują litery, cyfry i znaki podkreślenia (\_).</span><span class="sxs-lookup"><span data-stu-id="2e2ae-174">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="2e2ae-175">Rozmiar</span><span class="sxs-lookup"><span data-stu-id="2e2ae-175">Size</span></span>
<span data-ttu-id="2e2ae-176">Informacje o aplikacji są ograniczone do **1024** znaków na wywołanie (po zakodowaniu w formacie JSON przez agenta Engagement).</span><span class="sxs-lookup"><span data-stu-id="2e2ae-176">Application information are limited to **1024** characters per call (once encoded in JSON by the Engagement agent).</span></span>

<span data-ttu-id="2e2ae-177">W poprzednim przykładzie JSON na serwer wysyłane jest 44 znaków:</span><span class="sxs-lookup"><span data-stu-id="2e2ae-177">In the previous example, the JSON sent to the server is 44 characters long:</span></span>

    {"birthdate":"1983-12-07","gender":"female"}
