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
# <a name="deprecated-web-services-examples-using-r-code-on-azure-machine-learning-and-published-to-microsoft-azure-marketplace"></a>(przestarzałe) Sieci Web usług przy użyciu kodu języka R w usłudze Azure Machine Learning przykłady i opublikowane w portalu Microsoft Azure Marketplace

> [!NOTE]
> Microsoft DataMarket została wycofana i te interfejsy API są przestarzałe. 
> 
> Możesz znaleźć wiele eksperymenty przykład przydatne i interfejsów API w [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com). Aby uzyskać więcej informacji o galerii, zobacz [udziału i odnajdywania zasobów w Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).

W tym artykule są przykład w sieci web usługi zostały utworzone przy użyciu usługi Azure Machine Learning i opublikowane w portalu Azure Marketplace. Każdy przykład usługi sieci web zawiera kompleksowe dołączonym dokumentem, osadzanie przykładowych zestawów danych do testowania usług i wyjaśniający, jak użytkownik może utworzyć podobne usługi się. 

W usłudze Azure Machine Learning Studio użytkownicy mogą pisać kod języka R i za pomocą kilku kliknięć, należy opublikować go jako usługi sieci web dla aplikacji i urządzeń korzystać z całego świata. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Z Tworzenie prostego kalkulatory, zapewniające statystyczne funkcjonalność do tworzenia niestandardowych predykcyjne analizy wskaźniki nastrojów klientów wyszukiwania tekstu, zarówno nowe, jak i doświadczeni użytkownicy R mogą korzystać z łatwość, z którym użytkownicy usługi Azure Machine Learning operacjonalizować R Kod. Te sieci web, które usługi może być używana przez użytkowników, potencjalnie za pomocą aplikacji mobilnej lub witryny sieci Web, przeznaczenia tych przykładów usług sieci web jest pokazanie, jak operacjonalizować uczenia maszynowego R skrypty w celach analitycznych i służyć do tworzenia usług sieci web na górze R kodu.

Każdy przykład zawiera przykład C# korzystania z usług sieci web.

![Diagram kodu języka R w usłudze Azure Machine Learning: R rozwiązania niezastrzeżonej użyć lub opublikowane w portalu Azure Marketplace.][1]

Należy rozważyć następujące scenariusze.

## <a name="scenario-1-generic-model"></a>Scenariusz 1: Ogólny model
Użytkownik pracuje z ogólnym modelu, który można zastosować do danych nowego użytkownika, takich jak podstawowe prognozowania czasu serii danych lub niestandardowej metody R z zaawansowana analityka. Ten użytkownik publikuje model jako usługę sieci web w taki sposób, aby inni użytkownicy mogli korzystać z danymi.

* [Klasyfikator binarny](machine-learning-r-csharp-binary-classifier.md)
* [Model klastra](machine-learning-r-csharp-cluster-model.md)
* [Wieloczynnikowa regresja liniowa](machine-learning-r-csharp-multivariate-linear-regression.md)
* [Prognozowanie — wygładzanie wykładnicze](machine-learning-r-csharp-forecasting-exponential-smoothing.md)
* [ETS + prognozowania STL](machine-learning-r-csharp-retail-demand-forecasting.md)
* [Funkcja prognozowania - Autoregressive zintegrowane przeniesienie średniej (ARIMA)](machine-learning-r-csharp-arima.md)
* [Analiza przeżycia](machine-learning-r-csharp-survival-analysis.md)

## <a name="scenario-2-trained-model--specific-data"></a>Scenariusz 2: Uczonego modelu — określonych danych
Jeśli użytkownik ma dane, które zawiera przydatne prognoz przez kod języka R, takie jak duża przykładowe kwestionariusz charakteru w klastrze za pomocą algorytmu k średnich do prognozowania charakteru typu użytkownika lub danych badania kondycji, który może służyć do prognozowania ryzyka poszczególnych dla raka płuc z pakietem analizy R przeżycia. Użytkownik publikuje dane za pośrednictwem usługi sieci web, który prognozuje wyniku nowego użytkownika.

## <a name="scenario-3-trained-model--generic-data"></a>Scenariusz 3: Uczonego modelu — danych typu ogólnego
Użytkownik ma rodzajowy danych (na przykład Boże tekst), które umożliwia usługi sieci web utworzony i objęty zastosowane na różnych urządzeniach przypadki użycia i scenariuszy.

* [Analiza tonacji na podstawie leksykonu](machine-learning-r-csharp-lexicon-based-sentiment-analysis.md)

## <a name="scenario-4-advanced-calculator"></a>Scenariusz 4: Kalkulator zaawansowane
Użytkownik udostępnia zaawansowane obliczeń lub symulacje, które nie wymagają żadnych uczonego modelu lub dopasowania modelu do danych użytkownika.

* [Różnica w teście proporcji](machine-learning-r-csharp-difference-in-two-proportions.md)
* [Pakiet zwykłego rozkładu](machine-learning-r-csharp-normal-distribution.md)
* [Pakiet rozkładu dwumianowego](machine-learning-r-csharp-binomial-distribution.md)

## <a name="faq"></a>Często zadawane pytania
Często zadawane pytania dotyczące wykorzystania usługi sieci web i publikowanie w portalu Marketplace, zobacz [tutaj](machine-learning-marketplace-faq.md).

[1]: ./media/machine-learning-r-csharp-web-service-examples/machine-learning-r-code-options-for-using-and-sharing-cloud.png



