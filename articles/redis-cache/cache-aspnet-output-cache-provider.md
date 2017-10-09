---
title: "aaaCache dostawcy pamięci podręcznej danych wyjściowych programu ASP.NET"
description: "Dowiedz się, jak toocache strony ASP.NET wyjściowe pamięci podręcznej Redis Azure"
services: redis-cache
documentationcenter: na
author: steved0x
manager: douge
editor: tysonn
ms.assetid: 78469a66-0829-484f-8660-b2598ec60fbf
ms.service: cache
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 02/14/2017
ms.author: sdanie
ms.openlocfilehash: fc38cc657604b351f55ad8febac383783ac29700
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="aspnet-output-cache-provider-for-azure-redis-cache"></a>Dostawcy pamięci podręcznej danych wyjściowych programu ASP.NET na platformie Azure pamięci podręcznej Redis
Witaj Redis dostawcy wyjściowej pamięci podręcznej jest mechanizm poza procesem magazynu danych w pamięci podręcznej danych wyjściowych. Dane te są specjalnie z myślą o pełnej odpowiedzi HTTP (strona buforowanie danych wyjściowych). Dostawca Hello podłącza się do hello nowe dane wyjściowe pamięci podręcznej dostawcy punkcie rozszerzenia wprowadzone w programie ASP.NET 4.

Witaj toouse Redis dostawcy wyjściowej pamięci podręcznej, najpierw skonfigurować pamięć podręczną, a następnie skonfiguruj aplikację ASP.NET przy użyciu pakietu NuGet dostawcy Redis pamięci podręcznej danych wyjściowych hello. W tym temacie znajdują się wskazówki dotyczące konfigurowania Twojej aplikacji hello toouse Redis dostawcy wyjściowej pamięci podręcznej. Aby uzyskać więcej informacji na temat tworzenia i konfigurowania wystąpienia pamięci podręcznej Redis Azure, zobacz [tworzenia pamięci podręcznej](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache).

## <a name="store-aspnet-page-output-in-hello-cache"></a>Przechowywanie danych wyjściowych strony ASP.NET w pamięci podręcznej hello
tooconfigure aplikacji klienckiej w programie Visual Studio przy użyciu pakietu NuGet stanu sesji pamięci podręcznej Redis hello, kliknij przycisk **Menedżera pakietów NuGet**, **Konsola Menedżera pakietów** z hello **narzędzia** menu.

Uruchom hello następujące polecenie z hello `Package Manager Console` okna.
    
```
Install-Package Microsoft.Web.RedisOutputCacheProvider
```

