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
# <a name="how-toouse-apache-cordova-client-library-for-azure-mobile-apps"></a>Jak toouse Apache Cordova klienta biblioteki usługi Azure Mobile Apps
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

Ten przewodnik zawiera wskazówki, tooperform typowych scenariuszy przy użyciu hello najnowszych [Apache wtyczki Cordova dla usługi Azure Mobile Apps]. W przypadku nowych aplikacji mobilnej tooAzure najpierw zakończyć [Azure Mobile Apps Szybki Start] toocreate zaplecza, Utwórz tabelę i Pobierz wstępnie skompilowanym projektem Apache Cordova. W tym przewodniku, możemy skupić się na powitania klienta wtyczki programu Apache Cordova.

## <a name="supported-platforms"></a>Obsługiwane platformy
Zestaw SDK obsługuje Apache Cordova 6.0.0 i później z systemem iOS, Android i Windows urządzeń.  Obsługa platform Hello jest następujący:

* Interfejs API systemu android 19 – 24 (KitKat za pośrednictwem nugacie).
* System iOS w wersji 8.0 lub nowszej.
* Windows Phone 8.1.
* Platforma uniwersalna systemu Windows.

## <a name="Setup"></a>Instalacji i wymagania wstępne
W tym przewodniku założono, że utworzono wewnętrznej bazie danych z tabeli. W tym przewodniku założono tabeli hello ma hello tego samego schematu jako tabele hello w tych samouczkach. W tym przewodniku założono również, dodano hello wtyczki Cordova Apache tooyour kodu.  Jeśli użytkownik nie zostało zrobione, można dodać projektu tooyour wtyczki oprogramowania Apache Cordova hello hello w wierszu polecenia:

```
cordova plugin add cordova-plugin-ms-azure-mobile-apps
```

Aby uzyskać więcej informacji na temat tworzenia [pierwszej aplikacji platformy Apache Cordova], ich w dokumentacji.

## <a name="ionic"></a>Konfigurowanie aplikacji jonowych v2

tooproperly Konfigurowanie projektu jonowych v2 najpierw utworzyć podstawową aplikację i dodawanie wtyczki Cordova hello:

```
ionic start projectName --v2
cd projectName
ionic plugin add cordova-plugin-ms-azure-mobile-apps
```

Dodaj następujące wiersze zbyt hello`app.component.ts` toocreate powitania klienta obiektu:

```
declare var WindowsAzure: any;
var client = new WindowsAzure.MobileServiceClient("https://yoursite.azurewebsites.net");
```

Można teraz skompilować i uruchomić projekt hello w przeglądarce hello:

```
ionic platform add browser
ionic run browser
```

Witaj wtyczkę Azure Mobile Apps Cordova obsługuje zarówno jonowych aplikacje v1 i v2.  Tylko aplikacje hello jonowych v2 wymagają dodatkowych deklaracji dla hello `WindowsAzure` obiektu.

[!INCLUDE [app-service-mobile-html-js-library.md](../../includes/app-service-mobile-html-js-library.md)]

## <a name="auth"></a>Porady: uwierzytelnianie użytkowników
Usługa aplikacji Azure obsługuje uwierzytelniania i autoryzacji użytkowników aplikacji przy użyciu różnych dostawców tożsamości zewnętrznych: Facebook, Google, Microsoft Account i Twitter. Możesz ustawić uprawnienia na dostęp do tabel toorestrict dla określonych operacji tooonly uwierzytelnieni użytkownicy. Umożliwia także tożsamości hello reguł autoryzacji użytkowników uwierzytelnionych tooimplement w skryptach serwera. Aby uzyskać więcej informacji, zobacz hello [Rozpoczynanie pracy z uwierzytelnianiem] samouczka.

Korzystając z uwierzytelniania w aplikacji oprogramowania Apache Cordova, hello następujące wtyczki Cordova muszą być dostępne:

* [cordova wtyczka urządzenie]
* [cordova wtyczka inappbrowser]

Obsługiwane są dwa przepływy uwierzytelniania: przepływu serwera i klienta przepływu.  powitania serwera przepływu zapewnia hello najprostszym uwierzytelniania, ponieważ zależy od interfejsu uwierzytelniania sieci web dostawcy hello. Witaj przepływu klienta umożliwia lepsza integracja z możliwości specyficznych dla urządzeń takich jak single-sign-on jako opiera się na zestawy SDK urządzenia specyficznego dla dostawcy.

[!INCLUDE [app-service-mobile-html-js-auth-library.md](../../includes/app-service-mobile-html-js-auth-library.md)]

