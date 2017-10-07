---
title: "aaaOverview protokołu IPv6 dla modułu równoważenia obciążenia Azure | Dokumentacja firmy Microsoft"
description: "Opis obsługi protokołu IPv6 dla modułu równoważenia obciążenia w Azure i maszyn wirtualnych z równoważeniem obciążenia."
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
keywords: "Protokół IPv6, usługi równoważenia obciążenia azure, podwójnego stosu, publiczny adres ip, natywnego protokołu ipv6, mobile, iot"
ms.assetid: 6a1d583f-a305-40fd-a94b-fa42e1943bbb
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/14/2016
ms.author: kumud
ms.openlocfilehash: 5b203f77d86cc1ad455f4ebb297097aef46b658d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-ipv6-for-azure-load-balancer"></a>Omówienie protokołu IPv6 dla modułu równoważenia obciążenia Azure

Internetowy usług równoważenia obciążenia można wdrożyć przy użyciu adresu IPv6. Ponadto łączności tooIPv4 dzięki temu hello następujące możliwości:

* Natywny end-to-end łączności IPv6 między maszynami wirtualnymi Azure (maszyny wirtualne) i publiczny klientów internetowych za pośrednictwem usługi równoważenia obciążenia hello.
* Natywny end-to-end wychodzącego łączności IPv6 między maszynami wirtualnymi i publiczny klientów obsługujących protokół Internet IPv6.

Witaj poniższej ilustracji przedstawiono funkcje hello IPv6 dla usługi równoważenia obciążenia Azure.

![Moduł równoważenia obciążenia Azure z protokołu IPv6](./media/load-balancer-ipv6-overview/load-balancer-ipv6.png)

Po wdrożeniu IPv4 lub Internet włączony protokół IPv6 klienta może komunikować się z hello publicznych adresów IPv4 lub IPv6 lub nazwy hostów hello Azure internetowych usługi równoważenia obciążenia. trasy modułu równoważenia obciążenia Hello hello IPv6 pakietów toohello prywatne adresy IPv6 hello maszyn wirtualnych przy użyciu translatora adresów sieciowych (NAT). powitania klienta IPv6 Internet nie komunikują się bezpośrednio z hello adres IPv6 hello maszyn wirtualnych.

## <a name="features"></a>Funkcje

Natywnej obsługi protokołu IPv6 dla maszyn wirtualnych wdrożonych za pośrednictwem usługi Azure Resource Manager zapewnia:

1. Równoważeniem obciążenia IPv6 usług dla klientów protokołu IPv6 w hello Internet
2. Punkty końcowe natywnego protokołu IPv6 i IPv4 na maszynach wirtualnych ("dwa skumulowany")
3. Przychodzący i wychodzący zainicjowane natywnego połączenia protokołu IPv6
4. Obsługiwane protokoły TCP, UDP i HTTP (S) Włącz pełną gamę architektury usługi

## <a name="benefits"></a>Korzyści

Ta funkcja umożliwia hello następujące kluczowe korzyści:

* Spełniają wymaganie, aby nowe aplikacje był dostępny klienci wyłącznie internetowi tooIPv6 wykonawcze dla instytucji rządowych
* Włącz mobile i Internet skumulowany podwójnego tooaddress maszyn wirtualnych platformy Azure (IPv4 i IPv6) rzeczy (IOT) deweloperzy toouse hello rosnącym mobile & rynkach IOT

## <a name="details-and-limitations"></a>Szczegółowe informacje i ograniczenia

Szczegóły

