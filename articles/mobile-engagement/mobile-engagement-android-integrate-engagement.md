---
title: "Integracja zestawu SDK systemu Android z usługi Azure Mobile Engagement"
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
ms.openlocfilehash: 35bd92e52b7a02f58620a03156902f9f91be57ae
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-integrate-engagement-on-android"></a><span data-ttu-id="0dc90-103">Integrowanie usługi Engagement w systemie Android</span><span class="sxs-lookup"><span data-stu-id="0dc90-103">How to Integrate Engagement on Android</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0dc90-104">Aplikacje uniwersalne systemu Windows</span><span class="sxs-lookup"><span data-stu-id="0dc90-104">Windows Universal</span></span>](mobile-engagement-windows-store-integrate-engagement.md)
> * [<span data-ttu-id="0dc90-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="0dc90-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="0dc90-106">iOS</span><span class="sxs-lookup"><span data-stu-id="0dc90-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="0dc90-107">Android</span><span class="sxs-lookup"><span data-stu-id="0dc90-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md)
> 
> 

<span data-ttu-id="0dc90-108">W tej procedurze opisano Najprostszym sposobem, aby aktywować analizy i funkcji w aplikacji systemu Android monitorowania usługi Engagement.</span><span class="sxs-lookup"><span data-stu-id="0dc90-108">This procedure describes the simplest way to activate Engagement's Analytics and Monitoring functions in your Android application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0dc90-109">Minimalny poziom interfejsu API zestawu SDK systemu Android musi być 10 lub nowszej (Android 2.3.3 lub nowszej).</span><span class="sxs-lookup"><span data-stu-id="0dc90-109">Your minimum Android SDK API level must be 10 or higher (Android 2.3.3 or higher).</span></span>
> 
> 

