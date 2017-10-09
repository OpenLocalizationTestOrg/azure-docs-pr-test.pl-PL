---
title: "Omówienie aaaRedirect bramy aplikacji Azure | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat możliwości przekierowania hello bramę aplikacji Azure"
services: application-gateway
documentationcenter: na
author: amsriva
manager: timlt
editor: 
tags: azure-resource-manager
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/18/2017
ms.author: amsriva
ms.openlocfilehash: 7149e3bd000d336c51995fb0e90f971b4d9ba2be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="application-gateway-redirect-overview"></a>Omówienie przekierowania bramy aplikacji

Typowy scenariusz dla wielu aplikacji sieci web jest toosupport automatyczne HTTP tooHTTPS przekierowania tooensure cała komunikacja między aplikacją a jego użytkowników występuje za pośrednictwem ścieżki zaszyfrowane. W ciągu ostatnich hello klienci użyto technik, takich jak tworzenie puli dedykowanych wewnętrznej bazy danych, którego jedynym celem jest tooredirect żądań, które otrzymuje na HTTP tooHTTPS.  Brama aplikacji w obsługuje teraz możliwość tooredirect ruchu na powitania bramy aplikacji. Upraszcza konfigurację aplikacji, optymalizację użycia zasobów hello i obsługę nowych scenariuszy przekierowania tym globalnych i opartych na ścieżce przekierowania. Obsługa przekierowania bramy aplikacji nie jest ograniczona tylko przekierowania HTTPS -> tooHTTP. Jest to mechanizm ogólnego przekierowania, co umożliwia obsługę przekierowywania ruchu odbieranego na jeden odbiornik tooanother odbiornika dla bramy aplikacji. Obsługuje ona również przekierowania tooan zewnętrznej witryny również. Obsługa przekierowania bramy aplikacji oferuje hello następujące możliwości:

1. Globalne przekierowanie z jednego odbiornika odbiornika tooanother na powitania bramy. Dzięki temu tooHTTPS przekierowywania w lokacji.
2. Przekierowanie na podstawie ścieżki. Tego typu przekierowania umożliwia przekierowywanie HTTP tooHTTPS tylko w obszarze określonej lokacji, na przykład obszar koszyka zakupów wskazywane przez/koszyka / *.
3. Przekieruj tooexternal lokacji.

![przekierowania](./media/application-gateway-redirect-overview/redirect.png)

Dzięki tej zmianie klientów musi toocreate nowy obiekt konfiguracji przekierowania, określający odbiornika docelowy hello lub wymagane jest przekierowanie toowhich zewnętrznej witryny. element konfiguracji Hello obsługuje również tooenable opcje dołączanie hello ścieżka identyfikatora URI i zapytań, ciąg toohello przekierowany adres URL. Klientów można również wybrać, czy Przekierowanie tymczasowe (kod stanu HTTP 302) lub przekierowanie trwałe (kod stanu HTTP 301). Po utworzeniu tej konfiguracji przekierowania jest dołączona toohello źródła odbiornika za pomocą nowej reguły. Przy użyciu podstawowe reguły hello przekierowania konfiguracja jest skojarzony z odbiornika źródła i globalnych przekierowania. Stosowania reguły na podstawie ścieżki konfiguracji przekierowania hello jest zdefiniowana na mapie ścieżki adresu URL hello i dlatego ma zastosowanie tylko w obszarze określonej ścieżki toohello lokacji.

### <a name="next-steps"></a>Następne kroki

[Skonfiguruj adres URL przekierowania na bramy aplikacji](application-gateway-configure-redirect-powershell.md)
