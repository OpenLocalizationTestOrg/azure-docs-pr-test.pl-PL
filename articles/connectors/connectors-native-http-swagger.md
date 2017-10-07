---
title: "punkty końcowe REST aaaCall z HTTP + Swagger connector dla usługi Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Połącz tooREST punktów końcowych z aplikacji logiki za pośrednictwem programu Swagger z hello HTTP + łącznika programu Swagger"
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
tags: connectors
ms.assetid: eccfd87c-c5fe-4cf7-b564-9752775fd667
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: jehollan; LADocs
ms.openlocfilehash: baaa57689ff41fcd052f9d86086e36619ddec46e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-http--swagger-action"></a>Rozpoczynanie pracy z Witaj HTTP + akcji struktury Swagger

Można utworzyć punkt końcowy REST tooany łącznika najwyższej jakości za pomocą [dokumentu Swagger](https://swagger.io) korzystając Witaj HTTP + Swagger działania w przepływie pracy aplikacji logiki. Toocall aplikacje logiki można rozszerzać dowolnego punktu końcowego REST o najwyższej jakości środowisko projektanta aplikacji logiki.

aplikacje logiki toocreate z łączników, zobacz temat toolearn [Utwórz nową aplikację logiki](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="use-http--swagger-as-a-trigger-or-an-action"></a>Użyj protokołu HTTP + Swagger jako wyzwalacz lub akcji

Witaj HTTP + Swagger trigger i action pracy hello takie same jak hello [akcji HTTP](connectors-native-http.md) choć zapewnia lepsze środowisko pracy w Projektancie aplikacji logiki w przypadku wystawianego hello interfejsu API struktury i dane wyjściowe z hello [Swagger metadanych](https://swagger.io) . Witaj HTTP + łącznika struktury Swagger można również używane jako wyzwalacz. Tooimplement wyzwalacz sondowania, należy wykonać sondowanie hello wzorzec, który jest opisany w [Tworzenie niestandardowych interfejsów API toocall innych interfejsów API, usług i systemy z aplikacji logiki](../logic-apps/logic-apps-create-api-app.md#polling-triggers).

Dowiedz się więcej o [logiki aplikacji wyzwalacze i akcje](connectors-overview.md).

Poniżej przedstawiono przykład sposobu toouse hello HTTP + Swagger operacji jako akcja w przepływie pracy w aplikacji logiki.

1. Wybierz hello **nowy krok** przycisku.
2. Wybierz **Dodaj akcję**.
3. W hello akcji wyszukiwania wpisz **swagger** toolist Witaj HTTP + akcji struktury Swagger.
   
    ![Wybierz opcję HTTP + Swagger akcji](./media/connectors-native-http-swagger/using-action-1.png)
4. Wpisz adres URL dokumentu Swagger hello:
   
   * toowork z hello projektanta aplikacji logiki, hello adres URL musi być punkt końcowy HTTPS i włączono CORS.
   * Jeśli dokumentu Swagger hello nie spełnia tego wymagania, możesz użyć [magazynu Azure z włączonym mechanizmem CORS](#hosting-swagger-from-storage) toostore hello dokumentu.
5. Kliknij przycisk **dalej** tooread i renderowania z hello dokumentu Swagger.
6. Dodaj w żadnych parametrów, które są wymagane dla wywołania hello HTTP.
   
    ![Zakończenie akcji HTTP](./media/connectors-native-http-swagger/using-action-2.png)
7. toosave i publikowanie aplikacji logiki, kliknij przycisk **zapisać** na pasku narzędzi projektanta.

### <a name="host-swagger-from-azure-storage"></a>Swagger hosta z usługi Azure Storage
Możesz tooreference dokumentu Swagger nie jest obsługiwany lub który nie spełnia wymagania zabezpieczeń i cross-origin hello hello projektanta. tooresolve ten problem, można przechowywać dokumentu Swagger hello w usłudze Azure Storage i Włącz dokument hello tooreference CORS.  

Poniżej przedstawiono toocreate kroki hello, konfigurowanie i przechowywanie dokumentów struktury Swagger w usłudze Azure Storage:

1. [Utwórz konto magazynu platformy Azure z magazynu obiektów Blob Azure](../storage/common/storage-create-storage-account.md). tooperform ten krok, ustawianie uprawnień zbyt**dostępu publicznego**.

2. Włącz CORS na powitania obiektu blob. 

   tooautomatically tego ustawienia, można użyć [ten skrypt programu PowerShell](https://github.com/logicappsio/EnableCORSAzureBlob/blob/master/EnableCORSAzureBlob.ps1).

3. Przekaż hello Swagger pliku toohello blob. 

   Ten krok można wykonać z hello [portalu Azure](https://portal.azure.com) lub z narzędzia, takiego jak [Eksploratora usługi Storage Azure](http://storageexplorer.com/).

4. Odwołuje się do dokumentu toohello łącza HTTPS w magazynie obiektów Blob Azure. 

   łącze Hello używany format to:

   `https://*storageAccountName*.blob.core.windows.net/*container*/*filename*`

## <a name="technical-details"></a>Szczegóły techniczne
Poniżej przedstawiono hello szczegółów hello wyzwalacze i akcje tego HTTP + Swagger łącznik obsługuje.

## <a name="http--swagger-triggers"></a>HTTP + wyzwalaczy programu Swagger
Wyzwalacz jest zdarzenie, które mogą być używane toostart przepływu pracy hello zdefiniowanej w aplikacji logiki. [Dowiedz się więcej na temat wyzwalaczy.](connectors-overview.md) Witaj HTTP + Swagger łącznik ma jeden wyzwalacz.

| Wyzwalacz | Opis |
| --- | --- |
| HTTP + struktury Swagger |Wykonaj wywołanie HTTP i zwróć hello zawartości odpowiedzi |

## <a name="http--swagger-actions"></a>HTTP + akcje programu Swagger
Akcja jest operacja odbywa się przez hello przepływ pracy, który jest zdefiniowany w aplikacji logiki. [Dowiedz się więcej na temat akcji.](connectors-overview.md) Witaj HTTP + Swagger łącznik ma jedną akcję możliwe.

| Akcja | Opis |
| --- | --- |
| HTTP + struktury Swagger |Wykonaj wywołanie HTTP i zwróć hello zawartości odpowiedzi |

### <a name="action-details"></a>Szczegóły akcji
Witaj HTTP + Swagger łącznika jest dostarczany z jedną akcję możliwe. Poniżej znajdują się informacje o każdej akcji hello, wymaganych i opcjonalnych pól wejściowych i hello odpowiadającego szczegóły danych wyjściowych, które są skojarzone z ich użycia.

#### <a name="http--swagger"></a>HTTP + struktury Swagger
Przesyłania żądania wychodzącego HTTP pomocy metadanych struktury Swagger.
Znak gwiazdki (*) oznacza wymaganego pola.

| Nazwa wyświetlana | Nazwa właściwości | Opis |
| --- | --- | --- |
| Metoda * |— Metoda |Toouse zlecenie HTTP. |
| IDENTYFIKATOR URI * |Identyfikator URI |Identyfikator URI dla żądania hello HTTP. |
| Nagłówki |Nagłówki |Obiekt JSON tooinclude nagłówków HTTP. |
| Treść |Treści |Witaj treści żądania HTTP. |
| Authentication |Uwierzytelnianie |Toouse uwierzytelniania dla żądania. Aby uzyskać więcej informacji, zobacz hello [łącznika HTTP](connectors-native-http.md#authentication). |

**Szczegóły danych wyjściowych**

Odpowiedź HTTP

| Nazwa właściwości | Typ danych | Opis |
| --- | --- | --- |
| Nagłówki |Obiekt |Nagłówki odpowiedzi |
| Treść |Obiekt |Obiekt odpowiedzi |
| Kod stanu |int |Kod stanu HTTP |

### <a name="http-responses"></a>Odpowiedzi HTTP
Podczas wprowadzania wywołania toovarious akcje, może pobrać niektórych odpowiedzi. Poniżej znajduje się tabela przedstawiono odpowiedzi odpowiedniego wraz z opisami.

| Nazwa | Opis |
| --- | --- |
| 200 |OK |
| 202 |Zaakceptowane |
| 400 |Nieprawidłowe żądanie |
| 401 |Brak autoryzacji |
| 403 |Dostęp zabroniony |
| 404 |Nie można odnaleźć |
| 500 |Wewnętrzny błąd serwera. Wystąpił nieznany błąd. |

- - -
## <a name="next-steps"></a>Następne kroki

* [Tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md)
* [Znajdź inne łączniki](apis-list.md)