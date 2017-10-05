---
title: Debugowanie modelu w Azure Machine Learning | Dokumentacja firmy Microsoft
description: "Jak można debugować błędy wygenerowane przez moduły Train Model i Score Model w usłudze Azure Machine Learning."
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
ms.openlocfilehash: d4cc94a6395ea45bccf65d9a9f3118ec98cb258d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="debug-your-model-in-azure-machine-learning"></a><span data-ttu-id="441a1-103">Debugowanie modelu w usłudze Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="441a1-103">Debug your Model in Azure Machine Learning</span></span>

<span data-ttu-id="441a1-104">W tym artykule opisano potencjalnych przyczyn, dlaczego jedną z następujących awarii dwóch węzłów może napotkać podczas uruchamiania modelu:</span><span class="sxs-lookup"><span data-stu-id="441a1-104">This article explains the potential reasons why either of the following two failures might be encountered when running a model:</span></span>

* <span data-ttu-id="441a1-105">[Train Model] [ train-model] moduł powoduje błąd</span><span class="sxs-lookup"><span data-stu-id="441a1-105">the [Train Model][train-model] module produces an error</span></span> 
* <span data-ttu-id="441a1-106">[Score Model] [ score-model] modułu tworzy niepoprawnych wyników</span><span class="sxs-lookup"><span data-stu-id="441a1-106">the [Score Model][score-model] module produces incorrect results</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="train-model-module-produces-an-error"></a><span data-ttu-id="441a1-107">Train Model moduł powoduje błąd</span><span class="sxs-lookup"><span data-stu-id="441a1-107">Train Model Module produces an error</span></span>

![image1](./media/machine-learning-debug-models/train_model-1.png)

<span data-ttu-id="441a1-109">[Train Model] [ train-model] modułu oczekuje dwóch parametrów wejściowych:</span><span class="sxs-lookup"><span data-stu-id="441a1-109">The [Train Model][train-model] Module expects two inputs:</span></span>

1. <span data-ttu-id="441a1-110">Typ modelu uczenia maszynowego z kolekcji modeli udostępniane przez usługi Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="441a1-110">The type of machine learning model from the collection of models provided by Azure Machine Learning.</span></span>
2. <span data-ttu-id="441a1-111">Dane szkoleniowe z określonej kolumny etykiety, który określa zmienną do prognozowania (innych kolumn są rozpatrywane funkcji).</span><span class="sxs-lookup"><span data-stu-id="441a1-111">The training data with a specified Label column which specifies the variable to predict (the other columns are assumed to be Features).</span></span>

<span data-ttu-id="441a1-112">Ten moduł może utworzyć wystąpił błąd w następujących przypadkach:</span><span class="sxs-lookup"><span data-stu-id="441a1-112">This module can produce an error in the following cases:</span></span>

1. <span data-ttu-id="441a1-113">Kolumna etykiety została określona nieprawidłowo.</span><span class="sxs-lookup"><span data-stu-id="441a1-113">The Label column is specified incorrectly.</span></span> <span data-ttu-id="441a1-114">Może to nastąpić, jeśli wybrano więcej niż jednej kolumny jako etykietę lub wybrano nieprawidłowy indeks.</span><span class="sxs-lookup"><span data-stu-id="441a1-114">This can happen if either more than one column is selected as the Label or an incorrect column index is selected.</span></span> <span data-ttu-id="441a1-115">Na przykład drugim przypadku będą miały zastosowania, jeśli indeks kolumny 30 jest używany z wejściowego zestawu danych, która zawiera tylko 25 kolumn.</span><span class="sxs-lookup"><span data-stu-id="441a1-115">For example, the second case would apply if a column index of 30 is used with an input dataset which has only 25 columns.</span></span>

2. <span data-ttu-id="441a1-116">Zestaw danych nie zawiera żadnych kolumn funkcji.</span><span class="sxs-lookup"><span data-stu-id="441a1-116">The dataset does not contain any Feature columns.</span></span> <span data-ttu-id="441a1-117">Na przykład jeśli wejściowy zestaw danych zawiera tylko jedną kolumnę, która jest oznaczona jako kolumna etykiety, nie byłoby żadne funkcje umożliwiające tworzenie modelu.</span><span class="sxs-lookup"><span data-stu-id="441a1-117">For example, if the input dataset has only one column, which is marked as the Label column, there would be no features with which to build the model.</span></span> <span data-ttu-id="441a1-118">W takim przypadku [Train Model] [ train-model] moduł powoduje błąd.</span><span class="sxs-lookup"><span data-stu-id="441a1-118">In this case, the [Train Model][train-model] module produces an error.</span></span>

3. <span data-ttu-id="441a1-119">Wejściowy zestaw danych (funkcji lub etykiety) zawiera nieskończoności jako wartość.</span><span class="sxs-lookup"><span data-stu-id="441a1-119">The input dataset (Features or Label) contains Infinity as a value.</span></span>

## <a name="score-model-module-produces-incorrect-results"></a><span data-ttu-id="441a1-120">Moduł score Model tworzy niepoprawnych wyników</span><span class="sxs-lookup"><span data-stu-id="441a1-120">Score Model Module produces incorrect results</span></span>

![image2](./media/machine-learning-debug-models/train_test-2.png)

