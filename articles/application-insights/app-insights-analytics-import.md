---
title: "aaaImport Twojego tooAnalytics danych w usłudze Azure Application Insights | Dokumentacja firmy Microsoft"
description: "Importowanie danych statycznych toojoin o telemetrii aplikacji lub zaimportować tooquery strumień danych, z Analytics."
services: application-insights
keywords: "Otwórz schematu, importowania danych"
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: bwren
ms.openlocfilehash: 7a3a3c9155adc1885dd366ddb13dda80bb894adb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="import-data-into-analytics"></a>Importowanie danych do analityka

Importowanie danych tabelarycznych w [Analytics](app-insights-analytics.md), albo toojoin za pomocą [usługi Application Insights](app-insights-overview.md) dane telemetryczne z aplikacji, lub tak, aby można analizować je jako osobne strumienia. Analytics to zaawansowane zapytania języka tooanalyzing dobrze nadaje się oznaczony znacznikiem czasowym dużych strumieni danych telemetrycznych.

Możesz zaimportować dane analizy przy użyciu własnego schematu. Nie ma toouse hello standardowe usługi Application Insights schematów, takich jak żądania lub śledzenia.

Możesz zaimportować JSON lub widoku źródła danych (wartości rozdzielonych ogranicznikami - przecinek, średnik lub kartę) plików.

Istnieją trzy sytuacje, w którym importowanie tooAnalytics jest przydatne:

* **Dołącz z danych telemetrycznych aplikacji.** Na przykład można zaimportować tabelę, która mapuje adresy URL z tytułów do odczytu strony toomore z witryny sieci Web. W module analiz można utworzyć raport wykresu pulpitu nawigacyjnego, który zawiera hello dziesięć najpopularniejszych stron w witrynie sieci Web. Teraz go można wyświetlić hello tytuły stron zamiast hello adresów URL.
* **Korelowanie dane telemetryczne aplikacji** z innych źródeł, takie jak ruch w sieci, dane serwera lub CDN pliki dziennika.
* **Zastosuj Analytics tooa odrębne strumienia.** Application Insights Analytics jest zaawansowane narzędzia, która współdziała również z rozrzedzony, strumienie oznaczony znacznikiem czasowym — znacznie lepszą niż SQL w wielu przypadkach. Jeśli masz takich strumienia z z innego źródła, można analizować je z Analytics.

Wysyłanie danych tooyour źródło danych jest bardzo proste. 

1. (Jeden raz) Zdefiniuj schematu hello danych w źródle danych.
2. (Okresowo) Przekaż tooAzure magazynu danych, a przesadzamy toonotify interfejsu API REST hello które czeka na wprowadzanie nowych danych. W ciągu kilku minut hello dane są dostępne dla kwerendy w module analiz.

Hello częstotliwość przekazywania hello jest zdefiniowane przez użytkownika i tempa chcesz Twojej toobe danych jest niedostępne dla zapytań. Jest bardziej wydajne danych tooupload w większych fragmentów, ale nie większą niż 1GB.

