---
title: "Typy adresów IP na platformie Azure | Microsoft Docs"
description: "Dowiedz się więcej na temat publicznych i prywatnych adresów IP na platformie Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: jeconnoc
editor: 
tags: azure-resource-manager
ms.assetid: 610b911c-f358-4cfe-ad82-8b61b87c3b7e
ms.service: virtual-network
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/18/2017
ms.author: jdial
ms.openlocfilehash: 8ddd582ed159e10add896252c40feb19780c42fb
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/11/2017
---
# <a name="ip-address-types-and-allocation-methods-in-azure"></a>Typy adresów IP i metody alokacji na platformie Azure

Do zasobów platformy Azure można przypisać adresy IP w celu komunikowania się z innymi zasobami platformy Azure, siecią lokalną i Internetem. Istnieją dwa typy adresów IP, których można użyć na platformie Azure:

* **Publiczne adresy IP**: używane do komunikacji z Internetem łącznie z publicznymi usługami platformy Azure.
* **Prywatne adresy IP**: używane do komunikacji w ramach sieci wirtualnej platformy Azure i Twojej lokalnej sieci, gdy używasz bramy sieci VPN lub obwodu ExpressRoute w celu rozszerzenia swojej sieci na platformę Azure.

> [!NOTE]
> Platforma Azure oferuje dwa różne modele wdrażania związane z tworzeniem zasobów i pracą z nimi: [model wdrażania przy użyciu usługi Azure Resource Manager i model klasyczny](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).  Ten artykuł dotyczy używania modelu wdrażania usługi Resource Manager zalecanego przez firmę Microsoft w przypadku większości nowych wdrożeń zamiast [klasycznego modelu wdrażania](virtual-network-ip-addresses-overview-classic.md).
> 

