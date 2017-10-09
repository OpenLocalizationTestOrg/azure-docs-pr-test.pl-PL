---
title: "Witaj tooUse aaaHow API zaangażowania w systemie Android"
description: "Najnowszy zestaw SDK systemu Android — jak tooUse hello API zaangażowania w systemie Android"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 09b62659-82ae-4a55-8784-fca0b6b22eaf
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: na
ms.topic: article
ms.date: 07/25/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: e0b2d484616c0c7874e77c5283d94c3063949ed2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-engagement-api-on-android"></a><span data-ttu-id="08f9f-103">Jak tooUse hello API zaangażowania w systemie Android</span><span class="sxs-lookup"><span data-stu-id="08f9f-103">How tooUse hello Engagement API on Android</span></span>
<span data-ttu-id="08f9f-104">Ten dokument jest dodatek toohello [opcje zaawansowane raportowanie dla systemu Android zestaw SDK usługi Mobile Engagement](mobile-engagement-android-advanced-reporting.md).</span><span class="sxs-lookup"><span data-stu-id="08f9f-104">This document is an add-on toohello document [Advanced Reporting options for Android Mobile Engagement SDK](mobile-engagement-android-advanced-reporting.md).</span></span> <span data-ttu-id="08f9f-105">Zapewnia on głębokość szczegóły dotyczące sposobu toouse hello tooreport interfejsu API usługi Engagement statystyk aplikacji.</span><span class="sxs-lookup"><span data-stu-id="08f9f-105">It provides in depth details about how toouse hello Engagement API tooreport your application statistics.</span></span>

<span data-ttu-id="08f9f-106">Należy pamiętać, że jeśli mają tylko tooreport zaangażowania sesji aplikacji, działań, awarii (Crash) i informacje techniczne, następnie hello Najprostszym sposobem jest toomake wszystkie Twoje `Activity` klasy podrzędne dziedziczą odpowiadającego hello `EngagementActivity` klasy.</span><span class="sxs-lookup"><span data-stu-id="08f9f-106">Keep in mind that if you only want Engagement tooreport your application's sessions, activities, crashes and technical information, then hello simplest way is toomake all your `Activity` sub-classes inherit from hello corresponding `EngagementActivity` class.</span></span>

<span data-ttu-id="08f9f-107">Jeśli chcesz, aby toodo więcej, na przykład, jeśli potrzebujesz tooreport aplikacji określonych zdarzeń, błędów i zadań, czy masz tooreport działania aplikacji w inny sposób niż jeden zaimplementowana w hello hello `EngagementActivity` klas, wówczas należy toouse hello Interfejs API usługi Engagement.</span><span class="sxs-lookup"><span data-stu-id="08f9f-107">If you want toodo more, for example if you need tooreport application specific events, errors and jobs, or if you have tooreport your application's activities in a different way than hello one implemented in hello `EngagementActivity` classes, then you need toouse hello Engagement API.</span></span>

<span data-ttu-id="08f9f-108">Hello zaangażowania interfejsu API jest zapewniana przez hello `EngagementAgent` klasy.</span><span class="sxs-lookup"><span data-stu-id="08f9f-108">hello Engagement API is provided by hello `EngagementAgent` class.</span></span> <span data-ttu-id="08f9f-109">Wystąpienie tej klasy może być pobierane przez wywołanie hello `EngagementAgent.getInstance(Context)` metody statycznej (należy pamiętać, że hello `EngagementAgent` obiektu zwróconego jest pojedyncza).</span><span class="sxs-lookup"><span data-stu-id="08f9f-109">An instance of this class can be retrieved by calling hello `EngagementAgent.getInstance(Context)` static method (note that hello `EngagementAgent` object returned is a singleton).</span></span>

