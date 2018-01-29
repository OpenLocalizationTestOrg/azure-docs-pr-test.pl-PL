Utworzenie maszyny wirtualnej (VM) platformy Azure wymaga utworzenia [sieci wirtualnej](../articles/virtual-network/virtual-networks-overview.md) (VNet) lub użycia istniejącej sieci wirtualnej. Należy także określić sposób dostępu do maszyn wirtualnych w sieci wirtualnej. Ważne jest [zaplanowanie tworzenia zasobów](../articles/virtual-network/virtual-network-vnet-plan-design-arm.md) i dokładne zapoznanie się z [limitami zasobów sieciowych](../articles/azure-subscription-service-limits.md#networking-limits).

Na poniższej ilustracji przedstawiono maszyny wirtualne jako serwery sieci Web i serwery baz danych. Poszczególne zestawy maszyn wirtualnych są przypisane do oddzielnych podsieci w sieci wirtualnej.

![Sieć wirtualna Azure](./media/virtual-machines-common-network-overview/vnetoverview.png)

Można utworzyć sieci wirtualnej, przed tworzenie maszyny Wirtualnej lub można podczas tworzenia maszyny Wirtualnej. Należy utworzyć następujące zasoby, umożliwiające obsługę komunikacji z maszyną wirtualną:

- Interfejsy sieciowe
- Adresy IP
- Sieć wirtualna i podsieci

Oprócz tych podstawowych zasobów należy również rozważyć utworzenie poniższych opcjonalnych zasobów:

- Grupy zabezpieczeń sieci
- Moduły równoważenia obciążenia 

## <a name="network-interfaces"></a>Interfejsy sieciowe

[Interfejs sieciowy (karta sieciowa)](../articles/virtual-network/virtual-network-network-interface.md) to wzajemne połączenie między maszyną wirtualną (VM) i siecią wirtualną (VNet). Maszyna wirtualna musi mieć co najmniej jedną kartę sieciową. Może jednak mieć więcej kart, w zależności od rozmiaru podanego przy jej tworzeniu. Dowiedz się więcej o jak wiele kart sieciowych każdej maszyny Wirtualnej obsługuje rozmiar [Windows](../articles/virtual-machines/windows/sizes.md) lub [Linux](../articles/virtual-machines/linux/sizes.md).

Można utworzyć Maszynę wirtualną z wieloma kartami sieciowymi i Dodaj lub usuń kart sieciowych przez cały cykl życia maszyny wirtualnej. Zezwalaj na wiele kart sieciowych maszyny Wirtualnej, aby połączyć się z różnymi podsieciami i wysyłanie i odbieranie danych za pośrednictwem interfejsu najbardziej odpowiednie.

Jeśli maszyna wirtualna jest członkiem zestawu dostępności, wszystkie maszyny wirtualne w tym zestawie dostępności muszą mieć jedną kartę sieciową albo wiele kart sieciowych. W tym drugim przypadku maszyny wirtualne nie muszą mieć tyle samo kart sieciowych, ale muszą mieć co najmniej dwie karty.

Wszystkie karty sieciowe dołączone do danej maszyny wirtualnej muszą znajdować się w tej samej lokalizacji i subskrypcji co maszyna wirtualna. Wszystkie karty sieciowe muszą być podłączone do sieci wirtualnej, która znajduje się w tej samej lokalizacji i subskrypcji platformy Azure co karta sieciowa. Można zmienić podsieci maszyny Wirtualnej jest połączona z po jej utworzeniu, ale nie można zmienić sieci wirtualnej. Każda karta sieciowa dołączona do maszyny wirtualnej ma przypisany adres MAC, który pozostaje stały do momentu usunięcia maszyny wirtualnej.

Poniższa tabela zawiera listę metod, których można użyć do utworzenia interfejsu sieciowego.

| Metoda | Opis |
| ------ | ----------- |
| Portal Azure | Interfejs sieciowy jest tworzony automatycznie podczas tworzenia maszyny wirtualnej w witrynie Azure Portal (nie można użyć oddzielnie utworzonej karty sieciowej). Maszyna wirtualna utworzona w portalu może mieć tylko jedną kartę sieciową. Jeśli chcesz utworzyć maszynę wirtualną zawierającą więcej niż jedną kartę sieciową, musisz użyć innej metody. |
| [Azure PowerShell](../articles/virtual-machines/windows/multiple-nics.md) | Użyj polecenia [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) z parametrem **-PublicIpAddressId** umożliwiającym podanie identyfikatora wcześniej utworzonego publicznego adresu IP. |
| [Interfejs wiersza polecenia platformy Azure](../articles/virtual-machines/linux/multiple-nics.md) | Aby podać identyfikator wcześniej utworzonego publicznego adresu IP, użyj polecenia [az network nic create](https://docs.microsoft.com/cli/azure/network/nic#create) z parametrem **--public-ip-address**. |
| [Szablon](../articles/virtual-network/virtual-network-deploy-multinic-arm-template.md) | Przewodnik [Interfejs sieciowy w sieci wirtualnej z publicznym adresem IP](https://github.com/Azure/azure-quickstart-templates/tree/master/101-nic-publicip-dns-vnet) ułatwia wdrożenie interfejsu sieciowego przy użyciu szablonu. |

## <a name="ip-addresses"></a>Adresy IP 

Platforma Azure umożliwia przypisanie do karty sieciowej następujących typów [adresów IP](../articles/virtual-network/virtual-network-ip-addresses-overview-arm.md):

- **Publiczne adresy IP** — używane do komunikacji przychodzącej i wychodzącej (bez użycia translatora adresów sieciowych [NAT]) z Internetem i innymi zasobami platformy Azure niepołączonymi z siecią wirtualną. Przypisanie publicznego adresu IP do karty sieciowej jest opcjonalne. Publiczne adresy IP ma nominalnego opłat, i ma maksymalną liczbę, który może służyć na subskrypcję.
- **Prywatne adresy IP** — używane do komunikacji w sieci wirtualnej i lokalnej oraz z Internetem (z użyciem translatora adresów sieciowych). Do maszyny wirtualnej należy przypisać co najmniej jeden prywatny adres IP. Aby dowiedzieć się więcej o użyciu translatora adresów sieciowych na platformie Azure, zapoznaj się z tematem [Informacje o połączeniach wychodzących na platformie Azure](../articles/load-balancer/load-balancer-outbound-connections.md).

Publiczne adresy IP można przypisywać do maszyn wirtualnych lub modułów równoważenia obciążenia dostępnych z Internetu. Prywatne adresy IP można przypisywać do maszyn wirtualnych i wewnętrznych modułów równoważenia obciążenia. Przypisywanie adresów IP do maszyn wirtualnych odbywa się przy użyciu interfejsu sieciowego.

Istnieją dwie metody przydzielania adresu IP do zasobu — dynamiczna i statyczna. Domyślną metodą alokacji jest metoda dynamiczna, w której adres IP nie jest przydzielany w czasie jego tworzenia. Zamiast tego adres IP jest przydzielany podczas tworzenia maszyny wirtualnej lub uruchamiania zatrzymanej maszyny wirtualnej. Adres IP jest zwalniany, gdy zatrzymasz lub usuniesz maszynę wirtualną. 

Aby mieć pewność, że adres IP maszyny wirtualnej pozostaje taki sam, ustaw metodę alokacji jawnie jako statyczną. W takim przypadku adres IP jest przypisywany natychmiast. Jest on zwalniany tylko wtedy, gdy usuniesz maszynę wirtualną lub zmienisz jej metodę alokacji na dynamiczną.
    
Poniższa tabela zawiera listę metod, których można użyć do utworzenia adresu IP.

| Metoda | Opis |
| ------ | ----------- |
| [Azure Portal](../articles/virtual-network/virtual-network-deploy-static-pip-arm-portal.md) | Domyślnie publiczne adresy IP są dynamiczne, a skojarzone z nimi adresy mogą ulec zmianie po zatrzymaniu lub usunięciu maszyny wirtualnej. Aby mieć pewność, że maszyna wirtualna zawsze używa tego samego publicznego adresu IP, utwórz statyczny publiczny adres IP. Domyślnie podczas tworzenia maszyny wirtualnej w portalu do karty sieciowej jest przypisywany dynamiczny prywatny adres IP. Po utworzeniu maszyny Wirtualnej, można zmienić ten adres IP statyczne.|
| [Azure PowerShell](../articles/virtual-network/virtual-network-deploy-static-pip-arm-ps.md) | Użyj polecenia [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress) z parametrem **-AllocationMethod** jako dynamicznym lub statycznym. |
| [Interfejs wiersza polecenia platformy Azure](../articles/virtual-network/virtual-network-deploy-static-pip-arm-cli.md) | Użyj polecenia [az network public-ip create](https://docs.microsoft.com/cli/azure/network/public-ip#create) z parametrem **--allocation-method** jako dynamicznym lub statycznym. |
| [Szablon](../articles/virtual-network/virtual-network-deploy-static-pip-arm-template.md) | Przewodnik [Interfejs sieciowy w sieci wirtualnej z publicznym adresem IP](https://github.com/Azure/azure-quickstart-templates/tree/master/101-nic-publicip-dns-vnet) ułatwia wdrożenie publicznego adresu IP przy użyciu szablonu. |

Po utworzeniu publicznego adresu IP można skojarzyć go z maszyną wirtualną, przypisując go do karty sieciowej.

## <a name="virtual-network-and-subnets"></a>Sieć wirtualna i podsieci

Podsieć jest zakresem adresów IP w sieci wirtualnej. Sieć wirtualną można podzielić na wiele podsieci w celu jej uporządkowania i zapewnienia bezpieczeństwa. Każda karta sieciowa w maszynie wirtualnej jest połączona z jedną podsiecią w jednej sieci wirtualnej. Karty sieciowe połączone z podsieciami (tymi samymi lub różnymi) w ramach sieci wirtualnej mogą komunikować się ze sobą bez dodatkowego konfigurowania.

Konfigurowanie sieci wirtualnej obejmuje określenie topologii, w tym dostępnych przestrzeni adresowych i podsieci. Jeśli sieć wirtualna ma być połączona z innymi sieciami wirtualnymi lub lokalnymi, musisz wybrać zakresy adresów, które nie nakładają się na siebie. Adresy IP są prywatne i nie są dostępne przez Internet, lecz dotyczy to tylko adresów IP bez obsługi routingu, takich jak 10.0.0.0/8, 172.16.0.0/12 lub 192.168.0.0/16. Obecnie platforma Azure traktuje dowolny zakres adresów jako część przestrzeni prywatnych adresów IP w sieci wirtualnej. Przestrzeń ta jest dostępna w danej sieci wirtualnej oraz pozostałych, wzajemnie połączonych sieciach wirtualnych, a także z lokalizacji lokalnej. 

Jeśli w Twojej organizacji sieciami wewnętrznymi zajmuje się inna osoba, porozmawiaj z nią przed wybraniem przestrzeni adresowej. Upewnij się, że przestrzenie nie nakładają się na siebie i udostępnij informację o tym, jakiej przestrzeni zamierzasz używać, tak aby inne osoby nie korzystały z tego samego zakresu adresów IP. 

Domyślnie między podsieciami nie ma zabezpieczeń granicznych, co pozwala maszynom wirtualnym znajdującym się w poszczególnych podsieciach komunikować się ze sobą. Można jednak skonfigurować sieciowe grupy zabezpieczeń (NSG), które umożliwiają kontrolowanie ruchu przychodzącego do podsieci i maszyn wirtualnych oraz ruchu wychodzącego. 

Poniższa tabela zawiera listę metod, których można użyć do utworzenia sieci wirtualnej i podsieci. 

| Metoda | Opis |
| ------ | ----------- |
| [Azure Portal](../articles/virtual-network/virtual-networks-create-vnet-arm-pportal.md) | Jeśli wybierzesz opcję utworzenia sieci wirtualnej podczas tworzenia maszyny wirtualnej na platformie Azure, nazwa sieci wirtualnej będzie składać się z nazwy grupy zasobów zawierającej sieć wirtualną i ciągu **-vnet**. Przestrzeń adresowa to 10.0.0.0/24, wymagana nazwa podsieci to **domyślna**, a zakres adresów podsieci to 10.0.0.0/24. |
| [Azure PowerShell](../articles/virtual-network/virtual-networks-create-vnet-arm-ps.md) | Aby utworzyć podsieć i sieć wirtualną, użyj poleceń [New-AzureRmVirtualNetworkSubnetConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmVirtualNetworkSubnetConfig) i [New-AzureRmVirtualNetwork](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmVirtualNetwork). Za pomocą polecenia [AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/add-azurermvirtualnetworksubnetconfig) możesz również dodać podsieć do istniejącej sieci wirtualnej. |
| [Interfejs wiersza polecenia platformy Azure](../articles/virtual-network/virtual-networks-create-vnet-arm-cli.md) | Podsieć i sieć wirtualna są tworzone jednocześnie. Użyj polecenia [az network vnet create](https://docs.microsoft.com/cli/azure/network/vnet#create) z parametrem**--subnet-name**, podając nazwę podsieci. |
| [Szablon](../articles/virtual-network/virtual-networks-create-vnet-arm-template-click.md) | Najprostszym sposobem utworzenia sieci wirtualnej i podsieci jest pobranie istniejącego szablonu, takiego jak [Sieć wirtualna z dwiema podsieciami](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets), i dostosowanie go do własnych potrzeb. |

## <a name="network-security-groups"></a>Grupy zabezpieczeń sieci

[Sieciowa grupa zabezpieczeń](../articles/virtual-network/virtual-networks-nsg.md) zawiera listę reguł listy kontroli dostępu (ACL), które blokują lub zezwalają na ruch sieciowy do podsieci i/lub kart sieciowych. Sieciowe grupy zabezpieczeń można kojarzyć z podsieciami lub poszczególnymi kartami sieciowymi połączonymi z podsiecią. Gdy sieciowa grupa zabezpieczeń jest skojarzona z podsiecią, reguły listy ACL dotyczą wszystkich maszyn wirtualnych w tej podsieci. Ponadto ruch do poszczególnych kart sieciowych można ograniczyć przez skojarzenie sieciowej grupy zabezpieczeń bezpośrednio z kartą sieciową.

Sieciowe grupy zabezpieczeń zawierają dwa zestawy reguł: zestaw reguł przychodzących i wychodzących. Priorytety reguł muszą być unikatowe w poszczególnych zestawach. Każda reguła ma właściwości protokołu, zakresów portów źródłowych i docelowych, prefiksów adresów, kierunku ruchu, priorytetu i typu dostępu. 

Wszystkie sieciowe grupy zabezpieczeń zawierają zestaw reguł domyślnych. Reguł domyślnych nie można usunąć, ale ponieważ mają przypisany najniższy priorytet, mogą być zastąpione przez tworzone zasady. 

Po skojarzeniu sieciowej grupy zabezpieczeń z kartą sieciową reguły dostępu do sieci w sieciowej grupie zabezpieczeń są stosowane tylko do tej karty sieciowej. Jeśli na maszynie wirtualnej z wieloma kartami sieciowymi sieciowa grupa zabezpieczeń jest stosowana do jednej karty sieciowej, nie ma to wpływu na ruch powiązany z innymi kartami sieciowymi. Można skojarzyć różne sieciowe grupy zabezpieczeń z kartą sieciową (lub maszyną wirtualną, w zależności od modelu wdrażania) i podsiecią, z którą jest powiązana karta sieciowa albo maszyna wirtualna. Priorytet zależy od kierunku ruchu.

Pamiętaj, aby [zaplanować](../articles/virtual-network/virtual-networks-nsg.md#planning) sieciowe grupy zabezpieczeń podczas planowania sieci wirtualnej i maszyn wirtualnych.

Poniższa tabela zawiera listę metod, których można użyć do utworzenia sieciowej grupy zabezpieczeń.

| Metoda | Opis |
| ------ | ----------- |
| [Azure Portal](../articles/virtual-network/virtual-networks-create-nsg-arm-pportal.md) | Utworzenie maszyny wirtualnej w witrynie Azure Portal obejmuje automatyczne utworzenie sieciowej grupy zabezpieczeń i skojarzenie jej z kartą sieciową. Nazwa sieciowej grupy zabezpieczeń składa się z nazwy maszyny wirtualnej i ciągu **-nsg**. Konfiguracja tej sieciowej grupy zabezpieczeń jest następująca: jedna reguła ruchu przychodzącego z priorytetem 1000, ustawienie usługi — RDP, ustawienie protokołu — TCP, ustawienie portu — 3389 i ustawienie akcji — Zezwalaj. Jeśli chcesz zezwolić na inne rodzaje ruchu przychodzącego do maszyny wirtualnej, musisz dodać dodatkowe reguły do sieciowej grupy zabezpieczeń. |
| [Azure PowerShell](../articles/virtual-network/virtual-networks-create-nsg-arm-ps.md) | Użyj polecenia [New-AzureRmNetworkSecurityRuleConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmNetworkSecurityRuleConfig) i podaj wymagane informacje dotyczące reguły. Użyj polecenia [New-AzureRmNetworkSecurityGroup](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmNetworkSecurityGroup), aby utworzyć sieciową grupę zabezpieczeń. Użyj polecenia [Set-AzureRmVirtualNetworkSubnetConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/Set-AzureRmVirtualNetworkSubnetConfig), aby skonfigurować sieciową grupę zabezpieczeń dla podsieci. Użyj polecenia [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork), aby dodać sieciową grupę zabezpieczeń do sieci wirtualnej. |
| [Interfejs wiersza polecenia platformy Azure](../articles/virtual-network/virtual-networks-create-nsg-arm-cli.md) | Użyj polecenia [az network nsg create](https://docs.microsoft.com/cli/azure/network/nsg#create), aby utworzyć początkową sieciową grupę zabezpieczeń. Użyj polecenia [az network nsg rule create](https://docs.microsoft.com/cli/azure/network/nsg/rule#create), aby dodać reguły do sieciowej grupy zabezpieczeń. Użyj polecenia [az network vnet subnet update](https://docs.microsoft.com/cli/azure/network/vnet/subnet#update), aby dodać sieciową grupę zabezpieczeń do podsieci. |
| [Szablon](../articles/virtual-network/virtual-networks-create-nsg-arm-template.md) | Przewodnik [Tworzenie sieciowej grupy zabezpieczeń](https://github.com/Azure/azure-quickstart-templates/tree/master/101-security-group-create) ułatwia wdrożenie sieciowej grupy zabezpieczeń przy użyciu szablonu. |

## <a name="load-balancers"></a>Moduły równoważenia obciążenia

Usługa [Azure Load Balancer](../articles/load-balancer/load-balancer-overview.md) zapewnia aplikacjom wysoką dostępność i wydajność sieci. Moduł równoważenia obciążenia można skonfigurować pod kątem [równoważenia przychodzącego ruchu internetowego](../articles/load-balancer/load-balancer-internet-overview.md) do maszyn wirtualnych lub [równoważenia ruchu między maszynami wirtualnymi w sieci wirtualnej](../articles/load-balancer/load-balancer-internal-overview.md). Moduł równoważenia obciążenia umożliwia również równoważenie ruchu między komputerami lokalnymi i maszynami wirtualnymi w sieci obejmującej różne lokalizacje oraz przekazywanie ruchu zewnętrznego do określonej maszyny wirtualnej.

Moduł równoważenia obciążenia mapuje ruch przychodzący i wychodzący między publicznym adresem IP i portem modułu równoważenia obciążenia a prywatnym adresem IP i portem maszyny wirtualnej.

Podczas tworzenia modułu równoważenia obciążenia należy również wziąć pod uwagę te elementy konfiguracji:

- **Konfiguracja adresów IP frontonu** — moduł równoważenia obciążenia może zawierać jeden lub większą liczbę adresów IP frontonu, znanych także jako wirtualne adresy IP (VIP). Te adresy IP są używane podczas transferu danych przychodzących.
- **Pula adresów zaplecza** — adresy IP skojarzone z kartą sieciową, do której jest dystrybuowane obciążenie.
- **Reguły NAT** — definiują sposób kierowania ruchu przychodzącego do adresu IP frontonu i dystrybuowania tego ruchu do adresu IP zaplecza.
- **Reguły modułu równoważenia obciążenia** — mapują dany adres IP frontonu i kombinację portów na zestaw adresów IP zaplecza i kombinację portów. Moduł równoważenia obciążenia może mieć różne reguły równoważenia obciążenia. Każda reguła zawiera kombinację adresu IP frontonu i portu oraz adresu IP zaplecza i portu, które są powiązane z maszynami wirtualnymi.
- **[Sondy](../articles/load-balancer/load-balancer-custom-probe-overview.md)** — monitorują kondycję maszyn wirtualnych. Jeśli sonda nie odpowiada, moduł równoważenia obciążenia zaprzestaje inicjowania nowych połączeń z maszyną wirtualną o złej kondycji. Nie ma to wpływu na istniejące połączenia. Nowe połączenia są inicjowane z maszynami wirtualnymi o prawidłowej kondycji.

Poniższa tabela zawiera listę metod, których można użyć do utworzenia modułu równoważenia obciążenia dostępnego z Internetu.

| Metoda | Opis |
| ------ | ----------- |
| Portal Azure | Obecnie nie ma możliwości utworzenia modułu równoważenia obciążenia dostępnego z Internetu za pomocą witryny Azure Portal. |
| [Azure PowerShell](../articles/load-balancer/load-balancer-get-started-internet-arm-ps.md) | Użyj polecenia [New-AzureRmLoadBalancerFrontendIpConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerFrontendIpConfig) z parametrem **-PublicIpAddress**, aby udostępnić identyfikator wcześniej utworzonego publicznego adresu IP. Użyj polecenia [New-AzureRmLoadBalancerBackendAddressPoolConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerBackendAddressPoolConfig), aby utworzyć konfigurację puli adresów zaplecza. Użyj polecenia [New-AzureRmLoadBalancerInboundNatRuleConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerInboundNatRuleConfig), aby utworzyć reguły NAT dla ruchu przychodzącego przy użyciu utworzonej konfiguracji adresów IP frontonu. Użyj polecenia [New-AzureRmLoadBalancerProbeConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerProbeConfig), aby utworzyć wymagane sondy. Użyj polecenia [New-AzureRmLoadBalancerRuleConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerRuleConfig), aby utworzyć konfigurację modułu równoważenia obciążenia. Użyj polecenia [New-AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer), aby utworzyć moduł równoważenia obciążenia.|
| [Interfejs wiersza polecenia platformy Azure](../articles/load-balancer/load-balancer-get-started-internet-arm-cli.md) | Użyj polecenia [az network lb create](https://docs.microsoft.com/cli/azure/network/lb#create), aby utworzyć początkową konfigurację modułu równoważenia obciążenia. Użyj polecenia [az network lb frontend-ip create](https://docs.microsoft.com/cli/azure/network/lb/frontend-ip#create), aby dodać wcześniej utworzony publiczny adres IP. Użyj polecenia [az network lb address-pool create](https://docs.microsoft.com/cli/azure/network/lb/address-pool#create), aby dodać konfigurację puli adresów zaplecza. Użyj polecenia [az network lb inbound-nat-rule create](https://docs.microsoft.com/cli/azure/network/lb/inbound-nat-rule#create), aby dodać reguły NAT. Użyj polecenia [az network lb rule create](https://docs.microsoft.com/cli/azure/network/lb/rule#create), aby dodać reguły modułu równoważenia obciążenia. Użyj polecenia [az network lb probe create](https://docs.microsoft.com/cli/azure/network/lb/probe#create), aby dodać sondy. |
| [Szablon](../articles/load-balancer/load-balancer-get-started-internet-arm-template.md) | Przewodnik [Moduł równoważenia obciążenia z dwiema maszynami wirtualnymi oraz konfiguracja reguł NAT w module równoważenia obciążenia](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-loadbalancer-natrules) ułatwia wdrożenie modułu równoważenia obciążenia przy użyciu szablonu. |
    
Poniższa tabela zawiera listę metod, których można użyć do utworzenia wewnętrznego modułu równoważenia obciążenia.

| Metoda | Opis |
| ------ | ----------- |
| Portal Azure | Obecnie nie ma możliwości utworzenia wewnętrznego modułu równoważenia obciążenia za pomocą witryny Azure Portal. |
| [Azure PowerShell](../articles/load-balancer/load-balancer-get-started-ilb-arm-ps.md) | Użyj polecenia [New-AzureRmLoadBalancerFrontendIpConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerFrontendIpConfig) z parametrem **-PrivateIpAddress**, aby podać prywatny adres IP w podsieci. Użyj polecenia [New-AzureRmLoadBalancerBackendAddressPoolConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerBackendAddressPoolConfig), aby utworzyć konfigurację puli adresów zaplecza. Użyj polecenia [New-AzureRmLoadBalancerInboundNatRuleConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerInboundNatRuleConfig), aby utworzyć reguły NAT dla ruchu przychodzącego przy użyciu utworzonej konfiguracji adresów IP frontonu. Użyj polecenia [New-AzureRmLoadBalancerProbeConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerProbeConfig), aby utworzyć wymagane sondy. Użyj polecenia [New-AzureRmLoadBalancerRuleConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerRuleConfig), aby utworzyć konfigurację modułu równoważenia obciążenia. Użyj polecenia [New-AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer), aby utworzyć moduł równoważenia obciążenia.|
| [Interfejs wiersza polecenia platformy Azure](../articles/load-balancer/load-balancer-get-started-ilb-arm-cli.md) | Użyj polecenia [az network lb create](https://docs.microsoft.com/cli/azure/network/lb#create), aby utworzyć początkową konfigurację modułu równoważenia obciążenia. Użyj polecenia [az network lb frontend-ip create](https://docs.microsoft.com/cli/azure/network/lb/frontend-ip#create) z parametrem **--private-ip-address**, aby zdefiniować prywatny adres IP. Użyj polecenia [az network lb address-pool create](https://docs.microsoft.com/cli/azure/network/lb/address-pool#create), aby dodać konfigurację puli adresów zaplecza. Użyj polecenia [az network lb inbound-nat-rule create](https://docs.microsoft.com/cli/azure/network/lb/inbound-nat-rule#create), aby dodać reguły NAT. Użyj polecenia [az network lb rule create](https://docs.microsoft.com/cli/azure/network/lb/rule#create), aby dodać reguły modułu równoważenia obciążenia. Użyj polecenia [az network lb probe create](https://docs.microsoft.com/cli/azure/network/lb/probe#create), aby dodać sondy.|
| [Szablon](../articles/load-balancer/load-balancer-get-started-ilb-arm-template.md) | Przewodnik [Moduł równoważenia obciążenia z dwiema maszynami wirtualnymi oraz konfiguracja reguł NAT w module równoważenia obciążenia](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-internal-load-balancer) ułatwia wdrożenie modułu równoważenia obciążenia przy użyciu szablonu. |

## <a name="vms"></a>Maszyny wirtualne

Maszyny wirtualne można tworzyć w tej samej sieci wirtualnej i mogą one komunikować się ze sobą przy użyciu prywatnych adresów IP. Komunikacja między maszynami jest możliwa, nawet jeśli znajdują się one w różnych podsieciach — nie ma potrzeby konfigurowania bramy ani używania publicznych adresów IP. Aby połączyć maszyny wirtualne z siecią wirtualną, podczas tworzenia poszczególnych maszyn wirtualnych należy przypisać je do utworzonej sieci wirtualnej i podsieci. Ustawienia sieci maszyn wirtualnych są określane podczas wdrażania lub uruchamiania.  

Przypisywanie adresów IP odbywa się podczas wdrażania maszyn wirtualnych. Jeśli w sieci wirtualnej lub podsieci wdrożono wiele maszyn wirtualnych, uzyskują one adresy IP podczas uruchamiania. Dynamiczny adres IP (DIP) jest wewnętrznym adresem IP skojarzonym z maszyną wirtualną. Do maszyny wirtualnej można przydzielić statyczny adres DIP. W przypadku przydzielenia statycznego adresu DIP rozważ użycie określonej podsieci, aby uniknąć przypadkowego ponownego użycia statycznego adresu DIP dla innej maszyny wirtualnej.  

Migracja utworzonej maszyny wirtualnej do sieci wirtualnej nie obejmuje jedynie wprowadzenia prostej zmiany w konfiguracji. Maszynę wirtualną należy ponownie wdrożyć w sieci wirtualnej. Najprostszym sposobem ponownego wdrożenia jest usunięcie maszyny wirtualnej (ale bez usuwania jakichkolwiek dysków podłączonych do niej), a następnie ponowne utworzenie maszyny wirtualnej w sieci wirtualnej przy użyciu oryginalnych dysków. 

Poniższa tabela zawiera listę metod, których można użyć do utworzenia maszyny wirtualnej w sieci wirtualnej.

| Metoda | Opis |
| ------ | ----------- |
| [Azure Portal](../articles/virtual-machines/windows/quick-create-portal.md) | Używane są domyślne ustawienia sieci, takie jak podczas tworzenia maszyny wirtualnej z jedną kartą sieciową. Aby utworzyć maszynę wirtualną z wieloma kartami sieciowymi, należy użyć innej metody. |
| [Azure PowerShell](../articles/virtual-machines/windows/tutorial-manage-vm.md) | Obejmuje użycie polecenia [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface) w celu dodania wcześniej utworzonej karty sieciowej do konfiguracji maszyny wirtualnej. |
| [Interfejs wiersza polecenia platformy Azure](../articles/virtual-machines/linux/create-cli-complete.md) | Tworzenie i łączenie maszyny Wirtualnej do sieci wirtualnej, podsieci i karty interfejsu Sieciowego z kompilacji jako poszczególne kroki. |
| [Szablon](../articles/virtual-machines/windows/ps-template.md) | Przewodnik [Bardzo proste wdrożenie maszyny wirtualnej z systemem Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows) ułatwia wdrożenie maszyny wirtualnej przy użyciu szablonu. |

## <a name="next-steps"></a>Następne kroki
Aby specyficzne dla maszyny Wirtualnej instrukcje na temat zarządzania sieci wirtualnych platformy Azure dla maszyn wirtualnych, zobacz [Windows](../articles/virtual-machines/windows/tutorial-virtual-network.md) lub [Linux](../articles/virtual-machines/linux/tutorial-virtual-network.md) samouczki.

Dostępne są także samouczki dotyczące maszyn wirtualnych równoważenia obciążenia i utworzyć aplikacje o wysokiej dostępności dla [Windows](../articles/virtual-machines/windows/tutorial-load-balancer.md) lub [Linux](../articles/virtual-machines/linux/tutorial-load-balancer.md).

- Dowiedz się, jak skonfigurować [trasy zdefiniowane przez użytkownika i przekazywanie adresów IP](../articles/virtual-network/virtual-networks-udr-overview.md). 
- Dowiedz się, jak skonfigurować [połączenia między sieciami wirtualnymi](../articles/vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).
- Dowiedz się, jak [rozwiązywać problemy z trasami](../articles/virtual-network/virtual-network-routes-troubleshoot-portal.md).