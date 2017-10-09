---
title: aaaGet wprowadzenie testowanie w produkcji dla aplikacji sieci Web
description: "Więcej informacji na temat hello testu funkcji produkcji (TiP) w aplikacji sieci Web usługi aplikacji Azure."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 4623468d-886e-4203-8012-8f86deb2790b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/13/2016
ms.author: cephalin
ms.openlocfilehash: 2ddbd532ffe2a4f3e07fd386d9741a3fde3639ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-test-in-production-for-web-apps"></a>Rozpoczynanie pracy z testami w środowisku produkcyjnym dla usługi Web Apps
W środowisku produkcyjnym, albo na żywo — testowania aplikacji sieci web przy użyciu ruchu na żywo klienta jest strategię testu, w której deweloperzy aplikacji coraz zintegrować ich [elastyczne programowanie](https://en.wikipedia.org/wiki/Agile_software_development) metodologii. Umożliwia tootest hello jakości aplikacji z obsługą ruchu na żywo użytkownika w środowisku produkcyjnym jako min. toosynthesized danych w środowisku testowym. W przypadku wystawianego użytkownikom tooreal aplikacji, może być poinformowany hello rzeczywistych problemów, które aplikacji mogą się spodziewać po wdrożeniu. Można sprawdzić hello funkcji, wydajności i wartość aktualizacji aplikacji przed hello woluminu, szybkość pracy i różnych ruch rzeczywistego użytkownika, który nigdy nie można określić w przybliżeniu w środowisku testowym.

## <a name="traffic-routing-in-app-service-web-apps"></a>Ruch routingu w aplikacji sieci Web usługi aplikacji
Z hello routingu ruchu w narzędziu [usłudze Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714), można kierować część tooone ruchu na żywo użytkownika lub więcej [miejsc wdrożenia](web-sites-staged-publishing.md), a następnie analizować aplikacji za pomocą [aplikacji Azure Informacje na temat technologii](/services/application-insights/) lub [Azure HDInsight](/services/hdinsight/), lub narzędzie innej firmy, takich jak [usługi New Relic](/marketplace/partners/newrelic/newrelic/) toovalidate zmiany. Na przykład można zaimplementować hello następujące scenariusze z usługi aplikacji:

* Wykrywanie usterki funkcjonalności i wskazanie wąskich gardeł wydajności w danym wdrożeniu aktualizacji wcześniejszego całej toosite
* Wykonaj "lotach kontrolowane testu" zmiany poprzez pomiar użyteczność metryki na powitania aplikacji w wersji beta
* Stopniowo zwiększać tooa nową aktualizację, a następnie bezpiecznie z powrotem w dół toohello bieżącej wersji w przypadku wystąpienia błędu 
* Optymalizacja wyników biznesowych aplikacji przez uruchomienie [A / B testów](https://en.wikipedia.org/wiki/A/B_testing) lub [wielu zmiennych testy](https://en.wikipedia.org/wiki/Multivariate_testing_in_marketing) w wielu miejsc wdrożenia

### <a name="requirements-for-using-traffic-routing-in-web-apps"></a>Wymagania dotyczące używania funkcji routingu ruchu w aplikacjach sieci Web
* Aplikacja sieci web muszą działać w **standardowe** lub **Premium** warstwy, ponieważ jest wymagane dla wielu miejsc wdrożenia.
* W kolejności toowork poprawnie, Routing ruchu wymaga włączone w przeglądarce użytkownika hello toobe plików cookie. Routing ruchu używa plików cookie toopin miejsce wdrożenia klienta przeglądarki tooa hello życia powitania klienta sesji.
* Routing ruchu obsługuje zaawansowane scenariusze Porada za pomocą poleceń cmdlet programu Azure PowerShell.

## <a name="route-traffic-segment-tooa-deployment-slot"></a>Miejsce wdrożenia tooa segmentu ruch trasy
Na poziomie podstawowe hello w każdym scenariuszu poradę trasy jest wstępnie zdefiniowanych wartości procentowej miejsca wdrożenia nieprodukcyjnych tooa Twojego ruchu sieciowego na żywo. toodo, wykonaj hello czynności:

> [!NOTE]
> Witaj podanymi tu instrukcjami przyjęto założenie, że masz już [miejsce wdrożenia nieprodukcyjnych](web-sites-staged-publishing.md) i że hello zawartość aplikacji sieci web jest już [wdrożone](web-sites-deploy.md) tooit.
> 
> 

1. Zaloguj się do hello [Azure Portal](https://portal.azure.com/).
2. W bloku aplikacja sieci web, kliknij przycisk **ustawienia** > **routingu ruchu**.
   ![](./media/app-service-web-test-in-production/01-traffic-routing.png)
3. Wybierz hello miejsca, interesujące tooroute ruchu tooand hello procent hello ruch związany z konieczna, następnie kliknij przycisk **zapisać**.
   
    ![](./media/app-service-web-test-in-production/02-select-slot.png)
4. Miejsce wdrożenia Przejdź toohello bloku. Powinna zostać wyświetlona na żywo ruch jest kierowany tooit.
   
    ![](./media/app-service-web-test-in-production/03-traffic-routed.png)

Po skonfigurowaniu routingu ruchu hello określony odsetek klientów, będzie losowo routingiem tooyour miejsca nieprodukcyjnych. Jest jednak ważne toonote po tooa automatycznie routingiem określonych miejsca, klient będzie gniazdo toothat "przypiętych" hello życia tej sesji klienta. To zrobić przy użyciu pliku cookie sesji użytkownika hello toopin. Jeśli inspekcję żądań hello HTTP, można znaleźć `TipMix` plików cookie w wszystkich kolejnych żądań.

![](./media/app-service-web-test-in-production/04-tip-cookie.png)

## <a name="force-client-requests-tooa-specific-slot"></a>Wymuś miejsca określonego tooa żądania klienta
W routingu ruchu tooautomatic dodanie usługi aplikacji jest możliwe tooroute żądań tooa określonego miejsca. Jest to przydatne, jeśli chcesz, aby mogli użytkowników tooopt w toobe — do lub zrezygnować z aplikacji w wersji beta. toodo, użyj hello `x-ms-routing-name` parametr zapytania.

tooreroute użytkownicy tooa określone miejsce przy użyciu `x-ms-routing-name`, należy upewnić się, gniazdo hello została już dodana toohello listy routingu ruchu. Ponieważ jawnie ma miejsce tooa tooroute, hello rzeczywiste routingu procent, należy ustawić nie ma znaczenia. Jeśli chcesz, możesz sformułować "link beta", które użytkownik może kliknąć tooaccess hello aplikacji w wersji beta.

![](./media/app-service-web-test-in-production/06-enable-x-ms-routing-name.png)

### <a name="opt-users-out-of-beta-app"></a>Uczestnictwa użytkowników poza aplikacją w wersji beta
Użytkownicy toolet zrezygnować z aplikacji w wersji beta, na przykład można umieścić tego łącza na stronie sieci web:

    <a href="<webappname>.azurewebsites.net/?x-ms-routing-name=self">Go back tooproduction app</a>

ciąg Hello `x-ms-routing-name=self` określa hello miejsca produkcji. Po hello łącze hello dostępu do przeglądarki klienta, nie tylko jego przekierowanie gniazda produkcyjnego toohello, ale każde kolejne żądanie będzie zawierać hello `x-ms-routing-name=self` PIN gniazda produkcyjnego toohello sesji hello pliku cookie.

![](./media/app-service-web-test-in-production/05-access-production-slot.png)

### <a name="opt-users-in-toobeta-app"></a>Uczestnictwa użytkowników w aplikacji toobeta
Użytkownicy toolet zrezygnować w aplikacji w wersji beta tooyour, zestaw hello sam zapytania Nazwa parametru toohello hello nieprodukcyjnych gniazda, na przykład:

        <webappname>.azurewebsites.net/?x-ms-routing-name=staging

## <a name="more-resources"></a>Więcej zasobów
* [Konfigurowanie środowisk dla aplikacji sieci web w usłudze Azure App Service przejściowych](web-sites-staged-publishing.md)
* [Wdrażanie złożonych aplikacji przewidywalnego na platformie Azure](app-service-deploy-complex-application-predictably.md)
* [Programowanie zwinne oprogramowania z usługi aplikacji Azure](app-service-agile-software-development.md)
* [Wykorzystywać środowisk opracowywania oprogramowania dla aplikacji sieci web](app-service-web-staged-publishing-realworld-scenarios.md)

