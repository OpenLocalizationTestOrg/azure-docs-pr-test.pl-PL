---
title: "(przestarzałe) Przykłady skompilowanej za pomocą R - Azure usługi Machine learning web | Dokumentacja firmy Microsoft"
description: "(przestarzałe) Znajdź przydatne zbiór sieci web usług przykłady utworzone za pomocą kodu języka R i uczenia maszynowego i opublikowane w portalu Azure Marketplace."
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
redirect_document_id: TRUE
ms.openlocfilehash: 9514025db6f812f9e7934ea2d1575e948d6585b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-web-services-examples-using-r-code-on-azure-machine-learning-and-published-to-microsoft-azure-marketplace"></a><span data-ttu-id="f7087-104">(przestarzałe) Sieci Web usług przy użyciu kodu języka R w usłudze Azure Machine Learning przykłady i opublikowane w portalu Microsoft Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="f7087-104">(deprecated) Web services examples using R code on Azure Machine Learning and published to Microsoft Azure Marketplace</span></span>

> [!NOTE]
> <span data-ttu-id="f7087-105">Microsoft DataMarket została wycofana i te interfejsy API są przestarzałe.</span><span class="sxs-lookup"><span data-stu-id="f7087-105">The Microsoft DataMarket is being retired and these APIs have been deprecated.</span></span> 
> 
> <span data-ttu-id="f7087-106">Możesz znaleźć wiele eksperymenty przykład przydatne i interfejsów API w [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="f7087-106">You can find many useful example experiments and APIs in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="f7087-107">Aby uzyskać więcej informacji o galerii, zobacz [udziału i odnajdywania zasobów w Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="f7087-107">For more information about the Gallery, see [Share and discover resources in the Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="f7087-108">W tym artykule są przykład w sieci web usługi zostały utworzone przy użyciu usługi Azure Machine Learning i opublikowane w portalu Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="f7087-108">In this article are example web services were created using Azure Machine Learning and published to the Azure Marketplace.</span></span> <span data-ttu-id="f7087-109">Każdy przykład usługi sieci web zawiera kompleksowe dołączonym dokumentem, osadzanie przykładowych zestawów danych do testowania usług i wyjaśniający, jak użytkownik może utworzyć podobne usługi się.</span><span class="sxs-lookup"><span data-stu-id="f7087-109">Each web service example has a comprehensive document attached, embedding sample data sets for testing the services and explaining how the user can create a similar service themselves.</span></span> 

<span data-ttu-id="f7087-110">W usłudze Azure Machine Learning Studio użytkownicy mogą pisać kod języka R i za pomocą kilku kliknięć, należy opublikować go jako usługi sieci web dla aplikacji i urządzeń korzystać z całego świata.</span><span class="sxs-lookup"><span data-stu-id="f7087-110">In Azure Machine Learning Studio, users can write R code and with a few clicks, publish it as a web service for applications and devices to consume around the world.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="f7087-111">Z Tworzenie prostego kalkulatory, zapewniające statystyczne funkcjonalność do tworzenia niestandardowych predykcyjne analizy wskaźniki nastrojów klientów wyszukiwania tekstu, zarówno nowe, jak i doświadczeni użytkownicy R mogą korzystać z łatwość, z którym użytkownicy usługi Azure Machine Learning operacjonalizować R Kod.</span><span class="sxs-lookup"><span data-stu-id="f7087-111">From producing simple calculators that provide statistical functionality to creating a custom text-mining sentiment analysis predictor, both new and experienced R users can benefit from the ease with which users of Azure Machine Learning can operationalize R code.</span></span> <span data-ttu-id="f7087-112">Te sieci web, które usługi może być używana przez użytkowników, potencjalnie za pomocą aplikacji mobilnej lub witryny sieci Web, przeznaczenia tych przykładów usług sieci web jest pokazanie, jak operacjonalizować uczenia maszynowego R skrypty w celach analitycznych i służyć do tworzenia usług sieci web na górze R kodu.</span><span class="sxs-lookup"><span data-stu-id="f7087-112">While these web services could be consumed by users, potentially through a mobile app or a website, the purpose of these web services examples is to show how Machine Learning can operationalize R scripts for analytical purposes and be used to create web services on top of R code.</span></span>

<span data-ttu-id="f7087-113">Każdy przykład zawiera przykład C# korzystania z usług sieci web.</span><span class="sxs-lookup"><span data-stu-id="f7087-113">Each example includes a C# example for web service consumption.</span></span>

![Diagram kodu języka R w usłudze Azure Machine Learning: R rozwiązania niezastrzeżonej użyć lub opublikowane w portalu Azure Marketplace.][1]

<span data-ttu-id="f7087-115">Należy rozważyć następujące scenariusze.</span><span class="sxs-lookup"><span data-stu-id="f7087-115">Consider the following scenarios.</span></span>

## <a name="scenario-1-generic-model"></a><span data-ttu-id="f7087-116">Scenariusz 1: Ogólny model</span><span class="sxs-lookup"><span data-stu-id="f7087-116">Scenario 1: Generic model</span></span>
<span data-ttu-id="f7087-117">Użytkownik pracuje z ogólnym modelu, który można zastosować do danych nowego użytkownika, takich jak podstawowe prognozowania czasu serii danych lub niestandardowej metody R z zaawansowana analityka.</span><span class="sxs-lookup"><span data-stu-id="f7087-117">A user works with a generic model that can be applied to a new user’s data, such as a basic forecasting of time series data or a custom-built R method with advanced analytics.</span></span> <span data-ttu-id="f7087-118">Ten użytkownik publikuje model jako usługę sieci web w taki sposób, aby inni użytkownicy mogli korzystać z danymi.</span><span class="sxs-lookup"><span data-stu-id="f7087-118">This user publishes the model as a web service for others to consume with their data.</span></span>

* [<span data-ttu-id="f7087-119">Klasyfikator binarny</span><span class="sxs-lookup"><span data-stu-id="f7087-119">Binary Classifier</span></span>](machine-learning-r-csharp-binary-classifier.md)
* [<span data-ttu-id="f7087-120">Model klastra</span><span class="sxs-lookup"><span data-stu-id="f7087-120">Cluster Model</span></span>](machine-learning-r-csharp-cluster-model.md)
* [<span data-ttu-id="f7087-121">Wieloczynnikowa regresja liniowa</span><span class="sxs-lookup"><span data-stu-id="f7087-121">Multivariate Linear Regression</span></span>](machine-learning-r-csharp-multivariate-linear-regression.md)
* [<span data-ttu-id="f7087-122">Prognozowanie — wygładzanie wykładnicze</span><span class="sxs-lookup"><span data-stu-id="f7087-122">Forecasting - Exponential Smoothing</span></span>](machine-learning-r-csharp-forecasting-exponential-smoothing.md)
* [<span data-ttu-id="f7087-123">ETS + prognozowania STL</span><span class="sxs-lookup"><span data-stu-id="f7087-123">ETS + STL Forecasting</span></span>](machine-learning-r-csharp-retail-demand-forecasting.md)
* [<span data-ttu-id="f7087-124">Funkcja prognozowania - Autoregressive zintegrowane przeniesienie średniej (ARIMA)</span><span class="sxs-lookup"><span data-stu-id="f7087-124">Forecasting - Autoregressive Integrated Moving Average (ARIMA)</span></span>](machine-learning-r-csharp-arima.md)
* [<span data-ttu-id="f7087-125">Analiza przeżycia</span><span class="sxs-lookup"><span data-stu-id="f7087-125">Survival Analysis</span></span>](machine-learning-r-csharp-survival-analysis.md)

## <a name="scenario-2-trained-model--specific-data"></a><span data-ttu-id="f7087-126">Scenariusz 2: Uczonego modelu — określonych danych</span><span class="sxs-lookup"><span data-stu-id="f7087-126">Scenario 2: Trained model – specific data</span></span>
<span data-ttu-id="f7087-127">Jeśli użytkownik ma dane, które zawiera przydatne prognoz przez kod języka R, takie jak duża przykładowe kwestionariusz charakteru w klastrze za pomocą algorytmu k średnich do prognozowania charakteru typu użytkownika lub danych badania kondycji, który może służyć do prognozowania ryzyka poszczególnych dla raka płuc z pakietem analizy R przeżycia.</span><span class="sxs-lookup"><span data-stu-id="f7087-127">A user has data that provides useful predictions through R code, such as a large sample of personality questionnaires clustered through a k-means algorithm to predict the user’s personality type, or health survey data that can be used to predict an individual’s risk for lung cancer with a survival analysis R package.</span></span> <span data-ttu-id="f7087-128">Użytkownik publikuje dane za pośrednictwem usługi sieci web, który prognozuje wyniku nowego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="f7087-128">The user publishes the data through a web service that predicts a new user’s outcome.</span></span>

## <a name="scenario-3-trained-model--generic-data"></a><span data-ttu-id="f7087-129">Scenariusz 3: Uczonego modelu — danych typu ogólnego</span><span class="sxs-lookup"><span data-stu-id="f7087-129">Scenario 3: Trained model – generic data</span></span>
<span data-ttu-id="f7087-130">Użytkownik ma rodzajowy danych (na przykład Boże tekst), które umożliwia usługi sieci web utworzony i objęty zastosowane na różnych urządzeniach przypadki użycia i scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="f7087-130">A user has generic data (such as a text corpus) that allows a web service to be built and applied generically across different types of use cases and scenarios.</span></span>

* [<span data-ttu-id="f7087-131">Analiza tonacji na podstawie leksykonu</span><span class="sxs-lookup"><span data-stu-id="f7087-131">Lexicon Based Sentiment Analysis</span></span>](machine-learning-r-csharp-lexicon-based-sentiment-analysis.md)

## <a name="scenario-4-advanced-calculator"></a><span data-ttu-id="f7087-132">Scenariusz 4: Kalkulator zaawansowane</span><span class="sxs-lookup"><span data-stu-id="f7087-132">Scenario 4: Advanced calculator</span></span>
<span data-ttu-id="f7087-133">Użytkownik udostępnia zaawansowane obliczeń lub symulacje, które nie wymagają żadnych uczonego modelu lub dopasowania modelu do danych użytkownika.</span><span class="sxs-lookup"><span data-stu-id="f7087-133">A user provides advanced calculations or simulations that don’t require any trained model or fitting of a model to the user’s data.</span></span>

* [<span data-ttu-id="f7087-134">Różnica w teście proporcji</span><span class="sxs-lookup"><span data-stu-id="f7087-134">Difference in Proportions Test</span></span>](machine-learning-r-csharp-difference-in-two-proportions.md)
* [<span data-ttu-id="f7087-135">Pakiet zwykłego rozkładu</span><span class="sxs-lookup"><span data-stu-id="f7087-135">Normal Distribution Suite</span></span>](machine-learning-r-csharp-normal-distribution.md)
* [<span data-ttu-id="f7087-136">Pakiet rozkładu dwumianowego</span><span class="sxs-lookup"><span data-stu-id="f7087-136">Binomial Distribution Suite</span></span>](machine-learning-r-csharp-binomial-distribution.md)

## <a name="faq"></a><span data-ttu-id="f7087-137">Często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="f7087-137">FAQ</span></span>
<span data-ttu-id="f7087-138">Często zadawane pytania dotyczące wykorzystania usługi sieci web i publikowanie w portalu Marketplace, zobacz [tutaj](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="f7087-138">For frequently asked questions on consumption of the web service or publishing to the Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-web-service-examples/machine-learning-r-code-options-for-using-and-sharing-cloud.png