## <a name="engagement-concepts"></a><span data-ttu-id="08f9f-110">Pojęcia dotyczące usługi Engagement</span><span class="sxs-lookup"><span data-stu-id="08f9f-110">Engagement concepts</span></span>
<span data-ttu-id="08f9f-111">Hello następujące części uściślić hello wspólnej [Mobile Engagement pojęcia](mobile-engagement-concepts.md), hello platformy Android.</span><span class="sxs-lookup"><span data-stu-id="08f9f-111">hello following parts refine hello common [Mobile Engagement Concepts](mobile-engagement-concepts.md), for hello Android platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="08f9f-112">`Session` i `Activity`</span><span class="sxs-lookup"><span data-stu-id="08f9f-112">`Session` and `Activity`</span></span>
<span data-ttu-id="08f9f-113">Jeśli użytkownik hello pozostaje więcej niż kilka sekund bezczynności między dwiema *działania*, następnie ta sekwencja z *działania* jest podzielony na dwie różne *sesji*.</span><span class="sxs-lookup"><span data-stu-id="08f9f-113">If hello user stays more than a few seconds idle between two *activities*, then his sequence of *activities* is split in two distinct *sessions*.</span></span> <span data-ttu-id="08f9f-114">Te kilka sekund, są nazywane hello "limit czasu sesji".</span><span class="sxs-lookup"><span data-stu-id="08f9f-114">These few seconds are called hello "session timeout".</span></span>

<span data-ttu-id="08f9f-115">*Działania* są zwykle skojarzone z jednego ekranu aplikacji hello, która jest toosay hello *działania* uruchamiana, gdy hello ekran jest wyświetlany i zatrzymuje po zamknięciu ekranu hello: hello jest przypadek, kiedy Witaj Engagement SDK jest zintegrowany przy użyciu hello `EngagementActivity` klasy.</span><span class="sxs-lookup"><span data-stu-id="08f9f-115">An *activity* is usually associated with one screen of hello application, that is toosay hello *activity* starts when hello screen is displayed and stops when hello screen is closed: this is hello case when hello Engagement SDK is integrated by using hello `EngagementActivity` classes.</span></span>

<span data-ttu-id="08f9f-116">Ale *działania* można sterować także ręcznie przy użyciu hello interfejsu API usługi Engagement.</span><span class="sxs-lookup"><span data-stu-id="08f9f-116">But *activities* can also be controlled manually by using hello Engagement API.</span></span> <span data-ttu-id="08f9f-117">Umożliwia to toosplit danego ekranu w kilku tooget części sub więcej szczegółów na temat hello użycia tego ekranu (na przykład częstotliwość tooknown i jak długo okna dialogowe są używane wewnątrz tego ekranu).</span><span class="sxs-lookup"><span data-stu-id="08f9f-117">This allows toosplit a given screen in several sub parts tooget more details about hello usage of this screen (for example tooknown how often and how long dialogs are used inside this screen).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="08f9f-118">Działania raportowania</span><span class="sxs-lookup"><span data-stu-id="08f9f-118">Reporting Activities</span></span>
> [!IMPORTANT]
> <span data-ttu-id="08f9f-119">Nie ma potrzeby tooreport działań, takich jak opisane w tej sekcji, jeśli używasz hello `EngagementActivity` klasy i jej wariantów zgodnie z objaśnieniem w hello jak tooIntegrate Engagement Android dokumentu.</span><span class="sxs-lookup"><span data-stu-id="08f9f-119">You don't need tooreport activities like described in this section if you are using hello `EngagementActivity` class and its variants as explained in hello How tooIntegrate Engagement on Android document.</span></span>
> 
> 

### <a name="user-starts-a-new-activity"></a><span data-ttu-id="08f9f-120">Użytkownik uruchamia nowe działanie</span><span class="sxs-lookup"><span data-stu-id="08f9f-120">User starts a new Activity</span></span>
            EngagementAgent.getInstance(this).startActivity(this, "MyUserActivity", null);
            // Passing hello current activity is required for Reach toodisplay in-app notifications, passing null will postpone such announcements and polls.

<span data-ttu-id="08f9f-121">Należy toocall `startActivity()` każde działanie użytkownika hello czasu zmiany.</span><span class="sxs-lookup"><span data-stu-id="08f9f-121">You need toocall `startActivity()` each time hello user activity changes.</span></span> <span data-ttu-id="08f9f-122">Hello pierwszej wywołania funkcji toothis uruchamia nową sesję użytkownika.</span><span class="sxs-lookup"><span data-stu-id="08f9f-122">hello first call toothis function starts a new user session.</span></span>

