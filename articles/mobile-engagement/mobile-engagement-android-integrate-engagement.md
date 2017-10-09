---
title: aaaAzure Mobile Engagement Android SDK integracji
description: "Najnowsze aktualizacje i procedury dotyczące zestawu SDK systemu Android dla usługi Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a5487793-1a12-4f6c-a1cf-587c5a671e6b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 4f79936ea0fa6102023dec2b4682032a4a81fa9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-engagement-on-android"></a><span data-ttu-id="ea59c-103">Jak tooIntegrate zaangażowania w systemie Android</span><span class="sxs-lookup"><span data-stu-id="ea59c-103">How tooIntegrate Engagement on Android</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ea59c-104">Aplikacje uniwersalne systemu Windows</span><span class="sxs-lookup"><span data-stu-id="ea59c-104">Windows Universal</span></span>](mobile-engagement-windows-store-integrate-engagement.md)
> * [<span data-ttu-id="ea59c-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="ea59c-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="ea59c-106">iOS</span><span class="sxs-lookup"><span data-stu-id="ea59c-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="ea59c-107">Android</span><span class="sxs-lookup"><span data-stu-id="ea59c-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md)
> 
> 

<span data-ttu-id="ea59c-108">W tej procedurze opisano analizy i funkcji w aplikacji systemu Android monitorowania hello najprostszy sposób tooactivate usługi Engagement.</span><span class="sxs-lookup"><span data-stu-id="ea59c-108">This procedure describes hello simplest way tooactivate Engagement's Analytics and Monitoring functions in your Android application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ea59c-109">Minimalny poziom interfejsu API zestawu SDK systemu Android musi być 10 lub nowszej (Android 2.3.3 lub nowszej).</span><span class="sxs-lookup"><span data-stu-id="ea59c-109">Your minimum Android SDK API level must be 10 or higher (Android 2.3.3 or higher).</span></span>
> 
> 

