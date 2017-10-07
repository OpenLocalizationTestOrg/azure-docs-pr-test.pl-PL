---
title: "aaaPoint nazwę domeny firmy Internet domeny tooa Traffic Manager | Dokumentacja firmy Microsoft"
description: "Ten artykuł pomoże Ci wskaż nazwę domeny firmowej domeny nazwa tooa Menedżera ruchu."
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 29822946-2d45-4434-ba47-fc180a445cc3
ms.service: traffic-manager
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/11/2016
ms.author: kumud
ms.openlocfilehash: 84c428f60a1dc70452bf957d98a68c95e0b51715
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="point-a-company-internet-domain-tooan-azure-traffic-manager-domain"></a>Ustawianie firmowej domeny usługi Azure Traffic Manager tooan domeny Internet

Podczas tworzenia profilu usługi Traffic Manager platforma Azure automatycznie przypisuje nazwę DNS dla danego profilu. toouse nazwę strefy DNS, utworzyć rekord CNAME DNS, który mapuje nazwę domeny profilu usługi Traffic Manager toohello. Nazwa domeny usługi Traffic Manager hello można znaleźć w hello **ogólne** sekcji na stronie konfiguracji hello hello profilu usługi Traffic Manager.

Na przykład toopoint nazwy www.contoso.com toohello contoso.trafficmanager.net nazwy DNS Menedżera ruchu, należy utworzyć powitania po rekord zasobu DNS:

    www.contoso.com IN CNAME contoso.trafficmanager.net

Wszystkie żądania ruchu za*www.contoso.com* uzyskać kierowane za*contoso.trafficmanager.net*.

> [!IMPORTANT]
> Nie może wskazywać domeny drugiego poziomu, takich jak *contoso.com*, toohello domeny usługi Traffic Manager. Standardy protokołu DNS nie zezwalają na ustanawianie rekordów CNAME dla nazw domen drugiego poziomu.

## <a name="next-steps"></a>Następne kroki

* [Metody routingu w usłudze Traffic Manager](traffic-manager-routing-methods.md)
* [Traffic Manager — wyłączanie, włączanie lub usuwanie profilu](disable-enable-or-delete-a-profile.md)
* [Traffic Manager — wyłączanie lub włączanie punktu końcowego](disable-or-enable-an-endpoint.md)
