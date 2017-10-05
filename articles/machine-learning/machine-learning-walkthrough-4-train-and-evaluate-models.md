---
title: 'Krok 4: Nauczanie i Ewaluacja modeli predykcyjnych analityczne | Dokumentacja firmy Microsoft'
description: "Krok 4 opracowanie wskazówki rozwiązanie predykcyjne: pociągu, wynik i ocena wielu modeli w usłudze Azure Machine Learning Studio."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: d905f6b3-9201-4117-b769-5f9ed5ee1cac
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 58d46dd1464ec0a3fc9639f78d4429e0e778c2bf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="walkthrough-step-4-train-and-evaluate-the-predictive-analytic-models"></a><span data-ttu-id="aac93-103">Przewodnik, krok 4. Uczenie i ocenianie modeli do analizy predykcyjnej</span><span class="sxs-lookup"><span data-stu-id="aac93-103">Walkthrough Step 4: Train and evaluate the predictive analytic models</span></span>
<span data-ttu-id="aac93-104">Ten temat zawiera wskazówki, czwarty krok [tworzenie rozwiązania analizy predykcyjnej w usłudze Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="aac93-104">This topic contains the fourth step of the walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. [<span data-ttu-id="aac93-105">Tworzenie obszaru roboczego usługi Machine Learning</span><span class="sxs-lookup"><span data-stu-id="aac93-105">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="aac93-106">Przekazywanie istniejących danych</span><span class="sxs-lookup"><span data-stu-id="aac93-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="aac93-107">Tworzenie nowego eksperymentu</span><span class="sxs-lookup"><span data-stu-id="aac93-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. <span data-ttu-id="aac93-108">**Nauczanie i ocena modeli**</span><span class="sxs-lookup"><span data-stu-id="aac93-108">**Train and evaluate the models**</span></span>
5. [<span data-ttu-id="aac93-109">Wdrażanie usługi sieci Web</span><span class="sxs-lookup"><span data-stu-id="aac93-109">Deploy the Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="aac93-110">Dostęp do usługi sieci Web</span><span class="sxs-lookup"><span data-stu-id="aac93-110">Access the Web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<span data-ttu-id="aac93-111">Jedną z zalet przy użyciu usługi Azure Machine Learning Studio do tworzenia modeli uczenia maszyny jest możliwość spróbuj więcej niż jeden typ modelu jednocześnie w jednym eksperymentu, a następnie porównaj wyniki.</span><span class="sxs-lookup"><span data-stu-id="aac93-111">One of the benefits of using Azure Machine Learning Studio for creating machine learning models is the ability to try more than one type of model at a time in a single experiment and compare the results.</span></span> <span data-ttu-id="aac93-112">Ten typ eksperymenty ułatwia znalezienie najlepszego rozwiązania dla danego problemu.</span><span class="sxs-lookup"><span data-stu-id="aac93-112">This type of experimentation helps you find the best solution for your problem.</span></span>

<span data-ttu-id="aac93-113">W eksperymencie, które firma Microsoft tworzony jest w tym przewodniku możemy utworzyć dwa rodzaje modeli i porównać ich wyników oceniania zdecydować, który algorytm możemy mają być używane w naszych końcowy eksperyment.</span><span class="sxs-lookup"><span data-stu-id="aac93-113">In the experiment we're developing in this walkthrough, we'll create two different types of models and then compare their scoring results to decide which algorithm we want to use in our final experiment.</span></span>  

<span data-ttu-id="aac93-114">Istnieją różne modele, firma Microsoft może wyboru.</span><span class="sxs-lookup"><span data-stu-id="aac93-114">There are various models we could choose from.</span></span> <span data-ttu-id="aac93-115">Aby wyświetlić dostępne modele, rozwiń węzeł **uczenia maszynowego** węzła na palecie modułów, a następnie rozwiń węzeł **zainicjować modelu** i węzły znajdujące się poniżej.</span><span class="sxs-lookup"><span data-stu-id="aac93-115">To see the models available, expand the **Machine Learning** node in the module palette, and then expand **Initialize Model** and the nodes beneath it.</span></span> <span data-ttu-id="aac93-116">Na potrzeby tego eksperymentu wybierzemy [maszyny wektorowa obsługa Two-Class] [ two-class-support-vector-machine] (SVM) i [Two-Class Boosted drzewa decyzyjnego] [ two-class-boosted-decision-tree] modułów.</span><span class="sxs-lookup"><span data-stu-id="aac93-116">For the purposes of this experiment, we'll select the [Two-Class Support Vector Machine][two-class-support-vector-machine] (SVM) and the [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] modules.</span></span>    

> [!TIP]
> <span data-ttu-id="aac93-117">Aby uzyskać dodatkową pomoc przy wyborze, który algorytm uczenia maszynowego najlepiej pasujące do określonej problem próbuje rozwiązać, zobacz [Wybieranie algorytmów w Microsoft Azure Machine Learning](machine-learning-algorithm-choice.md).</span><span class="sxs-lookup"><span data-stu-id="aac93-117">To get help deciding which Machine Learning algorithm best suits the particular problem you're trying to solve, see [How to choose algorithms for Microsoft Azure Machine Learning](machine-learning-algorithm-choice.md).</span></span>
> 
> 

## <a name="train-the-models"></a><span data-ttu-id="aac93-118">Modele uczenia</span><span class="sxs-lookup"><span data-stu-id="aac93-118">Train the models</span></span>

<span data-ttu-id="aac93-119">Dodamy zarówno [Two-Class Boosted drzewa decyzyjnego] [ two-class-boosted-decision-tree] modułu i [maszyny wektorowa obsługa Two-Class] [ two-class-support-vector-machine] modułu, w tym eksperymencie.</span><span class="sxs-lookup"><span data-stu-id="aac93-119">We'll add both the [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module and [Two-Class Support Vector Machine][two-class-support-vector-machine] module in this experiment.</span></span>

### <a name="two-class-boosted-decision-tree"></a><span data-ttu-id="aac93-120">Two-Class Boosted algorytm</span><span class="sxs-lookup"><span data-stu-id="aac93-120">Two-Class Boosted Decision Tree</span></span>

<span data-ttu-id="aac93-121">Najpierw skonfiguruj boosted decyzji drzewa modelu.</span><span class="sxs-lookup"><span data-stu-id="aac93-121">First, let's set up the boosted decision tree model.</span></span>

1. <span data-ttu-id="aac93-122">Znajdź [Two-Class Boosted drzewa decyzyjnego] [ two-class-boosted-decision-tree] modułu na palecie modułów i przeciągnij go do obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="aac93-122">Find the [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module in the module palette and drag it onto the canvas.</span></span>

2. <span data-ttu-id="aac93-123">Znajdź [Train Model] [ train-model] modułu, przeciągnij go do obszaru roboczego, a następnie połącz dane wyjściowe [Two-Class Boosted drzewa decyzyjnego] [ two-class-boosted-decision-tree] port wejściowy modułu po lewej stronie [Train Model] [ train-model] modułu.</span><span class="sxs-lookup"><span data-stu-id="aac93-123">Find the [Train Model][train-model] module, drag it onto the canvas, and then connect the output of the [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module to the left input port of the [Train Model][train-model] module.</span></span>
   
   <span data-ttu-id="aac93-124">[Two-Class Boosted drzewa decyzyjnego] [ two-class-boosted-decision-tree] modułu inicjuje rodzajowy modelu i [Train Model] [ train-model] używa danych szkoleniowych do uczenia model.</span><span class="sxs-lookup"><span data-stu-id="aac93-124">The [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module initializes the generic model, and [Train Model][train-model] uses training data to train the model.</span></span> 

3. <span data-ttu-id="aac93-125">Połącz dane wyjściowe po lewej stronie po lewej stronie [wykonanie skryptu języka R] [ execute-r-script] modułu po prawej stronie wprowadź port [Train Model] [ train-model] (zdecydowaliśmy w module [Kroku 3](machine-learning-walkthrough-3-create-new-experiment.md) tego przewodnika to użycie danych pochodzących z lewej strony modułu podziału danych szkoleń).</span><span class="sxs-lookup"><span data-stu-id="aac93-125">Connect the left output of the left [Execute R Script][execute-r-script] module to the right input port of the [Train Model][train-model] module (we decided in [Step 3](machine-learning-walkthrough-3-create-new-experiment.md) of this walkthrough to use the data coming from the left side of the Split Data module for training).</span></span>
   
   > [!TIP]
   > <span data-ttu-id="aac93-126">Firma Microsoft nie ma potrzeby dwóch danych wejściowych, a drugi dane wyjściowe [wykonanie skryptu języka R] [ execute-r-script] modułu do tego eksperymentu, dlatego firma Microsoft może narazić je odłączyć.</span><span class="sxs-lookup"><span data-stu-id="aac93-126">We don't need two of the inputs and one of the outputs of the [Execute R Script][execute-r-script] module for this experiment, so we can leave them unattached.</span></span> 
   > 
   > 

<span data-ttu-id="aac93-127">Ta część eksperyment teraz wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="aac93-127">This portion of the experiment now looks something like this:</span></span>  

![Uczenie modelu][1]

<span data-ttu-id="aac93-129">Teraz musimy sprawdzić [Train Model] [ train-model] modułu czy chcemy model do przewidywania wartości ryzyka kredytowego.</span><span class="sxs-lookup"><span data-stu-id="aac93-129">Now we need to tell the [Train Model][train-model] module that we want the model to predict the Credit Risk value.</span></span>

1. <span data-ttu-id="aac93-130">Wybierz [Train Model] [ train-model] modułu.</span><span class="sxs-lookup"><span data-stu-id="aac93-130">Select the [Train Model][train-model] module.</span></span> <span data-ttu-id="aac93-131">W **właściwości** okienku, kliknij przycisk **Uruchom selektor kolumn**.</span><span class="sxs-lookup"><span data-stu-id="aac93-131">In the **Properties** pane, click **Launch column selector**.</span></span>

2. <span data-ttu-id="aac93-132">W **wybrać pojedynczą kolumnę** okna dialogowego, wpisz "ryzyko kredytowe" w polu wyszukiwania w obszarze **dostępne kolumny**, wybierz "Ryzyko kredytowe" poniżej i kliknij przycisk strzałki w prawo ( **>** ) aby przenieść "Ryzyka kredytowego" **wybrane kolumny**.</span><span class="sxs-lookup"><span data-stu-id="aac93-132">In the **Select a single column** dialog, type "credit risk" in the search field under **Available Columns**, select "Credit risk" below, and click the right arrow button (**>**) to move "Credit risk" to **Selected Columns**.</span></span> 

    ![Wybierz kolumnę ryzyka kredytowego modułu Train Model][0]

3. <span data-ttu-id="aac93-134">Kliknij przycisk **OK** znacznik wyboru.</span><span class="sxs-lookup"><span data-stu-id="aac93-134">Click the **OK** check mark.</span></span>

### <a name="two-class-support-vector-machine"></a><span data-ttu-id="aac93-135">Algorytm SVM dla problemu dwuklasowego</span><span class="sxs-lookup"><span data-stu-id="aac93-135">Two-Class Support Vector Machine</span></span>

<span data-ttu-id="aac93-136">Następnie skonfigurowanie SVM modelu.</span><span class="sxs-lookup"><span data-stu-id="aac93-136">Next, we set up the SVM model.</span></span>  

<span data-ttu-id="aac93-137">Pierwszy, nieco wyjaśnienie SVM.</span><span class="sxs-lookup"><span data-stu-id="aac93-137">First, a little explanation about SVM.</span></span> <span data-ttu-id="aac93-138">Drzewa decyzyjne boosted działają prawidłowo w przypadku funkcji dowolnego typu.</span><span class="sxs-lookup"><span data-stu-id="aac93-138">Boosted decision trees work well with features of any type.</span></span> <span data-ttu-id="aac93-139">Jednak ponieważ moduł SVM generuje klasyfikatora liniowego, modelu, który generuje ma najlepsze błąd testu, gdy wszystkie funkcje numeryczne mieć takiej samej skali.</span><span class="sxs-lookup"><span data-stu-id="aac93-139">However, since the SVM module generates a linear classifier, the model that it generates has the best test error when all numeric features have the same scale.</span></span> <span data-ttu-id="aac93-140">Aby przekonwertować wszystkie funkcje numeryczne takiej samej skali, używamy transformację "Tanh" (z [normalizacji danych] [ normalize-data] modułu).</span><span class="sxs-lookup"><span data-stu-id="aac93-140">To convert all numeric features to the same scale, we use a "Tanh" transformation (with the [Normalize Data][normalize-data] module).</span></span> <span data-ttu-id="aac93-141">To przekształca naszych numery w zakresie [0,1].</span><span class="sxs-lookup"><span data-stu-id="aac93-141">This transforms our numbers into the [0,1] range.</span></span> <span data-ttu-id="aac93-142">Moduł SVM konwertuje ciąg funkcji funkcje podzielone na kategorie, a następnie binarne funkcji 0/1, nie należy ręcznie Przekształcanie funkcji ciągu.</span><span class="sxs-lookup"><span data-stu-id="aac93-142">The SVM module converts string features to categorical features and then to binary 0/1 features, so we don't need to manually transform string features.</span></span> <span data-ttu-id="aac93-143">Ponadto nie chcemy przekształcenie ryzyka kredytowego kolumna (kolumna 21) — liczbowych jest, ale jest wartość możemy uczony model do przewidywania, więc musimy pozostawiony.</span><span class="sxs-lookup"><span data-stu-id="aac93-143">Also, we don't want to transform the Credit Risk column (column 21) - it's numeric, but it's the value we're training the model to predict, so we need to leave it alone.</span></span>  

<span data-ttu-id="aac93-144">Aby skonfigurować SVM model, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="aac93-144">To set up the SVM model, do the following:</span></span>

1. <span data-ttu-id="aac93-145">Znajdź [maszyny wektorowa obsługa Two-Class] [ two-class-support-vector-machine] modułu na palecie modułów i przeciągnij go do obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="aac93-145">Find the [Two-Class Support Vector Machine][two-class-support-vector-machine] module in the module palette and drag it onto the canvas.</span></span>

2. <span data-ttu-id="aac93-146">Kliknij prawym przyciskiem myszy [Train Model] [ train-model] modułu, wybierz opcję **kopiowania**i kliknij prawym przyciskiem myszy kanwę i wybierz **Wklej**.</span><span class="sxs-lookup"><span data-stu-id="aac93-146">Right-click the [Train Model][train-model] module, select **Copy**, and then right-click the canvas and select **Paste**.</span></span> <span data-ttu-id="aac93-147">Kopię [Train Model] [ train-model] moduł ma tego samego kolumnę zaznaczenia co oryginalny.</span><span class="sxs-lookup"><span data-stu-id="aac93-147">The copy of the [Train Model][train-model] module has the same column selection as the original.</span></span>

3. <span data-ttu-id="aac93-148">Połącz dane wyjściowe [maszyny wektorowa obsługa Two-Class] [ two-class-support-vector-machine] modułu po lewej stronie wprowadź port drugiego [Train Model] [ train-model] modułu.</span><span class="sxs-lookup"><span data-stu-id="aac93-148">Connect the output of the [Two-Class Support Vector Machine][two-class-support-vector-machine] module to the left input port of the second [Train Model][train-model] module.</span></span>

4. <span data-ttu-id="aac93-149">Znajdź [normalizacji danych] [ normalize-data] modułu i przeciągnij go do obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="aac93-149">Find the [Normalize Data][normalize-data] module and drag it onto the canvas.</span></span>

5. <span data-ttu-id="aac93-150">Połącz dane wyjściowe po lewej stronie po lewej stronie [wykonanie skryptu języka R] [ execute-r-script] modułu w danych wejściowych w tym module (powiadomienia, czy port wyjściowy modułu może być podłączony do więcej niż jeden moduł innych).</span><span class="sxs-lookup"><span data-stu-id="aac93-150">Connect the left output of the left [Execute R Script][execute-r-script] module to the input of this module (notice that the output port of a module may be connected to more than one other module).</span></span>

6. <span data-ttu-id="aac93-151">Połącz lewy port wyjściowy [normalizacji danych] [ normalize-data] modułu po prawej stronie wprowadź port drugiego [Train Model] [ train-model] modułu.</span><span class="sxs-lookup"><span data-stu-id="aac93-151">Connect the left output port of the [Normalize Data][normalize-data] module to the right input port of the second [Train Model][train-model] module.</span></span>

<span data-ttu-id="aac93-152">Ta część naszego eksperyment powinien teraz wyglądać mniej więcej tak:</span><span class="sxs-lookup"><span data-stu-id="aac93-152">This portion of our experiment should now look something like this:</span></span>  

![Uczenie modelu drugi][2]  

<span data-ttu-id="aac93-154">Teraz skonfigurować [normalizacji danych] [ normalize-data] modułu:</span><span class="sxs-lookup"><span data-stu-id="aac93-154">Now configure the [Normalize Data][normalize-data] module:</span></span>

1. <span data-ttu-id="aac93-155">Kliknij, aby wybrać [normalizacji danych] [ normalize-data] modułu.</span><span class="sxs-lookup"><span data-stu-id="aac93-155">Click to select the [Normalize Data][normalize-data] module.</span></span> <span data-ttu-id="aac93-156">W **właściwości** okienku wybierz **Tanh** dla **metody przekształcania** parametru.</span><span class="sxs-lookup"><span data-stu-id="aac93-156">In the **Properties** pane, select **Tanh** for the **Transformation method** parameter.</span></span>

2. <span data-ttu-id="aac93-157">Kliknij przycisk **Uruchom selektor kolumn**, wybierz opcję "Brak kolumn" dla **od**, wybierz pozycję **Include** z pierwszej listy rozwijanej wybierz **typ kolumny** w drugim listy rozwijanej, a następnie wybierz **liczbowych** na liście rozwijanej trzecich.</span><span class="sxs-lookup"><span data-stu-id="aac93-157">Click **Launch column selector**, select "No columns" for **Begin With**, select **Include** in the first dropdown, select **column type** in the second dropdown, and select **Numeric** in the third dropdown.</span></span> <span data-ttu-id="aac93-158">To ustawienie określa przekształcone wszystkie kolumny liczbowe (i tylko numeryczne).</span><span class="sxs-lookup"><span data-stu-id="aac93-158">This specifies that all the numeric columns (and only numeric) are transformed.</span></span>

3. <span data-ttu-id="aac93-159">Kliknij znak plus (+) z prawej strony tego wiersza — spowoduje to utworzenie wiersza listę rozwijaną.</span><span class="sxs-lookup"><span data-stu-id="aac93-159">Click the plus sign (+) to the right of this row - this creates a row of dropdowns.</span></span> <span data-ttu-id="aac93-160">Wybierz **wykluczyć** z pierwszej listy rozwijanej wybierz **nazwy kolumn** w drugim listy rozwijanej, a następnie wprowadź "Ryzyko kredytowe" w polu tekstowym.</span><span class="sxs-lookup"><span data-stu-id="aac93-160">Select **Exclude** in the first dropdown, select **column names** in the second dropdown, and enter "Credit risk" in the text field.</span></span> <span data-ttu-id="aac93-161">Określa kolumnę ryzyka kredytowego należy ją ignorować (należy to zrobić, ponieważ ta kolumna jest liczbowe w związku z czym może zostać przekształcone Jeśli firma Microsoft nie go wykluczyć).</span><span class="sxs-lookup"><span data-stu-id="aac93-161">This specifies that the Credit Risk column should be ignored (we need to do this because this column is numeric and so would be transformed if we didn't exclude it).</span></span>

4. <span data-ttu-id="aac93-162">Kliknij przycisk **OK** znacznik wyboru.</span><span class="sxs-lookup"><span data-stu-id="aac93-162">Click the **OK** check mark.</span></span>  

    ![Wybierz kolumnę do modułu normalizacji danych][5]

<span data-ttu-id="aac93-164">[Normalizacji danych] [ normalize-data] modułu ma teraz wartość przekształcenie Tanh dla wszystkich kolumn liczbowych, z wyjątkiem kolumny ryzyka kredytowego.</span><span class="sxs-lookup"><span data-stu-id="aac93-164">The [Normalize Data][normalize-data] module is now set to perform a Tanh transformation on all numeric columns except for the Credit Risk column.</span></span>  

## <a name="score-and-evaluate-the-models"></a><span data-ttu-id="aac93-165">Uczenie i Ewaluacja modeli</span><span class="sxs-lookup"><span data-stu-id="aac93-165">Score and evaluate the models</span></span>

<span data-ttu-id="aac93-166">Używamy testowania danych, który został oddzielony się przez [podziału danych] [ split] modułu do wyniku naszych przeszkolone modeli.</span><span class="sxs-lookup"><span data-stu-id="aac93-166">We use the testing data that was separated out by the [Split Data][split] module to score our trained models.</span></span> <span data-ttu-id="aac93-167">Firma Microsoft może następnie porównaj wyniki działania dwa modele, aby zobaczyć, która jest generowana w poszukiwaniu lepszych wyników.</span><span class="sxs-lookup"><span data-stu-id="aac93-167">We can then compare the results of the two models to see which generated better results.</span></span>  

### <a name="add-the-score-model-modules"></a><span data-ttu-id="aac93-168">Dodaj moduł Score Model</span><span class="sxs-lookup"><span data-stu-id="aac93-168">Add the Score Model modules</span></span>

1. <span data-ttu-id="aac93-169">Znajdź [Score Model] [ score-model] modułu i przeciągnij go do obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="aac93-169">Find the [Score Model][score-model] module and drag it onto the canvas.</span></span>

2. <span data-ttu-id="aac93-170">Połącz [Train Model] [ train-model] moduł, który jest połączony z [Two-Class Boosted drzewa decyzyjnego] [ two-class-boosted-decision-tree] port wejściowy modułu w lewo [Score Model] [ score-model] modułu.</span><span class="sxs-lookup"><span data-stu-id="aac93-170">Connect the [Train Model][train-model] module that's connected to the [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module to the left input port of the [Score Model][score-model] module.</span></span>

3. <span data-ttu-id="aac93-171">Połącz prawo [wykonanie skryptu języka R] [ execute-r-script] modułu (danych testowych) po prawej stronie wprowadź port [Score Model] [ score-model] modułu.</span><span class="sxs-lookup"><span data-stu-id="aac93-171">Connect the right [Execute R Script][execute-r-script] module (our testing data) to the right input port of the [Score Model][score-model] module.</span></span>

    ![Moduł score Model połączenia][6]
   
   <span data-ttu-id="aac93-173">[Score Model] [ score-model] modułu można teraz odpowiednie informacje środki z danych testowych, uruchom go za pośrednictwem modelu i porównywania prognoz modelu generuje z kolumną ryzyka rzeczywiste środki w Testowanie danych.</span><span class="sxs-lookup"><span data-stu-id="aac93-173">The [Score Model][score-model] module can now take the credit information from the testing data, run it through the model, and compare the predictions the model generates with the actual credit risk column in the testing data.</span></span>

4. <span data-ttu-id="aac93-174">Skopiuj i Wklej [Score Model] [ score-model] modułu do utworzenia drugiej kopii.</span><span class="sxs-lookup"><span data-stu-id="aac93-174">Copy and paste the [Score Model][score-model] module to create a second copy.</span></span>

5. <span data-ttu-id="aac93-175">Połącz dane wyjściowe modelu SVM (to znaczy portem wyjściowym [Train Model] [ train-model] moduł, który jest połączony z [maszyny wektorowa obsługa Two-Class] [ two-class-support-vector-machine] modułu) do portu wejściowego drugiego [Score Model] [ score-model] modułu.</span><span class="sxs-lookup"><span data-stu-id="aac93-175">Connect the output of the SVM model (that is, the output port of the [Train Model][train-model] module that's connected to the [Two-Class Support Vector Machine][two-class-support-vector-machine] module) to the input port of the second [Score Model][score-model] module.</span></span>

6. <span data-ttu-id="aac93-176">SVM model zostały celu przekształcenia do danych testowych, jak robiliśmy danych szkoleniowych.</span><span class="sxs-lookup"><span data-stu-id="aac93-176">For the SVM model, we have to do the same transformation to the test data as we did to the training data.</span></span> <span data-ttu-id="aac93-177">Aby skopiować i wkleić [normalizacji danych] [ normalize-data] modułu Tworzenie drugiej kopii i połącz go z prawej strony [wykonanie skryptu języka R] [ execute-r-script] modułu.</span><span class="sxs-lookup"><span data-stu-id="aac93-177">So copy and paste the [Normalize Data][normalize-data] module to create a second copy and connect it to the right [Execute R Script][execute-r-script] module.</span></span>

7. <span data-ttu-id="aac93-178">Połącz dane wyjściowe po lewej stronie drugiego [normalizacji danych] [ normalize-data] modułu po prawej stronie wprowadź port drugiego [Score Model] [ score-model] modułu.</span><span class="sxs-lookup"><span data-stu-id="aac93-178">Connect the left output of the second [Normalize Data][normalize-data] module to the right input port of the second [Score Model][score-model] module.</span></span>

    ![Zarówno modułów Score Model połączenia][7]

### <a name="add-the-evaluate-model-module"></a><span data-ttu-id="aac93-180">Dodanie modułu Evaluate Model</span><span class="sxs-lookup"><span data-stu-id="aac93-180">Add the Evaluate Model module</span></span>

<span data-ttu-id="aac93-181">Aby ocenić dwóch wyników oceniania i porównaj je, używamy [Evaluate Model] [ evaluate-model] modułu.</span><span class="sxs-lookup"><span data-stu-id="aac93-181">To evaluate the two scoring results and compare them, we use an [Evaluate Model][evaluate-model] module.</span></span>  

1. <span data-ttu-id="aac93-182">Znajdź [Evaluate Model] [ evaluate-model] modułu i przeciągnij go do obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="aac93-182">Find the [Evaluate Model][evaluate-model] module and drag it onto the canvas.</span></span>

2. <span data-ttu-id="aac93-183">Połącz port wyjściowy [Score Model] [ score-model] modułu skojarzonego z tym modelem drzewa decyzyjnego boosted do lewy port wejściowy z [Evaluate Model] [ evaluate-model] modułu.</span><span class="sxs-lookup"><span data-stu-id="aac93-183">Connect the output port of the [Score Model][score-model] module associated with the boosted decision tree model to the left input port of the [Evaluate Model][evaluate-model] module.</span></span>

3. <span data-ttu-id="aac93-184">Połącz innych [Score Model] [ score-model] port wejściowy modułu z prawej strony.</span><span class="sxs-lookup"><span data-stu-id="aac93-184">Connect the other [Score Model][score-model] module to the right input port.</span></span>  

    ![Ocena modelu modułu połączone][8]

### <a name="run-the-experiment-and-check-the-results"></a><span data-ttu-id="aac93-186">Uruchom eksperyment i sprawdzić wyniki</span><span class="sxs-lookup"><span data-stu-id="aac93-186">Run the experiment and check the results</span></span>

<span data-ttu-id="aac93-187">Aby uruchomić eksperyment, kliknij przycisk **Uruchom** znajdujący się poniżej obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="aac93-187">To run the experiment, click the **RUN** button below the canvas.</span></span> <span data-ttu-id="aac93-188">Może upłynąć kilka minut.</span><span class="sxs-lookup"><span data-stu-id="aac93-188">It may take a few minutes.</span></span> <span data-ttu-id="aac93-189">Wskaźnik Obracająca dla każdego modułu pokazuje, że jest uruchomiona, i czym wyświetlany zielony znacznik wyboru, po zakończeniu modułu.</span><span class="sxs-lookup"><span data-stu-id="aac93-189">A spinning indicator on each module shows that it's running, and then a green check mark shows when the module is finished.</span></span> <span data-ttu-id="aac93-190">Jeśli zaznaczono wszystkie moduły eksperyment zakończył działanie.</span><span class="sxs-lookup"><span data-stu-id="aac93-190">When all the modules have a check mark, the experiment has finished running.</span></span>

<span data-ttu-id="aac93-191">Eksperyment powinien teraz wyglądać mniej więcej tak:</span><span class="sxs-lookup"><span data-stu-id="aac93-191">The experiment should now look something like this:</span></span>  

![Ocena obu modeli][3]

<span data-ttu-id="aac93-193">Aby sprawdzić wyniki, kliknij port wyjściowy [Evaluate Model] [ evaluate-model] moduł i zaznacz **Visualize**.</span><span class="sxs-lookup"><span data-stu-id="aac93-193">To check the results, click the output port of the [Evaluate Model][evaluate-model] module and select **Visualize**.</span></span>  

<span data-ttu-id="aac93-194">[Evaluate Model] [ evaluate-model] modułu tworzy parę krzywych i metryk, które pozwalają porównać wyniki dwa modele scored.</span><span class="sxs-lookup"><span data-stu-id="aac93-194">The [Evaluate Model][evaluate-model] module produces a pair of curves and metrics that allow you to compare the results of the two scored models.</span></span> <span data-ttu-id="aac93-195">Można wyświetlić wyniki w postaci krzywych cech Operator odbiornika (ROC), krzywych dokładności/wycofania lub krzywych przyrostu.</span><span class="sxs-lookup"><span data-stu-id="aac93-195">You can view the results as Receiver Operator Characteristic (ROC) curves, Precision/Recall curves, or Lift curves.</span></span> <span data-ttu-id="aac93-196">Dodatkowe dane wyświetlane obejmuje macierz pomyłek, łączne wartości dla obszarze krzywej (AUC) i innych metryk.</span><span class="sxs-lookup"><span data-stu-id="aac93-196">Additional data displayed includes a confusion matrix, cumulative values for the area under the curve (AUC), and other metrics.</span></span> <span data-ttu-id="aac93-197">Można zmienić wartość progowa za pomocą suwaka, lewo lub w prawo i zobacz, jak wpływa na zbiór metryki.</span><span class="sxs-lookup"><span data-stu-id="aac93-197">You can change the threshold value by moving the slider left or right and see how it affects the set of metrics.</span></span>  

<span data-ttu-id="aac93-198">Po prawej stronie wykresu **oceniane zestawu danych** lub **oceniane zestawu danych, aby porównać** Wyróżnij skojarzone krzywej i wyświetlania metryk skojarzone poniżej.</span><span class="sxs-lookup"><span data-stu-id="aac93-198">To the right of the graph, click **Scored dataset** or **Scored dataset to compare** to highlight the associated curve and to display the associated metrics below.</span></span> <span data-ttu-id="aac93-199">W legendzie dla krzywych "Oceniane zestawu danych" odpowiada lewy port wejściowy z [Evaluate Model] [ evaluate-model] moduł — w tym przypadku jest to model drzewa boosted decyzji.</span><span class="sxs-lookup"><span data-stu-id="aac93-199">In the legend for the curves, "Scored dataset" corresponds to the left input port of the [Evaluate Model][evaluate-model] module - in our case, this is the boosted decision tree model.</span></span> <span data-ttu-id="aac93-200">"Zestawu danych, aby porównać wynik" odpowiada prawy port wejściowy - SVM modelu w tym przypadku.</span><span class="sxs-lookup"><span data-stu-id="aac93-200">"Scored dataset to compare" corresponds to the right input port - the SVM model in our case.</span></span> <span data-ttu-id="aac93-201">Po kliknięciu jednego z tych etykiet zostanie wyróżniona krzywej modelu i wyświetlane są odpowiednie metryki, jak pokazano na poniższym rysunku.</span><span class="sxs-lookup"><span data-stu-id="aac93-201">When you click one of these labels, the curve for that model is highlighted and the corresponding metrics are displayed, as shown in the following graphic.</span></span>  

![Krzywe ROC dla modeli][4]

<span data-ttu-id="aac93-203">Badanie tych wartości, można zdecydować, model, który jest najbardziej zbliżony do daje rezultatów, którego szukasz.</span><span class="sxs-lookup"><span data-stu-id="aac93-203">By examining these values, you can decide which model is closest to giving you the results you're looking for.</span></span> <span data-ttu-id="aac93-204">Możesz wrócić do poprzedniej strony i iterację eksperymentu, zmieniając wartości parametrów w różne modele.</span><span class="sxs-lookup"><span data-stu-id="aac93-204">You can go back and iterate on your experiment by changing parameter values in the different models.</span></span> 

<span data-ttu-id="aac93-205">Nauki i grafik interpretowanie te wyniki i dostrajania wydajności modelu wykracza poza zakres tego przewodnika.</span><span class="sxs-lookup"><span data-stu-id="aac93-205">The science and art of interpreting these results and tuning the model performance is outside the scope of this walkthrough.</span></span> <span data-ttu-id="aac93-206">Aby uzyskać dodatkową pomoc może przeczytać następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="aac93-206">For additional help, you might read the following articles:</span></span>
- [<span data-ttu-id="aac93-207">Jak do oceny wydajności modelu w usłudze Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="aac93-207">How to evaluate model performance in Azure Machine Learning</span></span>](machine-learning-evaluate-model-performance.md)
- [<span data-ttu-id="aac93-208">Wybierz parametry w celu zoptymalizowania algorytmy w usłudze Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="aac93-208">Choose parameters to optimize your algorithms in Azure Machine Learning</span></span>](machine-learning-algorithm-parameters-optimize.md)
- [<span data-ttu-id="aac93-209">Interpretowanie wyników modelu w usłudze Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="aac93-209">Interpret model results in Azure Machine Learning</span></span>](machine-learning-interpret-model-results.md)

> [!TIP]
> <span data-ttu-id="aac93-210">Zawsze uruchomić eksperyment rekord tego iteracji jest przechowywanych w historii uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="aac93-210">Each time you run the experiment a record of that iteration is kept in the Run History.</span></span> <span data-ttu-id="aac93-211">Można wyświetlić te iteracji i wróć do każdej z nich, klikając **WYŚWIETL HISTORIĘ URUCHAMIANIA** poniżej obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="aac93-211">You can view these iterations, and return to any of them, by clicking **VIEW RUN HISTORY** below the canvas.</span></span> <span data-ttu-id="aac93-212">Możesz również kliknąć **uprzedniego uruchomienia** w **właściwości** okienko, aby powrócić do iteracji, bezpośrednio przed otwartych.</span><span class="sxs-lookup"><span data-stu-id="aac93-212">You can also click **Prior Run** in the **Properties** pane to return to the iteration immediately preceding the one you have open.</span></span>
> 
> <span data-ttu-id="aac93-213">Można utworzyć kopię dowolną iterację eksperymentu, klikając **SAVE AS** poniżej obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="aac93-213">You can make a copy of any iteration of your experiment by clicking **SAVE AS** below the canvas.</span></span> 
> <span data-ttu-id="aac93-214">Użyj eksperymentu **Podsumowanie** i **opis** właściwości, aby rejestrować co podjęto w Twojej iteracje eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="aac93-214">Use the experiment's **Summary** and **Description** properties to keep a record of what you've tried in your experiment iterations.</span></span>
> 
> <span data-ttu-id="aac93-215">Aby uzyskać więcej informacji, zobacz [Zarządzanie iteracjami eksperymentów w usłudze Azure Machine Learning Studio](machine-learning-manage-experiment-iterations.md).</span><span class="sxs-lookup"><span data-stu-id="aac93-215">For more details, see [Manage experiment iterations in Azure Machine Learning Studio](machine-learning-manage-experiment-iterations.md).</span></span>  
> 
> 

- - -
<span data-ttu-id="aac93-216">**Następnie: [wdrażanie usługi sieci web](machine-learning-walkthrough-5-publish-web-service.md)**</span><span class="sxs-lookup"><span data-stu-id="aac93-216">**Next: [Deploy the web service](machine-learning-walkthrough-5-publish-web-service.md)**</span></span>

[0]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/train-model-select-column.png
[1]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/experiment-with-train-model.png
[2]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/svm-model-added.png
[3]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/final-experiment.png
[4]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/roc-curves.png
[5]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/normalize-data-select-column.png
[6]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/score-model-connected.png
[7]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/both-score-models-added.png
[8]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/evaluate-model-added.png


<!-- Module References -->
[evaluate-model]: https://msdn.microsoft.com/library/azure/927d65ac-3b50-4694-9903-20f6c1672089/
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[normalize-data]: https://msdn.microsoft.com/library/azure/986df333-6748-4b85-923d-871df70d6aaf/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
[two-class-boosted-decision-tree]: https://msdn.microsoft.com/library/azure/e3c522f8-53d9-4829-8ea4-5c6a6b75330c/
[two-class-support-vector-machine]: https://msdn.microsoft.com/library/azure/12d8479b-74b4-4e67-b8de-d32867380e20/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
