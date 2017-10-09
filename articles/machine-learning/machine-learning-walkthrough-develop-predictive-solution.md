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
# <a name="walkthrough-develop-a-predictive-analytics-solution-for-credit-risk-assessment-in-azure-machine-learning"></a><span data-ttu-id="8795a-104">Przewodnik: tworzenie rozwiązania analizy predykcyjnej w celu oceny ryzyka kredytowego w usłudze Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="8795a-104">Walkthrough: Develop a predictive analytics solution for credit risk assessment in Azure Machine Learning</span></span>

<span data-ttu-id="8795a-105">W tym przewodniku traktujemy rozszerzonej przyjrzeć hello procesu tworzenia rozwiązania analizy predykcyjnej w usłudze Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="8795a-105">In this walkthrough, we take an extended look at hello process of developing a predictive analytics solution in Machine Learning Studio.</span></span> <span data-ttu-id="8795a-106">Firma Microsoft opracowywanie prostego modelu w usłudze Machine Learning Studio, a następnie wdrożyć go jako usługi sieci web Azure Machine Learning, gdzie hello modelu można przewidzieć przy użyciu nowych danych.</span><span class="sxs-lookup"><span data-stu-id="8795a-106">We develop a simple model in Machine Learning Studio, and then deploy it as an Azure Machine Learning web service where hello model can make predictions using new data.</span></span> 

<span data-ttu-id="8795a-107">W tym przewodniku przyjęto założenie, że co najmniej raz użyto wcześniej usługi Machine Learning Studio oraz że znasz niektóre pojęcia związane z uczeniem maszynowym.</span><span class="sxs-lookup"><span data-stu-id="8795a-107">This walkthrough assumes that you've used Machine Learning Studio at least once before, and that you have some understanding of machine learning concepts.</span></span> <span data-ttu-id="8795a-108">Nie zakładamy jednak, że jesteś ekspertem w którejkolwiek z tych dziedzin.</span><span class="sxs-lookup"><span data-stu-id="8795a-108">But it doesn't assume you're an expert in either.</span></span>

<span data-ttu-id="8795a-109">Jeśli nie znasz **Azure Machine Learning Studio** przed może być toostart z samouczka hello [Utwórz pierwszy połączenie analiz danych eksperymentu w usłudze Azure Machine Learning Studio](machine-learning-create-experiment.md).</span><span class="sxs-lookup"><span data-stu-id="8795a-109">If you've never used **Azure Machine Learning Studio** before, you might want toostart with hello tutorial, [Create your first data science experiment in Azure Machine Learning Studio](machine-learning-create-experiment.md).</span></span> <span data-ttu-id="8795a-110">Ten samouczek przedstawia Machine Learning Studio na powitania po raz pierwszy.</span><span class="sxs-lookup"><span data-stu-id="8795a-110">That tutorial takes you through Machine Learning Studio for hello first time.</span></span> <span data-ttu-id="8795a-111">Przedstawia on hello podstawy modułów jak toodrag i upuść na eksperymentu, je połączyć ze sobą, uruchom eksperyment hello i przyjrzyj się hello wyników.</span><span class="sxs-lookup"><span data-stu-id="8795a-111">It shows you hello basics of how toodrag-and-drop modules onto your experiment, connect them together, run hello experiment, and look at hello results.</span></span> <span data-ttu-id="8795a-112">Kolejnym narzędziem, które mogą być pomocne w ramach wprowadzenia jest diagram, który zawiera omówienie funkcji hello usługi Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="8795a-112">Another tool that may be helpful for getting started is a diagram that gives an overview of hello capabilities of Machine Learning Studio.</span></span> <span data-ttu-id="8795a-113">Możesz go pobrać i wydrukować tutaj: [Diagram przeglądowy możliwości usługi Azure Machine Learning Studio](machine-learning-studio-overview-diagram.md).</span><span class="sxs-lookup"><span data-stu-id="8795a-113">You can download and print it from here: [Overview diagram of Azure Machine Learning Studio capabilities](machine-learning-studio-overview-diagram.md).</span></span>
 
<span data-ttu-id="8795a-114">Jeśli nowe pole toohello ogólnie uczenia maszynowego, brak seria filmów, które mogą okazać się przydatne tooyou.</span><span class="sxs-lookup"><span data-stu-id="8795a-114">If you're new toohello field of machine learning in general, there's a video series that might be helpful tooyou.</span></span> <span data-ttu-id="8795a-115">Jest to [nauki danych dla początkujących](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) go umożliwiają wprowadzenie dużą learning toomachine, przy użyciu języka codzienne oraz pojęcia.</span><span class="sxs-lookup"><span data-stu-id="8795a-115">It's called [Data Science for Beginners](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) and it can give you a great introduction toomachine learning using everyday language and concepts.</span></span>


[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]
 

## <a name="hello-problem"></a><span data-ttu-id="8795a-116">Witaj problem</span><span class="sxs-lookup"><span data-stu-id="8795a-116">hello problem</span></span>

