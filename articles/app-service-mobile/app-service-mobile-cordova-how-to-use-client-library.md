---
title: "tooUse aaaHow Apache wtyczki Cordova dla usługi Azure Mobile Apps"
description: "Jak tooUse Apache wtyczki Cordova dla usługi Azure Mobile Apps"
services: app-service\mobile
documentationcenter: javascript
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: a56a1ce4-de0c-4f3c-8763-66252c52aa59
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-html
ms.devlang: javascript
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: d3e0639e6478c409132af25304a2fb0f28401e98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-apache-cordova-client-library-for-azure-mobile-apps"></a><span data-ttu-id="22647-103">Jak toouse Apache Cordova klienta biblioteki usługi Azure Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="22647-103">How toouse Apache Cordova client library for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

<span data-ttu-id="22647-104">Ten przewodnik zawiera wskazówki, tooperform typowych scenariuszy przy użyciu hello najnowszych [Apache wtyczki Cordova dla usługi Azure Mobile Apps].</span><span class="sxs-lookup"><span data-stu-id="22647-104">This guide teaches you tooperform common scenarios using hello latest [Apache Cordova Plugin for Azure Mobile Apps].</span></span> <span data-ttu-id="22647-105">W przypadku nowych aplikacji mobilnej tooAzure najpierw zakończyć [Azure Mobile Apps Szybki Start] toocreate zaplecza, Utwórz tabelę i Pobierz wstępnie skompilowanym projektem Apache Cordova.</span><span class="sxs-lookup"><span data-stu-id="22647-105">If you are new tooAzure Mobile Apps, first complete [Azure Mobile Apps Quick Start] toocreate a backend, create a table, and download a pre-built Apache Cordova project.</span></span> <span data-ttu-id="22647-106">W tym przewodniku, możemy skupić się na powitania klienta wtyczki programu Apache Cordova.</span><span class="sxs-lookup"><span data-stu-id="22647-106">In this guide, we focus on hello client-side Apache Cordova Plugin.</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="22647-107">Obsługiwane platformy</span><span class="sxs-lookup"><span data-stu-id="22647-107">Supported platforms</span></span>
<span data-ttu-id="22647-108">Zestaw SDK obsługuje Apache Cordova 6.0.0 i później z systemem iOS, Android i Windows urządzeń.</span><span class="sxs-lookup"><span data-stu-id="22647-108">This SDK supports Apache Cordova v6.0.0 and later on iOS, Android, and Windows devices.</span></span>  <span data-ttu-id="22647-109">Obsługa platform Hello jest następujący:</span><span class="sxs-lookup"><span data-stu-id="22647-109">hello platform support is as follows:</span></span>

* <span data-ttu-id="22647-110">Interfejs API systemu android 19 – 24 (KitKat za pośrednictwem nugacie).</span><span class="sxs-lookup"><span data-stu-id="22647-110">Android API 19-24 (KitKat through Nougat).</span></span>
* <span data-ttu-id="22647-111">System iOS w wersji 8.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="22647-111">iOS versions 8.0 and later.</span></span>
* <span data-ttu-id="22647-112">Windows Phone 8.1.</span><span class="sxs-lookup"><span data-stu-id="22647-112">Windows Phone 8.1.</span></span>
* <span data-ttu-id="22647-113">Platforma uniwersalna systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="22647-113">Universal Windows Platform.</span></span>

## <span data-ttu-id="22647-114"><a name="Setup"></a>Instalacji i wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="22647-114"><a name="Setup"></a>Setup and prerequisites</span></span>
<span data-ttu-id="22647-115">W tym przewodniku założono, że utworzono wewnętrznej bazie danych z tabeli.</span><span class="sxs-lookup"><span data-stu-id="22647-115">This guide assumes that you have created a backend with a table.</span></span> <span data-ttu-id="22647-116">W tym przewodniku założono tabeli hello ma hello tego samego schematu jako tabele hello w tych samouczkach.</span><span class="sxs-lookup"><span data-stu-id="22647-116">This guide assumes that hello table has hello same schema as hello tables in those tutorials.</span></span> <span data-ttu-id="22647-117">W tym przewodniku założono również, dodano hello wtyczki Cordova Apache tooyour kodu.</span><span class="sxs-lookup"><span data-stu-id="22647-117">This guide also assumes that you have added hello Apache Cordova Plugin tooyour code.</span></span>  <span data-ttu-id="22647-118">Jeśli użytkownik nie zostało zrobione, można dodać projektu tooyour wtyczki oprogramowania Apache Cordova hello hello w wierszu polecenia:</span><span class="sxs-lookup"><span data-stu-id="22647-118">If you have not done so, you may add hello Apache Cordova plugin tooyour project on hello command line:</span></span>

