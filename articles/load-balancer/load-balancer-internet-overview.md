---
title: "Omówienie usługi równoważenia obciążenia internetowy | Dokumentacja firmy Microsoft"
description: "Omówienie internetowy modułu równoważenia obciążenia i ich funkcje. Jak usługi równoważenia obciążenia działa na platformie Azure przy użyciu maszyn wirtualnych i usług w chmurze."
services: load-balancer
documentationcenter: na
author: KumudD
manager: timlt
editor: tysonn
ms.assetid: 529b37aa-a45c-41d1-8877-fee8cc1fa375
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/25/2017
ms.author: kumud
ms.openlocfilehash: 5b9ffeadf6b1ffc4eaf4f49b85ba752c27da0e46
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/11/2017
---
# <a name="internet-facing-load-balancer-overview"></a>Omówienie usługi równoważenia obciążenia połączonej Internet

[!INCLUDE [load-balancer-basic-sku-include.md](../../includes/load-balancer-basic-sku-include.md)]

Moduł równoważenia obciążenia Azure mapuje publiczny adres IP i port numer ruchu przychodzącego do prywatnego adresu IP adres i numer portu maszyny wirtualnej i odwrotnie dla ruchu odpowiedzi z maszyny wirtualnej. Reguły równoważenia obciążenia umożliwiają dystrybucji określonych rodzajów ruchu sieciowego między wiele maszyn wirtualnych lub usług. Na przykład mogą rozprzestrzeniać się obciążenie ruchu w sieci web żądania wielu serwerów sieci web lub role sieci web.

Dla usługi w chmurze, zawierającej wystąpienia ról sieci web lub roli proces roboczy można określić publiczny punkt końcowy w pliku definicji (csdef) usługi.

*Servicedefinition.csdef* plik zawiera konfigurację punktu końcowego i jeśli istnieje wiele wystąpień roli we wdrożeniu roli sieci web lub procesu roboczego Instalatora dla niego będzie usługa równoważenia obciążenia. Liczba wystąpień w pliku konfiguracji usługi (.csfg) zmienia sposób można dodać do wdrożenia chmury wystąpień.

## <a name="example-of-an-internet-facing-load-balancer"></a>Przykład internetowy modułu równoważenia obciążenia

Na poniższej ilustracji przedstawiono punktu końcowego równoważeniem obciążenia dla ruchu w sieci web współużytkowany trzech maszyn wirtualnych dla publicznych i prywatnych port TCP 80. Te trzy maszyny wirtualne są w zestawie o zrównoważonym obciążeniu.

![przykład modułu równoważenia obciążenia publiczny](./media/load-balancer-internet-overview/IC727496.png)

Rysunek 1 — równoważeniem obciążenia punktu końcowego dla ruchu w sieci web

Gdy klienci internetowi wysyłać żądania strony sieci web do publicznego adresu IP na porcie TCP 80 usługi w chmurze, usługi równoważenia obciążenia Azure dystrybuuje żądania między trzy maszyny wirtualne w zestawie równoważeniem obciążenia. Aby uzyskać więcej informacji dotyczących algorytmów równoważenia obciążenia, zobacz [strony Przegląd usługi równoważenia obciążenia](load-balancer-overview.md#load-balancer-features).

Domyślnie usługa równoważenia obciążenia Azure dystrybuuje ruch sieciowy równomiernie wielu wystąpień maszyny wirtualnej. Można również skonfigurować koligację sesji, aby uzyskać więcej informacji, zobacz [tryb dystrybucji modułu równoważenia obciążenia](load-balancer-distribution-mode.md).

## <a name="next-steps"></a>Następne kroki

Dowiedz się więcej o [wewnętrznego modułu równoważenia obciążenia](load-balancer-internal-overview.md) aby lepiej zrozumieć, w których usługi równoważenia obciążenia jest lepszym rozwiązaniem dla danego wdrożenia w chmurze.

Możesz również [rozpocząć tworzenie internetowy modułu równoważenia obciążenia](load-balancer-get-started-internet-arm-ps.md) i skonfigurować typ [trybu rozkładu](load-balancer-distribution-mode.md) dla zachowania ruchu sieci usługi równoważenia obciążenia określonego.

Jeśli zastosowanie wymaga zachowania działających połączeń z serwerami za modułem równoważenia obciążenia, zapoznaj się z informacjami o [ustawieniach limitu czasu bezczynności protokołu TCP modułu równoważenia obciążenia](load-balancer-tcp-idle-timeout.md). Pozwoli to zrozumieć zachowanie bezczynnego połączenia podczas używania usługi Azure Load Balancer.