<span data-ttu-id="0dc90-110">Poniższe kroki są wystarczająca liczba na aktywuje raport dzienniki wymagane do obliczenia wszystkich statystyki dotyczące użytkowników, sesji, działania, awarii (Crash) i Technicals.</span><span class="sxs-lookup"><span data-stu-id="0dc90-110">The following steps are enough to activates the report of logs needed to compute all statistics regarding Users, Sessions, Activities, Crashes and Technicals.</span></span> <span data-ttu-id="0dc90-111">Raport dzienniki wymagane do obliczenia innych danych statystycznych, takich jak zdarzenia i błędy zadań musi zostać wykonane ręcznie przy użyciu interfejsu API usługi Engagement (zobacz [sposobu korzystania z zaawansowanych Mobile Engagement znakowanie interfejsu API w dla systemu Android](mobile-engagement-android-use-engagement-api.md) ponieważ te statystyki są aplikacji zależnej.</span><span class="sxs-lookup"><span data-stu-id="0dc90-111">The report of logs needed to compute other statistics like Events, Errors and Jobs must be done manually using the Engagement API (see [How to use the advanced Mobile Engagement tagging API in your Android](mobile-engagement-android-use-engagement-api.md) since these statistics are application dependent.</span></span>

## <a name="embed-the-engagement-sdk-and-service-into-your-android-project"></a><span data-ttu-id="0dc90-112">Osadź Engagement SDK i usługi do projektu systemu Android</span><span class="sxs-lookup"><span data-stu-id="0dc90-112">Embed the Engagement SDK and service into your Android project</span></span>
<span data-ttu-id="0dc90-113">Pobierz zestaw SDK systemu Android z [tutaj](https://aka.ms/vq9mfn) uzyskać `mobile-engagement-VERSION.jar` i umieść je w `libs` folderu projektu systemu Android (Utwórz folder biblioteki, jeśli jeszcze nie istnieje).</span><span class="sxs-lookup"><span data-stu-id="0dc90-113">Download the Android SDK from [here](https://aka.ms/vq9mfn) Get `mobile-engagement-VERSION.jar` and put them into the `libs` folder of your Android project (create the libs folder if it does not exist yet).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0dc90-114">W przypadku tworzenia pakietu aplikacji z narzędzia ProGuard, należy zachować niektóre klasy.</span><span class="sxs-lookup"><span data-stu-id="0dc90-114">If you build your application package with ProGuard, you need to keep some classes.</span></span> <span data-ttu-id="0dc90-115">Możesz użyć następującego fragmentu kodu konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="0dc90-115">You can use the following configuration snippet:</span></span>
> 
> <span data-ttu-id="0dc90-116">-zachować Klasa publiczna * rozszerza android.os.IInterface — Zachowaj {com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS — klasa</span><span class="sxs-lookup"><span data-stu-id="0dc90-116">-keep public class * extends android.os.IInterface -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {</span></span>
> 
> <span data-ttu-id="0dc90-117"><methods>; }</span><span class="sxs-lookup"><span data-stu-id="0dc90-117"><methods>; }</span></span>
> 
> 

<span data-ttu-id="0dc90-118">Określ ciąg połączenia zaangażowania przez wywołanie następującej metody w działaniu uruchamiania:</span><span class="sxs-lookup"><span data-stu-id="0dc90-118">Specify your Engagement connection string by calling the following method in the launcher activity:</span></span>

            EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
            engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
            EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="0dc90-119">Ciąg połączenia dla aplikacji jest wyświetlana w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="0dc90-119">The connection string for your application is displayed on Azure Portal.</span></span>

* <span data-ttu-id="0dc90-120">Jeśli brakuje, należy dodać następujące uprawnienia dla systemu Android (przed `<application>` tagu):</span><span class="sxs-lookup"><span data-stu-id="0dc90-120">If missing, add the following Android permissions (before the `<application>` tag):</span></span>
  
          <uses-permission android:name="android.permission.INTERNET"/>
          <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
* <span data-ttu-id="0dc90-121">Dodaj poniższą sekcję (między `<application>` i `</application>` tagów):</span><span class="sxs-lookup"><span data-stu-id="0dc90-121">Add the following section (between the `<application>` and `</application>` tags):</span></span>
  
          <service
            android:name="com.microsoft.azure.engagement.service.EngagementService"
            android:exported="false"
            android:label="<Your application name>Service"
            android:process=":Engagement"/>
* <span data-ttu-id="0dc90-122">Zmień `<Your application name>` według nazwy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0dc90-122">Change `<Your application name>` by the name of your application.</span></span>

> [!TIP]
> <span data-ttu-id="0dc90-123">`android:label` Atrybutu umożliwia wybór nazwy usługi Engagement, jak będzie wyświetlany użytkownikom końcowym na ekranie telefon "Uruchamianie usługi".</span><span class="sxs-lookup"><span data-stu-id="0dc90-123">The `android:label` attribute allows you to choose the name of the Engagement service as it will appear to the end-users in the "Running services" screen of their phone.</span></span> <span data-ttu-id="0dc90-124">Zalecane jest aby ustawić wartość tego atrybutu `"<Your application name>Service"` (np. `"AcmeFunGameService"`).</span><span class="sxs-lookup"><span data-stu-id="0dc90-124">It is recommended to set this attribute to `"<Your application name>Service"` (e.g. `"AcmeFunGameService"`).</span></span>
> 
> 

<span data-ttu-id="0dc90-125">Określanie `android:process` atrybutu zapewnia, że usługi Engagement będą uruchamiane w swoim własnym procesie (uruchamianie zaangażowania w ramach tego samego procesu, zgodnie z aplikacji spowoduje, że Twoje main/wątku interfejsu użytkownika będzie potencjalnie mniej dynamiczne).</span><span class="sxs-lookup"><span data-stu-id="0dc90-125">Specifying the `android:process` attribute ensures that the Engagement service will run in its own process (running Engagement in the same process as your application will make your main/UI thread potentially less responsive).</span></span>

> [!NOTE]
> <span data-ttu-id="0dc90-126">Kod umieszczony w `Application.onCreate()` i innych wywołań zwrotnych aplikacji zostanie uruchomione dla procesów wszystkich aplikacji, w tym usługi Engagement.</span><span class="sxs-lookup"><span data-stu-id="0dc90-126">Any code you place in `Application.onCreate()` and other application callbacks will be run for all your application's processes, including the Engagement service.</span></span> <span data-ttu-id="0dc90-127">Może mieć niepożądane skutki uboczne (takich jak przydziału pamięci niepotrzebnych i wątków w procesie stopnia zaangażowania, zduplikowany odbiorniki emisji lub usługi).</span><span class="sxs-lookup"><span data-stu-id="0dc90-127">It may have unwanted side effects (like unneeded memory allocations and threads in the Engagement's process, duplicate broadcast receivers or services).</span></span>
> 
> 

<span data-ttu-id="0dc90-128">Jeśli można zastąpić `Application.onCreate()`, zaleca się Dodaj poniższy fragment kodu na początku Twojej `Application.onCreate()` funkcji:</span><span class="sxs-lookup"><span data-stu-id="0dc90-128">If you override `Application.onCreate()`, it's recommended to add the following code snippet at the beginning of your `Application.onCreate()` function:</span></span>

             public void onCreate()
             {
               if (EngagementAgentUtils.isInDedicatedEngagementProcess(this))
                 return;

               ... Your code...
             }

<span data-ttu-id="0dc90-129">Tak samo postąpić w `Application.onTerminate()`, `Application.onLowMemory()` i `Application.onConfigurationChanged(...)`.</span><span class="sxs-lookup"><span data-stu-id="0dc90-129">You can do the same thing for `Application.onTerminate()`, `Application.onLowMemory()` and `Application.onConfigurationChanged(...)`.</span></span>

<span data-ttu-id="0dc90-130">Można rozszerzać `EngagementApplication` zamiast rozszerzanie `Application`: wywołanie zwrotne `Application.onCreate()` jest wyboru procesu i wywołania `Application.onApplicationProcessCreate()` tylko jeśli bieżący proces nie jest obsługującym usługę zaangażowania, te same zasady poprosić o innych wywołań zwrotnych.</span><span class="sxs-lookup"><span data-stu-id="0dc90-130">You can also extend `EngagementApplication` instead of extending `Application`: the callback `Application.onCreate()` does the process check and calls `Application.onApplicationProcessCreate()` only if the current process is not the one hosting the Engagement service, the same rules apply for the other callbacks.</span></span>

## <a name="basic-reporting"></a><span data-ttu-id="0dc90-131">Podstawowym raportowaniem</span><span class="sxs-lookup"><span data-stu-id="0dc90-131">Basic reporting</span></span>
### <a name="recommended-method-overload-your-activity-classes"></a><span data-ttu-id="0dc90-132">Zalecana metoda: przeciążenia sieci `Activity` klas</span><span class="sxs-lookup"><span data-stu-id="0dc90-132">Recommended method: overload your `Activity` classes</span></span>
<span data-ttu-id="0dc90-133">Aby aktywować raportu wszystkie dzienniki wymagane przez zaangażowania można obliczyć użytkowników, sesji, działania, awarii (Crash) i statystyki technicznych, po prostu należy wszystkie Twoje `*Activity` klasy podrzędne dziedziczą odpowiadającego `Engagement*Activity` klasy (np. Jeśli zwiększa działanie starszej wersji `ListActivity`, rozszerza upewnij `EngagementListActivity`).</span><span class="sxs-lookup"><span data-stu-id="0dc90-133">In order to activate the report of all the logs required by Engagement to compute Users, Sessions, Activities, Crashes and Technical statistics, you just have to make all your `*Activity` sub-classes inherit from the corresponding `Engagement*Activity` classes (e.g. if your legacy activity extends `ListActivity`, make it extends `EngagementListActivity`).</span></span>

<span data-ttu-id="0dc90-134">**Bez usługi Engagement:**</span><span class="sxs-lookup"><span data-stu-id="0dc90-134">**Without Engagement :**</span></span>

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

<span data-ttu-id="0dc90-135">**Z usługi Engagement:**</span><span class="sxs-lookup"><span data-stu-id="0dc90-135">**With Engagement :**</span></span>

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
> <span data-ttu-id="0dc90-136">Korzystając z `EngagementListActivity` lub `EngagementExpandableListActivity`, upewnij się, że wszelkie wywołanie `requestWindowFeature(...);` staje się przed wywołaniem do `super.onCreate(...);`, w przeciwnym razie wystąpi awaria.</span><span class="sxs-lookup"><span data-stu-id="0dc90-136">When using `EngagementListActivity` or `EngagementExpandableListActivity`, make sure any call to `requestWindowFeature(...);` is made before the call to `super.onCreate(...);`, otherwise a crash will occur.</span></span>
> 
> 

<span data-ttu-id="0dc90-137">Te klasy w można znaleźć `src` folderu i skopiować je do projektu.</span><span class="sxs-lookup"><span data-stu-id="0dc90-137">You can find these classes in the `src` folder, and can copy them into your project.</span></span> <span data-ttu-id="0dc90-138">Klasy są również w **JavaDoc**.</span><span class="sxs-lookup"><span data-stu-id="0dc90-138">The classes are also in the **JavaDoc**.</span></span>

### <a name="alternate-method-call-startactivity-and-endactivity-manually"></a><span data-ttu-id="0dc90-139">Alternatywna metoda: wywołanie `startActivity()` i `endActivity()` ręcznie</span><span class="sxs-lookup"><span data-stu-id="0dc90-139">Alternate method: call `startActivity()` and `endActivity()` manually</span></span>
<span data-ttu-id="0dc90-140">Jeśli nie możesz lub nie było przeciążyć Twojej `Activity` klas, można zamiast tego rozpoczęcia i zakończenia działań przez wywołanie metody `EngagementAgent`przez metody bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="0dc90-140">If you cannot or do not want to overload your `Activity` classes, you can instead start and end your activities by calling `EngagementAgent`'s methods directly.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0dc90-141">Zestaw SDK systemu Android nigdy nie wywołuje `endActivity()` metody, nawet wtedy, gdy aplikacja zostanie zamknięta (w systemie Android, aplikacje są faktycznie nigdy nie zamknięte).</span><span class="sxs-lookup"><span data-stu-id="0dc90-141">The Android SDK never calls the `endActivity()` method, even when the application is closed (on Android, applications are actually never closed).</span></span> <span data-ttu-id="0dc90-142">W związku z tym jest *wysokiej* zaleca, aby wywołać `startActivity()` metody w `onResume` wywołania zwrotnego z *wszystkie* działaniami i `endActivity()` metody w `onPause()` wywołania zwrotnego z *wszystkie* działań.</span><span class="sxs-lookup"><span data-stu-id="0dc90-142">Thus, it is *HIGHLY* recommended to call the `startActivity()` method in the `onResume` callback of *ALL* your activities, and the `endActivity()` method in the `onPause()` callback of *ALL* your activities.</span></span> <span data-ttu-id="0dc90-143">Jest to jedyny sposób należy upewnić się, że sesje nie zostaną ujawnione.</span><span class="sxs-lookup"><span data-stu-id="0dc90-143">This is the only way to be sure that sessions will not be leaked.</span></span> <span data-ttu-id="0dc90-144">Jeśli przeciek sesji usługi Engagement nigdy nie spowoduje rozłączenie z zapleczem usługi Engagement (ponieważ usługa połączono tak długo, jak długo trwa oczekiwanie na sesji).</span><span class="sxs-lookup"><span data-stu-id="0dc90-144">If a session is leaked, the Engagement service will never disconnect from the Engagement backend (since the service stays connected as long as a session is pending).</span></span>
> 
> 

<span data-ttu-id="0dc90-145">Oto przykład:</span><span class="sxs-lookup"><span data-stu-id="0dc90-145">Here is an example:</span></span>

            public class MyActivity extends Some3rdPartyActivity
            {
              @Override
              protected void onResume()
              {
                super.onResume();
                String activityNameOnEngagement = EngagementAgentUtils.buildEngagementActivityName(getClass()); // Uses short class name and removes "Activity" at the end.
                EngagementAgent.getInstance(this).startActivity(this, activityNameOnEngagement, null);
              }

              @Override
              protected void onPause()
              {
                super.onPause();
                EngagementAgent.getInstance(this).endActivity();
              }
            }

<span data-ttu-id="0dc90-146">W tym przykładzie są bardzo podobne do `EngagementActivity` klasy i jej wariantów, którego kod źródłowy jest udostępniany w `src` folderu.</span><span class="sxs-lookup"><span data-stu-id="0dc90-146">This example very similiar to the `EngagementActivity` class and its variants, whose source code is provided in the `src` folder.</span></span>

## <a name="test"></a><span data-ttu-id="0dc90-147">Testowanie</span><span class="sxs-lookup"><span data-stu-id="0dc90-147">Test</span></span>
<span data-ttu-id="0dc90-148">Teraz Sprawdź, czy integracją przez uruchomienie aplikacji mobilnej w emulator lub urządzenie i weryfikowanie rejestruje sesji na karcie Monitor.</span><span class="sxs-lookup"><span data-stu-id="0dc90-148">Now please verify your integration by running your mobile app in an emulator or device and verifying that it registers a session on the Monitor tab.</span></span>

<span data-ttu-id="0dc90-149">Następne sekcje są opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="0dc90-149">The next sections are optional.</span></span>

## <a name="location-reporting"></a><span data-ttu-id="0dc90-150">Raportowanie lokalizacji</span><span class="sxs-lookup"><span data-stu-id="0dc90-150">Location reporting</span></span>
<span data-ttu-id="0dc90-151">Jeśli chcesz lokalizacje, które mają być zgłaszane należy dodać kilka wierszy konfiguracji (między `<application>` i `</application>` tagów).</span><span class="sxs-lookup"><span data-stu-id="0dc90-151">If you want locations to be reported, you need to add a few lines of configuration (between the `<application>` and `</application>` tags).</span></span>

### <a name="lazy-area-location-reporting"></a><span data-ttu-id="0dc90-152">Raportowanie lokalizacji obszaru z opóźnieniem</span><span class="sxs-lookup"><span data-stu-id="0dc90-152">Lazy area location reporting</span></span>
<span data-ttu-id="0dc90-153">Umożliwia raportowanie lokalizacji obszaru z opóźnieniem zgłoszenia kraj, region i lokalizację skojarzone z urządzeniami.</span><span class="sxs-lookup"><span data-stu-id="0dc90-153">Lazy area location reporting allows to report the country, region and locality associated to devices.</span></span> <span data-ttu-id="0dc90-154">Raportowanie lokalizacji tego typu używa tylko lokalizacje sieciowe (na podstawie Identyfikatora komórki lub Wi-Fi).</span><span class="sxs-lookup"><span data-stu-id="0dc90-154">This type of location reporting only uses network locations (based on Cell ID or WIFI).</span></span> <span data-ttu-id="0dc90-155">Obszar urządzenia są zgłaszane co najwyżej raz na sesję.</span><span class="sxs-lookup"><span data-stu-id="0dc90-155">The device area is reported at most once per session.</span></span> <span data-ttu-id="0dc90-156">GPS nigdy nie jest używana, a w związku z tym ten typ lokalizacji raportu ma bardzo nieliczne (nie musi wypowiedzieć nie) wpływ na baterii.</span><span class="sxs-lookup"><span data-stu-id="0dc90-156">The GPS is never used, and thus this type of location report has very few (not to say no) impact on the battery.</span></span>

<span data-ttu-id="0dc90-157">Obszary zgłoszone są używane do obliczeniowe geograficzne statystyki dotyczące użytkowników, sesji, zdarzenia i błędy.</span><span class="sxs-lookup"><span data-stu-id="0dc90-157">Reported areas are used to compute geographic statistics about users, sessions, events and errors.</span></span> <span data-ttu-id="0dc90-158">Mogą one również używane jako kryterium w kampanie Zasięgowe.</span><span class="sxs-lookup"><span data-stu-id="0dc90-158">They can also be used as criterion in Reach campaigns.</span></span>

<span data-ttu-id="0dc90-159">Aby włączyć raportowanie lokalizacji obszaru z opóźnieniem, należy go za pomocą konfiguracji wymienione wcześniej w tej procedurze:</span><span class="sxs-lookup"><span data-stu-id="0dc90-159">To enable lazy area location reporting, you can do it by using the configuration previously mentioned in this procedure :</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setLazyAreaLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="0dc90-160">Należy również dodać następujące uprawnienia, jeśli brakuje:</span><span class="sxs-lookup"><span data-stu-id="0dc90-160">You also need to add the following permission if missing:</span></span>

            <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

<span data-ttu-id="0dc90-161">Lub możesz korzystać ``ACCESS_FINE_LOCATION`` Jeśli już używać w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0dc90-161">Or you can keep using ``ACCESS_FINE_LOCATION`` if you already use it in your application.</span></span>

### <a name="real-time-location-reporting"></a><span data-ttu-id="0dc90-162">Raportowanie lokalizacji w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="0dc90-162">Real time location reporting</span></span>
<span data-ttu-id="0dc90-163">Raportowanie lokalizacji w czasie rzeczywistym umożliwia zgłoszenia współrzędne geograficzne skojarzonego z urządzeń.</span><span class="sxs-lookup"><span data-stu-id="0dc90-163">Real time location reporting allows to report the latitude and longitude associated to devices.</span></span> <span data-ttu-id="0dc90-164">Domyślnie raportowanie lokalizacji tego typu używa tylko lokalizacje sieciowe (na podstawie Identyfikatora komórki lub Wi-Fi) i raportowania jest aktywne po uruchomieniu aplikacji na pierwszym planie (np. podczas sesji).</span><span class="sxs-lookup"><span data-stu-id="0dc90-164">By default, this type of location reporting only uses network locations (based on Cell ID or WIFI), and the reporting is only active when the application runs in foreground (i.e. during a session).</span></span>

<span data-ttu-id="0dc90-165">Lokalizacje w czasie rzeczywistym *nie* używany do obliczania statystyk.</span><span class="sxs-lookup"><span data-stu-id="0dc90-165">Real time locations are *NOT* used to compute statistics.</span></span> <span data-ttu-id="0dc90-166">Ich jedynym celem jest, aby zezwolić na użycie grodzenia czasu rzeczywistego \<Reach-odbiorców geofencing\> kryterium w kampanie Zasięgowe.</span><span class="sxs-lookup"><span data-stu-id="0dc90-166">Their only purpose is to allow the use of real time geo-fencing \<Reach-Audience-geofencing\> criterion in Reach campaigns.</span></span>

<span data-ttu-id="0dc90-167">Aby włączyć raportowanie miejsca w czasie rzeczywistym, należy go za pomocą konfiguracji wymienione wcześniej w tej procedurze:</span><span class="sxs-lookup"><span data-stu-id="0dc90-167">To enable real time location reporting, you can do it by using the configuration previously mentioned in this procedure :</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="0dc90-168">Należy również dodać następujące uprawnienia, jeśli brakuje:</span><span class="sxs-lookup"><span data-stu-id="0dc90-168">You also need to add the following permission if missing:</span></span>

            <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

<span data-ttu-id="0dc90-169">Lub możesz korzystać ``ACCESS_FINE_LOCATION`` Jeśli już używać w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0dc90-169">Or you can keep using ``ACCESS_FINE_LOCATION`` if you already use it in your application.</span></span>

#### <a name="gps-based-reporting"></a><span data-ttu-id="0dc90-170">GPS na podstawie raportowania</span><span class="sxs-lookup"><span data-stu-id="0dc90-170">GPS based reporting</span></span>
<span data-ttu-id="0dc90-171">Domyślnie raportowanie lokalizacji w czasie rzeczywistym używa tylko lokalizacje sieciowe.</span><span class="sxs-lookup"><span data-stu-id="0dc90-171">By default, real time location reporting only uses network based locations.</span></span> <span data-ttu-id="0dc90-172">Aby włączyć korzystanie z GPS na podstawie lokalizacji (które są znacznie bardziej precyzyjne), użyj obiektu konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="0dc90-172">To enable the use of GPS based locations (which are far more precise), use the configuration object:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setFineRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="0dc90-173">Należy również dodać następujące uprawnienia, jeśli brakuje:</span><span class="sxs-lookup"><span data-stu-id="0dc90-173">You also need to add the following permission if missing:</span></span>

            <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>

#### <a name="background-reporting"></a><span data-ttu-id="0dc90-174">Raportowanie w tle</span><span class="sxs-lookup"><span data-stu-id="0dc90-174">Background reporting</span></span>
<span data-ttu-id="0dc90-175">Domyślnie raportowanie lokalizacji w czasie rzeczywistym jest aktywne po uruchomieniu aplikacji na pierwszym planie (np. podczas sesji).</span><span class="sxs-lookup"><span data-stu-id="0dc90-175">By default, real time location reporting is only active when the application runs in foreground (i.e. during a session).</span></span> <span data-ttu-id="0dc90-176">Aby włączyć raportowanie również, w tle, użyj obiektu konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="0dc90-176">To enable the reporting also in background, use the configuration object:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setBackgroundRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

> [!NOTE]
> <span data-ttu-id="0dc90-177">Gdy aplikacja zostanie uruchomiona w tle, tylko do sieci na podstawie lokalizacji są raportowane, nawet jeśli włączono GPS.</span><span class="sxs-lookup"><span data-stu-id="0dc90-177">When the application runs in background, only network based locations are reported, even if you enabled the GPS.</span></span>
> 
> 

<span data-ttu-id="0dc90-178">Raport lokalizacji tła zostanie zatrzymana, jeśli użytkownik ponownym uruchomieniu urządzenia, można dodać, to aby stał się automatycznie uruchomiony ponownie w czasie rozruchu:</span><span class="sxs-lookup"><span data-stu-id="0dc90-178">The background location report will be stopped if the user reboots its device, you can add this to make it automatically restart at boot time:</span></span>

            <receiver android:name="com.microsoft.azure.engagement.EngagementLocationBootReceiver"
               android:exported="false">
               <intent-filter>
                  <action android:name="android.intent.action.BOOT_COMPLETED" />
               </intent-filter>
            </receiver>

<span data-ttu-id="0dc90-179">Należy również dodać następujące uprawnienia, jeśli brakuje:</span><span class="sxs-lookup"><span data-stu-id="0dc90-179">You also need to add the following permission if missing:</span></span>

            <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />

### <a name="android-m-permissions"></a><span data-ttu-id="0dc90-180">Android M uprawnień</span><span class="sxs-lookup"><span data-stu-id="0dc90-180">Android M permissions</span></span>
<span data-ttu-id="0dc90-181">Począwszy od systemu Android M, niektóre uprawnienia są zarządzane w czasie wykonywania i wymaga zatwierdzenia użytkownika.</span><span class="sxs-lookup"><span data-stu-id="0dc90-181">Starting with Android M, some permissions are managed at runtime and needs user approval.</span></span>

<span data-ttu-id="0dc90-182">Uprawnienia środowiska uruchomieniowego zostaną wyłączone domyślnie do nowych instalacji aplikacji, jeśli docelowy poziom interfejsu API systemu Android 23.</span><span class="sxs-lookup"><span data-stu-id="0dc90-182">The runtime permissions will be turned off by default for new app installations if you target Android API level 23.</span></span> <span data-ttu-id="0dc90-183">W przeciwnym razie ona zostanie włączona domyślnie.</span><span class="sxs-lookup"><span data-stu-id="0dc90-183">Otherwise it will be turned on by default.</span></span>

<span data-ttu-id="0dc90-184">Użytkownik może Włącz/wyłącz te uprawnienia z menu ustawień urządzenia.</span><span class="sxs-lookup"><span data-stu-id="0dc90-184">The user can enable/disable those permissions from the device settings menu.</span></span> <span data-ttu-id="0dc90-185">Wyłączenie uprawnień z menu systemowe kasuje procesów w tle aplikacji, jest zachowanie systemu które nie ma wpływu na możliwość odbierania wypychania w tle.</span><span class="sxs-lookup"><span data-stu-id="0dc90-185">Turning off permissions from system menu kills background processes of the application, this is a system behavior and has no impact on ability to receive push in background.</span></span>

<span data-ttu-id="0dc90-186">W kontekście usługi Mobile Engagement dostępne są następujące uprawnienia, które wymagają zatwierdzenia w czasie wykonywania:</span><span class="sxs-lookup"><span data-stu-id="0dc90-186">In the context of Mobile Engagement, the permissions that require approval at runtime are:</span></span>

* `ACCESS_COARSE_LOCATION`
* `ACCESS_FINE_LOCATION`
* <span data-ttu-id="0dc90-187">`WRITE_EXTERNAL_STORAGE`(tylko wtedy, gdy przeznaczonych dla interfejsu API systemu Android na poziomie 23 tej)</span><span class="sxs-lookup"><span data-stu-id="0dc90-187">`WRITE_EXTERNAL_STORAGE` (only when targeting Android API level 23 for this one)</span></span>

<span data-ttu-id="0dc90-188">Zewnętrzna pamięć masowa jest używany tylko dla funkcji szerszej Reach.</span><span class="sxs-lookup"><span data-stu-id="0dc90-188">The external storage is used only for Reach big picture feature.</span></span> <span data-ttu-id="0dc90-189">Jeśli okaże się, prosząc użytkowników o uprawnienie to można problem, można go usunąć Jeśli używane tylko w przypadku usługi Mobile Engagement, ale kosztem wyłączenie funkcji Duży obraz.</span><span class="sxs-lookup"><span data-stu-id="0dc90-189">If you find asking users this permission to be disruptive, you can remove it if you used it only for Mobile Engagement but at the cost of disabling big picture feature.</span></span>

<span data-ttu-id="0dc90-190">W przypadku funkcji lokalizacji należy zażądać uprawnień użytkownika za pomocą okna dialogowego w standardowym systemie.</span><span class="sxs-lookup"><span data-stu-id="0dc90-190">For the location features, you should request permissions to user using a standard system dialog.</span></span> <span data-ttu-id="0dc90-191">Jeśli użytkownik zaakceptuje, należy przekazać do ``EngagementAgent`` podjęcie zmiana pod uwagę w czasie rzeczywistym (w przeciwnym razie zmiany zostaną przetworzone przy następnym użytkownik uruchamia aplikację).</span><span class="sxs-lookup"><span data-stu-id="0dc90-191">If the user approves, you need to tell ``EngagementAgent`` to take that change into account in real time (otherwise the change will be processed the next time the user launches the application).</span></span>

<span data-ttu-id="0dc90-192">Oto przykład kodu do użycia w działaniu aplikacji, aby zażądać uprawnień i przekazuje wynik w przypadku wartości dodatniej do ``EngagementAgent``:</span><span class="sxs-lookup"><span data-stu-id="0dc90-192">Here is a code sample to use in an activity of your application to request permissions and forward the result if positive to ``EngagementAgent``:</span></span>

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
         * Request location permission, but this won't explain why it is needed to the user.
         * The standard Android documentation explains with more details how to display a rationale activity to explain the user why the permission is needed in your application.
         * Putting COARSE vs FINE has no impact here, they are part of the same group for runtime permission management.
         */
        if (checkSelfPermission(android.Manifest.permission.ACCESS_FINE_LOCATION) != PackageManager.PERMISSION_GRANTED)
          requestPermissions(new String[] { android.Manifest.permission.ACCESS_FINE_LOCATION }, 0);

        /* Only if you want to keep features using external storage */
        if (checkSelfPermission(android.Manifest.permission.WRITE_EXTERNAL_STORAGE) != PackageManager.PERMISSION_GRANTED)
          requestPermissions(new String[] { android.Manifest.permission.WRITE_EXTERNAL_STORAGE }, 1);
      }
    }

    @Override
    public void onRequestPermissionsResult(int requestCode, String[] permissions, int[] grantResults)
    {
      /* Only a positive location permission update requires engagement agent refresh, hence the request code matching from above function */
      if (requestCode == 0 && grantResults[0] == PackageManager.PERMISSION_GRANTED)
        getEngagementAgent().refreshPermissions();
    }

