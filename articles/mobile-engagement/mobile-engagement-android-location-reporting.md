---
title: aaaLocation raportowanie dla zestawem Azure Mobile Engagement Android SDK
description: "Opisuje sposób lokalizacji tooconfigure raportowanie dla zestawem Azure Mobile Engagement Android SDK"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 6cab5ed1-b767-46ac-9f0b-48a4e249d88c
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/12/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: c2cb097df2a77bee2d56ffe9509dc116548db408
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="location-reporting-for-azure-mobile-engagement-android-sdk"></a><span data-ttu-id="b40e2-103">Lokalizacja raportowania dla usługi Azure Mobile Engagement Android SDK</span><span class="sxs-lookup"><span data-stu-id="b40e2-103">Location Reporting for Azure Mobile Engagement Android SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b40e2-104">Android</span><span class="sxs-lookup"><span data-stu-id="b40e2-104">Android</span></span>](mobile-engagement-android-integrate-engagement.md)
> 
> 

<span data-ttu-id="b40e2-105">W tym temacie opisano sposób lokalizacji toodo raportowania dla aplikacji systemu Android.</span><span class="sxs-lookup"><span data-stu-id="b40e2-105">This topic describes how toodo location reporting for your Android application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b40e2-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="b40e2-106">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

## <a name="location-reporting"></a><span data-ttu-id="b40e2-107">Raportowanie lokalizacji</span><span class="sxs-lookup"><span data-stu-id="b40e2-107">Location reporting</span></span>
<span data-ttu-id="b40e2-108">Jeśli chcesz toobe lokalizacji zgłoszone, należy tooadd kilka wierszy konfiguracji (między hello `<application>` i `</application>` tagów).</span><span class="sxs-lookup"><span data-stu-id="b40e2-108">If you want locations toobe reported, you need tooadd a few lines of configuration (between hello `<application>` and `</application>` tags).</span></span>

### <a name="lazy-area-location-reporting"></a><span data-ttu-id="b40e2-109">Raportowanie lokalizacji obszaru z opóźnieniem</span><span class="sxs-lookup"><span data-stu-id="b40e2-109">Lazy area location reporting</span></span>
<span data-ttu-id="b40e2-110">Raportowanie lokalizacji obszaru z opóźnieniem umożliwia raportowania hello kraju, regionu i lokalizacji, skojarzone z urządzeń.</span><span class="sxs-lookup"><span data-stu-id="b40e2-110">Lazy area location reporting enables reporting hello country, region, and locality associated with devices.</span></span> <span data-ttu-id="b40e2-111">Raportowanie lokalizacji tego typu używa tylko lokalizacje sieciowe (na podstawie Identyfikatora komórki lub Wi-Fi).</span><span class="sxs-lookup"><span data-stu-id="b40e2-111">This type of location reporting only uses network locations (based on Cell ID or WIFI).</span></span> <span data-ttu-id="b40e2-112">obszar urządzenia Hello jest zgłaszana co najwyżej raz na sesję.</span><span class="sxs-lookup"><span data-stu-id="b40e2-112">hello device area is reported at most once per session.</span></span> <span data-ttu-id="b40e2-113">Hello GPS nigdy nie jest używany, a w związku z tym tego typu lokalizacji raportu ma niski wpływ na powitania baterii.</span><span class="sxs-lookup"><span data-stu-id="b40e2-113">hello GPS is never used, and thus this type of location report has low impact on hello battery.</span></span>

<span data-ttu-id="b40e2-114">Obszary zgłoszone są używane toocompute geograficzne statystyki dotyczące użytkowników, sesji zdarzenia i błędy.</span><span class="sxs-lookup"><span data-stu-id="b40e2-114">Reported areas are used toocompute geographic statistics about users, sessions, events, and errors.</span></span> <span data-ttu-id="b40e2-115">Mogą one również używane jako kryterium w kampanie Zasięgowe.</span><span class="sxs-lookup"><span data-stu-id="b40e2-115">They can also be used as criterion in Reach campaigns.</span></span>

