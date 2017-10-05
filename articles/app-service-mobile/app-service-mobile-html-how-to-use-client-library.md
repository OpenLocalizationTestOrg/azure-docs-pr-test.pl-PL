---
title: "Jak używać zestawu JavaScript SDK usługi Azure Mobile Apps"
description: "Sposób użycia v usługi Azure Mobile Apps"
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
ms.openlocfilehash: 0c4b4de560d70592f5bbdee28b56a7686b5689f4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-the-javascript-client-library-for-azure-mobile-apps"></a><span data-ttu-id="b9358-103">Jak używać biblioteki klienckiej JavaScript w usłudze Azure Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="b9358-103">How to Use the JavaScript client library for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

<span data-ttu-id="b9358-104">Ten przewodnik zawiera wskazówki do wykonywania typowych scenariuszy przy użyciu najnowszych [JavaScript SDK usługi Azure Mobile Apps].</span><span class="sxs-lookup"><span data-stu-id="b9358-104">This guide teaches you to perform common scenarios using the latest [JavaScript SDK for Azure Mobile Apps].</span></span> <span data-ttu-id="b9358-105">Jeśli jesteś nowym użytkownikiem usługi Azure Mobile Apps, najpierw wykonać [Azure Mobile Apps Szybki Start] tworzenie zaplecza i Utwórz tabelę.</span><span class="sxs-lookup"><span data-stu-id="b9358-105">If you are new to Azure Mobile Apps, first complete [Azure Mobile Apps Quick Start] to create a backend and create a table.</span></span> <span data-ttu-id="b9358-106">W tym przewodniku możemy skupić się na przy użyciu zaplecza aplikacji mobilnych w aplikacji sieci Web HTML/JavaScript.</span><span class="sxs-lookup"><span data-stu-id="b9358-106">In this guide, we focus on using the mobile backend in HTML/JavaScript Web applications.</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="b9358-107">Obsługiwane platformy</span><span class="sxs-lookup"><span data-stu-id="b9358-107">Supported platforms</span></span>
<span data-ttu-id="b9358-108">Ograniczona obsługa przeglądarek do wersji bieżącej i ostatni główne przeglądarki: Google Chrome, Microsoft Edge, programu Microsoft Internet Explorer i Mozilla Firefox.</span><span class="sxs-lookup"><span data-stu-id="b9358-108">We limit browser support to the current and last versions of the major browsers:  Google Chrome, Microsoft Edge, Microsoft Internet Explorer, and Mozilla Firefox.</span></span>  <span data-ttu-id="b9358-109">Przewidujemy, zestawu SDK do funkcji ze względnie nowoczesne przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="b9358-109">We expect the SDK to function with any relatively modern browser.</span></span>

<span data-ttu-id="b9358-110">Pakiet jest dystrybuowany jako moduł uniwersalnych JavaScript tak CommonJS formaty i obsługuje zmienne globalne, AMD.</span><span class="sxs-lookup"><span data-stu-id="b9358-110">The package is distributed as a Universal JavaScript Module, so it supports globals, AMD, and CommonJS formats.</span></span>

## <span data-ttu-id="b9358-111"><a name="Setup"></a>Instalacji i wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="b9358-111"><a name="Setup"></a>Setup and prerequisites</span></span>
<span data-ttu-id="b9358-112">W tym przewodniku założono, że utworzono wewnętrznej bazie danych z tabeli.</span><span class="sxs-lookup"><span data-stu-id="b9358-112">This guide assumes that you have created a backend with a table.</span></span> <span data-ttu-id="b9358-113">W tym przewodniku założono, że tabela ma ten sam schemat jako tabele w tych samouczkach.</span><span class="sxs-lookup"><span data-stu-id="b9358-113">This guide assumes that the table has the same schema as the tables in those tutorials.</span></span>

<span data-ttu-id="b9358-114">Instalowanie zestawu SDK usługi Azure Mobile Apps JavaScript może odbywać się za pośrednictwem `npm` polecenia:</span><span class="sxs-lookup"><span data-stu-id="b9358-114">Installing the Azure Mobile Apps JavaScript SDK can be done via the `npm` command:</span></span>

