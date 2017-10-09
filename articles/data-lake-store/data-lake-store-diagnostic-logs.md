---
title: "dzienniki diagnostyczne aaaViewing dla usługi Azure Data Lake Store | Dokumentacja firmy Microsoft"
description: "Zrozumienie sposobu toosetup i dostępu do dzienników diagnostycznych dla usługi Azure Data Lake Store "
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: f6e75eb1-d0ae-47cf-bdb8-06684b7c0a94
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 11fbf7f517f97abdcaf809c1ebeeb51424ab2c1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-diagnostic-logs-for-azure-data-lake-store"></a>Uzyskiwanie dostępu do dzienników diagnostycznych dla usługi Azure Data Lake Store
Więcej informacji na temat jak tooenable rejestrowania diagnostycznego dla konta usługi Data Lake Store i sposobu logowania tooview hello zbierane dla Twojego konta.

Organizacje mogą włączyć rejestrowania diagnostycznego w celu ich Azure Data Lake Store konta toocollect danych zapisy inspekcji dostępu do których znajdują się informacje, takie jak listy użytkowników uzyskujących dostęp do danych hello, jak często jest uzyskiwany dostęp do danych hello, jak dużo danych jest przechowywana w hello konta itp.

## <a name="prerequisites"></a>Wymagania wstępne
* **Subskrypcja platformy Azure**. Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Konto usługi Azure Data Lake Store**. Postępuj zgodnie z instrukcjami hello w [wprowadzenie do usługi Azure Data Lake Store za pomocą portalu Azure hello](data-lake-store-get-started-portal.md).

