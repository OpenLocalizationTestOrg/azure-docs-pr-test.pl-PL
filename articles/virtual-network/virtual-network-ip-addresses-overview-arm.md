---
title: "typy adresów aaaIP na platformie Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej na temat publicznych i prywatnych adresów IP na platformie Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
tags: azure-resource-manager
ms.assetid: 610b911c-f358-4cfe-ad82-8b61b87c3b7e
ms.service: virtual-network
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/27/2016
ms.author: jdial
ms.openlocfilehash: 402d3707c00f0b3bf3ef1febd5ade66223da74bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="ip-address-types-and-allocation-methods-in-azure"></a>Typy adresów IP i metody alokacji na platformie Azure
Można przypisać IP adresów tooAzure zasobów toocommunicate z innych zasobów platformy Azure, sieci lokalnej i hello Internet. Istnieją dwa typy adresów IP, których można użyć na platformie Azure:

* **Publiczne adresy IP**: używany do komunikacji z hello internetowych, takich jak Azure usługi publicznych
* **Adresy IP prywatnego**: używany do komunikacji w sieci wirtualnej platformy Azure (VNet) i lokalnej sieci podczas korzystania z bramy sieci VPN lub tooextend obwodu ExpressRoute tooAzure Twojej sieci.

> [!NOTE]
> Platforma Azure oferuje dwa różne modele wdrażania związane z tworzeniem zasobów i pracą z nimi: [model wdrażania przy użyciu usługi Azure Resource Manager i model klasyczny](../resource-manager-deployment-model.md).  W tym artykule omówiono przy użyciu modelu wdrażania Menedżera zasobów hello, który firma Microsoft zaleca dla większości nowych wdrożeń zamiast hello [klasycznego modelu wdrażania](virtual-network-ip-addresses-overview-classic.md).
> 

