---
title: "AAA(deprecated) leksykonie na podstawie wskaźniki nastrojów klientów analiza - Azure | Dokumentacja firmy Microsoft"
description: "(przestarzałe) Leksykonie na podstawie analizy wskaźniki nastrojów klientów"
services: machine-learning
documentationcenter: 
author: pengxia
manager: jhubbard
editor: cgronlun
ms.assetid: 912f41af-966c-4d79-a413-6f9fc02823df
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: pengxia
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: 1ed7e19441c6a8ad270a0c0f567b4aea588a583e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-lexicon-based-sentiment-analysis"></a><span data-ttu-id="bbfe2-103">(przestarzałe) Leksykonie na podstawie analizy wskaźniki nastrojów klientów</span><span class="sxs-lookup"><span data-stu-id="bbfe2-103">(deprecated) Lexicon Based Sentiment Analysis</span></span>

> [!NOTE]
> <span data-ttu-id="bbfe2-104">Witaj Microsoft DataMarket została wycofana i ten interfejs API jest przestarzały.</span><span class="sxs-lookup"><span data-stu-id="bbfe2-104">hello Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="bbfe2-105">Możesz znaleźć wiele interfejsów API i przydatne przykład eksperymenty w hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="bbfe2-105">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="bbfe2-106">Aby uzyskać więcej informacji na temat hello galerii, zobacz [udziału i odnajdywania zasobów w hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="bbfe2-106">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="bbfe2-107">Jak można mierzenia opinie użytkowników i stanowisk kierunku marek lub tematów w trybie online sieci społecznościowych, takich jak Facebook ogłoszenia tweetów, recenzje itp.?</span><span class="sxs-lookup"><span data-stu-id="bbfe2-107">How can you measure users’ opinions and attitudes toward brands or topics in online social networks, such as Facebook posts, tweets, reviews, etc.?</span></span> <span data-ttu-id="bbfe2-108">Wskaźniki nastrojów klientów analizy zapewnia metodę analizowania takie pytania.</span><span class="sxs-lookup"><span data-stu-id="bbfe2-108">Sentiment analysis provides a method for analyzing such questions.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="bbfe2-109">Zazwyczaj są dwie metody analizy wskaźniki nastrojów klientów.</span><span class="sxs-lookup"><span data-stu-id="bbfe2-109">There are generally two methods for sentiment analysis.</span></span> <span data-ttu-id="bbfe2-110">Jedna używa algorytmu uczenia nadzorowanego i hello innych może być traktowana jako learning nienadzorowanych.</span><span class="sxs-lookup"><span data-stu-id="bbfe2-110">One is using a supervised learning algorithm, and hello other can be treated as unsupervised learning.</span></span> <span data-ttu-id="bbfe2-111">Algorytm uczenia nadzorowanego zazwyczaj opiera się model klasyfikacji na dużych Boże adnotacjami.</span><span class="sxs-lookup"><span data-stu-id="bbfe2-111">A supervised learning algorithm generally builds a classification model on a large annotated corpus.</span></span> <span data-ttu-id="bbfe2-112">Dokładność głównie opiera się na powitania jakości adnotacji hello i zwykle proces szkolenia hello potrwa długo.</span><span class="sxs-lookup"><span data-stu-id="bbfe2-112">Its accuracy is mainly based on hello quality of hello annotation, and usually hello training process will take a long time.</span></span> <span data-ttu-id="bbfe2-113">Oprócz, gdy Trwa stosowanie hello algorytmu tooanother domeny, wynik hello zazwyczaj nie jest dobrym.</span><span class="sxs-lookup"><span data-stu-id="bbfe2-113">Besides that, when we apply hello algorithm tooanother domain, hello result is usually not good.</span></span> <span data-ttu-id="bbfe2-114">W porównaniu learning toosupervised, leksykonie na podstawie uczenie nienadzorowane używa słownika wskaźniki nastrojów klientów, które nie wymagają przechowywania Boże dużej ilości danych i szkolenia — co staje się znacznie szybciej hello całego procesu.</span><span class="sxs-lookup"><span data-stu-id="bbfe2-114">Compared toosupervised learning, lexicon-based unsupervised learning uses a sentiment dictionary, which doesn’t require storing a large data corpus and training - which makes hello whole process much faster.</span></span> 

<span data-ttu-id="bbfe2-115">Nasze [usługi](https://datamarket.azure.com/dataset/aml_labs/lexicon_based_sentiment_analysis) jest zbudowany na powitania leksykonie subiektywnej oceny MPQA (http://mpqa.cs.pitt.edu/lexicons/subj_lexicon/), które jest jednym z leksykonów subiektywnej oceny hello najczęściej używane.</span><span class="sxs-lookup"><span data-stu-id="bbfe2-115">Our [service](https://datamarket.azure.com/dataset/aml_labs/lexicon_based_sentiment_analysis) is built on hello MPQA Subjectivity Lexicon (http://mpqa.cs.pitt.edu/lexicons/subj_lexicon/), which is one of hello most commonly used subjectivity lexicons.</span></span> <span data-ttu-id="bbfe2-116">Brak 5097 ujemna 2533 dodatnią wyrażenia w MPQA.</span><span class="sxs-lookup"><span data-stu-id="bbfe2-116">There are 5097 negative and 2533 positive words in MPQA.</span></span> <span data-ttu-id="bbfe2-117">I wszystkie te słowa, które są przypisane jako bieguna silne lub słabe.</span><span class="sxs-lookup"><span data-stu-id="bbfe2-117">And all of these words are annotated as strong or weak polarity.</span></span> <span data-ttu-id="bbfe2-118">Boże całego Hello podlega GNU General Public License.</span><span class="sxs-lookup"><span data-stu-id="bbfe2-118">hello whole corpus is under GNU General Public License.</span></span> <span data-ttu-id="bbfe2-119">Usługa sieci web Hello może być tooany zastosowane krótkie zdania, takie jak tweetów i ogłoszeń Facebook.</span><span class="sxs-lookup"><span data-stu-id="bbfe2-119">hello web service can be applied tooany short sentences, such as tweets and Facebook posts.</span></span> 

> <span data-ttu-id="bbfe2-120">Ta usługa sieci web może być używana przez użytkowników — potencjalnie za pomocą aplikacji mobilnej, za pośrednictwem witryny sieci Web lub nawet na komputerze lokalnym, na przykład.</span><span class="sxs-lookup"><span data-stu-id="bbfe2-120">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer for example.</span></span> <span data-ttu-id="bbfe2-121">Ale hello hello usługi sieci web służy również tooserve, na przykład jak usługi Azure Machine Learning można toocreate używanych usług sieci web na podstawie kodu języka R.</span><span class="sxs-lookup"><span data-stu-id="bbfe2-121">But hello purpose of hello web service is also tooserve as an example of how Azure Machine Learning can be used toocreate web services on top of R code.</span></span> <span data-ttu-id="bbfe2-122">Przy użyciu kilku wierszy kodu języka R i kliknięcia przycisku w usłudze Azure Machine Learning Studio eksperyment można tworzyć z kodem R i opublikowane jako usługę sieci web.</span><span class="sxs-lookup"><span data-stu-id="bbfe2-122">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="bbfe2-123">usługi sieci web Hello można następnie toohello opublikowane w portalu Azure Marketplace i używane przez użytkowników i urządzeń w Witaj świecie bez ustawień infrastruktury przez autora hello hello usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="bbfe2-123">hello web service can then be published toohello Azure Marketplace and consumed by users and devices across hello world with no infrastructure setup by hello author of hello web service.</span></span>
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="bbfe2-124">Użycie usługi sieci web</span><span class="sxs-lookup"><span data-stu-id="bbfe2-124">Consumption of web service</span></span>
<span data-ttu-id="bbfe2-125">dane wejściowe Hello może być dowolny tekst, ale usługi sieci web hello lepiej współpracuje z krótkim zdań.</span><span class="sxs-lookup"><span data-stu-id="bbfe2-125">hello input data can be any text, but hello web service works better with short sentences.</span></span> <span data-ttu-id="bbfe2-126">dane wyjściowe Hello jest liczbą z zakresu od -1 do 1.</span><span class="sxs-lookup"><span data-stu-id="bbfe2-126">hello output is a numeric value between -1 and 1.</span></span> <span data-ttu-id="bbfe2-127">Dowolna wartość poniżej 0 oznacza, że hello wskaźniki nastrojów klientów tekstu hello jest ujemna Jeśli dodatnią powyżej 0.</span><span class="sxs-lookup"><span data-stu-id="bbfe2-127">Any value below 0 denotes that hello sentiment of hello text is negative; positive if above 0.</span></span> <span data-ttu-id="bbfe2-128">wartość bezwzględna Hello wyniku hello określa siłę hello hello skojarzone wskaźniki nastrojów klientów.</span><span class="sxs-lookup"><span data-stu-id="bbfe2-128">hello absolute value of hello result denotes hello strength of hello associated sentiment.</span></span> 

> <span data-ttu-id="bbfe2-129">Ta usługa hostowana na hello Azure Marketplace jest usługi OData; te można wywoływać za pomocą metody POST lub GET.</span><span class="sxs-lookup"><span data-stu-id="bbfe2-129">This service, as hosted on hello Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="bbfe2-130">Istnieje wiele sposobów używania usługi hello w zautomatyzowany sposób (przykładową aplikację jest [tutaj](http://microsoftazuremachinelearning.azurewebsites.net/)).</span><span class="sxs-lookup"><span data-stu-id="bbfe2-130">There are multiple ways of consuming hello service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="bbfe2-131">Rozpoczynanie korzystania z usług sieci web kod C#:</span><span class="sxs-lookup"><span data-stu-id="bbfe2-131">Starting C# code for web service consumption:</span></span>
    public class ScoreResult
    {
            [DataMember]
            public double result
            {
                get;
                set;
            }
    }

    void main()
    {
            using (var wb = new WebClient())
            {
                var acitionUri = new Uri("PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score");
                DataServiceContext ctx = new DataServiceContext(acitionUri);
                var cred = new NetworkCredential("PutEmailAddressHere", "ChangeToAPIKey");
                var cache = new CredentialCache();

                cache.Add(acitionUri, "Basic", cred);
                ctx.Credentials = cache;
                var query = ctx.Execute<ScoreResult>(acitionUri, "POST", true, new BodyOperationParameter("Text", TextBox1.Text));
                ScoreResult scoreResult = query.ElementAt(0);
                double result = scoreResult.result;
            }
    }



<span data-ttu-id="bbfe2-132">dane wejściowe Hello jest "Obecnie jest dobrym dzień".</span><span class="sxs-lookup"><span data-stu-id="bbfe2-132">hello input is “Today is a good day.”</span></span> <span data-ttu-id="bbfe2-133">dane wyjściowe Hello jest "1", który wskazuje dodatnią wskaźniki nastrojów klientów skojarzonych z zdania wejściowych hello.</span><span class="sxs-lookup"><span data-stu-id="bbfe2-133">hello output is “1”, which indicates a positive sentiment associated with hello input sentence.</span></span> 

## <a name="creation-of-web-service"></a><span data-ttu-id="bbfe2-134">Tworzenie usługi sieci web</span><span class="sxs-lookup"><span data-stu-id="bbfe2-134">Creation of web service</span></span>
> <span data-ttu-id="bbfe2-135">Ta usługa sieci web został utworzony przy użyciu usługi Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="bbfe2-135">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="bbfe2-136">Bezpłatna wersja próbna, a także wprowadzające filmy wideo dotyczące tworzenia eksperymenty i [publikowania usług sieci web](machine-learning-publish-a-machine-learning-web-service.md), można znaleźć pod adresem [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="bbfe2-136">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="bbfe2-137">Poniżej przedstawiono zrzut ekranu hello eksperymentu, utworzona hello kod przykład i usługi sieci web dla każdego z modułów hello w ramach eksperymentu hello.</span><span class="sxs-lookup"><span data-stu-id="bbfe2-137">Below is a screenshot of hello experiment that created hello web service and example code for each of hello modules within hello experiment.</span></span>
> 
> 

<span data-ttu-id="bbfe2-138">Za pomocą w usłudze Azure Machine Learning nowy pusty eksperyment została utworzona.</span><span class="sxs-lookup"><span data-stu-id="bbfe2-138">From within Azure Machine Learning, a new blank experiment was created.</span></span> <span data-ttu-id="bbfe2-139">na poniższej ilustracji Hello przedstawia hello przepływ eksperymentu analizy na podstawie leksykonie wskaźniki nastrojów klientów.</span><span class="sxs-lookup"><span data-stu-id="bbfe2-139">hello figure below shows hello experiment flow of lexicon-based sentiment analysis.</span></span> <span data-ttu-id="bbfe2-140">Plik "sent_dict.csv" Hello jest hello MPQA subiektywnej oceny leksykonie i jest ustawiony jako jedno z wejść hello z [wykonanie skryptu języka R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="bbfe2-140">hello “sent_dict.csv” file is hello MPQA subjectivity lexicon, and is set as one of hello inputs of [Execute R Script][execute-r-script].</span></span> <span data-ttu-id="bbfe2-141">Inny danych wejściowych jest próbkowany przeglądu z zestawu danych przeglądu Amazon powitania dla testu, w którym możemy wykonać wybór, zmiana nazwy kolumny i podziałem operacji.</span><span class="sxs-lookup"><span data-stu-id="bbfe2-141">Another input is a sampled review from hello Amazon review dataset for test, where we performed selection, column name modification, and split operations.</span></span> <span data-ttu-id="bbfe2-142">Wykorzystywane leksykonie subiektywnej oceny hello toostore skrót pakietu w pamięci hello i przyspieszyć proces obliczeń wynik hello.</span><span class="sxs-lookup"><span data-stu-id="bbfe2-142">We use a hash package toostore hello subjectivity lexicon in hello memory and accelerate hello score computation process.</span></span> <span data-ttu-id="bbfe2-143">Hello całego tekstu zostanie stokenizowanego przez pakiet "tm" i w porównaniu z word hello hello słownika wskaźniki nastrojów klientów.</span><span class="sxs-lookup"><span data-stu-id="bbfe2-143">hello whole text will be tokenized by “tm” package and compared with hello word in hello sentiment dictionary.</span></span> <span data-ttu-id="bbfe2-144">Na koniec wynikiem będzie obliczana przez dodanie wagi hello każdego wyrazu subiektywne w tekście hello.</span><span class="sxs-lookup"><span data-stu-id="bbfe2-144">Finally, a score will be calculated by adding hello weight of each subjective word in hello text.</span></span> 

### <a name="experiment-flow"></a><span data-ttu-id="bbfe2-145">Przepływ eksperymentu:</span><span class="sxs-lookup"><span data-stu-id="bbfe2-145">Experiment flow:</span></span>
![Przepływ eksperymentu][2]

#### <a name="module-1"></a><span data-ttu-id="bbfe2-147">Moduł 1:</span><span class="sxs-lookup"><span data-stu-id="bbfe2-147">Module 1:</span></span>
    # Map 1-based optional input ports toovariables
    sent_dict_data<- maml.mapInputPort(1) # class: data.frame
    dataset2 <- maml.mapInputPort(2) # class: data.frame

# <a name="install-hash-package"></a><span data-ttu-id="bbfe2-148">Zainstaluj pakiet wyznaczania wartości skrótu</span><span class="sxs-lookup"><span data-stu-id="bbfe2-148">Install hash package</span></span>
    install.packages("src/hash_2.2.6.zip", lib = ".", repos = NULL, verbose = TRUE)
    success <- library("hash", lib.loc = ".", logical.return = TRUE, verbose = TRUE)
    library(tm)
    library(stringr)

    #create sentiment dictionary
    negation_word <- c("not","nor", "no")
    result <- c()
    sent_dict <- hash()
    sent_dict <- hash(sent_dict_data$word, sent_dict_data$polarity)

    #  Compute sentiment score for each document
    for (m in 1:nrow(dataset2)){
    polarity_ratio <- 0
    polarity_total <- 0
    not <- 0
    sentence <- tolower(dataset2[m,1])
    if (nchar(sentence) > 0){
        token_array <- scan_tokenizer(sentence)
        for (j in 1:length(token_array)){
            word = str_replace_all(token_array[j], "[^[:alnum:]]", "")
            for (k in 1:length(negation_word)){
              if (word == negation_word[k]){
                not <- (not+1) %% 2

              }
            }
            if (word != ""){
                if (!is.null(sent_dict[[word]])){
                  polarity_ratio <- polarity_ratio + (-2*not+1)*sent_dict[[word]]
                  polarity_total <- polarity_total + abs(sent_dict[[word]])
                }
            }

        }
    }
    if (polarity_total > 0){
        result <- c(result, polarity_ratio/polarity_total)
    }else{
        result<- c(result,0)
    }
    }

    # Sample operation
    data.set <- data.frame(result)

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("data.set")



## <a name="limitations"></a><span data-ttu-id="bbfe2-149">Ograniczenia</span><span class="sxs-lookup"><span data-stu-id="bbfe2-149">Limitations</span></span>
<span data-ttu-id="bbfe2-150">Z perspektywy algorytm analizy na podstawie leksykonie wskaźniki nastrojów klientów jest narzędzie analizy ogólne wskaźniki nastrojów klientów, które mogą nie działać lepiej niż hello metody klasyfikacji dla określonych pól.</span><span class="sxs-lookup"><span data-stu-id="bbfe2-150">From an algorithm perspective, lexicon-based sentiment analysis is a general sentiment analysis tool, which may not perform better than hello classification method for specific fields.</span></span> <span data-ttu-id="bbfe2-151">problem negacji Hello nie jest również uwzględnione.</span><span class="sxs-lookup"><span data-stu-id="bbfe2-151">hello negation problem is not well dealt with.</span></span> <span data-ttu-id="bbfe2-152">Firma Microsoft kodowania negacji kilka wyrazów w naszym programu, ale lepiej jest za pomocą słownika negacji i niektóre reguły kompilacji.</span><span class="sxs-lookup"><span data-stu-id="bbfe2-152">We hardcode several negation words in our program, but a better way is using a negation dictionary and build some rules.</span></span> <span data-ttu-id="bbfe2-153">usługi sieci web Hello dokonuje lepiej na krótka i prosta zdań, takich jak tweetów i ogłoszeń Facebook niż zdań długich i złożonych, takie jak recenzje Amazon.</span><span class="sxs-lookup"><span data-stu-id="bbfe2-153">hello web service performs better on short and simple sentences, such as tweets and Facebook posts, than on long and complex sentences such as Amazon reviews.</span></span> 

## <a name="faq"></a><span data-ttu-id="bbfe2-154">Często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="bbfe2-154">FAQ</span></span>
<span data-ttu-id="bbfe2-155">Często zadawane pytania dotyczące wykorzystania hello usługi sieci web lub toohello publikowania portalu Azure Marketplace, zobacz [tutaj](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="bbfe2-155">For frequently asked questions on consumption of hello web service or publishing toohello Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-lexicon-based-sentiment-analysis/sentiment_analysis_1.png
[2]: ./media/machine-learning-r-csharp-lexicon-based-sentiment-analysis/sentiment_analysis_2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/


