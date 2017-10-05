---
title: "(przestarzałe) Leksykonie na podstawie analizy wskaźniki nastrojów klientów - Azure | Dokumentacja firmy Microsoft"
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
redirect_document_id: TRUE
ms.openlocfilehash: 7bc80a1e1067296528eca1a843ea30b0c27af616
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-lexicon-based-sentiment-analysis"></a>(przestarzałe) Leksykonie na podstawie analizy wskaźniki nastrojów klientów

> [!NOTE]
> Microsoft DataMarket została wycofana i ten interfejs API jest przestarzały. 
> 
> Możesz znaleźć wiele eksperymenty przykład przydatne i interfejsów API w [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com). Aby uzyskać więcej informacji o galerii, zobacz [udziału i odnajdywania zasobów w Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).

Jak można mierzenia opinie użytkowników i stanowisk kierunku marek lub tematów w trybie online sieci społecznościowych, takich jak Facebook ogłoszenia tweetów, recenzje itp.? Wskaźniki nastrojów klientów analizy zapewnia metodę analizowania takie pytania.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Zazwyczaj są dwie metody analizy wskaźniki nastrojów klientów. Jedna używa algorytmu uczenia nadzorowanego, a drugi może być traktowana jako uczenie nienadzorowane. Algorytm uczenia nadzorowanego zazwyczaj opiera się model klasyfikacji na dużych Boże adnotacjami. Dokładność zależy głównie jakości adnotacji i zwykle Szkolenie potrwa długo. Oprócz, gdy Trwa stosowanie algorytmu do innej domeny, wynik zazwyczaj nie jest dobra. W porównaniu do nadzorowane nauki, na podstawie leksykonie używa uczenie nienadzorowane słownika wskaźniki nastrojów klientów, które nie wymagają przechowywania Boże dużej ilości danych i szkolenia — które sprawia, że cały proces znacznie szybsze. 

