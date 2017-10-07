---
title: "aaaLog API modułów zbierających dane HTTP Analytics | Dokumentacja firmy Microsoft"
description: "Za pomocą hello interfejsu API modułów zbierających dane dziennika Analytics HTTP tooadd POST JSON danych toohello analizy dzienników repozytorium za pomocą dowolnego klienta, który można wywołać hello interfejsu API REST. W tym artykule opisano sposób toouse hello interfejsu API i zawiera przykłady toopublish danych przy użyciu różnych języków programowania."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: 
ms.assetid: a831fd90-3f55-423b-8b20-ccbaaac2ca75
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: bwren
ms.openlocfilehash: c2921082831c49da764d946ac9c4fab975a38185
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="send-data-toolog-analytics-with-hello-http-data-collector-api"></a>Wysyłanie danych tooLog Analytics z hello interfejsu API modułów zbierających dane HTTP
W tym artykule opisano, jak toouse hello interfejsu API modułów zbierających dane HTTP toosend danych tooLog Analytics z klienta interfejsu API REST.  Opisuje jak tooformat danych zbieranych przez skrypt lub aplikację, dołączyć go w żądaniu i mieć tego żądania uprawnień przez analizy dzienników.  Przykłady są dostępne dla programu PowerShell, C# i Python.

## <a name="concepts"></a>Pojęcia
Możesz użyć hello interfejsu API modułów zbierających dane HTTP toosend danych tooLog Analytics za pomocą dowolnego klienta, który można wywołać interfejsu API REST.  Może to być element runbook automatyzacji Azure, która gromadzi zarządzania danych z platformy Azure lub innej chmurze lub może być system zarządzania alternatywnego, który używa tooconsolidate analizy dzienników i analizowania danych.

Wszystkie dane w repozytorium analizy dzienników hello są przechowywane jako rekord typu określonego rekordu.  Twoje dane toosend toohello interfejsu API modułów zbierających dane HTTP formacie wielu rekordów w formacie JSON.  Podczas przesyłania danych hello pojedynczego rekordu jest tworzony w repozytorium powitania dla każdego rekordu w ładunku żądania hello.


![Omówienie modułów zbierających dane HTTP](media/log-analytics-data-collector-api/overview.png)



## <a name="create-a-request"></a>Utwórz żądanie
Moduł zbierający dane hello HTTP toouse interfejsu API, Utwórz żądanie POST zawiera toosend danych hello w JavaScript Object Notation (JSON).  Witaj trzech kolejnych tabel listy hello atrybutów, które są wymagane dla każdego żądania. Opisano każdy atrybut bardziej szczegółowo w dalszej części artykułu hello.

### <a name="request-uri"></a>Identyfikator URI żądania
| Atrybut | Właściwość |
|:--- |:--- |
| Metoda |POST |
| IDENTYFIKATOR URI |https://\<CustomerId\>.ods.opinsights.azure.com/api/logs?api-version=2016-04-01 |
| Typ zawartości |application/json |

### <a name="request-uri-parameters"></a>Parametry identyfikatora URI żądania
| Parametr | Opis |
|:--- |:--- |
| CustomerID |Witaj Unikatowy identyfikator dla obszaru roboczego programu Microsoft Operations Management Suite hello. |
| Zasób |Nazwa zasobu Hello interfejsu API: / api/logs. |
| Wersja interfejsu API |Wersja Hello toouse hello interfejsu API z tym żądaniem. Obecnie jest 2016-04-01. |

### <a name="request-headers"></a>Nagłówki żądania
| Nagłówek | Opis |
|:--- |:--- |
| Autoryzacja |Witaj autoryzacji podpisu. W dalszej części artykułu hello możesz przeczytać temat toocreate SHA256 HMAC nagłówka. |
| Typ dziennika |Określ typ rekordu hello danych hello jest przesyłane. Typ dziennika hello obsługuje obecnie tylko znaki alfanumeryczne. Nie obsługuje wartości numeryczne i znaki specjalne. |
| x-ms-date |Data Hello przetworzono Żądanie hello w formacie RFC 1123. |
| czas wygenerowany — pola |Hello nazwę pola danych hello zawiera sygnaturę czasową hello hello elementu danych. Jeśli określisz pola, a następnie jego zawartość jest używana dla **TimeGenerated**. Jeśli to pole nie jest określony, domyślnie dla hello **TimeGenerated** jest czas hello tego hello jest pozyskanych wiadomości. Witaj zawartość pola wiadomość hello należy stosować hello ISO 8601 w formacie RRRR-MM-Ddtgg. |

