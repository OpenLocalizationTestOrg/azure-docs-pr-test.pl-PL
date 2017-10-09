---
title: wyzwalacz cyklu hello aaaAdd w aplikacji logiki | Dokumentacja firmy Microsoft
description: "Omówienie hello cyklu wyzwalacza i w jaki sposób toouse go z aplikacji logiki platformy Azure."
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
ms.openlocfilehash: e7c625c382a88a1e7cdfff4ddc0caf55727232bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-recurrence-trigger"></a>Rozpoczynanie pracy z wyzwalaczem cyklu hello
Za pomocą wyzwalacza cyklu hello, mogą tworzyć zaawansowane przepływy pracy w chmurze hello.

Można na przykład:

* Planowanie przepływu pracy toorun procedury składowane SQL każdego dnia.
* Wyślij wiadomość e-mail podsumowanie wszystkich tweetów w ciągu ostatniego tygodnia o niektórych hasztagiem hello.

tooget uruchomiony przy użyciu wyzwalacza cyklu hello w aplikacji logiki, zobacz [tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="use-a-recurrence-trigger"></a>Użyj wyzwalacz cyklu
Wyzwalacz jest zdarzenie, które mogą być używane toostart przepływu pracy hello zdefiniowanej w aplikacji logiki. [Dowiedz się więcej o wyzwalaczy](connectors-overview.md).

Oto przykład sekwencji jak tooset się cykl wyzwalacz w aplikacji logiki:

1. Dodaj hello **cyklu** jako hello pierwszym etapem aplikacji logiki.
2. Wprowadź parametry hello hello interwał cyklu.

Aplikacja logiki Hello uruchamia uruchamianie po każdym interwale czasu.

![Wyzwalacz HTTP](./media/connectors-native-recurrence/using-trigger.png)

## <a name="trigger-details"></a>Szczegóły wyzwalacza
wyzwalacz cyklu Hello ma następujące właściwości, które można skonfigurować hello.

Generowane aplikacji logiki, po upływie czasu określonego czasu.
A * oznacza, że jest polem wymaganym.

| Nazwa wyświetlana | Nazwa właściwości | Opis |
| --- | --- | --- |
| Częstotliwość * |frequency |Jednostka czasu Hello: `Second`, `Minute`, `Hour`, `Day`, lub `Year`. |
| Interwał * |interval |Interwał powitania hello podana częstotliwość cyklu hello. |
| Strefa czasowa |Strefa czasowa |Jeśli godzina rozpoczęcia jest dostarczany bez przesunięcie czasu UTC, będą używane tej strefy czasowej. |
| Godzina rozpoczęcia |startTime |Godzina rozpoczęcia Hello w [formacie ISO 8601](https://en.wikipedia.org/wiki/ISO_8601#Combined_date_and_time_representations). |

<br>

## <a name="next-steps"></a>Następne kroki
Teraz, wypróbuj hello platformy i [tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md). Można eksplorować hello innych dostępnych łączników w aplikacjach logiki analizując naszych [listy interfejsów API](apis-list.md).

