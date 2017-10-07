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
# <a name="how-toointegrate-engagement-on-ios"></a><span data-ttu-id="f1fcc-103">Jak tooIntegrate zaangażowania w systemie iOS</span><span class="sxs-lookup"><span data-stu-id="f1fcc-103">How tooIntegrate Engagement on iOS</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f1fcc-104">Aplikacje uniwersalne systemu Windows</span><span class="sxs-lookup"><span data-stu-id="f1fcc-104">Windows Universal</span></span>](mobile-engagement-windows-store-integrate-engagement.md)
> * [<span data-ttu-id="f1fcc-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="f1fcc-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="f1fcc-106">iOS</span><span class="sxs-lookup"><span data-stu-id="f1fcc-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="f1fcc-107">Android</span><span class="sxs-lookup"><span data-stu-id="f1fcc-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md)
>
>

<span data-ttu-id="f1fcc-108">W tej procedurze opisano analizy i funkcji w aplikacji systemu iOS monitorowania hello najprostszy sposób tooactivate usługi Engagement.</span><span class="sxs-lookup"><span data-stu-id="f1fcc-108">This procedure describes hello simplest way tooactivate Engagement's Analytics and Monitoring functions in your iOS application.</span></span>

<span data-ttu-id="f1fcc-109">Witaj Engagement SDK wymaga systemu iOS7 + i Xcode 8 +: hello cel wdrożenia aplikacji musi mieć co najmniej system iOS 7.</span><span class="sxs-lookup"><span data-stu-id="f1fcc-109">hello Engagement SDK requires iOS7+ and Xcode 8+: hello deployment target of your application must be at least iOS 7.</span></span>

