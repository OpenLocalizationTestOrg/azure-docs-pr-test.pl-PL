---
title: AAA(deprecated) modelu klastra - Azure | Dokumentacja firmy Microsoft
description: "(przestarzałe) Model klastra"
services: machine-learning
documentationcenter: 
author: FrancescaLazzeri
manager: jhubbard
editor: cgronlun
ms.assetid: 51b8d012-ed44-4312-920c-9c808dfd4ff6
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: lazzeri
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: 7b2dffb855a8d91114752b579115e97d07210e45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-cluster-model"></a>(przestarzałe) Model klastra

> [!NOTE]
> Witaj Microsoft DataMarket została wycofana i ten interfejs API jest przestarzały. 
> 
> Możesz znaleźć wiele interfejsów API i przydatne przykład eksperymenty w hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com). Aby uzyskać więcej informacji na temat hello galerii, zobacz [udziału i odnajdywania zasobów w hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).

Jak możemy przewidzieć grup zachowania posiadacze kart mający środki w kolejności tooreduce hello opłat poza ryzyko wystawców karty kredytowej Można zdefiniować grupy cech charakteru pracowników w kolejności tooimprove ich działania w miejscu pracy? Jak lekarzy klasyfikowania pacjentów na grupy na podstawie charakterystyk hello ich chorób Zasadniczo wszystkie te pytania można odpowiedzi za pomocą analizy klastra.   

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Analiza klastra klasyfikuje zestaw z uwagi na co najmniej dwa wykluczają się wzajemnie nieznany grupy na podstawie kombinacji zmiennych. Celem Hello analizy klastra to toodiscover systemu organizacji uwagi, zwykle osób lub ich właściwości, do grup, których członkami grup hello właściwości wspólnych. To [usługi](https://datamarket.azure.com/dataset/aml_labs/k_cluster_model) używa hello K-średnich metodologii, często używane techniki klastrowania toocluster dowolnych danych w grupach. Tej usługi sieci web pobiera dane hello i hello liczba k klastrów jako dane wejściowe i tworzy prognoz, którego toowhich grup k hello należy każdego uwag. 

> Ta usługa sieci web może być używana przez użytkowników — potencjalnie za pomocą aplikacji mobilnej, za pośrednictwem witryny sieci Web lub nawet na komputerze lokalnym, na przykład. Ale hello hello usługi sieci web służy również tooserve, na przykład jak usługi Azure Machine Learning można toocreate używanych usług sieci web na podstawie kodu języka R. Przy użyciu kilku wierszy kodu języka R i kliknięcia przycisku w usłudze Azure Machine Learning Studio eksperyment można tworzyć z kodem R i opublikowane jako usługę sieci web. usługi sieci web Hello można następnie toohello opublikowane w portalu Azure Marketplace i używane przez użytkowników i urządzeń w Witaj świecie bez ustawień infrastruktury przez autora hello hello usługi sieci web.  
> 
> 

## <a name="consumption-of-web-service"></a>Użycie usługi sieci web
Ta usługa sieci web grupuje dane hello na zestaw k grup i dane wyjściowe hello przypisanie do grupy dla każdego wiersza. Usługa sieci web Hello oczekuje hello użytkownika końcowego tooinput dane jako ciąg, gdzie wiersze są oddzielone przecinkami (,), a kolumny oddzielonych średnikami (;). Usługa sieci web Hello oczekuje 1 wiersz naraz. Przykład zestawu danych może wyglądać następująco:

![Dane przykładowe][1]

Załóżmy, że tooseparate użytkownik chciał hello tych danych na 3 grupy wykluczają się wzajemnie. Witaj danych wejściowych dla hello powyżej zestawu danych będą następujące hello: wartość = "10 5; 2,18; 1; 6,7; 5; 5,22; 3; 4,12; 2; 1,10; 3; 4"; k = "3". dane wyjściowe Hello jest hello członkostwa w grupie przewidywane dla każdego hello wierszy.

> Ta usługa hostowana na hello Azure Marketplace jest usługi OData; te można wywoływać za pomocą metody POST lub GET. 
> 
> 

Istnieje wiele sposobów używania usługi hello w zautomatyzowany sposób (przykładową aplikację jest [tutaj](http://microsoftazuremachinelearning.azurewebsites.net/ClusterModel.aspx)).

### <a name="starting-c-code-for-web-service-consumption"></a>Rozpoczynanie korzystania z usług sieci web kod C#:
    public class Input
    {
            public string value;
            public string k;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { value = TextBox1.Text, k = TextBox2.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }




## <a name="creation-of-web-service"></a>Tworzenie usługi sieci web
> Ta usługa sieci web został utworzony przy użyciu usługi Azure Machine Learning. Bezpłatna wersja próbna, a także wprowadzające filmy wideo dotyczące tworzenia eksperymenty i [publikowania usług sieci web](machine-learning-publish-a-machine-learning-web-service.md), można znaleźć pod adresem [azure.com/ml](http://azure.com/ml). Poniżej przedstawiono zrzut ekranu hello eksperymentu, utworzona hello kod przykład i usługi sieci web dla każdego z modułów hello w ramach eksperymentu hello.
> 
> 

Za pomocą w usłudze Azure Machine Learning nowy pusty eksperyment została utworzona i dwa [wykonanie skryptu języka R] [ execute-r-script] modułów pobierane na powitania obszaru roboczego. Schemat danych Hello został utworzony przy użyciu prostego [wykonanie skryptu języka R][execute-r-script]. Następnie hello schemat danych został połączony toohello klastra sekcji modelu, ponownie utworzone za pomocą [wykonanie skryptu języka R][execute-r-script]. W hello [wykonanie skryptu języka R] [ execute-r-script] używana na potrzeby modelu klastra hello, usługa sieci web hello następnie korzysta z funkcji "k średnich" hello, która jest wbudowane w hello [wykonanie skryptu języka R] [ execute-r-script] z usługi Azure Machine Learning.    

![Przepływ eksperymentu][3]

#### <a name="module-1"></a>Moduł 1:
    #Enter hello input data as a string 
    mydata <- data.frame(value = "1; 3; 5; 6; 7; 7, 5; 5; 6; 7; 2; 1, 3; 7; 2; 9; 56; 6, 1; 4; 5; 26; 4; 23, 15; 35; 6; 7; 12; 1, 32; 51; 62; 7; 21; 1", k=5, stringsAsFactors=FALSE)

    maml.mapOutputPort("mydata");     


#### <a name="module-2"></a>Moduł 2:
    # Map 1-based optional input ports toovariables
    mydata <- maml.mapInputPort(1) # class: data.frame

    data.split <- strsplit(mydata[1,1], ",")[[1]]
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE)
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE)
    data.split <- as.data.frame(t(data.split))

    data.split <- data.matrix(data.split)
    data.split <- data.frame(data.split)

    # K-Means cluster analysis
    fit <- kmeans(data.split, mydata$k) # k-cluster solution

    # Get cluster means 
    aggregate(data.split,by=list(fit$cluster),FUN=mean)
    # Append cluster assignment
    mydatafinal <- data.frame(t(fit$cluster))
    n_col=ncol(mydatafinal)
    colnames(mydatafinal) <- paste("V",1:n_col,sep="")

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("mydatafinal");


## <a name="limitations"></a>Ograniczenia
Jest bardzo prosty przykład klastrowania usługi sieci web. Jak wynika z powyższych hello przykładowy kod, nie błąd Przechwytywanie jest zaimplementowana i usługi hello przyjęto założenie, że wszystko jest ciągłe zmiennej (nie podzielone na kategorie funkcji dozwolone), jako hello usługi tylko dane wejściowe wartości liczbowe w czasie hello hello tworzenia tej sieci Web Usługa. Ponadto usługa hello obsługuje obecnie rozmiar ograniczoną ilość danych, powodu toohello charakter żądanie/odpowiedź usługi sieci web hello połączeń i hello fakt, że hello modelu jest nadaje się zawsze nosi nazwę usługi sieci web hello. 

## <a name="faq"></a>Często zadawane pytania
Często zadawane pytania dotyczące wykorzystania hello usługi sieci web lub toohello publikowania portalu Azure Marketplace, zobacz [tutaj](machine-learning-marketplace-faq.md).

[1]: ./media/machine-learning-r-csharp-cluster-model/cluster-img1.png
[2]: ./media/machine-learning-r-csharp-cluster-model/cluster-img2.png
[3]: ./media/machine-learning-r-csharp-cluster-model/cluster-img3.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

