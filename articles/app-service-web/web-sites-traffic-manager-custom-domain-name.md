---
title: "aaaConfigure niestandardowej nazwy domeny dla aplikacji sieci web w usłudze Azure App Service, który używa Menedżera ruchu do równoważenia obciążenia."
description: "Użyj nazwy domeny niestandardowej dla aplikacji sieci web w usłudze Azure App Service, która obejmuje usługi Traffic Manager w programie Równoważenie obciążenia."
services: app-service\web
documentationcenter: 
author: cephalin
manager: cfowler
editor: 
ms.assetid: 0f96c0e7-0901-489b-a95a-e3b66ca0a1c2
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2016
ms.author: cephalin
ms.openlocfilehash: dfde5fc6b445b30b10e03dcb03e8d072130d9377
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-a-custom-domain-name-for-a-web-app-in-azure-app-service-using-traffic-manager"></a>Konfigurowanie niestandardowej nazwy domeny dla aplikacji sieci web w usłudze Azure App Service przy użyciu Menedżera ruchu
[!INCLUDE [web-selector](../../includes/websites-custom-domain-selector.md)]

[!INCLUDE [intro](../../includes/custom-dns-web-site-intro-traffic-manager.md)]

Ten artykuł zawiera ogólne instrukcje dotyczące korzystania z usługi Azure App Service przy użyciu niestandardowej nazwy domeny, korzystających z usługi Traffic Manager w celu równoważenia obciążenia.

[!INCLUDE [tmwebsitefooter](../../includes/custom-dns-web-site-traffic-manager-notes.md)]

[!INCLUDE [introfooter](../../includes/custom-dns-web-site-intro-notes.md)]

<a name="understanding-records"></a>

## <a name="understanding-dns-records"></a>Opis rekordów DNS
[!INCLUDE [understandingdns](../../includes/custom-dns-web-site-understanding-dns-traffic-manager.md)]

<a name="bkmk_configsharedmode"></a>

## <a name="configure-your-web-apps-for-standard-mode"></a>Konfigurowanie aplikacji sieci web dla Tryb standardowy
[!INCLUDE [modes](../../includes/custom-dns-web-site-modes-traffic-manager.md)]

<a name="bkmk_configurecname"></a>

## <a name="add-a-dns-record-for-your-custom-domain"></a>Dodaj rekord DNS dla domeny niestandardowej
> [!NOTE]
> Jeśli zostały nabyte domeny przy użyciu aplikacji sieci Web usługi aplikacji Azure Pomiń następujące kroki i odwoływać się toohello ostatniego kroku [kupić domenę dla aplikacji sieci Web](custom-dns-web-site-buydomains-web-app.md) artykułu.
> 
> 

tooassociate domeny niestandardowej z aplikacją sieci web w usłudze Azure App Service, należy dodać nowy wpis w tabeli DNS hello dla domeny niestandardowej przy użyciu narzędzi dostarczonych przez rejestratora domen hello zakupionym z nazwą domeny. Używa hello następujące kroki toolocate i hello narzędzia systemu DNS.

1. Zaloguj się na koncie tooyour u rejestratora domen i poszukaj stronę Zarządzanie rekordami DNS. Znajdź łącza lub obszarów witryny hello oznaczone jako **nazwy domeny**, **DNS**, lub **nazwy serwera zarządzania**. Często łącza strony toothis można znaleźć można wyświetlanie informacji o koncie przez, a następnie sprawdzając takich jak łącze **mojej domeny**.
2. Po znalezieniu hello strony zarządzania dla nazwy domeny, poszukaj link umożliwiający rekordy DNS hello tooedit. Może to być wymieniona jako **pliku strefy**, **rekordy DNS**, lub jako **zaawansowane** link konfiguracji.
   
   * Strona Hello najprawdopodobniej będzie mieć kilka rekordów już utworzone, takich jak kojarzenie wpis "**@**"lub"\*" ze stroną "postojowego domeny". Może również zawierać rekordy dotyczące typowych poddomen takich jak **www**.
   * zaznaczyć strony Hello **rekordy CNAME**, lub podaj tooselect listy rozwijanej Typ rekordu. Go może również zawierać inne rekordy takich jak **rekordy** i **rekordów MX**. W niektórych przypadkach rekordy CNAME zostanie wywołana przez inne nazwy, takie jak **rekord aliasu**.
   * Strona Hello będą także mieć pól, które pozwalają zbyt**mapy** z **nazwy hosta** lub **nazwy domeny** tooanother nazwy domeny.
3. Podczas hello specyfice każdy Rejestrator różnią się ogólnie mapowania *z* niestandardową nazwę domeny (takich jak **contoso.com**,) *do* nazwy domeny usługi Traffic Manager hello (**contoso.trafficmanager.net**) używany dla aplikacji sieci web.
   
   > [!NOTE]
   > Alternatywnie Jeśli rekord jest już używana, należy toopreemptively powiązać tooit Twoje aplikacje, możesz utworzyć dodatkowe rekord CNAME. Na przykład powiązanie toopreemptively **www.contoso.com** tooyour aplikacji sieci web, Utwórz rekord CNAME z **awverify.www** za**contoso.trafficmanager.net**. Następnie można dodać "www.contoso.com" tooyour aplikacji sieci Web bez konieczności zmieniania rekord CNAME "www" hello. Aby uzyskać więcej informacji, zobacz [rekordy DNS Utwórz dla aplikacji sieci web w domenie niestandardowych][CREATEDNS].
   > 
   > 
4. Po zakończeniu dodawania lub modyfikowania rekordów DNS u rejestratora, Zapisz zmiany hello.

<a name="enabledomain"></a>

## <a name="enable-traffic-manager"></a>Menedżer ruchu
[!INCLUDE [modes](../../includes/custom-dns-web-site-enable-on-traffic-manager.md)]

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji, zobacz hello [Centrum deweloperów środowiska Node.js](/develop/nodejs/).

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- URL List -->

[CREATEDNS]: ../dns/dns-web-sites-custom-domain.md
