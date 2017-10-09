---
title: "aaaCache dostawcę stanu sesji ASP.NET | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak stan sesji ASP.NET toostore przy użyciu pamięci podręcznej Redis Azure"
services: redis-cache
documentationcenter: na
author: steved0x
manager: douge
editor: tysonn
ms.assetid: 192f384c-836a-479a-bb65-8c3e6d6522bb
ms.service: cache
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 05/01/2017
ms.author: sdanie
ms.openlocfilehash: 9ea84cf67b9314b15dce696f596d399921194510
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="aspnet-session-state-provider-for-azure-redis-cache"></a>Dostawca stanu sesji ASP.NET dla usługi Azure Redis Cache
Pamięć podręczna Redis Azure udostępnia dostawcę stanu sesji można używać toostore Twojego stanu sesji w pamięci podręcznej, a nie w pamięci lub na serwerze SQL w bazie danych. toouse hello buforowania dostawcę stanu sesji, najpierw skonfigurować pamięć podręczną, a następnie skonfiguruj aplikację ASP.NET przy użyciu pakietu NuGet stanu sesji pamięci podręcznej Redis hello pamięci podręcznej.

Często nie jest praktyczne w chmurze rzeczywistych tooavoid aplikacji, przechowywanie jakiegoś stanu sesji użytkownika, ale niektóre podejścia mieć wpływ na wydajność i skalowalność więcej niż inne. Jeśli masz stanu toostore hello najlepszym rozwiązaniem jest stan mała ilość hello tookeep i zapisze go w plikach cookie. Jeśli, który nie jest możliwe, hello dalej najlepszym rozwiązaniem jest toouse stanu sesji ASP.NET u dostawcy dla rozproszonych, w pamięci podręcznej. Hello najgorszy rozwiązaniem z punktu widzenia wydajności i skalowalności jest toouse dostawcę stanu sesji kopii zapasowej bazy danych. W tym temacie znajdują się wskazówki dotyczące używania hello dostawcę stanu sesji ASP.NET dla pamięci podręcznej Redis Azure. Aby uzyskać informacje o innych opcjach stanu sesji, zobacz [opcje stanu sesji ASP.NET](#aspnet-session-state-options).

## <a name="store-aspnet-session-state-in-hello-cache"></a>Przechowywanie stanu sesji ASP.NET w pamięci podręcznej hello
tooconfigure aplikacji klienckiej w programie Visual Studio przy użyciu pakietu NuGet stanu sesji pamięci podręcznej Redis hello, kliknij przycisk **Menedżera pakietów NuGet**, **Konsola Menedżera pakietów** z hello **narzędzia** menu.

Uruchom hello następujące polecenie z hello `Package Manager Console` okna.
    
```
Install-Package Microsoft.Web.RedisSessionStateProvider
```

> [!IMPORTANT]
> Jeśli używasz funkcji Klaster z warstwy premium hello hello, musisz użyć [pakietu RedisSessionStateProvider](https://www.nuget.org/packages/Microsoft.Web.RedisSessionStateProvider) 2.0.1 lub nowszej albo wyjątek zostanie zgłoszony. Przenoszenie too2.0.1 lub nowszej jest istotne zmiany; Aby uzyskać więcej informacji, zobacz [v2.0.0 fundamentalne zmiany szczegółów](https://github.com/Azure/aspnet-redis-providers/wiki/v2.0.0-Breaking-Change-Details). W czasie hello aktualizacji tego artykułu hello bieżąca wersja tego pakietu jest 2.2.3.
> 
> 

Pakiet NuGet dostawcę stanu sesji Redis Hello ma zależność na powitania StackExchange.Redis.StrongName pakietu. Jeśli w projekcie nie ma pakietu StackExchange.Redis.StrongName hello, jest zainstalowana.

>[!NOTE]
>Dodanie toohello o silnych nazwach StackExchange.Redis.StrongName pakietu jest również hello programie StackExchange.Redis nie-o silnych nazwach wersji. Jeśli projekt używa hello nie-o silnych nazwach programie StackExchange.Redis wersji należy go odinstalować, w przeciwnym razie możesz pobrać konfliktów nazw w projekcie. Aby uzyskać więcej informacji na temat tych pakietów, zobacz [.NET Konfigurowanie klientów pamięci podręcznej](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients).
>
>

Hello NuGet pakietu pliki do pobrania i dodaje hello wymagany zestaw odwołuje się i dodaje hello następujących sekcji w pliku web.config. Ta sekcja zawiera hello wymagana konfiguracja dla hello toouse aplikacji programu ASP.NET dostawcę stanu sesji pamięci podręcznej Redis.

```xml
<sessionState mode="Custom" customProvider="MySessionStateStore">
    <providers>
    <!--
    <add name="MySessionStateStore"
           host = "127.0.0.1" [String]
        port = "" [number]
        accessKey = "" [String]
        ssl = "false" [true|false]
        throwOnError = "true" [true|false]
        retryTimeoutInMilliseconds = "0" [number]
        databaseId = "0" [number]
        applicationName = "" [String]
        connectionTimeoutInMilliseconds = "5000" [number]
        operationTimeoutInMilliseconds = "5000" [number]
    />
    -->
    <add name="MySessionStateStore" type="Microsoft.Web.Redis.RedisSessionStateProvider" host="127.0.0.1" accessKey="" ssl="false"/>
    </providers>
</sessionState>
```

Hello stwierdził, że sekcja zawiera przykład atrybuty hello i przykładowe ustawienia dla każdego atrybutu.

Skonfiguruj atrybuty hello hello wartościami z Twojej blok pamięci podręcznej w portalu Microsoft Azure hello oraz hello inne wartości zgodnie z potrzebami. Aby uzyskać instrukcje dotyczące uzyskiwania dostępu do właściwości pamięci podręcznej, zobacz [Redis skonfigurować ustawienia pamięci podręcznej](cache-configure.md#configure-redis-cache-settings).

* **host** — Określ punktu końcowego pamięci podręcznej.
* **port** — port bez protokołu SSL lub portem SSL, w zależności od hello ustawienia protokołu ssl.
* **accessKey** — Użyj albo hello klucz podstawowy lub pomocniczy dla pamięci podręcznej.
* **Protokół SSL** — wartość true, jeśli chcesz toosecure pamięci podręcznej/klienta komunikacji z użyciem protokołu ssl; w przeciwnym razie wartość false. Należy się toospecify hello poprawnego portu.
  * port bez protokołu SSL Hello jest domyślnie wyłączona, dla nowych pamięci podręcznych. Określ wartość true dla tej hello toouse ustawienie portu protokołu SSL. Aby uzyskać więcej informacji na temat włączania portu bez protokołu SSL hello Zobacz hello [porty dostępu](cache-configure.md#access-ports) części hello [skonfigurować pamięć podręczną](cache-configure.md) tematu.
* **throwOnError** — wartość true, jeśli chcesz toobe wyjątek zgłoszony w przypadku awarii lub false Jeśli chcesz toofail operacji hello w trybie dyskretnym. Z powodu błędu można sprawdzić przez sprawdzenie właściwości statycznej Microsoft.Web.Redis.RedisSessionStateProvider.LastException hello. Witaj domyślna to true.
* **retryTimeoutInMilliseconds** — operacji, które nie są zwalniane w danym przedziale czasu wyrażona w milisekundach. pierwsza próba Hello występuje po 20 milisekund, a następnie wykonywane co sekundę do momentu wygaśnięcia hello retryTimeoutInMilliseconds interwału. Natychmiast po tym okresie operacji hello próba zostanie ponowiona jeden raz ostatni. Jeśli nadal nie operacji hello, hello wyjątku wstecz wywołującego toohello, w zależności od ustawienia throwOnError hello. Witaj, wartość domyślna to 0, co oznacza brak ponownych prób.
* **databaseId** — Określa, które toouse bazy danych dla pamięci podręcznej dane wyjściowe. Jeśli nie zostanie określony, zostanie użyta hello domyślna wartość 0.
* **applicationName** — klucze są przechowywane w pamięci podręcznej redis jako `{<Application Name>_<Session ID>}_Data`. Ten schemat nazewnictwa umożliwia wielu aplikacjom tooshare hello tego samego wystąpienia pamięci podręcznej Redis. Ten parametr jest opcjonalny i jeśli nie zostanie określona wartość domyślna jest używany.
* **connectionTimeoutInMilliseconds** — to ustawienie umożliwia ustawianie na powitania klienta programie StackExchange.Redis connectTimeout hello toooverride. Jeśli nie zostanie określony, hello domyślne ustawienie connectTimeout 5000 jest używany. Aby uzyskać więcej informacji, zobacz [model konfiguracji w programie StackExchange.Redis](http://go.microsoft.com/fwlink/?LinkId=398705).
* **operationTimeoutInMilliseconds** — to ustawienie umożliwia ustawianie na powitania klienta programie StackExchange.Redis syncTimeout hello toooverride. Jeśli nie zostanie określony, hello syncTimeout domyślnie 1000 jest używany. Aby uzyskać więcej informacji, zobacz [model konfiguracji w programie StackExchange.Redis](http://go.microsoft.com/fwlink/?LinkId=398705).

Aby uzyskać więcej informacji na temat tych właściwości, zobacz hello oryginalnego blogu post powiadomienie na [Announcing ASP.NET dostawcę stanu sesji dla pamięci podręcznej Redis](http://blogs.msdn.com/b/webdev/archive/2014/05/12/announcing-asp-net-session-state-provider-for-redis-preview-release.aspx).

Nie zapomnij toocomment limit hello standardowej InProc sesji stanu dostawcy sekcji w pliku web.config.

```xml
<!-- <sessionState mode="InProc"
     customProvider="DefaultSessionProvider">
     <providers>
        <add name="DefaultSessionProvider"
              type="System.Web.Providers.DefaultSessionStateProvider,
                    System.Web.Providers, Version=1.0.0.0, Culture=neutral,
                    PublicKeyToken=31bf3856ad364e35"
              connectionStringName="DefaultConnection" />
      </providers>
</sessionState> -->
```

Te kroki są wykonywane, aplikacji po hello toouse skonfigurowanego dostawcy stanu sesji pamięci podręcznej Redis. Gdy używasz stanu sesji w aplikacji, jest ona przechowywana w wystąpienia pamięci podręcznej Redis Azure.

> [!IMPORTANT]
> Dane przechowywane w pamięci podręcznej hello musi być możliwy do serializacji, w odróżnieniu od hello danych, które mogą być przechowywane w hello domyślny dostawca stanu sesji ASP.NET w pamięci. W przypadku hello dostawcę stanu sesji dla pamięci podręcznej Redis upewnij się że hello typów danych, które są przechowywane w stanie sesji są możliwy do serializacji.
> 
> 

## <a name="aspnet-session-state-options"></a>Opcje stanu sesji ASP.NET
* Dostawca stanu sesji pamięci — ten dostawca przechowuje hello stanu sesji w pamięci. Zaletą Hello przy użyciu tego dostawcy jest jest proste i szybkie. Jednak nie można skalować aplikacji sieci Web, jeśli używasz w pamięci dostawcy, ponieważ nie będzie on rozpowszechniany.
* Dostawca stanu sesji SQL Server — ten dostawca przechowuje hello stanu sesji w programie Sql Server. Użyj tego dostawcy, jeśli stan sesji hello toostore magazynu trwałego. Można skalować aplikacji sieci Web, ale dla sesji przy użyciu programu Sql Server ma negatywny wpływ na wydajność w aplikacji sieci Web.
* Rozproszone w pamięci dostawcę stanu sesji takich jak Redis pamięci podręcznej dostawcę stanu sesji — dzięki temu dostawcy hello najlepsze cechy obu tych środowisk. Aplikacja sieci Web może mieć proste, szybkie i skalowalne dostawcę stanu sesji. Ponieważ tego dostawcy magazynów hello stanu sesji w pamięci podręcznej, aplikacja ma tootake pod uwagę w wszystkie hello charakterystyki skojarzonej w przypadku tooa rozproszonych w pamięci podręcznej, takie jak awarie sieci. Najlepsze rozwiązania dotyczące używania pamięci podręcznej, zobacz [buforowanie wskazówki](../best-practices-caching.md) z Microsoft Patterns & rozwiązań [projekt aplikacji w chmurze Azure i wskazówki dotyczące implementacji](https://github.com/mspnp/azure-guidance).

Aby uzyskać więcej informacji o stanie sesji i innych najlepszych rozwiązań, zobacz [Web Development Best Practices (kompilowanie praktyczne aplikacje w chmurze platformy Azure)](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices).

## <a name="next-steps"></a>Następne kroki
Zapoznaj się z hello [dostawcy wyjściowej pamięci podręcznej programu ASP.NET dla pamięci podręcznej Redis Azure](cache-aspnet-output-cache-provider.md).

