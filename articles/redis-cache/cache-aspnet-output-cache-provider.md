---
title: "Dostawcy pamięci podręcznej pamięci podręcznej danych wyjściowych programu ASP.NET"
description: "Dowiedz się, jak i pamięci podręcznej danych wyjściowych strony ASP.NET przy użyciu pamięci podręcznej Redis Azure"
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
ms.openlocfilehash: 845f25637a0e48460fc76c1ee36060274b3cec38
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="aspnet-output-cache-provider-for-azure-redis-cache"></a><span data-ttu-id="961f6-103">Dostawcy pamięci podręcznej danych wyjściowych programu ASP.NET na platformie Azure pamięci podręcznej Redis</span><span class="sxs-lookup"><span data-stu-id="961f6-103">ASP.NET Output Cache Provider for Azure Redis Cache</span></span>
<span data-ttu-id="961f6-104">Dostawcy Redis wyjściowej pamięci podręcznej jest mechanizmem poza procesem magazynu danych w pamięci podręcznej danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="961f6-104">The Redis Output Cache Provider is an out-of-process storage mechanism for output cache data.</span></span> <span data-ttu-id="961f6-105">Dane te są specjalnie z myślą o pełnej odpowiedzi HTTP (strona buforowanie danych wyjściowych).</span><span class="sxs-lookup"><span data-stu-id="961f6-105">This data is specifically for full HTTP responses (page output caching).</span></span> <span data-ttu-id="961f6-106">Dostawca podłącza się do nowego dane wyjściowe pamięci podręcznej dostawcy rozszerzeń punktu wprowadzone w programie ASP.NET 4.</span><span class="sxs-lookup"><span data-stu-id="961f6-106">The provider plugs into the new output cache provider extensibility point that was introduced in ASP.NET 4.</span></span>

<span data-ttu-id="961f6-107">Aby użyć dostawcy Redis wyjściowej pamięci podręcznej, najpierw skonfigurować pamięć podręczną, a następnie skonfiguruj aplikację ASP.NET przy użyciu pakietu NuGet dostawcy Redis pamięci podręcznej danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="961f6-107">To use the Redis Output Cache Provider, first configure your cache, and then configure your ASP.NET application using the Redis Output Cache Provider NuGet package.</span></span> <span data-ttu-id="961f6-108">W tym temacie znajdują się wskazówki dotyczące konfigurowania aplikacji umożliwiająca użycie dostawcy Redis wyjściowej pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="961f6-108">This topic provides guidance on configuring your application to use the Redis Output Cache Provider.</span></span> <span data-ttu-id="961f6-109">Aby uzyskać więcej informacji na temat tworzenia i konfigurowania wystąpienia pamięci podręcznej Redis Azure, zobacz [tworzenia pamięci podręcznej](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache).</span><span class="sxs-lookup"><span data-stu-id="961f6-109">For more information about creating and configuring an Azure Redis Cache instance, see [Create a cache](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache).</span></span>

## <a name="store-aspnet-page-output-in-the-cache"></a><span data-ttu-id="961f6-110">Przechowywanie w pamięci podręcznej danych wyjściowych strony ASP.NET</span><span class="sxs-lookup"><span data-stu-id="961f6-110">Store ASP.NET page output in the cache</span></span>
<span data-ttu-id="961f6-111">Kliknij, aby skonfigurować aplikację klienta w programie Visual Studio przy użyciu pakietu NuGet stanu sesji pamięci podręcznej Redis **Menedżera pakietów NuGet**, **Konsola Menedżera pakietów** z **narzędzia** menu.</span><span class="sxs-lookup"><span data-stu-id="961f6-111">To configure a client application in Visual Studio using the Redis Cache Session State NuGet package, click **NuGet Package Manager**, **Package Manager Console** from the **Tools** menu.</span></span>

<span data-ttu-id="961f6-112">W oknie `Package Manager Console` uruchom następujące polecenie.</span><span class="sxs-lookup"><span data-stu-id="961f6-112">Run the following command from the `Package Manager Console` window.</span></span>
    
