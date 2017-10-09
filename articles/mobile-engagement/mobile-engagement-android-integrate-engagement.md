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
# <a name="how-toointegrate-engagement-on-android"></a>Jak tooIntegrate zaangażowania w systemie Android
> [!div class="op_single_selector"]
> * [Aplikacje uniwersalne systemu Windows](mobile-engagement-windows-store-integrate-engagement.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md)
> * [iOS](mobile-engagement-ios-integrate-engagement.md)
> * [Android](mobile-engagement-android-integrate-engagement.md)
> 
> 

W tej procedurze opisano analizy i funkcji w aplikacji systemu Android monitorowania hello najprostszy sposób tooactivate usługi Engagement.

> [!IMPORTANT]
> Minimalny poziom interfejsu API zestawu SDK systemu Android musi być 10 lub nowszej (Android 2.3.3 lub nowszej).
> 
> 

wymaga wystarczającej ilości raportu hello tooactivates dzienników toocompute wszystkie statystyki dotyczące użytkowników, sesji, działania, awarii (Crash) i Technicals to Hello następujące kroki. Raport Hello dzienników potrzebne toocompute innych danych statystycznych jak zadań, błędy i zdarzenia musi zostać wykonane ręcznie przy użyciu hello zaangażowania interfejsu API (zobacz [jak toouse hello zaawansowane znakowanie interfejsu API w dla systemu Android w usłudze Mobile Engagement](mobile-engagement-android-use-engagement-api.md) od tych statystyki są aplikacji zależnej.

## <a name="embed-hello-engagement-sdk-and-service-into-your-android-project"></a>Osadź hello Engagement SDK i usługi do projektu systemu Android
Pobieranie hello zestawu SDK systemu Android z [tutaj](https://aka.ms/vq9mfn) uzyskać `mobile-engagement-VERSION.jar` i umieść je w hello `libs` folderu projektu systemu Android (Utwórz folder biblioteki hello, jeśli jeszcze nie istnieje).

> [!IMPORTANT]
> Tworzenie pakietu aplikacji z narzędzia ProGuard, należy najpierw tookeep niektórych klas. Program hello następującego fragmentu konfiguracji:
> 
> -zachować Klasa publiczna * rozszerza android.os.IInterface — Zachowaj {com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS — klasa
> 
> <methods>; }
> 
> 

Określ ciąg połączenia zaangażowania przez wywołanie hello następujące metody w działaniu uruchamiania hello:

            EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
            engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
            EngagementAgent.getInstance(this).init(engagementConfiguration);

Parametry połączenia Hello aplikacji jest wyświetlana w portalu Azure.

* Jeśli brakuje, należy dodać hello następujących uprawnień dla systemu Android (przed hello `<application>` tagu):
  
          <uses-permission android:name="android.permission.INTERNET"/>
          <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
* Dodaj następujące sekcji hello (między hello `<application>` i `</application>` tagów):
  
          <service
            android:name="com.microsoft.azure.engagement.service.EngagementService"
            android:exported="false"
            android:label="<Your application name>Service"
            android:process=":Engagement"/>
* Zmień `<Your application name>` hello nazwę aplikacji.

> [!TIP]
> Witaj `android:label` atrybutu pozwala toochoose nazwę hello hello usługi Engagement jak będzie wyświetlany użytkownikom końcowym toohello ekranie powitania "Uruchamianie usługi" Telefon. Jest zalecana tooset za ten atrybut`"<Your application name>Service"` (np. `"AcmeFunGameService"`).
> 
> 

Określanie hello `android:process` zapewnia atrybut tej usługi Engagement hello będą uruchamiane w swoim własnym procesie (uruchomionego zaangażowania w hello tego samego procesu jak aplikacji spowoduje, że Twoje main/wątku interfejsu użytkownika będzie potencjalnie mniej dynamiczne).

> [!NOTE]
> Kod umieszczony w `Application.onCreate()` i innych wywołań zwrotnych aplikacji zostanie uruchomione dla procesów wszystkich aplikacji, w tym hello usługi Engagement. Może mieć niepożądane skutki uboczne (takich jak przydziału pamięci niepotrzebnych i wątków w procesie hello zaangażowania, zduplikowany odbiorniki emisji lub usługi).
> 
> 

Jeśli można zastąpić `Application.onCreate()`, jest zalecane tooadd hello następującego fragmentu kodu na początku hello Twojej `Application.onCreate()` funkcji:

             public void onCreate()
             {
               if (EngagementAgentUtils.isInDedicatedEngagementProcess(this))
                 return;

               ... Your code...
             }

Możesz zrobić hello samo dla `Application.onTerminate()`, `Application.onLowMemory()` i `Application.onConfigurationChanged(...)`.

Można również rozszerzyć zasięg `EngagementApplication` zamiast rozszerzanie `Application`: hello wywołania zwrotnego `Application.onCreate()` hello procesu wyboru i wywołania `Application.onApplicationProcessCreate()` tylko jeśli hello bieżący proces jest nie hello jeden hello zaangażowania Usługa hostingu, hello te same zasady stosowane dla Witaj innych wywołań zwrotnych.

## <a name="basic-reporting"></a>Podstawowym raportowaniem
### <a name="recommended-method-overload-your-activity-classes"></a>Zalecana metoda: przeciążenia sieci `Activity` klas
W raporcie hello tooactivate kolejności wszystkich dzienników hello wymagane przez zaangażowania toocompute użytkowników, sesji, działania, awarii (Crash) i statystyki technicznych, wystarczy toomake wszystkie Twoje `*Activity` klasy podrzędne dziedziczą odpowiadającego hello `Engagement*Activity` klasy (np. Jeśli działanie starszej wersji `ListActivity`, Utwórz rozszerza `EngagementListActivity`).

**Bez usługi Engagement:**

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

**Z usługi Engagement:**

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
> Korzystając z `EngagementListActivity` lub `EngagementExpandableListActivity`, upewnij się, że w żadnym wywołaniu zbyt`requestWindowFeature(...);` dokonane przed wywołaniem hello zbyt`super.onCreate(...);`, w przeciwnym razie wystąpi awaria.
> 
> 

Te klasy można znaleźć w hello `src` folderu i skopiować je do projektu. klasy Hello znajdują się również w hello **JavaDoc**.

### <a name="alternate-method-call-startactivity-and-endactivity-manually"></a>Alternatywna metoda: wywołanie `startActivity()` i `endActivity()` ręcznie
Jeśli nie możesz lub nie ma toooverload Twojego `Activity` klasy, można zamiast tego rozpoczęcia i zakończenia działań przez wywołanie metody `EngagementAgent`przez metody bezpośrednio.

> [!IMPORTANT]
> zestaw SDK systemu Android Hello nigdy nie wywołuje hello `endActivity()` metody, nawet wtedy, gdy aplikacja hello jest zamknięta (w systemie Android, aplikacje są faktycznie nigdy nie zamknięte). W związku z tym jest *wysokiej* zalecane toocall hello `startActivity()` metoda hello `onResume` wywołania zwrotnego z *wszystkie* działań i hello `endActivity()` metoda hello `onPause()` Wywołanie zwrotne z *wszystkie* działań. Jest to hello tylko sposób toobe się upewnić, że sesje nie zostaną ujawnione. Jeśli przeciek sesji hello usługi Engagement nigdy nie spowoduje rozłączenie z zapleczem usługi Engagement hello (ponieważ usługa hello połączono tak długo, jak długo trwa oczekiwanie na sesji).
> 
> 

Oto przykład:

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

Ten przykład toohello bardzo podobne `EngagementActivity` klasy i jej wariantów, którego kod źródłowy jest udostępniany w hello `src` folderu.

## <a name="test"></a>Testowanie
Teraz Sprawdź, czy integracją przez uruchomienie aplikacji mobilnej w emulator lub urządzenie i weryfikowanie rejestruje sesji na karcie monitorowanie hello.

następne sekcje Hello są opcjonalne.

## <a name="location-reporting"></a>Raportowanie lokalizacji
Jeśli chcesz toobe lokalizacji zgłoszone, należy tooadd kilka wierszy konfiguracji (między hello `<application>` i `</application>` tagów).

### <a name="lazy-area-location-reporting"></a>Raportowanie lokalizacji obszaru z opóźnieniem
Raportowanie lokalizacji obszaru z opóźnieniem umożliwia tooreport hello kraj, region i lokalizację skojarzone toodevices. Raportowanie lokalizacji tego typu używa tylko lokalizacje sieciowe (na podstawie Identyfikatora komórki lub Wi-Fi). obszar urządzenia Hello jest zgłaszana co najwyżej raz na sesję. Hello GPS nie jest nigdy używana, a zatem ten typ lokalizacji raportu ma bardzo nieliczne (nie toosay żadnych) wpływ na powitania baterii.

Obszary zgłoszone są używane toocompute geograficzne statystyki dotyczące użytkowników, sesji, zdarzenia i błędy. Mogą one również używane jako kryterium w kampanie Zasięgowe.

lokalizacji obszaru z opóźnieniem tooenable raportowania, możesz zrobić to za pomocą konfiguracji hello wymienione wcześniej w tej procedurze:

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setLazyAreaLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

Należy również następujące uprawnienia, jeśli brakuje hello tooadd:

            <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

Lub możesz korzystać ``ACCESS_FINE_LOCATION`` Jeśli już używać w aplikacji.

### <a name="real-time-location-reporting"></a>Raportowanie lokalizacji w czasie rzeczywistym
Raportowanie lokalizacji w czasie rzeczywistym umożliwia tooreport hello szerokości i długości geograficznej skojarzone toodevices. Domyślnie raportowanie lokalizacji tego typu używa tylko lokalizacje sieciowe (na podstawie Identyfikatora komórki lub Wi-Fi), a raportowanie hello jest aktywny tylko po hello aplikacja jest uruchamiana na pierwszym planie (np. podczas sesji).

Lokalizacje w czasie rzeczywistym *nie* używane toocompute statystyk. Ich jedynym celem jest użycie hello tooallow grodzenia czasu rzeczywistego \<Reach-odbiorców geofencing\> kryterium w kampanie Zasięgowe.

Lokalizacja czasu rzeczywistego tooenable raportowania, możesz zrobić to za pomocą konfiguracji hello wymienione wcześniej w tej procedurze:

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

Należy również następujące uprawnienia, jeśli brakuje hello tooadd:

            <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

Lub możesz korzystać ``ACCESS_FINE_LOCATION`` Jeśli już używać w aplikacji.

#### <a name="gps-based-reporting"></a>GPS na podstawie raportowania
Domyślnie raportowanie lokalizacji w czasie rzeczywistym używa tylko lokalizacje sieciowe. Użycie hello tooenable GPS na podstawie lokalizacji (które są znacznie bardziej precyzyjne), użyj obiektu konfiguracji hello:

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setFineRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

Należy również następujące uprawnienia, jeśli brakuje hello tooadd:

            <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>

#### <a name="background-reporting"></a>Raportowanie w tle
Domyślnie raportowanie lokalizacji w czasie rzeczywistym jest aktywne uruchomienie aplikacji hello na pierwszym planie (np. podczas sesji). raportowania hello tooenable również w tle, użyj obiektu konfiguracji hello:

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setBackgroundRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

> [!NOTE]
> Po uruchomieniu aplikacji hello w tle, tylko lokalizacje sieciowe są raportowane, nawet jeśli włączono hello GPS.
> 
> 

Hello tła lokalizacji raportu zostanie zatrzymana, jeśli użytkownik hello ponownym uruchomieniu urządzenia, można dodać tego toomake automatycznie uruchomiony ponownie w czasie rozruchu:

            <receiver android:name="com.microsoft.azure.engagement.EngagementLocationBootReceiver"
               android:exported="false">
               <intent-filter>
                  <action android:name="android.intent.action.BOOT_COMPLETED" />
               </intent-filter>
            </receiver>

Należy również następujące uprawnienia, jeśli brakuje hello tooadd:

            <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />

### <a name="android-m-permissions"></a>Android M uprawnień
Począwszy od systemu Android M, niektóre uprawnienia są zarządzane w czasie wykonywania i wymaga zatwierdzenia użytkownika.

Hello środowiska uruchomieniowego uprawnienia zostaną wyłączone domyślnie do nowych instalacji aplikacji, w przypadku skierowania interfejsu API systemu Android na poziomie 23. W przeciwnym razie ona zostanie włączona domyślnie.

Hello użytkownika można włączyć/wyłączyć te uprawnienia z menu ustawień urządzenia hello. Wyłączenie uprawnień z menu systemowe kasuje procesów w tle aplikacji hello, jest zachowanie systemu które nie ma wpływu na możliwość tooreceive wypychania w tle.

W kontekście hello Mobile Engagement hello uprawnienia, które wymagają zatwierdzenia w czasie wykonywania są:

* `ACCESS_COARSE_LOCATION`
* `ACCESS_FINE_LOCATION`
* `WRITE_EXTERNAL_STORAGE`(tylko wtedy, gdy przeznaczonych dla interfejsu API systemu Android na poziomie 23 tej)

magazynu zewnętrznego Hello jest używany tylko dla funkcji szerszej Reach. Jeśli okaże się, prosząc użytkowników o tym destrukcyjne toobe uprawnienia, możesz je usunąć używane tylko w przypadku usługi Mobile Engagement, ale się to kosztem hello wyłączenia funkcji Duży obraz.

W przypadku funkcji lokalizacji hello należy zażądać toouser uprawnienia za pomocą okna dialogowego standardowy system. Jeśli zatwierdza hello użytkownika, należy tootell ``EngagementAgent`` tootake, która zmienia pod uwagę w czasie rzeczywistym (w przeciwnym razie Zmień hello będzie przetworzonych hello dalej hello użytkownika powoduje uruchomienie hello aplikacji w czasie).

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

## <a name="advanced-reporting"></a>Zaawansowane raportowanie
Opcjonalnie, jeśli chcesz tooreport aplikacji określonych zdarzeń, błędów i zadań, należy toouse hello zaangażowania interfejsu API za pomocą metody hello hello `EngagementAgent` klasy. Obiekt tej klasy może być pobranych przez wywołanie hello `EngagementAgent.getInstance()` metody statycznej.

Hello zaangażowania interfejs API umożliwia toouse wszystkie funkcje zaawansowane usługi Engagement i została szczegółowo opisana na powitania jak tooUse interfejsu API programu zaangażowania w systemie Android (a także w dokumentacji technicznej hello hello `EngagementAgent` klasy).

## <a name="advanced-configuration-in-androidmanifestxml"></a>Konfiguracja zaawansowana (w pliku AndroidManifest.xml)
### <a name="wake-locks"></a>Wznawianie pracy blokad
Toobe się upewnić, że statystyki są wysyłane w czasie rzeczywistym za pomocą sieci Wi-Fi lub ekranu hello jest wyłączona, dodać hello następujące uprawnienia opcjonalne:

            <uses-permission android:name="android.permission.WAKE_LOCK"/>

### <a name="crash-report"></a>Raport o awarii
Raporty awarii toodisable, należy dodać to (między hello `<application>` i `</application>` tagów):

            <meta-data android:name="engagement:reportCrash" android:value="false"/>

### <a name="burst-threshold"></a>Próg serii
Domyślnie raporty usługi Engagement hello rejestruje się w czasie rzeczywistym. Jeśli aplikacja zgłasza dzienniki bardzo często, jest lepsze toobuffer hello dzienniki i tooreport ich jednocześnie na regularne podstawy czasu (jest to nazywane hello "tryb serii"). toodo tak, dodaj ją (między hello `<application>` i `</application>` tagów):

            <meta-data android:name="engagement:burstThreshold" android:value="{interval between too bursts (in milliseconds)}"/>

Witaj tryb serii wydłużyć baterii hello życia ale ma wpływ na powitania Monitor zaangażowania: wszystkie czas trwania zadania i sesje będą zaokrąglone toohello serii próg (w związku z tym sesji i zadania krótsze niż próg serii hello może nie być widoczna). Jest zalecana toouse próg w serii się niż 30000 (30s).

### <a name="session-timeout"></a>Limit czasu sesji
Domyślnie sesja jest 10s zakończone po zakończeniu hello jego ostatniej aktywności (która zazwyczaj występuje przez naciśnięcie przycisku hello Home lub kopii klucza, przez ustawienie hello phone bezczynności lub przejście do innej aplikacji). Jest to tooavoid podziału sesji każdego użytkownika w czasie hello wyjść i bardzo szybko powrócić toohello aplikacji (które mogą wystąpić podczas odebrania on obrazu, sprawdź powiadomienia itp.). Ten parametr może być toomodify. toodo tak, dodaj ją (między hello `<application>` i `</application>` tagów):

            <meta-data android:name="engagement:sessionTimeout" android:value="{session timeout (in milliseconds)}"/>

## <a name="disable-log-reporting"></a>Wyłączanie dziennika raportowania
### <a name="using-a-method-call"></a>Przy użyciu wywołania metody
Jeśli chcesz toostop zaangażowania wysyłania dzienników, można wywołać:

            EngagementAgent.getInstance(context).setEnabled(false);

To wywołanie jest trwały: używa plików udostępnionych preferencji.

Jeśli zaangażowania jest aktywny, gdy wywołanie tej funkcji, może upłynąć 1 minutę hello toostop usługi. Jednak nie będzie uruchomić usługi hello na wszystkich hello następnym uruchomieniu aplikacji hello.

Możesz włączyć ponownie raportowania przez wywołanie metody hello sam działać z dziennika `true`.

### <a name="integration-in-your-own-preferenceactivity"></a>Integracja z własną`PreferenceActivity`
Zamiast wywoływania tej funkcji, to ustawienie można również zintegrować bezpośrednio w istniejącą `PreferenceActivity`.

Toouse zaangażowania preferencje plików (w trybie żądaną hello) można skonfigurować w hello `AndroidManifest.xml` pliku z `application meta-data`:

* Witaj `engagement:agent:settings:name` klucz to nazwa hello toodefine używanych plików udostępnionych preferencji hello.
* Witaj `engagement:agent:settings:mode` klucza jest tryb hello toodefine używanych plików udostępnionych preferencji hello, należy użyć hello tego samego trybu jako w Twojej `PreferenceActivity`. Tryb Hello muszą być przekazywane w postaci liczby: Jeśli korzystasz z kombinacją flag stałej w kodzie, sprawdź wartość całkowita hello.

Zaangażowania zawsze używać hello `engagement:key` logiczna klucz w pliku preferencji hello zarządzania to ustawienie.

Witaj następujący przykład `AndroidManifest.xml` pokazuje hello wartości domyślne:

            <application>
                [...]
                <meta-data
                  android:name="engagement:agent:settings:name"
                  android:value="engagement.agent" />
                <meta-data
                  android:name="engagement:agent:settings:mode"
                  android:value="0" />

Następnie można dodać `CheckBoxPreference` w układzie preferencji, takich jak hello jednym następującego:

            <CheckBoxPreference
              android:key="engagement:enabled"
              android:defaultValue="true"
              android:title="Use Engagement"
              android:summaryOn="Engagement is enabled."
              android:summaryOff="Engagement is disabled." />

<!-- URLs. -->
[Device API]: http://go.microsoft.com/?linkid=9876094
