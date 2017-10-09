---
title: "dzienniki diagnostyczne aaaViewing dla usługi Azure Data Lake Analytics | Dokumentacja firmy Microsoft"
description: "Zrozumienie sposobu dostępu diagnostycznych i toosetup logowania dla usługi Azure Data Lake analytics "
services: data-lake-analytics
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: cf5633d4-bc43-444e-90fc-f90fbd0b7935
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 4cd1eb6f585c1ef96c358340232ef85721a972b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-diagnostic-logs-for-azure-data-lake-analytics"></a>Uzyskiwanie dostępu do dzienników diagnostycznych dla usługi Azure Data Lake Analytics

Rejestrowanie diagnostyczne umożliwia zapisy inspekcji dostępu do danych toocollect. Te dzienniki zawierają informacje, takie jak:

* Lista użytkowników, które uzyskiwały dostęp do danych hello.
* Jak często hello jest uzyskiwany dostęp do danych.
* Ile dane są przechowywane na koncie hello.

## <a name="enable-logging"></a>Włącz rejestrowanie

1. Zaloguj się na toohello [portalu Azure](https://portal.azure.com).

2. Otwórz konto usługi Data Lake Analytics i wybierz **dzienniki diagnostyczne** z hello __Monitor__ sekcji. Następnie wybierz pozycję __Włącz diagnostykę__.

    ![Włącz diagnostykę toocollect inspekcji i Dzienniki żądań](./media/data-lake-analytics-diagnostic-logs/turn-on-logging.png)

3. Z __ustawień diagnostycznych__, too__On__ stan hello i wybraniu opcji rejestrowania.

    ![Włącz diagnostykę toocollect inspekcji i Dzienniki żądań](./media/data-lake-analytics-diagnostic-logs/enable-diagnostic-logs.png "Włączanie dzienników diagnostycznych")

   * Ustaw **stan** za**na** tooenable rejestrowania diagnostycznego.

   * Można wybrać hello procesu toostore danych na trzy różne sposoby.

     * Wybierz __archiwum konta magazynu tooa__ toostore logowania na koncie magazynu platformy Azure. Użyj tej opcji, jeśli chcesz, aby tooarchive hello danych. Jeśli wybierzesz tę opcję, musisz podać magazynu Azure konta toosave hello dzienników.

     * Wybierz **strumienia tooan Centrum zdarzeń** tooan danych dziennika toostream Azure Event Hub. Użyj tej opcji, jeśli masz potoku przetwarzania podrzędnego, która analizuje przychodzące dzienniki w czasie rzeczywistym. Jeśli wybierzesz tę opcję, podaj szczegóły hello w hello Azure Event Hub ma toouse.

     * Wybierz __wysyłania tooLog Analytics__ toosend hello danych toohello usługi analizy dzienników. Tej opcji należy używać wtedy, gdy mają toogather analizy dzienników toouse i analizować dzienniki.
   * Określ, czy dzienniki inspekcji tooget Dzienniki żądań i/lub.  Dziennik żądań przechwytuje każde żądanie interfejsu API. Dziennik inspekcji rejestruje wszystkie operacje, które są uruchamiane w tym żądania interfejsu API.

   * Dla __archiwum konta magazynu tooa__, określ hello liczbę dni tooretain hello danych.

   * Kliknij pozycję __Zapisz__.

        > [!NOTE]
        > Musisz wybrać __archiwum konta magazynu tooa__, __strumienia tooan Centrum zdarzeń__ lub __wysyłania tooLog Analytics__ przed kliknięciem przycisku hello __zapisać__przycisku.

Po włączeniu ustawienia diagnostyki może zwracać toohello __dzienników diagnostycznych__ dzienniki hello tooview bloku.

## <a name="view-logs"></a>Wyświetl dzienniki

### <a name="use-hello-data-lake-analytics-view"></a>Użyj widoku usługi Data Lake Analytics hello

1. Z usługi Data Lake Analytics konta bloku, w obszarze **monitorowanie**, wybierz pozycję **dzienników diagnostycznych** i wybierz opcję toodisplay wpis w dziennikach.

    ![Widok rejestrowania diagnostycznego](./media/data-lake-analytics-diagnostic-logs/view-diagnostic-logs.png "wyświetlania dziennika diagnostycznego")

2. Witaj dzienniki są pogrupowane według **dzienników inspekcji** i **żądania dzienniki**.

    ![wpisy dziennika](./media/data-lake-analytics-diagnostic-logs/diagnostic-log-entries.png)

   * Dzienniki żądań przechwytuje każde żądanie interfejsu API na powitania konta usługi Data Lake Analytics.
   * Dzienniki inspekcji są podobne dzienniki toorequest, ale zawiera bardziej szczegółowy podział hello operacji. Na przykład wywołanie interfejsu API przekazywanych w dzienniku żądanie może spowodować wiele operacji "Dołącz" w jego dzienniku inspekcji.

3. Kliknij przycisk hello **Pobierz** łącze toodownload wpisu dziennika, który logowania.

### <a name="use-hello-azure-storage-account-that-contains-log-data"></a>Użyj konta usługi Magazyn Azure hello zawierającego dane dziennika

1. Otwarcie bloku konta usługi Azure Storage hello skojarzony z usługą Data Lake Analytics rejestrowania, a następnie kliknij przycisk __obiekty BLOB__. Witaj **usługa Blob** blok zawiera dwa kontenery.

    ![Widok rejestrowania diagnostycznego](./media/data-lake-analytics-diagnostic-logs/view-diagnostic-logs-storage-account.png "wyświetlania dziennika diagnostycznego")

   * kontener Hello **insights dzienniki inspekcji** zawiera hello dzienników inspekcji.
   * kontener Hello **insights dzienniki żądania** zawiera hello Dzienniki żądań.
2. W tych kontenerach hello dzienniki są przechowywane w obszarze hello następujące struktury:

        resourceId=/
          SUBSCRIPTIONS/
            <<SUBSCRIPTION_ID>>/
              RESOURCEGROUPS/
                <<RESOURCE_GRP_NAME>>/
                  PROVIDERS/
                    MICROSOFT.DATALAKEANALYTICS/
                      ACCOUNTS/
                        <DATA_LAKE_ANALYTICS_NAME>>/
                          y=####/
                            m=##/
                              d=##/
                                h=##/
                                  m=00/
                                    PT1H.json

   > [!NOTE]
   > Witaj `##` wpisy w ścieżce hello zawierają hello roku, miesiąc, dzień i godzinę, w których hello dziennika został utworzony. Data Lake Analytics tworzą jeden plik co godzinę, więc `m=` zawsze zawiera wartość `00`.

    Na przykład może być dziennik inspekcji tooan pełną ścieżkę hello:

        https://adllogs.blob.core.windows.net/insights-logs-audit/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/mydatalakeanalytics/y=2016/m=07/d=18/h=04/m=00/PT1H.json

    Podobnie może być hello pełną ścieżkę tooa żądania dziennika:

        https://adllogs.blob.core.windows.net/insights-logs-requests/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/mydatalakeanalytics/y=2016/m=07/d=18/h=14/m=00/PT1H.json

## <a name="log-structure"></a>Struktura dziennika

Witaj dzienniki inspekcji i żądania są w formacie JSON strukturalnych.

### <a name="request-logs"></a>Dzienniki żądań

Oto przykładowy wpis w dzienniku żądania w formacie JSON hello. Każdy obiekt blob ma jeden obiekt głównego o nazwie **rekordów** zawiera tablicę obiektów dziennika.

    {
    "records":
      [        
        . . . .
        ,
        {
             "time": "2016-07-07T21:02:53.456Z",
             "resourceId": "/SUBSCRIPTIONS/<subscription_id>/RESOURCEGROUPS/<resource_group_name>/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/<data_lake_analytics_account_name>",
             "category": "Requests",
             "operationName": "GetAggregatedJobHistory",
             "resultType": "200",
             "callerIpAddress": "::ffff:1.1.1.1",
             "correlationId": "4a11c709-05f5-417c-a98d-6e81b3e29c58",
             "identity": "1808bd5f-62af-45f4-89d8-03c5e81bac30",
             "properties": {
                 "HttpMethod":"POST",
                 "Path":"/JobAggregatedHistory",
                 "RequestContentLength":122,
                 "ClientRequestId":"3b7adbd9-3519-4f28-a61c-bd89506163b8",
                 "StartTime":"2016-07-07T21:02:52.472Z",
                 "EndTime":"2016-07-07T21:02:53.456Z"
                 }
        }
        ,
        . . . .
      ]
    }

#### <a name="request-log-schema"></a>Schemat dziennika żądania

| Nazwa | Typ | Opis |
| --- | --- | --- |
| time |Ciąg |Sygnatura czasowa Hello (w formacie UTC) hello dziennika |
| resourceId |Ciąg |Umieść Hello identyfikator zasobu hello, który miał operacji na |
| category |Ciąg |Kategoria dziennika Hello. Na przykład **żądań**. |
| operationName |Ciąg |Nazwa operacji hello, którym jest zalogowany. Na przykład GetAggregatedJobHistory. |
| resultType |Ciąg |Stan Hello hello operacji, na przykład 200. |
| callerIpAddress |Ciąg |adres IP powitania klienta hello wnioskiem hello |
| correlationId |Ciąg |Identyfikator Hello hello dziennika. Ta wartość może być używana toogroup zbiór wpisów dziennika powiązane. |
| identity |Obiekt |tożsamość Hello, generowany hello dziennika |
| properties |JSON |Zobacz hello następnej sekcji (schemat właściwości dziennika żądania), aby uzyskać więcej informacji |

#### <a name="request-log-properties-schema"></a>Schemat właściwości dziennika żądania

| Nazwa | Typ | Opis |
| --- | --- | --- |
| HttpMethod |Ciąg |Hello metoda HTTP używana dla operacji hello. Na przykład GET. |
| Ścieżka |Ciąg |Witaj ścieżki hello operacja została wykonana na |
| RequestContentLength |int |Długość zawartości Hello hello HTTP żądania |
| ClientRequestId |Ciąg |Witaj identyfikator, który unikatowo identyfikuje tego żądania |
| Czas rozpoczęcia |Ciąg |czas Hello, w których powitania serwera odebrano hello żądania |
| wartość endTime |Ciąg |czas Hello, w których hello serwer wysłał odpowiedź |

### <a name="audit-logs"></a>Dzienniki inspekcji

Oto przykładowy wpis w dzienniku inspekcji w formacie JSON hello. Każdy obiekt blob ma jeden obiekt głównego o nazwie **rekordów** zawiera tablicę obiektów dziennika.

    {
    "records":
      [        
        . . . .
        ,
        {
             "time": "2016-07-28T19:15:16.245Z",
             "resourceId": "/SUBSCRIPTIONS/<subscription_id>/RESOURCEGROUPS/<resource_group_name>/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/<data_lake_ANALYTICS_account_name>",
             "category": "Audit",
             "operationName": "JobSubmitted",
             "identity": "user@somewhere.com",
             "properties": {
                 "JobId":"D74B928F-5194-4E6C-971F-C27026C290E6",
                 "JobName": "New Job",
                 "JobRuntimeName": "default",
                 "SubmitTime": "7/28/2016 7:14:57 PM"
                 }
        }
        ,
        . . . .
      ]
    }

#### <a name="audit-log-schema"></a>Schemat dziennika inspekcji

| Nazwa | Typ | Opis |
| --- | --- | --- |
| time |Ciąg |Sygnatura czasowa Hello (w formacie UTC) hello dziennika |
| resourceId |Ciąg |Umieść Hello identyfikator zasobu hello, który miał operacji na |
| category |Ciąg |Kategoria dziennika Hello. Na przykład **inspekcji**. |
| operationName |Ciąg |Nazwa operacji hello, którym jest zalogowany. Na przykład JobSubmitted. |
| resultType |Ciąg |Podstan hello stanu zadania (operationName). |
| resultSignature |Ciąg |Więcej informacji na temat stanu zadania hello (operationName). |
| identity |Ciąg |Użytkownik Hello żądanej operacji hello. Na przykład susan@contoso.com. |
| properties |JSON |Zobacz hello następnej sekcji (schemat właściwości dziennika inspekcji), aby uzyskać więcej informacji |

> [!NOTE]
> **Typ resultType** i **resultSignature** udostępniają informacje dotyczące hello wynik operacji i zawierać tylko wartości, jeśli operacja została ukończona. Na przykład tylko z wartościami, gdy **operationName** zawiera wartość **JobStarted** lub **JobEnded**.
>
>

#### <a name="audit-log-properties-schema"></a>Schemat właściwości dziennika inspekcji

| Nazwa | Typ | Opis |
| --- | --- | --- |
| JobId |Ciąg |zadanie toohello przypisanego Identyfikatora Hello |
| Nazwa zadania |Ciąg |Witaj nazwą podaną hello zadania |
| JobRunTime |Ciąg |środowisko uruchomieniowe Hello używane tooprocess hello zadania |
| SubmitTime |Ciąg |Witaj czas (w formacie UTC) to hello zadanie zostało przesłane |
| Czas rozpoczęcia |Ciąg |zadanie hello czasu Hello uruchomienia po przesłaniu (w formacie UTC) |
| wartość endTime |Ciąg |Witaj czasu hello zadanie zakończone |
| Równoległość |Ciąg |Liczba Hello wymagane dla tego zadania podczas przesyłania jednostki usługi Data Lake Analytics |

> [!NOTE]
> **SubmitTime**, **StartTime**, **EndTime**, i **równoległości** udostępniają informacje dotyczące operacji. Te wpisy tylko zawierać wartość, jeśli operacja ma uruchomione lub ukończone. Na przykład **SubmitTime** zawiera tylko wartości po **operationName** ma wartość hello **JobSubmitted**.

## <a name="process-hello-log-data"></a>Dane dziennika hello procesów

Azure Data Lake Analytics zawiera przykładowe tooprocess i analizować dane dzienników hello. Można znaleźć przykład hello w [https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample](https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample).

## <a name="next-steps"></a>Następne kroki
* [Omówienie usługi Azure Data Lake Analytics](data-lake-analytics-overview.md)
