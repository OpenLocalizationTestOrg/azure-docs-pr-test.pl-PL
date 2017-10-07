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
# <a name="session-state-with-azure-redis-cache-in-azure-app-service"></a>Stan sesji i usługa Azure Redis Cache w usłudze Azure App Service
W tym temacie wyjaśniono, jak toouse hello usługi pamięć podręczna Redis Azure dla stanu sesji.

Jeśli aplikacja sieci web platformy ASP.NET używa stanu sesji, należy tooconfigure zewnętrznego dostawcę stanu sesji (hello usługi pamięć podręczna Redis lub dostawcę stanu sesji SQL Server). Jeśli używasz stanu sesji i nie używasz dostawcy zewnętrznego, będzie ograniczona tooone wystąpienie aplikacji sieci web. Witaj usługi pamięć podręczna Redis jest tooenable najszybszym i najprostszym hello.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a id="createcache"></a>Utwórz hello pamięci podręcznej
Postępuj zgodnie z [te kierunkach](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#create-cache) toocreate hello w pamięci podręcznej.

## <a id="configureproject"></a>Dodawanie pakietu RedisSessionStateProvider NuGet pakietu tooyour sieci web aplikacji hello
Zainstaluj hello NuGet `RedisSessionStateProvider` pakietu.  Użyj hello następujące polecenie tooinstall z konsoli Menedżera pakietów hello (**narzędzia** > **Menedżera pakietów NuGet** > **Konsola Menedżera pakietów**):

  `PM> Install-Package Microsoft.Web.RedisSessionStateProvider`

tooinstall z **narzędzia** > **Menedżera pakietów NuGet** > **Zarządzaj pakietami NugGet dla rozwiązania**, wyszukaj `RedisSessionStateProvider`.

Aby uzyskać więcej informacji, zobacz hello [strony pakietu NuGet RedisSessionStateProvider](http://www.nuget.org/packages/Microsoft.Web.RedisSessionStateProvider/) i [Konfigurowanie klienta pamięci podręcznej hello](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#NuGet).

## <a id="configurewebconfig"></a>Modyfikowanie hello pliku Web.Config
Ponadto zestaw toomaking odwołuje się do pamięci podręcznej, hello pakiet NuGet Dodaje wpisy zastępcze w hello *web.config* pliku. 

1. Otwórz hello *web.config* i Znajdź hello hello **sessionState** elementu.
2. Wprowadź wartości hello `host`, `accessKey`, `port` (hello SSL port 6380) i ustaw `SSL` zbyt`true`. Te wartości można uzyskać z hello [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715) bloku dla swojego wystąpienia w pamięci podręcznej. Aby uzyskać więcej informacji, zobacz [połączyć z pamięci podręcznej toohello](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#connect-to-cache). Należy pamiętać, że port bez protokołu SSL hello jest domyślnie wyłączona dla nowych pamięci podręcznych. Aby uzyskać więcej informacji na temat włączania portu bez protokołu SSL hello Zobacz hello [porty dostępu](https://msdn.microsoft.com/library/azure/dn793612.aspx#AccessPorts) części hello [Konfigurowanie pamięci podręcznej w pamięci podręcznej Redis Azure](https://msdn.microsoft.com/library/azure/dn793612.aspx) tematu. Hello następujący kod przedstawia hello zmiany toohello *web.config* pliku, w szczególności zmiany hello zbyt*portu*, *hosta*, accessKey * i *ssl*.
   
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

## <a id="usesessionobject"></a>Użyj hello obiektu Session w kodzie
Ostatnim krokiem Hello jest toobegin przy użyciu hello obiektu Session w kodzie ASP.NET. Dodaj stan toosession obiektów przy użyciu hello **Session.Add** metody. Ta metoda używa par klucz wartość toostore elementów w pamięci podręcznej stanu sesji hello.

    string strValue = "yourvalue";
    Session.Add("yourkey", strValue);

powitania po kod pobiera tę wartość ze stanu sesji.

    object objValue = Session["yourkey"];
    if (objValue != null)
       strValue = (string)objValue;    

Umożliwia także hello pamięci podręcznej Redis toocache obiektów w aplikacji sieci web. Aby uzyskać więcej informacji, zobacz [MVC movie app with Azure Redis Cache in 15 minutes](https://azure.microsoft.com/blog/2014/06/05/mvc-movie-app-with-azure-redis-cache-in-15-minutes/) (Tworzenie aplikacji filmowej MVC przy użyciu usługi Azure Redis Cache w ciągu 15 minut).
Aby uzyskać więcej informacji na temat stanu sesji ASP.NET toouse, zobacz [przegląd stanu sesji ASP.NET][ASP.NET Session State Overview].

> [!NOTE]
> Tooget wprowadzenie do usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź zbyt[Wypróbuj usługę App Service](https://azure.microsoft.com/try/app-service/), gdzie możesz od razu utworzyć krótkotrwałą, początkową aplikację sieci web w usłudze App Service. Bez kart kredytowych i bez zobowiązań.
> 
> 

## <a name="whats-changed"></a>Co zostało zmienione
* Toohello przewodnik zmiany z tooApp witryn sieci Web usługi dla: [usłudze Azure App Service i jej wpływ na istniejące usługi platformy Azure](http://go.microsoft.com/fwlink/?LinkId=529714)
  
  *Autor: [Rick Anderson](https://twitter.com/RickAndMSFT)*

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

