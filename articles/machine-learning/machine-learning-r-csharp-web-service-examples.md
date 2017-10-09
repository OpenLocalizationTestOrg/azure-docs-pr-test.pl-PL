---
title: "AAA(deprecated) Machine learning web services przykłady skompilowanej za pomocą R - Azure | Dokumentacja firmy Microsoft"
description: "(przestarzałe) Znajdź przydatny zestaw przykłady usługi sieci web utworzone za pomocą kodu języka R i uczenia maszynowego i opublikowane toohello portalu Azure Marketplace."
keywords: "CSharp, kod r przykłady usług sieci web"
services: machine-learning
documentationcenter: 
author: jaymathe
manager: jhubbard
editor: cgronlun
ms.assetid: 97d66cb7-6a84-4ae9-8095-0b5f5ba82d7f
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: jaymathe
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: 20b074d38e65aed907d40549bb61f124cb5dfe1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-web-services-examples-using-r-code-on-azure-machine-learning-and-published-toomicrosoft-azure-marketplace"></a><span data-ttu-id="8c4d6-104">(przestarzałe) Przykłady przy użyciu kodu języka R w usłudze Azure Machine Learning i tooMicrosoft opublikowane w portalu Azure Marketplace usług sieci Web</span><span class="sxs-lookup"><span data-stu-id="8c4d6-104">(deprecated) Web services examples using R code on Azure Machine Learning and published tooMicrosoft Azure Marketplace</span></span>

