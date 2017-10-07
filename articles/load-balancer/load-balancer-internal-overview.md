---
title: "Moduł równoważenia obciążenia aaaInternal omówienie | Dokumentacja firmy Microsoft"
description: "Omówienie dla wewnętrznego modułu równoważenia obciążenia i ich funkcje. Jak działa moduł równoważenia obciążenia dla platformy Azure i możliwe scenariusze tooconfigure wewnętrznych punktów końcowych"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: tysonn
ms.assetid: 36065bfe-0ef1-46f9-a9e1-80b229105c85
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 9a901aad224d8821c154e130e142699d57282b25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="internal-load-balancer-overview"></a>Omówienie usługi równoważenia obciążenia wewnętrznego

W odróżnieniu od hello Internet równoważenia obciążenia hello wewnętrznego modułu równoważenia obciążenia (ILB) określa, że ruch tooresources tylko wewnątrz usługi w chmurze hello lub przy użyciu sieci VPN tooaccess hello infrastruktury platformy Azure. Hello infrastruktury ogranicza dostęp toohello ze zrównoważonym obciążeniem wirtualnych adresów IP (VIP) usługi w chmurze lub sieć wirtualną tak, aby nigdy nie będą punktu końcowego Internet tooan bezpośrednio uwidocznione. To umożliwia wewnętrzny wiersz toorun aplikacje biznesowe (LOB) na platformie Azure i są dostępne z chmury hello lub z zasobami lokalnymi.

## <a name="why-you-may-need-an-internal-load-balancer"></a>Dlaczego może być konieczne wewnętrznego modułu równoważenia obciążenia

Azure wewnętrzny załadować równoważenia (ILB) zapewnia zrównoważenia obciążenia między maszyn wirtualnych, które znajdują się wewnątrz usługi w chmurze lub sieci wirtualnej z zakresu regionalnego. Informacje o konfiguracji sieci wirtualnych z zakresu regionalnego i użyj hello, zobacz [regionalnych sieci wirtualnych](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/) w hello Azure blog. Modułu ILB nie można zastosować w istniejących sieciach wirtualnych, które zostały skonfigurowane przy użyciu grupy koligacji.

ILB umożliwia hello następujące typy równoważenia obciążenia:

* W ramach usługi w chmurze z maszyny wirtualnej zestawu tooa maszyn wirtualnych, które znajdują się w obrębie hello sama usługa w chmurze (zobacz rysunek 1).
* W ramach sieci wirtualnej, z maszyn wirtualnych w zestawie tooa sieci wirtualnej hello maszyn wirtualnych, które znajdują się w obrębie hello sama usługa w chmurze z hello wirtualnych sieci (patrz rysunek 2).
* Dla sieci wirtualnej między lokalizacjami, z zestawu tooa komputerów lokalnych maszyn wirtualnych, które znajdują się w obrębie hello sama usługa w chmurze z hello wirtualnych sieci (patrz rysunek 3).
* Internetowy, wielowarstwowych aplikacji, w których hello zaplecza warstw nie są skierowane do Internetu, ale wymagają równoważenia obciążenia dla ruchu z hello internetowy warstwy.
* Równoważenie obciążenia dla aplikacji biznesowych hostowane na platformie Azure, bez konieczności dodatkowego obciążenia równoważenia sprzętu lub oprogramowania. W tym na serwerach lokalnych w hello zestaw komputerów, których ruch jest obciążenia zrównoważone.

## <a name="internet-facing-multi-tier-applications"></a>Aplikacje wielowarstwowe internetowy

Warstwa sieci web Hello ma Internet połączonej punktów końcowych dla klientów internetowych i jest częścią zestawu o zrównoważonym obciążeniu. Moduł równoważenia obciążenia Hello dystrybuuje ruch przychodzący z klientów w sieci web dla TCP port 443 (HTTPS) toohello serwerów sieci web.

serwery bazy danych Hello są za punktem końcowym ILB, której serwery sieci web hello jest używany przez Magazyn. Punkt końcowy, których ruch jest równoważone między serwerami bazy danych hello hello ILB zestawu o zrównoważonym obciążeniu usługi tej bazy danych.

