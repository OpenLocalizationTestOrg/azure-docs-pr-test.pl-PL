---
title: "aaaEnabling zakończenia tooend protokół SSL dla bramy aplikacji Azure | Dokumentacja firmy Microsoft"
description: "Ta strona zawiera omówienie tooend zakończenia bramy aplikacji hello obsługi protokołu SSL."
documentationcenter: na
services: application-gateway
author: amsriva
manager: rossort
editor: amsriva
ms.assetid: 3976399b-25ad-45eb-8eb3-fdb736a598c5
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: amsriva
ms.openlocfilehash: c5cb398a1e7d9a08662a3120baad98edb5575917
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-end-tooend-ssl-with-application-gateway"></a>Przegląd końcowy tooend SSL z bramy aplikacji

Brama aplikacji w obsługuje kończenia żądań SSL na powitania bramy, po zwykle przepływu ruchu, który niezaszyfrowanej toohello serwerów wewnętrznej bazy danych. Ta funkcja umożliwia unburdened z kosztownych koszty szyfrowania i odszyfrowywania toobe serwerów sieci web. Jednak w przypadku niektórych klientów serwerów wewnętrznej bazy danych toohello niezaszyfrowane komunikacja nie jest dopuszczalne opcją. Niezaszyfrowane komunikacji może być ze względu na wymagania toosecurity, wymagania dotyczące zgodności, lub aplikacja hello mogą tylko zaakceptować bezpiecznego połączenia. Dla takich aplikacji bramy aplikacji obsługuje zakończenia tooend protokołu SSL szyfrowania.

## <a name="overview"></a>Omówienie

Tooend końcowych SSL pozwala toosecurely przesyłać szyfrowane, gdy nadal korzystanie z zalet funkcji równoważenia obciążenia warstwy 7 hello bramę aplikacji zawiera poufne dane toohello wewnętrznej bazy danych. Niektóre z tych funkcji są koligacji na podstawie plików cookie sesji, na podstawie adresu URL routingu, pomocy technicznej dla routingu na podstawie witryn lub możliwości tooinject X - przekazywane-* nagłówków.

Przy zastosowaniu trybu komunikacji SSL tooend zakończenia, brama aplikacji w kończy hello sesji SSL na powitania bramy i odszyfrowuje ruchu użytkowników. Stosuje następnie hello skonfigurowane reguły tooselect odpowiednie zaplecza puli wystąpienia tooroute ruchu. Brama aplikacji w następnie inicjuje nowy serwer wewnętrznej bazy danych toohello połączenia SSL i ponownie szyfruje dane przy użyciu certyfikatu klucza publicznego serwera wewnętrznej bazy danych hello przed przesłaniem hello żądania toohello wewnętrznej bazy danych. Tooend zakończenia, który jest włączony protokół SSL, ustawiając ustawienia protokołu w tooHTTPS BackendHTTPSetting, który jest następnie stosowany tooa puli wewnętrznej bazy danych. Każdy serwer wewnętrznej bazy danych w puli zaplecza hello z tooend zakończenia, który włączony protokół SSL musi mieć certyfikat tooallow bezpiecznej komunikacji.

![Scenariusz ssl tooend zakończenia][1]

W tym przykładzie żądań przy użyciu TLS1.2 są serwerami routingiem toobackend w Pool1 przy użyciu tooend końcowych SSL.

## <a name="end-tooend-ssl-and-whitelisting-of-certificates"></a>Zakończenie tooend SSL i certyfikatów niedozwolonych

Brama aplikacji w komunikuje się tylko z zaplecza znane są wystąpienia białej swój certyfikat z bramy aplikacji hello. niedozwolonych tooenable certyfikaty, należy przekazać klucza publicznego hello bramy aplikacji toohello certyfikaty serwera wewnętrznej bazy danych (nie hello certyfikatu głównego). Następnie dozwolone są tylko połączenia tooknown i białej zapleczy. Witaj pozostałych zapleczy powoduje błąd bramy. Certyfikaty z podpisem własnym są przeznaczone tylko do celów testowych i nie są zalecane dla obciążeń w środowisku produkcyjnym. Takie certyfikaty mają białej toobe z bramy aplikacji hello zgodnie z opisem w poprzednich krokach przed ich użyciem hello.

## <a name="next-steps"></a>Następne kroki

Po zapoznawanie tooend końcowych SSL, przejdź zbyt[włączyć tooend końcowych SSL na bramie aplikacji](application-gateway-end-to-end-ssl-powershell.md) toocreate bramy aplikacji przy użyciu kończyć tooend protokołu SSL.

<!--Image references-->

[1]: ./media/application-gateway-backend-ssl/scenario.png