> [!NOTE]
> <span data-ttu-id="8c4d6-105">Witaj Microsoft DataMarket została wycofana i te interfejsy API są przestarzałe.</span><span class="sxs-lookup"><span data-stu-id="8c4d6-105">hello Microsoft DataMarket is being retired and these APIs have been deprecated.</span></span> 
> 
> <span data-ttu-id="8c4d6-106">Możesz znaleźć wiele interfejsów API i przydatne przykład eksperymenty w hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="8c4d6-106">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="8c4d6-107">Aby uzyskać więcej informacji na temat hello galerii, zobacz [udziału i odnajdywania zasobów w hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="8c4d6-107">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="8c4d6-108">W tym artykule są przykład sieci web, usługi zostały utworzone przy użyciu usługi Azure Machine Learning i publikowane toohello portalu Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="8c4d6-108">In this article are example web services were created using Azure Machine Learning and published toohello Azure Marketplace.</span></span> <span data-ttu-id="8c4d6-109">Każdy przykład usługi sieci web zawiera kompleksowe dołączonym dokumentem, osadzanie przykładowych zestawów danych dla usługi hello testowania i wyjaśnia, jak hello użytkownik może tworzyć podobne usługi się.</span><span class="sxs-lookup"><span data-stu-id="8c4d6-109">Each web service example has a comprehensive document attached, embedding sample data sets for testing hello services and explaining how hello user can create a similar service themselves.</span></span> 

<span data-ttu-id="8c4d6-110">W usłudze Azure Machine Learning Studio użytkownicy mogą pisać kod języka R i za pomocą kilku kliknięć, należy opublikować go jako usługi sieci web dla aplikacji i urządzeń tooconsume wokół hello world.</span><span class="sxs-lookup"><span data-stu-id="8c4d6-110">In Azure Machine Learning Studio, users can write R code and with a few clicks, publish it as a web service for applications and devices tooconsume around hello world.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="8c4d6-111">Z Tworzenie prostego kalkulatory, zapewniające toocreating funkcji statystycznych, niestandardowe predykcyjne analizy wskaźniki nastrojów klientów wyszukiwania tekstu, zarówno nowe, jak i doświadczeni użytkownicy R mogą korzystać z łatwość hello, z którym użytkownicy usługi Azure Machine Learning operacjonalizować R Kod.</span><span class="sxs-lookup"><span data-stu-id="8c4d6-111">From producing simple calculators that provide statistical functionality toocreating a custom text-mining sentiment analysis predictor, both new and experienced R users can benefit from hello ease with which users of Azure Machine Learning can operationalize R code.</span></span> <span data-ttu-id="8c4d6-112">Gdy te usługi sieci web może być używana przez użytkowników, potencjalnie za pomocą aplikacji mobilnej lub witryny sieci Web, cel hello te przykłady jest tooshow jak operacjonalizować uczenia maszynowego usługi sieci web R skrypty w celach analitycznych i toocreate używanych usług sieci web na w górnej części kodu języka R.</span><span class="sxs-lookup"><span data-stu-id="8c4d6-112">While these web services could be consumed by users, potentially through a mobile app or a website, hello purpose of these web services examples is tooshow how Machine Learning can operationalize R scripts for analytical purposes and be used toocreate web services on top of R code.</span></span>

<span data-ttu-id="8c4d6-113">Każdy przykład zawiera przykład C# korzystania z usług sieci web.</span><span class="sxs-lookup"><span data-stu-id="8c4d6-113">Each example includes a C# example for web service consumption.</span></span>

![Diagram kodu języka R w usłudze Azure Machine Learning: R rozwiązań własnościowych użycia lub toohello opublikowane w portalu Azure Marketplace.][1]

<span data-ttu-id="8c4d6-115">Należy rozważyć następujące scenariusze hello.</span><span class="sxs-lookup"><span data-stu-id="8c4d6-115">Consider hello following scenarios.</span></span>

## <a name="scenario-1-generic-model"></a><span data-ttu-id="8c4d6-116">Scenariusz 1: Ogólny model</span><span class="sxs-lookup"><span data-stu-id="8c4d6-116">Scenario 1: Generic model</span></span>
<span data-ttu-id="8c4d6-117">Użytkownik pracuje z ogólnym modelu, który może być danych zastosowanych tooa nowego użytkownika, takich jak podstawowe prognozowania czasu serii danych lub niestandardowej metody R z zaawansowana analityka.</span><span class="sxs-lookup"><span data-stu-id="8c4d6-117">A user works with a generic model that can be applied tooa new user’s data, such as a basic forecasting of time series data or a custom-built R method with advanced analytics.</span></span> <span data-ttu-id="8c4d6-118">Ten użytkownik publikuje hello model jako usługę sieci web dla innych tooconsume z danymi.</span><span class="sxs-lookup"><span data-stu-id="8c4d6-118">This user publishes hello model as a web service for others tooconsume with their data.</span></span>

* [<span data-ttu-id="8c4d6-119">Klasyfikator binarny</span><span class="sxs-lookup"><span data-stu-id="8c4d6-119">Binary Classifier</span></span>](machine-learning-r-csharp-binary-classifier.md)
* [<span data-ttu-id="8c4d6-120">Model klastra</span><span class="sxs-lookup"><span data-stu-id="8c4d6-120">Cluster Model</span></span>](machine-learning-r-csharp-cluster-model.md)
* [<span data-ttu-id="8c4d6-121">Wieloczynnikowa regresja liniowa</span><span class="sxs-lookup"><span data-stu-id="8c4d6-121">Multivariate Linear Regression</span></span>](machine-learning-r-csharp-multivariate-linear-regression.md)
* [<span data-ttu-id="8c4d6-122">Prognozowanie — wygładzanie wykładnicze</span><span class="sxs-lookup"><span data-stu-id="8c4d6-122">Forecasting - Exponential Smoothing</span></span>](machine-learning-r-csharp-forecasting-exponential-smoothing.md)
* [<span data-ttu-id="8c4d6-123">ETS + prognozowania STL</span><span class="sxs-lookup"><span data-stu-id="8c4d6-123">ETS + STL Forecasting</span></span>](machine-learning-r-csharp-retail-demand-forecasting.md)
* [<span data-ttu-id="8c4d6-124">Funkcja prognozowania - Autoregressive zintegrowane przeniesienie średniej (ARIMA)</span><span class="sxs-lookup"><span data-stu-id="8c4d6-124">Forecasting - Autoregressive Integrated Moving Average (ARIMA)</span></span>](machine-learning-r-csharp-arima.md)
* [<span data-ttu-id="8c4d6-125">Analiza przeżycia</span><span class="sxs-lookup"><span data-stu-id="8c4d6-125">Survival Analysis</span></span>](machine-learning-r-csharp-survival-analysis.md)

## <a name="scenario-2-trained-model--specific-data"></a><span data-ttu-id="8c4d6-126">Scenariusz 2: Uczonego modelu — określonych danych</span><span class="sxs-lookup"><span data-stu-id="8c4d6-126">Scenario 2: Trained model – specific data</span></span>
<span data-ttu-id="8c4d6-127">Jeśli użytkownik ma dane, które zawiera przydatne prognoz przez kod języka R, takich jak duże przykładowe kwestionariusz charakteru w klastrze za pośrednictwem k średnich algorytmu toopredict hello charakteru typu użytkownika lub kondycji badanie danych, które mogą być używane toopredict danej osoby ryzyka dla raka płuc z pakietem analizy R przeżycia.</span><span class="sxs-lookup"><span data-stu-id="8c4d6-127">A user has data that provides useful predictions through R code, such as a large sample of personality questionnaires clustered through a k-means algorithm toopredict hello user’s personality type, or health survey data that can be used toopredict an individual’s risk for lung cancer with a survival analysis R package.</span></span> <span data-ttu-id="8c4d6-128">Użytkownik Hello publikuje dane hello za pośrednictwem usługi sieci web, który prognozuje wyniku nowego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="8c4d6-128">hello user publishes hello data through a web service that predicts a new user’s outcome.</span></span>

## <a name="scenario-3-trained-model--generic-data"></a><span data-ttu-id="8c4d6-129">Scenariusz 3: Uczonego modelu — danych typu ogólnego</span><span class="sxs-lookup"><span data-stu-id="8c4d6-129">Scenario 3: Trained model – generic data</span></span>
<span data-ttu-id="8c4d6-130">Użytkownik ma rodzajowy danych (na przykład Boże tekst), które umożliwia toobe usługi sieci web utworzony i objęty zastosowane na różnych urządzeniach przypadki użycia i scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="8c4d6-130">A user has generic data (such as a text corpus) that allows a web service toobe built and applied generically across different types of use cases and scenarios.</span></span>

* [<span data-ttu-id="8c4d6-131">Analiza tonacji na podstawie leksykonu</span><span class="sxs-lookup"><span data-stu-id="8c4d6-131">Lexicon Based Sentiment Analysis</span></span>](machine-learning-r-csharp-lexicon-based-sentiment-analysis.md)

## <a name="scenario-4-advanced-calculator"></a><span data-ttu-id="8c4d6-132">Scenariusz 4: Kalkulator zaawansowane</span><span class="sxs-lookup"><span data-stu-id="8c4d6-132">Scenario 4: Advanced calculator</span></span>
<span data-ttu-id="8c4d6-133">Użytkownik udostępnia zaawansowane obliczeń lub symulacje, które nie wymagają żadnych uczonego modelu lub dopasowywania danych użytkownika toohello modelu.</span><span class="sxs-lookup"><span data-stu-id="8c4d6-133">A user provides advanced calculations or simulations that don’t require any trained model or fitting of a model toohello user’s data.</span></span>

* [<span data-ttu-id="8c4d6-134">Różnica w teście proporcji</span><span class="sxs-lookup"><span data-stu-id="8c4d6-134">Difference in Proportions Test</span></span>](machine-learning-r-csharp-difference-in-two-proportions.md)
* [<span data-ttu-id="8c4d6-135">Pakiet zwykłego rozkładu</span><span class="sxs-lookup"><span data-stu-id="8c4d6-135">Normal Distribution Suite</span></span>](machine-learning-r-csharp-normal-distribution.md)
* [<span data-ttu-id="8c4d6-136">Pakiet rozkładu dwumianowego</span><span class="sxs-lookup"><span data-stu-id="8c4d6-136">Binomial Distribution Suite</span></span>](machine-learning-r-csharp-binomial-distribution.md)

## <a name="faq"></a><span data-ttu-id="8c4d6-137">Często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="8c4d6-137">FAQ</span></span>
<span data-ttu-id="8c4d6-138">Często zadawane pytania dotyczące wykorzystania usługi sieci web hello lub toohello publikowania witryny Marketplace, zobacz [tutaj](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="8c4d6-138">For frequently asked questions on consumption of hello web service or publishing toohello Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-web-service-examples/machine-learning-r-code-options-for-using-and-sharing-cloud.png



