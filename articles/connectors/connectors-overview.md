---
title: "aaaOverview łączników aplikacji logiki | Dokumentacja firmy Microsoft"
description: "Omówienie łączniki, które mogą być używane w aplikacji logiki"
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: ca8dab2e-9b69-4b1e-865d-1facd9f0cdac
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/15/2016
ms.author: jehollan
ms.openlocfilehash: dc4cac4c0dfaa2f9fd218ffc04414fa8e52a91d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-connectors-in-a-logic-app"></a>Używanie łączników w aplikacji logiki
Łączników udostępnia akcji tooevents szybki dostęp, danych i usług, protokołów i platform.  Witaj pełną listę łączników, które obsługuje Logic Apps można [można znaleźć tutaj](apis-list.md).  Łączniki mogą być używane jako wyzwalacz lub akcji w aplikacji logiki i może wymagać skonfigurowany *połączenia* toouse (na przykład: autoryzowanie Twitter konta tooaccess lub post w Twoim imieniu).

## <a name="basics"></a>Podstawy
Łączniki są obsługiwane usługi są dostępne jako część logiki toointegrate aplikacji z innych usług, takich jak Dynamics, Azure, Salesforce, [i więcej](apis-list.md).  Są wdrażane i zarządzane przez firmę Microsoft, więc można tworzyć przepływy pracy integracji z skali, przepływności i podjąć obsługę zabezpieczeń.  Można dodać aplikacji logiki tooa łącznika wyszukiwanie i wybierając akcję łącznik lub wyzwolenia w obszarze **Pokaż Microsoft zarządzanych interfejsów API**.

![Menu Akcja wybierania wyzwalacza][1]

Każdy łącznik akcji lub wyzwalacza będzie mieć jego zbiór właściwości tooconfigure.  Kliknij hello informacji przycisków toolearn więcej informacji na temat akcji lub odwołać dokumentacji [toolearn więcej](apis-list.md).

Jeśli chcesz toointegrate z usługą lub interfejsu API, które nie są jeszcze łącznika można rozszerzać logiki aplikacji za pośrednictwem [niestandardowy łącznik](../logic-apps/logic-apps-create-api-app.md) lub po prostu Wywołaj bezpośrednio toohello usługi za pośrednictwem protokołu, takich jak HTTP.

## <a name="triggers"></a>Wyzwalacze
Niektóre łączniki ma wyzwalacz, co oznacza zdarzenia z tego łącznika spowoduje uruchomienie aplikacji logiki i przekazywanie danych w ramach wyzwalacza hello.  Wyzwalacz jest zawsze hello pierwszym etapem aplikacji logiki.  Wyzwalacze popularnych obejmują operacje takie jak:

* Cyklu — uruchamiane co godzinę
* Po odebraniu żądania HTTP
* Po dodaniu elementu tooa kolejki
* Po odebraniu wiadomości e-mail

Niektóre wyzwalacze uruchomią hello błyskawicznych zdarzeń odbywa się w ramach aplikacji logiki toohello powiadomień, a inne interwał cyklu skonfigurowane na częstotliwość hello aplikacji logiki będzie sprawdzać usługi hello zdarzenie (w górę tooevery 15 sekund), należy.  

Po odebraniu zdarzenia, uruchom aplikację logiki hello będą uruchamiane, a hello działań w przepływie pracy hello zostanie uruchomiony.  Można również tooaccess może wyzwolić żadnych danych z hello w całym przepływie pracy hello (na przykład hello "na nowy tweet" wyzwalacza przekazuje hello tweet na powitania Uruchom).

## <a name="actions"></a>Akcje
Większość łączników ma jednego lub wielu akcje, które mogą być wykonywane w ramach hello przepływu pracy.  Akcje są wszystkie kroki, które stanie po uruchomieniu hello zostało uruchomione z wyzwalacza.  tooadd akcji kliknij hello **nowy krok** przycisk i wyszukaj hello ma toouse łącznika.  Raz wybrane (i po konfigurowanie wszelkich [połączeń](#connections) które mogą być wymagane) zobaczysz hello akcji karty można skonfigurować.  Wybierz dane z poprzednich kroków, klikając na dowolnym hello tokenów dla danych wyjściowych lub wprowadź w dowolnej innej konfiguracji zgodnie z potrzebami.

![Konfigurowanie akcji łącznika][2]

## <a name="connections"></a>Połączenia
Większość łączników wymagają tooconfigure *połączenia* przed użyciem hello łącznika.  A *połączenia* jest żadnych nazwą logowania lub Konfiguracja połączenia potrzebna tooaccess hello łącznika.  Łączniki, które korzysta z protokołu OAuth i tworzyć połączenia oznacza logowanie do usługi hello (takich jak usługi Office 365, Salesforce lub GitHub), gdzie tokenu dostępu mogą być szyfrowane i bezpiecznie przechowywane w magazynie Azure tajny.  Inne łączniki (na przykład FTP i SQL) wymagają połączenie, zawierający konfigurację, takie jak adres serwera, nazwę użytkownika i hasło.  Te dane konfiguracyjne połączenia są również są szyfrowane i bezpiecznie zmagazynowane.  Połączenia będą mogli tooaccess hello usługi, tak długo, jak usługa hello umożliwia.  Dla połączeń usługi Azure Active Directory OAuth (takich jak usługi Office 365 i Dynamics) może w dalszym ciągu tokenu dostępu hello toorefresh przez nieograniczony czas.  Inne usługi może wprowadzić limity na jak długo możemy użyć tokenu bez Trwa odświeżanie.  Ogólnie rzecz biorąc pewne akcje, takie jak zmiana haseł spowoduje unieważnienie wszystkich tokenów dostępu.  

Połączenia można wyświetlać i zarządzać na platformie Azure, klikając **Przeglądaj** i wybierając **połączenia interfejsu API**.  Z hello zasobów połączenia interfejsu API można wyświetlać, edytować, zaktualizować lub ponownie autoryzować połączeń, które zostały utworzone.

## <a name="next-steps"></a>Następne kroki
* [Tworzenie pierwszej aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md)
* [Dowiedz się wspólne używa i przykładowe aplikacje logiki](../logic-apps/logic-apps-examples-and-scenarios.md)
* [Rozpoczynanie pracy z enterprise integracji wyzwalacze i akcje](../logic-apps/logic-apps-enterprise-integration-overview.md)

<!--Image References -->
[1]: ./media/connectors-overview/addAction.png
[2]: ./media/connectors-overview/configureAction.png
