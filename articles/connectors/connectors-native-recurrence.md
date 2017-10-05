---
title: Dodaj wyzwalacza cyklu w aplikacjach logiki | Dokumentacja firmy Microsoft
description: "Przegląd cyklu wyzwalacza i jak z niego korzystać z aplikacji logiki platformy Azure."
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: 51dd4f22-7dc5-41af-a0a9-e7148378cd50
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: jehollan
ms.openlocfilehash: fe558958c316c8dba42163e277ae01451f712e5a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-recurrence-trigger"></a>Rozpoczynanie pracy z wyzwalaczem cyklu
Przy użyciu wyzwalacza cyklu, można tworzyć rozbudowane przepływy pracy w chmurze.

Można na przykład:

* Planowanie przepływu pracy do uruchomienia codziennie procedury składowane SQL.
* Wyślij wiadomość e-mail podsumowanie wszystkich tweetów w ostatnim tygodniu o niektórych hasztagiem.

Aby rozpocząć korzystanie z wyzwalacza cyklu w aplikacji logiki, zobacz [tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="use-a-recurrence-trigger"></a>Użyj wyzwalacz cyklu
Wyzwalacz to zdarzenie służy do uruchomienia przepływu pracy, który jest zdefiniowany w aplikacji logiki. [Dowiedz się więcej o wyzwalaczy](connectors-overview.md).

Oto przykład sekwencji sposobu konfigurowania wyzwalacz cyklu w aplikacji logiki:

1. Dodaj **cyklu** wyzwalacza jako pierwszy krok w aplikacji logiki.
2. Wprowadź interwał cyklu w parametrach.

Uruchomieniu aplikacji logiki teraz uruchamianie po każdym interwale czasu.

![Wyzwalacz HTTP](./media/connectors-native-recurrence/using-trigger.png)

## <a name="trigger-details"></a>Szczegóły wyzwalacza
Wyzwalacz cyklu ma następujące właściwości, które można skonfigurować.

Generowane aplikacji logiki, po upływie czasu określonego czasu.
A * oznacza, że jest polem wymaganym.

| Nazwa wyświetlana | Nazwa właściwości | Opis |
| --- | --- | --- |
| Częstotliwość * |częstotliwość |Jednostka czasu: `Second`, `Minute`, `Hour`, `Day`, lub `Year`. |
| Interwał * |Interwał |Interwał częstotliwości danego cyklu. |
| Strefa czasowa |Strefa czasowa |Jeśli godzina rozpoczęcia jest dostarczany bez przesunięcie czasu UTC, będą używane tej strefy czasowej. |
| Godzina rozpoczęcia |startTime |Czas rozpoczęcia w [formacie ISO 8601](https://en.wikipedia.org/wiki/ISO_8601#Combined_date_and_time_representations). |

<br>

## <a name="next-steps"></a>Następne kroki
Teraz, wypróbuj platformy i [tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md). Dostępne łączniki w aplikacjach logiki można eksplorować analizując naszych [listy interfejsów API](apis-list.md).

