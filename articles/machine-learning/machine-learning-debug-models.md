---
title: "aaaDebug modelu w usłudze Azure Machine Learning | Dokumentacja firmy Microsoft"
description: "Jak błędy toodebug utworzonego przez Train Model i Score Model moduły w usłudze Azure Machine Learning."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 629dc45e-ac1e-4b7d-b120-08813dc448be
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bradsev;garye
ms.openlocfilehash: ee38ca8ce38d4fc7add5ba70c80ab9bb2ceaf1d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="debug-your-model-in-azure-machine-learning"></a><span data-ttu-id="7eebb-103">Debugowanie modelu w usłudze Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="7eebb-103">Debug your Model in Azure Machine Learning</span></span>

<span data-ttu-id="7eebb-104">W tym artykule opisano potencjalnych przyczyn hello, dlaczego albo powitania po awarii dwóch węzłów może napotkać podczas uruchamiania modelu:</span><span class="sxs-lookup"><span data-stu-id="7eebb-104">This article explains hello potential reasons why either of hello following two failures might be encountered when running a model:</span></span>

* <span data-ttu-id="7eebb-105">Witaj [Train Model] [ train-model] moduł powoduje błąd</span><span class="sxs-lookup"><span data-stu-id="7eebb-105">hello [Train Model][train-model] module produces an error</span></span> 
* <span data-ttu-id="7eebb-106">Witaj [Score Model] [ score-model] modułu tworzy niepoprawnych wyników</span><span class="sxs-lookup"><span data-stu-id="7eebb-106">hello [Score Model][score-model] module produces incorrect results</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="train-model-module-produces-an-error"></a><span data-ttu-id="7eebb-107">Train Model moduł powoduje błąd</span><span class="sxs-lookup"><span data-stu-id="7eebb-107">Train Model Module produces an error</span></span>

![image1](./media/machine-learning-debug-models/train_model-1.png)

<span data-ttu-id="7eebb-109">Witaj [Train Model] [ train-model] modułu oczekuje dwóch parametrów wejściowych:</span><span class="sxs-lookup"><span data-stu-id="7eebb-109">hello [Train Model][train-model] Module expects two inputs:</span></span>

1. <span data-ttu-id="7eebb-110">Typ Hello modelu uczenia maszynowego z kolekcji hello modeli udostępniane przez usługi Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="7eebb-110">hello type of machine learning model from hello collection of models provided by Azure Machine Learning.</span></span>
2. <span data-ttu-id="7eebb-111">Witaj dane szkoleniowe z określonej kolumny etykiety, który określa hello toopredict zmiennej (hello innych kolumn są zakłada, że funkcje toobe).</span><span class="sxs-lookup"><span data-stu-id="7eebb-111">hello training data with a specified Label column which specifies hello variable toopredict (hello other columns are assumed toobe Features).</span></span>

<span data-ttu-id="7eebb-112">Ten moduł może utworzyć błędu w hello w następujących przypadkach:</span><span class="sxs-lookup"><span data-stu-id="7eebb-112">This module can produce an error in hello following cases:</span></span>

1. <span data-ttu-id="7eebb-113">Witaj etykiety kolumn została określona nieprawidłowo.</span><span class="sxs-lookup"><span data-stu-id="7eebb-113">hello Label column is specified incorrectly.</span></span> <span data-ttu-id="7eebb-114">Może to nastąpić, jeśli wybrano więcej niż jedną kolumnę jako hello etykiety lub wybrano nieprawidłowy indeks.</span><span class="sxs-lookup"><span data-stu-id="7eebb-114">This can happen if either more than one column is selected as hello Label or an incorrect column index is selected.</span></span> <span data-ttu-id="7eebb-115">Na przykład hello drugim przypadku będą miały zastosowania, jeśli indeks kolumny 30 jest używany z wejściowego zestawu danych, która zawiera tylko 25 kolumn.</span><span class="sxs-lookup"><span data-stu-id="7eebb-115">For example, hello second case would apply if a column index of 30 is used with an input dataset which has only 25 columns.</span></span>