```
Install-Package Microsoft.Web.RedisOutputCacheProvider
```

<span data-ttu-id="961f6-113">Pakiet NuGet dostawcy pamięci podręcznej danych wyjściowych Redis ma zależność od pakietu StackExchange.Redis.StrongName.</span><span class="sxs-lookup"><span data-stu-id="961f6-113">The Redis Output Cache Provider NuGet package has a dependency on the StackExchange.Redis.StrongName package.</span></span> <span data-ttu-id="961f6-114">Jeśli w projekcie nie ma pakietu StackExchange.Redis.StrongName, jest zainstalowana.</span><span class="sxs-lookup"><span data-stu-id="961f6-114">If the StackExchange.Redis.StrongName package is not present in your project, it is installed.</span></span> <span data-ttu-id="961f6-115">Aby uzyskać więcej informacji o pakiecie NuGet dostawcy Redis pamięci podręcznej danych wyjściowych, zobacz [RedisOutputCacheProvider](https://www.nuget.org/packages/Microsoft.Web.RedisOutputCacheProvider/) NuGet strony.</span><span class="sxs-lookup"><span data-stu-id="961f6-115">For more information about the Redis Output Cache Provider NuGet package, see the [RedisOutputCacheProvider](https://www.nuget.org/packages/Microsoft.Web.RedisOutputCacheProvider/) NuGet page.</span></span>

>[!NOTE]
><span data-ttu-id="961f6-116">Oprócz pakietu StackExchange.Redis.StrongName o silnych nazwach jest także wersja z systemem innym niż-o silnych nazwach programie StackExchange.Redis.</span><span class="sxs-lookup"><span data-stu-id="961f6-116">In addition to the strong-named StackExchange.Redis.StrongName package, there is also the StackExchange.Redis non-strong-named version.</span></span> <span data-ttu-id="961f6-117">Jeśli projekt korzysta z wersji programie StackExchange.Redis nie-o silnych nazwach, należy go odinstalować, w przeciwnym razie możesz pobrać konfliktów nazw w projekcie.</span><span class="sxs-lookup"><span data-stu-id="961f6-117">If your project is using the non-strong-named StackExchange.Redis version you must uninstall it, otherwise you get naming conflicts in your project.</span></span> <span data-ttu-id="961f6-118">Aby uzyskać więcej informacji na temat tych pakietów, zobacz [.NET Konfigurowanie klientów pamięci podręcznej](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients).</span><span class="sxs-lookup"><span data-stu-id="961f6-118">For more information about these packages, see [Configure .NET cache clients](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients).</span></span>
>
>

<span data-ttu-id="961f6-119">Pakiet NuGet pliki do pobrania i dodaje odwołania do wymaganych zestawów i dodaje następującą sekcję do pliku web.config.</span><span class="sxs-lookup"><span data-stu-id="961f6-119">The NuGet package downloads and adds the required assembly references and adds the following section into your web.config file.</span></span> <span data-ttu-id="961f6-120">Ta sekcja zawiera wymagana konfiguracja dla aplikacji ASP.NET do używania dostawcy Redis wyjściowej pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="961f6-120">This section contains the required configuration for your ASP.NET application to use the Redis Output Cache Provider.</span></span>

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

<span data-ttu-id="961f6-121">Komentarze sekcji przedstawiono przykład atrybutów i przykładowe ustawienia dla każdego atrybutu.</span><span class="sxs-lookup"><span data-stu-id="961f6-121">The commented section provides an example of the attributes and sample settings for each attribute.</span></span>

<span data-ttu-id="961f6-122">Skonfiguruj atrybuty wartościami z Twojej blok pamięci podręcznej w portalu Microsoft Azure oraz innych wartości zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="961f6-122">Configure the attributes with the values from your cache blade in the Microsoft Azure portal, and configure the other values as desired.</span></span> <span data-ttu-id="961f6-123">Aby uzyskać instrukcje dotyczące uzyskiwania dostępu do właściwości pamięci podręcznej, zobacz [Redis skonfigurować ustawienia pamięci podręcznej](cache-configure.md#configure-redis-cache-settings).</span><span class="sxs-lookup"><span data-stu-id="961f6-123">For instructions on accessing your cache properties, see [Configure Redis cache settings](cache-configure.md#configure-redis-cache-settings).</span></span>

* <span data-ttu-id="961f6-124">**host** — Określ punktu końcowego pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="961f6-124">**host** – specify your cache endpoint.</span></span>
* <span data-ttu-id="961f6-125">**port** — port bez protokołu SSL lub portem SSL, w zależności od ustawień protokołu ssl.</span><span class="sxs-lookup"><span data-stu-id="961f6-125">**port** – use either your non-SSL port or your SSL port, depending on the ssl settings.</span></span>
* <span data-ttu-id="961f6-126">**accessKey** — Użyj klucz podstawowy lub pomocniczy dla pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="961f6-126">**accessKey** – use either the primary or secondary key for your cache.</span></span>
* <span data-ttu-id="961f6-127">**Protokół SSL** — wartość true, jeśli chcesz zabezpieczyć komunikację pamięci podręcznej/klienta przy użyciu protokołu ssl; w przeciwnym razie wartość false.</span><span class="sxs-lookup"><span data-stu-id="961f6-127">**ssl** – true if you want to secure cache/client communications with ssl; otherwise false.</span></span> <span data-ttu-id="961f6-128">Należy określić właściwego portu.</span><span class="sxs-lookup"><span data-stu-id="961f6-128">Be sure to specify the correct port.</span></span>
  * <span data-ttu-id="961f6-129">Port bez obsługi protokołu SSL jest domyślnie wyłączony w przypadku nowych pamięci podręcznych.</span><span class="sxs-lookup"><span data-stu-id="961f6-129">The non-SSL port is disabled by default for new caches.</span></span> <span data-ttu-id="961f6-130">Określ wartość true dla tego ustawienia używał portu protokołu SSL.</span><span class="sxs-lookup"><span data-stu-id="961f6-130">Specify true for this setting to use the SSL port.</span></span> <span data-ttu-id="961f6-131">Aby uzyskać więcej informacji na temat włączania portu bez protokołu SSL, zobacz [porty dostępu](cache-configure.md#access-ports) sekcji [skonfigurować pamięć podręczną](cache-configure.md) tematu.</span><span class="sxs-lookup"><span data-stu-id="961f6-131">For more information about enabling the non-SSL port, see the [Access Ports](cache-configure.md#access-ports) section in the [Configure a cache](cache-configure.md) topic.</span></span>
* <span data-ttu-id="961f6-132">**databaseId** — określonej bazy danych do użycia na potrzeby pamięci podręcznej dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="961f6-132">**databaseId** – Specified which database to use for cache output data.</span></span> <span data-ttu-id="961f6-133">Jeśli nie zostanie określony, zostanie użyta domyślna wartość 0.</span><span class="sxs-lookup"><span data-stu-id="961f6-133">If not specified, the default value of 0 is used.</span></span>
* <span data-ttu-id="961f6-134">**applicationName** — klucze są przechowywane w pamięci podręcznej redis jako `<AppName>_<SessionId>_Data`.</span><span class="sxs-lookup"><span data-stu-id="961f6-134">**applicationName** – Keys are stored in redis as `<AppName>_<SessionId>_Data`.</span></span> <span data-ttu-id="961f6-135">Ten schemat nazewnictwa umożliwia wielu aplikacji do udostępniania tego samego klucza.</span><span class="sxs-lookup"><span data-stu-id="961f6-135">This naming scheme enables multiple applications to share the same key.</span></span> <span data-ttu-id="961f6-136">Ten parametr jest opcjonalny i jeśli nie zostanie określona wartość domyślna jest używany.</span><span class="sxs-lookup"><span data-stu-id="961f6-136">This parameter is optional and if you do not provide it a default value is used.</span></span>
* <span data-ttu-id="961f6-137">**connectionTimeoutInMilliseconds** — to ustawienie pozwala zastąpić ustawienie connectTimeout w programie StackExchange.Redis klienta.</span><span class="sxs-lookup"><span data-stu-id="961f6-137">**connectionTimeoutInMilliseconds** – This setting allows you to override the connectTimeout setting in the StackExchange.Redis client.</span></span> <span data-ttu-id="961f6-138">Jeśli nie zostanie określona, używane jest domyślne ustawienie connectTimeout 5000.</span><span class="sxs-lookup"><span data-stu-id="961f6-138">If not specified, the default connectTimeout setting of 5000 is used.</span></span> <span data-ttu-id="961f6-139">Aby uzyskać więcej informacji, zobacz [model konfiguracji w programie StackExchange.Redis](http://go.microsoft.com/fwlink/?LinkId=398705).</span><span class="sxs-lookup"><span data-stu-id="961f6-139">For more information, see [StackExchange.Redis configuration model](http://go.microsoft.com/fwlink/?LinkId=398705).</span></span>
* <span data-ttu-id="961f6-140">**operationTimeoutInMilliseconds** — to ustawienie pozwala zastąpić ustawienie syncTimeout w programie StackExchange.Redis klienta.</span><span class="sxs-lookup"><span data-stu-id="961f6-140">**operationTimeoutInMilliseconds** – This setting allows you to override the syncTimeout setting in the StackExchange.Redis client.</span></span> <span data-ttu-id="961f6-141">Jeśli nie zostanie określona, używane jest domyślne ustawienie syncTimeout 1000.</span><span class="sxs-lookup"><span data-stu-id="961f6-141">If not specified, the default syncTimeout setting of 1000 is used.</span></span> <span data-ttu-id="961f6-142">Aby uzyskać więcej informacji, zobacz [model konfiguracji w programie StackExchange.Redis](http://go.microsoft.com/fwlink/?LinkId=398705).</span><span class="sxs-lookup"><span data-stu-id="961f6-142">For more information, see [StackExchange.Redis configuration model](http://go.microsoft.com/fwlink/?LinkId=398705).</span></span>

<span data-ttu-id="961f6-143">Dodaj dyrektywy OutputCache na każdej stronie, dla którego chcesz pamięci podręcznej danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="961f6-143">Add an OutputCache directive to each page for which you wish to cache the output.</span></span>

```
<%@ OutputCache Duration="60" VaryByParam="*" %>
```

<span data-ttu-id="961f6-144">W poprzednim przykładzie dane buforowane strony pozostaje w pamięci podręcznej przez 60 sekund i inną wersję strony są buforowane dla każdej kombinacji parametrów.</span><span class="sxs-lookup"><span data-stu-id="961f6-144">In the previous example, the cached page data remains in the cache for 60 seconds, and a different version of the page is cached for each parameter combination.</span></span> <span data-ttu-id="961f6-145">Aby uzyskać więcej informacji na temat dyrektywie OutputCache zobacz [ @OutputCache ](http://go.microsoft.com/fwlink/?linkid=320837).</span><span class="sxs-lookup"><span data-stu-id="961f6-145">For more information about the OutputCache directive, see [@OutputCache](http://go.microsoft.com/fwlink/?linkid=320837).</span></span>

<span data-ttu-id="961f6-146">Gdy te kroki są wykonywane, aplikacja jest skonfigurowana do używania dostawcy Redis wyjściowej pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="961f6-146">Once these steps are performed, your application is configured to use the Redis Output Cache Provider.</span></span>

## <a name="next-steps"></a><span data-ttu-id="961f6-147">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="961f6-147">Next steps</span></span>
<span data-ttu-id="961f6-148">Zapoznaj się z [dostawcę stanu sesji ASP.NET dla pamięci podręcznej Redis Azure](cache-aspnet-session-state-provider.md).</span><span class="sxs-lookup"><span data-stu-id="961f6-148">Check out the [ASP.NET Session State Provider for Azure Redis Cache](cache-aspnet-session-state-provider.md).</span></span>