Nasze [usługi](https://datamarket.azure.com/dataset/aml_labs/lexicon_based_sentiment_analysis) jest oparty na leksykonie subiektywnej oceny MPQA (http://mpqa.cs.pitt.edu/lexicons/subj_lexicon/), które jest jednym z leksykonów najczęściej używane subiektywnej oceny. Brak 5097 ujemna 2533 dodatnią wyrażenia w MPQA. I wszystkie te słowa, które są przypisane jako bieguna silne lub słabe. Całe Boże podlega GNU General Public License. Usługi sieci web można zastosować do dowolnego krótkie zdania, takie jak tweetów i ogłoszeń usługi Facebook. 

> Ta usługa sieci web może być używana przez użytkowników — potencjalnie za pomocą aplikacji mobilnej, za pośrednictwem witryny sieci Web lub nawet na komputerze lokalnym, na przykład. Ale celem usługi sieci web jest również służyć jako przykład sposobu użycia usługi Azure Machine Learning do tworzenia usług sieci web na podstawie kodu języka R. Przy użyciu kilku wierszy kodu języka R i kliknięcia przycisku w usłudze Azure Machine Learning Studio eksperyment można tworzyć z kodem R i opublikowane jako usługę sieci web. Usługi sieci web może następnie opublikowane w portalu Azure Marketplace i używane przez użytkowników i urządzeń w całym świecie bez ustawień infrastruktury przez autora usługi sieci web.
> 
> 

## <a name="consumption-of-web-service"></a>Użycie usługi sieci web
Dane wejściowe mogą być tekstem, ale usługi sieci web lepiej współpracuje z krótkim zdań. Wynik jest wartością liczbową z przedziału od -1 do 1. Dowolna wartość poniżej 0 oznacza, że wskaźniki nastrojów klientów tekstu jest ujemna Jeśli dodatnią powyżej 0. Wartość bezwzględna wyniku określa siłę skojarzone wskaźniki nastrojów klientów. 

> Ta usługa hostowana w portalu Azure Marketplace jest usługi OData; te można wywoływać za pomocą metody POST lub GET. 
> 
> 

Istnieje wiele sposobów używania usługi w zautomatyzowany sposób (przykładową aplikację jest [tutaj](http://microsoftazuremachinelearning.azurewebsites.net/)).

### <a name="starting-c-code-for-web-service-consumption"></a>Rozpoczynanie korzystania z usług sieci web kod C#:
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



Dane wejściowe są "Obecnie jest dobrym dzień". Dane wyjściowe są "1", który wskazuje dodatnią wskaźniki nastrojów klientów skojarzonych z wejściowych zdanie. 

## <a name="creation-of-web-service"></a>Tworzenie usługi sieci web
> Ta usługa sieci web został utworzony przy użyciu usługi Azure Machine Learning. Bezpłatna wersja próbna, a także wprowadzające filmy wideo dotyczące tworzenia eksperymenty i [publikowania usług sieci web](machine-learning-publish-a-machine-learning-web-service.md), można znaleźć pod adresem [azure.com/ml](http://azure.com/ml). Poniżej przedstawiono zrzut ekranu doświadczenia utworzony kod przykład i usługi sieci web dla każdego z modułów w ramach eksperymentu.
> 
> 

Za pomocą w usłudze Azure Machine Learning nowy pusty eksperyment została utworzona. Na poniższym rysunku przedstawiono przepływ eksperymentu analizy na podstawie leksykonie wskaźniki nastrojów klientów. Plik "sent_dict.csv" jest leksykonie subiektywnej oceny MPQA i jest ustawiony jako jedno z wejść z [wykonanie skryptu języka R][execute-r-script]. Inny danych wejściowych jest próbkowany przeglądu z zestawu danych przeglądu Amazon dla testu, w którym możemy wykonać wybór, zmiana nazwy kolumny i podziałem operacji. Używamy pakietu skrót do przechowywania leksykonie subiektywnej oceny w pamięci i przyspieszyć proces wyników obliczeń. Cały tekst zostanie stokenizowanego przez pakiet "tm" i w porównaniu z programu word w słowniku wskaźniki nastrojów klientów. Na koniec wynikiem będzie obliczana przez dodanie wagę każdego wyrazu subiektywne w tekście. 

### <a name="experiment-flow"></a>Przepływ eksperymentu:
![Przepływ eksperymentu][2]

#### <a name="module-1"></a>Moduł 1:
    # Map 1-based optional input ports to variables
    sent_dict_data<- maml.mapInputPort(1) # class: data.frame
    dataset2 <- maml.mapInputPort(2) # class: data.frame

# <a name="install-hash-package"></a>Zainstaluj pakiet wyznaczania wartości skrótu
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

    # Select data.frame to be sent to the output Dataset port
    maml.mapOutputPort("data.set")



## <a name="limitations"></a>Ograniczenia
Z perspektywy algorytm analizy na podstawie leksykonie wskaźniki nastrojów klientów jest narzędzie analizy ogólne wskaźniki nastrojów klientów, które mogą nie działać lepiej niż metody klasyfikacji dla określonych pól. Problem negacji nie jest również uwzględnione. Firma Microsoft kodowania negacji kilka wyrazów w naszym programu, ale lepiej jest za pomocą słownika negacji i niektóre reguły kompilacji. Usługa sieci web dokonuje lepiej na krótka i prosta zdań, takich jak tweetów i ogłoszeń Facebook, niż zdań długich i złożonych, takie jak recenzje Amazon. 

## <a name="faq"></a>Często zadawane pytania
Często zadawane pytania dotyczące wykorzystania usługi sieci web i publikowanie w portalu Azure Marketplace, zobacz [tutaj](machine-learning-marketplace-faq.md).

[1]: ./media/machine-learning-r-csharp-lexicon-based-sentiment-analysis/sentiment_analysis_1.png
[2]: ./media/machine-learning-r-csharp-lexicon-based-sentiment-analysis/sentiment_analysis_2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/


