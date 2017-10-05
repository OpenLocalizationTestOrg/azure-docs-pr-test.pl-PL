---
title: "Stan sesji i usługa Azure Redis Cache w usłudze Azure App Service"
description: "Dowiedz się, jak używać usługi Azure Redis Cache do obsługi buforowania informacji o stanie sesji programu ASP.NET."
services: app-service\web
documentationcenter: .net
author: Rick-Anderson
manager: erikre
editor: none
ms.assetid: 4f98d289-2698-464d-85cd-99ec40fad1f2
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: get-started-article
ms.date: 06/27/2016
ms.author: riande
ms.openlocfilehash: 64fa909daf92b2b1f0cf4c7b334edba807fe7228
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="session-state-with-azure-redis-cache-in-azure-app-service"></a><span data-ttu-id="2cb31-103">Stan sesji i usługa Azure Redis Cache w usłudze Azure App Service</span><span class="sxs-lookup"><span data-stu-id="2cb31-103">Session state with Azure Redis cache in Azure App Service</span></span>
<span data-ttu-id="2cb31-104">W tym temacie wyjaśniono, jak używać usługi Azure Redis Cache do buforowania informacji o stanie sesji.</span><span class="sxs-lookup"><span data-stu-id="2cb31-104">This topic explains how to use the Azure Redis Cache Service for session state.</span></span>

