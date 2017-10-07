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
# <a name="deprecated-normal-distribution-suite"></a>(przestarzałe) Rozkład normalny Suite

> [!NOTE]
> Witaj Microsoft DataMarket została wycofana i ten interfejs API jest przestarzały. 
> 
> Możesz znaleźć wiele interfejsów API i przydatne przykład eksperymenty w hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com). Aby uzyskać więcej informacji na temat hello galerii, zobacz [udziału i odnajdywania zasobów w hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).

Hello rozkładu normalnego pakietu to zestaw usług sieci web przykładowej ([Generator](https://datamarket.azure.com/dataset/aml_labs/ndg7), [Kalkulator kwantyl](https://datamarket.azure.com/dataset/aml_labs/ndq5), [Kalkulator prawdopodobieństwo](https://datamarket.azure.com/dataset/aml_labs/ndp5)) ułatwiające generowania i obsługa rozkład normalny. usługi Hello Zezwalaj na generowanie sekwencji rozkładu normalnego o dowolnej długości obliczanie quantiles z danym prawdopodobieństwo i obliczanie prawdopodobieństwa z danym kwantyl. Każdej z usług hello emituje różne dane wyjściowe na podstawie hello wybrane usługi (zobacz opis poniżej). Hello Suite rozkładu normalnego opiera się na powitania R funkcji qnorm, rnorm i pnorm, które są zawarte w pakiecie Statystyka R.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

> Ta usługa sieci web może być używana przez użytkowników — potencjalnie za pomocą aplikacji mobilnej, za pośrednictwem witryny sieci Web lub nawet na komputerze lokalnym, na przykład. Ale hello hello usługi sieci web służy również tooserve, na przykład jak usługi Azure Machine Learning można toocreate używanych usług sieci web na podstawie kodu języka R. Przy użyciu kilku wierszy kodu języka R i kliknięcia przycisku w usłudze Azure Machine Learning Studio eksperyment można tworzyć z kodem R i opublikowane jako usługę sieci web. usługi sieci web Hello można następnie toohello opublikowane w portalu Azure Marketplace i używane przez użytkowników i urządzeń w Witaj świecie bez ustawień infrastruktury przez autora hello hello usługi sieci web.  
> 
> 

## <a name="consumption-of-web-service"></a>Użycie usługi sieci web
Witaj rozkładu normalnego pakietu zawiera powitania po 3 usługi.

### <a name="normal-distribution-quantile-calculator"></a>Kalkulator kwantyl rozkładu normalnego
Ta usługa akceptuje 4 argumenty rozkładu normalnego i oblicza kwantyl hello skojarzone.

argumenty wejściowe Hello są:

* p - pojedynczego prawdopodobieństwo zdarzenia z rozkładu normalnego. 
* Oznacza — Witaj średniej rozkładu normalnego.
* SD - odchylenie standardowe hello rozkładu normalnego. 
* Strona - L dla hello dolnej strony hello dystrybucji i U dla hello górna hello dystrybucji.

dane wyjściowe Hello hello usługi jest kwantyl hello obliczane, który jest skojarzony z hello podane prawdopodobieństwa.

### <a name="normal-distribution-probability-calculator"></a>Kalkulator prawdopodobieństwa rozkładu normalnego
Ta usługa akceptuje 4 argumenty rozkładu normalnego i oblicza prawdopodobieństwo hello skojarzone.

argumenty wejściowe Hello są:

* q - pojedynczego kwantyl zdarzenia z rozkładu normalnego. 
* Oznacza — Witaj średniej rozkładu normalnego.
* SD - odchylenie standardowe hello rozkładu normalnego. 
* Strona - L dla hello dolnej strony hello dystrybucji i U dla hello górna hello dystrybucji.

dane wyjściowe Hello hello usługi jest prawdopodobieństwo hello obliczana jest skojarzona z hello podane kwantyl.

### <a name="normal-distribution-generator"></a>Generator rozkładu normalnego
Ta usługa akceptuje 3 argumenty rozkładu normalnego i generuje sekwencję losowych liczb, które są zazwyczaj dystrybuowane. Witaj następujących argumentów należy podawać tooit w ramach żądania hello:

* n - hello Liczba uwag. 
* oznacza — Witaj średniej rozkładu normalnego.
* SD - odchylenie standardowe hello rozkładu normalnego. 

dane wyjściowe Hello usługi hello jest sekwencją n długość z rozkładu normalnego oparte na powitania średnią i sd argumentów.

> Ta usługa hostowana na hello Azure Marketplace jest usługi OData; te można wywoływać za pomocą metody POST lub GET. 
> 
> 

Istnieje wiele sposobów używania usługi hello w zautomatyzowany sposób (przykładowe aplikacje są w tym miejscu: [Generator](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionGenerator.aspx), [Kalkulator prawdopodobieństwo](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionProbabilityCalculator.aspx), [Kalkulator kwantyl](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionQuantileCalculator.aspx)).

### <a name="starting-c-code-for-web-service-consumption"></a>Rozpoczynanie korzystania z usług sieci web kod C#:
### <a name="normal-distribution-quantile-calculator"></a>Kalkulator kwantyl rozkładu normalnego
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


### <a name="normal-distribution-probability-calculator"></a>Kalkulator prawdopodobieństwa rozkładu normalnego
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

### <a name="normal-distribution-generator"></a>Generator rozkładu normalnego
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


## <a name="creation-of-web-service"></a>Tworzenie usługi sieci web
> Ta usługa sieci web został utworzony przy użyciu usługi Azure Machine Learning. Bezpłatna wersja próbna, a także wprowadzające filmy wideo dotyczące tworzenia eksperymenty i [publikowania usług sieci web](machine-learning-publish-a-machine-learning-web-service.md), można znaleźć pod adresem [azure.com/ml](http://azure.com/ml). 
> 
> 

Poniżej przedstawiono zrzut ekranu hello eksperymentu, utworzona hello kod przykład i usługi sieci web dla każdego z modułów hello w ramach eksperymentu hello.

### <a name="normal-distribution-quantile-calculator"></a>Kalkulator kwantyl rozkładu normalnego
Przepływ eksperymentu:

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

### <a name="normal-distribution-probability-calculator"></a>Kalkulator prawdopodobieństwa rozkładu normalnego
Przepływ eksperymentu:

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

### <a name="normal-distribution-generator"></a>Generator rozkładu normalnego
Przepływ eksperymentu:

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

## <a name="limitations"></a>Ograniczenia
Są to bardzo proste przykłady otaczającego hello rozkładu normalnego. Jak wynika z powyższych hello przykładowy kod, małego Przechwytywanie błędu jest zaimplementowana.

## <a name="faq"></a>Często zadawane pytania
Często zadawane pytania dotyczące wykorzystania hello usługi sieci web lub toohello publikowania portalu Azure Marketplace, zobacz [tutaj](machine-learning-marketplace-faq.md).

[1]: ./media/machine-learning-r-csharp-normal-distribution/normal-img1.png
[2]: ./media/machine-learning-r-csharp-normal-distribution/normal-img2.png
[3]: ./media/machine-learning-r-csharp-normal-distribution/normal-img3.png
[4]: ./media/machine-learning-r-csharp-normal-distribution/normal-img4.png

