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
# <a name="how-toouse-hello-javascript-client-library-for-azure-mobile-apps"></a><span data-ttu-id="f4521-103">Jak tooUse hello biblioteki klienckiej JavaScript dla usługi Azure Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="f4521-103">How tooUse hello JavaScript client library for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

<span data-ttu-id="f4521-104">Ten przewodnik zawiera wskazówki, tooperform typowych scenariuszy przy użyciu hello najnowszych [JavaScript SDK usługi Azure Mobile Apps].</span><span class="sxs-lookup"><span data-stu-id="f4521-104">This guide teaches you tooperform common scenarios using hello latest [JavaScript SDK for Azure Mobile Apps].</span></span> <span data-ttu-id="f4521-105">W przypadku nowych aplikacji mobilnej tooAzure najpierw zakończyć [Azure Mobile Apps Szybki Start] toocreate wewnętrznej bazie danych i Utwórz tabelę.</span><span class="sxs-lookup"><span data-stu-id="f4521-105">If you are new tooAzure Mobile Apps, first complete [Azure Mobile Apps Quick Start] toocreate a backend and create a table.</span></span> <span data-ttu-id="f4521-106">W tym przewodniku możemy skupić się na przy użyciu zaplecza aplikacji mobilnych hello w aplikacji sieci Web HTML/JavaScript.</span><span class="sxs-lookup"><span data-stu-id="f4521-106">In this guide, we focus on using hello mobile backend in HTML/JavaScript Web applications.</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="f4521-107">Obsługiwane platformy</span><span class="sxs-lookup"><span data-stu-id="f4521-107">Supported platforms</span></span>
<span data-ttu-id="f4521-108">Firma Microsoft ograniczyć bieżącego toohello Obsługa przeglądarki i ostatniej wersji hello główne przeglądarki: Google Chrome, Microsoft Edge, programu Microsoft Internet Explorer i Mozilla Firefox.</span><span class="sxs-lookup"><span data-stu-id="f4521-108">We limit browser support toohello current and last versions of hello major browsers:  Google Chrome, Microsoft Edge, Microsoft Internet Explorer, and Mozilla Firefox.</span></span>  <span data-ttu-id="f4521-109">Oczekujemy hello toofunction zestawu SDK z dowolnej stosunkowo nowoczesne przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="f4521-109">We expect hello SDK toofunction with any relatively modern browser.</span></span>

<span data-ttu-id="f4521-110">Hello pakiet jest dystrybuowany jako moduł uniwersalnych JavaScript, więc CommonJS formaty i obsługuje zmienne globalne, AMD.</span><span class="sxs-lookup"><span data-stu-id="f4521-110">hello package is distributed as a Universal JavaScript Module, so it supports globals, AMD, and CommonJS formats.</span></span>

## <span data-ttu-id="f4521-111"><a name="Setup"></a>Instalacji i wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f4521-111"><a name="Setup"></a>Setup and prerequisites</span></span>
<span data-ttu-id="f4521-112">W tym przewodniku założono, że utworzono wewnętrznej bazie danych z tabeli.</span><span class="sxs-lookup"><span data-stu-id="f4521-112">This guide assumes that you have created a backend with a table.</span></span> <span data-ttu-id="f4521-113">W tym przewodniku założono tabeli hello ma hello tego samego schematu jako tabele hello w tych samouczkach.</span><span class="sxs-lookup"><span data-stu-id="f4521-113">This guide assumes that hello table has hello same schema as hello tables in those tutorials.</span></span>

<span data-ttu-id="f4521-114">Instalowanie hello zestaw SDK usługi Azure Mobile Apps JavaScript może odbywać się za pośrednictwem hello `npm` polecenia:</span><span class="sxs-lookup"><span data-stu-id="f4521-114">Installing hello Azure Mobile Apps JavaScript SDK can be done via hello `npm` command:</span></span>

```
npm install azure-mobile-apps-client --save
```

