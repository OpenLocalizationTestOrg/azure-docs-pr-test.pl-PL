---
title: "Omówienie usługi równoważenia obciążenia aaaAzure | Dokumentacja firmy Microsoft"
description: "Omówienie funkcji równoważenia obciążenia Azure, architektura i implementacji. Dowiedz się, jak działa usługa równoważenia obciążenia hello i wykorzystać go w chmurze hello."
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
ms.assetid: 0f313dc0-f007-4cee-b2b9-f542357925a3
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 2376a02f7cbbbed6a90f216419c0c3d30f594272
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-load-balancer-overview"></a>Omówienie usługi Azure Load Balancer

Moduł równoważenia obciążenia Azure zapewnia wysoką wydajność dostępności i sieci tooyour aplikacji. Jest równoważenia obciążenia warstwy 4 (TCP, UDP), który rozdziela przychodzący ruch między dobrej kondycji wystąpień usługi zdefiniowane w zestawie o zrównoważonym obciążeniu.

Moduł równoważenia obciążenia Azure można skonfigurować w celu:

* Obciążenie saldo przychodzące Internet ruchu toovirtual maszyn. Ta konfiguracja jest określana jako [równoważenia obciążenia internetowy](load-balancer-internet-overview.md).
* Ruch Równoważenie obciążenia między maszynami wirtualnymi w sieci wirtualnej, między maszynami wirtualnymi w usługi w chmurze lub między komputerami lokalnymi i maszyn wirtualnych w sieci wirtualnej między lokalizacjami. Ta konfiguracja jest określana jako [równoważenia obciążenia wewnętrznego](load-balancer-internal-overview.md).
* Przekazuje ruch zewnętrzny tooa określonej maszyny wirtualnej.

Wszystkie zasoby w chmurze hello muszą dostępny z Internetu hello publicznego toobe adresów IP. Hello infrastruktury chmury na platformie Azure używa bez obsługi routingu adresów IP do jej zasobów. Azure używa translatora adresów sieciowych (NAT) z adresów toocommunicate toohello Internet publicznego adresu IP.

## <a name="azure-deployment-models"></a>Modele wdrażania platformy Azure

Jest ważne toounderstand hello różnice między hello Azure classic i Menedżer zasobów [modele wdrażania](../azure-resource-manager/resource-manager-deployment-model.md). Moduł równoważenia obciążenia Azure jest konfigurowane różnie w każdym modelu.

### <a name="azure-classic-deployment-model"></a>Azure klasycznego modelu wdrażania

Maszyn wirtualnych wdrożonych w obrębie granicy usługi chmury mogą być zgrupowane toouse modułu równoważenia obciążenia. W tym modelu publicznego adresu IP i pełni kwalifikowana nazwa domeny, (FQDN) są przypisane tooa usługi w chmurze. Moduł równoważenia obciążenia Hello portu tłumaczenia i obciążenia równoważy hello ruchu sieciowego za pomocą hello publicznego adresu IP dla usługi w chmurze hello.

Ruch z równoważeniem obciążenia jest zdefiniowane przez punkty końcowe. Punkty końcowe tłumaczenia portu mają relacją między portu przypisany publicznego hello hello publicznego adresu IP i portu lokalnego hello przypisane usługi toohello na określonej maszyny wirtualnej. Punkty końcowe równoważenia obciążenia mają relacji jeden do wielu między hello publicznego adresu IP i usługami toohello przypisane porty lokalne powitania na maszynach wirtualnych hello hello w usłudze w chmurze.

![Moduł równoważenia obciążenia Azure w hello klasycznego modelu wdrażania](./media/load-balancer-overview/asm-lb.png)

Rysunek 1 - Azure usługi równoważenia obciążenia w hello klasycznego modelu wdrażania

Etykieta domeny Hello hello publiczny adres IP, który używa modułu równoważenia obciążenia dla tego modelu wdrażania hello jest \<nazwa usługi w chmurze\>. cloudapp.net. Witaj poniższy rysunek przedstawia hello modułu równoważenia obciążenia Azure w tym modelu.

