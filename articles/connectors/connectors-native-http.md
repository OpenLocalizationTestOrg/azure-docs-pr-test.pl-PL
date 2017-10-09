---
title: "aaaCommunicate z dowolnego punktu końcowego za pośrednictwem protokołu HTTP - Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Tworzenie aplikacji logiki, które mogą się komunikować z dowolnego punktu końcowego za pośrednictwem protokołu HTTP"
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
tags: connectors
ms.assetid: e11c6b4d-65a5-4d2d-8e13-38150db09c0b
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/15/2016
ms.author: jehollan; LADocs
ms.openlocfilehash: 9793601839437a2b880bdb81e15881270cacc963
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-http-action"></a>Rozpoczynanie pracy z hello akcji HTTP

Hello akcji HTTP możesz rozszerzyć przepływy pracy dla Twojej organizacji i komunikacji tooany punktu końcowego za pośrednictwem protokołu HTTP.

Możesz:

* Tworzenie przepływów pracy aplikacji, które aktywować (wyzwalacz) witryny sieci Web, którą zarządzasz systemowi logiki.
* Komunikacji tooany punktu końcowego za pośrednictwem protokołu HTTP tooextend przepływy pracy do innych usług.

tooget uruchomiony przy użyciu akcji hello HTTP w aplikacji logiki, zobacz [tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="use-hello-http-trigger"></a>Użyj wyzwalacza hello HTTP
Wyzwalacz jest zdarzenie, które mogą być używane toostart przepływu pracy hello zdefiniowanej w aplikacji logiki. [Dowiedz się więcej o wyzwalaczy](connectors-overview.md).

Oto przykład sekwencji jak tooset się hello HTTP wyzwalacz w hello projektanta aplikacji logiki.

1. Dodaj hello wyzwalacza HTTP w aplikacji logiki.
2. Wypełnij hello parametry dla punktu końcowego hello HTTP, które mają toopoll.
3. Zmodyfikuj interwał cyklu hello na częstotliwości powinna sondowania.

   Aplikacja logiki Hello teraz generowane z zawartość, która jest zwracana podczas każdego wyboru.

   ![Wyzwalacz HTTP](./media/connectors-native-http/using-trigger.png)

### <a name="how-hello-http-trigger-works"></a>Jak działa hello wyzwalacza HTTP

wyzwalacza HTTP Hello wysyła punktu końcowego tooHTTP wywołania interwału powtarzania. Domyślnie kodu odpowiedzi HTTP, który jest niższa niż 300 powoduje, że toorun aplikacji logiki. toospecify czy aplikacji logiki hello powinny wyzwalać, można edytować hello aplikacji logiki w widoku kodu i dodać warunek oceniający po hello wywołanie HTTP. Oto przykład wyzwalacza HTTP, który generowane, gdy hello zwrócił kod stanu jest większa lub równa zbyt`400`.

```javascript
"Http":
{
    "conditions": [
        {
            "expression": "@greaterOrEquals(triggerOutputs()['statusCode'], 400)"
        }
    ],
    "inputs": {
        "method": "GET",
        "uri": "https://blogs.msdn.microsoft.com/logicapps/",
        "headers": {
            "accept-language": "en"
        }
    },
    "recurrence": {
        "frequency": "Second",
        "interval": 15
    },
    "type": "Http"
}
```

Szczegółowe informacje o parametrach wyzwalacza hello HTTP są dostępne na [MSDN](https://msdn.microsoft.com/library/azure/mt643939.aspx#HTTP-trigger).

## <a name="use-hello-http-action"></a>Za pomocą akcji hello HTTP

Akcja jest operacja odbywa się przez hello przepływ pracy, który jest zdefiniowany w aplikacji logiki. 
[Dowiedz się więcej o akcjach](connectors-overview.md).

1. Wybierz **nowy krok** > **Dodaj akcję**.
3. W polu wyszukiwania akcji hello wpisz **http** toolist hello HTTP akcji.
   
    ![Wybierz akcję hello HTTP](./media/connectors-native-http/using-action-1.png)

4. Dodaj wszelkie wymagane parametry dla wywołania hello HTTP.
   
    ![Witaj pełną Akcja HTTP](./media/connectors-native-http/using-action-2.png)

5. Na pasku narzędzi Projektanta hello, kliknij przycisk **zapisać**. Aplikację logiki zostaną zapisane i opublikowane (aktywowanego) na powitania tym samym czasie.

## <a name="http-trigger"></a>Wyzwalacz HTTP
Poniżej przedstawiono szczegóły hello hello wyzwalacz, który obsługuje ten łącznik. Łącznik HTTP Hello ma jeden wyzwalacz.

| Wyzwalacz | Opis |
| --- | --- |
| HTTP |Wykonuje wywołanie HTTP i zwraca hello zawartości odpowiedzi. |

## <a name="http-action"></a>Akcja HTTP
Poniżej przedstawiono szczegóły hello hello akcję, która obsługuje ten łącznik. Łącznik HTTP Hello ma jedną akcję możliwe.

| Akcja | Opis |
| --- | --- |
| HTTP |Wykonuje wywołanie HTTP i zwraca hello zawartości odpowiedzi. |

## <a name="http-details"></a>Szczegóły HTTP
Witaj poniższych tabelach opisano hello wymagane i opcjonalne pola wejściowego dla akcji hello i hello odpowiednie dane wyjściowe szczegóły, które są skojarzone z przy użyciu akcji hello.

#### <a name="http-request"></a>Żądania HTTP
Oto Hello pól wejściowych dla akcji hello, dzięki czemu żądania wychodzącego HTTP.
A * oznacza, że jest polem wymaganym.

| Nazwa wyświetlana | Nazwa właściwości | Opis |
| --- | --- | --- |
| Metoda * |— Metoda |toouse zlecenie Hello HTTP |
| IDENTYFIKATOR URI * |Identyfikator URI |Witaj identyfikatora URI dla żądania hello HTTP |
| Nagłówki |Nagłówki |Obiekt JSON tooinclude nagłówki HTTP |
| Treść |Treści |Witaj treści żądania HTTP |
| Authentication |Uwierzytelnianie |Szczegóły w hello [uwierzytelniania](#authentication) sekcji |

<br>

#### <a name="output-details"></a>Szczegóły danych wyjściowych
Witaj poniżej przedstawiono szczegóły danych wyjściowych dla hello odpowiedzi HTTP.

| Nazwa właściwości | Typ danych | Opis |
| --- | --- | --- |
| Nagłówki |Obiekt |Nagłówki odpowiedzi |
| Treść |Obiekt |Obiekt odpowiedzi |
| Kod stanu |int |Kod stanu HTTP |

## <a name="authentication"></a>Authentication
Funkcja Logic Apps Hello pozwala toouse różnych typów uwierzytelniania względem punktów końcowych HTTP. Za pomocą tego uwierzytelnienia hello **HTTP**,  **[HTTP + Swagger](connectors-native-http-swagger.md)**, i  **[HTTP elementu Webhook](connectors-native-webhook.md)**  łączniki. następujące typy uwierzytelniania Hello są konfigurowane:

* [Uwierzytelnianie podstawowe](#basic-authentication)
* [Uwierzytelnianie certyfikatu klienta](#client-certificate-authentication)
* [Azure uwierzytelniania OAuth usługi Active Directory (Azure AD)](#azure-active-directory-oauth-authentication)

#### <a name="basic-authentication"></a>Uwierzytelnianie podstawowe

powitania po obiekt uwierzytelniania jest wymagany dla uwierzytelniania podstawowego.
A * oznacza, że jest polem wymaganym.

| Nazwa właściwości | Typ danych | Opis |
| --- | --- | --- |
| Typ * |type |Typ uwierzytelniania (musi być `Basic` dla uwierzytelniania podstawowego) |
| Nazwa użytkownika * |nazwa użytkownika |Tooauthenticate nazwy użytkownika |
| Hasło * |hasło |Tooauthenticate hasła |

> [!TIP]
> Toouse hasła, gdy nie można pobrać z definicji hello, należy użyć `securestring` parametr i hello `@parameters()`  
>  [funkcji definicji przepływu pracy](http://aka.ms/logicappdocs).

Na przykład:

```javascript
{
    "type": "Basic",
    "username": "user",
    "password": "test"
}
```

#### <a name="client-certificate-authentication"></a>Uwierzytelnianie certyfikatów klientów

Witaj następujący obiekt uwierzytelniania jest potrzebne uwierzytelnianie certyfikatu klienta. A * oznacza, że jest polem wymaganym.

| Nazwa właściwości | Typ danych | Opis |
| --- | --- | --- |
| Typ * |type |Witaj typ uwierzytelniania (musi być `ClientCertificate` dla certyfikatów klienta SSL) |
| PFX * |PFX |Witaj algorytmem Base64 zawartość pliku wymiany informacji osobistych (PFX) hello |
| Hasło * |hasło |tooaccess hasło Hello hello pliku PFX |

> [!TIP]
> toouse parametr, który nie będzie można odczytać w definicji powitania po zapisaniu hello logikę aplikacji, można użyć `securestring` parametr i hello `@parameters()`  
>  [funkcji definicji przepływu pracy](http://aka.ms/logicappdocs).

Na przykład:

```javascript
{
    "type": "ClientCertificate",
    "pfx": "aGVsbG8g...d29ybGQ=",
    "password": "@parameters('myPassword')"
}
```

#### <a name="azure-ad-oauth-authentication"></a>Azure uwierzytelniania AD OAuth
powitania po obiekt uwierzytelniania jest wymagany dla uwierzytelniania usługi Azure AD OAuth. A * oznacza, że jest polem wymaganym.

| Nazwa właściwości | Typ danych | Opis |
| --- | --- | --- |
| Typ * |type |Witaj typ uwierzytelniania (musi być `ActiveDirectoryOAuth` dla usługi Azure AD OAuth) |
| Dzierżawy * |Dzierżawy |Identyfikator dzierżawy Hello dzierżawy hello Azure AD |
| Grupy odbiorców * |grupy odbiorców |zasób Hello żądają toouse autoryzacji. Na przykład: `https://management.core.windows.net/` |
| Klient identyfikator * |clientId |Witaj identyfikator klienta aplikacji hello Azure AD |
| Klucz tajny * |klucz tajny |klucz tajny Hello powitania klienta, który żąda hello tokenu |

> [!TIP]
> Można użyć `securestring` parametr i hello `@parameters()` [funkcji definicji przepływu pracy](http://aka.ms/logicappdocs) toouse parametr, który nie będzie można odczytać w definicji powitania po zapisaniu.
> 
> 

Na przykład:

```javascript
{
    "type": "ActiveDirectoryOAuth",
    "tenant": "72f988bf-86f1-41af-91ab-2d7cd011db47",
    "audience": "https://management.core.windows.net/",
    "clientId": "34750e0b-72d1-4e4f-bbbe-664f6d04d411",
    "secret": "hcqgkYc9ebgNLA5c+GDg7xl9ZJMD88TmTJiJBgZ8dFo="
}
```

## <a name="next-steps"></a>Następne kroki
Teraz, wypróbuj hello platformy i [tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md). Można eksplorować hello innych dostępnych łączników w aplikacjach logiki analizując naszych [listy interfejsów API](apis-list.md).

