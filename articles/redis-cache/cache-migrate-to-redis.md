---
title: "aaaMigrate usługi zarządzana pamięć podręczna aplikacji tooRedis - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toomigrate usługi zarządzana pamięć podręczna i pamięci podręcznej w roli aplikacji tooAzure pamięci podręcznej Redis"
services: redis-cache
documentationcenter: na
author: steved0x
manager: douge
editor: tysonn
ms.assetid: 041f077b-8c8e-4d7c-a3fc-89d334ed70d6
ms.service: cache
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 05/30/2017
ms.author: sdanie
ms.openlocfilehash: bd81722820acf0d2637828fbb6100c723aafeba5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-from-managed-cache-service-tooazure-redis-cache"></a>Migrowanie z usługi zarządzana pamięć podręczna tooAzure pamięci podręcznej Redis
Migrowanie aplikacji korzystających z usługi zarządzana pamięć podręczna Azure tooAzure pamięci podręcznej Redis można wykonywać przy minimalnych zmianach tooyour aplikacji, w zależności od funkcji usługi zarządzana pamięć podręczna hello używanych przez aplikację do buforowania. Hello interfejsów API nie są dokładnie hello tego samego są podobne, i znacznie istniejący kod, który używa usługi zarządzana pamięć podręczna tooaccess pamięci podręcznej mogą być ponownie używane przy minimalnych zmianach. W tym temacie przedstawiono sposób toomake hello niezbędną konfigurację i aplikacji zmian toomigrate Twojego toouse aplikacji usługi zarządzana pamięć podręczna pamięć podręczna Redis Azure i pokazuje, jak niektóre funkcje hello pamięć podręczna Redis Azure może być używane tooimplement hello funkcji Usługi zarządzana pamięć podręczna pamięci podręcznej.