## <a name="advanced-reporting"></a><span data-ttu-id="0dc90-193">Zaawansowane raportowanie</span><span class="sxs-lookup"><span data-stu-id="0dc90-193">Advanced reporting</span></span>
<span data-ttu-id="0dc90-194">Opcjonalnie, jeśli chcesz zgłosić aplikacji określonych zdarzeń, błędów i zadań, należy użyć interfejsu API usługi Engagement za pomocą metody `EngagementAgent` klasy.</span><span class="sxs-lookup"><span data-stu-id="0dc90-194">Optionally, if you want to report application specific events, errors and jobs, you need to use the Engagement API through the methods of the `EngagementAgent` class.</span></span> <span data-ttu-id="0dc90-195">Obiekt tej klasy może być pobranych przez wywołanie metody `EngagementAgent.getInstance()` metody statycznej.</span><span class="sxs-lookup"><span data-stu-id="0dc90-195">An object of this class can be retreived by calling the `EngagementAgent.getInstance()` static method.</span></span>

<span data-ttu-id="0dc90-196">Interfejsu API usługi Engagement pozwala korzystać ze wszystkich zaawansowanych możliwości usługi Engagement i została szczegółowo opisana w sposób używania interfejsu API programu zaangażowania w systemie Android (jak również w dokumentacji technicznej `EngagementAgent` klasy).</span><span class="sxs-lookup"><span data-stu-id="0dc90-196">The Engagement API allows to use all of Engagement's advanced capabilities and is detailed in the How to Use the Engagement API on Android (as well as in the technical documentation of the `EngagementAgent` class).</span></span>