### <a name="azure-resource-manager-deployment-model"></a>Model wdrażania usługi Azure Resource Manager

W modelu wdrażania usługi Resource Manager hello nie ma żadnych toocreate konieczność usługi w chmurze. Moduł równoważenia obciążenia Hello jest tworzony tooexplicitly kierować ruchem między wieloma maszynami wirtualnymi.

Publiczny adres IP jest pojedynczego zasobu, który zawiera etykietę domeny (nazwa DNS). Hello publiczny adres IP jest skojarzony z zasobem usługi równoważenia obciążenia hello. Reguły modułu równoważenia obciążenia i przychodzącej reguły NAT użyć hello publicznego adresu IP, który został hello punktu końcowego Internet hello zasobów, które są odbieranie ruchu sieciowego z równoważeniem obciążenia.

Prywatny lub publiczny adres IP jest przypisany maszyny wirtualnej tooa zasobów dołączony toohello sieci interfejsu. Po dodaniu puli adresów IP zaplecza tooa usługi równoważenia obciążenia interfejsu sieciowego hello modułu równoważenia obciążenia jest toosend stanie równoważeniem obciążenia ruchu sieciowego na podstawie równoważeniem obciążenia reguł hello, które są tworzone.

Witaj poniższy rysunek przedstawia hello Azure usługi równoważenia obciążenia w danym modelu:

![Równoważenia obciążenia Azure Resource Manager](./media/load-balancer-overview/arm-lb.png)

Rysunek 2 — równoważenia obciążenia Azure Resource Manager

Moduł równoważenia obciążenia Hello mogą być zarządzane za pomocą Menedżera zasobów na podstawie szablonów, interfejsów API i narzędzia. toolearn więcej o Resource Manager, zobacz hello [omówienie Resource Manager](../azure-resource-manager/resource-group-overview.md).

## <a name="load-balancer-features"></a>Funkcje równoważenia obciążenia

* Dystrybucji wyznaczania wartości skrótu

    Moduł równoważenia obciążenia Azure używa algorytmu wyznaczania wartości skrótu dystrybucji. Domyślnie używa skrót 5-elementowej składa się z źródłowy adres IP, port źródłowy, docelowy adres IP, docelowy port i protokół typu toomap ruchu tooavailable serwerów. Zapewnia tylko lepkości *w* sesji transportu. Pakietów hello tej samej sesji TCP lub UDP zostanie przekierowany toohello samo wystąpienie za punktem końcowym hello równoważeniem obciążenia. Gdy powitania klienta zostanie zamknięte i ponownie otwiera połączenia hello lub uruchamia nową sesję z hello tego samego źródłowego adresu IP, zmiany portu źródłowego hello. Może to spowodować hello ruchu toogo tooa innym punktem końcowym w różnych centrach danych.

    Aby uzyskać więcej informacji, zobacz [tryb dystrybucji modułu równoważenia obciążenia](load-balancer-distribution-mode.md). Witaj poniższy rysunek przedstawia dystrybucji hello wyznaczania wartości skrótu:

    ![Dystrybucji wyznaczania wartości skrótu](./media/load-balancer-overview/load-balancer-distribution.png)

    Rysunek 3 – skrótu na podstawie dystrybucji

