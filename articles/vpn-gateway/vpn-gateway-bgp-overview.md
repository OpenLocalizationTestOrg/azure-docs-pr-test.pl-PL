---
title: "aaaOverview protokołu BGP z bramy sieci VPN platformy Azure | Dokumentacja firmy Microsoft"
description: "Ten artykuł zawiera omówienie użycia protokołu BGP z bramami sieci VPN na platformie Azure."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: 
ms.assetid: f8c3985c-c128-4f34-835c-0e88742bf36e
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/12/2017
ms.author: yushwang
ms.openlocfilehash: ced3f77ecd791c84fb72b96447e839be3bf94846
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-bgp-with-azure-vpn-gateways"></a>Omówienie użycia protokołu BGP z bramami sieci VPN na platformie Azure
W tym artykule omówiono obsługę protokołu BGP (Border Gateway Protocol) w bramach sieci VPN na platformie Azure.

Protokół BGP jest hello standardowy protokół routingu często używane w hello Internet tooexchange routingu i uzyskiwanie informacji między dwie lub więcej sieci. Gdy używane w kontekście hello sieciach wirtualnych platformy Azure, BGP umożliwia bramy sieci VPN hello Azure i lokalnego urządzenia sieci VPN, o nazwie elementów równorzędnych protokołu BGP lub sąsiadów, tooexchange "tras" który poinformuje zarówno bramy na powitania dostępności i uzyskiwanie tych prefiksy toogo za pośrednictwem bramy hello lub routery związane. Protokół BGP można także włączyć routing tranzytowy między wieloma sieciami przez propagowania tras BGP bramy uczy się z jednego tooall elementu równorzędnego protokołu BGP innych elementów równorzędnych protokołu BGP. 

## <a name="why-use-bgp"></a>Dlaczego warto używać protokołu BGP?
Protokół BGP stanowi funkcję opcjonalną, której można używać z bramami sieci VPN na platformie Azure opartymi na trasie. Należy również upewnij się, że urządzenia sieci VPN między lokalnymi obsługuje protokołu BGP przed włączeniem funkcji hello. Można kontynuować toouse bramy sieci VPN platformy Azure i lokalnego urządzenia sieci VPN bez protokołu BGP. Jest hello odpowiednik przy użyciu statycznych tras (bez BGP) *a* przy użyciu routingu dynamicznego z protokołem BGP między sieciami i Azure.

Protokół BGP oferuje kilka zalet i nowych możliwości:

### <a name="support-automatic-and-flexible-prefix-updates"></a>Obsługa automatycznych i elastycznych aktualizacji prefiksów
Z obsługą protokołu BGP wystarczy toodeclare minimalna prefiks tooa określonego elementu równorzędnego protokołu BGP przez tunel VPN S2S protokołu IPsec hello. Można go jak prefiks hosta (/ 32) z hello adres IP elementu równorzędnego protokołu BGP lokalnego urządzenia sieci VPN. Można kontrolować, które lokalnymi prefiksy sieci ma tooadvertise tooAzure tooallow tooaccess Twojej sieci wirtualnej platformy Azure.

Można również anonsują większych prefiksy, które mogą zawierać części sieci wirtualnej prefiksy adresów, takich jak duże prywatnych przestrzeni adresów IP (np. 10.0.0.0/8). Należy pamiętać, chociaż hello prefiksy nie może być identyczny z jednym z prefiksami Twojej sieci wirtualnej. Te trasy identyczne tooyour sieci wirtualnej prefiksy zostaną odrzucone.

### <a name="support-multiple-tunnels-between-a-vnet-and-an-on-premises-site-with-automatic-failover-based-on-bgp"></a>Obsługa wielu tuneli między siecią wirtualną i lokacją lokalną z funkcją automatycznego trybu failover w oparciu o protokół BGP
Można ustanowić wiele połączeń między sieci wirtualnej platformy Azure i lokalnego urządzenia sieci VPN w hello tej samej lokalizacji. Ta funkcja udostępnia wiele tuneli (ścieżki) między dwiema sieciami hello w konfiguracji aktywny aktywny. Jeśli jeden z tuneli hello jest rozłączony, hello odpowiednie trasy zostaną wycofane za pośrednictwem protokołu BGP i hello ruch kierowany tuneli pozostałych toohello.

powitania po diagramie przedstawiono prosty przykład tej instalacji wysokiej dostępności:

![Wiele aktywnych ścieżek](./media/vpn-gateway-bgp-overview/multiple-active-tunnels.png)

### <a name="support-transit-routing-between-your-on-premises-networks-and-multiple-azure-vnets"></a>Obsługa routingu tranzytowego między sieciami lokalnymi i wieloma sieciami wirtualnymi na platformie Azure
BGP umożliwia wielu bram toolearn oraz propagację prefiksy z różnymi sieciami, czy są one bezpośrednio lub pośrednio połączone. Umożliwia to realizowany przy użyciu bram sieci VPN na platformie Azure routing tranzytowy między lokalnymi lokacjami lub w obrębie wielu sieci wirtualnych Azure.

Witaj poniższym diagramie przedstawiono przykład topologii z wieloma przeskokami z wielu ścieżek, które można przesyłania ruchem między sieciami dwóch lokalnych hello za pośrednictwem bramy sieci VPN platformy Azure w ramach hello Microsoft Networks:

![Przesyłanie z wieloma przeskokami](./media/vpn-gateway-bgp-overview/full-mesh-transit.png)

## <a name="bgp-faq"></a>CZĘSTO ZADAWANE PYTANIA DOTYCZĄCE PROTOKOŁU BGP
[!INCLUDE [vpn-gateway-bgp-faq-include](../../includes/vpn-gateway-bpg-faq-include.md)]

## <a name="next-steps"></a>Następne kroki
Zobacz [wprowadzenie do korzystania z protokołu BGP w bramach sieci VPN platformy Azure](vpn-gateway-bgp-resource-manager-ps.md) dla tooconfigure kroki BGP między lokalizacjami i połączeń do wirtualnymi.