```
cordova plugin add cordova-plugin-ms-azure-mobile-apps
```

<span data-ttu-id="22647-119">Aby uzyskać więcej informacji na temat tworzenia [pierwszej aplikacji platformy Apache Cordova], ich w dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="22647-119">For more information on creating [your first Apache Cordova app], see their documentation.</span></span>

## <span data-ttu-id="22647-120"><a name="ionic"></a>Konfigurowanie aplikacji jonowych v2</span><span class="sxs-lookup"><span data-stu-id="22647-120"><a name="ionic"></a>Setting up an Ionic v2 app</span></span>

<span data-ttu-id="22647-121">tooproperly Konfigurowanie projektu jonowych v2 najpierw utworzyć podstawową aplikację i dodawanie wtyczki Cordova hello:</span><span class="sxs-lookup"><span data-stu-id="22647-121">tooproperly configure an Ionic v2 project, first create a basic app and add hello Cordova plugin:</span></span>

```
ionic start projectName --v2
cd projectName
ionic plugin add cordova-plugin-ms-azure-mobile-apps
```

<span data-ttu-id="22647-122">Dodaj następujące wiersze zbyt hello`app.component.ts` toocreate powitania klienta obiektu:</span><span class="sxs-lookup"><span data-stu-id="22647-122">Add hello following lines too`app.component.ts` toocreate hello client object:</span></span>

```
declare var WindowsAzure: any;
var client = new WindowsAzure.MobileServiceClient("https://yoursite.azurewebsites.net");
```

<span data-ttu-id="22647-123">Można teraz skompilować i uruchomić projekt hello w przeglądarce hello:</span><span class="sxs-lookup"><span data-stu-id="22647-123">You can now build and run hello project in hello browser:</span></span>

```
ionic platform add browser
ionic run browser
```

<span data-ttu-id="22647-124">Witaj wtyczkę Azure Mobile Apps Cordova obsługuje zarówno jonowych aplikacje v1 i v2.</span><span class="sxs-lookup"><span data-stu-id="22647-124">hello Azure Mobile Apps Cordova plugin supports both Ionic v1 and v2 apps.</span></span>  <span data-ttu-id="22647-125">Tylko aplikacje hello jonowych v2 wymagają dodatkowych deklaracji dla hello `WindowsAzure` obiektu.</span><span class="sxs-lookup"><span data-stu-id="22647-125">Only hello Ionic v2 apps require the additional declaration for hello `WindowsAzure` object.</span></span>

[!INCLUDE [app-service-mobile-html-js-library.md](../../includes/app-service-mobile-html-js-library.md)]

## <span data-ttu-id="22647-126"><a name="auth"></a>Porady: uwierzytelnianie użytkowników</span><span class="sxs-lookup"><span data-stu-id="22647-126"><a name="auth"></a>How to: Authenticate users</span></span>
<span data-ttu-id="22647-127">Usługa aplikacji Azure obsługuje uwierzytelniania i autoryzacji użytkowników aplikacji przy użyciu różnych dostawców tożsamości zewnętrznych: Facebook, Google, Microsoft Account i Twitter.</span><span class="sxs-lookup"><span data-stu-id="22647-127">Azure App Service supports authenticating and authorizing app users using various external identity providers: Facebook, Google, Microsoft Account, and Twitter.</span></span> <span data-ttu-id="22647-128">Możesz ustawić uprawnienia na dostęp do tabel toorestrict dla określonych operacji tooonly uwierzytelnieni użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="22647-128">You can set permissions on tables toorestrict access for specific operations tooonly authenticated users.</span></span> <span data-ttu-id="22647-129">Umożliwia także tożsamości hello reguł autoryzacji użytkowników uwierzytelnionych tooimplement w skryptach serwera.</span><span class="sxs-lookup"><span data-stu-id="22647-129">You can also use hello identity of authenticated users tooimplement authorization rules in server scripts.</span></span> <span data-ttu-id="22647-130">Aby uzyskać więcej informacji, zobacz hello [Rozpoczynanie pracy z uwierzytelnianiem] samouczka.</span><span class="sxs-lookup"><span data-stu-id="22647-130">For more information, see hello [Get started with authentication] tutorial.</span></span>

