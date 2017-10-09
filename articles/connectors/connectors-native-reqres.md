---
title: "Akcje żądań i odpowiedzi aaaUse | Dokumentacja firmy Microsoft"
description: "Omówienie hello żądań i odpowiedzi trigger i action w aplikacji logiki platformy Azure"
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: 566924a4-0988-4d86-9ecd-ad22507858c0
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: jehollan
ms.openlocfilehash: 24c378cc12d5f3f65116d5e59278236186a99662
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-request-and-response-components"></a>Rozpoczęcie pracy ze składnikami hello żądań i odpowiedzi
Składnikom hello żądań i odpowiedzi w aplikacji logiki może odpowiedzieć w czasie rzeczywistym tooevents.

Można na przykład:

* Odpowiedz tooan żądania HTTP z danymi z lokalną bazą danych za pośrednictwem aplikacji logiki.
* Uruchomienie aplikacji logiki z zdarzenie zewnętrznego elementu webhook.
* Wywołania z akcją żądań i odpowiedzi z poziomu innej aplikacji logiki aplikacji logiki.

tooget uruchomiony przy użyciu akcji hello żądań i odpowiedzi w aplikacji logiki, zobacz [tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="use-hello-http-request-trigger"></a>Użyj hello wyzwalacza żądania HTTP
Wyzwalacz jest zdarzenie, które mogą być używane toostart przepływu pracy hello zdefiniowanej w aplikacji logiki. [Dowiedz się więcej o wyzwalaczy](connectors-overview.md).

Oto przykład sekwencji jak tooset się HTTP żądania w hello projektanta aplikacji logiki.

1. Dodaj wyzwalacza hello **żądania - zostanie odebrane żądanie HTTP podczas** w aplikacji logiki. Opcjonalnie można podać schematu JSON (przy użyciu narzędzia, takiego jak [JSONSchema.net](http://jsonschema.net)) dla hello treści żądania. Dzięki temu hello projektanta toogenerate tokeny dla właściwości w żądaniu hello HTTP.
2. Dodaj inną akcję, dzięki czemu można zapisać hello aplikacji logiki.
3. Po zapisaniu hello aplikacji logiki, może uzyskać adres URL żądania hello HTTP z hello żądania karty.
4. HTTP POST (można użyć narzędzia, takiego jak [Postman](https://www.getpostman.com/)) toohello adres URL wyzwalaczy hello aplikacji logiki.

> [!NOTE]
> Jeśli nie zdefiniowano akcję odpowiedzi `202 ACCEPTED` odpowiedzi jest zwracany natychmiast toohello wywołującego. Możesz użyć toocustomize akcji odpowiedzi hello odpowiedzi.
> 
> 

![Wyzwalacz odpowiedzi](./media/connectors-native-reqres/using-trigger.png)

## <a name="use-hello-http-response-action"></a>Użyj hello akcji odpowiedzi HTTP
Hello akcji odpowiedzi HTTP jest prawidłowa tylko w przypadku, gdy jest używany w przepływie pracy, który jest wyzwalana przez żądanie HTTP. Jeśli nie zdefiniowano akcję odpowiedzi `202 ACCEPTED` odpowiedzi jest zwracany natychmiast toohello wywołującego.  Można dodać akcję odpowiedzi na dowolnym etapie w przepływie pracy hello. aplikacji logiki Hello przechowuje tylko przychodzące żądanie hello otwarte przez jedną minutę na odpowiedź.  Po minucie, jeśli odpowiedź nie została wysłana z hello przepływu pracy (i istnieje akcja odpowiedzi w definicji hello) `504 GATEWAY TIMEOUT` jest zwracany toohello wywołującego.

Oto jak tooadd akcji odpowiedzi HTTP:

1. Wybierz hello **nowy krok** przycisku.
2. Wybierz **Dodaj akcję**.
3. W polu wyszukiwania akcji hello wpisz **odpowiedzi** hello toolist akcji odpowiedzi.
   
    ![Wybierz akcję odpowiedzi hello](./media/connectors-native-reqres/using-action-1.png)
4. Dodaj w żadnych parametrów, które są wymagane dla komunikatu odpowiedzi HTTP hello.
   
    ![Zakończenie hello akcji odpowiedzi](./media/connectors-native-reqres/using-action-2.png)
5. Kliknij przycisk hello lewego górnego rogu hello toosave narzędzi i Twoje logiki aplikacji zapisze zarówno i publikowanie (Aktywuj).

## <a name="request-trigger"></a>Wyzwalacz żądania
Poniżej przedstawiono szczegóły hello hello wyzwalacz, który obsługuje ten łącznik. Brak wyzwalacz pojedyncze żądanie.

| Wyzwalacz | Opis |
| --- | --- |
| Żądanie |Występuje, gdy zostanie odebrane żądanie HTTP |

## <a name="response-action"></a>Akcja odpowiedzi
Poniżej przedstawiono szczegóły hello hello akcję, która obsługuje ten łącznik. Brak akcji pojedynczą odpowiedź, który można użyć tylko, gdy towarzyszy wyzwalacz żądania.

| Akcja | Opis |
| --- | --- |
| Odpowiedź |Zwraca toohello odpowiedzi skorelowane żądanie HTTP |

### <a name="trigger-and-action-details"></a>Szczegóły TRIGGER i action
Hello poniższych tabelach opisano hello pól wejściowych dla hello trigger i action i hello szczegóły danych wyjściowych.

#### <a name="request-trigger"></a>Wyzwalacz żądania
Witaj poniżej znajduje się pole wejściowe dla wyzwalacza hello z przychodzącego żądania HTTP.

| Nazwa wyświetlana | Nazwa właściwości | Opis |
| --- | --- | --- |
| Schematu JSON |Schemat |Witaj schematu JSON w treści żądania HTTP hello |

<br>

**Szczegóły danych wyjściowych**

Witaj poniżej przedstawiono szczegóły danych wyjściowych hello żądania.

| Nazwa właściwości | Typ danych | Opis |
| --- | --- | --- |
| Nagłówki |Obiekt |Nagłówki żądania |
| Treść |Obiekt |Obiekt żądania |

#### <a name="response-action"></a>Akcja odpowiedzi
Oto Hello pól wejściowych dla hello akcji odpowiedzi HTTP. A * oznacza, że jest polem wymaganym.

| Nazwa wyświetlana | Nazwa właściwości | Opis |
| --- | --- | --- |
| Kod stanu * |statusCode |Witaj kod stanu HTTP |
| Nagłówki |Nagłówki |Obiekt JSON w dowolnym tooinclude nagłówki odpowiedzi |
| Treść |Treści |treść odpowiedzi Hello |

## <a name="next-steps"></a>Następne kroki
Teraz, wypróbuj hello platformy i [tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md). Można eksplorować hello innych dostępnych łączników w aplikacjach logiki analizując naszych [listy interfejsów API](apis-list.md).