### <a name="configure-external-redirect-urls"></a>Porady: Konfigurowanie usługi Mobile App Service dla adresy URL przekierowań zewnętrznych.
Kilka typów aplikacji oprogramowania Apache Cordova używać toohandle możliwości sprzężenia zwrotnego, które przepływu OAuth interfejsu użytkownika.  Przepływu OAuth interfejsu użytkownika na hoście lokalnym spowodować problemy, ponieważ usługa uwierzytelniania hello tylko wie jak tooutilize usługi domyślnie.  Przykłady problematyczne przepływu OAuth interfejs użytkownika:

* Hello Ripple emulator.
* Załaduj ponownie z Ionic na żywo.
* Uruchomienie hello zaplecze aplikacji mobilnej lokalnie
* Uruchomiona hello zaplecza aplikacji mobilnych w innej usłudze Azure App Service niż hello jeden zapewniający uwierzytelnianie.

Wykonaj te instrukcje tooadd toohello lokalnych ustawień konfiguracji:

1. Zaloguj się za toohello [portalu Azure]
2. Wybierz **wszystkie zasoby** lub **usługi aplikacji** następnie kliknij nazwę hello aplikacji mobilnej.
3. Kliknij przycisk **narzędzia**
4. Kliknij przycisk **Eksploratora zasobów** w hello OBSERVE menu, następnie kliknij przycisk **Przejdź**.  Powoduje otwarcie nowego okna lub karty.
5. Rozwiń węzeł hello **config**, **authsettings** węzłów witryny w nawigacji po lewej stronie powitania.
6. Kliknij przycisk **edycji**
7. Wyszukaj element "allowedExternalRedirectUrls" hello.  Może zostać ustawiony toonull lub tablicy wartości.  Zmień toohello wartość hello następujące wartości:

         "allowedExternalRedirectUrls": [
             "http://localhost:3000",
             "https://localhost:3000"
         ],

    Zastąp adresy URL hello hello adresy URL usługi.  Przykładami "http://localhost: 3000" (dla hello usługi próbki Node.js) lub "http://localhost:4400" (dla usługi Ripple hello).  Jednak te adresy URL są przykłady - sytuacji, w tym hello usług wymienionych w przykładach hello może się różnić.
8. Kliknij przycisk hello **odczytu/zapisu** przycisku na powitania prawym górnym rogu ekranu hello.
9. Kliknij zielony hello **PUT** przycisku.

Ustawienia Hello są zapisywane w tym momencie.  Nie zamykaj okna przeglądarki hello ustawienia hello ma zakończenie zapisywania.
Również dodać te ustawienia sprzężenia zwrotnego adresy URL toohello mechanizmu CORS usługi aplikacji:

1. Zaloguj się za toohello [portalu Azure]
2. Wybierz **wszystkie zasoby** lub **usługi aplikacji** następnie kliknij nazwę hello aplikacji mobilnej.
3. automatycznie zostanie otwarty blok ustawień Hello.  Jeśli nie kliknij przycisk **wszystkie ustawienia**.
4. Kliknij przycisk **CORS** w menu hello interfejsu API.
5. Wprowadź adres URL hello, która ma tooadd w polu hello, a następnie naciśnij klawisz Enter.
6. Wprowadź dodatkowe adresy URL, zgodnie z potrzebami.
7. Kliknij przycisk **zapisać** toosave hello ustawienia.

Trwa około 10 – 15 sekund hello nowe ustawienia tootake efektu.

## <a name="register-for-push"></a>Porady: rejestrowanie do powiadomień wypychanych
Zainstaluj hello [phonegap wtyczka wypychanie] toohandle powiadomień wypychanych.  Ten dodatek plug-in można łatwo dodać przy użyciu `cordova plugin add` polecenie w wierszu polecenia hello lub za pomocą Instalatora dodatku Git hello w programie Visual Studio.  Następujący kod w aplikacji platformy Apache Cordova rejestruje urządzenie dla powiadomień wypychanych:

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

Za pomocą powiadomień wypychanych toosend hello zestaw SDK usługi Notification Hubs z powitania serwera.  Nigdy nie wysyłaj powiadomienia wypychane bezpośrednio od klientów. Wykonanie tej dlatego może być używane tootrigger odmowa atak usługi Notification Hubs lub hello systemu powiadomień platformy.  Witaj systemu powiadomień platformy można zakaz ruchu wyniku takich ataków.

## <a name="more-information"></a>Więcej informacji

Można znaleźć szczegółowe szczegóły interfejsu API w naszym [dokumentacji interfejsu API](http://azure.github.io/azure-mobile-apps-js-client/).

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