> [!NOTE]
> *Uzyskano wiele tooanalyze źródeł danych?* [*Należy rozważyć użycie* logstash *tooship dane do usługi Application Insights.*](https://github.com/Microsoft/logstash-output-application-insights)
> 

## <a name="before-you-start"></a>Przed rozpoczęciem

Potrzebne elementy:

1. Zasób usługi Application Insights w Microsoft Azure.

 * Jeśli chcesz tooanalyze danych niezależnie od innych telemetrii [utworzyć nowy zasób usługi Application Insights](app-insights-create-new-resource.md).
 * Sprzęganie lub porównywanie danych za pomocą dane telemetryczne z aplikacji, która jest już skonfigurowane przy użyciu usługi Application Insights, można użyć hello zasobów dla danej aplikacji.
 * Współautor lub właściciela zasobu toothat dostępu.
 
2. Magazyn Azure. Przekaż tooAzure magazynu, a Analytics pobiera dane z tego miejsca. 

 * Zaleca się tworzenie konta magazynu dedykowane dla obiektów blob. Jeżeli obiektów blob są współużytkowane z innymi procesami, trwa dłużej naszych tooread procesy obiektów blob.


## <a name="define-your-schema"></a>Definiowania schematu

Przed importowaniem danych, należy zdefiniować *źródła danych* określającej schematu hello danych.
Może zawierać maksymalnie too50 źródeł danych w pojedynczy zasób usługi Application Insights

1. Uruchom Kreatora źródła danych hello. Użyj przycisku "Dodaj nowe źródło danych". Alternatywnie — kliknij przycisk Ustawienia w prawym górnym rogu i wybierz w menu rozwijanym "Źródła danych".

    ![Dodaj nowe źródło danych](./media/app-insights-analytics-import/add-new-data-source.png)

    Podaj nazwę dla nowego źródła danych.

2. Definiowanie formatu hello plików, które możesz przekazać.

    Można ręcznie zdefiniować hello format lub Przekaż plik przykładowy.

    Pierwszy wiersz hello próbki hello hello danych jest w formacie CSV, może być nagłówki kolumn. Można zmienić nazwy pól hello w następnym kroku hello.

    przykład Witaj powinna zawierać co najmniej 10 wierszy lub rekordów danych.

    Nazwy kolumn lub pole ma alfanumerycznych nazw (bez spacji i znaków interpunkcyjnych).

    ![Przekaż plik przykładowy](./media/app-insights-analytics-import/sample-data-file.png)


3. Otrzymano schemat hello przeglądu hello kreatora. Jeśli typy hello z próbki go wywnioskować, może być konieczne tooadjust typy hello wywnioskować hello kolumn.

    ![Przejrzyj hello wywnioskować schematu](./media/app-insights-analytics-import/data-source-review-schema.png)

 * (opcjonalnie) Przekaż definicji schematu. Zobacz hello format poniżej.

 * Wybierz sygnatury czasowej. Wszystkie dane w module analiz musi mieć pola sygnatury czasowej. Musi mieć typ `datetime`, ale nie ma toobe o nazwie "timestamp". Jeśli dane mają kolumny zawierającej daty i godziny w formacie ISO, wybierz tę opcję, jako hello kolumny znaczników czasu. W przeciwnym razie wybierz pozycję "jako dane dostarczone", a proces importowania hello doda pola sygnatury czasowej.

5. Utwórz źródło danych hello.

### <a name="schema-definition-file-format"></a>Format pliku definicji schematu

Zamiast edycji hello schematu w interfejsie użytkownika, można załadować definicji schematu hello z pliku. format definicji schematu Hello jest następujący: 

Format rozdzielanego 
```
[ 
    {"location": "0", "name": "RequestName", "type": "string"}, 
    {"location": "1", "name": "timestamp", "type": "datetime"}, 
    {"location": "2", "name": "IPAddress", "type": "string"} 
] 
```

JSON format 
```
[ 
    {"location": "$.name", "name": "name", "type": "string"}, 
    {"location": "$.alias", "name": "alias", "type": "string"}, 
    {"location": "$.room", "name": "room", "type": "long"} 
]
```
 
Każda kolumna jest identyfikowany przez hello lokalizację, nazwy i typu. 

* Lokalizacja — pliku rozdzielanego go sformatować jest pozycja hello wartości hello zamapowane. JSON format jest jpath hello hello mapowane klucza.
* Nazwa — Witaj wyświetlana nazwa kolumny hello.
* Typ — typ danych hello tej kolumny.
 
W przypadku użyto przykładowych danych i rozdzielana format pliku, definicji schematu hello należy mapować wszystkie kolumny i dodać nowe kolumny na końcu hello. 

JSON umożliwia mapowania częściowe hello danych, w związku z tym hello definicji schematu formatu JSON nie ma toomap każdego klucza, który znajduje się w przykładowych danych. Można również mapować kolumn, które nie są częścią hello przykładowych danych. 

## <a name="import-data"></a>Importowanie danych

tooimport danych, przekaż go tooAzure magazynu lub Utwórz klucz dostępu dla niego, a następnie dokonaj wywołania interfejsu API REST.

![Dodaj nowe źródło danych](./media/app-insights-analytics-import/analytics-upload-process.png)

Wykonaj powitania po procesie ręcznie lub skonfigurować toodo systemu go w regularnych odstępach czasu. Należy toofollow te kroki dla każdego bloku danych ma tooimport.

1. Przekazywanie danych hello zbyt[magazynu obiektów blob Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md). 

 * Obiekty BLOB może być dowolnej wielkości zapasowej too1GB jako nieskompresowane. Duże obiekty BLOB setek MB idealnie nadają się z punktu widzenia wydajności.
 * Można skompresować je z Gzip tooimprove przekazywania czas i czas oczekiwania na powitania toobe danych jest dostępne dla zapytania. Użyj hello `.gz` rozszerzenie nazwy pliku.
 * W tym celu wywołania tooavoid z różnych usług spowolnienia jest najlepszym toouse oddzielnego konta magazynu.
 * Podczas wysyłania danych w wysokiej częstotliwości, co kilka sekund, zalecane jest toouse więcej niż jedno konto magazynu, ze względu na wydajność.

 
2. [Utwórz klucz sygnatura dostępu współdzielonego dla obiekt blob hello](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md). klucz Hello powinny mieć okres ważności jeden dzień i zapewniają dostęp do odczytu.
3. Należy toonotify wywołania REST usługi Application Insights, która oczekuje na dane.

 * Punkt końcowy:`https://dc.services.visualstudio.com/v2/track`
 * Metoda HTTP: POST
 * Ładunek:

```JSON

    {
       "data": {
            "baseType":"OpenSchemaData",
            "baseData":{
               "ver":"2",
               "blobSasUri":"<Blob URI with Shared Access Key>",
               "sourceName":"<Schema ID>",
               "sourceVersion":"1.0"
             }
       },
       "ver":1,
       "name":"Microsoft.ApplicationInsights.OpenSchema",
       "time":"<DateTime>",
       "iKey":"<instrumentation key>"
    }
```

symbole zastępcze Hello to:

* `Blob URI with Shared Access Key`: Otrzymujesz to z procedury hello do tworzenia kluczy. Jest toohello określonego obiektu blob.
* `Schema ID`: hello generowane dla określonych schemat Identyfikatora schematu. Witaj danych w tym obiekcie blob powinna być zgodna toohello schematu.
* `DateTime`: hello czas na powitania, które zostało przesłane żądanie, UTC. Możemy zaakceptować te formaty: ISO8601 (takich jak "2016-01-01-13:45:01"); Rfc822 ("śro, 14 gru 16 14:57:01 + 0000"); RFC850 ("Środa, 16-14-gru UTC 14:57:00"); RFC1123 ("śro 14 gru 2016 14:57:00 + 0000").
* `Instrumentation key`zasobu usługi Application Insights.

Witaj dane są dostępne w module analiz po kilku minutach.

## <a name="error-responses"></a>Błąd odpowiedzi

* **Nieprawidłowe żądanie 400**: wskazuje, że hello ładunku żądania jest nieprawidłowy. Sprawdzanie:
 * Instrumentacja poprawny klucz.
 * Wartość czas ważności. Należy go hello czasu w formacie UTC.
 * JSON zdarzenia hello zgodne toohello schematu.
* **403 Zabroniony**: hello obiektu blob zostało wysłane nie jest dostępny. Upewnij się, że hello udostępniony klucz dostępu jest prawidłowa i nie wygasł.
* **Nie można odnaleźć 404**:
 * Witaj obiektu blob nie istnieje.
 * Hello sourceId jest nieprawidłowy.

Bardziej szczegółowe informacje są dostępne w komunikacie o błędzie odpowiedzi hello.


## <a name="sample-code"></a>Przykładowy kod

Ten kod zawiera hello [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) pakietu NuGet.

### <a name="classes"></a>Klasy

```C#
namespace IngestionClient 
{ 
    using System; 
    using Newtonsoft.Json; 

    public class AnalyticsDataSourceIngestionRequest 
    { 
        #region Members 
        private const string BaseDataRequiredVersion = "2"; 
        private const string RequestName = "Microsoft.ApplicationInsights.OpenSchema"; 
        #endregion Members 

        public AnalyticsDataSourceIngestionRequest(string ikey, string schemaId, string blobSasUri, int version = 1) 
        { 
            Ver = version; 
            IKey = ikey; 
            Data = new Data 
            { 
                BaseData = new BaseData 
                { 
                    Ver = BaseDataRequiredVersion, 
                    BlobSasUri = blobSasUri, 
                    SourceName = schemaId, 
                    SourceVersion = version.ToString() 
                } 
            }; 
        } 


        [JsonProperty("data")] 
        public Data Data { get; set; } 

        [JsonProperty("ver")] 
        public int Ver { get; set; } 

        [JsonProperty("name")] 
        public string Name { get { return RequestName; } } 

        [JsonProperty("time")] 
        public DateTime Time { get { return DateTime.UtcNow; } } 

        [JsonProperty("iKey")] 
        public string IKey { get; set; } 
    } 

    #region Internal Classes 

    public class Data 
    { 
        private const string DataBaseType = "OpenSchemaData"; 

        [JsonProperty("baseType")] 
        public string BaseType 
        { 
            get { return DataBaseType; } 
        } 

        [JsonProperty("baseData")] 
        public BaseData BaseData { get; set; } 
    } 


    public class BaseData 
    { 
        [JsonProperty("ver")] 
        public string Ver { get; set; } 

        [JsonProperty("blobSasUri")] 
        public string BlobSasUri { get; set; } 

        [JsonProperty("sourceName")] 
        public string SourceName { get; set; } 

        [JsonProperty("sourceVersion")] 
        public string SourceVersion { get; set; } 
    } 

    #endregion Internal Classes 
} 


namespace IngestionClient 
{ 
    using System; 
    using System.IO; 
    using System.Net; 
    using System.Text; 
    using System.Threading.Tasks; 
    using Newtonsoft.Json; 

    public class AnalyticsDataSourceClient 
    { 
        #region Members 
        private readonly Uri endpoint = new Uri("https://dc.services.visualstudio.com/v2/track"); 
        private const string RequestContentType = "application/json; charset=UTF-8"; 
        private const string RequestAccess = "application/json"; 
        #endregion Members 

        #region Public 

        public async Task<bool> RequestBlobIngestion(AnalyticsDataSourceIngestionRequest ingestionRequest) 
        { 
            HttpWebRequest request = WebRequest.CreateHttp(endpoint); 
            request.Method = WebRequestMethods.Http.Post; 
            request.ContentType = RequestContentType; 
            request.Accept = RequestAccess; 

            string notificationJson = Serialize(ingestionRequest); 
            byte[] notificationBytes = GetContentBytes(notificationJson); 
            request.ContentLength = notificationBytes.Length; 

            Stream requestStream = request.GetRequestStream(); 
            requestStream.Write(notificationBytes, 0, notificationBytes.Length); 
            requestStream.Close(); 

            try 
            { 
                using (var response = (HttpWebResponse)await request.GetResponseAsync())
                {
                    return response.StatusCode == HttpStatusCode.OK;
                }
            } 
            catch (WebException e) 
            { 
                HttpWebResponse httpResponse = e.Response as HttpWebResponse; 
                if (httpResponse != null) 
                { 
                    Console.WriteLine( 
                        "Ingestion request failed with status code: {0}. Error: {1}", 
                        httpResponse.StatusCode, 
                        httpResponse.StatusDescription); 
                    return false; 
                }
                throw; 
            } 
        } 
        #endregion Public 

        #region Private 
        private byte[] GetContentBytes(string content) 
        { 
            return Encoding.UTF8.GetBytes(content);
        } 


        private string Serialize(AnalyticsDataSourceIngestionRequest ingestionRequest) 
        { 
            return JsonConvert.SerializeObject(ingestionRequest); 
        } 
        #endregion Private 
    } 
} 
```

### <a name="ingest-data"></a>Pobieranie danych

Użyj tego kodu dla każdego obiektu blob. 

```C#
   AnalyticsDataSourceClient client = new AnalyticsDataSourceClient(); 

   var ingestionRequest = new AnalyticsDataSourceIngestionRequest("iKey", "sourceId", "blobUrlWithSas"); 

   bool success = await client.RequestBlobIngestion(ingestionRequest);
```

## <a name="next-steps"></a>Następne kroki

* [Samouczek hello język zapytań usługi Analiza dzienników](app-insights-analytics-tour.md)
* [Użyj *Logstash* toosend tooApplication danych usługi Insights](https://github.com/Microsoft/logstash-output-application-insights)
