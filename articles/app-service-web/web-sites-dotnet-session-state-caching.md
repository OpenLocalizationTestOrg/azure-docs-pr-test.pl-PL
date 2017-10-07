---
title: "Stan aaaSession z pamięcią podręczną Azure Redis w usłudze Azure App Service"
description: "Dowiedz się, jak toouse hello usługi pamięć podręczna Azure toosupport ASP.NET sesji buforowania informacji o stanie."
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
ms.openlocfilehash: f689b6754ea072aa195f822ab6482f4bf2748375
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="session-state-with-azure-redis-cache-in-azure-app-service"></a><span data-ttu-id="a8be4-103">Stan sesji i usługa Azure Redis Cache w usłudze Azure App Service</span><span class="sxs-lookup"><span data-stu-id="a8be4-103">Session state with Azure Redis cache in Azure App Service</span></span>
<span data-ttu-id="a8be4-104">W tym temacie wyjaśniono, jak toouse hello usługi pamięć podręczna Redis Azure dla stanu sesji.</span><span class="sxs-lookup"><span data-stu-id="a8be4-104">This topic explains how toouse hello Azure Redis Cache Service for session state.</span></span>

<span data-ttu-id="a8be4-105">Jeśli aplikacja sieci web platformy ASP.NET używa stanu sesji, należy tooconfigure zewnętrznego dostawcę stanu sesji (hello usługi pamięć podręczna Redis lub dostawcę stanu sesji SQL Server).</span><span class="sxs-lookup"><span data-stu-id="a8be4-105">If your ASP.NET web app uses session state, you will need tooconfigure an external session state provider (either hello Redis Cache Service or a SQL Server session state provider).</span></span> <span data-ttu-id="a8be4-106">Jeśli używasz stanu sesji i nie używasz dostawcy zewnętrznego, będzie ograniczona tooone wystąpienie aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="a8be4-106">If you use session state, and don't use an external provider, you will be limited tooone instance of your web app.</span></span> <span data-ttu-id="a8be4-107">Witaj usługi pamięć podręczna Redis jest tooenable najszybszym i najprostszym hello.</span><span class="sxs-lookup"><span data-stu-id="a8be4-107">hello Redis Cache Service is hello fastest and simplest tooenable.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <span data-ttu-id="a8be4-108"><a id="createcache"></a>Utwórz hello pamięci podręcznej</span><span class="sxs-lookup"><span data-stu-id="a8be4-108"><a id="createcache"></a>Create hello Cache</span></span>
<span data-ttu-id="a8be4-109">Postępuj zgodnie z [te kierunkach](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#create-cache) toocreate hello w pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="a8be4-109">Follow [these directions](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#create-cache) toocreate hello cache.</span></span>

## <span data-ttu-id="a8be4-110"><a id="configureproject"></a>Dodawanie pakietu RedisSessionStateProvider NuGet pakietu tooyour sieci web aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="a8be4-110"><a id="configureproject"></a>Add hello RedisSessionStateProvider NuGet package tooyour web app</span></span>
<span data-ttu-id="a8be4-111">Zainstaluj hello NuGet `RedisSessionStateProvider` pakietu.</span><span class="sxs-lookup"><span data-stu-id="a8be4-111">Install hello NuGet `RedisSessionStateProvider` package.</span></span>  <span data-ttu-id="a8be4-112">Użyj hello następujące polecenie tooinstall z konsoli Menedżera pakietów hello (**narzędzia** > **Menedżera pakietów NuGet** > **Konsola Menedżera pakietów**):</span><span class="sxs-lookup"><span data-stu-id="a8be4-112">Use hello following command tooinstall from hello package manager console (**Tools** > **NuGet Package Manager** > **Package Manager Console**):</span></span>

  `PM> Install-Package Microsoft.Web.RedisSessionStateProvider`

<span data-ttu-id="a8be4-113">tooinstall z **narzędzia** > **Menedżera pakietów NuGet** > **Zarządzaj pakietami NugGet dla rozwiązania**, wyszukaj `RedisSessionStateProvider`.</span><span class="sxs-lookup"><span data-stu-id="a8be4-113">tooinstall from **Tools** > **NuGet Package Manager** > **Manage NugGet Packages for Solution**, search for `RedisSessionStateProvider`.</span></span>

<span data-ttu-id="a8be4-114">Aby uzyskać więcej informacji, zobacz hello [strony pakietu NuGet RedisSessionStateProvider](http://www.nuget.org/packages/Microsoft.Web.RedisSessionStateProvider/) i [Konfigurowanie klienta pamięci podręcznej hello](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#NuGet).</span><span class="sxs-lookup"><span data-stu-id="a8be4-114">For more information see hello [NuGet RedisSessionStateProvider page](http://www.nuget.org/packages/Microsoft.Web.RedisSessionStateProvider/) and [Configure hello cache client](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#NuGet).</span></span>

## <span data-ttu-id="a8be4-115"><a id="configurewebconfig"></a>Modyfikowanie hello pliku Web.Config</span><span class="sxs-lookup"><span data-stu-id="a8be4-115"><a id="configurewebconfig"></a>Modify hello Web.Config File</span></span>
<span data-ttu-id="a8be4-116">Ponadto zestaw toomaking odwołuje się do pamięci podręcznej, hello pakiet NuGet Dodaje wpisy zastępcze w hello *web.config* pliku.</span><span class="sxs-lookup"><span data-stu-id="a8be4-116">In addition toomaking assembly references for Cache, hello NuGet package adds stub entries in hello *web.config* file.</span></span> 

1. <span data-ttu-id="a8be4-117">Otwórz hello *web.config* i Znajdź hello hello **sessionState** elementu.</span><span class="sxs-lookup"><span data-stu-id="a8be4-117">Open hello *web.config* and find hello hello **sessionState** element.</span></span>
2. <span data-ttu-id="a8be4-118">Wprowadź wartości hello `host`, `accessKey`, `port` (hello SSL port 6380) i ustaw `SSL` zbyt`true`.</span><span class="sxs-lookup"><span data-stu-id="a8be4-118">Enter hello values for `host`, `accessKey`, `port` (hello SSL port should be 6380), and set `SSL` too`true`.</span></span> <span data-ttu-id="a8be4-119">Te wartości można uzyskać z hello [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715) bloku dla swojego wystąpienia w pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="a8be4-119">These values can be obtained from hello [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715) blade for your cache instance.</span></span> <span data-ttu-id="a8be4-120">Aby uzyskać więcej informacji, zobacz [połączyć z pamięci podręcznej toohello](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#connect-to-cache).</span><span class="sxs-lookup"><span data-stu-id="a8be4-120">For more information, see [Connect toohello cache](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#connect-to-cache).</span></span> <span data-ttu-id="a8be4-121">Należy pamiętać, że port bez protokołu SSL hello jest domyślnie wyłączona dla nowych pamięci podręcznych.</span><span class="sxs-lookup"><span data-stu-id="a8be4-121">Note that hello non-SSL port is disabled by default for new caches.</span></span> <span data-ttu-id="a8be4-122">Aby uzyskać więcej informacji na temat włączania portu bez protokołu SSL hello Zobacz hello [porty dostępu](https://msdn.microsoft.com/library/azure/dn793612.aspx#AccessPorts) części hello [Konfigurowanie pamięci podręcznej w pamięci podręcznej Redis Azure](https://msdn.microsoft.com/library/azure/dn793612.aspx) tematu.</span><span class="sxs-lookup"><span data-stu-id="a8be4-122">For more information about enabling hello non-SSL port, see hello [Access Ports](https://msdn.microsoft.com/library/azure/dn793612.aspx#AccessPorts) section in hello [Configure a cache in Azure Redis Cache](https://msdn.microsoft.com/library/azure/dn793612.aspx) topic.</span></span> <span data-ttu-id="a8be4-123">Hello następujący kod przedstawia hello zmiany toohello *web.config* pliku, w szczególności zmiany hello zbyt*portu*, *hosta*, accessKey * i *ssl*.</span><span class="sxs-lookup"><span data-stu-id="a8be4-123">hello following markup shows hello changes toohello *web.config* file, specifically hello changes too*port*, *host*, accessKey*, and *ssl*.</span></span>
   
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

## <span data-ttu-id="a8be4-124"><a id="usesessionobject"></a>Użyj hello obiektu Session w kodzie</span><span class="sxs-lookup"><span data-stu-id="a8be4-124"><a id="usesessionobject"></a> Use hello Session Object in Code</span></span>
<span data-ttu-id="a8be4-125">Ostatnim krokiem Hello jest toobegin przy użyciu hello obiektu Session w kodzie ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="a8be4-125">hello final step is toobegin using hello Session object in your ASP.NET code.</span></span> <span data-ttu-id="a8be4-126">Dodaj stan toosession obiektów przy użyciu hello **Session.Add** metody.</span><span class="sxs-lookup"><span data-stu-id="a8be4-126">You add objects toosession state by using hello **Session.Add** method.</span></span> <span data-ttu-id="a8be4-127">Ta metoda używa par klucz wartość toostore elementów w pamięci podręcznej stanu sesji hello.</span><span class="sxs-lookup"><span data-stu-id="a8be4-127">This method uses key-value pairs toostore items in hello session state cache.</span></span>

    string strValue = "yourvalue";
    Session.Add("yourkey", strValue);

<span data-ttu-id="a8be4-128">powitania po kod pobiera tę wartość ze stanu sesji.</span><span class="sxs-lookup"><span data-stu-id="a8be4-128">hello following code retrieves this value from session state.</span></span>

    object objValue = Session["yourkey"];
    if (objValue != null)
       strValue = (string)objValue;    

<span data-ttu-id="a8be4-129">Umożliwia także hello pamięci podręcznej Redis toocache obiektów w aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="a8be4-129">You can also use hello Redis Cache toocache objects in your web app.</span></span> <span data-ttu-id="a8be4-130">Aby uzyskać więcej informacji, zobacz [MVC movie app with Azure Redis Cache in 15 minutes](https://azure.microsoft.com/blog/2014/06/05/mvc-movie-app-with-azure-redis-cache-in-15-minutes/) (Tworzenie aplikacji filmowej MVC przy użyciu usługi Azure Redis Cache w ciągu 15 minut).</span><span class="sxs-lookup"><span data-stu-id="a8be4-130">For more info, see [MVC movie app with Azure Redis Cache in 15 minutes](https://azure.microsoft.com/blog/2014/06/05/mvc-movie-app-with-azure-redis-cache-in-15-minutes/).</span></span>
<span data-ttu-id="a8be4-131">Aby uzyskać więcej informacji na temat stanu sesji ASP.NET toouse, zobacz [przegląd stanu sesji ASP.NET][ASP.NET Session State Overview].</span><span class="sxs-lookup"><span data-stu-id="a8be4-131">For more details about how toouse ASP.NET session state, see [ASP.NET Session State Overview][ASP.NET Session State Overview].</span></span>

> [!NOTE]
> <span data-ttu-id="a8be4-132">Tooget wprowadzenie do usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź zbyt[Wypróbuj usługę App Service](https://azure.microsoft.com/try/app-service/), gdzie możesz od razu utworzyć krótkotrwałą, początkową aplikację sieci web w usłudze App Service.</span><span class="sxs-lookup"><span data-stu-id="a8be4-132">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="a8be4-133">Bez kart kredytowych i bez zobowiązań.</span><span class="sxs-lookup"><span data-stu-id="a8be4-133">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="a8be4-134">Co zostało zmienione</span><span class="sxs-lookup"><span data-stu-id="a8be4-134">What's changed</span></span>
* <span data-ttu-id="a8be4-135">Toohello przewodnik zmiany z tooApp witryn sieci Web usługi dla: [usłudze Azure App Service i jej wpływ na istniejące usługi platformy Azure](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="a8be4-135">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>
  
  <span data-ttu-id="a8be4-136">*Autor: [Rick Anderson](https://twitter.com/RickAndMSFT)*</span><span class="sxs-lookup"><span data-stu-id="a8be4-136">*By [Rick Anderson](https://twitter.com/RickAndMSFT)*</span></span>

[installed hello latest]: http://www.windowsazure.com/downloads/?sdk=net  
[ASP.NET Session State Overview]: http://msdn.microsoft.com/library/ms178581.aspx

[NewIcon]: ./media/web-sites-dotnet-session-state-caching/CacheScreenshot_NewButton.png
[NewCacheDialog]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_CreateOptions.png
[CacheIcon]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_CacheIcon.png
[NuGetDialog]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_NuGet.png
[OutputConfig]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_OC_WebConfig.png
[CacheConfig]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_CacheConfig.png
[EndpointURL]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_EndpointURL.png
[ManageKeys]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_ManageAccessKeys.png

