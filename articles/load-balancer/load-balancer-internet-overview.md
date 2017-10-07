---
title: "aaaInternet ukierunkowane Omówienie usługi równoważenia obciążenia | Dokumentacja firmy Microsoft"
description: "Omówienie internetowy modułu równoważenia obciążenia i ich funkcje. Jak usługi równoważenia obciążenia działa na platformie Azure przy użyciu maszyn wirtualnych i usług w chmurze."
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: tysonn
ms.assetid: 529b37aa-a45c-41d1-8877-fee8cc1fa375
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 3514f945d69ec576ed256cdd01069491e3e43936
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="internet-facing-load-balancer-overview"></a>Omówienie usługi równoważenia obciążenia połączonej Internet

Moduł równoważenia obciążenia Azure mapuje hello publicznego adresu IP adres i numer portu przychodzącego ruchu toohello prywatnego adresu IP adres i numer portu hello maszyny wirtualnej i na odwrót hello ruchu odpowiedzi z maszyny wirtualnej hello. Reguły równoważenia obciążenia pozwalają toodistribute określonych rodzajów ruchu sieciowego między wiele maszyn wirtualnych lub usług. Na przykład wielu serwerów sieci web lub role sieci web można rozmieścić hello obciążenia ruchu żądania sieci web.

Dla usługi w chmurze, zawierającej wystąpienia ról sieci web lub roli proces roboczy można określić publiczny punkt końcowy w pliku definicji (csdef) hello usługi.

Witaj *servicedefinition.csdef* plik zawiera hello konfiguracji punktu końcowego i jeśli istnieje wiele wystąpień roli we wdrożeniu roli sieci web lub procesu roboczego hello modułu równoważenia obciążenia będzie skonfigurowana. wdrożenie chmury tooyour wystąpień Hello sposób tooadd zmienia hello liczbę wystąpień w pliku konfiguracji usługi hello (.csfg).

Witaj poniższej ilustracji przedstawiono punktu końcowego równoważeniem obciążenia dla ruchu w sieci web współużytkowany trzech maszyn wirtualnych do hello publiczne i prywatne port TCP 80. Te trzy maszyny wirtualne są w zestawie o zrównoważonym obciążeniu.

![przykład modułu równoważenia obciążenia publiczny](./media/load-balancer-internet-overview/IC727496.png)

Rysunek 1 — równoważeniem obciążenia punktu końcowego dla ruchu w sieci web

Gdy klienci internetowi wysyłać żądania strony sieci web toohello publicznego adresu IP usługi w chmurze hello na porcie TCP 80, hello Azure Load Balancer rozdziela żądania hello między hello trzech maszyn wirtualnych w zestawie o zrównoważonym obciążeniu hello. Aby uzyskać więcej informacji na temat algorytmów równoważenia obciążenia, zobacz hello [strony Przegląd usługi równoważenia obciążenia](load-balancer-overview.md#load-balancer-features).

Domyślnie usługa równoważenia obciążenia Azure dystrybuuje ruch sieciowy równomiernie wielu wystąpień maszyny wirtualnej. Można również skonfigurować koligację sesji, aby uzyskać więcej informacji, zobacz [tryb dystrybucji modułu równoważenia obciążenia](load-balancer-distribution-mode.md).

## <a name="next-steps"></a>Następne kroki

Dowiedz się więcej o [wewnętrznego modułu równoważenia obciążenia](load-balancer-internal-overview.md) toobetter zrozumienie, które usługa równoważenia obciążenia jest lepszym rozwiązaniem dla danego wdrożenia w chmurze.

Możesz również [rozpocząć tworzenie internetowy modułu równoważenia obciążenia](load-balancer-get-started-internet-arm-ps.md) i skonfigurować typ [trybu rozkładu](load-balancer-distribution-mode.md) dla zachowania ruchu sieci usługi równoważenia obciążenia określonego.

Jeśli aplikacja wymaga połączenia tookeep aktywności dla serwerów za modułem równoważenia obciążenia, użytkownik może dowiedzieć się więcej o [ustawienia limitu czasu protokołu TCP dla usługi równoważenia obciążenia w stanie bezczynności](load-balancer-tcp-idle-timeout.md). Aby ułatwić toolearn dotyczących zachowania bezczynności połączenia podczas korzystania z usługi równoważenia obciążenia Azure.
