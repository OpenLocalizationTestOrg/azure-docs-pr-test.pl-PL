---
title: "aaaConfigure sieci wirtualnej dla podręczna Redis Azure Premium | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate i zarządzanie nimi obsługi sieci wirtualnej dla swoich wystąpień pamięci podręcznej Redis Azure warstwy Premium"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 8b1e43a0-a70e-41e6-8994-0ac246d8bf7f
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: sdanie
ms.openlocfilehash: fab715f4d9365ee4c2f8b89d2e2e58768c25b671
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-virtual-network-support-for-a-premium-azure-redis-cache"></a>W jaki sposób tooconfigure sieci wirtualnej obsługę podręczna Redis Azure Premium
Pamięć podręczna Redis Azure ma inną pamięci podręcznej oferty, które zapewniają elastyczność w wyborze hello rozmiar pamięci podręcznej i funkcji, łącznie z funkcji warstwy Premium, takich jak klastrowanie, trwałości i obsługi sieci wirtualnej. Sieci wirtualnej jest w chmurze hello sieci prywatnej. Po skonfigurowaniu wystąpienia pamięci podręcznej Redis Azure z sieci wirtualnej nie jest publicznie adresowana i jest możliwy tylko z maszyn wirtualnych i aplikacji w obrębie hello sieci wirtualnej. W tym artykule opisano, jak sieci wirtualnej tooconfigure obsługują dla wystąpienia pamięci podręcznej Redis Azure premium.

> [!NOTE]
> Pamięć podręczna Redis Azure obsługuje zarówno classic i sieci wirtualnych Menedżera zasobów.
> 
> 

Aby uzyskać informacji o innych funkcjach pamięci podręcznej premium, zobacz [warstwy pamięci podręcznej Redis Azure Premium toohello wprowadzenie](cache-premium-tier-intro.md).

