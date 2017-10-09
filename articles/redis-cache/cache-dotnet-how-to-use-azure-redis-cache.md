---
title: "tooUse aaaHow pamięć podręczna Redis Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooimprove hello wydajności aplikacji platformy Azure z pamięcią podręczną Redis Azure"
services: redis-cache,app-service
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: c502f74c-44de-4087-8303-1b1f43da12d5
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 07/27/2017
ms.author: sdanie
ms.openlocfilehash: 763d70c10972eec9a1885969e8da5bf1c4084727
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-redis-cache"></a><span data-ttu-id="86a87-103">Jak tooUse Azure pamięci podręcznej Redis</span><span class="sxs-lookup"><span data-stu-id="86a87-103">How tooUse Azure Redis Cache</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="86a87-104">.NET</span><span class="sxs-lookup"><span data-stu-id="86a87-104">.NET</span></span>](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [<span data-ttu-id="86a87-105">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="86a87-105">ASP.NET</span></span>](cache-web-app-howto.md)
> * [<span data-ttu-id="86a87-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="86a87-106">Node.js</span></span>](cache-nodejs-get-started.md)
> * [<span data-ttu-id="86a87-107">Java</span><span class="sxs-lookup"><span data-stu-id="86a87-107">Java</span></span>](cache-java-get-started.md)
> * [<span data-ttu-id="86a87-108">Python</span><span class="sxs-lookup"><span data-stu-id="86a87-108">Python</span></span>](cache-python-get-started.md)
> 
> 

<span data-ttu-id="86a87-109">W tym przewodniku przedstawiono sposób tooget uruchamiania przy użyciu **pamięć podręczna Redis Azure**.</span><span class="sxs-lookup"><span data-stu-id="86a87-109">This guide shows you how tooget started using **Azure Redis Cache**.</span></span> <span data-ttu-id="86a87-110">Pamięć podręczna Redis Azure firmy Microsoft jest oparta na powitania popularnych typu open source pamięci podręcznej Redis.</span><span class="sxs-lookup"><span data-stu-id="86a87-110">Microsoft Azure Redis Cache is based on hello popular open source Redis Cache.</span></span> <span data-ttu-id="86a87-111">Daje dostęp do tooa bezpiecznego, dedykowane pamięć podręczna Redis, zarządzany przez firmę Microsoft.</span><span class="sxs-lookup"><span data-stu-id="86a87-111">It gives you access tooa secure, dedicated Redis cache, managed by Microsoft.</span></span> <span data-ttu-id="86a87-112">Pamięć podręczna utworzona przy użyciu usługi Azure Redis Cache jest dostępna z poziomu dowolnej aplikacji w ramach platformy Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="86a87-112">A cache created using Azure Redis Cache is accessible from any application within Microsoft Azure.</span></span>

<span data-ttu-id="86a87-113">Pamięć podręczna Redis Azure firmy Microsoft jest dostępna w hello następujące warstwy:</span><span class="sxs-lookup"><span data-stu-id="86a87-113">Microsoft Azure Redis Cache is available in hello following tiers:</span></span>

* <span data-ttu-id="86a87-114">**Podstawowa** — jeden węzeł.</span><span class="sxs-lookup"><span data-stu-id="86a87-114">**Basic** – Single node.</span></span> <span data-ttu-id="86a87-115">Wiele wielkości too53 GB.</span><span class="sxs-lookup"><span data-stu-id="86a87-115">Multiple sizes up too53 GB.</span></span>
* <span data-ttu-id="86a87-116">**Standardowa** — dwa węzły (węzeł podstawowy i węzeł repliki).</span><span class="sxs-lookup"><span data-stu-id="86a87-116">**Standard** – Two-node Primary/Replica.</span></span> <span data-ttu-id="86a87-117">Wiele wielkości too53 GB.</span><span class="sxs-lookup"><span data-stu-id="86a87-117">Multiple sizes up too53 GB.</span></span> <span data-ttu-id="86a87-118">Umowa SLA na poziomie 99,9%.</span><span class="sxs-lookup"><span data-stu-id="86a87-118">99.9% SLA.</span></span>
* <span data-ttu-id="86a87-119">**Premium** — dwa węzły podstawowego/repliki o zapasowej odłamków too10.</span><span class="sxs-lookup"><span data-stu-id="86a87-119">**Premium** – Two-node Primary/Replica with up too10 shards.</span></span> <span data-ttu-id="86a87-120">Różne rozmiary od 6 GB too530 GB.</span><span class="sxs-lookup"><span data-stu-id="86a87-120">Multiple sizes from 6 GB too530 GB.</span></span> <span data-ttu-id="86a87-121">Wszystkie funkcje warstwy Standardowej i dodatkowe funkcje, m.in. obsługa [klastra Redis](cache-how-to-premium-clustering.md), [stanu trwałego pamięci podręcznej Redis](cache-how-to-premium-persistence.md) oraz usługi [Azure Virtual Network](cache-how-to-premium-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="86a87-121">All Standard tier features and more including support for [Redis cluster](cache-how-to-premium-clustering.md), [Redis persistence](cache-how-to-premium-persistence.md), and [Azure Virtual Network](cache-how-to-premium-vnet.md).</span></span> <span data-ttu-id="86a87-122">Umowa SLA na poziomie 99,9%.</span><span class="sxs-lookup"><span data-stu-id="86a87-122">99.9% SLA.</span></span>

<span data-ttu-id="86a87-123">Poszczególne warstwy różnią się od siebie pod względem funkcji i cen.</span><span class="sxs-lookup"><span data-stu-id="86a87-123">Each tier differs in terms of features and pricing.</span></span> <span data-ttu-id="86a87-124">Informacje dotyczące cen można znaleźć w artykule [Pamięć podręczna Redis — cennik][Cache Pricing Details].</span><span class="sxs-lookup"><span data-stu-id="86a87-124">For information on pricing, see [Cache Pricing Details][Cache Pricing Details].</span></span>

<span data-ttu-id="86a87-125">W tym przewodniku przedstawiono sposób toouse hello [programie StackExchange.Redis] [ StackExchange.Redis] klienta przy użyciu C\# kodu.</span><span class="sxs-lookup"><span data-stu-id="86a87-125">This guide shows you how toouse hello [StackExchange.Redis][StackExchange.Redis] client using C\# code.</span></span> <span data-ttu-id="86a87-126">Witaj omówione scenariusze obejmują **tworzenie i konfigurowanie pamięci podręcznej**, **Konfigurowanie klientów pamięci podręcznej**, i **Dodawanie i usuwanie obiektów z pamięci podręcznej hello**.</span><span class="sxs-lookup"><span data-stu-id="86a87-126">hello scenarios covered include **creating and configuring a cache**, **configuring cache clients**, and **adding and removing objects from hello cache**.</span></span> <span data-ttu-id="86a87-127">Aby uzyskać więcej informacji na temat korzystania z usługi Azure Redis Cache, zobacz [Następne kroki][Next Steps].</span><span class="sxs-lookup"><span data-stu-id="86a87-127">For more information on using Azure Redis Cache, see [Next Steps][Next Steps].</span></span> <span data-ttu-id="86a87-128">Krok po kroku samouczek tworzenia aplikacji sieci web z pamięci podręcznej Redis ASP.NET MVC, zobacz [jak toocreate aplikacji sieci Web z pamięci podręcznej Redis](cache-web-app-howto.md).</span><span class="sxs-lookup"><span data-stu-id="86a87-128">For a step-by-step tutorial of building an ASP.NET MVC web app with Redis Cache, see [How toocreate a Web App with Redis Cache](cache-web-app-howto.md).</span></span>

<a name="getting-started-cache-service"></a>

## <a name="get-started-with-azure-redis-cache"></a><span data-ttu-id="86a87-129">Rozpoczęcie pracy z usługą Azure Redis Cache</span><span class="sxs-lookup"><span data-stu-id="86a87-129">Get Started with Azure Redis Cache</span></span>
<span data-ttu-id="86a87-130">Rozpoczęcie pracy z usługą Azure Redis Cache jest proste.</span><span class="sxs-lookup"><span data-stu-id="86a87-130">Getting started with Azure Redis Cache is easy.</span></span> <span data-ttu-id="86a87-131">tooget pracę, należy udostępnić i skonfigurować pamięć podręczną.</span><span class="sxs-lookup"><span data-stu-id="86a87-131">tooget started, you provision and configure a cache.</span></span> <span data-ttu-id="86a87-132">Następnie należy skonfigurować klientów pamięci podręcznej hello, więc mogą uzyskiwać dostęp do pamięci podręcznej hello.</span><span class="sxs-lookup"><span data-stu-id="86a87-132">Next, you configure hello cache clients so they can access hello cache.</span></span> <span data-ttu-id="86a87-133">Po skonfigurowaniu hello pamięci podręcznej klientów, można rozpocząć pracę z nimi.</span><span class="sxs-lookup"><span data-stu-id="86a87-133">Once hello cache clients are configured, you can begin working with them.</span></span>

* <span data-ttu-id="86a87-134">[Tworzenie pamięci podręcznej hello][Create hello cache]</span><span class="sxs-lookup"><span data-stu-id="86a87-134">[Create hello cache][Create hello cache]</span></span>
* <span data-ttu-id="86a87-135">[Konfigurowanie klientów pamięci podręcznej hello][Configure hello cache clients]</span><span class="sxs-lookup"><span data-stu-id="86a87-135">[Configure hello cache clients][Configure hello cache clients]</span></span>

<a name="create-cache"></a>

## <a name="create-a-cache"></a><span data-ttu-id="86a87-136">Tworzenie pamięci podręcznej</span><span class="sxs-lookup"><span data-stu-id="86a87-136">Create a cache</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

### <a name="tooaccess-your-cache-after-its-created"></a><span data-ttu-id="86a87-137">tooaccess pamięć podręczną po jego utworzeniu</span><span class="sxs-lookup"><span data-stu-id="86a87-137">tooaccess your cache after it's created</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-browse.md)]

<span data-ttu-id="86a87-138">Aby uzyskać więcej informacji o konfigurowaniu pamięci podręcznej, zobacz [jak tooconfigure pamięć podręczna Redis Azure](cache-configure.md).</span><span class="sxs-lookup"><span data-stu-id="86a87-138">For more information about configuring your cache, see [How tooconfigure Azure Redis Cache](cache-configure.md).</span></span>

<a name="NuGet"></a>

## <a name="configure-hello-cache-clients"></a><span data-ttu-id="86a87-139">Konfigurowanie klientów pamięci podręcznej hello</span><span class="sxs-lookup"><span data-stu-id="86a87-139">Configure hello cache clients</span></span>
[!INCLUDE [redis-cache-configure](../../includes/redis-cache-configure-stackexchange-redis-nuget.md)]

<span data-ttu-id="86a87-140">Gdy projekt klienta zostanie skonfigurowany do buforowania, można użyć hello metod opisanych w hello następujące sekcje zawierają informacje dotyczące pracy z pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="86a87-140">Once your client project is configured for caching, you can use hello techniques described in hello following sections for working with your cache.</span></span>

<a name="working-with-caches"></a>

## <a name="working-with-caches"></a><span data-ttu-id="86a87-141">Praca z pamięciami podręcznymi</span><span class="sxs-lookup"><span data-stu-id="86a87-141">Working with Caches</span></span>
<span data-ttu-id="86a87-142">Witaj w tej sekcji opisano sposób tooperform typowe zadania z pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="86a87-142">hello steps in this section describe how tooperform common tasks with Cache.</span></span>

* <span data-ttu-id="86a87-143">[Połącz toohello pamięci podręcznej][Connect toohello cache]</span><span class="sxs-lookup"><span data-stu-id="86a87-143">[Connect toohello cache][Connect toohello cache]</span></span>
* <span data-ttu-id="86a87-144">[Dodaj i pobrać z pamięci podręcznej hello obiektów][Add and retrieve objects from hello cache]</span><span class="sxs-lookup"><span data-stu-id="86a87-144">[Add and retrieve objects from hello cache][Add and retrieve objects from hello cache]</span></span>
* [<span data-ttu-id="86a87-145">Praca z obiektami .NET w pamięci podręcznej hello</span><span class="sxs-lookup"><span data-stu-id="86a87-145">Work with .NET objects in hello cache</span></span>](#work-with-net-objects-in-the-cache)

<a name="connect-to-cache"></a>

## <a name="connect-toohello-cache"></a><span data-ttu-id="86a87-146">Połącz toohello pamięci podręcznej</span><span class="sxs-lookup"><span data-stu-id="86a87-146">Connect toohello cache</span></span>
<span data-ttu-id="86a87-147">tooprogrammatically pracy z pamięci podręcznej, należy buforu toohello odwołań.</span><span class="sxs-lookup"><span data-stu-id="86a87-147">tooprogrammatically work with a cache, you need a reference toohello cache.</span></span> <span data-ttu-id="86a87-148">Dodaj powitania od góry toohello dla dowolnego pliku, z którego chcesz toouse hello programie StackExchange.Redis klienta tooaccess pamięć podręczna Redis Azure.</span><span class="sxs-lookup"><span data-stu-id="86a87-148">Add hello following toohello top of any file from which you want toouse hello StackExchange.Redis client tooaccess an Azure Redis Cache.</span></span>

    using StackExchange.Redis;

> [!NOTE]
> <span data-ttu-id="86a87-149">Witaj programie StackExchange.Redis klienta wymaga programu .NET Framework 4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="86a87-149">hello StackExchange.Redis client requires .NET Framework 4 or higher.</span></span>
> 
> 

<span data-ttu-id="86a87-150">Witaj toohello połączenia z pamięcią podręczną Redis Azure jest zarządzana przez hello `ConnectionMultiplexer` klasy.</span><span class="sxs-lookup"><span data-stu-id="86a87-150">hello connection toohello Azure Redis Cache is managed by hello `ConnectionMultiplexer` class.</span></span> <span data-ttu-id="86a87-151">Ta klasa powinny być udostępniane i użyć ponownie w całej aplikacji klienckiej i nie musi toobe utworzone na podstawie na operację.</span><span class="sxs-lookup"><span data-stu-id="86a87-151">This class should be shared and reused throughout your client application, and does not need toobe created on a per operation basis.</span></span> 

<span data-ttu-id="86a87-152">tooan tooconnect pamięć podręczna Redis Azure i można zwrócić wystąpienia połączonych `ConnectionMultiplexer`, wywołanie hello statycznych `Connect` — metoda i przekaż hello pamięci podręcznej punktu końcowego i klucz.</span><span class="sxs-lookup"><span data-stu-id="86a87-152">tooconnect tooan Azure Redis Cache and be returned an instance of a connected `ConnectionMultiplexer`, call hello static `Connect` method and pass in hello cache endpoint and key.</span></span> <span data-ttu-id="86a87-153">Za pomocą klawisza hello wygenerowane z portalu Azure jako parametr password hello hello.</span><span class="sxs-lookup"><span data-stu-id="86a87-153">Use hello key generated from hello Azure portal as hello password parameter.</span></span>

    ConnectionMultiplexer connection = ConnectionMultiplexer.Connect("contoso5.redis.cache.windows.net,abortConnect=false,ssl=true,password=...");

> [!IMPORTANT]
> <span data-ttu-id="86a87-154">Ostrzeżenie: Nigdy nie przechowuj poświadczeń w kodzie źródłowym.</span><span class="sxs-lookup"><span data-stu-id="86a87-154">Warning: Never store credentials in source code.</span></span> <span data-ttu-id="86a87-155">tookeep to prosty przykład I używam wyświetlania ich w kodzie źródłowym hello.</span><span class="sxs-lookup"><span data-stu-id="86a87-155">tookeep this sample simple, I’m showing them in hello source code.</span></span> <span data-ttu-id="86a87-156">Zobacz [jak ciągi aplikacji i pracy ciągów połączenia] [ How Application Strings and Connection Strings Work] informacji na temat toostore poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="86a87-156">See [How Application Strings and Connection Strings Work][How Application Strings and Connection Strings Work] for information on how toostore credentials.</span></span>
> 
> 

<span data-ttu-id="86a87-157">Jeśli nie chcesz toouse SSL, albo ustaw `ssl=false` lub Pomiń hello `ssl` parametru.</span><span class="sxs-lookup"><span data-stu-id="86a87-157">If you don't want toouse SSL, either set `ssl=false` or omit hello `ssl` parameter.</span></span>

> [!NOTE]
> <span data-ttu-id="86a87-158">port bez protokołu SSL Hello jest domyślnie wyłączona, dla nowych pamięci podręcznych.</span><span class="sxs-lookup"><span data-stu-id="86a87-158">hello non-SSL port is disabled by default for new caches.</span></span> <span data-ttu-id="86a87-159">Aby uzyskać instrukcje na temat włączania portu bez protokołu SSL hello, zobacz [porty dostępu](cache-configure.md#access-ports).</span><span class="sxs-lookup"><span data-stu-id="86a87-159">For instructions on enabling hello non-SSL port, see [Access Ports](cache-configure.md#access-ports).</span></span>
> 
> 

<span data-ttu-id="86a87-160">Jednym z podejść toosharing `ConnectionMultiplexer` toohave statycznej właściwości, która zwraca wystąpienie połączonych toohello podobnie poniższy przykład jest wystąpienie w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="86a87-160">One approach toosharing a `ConnectionMultiplexer` instance in your application is toohave a static property that returns a connected instance, similar toohello following example.</span></span> <span data-ttu-id="86a87-161">Metoda ta umożliwia tooinitialize sposób zapewniający obsługę wielowątkowości, tylko jeden połączony `ConnectionMultiplexer` wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="86a87-161">This approach provides a thread-safe way tooinitialize only a single connected `ConnectionMultiplexer` instance.</span></span> <span data-ttu-id="86a87-162">W tych przykładach `abortConnect` jest zestaw toofalse, co oznacza, nawet jeśli nie zostanie nawiązane połączenie toohello pamięć podręczna Redis Azure powiedzie się hello wywołania.</span><span class="sxs-lookup"><span data-stu-id="86a87-162">In these examples `abortConnect` is set toofalse, which means that hello call succeeds even if a connection toohello Azure Redis Cache is not established.</span></span> <span data-ttu-id="86a87-163">Jedna funkcja klucza `ConnectionMultiplexer` jest on automatycznie przywraca łączności toohello w pamięci podręcznej po hello problem z siecią lub inne przyczyny zostaną rozwiązane.</span><span class="sxs-lookup"><span data-stu-id="86a87-163">One key feature of `ConnectionMultiplexer` is that it automatically restores connectivity toohello cache once hello network issue or other causes are resolved.</span></span>

    private static Lazy<ConnectionMultiplexer> lazyConnection = new Lazy<ConnectionMultiplexer>(() =>
    {
        return ConnectionMultiplexer.Connect("contoso5.redis.cache.windows.net,abortConnect=false,ssl=true,password=...");
    });

    public static ConnectionMultiplexer Connection
    {
        get
        {
            return lazyConnection.Value;
        }
    }

<span data-ttu-id="86a87-164">Więcej informacji na temat opcji zaawansowanej konfiguracji połączenia znajduje się w opisie [modelu konfiguracji StackExchange.Redis][StackExchange.Redis configuration model].</span><span class="sxs-lookup"><span data-stu-id="86a87-164">For more information on advanced connection configuration options, see [StackExchange.Redis configuration model][StackExchange.Redis configuration model].</span></span>

[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

<span data-ttu-id="86a87-165">Po nawiązaniu połączenia hello zwrócić bazy danych pamięci podręcznej redis toohello odwołania przez wywołanie hello `ConnectionMultiplexer.GetDatabase` metody.</span><span class="sxs-lookup"><span data-stu-id="86a87-165">Once hello connection is established, return a reference toohello redis cache database by calling hello `ConnectionMultiplexer.GetDatabase` method.</span></span> <span data-ttu-id="86a87-166">zwróciła obiekt Hello hello `GetDatabase` metody jest obiektem przekazujące lekkie i nie wymaga toobe przechowywane.</span><span class="sxs-lookup"><span data-stu-id="86a87-166">hello object returned from hello `GetDatabase` method is a lightweight pass-through object and does not need toobe stored.</span></span>

    // Connection refers tooa property that returns a ConnectionMultiplexer
    // as shown in hello previous example.
    IDatabase cache = Connection.GetDatabase();

    // Perform cache operations using hello cache object...
    // Simple put of integral data types into hello cache
    cache.StringSet("key1", "value");
    cache.StringSet("key2", 25);

    // Simple get of data types from hello cache
    string key1 = cache.StringGet("key1");
    int key2 = (int)cache.StringGet("key2");

<span data-ttu-id="86a87-167">Pamięci podręcznej pamięci podręcznej Redis Azure mają można skonfigurować liczbę baz danych (domyślnie 16), które mogą być używane toologically oddzielne hello danych w pamięci podręcznej Redis.</span><span class="sxs-lookup"><span data-stu-id="86a87-167">Azure Redis caches have a configurable number of databases (default of 16) that can be used toologically separate hello data within a Redis cache.</span></span> <span data-ttu-id="86a87-168">Aby uzyskać więcej informacji, zobacz [What are Redis databases?](cache-faq.md#what-are-redis-databases) (Co to są bazy danych Redis?) i [Default Redis server configuration](cache-configure.md#default-redis-server-configuration) (Domyślna konfiguracja serwera Redis).</span><span class="sxs-lookup"><span data-stu-id="86a87-168">For more information, see [What are Redis databases?](cache-faq.md#what-are-redis-databases) and [Default Redis server configuration](cache-configure.md#default-redis-server-configuration).</span></span>

<span data-ttu-id="86a87-169">Teraz, gdy wiesz, jak wystąpienia pamięci podręcznej Redis Azure tooan tooconnect i przywracać toohello odwołania pamięci podręcznej bazy danych, Przyjrzyjmy się pracy z pamięci podręcznej hello.</span><span class="sxs-lookup"><span data-stu-id="86a87-169">Now that you know how tooconnect tooan Azure Redis Cache instance and return a reference toohello cache database, let's look at working with hello cache.</span></span>

<a name="add-object"></a>

## <a name="add-and-retrieve-objects-from-hello-cache"></a><span data-ttu-id="86a87-170">Dodaj i pobrać z pamięci podręcznej hello obiektów</span><span class="sxs-lookup"><span data-stu-id="86a87-170">Add and retrieve objects from hello cache</span></span>
<span data-ttu-id="86a87-171">Elementy można przechowywane w i pobierane z pamięci podręcznej za pomocą hello `StringSet` i `StringGet` metody.</span><span class="sxs-lookup"><span data-stu-id="86a87-171">Items can be stored in and retrieved from a cache by using hello `StringSet` and `StringGet` methods.</span></span>

    // If key1 exists, it is overwritten.
    cache.StringSet("key1", "value1");

    string value = cache.StringGet("key1");

<span data-ttu-id="86a87-172">W pamięci podręcznej redis, większość danych jako ciągi Redis, ale te ciągi mogą zawierać wiele typów danych, w tym serializacji danych binarnych, którego można użyć w przypadku przechowywania .NET obiektów w pamięci podręcznej hello magazynów.</span><span class="sxs-lookup"><span data-stu-id="86a87-172">Redis stores most data as Redis strings, but these strings can contain many types of data, including serialized binary data, which can be used when storing .NET objects in hello cache.</span></span>

<span data-ttu-id="86a87-173">Podczas wywoływania metody `StringGet`, jeśli obiekt hello istnieje, jest zwracany, a jeśli nie, `null` jest zwracany.</span><span class="sxs-lookup"><span data-stu-id="86a87-173">When calling `StringGet`, if hello object exists, it is returned, and if it does not, `null` is returned.</span></span> <span data-ttu-id="86a87-174">Jeśli `null` jest zwracany, można pobrać wartości hello ze źródła danych odpowiednie hello i zapisz go w pamięci podręcznej hello na potrzeby późniejszego wykorzystania.</span><span class="sxs-lookup"><span data-stu-id="86a87-174">If `null` is returned, you can retrieve hello value from hello desired data source and store it in hello cache for subsequent use.</span></span> <span data-ttu-id="86a87-175">Ten wzorzec użycia jest określany jako hello Zarezerwuj pamięć podręczna wzorzec.</span><span class="sxs-lookup"><span data-stu-id="86a87-175">This usage pattern is known as hello cache-aside pattern.</span></span>

    string value = cache.StringGet("key1");
    if (value == null)
    {
        // hello item keyed by "key1" is not in hello cache. Obtain
        // it from hello desired data source and add it toohello cache.
        value = GetValueFromDataSource();

        cache.StringSet("key1", value);
    }

<span data-ttu-id="86a87-176">Można również użyć `RedisValue`, jak pokazano w hello poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="86a87-176">You can also use `RedisValue`, as shown in hello following example.</span></span> <span data-ttu-id="86a87-177">Typ `RedisValue` ma niejawne operatory do pracy z integralnymi typami danych. To rozwiązanie może być użyteczne, jeśli oczekiwaną wartością dla elementu w pamięci podręcznej jest `null`.</span><span class="sxs-lookup"><span data-stu-id="86a87-177">`RedisValue` has implicit operators for working with integral data types, and can be useful if `null` is an expected value for a cached item.</span></span>


    RedisValue value = cache.StringGet("key1");
    if (!value.HasValue)
    {
        value = GetValueFromDataSource();
        cache.StringSet("key1", value);
    }


<span data-ttu-id="86a87-178">wygaśnięcie hello toospecify elementu w pamięci podręcznej hello, użyj hello `TimeSpan` parametr `StringSet`.</span><span class="sxs-lookup"><span data-stu-id="86a87-178">toospecify hello expiration of an item in hello cache, use hello `TimeSpan` parameter of `StringSet`.</span></span>

    cache.StringSet("key1", "value1", TimeSpan.FromMinutes(90));

## <a name="work-with-net-objects-in-hello-cache"></a><span data-ttu-id="86a87-179">Praca z obiektami .NET w pamięci podręcznej hello</span><span class="sxs-lookup"><span data-stu-id="86a87-179">Work with .NET objects in hello cache</span></span>
<span data-ttu-id="86a87-180">Usługa Azure Redis Cache może buforować obiekty platformy .NET oraz pierwotne typy danych, ale zanim będzie możliwe buforowanie obiektu platformy .NET, trzeba go serializować.</span><span class="sxs-lookup"><span data-stu-id="86a87-180">Azure Redis Cache can cache both .NET objects and primitive data types, but before a .NET object can be cached it must be serialized.</span></span> <span data-ttu-id="86a87-181">Serializację obiektu .NET jest odpowiedzialny za hello Deweloper aplikacji hello i zapewnia elastyczność developer hello hello wyborze hello serializatora.</span><span class="sxs-lookup"><span data-stu-id="86a87-181">This .NET object serialization is hello responsibility of hello application developer, and gives hello developer flexibility in hello choice of hello serializer.</span></span>

<span data-ttu-id="86a87-182">Jeden tooserialize prosty sposób obiektów jest toouse hello `JsonConvert` metody serializacji w [Newtonsoft.Json.NET](https://www.nuget.org/packages/Newtonsoft.Json/8.0.1-beta1) i serializacji tooand z formatu JSON.</span><span class="sxs-lookup"><span data-stu-id="86a87-182">One simple way tooserialize objects is toouse hello `JsonConvert` serialization methods in [Newtonsoft.Json.NET](https://www.nuget.org/packages/Newtonsoft.Json/8.0.1-beta1) and serialize tooand from JSON.</span></span> <span data-ttu-id="86a87-183">Witaj poniższy przykład przedstawia get i set z `Employee` wystąpienie obiektu.</span><span class="sxs-lookup"><span data-stu-id="86a87-183">hello following example shows a get and set using an `Employee` object instance.</span></span>

    class Employee
    {
        public int Id { get; set; }
        public string Name { get; set; }

        public Employee(int EmployeeId, string Name)
        {
            this.Id = EmployeeId;
            this.Name = Name;
        }
    }

    // Store toocache
    cache.StringSet("e25", JsonConvert.SerializeObject(new Employee(25, "Clayton Gragg")));

    // Retrieve from cache
    Employee e25 = JsonConvert.DeserializeObject<Employee>(cache.StringGet("e25"));

<a name="next-steps"></a>

## <a name="next-steps"></a><span data-ttu-id="86a87-184">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="86a87-184">Next Steps</span></span>
<span data-ttu-id="86a87-185">Teraz, kiedy znasz już podstawy hello, należy wykonać te dodatkowe informacje o pamięci podręcznej Redis Azure toolearn łącza.</span><span class="sxs-lookup"><span data-stu-id="86a87-185">Now that you've learned hello basics, follow these links toolearn more about Azure Redis Cache.</span></span>

* <span data-ttu-id="86a87-186">Zapoznaj się z hello dostawcy platformy ASP.NET dla pamięci podręcznej Redis Azure.</span><span class="sxs-lookup"><span data-stu-id="86a87-186">Check out hello ASP.NET providers for Azure Redis Cache.</span></span>
  * [<span data-ttu-id="86a87-187">Dostawca stanu sesji usługi Azure Redis</span><span class="sxs-lookup"><span data-stu-id="86a87-187">Azure Redis Session State Provider</span></span>](cache-aspnet-session-state-provider.md)
  * [<span data-ttu-id="86a87-188">Dostawca wyjściowej pamięci podręcznej programu ASP.NET w usłudze Azure Redis Cache</span><span class="sxs-lookup"><span data-stu-id="86a87-188">Azure Redis Cache ASP.NET Output Cache Provider</span></span>](cache-aspnet-output-cache-provider.md)
* <span data-ttu-id="86a87-189">[Włącz diagnostykę w pamięci podręcznej](cache-how-to-monitor.md#enable-cache-diagnostics) można więc [monitor](cache-how-to-monitor.md) hello kondycji pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="86a87-189">[Enable cache diagnostics](cache-how-to-monitor.md#enable-cache-diagnostics) so you can [monitor](cache-how-to-monitor.md) hello health of your cache.</span></span> <span data-ttu-id="86a87-190">Możesz wyświetlić hello metryki w hello portalu Azure i może również [pobrać i przejrzyj](https://github.com/rustd/RedisSamples/tree/master/CustomMonitoring) je za pomocą narzędzi hello wybranych przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="86a87-190">You can view hello metrics in hello Azure portal and you can also [download and review](https://github.com/rustd/RedisSamples/tree/master/CustomMonitoring) them using hello tools of your choice.</span></span>
* <span data-ttu-id="86a87-191">Zapoznaj się z hello [programie StackExchange.Redis pamięci podręcznej klienta dokumentacji][StackExchange.Redis cache client documentation].</span><span class="sxs-lookup"><span data-stu-id="86a87-191">Check out hello [StackExchange.Redis cache client documentation][StackExchange.Redis cache client documentation].</span></span>
  * <span data-ttu-id="86a87-192">Dostęp do usługi Azure Redis Cache można uzyskać z wielu klientów Redis i przy użyciu wielu języków programowania.</span><span class="sxs-lookup"><span data-stu-id="86a87-192">Azure Redis Cache can be accessed from many Redis clients and development languages.</span></span> <span data-ttu-id="86a87-193">Więcej informacji znajduje się na stronie [http://redis.io/clients][http://redis.io/clients].</span><span class="sxs-lookup"><span data-stu-id="86a87-193">For more information, see [http://redis.io/clients][http://redis.io/clients].</span></span>
* <span data-ttu-id="86a87-194">Usługi Azure Redis Cache można również używać z usługami i narzędziami innych firm, takimi jak Redsmin i Redis Desktop Manager.</span><span class="sxs-lookup"><span data-stu-id="86a87-194">Azure Redis Cache can also be used with third-party services and tools such as Redsmin and Redis Desktop Manager.</span></span>
  * <span data-ttu-id="86a87-195">Aby uzyskać więcej informacji o Redsmin, zobacz [jak tooretrieve połączenia Azure Redis ciąg i korzystania z niego Redsmin][How tooretrieve an Azure Redis connection string and use it with Redsmin].</span><span class="sxs-lookup"><span data-stu-id="86a87-195">For more information about Redsmin, see [How tooretrieve an Azure Redis connection string and use it with Redsmin][How tooretrieve an Azure Redis connection string and use it with Redsmin].</span></span>
  * <span data-ttu-id="86a87-196">Dostęp do danych w usłudze Azure Redis Cache oraz możliwość ich inspekcji można uzyskać za pomocą graficznego interfejsu użytkownika, używając usługi [RedisDesktopManager](https://github.com/uglide/RedisDesktopManager).</span><span class="sxs-lookup"><span data-stu-id="86a87-196">Access and inspect your data in Azure Redis Cache with a GUI using [RedisDesktopManager](https://github.com/uglide/RedisDesktopManager).</span></span>
* <span data-ttu-id="86a87-197">Zobacz hello [redis] [ redis] dokumentacji i przeczytaj temat [redis typy danych] [ redis data types] i [wprowadzenie piętnastu minut typy danych tooRedis][a fifteen minute introduction tooRedis data types].</span><span class="sxs-lookup"><span data-stu-id="86a87-197">See hello [redis][redis] documentation and read about [redis data types][redis data types] and [a fifteen minute introduction tooRedis data types][a fifteen minute introduction tooRedis data types].</span></span>

<!-- INTRA-TOPIC LINKS -->
[Next Steps]: #next-steps
[Introduction tooAzure Redis Cache (Video)]: #video
[What is Azure Redis Cache?]: #what-is
[Create an Azure Cache]: #create-cache
[Which type of caching is right for me?]: #choosing-cache
[Prepare Your Visual Studio Project tooUse Azure Caching]: #prepare-vs
[Configure Your Application tooUse Caching]: #configure-app
[Get Started with Azure Redis Cache]: #getting-started-cache-service
[Create hello cache]: #create-cache
[Configure hello cache]: #enable-caching
[Configure hello cache clients]: #NuGet
[Working with Caches]: #working-with-caches
[Connect toohello cache]: #connect-to-cache
[Add and retrieve objects from hello cache]: #add-object
[Specify hello expiration of an object in hello cache]: #specify-expiration
[Store ASP.NET session state in hello cache]: #store-session


<!-- IMAGES -->


[StackExchangeNuget]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-stackexchange-redis.png

[NuGetMenu]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-manage-nuget-menu.png

[CacheProperties]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-properties.png

[ManageKeys]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-manage-keys.png

[SessionStateNuGet]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-session-state-provider.png

[BrowseCaches]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-browse-caches.png

[Caches]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-caches.png







<!-- LINKS -->
[http://redis.io/clients]: http://redis.io/clients
[Develop in other languages for Azure Redis Cache]: http://msdn.microsoft.com/library/azure/dn690470.aspx
[How tooretrieve an Azure Redis connection string and use it with Redsmin]: https://redsmin.uservoice.com/knowledgebase/articles/485711-how-to-connect-redsmin-to-azure-redis-cache
[Azure Redis Session State Provider]: http://go.microsoft.com/fwlink/?LinkId=398249
[How to: Configure a Cache Client Programmatically]: http://msdn.microsoft.com/library/windowsazure/gg618003.aspx
[Session State Provider for Azure Cache]: http://go.microsoft.com/fwlink/?LinkId=320835
[Azure AppFabric Cache: Caching Session State]: http://www.microsoft.com/showcase/details.aspx?uuid=87c833e9-97a9-42b2-8bb1-7601f9b5ca20
[Output Cache Provider for Azure Cache]: http://go.microsoft.com/fwlink/?LinkId=320837
[Azure Shared Caching]: http://msdn.microsoft.com/library/windowsazure/gg278356.aspx
[Team Blog]: http://blogs.msdn.com/b/windowsazure/
[Azure Caching]: http://www.microsoft.com/showcase/Search.aspx?phrase=azure+caching
[How tooConfigure Virtual Machine Sizes]: http://go.microsoft.com/fwlink/?LinkId=164387
[Azure Caching Capacity Planning Considerations]: http://go.microsoft.com/fwlink/?LinkId=320167
[Azure Caching]: http://go.microsoft.com/fwlink/?LinkId=252658
[How to: Set hello Cacheability of an ASP.NET Page Declaratively]: http://msdn.microsoft.com/library/zd1ysf1y.aspx
[How to: Set a Page's Cacheability Programmatically]: http://msdn.microsoft.com/library/z852zf6b.aspx
[Configure a cache in Azure Redis Cache]: http://msdn.microsoft.com/library/azure/dn793612.aspx

[StackExchange.Redis configuration model]: https://stackexchange.github.io/StackExchange.Redis/Configuration

[Work with .NET objects in hello cache]: http://msdn.microsoft.com/library/dn690521.aspx#Objects


[NuGet Package Manager Installation]: http://go.microsoft.com/fwlink/?LinkId=240311
[Cache Pricing Details]: http://www.windowsazure.com/pricing/details/cache/
[Azure portal]: https://portal.azure.com/

[Overview of Azure Redis Cache]: http://go.microsoft.com/fwlink/?LinkId=320830
[Azure Redis Cache]: http://go.microsoft.com/fwlink/?LinkId=398247

[Migrate tooAzure Redis Cache]: http://go.microsoft.com/fwlink/?LinkId=317347
[Azure Redis Cache Samples]: http://go.microsoft.com/fwlink/?LinkId=320840
[Using Resource groups toomanage your Azure resources]: ../azure-resource-manager/resource-group-overview.md

[StackExchange.Redis]: http://github.com/StackExchange/StackExchange.Redis
[StackExchange.Redis cache client documentation]: http://github.com/StackExchange/StackExchange.Redis#documentation

[Redis]: http://redis.io/documentation
[Redis data types]: http://redis.io/topics/data-types
[a fifteen minute introduction tooRedis data types]: http://redis.io/topics/data-types-intro

[How Application Strings and Connection Strings Work]: http://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/