* Przekierowanie portów

    Sterowanie za pośrednictwem komunikacji przychodzącej jak odbywa się Azure oferuje usługi równoważenia obciążenia. Ta komunikacja ruch inicjowane z Internetu hosty, maszyny wirtualne w innych usług w chmurze lub sieci wirtualne. Ten formant jest reprezentowany przez punkt końcowy (nazywanych również wejściowy punkt końcowy).

    Wejściowy punkt końcowy nasłuchuje na porcie publicznego i przekazuje ruch tooan wewnętrznego portu. Można mapować hello takie same porty dla wewnętrznego lub zewnętrznego punktu końcowego lub użyć innego portu dla nich. Na przykład może mieć tooport toolisten skonfigurowanego serwera sieci web 81 podczas mapowania publiczny punkt końcowy hello jest port 80. Tworzenie Hello publiczny punkt końcowy wyzwala hello utworzenie wystąpienia usługi równoważenia obciążenia.

    Gdy utworzona za pomocą hello portalu Azure, portalu hello automatycznie tworzy maszynę wirtualną toohello punktów końcowych dla hello protokołu RDP (Remote Desktop) i zdalnego ruch w sesji środowiska Windows PowerShell. Można użyć tych punktów końcowych tooremotely administrować hello maszyny wirtualnej za pośrednictwem hello Internet.

* Automatyczna ponowna konfiguracja

    Moduł równoważenia obciążenia Azure natychmiast ponownie konfiguruje się wystąpień skalowanie w górę lub w dół. Na przykład tego procesu ponownej konfiguracji odbywa się wraz ze zwiększeniem, hello liczba wystąpień ról sieć web/proces roboczy w usłudze w chmurze lub podczas dodawania kolejnych maszyn wirtualnych do hello Ustaw sam równoważeniem obciążenia.

