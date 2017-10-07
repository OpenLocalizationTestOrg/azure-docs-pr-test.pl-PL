---
title: "Machine Learning interfejsów API: Analiza tekstu | Dokumentacja firmy Microsoft"
description: "Interfejsów API firmy Microsoft Machine Learning tekst Analytics może być używane tooanalyze bez struktury tekst dla analizy wskaźniki nastrojów klientów, wyodrębniania klucza frazy, wykrywania języka i wykrywania tematu."
services: machine-learning
documentationcenter: 
author: onewth
manager: jhubbard
editor: cgronlun
ms.assetid: 5b60694e-5521-4e4d-bf6a-1a92fdf94b65
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: onewth
ROBOTS: NOINDEX
redirect_url: ../cognitive-services/cognitive-services-text-analytics-quick-start
redirect_document_id: True
ms.openlocfilehash: 49380c83849c5d5fdd8dce4f3899ebcb3d6870f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="machine-learning-apis-text-analytics-for-sentiment-key-phrase-extraction-language-detection-and-topic-detection"></a>Interfejsy API usługi Machine Learning: analiza tekstu dla tonacji, wyodrębnianie kluczowych fraz, wykrywanie języka i wykrywanie tematów
> [!NOTE]
> Ten przewodnik jest przeznaczony dla wersji 1 hello interfejsu API. W wersji 2 [ **odwołuje się dokument toothis**](../cognitive-services/cognitive-services-text-analytics-quick-start.md). W wersji 2 jest teraz hello preferowaną wersję tego interfejsu API.
> 
> 

