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
# <a name="aspnet-output-cache-provider-for-azure-redis-cache"></a><span data-ttu-id="6d1be-103">Dostawcy pamięci podręcznej danych wyjściowych programu ASP.NET na platformie Azure pamięci podręcznej Redis</span><span class="sxs-lookup"><span data-stu-id="6d1be-103">ASP.NET Output Cache Provider for Azure Redis Cache</span></span>
<span data-ttu-id="6d1be-104">Witaj Redis dostawcy wyjściowej pamięci podręcznej jest mechanizm poza procesem magazynu danych w pamięci podręcznej danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="6d1be-104">hello Redis Output Cache Provider is an out-of-process storage mechanism for output cache data.</span></span> <span data-ttu-id="6d1be-105">Dane te są specjalnie z myślą o pełnej odpowiedzi HTTP (strona buforowanie danych wyjściowych).</span><span class="sxs-lookup"><span data-stu-id="6d1be-105">This data is specifically for full HTTP responses (page output caching).</span></span> <span data-ttu-id="6d1be-106">Dostawca Hello podłącza się do hello nowe dane wyjściowe pamięci podręcznej dostawcy punkcie rozszerzenia wprowadzone w programie ASP.NET 4.</span><span class="sxs-lookup"><span data-stu-id="6d1be-106">hello provider plugs into hello new output cache provider extensibility point that was introduced in ASP.NET 4.</span></span>

<span data-ttu-id="6d1be-107">Witaj toouse Redis dostawcy wyjściowej pamięci podręcznej, najpierw skonfigurować pamięć podręczną, a następnie skonfiguruj aplikację ASP.NET przy użyciu pakietu NuGet dostawcy Redis pamięci podręcznej danych wyjściowych hello.</span><span class="sxs-lookup"><span data-stu-id="6d1be-107">toouse hello Redis Output Cache Provider, first configure your cache, and then configure your ASP.NET application using hello Redis Output Cache Provider NuGet package.</span></span> <span data-ttu-id="6d1be-108">W tym temacie znajdują się wskazówki dotyczące konfigurowania Twojej aplikacji hello toouse Redis dostawcy wyjściowej pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="6d1be-108">This topic provides guidance on configuring your application toouse hello Redis Output Cache Provider.</span></span> <span data-ttu-id="6d1be-109">Aby uzyskać więcej informacji na temat tworzenia i konfigurowania wystąpienia pamięci podręcznej Redis Azure, zobacz [tworzenia pamięci podręcznej](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache).</span><span class="sxs-lookup"><span data-stu-id="6d1be-109">For more information about creating and configuring an Azure Redis Cache instance, see [Create a cache](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache).</span></span>

## <a name="store-aspnet-page-output-in-hello-cache"></a><span data-ttu-id="6d1be-110">Przechowywanie danych wyjściowych strony ASP.NET w pamięci podręcznej hello</span><span class="sxs-lookup"><span data-stu-id="6d1be-110">Store ASP.NET page output in hello cache</span></span>
<span data-ttu-id="6d1be-111">tooconfigure aplikacji klienckiej w programie Visual Studio przy użyciu pakietu NuGet stanu sesji pamięci podręcznej Redis hello, kliknij przycisk **Menedżera pakietów NuGet**, **Konsola Menedżera pakietów** z hello **narzędzia** menu.</span><span class="sxs-lookup"><span data-stu-id="6d1be-111">tooconfigure a client application in Visual Studio using hello Redis Cache Session State NuGet package, click **NuGet Package Manager**, **Package Manager Console** from hello **Tools** menu.</span></span>

<span data-ttu-id="6d1be-112">Uruchom hello następujące polecenie z hello `Package Manager Console` okna.</span><span class="sxs-lookup"><span data-stu-id="6d1be-112">Run hello following command from hello `Package Manager Console` window.</span></span>
    
```
Install-Package Microsoft.Web.RedisOutputCacheProvider
```

