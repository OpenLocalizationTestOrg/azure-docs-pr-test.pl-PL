---
title: 'Krok 3: Tworzenie nowego eksperymentu uczenia maszynowego | Dokumentacja firmy Microsoft'
description: "Krok 3 opracowanie wskazówki rozwiązanie predykcyjne: Tworzenie nowego eksperymentu uczenia w usłudze Azure Machine Learning Studio."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 660e3c27-55ef-4c33-a4e9-dff4d1224630
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: cd410316910bce76f5c915c06e83b24c034481b7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="walkthrough-step-3-create-a-new-azure-machine-learning-experiment"></a><span data-ttu-id="59da8-103">Przewodnik, krok 3. Tworzenie nowego eksperymentu usługi Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="59da8-103">Walkthrough Step 3: Create a new Azure Machine Learning experiment</span></span>
<span data-ttu-id="59da8-104">Jest to trzeci krok wskazówki, [tworzenie rozwiązania analizy predykcyjnej w usłudze Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="59da8-104">This is the third step of the walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. [<span data-ttu-id="59da8-105">Tworzenie obszaru roboczego usługi Machine Learning</span><span class="sxs-lookup"><span data-stu-id="59da8-105">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="59da8-106">Przekazywanie istniejących danych</span><span class="sxs-lookup"><span data-stu-id="59da8-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. <span data-ttu-id="59da8-107">**Tworzenie nowego eksperymentu**</span><span class="sxs-lookup"><span data-stu-id="59da8-107">**Create a new experiment**</span></span>
4. [<span data-ttu-id="59da8-108">Nauczanie i ocena modeli</span><span class="sxs-lookup"><span data-stu-id="59da8-108">Train and evaluate the models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="59da8-109">Wdrażanie usługi sieci Web</span><span class="sxs-lookup"><span data-stu-id="59da8-109">Deploy the Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="59da8-110">Dostęp do usługi sieci Web</span><span class="sxs-lookup"><span data-stu-id="59da8-110">Access the Web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<span data-ttu-id="59da8-111">Następnym krokiem w ramach tego przewodnika jest tworzenie eksperymentu w usłudze Machine Learning Studio, która używa zestawu danych, które możemy przekazać.</span><span class="sxs-lookup"><span data-stu-id="59da8-111">The next step in this walkthrough is to create an experiment in Machine Learning Studio that uses the dataset we uploaded.</span></span>  

1. <span data-ttu-id="59da8-112">W Studio, kliknij przycisk **+ nowy** w dolnej części okna.</span><span class="sxs-lookup"><span data-stu-id="59da8-112">In Studio, click **+NEW** at the bottom of the window.</span></span>
2. <span data-ttu-id="59da8-113">Wybierz **EKSPERYMENTU**, a następnie wybierz pozycję "Pusty eksperyment".</span><span class="sxs-lookup"><span data-stu-id="59da8-113">Select **EXPERIMENT**, and then select "Blank Experiment".</span></span> 

    ![Tworzenie nowego eksperymentu][0]

2. <span data-ttu-id="59da8-115">Wybierz domyślną nazwę eksperymentu w górnej części obszaru roboczego i zmień jego nazwę, wpisując tekst opisowy.</span><span class="sxs-lookup"><span data-stu-id="59da8-115">Select the default experiment name at the top of the canvas and rename it to something meaningful.</span></span>

    ![Zmień nazwę eksperymentu][5]
   
   > [!TIP]
   > <span data-ttu-id="59da8-117">Dobrym rozwiązaniem, aby wypełnić jest **Podsumowanie** i **opis** do eksperymentu w **właściwości** okienka.</span><span class="sxs-lookup"><span data-stu-id="59da8-117">It's a good practice to fill in **Summary** and **Description** for the experiment in the **Properties** pane.</span></span> <span data-ttu-id="59da8-118">Te właściwości zapewniają możliwość dokumentu eksperyment, dzięki czemu każdy, kto analizuje go później będzie zrozumiałe, cele i metodologii.</span><span class="sxs-lookup"><span data-stu-id="59da8-118">These properties give you the chance to document the experiment so that anyone who looks at it later will understand your goals and methodology.</span></span>
   > 
   > ![Właściwości eksperymentu][6]
   > 
3. <span data-ttu-id="59da8-120">Na palecie modułów z lewej strony obszaru roboczego eksperymentu, rozwiń węzeł **zapisane zestawów danych**.</span><span class="sxs-lookup"><span data-stu-id="59da8-120">In the module palette to the left of the experiment canvas, expand **Saved Datasets**.</span></span>
4. <span data-ttu-id="59da8-121">Znaleźć zestaw danych został utworzony w obszarze **Moje zestawów danych** i przeciągnij go do obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="59da8-121">Find the dataset you created under **My Datasets** and drag it onto the canvas.</span></span> <span data-ttu-id="59da8-122">Możesz również znaleźć zestaw danych, wprowadzając nazwę w **wyszukiwania** pole powyżej palety.</span><span class="sxs-lookup"><span data-stu-id="59da8-122">You can also find the dataset by entering the name in the **Search** box above the palette.</span></span>  

    ![Dodaj zestaw danych do eksperymentu][7]

## <a name="prepare-the-data"></a><span data-ttu-id="59da8-124">Przygotowanie danych</span><span class="sxs-lookup"><span data-stu-id="59da8-124">Prepare the data</span></span>
<span data-ttu-id="59da8-125">Można wyświetlić pierwszych 100 wierszy danych i niektóre informacje statystyczne dla całego zestawu danych: kliknij port wyjściowy zestaw danych (małe koło u dołu) i wybierz **Visualize**.</span><span class="sxs-lookup"><span data-stu-id="59da8-125">You can view the first 100 rows of the data and some statistical information for the whole dataset: Click the output port of the dataset (the small circle at the bottom) and select **Visualize**.</span></span>  

<span data-ttu-id="59da8-126">Ponieważ plik danych nie został dostarczony z nagłówków kolumn, Studio udostępnił ogólnego nagłówki (Col1, Col2, *itp.*).</span><span class="sxs-lookup"><span data-stu-id="59da8-126">Because the data file didn't come with column headings, Studio has provided generic headings (Col1, Col2, *etc.*).</span></span> <span data-ttu-id="59da8-127">Dobrym nagłówki nie są niezbędne do tworzenia modelu, ale to na łatwiejsze do pracy z danymi w eksperymencie.</span><span class="sxs-lookup"><span data-stu-id="59da8-127">Good headings aren't essential to creating a model, but they make it easier to work with the data in the experiment.</span></span> <span data-ttu-id="59da8-128">Ponadto możemy po pewnym czasie publikowania tego modelu w usłudze sieci web, nagłówki zidentyfikować kolumny do użytkownika usługi.</span><span class="sxs-lookup"><span data-stu-id="59da8-128">Also, when we eventually publish this model in a web service, the headings help identify the columns to the user of the service.</span></span>  

<span data-ttu-id="59da8-129">Można dodać nagłówków kolumn za pomocą [edytowanie metadanych] [ edit-metadata] modułu.</span><span class="sxs-lookup"><span data-stu-id="59da8-129">We can add column headings using the [Edit Metadata][edit-metadata] module.</span></span>
<span data-ttu-id="59da8-130">Możesz użyć [edytowanie metadanych] [ edit-metadata] modułu, aby zmienić metadane skojarzone z zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="59da8-130">You use the [Edit Metadata][edit-metadata] module to change metadata associated with a dataset.</span></span> <span data-ttu-id="59da8-131">W takim przypadku stosujemy go udostępnia więcej przyjazne nazwy dla nagłówków kolumn.</span><span class="sxs-lookup"><span data-stu-id="59da8-131">In this case, we use it to provide more friendly names for column headings.</span></span> 

<span data-ttu-id="59da8-132">Aby użyć [edytowanie metadanych][edit-metadata], należy najpierw określić, które kolumny do zmodyfikowania (w tym przypadku wszystkie z nich.) Następnie określ akcję do wykonania na podstawie tych kolumn (w tym przypadku zmiana nagłówków kolumn.)</span><span class="sxs-lookup"><span data-stu-id="59da8-132">To use [Edit Metadata][edit-metadata], you first specify which columns to modify (in this case, all of them.) Next, you specify the action to be performed on those columns (in this case, changing column headings.)</span></span>

1. <span data-ttu-id="59da8-133">Na palecie modułów, wpisz "metadanych" **wyszukiwania** pole.</span><span class="sxs-lookup"><span data-stu-id="59da8-133">In the module palette, type "metadata" in the **Search** box.</span></span> <span data-ttu-id="59da8-134">[Edytowanie metadanych] [ edit-metadata] pojawia się na liście modułów.</span><span class="sxs-lookup"><span data-stu-id="59da8-134">The [Edit Metadata][edit-metadata] appears in the module list.</span></span>

2. <span data-ttu-id="59da8-135">Kliknij i przeciągnij [edytowanie metadanych] [ edit-metadata] modułu kanwę i upuść ją poniżej dodaliśmy wcześniej zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="59da8-135">Click and drag the [Edit Metadata][edit-metadata] module onto the canvas and drop it below the dataset we added earlier.</span></span>

3. <span data-ttu-id="59da8-136">Zestaw danych, aby połączyć [edytowanie metadanych][edit-metadata]: kliknij port wyjściowy zestaw danych (małe koło w dolnej części zestawu danych), przeciągnij, aby port wejściowy z [edytowanie metadanych] [ edit-metadata] (małe koło w górnej części modułu) następnie zwolnij przycisk myszy.</span><span class="sxs-lookup"><span data-stu-id="59da8-136">Connect the dataset to the [Edit Metadata][edit-metadata]: click the output port of the dataset (the small circle at the bottom of the dataset), drag to the input port of [Edit Metadata][edit-metadata] (the small circle at the top of the module), then release the mouse button.</span></span> <span data-ttu-id="59da8-137">Zestaw danych i modułu pozostały połączone, nawet w przypadku przenoszenia jednej na kanwie.</span><span class="sxs-lookup"><span data-stu-id="59da8-137">The dataset and module remain connected even if you move either around on the canvas.</span></span>
   
   <span data-ttu-id="59da8-138">Eksperyment powinien teraz wyglądać mniej więcej tak:</span><span class="sxs-lookup"><span data-stu-id="59da8-138">The experiment should now look something like this:</span></span>  
   
   ![Dodawanie metadanych edycji][1]
   
   <span data-ttu-id="59da8-140">Czerwony wykrzyknik wskazuje, że firma Microsoft nie zostało to jeszcze ustawiony właściwości dla tego modułu.</span><span class="sxs-lookup"><span data-stu-id="59da8-140">The red exclamation mark indicates that we haven't set the properties for this module yet.</span></span> <span data-ttu-id="59da8-141">Robimy tego dalej.</span><span class="sxs-lookup"><span data-stu-id="59da8-141">We'll do that next.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="59da8-142">Aby dodać komentarz do modułu, kliknij dwukrotnie moduł i wpisz tekst.</span><span class="sxs-lookup"><span data-stu-id="59da8-142">You can add a comment to a module by double-clicking the module and entering text.</span></span> <span data-ttu-id="59da8-143">Pozwoli to od razu sprawdzić rolę modułu w eksperymencie.</span><span class="sxs-lookup"><span data-stu-id="59da8-143">This can help you see at a glance what the module is doing in your experiment.</span></span> <span data-ttu-id="59da8-144">W takim przypadku kliknij dwukrotnie [edytowanie metadanych] [ edit-metadata] moduł i wpisz komentarz "Dodaj nagłówki kolumn".</span><span class="sxs-lookup"><span data-stu-id="59da8-144">In this case, double-click the [Edit Metadata][edit-metadata] module and type the comment "Add column headings".</span></span> <span data-ttu-id="59da8-145">Kliknij gdziekolwiek na kanwę, aby zamknąć okno tekstu.</span><span class="sxs-lookup"><span data-stu-id="59da8-145">Click anywhere else on the canvas to close the text box.</span></span> <span data-ttu-id="59da8-146">Aby wyświetlić komentarz, kliknij strzałkę w dół w module.</span><span class="sxs-lookup"><span data-stu-id="59da8-146">To display the comment, click the down-arrow on the module.</span></span>
   > 
   > ![Edytuj moduł metadanych z komentarzem dodane][8]
   > 
4. <span data-ttu-id="59da8-148">Wybierz [edytowanie metadanych][edit-metadata], a następnie w **właściwości** kliknij w okienku po prawej stronie kanwy **Uruchom selektor kolumn**.</span><span class="sxs-lookup"><span data-stu-id="59da8-148">Select [Edit Metadata][edit-metadata], and in the **Properties** pane to the right of the canvas, click **Launch column selector**.</span></span>

5. <span data-ttu-id="59da8-149">W **wybierz kolumny** okno dialogowe, wybierz wszystkie wiersze w **dostępne kolumny** i kliknij przycisk > Aby przenieść je na **wybrane kolumny**.</span><span class="sxs-lookup"><span data-stu-id="59da8-149">In the **Select columns** dialog, select all the rows in **Available Columns** and click > to move them to **Selected Columns**.</span></span>
   <span data-ttu-id="59da8-150">Okno dialogowe powinien wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="59da8-150">The dialog should look like this:</span></span>

   ![Selektor kolumn z wybrano wszystkich kolumn][2]

6. <span data-ttu-id="59da8-152">Kliknij przycisk **OK** znacznik wyboru.</span><span class="sxs-lookup"><span data-stu-id="59da8-152">Click the **OK** check mark.</span></span>

7. <span data-ttu-id="59da8-153">W **właściwości** okienka, poszukaj **nowych nazw kolumn** parametru.</span><span class="sxs-lookup"><span data-stu-id="59da8-153">Back in the **Properties** pane, look for the **New column names** parameter.</span></span> <span data-ttu-id="59da8-154">W tym miejscu wprowadź listę nazw 21 kolumn w zestawie danych, oddzielonych przecinkami i kolejność kolumn.</span><span class="sxs-lookup"><span data-stu-id="59da8-154">In this field, enter a list of names for the 21 columns in the dataset, separated by commas and in column order.</span></span> <span data-ttu-id="59da8-155">Można uzyskać nazwy kolumn w dokumentacji zestawu danych w witrynie sieci Web UCI, lub dla wygody można skopiować i wkleić poniżej:</span><span class="sxs-lookup"><span data-stu-id="59da8-155">You can obtain the columns names from the dataset documentation on the UCI website, or for convenience you can copy and paste the following list:</span></span>  
   
       Status of checking account, Duration in months, Credit history, Purpose, Credit amount, Savings account/bond, Present employment since, Installment rate in percentage of disposable income, Personal status and sex, Other debtors, Present residence since, Property, Age in years, Other installment plans, Housing, Number of existing credits, Job, Number of people providing maintenance for, Telephone, Foreign worker, Credit risk  
   
   <span data-ttu-id="59da8-156">W okienku właściwości wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="59da8-156">The Properties pane looks like this:</span></span>
   
   ![Właściwości metadanych edycji][3]

> [!TIP]
> <span data-ttu-id="59da8-158">Jeśli chcesz sprawdzić nagłówki kolumn, należy uruchomić eksperyment (kliknij **Uruchom** poniżej obszaru roboczego eksperymentu).</span><span class="sxs-lookup"><span data-stu-id="59da8-158">If you want to verify the column headings, run the experiment (click **RUN** below the experiment canvas).</span></span> <span data-ttu-id="59da8-159">Po zakończeniu pracy (zielony znacznik wyboru jest wyświetlane na [edytowanie metadanych][edit-metadata]), kliknij port wyjściowy [edytowanie metadanych] [ edit-metadata] modułu, i wybierz **Visualize**.</span><span class="sxs-lookup"><span data-stu-id="59da8-159">When it finishes running (a green check mark appears on [Edit Metadata][edit-metadata]), click the output port of the [Edit Metadata][edit-metadata] module, and select **Visualize**.</span></span> <span data-ttu-id="59da8-160">Dane wyjściowe każdy moduł jest widoczny w taki sam sposób, aby wyświetlić postęp danych za pośrednictwem eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="59da8-160">You can view the output of any module in the same way to view the progress of the data through the experiment.</span></span>
> 
> 

## <a name="create-training-and-test-datasets"></a><span data-ttu-id="59da8-161">Tworzenie szkolenia i testowanie zbiory danych</span><span class="sxs-lookup"><span data-stu-id="59da8-161">Create training and test datasets</span></span>
<span data-ttu-id="59da8-162">Potrzebujemy niektórych danych do nauczenia modelu, a niektóre testowania go.</span><span class="sxs-lookup"><span data-stu-id="59da8-162">We need some data to train the model and some to test it.</span></span>
<span data-ttu-id="59da8-163">Dlatego w następnym kroku eksperyment, możemy podzielić zestawu danych na dwa oddzielne zestawy danych: jeden dla uczenie modelu, a drugi do testowania go.</span><span class="sxs-lookup"><span data-stu-id="59da8-163">So in the next step of the experiment, we split the dataset into two separate datasets: one for training our model and one for testing it.</span></span>

<span data-ttu-id="59da8-164">Aby to zrobić, używamy [podziału danych] [ split] modułu.</span><span class="sxs-lookup"><span data-stu-id="59da8-164">To do this, we use the [Split Data][split] module.</span></span>  

1. <span data-ttu-id="59da8-165">Znajdź [podziału danych] [ split] modułu, przeciągnij go do obszaru roboczego i połącz go z [edytowanie metadanych] [ edit-metadata] modułu.</span><span class="sxs-lookup"><span data-stu-id="59da8-165">Find the [Split Data][split] module, drag it onto the canvas, and connect it to the [Edit Metadata][edit-metadata] module.</span></span>

2. <span data-ttu-id="59da8-166">Domyślnie współczynnik rozdzielania wynosi 0,5 i **podziału Randomized** ustawiono parametr.</span><span class="sxs-lookup"><span data-stu-id="59da8-166">By default, the split ratio is 0.5 and the **Randomized split** parameter is set.</span></span> <span data-ttu-id="59da8-167">Oznacza, że losowe pół danych wyjściowych za pośrednictwem jednego portu [podziału danych] [ split] modułu i połowy przez innych.</span><span class="sxs-lookup"><span data-stu-id="59da8-167">This means that a random half of the data is output through one port of the [Split Data][split] module, and half through the other.</span></span> <span data-ttu-id="59da8-168">Te parametry można dostosować, jak również **Random seed** parametr, aby zmienić podziału między celów szkoleniowych i testów danych.</span><span class="sxs-lookup"><span data-stu-id="59da8-168">You can adjust these parameters, as well as the **Random seed** parameter, to change the split between training and testing data.</span></span> <span data-ttu-id="59da8-169">Na przykład możemy pozostaw je jako — jest.</span><span class="sxs-lookup"><span data-stu-id="59da8-169">For this example, we leave them as-is.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="59da8-170">Właściwość **ułamek wierszy w pierwszym wyjściowy zestaw danych** Określa, ile danych jest wysyłany za pośrednictwem *po lewej stronie* output portu.</span><span class="sxs-lookup"><span data-stu-id="59da8-170">The property **Fraction of rows in the first output dataset** determines how much of the data is output through the *left* output port.</span></span> <span data-ttu-id="59da8-171">Na przykład jeśli ustawisz stosunek 0,7 70% danych wówczas dane wyjściowe za pośrednictwem lewy port i 30% za pośrednictwem prawy port.</span><span class="sxs-lookup"><span data-stu-id="59da8-171">For instance, if you set the ratio to 0.7, then 70% of the data is output through the left port and 30% through the right port.</span></span>  
   > 
   > 

3. <span data-ttu-id="59da8-172">Kliknij dwukrotnie [podziału danych] [ split] moduł i wpisz komentarz, "danych szkoleniowych/testowania podzielić 50%".</span><span class="sxs-lookup"><span data-stu-id="59da8-172">Double-click the [Split Data][split] module and enter the comment, "Training/testing data split 50%".</span></span> 

<span data-ttu-id="59da8-173">Możemy użyć danych wyjściowych z [podziału danych] [ split] modułu jednak firma Microsoft, takich jak, ale ta funkcja pozwala wybrać wykorzystywać dane po lewej stronie, ponieważ dane szkoleniowe i prawa testowania jako dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="59da8-173">We can use the outputs of the [Split Data][split] module however we like, but let's choose to use the left output as training data and the right output as testing data.</span></span>  

<span data-ttu-id="59da8-174">Jak wspomniano w [poprzedniego kroku](machine-learning-walkthrough-2-upload-data.md), misclassifying ryzyko kredytowe wysokiej jako niski koszt jest pięć razy wyższa niż koszt misclassifying niskie ryzyko kredytowe jako wysoki.</span><span class="sxs-lookup"><span data-stu-id="59da8-174">As mentioned in the [previous step](machine-learning-walkthrough-2-upload-data.md), the cost of misclassifying a high credit risk as low is five times higher than the cost of misclassifying a low credit risk as high.</span></span> <span data-ttu-id="59da8-175">Aby to uwzględniać, możemy wygenerować nowy zestaw danych, które odzwierciedla tej funkcji koszt.</span><span class="sxs-lookup"><span data-stu-id="59da8-175">To account for this, we generate a new dataset that reflects this cost function.</span></span> <span data-ttu-id="59da8-176">W nowy zestaw danych każdy przykład wysokiego ryzyka są replikowane pięć razy podczas każdego przykład niskiego ryzyka nie jest replikowany.</span><span class="sxs-lookup"><span data-stu-id="59da8-176">In the new dataset, each high risk example is replicated five times, while each low risk example is not replicated.</span></span>   

<span data-ttu-id="59da8-177">Możemy replikacja za pomocą kodu języka R:</span><span class="sxs-lookup"><span data-stu-id="59da8-177">We can do this replication using R code:</span></span>  

1. <span data-ttu-id="59da8-178">Znajdź i przeciągnij [wykonanie skryptu języka R] [ execute-r-script] modułu na kanwie eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="59da8-178">Find and drag the [Execute R Script][execute-r-script] module onto the experiment canvas.</span></span> 

2. <span data-ttu-id="59da8-179">Połącz lewy port wyjściowy [podziału danych] [ split] modułu do pierwszego portu wejściowego ("Dataset1") z [wykonanie skryptu języka R] [ execute-r-script] modułu.</span><span class="sxs-lookup"><span data-stu-id="59da8-179">Connect the left output port of the [Split Data][split] module to the first input port ("Dataset1") of the [Execute R Script][execute-r-script] module.</span></span>

3. <span data-ttu-id="59da8-180">Kliknij dwukrotnie [wykonanie skryptu języka R] [ execute-r-script] modułu, a następnie wprowadź komentarz, "Ustaw korekty kosztu".</span><span class="sxs-lookup"><span data-stu-id="59da8-180">Double-click the [Execute R Script][execute-r-script] module and enter the comment, "Set cost adjustment".</span></span>

4. <span data-ttu-id="59da8-181">W **właściwości** okienku usunąć domyślny tekst w **skrypt języka R** parametr, a następnie wprowadź ten skrypt:</span><span class="sxs-lookup"><span data-stu-id="59da8-181">In the **Properties** pane, delete the default text in the **R Script** parameter and enter this script:</span></span>
   
       dataset1 <- maml.mapInputPort(1)
       data.set<-dataset1[dataset1[,21]==1,]
       pos<-dataset1[dataset1[,21]==2,]
       for (i in 1:5) data.set<-rbind(data.set,pos)
       maml.mapOutputPort("data.set")

    ![Skrypt języka R w module wykonanie skryptu języka R][9]

<span data-ttu-id="59da8-183">Konieczne tej samej operacji replikacji dla każdego produktu [podziału danych] [ split] modułu, aby dane szkolenia i testowania mieć takiego samego dostosowania kosztów.</span><span class="sxs-lookup"><span data-stu-id="59da8-183">We need to do this same replication operation for each output of the [Split Data][split] module so that the training and testing data have the same cost adjustment.</span></span> <span data-ttu-id="59da8-184">Najprostszym sposobem, w tym celu jest duplikując [wykonanie skryptu języka R] [ execute-r-script] modułu właśnie wprowadziliśmy i połączenia jej z drugiej output port [podziału danych] [ split] modułu.</span><span class="sxs-lookup"><span data-stu-id="59da8-184">The easiest way to do this is by duplicating the [Execute R Script][execute-r-script] module we just made and connecting it to the other output port of the [Split Data][split] module.</span></span>

1. <span data-ttu-id="59da8-185">Kliknij prawym przyciskiem myszy [wykonanie skryptu języka R] [ execute-r-script] moduł i zaznacz **kopiowania**.</span><span class="sxs-lookup"><span data-stu-id="59da8-185">Right-click the [Execute R Script][execute-r-script] module and select **Copy**.</span></span>

2. <span data-ttu-id="59da8-186">Kliknij prawym przyciskiem myszy obszaru roboczego eksperymentu, a następnie wybierz **Wklej**.</span><span class="sxs-lookup"><span data-stu-id="59da8-186">Right-click the experiment canvas and select **Paste**.</span></span>

3. <span data-ttu-id="59da8-187">Przeciągnij nowy moduł w określonej pozycji, a następnie połącz portem wyjściowym prawo [podziału danych] [ split] na pierwszy port wejściowy tego nowego modułu [wykonanie skryptu języka R] [ execute-r-script] modułu.</span><span class="sxs-lookup"><span data-stu-id="59da8-187">Drag the new module into position, and then connect the right output port of the [Split Data][split] module to the first input port of this new [Execute R Script][execute-r-script] module.</span></span> 

4. <span data-ttu-id="59da8-188">W dolnej części obszaru roboczego, kliknij przycisk **Uruchom**.</span><span class="sxs-lookup"><span data-stu-id="59da8-188">At the bottom of the canvas, click **Run**.</span></span> 

> [!TIP]
> <span data-ttu-id="59da8-189">Kopii modułu wykonania skryptu języka R zawiera sam skrypt jako oryginalnego modułu.</span><span class="sxs-lookup"><span data-stu-id="59da8-189">The copy of the Execute R Script module contains the same script as the original module.</span></span> <span data-ttu-id="59da8-190">Podczas kopiowania i wklejania modułu na kanwie kopię zachowuje wszystkie właściwości oryginału.</span><span class="sxs-lookup"><span data-stu-id="59da8-190">When you copy and paste a module on the canvas, the copy retains all the properties of the original.</span></span>  
> 
> 

<span data-ttu-id="59da8-191">Naszym doświadczeniu teraz wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="59da8-191">Our experiment now looks something like this:</span></span>

![Dodanie modułu podziału i skrypty języka R][4]

<span data-ttu-id="59da8-193">Aby uzyskać więcej informacji na używanie skryptów języka R w eksperymentów, zobacz [rozszerzanie eksperymentu z R](machine-learning-extend-your-experiment-with-r.md).</span><span class="sxs-lookup"><span data-stu-id="59da8-193">For more information on using R scripts in your experiments, see [Extend your experiment with R](machine-learning-extend-your-experiment-with-r.md).</span></span>

<span data-ttu-id="59da8-194">**Następnie: [pociągu i Ewaluacja modeli](machine-learning-walkthrough-4-train-and-evaluate-models.md)**</span><span class="sxs-lookup"><span data-stu-id="59da8-194">**Next: [Train and evaluate the models](machine-learning-walkthrough-4-train-and-evaluate-models.md)**</span></span>

[0]: ./media/machine-learning-walkthrough-3-create-new-experiment/create-new-experiment.png
[5]: ./media/machine-learning-walkthrough-3-create-new-experiment/rename-experiment.png
[6]: ./media/machine-learning-walkthrough-3-create-new-experiment/experiment-properties.png
[7]: ./media/machine-learning-walkthrough-3-create-new-experiment/add-dataset-to-experiment.png
[8]: ./media/machine-learning-walkthrough-3-create-new-experiment/edit-metadata-with-comment.png
[9]: ./media/machine-learning-walkthrough-3-create-new-experiment/execute-r-script.png
[1]: ./media/machine-learning-walkthrough-3-create-new-experiment/experiment-with-edit-metadata-module.png
[2]: ./media/machine-learning-walkthrough-3-create-new-experiment/select-columns.png
[3]: ./media/machine-learning-walkthrough-3-create-new-experiment/edit-metadata-properties.png
[4]: ./media/machine-learning-walkthrough-3-create-new-experiment/experiment.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
