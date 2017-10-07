---
title: "Witaj tooUse aaaHow JavaScript SDK usługi Azure Mobile Apps"
description: "Jak v tooUse usługi Azure Mobile Apps"
services: app-service\mobile
documentationcenter: javascript
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 53b78965-caa3-4b22-bb67-5bd5c19d03c4
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: html
ms.devlang: javascript
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: 3fcbb0c5bd6918a285bdafa1946ba0bd47bb21b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-javascript-client-library-for-azure-mobile-apps"></a>Jak tooUse hello biblioteki klienckiej JavaScript dla usługi Azure Mobile Apps
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

Ten przewodnik zawiera wskazówki, tooperform typowych scenariuszy przy użyciu hello najnowszych [JavaScript SDK usługi Azure Mobile Apps]. W przypadku nowych aplikacji mobilnej tooAzure najpierw zakończyć [Azure Mobile Apps Szybki Start] toocreate wewnętrznej bazie danych i Utwórz tabelę. W tym przewodniku możemy skupić się na przy użyciu zaplecza aplikacji mobilnych hello w aplikacji sieci Web HTML/JavaScript.

## <a name="supported-platforms"></a>Obsługiwane platformy
Firma Microsoft ograniczyć bieżącego toohello Obsługa przeglądarki i ostatniej wersji hello główne przeglądarki: Google Chrome, Microsoft Edge, programu Microsoft Internet Explorer i Mozilla Firefox.  Oczekujemy hello toofunction zestawu SDK z dowolnej stosunkowo nowoczesne przeglądarki.

Hello pakiet jest dystrybuowany jako moduł uniwersalnych JavaScript, więc CommonJS formaty i obsługuje zmienne globalne, AMD.

## <a name="Setup"></a>Instalacji i wymagania wstępne
W tym przewodniku założono, że utworzono wewnętrznej bazie danych z tabeli. W tym przewodniku założono tabeli hello ma hello tego samego schematu jako tabele hello w tych samouczkach.

Instalowanie hello zestaw SDK usługi Azure Mobile Apps JavaScript może odbywać się za pośrednictwem hello `npm` polecenia:

```
npm install azure-mobile-apps-client --save
```

Biblioteka Hello mogą służyć jako moduł ES2015 w środowiskach CommonJS, takie jak Browserify i Webpack i jako biblioteki AMD.  Na przykład:

```
# For ECMAScript 5.1 CommonJS
var WindowsAzure = require('azure-mobile-apps-client');
# For ES2015 modules
import * as WindowsAzure from 'azure-mobile-apps-client';
```

Można także użyć wbudowanych wersji hello zestawu SDK, pobierając bezpośrednio z naszych CDN:

```html
<script src="https://zumo.blob.core.windows.net/sdk/azure-mobile-apps-client.min.js"></script>
```

[!INCLUDE [app-service-mobile-html-js-library](../../includes/app-service-mobile-html-js-library.md)]

## <a name="auth"></a>Porady: uwierzytelnianie użytkowników
Usługa aplikacji Azure obsługuje uwierzytelniania i autoryzacji użytkowników aplikacji przy użyciu różnych dostawców tożsamości zewnętrznych: Facebook, Google, Microsoft Account i Twitter. Możesz ustawić uprawnienia na dostęp do tabel toorestrict dla określonych operacji tooonly uwierzytelnieni użytkownicy. Umożliwia także tożsamości hello reguł autoryzacji użytkowników uwierzytelnionych tooimplement w skryptach serwera. Aby uzyskać więcej informacji, zobacz hello [Rozpoczynanie pracy z uwierzytelnianiem] samouczka.

Obsługiwane są dwa przepływy uwierzytelniania: przepływu serwera i klienta przepływu.  powitania serwera przepływu zapewnia hello najprostszym uwierzytelniania, ponieważ zależy od interfejsu uwierzytelniania sieci web dostawcy hello. Witaj przepływu klienta umożliwia lepsza integracja z możliwości specyficznych dla urządzeń takich jak single-sign-on, ponieważ zależy od określonego dostawcy SDK.

[!INCLUDE [app-service-mobile-html-js-auth-library](../../includes/app-service-mobile-html-js-auth-library.md)]

### <a name="configure-external-redirect-urls"></a>Porady: Konfigurowanie usługi Mobile App Service dla adresy URL przekierowań zewnętrznych.
Kilka typów aplikacji JavaScript Użyj toohandle możliwości sprzężenia zwrotnego, które przepływu OAuth interfejsu użytkownika.  Te możliwości to m.in.:

* Usługą lokalnie
* Przy użyciu przeładowania na żywo z hello jonowych Framework
* Przekierowywanie tooApp usługi uwierzytelniania.

Uruchomiony lokalnie może spowodować problemy, ponieważ domyślnie jest tylko uwierzytelnianie usługi aplikacji skonfigurowany dostęp tooallow z zaplecza aplikacji mobilnej. Użyj hello następujące kroki toochange hello uwierzytelniania tooenable ustawienia usługi aplikacji podczas uruchamiania lokalnego serwera hello:

1. Zaloguj się za toohello [portalu Azure]
2. Przejdź tooyour zaplecza aplikacji mobilnej.
3. Wybierz **Eksploratora zasobów** w hello **narzędzi PROGRAMISTYCZNYCH** menu.
4. Kliknij przycisk **Przejdź** Eksploratora zasobów hello tooopen dla zaplecza aplikacji mobilnej w nowej karcie lub w oknie.
5. Rozwiń węzeł hello **config** > **authsettings** węzła dla aplikacji.
6. Kliknij przycisk hello **Edytuj** przycisk tooenable edycji hello zasobu.
7. Znajdź hello **allowedExternalRedirectUrls** element, który może mieć wartości null. Dodaj adresami URL w tablicy:

         "allowedExternalRedirectUrls": [
             "http://localhost:3000",
             "https://localhost:3000"
         ],

    Zamień adresy URL hello w tablicy hello hello adresy URL usługi, który w tym przykładzie jest `http://localhost:3000` hello lokalnej usługi próbki Node.js. Można także użyć `http://localhost:4400` hello Ripple usługi lub innych URL, w zależności od sposobu skonfigurowania aplikacji.
8. U góry hello hello strony, kliknij przycisk **odczytu/zapisu**, następnie kliknij przycisk **PUT** toosave aktualizacji.

Należy również tooadd hello tych samych ustawień listy dozwolonych CORS toohello sprzężenia zwrotnego adresów URL:

1. Przejdź wstecz toohello [portalu Azure].
2. Przejdź tooyour zaplecza aplikacji mobilnej.
3. Kliknij przycisk **CORS** w hello **interfejsu API** menu.
4. Wprowadź każdy adres URL w hello pusty **dozwolone źródła** pola tekstowego.  Utworzono nowe pole tekstowe.
5. Kliknij przycisk **ZAPISZ**

Po aktualizacji hello wewnętrznej bazy danych, będzie możliwe toouse hello nowym adresem URL sprzężenia zwrotnego w aplikacji.

<!-- URLs. -->
[Start Azure szybkie aplikacji mobilnych]: app-service-mobile-cordova-get-started.md
[Wprowadzenie do uwierzytelniania]: app-service-mobile-cordova-get-started-users.md
[Add authentication tooyour app]: app-service-mobile-cordova-get-started-users.md

[Witryna Azure Portal]: https://portal.azure.com/
[Zestaw SDK JavaScript dla usługi Azure Mobile Apps]: https://www.npmjs.com/package/azure-mobile-apps-client
[Query object documentation]: https://msdn.microsoft.com/en-us/library/azure/jj613353.aspx
