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
# <a name="manage-expiration-of-azure-web-appscloud-services-aspnet-or-iis-content-in-azure-cdn"></a>Zarządzaj wygasaniem zawartości usług Azure Web Apps/Cloud Services, ASP.NET lub usługi IIS w usłudze Azure CDN
> [!div class="op_single_selector"]
> * [Usługi aplikacji/w chmurze Azure sieci Web, ASP.NET lub usług IIS](cdn-manage-expiration-of-cloud-service-content.md)
> * [Usługa blob magazynu Azure](cdn-manage-expiration-of-blob-content.md)
> 
> 

Mogą być buforowane pliki z dowolnego publicznie dostępnego źródła serwera sieci web w usłudze Azure CDN, dopóki nie upłynie jego czas wygaśnięcia (TTL).  Witaj czas wygaśnięcia jest określany przez hello [ *Cache-Control* nagłówka](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) hello HTTP odpowiedzi z serwera źródłowego hello.  W tym artykule opisano sposób tooset `Cache-Control` nagłówki dla aplikacji sieci Web platformy Azure, usługi w chmurze Azure, aplikacji programu ASP.NET i witryny internetowe usługi informacyjne, które są skonfigurowane podobnie.

> [!TIP]
> Możesz wybrać tooset nie czas wygaśnięcia pliku.  W takim przypadku Azure CDN automatycznie stosuje domyślny czas wygaśnięcia wynosi siedem dni.
> 
> Aby uzyskać więcej informacji na temat działania usługi Azure CDN toospeed toofiles dostępu i innych zasobów, zobacz hello [Omówienie usługi Azure CDN](cdn-overview.md).
> 
> 

## <a name="setting-cache-control-headers-in-configuration"></a>Nagłówki Cache-Control ustawienia w konfiguracji
Dla zawartości statycznej, takich jak obrazy i arkusze stylów, możesz kontrolować częstotliwość aktualizacji hello modyfikując hello **applicationHost.config** lub **web.config** plików dla aplikacji sieci web.  Witaj **system.webServer\staticContent\clientCache** w pliku konfiguracji hello ustawi hello `Cache-Control` nagłówek dla zawartości. Aby uzyskać **web.config**, ustawienia konfiguracji hello będzie miało wpływ na wszystkie elementy w folderze hello i wszystkie podfoldery Jeśli zastąpiona na poziomie podfolder hello.  Na przykład można ustawić domyślnego time-to-live na powitania głównego toohave całej zawartości statycznej pamięci podręcznej dla 3 dni, ale ma podfolder, który ma więcej zmiennej zawartości z ustawieniem pamięci podręcznej 6 godzin.  Dla **applicationHost.config**, wszystkie aplikacje w witrynie hello zostaną zmienione, ale może zostać zastąpiona w **web.config** plików w aplikacji hello.

Witaj następujące XML przedstawiono przykład ustawienie **clientCache** toospecify, a maksymalny wiek 3 dni:  

```xml
<configuration>
    <system.webServer>
        <staticContent>
            <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="3.00:00:00" />
        </staticContent>
    </system.webServer>
</configuration>
```

Określanie **UseMaxAge** dodaje `Cache-Control: max-age=<nnn>` nagłówka toohello odpowiedzi na podstawie hello wartości określone w hello **CacheControlMaxAge** atrybutu. format Hello hello timespan jest dla hello **cacheControlMaxAge** atrybutu <days>.<hours>:<min>:<sec>. Aby uzyskać więcej informacji na temat hello **clientCache** węzła, zobacz [pamięci podręcznej klienta <clientCache> ](http://www.iis.net/ConfigReference/system.webServer/staticContent/clientCache).  

## <a name="setting-cache-control-headers-in-code"></a>Ustawianie Cache-Control nagłówków w kodzie
Dla aplikacji ASP.NET można ustawić zachowanie buforowania w sieci CDN hello programowo przez ustawienie hello **HttpResponse.Cache** właściwości. Aby uzyskać więcej informacji na temat hello **HttpResponse.Cache** właściwości, zobacz [właściwości HttpResponse.Cache](http://msdn.microsoft.com/library/system.web.httpresponse.cache.aspx) i [HttpCachePolicy klasy](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx).  

Jeśli chcesz tooprogrammatically pamięci podręcznej zawartość aplikacji ASP.NET, upewnij się, czy przez ustawienie zbyt HttpCacheability jest oznaczony jako buforowalnej zawartości hello*publicznego*. Ponadto upewnij się, że moduł weryfikacji pamięci podręcznej jest ustawiona. Moduł sprawdzania poprawności Hello pamięci podręcznej może być ostatniej modyfikacji sygnatury czasowej ustawiony przez wywołanie SetLastModified lub wartość etag ustawiony przez wywołanie SetETag. Opcjonalnie można również określić czas wygaśnięcia pamięci podręcznej przez wywołanie metody SetExpires lub może polegać na powitania: domyślny algorytm heurystyczny pamięci podręcznej opisem we wcześniejszej części tego dokumentu.  

Na przykład zawartość toocache przez jedną godzinę, Dodaj następujące hello:  

```csharp
// Set hello caching parameters.
Response.Cache.SetExpires(DateTime.Now.AddHours(1));
Response.Cache.SetCacheability(HttpCacheability.Public);
Response.Cache.SetLastModified(DateTime.Now);
```

## <a name="next-steps"></a>Następne kroki
* [Przeczytaj szczegółowe informacje o hello **clientCache** — element](http://www.iis.net/ConfigReference/system.webServer/staticContent/clientCache)
* [Zapoznaj się dokumentacją hello hello **HttpResponse.Cache** właściwości](http://msdn.microsoft.com/library/system.web.httpresponse.cache.aspx) 
* [Zapoznaj się dokumentacją hello hello **klasy HttpCachePolicy**](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx).  

