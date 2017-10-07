---
title: "Funkcje zdefiniowane przez użytkownika Stream Analytics JavaScript aaaAzure | Dokumentacja firmy Microsoft"
description: "Wykonaj mechanika zaawansowanych zapytań z języka JavaScript funkcje zdefiniowane przez użytkownika"
keywords: "JavaScript, funkcje udf zdefiniowane przez użytkownika"
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 28eeb8f6437c23989e8887687b950361fed4414c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-stream-analytics-javascript-user-defined-functions"></a>Azure Stream Analytics JavaScript funkcje zdefiniowane przez użytkownika
Usługa Azure Stream Analytics obsługuje funkcje zdefiniowane przez użytkownika napisane w języku JavaScript. Z hello bogaty zestaw **ciąg**, **RegExp**, **matematyczne**, **tablicy**, i **data** metody który Udostępnia JavaScript, danych złożonych przekształceń zadania usługi analiza strumienia stają się łatwiejsze toocreate.

## <a name="javascript-user-defined-functions"></a>JavaScript — funkcje zdefiniowane przez użytkownika
Funkcje zdefiniowane przez użytkownika JavaScript obsługuje bezstanowych, tylko do obliczeń funkcje skalarne, które nie wymagają łączność zewnętrzną. Witaj zwracać wartość funkcji może być tylko wartość skalarną (jeden). Po dodaniu zadania JavaScript tooa funkcja zdefiniowana przez użytkownika funkcja hello dowolne miejsce w zapytaniu hello, takich jak wbudowanych funkcji skalarnej.

Poniżej przedstawiono kilka scenariuszy, w którym może być przydatne funkcje zdefiniowane przez użytkownika JavaScript:
* Analizowanie i operowanie nimi ciągów, które mają funkcji wyrażenie regularne, na przykład **Regexp_Replace()** i **Regexp_Extract()**
* Dekodowanie i kodowania danych, na przykład konwersja binarny szesnastkowy
* Wykonywanie obliczeń mathematic JavaScript **matematyczne** funkcji
* Wykonywanie operacji na tablicy jak sortowania, sprzężenia, Znajdź i wypełnienia

Poniżej przedstawiono niektóre czynności, które nie można wykonać przy użyciu funkcji zdefiniowanej przez użytkownika JavaScript w Stream Analytics:
* Wywołanie limit zewnętrzne punkty końcowe REST, na przykład wykonywania wstecznego wyszukiwania IP lub ściągania danych referencyjnych ze źródła zewnętrznego
* Przeprowadź niestandardowe zdarzenie format serializacji lub deserializacji w danych wejściowych/wyjściowych
* Tworzenie wartości zagregowanych niestandardowych

Mimo że funkcje takie jak **Date.GetDate()** lub **Math.random()** nie są blokowane w definicji funkcji hello, należy unikać używania ich. Te funkcje **nie** zwracany hello sam powoduje za każdym razem należy wywołać i hello usługi Azure Stream Analytics nie przechowuje dziennika wywołania funkcji i zwróciło wyników. Jeśli funkcja zwraca różne wyniki na powitania same zdarzenia, powtarzalność nie jest gwarantowana po ponownym uruchomieniu zadania przez Ciebie lub hello usługi Stream Analytics.

## <a name="add-a-javascript-user-defined-function-in-hello-azure-portal"></a>Dodawanie funkcji zdefiniowanej przez użytkownika JavaScript w hello portalu Azure
toocreate proste funkcji zdefiniowanej przez użytkownika JavaScript w obszarze na istniejące zadanie usługi Stream Analytics, wykonaj następujące kroki:

1.  W portalu Azure hello Znajdź zadania usługi analiza strumienia.
2.  W obszarze **TOPOLOGII zadania**, wybierz funkcji. Zostanie wyświetlona pusta lista funkcji.
3.  toocreate nowych funkcji zdefiniowanej przez użytkownika, wybierz **Dodaj**.
4.  Na powitania **nową funkcję** bloku dla **typu funkcji**, wybierz pozycję **JavaScript**. Domyślny szablon funkcji zostanie wyświetlony w edytorze hello.
5.  Dla hello **UDF alias**, wprowadź **hex2Int**i zmień implementację funkcji hello w następujący sposób:

    ```
    // Convert Hex value toointeger.
    function main(hexValue) {
        return parseInt(hexValue, 16);
    }
    ```

6.  Wybierz pozycję **Zapisz**. Funkcji pojawia się na liście hello funkcji.
7.  Wybierz nowe hello **hex2Int** funkcji i sprawdź hello definicji funkcji. Wszystkie funkcje mają **UDF** alias funkcja toohello dodany prefiks. Należy zbyt*zawierać prefiks hello* podczas wywołania funkcji hello w kwerendzie Stream Analytics. W takim przypadku należy wywołać **UDF.hex2Int**.