<span data-ttu-id="8795a-117">Załóżmy, że należy toopredict ryzyko kredytowe osoby na podstawie hello informacji przez ich nadać we wniosku kredytowym.</span><span class="sxs-lookup"><span data-stu-id="8795a-117">Suppose you need toopredict an individual's credit risk based on hello information they gave on a credit application.</span></span>  

<span data-ttu-id="8795a-118">Ocenia ryzyka kredytowego to złożony problem, ale ułatwimy ją nieco dzięki informacjom podanym w tym przewodniku.</span><span class="sxs-lookup"><span data-stu-id="8795a-118">Credit risk assessment is a complex problem, but we can simplify it a bit for this walkthrough.</span></span> <span data-ttu-id="8795a-119">Użyjemy jej jako przykładu sposobu tworzenia rozwiązania do analizy predykcyjnej przy użyciu usługi Microsoft Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="8795a-119">We'll use it as an example of how you can create a predictive analytics solution using Microsoft Azure Machine Learning.</span></span> <span data-ttu-id="8795a-120">toodo, używamy Azure Machine Learning Studio i usługi sieci web usługi Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="8795a-120">toodo this, we use Azure Machine Learning Studio and a Machine Learning web service.</span></span>  

## <a name="hello-solution"></a><span data-ttu-id="8795a-121">Witaj rozwiązania</span><span class="sxs-lookup"><span data-stu-id="8795a-121">hello solution</span></span>

<span data-ttu-id="8795a-122">Pracę z tym szczegółowym przewodnikiem rozpoczniemy od publicznie dostępnych danych ryzyka kredytowego oraz utworzenia i uczenia modelu predykcyjnego na podstawie tych danych.</span><span class="sxs-lookup"><span data-stu-id="8795a-122">In this detailed walkthrough, we start with publicly available credit risk data and develop and train a predictive model based on that data.</span></span> <span data-ttu-id="8795a-123">Następnie możemy wdrożyć hello model jako usługę sieci web dzięki mogą być używane przez inne osoby oceny ryzyka kredytowego.</span><span class="sxs-lookup"><span data-stu-id="8795a-123">Then we deploy hello model as a web service so it can be used by others for credit risk assessment.</span></span>

<span data-ttu-id="8795a-124">toocreate to rozwiązanie do oceny ryzyka kredytowej firma Microsoft, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="8795a-124">toocreate this credit risk assessment solution, we follow these steps:</span></span>  

1. [<span data-ttu-id="8795a-125">Tworzenie obszaru roboczego usługi Machine Learning</span><span class="sxs-lookup"><span data-stu-id="8795a-125">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="8795a-126">Przekazywanie istniejących danych</span><span class="sxs-lookup"><span data-stu-id="8795a-126">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="8795a-127">Tworzenie eksperymentu</span><span class="sxs-lookup"><span data-stu-id="8795a-127">Create an experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="8795a-128">Nauczanie i Ewaluacja modeli hello</span><span class="sxs-lookup"><span data-stu-id="8795a-128">Train and evaluate hello models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="8795a-129">Wdrażanie usługi sieci web hello</span><span class="sxs-lookup"><span data-stu-id="8795a-129">Deploy hello web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="8795a-130">Usługa sieci web hello dostępu</span><span class="sxs-lookup"><span data-stu-id="8795a-130">Access hello web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

> [!TIP] 
> <span data-ttu-id="8795a-131">Kopia robocza hello eksperymentu, która opracowywania można znaleźć w tym przewodniku w hello [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="8795a-131">You can find a working copy of hello experiment that we develop in this walkthrough in hello [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="8795a-132">Przejdź za**[wskazówki - prognozowania ryzyko kredytowe](https://gallery.cortanaintelligence.com/Experiment/Walkthrough-Credit-risk-prediction-1)**  i kliknij przycisk **Otwórz w Studio** toodownload kopię eksperymentu hello do obszaru roboczego usługi Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="8795a-132">Go too**[Walkthrough - Credit risk prediction](https://gallery.cortanaintelligence.com/Experiment/Walkthrough-Credit-risk-prediction-1)** and click **Open in Studio** toodownload a copy of hello experiment into your Machine Learning Studio workspace.</span></span>
> 
> <span data-ttu-id="8795a-133">Ten przewodnik jest oparty na uproszczonej wersji hello przykładowych eksperymentów, [klasyfikacji binarnej: prognozowania ryzyko kredytowe](http://go.microsoft.com/fwlink/?LinkID=525270), są dostępne również w hello [galerii](http://gallery.cortanaintelligence.com/).</span><span class="sxs-lookup"><span data-stu-id="8795a-133">This walkthrough is based on a simplified version of hello sample experiment, [Binary Classification: Credit risk prediction](http://go.microsoft.com/fwlink/?LinkID=525270), also available in hello [Gallery](http://gallery.cortanaintelligence.com/).</span></span>