## <a name="overview"></a>Omówienie
Pakiet Analiza tekstu jest Hello interfejsu API z analizy tekstu [usług sieci web](https://datamarket.azure.com/dataset/amla/text-analytics) skompilowanej za pomocą usługi Azure Machine Learning. Witaj interfejsu API mogą być używane tooanalyze niestrukturalnych tekst dla zadań, takich jak analizy wskaźniki nastrojów klientów, wyodrębniania klucza frazy, wykrywania języka i wykrywania tematu. Nie szkolenia, dane są niezbędne toouse tego interfejsu API: Przełącz tylko dane tekstowe. Ten interfejs API korzysta z przetwarzania toodeliver techniki najlepiej w klasie prognoz zaawansowane języka naturalnego.

Analiza tekstu w akcji można wyświetlić na naszych [lokacji pokaz](https://text-analytics-demo.azurewebsites.net/), gdzie można również znaleźć [przykłady](https://text-analytics-demo.azurewebsites.net/Home/SampleCode) na temat tooimplement Analiza tekstu w języku C# i Python.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

- - -
## <a name="sentiment-analysis"></a>Analiza opinii
Witaj interfejsu API zwraca wynik liczbowych między 0 i 1. Zamknij too1 wyniki wskazują dodatnią wskaźniki nastrojów klientów, gdy too0 Zamknij wyniki wskazują ujemna wskaźniki nastrojów klientów. Wynik opinii jest generowany przy użyciu technik klasyfikacji. Klasyfikator toohello wejściowe funkcji Hello obejmują n g, funkcje generowane na podstawie części z mowy tagów i osadzeń programu word. Obecnie język angielski jest hello tylko obsługiwanego języka.

## <a name="key-phrase-extraction"></a>Wyodrębnianie kluczowych fraz
Hello interfejsu API zwraca listę ciągów określające hello klucza punktach wystąpienia w hello wejściowego tekstu. Korzystamy z technik używanych w wyrafinowanym zestawie narzędzi do przetwarzania języka naturalnego pakietu Microsoft Office. Obecnie język angielski jest hello tylko obsługiwanego języka.

## <a name="language-detection"></a>Wykrywanie języka
Witaj interfejsu API zwraca hello wykryto języka i wynik liczbową pomiędzy 0 i 1. Zamknij too1 wyniki wskazują 100% pewności, czy język hello zidentyfikowane ma wartość true. Obsługiwanych jest 120 języków.

## <a name="topic-detection"></a>Wykrywanie tematu
To jest nowo wydanego interfejsu API, który zwraca górny tematy wykryto hello listę rekordów przesłanych tekstu. Temat jest identyfikowany za pomocą frazy kluczowej, która może być jednym wyrazem lub większą liczbą pokrewnych wyrazów. Ten interfejs API wymaga co najmniej 100 tekstu rejestruje toobe przesłane, ale jest zaprojektowana toodetect tematy setkach toothousands rekordów. Należy pamiętać, że ten interfejs API nalicza 1 transakcję na przesłany rekord tekstowy. Witaj interfejsu API jest zaprojektowana toowork dla człowieka krótkie, zapisane tekstu, takie jak przeglądy i opinie użytkowników.

- - -
## <a name="api-definition"></a>Definicja interfejsu API
### <a name="headers"></a>Nagłówki
Upewnij się, obejmują nagłówki poprawne hello w żądaniu, która powinna być w następujący sposób:

    Authorization: Basic <creds>
    Accept: application/json

    Where <creds> = ConvertToBase64(“AccountKey:” + yourActualAccountKey);  

Klucz konta z Twojego konta można znaleźć w hello [rynku danych Azure](https://datamarket.azure.com/account/keys). Należy pamiętać, że obecnie tylko JSON jest akceptowany formatów wejściowych i wyjściowych. XML nie jest obsługiwane.

- - -
## <a name="single-response-apis"></a>Interfejsy API pojedynczą odpowiedź
### <a name="getsentiment"></a>GetSentiment
**ADRES URL**    

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentiment

**Przykładowe żądanie**

W poniższym wywołaniu hello prosimy analizy wskaźniki nastrojów klientów frazy powitania "Hello World":

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentiment?Text=hello+world

Spowoduje to zwrócenie odpowiedzi w następujący sposób:

    {
      "odata.metadata":"https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/$metadata",
        "Score":1.0
    }

- - -
### <a name="getkeyphrases"></a>GetKeyPhrases
**ADRES URL**

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrases

**Przykładowe żądanie**

W poniższym wywołaniu hello prosimy fraz klucza hello znalezione w tekście hello "Był cudowne toostay hoteli, a z decor unikatowy i pracownicy przyjazną":

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrases?
    Text=It+was+a+wonderful+hotel+to+stay+at,+with+unique+decor+and+friendly+staff

Spowoduje to zwrócenie odpowiedzi w następujący sposób:

    {
      "odata.metadata":"https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/$metadata",
      "KeyPhrases":[
        "wonderful hotel",
        "unique decor",
        "friendly staff"
      ]
    }

- - -
### <a name="getlanguage"></a>GetLanguage
**ADRES URL**

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguage

**Przykładowe żądanie**

W poniższym wywołaniu GET hello, prosimy dla hello wskaźniki nastrojów klientów hello zwrotów klucza w tekście hello *Witaj świecie*

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguages?
    Text=Hello+World

Spowoduje to zwrócenie odpowiedzi w następujący sposób:

    {
      "UnknownLanguage": false,
      "DetectedLanguages": [{
        "Name": "English",
        "Iso6391Name": "en",
        "Score": 1.0
      }]
    }

**Parametry opcjonalne**

`NumberOfLanguagesToDetect`jest parametrem opcjonalnym. Witaj domyślna to 1.

- - -
## <a name="batch-apis"></a>Interfejsy API partii
Hello usługi Analiza tekstu umożliwia możesz toodo wskaźniki nastrojów klientów i ekstrakcje frazy klucza w trybie wsadowym. Należy pamiętać, liczby poszczególnych rekordów hello oceniane jako jedna transakcja. Na przykład jeśli żądanie wskaźniki nastrojów klientów do 1000 rekordów w pojedynczym wywołaniu 1000 transakcji będzie odejmowana.

Należy pamiętać, że identyfikatory hello wprowadzane do systemu hello są identyfikatory hello zwrócone przez hello system. Usługa sieci web Hello nie sprawdza, czy te identyfikatory są unikatowe. Jest odpowiedzialny za hello hello wywołującego tooverify unikatowości. 

### <a name="getsentimentbatch"></a>GetSentimentBatch
**ADRES URL**    

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentimentBatch

**Przykładowe żądanie**

W hello POST wywołania poniżej, prosimy dla opinie hello fraz powitania "Hello World", "Foo Hello World" i "Hello Moje World" w treści żądania hello hello:

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentimentBatch 

Treść żądania:

    {"Inputs":
    [
        {"Id":"1","Text":"hello world"},
        {"Id":"2","Text":"hello foo world"},
        {"Id":"3","Text":"hello my world"},
    ]}

W odpowiedzi hello poniżej można uzyskać listy hello wyników skojarzone z tekstu identyfikatory:

    {
      "odata.metadata":"<url>", 
      "SentimentBatch":
      [
        {"Score":0.9549767,"Id":"1"},
        {"Score":0.7767222,"Id":"2"},
        {"Score":0.8988889,"Id":"3"}
      ],  
      "Errors":[]
    }


- - -
### <a name="getkeyphrasesbatch"></a>GetKeyPhrasesBatch
**ADRES URL**

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrasesBatch

**Przykładowe żądanie**

W tym przykładzie prosimy hello lista opinie hello zwrotów klucza w hello następujące teksty: 

* "Był cudowne toostay hoteli, a z decor unikatowy i pracownicy przyjazną"
* "Był niesamowite konferencji kompilacji z bardzo interesujące rozmów"
* "hello ruchu olbrzymich, I poświęconego trzy godziny przechodzi lotnisku toohello"

Zgłoszenia żądania jako punktu końcowego toohello wywołania POST:

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrasesBatch

Treść żądania:

    {"Inputs":
    [
        {"Id":"1","Text":"It was a wonderful hotel toostay at, with unique decor and friendly staff"},
        {"Id":"2","Text":"It was an amazing build conference, with very interesting talks"},
        {"Id":"3","Text":"hello traffic was terrible, I spent three hours going toohello airport"}
    ]}

W odpowiedzi hello poniżej można pobrać listy hello klucza fraz skojarzone z tekstu identyfikatory:

    { "odata.metadata":"<url>",
         "KeyPhrasesBatch":
        [
           {"KeyPhrases":["unique decor","friendly staff","wonderful hotel"],"Id":"1"},
           {"KeyPhrases":["amazing build conference","interesting talks"],"Id":"2"},
           {"KeyPhrases":["hours","traffic","airport"],"Id":"3" }
        ],
        "Errors":[]
    }

- - -
### <a name="getlanguagebatch"></a>GetLanguageBatch

W poniższym wywołaniu POST hello prosimy wykrywania dla dwóch parametrów wejściowych tekst:

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguageBatch

Treść żądania:

    {
      "Inputs": [
        {"Text": "hello world", "Id": "1"},
        {"Text": "c'est la vie", "Id": "2"}
      ]
    }

To polecenie zwróci powitania po odpowiedzi, w którym angielski zostanie wykryta w hello pierwsze dane wejściowe i francuskim w drugiej danej wejściowej hello:

    {
       "LanguageBatch": [{
         "Id": "1",
         "DetectedLanguages": [{
            "Name": "English",
            "Iso6391Name": "en",
            "Score": 1.0
         }],
         "UnknownLanguage": false
       },
       {
         "Id": "2",
         "DetectedLanguages": [{
            "Name": "French",
            "Iso6391Name": "fr",
            "Score": 1.0
         }],
         "UnknownLanguage": false
       }],
       "Errors": []
    }

- - -
## <a name="topic-detection-apis"></a>Interfejsy API wykrywania tematu
To jest nowo wydanego interfejsu API, który zwraca górny tematy wykryto hello listę rekordów przesłanych tekstu. Temat jest identyfikowany za pomocą frazy kluczowej, która może być jednym wyrazem lub większą liczbą pokrewnych wyrazów. Należy pamiętać, że ten interfejs API nalicza 1 transakcję na przesłany rekord tekstowy.

Ten interfejs API wymaga co najmniej 100 tekstu rejestruje toobe przesłane, ale jest zaprojektowana toodetect tematy setkach toothousands rekordów.

### <a name="topics--submit-job"></a>Tematy — przesyłania zadania
**ADRES URL**

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/StartTopicDetection

**Przykładowe żądanie**

W poniższym wywołaniu POST hello prosimy tematy dotyczące zestawu 100 artykułów, gdzie hello imienia i wejściowych przedstawiono artykuły, a dwie StopPhrases są uwzględniane.

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/StartTopicDetection HTTP/1.1

Treść żądania:

    {"Inputs":[
        {"Id":"1","Text":"I loved hello food at this restaurant"},
        ...,
        {"Id":"100","Text":"I hated hello decor"}
    ],
    "StopPhrases":[
        "restaurant", “visitor"
    ]}

W odpowiedzi hello poniżej możesz uzyskać hello JobId przesłane zadanie hello:

    {
        "odata.metadata":"<url>",
        "JobId":"<JobId>"
    }

Lista pojedynczego wyrazu lub wiele wyrażeń słowa, które nie powinny być zwracane jako — tematy. Może być używane toofilter się bardzo ogólnych tematów. Na przykład w zestawie danych o przeglądami hoteli "hoteli" i "hostel" może być fraz za pośrednictwem stop.  

### <a name="topics--poll-for-job-results"></a>Tematy — sondowania dla wyników zadania
**ADRES URL**

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetTopicDetectionResult

**Przykładowe żądanie**

Przekaż hello JobId zwracane z hello "Przesyłania zadania" krok toofetch hello wyników. Firma Microsoft zaleca wywołań tego punktu końcowego co minutę, dopóki stan = "Zakończ" hello odpowiedzi. Potrwa około 10 minutach toocomplete zadania, lub dłużej zadań z wielu tysięcy rekordów.

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetTopicDetectionResult?JobId=<JobId>


Podczas przetwarzania, odpowiedź hello będzie wyglądać następująco:

    {
        "odata.metadata":"<url>",
        "Status":"Running",
         "TopicInfo":[],
        "TopicAssignment":[],
        "Errors":[]
    }


Witaj interfejsu API zwraca dane wyjściowe w formacie JSON w hello następującego formatu:

    {
        "odata.metadata":"<url>",
        "Status":"Finished",
        "TopicInfo":[
        {
            "TopicId":"ed00480e-f0a0-41b3-8fe4-07c1593f4afd",
            "Score":8.0,
            "KeyPhrase":"food"
        },
        ...
        {
            "TopicId":"a5ca3f1a-fdb1-4f02-8f1b-89f2f626d692",
            "Score":6.0,
            "KeyPhrase":"decor"
            }
          ],
        "TopicAssignment":[
        {
            "Id":"1",
            "TopicId":"ed00480e-f0a0-41b3-8fe4-07c1593f4afd",
            "Distance":0.7809
        },
        ...
        {
            "Id":"100",
            "TopicId":"a5ca3f1a-fdb1-4f02-8f1b-89f2f626d692",
            "Distance":0.8034
        }
        ],
        "Errors":[]


Witaj właściwości dla każdej części odpowiedź hello są następujące:

**Właściwości TopicInfo**

| Klucz | Opis |
|:--- |:--- |
| TopicId |Unikatowy identyfikator dla każdego tematu. |
| Wynik |Liczba rekordów przypisany tootopic. |
| KeyPhrase |Summarizing wyraz lub frazę hello tematu. Może być 1 lub wiele słów. |

**Właściwości TopicAssignment**

| Klucz | Opis |
|:--- |:--- |
| Identyfikator |Identyfikator rekordu hello. Oznacza identyfikator toohello zawarte w danych wejściowych hello. |
| TopicId |Identyfikator tematu Hello który hello rekord został przypisany do. |
| odległość |Pewność, że rekord hello należy toohello tematu. Odległość bliżej toozero wskazuje większą wiarą. |

