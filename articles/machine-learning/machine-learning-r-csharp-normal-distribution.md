---
title: "AAA(deprecated) rozkładu normalnego pakietu usługi sieci Web - Azure | Dokumentacja firmy Microsoft"
description: "(przestarzałe) Pakiet usługi sieci Web rozkładu normalnego"
services: machine-learning
documentationcenter: 
author: ireiter
manager: jhubbard
editor: cgronlun
ms.assetid: aab7b92e-953b-43d8-b0af-031394406bfe
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
ms.openlocfilehash: 8bdb5afd9fee88587f548d7c5299480f64289bbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-normal-distribution-suite"></a><span data-ttu-id="f986a-103">(przestarzałe) Rozkład normalny Suite</span><span class="sxs-lookup"><span data-stu-id="f986a-103">(deprecated) Normal Distribution Suite</span></span>

> [!NOTE]
> <span data-ttu-id="f986a-104">Witaj Microsoft DataMarket została wycofana i ten interfejs API jest przestarzały.</span><span class="sxs-lookup"><span data-stu-id="f986a-104">hello Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="f986a-105">Możesz znaleźć wiele interfejsów API i przydatne przykład eksperymenty w hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="f986a-105">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="f986a-106">Aby uzyskać więcej informacji na temat hello galerii, zobacz [udziału i odnajdywania zasobów w hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="f986a-106">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="f986a-107">Hello rozkładu normalnego pakietu to zestaw usług sieci web przykładowej ([Generator](https://datamarket.azure.com/dataset/aml_labs/ndg7), [Kalkulator kwantyl](https://datamarket.azure.com/dataset/aml_labs/ndq5), [Kalkulator prawdopodobieństwo](https://datamarket.azure.com/dataset/aml_labs/ndp5)) ułatwiające generowania i obsługa rozkład normalny.</span><span class="sxs-lookup"><span data-stu-id="f986a-107">hello Normal Distribution Suite is a set of sample web services ([Generator](https://datamarket.azure.com/dataset/aml_labs/ndg7), [Quantile Calculator](https://datamarket.azure.com/dataset/aml_labs/ndq5), [Probability Calculator](https://datamarket.azure.com/dataset/aml_labs/ndp5)) that help in generating and handling normal distributions.</span></span> <span data-ttu-id="f986a-108">usługi Hello Zezwalaj na generowanie sekwencji rozkładu normalnego o dowolnej długości obliczanie quantiles z danym prawdopodobieństwo i obliczanie prawdopodobieństwa z danym kwantyl.</span><span class="sxs-lookup"><span data-stu-id="f986a-108">hello services allow generating a normal distribution sequence of any length, calculating quantiles from a given probability, and calculating probability from a given quantile.</span></span> <span data-ttu-id="f986a-109">Każdej z usług hello emituje różne dane wyjściowe na podstawie hello wybrane usługi (zobacz opis poniżej).</span><span class="sxs-lookup"><span data-stu-id="f986a-109">Each of hello services emits different outputs based on hello selected service (see description below).</span></span> <span data-ttu-id="f986a-110">Hello Suite rozkładu normalnego opiera się na powitania R funkcji qnorm, rnorm i pnorm, które są zawarte w pakiecie Statystyka R.</span><span class="sxs-lookup"><span data-stu-id="f986a-110">hello Normal Distribution Suite is based on hello R functions qnorm, rnorm, and pnorm, which are included in R stats package.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

> <span data-ttu-id="f986a-111">Ta usługa sieci web może być używana przez użytkowników — potencjalnie za pomocą aplikacji mobilnej, za pośrednictwem witryny sieci Web lub nawet na komputerze lokalnym, na przykład.</span><span class="sxs-lookup"><span data-stu-id="f986a-111">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="f986a-112">Ale hello hello usługi sieci web służy również tooserve, na przykład jak usługi Azure Machine Learning można toocreate używanych usług sieci web na podstawie kodu języka R.</span><span class="sxs-lookup"><span data-stu-id="f986a-112">But hello purpose of hello web service is also tooserve as an example of how Azure Machine Learning can be used toocreate web services on top of R code.</span></span> <span data-ttu-id="f986a-113">Przy użyciu kilku wierszy kodu języka R i kliknięcia przycisku w usłudze Azure Machine Learning Studio eksperyment można tworzyć z kodem R i opublikowane jako usługę sieci web.</span><span class="sxs-lookup"><span data-stu-id="f986a-113">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="f986a-114">usługi sieci web Hello można następnie toohello opublikowane w portalu Azure Marketplace i używane przez użytkowników i urządzeń w Witaj świecie bez ustawień infrastruktury przez autora hello hello usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="f986a-114">hello web service can then be published toohello Azure Marketplace and consumed by users and devices across hello world with no infrastructure setup by hello author of hello web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="f986a-115">Użycie usługi sieci web</span><span class="sxs-lookup"><span data-stu-id="f986a-115">Consumption of web service</span></span>
<span data-ttu-id="f986a-116">Witaj rozkładu normalnego pakietu zawiera powitania po 3 usługi.</span><span class="sxs-lookup"><span data-stu-id="f986a-116">hello Normal Distribution Suite includes hello following 3 services.</span></span>

### <a name="normal-distribution-quantile-calculator"></a><span data-ttu-id="f986a-117">Kalkulator kwantyl rozkładu normalnego</span><span class="sxs-lookup"><span data-stu-id="f986a-117">Normal Distribution Quantile Calculator</span></span>
<span data-ttu-id="f986a-118">Ta usługa akceptuje 4 argumenty rozkładu normalnego i oblicza kwantyl hello skojarzone.</span><span class="sxs-lookup"><span data-stu-id="f986a-118">This service accepts 4 arguments of a normal distribution and calculates hello associated quantile.</span></span>

<span data-ttu-id="f986a-119">argumenty wejściowe Hello są:</span><span class="sxs-lookup"><span data-stu-id="f986a-119">hello input arguments are:</span></span>

* <span data-ttu-id="f986a-120">p - pojedynczego prawdopodobieństwo zdarzenia z rozkładu normalnego.</span><span class="sxs-lookup"><span data-stu-id="f986a-120">p - A single probability of an event with normal distribution.</span></span> 
* <span data-ttu-id="f986a-121">Oznacza — Witaj średniej rozkładu normalnego.</span><span class="sxs-lookup"><span data-stu-id="f986a-121">Mean - hello normal distribution mean.</span></span>
* <span data-ttu-id="f986a-122">SD - odchylenie standardowe hello rozkładu normalnego.</span><span class="sxs-lookup"><span data-stu-id="f986a-122">SD - hello normal distribution standard deviation.</span></span> 
* <span data-ttu-id="f986a-123">Strona - L dla hello dolnej strony hello dystrybucji i U dla hello górna hello dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="f986a-123">Side - L for hello lower side of hello distribution and U for hello upper side of hello distribution.</span></span>

<span data-ttu-id="f986a-124">dane wyjściowe Hello hello usługi jest kwantyl hello obliczane, który jest skojarzony z hello podane prawdopodobieństwa.</span><span class="sxs-lookup"><span data-stu-id="f986a-124">hello output of hello service is hello calculated quantile that is associated with hello given probability.</span></span>

### <a name="normal-distribution-probability-calculator"></a><span data-ttu-id="f986a-125">Kalkulator prawdopodobieństwa rozkładu normalnego</span><span class="sxs-lookup"><span data-stu-id="f986a-125">Normal Distribution Probability Calculator</span></span>
<span data-ttu-id="f986a-126">Ta usługa akceptuje 4 argumenty rozkładu normalnego i oblicza prawdopodobieństwo hello skojarzone.</span><span class="sxs-lookup"><span data-stu-id="f986a-126">This service accepts 4 arguments of a normal distribution and calculates hello associated probability.</span></span>

<span data-ttu-id="f986a-127">argumenty wejściowe Hello są:</span><span class="sxs-lookup"><span data-stu-id="f986a-127">hello input arguments are:</span></span>

* <span data-ttu-id="f986a-128">q - pojedynczego kwantyl zdarzenia z rozkładu normalnego.</span><span class="sxs-lookup"><span data-stu-id="f986a-128">q - A single quantile of an event with normal distribution.</span></span> 
* <span data-ttu-id="f986a-129">Oznacza — Witaj średniej rozkładu normalnego.</span><span class="sxs-lookup"><span data-stu-id="f986a-129">Mean - hello normal distribution mean.</span></span>
* <span data-ttu-id="f986a-130">SD - odchylenie standardowe hello rozkładu normalnego.</span><span class="sxs-lookup"><span data-stu-id="f986a-130">SD - hello normal distribution standard deviation.</span></span> 
* <span data-ttu-id="f986a-131">Strona - L dla hello dolnej strony hello dystrybucji i U dla hello górna hello dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="f986a-131">Side - L for hello lower side of hello distribution and U for hello upper side of hello distribution.</span></span>

<span data-ttu-id="f986a-132">dane wyjściowe Hello hello usługi jest prawdopodobieństwo hello obliczana jest skojarzona z hello podane kwantyl.</span><span class="sxs-lookup"><span data-stu-id="f986a-132">hello output of hello service is hello calculated probability that is associated with hello given quantile.</span></span>

### <a name="normal-distribution-generator"></a><span data-ttu-id="f986a-133">Generator rozkładu normalnego</span><span class="sxs-lookup"><span data-stu-id="f986a-133">Normal Distribution Generator</span></span>
<span data-ttu-id="f986a-134">Ta usługa akceptuje 3 argumenty rozkładu normalnego i generuje sekwencję losowych liczb, które są zazwyczaj dystrybuowane.</span><span class="sxs-lookup"><span data-stu-id="f986a-134">This service accepts 3 arguments of a normal distribution and generates a random sequence of numbers that are normally distributed.</span></span> <span data-ttu-id="f986a-135">Witaj następujących argumentów należy podawać tooit w ramach żądania hello:</span><span class="sxs-lookup"><span data-stu-id="f986a-135">hello following arguments should be provided tooit within hello request:</span></span>

* <span data-ttu-id="f986a-136">n - hello Liczba uwag.</span><span class="sxs-lookup"><span data-stu-id="f986a-136">n - hello number of observations.</span></span> 
* <span data-ttu-id="f986a-137">oznacza — Witaj średniej rozkładu normalnego.</span><span class="sxs-lookup"><span data-stu-id="f986a-137">mean - hello normal distribution mean.</span></span>
* <span data-ttu-id="f986a-138">SD - odchylenie standardowe hello rozkładu normalnego.</span><span class="sxs-lookup"><span data-stu-id="f986a-138">sd - hello normal distribution standard deviation.</span></span> 

<span data-ttu-id="f986a-139">dane wyjściowe Hello usługi hello jest sekwencją n długość z rozkładu normalnego oparte na powitania średnią i sd argumentów.</span><span class="sxs-lookup"><span data-stu-id="f986a-139">hello output of hello service is a sequence of length n with a normal distribution based on hello mean and sd arguments.</span></span>

> <span data-ttu-id="f986a-140">Ta usługa hostowana na hello Azure Marketplace jest usługi OData; te można wywoływać za pomocą metody POST lub GET.</span><span class="sxs-lookup"><span data-stu-id="f986a-140">This service, as hosted on hello Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="f986a-141">Istnieje wiele sposobów używania usługi hello w zautomatyzowany sposób (przykładowe aplikacje są w tym miejscu: [Generator](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionGenerator.aspx), [Kalkulator prawdopodobieństwo](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionProbabilityCalculator.aspx), [Kalkulator kwantyl](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionQuantileCalculator.aspx)).</span><span class="sxs-lookup"><span data-stu-id="f986a-141">There are multiple ways of consuming hello service in an automated fashion (example apps are here: [Generator](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionGenerator.aspx), [Probability Calculator](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionProbabilityCalculator.aspx), [Quantile Calculator](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionQuantileCalculator.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="f986a-142">Rozpoczynanie korzystania z usług sieci web kod C#:</span><span class="sxs-lookup"><span data-stu-id="f986a-142">Starting C# code for web service consumption:</span></span>
### <a name="normal-distribution-quantile-calculator"></a><span data-ttu-id="f986a-143">Kalkulator kwantyl rozkładu normalnego</span><span class="sxs-lookup"><span data-stu-id="f986a-143">Normal Distribution Quantile Calculator</span></span>
    public class Input
    {
            public string p;
            public string mean;
            public string sd;
            public string side;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { p = TextBox1.Text, mean = TextBox2.Text, sd = TextBox3.Text, side = TextBox4.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }


### <a name="normal-distribution-probability-calculator"></a><span data-ttu-id="f986a-144">Kalkulator prawdopodobieństwa rozkładu normalnego</span><span class="sxs-lookup"><span data-stu-id="f986a-144">Normal Distribution Probability Calculator</span></span>
    public class Input
    {
            public string q;
            public string mean;
            public string sd;
            public string side;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { q = TextBox1.Text, mean = TextBox2.Text, sd = TextBox3.Text, side = TextBox4.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }

### <a name="normal-distribution-generator"></a><span data-ttu-id="f986a-145">Generator rozkładu normalnego</span><span class="sxs-lookup"><span data-stu-id="f986a-145">Normal Distribution Generator</span></span>
    public class Input
    {
            public string n;
            public string mean;
            public string sd;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { n = TextBox1.Text, mean = TextBox2.Text, sd = TextBox3.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }


## <a name="creation-of-web-service"></a><span data-ttu-id="f986a-146">Tworzenie usługi sieci web</span><span class="sxs-lookup"><span data-stu-id="f986a-146">Creation of web service</span></span>
> <span data-ttu-id="f986a-147">Ta usługa sieci web został utworzony przy użyciu usługi Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="f986a-147">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="f986a-148">Bezpłatna wersja próbna, a także wprowadzające filmy wideo dotyczące tworzenia eksperymenty i [publikowania usług sieci web](machine-learning-publish-a-machine-learning-web-service.md), można znaleźć pod adresem [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="f986a-148">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> 
> 
> 

<span data-ttu-id="f986a-149">Poniżej przedstawiono zrzut ekranu hello eksperymentu, utworzona hello kod przykład i usługi sieci web dla każdego z modułów hello w ramach eksperymentu hello.</span><span class="sxs-lookup"><span data-stu-id="f986a-149">Below is a screenshot of hello experiment that created hello web service and example code for each of hello modules within hello experiment.</span></span>

### <a name="normal-distribution-quantile-calculator"></a><span data-ttu-id="f986a-150">Kalkulator kwantyl rozkładu normalnego</span><span class="sxs-lookup"><span data-stu-id="f986a-150">Normal Distribution Quantile Calculator</span></span>
<span data-ttu-id="f986a-151">Przepływ eksperymentu:</span><span class="sxs-lookup"><span data-stu-id="f986a-151">Experiment flow:</span></span>

![Przepływ eksperymentu][2]

    #Data schema with example data (replaced with data from web service)
    data.set=data.frame(p=0.1,mean=0,sd=1,side='L');
    maml.mapOutputPort("data.set"); #send data toooutput port

    # Map 1-based optional input ports toovariables
    dataset1 <- maml.mapInputPort(1) # class: data.frame

    param = dataset1
    if (param$p < 0 ) {
    print('Bad input: p must be between 0 and 1')
    param$p = 0
    } else if (param$p > 1) {
    print('Bad input: p must be between 0 and 1')
    param$p = 1
    }
    q = qnorm(param$p,mean=param$mean,sd=param$sd)

    if (param$side == 'U'){
    q = 2* param$mean - q
    } else if (param$side =='L') {
    q = q
    } else {
    print("Invalid side choice")
    }

    output = as.data.frame(q)

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("output");

### <a name="normal-distribution-probability-calculator"></a><span data-ttu-id="f986a-153">Kalkulator prawdopodobieństwa rozkładu normalnego</span><span class="sxs-lookup"><span data-stu-id="f986a-153">Normal Distribution Probability Calculator</span></span>
<span data-ttu-id="f986a-154">Przepływ eksperymentu:</span><span class="sxs-lookup"><span data-stu-id="f986a-154">Experiment flow:</span></span>

![Przepływ eksperymentu][3]

     #Data schema with example data (replaced with data from web service)
    data.set=data.frame(q=-1,mean=0,sd=1,side='L');
    maml.mapOutputPort("data.set"); #send data toooutput port

    # Map 1-based optional input ports toovariables
    dataset1 <- maml.mapInputPort(1) # class: data.frame

    param = dataset1
    prob = pnorm(param$q,mean=param$mean,sd=param$sd)

    if (param$side == 'U'){
    prob = 1 - prob
    } else if (param$side =='B') {
    prob = ifelse(prob<=0.5,prob * 2, 1)
    } else if (param$side =='L') {
    prob = prob
    } else {
    print("Invalid side choice")
    }

    output = as.data.frame(prob)

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("output");

### <a name="normal-distribution-generator"></a><span data-ttu-id="f986a-156">Generator rozkładu normalnego</span><span class="sxs-lookup"><span data-stu-id="f986a-156">Normal Distribution Generator</span></span>
<span data-ttu-id="f986a-157">Przepływ eksperymentu:</span><span class="sxs-lookup"><span data-stu-id="f986a-157">Experiment flow:</span></span>

![Przepływ eksperymentu][4]

    #Data schema with example data (replaced with data from web service)
    data.set=data.frame(n=50,mean=0,sd=1);
    maml.mapOutputPort("data.set"); #send data toooutput port

    # Map 1-based optional input ports toovariables
    dataset1 <- maml.mapInputPort(1) # class: data.frame

    param = dataset1
    dist = rnorm(param$n,mean=param$mean,sd=param$sd)

    output = as.data.frame(t(dist))

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("output");

## <a name="limitations"></a><span data-ttu-id="f986a-159">Ograniczenia</span><span class="sxs-lookup"><span data-stu-id="f986a-159">Limitations</span></span>
<span data-ttu-id="f986a-160">Są to bardzo proste przykłady otaczającego hello rozkładu normalnego.</span><span class="sxs-lookup"><span data-stu-id="f986a-160">These are very simple examples surrounding hello normal distribution.</span></span> <span data-ttu-id="f986a-161">Jak wynika z powyższych hello przykładowy kod, małego Przechwytywanie błędu jest zaimplementowana.</span><span class="sxs-lookup"><span data-stu-id="f986a-161">As can be seen from hello example code above, little error catching is implemented.</span></span>

## <a name="faq"></a><span data-ttu-id="f986a-162">Często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="f986a-162">FAQ</span></span>
<span data-ttu-id="f986a-163">Często zadawane pytania dotyczące wykorzystania hello usługi sieci web lub toohello publikowania portalu Azure Marketplace, zobacz [tutaj](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="f986a-163">For frequently asked questions on consumption of hello web service or publishing toohello Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-normal-distribution/normal-img1.png
[2]: ./media/machine-learning-r-csharp-normal-distribution/normal-img2.png
[3]: ./media/machine-learning-r-csharp-normal-distribution/normal-img3.png
[4]: ./media/machine-learning-r-csharp-normal-distribution/normal-img4.png