## <a name="advanced-configuration-in-androidmanifestxml"></a><span data-ttu-id="0dc90-197">Konfiguracja zaawansowana (w pliku AndroidManifest.xml)</span><span class="sxs-lookup"><span data-stu-id="0dc90-197">Advanced configuration (in AndroidManifest.xml)</span></span>
### <a name="wake-locks"></a><span data-ttu-id="0dc90-198">Wznawianie pracy blokad</span><span class="sxs-lookup"><span data-stu-id="0dc90-198">Wake locks</span></span>
<span data-ttu-id="0dc90-199">Należy upewnić się, że dane statystyczne są wysyłane w czasie rzeczywistym za pomocą sieci Wi-Fi lub ekranu jest wyłączona, należy dodać następujące uprawnienia opcjonalne:</span><span class="sxs-lookup"><span data-stu-id="0dc90-199">If you want to be sure that statistics are sent in real time when using Wifi or when the screen is off, add the following optional permission:</span></span>

            <uses-permission android:name="android.permission.WAKE_LOCK"/>

### <a name="crash-report"></a><span data-ttu-id="0dc90-200">Raport o awarii</span><span class="sxs-lookup"><span data-stu-id="0dc90-200">Crash report</span></span>
<span data-ttu-id="0dc90-201">Jeśli chcesz wyłączyć raporty awarii, dodaj ją (między `<application>` i `</application>` tagów):</span><span class="sxs-lookup"><span data-stu-id="0dc90-201">If you want to disable crash reports, add this (between the `<application>` and `</application>` tags):</span></span>

            <meta-data android:name="engagement:reportCrash" android:value="false"/>