<span data-ttu-id="f4521-115">Biblioteka Hello mogą służyć jako moduł ES2015 w środowiskach CommonJS, takie jak Browserify i Webpack i jako biblioteki AMD.</span><span class="sxs-lookup"><span data-stu-id="f4521-115">hello library can also be used as an ES2015 module, within CommonJS environments such as Browserify and Webpack and as an AMD library.</span></span>  <span data-ttu-id="f4521-116">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="f4521-116">For example:</span></span>

```
# For ECMAScript 5.1 CommonJS
var WindowsAzure = require('azure-mobile-apps-client');
# For ES2015 modules
import * as WindowsAzure from 'azure-mobile-apps-client';
```

<span data-ttu-id="f4521-117">Można także użyć wbudowanych wersji hello zestawu SDK, pobierając bezpośrednio z naszych CDN:</span><span class="sxs-lookup"><span data-stu-id="f4521-117">You can also use a pre-built version of hello SDK by downloading directly from our CDN:</span></span>

```html
<script src="https://zumo.blob.core.windows.net/sdk/azure-mobile-apps-client.min.js"></script>
```

[!INCLUDE [app-service-mobile-html-js-library](../../includes/app-service-mobile-html-js-library.md)]

## <span data-ttu-id="f4521-118"><a name="auth"></a>Porady: uwierzytelnianie użytkowników</span><span class="sxs-lookup"><span data-stu-id="f4521-118"><a name="auth"></a>How to: Authenticate users</span></span>
<span data-ttu-id="f4521-119">Usługa aplikacji Azure obsługuje uwierzytelniania i autoryzacji użytkowników aplikacji przy użyciu różnych dostawców tożsamości zewnętrznych: Facebook, Google, Microsoft Account i Twitter.</span><span class="sxs-lookup"><span data-stu-id="f4521-119">Azure App Service supports authenticating and authorizing app users using various external identity providers: Facebook, Google, Microsoft Account, and Twitter.</span></span> <span data-ttu-id="f4521-120">Możesz ustawić uprawnienia na dostęp do tabel toorestrict dla określonych operacji tooonly uwierzytelnieni użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="f4521-120">You can set permissions on tables toorestrict access for specific operations tooonly authenticated users.</span></span> <span data-ttu-id="f4521-121">Umożliwia także tożsamości hello reguł autoryzacji użytkowników uwierzytelnionych tooimplement w skryptach serwera.</span><span class="sxs-lookup"><span data-stu-id="f4521-121">You can also use hello identity of authenticated users tooimplement authorization rules in server scripts.</span></span> <span data-ttu-id="f4521-122">Aby uzyskać więcej informacji, zobacz hello [Rozpoczynanie pracy z uwierzytelnianiem] samouczka.</span><span class="sxs-lookup"><span data-stu-id="f4521-122">For more information, see hello [Get started with authentication] tutorial.</span></span>

<span data-ttu-id="f4521-123">Obsługiwane są dwa przepływy uwierzytelniania: przepływu serwera i klienta przepływu.</span><span class="sxs-lookup"><span data-stu-id="f4521-123">Two authentication flows are supported: a server flow and a client flow.</span></span>  <span data-ttu-id="f4521-124">powitania serwera przepływu zapewnia hello najprostszym uwierzytelniania, ponieważ zależy od interfejsu uwierzytelniania sieci web dostawcy hello.</span><span class="sxs-lookup"><span data-stu-id="f4521-124">hello server flow provides hello simplest authentication experience, as it relies on hello provider's web authentication interface.</span></span> <span data-ttu-id="f4521-125">Witaj przepływu klienta umożliwia lepsza integracja z możliwości specyficznych dla urządzeń takich jak single-sign-on, ponieważ zależy od określonego dostawcy SDK.</span><span class="sxs-lookup"><span data-stu-id="f4521-125">hello client flow allows for deeper integration with device-specific capabilities such as single-sign-on as it relies on provider-specific SDKs.</span></span>