powitania po obraz pokazuje hello internetowy aplikację wielowarstwową w hello sama usługa w chmurze.

![Wewnętrzny usługą równoważenia obciążenia, jednej chmury](./media/load-balancer-internal-overview/IC736321.png)

Rysunek 1 — internetowy wielowarstwową aplikację

Inny możliwości zastosowania dla aplikacji wielowarstwowych jest gdy hello ILB wdrożony tooa innej usługi w chmurze, niż hello jednej odbierającą usługi hello na powitania ILB.

Chmura punktem końcowym ILB toohello dostęp do usług za pomocą hello będzie mieć tej samej sieci wirtualnej. punktem końcowym ILB w hello hello powitania po pokazuje obrazu w innej usługi chmury z wewnętrznej bazy danych hello są serwery frontonu sieci web i przy użyciu tej samej sieci wirtualnej.

![Wewnętrzny zrównoważenia obciążenia między usługi w chmurze](./media/load-balancer-internal-overview/IC744147.png)

Rysunek 2 — serwery frontonu w innej usługi chmury

## <a name="intranet-line-of-business-applications"></a>Intranet linii aplikacji biznesowych

Ruch pochodzący od klientów w sieci lokalnej hello Pobierz równoważeniem obciążenia na powitania zestawu serwerów LOB przy użyciu sieci tooAzure połączenia sieci VPN.

Maszyna klienta Hello będzie mieć dostęp do adresu IP tooan z usługi sieci VPN platformy Azure przy użyciu sieci VPN toosite punktu. Umożliwia on hello hello użycia aplikacji LOB hostowanej za punktem końcowym ILB hello.

![Wewnętrzne równoważenie, przy użyciu sieci VPN toosite punktu obciążenia](./media/load-balancer-internal-overview/IC744148.png)

Rysunek 3 - aplikacji biznesowych przez punkt końcowy hello równoważeniem obciążenia

Inny scenariusz hello LOB jest toohave witryny toosite VPN toohello sieci wirtualnej którym punktem końcowym ILB hello jest skonfigurowane. Dzięki temu końcowym ILB toohello toobe kierowany ruch sieci lokalnej.

![Obciążenia wewnętrznego równoważenia przy użyciu witryny toosite sieci VPN](./media/load-balancer-internal-overview/IC744150.png)

Rysunek 4 - ruchu w sieci lokalnej kierowane punktem końcowym ILB toohello

## <a name="limitations"></a>Ograniczenia

Wewnętrzny moduł równoważenia obciążenia konfiguracje nie obsługują SNAT. W kontekście hello tego dokumentu SNAT odnosi się translatora adresów sieciowych źródła tooport Zamaskowana.  Dotyczy to tooscenarios których maszyn wirtualnych w puli usługi równoważenia obciążenia wymaga adresu IP frontonu tooreach hello odpowiednich wewnętrzny moduł równoważenia obciążenia firmy. W tym scenariuszu nie jest obsługiwana dla wewnętrznego modułu równoważenia obciążenia. Wystąpią błędy połączenia, gdy przepływ hello jest równoważone toohello maszyny Wirtualnej, które pochodzą hello przepływu. Należy użyć modułu równoważenia obciążenia styl serwera proxy dla takich scenariuszy.

## <a name="next-steps"></a>Następne kroki

[Pomocy technicznej platformy Azure Resource Manager dla usługi równoważenia obciążenia Azure](load-balancer-arm.md)

[Przed rozpoczęciem konfigurowania internetowy modułu równoważenia obciążenia](load-balancer-get-started-internet-arm-ps.md)

[Przed rozpoczęciem konfigurowania wewnętrznego modułu równoważenia obciążenia](load-balancer-get-started-ilb-arm-ps.md)

[Configure a Load balancer distribution mode](load-balancer-distribution-mode.md) (Konfigurowanie trybu dystrybucji modułu równoważenia obciążenia)

[Configure idle TCP timeout settings for your load balancer](load-balancer-tcp-idle-timeout.md) (Konfigurowanie ustawień limitu czasu bezczynności protokołu TCP dla modułu równoważenia obciążenia)
