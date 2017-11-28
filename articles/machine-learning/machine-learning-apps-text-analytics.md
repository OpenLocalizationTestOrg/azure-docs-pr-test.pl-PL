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
# <a name="machine-learning-apis-text-analytics-for-sentiment-key-phrase-extraction-language-detection-and-topic-detection"></a><span data-ttu-id="e17dd-103">Interfejsy API usługi Machine Learning: analiza tekstu dla tonacji, wyodrębnianie kluczowych fraz, wykrywanie języka i wykrywanie tematów</span><span class="sxs-lookup"><span data-stu-id="e17dd-103">Machine Learning APIs: Text Analytics for Sentiment, Key Phrase Extraction, Language Detection and Topic Detection</span></span>
> [!NOTE]
> <span data-ttu-id="e17dd-104">Ten przewodnik jest przeznaczony dla wersji 1 hello interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="e17dd-104">This guide is for version 1 of hello API.</span></span> <span data-ttu-id="e17dd-105">W wersji 2 [ **odwołuje się dokument toothis**](../cognitive-services/cognitive-services-text-analytics-quick-start.md).</span><span class="sxs-lookup"><span data-stu-id="e17dd-105">For version 2, [**refer toothis document**](../cognitive-services/cognitive-services-text-analytics-quick-start.md).</span></span> <span data-ttu-id="e17dd-106">W wersji 2 jest teraz hello preferowaną wersję tego interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="e17dd-106">Version 2 is now hello preferred version of this API.</span></span>
> 
> 

