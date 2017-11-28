---
title: "Jak używać usługi Azure Redis Cache | Microsoft Docs"
description: "Informacje na temat zwiększania wydajności aplikacji Azure za pomocą usługi Azure Redis Cache"
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
ms.openlocfilehash: 3dfc026490093523446650c510dbebdd660e8b6b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-azure-redis-cache"></a><span data-ttu-id="896d8-103">Jak używać usługi Azure Redis Cache</span><span class="sxs-lookup"><span data-stu-id="896d8-103">How to Use Azure Redis Cache</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="896d8-104">.NET</span><span class="sxs-lookup"><span data-stu-id="896d8-104">.NET</span></span>](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [<span data-ttu-id="896d8-105">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="896d8-105">ASP.NET</span></span>](cache-web-app-howto.md)
> * [<span data-ttu-id="896d8-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="896d8-106">Node.js</span></span>](cache-nodejs-get-started.md)
> * [<span data-ttu-id="896d8-107">Java</span><span class="sxs-lookup"><span data-stu-id="896d8-107">Java</span></span>](cache-java-get-started.md)
> * [<span data-ttu-id="896d8-108">Python</span><span class="sxs-lookup"><span data-stu-id="896d8-108">Python</span></span>](cache-python-get-started.md)
> 
> 

<span data-ttu-id="896d8-109">W tym przewodniku przedstawiono, jak rozpocząć pracę z usługą **Azure Redis Cache**.</span><span class="sxs-lookup"><span data-stu-id="896d8-109">This guide shows you how to get started using **Azure Redis Cache**.</span></span> <span data-ttu-id="896d8-110">Usługa Microsoft Azure Redis Cache jest oparta na popularnej pamięci podręcznej Redis typu open source.</span><span class="sxs-lookup"><span data-stu-id="896d8-110">Microsoft Azure Redis Cache is based on the popular open source Redis Cache.</span></span> <span data-ttu-id="896d8-111">Umożliwia dostęp do bezpiecznej, dedykowanej pamięci podręcznej Redis, zarządzanej przez firmę Microsoft.</span><span class="sxs-lookup"><span data-stu-id="896d8-111">It gives you access to a secure, dedicated Redis cache, managed by Microsoft.</span></span> <span data-ttu-id="896d8-112">Pamięć podręczna utworzona przy użyciu usługi Azure Redis Cache jest dostępna z poziomu dowolnej aplikacji w ramach platformy Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="896d8-112">A cache created using Azure Redis Cache is accessible from any application within Microsoft Azure.</span></span>

<span data-ttu-id="896d8-113">Usługa Microsoft Azure Redis Cache jest dostępna w następujących warstwach:</span><span class="sxs-lookup"><span data-stu-id="896d8-113">Microsoft Azure Redis Cache is available in the following tiers:</span></span>

* <span data-ttu-id="896d8-114">**Podstawowa** — jeden węzeł.</span><span class="sxs-lookup"><span data-stu-id="896d8-114">**Basic** – Single node.</span></span> <span data-ttu-id="896d8-115">Wiele rozmiarów do 53 GB.</span><span class="sxs-lookup"><span data-stu-id="896d8-115">Multiple sizes up to 53 GB.</span></span>
* <span data-ttu-id="896d8-116">**Standardowa** — dwa węzły (węzeł podstawowy i węzeł repliki).</span><span class="sxs-lookup"><span data-stu-id="896d8-116">**Standard** – Two-node Primary/Replica.</span></span> <span data-ttu-id="896d8-117">Wiele rozmiarów do 53 GB.</span><span class="sxs-lookup"><span data-stu-id="896d8-117">Multiple sizes up to 53 GB.</span></span> <span data-ttu-id="896d8-118">Umowa SLA na poziomie 99,9%.</span><span class="sxs-lookup"><span data-stu-id="896d8-118">99.9% SLA.</span></span>
* <span data-ttu-id="896d8-119">**Premium** — dwa węzły (węzeł podstawowy i węzeł repliki) zawierające do 10 fragmentów.</span><span class="sxs-lookup"><span data-stu-id="896d8-119">**Premium** – Two-node Primary/Replica with up to 10 shards.</span></span> <span data-ttu-id="896d8-120">Wiele rozmiarów od 6 GB do 530 GB.</span><span class="sxs-lookup"><span data-stu-id="896d8-120">Multiple sizes from 6 GB to 530 GB.</span></span> <span data-ttu-id="896d8-121">Wszystkie funkcje warstwy Standardowej i dodatkowe funkcje, m.in. obsługa [klastra Redis](cache-how-to-premium-clustering.md), [stanu trwałego pamięci podręcznej Redis](cache-how-to-premium-persistence.md) oraz usługi [Azure Virtual Network](cache-how-to-premium-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="896d8-121">All Standard tier features and more including support for [Redis cluster](cache-how-to-premium-clustering.md), [Redis persistence](cache-how-to-premium-persistence.md), and [Azure Virtual Network](cache-how-to-premium-vnet.md).</span></span> <span data-ttu-id="896d8-122">Umowa SLA na poziomie 99,9%.</span><span class="sxs-lookup"><span data-stu-id="896d8-122">99.9% SLA.</span></span>

<span data-ttu-id="896d8-123">Poszczególne warstwy różnią się od siebie pod względem funkcji i cen.</span><span class="sxs-lookup"><span data-stu-id="896d8-123">Each tier differs in terms of features and pricing.</span></span> <span data-ttu-id="896d8-124">Informacje dotyczące cen można znaleźć w artykule [Pamięć podręczna Redis — cennik][Cache Pricing Details].</span><span class="sxs-lookup"><span data-stu-id="896d8-124">For information on pricing, see [Cache Pricing Details][Cache Pricing Details].</span></span>

<span data-ttu-id="896d8-125">W tym przewodniku przedstawiono, jak korzystać z klienta [StackExchange.Redis][StackExchange.Redis] przy użyciu kodu C\#.</span><span class="sxs-lookup"><span data-stu-id="896d8-125">This guide shows you how to use the [StackExchange.Redis][StackExchange.Redis] client using C\# code.</span></span> <span data-ttu-id="896d8-126">Opisane scenariusze obejmują **tworzenie i konfigurowanie pamięci podręcznej**, **konfigurowanie klientów pamięci podręcznej** oraz **dodawanie i usuwanie obiektów z pamięci podręcznej**.</span><span class="sxs-lookup"><span data-stu-id="896d8-126">The scenarios covered include **creating and configuring a cache**, **configuring cache clients**, and **adding and removing objects from the cache**.</span></span> <span data-ttu-id="896d8-127">Aby uzyskać więcej informacji na temat korzystania z usługi Azure Redis Cache, zobacz [Następne kroki][Next Steps].</span><span class="sxs-lookup"><span data-stu-id="896d8-127">For more information on using Azure Redis Cache, see [Next Steps][Next Steps].</span></span> <span data-ttu-id="896d8-128">Samouczek krok po kroku dotyczący tworzenia aplikacji sieci Web ASP.NET MVC z użyciem pamięci podręcznej Redis znajduje się w artykule [Tworzenie aplikacji sieci Web z użyciem pamięci podręcznej Redis](cache-web-app-howto.md).</span><span class="sxs-lookup"><span data-stu-id="896d8-128">For a step-by-step tutorial of building an ASP.NET MVC web app with Redis Cache, see [How to create a Web App with Redis Cache](cache-web-app-howto.md).</span></span>

<a name="getting-started-cache-service"></a>

## <a name="get-started-with-azure-redis-cache"></a><span data-ttu-id="896d8-129">Rozpoczęcie pracy z usługą Azure Redis Cache</span><span class="sxs-lookup"><span data-stu-id="896d8-129">Get Started with Azure Redis Cache</span></span>
<span data-ttu-id="896d8-130">Rozpoczęcie pracy z usługą Azure Redis Cache jest proste.</span><span class="sxs-lookup"><span data-stu-id="896d8-130">Getting started with Azure Redis Cache is easy.</span></span> <span data-ttu-id="896d8-131">Aby rozpocząć, należy aprowizować i skonfigurować pamięć podręczną.</span><span class="sxs-lookup"><span data-stu-id="896d8-131">To get started, you provision and configure a cache.</span></span> <span data-ttu-id="896d8-132">Następnie należy skonfigurować klientów pamięci podręcznej, aby mogli uzyskać dostęp do pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="896d8-132">Next, you configure the cache clients so they can access the cache.</span></span> <span data-ttu-id="896d8-133">Po skonfigurowaniu klientów pamięci podręcznej można rozpocząć pracę.</span><span class="sxs-lookup"><span data-stu-id="896d8-133">Once the cache clients are configured, you can begin working with them.</span></span>

* <span data-ttu-id="896d8-134">[Tworzenie pamięci podręcznej][Create the cache]</span><span class="sxs-lookup"><span data-stu-id="896d8-134">[Create the cache][Create the cache]</span></span>
* <span data-ttu-id="896d8-135">[Konfigurowanie klientów pamięci podręcznej][Configure the cache clients]</span><span class="sxs-lookup"><span data-stu-id="896d8-135">[Configure the cache clients][Configure the cache clients]</span></span>

<a name="create-cache"></a>

## <a name="create-a-cache"></a><span data-ttu-id="896d8-136">Tworzenie pamięci podręcznej</span><span class="sxs-lookup"><span data-stu-id="896d8-136">Create a cache</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

### <a name="to-access-your-cache-after-its-created"></a><span data-ttu-id="896d8-137">Aby uzyskać dostęp do pamięci podręcznej po jej utworzeniu</span><span class="sxs-lookup"><span data-stu-id="896d8-137">To access your cache after it's created</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-browse.md)]

<span data-ttu-id="896d8-138">Więcej informacji na temat konfigurowania pamięci podręcznej znajduje się w temacie [How to configure Azure Redis Cache](cache-configure.md) (Konfigurowanie usługi Azure Redis Cache).</span><span class="sxs-lookup"><span data-stu-id="896d8-138">For more information about configuring your cache, see [How to configure Azure Redis Cache](cache-configure.md).</span></span>

<a name="NuGet"></a>

## <a name="configure-the-cache-clients"></a><span data-ttu-id="896d8-139">Konfigurowanie klientów pamięci podręcznej</span><span class="sxs-lookup"><span data-stu-id="896d8-139">Configure the cache clients</span></span>
[!INCLUDE [redis-cache-configure](../../includes/redis-cache-configure-stackexchange-redis-nuget.md)]

<span data-ttu-id="896d8-140">Po skonfigurowaniu projektu klienta do buforowania będzie można pracować z pamięcią podręczną przy użyciu metod opisanych w poniższych sekcjach.</span><span class="sxs-lookup"><span data-stu-id="896d8-140">Once your client project is configured for caching, you can use the techniques described in the following sections for working with your cache.</span></span>

<a name="working-with-caches"></a>

## <a name="working-with-caches"></a><span data-ttu-id="896d8-141">Praca z pamięciami podręcznymi</span><span class="sxs-lookup"><span data-stu-id="896d8-141">Working with Caches</span></span>
<span data-ttu-id="896d8-142">W tej sekcji opisano sposób wykonywania typowych zadań z pamięcią podręczną.</span><span class="sxs-lookup"><span data-stu-id="896d8-142">The steps in this section describe how to perform common tasks with Cache.</span></span>

* <span data-ttu-id="896d8-143">[Łączenie z pamięcią podręczną][Connect to the cache]</span><span class="sxs-lookup"><span data-stu-id="896d8-143">[Connect to the cache][Connect to the cache]</span></span>
* <span data-ttu-id="896d8-144">[Dodawanie i pobieranie obiektów z pamięci podręcznej][Add and retrieve objects from the cache]</span><span class="sxs-lookup"><span data-stu-id="896d8-144">[Add and retrieve objects from the cache][Add and retrieve objects from the cache]</span></span>
* [<span data-ttu-id="896d8-145">Praca z obiektami platformy .NET w pamięci podręcznej</span><span class="sxs-lookup"><span data-stu-id="896d8-145">Work with .NET objects in the cache</span></span>](#work-with-net-objects-in-the-cache)

<a name="connect-to-cache"></a>

## <a name="connect-to-the-cache"></a><span data-ttu-id="896d8-146">Łączenie z pamięcią podręczną</span><span class="sxs-lookup"><span data-stu-id="896d8-146">Connect to the cache</span></span>
<span data-ttu-id="896d8-147">Aby programowo pracować z pamięcią podręczną, potrzebujesz odwołania do pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="896d8-147">To programmatically work with a cache, you need a reference to the cache.</span></span> <span data-ttu-id="896d8-148">Dodaj poniższy kod na początku każdego pliku, z którego chcesz użyć klienta StackExchange.Redis, aby uzyskać dostęp do pamięci podręcznej Redis Azure.</span><span class="sxs-lookup"><span data-stu-id="896d8-148">Add the following to the top of any file from which you want to use the StackExchange.Redis client to access an Azure Redis Cache.</span></span>

    using StackExchange.Redis;

> [!NOTE]
> <span data-ttu-id="896d8-149">Klient StackExchange.Redis wymaga programu .NET Framework 4 lub jego nowszej wersji.</span><span class="sxs-lookup"><span data-stu-id="896d8-149">The StackExchange.Redis client requires .NET Framework 4 or higher.</span></span>
> 
> 

<span data-ttu-id="896d8-150">Połączenie z usługą Azure Redis Cache jest zarządzane przez klasę `ConnectionMultiplexer`.</span><span class="sxs-lookup"><span data-stu-id="896d8-150">The connection to the Azure Redis Cache is managed by the `ConnectionMultiplexer` class.</span></span> <span data-ttu-id="896d8-151">Ta klasa powinna być udostępniana i ponownie używana w aplikacji klienta i nie trzeba jej tworzyć w oparciu o operację.</span><span class="sxs-lookup"><span data-stu-id="896d8-151">This class should be shared and reused throughout your client application, and does not need to be created on a per operation basis.</span></span> 

<span data-ttu-id="896d8-152">Aby połączyć się z usługą Azure Redis Cache i otrzymać wystąpienie połączonej klasy `ConnectionMultiplexer`, wywołaj statyczną metodę `Connect` i przekaż klucz oraz punkt końcowy pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="896d8-152">To connect to an Azure Redis Cache and be returned an instance of a connected `ConnectionMultiplexer`, call the static `Connect` method and pass in the cache endpoint and key.</span></span> <span data-ttu-id="896d8-153">Użyj klucza wygenerowanego w witrynie Azure Portal jako parametru hasła.</span><span class="sxs-lookup"><span data-stu-id="896d8-153">Use the key generated from the Azure portal as the password parameter.</span></span>

    ConnectionMultiplexer connection = ConnectionMultiplexer.Connect("contoso5.redis.cache.windows.net,abortConnect=false,ssl=true,password=...");

> [!IMPORTANT]
> <span data-ttu-id="896d8-154">Ostrzeżenie: Nigdy nie przechowuj poświadczeń w kodzie źródłowym.</span><span class="sxs-lookup"><span data-stu-id="896d8-154">Warning: Never store credentials in source code.</span></span> <span data-ttu-id="896d8-155">Tutaj zostały one pokazane w kodzie źródłowym, aby uprościć przykład.</span><span class="sxs-lookup"><span data-stu-id="896d8-155">To keep this sample simple, I’m showing them in the source code.</span></span> <span data-ttu-id="896d8-156">Informacje na temat przechowywania poświadczeń znajdują się w artykule [How Application Strings and Connection Strings Work][How Application Strings and Connection Strings Work] (Sposób działania ciągów aplikacji i parametrów połączenia).</span><span class="sxs-lookup"><span data-stu-id="896d8-156">See [How Application Strings and Connection Strings Work][How Application Strings and Connection Strings Work] for information on how to store credentials.</span></span>
> 
> 

<span data-ttu-id="896d8-157">Jeśli nie chcesz używać protokołu SSL, ustaw wartość `ssl=false` lub pomiń parametr `ssl`.</span><span class="sxs-lookup"><span data-stu-id="896d8-157">If you don't want to use SSL, either set `ssl=false` or omit the `ssl` parameter.</span></span>

> [!NOTE]
> <span data-ttu-id="896d8-158">Port bez obsługi protokołu SSL jest domyślnie wyłączony w przypadku nowych pamięci podręcznych.</span><span class="sxs-lookup"><span data-stu-id="896d8-158">The non-SSL port is disabled by default for new caches.</span></span> <span data-ttu-id="896d8-159">Instrukcje dotyczące włączania portu bez obsługi protokołu SSL znajdują się w sekcji [Access Ports](cache-configure.md#access-ports) (Porty dostępu).</span><span class="sxs-lookup"><span data-stu-id="896d8-159">For instructions on enabling the non-SSL port, see [Access Ports](cache-configure.md#access-ports).</span></span>
> 
> 

<span data-ttu-id="896d8-160">Jednym z rozwiązań w zakresie udostępniania wystąpienia klasy `ConnectionMultiplexer` w aplikacji jest korzystanie z właściwości statycznej, która zwraca połączone wystąpienie podobnie jak w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="896d8-160">One approach to sharing a `ConnectionMultiplexer` instance in your application is to have a static property that returns a connected instance, similar to the following example.</span></span> <span data-ttu-id="896d8-161">To podejście oferuje bezpieczny wątkowo sposób na inicjowanie tylko jednego połączonego wystąpienia klasy `ConnectionMultiplexer`.</span><span class="sxs-lookup"><span data-stu-id="896d8-161">This approach provides a thread-safe way to initialize only a single connected `ConnectionMultiplexer` instance.</span></span> <span data-ttu-id="896d8-162">W tych przykładach parametr `abortConnect` ma wartość false, co oznacza, że wystąpienie zostanie wykonane pomyślnie, nawet jeśli połączenie z usługą Azure Redis Cache nie zostanie nawiązane.</span><span class="sxs-lookup"><span data-stu-id="896d8-162">In these examples `abortConnect` is set to false, which means that the call succeeds even if a connection to the Azure Redis Cache is not established.</span></span> <span data-ttu-id="896d8-163">Kluczowa funkcja klasy `ConnectionMultiplexer` polega na automatycznym przywracaniu łączności z pamięcią podręczną po rozwiązaniu problemu z siecią lub usunięciu innych przyczyn.</span><span class="sxs-lookup"><span data-stu-id="896d8-163">One key feature of `ConnectionMultiplexer` is that it automatically restores connectivity to the cache once the network issue or other causes are resolved.</span></span>

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

<span data-ttu-id="896d8-164">Więcej informacji na temat opcji zaawansowanej konfiguracji połączenia znajduje się w opisie [modelu konfiguracji StackExchange.Redis][StackExchange.Redis configuration model].</span><span class="sxs-lookup"><span data-stu-id="896d8-164">For more information on advanced connection configuration options, see [StackExchange.Redis configuration model][StackExchange.Redis configuration model].</span></span>

[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

<span data-ttu-id="896d8-165">Po nawiązaniu połączenia zwróć odwołanie do bazy danych pamięci podręcznej Redis przez wywołanie metody `ConnectionMultiplexer.GetDatabase`.</span><span class="sxs-lookup"><span data-stu-id="896d8-165">Once the connection is established, return a reference to the redis cache database by calling the `ConnectionMultiplexer.GetDatabase` method.</span></span> <span data-ttu-id="896d8-166">Obiekt zwracany z metody `GetDatabase` jest lekkim obiektem przekazującym i nie wymaga przechowywania.</span><span class="sxs-lookup"><span data-stu-id="896d8-166">The object returned from the `GetDatabase` method is a lightweight pass-through object and does not need to be stored.</span></span>

    // Connection refers to a property that returns a ConnectionMultiplexer
    // as shown in the previous example.
    IDatabase cache = Connection.GetDatabase();

    // Perform cache operations using the cache object...
    // Simple put of integral data types into the cache
    cache.StringSet("key1", "value");
    cache.StringSet("key2", 25);

    // Simple get of data types from the cache
    string key1 = cache.StringGet("key1");
    int key2 = (int)cache.StringGet("key2");

<span data-ttu-id="896d8-167">Pamięci podręczne Azure Redis Cache mają konfigurowalną liczbę baz danych (domyślnie 16), których można użyć do logicznego odseparowania danych w pamięci podręcznej Redis Cache.</span><span class="sxs-lookup"><span data-stu-id="896d8-167">Azure Redis caches have a configurable number of databases (default of 16) that can be used to logically separate the data within a Redis cache.</span></span> <span data-ttu-id="896d8-168">Aby uzyskać więcej informacji, zobacz [What are Redis databases?](cache-faq.md#what-are-redis-databases) (Co to są bazy danych Redis?) i [Default Redis server configuration](cache-configure.md#default-redis-server-configuration) (Domyślna konfiguracja serwera Redis).</span><span class="sxs-lookup"><span data-stu-id="896d8-168">For more information, see [What are Redis databases?](cache-faq.md#what-are-redis-databases) and [Default Redis server configuration](cache-configure.md#default-redis-server-configuration).</span></span>

<span data-ttu-id="896d8-169">Teraz gdy wiesz, jak połączyć się z wystąpieniem usługi Azure Redis Cache i zwrócić odwołanie do bazy danych pamięci podręcznej, przyjrzyjmy się pracy z pamięcią podręczną.</span><span class="sxs-lookup"><span data-stu-id="896d8-169">Now that you know how to connect to an Azure Redis Cache instance and return a reference to the cache database, let's look at working with the cache.</span></span>

<a name="add-object"></a>

## <a name="add-and-retrieve-objects-from-the-cache"></a><span data-ttu-id="896d8-170">Dodawanie i pobieranie obiektów z pamięci podręcznej</span><span class="sxs-lookup"><span data-stu-id="896d8-170">Add and retrieve objects from the cache</span></span>
<span data-ttu-id="896d8-171">Elementy można zapisywać do pamięci podręcznej i pobierać z niej za pomocą metod `StringSet` i `StringGet`.</span><span class="sxs-lookup"><span data-stu-id="896d8-171">Items can be stored in and retrieved from a cache by using the `StringSet` and `StringGet` methods.</span></span>

    // If key1 exists, it is overwritten.
    cache.StringSet("key1", "value1");

    string value = cache.StringGet("key1");

<span data-ttu-id="896d8-172">Usługa Redis przechowuje większość danych w formie ciągów Redis, ale ciągi te mogą zawierać wiele typów danych, w tym serializowane dane binarne, które mogą być używane podczas przechowywania obiektów platformy .NET w pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="896d8-172">Redis stores most data as Redis strings, but these strings can contain many types of data, including serialized binary data, which can be used when storing .NET objects in the cache.</span></span>

<span data-ttu-id="896d8-173">Podczas wywoływania metody `StringGet`, jeśli obiekt istnieje, jest zwracany, a jeśli nie, zwracana jest wartość `null`.</span><span class="sxs-lookup"><span data-stu-id="896d8-173">When calling `StringGet`, if the object exists, it is returned, and if it does not, `null` is returned.</span></span> <span data-ttu-id="896d8-174">W przypadku zwrócenia wartości `null` można pobrać wartość z żądanego źródła danych i zapisać ją w pamięci podręcznej do późniejszego użytku.</span><span class="sxs-lookup"><span data-stu-id="896d8-174">If `null` is returned, you can retrieve the value from the desired data source and store it in the cache for subsequent use.</span></span> <span data-ttu-id="896d8-175">Ten wzorzec użycia nazywamy wzorcem z odkładaniem do pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="896d8-175">This usage pattern is known as the cache-aside pattern.</span></span>

    string value = cache.StringGet("key1");
    if (value == null)
    {
        // The item keyed by "key1" is not in the cache. Obtain
        // it from the desired data source and add it to the cache.
        value = GetValueFromDataSource();

        cache.StringSet("key1", value);
    }

<span data-ttu-id="896d8-176">Alternatywnie możesz użyć typu `RedisValue`, jak pokazano w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="896d8-176">You can also use `RedisValue`, as shown in the following example.</span></span> <span data-ttu-id="896d8-177">Typ `RedisValue` ma niejawne operatory do pracy z integralnymi typami danych. To rozwiązanie może być użyteczne, jeśli oczekiwaną wartością dla elementu w pamięci podręcznej jest `null`.</span><span class="sxs-lookup"><span data-stu-id="896d8-177">`RedisValue` has implicit operators for working with integral data types, and can be useful if `null` is an expected value for a cached item.</span></span>


    RedisValue value = cache.StringGet("key1");
    if (!value.HasValue)
    {
        value = GetValueFromDataSource();
        cache.StringSet("key1", value);
    }


<span data-ttu-id="896d8-178">Aby określić wygaśnięcie elementu w pamięci podręcznej, użyj parametru `TimeSpan` metody `StringSet`.</span><span class="sxs-lookup"><span data-stu-id="896d8-178">To specify the expiration of an item in the cache, use the `TimeSpan` parameter of `StringSet`.</span></span>

    cache.StringSet("key1", "value1", TimeSpan.FromMinutes(90));

## <a name="work-with-net-objects-in-the-cache"></a><span data-ttu-id="896d8-179">Praca z obiektami platformy .NET w pamięci podręcznej</span><span class="sxs-lookup"><span data-stu-id="896d8-179">Work with .NET objects in the cache</span></span>
<span data-ttu-id="896d8-180">Usługa Azure Redis Cache może buforować obiekty platformy .NET oraz pierwotne typy danych, ale zanim będzie możliwe buforowanie obiektu platformy .NET, trzeba go serializować.</span><span class="sxs-lookup"><span data-stu-id="896d8-180">Azure Redis Cache can cache both .NET objects and primitive data types, but before a .NET object can be cached it must be serialized.</span></span> <span data-ttu-id="896d8-181">Odpowiedzialność za serializację obiektu .NET spoczywa na deweloperze aplikacji, który ma możliwość wybrania serializatora.</span><span class="sxs-lookup"><span data-stu-id="896d8-181">This .NET object serialization is the responsibility of the application developer, and gives the developer flexibility in the choice of the serializer.</span></span>

<span data-ttu-id="896d8-182">Prostym sposobem na wykonywanie serializacji obiektów jest użycie metod serializacji `JsonConvert` w środowisku [Newtonsoft.Json.NET](https://www.nuget.org/packages/Newtonsoft.Json/8.0.1-beta1) oraz serializacja do i z formatu JSON.</span><span class="sxs-lookup"><span data-stu-id="896d8-182">One simple way to serialize objects is to use the `JsonConvert` serialization methods in [Newtonsoft.Json.NET](https://www.nuget.org/packages/Newtonsoft.Json/8.0.1-beta1) and serialize to and from JSON.</span></span> <span data-ttu-id="896d8-183">W poniższym przykładzie pokazano metody get i set używające wystąpienia obiektu `Employee`.</span><span class="sxs-lookup"><span data-stu-id="896d8-183">The following example shows a get and set using an `Employee` object instance.</span></span>

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

    // Store to cache
    cache.StringSet("e25", JsonConvert.SerializeObject(new Employee(25, "Clayton Gragg")));

    // Retrieve from cache
    Employee e25 = JsonConvert.DeserializeObject<Employee>(cache.StringGet("e25"));

<a name="next-steps"></a>

## <a name="next-steps"></a><span data-ttu-id="896d8-184">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="896d8-184">Next Steps</span></span>
<span data-ttu-id="896d8-185">Teraz, kiedy znasz już podstawy, skorzystaj z poniższych linków i dowiedz się więcej na temat usługi Azure Redis Cache.</span><span class="sxs-lookup"><span data-stu-id="896d8-185">Now that you've learned the basics, follow these links to learn more about Azure Redis Cache.</span></span>

* <span data-ttu-id="896d8-186">Sprawdź dostawców programu ASP.NET dla usługi Azure Redis Cache.</span><span class="sxs-lookup"><span data-stu-id="896d8-186">Check out the ASP.NET providers for Azure Redis Cache.</span></span>
  * [<span data-ttu-id="896d8-187">Dostawca stanu sesji usługi Azure Redis</span><span class="sxs-lookup"><span data-stu-id="896d8-187">Azure Redis Session State Provider</span></span>](cache-aspnet-session-state-provider.md)
  * [<span data-ttu-id="896d8-188">Dostawca wyjściowej pamięci podręcznej programu ASP.NET w usłudze Azure Redis Cache</span><span class="sxs-lookup"><span data-stu-id="896d8-188">Azure Redis Cache ASP.NET Output Cache Provider</span></span>](cache-aspnet-output-cache-provider.md)
* <span data-ttu-id="896d8-189">[Włącz diagnostykę pamięci podręcznej](cache-how-to-monitor.md#enable-cache-diagnostics), aby móc [monitorować](cache-how-to-monitor.md) jej kondycję.</span><span class="sxs-lookup"><span data-stu-id="896d8-189">[Enable cache diagnostics](cache-how-to-monitor.md#enable-cache-diagnostics) so you can [monitor](cache-how-to-monitor.md) the health of your cache.</span></span> <span data-ttu-id="896d8-190">Możesz wyświetlać metryki w witrynie Azure Portal oraz [pobierać i przeglądać](https://github.com/rustd/RedisSamples/tree/master/CustomMonitoring) je przy użyciu wybranych przez siebie narzędzi.</span><span class="sxs-lookup"><span data-stu-id="896d8-190">You can view the metrics in the Azure portal and you can also [download and review](https://github.com/rustd/RedisSamples/tree/master/CustomMonitoring) them using the tools of your choice.</span></span>
* <span data-ttu-id="896d8-191">Zapoznaj się z [dokumentacją dotyczącą klienta pamięci podręcznej StackExchange.Redis][StackExchange.Redis cache client documentation].</span><span class="sxs-lookup"><span data-stu-id="896d8-191">Check out the [StackExchange.Redis cache client documentation][StackExchange.Redis cache client documentation].</span></span>
  * <span data-ttu-id="896d8-192">Dostęp do usługi Azure Redis Cache można uzyskać z wielu klientów Redis i przy użyciu wielu języków programowania.</span><span class="sxs-lookup"><span data-stu-id="896d8-192">Azure Redis Cache can be accessed from many Redis clients and development languages.</span></span> <span data-ttu-id="896d8-193">Więcej informacji znajduje się na stronie [http://redis.io/clients][http://redis.io/clients].</span><span class="sxs-lookup"><span data-stu-id="896d8-193">For more information, see [http://redis.io/clients][http://redis.io/clients].</span></span>
* <span data-ttu-id="896d8-194">Usługi Azure Redis Cache można również używać z usługami i narzędziami innych firm, takimi jak Redsmin i Redis Desktop Manager.</span><span class="sxs-lookup"><span data-stu-id="896d8-194">Azure Redis Cache can also be used with third-party services and tools such as Redsmin and Redis Desktop Manager.</span></span>
  * <span data-ttu-id="896d8-195">Więcej informacji na temat usługi Redsmin znajduje się w artykule [How to retrieve an Azure Redis connection string and use it with Redsmin][How to retrieve an Azure Redis connection string and use it with Redsmin] (Jak pobrać parametry połączenia usługi Azure Redis i używać ich w usłudze Redsmin).</span><span class="sxs-lookup"><span data-stu-id="896d8-195">For more information about Redsmin, see [How to retrieve an Azure Redis connection string and use it with Redsmin][How to retrieve an Azure Redis connection string and use it with Redsmin].</span></span>
  * <span data-ttu-id="896d8-196">Dostęp do danych w usłudze Azure Redis Cache oraz możliwość ich inspekcji można uzyskać za pomocą graficznego interfejsu użytkownika, używając usługi [RedisDesktopManager](https://github.com/uglide/RedisDesktopManager).</span><span class="sxs-lookup"><span data-stu-id="896d8-196">Access and inspect your data in Azure Redis Cache with a GUI using [RedisDesktopManager](https://github.com/uglide/RedisDesktopManager).</span></span>
* <span data-ttu-id="896d8-197">Zapoznaj się z dokumentacją dotyczącą usługi [Redis][redis], przeczytaj o [typach danych usługi Redis][redis data types] oraz poznaj [piętnastominutowe wprowadzenie do typów danych usługi Redis][a fifteen minute introduction to Redis data types].</span><span class="sxs-lookup"><span data-stu-id="896d8-197">See the [redis][redis] documentation and read about [redis data types][redis data types] and [a fifteen minute introduction to Redis data types][a fifteen minute introduction to Redis data types].</span></span>

<!-- INTRA-TOPIC LINKS -->
[Next Steps]: #next-steps
[Introduction to Azure Redis Cache (Video)]: #video
[What is Azure Redis Cache?]: #what-is
[Create an Azure Cache]: #create-cache
[Which type of caching is right for me?]: #choosing-cache
[Prepare Your Visual Studio Project to Use Azure Caching]: #prepare-vs
[Configure Your Application to Use Caching]: #configure-app
[Get Started with Azure Redis Cache]: #getting-started-cache-service
[Create the cache]: #create-cache
[Configure the cache]: #enable-caching
[Configure the cache clients]: #NuGet
[Working with Caches]: #working-with-caches
[Connect to the cache]: #connect-to-cache
[Add and retrieve objects from the cache]: #add-object
[Specify the expiration of an object in the cache]: #specify-expiration
[Store ASP.NET session state in the cache]: #store-session


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
[How to retrieve an Azure Redis connection string and use it with Redsmin]: https://redsmin.uservoice.com/knowledgebase/articles/485711-how-to-connect-redsmin-to-azure-redis-cache
[Azure Redis Session State Provider]: http://go.microsoft.com/fwlink/?LinkId=398249
[How to: Configure a Cache Client Programmatically]: http://msdn.microsoft.com/library/windowsazure/gg618003.aspx
[Session State Provider for Azure Cache]: http://go.microsoft.com/fwlink/?LinkId=320835
[Azure AppFabric Cache: Caching Session State]: http://www.microsoft.com/showcase/details.aspx?uuid=87c833e9-97a9-42b2-8bb1-7601f9b5ca20
[Output Cache Provider for Azure Cache]: http://go.microsoft.com/fwlink/?LinkId=320837
[Azure Shared Caching]: http://msdn.microsoft.com/library/windowsazure/gg278356.aspx
[Team Blog]: http://blogs.msdn.com/b/windowsazure/
[Azure Caching]: http://www.microsoft.com/showcase/Search.aspx?phrase=azure+caching
[How to Configure Virtual Machine Sizes]: http://go.microsoft.com/fwlink/?LinkId=164387
[Azure Caching Capacity Planning Considerations]: http://go.microsoft.com/fwlink/?LinkId=320167
[Azure Caching]: http://go.microsoft.com/fwlink/?LinkId=252658
[How to: Set the Cacheability of an ASP.NET Page Declaratively]: http://msdn.microsoft.com/library/zd1ysf1y.aspx
[How to: Set a Page's Cacheability Programmatically]: http://msdn.microsoft.com/library/z852zf6b.aspx
[Configure a cache in Azure Redis Cache]: http://msdn.microsoft.com/library/azure/dn793612.aspx

[StackExchange.Redis configuration model]: https://stackexchange.github.io/StackExchange.Redis/Configuration

[Work with .NET objects in the cache]: http://msdn.microsoft.com/library/dn690521.aspx#Objects


[NuGet Package Manager Installation]: http://go.microsoft.com/fwlink/?LinkId=240311
[Cache Pricing Details]: http://www.windowsazure.com/pricing/details/cache/
[Azure portal]: https://portal.azure.com/

[Overview of Azure Redis Cache]: http://go.microsoft.com/fwlink/?LinkId=320830
[Azure Redis Cache]: http://go.microsoft.com/fwlink/?LinkId=398247

[Migrate to Azure Redis Cache]: http://go.microsoft.com/fwlink/?LinkId=317347
[Azure Redis Cache Samples]: http://go.microsoft.com/fwlink/?LinkId=320840
[Using Resource groups to manage your Azure resources]: ../azure-resource-manager/resource-group-overview.md

[StackExchange.Redis]: http://github.com/StackExchange/StackExchange.Redis
[StackExchange.Redis cache client documentation]: http://github.com/StackExchange/StackExchange.Redis#documentation

[Redis]: http://redis.io/documentation
[Redis data types]: http://redis.io/topics/data-types
[a fifteen minute introduction to Redis data types]: http://redis.io/topics/data-types-intro

[How Application Strings and Connection Strings Work]: http://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/