2. <span data-ttu-id="7eebb-116">Witaj zestawu danych nie zawiera żadnych kolumn funkcji.</span><span class="sxs-lookup"><span data-stu-id="7eebb-116">hello dataset does not contain any Feature columns.</span></span> <span data-ttu-id="7eebb-117">Na przykład jeśli hello wejściowy zestaw danych zawiera tylko jedną kolumnę, która jest oznaczona jako kolumna etykiety hello, nie byłoby żadnych funkcji, z którym modelem hello toobuild.</span><span class="sxs-lookup"><span data-stu-id="7eebb-117">For example, if hello input dataset has only one column, which is marked as hello Label column, there would be no features with which toobuild hello model.</span></span> <span data-ttu-id="7eebb-118">W takim przypadku hello [Train Model] [ train-model] moduł powoduje błąd.</span><span class="sxs-lookup"><span data-stu-id="7eebb-118">In this case, hello [Train Model][train-model] module produces an error.</span></span>

3. <span data-ttu-id="7eebb-119">Hello wejściowy zestaw danych (funkcji lub etykiety) zawiera nieskończoności jako wartość.</span><span class="sxs-lookup"><span data-stu-id="7eebb-119">hello input dataset (Features or Label) contains Infinity as a value.</span></span>

## <a name="score-model-module-produces-incorrect-results"></a><span data-ttu-id="7eebb-120">Moduł score Model tworzy niepoprawnych wyników</span><span class="sxs-lookup"><span data-stu-id="7eebb-120">Score Model Module produces incorrect results</span></span>

![image2](./media/machine-learning-debug-models/train_test-2.png)

<span data-ttu-id="7eebb-122">W typowej szkolenia/testowania eksperyment do uczenia nadzorowanego, hello [podziału danych] [ split] modułu hello oryginalnego zestawu danych jest podzielony na dwie części: jednej strony jest używane tootrain hello modelu i używany jednej strony tooscore jak wykonuje hello trenowanego modelu.</span><span class="sxs-lookup"><span data-stu-id="7eebb-122">In a typical training/testing experiment for supervised learning, hello [Split Data][split] module divides hello original dataset into two parts: one part is used tootrain hello model and one part is used tooscore how well hello trained model performs.</span></span> <span data-ttu-id="7eebb-123">uczonego modelu Hello jest używane tooscore hello dane testowe, po którym hello wyniki są obliczane toodetermine dokładność hello hello modelu.</span><span class="sxs-lookup"><span data-stu-id="7eebb-123">hello trained model is then used tooscore hello test data, after which hello results are evaluated toodetermine hello accuracy of hello model.</span></span>

<span data-ttu-id="7eebb-124">Witaj [Score Model] [ score-model] moduł wymaga dwóch parametrów wejściowych:</span><span class="sxs-lookup"><span data-stu-id="7eebb-124">hello [Score Model][score-model] module requires two inputs:</span></span>

1. <span data-ttu-id="7eebb-125">Dane wyjściowe uczonego modelu hello [Train Model] [ train-model] modułu.</span><span class="sxs-lookup"><span data-stu-id="7eebb-125">A trained model output from hello [Train Model][train-model] module.</span></span>
2. <span data-ttu-id="7eebb-126">Oceniania zestawu danych, który różni się od zestawu danych hello używane tootrain hello modelu.</span><span class="sxs-lookup"><span data-stu-id="7eebb-126">A scoring dataset that is different from hello dataset used tootrain hello model.</span></span>