* Monitorowanie usługi

    Moduł równoważenia obciążenia Azure można badania kondycji hello hello różne wystąpienia serwera. W przypadku awarii toorespond sondę modułu równoważenia obciążenia hello zatrzymuje, wysyłanie nowych połączeń toohello złej kondycji wystąpień. Nie dotyczy istniejących połączeń.

    Obsługiwane są trzy typy sond:

    + **Sondowanie agenta gościa (na platformie jako usługa maszyn wirtualnych tylko):** hello agenta gościa w maszynie wirtualnej hello korzysta z usługi równoważenia obciążenia hello. Hello agenta gościa wykrywa i wysyła odpowiedź HTTP 200 OK tylko wtedy, gdy hello wystąpienie jest w stanie gotowe hello (tj. hello wystąpienia nie jest w stanie tak zajęty, odtwarzanie lub zatrzymywanie). W przypadku niepowodzenia toorespond HTTP 200 OK agenta hello znaczniki usługi równoważenia obciążenia hello hello wystąpienia jako odpowiadać i kończy działanie wysyłania ruchu toothat wystąpienia. Moduł równoważenia obciążenia Hello nadal tooping hello wystąpienia. Agent gościa hello odpowie 200 protokołu HTTP, hello modułu równoważenia obciążenia będzie wysyłać ruch toothat wystąpienia ponownie. Podczas korzystania z roli sieci web, kodu witryny sieci Web jest zwykle działa w w3wp.exe, który nie jest monitorowane przez hello Azure sieci szkieletowej lub agenta gościa. To oznacza, że błędy w w3wp.exe (np. w odpowiedzi HTTP 500) nie będzie toohello zgłoszone agenta gościa, a hello modułu równoważenia obciążenia nie będzie wiedzieć, tootake danego wystąpienia poza obrotu.
    + **Niestandardowe badanie HTTP:** sonda zastępuje hello domyślnej funkcji badania (agenta gościa). Można użyć toocreate kondycję hello toodetermine niestandardowej logiki własne hello wystąpienia roli. Moduł równoważenia obciążenia Hello będzie regularnie sondowania punktu końcowego (co 15 sekund, domyślnie). wystąpienie Hello jest uznawany za toobe rotacji, jeśli odpowiada 200 protokołu HTTP lub TCP potwierdzenia w hello limicie czasu (domyślnie 31 sekund). Jest to przydatne wykonywania własnego wystąpienia tooremove logiki z obrotu hello usługi równoważenia obciążenia. Na przykład można skonfigurować hello wystąpienia tooreturn stan – 200, jeśli wystąpienie hello jest ponad 90% zasobów Procesora. Dla role sieci web, które używają w3wp.exe, możesz również uzyskać automatyczne monitorowania witryny sieci Web, ponieważ badanie stanu – 200 toohello zwracać błędów w kodzie witryny sieci Web.
    + **Niestandardowe sondowaniem TCP:** sonda opiera się na pomyślne port sondy tooa zdefiniowane ustanowienia TCP sesji.

    Aby uzyskać więcej informacji, zobacz hello [schematu LoadBalancerProbe](https://msdn.microsoft.com/library/azure/jj151530.aspx).

* Źródło translatora adresów Sieciowych

    Wszystkie toohello ruch wychodzący Internetu, która pochodzi z usługi podlega źródła translatora adresów Sieciowych (SNAT) przy użyciu hello tego samego adresu VIP, ponieważ hello ruchu przychodzącego. SNAT oferuje istotne korzyści:

    + Umożliwia on łatwe uaktualnianie i odzyskiwanie po awarii usługi, ponieważ hello VIP można dynamicznie mapowane tooanother wystąpienie usługi hello.
    + Ułatwia ona zarządzanie listę kontroli dostępu (ACL) kontrolą dostępu. Listy kontroli dostępu w przeliczeniu na adresy VIP nie zmieniaj jako skalowania usługi w górę, dół, lub pobrać ponownej instalacji.

    konfiguracji usługi równoważenia obciążenia Hello obsługuje pełne stożkowy NAT UDP. Pełna stożkowy translatora adresów Sieciowych jest typem translatora adresów Sieciowych, gdzie hello port zezwala na połączenia przychodzące z dowolnym hostem zewnętrznych (w odpowiedzi żądania wychodzącego tooan).

    Dla każdego nowego wychodzące połączenie, które inicjuje maszynę wirtualną portu wychodzącego również jest przydzielany przez hello równoważenia obciążenia. hoście zewnętrznym Hello widzi ruch przydzielone wirtualne adresy IP IP portu wirtualnego. Scenariusze, które wymagają dużej liczby połączeń wychodzących, zalecane jest toouse [poziomie wystąpienia publicznego adresu IP](../virtual-network/virtual-networks-instance-level-public-ip.md) adresów hello maszyny wirtualne mają SNAT dedykowany adres IP ruchu wychodzącego. Zmniejsza ryzyko hello wyczerpania portu.

    Zobacz [połączeń wychodzących](load-balancer-outbound-connections.md) artykułu, aby uzyskać więcej informacji na ten temat.

### <a name="support-for-multiple-load-balanced-ip-addresses-for-virtual-machines"></a>Obsługa wielu adresów IP z równoważeniem obciążenia dla maszyn wirtualnych
Można przypisać więcej niż jeden z równoważeniem obciążenia publicznego zbiór adresów IP tooa maszyn wirtualnych. Z tej możliwości może obsługiwać wiele witryn sieci Web protokołu SSL i/lub wielu odbiorniki grupy dostępności AlwaysOn programu SQL Server na powitania sam zestaw maszyn wirtualnych. Aby uzyskać więcej informacji, zobacz [wieloma wirtualnymi adresami IP dla danej usługi chmury](load-balancer-multivip.md).

[!INCLUDE [load-balancer-compare-tm-ag-lb-include.md](../../includes/load-balancer-compare-tm-ag-lb-include.md)]

## <a name="limitations"></a>Ograniczenia

Pul zaplecza modułu równoważenia obciążenia może zawierać żadnych SKU maszyny Wirtualnej, z wyjątkiem warstwy podstawowa.

## <a name="next-steps"></a>Następne kroki

- Dowiedz się więcej o [internetowy modułu równoważenia obciążenia](load-balancer-internet-overview.md)

- Dowiedz się więcej o [Omówienie usługi równoważenia obciążenia wewnętrznego](load-balancer-internal-overview.md)

- Utwórz [internetowy modułu równoważenia obciążenia](load-balancer-get-started-internet-portal.md)

- Dowiedz się więcej o niektórych hello innego klucza [możliwości w zakresie obsługi](../networking/networking-overview.md) platformy Azure