<span data-ttu-id="b40e2-116">Możesz włączyć lokalizacji obszaru z opóźnieniem raportowania przy użyciu konfiguracji hello wymienione wcześniej w tej procedurze:</span><span class="sxs-lookup"><span data-stu-id="b40e2-116">You enable lazy area location reporting by using hello configuration previously mentioned in this procedure:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setLazyAreaLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="b40e2-117">Należy również toospecify uprawnienia lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="b40e2-117">You also need toospecify a location permission.</span></span> <span data-ttu-id="b40e2-118">Ten kod zawiera ``COARSE`` uprawnienia:</span><span class="sxs-lookup"><span data-stu-id="b40e2-118">This code uses ``COARSE`` permission:</span></span>

    <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

<span data-ttu-id="b40e2-119">Jeśli aplikacja wymaga, możesz użyć ``ACCESS_FINE_LOCATION`` zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="b40e2-119">If your app requires it, you can use ``ACCESS_FINE_LOCATION`` instead.</span></span>

### <a name="real-time-location-reporting"></a><span data-ttu-id="b40e2-120">Raportowanie lokalizacji w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="b40e2-120">Real-time location reporting</span></span>
<span data-ttu-id="b40e2-121">Raportowanie lokalizacji w czasie rzeczywistym umożliwia raportowania hello współrzędne geograficzne., skojarzone z urządzeń.</span><span class="sxs-lookup"><span data-stu-id="b40e2-121">Real-time location reporting enables reporting hello latitude and longitude associated with devices.</span></span> <span data-ttu-id="b40e2-122">Domyślnie raportowanie lokalizacji tego typu używa tylko lokalizacje sieciowe, na podstawie Identyfikatora komórki lub Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="b40e2-122">By default, this type of location reporting only uses network locations, based on Cell ID or WIFI.</span></span> <span data-ttu-id="b40e2-123">Raportowanie Hello jest aktywne, gdy aplikacja hello działa na pierwszym planie (na przykład podczas sesji).</span><span class="sxs-lookup"><span data-stu-id="b40e2-123">hello reporting is only active when hello application runs in foreground (for example, during a session).</span></span>

<span data-ttu-id="b40e2-124">W czasie rzeczywistym lokalizacje są *nie* używane toocompute statystyk.</span><span class="sxs-lookup"><span data-stu-id="b40e2-124">Real-time locations are *NOT* used toocompute statistics.</span></span> <span data-ttu-id="b40e2-125">Ich jedynym celem jest użycie hello tooallow grodzenia w czasie rzeczywistym \<Reach-odbiorców geofencing\> kryterium w kampanie Zasięgowe.</span><span class="sxs-lookup"><span data-stu-id="b40e2-125">Their only purpose is tooallow hello use of real-time geo-fencing \<Reach-Audience-geofencing\> criterion in Reach campaigns.</span></span>

<span data-ttu-id="b40e2-126">tooenable lokalizacji w czasie rzeczywistym, raportowanie, Dodaj wiersz z toowhere kodu ustawić parametry połączenia zaangażowania hello hello uruchamiania działania.</span><span class="sxs-lookup"><span data-stu-id="b40e2-126">tooenable real-time location reporting, add a line of code toowhere you set hello Engagement connection string in hello launcher activity.</span></span> <span data-ttu-id="b40e2-127">wynik Hello wygląda hello:</span><span class="sxs-lookup"><span data-stu-id="b40e2-127">hello result looks like hello following:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

        You also need toospecify a location permission. This code uses ``COARSE`` permission:

            <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

        If your app requires it, you can use ``ACCESS_FINE_LOCATION`` instead.

