---
title: 'Krok 4: Nauczanie i Ewaluacja modeli predykcyjnych analityczne hello | Dokumentacja firmy Microsoft'
description: "Krok 4 hello opracowanie wskazówki rozwiązanie predykcyjne: pociągu, wynik i ocena wielu modeli w usłudze Azure Machine Learning Studio."
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
ms.openlocfilehash: d86d7c5ae7524f71fe44d985db67c4618b7965a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-4-train-and-evaluate-hello-predictive-analytic-models"></a><span data-ttu-id="158c3-103">Wskazówki krok 4: Nauczanie i Ewaluacja modeli predykcyjnych analityczne hello</span><span class="sxs-lookup"><span data-stu-id="158c3-103">Walkthrough Step 4: Train and evaluate hello predictive analytic models</span></span>
<span data-ttu-id="158c3-104">Ten temat zawiera hello czwarty krok wskazówki hello [tworzenie rozwiązania analizy predykcyjnej w usłudze Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="158c3-104">This topic contains hello fourth step of hello walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. [<span data-ttu-id="158c3-105">Tworzenie obszaru roboczego usługi Machine Learning</span><span class="sxs-lookup"><span data-stu-id="158c3-105">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="158c3-106">Przekazywanie istniejących danych</span><span class="sxs-lookup"><span data-stu-id="158c3-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="158c3-107">Tworzenie nowego eksperymentu</span><span class="sxs-lookup"><span data-stu-id="158c3-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. <span data-ttu-id="158c3-108">**Nauczanie i Ewaluacja modeli hello**</span><span class="sxs-lookup"><span data-stu-id="158c3-108">**Train and evaluate hello models**</span></span>
5. [<span data-ttu-id="158c3-109">Wdrażanie usługi sieci Web hello</span><span class="sxs-lookup"><span data-stu-id="158c3-109">Deploy hello Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="158c3-110">Witaj dostępu do usługi sieci Web</span><span class="sxs-lookup"><span data-stu-id="158c3-110">Access hello Web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<span data-ttu-id="158c3-111">Jedną z zalet hello przy użyciu usługi Azure Machine Learning Studio do tworzenia modeli uczenia maszyny jest więcej niż jeden typ modelu tootry możliwości hello jednocześnie w jednym eksperymentu i porównywania wyników hello.</span><span class="sxs-lookup"><span data-stu-id="158c3-111">One of hello benefits of using Azure Machine Learning Studio for creating machine learning models is hello ability tootry more than one type of model at a time in a single experiment and compare hello results.</span></span> <span data-ttu-id="158c3-112">Ten typ eksperymenty ułatwia hello najlepszego rozwiązania dla danego problemu.</span><span class="sxs-lookup"><span data-stu-id="158c3-112">This type of experimentation helps you find hello best solution for your problem.</span></span>

<span data-ttu-id="158c3-113">W eksperymencie hello możemy tworzony jest w tym przewodniku, firma Microsoft będzie utworzyć dwa rodzaje modeli a następnie porównaj ich oceniania toodecide wyniki który algorytm chcemy toouse w naszym końcowy eksperyment.</span><span class="sxs-lookup"><span data-stu-id="158c3-113">In hello experiment we're developing in this walkthrough, we'll create two different types of models and then compare their scoring results toodecide which algorithm we want toouse in our final experiment.</span></span>  

<span data-ttu-id="158c3-114">Istnieją różne modele, firma Microsoft może wyboru.</span><span class="sxs-lookup"><span data-stu-id="158c3-114">There are various models we could choose from.</span></span> <span data-ttu-id="158c3-115">toosee hello modeli dostępnych, rozwiń węzeł hello **Machine Learning** węzła w palecie modułów hello, a następnie rozwiń węzeł **zainicjować modelu** i węzły hello znajdujące się poniżej.</span><span class="sxs-lookup"><span data-stu-id="158c3-115">toosee hello models available, expand hello **Machine Learning** node in hello module palette, and then expand **Initialize Model** and hello nodes beneath it.</span></span> <span data-ttu-id="158c3-116">Dla celów hello tego eksperymentu, wybierzemy hello [maszyny wektorowa obsługa Two-Class] [ two-class-support-vector-machine] (SVM) i hello [Two-Class Boosted drzewa decyzyjnego] [ two-class-boosted-decision-tree] modułów.</span><span class="sxs-lookup"><span data-stu-id="158c3-116">For hello purposes of this experiment, we'll select hello [Two-Class Support Vector Machine][two-class-support-vector-machine] (SVM) and hello [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] modules.</span></span>    

> [!TIP]
> <span data-ttu-id="158c3-117">tooget dodatkową pomoc przy wyborze Algorytm uczenia maszynowego, które najlepiej pasujące do konkretnych problemów hello próbujesz toosolve, zobacz [jak toochoose algorytmów uczenia maszynowego Azure Microsoft](machine-learning-algorithm-choice.md).</span><span class="sxs-lookup"><span data-stu-id="158c3-117">tooget help deciding which Machine Learning algorithm best suits hello particular problem you're trying toosolve, see [How toochoose algorithms for Microsoft Azure Machine Learning](machine-learning-algorithm-choice.md).</span></span>
> 
> 

## <a name="train-hello-models"></a><span data-ttu-id="158c3-118">Modele hello pociągu</span><span class="sxs-lookup"><span data-stu-id="158c3-118">Train hello models</span></span>

<span data-ttu-id="158c3-119">Dodamy zarówno hello [Two-Class Boosted drzewa decyzyjnego] [ two-class-boosted-decision-tree] modułu i [maszyny wektorowa obsługa Two-Class] [ two-class-support-vector-machine] modułu, w tym eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="158c3-119">We'll add both hello [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module and [Two-Class Support Vector Machine][two-class-support-vector-machine] module in this experiment.</span></span>

### <a name="two-class-boosted-decision-tree"></a><span data-ttu-id="158c3-120">Two-Class Boosted algorytm</span><span class="sxs-lookup"><span data-stu-id="158c3-120">Two-Class Boosted Decision Tree</span></span>

<span data-ttu-id="158c3-121">Najpierw skonfiguruj hello boosted decyzji drzewa modelu.</span><span class="sxs-lookup"><span data-stu-id="158c3-121">First, let's set up hello boosted decision tree model.</span></span>

1. <span data-ttu-id="158c3-122">Znajdź hello [Two-Class Boosted drzewa decyzyjnego] [ two-class-boosted-decision-tree] modułu w palecie modułów hello i przeciągnij go na powitania kanwy.</span><span class="sxs-lookup"><span data-stu-id="158c3-122">Find hello [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module in hello module palette and drag it onto hello canvas.</span></span>

2. <span data-ttu-id="158c3-123">Znajdź hello [Train Model] [ train-model] modułu, przeciągnij je na kanwie hello, a następnie połącz dane wyjściowe hello hello [Two-Class Boosted drzewa decyzyjnego] [ two-class-boosted-decision-tree]toohello modułu pozostałych port wejściowy z hello [Train Model] [ train-model] modułu.</span><span class="sxs-lookup"><span data-stu-id="158c3-123">Find hello [Train Model][train-model] module, drag it onto hello canvas, and then connect hello output of hello [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module toohello left input port of hello [Train Model][train-model] module.</span></span>
   
   <span data-ttu-id="158c3-124">Witaj [Two-Class Boosted drzewa decyzyjnego] [ two-class-boosted-decision-tree] modułu inicjuje hello rodzajowy modelu i [Train Model] [ train-model] używa danych szkoleniowych tootrain hello modelu.</span><span class="sxs-lookup"><span data-stu-id="158c3-124">hello [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module initializes hello generic model, and [Train Model][train-model] uses training data tootrain hello model.</span></span> 

3. <span data-ttu-id="158c3-125">Połącz powitania po lewej stronie dane wyjściowe lewej hello [wykonanie skryptu języka R] [ execute-r-script] portu hello danych wejściowych modułu toohello prawo [Train Model] [ train-model] modułu (Firma Microsoft decyzje podejmowane w [kroku 3](machine-learning-walkthrough-3-create-new-experiment.md) tych danych hello toouse wskazówki pochodzące z powitania po lewej stronie powitania podziału danych modułu szkoleń).</span><span class="sxs-lookup"><span data-stu-id="158c3-125">Connect hello left output of hello left [Execute R Script][execute-r-script] module toohello right input port of hello [Train Model][train-model] module (we decided in [Step 3](machine-learning-walkthrough-3-create-new-experiment.md) of this walkthrough toouse hello data coming from hello left side of hello Split Data module for training).</span></span>
   
   > [!TIP]
   > <span data-ttu-id="158c3-126">Firma Microsoft nie ma potrzeby dwóch danych wejściowych hello i jeden hello elementy wyjściowe hello [wykonanie skryptu języka R] [ execute-r-script] modułu do tego eksperymentu, dlatego firma Microsoft może narazić je odłączyć.</span><span class="sxs-lookup"><span data-stu-id="158c3-126">We don't need two of hello inputs and one of hello outputs of hello [Execute R Script][execute-r-script] module for this experiment, so we can leave them unattached.</span></span> 
   > 
   > 

<span data-ttu-id="158c3-127">Ta część eksperymentu hello teraz wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="158c3-127">This portion of hello experiment now looks something like this:</span></span>  

![Uczenie modelu][1]

<span data-ttu-id="158c3-129">Teraz potrzebujemy tootell hello [Train Model] [ train-model] modułu czy chcemy hello modelu toopredict hello ryzyka kredytowego wartość.</span><span class="sxs-lookup"><span data-stu-id="158c3-129">Now we need tootell hello [Train Model][train-model] module that we want hello model toopredict hello Credit Risk value.</span></span>

1. <span data-ttu-id="158c3-130">Wybierz hello [Train Model] [ train-model] modułu.</span><span class="sxs-lookup"><span data-stu-id="158c3-130">Select hello [Train Model][train-model] module.</span></span> <span data-ttu-id="158c3-131">W hello **właściwości** okienku, kliknij przycisk **Uruchom selektor kolumn**.</span><span class="sxs-lookup"><span data-stu-id="158c3-131">In hello **Properties** pane, click **Launch column selector**.</span></span>

2. <span data-ttu-id="158c3-132">W hello **wybrać pojedynczą kolumnę** okna dialogowego, wpisz "ryzyko kredytowe" w polu wyszukiwania hello w obszarze **dostępne kolumny**, wybierz "Ryzyko kredytowe" poniżej i kliknij przycisk strzałki w prawo hello ( **>** ) toomove "Karty kredytowej ryzyka" zbyt**wybrane kolumny**.</span><span class="sxs-lookup"><span data-stu-id="158c3-132">In hello **Select a single column** dialog, type "credit risk" in hello search field under **Available Columns**, select "Credit risk" below, and click hello right arrow button (**>**) toomove "Credit risk" too**Selected Columns**.</span></span> 

    ![Wybierz kolumnę ryzyka kredytowego hello modułu Train Model hello][0]

3. <span data-ttu-id="158c3-134">Kliknij przycisk hello **OK** znacznik wyboru.</span><span class="sxs-lookup"><span data-stu-id="158c3-134">Click hello **OK** check mark.</span></span>

### <a name="two-class-support-vector-machine"></a><span data-ttu-id="158c3-135">Algorytm SVM dla problemu dwuklasowego</span><span class="sxs-lookup"><span data-stu-id="158c3-135">Two-Class Support Vector Machine</span></span>

<span data-ttu-id="158c3-136">Następnie skonfiguruj firma Microsoft hello SVM modelu.</span><span class="sxs-lookup"><span data-stu-id="158c3-136">Next, we set up hello SVM model.</span></span>  

<span data-ttu-id="158c3-137">Pierwszy, nieco wyjaśnienie SVM.</span><span class="sxs-lookup"><span data-stu-id="158c3-137">First, a little explanation about SVM.</span></span> <span data-ttu-id="158c3-138">Drzewa decyzyjne boosted działają prawidłowo w przypadku funkcji dowolnego typu.</span><span class="sxs-lookup"><span data-stu-id="158c3-138">Boosted decision trees work well with features of any type.</span></span> <span data-ttu-id="158c3-139">Jednak ponieważ moduł SVM hello generuje klasyfikatora liniowego, hello modelu, który generuje ma najlepsze błąd testu hello gdy wszystkie funkcje numeryczne hello samej skali.</span><span class="sxs-lookup"><span data-stu-id="158c3-139">However, since hello SVM module generates a linear classifier, hello model that it generates has hello best test error when all numeric features have hello same scale.</span></span> <span data-ttu-id="158c3-140">tooconvert cyfr toohello funkcje skalowania takie same, używamy transformację "Tanh" (z hello [normalizacji danych] [ normalize-data] modułu).</span><span class="sxs-lookup"><span data-stu-id="158c3-140">tooconvert all numeric features toohello same scale, we use a "Tanh" transformation (with hello [Normalize Data][normalize-data] module).</span></span> <span data-ttu-id="158c3-141">To przekształca naszych numery w zakresie hello [0,1].</span><span class="sxs-lookup"><span data-stu-id="158c3-141">This transforms our numbers into hello [0,1] range.</span></span> <span data-ttu-id="158c3-142">Moduł SVM Hello konwertuje ciąg funkcji toocategorical funkcje i następnie toobinary 0/1, dlatego firma Microsoft nie muszą toomanually transformacja funkcje ciągu.</span><span class="sxs-lookup"><span data-stu-id="158c3-142">hello SVM module converts string features toocategorical features and then toobinary 0/1 features, so we don't need toomanually transform string features.</span></span> <span data-ttu-id="158c3-143">Ponadto nie chcemy tootransform hello ryzyka kredytowego kolumna (kolumna 21) — jest liczbowego, ale jest wartość hello możemy uczony hello toopredict modelu, potrzebujemy tooleave ją samodzielnie.</span><span class="sxs-lookup"><span data-stu-id="158c3-143">Also, we don't want tootransform hello Credit Risk column (column 21) - it's numeric, but it's hello value we're training hello model toopredict, so we need tooleave it alone.</span></span>  

<span data-ttu-id="158c3-144">tooset model SVM hello, hello następujące:</span><span class="sxs-lookup"><span data-stu-id="158c3-144">tooset up hello SVM model, do hello following:</span></span>

1. <span data-ttu-id="158c3-145">Znajdź hello [maszyny wektorowa obsługa Two-Class] [ two-class-support-vector-machine] modułu w palecie modułów hello i przeciągnij go na powitania kanwy.</span><span class="sxs-lookup"><span data-stu-id="158c3-145">Find hello [Two-Class Support Vector Machine][two-class-support-vector-machine] module in hello module palette and drag it onto hello canvas.</span></span>

2. <span data-ttu-id="158c3-146">Powitania kliknij prawym przyciskiem myszy [Train Model] [ train-model] modułu, wybierz opcję **kopiowania**, a następnie kliknij prawym przyciskiem myszy hello kanwy i wybierz **Wklej**.</span><span class="sxs-lookup"><span data-stu-id="158c3-146">Right-click hello [Train Model][train-model] module, select **Copy**, and then right-click hello canvas and select **Paste**.</span></span> <span data-ttu-id="158c3-147">Witaj kopię hello [Train Model] [ train-model] moduł ma hello tego samego wyboru kolumny jako hello oryginalnego.</span><span class="sxs-lookup"><span data-stu-id="158c3-147">hello copy of hello [Train Model][train-model] module has hello same column selection as hello original.</span></span>

3. <span data-ttu-id="158c3-148">Połącz dane wyjściowe hello hello [maszyny wektorowa obsługa Two-Class] [ two-class-support-vector-machine] toohello modułu w lewo drugi port wejściowy z hello [Train Model] [ train-model] Moduł.</span><span class="sxs-lookup"><span data-stu-id="158c3-148">Connect hello output of hello [Two-Class Support Vector Machine][two-class-support-vector-machine] module toohello left input port of hello second [Train Model][train-model] module.</span></span>

4. <span data-ttu-id="158c3-149">Znajdź hello [normalizacji danych] [ normalize-data] modułu i przeciągnij go na powitania kanwy.</span><span class="sxs-lookup"><span data-stu-id="158c3-149">Find hello [Normalize Data][normalize-data] module and drag it onto hello canvas.</span></span>

5. <span data-ttu-id="158c3-150">Połącz powitania po lewej stronie dane wyjściowe lewej hello [wykonanie skryptu języka R] [ execute-r-script] wejścia modułu toohello tego modułu (powiadomienie, że hello port wyjściowy modułu mogą być połączone toomore niż inny moduł).</span><span class="sxs-lookup"><span data-stu-id="158c3-150">Connect hello left output of hello left [Execute R Script][execute-r-script] module toohello input of this module (notice that hello output port of a module may be connected toomore than one other module).</span></span>

6. <span data-ttu-id="158c3-151">Połącz hello pozostałych portem wyjściowym hello [normalizacji danych] [ normalize-data] prawo toohello modułu drugie dane wejściowe portu hello [Train Model] [ train-model] modułu.</span><span class="sxs-lookup"><span data-stu-id="158c3-151">Connect hello left output port of hello [Normalize Data][normalize-data] module toohello right input port of hello second [Train Model][train-model] module.</span></span>

<span data-ttu-id="158c3-152">Ta część naszego eksperyment powinien teraz wyglądać mniej więcej tak:</span><span class="sxs-lookup"><span data-stu-id="158c3-152">This portion of our experiment should now look something like this:</span></span>  

![Szkolenie hello drugim modelu][2]  

<span data-ttu-id="158c3-154">Teraz skonfigurować hello [normalizacji danych] [ normalize-data] modułu:</span><span class="sxs-lookup"><span data-stu-id="158c3-154">Now configure hello [Normalize Data][normalize-data] module:</span></span>

1. <span data-ttu-id="158c3-155">Kliknij przycisk tooselect hello [normalizacji danych] [ normalize-data] modułu.</span><span class="sxs-lookup"><span data-stu-id="158c3-155">Click tooselect hello [Normalize Data][normalize-data] module.</span></span> <span data-ttu-id="158c3-156">W hello **właściwości** okienku wybierz **Tanh** dla hello **metody przekształcania** parametru.</span><span class="sxs-lookup"><span data-stu-id="158c3-156">In hello **Properties** pane, select **Tanh** for hello **Transformation method** parameter.</span></span>

2. <span data-ttu-id="158c3-157">Kliknij przycisk **Uruchom selektor kolumn**, wybierz opcję "Brak kolumn" dla **od**, wybierz pozycję **Include** hello pierwszej listy rozwijanej, wybierz **typ kolumny**w hello drugi listy rozwijanej i wybierz **liczbowych** w hello trzeci listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="158c3-157">Click **Launch column selector**, select "No columns" for **Begin With**, select **Include** in hello first dropdown, select **column type** in hello second dropdown, and select **Numeric** in hello third dropdown.</span></span> <span data-ttu-id="158c3-158">To ustawienie określa przekształcone wszystkich hello liczbowych kolumn (i tylko numeryczne).</span><span class="sxs-lookup"><span data-stu-id="158c3-158">This specifies that all hello numeric columns (and only numeric) are transformed.</span></span>

3. <span data-ttu-id="158c3-159">Kliknij przycisk hello toohello znak plus (+) bezpośrednio z tego wiersza — spowoduje to utworzenie wiersza listę rozwijaną.</span><span class="sxs-lookup"><span data-stu-id="158c3-159">Click hello plus sign (+) toohello right of this row - this creates a row of dropdowns.</span></span> <span data-ttu-id="158c3-160">Wybierz **wykluczyć** hello pierwszej listy rozwijanej, wybierz **nazwy kolumn** w hello drugi listy rozwijanej, a następnie wprowadź "Ryzyko kredytowe" w polu tekstowym hello.</span><span class="sxs-lookup"><span data-stu-id="158c3-160">Select **Exclude** in hello first dropdown, select **column names** in hello second dropdown, and enter "Credit risk" in hello text field.</span></span> <span data-ttu-id="158c3-161">Określa, należy ją ignorować tej kolumny ryzyka kredytowego hello (potrzebujemy toodo to ponieważ ta kolumna jest liczbowych i tak może zostać przekształcone, jeśli firma Microsoft nie go wykluczyć).</span><span class="sxs-lookup"><span data-stu-id="158c3-161">This specifies that hello Credit Risk column should be ignored (we need toodo this because this column is numeric and so would be transformed if we didn't exclude it).</span></span>

4. <span data-ttu-id="158c3-162">Kliknij przycisk hello **OK** znacznik wyboru.</span><span class="sxs-lookup"><span data-stu-id="158c3-162">Click hello **OK** check mark.</span></span>  

    ![Wybierz kolumny hello normalizacji danych modułu][5]

<span data-ttu-id="158c3-164">Witaj [normalizacji danych] [ normalize-data] modułu jest teraz tooperform zestaw transformację Tanh na wszystkich kolumn liczbowych, z wyjątkiem hello ryzyka kredytowego.</span><span class="sxs-lookup"><span data-stu-id="158c3-164">hello [Normalize Data][normalize-data] module is now set tooperform a Tanh transformation on all numeric columns except for hello Credit Risk column.</span></span>  

## <a name="score-and-evaluate-hello-models"></a><span data-ttu-id="158c3-165">Wynik i ocena hello modeli</span><span class="sxs-lookup"><span data-stu-id="158c3-165">Score and evaluate hello models</span></span>

<span data-ttu-id="158c3-166">Używamy hello testowanie danych, który został oddzielony przez hello [podziału danych] [ split] tooscore modułu naszych przeszkolone modeli.</span><span class="sxs-lookup"><span data-stu-id="158c3-166">We use hello testing data that was separated out by hello [Split Data][split] module tooscore our trained models.</span></span> <span data-ttu-id="158c3-167">Firma Microsoft następnie porównaj wyniki hello hello dwa modele toosee który wygenerować lepsze wyniki.</span><span class="sxs-lookup"><span data-stu-id="158c3-167">We can then compare hello results of hello two models toosee which generated better results.</span></span>  

### <a name="add-hello-score-model-modules"></a><span data-ttu-id="158c3-168">Dodaj moduły Score Model hello</span><span class="sxs-lookup"><span data-stu-id="158c3-168">Add hello Score Model modules</span></span>

1. <span data-ttu-id="158c3-169">Znajdź hello [Score Model] [ score-model] modułu i przeciągnij go na powitania kanwy.</span><span class="sxs-lookup"><span data-stu-id="158c3-169">Find hello [Score Model][score-model] module and drag it onto hello canvas.</span></span>

2. <span data-ttu-id="158c3-170">Połącz hello [Train Model] [ train-model] moduł, który został podłączony toohello [Two-Class Boosted drzewa decyzyjnego] [ two-class-boosted-decision-tree] wejścia po lewej stronie toohello modułu Port hello [Score Model] [ score-model] modułu.</span><span class="sxs-lookup"><span data-stu-id="158c3-170">Connect hello [Train Model][train-model] module that's connected toohello [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module toohello left input port of hello [Score Model][score-model] module.</span></span>

3. <span data-ttu-id="158c3-171">Połącz prawo hello [wykonanie skryptu języka R] [ execute-r-script] prawo toohello modułu (danych testowych) danych wejściowych portu hello [Score Model] [ score-model] modułu.</span><span class="sxs-lookup"><span data-stu-id="158c3-171">Connect hello right [Execute R Script][execute-r-script] module (our testing data) toohello right input port of hello [Score Model][score-model] module.</span></span>

    ![Moduł score Model połączenia][6]
   
   <span data-ttu-id="158c3-173">Witaj [Score Model] [ score-model] modułu teraz może zająć hello środki informacji z hello testowanie danych, uruchom go za pomocą modelu hello i porównaj hello prognoz modelu hello generuje z rzeczywistego hello karty kredytowej ryzyka Kolumna w hello testowanie danych.</span><span class="sxs-lookup"><span data-stu-id="158c3-173">hello [Score Model][score-model] module can now take hello credit information from hello testing data, run it through hello model, and compare hello predictions hello model generates with hello actual credit risk column in hello testing data.</span></span>

4. <span data-ttu-id="158c3-174">Skopiuj i Wklej hello [Score Model] [ score-model] toocreate modułu drugiej kopii.</span><span class="sxs-lookup"><span data-stu-id="158c3-174">Copy and paste hello [Score Model][score-model] module toocreate a second copy.</span></span>

5. <span data-ttu-id="158c3-175">Połącz dane wyjściowe hello hello SVM modelu (to znaczy hello output portu hello [Train Model] [ train-model] moduł, który został podłączony toohello [maszyny wektorowa obsługa Two-Class] [ two-class-support-vector-machine] modułu) toohello drugie dane wejściowe portu hello [Score Model] [ score-model] modułu.</span><span class="sxs-lookup"><span data-stu-id="158c3-175">Connect hello output of hello SVM model (that is, hello output port of hello [Train Model][train-model] module that's connected toohello [Two-Class Support Vector Machine][two-class-support-vector-machine] module) toohello input port of hello second [Score Model][score-model] module.</span></span>

6. <span data-ttu-id="158c3-176">Model SVM hello zostały toodo hello tych samych danych test toohello przekształcania, jak robiliśmy toohello danych szkoleniowych.</span><span class="sxs-lookup"><span data-stu-id="158c3-176">For hello SVM model, we have toodo hello same transformation toohello test data as we did toohello training data.</span></span> <span data-ttu-id="158c3-177">Dlatego skopiuj i Wklej hello [normalizacji danych] [ normalize-data] toocreate modułu drugiej kopii i podłącz go prawo toohello [wykonanie skryptu języka R] [ execute-r-script] modułu.</span><span class="sxs-lookup"><span data-stu-id="158c3-177">So copy and paste hello [Normalize Data][normalize-data] module toocreate a second copy and connect it toohello right [Execute R Script][execute-r-script] module.</span></span>

7. <span data-ttu-id="158c3-178">Drugie połączenie powitania po lewej stronie dane wyjściowe hello [normalizacji danych] [ normalize-data] prawo toohello modułu drugie dane wejściowe portu hello [Score Model] [ score-model] Moduł.</span><span class="sxs-lookup"><span data-stu-id="158c3-178">Connect hello left output of hello second [Normalize Data][normalize-data] module toohello right input port of hello second [Score Model][score-model] module.</span></span>

    ![Zarówno modułów Score Model połączenia][7]

### <a name="add-hello-evaluate-model-module"></a><span data-ttu-id="158c3-180">Dodawanie modułu Evaluate Model hello</span><span class="sxs-lookup"><span data-stu-id="158c3-180">Add hello Evaluate Model module</span></span>

<span data-ttu-id="158c3-181">tooevaluate Witaj dwie wyników oceniania i porównaj je, używamy [Evaluate Model] [ evaluate-model] modułu.</span><span class="sxs-lookup"><span data-stu-id="158c3-181">tooevaluate hello two scoring results and compare them, we use an [Evaluate Model][evaluate-model] module.</span></span>  

1. <span data-ttu-id="158c3-182">Znajdź hello [Evaluate Model] [ evaluate-model] modułu i przeciągnij go na powitania kanwy.</span><span class="sxs-lookup"><span data-stu-id="158c3-182">Find hello [Evaluate Model][evaluate-model] module and drag it onto hello canvas.</span></span>

2. <span data-ttu-id="158c3-183">Połącz port wyjściowy hello hello [Score Model] [ score-model] moduł skojarzony z hello boosted decyzji drzewa po lewej toohello modelu danych wejściowych portu hello [Evaluate Model] [ evaluate-model] modułu.</span><span class="sxs-lookup"><span data-stu-id="158c3-183">Connect hello output port of hello [Score Model][score-model] module associated with hello boosted decision tree model toohello left input port of hello [Evaluate Model][evaluate-model] module.</span></span>

3. <span data-ttu-id="158c3-184">Połącz hello innych [Score Model] [ score-model] toohello modułu prawo wejściowych portu.</span><span class="sxs-lookup"><span data-stu-id="158c3-184">Connect hello other [Score Model][score-model] module toohello right input port.</span></span>  

    ![Ocena modelu modułu połączone][8]

### <a name="run-hello-experiment-and-check-hello-results"></a><span data-ttu-id="158c3-186">Uruchom eksperyment hello i hello wyniki sprawdzenia</span><span class="sxs-lookup"><span data-stu-id="158c3-186">Run hello experiment and check hello results</span></span>

<span data-ttu-id="158c3-187">toorun hello eksperyment, kliknij przycisk hello **Uruchom** znajdujący się poniżej hello kanwy.</span><span class="sxs-lookup"><span data-stu-id="158c3-187">toorun hello experiment, click hello **RUN** button below hello canvas.</span></span> <span data-ttu-id="158c3-188">Może upłynąć kilka minut.</span><span class="sxs-lookup"><span data-stu-id="158c3-188">It may take a few minutes.</span></span> <span data-ttu-id="158c3-189">Wskaźnik Obracająca dla każdego modułu pokazuje, że jest uruchomiona, i czym wyświetlany po zakończeniu modułu hello zielony znacznik wyboru.</span><span class="sxs-lookup"><span data-stu-id="158c3-189">A spinning indicator on each module shows that it's running, and then a green check mark shows when hello module is finished.</span></span> <span data-ttu-id="158c3-190">Jeśli zaznaczono wszystkie moduły hello eksperymentu hello zakończył działanie.</span><span class="sxs-lookup"><span data-stu-id="158c3-190">When all hello modules have a check mark, hello experiment has finished running.</span></span>

<span data-ttu-id="158c3-191">Hello eksperyment powinien teraz wyglądać mniej więcej tak:</span><span class="sxs-lookup"><span data-stu-id="158c3-191">hello experiment should now look something like this:</span></span>  

![Ocena obu modeli][3]

<span data-ttu-id="158c3-193">toocheck hello wyników, kliknij port wyjściowy hello hello [Evaluate Model] [ evaluate-model] moduł i zaznacz **Visualize**.</span><span class="sxs-lookup"><span data-stu-id="158c3-193">toocheck hello results, click hello output port of hello [Evaluate Model][evaluate-model] module and select **Visualize**.</span></span>  

<span data-ttu-id="158c3-194">Witaj [Evaluate Model] [ evaluate-model] modułu tworzy parę krzywych i metryki, które pozwalają wyniki hello toocompare dwa modele scored hello.</span><span class="sxs-lookup"><span data-stu-id="158c3-194">hello [Evaluate Model][evaluate-model] module produces a pair of curves and metrics that allow you toocompare hello results of hello two scored models.</span></span> <span data-ttu-id="158c3-195">Można wyświetlić wyniki hello jako krzywych cech Operator odbiornika (ROC), krzywych dokładności/wycofania lub krzywych przyrostu.</span><span class="sxs-lookup"><span data-stu-id="158c3-195">You can view hello results as Receiver Operator Characteristic (ROC) curves, Precision/Recall curves, or Lift curves.</span></span> <span data-ttu-id="158c3-196">Dodatkowe dane wyświetlane obejmuje macierz pomyłek, łączne wartości dla hello obszarze hello krzywej (AUC) i innych metryk.</span><span class="sxs-lookup"><span data-stu-id="158c3-196">Additional data displayed includes a confusion matrix, cumulative values for hello area under hello curve (AUC), and other metrics.</span></span> <span data-ttu-id="158c3-197">Można zmienić wartości progowej hello przez przenoszenie hello suwak w lewo lub w prawo i zobacz, jak wpływa na powitania zbiór metryki.</span><span class="sxs-lookup"><span data-stu-id="158c3-197">You can change hello threshold value by moving hello slider left or right and see how it affects hello set of metrics.</span></span>  

<span data-ttu-id="158c3-198">Kliknij toohello rogu wykresu hello **oceniane zestawu danych** lub **oceniane toocompare zestawu danych** toohighlight hello skojarzone krzywej i toodisplay hello skojarzone metryki poniżej.</span><span class="sxs-lookup"><span data-stu-id="158c3-198">toohello right of hello graph, click **Scored dataset** or **Scored dataset toocompare** toohighlight hello associated curve and toodisplay hello associated metrics below.</span></span> <span data-ttu-id="158c3-199">Legenda hello krzywych na powitania, "Oceniane zestawu danych" odpowiada toohello pozostałych port wejściowy z hello [Evaluate Model] [ evaluate-model] moduł — w tym przypadku jest to hello boosted decyzji drzewa modelu.</span><span class="sxs-lookup"><span data-stu-id="158c3-199">In hello legend for hello curves, "Scored dataset" corresponds toohello left input port of hello [Evaluate Model][evaluate-model] module - in our case, this is hello boosted decision tree model.</span></span> <span data-ttu-id="158c3-200">"Oceniane toocompare zestawu danych" odpowiada prawy port wejściowy toohello - hello SVM modelu w tym przypadku.</span><span class="sxs-lookup"><span data-stu-id="158c3-200">"Scored dataset toocompare" corresponds toohello right input port - hello SVM model in our case.</span></span> <span data-ttu-id="158c3-201">Po kliknięciu jednego z tych etykiet zostanie wyróżniona krzywej hello modelu i metryki odpowiedniego hello są wyświetlane, pokazane na powitania po grafiki.</span><span class="sxs-lookup"><span data-stu-id="158c3-201">When you click one of these labels, hello curve for that model is highlighted and hello corresponding metrics are displayed, as shown in hello following graphic.</span></span>  

![Krzywe ROC dla modeli][4]

<span data-ttu-id="158c3-203">Badanie tych wartości, można zdecydować, model, który jest najbliższy toogiving hello wyników, którego szukasz.</span><span class="sxs-lookup"><span data-stu-id="158c3-203">By examining these values, you can decide which model is closest toogiving you hello results you're looking for.</span></span> <span data-ttu-id="158c3-204">Możesz wrócić do poprzedniej strony i iterację eksperymentu, zmieniając wartości parametrów w różne modele hello.</span><span class="sxs-lookup"><span data-stu-id="158c3-204">You can go back and iterate on your experiment by changing parameter values in hello different models.</span></span> 

<span data-ttu-id="158c3-205">Witaj nauki i grafik interpretowanie te wyniki i dostrajania wydajności modelu hello jest hello poza zakres tego przewodnika.</span><span class="sxs-lookup"><span data-stu-id="158c3-205">hello science and art of interpreting these results and tuning hello model performance is outside hello scope of this walkthrough.</span></span> <span data-ttu-id="158c3-206">Aby uzyskać dodatkową pomoc mogą odczytać hello następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="158c3-206">For additional help, you might read hello following articles:</span></span>
- [<span data-ttu-id="158c3-207">Jak tooevaluate modelu wydajności w usłudze Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="158c3-207">How tooevaluate model performance in Azure Machine Learning</span></span>](machine-learning-evaluate-model-performance.md)
- [<span data-ttu-id="158c3-208">Wybierz parametry toooptimize algorytmy w usłudze Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="158c3-208">Choose parameters toooptimize your algorithms in Azure Machine Learning</span></span>](machine-learning-algorithm-parameters-optimize.md)
- [<span data-ttu-id="158c3-209">Interpretowanie wyników modelu w usłudze Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="158c3-209">Interpret model results in Azure Machine Learning</span></span>](machine-learning-interpret-model-results.md)

> [!TIP]
> <span data-ttu-id="158c3-210">Każdym uruchomieniu eksperymentu hello rekord tego iteracji jest przechowywany w hello Uruchom historii.</span><span class="sxs-lookup"><span data-stu-id="158c3-210">Each time you run hello experiment a record of that iteration is kept in hello Run History.</span></span> <span data-ttu-id="158c3-211">Można wyświetlić te iteracji i zwracać tooany z nich, klikając **WYŚWIETL HISTORIĘ URUCHAMIANIA** poniżej hello kanwy.</span><span class="sxs-lookup"><span data-stu-id="158c3-211">You can view these iterations, and return tooany of them, by clicking **VIEW RUN HISTORY** below hello canvas.</span></span> <span data-ttu-id="158c3-212">Możesz również kliknąć **uprzedniego uruchomienia** w hello **właściwości** iteracji toohello tooreturn okienko poprzedzającego hello mają otwarte.</span><span class="sxs-lookup"><span data-stu-id="158c3-212">You can also click **Prior Run** in hello **Properties** pane tooreturn toohello iteration immediately preceding hello one you have open.</span></span>
> 
> <span data-ttu-id="158c3-213">Można utworzyć kopię dowolną iterację eksperymentu, klikając **SAVE AS** poniżej hello kanwy.</span><span class="sxs-lookup"><span data-stu-id="158c3-213">You can make a copy of any iteration of your experiment by clicking **SAVE AS** below hello canvas.</span></span> 
> <span data-ttu-id="158c3-214">Użyj eksperymentu hello **Podsumowanie** i **opis** tookeep właściwości rekordu zawierającego co podjęto w Twojej iteracje eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="158c3-214">Use hello experiment's **Summary** and **Description** properties tookeep a record of what you've tried in your experiment iterations.</span></span>
> 
> <span data-ttu-id="158c3-215">Aby uzyskać więcej informacji, zobacz [Zarządzanie iteracjami eksperymentów w usłudze Azure Machine Learning Studio](machine-learning-manage-experiment-iterations.md).</span><span class="sxs-lookup"><span data-stu-id="158c3-215">For more details, see [Manage experiment iterations in Azure Machine Learning Studio](machine-learning-manage-experiment-iterations.md).</span></span>  
> 
> 

- - -
<span data-ttu-id="158c3-216">**Następnie: [wdrażanie usługi sieci web hello](machine-learning-walkthrough-5-publish-web-service.md)**</span><span class="sxs-lookup"><span data-stu-id="158c3-216">**Next: [Deploy hello web service](machine-learning-walkthrough-5-publish-web-service.md)**</span></span>

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
