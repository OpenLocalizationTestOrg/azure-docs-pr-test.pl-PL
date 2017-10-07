---
title: "aaaPricing & rozliczeń - Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak działa cennik i rozliczenia dla usługi Azure Logic Apps."
author: kevinlam1
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: f8f528f5-51c5-4006-b571-54ef74532f32
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: LADocs; klam
ms.openlocfilehash: fa10cbbf7657afba7fadb7c76817b7a5e4af7b42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="logic-apps-pricing-model"></a>Model cen aplikacji logiki
Aplikacje logiki platformy Azure pozwala tooscale i wykonaj integrację przepływów pracy w chmurze hello.  Poniżej przedstawiono szczegóły na powitania rozliczeń i planów cenowych dla usługi Logic Apps.
## <a name="consumption-pricing"></a>Cennik zużycie
Nowo utworzona Logic Apps użyć planu zużycia. Z aplikacji logiki hello zużycie modelu cenowego płacisz tylko za można użyć.  Aplikacje logiki nie są ograniczane, korzystając z planu zużycia.
Wszystkie akcje wykonywane podczas uruchomienia wystąpienia aplikacji logiki są naliczane.
### <a name="what-are-action-executions"></a>Co to są wykonania akcji?
Każdy krok w definicji aplikacji logiki jest akcji, która zawiera wyzwalacze, kroki przepływu sterowania, takie jak warunków, zakresów dla każdej pętli, czy do pętli, wywołuje akcje toonative tooconnectors i wywołania.
Wyzwalacze są specjalne akcji, które są zaprojektowane tooinstantiate nowe wystąpienie aplikacji logiki, po wystąpieniu określonego zdarzenia.  Istnieje kilka różnych zachowań wyzwalaczy, które mogą wpłynąć na sposób taryfowych hello aplikacji logiki.
* **Wyzwalacz sondowania** — tego wyzwalacza stale sonduje punkt końcowy, dopóki nie odbierze komunikatu, który spełnia kryteria hello tworzenia wystąpienia aplikacji logiki.  Interwał sondowania Hello można skonfigurować w hello wyzwalacza w hello projektanta aplikacji logiki.  Każde żądanie sondowania, nawet jeśli nie tworzy wystąpienie aplikacji logiki, traktowana jako wykonywania akcji.
* **Wyzwalacz Webhook** — tego wyzwalacza czeka na toosend klienta go żądania w określonym punkcie końcowym.  Każde żądanie wysłane punkt końcowy elementu webhook toohello traktowana jako wykonywania akcji. Witaj żądania i hello wyzwalacza HTTP elementu Webhook są zarówno wyzwalaczy elementu webhook.
* **Wyzwalacz cyklu** — tego wyzwalacza tworzy wystąpienie aplikacji logiki hello oparte na interwał cyklu hello skonfigurowane w hello wyzwalacza.  Na przykład wyzwalacz cyklu może być skonfigurowany toorun co trzy dni lub nawet co minutę.

Wyzwalacz wykonaniami są widoczne w bloku zasobów aplikacji logiki hello w hello części Historia wyzwalacza.

Wszystkie akcje, które zostały wykonane, czy zostały one powiodły się czy nie są mierzone jako wykonywania akcji.  Akcje, które zostały pominięte, ponieważ nie został spełniony warunek tooa lub akcje, które nie wykonać operacji, ponieważ aplikacja logiki hello przerwane przed ukończeniem, nie są liczone jako wykonania akcji.

Na iteracji pętli hello zliczane są działania wykonywane w pętli.  Na przykład jednej akcji w każdej pętli for iteracja listę pozycji 10 są liczone jako hello liczba elementów na liście hello (10) pomnożona przez hello liczbę akcji w pętli hello (1) plus jeden rozpoczęcia hello hello pętli , które w tym przykładzie będzie (10 * 1) + 1 = 11 wykonania akcji.
Wyłączone Logic Apps nie może mieć nowych wystąpień utworzonych i w związku z tym podczas wyłączony, nie pobiera.  Należy zachować ostrożność, po wyłączeniu aplikacji logiki może zająć nieco czasu dla tooquiesce wystąpień hello przed całkowicie wyłączana.
### <a name="integration-account-usage"></a>Użycie konta integracji
Uwzględnione w podstawie zużycia użycia jest [konta integracji](logic-apps-enterprise-integration-create-integration-account.md) do badań, projektowania i testowania, dzięki czemu toouse hello [B2B/EDI](logic-apps-enterprise-integration-b2b.md) i [przetwarzania XML](logic-apps-enterprise-integration-xml.md)funkcji Logic Apps bez ponoszenia dodatkowych kosztów. Są możliwe toocreate maksymalnie jednego konta dla regionu i przechowywać too10 umowy i 25 mapy. Schematy, certyfikaty i partnerów mają Brak ograniczeń i możesz przekazać tyle, zgodnie z potrzebami.

Oprócz włączenia toohello kont integracji z użycia, można również utworzyć konta standardowe integracji bez tych ograniczeń i z naszego standardowego SLA aplikacji logiki. Aby uzyskać więcej informacji, zobacz [cennik platformy Azure](https://azure.microsoft.com/pricing/details/logic-apps).

## <a name="app-service-plans"></a>Plany usługi App Service
Aplikacje logiki wcześniej utworzony odwołujące się do planu usługi App Service jest nadal toobehave jako przed. W zależności od wybranego planu hello są ograniczane po hello wyznaczonych wykonaniami codzienne przekroczona, ale są rozliczane za pomocą licznika wykonywania akcji hello.
EA używających planu usługi App Service w ich subskrypcję, która nie ma toobe jawnie skojarzone z hello aplikacji logiki, uzyskać korzyści ilości hello uwzględnione.  Na przykład jeśli standardowy Plan usługi App Service w subskrypcji EA i aplikacji logiki w tej samej subskrypcji hello, a następnie nie są pobierane za 10 000 wykonania akcji na dzień (patrz tabela poniżej). 

Plany usługi App Service i ich codzienne wykonaniami dozwolonych akcji:
|  | Zwolnij/udostępnione/Basic | Standardowa | Premium |
| --- | --- | --- | --- |
| Wykonania akcji na dzień |200 |10 000 |50,000 |
### <a name="convert-from-app-service-plan-pricing-tooconsumption"></a>Konwertowanie z cennik tooConsumption Plan usługi aplikacji
toochange aplikację logiki, która ma Plan usługi aplikacji skojarzonych z nim tooa zużycie modelu, Usuń hello odwołanie toohello planu usługi App Service w hello definicję aplikacji logiki.  Ta zmiana może odbywać się za pomocą polecenia cmdlet programu PowerShell tooa wywołania:`Set-AzureRmLogicApp -ResourceGroupName ‘rgname’ -Name ‘wfname’ –UseConsumptionModel -Force`
## <a name="pricing"></a>Cennik
Aby uzyskać szczegółowe informacje o cenach, zobacz [cennik aplikacje logiki](https://azure.microsoft.com/pricing/details/logic-apps).

## <a name="next-steps"></a>Następne kroki
* [Omówienie usługi Logic Apps][whatis]
* [Tworzenie pierwszej aplikacji logiki][create]

[pricing]: https://azure.microsoft.com/pricing/details/logic-apps/
[whatis]: logic-apps-what-are-logic-apps.md
[create]: logic-apps-create-a-logic-app.md

