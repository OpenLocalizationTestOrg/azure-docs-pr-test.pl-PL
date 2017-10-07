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
# <a name="deprecated-difference-in-proportions-test"></a>(przestarzałe) Różnica w teście proporcji

> [!NOTE]
> Witaj Microsoft DataMarket została wycofana i ten interfejs API jest przestarzały. 
> 
> Możesz znaleźć wiele interfejsów API i przydatne przykład eksperymenty w hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com). Aby uzyskać więcej informacji na temat hello galerii, zobacz [udziału i odnajdywania zasobów w hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).

Różnią się dwóch proporcji statystycznie? Załóżmy, że użytkownik chce, aby toodetermine filmy toocompare dwa, jeśli jeden film jest znacznie wyższa część "lubi" kiedy porównaniu toohello innych. Z przykładowym duży może być statystycznie znacząca różnica między proporcje hello 0,50 i 0,51. Z małej przykładowej prawdopodobnie toodetermine wystarczającej ilości danych jeśli proporcje te są faktycznie różne. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

To [usługi sieci web](https://datamarket.azure.com/dataset/aml_labs/prop_test) przeprowadza test hipoteza hello różnica dwóch proporcji oparte na danych wejściowych użytkownika hello liczbę sukcesów i hello łączna liczba prób dla grup porównania hello 2. Możliwy scenariusz tej usługi sieci web może być wywołana z poziomu movie app porównania, informuje użytkownika hello czy jedną filmy hello jest naprawdę "zbędne" częściej niż hello inne, na podstawie filmu klasyfikacji.

> Ta usługa sieci web może być używana przez użytkowników — potencjalnie za pomocą aplikacji mobilnej, za pośrednictwem witryny sieci Web lub nawet na komputerze lokalnym, na przykład. Ale hello hello usługi sieci web służy również tooserve, na przykład jak usługi Azure Machine Learning można toocreate używanych usług sieci web na podstawie kodu języka R. Przy użyciu kilku wierszy kodu języka R i kliknięcia przycisku w usłudze Azure Machine Learning Studio eksperyment można tworzyć z kodem R i opublikowane jako usługę sieci web. usługi sieci web Hello można następnie toohello opublikowane w portalu Azure Marketplace i używane przez użytkowników i urządzeń w Witaj świecie bez ustawień infrastruktury przez autora hello hello usługi sieci web.
> 
> 

## <a name="consumption-of-web-service"></a>Użycie usługi sieci web
Ta usługa akceptuje argumenty 4, i jest hipoteza testowych proporcji.

argumenty wejściowe Hello są:

* Successes1 — liczba zdarzeń pomyślnego w przykładzie 1.
* Successes2 — liczba zdarzeń pomyślnego w przykładzie 2.
* Total1 — rozmiar próbki 1.
* Total2 — rozmiar próbki 2.

dane wyjściowe Hello usługi hello jest wynikiem hello hipoteza hello test wraz z hello chi-square Statystyka, df, p wartość, a udział procentowy w granice 1/2 i przedział ufności próbki.

> Ta usługa hostowana na hello Azure Marketplace jest usługi OData; te można wywoływać za pomocą metody POST lub GET. 
> 
> 

Istnieje wiele sposobów używania usługi hello w zautomatyzowany sposób (przykładową aplikację jest [tutaj](http://microsoftazuremachinelearning.azurewebsites.net/DifferenceInProportionsTest.aspx)).

### <a name="starting-c-code-for-web-service-consumption"></a>Rozpoczynanie korzystania z usług sieci web kod C#:
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


## <a name="creation-of-web-service"></a>Tworzenie usługi sieci web
> Ta usługa sieci web został utworzony przy użyciu usługi Azure Machine Learning. Bezpłatna wersja próbna, a także wprowadzające filmy wideo dotyczące tworzenia eksperymenty i [publikowania usług sieci web](machine-learning-publish-a-machine-learning-web-service.md), można znaleźć pod adresem [azure.com/ml](http://azure.com/ml). Poniżej przedstawiono zrzut ekranu hello eksperymentu, utworzona hello kod przykład i usługi sieci web dla każdego z modułów hello w ramach eksperymentu hello.
> 
> 

Za pomocą w usłudze Azure Machine Learning nowy pusty eksperyment została utworzona przy użyciu dwóch [wykonanie skryptu języka R] [ execute-r-script] modułów. W module pierwszy hello hello schemat danych jest zdefiniowana, gdy drugi moduł hello używa polecenia prop.test hello R tooperform hello hipotetyczny test proporcje 2. 

### <a name="experiment-flow"></a>Przepływ eksperymentu:
![Przepływ eksperymentu][2]

#### <a name="module-1"></a>Moduł 1:
    ####Schema definition  
    data.set=data.frame(successes1=50,successes2=60,total1=100,total2=100);
    maml.mapOutputPort("data.set"); #send data toooutput port
    dataset1 = maml.mapInputPort(1) #read data from input port


#### <a name="module-2"></a>Moduł 2:
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


## <a name="limitations"></a>Ograniczenia
Jest bardzo prosty przykład dla testu różnicy w proporcjach 2. Jak wynika z powyższych hello przykładowy kod, nie błąd Przechwytywanie jest zaimplementowany i usługi hello zakłada, że wszystkie zmienne hello są ciągłe.

## <a name="faq"></a>Często zadawane pytania
Często zadawane pytania dotyczące wykorzystania hello usługi sieci web lub toohello publikowania portalu Azure Marketplace, zobacz [tutaj](machine-learning-marketplace-faq.md).

[1]: ./media/machine-learning-r-csharp-difference-in-two-proportions/hyptest-img1.png
[2]: ./media/machine-learning-r-csharp-difference-in-two-proportions/hyptest-img2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

