> [!div class="op_single_selector"]
> * [Portal](../articles/virtual-network/virtual-network-multiple-ip-addresses-portal.md)
> * [PowerShell](../articles/virtual-network/virtual-network-multiple-ip-addresses-powershell.md)
> * [Interfejs wiersza polecenia 2.0](../articles/virtual-network/virtual-network-multiple-ip-addresses-cli.md)
> * [Interfejs wiersza polecenia 1.0](../articles/virtual-network/virtual-network-multiple-ip-addresses-cli-nodejs.md)
> * [Szablon](../articles/virtual-network/virtual-network-multiple-ip-addresses-template.md)
>

Maszyny wirtualnej Azure (VM) ma jedną lub więcej interfejsów sieciowych (NIC) dołączony tooit. Dowolnej karty interfejsu Sieciowego może mieć jeden lub więcej statyczne lub dynamiczne publiczne i prywatne IP adresów tooit przypisane. Przypisywanie IP wielu adresów tooa maszyny Wirtualnej umożliwia hello następujące możliwości:

* Hostowanie wielu witryn sieci Web lub usług z różnymi adresami IP i certyfikatami SSL na jednym serwerze.
* Może służyć jako sieciowe urządzenie wirtualne, takie jak zapora lub moduł równoważenia obciążenia.
* Witaj tooadd możliwości adresów żadnego hello prywatnego adresu IP dla każdego tooan kart sieciowych hello puli zaplecza modułu równoważenia obciążenia Azure. Witaj poza tylko hello podstawowego adresu IP hello podstawowej karty Sieciowej może być dodane tooa puli zaplecza. więcej informacji o toolearn jak tooload równoważenie wielu konfiguracji adresów IP, odczytać hello [wielu konfiguracji adresów IP równoważenia obciążenia](../articles/load-balancer/load-balancer-multiple-ip.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artykułu.

Co tooa kartę Sieciową podłączoną maszyna wirtualna ma jedną lub więcej konfiguracje adresów IP skojarzonych tooit. Każdej konfiguracji jest przypisany jeden statyczny lub dynamiczny prywatny adres IP. Każdej konfiguracji mogą zawierać jeden publiczny tooit skojarzonych zasobów adresu IP. Zasób publiczny adres IP ma albo dynamicznej lub statycznej publicznego adresu IP przypisany adres tooit. adresy toolearn więcej informacji na temat adresu IP na platformie Azure, przeczytaj hello [adresów IP na platformie Azure](../articles/virtual-network/virtual-network-ip-addresses-overview-arm.md) artykułu. 

Brak limit toohow wiele prywatnego adresu IP można przypisać adresów tooa karty sieciowej. Istnieje również limit toohow wiele publicznych adresów IP, które mogą być używane w subskrypcji platformy Azure. Zobacz hello [Azure ogranicza](../articles/azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits) artykułu, aby uzyskać szczegółowe informacje.
