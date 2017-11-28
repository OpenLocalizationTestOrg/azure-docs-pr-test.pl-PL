---
title: "Różnica w teście proporcje - Azure aaa(deprecated) | Dokumentacja firmy Microsoft"
description: "(przestarzałe) Różnica w teście proporcji"
services: machine-learning
documentationcenter: 
author: aniedea
manager: jhubbard
editor: cgronlun
ms.assetid: 9356b821-5345-44f6-8e26-719f2dea5e6d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: aniedea
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: 820aad377f9dec12b0ef455974aaa95f6e8d723a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-difference-in-proportions-test"></a><span data-ttu-id="904ea-103">(przestarzałe) Różnica w teście proporcji</span><span class="sxs-lookup"><span data-stu-id="904ea-103">(deprecated) Difference in Proportions Test</span></span>

> [!NOTE]
> <span data-ttu-id="904ea-104">Witaj Microsoft DataMarket została wycofana i ten interfejs API jest przestarzały.</span><span class="sxs-lookup"><span data-stu-id="904ea-104">hello Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="904ea-105">Możesz znaleźć wiele interfejsów API i przydatne przykład eksperymenty w hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="904ea-105">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="904ea-106">Aby uzyskać więcej informacji na temat hello galerii, zobacz [udziału i odnajdywania zasobów w hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="904ea-106">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="904ea-107">Różnią się dwóch proporcji statystycznie?</span><span class="sxs-lookup"><span data-stu-id="904ea-107">Are two proportions statistically different?</span></span> <span data-ttu-id="904ea-108">Załóżmy, że użytkownik chce, aby toodetermine filmy toocompare dwa, jeśli jeden film jest znacznie wyższa część "lubi" kiedy porównaniu toohello innych.</span><span class="sxs-lookup"><span data-stu-id="904ea-108">Suppose a user wants toocompare two movies toodetermine if one movie has a significantly higher proportion of ‘likes’ when compared toohello other.</span></span> <span data-ttu-id="904ea-109">Z przykładowym duży może być statystycznie znacząca różnica między proporcje hello 0,50 i 0,51.</span><span class="sxs-lookup"><span data-stu-id="904ea-109">With a large sample, there could be a statistically significant difference between hello proportions 0.50 and 0.51.</span></span> <span data-ttu-id="904ea-110">Z małej przykładowej prawdopodobnie toodetermine wystarczającej ilości danych jeśli proporcje te są faktycznie różne.</span><span class="sxs-lookup"><span data-stu-id="904ea-110">With a small sample, there may not be enough data toodetermine if these proportions are actually different.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="904ea-111">To [usługi sieci web](https://datamarket.azure.com/dataset/aml_labs/prop_test) przeprowadza test hipoteza hello różnica dwóch proporcji oparte na danych wejściowych użytkownika hello liczbę sukcesów i hello łączna liczba prób dla grup porównania hello 2.</span><span class="sxs-lookup"><span data-stu-id="904ea-111">This [web service](https://datamarket.azure.com/dataset/aml_labs/prop_test) conducts a hypothesis test of hello difference in two proportions based on user input of hello number of successes and hello total number of trials for hello 2 comparison groups.</span></span> <span data-ttu-id="904ea-112">Możliwy scenariusz tej usługi sieci web może być wywołana z poziomu movie app porównania, informuje użytkownika hello czy jedną filmy hello jest naprawdę "zbędne" częściej niż hello inne, na podstawie filmu klasyfikacji.</span><span class="sxs-lookup"><span data-stu-id="904ea-112">In one possible scenario, this web service could be called from within a movie comparison app, telling hello user whether one of hello movies is really ‘liked’ more often than hello other, based on movie ratings.</span></span>

> <span data-ttu-id="904ea-113">Ta usługa sieci web może być używana przez użytkowników — potencjalnie za pomocą aplikacji mobilnej, za pośrednictwem witryny sieci Web lub nawet na komputerze lokalnym, na przykład.</span><span class="sxs-lookup"><span data-stu-id="904ea-113">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="904ea-114">Ale hello hello usługi sieci web służy również tooserve, na przykład jak usługi Azure Machine Learning można toocreate używanych usług sieci web na podstawie kodu języka R.</span><span class="sxs-lookup"><span data-stu-id="904ea-114">But hello purpose of hello web service is also tooserve as an example of how Azure Machine Learning can be used toocreate web services on top of R code.</span></span> <span data-ttu-id="904ea-115">Przy użyciu kilku wierszy kodu języka R i kliknięcia przycisku w usłudze Azure Machine Learning Studio eksperyment można tworzyć z kodem R i opublikowane jako usługę sieci web.</span><span class="sxs-lookup"><span data-stu-id="904ea-115">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="904ea-116">usługi sieci web Hello można następnie toohello opublikowane w portalu Azure Marketplace i używane przez użytkowników i urządzeń w Witaj świecie bez ustawień infrastruktury przez autora hello hello usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="904ea-116">hello web service can then be published toohello Azure Marketplace and consumed by users and devices across hello world with no infrastructure setup by hello author of hello web service.</span></span>
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="904ea-117">Użycie usługi sieci web</span><span class="sxs-lookup"><span data-stu-id="904ea-117">Consumption of web service</span></span>
<span data-ttu-id="904ea-118">Ta usługa akceptuje argumenty 4, i jest hipoteza testowych proporcji.</span><span class="sxs-lookup"><span data-stu-id="904ea-118">This service accepts 4 arguments and does a hypothesis test of proportions.</span></span>

<span data-ttu-id="904ea-119">argumenty wejściowe Hello są:</span><span class="sxs-lookup"><span data-stu-id="904ea-119">hello input arguments are:</span></span>

* <span data-ttu-id="904ea-120">Successes1 — liczba zdarzeń pomyślnego w przykładzie 1.</span><span class="sxs-lookup"><span data-stu-id="904ea-120">Successes1 - Number of success events in sample 1.</span></span>
* <span data-ttu-id="904ea-121">Successes2 — liczba zdarzeń pomyślnego w przykładzie 2.</span><span class="sxs-lookup"><span data-stu-id="904ea-121">Successes2 - Number of success events in sample 2.</span></span>
* <span data-ttu-id="904ea-122">Total1 — rozmiar próbki 1.</span><span class="sxs-lookup"><span data-stu-id="904ea-122">Total1 -  Size of sample 1.</span></span>
* <span data-ttu-id="904ea-123">Total2 — rozmiar próbki 2.</span><span class="sxs-lookup"><span data-stu-id="904ea-123">Total2 - Size of sample 2.</span></span>

<span data-ttu-id="904ea-124">dane wyjściowe Hello usługi hello jest wynikiem hello hipoteza hello test wraz z hello chi-square Statystyka, df, p wartość, a udział procentowy w granice 1/2 i przedział ufności próbki.</span><span class="sxs-lookup"><span data-stu-id="904ea-124">hello output of hello service is hello result of hello hypothesis test along with hello chi-square statistic, df, p-value, and proportion in sample 1/2 and confidence interval bounds.</span></span>

> <span data-ttu-id="904ea-125">Ta usługa hostowana na hello Azure Marketplace jest usługi OData; te można wywoływać za pomocą metody POST lub GET.</span><span class="sxs-lookup"><span data-stu-id="904ea-125">This service, as hosted on hello Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="904ea-126">Istnieje wiele sposobów używania usługi hello w zautomatyzowany sposób (przykładową aplikację jest [tutaj](http://microsoftazuremachinelearning.azurewebsites.net/DifferenceInProportionsTest.aspx)).</span><span class="sxs-lookup"><span data-stu-id="904ea-126">There are multiple ways of consuming hello service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/DifferenceInProportionsTest.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="904ea-127">Rozpoczynanie korzystania z usług sieci web kod C#:</span><span class="sxs-lookup"><span data-stu-id="904ea-127">Starting C# code for web service consumption:</span></span>
    public class Input
    {
            public string successes1;
            public string successes2;
            public string total1;
            public string total2;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { successes1 = TextBox1.Text, successes2 = TextBox2.Text, total1 = TextBox3.Text, total2 = TextBox4.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }


## <a name="creation-of-web-service"></a><span data-ttu-id="904ea-128">Tworzenie usługi sieci web</span><span class="sxs-lookup"><span data-stu-id="904ea-128">Creation of web service</span></span>
> <span data-ttu-id="904ea-129">Ta usługa sieci web został utworzony przy użyciu usługi Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="904ea-129">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="904ea-130">Bezpłatna wersja próbna, a także wprowadzające filmy wideo dotyczące tworzenia eksperymenty i [publikowania usług sieci web](machine-learning-publish-a-machine-learning-web-service.md), można znaleźć pod adresem [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="904ea-130">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="904ea-131">Poniżej przedstawiono zrzut ekranu hello eksperymentu, utworzona hello kod przykład i usługi sieci web dla każdego z modułów hello w ramach eksperymentu hello.</span><span class="sxs-lookup"><span data-stu-id="904ea-131">Below is a screenshot of hello experiment that created hello web service and example code for each of hello modules within hello experiment.</span></span>
> 
> 

<span data-ttu-id="904ea-132">Za pomocą w usłudze Azure Machine Learning nowy pusty eksperyment została utworzona przy użyciu dwóch [wykonanie skryptu języka R] [ execute-r-script] modułów.</span><span class="sxs-lookup"><span data-stu-id="904ea-132">From within Azure Machine Learning, a new blank experiment was created with two [Execute R Script][execute-r-script] modules.</span></span> <span data-ttu-id="904ea-133">W module pierwszy hello hello schemat danych jest zdefiniowana, gdy drugi moduł hello używa polecenia prop.test hello R tooperform hello hipotetyczny test proporcje 2.</span><span class="sxs-lookup"><span data-stu-id="904ea-133">In hello first module hello data schema is defined, while hello second module uses hello prop.test command within R tooperform hello hypothesis test for 2 proportions.</span></span> 

### <a name="experiment-flow"></a><span data-ttu-id="904ea-134">Przepływ eksperymentu:</span><span class="sxs-lookup"><span data-stu-id="904ea-134">Experiment flow:</span></span>
![Przepływ eksperymentu][2]

#### <a name="module-1"></a><span data-ttu-id="904ea-136">Moduł 1:</span><span class="sxs-lookup"><span data-stu-id="904ea-136">Module 1:</span></span>
    ####Schema definition  
    data.set=data.frame(successes1=50,successes2=60,total1=100,total2=100);
    maml.mapOutputPort("data.set"); #send data toooutput port
    dataset1 = maml.mapInputPort(1) #read data from input port


#### <a name="module-2"></a><span data-ttu-id="904ea-137">Moduł 2:</span><span class="sxs-lookup"><span data-stu-id="904ea-137">Module 2:</span></span>
    test=prop.test(c(dataset1$successes1[1],dataset1$successes2[1]),c(dataset1$total1[1],dataset1$total2[1])) #conduct hypothesis test

    result=data.frame(
    result=ifelse(test$p.value<0.05,"hello proportions are different!",
    "hello proportions aren't different statistically."),
    ChiSquarestatistic=round(test$statistic,2),df=test$parameter,
    pvalue=round(test$p.value,4),
    proportion1=round(test$estimate[1],4),
    proportion2=round(test$estimate[2],4),
    confintlow=round(test$conf.int[1],4),
    confinthigh=round(test$conf.int[2],4)) 

    maml.mapOutputPort("result"); #output port


## <a name="limitations"></a><span data-ttu-id="904ea-138">Ograniczenia</span><span class="sxs-lookup"><span data-stu-id="904ea-138">Limitations</span></span>
<span data-ttu-id="904ea-139">Jest bardzo prosty przykład dla testu różnicy w proporcjach 2.</span><span class="sxs-lookup"><span data-stu-id="904ea-139">This is a very simple example for a test of difference in 2 proportions.</span></span> <span data-ttu-id="904ea-140">Jak wynika z powyższych hello przykładowy kod, nie błąd Przechwytywanie jest zaimplementowany i usługi hello zakłada, że wszystkie zmienne hello są ciągłe.</span><span class="sxs-lookup"><span data-stu-id="904ea-140">As can be seen from hello example code above, no error catching is implemented and hello service assumes that all hello variables are continuous.</span></span>

## <a name="faq"></a><span data-ttu-id="904ea-141">Często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="904ea-141">FAQ</span></span>
<span data-ttu-id="904ea-142">Często zadawane pytania dotyczące wykorzystania hello usługi sieci web lub toohello publikowania portalu Azure Marketplace, zobacz [tutaj](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="904ea-142">For frequently asked questions on consumption of hello web service or publishing toohello Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-difference-in-two-proportions/hyptest-img1.png
[2]: ./media/machine-learning-r-csharp-difference-in-two-proportions/hyptest-img2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

