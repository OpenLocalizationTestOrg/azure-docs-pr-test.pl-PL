---
title: "(przestarzałe) Różnica w teście proporcje - Azure | Dokumentacja firmy Microsoft"
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
redirect_document_id: TRUE
ms.openlocfilehash: a08f91ca76eef2562caeb9eb64cec5e549ed2f5f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-difference-in-proportions-test"></a><span data-ttu-id="0742d-103">(przestarzałe) Różnica w teście proporcji</span><span class="sxs-lookup"><span data-stu-id="0742d-103">(deprecated) Difference in Proportions Test</span></span>

> [!NOTE]
> <span data-ttu-id="0742d-104">Microsoft DataMarket została wycofana i ten interfejs API jest przestarzały.</span><span class="sxs-lookup"><span data-stu-id="0742d-104">The Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="0742d-105">Możesz znaleźć wiele eksperymenty przykład przydatne i interfejsów API w [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="0742d-105">You can find many useful example experiments and APIs in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="0742d-106">Aby uzyskać więcej informacji o galerii, zobacz [udziału i odnajdywania zasobów w Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="0742d-106">For more information about the Gallery, see [Share and discover resources in the Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="0742d-107">Różnią się dwóch proporcji statystycznie?</span><span class="sxs-lookup"><span data-stu-id="0742d-107">Are two proportions statistically different?</span></span> <span data-ttu-id="0742d-108">Załóżmy, że użytkownik chce, aby porównać dwa filmów, aby sprawdzić, czy jeden film jest znacznie wyższa część "lubi" Kiedy w porównaniu do drugiego.</span><span class="sxs-lookup"><span data-stu-id="0742d-108">Suppose a user wants to compare two movies to determine if one movie has a significantly higher proportion of ‘likes’ when compared to the other.</span></span> <span data-ttu-id="0742d-109">Z przykładowym duży może być statystycznie znacząca różnica między proporcje 0,50 i 0,51.</span><span class="sxs-lookup"><span data-stu-id="0742d-109">With a large sample, there could be a statistically significant difference between the proportions 0.50 and 0.51.</span></span> <span data-ttu-id="0742d-110">Przy małej przykładowej prawdopodobnie za mało danych do ustalenia, czy te proporcje są faktycznie różnych.</span><span class="sxs-lookup"><span data-stu-id="0742d-110">With a small sample, there may not be enough data to determine if these proportions are actually different.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="0742d-111">To [usługi sieci web](https://datamarket.azure.com/dataset/aml_labs/prop_test) przeprowadza test hipoteza różnica dwóch proporcji oparte na danych wejściowych użytkownika liczbę sukcesów i łączna liczba prób dla grupy 2 porównania.</span><span class="sxs-lookup"><span data-stu-id="0742d-111">This [web service](https://datamarket.azure.com/dataset/aml_labs/prop_test) conducts a hypothesis test of the difference in two proportions based on user input of the number of successes and the total number of trials for the 2 comparison groups.</span></span> <span data-ttu-id="0742d-112">Możliwy scenariusz tej usługi sieci web może być wywołana z poziomu movie app porównania, informujący użytkownika, czy jeden filmów jest naprawdę "zbędne" częściej niż inne, na podstawie filmu klasyfikacji.</span><span class="sxs-lookup"><span data-stu-id="0742d-112">In one possible scenario, this web service could be called from within a movie comparison app, telling the user whether one of the movies is really ‘liked’ more often than the other, based on movie ratings.</span></span>

> <span data-ttu-id="0742d-113">Ta usługa sieci web może być używana przez użytkowników — potencjalnie za pomocą aplikacji mobilnej, za pośrednictwem witryny sieci Web lub nawet na komputerze lokalnym, na przykład.</span><span class="sxs-lookup"><span data-stu-id="0742d-113">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="0742d-114">Ale celem usługi sieci web jest również służyć jako przykład sposobu użycia usługi Azure Machine Learning do tworzenia usług sieci web na podstawie kodu języka R.</span><span class="sxs-lookup"><span data-stu-id="0742d-114">But the purpose of the web service is also to serve as an example of how Azure Machine Learning can be used to create web services on top of R code.</span></span> <span data-ttu-id="0742d-115">Przy użyciu kilku wierszy kodu języka R i kliknięcia przycisku w usłudze Azure Machine Learning Studio eksperyment można tworzyć z kodem R i opublikowane jako usługę sieci web.</span><span class="sxs-lookup"><span data-stu-id="0742d-115">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="0742d-116">Usługi sieci web może następnie opublikowane w portalu Azure Marketplace i używane przez użytkowników i urządzeń w całym świecie bez ustawień infrastruktury przez autora usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="0742d-116">The web service can then be published to the Azure Marketplace and consumed by users and devices across the world with no infrastructure setup by the author of the web service.</span></span>
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="0742d-117">Użycie usługi sieci web</span><span class="sxs-lookup"><span data-stu-id="0742d-117">Consumption of web service</span></span>
<span data-ttu-id="0742d-118">Ta usługa akceptuje argumenty 4, i jest hipoteza testowych proporcji.</span><span class="sxs-lookup"><span data-stu-id="0742d-118">This service accepts 4 arguments and does a hypothesis test of proportions.</span></span>

<span data-ttu-id="0742d-119">Argumenty wejściowe są:</span><span class="sxs-lookup"><span data-stu-id="0742d-119">The input arguments are:</span></span>

* <span data-ttu-id="0742d-120">Successes1 — liczba zdarzeń pomyślnego w przykładzie 1.</span><span class="sxs-lookup"><span data-stu-id="0742d-120">Successes1 - Number of success events in sample 1.</span></span>
* <span data-ttu-id="0742d-121">Successes2 — liczba zdarzeń pomyślnego w przykładzie 2.</span><span class="sxs-lookup"><span data-stu-id="0742d-121">Successes2 - Number of success events in sample 2.</span></span>
* <span data-ttu-id="0742d-122">Total1 — rozmiar próbki 1.</span><span class="sxs-lookup"><span data-stu-id="0742d-122">Total1 -  Size of sample 1.</span></span>
* <span data-ttu-id="0742d-123">Total2 — rozmiar próbki 2.</span><span class="sxs-lookup"><span data-stu-id="0742d-123">Total2 - Size of sample 2.</span></span>

<span data-ttu-id="0742d-124">Dane wyjściowe usługi jest wynikiem hipotezę test wraz z chi-square Statystyka, df, p wartość, a udział procentowy w granice 1/2 i przedział ufności próbki.</span><span class="sxs-lookup"><span data-stu-id="0742d-124">The output of the service is the result of the hypothesis test along with the chi-square statistic, df, p-value, and proportion in sample 1/2 and confidence interval bounds.</span></span>

> <span data-ttu-id="0742d-125">Ta usługa hostowana w portalu Azure Marketplace jest usługi OData; te można wywoływać za pomocą metody POST lub GET.</span><span class="sxs-lookup"><span data-stu-id="0742d-125">This service, as hosted on the Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="0742d-126">Istnieje wiele sposobów używania usługi w zautomatyzowany sposób (przykładową aplikację jest [tutaj](http://microsoftazuremachinelearning.azurewebsites.net/DifferenceInProportionsTest.aspx)).</span><span class="sxs-lookup"><span data-stu-id="0742d-126">There are multiple ways of consuming the service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/DifferenceInProportionsTest.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="0742d-127">Rozpoczynanie korzystania z usług sieci web kod C#:</span><span class="sxs-lookup"><span data-stu-id="0742d-127">Starting C# code for web service consumption:</span></span>
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


## <a name="creation-of-web-service"></a><span data-ttu-id="0742d-128">Tworzenie usługi sieci web</span><span class="sxs-lookup"><span data-stu-id="0742d-128">Creation of web service</span></span>
> <span data-ttu-id="0742d-129">Ta usługa sieci web został utworzony przy użyciu usługi Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="0742d-129">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="0742d-130">Bezpłatna wersja próbna, a także wprowadzające filmy wideo dotyczące tworzenia eksperymenty i [publikowania usług sieci web](machine-learning-publish-a-machine-learning-web-service.md), można znaleźć pod adresem [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="0742d-130">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="0742d-131">Poniżej przedstawiono zrzut ekranu doświadczenia utworzony kod przykład i usługi sieci web dla każdego z modułów w ramach eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="0742d-131">Below is a screenshot of the experiment that created the web service and example code for each of the modules within the experiment.</span></span>
> 
> 

<span data-ttu-id="0742d-132">Za pomocą w usłudze Azure Machine Learning nowy pusty eksperyment została utworzona przy użyciu dwóch [wykonanie skryptu języka R] [ execute-r-script] modułów.</span><span class="sxs-lookup"><span data-stu-id="0742d-132">From within Azure Machine Learning, a new blank experiment was created with two [Execute R Script][execute-r-script] modules.</span></span> <span data-ttu-id="0742d-133">W pierwszym moduł, który jest zdefiniowany schemat danych a druga modułu używa prop.test polecenia w R do przeprowadzenia testu hipoteza proporcje 2.</span><span class="sxs-lookup"><span data-stu-id="0742d-133">In the first module the data schema is defined, while the second module uses the prop.test command within R to perform the hypothesis test for 2 proportions.</span></span> 

### <a name="experiment-flow"></a><span data-ttu-id="0742d-134">Przepływ eksperymentu:</span><span class="sxs-lookup"><span data-stu-id="0742d-134">Experiment flow:</span></span>
![Przepływ eksperymentu][2]

#### <a name="module-1"></a><span data-ttu-id="0742d-136">Moduł 1:</span><span class="sxs-lookup"><span data-stu-id="0742d-136">Module 1:</span></span>
    ####Schema definition  
    data.set=data.frame(successes1=50,successes2=60,total1=100,total2=100);
    maml.mapOutputPort("data.set"); #send data to output port
    dataset1 = maml.mapInputPort(1) #read data from input port


#### <a name="module-2"></a><span data-ttu-id="0742d-137">Moduł 2:</span><span class="sxs-lookup"><span data-stu-id="0742d-137">Module 2:</span></span>
    test=prop.test(c(dataset1$successes1[1],dataset1$successes2[1]),c(dataset1$total1[1],dataset1$total2[1])) #conduct hypothesis test

    result=data.frame(
    result=ifelse(test$p.value<0.05,"The proportions are different!",
    "The proportions aren't different statistically."),
    ChiSquarestatistic=round(test$statistic,2),df=test$parameter,
    pvalue=round(test$p.value,4),
    proportion1=round(test$estimate[1],4),
    proportion2=round(test$estimate[2],4),
    confintlow=round(test$conf.int[1],4),
    confinthigh=round(test$conf.int[2],4)) 

    maml.mapOutputPort("result"); #output port


## <a name="limitations"></a><span data-ttu-id="0742d-138">Ograniczenia</span><span class="sxs-lookup"><span data-stu-id="0742d-138">Limitations</span></span>
<span data-ttu-id="0742d-139">Jest bardzo prosty przykład dla testu różnicy w proporcjach 2.</span><span class="sxs-lookup"><span data-stu-id="0742d-139">This is a very simple example for a test of difference in 2 proportions.</span></span> <span data-ttu-id="0742d-140">Jak wynika z przykładowy kod powyżej, nie błąd Przechwytywanie jest zaimplementowany i usługa zakłada, że wszystkie zmienne są ciągłe.</span><span class="sxs-lookup"><span data-stu-id="0742d-140">As can be seen from the example code above, no error catching is implemented and the service assumes that all the variables are continuous.</span></span>

## <a name="faq"></a><span data-ttu-id="0742d-141">Często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="0742d-141">FAQ</span></span>
<span data-ttu-id="0742d-142">Często zadawane pytania dotyczące wykorzystania usługi sieci web i publikowanie w portalu Azure Marketplace, zobacz [tutaj](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="0742d-142">For frequently asked questions on consumption of the web service or publishing to the Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-difference-in-two-proportions/hyptest-img1.png
[2]: ./media/machine-learning-r-csharp-difference-in-two-proportions/hyptest-img2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