<span data-ttu-id="22647-131">Korzystając z uwierzytelniania w aplikacji oprogramowania Apache Cordova, hello następujące wtyczki Cordova muszą być dostępne:</span><span class="sxs-lookup"><span data-stu-id="22647-131">When using authentication in an Apache Cordova app, hello following Cordova plugins must be available:</span></span>

* <span data-ttu-id="22647-132">[cordova wtyczka urządzenie]</span><span class="sxs-lookup"><span data-stu-id="22647-132">[cordova-plugin-device]</span></span>
* <span data-ttu-id="22647-133">[cordova wtyczka inappbrowser]</span><span class="sxs-lookup"><span data-stu-id="22647-133">[cordova-plugin-inappbrowser]</span></span>

<span data-ttu-id="22647-134">Obsługiwane są dwa przepływy uwierzytelniania: przepływu serwera i klienta przepływu.</span><span class="sxs-lookup"><span data-stu-id="22647-134">Two authentication flows are supported: a server flow and a client flow.</span></span>  <span data-ttu-id="22647-135">powitania serwera przepływu zapewnia hello najprostszym uwierzytelniania, ponieważ zależy od interfejsu uwierzytelniania sieci web dostawcy hello.</span><span class="sxs-lookup"><span data-stu-id="22647-135">hello server flow provides hello simplest authentication experience, as it relies on hello provider's web authentication interface.</span></span> <span data-ttu-id="22647-136">Witaj przepływu klienta umożliwia lepsza integracja z możliwości specyficznych dla urządzeń takich jak single-sign-on jako opiera się na zestawy SDK urządzenia specyficznego dla dostawcy.</span><span class="sxs-lookup"><span data-stu-id="22647-136">hello client flow allows for deeper integration with device-specific capabilities such as single-sign-on as it relies on provider-specific device-specific SDKs.</span></span>

[!INCLUDE [app-service-mobile-html-js-auth-library.md](../../includes/app-service-mobile-html-js-auth-library.md)]

### <span data-ttu-id="22647-137"><a name="configure-external-redirect-urls"></a>Porady: Konfigurowanie usługi Mobile App Service dla adresy URL przekierowań zewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="22647-137"><a name="configure-external-redirect-urls"></a>How to: Configure your Mobile App Service for external redirect URLs.</span></span>
<span data-ttu-id="22647-138">Kilka typów aplikacji oprogramowania Apache Cordova używać toohandle możliwości sprzężenia zwrotnego, które przepływu OAuth interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="22647-138">Several types of Apache Cordova applications use a loopback capability toohandle OAuth UI flows.</span></span>  <span data-ttu-id="22647-139">Przepływu OAuth interfejsu użytkownika na hoście lokalnym spowodować problemy, ponieważ usługa uwierzytelniania hello tylko wie jak tooutilize usługi domyślnie.</span><span class="sxs-lookup"><span data-stu-id="22647-139">OAuth UI flows on localhost cause problems since hello authentication service only knows how tooutilize your service by default.</span></span>  <span data-ttu-id="22647-140">Przykłady problematyczne przepływu OAuth interfejs użytkownika:</span><span class="sxs-lookup"><span data-stu-id="22647-140">Examples of problematic OAuth UI flows include:</span></span>