<span data-ttu-id="08f9f-123">Witaj najlepsze miejsce toocall, ta funkcja jest na każde działanie `onResume` wywołania zwrotnego.</span><span class="sxs-lookup"><span data-stu-id="08f9f-123">hello best place toocall this function is on each activity `onResume` callback.</span></span>

### <a name="user-ends-his-current-activity"></a><span data-ttu-id="08f9f-124">Użytkownik kończy swoje bieżące działanie</span><span class="sxs-lookup"><span data-stu-id="08f9f-124">User ends his current Activity</span></span>
            EngagementAgent.getInstance(this).endActivity();

<span data-ttu-id="08f9f-125">Należy toocall `endActivity()` co najmniej raz, gdy użytkownik hello kończy swoje ostatnie działanie.</span><span class="sxs-lookup"><span data-stu-id="08f9f-125">You need toocall `endActivity()` at least once when hello user finishes his last activity.</span></span> <span data-ttu-id="08f9f-126">Informuje hello Engagement SDK hello użytkownik jest obecnie w stanie bezczynności, czy że sesji użytkownika hello muszą toobe zamknąć raz limit czasu sesji hello wygaśnie (jeśli wywołujesz `startActivity()` przed upłynięciem limitu czasu sesji hello, po prostu wznowieniu sesji hello).</span><span class="sxs-lookup"><span data-stu-id="08f9f-126">This informs hello Engagement SDK that hello user is currently idle, and that hello user session need toobe closed once hello session timeout will expire (if you call `startActivity()` before hello session timeout expires, hello session is simply resumed).</span></span>

<span data-ttu-id="08f9f-127">Witaj najlepsze miejsce toocall, ta funkcja jest na każde działanie `onPause` wywołania zwrotnego.</span><span class="sxs-lookup"><span data-stu-id="08f9f-127">hello best place toocall this function is on each activity `onPause` callback.</span></span>

## <a name="reporting-events"></a><span data-ttu-id="08f9f-128">Zdarzenia raportowania</span><span class="sxs-lookup"><span data-stu-id="08f9f-128">Reporting Events</span></span>
### <a name="session-events"></a><span data-ttu-id="08f9f-129">Zdarzenia sesji</span><span class="sxs-lookup"><span data-stu-id="08f9f-129">Session events</span></span>
<span data-ttu-id="08f9f-130">Zdarzenia sesji są zazwyczaj używane tooreport hello akcje wykonywane przez użytkownika podczas jego sesji.</span><span class="sxs-lookup"><span data-stu-id="08f9f-130">Session events are usually used tooreport hello actions performed by a user during his session.</span></span>

<span data-ttu-id="08f9f-131">**Przykład bez dodatkowe dane:**</span><span class="sxs-lookup"><span data-stu-id="08f9f-131">**Example without extra data:**</span></span>

            public MyActivity extends EngagementActivity {
               [...]
               @Override
               public boolean onPrepareOptionsMenu(Menu menu) {
                  getEngagementAgent().sendSessionEvent("menu_shown", null);
               }
               [...]
            }

<span data-ttu-id="08f9f-132">**Przykład: dodatkowe dane:**</span><span class="sxs-lookup"><span data-stu-id="08f9f-132">**Example with extra data:**</span></span>

            public MyActivity extends EngagementActivity {
              [...]
              @Override
              public boolean onMenuItemSelected(int featureId, MenuItem item) {
                Bundle extras = new Bundle();
                extras.putInt("id", item.getItemId());
                getEngagementAgent().sendSessionEvent("menu_selected", extras);
              }
              [...]
            }

### <a name="standalone-events"></a><span data-ttu-id="08f9f-133">Autonomiczny zdarzenia</span><span class="sxs-lookup"><span data-stu-id="08f9f-133">Standalone Events</span></span>
<span data-ttu-id="08f9f-134">Zdarzenia toosession sprzeczne poza hello kontekstu sesji mogą występować zdarzenia autonomicznych.</span><span class="sxs-lookup"><span data-stu-id="08f9f-134">Contrary toosession events, standalone events can occur outside of hello context of a session.</span></span>

<span data-ttu-id="08f9f-135">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="08f9f-135">**Example:**</span></span>

