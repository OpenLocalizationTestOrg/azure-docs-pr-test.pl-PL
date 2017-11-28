---
title: "aaaGet wprowadzenie do usługi Azure Mobile Engagement dla aplikacji sieci Web | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse usługi Azure Mobile Engagement z analizy i powiadomieniami wypychanymi dla aplikacji sieci Web."
services: mobile-engagement
documentationcenter: Mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 04afe53a-4caf-4c80-bd75-20cc630cd75c
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: js
ms.topic: hero-article
ms.date: 06/01/2016
ms.author: piyushjo
ms.openlocfilehash: a84c96cac13bf3b85e72aef55da5c91693e1766c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-web-apps"></a><span data-ttu-id="044fd-103">Wprowadzenie do usługi Azure Mobile Engagement dla aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="044fd-103">Get started with Azure Mobile Engagement for Web Apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="044fd-104">W tym temacie opisano sposób toounderstand usługi Azure Mobile Engagement toouse użycia aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="044fd-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your Web App usage.</span></span>

> [!NOTE]
> <span data-ttu-id="044fd-105">Usługa Azure Mobile Engagement Hello zostaną wycofane 2018 marca i jest obecnie tylko dostępne tooexisting klientów.</span><span class="sxs-lookup"><span data-stu-id="044fd-105">hello Azure Mobile Engagement service will be retired March 2018 and is currently only available tooexisting customers.</span></span> <span data-ttu-id="044fd-106">Aby uzyskać więcej informacji, zobacz [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span><span class="sxs-lookup"><span data-stu-id="044fd-106">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

<span data-ttu-id="044fd-107">Ten samouczek wymaga następujących hello:</span><span class="sxs-lookup"><span data-stu-id="044fd-107">This tutorial requires hello following:</span></span>

* <span data-ttu-id="044fd-108">Visual Studio 2015 lub dowolny inny edytor</span><span class="sxs-lookup"><span data-stu-id="044fd-108">Visual Studio 2015 or any other editor of your choice</span></span>
* [<span data-ttu-id="044fd-109">Zestaw SDK sieci Web</span><span class="sxs-lookup"><span data-stu-id="044fd-109">Web SDK</span></span>](http://aka.ms/P7b453)

<span data-ttu-id="044fd-110">Zestaw SDK sieci Web jest w wersji zapoznawczej i tylko obsługuje analityka w chwili hello i wysyłania powiadomień wypychanych w aplikacji lub przeglądarka nie obsługuje jeszcze.</span><span class="sxs-lookup"><span data-stu-id="044fd-110">This Web SDK is in Preview and only supports Analytics at hello moment and doesn't support sending browser or in-app push notifications yet.</span></span> 

> [!NOTE]
> <span data-ttu-id="044fd-111">toocomplete tego samouczka, musi mieć aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="044fd-111">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="044fd-112">Jeśli go nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="044fd-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="044fd-113">Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-web-app-get-started).</span><span class="sxs-lookup"><span data-stu-id="044fd-113">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-web-app-get-started).</span></span>
> 
> 

## <a name="setup-mobile-engagement-for-your-web-app"></a><span data-ttu-id="044fd-114">Konfigurowanie usługi Mobile Engagement dla aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="044fd-114">Setup Mobile Engagement for your Web app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="044fd-115"><a id="connecting-app"></a>Połączenie z zapleczem usługi Mobile Engagement toohello aplikacji</span><span class="sxs-lookup"><span data-stu-id="044fd-115"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="044fd-116">Ten samouczek przedstawia "podstawową integrację," będący hello minimalny zestaw wymagany toocollect danych.</span><span class="sxs-lookup"><span data-stu-id="044fd-116">This tutorial presents a "basic integration," which is hello minimal set required toocollect data.</span></span>

<span data-ttu-id="044fd-117">Utworzymy aplikację sieci web podstawowe z integracji programu Visual Studio toodemonstrate hello chociaż hello kroki można wykonać z dowolnej aplikacji sieci web również utworzone poza Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="044fd-117">We will create a basic web app with Visual Studio toodemonstrate hello integration though you can follow hello steps with any web application created outside of Visual Studio also.</span></span> 

### <a name="create-a-new-web-app"></a><span data-ttu-id="044fd-118">Tworzenie nowej aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="044fd-118">Create a new Web App</span></span>
<span data-ttu-id="044fd-119">Hello następujących krokach założono użycie hello programu Visual Studio 2015 chociaż hello kroki są podobne we wcześniejszych wersjach programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="044fd-119">hello following steps assume hello use of Visual Studio 2015 though hello steps are similar in earlier versions of Visual Studio.</span></span> 

1. <span data-ttu-id="044fd-120">Uruchom program Visual Studio w hello **Home** ekranu wybierz **nowy projekt**.</span><span class="sxs-lookup"><span data-stu-id="044fd-120">Start Visual Studio, and in hello **Home** screen, select **New Project**.</span></span>
2. <span data-ttu-id="044fd-121">W oknie podręcznym hello wybierz **Web** -> **aplikacji sieci Web ASP.Net**.</span><span class="sxs-lookup"><span data-stu-id="044fd-121">In hello pop-up, select **Web** -> **ASP.Net Web Application**.</span></span> <span data-ttu-id="044fd-122">Wypełnij aplikacji hello **nazwa**, **lokalizacji** i **Nazwa rozwiązania**, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="044fd-122">Fill in hello app **Name**, **Location** and  **Solution name**, and then click **OK**.</span></span>
3. <span data-ttu-id="044fd-123">W hello **wybierz szablon** menu podręczne, wybierz **pusty** w obszarze **ASP.Net 4.5 szablony** i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="044fd-123">In hello **Select a template** popup, select **Empty** under **ASP.Net 4.5 Templates** and click **OK**.</span></span> 

<span data-ttu-id="044fd-124">Został utworzony nowy pusty projekt aplikacji sieci Web do której zostanie zintegrowana hello zestaw SDK usługi Azure Mobile Engagement w sieci Web.</span><span class="sxs-lookup"><span data-stu-id="044fd-124">You have now created a new blank Web App project into which we will integrate hello Azure Mobile Engagement Web SDK.</span></span>

### <a name="connect-your-app-toomobile-engagement-backend"></a><span data-ttu-id="044fd-125">Połącz zapleczu swojej aplikacji tooMobile zaangażowania</span><span class="sxs-lookup"><span data-stu-id="044fd-125">Connect your app tooMobile Engagement backend</span></span>
1. <span data-ttu-id="044fd-126">Utwórz nowy folder o nazwie **javascript** w rozwiązaniu i Dodaj plik sieci Web node.js SDK hello **azure engagement.js** do niego.</span><span class="sxs-lookup"><span data-stu-id="044fd-126">Create a new folder called **javascript** in your solution and add hello Web SDK JS file **azure-engagement.js** into it.</span></span> 
2. <span data-ttu-id="044fd-127">Dodaj nowy plik o nazwie **main.js** w tym folderze javascript z hello następującego kodu.</span><span class="sxs-lookup"><span data-stu-id="044fd-127">Add a new file called **main.js** in this javascript folder with hello following code.</span></span> <span data-ttu-id="044fd-128">Upewnij się, że parametry połączenia hello tooupdate.</span><span class="sxs-lookup"><span data-stu-id="044fd-128">Make sure tooupdate hello connection string.</span></span> <span data-ttu-id="044fd-129">To `azureEngagement` obiekt będzie używana tooaccess metody zestawu SDK sieci Web.</span><span class="sxs-lookup"><span data-stu-id="044fd-129">This `azureEngagement` object will be used tooaccess Web SDK methods.</span></span> 
   
        var azureEngagement = {
            debug: true,
            connectionString: 'xxxxx'
        };
   
    ![Program Visual Studio z plikami js][1]

## <a name="enable-real-time-monitoring"></a><span data-ttu-id="044fd-131">Włączanie monitorowania w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="044fd-131">Enable real-time monitoring</span></span>
<span data-ttu-id="044fd-132">W kolejności toostart wysyłanie danych i zapewnienie, że hello użytkownicy są aktywni konieczne jest wysłanie co najmniej jeden zapleczem usługi Mobile Engagement toohello działania.</span><span class="sxs-lookup"><span data-stu-id="044fd-132">In order toostart sending data and ensuring that hello users are active, you must send at least one Activity toohello Mobile Engagement backend.</span></span> <span data-ttu-id="044fd-133">Działania w kontekście hello aplikacji sieci web to strona sieci web.</span><span class="sxs-lookup"><span data-stu-id="044fd-133">An activity in hello context of a web app is a web page.</span></span> 

1. <span data-ttu-id="044fd-134">Utwórz nową stronę o nazwie **home.html** w rozwiązaniu i ustaw go jako rozpoczęciem powitalne strony dla aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="044fd-134">Create a new page called **home.html** in your solution and set it as hello starting page for your web app.</span></span> 
2. <span data-ttu-id="044fd-135">Zawierają hello dwa skrypty JavaScript, dodana przez dodanie następujących hello w tagu treści hello we wcześniejszej części tej strony.</span><span class="sxs-lookup"><span data-stu-id="044fd-135">Include hello two javascripts we added earlier in this page by adding hello following within hello body tag.</span></span> 
   
        <script type="text/javascript" src="javascript/main.js"></script>
        <script type="text/javascript" src="javascript/azure-engagement.js"></script>
3. <span data-ttu-id="044fd-136">Zaktualizuj hello treści tag toocall EngagementAgent w `startActivity` — metoda</span><span class="sxs-lookup"><span data-stu-id="044fd-136">Update hello body tag toocall EngagementAgent's `startActivity` method</span></span>
   
        <body onload="engagement.agent.startActivity('Home')">
4. <span data-ttu-id="044fd-137">Twoja strona **home.html** będzie wyglądać tak:</span><span class="sxs-lookup"><span data-stu-id="044fd-137">Here is what your **home.html** will look like</span></span>
   
        <html>
        <head>
            ...
        </head>
        <body onload="engagement.agent.startActivity('Home')">
            <script type="text/javascript" src="javascript/main.js"></script>
            <script type="text/javascript" src="javascript/azure-engagement.js"></script>
        </body>
        </html>

## <a name="connect-app-with-real-time-monitoring"></a><span data-ttu-id="044fd-138">Łączenie aplikacji z funkcją monitorowania w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="044fd-138">Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

  ![][2]

## <a name="extend-analytics"></a><span data-ttu-id="044fd-139">Poszerzanie analizy</span><span class="sxs-lookup"><span data-stu-id="044fd-139">Extend analytics</span></span>
<span data-ttu-id="044fd-140">W tym miejscu wszystkie metody hello są obecnie dostępne z zestawu SDK sieci Web służącego do analizy:</span><span class="sxs-lookup"><span data-stu-id="044fd-140">Here are all hello methods currently available with Web SDK that you can use for analytics:</span></span>

1. <span data-ttu-id="044fd-141">Działania/strony sieci Web:</span><span class="sxs-lookup"><span data-stu-id="044fd-141">Activities/Web pages:</span></span>
   
        engagement.agent.startActivity(name);
        engagement.agent.endActivity();
2. <span data-ttu-id="044fd-142">Zdarzenia</span><span class="sxs-lookup"><span data-stu-id="044fd-142">Events</span></span>
   
        engagement.agent.sendEvent(name, extras);
3. <span data-ttu-id="044fd-143">Błędy</span><span class="sxs-lookup"><span data-stu-id="044fd-143">Errors</span></span>
   
        engagement.agent.sendError(name, extras);
4. <span data-ttu-id="044fd-144">Zadania</span><span class="sxs-lookup"><span data-stu-id="044fd-144">Jobs</span></span>
   
        engagement.agent.startJob(name);
        engagement.agent.endJob(name);

<!-- Images. -->
[1]: ./media/mobile-engagement-web-app-get-started/visual-studio-solution-js.png
[2]: ./media/mobile-engagement-web-app-get-started/session.png