## <a name="why-vnet"></a>Dlaczego sieci wirtualnej?
[Sieć wirtualna platformy Azure (VNet)](https://azure.microsoft.com/services/virtual-network/) wdrożenie zapewnia większe bezpieczeństwo i izolację dla pamięci podręcznej Redis Azure, jak również podsieci, zasad kontroli dostępu i inne funkcje toofurther ograniczyć dostęp.

## <a name="virtual-network-support"></a>Obsługa sieci wirtualnej
Obsługa usługi Virtual Network (VNet) jest skonfigurowany na powitania **nowa pamięć podręczna Redis** bloku podczas tworzenia pamięci podręcznej. 

[!INCLUDE [redis-cache-create](../../includes/redis-cache-premium-create.md)]

Po wybraniu warstwie cenowej premium można skonfigurować integracji Redis sieci wirtualnej, wybierając sieć wirtualną, która znajduje się w hello tej samej subskrypcji i lokalizacji co pamięć podręczną. toouse nowej sieci wirtualnej, utwórz go najpierw wykonać kroki hello w [Utwórz sieć wirtualną przy użyciu portalu Azure hello](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) lub [utworzyć sieć wirtualną (klasyczne) przy użyciu portalu Azure hello](../virtual-network/virtual-networks-create-vnet-classic-pportal.md) , a następnie wróć toohello **Nowa pamięć podręczna Redis** toocreate bloku i skonfigurować pamięć podręczną premium.

Witaj tooconfigure sieci wirtualnej dla nowej pamięci podręcznej, kliknij przycisk **sieci wirtualnej** na powitania **nowa pamięć podręczna Redis** bloku, a następnie wybierz hello potrzeby sieci wirtualnej z listy rozwijanej hello.

![Sieć wirtualna][redis-cache-vnet]

Wybierz hello odpowiednie podsieci z hello **podsieci** listy rozwijanej liście, a następnie określ hello potrzeby **statyczny adres IP**. Jeśli używasz klasycznego hello sieci wirtualnej **statyczny adres IP** pole jest opcjonalne, a jeśli nie zostanie określona, wybrano jeden z hello wybrane podsieci.

> [!IMPORTANT]
> Podczas wdrażania tooa pamięć podręczna Redis Azure Resource Manager sieci wirtualnej, hello pamięci podręcznej musi być w dedykowanym podsieć, która nie zawiera żadnych innych zasobów, z wyjątkiem wystąpienia pamięci podręcznej Redis Azure. Toodeploy podejmowana jest próba tooa pamięć podręczna Redis Azure podsieci tooa Menedżera zasobów w sieci wirtualnej, która zawiera inne zasoby, hello wdrożenie nie powiedzie się.
> 
> 

![Sieć wirtualna][redis-cache-vnet-ip]

> [!IMPORTANT]
> Azure rezerwuje niektórych adresów IP w każdej podsieci, a nie można użyć tych adresów. Witaj imię i nazwisko adresów IP podsieci hello są zastrzeżone dla protokołu zgodność, wraz z trzech więcej adresów używanych na potrzeby usług Azure. Aby uzyskać więcej informacji, zobacz [istnieją wszystkie ograniczenia dotyczące używania adresów IP w ramach tych podsieci?](../virtual-network/virtual-networks-faq.md#are-there-any-restrictions-on-using-ip-addresses-within-these-subnets)
> 
> W przypadku dodawania adresów IP toohello używanych przez infrastrukturę sieci Wirtualnej Azure hello każdy Redis wystąpienia adresów IP używa dwóch podsieci hello na niezależnych i jeden dodatkowy adres IP dla modułu równoważenia obciążenia hello. Pamięć podręczna nieklastrowanych jest uważany za toohave jednego niezależnego fragmentu.
> 
> 

Po utworzeniu pamięci podręcznej hello hello konfiguracji hello sieci wirtualnej można wyświetlić, klikając **sieci wirtualnej** z hello **zasobów menu**.

![Sieć wirtualna][redis-cache-vnet-info]

tooconnect tooyour Azure Redis wystąpienia pamięci podręcznej przy użyciu sieci wirtualnej, określ nazwę hosta hello pamięć podręczną w parametrach połączenia hello, jak pokazano w hello poniższy przykład:

    private static Lazy<ConnectionMultiplexer> lazyConnection = new Lazy<ConnectionMultiplexer>(() =>
    {
        return ConnectionMultiplexer.Connect("contoso5premium.redis.cache.windows.net,abortConnect=false,ssl=true,password=password");
    });

    public static ConnectionMultiplexer Connection
    {
        get
        {
            return lazyConnection.Value;
        }
    }

## <a name="azure-redis-cache-vnet-faq"></a>Sieć wirtualna pamięci podręcznej Azure Redis — często zadawane pytania
Witaj, następujące listy zawiera zadawane pytania dotyczące skalowania pamięć podręczna Redis Azure hello toocommonly odpowiedzi.

* [Co to są niektórych typowych problemów błędnej konfiguracji sieci wirtualnych i pamięci podręcznej Redis Azure?](#what-are-some-common-misconfiguration-issues-with-azure-redis-cache-and-vnets)
* [Jak sprawdzić, czy Moje pamięci podręcznej działa w sieci Wirtualnej?](#how-can-i-verify-that-my-cache-is-working-in-a-vnet)
* [Sieci wirtualne można używać z standard lub podstawowa pamięci podręcznej?](#can-i-use-vnets-with-a-standard-or-basic-cache)
* [Dlaczego Tworzenie pamięci podręcznej Redis powiedzie w niektórych podsieci, a innych nie?](#why-does-creating-a-redis-cache-fail-in-some-subnets-but-not-others)
* [Jakie są wymagania dotyczące miejsca na powitania podsieci adresów?](#what-are-the-subnet-address-space-requirements)
* [Wszystkie funkcje pamięci podręcznej działają odnośnie do hostowania pamięci podręcznej w sieci Wirtualnej?](#do-all-cache-features-work-when-hosting-a-cache-in-a-vnet)

## <a name="what-are-some-common-misconfiguration-issues-with-azure-redis-cache-and-vnets"></a>Co to są niektórych typowych problemów błędnej konfiguracji sieci wirtualnych i pamięci podręcznej Redis Azure?
Gdy pamięć podręczna Redis Azure znajduje się w sieci wirtualnej, porty hello hello następujące tabele są używane. 

>[!IMPORTANT]
>Porty hello w hello następujące tabele są zablokowane, hello pamięci podręcznej mogą nie działać poprawnie. Co najmniej jeden z tych portów zablokowane jest posiadanie hello najbardziej typowych konfiguracji problem przy użyciu pamięci podręcznej Redis Azure w sieci wirtualnej.
> 
> 

- [Wymagania dotyczące portów wychodzących](#outbound-port-requirements)
- [Wymagania dotyczące portów dla ruchu przychodzącego](#inbound-port-requirements)

### <a name="outbound-port-requirements"></a>Wymagania dotyczące portów wychodzących

Istnieje siedem wymagań dotyczących portu wychodzącego.

- W razie potrzeby, wszystkie toohello połączenia wychodzące przez internet, mogą być wprowadzane za pośrednictwem klienta lokalnego inspekcji urządzenia.
- Trzy porty hello trasy punkty końcowe tooAzure ruchu obsługi usługi Azure Storage i Azure DNS.
- Witaj, pozostałe zakresy portów i komunikacji podsieci wewnętrznej pamięci podręcznej Redis. Brak reguł NSG podsieci są niezbędne do komunikacji podsieci wewnętrznej pamięci podręcznej Redis.

| Porty | Kierunek | Protokół transportu | Przeznaczenie | Lokalny adres IP | Zdalny adres IP |
| --- | --- | --- | --- | --- | --- |
| 80, 443 |Wychodzący |TCP |Redis zależności na platformie Azure magazynu/infrastruktury kluczy publicznych (Internet) | (Redis podsieci) |* |
| 53 |Wychodzący |TCP/UDP |Redis zależności w systemie DNS (Internet/VNet) | (Redis podsieci) |* |
| 8443 |Wychodzący |TCP |Wewnętrzny komunikację z usługą Redis | (Redis podsieci) | (Redis podsieci) |
| 10221-10231 |Wychodzący |TCP |Wewnętrzny komunikację z usługą Redis | (Redis podsieci) | (Redis podsieci) |
| 20226 |Wychodzący |TCP |Wewnętrzny komunikację z usługą Redis | (Redis podsieci) |(Redis podsieci) |
| 13000-13999 |Wychodzący |TCP |Wewnętrzny komunikację z usługą Redis | (Redis podsieci) |(Redis podsieci) |
| 15000-15999 |Wychodzący |TCP |Wewnętrzny komunikację z usługą Redis | (Redis podsieci) |(Redis podsieci) |


### <a name="inbound-port-requirements"></a>Wymagania dotyczące portów dla ruchu przychodzącego

Ma osiem wymagań zakresu portów przychodzących. Przychodzące żądania w tych zakresów są ruch przychodzący z innych usług hostowanych w hello tej samej sieci Wirtualnej lub toohello wewnętrznej komunikacji podsieci Redis.

| Porty | Kierunek | Protokół transportu | Przeznaczenie | Lokalny adres IP | Zdalny adres IP |
| --- | --- | --- | --- | --- | --- |
| 6379, 6380 |Przychodzący |TCP |Równoważenie obciążenia Azure tooRedis komunikacji klienta, | (Redis podsieci) |Sieć wirtualna Azure Load Balancer |
| 8443 |Przychodzący |TCP |Wewnętrzny komunikację z usługą Redis | (Redis podsieci) |(Redis podsieci) |
| 8500 |Przychodzący |TCP/UDP |Równoważenia obciążenia Azure | (Redis podsieci) |Azure Load Balancer |
| 10221-10231 |Przychodzący |TCP |Wewnętrzny komunikację z usługą Redis | (Redis podsieci) |(Redis podsieć), usługi równoważenia obciążenia Azure |
| 13000-13999 |Przychodzący |TCP |TooRedis komunikacji klienta klastrów równoważenia obciążenia Azure | (Redis podsieci) |Sieć wirtualna Azure Load Balancer |
| 15000-15999 |Przychodzący |TCP |Równoważenie obciążenia klastrów, Azure tooRedis komunikacji klienta | (Redis podsieci) |Sieć wirtualna Azure Load Balancer |
| 16001 |Przychodzący |TCP/UDP |Równoważenia obciążenia Azure | (Redis podsieci) |Azure Load Balancer |
| 20226 |Przychodzący |TCP |Wewnętrzny komunikację z usługą Redis | (Redis podsieci) |(Redis podsieci) |

### <a name="additional-vnet-network-connectivity-requirements"></a>Dodatkowe wymagania dotyczące łączności sieci sieci Wirtualnej

Istnieją wymagania dotyczące łączności sieciowej pamięci podręcznej Redis Azure nie może być początkowo spełnieniu w sieci wirtualnej. Pamięć podręczna Redis Azure wymaga hello wszystkie następujące elementy toofunction poprawnie, gdy jest używany w ramach sieci wirtualnej.

* Wychodzące połączenie tooAzure magazynu punktów końcowych sieci na całym świecie. Obejmuje to punkty końcowe znajduje się w hello tego samego regionu hello wystąpienia pamięci podręcznej Redis Azure, a także punkty końcowe usługi storage znajduje się w **innych** regiony platformy Azure. Punkty końcowe usługi Azure Storage rozwiązania w obszarze hello następujące domeny DNS: *table.core.windows.net*, *blob.core.windows.net*, *queue.core.windows.net*i *file.core.windows.net*. 
* Wychodzące połączenia sieciowego zbyt*ocsp.msocsp.com*, *mscrl.microsoft.com*, i *crl.microsoft.com*. To połączenie jest toosupport wymagane funkcje protokołu SSL.
* Witaj konfigurację systemu DNS dla sieci wirtualnej hello musi on mieć możliwość rozpoznawania wszystkie punkty końcowe hello i domeny wymienione w hello wcześniejszych punktów. W celu zapewnienia prawidłowy infrastruktura DNS jest skonfigurowany i dla sieci wirtualnej hello można spełnić te wymagania systemu DNS.
* Toohello połączenia wychodzącego po Azure punktów końcowych monitorowania, które rozwiązanie w obszarze hello następujące domeny DNS: shoebox2 black.shoebox2.metrics.nsatc.net, prod2.prod2.metrics.nsatc.net Północna, azglobal-black.azglobal.metrics.nsatc.net, wschód prod2.prod2.metrics.nsatc.net shoebox2-red.shoebox2.metrics.nsatc.net azglobal-red.azglobal.metrics.nsatc.net.

### <a name="how-can-i-verify-that-my-cache-is-working-in-a-vnet"></a>Jak sprawdzić, czy Moje pamięci podręcznej działa w sieci Wirtualnej?

>[!IMPORTANT]
>Podczas łączenia z wystąpienia pamięci podręcznej Redis Azure tooan, który znajduje się w sieci Wirtualnej, klienci muszą być w pamięci podręcznej hello tej samej sieci Wirtualnej, w tym testowanie aplikacji ani badanie narzędzia diagnostyczne.
>
>

Po skonfigurowaniu wymagania dotyczące portów hello zgodnie z opisem w poprzedniej sekcji hello można sprawdzić, czy pamięć podręczna działa, wykonując następujące kroki hello.

- [Ponowny rozruch](cache-administration.md#reboot) wszystkie hello węzłów w pamięci podręcznej. Jeśli wszystkie hello wymagane zależności buforu jest nieosiągalny (zgodnie z opisem w [ruchu przychodzącego wymagania dotyczące portów](cache-how-to-premium-vnet.md#inbound-port-requirements) i [wymagania dotyczące portów wychodzących](cache-how-to-premium-vnet.md#outbound-port-requirements)), hello pamięci podręcznej nie będzie możliwe toorestart pomyślnie.
- Po hello pamięci podręcznej węzły zostały ponownie uruchomione (zgodnie z raportem hello stan pamięci podręcznej w hello portalu Azure), można wykonać hello następujące testy:
  - polecenie ping hello punkt końcowy (przy użyciu portu 6380) z komputera, który mieści się w hello tej samej sieci Wirtualnej jako hello pamięci podręcznej, za pomocą [tcping](https://www.elifulkerson.com/projects/tcping.php). Na przykład:
    
    `tcping.exe contosocache.redis.cache.windows.net 6380`
    
    Jeśli hello `tcping` narzędzie informuje, że hello port jest otwarty, pamięć podręczna hello jest dostępny dla połączeń z klientami w hello sieci Wirtualnej.

  - Inny sposób tootest jest toocreate klienta pamięci podręcznej testu (co może być prostą aplikację konsoli przy użyciu programie StackExchange.Redis) który łączy z pamięci podręcznej toohello i dodaje i pobiera niektóre elementy z pamięci podręcznej hello. Zainstaluj klienta próbki hello na maszynie Wirtualnej, która znajduje się w tej samej sieci Wirtualnej jako pamięci podręcznej hello Witaj i uruchom go tooverify łączności toohello w pamięci podręcznej.


### <a name="can-i-use-vnets-with-a-standard-or-basic-cache"></a>Sieci wirtualne można używać z standard lub podstawowa pamięci podręcznej?
Sieci wirtualne można używać tylko z pamięci podręcznych premium.

### <a name="why-does-creating-a-redis-cache-fail-in-some-subnets-but-not-others"></a>Dlaczego Tworzenie pamięci podręcznej Redis powiedzie w niektórych podsieci, a innych nie?
Jeśli wdrażasz tooa pamięć podręczna Redis Azure Resource Manager sieci wirtualnej hello pamięci podręcznej musi być w dedykowanym podsieci, która zawiera inny typ zasobu. Toodeploy podejmowana jest próba tooa pamięć podręczna Redis Azure podsieci sieci wirtualnej Resource Manager, która zawiera inne zasoby, hello wdrożenie nie powiedzie się. Należy usunąć istniejące zasoby hello wewnątrz podsieci hello przed utworzeniem nowej pamięci podręcznej Redis.

Można wdrożyć wiele typów o tooa zasoby klasyczne sieci wirtualnej tak długo, jak długo ma za mało IP adresów dostępne.

### <a name="what-are-hello-subnet-address-space-requirements"></a>Jakie są wymagania dotyczące miejsca na powitania podsieci adresów?
Azure rezerwuje niektórych adresów IP w każdej podsieci, a nie można użyć tych adresów. Witaj imię i nazwisko adresów IP podsieci hello są zastrzeżone dla protokołu zgodność, wraz z trzech więcej adresów używanych na potrzeby usług Azure. Aby uzyskać więcej informacji, zobacz [istnieją wszystkie ograniczenia dotyczące używania adresów IP w ramach tych podsieci?](../virtual-network/virtual-networks-faq.md#are-there-any-restrictions-on-using-ip-addresses-within-these-subnets)

W przypadku dodawania adresów IP toohello używanych przez infrastrukturę sieci Wirtualnej Azure hello każdy Redis wystąpienia adresów IP używa dwóch podsieci hello na niezależnych i jeden dodatkowy adres IP dla modułu równoważenia obciążenia hello. Pamięć podręczna nieklastrowanych jest uważany za toohave jednego niezależnego fragmentu.

### <a name="do-all-cache-features-work-when-hosting-a-cache-in-a-vnet"></a>Wszystkie funkcje pamięci podręcznej działają odnośnie do hostowania pamięci podręcznej w sieci Wirtualnej?
Jeśli pamięć podręczna jest częścią sieci Wirtualnej, tylko klienci w sieci Wirtualnej hello można uzyskać dostępu do pamięci podręcznej hello. W związku z tym hello następujące funkcje zarządzania pamięci podręcznej nie działają w tej chwili.

* Redis konsoli — konsoli Redis jest uruchamiana w przeglądarce lokalnego znajduje się poza hello sieci Wirtualnej, nie można połączyć z pamięci podręcznej tooyour.

## <a name="use-expressroute-with-azure-redis-cache"></a>Użyj usługi ExpressRoute z pamięcią podręczną Azure Redis
Klienci mogą się łączyć [Azure ExpressRoute](https://azure.microsoft.com/services/expressroute/) infrastruktury sieci wirtualnej tootheir obwód, w związku z tym rozszerzanie ich tooAzure sieci lokalnej. 

Domyślnie nowo utworzony obwodu usługi expressroute nie tunelowanie wymuszone (anons trasę domyślną wartość 0.0.0.0/0) w sieci Wirtualnej. W związku z tym wychodzące połączenie z Internetem jest dozwolona bezpośrednio z hello sieci Wirtualnej i aplikacje klienckie są możliwe tooconnect tooother Azure punktów końcowych, łącznie z pamięcią podręczną Redis Azure.

Typowa konfiguracja klienta jest wymuszone tunelowanie toouse (anonsowanie trasy domyślnej) który wymusza wychodzącego Internet ruchu tooinstead przepływu lokalnymi. Tego przepływu ruchu przerywa połączenie z pamięcią podręczną Redis Azure, jeśli ruch wychodzący hello jest następnie zablokowany lokalnego pozwalający hello wystąpienia pamięci podręcznej Redis Azure nie jest możliwe toocommunicate z jego zależności.

rozwiązanie Hello jest toodefine jednej (lub więcej) zdefiniowane przez użytkownika tras (Udr) na powitania podsieci, która zawiera hello pamięć podręczna Redis Azure. PRZEZ definiuje tras specyficzne dla podsieci, które będą honorowane zamiast hello trasy domyślnej.

Jeśli to możliwe zaleca się hello toouse następującej konfiguracji:

* konfiguracji usługi ExpressRoute Hello anonsuje 0.0.0.0/0 i domyślnie życie tuneli wszystkich ruch wychodzący lokalnymi.
* Hello stosowane przez toohello podsieć zawierająca hello pamięć podręczna Redis Azure definiuje 0.0.0.0/0 trasa pracy dla toohello ruchu TCP/IP publicznego Internetu; na przykład przez ustawienie hello następnego przeskoku too'Internet typu ".

Witaj połączony wpływ tych kroków jest hello na poziomie podsieci przez ma pierwszeństwo przed hello ExpressRoute wymuszone tunelowanie, w związku z tym zapewnienie wychodzący dostęp do Internetu z hello pamięć podręczna Redis Azure.

Łączącego wystąpienie pamięci podręcznej Redis Azure tooan z aplikacji lokalnych przy użyciu usługi ExpressRoute nie jest scenariuszem typowy sposób powodu przyczyn tooperformance (Aby uzyskać najlepszą wydajność pamięci podręcznej Redis Azure klienci powinni mieć w hello tego samego regionu hello pamięć podręczna Redis Azure).

>[!IMPORTANT] 
>Witaj tras określonych w przez **musi** można tootake wystarczająco konkretny, pierwszeństwo nad dowolnym trasy anonsowane przez hello konfiguracji usługi ExpressRoute. Witaj poniższy przykład używa zakresu adresów szerokie 0.0.0.0/0 hello i jako taki może potencjalnie być przypadkowo przesłonięta przez anonsów tras za pomocą bardziej szczegółowych zakresów adresów.

>[!WARNING]  
>Pamięć podręczna Redis Azure nie jest obsługiwany w konfiguracji usługi ExpressRoute który **niepoprawnie cross anonsowanie trasy z hello publicznej komunikacji równorzędnej ścieżka toohello prywatnej komunikacji równorzędnej ścieżka**. Konfiguracji usługi ExpressRoute, które mają publicznej komunikacji równorzędnej skonfigurowane, otrzymywać anonsów tras od firmy Microsoft dla dużych zestawów zakresów adresów IP firmy Microsoft Azure. Jeśli te zakresy adresów są niepoprawnie cross anonsowany w ścieżki prywatnej komunikacji równorzędnej hello, wynik hello są wszystkich pakietów sieciowych wychodzące z wystąpienia pamięci podręcznej Redis Azure hello podsieci sieci lokalnej klienta niepoprawnie tunneled życie tooa infrastruktura. Ten przepływ sieci dzieli pamięci podręcznej Redis Azure. problem toothis rozwiązania Hello jest toostop tras między reklamy hello publicznej komunikacji równorzędnej ścieżka toohello prywatnej komunikacji równorzędnej ścieżka.


Informacje na trasach zdefiniowanych przez użytkownika jest dostępna w tym [omówienie](../virtual-network/virtual-networks-udr-overview.md).

Aby uzyskać więcej informacji na temat połączenia ExpressRoute, zobacz [opis techniczny ExpressRoute](../expressroute/expressroute-introduction.md).

## <a name="next-steps"></a>Następne kroki
Dowiedz się, jak toouse premium więcej pamięci podręcznej funkcji.

* [Wprowadzenie toohello pamięci podręcznej Redis Azure Premium warstwy](cache-premium-tier-intro.md)

<!-- IMAGES -->

[redis-cache-vnet]: ./media/cache-how-to-premium-vnet/redis-cache-vnet.png

[redis-cache-vnet-ip]: ./media/cache-how-to-premium-vnet/redis-cache-vnet-ip.png

[redis-cache-vnet-info]: ./media/cache-how-to-premium-vnet/redis-cache-vnet-info.png

