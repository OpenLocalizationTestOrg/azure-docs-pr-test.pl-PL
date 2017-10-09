---
title: "zestaw SDK usługi Mobile Engagement w sieci Web integracji aaaAzure | Dokumentacja firmy Microsoft"
description: "Witaj najnowsze aktualizacje i procedury dotyczące hello zestaw SDK usługi Azure Mobile Engagement w sieci Web"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: b5daa2a2-942b-489d-aa1d-568c3b25e56f
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: web
ms.devlang: js
ms.topic: article
ms.date: 02/29/2016
ms.author: piyushjo
ms.openlocfilehash: 99613b68b615bec4ddcfcc8e4e0133ce9d887bad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-mobile-engagement-in-a-web-application"></a><span data-ttu-id="44fbc-103">Integrowanie usługi Azure Mobile Engagement w aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="44fbc-103">Integrate Azure Mobile Engagement in a web application</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="44fbc-104">Aplikacje uniwersalne systemu Windows</span><span class="sxs-lookup"><span data-stu-id="44fbc-104">Windows Universal</span></span>](mobile-engagement-windows-store-integrate-engagement.md)
> * [<span data-ttu-id="44fbc-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="44fbc-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="44fbc-106">iOS</span><span class="sxs-lookup"><span data-stu-id="44fbc-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="44fbc-107">Android</span><span class="sxs-lookup"><span data-stu-id="44fbc-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md)
> 
> 

<span data-ttu-id="44fbc-108">Witaj procedur w tym artykule opisano hello najprostszy sposób tooactivate hello analizy i monitorowania funkcji w usłudze Azure Mobile Engagement w aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="44fbc-108">hello procedures in this article describe hello simplest way tooactivate hello analytics and monitoring functions in Azure Mobile Engagement in your web application.</span></span>