Jeśli znasz klasyczny model wdrażania, sprawdź [różnice w adresowaniu IP między wersją klasyczną i usługą Resource Manager](virtual-network-ip-addresses-overview-classic.md#differences-between-resource-manager-and-classic-deployments).

## <a name="public-ip-addresses"></a>Publiczne adresy IP

Publiczne adresy IP umożliwiają zasobom platformy Azure komunikację z Internetem i publicznymi usługami Azure, takimi jak [Azure Redis Cache](https://azure.microsoft.com/services/cache), [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs) [SQL Database](../sql-database/sql-database-technical-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json) i [Azure Storage](../storage/common/storage-introduction.md?toc=%2fazure%2fvirtual-network%2ftoc.json).

W usłudze Azure Resource Manager [publiczny adres IP](virtual-network-public-ip-address.md) jest zasobem, który ma własne właściwości. Niektóre zasoby, z którymi możesz powiązać zasób publicznego adresu IP, to:

* Interfejsy sieciowe maszyny wirtualnej
* Moduły równoważenia obciążenia dostępne z Internetu
* Bramy sieci VPN
* Bramy aplikacji

### <a name="ip-address-version"></a>Wersja adresu IP

Publiczne adresy IP są tworzone przy użyciu adresu IPv4 lub IPv6. Publiczne adresy IPv6 można przypisywać tylko do modułów równoważenia obciążenia dostępnych z Internetu.

### <a name="sku"></a>SKU

Publiczne adresy IP są tworzone przy użyciu jednej z następujących jednostek SKU:

#### <a name="basic"></a>Podstawowa

Wszystkie publiczne adresy IP utworzone przed wprowadzeniem jednostek SKU są publicznymi adresami IP opartymi na podstawowej jednostce SKU. Od momentu wprowadzenia jednostki SKU masz opcję określania, którą jednostką SKU ma być publiczny adres IP. Podstawowe adresy SKU:

- Są przypisywane przy użyciu metody alokacji statycznej lub dynamicznej.
- Są przypisywane do zasobów platformy Azure, do których można przypisać publiczny adres IP, takich jak interfejsy sieciowe, bramy VPN Gateway, bramy Application Gateway i moduły równoważenia obciążenia dostępne z Internetu.
- Mogą być przypisywane do określonej strefy.
- Nie są strefowo nadmiarowe. Aby dowiedzieć się więcej o strefach dostępności, zobacz [Availability zones overview (Omówienie stref dostępności)](../availability-zones/az-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json).

#### <a name="standard"></a>Standardowa

Standardowe publiczne adresy IP jednostek SKU:

- Są przypisywane tylko przy użyciu metody alokacji statycznej.
- Są przypisywane do interfejsów sieciowych lub standardowych modułów równoważenia obciążenia dostępnych z Internetu. Aby uzyskać więcej informacji na temat jednostek SKU usługi Azure Load Balancer, zobacz [Azure load balancer standard SKU (Usługa Azure Load Balancer — standardowa jednostka SKU)](../load-balancer/load-balancer-standard-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json).
- Są domyślnie strefowo nadmiarowe. Mogą być tworzone strefowo i być gwarantowane w określonej strefie dostępności.  Aby dowiedzieć się więcej o strefach dostępności, zobacz [Availability zones overview (Omówienie stref dostępności)](../availability-zones/az-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json).
 
> [!NOTE]
> Po przypisaniu standardowego publicznego adresu IP jednostki SKU do interfejsu sieciowego maszyny wirtualnej musisz jawnie zezwolić na ruch do miejsca przeznaczenia przy użyciu [sieciowej grupy zabezpieczeń](security-overview.md#network-security-groups).  Próba komunikacji z zasobem będzie kończyć się niepowodzeniem do momentu utworzenia i skojarzenia sieciowej grupy zabezpieczeń, a następnie jawnego zezwolenia na żądany ruch.

Standardowa jednostka SKU jest dostępna w wersji zapoznawczej. Przed utworzeniem standardowego publicznego adresu IP jednostki SKU musisz zarejestrować się do korzystania z wersji zapoznawczej i utworzyć adres w obsługiwanej lokalizacji. Aby zarejestrować się do korzystania z wersji zapoznawczej, zobacz część [Register for the standard SKU preview (Rejestrowanie się do korzystania ze standardowej jednostki SKU w wersji zapoznawczej)](virtual-network-public-ip-address.md#register-for-the-standard-sku-preview). Aby dowiedzieć się więcej na temat obsługi dodatkowych regionów, zapoznaj się z listą obsługiwanych lokalizacji (regionów) w sekcji [Region availability (Dostępność w regionach)](../load-balancer/load-balancer-standard-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#region-availability) i monitoruj stronę [aktualizacji usługi Azure Virtual Network](https://azure.microsoft.com/updates/?product=virtual-network).


### <a name="allocation-method"></a>Metoda alokacji

Istnieją dwie metody, w których adres IP jest przydzielany do publicznego zasobu adresu IP — *dynamiczna* i *statyczna*. Domyślną metodą alokacji jest metoda *dynamiczna*, w której adres IP **nie** jest przydzielany w czasie jego tworzenia. Zamiast tego publiczny adres IP jest przydzielany, gdy uruchamiasz (lub tworzysz) skojarzony zasób (np. maszynę wirtualną lub moduł równoważenia obciążenia). Adres IP jest zwalniany, gdy zatrzymasz (lub usuniesz) zasób. Na przykład po zwolnieniu z zasobu A adres IP można przypisać do innego zasobu. Jeśli adres IP zostanie przypisany do innego zasobu po zatrzymaniu zasobu A, po ponownym uruchomieniu zasobu A zostanie przypisany inny adres IP.

Aby zapewnić, żeby adres IP skojarzonego zasobu pozostawał taki sam, należy ustawić metodę alokacji jawnie jako *statyczną*. Statyczny adres IP jest przypisywany natychmiast. Adres jest zwalniany tylko wtedy, gdy usuniesz zasób lub zmienisz jego metodę alokacji na *dynamiczną*.

> [!NOTE]
> Nawet gdy ustawisz metodę alokacji jako *statyczną*, nie możesz określić rzeczywistego adresu IP przypisanego do publicznego zasobu adresu IP. Platforma Azure przypisuje adres IP z puli adresów IP dostępnych w lokalizacji platformy Azure, w której zasób jest tworzony.
>

Statyczne publiczne adresy IP są powszechnie używane w następujących scenariuszach:

* Gdy musisz aktualizować reguły zapory, aby komunikować się z zasobami platformy Azure.
* Rozpoznawanie nazw DNS, gdzie zmiana adresu IP wymaga aktualizacji rekordów A.
* Zasoby platformy Azure komunikują się z innymi aplikacjami lub usługami, które korzystają z modelu zabezpieczeń opartych na adres IP.
* Używasz certyfikatów SSL połączonych z adresem IP.

> [!NOTE]
> Platforma Azure przydziela publiczne adresy IP z zakresu unikatowego dla każdego regionu platformy Azure. Aby uzyskać szczegółowe informacje, zobacz [Azure Datacenter IP ranges (Zakresy adresów IP centrum danych platformy Azure)](https://www.microsoft.com/download/details.aspx?id=41653).
>

### <a name="dns-hostname-resolution"></a>Rozpoznawanie nazw hostów DNS
Możesz określić etykietę nazwy domeny DNS dla publicznego zasobu adresu IP, który tworzy mapowanie witryny *domainnamelabel*.*location*.cloudapp.azure.com na publiczny adres IP na serwerach DNS zarządzanych przez platformę Azure. Jeśli na przykład utworzysz publiczny zasób adresu IP mający **contoso** jako wartość parametru *domainnamelabel* w *lokalizacji* platformy Azure w **Zachodnich stanach USA**, w pełni kwalifikowana nazwa domeny (FQDN) **contoso.westus.cloudapp.azure.com** zostanie rozpoznana jako publiczny adres IP zasobu. Nazwy FQDN możesz użyć do utworzenia rekordu CNAME domeny niestandardowej wskazującego na publiczny adres IP na platformie Azure.

> [!IMPORTANT]
> Każda utworzona etykieta nazwy domeny musi być unikatowa w swojej lokalizacji na platformie Azure.  
>

### <a name="virtual-machines"></a>Maszyny wirtualne

Możesz skojarzyć publiczny adres IP z maszyną wirtualną systemu [Windows](../virtual-machines/windows/overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json) lub [Linux](../virtual-machines/linux/overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json), przypisując go do **interfejsu sieciowego**. Do maszyny wirtualnej możesz przypisać dynamiczny lub statyczny publiczny adres IP. Dowiedz się więcej o [przypisywaniu adresów IP do interfejsów sieciowych](virtual-network-network-interface-addresses.md).

### <a name="internet-facing-load-balancers"></a>Moduły równoważenia obciążenia dostępne z Internetu

Publiczny adres IP utworzony przy użyciu dowolnej jednostki [SKU](#SKU) możesz skojarzyć z usługą [Azure Load Balancer](../load-balancer/load-balancer-overview.md), przypisując go do konfiguracji **frontonu** modułu równoważenia obciążenia. Publiczny adres IP służy jako wirtualny adres IP (VIP) o zrównoważonym obciążeniu. Do frontonu modułu równoważenia obciążenia możesz przypisać dynamiczny lub statyczny publiczny adres IP. Do frontonu modułu równoważenia obciążenia możesz także przypisać wiele publicznych adresów IP, co umożliwiają scenariusze [wielu wirtualnych adresów IP](../load-balancer/load-balancer-multivip.md?toc=%2fazure%2fvirtual-network%2ftoc.json), takie jak środowisko wielodostępne z witrynami internetowymi opartymi na protokole SSL. Aby uzyskać więcej informacji na temat jednostek SKU usługi Azure Load Balancer, zobacz [Azure load balancer standard SKU (Usługa Azure Load Balancer — standardowa jednostka SKU)](../load-balancer/load-balancer-standard-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json).

### <a name="vpn-gateways"></a>Bramy sieci VPN

Usługa [Azure VPN Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-network%2ftoc.json) służy do łączenia sieci wirtualnej platformy Azure z innymi sieciami wirtualnymi platformy Azure lub siecią lokalną. Publiczny adres IP jest przypisywany do bramy VPN Gateway w celu umożliwienia komunikacji z siecią zdalną. Do bramy sieci VPN możesz przypisać tylko *dynamiczny* publiczny adres IP.

### <a name="application-gateways"></a>Bramy aplikacji

Publiczny adres IP możesz skojarzyć z usługą [Application Gateway](../application-gateway/application-gateway-introduction.md?toc=%2fazure%2fvirtual-network%2ftoc.json) platformy Azure, przypisując go do konfiguracji **frontonu** bramy. Ten publiczny adres IP służy jako adres VIP o zrównoważonym obciążeniu. Do konfiguracji frontonu bramy aplikacji możesz przypisać tylko *dynamiczny* publiczny adres IP.

### <a name="at-a-glance"></a>W skrócie
W poniższej tabeli przedstawiono określone właściwości, za pomocą których publiczny adres IP można skojarzyć z zasobem najwyższego poziomu, oraz ewentualne metody alokacji (dynamicznej lub statycznej), których można użyć.

| Zasób najwyższego poziomu | Skojarzenie adresu IP | Dynamiczny | Statyczny |
| --- | --- | --- | --- |
| Maszyna wirtualna |Interfejs sieciowy |Tak |Tak |
| Moduł równoważenia obciążenia dostępny z Internetu |Konfiguracja frontonu |Tak |Tak |
| Brama sieci VPN |Konfiguracja adresu IP bramy |Tak |Nie |
| Brama aplikacji |Konfiguracja frontonu |Tak |Nie |

## <a name="private-ip-addresses"></a>Prywatne adresy IP
Prywatne adresy IP umożliwiają zasobom platformy Azure komunikację z innymi zasobami w [sieci wirtualnej](virtual-networks-overview.md) lub sieci lokalnej za pomocą bramy sieci VPN lub obwodu ExpressRoute bez użycia adresu IP dostępnego w Internecie.

W modelu wdrażania przy użyciu usługi Azure Resource Manager prywatny adres IP jest skojarzony z następującymi typami zasobów platformy Azure:

* Interfejsy sieciowe maszyny wirtualnej
* Wewnętrzne moduły równoważenia obciążenia (ILB)
* Bramy aplikacji

### <a name="ip-address-version"></a>Wersja adresu IP

Prywatne adresy IP są tworzone przy użyciu adresy IPv4 lub IPv6. Prywatne adresy IPv6 można przypisywać tylko przy użyciu dynamicznej metody alokacji. Nie można komunikować się między prywatnymi adresami IPv6 w sieci wirtualnej. Możesz komunikować się w ramach ruchu przychodzącego z prywatnym adresem IPv6 z Internetu przy użyciu modułu równoważenia obciążenia dostępnego z Internetu. Szczegółowe informacje można znaleźć w temacie [Tworzenie modułu równoważenia obciążenia połączonego z Internetem przy użyciu protokołu IPv6](../load-balancer/load-balancer-ipv6-internet-ps.md?toc=%2fazure%2fvirtual-network%2ftoc.json).

### <a name="allocation-method"></a>Metoda alokacji

Prywatny adres IP jest przydzielany z zakresu adresów w podsieci, do której zasób jest dołączony. Zakres adresów samej podsieci jest częścią zakresu adresów sieci wirtualnej.

Istnieją dwie metody przydzielania prywatnego adresu IP: *dynamiczna* i *statyczna*. Domyślną metodą alokacji jest metoda *dynamiczna*, gdzie adres IP jest przydzielany automatycznie z podsieci zasobu (przy użyciu protokołu DHCP). Ten adres IP może się zmieniać, gdy zatrzymujesz i uruchamiasz zasób.

Możesz ustawić metodę alokacji jako *statyczną*, aby zapewnić, że adres IP pozostaje bez zmian. W przypadku wybrania metody *statycznej* musisz również podać prawidłowy adres IP, który jest częścią podsieci zasobu.

Statyczne prywatne adresy IP są powszechnie używane do:

* Maszyn wirtualnych, które działają jako kontrolery domeny lub serwery DNS.
* Zasobów, które wymagają reguł zapory korzystających z adresów IP.
* Zasoby dostępne dla innych aplikacji/zasobów za pomocą adresu IP.

### <a name="virtual-machines"></a>Maszyny wirtualne

Prywatny adres IP jest przypisywany do **interfejsu sieciowego** maszyny wirtualnej z systemem [Windows](../virtual-machines/windows/overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json) lub [Linux](../virtual-machines/linux/overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json). Jeśli maszyna wirtualna ma wiele interfejsów sieciowych, prywatny adres IP jest przypisywany do każdego interfejsu sieciowego. Metodę alokacji dla interfejsu sieciowego możesz określić jako dynamiczną lub statyczną.

#### <a name="internal-dns-hostname-resolution-for-virtual-machines"></a>Wewnętrzne rozpoznawanie nazwy hosta DNS (dla maszyn wirtualnych)

Wszystkie maszyny wirtualne platformy Azure są domyślnie skonfigurowane z [serwerami DNS zarządzanymi przez platformę Azure](virtual-networks-name-resolution-for-vms-and-role-instances.md#azure-provided-name-resolution), chyba że jawnie skonfigurujesz niestandardowe serwery DNS. Te serwery DNS zapewniają rozpoznawanie nazw wewnętrznych maszyn wirtualnych znajdujących się w tej samej sieci wirtualnej.

Podczas tworzenia maszyny wirtualnej mapowanie nazwy hosta na jego prywatny adres IP jest dodawane do serwerów DNS zarządzanych przez platformę Azure. W przypadku maszyny wirtualnej z wieloma interfejsami sieciowymi nazwa hosta jest mapowana na prywatny adres IP głównego interfejsu sieciowego.

Maszyny wirtualne skonfigurowane przy użyciu serwerów DNS zarządzanych przez platformę Azure będą mogły rozpoznać nazwy hostów wszystkich maszyn wirtualnych w ramach ich sieci wirtualnej według ich prywatnych adresów IP.

### <a name="internal-load-balancers-ilb--application-gateways"></a>Wewnętrzne moduły równoważenia obciążenia (ILB) i bramy aplikacji

Prywatny adres IP możesz przypisać do konfiguracji **frontonu** [wewnętrznego modułu równoważenia obciążenia platformy Azure](../load-balancer/load-balancer-internal-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (ILB) lub [bramy aplikacji platformy Azure](../application-gateway/application-gateway-introduction.md?toc=%2fazure%2fvirtual-network%2ftoc.json). Ten prywatny adres IP służy jako wewnętrzny punkt końcowy dostępny tylko dla zasobów w ramach jego sieci wirtualnej i sieci zdalnych podłączonych do sieci wirtualnej. Do konfiguracji frontonu możesz przypisać dynamiczny albo statyczny prywatny adres IP.

### <a name="at-a-glance"></a>W skrócie
W poniższej tabeli przedstawiono określone właściwości, za pomocą których prywatny adres IP można skojarzyć z zasobem najwyższego poziomu, oraz ewentualne metody alokacji (dynamicznej lub statycznej), których można użyć.

| Zasób najwyższego poziomu | Skojarzenie adresu IP | Dynamiczny | Statyczny |
| --- | --- | --- | --- |
| Maszyna wirtualna |Interfejs sieciowy |Tak |Tak |
| Moduł równoważenia obciążenia |Konfiguracja frontonu |Tak |Tak |
| Brama aplikacji |Konfiguracja frontonu |Tak |Tak |

## <a name="limits"></a>Limity
Ograniczenia nakładane na adresowanie IP zostały wymienione w pełnym zestawieniu [ograniczeń dla sieci](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#networking-limits) na platformie Azure. Ograniczenia są podzielone według regionu i subskrypcji. [Kontaktując się z pomocą techniczną](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade), możesz zwiększyć domyślne limity do maksimum w zależności od potrzeb biznesowych.

## <a name="pricing"></a>Cennik
Publiczne adresy IP mogą być związane z nominalnymi opłatami. Aby dowiedzieć się więcej o cenach adresów IP na platformie Azure, przejrzyj stronę [Cennik adresów IP](https://azure.microsoft.com/pricing/details/ip-addresses).

## <a name="next-steps"></a>Następne kroki
* [Wdrażanie maszyny wirtualnej ze statycznym publicznym adresem IP przy użyciu witryny Azure Portal](virtual-network-deploy-static-pip-arm-portal.md)
* [Wdrażanie maszyny wirtualnej ze statycznym publicznym adresem IP przy użyciu szablonu](virtual-network-deploy-static-pip-arm-template.md)
* [Wdrażanie maszyny wirtualnej ze statycznym prywatnym adresem IP przy użyciu witryny Azure Portal](virtual-networks-static-private-ip-arm-pportal.md)
