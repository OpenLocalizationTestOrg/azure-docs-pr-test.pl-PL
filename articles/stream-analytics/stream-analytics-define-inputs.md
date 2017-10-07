---
title: "Połączenie danych: dane wejściowe ze strumienia zdarzeń strumienia danych | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o konfigurowaniu tooStream połączenia danych o nazwie \"dane wejściowe\" Analytics. Dane wejściowe zawierają strumień danych zdarzeń i również danych referencyjnych."
keywords: "strumień danych, połączenie danych strumienia zdarzeń"
services: stream-analytics
documentationcenter: 
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: 8155823c-9dd8-4a6b-8393-34452d299b68
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 07/05/2017
ms.author: samacha
ms.openlocfilehash: be2008f159061c5c9be9d0314c27fa67193e3269
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="data-connection-learn-about-data-stream-inputs-from-events-toostream-analytics"></a>Połączenie danych: Dowiedz się więcej o danych wejścia strumienia z tooStream zdarzenia analityka
Witaj zadanie usługi Stream Analytics tooa połączenia danych jest strumienia zdarzeń źródła danych, który jest określony tooas hello zadania *wejściowych*. Analiza strumienia ma najwyższej jakości integracji z źródeł strumienia danych Azure, w tym [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/), [Centrum IoT Azure](https://azure.microsoft.com/services/iot-hub/), i [magazynu obiektów Blob Azure](https://azure.microsoft.com/services/storage/blobs/). Te dane wejściowe źródeł może pochodzić z hello tej samej subskrypcji platformy Azure jako zadanie analizy lub z innej subskrypcji.

## <a name="data-input-types-data-stream-and-reference-data"></a>Dane wejściowe typy: danych strumienia i danych referencyjnych
Jako źródło danych tooa przekazania danych, ma używane przez zadanie usługi Stream Analytics hello i przetwarzane w czasie rzeczywistym. Dane wejściowe są podzielone na dwa typy: dane strumienia danych wejściowych i odwołują się dane wejściowe dane.

### <a name="data-stream-inputs"></a>Dane wejściowe strumienia danych
Strumień danych jest niepowiązany sekwencji zdarzeń w czasie. Zadania usługi analiza strumienia musi zawierać co najmniej jednego danych elementu wejściowego strumienia. Centra zdarzeń, Centrum IoT i magazynu obiektów Blob są obsługiwane jako źródeł dla wejścia strumienia danych. Centra zdarzeń są używane toocollect strumieni zdarzeń z wielu urządzeń i usług. Strumienie te mogą obejmować źródła działań mediów społecznościowych, handlu standardowych informacji lub dane z czujników. Centra IoT są zoptymalizowane toocollect danych z połączonych urządzeń w scenariuszach Internetu rzeczy (IoT).  Magazyn obiektów blob może służyć jako źródło danych wejściowych do wprowadzania danych zbiorczego jako strumienia, takich jak pliki dziennika.  

### <a name="reference-data"></a>Dane referencyjne
Analiza strumienia obsługuje również znane jako dane wejściowe *danych referencyjnych*. Jest to dane pomocnicze, który jest statycznych lub który zmienia się powoli. Zazwyczaj jest używany do wykonywania korelacji i wyszukiwania. Na przykład można sprzęgnąć danych w toodata wejściowego strumienia danych hello w danych referencyjnych hello, ile przeprowadza się toolook sprzężenia SQL, wartości statyczne. Magazyn obiektów Blob Azure jest obecnie obsługiwane tylko hello źródło danych wejściowych danych referencyjnych. Odwołanie do źródła danych typu blob są ograniczone rozmiar too100 MB.

toolearn toocreate odwołania danych wejść, zobacz temat [danych referencyjnych użyj](stream-analytics-use-reference-data.md).  

## <a name="create-data-stream-input-from-event-hubs"></a>Tworzenie elementu wejściowego strumienia danych z usługi Event Hubs

Usługa Azure Event Hubs zapewnia wysoką skalowalnością ingestors zdarzeń publikowania / subskrypcji. Centrum zdarzeń można zbierać miliony zdarzeń na sekundę, dzięki czemu możliwe jest przetwarzanie i analizowanie olbrzymich ilości danych wytworzonych przez podłączone urządzenia i aplikacje hello. Centra zdarzeń i analiza strumienia razem umożliwiają end-to-end rozwiązania do analiz w czasie rzeczywistym — usługi Event Hubs umożliwia strumieniowe źródło zdarzeń na platformie Azure w czasie rzeczywistym, i zadania usługi analiza strumienia może przetwarzać tych zdarzeń w czasie rzeczywistym. Na przykład możesz wysłać kliknięć w sieci web, odczyty czujników lub online dziennika zdarzeń tooEvent koncentratorów. Następnie możesz utworzyć toouse zadania usługi analiza strumienia usługi Event Hubs jako hello strumieni danych wejściowych w czasie rzeczywistym filtrowania, agregację i korelacji.

Sygnatura czasowa domyślne Hello zdarzenia pochodzące z usługi Event Hubs w Stream Analytics jest hello Centrum zdarzeń, która jest dostarczona hello sygnatury czasowej, która hello zdarzeń `EventEnqueuedUtcTime`. tooprocess hello danych jako strumień przy użyciu sygnatury czasowej w ładunku zdarzenia hello, musisz użyć hello [TIMESTAMP BY](https://msdn.microsoft.com/library/azure/dn834998.aspx) — słowo kluczowe.

### <a name="consumer-groups"></a>Grupy odbiorców
Należy skonfigurować każdy analiza strumienia zdarzeń Centrum wejściowych toohave własne grupy odbiorców. Jeśli zadanie zawiera samosprzężenie lub składa się z wielu danych wejściowych, niektóre dane wejściowe mogą odczytać przez więcej niż jeden czytnik poniżej. Taka sytuacja wpływa na powitania liczbę czytników w grupie jednego konsumenta. tooavoid przekraczającej hello usługi Event Hubs limitu pięciu czytników dla każdej grupy odbiorców dla każdej partycji jest najlepszym toodesignate praktyki konsumenta grupy dla każdego zadania usługi analiza strumienia. Istnieje również limit 20 grup odbiorców, na Centrum zdarzeń. Aby uzyskać więcej informacji, zobacz [Event Hubs Programming Guide](../event-hubs/event-hubs-programming-guide.md).

### <a name="configure-an-event-hub-as-a-data-stream-input"></a>Konfigurowanie Centrum zdarzeń jako strumienia danych wejściowych
Witaj poniższej tabeli opisano każdej właściwości w hello **wprowadzania nowych** bloku w hello portalu Azure podczas konfigurowania Centrum zdarzeń jako dane wejściowe.

| Właściwość | Opis |
| --- | --- |
| **Alias wejściowy** |Przyjazną nazwę używaną w tooreference zapytania zadania hello wejściowego. |
| **Przestrzeń nazw magistrali usług** |Azure Service Bus przestrzeń nazw, które to kontener dla zestawu jednostek do obsługi komunikatów. Podczas tworzenia nowego Centrum zdarzeń można również utworzyć przestrzeni nazw usługi Service Bus. |
| **Nazwa Centrum zdarzeń** |Nazwa Hello toouse Centrum zdarzeń hello jako dane wejściowe. |
| **Nazwa zasad Centrum zdarzeń** |Witaj zasady dostępu współdzielonego, który zapewnia Centrum zdarzeń toohello dostępu. Wszystkie zasady dostępu współdzielonego ma nazwę uprawnienia ustawić i klucze dostępu. |
| **Grupy konsumentów Centrum zdarzeń** (opcjonalnie) |powitania klienta grupy toouse tooingest dane z hello Centrum zdarzeń. Jeśli zostanie określona żadna grupa odbiorców, zadanie usługi Stream Analytics hello używa hello domyślna grupa odbiorców. Firma Microsoft zaleca użycie grupy konsumentów różne dla każdego zadania usługi analiza strumienia. |
| **Format serializacji zdarzeń** |Witaj format serializacji (JSON, CSV lub Avro) hello przychodzącego strumienia danych. |
| **Kodowanie** | UTF-8 jest obecnie obsługiwane tylko hello format kodowania. |

Gdy dane pochodzą z Centrum zdarzeń, masz następujące pola metadanych w kwerendzie Stream Analytics toohello dostępu:

| Właściwość | Opis |
| --- | --- |
| **EventProcessedUtcTime** |Hello Data i godzina zdarzenie hello zostało przetworzone przez usługę Stream Analytics. |
| **EventEnqueuedUtcTime** |Witaj Data i godzina zdarzenie hello otrzymała usługi Event Hubs. |
| **PartitionId** |Identyfikator partycji liczony od zera Hello hello adapter wejścia. |

Na przykład przy użyciu tych pól, można napisać zapytanie, takich jak hello poniższy przykład:

````
SELECT
    EventProcessedUtcTime,
    EventEnqueuedUtcTime,
    PartitionId
FROM Input
````

## <a name="create-data-stream-input-from-iot-hub"></a>Tworzenie elementu wejściowego strumienia danych z Centrum IoT
Centrum Iot Azure to wysoce skalowalna publikowania / subskrypcji zoptymalizowane pod kątem scenariuszach IoT systemem zbierania zdarzeń.

Sygnatura czasowa domyślne Hello zdarzenia pochodzące z Centrum IoT w Stream Analytics jest dostarczona hello sygnatury czasowej, która hello zdarzeń Centrum IoT hello, który jest `EventEnqueuedUtcTime`. tooprocess hello danych jako strumień przy użyciu sygnatury czasowej w ładunku zdarzenia hello, musisz użyć hello [TIMESTAMP BY](https://msdn.microsoft.com/library/azure/dn834998.aspx) — słowo kluczowe.

> [!NOTE]
> Tylko wiadomości wysyłane z `DeviceClient` właściwości mogą być przetwarzane.
> 
> 

### <a name="consumer-groups"></a>Grupy odbiorców
Należy skonfigurować każdy toohave wejściowych Centrum IoT analiza strumienia własne grupy odbiorców. Jeśli zadanie zawiera samosprzężenie lub składa się z wielu danych wejściowych, niektóre dane wejściowe mogą odczytać przez więcej niż jeden czytnik poniżej. Taka sytuacja wpływa na powitania liczbę czytników w grupie jednego konsumenta. tooavoid przekraczającej hello Azure IoT Hub limitu pięciu czytników dla każdej grupy odbiorców dla każdej partycji jest najlepszym toodesignate praktyki konsumenta grupy dla każdego zadania usługi analiza strumienia.

### <a name="configure-an-iot-hub-as-a-data-stream-input"></a>Konfigurowanie Centrum IoT jako strumienia danych wejściowych
Witaj poniższej tabeli opisano każdej właściwości w hello **wprowadzania nowych** bloku w hello portalu Azure podczas konfigurowania Centrum IoT jako dane wejściowe.

| Właściwość | Opis |
| --- | --- |
| **Alias wejściowy** |Przyjazną nazwę używaną w tooreference zapytania zadania hello wejściowego.|
| **Centrum IoT** |Nazwa Hello toouse Centrum IoT hello jako dane wejściowe. |
| **Punkt końcowy** |Witaj punktu końcowego Centrum IoT hello.|
| **Nazwa zasady dostępu współdzielonego** |zasady dostępu Hello udostępnione, która zapewnia Centrum IoT toohello dostępu. Wszystkie zasady dostępu współdzielonego ma nazwę uprawnienia ustawić i klucze dostępu. |
| **Klucz zasady dostępu współdzielonego** |klucz dostępu współdzielonego Hello używany Centrum IoT toohello dostępu tooauthorize. |
| **Grupy odbiorców** (opcjonalnie) |powitania klienta grupy toouse tooingest danych z Centrum IoT hello. Jeśli zostanie określona żadna grupa odbiorców, zadanie usługi Stream Analytics korzysta hello domyślna grupa odbiorców. Zalecane jest użycie grupy odbiorców różne dla każdego zadania usługi analiza strumienia. |
| **Format serializacji zdarzeń** |Witaj format serializacji (JSON, CSV lub Avro) hello przychodzącego strumienia danych. |
| **Kodowanie** |UTF-8 jest obecnie obsługiwane tylko hello format kodowania. |

Gdy dane pochodzą z Centrum IoT, masz następujące pola metadanych w kwerendzie Stream Analytics toohello dostępu:

| Właściwość | Opis |
| --- | --- |
| **EventProcessedUtcTime** |Witaj Data i godzina zdarzenia hello została przetworzona. |
| **EventEnqueuedUtcTime** |Witaj Data i godzina zdarzenia hello otrzymała hello Centrum IoT. |
| **PartitionId** |Identyfikator partycji liczony od zera Hello hello adapter wejścia. |
| **IoTHub.MessageId** | Identyfikator, który został użyty toocorrelate dwukierunkowej komunikacji w Centrum IoT. |
| **IoTHub.CorrelationId** |Identyfikator, który jest używany w odpowiedzi komunikat i opinie w Centrum IoT. |
| **IoTHub.ConnectionDeviceId** |Identyfikator uwierzytelniania Hello używany toosend tego komunikatu. Ta wartość jest dołączana do komunikatów servicebound przez Centrum IoT hello. |
| **IoTHub.ConnectionDeviceGenerationId** |Identyfikator generacji Hello hello uwierzytelniony urządzenie, które było używane toosend tego komunikatu. Ta wartość jest dołączana do komunikatów servicebound przez Centrum IoT hello. |
| **IoTHub.EnqueuedTime** |czas Hello otrzymania wiadomości powitania przez Centrum IoT hello. |
| **IoTHub.StreamId** |Właściwość zdarzenie niestandardowe dodane przez hello nadawcy urządzenia. |


## <a name="create-data-stream-input-from-blob-storage"></a>Tworzenie elementu wejściowego strumienia danych z magazynu obiektów Blob
W przypadku scenariuszy z dużych ilości danych bez struktury toostore w chmurze hello magazynu obiektów Blob Azure oferuje ekonomiczne i skalowalne rozwiązanie. Dane w magazynie obiektów Blob jest zazwyczaj uważana za przechowywanych danych. Jednak będzie można przetwarzać jako strumień danych przez usługę Stream Analytics. Typowy scenariusz w danych wejściowych magazynu obiektów Blob z usługi Stream Analytics jest przetwarzania dziennika. W tym scenariuszu zostały przechwycone dane telemetryczne z systemu i potrzeb toobe przeanalizować i przetworzyć tooextract istotnych danych.

Witaj domyślne sygnatura czasowa zdarzenia magazynu obiektów Blob w Stream Analytics jest ostatniej modyfikacji hello sygnatury czasowej, która hello obiektów blob, który jest `BlobLastModifiedUtcTime`. tooprocess hello danych jako strumień przy użyciu sygnatury czasowej w ładunku zdarzenia hello, musisz użyć hello [TIMESTAMP BY](https://msdn.microsoft.com/library/azure/dn834998.aspx) — słowo kluczowe.

Wejść w formacie CSV *wymagają* toodefine wiersz nagłówka pola hello zestawu danych. Ponadto wszystkie pola wiersz nagłówka musi być unikatowa.

> [!NOTE]
> Analiza strumienia nie obsługuje dodawania istniejącym obiektem blob tooan zawartości. Analiza strumienia zostaną wyświetlone tylko raz obiektu blob, a wszelkie zmiany, które są wykonywane w obiekcie blob powitania po hello zadania może odczytywać hello dane nie są przetwarzane. Najlepszym rozwiązaniem jest tooupload wszystkich danych hello raz, a następnie nie Dodaj magazynu obiektów blob toothat zdarzenia.
> 

### <a name="configure-blob-storage-as-a-data-stream-input"></a>Konfigurowanie magazynu obiektów Blob jako strumienia danych wejściowych

Witaj poniższej tabeli opisano każdej właściwości w hello **wprowadzania nowych** bloku w hello portalu Azure podczas konfigurowania magazynu obiektów Blob jako dane wejściowe.

| Właściwość | Opis |
| --- | --- |
| **Alias wejściowy** | Przyjazną nazwę używaną w tooreference zapytania zadania hello wejściowego. |
| **Konto magazynu** | Nazwa Hello hello konta magazynu, gdzie znajdują się pliki blob hello. |
| **Klucz konta magazynu** | klucz tajny Hello skojarzone z kontem magazynu hello. |
| **Kontener** | kontener Hello hello obiektów blob w danych wejściowych. Kontenery umożliwiają logiczne grupowanie dla obiektów blob przechowywanych w hello usługi obiektów Blob Microsoft Azure. Podczas przekazywania toohello obiektu blob usługi magazynu obiektów Blob platformy Azure, należy określić kontener dla tego obiektu blob. |
| **Wzorzec ścieżki** (opcjonalnie) | Ścieżka pliku Hello użyć obiektów blob hello toolocate w określonym kontenerze hello. W ścieżce hello, można określić jedną lub więcej wystąpień hello następujących trzech zmiennych: `{date}`, `{time}`, lub`{partition}`<br/><br/>Przykład 1:`cluster1/logs/{date}/{time}/{partition}`<br/><br/>Przykład 2:`cluster1/logs/{date}`<br/><br/>Witaj `*` znak nie jest dozwolona wartość hello ścieżki prefiks. Jedyne prawidłowe <a HREF="https://msdn.microsoft.com/library/azure/dd135715.aspx">znaków obiektów blob platformy Azure</a> są dozwolone. |
| **Format daty** (opcjonalnie) | Użycie zmiennej Data hello w ścieżce hello hello format daty, w których hello pliki są organizowane. Przykład:`YYYY/MM/DD` |
| **Format czasu** (opcjonalnie) |  Użycie zmiennej czasu hello w ścieżce hello hello format czasu, w którym hello pliki są organizowane. Obecnie obsługiwane tylko hello wartość jest `HH`. |
| **Format serializacji zdarzeń** | Witaj format serializacji (JSON, CSV lub Avro) dla przychodzących strumieni danych. |
| **Kodowanie** | Dla woluminu CSV i JSON UTF-8 jest obecnie hello obsługiwany tylko format kodowania. |

Gdy dane pochodzą ze źródła magazynu obiektów Blob, masz następujące pola metadanych w kwerendzie Stream Analytics toohello dostępu:

| Właściwość | Opis |
| --- | --- |
| **Element BlobName** |Nazwa Hello hello blob danych wejściowych hello zdarzeń pochodzi z. |
| **EventProcessedUtcTime** |Hello Data i godzina zdarzenie hello zostało przetworzone przez usługę Stream Analytics. |
| **BlobLastModifiedUtcTime** |Witaj, Data i godzina ostatniej modyfikacji tego obiektu blob hello. |
| **PartitionId** |Identyfikator partycji liczony od zera Hello hello adapter wejścia. |

Na przykład przy użyciu tych pól, można napisać zapytanie, takich jak hello poniższy przykład:

````
SELECT
    BlobName,
    EventProcessedUtcTime,
    BlobLastModifiedUtcTime
FROM Input
````

## <a name="get-help"></a>Uzyskiwanie pomocy
Aby uzyskać dodatkową pomoc, spróbuj naszych [forum usługi Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Następne kroki
Znasz opcji połączenia danych na platformie Azure dla Twojego zadania usługi analiza strumienia. toolearn więcej informacji na temat usługi Stream Analytics, zobacz:

* [Get started using Azure Stream Analytics (Rozpoczynanie pracy z usługą Azure Stream Analytics)](stream-analytics-real-time-fraud-detection.md)
* [Scale Azure Stream Analytics jobs (Skalowanie zadań usługi Azure Stream Analytics)](stream-analytics-scale-jobs.md)
* [Azure Stream Analytics Query Language Reference (Dokumentacja dotycząca języka zapytań usługi Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Stream Analytics Management REST API Reference (Dokumentacja interfejsu API REST zarządzania usługą Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835031.aspx)

<!--Link references-->
[stream.analytics.developer.guide]: ../stream-analytics-developer-guide.md
[stream.analytics.scale.jobs]: stream-analytics-scale-jobs.md
[stream.analytics.introduction]: stream-analytics-introduction.md
[stream.analytics.get.started]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301
