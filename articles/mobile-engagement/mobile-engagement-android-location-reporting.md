---
title: "Lokalizacja raportowania dla usługi Azure Mobile Engagement Android SDK"
description: "Opisuje sposób konfigurowania lokalizacji raportowanie dla zestawem Azure Mobile Engagement Android SDK"
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
ms.openlocfilehash: 777d5719cce505b55dfb61c91dcac7e713b077a9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="location-reporting-for-azure-mobile-engagement-android-sdk"></a><span data-ttu-id="94f87-103">Lokalizacja raportowania dla usługi Azure Mobile Engagement Android SDK</span><span class="sxs-lookup"><span data-stu-id="94f87-103">Location Reporting for Azure Mobile Engagement Android SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="94f87-104">Android</span><span class="sxs-lookup"><span data-stu-id="94f87-104">Android</span></span>](mobile-engagement-android-integrate-engagement.md)
> 
> 

<span data-ttu-id="94f87-105">W tym temacie opisano sposób wykonywania lokalizacji raportowanie dla aplikacji systemu Android.</span><span class="sxs-lookup"><span data-stu-id="94f87-105">This topic describes how to do location reporting for your Android application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="94f87-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="94f87-106">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

## <a name="location-reporting"></a><span data-ttu-id="94f87-107">Raportowanie lokalizacji</span><span class="sxs-lookup"><span data-stu-id="94f87-107">Location reporting</span></span>
<span data-ttu-id="94f87-108">Jeśli chcesz lokalizacje, które mają być zgłaszane należy dodać kilka wierszy konfiguracji (między `<application>` i `</application>` tagów).</span><span class="sxs-lookup"><span data-stu-id="94f87-108">If you want locations to be reported, you need to add a few lines of configuration (between the `<application>` and `</application>` tags).</span></span>

### <a name="lazy-area-location-reporting"></a><span data-ttu-id="94f87-109">Raportowanie lokalizacji obszaru z opóźnieniem</span><span class="sxs-lookup"><span data-stu-id="94f87-109">Lazy area location reporting</span></span>
<span data-ttu-id="94f87-110">Raportowanie lokalizacji obszaru z opóźnieniem umożliwia raportowanie kraju, region i lokalizację skojarzone z urządzeń.</span><span class="sxs-lookup"><span data-stu-id="94f87-110">Lazy area location reporting enables reporting the country, region, and locality associated with devices.</span></span> <span data-ttu-id="94f87-111">Raportowanie lokalizacji tego typu używa tylko lokalizacje sieciowe (na podstawie Identyfikatora komórki lub Wi-Fi).</span><span class="sxs-lookup"><span data-stu-id="94f87-111">This type of location reporting only uses network locations (based on Cell ID or WIFI).</span></span> <span data-ttu-id="94f87-112">Obszar urządzenia są zgłaszane co najwyżej raz na sesję.</span><span class="sxs-lookup"><span data-stu-id="94f87-112">The device area is reported at most once per session.</span></span> <span data-ttu-id="94f87-113">GPS nigdy nie jest używany, a w związku z tym tego typu lokalizacji raportu ma niski wpływ na baterii.</span><span class="sxs-lookup"><span data-stu-id="94f87-113">The GPS is never used, and thus this type of location report has low impact on the battery.</span></span>

<span data-ttu-id="94f87-114">Obszary zgłoszone są używane do obliczeniowe geograficzne statystyki dotyczące użytkowników, sesji zdarzenia i błędy.</span><span class="sxs-lookup"><span data-stu-id="94f87-114">Reported areas are used to compute geographic statistics about users, sessions, events, and errors.</span></span> <span data-ttu-id="94f87-115">Mogą one również używane jako kryterium w kampanie Zasięgowe.</span><span class="sxs-lookup"><span data-stu-id="94f87-115">They can also be used as criterion in Reach campaigns.</span></span>

<span data-ttu-id="94f87-116">Możesz włączyć lokalizacji obszaru z opóźnieniem raportowania przy użyciu konfiguracji wymienione wcześniej w tej procedurze:</span><span class="sxs-lookup"><span data-stu-id="94f87-116">You enable lazy area location reporting by using the configuration previously mentioned in this procedure:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setLazyAreaLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="94f87-117">Należy również określić uprawnienie lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="94f87-117">You also need to specify a location permission.</span></span> <span data-ttu-id="94f87-118">Ten kod zawiera ``COARSE`` uprawnienia:</span><span class="sxs-lookup"><span data-stu-id="94f87-118">This code uses ``COARSE`` permission:</span></span>

    <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

<span data-ttu-id="94f87-119">Jeśli aplikacja wymaga, możesz użyć ``ACCESS_FINE_LOCATION`` zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="94f87-119">If your app requires it, you can use ``ACCESS_FINE_LOCATION`` instead.</span></span>