#### <a name="gps-based-reporting"></a><span data-ttu-id="b40e2-128">GPS na podstawie raportowania</span><span class="sxs-lookup"><span data-stu-id="b40e2-128">GPS based reporting</span></span>
<span data-ttu-id="b40e2-129">Domyślnie raportowanie lokalizacji w czasie rzeczywistym używa tylko lokalizacje sieciowe.</span><span class="sxs-lookup"><span data-stu-id="b40e2-129">By default, real-time location reporting only uses network-based locations.</span></span> <span data-ttu-id="b40e2-130">Użyj hello tooenable GPS na podstawie lokalizacji, które są znacznie bardziej dokładne, użyj obiektu konfiguracji hello:</span><span class="sxs-lookup"><span data-stu-id="b40e2-130">tooenable hello use of GPS-based locations, which are far more precise, use hello configuration object:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setFineRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="b40e2-131">Należy również następujące uprawnienia, jeśli brakuje hello tooadd:</span><span class="sxs-lookup"><span data-stu-id="b40e2-131">You also need tooadd hello following permission if missing:</span></span>

    <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>

#### <a name="background-reporting"></a><span data-ttu-id="b40e2-132">Raportowanie w tle</span><span class="sxs-lookup"><span data-stu-id="b40e2-132">Background reporting</span></span>
<span data-ttu-id="b40e2-133">Domyślnie raportowanie lokalizacji w czasie rzeczywistym jest aktywne uruchomienie aplikacji hello na pierwszym planie (na przykład podczas sesji).</span><span class="sxs-lookup"><span data-stu-id="b40e2-133">By default, real-time location reporting is only active when hello application runs in foreground (for example, during a session).</span></span> <span data-ttu-id="b40e2-134">Witaj tooenable także raportowanie w tle, należy użyć tego obiektu konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="b40e2-134">tooenable hello reporting also in background, use this configuration object:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setBackgroundRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

> [!NOTE]
> <span data-ttu-id="b40e2-135">Po uruchomieniu aplikacji hello w tle, tylko lokalizacje sieciowe są raportowane, nawet jeśli włączono hello GPS.</span><span class="sxs-lookup"><span data-stu-id="b40e2-135">When hello application runs in background, only network-based locations are reported, even if you enabled hello GPS.</span></span>
> 
> 

<span data-ttu-id="b40e2-136">Jeśli użytkownik hello ponownego uruchamiania urządzenia, hello tła lokalizacji raportu została zatrzymana.</span><span class="sxs-lookup"><span data-stu-id="b40e2-136">If hello user reboots their device, hello background location report is stopped.</span></span> <span data-ttu-id="b40e2-137">toomake automatycznie uruchomiony ponownie w czasie rozruchu, Dodaj ten kod.</span><span class="sxs-lookup"><span data-stu-id="b40e2-137">toomake it automatically restart at boot time, add this code.</span></span>

    <receiver android:name="com.microsoft.azure.engagement.EngagementLocationBootReceiver"
           android:exported="false">
        <intent-filter>
            <action android:name="android.intent.action.BOOT_COMPLETED" />
        </intent-filter>
    </receiver>

<span data-ttu-id="b40e2-138">Należy również następujące uprawnienia, jeśli brakuje hello tooadd:</span><span class="sxs-lookup"><span data-stu-id="b40e2-138">You also need tooadd hello following permission if missing:</span></span>

    <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />

## <a name="android-m-permissions"></a><span data-ttu-id="b40e2-139">Android M uprawnień</span><span class="sxs-lookup"><span data-stu-id="b40e2-139">Android M permissions</span></span>
<span data-ttu-id="b40e2-140">Począwszy od systemu Android M, niektóre uprawnienia są zarządzane w czasie wykonywania i wymagają zatwierdzenia użytkownika.</span><span class="sxs-lookup"><span data-stu-id="b40e2-140">Starting with Android M, some permissions are managed at runtime and need user approval.</span></span>

