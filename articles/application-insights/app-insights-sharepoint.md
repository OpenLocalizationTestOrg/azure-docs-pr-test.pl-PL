---
title: "aaaMonitor witryny programu SharePoint za pomocą usługi Application Insights"
description: "Rozpocznij monitorowanie nowej aplikacji przy użyciu nowego klucza instrumentacji"
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 2bfe5910-d673-4cf6-a5c1-4c115eae1be0
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/24/2016
ms.author: bwren
ms.openlocfilehash: acfe99c24a4d77daec1017de0442ec952a1faba2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-sharepoint-site-with-application-insights"></a>Monitorowanie witryny programu SharePoint za pomocą usługi Application Insights
Azure Application Insights monitorów hello dostępności, wydajności i użycia aplikacji. Tutaj dowiesz się, jak tooset go do witryny programu SharePoint.

## <a name="create-an-application-insights-resource"></a>Tworzenie zasobu usługi Application Insights
W hello [portalu Azure](https://portal.azure.com), Utwórz nowy zasób usługi Application Insights. Wybierz platformy ASP.NET, jako typ aplikacji hello.

![Kliknij polecenie Właściwości, wybierz hello klucza, a następnie naciśnij klawisze ctrl + C](./media/app-insights-sharepoint/01-new.png)

Blok Hello, którego kliknięcie spowoduje otwarcie jest hello miejsce, gdy pojawi się dane wydajności i użycia dotyczące Twojej aplikacji. tooget tooit wstecz następnym logowaniu tooAzure, należy odnaleźć kafelka dla niego na ekranie startowym hello. Alternatywnie kliknij przycisk Przeglądaj toofind go.

## <a name="add-our-script-tooyour-web-pages"></a>Dodaj stronach sieci web tooyour skryptu
W Szybki Start Pobierz hello skryptu dla stron sieci web:

![](./media/app-insights-sharepoint/02-monitor-web-page.png)

Wstaw skrypt hello tuż przed hello &lt;/head&gt; tag każdej strony ma tootrack. Jeśli strony głównej witryny sieci Web, można umieścić hello skryptu. Na przykład w projekcie MVC programu ASP.NET możesz go umieścić w pliku View\Shared\_Layout.cshtml

skrypt Hello zawiera klucz Instrumentacji hello kieruje zasobu usługi Application Insights tooyour telemetrii hello.

### <a name="add-hello-code-tooyour-site-pages"></a>Dodaj hello kodowe tooyour lokacji
#### <a name="on-hello-master-page"></a>Na stronie wzorcowej hello
Czy można edytować strony wzorcowej hello witryny, które zapewniają, monitorowanie dla każdej strony w witrynie hello.

Strona wzorcowa hello do edycji przy użyciu programu SharePoint Designer lub inny edytor.

![](./media/app-insights-sharepoint/03-master.png)

Dodaj kod hello tuż przed hello </head> tagu. 

![](./media/app-insights-sharepoint/04-code.png)

#### <a name="or-on-individual-pages"></a>Lub na poszczególnych stronach
toomonitor ograniczony zestaw stron, dodać skrypt hello osobno tooeach strony. 

Wstaw części sieci web i osadzone hello fragment kodu.

![](./media/app-insights-sharepoint/05-page.png)

## <a name="view-data-about-your-app"></a>Wyświetlanie danych aplikacji
Ponownie wdróż aplikację.

Zwracany tooyour bloku aplikacji w hello [portalu Azure](https://portal.azure.com).

pierwsze zdarzenia Hello będzie w wynikach wyszukiwania. 

![](./media/app-insights-sharepoint/09-search.png)

Jeśli oczekujesz większej ilości danych, kliknij przycisk Odśwież po kilku sekundach.

W bloku omówienie hello, kliknij **analizy użycia** toocharts toosee użytkowników, sesji i wyświetleń strony:

![](./media/app-insights-sharepoint/06-usage.png)

Kliknij żadnych toosee wykresu więcej szczegółów — na przykład wyświetleń strony:

![](./media/app-insights-sharepoint/07-pages.png)

Lub pozycję Użytkownicy:

![](./media/app-insights-sharepoint/08-users.png)

## <a name="capturing-user-id"></a>Przechwytywanie identyfikatora użytkownika
fragment kodu Hello standardowe strony sieci web nie przechwytuje hello identyfikator użytkownika z programu SharePoint, ale możesz to zrobić z małych modyfikacji.

1. Kopiowanie klucza instrumentacji aplikacji z hello Essentials listy rozwijanej w usłudze Application Insights. 

    ![](./media/app-insights-sharepoint/02-props.png)

1. Zastąp klucza Instrumentacji hello "XXXX" we fragmencie hello poniżej. 
2. Osadź hello skryptu w aplikacji SharePoint zamiast fragment hello, uzyskasz hello portalu.

```


<SharePoint:ScriptLink ID="ScriptLink1" name="SP.js" runat="server" localizable="false" loadafterui="true" /> 
<SharePoint:ScriptLink ID="ScriptLink2" name="SP.UserProfiles.js" runat="server" localizable="false" loadafterui="true" /> 

<script type="text/javascript"> 
var personProperties; 

// Ensure that hello SP.UserProfiles.js file is loaded before hello custom code runs. 
SP.SOD.executeOrDelayUntilScriptLoaded(getUserProperties, 'SP.UserProfiles.js'); 

function getUserProperties() { 
    // Get hello current client context and PeopleManager instance. 
    var clientContext = new SP.ClientContext.get_current(); 
    var peopleManager = new SP.UserProfiles.PeopleManager(clientContext); 

    // Get user properties for hello target user. 
    // tooget hello PersonProperties object for hello current user, use hello 
    // getMyProperties method. 

    personProperties = peopleManager.getMyProperties(); 

    // Load hello PersonProperties object and send hello request. 
    clientContext.load(personProperties); 
    clientContext.executeQueryAsync(onRequestSuccess, onRequestFail); 
} 

// This function runs if hello executeQueryAsync call succeeds. 
function onRequestSuccess() { 
var appInsights=window.appInsights||function(config){
function s(config){t[config]=function(){var i=arguments;t.queue.push(function(){t[config].apply(t,i)})}}var t={config:config},r=document,f=window,e="script",o=r.createElement(e),i,u;for(o.src=config.url||"//az416426.vo.msecnd.net/scripts/a/ai.0.js",r.getElementsByTagName(e)[0].parentNode.appendChild(o),t.cookie=r.cookie,t.queue=[],i=["Event","Exception","Metric","PageView","Trace"];i.length;)s("track"+i.pop());return config.disableExceptionTracking||(i="onerror",s("_"+i),u=f[i],f[i]=function(config,r,f,e,o){var s=u&&u(config,r,f,e,o);return s!==!0&&t["_"+i](config,r,f,e,o),s}),t
    }({
        instrumentationKey:"XXXX"
    });
    window.appInsights=appInsights;
    appInsights.trackPageView(document.title,window.location.href, {User: personProperties.get_displayName()});
} 

// This function runs if hello executeQueryAsync call fails. 
function onRequestFail(sender, args) { 
} 
</script> 


```



## <a name="next-steps"></a>Następne kroki
* [Testów sieci Web](app-insights-monitor-web-app-availability.md) toomonitor hello dostępności witryny.
* [Usługa Application Insights](app-insights-overview.md) dla innych typów aplikacji.

<!--Link references-->