<span data-ttu-id="6d1be-113">Pakiet NuGet dostawcy Redis pamięci podręcznej danych wyjściowych Hello ma zależność na powitania StackExchange.Redis.StrongName pakietu.</span><span class="sxs-lookup"><span data-stu-id="6d1be-113">hello Redis Output Cache Provider NuGet package has a dependency on hello StackExchange.Redis.StrongName package.</span></span> <span data-ttu-id="6d1be-114">Jeśli w projekcie nie ma pakietu StackExchange.Redis.StrongName hello, jest zainstalowana.</span><span class="sxs-lookup"><span data-stu-id="6d1be-114">If hello StackExchange.Redis.StrongName package is not present in your project, it is installed.</span></span> <span data-ttu-id="6d1be-115">Aby uzyskać więcej informacji o pakiecie NuGet dostawcy Redis pamięci podręcznej danych wyjściowych hello, zobacz hello [RedisOutputCacheProvider](https://www.nuget.org/packages/Microsoft.Web.RedisOutputCacheProvider/) NuGet strony.</span><span class="sxs-lookup"><span data-stu-id="6d1be-115">For more information about hello Redis Output Cache Provider NuGet package, see hello [RedisOutputCacheProvider](https://www.nuget.org/packages/Microsoft.Web.RedisOutputCacheProvider/) NuGet page.</span></span>

>[!NOTE]
><span data-ttu-id="6d1be-116">Dodanie toohello o silnych nazwach StackExchange.Redis.StrongName pakietu jest również hello programie StackExchange.Redis nie-o silnych nazwach wersji.</span><span class="sxs-lookup"><span data-stu-id="6d1be-116">In addition toohello strong-named StackExchange.Redis.StrongName package, there is also hello StackExchange.Redis non-strong-named version.</span></span> <span data-ttu-id="6d1be-117">Jeśli projekt używa hello nie-o silnych nazwach programie StackExchange.Redis wersji należy go odinstalować, w przeciwnym razie możesz pobrać konfliktów nazw w projekcie.</span><span class="sxs-lookup"><span data-stu-id="6d1be-117">If your project is using hello non-strong-named StackExchange.Redis version you must uninstall it, otherwise you get naming conflicts in your project.</span></span> <span data-ttu-id="6d1be-118">Aby uzyskać więcej informacji na temat tych pakietów, zobacz [.NET Konfigurowanie klientów pamięci podręcznej](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients).</span><span class="sxs-lookup"><span data-stu-id="6d1be-118">For more information about these packages, see [Configure .NET cache clients](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients).</span></span>
>
>

<span data-ttu-id="6d1be-119">Hello NuGet pakietu pliki do pobrania i dodaje hello wymagany zestaw odwołuje się i dodaje hello następujących sekcji w pliku web.config.</span><span class="sxs-lookup"><span data-stu-id="6d1be-119">hello NuGet package downloads and adds hello required assembly references and adds hello following section into your web.config file.</span></span> <span data-ttu-id="6d1be-120">Ta sekcja zawiera hello wymagana konfiguracja dla hello toouse aplikacji programu ASP.NET Redis dostawcy wyjściowej pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="6d1be-120">This section contains hello required configuration for your ASP.NET application toouse hello Redis Output Cache Provider.</span></span>

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

<span data-ttu-id="6d1be-121">Hello stwierdził, że sekcja zawiera przykład atrybuty hello i przykładowe ustawienia dla każdego atrybutu.</span><span class="sxs-lookup"><span data-stu-id="6d1be-121">hello commented section provides an example of hello attributes and sample settings for each attribute.</span></span>

<span data-ttu-id="6d1be-122">Skonfiguruj atrybuty hello hello wartościami z Twojej blok pamięci podręcznej w portalu Microsoft Azure hello oraz hello inne wartości zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="6d1be-122">Configure hello attributes with hello values from your cache blade in hello Microsoft Azure portal, and configure hello other values as desired.</span></span> <span data-ttu-id="6d1be-123">Aby uzyskać instrukcje dotyczące uzyskiwania dostępu do właściwości pamięci podręcznej, zobacz [Redis skonfigurować ustawienia pamięci podręcznej](cache-configure.md#configure-redis-cache-settings).</span><span class="sxs-lookup"><span data-stu-id="6d1be-123">For instructions on accessing your cache properties, see [Configure Redis cache settings](cache-configure.md#configure-redis-cache-settings).</span></span>

* <span data-ttu-id="6d1be-124">**host** — Określ punktu końcowego pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="6d1be-124">**host** – specify your cache endpoint.</span></span>
* <span data-ttu-id="6d1be-125">**port** — port bez protokołu SSL lub portem SSL, w zależności od hello ustawienia protokołu ssl.</span><span class="sxs-lookup"><span data-stu-id="6d1be-125">**port** – use either your non-SSL port or your SSL port, depending on hello ssl settings.</span></span>
* <span data-ttu-id="6d1be-126">**accessKey** — Użyj albo hello klucz podstawowy lub pomocniczy dla pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="6d1be-126">**accessKey** – use either hello primary or secondary key for your cache.</span></span>
* <span data-ttu-id="6d1be-127">**Protokół SSL** — wartość true, jeśli chcesz toosecure pamięci podręcznej/klienta komunikacji z użyciem protokołu ssl; w przeciwnym razie wartość false.</span><span class="sxs-lookup"><span data-stu-id="6d1be-127">**ssl** – true if you want toosecure cache/client communications with ssl; otherwise false.</span></span> <span data-ttu-id="6d1be-128">Należy się toospecify hello poprawnego portu.</span><span class="sxs-lookup"><span data-stu-id="6d1be-128">Be sure toospecify hello correct port.</span></span>
  * <span data-ttu-id="6d1be-129">port bez protokołu SSL Hello jest domyślnie wyłączona, dla nowych pamięci podręcznych.</span><span class="sxs-lookup"><span data-stu-id="6d1be-129">hello non-SSL port is disabled by default for new caches.</span></span> <span data-ttu-id="6d1be-130">Określ wartość true dla tej hello toouse ustawienie portu protokołu SSL.</span><span class="sxs-lookup"><span data-stu-id="6d1be-130">Specify true for this setting toouse hello SSL port.</span></span> <span data-ttu-id="6d1be-131">Aby uzyskać więcej informacji na temat włączania portu bez protokołu SSL hello Zobacz hello [porty dostępu](cache-configure.md#access-ports) części hello [skonfigurować pamięć podręczną](cache-configure.md) tematu.</span><span class="sxs-lookup"><span data-stu-id="6d1be-131">For more information about enabling hello non-SSL port, see hello [Access Ports](cache-configure.md#access-ports) section in hello [Configure a cache](cache-configure.md) topic.</span></span>
* <span data-ttu-id="6d1be-132">**databaseId** — określone dane wyjściowe toouse bazy danych, które dla pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="6d1be-132">**databaseId** – Specified which database toouse for cache output data.</span></span> <span data-ttu-id="6d1be-133">Jeśli nie zostanie określony, zostanie użyta hello domyślna wartość 0.</span><span class="sxs-lookup"><span data-stu-id="6d1be-133">If not specified, hello default value of 0 is used.</span></span>
* <span data-ttu-id="6d1be-134">**applicationName** — klucze są przechowywane w pamięci podręcznej redis jako `<AppName>_<SessionId>_Data`.</span><span class="sxs-lookup"><span data-stu-id="6d1be-134">**applicationName** – Keys are stored in redis as `<AppName>_<SessionId>_Data`.</span></span> <span data-ttu-id="6d1be-135">Ten schemat nazewnictwa umożliwia wielu hello tooshare aplikacji tego samego klucza.</span><span class="sxs-lookup"><span data-stu-id="6d1be-135">This naming scheme enables multiple applications tooshare hello same key.</span></span> <span data-ttu-id="6d1be-136">Ten parametr jest opcjonalny i jeśli nie zostanie określona wartość domyślna jest używany.</span><span class="sxs-lookup"><span data-stu-id="6d1be-136">This parameter is optional and if you do not provide it a default value is used.</span></span>
* <span data-ttu-id="6d1be-137">**connectionTimeoutInMilliseconds** — to ustawienie umożliwia ustawianie na powitania klienta programie StackExchange.Redis connectTimeout hello toooverride.</span><span class="sxs-lookup"><span data-stu-id="6d1be-137">**connectionTimeoutInMilliseconds** – This setting allows you toooverride hello connectTimeout setting in hello StackExchange.Redis client.</span></span> <span data-ttu-id="6d1be-138">Jeśli nie zostanie określony, hello domyślne ustawienie connectTimeout 5000 jest używany.</span><span class="sxs-lookup"><span data-stu-id="6d1be-138">If not specified, hello default connectTimeout setting of 5000 is used.</span></span> <span data-ttu-id="6d1be-139">Aby uzyskać więcej informacji, zobacz [model konfiguracji w programie StackExchange.Redis](http://go.microsoft.com/fwlink/?LinkId=398705).</span><span class="sxs-lookup"><span data-stu-id="6d1be-139">For more information, see [StackExchange.Redis configuration model](http://go.microsoft.com/fwlink/?LinkId=398705).</span></span>
* <span data-ttu-id="6d1be-140">**operationTimeoutInMilliseconds** — to ustawienie umożliwia ustawianie na powitania klienta programie StackExchange.Redis syncTimeout hello toooverride.</span><span class="sxs-lookup"><span data-stu-id="6d1be-140">**operationTimeoutInMilliseconds** – This setting allows you toooverride hello syncTimeout setting in hello StackExchange.Redis client.</span></span> <span data-ttu-id="6d1be-141">Jeśli nie zostanie określony, hello syncTimeout domyślnie 1000 jest używany.</span><span class="sxs-lookup"><span data-stu-id="6d1be-141">If not specified, hello default syncTimeout setting of 1000 is used.</span></span> <span data-ttu-id="6d1be-142">Aby uzyskać więcej informacji, zobacz [model konfiguracji w programie StackExchange.Redis](http://go.microsoft.com/fwlink/?LinkId=398705).</span><span class="sxs-lookup"><span data-stu-id="6d1be-142">For more information, see [StackExchange.Redis configuration model](http://go.microsoft.com/fwlink/?LinkId=398705).</span></span>

<span data-ttu-id="6d1be-143">Dodaj stronę tooeach w dyrektywie OutputCache dla którego chcesz toocache hello w danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="6d1be-143">Add an OutputCache directive tooeach page for which you wish toocache hello output.</span></span>

```
<%@ OutputCache Duration="60" VaryByParam="*" %>
```

<span data-ttu-id="6d1be-144">W poprzednim przykładzie hello hello buforowane strony danych pozostaje w pamięci podręcznej hello przez 60 sekund, a inna wersja hello strony są buforowane dla każdej kombinacji parametrów.</span><span class="sxs-lookup"><span data-stu-id="6d1be-144">In hello previous example, hello cached page data remains in hello cache for 60 seconds, and a different version of hello page is cached for each parameter combination.</span></span> <span data-ttu-id="6d1be-145">Aby uzyskać więcej informacji na temat dyrektywy OutputCache hello zobacz [ @OutputCache ](http://go.microsoft.com/fwlink/?linkid=320837).</span><span class="sxs-lookup"><span data-stu-id="6d1be-145">For more information about hello OutputCache directive, see [@OutputCache](http://go.microsoft.com/fwlink/?linkid=320837).</span></span>

<span data-ttu-id="6d1be-146">Po te kroki są wykonywane, aplikacja jest skonfigurowana toouse hello Redis dostawcy wyjściowej pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="6d1be-146">Once these steps are performed, your application is configured toouse hello Redis Output Cache Provider.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6d1be-147">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6d1be-147">Next steps</span></span>
<span data-ttu-id="6d1be-148">Zapoznaj się z hello [dostawcę stanu sesji ASP.NET dla pamięci podręcznej Redis Azure](cache-aspnet-session-state-provider.md).</span><span class="sxs-lookup"><span data-stu-id="6d1be-148">Check out hello [ASP.NET Session State Provider for Azure Redis Cache](cache-aspnet-session-state-provider.md).</span></span>

