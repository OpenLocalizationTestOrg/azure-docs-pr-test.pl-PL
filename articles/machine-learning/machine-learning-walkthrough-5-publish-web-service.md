---
title: "Krok 5: Wdrażanie usługi sieci web uczenie maszynowe hello | Dokumentacja firmy Microsoft"
description: "Krok 5 hello opracowanie wskazówki rozwiązanie predykcyjne: Wdrażanie eksperyment predykcyjny w usłudze Machine Learning Studio jako usługę sieci web."
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
ms.openlocfilehash: 76391010972ed1450bbda8bfb2352c7b22b51ccc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-5-deploy-hello-azure-machine-learning-web-service"></a><span data-ttu-id="3ff8b-103">Wskazówki krok 5: Wdrażanie usługi sieci web Azure Machine Learning hello</span><span class="sxs-lookup"><span data-stu-id="3ff8b-103">Walkthrough Step 5: Deploy hello Azure Machine Learning web service</span></span>
<span data-ttu-id="3ff8b-104">Jest hello krok piątym powitania przewodnika, [tworzenie rozwiązania analizy predykcyjnej w usłudze Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="3ff8b-104">This is hello fifth step of hello walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. [<span data-ttu-id="3ff8b-105">Tworzenie obszaru roboczego usługi Machine Learning</span><span class="sxs-lookup"><span data-stu-id="3ff8b-105">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="3ff8b-106">Przekazywanie istniejących danych</span><span class="sxs-lookup"><span data-stu-id="3ff8b-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="3ff8b-107">Tworzenie nowego eksperymentu</span><span class="sxs-lookup"><span data-stu-id="3ff8b-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="3ff8b-108">Nauczanie i Ewaluacja modeli hello</span><span class="sxs-lookup"><span data-stu-id="3ff8b-108">Train and evaluate hello models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. <span data-ttu-id="3ff8b-109">**Wdrażanie usługi sieci web hello**</span><span class="sxs-lookup"><span data-stu-id="3ff8b-109">**Deploy hello web service**</span></span>
6. [<span data-ttu-id="3ff8b-110">Usługa sieci web hello dostępu</span><span class="sxs-lookup"><span data-stu-id="3ff8b-110">Access hello web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<span data-ttu-id="3ff8b-111">toogive innych toouse szansy hello model predykcyjny opracowaliśmy w ramach tego przewodnika, możemy wdrożyć go jako usługę sieci web na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="3ff8b-111">toogive others a chance toouse hello predictive model we've developed in this walkthrough, we can deploy it as a web service on Azure.</span></span>

<span data-ttu-id="3ff8b-112">Zapasowej punktu toothis możemy były zmieniane uczenie modelu.</span><span class="sxs-lookup"><span data-stu-id="3ff8b-112">Up toothis point we've been experimenting with training our model.</span></span> <span data-ttu-id="3ff8b-113">Ale hello wdrożona usługa ma już szkolenia toodo — będzie prognoz nowe toogenerate przez oceniania danych wejściowych użytkownika hello oparte na modelu.</span><span class="sxs-lookup"><span data-stu-id="3ff8b-113">But hello deployed service is no longer going toodo training - it's going toogenerate new predictions by scoring hello user's input based on our model.</span></span> <span data-ttu-id="3ff8b-114">Dlatego chcemy toodo niektórych tooconvert przygotowania, to eksperymentować z ***szkolenia*** eksperymentu tooa ***predykcyjnej*** eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="3ff8b-114">So we're going toodo some preparation tooconvert this experiment from a ***training*** experiment tooa ***predictive*** experiment.</span></span> 

<span data-ttu-id="3ff8b-115">Jest to proces trzech etapów:</span><span class="sxs-lookup"><span data-stu-id="3ff8b-115">This is a three-step process:</span></span>  

1. <span data-ttu-id="3ff8b-116">Usuń jeden z modeli hello</span><span class="sxs-lookup"><span data-stu-id="3ff8b-116">Remove one of hello models</span></span>
2. <span data-ttu-id="3ff8b-117">Konwertuj hello *eksperyment uczenia* utworzyliśmy do *eksperyment predykcyjny*</span><span class="sxs-lookup"><span data-stu-id="3ff8b-117">Convert hello *training experiment* we've created into a *predictive experiment*</span></span>
3. <span data-ttu-id="3ff8b-118">Wdrażanie hello eksperyment predykcyjny jako usługę sieci web</span><span class="sxs-lookup"><span data-stu-id="3ff8b-118">Deploy hello predictive experiment as a web service</span></span>

## <a name="remove-one-of-hello-models"></a><span data-ttu-id="3ff8b-119">Usuń jeden z modeli hello</span><span class="sxs-lookup"><span data-stu-id="3ff8b-119">Remove one of hello models</span></span>

<span data-ttu-id="3ff8b-120">Najpierw należy tootrim tego eksperymentu w dół nieco.</span><span class="sxs-lookup"><span data-stu-id="3ff8b-120">First, we need tootrim this experiment down a little.</span></span> <span data-ttu-id="3ff8b-121">Obecnie istnieją dwa różne modele w eksperymencie hello, ale będą tylko jeden model toouse podczas możemy wdrożyć ją jako usługę sieci web.</span><span class="sxs-lookup"><span data-stu-id="3ff8b-121">We currently have two different models in hello experiment, but we only want toouse one model when we deploy this as a web service.</span></span>  

<span data-ttu-id="3ff8b-122">Załóżmy, że firma Microsoft decydujesz się tym hello boosted drzewa model działa lepiej niż hello SVM modelu.</span><span class="sxs-lookup"><span data-stu-id="3ff8b-122">Let's say we've decided that hello boosted tree model performed better than hello SVM model.</span></span> <span data-ttu-id="3ff8b-123">Dlatego hello pierwszy element toodo hello Usuń [maszyny wektorowa obsługa Two-Class] [ two-class-support-vector-machine] modułu i hello modułów, które były używane na potrzeby uczenia go.</span><span class="sxs-lookup"><span data-stu-id="3ff8b-123">So hello first thing toodo is remove hello [Two-Class Support Vector Machine][two-class-support-vector-machine] module and hello modules that were used for training it.</span></span> <span data-ttu-id="3ff8b-124">Może być toomake kopię eksperymentu hello najpierw klikając **Zapisz jako** u dołu hello hello eksperymentu kanwy.</span><span class="sxs-lookup"><span data-stu-id="3ff8b-124">You may want toomake a copy of hello experiment first by clicking **Save As** at hello bottom of hello experiment canvas.</span></span>

<span data-ttu-id="3ff8b-125">Potrzebujemy hello toodelete następujących modułów:</span><span class="sxs-lookup"><span data-stu-id="3ff8b-125">We need toodelete hello following modules:</span></span>  

* <span data-ttu-id="3ff8b-126">[Obsługa Two-Class wektor maszyny][two-class-support-vector-machine]</span><span class="sxs-lookup"><span data-stu-id="3ff8b-126">[Two-Class Support Vector Machine][two-class-support-vector-machine]</span></span>
* <span data-ttu-id="3ff8b-127">[Uczenie modelu] [ train-model] i [Score Model] [ score-model] modułów, które zostały połączone tooit</span><span class="sxs-lookup"><span data-stu-id="3ff8b-127">[Train Model][train-model] and [Score Model][score-model] modules that were connected tooit</span></span>
* <span data-ttu-id="3ff8b-128">[Normalizuj danych] [ normalize-data] (oba)</span><span class="sxs-lookup"><span data-stu-id="3ff8b-128">[Normalize Data][normalize-data] (both of them)</span></span>
* <span data-ttu-id="3ff8b-129">[Ocena modelu] [ evaluate-model] (ponieważ jesteśmy zakończono ocenę modeli hello)</span><span class="sxs-lookup"><span data-stu-id="3ff8b-129">[Evaluate Model][evaluate-model] (because we're finished evaluating hello models)</span></span>

<span data-ttu-id="3ff8b-130">Wybierz każdego modułu i naciśnij klawisz Delete hello lub moduł powitania kliknij prawym przyciskiem myszy i wybierz **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="3ff8b-130">Select each module and press hello Delete key, or right-click hello module and select **Delete**.</span></span> 

![Usunięte hello SVM modelu][3a]

<span data-ttu-id="3ff8b-132">Nasz model powinien teraz wyglądać mniej więcej tak:</span><span class="sxs-lookup"><span data-stu-id="3ff8b-132">Our model should now look something like this:</span></span>

![Usunięte hello SVM modelu][3]

<span data-ttu-id="3ff8b-134">Teraz jest gotowy toodeploy model to przy użyciu hello [Two-Class Boosted drzewa decyzyjnego][two-class-boosted-decision-tree].</span><span class="sxs-lookup"><span data-stu-id="3ff8b-134">Now we're ready toodeploy this model using hello [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree].</span></span>

## <a name="convert-hello-training-experiment-tooa-predictive-experiment"></a><span data-ttu-id="3ff8b-135">Konwertuj eksperyment predykcyjny tooa hello szkolenia eksperymentu</span><span class="sxs-lookup"><span data-stu-id="3ff8b-135">Convert hello training experiment tooa predictive experiment</span></span>

<span data-ttu-id="3ff8b-136">tooget to modelu gotowe do wdrożenia, potrzebujemy tooconvert to szkolenia eksperyment predykcyjny tooa eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="3ff8b-136">tooget this model ready for deployment, we need tooconvert this training experiment tooa predictive experiment.</span></span> <span data-ttu-id="3ff8b-137">Obejmuje to trzy kroki:</span><span class="sxs-lookup"><span data-stu-id="3ff8b-137">This involves three steps:</span></span>

1. <span data-ttu-id="3ff8b-138">Zapisz model hello możemy gdy udało się nauczyć, a następnie zastąp naszych modułów szkoleniowych</span><span class="sxs-lookup"><span data-stu-id="3ff8b-138">Save hello model we've trained and then replace our training modules</span></span>
2. <span data-ttu-id="3ff8b-139">TRIM hello eksperymentu tooremove modułów, które były potrzebne tylko w przypadku szkolenia</span><span class="sxs-lookup"><span data-stu-id="3ff8b-139">Trim hello experiment tooremove modules that were only needed for training</span></span>
3. <span data-ttu-id="3ff8b-140">Zdefiniuj gdzie hello usługi sieci web będzie akceptować dane wejściowe i gdzie generuje dane wyjściowe hello</span><span class="sxs-lookup"><span data-stu-id="3ff8b-140">Define where hello web service will accept input and where it generates hello output</span></span>

<span data-ttu-id="3ff8b-141">Firma Microsoft może to zrobić ręcznie, ale na szczęście wszystkie trzy kroki można wykonać, klikając **ustawić usługę sieci Web** u dołu hello kanwy eksperymentu hello (i wybierając hello **predykcyjnej usługi sieci Web** Opcja).</span><span class="sxs-lookup"><span data-stu-id="3ff8b-141">We could do this manually, but fortunately all three steps can be accomplished by clicking **Set Up Web Service** at hello bottom of hello experiment canvas (and selecting hello **Predictive Web Service** option).</span></span>

> [!TIP]
> <span data-ttu-id="3ff8b-142">Jeśli chcesz bardziej szczegółowe informacje na, co się stanie po przekonwertowaniu tooa eksperymentu uczenia predykcyjnej eksperymentu, zobacz [jak tooprepare modelu do wdrożenia w usłudze Azure Machine Learning Studio](machine-learning-convert-training-experiment-to-scoring-experiment.md).</span><span class="sxs-lookup"><span data-stu-id="3ff8b-142">If you want more details on what happens when you convert a training experiment tooa predictive experiment, see [How tooprepare your model for deployment in Azure Machine Learning Studio](machine-learning-convert-training-experiment-to-scoring-experiment.md).</span></span>

<span data-ttu-id="3ff8b-143">Po kliknięciu **ustawić usługę sieci Web**, ma miejsce kilka rzeczy:</span><span class="sxs-lookup"><span data-stu-id="3ff8b-143">When you click **Set Up Web Service**, several things happen:</span></span>

* <span data-ttu-id="3ff8b-144">Hello uczonego modelu jest przekonwertowanego tooa pojedynczego **Uczonego modelu** modułu i przechowywane w toohello palety modułu hello lewej hello kanwy eksperymentu (można znaleźć go w **przeszkolone modele**)</span><span class="sxs-lookup"><span data-stu-id="3ff8b-144">hello trained model is converted tooa single **Trained Model** module and stored in hello module palette toohello left of hello experiment canvas (you can find it under **Trained Models**)</span></span>
* <span data-ttu-id="3ff8b-145">Moduły, które były używane do trenowania zostaną usunięte; w szczególności:</span><span class="sxs-lookup"><span data-stu-id="3ff8b-145">Modules that were used for training are removed; specifically:</span></span>
  * <span data-ttu-id="3ff8b-146">[Two-Class Boosted algorytm][two-class-boosted-decision-tree]</span><span class="sxs-lookup"><span data-stu-id="3ff8b-146">[Two-Class Boosted Decision Tree][two-class-boosted-decision-tree]</span></span>
  * <span data-ttu-id="3ff8b-147">[Train Model][train-model]</span><span class="sxs-lookup"><span data-stu-id="3ff8b-147">[Train Model][train-model]</span></span>
  * <span data-ttu-id="3ff8b-148">[Podział danych][split]</span><span class="sxs-lookup"><span data-stu-id="3ff8b-148">[Split Data][split]</span></span>
  * <span data-ttu-id="3ff8b-149">Witaj drugi [wykonanie skryptu języka R] [ execute-r-script] moduł, który był używany dla danych testowych</span><span class="sxs-lookup"><span data-stu-id="3ff8b-149">hello second [Execute R Script][execute-r-script] module that was used for test data</span></span>
* <span data-ttu-id="3ff8b-150">Hello zapisane uczonego modelu zostanie dodany do eksperymentu hello</span><span class="sxs-lookup"><span data-stu-id="3ff8b-150">hello saved trained model is added back into hello experiment</span></span>
* <span data-ttu-id="3ff8b-151">**Usługi danych wejściowych w sieci Web** i **sieci Web usług** moduły są dodawane (te informacje pozwalają określić gdzie wprowadzić dane użytkownika hello hello modelu i jakie dane są zwracane podczas uzyskiwania dostępu do usługi sieci web hello)</span><span class="sxs-lookup"><span data-stu-id="3ff8b-151">**Web service input** and **Web service output** modules are added (these identify where hello user's data will enter hello model, and what data is returned, when hello web service is accessed)</span></span>

> [!NOTE]
> <span data-ttu-id="3ff8b-152">Widać, że hello eksperyment został zapisany w dwóch częściach na kartach dodanych u góry hello kanwy eksperymentu hello.</span><span class="sxs-lookup"><span data-stu-id="3ff8b-152">You can see that hello experiment is saved in two parts under tabs that have been added at hello top of hello experiment canvas.</span></span> <span data-ttu-id="3ff8b-153">Witaj oryginalnego eksperyment uczenia jest karcie hello **eksperyment uczenia**, i podlega hello nowo utworzony eksperyment predykcyjny **eksperyment predykcyjny**.</span><span class="sxs-lookup"><span data-stu-id="3ff8b-153">hello original training experiment is under hello tab **Training experiment**, and hello newly created predictive experiment is under **Predictive experiment**.</span></span> <span data-ttu-id="3ff8b-154">eksperyment predykcyjny Hello jest hello jedną, które firma Microsoft będzie wdrożyć jako usługę sieci web.</span><span class="sxs-lookup"><span data-stu-id="3ff8b-154">hello predictive experiment is hello one we'll deploy as a web service.</span></span>

<span data-ttu-id="3ff8b-155">Potrzebujemy tootake jednego dodatkowego kroku z tego konkretnego eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="3ff8b-155">We need tootake one additional step with this particular experiment.</span></span>
<span data-ttu-id="3ff8b-156">Dodaliśmy dwie [wykonanie skryptu języka R] [ execute-r-script] tooprovide modułów wagi funkcji toohello danych.</span><span class="sxs-lookup"><span data-stu-id="3ff8b-156">We added two [Execute R Script][execute-r-script] modules tooprovide a weighting function toohello data.</span></span> <span data-ttu-id="3ff8b-157">Po prostu lewy, czego potrzeba do uczenie i testowanie, który został, firma Microsoft może zająć się tych modułów w hello ostatecznego modelu.</span><span class="sxs-lookup"><span data-stu-id="3ff8b-157">That was just a trick we needed for training and testing, so we can take out those modules in hello final model.</span></span>
<span data-ttu-id="3ff8b-158">Usługa Machine Learning Studio usunąć jedną [wykonanie skryptu języka R] [ execute-r-script] modułu usunięcie hello [podziału] [ split] modułu.</span><span class="sxs-lookup"><span data-stu-id="3ff8b-158">Machine Learning Studio removed one [Execute R Script][execute-r-script] module when it removed hello [Split][split] module.</span></span> <span data-ttu-id="3ff8b-159">Teraz można usunąć hello innych i połącz [Edytor metadanych] [ metadata-editor] bezpośrednio za[Score Model][score-model].</span><span class="sxs-lookup"><span data-stu-id="3ff8b-159">Now we can remove hello other and connect [Metadata Editor][metadata-editor] directly too[Score Model][score-model].</span></span>    

<span data-ttu-id="3ff8b-160">Naszym doświadczeniu powinna wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="3ff8b-160">Our experiment should now look like this:</span></span>  

![Oceniania hello trenowanego modelu.][4]  

> [!NOTE]
> <span data-ttu-id="3ff8b-162">Możesz się zastanawiać, dlaczego możemy left hello danych karty kredytowej niemiecki UCI dataset w eksperyment predykcyjny hello.</span><span class="sxs-lookup"><span data-stu-id="3ff8b-162">You may be wondering why we left hello UCI German Credit Card Data dataset in hello predictive experiment.</span></span> <span data-ttu-id="3ff8b-163">Usługa Hello przechodzi tooscore hello danych użytkownika, nie hello oryginalnego zestawu danych, więc Dlaczego pozostaw hello oryginalnego zestawu danych w modelu hello?</span><span class="sxs-lookup"><span data-stu-id="3ff8b-163">hello service is going tooscore hello user's data, not hello original dataset, so why leave hello original dataset in hello model?</span></span>
> 
> <span data-ttu-id="3ff8b-164">Jest PRAWDA, nie wymagają hello oryginalnych danych karty kredytowej hello usługi.</span><span class="sxs-lookup"><span data-stu-id="3ff8b-164">It's true that hello service doesn't need hello original credit card data.</span></span> <span data-ttu-id="3ff8b-165">Jednak musi hello schematu dla danych, które obejmują takie informacje jak liczbę kolumn są i kolumny, które są liczbowych.</span><span class="sxs-lookup"><span data-stu-id="3ff8b-165">But it does need hello schema for that data, which includes information such as how many columns there are and which columns are numeric.</span></span> <span data-ttu-id="3ff8b-166">Informacje o schemacie jest konieczne toointerpret hello danych użytkownika.</span><span class="sxs-lookup"><span data-stu-id="3ff8b-166">This schema information is necessary toointerpret hello user's data.</span></span> <span data-ttu-id="3ff8b-167">Firma Microsoft pozostawić te składniki, połączony, dzięki czemu hello oceniania moduł ma hello schemat zestawu danych podczas hello usługa jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="3ff8b-167">We leave these components connected so that hello scoring module has hello dataset schema when hello service is running.</span></span> <span data-ttu-id="3ff8b-168">Witaj danych nie jest używana, tylko hello schematu.</span><span class="sxs-lookup"><span data-stu-id="3ff8b-168">hello data isn't used, just hello schema.</span></span>  
> 
> 

<span data-ttu-id="3ff8b-169">Uruchom eksperyment hello raz ostatni (kliknij **Uruchom**.) Nadal działa tooverify, który hello modelu, kliknij przycisk dane wyjściowe hello hello [Score Model] [ score-model] moduł i zaznacz **wyświetlanie wyników**.</span><span class="sxs-lookup"><span data-stu-id="3ff8b-169">Run hello experiment one last time (click **Run**.) If you want tooverify that hello model is still working, click hello output of hello [Score Model][score-model] module and select **View Results**.</span></span> <span data-ttu-id="3ff8b-170">Widać, że oryginalne dane hello zostanie wyświetlona, wraz z hello środki ryzyka wartość ("oceniane etykiety") i hello oceniania wartość prawdopodobieństwa ("wynik prawdopodobieństwa".)</span><span class="sxs-lookup"><span data-stu-id="3ff8b-170">You can see that hello original data is displayed, along with hello credit risk value ("Scored Labels") and hello scoring probability value ("Scored Probabilities".)</span></span> 

## <a name="deploy-hello-web-service"></a><span data-ttu-id="3ff8b-171">Wdrażanie usługi sieci web hello</span><span class="sxs-lookup"><span data-stu-id="3ff8b-171">Deploy hello web service</span></span>
<span data-ttu-id="3ff8b-172">Hello eksperymentu można wdrożyć jako albo klasycznym usługi sieci web, lub Nowa usługa sieci web, która jest oparta na usłudze Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="3ff8b-172">You can deploy hello experiment as either a Classic web service, or as a New web service that's based on Azure Resource Manager.</span></span>

### <a name="deploy-as-a-classic-web-service"></a><span data-ttu-id="3ff8b-173">Wdrożyć jako usługę sieci web klasycznego</span><span class="sxs-lookup"><span data-stu-id="3ff8b-173">Deploy as a Classic web service</span></span>
<span data-ttu-id="3ff8b-174">Kliknij toodeploy pochodzące z naszych eksperymentu usługi sieci web Klasyczny **wdrażanie usługi sieci Web** poniżej hello obszar roboczy i wybierz **wdrażanie usługi sieci Web [klasyczny]**.</span><span class="sxs-lookup"><span data-stu-id="3ff8b-174">toodeploy a Classic web service derived from our experiment, click **Deploy Web Service** below hello canvas and select **Deploy Web Service [Classic]**.</span></span> <span data-ttu-id="3ff8b-175">Usługa Machine Learning Studio wdraża hello eksperymentu jako usługę sieci web i przejście pulpitu nawigacyjnego toohello dla tej usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="3ff8b-175">Machine Learning Studio deploys hello experiment as a web service and takes you toohello dashboard for that web service.</span></span> <span data-ttu-id="3ff8b-176">Na tej stronie można zwrócić eksperymentu toohello (**widoku migawki** lub **wyświetlić najnowszych**) i uruchamianie testu prostego powitania usługi sieci web (zobacz **testowanie usługi sieci web hello** poniżej).</span><span class="sxs-lookup"><span data-stu-id="3ff8b-176">From this page you can return toohello experiment (**View snapshot** or **View latest**) and run a simple test of hello web service (see **Test hello web service** below).</span></span> <span data-ttu-id="3ff8b-177">Istnieje również tutaj informacje dotyczące tworzenia aplikacji, które mogą uzyskiwać dostęp do usługi sieci web hello (omówiona w następnym kroku hello tego przewodnika).</span><span class="sxs-lookup"><span data-stu-id="3ff8b-177">There is also information here for creating applications that can access hello web service (more on that in hello next step of this walkthrough).</span></span>

![Pulpit nawigacyjny usługi sieci Web][6]

<span data-ttu-id="3ff8b-179">Można skonfigurować usługę hello klikając hello **konfiguracji** kartę. W tym miejscu można zmodyfikować hello nazwy usługi (jest nazwę eksperymentu danego hello domyślnie) i nadaj mu opis.</span><span class="sxs-lookup"><span data-stu-id="3ff8b-179">You can configure hello service by clicking hello **CONFIGURATION** tab. Here you can modify hello service name (it's given hello experiment name by default) and give it a description.</span></span> <span data-ttu-id="3ff8b-180">Możesz też udzielić większej liczby etykiet przyjazną dla hello danych wejściowych i wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="3ff8b-180">You can also give more friendly labels for hello input and output data.</span></span>  

![Konfiguruj usługę sieci web hello][5]  

### <a name="deploy-as-a-new-web-service"></a><span data-ttu-id="3ff8b-182">Wdrożyć jako nową usługę sieci web</span><span class="sxs-lookup"><span data-stu-id="3ff8b-182">Deploy as a New web service</span></span>

> [!NOTE] 
> <span data-ttu-id="3ff8b-183">toodeploy nową usługę sieci web, należy posiadać odpowiednie uprawnienia w hello toowhich subskrypcji, które wdrażasz hello usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="3ff8b-183">toodeploy a New web service you must have sufficient permissions in hello subscription toowhich you are deploying hello web service.</span></span> <span data-ttu-id="3ff8b-184">Aby uzyskać więcej informacji, zobacz [zarządzania usługi sieci web przy użyciu portalu usługi sieci Web systemu Azure Machine Learning hello](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="3ff8b-184">For more information, see [Manage a web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="3ff8b-185">toodeploy nową usługę sieci web pochodzące z naszym doświadczeniu:</span><span class="sxs-lookup"><span data-stu-id="3ff8b-185">toodeploy a New web service derived from our experiment:</span></span>

1. <span data-ttu-id="3ff8b-186">Kliknij przycisk **wdrażanie usługi sieci Web** poniżej hello obszar roboczy i wybierz **wdrażanie usługi sieci Web [New]**.</span><span class="sxs-lookup"><span data-stu-id="3ff8b-186">Click **Deploy Web Service** below hello canvas and select **Deploy Web Service [New]**.</span></span> <span data-ttu-id="3ff8b-187">Usługa Machine Learning Studio transfery usługi sieci web Azure Machine Learning toohello **wdrażanie eksperymentu** strony.</span><span class="sxs-lookup"><span data-stu-id="3ff8b-187">Machine Learning Studio transfers you toohello Azure Machine Learning web services **Deploy Experiment** page.</span></span>

2. <span data-ttu-id="3ff8b-188">Wprowadź nazwę usługi sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="3ff8b-188">Enter a name for hello web service.</span></span> 

3. <span data-ttu-id="3ff8b-189">Aby uzyskać **planu cen**, można wybrać planu cenowego istniejących lub wybierz opcję "Utwórz nowe" i podać hello nowego planu nazwę i wybierz hello miesięczne opcji plan.</span><span class="sxs-lookup"><span data-stu-id="3ff8b-189">For **Price Plan**, you can select an existing pricing plan, or select "Create new" and give hello new plan a name and select hello monthly plan option.</span></span> <span data-ttu-id="3ff8b-190">plan Hello się, że warstw domyślne plany toohello Twojego domyślnego regionu i usługi sieci web jest wdrożone toothat regionu.</span><span class="sxs-lookup"><span data-stu-id="3ff8b-190">hello plan tiers default toohello plans for your default region and your web service is deployed toothat region.</span></span>

4. <span data-ttu-id="3ff8b-191">Kliknij przycisk **wdrażanie**.</span><span class="sxs-lookup"><span data-stu-id="3ff8b-191">Click **Deploy**.</span></span>

<span data-ttu-id="3ff8b-192">Po kilku minutach hello **szybkiego startu** zostanie otwarta strona dla usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="3ff8b-192">After a few minutes, hello **Quickstart** page for your web service opens.</span></span>

<span data-ttu-id="3ff8b-193">Można skonfigurować usługę hello klikając hello **Konfiguruj** kartę. W tym miejscu można zmodyfikować usługi hello tytuł i nadaj mu opis.</span><span class="sxs-lookup"><span data-stu-id="3ff8b-193">You can configure hello service by clicking hello **Configure** tab. Here you can modify hello service title and give it a description.</span></span> 

<span data-ttu-id="3ff8b-194">tootest hello usługi sieci web, kliknij przycisk hello **testu** kartę (zobacz **testowanie usługi sieci web hello** poniżej).</span><span class="sxs-lookup"><span data-stu-id="3ff8b-194">tootest hello web service, click hello **Test** tab (see **Test hello web service** below).</span></span> <span data-ttu-id="3ff8b-195">Informacje dotyczące tworzenia aplikacji, które mogą uzyskiwać dostęp do usługi sieci web hello, kliknij przycisk hello **Consume** kartę (hello następnego kroku w tym przewodniku zostaną umieszczone w bardziej szczegółowo).</span><span class="sxs-lookup"><span data-stu-id="3ff8b-195">For information on creating applications that can access hello web service, click hello **Consume** tab (hello next step in this walkthrough will go into more detail).</span></span>

> [!TIP]
> <span data-ttu-id="3ff8b-196">Po jej wdrożeniu można aktualizować hello usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="3ff8b-196">You can update hello web service after you've deployed it.</span></span> <span data-ttu-id="3ff8b-197">Na przykład, jeśli chcesz toochange modelu, następnie należy można edytować eksperyment uczenia hello, dostosować parametry modelu hello i kliknij przycisk **wdrażanie usługi sieci Web**, wybierając żądane **wdrażanie usługi sieci Web [klasyczny]** lub  **Wdrażanie usługi sieci Web [New]**.</span><span class="sxs-lookup"><span data-stu-id="3ff8b-197">For example, if you want toochange your model, then you can edit hello training experiment, tweak hello model parameters, and click **Deploy Web Service**, selecting **Deploy Web Service [Classic]** or **Deploy Web Service [New]**.</span></span> <span data-ttu-id="3ff8b-198">Wdrażając hello eksperyment ponownie, zastępuje hello usługi sieci web, teraz, używając zaktualizowanych modelu.</span><span class="sxs-lookup"><span data-stu-id="3ff8b-198">When you deploy hello experiment again, it replaces hello web service, now using your updated model.</span></span>  
> 
> 

## <a name="test-hello-web-service"></a><span data-ttu-id="3ff8b-199">Usługa sieci web hello testu</span><span class="sxs-lookup"><span data-stu-id="3ff8b-199">Test hello web service</span></span>

<span data-ttu-id="3ff8b-200">Podczas uzyskiwania dostępu do usługi sieci web hello dane użytkownika hello przechodzi przez hello **sieci Web dane wejściowe usługi** modułu, w którym przekazany toohello [Score Model] [ score-model] modułu i oceniane.</span><span class="sxs-lookup"><span data-stu-id="3ff8b-200">When hello web service is accessed, hello user's data enters through hello **Web service input** module where it's passed toohello [Score Model][score-model] module and scored.</span></span> <span data-ttu-id="3ff8b-201">sposób Hello skonfigurowaliśmy eksperyment predykcyjny hello, hello model oczekuje danych w hello takie same w formacie zestawu danych hello oryginalnego środki ryzyka.</span><span class="sxs-lookup"><span data-stu-id="3ff8b-201">hello way we've set up hello predictive experiment, hello model expects data in hello same format as hello original credit risk dataset.</span></span>
<span data-ttu-id="3ff8b-202">Hello są zwracane wyniki toohello użytkownika z hello usługi sieci web za pośrednictwem hello **sieci Web usług** modułu.</span><span class="sxs-lookup"><span data-stu-id="3ff8b-202">hello results are returned toohello user from hello web service through hello **Web service output** module.</span></span>

> [!TIP]
> <span data-ttu-id="3ff8b-203">sposób Hello mamy hello eksperyment predykcyjny skonfigurowane, hello całego wynikiem hello [Score Model] [ score-model] modułu są zwracane.</span><span class="sxs-lookup"><span data-stu-id="3ff8b-203">hello way we have hello predictive experiment configured, hello entire results from hello [Score Model][score-model] module are returned.</span></span> <span data-ttu-id="3ff8b-204">W tym wszystkich danych wejściowych hello oraz wartość ryzyko kredytowe hello i hello oceniania prawdopodobieństwa.</span><span class="sxs-lookup"><span data-stu-id="3ff8b-204">This includes all hello input data plus hello credit risk value and hello scoring probability.</span></span> <span data-ttu-id="3ff8b-205">Ale może inny zwracać — na przykład można zwrócić tylko hello wartość ryzyko kredytowe.</span><span class="sxs-lookup"><span data-stu-id="3ff8b-205">But you can return something different if you want - for example, you could return just hello credit risk value.</span></span> <span data-ttu-id="3ff8b-206">toodo, Wstaw [kolumny projektu] [ project-columns] modułu między [Score Model] [ score-model] i hello **sieci Web produktu** nie ma kolumn tooeliminate hello tooreturn usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="3ff8b-206">toodo this, insert a [Project Columns][project-columns] module between [Score Model][score-model] and hello **Web service output** tooeliminate columns you don't want hello web service tooreturn.</span></span> 
> 
> 

<span data-ttu-id="3ff8b-207">Można przetestować web klasycznym usługi w **Machine Learning Studio** lub hello **usługi sieci Web systemu Azure Machine Learning** portalu.</span><span class="sxs-lookup"><span data-stu-id="3ff8b-207">You can test a Classic web service either in **Machine Learning Studio** or in hello **Azure Machine Learning Web Services** portal.</span></span>
<span data-ttu-id="3ff8b-208">Możesz przetestować nową usługę sieci web tylko w hello **usługi sieci Web usługi Machine Learning** portalu.</span><span class="sxs-lookup"><span data-stu-id="3ff8b-208">You can test a New web service only in hello **Machine Learning Web Services** portal.</span></span>

> [!TIP]
> <span data-ttu-id="3ff8b-209">Podczas testowania, w portalu usługi sieci Web systemu Azure Machine Learning hello, może mieć portalu hello Utwórz dane przykładowe służy tootest hello żądań i odpowiedzi usługi.</span><span class="sxs-lookup"><span data-stu-id="3ff8b-209">When testing in hello Azure Machine Learning Web Services portal, you can have hello portal create sample data that you can use tootest hello Request-Response service.</span></span> <span data-ttu-id="3ff8b-210">Na powitania **Konfiguruj** wybierz przycisk Tak, aby uzyskać **przykładowych danych włączone?**.</span><span class="sxs-lookup"><span data-stu-id="3ff8b-210">On hello **Configure** page, select "Yes" for **Sample Data Enabled?**.</span></span> <span data-ttu-id="3ff8b-211">Po otwarciu karty hello żądań i odpowiedzi na powitania **testu** strony portalu hello wypełnia przykładowych danych z zestawu danych hello oryginalnego środki ryzyka.</span><span class="sxs-lookup"><span data-stu-id="3ff8b-211">When you open hello Request-Response tab on hello **Test** page, hello portal fills in sample data taken from hello original credit risk dataset.</span></span>

### <a name="test-a-classic-web-service"></a><span data-ttu-id="3ff8b-212">Testowanie usługi sieci web klasycznego</span><span class="sxs-lookup"><span data-stu-id="3ff8b-212">Test a Classic web service</span></span>

<span data-ttu-id="3ff8b-213">W usłudze Machine Learning Studio lub w portalu usługi sieci Web usługi Machine Learning hello można testować usługi sieci web klasycznego.</span><span class="sxs-lookup"><span data-stu-id="3ff8b-213">You can test a Classic web service in Machine Learning Studio or in hello Machine Learning Web Services portal.</span></span> 

#### <a name="test-in-machine-learning-studio"></a><span data-ttu-id="3ff8b-214">Testowanie w usłudze Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="3ff8b-214">Test in Machine Learning Studio</span></span>

1. <span data-ttu-id="3ff8b-215">Na powitania **pulpitu NAWIGACYJNEGO** usługi sieci web powitania kliknij pozycję hello **testu** przycisku w obszarze **domyślny punkt końcowy**.</span><span class="sxs-lookup"><span data-stu-id="3ff8b-215">On hello **DASHBOARD** page for hello web service, click hello **Test** button under **Default Endpoint**.</span></span> <span data-ttu-id="3ff8b-216">Okno dialogowe wyskakującej i monituje o dane wejściowe hello hello usługi.</span><span class="sxs-lookup"><span data-stu-id="3ff8b-216">A dialog pops up and asks you for hello input data for hello service.</span></span> <span data-ttu-id="3ff8b-217">Te są hello tej samej kolumny, które znajdowały się w zestawie danych hello oryginalnego środki ryzyka.</span><span class="sxs-lookup"><span data-stu-id="3ff8b-217">These are hello same columns that appeared in hello original credit risk dataset.</span></span>  

2. <span data-ttu-id="3ff8b-218">Wprowadź zestaw danych, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="3ff8b-218">Enter a set of data and then click **OK**.</span></span> 

#### <a name="test-in-hello-machine-learning-web-services-portal"></a><span data-ttu-id="3ff8b-219">Testowanie w portalu usługi sieci Web usługi Machine Learning hello</span><span class="sxs-lookup"><span data-stu-id="3ff8b-219">Test in hello Machine Learning Web Services portal</span></span>

1. <span data-ttu-id="3ff8b-220">Na powitania **pulpitu NAWIGACYJNEGO** usługi sieci web powitania kliknij pozycję hello **Podgląd testów** łącze w obszarze **domyślny punkt końcowy**.</span><span class="sxs-lookup"><span data-stu-id="3ff8b-220">On hello **DASHBOARD** page for hello web service, click hello **Test preview** link under **Default Endpoint**.</span></span> <span data-ttu-id="3ff8b-221">Strona testowa Hello w portalu usługi sieci Web systemu Azure Machine Learning hello punktu końcowego usługi sieci web hello otwiera i monituje o dane wejściowe hello hello usługi.</span><span class="sxs-lookup"><span data-stu-id="3ff8b-221">hello test page in hello Azure Machine Learning Web Services portal for hello web service endpoint opens and asks you for hello input data for hello service.</span></span> <span data-ttu-id="3ff8b-222">Te są hello tej samej kolumny, które znajdowały się w zestawie danych hello oryginalnego środki ryzyka.</span><span class="sxs-lookup"><span data-stu-id="3ff8b-222">These are hello same columns that appeared in hello original credit risk dataset.</span></span>

2. <span data-ttu-id="3ff8b-223">Kliknij przycisk **Test żądań i odpowiedzi**.</span><span class="sxs-lookup"><span data-stu-id="3ff8b-223">Click **Test Request-Response**.</span></span> 

### <a name="test-a-new-web-service"></a><span data-ttu-id="3ff8b-224">Przetestować nową usługę sieci web</span><span class="sxs-lookup"><span data-stu-id="3ff8b-224">Test a New web service</span></span>

<span data-ttu-id="3ff8b-225">Tylko w portalu usługi sieci Web usługi Machine Learning hello można przetestować nową usługę sieci web.</span><span class="sxs-lookup"><span data-stu-id="3ff8b-225">You can test a New web service only in hello Machine Learning Web Services portal.</span></span>

1. <span data-ttu-id="3ff8b-226">W hello [usługi sieci Web systemu Azure Machine Learning](https://services.azureml.net/quickstart) portalu, kliknij przycisk **testu** u góry hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="3ff8b-226">In hello [Azure Machine Learning Web Services](https://services.azureml.net/quickstart) portal, click **Test** at hello top of hello page.</span></span> <span data-ttu-id="3ff8b-227">Witaj **testu** zostanie otwarta strona i można wprowadzić dane dotyczące hello usługi.</span><span class="sxs-lookup"><span data-stu-id="3ff8b-227">hello **Test** page opens and you can input data for hello service.</span></span> <span data-ttu-id="3ff8b-228">Hello pól wejściowych wyświetlane odpowiada toohello kolumn, które znajdowały się w zestawie danych hello oryginalnego środki ryzyka.</span><span class="sxs-lookup"><span data-stu-id="3ff8b-228">hello input fields displayed correspond toohello columns that appeared in hello original credit risk dataset.</span></span> 

2. <span data-ttu-id="3ff8b-229">Wprowadź zestaw danych, a następnie kliknij przycisk **testu żądanie-odpowiedź**.</span><span class="sxs-lookup"><span data-stu-id="3ff8b-229">Enter a set of data and then click **Test Request-Response**.</span></span>

<span data-ttu-id="3ff8b-230">Witaj wyniki testu hello są wyświetlane na hello prawej strony hello hello kolumny wyjściowej.</span><span class="sxs-lookup"><span data-stu-id="3ff8b-230">hello results of hello test are displayed on hello right-hand side of hello page in hello output column.</span></span> 


## <a name="manage-hello-web-service"></a><span data-ttu-id="3ff8b-231">Zarządzanie usługą sieci web hello</span><span class="sxs-lookup"><span data-stu-id="3ff8b-231">Manage hello web service</span></span>

### <a name="manage-a-classic-web-service-in-hello-azure-classic-portal"></a><span data-ttu-id="3ff8b-232">Zarządzanie usługą sieci web klasycznego w hello klasycznego portalu Azure</span><span class="sxs-lookup"><span data-stu-id="3ff8b-232">Manage a Classic web service in hello Azure classic portal</span></span>

<span data-ttu-id="3ff8b-233">Po wdrożeniu usługi sieci web klasycznego, można było zarządzać nim z hello [klasycznego portalu Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="3ff8b-233">Once you've deployed your Classic web service, you can manage it from hello [Azure classic portal](https://manage.windowsazure.com).</span></span>

1. <span data-ttu-id="3ff8b-234">Zaloguj się toohello [klasycznego portalu Azure](https://manage.windowsazure.com)</span><span class="sxs-lookup"><span data-stu-id="3ff8b-234">Sign in toohello [Azure classic portal](https://manage.windowsazure.com)</span></span>
2. <span data-ttu-id="3ff8b-235">Witaj Panel usługi Microsoft Azure, kliknij przycisk **UCZENIA MASZYNOWEGO**</span><span class="sxs-lookup"><span data-stu-id="3ff8b-235">In hello Microsoft Azure services panel, click **MACHINE LEARNING**</span></span>
3. <span data-ttu-id="3ff8b-236">Kliknij obszar roboczy</span><span class="sxs-lookup"><span data-stu-id="3ff8b-236">Click your workspace</span></span>
4. <span data-ttu-id="3ff8b-237">Kliknij przycisk hello **usług sieci Web** kartę</span><span class="sxs-lookup"><span data-stu-id="3ff8b-237">Click hello **Web services** tab</span></span>
5. <span data-ttu-id="3ff8b-238">Kliknij opcję usługi sieci web hello utworzyliśmy</span><span class="sxs-lookup"><span data-stu-id="3ff8b-238">Click hello web service we created</span></span>
6. <span data-ttu-id="3ff8b-239">Kliknij punkt końcowy "domyślne" hello</span><span class="sxs-lookup"><span data-stu-id="3ff8b-239">Click hello "default" endpoint</span></span>

<span data-ttu-id="3ff8b-240">W tym miejscu można wykonywać czynności, takie jak monitorowanie, jak robi hello usługi sieci web i upewnij ulepszeń wydajności przez zmianę liczby równoczesnych wywołań hello usługi może obsłużyć.</span><span class="sxs-lookup"><span data-stu-id="3ff8b-240">From here, you can do things like monitor how hello web service is doing and make performance tweaks by changing how many concurrent calls hello service can handle.</span></span>

<span data-ttu-id="3ff8b-241">Aby uzyskać więcej informacji, zobacz:</span><span class="sxs-lookup"><span data-stu-id="3ff8b-241">For more details, see:</span></span>

* [<span data-ttu-id="3ff8b-242">Tworzenie punktów końcowych</span><span class="sxs-lookup"><span data-stu-id="3ff8b-242">Creating Endpoints</span></span>](machine-learning-create-endpoint.md)
* [<span data-ttu-id="3ff8b-243">Skalowanie usługi sieci web</span><span class="sxs-lookup"><span data-stu-id="3ff8b-243">Scaling web service</span></span>](machine-learning-scaling-webservice.md)

### <a name="manage-a-classic-or-new-web-service-in-hello-azure-machine-learning-web-services-portal"></a><span data-ttu-id="3ff8b-244">Zarządzanie Classic lub nową usługę sieci web w portalu usługi sieci Web systemu Azure Machine Learning hello</span><span class="sxs-lookup"><span data-stu-id="3ff8b-244">Manage a Classic or New web service in hello Azure Machine Learning Web Services portal</span></span>

<span data-ttu-id="3ff8b-245">Po wdrożeniu usługi sieci web, czy klasycznego lub nowe, można było zarządzać nim z hello [usługi sieci Web Microsoft Azure Machine Learning](https://services.azureml.net/quickstart) portalu.</span><span class="sxs-lookup"><span data-stu-id="3ff8b-245">Once you've deployed your web service, whether Classic or New, you can manage it from hello [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/quickstart) portal.</span></span>

<span data-ttu-id="3ff8b-246">wydajność hello toomonitor usługi sieci web:</span><span class="sxs-lookup"><span data-stu-id="3ff8b-246">toomonitor hello performance of your web service:</span></span>

1. <span data-ttu-id="3ff8b-247">Zaloguj się toohello [usługi sieci Web Microsoft Azure Machine Learning](https://services.azureml.net/quickstart) portalu</span><span class="sxs-lookup"><span data-stu-id="3ff8b-247">Sign in toohello [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/quickstart) portal</span></span>
2. <span data-ttu-id="3ff8b-248">Kliknij przycisk **usług sieci Web**</span><span class="sxs-lookup"><span data-stu-id="3ff8b-248">Click **Web services**</span></span>
3. <span data-ttu-id="3ff8b-249">Kliknij opcję usługi sieci web</span><span class="sxs-lookup"><span data-stu-id="3ff8b-249">Click your web service</span></span>
4. <span data-ttu-id="3ff8b-250">Kliknij przycisk hello **pulpitu nawigacyjnego**</span><span class="sxs-lookup"><span data-stu-id="3ff8b-250">Click hello **Dashboard**</span></span>

- - -
<span data-ttu-id="3ff8b-251">**Następnie: [dostępu do usługi sieci web hello](machine-learning-walkthrough-6-access-web-service.md)**</span><span class="sxs-lookup"><span data-stu-id="3ff8b-251">**Next: [Access hello web service](machine-learning-walkthrough-6-access-web-service.md)**</span></span>

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
