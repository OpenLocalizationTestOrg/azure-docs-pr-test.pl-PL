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
# <a name="monitor-a-sharepoint-site-with-application-insights"></a><span data-ttu-id="8fd8b-103">Monitorowanie witryny programu SharePoint za pomocą usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="8fd8b-103">Monitor a SharePoint site with Application Insights</span></span>
<span data-ttu-id="8fd8b-104">Azure Application Insights monitorów hello dostępności, wydajności i użycia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8fd8b-104">Azure Application Insights monitors hello availability, performance and usage of your apps.</span></span> <span data-ttu-id="8fd8b-105">Tutaj dowiesz się, jak tooset go do witryny programu SharePoint.</span><span class="sxs-lookup"><span data-stu-id="8fd8b-105">Here you'll learn how tooset it up for a SharePoint site.</span></span>

## <a name="create-an-application-insights-resource"></a><span data-ttu-id="8fd8b-106">Tworzenie zasobu usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="8fd8b-106">Create an Application Insights resource</span></span>
<span data-ttu-id="8fd8b-107">W hello [portalu Azure](https://portal.azure.com), Utwórz nowy zasób usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="8fd8b-107">In hello [Azure portal](https://portal.azure.com), create a new Application Insights resource.</span></span> <span data-ttu-id="8fd8b-108">Wybierz platformy ASP.NET, jako typ aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="8fd8b-108">Choose ASP.NET as hello application type.</span></span>

![Kliknij polecenie Właściwości, wybierz hello klucza, a następnie naciśnij klawisze ctrl + C](./media/app-insights-sharepoint/01-new.png)

<span data-ttu-id="8fd8b-110">Blok Hello, którego kliknięcie spowoduje otwarcie jest hello miejsce, gdy pojawi się dane wydajności i użycia dotyczące Twojej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8fd8b-110">hello blade that opens is hello place where you'll see performance and usage data about your app.</span></span> <span data-ttu-id="8fd8b-111">tooget tooit wstecz następnym logowaniu tooAzure, należy odnaleźć kafelka dla niego na ekranie startowym hello.</span><span class="sxs-lookup"><span data-stu-id="8fd8b-111">tooget back tooit next time you login tooAzure, you should find a tile for it on hello start screen.</span></span> <span data-ttu-id="8fd8b-112">Alternatywnie kliknij przycisk Przeglądaj toofind go.</span><span class="sxs-lookup"><span data-stu-id="8fd8b-112">Alternatively click Browse toofind it.</span></span>

## <a name="add-our-script-tooyour-web-pages"></a><span data-ttu-id="8fd8b-113">Dodaj stronach sieci web tooyour skryptu</span><span class="sxs-lookup"><span data-stu-id="8fd8b-113">Add our script tooyour web pages</span></span>
<span data-ttu-id="8fd8b-114">W Szybki Start Pobierz hello skryptu dla stron sieci web:</span><span class="sxs-lookup"><span data-stu-id="8fd8b-114">In Quick Start, get hello script for web pages:</span></span>

![](./media/app-insights-sharepoint/02-monitor-web-page.png)

<span data-ttu-id="8fd8b-115">Wstaw skrypt hello tuż przed hello &lt;/head&gt; tag każdej strony ma tootrack.</span><span class="sxs-lookup"><span data-stu-id="8fd8b-115">Insert hello script just before hello &lt;/head&gt; tag of every page you want tootrack.</span></span> <span data-ttu-id="8fd8b-116">Jeśli strony głównej witryny sieci Web, można umieścić hello skryptu.</span><span class="sxs-lookup"><span data-stu-id="8fd8b-116">If your website has a master page, you can put hello script there.</span></span> <span data-ttu-id="8fd8b-117">Na przykład w projekcie MVC programu ASP.NET możesz go umieścić w pliku View\Shared\_Layout.cshtml</span><span class="sxs-lookup"><span data-stu-id="8fd8b-117">For example, in an ASP.NET MVC project, you'd put it in View\Shared\_Layout.cshtml</span></span>

<span data-ttu-id="8fd8b-118">skrypt Hello zawiera klucz Instrumentacji hello kieruje zasobu usługi Application Insights tooyour telemetrii hello.</span><span class="sxs-lookup"><span data-stu-id="8fd8b-118">hello script contains hello instrumentation key that directs hello telemetry tooyour Application Insights resource.</span></span>

### <a name="add-hello-code-tooyour-site-pages"></a><span data-ttu-id="8fd8b-119">Dodaj hello kodowe tooyour lokacji</span><span class="sxs-lookup"><span data-stu-id="8fd8b-119">Add hello code tooyour site pages</span></span>
#### <a name="on-hello-master-page"></a><span data-ttu-id="8fd8b-120">Na stronie wzorcowej hello</span><span class="sxs-lookup"><span data-stu-id="8fd8b-120">On hello master page</span></span>
<span data-ttu-id="8fd8b-121">Czy można edytować strony wzorcowej hello witryny, które zapewniają, monitorowanie dla każdej strony w witrynie hello.</span><span class="sxs-lookup"><span data-stu-id="8fd8b-121">If you can edit hello site's master page, that will provide monitoring for every page in hello site.</span></span>

<span data-ttu-id="8fd8b-122">Strona wzorcowa hello do edycji przy użyciu programu SharePoint Designer lub inny edytor.</span><span class="sxs-lookup"><span data-stu-id="8fd8b-122">Check out hello master page and edit it using SharePoint Designer or any other editor.</span></span>

![](./media/app-insights-sharepoint/03-master.png)

<span data-ttu-id="8fd8b-123">Dodaj kod hello tuż przed hello </head> tagu.</span><span class="sxs-lookup"><span data-stu-id="8fd8b-123">Add hello code just before hello </head> tag.</span></span> 

![](./media/app-insights-sharepoint/04-code.png)

#### <a name="or-on-individual-pages"></a><span data-ttu-id="8fd8b-124">Lub na poszczególnych stronach</span><span class="sxs-lookup"><span data-stu-id="8fd8b-124">Or on individual pages</span></span>
<span data-ttu-id="8fd8b-125">toomonitor ograniczony zestaw stron, dodać skrypt hello osobno tooeach strony.</span><span class="sxs-lookup"><span data-stu-id="8fd8b-125">toomonitor a limited set of pages, add hello script separately tooeach page.</span></span> 

<span data-ttu-id="8fd8b-126">Wstaw części sieci web i osadzone hello fragment kodu.</span><span class="sxs-lookup"><span data-stu-id="8fd8b-126">Insert a web part and embed hello code snippet in it.</span></span>

![](./media/app-insights-sharepoint/05-page.png)

## <a name="view-data-about-your-app"></a><span data-ttu-id="8fd8b-127">Wyświetlanie danych aplikacji</span><span class="sxs-lookup"><span data-stu-id="8fd8b-127">View data about your app</span></span>
<span data-ttu-id="8fd8b-128">Ponownie wdróż aplikację.</span><span class="sxs-lookup"><span data-stu-id="8fd8b-128">Redeploy your app.</span></span>

<span data-ttu-id="8fd8b-129">Zwracany tooyour bloku aplikacji w hello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8fd8b-129">Return tooyour application blade in hello [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="8fd8b-130">pierwsze zdarzenia Hello będzie w wynikach wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="8fd8b-130">hello first events will appear in Search.</span></span> 

![](./media/app-insights-sharepoint/09-search.png)

<span data-ttu-id="8fd8b-131">Jeśli oczekujesz większej ilości danych, kliknij przycisk Odśwież po kilku sekundach.</span><span class="sxs-lookup"><span data-stu-id="8fd8b-131">Click Refresh after a few seconds if you're expecting more data.</span></span>

<span data-ttu-id="8fd8b-132">W bloku omówienie hello, kliknij **analizy użycia** toocharts toosee użytkowników, sesji i wyświetleń strony:</span><span class="sxs-lookup"><span data-stu-id="8fd8b-132">From hello overview blade, click **Usage analytics** toosee toocharts of users, sessions and page views:</span></span>

![](./media/app-insights-sharepoint/06-usage.png)

<span data-ttu-id="8fd8b-133">Kliknij żadnych toosee wykresu więcej szczegółów — na przykład wyświetleń strony:</span><span class="sxs-lookup"><span data-stu-id="8fd8b-133">Click any chart toosee more details - for example Page Views:</span></span>

![](./media/app-insights-sharepoint/07-pages.png)

<span data-ttu-id="8fd8b-134">Lub pozycję Użytkownicy:</span><span class="sxs-lookup"><span data-stu-id="8fd8b-134">Or Users:</span></span>

![](./media/app-insights-sharepoint/08-users.png)

## <a name="capturing-user-id"></a><span data-ttu-id="8fd8b-135">Przechwytywanie identyfikatora użytkownika</span><span class="sxs-lookup"><span data-stu-id="8fd8b-135">Capturing User Id</span></span>
<span data-ttu-id="8fd8b-136">fragment kodu Hello standardowe strony sieci web nie przechwytuje hello identyfikator użytkownika z programu SharePoint, ale możesz to zrobić z małych modyfikacji.</span><span class="sxs-lookup"><span data-stu-id="8fd8b-136">hello standard web page code snippet doesn't capture hello user id from SharePoint, but you can do that with a small modification.</span></span>

1. <span data-ttu-id="8fd8b-137">Kopiowanie klucza instrumentacji aplikacji z hello Essentials listy rozwijanej w usłudze Application Insights.</span><span class="sxs-lookup"><span data-stu-id="8fd8b-137">Copy your app's instrumentation key from hello Essentials drop-down in Application Insights.</span></span> 

    ![](./media/app-insights-sharepoint/02-props.png)

1. <span data-ttu-id="8fd8b-138">Zastąp klucza Instrumentacji hello "XXXX" we fragmencie hello poniżej.</span><span class="sxs-lookup"><span data-stu-id="8fd8b-138">Substitute hello instrumentation key for 'XXXX' in hello snippet below.</span></span> 
2. <span data-ttu-id="8fd8b-139">Osadź hello skryptu w aplikacji SharePoint zamiast fragment hello, uzyskasz hello portalu.</span><span class="sxs-lookup"><span data-stu-id="8fd8b-139">Embed hello script in your SharePoint app instead of hello snippet you get from hello portal.</span></span>

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



## <a name="next-steps"></a><span data-ttu-id="8fd8b-140">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8fd8b-140">Next Steps</span></span>
* <span data-ttu-id="8fd8b-141">[Testów sieci Web](app-insights-monitor-web-app-availability.md) toomonitor hello dostępności witryny.</span><span class="sxs-lookup"><span data-stu-id="8fd8b-141">[Web tests](app-insights-monitor-web-app-availability.md) toomonitor hello availability of your site.</span></span>
* <span data-ttu-id="8fd8b-142">[Usługa Application Insights](app-insights-overview.md) dla innych typów aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8fd8b-142">[Application Insights](app-insights-overview.md) for other types of app.</span></span>

<!--Link references-->