## <a name="overview"></a><span data-ttu-id="e17dd-107">Omówienie</span><span class="sxs-lookup"><span data-stu-id="e17dd-107">Overview</span></span>
<span data-ttu-id="e17dd-108">Pakiet Analiza tekstu jest Hello interfejsu API z analizy tekstu [usług sieci web](https://datamarket.azure.com/dataset/amla/text-analytics) skompilowanej za pomocą usługi Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="e17dd-108">hello Text Analytics API is a suite of text analytics [web services](https://datamarket.azure.com/dataset/amla/text-analytics) built with Azure Machine Learning.</span></span> <span data-ttu-id="e17dd-109">Witaj interfejsu API mogą być używane tooanalyze niestrukturalnych tekst dla zadań, takich jak analizy wskaźniki nastrojów klientów, wyodrębniania klucza frazy, wykrywania języka i wykrywania tematu.</span><span class="sxs-lookup"><span data-stu-id="e17dd-109">hello API can be used tooanalyze unstructured text for tasks such as sentiment analysis, key phrase extraction, language detection and topic detection.</span></span> <span data-ttu-id="e17dd-110">Nie szkolenia, dane są niezbędne toouse tego interfejsu API: Przełącz tylko dane tekstowe.</span><span class="sxs-lookup"><span data-stu-id="e17dd-110">No training data is needed toouse this API: just bring your text data.</span></span> <span data-ttu-id="e17dd-111">Ten interfejs API korzysta z przetwarzania toodeliver techniki najlepiej w klasie prognoz zaawansowane języka naturalnego.</span><span class="sxs-lookup"><span data-stu-id="e17dd-111">This API uses advanced natural language processing techniques toodeliver best in class predictions.</span></span>

<span data-ttu-id="e17dd-112">Analiza tekstu w akcji można wyświetlić na naszych [lokacji pokaz](https://text-analytics-demo.azurewebsites.net/), gdzie można również znaleźć [przykłady](https://text-analytics-demo.azurewebsites.net/Home/SampleCode) na temat tooimplement Analiza tekstu w języku C# i Python.</span><span class="sxs-lookup"><span data-stu-id="e17dd-112">You can see text analytics in action on our [demo site](https://text-analytics-demo.azurewebsites.net/), where you will also find [samples](https://text-analytics-demo.azurewebsites.net/Home/SampleCode) on how tooimplement text analytics in C# and Python.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

- - -
## <a name="sentiment-analysis"></a><span data-ttu-id="e17dd-113">Analiza opinii</span><span class="sxs-lookup"><span data-stu-id="e17dd-113">Sentiment analysis</span></span>
<span data-ttu-id="e17dd-114">Witaj interfejsu API zwraca wynik liczbowych między 0 i 1.</span><span class="sxs-lookup"><span data-stu-id="e17dd-114">hello API returns a numeric score between 0 & 1.</span></span> <span data-ttu-id="e17dd-115">Zamknij too1 wyniki wskazują dodatnią wskaźniki nastrojów klientów, gdy too0 Zamknij wyniki wskazują ujemna wskaźniki nastrojów klientów.</span><span class="sxs-lookup"><span data-stu-id="e17dd-115">Scores close too1 indicate positive sentiment, while scores close too0 indicate negative sentiment.</span></span> <span data-ttu-id="e17dd-116">Wynik opinii jest generowany przy użyciu technik klasyfikacji.</span><span class="sxs-lookup"><span data-stu-id="e17dd-116">Sentiment score is generated using classification techniques.</span></span> <span data-ttu-id="e17dd-117">Klasyfikator toohello wejściowe funkcji Hello obejmują n g, funkcje generowane na podstawie części z mowy tagów i osadzeń programu word.</span><span class="sxs-lookup"><span data-stu-id="e17dd-117">hello input features toohello classifier include n-grams, features generated from part-of-speech tags, and word embeddings.</span></span> <span data-ttu-id="e17dd-118">Obecnie język angielski jest hello tylko obsługiwanego języka.</span><span class="sxs-lookup"><span data-stu-id="e17dd-118">Currently, English is hello only supported language.</span></span>

## <a name="key-phrase-extraction"></a><span data-ttu-id="e17dd-119">Wyodrębnianie kluczowych fraz</span><span class="sxs-lookup"><span data-stu-id="e17dd-119">Key phrase extraction</span></span>
<span data-ttu-id="e17dd-120">Hello interfejsu API zwraca listę ciągów określające hello klucza punktach wystąpienia w hello wejściowego tekstu.</span><span class="sxs-lookup"><span data-stu-id="e17dd-120">hello API returns a list of strings denoting hello key talking points in hello input text.</span></span> <span data-ttu-id="e17dd-121">Korzystamy z technik używanych w wyrafinowanym zestawie narzędzi do przetwarzania języka naturalnego pakietu Microsoft Office.</span><span class="sxs-lookup"><span data-stu-id="e17dd-121">We employ techniques from Microsoft Office's sophisticated Natural Language Processing toolkit.</span></span> <span data-ttu-id="e17dd-122">Obecnie język angielski jest hello tylko obsługiwanego języka.</span><span class="sxs-lookup"><span data-stu-id="e17dd-122">Currently, English is hello only supported language.</span></span>

## <a name="language-detection"></a><span data-ttu-id="e17dd-123">Wykrywanie języka</span><span class="sxs-lookup"><span data-stu-id="e17dd-123">Language detection</span></span>
<span data-ttu-id="e17dd-124">Witaj interfejsu API zwraca hello wykryto języka i wynik liczbową pomiędzy 0 i 1.</span><span class="sxs-lookup"><span data-stu-id="e17dd-124">hello API returns hello detected language and a numeric score between 0 & 1.</span></span> <span data-ttu-id="e17dd-125">Zamknij too1 wyniki wskazują 100% pewności, czy język hello zidentyfikowane ma wartość true.</span><span class="sxs-lookup"><span data-stu-id="e17dd-125">Scores close too1 indicate 100% certainty that hello identified language is true.</span></span> <span data-ttu-id="e17dd-126">Obsługiwanych jest 120 języków.</span><span class="sxs-lookup"><span data-stu-id="e17dd-126">A total of 120 languages are supported.</span></span>

## <a name="topic-detection"></a><span data-ttu-id="e17dd-127">Wykrywanie tematu</span><span class="sxs-lookup"><span data-stu-id="e17dd-127">Topic detection</span></span>
<span data-ttu-id="e17dd-128">To jest nowo wydanego interfejsu API, który zwraca górny tematy wykryto hello listę rekordów przesłanych tekstu.</span><span class="sxs-lookup"><span data-stu-id="e17dd-128">This is a newly released API which returns hello top detected topics for a list of submitted text records.</span></span> <span data-ttu-id="e17dd-129">Temat jest identyfikowany za pomocą frazy kluczowej, która może być jednym wyrazem lub większą liczbą pokrewnych wyrazów.</span><span class="sxs-lookup"><span data-stu-id="e17dd-129">A topic is identified with a key phrase, which can be one or more related words.</span></span> <span data-ttu-id="e17dd-130">Ten interfejs API wymaga co najmniej 100 tekstu rejestruje toobe przesłane, ale jest zaprojektowana toodetect tematy setkach toothousands rekordów.</span><span class="sxs-lookup"><span data-stu-id="e17dd-130">This API requires a minimum of 100 text records toobe submitted, but is designed toodetect topics across hundreds toothousands of records.</span></span> <span data-ttu-id="e17dd-131">Należy pamiętać, że ten interfejs API nalicza 1 transakcję na przesłany rekord tekstowy.</span><span class="sxs-lookup"><span data-stu-id="e17dd-131">Note that this API charges 1 transaction per text record submitted.</span></span> <span data-ttu-id="e17dd-132">Witaj interfejsu API jest zaprojektowana toowork dla człowieka krótkie, zapisane tekstu, takie jak przeglądy i opinie użytkowników.</span><span class="sxs-lookup"><span data-stu-id="e17dd-132">hello API is designed toowork well for short, human written text such as reviews and user feedback.</span></span>

- - -
## <a name="api-definition"></a><span data-ttu-id="e17dd-133">Definicja interfejsu API</span><span class="sxs-lookup"><span data-stu-id="e17dd-133">API Definition</span></span>
### <a name="headers"></a><span data-ttu-id="e17dd-134">Nagłówki</span><span class="sxs-lookup"><span data-stu-id="e17dd-134">Headers</span></span>
<span data-ttu-id="e17dd-135">Upewnij się, obejmują nagłówki poprawne hello w żądaniu, która powinna być w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="e17dd-135">Ensure that you include hello correct headers in your request, which should be as follows:</span></span>

    Authorization: Basic <creds>
    Accept: application/json

    Where <creds> = ConvertToBase64(“AccountKey:” + yourActualAccountKey);  

<span data-ttu-id="e17dd-136">Klucz konta z Twojego konta można znaleźć w hello [rynku danych Azure](https://datamarket.azure.com/account/keys).</span><span class="sxs-lookup"><span data-stu-id="e17dd-136">You can find your account key from your account in hello [Azure Data Market](https://datamarket.azure.com/account/keys).</span></span> <span data-ttu-id="e17dd-137">Należy pamiętać, że obecnie tylko JSON jest akceptowany formatów wejściowych i wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="e17dd-137">Note that currently only JSON is accepted for input and output formats.</span></span> <span data-ttu-id="e17dd-138">XML nie jest obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="e17dd-138">XML is not supported.</span></span>

- - -
## <a name="single-response-apis"></a><span data-ttu-id="e17dd-139">Interfejsy API pojedynczą odpowiedź</span><span class="sxs-lookup"><span data-stu-id="e17dd-139">Single Response APIs</span></span>
### <a name="getsentiment"></a><span data-ttu-id="e17dd-140">GetSentiment</span><span class="sxs-lookup"><span data-stu-id="e17dd-140">GetSentiment</span></span>
<span data-ttu-id="e17dd-141">**ADRES URL**</span><span class="sxs-lookup"><span data-stu-id="e17dd-141">**URL**</span></span>    

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentiment

<span data-ttu-id="e17dd-142">**Przykładowe żądanie**</span><span class="sxs-lookup"><span data-stu-id="e17dd-142">**Example request**</span></span>

<span data-ttu-id="e17dd-143">W poniższym wywołaniu hello prosimy analizy wskaźniki nastrojów klientów frazy powitania "Hello World":</span><span class="sxs-lookup"><span data-stu-id="e17dd-143">In hello call below, we are requesting sentiment analysis for hello phrase "Hello World":</span></span>

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentiment?Text=hello+world

<span data-ttu-id="e17dd-144">Spowoduje to zwrócenie odpowiedzi w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="e17dd-144">This will return a response as follows:</span></span>

    {
      "odata.metadata":"https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/$metadata",
        "Score":1.0
    }

- - -
### <a name="getkeyphrases"></a><span data-ttu-id="e17dd-145">GetKeyPhrases</span><span class="sxs-lookup"><span data-stu-id="e17dd-145">GetKeyPhrases</span></span>
<span data-ttu-id="e17dd-146">**ADRES URL**</span><span class="sxs-lookup"><span data-stu-id="e17dd-146">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrases

<span data-ttu-id="e17dd-147">**Przykładowe żądanie**</span><span class="sxs-lookup"><span data-stu-id="e17dd-147">**Example request**</span></span>

<span data-ttu-id="e17dd-148">W poniższym wywołaniu hello prosimy fraz klucza hello znalezione w tekście hello "Był cudowne toostay hoteli, a z decor unikatowy i pracownicy przyjazną":</span><span class="sxs-lookup"><span data-stu-id="e17dd-148">In hello call below, we are requesting hello key phrases found in hello text "It was a wonderful hotel toostay at, with unique decor and friendly staff":</span></span>

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrases?
    Text=It+was+a+wonderful+hotel+to+stay+at,+with+unique+decor+and+friendly+staff

<span data-ttu-id="e17dd-149">Spowoduje to zwrócenie odpowiedzi w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="e17dd-149">This will return a response as follows:</span></span>

    {
      "odata.metadata":"https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/$metadata",
      "KeyPhrases":[
        "wonderful hotel",
        "unique decor",
        "friendly staff"
      ]
    }

- - -
### <a name="getlanguage"></a><span data-ttu-id="e17dd-150">GetLanguage</span><span class="sxs-lookup"><span data-stu-id="e17dd-150">GetLanguage</span></span>
<span data-ttu-id="e17dd-151">**ADRES URL**</span><span class="sxs-lookup"><span data-stu-id="e17dd-151">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguage

<span data-ttu-id="e17dd-152">**Przykładowe żądanie**</span><span class="sxs-lookup"><span data-stu-id="e17dd-152">**Example request**</span></span>

<span data-ttu-id="e17dd-153">W poniższym wywołaniu GET hello, prosimy dla hello wskaźniki nastrojów klientów hello zwrotów klucza w tekście hello *Witaj świecie*</span><span class="sxs-lookup"><span data-stu-id="e17dd-153">In hello GET call below, we are requesting for hello sentiment for hello key phrases in hello text *Hello World*</span></span>

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguages?
    Text=Hello+World

<span data-ttu-id="e17dd-154">Spowoduje to zwrócenie odpowiedzi w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="e17dd-154">This will return a response as follows:</span></span>

    {
      "UnknownLanguage": false,
      "DetectedLanguages": [{
        "Name": "English",
        "Iso6391Name": "en",
        "Score": 1.0
      }]
    }

<span data-ttu-id="e17dd-155">**Parametry opcjonalne**</span><span class="sxs-lookup"><span data-stu-id="e17dd-155">**Optional parameters**</span></span>

<span data-ttu-id="e17dd-156">`NumberOfLanguagesToDetect`jest parametrem opcjonalnym.</span><span class="sxs-lookup"><span data-stu-id="e17dd-156">`NumberOfLanguagesToDetect` is an optional parameter.</span></span> <span data-ttu-id="e17dd-157">Witaj domyślna to 1.</span><span class="sxs-lookup"><span data-stu-id="e17dd-157">hello default is 1.</span></span>

- - -
## <a name="batch-apis"></a><span data-ttu-id="e17dd-158">Interfejsy API partii</span><span class="sxs-lookup"><span data-stu-id="e17dd-158">Batch APIs</span></span>
<span data-ttu-id="e17dd-159">Hello usługi Analiza tekstu umożliwia możesz toodo wskaźniki nastrojów klientów i ekstrakcje frazy klucza w trybie wsadowym.</span><span class="sxs-lookup"><span data-stu-id="e17dd-159">hello Text Analytics service allows you toodo sentiment and key-phrase extractions in batch mode.</span></span> <span data-ttu-id="e17dd-160">Należy pamiętać, liczby poszczególnych rekordów hello oceniane jako jedna transakcja.</span><span class="sxs-lookup"><span data-stu-id="e17dd-160">Note that each of hello records scored counts as one transaction.</span></span> <span data-ttu-id="e17dd-161">Na przykład jeśli żądanie wskaźniki nastrojów klientów do 1000 rekordów w pojedynczym wywołaniu 1000 transakcji będzie odejmowana.</span><span class="sxs-lookup"><span data-stu-id="e17dd-161">As an example, if you request sentiment for 1000 records in a single call, 1000 transactions will be deducted.</span></span>

<span data-ttu-id="e17dd-162">Należy pamiętać, że identyfikatory hello wprowadzane do systemu hello są identyfikatory hello zwrócone przez hello system.</span><span class="sxs-lookup"><span data-stu-id="e17dd-162">Note that hello IDs entered into hello system are hello IDs returned by hello system.</span></span> <span data-ttu-id="e17dd-163">Usługa sieci web Hello nie sprawdza, czy te identyfikatory są unikatowe.</span><span class="sxs-lookup"><span data-stu-id="e17dd-163">hello web service does not check that these IDs are unique.</span></span> <span data-ttu-id="e17dd-164">Jest odpowiedzialny za hello hello wywołującego tooverify unikatowości.</span><span class="sxs-lookup"><span data-stu-id="e17dd-164">It is hello responsibility of hello caller tooverify uniqueness.</span></span> 

### <a name="getsentimentbatch"></a><span data-ttu-id="e17dd-165">GetSentimentBatch</span><span class="sxs-lookup"><span data-stu-id="e17dd-165">GetSentimentBatch</span></span>
<span data-ttu-id="e17dd-166">**ADRES URL**</span><span class="sxs-lookup"><span data-stu-id="e17dd-166">**URL**</span></span>    

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentimentBatch

<span data-ttu-id="e17dd-167">**Przykładowe żądanie**</span><span class="sxs-lookup"><span data-stu-id="e17dd-167">**Example request**</span></span>

<span data-ttu-id="e17dd-168">W hello POST wywołania poniżej, prosimy dla opinie hello fraz powitania "Hello World", "Foo Hello World" i "Hello Moje World" w treści żądania hello hello:</span><span class="sxs-lookup"><span data-stu-id="e17dd-168">In hello POST call below, we are requesting for hello sentiments of hello phrases "Hello World", "Hello Foo World" and "Hello My World" in hello body of hello request:</span></span>

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentimentBatch 

<span data-ttu-id="e17dd-169">Treść żądania:</span><span class="sxs-lookup"><span data-stu-id="e17dd-169">Request body:</span></span>

    {"Inputs":
    [
        {"Id":"1","Text":"hello world"},
        {"Id":"2","Text":"hello foo world"},
        {"Id":"3","Text":"hello my world"},
    ]}

<span data-ttu-id="e17dd-170">W odpowiedzi hello poniżej można uzyskać listy hello wyników skojarzone z tekstu identyfikatory:</span><span class="sxs-lookup"><span data-stu-id="e17dd-170">In hello response below, you get hello list of scores associated with your text Ids:</span></span>

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
### <a name="getkeyphrasesbatch"></a><span data-ttu-id="e17dd-171">GetKeyPhrasesBatch</span><span class="sxs-lookup"><span data-stu-id="e17dd-171">GetKeyPhrasesBatch</span></span>
<span data-ttu-id="e17dd-172">**ADRES URL**</span><span class="sxs-lookup"><span data-stu-id="e17dd-172">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrasesBatch

<span data-ttu-id="e17dd-173">**Przykładowe żądanie**</span><span class="sxs-lookup"><span data-stu-id="e17dd-173">**Example request**</span></span>

<span data-ttu-id="e17dd-174">W tym przykładzie prosimy hello lista opinie hello zwrotów klucza w hello następujące teksty:</span><span class="sxs-lookup"><span data-stu-id="e17dd-174">In this example, we are requesting for hello list of sentiments for hello key phrases in hello following texts:</span></span> 

* <span data-ttu-id="e17dd-175">"Był cudowne toostay hoteli, a z decor unikatowy i pracownicy przyjazną"</span><span class="sxs-lookup"><span data-stu-id="e17dd-175">"It was a wonderful hotel toostay at, with unique decor and friendly staff"</span></span>
* <span data-ttu-id="e17dd-176">"Był niesamowite konferencji kompilacji z bardzo interesujące rozmów"</span><span class="sxs-lookup"><span data-stu-id="e17dd-176">"It was an amazing build conference, with very interesting talks"</span></span>
* <span data-ttu-id="e17dd-177">"hello ruchu olbrzymich, I poświęconego trzy godziny przechodzi lotnisku toohello"</span><span class="sxs-lookup"><span data-stu-id="e17dd-177">"hello traffic was terrible, I spent three hours going toohello airport"</span></span>

<span data-ttu-id="e17dd-178">Zgłoszenia żądania jako punktu końcowego toohello wywołania POST:</span><span class="sxs-lookup"><span data-stu-id="e17dd-178">This request is made as a POST call toohello endpoint:</span></span>

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrasesBatch

<span data-ttu-id="e17dd-179">Treść żądania:</span><span class="sxs-lookup"><span data-stu-id="e17dd-179">Request body:</span></span>

    {"Inputs":
    [
        {"Id":"1","Text":"It was a wonderful hotel toostay at, with unique decor and friendly staff"},
        {"Id":"2","Text":"It was an amazing build conference, with very interesting talks"},
        {"Id":"3","Text":"hello traffic was terrible, I spent three hours going toohello airport"}
    ]}

<span data-ttu-id="e17dd-180">W odpowiedzi hello poniżej można pobrać listy hello klucza fraz skojarzone z tekstu identyfikatory:</span><span class="sxs-lookup"><span data-stu-id="e17dd-180">In hello response below, you get hello list of key phrases associated with your text Ids:</span></span>

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
### <a name="getlanguagebatch"></a><span data-ttu-id="e17dd-181">GetLanguageBatch</span><span class="sxs-lookup"><span data-stu-id="e17dd-181">GetLanguageBatch</span></span>

<span data-ttu-id="e17dd-182">W poniższym wywołaniu POST hello prosimy wykrywania dla dwóch parametrów wejściowych tekst:</span><span class="sxs-lookup"><span data-stu-id="e17dd-182">In hello POST call below, we are requesting language detection for two text inputs:</span></span>

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguageBatch

<span data-ttu-id="e17dd-183">Treść żądania:</span><span class="sxs-lookup"><span data-stu-id="e17dd-183">Request body:</span></span>

    {
      "Inputs": [
        {"Text": "hello world", "Id": "1"},
        {"Text": "c'est la vie", "Id": "2"}
      ]
    }

<span data-ttu-id="e17dd-184">To polecenie zwróci powitania po odpowiedzi, w którym angielski zostanie wykryta w hello pierwsze dane wejściowe i francuskim w drugiej danej wejściowej hello:</span><span class="sxs-lookup"><span data-stu-id="e17dd-184">This returns hello following response, where English is detected in hello first input and French in hello second input:</span></span>

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
## <a name="topic-detection-apis"></a><span data-ttu-id="e17dd-185">Interfejsy API wykrywania tematu</span><span class="sxs-lookup"><span data-stu-id="e17dd-185">Topic Detection APIs</span></span>
<span data-ttu-id="e17dd-186">To jest nowo wydanego interfejsu API, który zwraca górny tematy wykryto hello listę rekordów przesłanych tekstu.</span><span class="sxs-lookup"><span data-stu-id="e17dd-186">This is a newly released API which returns hello top detected topics for a list of submitted text records.</span></span> <span data-ttu-id="e17dd-187">Temat jest identyfikowany za pomocą frazy kluczowej, która może być jednym wyrazem lub większą liczbą pokrewnych wyrazów.</span><span class="sxs-lookup"><span data-stu-id="e17dd-187">A topic is identified with a key phrase, which can be one or more related words.</span></span> <span data-ttu-id="e17dd-188">Należy pamiętać, że ten interfejs API nalicza 1 transakcję na przesłany rekord tekstowy.</span><span class="sxs-lookup"><span data-stu-id="e17dd-188">Note that this API charges 1 transaction per text record submitted.</span></span>

<span data-ttu-id="e17dd-189">Ten interfejs API wymaga co najmniej 100 tekstu rejestruje toobe przesłane, ale jest zaprojektowana toodetect tematy setkach toothousands rekordów.</span><span class="sxs-lookup"><span data-stu-id="e17dd-189">This API requires a minimum of 100 text records toobe submitted, but is designed toodetect topics across hundreds toothousands of records.</span></span>

### <a name="topics--submit-job"></a><span data-ttu-id="e17dd-190">Tematy — przesyłania zadania</span><span class="sxs-lookup"><span data-stu-id="e17dd-190">Topics – Submit job</span></span>
<span data-ttu-id="e17dd-191">**ADRES URL**</span><span class="sxs-lookup"><span data-stu-id="e17dd-191">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/StartTopicDetection

<span data-ttu-id="e17dd-192">**Przykładowe żądanie**</span><span class="sxs-lookup"><span data-stu-id="e17dd-192">**Example request**</span></span>

<span data-ttu-id="e17dd-193">W poniższym wywołaniu POST hello prosimy tematy dotyczące zestawu 100 artykułów, gdzie hello imienia i wejściowych przedstawiono artykuły, a dwie StopPhrases są uwzględniane.</span><span class="sxs-lookup"><span data-stu-id="e17dd-193">In hello POST call below, we are requesting topics for a set of 100 articles, where hello first and last input articles are shown, and two StopPhrases are included.</span></span>

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/StartTopicDetection HTTP/1.1

<span data-ttu-id="e17dd-194">Treść żądania:</span><span class="sxs-lookup"><span data-stu-id="e17dd-194">Request body:</span></span>

    {"Inputs":[
        {"Id":"1","Text":"I loved hello food at this restaurant"},
        ...,
        {"Id":"100","Text":"I hated hello decor"}
    ],
    "StopPhrases":[
        "restaurant", “visitor"
    ]}

<span data-ttu-id="e17dd-195">W odpowiedzi hello poniżej możesz uzyskać hello JobId przesłane zadanie hello:</span><span class="sxs-lookup"><span data-stu-id="e17dd-195">In hello response below, you get hello JobId for hello submitted job:</span></span>

    {
        "odata.metadata":"<url>",
        "JobId":"<JobId>"
    }

<span data-ttu-id="e17dd-196">Lista pojedynczego wyrazu lub wiele wyrażeń słowa, które nie powinny być zwracane jako — tematy.</span><span class="sxs-lookup"><span data-stu-id="e17dd-196">A list of single word or multiple word phrases which should not be returned as topics.</span></span> <span data-ttu-id="e17dd-197">Może być używane toofilter się bardzo ogólnych tematów.</span><span class="sxs-lookup"><span data-stu-id="e17dd-197">Can be used toofilter out very generic topics.</span></span> <span data-ttu-id="e17dd-198">Na przykład w zestawie danych o przeglądami hoteli "hoteli" i "hostel" może być fraz za pośrednictwem stop.</span><span class="sxs-lookup"><span data-stu-id="e17dd-198">For example, in a dataset about hotel reviews, "hotel" and "hostel" may be sensible stop phrases.</span></span>  

### <a name="topics--poll-for-job-results"></a><span data-ttu-id="e17dd-199">Tematy — sondowania dla wyników zadania</span><span class="sxs-lookup"><span data-stu-id="e17dd-199">Topics – Poll for job results</span></span>
<span data-ttu-id="e17dd-200">**ADRES URL**</span><span class="sxs-lookup"><span data-stu-id="e17dd-200">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetTopicDetectionResult

<span data-ttu-id="e17dd-201">**Przykładowe żądanie**</span><span class="sxs-lookup"><span data-stu-id="e17dd-201">**Example request**</span></span>

<span data-ttu-id="e17dd-202">Przekaż hello JobId zwracane z hello "Przesyłania zadania" krok toofetch hello wyników.</span><span class="sxs-lookup"><span data-stu-id="e17dd-202">Pass hello JobId returned from hello ‘Submit job’ step toofetch hello results.</span></span> <span data-ttu-id="e17dd-203">Firma Microsoft zaleca wywołań tego punktu końcowego co minutę, dopóki stan = "Zakończ" hello odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="e17dd-203">We recommend that you call this endpoint every minute until Status=’Complete’ in hello response.</span></span> <span data-ttu-id="e17dd-204">Potrwa około 10 minutach toocomplete zadania, lub dłużej zadań z wielu tysięcy rekordów.</span><span class="sxs-lookup"><span data-stu-id="e17dd-204">It will take around 10 mins for a job toocomplete, or longer for jobs with many thousands of records.</span></span>

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetTopicDetectionResult?JobId=<JobId>


<span data-ttu-id="e17dd-205">Podczas przetwarzania, odpowiedź hello będzie wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="e17dd-205">While it is processing, hello response will be as follows:</span></span>

    {
        "odata.metadata":"<url>",
        "Status":"Running",
         "TopicInfo":[],
        "TopicAssignment":[],
        "Errors":[]
    }


<span data-ttu-id="e17dd-206">Witaj interfejsu API zwraca dane wyjściowe w formacie JSON w hello następującego formatu:</span><span class="sxs-lookup"><span data-stu-id="e17dd-206">hello API returns output in JSON format in hello following format:</span></span>

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


<span data-ttu-id="e17dd-207">Witaj właściwości dla każdej części odpowiedź hello są następujące:</span><span class="sxs-lookup"><span data-stu-id="e17dd-207">hello properties for each part of hello response are as follows:</span></span>

<span data-ttu-id="e17dd-208">**Właściwości TopicInfo**</span><span class="sxs-lookup"><span data-stu-id="e17dd-208">**TopicInfo properties**</span></span>

| <span data-ttu-id="e17dd-209">Klucz</span><span class="sxs-lookup"><span data-stu-id="e17dd-209">Key</span></span> | <span data-ttu-id="e17dd-210">Opis</span><span class="sxs-lookup"><span data-stu-id="e17dd-210">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="e17dd-211">TopicId</span><span class="sxs-lookup"><span data-stu-id="e17dd-211">TopicId</span></span> |<span data-ttu-id="e17dd-212">Unikatowy identyfikator dla każdego tematu.</span><span class="sxs-lookup"><span data-stu-id="e17dd-212">A unique identifier for each topic.</span></span> |
| <span data-ttu-id="e17dd-213">Wynik</span><span class="sxs-lookup"><span data-stu-id="e17dd-213">Score</span></span> |<span data-ttu-id="e17dd-214">Liczba rekordów przypisany tootopic.</span><span class="sxs-lookup"><span data-stu-id="e17dd-214">Count of records assigned tootopic.</span></span> |
| <span data-ttu-id="e17dd-215">KeyPhrase</span><span class="sxs-lookup"><span data-stu-id="e17dd-215">KeyPhrase</span></span> |<span data-ttu-id="e17dd-216">Summarizing wyraz lub frazę hello tematu.</span><span class="sxs-lookup"><span data-stu-id="e17dd-216">A summarizing word or phrase for hello topic.</span></span> <span data-ttu-id="e17dd-217">Może być 1 lub wiele słów.</span><span class="sxs-lookup"><span data-stu-id="e17dd-217">Can be 1 or multiple words.</span></span> |

<span data-ttu-id="e17dd-218">**Właściwości TopicAssignment**</span><span class="sxs-lookup"><span data-stu-id="e17dd-218">**TopicAssignment properties**</span></span>

| <span data-ttu-id="e17dd-219">Klucz</span><span class="sxs-lookup"><span data-stu-id="e17dd-219">Key</span></span> | <span data-ttu-id="e17dd-220">Opis</span><span class="sxs-lookup"><span data-stu-id="e17dd-220">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="e17dd-221">Identyfikator</span><span class="sxs-lookup"><span data-stu-id="e17dd-221">Id</span></span> |<span data-ttu-id="e17dd-222">Identyfikator rekordu hello.</span><span class="sxs-lookup"><span data-stu-id="e17dd-222">Identifier for hello record.</span></span> <span data-ttu-id="e17dd-223">Oznacza identyfikator toohello zawarte w danych wejściowych hello.</span><span class="sxs-lookup"><span data-stu-id="e17dd-223">Equates toohello ID included in hello input.</span></span> |
| <span data-ttu-id="e17dd-224">TopicId</span><span class="sxs-lookup"><span data-stu-id="e17dd-224">TopicId</span></span> |<span data-ttu-id="e17dd-225">Identyfikator tematu Hello który hello rekord został przypisany do.</span><span class="sxs-lookup"><span data-stu-id="e17dd-225">hello topic ID which hello record has been assigned to.</span></span> |
| <span data-ttu-id="e17dd-226">odległość</span><span class="sxs-lookup"><span data-stu-id="e17dd-226">Distance</span></span> |<span data-ttu-id="e17dd-227">Pewność, że rekord hello należy toohello tematu.</span><span class="sxs-lookup"><span data-stu-id="e17dd-227">Confidence that hello record belongs toohello topic.</span></span> <span data-ttu-id="e17dd-228">Odległość bliżej toozero wskazuje większą wiarą.</span><span class="sxs-lookup"><span data-stu-id="e17dd-228">Distance closer toozero indicates higher confidence.</span></span> |