* <span data-ttu-id="22647-141">Hello Ripple emulator.</span><span class="sxs-lookup"><span data-stu-id="22647-141">hello Ripple emulator.</span></span>
* <span data-ttu-id="22647-142">Załaduj ponownie z Ionic na żywo.</span><span class="sxs-lookup"><span data-stu-id="22647-142">Live Reload with Ionic.</span></span>
* <span data-ttu-id="22647-143">Uruchomienie hello zaplecze aplikacji mobilnej lokalnie</span><span class="sxs-lookup"><span data-stu-id="22647-143">Running hello mobile backend locally</span></span>
* <span data-ttu-id="22647-144">Uruchomiona hello zaplecza aplikacji mobilnych w innej usłudze Azure App Service niż hello jeden zapewniający uwierzytelnianie.</span><span class="sxs-lookup"><span data-stu-id="22647-144">Running hello mobile backend in a different Azure App Service than hello one providing authentication.</span></span>

<span data-ttu-id="22647-145">Wykonaj te instrukcje tooadd toohello lokalnych ustawień konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="22647-145">Follow these instructions tooadd your local settings toohello configuration:</span></span>

1. <span data-ttu-id="22647-146">Zaloguj się za toohello [portalu Azure]</span><span class="sxs-lookup"><span data-stu-id="22647-146">Log in toohello [Azure portal]</span></span>
2. <span data-ttu-id="22647-147">Wybierz **wszystkie zasoby** lub **usługi aplikacji** następnie kliknij nazwę hello aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="22647-147">Select **All resources** or **App Services** then click hello name of your Mobile App.</span></span>
3. <span data-ttu-id="22647-148">Kliknij przycisk **narzędzia**</span><span class="sxs-lookup"><span data-stu-id="22647-148">Click **Tools**</span></span>
4. <span data-ttu-id="22647-149">Kliknij przycisk **Eksploratora zasobów** w hello OBSERVE menu, następnie kliknij przycisk **Przejdź**.</span><span class="sxs-lookup"><span data-stu-id="22647-149">Click **Resource explorer** in hello OBSERVE menu, then click **Go**.</span></span>  <span data-ttu-id="22647-150">Powoduje otwarcie nowego okna lub karty.</span><span class="sxs-lookup"><span data-stu-id="22647-150">A new window or tab opens.</span></span>
5. <span data-ttu-id="22647-151">Rozwiń węzeł hello **config**, **authsettings** węzłów witryny w nawigacji po lewej stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="22647-151">Expand hello **config**, **authsettings** nodes for your site in hello left-hand navigation.</span></span>
6. <span data-ttu-id="22647-152">Kliknij przycisk **edycji**</span><span class="sxs-lookup"><span data-stu-id="22647-152">Click **Edit**</span></span>
7. <span data-ttu-id="22647-153">Wyszukaj element "allowedExternalRedirectUrls" hello.</span><span class="sxs-lookup"><span data-stu-id="22647-153">Look for hello "allowedExternalRedirectUrls" element.</span></span>  <span data-ttu-id="22647-154">Może zostać ustawiony toonull lub tablicy wartości.</span><span class="sxs-lookup"><span data-stu-id="22647-154">It may be set toonull or an array of values.</span></span>  <span data-ttu-id="22647-155">Zmień toohello wartość hello następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="22647-155">Change hello value toohello following value:</span></span>

         "allowedExternalRedirectUrls": [
             "http://localhost:3000",
             "https://localhost:3000"
         ],

    <span data-ttu-id="22647-156">Zastąp adresy URL hello hello adresy URL usługi.</span><span class="sxs-lookup"><span data-stu-id="22647-156">Replace hello URLs with hello URLs of your service.</span></span>  <span data-ttu-id="22647-157">Przykładami "http://localhost: 3000" (dla hello usługi próbki Node.js) lub "http://localhost:4400" (dla usługi Ripple hello).</span><span class="sxs-lookup"><span data-stu-id="22647-157">Examples include "http://localhost:3000" (for hello Node.js sample service), or "http://localhost:4400" (for hello Ripple service).</span></span>  <span data-ttu-id="22647-158">Jednak te adresy URL są przykłady - sytuacji, w tym hello usług wymienionych w przykładach hello może się różnić.</span><span class="sxs-lookup"><span data-stu-id="22647-158">However, these URLs are examples - your situation, including for hello services mentioned in hello examples, may be different.</span></span>
