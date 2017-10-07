---
title: "Witaj aaaUnderstand język zapytań Centrum IoT Azure | Dokumentacja firmy Microsoft"
description: "Przewodnik dewelopera — opis hello Centrum IoT przypominającego SQL zapytań języka używany tooretrieve informacji na temat zadań z Centrum IoT i twins urządzenia."
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: 851a9ed3-b69e-422e-8a5d-1d79f91ddf15
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/17
ms.author: elioda
ms.openlocfilehash: 01a7c8ffdf44c6c27b834739d02c8fef1dd3d3fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="reference---iot-hub-query-language-for-device-twins-jobs-and-message-routing"></a>Odwołanie - Centrum IoT zapytania języka twins urządzenia, zadania i rozsyłania wiadomości

Centrum IoT zapewnia informacje tooretrieve zaawansowanych języka przypominającego SQL dotyczące [twins urządzenia] [ lnk-twins] i [zadania][lnk-jobs]i [rozsyłania wiadomości][lnk-devguide-messaging-routes]. W tym artykule przedstawiono:

* Wprowadzenie toohello najważniejszych funkcji hello język zapytań Centrum IoT, i
* Witaj szczegółowy opis hello języka.

## <a name="get-started-with-device-twin-queries"></a>Wprowadzenie do kwerend dwie urządzenia
[Urządzenie twins] [ lnk-twins] może zawierać dowolne obiekty JSON jako znaczniki i właściwości. Centrum IoT umożliwia twins urządzenia tooquery jako pojedynczego dokumentu JSON zawierający wszystkie informacje dwie urządzenia.
Przykładowa, na przykład, że Twoje twins urządzenia Centrum IoT hello następujące struktury:

```json
{
    "deviceId": "myDeviceId",
    "etag": "AAAAAAAAAAc=",
    "tags": {
        "location": {
            "region": "US",
            "plant": "Redmond43"
        }
    },
    "properties": {
        "desired": {
            "telemetryConfig": {
                "configId": "db00ebf5-eeeb-42be-86a1-458cccb69e57",
                "sendFrequencyInSecs": 300
            },
            "$metadata": {
            ...
            },
            "$version": 4
        },
        "reported": {
            "connectivity": {
                "type": "cellular"
            },
            "telemetryConfig": {
                "configId": "db00ebf5-eeeb-42be-86a1-458cccb69e57",
                "sendFrequencyInSecs": 300,
                "status": "Success"
            },
            "$metadata": {
            ...
            },
            "$version": 7
        }
    }
}
```

Centrum IoT udostępnia hello urządzenia twins jako kolekcji dokumentów o nazwie **urządzeń**.
Dlatego hello następujące zapytanie pobiera hello cały zestaw twins urządzenia:

```sql
SELECT * FROM devices
```

> [!NOTE]
> [Zestawy Azure SDK IoT] [ lnk-hub-sdks] obsługuje stronicowania duże wyniki.

Centrum IoT umożliwia twins urządzenia tooretrieve filtrowanie z dowolnego warunków. Na przykład

```sql
SELECT * FROM devices
WHERE tags.location.region = 'US'
```

pobiera hello twins urządzenia z hello **location.region** znacznik ustawiony za**USA**.
Operatory logiczne i arytmetyczne porównania są obsługiwane również na przykład

```sql
SELECT * FROM devices
WHERE tags.location.region = 'US'
    AND properties.reported.telemetryConfig.sendFrequencyInSecs >= 60
```

pobiera wszystkie twins urządzenia znajdujące się w hello nam skonfigurowane toosend telemetrii mniej częściej niż co minutę. Dla wygody, jest również możliwe toouse tablicowych z hello **IN** i **nW** operatory (nie w). Na przykład

```sql
SELECT * FROM devices
WHERE properties.reported.connectivity IN ['wired', 'wifi']
```

pobiera wszystkie twins urządzenia, które zgłosił sieci Wi-Fi lub łączności przewodowej. Jego jest często konieczne tooidentify wszystkie twins urządzenia zawierające określoną właściwość. Centrum IoT obsługuje funkcję hello `is_defined()` w tym celu. Na przykład

