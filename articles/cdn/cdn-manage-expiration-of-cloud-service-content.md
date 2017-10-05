---
title: "Zarządzaj wygasaniem zawartości sieci web w usłudze Azure CDN | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak zarządzać wygasaniem zawartości usług Azure Web Apps/Cloud Services, ASP.NET lub usługi IIS w usłudze Azure CDN."
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
ms.openlocfilehash: c207d780857a61d4b1fc0f39e6185cae67abc955
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="manage-expiration-of-azure-web-appscloud-services-aspnet-or-iis-content-in-azure-cdn"></a><span data-ttu-id="9d2bb-103">Zarządzaj wygasaniem zawartości usług Azure Web Apps/Cloud Services, ASP.NET lub usługi IIS w usłudze Azure CDN</span><span class="sxs-lookup"><span data-stu-id="9d2bb-103">Manage expiration of Azure Web Apps/Cloud Services, ASP.NET, or IIS content in Azure CDN</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9d2bb-104">Usługi aplikacji/w chmurze Azure sieci Web, ASP.NET lub usług IIS</span><span class="sxs-lookup"><span data-stu-id="9d2bb-104">Azure Web Apps/Cloud Services, ASP.NET, or IIS</span></span>](cdn-manage-expiration-of-cloud-service-content.md)
> * [<span data-ttu-id="9d2bb-105">Usługa blob magazynu Azure</span><span class="sxs-lookup"><span data-stu-id="9d2bb-105">Azure Storage blob service</span></span>](cdn-manage-expiration-of-blob-content.md)
> 
> 

<span data-ttu-id="9d2bb-106">Mogą być buforowane pliki z dowolnego publicznie dostępnego źródła serwera sieci web w usłudze Azure CDN, dopóki nie upłynie jego czas wygaśnięcia (TTL).</span><span class="sxs-lookup"><span data-stu-id="9d2bb-106">Files from any publicly accessible origin web server can be cached in Azure CDN until its time-to-live (TTL) elapses.</span></span>  <span data-ttu-id="9d2bb-107">Czas wygaśnięcia jest określany przez [ *Cache-Control* nagłówka](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) w odpowiedzi HTTP z serwera pochodzenia.</span><span class="sxs-lookup"><span data-stu-id="9d2bb-107">The TTL is determined by the [*Cache-Control* header](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) in the HTTP response from the origin server.</span></span>  <span data-ttu-id="9d2bb-108">W tym artykule opisano sposób ustawiania `Cache-Control` nagłówki dla aplikacji sieci Web platformy Azure, usługi w chmurze Azure, aplikacji programu ASP.NET i witryny internetowe usługi informacyjne, które są skonfigurowane podobnie.</span><span class="sxs-lookup"><span data-stu-id="9d2bb-108">This article describes how to set `Cache-Control` headers for Azure Web Apps, Azure Cloud Services, ASP.NET applications, and Internet Information Services sites, all of which are configured similarly.</span></span>