### <a name="real-time-location-reporting"></a><span data-ttu-id="94f87-120">Raportowanie lokalizacji w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="94f87-120">Real-time location reporting</span></span>
<span data-ttu-id="94f87-121">Raportowanie lokalizacji w czasie rzeczywistym umożliwia raportowanie współrzędne geograficzne skojarzone z urządzeń.</span><span class="sxs-lookup"><span data-stu-id="94f87-121">Real-time location reporting enables reporting the latitude and longitude associated with devices.</span></span> <span data-ttu-id="94f87-122">Domyślnie raportowanie lokalizacji tego typu używa tylko lokalizacje sieciowe, na podstawie Identyfikatora komórki lub Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="94f87-122">By default, this type of location reporting only uses network locations, based on Cell ID or WIFI.</span></span> <span data-ttu-id="94f87-123">Raportowania jest aktywna tylko po uruchomieniu aplikacji na pierwszym planie (na przykład podczas sesji).</span><span class="sxs-lookup"><span data-stu-id="94f87-123">The reporting is only active when the application runs in foreground (for example, during a session).</span></span>

<span data-ttu-id="94f87-124">W czasie rzeczywistym lokalizacje są *nie* używany do obliczania statystyk.</span><span class="sxs-lookup"><span data-stu-id="94f87-124">Real-time locations are *NOT* used to compute statistics.</span></span> <span data-ttu-id="94f87-125">Ich jedynym celem jest, aby zezwolić na użycie grodzenia w czasie rzeczywistym \<Reach-odbiorców geofencing\> kryterium w kampanie Zasięgowe.</span><span class="sxs-lookup"><span data-stu-id="94f87-125">Their only purpose is to allow the use of real-time geo-fencing \<Reach-Audience-geofencing\> criterion in Reach campaigns.</span></span>

<span data-ttu-id="94f87-126">Aby włączyć lokalizacji w czasie rzeczywistym, raportowanie, Dodaj wiersz kodu do których wartość parametrów połączenia usługi Engagement w działaniu uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="94f87-126">To enable real-time location reporting, add a line of code to where you set the Engagement connection string in the launcher activity.</span></span> <span data-ttu-id="94f87-127">Wynik wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="94f87-127">The result looks like the following:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

        You also need to specify a location permission. This code uses ``COARSE`` permission:

            <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

        If your app requires it, you can use ``ACCESS_FINE_LOCATION`` instead.

#### <a name="gps-based-reporting"></a><span data-ttu-id="94f87-128">GPS na podstawie raportowania</span><span class="sxs-lookup"><span data-stu-id="94f87-128">GPS based reporting</span></span>
<span data-ttu-id="94f87-129">Domyślnie raportowanie lokalizacji w czasie rzeczywistym używa tylko lokalizacje sieciowe.</span><span class="sxs-lookup"><span data-stu-id="94f87-129">By default, real-time location reporting only uses network-based locations.</span></span> <span data-ttu-id="94f87-130">Aby włączyć korzystanie z lokalizacji na podstawie GPS, czyli znacznie bardziej dokładne, użyj obiektu konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="94f87-130">To enable the use of GPS-based locations, which are far more precise, use the configuration object:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setFineRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="94f87-131">Należy również dodać następujące uprawnienia, jeśli brakuje:</span><span class="sxs-lookup"><span data-stu-id="94f87-131">You also need to add the following permission if missing:</span></span>

    <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>

#### <a name="background-reporting"></a><span data-ttu-id="94f87-132">Raportowanie w tle</span><span class="sxs-lookup"><span data-stu-id="94f87-132">Background reporting</span></span>
<span data-ttu-id="94f87-133">Domyślnie raportowanie lokalizacji w czasie rzeczywistym jest aktywne po uruchomieniu aplikacji na pierwszym planie (na przykład podczas sesji).</span><span class="sxs-lookup"><span data-stu-id="94f87-133">By default, real-time location reporting is only active when the application runs in foreground (for example, during a session).</span></span> <span data-ttu-id="94f87-134">Aby włączyć raportowanie również, w tle, użyj tego obiektu konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="94f87-134">To enable the reporting also in background, use this configuration object:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setBackgroundRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

> [!NOTE]
> <span data-ttu-id="94f87-135">Po uruchomieniu aplikacji w tle, tylko lokalizacje sieciowe są raportowane, nawet jeśli włączono GPS.</span><span class="sxs-lookup"><span data-stu-id="94f87-135">When the application runs in background, only network-based locations are reported, even if you enabled the GPS.</span></span>
> 
> 

<span data-ttu-id="94f87-136">Jeśli użytkownik uruchamia swojego urządzenia, lokalizacji raportu tła jest zatrzymana.</span><span class="sxs-lookup"><span data-stu-id="94f87-136">If the user reboots their device, the background location report is stopped.</span></span> <span data-ttu-id="94f87-137">Aby umożliwić automatyczne ponowne uruchomienie przy rozruchu, Dodaj ten kod.</span><span class="sxs-lookup"><span data-stu-id="94f87-137">To make it automatically restart at boot time, add this code.</span></span>

    <receiver android:name="com.microsoft.azure.engagement.EngagementLocationBootReceiver"
           android:exported="false">
        <intent-filter>
            <action android:name="android.intent.action.BOOT_COMPLETED" />
        </intent-filter>
    </receiver>

