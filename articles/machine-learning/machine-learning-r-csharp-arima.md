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
# <a name="deprecated-forecasting---autoregressive-integrated-moving-average-arima"></a><span data-ttu-id="25594-103">(przestarzałe) Funkcja prognozowania - Autoregressive zintegrowane przeniesienie średniej (ARIMA)</span><span class="sxs-lookup"><span data-stu-id="25594-103">(deprecated) Forecasting - Autoregressive Integrated Moving Average (ARIMA)</span></span>

> [!NOTE]
> <span data-ttu-id="25594-104">Microsoft DataMarket została wycofana i ten interfejs API jest przestarzały.</span><span class="sxs-lookup"><span data-stu-id="25594-104">The Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="25594-105">Możesz znaleźć wiele eksperymenty przykład przydatne i interfejsów API w [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="25594-105">You can find many useful example experiments and APIs in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="25594-106">Aby uzyskać więcej informacji o galerii, zobacz [udziału i odnajdywania zasobów w Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="25594-106">For more information about the Gallery, see [Share and discover resources in the Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>


<span data-ttu-id="25594-107">To [usługi](https://datamarket.azure.com/dataset/aml_labs/arima) implementuje Autoregressive zintegrowane przeniesienie średniej (ARIMA) do tworzenia prognoz na podstawie historycznych danych przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="25594-107">This [service](https://datamarket.azure.com/dataset/aml_labs/arima) implements Autoregressive Integrated Moving Average (ARIMA) to produce predictions based on the historical data provided by the user.</span></span> <span data-ttu-id="25594-108">Żądanie dla określonego produktu zwiększy tego roku?</span><span class="sxs-lookup"><span data-stu-id="25594-108">Will the demand for a specific product increase this year?</span></span> <span data-ttu-id="25594-109">Można I przewidywanie Moje sprzedaży produktów w sezonie świąt tak, aby efektywnie można zaplanować Mój spis?</span><span class="sxs-lookup"><span data-stu-id="25594-109">Can I predict my product sales for the Christmas season, so that I can effectively plan my inventory?</span></span> <span data-ttu-id="25594-110">Modeli prognozowania są w stanie rozwiązać takie pytania.</span><span class="sxs-lookup"><span data-stu-id="25594-110">Forecasting models are apt to address such questions.</span></span> <span data-ttu-id="25594-111">Podana historycznych danych, te modele Sprawdź, czy ukryty trendów i sezonowości do przewidywania przyszłych trendów.</span><span class="sxs-lookup"><span data-stu-id="25594-111">Given the past data, these models examine hidden trends and seasonality to predict future trends.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

> <span data-ttu-id="25594-112">Ta usługa sieci web może być używana przez użytkowników — potencjalnie za pomocą aplikacji mobilnej, za pośrednictwem witryny sieci Web lub nawet na komputerze lokalnym, na przykład.</span><span class="sxs-lookup"><span data-stu-id="25594-112">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="25594-113">Ale celem usługi sieci web jest również służyć jako przykład sposobu użycia usługi Azure Machine Learning do tworzenia usług sieci web na podstawie kodu języka R.</span><span class="sxs-lookup"><span data-stu-id="25594-113">But the purpose of the web service is also to serve as an example of how Azure Machine Learning can be used to create web services on top of R code.</span></span> <span data-ttu-id="25594-114">Przy użyciu kilku wierszy kodu języka R i kliknięcia przycisku w usłudze Azure Machine Learning Studio eksperyment można tworzyć z kodem R i opublikowane jako usługę sieci web.</span><span class="sxs-lookup"><span data-stu-id="25594-114">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="25594-115">Usługi sieci web może następnie opublikowane w portalu Azure Marketplace i używane przez użytkowników i urządzeń w całym świecie bez ustawień infrastruktury przez autora usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="25594-115">The web service can then be published to the Azure Marketplace and consumed by users and devices across the world with no infrastructure setup by the author of the web service.</span></span>
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="25594-116">Użycie usługi sieci web</span><span class="sxs-lookup"><span data-stu-id="25594-116">Consumption of web service</span></span>
<span data-ttu-id="25594-117">Ta usługa akceptuje 4 argumenty i oblicza prognoz ARIMA.</span><span class="sxs-lookup"><span data-stu-id="25594-117">This service accepts 4 arguments and calculates the ARIMA forecasts.</span></span>
<span data-ttu-id="25594-118">Argumenty wejściowe są:</span><span class="sxs-lookup"><span data-stu-id="25594-118">The input arguments are:</span></span>

* <span data-ttu-id="25594-119">Częstotliwość — wskazuje częstotliwość nieprzetworzone dane (codziennie/co tydzień/co miesiąc/co kwartał/co rok).</span><span class="sxs-lookup"><span data-stu-id="25594-119">Frequency - Indicates the frequency of the raw data (daily/weekly/monthly/quarterly/yearly).</span></span>
* <span data-ttu-id="25594-120">Zakres - przyszłości prognozy przedziale czasu.</span><span class="sxs-lookup"><span data-stu-id="25594-120">Horizon - Future forecast time-frame.</span></span>
* <span data-ttu-id="25594-121">Data — Dodawanie nowych danych serii czas po raz.</span><span class="sxs-lookup"><span data-stu-id="25594-121">Date - Add in the new time series data for time.</span></span>
* <span data-ttu-id="25594-122">Wartość — Dodawanie nowych wartości czasu serii danych.</span><span class="sxs-lookup"><span data-stu-id="25594-122">Value - Add in the new time series data values.</span></span>

<span data-ttu-id="25594-123">Dane wyjściowe usługi są wartościami wyliczanymi prognozy.</span><span class="sxs-lookup"><span data-stu-id="25594-123">The output of the service is the calculated forecast values.</span></span> 

<span data-ttu-id="25594-124">Przykładowe dane wejściowe może być:</span><span class="sxs-lookup"><span data-stu-id="25594-124">Sample input could be:</span></span> 

* <span data-ttu-id="25594-125">Częstotliwość - 12</span><span class="sxs-lookup"><span data-stu-id="25594-125">Frequency - 12</span></span>
* <span data-ttu-id="25594-126">Zakres - 12</span><span class="sxs-lookup"><span data-stu-id="25594-126">Horizon - 12</span></span>
* <span data-ttu-id="25594-127">Data — 15/1/2012 15-2/2012; 3/15/2012; 4 15/2012; 15-5/2012; 6/15/2012; 7, 15/2012; 8 / 15 2012 9, 15/2012 10/15/2012; 11 15/2012; 12/15/2012; 1/15/2013 2013-2/15; 2013-3/15; 2013-4/15; 2013-5/15; 6/15/2013; 2013-7/15; 8 / 15/2013 2013-9/15; 10/15/2013; 11/15/2013; 12/15/2013; 2014-1-15, 2014-2-15, 2014-3-15; 2014-4-15; 2014-5-15; 2014-6-15; 2014-7-15, 8 / 2014-15; 2014-9-15</span><span class="sxs-lookup"><span data-stu-id="25594-127">Date - 1/15/2012;2/15/2012;3/15/2012;4/15/2012;5/15/2012;6/15/2012;7/15/2012;8/15/2012;9/15/2012;10/15/2012;11/15/2012;12/15/2012; 1/15/2013;2/15/2013;3/15/2013;4/15/2013;5/15/2013;6/15/2013;7/15/2013;8/15/2013;9/15/2013;10/15/2013;11/15/2013;12/15/2013; 1/15/2014;2/15/2014;3/15/2014;4/15/2014;5/15/2014;6/15/2014;7/15/2014;8/15/2014;9/15/2014</span></span>
* <span data-ttu-id="25594-128">Wartość — 3.479; 3.68; 3.832; 3.941; 3.797; 3.586; 3.508; 3.731; 3.915; 3.844; 3.634; 3.549; 3.557; 3.785; 3.782; 3.601; 3.544; 3.556; 3.65; 3.709; 3.682; 3.511; 3.429 3.51; 3.523; 3.525; 3.626; 3.695; 3.711; 3.711; 3.693; 3.571; 3.509</span><span class="sxs-lookup"><span data-stu-id="25594-128">Value - 3.479;3.68;3.832;3.941;3.797;3.586;3.508;3.731;3.915;3.844;3.634;3.549;3.557;3.785;3.782;3.601;3.544;3.556;3.65;3.709;3.682;3.511; 3.429;3.51;3.523;3.525;3.626;3.695;3.711;3.711;3.693;3.571;3.509</span></span>

> <span data-ttu-id="25594-129">Ta usługa hostowana w portalu Azure Marketplace jest usługi OData; te można wywoływać za pomocą metody POST lub GET.</span><span class="sxs-lookup"><span data-stu-id="25594-129">This service, as hosted on the Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="25594-130">Istnieje wiele sposobów używania usługi w zautomatyzowany sposób (przykładową aplikację jest [tutaj](http://microsoftazuremachinelearning.azurewebsites.net/ArimaForecasting.aspx)).</span><span class="sxs-lookup"><span data-stu-id="25594-130">There are multiple ways of consuming the service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/ArimaForecasting.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="25594-131">Rozpoczynanie korzystania z usług sieci web kod C#:</span><span class="sxs-lookup"><span data-stu-id="25594-131">Starting C# code for web service consumption:</span></span>
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

## <a name="creation-of-web-service"></a><span data-ttu-id="25594-132">Tworzenie usługi sieci web</span><span class="sxs-lookup"><span data-stu-id="25594-132">Creation of web service</span></span>
> <span data-ttu-id="25594-133">Ta usługa sieci web został utworzony przy użyciu usługi Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="25594-133">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="25594-134">Bezpłatna wersja próbna, a także wprowadzające filmy wideo dotyczące tworzenia eksperymenty i [publikowania usług sieci web](machine-learning-publish-a-machine-learning-web-service.md), można znaleźć pod adresem [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="25594-134">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="25594-135">Poniżej przedstawiono zrzut ekranu doświadczenia utworzony kod przykład i usługi sieci web dla każdego z modułów w ramach eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="25594-135">Below is a screenshot of the experiment that created the web service and example code for each of the modules within the experiment.</span></span>
> 
> 

<span data-ttu-id="25594-136">Za pomocą w usłudze Azure Machine Learning nowy pusty eksperyment została utworzona.</span><span class="sxs-lookup"><span data-stu-id="25594-136">From within Azure Machine Learning, a new blank experiment was created.</span></span> <span data-ttu-id="25594-137">Przekazany ze schematem wstępnie zdefiniowanych danych przykładowych danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="25594-137">Sample input data was uploaded with a predefined data schema.</span></span> <span data-ttu-id="25594-138">Połączony z danymi schemat jest [wykonanie skryptu języka R] [ execute-r-script] moduł, który generuje ARIMA, funkcja prognozowania modelu przy użyciu funkcji "auto.arima" i "prognozy" z R.</span><span class="sxs-lookup"><span data-stu-id="25594-138">Linked to the data schema is an [Execute R Script][execute-r-script] module, which generates the ARIMA forecasting model by using ‘auto.arima’ and ‘forecast’ functions from R.</span></span> 

### <a name="experiment-flow"></a><span data-ttu-id="25594-139">Przepływ eksperymentu:</span><span class="sxs-lookup"><span data-stu-id="25594-139">Experiment flow:</span></span>
![Tworzenie obszaru roboczego][2]

#### <a name="module-1"></a><span data-ttu-id="25594-141">Moduł 1:</span><span class="sxs-lookup"><span data-stu-id="25594-141">Module 1:</span></span>
    # Add in the CSV file with the data in the format shown below 
![Tworzenie obszaru roboczego][3]    

#### <a name="module-2"></a><span data-ttu-id="25594-143">Moduł 2:</span><span class="sxs-lookup"><span data-stu-id="25594-143">Module 2:</span></span>
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


## <a name="limitations"></a><span data-ttu-id="25594-144">Ograniczenia</span><span class="sxs-lookup"><span data-stu-id="25594-144">Limitations</span></span>
<span data-ttu-id="25594-145">Jest bardzo prosty przykład prognozowania ARIMA.</span><span class="sxs-lookup"><span data-stu-id="25594-145">This is a very simple example for ARIMA forecasting.</span></span> <span data-ttu-id="25594-146">Jak wynika z przykładowy kod powyżej, nie błąd Przechwytywanie jest zaimplementowana, a usługa przyjęto założenie, że wszystkie zmienne są ciągłe/dodatnie wartości i częstotliwości powinna być liczbą całkowitą większą niż 1.</span><span class="sxs-lookup"><span data-stu-id="25594-146">As can be seen from the example code above, no error catching is implemented, and the service assumes that all the variables are continuous/positive values and the frequency should be an integer greater than 1.</span></span> <span data-ttu-id="25594-147">Długość wektorów wartość daty i powinna być taka sama.</span><span class="sxs-lookup"><span data-stu-id="25594-147">The length of the date and value vectors should be the same.</span></span> <span data-ttu-id="25594-148">Zmienna daty należy stosować się do formatu ' mm/dd/rrrr'.</span><span class="sxs-lookup"><span data-stu-id="25594-148">The date variable should adhere to the format ‘mm/dd/yyyy’.</span></span>

## <a name="faq"></a><span data-ttu-id="25594-149">Często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="25594-149">FAQ</span></span>
<span data-ttu-id="25594-150">Często zadawane pytania dotyczące wykorzystania usługi sieci web i publikowanie w portalu marketplace, zobacz [tutaj](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="25594-150">For frequently asked questions on consumption of the web service or publishing to marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-arima/arima-img1.png
[2]: ./media/machine-learning-r-csharp-arima/arima-img2.png
[3]: ./media/machine-learning-r-csharp-arima/arima-img3.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

