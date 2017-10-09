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
# <a name="how-toouse-azure-redis-cache"></a>Jak tooUse Azure pamięci podręcznej Redis
> [!div class="op_single_selector"]
> * [.NET](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [ASP.NET](cache-web-app-howto.md)
> * [Node.js](cache-nodejs-get-started.md)
> * [Java](cache-java-get-started.md)
> * [Python](cache-python-get-started.md)
> 
> 

W tym przewodniku przedstawiono sposób tooget uruchamiania przy użyciu **pamięć podręczna Redis Azure**. Pamięć podręczna Redis Azure firmy Microsoft jest oparta na powitania popularnych typu open source pamięci podręcznej Redis. Daje dostęp do tooa bezpiecznego, dedykowane pamięć podręczna Redis, zarządzany przez firmę Microsoft. Pamięć podręczna utworzona przy użyciu usługi Azure Redis Cache jest dostępna z poziomu dowolnej aplikacji w ramach platformy Microsoft Azure.

Pamięć podręczna Redis Azure firmy Microsoft jest dostępna w hello następujące warstwy:

* **Podstawowa** — jeden węzeł. Wiele wielkości too53 GB.
* **Standardowa** — dwa węzły (węzeł podstawowy i węzeł repliki). Wiele wielkości too53 GB. Umowa SLA na poziomie 99,9%.
* **Premium** — dwa węzły podstawowego/repliki o zapasowej odłamków too10. Różne rozmiary od 6 GB too530 GB. Wszystkie funkcje warstwy Standardowej i dodatkowe funkcje, m.in. obsługa [klastra Redis](cache-how-to-premium-clustering.md), [stanu trwałego pamięci podręcznej Redis](cache-how-to-premium-persistence.md) oraz usługi [Azure Virtual Network](cache-how-to-premium-vnet.md). Umowa SLA na poziomie 99,9%.

Poszczególne warstwy różnią się od siebie pod względem funkcji i cen. Informacje dotyczące cen można znaleźć w artykule [Pamięć podręczna Redis — cennik][Cache Pricing Details].

W tym przewodniku przedstawiono sposób toouse hello [programie StackExchange.Redis] [ StackExchange.Redis] klienta przy użyciu C\# kodu. Witaj omówione scenariusze obejmują **tworzenie i konfigurowanie pamięci podręcznej**, **Konfigurowanie klientów pamięci podręcznej**, i **Dodawanie i usuwanie obiektów z pamięci podręcznej hello**. Aby uzyskać więcej informacji na temat korzystania z usługi Azure Redis Cache, zobacz [Następne kroki][Next Steps]. Krok po kroku samouczek tworzenia aplikacji sieci web z pamięci podręcznej Redis ASP.NET MVC, zobacz [jak toocreate aplikacji sieci Web z pamięci podręcznej Redis](cache-web-app-howto.md).

<a name="getting-started-cache-service"></a>

## <a name="get-started-with-azure-redis-cache"></a>Rozpoczęcie pracy z usługą Azure Redis Cache
Rozpoczęcie pracy z usługą Azure Redis Cache jest proste. tooget pracę, należy udostępnić i skonfigurować pamięć podręczną. Następnie należy skonfigurować klientów pamięci podręcznej hello, więc mogą uzyskiwać dostęp do pamięci podręcznej hello. Po skonfigurowaniu hello pamięci podręcznej klientów, można rozpocząć pracę z nimi.

* [Tworzenie pamięci podręcznej hello][Create hello cache]
* [Konfigurowanie klientów pamięci podręcznej hello][Configure hello cache clients]

<a name="create-cache"></a>

## <a name="create-a-cache"></a>Tworzenie pamięci podręcznej
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

### <a name="tooaccess-your-cache-after-its-created"></a>tooaccess pamięć podręczną po jego utworzeniu
[!INCLUDE [redis-cache-create](../../includes/redis-cache-browse.md)]

Aby uzyskać więcej informacji o konfigurowaniu pamięci podręcznej, zobacz [jak tooconfigure pamięć podręczna Redis Azure](cache-configure.md).

<a name="NuGet"></a>

## <a name="configure-hello-cache-clients"></a>Konfigurowanie klientów pamięci podręcznej hello
[!INCLUDE [redis-cache-configure](../../includes/redis-cache-configure-stackexchange-redis-nuget.md)]

Gdy projekt klienta zostanie skonfigurowany do buforowania, można użyć hello metod opisanych w hello następujące sekcje zawierają informacje dotyczące pracy z pamięci podręcznej.

<a name="working-with-caches"></a>

## <a name="working-with-caches"></a>Praca z pamięciami podręcznymi
Witaj w tej sekcji opisano sposób tooperform typowe zadania z pamięci podręcznej.

* [Połącz toohello pamięci podręcznej][Connect toohello cache]
* [Dodaj i pobrać z pamięci podręcznej hello obiektów][Add and retrieve objects from hello cache]
* [Praca z obiektami .NET w pamięci podręcznej hello](#work-with-net-objects-in-the-cache)

<a name="connect-to-cache"></a>

## <a name="connect-toohello-cache"></a>Połącz toohello pamięci podręcznej
tooprogrammatically pracy z pamięci podręcznej, należy buforu toohello odwołań. Dodaj powitania od góry toohello dla dowolnego pliku, z którego chcesz toouse hello programie StackExchange.Redis klienta tooaccess pamięć podręczna Redis Azure.

    using StackExchange.Redis;

> [!NOTE]
> Witaj programie StackExchange.Redis klienta wymaga programu .NET Framework 4 lub nowszej.
> 
> 

Witaj toohello połączenia z pamięcią podręczną Redis Azure jest zarządzana przez hello `ConnectionMultiplexer` klasy. Ta klasa powinny być udostępniane i użyć ponownie w całej aplikacji klienckiej i nie musi toobe utworzone na podstawie na operację. 

tooan tooconnect pamięć podręczna Redis Azure i można zwrócić wystąpienia połączonych `ConnectionMultiplexer`, wywołanie hello statycznych `Connect` — metoda i przekaż hello pamięci podręcznej punktu końcowego i klucz. Za pomocą klawisza hello wygenerowane z portalu Azure jako parametr password hello hello.

    ConnectionMultiplexer connection = ConnectionMultiplexer.Connect("contoso5.redis.cache.windows.net,abortConnect=false,ssl=true,password=...");

> [!IMPORTANT]
> Ostrzeżenie: Nigdy nie przechowuj poświadczeń w kodzie źródłowym. tookeep to prosty przykład I używam wyświetlania ich w kodzie źródłowym hello. Zobacz [jak ciągi aplikacji i pracy ciągów połączenia] [ How Application Strings and Connection Strings Work] informacji na temat toostore poświadczeń.
> 
> 

Jeśli nie chcesz toouse SSL, albo ustaw `ssl=false` lub Pomiń hello `ssl` parametru.

> [!NOTE]
> port bez protokołu SSL Hello jest domyślnie wyłączona, dla nowych pamięci podręcznych. Aby uzyskać instrukcje na temat włączania portu bez protokołu SSL hello, zobacz [porty dostępu](cache-configure.md#access-ports).
> 
> 

Jednym z podejść toosharing `ConnectionMultiplexer` toohave statycznej właściwości, która zwraca wystąpienie połączonych toohello podobnie poniższy przykład jest wystąpienie w aplikacji. Metoda ta umożliwia tooinitialize sposób zapewniający obsługę wielowątkowości, tylko jeden połączony `ConnectionMultiplexer` wystąpienia. W tych przykładach `abortConnect` jest zestaw toofalse, co oznacza, nawet jeśli nie zostanie nawiązane połączenie toohello pamięć podręczna Redis Azure powiedzie się hello wywołania. Jedna funkcja klucza `ConnectionMultiplexer` jest on automatycznie przywraca łączności toohello w pamięci podręcznej po hello problem z siecią lub inne przyczyny zostaną rozwiązane.

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

Więcej informacji na temat opcji zaawansowanej konfiguracji połączenia znajduje się w opisie [modelu konfiguracji StackExchange.Redis][StackExchange.Redis configuration model].

[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

Po nawiązaniu połączenia hello zwrócić bazy danych pamięci podręcznej redis toohello odwołania przez wywołanie hello `ConnectionMultiplexer.GetDatabase` metody. zwróciła obiekt Hello hello `GetDatabase` metody jest obiektem przekazujące lekkie i nie wymaga toobe przechowywane.

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

Pamięci podręcznej pamięci podręcznej Redis Azure mają można skonfigurować liczbę baz danych (domyślnie 16), które mogą być używane toologically oddzielne hello danych w pamięci podręcznej Redis. Aby uzyskać więcej informacji, zobacz [What are Redis databases?](cache-faq.md#what-are-redis-databases) (Co to są bazy danych Redis?) i [Default Redis server configuration](cache-configure.md#default-redis-server-configuration) (Domyślna konfiguracja serwera Redis).

Teraz, gdy wiesz, jak wystąpienia pamięci podręcznej Redis Azure tooan tooconnect i przywracać toohello odwołania pamięci podręcznej bazy danych, Przyjrzyjmy się pracy z pamięci podręcznej hello.

<a name="add-object"></a>

## <a name="add-and-retrieve-objects-from-hello-cache"></a>Dodaj i pobrać z pamięci podręcznej hello obiektów
Elementy można przechowywane w i pobierane z pamięci podręcznej za pomocą hello `StringSet` i `StringGet` metody.

    // If key1 exists, it is overwritten.
    cache.StringSet("key1", "value1");

    string value = cache.StringGet("key1");

W pamięci podręcznej redis, większość danych jako ciągi Redis, ale te ciągi mogą zawierać wiele typów danych, w tym serializacji danych binarnych, którego można użyć w przypadku przechowywania .NET obiektów w pamięci podręcznej hello magazynów.

Podczas wywoływania metody `StringGet`, jeśli obiekt hello istnieje, jest zwracany, a jeśli nie, `null` jest zwracany. Jeśli `null` jest zwracany, można pobrać wartości hello ze źródła danych odpowiednie hello i zapisz go w pamięci podręcznej hello na potrzeby późniejszego wykorzystania. Ten wzorzec użycia jest określany jako hello Zarezerwuj pamięć podręczna wzorzec.

    string value = cache.StringGet("key1");
    if (value == null)
    {
        // hello item keyed by "key1" is not in hello cache. Obtain
        // it from hello desired data source and add it toohello cache.
        value = GetValueFromDataSource();

        cache.StringSet("key1", value);
    }

Można również użyć `RedisValue`, jak pokazano w hello poniższy przykład. Typ `RedisValue` ma niejawne operatory do pracy z integralnymi typami danych. To rozwiązanie może być użyteczne, jeśli oczekiwaną wartością dla elementu w pamięci podręcznej jest `null`.


    RedisValue value = cache.StringGet("key1");
    if (!value.HasValue)
    {
        value = GetValueFromDataSource();
        cache.StringSet("key1", value);
    }


wygaśnięcie hello toospecify elementu w pamięci podręcznej hello, użyj hello `TimeSpan` parametr `StringSet`.

    cache.StringSet("key1", "value1", TimeSpan.FromMinutes(90));

## <a name="work-with-net-objects-in-hello-cache"></a>Praca z obiektami .NET w pamięci podręcznej hello
Usługa Azure Redis Cache może buforować obiekty platformy .NET oraz pierwotne typy danych, ale zanim będzie możliwe buforowanie obiektu platformy .NET, trzeba go serializować. Serializację obiektu .NET jest odpowiedzialny za hello Deweloper aplikacji hello i zapewnia elastyczność developer hello hello wyborze hello serializatora.

Jeden tooserialize prosty sposób obiektów jest toouse hello `JsonConvert` metody serializacji w [Newtonsoft.Json.NET](https://www.nuget.org/packages/Newtonsoft.Json/8.0.1-beta1) i serializacji tooand z formatu JSON. Witaj poniższy przykład przedstawia get i set z `Employee` wystąpienie obiektu.

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

## <a name="next-steps"></a>Następne kroki
Teraz, kiedy znasz już podstawy hello, należy wykonać te dodatkowe informacje o pamięci podręcznej Redis Azure toolearn łącza.

* Zapoznaj się z hello dostawcy platformy ASP.NET dla pamięci podręcznej Redis Azure.
  * [Dostawca stanu sesji usługi Azure Redis](cache-aspnet-session-state-provider.md)
  * [Dostawca wyjściowej pamięci podręcznej programu ASP.NET w usłudze Azure Redis Cache](cache-aspnet-output-cache-provider.md)
* [Włącz diagnostykę w pamięci podręcznej](cache-how-to-monitor.md#enable-cache-diagnostics) można więc [monitor](cache-how-to-monitor.md) hello kondycji pamięci podręcznej. Możesz wyświetlić hello metryki w hello portalu Azure i może również [pobrać i przejrzyj](https://github.com/rustd/RedisSamples/tree/master/CustomMonitoring) je za pomocą narzędzi hello wybranych przez użytkownika.
* Zapoznaj się z hello [programie StackExchange.Redis pamięci podręcznej klienta dokumentacji][StackExchange.Redis cache client documentation].
  * Dostęp do usługi Azure Redis Cache można uzyskać z wielu klientów Redis i przy użyciu wielu języków programowania. Więcej informacji znajduje się na stronie [http://redis.io/clients][http://redis.io/clients].
* Usługi Azure Redis Cache można również używać z usługami i narzędziami innych firm, takimi jak Redsmin i Redis Desktop Manager.
  * Aby uzyskać więcej informacji o Redsmin, zobacz [jak tooretrieve połączenia Azure Redis ciąg i korzystania z niego Redsmin][How tooretrieve an Azure Redis connection string and use it with Redsmin].
  * Dostęp do danych w usłudze Azure Redis Cache oraz możliwość ich inspekcji można uzyskać za pomocą graficznego interfejsu użytkownika, używając usługi [RedisDesktopManager](https://github.com/uglide/RedisDesktopManager).
* Zobacz hello [redis] [ redis] dokumentacji i przeczytaj temat [redis typy danych] [ redis data types] i [wprowadzenie piętnastu minut typy danych tooRedis][a fifteen minute introduction tooRedis data types].

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


