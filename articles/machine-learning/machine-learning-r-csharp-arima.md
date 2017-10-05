---
title: "(przestarzałe) Funkcja prognozowania: Autoregressive zintegrowane przeniesienie średniej (ARIMA) - Azure | Dokumentacja firmy Microsoft"
description: "(przestarzałe) Funkcja prognozowania - Autoregressive zintegrowane przeniesienie średniej (ARIMA)"
services: machine-learning
documentationcenter: 
author: yijichen
manager: jhubbard
editor: cgronlun
ms.assetid: 1e0d525f-8a9e-4b42-87e0-c9423f059f8c
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: yijichen
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: TRUE
ms.openlocfilehash: 6be76618c8ce5917f8fdfdea851c3ca65f9fddd4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-forecasting---autoregressive-integrated-moving-average-arima"></a>(przestarzałe) Funkcja prognozowania - Autoregressive zintegrowane przeniesienie średniej (ARIMA)

> [!NOTE]
> Microsoft DataMarket została wycofana i ten interfejs API jest przestarzały. 
> 
> Możesz znaleźć wiele eksperymenty przykład przydatne i interfejsów API w [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com). Aby uzyskać więcej informacji o galerii, zobacz [udziału i odnajdywania zasobów w Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).


To [usługi](https://datamarket.azure.com/dataset/aml_labs/arima) implementuje Autoregressive zintegrowane przeniesienie średniej (ARIMA) do tworzenia prognoz na podstawie historycznych danych przez użytkownika. Żądanie dla określonego produktu zwiększy tego roku? Można I przewidywanie Moje sprzedaży produktów w sezonie świąt tak, aby efektywnie można zaplanować Mój spis? Modeli prognozowania są w stanie rozwiązać takie pytania. Podana historycznych danych, te modele Sprawdź, czy ukryty trendów i sezonowości do przewidywania przyszłych trendów. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

> Ta usługa sieci web może być używana przez użytkowników — potencjalnie za pomocą aplikacji mobilnej, za pośrednictwem witryny sieci Web lub nawet na komputerze lokalnym, na przykład. Ale celem usługi sieci web jest również służyć jako przykład sposobu użycia usługi Azure Machine Learning do tworzenia usług sieci web na podstawie kodu języka R. Przy użyciu kilku wierszy kodu języka R i kliknięcia przycisku w usłudze Azure Machine Learning Studio eksperyment można tworzyć z kodem R i opublikowane jako usługę sieci web. Usługi sieci web może następnie opublikowane w portalu Azure Marketplace i używane przez użytkowników i urządzeń w całym świecie bez ustawień infrastruktury przez autora usługi sieci web.
> 
> 

## <a name="consumption-of-web-service"></a>Użycie usługi sieci web
Ta usługa akceptuje 4 argumenty i oblicza prognoz ARIMA.
Argumenty wejściowe są:

* Częstotliwość — wskazuje częstotliwość nieprzetworzone dane (codziennie/co tydzień/co miesiąc/co kwartał/co rok).
* Zakres - przyszłości prognozy przedziale czasu.
* Data — Dodawanie nowych danych serii czas po raz.
* Wartość — Dodawanie nowych wartości czasu serii danych.

Dane wyjściowe usługi są wartościami wyliczanymi prognozy. 

Przykładowe dane wejściowe może być: 

* Częstotliwość - 12
* Zakres - 12
* Data — 15/1/2012 15-2/2012; 3/15/2012; 4 15/2012; 15-5/2012; 6/15/2012; 7, 15/2012; 8 / 15 2012 9, 15/2012 10/15/2012; 11 15/2012; 12/15/2012; 1/15/2013 2013-2/15; 2013-3/15; 2013-4/15; 2013-5/15; 6/15/2013; 2013-7/15; 8 / 15/2013 2013-9/15; 10/15/2013; 11/15/2013; 12/15/2013; 2014-1-15, 2014-2-15, 2014-3-15; 2014-4-15; 2014-5-15; 2014-6-15; 2014-7-15, 8 / 2014-15; 2014-9-15
* Wartość — 3.479; 3.68; 3.832; 3.941; 3.797; 3.586; 3.508; 3.731; 3.915; 3.844; 3.634; 3.549; 3.557; 3.785; 3.782; 3.601; 3.544; 3.556; 3.65; 3.709; 3.682; 3.511; 3.429 3.51; 3.523; 3.525; 3.626; 3.695; 3.711; 3.711; 3.693; 3.571; 3.509

> Ta usługa hostowana w portalu Azure Marketplace jest usługi OData; te można wywoływać za pomocą metody POST lub GET. 
> 
> 

Istnieje wiele sposobów używania usługi w zautomatyzowany sposób (przykładową aplikację jest [tutaj](http://microsoftazuremachinelearning.azurewebsites.net/ArimaForecasting.aspx)).

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
          var input = new Input() { frequency = TextBox1.Text, horizon = TextBox2.Text, date = TextBox3.Text, value = TextBox4.Text };
        var json = JsonConvert.SerializeObject(input);
        var acitionUri =  "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";

          var httpClient = new HttpClient();
           httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere","ChangeToAPIKey");
           httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));
          var query = httpClient.PostAsync(acitionUri,new StringContent(json));
          var result = query.Result.Content;
          var scoreResult = result.ReadAsStringAsync().Result;
      }

