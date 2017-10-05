---
title: "Krok 5: Wdrażanie usługi sieci web Machine Learning | Dokumentacja firmy Microsoft"
description: "Krok 5 opracowanie wskazówki rozwiązanie predykcyjne: Wdrażanie eksperyment predykcyjny w usłudze Machine Learning Studio jako usługę sieci web."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 3fca74a3-c44b-4583-a218-c14c46ee5338
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: cec1bcceea158a20742c7019a266dcefaac4c9cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="walkthrough-step-5-deploy-the-azure-machine-learning-web-service"></a><span data-ttu-id="cd417-103">Przewodnik, krok 5. Wdrażanie usługi sieci Web Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="cd417-103">Walkthrough Step 5: Deploy the Azure Machine Learning web service</span></span>
<span data-ttu-id="cd417-104">Jest to krok piąty tego przewodnika, [tworzenie rozwiązania analizy predykcyjnej w usłudze Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="cd417-104">This is the fifth step of the walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. [<span data-ttu-id="cd417-105">Tworzenie obszaru roboczego usługi Machine Learning</span><span class="sxs-lookup"><span data-stu-id="cd417-105">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="cd417-106">Przekazywanie istniejących danych</span><span class="sxs-lookup"><span data-stu-id="cd417-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="cd417-107">Tworzenie nowego eksperymentu</span><span class="sxs-lookup"><span data-stu-id="cd417-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="cd417-108">Nauczanie i ocena modeli</span><span class="sxs-lookup"><span data-stu-id="cd417-108">Train and evaluate the models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. <span data-ttu-id="cd417-109">**Wdrażanie usługi sieci Web**</span><span class="sxs-lookup"><span data-stu-id="cd417-109">**Deploy the web service**</span></span>
6. [<span data-ttu-id="cd417-110">Uzyskiwanie dostępu do usługi sieci Web</span><span class="sxs-lookup"><span data-stu-id="cd417-110">Access the web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<span data-ttu-id="cd417-111">Udostępniania możliwość użycia modelu predykcyjnego, który opracowaliśmy w ramach tego przewodnika, możemy go wdrożyć jako usługę sieci web na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="cd417-111">To give others a chance to use the predictive model we've developed in this walkthrough, we can deploy it as a web service on Azure.</span></span>

<span data-ttu-id="cd417-112">Do tego momentu możemy były zmieniane uczenie modelu.</span><span class="sxs-lookup"><span data-stu-id="cd417-112">Up to this point we've been experimenting with training our model.</span></span> <span data-ttu-id="cd417-113">Ale wdrożonej usługi nie będzie przeprowadzenie szkolenia — będzie można wygenerować nowy prognoz przez oceniania oparte na modelu danych wejściowych użytkownika.</span><span class="sxs-lookup"><span data-stu-id="cd417-113">But the deployed service is no longer going to do training - it's going to generate new predictions by scoring the user's input based on our model.</span></span> <span data-ttu-id="cd417-114">Dlatego chcemy są pewne przygotowania można przekonwertować tego doświadczenia z ***szkolenia*** eksperymentu do ***predykcyjnej*** eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="cd417-114">So we're going to do some preparation to convert this experiment from a ***training*** experiment to a ***predictive*** experiment.</span></span> 

<span data-ttu-id="cd417-115">Jest to proces trzech etapów:</span><span class="sxs-lookup"><span data-stu-id="cd417-115">This is a three-step process:</span></span>  

1. <span data-ttu-id="cd417-116">Usuń jeden z modeli</span><span class="sxs-lookup"><span data-stu-id="cd417-116">Remove one of the models</span></span>
2. <span data-ttu-id="cd417-117">Konwertuj *eksperyment uczenia* utworzyliśmy do *eksperyment predykcyjny*</span><span class="sxs-lookup"><span data-stu-id="cd417-117">Convert the *training experiment* we've created into a *predictive experiment*</span></span>
3. <span data-ttu-id="cd417-118">Wdrażanie eksperyment predykcyjny jako usługę sieci web</span><span class="sxs-lookup"><span data-stu-id="cd417-118">Deploy the predictive experiment as a web service</span></span>

## <a name="remove-one-of-the-models"></a><span data-ttu-id="cd417-119">Usuń jeden z modeli</span><span class="sxs-lookup"><span data-stu-id="cd417-119">Remove one of the models</span></span>

<span data-ttu-id="cd417-120">Najpierw musimy nieco trim tego eksperymentu w dół.</span><span class="sxs-lookup"><span data-stu-id="cd417-120">First, we need to trim this experiment down a little.</span></span> <span data-ttu-id="cd417-121">Obecnie istnieją dwa różne modele w eksperymencie, ale chcemy używać jednego modelu do nas wdrażania to jako usługę sieci web.</span><span class="sxs-lookup"><span data-stu-id="cd417-121">We currently have two different models in the experiment, but we only want to use one model when we deploy this as a web service.</span></span>  

<span data-ttu-id="cd417-122">Załóżmy, że decydujesz się, że boosted drzewa modelu działa lepiej niż SVM model.</span><span class="sxs-lookup"><span data-stu-id="cd417-122">Let's say we've decided that the boosted tree model performed better than the SVM model.</span></span> <span data-ttu-id="cd417-123">Dlatego najpierw musisz usunąć [maszyny wektorowa obsługa Two-Class] [ two-class-support-vector-machine] modułu i modułów, które były używane na potrzeby uczenia go.</span><span class="sxs-lookup"><span data-stu-id="cd417-123">So the first thing to do is remove the [Two-Class Support Vector Machine][two-class-support-vector-machine] module and the modules that were used for training it.</span></span> <span data-ttu-id="cd417-124">Warto najpierw utworzyć kopię eksperyment, klikając **Zapisz jako** w dolnej części obszaru roboczego eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="cd417-124">You may want to make a copy of the experiment first by clicking **Save As** at the bottom of the experiment canvas.</span></span>

<span data-ttu-id="cd417-125">Musimy usunąć następujących modułów:</span><span class="sxs-lookup"><span data-stu-id="cd417-125">We need to delete the following modules:</span></span>  

* <span data-ttu-id="cd417-126">[Obsługa Two-Class wektor maszyny][two-class-support-vector-machine]</span><span class="sxs-lookup"><span data-stu-id="cd417-126">[Two-Class Support Vector Machine][two-class-support-vector-machine]</span></span>
* <span data-ttu-id="cd417-127">[Uczenie modelu] [ train-model] i [Score Model] [ score-model] modułów, które zostały dołączone do niego</span><span class="sxs-lookup"><span data-stu-id="cd417-127">[Train Model][train-model] and [Score Model][score-model] modules that were connected to it</span></span>
* <span data-ttu-id="cd417-128">[Normalizuj danych] [ normalize-data] (oba)</span><span class="sxs-lookup"><span data-stu-id="cd417-128">[Normalize Data][normalize-data] (both of them)</span></span>
* <span data-ttu-id="cd417-129">[Ocena modelu] [ evaluate-model] (ponieważ jesteśmy zakończono ocenę modeli)</span><span class="sxs-lookup"><span data-stu-id="cd417-129">[Evaluate Model][evaluate-model] (because we're finished evaluating the models)</span></span>

<span data-ttu-id="cd417-130">Wybierz każdego modułu i naciśnij klawisz Delete, lub kliknij prawym przyciskiem myszy moduł i zaznacz **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="cd417-130">Select each module and press the Delete key, or right-click the module and select **Delete**.</span></span> 

![Usunięte modelu SVM][3a]

<span data-ttu-id="cd417-132">Nasz model powinien teraz wyglądać mniej więcej tak:</span><span class="sxs-lookup"><span data-stu-id="cd417-132">Our model should now look something like this:</span></span>

![Usunięte modelu SVM][3]

<span data-ttu-id="cd417-134">Teraz już wszystko gotowe do wdrożenia tego model przy użyciu [Two-Class Boosted drzewa decyzyjnego][two-class-boosted-decision-tree].</span><span class="sxs-lookup"><span data-stu-id="cd417-134">Now we're ready to deploy this model using the [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree].</span></span>

## <a name="convert-the-training-experiment-to-a-predictive-experiment"></a><span data-ttu-id="cd417-135">Konwertuj eksperyment uczenia eksperyment predykcyjny</span><span class="sxs-lookup"><span data-stu-id="cd417-135">Convert the training experiment to a predictive experiment</span></span>

<span data-ttu-id="cd417-136">W celu przygotowania do wdrożenia tego modelu, musimy przekonwertować tej eksperyment uczenia eksperyment predykcyjny.</span><span class="sxs-lookup"><span data-stu-id="cd417-136">To get this model ready for deployment, we need to convert this training experiment to a predictive experiment.</span></span> <span data-ttu-id="cd417-137">Obejmuje to trzy kroki:</span><span class="sxs-lookup"><span data-stu-id="cd417-137">This involves three steps:</span></span>

1. <span data-ttu-id="cd417-138">Zapisz model możemy gdy udało się nauczyć, a następnie zastąp naszych modułów szkoleniowych</span><span class="sxs-lookup"><span data-stu-id="cd417-138">Save the model we've trained and then replace our training modules</span></span>
2. <span data-ttu-id="cd417-139">TRIM eksperyment, aby usunąć modułów, które były potrzebne tylko w przypadku szkolenia</span><span class="sxs-lookup"><span data-stu-id="cd417-139">Trim the experiment to remove modules that were only needed for training</span></span>
3. <span data-ttu-id="cd417-140">Zdefiniuj którym usługa sieci web będzie akceptować dane wejściowe i gdzie generuje dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="cd417-140">Define where the web service will accept input and where it generates the output</span></span>

<span data-ttu-id="cd417-141">Firma Microsoft może to zrobić ręcznie, ale na szczęście wszystkie trzy kroki można wykonać, klikając **ustawić usługę sieci Web** w dolnej części obszaru roboczego eksperymentu (i wybierając **predykcyjnej usługi sieci Web** opcja).</span><span class="sxs-lookup"><span data-stu-id="cd417-141">We could do this manually, but fortunately all three steps can be accomplished by clicking **Set Up Web Service** at the bottom of the experiment canvas (and selecting the **Predictive Web Service** option).</span></span>

> [!TIP]
> <span data-ttu-id="cd417-142">Jeśli chcesz bardziej szczegółowe informacje, na co się dzieje podczas konwertowania eksperyment uczenia eksperyment predykcyjny, zobacz [jak przygotować modelu do wdrożenia w usłudze Azure Machine Learning Studio](machine-learning-convert-training-experiment-to-scoring-experiment.md).</span><span class="sxs-lookup"><span data-stu-id="cd417-142">If you want more details on what happens when you convert a training experiment to a predictive experiment, see [How to prepare your model for deployment in Azure Machine Learning Studio](machine-learning-convert-training-experiment-to-scoring-experiment.md).</span></span>

<span data-ttu-id="cd417-143">Po kliknięciu **ustawić usługę sieci Web**, ma miejsce kilka rzeczy:</span><span class="sxs-lookup"><span data-stu-id="cd417-143">When you click **Set Up Web Service**, several things happen:</span></span>

* <span data-ttu-id="cd417-144">Trenowanego modelu jest konwertowana na jeden **Uczonego modelu** modułu i przechowywane na palecie modułów z lewej strony obszaru roboczego eksperymentu (można znaleźć go w **przeszkolone modele**)</span><span class="sxs-lookup"><span data-stu-id="cd417-144">The trained model is converted to a single **Trained Model** module and stored in the module palette to the left of the experiment canvas (you can find it under **Trained Models**)</span></span>
* <span data-ttu-id="cd417-145">Moduły, które były używane do trenowania zostaną usunięte; w szczególności:</span><span class="sxs-lookup"><span data-stu-id="cd417-145">Modules that were used for training are removed; specifically:</span></span>
  * <span data-ttu-id="cd417-146">[Two-Class Boosted algorytm][two-class-boosted-decision-tree]</span><span class="sxs-lookup"><span data-stu-id="cd417-146">[Two-Class Boosted Decision Tree][two-class-boosted-decision-tree]</span></span>
  * <span data-ttu-id="cd417-147">[Train Model][train-model]</span><span class="sxs-lookup"><span data-stu-id="cd417-147">[Train Model][train-model]</span></span>
  * <span data-ttu-id="cd417-148">[Podział danych][split]</span><span class="sxs-lookup"><span data-stu-id="cd417-148">[Split Data][split]</span></span>
  * <span data-ttu-id="cd417-149">drugi [wykonanie skryptu języka R] [ execute-r-script] moduł, który był używany dla danych testowych</span><span class="sxs-lookup"><span data-stu-id="cd417-149">the second [Execute R Script][execute-r-script] module that was used for test data</span></span>
* <span data-ttu-id="cd417-150">Zapisane trenowanego modelu jest dodawany do eksperymentu</span><span class="sxs-lookup"><span data-stu-id="cd417-150">The saved trained model is added back into the experiment</span></span>
* <span data-ttu-id="cd417-151">**Usługi danych wejściowych w sieci Web** i **sieci Web usług** moduły są dodawane (te informacje pozwalają określić gdzie przechodzą w modelu danych użytkownika i jakie dane są zwracane podczas uzyskiwania dostępu do usługi sieci web)</span><span class="sxs-lookup"><span data-stu-id="cd417-151">**Web service input** and **Web service output** modules are added (these identify where the user's data will enter the model, and what data is returned, when the web service is accessed)</span></span>

> [!NOTE]
> <span data-ttu-id="cd417-152">Widać, że eksperyment został zapisany w dwóch częściach na kartach, które zostały dodane w górnej części obszaru roboczego eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="cd417-152">You can see that the experiment is saved in two parts under tabs that have been added at the top of the experiment canvas.</span></span> <span data-ttu-id="cd417-153">Oryginalny eksperyment uczenia się na karcie **eksperyment uczenia**, i nowo utworzony eksperyment predykcyjny podlega **eksperyment predykcyjny**.</span><span class="sxs-lookup"><span data-stu-id="cd417-153">The original training experiment is under the tab **Training experiment**, and the newly created predictive experiment is under **Predictive experiment**.</span></span> <span data-ttu-id="cd417-154">Eksperyment predykcyjny jest firma Microsoft będzie wdrożyć jako usługę sieci web.</span><span class="sxs-lookup"><span data-stu-id="cd417-154">The predictive experiment is the one we'll deploy as a web service.</span></span>

<span data-ttu-id="cd417-155">Musimy wykonać jednego dodatkowego kroku z tego konkretnego eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="cd417-155">We need to take one additional step with this particular experiment.</span></span>
<span data-ttu-id="cd417-156">Dodaliśmy dwie [wykonanie skryptu języka R] [ execute-r-script] modułów, aby zapewnić funkcji wagę w odniesieniu do danych.</span><span class="sxs-lookup"><span data-stu-id="cd417-156">We added two [Execute R Script][execute-r-script] modules to provide a weighting function to the data.</span></span> <span data-ttu-id="cd417-157">Po prostu lewy, czego potrzeba do uczenie i testowanie, która jest więc firma Microsoft może zająć się tych modułów w ostatnim modelu.</span><span class="sxs-lookup"><span data-stu-id="cd417-157">That was just a trick we needed for training and testing, so we can take out those modules in the final model.</span></span>
<span data-ttu-id="cd417-158">Usługa Machine Learning Studio usunąć jedną [wykonanie skryptu języka R] [ execute-r-script] modułu po jego usunięciu [podziału] [ split] modułu.</span><span class="sxs-lookup"><span data-stu-id="cd417-158">Machine Learning Studio removed one [Execute R Script][execute-r-script] module when it removed the [Split][split] module.</span></span> <span data-ttu-id="cd417-159">Teraz możemy usunąć inny i połączyć [Edytor metadanych] [ metadata-editor] bezpośrednio do [Score Model][score-model].</span><span class="sxs-lookup"><span data-stu-id="cd417-159">Now we can remove the other and connect [Metadata Editor][metadata-editor] directly to [Score Model][score-model].</span></span>    

<span data-ttu-id="cd417-160">Naszym doświadczeniu powinna wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="cd417-160">Our experiment should now look like this:</span></span>  

![Ocenianie trenowanego modelu][4]  

> [!NOTE]
> <span data-ttu-id="cd417-162">Możesz się zastanawiać, dlaczego możemy wywołało dataset danych karty kredytowej niemiecki UCI eksperyment predykcyjny.</span><span class="sxs-lookup"><span data-stu-id="cd417-162">You may be wondering why we left the UCI German Credit Card Data dataset in the predictive experiment.</span></span> <span data-ttu-id="cd417-163">Usługa ma wynik danych użytkownika, nie oryginalnego zestawu danych, więc Dlaczego pozostaw oryginalnego zestawu danych w modelu?</span><span class="sxs-lookup"><span data-stu-id="cd417-163">The service is going to score the user's data, not the original dataset, so why leave the original dataset in the model?</span></span>
> 
> <span data-ttu-id="cd417-164">Jest to wartość true, że usługa nie wymaga oryginalnych danych karty kredytowej.</span><span class="sxs-lookup"><span data-stu-id="cd417-164">It's true that the service doesn't need the original credit card data.</span></span> <span data-ttu-id="cd417-165">Jednak musi schematu dla danych, które obejmują takie informacje jak liczbę kolumn są i kolumny, które są liczbowych.</span><span class="sxs-lookup"><span data-stu-id="cd417-165">But it does need the schema for that data, which includes information such as how many columns there are and which columns are numeric.</span></span> <span data-ttu-id="cd417-166">Informacje o schemacie jest interpretować dane użytkownika.</span><span class="sxs-lookup"><span data-stu-id="cd417-166">This schema information is necessary to interpret the user's data.</span></span> <span data-ttu-id="cd417-167">Firma Microsoft pozostawić te składniki, połączony, dzięki czemu oceniania moduł ma schemat zestawu danych, gdy usługa jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="cd417-167">We leave these components connected so that the scoring module has the dataset schema when the service is running.</span></span> <span data-ttu-id="cd417-168">Dane nie jest używana, tylko schemat.</span><span class="sxs-lookup"><span data-stu-id="cd417-168">The data isn't used, just the schema.</span></span>  
> 
> 

<span data-ttu-id="cd417-169">Uruchom eksperyment raz ostatni (kliknij **Uruchom**.) Jeśli chcesz sprawdzić, czy model nadal działa, kliknij przycisk dane wyjściowe [Score Model] [ score-model] moduł i zaznacz **wyświetlanie wyników**.</span><span class="sxs-lookup"><span data-stu-id="cd417-169">Run the experiment one last time (click **Run**.) If you want to verify that the model is still working, click the output of the [Score Model][score-model] module and select **View Results**.</span></span> <span data-ttu-id="cd417-170">Widać, że oryginalne dane zostanie wyświetlona, wraz z wartości ryzyka środki ("oceniane etykiety") i oceniania wartość prawdopodobieństwa ("wynik prawdopodobieństwa".)</span><span class="sxs-lookup"><span data-stu-id="cd417-170">You can see that the original data is displayed, along with the credit risk value ("Scored Labels") and the scoring probability value ("Scored Probabilities".)</span></span> 

## <a name="deploy-the-web-service"></a><span data-ttu-id="cd417-171">Wdrażanie usługi sieci Web</span><span class="sxs-lookup"><span data-stu-id="cd417-171">Deploy the web service</span></span>
<span data-ttu-id="cd417-172">Eksperyment można wdrożyć jako albo klasycznym usługi sieci web, lub Nowa usługa sieci web, która jest oparta na usłudze Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="cd417-172">You can deploy the experiment as either a Classic web service, or as a New web service that's based on Azure Resource Manager.</span></span>

### <a name="deploy-as-a-classic-web-service"></a><span data-ttu-id="cd417-173">Wdrożyć jako usługę sieci web klasycznego</span><span class="sxs-lookup"><span data-stu-id="cd417-173">Deploy as a Classic web service</span></span>
<span data-ttu-id="cd417-174">Aby wdrożyć usługę sieci web klasycznego pochodzące z naszych eksperyment, kliknij przycisk **wdrażanie usługi sieci Web** poniżej kanwy i wybierz **wdrażanie usługi sieci Web [klasyczny]**.</span><span class="sxs-lookup"><span data-stu-id="cd417-174">To deploy a Classic web service derived from our experiment, click **Deploy Web Service** below the canvas and select **Deploy Web Service [Classic]**.</span></span> <span data-ttu-id="cd417-175">Usługa Machine Learning Studio wdraża eksperymentu jako usługę sieci web i przejście do pulpitu nawigacyjnego dla tej usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="cd417-175">Machine Learning Studio deploys the experiment as a web service and takes you to the dashboard for that web service.</span></span> <span data-ttu-id="cd417-176">Na tej stronie możesz powrócić do eksperymentu (**widoku migawki** lub **wyświetlić najnowszych**) i uruchamianie testu proste usługi sieci web (zobacz **przetestować usługę sieci web** poniżej).</span><span class="sxs-lookup"><span data-stu-id="cd417-176">From this page you can return to the experiment (**View snapshot** or **View latest**) and run a simple test of the web service (see **Test the web service** below).</span></span> <span data-ttu-id="cd417-177">Istnieje również tutaj informacje dotyczące tworzenia aplikacji, które mogą uzyskiwać dostęp do usługi sieci web (omówiona w następnym kroku w tym przewodniku).</span><span class="sxs-lookup"><span data-stu-id="cd417-177">There is also information here for creating applications that can access the web service (more on that in the next step of this walkthrough).</span></span>

![Pulpit nawigacyjny usługi sieci Web][6]

<span data-ttu-id="cd417-179">Usługę można skonfigurować, klikając **konfiguracji** kartę.</span><span class="sxs-lookup"><span data-stu-id="cd417-179">You can configure the service by clicking the **CONFIGURATION** tab.</span></span> <span data-ttu-id="cd417-180">W tym miejscu można zmodyfikować nazwy usługi (go została podana nazwa eksperymentu domyślnie) i nadaj mu opis.</span><span class="sxs-lookup"><span data-stu-id="cd417-180">Here you can modify the service name (it's given the experiment name by default) and give it a description.</span></span> <span data-ttu-id="cd417-181">Możesz też udzielić większej liczby etykiet przyjazną dla danych wejściowych i wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="cd417-181">You can also give more friendly labels for the input and output data.</span></span>  

![Konfiguruj usługę sieci web][5]  

### <a name="deploy-as-a-new-web-service"></a><span data-ttu-id="cd417-183">Wdrożyć jako nową usługę sieci web</span><span class="sxs-lookup"><span data-stu-id="cd417-183">Deploy as a New web service</span></span>

> [!NOTE] 
> <span data-ttu-id="cd417-184">Aby wdrożyć nową usługę sieci web musi mieć wystarczające uprawnienia do subskrypcji, w której wdrażasz usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="cd417-184">To deploy a New web service you must have sufficient permissions in the subscription to which you are deploying the web service.</span></span> <span data-ttu-id="cd417-185">Aby uzyskać więcej informacji, zobacz [zarządzania usługi sieci web przy użyciu portalu usługi sieci Web systemu Azure Machine Learning](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="cd417-185">For more information, see [Manage a web service using the Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="cd417-186">Aby wdrożyć nową usługę sieci web pochodzące z naszym doświadczeniu:</span><span class="sxs-lookup"><span data-stu-id="cd417-186">To deploy a New web service derived from our experiment:</span></span>

1. <span data-ttu-id="cd417-187">Kliknij przycisk **wdrażanie usługi sieci Web** poniżej kanwy i wybierz **wdrażanie usługi sieci Web [New]**.</span><span class="sxs-lookup"><span data-stu-id="cd417-187">Click **Deploy Web Service** below the canvas and select **Deploy Web Service [New]**.</span></span> <span data-ttu-id="cd417-188">Usługa Machine Learning Studio przenosi do usług sieci web Azure Machine Learning **wdrażanie eksperymentu** strony.</span><span class="sxs-lookup"><span data-stu-id="cd417-188">Machine Learning Studio transfers you to the Azure Machine Learning web services **Deploy Experiment** page.</span></span>

2. <span data-ttu-id="cd417-189">Wprowadź nazwę usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="cd417-189">Enter a name for the web service.</span></span> 

3. <span data-ttu-id="cd417-190">Dla **planu cen**, można wybrać istniejącego planu cenowego, lub wybierz opcję "Utwórz nowy" i także nazwę nowego planu i wybierz opcję miesięczne planu.</span><span class="sxs-lookup"><span data-stu-id="cd417-190">For **Price Plan**, you can select an existing pricing plan, or select "Create new" and give the new plan a name and select the monthly plan option.</span></span> <span data-ttu-id="cd417-191">Plan domyślny warstw do planów dla regionu domyślnego i usługi sieci web jest wdrażany do tego regionu.</span><span class="sxs-lookup"><span data-stu-id="cd417-191">The plan tiers default to the plans for your default region and your web service is deployed to that region.</span></span>

4. <span data-ttu-id="cd417-192">Kliknij przycisk **wdrażanie**.</span><span class="sxs-lookup"><span data-stu-id="cd417-192">Click **Deploy**.</span></span>

<span data-ttu-id="cd417-193">Po kilku minutach **szybkiego startu** zostanie otwarta strona dla usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="cd417-193">After a few minutes, the **Quickstart** page for your web service opens.</span></span>

<span data-ttu-id="cd417-194">Usługę można skonfigurować, klikając **Konfiguruj** kartę.</span><span class="sxs-lookup"><span data-stu-id="cd417-194">You can configure the service by clicking the **Configure** tab.</span></span> <span data-ttu-id="cd417-195">W tym miejscu można zmodyfikować usługi tytuł i nadaj mu opis.</span><span class="sxs-lookup"><span data-stu-id="cd417-195">Here you can modify the service title and give it a description.</span></span> 

<span data-ttu-id="cd417-196">Aby przetestować usługę sieci web, kliknij przycisk **Test** kartę (zobacz **przetestować usługę sieci web** poniżej).</span><span class="sxs-lookup"><span data-stu-id="cd417-196">To test the web service, click the **Test** tab (see **Test the web service** below).</span></span> <span data-ttu-id="cd417-197">Aby uzyskać informacje dotyczące tworzenia aplikacji, które mogą uzyskiwać dostęp do usługi sieci web, kliknij przycisk **Consume** kartę (do następnego kroku w tym przewodniku zostaną umieszczone w bardziej szczegółowo).</span><span class="sxs-lookup"><span data-stu-id="cd417-197">For information on creating applications that can access the web service, click the **Consume** tab (the next step in this walkthrough will go into more detail).</span></span>

> [!TIP]
> <span data-ttu-id="cd417-198">Należy zaktualizować usługę sieci web, po jej wdrożeniu.</span><span class="sxs-lookup"><span data-stu-id="cd417-198">You can update the web service after you've deployed it.</span></span> <span data-ttu-id="cd417-199">Na przykład, jeśli chcesz zmienić model, a następnie edytować eksperyment uczenia, dostosować parametry modelu i kliknij przycisk **wdrażanie usługi sieci Web**, wybierając żądane **wdrażanie usługi sieci Web [klasyczny]** lub **Wdrażanie usługi sieci Web [New]**.</span><span class="sxs-lookup"><span data-stu-id="cd417-199">For example, if you want to change your model, then you can edit the training experiment, tweak the model parameters, and click **Deploy Web Service**, selecting **Deploy Web Service [Classic]** or **Deploy Web Service [New]**.</span></span> <span data-ttu-id="cd417-200">Wdrażając eksperyment ponownie, zastępuje usługę sieci web za pomocą zaktualizowanej modelu.</span><span class="sxs-lookup"><span data-stu-id="cd417-200">When you deploy the experiment again, it replaces the web service, now using your updated model.</span></span>  
> 
> 

## <a name="test-the-web-service"></a><span data-ttu-id="cd417-201">Testowanie usługi sieci web</span><span class="sxs-lookup"><span data-stu-id="cd417-201">Test the web service</span></span>

<span data-ttu-id="cd417-202">Podczas uzyskiwania dostępu do usługi sieci web dane użytkownika wprowadza za pośrednictwem **sieci Web dane wejściowe usługi** modułu, w którym są przekazywane do [Score Model] [ score-model] modułu i oceniane.</span><span class="sxs-lookup"><span data-stu-id="cd417-202">When the web service is accessed, the user's data enters through the **Web service input** module where it's passed to the [Score Model][score-model] module and scored.</span></span> <span data-ttu-id="cd417-203">Sposobu skonfigurowaliśmy eksperyment predykcyjny modelu oczekuje danych w tym samym formacie co oryginalnego zestawu danych ryzyko kredytowe.</span><span class="sxs-lookup"><span data-stu-id="cd417-203">The way we've set up the predictive experiment, the model expects data in the same format as the original credit risk dataset.</span></span>
<span data-ttu-id="cd417-204">Wyniki są zwracane do użytkownika z usługi sieci web za pośrednictwem **sieci Web usług** modułu.</span><span class="sxs-lookup"><span data-stu-id="cd417-204">The results are returned to the user from the web service through the **Web service output** module.</span></span>

> [!TIP]
> <span data-ttu-id="cd417-205">Sposób mamy eksperyment predykcyjny skonfigurowane, wynikiem całą [Score Model] [ score-model] modułu są zwracane.</span><span class="sxs-lookup"><span data-stu-id="cd417-205">The way we have the predictive experiment configured, the entire results from the [Score Model][score-model] module are returned.</span></span> <span data-ttu-id="cd417-206">W tym wszystkie dane wejściowe oraz wartość ryzyko kredytowe i oceniania prawdopodobieństwa.</span><span class="sxs-lookup"><span data-stu-id="cd417-206">This includes all the input data plus the credit risk value and the scoring probability.</span></span> <span data-ttu-id="cd417-207">Ale może inny zwracać — na przykład można zwrócić tylko wartość ryzyko kredytowe.</span><span class="sxs-lookup"><span data-stu-id="cd417-207">But you can return something different if you want - for example, you could return just the credit risk value.</span></span> <span data-ttu-id="cd417-208">Aby to zrobić, Wstaw [kolumny projektu] [ project-columns] modułu między [Score Model] [ score-model] i **sieci Web produktu**wyeliminować kolumny nie mają usługę sieci web do zwrócenia.</span><span class="sxs-lookup"><span data-stu-id="cd417-208">To do this, insert a [Project Columns][project-columns] module between [Score Model][score-model] and the **Web service output** to eliminate columns you don't want the web service to return.</span></span> 
> 
> 

<span data-ttu-id="cd417-209">Można przetestować web klasycznym usługi w **Machine Learning Studio** lub **usługi sieci Web systemu Azure Machine Learning** portalu.</span><span class="sxs-lookup"><span data-stu-id="cd417-209">You can test a Classic web service either in **Machine Learning Studio** or in the **Azure Machine Learning Web Services** portal.</span></span>
<span data-ttu-id="cd417-210">Możesz przetestować nową sieć web service tylko w **usługi sieci Web usługi Machine Learning** portalu.</span><span class="sxs-lookup"><span data-stu-id="cd417-210">You can test a New web service only in the **Machine Learning Web Services** portal.</span></span>

> [!TIP]
> <span data-ttu-id="cd417-211">Podczas testowania, w portalu usługi sieci Web systemu Azure Machine Learning, może mieć portalu tworzenie przykładowych danych, które służy do testowania usługi żądań i odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="cd417-211">When testing in the Azure Machine Learning Web Services portal, you can have the portal create sample data that you can use to test the Request-Response service.</span></span> <span data-ttu-id="cd417-212">Na **Konfiguruj** wybierz przycisk Tak, aby uzyskać **przykładowych danych włączone?**.</span><span class="sxs-lookup"><span data-stu-id="cd417-212">On the **Configure** page, select "Yes" for **Sample Data Enabled?**.</span></span> <span data-ttu-id="cd417-213">Po otwarciu karty żądań i odpowiedzi na **testu** strony portalu wypełnia przykładowe dane pobrane z oryginalnego zestawu danych ryzyko kredytowe.</span><span class="sxs-lookup"><span data-stu-id="cd417-213">When you open the Request-Response tab on the **Test** page, the portal fills in sample data taken from the original credit risk dataset.</span></span>

### <a name="test-a-classic-web-service"></a><span data-ttu-id="cd417-214">Testowanie usługi sieci web klasycznego</span><span class="sxs-lookup"><span data-stu-id="cd417-214">Test a Classic web service</span></span>

<span data-ttu-id="cd417-215">Usługi sieci web klasycznego można przetestować w usłudze Machine Learning Studio lub w portalu usługi sieci Web usługi Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="cd417-215">You can test a Classic web service in Machine Learning Studio or in the Machine Learning Web Services portal.</span></span> 

#### <a name="test-in-machine-learning-studio"></a><span data-ttu-id="cd417-216">Testowanie w usłudze Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="cd417-216">Test in Machine Learning Studio</span></span>

1. <span data-ttu-id="cd417-217">Na **pulpitu NAWIGACYJNEGO** usługi sieci web kliknij pozycję **testu** przycisku w obszarze **domyślny punkt końcowy**.</span><span class="sxs-lookup"><span data-stu-id="cd417-217">On the **DASHBOARD** page for the web service, click the **Test** button under **Default Endpoint**.</span></span> <span data-ttu-id="cd417-218">Okno dialogowe wyskakującej i monituje o dane wejściowe dla usługi.</span><span class="sxs-lookup"><span data-stu-id="cd417-218">A dialog pops up and asks you for the input data for the service.</span></span> <span data-ttu-id="cd417-219">Są to te same kolumny, które znajdowały się w zestawie danych oryginalnego ryzyko kredytowe.</span><span class="sxs-lookup"><span data-stu-id="cd417-219">These are the same columns that appeared in the original credit risk dataset.</span></span>  

2. <span data-ttu-id="cd417-220">Wprowadź zestaw danych, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="cd417-220">Enter a set of data and then click **OK**.</span></span> 

#### <a name="test-in-the-machine-learning-web-services-portal"></a><span data-ttu-id="cd417-221">Testowanie w portalu usługi sieci Web usługi Machine Learning</span><span class="sxs-lookup"><span data-stu-id="cd417-221">Test in the Machine Learning Web Services portal</span></span>

1. <span data-ttu-id="cd417-222">Na **pulpitu NAWIGACYJNEGO** usługi sieci web kliknij pozycję **Podgląd testów** łącze w obszarze **domyślny punkt końcowy**.</span><span class="sxs-lookup"><span data-stu-id="cd417-222">On the **DASHBOARD** page for the web service, click the **Test preview** link under **Default Endpoint**.</span></span> <span data-ttu-id="cd417-223">Strona testowa w portalu usługi sieci Web systemu Azure Machine Learning punktu końcowego usługi sieci web otwiera i monituje o dane wejściowe dla usługi.</span><span class="sxs-lookup"><span data-stu-id="cd417-223">The test page in the Azure Machine Learning Web Services portal for the web service endpoint opens and asks you for the input data for the service.</span></span> <span data-ttu-id="cd417-224">Są to te same kolumny, które znajdowały się w zestawie danych oryginalnego ryzyko kredytowe.</span><span class="sxs-lookup"><span data-stu-id="cd417-224">These are the same columns that appeared in the original credit risk dataset.</span></span>

2. <span data-ttu-id="cd417-225">Kliknij przycisk **Test żądań i odpowiedzi**.</span><span class="sxs-lookup"><span data-stu-id="cd417-225">Click **Test Request-Response**.</span></span> 

### <a name="test-a-new-web-service"></a><span data-ttu-id="cd417-226">Przetestować nową usługę sieci web</span><span class="sxs-lookup"><span data-stu-id="cd417-226">Test a New web service</span></span>

<span data-ttu-id="cd417-227">Możesz przetestować nową usługę sieci web tylko w portalu usługi sieci Web usługi Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="cd417-227">You can test a New web service only in the Machine Learning Web Services portal.</span></span>

1. <span data-ttu-id="cd417-228">W [usługi sieci Web systemu Azure Machine Learning](https://services.azureml.net/quickstart) portalu, kliknij przycisk **testu** w górnej części strony.</span><span class="sxs-lookup"><span data-stu-id="cd417-228">In the [Azure Machine Learning Web Services](https://services.azureml.net/quickstart) portal, click **Test** at the top of the page.</span></span> <span data-ttu-id="cd417-229">**Testu** zostanie otwarta strona i można wprowadzić dane dotyczące usługi.</span><span class="sxs-lookup"><span data-stu-id="cd417-229">The **Test** page opens and you can input data for the service.</span></span> <span data-ttu-id="cd417-230">Wyświetlane pól wejściowych odpowiada kolumn, które znajdowały się w zestawie danych oryginalnego ryzyko kredytowe.</span><span class="sxs-lookup"><span data-stu-id="cd417-230">The input fields displayed correspond to the columns that appeared in the original credit risk dataset.</span></span> 

2. <span data-ttu-id="cd417-231">Wprowadź zestaw danych, a następnie kliknij przycisk **testu żądanie-odpowiedź**.</span><span class="sxs-lookup"><span data-stu-id="cd417-231">Enter a set of data and then click **Test Request-Response**.</span></span>

<span data-ttu-id="cd417-232">Wyniki testu są wyświetlane po prawej stronie strony w kolumnie wyników.</span><span class="sxs-lookup"><span data-stu-id="cd417-232">The results of the test are displayed on the right-hand side of the page in the output column.</span></span> 


## <a name="manage-the-web-service"></a><span data-ttu-id="cd417-233">Zarządzanie usługą sieci web</span><span class="sxs-lookup"><span data-stu-id="cd417-233">Manage the web service</span></span>

### <a name="manage-a-classic-web-service-in-the-azure-classic-portal"></a><span data-ttu-id="cd417-234">Zarządzanie usługą sieci web klasycznego w klasycznym portalu Azure</span><span class="sxs-lookup"><span data-stu-id="cd417-234">Manage a Classic web service in the Azure classic portal</span></span>

<span data-ttu-id="cd417-235">Po wdrożeniu usługi sieci web klasycznego, można zarządzać nim z [klasycznego portalu Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="cd417-235">Once you've deployed your Classic web service, you can manage it from the [Azure classic portal](https://manage.windowsazure.com).</span></span>

1. <span data-ttu-id="cd417-236">Zaloguj się do [klasycznego portalu Azure](https://manage.windowsazure.com)</span><span class="sxs-lookup"><span data-stu-id="cd417-236">Sign in to the [Azure classic portal](https://manage.windowsazure.com)</span></span>
2. <span data-ttu-id="cd417-237">W panelu usługi Microsoft Azure, kliknij przycisk **UCZENIA MASZYNOWEGO**</span><span class="sxs-lookup"><span data-stu-id="cd417-237">In the Microsoft Azure services panel, click **MACHINE LEARNING**</span></span>
3. <span data-ttu-id="cd417-238">Kliknij obszar roboczy</span><span class="sxs-lookup"><span data-stu-id="cd417-238">Click your workspace</span></span>
4. <span data-ttu-id="cd417-239">Kliknij przycisk **usług sieci Web** kartę</span><span class="sxs-lookup"><span data-stu-id="cd417-239">Click the **Web services** tab</span></span>
5. <span data-ttu-id="cd417-240">Kliknij usługę sieci web, którą utworzyliśmy</span><span class="sxs-lookup"><span data-stu-id="cd417-240">Click the web service we created</span></span>
6. <span data-ttu-id="cd417-241">Kliknij punkt końcowy "domyślne"</span><span class="sxs-lookup"><span data-stu-id="cd417-241">Click the "default" endpoint</span></span>

<span data-ttu-id="cd417-242">W tym miejscu można wykonywać czynności takie, jak monitorować jak wykonywanie operacji usługi sieci web i ulepszeń wydajności upewnij, zmieniając liczby współbieżnych wywołań usługi może obsłużyć.</span><span class="sxs-lookup"><span data-stu-id="cd417-242">From here, you can do things like monitor how the web service is doing and make performance tweaks by changing how many concurrent calls the service can handle.</span></span>

<span data-ttu-id="cd417-243">Aby uzyskać więcej informacji, zobacz:</span><span class="sxs-lookup"><span data-stu-id="cd417-243">For more details, see:</span></span>

* [<span data-ttu-id="cd417-244">Tworzenie punktów końcowych</span><span class="sxs-lookup"><span data-stu-id="cd417-244">Creating Endpoints</span></span>](machine-learning-create-endpoint.md)
* [<span data-ttu-id="cd417-245">Skalowanie usługi sieci web</span><span class="sxs-lookup"><span data-stu-id="cd417-245">Scaling web service</span></span>](machine-learning-scaling-webservice.md)

### <a name="manage-a-classic-or-new-web-service-in-the-azure-machine-learning-web-services-portal"></a><span data-ttu-id="cd417-246">Zarządzanie Classic lub nową usługę sieci web w portalu usługi sieci Web systemu Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="cd417-246">Manage a Classic or New web service in the Azure Machine Learning Web Services portal</span></span>

<span data-ttu-id="cd417-247">Po wdrożeniu usługi sieci web, czy klasycznego lub nowe, można zarządzać nim z [usługi sieci Web Microsoft Azure Machine Learning](https://services.azureml.net/quickstart) portalu.</span><span class="sxs-lookup"><span data-stu-id="cd417-247">Once you've deployed your web service, whether Classic or New, you can manage it from the [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/quickstart) portal.</span></span>

<span data-ttu-id="cd417-248">Aby monitorować wydajność usługi sieci web:</span><span class="sxs-lookup"><span data-stu-id="cd417-248">To monitor the performance of your web service:</span></span>

1. <span data-ttu-id="cd417-249">Zaloguj się do [usługi sieci Web Microsoft Azure Machine Learning](https://services.azureml.net/quickstart) portalu</span><span class="sxs-lookup"><span data-stu-id="cd417-249">Sign in to the [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/quickstart) portal</span></span>
2. <span data-ttu-id="cd417-250">Kliknij przycisk **usług sieci Web**</span><span class="sxs-lookup"><span data-stu-id="cd417-250">Click **Web services**</span></span>
3. <span data-ttu-id="cd417-251">Kliknij opcję usługi sieci web</span><span class="sxs-lookup"><span data-stu-id="cd417-251">Click your web service</span></span>
4. <span data-ttu-id="cd417-252">Kliknij przycisk **pulpitu nawigacyjnego**</span><span class="sxs-lookup"><span data-stu-id="cd417-252">Click the **Dashboard**</span></span>

- - -
<span data-ttu-id="cd417-253">**Następnie: [dostęp do usługi sieci web](machine-learning-walkthrough-6-access-web-service.md)**</span><span class="sxs-lookup"><span data-stu-id="cd417-253">**Next: [Access the web service](machine-learning-walkthrough-6-access-web-service.md)**</span></span>

[3]: ./media/machine-learning-walkthrough-5-publish-web-service/publish3.png
[3a]: ./media/machine-learning-walkthrough-5-publish-web-service/publish3a.png
[4]: ./media/machine-learning-walkthrough-5-publish-web-service/publish4.png
[5]: ./media/machine-learning-walkthrough-5-publish-web-service/publish5.png
[6]: ./media/machine-learning-walkthrough-5-publish-web-service/publish6.png


<!-- Module References -->
[evaluate-model]: https://msdn.microsoft.com/library/azure/927d65ac-3b50-4694-9903-20f6c1672089/
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[metadata-editor]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[normalize-data]: https://msdn.microsoft.com/library/azure/986df333-6748-4b85-923d-871df70d6aaf/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
[two-class-boosted-decision-tree]: https://msdn.microsoft.com/library/azure/e3c522f8-53d9-4829-8ea4-5c6a6b75330c/
[two-class-support-vector-machine]: https://msdn.microsoft.com/library/azure/12d8479b-74b4-4e67-b8de-d32867380e20/
[project-columns]: https://msdn.microsoft.com/en-us/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
