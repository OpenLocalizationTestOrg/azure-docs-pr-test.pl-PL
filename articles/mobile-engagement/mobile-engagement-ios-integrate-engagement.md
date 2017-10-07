---
title: aaaAzure Mobile Engagement iOS SDK Integration | Dokumentacja firmy Microsoft
description: "Najnowsze aktualizacje i procedury dla systemu iOS SDK dla usługi Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 947ea44b-00c1-450f-9a3b-74437954dc56
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 07/17/2017
ms.author: piyushjo
ms.openlocfilehash: 66ce34efabede7d882caa8a91431a8df71e4fb59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-engagement-on-ios"></a>Jak tooIntegrate zaangażowania w systemie iOS
> [!div class="op_single_selector"]
> * [Aplikacje uniwersalne systemu Windows](mobile-engagement-windows-store-integrate-engagement.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md)
> * [iOS](mobile-engagement-ios-integrate-engagement.md)
> * [Android](mobile-engagement-android-integrate-engagement.md)
>
>

W tej procedurze opisano analizy i funkcji w aplikacji systemu iOS monitorowania hello najprostszy sposób tooactivate usługi Engagement.

Witaj Engagement SDK wymaga systemu iOS7 + i Xcode 8 +: hello cel wdrożenia aplikacji musi mieć co najmniej system iOS 7.

> [!NOTE]
> Jeśli naprawdę są zależne od XCode 7, możesz użyć hello [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh). Brak znaną usterką na powitania moduł Reach tej poprzedniej wersji podczas uruchamiania na Zobacz urządzeń z systemem iOS 10 [hello integracji modułu reach](mobile-engagement-ios-integrate-engagement-reach.md) więcej szczegółów. Jeśli wybierz toouse hello SDK v3.2.4 pominąć hello `UserNotifications.framework` zaimportować w hello następnego kroku.
>
>

