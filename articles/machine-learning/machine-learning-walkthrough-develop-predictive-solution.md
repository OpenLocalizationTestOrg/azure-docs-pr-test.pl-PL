---
title: "Rozwiązanie predykcyjne do oceny ryzyka kredytowego w usłudze Machine Learning | Microsoft Docs"
description: "Szczegółowy przewodnik pokazujący sposób tworzenia rozwiązania analizy predykcyjnej w celu oceny ryzyka kredytowego w usłudze Azure Machine Learning Studio."
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
ms.openlocfilehash: e1af999b2fde8ffa2a0ffd1b88230f0aaab32b37
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="walkthrough-develop-a-predictive-analytics-solution-for-credit-risk-assessment-in-azure-machine-learning"></a><span data-ttu-id="4b000-104">Przewodnik: tworzenie rozwiązania analizy predykcyjnej w celu oceny ryzyka kredytowego w usłudze Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="4b000-104">Walkthrough: Develop a predictive analytics solution for credit risk assessment in Azure Machine Learning</span></span>

<span data-ttu-id="4b000-105">W tym przewodniku przedstawiono szczegółowo proces opracowywania rozwiązania do analizy predykcyjnej w usłudze Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="4b000-105">In this walkthrough, we take an extended look at the process of developing a predictive analytics solution in Machine Learning Studio.</span></span> <span data-ttu-id="4b000-106">Opracowaliśmy prosty model w usłudze Machine Learning Studio, a następnie wdrożyliśmy go w postaci usługi sieci Web Azure Machine Learning, w której model może tworzyć prognozy przy użyciu nowych danych.</span><span class="sxs-lookup"><span data-stu-id="4b000-106">We develop a simple model in Machine Learning Studio, and then deploy it as an Azure Machine Learning web service where the model can make predictions using new data.</span></span> 

<span data-ttu-id="4b000-107">W tym przewodniku przyjęto założenie, że co najmniej raz użyto wcześniej usługi Machine Learning Studio oraz że znasz niektóre pojęcia związane z uczeniem maszynowym.</span><span class="sxs-lookup"><span data-stu-id="4b000-107">This walkthrough assumes that you've used Machine Learning Studio at least once before, and that you have some understanding of machine learning concepts.</span></span> <span data-ttu-id="4b000-108">Nie zakładamy jednak, że jesteś ekspertem w którejkolwiek z tych dziedzin.</span><span class="sxs-lookup"><span data-stu-id="4b000-108">But it doesn't assume you're an expert in either.</span></span>

<span data-ttu-id="4b000-109">Jeśli nigdy wcześniej nie używano usługi **Azure Machine Learning Studio**, możesz najpierw skorzystać z samouczka [Tworzenie pierwszego eksperymentu dotyczącego przetwarzania danych w usłudze Azure Machine Learning Studio](machine-learning-create-experiment.md).</span><span class="sxs-lookup"><span data-stu-id="4b000-109">If you've never used **Azure Machine Learning Studio** before, you might want to start with the tutorial, [Create your first data science experiment in Azure Machine Learning Studio](machine-learning-create-experiment.md).</span></span> <span data-ttu-id="4b000-110">Ten samouczek przedstawia pracę z usługą Machine Learning Studio po raz pierwszy.</span><span class="sxs-lookup"><span data-stu-id="4b000-110">That tutorial takes you through Machine Learning Studio for the first time.</span></span> <span data-ttu-id="4b000-111">Podstawowe informacje przedstawione w tym samouczku obejmują przeciąganie modułów i upuszczanie ich w obszarze eksperymentu, łączenie modułów ze sobą, uruchamianie eksperymentu oraz przeglądanie wyników.</span><span class="sxs-lookup"><span data-stu-id="4b000-111">It shows you the basics of how to drag-and-drop modules onto your experiment, connect them together, run the experiment, and look at the results.</span></span> <span data-ttu-id="4b000-112">Inne narzędzie, które może być pomocne przy rozpoczynaniu pracy, to diagram zawierający omówienie możliwości usługi Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="4b000-112">Another tool that may be helpful for getting started is a diagram that gives an overview of the capabilities of Machine Learning Studio.</span></span> <span data-ttu-id="4b000-113">Możesz go pobrać i wydrukować tutaj: [Diagram przeglądowy możliwości usługi Azure Machine Learning Studio](machine-learning-studio-overview-diagram.md).</span><span class="sxs-lookup"><span data-stu-id="4b000-113">You can download and print it from here: [Overview diagram of Azure Machine Learning Studio capabilities](machine-learning-studio-overview-diagram.md).</span></span>
 
<span data-ttu-id="4b000-114">Jeśli uczenie maszynowe to dla Ciebie nowość, możesz skorzystać z serii pomocnych filmów wideo.</span><span class="sxs-lookup"><span data-stu-id="4b000-114">If you're new to the field of machine learning in general, there's a video series that might be helpful to you.</span></span> <span data-ttu-id="4b000-115">Jest ona zatytułowana [Data Science for Beginners](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) (Analiza danych dla początkujących) i oferuje znakomite wprowadzenie do uczenia maszynowego przedstawione przy użyciu codziennego języka i pojęć.</span><span class="sxs-lookup"><span data-stu-id="4b000-115">It's called [Data Science for Beginners](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) and it can give you a great introduction to machine learning using everyday language and concepts.</span></span>