### <a name="burst-threshold"></a><span data-ttu-id="0dc90-202">Próg serii</span><span class="sxs-lookup"><span data-stu-id="0dc90-202">Burst threshold</span></span>
<span data-ttu-id="0dc90-203">Domyślnie raporty usługi Engagement rejestruje się w czasie rzeczywistym.</span><span class="sxs-lookup"><span data-stu-id="0dc90-203">By default, the Engagement service reports logs in real time.</span></span> <span data-ttu-id="0dc90-204">Jeśli aplikacja zgłasza dzienniki bardzo często, lepiej jest buforu dzienniki i raportuj je w całości na regularne podstawy czasu (jest to nazywane "tryb serii").</span><span class="sxs-lookup"><span data-stu-id="0dc90-204">If your application reports logs very frequently, it is better to buffer the logs and to report them all at once on a regular time base (this is called the "burst mode").</span></span> <span data-ttu-id="0dc90-205">Aby to zrobić, Dodaj (między `<application>` i `</application>` tagów):</span><span class="sxs-lookup"><span data-stu-id="0dc90-205">To do so, add this (between the `<application>` and `</application>` tags):</span></span>

            <meta-data android:name="engagement:burstThreshold" android:value="{interval between too bursts (in milliseconds)}"/>

<span data-ttu-id="0dc90-206">Tryb serii nieco zwiększyć czas pracy baterii, ale ma wpływ na monitorowanie usługi Engagement: wszystkie czas trwania sesji i zadania zostanie zaokrąglony próg serii (w związku z tym sesji i zadania krótsze niż próg serii może nie być widoczna).</span><span class="sxs-lookup"><span data-stu-id="0dc90-206">The burst mode slightly increase the battery life but has an impact on the Engagement Monitor: all sessions and jobs duration will be rounded to the burst threshold (thus, sessions and jobs shorter than the burst threshold may not be visible).</span></span> <span data-ttu-id="0dc90-207">Zaleca się przy użyciu progu w serii się niż 30000 (30s).</span><span class="sxs-lookup"><span data-stu-id="0dc90-207">It is recommended to use a burst threshold no longer than 30000 (30s).</span></span>

