---
title: "typy adresów aaaIP na platformie Azure (klasyczne) | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat publiczne i prywatne adresy IP (klasyczne) na platformie Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
tags: azure-service-management
ms.assetid: 2f8664ab-2daf-43fa-bbeb-be9773efc978
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/11/2016
ms.author: jdial
ms.openlocfilehash: 7e09a5ad5b5f2d55329152b5d843de3c4455d1b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="ip-address-types-and-allocation-methods-classic-in-azure"></a>Typy adresów IP i metod alokacji (klasyczne) na platformie Azure
Można przypisać IP adresów tooAzure zasobów toocommunicate z innych zasobów platformy Azure, sieci lokalnej i hello Internet. Istnieją dwa typy adresów IP można używać w Azure: prywatnych i publicznych.

Publiczne adresy IP są używane do komunikacji z hello internetowych, takich jak Azure usługi publicznych.

Prywatne adresy IP są używane do komunikacji w ramach sieci wirtualnej platformy Azure (VNet), usługa w chmurze i sieci lokalnej, podczas korzystania z bramy sieci VPN lub tooextend obwodu ExpressRoute tooAzure Twojej sieci.

> [!IMPORTANT]
> Platforma Azure oferuje dwa różne modele wdrażania związane z tworzeniem zasobów i pracą z nimi: [model wdrażania przy użyciu usługi Azure Resource Manager i model klasyczny](../resource-manager-deployment-model.md).  W tym artykule omówiono przy użyciu hello klasycznego modelu wdrażania. Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać Menedżera zasobów. Więcej informacji na temat adresów IP w Menedżerze zasobów przez odczytywania hello [adresów IP](virtual-network-ip-addresses-overview-arm.md) artykułu.