Jeśli znasz hello klasycznego modelu wdrażania, sprawdź hello [różnice między classic o adresowaniu IP i Menedżer zasobów](virtual-network-ip-addresses-overview-classic.md#differences-between-resource-manager-and-classic-deployments).

## <a name="public-ip-addresses"></a>Publiczne adresy IP
Publiczne adresy IP umożliwiają toocommunicate zasobów platformy Azure z publicznymi usługami Internet i Azure [pamięć podręczna Redis Azure](https://azure.microsoft.com/services/cache/), [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/), [baz danych](../sql-database/sql-database-technical-overview.md), i [magazynu Azure](../storage/common/storage-introduction.md).

W usłudze Azure Resource Manager [publiczny adres IP](resource-groups-networking.md#public-ip-address) jest zasobem, który ma własne właściwości. Zasób publiczny adres IP można skojarzyć z dowolną hello następujące zasoby:

* Maszyny wirtualne (VM)
* Moduły równoważenia obciążenia dostępne z Internetu
* Bramy sieci VPN
* Bramy aplikacji

### <a name="allocation-method"></a>Metoda alokacji
Istnieją dwie metody, w których adres IP jest przydzielany tooa *publicznego* IP zasobu, *dynamiczne* lub *statycznych*. Metoda alokacji domyślne Hello jest *dynamiczne*, gdzie adres IP jest **nie** przydzielane na powitania czasu jej utworzenia. Zamiast tego hello publiczny adres IP został przydzielony podczas uruchamiania (lub utworzyć) hello skojarzonych zasobów (takich jak wirtualna lub Usługa równoważenia obciążenia). adres IP Hello jest zwalniany, kiedy Zatrzymaj (lub usunąć) hello zasobów. Powoduje to toochange adres IP hello podczas zatrzymywania i uruchamiania zasobu.

adres IP hello tooensure dla hello zasobów pozostaje hello takie same, można ustawić metodę alokacji hello jawnie także*statycznych*. W takim przypadku adres IP jest przypisywany natychmiast. Po uwolnieniu tylko wtedy, gdy usunięcie zasobu hello lub zmienić jej metodę alokacji zbyt*dynamiczne*.

> [!NOTE]
> Nawet po ustawieniu metodę alokacji hello zbyt*statycznych*, nie można określić toohello przypisany adres IP rzeczywistego hello *publicznego adresu IP zasobu*. Zamiast tego pobiera przydzielone z puli dostępnych adresów IP w hello Azure lokalizacji zasobów hello jest tworzony w.
>

Statyczne publiczne adresy IP są często używane w hello następujące scenariusze:

* Użytkownicy końcowi potrzebują toocommunicate reguły zapory tooupdate z zasobów platformy Azure.
* Rozpoznawanie nazw DNS, gdzie zmiana adresu IP wymaga aktualizacji rekordów A.
* Zasoby platformy Azure komunikują się z innymi aplikacjami lub usługami, które korzystają z modelu zabezpieczeń opartych na adres IP.
* Możesz używać adresu IP połączonego tooan certyfikaty SSL.

> [!NOTE]
> Lista Hello zakresy adresów IP, z których publicznych adresów IP (dynamiczny/statyczny) zasoby są przydzielane tooAzure jest opublikowana w [zakresy IP centrum danych Azure](https://www.microsoft.com/download/details.aspx?id=41653).
>

### <a name="dns-hostname-resolution"></a>Rozpoznawanie nazw hostów DNS
Można określić etykiety nazwy domeny DNS dla publicznego zasób adresu IP, który tworzy mapowanie dla *domainnamelabel*. *Lokalizacja*. cloudapp.azure.com toohello publicznego adresu IP w hello serwery zarządzane Azure DNS. Na przykład jeśli utworzono zasób publicznego adresu IP z **contoso** jako *domainnamelabel* w hello **zachodnie stany USA** Azure *lokalizacji*, hello pełni kwalifikowaną nazwę domeny (FQDN) **contoso.westus.cloudapp.azure.com** rozwiąże toohello publicznego adresu IP hello zasobów. Można użyć tej nazwy FQDN toocreate domeny niestandardowej rekord CNAME, wskazując toohello publicznego adresu IP na platformie Azure.

> [!IMPORTANT]
> Każda utworzona etykieta nazwy domeny musi być unikatowa w swojej lokalizacji na platformie Azure.  
>

### <a name="virtual-machines"></a>Maszyny wirtualne
Możesz skojarzyć publiczny adres IP z [Windows](../virtual-machines/windows/overview.md) lub [Linux](../virtual-machines/virtual-machines-linux-about.md) maszyny Wirtualnej, przypisując tooits **interfejsu sieciowego**. W przypadku hello maszyny wirtualnej z wieloma interfejsami sieciowymi, można go przypisać toohello *głównej* tylko interfejsu sieciowego. Można przypisać z dynamicznego lub statycznego publicznego adresu IP adres tooa maszyny Wirtualnej.

### <a name="internet-facing-load-balancers"></a>Moduły równoważenia obciążenia dostępne z Internetu
Możesz skojarzyć publiczny adres IP z [moduł równoważenia obciążenia Azure](../load-balancer/load-balancer-overview.md), przypisując toohello modułu równoważenia obciążenia **frontonu** konfiguracji. Ten publiczny adres IP służy jako wirtualny adres IP (VIP) o zrównoważonym obciążeniu. Można przypisać z dynamicznego lub statycznego publicznego adresu IP adres tooa modułu równoważenia obciążenia frontonu. Można także przypisać wiele publicznego adresu IP adresów tooa modułu równoważenia obciążenia frontonu, dzięki czemu [wielu wirtualnych adresów IP](../load-balancer/load-balancer-multivip.md) scenariuszy, takich jak środowiska z wieloma dzierżawami z witrynami sieci Web oparta na protokole SSL.

### <a name="vpn-gateways"></a>Bramy sieci VPN
[Brama sieci VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md) jest używane tooconnect sieci wirtualnej platformy Azure (VNet) tooother sieci wirtualnych platformy Azure lub tooan sieci lokalnej. Należy tooassign publicznego tooits adres IP **konfiguracji IP** tooenable on toocommunicate hello sieci zdalnej. Obecnie można przypisać tylko *dynamiczne* publicznego bramy sieci VPN tooa adresów IP.

### <a name="application-gateways"></a>Bramy aplikacji
Publiczny adres IP można skojarzyć z platformy Azure [brama aplikacji w](../application-gateway/application-gateway-introduction.md), przypisując bramy toohello **frontonu** konfiguracji. Ten publiczny adres IP służy jako adres VIP o zrównoważonym obciążeniu. Obecnie można przypisać tylko *dynamiczne* publicznej konfiguracji adresu IP tooan aplikacji bramy serwera sieci Web.

### <a name="at-a-glance"></a>W skrócie
w poniższej tabeli Hello pokazuje hello konkretnej właściwości, za pomocą których może być publiczny adres IP skojarzony tooa zasobu najwyższego poziomu i metod alokacji możliwe hello (dynamiczna lub statyczna), które mogą być używane.

| Zasób najwyższego poziomu | Skojarzenie adresu IP | Dynamiczny | Statyczny |
| --- | --- | --- | --- |
| Maszyna wirtualna |Interfejs sieciowy |Tak |Tak |
| Moduł równoważenia obciążenia |Konfiguracja frontonu |Tak |Tak |
| Brama sieci VPN |Konfiguracja adresu IP bramy |Tak |Nie |
| Brama aplikacji |Konfiguracja frontonu |Tak |Nie |

## <a name="private-ip-addresses"></a>Prywatne adresy IP
Zezwalaj na prywatne adresy IP toocommunicate zasobów platformy Azure z innych zasobów w [sieci wirtualnej](virtual-networks-overview.md) lub sieci lokalnej za pośrednictwem bramy sieci VPN lub obwodu ExpressRoute, bez korzystania z adresu IP dostępny z Internetu.

W modelu wdrażania usługi Azure Resource Manager hello prywatnego adresu IP jest skojarzony toohello następujące typy zasobów platformy Azure:

* Maszyny wirtualne
* Wewnętrzne moduły równoważenia obciążenia (ILB)
* Bramy aplikacji

### <a name="allocation-method"></a>Metoda alokacji
Prywatny adres IP został przydzielony adres powitania od zakresu hello podsieci toowhich hello zasobu jest dołączony. zakres adresów Hello hello podsieć jest częścią zakresu adresów hello sieci wirtualnej.

Istnieją dwie metody przydzielania prywatnego adresu IP: *dynamiczna* i *statyczna*. Metoda alokacji domyślne Hello jest *dynamiczne*, gdzie adres IP hello jest automatycznie przydzielony z podsieci hello zasób (za pomocą protokołu DHCP). Ten adres IP, można zmienić podczas zatrzymywania i uruchamiania hello zasobów.

Można ustawić metodę alokacji hello także*statycznych* pozostaje adres IP hello tooensure hello takie same. W takim przypadku należy również tooprovide prawidłowy adres IP, który jest częścią podsieci hello zasobów.

Statyczne prywatne adresy IP są powszechnie używane do:

* Maszyn wirtualnych, które działają jako kontrolery domeny lub serwery DNS.
* Zasobów, które wymagają reguł zapory korzystających z adresów IP.
* Zasoby dostępne dla innych aplikacji/zasobów za pomocą adresu IP.

### <a name="virtual-machines"></a>Maszyny wirtualne
Prywatny adres IP jest przypisany toohello **interfejsu sieciowego** z [Windows](../virtual-machines/windows/overview.md) lub [Linux](../virtual-machines/virtual-machines-linux-about.md) maszyny Wirtualnej. W przypadku maszyny wirtualnej z wieloma interfejsami sieciowymi każdy interfejs otrzymuje przypisany prywatny adres IP. Metoda alokacji hello można określić jako dynamiczne lub statyczne dla interfejsu sieciowego.

#### <a name="internal-dns-hostname-resolution-for-vms"></a>Wewnętrzne rozpoznawanie nazwy hosta DNS (dla maszyn wirtualnych)
Wszystkie maszyny wirtualne platformy Azure są domyślnie skonfigurowane z [serwerami DNS zarządzanymi przez platformę Azure](virtual-networks-name-resolution-for-vms-and-role-instances.md#azure-provided-name-resolution), chyba że jawnie skonfigurujesz niestandardowe serwery DNS. Te serwery DNS zapewniają rozpoznawania nazw wewnętrznych dla maszyn wirtualnych znajdujących się w obrębie hello sam sieci wirtualnej.

Podczas tworzenia maszyny Wirtualnej, mapowanie hello hostname tooits prywatnego adresu IP jest dodawana toohello serwery zarządzane Azure DNS. W przypadku interfejsu wielu sieci maszyny Wirtualnej jest mapowany hello hostname toohello prywatnego adresu IP hello podstawowy interfejs sieciowy.

Maszyny wirtualne skonfigurowane przy użyciu serwerów DNS zarządzane Azure będzie nazwy hostów hello stanie tooresolve wszystkich maszyn wirtualnych w ramach sieci wirtualnej tootheir prywatne adresy IP.

### <a name="internal-load-balancers-ilb--application-gateways"></a>Wewnętrzne moduły równoważenia obciążenia (ILB) i bramy aplikacji
Prywatne toohello adresów IP można przypisać **frontonu** konfiguracji [Azure wewnętrzny moduł równoważenia obciążenia](../load-balancer/load-balancer-internal-overview.md) (ILB) lub [brama aplikacji w usłudze Azure](../application-gateway/application-gateway-introduction.md). Ta prywatnego adresu IP służy jako wewnętrzny punkt końcowy, dostępny tylko zasoby toohello sieć wirtualną (VNet) i sieci zdalne hello połączony toohello sieci wirtualnej. Można przypisać albo dynamicznej lub statycznej prywatnej konfiguracji adresu IP toohello frontonu.

### <a name="at-a-glance"></a>W skrócie
w poniższej tabeli Hello pokazuje hello konkretnej właściwości, za pomocą których może być prywatny adres IP skojarzone tooa zasobu najwyższego poziomu i metod alokacji możliwe hello (dynamiczna lub statyczna), które mogą być używane.

| Zasób najwyższego poziomu | Skojarzenie adresu IP | Dynamiczny | Statyczny |
| --- | --- | --- | --- |
| Maszyna wirtualna |Interfejs sieciowy |Tak |Tak |
| Moduł równoważenia obciążenia |Konfiguracja frontonu |Tak |Tak |
| Brama aplikacji |Konfiguracja frontonu |Tak |Tak |

## <a name="limits"></a>Limity
Witaj ograniczenia narzucone na adresy IP są wskazane hello pełny zestaw [ogranicza sieciach](../azure-subscription-service-limits.md#networking-limits) na platformie Azure. Te ograniczenia są podzielone według regionu i subskrypcji. Możesz [się z pomocą techniczną](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooincrease hello domyślne limity zapasowej maksymalnych toohello na podstawie Twoich potrzeb biznesowych.

## <a name="pricing"></a>Cennik
Publiczne adresy IP mogą być związane z nominalnymi opłatami. adres toolearn więcej informacji na temat IP cennik na platformie Azure, przejrzyj hello [cennik adres IP](https://azure.microsoft.com/pricing/details/ip-addresses) strony.

## <a name="next-steps"></a>Następne kroki
* [Wdróż maszynę Wirtualną za pomocą statycznego publicznego adresu IP za pomocą hello portalu Azure](virtual-network-deploy-static-pip-arm-portal.md)
* [Wdrażanie maszyny wirtualnej ze statycznym publicznym adresem IP przy użyciu szablonu](virtual-network-deploy-static-pip-arm-template.md)
* [Wdrożenie maszyny Wirtualnej za pomocą statycznego prywatnego adresu IP przy użyciu hello portalu Azure](virtual-networks-static-private-ip-arm-pportal.md)