### <a name="session-timeout"></a><span data-ttu-id="0dc90-208">Limit czasu sesji</span><span class="sxs-lookup"><span data-stu-id="0dc90-208">Session timeout</span></span>
<span data-ttu-id="0dc90-209">Domyślnie sesja jest 10s zakończone po zakończeniu jego ostatniej aktywności (która zazwyczaj występuje po naciśnięciu klawisza Home lub Wstecz, przez ustawienie bezczynności telefonu lub przejście do innej aplikacji).</span><span class="sxs-lookup"><span data-stu-id="0dc90-209">By default, a session is ended 10s after the end of its last activity (which usually occurs by pressing the Home or Back key, by setting the phone idle or by jumping into another application).</span></span> <span data-ttu-id="0dc90-210">Pozwoli to uniknąć podziału sesji każdy czas zakończenia użytkownika i bardzo szybko powrócić do aplikacji (które mogą wystąpić podczas odebrania on obrazu, sprawdź powiadomienia itp.).</span><span class="sxs-lookup"><span data-stu-id="0dc90-210">This is to avoid a session split each time the user exit and return to the application very quickly (which can happen when he pick up a image, check a notification, etc.).</span></span> <span data-ttu-id="0dc90-211">Można modyfikować tego parametru.</span><span class="sxs-lookup"><span data-stu-id="0dc90-211">You may want to modify this parameter.</span></span> <span data-ttu-id="0dc90-212">Aby to zrobić, Dodaj (między `<application>` i `</application>` tagów):</span><span class="sxs-lookup"><span data-stu-id="0dc90-212">To do so, add this (between the `<application>` and `</application>` tags):</span></span>

            <meta-data android:name="engagement:sessionTimeout" android:value="{session timeout (in milliseconds)}"/>

