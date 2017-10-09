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
# <a name="deprecated-web-services-examples-using-r-code-on-azure-machine-learning-and-published-toomicrosoft-azure-marketplace"></a>(przestarzałe) Przykłady przy użyciu kodu języka R w usłudze Azure Machine Learning i tooMicrosoft opublikowane w portalu Azure Marketplace usług sieci Web

> [!NOTE]
> Witaj Microsoft DataMarket została wycofana i te interfejsy API są przestarzałe. 
> 
> Możesz znaleźć wiele interfejsów API i przydatne przykład eksperymenty w hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com). Aby uzyskać więcej informacji na temat hello galerii, zobacz [udziału i odnajdywania zasobów w hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).

W tym artykule są przykład sieci web, usługi zostały utworzone przy użyciu usługi Azure Machine Learning i publikowane toohello portalu Azure Marketplace. Każdy przykład usługi sieci web zawiera kompleksowe dołączonym dokumentem, osadzanie przykładowych zestawów danych dla usługi hello testowania i wyjaśnia, jak hello użytkownik może tworzyć podobne usługi się. 

W usłudze Azure Machine Learning Studio użytkownicy mogą pisać kod języka R i za pomocą kilku kliknięć, należy opublikować go jako usługi sieci web dla aplikacji i urządzeń tooconsume wokół hello world. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Z Tworzenie prostego kalkulatory, zapewniające toocreating funkcji statystycznych, niestandardowe predykcyjne analizy wskaźniki nastrojów klientów wyszukiwania tekstu, zarówno nowe, jak i doświadczeni użytkownicy R mogą korzystać z łatwość hello, z którym użytkownicy usługi Azure Machine Learning operacjonalizować R Kod. Gdy te usługi sieci web może być używana przez użytkowników, potencjalnie za pomocą aplikacji mobilnej lub witryny sieci Web, cel hello te przykłady jest tooshow jak operacjonalizować uczenia maszynowego usługi sieci web R skrypty w celach analitycznych i toocreate używanych usług sieci web na w górnej części kodu języka R.

Każdy przykład zawiera przykład C# korzystania z usług sieci web.

![Diagram kodu języka R w usłudze Azure Machine Learning: R rozwiązań własnościowych użycia lub toohello opublikowane w portalu Azure Marketplace.][1]

Należy rozważyć następujące scenariusze hello.

## <a name="scenario-1-generic-model"></a>Scenariusz 1: Ogólny model
Użytkownik pracuje z ogólnym modelu, który może być danych zastosowanych tooa nowego użytkownika, takich jak podstawowe prognozowania czasu serii danych lub niestandardowej metody R z zaawansowana analityka. Ten użytkownik publikuje hello model jako usługę sieci web dla innych tooconsume z danymi.

* [Klasyfikator binarny](machine-learning-r-csharp-binary-classifier.md)
* [Model klastra](machine-learning-r-csharp-cluster-model.md)
* [Wieloczynnikowa regresja liniowa](machine-learning-r-csharp-multivariate-linear-regression.md)
* [Prognozowanie — wygładzanie wykładnicze](machine-learning-r-csharp-forecasting-exponential-smoothing.md)
* [ETS + prognozowania STL](machine-learning-r-csharp-retail-demand-forecasting.md)
* [Funkcja prognozowania - Autoregressive zintegrowane przeniesienie średniej (ARIMA)](machine-learning-r-csharp-arima.md)
* [Analiza przeżycia](machine-learning-r-csharp-survival-analysis.md)

## <a name="scenario-2-trained-model--specific-data"></a>Scenariusz 2: Uczonego modelu — określonych danych
Jeśli użytkownik ma dane, które zawiera przydatne prognoz przez kod języka R, takich jak duże przykładowe kwestionariusz charakteru w klastrze za pośrednictwem k średnich algorytmu toopredict hello charakteru typu użytkownika lub kondycji badanie danych, które mogą być używane toopredict danej osoby ryzyka dla raka płuc z pakietem analizy R przeżycia. Użytkownik Hello publikuje dane hello za pośrednictwem usługi sieci web, który prognozuje wyniku nowego użytkownika.

## <a name="scenario-3-trained-model--generic-data"></a>Scenariusz 3: Uczonego modelu — danych typu ogólnego
Użytkownik ma rodzajowy danych (na przykład Boże tekst), które umożliwia toobe usługi sieci web utworzony i objęty zastosowane na różnych urządzeniach przypadki użycia i scenariuszy.

* [Analiza tonacji na podstawie leksykonu](machine-learning-r-csharp-lexicon-based-sentiment-analysis.md)

## <a name="scenario-4-advanced-calculator"></a>Scenariusz 4: Kalkulator zaawansowane
Użytkownik udostępnia zaawansowane obliczeń lub symulacje, które nie wymagają żadnych uczonego modelu lub dopasowywania danych użytkownika toohello modelu.

* [Różnica w teście proporcji](machine-learning-r-csharp-difference-in-two-proportions.md)
* [Pakiet zwykłego rozkładu](machine-learning-r-csharp-normal-distribution.md)
* [Pakiet rozkładu dwumianowego](machine-learning-r-csharp-binomial-distribution.md)

## <a name="faq"></a>Często zadawane pytania
Często zadawane pytania dotyczące wykorzystania usługi sieci web hello lub toohello publikowania witryny Marketplace, zobacz [tutaj](machine-learning-marketplace-faq.md).

[1]: ./media/machine-learning-r-csharp-web-service-examples/machine-learning-r-code-options-for-using-and-sharing-cloud.png



