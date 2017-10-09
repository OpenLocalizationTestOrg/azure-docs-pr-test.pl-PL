---
title: aaaVirtual sieci i maszyn wirtualnych systemu Windows na platformie Azure | Dokumentacja firmy Microsoft
description: "Więcej informacji na temat sieci pod kątem toohello podstawy tworzenia maszyn wirtualnych systemu Windows na platformie Azure."
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 5493e9f7-7d45-4e98-be9a-657a53708746
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: davidmu
ms.openlocfilehash: e28a4782f9f6c69f6101e45dbb560ccd694a1e07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-networks-and-windows-virtual-machines-in-azure"></a>Sieci wirtualne i maszyny wirtualne z systemem Windows na platformie Azure 

Utworzenie maszyny wirtualnej (VM) platformy Azure wymaga utworzenia [sieci wirtualnej](../../virtual-network/virtual-networks-overview.md) (VNet) lub użycia istniejącej sieci wirtualnej. Należy również toodecide jak maszyny wirtualne są zamierzone toobe dostępny na powitania sieci wirtualnej. Ważne jest zbyt[planu przed utworzeniem zasobów](../../virtual-network/virtual-network-vnet-plan-design-arm.md) i upewnij się, że rozumiesz hello [limitów zasobów sieciowych](../../azure-subscription-service-limits.md#networking-limits).

W następującej ilustracji hello maszyny wirtualne są reprezentowane jako serwery sieci web i serwery bazy danych. Każdy zestaw maszyn wirtualnych przypisanych podsieci tooseparate w hello sieci wirtualnej.

![Sieć wirtualna Azure](./media/network-overview/vnetoverview.png)

Aby utworzyć Maszynę wirtualną lub hello sieci wirtualnej można utworzyć podczas tworzenia maszyny Wirtualnej można utworzyć sieci wirtualnej. W drugim przypadku sieć wirtualna jest tworzona automatycznie w czasie tworzenia maszyny wirtualnej.

Te zasoby możesz tworzyć toosupport komunikacji z maszyny Wirtualnej:

- Interfejsy sieciowe
- Adresy IP
- Sieć wirtualna i podsieci

Ponadto toothose zasoby podstawowe, należy również rozważyć tych opcjonalnych zasobów:

- Grupy zabezpieczeń sieci
- Moduły równoważenia obciążenia 

## <a name="network-interfaces"></a>Interfejsy sieciowe

A [interfejsu sieciowego (NIC)](../../virtual-network/virtual-network-network-interface.md) jest hello połączenia między Maszynę wirtualną i sieć wirtualną (VNet). Maszyna wirtualna musi mieć co najmniej jednej karty Sieciowej, ale może zawierać więcej niż jeden, w zależności od rozmiaru hello hello tworzenia maszyny Wirtualnej. Aby dowiedzieć się, ile kart sieciowych mogą obsługiwać maszyny wirtualne o konkretnym rozmiarze, zobacz [Rozmiary maszyn wirtualnych na platformie Azure](sizes.md). 

Jeśli chcesz toocreate maszyny Wirtualnej z więcej niż jedną kartą Sieciową, należy utworzyć hello maszyny Wirtualnej przy użyciu co najmniej dwóch.  Po utworzeniu można dodać dodatkowe karty sieciowe numer toohello obsługiwane przez hello rozmiar maszyny Wirtualnej, ale nie można dodać dodatkowe karty sieciowe tooa tworzyć tylko z jednej maszyny Wirtualnej, niezależnie od tego, jak wiele kart sieciowych obsługuje hello rozmiar maszyny Wirtualnej. 

Jeśli hello maszyny Wirtualnej zostanie dodany zestaw dostępności tooan, wszystkich maszyn wirtualnych w zestawie dostępności hello musi mieć jednego lub wielu kart sieciowych. Maszyny wirtualne z więcej niż jednej karty Sieciowej nie są wymagane toohave hello samą liczbę kart sieciowych, ale ich muszą mieć co najmniej dwóch.

Każdy tooa kartę Sieciową podłączoną, maszyna wirtualna musi znajdować się w hello tej samej lokalizacji i subskrypcji, jak hello maszyny Wirtualnej. Każda karta sieciowa musi być tooa połączonych sieci wirtualnej, który istnieje w hello takie same lokalizacji platformy Azure i subskrypcji, jak hello karty sieciowej. Po utworzeniu karty Sieciowej, można zmienić podsieci hello, w której jest dołączona do, ale nie można zmienić hello jest podłączony do sieci wirtualnej.  Poszczególne karty Sieciowe dołączony tooa, że maszyna wirtualna jest przypisany adres MAC, które nie zmieniają się do momentu usunięcia hello maszyny Wirtualnej.

Poniższa tabela zawiera metody hello służy toocreate interfejsu sieciowego.

| Metoda | Opis |
| ------ | ----------- |
| Azure Portal | Po utworzeniu maszyny Wirtualnej w portalu Azure hello interfejs sieciowy jest utworzony automatycznie (nie można użyć karty Sieciowej są tworzone oddzielnie). Hello portal tworzy Maszynę wirtualną z tylko jedną kartę sieciową. Jeśli chcesz toocreate maszyny Wirtualnej z więcej niż jedną kartą Sieciową, należy utworzyć ją za pomocą innej metody. |
| [Azure PowerShell](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md) | Użyj [AzureRmNetworkInterface nowy](/powershell/module/azurerm.network/new-azurermnetworkinterface) z hello **- PublicIpAddressId** parametru tooprovide hello identyfikatorem hello publicznego adresu IP utworzony wcześniej. |
| [Interfejs wiersza polecenia platformy Azure](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md) | Identyfikator hello tooprovide hello publicznego adresu IP adresów, które utworzonego wcześniej, użyj [tworzenie kart interfejsu sieciowego az](https://docs.microsoft.com/cli/azure/network/nic#create) z hello **— publiczny adres** parametru. |
| [Szablon](../../virtual-network/virtual-network-deploy-multinic-arm-template.md) | Przewodnik [Interfejs sieciowy w sieci wirtualnej z publicznym adresem IP](https://github.com/Azure/azure-quickstart-templates/tree/master/101-nic-publicip-dns-vnet) ułatwia wdrożenie interfejsu sieciowego przy użyciu szablonu. |

## <a name="ip-addresses"></a>Adresy IP 

Można przypisać tego typu [adresów IP](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) tooa karty Sieciowej na platformie Azure:

- **Publiczne adresy IP** — używane toocommunicate ruchu przychodzącego i wychodzącego (bez translatora adresów sieciowych (NAT)) z hello internetowych i innych zasobów platformy Azure niepołączone tooa sieci wirtualnej. Przypisywanie publicznego tooa adresu IP karty Sieciowej jest opcjonalna. Za korzystanie z publicznych adresów IP są naliczane nominalne opłaty. Dodatkowo istnieje ograniczenie liczby adresów używanych w ramach jednej subskrypcji.
- **Adresy IP prywatnego** — używana do komunikacji w sieci wirtualnej, sieci lokalnej i hello Internetem (NAT). Należy przypisać co najmniej jednego prywatnego tooa adres IP maszyny Wirtualnej. toolearn więcej informacji na temat translatora adresów Sieciowych na platformie Azure, przeczytaj [Opis połączeń wychodzących na platformie Azure](../../load-balancer/load-balancer-outbound-connections.md).

Można przypisać publicznego tooVMs adresy IP lub internetowy usług równoważenia obciążenia. Można przypisać prywatnej tooVMs adresów IP i wewnętrzne moduły równoważenia obciążenia. Można przypisać tooa adresów IP maszyny Wirtualnej przy użyciu interfejsu sieciowego.

Istnieją dwie metody, w których jest przydzielić zasób tooa - dynamicznej lub statycznej adresu IP. Metoda alokacji domyślne Hello jest dynamiczny, w przypadku, gdy adres IP nie jest przydzielony podczas jego tworzenia. Zamiast tego adresu IP hello zaalokowano podczas tworzenia maszyny Wirtualnej lub uruchamiania zatrzymanej maszyny Wirtualnej. adres IP Hello jest zwalniany, kiedy należy zatrzymać lub usunąć hello maszyny Wirtualnej. 

adres IP hello tooensure hello maszyna wirtualna pozostaje hello takie same, można ustawić jawnie metodę alokacji hello toostatic. W takim przypadku adres IP jest przypisywany natychmiast. Po uwolnieniu tylko wtedy, gdy usunięcie hello maszyny Wirtualnej lub zmienić jego toodynamic metodę alokacji.
    
Poniższa tabela zawiera metody hello służy toocreate adresu IP.

| Metoda | Opis |
| ------ | ----------- |
| [Witryna Azure Portal](../../virtual-network/virtual-network-deploy-static-pip-arm-portal.md) | Domyślnie publiczne adresy IP są dynamiczne i toothem adres skojarzony hello może ulec zmianie po hello maszyny Wirtualnej jest zatrzymana lub usunięty. tooguarantee, który zawsze hello maszyna wirtualna używa hello sam publiczny adres IP, należy utworzyć statycznego publicznego adresu IP. Domyślnie hello portal przypisuje dynamiczne prywatnego adresu IP adres tooa karty Sieciowej, podczas tworzenia maszyny Wirtualnej. Ten toostatic można zmienić po hello utworzenia maszyny Wirtualnej.|
| [Azure PowerShell](../../virtual-network/virtual-network-deploy-static-pip-arm-ps.md) | Możesz użyć [AzureRmPublicIpAddress nowy](/powershell/module/azurerm.network/new-azurermpublicipaddress) z hello **- AllocationMethod** parametr jako dynamicznej lub statycznej. |
| [Interfejs wiersza polecenia platformy Azure](../../virtual-network/virtual-network-deploy-static-pip-arm-cli.md) | Używasz [utworzyć az sieci publicznej ip](https://docs.microsoft.com/cli/azure/network/public-ip#create) z hello **— metoda alokacji** parametr jako dynamicznej lub statycznej. |
| [Szablon](../../virtual-network/virtual-network-deploy-static-pip-arm-template.md) | Przewodnik [Interfejs sieciowy w sieci wirtualnej z publicznym adresem IP](https://github.com/Azure/azure-quickstart-templates/tree/master/101-nic-publicip-dns-vnet) ułatwia wdrożenie publicznego adresu IP przy użyciu szablonu. |

Po utworzeniu publicznego adresu IP, można ją skojarzyć z maszyny Wirtualnej przypisując tooa karty sieciowej.

## <a name="virtual-network-and-subnets"></a>Sieć wirtualna i podsieci

Podsieć to zakres adresów IP w hello sieci wirtualnej. Sieć wirtualną można podzielić na wiele podsieci w celu jej uporządkowania i zapewnienia bezpieczeństwa. Poszczególne karty Sieciowe w maszynie Wirtualnej jest połączonych tooone podsieci w jednej sieci wirtualnej. Karty sieciowe połączone toosubnets (tych samych lub różnych) w ramach sieci wirtualnej mogą komunikować się ze sobą bez dodatkowego konfigurowania.

Po skonfigurowaniu sieci wirtualnej można określić topologię hello, łącznie ze spacjami dostępny adres hello i podsieci. Jeśli hello sieci wirtualnej jest tooother toobe połączone sieci wirtualne lub lokalnej sieci, należy wybrać zakresów adresów, które nie nakładają się. adresy IP Hello są prywatne i jest niedostępny z Internetu, która była wartość true tylko w przypadku hello-routeable adresów IP, np. 10.0.0.0/8, 172.16.0.0/12 lub 192.168.0.0/16 hello. Teraz Azure traktuje wszystkie zakres adresów jako część hello prywatnej sieci wirtualnej przestrzeni adresów IP będzie on dostępny w ramach hello sieci wirtualnej, w ramach połączonych sieci wirtualnych i z lokalizacji lokalnej. 

Jeśli pracujesz w organizacji ktoś jest odpowiedzialny za hello sieciach wewnętrznych, należy skontaktować osoby toothat przed wybraniem przestrzeń adresowa. Upewnij się, że nie pokrywają się i powiadom go hello odstępu toouse tak nie próbują toouse hello tego samego zakresu adresów IP. 

Domyślnie między podsieciami, więc maszyn wirtualnych w każdym z tych podsieci można rozmawiać tooone jest nie granicy zabezpieczeń innego. Można jednak skonfigurować grupy zabezpieczeń sieci (NSG), które pozwalają toocontrol hello ruchu przepływu tooand z podsieci i tooand z maszyn wirtualnych. 

Poniższa tabela zawiera metody hello umożliwia toocreate sieci wirtualnej i podsieci.   

| Metoda | Opis |
| ------ | ----------- |
| [Witryna Azure Portal](../../virtual-network/virtual-networks-create-vnet-arm-pportal.md) | Jeśli umożliwisz utworzyć sieć wirtualną podczas tworzenia maszyny Wirtualnej Azure, nazwa hello jest kombinacją hello Nazwa grupy zasobów, zawierającą hello sieci wirtualnej i **- vnet**. przestrzeń adresowa Hello jest 10.0.0.0/24, Nazwa podsieci wymagane hello jest **domyślne**, i zakres adresów podsieci hello jest 10.0.0.0/24. |
| [Azure PowerShell](../../virtual-network/virtual-networks-create-vnet-arm-ps.md) | Możesz użyć [AzureRmVirtualNetworkSubnetConfig nowy](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmVirtualNetworkSubnetConfig) i [New-AzureRmVirtualNetwork](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmVirtualNetwork) toocreate podsieci i sieci wirtualnej. Można również użyć [AzureRmVirtualNetworkSubnetConfig Dodaj](/powershell/module/azurerm.network/add-azurermvirtualnetworksubnetconfig) tooadd tooan podsieci istniejącej sieci wirtualnej. |
| [Interfejs wiersza polecenia platformy Azure](../../virtual-network/virtual-networks-create-vnet-arm-cli.md) | Witaj podsieci i sieci wirtualnej hello są tworzone w hello sam czas. Podaj **— Nazwa podsieci** parametru zbyt[tworzenie sieci wirtualnej sieci az](https://docs.microsoft.com/cli/azure/network/vnet#create) nazwą podsieci hello. |
| [Szablon](../../virtual-network/virtual-networks-create-vnet-arm-template-click.md) | Witaj Najprostszym sposobem toocreate sieci wirtualnej i podsieci jest toodownload istniejącego szablonu, takie jak [sieci wirtualnej z dwoma podsieciami](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets)i zmodyfikuj go do potrzeb. |

## <a name="network-security-groups"></a>Grupy zabezpieczeń sieci

A [grupy zabezpieczeń sieci (NSG)](../../virtual-network/virtual-networks-nsg.md) zawiera listę reguł listy kontroli dostępu (ACL), które lub odmawiają toosubnets ruchu sieciowego i karty sieciowe. Grupy NSG można kojarzyć z podsieciami lub poszczególnych podsieci tooa połączonych kart sieciowych. Gdy grupa NSG jest skojarzona z podsiecią, reguły listy ACL hello zastosować tooall hello maszyn wirtualnych w tej podsieci. Ponadto ruch tooan poszczególnych kart interfejsu Sieciowego można ograniczyć przez skojarzenie grupy NSG bezpośrednio tooa karty sieciowej.

Sieciowe grupy zabezpieczeń zawierają dwa zestawy reguł: zestaw reguł przychodzących i wychodzących. Witaj priorytety reguł muszą być unikatowe w każdym z nich. Każda reguła ma właściwości protokołu, zakresów portów źródłowych i docelowych, prefiksów adresów, kierunku ruchu, priorytetu i typu dostępu. 

Wszystkie sieciowe grupy zabezpieczeń zawierają zestaw reguł domyślnych. Nie można usunąć reguły domyślne Hello, ale ponieważ mają przypisany najniższy priorytet hello, mogą być zastąpione przez hello utworzonych reguł. 

Po skojarzeniu grupy NSG tooa kart hello reguły dostępu do sieci w hello NSG są stosowane tylko toothat karty sieciowej. Jeśli grupa NSG jest stosowane tooa pojedyncza karta sieciowa w maszynie Wirtualnej wieloma kartami Sieciowymi, nie dotyczy ruchu toohello inne karty sieciowe. Można skojarzyć różne grupy NSG tooa karty Sieciowej (lub maszyny Wirtualnej, w zależności od modelu wdrażania hello) i hello podsieci, która jest powiązana karta sieciowa lub maszyna wirtualna. Priorytet znajduje się na podstawie hello kierunek ruchu.

Upewnij się, zbyt[planu](../../virtual-network/virtual-networks-nsg.md#planning) NSG podczas planowania maszyn wirtualnych i sieci wirtualnej.

Poniższa tabela zawiera metody hello służy toocreate grupy zabezpieczeń sieci.

| Metoda | Opis |
| ------ | ----------- |
| [Witryna Azure Portal](../../virtual-network/virtual-networks-create-nsg-arm-pportal.md) | Po utworzeniu maszyny Wirtualnej w portalu Azure hello grupa NSG jest tworzona automatycznie i tworzy skojarzone toohello kart hello portalu. Nazwa Hello hello NSG jest kombinacją nazwy hello hello maszyny Wirtualnej i **- nsg**. Ta grupa NSG zawiera jedną regułę ruchu przychodzącego z priorytet 1000, tooRDP zestawu usługi, tooTCP zestaw protokołu hello too3389 ustawiony port i tooAllow ustawić akcji. Jeśli chcesz tooallow żadnych innych ruch przychodzący toohello maszyny Wirtualnej, należy dodać toohello dodatkowe reguły NSG. |
| [Azure PowerShell](../../virtual-network/virtual-networks-create-nsg-arm-ps.md) | Użyj [AzureRmNetworkSecurityRuleConfig nowy](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmNetworkSecurityRuleConfig) hello wymagany regułę informacje. Użyj [AzureRmNetworkSecurityGroup nowy](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmNetworkSecurityGroup) toocreate hello NSG. Użyj [AzureRmVirtualNetworkSubnetConfig zestaw](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/Set-AzureRmVirtualNetworkSubnetConfig) hello tooconfigure NSG dla podsieci hello. Użyj [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork) tooadd hello NSG toohello sieci wirtualnej. |
| [Interfejs wiersza polecenia platformy Azure](../../virtual-network/virtual-networks-create-nsg-arm-cli.md) | Użyj [utworzyć nsg sieci az](https://docs.microsoft.com/cli/azure/network/nsg#create) tooinitially utworzyć hello NSG. Użyj [Tworzenie reguły nsg sieci az](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) tooadd zasady toohello NSG. Użyj [zaktualizować podsieci sieci wirtualnej sieci az](https://docs.microsoft.com/en-us/cli/azure/network/vnet/subnet#update) tooadd hello NSG toohello podsieci. |
| [Szablon](../../virtual-network/virtual-networks-create-nsg-arm-template.md) | Przewodnik [Tworzenie sieciowej grupy zabezpieczeń](https://github.com/Azure/azure-quickstart-templates/tree/master/101-security-group-create) ułatwia wdrożenie sieciowej grupy zabezpieczeń przy użyciu szablonu. |

## <a name="load-balancers"></a>Moduły równoważenia obciążenia

[Moduł równoważenia obciążenia Azure](../../load-balancer/load-balancer-overview.md) zapewnia wysoką dostępność i sieci wydajność tooyour aplikacji. Moduł równoważenia obciążenia można skonfigurować za[saldo przychodzącego ruchu internetowego](../../load-balancer/load-balancer-internet-overview.md) tooVMs lub [równoważenie ruchu między maszynami wirtualnymi w sieci wirtualnej](../../load-balancer/load-balancer-internal-overview.md). Moduł równoważenia obciążenia umożliwiają równoważenie również ruch między komputerami lokalnymi i maszyn wirtualnych w sieci między lokalizacjami lub tooa przekazywać ruch zewnętrzny określonej maszyny Wirtualnej.

Witaj obciążenia równoważenia mapy ruchu przychodzącego i wychodzącego między hello publiczny adres IP i port na powitania modułu równoważenia obciążenia i hello prywatnego adresu IP i portu hello maszyny Wirtualnej.

Podczas tworzenia modułu równoważenia obciążenia należy również wziąć pod uwagę te elementy konfiguracji:

- **Konfiguracja adresów IP frontonu** — moduł równoważenia obciążenia może zawierać jeden lub większą liczbę adresów IP frontonu, znanych także jako wirtualne adresy IP (VIP). Te adresy IP stanowią wejściowych hello ruchu.
- **Pula adresów zaplecza** — dystrybucji adresów IP, które są skojarzone z hello kart toowhich obciążenia.
- **Reguły NAT** — definiuje sposób przychodzący ruch przez hello IP frontonu i adres IP zaplecza toohello rozproszonych.
- **Reguły modułu równoważenia obciążenia** -mapuje danego adresu IP frontonu i portu kombinacja tooa zbiór adresów IP zaplecza i portu kombinacji. Moduł równoważenia obciążenia może mieć różne reguły równoważenia obciążenia. Każda reguła zawiera kombinację adresu IP frontonu i portu oraz adresu IP zaplecza i portu, które są powiązane z maszynami wirtualnymi.
- **[Sondy](../../load-balancer/load-balancer-custom-probe-overview.md)**  -monitorów hello kondycji maszyn wirtualnych. W przypadku awarii toorespond sondę modułu równoważenia obciążenia hello zatrzymuje wysyłanie nowych połączeń toohello złej kondycji maszyny Wirtualnej. nie dotyczy Hello istniejących połączeń i nowych połączeń są wysyłane toohealthy maszyn wirtualnych.

Poniższa tabela zawiera metody hello służy toocreate do modułu równoważenia obciążenia skierowane do Internetu.

| Metoda | Opis |
| ------ | ----------- |
| Azure Portal | Obecnie nie można utworzyć modułu równoważenia obciążenia skierowane do Internetu za pomocą hello portalu Azure. |
| [Azure PowerShell](../../load-balancer/load-balancer-get-started-internet-arm-ps.md) | Identyfikator hello tooprovide hello publicznego adresu IP adresów, które utworzonego wcześniej, użyj [AzureRmLoadBalancerFrontendIpConfig nowy](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerFrontendIpConfig) z hello **- publicznego adresu IP** parametru. Użyj [AzureRmLoadBalancerBackendAddressPoolConfig nowy](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerBackendAddressPoolConfig) toocreate hello konfiguracji hello puli adresów zaplecza. Użyj [AzureRmLoadBalancerInboundNatRuleConfig nowy](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerInboundNatRuleConfig) toocreate przychodzącej reguły NAT skojarzone z hello frontonu konfiguracji IP utworzony. Użyj [AzureRmLoadBalancerProbeConfig nowy](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerProbeConfig) toocreate hello sondy, że należy. Użyj [AzureRmLoadBalancerRuleConfig nowy](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerRuleConfig) konfiguracji usługi równoważenia obciążenia hello toocreate. Użyj [AzureRmLoadBalancer nowy](/powershell/module/azurerm.network/new-azurermloadbalancer) modułu równoważenia obciążenia hello toocreate.|
| [Interfejs wiersza polecenia platformy Azure](../../load-balancer/load-balancer-get-started-internet-arm-cli.md) | Użyj [utworzyć równoważeniem obciążenia sieciowego az](https://docs.microsoft.com/cli/azure/network/lb#create) konfiguracji usługi równoważenia obciążenia początkowej hello toocreate. Użyj [utworzyć az sieci lb-ip frontonu](https://docs.microsoft.com/cli/azure/network/lb/frontend-ip#create) tooadd hello publiczny adres IP, który wcześniej utworzony. Użyj [az lb puli adresów sieciowych — tworzenie](https://docs.microsoft.com/cli/azure/network/lb/address-pool#create) tooadd hello konfiguracji hello puli adresów zaplecza. Użyj [az sieci lb ruchu przychodzącego translatora adresów sieciowych — reguły tworzenia](https://docs.microsoft.com/cli/azure/network/lb/inbound-nat-rule#create) reguł NAT tooadd. Użyj [utworzyć regułę równoważeniem obciążenia sieciowego az](https://docs.microsoft.com/cli/azure/network/lb/rule#create) reguły modułu równoważenia obciążenia hello tooadd. Użyj [utworzyć sondy równoważeniem obciążenia sieciowego az](https://docs.microsoft.com/cli/azure/network/lb/probe#create) tooadd hello sondy. |
| [Szablon](../../load-balancer/load-balancer-get-started-internet-arm-template.md) | Użyj [2 maszyny wirtualne w usłudze równoważenia obciążenia i skonfigurować reguły NAT na powitania LB](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-loadbalancer-natrules) wskazówki dotyczące wdrażania usługi równoważenia obciążenia przy użyciu szablonu. |
    
Poniższa tabela zawiera metody hello służy toocreate wewnętrznego modułu równoważenia obciążenia.

| Metoda | Opis |
| ------ | ----------- |
| Azure Portal | Nie można obecnie utworzyć wewnętrznego modułu równoważenia obciążenia przy użyciu hello portalu Azure. |
| [Azure PowerShell](../../load-balancer/load-balancer-get-started-ilb-arm-ps.md) | tooprovide prywatnego adresu IP w podsieci sieci hello, użyj [AzureRmLoadBalancerFrontendIpConfig nowy](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerFrontendIpConfig) z hello **elementu PrivateIpAddress -** parametru. Użyj [AzureRmLoadBalancerBackendAddressPoolConfig nowy](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerBackendAddressPoolConfig) toocreate hello konfiguracji hello puli adresów zaplecza. Użyj [AzureRmLoadBalancerInboundNatRuleConfig nowy](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerInboundNatRuleConfig) toocreate przychodzącej reguły NAT skojarzone z hello frontonu konfiguracji IP utworzony. Użyj [AzureRmLoadBalancerProbeConfig nowy](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerProbeConfig) toocreate hello sondy, że należy. Użyj [AzureRmLoadBalancerRuleConfig nowy](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerRuleConfig) konfiguracji usługi równoważenia obciążenia hello toocreate. Użyj [AzureRmLoadBalancer nowy](/powershell/module/azurerm.network/new-azurermloadbalancer) modułu równoważenia obciążenia hello toocreate.|
| [Interfejs wiersza polecenia platformy Azure](../../load-balancer/load-balancer-get-started-ilb-arm-cli.md) | Użyj hello [utworzyć równoważeniem obciążenia sieciowego az](https://docs.microsoft.com/cli/azure/network/lb#create) konfiguracji usługi równoważenia obciążenia początkowej hello toocreate polecenia. toodefine hello prywatnego adresu IP, użyj [utworzyć az sieci lb-ip frontonu](https://docs.microsoft.com/cli/azure/network/lb/frontend-ip#create) z hello **— prywatny adres ip** parametru. Użyj [az lb puli adresów sieciowych — tworzenie](https://docs.microsoft.com/cli/azure/network/lb/address-pool#create) tooadd hello konfiguracji hello puli adresów zaplecza. Użyj [az sieci lb ruchu przychodzącego translatora adresów sieciowych — reguły tworzenia](https://docs.microsoft.com/cli/azure/network/lb/inbound-nat-rule#create) reguł NAT tooadd. Użyj [utworzyć regułę równoważeniem obciążenia sieciowego az](https://docs.microsoft.com/cli/azure/network/lb/rule#create) reguły modułu równoważenia obciążenia hello tooadd. Użyj [utworzyć sondy równoważeniem obciążenia sieciowego az](https://docs.microsoft.com/cli/azure/network/lb/probe#create) tooadd hello sondy.|
| [Szablon](../../load-balancer/load-balancer-get-started-ilb-arm-template.md) | Użyj [2 maszyny wirtualne w usłudze równoważenia obciążenia i skonfigurować reguły NAT na powitania LB](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-internal-load-balancer) wskazówki dotyczące wdrażania usługi równoważenia obciążenia przy użyciu szablonu. |

## <a name="vms"></a>Maszyny wirtualne

Maszyny wirtualne mogą zostać utworzone w hello sam sieciami wirtualnymi i ich mogą łączyć się tooeach innych adresów przy użyciu prywatnego adresu IP. Łączą nawet wtedy, gdy znajdują się w różnych podsieciach bez tooconfigure potrzeby hello bramy ani używania publicznych adresów IP. tooput maszyn wirtualnych do sieci wirtualnej, Utwórz hello sieci wirtualnej, a następnie podczas tworzenia każdej maszyny Wirtualnej, należy przypisać mu toohello sieci wirtualnej i podsieci. Ustawienia sieci maszyn wirtualnych są określane podczas wdrażania lub uruchamiania.  

Przypisywanie adresów IP odbywa się podczas wdrażania maszyn wirtualnych. Jeśli w sieci wirtualnej lub podsieci wdrożono wiele maszyn wirtualnych, uzyskują one adresy IP podczas uruchamiania. Dynamicznego adresu IP (DIP) jest hello wewnętrznego adresu IP skojarzonego z maszyny Wirtualnej. Można przypisać statycznego tooa DIP maszyny Wirtualnej. Jeśli przydzielone DIP statycznych, należy rozważyć przy użyciu tooavoid określonej podsieci, przypadkowo ponowne użycie statycznego adresu DIP do innej maszyny Wirtualnej.  

Jeśli tworzenie maszyny Wirtualnej i później chcesz toomigrate go w sieci wirtualnej, nie jest zmiana konfiguracji proste. Należy ponownie wdrożyć hello maszyny Wirtualnej do hello sieci wirtualnej. Hello Najprostszym sposobem tooredeploy jest toodelete hello maszyny Wirtualnej, ale nie wszystkie dyski podłączone tooit, a następnie ponownie utwórz hello maszynę Wirtualną przy użyciu hello oryginalnych dysków w hello sieci wirtualnej. 

Poniższa tabela zawiera hello metody, której można toocreate maszyny Wirtualnej w sieci wirtualnej.

| Metoda | Opis |
| ------ | ----------- |
| [Witryna Azure Portal](../virtual-machines-windows-hero-tutorial.md) | Ustawienia sieci domyślne hello używa, które były wcześniej wspomniano toocreate maszynę Wirtualną z jednej karty sieciowej. toocreate Maszynę wirtualną z wieloma kartami sieciowymi, należy użyć innej metody. |
| [Azure PowerShell](../virtual-machines-windows-ps-create.md) | Obejmuje użycie hello [AzureRmVMNetworkInterface Dodaj](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface) tooadd hello wcześniej utworzony toohello konfiguracji maszyny Wirtualnej karty Sieciowej. |
| [Szablon](ps-template.md) | Przewodnik [Bardzo proste wdrożenie maszyny wirtualnej z systemem Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows) ułatwia wdrożenie maszyny wirtualnej przy użyciu szablonu. |

## <a name="next-steps"></a>Następne kroki

- Dowiedz się, jak tooconfigure [trasy zdefiniowane przez użytkownika i przesyłanie dalej IP](../../virtual-network/virtual-networks-udr-overview.md). 
- Dowiedz się, jak tooconfigure [połączeń tooVNet sieci wirtualnej](../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).
- Dowiedz się, jak za[Rozwiązywanie problemów z tras](../../virtual-network/virtual-network-routes-troubleshoot-portal.md).