## <a name="disable-log-reporting"></a><span data-ttu-id="0dc90-213">Wyłączanie dziennika raportowania</span><span class="sxs-lookup"><span data-stu-id="0dc90-213">Disable log reporting</span></span>
### <a name="using-a-method-call"></a><span data-ttu-id="0dc90-214">Przy użyciu wywołania metody</span><span class="sxs-lookup"><span data-stu-id="0dc90-214">Using a method call</span></span>
<span data-ttu-id="0dc90-215">Jeśli chcesz zaangażowania, aby zatrzymać wysyłanie dzienników można wywołać:</span><span class="sxs-lookup"><span data-stu-id="0dc90-215">If you want Engagement to stop sending logs, you can call:</span></span>

            EngagementAgent.getInstance(context).setEnabled(false);

<span data-ttu-id="0dc90-216">To wywołanie jest trwały: używa plików udostępnionych preferencji.</span><span class="sxs-lookup"><span data-stu-id="0dc90-216">This call is persistent: it uses a shared preferences file.</span></span>

<span data-ttu-id="0dc90-217">Jeśli zaangażowania jest aktywny, gdy wywołanie tej funkcji, może potrwać minutę do zatrzymania usługi.</span><span class="sxs-lookup"><span data-stu-id="0dc90-217">If Engagement is active when you call this function, it may take 1 minute for the service to stop.</span></span> <span data-ttu-id="0dc90-218">Jednak go nie Uruchom usługę na wszystkich przy następnym uruchomieniu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0dc90-218">However it won't launch the service at all the next time you launch the application.</span></span>

