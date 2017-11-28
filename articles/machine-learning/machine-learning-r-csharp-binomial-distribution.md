---
title: "(przestarzałe) Pakiet dwumianowy - Azure | Dokumentacja firmy Microsoft"
description: "(przestarzałe) Pakiet dwumianowy"
services: machine-learning
documentationcenter: 
author: ireiter
manager: jhubbard
editor: cgronlun
ms.assetid: 6d102d57-8f20-4ab3-be31-02fcfe4d15ed
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: ireiter
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: TRUE
ms.openlocfilehash: 6f0a6d06e7401c8360a92a707a0552f41ff3657c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-binomial-distribution-suite"></a><span data-ttu-id="dcf0d-103">(przestarzałe) Pakiet dwumianowy</span><span class="sxs-lookup"><span data-stu-id="dcf0d-103">(deprecated) Binomial Distribution Suite</span></span>

> [!NOTE]
> <span data-ttu-id="dcf0d-104">Microsoft DataMarket została wycofana i ten interfejs API jest przestarzały.</span><span class="sxs-lookup"><span data-stu-id="dcf0d-104">The Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="dcf0d-105">Możesz znaleźć wiele eksperymenty przykład przydatne i interfejsów API w [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="dcf0d-105">You can find many useful example experiments and APIs in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="dcf0d-106">Aby uzyskać więcej informacji o galerii, zobacz [udziału i odnajdywania zasobów w Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="dcf0d-106">For more information about the Gallery, see [Share and discover resources in the Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="dcf0d-107">Pakiet dwumianowy to zestaw usług sieci web przykładowej ([Generator dwumianowy](https://datamarket.azure.com/dataset/aml_labs/bdg5), [Kalkulator prawdopodobieństwo](https://datamarket.azure.com/dataset/aml_labs/bdp4), [Kalkulator kwantyl](https://datamarket.azure.com/dataset/aml_labs/bdq5)) ułatwiające podczas generowania i dotyczącą dwumianowy dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="dcf0d-107">The Binomial Distribution Suite is a set of sample web services ([Binomial Generator](https://datamarket.azure.com/dataset/aml_labs/bdg5), [Probability Calculator](https://datamarket.azure.com/dataset/aml_labs/bdp4), [Quantile Calculator](https://datamarket.azure.com/dataset/aml_labs/bdq5)) that help in generating and dealing with binomial distributions.</span></span> <span data-ttu-id="dcf0d-108">Usługi pozwalają generowania sekwencję dwumianowy o dowolnej długości obliczanie quantiles z podanej prawdopodobieństwo i obliczanie prawdopodobieństwa z danym kwantyl.</span><span class="sxs-lookup"><span data-stu-id="dcf0d-108">The services allow generating a binomial distribution sequence of any length, calculating quantiles out of given probability and calculating probability from a given quantile.</span></span> <span data-ttu-id="dcf0d-109">Emituje każdej z usług innej dane wyjściowe na podstawie wybranej usługi (zobacz opis poniżej).</span><span class="sxs-lookup"><span data-stu-id="dcf0d-109">Each of the services emits different outputs based on the selected service (see description below).</span></span> <span data-ttu-id="dcf0d-110">Pakiet dwumianowy opiera się na qbinom funkcje R, rbinom i pbinom, które są zawarte w pakiecie Statystyka R.</span><span class="sxs-lookup"><span data-stu-id="dcf0d-110">The Binomial Distribution Suite is based on the R functions qbinom, rbinom, and pbinom, which are included in the R stats package.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

> <span data-ttu-id="dcf0d-111">Te usługi sieci web może być używana przez użytkowników — potencjalnie bezpośrednio w portalu marketplace, za pomocą aplikacji mobilnej, za pośrednictwem witryny sieci Web lub nawet na komputerze lokalnym, na przykład.</span><span class="sxs-lookup"><span data-stu-id="dcf0d-111">These web services could be consumed by users – potentially directly on the marketplace, through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="dcf0d-112">Ale celem usługi sieci web jest również służyć jako przykład sposobu użycia usługi Azure Machine Learning do tworzenia usług sieci web na podstawie kodu języka R.</span><span class="sxs-lookup"><span data-stu-id="dcf0d-112">But the purpose of the web service is also to serve as an example of how Azure Machine Learning can be used to create web services on top of R code.</span></span> <span data-ttu-id="dcf0d-113">Przy użyciu kilku wierszy kodu języka R i kliknięcia przycisku w usłudze Azure Machine Learning Studio eksperyment można tworzyć z kodem R i opublikowane jako usługę sieci web.</span><span class="sxs-lookup"><span data-stu-id="dcf0d-113">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="dcf0d-114">Następnie usługa sieci web mogą być publikowane w portalu Azure Marketplace i używane przez użytkowników i urządzeń na całym świecie — nie konfigurowania infrastruktury przez autora usługi sieci web jest wymagana.</span><span class="sxs-lookup"><span data-stu-id="dcf0d-114">The web service can then be published to the Azure Marketplace and consumed by users and devices across the world – no infrastructure setup by the author of the web service is required.</span></span>
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="dcf0d-115">Użycie usługi sieci web</span><span class="sxs-lookup"><span data-stu-id="dcf0d-115">Consumption of web service</span></span>
<span data-ttu-id="dcf0d-116">Pakiet dwumianowy obejmują następujące usługi 3.</span><span class="sxs-lookup"><span data-stu-id="dcf0d-116">The Binomial Distribution Suite includes the following 3 services.</span></span>

### <a name="binomial-distribution-quantile-calculator"></a><span data-ttu-id="dcf0d-117">Kalkulator kwantyl dwumianowy</span><span class="sxs-lookup"><span data-stu-id="dcf0d-117">Binomial Distribution Quantile Calculator</span></span>
<span data-ttu-id="dcf0d-118">Ta usługa akceptuje 4 argumenty rozkładu normalnego i oblicza kwantyl skojarzone.</span><span class="sxs-lookup"><span data-stu-id="dcf0d-118">This service accepts 4 arguments of a normal distribution and calculates the associated quantile.</span></span>
<span data-ttu-id="dcf0d-119">Argumenty wejściowe są:</span><span class="sxs-lookup"><span data-stu-id="dcf0d-119">The input arguments are:</span></span>

* <span data-ttu-id="dcf0d-120">p - pojedynczego zagregowane prawdopodobieństwo wielu prób.</span><span class="sxs-lookup"><span data-stu-id="dcf0d-120">p - A single aggregated probability of multiple trials.</span></span>  
* <span data-ttu-id="dcf0d-121">rozmiar — liczba prób.</span><span class="sxs-lookup"><span data-stu-id="dcf0d-121">size - The number of trials.</span></span>
* <span data-ttu-id="dcf0d-122">PRAWDPD - prawdopodobieństwo sukcesu w wersji próbnej.</span><span class="sxs-lookup"><span data-stu-id="dcf0d-122">prob - The probability of success in a trial.</span></span>
* <span data-ttu-id="dcf0d-123">Strona - L stronie niższe rozkładu U dla górna część dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="dcf0d-123">Side - L for the lower side of the distribution, U for the upper side of the distribution.</span></span> 

<span data-ttu-id="dcf0d-124">Dane wyjściowe usługi jest kwantyl obliczeniowych, który jest skojarzony z danym prawdopodobieństwa.</span><span class="sxs-lookup"><span data-stu-id="dcf0d-124">The output of the service is the calculated quantile that is associated with the given probability.</span></span>

### <a name="binomial-distribution-probability-calculator"></a><span data-ttu-id="dcf0d-125">Kalkulator prawdopodobieństwo dwumianowy</span><span class="sxs-lookup"><span data-stu-id="dcf0d-125">Binomial Distribution Probability Calculator</span></span>
<span data-ttu-id="dcf0d-126">Ta usługa akceptuje 4 argumenty dwumianowy i oblicza prawdopodobieństwo skojarzone.</span><span class="sxs-lookup"><span data-stu-id="dcf0d-126">This service accepts 4 arguments of a binomial distribution and calculates the associated probability.</span></span>
<span data-ttu-id="dcf0d-127">Argumenty wejściowe są:</span><span class="sxs-lookup"><span data-stu-id="dcf0d-127">The input arguments are:</span></span>

* <span data-ttu-id="dcf0d-128">q - pojedynczego kwantyl zdarzenia z dwumianowy.</span><span class="sxs-lookup"><span data-stu-id="dcf0d-128">q - A single quantile of an event with binomial distribution.</span></span> 
* <span data-ttu-id="dcf0d-129">rozmiar — liczba prób.</span><span class="sxs-lookup"><span data-stu-id="dcf0d-129">size - The number of trials.</span></span>
* <span data-ttu-id="dcf0d-130">PRAWDPD - prawdopodobieństwo sukcesu w wersji próbnej.</span><span class="sxs-lookup"><span data-stu-id="dcf0d-130">prob - The probability of success in a trial.</span></span>
* <span data-ttu-id="dcf0d-131">Strona - L stronie niższe rozkładu U dla górna część dystrybucji lub E równą jeden numer sukcesy.</span><span class="sxs-lookup"><span data-stu-id="dcf0d-131">side - L for the lower side of the distribution, U for the upper side of the distribution, or E that is equal to a single number of successes.</span></span>

<span data-ttu-id="dcf0d-132">Dane wyjściowe usługi jest obliczeniowej prawdopodobieństwo, że jest skojarzony z danym kwantyl.</span><span class="sxs-lookup"><span data-stu-id="dcf0d-132">The output of the service is the calculated probability that is associated with the given quantile.</span></span>

### <a name="binomial-distribution-generator"></a><span data-ttu-id="dcf0d-133">Generator dwumianowy</span><span class="sxs-lookup"><span data-stu-id="dcf0d-133">Binomial Distribution Generator</span></span>
<span data-ttu-id="dcf0d-134">Ta usługa akceptuje 3 argumenty dwumianowy i generuje sekwencję losowych liczb, które są dystrybuowane binomially.</span><span class="sxs-lookup"><span data-stu-id="dcf0d-134">This service accepts 3 arguments of a binomial distribution and generates a random sequence of numbers that are binomially distributed.</span></span> <span data-ttu-id="dcf0d-135">W ramach żądania do niej należy podać następujące argumenty:</span><span class="sxs-lookup"><span data-stu-id="dcf0d-135">The following arguments should be provided to it within the request:</span></span>

* <span data-ttu-id="dcf0d-136">n - liczba uwag.</span><span class="sxs-lookup"><span data-stu-id="dcf0d-136">n - Number of observations.</span></span> 
* <span data-ttu-id="dcf0d-137">rozmiar — liczba prób.</span><span class="sxs-lookup"><span data-stu-id="dcf0d-137">size - Number of trials.</span></span>
* <span data-ttu-id="dcf0d-138">PRAWDPD - prawdopodobieństwo sukcesu.</span><span class="sxs-lookup"><span data-stu-id="dcf0d-138">prob - Probability of success.</span></span>

<span data-ttu-id="dcf0d-139">Dane wyjściowe usługi jest sekwencją n długość z dwumianowy, oparto na argumentach rozmiaru i PRAWDPD.</span><span class="sxs-lookup"><span data-stu-id="dcf0d-139">The output of the service is a sequence of length n with a binomial distribution based on the size and prob arguments.</span></span>

> <span data-ttu-id="dcf0d-140">Ta usługa hostowana w portalu Azure Marketplace jest usługi OData; te można wywoływać za pomocą metody POST lub GET.</span><span class="sxs-lookup"><span data-stu-id="dcf0d-140">This service, as hosted on the Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="dcf0d-141">Istnieje wiele sposobów używania usługi w zautomatyzowany sposób (przykładowe aplikacje są w tym miejscu: [Generator](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionGenerator.aspx), [Kalkulator prawdopodobieństwo](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionProbabilityCalculator.aspx), [Kalkulator kwantyl](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionQuantileCalculator)).</span><span class="sxs-lookup"><span data-stu-id="dcf0d-141">There are multiple ways of consuming the service in an automated fashion (example apps are here: [Generator](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionGenerator.aspx), [Probability Calculator](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionProbabilityCalculator.aspx), [Quantile Calculator](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionQuantileCalculator)).</span></span> 

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="dcf0d-142">Rozpoczynanie korzystania z usług sieci web kod C#:</span><span class="sxs-lookup"><span data-stu-id="dcf0d-142">Starting C# code for web service consumption:</span></span>
### <a name="binomial-distribution-quantile-calculator"></a><span data-ttu-id="dcf0d-143">Kalkulator kwantyl dwumianowy</span><span class="sxs-lookup"><span data-stu-id="dcf0d-143">Binomial Distribution Quantile Calculator</span></span>
    public class Input
    {
            public string p;
            public string size;
            public string prob;
            public string side;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void main()
    {
            var input = new Input() { p = TextBox1.Text, size = TextBox2.Text, prob = TextBox3.Text, side = TextBox4.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }

### <a name="binomial-distribution-probability-calculator"></a><span data-ttu-id="dcf0d-144">Kalkulator prawdopodobieństwo dwumianowy</span><span class="sxs-lookup"><span data-stu-id="dcf0d-144">Binomial Distribution Probability Calculator</span></span>
    public class Input
    {
            public string q;
            public string size;
            public string prob;
            public string side;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { q = TextBox1.Text, size = TextBox2.Text, prob = TextBox3.Text, side = TextBox4.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = " PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }


### <a name="binomial-distribution-generator"></a><span data-ttu-id="dcf0d-145">Generator dwumianowy</span><span class="sxs-lookup"><span data-stu-id="dcf0d-145">Binomial Distribution Generator</span></span>
    public class Input
    {
            public string n;
            public string size;
            public string p;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { n = TextBox1.Text, size = TextBox2.Text, p = TextBox3.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }





## <a name="creation-of-web-service"></a><span data-ttu-id="dcf0d-146">Tworzenie usługi sieci web</span><span class="sxs-lookup"><span data-stu-id="dcf0d-146">Creation of web service</span></span>
> <span data-ttu-id="dcf0d-147">Ta usługa sieci web został utworzony przy użyciu usługi Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="dcf0d-147">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="dcf0d-148">Bezpłatna wersja próbna, a także wprowadzające filmy wideo dotyczące tworzenia eksperymenty i [publikowania usług sieci web](machine-learning-publish-a-machine-learning-web-service.md), można znaleźć pod adresem [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="dcf0d-148">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="dcf0d-149">Poniżej przedstawiono zrzut ekranu doświadczenia utworzony kod przykład i usługi sieci web dla każdego z modułów w ramach eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="dcf0d-149">Below is a screenshot of the experiment that created the web service and example code for each of the modules within the experiment.</span></span>
> 
> 

### <a name="binomial-distribution-quantile-calculator"></a><span data-ttu-id="dcf0d-150">Kalkulator kwantyl dwumianowy</span><span class="sxs-lookup"><span data-stu-id="dcf0d-150">Binomial Distribution Quantile Calculator</span></span>
![Tworzenie obszaru roboczego][4]

#### <a name="module-1"></a><span data-ttu-id="dcf0d-152">Moduł 1:</span><span class="sxs-lookup"><span data-stu-id="dcf0d-152">Module 1:</span></span>
    #data schema with example data (replaced with data from web service)
    data.set=data.frame(p=0.1,size=10,prob=.5,side='L');
    maml.mapOutputPort("data.set"); #send data to output port
#### <a name="module-2"></a><span data-ttu-id="dcf0d-153">Moduł 2:</span><span class="sxs-lookup"><span data-stu-id="dcf0d-153">Module 2:</span></span>
    dataset1 <- maml.mapInputPort(1) # class: data.frame
    param = dataset1
    if (param$p < 0 ) {
    print('Bad input: p must be between 0 and 1')
    param$p = 0
    } else if (param$p > 1) {
    print('Bad input: p must be between 0 and 1')
    param$p = 1
    }

    if (param$prob < 0 ) {
    print('Bad input: prob must be between 0 and 1')
    param$prob = 0
    } else if (param$prob > 1) {
    print('Bad input: prob must be between 0 and 1')
    param$prob = 1
    }

    quantile = qbinom(param$p,size=param$size,prob=param$prob)
    df = data.frame(x=1:param$size, prob=dbinom(1:param$size, param$size, prob=param$prob))
    quantile

    if (param$side == 'U'){
    quantile = qbinom(param$p,size=param$size,prob=param$prob,lower.tail = F)
    band=subset(df,x>quantile)
    } else if (param$side =='L') {
    quantile = qbinom(param$p,size=param$size,prob=param$prob,lower.tail = T)
    band=subset(df,x<=quantile)
    } else {
    print("Invalid side choice")
    }

    output = as.data.frame(quantile)

    # Select data.frame to be sent to the output Dataset port
    maml.mapOutputPort("output");


### <a name="binomial-distribution-probability-calculator"></a><span data-ttu-id="dcf0d-154">Kalkulator prawdopodobieństwo dwumianowy</span><span class="sxs-lookup"><span data-stu-id="dcf0d-154">Binomial Distribution Probability Calculator</span></span>
![Tworzenie obszaru roboczego][5]

#### <a name="module-1"></a><span data-ttu-id="dcf0d-156">Moduł 1:</span><span class="sxs-lookup"><span data-stu-id="dcf0d-156">Module 1:</span></span>
    #data schema with example data (replaced with data from web service)
    data.set=data.frame(q=5,size=10,prob=.5,side='L');
    maml.mapOutputPort("data.set"); #send data to output port


#### <a name="module-2"></a><span data-ttu-id="dcf0d-157">Moduł 2:</span><span class="sxs-lookup"><span data-stu-id="dcf0d-157">Module 2:</span></span>
    dataset1 <- maml.mapInputPort(1) # class: data.frame
    param = dataset1
    prob = pbinom(param$q,size=param$size,prob=param$prob)
    prob.eq = dbinom(param$q,size=param$size,prob=param$prob)
    df = data.frame(x=1:param$size, prob=dbinom(1:param$size, param$size, prob=param$prob))
    prob

    if (param$side == 'U'){
    prob = 1 - prob
    band=subset(df,x>param$q)
    } else if (param$side =='E') {
    prob = prob.eq
    band=subset(df,x==param$q)
    } else if (param$side =='L') {
    prob = prob
    band=subset(df,x<=param$q)
    } else {
    print("Invalid side choice")
    }

    output = as.data.frame(prob)

    # Select data.frame to be sent to the output Dataset port
    maml.mapOutputPort("output");

### <a name="binomial-distribution-generator"></a><span data-ttu-id="dcf0d-158">Generator dwumianowy</span><span class="sxs-lookup"><span data-stu-id="dcf0d-158">Binomial Distribution Generator</span></span>
![Tworzenie obszaru roboczego][6]

#### <a name="module-1"></a><span data-ttu-id="dcf0d-160">Moduł 1:</span><span class="sxs-lookup"><span data-stu-id="dcf0d-160">Module 1:</span></span>
    #data schema with example data (replaced with data from web service)
    data.set=data.frame(n=50,size=10,p=.5);
    maml.mapOutputPort("data.set"); #send data to output port

#### <a name="module-2"></a><span data-ttu-id="dcf0d-161">Moduł 2:</span><span class="sxs-lookup"><span data-stu-id="dcf0d-161">Module 2:</span></span>
    dataset1 <- maml.mapInputPort(1) # class: data.frame
    param = dataset1
    dist = rbinom(param$n,param$size,param$p)

    output = as.data.frame(t(dist))

    # Select data.frame to be sent to the output Dataset port
    maml.mapOutputPort("output");

## <a name="limitations"></a><span data-ttu-id="dcf0d-162">Ograniczenia</span><span class="sxs-lookup"><span data-stu-id="dcf0d-162">Limitations</span></span>
<span data-ttu-id="dcf0d-163">Są to bardzo proste przykłady otaczającego dwumianowy.</span><span class="sxs-lookup"><span data-stu-id="dcf0d-163">These are very simple examples surrounding the binomial distribution.</span></span> <span data-ttu-id="dcf0d-164">Jak wynika z przykładowy kod powyżej, małego Przechwytywanie błędu jest zaimplementowana.</span><span class="sxs-lookup"><span data-stu-id="dcf0d-164">As can be seen from the example code above, little error catching is implemented.</span></span>

## <a name="faq"></a><span data-ttu-id="dcf0d-165">Często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="dcf0d-165">FAQ</span></span>
<span data-ttu-id="dcf0d-166">Często zadawane pytania dotyczące wykorzystania usługi sieci web i publikowanie w portalu Azure Marketplace, zobacz [tutaj](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="dcf0d-166">For frequently asked questions on consumption of the web service or publishing to the Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_1.png

[2]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_2.png

[3]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_3.png

[4]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_4.png

[5]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_5.png

[6]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_6.png

