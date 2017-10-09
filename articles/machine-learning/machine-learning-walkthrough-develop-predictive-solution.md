---
title: "rozwiązanie predykcyjne aaaA do ryzyka kredytowego w usłudze Machine Learning | Dokumentacja firmy Microsoft"
description: "Szczegółowy przewodnik pokazujący sposób toocreate rozwiązania analizy predykcyjnej kredytu ocena ryzyka w usłudze Azure Machine Learning Studio."
keywords: "ryzyko kredytowe, rozwiązanie analizy predykcyjnej, ocena ryzyka"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 43300854-a14e-4cd2-9bb1-c55c779e0e93
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 00ed39081e6952b8d03b37a8285d8dc3ddff2cb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-develop-a-predictive-analytics-solution-for-credit-risk-assessment-in-azure-machine-learning"></a>Przewodnik: tworzenie rozwiązania analizy predykcyjnej w celu oceny ryzyka kredytowego w usłudze Azure Machine Learning

W tym przewodniku traktujemy rozszerzonej przyjrzeć hello procesu tworzenia rozwiązania analizy predykcyjnej w usłudze Machine Learning Studio. Firma Microsoft opracowywanie prostego modelu w usłudze Machine Learning Studio, a następnie wdrożyć go jako usługi sieci web Azure Machine Learning, gdzie hello modelu można przewidzieć przy użyciu nowych danych. 

W tym przewodniku przyjęto założenie, że co najmniej raz użyto wcześniej usługi Machine Learning Studio oraz że znasz niektóre pojęcia związane z uczeniem maszynowym. Nie zakładamy jednak, że jesteś ekspertem w którejkolwiek z tych dziedzin.

Jeśli nie znasz **Azure Machine Learning Studio** przed może być toostart z samouczka hello [Utwórz pierwszy połączenie analiz danych eksperymentu w usłudze Azure Machine Learning Studio](machine-learning-create-experiment.md). Ten samouczek przedstawia Machine Learning Studio na powitania po raz pierwszy. Przedstawia on hello podstawy modułów jak toodrag i upuść na eksperymentu, je połączyć ze sobą, uruchom eksperyment hello i przyjrzyj się hello wyników. Kolejnym narzędziem, które mogą być pomocne w ramach wprowadzenia jest diagram, który zawiera omówienie funkcji hello usługi Machine Learning Studio. Możesz go pobrać i wydrukować tutaj: [Diagram przeglądowy możliwości usługi Azure Machine Learning Studio](machine-learning-studio-overview-diagram.md).
 
Jeśli nowe pole toohello ogólnie uczenia maszynowego, brak seria filmów, które mogą okazać się przydatne tooyou. Jest to [nauki danych dla początkujących](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) go umożliwiają wprowadzenie dużą learning toomachine, przy użyciu języka codzienne oraz pojęcia.


[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]
 

## <a name="hello-problem"></a>Witaj problem

Załóżmy, że należy toopredict ryzyko kredytowe osoby na podstawie hello informacji przez ich nadać we wniosku kredytowym.  

Ocenia ryzyka kredytowego to złożony problem, ale ułatwimy ją nieco dzięki informacjom podanym w tym przewodniku. Użyjemy jej jako przykładu sposobu tworzenia rozwiązania do analizy predykcyjnej przy użyciu usługi Microsoft Azure Machine Learning. toodo, używamy Azure Machine Learning Studio i usługi sieci web usługi Machine Learning.  

## <a name="hello-solution"></a>Witaj rozwiązania

Pracę z tym szczegółowym przewodnikiem rozpoczniemy od publicznie dostępnych danych ryzyka kredytowego oraz utworzenia i uczenia modelu predykcyjnego na podstawie tych danych. Następnie możemy wdrożyć hello model jako usługę sieci web dzięki mogą być używane przez inne osoby oceny ryzyka kredytowego.

toocreate to rozwiązanie do oceny ryzyka kredytowej firma Microsoft, wykonaj następujące kroki:  

1. [Tworzenie obszaru roboczego usługi Machine Learning](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [Przekazywanie istniejących danych](machine-learning-walkthrough-2-upload-data.md)
3. [Tworzenie eksperymentu](machine-learning-walkthrough-3-create-new-experiment.md)
4. [Nauczanie i Ewaluacja modeli hello](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [Wdrażanie usługi sieci web hello](machine-learning-walkthrough-5-publish-web-service.md)
6. [Usługa sieci web hello dostępu](machine-learning-walkthrough-6-access-web-service.md)

> [!TIP] 
> Kopia robocza hello eksperymentu, która opracowywania można znaleźć w tym przewodniku w hello [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com). Przejdź za**[wskazówki - prognozowania ryzyko kredytowe](https://gallery.cortanaintelligence.com/Experiment/Walkthrough-Credit-risk-prediction-1)**  i kliknij przycisk **Otwórz w Studio** toodownload kopię eksperymentu hello do obszaru roboczego usługi Machine Learning Studio.
> 
> Ten przewodnik jest oparty na uproszczonej wersji hello przykładowych eksperymentów, [klasyfikacji binarnej: prognozowania ryzyko kredytowe](http://go.microsoft.com/fwlink/?LinkID=525270), są dostępne również w hello [galerii](http://gallery.cortanaintelligence.com/).