## <a name="call-a-javascript-user-defined-function-in-a-query"></a>Wywoływanie funkcji zdefiniowanej przez użytkownika JavaScript w kwerendzie

1. W hello zapytania edytora, w obszarze **TOPOLOGII zadania**, wybierz pozycję **zapytania**.
2.  Edytuj zapytanie, a następnie wywołać hello — funkcja zdefiniowana przez użytkownika, takie jak to:

    ```
    SELECT
        time,
        UDF.hex2Int(offset) AS IntOffset
    INTO
        output
    FROM
        InputStream
    ```

3.  tooupload hello przykładowy plik danych, kliknij prawym przyciskiem myszy hello zadania w danych wejściowych.
4.  tootest kwerendy, wybierz opcję **testu**.


## <a name="supported-javascript-objects"></a>Obsługiwane obiektów JavaScript
Funkcje zdefiniowane przez użytkownika JavaScript analiza strumienia Azure obsługuje standardowego, wbudowanego obiektów JavaScript. Aby uzyskać listę tych obiektów, zobacz [obiektów globalnych](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects).

### <a name="stream-analytics-and-javascript-type-conversion"></a>Konwersja typu Stream Analytics i języka JavaScript

Ma różnic w typach hello, które obsługują język zapytań usługi Stream Analytics hello i JavaScript. Poniższa tabela zawiera hello konwersji mapowań między hello dwóch:

Stream Analytics | JavaScript
--- | ---
bigint | Numer (JavaScript może reprezentować tylko liczby całkowite się tooprecisely 2 ^ 53)
Data i godzina | Data (JavaScript tylko obsługuje w milisekundach)
O podwójnej precyzji | Liczba
nvarchar(max) | Ciąg
rekord | Obiekt
Tablica | Tablica
WARTOŚĆ NULL | Wartość null


Poniżej przedstawiono konwersje JavaScript do Stream Analytics:


JavaScript | Stream Analytics
--- | ---
Liczba | Bigint (jeśli jest to liczba hello jest okrągłych i między long. Wartość MinValue i długi. MaxValue; w przeciwnym razie jest podwójny)
Date | Data i godzina
Ciąg | nvarchar(max)
Obiekt | rekord
Tablica | Tablica
Wartość null, niezdefiniowane | WARTOŚĆ NULL
Innego typu (na przykład funkcja lub błąd) | Nieobsługiwane (powoduje błąd czasu wykonywania)

## <a name="troubleshooting"></a>Rozwiązywanie problemów
Błędy środowiska wykonawczego języka JavaScript są traktowane jako błąd krytyczny i są udostępniane za pośrednictwem hello dziennik aktywności. tooretrieve hello logowania, hello portalu Azure, przejdź tooyour zadania i wybierz **dziennik aktywności**.


## <a name="other-javascript-user-defined-function-patterns"></a>Innymi wzorami zdefiniowane przez użytkownika funkcja JavaScript

### <a name="write-nested-json-toooutput"></a>Zapis zagnieżdżonych toooutput JSON
Jeśli masz krok przetwarzania monitowania, który używa jako dane wejściowe zadania usługi analiza strumienia wyjściowego i wymaga formatu JSON, można napisać toooutput ciągu JSON. Witaj w następnym przykładzie wywołuje hello **JSON.stringify()** funkcji toopack wszystkich par nazwa/wartość hello danych wejściowych, a następnie zapisać je jako pojedynczy ciąg w danych wyjściowych.

**Definicja funkcji zdefiniowanej przez użytkownika JavaScript:**

```
function main(x) {
return JSON.stringify(x);
}
```

**Przykładowe zapytanie:**
```
SELECT
    DataString,
    DataValue,
    HexValue,
    UDF.json_stringify(input) As InputEvent
INTO
    output
FROM
    input PARTITION BY PARTITIONID
```

## <a name="get-help"></a>Uzyskiwanie pomocy
Aby uzyskać dodatkową pomoc, spróbuj naszych [forum usługi Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Następne kroki
* [Wprowadzenie tooAzure analiza strumienia](stream-analytics-introduction.md)
* [Get started using Azure Stream Analytics (Rozpoczynanie pracy z usługą Azure Stream Analytics)](stream-analytics-real-time-fraud-detection.md)
* [Scale Azure Stream Analytics jobs (Skalowanie zadań usługi Azure Stream Analytics)](stream-analytics-scale-jobs.md)
* [Dokumentacja języka zapytań usługi Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Usługa Azure Stream Analytics management dokumentacji interfejsu API REST](https://msdn.microsoft.com/library/azure/dn835031.aspx)