> [!TIP]
> <span data-ttu-id="9d2bb-109">Można ustawić nie TTL w pliku.</span><span class="sxs-lookup"><span data-stu-id="9d2bb-109">You may choose to set no TTL on a file.</span></span>  <span data-ttu-id="9d2bb-110">W takim przypadku Azure CDN automatycznie stosuje domyślny czas wygaśnięcia wynosi siedem dni.</span><span class="sxs-lookup"><span data-stu-id="9d2bb-110">In this case, Azure CDN automatically applies a default TTL of seven days.</span></span>
> 
> <span data-ttu-id="9d2bb-111">Aby uzyskać więcej informacji na temat działania usługi Azure CDN do Przyspieszanie dostępu do plików i innych zasobów, zobacz [Omówienie usługi Azure CDN](cdn-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9d2bb-111">For more information about how Azure CDN works to speed up access to files and other resources, see the [Azure CDN Overview](cdn-overview.md).</span></span>
> 
> 

## <a name="setting-cache-control-headers-in-configuration"></a><span data-ttu-id="9d2bb-112">Nagłówki Cache-Control ustawienia w konfiguracji</span><span class="sxs-lookup"><span data-stu-id="9d2bb-112">Setting Cache-Control Headers in configuration</span></span>
<span data-ttu-id="9d2bb-113">Dla zawartości statycznej, takich jak obrazy i arkusze stylów, możesz kontrolować częstotliwość aktualizacji przez zmodyfikowanie **applicationHost.config** lub **web.config** plików dla aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="9d2bb-113">For static content, such as images and style sheets, you can control the update frequency by modifying the **applicationHost.config** or **web.config** files for your web application.</span></span>  <span data-ttu-id="9d2bb-114">**System.webServer\staticContent\clientCache** ustawi elementu w pliku konfiguracyjnym `Cache-Control` nagłówek dla zawartości.</span><span class="sxs-lookup"><span data-stu-id="9d2bb-114">The **system.webServer\staticContent\clientCache** element in the configuration file will set the `Cache-Control` header for your content.</span></span> <span data-ttu-id="9d2bb-115">Aby uzyskać **web.config**, ustawienia konfiguracji będzie miało wpływ na wszystkie elementy w folderze i wszystkie podfoldery, jeśli zastąpiona na poziomie podfolder.</span><span class="sxs-lookup"><span data-stu-id="9d2bb-115">For **web.config**, the configuration settings will affect everything in the folder and all subfolders, unless overridden at the subfolder level.</span></span>  <span data-ttu-id="9d2bb-116">Można na przykład domyślny czas wygaśnięcia główny zestaw ma wszystkie zawartości statycznej pamięci podręcznej dla 3 dni, ale ma podfolder, który ma więcej zmiennych zawartość z ustawieniem pamięci podręcznej 6 godzin.</span><span class="sxs-lookup"><span data-stu-id="9d2bb-116">For example, you can set a default time-to-live at the root to have all static content cached for 3 days, but have a subfolder that has more variable content with a cache setting of 6 hours.</span></span>  <span data-ttu-id="9d2bb-117">Dla **applicationHost.config**, wszystkie aplikacje w witrynie zostaną zmienione, ale może zostać zastąpiona w **web.config** plików w aplikacjach.</span><span class="sxs-lookup"><span data-stu-id="9d2bb-117">For **applicationHost.config**, all applications on the site will be affected, but can be overridden in **web.config** files in the applications.</span></span>

<span data-ttu-id="9d2bb-118">Następujący kod XML przedstawiono przykład ustawienie **clientCache** określić maksymalny wiek 3 dni:</span><span class="sxs-lookup"><span data-stu-id="9d2bb-118">The following XML shows an example of setting **clientCache** to specify a maximum age of 3 days:</span></span>  

```xml
<configuration>
    <system.webServer>
        <staticContent>
            <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="3.00:00:00" />
        </staticContent>
    </system.webServer>
</configuration>
```

<span data-ttu-id="9d2bb-119">Określanie **UseMaxAge** dodaje `Cache-Control: max-age=<nnn>` nagłówka w odpowiedzi na podstawie wartości określone w **CacheControlMaxAge** atrybutu.</span><span class="sxs-lookup"><span data-stu-id="9d2bb-119">Specifying **UseMaxAge** adds a `Cache-Control: max-age=<nnn>` header to the response based on the value specified in the **CacheControlMaxAge** attribute.</span></span> <span data-ttu-id="9d2bb-120">Format elementu timespan **cacheControlMaxAge** atrybutu <days>.<hours>:<min>:<sec>.</span><span class="sxs-lookup"><span data-stu-id="9d2bb-120">The format of the timespan is for the **cacheControlMaxAge** attribute is <days>.<hours>:<min>:<sec>.</span></span> <span data-ttu-id="9d2bb-121">Aby uzyskać więcej informacji na temat **clientCache** węzła, zobacz [pamięci podręcznej klienta <clientCache> ](http://www.iis.net/ConfigReference/system.webServer/staticContent/clientCache).</span><span class="sxs-lookup"><span data-stu-id="9d2bb-121">For more information on the **clientCache** node, see [Client Cache <clientCache>](http://www.iis.net/ConfigReference/system.webServer/staticContent/clientCache).</span></span>  

## <a name="setting-cache-control-headers-in-code"></a><span data-ttu-id="9d2bb-122">Ustawianie Cache-Control nagłówków w kodzie</span><span class="sxs-lookup"><span data-stu-id="9d2bb-122">Setting Cache-Control Headers in Code</span></span>
<span data-ttu-id="9d2bb-123">Dla aplikacji ASP.NET można ustawić CDN buforowanie programowo, ustawiając **HttpResponse.Cache** właściwości.</span><span class="sxs-lookup"><span data-stu-id="9d2bb-123">For ASP.NET applications, you can set the CDN caching behavior programmatically by setting the **HttpResponse.Cache** property.</span></span> <span data-ttu-id="9d2bb-124">Aby uzyskać więcej informacji na temat **HttpResponse.Cache** właściwości, zobacz [właściwości HttpResponse.Cache](http://msdn.microsoft.com/library/system.web.httpresponse.cache.aspx) i [HttpCachePolicy klasy](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx).</span><span class="sxs-lookup"><span data-stu-id="9d2bb-124">For more information on the **HttpResponse.Cache** property, see [HttpResponse.Cache Property](http://msdn.microsoft.com/library/system.web.httpresponse.cache.aspx) and [HttpCachePolicy Class](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx).</span></span>  

<span data-ttu-id="9d2bb-125">Jeśli chcesz programowo pamięci podręcznej zawartości aplikacji w programie ASP.NET, upewnij się, czy zawartość jest oznaczony jako buforowalnej ustawiając HttpCacheability *publicznego*.</span><span class="sxs-lookup"><span data-stu-id="9d2bb-125">If you want to programmatically cache application content in ASP.NET, make sure that the content is marked as cacheable by setting HttpCacheability to *Public*.</span></span> <span data-ttu-id="9d2bb-126">Ponadto upewnij się, że moduł weryfikacji pamięci podręcznej jest ustawiona.</span><span class="sxs-lookup"><span data-stu-id="9d2bb-126">Also, ensure that a cache validator is set.</span></span> <span data-ttu-id="9d2bb-127">Moduł sprawdzania poprawności pamięci podręcznej może być ostatniej modyfikacji sygnatury czasowej ustawiony przez wywołanie SetLastModified lub wartość etag ustawiony przez wywołanie SetETag.</span><span class="sxs-lookup"><span data-stu-id="9d2bb-127">The cache validator can be a Last Modified timestamp set by calling SetLastModified, or an etag value set by calling SetETag.</span></span> <span data-ttu-id="9d2bb-128">Opcjonalnie można również określić czas wygaśnięcia pamięci podręcznej przez wywołanie metody SetExpires lub może polegać na domyślny algorytm heurystyczny pamięci podręcznej, opisem we wcześniejszej części tego dokumentu.</span><span class="sxs-lookup"><span data-stu-id="9d2bb-128">Optionally, you can also specify a cache expiration time by calling SetExpires, or you can rely on the default cache heuristics described earlier in this document.</span></span>  

<span data-ttu-id="9d2bb-129">Na przykład do pamięci podręcznej zawartości przez jedną godzinę, należy dodać:</span><span class="sxs-lookup"><span data-stu-id="9d2bb-129">For example, to cache content for one hour, add the following:</span></span>  

```csharp
// Set the caching parameters.
Response.Cache.SetExpires(DateTime.Now.AddHours(1));
Response.Cache.SetCacheability(HttpCacheability.Public);
Response.Cache.SetLastModified(DateTime.Now);
```

## <a name="next-steps"></a><span data-ttu-id="9d2bb-130">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9d2bb-130">Next Steps</span></span>
* [<span data-ttu-id="9d2bb-131">Przeczytaj szczegółowe informacje na temat **clientCache** — element</span><span class="sxs-lookup"><span data-stu-id="9d2bb-131">Read details about the **clientCache** element</span></span>](http://www.iis.net/ConfigReference/system.webServer/staticContent/clientCache)
* [<span data-ttu-id="9d2bb-132">Przeczytaj dokumentację **HttpResponse.Cache** właściwości</span><span class="sxs-lookup"><span data-stu-id="9d2bb-132">Read the documentation for the **HttpResponse.Cache** Property</span></span>](http://msdn.microsoft.com/library/system.web.httpresponse.cache.aspx) 
* <span data-ttu-id="9d2bb-133">[Przeczytaj dokumentację **klasy HttpCachePolicy**](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx).</span><span class="sxs-lookup"><span data-stu-id="9d2bb-133">[Read the documentation for the **HttpCachePolicy Class**](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx).</span></span>  

