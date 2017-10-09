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
# <a name="deprecated-cluster-model"></a><span data-ttu-id="f9018-103">(przestarzałe) Model klastra</span><span class="sxs-lookup"><span data-stu-id="f9018-103">(deprecated) Cluster Model</span></span>

> [!NOTE]
> <span data-ttu-id="f9018-104">Witaj Microsoft DataMarket została wycofana i ten interfejs API jest przestarzały.</span><span class="sxs-lookup"><span data-stu-id="f9018-104">hello Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="f9018-105">Możesz znaleźć wiele interfejsów API i przydatne przykład eksperymenty w hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="f9018-105">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="f9018-106">Aby uzyskać więcej informacji na temat hello galerii, zobacz [udziału i odnajdywania zasobów w hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="f9018-106">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="f9018-107">Jak możemy przewidzieć grup zachowania posiadacze kart mający środki w kolejności tooreduce hello opłat poza ryzyko wystawców karty kredytowej</span><span class="sxs-lookup"><span data-stu-id="f9018-107">How can we predict groups of credit cardholders’ behaviors in order tooreduce hello charge-off risk of credit card issuers?</span></span> <span data-ttu-id="f9018-108">Można zdefiniować grupy cech charakteru pracowników w kolejności tooimprove ich działania w miejscu pracy?</span><span class="sxs-lookup"><span data-stu-id="f9018-108">How can we define groups of personality traits of employees in order tooimprove their performance at work?</span></span> <span data-ttu-id="f9018-109">Jak lekarzy klasyfikowania pacjentów na grupy na podstawie charakterystyk hello ich chorób</span><span class="sxs-lookup"><span data-stu-id="f9018-109">How can doctors classify patients into groups based on hello characteristics of their diseases?</span></span> <span data-ttu-id="f9018-110">Zasadniczo wszystkie te pytania można odpowiedzi za pomocą analizy klastra.</span><span class="sxs-lookup"><span data-stu-id="f9018-110">In principle, all of these questions can be answered through cluster analysis.</span></span>   

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="f9018-111">Analiza klastra klasyfikuje zestaw z uwagi na co najmniej dwa wykluczają się wzajemnie nieznany grupy na podstawie kombinacji zmiennych.</span><span class="sxs-lookup"><span data-stu-id="f9018-111">Cluster analysis classifies a set of observations into two or more mutually exclusive unknown groups based on combinations of variables.</span></span> <span data-ttu-id="f9018-112">Celem Hello analizy klastra to toodiscover systemu organizacji uwagi, zwykle osób lub ich właściwości, do grup, których członkami grup hello właściwości wspólnych.</span><span class="sxs-lookup"><span data-stu-id="f9018-112">hello purpose of cluster analysis is toodiscover a system of organizing observations, usually people or their characteristics, into groups, where members of hello groups share properties in common.</span></span> <span data-ttu-id="f9018-113">To [usługi](https://datamarket.azure.com/dataset/aml_labs/k_cluster_model) używa hello K-średnich metodologii, często używane techniki klastrowania toocluster dowolnych danych w grupach.</span><span class="sxs-lookup"><span data-stu-id="f9018-113">This [service](https://datamarket.azure.com/dataset/aml_labs/k_cluster_model) uses hello K-Means methodology, a commonly used clustering technique, toocluster arbitrary data into groups.</span></span> <span data-ttu-id="f9018-114">Tej usługi sieci web pobiera dane hello i hello liczba k klastrów jako dane wejściowe i tworzy prognoz, którego toowhich grup k hello należy każdego uwag.</span><span class="sxs-lookup"><span data-stu-id="f9018-114">This web service takes hello data and hello number of k clusters as input, and produces predictions of which of hello k groups toowhich each observations belongs.</span></span> 

> <span data-ttu-id="f9018-115">Ta usługa sieci web może być używana przez użytkowników — potencjalnie za pomocą aplikacji mobilnej, za pośrednictwem witryny sieci Web lub nawet na komputerze lokalnym, na przykład.</span><span class="sxs-lookup"><span data-stu-id="f9018-115">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="f9018-116">Ale hello hello usługi sieci web służy również tooserve, na przykład jak usługi Azure Machine Learning można toocreate używanych usług sieci web na podstawie kodu języka R.</span><span class="sxs-lookup"><span data-stu-id="f9018-116">But hello purpose of hello web service is also tooserve as an example of how Azure Machine Learning can be used toocreate web services on top of R code.</span></span> <span data-ttu-id="f9018-117">Przy użyciu kilku wierszy kodu języka R i kliknięcia przycisku w usłudze Azure Machine Learning Studio eksperyment można tworzyć z kodem R i opublikowane jako usługę sieci web.</span><span class="sxs-lookup"><span data-stu-id="f9018-117">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="f9018-118">usługi sieci web Hello można następnie toohello opublikowane w portalu Azure Marketplace i używane przez użytkowników i urządzeń w Witaj świecie bez ustawień infrastruktury przez autora hello hello usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="f9018-118">hello web service can then be published toohello Azure Marketplace and consumed by users and devices across hello world with no infrastructure setup by hello author of hello web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="f9018-119">Użycie usługi sieci web</span><span class="sxs-lookup"><span data-stu-id="f9018-119">Consumption of web service</span></span>
<span data-ttu-id="f9018-120">Ta usługa sieci web grupuje dane hello na zestaw k grup i dane wyjściowe hello przypisanie do grupy dla każdego wiersza.</span><span class="sxs-lookup"><span data-stu-id="f9018-120">This web service groups hello data into a set of k groups and outputs hello group assignment for each row.</span></span> <span data-ttu-id="f9018-121">Usługa sieci web Hello oczekuje hello użytkownika końcowego tooinput dane jako ciąg, gdzie wiersze są oddzielone przecinkami (,), a kolumny oddzielonych średnikami (;).</span><span class="sxs-lookup"><span data-stu-id="f9018-121">hello web service expects hello end user tooinput data as a string where rows are separated by commas (,) and columns are separated by semicolons (;).</span></span> <span data-ttu-id="f9018-122">Usługa sieci web Hello oczekuje 1 wiersz naraz.</span><span class="sxs-lookup"><span data-stu-id="f9018-122">hello web service expects 1 row at a time.</span></span> <span data-ttu-id="f9018-123">Przykład zestawu danych może wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="f9018-123">An example dataset could look like this:</span></span>

![Dane przykładowe][1]

<span data-ttu-id="f9018-125">Załóżmy, że tooseparate użytkownik chciał hello tych danych na 3 grupy wykluczają się wzajemnie.</span><span class="sxs-lookup"><span data-stu-id="f9018-125">Suppose hello user wanted tooseparate this data into 3 mutually exclusive groups.</span></span> <span data-ttu-id="f9018-126">Witaj danych wejściowych dla hello powyżej zestawu danych będą następujące hello: wartość = "10 5; 2,18; 1; 6,7; 5; 5,22; 3; 4,12; 2; 1,10; 3; 4"; k = "3".</span><span class="sxs-lookup"><span data-stu-id="f9018-126">hello data input for hello above dataset would be hello following: value = “10;5;2,18;1;6,7;5;5,22;3;4,12;2;1,10;3;4”; k=”3”.</span></span> <span data-ttu-id="f9018-127">dane wyjściowe Hello jest hello członkostwa w grupie przewidywane dla każdego hello wierszy.</span><span class="sxs-lookup"><span data-stu-id="f9018-127">hello output is hello predicted group membership for each of hello rows.</span></span>

> <span data-ttu-id="f9018-128">Ta usługa hostowana na hello Azure Marketplace jest usługi OData; te można wywoływać za pomocą metody POST lub GET.</span><span class="sxs-lookup"><span data-stu-id="f9018-128">This service, as hosted on hello Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="f9018-129">Istnieje wiele sposobów używania usługi hello w zautomatyzowany sposób (przykładową aplikację jest [tutaj](http://microsoftazuremachinelearning.azurewebsites.net/ClusterModel.aspx)).</span><span class="sxs-lookup"><span data-stu-id="f9018-129">There are multiple ways of consuming hello service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/ClusterModel.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="f9018-130">Rozpoczynanie korzystania z usług sieci web kod C#:</span><span class="sxs-lookup"><span data-stu-id="f9018-130">Starting C# code for web service consumption:</span></span>
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




## <a name="creation-of-web-service"></a><span data-ttu-id="f9018-131">Tworzenie usługi sieci web</span><span class="sxs-lookup"><span data-stu-id="f9018-131">Creation of web service</span></span>
> <span data-ttu-id="f9018-132">Ta usługa sieci web został utworzony przy użyciu usługi Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="f9018-132">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="f9018-133">Bezpłatna wersja próbna, a także wprowadzające filmy wideo dotyczące tworzenia eksperymenty i [publikowania usług sieci web](machine-learning-publish-a-machine-learning-web-service.md), można znaleźć pod adresem [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="f9018-133">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="f9018-134">Poniżej przedstawiono zrzut ekranu hello eksperymentu, utworzona hello kod przykład i usługi sieci web dla każdego z modułów hello w ramach eksperymentu hello.</span><span class="sxs-lookup"><span data-stu-id="f9018-134">Below is a screenshot of hello experiment that created hello web service and example code for each of hello modules within hello experiment.</span></span>
> 
> 

<span data-ttu-id="f9018-135">Za pomocą w usłudze Azure Machine Learning nowy pusty eksperyment została utworzona i dwa [wykonanie skryptu języka R] [ execute-r-script] modułów pobierane na powitania obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="f9018-135">From within Azure Machine Learning, a new blank experiment was created and two [Execute R Script][execute-r-script] modules pulled onto hello workspace.</span></span> <span data-ttu-id="f9018-136">Schemat danych Hello został utworzony przy użyciu prostego [wykonanie skryptu języka R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="f9018-136">hello data schema was created with a simple [Execute R Script][execute-r-script].</span></span> <span data-ttu-id="f9018-137">Następnie hello schemat danych został połączony toohello klastra sekcji modelu, ponownie utworzone za pomocą [wykonanie skryptu języka R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="f9018-137">Then, hello data schema was linked toohello cluster model section, again created with an [Execute R Script][execute-r-script].</span></span> <span data-ttu-id="f9018-138">W hello [wykonanie skryptu języka R] [ execute-r-script] używana na potrzeby modelu klastra hello, usługa sieci web hello następnie korzysta z funkcji "k średnich" hello, która jest wbudowane w hello [wykonanie skryptu języka R] [ execute-r-script] z usługi Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="f9018-138">In hello [Execute R Script][execute-r-script] used for hello cluster model, hello web service then utilizes hello “k-means” function, which is prebuilt into hello [Execute R Script][execute-r-script] of Azure Machine Learning.</span></span>    

![Przepływ eksperymentu][3]

#### <a name="module-1"></a><span data-ttu-id="f9018-140">Moduł 1:</span><span class="sxs-lookup"><span data-stu-id="f9018-140">Module 1:</span></span>
    #Enter hello input data as a string 
    mydata <- data.frame(value = "1; 3; 5; 6; 7; 7, 5; 5; 6; 7; 2; 1, 3; 7; 2; 9; 56; 6, 1; 4; 5; 26; 4; 23, 15; 35; 6; 7; 12; 1, 32; 51; 62; 7; 21; 1", k=5, stringsAsFactors=FALSE)

    maml.mapOutputPort("mydata");     


#### <a name="module-2"></a><span data-ttu-id="f9018-141">Moduł 2:</span><span class="sxs-lookup"><span data-stu-id="f9018-141">Module 2:</span></span>
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


## <a name="limitations"></a><span data-ttu-id="f9018-142">Ograniczenia</span><span class="sxs-lookup"><span data-stu-id="f9018-142">Limitations</span></span>
<span data-ttu-id="f9018-143">Jest bardzo prosty przykład klastrowania usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="f9018-143">This is a very simple example of a clustering web service.</span></span> <span data-ttu-id="f9018-144">Jak wynika z powyższych hello przykładowy kod, nie błąd Przechwytywanie jest zaimplementowana i usługi hello przyjęto założenie, że wszystko jest ciągłe zmiennej (nie podzielone na kategorie funkcji dozwolone), jako hello usługi tylko dane wejściowe wartości liczbowe w czasie hello hello tworzenia tej sieci Web Usługa.</span><span class="sxs-lookup"><span data-stu-id="f9018-144">As can be seen from hello example code above, no error catching is implemented and hello service assumes everything is a continuous variable (no categorical features allowed), as hello service only inputs numeric values at hello time of hello creation of this web service.</span></span> <span data-ttu-id="f9018-145">Ponadto usługa hello obsługuje obecnie rozmiar ograniczoną ilość danych, powodu toohello charakter żądanie/odpowiedź usługi sieci web hello połączeń i hello fakt, że hello modelu jest nadaje się zawsze nosi nazwę usługi sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="f9018-145">Also, hello service currently handles limited data size, due toohello request/response nature of hello web service call and hello fact that hello model is being fit every time hello web service is called.</span></span> 

## <a name="faq"></a><span data-ttu-id="f9018-146">Często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="f9018-146">FAQ</span></span>
<span data-ttu-id="f9018-147">Często zadawane pytania dotyczące wykorzystania hello usługi sieci web lub toohello publikowania portalu Azure Marketplace, zobacz [tutaj](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="f9018-147">For frequently asked questions on consumption of hello web service or publishing toohello Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-cluster-model/cluster-img1.png
[2]: ./media/machine-learning-r-csharp-cluster-model/cluster-img2.png
[3]: ./media/machine-learning-r-csharp-cluster-model/cluster-img3.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

