---
title: "często zadawane pytania dotyczące pamięci podręcznej Redis aaaAzure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, że hello odpowiedzi na pytania toocommon, wzorców i najlepszych rozwiązań dla pamięci podręcznej Redis Azure"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: c2c52b7d-b2d1-433a-b635-c20180e5cab2
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: sdanie
ms.openlocfilehash: 2c6ed2f65f755bd08f04857b7af31f520cf4f158
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-redis-cache-faq"></a>Azure Redis Cache — często zadawane pytania
Dowiedz się, że hello odpowiedzi na pytania toocommon wzorców i najlepszych rozwiązań dla pamięci podręcznej Redis Azure.

## <a name="what-if-my-question-isnt-answered-here"></a>Co zrobić, jeśli mojego pytania nie ma odpowiedzi w tym miejscu?
Jeśli Twoje pytanie nie ma na liście w tym miejscu, Daj nam znać, a pomożemy Ci znaleźć odpowiedź.

* Można wysłać zapytanie do hello komentarze na końcu hello tych często zadawanych PYTAŃ i kontaktowaniu się z team pamięć podręczna Azure hello i innymi członkami społeczności informacje w tym artykule.
* tooreach większej liczby osób, należy wysłać zapytanie na powitania [Forum MSDN pamięci podręcznej Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=azurecache) i kontaktowaniu się z team pamięć podręczna Azure hello i innych członków społeczności hello.
* Jeśli chcesz toomake żądania funkcji, można przesłać swoich żądań i pomysłów za[głos użytkownika pamięci podręcznej Redis Azure](https://feedback.azure.com/forums/169382-cache).
* Możesz również wysłać wiadomość e-mail na toous [opinii zewnętrznych pamięci podręcznej Azure](mailto:azurecache@microsoft.com).

## <a name="azure-redis-cache-basics"></a>Podstawy pamięci podręcznej Redis Azure
Hello — często zadawane pytania w tej sekcji opisano niektóre hello podstawy pamięć podręczna Redis Azure.

* [Co to jest usługa Azure Redis Cache?](#what-is-azure-redis-cache)
* [Jak można zacząć korzystać z pamięci podręcznej Redis Azure?](#how-can-i-get-started-with-azure-redis-cache)

Witaj poniższe często zadawane pytania dotyczą podstawowych pojęć i pytania dotyczące pamięci podręcznej Redis Azure i są odbierane w jednym z hello pozostałe sekcje — często zadawane pytania.

* [Której oferty i jakiego rozmiaru usługi Redis Cache mam użyć?](#what-redis-cache-offering-and-size-should-i-use)
* [Jakie klientów pamięci podręcznej Redis można użyć?](#what-redis-cache-clients-can-i-use)
* [Czy istnieje lokalne emulatora dla pamięci podręcznej Redis Azure?](#is-there-a-local-emulator-for-azure-redis-cache)
* [Jak monitorować hello kondycji i wydajności Moje pamięci podręcznej](#how-do-i-monitor-the-health-and-performance-of-my-cache)

## <a name="planning-faqs"></a>Często zadawane pytania dotyczące planowania
* [Której oferty i jakiego rozmiaru usługi Redis Cache mam użyć?](#what-redis-cache-offering-and-size-should-i-use)
* [Wydajność pamięci podręcznej Redis Azure](#azure-redis-cache-performance)
* [W jakim regionie należy znaleźć Moje pamięci podręcznej?](#in-what-region-should-i-locate-my-cache)
* [Jak m rozliczane dla pamięci podręcznej Redis Azure?](#how-am-i-billed-for-azure-redis-cache)
* [Z chmury Azure dla instytucji rządowych, chmury Azure Chin lub Microsoft Azure Niemcy można używać usługi pamięć podręczna Redis Azure?](#can-i-use-azure-redis-cache-with-azure-government-cloud-azure-china-cloud-or-microsoft-azure-germany)

## <a name="development-faqs"></a>Programowanie — często zadawane pytania
* [Co zrobić opcje konfiguracji w programie StackExchange.Redis hello?](#what-do-the-stackexchangeredis-configuration-options-do)
* [Jakie klientów pamięci podręcznej Redis można użyć?](#what-redis-cache-clients-can-i-use)
* [Czy istnieje lokalne emulatora dla pamięci podręcznej Redis Azure?](#is-there-a-local-emulator-for-azure-redis-cache)
* [Jak uruchomić polecenia Redis?](#how-can-i-run-redis-commands)
* [Dlaczego nie pamięci podręcznej Redis Azure ma MSDN dotyczące biblioteki klas podobnie jak niektóre hello innymi usługami Azure?](#why-doesnt-azure-redis-cache-have-an-msdn-class-library-reference-like-some-of-the-other-azure-services)
* [Pamięć podręczna Redis Azure można używać jako pamięci podręcznej sesji PHP?](#can-i-use-azure-redis-cache-as-a-php-session-cache)
* [Co to są Redis baz danych?](#what-are-redis-databases)

## <a name="security-faqs"></a>Często zadawane pytania dotyczące zabezpieczeń
* [Jeśli włączenie portu bez protokołu SSL hello podłączania tooRedis?](#when-should-i-enable-the-non-ssl-port-for-connecting-to-redis)

## <a name="production-faqs"></a>Produkcja — często zadawane pytania
* [Jakie są najlepsze rozwiązania produkcyjnym?](#what-are-some-production-best-practices)
* [Jakie są kwestie hello za pomocą wspólnego poleceń Redis?](#what-are-some-of-the-considerations-when-using-common-redis-commands)
* [Jak testu wydajności i przetestować hello wydajności Moje pamięci podręcznej?](#how-can-i-benchmark-and-test-the-performance-of-my-cache)
* [Ważne informacje dotyczące wzrostu puli wątków](#important-details-about-threadpool-growth)
* [Włączyć tooget serwera wykazu Globalnego więcej przepływności na powitania klienta za pomocą programie StackExchange.Redis](#enable-server-gc-to-get-more-throughput-on-the-client-when-using-stackexchangeredis)
* [Zagadnienia dotyczące wydajności wokół połączeń](#performance-considerations-around-connections)

## <a name="monitoring-and-troubleshooting-faqs"></a>Monitorowanie i rozwiązywanie problemów — często zadawane pytania
często zadawane pytania dotyczące Hello w tej sekcji obejmują typowe monitorowania i pytania dotyczące rozwiązywania problemów. Aby uzyskać więcej informacji dotyczących monitorowania i rozwiązywania problemów z wystąpienia pamięci podręcznej Redis Azure, zobacz [jak toomonitor Azure pamięci podręcznej Redis](cache-how-to-monitor.md) i [jak tootroubleshoot Azure pamięci podręcznej Redis](cache-how-to-troubleshoot.md).

* [Jak monitorować hello kondycji i wydajności Moje pamięci podręcznej](#how-do-i-monitor-the-health-and-performance-of-my-cache)
* [Dlaczego widzę limitów czasu?](#why-am-i-seeing-timeouts)
* [Dlaczego moja klient został odłączony od hello pamięci podręcznej?](#why-was-my-client-disconnected-from-the-cache)

## <a name="prior-cache-offering-faqs"></a>Wcześniejsze oferty pamięci podręcznej często zadawane pytania
* [Które oferty Azure w pamięci podręcznej jest dla mnie odpowiednia?](#which-azure-cache-offering-is-right-for-me)

### <a name="what-is-azure-redis-cache"></a>Co to jest usługa Azure Redis Cache?
Pamięć podręczna Redis Azure jest oparta na powitania popularnych open source [pamięci podręcznej Redis](http://redis.io). Daje dostęp tooa bezpiecznego, dedykowane pamięć podręczna Redis, zarządzane przez firmę Microsoft i jest dostępny z poziomu dowolnej aplikacji w obrębie platformy Azure. Aby uzyskać bardziej szczegółowe informacje, zobacz hello [pamięć podręczna Redis Azure](https://azure.microsoft.com/services/cache/) stronę produktu w witrynie Azure.com.

### <a name="how-can-i-get-started-with-azure-redis-cache"></a>Jak można zacząć korzystać z pamięci podręcznej Redis Azure?
Istnieje kilka metod, które możesz rozpocząć pracę z pamięci podręcznej Redis Azure.

* Można wyewidencjonować jedną z naszymi samouczkami, aby uzyskać [.NET](cache-dotnet-how-to-use-azure-redis-cache.md), [ASP.NET](cache-web-app-howto.md), [Java](cache-java-get-started.md), [Node.js](cache-nodejs-get-started.md), i [Python](cache-python-get-started.md).
* Możesz obserwować [jak tooBuild wysokiej wydajności aplikacji za pomocą programu Microsoft Azure pamięci podręcznej Redis](https://azure.microsoft.com/documentation/videos/how-to-build-high-performance-apps-using-microsoft-azure-cache/).
* Można wyewidencjonować powitania klienta dokumentacji klientom Witaj zgodnie z językiem programowania hello toosee Twojego projektu, jak toouse Redis. Istnieje wielu klientów pamięci podręcznej Redis, które mogą być używane z pamięci podręcznej Redis Azure. Lista klientów pamięci podręcznej Redis, zobacz [http://redis.io/clients](http://redis.io/clients).

Jeśli nie masz jeszcze konta platformy Azure, możesz:

* [Utworzyć bezpłatne konto platformy Azure ](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero). Otrzymasz kredyt, które mogą być używane tootry limit płatnej usług platformy Azure. Nawet po wyczerpaniu kredytu hello, można zachować hello konto i korzystać z bezpłatnych usług platformy Azure i funkcji.
* [Aktywować korzyści subskrybenta programu Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=redis_cache_hero). W ramach subskrypcji MSDN co miesiąc otrzymasz środki, które możesz przeznaczyć na płatne usługi platformy Azure.

<a name="cache-size"></a>

### <a name="what-redis-cache-offering-and-size-should-i-use"></a>Jakie oferty i rozmiary pamięci podręcznej Redis mam wybrać?
Każde rozwiązanie pamięci podręcznej Redis Azure zapewnia różne poziomy **rozmiar**, **przepustowości**, **wysokiej dostępności**, i **SLA** opcje.

Witaj poniżej przedstawiono zagadnienia dotyczące wybierania oferty pamięci podręcznej.

* **Pamięć**: hello warstwy Basic i Standard oferują 250 MB – 53 GB. Witaj warstwy Premium zapewnia too530 GB. Aby uzyskać więcej informacji, zobacz [cennik usługi Azure Redis pamięci podręcznej](https://azure.microsoft.com/pricing/details/cache/).
* **Wydajność sieci**: Jeśli masz obciążenia, która wymaga wysokiej przepływności hello warstwy Premium oferuje więcej przepustowości w porównaniu tooStandard lub Basic. Również w każdej warstwie większy rozmiar pamięci podręcznej ma więcej przepustowości z powodu hello podstawowej maszyny Wirtualnej, który obsługuje hello pamięci podręcznej. Zobacz hello [następujących tabeli](#cache-performance) Aby uzyskać więcej informacji.
* **Przepływność**: hello warstwy Premium oferuje hello maksymalna dostępna przepustowość. Jeśli klienta lub serwera pamięci podręcznej hello osiągnie hello limity przepustowości, może zostać wyświetlony przekroczeń limitu czasu na powitania po stronie klienta. Aby uzyskać więcej informacji zobacz hello w poniższej tabeli.
* **Wysoka dostępność/SLA**: pamięć podręczna Redis Azure gwarantuje, że pamięć podręczna Standard/Premium jest dostępna co najmniej 99,9% czasu hello. Zobacz toolearn więcej informacji na temat naszych SLA [cennik usługi Azure Redis pamięci podręcznej](https://azure.microsoft.com/support/legal/sla/cache/v1_0/). Hello SLA obejmuje tylko punkty końcowe pamięci podręcznej toohello łączności. Witaj SLA nie obejmuje ochrony przed utratą danych. Zalecamy używanie funkcji trwałości danych pamięci podręcznej Redis hello w hello Premium warstwy tooincrease odporności przed utratą danych.
* **Trwałość danych redis**: hello warstwy Premium pozwala toopersist hello pamięci podręcznej danych na koncie magazynu Azure. W pamięci podręcznej Basic/Standard wszystkie dane hello są przechowywane tylko w pamięci. W przypadku podstawowej problemów infrastruktury może być ryzyko utraty danych. Zalecamy używanie funkcji trwałości danych pamięci podręcznej Redis hello w hello Premium warstwy tooincrease odporności przed utratą danych. Pamięć podręczna Redis Azure oferuje RDB i AOF (wkrótce) opcje w trwałość Redis. Aby uzyskać więcej informacji, zobacz [jak tooconfigure trwałości dla podręczna Redis Azure Premium](cache-how-to-premium-persistence.md).
* **Klaster redis**: toocreate buforuje większych niż 53 GB lub tooshard danych między wieloma węzłami Redis, możesz użyć Redis klastrowania, która jest dostępna w warstwie Premium hello. Każdy węzeł składa się z pary pamięć podręczna podstawowy/repliki wysokiej dostępności. Aby uzyskać więcej informacji, zobacz [jak tooconfigure klastrowania podręczna Redis Azure Premium](cache-how-to-premium-clustering.md).
* **Zwiększonych zabezpieczeń i sieci izolacji**: wdrożenie wirtualne sieci Azure (VNET) zapewnia większe bezpieczeństwo i izolację dla pamięci podręcznej Redis Azure, jak również podsieci, zasad kontroli dostępu i inne funkcje toofurther ograniczyć dostęp. Aby uzyskać więcej informacji, zobacz [jak tooconfigure sieci wirtualnej obsługę podręczna Redis Azure Premium](cache-how-to-premium-vnet.md).
* **Konfigurowanie pamięci podręcznej Redis**: hello Standard i Premium warstw pamięci podręcznej Redis można skonfigurować dla powiadomienia przestrzeni kluczy.
* **Maksymalna liczba połączeń klienckich**: hello warstwy Premium oferuje hello maksymalną liczbę klientów, którzy mogą łączyć się tooRedis, z większej liczby połączeń dla większy rozmiar pamięci podręcznej. Aby uzyskać więcej informacji, zobacz [cennik usługi pamięć podręczna Redis Azure](https://azure.microsoft.com/pricing/details/cache/).
* **Dedykowane Core dla serwera Redis**: W warstwie Premium hello, różnej wielkości pamięci podręcznej ma dedykowany core Redis. W warstwach Basic/Standard hello hello rozmiar C1 i powyżej ma dedykowany core dla serwera Redis.
* **Redis jest jednowątkowy** mających więcej niż dwa rdzenie nie zapewnia dodatkowych korzyści za pośrednictwem o tylko dwa rdzenie, ale większych rozmiarów maszyn wirtualnych zwykle mają więcej przepustowości niż mniejsze. Jeśli klienta lub serwera pamięci podręcznej hello osiągnie hello limity przepustowości, zostanie wyświetlony przekroczeń limitu czasu na powitania po stronie klienta.
* **Ulepszenia wydajności**: pamięci podręcznych w warstwie Premium hello są wdrażane na sprzęcie, który ma szybkich procesorów, zapewniając lepszą wydajność w porównaniu toohello Basic lub Standard warstwy. Pamięci podręczne warstwy Premium ma wyższą przepływność i dolnym opóźnienia.

<a name="cache-performance"></a>

### <a name="azure-redis-cache-performance"></a>Wydajność pamięci podręcznej Redis Azure
Hello poniższej tabeli przedstawiono wartości maksymalnej przepustowości hello obserwowanych podczas badania różnych rozmiarach Standard i Premium buforuje przy użyciu `redis-benchmark.exe` z maszyn wirtualnych Iaas względem punktu końcowego pamięci podręcznej Redis Azure hello. 

>[!NOTE] 
>Te wartości nie ma gwarancji i ma nie umowy SLA dla tych numerów, ale powinien być typowych. Powinny zostać załadowane test własnych aplikacji toodetermine hello prawo rozmiar pamięci podręcznej dla aplikacji.
>
>

Z tej tabeli firma Microsoft może wykonywać Rysowanie hello następujących wniosków:

* Przepływność dla pamięci podręcznych hello, będące powitalne sam rozmiar jest większa w hello warstwy Premium toohello porównaniu warstwy standardowa. Na przykład o 6 GB pamięci podręcznej, przepływności P1 jest RPS 180 000 jako porównaniu too49, 000 dla C3.
* Z pamięci podręcznej Redis klaster przepływności zwiększa liniowo jako zwiększyć liczbę hello odłamków (węzłów) w klastrze hello. Na przykład, jeśli tworzysz klaster P4 10 odłamków, następnie hello dostępne przepływność wynosi 400 000 * 10 = 4 miliony RPS.
* Przepływność o większych rozmiarach klucza jest większa w warstwie Premium hello porównaniu toohello warstwy standardowa.

| Warstwa cenowa | Rozmiar | Rdzenie procesora CPU | Dostępna przepustowość | Rozmiar wartości 1 KB |
| --- | --- | --- | --- | --- |
| **Rozmiary standardowe pamięci podręcznej** | | |**Megabity na sekundę (Mb/s) / MB na sekundę (MB/s)** |**Liczba żądań na sekundę (RPS)** |
| C0 |250 MB |Udostępniona |5 / 0.625 |600 |
| C1 |1 GB |1 |100 / 12.5 |12,200 |
| C2 |2,5 GB |2 |200 / 25 |24,000 |
| C3 |6 GB |4 |400 / 50 |49,000 |
| C4 |13 GB |2 |500 / 62.5 |61,000 |
| C5 |26 GB |4 |1,000 / 125 |115,000 |
| C6 |53 GB |8 |2,000 / 250 |150,000 |
| **Rozmiar pamięci podręcznej — wersja Premium** | |**Rdzenie procesora CPU na niezależnego fragmentu** | **Megabity na sekundę (Mb/s) / MB na sekundę (MB/s)** |**Liczba żądań na sekundę (RPS) na niezależnego fragmentu** |
| P1 |6 GB |2 |1,500 / 187.5 |180,000 |
| P2 |13 GB |4 |3,000 / 375 |360,000 |
| P3 |26 GB |4 |3,000 / 375 |360,000 |
| P4 |53 GB |8 |6,000 / 750 |400 000 |

Aby uzyskać instrukcje dotyczące pobierania hello Redis narzędzi, takich jak `redis-benchmark.exe`, zobacz hello [jak uruchomić polecenia Redis?](#cache-commands) sekcji.

<a name="cache-region"></a>

### <a name="in-what-region-should-i-locate-my-cache"></a>W jakim regionie należy znaleźć Moje pamięci podręcznej?
Aby uzyskać najlepszą wydajność i najniższym opóźnieniu zlokalizować pamięć podręczna Redis Azure w hello tym samym regionie co aplikacja klienta pamięci podręcznej.

<a name="cache-billing"></a>

### <a name="how-am-i-billed-for-azure-redis-cache"></a>Jak m rozliczane dla pamięci podręcznej Redis Azure?
Cennik usługi pamięć podręczna Redis Azure jest [tutaj](https://azure.microsoft.com/pricing/details/cache/). Cennik Hello wymieniono ceny za godzinę. Pamięci podręczne są rozliczane na podstawie na minutę od czasu hello, utworzenia pamięci podręcznej hello czasu hello pamięci podręcznej zostanie usunięty. Nie ma żadnych opcji dla zatrzymanie lub wstrzymanie rozliczeń hello pamięci podręcznej.

### <a name="can-i-use-azure-redis-cache-with-azure-government-cloud-azure-china-cloud-or-microsoft-azure-germany"></a>Z chmury Azure dla instytucji rządowych, chmury Azure Chin lub Microsoft Azure Niemcy można używać usługi pamięć podręczna Redis Azure?
Tak, pamięć podręczna Redis Azure jest dostępna w chmurze platformy Azure dla instytucji rządowych, chmury Azure Chin i Microsoft platformy Azure w Niemczech. adresy URL Hello dostęp i zarządzanie pamięcią podręczną Redis Azure różnią się w tych chmurach w porównaniu z chmury publicznej Azure. 

| Chmura   | Sufiks DNS dla pamięci podręcznej Redis            |
|---------|---------------------------------|
| Publiczne  | *. redis.cache.windows.net       |
| Rząd USA  | *. redis.cache.usgovcloudapi.net |
| Niemcy | *. redis.cache.cloudapi.de       |
| Chiny   | *. redis.cache.chinacloudapi.cn  |

Aby uzyskać więcej informacji na uwagi dotyczące korzystania z innych chmur pamięć podręczna Redis Azure Zobacz hello następującego łącza.

- [Baz danych Azure dla instytucji rządowych — pamięć podręczna Azure Redis](../azure-government/documentation-government-services-database.md#azure-redis-cache)
- [Chmury Azure Chin — pamięć podręczna Azure Redis](https://www.azure.cn/documentation/services/redis-cache/)
- [Niemcy platformy Microsoft Azure](https://azure.microsoft.com/overview/clouds/germany/)

Uzyskać informacji o użyciu pamięci podręcznej Redis Azure przy użyciu programu PowerShell w chmurze platformy Azure dla instytucji rządowych, chmury Azure Chin i Microsoft Azure Niemczech, zobacz [jak tooconnect tooother chmur — pamięć podręczna Redis Azure PowerShell](cache-howto-manage-redis-cache-powershell.md#how-to-connect-to-other-clouds).

<a name="cache-configuration"></a>

### <a name="what-do-hello-stackexchangeredis-configuration-options-do"></a>Co zrobić opcje konfiguracji w programie StackExchange.Redis hello?
Programie StackExchange.Redis ma wiele opcji. Ta sekcja zawiera informacje o niektórych typowych ustawień hello. Aby uzyskać szczegółowe informacje o programie StackExchange.Redis opcjach, zobacz [konfiguracji w programie StackExchange.Redis](https://stackexchange.github.io/StackExchange.Redis/Configuration).

| ConfigurationOptions | Opis | Zalecenie |
| --- | --- | --- |
| AbortOnConnectFail |Po ustawieniu tootrue, nie nawiąże połączenia powitania po awarii sieci. |Ustaw toofalse i umożliwić programie StackExchange.Redis automatycznie ponownie. |
| ConnectRetry |Witaj liczba prób połączenia toorepeat podczas początkowego połączenia. |Zobacz hello następujące wskazówki. |
| ConnectTimeout |Limit czasu w ms na operacje connect. |Zobacz hello następujące wskazówki. |

Zazwyczaj domyślne wartości hello powitania klienta są wystarczające. Można dostosować opcje hello w oparciu o obciążenie.

* **Ponowne próby**
  * ConnectRetry i ConnectTimeout ogólne wskazówki hello jest toofail szybkiego i ponów próbę. W tych wskazówkach opiera się na obciążenie i ilość czasu na średni go przyjmuje dla Twojego tooissue klienta polecenie Redis i odpowiedzi.
  * Let programie StackExchange.Redis automatycznie ponownie zestawione, zamiast sprawdzanie stanu połączenia i ponowne łączenie samodzielnie. **Unikaj używania właściwości ConnectionMultiplexer.IsConnected hello**.
  * Snowballing — czasami może wystąpić problem, gdzie są ponawianie próby i hello ponowi próbę snowball i nigdy nie przywraca. W przypadku snowballing, należy rozważyć przy użyciu algorytmu ponawiania wykładniczego wycofywania, zgodnie z opisem w [ponów ogólne wskazówki](../best-practices-retry-general.md) opublikowane przez grupę Microsoft Patterns & rozwiązań hello.
* **Wartości limitu czasu**
  * Należy wziąć pod uwagę obciążenie i ustaw wartości hello odpowiednio. Jeśli przechowujesz wartości duża wartość hello limitu czasu tooa wyższy.
  * Ustaw `AbortOnConnectFail` toofalse i pozwolić na programie StackExchange.Redis ponownie dla Ciebie.
  * Używać jednego wystąpienia ConnectionMultiplexer dla aplikacji hello. Można użyć toocreate LazyConnection pojedyncze wystąpienie, które jest zwracana przez właściwość połączenia, jak pokazano w [połączyć toohello pamięci podręcznej za pomocą klasy ConnectionMultiplexer hello](cache-dotnet-how-to-use-azure-redis-cache.md#connect-to-the-cache).
  * Zestaw hello `ConnectionMultiplexer.ClientName` właściwości tooan wystąpienia unikatowa nazwa aplikacji w celach diagnostycznych.
  * Używanych jest wiele `ConnectionMultiplexer` wystąpień dla niestandardowych obciążeń.
      * Jeśli masz różne obciążenia w aplikacji, można wykonać tego modelu. Na przykład:
      * Może mieć jeden multiplekser dotyczące postępowania w przypadku dużych kluczy.
      * Może mieć jeden multiplekser dotyczące postępowania z kluczami mała.
      * Można ustawić różne wartości limitów czasu połączenia i Logika ponawiania próby dla każdego ConnectionMultiplexer, którego używasz.
      * Zestaw hello `ClientName` właściwości każdego multiplekser toohelp Diagnostyka.
      * W tych wskazówkach może spowodować opóźnienia, uproszczone toomore na `ConnectionMultiplexer`.

### <a name="what-redis-cache-clients-can-i-use"></a>Jakie klientów pamięci podręcznej Redis można użyć?
Jedną z najważniejszych hello o Redis zakłada, że wielu klientów, obsługa wielu języków programowania inny. Aby uzyskać bieżącą listę klientów, zobacz [Redis klientów](http://redis.io/clients). Samouczki, które obejmują kilka różnych języków i klientów, zobacz [jak toouse Azure pamięci podręcznej Redis](cache-dotnet-how-to-use-azure-redis-cache.md) i kliknij przycisk hello żądany język z hello przełącznik języka u góry hello hello artykułu.

[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

<a name="cache-emulator"></a>

### <a name="is-there-a-local-emulator-for-azure-redis-cache"></a>Czy istnieje lokalne emulatora dla pamięci podręcznej Redis Azure?
Nie jest nie emulator lokalnej pamięci podręcznej Redis Azure, ale wersja MSOpenTech hello redis server.exe można uruchomić z hello [Redis narzędzia wiersza polecenia](https://github.com/MSOpenTech/redis/releases/) na lokalnym komputerze, a następnie połącz tooget tooit podobne środowisko tooa lokalnej pamięci podręcznej Emulator, jak pokazano w hello poniższy przykład:

    private static Lazy<ConnectionMultiplexer>
          lazyConnection = new Lazy<ConnectionMultiplexer>
        (() =>
        {
            // Connect tooa locally running instance of Redis toosimulate a local cache emulator experience.
            return ConnectionMultiplexer.Connect("127.0.0.1:6379");
        });

        public static ConnectionMultiplexer Connection
        {
            get
            {
                return lazyConnection.Value;
            }
        }


Opcjonalnie można skonfigurować [redis.conf](http://redis.io/topics/config) toomore pliku ściśle odpowiadające hello [domyślne ustawienia pamięci podręcznej](cache-configure.md#default-redis-server-configuration) dla Twojego online pamięć podręczna Redis Azure w razie potrzeby.

<a name="cache-commands"></a>

### <a name="how-can-i-run-redis-commands"></a>Jak uruchomić polecenia Redis?
Można użyć dowolnego z poleceń hello wymienionych w [Redis polecenia](http://redis.io/commands#) z wyjątkiem hello poleceń w [polecenia nie są obsługiwane w pamięci podręcznej Redis Azure Redis](cache-configure.md#redis-commands-not-supported-in-azure-redis-cache). Masz kilka opcji toorun Redis poleceń.

* Jeśli masz pamięci podręcznej Standard lub Premium, możesz uruchamiać polecenia Redis przy użyciu hello [Redis konsoli](cache-configure.md#redis-console). Konsola Redis Hello zapewnia toorun bezpieczny sposób polecenia Redis w portalu Azure hello.
* Umożliwia także narzędzi wiersza polecenia hello Redis. toouse, wykonaj hello następujące kroki:
* Pobierz hello [Redis narzędzia wiersza polecenia](https://github.com/MSOpenTech/redis/releases/).
* Połącz przy użyciu pamięci podręcznej toohello `redis-cli.exe`. Przekazywanie hello punkt końcowy za pomocą przełącznika -h hello i hello klucza za pomocą pokazane na powitania poniższy przykład:
* `redis-cli -h <your cache="" name="">
  .redis.cache.windows.net -a <key>
  `

> [!NOTE]
> Witaj narzędzia wiersza polecenia Redis nie działa z hello SSL port, ale można użyć narzędzia, takie jak `stunnel` toosecurely połącz port SSL toohello narzędzia hello wykonując instrukcje hello z hello [Announcing ASP.NET dostawcę stanu sesji dla Wersja zapoznawcza redis](http://blogs.msdn.com/b/webdev/archive/2014/05/12/announcing-asp-net-session-state-provider-for-redis-preview-release.aspx) wpis w blogu.
>
>

<a name="cache-reference"></a>

### <a name="why-doesnt-azure-redis-cache-have-an-msdn-class-library-reference-like-some-of-hello-other-azure-services"></a>Dlaczego nie pamięci podręcznej Redis Azure ma MSDN dotyczące biblioteki klas podobnie jak niektóre hello innymi usługami Azure?
Pamięć podręczna Redis Azure firmy Microsoft jest oparta na powitania popularnych typu open source pamięci podręcznej Redis i są dostępne dla różnych typów [Redis klientów](http://redis.io/clients) dla wielu języków programowania. Każdy klient ma własnego interfejsu API czy sprawia, że wywołuje, używając wystąpienia pamięci podręcznej Redis toohello [Redis polecenia](http://redis.io/commands).

Dlatego różni się każdego klienta, nie nie jedno odwołanie scentralizowane klasy w witrynie MSDN, i każdy klient przechowuje własnej dokumentacji. Ponadto toohello odwołania dokumentacji, istnieje kilka samouczki przedstawiający sposób uruchamiania tooget z pamięci podręcznej Redis Azure za pomocą różnych języków i klientów pamięci podręcznej. Zobacz te samouczki tooaccess [jak toouse Azure pamięci podręcznej Redis](cache-dotnet-how-to-use-azure-redis-cache.md) i kliknij przycisk hello żądany język z hello przełącznik języka u góry hello hello artykułu.

### <a name="can-i-use-azure-redis-cache-as-a-php-session-cache"></a>Pamięć podręczna Redis Azure można używać jako pamięci podręcznej sesji PHP?
Tak, toouse pamięci podręcznej Redis Azure jako pamięci podręcznej sesji PHP, określ hello wystąpienia pamięci podręcznej Redis Azure tooyour ciągu połączenia w `session.save_path`.

> [!IMPORTANT]
> Przy użyciu pamięci podręcznej Redis Azure w pamięci podręcznej sesji PHP, muszą być adres URL kodowania hello zabezpieczeń kluczy używanych tooconnect toohello pamięci podręcznej, jak pokazano w hello poniższy przykład:
>
> `session.save_path = "tcp://mycache.redis.cache.windows.net:6379?auth=<url encoded primary or secondary key here>";`
>
> Jeśli klucz hello nie jest kodowany adres URL, może zostać wyświetlony wyjątek z następującym komunikatem, takich jak:`Failed tooparse session.save_path`
>
>

Aby uzyskać więcej informacji o użyciu pamięci podręcznej Redis jako pamięci podręcznej sesji PHP z klientem PhpRedis hello, zobacz [programu obsługi PHP sesji](https://github.com/phpredis/phpredis#php-session-handler).

### <a name="what-are-redis-databases"></a>Co to są Redis baz danych?

Bazy danych redis to logiczne rozdzielenie danych w ramach hello tego samego wystąpienia pamięci podręcznej Redis. pamięć podręczna Hello jest współużytkowana przez wszystkie hello bazy danych i zmniejszenie zużycia pamięci Rzeczywiste danego bazy danych zależy od hello kluczy/wartości przechowywane w bazie danych. Na przykład pamięć podręczną C6 ma 53 GB pamięci. Można wybrać tooput wszystkie 53 GB na jedną bazę danych lub Podziel między wieloma bazami danych. 

> [!NOTE]
> Korzystając z włączoną funkcją klastrowania podręczna Redis Azure Premium, tylko bazy danych 0 jest dostępna. To ograniczenie wewnętrzne ograniczenie pamięci podręcznej Redis i nie jest określone tooAzure pamięci podręcznej Redis. Aby uzyskać więcej informacji, zobacz [należy toomake wszelkie zmiany toomy klienta aplikacji toouse klastra?](cache-how-to-premium-clustering.md#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering)
> 
> 


<a name="cache-ssl"></a>

### <a name="when-should-i-enable-hello-non-ssl-port-for-connecting-tooredis"></a>Jeśli włączenie portu bez protokołu SSL hello podłączania tooRedis?
Redis serwer nie obsługuje natywnie SSL, ale nie w pamięci podręcznej Redis Azure. Jeśli łączysz tooAzure pamięci podręcznej Redis i klient obsługuje protokół SSL, takich jak programie StackExchange.Redis, należy użyć protokołu SSL.

>[!NOTE]
>port bez protokołu SSL Hello jest wyłączony domyślnie do nowych wystąpień w pamięci podręcznej Redis Azure. Jeśli klient nie obsługuje protokołu SSL, a następnie hello portu bez protokołu SSL należy włączyć, wykonując instrukcje hello z hello [portów](cache-configure.md#access-ports) sekcji hello [Konfigurowanie pamięci podręcznej w pamięci podręcznej Redis Azure](cache-configure.md) artykułu.
>
>

Redis narzędzi, takich jak `redis-cli` hello SSL port nie działają, ale można użyć narzędzia, takie jak `stunnel` toosecurely połącz port SSL toohello narzędzia hello wykonując instrukcje hello z hello [Announcing dostawcę stanu sesji ASP.NET dla wersji zapoznawczej Redis](http://blogs.msdn.com/b/webdev/archive/2014/05/12/announcing-asp-net-session-state-provider-for-redis-preview-release.aspx) wpis w blogu.

Aby uzyskać instrukcje dotyczące pobierania hello Redis narzędzia, zobacz hello [jak uruchomić polecenia Redis?](#cache-commands) sekcji.

### <a name="what-are-some-production-best-practices"></a>Jakie są najlepsze rozwiązania produkcyjnym?
* [Najlepsze rozwiązania w programie StackExchange.Redis](#stackexchangeredis-best-practices)
* [Konfiguracja i pojęć](#configuration-and-concepts)
* [Testowanie wydajności](#performance-testing)

#### <a name="stackexchangeredis-best-practices"></a>Najlepsze rozwiązania w programie StackExchange.Redis
* Ustaw `AbortConnect` toofalse, a następnie umożliwił hello ConnectionMultiplexer automatycznie ponownie. [Aby uzyskać szczegółowe informacje, zobacz](https://gist.github.com/JonCole/36ba6f60c274e89014dd#file-se-redis-setabortconnecttofalse-md).
* Ponowne użycie hello ConnectionMultiplexer — nie należy tworzyć nowego filtru dla każdego żądania. Witaj `Lazy<ConnectionMultiplexer>` wzorzec [pokazane](cache-dotnet-how-to-use-azure-redis-cache.md#connect-to-the-cache) jest zalecane.
* Redis działa najlepiej o mniejszej wartości, dlatego należy rozważyć siekanie zapasową większy danych do wielu kluczy. W [rozważania Redis](https://groups.google.com/forum/#!searchin/redis-db/size/redis-db/n7aa2A4DZDs/3OeEPHSQBAAJ), 100 kb jest uznawany za duża. Odczyt [w tym artykule](https://gist.github.com/JonCole/db0e90bedeb3fc4823c2#large-requestresponse-size) na przykład problem, który może być spowodowany dużej wartości.
* Konfigurowanie sieci [ustawienia puli wątków](#important-details-about-threadpool-growth) tooavoid przekroczeń limitu czasu.
* Użyj co najmniej hello connectTimeout domyślne 5 sekund. Ten interwał spowodowałoby to nadanie programie StackExchange.Redis wystarczający czas toore-nawiązania połączenia hello, w przypadku blip sieci.
* Należy pamiętać o hello wydajności kosztów związanych z różne operacje, na którym jest uruchomiony. Na przykład Witaj `KEYS` polecenia jest operacją O(n) i należy unikać. Witaj [lokacji redis.io](http://redis.io/commands/) zawiera szczegóły wokół hello złożoności czasu dla każdej operacji, który go obsługuje. Kliknij każdy złożoności hello toosee polecenie dla każdej operacji.

#### <a name="configuration-and-concepts"></a>Konfiguracja i pojęć
* Użyj Standard lub Premium warstwy dla systemów produkcyjnych. Hello warstwy podstawowa jest systemem jednego węzła z ma replikacji danych i nie umowy dotyczącej poziomu usług. Należy także użyć co najmniej C1 pamięci podręcznej. Pamięci podręczne C0 są zazwyczaj używane w scenariuszach proste tworzenie/testowanie oprogramowania.
* Należy pamiętać, że jest Redis **w pamięci** magazynu danych. Odczyt [w tym artykule](https://gist.github.com/JonCole/b6354d92a2d51c141490f10142884ea4#file-whathappenedtomydatainredis-md) tak, aby poznać scenariuszy, w których może wystąpić utrata danych.
* Opracowanie systemu tak, aby mogły obsługiwać połączenia blips [toopatching i pracy awaryjnej](https://gist.github.com/JonCole/317fe03805d5802e31cfa37e646e419d#file-azureredis-patchingexplained-md).

#### <a name="performance-testing"></a>Testowanie wydajności
* Uruchom przy użyciu `redis-benchmark.exe` tooget działanie możliwe przepływności przed zapisaniem testów wydajności. Ponieważ `redis-benchmark` nie obsługuje protokołu SSL, należy najpierw [włączenie portu hello bez protokołu SSL za pośrednictwem portalu Azure hello](cache-configure.md#access-ports) przed uruchomieniem testu hello. Przykłady można znaleźć [jak testu wydajności i przetestować hello wydajności Moje pamięci podręcznej?](#how-can-i-benchmark-and-test-the-performance-of-my-cache)
* powitania klienta używane do testowania maszyny Wirtualnej musi należeć do hello tego samego regionu wystąpienia pamięci podręcznej Redis.
* Zalecamy używanie Dv2 serii maszyn wirtualnych klienta jako lepsze sprzęt i nadać hello najlepsze wyniki.
* Upewnij się, klient zostanie wybrana maszyna wirtualna ma co najmniej tyle możliwości obliczeniowych i przepustowości jako pamięci podręcznej hello, testowany.
* Włączenie funkcji VRSS na komputerze klienckim hello są w systemie Windows. [Aby uzyskać szczegółowe informacje, zobacz](https://technet.microsoft.com/library/dn383582.aspx).
* Wystąpienia pamięci podręcznej Redis warstwy Premium mają lepiej sieci opóźnienia i przepływności, ponieważ działają na lepsze sprzętu dla procesora CPU i sieci.

<a name="cache-redis-commands"></a>

### <a name="what-are-some-of-hello-considerations-when-using-common-redis-commands"></a>Jakie są kwestie hello za pomocą wspólnego poleceń Redis?
* Nie należy uruchamiać niektórych poleceń pamięci podręcznej Redis, przyjmujących toocomplete dużo czasu, bez zrozumienia wpływu hello tych poleceń.
  * Na przykład nie uruchamiaj hello [KLUCZE](http://redis.io/commands/keys) command w środowisku produkcyjnym może zająć tooreturn dużo czasu, w zależności od hello liczbę kluczy. Redis jest serwerem jednowątkowe i przetwarza polecenia co naraz. Jeśli masz inne polecenia wydane po KLUCZE ich nie będą przetwarzane aż polecenie KLUCZE hello przetworzy Redis. Witaj [lokacji redis.io](http://redis.io/commands/) zawiera szczegóły wokół hello złożoności czasu dla każdej operacji, który go obsługuje. Kliknij każdy złożoności hello toosee polecenie dla każdej operacji.
* Rozmiary kluczy — należy używać małych klucza/wartości lub dużych klucza/wartości? Ogólnie rzecz biorąc to zależy od scenariusza hello. Scenariusz wymaga większych kluczy, można dopasować hello ConnectionTimeout i spróbuj ponownie wartości i dostosować Logika ponawiania. Z perspektywy serwera Redis mniejszej wartości są przestrzegane toohave lepszą wydajność.
* Te zagadnienia nie oznacza, że nie można przechowywać większe wartości w pamięci podręcznej Redis; należy pamiętać o hello następujące zagadnienia. Opóźnienia będzie wyższa. Jeśli jeden zestaw danych, który jest większy i jedną, która jest mniejsza, można użyć wielu wystąpień ConnectionMultiplexer, każdy skonfigurowany zestaw różne wartości limitu czasu i ponów próbę, zgodnie z opisem w poprzedniej hello [co hello Opcje konfiguracji w programie StackExchange.Redis czy](#cache-configuration) sekcji.

<a name="cache-benchmarking"></a>

### <a name="how-can-i-benchmark-and-test-hello-performance-of-my-cache"></a>Jak testu wydajności i przetestować hello wydajności Moje pamięci podręcznej?
* [Włącz diagnostykę w pamięci podręcznej](cache-how-to-monitor.md#enable-cache-diagnostics) można więc [monitor](cache-how-to-monitor.md) hello kondycji pamięci podręcznej. Możesz wyświetlić hello metryki w hello portalu Azure i może również [pobrać i przejrzyj](https://github.com/rustd/RedisSamples/tree/master/CustomMonitoring) je za pomocą narzędzi hello wybranych przez użytkownika.
* Test tooload redis benchmark.exe można użyć serwera Redis.
* Sprawdź, czy klient testowania obciążenia hello i pamięć podręczna Redis hello są hello tego samego regionu.
* Użyj redis cli.exe i monitorować hello pamięci podręcznej za pomocą polecenia informacje hello.
* Jeżeli obciążenie jest przyczyną fragmentacji pamięci wysokiej, należy skalować tooa większy rozmiar pamięci podręcznej.
* Aby uzyskać instrukcje dotyczące pobierania hello Redis narzędzia, zobacz hello [jak uruchomić polecenia Redis?](#cache-commands) sekcji.

Witaj następujące polecenia. podać przykład za pomocą redis benchmark.exe. Aby uzyskać dokładne wyniki, uruchom następujące polecenia z maszyny Wirtualnej w hello tym samym regionie co pamięć podręczną.

* Przy użyciu 1 ładunku k żądań potokowe SET testu

  `redis-benchmark.exe -h **yourcache**.redis.cache.windows.net -a **yourAccesskey** -t SET -n 1000000 -d 1024 -P 50`
* Test potokowe pobrać żądania przy użyciu 1 ładunku k.
  Uwaga: Uruchamianie testu zestaw hello pokazanym powyżej pierwszego toopopulate pamięci podręcznej

  `redis-benchmark.exe -h **yourcache**.redis.cache.windows.net -a **yourAccesskey** -t GET -n 1000000 -d 1024 -P 50`

<a name="threadpool"></a>

### <a name="important-details-about-threadpool-growth"></a>Ważne informacje dotyczące wzrostu puli wątków
Witaj puli wątków CLR ma dwa typy wątków - "Pracownik" i "We/wy wykonania Port" (alias portu) wątków.

* Wątki robocze są używane podczas dla elementów, jak przetwarzanie `Task.Run(…)` lub `ThreadPool.QueueUserWorkItem(…)` metody. Wątki te są również używane przez różne składniki w hello CLR podczas pracy musi toohappen wątku w tle.
* Wątki portu są używane w przypadku asynchroniczne We/Wy (np. zawartości z sieci hello).

Pula wątków Hello zapewnia nowych wątków roboczych lub wątków zakończenia We/Wy na żądanie (bez żadnych ograniczania), dopóki osiągnie ustawienie "Minimalny" hello, dla każdego typu wątku. Minimalna liczba wątków hello jest domyślnie toohello liczby procesorów w systemie.

Raz hello liczba "istniejących wątków (zajęty) trafień hello minimalna" Liczba wątków hello puli wątków będzie przepustowości hello jaką go injects nowego wątku tooone wątków na 500 milisekund. Zwykle jeśli system pobiera serii pracy wymagające wątku portu, zostanie przetworzony pracy bardzo szybko. Jednak jeśli serii hello pracy jest większa niż hello skonfigurowane ustawienie "Minimalny", będą pewne opóźnienie podczas przetwarzania niektórych hello pracy jako hello puli wątków czeka na jedno z następujących toohappen.

1. Istniejące wątku staje się wolnego tooprocess hello pracy.
2. Nie istniejącego wątku staje się bezpłatnie do 500 MS., dzięki utworzeniu nowego wątku.

Zasadniczo oznacza to, że gdy hello liczba wątków zajęty jest większa niż minimalna wątków, prawdopodobnie płatność opóźnienie 500 MS. przed przetworzeniem ruchu sieciowego przez aplikację hello. Ponadto jest ważne toonote, że kiedy istniejący wątku jest bezczynne przez czas dłuższy niż 15 sekund (oparte na I Zapamiętaj), będzie go wyczyszczone, a można powtórzyć ten cykl wzrostu i kurczenia.

Jeśli przyjrzymy się komunikat o błędzie na przykład w programie StackExchange.Redis (kompilacji 1.0.450 lub nowsza), zobaczysz, że teraz Wyświetla statystyki puli wątków (zobacz poniżej szczegóły portu i proces ROBOCZY).

    System.TimeoutException: Timeout performing GET MyKey, inst: 2, mgr: Inactive,
    queue: 6, qu: 0, qs: 6, qc: 0, wr: 0, wq: 0, in: 0, ar: 0,
    IOCP: (Busy=6,Free=994,Min=4,Max=1000),
    WORKER: (Busy=3,Free=997,Min=4,Max=1000)

W poprzednim przykładzie hello widać, że dla portu wątku są 6 zajęty wątków i hello system jest skonfigurowany tooallow 4 minimalna liczba wątków. W takim przypadku powitania klienta będzie prawdopodobnie przejrzane dwóch opóźnienia 500 ms ponieważ 6 > 4.

Należy pamiętać, programie StackExchange.Redis można trafień limitów czasu Jeśli pobiera ograniczenie wzrostu wątków portu lub procesu roboczego.

### <a name="recommendation"></a>Zalecenie
Biorąc pod uwagę te informacje, zdecydowanie zalecane klientów ustawienie hello Konfiguracja minimalna wartość portu i proces ROBOCZY toosomething wątków większa niż wartość domyślna hello. Firma Microsoft nie można nadać pasującego wskazówki dotyczące co ta wartość powinna być, ponieważ wartość prawej strony hello w jednej aplikacji będzie zbyt wysoki/niska dla innej aplikacji. To ustawienie również może wpłynąć na wydajność hello innych części złożonych aplikacji, więc każdy klient wymaga strojenia toofine potrzebne w tym tootheir ustawienia określone. Dobrym miejscem początkowy jest 200 lub 300, przetestowanie i dostosowanie zgodnie z potrzebami.

Jak tooconfigure tego ustawienia:

* W programie ASP.NET, użyj hello [ustawienie konfiguracji "minIoThreads"] [ "minIoThreads" configuration setting] w obszarze hello `<processModel>` element konfiguracji w pliku web.config. Jeśli korzystasz z wewnątrz witryn sieci Web platformy Azure, to ustawienie nie jest uwidaczniana, za pomocą opcji konfiguracji hello. Należy jednak nadal być stanie tooconfigure to ustawienie programowo (patrz poniżej), od wybranej metody Application_Start w global.asax.cs.

  > [!NOTE] 
  > Witaj podana w tym elemencie konfiguracji jest *-core* ustawienie. Na przykład jeśli korzystasz z 4-rdzeniową maszyną i chcesz Twojej toobe ustawienie minIOThreads 200 w czasie wykonywania, czy użyć `<processModel minIoThreads="50"/>`.
  >

* Poza ASP.NET, użyj hello [ThreadPool.SetMinThreads(...) ](https://msdn.microsoft.com/library/system.threading.threadpool.setminthreads.aspx) Interfejsu API.

<a name="server-gc"></a>

### <a name="enable-server-gc-tooget-more-throughput-on-hello-client-when-using-stackexchangeredis"></a>Włączyć tooget serwera wykazu Globalnego więcej przepływności na powitania klienta za pomocą programie StackExchange.Redis
Włączenie serwera wykazu Globalnego można zoptymalizować powitania klienta i zapewnić lepszą wydajność i Przepływność przy użyciu programie StackExchange.Redis. Aby uzyskać więcej informacji na serwerze wykazu Globalnego i w jaki sposób tooenable, zobacz następujące artykuły hello:

* [tooenable serwera wykazu Globalnego](https://msdn.microsoft.com/library/ms229357.aspx)
* [Podstawy dotyczące wyrzucania elementów bezużytecznych](https://msdn.microsoft.com/library/ee787088.aspx)
* [Wyrzucanie elementów bezużytecznych i wydajność](https://msdn.microsoft.com/library/ee851764.aspx)


### <a name="performance-considerations-around-connections"></a>Zagadnienia dotyczące wydajności wokół połączeń

Każda warstwa cenowa ma inną limity dla połączeń klienckich, pamięci oraz przepustowości. Podczas każdego rozmiaru pamięci podręcznej umożliwia *do* określonej liczby połączeń, każdy tooRedis połączenia obciążenie ma skojarzonych z nim. Przykładem takich obciążenie będzie użycia Procesora i pamięci w wyniku szyfrowania TLS/SSL. Hello limit maksymalnej liczby połączeń dla rozmiaru pamięci podręcznej danego zakłada lekkim załadować pamięci podręcznej. Czy ładowanie z połączenia koszty *plus* obciążenia z operacjami klienta przekracza pojemność systemu hello, hello pamięci podręcznej można doświadczyć problemów dotyczących pojemności, nawet jeśli nie przekroczono limit połączenia hello hello bieżący rozmiar pamięci podręcznej.

Aby uzyskać więcej informacji na temat limitów różnych połączeń powitania dla każdej warstwy, zobacz [cennik usługi pamięć podręczna Redis Azure](https://azure.microsoft.com/pricing/details/cache/). Aby uzyskać więcej informacji na temat połączeń i inne konfiguracje domyślne, zobacz [Redis domyślnej konfiguracji serwera](cache-configure.md#default-redis-server-configuration).

<a name="cache-monitor"></a>

### <a name="how-do-i-monitor-hello-health-and-performance-of-my-cache"></a>Jak monitorować hello kondycji i wydajności Moje pamięci podręcznej
Wystąpienia pamięci podręcznej Redis Azure firmy Microsoft mogą być monitorowane w hello [portalu Azure](https://portal.azure.com). Można wyświetlić metryki, przypiąć metryki wykresy toohello tablicy startowej, Dostosuj zakres dat i godzin hello monitorowania wykresy, dodać i usunąć metryki z wykresy hello i ustawić alerty, gdy zostaną spełnione określone warunki. Aby uzyskać więcej informacji, zobacz [pamięci podręcznej Redis Azure Monitor](cache-how-to-monitor.md).

Witaj pamięci podręcznej Redis **zasobów menu** zawiera również kilka narzędzi do monitorowania i rozwiązywania problemów pamięci podręczne.

* **Diagnozowanie i rozwiązywanie problemów** zawiera informacje o najczęściej występujących problemów i strategii w celu ich rozwiązania.
* **Kondycja zasobów** oczekuje zasobu i informuje, czy działa on zgodnie z oczekiwaniami. Aby uzyskać więcej informacji na temat hello usługi kondycji zasobów Azure, zobacz [Przegląd kondycji zasobów Azure](../resource-health/resource-health-overview.md).
* **Nowe żądanie pomocy technicznej** udostępnia opcje tooopen żądania pomocy technicznej dla pamięci podręcznej.

Te narzędzia Włącz możesz toomonitor hello kondycji wystąpień z pamięci podręcznej Redis Azure i pomocne w zarządzaniu aplikacjami buforowania. Aby uzyskać więcej informacji, zobacz hello "Pomocy technicznej i rozwiązywania problemów z ustawienia" część [jak tooconfigure Azure pamięci podręcznej Redis](cache-configure.md).

<a name="cache-timeouts"></a>

### <a name="why-am-i-seeing-timeouts"></a>Dlaczego widzę limitów czasu?
Limity czasu wprowadzenia w powitania klienta użycie tootalk tooRedis. Po wysłaniu polecenia serwera Redis toohello polecenia hello jest umieszczone w kolejce i serwera Redis ostatecznie przejmuje hello polecenia i go uruchomi. Jednak powitania klienta może przekroczono limit czasu podczas tego procesu, a jeśli nie wystąpił wyjątek jest zgłaszany na powitania wywołanie po stronie. Aby uzyskać więcej informacji na temat rozwiązywania problemów limitu czasu, zobacz [rozwiązywania problemów klienta](cache-how-to-troubleshoot.md#client-side-troubleshooting) i [wyjątków przekroczenia limitu czasu w programie StackExchange.Redis](cache-how-to-troubleshoot.md#stackexchangeredis-timeout-exceptions).

<a name="cache-disconnect"></a>

### <a name="why-was-my-client-disconnected-from-hello-cache"></a>Dlaczego moja klient został odłączony od hello pamięci podręcznej?
Witaj poniżej przedstawiono niektóre typowe Przyczyna rozłączenia pamięci podręcznej.

* Powoduje, że po stronie klienta
  * Aplikacja kliencka Hello zostało wdrożone.
  * Aplikacja kliencka Hello wykonać operacji skalowania.
    * W przypadku hello aplikacji sieci Web lub usługi w chmurze, może to być spowodowane skalowanie tooauto.
  * Witaj warstwy sieci po stronie klienta hello zmienione.
  * Przejściowy błąd powitania klienta lub hello węzłów sieci między powitania klienta i serwera hello.
  * wartości progowych przepustowości Hello były dostępne.
  * Procesora powiązany operacji trwało zbyt długo toocomplete.
* Powoduje, że po stronie serwera
  * Na powitania standardowe pamięci podręcznej oferty hello usługi pamięć podręczna Redis Azure inicjowane awaryjnej z węzła pomocniczego toohello hello węzła podstawowego.
  * Azure została poprawki wystąpienia hello wdrożonym hello pamięci podręcznej
    * Może to być aktualizacje serwera Redis lub ogólne konserwacji maszyny Wirtualnej.

### <a name="which-azure-cache-offering-is-right-for-me"></a>Która oferta pamięci podręcznej systemu Azure jest dla mnie najlepsza?
> [!IMPORTANT]
> Zgodnie z ostatniego roku [anonsu](https://azure.microsoft.com/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/), usługa usługi zarządzana pamięć podręczna Azure i pamięci podręcznej na roli Azure **zostały wycofane** w dniu 30 listopada 2016 r. Firma Microsoft zaleca toouse [pamięć podręczna Redis Azure](https://azure.microsoft.com/services/cache/). Aby uzyskać informacje na temat migracji, zobacz [migracji z usługi zarządzana pamięć podręczna tooAzure pamięci podręcznej Redis](cache-migrate-to-redis.md).
>
>

### <a name="azure-redis-cache"></a>Azure Redis Cache
Pamięć podręczna Redis Azure jest ogólnie dostępna w rozmiarach się too53 GB i ma dostępność na poziomie 99,9%. nowe Hello [warstwy premium](cache-premium-tier-intro.md) oferuje rozmiary too530 GB i pomocy technicznej dla klastra sieć Wirtualną i trwałości z SLA 99,9%.

Azure pamięci podręcznej Redis zapewnia klientom Witaj możliwości toouse bezpieczny, w wersji dedykowanej pamięci podręcznej Redis, zarządzany przez firmę Microsoft. Z tej oferty można uzyskać tooleverage hello bogatemu zestawowi funkcji i ekosystemem pochodzącymi z pamięci podręcznej Redis i niezawodnych hosting i monitorowania firmy Microsoft.

W przeciwieństwie do tradycyjnych pamięci podręczne, które dotyczą tylko z pary klucz wartość Redis jest popularnych jego wysokiej wydajności typów danych. Redis również obsługuje uruchamianie operacji niepodzielnych w tych typów, takie jak dodanie ciągu tooa; Zwiększanie wartości hello w skrót; Wypychanie listy tooa; Obliczanie przecięcia zestawu, Unii i różnica; lub pobierania hello członek o najwyższej klasyfikacji w zestawie posortowane. Inne funkcje obejmują obsługę transakcji, pub/sub, Lua skryptów, klucze z ograniczoną time-to-live i zachowują się Redis toomake ustawień konfiguracji, takich jak tradycyjnych pamięci podręcznej.

Inny Powodzenie tooRedis kluczowym aspektem jest hello typu open source dobrej kondycji, aktywny ekosystem wbudowane wokół niego. Znajduje to odzwierciedlenie w hello różnorodnych klientów pamięci podręcznej Redis dostępne w wielu językach. Ten ekosystem i szerokiego zakresu klientów Zezwalaj toobe pamięć podręczna Redis Azure używany przez niemal dowolnym obciążeniu, które tworzysz wewnątrz Azure.

Aby uzyskać więcej informacji na temat rozpoczynania pracy z pamięcią podręczną Redis Azure, zobacz [jak tooUse Azure pamięci podręcznej Redis](cache-dotnet-how-to-use-azure-redis-cache.md) i [dokumentacji pamięć podręczna Redis Azure](index.md).

### <a name="managed-cache-service"></a>Zarządzane usługi pamięć podręczna
[Zarządzana pamięć podręczna usługi została wycofana w dniu 30 listopada 2016 r.](https://azure.microsoft.com/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/)

tooview zarchiwizowane dokumentacji, zobacz [zarchiwizowane dokumentację usługi pamięć podręczna zarządzane](https://msdn.microsoft.com/library/azure/dn386094.aspx).

### <a name="in-role-cache"></a>Pamięć podręczna oparta na roli
[Pamięć podręczna w roli została wycofana w dniu 30 listopada 2016 r.](https://azure.microsoft.com/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/)

tooview zarchiwizowane dokumentacji, zobacz [zarchiwizowane dokumentacji pamięci podręcznej w roli](https://msdn.microsoft.com/library/azure/dn386103.aspx).

["minIoThreads" configuration setting]: https://msdn.microsoft.com/library/vstudio/7w2sway1(v=vs.100).aspx