## <a name="creation-of-web-service"></a>Tworzenie usługi sieci web
> Ta usługa sieci web został utworzony przy użyciu usługi Azure Machine Learning. Bezpłatna wersja próbna, a także wprowadzające filmy wideo dotyczące tworzenia eksperymenty i [publikowania usług sieci web](machine-learning-publish-a-machine-learning-web-service.md), można znaleźć pod adresem [azure.com/ml](http://azure.com/ml). Poniżej przedstawiono zrzut ekranu doświadczenia utworzony kod przykład i usługi sieci web dla każdego z modułów w ramach eksperymentu.
> 
> 

Za pomocą w usłudze Azure Machine Learning nowy pusty eksperyment została utworzona. Przekazany ze schematem wstępnie zdefiniowanych danych przykładowych danych wejściowych. Połączony z danymi schemat jest [wykonanie skryptu języka R] [ execute-r-script] moduł, który generuje ARIMA, funkcja prognozowania modelu przy użyciu funkcji "auto.arima" i "prognozy" z R. 

### <a name="experiment-flow"></a>Przepływ eksperymentu:
![Tworzenie obszaru roboczego][2]

#### <a name="module-1"></a>Moduł 1:
    # Add in the CSV file with the data in the format shown below 
![Tworzenie obszaru roboczego][3]    

#### <a name="module-2"></a>Moduł 2:
    # data input
    data <- maml.mapInputPort(1) # class: data.frame
    library(forecast)

    # preprocessing
    colnames(data) <- c("frequency", "horizon", "dates", "values")
    dates <- strsplit(data$dates, ";")[[1]]
    values <- strsplit(data$values, ";")[[1]]

    dates <- as.Date(dates, format = '%m/%d/%Y')
    values <- as.numeric(values)

    # fit a time-series model
    train_ts<- ts(values, frequency=data$frequency)
    fit1 <- auto.arima(train_ts)
    train_model <- forecast(fit1, h = data$horizon)
    plot(train_model)

    # produce forecasting
    train_pred <- round(train_model$mean,2)
    data.forecast <- as.data.frame(t(train_pred))
    colnames(data.forecast) <- paste("Forecast", 1:data$horizon, sep="")

    # data output
    maml.mapOutputPort("data.forecast");


## <a name="limitations"></a>Ograniczenia
Jest bardzo prosty przykład prognozowania ARIMA. Jak wynika z przykładowy kod powyżej, nie błąd Przechwytywanie jest zaimplementowana, a usługa przyjęto założenie, że wszystkie zmienne są ciągłe/dodatnie wartości i częstotliwości powinna być liczbą całkowitą większą niż 1. Długość wektorów wartość daty i powinna być taka sama. Zmienna daty należy stosować się do formatu ' mm/dd/rrrr'.

## <a name="faq"></a>Często zadawane pytania
Często zadawane pytania dotyczące wykorzystania usługi sieci web i publikowanie w portalu marketplace, zobacz [tutaj](machine-learning-marketplace-faq.md).

[1]: ./media/machine-learning-r-csharp-arima/arima-img1.png
[2]: ./media/machine-learning-r-csharp-arima/arima-img2.png
[3]: ./media/machine-learning-r-csharp-arima/arima-img3.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