## <a name="authorization"></a>Autoryzacja
Wszelkie toohello żądania interfejsu API modułów zbierających dane dziennika Analytics HTTP musi zawierać nagłówek uwierzytelnienia. tooauthenticate żądanie, musisz zalogować się Żądanie hello hello podstawowego lub hello dodatkowy klucz dla obszaru roboczego hello, w której wysłano żądanie hello. Następnie przekaż tego podpisu, jako część żądania hello.   

Oto hello format nagłówka autoryzacji hello:

```
Authorization: SharedKey <WorkspaceID>:<Signature>
```

*WorkspaceID* jest unikatowy identyfikator obszaru roboczego usługi Operations Management Suite hello hello. *Podpis* jest [Hash-based kodu (metoda HMAC Message Authentication)](https://msdn.microsoft.com/library/system.security.cryptography.hmacsha256.aspx) jest utworzone na podstawie żądania hello i następnie obliczane przy użyciu hello [algorytm SHA256](https://msdn.microsoft.com/library/system.security.cryptography.sha256.aspx). Następnie należy kodować je przy użyciu kodowania Base64.

Użyj tego formatu hello tooencode **SharedKey** podpisu ciągu:

```
StringToSign = VERB + "\n" +
                  Content-Length + "\n" +
               Content-Type + "\n" +
                  x-ms-date + "\n" +
                  "/api/logs";
```

Oto przykład ciągu podpisu:

```
POST\n1024\napplication/json\nx-ms-date:Mon, 04 Apr 2016 08:00:00 GMT\n/api/logs
```

Jeśli masz ciąg podpisu hello, kodować je przy użyciu hello Algorytm HMAC SHA256 na powitania ciąg algorytmem UTF-8, a następnie kodowanie hello wynik w postaci Base64. Użyj następującego formatu:

```
Signature=Base64(HMAC-SHA256(UTF8(StringToSign)))
```

Witaj w kolejnych sekcjach hello mają przykładowy kod toohelp utworzyć nagłówek autoryzacji.

## <a name="request-body"></a>Treść żądania
Witaj treść wiadomości powitania musi być w formacie JSON. Musi zawierać co najmniej jeden rekord z pary nazw i wartości właściwości hello w następującym formacie:

```
{
"property1": "value1",
" property 2": "value2"
" property 3": "value3",
" property 4": "value4"
}
```

Partii z wielu rekordów razem w jednym żądaniu, za pomocą hello zgodny z formatem. Wszystkie rekordy hello musi być hello rekordów samego typu.

```
{
"property1": "value1",
" property 2": "value2"
" property 3": "value3",
" property 4": "value4"
},
{
"property1": "value1",
" property 2": "value2"
" property 3": "value3",
" property 4": "value4"
}
```

## <a name="record-type-and-properties"></a>Typ rekordu i właściwości
Typ niestandardowy rekord należy zdefiniować podczas przesyłania danych za pośrednictwem hello interfejsu API modułów zbierających dane dziennika Analytics HTTP. Obecnie nie można zapisać danych tooexisting typy rekordów, które zostały utworzone przez inne typy danych i rozwiązań. Analiza dzienników odczytuje hello przychodzących danych, a następnie tworzy właściwości, które są zgodne z typami danych hello hello wartości, które należy wprowadzić.

Każdy toohello żądanie musi zawierać interfejs API analizy dziennika **typ dziennika** nagłówek o nazwie hello hello typu rekordu. sufiks Hello **_CL** jest nazwą automatycznie dołączany toohello wprowadź toodistinguish ona z dziennika inne typy jako dziennik niestandardowy. Na przykład, jeśli wprowadzona nazwa hello **MyNewRecordType**, analizy dzienników tworzy rekord typu hello **MyNewRecordType_CL**. Pomaga to zapewnić, że nie występują żadne konflikty między nazwami utworzonych przez użytkownika typu i te w obecne lub przyszłe rozwiązania firmy Microsoft.

Typ danych właściwości tooidentify, analizy dzienników dodaje sufiks nazwy właściwości toohello. Jeśli jakaś właściwość zawiera wartość null, właściwość hello jest niedostępna w tym rekordzie. Poniższa tabela zawiera typ danych właściwości hello i odpowiedniego sufiksu:

| Typ danych właściwości | Sufiks |
|:--- |:--- |
| Ciąg |_s |
| Wartość logiczna |_b |
| O podwójnej precyzji |_d |
| Data i godzina |_t — |
| IDENTYFIKATOR GUID |_g |

Typ danych Hello, który używa analizy dzienników dla każdej właściwości zależy od tego, czy typ rekordu hello hello nowy rekord już istnieje.

* Jeśli nie istnieje typ rekordu hello, analizy dzienników tworzy nową. Analiza dzienników używa typu JSON hello wnioskowania typu danych hello toodetermine dla każdej właściwości w nowym rekordzie hello.
* Jeśli istnieje typ rekordu hello, analizy dzienników prób toocreate nowy rekord na podstawie istniejącej właściwości. Jeśli hello typ danych właściwości w hello nowy rekord nie odpowiada i nie może być skonwertowany toohello istniejący typ lub jeśli hello rekord zawiera właściwość, która nie istnieje, analizy dzienników tworzy nową właściwość, która ma hello odpowiedniego sufiksu.

Na przykład utworzyć rekord z trzech właściwości tego wpisu przesyłania **number_d**, **boolean_b**, i **string_s**:

![Przykładowy rekord 1](media/log-analytics-data-collector-api/record-01.png)

Jeśli tego wpisu dalej, następnie przesłane ze wszystkich wartości w formacie ciągów, hello właściwości nie może zmienić. Te wartości mogą być przekonwertowana tooexisting typów danych:

![Przykładowy rekord 2](media/log-analytics-data-collector-api/record-02.png)

Ale jeśli wprowadzono następnie tego przesłania dalej, analizy dzienników utworzyć hello nowe właściwości **boolean_d** i **string_d**. Nie można przekonwertować wartości:

![Przykładowy rekord 3](media/log-analytics-data-collector-api/record-03.png)

Jeśli następnie przesłane powitania od wejścia, przed utworzeniem typu rekordu hello, analizy dzienników utworzyć rekord z trzech właściwości **liczba_s**, **boolean_s**, i **string_s**. W tym wpisie wartości początkowej hello jest sformatowany jako ciąg:

![Przykładowy rekord 4](media/log-analytics-data-collector-api/record-04.png)

## <a name="data-limits"></a>Limity danych
Istnieją pewne ograniczenia wokół danych hello zaksięgowany toohello dane analizy dziennika kolekcji interfejsu API.

* Maksymalnie 30 MB na post tooLog interfejsu API modułów zbierających dane analizy. Jest to limit rozmiaru dla pojedynczego żądania post. Jeśli hello dane z pojedynczego post, która przekracza 30 MB, należy rozdzielić hello fragmentów danych w górę toosmaller o rozmiarze i wyślij je jednocześnie.
* Maksymalny limit 32 KB wartości pól. Jeśli wartość pola hello jest większa niż 32 KB, zostanie obcięta hello danych.
* Zalecana maksymalna liczba pól dla danego typu jest 50. Jest to limit praktyczne doświadczenie użyteczność i wyszukiwania.  

## <a name="return-codes"></a>Kody powrotne
Kod stanu HTTP 200 Hello oznacza, że otrzymano Żądanie hello do przetwarzania. Oznacza to, że hello została pomyślnie zakończona.

Poniższa tabela zawiera kompletny zestaw kodów stanu, które mogą zwracać usługi hello hello:

| Kod | Stan | Kod błędu: | Opis |
|:--- |:--- |:--- |:--- |
| 200 |OK | |pomyślnie zaakceptowano żądanie Hello. |
| 400 |Nieprawidłowe żądanie |InactiveCustomer |obszar roboczy Hello został zamknięty. |
| 400 |Nieprawidłowe żądanie |InvalidApiVersion |Określona wersja Hello interfejsu API nie został rozpoznany przez usługę hello. |
| 400 |Nieprawidłowe żądanie |InvalidCustomerId |Określony identyfikator obszaru roboczego Hello jest nieprawidłowy. |
| 400 |Nieprawidłowe żądanie |InvalidDataFormat |Przekazano nieprawidłowy JSON. treść odpowiedzi Hello może zawierać więcej informacji na temat sposobu tooresolve hello błędu. |
| 400 |Nieprawidłowe żądanie |InvalidLogType |Typ dziennika Hello określony zawartych w niej znaków specjalnych ani wartości numeryczne. |
| 400 |Nieprawidłowe żądanie |MissingApiVersion |wersja interfejsu API Hello nie została określona. |
| 400 |Nieprawidłowe żądanie |MissingContentType |nie określono Hello typu zawartości. |
| 400 |Nieprawidłowe żądanie |MissingLogType |Hello wymagany typ wartości dziennika nie został określony. |
| 400 |Nieprawidłowe żądanie |UnsupportedContentType |Typ zawartości Hello nie została ustawiona zbyt**application/json**. |
| 403 |Dostęp zabroniony |InvalidAuthorization |Usługa Hello nie tooauthenticate hello żądania. Sprawdź tego hello obszaru roboczego połączenia i identyfikator klucza są poprawne. |
| 404 |Nie można odnaleźć | | Podany adres URL hello jest niepoprawna albo hello żądania jest za duży. |
| 429 |Zbyt wiele żądań | | Usługa Hello występuje duża liczba dane z konta. Spróbuj ponownie później hello żądania. |
| 500 |Wewnętrzny błąd serwera |UnspecifiedError |Usługa Hello napotkał błąd wewnętrzny. Ponów żądanie hello. |
| 503 |Usługa jest niedostępna |ServiceUnavailable |Usługa Hello jest obecnie niedostępna tooreceive żądań. Ponów żądanie. |

## <a name="query-data"></a>Zapytania o dane
tooquery danych przesyłanych przez hello interfejsu API z modułu zbierającego dane HTTP Analytics dziennika, Wyszukaj rekordy z **typu** który jest taki sam toohello **LogType** wartość, która została określona, dołączony **_CL**. Na przykład jeśli użyto **MyCustomLog**, a następnie zwróci wszystkie rekordy z **typu = MyCustomLog_CL**.

>[!NOTE]
> Jeśli obszaru roboczego został uaktualniony toohello [języka zapytań nowe analizy dzienników](log-analytics-log-search-upgrade.md), następnie hello powyżej zapytania spowoduje zmianę następujących toohello.

> `MyCustomLog_CL`

## <a name="sample-requests"></a>Próbki żądań
W kolejnych sekcjach hello znajdują się przykłady tego, jak toosubmit toohello danych interfejsu API modułów zbierających dane dziennika Analytics HTTP przy użyciu różnych języków programowania.

Dla każdej próbki wykonaj te kroki tooset hello zmienne dla nagłówka autoryzacji hello:

1. W portalu usługi Operations Management Suite hello, wybierz hello **ustawienia** Kafelek, a następnie wybierz hello **połączonych źródeł** kartę.
2. toohello prawo **identyfikator obszaru roboczego**, wybierz ikonę kopiowania hello, a następnie wklej identyfikator hello jako wartość hello hello **identyfikator klienta** zmiennej.
3. toohello prawo **klucza podstawowego**, wybierz ikonę kopiowania hello, a następnie wklej identyfikator hello jako wartość hello hello **klucz wstępny** zmiennej.

Można również zmienić hello zmienne typu dziennika hello oraz dane JSON.

### <a name="powershell-sample"></a>Przykładowe programu PowerShell
```
# Replace with your Workspace ID
$CustomerId = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"  

# Replace with your Primary Key
$SharedKey = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"

# Specify hello name of hello record type that you'll be creating
$LogType = "MyRecordType"

# Specify a field with hello created time for hello records
$TimeStampField = "DateValue"


# Create two records with hello same set of properties toocreate
$json = @"
[{  "StringValue": "MyString1",
    "NumberValue": 42,
    "BooleanValue": true,
    "DateValue": "2016-05-12T20:00:00.625Z",
    "GUIDValue": "9909ED01-A74C-4874-8ABF-D2678E3AE23D"
},
{   "StringValue": "MyString2",
    "NumberValue": 43,
    "BooleanValue": false,
    "DateValue": "2016-05-12T20:00:00.625Z",
    "GUIDValue": "8809ED01-A74C-4874-8ABF-D2678E3AE23D"
}]
"@

# Create hello function toocreate hello authorization signature
Function Build-Signature ($customerId, $sharedKey, $date, $contentLength, $method, $contentType, $resource)
{
    $xHeaders = "x-ms-date:" + $date
    $stringToHash = $method + "`n" + $contentLength + "`n" + $contentType + "`n" + $xHeaders + "`n" + $resource

    $bytesToHash = [Text.Encoding]::UTF8.GetBytes($stringToHash)
    $keyBytes = [Convert]::FromBase64String($sharedKey)

    $sha256 = New-Object System.Security.Cryptography.HMACSHA256
    $sha256.Key = $keyBytes
    $calculatedHash = $sha256.ComputeHash($bytesToHash)
    $encodedHash = [Convert]::ToBase64String($calculatedHash)
    $authorization = 'SharedKey {0}:{1}' -f $customerId,$encodedHash
    return $authorization
}


# Create hello function toocreate and post hello request
Function Post-OMSData($customerId, $sharedKey, $body, $logType)
{
    $method = "POST"
    $contentType = "application/json"
    $resource = "/api/logs"
    $rfc1123date = [DateTime]::UtcNow.ToString("r")
    $contentLength = $body.Length
    $signature = Build-Signature `
        -customerId $customerId `
        -sharedKey $sharedKey `
        -date $rfc1123date `
        -contentLength $contentLength `
        -fileName $fileName `
        -method $method `
        -contentType $contentType `
        -resource $resource
    $uri = "https://" + $customerId + ".ods.opinsights.azure.com" + $resource + "?api-version=2016-04-01"

    $headers = @{
        "Authorization" = $signature;
        "Log-Type" = $logType;
        "x-ms-date" = $rfc1123date;
        "time-generated-field" = $TimeStampField;
    }

    $response = Invoke-WebRequest -Uri $uri -Method $method -ContentType $contentType -Headers $headers -Body $body -UseBasicParsing
    return $response.StatusCode

}

# Submit hello data toohello API endpoint
Post-OMSData -customerId $customerId -sharedKey $sharedKey -body ([System.Text.Encoding]::UTF8.GetBytes($json)) -logType $logType  
```

### <a name="c-sample"></a>Przykład w języku C#
```
using System;
using System.Net;
using System.Net.Http;
using System.Net.Http.Headers;
using System.Security.Cryptography;
using System.Text;
using System.Threading.Tasks;

namespace OIAPIExample
{
    class ApiExample
    {
        // An example JSON object, with key/value pairs
        static string json = @"[{""DemoField1"":""DemoValue1"",""DemoField2"":""DemoValue2""},{""DemoField3"":""DemoValue3"",""DemoField4"":""DemoValue4""}]";

        // Update customerId tooyour Operations Management Suite workspace ID
        static string customerId = "xxxxxxxx-xxx-xxx-xxx-xxxxxxxxxxxx";

        // For sharedKey, use either hello primary or hello secondary Connected Sources client authentication key   
        static string sharedKey = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx";

        // LogName is name of hello event type that is being submitted tooLog Analytics
        static string LogName = "DemoExample";

        // You can use an optional field toospecify hello timestamp from hello data. If hello time field is not specified, Log Analytics assumes hello time is hello message ingestion time
        static string TimeStampField = "";

        static void Main()
        {
            // Create a hash for hello API signature
            var datestring = DateTime.UtcNow.ToString("r");
            string stringToHash = "POST\n" + json.Length + "\napplication/json\n" + "x-ms-date:" + datestring + "\n/api/logs";
            string hashedString = BuildSignature(stringToHash, sharedKey);
            string signature = "SharedKey " + customerId + ":" + hashedString;

            PostData(signature, datestring, json);
        }

        // Build hello API signature
        public static string BuildSignature(string message, string secret)
        {
            var encoding = new System.Text.ASCIIEncoding();
            byte[] keyByte = Convert.FromBase64String(secret);
            byte[] messageBytes = encoding.GetBytes(message);
            using (var hmacsha256 = new HMACSHA256(keyByte))
            {
                byte[] hash = hmacsha256.ComputeHash(messageBytes);
                return Convert.ToBase64String(hash);
            }
        }

        // Send a request toohello POST API endpoint
        public static void PostData(string signature, string date, string json)
        {
            try
            {
                string url = "https://" + customerId + ".ods.opinsights.azure.com/api/logs?api-version=2016-04-01";

                System.Net.Http.HttpClient client = new System.Net.Http.HttpClient();
                client.DefaultRequestHeaders.Add("Accept", "application/json");
                client.DefaultRequestHeaders.Add("Log-Type", LogName);
                client.DefaultRequestHeaders.Add("Authorization", signature);
                client.DefaultRequestHeaders.Add("x-ms-date", date);
                client.DefaultRequestHeaders.Add("time-generated-field", TimeStampField);

                System.Net.Http.HttpContent httpContent = new StringContent(json, Encoding.UTF8);
                httpContent.Headers.ContentType = new MediaTypeHeaderValue("application/json");
                Task<System.Net.Http.HttpResponseMessage> response = client.PostAsync(new Uri(url), httpContent);

                System.Net.Http.HttpContent responseContent = response.Result.Content;
                string result = responseContent.ReadAsStringAsync().Result;
                Console.WriteLine("Return Result: " + result);
            }
            catch (Exception excep)
            {
                Console.WriteLine("API Post Exception: " + excep.Message);
            }
        }
    }
}

```

### <a name="python-sample"></a>Przykładowe Python
```
import json
import requests
import datetime
import hashlib
import hmac
import base64

# Update hello customer ID tooyour Operations Management Suite workspace ID
customer_id = 'xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx'

# For hello shared key, use either hello primary or hello secondary Connected Sources client authentication key   
shared_key = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"

# hello log type is hello name of hello event that is being submitted
log_type = 'WebMonitorTest'

# An example JSON web monitor object
json_data = [{
   "slot_ID": 12345,
    "ID": "5cdad72f-c848-4df0-8aaa-ffe033e75d57",
    "availability_Value": 100,
    "performance_Value": 6.954,
    "measurement_Name": "last_one_hour",
    "duration": 3600,
    "warning_Threshold": 0,
    "critical_Threshold": 0,
    "IsActive": "true"
},
{   
    "slot_ID": 67890,
    "ID": "b6bee458-fb65-492e-996d-61c4d7fbb942",
    "availability_Value": 100,
    "performance_Value": 3.379,
    "measurement_Name": "last_one_hour",
    "duration": 3600,
    "warning_Threshold": 0,
    "critical_Threshold": 0,
    "IsActive": "false"
}]
body = json.dumps(json_data)

#####################
######Functions######  
#####################

# Build hello API signature
def build_signature(customer_id, shared_key, date, content_length, method, content_type, resource):
    x_headers = 'x-ms-date:' + date
    string_to_hash = method + "\n" + str(content_length) + "\n" + content_type + "\n" + x_headers + "\n" + resource
    bytes_to_hash = bytes(string_to_hash).encode('utf-8')  
    decoded_key = base64.b64decode(shared_key)
    encoded_hash = base64.b64encode(hmac.new(decoded_key, bytes_to_hash, digestmod=hashlib.sha256).digest())
    authorization = "SharedKey {}:{}".format(customer_id,encoded_hash)
    return authorization

# Build and send a request toohello POST API
def post_data(customer_id, shared_key, body, log_type):
    method = 'POST'
    content_type = 'application/json'
    resource = '/api/logs'
    rfc1123date = datetime.datetime.utcnow().strftime('%a, %d %b %Y %H:%M:%S GMT')
    content_length = len(body)
    signature = build_signature(customer_id, shared_key, rfc1123date, content_length, method, content_type, resource)
    uri = 'https://' + customer_id + '.ods.opinsights.azure.com' + resource + '?api-version=2016-04-01'

    headers = {
        'content-type': content_type,
        'Authorization': signature,
        'Log-Type': log_type,
        'x-ms-date': rfc1123date
    }

    response = requests.post(uri,data=body, headers=headers)
    if (response.status_code >= 200 and response.status_code <= 299):
        print 'Accepted'
    else:
        print "Response code: {}".format(response.status_code)

post_data(customer_id, shared_key, body, log_type)
```

## <a name="next-steps"></a>Następne kroki
- Użyj hello [interfejs API dziennika wyszukiwania](log-analytics-log-search-api.md) tooretrieve danych z hello analizy dzienników repozytorium.
