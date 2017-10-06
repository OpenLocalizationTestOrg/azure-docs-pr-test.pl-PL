---
title: "Łącznik aaaWebhook dla usługi Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Jak akcje elementu webhook toouse i wyzwalaczy tooperform akcje, takie jak tablicy filtrów z aplikacji logiki"
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
tags: connectors
ms.assetid: 71775384-6c3a-482c-a484-6624cbe4fcc7
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/21/2016
ms.author: jehollan; LADocs
ms.openlocfilehash: b2dee12750f3f20f10e7b257da05a79f28f90f43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-webhook-connector"></a>Rozpoczynanie pracy z hello łącznika elementu webhook

O działaniu elementu webhook hello i wyzwalacza można uruchomić, wstrzymywać i wznawiać przepływy tooperform te zadania:

* Wyzwalanie z [Azure Event Hub](https://github.com/logicappsio/EventHubAPI) po odebraniu elementu
* Oczekiwanie na zatwierdzenie przed kontynuowaniem przepływu pracy

Dowiedz się więcej o [jak toocreate niestandardowych interfejsów API, który obsługuje elementu webhook](../logic-apps/logic-apps-create-api-app.md).

## <a name="use-hello-webhook-trigger"></a>Użyj hello wyzwalacza elementu webhook

A [ *wyzwalacza* ](connectors-overview.md) jest zdarzeniem, która uruchamia przepływ pracy aplikacji logiki. Wyzwalacz elementu webhook jest oparty na zdarzeniach i nie zależą od sondowania dla nowych elementów. Podobnie jak hello [wyzwalacza żądania](connectors-native-reqres.md), aplikację logiki hello generowane hello błyskawiczne, że zdarzenie. rejestruje wyzwalacza elementu webhook Hello *wywołania zwrotnego adresu URL* tooa usługi i używa tego adresu URL toofire hello logiki aplikacji jako wymagane.

Oto przykład pokazujący, jak tooset się HTTP wyzwalacz w hello projektanta aplikacji logiki. Witaj krokach założono została już wdrożona, lub uzyskują dostęp do interfejsu API, który wykonuje hello [webhook subskrybowanie i anulowanie subskrypcji wzorca w aplikacjach logiki](../logic-apps/logic-apps-create-api-app.md#webhook-triggers). Witaj subskrybowania wywołań ma zostać zapisane przy użyciu nowego elementu webhook aplikacji logiki lub przełączono z tooenabled wyłączone. Wywołanie subskrypcję Hello są wysyłane w przypadku elementu webhook aplikacji logiki wyzwalacza jest usunięte i zapisać lub przełączono z toodisabled włączone.

**wyzwalacz webhook hello tooadd**

1. Dodaj hello **HTTP elementu Webhook** jako hello pierwszym etapem aplikacji logiki.
2. Wypełnij hello parametrów dla elementu webhook hello subskrybowanie i anulowanie subskrypcji wywołania.

   W tym kroku następuje hello sam wzorca jako hello [akcji HTTP](connectors-native-http.md) format.

     ![Wyzwalacz protokołu HTTP](./media/connectors-native-webhook/using-trigger.png)

3. Dodaj co najmniej jedną akcję.
4. Kliknij przycisk **zapisać** toopublish hello logiki aplikacji. Ten krok hello wywołania subskrypcji punkt końcowy z hello wywołania zwrotnego adresu URL potrzebne tootrigger tej aplikacji logiki.
5. Po każdej zmianie hello sprawia, że usługa `HTTP POST` toohello wywołania zwrotnego adresu URL, hello uruchamiany aplikacji logiki i zawiera wszystkie dane przekazywane do hello żądania.

## <a name="use-hello-webhook-action"></a>Użyj hello akcji elementu webhook

[ *Akcji* ](connectors-overview.md) operacji odbywa się przez przepływ pracy hello zdefiniowanych w aplikacji logiki. Rejestruje działania elementu webhook *wywołania zwrotnego adresu URL* z usługą i czeka, aż hello adres URL jest wywoływana przed wznowieniem. Witaj ["Wyślij E-mail zatwierdzenia"](connectors-create-api-office365-outlook.md) przykładem łącznik, który wykonuje tego wzorca. Ten wzorzec można rozszerzyć do dowolnej usługi za pomocą akcji elementu webhook hello. 

Oto przykład pokazujący sposób tooset działaniami elementu webhook w hello projektanta aplikacji logiki. Tych krokach przyjęto założenie, zostały już wdrożone, lub uzyskują dostęp do interfejsu API, który wykonuje hello [webhook subskrybowanie i anulowanie subskrypcji wzorzec używany w aplikacjach logiki](../logic-apps/logic-apps-create-api-app.md#webhook-actions). Witaj subskrybowania wywołań są wysyłane w przypadku aplikacji logiki wykonuje akcję elementu webhook hello. Wywołanie subskrypcję Hello są wysyłane w przypadku Uruchom zostało anulowane podczas oczekiwania na odpowiedź lub przed hello logiki aplikacji upłynie limit czasu.

**tooadd akcji elementu webhook**

1. Wybierz **nowy krok** > **Dodaj akcję**.

2. W polu wyszukiwania hello wpisz "elementu webhook" hello toofind **HTTP elementu Webhook** akcji.

    ![Wybierz akcję zapytania](./media/connectors-native-webhook/using-action-1.png)

3. Wypełnij hello parametrów dla elementu webhook hello subskrybowanie i anulowanie subskrypcji wywołania

   W tym kroku następuje hello sam wzorca jako hello [akcji HTTP](connectors-native-http.md) format.

     ![Akcja pełnej kwerendy](./media/connectors-native-webhook/using-action-2.png)
   
   W czasie wykonywania hello logiki aplikacji wywołania hello subskrypcji punktu końcowego po osiągnięciu tego kroku.

4. Kliknij przycisk **zapisać** toopublish hello logiki aplikacji.

## <a name="technical-details"></a>Szczegóły techniczne

Poniżej przedstawiono więcej informacji o hello wyzwalacze i akcje obsługuje tego elementu webhook.

## <a name="webhook-triggers"></a>Wyzwalacze elementu Webhook

| Akcja | Opis |
| --- | --- |
| HTTP elementu Webhook |Subskrypcja usługi tooa adresów URL wywołania zwrotnego, który można wywołać hello adresu URL toofire logiki aplikacji zgodnie z potrzebami. |

### <a name="trigger-details"></a>Szczegóły wyzwalacza

#### <a name="http-webhook"></a>HTTP elementu Webhook

Subskrypcja usługi tooa adresów URL wywołania zwrotnego, który można wywołać hello adresu URL toofire logiki aplikacji zgodnie z potrzebami.
* Oznacza, że wymagane pole.

| Nazwa wyświetlana | Nazwa właściwości | Opis |
| --- | --- | --- |
| Subskrypcja — metoda * |— Metoda |Metoda HTTP toouse Subskrybuj żądania |
| Subskrypcja URI * |Identyfikator URI |Toouse identyfikator URI protokołu HTTP dla żądania Subskrybuj |
| Anulowanie subskrypcji metody * |— Metoda |Toouse — metoda HTTP dla żądania anulowania |
| Anulowanie subskrypcji URI * |Identyfikator URI |Toouse identyfikator URI protokołu HTTP dla żądania anulowania |
| Subskrypcja treści |Treści |Żądania HTTP do subskrybowania |
| Subskrypcja nagłówki |Nagłówki |Nagłówki żądania HTTP do subskrybowania |
| Subskrypcja uwierzytelniania |Uwierzytelnianie |Toouse uwierzytelniania HTTP do subskrybowania. [Zobacz łącznika HTTP](connectors-native-http.md#authentication) Aby uzyskać więcej informacji |
| Anulowanie subskrypcji treści |Treści |Żądania HTTP do anulowania subskrypcji |
| Anulowanie subskrypcji nagłówki |Nagłówki |Nagłówki żądania HTTP do anulowania subskrypcji |
| Anulowanie subskrypcji uwierzytelniania |Uwierzytelnianie |Toouse uwierzytelniania HTTP do anulowania subskrypcji. [Zobacz łącznika HTTP](connectors-native-http.md#authentication) Aby uzyskać więcej informacji |

**Szczegóły danych wyjściowych**

Żądania elementu Webhook

| Nazwa właściwości | Typ danych | Opis |
| --- | --- | --- |
| Nagłówki |Obiekt |Nagłówki żądania elementu Webhook |
| Treść |Obiekt |Obiekt żądania elementu Webhook |
| Kod stanu |int |Kod stanu żądania elementu Webhook |

## <a name="webhook-actions"></a>Akcje elementu Webhook

| Akcja | Opis |
| --- | --- |
| HTTP elementu Webhook |Subskrypcja usługi tooa adresów URL wywołania zwrotnego, który można wywołać tooresume adres URL hello krok przepływu pracy, zgodnie z potrzebami. |

### <a name="action-details"></a>Szczegóły akcji

#### <a name="http-webhook"></a>HTTP elementu Webhook

Subskrypcja usługi tooa adresów URL wywołania zwrotnego, który można wywołać tooresume adres URL hello krok przepływu pracy, zgodnie z potrzebami.
* Oznacza, że wymagane pole.

| Nazwa wyświetlana | Nazwa właściwości | Opis |
| --- | --- | --- |
| Subskrypcja — metoda * |— Metoda |Metoda HTTP toouse Subskrybuj żądania |
| Subskrypcja URI * |Identyfikator URI |Toouse identyfikator URI protokołu HTTP dla żądania Subskrybuj |
| Anulowanie subskrypcji metody * |— Metoda |Toouse — metoda HTTP dla żądania anulowania |
| Anulowanie subskrypcji URI * |Identyfikator URI |Toouse identyfikator URI protokołu HTTP dla żądania anulowania |
| Subskrypcja treści |Treści |Żądania HTTP do subskrybowania |
| Subskrypcja nagłówki |Nagłówki |Nagłówki żądania HTTP do subskrybowania |
| Subskrypcja uwierzytelniania |Uwierzytelnianie |Toouse uwierzytelniania HTTP do subskrybowania. [Zobacz łącznika HTTP](connectors-native-http.md#authentication) Aby uzyskać więcej informacji |
| Anulowanie subskrypcji treści |Treści |Żądania HTTP do anulowania subskrypcji |
| Anulowanie subskrypcji nagłówki |Nagłówki |Nagłówki żądania HTTP do anulowania subskrypcji |
| Anulowanie subskrypcji uwierzytelniania |Uwierzytelnianie |Toouse uwierzytelniania HTTP do anulowania subskrypcji. [Zobacz łącznika HTTP](connectors-native-http.md#authentication) Aby uzyskać więcej informacji |

**Szczegóły danych wyjściowych**

Żądania elementu Webhook

| Nazwa właściwości | Typ danych | Opis |
| --- | --- | --- |
| Nagłówki |Obiekt |Nagłówki żądania elementu Webhook |
| Treść |Obiekt |Obiekt żądania elementu Webhook |
| Kod stanu |int |Kod stanu żądania elementu Webhook |

## <a name="next-steps"></a>Następne kroki

* [Tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md)
* [Znajdź inne łączniki](apis-list.md)