```
npm install azure-mobile-apps-client --save
```

<span data-ttu-id="b9358-115">Biblioteki mogą służyć jako moduł ES2015 w środowiskach CommonJS, takie jak Browserify i Webpack i jako AMD biblioteki.</span><span class="sxs-lookup"><span data-stu-id="b9358-115">The library can also be used as an ES2015 module, within CommonJS environments such as Browserify and Webpack and as an AMD library.</span></span>  <span data-ttu-id="b9358-116">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="b9358-116">For example:</span></span>

```
# For ECMAScript 5.1 CommonJS
var WindowsAzure = require('azure-mobile-apps-client');
# For ES2015 modules
import * as WindowsAzure from 'azure-mobile-apps-client';
```

<span data-ttu-id="b9358-117">Można także użyć wbudowanych wersji zestawu SDK, pobierając bezpośrednio z naszych CDN:</span><span class="sxs-lookup"><span data-stu-id="b9358-117">You can also use a pre-built version of the SDK by downloading directly from our CDN:</span></span>

```html
<script src="https://zumo.blob.core.windows.net/sdk/azure-mobile-apps-client.min.js"></script>
```

[!INCLUDE [app-service-mobile-html-js-library](../../includes/app-service-mobile-html-js-library.md)]

## <span data-ttu-id="b9358-118"><a name="auth"></a>Porady: uwierzytelnianie użytkowników</span><span class="sxs-lookup"><span data-stu-id="b9358-118"><a name="auth"></a>How to: Authenticate users</span></span>
<span data-ttu-id="b9358-119">Usługa aplikacji Azure obsługuje uwierzytelniania i autoryzacji użytkowników aplikacji przy użyciu różnych dostawców tożsamości zewnętrznych: Facebook, Google, Microsoft Account i Twitter.</span><span class="sxs-lookup"><span data-stu-id="b9358-119">Azure App Service supports authenticating and authorizing app users using various external identity providers: Facebook, Google, Microsoft Account, and Twitter.</span></span> <span data-ttu-id="b9358-120">Tabele, aby ograniczyć dostęp dla określonych operacji tylko do uwierzytelnionych użytkowników można ustawić uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="b9358-120">You can set permissions on tables to restrict access for specific operations to only authenticated users.</span></span> <span data-ttu-id="b9358-121">Umożliwia także tożsamość uwierzytelnionych użytkowników do zaimplementowania reguły autoryzacji w skryptach serwera.</span><span class="sxs-lookup"><span data-stu-id="b9358-121">You can also use the identity of authenticated users to implement authorization rules in server scripts.</span></span> <span data-ttu-id="b9358-122">Aby uzyskać więcej informacji, zobacz [Rozpoczynanie pracy z uwierzytelnianiem] samouczka.</span><span class="sxs-lookup"><span data-stu-id="b9358-122">For more information, see the [Get started with authentication] tutorial.</span></span>

<span data-ttu-id="b9358-123">Obsługiwane są dwa przepływy uwierzytelniania: przepływu serwera i klienta przepływu.</span><span class="sxs-lookup"><span data-stu-id="b9358-123">Two authentication flows are supported: a server flow and a client flow.</span></span>  <span data-ttu-id="b9358-124">Przepływ server zapewnia najprostszą środowisko uwierzytelniania, zależy od interfejsu uwierzytelniania sieci web dostawcy.</span><span class="sxs-lookup"><span data-stu-id="b9358-124">The server flow provides the simplest authentication experience, as it relies on the provider's web authentication interface.</span></span> <span data-ttu-id="b9358-125">Przepływ klienta zezwala lepszą integrację z możliwości specyficznych dla urządzeń, takich jak single-sign-on, ponieważ zależy od określonego dostawcy SDK.</span><span class="sxs-lookup"><span data-stu-id="b9358-125">The client flow allows for deeper integration with device-specific capabilities such as single-sign-on as it relies on provider-specific SDKs.</span></span>

[!INCLUDE [app-service-mobile-html-js-auth-library](../../includes/app-service-mobile-html-js-auth-library.md)]

