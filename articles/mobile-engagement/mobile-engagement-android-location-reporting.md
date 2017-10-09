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
# <a name="location-reporting-for-azure-mobile-engagement-android-sdk"></a>Lokalizacja raportowania dla usługi Azure Mobile Engagement Android SDK
> [!div class="op_single_selector"]
> * [Android](mobile-engagement-android-integrate-engagement.md)
> 
> 

W tym temacie opisano sposób lokalizacji toodo raportowania dla aplikacji systemu Android.

## <a name="prerequisites"></a>Wymagania wstępne
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

## <a name="location-reporting"></a>Raportowanie lokalizacji
Jeśli chcesz toobe lokalizacji zgłoszone, należy tooadd kilka wierszy konfiguracji (między hello `<application>` i `</application>` tagów).

### <a name="lazy-area-location-reporting"></a>Raportowanie lokalizacji obszaru z opóźnieniem
Raportowanie lokalizacji obszaru z opóźnieniem umożliwia raportowania hello kraju, regionu i lokalizacji, skojarzone z urządzeń. Raportowanie lokalizacji tego typu używa tylko lokalizacje sieciowe (na podstawie Identyfikatora komórki lub Wi-Fi). obszar urządzenia Hello jest zgłaszana co najwyżej raz na sesję. Hello GPS nigdy nie jest używany, a w związku z tym tego typu lokalizacji raportu ma niski wpływ na powitania baterii.

Obszary zgłoszone są używane toocompute geograficzne statystyki dotyczące użytkowników, sesji zdarzenia i błędy. Mogą one również używane jako kryterium w kampanie Zasięgowe.

Możesz włączyć lokalizacji obszaru z opóźnieniem raportowania przy użyciu konfiguracji hello wymienione wcześniej w tej procedurze:

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setLazyAreaLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

Należy również toospecify uprawnienia lokalizacji. Ten kod zawiera ``COARSE`` uprawnienia:

    <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

Jeśli aplikacja wymaga, możesz użyć ``ACCESS_FINE_LOCATION`` zamiast tego.

### <a name="real-time-location-reporting"></a>Raportowanie lokalizacji w czasie rzeczywistym
Raportowanie lokalizacji w czasie rzeczywistym umożliwia raportowania hello współrzędne geograficzne., skojarzone z urządzeń. Domyślnie raportowanie lokalizacji tego typu używa tylko lokalizacje sieciowe, na podstawie Identyfikatora komórki lub Wi-Fi. Raportowanie Hello jest aktywne, gdy aplikacja hello działa na pierwszym planie (na przykład podczas sesji).

W czasie rzeczywistym lokalizacje są *nie* używane toocompute statystyk. Ich jedynym celem jest użycie hello tooallow grodzenia w czasie rzeczywistym \<Reach-odbiorców geofencing\> kryterium w kampanie Zasięgowe.

tooenable lokalizacji w czasie rzeczywistym, raportowanie, Dodaj wiersz z toowhere kodu ustawić parametry połączenia zaangażowania hello hello uruchamiania działania. wynik Hello wygląda hello:

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

        You also need toospecify a location permission. This code uses ``COARSE`` permission:

            <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

        If your app requires it, you can use ``ACCESS_FINE_LOCATION`` instead.

#### <a name="gps-based-reporting"></a>GPS na podstawie raportowania
Domyślnie raportowanie lokalizacji w czasie rzeczywistym używa tylko lokalizacje sieciowe. Użyj hello tooenable GPS na podstawie lokalizacji, które są znacznie bardziej dokładne, użyj obiektu konfiguracji hello:

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setFineRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

Należy również następujące uprawnienia, jeśli brakuje hello tooadd:

    <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>

#### <a name="background-reporting"></a>Raportowanie w tle
Domyślnie raportowanie lokalizacji w czasie rzeczywistym jest aktywne uruchomienie aplikacji hello na pierwszym planie (na przykład podczas sesji). Witaj tooenable także raportowanie w tle, należy użyć tego obiektu konfiguracji:

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setBackgroundRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

> [!NOTE]
> Po uruchomieniu aplikacji hello w tle, tylko lokalizacje sieciowe są raportowane, nawet jeśli włączono hello GPS.
> 
> 

Jeśli użytkownik hello ponownego uruchamiania urządzenia, hello tła lokalizacji raportu została zatrzymana. toomake automatycznie uruchomiony ponownie w czasie rozruchu, Dodaj ten kod.

    <receiver android:name="com.microsoft.azure.engagement.EngagementLocationBootReceiver"
           android:exported="false">
        <intent-filter>
            <action android:name="android.intent.action.BOOT_COMPLETED" />
        </intent-filter>
    </receiver>

Należy również następujące uprawnienia, jeśli brakuje hello tooadd:

    <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />

## <a name="android-m-permissions"></a>Android M uprawnień
Począwszy od systemu Android M, niektóre uprawnienia są zarządzane w czasie wykonywania i wymagają zatwierdzenia użytkownika.

Interfejs API systemu Android na poziomie 23 w przypadku skierowania, hello środowiska uruchomieniowego uprawnienia są domyślnie wyłączona dla nowych instalacji aplikacji. W przeciwnym razie są włączone domyślnie.

Użytkownik może Włącz/wyłącz te uprawnienia z menu ustawień urządzenia hello. Wyłączenie uprawnień z menu systemowe hello kasuje procesów w tle hello aplikacji hello, który jest zachowanie systemowe i nie ma wpływu na możliwość tooreceive wypychania w tle.

W kontekście hello lokalizacji usługi Mobile Engagement raportowania są hello uprawnienia, które wymagają zatwierdzenia w czasie wykonywania:

* `ACCESS_COARSE_LOCATION`
* `ACCESS_FINE_LOCATION`

Zażądaj uprawnień od użytkownika hello przy użyciu okna dialogowego standardowy system. Jeśli użytkownik hello zatwierdza, poinformuj ``EngagementAgent`` tootake, która zmienia pod uwagę w czasie rzeczywistym. W przeciwnym razie zmiany hello jest przetworzonych hello dalej hello użytkownika powoduje uruchomienie hello aplikacji w czasie.

Oto toouse przykładowy kod w działaniu aplikacji toorequest uprawnienia i do przodu hello wynik Jeśli dodatnią zbyt``EngagementAgent``:

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