wymaga wystarczającej ilości raportu hello tooactivate dzienników toocompute wszystkie statystyki dotyczące użytkowników, sesji, działania, awarii (Crash) i Technicals to Hello następujące kroki. Raport Hello dzienników potrzebne toocompute innych danych statystycznych jak zadań, błędy i zdarzenia musi zostać wykonane ręcznie przy użyciu hello zaangażowania interfejsu API (zobacz [jak toouse hello zaawansowane znakowanie interfejsu API w aplikacji systemu iOS w usłudze Mobile Engagement](mobile-engagement-ios-use-engagement-api.md) od tych statystyk aplikacji są zależne.

## <a name="embed-hello-engagement-sdk-into-your-ios-project"></a>Osadź hello Engagement SDK do projektu systemu iOS
* Pobierz zestaw SDK systemu iOS hello z [tutaj](http://aka.ms/qk2rnj).
* Projekt dla systemu iOS tooyour Dodaj hello Engagement SDK: w środowisku Xcode, kliknij prawym przyciskiem myszy projekt i wybierz **"zbyt dodawania plików..."** i wybierz polecenie hello `EngagementSDK` folderu.
* Engagement wymaga dodatkowych struktur toowork: w obszarze Eksplorator projektów hello, otwórz okienko z projektu i wybierz hello prawidłowe. Następnie otwórz hello **"Fazy kompilacji"** kartę w hello **"Binarny z bibliotekami"** menu Dodaj następujące struktury:

  * `UserNotifications.framework`-zestaw hello Połącz jako`Optional`
  * `AdSupport.framework`-zestaw hello Połącz jako`Optional`
  * `SystemConfiguration.framework`
  * `CoreTelephony.framework`
  * `CFNetwork.framework`
  * `CoreLocation.framework`
  * `libxml2.dylib`

> [!NOTE]
> można usunąć Hello AdSupport framework. Engagement wymaga tego hello toocollect framework identyfikator IDFA. Jednak można wyłączyć kolekcji identyfikator IDFA \<ios-sdk zaangażowania — identyfikator idfa\> toocomply za pomocą nowych zasad Apple hello dotyczące tego identyfikatora.
>
>

## <a name="initialize-hello-engagement-sdk"></a>Inicjowanie hello Engagement SDK
Należy toomodify delegata aplikacji:

* U góry hello pliku implementacji należy zaimportować hello zaangażowania agenta:

      [...]
      #import "EngagementAgent.h"
* Inicjowanie usługi Engagement wewnątrz metody hello "**applicationDidFinishLaunching:**"lub"**aplikacji: didFinishLaunchingWithOptions:**":

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
      {
        [...]
        [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];
        [...]
      }

## <a name="basic-reporting"></a>Podstawowym raportowaniem
### <a name="recommended-method-overload-your-uiviewcontroller-classes"></a>Zalecana metoda: przeciążenia sieci `UIViewController` klas
W raporcie hello tooactivate kolejności wszystkich dzienników hello wymagane przez zaangażowania toocompute użytkowników, sesji, działania, awarii (Crash) i statystyki technicznych, możesz po prostu wprowadzić wszystkie Twoje `UIViewController` klasy podrzędne dziedziczą hello `EngagementViewController` klasy (zasada Aby uzyskać `UITableViewController`  - \> `EngagementTableViewController`).

**Bez usługi Engagement:**

    #import <UIKit/UIKit.h>

    @interface Tab1ViewController : UIViewController<UITextFieldDelegate> {
      UITextField* myTextField1;
      UITextField* myTextField2;
    }

    @property (nonatomic, retain) IBOutlet UITextField* myTextField1;
    @property (nonatomic, retain) IBOutlet UITextField* myTextField2;

**Z usługi Engagement:**

    #import <UIKit/UIKit.h>
    #import "EngagementViewController.h"

    @interface Tab1ViewController : EngagementViewController<UITextFieldDelegate> {
      UITextField* myTextField1;
      UITextField* myTextField2;
    }

    @property (nonatomic, retain) IBOutlet UITextField* myTextField1;
    @property (nonatomic, retain) IBOutlet UITextField* myTextField2;

### <a name="alternate-method-call-startactivity-manually"></a>Alternatywna metoda: wywołanie `startActivity()` ręcznie
Jeśli nie możesz lub nie ma toooverload Twojego `UIViewController` klas, zamiast tego można uruchomić działaniach, wywołując `EngagementAgent`w metody bezpośrednio.

> [!IMPORTANT]
> zestaw SDK systemu iOS Hello automatycznie wywołuje hello `endActivity()` metody, gdy aplikacja hello jest zamknięty. W związku z tym jest *wysokiej* zalecane toocall hello `startActivity` metody zmianie działania hello hello użytkownika i zbyt*nigdy* hello wywołania `endActivity` metody, ponieważ wywołanie tej metody wymusza Witaj toobe bieżąca sesja została zakończona.
>
>

## <a name="location-reporting"></a>Raportowanie lokalizacji
Apple warunków użytkowania usługi nie umożliwiają aplikacjom śledzenia w celu statystyki tylko lokalizacji toouse. W związku z tym zaleca się tooenable lokalizacji raportów tylko wtedy, gdy aplikacja także używać lokalizacji hello śledzenia z innego powodu.

Począwszy od systemu iOS 8, należy podać opis sposobu Twoja aplikacja korzysta z usług lokalizacji przez ustawienie ciąg dla klucza hello [NSLocationWhenInUseUsageDescription] lub [NSLocationAlwaysUsageDescription]w pliku Info.plist aplikacji. Jeśli chcesz tooreport lokalizacji w tle hello z Engagement Dodaj klucz hello NSLocationAlwaysUsageDescription. We wszystkich innych przypadkach Dodaj klucz hello NSLocationWhenInUseUsageDescription. Należy zauważyć, że możesz zarówno NSLocationAlwaysAndWhenInUseUsageDescription i NSLocationWhenInUseUsageDescription tooreport tła lokalizacji w systemie iOS 11.

### <a name="lazy-area-location-reporting"></a>Raportowanie lokalizacji obszaru z opóźnieniem
Raportowanie lokalizacji obszaru z opóźnieniem umożliwia tooreport hello kraj, region i lokalizację skojarzone toodevices. Raportowanie lokalizacji tego typu używa tylko lokalizacje sieciowe (na podstawie Identyfikatora komórki lub Wi-Fi). obszar urządzenia Hello jest zgłaszana co najwyżej raz na sesję. Hello GPS nie jest nigdy używana, a zatem ten typ lokalizacji raportu ma bardzo nieliczne (nie toosay żadnych) wpływ na powitania baterii.

Obszary zgłoszone są używane toocompute geograficzne statystyki dotyczące użytkowników, sesji, zdarzenia i błędy. Mogą one również używane jako kryterium w kampanie Zasięgowe. Ostatnia znana obszaru zgłoszonych dla urządzenia mogą być pobrane Dziękujemy toohello Hello [interfejsu API urządzenia].

Raportowanie lokalizacji obszaru z opóźnieniem tooenable Dodaj hello następującego wiersza po inicjowanie agenta zaangażowania hello:

    - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
    {
      [...]
      [[EngagementAgent shared] setLazyAreaLocationReport:YES];
      [...]
    }

### <a name="real-time-location-reporting"></a>Raportowanie lokalizacji w czasie rzeczywistym
Raportowanie lokalizacji w czasie rzeczywistym umożliwia tooreport hello szerokości i długości geograficznej skojarzone toodevices. Domyślnie raportowanie lokalizacji tego typu używa tylko lokalizacje sieciowe (na podstawie Identyfikatora komórki lub Wi-Fi), a raportowanie hello jest aktywny tylko po hello aplikacja jest uruchamiana na pierwszym planie (np. podczas sesji).

Lokalizacje w czasie rzeczywistym *nie* używane toocompute statystyk. Ich jedynym celem jest użycie hello tooallow grodzenia czasu rzeczywistego \<Reach-odbiorców geofencing\> kryterium w kampanie Zasięgowe.

miejsca w czasie rzeczywistym tooenable raportowania, należy dodać hello następującego wiersza po inicjowanie agenta zaangażowania hello:

    [[EngagementAgent shared] setRealtimeLocationReport:YES];

#### <a name="gps-based-reporting"></a>GPS na podstawie raportowania
Domyślnie raportowanie lokalizacji w czasie rzeczywistym używa tylko lokalizacje sieciowe. Użycie hello tooenable GPS na podstawie lokalizacji (które są znacznie bardziej precyzyjne), dodać:

    [[EngagementAgent shared] setFineRealtimeLocationReport:YES];

#### <a name="background-reporting"></a>Raportowanie w tle
Domyślnie raportowanie lokalizacji w czasie rzeczywistym jest aktywne uruchomienie aplikacji hello na pierwszym planie (np. podczas sesji). hello tooenable także raportowanie w tle, należy dodać:

    [[EngagementAgent shared] setBackgroundRealtimeLocationReport:YES withLaunchOptions:launchOptions];

> [!NOTE]
> Po uruchomieniu aplikacji hello w tle, tylko lokalizacje sieciowe są raportowane, nawet jeśli włączono hello GPS.
>
>

Implementacja tej funkcji będzie wywoływać [startMonitoringSignificantLocationChanges] po aplikacja przechodzi w tle hello. Należy pamiętać, że jej zostanie automatycznie uruchom ponownie aplikację na tle hello Jeśli jest to nowe zdarzenie lokalizacji.

## <a name="advanced-reporting"></a>Zaawansowane raportowanie
Opcjonalnie, jeśli chcesz tooreport aplikacji określonych zdarzeń, błędów i zadań, należy toouse hello zaangażowania interfejsu API za pomocą metody hello hello `EngagementAgent` klasy. Obiekt tej klasy mogą zostać pobrane przez wywołanie hello `[EngagementAgent shared]` metody statycznej.

Hello zaangażowania interfejs API umożliwia toouse wszystkie funkcje zaawansowane usługi Engagement i została szczegółowo opisana na powitania jak tooUse interfejsu API programu zaangażowania w systemie iOS (a także w dokumentacji technicznej hello hello `EngagementAgent` klasy).

## <a name="disable-idfa-collection"></a>Wyłącz funkcję zbierania identyfikator IDFA
Domyślnie program zaangażowania użyje hello [identyfikator IDFA] toouniquely identyfikacji użytkownika. Ale jeśli nie używasz reklamy w innym miejscu w aplikacji hello, mogą zostać odrzucone przez hello procesu przeglądu sklepu z aplikacjami. Identyfikator IDFA kolekcji można wyłączyć, dodając makro preprocesora hello `ENGAGEMENT_DISABLE_IDFA` w pliku pch (lub w hello `Build Settings` aplikacji). To zagwarantować, że nie jest żadnych odwołań zbyt`ASIdentifierManager`, `advertisingIdentifier` lub `isAdvertisingTrackingEnabled` w kompilacji aplikacji hello.

Integracji hello **prefix.pch** pliku:

    #define ENGAGEMENT_DISABLE_IDFA
    ...

Można Sprawdź, czy kolekcja identyfikator IDFA hello prawidłowo jest wyłączone w aplikacji w sprawdzając dzienników testu zaangażowania hello. Zobacz hello Testowanie integracji\<ios-sdk-engagement testu — identyfikator idfa\> dokumentacji, aby uzyskać więcej informacji.

## <a name="disable-log-reporting"></a>Wyłączanie dziennika raportowania
### <a name="using-a-method-call"></a>Przy użyciu wywołania metody
Jeśli chcesz toostop zaangażowania wysyłania dzienników, można wywołać:

    [[EngagementAgent shared] setEnabled:NO];

To wywołanie jest trwały: używa `NSUserDefaults` toostore hello informacji.

Możesz włączyć ponownie raportowania przez wywołanie metody hello sam działać z dziennika `YES`.

### <a name="integration-in-your-settings-bundle"></a>Integracja z ustawień pakietu
Zamiast wywoływania tej funkcji, to ustawienie można również zintegrować bezpośrednio w istniejącą `Settings.bundle` pliku. ciąg Hello `engagement_agent_enabled` musi być używany jako identyfikator preferencji hello, a musi być skojarzony tooa Przełącz przełącznika (`PSToggleSwitchSpecifier`).

Witaj następujący przykład `Settings.bundle` przedstawia sposób tooimplement go:

    <dict>
        <key>PreferenceSpecifiers</key>
        <array>
            <dict>
                <key>DefaultValue</key>
                <true/>
                <key>Key</key>
                <string>engagement_agent_enabled</string>
                <key>Title</key>
                <string>Log reporting enabled</string>
                <key>Type</key>
                <string>PSToggleSwitchSpecifier</string>
            </dict>
        </array>
        <key>StringsTable</key>
        <string>Root</string>
    </dict>

<!-- URLs. -->
[interfejsu API urządzenia]: http://go.microsoft.com/?linkid=9876094
[NSLocationWhenInUseUsageDescription]:https://developer.apple.com/library/prerelease/ios/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW26
[NSLocationAlwaysUsageDescription]:https://developer.apple.com/library/prerelease/ios/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW18
[startMonitoringSignificantLocationChanges]:http://developer.apple.com/library/IOs/#documentation/CoreLocation/Reference/CLLocationManager_Class/CLLocationManager/CLLocationManager.html#//apple_ref/occ/instm/CLLocationManager/startMonitoringSignificantLocationChanges
[identyfikator IDFA]:https://developer.apple.com/library/ios/documentation/AdSupport/Reference/ASIdentifierManager_Ref/ASIdentifierManager.html#//apple_ref/occ/instp/ASIdentifierManager/advertisingIdentifier
