---
title: "Monitorowanie witryny programu SharePoint za pomocą usługi Application Insights"
description: "Rozpocznij monitorowanie nowej aplikacji przy użyciu nowego klucza instrumentacji"
services: application-insights
documentationcenter: 
author: mrbullwinkle
manager: carmonm
ms.assetid: 2bfe5910-d673-4cf6-a5c1-4c115eae1be0
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/24/2016
ms.author: mbullwin
ms.openlocfilehash: 9c07ba125e0f9eae2b8f94661abf6dc1efc0cdad
ms.sourcegitcommit: e462e5cca2424ce36423f9eff3a0cf250ac146ad
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/01/2017
---
# <a name="monitor-a-sharepoint-site-with-application-insights"></a>Monitorowanie witryny programu SharePoint za pomocą usługi Application Insights
Usługa Azure Application Insights monitoruje dostępność, wydajność i użycie Twoich aplikacji. Tutaj dowiesz się, jak skonfigurować je dla witryny programu SharePoint.

## <a name="create-an-application-insights-resource"></a>Tworzenie zasobu usługi Application Insights
W witrynie [Azure Portal](https://portal.azure.com) utwórz nowy zasób usługi Application Insights. Wybierz ASP.NET jako typ aplikacji.

![Kliknij opcję Właściwości, zaznacz klucz i naciśnij klawisze Ctrl+C](./media/app-insights-sharepoint/01-new.png)

Blok, który zostanie otwarty, to miejsce, gdzie zobaczysz dane o wydajności i użyciu aplikacji. Aby wrócić do niego przy następnym logowaniu do platformy Azure, musisz znaleźć odpowiedni kafelek na ekranie startowym. Alternatywnie kliknij przycisk Przeglądaj, aby go znaleźć.

## <a name="add-our-script-to-your-web-pages"></a>Dodawanie naszego skryptu do stron sieci Web
Ze strony Szybki start pobierz skrypt dla stron sieci Web:

![](./media/app-insights-sharepoint/02-monitor-web-page.png)

Wstaw skrypt tuż przed tagiem &lt;/head&gt; na każdej stronie, którą chcesz śledzić. Jeśli witryna ma stronę wzorcową, możesz umieścić skrypt na tej stronie. Na przykład w projekcie MVC programu ASP.NET możesz go umieścić w pliku View\Shared\_Layout.cshtml

Skrypt zawiera klucz instrumentacji, który kieruje dane telemetryczne do zasobu usługi Application Insights.

### <a name="add-the-code-to-your-site-pages"></a>Dodawanie kodu do stron witryny
#### <a name="on-the-master-page"></a>Na stronie wzorcowej
Jeśli możesz edytować stronę wzorcową witryny, będzie ona umożliwiać monitorowanie każdej strony witryny.

Wyrejestruj stronę wzorcową i edytuj ją za pomocą programu SharePoint Designer lub innego dowolnego edytora.

![](./media/app-insights-sharepoint/03-master.png)

Dodaj kod przed tagiem </head>. 

![](./media/app-insights-sharepoint/04-code.png)

#### <a name="or-on-individual-pages"></a>Lub na poszczególnych stronach
Aby monitorować ograniczony zestaw stron, dodaj skrypt oddzielnie do każdej strony. 

Wstaw składnik Web Part i osadź w nim fragment kodu.

![](./media/app-insights-sharepoint/05-page.png)

## <a name="view-data-about-your-app"></a>Wyświetlanie danych aplikacji
Ponownie wdróż aplikację.

Wróć do bloku aplikacji w witrynie [Azure Portal](https://portal.azure.com).

Pierwsze zdarzenia będą wyświetlane w obszarze wyszukiwania. 

![](./media/app-insights-sharepoint/09-search.png)

Jeśli oczekujesz większej ilości danych, kliknij przycisk Odśwież po kilku sekundach.

W bloku przeglądu kliknij pozycję **Analiza użycia**, aby wyświetlić wykresy dotyczące użytkowników, sesji i wyświetleń stron:

![](./media/app-insights-sharepoint/06-usage.png)

Kliknij dowolny wykres, aby wyświetlić więcej szczegółów — na przykład wyświetlenia stron:

![](./media/app-insights-sharepoint/07-pages.png)

Lub pozycję Użytkownicy:

![](./media/app-insights-sharepoint/08-users.png)

## <a name="capturing-user-id"></a>Przechwytywanie identyfikatora użytkownika
Fragment kodu standardowej strony sieci Web nie przechwytuje identyfikatora użytkownika z programu SharePoint, ale możesz to zrobić za pomocą niewielkiej modyfikacji.

1. Skopiuj klucz instrumentacji aplikacji z listy rozwijanej Podstawy w usłudze Application Insights. 

    ![](./media/app-insights-sharepoint/02-props.png)

1. Zastąp klucz instrumentacji ciągiem „XXXX” we fragmencie kodu poniżej. 
2. Osadź skrypt w aplikacji programu SharePoint zamiast fragmentu kodu pobranego z portalu.

```


<SharePoint:ScriptLink ID="ScriptLink1" name="SP.js" runat="server" localizable="false" loadafterui="true" /> 
<SharePoint:ScriptLink ID="ScriptLink2" name="SP.UserProfiles.js" runat="server" localizable="false" loadafterui="true" /> 

<script type="text/javascript"> 
var personProperties; 

// Ensure that the SP.UserProfiles.js file is loaded before the custom code runs. 
SP.SOD.executeOrDelayUntilScriptLoaded(getUserProperties, 'SP.UserProfiles.js'); 

function getUserProperties() { 
    // Get the current client context and PeopleManager instance. 
    var clientContext = new SP.ClientContext.get_current(); 
    var peopleManager = new SP.UserProfiles.PeopleManager(clientContext); 

    // Get user properties for the target user. 
    // To get the PersonProperties object for the current user, use the 
    // getMyProperties method. 

    personProperties = peopleManager.getMyProperties(); 

    // Load the PersonProperties object and send the request. 
    clientContext.load(personProperties); 
    clientContext.executeQueryAsync(onRequestSuccess, onRequestFail); 
} 

// This function runs if the executeQueryAsync call succeeds. 
function onRequestSuccess() { 
var appInsights=window.appInsights||function(config){
function s(config){t[config]=function(){var i=arguments;t.queue.push(function(){t[config].apply(t,i)})}}var t={config:config},r=document,f=window,e="script",o=r.createElement(e),i,u;for(o.src=config.url||"//az416426.vo.msecnd.net/scripts/a/ai.0.js",r.getElementsByTagName(e)[0].parentNode.appendChild(o),t.cookie=r.cookie,t.queue=[],i=["Event","Exception","Metric","PageView","Trace"];i.length;)s("track"+i.pop());return config.disableExceptionTracking||(i="onerror",s("_"+i),u=f[i],f[i]=function(config,r,f,e,o){var s=u&&u(config,r,f,e,o);return s!==!0&&t["_"+i](config,r,f,e,o),s}),t
    }({
        instrumentationKey:"XXXX"
    });
    window.appInsights=appInsights;
    appInsights.trackPageView(document.title,window.location.href, {User: personProperties.get_displayName()});
} 

// This function runs if the executeQueryAsync call fails. 
function onRequestFail(sender, args) { 
} 
</script> 


```



## <a name="next-steps"></a>Następne kroki
* [Testy sieci Web](app-insights-monitor-web-app-availability.md) do monitorowania dostępności witryny.
* [Usługa Application Insights](app-insights-overview.md) dla innych typów aplikacji.

<!--Link references-->