<span data-ttu-id="44fbc-109">Wykonaj wszystkie statystyki dotyczące użytkowników, sesji, działania, awarii (Crash) i technicals hello kroki tooactivate hello dziennika raportów, które są potrzebne toocompute.</span><span class="sxs-lookup"><span data-stu-id="44fbc-109">Follow hello steps tooactivate hello log reports that are needed toocompute all statistics about users, sessions, activities, crashes, and technicals.</span></span> <span data-ttu-id="44fbc-110">Statystyki zależne od aplikacji, takich jak zdarzenia, błędy i zadań należy ręcznie uaktywnić raporty dziennika przy użyciu interfejsu API usługi Azure Mobile Engagement hello.</span><span class="sxs-lookup"><span data-stu-id="44fbc-110">For application-dependent statistics, such as events, errors, and jobs, you must activate log reports manually by using hello Azure Mobile Engagement API.</span></span> <span data-ttu-id="44fbc-111">Aby uzyskać więcej informacji, Dowiedz się [jak toouse hello zaawansowane znakowanie interfejsu API w aplikacji sieci web usługi Mobile Engagement](mobile-engagement-web-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="44fbc-111">For more information, learn [how toouse hello advanced Mobile Engagement tagging API in a web application](mobile-engagement-web-use-engagement-api.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="44fbc-112">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="44fbc-112">Introduction</span></span>
<span data-ttu-id="44fbc-113">[Pobierz zestaw SDK usługi Azure Mobile Engagement Web hello](http://aka.ms/P7b453).</span><span class="sxs-lookup"><span data-stu-id="44fbc-113">[Download hello Azure Mobile Engagement Web SDK](http://aka.ms/P7b453).</span></span>
<span data-ttu-id="44fbc-114">Hello przenośnych zaangażowania zestawu SDK sieci Web jest dostarczana jako pojedynczy plik JavaScript, azure-engagement.js, których tooinclude na każdej stronie Twojej witryny lub aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="44fbc-114">hello Mobile Engagement Web SDK is shipped as a single JavaScript file, azure-engagement.js, which you have tooinclude in each page of your site or web application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="44fbc-115">Przed uruchomieniem tego skryptu, należy uruchomić skrypt lub zapisu tooconfigure Mobile Engagement dla aplikacji fragment kodu.</span><span class="sxs-lookup"><span data-stu-id="44fbc-115">Before you run this script, you must run a script or code snippet that you write tooconfigure Mobile Engagement for your application.</span></span>
> 
> 

## <a name="browser-compatibility"></a><span data-ttu-id="44fbc-116">Zgodność przeglądarek</span><span class="sxs-lookup"><span data-stu-id="44fbc-116">Browser compatibility</span></span>
<span data-ttu-id="44fbc-117">Hello zestaw SDK usługi Mobile Engagement w sieci Web używa natywnego JSON, kodowania i dekodowania dodatkowo żądania AJAX toocross domeny (polegania na powitania specyfikacji W3C CORS).</span><span class="sxs-lookup"><span data-stu-id="44fbc-117">hello Mobile Engagement Web SDK uses native JSON encoding and decoding, in addition toocross-domain AJAX requests (relying on hello W3C CORS specification).</span></span> <span data-ttu-id="44fbc-118">Jest on zgodny z hello następujące przeglądarki:</span><span class="sxs-lookup"><span data-stu-id="44fbc-118">It's compatible with hello following browsers:</span></span>

* <span data-ttu-id="44fbc-119">Przeglądarka Microsoft Edge 12 +</span><span class="sxs-lookup"><span data-stu-id="44fbc-119">Microsoft Edge 12+</span></span>
* <span data-ttu-id="44fbc-120">Program Internet Explorer 10 +</span><span class="sxs-lookup"><span data-stu-id="44fbc-120">Internet Explorer 10+</span></span>
* <span data-ttu-id="44fbc-121">Firefox 3.5 +</span><span class="sxs-lookup"><span data-stu-id="44fbc-121">Firefox 3.5+</span></span>
* <span data-ttu-id="44fbc-122">Chrome 4 +</span><span class="sxs-lookup"><span data-stu-id="44fbc-122">Chrome 4+</span></span>
* <span data-ttu-id="44fbc-123">Safari 6 +</span><span class="sxs-lookup"><span data-stu-id="44fbc-123">Safari 6+</span></span>
* <span data-ttu-id="44fbc-124">Opera 12 +</span><span class="sxs-lookup"><span data-stu-id="44fbc-124">Opera 12+</span></span>

## <a name="configure-mobile-engagement"></a><span data-ttu-id="44fbc-125">Konfigurowanie usługi Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="44fbc-125">Configure Mobile Engagement</span></span>
<span data-ttu-id="44fbc-126">Napisać skrypt, który tworzy globalnym `azureEngagement` obiektu JavaScript, tak jak hello poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="44fbc-126">Write a script that creates a global `azureEngagement` JavaScript object, as in hello following example.</span></span> <span data-ttu-id="44fbc-127">Ponieważ witryna może być wielokrotność stron, w tym przykładzie założono, że ten skrypt znajduje się na każdej stronie.</span><span class="sxs-lookup"><span data-stu-id="44fbc-127">Because your site might have multiples pages, this example assumes that this script is included in every page.</span></span> <span data-ttu-id="44fbc-128">W tym przykładzie nosi nazwę obiektu JavaScript hello `azure-engagement-conf.js`.</span><span class="sxs-lookup"><span data-stu-id="44fbc-128">In this example, hello JavaScript object is named `azure-engagement-conf.js`.</span></span>

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      appVersionName: '1.0.0',
      appVersionCode: 1
    };

<span data-ttu-id="44fbc-129">Witaj `connectionString` wartość aplikacji zostanie wyświetlony w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="44fbc-129">hello `connectionString` value for your application is displayed in hello Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="44fbc-130">`appVersionName`i `appVersionCode` są opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="44fbc-130">`appVersionName` and `appVersionCode` are optional.</span></span> <span data-ttu-id="44fbc-131">Jednak zaleca się je skonfigurować tak, aby analiza może przetworzyć informacji o wersji.</span><span class="sxs-lookup"><span data-stu-id="44fbc-131">However, we recommend that you configure them so that analytics can process version information.</span></span>
> 
> 

## <a name="include-mobile-engagement-scripts-in-your-pages"></a><span data-ttu-id="44fbc-132">Uwzględnić skrypty Mobile Engagement na swoich stronach</span><span class="sxs-lookup"><span data-stu-id="44fbc-132">Include Mobile Engagement scripts in your pages</span></span>
<span data-ttu-id="44fbc-133">Dodaj usługi Mobile Engagement skrypty tooyour stron w jednym z hello następujące sposoby:</span><span class="sxs-lookup"><span data-stu-id="44fbc-133">Add Mobile Engagement scripts tooyour pages in one of hello following ways:</span></span>

    <head>
      ...
      <script type="text/javascript" src="azure-engagement-conf.js"></script>
      <script type="text/javascript" src="azure-engagement.js"></script>
      ...
    </head>

<span data-ttu-id="44fbc-134">Lub to:</span><span class="sxs-lookup"><span data-stu-id="44fbc-134">Or this:</span></span>

    <body>
      ...
      <script type="text/javascript" src="azure-engagement-conf.js"></script>
      <script type="text/javascript" src="azure-engagement.js"></script>
      ...
    </body>

## <a name="alias"></a><span data-ttu-id="44fbc-135">Alias</span><span class="sxs-lookup"><span data-stu-id="44fbc-135">Alias</span></span>
<span data-ttu-id="44fbc-136">Po załadowaniu hello skryptu zestaw SDK usługi Mobile Engagement w sieci Web tworzy hello **engagement** alias tooaccess hello interfejsów API zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="44fbc-136">After hello Mobile Engagement Web SDK script is loaded, it creates hello **engagement** alias tooaccess hello SDK APIs.</span></span> <span data-ttu-id="44fbc-137">Nie można użyć tego aliasu toodefine hello SDK konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="44fbc-137">You cannot use this alias toodefine hello SDK configuration.</span></span> <span data-ttu-id="44fbc-138">Ten alias jest używany jako odwołanie w niniejszej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="44fbc-138">This alias is used as a reference in this documentation.</span></span>

<span data-ttu-id="44fbc-139">Należy pamiętać, że jeśli hello domyślny alias powoduje konflikt z innym zmiennej globalnej ze strony użytkownika, można zmienić go w konfiguracji hello następujący przed załadowaniem hello zestaw SDK usługi Mobile Engagement w sieci Web:</span><span class="sxs-lookup"><span data-stu-id="44fbc-139">Note that if hello default alias conflicts with another global variable from your page, you can redefine it in hello configuration as follows before you load hello Mobile Engagement Web SDK:</span></span>

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      appVersionName: '1.0.0',
      appVersionCode: 1
      alias:'anotherAlias'
    };

## <a name="basic-reporting"></a><span data-ttu-id="44fbc-140">Podstawowym raportowaniem</span><span class="sxs-lookup"><span data-stu-id="44fbc-140">Basic reporting</span></span>
<span data-ttu-id="44fbc-141">Podstawowym raportowaniem w usłudze Mobile Engagement obejmuje statystyki poziomu sesji, takie jak statystyki dotyczące użytkowników, sesji, działaniami i awariami.</span><span class="sxs-lookup"><span data-stu-id="44fbc-141">Basic reporting in Mobile Engagement covers session-level statistics, such as statistics about users, sessions, activities, and crashes.</span></span>

### <a name="session-tracking"></a><span data-ttu-id="44fbc-142">Śledzenie sesji</span><span class="sxs-lookup"><span data-stu-id="44fbc-142">Session tracking</span></span>
<span data-ttu-id="44fbc-143">Sesja usługi Mobile Engagement jest podzielony na sekwencję działań, każdy identyfikowane przez nazwę.</span><span class="sxs-lookup"><span data-stu-id="44fbc-143">A Mobile Engagement session is divided into a sequence of activities, each identified by a name.</span></span>

<span data-ttu-id="44fbc-144">W klasycznej witryny zaleca się zadeklarować różnych działań na każdej stronie witryny.</span><span class="sxs-lookup"><span data-stu-id="44fbc-144">In a classic website, we recommend that you declare a different activity on each page of your site.</span></span> <span data-ttu-id="44fbc-145">Dla witryny sieci Web lub aplikacji sieci web w których hello nigdy nie zmienia bieżącej strony możesz tootrack hello działań na mniejszą skalę, takich jak stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="44fbc-145">For a website or web application in which hello current page never changes, you might want tootrack hello activities on a smaller scale, such as within hello page.</span></span>

<span data-ttu-id="44fbc-146">Albo, toostart lub zmień hello bieżącego działania użytkownika, wywołania hello `engagement.agent.startActivity` funkcji.</span><span class="sxs-lookup"><span data-stu-id="44fbc-146">Either way, toostart or change hello current user activity, call hello `engagement.agent.startActivity` function.</span></span> <span data-ttu-id="44fbc-147">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="44fbc-147">For example:</span></span>

    <body onload="yourOnload()">

    <!-- -->

    yourOnload = function() {
      [...]
      engagement.agent.startActivity('welcome');
    };

<span data-ttu-id="44fbc-148">Serwer usługi Mobile Engagement Hello kończy się automatycznie otwartych sesji w ciągu trzech minut po zamknięciu strony aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="44fbc-148">hello Mobile Engagement server automatically ends an open session within three minutes after hello application page is closed.</span></span>

<span data-ttu-id="44fbc-149">Alternatywnie można zakończyć sesję ręcznie przez wywołanie metody `engagement.agent.endActivity`.</span><span class="sxs-lookup"><span data-stu-id="44fbc-149">Alternatively, you can end a session manually by calling `engagement.agent.endActivity`.</span></span> <span data-ttu-id="44fbc-150">To ustawienie hello bieżącego użytkownika działania too'Idle. "</span><span class="sxs-lookup"><span data-stu-id="44fbc-150">This sets hello current user activity too'Idle.'</span></span>  <span data-ttu-id="44fbc-151">Sesja Hello zakończy później 10 sekund, chyba że nowy wywołanie za`engagement.agent.startActivity` wznawia hello sesji.</span><span class="sxs-lookup"><span data-stu-id="44fbc-151">hello session will end 10 seconds later unless a new call too`engagement.agent.startActivity` resumes hello session.</span></span>

<span data-ttu-id="44fbc-152">Witaj 10-sekundowe opóźnienie można skonfigurować w obiekcie globalnej hello, w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="44fbc-152">You can configure hello 10-second delay in hello global engagement object, as follows:</span></span>

    engagement.sessionTimeout = 2000; // 2 seconds
    // or
    engagement.sessionTimeout = 0; // end hello session as soon as endActivity is called

> [!NOTE]
> <span data-ttu-id="44fbc-153">Nie można użyć `engagement.agent.endActivity` w hello `onunload` wywołania zwrotnego, ponieważ na tym etapie nie można wprowadzić wywołania AJAX.</span><span class="sxs-lookup"><span data-stu-id="44fbc-153">You cannot use `engagement.agent.endActivity` in hello `onunload` callback because you cannot make AJAX calls at this stage.</span></span>
> 
> 

## <a name="advanced-reporting"></a><span data-ttu-id="44fbc-154">Zaawansowane raportowanie</span><span class="sxs-lookup"><span data-stu-id="44fbc-154">Advanced reporting</span></span>
<span data-ttu-id="44fbc-155">Opcjonalnie Jeśli chcesz tooreport zdarzenia specyficzne dla aplikacji, błędy i zadań, należy hello toouse Mobile Engagement z interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="44fbc-155">Optionally, if you want tooreport application-specific events, errors, and jobs, you need toouse hello Mobile Engagement API.</span></span> <span data-ttu-id="44fbc-156">Dostęp hello Mobile Engagement API za pośrednictwem hello `engagement.agent` obiektu.</span><span class="sxs-lookup"><span data-stu-id="44fbc-156">You access hello Mobile Engagement API through hello `engagement.agent` object.</span></span>

<span data-ttu-id="44fbc-157">Możesz uzyskać dostęp do wszystkich hello zaawansowane funkcje w usłudze Mobile Engagement w hello Mobile Engagement z interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="44fbc-157">You can access all of hello advanced capabilities in Mobile Engagement in hello Mobile Engagement API.</span></span> <span data-ttu-id="44fbc-158">Witaj interfejsu API została szczegółowo opisana w artykule hello [jak toouse hello zaawansowane znakowanie interfejsu API w aplikacji sieci web usługi Mobile Engagement](mobile-engagement-web-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="44fbc-158">hello API is detailed in hello article [How toouse hello advanced Mobile Engagement tagging API in a web application](mobile-engagement-web-use-engagement-api.md).</span></span>

## <a name="customize-hello-urls-used-for-ajax-calls"></a><span data-ttu-id="44fbc-159">Dostosowywanie hello adresy URL używany dla wywołań AJAX</span><span class="sxs-lookup"><span data-stu-id="44fbc-159">Customize hello URLs used for AJAX calls</span></span>
<span data-ttu-id="44fbc-160">Adresy URL można dostosować ten hello używanych przez zestaw SDK usługi Mobile Engagement w sieci Web.</span><span class="sxs-lookup"><span data-stu-id="44fbc-160">You can customize URLs that hello Mobile Engagement Web SDK uses.</span></span> <span data-ttu-id="44fbc-161">Na przykład może zastąpić konfiguracji hello tooredefine hello URL dziennika (hello SDK punktu końcowego logowania), podobnie do następującej:</span><span class="sxs-lookup"><span data-stu-id="44fbc-161">For example, tooredefine hello log URL (hello SDK endpoint for logging), you can override hello configuration like this:</span></span>

    window.azureEngagement = {
      ...
      urls: {
        ...        
        getLoggerUrl: function() {
        return 'someProxy/log';
        }
      }
    };

<span data-ttu-id="44fbc-162">Jeśli adres URL funkcji zwraca ciąg, który rozpoczyna się od `/`, `//`, `http://`, lub `https://`, hello domyślny schemat nie jest używany.</span><span class="sxs-lookup"><span data-stu-id="44fbc-162">If your URL functions return a string that begins with `/`, `//`, `http://`, or `https://`, hello default scheme is not used.</span></span> <span data-ttu-id="44fbc-163">Domyślnie program hello `https://` schemat jest używany dla tych adresów URL.</span><span class="sxs-lookup"><span data-stu-id="44fbc-163">By default, hello `https://` scheme is used for those URLs.</span></span> <span data-ttu-id="44fbc-164">Jeśli chcesz toocustomize hello domyślny schemat, Zastąp hello konfiguracji, takich jak to:</span><span class="sxs-lookup"><span data-stu-id="44fbc-164">If you want toocustomize hello default scheme, override hello configuration, like this:</span></span>

    window.azureEngagement = {
      ...
      urls: {
        ...         
        scheme: '//'
      }
    };
