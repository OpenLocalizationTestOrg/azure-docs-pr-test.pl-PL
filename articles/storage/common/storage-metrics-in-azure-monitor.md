---
title: Azure metryki magazynu w monitorze Azure | Dokumentacja firmy Microsoft
description: "Więcej informacji o nowe metryki oferowane za pośrednictwem Monitora Azure."
services: storage
documentationcenter: na
author: fhryo-msft
manager: cbrooks
editor: fhryo-msft
ms.assetid: 
ms.service: storage
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage
ms.date: 09/05/2017
ms.author: fryu
ms.openlocfilehash: d30a99044e335723e5d2c4bbd71fab7e4fd51145
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/11/2017
---
# <a name="azure-storage-metrics-in-azure-monitor-preview"></a>Azure metryki magazynu w monitorze Azure (wersja zapoznawcza)

Metryki dotyczące usługi Azure Storage możesz analizować trendy użycia i śledzenie żądań i diagnozowanie problemów z kontem magazynu.

Azure Monitor udostępnia interfejsy użytkownika ujednoliconego do monitorowania w różnych usługach Azure. Aby uzyskać więcej informacji, zobacz [Azure Monitor](../../monitoring-and-diagnostics/monitoring-overview.md). Magazyn Azure integruje się Azure Monitor wysyłając metryki danych do platformy Azure monitora.

## <a name="access-metrics"></a>Metryki dostępu