### <span data-ttu-id="b9358-126"><a name="configure-external-redirect-urls"></a>Porady: Konfigurowanie usługi Mobile App Service dla adresy URL przekierowań zewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="b9358-126"><a name="configure-external-redirect-urls"></a>How to: Configure your Mobile App Service for external redirect URLs.</span></span>
<span data-ttu-id="b9358-127">Kilka typów aplikacji JavaScript używania możliwości sprzężenia zwrotnego na potrzeby obsługi przepływu OAuth interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="b9358-127">Several types of JavaScript applications use a loopback capability to handle OAuth UI flows.</span></span>  <span data-ttu-id="b9358-128">Te możliwości to m.in.:</span><span class="sxs-lookup"><span data-stu-id="b9358-128">These capabilities include:</span></span>

* <span data-ttu-id="b9358-129">Usługą lokalnie</span><span class="sxs-lookup"><span data-stu-id="b9358-129">Running your service locally</span></span>
* <span data-ttu-id="b9358-130">Przy użyciu przeładowania na żywo z jonowych Framework</span><span class="sxs-lookup"><span data-stu-id="b9358-130">Using Live Reload with the Ionic Framework</span></span>
* <span data-ttu-id="b9358-131">Przekierowanie do usługi App Service dla uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="b9358-131">Redirecting to App Service for authentication.</span></span>

<span data-ttu-id="b9358-132">Uruchomiony lokalnie może spowodować problemy, ponieważ domyślnie uwierzytelniania usługi aplikacji jest tylko skonfigurowane i umożliwiają dostęp z zaplecza aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="b9358-132">Running locally can cause problems because, by default, App Service authentication is only configured to allow access from your Mobile App backend.</span></span> <span data-ttu-id="b9358-133">Aby zmienić ustawienia usługi aplikacji, aby włączyć uwierzytelnianie podczas uruchamiania lokalnego serwera, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="b9358-133">Use the following steps to change the App Service settings to enable authentication when running the server locally:</span></span>

1. <span data-ttu-id="b9358-134">Zaloguj się do witryny [Azure Portal].</span><span class="sxs-lookup"><span data-stu-id="b9358-134">Log in to the [Azure portal]</span></span>
2. <span data-ttu-id="b9358-135">Przejdź do zaplecza aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="b9358-135">Navigate to your Mobile App backend.</span></span>
3. <span data-ttu-id="b9358-136">Wybierz **Eksploratora zasobów** w **narzędzi PROGRAMISTYCZNYCH** menu.</span><span class="sxs-lookup"><span data-stu-id="b9358-136">Select **Resource explorer** in the **DEVELOPMENT TOOLS** menu.</span></span>
4. <span data-ttu-id="b9358-137">Kliknij przycisk **Przejdź** można otworzyć w nowej karcie lub w oknie Eksploratora zasobów dla zaplecza aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="b9358-137">Click **Go** to open the resource explorer for your Mobile App backend in a new tab or window.</span></span>
5. <span data-ttu-id="b9358-138">Rozwiń węzeł **config** > **authsettings** węzła dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b9358-138">Expand the **config** > **authsettings** node for your app.</span></span>
6. <span data-ttu-id="b9358-139">Kliknij przycisk **Edytuj** przycisk, aby umożliwić edytowanie zasobu.</span><span class="sxs-lookup"><span data-stu-id="b9358-139">Click the **Edit** button to enable editing of the resource.</span></span>
7. <span data-ttu-id="b9358-140">Znajdź **allowedExternalRedirectUrls** element, który może mieć wartości null.</span><span class="sxs-lookup"><span data-stu-id="b9358-140">Find the **allowedExternalRedirectUrls** element, which should be null.</span></span> <span data-ttu-id="b9358-141">Dodaj adresami URL w tablicy:</span><span class="sxs-lookup"><span data-stu-id="b9358-141">Add your URLs in an array:</span></span>

         "allowedExternalRedirectUrls": [
             "http://localhost:3000",
             "https://localhost:3000"
         ],

    <span data-ttu-id="b9358-142">Zamień na adresy URL usługi, czyli w tym przykładzie adresy URL w tablicy `http://localhost:3000` lokalnej usługi Node.js w próbce.</span><span class="sxs-lookup"><span data-stu-id="b9358-142">Replace the URLs in the array with the URLs of your service, which in this example is `http://localhost:3000` for the local Node.js sample service.</span></span> <span data-ttu-id="b9358-143">Można także użyć `http://localhost:4400` usługi Ripple lub innych URL, w zależności od sposobu skonfigurowania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b9358-143">You could also use `http://localhost:4400` for the Ripple service or some other URL, depending on how your app is configured.</span></span>