[!INCLUDE [app-service-mobile-html-js-auth-library](../../includes/app-service-mobile-html-js-auth-library.md)]

### <span data-ttu-id="f4521-126"><a name="configure-external-redirect-urls"></a>Porady: Konfigurowanie usługi Mobile App Service dla adresy URL przekierowań zewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="f4521-126"><a name="configure-external-redirect-urls"></a>How to: Configure your Mobile App Service for external redirect URLs.</span></span>
<span data-ttu-id="f4521-127">Kilka typów aplikacji JavaScript Użyj toohandle możliwości sprzężenia zwrotnego, które przepływu OAuth interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="f4521-127">Several types of JavaScript applications use a loopback capability toohandle OAuth UI flows.</span></span>  <span data-ttu-id="f4521-128">Te możliwości to m.in.:</span><span class="sxs-lookup"><span data-stu-id="f4521-128">These capabilities include:</span></span>

* <span data-ttu-id="f4521-129">Usługą lokalnie</span><span class="sxs-lookup"><span data-stu-id="f4521-129">Running your service locally</span></span>
* <span data-ttu-id="f4521-130">Przy użyciu przeładowania na żywo z hello jonowych Framework</span><span class="sxs-lookup"><span data-stu-id="f4521-130">Using Live Reload with hello Ionic Framework</span></span>
* <span data-ttu-id="f4521-131">Przekierowywanie tooApp usługi uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="f4521-131">Redirecting tooApp Service for authentication.</span></span>

<span data-ttu-id="f4521-132">Uruchomiony lokalnie może spowodować problemy, ponieważ domyślnie jest tylko uwierzytelnianie usługi aplikacji skonfigurowany dostęp tooallow z zaplecza aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="f4521-132">Running locally can cause problems because, by default, App Service authentication is only configured tooallow access from your Mobile App backend.</span></span> <span data-ttu-id="f4521-133">Użyj hello następujące kroki toochange hello uwierzytelniania tooenable ustawienia usługi aplikacji podczas uruchamiania lokalnego serwera hello:</span><span class="sxs-lookup"><span data-stu-id="f4521-133">Use hello following steps toochange hello App Service settings tooenable authentication when running hello server locally:</span></span>

1. <span data-ttu-id="f4521-134">Zaloguj się za toohello [portalu Azure]</span><span class="sxs-lookup"><span data-stu-id="f4521-134">Log in toohello [Azure portal]</span></span>
2. <span data-ttu-id="f4521-135">Przejdź tooyour zaplecza aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="f4521-135">Navigate tooyour Mobile App backend.</span></span>
3. <span data-ttu-id="f4521-136">Wybierz **Eksploratora zasobów** w hello **narzędzi PROGRAMISTYCZNYCH** menu.</span><span class="sxs-lookup"><span data-stu-id="f4521-136">Select **Resource explorer** in hello **DEVELOPMENT TOOLS** menu.</span></span>
4. <span data-ttu-id="f4521-137">Kliknij przycisk **Przejdź** Eksploratora zasobów hello tooopen dla zaplecza aplikacji mobilnej w nowej karcie lub w oknie.</span><span class="sxs-lookup"><span data-stu-id="f4521-137">Click **Go** tooopen hello resource explorer for your Mobile App backend in a new tab or window.</span></span>
5. <span data-ttu-id="f4521-138">Rozwiń węzeł hello **config** > **authsettings** węzła dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f4521-138">Expand hello **config** > **authsettings** node for your app.</span></span>
6. <span data-ttu-id="f4521-139">Kliknij przycisk hello **Edytuj** przycisk tooenable edycji hello zasobu.</span><span class="sxs-lookup"><span data-stu-id="f4521-139">Click hello **Edit** button tooenable editing of hello resource.</span></span>
7. <span data-ttu-id="f4521-140">Znajdź hello **allowedExternalRedirectUrls** element, który może mieć wartości null.</span><span class="sxs-lookup"><span data-stu-id="f4521-140">Find hello **allowedExternalRedirectUrls** element, which should be null.</span></span> <span data-ttu-id="f4521-141">Dodaj adresami URL w tablicy:</span><span class="sxs-lookup"><span data-stu-id="f4521-141">Add your URLs in an array:</span></span>

         "allowedExternalRedirectUrls": [
             "http://localhost:3000",
             "https://localhost:3000"
         ],

    <span data-ttu-id="f4521-142">Zamień adresy URL hello w tablicy hello hello adresy URL usługi, który w tym przykładzie jest `http://localhost:3000` hello lokalnej usługi próbki Node.js.</span><span class="sxs-lookup"><span data-stu-id="f4521-142">Replace hello URLs in hello array with hello URLs of your service, which in this example is `http://localhost:3000` for hello local Node.js sample service.</span></span> <span data-ttu-id="f4521-143">Można także użyć `http://localhost:4400` hello Ripple usługi lub innych URL, w zależności od sposobu skonfigurowania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f4521-143">You could also use `http://localhost:4400` for hello Ripple service or some other URL, depending on how your app is configured.</span></span>