* Hello usługa Azure DNS zawiera zarówno IPv4 A i IPv6 AAAA rejestruje nazwę i odpowiada rekordami zarówno dla usługi równoważenia obciążenia hello. powitania klienta wybiera które adresu (IPv4 lub IPv6) toocommunicate z.
* Gdy maszyna wirtualna inicjuje połączenia tooa połączony z Internetem IPv6 urządzenie publicznie, wirtualna hello źródłowy adres IPv6 jest (NAT) toohello publiczny adres IPv6 modułu równoważenia obciążenia hello translacji adresów sieciowych.
* Maszyny wirtualne z systemem operacyjnym Linux hello musi być skonfigurowany tooreceive adres IP protokołu IPv6 za pośrednictwem protokołu DHCP. Wiele hello Linux obrazów w galerii Azure są już hello skonfigurowane toosupport IPv6 bez żadnych modyfikacji. Aby uzyskać więcej informacji, zobacz [Konfigurowanie DHCPv6 dla maszyn wirtualnych systemu Linux](load-balancer-ipv6-for-linux.md)
* Jeśli wybierzesz toouse sondy kondycji z moduł równoważenia obciążenia, utworzyć sondy IPv4 i używać go zarówno hello IPv4 i IPv6 punktów końcowych. Jeśli usługa hello na maszynie Wirtualnej ulegnie awarii, zarówno hello IPv4 i IPv6 punktów końcowych są wyjmowane z obrotu.

Ograniczenia

* Nie można dodać reguły równoważenia obciążenia IPv6 w hello portalu Azure. Witaj reguły można tworzyć tylko za pomocą szablonu hello, interfejsu wiersza polecenia, programu PowerShell.
* Nie może uaktualnić istniejące adresy IPv6 toouse maszyn wirtualnych. Należy wdrożyć nowe maszyny wirtualne.
* Tooa jednym interfejsem sieciowym w każdej maszyny Wirtualnej można przypisać jeden adres IPv6.
* Witaj publiczne adresy IPv6 nie można przypisać tooa maszyny Wirtualnej. Ich można przypisać tylko tooa modułu równoważenia obciążenia.
* Nie można skonfigurować hello wstecznego wyszukiwania DNS dla sieci publicznych adresów IPv6.
* Witaj maszyn wirtualnych przy użyciu adresów IPv6 hello nie może być członkami usługi w chmurze platformy Azure. Można je tooan połączonych sieci wirtualnej platformy Azure (VNet) i komunikują się ze sobą za pośrednictwem ich adresów IPv4.
* Adresy IPv6 prywatnej można wdrożyć na poszczególnych maszynach wirtualnych w grupie zasobów, ale nie można wdrożyć w grupie zasobów za pomocą zestawów skali.
* Maszyny wirtualne platformy Azure nie może połączyć się za pośrednictwem IPv6 tooother w maszynach wirtualnych, usług platformy Azure lub urządzeń lokalnych. Można tylko komunikują się z modułem równoważenia obciążenia Azure hello za pośrednictwem protokołu IPv6. Jednak mogą się komunikować te inne zasoby przy użyciu protokołu IPv4.
* Ochrony sieciowej grupy zabezpieczeń (NSG) dla protokołu IPv4 jest obsługiwane w przypadku wdrożeń podwójny stos (IPv4 i IPv6). Grupy NSG są stosowane toohello punkty końcowe IPv6.
* punkt końcowy Hello IPv6 na powitania maszyna wirtualna nie jest bezpośrednio narażony toohello internet. Jest za modułem równoważenia obciążenia. Tylko hello porty określone w reguły modułu równoważenia obciążenia hello są dostępne za pośrednictwem protokołu IPv6.
* Zmiana hello IdleTimeout parametr dla protokołu IPv6 jest **obecnie nieobsługiwane**. Domyślna Hello to cztery minut.
* Zmiana hello parametru elementu loadDistributionMethod dla protokołu IPv6 jest **obecnie nieobsługiwane**.
* Zastrzeżone adresy IP protokołu IPv6 (gdzie IPAllocationMethod = static) są **obecnie nieobsługiwane**.

## <a name="next-steps"></a>Następne kroki

Dowiedz się, jak toodeploy modułu równoważenia obciążenia w przypadku adresu IPv6.

* [Dostępność IPv6 według regionu](https://go.microsoft.com/fwlink/?linkid=828357)
* [Wdrażanie równoważenia obciążenia w przypadku adresu IPv6 przy użyciu szablonu](load-balancer-ipv6-internet-template.md)
* [Wdrażanie równoważenia obciążenia w przypadku adresu IPv6 przy użyciu programu Azure PowerShell](load-balancer-ipv6-internet-ps.md)
* [Wdrażanie równoważenia obciążenia w przypadku adresu IPv6 przy użyciu wiersza polecenia platformy Azure](load-balancer-ipv6-internet-cli.md)