## <a name="enable-diagnostic-logging-for-your-data-lake-store-account"></a>Włączanie rejestrowania diagnostyki dla konta usługi Data Lake Store
1. Zaloguj się na nowy toohello [Azure Portal](https://portal.azure.com).
2. Otwórz konto usługi Data Lake Store, a w bloku konta usługi z usługą Data Lake Store, kliknij przycisk **ustawienia**, a następnie kliknij przycisk **dzienniki diagnostyczne**.
3. W hello **dzienników diagnostycznych** bloku, kliknij przycisk **Włącz diagnostykę**.

    ![Włączanie rejestrowania diagnostyki](./media/data-lake-store-diagnostic-logs/turn-on-diagnostics.png "Włączanie dzienników diagnostycznych")

3. W hello **diagnostycznych** bloku upewnij powitania po rejestrowania diagnostycznego tooconfigure zmiany.
   
    ![Włączanie rejestrowania diagnostyki](./media/data-lake-store-diagnostic-logs/enable-diagnostic-logs.png "Włączanie dzienników diagnostycznych")
   
   * Ustaw **stan** za**na** tooenable rejestrowania diagnostycznego.
   * Można wybrać hello procesu toostore danych na różne sposoby.
     
        * Wybierz opcję hello zbyt**archiwum konta magazynu tooa** toostore dzienniki tooan konta magazynu Azure. Użyj tej opcji, jeśli chcesz, aby tooarchive hello dane, które będą przetwarzane wsadowe w późniejszym terminie. Po wybraniu tej opcji należy podać konto usługi Azure Storage toosave hello dzienników.
        
        * Wybierz opcję hello zbyt**Centrum zdarzeń tooan strumienia** tooan danych dziennika toostream Azure Event Hub. Najprawdopodobniej będzie Użyj tej opcji, jeśli masz podrzędne przetwarzania potoku tooanalyze przychodzące dzienniki w czasie rzeczywistym. Jeśli wybierzesz tę opcję, podaj szczegóły hello w hello Azure Event Hub ma toouse.

        * Wybierz opcję hello zbyt**wysyłania tooLog Analytics** hello toouse danych dziennika wygenerowany hello tooanalyze usługi Analiza dzienników Azure. Jeśli wybierzesz tę opcję, należy udostępnić hello szczegółów dla obszaru roboczego usługi Operations Management Suite hello które hello Użyj przeprowadza analizę dzienników.
     
   * Określ, czy dzienniki inspekcji tooget Dzienniki żądań i/lub.
   * Określ hello liczbę dni, dla których hello dane muszą zostać zachowane. Przechowywania dotyczy tylko jeśli używane są dane dziennika tooarchive konta magazynu platformy Azure.
   * Kliknij pozycję **Zapisz**.

Po włączeniu ustawienia diagnostyki można obejrzeć hello loguje hello **dzienników diagnostycznych** kartę.

## <a name="view-diagnostic-logs-for-your-data-lake-store-account"></a>Wyświetlanie dzienników diagnostycznych dla Twojego konta usługi Data Lake Store
Istnieją dwa sposoby dane dziennika hello tooview dla konta usługi Data Lake Store.

* Z konta usługi Data Lake Store hello wyświetlić ustawienia
* Z konta magazynu Azure hello przechowywania danych hello

### <a name="using-hello-data-lake-store-settings-view"></a>Za pomocą hello przejrzeć ustawienia magazynu Data Lake
1. Z konta usługi Data Lake Store **ustawienia** bloku, kliknij przycisk **dzienników diagnostycznych**.
   
    ![Widok rejestrowania diagnostycznego](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs.png "wyświetlania dziennika diagnostycznego") 
2. W hello **dzienników diagnostycznych** bloku, powinny pojawić się dzienniki hello skategoryzowany przez **dzienników inspekcji** i **żądania dzienniki**.
   
   * Dzienniki żądań przechwytuje każde żądanie interfejsu API na powitania konta usługi Data Lake Store.
   * Dzienniki inspekcji są podobne dzienniki toorequest, ale zawiera bardziej szczegółowy podział hello operacje wykonywane na koncie usługi Data Lake Store hello. Na przykład wywołanie interfejsu API przekazywanych w dziennikach żądanie może spowodować wiele operacji "Dołącz" hello, dzienniki inspekcji.
3. Kliknij przycisk hello **Pobierz** łącze w odniesieniu do każdego dziennik dzienniki hello toodownload wpisu.

### <a name="from-hello-azure-storage-account-that-contains-log-data"></a>Z hello konta magazynu Azure, która zawiera dane dziennika
1. Otwarcie bloku konta usługi Azure Storage hello skojarzony z usługą Data Lake Store dla rejestrowania, a następnie kliknij przycisk obiektów blob. Witaj **usługa Blob** blok zawiera dwa kontenery.
   
    ![Widok rejestrowania diagnostycznego](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs-storage-account.png "wyświetlania dziennika diagnostycznego")
   
   * kontener Hello **insights dzienniki inspekcji** zawiera hello dzienników inspekcji.
   * kontener Hello **insights dzienniki żądania** zawiera hello Dzienniki żądań.
2. W tych kontenerach hello dzienniki są przechowywane w obszarze hello następujące struktury.
   
    ![Widok rejestrowania diagnostycznego](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs-storage-account-structure.png "wyświetlania dziennika diagnostycznego")
   
    Na przykład może być dziennik inspekcji tooan pełną ścieżkę hello`https://adllogs.blob.core.windows.net/insights-logs-audit/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/mydatalakestore/y=2016/m=07/d=18/h=04/m=00/PT1H.json`
   
    Podobnie, może być hello pełną ścieżkę tooa żądania dziennika`https://adllogs.blob.core.windows.net/insights-logs-requests/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/mydatalakestore/y=2016/m=07/d=18/h=14/m=00/PT1H.json`

## <a name="understand-hello-structure-of-hello-log-data"></a>Zrozumienie hello struktury danych dziennika hello
Witaj dzienniki inspekcji i żądania są w formacie JSON. W tej sekcji możemy Spójrz na powitania struktury JSON dla żądania i dzienniki inspekcji.

### <a name="request-logs"></a>Dzienniki żądań
Oto przykładowy wpis w dzienniku żądania w formacie JSON hello. Każdy obiekt blob ma jeden obiekt głównego o nazwie **rekordów** zawiera tablicę obiektów dziennika.

    {
    "records": 
      [        
        . . . .
        ,
        {
             "time": "2016-07-07T21:02:53.456Z",
             "resourceId": "/SUBSCRIPTIONS/<subscription_id>/RESOURCEGROUPS/<resource_group_name>/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/<data_lake_store_account_name>",
             "category": "Requests",
             "operationName": "GETCustomerIngressEgress",
             "resultType": "200",
             "callerIpAddress": "::ffff:1.1.1.1",
             "correlationId": "4a11c709-05f5-417c-a98d-6e81b3e29c58",
             "identity": "1808bd5f-62af-45f4-89d8-03c5e81bac30",
             "properties": {"HttpMethod":"GET","Path":"/webhdfs/v1/Samples/Outputs/Drivers.csv","RequestContentLength":0,"ClientRequestId":"3b7adbd9-3519-4f28-a61c-bd89506163b8","StartTime":"2016-07-07T21:02:52.472Z","EndTime":"2016-07-07T21:02:53.456Z"}
        }
        ,
        . . . .
      ]
    }

#### <a name="request-log-schema"></a>Schemat dziennika żądania
| Nazwa | Typ | Opis |
| --- | --- | --- |
| time |Ciąg |Sygnatura czasowa Hello (w formacie UTC) hello dziennika |
| resourceId |Ciąg |Umieść Hello identyfikator zasobu hello, w którym została wykonana operacja na |
| category |Ciąg |Kategoria dziennika Hello. Na przykład **żądań**. |
| operationName |Ciąg |Nazwa operacji hello, którym jest zalogowany. Na przykład getfilestatus. |
| resultType |Ciąg |Stan Hello hello operacji, na przykład 200. |
| callerIpAddress |Ciąg |adres IP powitania klienta hello wnioskiem hello |
| correlationId |Ciąg |Identyfikator Hello hello dziennika, który można użyć toogroup razem zbiór wpisów dziennika pokrewne |
| identity |Obiekt |tożsamość Hello, generowany hello dziennika |
| properties |JSON |Wymienione poniżej, aby uzyskać więcej informacji |

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
Oto przykładowy wpis w dzienniku inspekcji w formacie JSON hello. Każdy obiekt blob ma jeden obiekt głównego o nazwie **rekordów** zawiera tablicę obiektów dziennika

    {
    "records": 
      [        
        . . . .
        ,
        {
             "time": "2016-07-08T19:08:59.359Z",
             "resourceId": "/SUBSCRIPTIONS/<subscription_id>/RESOURCEGROUPS/<resource_group_name>/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/<data_lake_store_account_name>",
             "category": "Audit",
             "operationName": "SeOpenStream",
             "resultType": "0",
             "correlationId": "381110fc03534e1cb99ec52376ceebdf;Append_BrEKAmg;25.66.9.145",
             "identity": "A9DAFFAF-FFEE-4BB5-A4A0-1B6CBBF24355",
             "properties": {"StreamName":"adl://<data_lake_store_account_name>.azuredatalakestore.net/logs.csv"}
        }
        ,
        . . . .
      ]
    }

#### <a name="audit-log-schema"></a>Schemat dziennika inspekcji
| Nazwa | Typ | Opis |
| --- | --- | --- |
| time |Ciąg |Sygnatura czasowa Hello (w formacie UTC) hello dziennika |
| resourceId |Ciąg |Umieść Hello identyfikator zasobu hello, w którym została wykonana operacja na |
| category |Ciąg |Kategoria dziennika Hello. Na przykład **inspekcji**. |
| operationName |Ciąg |Nazwa operacji hello, którym jest zalogowany. Na przykład getfilestatus. |
| resultType |Ciąg |Stan Hello hello operacji, na przykład 200. |
| correlationId |Ciąg |Identyfikator Hello hello dziennika, który można użyć toogroup razem zbiór wpisów dziennika pokrewne |
| identity |Obiekt |tożsamość Hello, generowany hello dziennika |
| properties |JSON |Wymienione poniżej, aby uzyskać więcej informacji |

#### <a name="audit-log-properties-schema"></a>Schemat właściwości dziennika inspekcji
| Nazwa | Typ | Opis |
| --- | --- | --- |
| StreamName |Ciąg |Witaj ścieżki hello operacja została wykonana na |

## <a name="samples-tooprocess-hello-log-data"></a>Dane dziennika hello tooprocess próbek
Azure Data Lake Store zapewnia próbkę na temat tooprocess i analizować dane dzienników hello. Można znaleźć przykład hello w [https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample](https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample). 

## <a name="see-also"></a>Zobacz też
* [Omówienie usługi Azure Data Lake Store](data-lake-store-overview.md)
* [Zabezpieczanie danych w usłudze Data Lake Store](data-lake-store-secure-data.md)