<span data-ttu-id="441a1-122">W typowych eksperymentu uczenia/testowania dla uczenia nadzorowanego [podziału danych] [ split] modułu oryginalnego zestawu danych jest podzielony na dwie części: jedną część służy do nauczenia modelu, i jedną część służy do wyniku jak wykonuje również trenowanego modelu.</span><span class="sxs-lookup"><span data-stu-id="441a1-122">In a typical training/testing experiment for supervised learning, the [Split Data][split] module divides the original dataset into two parts: one part is used to train the model and one part is used to score how well the trained model performs.</span></span> <span data-ttu-id="441a1-123">Trenowanego modelu jest następnie używany do wyniku testu dane, po upływie którego wyniki są oceniane w celu sprawdzenia prawidłowości modelu.</span><span class="sxs-lookup"><span data-stu-id="441a1-123">The trained model is then used to score the test data, after which the results are evaluated to determine the accuracy of the model.</span></span>

<span data-ttu-id="441a1-124">[Score Model] [ score-model] moduł wymaga dwóch parametrów wejściowych:</span><span class="sxs-lookup"><span data-stu-id="441a1-124">The [Score Model][score-model] module requires two inputs:</span></span>

1. <span data-ttu-id="441a1-125">Dane wyjściowe uczonego modelu z [Train Model] [ train-model] modułu.</span><span class="sxs-lookup"><span data-stu-id="441a1-125">A trained model output from the [Train Model][train-model] module.</span></span>
2. <span data-ttu-id="441a1-126">Oceniania zestawu danych, który różni się od zestawu danych używany do uczenia modelu.</span><span class="sxs-lookup"><span data-stu-id="441a1-126">A scoring dataset that is different from the dataset used to train the model.</span></span>

<span data-ttu-id="441a1-127">Istnieje możliwość, że nawet jeśli eksperyment zakończy się powodzeniem, [Score Model] [ score-model] modułu tworzy niepoprawnych wyników.</span><span class="sxs-lookup"><span data-stu-id="441a1-127">It's possible that even though the experiment succeeds, the [Score Model][score-model] module produces incorrect results.</span></span> <span data-ttu-id="441a1-128">Może to spowodować na to kilka scenariuszy:</span><span class="sxs-lookup"><span data-stu-id="441a1-128">Several scenarios may cause this to happen:</span></span>

1. <span data-ttu-id="441a1-129">Jeśli etykiety są podzielone na kategorie i model regresji jest uczony na danych, nieprawidłowych danych wyjściowych będzie utworzonej przez [Score Model] [ score-model] modułu.</span><span class="sxs-lookup"><span data-stu-id="441a1-129">If the specified Label is categorical and a regression model is trained on the data, an incorrect output would be produced by the [Score Model][score-model] module.</span></span> <span data-ttu-id="441a1-130">Jest to spowodowane regresji wymaga zmiennej ciągłego odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="441a1-130">This is because regression requires a continuous response variable.</span></span> <span data-ttu-id="441a1-131">W takim wypadku byłoby bardziej odpowiednie do użycia z modelem klasyfikacji.</span><span class="sxs-lookup"><span data-stu-id="441a1-131">In this case, it would be more suitable to use a classification model.</span></span> 

2. <span data-ttu-id="441a1-132">Podobnie jeśli model klasyfikacji jest uczony w zestawie danych o zmiennoprzecinkową liczby w kolumnie Etykieta, może dać niepożądane wyniki.</span><span class="sxs-lookup"><span data-stu-id="441a1-132">Similarly, if a classification model is trained on a dataset having floating point numbers in the Label column, it may produce undesirable results.</span></span> <span data-ttu-id="441a1-133">Jest to spowodowane klasyfikacji wymaga zmiennej odrębny odpowiedzi, która zezwala tylko wartości zakresu za pośrednictwem skończona i zwykle nieco mały zestaw klas.</span><span class="sxs-lookup"><span data-stu-id="441a1-133">This is because classification requires a discrete response variable that only allows values that range over a finite, and usually somewhat small, set of classes.</span></span>

3. <span data-ttu-id="441a1-134">Jeśli oceniania zestawu danych nie zawiera wszystkie funkcje, które są używane do nauczenia modelu, [Score Model] [ score-model] powoduje błąd.</span><span class="sxs-lookup"><span data-stu-id="441a1-134">If the scoring dataset does not contain all the features used to train the model, the [Score Model][score-model] produces an error.</span></span>

4. <span data-ttu-id="441a1-135">Jeśli wiersza w zestawie danych oceniania zawiera brakujące wartości lub nieskończona wartość dla każdego z jego funkcji [Score Model] [ score-model] nie przyniesie żadnego wyniku odpowiadającego danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="441a1-135">If a row in the scoring dataset contains a missing value or an infinite value for any of its features, the [Score Model][score-model] will not produce any output corresponding to that row.</span></span>

5. <span data-ttu-id="441a1-136">[Score Model] [ score-model] może tworzyć identyczne dane wyjściowe dla wszystkich wierszy w zestawie wyników danych.</span><span class="sxs-lookup"><span data-stu-id="441a1-136">The [Score Model][score-model] may produce identical outputs for all rows in the scoring dataset.</span></span> <span data-ttu-id="441a1-137">To może wystąpić, na przykład podczas próby klasyfikacji za pomocą lasów decyzji, jeśli wybrano minimalną liczbę próbek na węzeł liścia musi mieć wartość większą niż liczba dostępnych przykłady szkolenia.</span><span class="sxs-lookup"><span data-stu-id="441a1-137">This could occur, for example, when attempting classification using Decision Forests if the minimum number of samples per leaf node is chosen to be more than the number of training examples available.</span></span>

<!-- Module References -->
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/

