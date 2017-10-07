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
# <a name="get-started-with-azure-mobile-engagement-for-web-apps"></a>Wprowadzenie do usługi Azure Mobile Engagement dla aplikacji sieci Web
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

W tym temacie opisano sposób toounderstand usługi Azure Mobile Engagement toouse użycia aplikacji sieci Web.

> [!NOTE]
> Usługa Azure Mobile Engagement Hello zostaną wycofane 2018 marca i jest obecnie tylko dostępne tooexisting klientów. Aby uzyskać więcej informacji, zobacz [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).

Ten samouczek wymaga następujących hello:

* Visual Studio 2015 lub dowolny inny edytor
* [Zestaw SDK sieci Web](http://aka.ms/P7b453)

Zestaw SDK sieci Web jest w wersji zapoznawczej i tylko obsługuje analityka w chwili hello i wysyłania powiadomień wypychanych w aplikacji lub przeglądarka nie obsługuje jeszcze. 

> [!NOTE]
> toocomplete tego samouczka, musi mieć aktywne konto platformy Azure. Jeśli go nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut. Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-web-app-get-started).
> 
> 

## <a name="setup-mobile-engagement-for-your-web-app"></a>Konfigurowanie usługi Mobile Engagement dla aplikacji sieci Web
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>Połączenie z zapleczem usługi Mobile Engagement toohello aplikacji
Ten samouczek przedstawia "podstawową integrację," będący hello minimalny zestaw wymagany toocollect danych.

Utworzymy aplikację sieci web podstawowe z integracji programu Visual Studio toodemonstrate hello chociaż hello kroki można wykonać z dowolnej aplikacji sieci web również utworzone poza Visual Studio. 

### <a name="create-a-new-web-app"></a>Tworzenie nowej aplikacji sieci Web
Hello następujących krokach założono użycie hello programu Visual Studio 2015 chociaż hello kroki są podobne we wcześniejszych wersjach programu Visual Studio. 

1. Uruchom program Visual Studio w hello **Home** ekranu wybierz **nowy projekt**.
2. W oknie podręcznym hello wybierz **Web** -> **aplikacji sieci Web ASP.Net**. Wypełnij aplikacji hello **nazwa**, **lokalizacji** i **Nazwa rozwiązania**, a następnie kliknij przycisk **OK**.
3. W hello **wybierz szablon** menu podręczne, wybierz **pusty** w obszarze **ASP.Net 4.5 szablony** i kliknij przycisk **OK**. 

Został utworzony nowy pusty projekt aplikacji sieci Web do której zostanie zintegrowana hello zestaw SDK usługi Azure Mobile Engagement w sieci Web.

### <a name="connect-your-app-toomobile-engagement-backend"></a>Połącz zapleczu swojej aplikacji tooMobile zaangażowania
1. Utwórz nowy folder o nazwie **javascript** w rozwiązaniu i Dodaj plik sieci Web node.js SDK hello **azure engagement.js** do niego. 
2. Dodaj nowy plik o nazwie **main.js** w tym folderze javascript z hello następującego kodu. Upewnij się, że parametry połączenia hello tooupdate. To `azureEngagement` obiekt będzie używana tooaccess metody zestawu SDK sieci Web. 
   
        var azureEngagement = {
            debug: true,
            connectionString: 'xxxxx'
        };
   
    ![Program Visual Studio z plikami js][1]

## <a name="enable-real-time-monitoring"></a>Włączanie monitorowania w czasie rzeczywistym
W kolejności toostart wysyłanie danych i zapewnienie, że hello użytkownicy są aktywni konieczne jest wysłanie co najmniej jeden zapleczem usługi Mobile Engagement toohello działania. Działania w kontekście hello aplikacji sieci web to strona sieci web. 

1. Utwórz nową stronę o nazwie **home.html** w rozwiązaniu i ustaw go jako rozpoczęciem powitalne strony dla aplikacji sieci web. 
2. Zawierają hello dwa skrypty JavaScript, dodana przez dodanie następujących hello w tagu treści hello we wcześniejszej części tej strony. 
   
        <script type="text/javascript" src="javascript/main.js"></script>
        <script type="text/javascript" src="javascript/azure-engagement.js"></script>
3. Zaktualizuj hello treści tag toocall EngagementAgent w `startActivity` — metoda
   
        <body onload="engagement.agent.startActivity('Home')">
4. Twoja strona **home.html** będzie wyglądać tak:
   
        <html>
        <head>
            ...
        </head>
        <body onload="engagement.agent.startActivity('Home')">
            <script type="text/javascript" src="javascript/main.js"></script>
            <script type="text/javascript" src="javascript/azure-engagement.js"></script>
        </body>
        </html>

## <a name="connect-app-with-real-time-monitoring"></a>Łączenie aplikacji z funkcją monitorowania w czasie rzeczywistym
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

  ![][2]

## <a name="extend-analytics"></a>Poszerzanie analizy
W tym miejscu wszystkie metody hello są obecnie dostępne z zestawu SDK sieci Web służącego do analizy:

1. Działania/strony sieci Web:
   
        engagement.agent.startActivity(name);
        engagement.agent.endActivity();
2. Zdarzenia
   
        engagement.agent.sendEvent(name, extras);
3. Błędy
   
        engagement.agent.sendError(name, extras);
4. Zadania
   
        engagement.agent.startJob(name);
        engagement.agent.endJob(name);

<!-- Images. -->
[1]: ./media/mobile-engagement-web-app-get-started/visual-studio-solution-js.png
[2]: ./media/mobile-engagement-web-app-get-started/session.png