8. <span data-ttu-id="f4521-144">U góry hello hello strony, kliknij przycisk **odczytu/zapisu**, następnie kliknij przycisk **PUT** toosave aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="f4521-144">At hello top of hello page, click **Read/Write**, then click **PUT** toosave your updates.</span></span>

<span data-ttu-id="f4521-145">Należy również tooadd hello tych samych ustawień listy dozwolonych CORS toohello sprzężenia zwrotnego adresów URL:</span><span class="sxs-lookup"><span data-stu-id="f4521-145">You also need tooadd hello same loopback URLs toohello CORS whitelist settings:</span></span>

1. <span data-ttu-id="f4521-146">Przejdź wstecz toohello [portalu Azure].</span><span class="sxs-lookup"><span data-stu-id="f4521-146">Navigate back toohello [Azure portal].</span></span>
2. <span data-ttu-id="f4521-147">Przejdź tooyour zaplecza aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="f4521-147">Navigate tooyour Mobile App backend.</span></span>
3. <span data-ttu-id="f4521-148">Kliknij przycisk **CORS** w hello **interfejsu API** menu.</span><span class="sxs-lookup"><span data-stu-id="f4521-148">Click **CORS** in hello **API** menu.</span></span>
4. <span data-ttu-id="f4521-149">Wprowadź każdy adres URL w hello pusty **dozwolone źródła** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="f4521-149">Enter each URL in hello empty **Allowed Origins** text box.</span></span>  <span data-ttu-id="f4521-150">Utworzono nowe pole tekstowe.</span><span class="sxs-lookup"><span data-stu-id="f4521-150">A new text box is created.</span></span>
5. <span data-ttu-id="f4521-151">Kliknij przycisk **ZAPISZ**</span><span class="sxs-lookup"><span data-stu-id="f4521-151">Click **SAVE**</span></span>

<span data-ttu-id="f4521-152">Po aktualizacji hello wewnętrznej bazy danych, będzie możliwe toouse hello nowym adresem URL sprzężenia zwrotnego w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f4521-152">After hello backend updates, you will be able toouse hello new loopback URLs in your app.</span></span>

<!-- URLs. -->
[Start Azure szybkie aplikacji mobilnych]: app-service-mobile-cordova-get-started.md
[Wprowadzenie do uwierzytelniania]: app-service-mobile-cordova-get-started-users.md
[Add authentication tooyour app]: app-service-mobile-cordova-get-started-users.md

[Witryna Azure Portal]: https://portal.azure.com/
[Zestaw SDK JavaScript dla usługi Azure Mobile Apps]: https://www.npmjs.com/package/azure-mobile-apps-client
[Query object documentation]: https://msdn.microsoft.com/en-us/library/azure/jj613353.aspx
