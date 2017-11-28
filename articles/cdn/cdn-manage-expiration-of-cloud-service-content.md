---
title: "aaaManage wygaśnięcia zawartości sieci web w usłudze Azure CDN | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toomanage wygaśnięcia zawartości usług Azure Web Apps/Cloud Services, ASP.NET lub usługi IIS w usłudze Azure CDN."
services: cdn
documentationcenter: .NET
author: zhangmanling
manager: erikre
editor: 
ms.assetid: bef53fcc-bb13-4002-9324-9edee9da8288
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: a0154236c3893b627f4480e0688f555964862556
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-expiration-of-azure-web-appscloud-services-aspnet-or-iis-content-in-azure-cdn"></a><span data-ttu-id="fbcc7-103">Zarządzaj wygasaniem zawartości usług Azure Web Apps/Cloud Services, ASP.NET lub usługi IIS w usłudze Azure CDN</span><span class="sxs-lookup"><span data-stu-id="fbcc7-103">Manage expiration of Azure Web Apps/Cloud Services, ASP.NET, or IIS content in Azure CDN</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fbcc7-104">Usługi aplikacji/w chmurze Azure sieci Web, ASP.NET lub usług IIS</span><span class="sxs-lookup"><span data-stu-id="fbcc7-104">Azure Web Apps/Cloud Services, ASP.NET, or IIS</span></span>](cdn-manage-expiration-of-cloud-service-content.md)
> * [<span data-ttu-id="fbcc7-105">Usługa blob magazynu Azure</span><span class="sxs-lookup"><span data-stu-id="fbcc7-105">Azure Storage blob service</span></span>](cdn-manage-expiration-of-blob-content.md)
> 
> 

<span data-ttu-id="fbcc7-106">Mogą być buforowane pliki z dowolnego publicznie dostępnego źródła serwera sieci web w usłudze Azure CDN, dopóki nie upłynie jego czas wygaśnięcia (TTL).</span><span class="sxs-lookup"><span data-stu-id="fbcc7-106">Files from any publicly accessible origin web server can be cached in Azure CDN until its time-to-live (TTL) elapses.</span></span>  <span data-ttu-id="fbcc7-107">Witaj czas wygaśnięcia jest określany przez hello [ *Cache-Control* nagłówka](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) hello HTTP odpowiedzi z serwera źródłowego hello.</span><span class="sxs-lookup"><span data-stu-id="fbcc7-107">hello TTL is determined by hello [*Cache-Control* header](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) in hello HTTP response from hello origin server.</span></span>  <span data-ttu-id="fbcc7-108">W tym artykule opisano sposób tooset `Cache-Control` nagłówki dla aplikacji sieci Web platformy Azure, usługi w chmurze Azure, aplikacji programu ASP.NET i witryny internetowe usługi informacyjne, które są skonfigurowane podobnie.</span><span class="sxs-lookup"><span data-stu-id="fbcc7-108">This article describes how tooset `Cache-Control` headers for Azure Web Apps, Azure Cloud Services, ASP.NET applications, and Internet Information Services sites, all of which are configured similarly.</span></span>

