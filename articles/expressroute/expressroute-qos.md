---
title: "Wymagania dotyczące usługi ExpressRoute aaaQoS | Dokumentacja firmy Microsoft"
description: "Ta strona zawiera szczegółowe wymagania dotyczące konfigurowania technologii QoS oraz zarządzania nią na potrzeby obwodów usługi ExpressRoute."
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: 
ms.assetid: db1c1447-0283-4a09-907b-ae481adc40c7
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/25/2017
ms.author: cherylmc
ms.openlocfilehash: 46cc81bd38ff50dd9e7a1bfdd0faa457ff7b2fa1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-qos-requirements"></a>Wymagania dotyczące technologii QoS w usłudze ExpressRoute
Program Skype dla firm obejmuje różne obciążenia, które wymagają zróżnicowanej obsługi w technologii QoS. Jeśli planujesz tooconsume głosu usługi ExpressRoute, należy przestrzegać toohello wymagania opisane poniżej.

![](./media/expressroute-qos/expressroute-qos.png)

> [!NOTE]
> Mają zastosowanie wymagania QoS toohello komunikacji równorzędnej firmy Microsoft tylko. Witaj wartości DSCP w ruchu sieciowego w komunikacji równorzędnej publicznej platformy Azure i Azure prywatnej komunikacji równorzędnej otrzymano będzie too0 resetowania. 
> 
> 

Witaj Poniższa tabela zawiera listę oznaczenia wartościami DSCP używane przez usługi Skype dla firm. Odwołuje się zbyt[Zarządzanie QoS dla usługi Skype dla firm](https://technet.microsoft.com/library/gg405409.aspx) Aby uzyskać więcej informacji.

| **Klasa ruchu** | **Obsługa (oznaczanie DSCP)** | **Obciążenia programu Skype dla firm** |
| --- | --- | --- |
| **Połączenia głosowe** |EF (46) |Połączenia głosowe Skype/Lync |
| **Interaktywne** |AF41 (34) |Wideo, VBSS |
| AF21 (18) |Współdzielenie aplikacji | |
| **Domyślne** |AF11 (10) |Transfer plików |
| CS0 (0) |Inne | |

* Należy sklasyfikować hello obciążeń i oznaczenia wartościami DSCP prawo hello. Wykonaj hello wskazówki [tutaj](https://technet.microsoft.com/library/gg405409.aspx) na temat oznaczenia wartościami DSCP tooset w sieci.
* Skonfiguruj i obsługuj wiele kolejek w technologii QoS w sieci. Głosu musi być klasą autonomicznej i traktowane EF hello określone w dokumencie RFC 3246. 
* Można określić hello kolejkowania mechanizm, zasady wykrywania przeciążenia oraz możliwości przydziału przepustowości dla klasy ruchu. Jednak hello DSCP oznaczenie dla usługi Skype dla firm obciążeń muszą zostać zachowane. Jeśli używasz oznaczenia wartościami DSCP nie są wymienione powyżej, np. AF31 (26), muszą zmodyfikować tego too0 wartości DSCP przed wysłaniem tooMicrosoft pakietów hello. Firma Microsoft wysyła tylko pakietów oznaczonych hello wartości DSCP pokazano hello powyżej tabeli. 

## <a name="next-steps"></a>Następne kroki
* Zobacz wymagania toohello [Routing](expressroute-routing.md) i [NAT](expressroute-nat.md).
* Zobacz następujące hello łączy tooconfigure połączenie ExpressRoute.
  
  * [Tworzenie obwodu usługi ExpressRoute](expressroute-howto-circuit-classic.md)
  * [Configure routing (Konfigurowanie routingu)](expressroute-howto-routing-classic.md)
  * [Link sieci wirtualnej tooan obwodu usługi expressroute](expressroute-howto-linkvnet-classic.md)