```SQL
SELECT * FROM devices
WHERE is_defined(properties.reported.connectivity)
```

pobrać wszystkie twins urządzenia, które definiują hello `connectivity` zgłosił właściwości. Zobacz toohello [klauzuli WHERE] [ lnk-query-where] sekcję, aby hello pełną dokumentację hello możliwości filtrowania.

Grupowanie i agregacje są również obsługiwane. Na przykład

```sql
SELECT properties.reported.telemetryConfig.status AS status,
    COUNT() AS numberOfDevices
FROM devices
GROUP BY properties.reported.telemetryConfig.status
```

Zwraca liczby hello urządzeń hello każdy stan konfiguracji telemetrii.

```json
[
    {
        "numberOfDevices": 3,
        "status": "Success"
    },
    {
        "numberOfDevices": 2,
        "status": "Pending"
    },
    {
        "numberOfDevices": 1,
        "status": "Error"
    }
]
```

Witaj powyższy przykład ilustruje sytuację, w którym trzech urządzeń zgłoszonych Konfiguracja zakończyła się pomyślnie, nadal są dwa stosowania konfiguracji hello i jedną zgłosił błąd.

### <a name="c-example"></a>Przykład C#
funkcje kwerend Hello jest udostępniany przez hello [C# usługi SDK] [ lnk-hub-sdks] w hello **RegistryManager** klasy.
Oto przykład prostego zapytania:

```csharp
var query = registryManager.CreateQuery("SELECT * FROM devices", 100);
while (query.HasMoreResults)
{
    var page = await query.GetNextAsTwinAsync();
    foreach (var twin in page)
    {
        // do work on twin object
    }
}
```

Uwaga jak hello **zapytania** utworzeniu wystąpienia obiektu z rozmiarem strony (w górę too1000), a następnie wiele stron mogą być pobierane przez wywołanie hello **GetNextAsTwinAsync** metody wiele razy.
Uwaga obiektu zapytania hello udostępnia wiele **dalej\***, w zależności od opcji deserializacji hello wymagane przez zapytanie hello, takich jak obiekty dwie lub zadanie urządzeń lub zwykły toobe JSON, używane podczas projekcji.

### <a name="nodejs-example"></a>Przykład node.js
funkcje kwerend Hello jest udostępniany przez hello [usługi Azure IoT SDK dla środowiska Node.js] [ lnk-hub-sdks] w hello **rejestru** obiektu.
Oto przykład prostego zapytania:

```nodejs
var query = registry.createQuery('SELECT * FROM devices', 100);
var onResults = function(err, results) {
    if (err) {
        console.error('Failed toofetch hello results: ' + err.message);
    } else {
        // Do something with hello results
        results.forEach(function(twin) {
            console.log(twin.deviceId);
        });

        if (query.hasMoreResults) {
            query.nextAsTwin(onResults);
        }
    }
};
query.nextAsTwin(onResults);
```

Uwaga jak hello **zapytania** utworzeniu wystąpienia obiektu z rozmiarem strony (w górę too1000), a następnie wiele stron mogą być pobierane przez wywołanie hello **nextAsTwin** metody wiele razy.
Uwaga obiektu zapytania hello udostępnia wiele **dalej\***, w zależności od opcji deserializacji hello wymagane przez zapytanie hello, takich jak obiekty dwie lub zadanie urządzeń lub zwykły toobe JSON, używane podczas projekcji.

### <a name="limitations"></a>Ograniczenia
> [!IMPORTANT]
> Wyniki zapytania może mieć kilka minut opóźnienie w zakresie toohello ostatnie wartości twins urządzenia. Jeśli zapytanie twins poszczególne urządzenia według identyfikatora, jest zawsze preferowana toouse hello pobrać interfejsu API dwie urządzenia, które zawsze zawiera najnowsze wartości hello i ma wyższy ograniczenie.

Obecnie porównania są obsługiwane tylko między typy pierwotne (nie obiektów), na przykład `... WHERE properties.desired.config = properties.reported.config` jest obsługiwana tylko w przypadku pierwotnych wartości tych właściwości.

## <a name="get-started-with-jobs-queries"></a>Wprowadzenie do kwerend zadania
[Zadania] [ lnk-jobs] Podaj tooexecute sposób operacje na zestawy urządzeń. Dwie każdego urządzenia zawiera informacje hello hello zadań, które jest częścią kolekcji o nazwie **zadania**.
Logicznie,

```json
{
    "deviceId": "myDeviceId",
    "etag": "AAAAAAAAAAc=",
    "tags": {
        ...
    },
    "properties": {
        ...
    },
    "jobs": [
        {
            "deviceId": "myDeviceId",
            "jobId": "myJobId",
            "jobType": "scheduleTwinUpdate",
            "status": "completed",
            "startTimeUtc": "2016-09-29T18:18:52.7418462",
            "endTimeUtc": "2016-09-29T18:20:52.7418462",
            "createdDateTimeUtc": "2016-09-29T18:18:56.7787107Z",
            "lastUpdatedDateTimeUtc": "2016-09-29T18:18:56.8894408Z",
            "outcome": {
                "deviceMethodResponse": null
            }
        },
        ...
    ]
}
```

Ta kolekcja jest obecnie kolejność jako **devices.jobs** w hello język zapytań Centrum IoT.

> [!IMPORTANT]
> Obecnie właściwości zadania hello nigdy nie jest zwracana podczas wykonywania zapytania twins urządzenia (to znaczy zapytań, które zawiera "z urządzeń"). Będą one dostępne tylko bezpośrednio z zapytania przy użyciu `FROM devices.jobs`.
>
>

Na przykład tooget wszystkie zadania (ostatnich i zaplanowane) wpływających na jednym urządzeniu, można użyć hello następujące zapytania:

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.deviceId = 'myDeviceId'
```

Należy zwrócić uwagę, jak to zapytanie informuje o stanie specyficzne dla urządzenia hello (oraz prawdopodobnie odpowiedź metoda bezpośrednia hello) każde zadanie zwrócone.
Możliwe jest również możliwe toofilter z dowolnego warunków logicznych na wszystkie właściwości obiektu w hello **devices.jobs** kolekcji.
Na przykład hello następujące zapytania:

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.deviceId = 'myDeviceId'
    AND devices.jobs.jobType = 'scheduleTwinUpdate'
    AND devices.jobs.status = 'completed'
    AND devices.jobs.createdTimeUtc > '2016-09-01'
```

pobiera zakończone urządzenia dwie Aktualizacja zadania dla urządzenia **myDeviceId** utworzonych po wrześniu 2016 r.

Możliwe jest również możliwe tooretrieve hello na urządzenie wyniki jednego zadania.

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.jobId = 'myJobId'
```

### <a name="limitations"></a>Ograniczenia
Obecnie zapytanie na **devices.jobs** nie obsługują:

* Projekcji, w związku z tym tylko `SELECT *` jest możliwe.
* Warunki, które odwołują się dwie urządzenia toohello dodanie właściwości toojob (zobacz hello powyższej sekcji).
* Wykonywanie agregacji, takie jak liczba, avg, Grupuj według.

## <a name="get-started-with-device-to-cloud-message-routes-query-expressions"></a>Wprowadzenie do wyrażenia zapytania tras wiadomości urządzenia do chmury

Przy użyciu [trasy urządzenia do chmury][lnk-devguide-messaging-routes], można skonfigurować Centrum IoT urządzenia chmury toodispatch wiadomości punkty końcowe toodifferent oparte na wyrażeniach porównywany poszczególne wiadomości.

trasy Hello [warunku] [ lnk-query-expressions] używa hello tego samego języka zapytań Centrum IoT jako warunki w zapytaniach dwie i zadania. Warunki trasy są oceniane w nagłówkach wiadomości powitania oraz i treść. Routingu wyrażeniu zapytania może obejmować tylko nagłówki wiadomości, tylko treści wiadomości powitania, lub obie te nagłówki komunikatów, a treść komunikatu. Centrum IoT zakłada określonego schematu hello nagłówków i treści wiadomości w kolejności tooroute wiadomości i hello w następujących sekcjach opisano, co jest wymagane dla trasy tooproperly Centrum IoT:

### <a name="routing-on-message-headers"></a>Routing w nagłówkach wiadomości

Centrum IoT przyjmuje następujące reprezentacja JSON w nagłówkach wiadomości do rozsyłania wiadomości powitania:

```json
{
    "$messageId": "",
    "$enqueuedTime": "",
    "$to": "",
    "$expiryTimeUtc": "",
    "$correlationId": "",
    "$userId": "",
    "$ack": "",
    "$connectionDeviceId": "",
    "$connectionDeviceGenerationId": "",
    "$connectionAuthMethod": "",
    "$content-type": "",
    "$content-encoding": "",

    "userProperty1": "",
    "userProperty2": ""
}
```

Właściwości systemu wiadomości są poprzedzane prefiksem hello `'$'` symbolu.
Właściwości użytkownika są zawsze dostępne z jego nazwą. Jeśli nazwa właściwości użytkownika sytuacji toocoincide z właściwością systemu (takich jak `$to`), hello właściwości użytkownika zostaną pobrane z hello `$to` wyrażenia.
Zawsze dostęp do właściwości systemu hello za pomocą nawiasów `{}`: na przykład można użyć wyrażenia hello `{$to}` tooaccess hello właściwości systemu `to`. Nazwy właściwości w nawiasach kwadratowych zawsze pobierają hello odpowiadających im właściwości systemu.

Należy pamiętać, że nazwy właściwości bez uwzględniania wielkości liter.

> [!NOTE]
> Wszystkie właściwości wiadomości są ciągami. Właściwości systemu, zgodnie z opisem w hello [przewodnik dewelopera po][lnk-devguide-messaging-format], nie są obecnie dostępne toouse w zapytaniach.
>

Na przykład, jeśli używasz `messageType` właściwości, może być tooroute wszystkie dane telemetryczne tooone endpoint i wszystkie alerty tooanother endpoint. Można napisać powitania po wyrażeniu tooroute hello telemetrii:

```sql
messageType = 'telemetry'
```

I powitania po wystąpieniu komunikatów alertu o wyrażenie tooroute hello:

```sql
messageType = 'alert'
```

Wyrażenia logiczne i funkcje są również obsługiwane. Ta funkcja umożliwia toodistinguish między poziom ważności, na przykład:

```sql
messageType = 'alerts' AND as_number(severity) <= 2
```

Zobacz toohello [wyrażenie i warunki] [ lnk-query-expressions] sekcję, aby hello pełną listę obsługiwanych operatory i funkcje.

### <a name="routing-on-message-bodies"></a>Routing w treści wiadomości

Centrum IoT można kierować tylko oparte na treść komunikatu zawartość, jeśli treść wiadomości powitania jest poprawnie sformułowany JSON zakodowane w formacie UTF-8, UTF-16 lub UTF-32. Należy ustawić typ zawartości hello wiadomość hello zbyt`application/json` i hello zawartości kodowania tooone hello obsługiwane UTF kodowania w tooallow nagłówki wiadomość hello wiadomość hello tooroute Centrum IoT na podstawie hello treści zawartości. Jeśli jeden z nagłówków hello nie zostanie określony, Centrum IoT nie będzie próbował tooevaluate dowolne wyrażenie zapytania dotyczące treści hello przed wiadomość hello. Jeśli wiadomość nie jest komunikat JSON lub jeśli wiadomość hello nie określa hello typu zawartości i kodowania zawartości, może nadal używać rozsyłanie wiadomości powitania tooroute oparte na nagłówkach wiadomości powitania wiadomości.

Można użyć `$body` w wiadomości powitania tooroute hello zapytania wyrażenia. Proste treści odwołania, typu odwołania tablicy treści lub wiele odwołań treści można użyć w wyrażeniu zapytania hello. Wyrażenie zapytania można także połączyć treści odwołanie z odwołaniem nagłówka wiadomości. Na przykład następujące hello są wszystkie wyrażenia prawidłową kwerendę:

```sql
$body.message.Weather.Location.State = 'WA'
$body.Weather.HistoricalData[0].Month = 'Feb'
$body.Weather.Temperature = 50 AND $body.message.Weather.IsEnabled
length($body.Weather.Location.State) = 2
$body.Weather.Temperature = 50 AND Status = 'Active'
```

## <a name="basics-of-an-iot-hub-query"></a>Podstawowe informacje o kwerendzie Centrum IoT
Każdy Centrum IoT kwerenda składa się SELECT i klauzul FROM oraz opcjonalnie WHERE i GROUP BY klauzul. Każdy zapytania jest uruchamiane na kolekcji dokumentów JSON, na przykład twins urządzenia. Klauzula FROM Hello wskazuje toobe kolekcji dokumentów hello iterowane na (**urządzeń** lub **devices.jobs**). Następnie hello filtru, w których stosowane jest klauzula hello. Z agregacji, wyniki hello tego kroku są grupowane jako hello określony w klauzuli GROUP BY, i dla każdej grupy jest generowany wiersz jak określono w klauzuli SELECT hello.

```sql
SELECT <select_list>
FROM <from_specification>
[WHERE <filter_condition>]
[GROUP BY <group_specification>]
```

## <a name="from-clause"></a>Klauzula FROM
Witaj **z < from_specification >** klauzuli może przyjmować tylko dwie wartości: **z urządzeń**, tooquery twins urządzenia, lub **z devices.jobs**, tooquery zadania na urządzenie szczegółowe informacje.

## <a name="where-clause"></a>Klauzula WHERE
Witaj **gdzie < filter_condition >** klauzula jest opcjonalne. Określa jeden lub więcej czynników, że hello dokumentów JSON w kolekcji FROM hello muszą spełniać toobe wchodzącego w skład hello wynik. Należy ocenić dowolnych dokumentów JSON hello określone warunki zbyt "true" toobe zawarte w wyniku hello.

Witaj dozwolone warunki opisane w sekcji [wyrażeń i warunki][lnk-query-expressions].

## <a name="select-clause"></a>Klauzula SELECT
Klauzula SELECT Hello (**Wybierz < select_list >**) jest obowiązkowy i określa, jakie wartości są pobierane z hello zapytania. Określa ona toobe wartości JSON hello używane toogenerate nowych obiektów JSON.
Dla każdego elementu hello filtrowane (i opcjonalnie grupowanych) podzestaw kolekcji FROM hello, faza projekcji hello generuje nowy obiekt JSON, skonstruowany przy wartości hello określonych w klauzuli SELECT hello.

Gramatyki hello w klauzuli SELECT hello jest następujący:

```
SELECT [TOP <max number>] <projection list>

<projection_list> ::=
    '*'
    | <projection_element> AS alias [, <projection_element> AS alias]+

<projection_element> :==
    attribute_name
    | <projection_element> '.' attribute_name
    | <aggregate>

<aggregate> :==
    count()
    | avg(<projection_element>)
    | sum(<projection_element>)
    | min(<projection_element>)
    | max(<projection_element>)
```

gdzie **attribute_name** odwołuje się właściwość tooany hello dokumentu JSON w hello FROM kolekcji. Przykłady klauzule SELECT można znaleźć w hello [wprowadzenie do zapytań dwie urządzenia] [ lnk-query-getstarted] sekcji.

Obecnie wybór klauzule różni się od **wybierz \***  są obsługiwane tylko w zapytaniach agregacji w twins urządzenia.

## <a name="group-by-clause"></a>klauzula GROUP BY
Witaj **GROUP BY < group_specification >** klauzula jest opcjonalny krok, który mogą być wykonywane po filtr hello określony w hello klauzuli WHERE, a przed projekcji hello określonej w hello wybierz. Grup dokumentów na podstawie hello wartości atrybutu. Te grupy są używane toogenerate agregowane wartości określonych w klauzuli SELECT hello.

Przykładem zapytanie, używając GROUP BY jest:

```sql
SELECT properties.reported.telemetryConfig.status AS status,
    COUNT() AS numberOfDevices
FROM devices
GROUP BY properties.reported.telemetryConfig.status
```

Witaj posiadanie składnia GROUP BY jest:

```
GROUP BY <group_by_element>
<group_by_element> :==
    attribute_name
    | < group_by_element > '.' attribute_name
```

gdzie **attribute_name** odwołuje się właściwość tooany hello dokumentu JSON w hello FROM kolekcji.

Obecnie hello klauzuli GROUP BY jest obsługiwana tylko podczas wykonywania zapytania twins urządzenia.

## <a name="expressions-and-conditions"></a>Wyrażenia i warunki
Na wysokim poziomie *wyrażenie*:

* Oblicza tooan wystąpienia typu JSON (na przykład wartość logiczna, liczba, ciąg, tablicy lub obiektu), a
* Jest zdefiniowana przez manipulację danymi pochodzących z dokumentu JSON hello urządzenia oraz stałe za pomocą wbudowanych operatorów i funkcji.

*Warunki* są wyrażeń określających tooa typu Boolean. Wszystkie inne niż wartość logiczna stała **true** jest uznawany za **false** (w tym **null**, **Niezdefiniowany**, dowolnego wystąpienia obiektu ani tablicy wszelkie string i wyraźnie hello Boolean **false**).

Hello składnia wyrażeń jest następująca:

```
<expression> ::=
    <constant> |
    attribute_name |
    <function_call> |
    <expression> binary_operator <expression> |
    <create_array_expression> |
    '(' <expression> ')'

<function_call> ::=
    <function_name> '(' expression ')'

<constant> ::=
    <undefined_constant>
    | <null_constant>
    | <number_constant>
    | <string_constant>
    | <array_constant>

<undefined_constant> ::= undefined
<null_constant> ::= null
<number_constant> ::= decimal_literal | hexadecimal_literal
<string_constant> ::= string_literal
<array_constant> ::= '[' <constant> [, <constant>]+ ']'
```

Gdzie:

| Symbol | Definicja |
| --- | --- |
| attribute_name | Wszystkie właściwości dokumentu JSON hello na powitania **FROM** kolekcji. |
| binary_operator | Wszelkie operatora binarnego na liście hello [operatory](#operators) sekcji. |
| nazwa_funkcji| Dowolne funkcje wymienione w hello [funkcje](#functions) sekcji. |
| decimal_literal |Float, wyrażone w notacji dziesiętnej. |
| hexadecimal_literal |Liczba wyrażona przez ciąg hello '0 x' następuje ciąg cyfr szesnastkowych. |
| literał |Literały ciągu są reprezentowane przez sekwencję zero lub więcej znaków Unicode lub sekwencji unikowych ciągów Unicode. Literały ciągu są ujęte w apostrofy (apostrof: ") lub podwójne cudzysłowy (cudzysłów:"). Dozwolone specjalne: `\'`, `\"`, `\\`, `\uXXXX` znaków Unicode, zdefiniowane przez 4 cyfr szesnastkowych. |

### <a name="operators"></a>Operatory
obsługiwane są następujące operatory Hello:

| Rodziny | Operatory |
| --- | --- |
| Operacje arytmetyczne |+,-,*,/,% |
| Logiczne |I, LUB NIE |
| Porównanie |=, !=, <, >, <=, >=, <> |

### <a name="functions"></a>Funkcje
Podczas wykonywania zapytania zadania i twins hello obsługiwana tylko funkcja jest:

| Funkcja | Opis |
| -------- | ----------- |
| IS_DEFINED(Property) | Zwraca wartość Boolean wskazującą, czy właściwość hello zostanie przypisana wartość (w tym `null`). |

W warunkach tras następujące funkcje matematyczne hello są obsługiwane:

| Funkcja | Opis |
| -------- | ----------- |
| ABS(x) | Zwraca hello bezwzględną () wartości dodatniej hello określone wyrażenie liczbowe. |
| EXP(x) | Zwraca hello wykładniczej wartość hello określona wyrażenia liczbowego (e ^ x). |
| Power(x,y) | Zwraca hello wartość hello określone wyrażenie toohello określony zasilania (x ^ y).|
| SQUARE(x) | Zwraca hello kwadratowy z hello określono wartość liczbową. |
| CEILING(x) | Zwraca hello najmniejszą liczbę całkowitą większą niż lub równa, hello określonego wyrażenia liczbowego. |
| FLOOR(x) | Zwraca hello największa liczba całkowita mniejsza lub równa toohello określone wyrażenie liczbowe. |
| SIGN(x) | Zwraca hello plus (+ 1) (0), lub znakiem minus (-1) z hello określone wyrażenie liczbowe.|
| SQRT(x) | Zwraca hello kwadratowy z hello określono wartość liczbową. |

W warunkach trasy hello następującego typu sprawdzanie i rzutowanie funkcje są obsługiwane:

| Funkcja | Opis |
| -------- | ----------- |
| AS_NUMBER | Konwertuje liczbę tooa ciąg wejściowy hello. `noop`Jeśli dane wejściowe jest liczbą; `Undefined` czy ciąg reprezentuje liczbę.|
| IS_ARRAY — | Zwraca wartość logiczną wskazującą, czy typ hello hello określone wyrażenie jest tablicą. |
| IS_BOOL | Zwraca wartość logiczną wskazującą, czy typ hello hello określone wyrażenie jest wartością logiczną. |
| IS_DEFINED | Zwraca wartość Boolean wskazującą, czy właściwość hello zostanie przypisana wartość. |
| IS_NULL | Zwraca wartość logiczną wskazującą, czy typ hello hello określone wyrażenie ma wartość null. |
| IS_NUMBER | Zwraca wartość logiczną wskazującą, czy typ hello hello określone wyrażenie jest liczbą. |
| IS_OBJECT — | Zwraca wartość logiczną wskazującą, czy typ hello hello określone wyrażenie jest obiektem JSON. |
| IS_PRIMITIVE | Zwraca wartość logiczną wskazującą, czy określony typ hello hello wyrażenie jest typu pierwotnego (string, Boolean, liczbowego lub `null`). |
| IS_STRING | Zwraca wartość logiczną wskazującą, czy typ hello hello określone wyrażenie jest ciągiem. |

W warunkach tras obsługiwane są następujące funkcje ciąg hello:

| Funkcja | Opis |
| -------- | ----------- |
| CONCAT(x,...) | Zwraca ciąg, który jest wynikiem hello łączenie dwóch lub więcej wartości ciągu. |
| LENGTH(x) | Witaj zwraca liczbę znaków hello określone wyrażenie ciągu.|
| LOWER(x) | Zwraca wyrażenie ciągu po przekonwertowaniu toolowercase danych wielką literę. |
| UPPER(x) | Zwraca wyrażenie ciągu po przekonwertowaniu toouppercase danych małą literę. |
| SUBSTRING (ciąg, start [, długość]) | Zwraca część wyrażenia ciągu, zaczynając od hello określono znaku na pozycji liczony od zera i kontynuuje toohello określone długości lub toohello końca ciągu hello. |
| INDEX_OF (ciąg, fragment) | Zwraca hello uruchamianie pozycję pierwszego wystąpienia hello hello drugiego wyrażenia ciągu w obrębie hello pierwszy określonego wyrażenia ciągu lub wartość -1, jeśli nie zostanie znaleziony ciąg hello.|
| STARTS_WITH (x, y) | Zwraca wartość Boolean wskazującą, czy pierwsze wyrażenie ciąg hello rozpoczyna się od hello drugi. |
| ENDS_WITH (x, y) | Zwraca wartość Boolean wskazującą, czy pierwsze wyrażenie ciąg hello kończy hello drugi. |
| CONTAINS(x,y) | Zwraca wartość Boolean wskazującą, czy pierwsze wyrażenie ciąg hello drugi zawiera hello. |

## <a name="next-steps"></a>Następne kroki
Dowiedz się, jak tooexecute zapytania w aplikacjach za pomocą [Azure IoT SDK][lnk-hub-sdks].

[lnk-query-where]: iot-hub-devguide-query-language.md#where-clause
[lnk-query-expressions]: iot-hub-devguide-query-language.md#expressions-and-conditions
[lnk-query-getstarted]: iot-hub-devguide-query-language.md#get-started-with-device-twin-queries

[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-jobs]: iot-hub-devguide-jobs.md
[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
[lnk-devguide-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-devguide-messaging-routes]: iot-hub-devguide-messages-read-custom.md
[lnk-devguide-messaging-format]: iot-hub-devguide-messages-construct.md
[lnk-devguide-messaging-routes]: ./iot-hub-devguide-messages-read-custom.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