>[!NOTE]
>Zarządzane usługi pamięć podręczna i pamięci podręcznej w roli zostały [wycofane](https://azure.microsoft.com/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/) 30 listopada 2016 r. Jeśli wszystkie wdrożenia pamięci podręcznej w roli, które mają tooAzure toomigrate pamięci podręcznej Redis, można wykonać kroki hello w tym artykule.

## <a name="migration-steps"></a>Kroki migracji
Witaj następujące kroki są wymagane toomigrate toouse aplikacji usługi zarządzana pamięć podręczna Redis Azure w pamięci podręcznej.

* Mapowanie usługi zarządzana pamięć podręczna funkcji tooAzure pamięci podręcznej Redis
* Wybierz ofertę pamięci podręcznej
* Tworzenie pamięci podręcznej
* Konfigurowanie klientów pamięci podręcznej hello
  * Usuń hello konfiguracji usługi zarządzana pamięć podręczna
  * Konfigurowanie klienta pamięci podręcznej przy użyciu hello pakietu NuGet w programie StackExchange.Redis
* Migrowanie kodu usługi zarządzana pamięć podręczna
  * Połącz toohello pamięci podręcznej za pomocą klasy ConnectionMultiplexer hello
  * Typy pierwotne danych programu Access w pamięci podręcznej hello
  * Praca z obiektami .NET w pamięci podręcznej hello
* Migracja stanu sesji ASP.NET i tooAzure pamięci podręcznej Redis do buforowania danych wyjściowych 

## <a name="map-managed-cache-service-features-tooazure-redis-cache"></a>Mapowanie usługi zarządzana pamięć podręczna funkcji tooAzure pamięci podręcznej Redis
Azure usługi zarządzana pamięć podręczna i pamięcią podręczną Redis Azure są podobne, ale niektóre funkcje ich wdrożenie na różne sposoby. W tej sekcji opisano niektóre różnice hello i znajdują się wskazówki dotyczące implementowania funkcji hello usługi zarządzana pamięć podręczna w pamięci podręcznej Redis Azure.

| Zarządzane funkcji usługi pamięć podręczna | Obsługa usługi pamięć podręczna zarządzanych | Obsługa pamięci podręcznej Redis Azure |
| --- | --- | --- |
| Bufory o nazwie |Domyślne pamięci podręcznej jest skonfigurowany, a w hello standardowa i Premium pamięci podręcznej oferty się dodatkowe toonine o nazwie pamięci podręcznych można skonfigurować w razie potrzeby. |Pamięci podręcznej pamięci podręcznej Redis Azure mają można skonfigurować liczbę baz danych (domyślnie 16), które mogą być używane tooimplement, który przechowuje podobne toonamed funkcji. Aby uzyskać więcej informacji, zobacz [What are Redis databases?](cache-faq.md#what-are-redis-databases) (Co to są bazy danych Redis?) i [Default Redis server configuration](cache-configure.md#default-redis-server-configuration) (Domyślna konfiguracja serwera Redis). |
| Wysoka dostępność |Zapewnia wysoką dostępność dla elementów w pamięci podręcznej hello ofert pamięci podręcznej hello standardowa i Premium. W przypadku utraty powodu niepowodzenia tooa elementów kopii zapasowych hello elementów w pamięci podręcznej hello są nadal dostępne. Zapisuje synchronicznie zostają toohello dodatkowej pamięci podręcznej. |Wysoka dostępność jest dostępna w hello standardowa i Premium pamięci podręcznej oferty, które w konfiguracji podstawowej/repliki dwoma węzłami (parę podstawowy/repliki ma każdego niezależnego fragmentu w pamięci podręcznej Premium). Zapisy toohello repliki są wykonywane asynchronicznie. Aby uzyskać więcej informacji, zobacz [cennik usługi pamięć podręczna Redis Azure](https://azure.microsoft.com/pricing/details/cache/). |
| Powiadomienia |Umożliwia klientom tooreceive asynchroniczne powiadomienia, gdy różnych operacji pamięci podręcznej są dokonywane na nazwanym pamięci podręcznej. |Aplikacje klienckie można użyć pamięci podręcznej Redis pub/sub lub [powiadomienia przestrzeni kluczy](cache-configure.md#keyspace-notifications-advanced-settings) tooachieve podobne toonotifications funkcji. |
| Lokalna pamięć podręczna |Przechowuje kopię obiektów buforowane lokalnie na powitania klienta do bardzo szybkiego dostępu. |Aplikacje klienckie potrzebny tooimplement tę funkcję za pomocą słownika lub podobne struktury danych. |
| Zasady wykluczania |Brak lub LRU. zasady domyślne Hello jest LRU. |Pamięć podręczna Redis Azure obsługuje następujące zasady wykluczania hello: volatile lru, allkeys lru, losowe volatile, allkeys — losowe ttl volatile, noeviction. zasady domyślne Hello jest volatile lru. Aby uzyskać więcej informacji, zobacz [Redis domyślna konfiguracja serwera](cache-configure.md#default-redis-server-configuration). |
| Zasady wygasania |Witaj domyślne zasady wygasania jest bezwzględną i hello domyślny wygaśnięcia interwał wynosi 10 minut. Dostępne są również zasady przedłużanie i Never. |Domyślnie nie wygasają elementów w pamięci podręcznej hello, ale wygaśnięcia można skonfigurować dla poszczególnych zapisu przy użyciu pamięci podręcznej zestawu przeciążenia. Aby uzyskać więcej informacji, zobacz [Dodawanie i pobieranie obiektów w pamięci podręcznej hello](cache-dotnet-how-to-use-azure-redis-cache.md#add-and-retrieve-objects-from-the-cache). |
| Regiony i znakowanie |Regiony są podgrupy dla elementów w pamięci podręcznej. Regiony obsługuje również adnotacji hello elementów pamięci podręcznej z dodatkowe ciągi opisową o nazwie tagów. Regiony obsługuje operacji wyszukiwania tooperform możliwości hello na oznakowanych elementów w tym regionie. Wszystkie elementy w obrębie regionu znajdują się w jednym węźle klastra pamięci podręcznej hello. |Pamięć podręczna Redis składa się z jednego węzła (o ile nie włączono klaster Redis) tak, aby nie stosować koncepcji hello regionów usługi zarządzana pamięć podręczna. Podczas pobierania kluczy, więc opisowe tagi można ją osadzić w hello nazwy klucza i później używane elementy hello tooretrieve redis obsługuje przeszukiwanie i operacje symboli wieloznacznych. Przykład wdrażania rozwiązania znakowania przy użyciu pamięci podręcznej Redis, zobacz [implementacja pamięci podręcznej znakowanie z pamięci podręcznej Redis](http://stackify.com/implementing-cache-tagging-redis/). |
| Serializacja |Zarządzana pamięć podręczna obsługuje NetDataContractSerializer, elementu BinaryFormatter między elementami i hello stosowania niestandardowego serializatorów. Domyślnie Hello jest NetDataContractSerializer. |Przed wprowadzeniem ich do pamięci podręcznej hello, wybór hello serializator hello zapasowej Deweloper aplikacji klienta toohello jest odpowiedzialny za hello obiekty .NET tooserialize powitania klienta aplikacji. Aby uzyskać więcej informacji i przykładowy kod, zobacz [Praca z obiektami .NET w pamięci podręcznej hello](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache). |
| Emulator pamięci podręcznej |Zarządzana pamięć podręczna zawiera emulator lokalnej pamięci podręcznej. |Pamięć podręczna Redis Azure ma emulatora, ale można [uruchamianie kompilacji MSOpenTech hello redis server.exe lokalnie](cache-faq.md#cache-emulator) tooprovide środowisko emulatora. |

## <a name="choose-a-cache-offering"></a>Wybierz ofertę pamięci podręcznej
Pamięć podręczna Redis Azure firmy Microsoft jest dostępna w hello następujące warstwy:

* **Podstawowa** — jeden węzeł. Wiele wielkości too53 GB.
* **Standardowa** — dwa węzły (węzeł podstawowy i węzeł repliki). Wiele wielkości too53 GB. Umowa SLA na poziomie 99,9%.
* **Premium** — dwa węzły podstawowego/repliki o zapasowej odłamków too10. Różne rozmiary od 6 GB too530 GB. Wszystkie funkcje warstwy Standardowej i dodatkowe funkcje, m.in. obsługa [klastra Redis](cache-how-to-premium-clustering.md), [stanu trwałego pamięci podręcznej Redis](cache-how-to-premium-persistence.md) oraz usługi [Azure Virtual Network](cache-how-to-premium-vnet.md). Umowa SLA na poziomie 99,9%.

Poszczególne warstwy różnią się od siebie pod względem funkcji i cen. Witaj funkcje zostały omówione w dalszej części tego przewodnika, a także aby uzyskać więcej informacji o cenach, zobacz [szczegóły cennika pamięci podręcznej](https://azure.microsoft.com/pricing/details/cache/).

Punkt początkowy dla migracji jest rozmiar hello toopick, odpowiadający hello rozmiar pamięci podręcznej usługi zarządzana pamięć podręczna poprzedniej, a następnie skalować w górę lub w dół w zależności od wymagań hello aplikacji. Aby uzyskać więcej wskazówek dotyczących wybierania hello prawo oferty usługi pamięć podręczna Redis Azure, zobacz [jakie oferty pamięć podręczna Redis i rozmiar należy używać?](cache-faq.md#what-redis-cache-offering-and-size-should-i-use).

## <a name="create-a-cache"></a>Tworzenie pamięci podręcznej
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

## <a name="configure-hello-cache-clients"></a>Konfigurowanie klientów pamięci podręcznej hello
Po hello pamięci podręcznej zostało utworzone i skonfigurowane, następnym krokiem hello jest tooremove hello usługi zarządzana pamięć podręczna konfiguracji, a następnie dodaj hello dodać hello konfiguracji pamięci podręcznej Redis Azure oraz odwołań do pamięci podręcznej klienci mogą uzyskiwać dostęp do pamięci podręcznej hello.

* Usuń hello konfiguracji usługi zarządzana pamięć podręczna
* Konfigurowanie klienta pamięci podręcznej przy użyciu hello pakietu NuGet w programie StackExchange.Redis

### <a name="remove-hello-managed-cache-service-configuration"></a>Usuń hello konfiguracji usługi zarządzana pamięć podręczna
Przed powitania klienta aplikacji można skonfigurować dla pamięci podręcznej Redis Azure, hello istniejącą konfigurację usługi zarządzana pamięć podręczna i odwołania do zestawów muszą zostać usunięte przez odinstalowanie pakietu zarządzane NuGet usługi pamięć podręczna hello.

toouninstall hello pakietu zarządzania pamięci podręcznej NuGet usługi kliknij prawym przyciskiem myszy projekt klienta hello w **Eksploratora rozwiązań** i wybierz polecenie **Zarządzaj pakietami NuGet**. Wybierz hello **zainstalowane pakiety** węzła i typu W**indowsAzure.Caching** do hello wyszukiwanie zainstalowane pakiety pole. Wybierz **Windows** **pamięć podręczna Azure** (lub **Windows** **buforowanie Azure** w zależności od wersji hello pakietu NuGet hello), kliknij  **Odinstaluj**, a następnie kliknij przycisk **Zamknij**.

![Odinstaluj pakiet NuGet usługi zarządzana pamięć podręczna Azure](./media/cache-migrate-to-redis/IC757666.jpg)

Odinstalowanie pakietu zarządzania NuGet usługi pamięć podręczna hello usuwa hello usługi zarządzana pamięć podręczna zestawów i wpisy usługi zarządzana pamięć podręczna hello hello app.config lub web.config powitania klienta aplikacji. Ponieważ nie można usunąć niektórych dostosowane ustawienia, podczas odinstalowywania pakietu NuGet hello, otwórz plik web.config lub app.config i upewnij się, że hello następujące elementy są usuwane.

Upewnij się, że hello `dataCacheClients` wpis zostanie usunięty z hello `configSections` elementu. Nie usuwaj całą hello `configSections` element; po prostu usuń hello `dataCacheClients` wpisu, jeśli jest obecny.

```xml
<configSections>
  <!-- Existing sections omitted for clarity. -->
  <section name="dataCacheClients"type="Microsoft.ApplicationServer.Caching.DataCacheClientsSection, Microsoft.ApplicationServer.Caching.Core" allowLocation="true" allowDefinition="Everywhere"/>
</configSections>
```

Upewnij się, że hello `dataCacheClients` sekcji zostanie usunięta. Witaj `dataCacheClients` sekcja będzie toohello podobnie poniższy przykład.

```xml
<dataCacheClients>
  <dataCacheClientname="default">
    <!--toouse hello in-role flavor of Azure Cache, set identifier toobe hello cache cluster role name -->
    <!--toouse hello Azure Managed Cache Service, set identifier toobe hello endpoint of hello cache cluster -->
    <autoDiscoverisEnabled="true"identifier="[Cache role name or Service Endpoint]"/>

    <!--<localCache isEnabled="true" sync="TimeoutBased" objectCount="100000" ttlValue="300" />-->
    <!--Use this section toospecify security settings for connecting tooyour cache. This section is not required if your cache is hosted on a role that is a part of your cloud service. -->
    <!--<securityProperties mode="Message" sslEnabled="true">
      <messageSecurity authorizationInfo="[Authentication Key]" />
    </securityProperties>-->
  </dataCacheClient>
</dataCacheClients>
```

Po usunięciu konfiguracji usługi zarządzana pamięć podręczna hello hello pamięci podręcznej klienta można skonfigurować zgodnie z opisem w następujących sekcji hello.

### <a name="configure-a-cache-client-using-hello-stackexchangeredis-nuget-package"></a>Konfigurowanie klienta pamięci podręcznej przy użyciu hello pakietu NuGet w programie StackExchange.Redis
[!INCLUDE [redis-cache-configure](../../includes/redis-cache-configure-stackexchange-redis-nuget.md)]

## <a name="migrate-managed-cache-service-code"></a>Migrowanie kodu usługi zarządzana pamięć podręczna
Interfejs API Hello hello programie StackExchange.Redis pamięci podręcznej klienta jest podobne toohello usługi pamięć podręczna zarządzane. Ta sekcja zawiera omówienie hello różnic.

### <a name="connect-toohello-cache-using-hello-connectionmultiplexer-class"></a>Połącz toohello pamięci podręcznej za pomocą klasy ConnectionMultiplexer hello
W przypadku usługi zarządzana pamięć podręczna pamięci podręcznej toohello połączenia zostały obsłużone przez hello `DataCacheFactory` i `DataCache` klasy. W pamięci podręcznej Redis Azure, te połączenia są zarządzane przez hello `ConnectionMultiplexer` klasy.

Dodaj następujące hello przy użyciu instrukcji toohello górnej części każdego pliku, z którego mają zostać tooaccess hello pamięci podręcznej.

```c#
using StackExchange.Redis
```

Jeśli tej przestrzeni nazw nie jest rozpoznawane, pamiętaj, że dodano hello pakietu NuGet w programie StackExchange.Redis zgodnie z opisem w [Konfigurowanie klientów pamięci podręcznej hello](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients).

> [!NOTE]
> Należy pamiętać, że w programie StackExchange.Redis powitania klienta wymaga programu .NET Framework 4 lub nowszej.
> 
> 

wystąpienie pamięci podręcznej Redis Azure tooan tooconnect, statyczne hello wywołania `ConnectionMultiplexer.Connect` — metoda i przekaż hello punktu końcowego i klucz. Jednym z podejść toosharing `ConnectionMultiplexer` toohave statycznej właściwości, która zwraca wystąpienie połączonych toohello podobnie poniższy przykład jest wystąpienie w aplikacji. Zapewnia to tooinitialize sposób zapewniający obsługę wielowątkowości tylko jedna połączona `ConnectionMultiplexer` wystąpienia. W tym przykładzie `abortConnect` jest zestaw toofalse, co oznacza, że wywołanie hello powiedzie się, nawet jeśli nie zostanie nawiązane połączenie pamięci podręcznej toohello. Jedna funkcja klucza `ConnectionMultiplexer` jest, że go automatycznie przywróci łączności toohello w pamięci podręcznej po hello problem z siecią lub inne przyczyny zostaną rozwiązane.

```c#
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
```

Witaj punktu końcowego pamięci podręcznej, kluczy i portów można uzyskać hello **pamięci podręcznej Redis** bloku dla swojego wystąpienia w pamięci podręcznej. Aby uzyskać więcej informacji, zobacz [właściwości pamięci podręcznej Redis](cache-configure.md#properties).

Po nawiązaniu połączenia hello zwrócić bazy danych pamięci podręcznej Redis toohello odwołania przez wywołanie hello `ConnectionMultiplexer.GetDatabase` metody. zwróciła obiekt Hello hello `GetDatabase` metody jest obiektem przekazujące lekkie i nie wymaga toobe przechowywane.

```c#
IDatabase cache = Connection.GetDatabase();

// Perform cache operations using hello cache object...
// Simple put of integral data types into hello cache
cache.StringSet("key1", "value");
cache.StringSet("key2", 25);

// Simple get of data types from hello cache
string key1 = cache.StringGet("key1");
int key2 = (int)cache.StringGet("key2");
```

Witaj programie StackExchange.Redis klient używa hello `RedisKey` i `RedisValue` typy do uzyskiwania dostępu i przechowywania w pamięci podręcznej hello elementów. Te typy mapowania na najbardziej pierwotne typy język, w tym ciągu, a często nie są używane bezpośrednio. Redis ciągów hello najprostsze typu wartości pamięci podręcznej Redis i mogą zawierać wiele typów danych, w tym serializacji strumienie binarne, i gdy nie można używać typu hello bezpośrednio, będzie używać metod, które zawierają `String` w nazwie hello. W przypadku najbardziej pierwotnych typów danych przechowywania i pobierania elementów z pamięci podręcznej hello przy użyciu hello `StringSet` i `StringGet` metod, o ile nie są przechowywane w pamięci podręcznej hello kolekcje lub inne typy danych Redis. 

`StringSet`i `StringGet` są bardzo podobne toohello usługi pamięć podręczna zarządzanej `Put` i `Get` metody z jednym z głównych różnica, że przed ustawić i pobierania obiektu platformy .NET do pamięci podręcznej hello użytkownik musi serializować ją najpierw. 

Podczas wywoływania metody `StringGet`, jeśli obiekt hello istnieje, jest zwracany i jeśli nie, zwracana jest wartość null. W takim przypadku można pobrać wartości hello ze źródła danych odpowiednie hello i zapisz go w pamięci podręcznej hello na potrzeby późniejszego wykorzystania. Jest to nazywane hello Zarezerwuj pamięć podręczna wzorca.

wygaśnięcie hello toospecify elementu w pamięci podręcznej hello, użyj hello `TimeSpan` parametr `StringSet`.

```c#
cache.StringSet("key1", "value1", TimeSpan.FromMinutes(90));
```

Pamięć podręczna Redis Azure może współpracować z obiektów platformy .NET, a także typy pierwotne danych, ale przed obiektu .NET mogą być buforowane musi być serializowany. To jest odpowiedzialny za hello Deweloper aplikacji hello. Zapewnia elastyczność developer hello hello wyborze hello serializatora. Aby uzyskać więcej informacji i przykładowy kod, zobacz [Praca z obiektami .NET w pamięci podręcznej hello](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache).

## <a name="migrate-aspnet-session-state-and-output-caching-tooazure-redis-cache"></a>Migracja stanu sesji ASP.NET i tooAzure pamięci podręcznej Redis do buforowania danych wyjściowych
Pamięć podręczna Redis Azure ma dostawców dla stanu sesji ASP.NET i buforowania danych wyjściowych strony. toomigrate aplikacji, która używa wersji usługi zarządzana pamięć podręczna hello tych dostawców, najpierw usuń hello istniejące sekcje z pliku web.config, a następnie skonfiguruj wersji pamięci podręcznej Redis Azure hello hello dostawców. Aby uzyskać instrukcje dotyczące używania hello dostawców ASP.NET pamięci podręcznej Redis Azure, zobacz [dostawcę stanu sesji ASP.NET dla pamięci podręcznej Redis Azure](cache-aspnet-session-state-provider.md) i [dostawcy wyjściowej pamięci podręcznej programu ASP.NET dla pamięci podręcznej Redis Azure](cache-aspnet-output-cache-provider.md).

## <a name="next-steps"></a>Następne kroki
Eksploruj hello [dokumentacji pamięć podręczna Redis Azure](https://azure.microsoft.com/documentation/services/cache/) samouczki, przykłady, klipów wideo i.