8. <span data-ttu-id="b9358-144">W górnej części strony kliknij **odczytu/zapisu**, następnie kliknij przycisk **PUT** Aby zapisać zmiany.</span><span class="sxs-lookup"><span data-stu-id="b9358-144">At the top of the page, click **Read/Write**, then click **PUT** to save your updates.</span></span>

<span data-ttu-id="b9358-145">Należy również dodać tych samych adresów URL sprzężenia zwrotnego do CORS ustawień listy dozwolonych adresów IP:</span><span class="sxs-lookup"><span data-stu-id="b9358-145">You also need to add the same loopback URLs to the CORS whitelist settings:</span></span>

1. <span data-ttu-id="b9358-146">Przejdź z powrotem do [Azure Portal].</span><span class="sxs-lookup"><span data-stu-id="b9358-146">Navigate back to the [Azure portal].</span></span>
2. <span data-ttu-id="b9358-147">Przejdź do zaplecza aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="b9358-147">Navigate to your Mobile App backend.</span></span>
3. <span data-ttu-id="b9358-148">Kliknij przycisk **CORS** w **interfejsu API** menu.</span><span class="sxs-lookup"><span data-stu-id="b9358-148">Click **CORS** in the **API** menu.</span></span>
4. <span data-ttu-id="b9358-149">Wprowadź każdy adres URL w pustej **dozwolone źródła** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="b9358-149">Enter each URL in the empty **Allowed Origins** text box.</span></span>  <span data-ttu-id="b9358-150">Utworzono nowe pole tekstowe.</span><span class="sxs-lookup"><span data-stu-id="b9358-150">A new text box is created.</span></span>
5. <span data-ttu-id="b9358-151">Kliknij przycisk **ZAPISZ**</span><span class="sxs-lookup"><span data-stu-id="b9358-151">Click **SAVE**</span></span>

<span data-ttu-id="b9358-152">Po aktualizacji wewnętrznej bazy danych, można korzystać z nowych sprzężenia zwrotnego adresów URL w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b9358-152">After the backend updates, you will be able to use the new loopback URLs in your app.</span></span>

<!-- URLs. -->
<span data-ttu-id="b9358-153">[Azure Mobile Apps Szybki Start]: app-service-mobile-cordova-get-started.md</span><span class="sxs-lookup"><span data-stu-id="b9358-153">[Azure Mobile Apps Quick Start]: app-service-mobile-cordova-get-started.md</span></span>
<span data-ttu-id="b9358-154">[Rozpoczynanie pracy z uwierzytelnianiem]: app-service-mobile-cordova-get-started-users.md</span><span class="sxs-lookup"><span data-stu-id="b9358-154">[Get started with authentication]: app-service-mobile-cordova-get-started-users.md</span></span>
[Add authentication to your app]: app-service-mobile-cordova-get-started-users.md

<span data-ttu-id="b9358-155">[Azure Portal]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="b9358-155">[Azure portal]: https://portal.azure.com/</span></span>
<span data-ttu-id="b9358-156">[JavaScript SDK usługi Azure Mobile Apps]: https://www.npmjs.com/package/azure-mobile-apps-client</span><span class="sxs-lookup"><span data-stu-id="b9358-156">[JavaScript SDK for Azure Mobile Apps]: https://www.npmjs.com/package/azure-mobile-apps-client</span></span>
[Query object documentation]: https://msdn.microsoft.com/en-us/library/azure/jj613353.aspx
