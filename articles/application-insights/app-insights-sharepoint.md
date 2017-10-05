---
title: "Monitorowanie witryny programu SharePoint za pomocą usługi Application Insights"
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
ms.openlocfilehash: a3b37674469a131016f46af590e1eee3ba4cdc73
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-a-sharepoint-site-with-application-insights"></a><span data-ttu-id="3697e-103">Monitorowanie witryny programu SharePoint za pomocą usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="3697e-103">Monitor a SharePoint site with Application Insights</span></span>
<span data-ttu-id="3697e-104">Usługa Azure Application Insights monitoruje dostępność, wydajność i użycie Twoich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3697e-104">Azure Application Insights monitors the availability, performance and usage of your apps.</span></span> <span data-ttu-id="3697e-105">Tutaj dowiesz się, jak skonfigurować je dla witryny programu SharePoint.</span><span class="sxs-lookup"><span data-stu-id="3697e-105">Here you'll learn how to set it up for a SharePoint site.</span></span>

## <a name="create-an-application-insights-resource"></a><span data-ttu-id="3697e-106">Tworzenie zasobu usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="3697e-106">Create an Application Insights resource</span></span>
<span data-ttu-id="3697e-107">W witrynie [Azure Portal](https://portal.azure.com) utwórz nowy zasób usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="3697e-107">In the [Azure portal](https://portal.azure.com), create a new Application Insights resource.</span></span> <span data-ttu-id="3697e-108">Wybierz ASP.NET jako typ aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3697e-108">Choose ASP.NET as the application type.</span></span>

![Kliknij opcję Właściwości, zaznacz klucz i naciśnij klawisze Ctrl+C](./media/app-insights-sharepoint/01-new.png)

<span data-ttu-id="3697e-110">Blok, który zostanie otwarty, to miejsce, gdzie zobaczysz dane o wydajności i użyciu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3697e-110">The blade that opens is the place where you'll see performance and usage data about your app.</span></span> <span data-ttu-id="3697e-111">Aby wrócić do niego przy następnym logowaniu do platformy Azure, musisz znaleźć odpowiedni kafelek na ekranie startowym.</span><span class="sxs-lookup"><span data-stu-id="3697e-111">To get back to it next time you login to Azure, you should find a tile for it on the start screen.</span></span> <span data-ttu-id="3697e-112">Alternatywnie kliknij przycisk Przeglądaj, aby go znaleźć.</span><span class="sxs-lookup"><span data-stu-id="3697e-112">Alternatively click Browse to find it.</span></span>

## <a name="add-our-script-to-your-web-pages"></a><span data-ttu-id="3697e-113">Dodawanie naszego skryptu do stron sieci Web</span><span class="sxs-lookup"><span data-stu-id="3697e-113">Add our script to your web pages</span></span>
<span data-ttu-id="3697e-114">Ze strony Szybki start pobierz skrypt dla stron sieci Web:</span><span class="sxs-lookup"><span data-stu-id="3697e-114">In Quick Start, get the script for web pages:</span></span>

![](./media/app-insights-sharepoint/02-monitor-web-page.png)

<span data-ttu-id="3697e-115">Wstaw skrypt tuż przed tagiem &lt;/head&gt; na każdej stronie, którą chcesz śledzić. Jeśli witryna ma stronę wzorcową, możesz umieścić skrypt na tej stronie.</span><span class="sxs-lookup"><span data-stu-id="3697e-115">Insert the script just before the &lt;/head&gt; tag of every page you want to track. If your website has a master page, you can put the script there.</span></span> <span data-ttu-id="3697e-116">Na przykład w projekcie MVC programu ASP.NET możesz go umieścić w pliku View\Shared\_Layout.cshtml</span><span class="sxs-lookup"><span data-stu-id="3697e-116">For example, in an ASP.NET MVC project, you'd put it in View\Shared\_Layout.cshtml</span></span>

<span data-ttu-id="3697e-117">Skrypt zawiera klucz instrumentacji, który kieruje dane telemetryczne do zasobu usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="3697e-117">The script contains the instrumentation key that directs the telemetry to your Application Insights resource.</span></span>

### <a name="add-the-code-to-your-site-pages"></a><span data-ttu-id="3697e-118">Dodawanie kodu do stron witryny</span><span class="sxs-lookup"><span data-stu-id="3697e-118">Add the code to your site pages</span></span>
#### <a name="on-the-master-page"></a><span data-ttu-id="3697e-119">Na stronie wzorcowej</span><span class="sxs-lookup"><span data-stu-id="3697e-119">On the master page</span></span>
<span data-ttu-id="3697e-120">Jeśli możesz edytować stronę wzorcową witryny, będzie ona umożliwiać monitorowanie każdej strony witryny.</span><span class="sxs-lookup"><span data-stu-id="3697e-120">If you can edit the site's master page, that will provide monitoring for every page in the site.</span></span>

<span data-ttu-id="3697e-121">Wyrejestruj stronę wzorcową i edytuj ją za pomocą programu SharePoint Designer lub innego dowolnego edytora.</span><span class="sxs-lookup"><span data-stu-id="3697e-121">Check out the master page and edit it using SharePoint Designer or any other editor.</span></span>

![](./media/app-insights-sharepoint/03-master.png)

<span data-ttu-id="3697e-122">Dodaj kod przed tagiem </head>.</span><span class="sxs-lookup"><span data-stu-id="3697e-122">Add the code just before the </head> tag.</span></span> 

![](./media/app-insights-sharepoint/04-code.png)

#### <a name="or-on-individual-pages"></a><span data-ttu-id="3697e-123">Lub na poszczególnych stronach</span><span class="sxs-lookup"><span data-stu-id="3697e-123">Or on individual pages</span></span>
<span data-ttu-id="3697e-124">Aby monitorować ograniczony zestaw stron, dodaj skrypt oddzielnie do każdej strony.</span><span class="sxs-lookup"><span data-stu-id="3697e-124">To monitor a limited set of pages, add the script separately to each page.</span></span> 

<span data-ttu-id="3697e-125">Wstaw składnik Web Part i osadź w nim fragment kodu.</span><span class="sxs-lookup"><span data-stu-id="3697e-125">Insert a web part and embed the code snippet in it.</span></span>

![](./media/app-insights-sharepoint/05-page.png)

## <a name="view-data-about-your-app"></a><span data-ttu-id="3697e-126">Wyświetlanie danych aplikacji</span><span class="sxs-lookup"><span data-stu-id="3697e-126">View data about your app</span></span>
<span data-ttu-id="3697e-127">Ponownie wdróż aplikację.</span><span class="sxs-lookup"><span data-stu-id="3697e-127">Redeploy your app.</span></span>

<span data-ttu-id="3697e-128">Wróć do bloku aplikacji w witrynie [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3697e-128">Return to your application blade in the [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="3697e-129">Pierwsze zdarzenia będą wyświetlane w obszarze wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="3697e-129">The first events will appear in Search.</span></span> 

![](./media/app-insights-sharepoint/09-search.png)

<span data-ttu-id="3697e-130">Jeśli oczekujesz większej ilości danych, kliknij przycisk Odśwież po kilku sekundach.</span><span class="sxs-lookup"><span data-stu-id="3697e-130">Click Refresh after a few seconds if you're expecting more data.</span></span>

<span data-ttu-id="3697e-131">W bloku przeglądu kliknij pozycję **Analiza użycia**, aby wyświetlić wykresy dotyczące użytkowników, sesji i wyświetleń stron:</span><span class="sxs-lookup"><span data-stu-id="3697e-131">From the overview blade, click **Usage analytics** to see to charts of users, sessions and page views:</span></span>

![](./media/app-insights-sharepoint/06-usage.png)

<span data-ttu-id="3697e-132">Kliknij dowolny wykres, aby wyświetlić więcej szczegółów — na przykład wyświetlenia stron:</span><span class="sxs-lookup"><span data-stu-id="3697e-132">Click any chart to see more details - for example Page Views:</span></span>

![](./media/app-insights-sharepoint/07-pages.png)

<span data-ttu-id="3697e-133">Lub pozycję Użytkownicy:</span><span class="sxs-lookup"><span data-stu-id="3697e-133">Or Users:</span></span>

![](./media/app-insights-sharepoint/08-users.png)

## <a name="capturing-user-id"></a><span data-ttu-id="3697e-134">Przechwytywanie identyfikatora użytkownika</span><span class="sxs-lookup"><span data-stu-id="3697e-134">Capturing User Id</span></span>
<span data-ttu-id="3697e-135">Fragment kodu standardowej strony sieci Web nie przechwytuje identyfikatora użytkownika z programu SharePoint, ale możesz to zrobić za pomocą niewielkiej modyfikacji.</span><span class="sxs-lookup"><span data-stu-id="3697e-135">The standard web page code snippet doesn't capture the user id from SharePoint, but you can do that with a small modification.</span></span>

1. <span data-ttu-id="3697e-136">Skopiuj klucz instrumentacji aplikacji z listy rozwijanej Podstawy w usłudze Application Insights.</span><span class="sxs-lookup"><span data-stu-id="3697e-136">Copy your app's instrumentation key from the Essentials drop-down in Application Insights.</span></span> 

    ![](./media/app-insights-sharepoint/02-props.png)

1. <span data-ttu-id="3697e-137">Zastąp klucz instrumentacji ciągiem „XXXX” we fragmencie kodu poniżej.</span><span class="sxs-lookup"><span data-stu-id="3697e-137">Substitute the instrumentation key for 'XXXX' in the snippet below.</span></span> 
2. <span data-ttu-id="3697e-138">Osadź skrypt w aplikacji programu SharePoint zamiast fragmentu kodu pobranego z portalu.</span><span class="sxs-lookup"><span data-stu-id="3697e-138">Embed the script in your SharePoint app instead of the snippet you get from the portal.</span></span>

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



## <a name="next-steps"></a><span data-ttu-id="3697e-139">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3697e-139">Next Steps</span></span>
* <span data-ttu-id="3697e-140">[Testy sieci Web](app-insights-monitor-web-app-availability.md) do monitorowania dostępności witryny.</span><span class="sxs-lookup"><span data-stu-id="3697e-140">[Web tests](app-insights-monitor-web-app-availability.md) to monitor the availability of your site.</span></span>
* <span data-ttu-id="3697e-141">[Usługa Application Insights](app-insights-overview.md) dla innych typów aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3697e-141">[Application Insights](app-insights-overview.md) for other types of app.</span></span>

<!--Link references-->