<span data-ttu-id="08f9f-136">Załóżmy, że tooreport zdarzenia występujące po wyzwoleniu emisji odbiornik:</span><span class="sxs-lookup"><span data-stu-id="08f9f-136">Suppose you want tooreport events occurring when a broadcast receiver is triggered:</span></span>

            /** Triggered by Intent.ACTION_BATTERY_LOW */
            public BatteryLowReceiver extends BroadcastReceiver {
              [...]
              @Override
              public void onReceive(Context context, Intent intent) {
                EngagementAgent.getInstance(context).sendEvent("battery_low", null);
              }
              [...]
            }

## <a name="reporting-errors"></a><span data-ttu-id="08f9f-137">Raportowanie błędów</span><span class="sxs-lookup"><span data-stu-id="08f9f-137">Reporting Errors</span></span>
### <a name="session-errors"></a><span data-ttu-id="08f9f-138">Błędy sesji</span><span class="sxs-lookup"><span data-stu-id="08f9f-138">Session errors</span></span>
<span data-ttu-id="08f9f-139">Błędy sesji są błędy hello zwykle używanych tooreport wpływające na powitania użytkownika podczas jego sesji.</span><span class="sxs-lookup"><span data-stu-id="08f9f-139">Session errors are usually used tooreport hello errors impacting hello user during his session.</span></span>

<span data-ttu-id="08f9f-140">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="08f9f-140">**Example:**</span></span>

            /** hello user has entered invalid data in a form */
            public MyActivity extends EngagementActivity {
              [...]
              public void onMyFormSubmitted(MyForm form) {
                [...]
                /* hello user has entered an invalid email address */
                getEngagementAgent().sendSessionError("sign_up_email", null);
                [...]
              }
              [...]
            }

### <a name="standalone-errors"></a><span data-ttu-id="08f9f-141">Błędy autonomiczny</span><span class="sxs-lookup"><span data-stu-id="08f9f-141">Standalone errors</span></span>
<span data-ttu-id="08f9f-142">Błędy sprzeczne toosession poza hello kontekstu sesji mogą wystąpić błędy autonomicznych.</span><span class="sxs-lookup"><span data-stu-id="08f9f-142">Contrary toosession errors, standalone errors can occur outside of hello context of a session.</span></span>

<span data-ttu-id="08f9f-143">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="08f9f-143">**Example:**</span></span>

<span data-ttu-id="08f9f-144">Witaj poniższy przykład przedstawia sposób tooreport wystąpił błąd, gdy pamięć hello staje się niskim w telefonie hello podczas procesu aplikacji jest uruchomiony.</span><span class="sxs-lookup"><span data-stu-id="08f9f-144">hello following example shows how tooreport an error whenever hello memory becomes low on hello phone while your application process is running.</span></span>

            public MyApplication extends EngagementApplication {

              @Override
              protected void onApplicationProcessLowMemory() {
                EngagementAgent.getInstance(this).sendError("low_memory", null);
              }
            }

## <a name="reporting-jobs"></a><span data-ttu-id="08f9f-145">Zadania raportowania</span><span class="sxs-lookup"><span data-stu-id="08f9f-145">Reporting Jobs</span></span>
### <a name="example"></a><span data-ttu-id="08f9f-146">Przykład</span><span class="sxs-lookup"><span data-stu-id="08f9f-146">Example</span></span>
<span data-ttu-id="08f9f-147">Załóżmy, że chcesz tooreport hello czas trwania procesu logowania:</span><span class="sxs-lookup"><span data-stu-id="08f9f-147">Suppose you want tooreport hello duration of your login process:</span></span>

            [...]
            public void signIn(Context context, ...) {

              /* We need an Android context toocall hello Engagement API, if you are extending Activity, Service, you can pass "this" */
              EngagementAgent engagementAgent = EngagementAgent.getInstance(context);

              /* Report sign in job has started */
              engagementAgent.startJob("sign_in", null);

              [... sign in ...]

              /* Report sign in job is now ended */
              engagementAgent.endJob("sign_in");
            }
            [...]