Pakiet NuGet dostawcy Redis pamięci podręcznej danych wyjściowych Hello ma zależność na powitania StackExchange.Redis.StrongName pakietu. Jeśli w projekcie nie ma pakietu StackExchange.Redis.StrongName hello, jest zainstalowana. Aby uzyskać więcej informacji o pakiecie NuGet dostawcy Redis pamięci podręcznej danych wyjściowych hello, zobacz hello [RedisOutputCacheProvider](https://www.nuget.org/packages/Microsoft.Web.RedisOutputCacheProvider/) NuGet strony.

>[!NOTE]
>Dodanie toohello o silnych nazwach StackExchange.Redis.StrongName pakietu jest również hello programie StackExchange.Redis nie-o silnych nazwach wersji. Jeśli projekt używa hello nie-o silnych nazwach programie StackExchange.Redis wersji należy go odinstalować, w przeciwnym razie możesz pobrać konfliktów nazw w projekcie. Aby uzyskać więcej informacji na temat tych pakietów, zobacz [.NET Konfigurowanie klientów pamięci podręcznej](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients).
>
>

Hello NuGet pakietu pliki do pobrania i dodaje hello wymagany zestaw odwołuje się i dodaje hello następujących sekcji w pliku web.config. Ta sekcja zawiera hello wymagana konfiguracja dla hello toouse aplikacji programu ASP.NET Redis dostawcy wyjściowej pamięci podręcznej.

```xml
<caching>
  <outputCachedefault Provider="MyRedisOutputCache">
    <providers>
      <!--
      <add name="MyRedisOutputCache"
        host = "127.0.0.1" [String]
        port = "" [number]
        accessKey = "" [String]
        ssl = "false" [true|false]
        databaseId = "0" [number]
        applicationName = "" [String]
        connectionTimeoutInMilliseconds = "5000" [number]
        operationTimeoutInMilliseconds = "5000" [number]
      />
      -->
      <add name="MyRedisOutputCache" type="Microsoft.Web.Redis.RedisOutputCacheProvider" host="127.0.0.1" accessKey="" ssl="false"/>
    </providers>
  </outputCache>
</caching>
```

Hello stwierdził, że sekcja zawiera przykład atrybuty hello i przykładowe ustawienia dla każdego atrybutu.

Skonfiguruj atrybuty hello hello wartościami z Twojej blok pamięci podręcznej w portalu Microsoft Azure hello oraz hello inne wartości zgodnie z potrzebami. Aby uzyskać instrukcje dotyczące uzyskiwania dostępu do właściwości pamięci podręcznej, zobacz [Redis skonfigurować ustawienia pamięci podręcznej](cache-configure.md#configure-redis-cache-settings).

* **host** — Określ punktu końcowego pamięci podręcznej.
* **port** — port bez protokołu SSL lub portem SSL, w zależności od hello ustawienia protokołu ssl.
* **accessKey** — Użyj albo hello klucz podstawowy lub pomocniczy dla pamięci podręcznej.
* **Protokół SSL** — wartość true, jeśli chcesz toosecure pamięci podręcznej/klienta komunikacji z użyciem protokołu ssl; w przeciwnym razie wartość false. Należy się toospecify hello poprawnego portu.
  * port bez protokołu SSL Hello jest domyślnie wyłączona, dla nowych pamięci podręcznych. Określ wartość true dla tej hello toouse ustawienie portu protokołu SSL. Aby uzyskać więcej informacji na temat włączania portu bez protokołu SSL hello Zobacz hello [porty dostępu](cache-configure.md#access-ports) części hello [skonfigurować pamięć podręczną](cache-configure.md) tematu.
* **databaseId** — określone dane wyjściowe toouse bazy danych, które dla pamięci podręcznej. Jeśli nie zostanie określony, zostanie użyta hello domyślna wartość 0.
* **applicationName** — klucze są przechowywane w pamięci podręcznej redis jako `<AppName>_<SessionId>_Data`. Ten schemat nazewnictwa umożliwia wielu hello tooshare aplikacji tego samego klucza. Ten parametr jest opcjonalny i jeśli nie zostanie określona wartość domyślna jest używany.
* **connectionTimeoutInMilliseconds** — to ustawienie umożliwia ustawianie na powitania klienta programie StackExchange.Redis connectTimeout hello toooverride. Jeśli nie zostanie określony, hello domyślne ustawienie connectTimeout 5000 jest używany. Aby uzyskać więcej informacji, zobacz [model konfiguracji w programie StackExchange.Redis](http://go.microsoft.com/fwlink/?LinkId=398705).
* **operationTimeoutInMilliseconds** — to ustawienie umożliwia ustawianie na powitania klienta programie StackExchange.Redis syncTimeout hello toooverride. Jeśli nie zostanie określony, hello syncTimeout domyślnie 1000 jest używany. Aby uzyskać więcej informacji, zobacz [model konfiguracji w programie StackExchange.Redis](http://go.microsoft.com/fwlink/?LinkId=398705).

Dodaj stronę tooeach w dyrektywie OutputCache dla którego chcesz toocache hello w danych wyjściowych.

```
<%@ OutputCache Duration="60" VaryByParam="*" %>
```

W poprzednim przykładzie hello hello buforowane strony danych pozostaje w pamięci podręcznej hello przez 60 sekund, a inna wersja hello strony są buforowane dla każdej kombinacji parametrów. Aby uzyskać więcej informacji na temat dyrektywy OutputCache hello zobacz [ @OutputCache ](http://go.microsoft.com/fwlink/?linkid=320837).

Po te kroki są wykonywane, aplikacja jest skonfigurowana toouse hello Redis dostawcy wyjściowej pamięci podręcznej.

## <a name="next-steps"></a>Następne kroki
Zapoznaj się z hello [dostawcę stanu sesji ASP.NET dla pamięci podręcznej Redis Azure](cache-aspnet-session-state-provider.md).