<span data-ttu-id="94f87-138">Należy również dodać następujące uprawnienia, jeśli brakuje:</span><span class="sxs-lookup"><span data-stu-id="94f87-138">You also need to add the following permission if missing:</span></span>

    <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />

## <a name="android-m-permissions"></a><span data-ttu-id="94f87-139">Android M uprawnień</span><span class="sxs-lookup"><span data-stu-id="94f87-139">Android M permissions</span></span>
<span data-ttu-id="94f87-140">Począwszy od systemu Android M, niektóre uprawnienia są zarządzane w czasie wykonywania i wymagają zatwierdzenia użytkownika.</span><span class="sxs-lookup"><span data-stu-id="94f87-140">Starting with Android M, some permissions are managed at runtime and need user approval.</span></span>

<span data-ttu-id="94f87-141">Interfejs API systemu Android na poziomie 23 w przypadku skierowania, uprawnienia środowiska uruchomieniowego są domyślnie wyłączona w przypadku nowych instalacji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="94f87-141">If you target Android API level 23, the runtime permissions are turned off by default for new app installations.</span></span> <span data-ttu-id="94f87-142">W przeciwnym razie są włączone domyślnie.</span><span class="sxs-lookup"><span data-stu-id="94f87-142">Otherwise they are turned on by default.</span></span>

<span data-ttu-id="94f87-143">Użytkownik może Włączanie/wyłączanie te uprawnienia z menu ustawień urządzenia.</span><span class="sxs-lookup"><span data-stu-id="94f87-143">You can enable/disable those permissions from the device settings menu.</span></span> <span data-ttu-id="94f87-144">Wyłączenie uprawnień z menu systemowego kasuje procesów w tle aplikacji, która jest zachowanie systemowe i nie ma wpływu na możliwość odbierania wypychania w tle.</span><span class="sxs-lookup"><span data-stu-id="94f87-144">Turning off permissions from the system menu kills the background processes of the application, which is a system behavior, and has no impact on ability to receive push in background.</span></span>

<span data-ttu-id="94f87-145">W kontekście lokalizacji usługi Mobile Engagement raportowania są uprawnienia, które wymagają zatwierdzenia w czasie wykonywania:</span><span class="sxs-lookup"><span data-stu-id="94f87-145">In the context of Mobile Engagement location reporting, the permissions that require approval at runtime are:</span></span>

* `ACCESS_COARSE_LOCATION`
* `ACCESS_FINE_LOCATION`

<span data-ttu-id="94f87-146">Zażądaj uprawnień od użytkownika, korzystając z okna dialogowego standardowy system.</span><span class="sxs-lookup"><span data-stu-id="94f87-146">Request permissions from the user using a standard system dialog.</span></span> <span data-ttu-id="94f87-147">Jeśli użytkownik zaakceptuje, poinformuj ``EngagementAgent`` podjęcie zmiana pod uwagę w czasie rzeczywistym.</span><span class="sxs-lookup"><span data-stu-id="94f87-147">If the user approves, tell ``EngagementAgent`` to take that change into account in real-time.</span></span> <span data-ttu-id="94f87-148">W przeciwnym razie zmiany są przetwarzane przy następnym użytkownik uruchamia aplikację.</span><span class="sxs-lookup"><span data-stu-id="94f87-148">Otherwise the change is processed the next time the user launches the application.</span></span>

<span data-ttu-id="94f87-149">Oto przykład kodu do użycia w działaniu aplikacji, aby zażądać uprawnień i przekazuje wynik w przypadku wartości dodatniej do ``EngagementAgent``:</span><span class="sxs-lookup"><span data-stu-id="94f87-149">Here is a code sample to use in an activity of your application to request permissions and forward the result if positive to ``EngagementAgent``:</span></span>

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
         * Request location permission, but this doesn't explain why it is needed to the user.
         * The standard Android documentation explains with more details how to display a rationale activity to explain the user why the permission is needed in your application.
         * Putting COARSE vs FINE has no impact here, they are part of the same group for runtime permission management.
         */
        if (checkSelfPermission(android.Manifest.permission.ACCESS_FINE_LOCATION) != PackageManager.PERMISSION_GRANTED)
          requestPermissions(new String[] { android.Manifest.permission.ACCESS_FINE_LOCATION }, 0);

      }
    }

    @Override
    public void onRequestPermissionsResult(int requestCode, String[] permissions, int[] grantResults)
    {
      /* Only a positive location permission update requires engagement agent refresh, hence the request code matching from above function */
      if (requestCode == 0 && grantResults[0] == PackageManager.PERMISSION_GRANTED)
        getEngagementAgent().refreshPermissions();
    }