> [!NOTE]
> <span data-ttu-id="f1fcc-110">Jeśli naprawdę są zależne od XCode 7, możesz użyć hello [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span><span class="sxs-lookup"><span data-stu-id="f1fcc-110">If you really depend on XCode 7 then you may use hello [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span></span> <span data-ttu-id="f1fcc-111">Brak znaną usterką na powitania moduł Reach tej poprzedniej wersji podczas uruchamiania na Zobacz urządzeń z systemem iOS 10 [hello integracji modułu reach](mobile-engagement-ios-integrate-engagement-reach.md) więcej szczegółów.</span><span class="sxs-lookup"><span data-stu-id="f1fcc-111">There is a known bug on hello Reach module of this previous version while running on iOS 10 devices see [hello reach module integration](mobile-engagement-ios-integrate-engagement-reach.md) for more details.</span></span> <span data-ttu-id="f1fcc-112">Jeśli wybierz toouse hello SDK v3.2.4 pominąć hello `UserNotifications.framework` zaimportować w hello następnego kroku.</span><span class="sxs-lookup"><span data-stu-id="f1fcc-112">If you choose toouse hello SDK v3.2.4 then just skip hello `UserNotifications.framework` import in hello next step.</span></span>
>
>

<span data-ttu-id="f1fcc-113">wymaga wystarczającej ilości raportu hello tooactivate dzienników toocompute wszystkie statystyki dotyczące użytkowników, sesji, działania, awarii (Crash) i Technicals to Hello następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="f1fcc-113">hello following steps are enough tooactivate hello report of logs needed toocompute all statistics regarding Users, Sessions, Activities, Crashes and Technicals.</span></span> <span data-ttu-id="f1fcc-114">Raport Hello dzienników potrzebne toocompute innych danych statystycznych jak zadań, błędy i zdarzenia musi zostać wykonane ręcznie przy użyciu hello zaangażowania interfejsu API (zobacz [jak toouse hello zaawansowane znakowanie interfejsu API w aplikacji systemu iOS w usłudze Mobile Engagement](mobile-engagement-ios-use-engagement-api.md) od tych statystyk aplikacji są zależne.</span><span class="sxs-lookup"><span data-stu-id="f1fcc-114">hello report of logs needed toocompute other statistics like Events, Errors and Jobs must be done manually using hello Engagement API  (see [How toouse hello advanced Mobile Engagement tagging API in your iOS app](mobile-engagement-ios-use-engagement-api.md) since these statistics are application dependent.</span></span>

## <a name="embed-hello-engagement-sdk-into-your-ios-project"></a><span data-ttu-id="f1fcc-115">Osadź hello Engagement SDK do projektu systemu iOS</span><span class="sxs-lookup"><span data-stu-id="f1fcc-115">Embed hello Engagement SDK into your iOS project</span></span>
* <span data-ttu-id="f1fcc-116">Pobierz zestaw SDK systemu iOS hello z [tutaj](http://aka.ms/qk2rnj).</span><span class="sxs-lookup"><span data-stu-id="f1fcc-116">Download hello iOS SDK from [here](http://aka.ms/qk2rnj).</span></span>
* <span data-ttu-id="f1fcc-117">Projekt dla systemu iOS tooyour Dodaj hello Engagement SDK: w środowisku Xcode, kliknij prawym przyciskiem myszy projekt i wybierz **"zbyt dodawania plików..."** i wybierz polecenie hello `EngagementSDK` folderu.</span><span class="sxs-lookup"><span data-stu-id="f1fcc-117">Add hello Engagement SDK tooyour iOS project: in Xcode, right click on your project and select **"Add files too..."** and choose hello `EngagementSDK` folder.</span></span>
* <span data-ttu-id="f1fcc-118">Engagement wymaga dodatkowych struktur toowork: w obszarze Eksplorator projektów hello, otwórz okienko z projektu i wybierz hello prawidłowe.</span><span class="sxs-lookup"><span data-stu-id="f1fcc-118">Engagement requires additional frameworks toowork: in hello project explorer, open your project pane and select hello correct target.</span></span> <span data-ttu-id="f1fcc-119">Następnie otwórz hello **"Fazy kompilacji"** kartę w hello **"Binarny z bibliotekami"** menu Dodaj następujące struktury:</span><span class="sxs-lookup"><span data-stu-id="f1fcc-119">Then, open hello **"Build phases"** tab and in hello **"Link Binary With Libraries"** menu, add these frameworks:</span></span>

  * <span data-ttu-id="f1fcc-120">`UserNotifications.framework`-zestaw hello Połącz jako`Optional`</span><span class="sxs-lookup"><span data-stu-id="f1fcc-120">`UserNotifications.framework` - set hello link as `Optional`</span></span>
  * <span data-ttu-id="f1fcc-121">`AdSupport.framework`-zestaw hello Połącz jako`Optional`</span><span class="sxs-lookup"><span data-stu-id="f1fcc-121">`AdSupport.framework` - set hello link as `Optional`</span></span>
  * `SystemConfiguration.framework`
  * `CoreTelephony.framework`
  * `CFNetwork.framework`
  * `CoreLocation.framework`
  * `libxml2.dylib`

> [!NOTE]
> <span data-ttu-id="f1fcc-122">można usunąć Hello AdSupport framework.</span><span class="sxs-lookup"><span data-stu-id="f1fcc-122">hello AdSupport framework can be removed.</span></span> <span data-ttu-id="f1fcc-123">Engagement wymaga tego hello toocollect framework identyfikator IDFA.</span><span class="sxs-lookup"><span data-stu-id="f1fcc-123">Engagement needs this framework toocollect hello IDFA.</span></span> <span data-ttu-id="f1fcc-124">Jednak można wyłączyć kolekcji identyfikator IDFA \<ios-sdk zaangażowania — identyfikator idfa\> toocomply za pomocą nowych zasad Apple hello dotyczące tego identyfikatora.</span><span class="sxs-lookup"><span data-stu-id="f1fcc-124">However, IDFA collection can be disabled \<ios-sdk-engagement-idfa\> toocomply with hello new Apple policy regarding this ID.</span></span>
>
>

## <a name="initialize-hello-engagement-sdk"></a><span data-ttu-id="f1fcc-125">Inicjowanie hello Engagement SDK</span><span class="sxs-lookup"><span data-stu-id="f1fcc-125">Initialize hello Engagement SDK</span></span>
<span data-ttu-id="f1fcc-126">Należy toomodify delegata aplikacji:</span><span class="sxs-lookup"><span data-stu-id="f1fcc-126">You need toomodify your Application Delegate:</span></span>

* <span data-ttu-id="f1fcc-127">U góry hello pliku implementacji należy zaimportować hello zaangażowania agenta:</span><span class="sxs-lookup"><span data-stu-id="f1fcc-127">At hello top of your implementation file, import hello Engagement agent:</span></span>

      [...]
      #import "EngagementAgent.h"
* <span data-ttu-id="f1fcc-128">Inicjowanie usługi Engagement wewnątrz metody hello "**applicationDidFinishLaunching:**"lub"**aplikacji: didFinishLaunchingWithOptions:**":</span><span class="sxs-lookup"><span data-stu-id="f1fcc-128">Initialize Engagement inside hello method '**applicationDidFinishLaunching:**' or '**application:didFinishLaunchingWithOptions:**':</span></span>

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
      {
        [...]
        [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];
        [...]
      }

## <a name="basic-reporting"></a><span data-ttu-id="f1fcc-129">Podstawowym raportowaniem</span><span class="sxs-lookup"><span data-stu-id="f1fcc-129">Basic reporting</span></span>
### <a name="recommended-method-overload-your-uiviewcontroller-classes"></a><span data-ttu-id="f1fcc-130">Zalecana metoda: przeciążenia sieci `UIViewController` klas</span><span class="sxs-lookup"><span data-stu-id="f1fcc-130">Recommended method: overload your `UIViewController` classes</span></span>
<span data-ttu-id="f1fcc-131">W raporcie hello tooactivate kolejności wszystkich dzienników hello wymagane przez zaangażowania toocompute użytkowników, sesji, działania, awarii (Crash) i statystyki technicznych, możesz po prostu wprowadzić wszystkie Twoje `UIViewController` klasy podrzędne dziedziczą hello `EngagementViewController` klasy (zasada Aby uzyskać `UITableViewController`  - \> `EngagementTableViewController`).</span><span class="sxs-lookup"><span data-stu-id="f1fcc-131">In order tooactivate hello report of all hello logs required by Engagement toocompute Users, Sessions, Activities, Crashes and Technical statistics, you can simply make all your `UIViewController` sub-classes inherit from hello `EngagementViewController` classes (same rule for `UITableViewController` -\> `EngagementTableViewController`).</span></span>

<span data-ttu-id="f1fcc-132">**Bez usługi Engagement:**</span><span class="sxs-lookup"><span data-stu-id="f1fcc-132">**Without Engagement :**</span></span>

    #import <UIKit/UIKit.h>

    @interface Tab1ViewController : UIViewController<UITextFieldDelegate> {
      UITextField* myTextField1;
      UITextField* myTextField2;
    }

    @property (nonatomic, retain) IBOutlet UITextField* myTextField1;
    @property (nonatomic, retain) IBOutlet UITextField* myTextField2;

<span data-ttu-id="f1fcc-133">**Z usługi Engagement:**</span><span class="sxs-lookup"><span data-stu-id="f1fcc-133">**With Engagement :**</span></span>

    #import <UIKit/UIKit.h>
    #import "EngagementViewController.h"

    @interface Tab1ViewController : EngagementViewController<UITextFieldDelegate> {
      UITextField* myTextField1;
      UITextField* myTextField2;
    }

    @property (nonatomic, retain) IBOutlet UITextField* myTextField1;
    @property (nonatomic, retain) IBOutlet UITextField* myTextField2;

### <a name="alternate-method-call-startactivity-manually"></a><span data-ttu-id="f1fcc-134">Alternatywna metoda: wywołanie `startActivity()` ręcznie</span><span class="sxs-lookup"><span data-stu-id="f1fcc-134">Alternate method: call `startActivity()` manually</span></span>
<span data-ttu-id="f1fcc-135">Jeśli nie możesz lub nie ma toooverload Twojego `UIViewController` klas, zamiast tego można uruchomić działaniach, wywołując `EngagementAgent`w metody bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="f1fcc-135">If you cannot or do not want toooverload your `UIViewController` classes, you can instead start your activities by calling `EngagementAgent`'s methods directly.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f1fcc-136">zestaw SDK systemu iOS Hello automatycznie wywołuje hello `endActivity()` metody, gdy aplikacja hello jest zamknięty.</span><span class="sxs-lookup"><span data-stu-id="f1fcc-136">hello iOS SDK automatically calls hello `endActivity()` method when hello application is closed.</span></span> <span data-ttu-id="f1fcc-137">W związku z tym jest *wysokiej* zalecane toocall hello `startActivity` metody zmianie działania hello hello użytkownika i zbyt*nigdy* hello wywołania `endActivity` metody, ponieważ wywołanie tej metody wymusza Witaj toobe bieżąca sesja została zakończona.</span><span class="sxs-lookup"><span data-stu-id="f1fcc-137">Thus, it is *HIGHLY* recommended toocall hello `startActivity` method whenever hello activity of hello user change, and too*NEVER* call hello `endActivity` method, since calling this method forces hello current session toobe ended.</span></span>
>
>

## <a name="location-reporting"></a><span data-ttu-id="f1fcc-138">Raportowanie lokalizacji</span><span class="sxs-lookup"><span data-stu-id="f1fcc-138">Location reporting</span></span>
<span data-ttu-id="f1fcc-139">Apple warunków użytkowania usługi nie umożliwiają aplikacjom śledzenia w celu statystyki tylko lokalizacji toouse.</span><span class="sxs-lookup"><span data-stu-id="f1fcc-139">Apple terms of service do not allow applications toouse location tracking for statistics purpose only.</span></span> <span data-ttu-id="f1fcc-140">W związku z tym zaleca się tooenable lokalizacji raportów tylko wtedy, gdy aplikacja także używać lokalizacji hello śledzenia z innego powodu.</span><span class="sxs-lookup"><span data-stu-id="f1fcc-140">Thus, it is recommended tooenable location reports only if your application also use hello location tracking for another reason.</span></span>

<span data-ttu-id="f1fcc-141">Począwszy od systemu iOS 8, należy podać opis sposobu Twoja aplikacja korzysta z usług lokalizacji przez ustawienie ciąg dla klucza hello [NSLocationWhenInUseUsageDescription] lub [NSLocationAlwaysUsageDescription]w pliku Info.plist aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f1fcc-141">Starting with iOS 8, you must provide a description for how your app uses location services by setting a string for hello key [NSLocationWhenInUseUsageDescription] or [NSLocationAlwaysUsageDescription] in your app's Info.plist file.</span></span> <span data-ttu-id="f1fcc-142">Jeśli chcesz tooreport lokalizacji w tle hello z Engagement Dodaj klucz hello NSLocationAlwaysUsageDescription.</span><span class="sxs-lookup"><span data-stu-id="f1fcc-142">If you want tooreport location in hello background with Engagement, add hello key NSLocationAlwaysUsageDescription.</span></span> <span data-ttu-id="f1fcc-143">We wszystkich innych przypadkach Dodaj klucz hello NSLocationWhenInUseUsageDescription.</span><span class="sxs-lookup"><span data-stu-id="f1fcc-143">In all other cases, add hello key NSLocationWhenInUseUsageDescription.</span></span> <span data-ttu-id="f1fcc-144">Należy zauważyć, że możesz zarówno NSLocationAlwaysAndWhenInUseUsageDescription i NSLocationWhenInUseUsageDescription tooreport tła lokalizacji w systemie iOS 11.</span><span class="sxs-lookup"><span data-stu-id="f1fcc-144">Note that you need both NSLocationAlwaysAndWhenInUseUsageDescription and NSLocationWhenInUseUsageDescription tooreport background location on iOS 11.</span></span>

### <a name="lazy-area-location-reporting"></a><span data-ttu-id="f1fcc-145">Raportowanie lokalizacji obszaru z opóźnieniem</span><span class="sxs-lookup"><span data-stu-id="f1fcc-145">Lazy area location reporting</span></span>
<span data-ttu-id="f1fcc-146">Raportowanie lokalizacji obszaru z opóźnieniem umożliwia tooreport hello kraj, region i lokalizację skojarzone toodevices.</span><span class="sxs-lookup"><span data-stu-id="f1fcc-146">Lazy area location reporting allows tooreport hello country, region and locality associated toodevices.</span></span> <span data-ttu-id="f1fcc-147">Raportowanie lokalizacji tego typu używa tylko lokalizacje sieciowe (na podstawie Identyfikatora komórki lub Wi-Fi).</span><span class="sxs-lookup"><span data-stu-id="f1fcc-147">This type of location reporting only uses network locations (based on Cell ID or WIFI).</span></span> <span data-ttu-id="f1fcc-148">obszar urządzenia Hello jest zgłaszana co najwyżej raz na sesję.</span><span class="sxs-lookup"><span data-stu-id="f1fcc-148">hello device area is reported at most once per session.</span></span> <span data-ttu-id="f1fcc-149">Hello GPS nie jest nigdy używana, a zatem ten typ lokalizacji raportu ma bardzo nieliczne (nie toosay żadnych) wpływ na powitania baterii.</span><span class="sxs-lookup"><span data-stu-id="f1fcc-149">hello GPS is never used, and thus this type of location report has very few (not toosay no) impact on hello battery.</span></span>

<span data-ttu-id="f1fcc-150">Obszary zgłoszone są używane toocompute geograficzne statystyki dotyczące użytkowników, sesji, zdarzenia i błędy.</span><span class="sxs-lookup"><span data-stu-id="f1fcc-150">Reported areas are used toocompute geographic statistics about users, sessions, events and errors.</span></span> <span data-ttu-id="f1fcc-151">Mogą one również używane jako kryterium w kampanie Zasięgowe.</span><span class="sxs-lookup"><span data-stu-id="f1fcc-151">They can also be used as criterion in Reach campaigns.</span></span> <span data-ttu-id="f1fcc-152">Ostatnia znana obszaru zgłoszonych dla urządzenia mogą być pobrane Dziękujemy toohello Hello [interfejsu API urządzenia].</span><span class="sxs-lookup"><span data-stu-id="f1fcc-152">hello last known area reported for a device can be retrieved thanks toohello [Device API].</span></span>

<span data-ttu-id="f1fcc-153">Raportowanie lokalizacji obszaru z opóźnieniem tooenable Dodaj hello następującego wiersza po inicjowanie agenta zaangażowania hello:</span><span class="sxs-lookup"><span data-stu-id="f1fcc-153">tooenable lazy area location reporting, add hello following line after initializing hello Engagement agent:</span></span>

    - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
    {
      [...]
      [[EngagementAgent shared] setLazyAreaLocationReport:YES];
      [...]
    }

### <a name="real-time-location-reporting"></a><span data-ttu-id="f1fcc-154">Raportowanie lokalizacji w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="f1fcc-154">Real time location reporting</span></span>
<span data-ttu-id="f1fcc-155">Raportowanie lokalizacji w czasie rzeczywistym umożliwia tooreport hello szerokości i długości geograficznej skojarzone toodevices.</span><span class="sxs-lookup"><span data-stu-id="f1fcc-155">Real time location reporting allows tooreport hello latitude and longitude associated toodevices.</span></span> <span data-ttu-id="f1fcc-156">Domyślnie raportowanie lokalizacji tego typu używa tylko lokalizacje sieciowe (na podstawie Identyfikatora komórki lub Wi-Fi), a raportowanie hello jest aktywny tylko po hello aplikacja jest uruchamiana na pierwszym planie (np. podczas sesji).</span><span class="sxs-lookup"><span data-stu-id="f1fcc-156">By default, this type of location reporting only uses network locations (based on Cell ID or WIFI), and hello reporting is only active when hello application runs in foreground (i.e. during a session).</span></span>

<span data-ttu-id="f1fcc-157">Lokalizacje w czasie rzeczywistym *nie* używane toocompute statystyk.</span><span class="sxs-lookup"><span data-stu-id="f1fcc-157">Real time locations are *NOT* used toocompute statistics.</span></span> <span data-ttu-id="f1fcc-158">Ich jedynym celem jest użycie hello tooallow grodzenia czasu rzeczywistego \<Reach-odbiorców geofencing\> kryterium w kampanie Zasięgowe.</span><span class="sxs-lookup"><span data-stu-id="f1fcc-158">Their only purpose is tooallow hello use of real time geo-fencing \<Reach-Audience-geofencing\> criterion in Reach campaigns.</span></span>

<span data-ttu-id="f1fcc-159">miejsca w czasie rzeczywistym tooenable raportowania, należy dodać hello następującego wiersza po inicjowanie agenta zaangażowania hello:</span><span class="sxs-lookup"><span data-stu-id="f1fcc-159">tooenable real time location reporting, add hello following line after initializing hello Engagement agent:</span></span>

    [[EngagementAgent shared] setRealtimeLocationReport:YES];

#### <a name="gps-based-reporting"></a><span data-ttu-id="f1fcc-160">GPS na podstawie raportowania</span><span class="sxs-lookup"><span data-stu-id="f1fcc-160">GPS based reporting</span></span>
<span data-ttu-id="f1fcc-161">Domyślnie raportowanie lokalizacji w czasie rzeczywistym używa tylko lokalizacje sieciowe.</span><span class="sxs-lookup"><span data-stu-id="f1fcc-161">By default, real time location reporting only uses network based locations.</span></span> <span data-ttu-id="f1fcc-162">Użycie hello tooenable GPS na podstawie lokalizacji (które są znacznie bardziej precyzyjne), dodać:</span><span class="sxs-lookup"><span data-stu-id="f1fcc-162">tooenable hello use of GPS based locations (which are far more precise), add:</span></span>

    [[EngagementAgent shared] setFineRealtimeLocationReport:YES];

#### <a name="background-reporting"></a><span data-ttu-id="f1fcc-163">Raportowanie w tle</span><span class="sxs-lookup"><span data-stu-id="f1fcc-163">Background reporting</span></span>
<span data-ttu-id="f1fcc-164">Domyślnie raportowanie lokalizacji w czasie rzeczywistym jest aktywne uruchomienie aplikacji hello na pierwszym planie (np. podczas sesji).</span><span class="sxs-lookup"><span data-stu-id="f1fcc-164">By default, real time location reporting is only active when hello application runs in foreground (i.e. during a session).</span></span> <span data-ttu-id="f1fcc-165">hello tooenable także raportowanie w tle, należy dodać:</span><span class="sxs-lookup"><span data-stu-id="f1fcc-165">tooenable hello reporting also in background, add:</span></span>

    [[EngagementAgent shared] setBackgroundRealtimeLocationReport:YES withLaunchOptions:launchOptions];

> [!NOTE]
> <span data-ttu-id="f1fcc-166">Po uruchomieniu aplikacji hello w tle, tylko lokalizacje sieciowe są raportowane, nawet jeśli włączono hello GPS.</span><span class="sxs-lookup"><span data-stu-id="f1fcc-166">When hello application runs in background, only network based locations are reported, even if you enabled hello GPS.</span></span>
>
>

<span data-ttu-id="f1fcc-167">Implementacja tej funkcji będzie wywoływać [startMonitoringSignificantLocationChanges] po aplikacja przechodzi w tle hello.</span><span class="sxs-lookup"><span data-stu-id="f1fcc-167">Implementation of this function will call [startMonitoringSignificantLocationChanges] when your application goes into hello background.</span></span> <span data-ttu-id="f1fcc-168">Należy pamiętać, że jej zostanie automatycznie uruchom ponownie aplikację na tle hello Jeśli jest to nowe zdarzenie lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="f1fcc-168">Be aware that it will automatically relaunch your application into hello background if a new location event arrives.</span></span>

## <a name="advanced-reporting"></a><span data-ttu-id="f1fcc-169">Zaawansowane raportowanie</span><span class="sxs-lookup"><span data-stu-id="f1fcc-169">Advanced reporting</span></span>
<span data-ttu-id="f1fcc-170">Opcjonalnie, jeśli chcesz tooreport aplikacji określonych zdarzeń, błędów i zadań, należy toouse hello zaangażowania interfejsu API za pomocą metody hello hello `EngagementAgent` klasy.</span><span class="sxs-lookup"><span data-stu-id="f1fcc-170">Optionally, if you want tooreport application specific events, errors and jobs, you need toouse hello Engagement API through hello methods of hello `EngagementAgent` class.</span></span> <span data-ttu-id="f1fcc-171">Obiekt tej klasy mogą zostać pobrane przez wywołanie hello `[EngagementAgent shared]` metody statycznej.</span><span class="sxs-lookup"><span data-stu-id="f1fcc-171">An object of this class can be retrieved by calling hello `[EngagementAgent shared]` static method.</span></span>

<span data-ttu-id="f1fcc-172">Hello zaangażowania interfejs API umożliwia toouse wszystkie funkcje zaawansowane usługi Engagement i została szczegółowo opisana na powitania jak tooUse interfejsu API programu zaangażowania w systemie iOS (a także w dokumentacji technicznej hello hello `EngagementAgent` klasy).</span><span class="sxs-lookup"><span data-stu-id="f1fcc-172">hello Engagement API allows toouse all of Engagement's advanced capabilities and is detailed in hello How tooUse the Engagement API on iOS (as well as in hello technical documentation of hello `EngagementAgent` class).</span></span>

## <a name="disable-idfa-collection"></a><span data-ttu-id="f1fcc-173">Wyłącz funkcję zbierania identyfikator IDFA</span><span class="sxs-lookup"><span data-stu-id="f1fcc-173">Disable IDFA collection</span></span>
<span data-ttu-id="f1fcc-174">Domyślnie program zaangażowania użyje hello [identyfikator IDFA] toouniquely identyfikacji użytkownika.</span><span class="sxs-lookup"><span data-stu-id="f1fcc-174">By default, Engagement will use hello [IDFA] toouniquely identify a user.</span></span> <span data-ttu-id="f1fcc-175">Ale jeśli nie używasz reklamy w innym miejscu w aplikacji hello, mogą zostać odrzucone przez hello procesu przeglądu sklepu z aplikacjami.</span><span class="sxs-lookup"><span data-stu-id="f1fcc-175">But if you’re not using advertising elsewhere in hello app, you might be rejected by hello App Store review process.</span></span> <span data-ttu-id="f1fcc-176">Identyfikator IDFA kolekcji można wyłączyć, dodając makro preprocesora hello `ENGAGEMENT_DISABLE_IDFA` w pliku pch (lub w hello `Build Settings` aplikacji).</span><span class="sxs-lookup"><span data-stu-id="f1fcc-176">IDFA collection can be disabled by adding hello preprocessor macro `ENGAGEMENT_DISABLE_IDFA` in your pch file (or in hello `Build Settings` of your application).</span></span> <span data-ttu-id="f1fcc-177">To zagwarantować, że nie jest żadnych odwołań zbyt`ASIdentifierManager`, `advertisingIdentifier` lub `isAdvertisingTrackingEnabled` w kompilacji aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="f1fcc-177">This will ensure that there is no references too`ASIdentifierManager`, `advertisingIdentifier` or `isAdvertisingTrackingEnabled` in hello application build.</span></span>

<span data-ttu-id="f1fcc-178">Integracji hello **prefix.pch** pliku:</span><span class="sxs-lookup"><span data-stu-id="f1fcc-178">Integration in hello **prefix.pch** file:</span></span>

    #define ENGAGEMENT_DISABLE_IDFA
    ...

<span data-ttu-id="f1fcc-179">Można Sprawdź, czy kolekcja identyfikator IDFA hello prawidłowo jest wyłączone w aplikacji w sprawdzając dzienników testu zaangażowania hello.</span><span class="sxs-lookup"><span data-stu-id="f1fcc-179">You can verify that hello IDFA collection is properly disabled in your application by checking hello Engagement test logs.</span></span> <span data-ttu-id="f1fcc-180">Zobacz hello Testowanie integracji\<ios-sdk-engagement testu — identyfikator idfa\> dokumentacji, aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="f1fcc-180">See hello Integration Test\<ios-sdk-engagement-test-idfa\> documentation for further information.</span></span>

## <a name="disable-log-reporting"></a><span data-ttu-id="f1fcc-181">Wyłączanie dziennika raportowania</span><span class="sxs-lookup"><span data-stu-id="f1fcc-181">Disable log reporting</span></span>
### <a name="using-a-method-call"></a><span data-ttu-id="f1fcc-182">Przy użyciu wywołania metody</span><span class="sxs-lookup"><span data-stu-id="f1fcc-182">Using a method call</span></span>
<span data-ttu-id="f1fcc-183">Jeśli chcesz toostop zaangażowania wysyłania dzienników, można wywołać:</span><span class="sxs-lookup"><span data-stu-id="f1fcc-183">If you want Engagement toostop sending logs, you can call:</span></span>

    [[EngagementAgent shared] setEnabled:NO];

<span data-ttu-id="f1fcc-184">To wywołanie jest trwały: używa `NSUserDefaults` toostore hello informacji.</span><span class="sxs-lookup"><span data-stu-id="f1fcc-184">This call is persistent: it uses `NSUserDefaults` toostore hello information.</span></span>

<span data-ttu-id="f1fcc-185">Możesz włączyć ponownie raportowania przez wywołanie metody hello sam działać z dziennika `YES`.</span><span class="sxs-lookup"><span data-stu-id="f1fcc-185">You can enable log reporting again by calling hello same function with `YES`.</span></span>

### <a name="integration-in-your-settings-bundle"></a><span data-ttu-id="f1fcc-186">Integracja z ustawień pakietu</span><span class="sxs-lookup"><span data-stu-id="f1fcc-186">Integration in your settings bundle</span></span>
<span data-ttu-id="f1fcc-187">Zamiast wywoływania tej funkcji, to ustawienie można również zintegrować bezpośrednio w istniejącą `Settings.bundle` pliku.</span><span class="sxs-lookup"><span data-stu-id="f1fcc-187">Instead of calling this function, you can also integrate this setting directly in your existing `Settings.bundle` file.</span></span> <span data-ttu-id="f1fcc-188">ciąg Hello `engagement_agent_enabled` musi być używany jako identyfikator preferencji hello, a musi być skojarzony tooa Przełącz przełącznika (`PSToggleSwitchSpecifier`).</span><span class="sxs-lookup"><span data-stu-id="f1fcc-188">hello string `engagement_agent_enabled` must be used as a hello preference identifier and it must be associated tooa toggle switch(`PSToggleSwitchSpecifier`).</span></span>

<span data-ttu-id="f1fcc-189">Witaj następujący przykład `Settings.bundle` przedstawia sposób tooimplement go:</span><span class="sxs-lookup"><span data-stu-id="f1fcc-189">hello following example of `Settings.bundle` shows how tooimplement it:</span></span>

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
