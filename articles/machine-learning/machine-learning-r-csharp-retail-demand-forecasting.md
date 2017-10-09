---
title: AAA(deprecated) Prognozowanie - ETS + STL - Azure | Dokumentacja firmy Microsoft
description: "(przestarzałe) Funkcja prognozowania - ETS + STL"
services: machine-learning
documentationcenter: 
author: xueshanz
manager: jhubbard
editor: cgronlun
ms.assetid: 153eab4d-6293-45e1-9871-ec339e810dd9
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: yijichen
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: 550d423898d46564936fdcfbf05b7c88d2e292c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-forecasting---ets--stl"></a>(przestarzałe) Funkcja prognozowania - ETS + STL

> [!NOTE]
> Witaj Microsoft DataMarket została wycofana i ten interfejs API jest przestarzały. 
> 
> Możesz znaleźć wiele interfejsów API i przydatne przykład eksperymenty w hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com). Aby uzyskać więcej informacji na temat hello galerii, zobacz [udziału i odnajdywania zasobów w hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).

To [usługi sieci web](https://datamarket.azure.com/dataset/aml_labs/demand_forecast) implementuje prognoz tooproduce modeli okresach Trend rozkładu (STL) i wykładniczej Wygładzanie (ETS) na podstawie hello danych historycznych podane przez użytkownika hello. Zostanie hello żądanie zwiększanie określonym produktem tego roku? Można I przewidywanie Moje sprzedaży produktu hello sezonu świąt tak, aby efektywnie można zaplanować Mój spis? Modeli prognozowania są stanie tooaddress takie pytania. Podane hello poza danych, te modele Sprawdź, czy ukryty trendów i sezonowości toopredict przyszłych trendów. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

> Ta usługa sieci web może być używana przez użytkowników — potencjalnie za pomocą aplikacji mobilnej, za pośrednictwem witryny sieci Web lub nawet na komputerze lokalnym, na przykład. Ale hello hello usługi sieci web służy również tooserve, na przykład jak usługi Azure Machine Learning można toocreate używanych usług sieci web na podstawie kodu języka R. Przy użyciu kilku wierszy kodu języka R i kliknięcia przycisku w usłudze Azure Machine Learning Studio eksperyment można tworzyć z kodem R i opublikowane jako usługę sieci web. usługi sieci web Hello można następnie toohello opublikowane w portalu Azure Marketplace i używane przez użytkowników i urządzeń w Witaj świecie bez ustawień infrastruktury przez autora hello hello usługi sieci web.  
> 
> 

## <a name="consumption-of-web-service"></a>Użycie usługi sieci web
Ta usługa akceptuje 4 argumenty i oblicza hello prognozy.
argumenty wejściowe Hello są:

* Częstotliwość — wskazuje częstotliwość hello hello nieprzetworzone dane (codziennie/co tydzień/co miesiąc/co kwartał/co rok).
* Zakres - przyszłości prognozy przedziale czasu.
* Data — Dodawanie nowych szeregów czasowych hello danych po raz.
* Wartość — dodatek hello wartości danych w nowej serii czasu.

dane wyjściowe Hello usługi hello jest hello obliczany prognozowania wartości.

Przykładowe dane wejściowe może być: 

* Częstotliwość - 12
* Zakres - 12
* Data — 15/1/2012 15-2/2012; 3/15/2012; 4 15/2012; 15-5/2012; 6/15/2012; 7, 15/2012; 8 / 15 2012 9, 15/2012 10/15/2012; 11 15/2012; 12/15/2012; 1/15/2013 2013-2/15; 2013-3/15; 2013-4/15; 2013-5/15; 6/15/2013; 2013-7/15; 8 / 15/2013 2013-9/15; 10/15/2013; 11/15/2013; 12/15/2013; 2014-1-15, 2014-2-15, 2014-3-15; 2014-4-15; 2014-5-15; 2014-6-15; 2014-7-15, 8 / 2014-15; 2014-9-15
* Wartość — 3.479; 3.68; 3.832; 3.941; 3.797; 3.586; 3.508; 3.731; 3.915; 3.844; 3.634; 3.549; 3.557; 3.785; 3.782; 3.601; 3.544; 3.556; 3.65; 3.709; 3.682; 3.511; 3.429 3.51; 3.523; 3.525; 3.626; 3.695; 3.711; 3.711; 3.693; 3.571; 3.509

> Ta usługa hostowana na hello Azure Marketplace jest usługi OData; te można wywoływać za pomocą metody POST lub GET. 
> 
> 

Istnieje wiele sposobów używania usługi hello w zautomatyzowany sposób (przykładową aplikację jest [tutaj](http://microsoftazuremachinelearning.azurewebsites.net/StlEtsForecasting.aspx)).

### <a name="starting-c-code-for-web-service-consumption"></a>Rozpoczynanie korzystania z usług sieci web kod C#:
    public class Input
    {
            public string frequency;
            public string horizon;
            public string date;
            public string value;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { frequency = TextBox1.Text, horizon = TextBox2.Text, date = TextBox3.Text, value = TextBox4.Text };         var json = JsonConvert.SerializeObject(input);
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

Za pomocą w usłudze Azure Machine Learning nowy pusty eksperyment została utworzona. Przekazany ze schematem wstępnie zdefiniowanych danych przykładowych danych wejściowych. Schemat danych połączonych toohello jest [wykonanie skryptu języka R] [ execute-r-script] moduł, generująca STL i ETS modeli prognozowania za pomocą "stl", "ets" i "prognozy" działa z R. 

### <a name="experiment-flow"></a>Przepływ eksperymentu:
![Przepływ eksperymentu][2]

#### <a name="module-1"></a>Moduł 1:
    # Add in hello CSV file with hello data in hello format shown below 
![Dane przykładowe][3]    

#### <a name="module-2"></a>Moduł 2:
    # Data input
    data <- maml.mapInputPort(1) # class: data.frame
    library(forecast)

    # Preprocessing
    colnames(data) <- c("frequency", "horizon", "dates", "values")
    dates <- strsplit(data$dates, ";")[[1]]
    values <- strsplit(data$values, ";")[[1]]

    dates <- as.Date(dates, format = '%m/%d/%Y')
    values <- as.numeric(values)

    # Fit a time series model
    train_ts<- ts(values, frequency=data$frequency)
    fit1 <- stl(train_ts,  s.window="periodic")
    train_model <- forecast(fit1, h = data$horizon, method = 'ets')
    plot(train_model)

    # Produce forcasting
    train_pred <- round(train_model$mean,2)
    data.forecast <- as.data.frame(t(train_pred))
    colnames(data.forecast) <- paste("Forecast", 1:data$horizon, sep="")

    # Data output
    maml.mapOutputPort("data.forecast");

## <a name="limitations"></a>Ograniczenia
To jest bardzo prosty przykład ETS + STL prognozowania. Jak wynika z powyższych hello przykładowy kod, nie błąd Przechwytywanie jest zaimplementowana, a usługa hello przyjęto założenie, że wszystkie zmienne hello są ciągłe/dodatnie wartości i częstotliwość hello musi być liczbą całkowitą większą niż 1. Hello długość wektorów hello wartość daty i powinny być takie same hello i hello hello szeregu czasowego musi być większa niż 2 * częstotliwości. Zmienna daty Hello przestrzegać toohello format "mm/dd/rrrr'.

## <a name="faq"></a>Często zadawane pytania
Często zadawane pytania dotyczące wykorzystania hello usługi sieci web lub toohello publikowania portalu Azure Marketplace, zobacz [tutaj](machine-learning-marketplace-faq.md).

[1]: ./media/machine-learning-r-csharp-retail-demand-forecasting/retail-img1.png
[2]: ./media/machine-learning-r-csharp-retail-demand-forecasting/retail-img2.png
[3]: ./media/machine-learning-r-csharp-retail-demand-forecasting/retail-img3.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

