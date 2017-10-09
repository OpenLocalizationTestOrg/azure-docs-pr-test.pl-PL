---
title: "aaaI używania usług Mobile Services, w jaki sposób usługi App Service pomaga?"
description: "Dowiedz się, jakie korzyści usługa aplikacji osiągać tooyour istniejące projekty usług Mobile Services."
services: app-service\mobile
documentationcenter: ios
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 26b68a11-8352-4f78-acd2-e4e0ec177781
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: na
ms.topic: get-started-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 315cc6eedcdca6c3f9f9bb9fd5ec7baf655b7e20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started"> </a>Korzystam z usługi Mobile Services. Jak usługa App Service może mi pomóc?
## <a name="overview"></a>Omówienie
Istniejąca Usługa mobilna jest bezpieczna i pozostanie objęta pomocą techniczną. Istnieją jednak liczba hello zalety *usłudze Azure App Service* zapewnia platformę dla twojej aplikacji mobilnej, które nie są obecnie dostępne w usłudze Mobile Services:

* Prostsze, łatwiejsze i bardziej ekonomiczne oferty aplikacji obejmujących klientów sieci Web i mobilnych
* Nowe funkcje hosta, w tym zadania Web Job, niestandardowe nazwy CName, skuteczniejsze monitorowanie
* Gotowa do użycia funkcja integracji z usługą Traffic Manager
* Zasobów lokalnych tooyour łączności i sieci VPN w tooHybrid dodanie połączeń przy użyciu sieci wirtualnej
* Monitorowanie, alerty i rozwiązywanie problemów dotyczących aplikacji przy użyciu usługi NewRelic lub AppInsights
* Bogatsze spektrum hello podstawowych zasobów obliczeniowych i cen
* Wbudowane automatyczne skalowanie, równoważenie obciążenia i monitorowanie wydajności
* Wbudowane możliwości wdrażania przejściowego, tworzenia kopii zapasowych, wycofywania i testowania w produkcji

## <a name="new-hosting-features"></a>Nowe funkcje hostingu
W *usłudze Azure App Service* hello *aplikacji mobilnej* hello uruchamia kod zaplecza w tym samym kontenerze co aplikacja sieci Web i aplikacji interfejsu API. Jako taki może potrwać korzystać ze wszystkich funkcji hello w tym kontenerze, w tym również te, które nie są aktualnie dostępne w usłudze Mobile Services:

* Dodawanie działającej w sposób ciągły logiki zaplecza za pośrednictwem zadań Web Job.
* Sprawdzanie, czy kod zaplecza zawsze działa.
* Użyj niestandardowych rekordów CNAME tooprovide przyjazną i stabilny nazwy tooyour punktom końcowym zaplecza mobilnego
* Geograficzne skalowanie aplikacji przy użyciu usługi Traffic Manager.
* Uwzględnianie wszystkich wybranych bibliotek i pakietów.
* (.NET) Korzystanie z dowolnej funkcji programu ASP.NET, w tym MVC.
* (Dla środowiska Node.js) Korzystaj z dowolnej czystej biblioteki języka JavaScript ekosystemu węzła hello, w tym wspólnych bibliotek MVC.

## <a name="access-on-premises-data-using-vnet"></a>Dostęp do danych lokalnych przy użyciu sieci wirtualnej
Z usługami Mobile dzisiaj tooaccess połączeń hybrydowych już można używać zasobów lokalnych. W niektórych sytuacjach preferowane jest jednak użycie rozwiązania VPN. *Usługa Azure App Service* umożliwia korzystanie z sieci wirtualnej platformy Azure na potrzeby kodu zaplecza aplikacji mobilnej.

## <a name="use-your-favorite-backend-language"></a>Korzystanie z ulubionego języka zaplecza
*Usługa aplikacji Azure* oferty szerszy i bardziej rozbudowane obsługę platform ASP.NET i Node.js, w tym dostęp do najnowszych środowisk uruchomieniowych toohello.

## <a name="set-up-automatic-scale"></a>Ustawianie skalowania automatycznego
W przypadku usługi Mobile Services wszystkie wystąpienia kodu zaplecza były uruchamiane na małych maszynach wirtualnych. *Usługa aplikacji Azure* pozwala tooselect hello rozmiar maszyn wirtualnych ze znacznie większego zestawu opcji. Możesz szybko skalować w górę lub w poziomie toohandle dowolnych przychodzących obciążeń klientów, w oparciu o różne metryki wydajności.

## <a name="be-in-hello-know"></a>Można w hello "wiedzieć"
Zareagować tooissues w czasie rzeczywistym za pomocą monitorowania i alertów tooautomatically powiadamiania Ciebie i Twojego zespołu. Integracja i analizy aplikacji zaawansowane funkcje monitorowania usługi New Relic i AppInsights bardziej szczegółowego wglądu tooget w sposób wykonuje aplikacji mobilnej. Z *usłudze Azure App Service* można teraz konfigurować alerty oparte na różnych metrykach wydajności — programowo i za pośrednictwem hello portalu Azure.

## <a name="keep-your-assets-safe"></a>Zabezpieczanie zasobów
Automatycznie twórz kopię zapasową zaplecza i bazy danych. Kod i dane są bezpieczne po awarii i łatwo przywrócone, dzięki czemu toorun firmy bez obaw.

## <a name="ready-stage-go"></a>Gotowe, przejściowe, już!
Dzięki *usłudze Azure App Service* można teraz tworzyć wiele prywatnych środowisk testowania i przejściowych dla aplikacji mobilnych. Za ich pomocą tooperform testowanie przed wdrożeniem. Zamień tooproduction bez przestojów. Aplikacje sieci Web są wstępnie załadowane, dzięki czemu hello najlepszym środowisku klienta.

Aby rozpocząć korzystanie z zalet *usługi App Service* dla istniejącej Usługi mobilnej, wykonaj czynności opisane w tym [samouczku](app-service-mobile-migrating-from-mobile-services.md).