[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]
 

## <a name="the-problem"></a><span data-ttu-id="4b000-116">Problem</span><span class="sxs-lookup"><span data-stu-id="4b000-116">The problem</span></span>

<span data-ttu-id="4b000-117">Załóżmy, że chcesz przewidzieć ryzyko kredytowe osoby na podstawie informacji przekazanych we wniosku kredytowym.</span><span class="sxs-lookup"><span data-stu-id="4b000-117">Suppose you need to predict an individual's credit risk based on the information they gave on a credit application.</span></span>  

<span data-ttu-id="4b000-118">Ocenia ryzyka kredytowego to złożony problem, ale ułatwimy ją nieco dzięki informacjom podanym w tym przewodniku.</span><span class="sxs-lookup"><span data-stu-id="4b000-118">Credit risk assessment is a complex problem, but we can simplify it a bit for this walkthrough.</span></span> <span data-ttu-id="4b000-119">Użyjemy jej jako przykładu sposobu tworzenia rozwiązania do analizy predykcyjnej przy użyciu usługi Microsoft Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="4b000-119">We'll use it as an example of how you can create a predictive analytics solution using Microsoft Azure Machine Learning.</span></span> <span data-ttu-id="4b000-120">W tym celu skorzystamy z usługi Azure Machine Learning Studio i usługi sieci Web Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="4b000-120">To do this, we use Azure Machine Learning Studio and a Machine Learning web service.</span></span>  

## <a name="the-solution"></a><span data-ttu-id="4b000-121">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="4b000-121">The solution</span></span>

<span data-ttu-id="4b000-122">Pracę z tym szczegółowym przewodnikiem rozpoczniemy od publicznie dostępnych danych ryzyka kredytowego oraz utworzenia i uczenia modelu predykcyjnego na podstawie tych danych.</span><span class="sxs-lookup"><span data-stu-id="4b000-122">In this detailed walkthrough, we start with publicly available credit risk data and develop and train a predictive model based on that data.</span></span> <span data-ttu-id="4b000-123">Następnie wdrożymy model jako usługę sieci Web, aby inne osoby mogły jej używać do oceny ryzyka kredytowego.</span><span class="sxs-lookup"><span data-stu-id="4b000-123">Then we deploy the model as a web service so it can be used by others for credit risk assessment.</span></span>

<span data-ttu-id="4b000-124">Aby utworzyć to rozwiązanie do oceny ryzyka kredytowego, wykonamy następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="4b000-124">To create this credit risk assessment solution, we follow these steps:</span></span>  

1. [<span data-ttu-id="4b000-125">Tworzenie obszaru roboczego usługi Machine Learning</span><span class="sxs-lookup"><span data-stu-id="4b000-125">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="4b000-126">Przekazywanie istniejących danych</span><span class="sxs-lookup"><span data-stu-id="4b000-126">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="4b000-127">Tworzenie eksperymentu</span><span class="sxs-lookup"><span data-stu-id="4b000-127">Create an experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="4b000-128">Nauczanie i ocena modeli</span><span class="sxs-lookup"><span data-stu-id="4b000-128">Train and evaluate the models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="4b000-129">Wdrażanie usługi sieci Web</span><span class="sxs-lookup"><span data-stu-id="4b000-129">Deploy the web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="4b000-130">Uzyskiwanie dostępu do usługi sieci Web</span><span class="sxs-lookup"><span data-stu-id="4b000-130">Access the web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

> [!TIP] 
> <span data-ttu-id="4b000-131">Funkcjonalną kopię eksperymentu opracowywanego w tym przewodniku można znaleźć w witrynie [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="4b000-131">You can find a working copy of the experiment that we develop in this walkthrough in the [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="4b000-132">Otwórz stronę **[Walkthrough — Credit risk prediction](https://gallery.cortanaintelligence.com/Experiment/Walkthrough-Credit-risk-prediction-1)** (Przewodnik — przewidywanie ryzyka kredytowego) i kliknij przycisk **Open in Studio** (Otwórz w usłudze Studio), aby pobrać kopię eksperymentu do obszaru roboczego usługi Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="4b000-132">Go to **[Walkthrough - Credit risk prediction](https://gallery.cortanaintelligence.com/Experiment/Walkthrough-Credit-risk-prediction-1)** and click **Open in Studio** to download a copy of the experiment into your Machine Learning Studio workspace.</span></span>
> 
> <span data-ttu-id="4b000-133">Ten przewodnik jest oparty na uproszczonej wersji przykładowego eksperymentu [Binary Classification: Credit risk prediction](http://go.microsoft.com/fwlink/?LinkID=525270) (Klasyfikacja binarna: przewidywanie ryzyka kredytowego) dostępnego również w witrynie [Gallery](http://gallery.cortanaintelligence.com/).</span><span class="sxs-lookup"><span data-stu-id="4b000-133">This walkthrough is based on a simplified version of the sample experiment, [Binary Classification: Credit risk prediction](http://go.microsoft.com/fwlink/?LinkID=525270), also available in the [Gallery](http://gallery.cortanaintelligence.com/).</span></span>