8. <span data-ttu-id="22647-159">Kliknij przycisk hello **odczytu/zapisu** przycisku na powitania prawym górnym rogu ekranu hello.</span><span class="sxs-lookup"><span data-stu-id="22647-159">Click hello **Read/Write** button in hello top-right corner of hello screen.</span></span>
9. <span data-ttu-id="22647-160">Kliknij zielony hello **PUT** przycisku.</span><span class="sxs-lookup"><span data-stu-id="22647-160">Click hello green **PUT** button.</span></span>

<span data-ttu-id="22647-161">Ustawienia Hello są zapisywane w tym momencie.</span><span class="sxs-lookup"><span data-stu-id="22647-161">hello settings are saved at this point.</span></span>  <span data-ttu-id="22647-162">Nie zamykaj okna przeglądarki hello ustawienia hello ma zakończenie zapisywania.</span><span class="sxs-lookup"><span data-stu-id="22647-162">Do not close hello browser window until hello settings have finished saving.</span></span>
<span data-ttu-id="22647-163">Również dodać te ustawienia sprzężenia zwrotnego adresy URL toohello mechanizmu CORS usługi aplikacji:</span><span class="sxs-lookup"><span data-stu-id="22647-163">Also add these loopback URLs toohello CORS settings for your App Service:</span></span>

1. <span data-ttu-id="22647-164">Zaloguj się za toohello [portalu Azure]</span><span class="sxs-lookup"><span data-stu-id="22647-164">Log in toohello [Azure portal]</span></span>
2. <span data-ttu-id="22647-165">Wybierz **wszystkie zasoby** lub **usługi aplikacji** następnie kliknij nazwę hello aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="22647-165">Select **All resources** or **App Services** then click hello name of your Mobile App.</span></span>
3. <span data-ttu-id="22647-166">automatycznie zostanie otwarty blok ustawień Hello.</span><span class="sxs-lookup"><span data-stu-id="22647-166">hello Settings blade opens automatically.</span></span>  <span data-ttu-id="22647-167">Jeśli nie kliknij przycisk **wszystkie ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="22647-167">If it doesn't, click **All Settings**.</span></span>
4. <span data-ttu-id="22647-168">Kliknij przycisk **CORS** w menu hello interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="22647-168">Click **CORS** under hello API menu.</span></span>
5. <span data-ttu-id="22647-169">Wprowadź adres URL hello, która ma tooadd w polu hello, a następnie naciśnij klawisz Enter.</span><span class="sxs-lookup"><span data-stu-id="22647-169">Enter hello URL that you wish tooadd in hello box provided and press Enter.</span></span>
6. <span data-ttu-id="22647-170">Wprowadź dodatkowe adresy URL, zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="22647-170">Enter additional URLs as needed.</span></span>
7. <span data-ttu-id="22647-171">Kliknij przycisk **zapisać** toosave hello ustawienia.</span><span class="sxs-lookup"><span data-stu-id="22647-171">Click **Save** toosave hello settings.</span></span>

<span data-ttu-id="22647-172">Trwa około 10 – 15 sekund hello nowe ustawienia tootake efektu.</span><span class="sxs-lookup"><span data-stu-id="22647-172">It takes approximately 10-15 seconds for hello new settings tootake effect.</span></span>

## <span data-ttu-id="22647-173"><a name="register-for-push"></a>Porady: rejestrowanie do powiadomień wypychanych</span><span class="sxs-lookup"><span data-stu-id="22647-173"><a name="register-for-push"></a>How to: Register for push notifications</span></span>
<span data-ttu-id="22647-174">Zainstaluj hello [phonegap wtyczka wypychanie] toohandle powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="22647-174">Install hello [phonegap-plugin-push] toohandle push notifications.</span></span>  <span data-ttu-id="22647-175">Ten dodatek plug-in można łatwo dodać przy użyciu `cordova plugin add` polecenie w wierszu polecenia hello lub za pomocą Instalatora dodatku Git hello w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="22647-175">This plugin can be easily added using the `cordova plugin add` command on hello command line, or via hello Git plugin installer within Visual Studio.</span></span>  <span data-ttu-id="22647-176">Następujący kod w aplikacji platformy Apache Cordova rejestruje urządzenie dla powiadomień wypychanych:</span><span class="sxs-lookup"><span data-stu-id="22647-176">The following code in your Apache Cordova app registers your device for push notifications:</span></span>