<span data-ttu-id="ea59c-110">wymaga wystarczającej ilości raportu hello tooactivates dzienników toocompute wszystkie statystyki dotyczące użytkowników, sesji, działania, awarii (Crash) i Technicals to Hello następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="ea59c-110">hello following steps are enough tooactivates hello report of logs needed toocompute all statistics regarding Users, Sessions, Activities, Crashes and Technicals.</span></span> <span data-ttu-id="ea59c-111">Raport Hello dzienników potrzebne toocompute innych danych statystycznych jak zadań, błędy i zdarzenia musi zostać wykonane ręcznie przy użyciu hello zaangażowania interfejsu API (zobacz [jak toouse hello zaawansowane znakowanie interfejsu API w dla systemu Android w usłudze Mobile Engagement](mobile-engagement-android-use-engagement-api.md) od tych statystyki są aplikacji zależnej.</span><span class="sxs-lookup"><span data-stu-id="ea59c-111">hello report of logs needed toocompute other statistics like Events, Errors and Jobs must be done manually using hello Engagement API (see [How toouse hello advanced Mobile Engagement tagging API in your Android](mobile-engagement-android-use-engagement-api.md) since these statistics are application dependent.</span></span>

## <a name="embed-hello-engagement-sdk-and-service-into-your-android-project"></a><span data-ttu-id="ea59c-112">Osadź hello Engagement SDK i usługi do projektu systemu Android</span><span class="sxs-lookup"><span data-stu-id="ea59c-112">Embed hello Engagement SDK and service into your Android project</span></span>
<span data-ttu-id="ea59c-113">Pobieranie hello zestawu SDK systemu Android z [tutaj](https://aka.ms/vq9mfn) uzyskać `mobile-engagement-VERSION.jar` i umieść je w hello `libs` folderu projektu systemu Android (Utwórz folder biblioteki hello, jeśli jeszcze nie istnieje).</span><span class="sxs-lookup"><span data-stu-id="ea59c-113">Download hello Android SDK from [here](https://aka.ms/vq9mfn) Get `mobile-engagement-VERSION.jar` and put them into hello `libs` folder of your Android project (create hello libs folder if it does not exist yet).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ea59c-114">Tworzenie pakietu aplikacji z narzędzia ProGuard, należy najpierw tookeep niektórych klas.</span><span class="sxs-lookup"><span data-stu-id="ea59c-114">If you build your application package with ProGuard, you need tookeep some classes.</span></span> <span data-ttu-id="ea59c-115">Program hello następującego fragmentu konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="ea59c-115">You can use hello following configuration snippet:</span></span>
> 
> <span data-ttu-id="ea59c-116">-zachować Klasa publiczna * rozszerza android.os.IInterface — Zachowaj {com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS — klasa</span><span class="sxs-lookup"><span data-stu-id="ea59c-116">-keep public class * extends android.os.IInterface -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {</span></span>
> 
> <span data-ttu-id="ea59c-117"><methods>; }</span><span class="sxs-lookup"><span data-stu-id="ea59c-117"><methods>; }</span></span>
> 
> 

<span data-ttu-id="ea59c-118">Określ ciąg połączenia zaangażowania przez wywołanie hello następujące metody w działaniu uruchamiania hello:</span><span class="sxs-lookup"><span data-stu-id="ea59c-118">Specify your Engagement connection string by calling hello following method in hello launcher activity:</span></span>

            EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
            engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
            EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="ea59c-119">Parametry połączenia Hello aplikacji jest wyświetlana w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="ea59c-119">hello connection string for your application is displayed on Azure Portal.</span></span>

* <span data-ttu-id="ea59c-120">Jeśli brakuje, należy dodać hello następujących uprawnień dla systemu Android (przed hello `<application>` tagu):</span><span class="sxs-lookup"><span data-stu-id="ea59c-120">If missing, add hello following Android permissions (before hello `<application>` tag):</span></span>
  
          <uses-permission android:name="android.permission.INTERNET"/>
          <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
* <span data-ttu-id="ea59c-121">Dodaj następujące sekcji hello (między hello `<application>` i `</application>` tagów):</span><span class="sxs-lookup"><span data-stu-id="ea59c-121">Add hello following section (between hello `<application>` and `</application>` tags):</span></span>
  
          <service
            android:name="com.microsoft.azure.engagement.service.EngagementService"
            android:exported="false"
            android:label="<Your application name>Service"
            android:process=":Engagement"/>
* <span data-ttu-id="ea59c-122">Zmień `<Your application name>` hello nazwę aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ea59c-122">Change `<Your application name>` by hello name of your application.</span></span>

> [!TIP]
> <span data-ttu-id="ea59c-123">Witaj `android:label` atrybutu pozwala toochoose nazwę hello hello usługi Engagement jak będzie wyświetlany użytkownikom końcowym toohello ekranie powitania "Uruchamianie usługi" Telefon.</span><span class="sxs-lookup"><span data-stu-id="ea59c-123">hello `android:label` attribute allows you toochoose hello name of hello Engagement service as it will appear toohello end-users in hello "Running services" screen of their phone.</span></span> <span data-ttu-id="ea59c-124">Jest zalecana tooset za ten atrybut`"<Your application name>Service"` (np. `"AcmeFunGameService"`).</span><span class="sxs-lookup"><span data-stu-id="ea59c-124">It is recommended tooset this attribute too`"<Your application name>Service"` (e.g. `"AcmeFunGameService"`).</span></span>
> 
> 

<span data-ttu-id="ea59c-125">Określanie hello `android:process` zapewnia atrybut tej usługi Engagement hello będą uruchamiane w swoim własnym procesie (uruchomionego zaangażowania w hello tego samego procesu jak aplikacji spowoduje, że Twoje main/wątku interfejsu użytkownika będzie potencjalnie mniej dynamiczne).</span><span class="sxs-lookup"><span data-stu-id="ea59c-125">Specifying hello `android:process` attribute ensures that hello Engagement service will run in its own process (running Engagement in hello same process as your application will make your main/UI thread potentially less responsive).</span></span>

> [!NOTE]
> <span data-ttu-id="ea59c-126">Kod umieszczony w `Application.onCreate()` i innych wywołań zwrotnych aplikacji zostanie uruchomione dla procesów wszystkich aplikacji, w tym hello usługi Engagement.</span><span class="sxs-lookup"><span data-stu-id="ea59c-126">Any code you place in `Application.onCreate()` and other application callbacks will be run for all your application's processes, including hello Engagement service.</span></span> <span data-ttu-id="ea59c-127">Może mieć niepożądane skutki uboczne (takich jak przydziału pamięci niepotrzebnych i wątków w procesie hello zaangażowania, zduplikowany odbiorniki emisji lub usługi).</span><span class="sxs-lookup"><span data-stu-id="ea59c-127">It may have unwanted side effects (like unneeded memory allocations and threads in hello Engagement's process, duplicate broadcast receivers or services).</span></span>
> 
> 

<span data-ttu-id="ea59c-128">Jeśli można zastąpić `Application.onCreate()`, jest zalecane tooadd hello następującego fragmentu kodu na początku hello Twojej `Application.onCreate()` funkcji:</span><span class="sxs-lookup"><span data-stu-id="ea59c-128">If you override `Application.onCreate()`, it's recommended tooadd hello following code snippet at hello beginning of your `Application.onCreate()` function:</span></span>

             public void onCreate()
             {
               if (EngagementAgentUtils.isInDedicatedEngagementProcess(this))
                 return;

               ... Your code...
             }

<span data-ttu-id="ea59c-129">Możesz zrobić hello samo dla `Application.onTerminate()`, `Application.onLowMemory()` i `Application.onConfigurationChanged(...)`.</span><span class="sxs-lookup"><span data-stu-id="ea59c-129">You can do hello same thing for `Application.onTerminate()`, `Application.onLowMemory()` and `Application.onConfigurationChanged(...)`.</span></span>

<span data-ttu-id="ea59c-130">Można również rozszerzyć zasięg `EngagementApplication` zamiast rozszerzanie `Application`: hello wywołania zwrotnego `Application.onCreate()` hello procesu wyboru i wywołania `Application.onApplicationProcessCreate()` tylko jeśli hello bieżący proces jest nie hello jeden hello zaangażowania Usługa hostingu, hello te same zasady stosowane dla Witaj innych wywołań zwrotnych.</span><span class="sxs-lookup"><span data-stu-id="ea59c-130">You can also extend `EngagementApplication` instead of extending `Application`: hello callback `Application.onCreate()` does hello process check and calls `Application.onApplicationProcessCreate()` only if hello current process is not hello one hosting hello Engagement service, hello same rules apply for hello other callbacks.</span></span>

## <a name="basic-reporting"></a><span data-ttu-id="ea59c-131">Podstawowym raportowaniem</span><span class="sxs-lookup"><span data-stu-id="ea59c-131">Basic reporting</span></span>
### <a name="recommended-method-overload-your-activity-classes"></a><span data-ttu-id="ea59c-132">Zalecana metoda: przeciążenia sieci `Activity` klas</span><span class="sxs-lookup"><span data-stu-id="ea59c-132">Recommended method: overload your `Activity` classes</span></span>
<span data-ttu-id="ea59c-133">W raporcie hello tooactivate kolejności wszystkich dzienników hello wymagane przez zaangażowania toocompute użytkowników, sesji, działania, awarii (Crash) i statystyki technicznych, wystarczy toomake wszystkie Twoje `*Activity` klasy podrzędne dziedziczą odpowiadającego hello `Engagement*Activity` klasy (np. Jeśli działanie starszej wersji `ListActivity`, Utwórz rozszerza `EngagementListActivity`).</span><span class="sxs-lookup"><span data-stu-id="ea59c-133">In order tooactivate hello report of all hello logs required by Engagement toocompute Users, Sessions, Activities, Crashes and Technical statistics, you just have toomake all your `*Activity` sub-classes inherit from hello corresponding `Engagement*Activity` classes (e.g. if your legacy activity extends `ListActivity`, make it extends `EngagementListActivity`).</span></span>

<span data-ttu-id="ea59c-134">**Bez usługi Engagement:**</span><span class="sxs-lookup"><span data-stu-id="ea59c-134">**Without Engagement :**</span></span>

            package com.company.myapp;

            import android.app.Activity;
            import android.os.Bundle;

            public class MyApp extends Activity
            {
              @Override
              public void onCreate(Bundle savedInstanceState)
              {
                super.onCreate(savedInstanceState);
                setContentView(R.layout.main);
              }
            }

<span data-ttu-id="ea59c-135">**Z usługi Engagement:**</span><span class="sxs-lookup"><span data-stu-id="ea59c-135">**With Engagement :**</span></span>

            package com.company.myapp;

            import com.microsoft.azure.engagement.activity.EngagementActivity;
            import android.os.Bundle;

            public class MyApp extends EngagementActivity
            {
              @Override
              public void onCreate(Bundle savedInstanceState)
              {
                super.onCreate(savedInstanceState);
                setContentView(R.layout.main);
              }
            }

> [!IMPORTANT]
> <span data-ttu-id="ea59c-136">Korzystając z `EngagementListActivity` lub `EngagementExpandableListActivity`, upewnij się, że w żadnym wywołaniu zbyt`requestWindowFeature(...);` dokonane przed wywołaniem hello zbyt`super.onCreate(...);`, w przeciwnym razie wystąpi awaria.</span><span class="sxs-lookup"><span data-stu-id="ea59c-136">When using `EngagementListActivity` or `EngagementExpandableListActivity`, make sure any call too`requestWindowFeature(...);` is made before hello call too`super.onCreate(...);`, otherwise a crash will occur.</span></span>
> 
> 

<span data-ttu-id="ea59c-137">Te klasy można znaleźć w hello `src` folderu i skopiować je do projektu.</span><span class="sxs-lookup"><span data-stu-id="ea59c-137">You can find these classes in hello `src` folder, and can copy them into your project.</span></span> <span data-ttu-id="ea59c-138">klasy Hello znajdują się również w hello **JavaDoc**.</span><span class="sxs-lookup"><span data-stu-id="ea59c-138">hello classes are also in hello **JavaDoc**.</span></span>

### <a name="alternate-method-call-startactivity-and-endactivity-manually"></a><span data-ttu-id="ea59c-139">Alternatywna metoda: wywołanie `startActivity()` i `endActivity()` ręcznie</span><span class="sxs-lookup"><span data-stu-id="ea59c-139">Alternate method: call `startActivity()` and `endActivity()` manually</span></span>
<span data-ttu-id="ea59c-140">Jeśli nie możesz lub nie ma toooverload Twojego `Activity` klasy, można zamiast tego rozpoczęcia i zakończenia działań przez wywołanie metody `EngagementAgent`przez metody bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="ea59c-140">If you cannot or do not want toooverload your `Activity` classes, you can instead start and end your activities by calling `EngagementAgent`'s methods directly.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ea59c-141">zestaw SDK systemu Android Hello nigdy nie wywołuje hello `endActivity()` metody, nawet wtedy, gdy aplikacja hello jest zamknięta (w systemie Android, aplikacje są faktycznie nigdy nie zamknięte).</span><span class="sxs-lookup"><span data-stu-id="ea59c-141">hello Android SDK never calls hello `endActivity()` method, even when hello application is closed (on Android, applications are actually never closed).</span></span> <span data-ttu-id="ea59c-142">W związku z tym jest *wysokiej* zalecane toocall hello `startActivity()` metoda hello `onResume` wywołania zwrotnego z *wszystkie* działań i hello `endActivity()` metoda hello `onPause()` Wywołanie zwrotne z *wszystkie* działań.</span><span class="sxs-lookup"><span data-stu-id="ea59c-142">Thus, it is *HIGHLY* recommended toocall hello `startActivity()` method in hello `onResume` callback of *ALL* your activities, and hello `endActivity()` method in hello `onPause()` callback of *ALL* your activities.</span></span> <span data-ttu-id="ea59c-143">Jest to hello tylko sposób toobe się upewnić, że sesje nie zostaną ujawnione.</span><span class="sxs-lookup"><span data-stu-id="ea59c-143">This is hello only way toobe sure that sessions will not be leaked.</span></span> <span data-ttu-id="ea59c-144">Jeśli przeciek sesji hello usługi Engagement nigdy nie spowoduje rozłączenie z zapleczem usługi Engagement hello (ponieważ usługa hello połączono tak długo, jak długo trwa oczekiwanie na sesji).</span><span class="sxs-lookup"><span data-stu-id="ea59c-144">If a session is leaked, hello Engagement service will never disconnect from hello Engagement backend (since hello service stays connected as long as a session is pending).</span></span>
> 
> 

<span data-ttu-id="ea59c-145">Oto przykład:</span><span class="sxs-lookup"><span data-stu-id="ea59c-145">Here is an example:</span></span>

            public class MyActivity extends Some3rdPartyActivity
            {
              @Override
              protected void onResume()
              {
                super.onResume();
                String activityNameOnEngagement = EngagementAgentUtils.buildEngagementActivityName(getClass()); // Uses short class name and removes "Activity" at hello end.
                EngagementAgent.getInstance(this).startActivity(this, activityNameOnEngagement, null);
              }

              @Override
              protected void onPause()
              {
                super.onPause();
                EngagementAgent.getInstance(this).endActivity();
              }
            }

<span data-ttu-id="ea59c-146">Ten przykład toohello bardzo podobne `EngagementActivity` klasy i jej wariantów, którego kod źródłowy jest udostępniany w hello `src` folderu.</span><span class="sxs-lookup"><span data-stu-id="ea59c-146">This example very similiar toohello `EngagementActivity` class and its variants, whose source code is provided in hello `src` folder.</span></span>

## <a name="test"></a><span data-ttu-id="ea59c-147">Testowanie</span><span class="sxs-lookup"><span data-stu-id="ea59c-147">Test</span></span>
<span data-ttu-id="ea59c-148">Teraz Sprawdź, czy integracją przez uruchomienie aplikacji mobilnej w emulator lub urządzenie i weryfikowanie rejestruje sesji na karcie monitorowanie hello.</span><span class="sxs-lookup"><span data-stu-id="ea59c-148">Now please verify your integration by running your mobile app in an emulator or device and verifying that it registers a session on hello Monitor tab.</span></span>

<span data-ttu-id="ea59c-149">następne sekcje Hello są opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="ea59c-149">hello next sections are optional.</span></span>

## <a name="location-reporting"></a><span data-ttu-id="ea59c-150">Raportowanie lokalizacji</span><span class="sxs-lookup"><span data-stu-id="ea59c-150">Location reporting</span></span>
<span data-ttu-id="ea59c-151">Jeśli chcesz toobe lokalizacji zgłoszone, należy tooadd kilka wierszy konfiguracji (między hello `<application>` i `</application>` tagów).</span><span class="sxs-lookup"><span data-stu-id="ea59c-151">If you want locations toobe reported, you need tooadd a few lines of configuration (between hello `<application>` and `</application>` tags).</span></span>

### <a name="lazy-area-location-reporting"></a><span data-ttu-id="ea59c-152">Raportowanie lokalizacji obszaru z opóźnieniem</span><span class="sxs-lookup"><span data-stu-id="ea59c-152">Lazy area location reporting</span></span>
<span data-ttu-id="ea59c-153">Raportowanie lokalizacji obszaru z opóźnieniem umożliwia tooreport hello kraj, region i lokalizację skojarzone toodevices.</span><span class="sxs-lookup"><span data-stu-id="ea59c-153">Lazy area location reporting allows tooreport hello country, region and locality associated toodevices.</span></span> <span data-ttu-id="ea59c-154">Raportowanie lokalizacji tego typu używa tylko lokalizacje sieciowe (na podstawie Identyfikatora komórki lub Wi-Fi).</span><span class="sxs-lookup"><span data-stu-id="ea59c-154">This type of location reporting only uses network locations (based on Cell ID or WIFI).</span></span> <span data-ttu-id="ea59c-155">obszar urządzenia Hello jest zgłaszana co najwyżej raz na sesję.</span><span class="sxs-lookup"><span data-stu-id="ea59c-155">hello device area is reported at most once per session.</span></span> <span data-ttu-id="ea59c-156">Hello GPS nie jest nigdy używana, a zatem ten typ lokalizacji raportu ma bardzo nieliczne (nie toosay żadnych) wpływ na powitania baterii.</span><span class="sxs-lookup"><span data-stu-id="ea59c-156">hello GPS is never used, and thus this type of location report has very few (not toosay no) impact on hello battery.</span></span>

<span data-ttu-id="ea59c-157">Obszary zgłoszone są używane toocompute geograficzne statystyki dotyczące użytkowników, sesji, zdarzenia i błędy.</span><span class="sxs-lookup"><span data-stu-id="ea59c-157">Reported areas are used toocompute geographic statistics about users, sessions, events and errors.</span></span> <span data-ttu-id="ea59c-158">Mogą one również używane jako kryterium w kampanie Zasięgowe.</span><span class="sxs-lookup"><span data-stu-id="ea59c-158">They can also be used as criterion in Reach campaigns.</span></span>

<span data-ttu-id="ea59c-159">lokalizacji obszaru z opóźnieniem tooenable raportowania, możesz zrobić to za pomocą konfiguracji hello wymienione wcześniej w tej procedurze:</span><span class="sxs-lookup"><span data-stu-id="ea59c-159">tooenable lazy area location reporting, you can do it by using hello configuration previously mentioned in this procedure :</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setLazyAreaLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="ea59c-160">Należy również następujące uprawnienia, jeśli brakuje hello tooadd:</span><span class="sxs-lookup"><span data-stu-id="ea59c-160">You also need tooadd hello following permission if missing:</span></span>

            <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

<span data-ttu-id="ea59c-161">Lub możesz korzystać ``ACCESS_FINE_LOCATION`` Jeśli już używać w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ea59c-161">Or you can keep using ``ACCESS_FINE_LOCATION`` if you already use it in your application.</span></span>

### <a name="real-time-location-reporting"></a><span data-ttu-id="ea59c-162">Raportowanie lokalizacji w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="ea59c-162">Real time location reporting</span></span>
<span data-ttu-id="ea59c-163">Raportowanie lokalizacji w czasie rzeczywistym umożliwia tooreport hello szerokości i długości geograficznej skojarzone toodevices.</span><span class="sxs-lookup"><span data-stu-id="ea59c-163">Real time location reporting allows tooreport hello latitude and longitude associated toodevices.</span></span> <span data-ttu-id="ea59c-164">Domyślnie raportowanie lokalizacji tego typu używa tylko lokalizacje sieciowe (na podstawie Identyfikatora komórki lub Wi-Fi), a raportowanie hello jest aktywny tylko po hello aplikacja jest uruchamiana na pierwszym planie (np. podczas sesji).</span><span class="sxs-lookup"><span data-stu-id="ea59c-164">By default, this type of location reporting only uses network locations (based on Cell ID or WIFI), and hello reporting is only active when hello application runs in foreground (i.e. during a session).</span></span>

<span data-ttu-id="ea59c-165">Lokalizacje w czasie rzeczywistym *nie* używane toocompute statystyk.</span><span class="sxs-lookup"><span data-stu-id="ea59c-165">Real time locations are *NOT* used toocompute statistics.</span></span> <span data-ttu-id="ea59c-166">Ich jedynym celem jest użycie hello tooallow grodzenia czasu rzeczywistego \<Reach-odbiorców geofencing\> kryterium w kampanie Zasięgowe.</span><span class="sxs-lookup"><span data-stu-id="ea59c-166">Their only purpose is tooallow hello use of real time geo-fencing \<Reach-Audience-geofencing\> criterion in Reach campaigns.</span></span>

<span data-ttu-id="ea59c-167">Lokalizacja czasu rzeczywistego tooenable raportowania, możesz zrobić to za pomocą konfiguracji hello wymienione wcześniej w tej procedurze:</span><span class="sxs-lookup"><span data-stu-id="ea59c-167">tooenable real time location reporting, you can do it by using hello configuration previously mentioned in this procedure :</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="ea59c-168">Należy również następujące uprawnienia, jeśli brakuje hello tooadd:</span><span class="sxs-lookup"><span data-stu-id="ea59c-168">You also need tooadd hello following permission if missing:</span></span>

            <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

<span data-ttu-id="ea59c-169">Lub możesz korzystać ``ACCESS_FINE_LOCATION`` Jeśli już używać w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ea59c-169">Or you can keep using ``ACCESS_FINE_LOCATION`` if you already use it in your application.</span></span>

#### <a name="gps-based-reporting"></a><span data-ttu-id="ea59c-170">GPS na podstawie raportowania</span><span class="sxs-lookup"><span data-stu-id="ea59c-170">GPS based reporting</span></span>
<span data-ttu-id="ea59c-171">Domyślnie raportowanie lokalizacji w czasie rzeczywistym używa tylko lokalizacje sieciowe.</span><span class="sxs-lookup"><span data-stu-id="ea59c-171">By default, real time location reporting only uses network based locations.</span></span> <span data-ttu-id="ea59c-172">Użycie hello tooenable GPS na podstawie lokalizacji (które są znacznie bardziej precyzyjne), użyj obiektu konfiguracji hello:</span><span class="sxs-lookup"><span data-stu-id="ea59c-172">tooenable hello use of GPS based locations (which are far more precise), use hello configuration object:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setFineRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="ea59c-173">Należy również następujące uprawnienia, jeśli brakuje hello tooadd:</span><span class="sxs-lookup"><span data-stu-id="ea59c-173">You also need tooadd hello following permission if missing:</span></span>

            <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>

#### <a name="background-reporting"></a><span data-ttu-id="ea59c-174">Raportowanie w tle</span><span class="sxs-lookup"><span data-stu-id="ea59c-174">Background reporting</span></span>
<span data-ttu-id="ea59c-175">Domyślnie raportowanie lokalizacji w czasie rzeczywistym jest aktywne uruchomienie aplikacji hello na pierwszym planie (np. podczas sesji).</span><span class="sxs-lookup"><span data-stu-id="ea59c-175">By default, real time location reporting is only active when hello application runs in foreground (i.e. during a session).</span></span> <span data-ttu-id="ea59c-176">raportowania hello tooenable również w tle, użyj obiektu konfiguracji hello:</span><span class="sxs-lookup"><span data-stu-id="ea59c-176">tooenable hello reporting also in background, use hello configuration object:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setBackgroundRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

> [!NOTE]
> <span data-ttu-id="ea59c-177">Po uruchomieniu aplikacji hello w tle, tylko lokalizacje sieciowe są raportowane, nawet jeśli włączono hello GPS.</span><span class="sxs-lookup"><span data-stu-id="ea59c-177">When hello application runs in background, only network based locations are reported, even if you enabled hello GPS.</span></span>
> 
> 

<span data-ttu-id="ea59c-178">Hello tła lokalizacji raportu zostanie zatrzymana, jeśli użytkownik hello ponownym uruchomieniu urządzenia, można dodać tego toomake automatycznie uruchomiony ponownie w czasie rozruchu:</span><span class="sxs-lookup"><span data-stu-id="ea59c-178">hello background location report will be stopped if hello user reboots its device, you can add this toomake it automatically restart at boot time:</span></span>

            <receiver android:name="com.microsoft.azure.engagement.EngagementLocationBootReceiver"
               android:exported="false">
               <intent-filter>
                  <action android:name="android.intent.action.BOOT_COMPLETED" />
               </intent-filter>
            </receiver>

<span data-ttu-id="ea59c-179">Należy również następujące uprawnienia, jeśli brakuje hello tooadd:</span><span class="sxs-lookup"><span data-stu-id="ea59c-179">You also need tooadd hello following permission if missing:</span></span>

            <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />

### <a name="android-m-permissions"></a><span data-ttu-id="ea59c-180">Android M uprawnień</span><span class="sxs-lookup"><span data-stu-id="ea59c-180">Android M permissions</span></span>
<span data-ttu-id="ea59c-181">Począwszy od systemu Android M, niektóre uprawnienia są zarządzane w czasie wykonywania i wymaga zatwierdzenia użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ea59c-181">Starting with Android M, some permissions are managed at runtime and needs user approval.</span></span>

<span data-ttu-id="ea59c-182">Hello środowiska uruchomieniowego uprawnienia zostaną wyłączone domyślnie do nowych instalacji aplikacji, w przypadku skierowania interfejsu API systemu Android na poziomie 23.</span><span class="sxs-lookup"><span data-stu-id="ea59c-182">hello runtime permissions will be turned off by default for new app installations if you target Android API level 23.</span></span> <span data-ttu-id="ea59c-183">W przeciwnym razie ona zostanie włączona domyślnie.</span><span class="sxs-lookup"><span data-stu-id="ea59c-183">Otherwise it will be turned on by default.</span></span>

<span data-ttu-id="ea59c-184">Hello użytkownika można włączyć/wyłączyć te uprawnienia z menu ustawień urządzenia hello.</span><span class="sxs-lookup"><span data-stu-id="ea59c-184">hello user can enable/disable those permissions from hello device settings menu.</span></span> <span data-ttu-id="ea59c-185">Wyłączenie uprawnień z menu systemowe kasuje procesów w tle aplikacji hello, jest zachowanie systemu które nie ma wpływu na możliwość tooreceive wypychania w tle.</span><span class="sxs-lookup"><span data-stu-id="ea59c-185">Turning off permissions from system menu kills background processes of hello application, this is a system behavior and has no impact on ability tooreceive push in background.</span></span>

<span data-ttu-id="ea59c-186">W kontekście hello Mobile Engagement hello uprawnienia, które wymagają zatwierdzenia w czasie wykonywania są:</span><span class="sxs-lookup"><span data-stu-id="ea59c-186">In hello context of Mobile Engagement, hello permissions that require approval at runtime are:</span></span>

* `ACCESS_COARSE_LOCATION`
* `ACCESS_FINE_LOCATION`
* <span data-ttu-id="ea59c-187">`WRITE_EXTERNAL_STORAGE`(tylko wtedy, gdy przeznaczonych dla interfejsu API systemu Android na poziomie 23 tej)</span><span class="sxs-lookup"><span data-stu-id="ea59c-187">`WRITE_EXTERNAL_STORAGE` (only when targeting Android API level 23 for this one)</span></span>

<span data-ttu-id="ea59c-188">magazynu zewnętrznego Hello jest używany tylko dla funkcji szerszej Reach.</span><span class="sxs-lookup"><span data-stu-id="ea59c-188">hello external storage is used only for Reach big picture feature.</span></span> <span data-ttu-id="ea59c-189">Jeśli okaże się, prosząc użytkowników o tym destrukcyjne toobe uprawnienia, możesz je usunąć używane tylko w przypadku usługi Mobile Engagement, ale się to kosztem hello wyłączenia funkcji Duży obraz.</span><span class="sxs-lookup"><span data-stu-id="ea59c-189">If you find asking users this permission toobe disruptive, you can remove it if you used it only for Mobile Engagement but at hello cost of disabling big picture feature.</span></span>

<span data-ttu-id="ea59c-190">W przypadku funkcji lokalizacji hello należy zażądać toouser uprawnienia za pomocą okna dialogowego standardowy system.</span><span class="sxs-lookup"><span data-stu-id="ea59c-190">For hello location features, you should request permissions toouser using a standard system dialog.</span></span> <span data-ttu-id="ea59c-191">Jeśli zatwierdza hello użytkownika, należy tootell ``EngagementAgent`` tootake, która zmienia pod uwagę w czasie rzeczywistym (w przeciwnym razie Zmień hello będzie przetworzonych hello dalej hello użytkownika powoduje uruchomienie hello aplikacji w czasie).</span><span class="sxs-lookup"><span data-stu-id="ea59c-191">If hello user approves, you need tootell ``EngagementAgent`` tootake that change into account in real time (otherwise hello change will be processed hello next time hello user launches hello application).</span></span>

<span data-ttu-id="ea59c-192">Oto toouse przykładowy kod w działaniu aplikacji toorequest uprawnienia i do przodu hello wynik Jeśli dodatnią zbyt``EngagementAgent``:</span><span class="sxs-lookup"><span data-stu-id="ea59c-192">Here is a code sample toouse in an activity of your application toorequest permissions and forward hello result if positive too``EngagementAgent``:</span></span>

    @Override
    public void onCreate(Bundle savedInstanceState)
    {
      /* Other code... */

      /* Request permissions */
      requestPermissions();
    }

    @TargetApi(Build.VERSION_CODES.M)
    private void requestPermissions()
    {
      /* Avoid crashing if not on Android M */
      if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.M)
      {
        /*
         * Request location permission, but this won't explain why it is needed toohello user.
         * hello standard Android documentation explains with more details how toodisplay a rationale activity tooexplain hello user why hello permission is needed in your application.
         * Putting COARSE vs FINE has no impact here, they are part of hello same group for runtime permission management.
         */
        if (checkSelfPermission(android.Manifest.permission.ACCESS_FINE_LOCATION) != PackageManager.PERMISSION_GRANTED)
          requestPermissions(new String[] { android.Manifest.permission.ACCESS_FINE_LOCATION }, 0);

        /* Only if you want tookeep features using external storage */
        if (checkSelfPermission(android.Manifest.permission.WRITE_EXTERNAL_STORAGE) != PackageManager.PERMISSION_GRANTED)
          requestPermissions(new String[] { android.Manifest.permission.WRITE_EXTERNAL_STORAGE }, 1);
      }
    }

    @Override
    public void onRequestPermissionsResult(int requestCode, String[] permissions, int[] grantResults)
    {
      /* Only a positive location permission update requires engagement agent refresh, hence hello request code matching from above function */
      if (requestCode == 0 && grantResults[0] == PackageManager.PERMISSION_GRANTED)
        getEngagementAgent().refreshPermissions();
    }

## <a name="advanced-reporting"></a><span data-ttu-id="ea59c-193">Zaawansowane raportowanie</span><span class="sxs-lookup"><span data-stu-id="ea59c-193">Advanced reporting</span></span>
<span data-ttu-id="ea59c-194">Opcjonalnie, jeśli chcesz tooreport aplikacji określonych zdarzeń, błędów i zadań, należy toouse hello zaangażowania interfejsu API za pomocą metody hello hello `EngagementAgent` klasy.</span><span class="sxs-lookup"><span data-stu-id="ea59c-194">Optionally, if you want tooreport application specific events, errors and jobs, you need toouse hello Engagement API through hello methods of hello `EngagementAgent` class.</span></span> <span data-ttu-id="ea59c-195">Obiekt tej klasy może być pobranych przez wywołanie hello `EngagementAgent.getInstance()` metody statycznej.</span><span class="sxs-lookup"><span data-stu-id="ea59c-195">An object of this class can be retreived by calling hello `EngagementAgent.getInstance()` static method.</span></span>

<span data-ttu-id="ea59c-196">Hello zaangażowania interfejs API umożliwia toouse wszystkie funkcje zaawansowane usługi Engagement i została szczegółowo opisana na powitania jak tooUse interfejsu API programu zaangażowania w systemie Android (a także w dokumentacji technicznej hello hello `EngagementAgent` klasy).</span><span class="sxs-lookup"><span data-stu-id="ea59c-196">hello Engagement API allows toouse all of Engagement's advanced capabilities and is detailed in hello How tooUse the Engagement API on Android (as well as in hello technical documentation of hello `EngagementAgent` class).</span></span>

## <a name="advanced-configuration-in-androidmanifestxml"></a><span data-ttu-id="ea59c-197">Konfiguracja zaawansowana (w pliku AndroidManifest.xml)</span><span class="sxs-lookup"><span data-stu-id="ea59c-197">Advanced configuration (in AndroidManifest.xml)</span></span>
### <a name="wake-locks"></a><span data-ttu-id="ea59c-198">Wznawianie pracy blokad</span><span class="sxs-lookup"><span data-stu-id="ea59c-198">Wake locks</span></span>
<span data-ttu-id="ea59c-199">Toobe się upewnić, że statystyki są wysyłane w czasie rzeczywistym za pomocą sieci Wi-Fi lub ekranu hello jest wyłączona, dodać hello następujące uprawnienia opcjonalne:</span><span class="sxs-lookup"><span data-stu-id="ea59c-199">If you want toobe sure that statistics are sent in real time when using Wifi or when hello screen is off, add hello following optional permission:</span></span>

            <uses-permission android:name="android.permission.WAKE_LOCK"/>

### <a name="crash-report"></a><span data-ttu-id="ea59c-200">Raport o awarii</span><span class="sxs-lookup"><span data-stu-id="ea59c-200">Crash report</span></span>
<span data-ttu-id="ea59c-201">Raporty awarii toodisable, należy dodać to (między hello `<application>` i `</application>` tagów):</span><span class="sxs-lookup"><span data-stu-id="ea59c-201">If you want toodisable crash reports, add this (between hello `<application>` and `</application>` tags):</span></span>

            <meta-data android:name="engagement:reportCrash" android:value="false"/>

### <a name="burst-threshold"></a><span data-ttu-id="ea59c-202">Próg serii</span><span class="sxs-lookup"><span data-stu-id="ea59c-202">Burst threshold</span></span>
<span data-ttu-id="ea59c-203">Domyślnie raporty usługi Engagement hello rejestruje się w czasie rzeczywistym.</span><span class="sxs-lookup"><span data-stu-id="ea59c-203">By default, hello Engagement service reports logs in real time.</span></span> <span data-ttu-id="ea59c-204">Jeśli aplikacja zgłasza dzienniki bardzo często, jest lepsze toobuffer hello dzienniki i tooreport ich jednocześnie na regularne podstawy czasu (jest to nazywane hello "tryb serii").</span><span class="sxs-lookup"><span data-stu-id="ea59c-204">If your application reports logs very frequently, it is better toobuffer hello logs and tooreport them all at once on a regular time base (this is called hello "burst mode").</span></span> <span data-ttu-id="ea59c-205">toodo tak, dodaj ją (między hello `<application>` i `</application>` tagów):</span><span class="sxs-lookup"><span data-stu-id="ea59c-205">toodo so, add this (between hello `<application>` and `</application>` tags):</span></span>

            <meta-data android:name="engagement:burstThreshold" android:value="{interval between too bursts (in milliseconds)}"/>

<span data-ttu-id="ea59c-206">Witaj tryb serii wydłużyć baterii hello życia ale ma wpływ na powitania Monitor zaangażowania: wszystkie czas trwania zadania i sesje będą zaokrąglone toohello serii próg (w związku z tym sesji i zadania krótsze niż próg serii hello może nie być widoczna).</span><span class="sxs-lookup"><span data-stu-id="ea59c-206">hello burst mode slightly increase hello battery life but has an impact on hello Engagement Monitor: all sessions and jobs duration will be rounded toohello burst threshold (thus, sessions and jobs shorter than hello burst threshold may not be visible).</span></span> <span data-ttu-id="ea59c-207">Jest zalecana toouse próg w serii się niż 30000 (30s).</span><span class="sxs-lookup"><span data-stu-id="ea59c-207">It is recommended toouse a burst threshold no longer than 30000 (30s).</span></span>

### <a name="session-timeout"></a><span data-ttu-id="ea59c-208">Limit czasu sesji</span><span class="sxs-lookup"><span data-stu-id="ea59c-208">Session timeout</span></span>
<span data-ttu-id="ea59c-209">Domyślnie sesja jest 10s zakończone po zakończeniu hello jego ostatniej aktywności (która zazwyczaj występuje przez naciśnięcie przycisku hello Home lub kopii klucza, przez ustawienie hello phone bezczynności lub przejście do innej aplikacji).</span><span class="sxs-lookup"><span data-stu-id="ea59c-209">By default, a session is ended 10s after hello end of its last activity (which usually occurs by pressing hello Home or Back key, by setting hello phone idle or by jumping into another application).</span></span> <span data-ttu-id="ea59c-210">Jest to tooavoid podziału sesji każdego użytkownika w czasie hello wyjść i bardzo szybko powrócić toohello aplikacji (które mogą wystąpić podczas odebrania on obrazu, sprawdź powiadomienia itp.).</span><span class="sxs-lookup"><span data-stu-id="ea59c-210">This is tooavoid a session split each time hello user exit and return toohello application very quickly (which can happen when he pick up a image, check a notification, etc.).</span></span> <span data-ttu-id="ea59c-211">Ten parametr może być toomodify.</span><span class="sxs-lookup"><span data-stu-id="ea59c-211">You may want toomodify this parameter.</span></span> <span data-ttu-id="ea59c-212">toodo tak, dodaj ją (między hello `<application>` i `</application>` tagów):</span><span class="sxs-lookup"><span data-stu-id="ea59c-212">toodo so, add this (between hello `<application>` and `</application>` tags):</span></span>

            <meta-data android:name="engagement:sessionTimeout" android:value="{session timeout (in milliseconds)}"/>

## <a name="disable-log-reporting"></a><span data-ttu-id="ea59c-213">Wyłączanie dziennika raportowania</span><span class="sxs-lookup"><span data-stu-id="ea59c-213">Disable log reporting</span></span>
### <a name="using-a-method-call"></a><span data-ttu-id="ea59c-214">Przy użyciu wywołania metody</span><span class="sxs-lookup"><span data-stu-id="ea59c-214">Using a method call</span></span>
<span data-ttu-id="ea59c-215">Jeśli chcesz toostop zaangażowania wysyłania dzienników, można wywołać:</span><span class="sxs-lookup"><span data-stu-id="ea59c-215">If you want Engagement toostop sending logs, you can call:</span></span>

            EngagementAgent.getInstance(context).setEnabled(false);

<span data-ttu-id="ea59c-216">To wywołanie jest trwały: używa plików udostępnionych preferencji.</span><span class="sxs-lookup"><span data-stu-id="ea59c-216">This call is persistent: it uses a shared preferences file.</span></span>

<span data-ttu-id="ea59c-217">Jeśli zaangażowania jest aktywny, gdy wywołanie tej funkcji, może upłynąć 1 minutę hello toostop usługi.</span><span class="sxs-lookup"><span data-stu-id="ea59c-217">If Engagement is active when you call this function, it may take 1 minute for hello service toostop.</span></span> <span data-ttu-id="ea59c-218">Jednak nie będzie uruchomić usługi hello na wszystkich hello następnym uruchomieniu aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="ea59c-218">However it won't launch hello service at all hello next time you launch hello application.</span></span>

<span data-ttu-id="ea59c-219">Możesz włączyć ponownie raportowania przez wywołanie metody hello sam działać z dziennika `true`.</span><span class="sxs-lookup"><span data-stu-id="ea59c-219">You can enable log reporting again by calling hello same function with `true`.</span></span>

### <a name="integration-in-your-own-preferenceactivity"></a><span data-ttu-id="ea59c-220">Integracja z własną`PreferenceActivity`</span><span class="sxs-lookup"><span data-stu-id="ea59c-220">Integration in your own `PreferenceActivity`</span></span>
<span data-ttu-id="ea59c-221">Zamiast wywoływania tej funkcji, to ustawienie można również zintegrować bezpośrednio w istniejącą `PreferenceActivity`.</span><span class="sxs-lookup"><span data-stu-id="ea59c-221">Instead of calling this function, you can also integrate this setting directly in your existing `PreferenceActivity`.</span></span>

<span data-ttu-id="ea59c-222">Toouse zaangażowania preferencje plików (w trybie żądaną hello) można skonfigurować w hello `AndroidManifest.xml` pliku z `application meta-data`:</span><span class="sxs-lookup"><span data-stu-id="ea59c-222">You can configure Engagement toouse your preferences file (with hello desired mode) in hello `AndroidManifest.xml` file with `application meta-data`:</span></span>

* <span data-ttu-id="ea59c-223">Witaj `engagement:agent:settings:name` klucz to nazwa hello toodefine używanych plików udostępnionych preferencji hello.</span><span class="sxs-lookup"><span data-stu-id="ea59c-223">hello `engagement:agent:settings:name` key is used toodefine hello name of hello shared preferences file.</span></span>
* <span data-ttu-id="ea59c-224">Witaj `engagement:agent:settings:mode` klucza jest tryb hello toodefine używanych plików udostępnionych preferencji hello, należy użyć hello tego samego trybu jako w Twojej `PreferenceActivity`.</span><span class="sxs-lookup"><span data-stu-id="ea59c-224">hello `engagement:agent:settings:mode` key is used toodefine hello mode of hello shared preferences file, you should use hello same mode as in your `PreferenceActivity`.</span></span> <span data-ttu-id="ea59c-225">Tryb Hello muszą być przekazywane w postaci liczby: Jeśli korzystasz z kombinacją flag stałej w kodzie, sprawdź wartość całkowita hello.</span><span class="sxs-lookup"><span data-stu-id="ea59c-225">hello mode must be passed as a number: if you are using a combination of constant flags in your code, check hello total value.</span></span>

<span data-ttu-id="ea59c-226">Zaangażowania zawsze używać hello `engagement:key` logiczna klucz w pliku preferencji hello zarządzania to ustawienie.</span><span class="sxs-lookup"><span data-stu-id="ea59c-226">Engagement always use hello `engagement:key` boolean key within hello preferences file for managing this setting.</span></span>

<span data-ttu-id="ea59c-227">Witaj następujący przykład `AndroidManifest.xml` pokazuje hello wartości domyślne:</span><span class="sxs-lookup"><span data-stu-id="ea59c-227">hello following example of `AndroidManifest.xml` shows hello default values:</span></span>

            <application>
                [...]
                <meta-data
                  android:name="engagement:agent:settings:name"
                  android:value="engagement.agent" />
                <meta-data
                  android:name="engagement:agent:settings:mode"
                  android:value="0" />

<span data-ttu-id="ea59c-228">Następnie można dodać `CheckBoxPreference` w układzie preferencji, takich jak hello jednym następującego:</span><span class="sxs-lookup"><span data-stu-id="ea59c-228">Then you can add a `CheckBoxPreference` in your preference layout like hello following one:</span></span>

            <CheckBoxPreference
              android:key="engagement:enabled"
              android:defaultValue="true"
              android:title="Use Engagement"
              android:summaryOn="Engagement is enabled."
              android:summaryOff="Engagement is disabled." />

<!-- URLs. -->
[Device API]: http://go.microsoft.com/?linkid=9876094