## <a name="public-ip-addresses"></a>Publiczne adresy IP
Publiczne adresy IP umożliwiają toocommunicate zasobów platformy Azure z publicznymi usługami Internet i Azure [pamięć podręczna Redis Azure](https://azure.microsoft.com/services/cache/), [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/), [baz danych](../sql-database/sql-database-technical-overview.md), i [magazynu Azure](../storage/common/storage-introduction.md).

Publiczny adres IP jest skojarzony z hello następujące typy zasobów:

* Usługi w chmurze
* Maszyny wirtualne IaaS (VM)
* Wystąpienia roli PaaS
* Bramy sieci VPN
* Bramy aplikacji

### <a name="allocation-method"></a>Metoda alokacji
Gdy publiczny adres IP musi toobe przypisane tooan zasobów platformy Azure, jest *dynamicznie* przydzielone z puli dostępny publiczny adres IP jest tworzony adresów w obrębie hello lokalizacji hello zasobów. Ten adres IP jest zwalniany po zatrzymaniu hello zasobów. W przypadku usługi w chmurze tak się stanie, gdy zostały zatrzymane wszystkie wystąpienia roli hello, które można uniknąć za pomocą *statycznych* (zastrzeżony) adres IP (zobacz [usługi w chmurze](#Cloud-services)).

> [!NOTE]
> Lista Hello zakresy adresów IP, z których publiczne adresy IP są przydzielane zasoby tooAzure jest opublikowana w [zakresy IP centrum danych Azure](https://www.microsoft.com/download/details.aspx?id=41653).
> 
> 

### <a name="dns-hostname-resolution"></a>Rozpoznawanie nazw hostów DNS
Podczas tworzenia usługi w chmurze lub maszyn wirtualnych IaaS, należy tooprovide nazwę DNS usługi chmury, która jest unikatowa dla wszystkich zasobów na platformie Azure. Spowoduje to utworzenie mapowanie w hello serwery zarządzane Azure DNS dla *dnsname*. cloudapp.net toohello publicznego adresu IP hello zasobów. Na przykład po utworzeniu usługi w chmurze przy użyciu nazwy DNS usługi chmury z **contoso**, hello pełni kwalifikowaną nazwą domeny (FQDN) **contoso.cloudapp.net** rozwiąże tooa publicznego adresu IP (VIP) usługi w chmurze Hello. Można użyć tej nazwy FQDN toocreate domeny niestandardowej rekord CNAME, wskazując toohello publicznego adresu IP na platformie Azure.

### <a name="cloud-services"></a>Usługi w chmurze
Usługi w chmurze ma zawsze publicznego adresu IP, adresów tooas określonego wirtualnego adresu IP (VIP). Punkty końcowe można tworzyć w chmurze usługi tooassociate różnych portów w hello VIP toointernal porty na maszynach wirtualnych i wystąpień roli w ramach usługi w chmurze hello. 

Usługi w chmurze może zawierać wiele maszyn wirtualnych IaaS lub wystąpień roli PaaS, wszystkie dostępnego za pośrednictwem hello tego samego adresu VIP usługi chmury. Można także przypisać [usługi w chmurze tooa wielu adresów VIP](../load-balancer/load-balancer-multivip.md), który umożliwia obsługę scenariuszy wielu wirtualnych adresów IP, takich jak środowiska z wieloma dzierżawami z witrynami sieci Web oparta na protokole SSL.

Można zapewnić hello publicznego adresu IP usługi w chmurze pozostaje hello są takie same, nawet wtedy, gdy wszystkie hello wystąpień roli zatrzymana, za pomocą *statycznych* publicznego adresu IP, określony tooas [zastrzeżonego adresu IP](virtual-networks-reserved-public-ip.md). Można utworzyć zasób statycznego adresu IP (zastrzeżony) w określonej lokalizacji i przypisz do niego tooany usługi w chmurze w tej lokalizacji. Nie można określić hello rzeczywisty adres IP dla adresu IP hello zastrzeżone, jest ona przydzielone z puli adresy IP dostępne w lokalizacji hello, w której jest tworzona. Ten adres IP nie zostaje zwolniony, dopóki nie zostaną jawnie usunięte.

Statyczny (zastrzeżony) publiczne adresy IP są często używane w scenariuszach hello, w przypadku, gdy usługa w chmurze:

* wymaga ustawienia toobe reguł zapory przez użytkowników końcowych.
* zależy od zewnętrznego rozpoznawania nazw DNS i aktualizowania rekordów wymagają dynamicznego adresu IP.
* korzysta z usługi zewnętrzne sieci web, które używają adresu IP na podstawie modelu zabezpieczeń.
* używa adresu IP połączonego tooan certyfikaty SSL.

> [!NOTE]
> Podczas tworzenia klasycznych maszyn wirtualnych, kontener *usługi w chmurze* jest tworzony przez platformę Azure, który ma wirtualnego adresu IP (VIP). Podczas tworzenia hello odbywa się za pośrednictwem portalu, domyślne połączenie RDP lub SSH *punktu końcowego* skonfigurowano przez hello portal toohello maszyny Wirtualnej do połączenia się przy użyciu adresu VIP usługi chmury hello. Tej usługi chmury wirtualne adresy IP może być zarezerwowana, co umożliwia efektywne zastrzeżonego adresu IP address tooconnect toohello maszyny Wirtualnej. Należy otworzyć porty dodatkowe, konfigurując więcej punktów końcowych.
> 
> 

### <a name="iaas-vms-and-paas-role-instances"></a>Maszyny wirtualne IaaS i wystąpienia roli PaaS
Można przypisać publiczny adres IP bezpośrednio tooan IaaS [wirtualna](../virtual-machines/virtual-machines-linux-about.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) lub wystąpienia roli PaaS w ramach usługi w chmurze. Jest to tooas określonym poziomie wystąpienia publicznego adresu IP ([ILPIP](virtual-networks-instance-level-public-ip.md)). Ten publiczny adres IP może być dynamiczny tylko.

> [!NOTE]
> Różni się to od hello VIP hello usługi w chmurze jest kontenerem dla maszyn wirtualnych IaaS i PaaS wystąpienia roli, ponieważ usługa w chmurze może zawierać wiele maszyn wirtualnych IaaS lub wystąpień roli PaaS, wszystkie dostępnego za pośrednictwem hello sam chmury VIP usługi.
> 
> 

### <a name="vpn-gateways"></a>Bramy sieci VPN
A [bramy sieci VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md) mogą być używane tooconnect tooother sieci wirtualnej Azure sieci sieci wirtualnych platformy Azure lub lokalnie. Brama VPN przypisano publiczny adres IP *dynamicznie*, które umożliwia komunikację z siecią zdalnego hello.

### <a name="application-gateways"></a>Bramy aplikacji
Azure [brama aplikacji w](../application-gateway/application-gateway-introduction.md) może służyć do Layer7 równoważenia obciążenia tooroute ruchu sieciowego oparte na HTTP. Brama aplikacji w przypisano publiczny adres IP *dynamicznie*, która służy jako hello VIP usługi równoważenia obciążenia.

### <a name="at-a-glance"></a>W skrócie
Witaj w poniższej tabeli przedstawiono każdego typu zasobu z metod alokacji możliwe hello (dynamiczny/statyczny) i możliwości tooassign wiele publicznych adresów IP.

| Zasób | Dynamiczny | Statyczny | Wiele adresów IP |
| --- | --- | --- | --- |
| Usługi w chmurze |Tak |Tak |Tak |
| Wystąpienia roli maszyny Wirtualnej IaaS i PaaS |Tak |Nie |Nie |
| Brama sieci VPN |Tak |Nie |Nie |
| Brama aplikacji |Tak |Nie |Nie |

## <a name="private-ip-addresses"></a>Prywatne adresy IP
Prywatne adresy IP Zezwalaj toocommunicate zasobów platformy Azure z innych zasobów w usłudze w chmurze lub [sieci wirtualnej](virtual-networks-overview.md)(VNet) lub w sieci lokalnej tooon (za pośrednictwem bramy sieci VPN lub obwodu ExpressRoute), bez użycia Internet dostępny adres IP.

W modelu wdrażania klasycznego Azure prywatnego adresu IP można przypisać toohello następujących zasobów platformy Azure:

* Maszyny wirtualne IaaS i wystąpienia roli PaaS
* Wewnętrzny moduł równoważenia obciążenia
* Brama aplikacji

### <a name="iaas-vms-and-paas-role-instances"></a>Maszyny wirtualne IaaS i wystąpienia roli PaaS
Maszyny wirtualnej (VM) utworzone za pomocą hello klasycznego modelu wdrażania są zawsze umieszczane w usłudze chmury, podobne wystąpień roli tooPaaS. zachowanie Hello prywatnych adresów IP w związku z tym są podobne do tych zasobów.

Jest ważne toonote, które usługa w chmurze mogą być wdrażane na dwa sposoby:

* Jako *autonomiczny* usługi, której nie znajduje się w sieci wirtualnej w chmurze.
* W ramach sieci wirtualnej.

#### <a name="allocation-method"></a>Metoda alokacji
W przypadku liczby *autonomiczny* cloud service, get zasoby przydzielone prywatnego adresu IP *dynamicznie* z prywatnego adresu IP centrum danych Azure hello zakresu adresów. Mogą być używane tylko do komunikacji z innych maszyn wirtualnych w ramach hello sama usługa w chmurze. Ten adres IP można zmienić, gdy zasób hello jest zatrzymana i uruchomiona.

W przypadku usługi w chmurze wdrożyć w ramach sieci wirtualnej, Pobierz prywatnej zasobów adresy IP przydzielone z zakresu adresów hello hello skojarzony adresy podsieci używane (jak określono w jego konfiguracji sieciowej). Ta prywatnych adresów IP może służyć do komunikacji między wszystkich maszyn wirtualnych w ramach hello sieci wirtualnej.

Ponadto w przypadku usług w chmurze w ramach sieci wirtualnej, prywatnego adresu IP jest przydzielany *dynamicznie* (przy użyciu protokołu DHCP) domyślnie. Może zmieniać podczas zasobów hello jest zatrzymana i uruchomiona. pozostaje adres IP hello tooensure hello same należy metodę alokacji hello tooset zbyt*statycznych*i podaj prawidłowy adres IP w ramach hello odpowiedniego zakresu adresów.

Statyczne prywatne adresy IP są powszechnie używane do:

* Maszyn wirtualnych, które działają jako kontrolery domeny lub serwery DNS.
* Maszyny wirtualne wymagające reguł zapory przy użyciu adresów IP.
* Maszyny wirtualne uruchomione usługi używane przez inne aplikacje za pomocą adresu IP.

#### <a name="internal-dns-hostname-resolution"></a>Wewnętrzny rozpoznawania nazwy hosta DNS
Wszystkie maszyny wirtualne platformy Azure i wystąpienia roli PaaS są skonfigurowane przy użyciu [serwery zarządzane Azure DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md#azure-provided-name-resolution) domyślnie, chyba że jawnie skonfigurować niestandardowych serwerów DNS. Te serwery DNS zapewniają rozpoznawania nazw wewnętrznych dla maszyn wirtualnych i wystąpień ról, które znajdują się w obrębie hello tej samej sieci wirtualnej lub usługę w chmurze.

Podczas tworzenia maszyny Wirtualnej, mapowanie hello hostname tooits prywatnego adresu IP jest dodawana toohello serwery zarządzane Azure DNS. W przypadku wielu kart Sieciowych maszyny Wirtualnej, jest mapowany hello hostname toohello prywatnego adresu IP hello podstawowej karty sieciowej. Informacje o mapowaniu jest jednak ograniczona tooresources w hello takie same w chmurze, usługi lub sieci wirtualnej.

W przypadku liczby *autonomiczny* cloud service, będziesz w stanie tooresolve nazwy hostów wszystkich wystąpień maszyn wirtualnych/roli w ramach hello sama usługa w chmurze tylko. W przypadku usługi w chmurze w ramach sieci wirtualnej można nazwy hostów stanie tooresolve wszystkich wystąpień maszyn wirtualnych/roli hello w hello sieci wirtualnej.

### <a name="internal-load-balancers-ilb--application-gateways"></a>Wewnętrzne moduły równoważenia obciążenia (ILB) i bramy aplikacji
Prywatne toohello adresów IP można przypisać **frontonu** konfiguracji [Azure wewnętrzny moduł równoważenia obciążenia](../load-balancer/load-balancer-internal-overview.md) (ILB) lub [brama aplikacji w usłudze Azure](../application-gateway/application-gateway-introduction.md). Ta prywatnego adresu IP służy jako wewnętrzny punkt końcowy, dostępny tylko zasoby toohello sieć wirtualną (VNet) i sieci zdalne hello połączony toohello sieci wirtualnej. Można przypisać albo dynamicznej lub statycznej prywatnej konfiguracji adresu IP toohello frontonu. Można także przypisać wielu prywatnego adresu IP adresów tooenable wielu wirtualnych adresów IP scenariuszy.

### <a name="at-a-glance"></a>W skrócie
Witaj w poniższej tabeli przedstawiono każdego typu zasobu z metod alokacji możliwe hello (dynamiczny/statyczny) i możliwości tooassign wiele prywatnych adresów IP.

| Zasób | Dynamiczny | Statyczny | Wiele adresów IP |
| --- | --- | --- | --- |
| Maszyna wirtualna (w *autonomiczny* usługi w chmurze) |Tak |Tak |Tak |
| Wystąpienia roli PaaS (w *autonomiczny* usługi w chmurze) |Tak |Nie |Tak |
| Wystąpienia roli maszyny Wirtualnej lub PaaS (w sieci wirtualnej) |Tak |Tak |Tak |
| Frontonu modułu równoważenia obciążenia wewnętrznego |Tak |Tak |Tak |
| Frontonu bramy aplikacji |Tak |Tak |Tak |

## <a name="limits"></a>Limity
w poniższej tabeli Hello pokazuje hello ograniczenia narzucone na IP adresowania na platformie Azure dla subskrypcji. Możesz [się z pomocą techniczną](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooincrease hello domyślne limity zapasowej maksymalnych toohello na podstawie Twoich potrzeb biznesowych.

|  | Limit domyślny | Limit maksymalny |
| --- | --- | --- |
| Publiczne adresy IP (dynamiczne) |5 |kontakt z pomocą techniczną |
| Zastrzeżone publiczne adresy IP |20 |kontakt z pomocą techniczną |
| Publiczny adres VIP dla wdrożenia (usługi w chmurze) |5 |kontakt z pomocą techniczną |
| Prywatny adres VIP (ILB) dla wdrożenia (usługi w chmurze) |1 |1 |

Upewnij się, że odczytu hello pełny zestaw [ogranicza sieciach](../azure-subscription-service-limits.md#networking-limits) na platformie Azure.

## <a name="pricing"></a>Cennik
W większości przypadków mogą publicznych adresów IP. Brak opłat nominalnego toouse dodatkowe i/lub statyczne publiczne adresy IP. Upewnij się, że rozumiesz hello [ceny struktury publiczne adresy IP](https://azure.microsoft.com/pricing/details/ip-addresses/).

## <a name="differences-between-resource-manager-and-classic-deployments"></a>Różnice między Resource Manager i w przypadku wdrożeń klasycznych
Poniżej przedstawiono porównanie funkcji adresowania IP w programie Menedżer zasobów i hello klasycznego modelu wdrażania.

|  | Zasób | Wdrożenie klasyczne | Resource Manager |
| --- | --- | --- | --- |
| **Publiczny adres IP** |***MASZYNA WIRTUALNA*** |Określony tooas ILPIP (tylko dynamiczny) |Określony tooas publicznego adresu IP (dynamiczna lub statyczna) |
|  ||Przypisane tooan maszyn wirtualnych IaaS lub wystąpień roli PaaS |Karta sieciowa toohello skojarzonego VM | |
|  |***Internet równoważenia obciążenia*** |Określony tooas VIP (dynamiczny) lub zastrzeżonego adresu IP (statyczny) |Określony tooas publicznego adresu IP (dynamiczna lub statyczna) | |
|  ||Usługi w chmurze tooa przypisany |Config frontonu modułu równoważenia obciążenia skojarzone toohello | |
|  | | | |
| **Prywatny adres IP** |***MASZYNA WIRTUALNA*** |Określony tooas a DIP |Określony tooas prywatnego adresu IP |
|  ||Przypisane tooan maszyn wirtualnych IaaS lub wystąpień roli PaaS |Przypisane toohello wirtualna karta sieciowa | |
|  |***Wewnętrzny moduł równoważenia obciążenia (ILB)*** |Przypisane toohello ILB (dynamiczna lub statyczna) |Konfiguracja frontonu przypisanej toohello ILB (dynamiczna lub statyczna) | |

## <a name="next-steps"></a>Następne kroki
* [Wdróż maszynę Wirtualną za pomocą statycznego prywatnego adresu IP](virtual-networks-static-private-ip-classic-pportal.md) przy użyciu hello portalu Azure.