> [!TIP]
> <span data-ttu-id="fbcc7-109">Możesz wybrać tooset nie czas wygaśnięcia pliku.</span><span class="sxs-lookup"><span data-stu-id="fbcc7-109">You may choose tooset no TTL on a file.</span></span>  <span data-ttu-id="fbcc7-110">W takim przypadku Azure CDN automatycznie stosuje domyślny czas wygaśnięcia wynosi siedem dni.</span><span class="sxs-lookup"><span data-stu-id="fbcc7-110">In this case, Azure CDN automatically applies a default TTL of seven days.</span></span>
> 
> <span data-ttu-id="fbcc7-111">Aby uzyskać więcej informacji na temat działania usługi Azure CDN toospeed toofiles dostępu i innych zasobów, zobacz hello [Omówienie usługi Azure CDN](cdn-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fbcc7-111">For more information about how Azure CDN works toospeed up access toofiles and other resources, see hello [Azure CDN Overview](cdn-overview.md).</span></span>
> 
> 

## <a name="setting-cache-control-headers-in-configuration"></a><span data-ttu-id="fbcc7-112">Nagłówki Cache-Control ustawienia w konfiguracji</span><span class="sxs-lookup"><span data-stu-id="fbcc7-112">Setting Cache-Control Headers in configuration</span></span>
<span data-ttu-id="fbcc7-113">Dla zawartości statycznej, takich jak obrazy i arkusze stylów, możesz kontrolować częstotliwość aktualizacji hello modyfikując hello **applicationHost.config** lub **web.config** plików dla aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="fbcc7-113">For static content, such as images and style sheets, you can control hello update frequency by modifying hello **applicationHost.config** or **web.config** files for your web application.</span></span>  <span data-ttu-id="fbcc7-114">Witaj **system.webServer\staticContent\clientCache** w pliku konfiguracji hello ustawi hello `Cache-Control` nagłówek dla zawartości.</span><span class="sxs-lookup"><span data-stu-id="fbcc7-114">hello **system.webServer\staticContent\clientCache** element in hello configuration file will set hello `Cache-Control` header for your content.</span></span> <span data-ttu-id="fbcc7-115">Aby uzyskać **web.config**, ustawienia konfiguracji hello będzie miało wpływ na wszystkie elementy w folderze hello i wszystkie podfoldery Jeśli zastąpiona na poziomie podfolder hello.</span><span class="sxs-lookup"><span data-stu-id="fbcc7-115">For **web.config**, hello configuration settings will affect everything in hello folder and all subfolders, unless overridden at hello subfolder level.</span></span>  <span data-ttu-id="fbcc7-116">Na przykład można ustawić domyślnego time-to-live na powitania głównego toohave całej zawartości statycznej pamięci podręcznej dla 3 dni, ale ma podfolder, który ma więcej zmiennej zawartości z ustawieniem pamięci podręcznej 6 godzin.</span><span class="sxs-lookup"><span data-stu-id="fbcc7-116">For example, you can set a default time-to-live at hello root toohave all static content cached for 3 days, but have a subfolder that has more variable content with a cache setting of 6 hours.</span></span>  <span data-ttu-id="fbcc7-117">Dla **applicationHost.config**, wszystkie aplikacje w witrynie hello zostaną zmienione, ale może zostać zastąpiona w **web.config** plików w aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="fbcc7-117">For **applicationHost.config**, all applications on hello site will be affected, but can be overridden in **web.config** files in hello applications.</span></span>

<span data-ttu-id="fbcc7-118">Witaj następujące XML przedstawiono przykład ustawienie **clientCache** toospecify, a maksymalny wiek 3 dni:</span><span class="sxs-lookup"><span data-stu-id="fbcc7-118">hello following XML shows an example of setting **clientCache** toospecify a maximum age of 3 days:</span></span>  

```xml
<configuration>
    <system.webServer>
        <staticContent>
            <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="3.00:00:00" />
        </staticContent>
    </system.webServer>
</configuration>
```

<span data-ttu-id="fbcc7-119">Określanie **UseMaxAge** dodaje `Cache-Control: max-age=<nnn>` nagłówka toohello odpowiedzi na podstawie hello wartości określone w hello **CacheControlMaxAge** atrybutu.</span><span class="sxs-lookup"><span data-stu-id="fbcc7-119">Specifying **UseMaxAge** adds a `Cache-Control: max-age=<nnn>` header toohello response based on hello value specified in hello **CacheControlMaxAge** attribute.</span></span> <span data-ttu-id="fbcc7-120">format Hello hello timespan jest dla hello **cacheControlMaxAge** atrybutu <days>.<hours>:<min>:<sec>.</span><span class="sxs-lookup"><span data-stu-id="fbcc7-120">hello format of hello timespan is for hello **cacheControlMaxAge** attribute is <days>.<hours>:<min>:<sec>.</span></span> <span data-ttu-id="fbcc7-121">Aby uzyskać więcej informacji na temat hello **clientCache** węzła, zobacz [pamięci podręcznej klienta <clientCache> ](http://www.iis.net/ConfigReference/system.webServer/staticContent/clientCache).</span><span class="sxs-lookup"><span data-stu-id="fbcc7-121">For more information on hello **clientCache** node, see [Client Cache <clientCache>](http://www.iis.net/ConfigReference/system.webServer/staticContent/clientCache).</span></span>  

## <a name="setting-cache-control-headers-in-code"></a><span data-ttu-id="fbcc7-122">Ustawianie Cache-Control nagłówków w kodzie</span><span class="sxs-lookup"><span data-stu-id="fbcc7-122">Setting Cache-Control Headers in Code</span></span>
<span data-ttu-id="fbcc7-123">Dla aplikacji ASP.NET można ustawić zachowanie buforowania w sieci CDN hello programowo przez ustawienie hello **HttpResponse.Cache** właściwości.</span><span class="sxs-lookup"><span data-stu-id="fbcc7-123">For ASP.NET applications, you can set hello CDN caching behavior programmatically by setting hello **HttpResponse.Cache** property.</span></span> <span data-ttu-id="fbcc7-124">Aby uzyskać więcej informacji na temat hello **HttpResponse.Cache** właściwości, zobacz [właściwości HttpResponse.Cache](http://msdn.microsoft.com/library/system.web.httpresponse.cache.aspx) i [HttpCachePolicy klasy](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx).</span><span class="sxs-lookup"><span data-stu-id="fbcc7-124">For more information on hello **HttpResponse.Cache** property, see [HttpResponse.Cache Property](http://msdn.microsoft.com/library/system.web.httpresponse.cache.aspx) and [HttpCachePolicy Class](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx).</span></span>  

<span data-ttu-id="fbcc7-125">Jeśli chcesz tooprogrammatically pamięci podręcznej zawartość aplikacji ASP.NET, upewnij się, czy przez ustawienie zbyt HttpCacheability jest oznaczony jako buforowalnej zawartości hello*publicznego*.</span><span class="sxs-lookup"><span data-stu-id="fbcc7-125">If you want tooprogrammatically cache application content in ASP.NET, make sure that hello content is marked as cacheable by setting HttpCacheability too*Public*.</span></span> <span data-ttu-id="fbcc7-126">Ponadto upewnij się, że moduł weryfikacji pamięci podręcznej jest ustawiona.</span><span class="sxs-lookup"><span data-stu-id="fbcc7-126">Also, ensure that a cache validator is set.</span></span> <span data-ttu-id="fbcc7-127">Moduł sprawdzania poprawności Hello pamięci podręcznej może być ostatniej modyfikacji sygnatury czasowej ustawiony przez wywołanie SetLastModified lub wartość etag ustawiony przez wywołanie SetETag.</span><span class="sxs-lookup"><span data-stu-id="fbcc7-127">hello cache validator can be a Last Modified timestamp set by calling SetLastModified, or an etag value set by calling SetETag.</span></span> <span data-ttu-id="fbcc7-128">Opcjonalnie można również określić czas wygaśnięcia pamięci podręcznej przez wywołanie metody SetExpires lub może polegać na powitania: domyślny algorytm heurystyczny pamięci podręcznej opisem we wcześniejszej części tego dokumentu.</span><span class="sxs-lookup"><span data-stu-id="fbcc7-128">Optionally, you can also specify a cache expiration time by calling SetExpires, or you can rely on hello default cache heuristics described earlier in this document.</span></span>  

<span data-ttu-id="fbcc7-129">Na przykład zawartość toocache przez jedną godzinę, Dodaj następujące hello:</span><span class="sxs-lookup"><span data-stu-id="fbcc7-129">For example, toocache content for one hour, add hello following:</span></span>  

```csharp
// Set hello caching parameters.
Response.Cache.SetExpires(DateTime.Now.AddHours(1));
Response.Cache.SetCacheability(HttpCacheability.Public);
Response.Cache.SetLastModified(DateTime.Now);
```

## <a name="next-steps"></a><span data-ttu-id="fbcc7-130">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="fbcc7-130">Next Steps</span></span>
* [<span data-ttu-id="fbcc7-131">Przeczytaj szczegółowe informacje o hello **clientCache** — element</span><span class="sxs-lookup"><span data-stu-id="fbcc7-131">Read details about hello **clientCache** element</span></span>](http://www.iis.net/ConfigReference/system.webServer/staticContent/clientCache)
* [<span data-ttu-id="fbcc7-132">Zapoznaj się dokumentacją hello hello **HttpResponse.Cache** właściwości</span><span class="sxs-lookup"><span data-stu-id="fbcc7-132">Read hello documentation for hello **HttpResponse.Cache** Property</span></span>](http://msdn.microsoft.com/library/system.web.httpresponse.cache.aspx) 
* <span data-ttu-id="fbcc7-133">[Zapoznaj się dokumentacją hello hello **klasy HttpCachePolicy**](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx).</span><span class="sxs-lookup"><span data-stu-id="fbcc7-133">[Read hello documentation for hello **HttpCachePolicy Class**](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx).</span></span>  