<span data-ttu-id="2cb31-105">Jeśli aplikacja sieci Web programu ASP.NET używa informacji o stanie sesji, należy skonfigurować zewnętrznego dostawcę stanu sesji (usługę Azure Redis Cache lub dostawcę stanu sesji programu SQL Server).</span><span class="sxs-lookup"><span data-stu-id="2cb31-105">If your ASP.NET web app uses session state, you will need to configure an external session state provider (either the Redis Cache Service or a SQL Server session state provider).</span></span> <span data-ttu-id="2cb31-106">Jeśli korzystasz z informacji o stanie sesji i nie używasz dostawcy zewnętrznego, obowiązuje ograniczenie do pojedynczego wystąpienia aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="2cb31-106">If you use session state, and don't use an external provider, you will be limited to one instance of your web app.</span></span> <span data-ttu-id="2cb31-107">Użycie usługi Azure Redis Cache jest najszybszym i najprostszym sposobem zapewnienia tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="2cb31-107">The Redis Cache Service is the fastest and simplest to enable.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <span data-ttu-id="2cb31-108"><a id="createcache"></a>Tworzenie pamięci podręcznej</span><span class="sxs-lookup"><span data-stu-id="2cb31-108"><a id="createcache"></a>Create the Cache</span></span>
<span data-ttu-id="2cb31-109">Wykonaj [te kroki](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#create-cache), aby utworzyć pamięć podręczną.</span><span class="sxs-lookup"><span data-stu-id="2cb31-109">Follow [these directions](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#create-cache) to create the cache.</span></span>

## <span data-ttu-id="2cb31-110"><a id="configureproject"></a>Dodawanie pakietu RedisSessionStateProvider NuGet do aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="2cb31-110"><a id="configureproject"></a>Add the RedisSessionStateProvider NuGet package to your web app</span></span>
<span data-ttu-id="2cb31-111">Zainstaluj pakiet NuGet `RedisSessionStateProvider`.</span><span class="sxs-lookup"><span data-stu-id="2cb31-111">Install the NuGet `RedisSessionStateProvider` package.</span></span>  <span data-ttu-id="2cb31-112">Użyj następującego polecenia do instalacji z poziomu konsoli menedżera pakietów (**Narzędzia** > **Menedżer pakietów NuGet** > **Konsola menedżera pakietów**):</span><span class="sxs-lookup"><span data-stu-id="2cb31-112">Use the following command to install from the package manager console (**Tools** > **NuGet Package Manager** > **Package Manager Console**):</span></span>

  `PM> Install-Package Microsoft.Web.RedisSessionStateProvider`

<span data-ttu-id="2cb31-113">Aby zainstalować z lokalizacji **Narzędzia** > **Menedżer pakietów NuGet** > **Zarządzaj pakietami NugGet dla rozwiązania**, wyszukaj `RedisSessionStateProvider`.</span><span class="sxs-lookup"><span data-stu-id="2cb31-113">To install from **Tools** > **NuGet Package Manager** > **Manage NugGet Packages for Solution**, search for `RedisSessionStateProvider`.</span></span>

<span data-ttu-id="2cb31-114">Aby uzyskać więcej informacji, zapoznaj się ze [stroną pakietu NuGet RedisSessionStateProvider](http://www.nuget.org/packages/Microsoft.Web.RedisSessionStateProvider/) i sekcją [Configure the cache client](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#NuGet) (Konfigurowanie klienta pamięci podręcznej).</span><span class="sxs-lookup"><span data-stu-id="2cb31-114">For more information see the [NuGet RedisSessionStateProvider page](http://www.nuget.org/packages/Microsoft.Web.RedisSessionStateProvider/) and [Configure the cache client](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#NuGet).</span></span>

## <span data-ttu-id="2cb31-115"><a id="configurewebconfig"></a>Modyfikowanie pliku Web.Config</span><span class="sxs-lookup"><span data-stu-id="2cb31-115"><a id="configurewebconfig"></a>Modify the Web.Config File</span></span>
<span data-ttu-id="2cb31-116">Oprócz tworzenia odwołań do zestawów dla pamięci podręcznej pakiet NuGet dodaje wpisy zastępcze w pliku *web.config*.</span><span class="sxs-lookup"><span data-stu-id="2cb31-116">In addition to making assembly references for Cache, the NuGet package adds stub entries in the *web.config* file.</span></span> 

1. <span data-ttu-id="2cb31-117">Otwórz plik *web.config* i znajdź element **sessionState**.</span><span class="sxs-lookup"><span data-stu-id="2cb31-117">Open the *web.config* and find the the **sessionState** element.</span></span>
2. <span data-ttu-id="2cb31-118">Wprowadź wartości dla `host`, `accessKey`, `port` (wymagany jest port SSL 6380) i ustaw opcję `SSL` na `true`.</span><span class="sxs-lookup"><span data-stu-id="2cb31-118">Enter the values for `host`, `accessKey`, `port` (the SSL port should be 6380), and set `SSL` to `true`.</span></span> <span data-ttu-id="2cb31-119">Te wartości można uzyskać z bloku witryny [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715) dotyczącego wystąpienia pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="2cb31-119">These values can be obtained from the [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715) blade for your cache instance.</span></span> <span data-ttu-id="2cb31-120">Aby uzyskać więcej informacji, zobacz sekcję [Connect to the cache](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#connect-to-cache) (Nawiązywanie połączenia z pamięcią podręczną).</span><span class="sxs-lookup"><span data-stu-id="2cb31-120">For more information, see [Connect to the cache](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#connect-to-cache).</span></span> <span data-ttu-id="2cb31-121">Port bez protokołu SSL jest domyślnie wyłączony w przypadku nowych pamięci podręcznych.</span><span class="sxs-lookup"><span data-stu-id="2cb31-121">Note that the non-SSL port is disabled by default for new caches.</span></span> <span data-ttu-id="2cb31-122">Aby uzyskać więcej informacji na temat włączania portu bez protokołu SSL, zobacz sekcję [Access Ports](https://msdn.microsoft.com/library/azure/dn793612.aspx#AccessPorts) (Porty dostępowe) w temacie [Configure a cache in Azure Redis Cache](https://msdn.microsoft.com/library/azure/dn793612.aspx) (Konfigurowanie pamięci podręcznej w usłudze Azure Redis Cache).</span><span class="sxs-lookup"><span data-stu-id="2cb31-122">For more information about enabling the non-SSL port, see the [Access Ports](https://msdn.microsoft.com/library/azure/dn793612.aspx#AccessPorts) section in the [Configure a cache in Azure Redis Cache](https://msdn.microsoft.com/library/azure/dn793612.aspx) topic.</span></span> <span data-ttu-id="2cb31-123">Następujący kod przedstawia zmiany *web.config* pliku, w szczególności zmiany *portu*, *hosta*, accessKey * i *ssl* .</span><span class="sxs-lookup"><span data-stu-id="2cb31-123">The following markup shows the changes to the *web.config* file, specifically the changes to *port*, *host*, accessKey*, and *ssl*.</span></span>
   
          <system.web>;
            <customErrors mode="Off" />;
            <authentication mode="None" />;
            <compilation debug="true" targetFramework="4.5" />;
            <httpRuntime targetFramework="4.5" />;
            <sessionState mode="Custom" customProvider="RedisSessionProvider">;
              <providers>;  
                  <!--<add name="RedisSessionProvider" 
                    host = "127.0.0.1" [String]
                    port = "" [number]
                    accessKey = "" [String]
                    ssl = "false" [true|false]
                    throwOnError = "true" [true|false]
                    retryTimeoutInMilliseconds = "0" [number]
                    databaseId = "0" [number]
                    applicationName = "" [String]
                  />;-->;
                 <add name="RedisSessionProvider" 
                      type="Microsoft.Web.Redis.RedisSessionStateProvider" 
                      port="6380"
                      host="movie2.redis.cache.windows.net" 
                      accessKey="m7PNV60CrvKpLqMUxosC3dSe6kx9nQ6jP5del8TmADk=" 
                      ssl="true" />;
              <!--<add name="MySessionStateStore" type="Microsoft.Web.Redis.RedisSessionStateProvider" host="127.0.0.1" accessKey="" ssl="false" />;-->;
              </providers>;
            </sessionState>;
          </system.web>;

## <span data-ttu-id="2cb31-124"><a id="usesessionobject"></a>Użycie obiektu Session w kodzie</span><span class="sxs-lookup"><span data-stu-id="2cb31-124"><a id="usesessionobject"></a> Use the Session Object in Code</span></span>
<span data-ttu-id="2cb31-125">Ostatnim krokiem jest rozpoczęcie korzystania z obiektu Session w kodzie ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="2cb31-125">The final step is to begin using the Session object in your ASP.NET code.</span></span> <span data-ttu-id="2cb31-126">Obiekty są dodawane do stanu sesji przy użyciu metody **Session.Add**.</span><span class="sxs-lookup"><span data-stu-id="2cb31-126">You add objects to session state by using the **Session.Add** method.</span></span> <span data-ttu-id="2cb31-127">Ta metoda używa par kluczy i wartości do przechowywania elementów w pamięci podręcznej stanu sesji.</span><span class="sxs-lookup"><span data-stu-id="2cb31-127">This method uses key-value pairs to store items in the session state cache.</span></span>

    string strValue = "yourvalue";
    Session.Add("yourkey", strValue);

<span data-ttu-id="2cb31-128">Poniższy kod pobiera tę wartość z informacji o stanie sesji.</span><span class="sxs-lookup"><span data-stu-id="2cb31-128">The following code retrieves this value from session state.</span></span>

    object objValue = Session["yourkey"];
    if (objValue != null)
       strValue = (string)objValue;    

<span data-ttu-id="2cb31-129">Możesz również użyć usługi Pamięć podręczna Redis do buforowania obiektów w aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="2cb31-129">You can also use the Redis Cache to cache objects in your web app.</span></span> <span data-ttu-id="2cb31-130">Aby uzyskać więcej informacji, zobacz [MVC movie app with Azure Redis Cache in 15 minutes](https://azure.microsoft.com/blog/2014/06/05/mvc-movie-app-with-azure-redis-cache-in-15-minutes/) (Tworzenie aplikacji filmowej MVC przy użyciu usługi Azure Redis Cache w ciągu 15 minut).</span><span class="sxs-lookup"><span data-stu-id="2cb31-130">For more info, see [MVC movie app with Azure Redis Cache in 15 minutes](https://azure.microsoft.com/blog/2014/06/05/mvc-movie-app-with-azure-redis-cache-in-15-minutes/).</span></span>
<span data-ttu-id="2cb31-131">Aby uzyskać więcej informacji na temat sposobu używania informacji o stanie sesji programu ASP.NET, zobacz [ASP.NET Session State Overview][ASP.NET Session State Overview] (Omówienie informacji o stanie sesji programu ASP.NET).</span><span class="sxs-lookup"><span data-stu-id="2cb31-131">For more details about how to use ASP.NET session state, see [ASP.NET Session State Overview][ASP.NET Session State Overview].</span></span>

> [!NOTE]
> <span data-ttu-id="2cb31-132">Jeśli chcesz zacząć korzystać z usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź do artykułu [Wypróbuj usługę App Service](https://azure.microsoft.com/try/app-service/), w którym wyjaśniono, jak od razu utworzyć początkową aplikację sieci Web o krótkim okresie istnienia w usłudze App Service.</span><span class="sxs-lookup"><span data-stu-id="2cb31-132">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="2cb31-133">Bez kart kredytowych i bez zobowiązań.</span><span class="sxs-lookup"><span data-stu-id="2cb31-133">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="2cb31-134">Co zostało zmienione</span><span class="sxs-lookup"><span data-stu-id="2cb31-134">What's changed</span></span>
* <span data-ttu-id="2cb31-135">Przewodnik dotyczący przejścia od usługi Witryny sieci Web do usługi App Service można znaleźć w temacie [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714) (Usługa Azure App Service i jej wpływ na istniejące usługi platformy Azure).</span><span class="sxs-lookup"><span data-stu-id="2cb31-135">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>
  
  <span data-ttu-id="2cb31-136">*Autor: [Rick Anderson](https://twitter.com/RickAndMSFT)*</span><span class="sxs-lookup"><span data-stu-id="2cb31-136">*By [Rick Anderson](https://twitter.com/RickAndMSFT)*</span></span>

[installed the latest]: http://www.windowsazure.com/downloads/?sdk=net  
[ASP.NET Session State Overview]: http://msdn.microsoft.com/library/ms178581.aspx

[NewIcon]: ./media/web-sites-dotnet-session-state-caching/CacheScreenshot_NewButton.png
[NewCacheDialog]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_CreateOptions.png
[CacheIcon]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_CacheIcon.png
[NuGetDialog]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_NuGet.png
[OutputConfig]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_OC_WebConfig.png
[CacheConfig]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_CacheConfig.png
[EndpointURL]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_EndpointURL.png
[ManageKeys]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_ManageAccessKeys.png