```
var pushOptions = {
    android: {
        senderId: '<from-gcm-console>'
    },
    ios: {
        alert: true,
        badge: true,
        sound: true
    },
    windows: {
    }
};
pushHandler = PushNotification.init(pushOptions);

pushHandler.on('registration', function (data) {
    registrationId = data.registrationId;
    // For cross-platform, you can use hello device plugin toodetermine hello device
    // Best is toouse device.platform
    var name = 'gcm'; // For android - default
    if (device.platform.toLowerCase() === 'ios')
        name = 'apns';
    if (device.platform.toLowerCase().substring(0, 3) === 'win')
        name = 'wns';
    client.push.register(name, registrationId);
});

pushHandler.on('notification', function (data) {
    // data is an object and is whatever is sent by hello PNS - check hello format
    // for your particular PNS
});

pushHandler.on('error', function (error) {
    // Handle errors
});
```

<span data-ttu-id="22647-177">Za pomocą powiadomień wypychanych toosend hello zestaw SDK usługi Notification Hubs z powitania serwera.</span><span class="sxs-lookup"><span data-stu-id="22647-177">Use hello Notification Hubs SDK toosend push notifications from hello server.</span></span>  <span data-ttu-id="22647-178">Nigdy nie wysyłaj powiadomienia wypychane bezpośrednio od klientów.</span><span class="sxs-lookup"><span data-stu-id="22647-178">Never send push notifications directly from clients.</span></span> <span data-ttu-id="22647-179">Wykonanie tej dlatego może być używane tootrigger odmowa atak usługi Notification Hubs lub hello systemu powiadomień platformy.</span><span class="sxs-lookup"><span data-stu-id="22647-179">Doing so could be used tootrigger a denial of service attack against Notification Hubs or hello PNS.</span></span>  <span data-ttu-id="22647-180">Witaj systemu powiadomień platformy można zakaz ruchu wyniku takich ataków.</span><span class="sxs-lookup"><span data-stu-id="22647-180">hello PNS could ban your traffic as a result of such attacks.</span></span>

## <a name="more-information"></a><span data-ttu-id="22647-181">Więcej informacji</span><span class="sxs-lookup"><span data-stu-id="22647-181">More information</span></span>

<span data-ttu-id="22647-182">Można znaleźć szczegółowe szczegóły interfejsu API w naszym [dokumentacji interfejsu API](http://azure.github.io/azure-mobile-apps-js-client/).</span><span class="sxs-lookup"><span data-stu-id="22647-182">You can find detailed API details in our [API documentation](http://azure.github.io/azure-mobile-apps-js-client/).</span></span>

<!-- URLs. -->
[portalu Azure]: https://portal.azure.com
[Azure Mobile Apps Szybki Start]: app-service-mobile-cordova-get-started.md
[Rozpoczynanie pracy z uwierzytelnianiem]: app-service-mobile-cordova-get-started-users.md
[Add authentication tooyour app]: app-service-mobile-cordova-get-started-users.md

[Apache wtyczki Cordova dla usługi Azure Mobile Apps]: https://www.npmjs.com/package/cordova-plugin-ms-azure-mobile-apps
[pierwszej aplikacji platformy Apache Cordova]: http://cordova.apache.org/#getstarted
[phonegap-facebook-plugin]: https://github.com/wizcorp/phonegap-facebook-plugin
[phonegap wtyczka wypychanie]: https://www.npmjs.com/package/phonegap-plugin-push
[cordova wtyczka urządzenie]: https://www.npmjs.com/package/cordova-plugin-device
[cordova wtyczka inappbrowser]: https://www.npmjs.com/package/cordova-plugin-inappbrowser
[Query object documentation]: https://msdn.microsoft.com/en-us/library/azure/jj613353.aspx