<span data-ttu-id="b40e2-141">Interfejs API systemu Android na poziomie 23 w przypadku skierowania, hello środowiska uruchomieniowego uprawnienia są domyślnie wyłączona dla nowych instalacji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b40e2-141">If you target Android API level 23, hello runtime permissions are turned off by default for new app installations.</span></span> <span data-ttu-id="b40e2-142">W przeciwnym razie są włączone domyślnie.</span><span class="sxs-lookup"><span data-stu-id="b40e2-142">Otherwise they are turned on by default.</span></span>

<span data-ttu-id="b40e2-143">Użytkownik może Włącz/wyłącz te uprawnienia z menu ustawień urządzenia hello.</span><span class="sxs-lookup"><span data-stu-id="b40e2-143">You can enable/disable those permissions from hello device settings menu.</span></span> <span data-ttu-id="b40e2-144">Wyłączenie uprawnień z menu systemowe hello kasuje procesów w tle hello aplikacji hello, który jest zachowanie systemowe i nie ma wpływu na możliwość tooreceive wypychania w tle.</span><span class="sxs-lookup"><span data-stu-id="b40e2-144">Turning off permissions from hello system menu kills hello background processes of hello application, which is a system behavior, and has no impact on ability tooreceive push in background.</span></span>

<span data-ttu-id="b40e2-145">W kontekście hello lokalizacji usługi Mobile Engagement raportowania są hello uprawnienia, które wymagają zatwierdzenia w czasie wykonywania:</span><span class="sxs-lookup"><span data-stu-id="b40e2-145">In hello context of Mobile Engagement location reporting, hello permissions that require approval at runtime are:</span></span>

* `ACCESS_COARSE_LOCATION`
* `ACCESS_FINE_LOCATION`

<span data-ttu-id="b40e2-146">Zażądaj uprawnień od użytkownika hello przy użyciu okna dialogowego standardowy system.</span><span class="sxs-lookup"><span data-stu-id="b40e2-146">Request permissions from hello user using a standard system dialog.</span></span> <span data-ttu-id="b40e2-147">Jeśli użytkownik hello zatwierdza, poinformuj ``EngagementAgent`` tootake, która zmienia pod uwagę w czasie rzeczywistym.</span><span class="sxs-lookup"><span data-stu-id="b40e2-147">If hello user approves, tell ``EngagementAgent`` tootake that change into account in real-time.</span></span> <span data-ttu-id="b40e2-148">W przeciwnym razie zmiany hello jest przetworzonych hello dalej hello użytkownika powoduje uruchomienie hello aplikacji w czasie.</span><span class="sxs-lookup"><span data-stu-id="b40e2-148">Otherwise hello change is processed hello next time hello user launches hello application.</span></span>

<span data-ttu-id="b40e2-149">Oto toouse przykładowy kod w działaniu aplikacji toorequest uprawnienia i do przodu hello wynik Jeśli dodatnią zbyt``EngagementAgent``:</span><span class="sxs-lookup"><span data-stu-id="b40e2-149">Here is a code sample toouse in an activity of your application toorequest permissions and forward hello result if positive too``EngagementAgent``:</span></span>

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
         * Request location permission, but this doesn't explain why it is needed toohello user.
         * hello standard Android documentation explains with more details how toodisplay a rationale activity tooexplain hello user why hello permission is needed in your application.
         * Putting COARSE vs FINE has no impact here, they are part of hello same group for runtime permission management.
         */
        if (checkSelfPermission(android.Manifest.permission.ACCESS_FINE_LOCATION) != PackageManager.PERMISSION_GRANTED)
          requestPermissions(new String[] { android.Manifest.permission.ACCESS_FINE_LOCATION }, 0);

      }
    }

    @Override
    public void onRequestPermissionsResult(int requestCode, String[] permissions, int[] grantResults)
    {
      /* Only a positive location permission update requires engagement agent refresh, hence hello request code matching from above function */
      if (requestCode == 0 && grantResults[0] == PackageManager.PERMISSION_GRANTED)
        getEngagementAgent().refreshPermissions();
    }