<span data-ttu-id="7eebb-127">Możliwe, że nawet jeśli eksperymentu hello zakończy się powodzeniem, hello tego [Score Model] [ score-model] modułu tworzy niepoprawnych wyników.</span><span class="sxs-lookup"><span data-stu-id="7eebb-127">It's possible that even though hello experiment succeeds, hello [Score Model][score-model] module produces incorrect results.</span></span> <span data-ttu-id="7eebb-128">Kilka scenariuszy może spowodować to toohappen:</span><span class="sxs-lookup"><span data-stu-id="7eebb-128">Several scenarios may cause this toohappen:</span></span>

1. <span data-ttu-id="7eebb-129">Jeśli hello określona etykieta jest podzielone na kategorie i model regresji jest uczony na powitania danych, nieprawidłowych danych wyjściowych może być realizowane przez hello [Score Model] [ score-model] modułu.</span><span class="sxs-lookup"><span data-stu-id="7eebb-129">If hello specified Label is categorical and a regression model is trained on hello data, an incorrect output would be produced by hello [Score Model][score-model] module.</span></span> <span data-ttu-id="7eebb-130">Jest to spowodowane regresji wymaga zmiennej ciągłego odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="7eebb-130">This is because regression requires a continuous response variable.</span></span> <span data-ttu-id="7eebb-131">W takim wypadku byłoby odpowiedniejsze toouse model klasyfikacji.</span><span class="sxs-lookup"><span data-stu-id="7eebb-131">In this case, it would be more suitable toouse a classification model.</span></span> 

2. <span data-ttu-id="7eebb-132">Podobnie jeśli model klasyfikacji jest uczony w zestawie danych o zmiennoprzecinkową liczby w kolumnie etykiety hello, może dać niepożądane wyniki.</span><span class="sxs-lookup"><span data-stu-id="7eebb-132">Similarly, if a classification model is trained on a dataset having floating point numbers in hello Label column, it may produce undesirable results.</span></span> <span data-ttu-id="7eebb-133">Jest to spowodowane klasyfikacji wymaga zmiennej odrębny odpowiedzi, która zezwala tylko wartości zakresu za pośrednictwem skończona i zwykle nieco mały zestaw klas.</span><span class="sxs-lookup"><span data-stu-id="7eebb-133">This is because classification requires a discrete response variable that only allows values that range over a finite, and usually somewhat small, set of classes.</span></span>

3. <span data-ttu-id="7eebb-134">Jeśli hello oceniania zestawu danych nie zawiera wszystkich hello funkcji używanych tootrain hello modelu, hello [Score Model] [ score-model] powoduje błąd.</span><span class="sxs-lookup"><span data-stu-id="7eebb-134">If hello scoring dataset does not contain all hello features used tootrain hello model, hello [Score Model][score-model] produces an error.</span></span>

4. <span data-ttu-id="7eebb-135">Jeśli wiersz w hello oceniania dataset zawiera brakujące wartości lub nieskończona wartość dla każdego z jego funkcji, hello [Score Model] [ score-model] nie utworzy odpowiedni wiersz toothat żadnych danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="7eebb-135">If a row in hello scoring dataset contains a missing value or an infinite value for any of its features, hello [Score Model][score-model] will not produce any output corresponding toothat row.</span></span>

5. <span data-ttu-id="7eebb-136">Witaj [Score Model] [ score-model] może tworzyć identyczne dane wyjściowe dla wszystkich wierszy hello oceniania zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="7eebb-136">hello [Score Model][score-model] may produce identical outputs for all rows in hello scoring dataset.</span></span> <span data-ttu-id="7eebb-137">To może wystąpić, na przykład podczas próby klasyfikacji za pomocą lasów decyzji, jeśli minimalna liczba próbek na węzeł liścia hello jest wybierany toobe ponad hello liczba dostępnych przykłady szkolenia.</span><span class="sxs-lookup"><span data-stu-id="7eebb-137">This could occur, for example, when attempting classification using Decision Forests if hello minimum number of samples per leaf node is chosen toobe more than hello number of training examples available.</span></span>

<!-- Module References -->
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/