<span data-ttu-id="0dc90-219">Możesz włączyć ponownie raportowania przez wywołanie tej samej funkcji z dziennika `true`.</span><span class="sxs-lookup"><span data-stu-id="0dc90-219">You can enable log reporting again by calling the same function with `true`.</span></span>

### <a name="integration-in-your-own-preferenceactivity"></a><span data-ttu-id="0dc90-220">Integracja z własną`PreferenceActivity`</span><span class="sxs-lookup"><span data-stu-id="0dc90-220">Integration in your own `PreferenceActivity`</span></span>
<span data-ttu-id="0dc90-221">Zamiast wywoływania tej funkcji, to ustawienie można również zintegrować bezpośrednio w istniejącą `PreferenceActivity`.</span><span class="sxs-lookup"><span data-stu-id="0dc90-221">Instead of calling this function, you can also integrate this setting directly in your existing `PreferenceActivity`.</span></span>

<span data-ttu-id="0dc90-222">Zaangażowania, aby użyć pliku preferencji (z odpowiednią tryb) można skonfigurować w `AndroidManifest.xml` pliku z `application meta-data`:</span><span class="sxs-lookup"><span data-stu-id="0dc90-222">You can configure Engagement to use your preferences file (with the desired mode) in the `AndroidManifest.xml` file with `application meta-data`:</span></span>

* <span data-ttu-id="0dc90-223">`engagement:agent:settings:name` Klucz służy do definiowania nazwę pliku udostępnionych preferencji.</span><span class="sxs-lookup"><span data-stu-id="0dc90-223">The `engagement:agent:settings:name` key is used to define the name of the shared preferences file.</span></span>
* <span data-ttu-id="0dc90-224">`engagement:agent:settings:mode` Klucz służy do definiowania trybu plików udostępnionych preferencji, należy użyć tego samego trybu jako w Twojej `PreferenceActivity`.</span><span class="sxs-lookup"><span data-stu-id="0dc90-224">The `engagement:agent:settings:mode` key is used to define the mode of the shared preferences file, you should use the same mode as in your `PreferenceActivity`.</span></span> <span data-ttu-id="0dc90-225">Tryb muszą być przekazywane w postaci liczby: Jeśli korzystasz z kombinacją flag stałej w kodzie, sprawdź wartość całkowita.</span><span class="sxs-lookup"><span data-stu-id="0dc90-225">The mode must be passed as a number: if you are using a combination of constant flags in your code, check the total value.</span></span>

<span data-ttu-id="0dc90-226">Użyj zaangażowania zawsze `engagement:key` logiczna klucz w pliku preferencji zarządzania to ustawienie.</span><span class="sxs-lookup"><span data-stu-id="0dc90-226">Engagement always use the `engagement:key` boolean key within the preferences file for managing this setting.</span></span>

<span data-ttu-id="0dc90-227">Poniższy przykład przedstawia `AndroidManifest.xml` przedstawiono wartości domyślne:</span><span class="sxs-lookup"><span data-stu-id="0dc90-227">The following example of `AndroidManifest.xml` shows the default values:</span></span>

            <application>
                [...]
                <meta-data
                  android:name="engagement:agent:settings:name"
                  android:value="engagement.agent" />
                <meta-data
                  android:name="engagement:agent:settings:mode"
                  android:value="0" />

<span data-ttu-id="0dc90-228">Następnie można dodać `CheckBoxPreference` w układzie preferencji podobny do następującego:</span><span class="sxs-lookup"><span data-stu-id="0dc90-228">Then you can add a `CheckBoxPreference` in your preference layout like the following one:</span></span>

            <CheckBoxPreference
              android:key="engagement:enabled"
              android:defaultValue="true"
              android:title="Use Engagement"
              android:summaryOn="Engagement is enabled."
              android:summaryOff="Engagement is disabled." />

<!-- URLs. -->
[Device API]: http://go.microsoft.com/?linkid=9876094