Azure Monitor oferuje wiele sposobów metryki dostępu. Użytkownik może uzyskiwać do nich dostęp z [portalu Azure](https://portal.azure.com), interfejsów API usługi Azure monitora (REST i .net) i rozwiązań analitycznych, takie jak operacji Management Suite i Centrum zdarzeń. Aby uzyskać więcej informacji, zobacz [metryki Monitor Azure](../../monitoring-and-diagnostics/monitoring-overview-metrics.md).

Metryki są domyślnie włączone i można uzyskać dostępu do 30 dni najnowszych danych. Jeśli chcesz zachować dane przez dłuższy okres czasu, można archiwizować dane metryk do konta usługi Azure Storage. Te ustawienia zostaną skonfigurowane w [ustawień diagnostycznych](../../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings) w monitorze Azure.

### <a name="access-metrics-in-the-azure-portal"></a>Metryki dostępu w portalu Azure

Można monitorować metryki wraz z upływem czasu, w portalu Azure. Poniżej przedstawiono przykład przedstawiający sposób wyświetlania **UsedCapacity** na poziomie konta.

![Zrzut ekranu przedstawiający dostęp do metryk w portalu Azure](./media/storage-metrics-in-azure-monitor/access-metrics-in-portal.png)

Dla metryki pomocnicze, wymiary możesz filtrować z żądaną wartością. Poniżej przedstawiono przykład przedstawiający sposób wyświetlania **transakcji** na poziomie konta z **Powodzenie** typ odpowiedzi.

![Zrzut ekranu przedstawiający dostęp do metryk z wymiarem w portalu Azure](./media/storage-metrics-in-azure-monitor/access-metrics-in-portal-with-dimension.png)

### <a name="access-metrics-with-the-rest-api"></a>Metryki dostępu przy użyciu interfejsu API REST

Azure Monitor udostępnia [interfejsów API REST](/rest/api/monitor/) odczytać metryki definicji i wartości. W tej sekcji przedstawiono sposób odczytać metryki magazynu. Identyfikator zasobu jest używany podczas wszystkich interfejsów API REST. Więcej informaiton odczytu [opis identyfikator zasobu dla usług w magazynie](#understanding-resource-id-for-services-in-storage).

Poniższy przykład przedstawia użycie [ArmClient](https://github.com/projectkudu/ARMClient) w wierszu polecenia, aby uprościć testowanie za pomocą interfejsu API REST.

#### <a name="list-account-level-metric-definition-with-the-rest-api"></a>Konto poziomu metryki definicji listy przy użyciu interfejsu API REST

Poniższy przykład przedstawia sposób wyświetlania definicji metryki na poziomie konta:

```
# Login to Azure and enter your credentials when prompted.
> armclient login

> armclient GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{storageAccountName}/providers/microsoft.insights/metricdefinitions?api-version=2017-05-01-preview

```

Jeśli chcesz listy definicji metryk dla obiekt blob, tabel, pliku lub kolejek, należy określić różne identyfikatory zasobów dla każdej usługi przy użyciu interfejsu API.

Odpowiedź zawiera metryki definicji w formacie JSON:

```Json
{
  "value": [
    {
      "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{storageAccountName}/providers/microsoft.insights/metricdefinitions/UsedCapacity",
      "resourceId": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{storageAccountName}",
      "category": "Capacity",
      "name": {
        "value": "UsedCapacity",
        "localizedValue": "Used capacity"
      },
      "isDimensionRequired": false,
      "unit": "Bytes",
      "primaryAggregationType": "Average",
      "metricAvailabilities": [
        {
          "timeGrain": "PT1M",
          "retention": "P30D"
        },
        {
          "timeGrain": "PT1H",
          "retention": "P30D"
        }
      ]
    },
    ... next metric definition
  ]
}

```

#### <a name="read-account-level-metric-values-with-the-rest-api"></a>Odczytać wartości metryki poziomu kont przy użyciu interfejsu API REST

Poniższy przykład pokazuje, jak można odczytać danych metryki na poziomie konta:

```
> armclient GET "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{storageAccountName}/providers/microsoft.insights/metrics?metric=Availability&api-version=2017-05-01-preview&aggregation=Average&interval=PT1H"

```

W powyżej przykład, jeśli chcesz odczytać wartości metryki dla obiekt blob, tabeli, plik lub kolejki, należy określić różne identyfikatory zasobów dla każdej usługi przy użyciu interfejsu API.

Następującą odpowiedź zawiera metryki wartości w formacie JSON:

```Json
{
  "cost": 0,
  "timespan": "2017-09-07T17:27:41Z/2017-09-07T18:27:41Z",
  "interval": "PT1H",
  "value": [
    {
      "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{storageAccountName}/providers/Microsoft.Insights/metrics/Availability",
      "type": "Microsoft.Insights/metrics",
      "name": {
        "value": "Availability",
        "localizedValue": "Availability"
      },
      "unit": "Percent",
      "timeseries": [
        {
          "metadatavalues": [],
          "data": [
            {
              "timeStamp": "2017-09-07T17:27:00Z",
              "average": 100.0
            }
          ]
        }
      ]
    }
  ]
}

```

## <a name="billing-for-metrics"></a>Rozliczeń dla metryki

Przy użyciu metryk w monitorze Azure jest obecnie bezpłatna. Jednak użycie dodatkowych rozwiązań wprowadzania danych metryki, użytkownik może zostać użyta przez te rozwiązania. Na przykład możesz są rozliczane przez usługi Azure Storage archiwizacji danych metryk do konta usługi Azure Storage. Lub jeśli strumienia danych metryki z usługą OMS dla zaawansowanej analizy, są rozliczane przez operację Management Suite (OMS).

## <a name="understanding-resource-id-for-services-in-azure-storage"></a>Identyfikator zasobu opis dla usług w usłudze Azure Storage

Identyfikator zasobu jest identyfikator zasobu na platformie Azure. Korzystając z interfejsu API REST Azure Monitor odczytać definicje metryk lub wartości, należy użyć Identyfikatora zasobu dla zasobu, na którym ma działać. Szablon Identyfikatora zasobu ma następujący format:

`
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/{resourceProviderNamespace}/{resourceType}/{resourceName}
`

Magazyn zapewnia metryk zarówno poziom konta magazynu i poziomu usług z monitorem Azure. Na przykład można pobrać metryki tylko magazynu obiektów Blob. Każdy poziom ma własną identyfikatorów zasobów, które służy do pobierania metryki tylko na tym poziomie.

### <a name="resource-id-for-a-storage-account"></a>Identyfikator zasobu dla konta magazynu

Poniżej przedstawiono format Określ identyfikator ID zasobu dla konta magazynu.

`
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{storageAccountName}
`

### <a name="resource-id-for-the-storage-services"></a>Identyfikator zasobu dla usług magazynu

Poniżej przedstawiono format Określ identyfikator ID zasobu dla każdej z usług magazynu.

* Identyfikator zasobu usługi blob`
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{storageAccountName}/blobServices/default
`
* Identyfikator zasobu usługi tabel`
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{storageAccountName}/tableServices/default
`
* Identyfikator zasobu usługi kolejki`
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{storageAccountName}/queueServices/default
`
* Identyfikator zasobu usługi plików`
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{storageAccountName}/fileServices/default
`

### <a name="resource-id-in-azure-monitor-rest-api"></a>Identyfikator zasobu w monitorze Azure interfejsu API REST

Poniżej przedstawiono wzorzec używana przy wywoływaniu interfejsu API REST Azure monitora.

`
GET {resourceId}/providers/microsoft.insights/metrics?{parameters}
`

## <a name="capacity-metrics"></a>Metryki pojemności

Wartości metryk wydajności są wysyłane do monitora Azure co godzinę. Wartości są odświeżane codziennie. Ziarno czasu określa przedział czasu, dla której przedstawiono wartości metryk. Ziarno czasu obsługiwanych na wszystkie metryki pojemności to jedna godzina (PT1H).

Usługa Azure Storage udostępnia następujące metryki wydajności w monitorze Azure.

### <a name="account-level"></a>Poziom konta

| Nazwa metryki | Opis |
| ------------------- | ----------------- |
| UsedCapacity | Wielkość magazynu używanego przez konta magazynu. W przypadku kont magazynu w warstwie standardowa jest to Suma pojemności używane przez obiekt blob, tabeli, pliku i kolejki. Dla kont premium magazynu i kont magazynu obiektów Blob jest taka sama jak BlobCapacity. <br/><br/> Jednostka: bajtów <br/> Typ agregacji: średni <br/> Przykładowe wartości: 1024 |

### <a name="blob-storage"></a>Blob Storage

| Nazwa metryki | Opis |
| ------------------- | ----------------- |
| BlobCapacity | Suma magazynu obiektów Blob używane w ramach konta magazynu. <br/><br/> Jednostka: bajtów <br/> Typ agregacji: średni <br/> Przykładowe wartości: 1024 <br/> Wymiar: BlobType ([definicji](#metrics-dimensions)) |
| Liczba obiektów blob    | Liczba przechowywanych w ramach konta magazynu obiektów blob. <br/><br/> Jednostka: liczba <br/> Typ agregacji: średni <br/> Przykładowe wartości: 1024 <br/> Wymiar: BlobType ([definicji](#metrics-dimensions)) |
| ContainerCount    | Liczba kontenerów w ramach konta magazynu. <br/><br/> Jednostka: liczba <br/> Typ agregacji: średni <br/> Przykładowe wartości: 1024 |

### <a name="table-storage"></a>Magazyn tabel

| Nazwa metryki | Opis |
| ------------------- | ----------------- |
| TableCapacity | Wielkość magazynu tabel używanych przez konto magazynu. <br/><br/> Jednostka: bajtów <br/> Typ agregacji: średni <br/> Przykładowe wartości: 1024 |
| TableCount   | Liczba tabel na koncie magazynu. <br/><br/> Jednostka: liczba <br/> Typ agregacji: średni <br/> Przykładowe wartości: 1024 |
| TableEntityCount | Liczba jednostek tabeli na koncie magazynu. <br/><br/> Jednostka: liczba <br/> Typ agregacji: średni <br/> Przykładowe wartości: 1024 |

### <a name="queue-storage"></a>Queue Storage

| Nazwa metryki | Opis |
| ------------------- | ----------------- |
| QueueCapacity | Wielkość kolejki magazynu używanego przez konta magazynu. <br/><br/> Jednostka: bajtów <br/> Typ agregacji: średni <br/> Przykładowe wartości: 1024 |
| QueueCount   | Liczba kolejek na koncie magazynu. <br/><br/> Jednostka: liczba <br/> Typ agregacji: średni <br/> Przykładowe wartości: 1024 |
| QueueMessageCount | Liczba wiadomości w kolejce niewygasłe na koncie magazynu. <br/><br/>Jednostka: liczba <br/> Typ agregacji: średni <br/> Przykładowe wartości: 1024 |

### <a name="file-storage"></a>File Storage

| Nazwa metryki | Opis |
| ------------------- | ----------------- |
| FileCapacity | Ilość przechowywania plików używane przez konto magazynu. <br/><br/> Jednostka: bajtów <br/> Typ agregacji: średni <br/> Przykładowe wartości: 1024 |
| FileCount   | Liczba plików w ramach konta magazynu. <br/><br/> Jednostka: liczba <br/> Typ agregacji: średni <br/> Przykładowe wartości: 1024 |
| FileShareCount | Liczba plików udziałów na koncie magazynu. <br/><br/> Jednostka: liczba <br/> Typ agregacji: średni <br/> Przykładowe wartości: 1024 |

## <a name="transaction-metrics"></a>Metryki transakcji

Metryki transakcji są wysyłane z usługi Azure Storage do monitorowania Azure co minutę. Wszystkie metryki transakcji są dostępne na poziomie usługi oraz konta (magazynu obiektów Blob, Magazyn tabel Azure plików i magazynu kolejek). Ziarno czasu określa przedział czasu, które są prezentowane wartości metryki. Ziarno czasu obsługiwane dla wszystkich transakcji metryki są PT1H i PT1M.

Usługa Azure Storage udostępnia następujące metryki transakcji w monitorze Azure.

| Nazwa metryki | Opis |
| ------------------- | ----------------- |
| Transakcje | Liczba żądań wysyłanych do usługi magazynu lub określonej operacji interfejsu API. Liczba ta obejmuje udane i nieudane żądania, a także żądań, które tworzone błędy. <br/><br/> Jednostka: liczba <br/> Typ agregacji: Całkowita liczba <br/> Zastosowanie wymiarów: wartość ResponseType, GeoType, Nazwa_funkcji_api ([definicji](#metrics-dimensions))<br/> Przykładowe wartości: 1024 |
| Zdarzenia związane z transferem danych przychodzących | Ilość danych wejściowych. Liczba ta obejmuje transfer danych przychodzących z zewnętrznego klienta do usługi Azure Storage, a także ruch przychodzący w obrębie platformy Azure. <br/><br/> Jednostka: bajtów <br/> Typ agregacji: Całkowita liczba <br/> Zastosowanie wymiarów: GeoType, Nazwa_funkcji_api ([definicji](#metrics-dimensions)) <br/> Przykładowe wartości: 1024 |
| Transfer danych wychodzących | Ilość danych wyjściowych. Liczba ta obejmuje wyjście z zewnętrznego klienta do usługi Azure Storage, a także Wyjście w obrębie platformy Azure. W związku z tym ta liczba nie odzwierciedla wyjście rozliczeniowy. <br/><br/> Jednostka: bajtów <br/> Typ agregacji: Całkowita liczba <br/> Zastosowanie wymiarów: GeoType, Nazwa_funkcji_api ([definicji](#metrics-dimensions)) <br/> Przykładowe wartości: 1024 |
| SuccessServerLatency | Średni czas używaną do przetwarzania żądań pomyślnie usługi Azure Storage. Ta wartość nie obejmuje opóźnienia sieci, określona w SuccessE2ELatency. <br/><br/> Jednostka: w milisekundach <br/> Typ agregacji: średni <br/> Zastosowanie wymiarów: GeoType, Nazwa_funkcji_api ([definicji](#metrics-dimensions)) <br/> Przykładowe wartości: 1024 |
| SuccessE2ELatency | Średnie opóźnienie end-to-end pomyślnych żądań wysyłanych do usługi magazynu lub określonej operacji interfejsu API. Ta wartość obejmuje wymagany czas przetwarzania w ramach usługi Azure Storage do odczytu żądania, wysyłania odpowiedzi i otrzyma odpowiedź. <br/><br/> Jednostka: w milisekundach <br/> Typ agregacji: średni <br/> Zastosowanie wymiarów: GeoType, Nazwa_funkcji_api ([definicji](#metrics-dimensions)) <br/> Przykładowe wartości: 1024 |
| Dostępność | Procent dostępności usługi magazynu lub określonej operacji interfejsu API. Dostępność jest obliczana przez pobranie wartość całkowita liczba żądań rozliczeń i podzielenie go przez liczbę odpowiednie żądania, w tym te żądania, które tworzone nieoczekiwane błędy. Wszystkie powodować nieoczekiwane błędy zmniejszona dostępność usługi magazynu lub określonej operacji interfejsu API. <br/><br/> Jednostka: procent <br/> Typ agregacji: średni <br/> Zastosowanie wymiarów: GeoType, Nazwa_funkcji_api ([definicji](#metrics-dimensions)) <br/> Przykładowe wartości: 99,99 |

## <a name="metrics-dimensions"></a>Wymiary metryk

Usługa Azure Storage obsługuje następujące wymiary metryki w monitorze Azure.

| Nazwa wymiaru | Opis |
| ------------------- | ----------------- |
| BlobType | Typ obiektu blob dla tylko metryki obiektów Blob. Obsługiwane wartości to **BlockBlob** i **PageBlob**. Dołącz obiekt Blob jest uwzględniona w BlockBlob. |
| Wartość ResponseType | Typ odpowiedzi transakcji. Dostępne wartości to: <br/><br/> <li>ServerOtherError: Inne błędy po stronie serwera, z wyjątkiem opisano te </li> <li> ServerBusyError: Żądanie uwierzytelniony zwrócił kod stanu HTTP 503. (Nie obsługuje jeszcze) </li> <li> ServerTimeoutError: Upłynął limit czasu żądania uwierzytelnionego który zwrócił kod stanu HTTP 500. Nastąpiło przekroczenie limitu czasu z powodu błędu serwera. </li> <li> ThrottlingError: Suma po stronie klienta i po stronie serwera błąd ograniczenia przepustowości (zostanie usunięta po ServerBusyError i ClientThrottlingError są obsługiwane) </li> <li> AuthorizationError: Żądanie uwierzytelniony nie powiodło się z powodu nieautoryzowanego dostępu do danych lub wystąpił błąd autoryzacji. </li> <li> NetworkError: Żądanie uwierzytelniony nie powiodło się z powodu błędów sieci. Najczęściej występuje, gdy klient przedwcześnie zamyka połączenie przed jego wygaśnięciem limitu czasu. </li> <li>  ClientThrottlingError: Błąd po stronie klienta ograniczenia przepustowości (nieobsługiwane jeszcze) </li> <li> ClientTimeoutError: Upłynął limit czasu żądania uwierzytelnionego który zwrócił kod stanu HTTP 500. Jeśli limit czasu sieci klienta lub limit czasu żądania jest ustawiona na mniejszą wartość niż oczekiwano przez usługę magazynu, jest oczekiwany limitu czasu. W przeciwnym razie zostanie zgłoszone jako ServerTimeoutError. </li> <li> ClientOtherError: Inne błędy po stronie klienta, z wyjątkiem opisane z nich. </li> <li> Powodzenie: Pomyślnie żądania|
| GeoType | Transakcja z podstawowej lub pomocniczej klastra. Dostępne wartości to podstawowe i pomocnicze. Dotyczy to dostęp do odczytu z magazynu geograficznie nadmiarowego Storage(RA-GRS) podczas odczytywania obiektów ze dodatkowej dzierżawy. |
| Nazwa_funkcji_api | Nazwa operacji. Na przykład: <br/> <li>Tworzony kontener</li> <li>DeleteBlob</li> <li>GetBlob</li> Nazwy wszystkich operacji, zobacz [dokumentu](/rest/api/storageservices/storage-analytics-logged-operations-and-status-messages#logged-operations.md). |

Obsługa metryki wymiarów należy określić wartość wymiaru, aby wyświetlić odpowiednie wartości metryki. Na przykład, jeśli przyjrzymy się **transakcji** wartość dla pomyślnej odpowiedzi, należy filtrować **wartość ResponseType** wymiaru z **Powodzenie**. Lub jeśli przyjrzymy się **BlobCount** wartość dla blokowych obiektów Blob, należy filtrować **BlobType** wymiaru z **BlockBlob**.

## <a name="service-continuity-of-legacy-metrics"></a>Ciągłość usługi starszych metryk

Metryki starszej wersji są dostępne równolegle z metryki Monitor Azure zarządzanych. Obsługa utrzymuje takie same, aż do usługi Azure Storage kończy się usługę w starszych metryki. Firma Microsoft będzie ogłaszamy końcowy planu po oficjalnie wydania metryki Monitor Azure zarządzanych.

## <a name="see-also"></a>Zobacz też

* [Azure Monitor](../../monitoring-and-diagnostics/monitoring-overview.md)