### <a name="report-errors-during-a-job"></a><span data-ttu-id="08f9f-148">Zgłoś błędy podczas wykonywania zadania</span><span class="sxs-lookup"><span data-stu-id="08f9f-148">Report Errors during a Job</span></span>
<span data-ttu-id="08f9f-149">Błędy mogą być powiązane tooa uruchomienia zadania zamiast powiązane toohello bieżącą sesję użytkownika.</span><span class="sxs-lookup"><span data-stu-id="08f9f-149">Errors can be related tooa running job instead of being related toohello current user session.</span></span>

<span data-ttu-id="08f9f-150">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="08f9f-150">**Example:**</span></span>

<span data-ttu-id="08f9f-151">Załóżmy, że chcesz tooreport wystąpił błąd podczas możesz zalogować się proces:</span><span class="sxs-lookup"><span data-stu-id="08f9f-151">Suppose you want tooreport an error during you login process:</span></span>

<span data-ttu-id="08f9f-152">[...] publiczny rejestrowanie void (kontekstu kontekstu,...) {</span><span class="sxs-lookup"><span data-stu-id="08f9f-152">[...] public void signIn(Context context, ...) {</span></span>

              /* We need an Android context toocall hello Engagement API, if you are extending Activity, Service, you can pass "this" */
              EngagementAgent engagementAgent = EngagementAgent.getInstance(context);

              /* Report sign in job has been started */
              engagementAgent.startJob("sign_in", null);

              /* Try toosign in */
              while(true)
                try {
                  trySignin();
                  break;
                }
                catch(Exception e) {
                  /* Report hello error tooEngagement */
                  engagementAgent.sendJobError("sign_in_error", "sign_in", null);

                  /* Retry after a moment */
                  sleep(2000);
                }
              [...]
              /* Report sign in job is now ended */
              engagementAgent.endJob("sign_in");
            }
            [...]

### <a name="reporting-events-during-a-job"></a><span data-ttu-id="08f9f-153">Zdarzenia raportowania podczas wykonywania zadania</span><span class="sxs-lookup"><span data-stu-id="08f9f-153">Reporting Events during a job</span></span>
<span data-ttu-id="08f9f-154">Zdarzenia mogą być powiązane tooa uruchomienia zadania zamiast powiązane toohello bieżącą sesję użytkownika.</span><span class="sxs-lookup"><span data-stu-id="08f9f-154">Events can be related tooa running job instead of being related toohello current user session.</span></span>

<span data-ttu-id="08f9f-155">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="08f9f-155">**Example:**</span></span>

<span data-ttu-id="08f9f-156">Załóżmy, że mamy sieci społecznościowych i używamy zadania tooreport hello całkowity czas podczas którego hello użytkownika jest serwer połączony toohello.</span><span class="sxs-lookup"><span data-stu-id="08f9f-156">Suppose we have a social network, and we use a job tooreport hello total time during which hello user is connected toohello server.</span></span> <span data-ttu-id="08f9f-157">Witaj użytkownika można łączność w tle nawet wtedy, gdy jest on za pomocą innej aplikacji, lub gdy hello phone jest uśpiony, więc nie ma żadnej sesji.</span><span class="sxs-lookup"><span data-stu-id="08f9f-157">hello user can stay connected in background even when he's using another application or when hello phone is sleeping, so there is no session.</span></span>

<span data-ttu-id="08f9f-158">Witaj użytkownika mogą odbierać komunikaty z jego znajomych, to zdarzenia zadania.</span><span class="sxs-lookup"><span data-stu-id="08f9f-158">hello user can receive messages from his friends, this is a job event.</span></span>

            [...]
            public void signin(Context context, ...) {
              [...Sign in code...]
              EngagementAgent.getInstance(context).startJob("connection", null);
            }
            [...]
            public void signout(Context context) {
              [...Sign out code...]
              EngagementAgent.getInstance(context).endJob("connection");
            }
            [...]
            public void onMessageReceived(Context context) {
              [...Notify in status bar...]
              EngagementAgent.getInstance(context).sendJobEvent("message_received", "connection", null);
            }
            [...]

## <a name="extra-parameters"></a><span data-ttu-id="08f9f-159">Dodatkowe parametry</span><span class="sxs-lookup"><span data-stu-id="08f9f-159">Extra parameters</span></span>
<span data-ttu-id="08f9f-160">Dowolne dane mogą być dołączone tooevents, błędów, działań i zadań.</span><span class="sxs-lookup"><span data-stu-id="08f9f-160">Arbitrary data can be attached tooevents, errors, activities and jobs.</span></span>

<span data-ttu-id="08f9f-161">Te dane mogą być elementami struktury, używa klasy pakietu dla systemu Android (w rzeczywistości działa jak dodatkowe parametry w lokalizacji docelowych z systemem Android).</span><span class="sxs-lookup"><span data-stu-id="08f9f-161">This data can be structured, it uses Android's Bundle class (actually, it works like extra parameters in Android Intents).</span></span> <span data-ttu-id="08f9f-162">Należy pamiętać, że pakiet może zawierać tablic lub innego wystąpienia pakietu.</span><span class="sxs-lookup"><span data-stu-id="08f9f-162">Note that a Bundle can contain arrays or another Bundle instances.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="08f9f-163">Jeśli umieścisz w parcelable lub które można serializować parametrów, upewnij się, ich `toString()` metoda jest implementowane tooreturn ciąg zrozumiałą dla użytkownika.</span><span class="sxs-lookup"><span data-stu-id="08f9f-163">If you put in parcelable or serializable parameters, make sure their `toString()` method is implemented tooreturn a human-readable string.</span></span> <span data-ttu-id="08f9f-164">Klas możliwych do serializacji, zawierające pola z systemem innym niż przejściowy, które nie są serializacji spowoduje awarii systemu Android, gdy będzie wywoływać`bundle.putSerializable("key",value);`</span><span class="sxs-lookup"><span data-stu-id="08f9f-164">Serializable classes that contain non transient fields that are not serializable will make Android crash when you will call `bundle.putSerializable("key",value);`</span></span>
> 
> [!WARNING]
> <span data-ttu-id="08f9f-165">Tablice rozrzedzonych w dodatkowe parametry nie są obsługiwane, oznacza to, że nie można serializować jako tablica.</span><span class="sxs-lookup"><span data-stu-id="08f9f-165">Sparse arrays in extra parameters are not supported, that is, it won't be serialized as an array.</span></span> <span data-ttu-id="08f9f-166">Należy przekonwertować je na standardowe tablice przed jego użyciem w dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="08f9f-166">You should convert them into standard arrays before using it in extra parameters.</span></span>
> 
> 

### <a name="example"></a><span data-ttu-id="08f9f-167">Przykład</span><span class="sxs-lookup"><span data-stu-id="08f9f-167">Example</span></span>
            Bundle extras = new Bundle();
            extras.putString("video_id", 123);
            extras.putString("ref_click", "http://foobar.com/blog");
            EngagementAgent.getInstance(context).sendEvent("video_clicked", extras);

### <a name="limits"></a><span data-ttu-id="08f9f-168">Limity</span><span class="sxs-lookup"><span data-stu-id="08f9f-168">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="08f9f-169">Klucze</span><span class="sxs-lookup"><span data-stu-id="08f9f-169">Keys</span></span>
<span data-ttu-id="08f9f-170">Każdy klucz w hello `Bundle` musi odpowiadać hello następującego wyrażenia regularnego:</span><span class="sxs-lookup"><span data-stu-id="08f9f-170">Each key in hello `Bundle` must match hello following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*`

<span data-ttu-id="08f9f-171">Oznacza to, że klucze musi rozpoczynać się od co najmniej jedną literą, następują litery, cyfry i znaki podkreślenia (\_).</span><span class="sxs-lookup"><span data-stu-id="08f9f-171">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="08f9f-172">Rozmiar</span><span class="sxs-lookup"><span data-stu-id="08f9f-172">Size</span></span>
<span data-ttu-id="08f9f-173">Dodatki są zbyt ograniczone**1024** znaków na wywołanie (po zakodowaniu w formacie JSON przez usługę zaangażowania hello).</span><span class="sxs-lookup"><span data-stu-id="08f9f-173">Extras are limited too**1024** characters per call (once encoded in JSON by hello Engagement service).</span></span>

<span data-ttu-id="08f9f-174">W hello poprzedni przykład, hello JSON wysyłane toohello serwera jest 58 znaków:</span><span class="sxs-lookup"><span data-stu-id="08f9f-174">In hello previous example, hello JSON sent toohello server is 58 characters long:</span></span>

            {"ref_click":"http:\/\/foobar.com\/blog","video_id":"123"}

## <a name="reporting-application-information"></a><span data-ttu-id="08f9f-175">Raportowanie informacji o aplikacji</span><span class="sxs-lookup"><span data-stu-id="08f9f-175">Reporting Application Information</span></span>
<span data-ttu-id="08f9f-176">Można ręcznie raportu śledzenia informacji (lub innych aplikacji szczegółowych informacji) przy użyciu hello `sendAppInfo()` funkcji.</span><span class="sxs-lookup"><span data-stu-id="08f9f-176">You can manually report tracking information (or any other application specific information) using hello `sendAppInfo()` function.</span></span>

<span data-ttu-id="08f9f-177">Należy pamiętać, że te informacje mogą zostać przesłane przyrostowo: tylko hello wartość najnowszej dla danego klucza zostaną zachowane dla danego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="08f9f-177">Note that these information can be sent incrementally: only hello latest value for a given key will be kept for a given device.</span></span>

<span data-ttu-id="08f9f-178">Podobnie jak dodatkowe zdarzenia hello klasy pakietu jest używane tooabstract informacje o aplikacji, należy pamiętać, że stałych lub podrzędna zawiera będzie traktowany jako płaska ciągów (za pomocą serializacji JSON).</span><span class="sxs-lookup"><span data-stu-id="08f9f-178">Like event extras, hello Bundle class is used tooabstract application information, note that arrays or sub-bundles will be treated as flat strings (using JSON serialization).</span></span>

### <a name="example"></a><span data-ttu-id="08f9f-179">Przykład</span><span class="sxs-lookup"><span data-stu-id="08f9f-179">Example</span></span>
<span data-ttu-id="08f9f-180">Oto kod przykładowy toosend użytkownika płci i Data urodzenia:</span><span class="sxs-lookup"><span data-stu-id="08f9f-180">Here is a code sample toosend user gender and birthdate:</span></span>

            Bundle appInfo = new Bundle();
            appInfo.putString("status", "premium");
            appInfo.putString("expiration", "2016-12-07"); // December 7th 2016
            EngagementAgent.getInstance(context).sendAppInfo(appInfo);

### <a name="limits"></a><span data-ttu-id="08f9f-181">Limity</span><span class="sxs-lookup"><span data-stu-id="08f9f-181">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="08f9f-182">Klucze</span><span class="sxs-lookup"><span data-stu-id="08f9f-182">Keys</span></span>
<span data-ttu-id="08f9f-183">Każdy klucz w hello `Bundle` musi odpowiadać hello następującego wyrażenia regularnego:</span><span class="sxs-lookup"><span data-stu-id="08f9f-183">Each key in hello `Bundle` must match hello following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*`

<span data-ttu-id="08f9f-184">Oznacza to, że klucze musi rozpoczynać się od co najmniej jedną literą, następują litery, cyfry i znaki podkreślenia (\_).</span><span class="sxs-lookup"><span data-stu-id="08f9f-184">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="08f9f-185">Rozmiar</span><span class="sxs-lookup"><span data-stu-id="08f9f-185">Size</span></span>
<span data-ttu-id="08f9f-186">Informacje o aplikacji są zbyt ograniczone**1024** znaków na wywołanie (po zakodowaniu w formacie JSON przez usługę zaangażowania hello).</span><span class="sxs-lookup"><span data-stu-id="08f9f-186">Application information are limited too**1024** characters per call (once encoded in JSON by hello Engagement service).</span></span>

<span data-ttu-id="08f9f-187">W hello poprzedni przykład, hello JSON wysyłane toohello serwera jest 44 znaków:</span><span class="sxs-lookup"><span data-stu-id="08f9f-187">In hello previous example, hello JSON sent toohello server is 44 characters long:</span></span>

            {"expiration":"2016-12-07","status":"premium"}
