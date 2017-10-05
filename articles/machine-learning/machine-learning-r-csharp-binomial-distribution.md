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
# <a name="deprecated-binomial-distribution-suite"></a>(przestarzałe) Pakiet dwumianowy

> [!NOTE]
> Microsoft DataMarket została wycofana i ten interfejs API jest przestarzały. 
> 
> Możesz znaleźć wiele eksperymenty przykład przydatne i interfejsów API w [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com). Aby uzyskać więcej informacji o galerii, zobacz [udziału i odnajdywania zasobów w Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).

Pakiet dwumianowy to zestaw usług sieci web przykładowej ([Generator dwumianowy](https://datamarket.azure.com/dataset/aml_labs/bdg5), [Kalkulator prawdopodobieństwo](https://datamarket.azure.com/dataset/aml_labs/bdp4), [Kalkulator kwantyl](https://datamarket.azure.com/dataset/aml_labs/bdq5)) ułatwiające podczas generowania i dotyczącą dwumianowy dystrybucji. Usługi pozwalają generowania sekwencję dwumianowy o dowolnej długości obliczanie quantiles z podanej prawdopodobieństwo i obliczanie prawdopodobieństwa z danym kwantyl. Emituje każdej z usług innej dane wyjściowe na podstawie wybranej usługi (zobacz opis poniżej). Pakiet dwumianowy opiera się na qbinom funkcje R, rbinom i pbinom, które są zawarte w pakiecie Statystyka R. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

> Te usługi sieci web może być używana przez użytkowników — potencjalnie bezpośrednio w portalu marketplace, za pomocą aplikacji mobilnej, za pośrednictwem witryny sieci Web lub nawet na komputerze lokalnym, na przykład. Ale celem usługi sieci web jest również służyć jako przykład sposobu użycia usługi Azure Machine Learning do tworzenia usług sieci web na podstawie kodu języka R. Przy użyciu kilku wierszy kodu języka R i kliknięcia przycisku w usłudze Azure Machine Learning Studio eksperyment można tworzyć z kodem R i opublikowane jako usługę sieci web. Następnie usługa sieci web mogą być publikowane w portalu Azure Marketplace i używane przez użytkowników i urządzeń na całym świecie — nie konfigurowania infrastruktury przez autora usługi sieci web jest wymagana.
> 
> 

## <a name="consumption-of-web-service"></a>Użycie usługi sieci web
Pakiet dwumianowy obejmują następujące usługi 3.

### <a name="binomial-distribution-quantile-calculator"></a>Kalkulator kwantyl dwumianowy
Ta usługa akceptuje 4 argumenty rozkładu normalnego i oblicza kwantyl skojarzone.
Argumenty wejściowe są:

* p - pojedynczego zagregowane prawdopodobieństwo wielu prób.  
* rozmiar — liczba prób.
* PRAWDPD - prawdopodobieństwo sukcesu w wersji próbnej.
* Strona - L stronie niższe rozkładu U dla górna część dystrybucji. 

Dane wyjściowe usługi jest kwantyl obliczeniowych, który jest skojarzony z danym prawdopodobieństwa.

### <a name="binomial-distribution-probability-calculator"></a>Kalkulator prawdopodobieństwo dwumianowy
Ta usługa akceptuje 4 argumenty dwumianowy i oblicza prawdopodobieństwo skojarzone.
Argumenty wejściowe są:

* q - pojedynczego kwantyl zdarzenia z dwumianowy. 
* rozmiar — liczba prób.
* PRAWDPD - prawdopodobieństwo sukcesu w wersji próbnej.
* Strona - L stronie niższe rozkładu U dla górna część dystrybucji lub E równą jeden numer sukcesy.

Dane wyjściowe usługi jest obliczeniowej prawdopodobieństwo, że jest skojarzony z danym kwantyl.

### <a name="binomial-distribution-generator"></a>Generator dwumianowy
Ta usługa akceptuje 3 argumenty dwumianowy i generuje sekwencję losowych liczb, które są dystrybuowane binomially. W ramach żądania do niej należy podać następujące argumenty:

* n - liczba uwag. 
* rozmiar — liczba prób.
* PRAWDPD - prawdopodobieństwo sukcesu.

Dane wyjściowe usługi jest sekwencją n długość z dwumianowy, oparto na argumentach rozmiaru i PRAWDPD.

> Ta usługa hostowana w portalu Azure Marketplace jest usługi OData; te można wywoływać za pomocą metody POST lub GET. 
> 
> 

Istnieje wiele sposobów używania usługi w zautomatyzowany sposób (przykładowe aplikacje są w tym miejscu: [Generator](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionGenerator.aspx), [Kalkulator prawdopodobieństwo](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionProbabilityCalculator.aspx), [Kalkulator kwantyl](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionQuantileCalculator)). 

### <a name="starting-c-code-for-web-service-consumption"></a>Rozpoczynanie korzystania z usług sieci web kod C#:
### <a name="binomial-distribution-quantile-calculator"></a>Kalkulator kwantyl dwumianowy
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

### <a name="binomial-distribution-probability-calculator"></a>Kalkulator prawdopodobieństwo dwumianowy
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


### <a name="binomial-distribution-generator"></a>Generator dwumianowy
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





## <a name="creation-of-web-service"></a>Tworzenie usługi sieci web
> Ta usługa sieci web został utworzony przy użyciu usługi Azure Machine Learning. Bezpłatna wersja próbna, a także wprowadzające filmy wideo dotyczące tworzenia eksperymenty i [publikowania usług sieci web](machine-learning-publish-a-machine-learning-web-service.md), można znaleźć pod adresem [azure.com/ml](http://azure.com/ml). Poniżej przedstawiono zrzut ekranu doświadczenia utworzony kod przykład i usługi sieci web dla każdego z modułów w ramach eksperymentu.
> 
> 

### <a name="binomial-distribution-quantile-calculator"></a>Kalkulator kwantyl dwumianowy
![Tworzenie obszaru roboczego][4]

#### <a name="module-1"></a>Moduł 1:
    #data schema with example data (replaced with data from web service)
    data.set=data.frame(p=0.1,size=10,prob=.5,side='L');
    maml.mapOutputPort("data.set"); #send data to output port
#### <a name="module-2"></a>Moduł 2:
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


### <a name="binomial-distribution-probability-calculator"></a>Kalkulator prawdopodobieństwo dwumianowy
![Tworzenie obszaru roboczego][5]

#### <a name="module-1"></a>Moduł 1:
    #data schema with example data (replaced with data from web service)
    data.set=data.frame(q=5,size=10,prob=.5,side='L');
    maml.mapOutputPort("data.set"); #send data to output port


#### <a name="module-2"></a>Moduł 2:
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

### <a name="binomial-distribution-generator"></a>Generator dwumianowy
![Tworzenie obszaru roboczego][6]

#### <a name="module-1"></a>Moduł 1:
    #data schema with example data (replaced with data from web service)
    data.set=data.frame(n=50,size=10,p=.5);
    maml.mapOutputPort("data.set"); #send data to output port

#### <a name="module-2"></a>Moduł 2:
    dataset1 <- maml.mapInputPort(1) # class: data.frame
    param = dataset1
    dist = rbinom(param$n,param$size,param$p)

    output = as.data.frame(t(dist))

    # Select data.frame to be sent to the output Dataset port
    maml.mapOutputPort("output");

## <a name="limitations"></a>Ograniczenia
Są to bardzo proste przykłady otaczającego dwumianowy. Jak wynika z przykładowy kod powyżej, małego Przechwytywanie błędu jest zaimplementowana.

## <a name="faq"></a>Często zadawane pytania
Często zadawane pytania dotyczące wykorzystania usługi sieci web i publikowanie w portalu Azure Marketplace, zobacz [tutaj](machine-learning-marketplace-faq.md).

[1]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_1.png

[2]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_2.png

[3]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_3.png

[4]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_4.png

[5]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_5.png

[6]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_6.png

