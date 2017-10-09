---
title: "AAA(deprecated) Suite dwumianowy — Azure | Dokumentacja firmy Microsoft"
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
redirect_document_id: True
ms.openlocfilehash: 6f94436cd19abeb518d179f340c8d4f43fcf4520
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-binomial-distribution-suite"></a><span data-ttu-id="10887-103">(przestarzałe) Pakiet dwumianowy</span><span class="sxs-lookup"><span data-stu-id="10887-103">(deprecated) Binomial Distribution Suite</span></span>

> [!NOTE]
> <span data-ttu-id="10887-104">Witaj Microsoft DataMarket została wycofana i ten interfejs API jest przestarzały.</span><span class="sxs-lookup"><span data-stu-id="10887-104">hello Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="10887-105">Możesz znaleźć wiele interfejsów API i przydatne przykład eksperymenty w hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="10887-105">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="10887-106">Aby uzyskać więcej informacji na temat hello galerii, zobacz [udziału i odnajdywania zasobów w hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="10887-106">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="10887-107">Hello dwumianowy Suite to zestaw usług sieci web przykładowej ([Generator dwumianowy](https://datamarket.azure.com/dataset/aml_labs/bdg5), [Kalkulator prawdopodobieństwo](https://datamarket.azure.com/dataset/aml_labs/bdp4), [Kalkulator kwantyl](https://datamarket.azure.com/dataset/aml_labs/bdq5)) ułatwiające podczas generowania i dotyczącą dwumianowy dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="10887-107">hello Binomial Distribution Suite is a set of sample web services ([Binomial Generator](https://datamarket.azure.com/dataset/aml_labs/bdg5), [Probability Calculator](https://datamarket.azure.com/dataset/aml_labs/bdp4), [Quantile Calculator](https://datamarket.azure.com/dataset/aml_labs/bdq5)) that help in generating and dealing with binomial distributions.</span></span> <span data-ttu-id="10887-108">Hello usługi obsługują generowanie sekwencji dwumianowy o dowolnej długości obliczanie quantiles z podanej prawdopodobieństwo i obliczanie prawdopodobieństwa z danym kwantyl.</span><span class="sxs-lookup"><span data-stu-id="10887-108">hello services allow generating a binomial distribution sequence of any length, calculating quantiles out of given probability and calculating probability from a given quantile.</span></span> <span data-ttu-id="10887-109">Każdej z usług hello emituje różne dane wyjściowe na podstawie hello wybrane usługi (zobacz opis poniżej).</span><span class="sxs-lookup"><span data-stu-id="10887-109">Each of hello services emits different outputs based on hello selected service (see description below).</span></span> <span data-ttu-id="10887-110">Hello Suite dwumianowy opiera się na hello R funkcji qbinom rbinom i pbinom, które są zawarte w pakiecie Statystyka R hello.</span><span class="sxs-lookup"><span data-stu-id="10887-110">hello Binomial Distribution Suite is based on hello R functions qbinom, rbinom, and pbinom, which are included in hello R stats package.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

> <span data-ttu-id="10887-111">Te usługi sieci web może być używana przez użytkowników — potencjalnie bezpośrednio na rynek hello, za pomocą aplikacji mobilnej, za pośrednictwem witryny sieci Web lub nawet na komputerze lokalnym, na przykład.</span><span class="sxs-lookup"><span data-stu-id="10887-111">These web services could be consumed by users – potentially directly on hello marketplace, through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="10887-112">Ale hello hello usługi sieci web służy również tooserve, na przykład jak usługi Azure Machine Learning można toocreate używanych usług sieci web na podstawie kodu języka R.</span><span class="sxs-lookup"><span data-stu-id="10887-112">But hello purpose of hello web service is also tooserve as an example of how Azure Machine Learning can be used toocreate web services on top of R code.</span></span> <span data-ttu-id="10887-113">Przy użyciu kilku wierszy kodu języka R i kliknięcia przycisku w usłudze Azure Machine Learning Studio eksperyment można tworzyć z kodem R i opublikowane jako usługę sieci web.</span><span class="sxs-lookup"><span data-stu-id="10887-113">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="10887-114">Usługa sieci web Hello można następnie toohello opublikowane w portalu Azure Marketplace oraz używane przez użytkowników i urządzeń w Witaj świecie – nie infrastruktury Konfiguracja przez autora hello hello usługi sieci web jest wymagana.</span><span class="sxs-lookup"><span data-stu-id="10887-114">hello web service can then be published toohello Azure Marketplace and consumed by users and devices across hello world – no infrastructure setup by hello author of hello web service is required.</span></span>
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="10887-115">Użycie usługi sieci web</span><span class="sxs-lookup"><span data-stu-id="10887-115">Consumption of web service</span></span>
<span data-ttu-id="10887-116">Witaj Suite dwumianowy obejmuje powitania po 3 usługi.</span><span class="sxs-lookup"><span data-stu-id="10887-116">hello Binomial Distribution Suite includes hello following 3 services.</span></span>

### <a name="binomial-distribution-quantile-calculator"></a><span data-ttu-id="10887-117">Kalkulator kwantyl dwumianowy</span><span class="sxs-lookup"><span data-stu-id="10887-117">Binomial Distribution Quantile Calculator</span></span>
<span data-ttu-id="10887-118">Ta usługa akceptuje 4 argumenty rozkładu normalnego i oblicza kwantyl hello skojarzone.</span><span class="sxs-lookup"><span data-stu-id="10887-118">This service accepts 4 arguments of a normal distribution and calculates hello associated quantile.</span></span>
<span data-ttu-id="10887-119">argumenty wejściowe Hello są:</span><span class="sxs-lookup"><span data-stu-id="10887-119">hello input arguments are:</span></span>

* <span data-ttu-id="10887-120">p - pojedynczego zagregowane prawdopodobieństwo wielu prób.</span><span class="sxs-lookup"><span data-stu-id="10887-120">p - A single aggregated probability of multiple trials.</span></span>  
* <span data-ttu-id="10887-121">rozmiar — Witaj liczba prób.</span><span class="sxs-lookup"><span data-stu-id="10887-121">size - hello number of trials.</span></span>
* <span data-ttu-id="10887-122">PRAWDPD - hello prawdopodobieństwo sukcesu w wersji próbnej.</span><span class="sxs-lookup"><span data-stu-id="10887-122">prob - hello probability of success in a trial.</span></span>
* <span data-ttu-id="10887-123">Strona - L dla strony niższe hello rozkładu hello U dla hello górna hello dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="10887-123">Side - L for hello lower side of hello distribution, U for hello upper side of hello distribution.</span></span> 

<span data-ttu-id="10887-124">dane wyjściowe Hello hello usługi jest kwantyl hello obliczane, który jest skojarzony z hello podane prawdopodobieństwa.</span><span class="sxs-lookup"><span data-stu-id="10887-124">hello output of hello service is hello calculated quantile that is associated with hello given probability.</span></span>

### <a name="binomial-distribution-probability-calculator"></a><span data-ttu-id="10887-125">Kalkulator prawdopodobieństwo dwumianowy</span><span class="sxs-lookup"><span data-stu-id="10887-125">Binomial Distribution Probability Calculator</span></span>
<span data-ttu-id="10887-126">Ta usługa akceptuje 4 argumenty dwumianowy i oblicza prawdopodobieństwo hello skojarzone.</span><span class="sxs-lookup"><span data-stu-id="10887-126">This service accepts 4 arguments of a binomial distribution and calculates hello associated probability.</span></span>
<span data-ttu-id="10887-127">argumenty wejściowe Hello są:</span><span class="sxs-lookup"><span data-stu-id="10887-127">hello input arguments are:</span></span>

* <span data-ttu-id="10887-128">q - pojedynczego kwantyl zdarzenia z dwumianowy.</span><span class="sxs-lookup"><span data-stu-id="10887-128">q - A single quantile of an event with binomial distribution.</span></span> 
* <span data-ttu-id="10887-129">rozmiar — Witaj liczba prób.</span><span class="sxs-lookup"><span data-stu-id="10887-129">size - hello number of trials.</span></span>
* <span data-ttu-id="10887-130">PRAWDPD - hello prawdopodobieństwo sukcesu w wersji próbnej.</span><span class="sxs-lookup"><span data-stu-id="10887-130">prob - hello probability of success in a trial.</span></span>
* <span data-ttu-id="10887-131">Strona - L-hello dolnej strony hello dystrybucji, U dla hello górna dystrybucji hello lub E tooa równy jeden liczbę sukcesów.</span><span class="sxs-lookup"><span data-stu-id="10887-131">side - L for hello lower side of hello distribution, U for hello upper side of hello distribution, or E that is equal tooa single number of successes.</span></span>

<span data-ttu-id="10887-132">dane wyjściowe Hello hello usługi jest prawdopodobieństwo hello obliczana jest skojarzona z hello podane kwantyl.</span><span class="sxs-lookup"><span data-stu-id="10887-132">hello output of hello service is hello calculated probability that is associated with hello given quantile.</span></span>

### <a name="binomial-distribution-generator"></a><span data-ttu-id="10887-133">Generator dwumianowy</span><span class="sxs-lookup"><span data-stu-id="10887-133">Binomial Distribution Generator</span></span>
<span data-ttu-id="10887-134">Ta usługa akceptuje 3 argumenty dwumianowy i generuje sekwencję losowych liczb, które są dystrybuowane binomially.</span><span class="sxs-lookup"><span data-stu-id="10887-134">This service accepts 3 arguments of a binomial distribution and generates a random sequence of numbers that are binomially distributed.</span></span> <span data-ttu-id="10887-135">Witaj następujących argumentów należy podawać tooit w ramach żądania hello:</span><span class="sxs-lookup"><span data-stu-id="10887-135">hello following arguments should be provided tooit within hello request:</span></span>

* <span data-ttu-id="10887-136">n - liczba uwag.</span><span class="sxs-lookup"><span data-stu-id="10887-136">n - Number of observations.</span></span> 
* <span data-ttu-id="10887-137">rozmiar — liczba prób.</span><span class="sxs-lookup"><span data-stu-id="10887-137">size - Number of trials.</span></span>
* <span data-ttu-id="10887-138">PRAWDPD - prawdopodobieństwo sukcesu.</span><span class="sxs-lookup"><span data-stu-id="10887-138">prob - Probability of success.</span></span>

<span data-ttu-id="10887-139">dane wyjściowe Hello usługi hello jest sekwencją n długość z dwumianowy, oparte na powitania rozmiaru i PRAWDPD argumentów.</span><span class="sxs-lookup"><span data-stu-id="10887-139">hello output of hello service is a sequence of length n with a binomial distribution based on hello size and prob arguments.</span></span>

> <span data-ttu-id="10887-140">Ta usługa hostowana na hello Azure Marketplace jest usługi OData; te można wywoływać za pomocą metody POST lub GET.</span><span class="sxs-lookup"><span data-stu-id="10887-140">This service, as hosted on hello Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="10887-141">Istnieje wiele sposobów używania usługi hello w zautomatyzowany sposób (przykładowe aplikacje są w tym miejscu: [Generator](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionGenerator.aspx), [Kalkulator prawdopodobieństwo](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionProbabilityCalculator.aspx), [Kalkulator kwantyl](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionQuantileCalculator)).</span><span class="sxs-lookup"><span data-stu-id="10887-141">There are multiple ways of consuming hello service in an automated fashion (example apps are here: [Generator](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionGenerator.aspx), [Probability Calculator](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionProbabilityCalculator.aspx), [Quantile Calculator](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionQuantileCalculator)).</span></span> 

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="10887-142">Rozpoczynanie korzystania z usług sieci web kod C#:</span><span class="sxs-lookup"><span data-stu-id="10887-142">Starting C# code for web service consumption:</span></span>
### <a name="binomial-distribution-quantile-calculator"></a><span data-ttu-id="10887-143">Kalkulator kwantyl dwumianowy</span><span class="sxs-lookup"><span data-stu-id="10887-143">Binomial Distribution Quantile Calculator</span></span>
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

### <a name="binomial-distribution-probability-calculator"></a><span data-ttu-id="10887-144">Kalkulator prawdopodobieństwo dwumianowy</span><span class="sxs-lookup"><span data-stu-id="10887-144">Binomial Distribution Probability Calculator</span></span>
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


### <a name="binomial-distribution-generator"></a><span data-ttu-id="10887-145">Generator dwumianowy</span><span class="sxs-lookup"><span data-stu-id="10887-145">Binomial Distribution Generator</span></span>
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





## <a name="creation-of-web-service"></a><span data-ttu-id="10887-146">Tworzenie usługi sieci web</span><span class="sxs-lookup"><span data-stu-id="10887-146">Creation of web service</span></span>
> <span data-ttu-id="10887-147">Ta usługa sieci web został utworzony przy użyciu usługi Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="10887-147">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="10887-148">Bezpłatna wersja próbna, a także wprowadzające filmy wideo dotyczące tworzenia eksperymenty i [publikowania usług sieci web](machine-learning-publish-a-machine-learning-web-service.md), można znaleźć pod adresem [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="10887-148">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="10887-149">Poniżej przedstawiono zrzut ekranu hello eksperymentu, utworzona hello kod przykład i usługi sieci web dla każdego z modułów hello w ramach eksperymentu hello.</span><span class="sxs-lookup"><span data-stu-id="10887-149">Below is a screenshot of hello experiment that created hello web service and example code for each of hello modules within hello experiment.</span></span>
> 
> 

### <a name="binomial-distribution-quantile-calculator"></a><span data-ttu-id="10887-150">Kalkulator kwantyl dwumianowy</span><span class="sxs-lookup"><span data-stu-id="10887-150">Binomial Distribution Quantile Calculator</span></span>
![Tworzenie obszaru roboczego][4]

#### <a name="module-1"></a><span data-ttu-id="10887-152">Moduł 1:</span><span class="sxs-lookup"><span data-stu-id="10887-152">Module 1:</span></span>
    #data schema with example data (replaced with data from web service)
    data.set=data.frame(p=0.1,size=10,prob=.5,side='L');
    maml.mapOutputPort("data.set"); #send data toooutput port
#### <a name="module-2"></a><span data-ttu-id="10887-153">Moduł 2:</span><span class="sxs-lookup"><span data-stu-id="10887-153">Module 2:</span></span>
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

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("output");


### <a name="binomial-distribution-probability-calculator"></a><span data-ttu-id="10887-154">Kalkulator prawdopodobieństwo dwumianowy</span><span class="sxs-lookup"><span data-stu-id="10887-154">Binomial Distribution Probability Calculator</span></span>
![Tworzenie obszaru roboczego][5]

#### <a name="module-1"></a><span data-ttu-id="10887-156">Moduł 1:</span><span class="sxs-lookup"><span data-stu-id="10887-156">Module 1:</span></span>
    #data schema with example data (replaced with data from web service)
    data.set=data.frame(q=5,size=10,prob=.5,side='L');
    maml.mapOutputPort("data.set"); #send data toooutput port


#### <a name="module-2"></a><span data-ttu-id="10887-157">Moduł 2:</span><span class="sxs-lookup"><span data-stu-id="10887-157">Module 2:</span></span>
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

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("output");

### <a name="binomial-distribution-generator"></a><span data-ttu-id="10887-158">Generator dwumianowy</span><span class="sxs-lookup"><span data-stu-id="10887-158">Binomial Distribution Generator</span></span>
![Tworzenie obszaru roboczego][6]

#### <a name="module-1"></a><span data-ttu-id="10887-160">Moduł 1:</span><span class="sxs-lookup"><span data-stu-id="10887-160">Module 1:</span></span>
    #data schema with example data (replaced with data from web service)
    data.set=data.frame(n=50,size=10,p=.5);
    maml.mapOutputPort("data.set"); #send data toooutput port

#### <a name="module-2"></a><span data-ttu-id="10887-161">Moduł 2:</span><span class="sxs-lookup"><span data-stu-id="10887-161">Module 2:</span></span>
    dataset1 <- maml.mapInputPort(1) # class: data.frame
    param = dataset1
    dist = rbinom(param$n,param$size,param$p)

    output = as.data.frame(t(dist))

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("output");

## <a name="limitations"></a><span data-ttu-id="10887-162">Ograniczenia</span><span class="sxs-lookup"><span data-stu-id="10887-162">Limitations</span></span>
<span data-ttu-id="10887-163">Są to bardzo proste przykłady otaczającego hello dwumianowy.</span><span class="sxs-lookup"><span data-stu-id="10887-163">These are very simple examples surrounding hello binomial distribution.</span></span> <span data-ttu-id="10887-164">Jak wynika z powyższych hello przykładowy kod, małego Przechwytywanie błędu jest zaimplementowana.</span><span class="sxs-lookup"><span data-stu-id="10887-164">As can be seen from hello example code above, little error catching is implemented.</span></span>

## <a name="faq"></a><span data-ttu-id="10887-165">Często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="10887-165">FAQ</span></span>
<span data-ttu-id="10887-166">Często zadawane pytania dotyczące wykorzystania hello usługi sieci web lub toohello publikowania portalu Azure Marketplace, zobacz [tutaj](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="10887-166">For frequently asked questions on consumption of hello web service or publishing toohello Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_1.png

[2]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_2.png

[3]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_3.png

[4]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_4.png

[5]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_5.png

[6]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_6.png

