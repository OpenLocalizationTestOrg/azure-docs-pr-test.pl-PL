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
redirect_document_id: True
ms.openlocfilehash: 4f3af41fd8873fdf75c6426fd395351cb41db190
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-forecasting---autoregressive-integrated-moving-average-arima"></a><span data-ttu-id="f6801-103">(przestarzałe) Funkcja prognozowania - Autoregressive zintegrowane przeniesienie średniej (ARIMA)</span><span class="sxs-lookup"><span data-stu-id="f6801-103">(deprecated) Forecasting - Autoregressive Integrated Moving Average (ARIMA)</span></span>

> [!NOTE]
> <span data-ttu-id="f6801-104">Witaj Microsoft DataMarket została wycofana i ten interfejs API jest przestarzały.</span><span class="sxs-lookup"><span data-stu-id="f6801-104">hello Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="f6801-105">Możesz znaleźć wiele interfejsów API i przydatne przykład eksperymenty w hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="f6801-105">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="f6801-106">Aby uzyskać więcej informacji na temat hello galerii, zobacz [udziału i odnajdywania zasobów w hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="f6801-106">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>


<span data-ttu-id="f6801-107">To [usługi](https://datamarket.azure.com/dataset/aml_labs/arima) implementuje na podstawie danych historycznych hello podane przez użytkownika hello prognoz tooproduce Autoregressive zintegrowane przeniesienie średniej (ARIMA).</span><span class="sxs-lookup"><span data-stu-id="f6801-107">This [service](https://datamarket.azure.com/dataset/aml_labs/arima) implements Autoregressive Integrated Moving Average (ARIMA) tooproduce predictions based on hello historical data provided by hello user.</span></span> <span data-ttu-id="f6801-108">Zostanie hello żądanie zwiększanie określonym produktem tego roku?</span><span class="sxs-lookup"><span data-stu-id="f6801-108">Will hello demand for a specific product increase this year?</span></span> <span data-ttu-id="f6801-109">Można I przewidywanie Moje sprzedaży produktu hello sezonu świąt tak, aby efektywnie można zaplanować Mój spis?</span><span class="sxs-lookup"><span data-stu-id="f6801-109">Can I predict my product sales for hello Christmas season, so that I can effectively plan my inventory?</span></span> <span data-ttu-id="f6801-110">Modeli prognozowania są stanie tooaddress takie pytania.</span><span class="sxs-lookup"><span data-stu-id="f6801-110">Forecasting models are apt tooaddress such questions.</span></span> <span data-ttu-id="f6801-111">Podane hello poza danych, te modele Sprawdź, czy ukryty trendów i sezonowości toopredict przyszłych trendów.</span><span class="sxs-lookup"><span data-stu-id="f6801-111">Given hello past data, these models examine hidden trends and seasonality toopredict future trends.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

> <span data-ttu-id="f6801-112">Ta usługa sieci web może być używana przez użytkowników — potencjalnie za pomocą aplikacji mobilnej, za pośrednictwem witryny sieci Web lub nawet na komputerze lokalnym, na przykład.</span><span class="sxs-lookup"><span data-stu-id="f6801-112">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="f6801-113">Ale hello hello usługi sieci web służy również tooserve, na przykład jak usługi Azure Machine Learning można toocreate używanych usług sieci web na podstawie kodu języka R.</span><span class="sxs-lookup"><span data-stu-id="f6801-113">But hello purpose of hello web service is also tooserve as an example of how Azure Machine Learning can be used toocreate web services on top of R code.</span></span> <span data-ttu-id="f6801-114">Przy użyciu kilku wierszy kodu języka R i kliknięcia przycisku w usłudze Azure Machine Learning Studio eksperyment można tworzyć z kodem R i opublikowane jako usługę sieci web.</span><span class="sxs-lookup"><span data-stu-id="f6801-114">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="f6801-115">usługi sieci web Hello można następnie toohello opublikowane w portalu Azure Marketplace i używane przez użytkowników i urządzeń w Witaj świecie bez ustawień infrastruktury przez autora hello hello usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="f6801-115">hello web service can then be published toohello Azure Marketplace and consumed by users and devices across hello world with no infrastructure setup by hello author of hello web service.</span></span>
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="f6801-116">Użycie usługi sieci web</span><span class="sxs-lookup"><span data-stu-id="f6801-116">Consumption of web service</span></span>
<span data-ttu-id="f6801-117">Ta usługa akceptuje 4 argumenty i oblicza hello ARIMA prognozy.</span><span class="sxs-lookup"><span data-stu-id="f6801-117">This service accepts 4 arguments and calculates hello ARIMA forecasts.</span></span>
<span data-ttu-id="f6801-118">argumenty wejściowe Hello są:</span><span class="sxs-lookup"><span data-stu-id="f6801-118">hello input arguments are:</span></span>

* <span data-ttu-id="f6801-119">Częstotliwość — wskazuje częstotliwość hello hello nieprzetworzone dane (codziennie/co tydzień/co miesiąc/co kwartał/co rok).</span><span class="sxs-lookup"><span data-stu-id="f6801-119">Frequency - Indicates hello frequency of hello raw data (daily/weekly/monthly/quarterly/yearly).</span></span>
* <span data-ttu-id="f6801-120">Zakres - przyszłości prognozy przedziale czasu.</span><span class="sxs-lookup"><span data-stu-id="f6801-120">Horizon - Future forecast time-frame.</span></span>
* <span data-ttu-id="f6801-121">Data — Dodawanie nowych szeregów czasowych hello danych po raz.</span><span class="sxs-lookup"><span data-stu-id="f6801-121">Date - Add in hello new time series data for time.</span></span>
* <span data-ttu-id="f6801-122">Wartość — dodatek hello wartości danych w nowej serii czasu.</span><span class="sxs-lookup"><span data-stu-id="f6801-122">Value - Add in hello new time series data values.</span></span>

<span data-ttu-id="f6801-123">dane wyjściowe Hello usługi hello jest hello obliczany prognozowania wartości.</span><span class="sxs-lookup"><span data-stu-id="f6801-123">hello output of hello service is hello calculated forecast values.</span></span> 

<span data-ttu-id="f6801-124">Przykładowe dane wejściowe może być:</span><span class="sxs-lookup"><span data-stu-id="f6801-124">Sample input could be:</span></span> 

* <span data-ttu-id="f6801-125">Częstotliwość - 12</span><span class="sxs-lookup"><span data-stu-id="f6801-125">Frequency - 12</span></span>
* <span data-ttu-id="f6801-126">Zakres - 12</span><span class="sxs-lookup"><span data-stu-id="f6801-126">Horizon - 12</span></span>
* <span data-ttu-id="f6801-127">Data — 15/1/2012 15-2/2012; 3/15/2012; 4 15/2012; 15-5/2012; 6/15/2012; 7, 15/2012; 8 / 15 2012 9, 15/2012 10/15/2012; 11 15/2012; 12/15/2012; 1/15/2013 2013-2/15; 2013-3/15; 2013-4/15; 2013-5/15; 6/15/2013; 2013-7/15; 8 / 15/2013 2013-9/15; 10/15/2013; 11/15/2013; 12/15/2013; 2014-1-15, 2014-2-15, 2014-3-15; 2014-4-15; 2014-5-15; 2014-6-15; 2014-7-15, 8 / 2014-15; 2014-9-15</span><span class="sxs-lookup"><span data-stu-id="f6801-127">Date - 1/15/2012;2/15/2012;3/15/2012;4/15/2012;5/15/2012;6/15/2012;7/15/2012;8/15/2012;9/15/2012;10/15/2012;11/15/2012;12/15/2012; 1/15/2013;2/15/2013;3/15/2013;4/15/2013;5/15/2013;6/15/2013;7/15/2013;8/15/2013;9/15/2013;10/15/2013;11/15/2013;12/15/2013; 1/15/2014;2/15/2014;3/15/2014;4/15/2014;5/15/2014;6/15/2014;7/15/2014;8/15/2014;9/15/2014</span></span>
* <span data-ttu-id="f6801-128">Wartość — 3.479; 3.68; 3.832; 3.941; 3.797; 3.586; 3.508; 3.731; 3.915; 3.844; 3.634; 3.549; 3.557; 3.785; 3.782; 3.601; 3.544; 3.556; 3.65; 3.709; 3.682; 3.511; 3.429 3.51; 3.523; 3.525; 3.626; 3.695; 3.711; 3.711; 3.693; 3.571; 3.509</span><span class="sxs-lookup"><span data-stu-id="f6801-128">Value - 3.479;3.68;3.832;3.941;3.797;3.586;3.508;3.731;3.915;3.844;3.634;3.549;3.557;3.785;3.782;3.601;3.544;3.556;3.65;3.709;3.682;3.511; 3.429;3.51;3.523;3.525;3.626;3.695;3.711;3.711;3.693;3.571;3.509</span></span>

> <span data-ttu-id="f6801-129">Ta usługa hostowana na hello Azure Marketplace jest usługi OData; te można wywoływać za pomocą metody POST lub GET.</span><span class="sxs-lookup"><span data-stu-id="f6801-129">This service, as hosted on hello Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="f6801-130">Istnieje wiele sposobów używania usługi hello w zautomatyzowany sposób (przykładową aplikację jest [tutaj](http://microsoftazuremachinelearning.azurewebsites.net/ArimaForecasting.aspx)).</span><span class="sxs-lookup"><span data-stu-id="f6801-130">There are multiple ways of consuming hello service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/ArimaForecasting.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="f6801-131">Rozpoczynanie korzystania z usług sieci web kod C#:</span><span class="sxs-lookup"><span data-stu-id="f6801-131">Starting C# code for web service consumption:</span></span>
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

## <a name="creation-of-web-service"></a><span data-ttu-id="f6801-132">Tworzenie usługi sieci web</span><span class="sxs-lookup"><span data-stu-id="f6801-132">Creation of web service</span></span>
> <span data-ttu-id="f6801-133">Ta usługa sieci web został utworzony przy użyciu usługi Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="f6801-133">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="f6801-134">Bezpłatna wersja próbna, a także wprowadzające filmy wideo dotyczące tworzenia eksperymenty i [publikowania usług sieci web](machine-learning-publish-a-machine-learning-web-service.md), można znaleźć pod adresem [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="f6801-134">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="f6801-135">Poniżej przedstawiono zrzut ekranu hello eksperymentu, utworzona hello kod przykład i usługi sieci web dla każdego z modułów hello w ramach eksperymentu hello.</span><span class="sxs-lookup"><span data-stu-id="f6801-135">Below is a screenshot of hello experiment that created hello web service and example code for each of hello modules within hello experiment.</span></span>
> 
> 

<span data-ttu-id="f6801-136">Za pomocą w usłudze Azure Machine Learning nowy pusty eksperyment została utworzona.</span><span class="sxs-lookup"><span data-stu-id="f6801-136">From within Azure Machine Learning, a new blank experiment was created.</span></span> <span data-ttu-id="f6801-137">Przekazany ze schematem wstępnie zdefiniowanych danych przykładowych danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="f6801-137">Sample input data was uploaded with a predefined data schema.</span></span> <span data-ttu-id="f6801-138">Schemat danych połączonych toohello jest [wykonanie skryptu języka R] [ execute-r-script] moduł, który generuje modelu prognozowania można używać ARIMA hello przy użyciu funkcji 'auto.arima' i "przewidywanie" z R.</span><span class="sxs-lookup"><span data-stu-id="f6801-138">Linked toohello data schema is an [Execute R Script][execute-r-script] module, which generates hello ARIMA forecasting model by using ‘auto.arima’ and ‘forecast’ functions from R.</span></span> 

### <a name="experiment-flow"></a><span data-ttu-id="f6801-139">Przepływ eksperymentu:</span><span class="sxs-lookup"><span data-stu-id="f6801-139">Experiment flow:</span></span>
![Tworzenie obszaru roboczego][2]

#### <a name="module-1"></a><span data-ttu-id="f6801-141">Moduł 1:</span><span class="sxs-lookup"><span data-stu-id="f6801-141">Module 1:</span></span>
    # Add in hello CSV file with hello data in hello format shown below 
![Tworzenie obszaru roboczego][3]    

#### <a name="module-2"></a><span data-ttu-id="f6801-143">Moduł 2:</span><span class="sxs-lookup"><span data-stu-id="f6801-143">Module 2:</span></span>
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


## <a name="limitations"></a><span data-ttu-id="f6801-144">Ograniczenia</span><span class="sxs-lookup"><span data-stu-id="f6801-144">Limitations</span></span>
<span data-ttu-id="f6801-145">Jest bardzo prosty przykład prognozowania ARIMA.</span><span class="sxs-lookup"><span data-stu-id="f6801-145">This is a very simple example for ARIMA forecasting.</span></span> <span data-ttu-id="f6801-146">Jak wynika z powyższych hello przykładowy kod, nie błąd Przechwytywanie jest zaimplementowana, a usługa hello przyjęto założenie, że wszystkie zmienne hello są ciągłe/dodatnie wartości i częstotliwość hello musi być liczbą całkowitą większą niż 1.</span><span class="sxs-lookup"><span data-stu-id="f6801-146">As can be seen from hello example code above, no error catching is implemented, and hello service assumes that all hello variables are continuous/positive values and hello frequency should be an integer greater than 1.</span></span> <span data-ttu-id="f6801-147">Długość Hello wektorów hello wartość daty i powinien hello w tej samej.</span><span class="sxs-lookup"><span data-stu-id="f6801-147">hello length of hello date and value vectors should be hello same.</span></span> <span data-ttu-id="f6801-148">Zmienna daty Hello przestrzegać toohello format "mm/dd/rrrr'.</span><span class="sxs-lookup"><span data-stu-id="f6801-148">hello date variable should adhere toohello format ‘mm/dd/yyyy’.</span></span>

## <a name="faq"></a><span data-ttu-id="f6801-149">Często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="f6801-149">FAQ</span></span>
<span data-ttu-id="f6801-150">Często zadawane pytania dotyczące wykorzystania usługi sieci web hello lub toomarketplace publikowania, zobacz [tutaj](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="f6801-150">For frequently asked questions on consumption of hello web service or publishing toomarketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-arima/arima-img1.png
[2]: ./media/machine-learning-r-csharp-arima/arima-img2.png
[3]: ./media/machine-learning-r-csharp-arima/arima-img3.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

