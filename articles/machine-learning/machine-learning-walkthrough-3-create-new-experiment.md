---
title: 'Krok 3: Tworzenie nowego eksperymentu uczenia maszynowego | Dokumentacja firmy Microsoft'
description: "Krok 3 hello opracowanie wskazówki rozwiązanie predykcyjne: Tworzenie nowego eksperymentu uczenia w usłudze Azure Machine Learning Studio."
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
ms.openlocfilehash: 4697d461a205c50c8d2aa6a3bd56697840cb30f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-3-create-a-new-azure-machine-learning-experiment"></a><span data-ttu-id="9f6ed-103">Przewodnik, krok 3. Tworzenie nowego eksperymentu usługi Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="9f6ed-103">Walkthrough Step 3: Create a new Azure Machine Learning experiment</span></span>
<span data-ttu-id="9f6ed-104">To hello trzeci krok wskazówki hello [tworzenie rozwiązania analizy predykcyjnej w usłudze Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="9f6ed-104">This is hello third step of hello walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. [<span data-ttu-id="9f6ed-105">Tworzenie obszaru roboczego usługi Machine Learning</span><span class="sxs-lookup"><span data-stu-id="9f6ed-105">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="9f6ed-106">Przekazywanie istniejących danych</span><span class="sxs-lookup"><span data-stu-id="9f6ed-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. <span data-ttu-id="9f6ed-107">**Tworzenie nowego eksperymentu**</span><span class="sxs-lookup"><span data-stu-id="9f6ed-107">**Create a new experiment**</span></span>
4. [<span data-ttu-id="9f6ed-108">Nauczanie i Ewaluacja modeli hello</span><span class="sxs-lookup"><span data-stu-id="9f6ed-108">Train and evaluate hello models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="9f6ed-109">Wdrażanie usługi sieci Web hello</span><span class="sxs-lookup"><span data-stu-id="9f6ed-109">Deploy hello Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="9f6ed-110">Witaj dostępu do usługi sieci Web</span><span class="sxs-lookup"><span data-stu-id="9f6ed-110">Access hello Web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<span data-ttu-id="9f6ed-111">następnym krokiem Hello w ramach tego przewodnika jest toocreate eksperymentu w usłudze Machine Learning Studio używającej hello zestawu danych, które możemy przekazać.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-111">hello next step in this walkthrough is toocreate an experiment in Machine Learning Studio that uses hello dataset we uploaded.</span></span>  

1. <span data-ttu-id="9f6ed-112">W Studio, kliknij przycisk **+ nowy** u dołu okna hello hello.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-112">In Studio, click **+NEW** at hello bottom of hello window.</span></span>
2. <span data-ttu-id="9f6ed-113">Wybierz **EKSPERYMENTU**, a następnie wybierz pozycję "Pusty eksperyment".</span><span class="sxs-lookup"><span data-stu-id="9f6ed-113">Select **EXPERIMENT**, and then select "Blank Experiment".</span></span> 

    ![Tworzenie nowego eksperymentu][0]

2. <span data-ttu-id="9f6ed-115">Wybierz hello domyślna nazwa u góry hello hello kanwy eksperymentu i zmień jego nazwę toosomething łatwy do rozpoznania.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-115">Select hello default experiment name at hello top of hello canvas and rename it toosomething meaningful.</span></span>

    ![Zmień nazwę eksperymentu][5]
   
   > [!TIP]
   > <span data-ttu-id="9f6ed-117">Toofill dobrym rozwiązaniem jest **Podsumowanie** i **opis** do eksperymentu hello w hello **właściwości** okienka.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-117">It's a good practice toofill in **Summary** and **Description** for hello experiment in hello **Properties** pane.</span></span> <span data-ttu-id="9f6ed-118">Przyznanie tych właściwości hello szansy toodocument hello eksperymentu, aby każdy, kto analizuje go później będzie zrozumiałe, cele i metodologii.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-118">These properties give you hello chance toodocument hello experiment so that anyone who looks at it later will understand your goals and methodology.</span></span>
   > 
   > ![Właściwości eksperymentu][6]
   > 
3. <span data-ttu-id="9f6ed-120">W hello modułu palety toohello lewej strony obszaru roboczego eksperymentu hello, rozwiń węzeł **zapisane zestawów danych**.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-120">In hello module palette toohello left of hello experiment canvas, expand **Saved Datasets**.</span></span>
4. <span data-ttu-id="9f6ed-121">Znajdź hello dataset utworzono w obszarze **Moje zestawów danych** i przeciągnij go na powitania kanwy.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-121">Find hello dataset you created under **My Datasets** and drag it onto hello canvas.</span></span> <span data-ttu-id="9f6ed-122">Możesz również znaleźć hello zestawu danych, wprowadzając nazwę hello w hello **wyszukiwania** pole powyżej hello palety.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-122">You can also find hello dataset by entering hello name in hello **Search** box above hello palette.</span></span>  

    ![Dodaj hello dataset toohello eksperymentu][7]

## <a name="prepare-hello-data"></a><span data-ttu-id="9f6ed-124">Przygotowanie danych hello</span><span class="sxs-lookup"><span data-stu-id="9f6ed-124">Prepare hello data</span></span>
<span data-ttu-id="9f6ed-125">Możesz wyświetlić hello pierwszych 100 wierszy danych hello i niektóre informacje statystyczne dla całego zestawu danych hello: kliknij port wyjściowy hello hello DataSet (hello małe kółko u dołu hello) i wybierz **Visualize**.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-125">You can view hello first 100 rows of hello data and some statistical information for hello whole dataset: Click hello output port of hello dataset (hello small circle at hello bottom) and select **Visualize**.</span></span>  

<span data-ttu-id="9f6ed-126">Ponieważ hello plik danych nie został dostarczony z nagłówków kolumn, Studio udostępnił ogólnego nagłówki (Col1, Col2, *itp.*).</span><span class="sxs-lookup"><span data-stu-id="9f6ed-126">Because hello data file didn't come with column headings, Studio has provided generic headings (Col1, Col2, *etc.*).</span></span> <span data-ttu-id="9f6ed-127">Dobrym nagłówki nie są istotne toocreating modelu, ale ich stał się łatwiejsze toowork z danymi hello w eksperymencie hello.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-127">Good headings aren't essential toocreating a model, but they make it easier toowork with hello data in hello experiment.</span></span> <span data-ttu-id="9f6ed-128">Gdy firma Microsoft ostatecznie opublikować ten model usługi sieci web, nagłówki hello pomóc w identyfikacji użytkownika toohello kolumn hello hello usługi.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-128">Also, when we eventually publish this model in a web service, hello headings help identify hello columns toohello user of hello service.</span></span>  

<span data-ttu-id="9f6ed-129">Można dodać nagłówków kolumn za pomocą hello [edytowanie metadanych] [ edit-metadata] modułu.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-129">We can add column headings using hello [Edit Metadata][edit-metadata] module.</span></span>
<span data-ttu-id="9f6ed-130">Użyj hello [edytowanie metadanych] [ edit-metadata] modułu toochange metadane skojarzone z zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-130">You use hello [Edit Metadata][edit-metadata] module toochange metadata associated with a dataset.</span></span> <span data-ttu-id="9f6ed-131">W takim przypadku stosujemy go tooprovide więcej przyjazne nazwy dla nagłówków kolumn.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-131">In this case, we use it tooprovide more friendly names for column headings.</span></span> 

<span data-ttu-id="9f6ed-132">toouse [edytowanie metadanych][edit-metadata], należy najpierw określić które toomodify kolumn (w tym przypadku wszystkie z nich.) Następnie określ hello toobe działania wykonywane na podstawie tych kolumn (w tym przypadku zmiana nagłówków kolumn.)</span><span class="sxs-lookup"><span data-stu-id="9f6ed-132">toouse [Edit Metadata][edit-metadata], you first specify which columns toomodify (in this case, all of them.) Next, you specify hello action toobe performed on those columns (in this case, changing column headings.)</span></span>

1. <span data-ttu-id="9f6ed-133">W palecie modułów hello, wpisz "metadanych" w hello **wyszukiwania** pole.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-133">In hello module palette, type "metadata" in hello **Search** box.</span></span> <span data-ttu-id="9f6ed-134">Witaj [edytowanie metadanych] [ edit-metadata] jest widoczna na liście modułu hello.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-134">hello [Edit Metadata][edit-metadata] appears in hello module list.</span></span>

2. <span data-ttu-id="9f6ed-135">Kliknij i przeciągnij hello [edytowanie metadanych] [ edit-metadata] modułu na powitania obszaru roboczego i upuść ją poniżej dataset hello dodane wcześniej.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-135">Click and drag hello [Edit Metadata][edit-metadata] module onto hello canvas and drop it below hello dataset we added earlier.</span></span>

3. <span data-ttu-id="9f6ed-136">Połącz hello dataset toohello [edytowanie metadanych][edit-metadata]: kliknij port wyjściowy hello hello DataSet (hello małe kółko u dołu hello hello zestawu danych), przeciągnij toohello port wejściowy z [edytowanie metadanych ] [ edit-metadata] (hello małe koło u góry hello modułu hello), następnie zwolnij przycisk myszy hello.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-136">Connect hello dataset toohello [Edit Metadata][edit-metadata]: click hello output port of hello dataset (hello small circle at hello bottom of hello dataset), drag toohello input port of [Edit Metadata][edit-metadata] (hello small circle at hello top of hello module), then release hello mouse button.</span></span> <span data-ttu-id="9f6ed-137">nawet w przypadku przenoszenia jednej na kanwie hello Hello zestawu danych i modułu pozostały połączone.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-137">hello dataset and module remain connected even if you move either around on hello canvas.</span></span>
   
   <span data-ttu-id="9f6ed-138">Hello eksperyment powinien teraz wyglądać mniej więcej tak:</span><span class="sxs-lookup"><span data-stu-id="9f6ed-138">hello experiment should now look something like this:</span></span>  
   
   ![Dodawanie metadanych edycji][1]
   
   <span data-ttu-id="9f6ed-140">Witaj czerwony wykrzyknik wskazuje, że firma Microsoft nie zostało to jeszcze ustawiony hello właściwości dla tego modułu.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-140">hello red exclamation mark indicates that we haven't set hello properties for this module yet.</span></span> <span data-ttu-id="9f6ed-141">Robimy tego dalej.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-141">We'll do that next.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="9f6ed-142">Można dodać moduł tooa komentarza, klikając dwukrotnie pozycję modułu hello i wprowadzanie tekstu.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-142">You can add a comment tooa module by double-clicking hello module and entering text.</span></span> <span data-ttu-id="9f6ed-143">Może to ułatwić jednym rzutem oka ocenić zadań jakie hello modułu w eksperymencie.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-143">This can help you see at a glance what hello module is doing in your experiment.</span></span> <span data-ttu-id="9f6ed-144">W takim przypadku kliknij dwukrotnie hello [edytowanie metadanych] [ edit-metadata] moduł i wpisz hello komentarz "Dodaj nagłówki kolumn".</span><span class="sxs-lookup"><span data-stu-id="9f6ed-144">In this case, double-click hello [Edit Metadata][edit-metadata] module and type hello comment "Add column headings".</span></span> <span data-ttu-id="9f6ed-145">Kliknij pole tekstowe hello tooclose kanwy hello gdziekolwiek.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-145">Click anywhere else on hello canvas tooclose hello text box.</span></span> <span data-ttu-id="9f6ed-146">toodisplay hello komentarza, kliknij przycisk strzałki hello na powitania modułu.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-146">toodisplay hello comment, click hello down-arrow on hello module.</span></span>
   > 
   > ![Edytuj moduł metadanych z komentarzem dodane][8]
   > 
4. <span data-ttu-id="9f6ed-148">Wybierz [edytowanie metadanych][edit-metadata]w hello **właściwości** kliknij okienko toohello prawo do kanwy hello **Uruchom selektor kolumn**.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-148">Select [Edit Metadata][edit-metadata], and in hello **Properties** pane toohello right of hello canvas, click **Launch column selector**.</span></span>

5. <span data-ttu-id="9f6ed-149">W hello **wybierz kolumny** okno dialogowe, wybierz wszystkie hello wierszy w **dostępne kolumny** i kliknij przycisk > toomove ich zbyt**wybrane kolumny**.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-149">In hello **Select columns** dialog, select all hello rows in **Available Columns** and click > toomove them too**Selected Columns**.</span></span>
   <span data-ttu-id="9f6ed-150">okno dialogowe Hello powinien wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="9f6ed-150">hello dialog should look like this:</span></span>

   ![Selektor kolumn z wybrano wszystkich kolumn][2]

6. <span data-ttu-id="9f6ed-152">Kliknij przycisk hello **OK** znacznik wyboru.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-152">Click hello **OK** check mark.</span></span>

7. <span data-ttu-id="9f6ed-153">Po powrocie do hello **właściwości** okienka, poszukaj hello **nowych nazw kolumn** parametru.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-153">Back in hello **Properties** pane, look for hello **New column names** parameter.</span></span> <span data-ttu-id="9f6ed-154">W tym miejscu wprowadź listę nazw kolumn 21 hello w zestawie danych hello, oddzielonych przecinkami i kolejność kolumn.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-154">In this field, enter a list of names for hello 21 columns in hello dataset, separated by commas and in column order.</span></span> <span data-ttu-id="9f6ed-155">Nazwy kolumn hello można uzyskać z hello dataset dokumentacji w witrynie sieci Web hello UCI lub dla wygody można skopiować i wkleić hello następującej listy:</span><span class="sxs-lookup"><span data-stu-id="9f6ed-155">You can obtain hello columns names from hello dataset documentation on hello UCI website, or for convenience you can copy and paste hello following list:</span></span>  
   
       Status of checking account, Duration in months, Credit history, Purpose, Credit amount, Savings account/bond, Present employment since, Installment rate in percentage of disposable income, Personal status and sex, Other debtors, Present residence since, Property, Age in years, Other installment plans, Housing, Number of existing credits, Job, Number of people providing maintenance for, Telephone, Foreign worker, Credit risk  
   
   <span data-ttu-id="9f6ed-156">w okienku właściwości Hello wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="9f6ed-156">hello Properties pane looks like this:</span></span>
   
   ![Właściwości metadanych edycji][3]

> [!TIP]
> <span data-ttu-id="9f6ed-158">Nagłówki kolumn hello tooverify, należy uruchomić eksperyment hello (kliknij **Uruchom** poniżej kanwy eksperymentu hello).</span><span class="sxs-lookup"><span data-stu-id="9f6ed-158">If you want tooverify hello column headings, run hello experiment (click **RUN** below hello experiment canvas).</span></span> <span data-ttu-id="9f6ed-159">Po zakończeniu pracy (zielony znacznik wyboru jest wyświetlane na [edytowanie metadanych][edit-metadata]), kliknij port wyjściowy hello hello [edytowanie metadanych] [ edit-metadata] Moduł, a następnie wybierz **Visualize**.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-159">When it finishes running (a green check mark appears on [Edit Metadata][edit-metadata]), click hello output port of hello [Edit Metadata][edit-metadata] module, and select **Visualize**.</span></span> <span data-ttu-id="9f6ed-160">Można wyświetlić dane wyjściowe hello każdy moduł w hello sam sposób tooview hello postęp hello danych za pośrednictwem hello eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-160">You can view hello output of any module in hello same way tooview hello progress of hello data through hello experiment.</span></span>
> 
> 

## <a name="create-training-and-test-datasets"></a><span data-ttu-id="9f6ed-161">Tworzenie szkolenia i testowanie zbiory danych</span><span class="sxs-lookup"><span data-stu-id="9f6ed-161">Create training and test datasets</span></span>
<span data-ttu-id="9f6ed-162">Potrzebujemy niektórych danych tootrain hello modelu i niektóre tootest go.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-162">We need some data tootrain hello model and some tootest it.</span></span>
<span data-ttu-id="9f6ed-163">Dlatego w hello następnego kroku hello eksperymentu, możemy podzielić hello zestawu danych na dwa oddzielne zestawy danych: jeden dla uczenie modelu, a drugi do testowania go.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-163">So in hello next step of hello experiment, we split hello dataset into two separate datasets: one for training our model and one for testing it.</span></span>

<span data-ttu-id="9f6ed-164">toodo, używamy hello [podziału danych] [ split] modułu.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-164">toodo this, we use hello [Split Data][split] module.</span></span>  

1. <span data-ttu-id="9f6ed-165">Znajdź hello [podziału danych] [ split] moduł, przeciągnij je na kanwie hello i podłącz go toohello [edytowanie metadanych] [ edit-metadata] modułu.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-165">Find hello [Split Data][split] module, drag it onto hello canvas, and connect it toohello [Edit Metadata][edit-metadata] module.</span></span>

2. <span data-ttu-id="9f6ed-166">Współczynnik rozdzielania hello jest domyślnie 0,5 i hello **podziału Randomized** ustawiono parametr.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-166">By default, hello split ratio is 0.5 and hello **Randomized split** parameter is set.</span></span> <span data-ttu-id="9f6ed-167">Oznacza, że losowe pół hello danych wyjściowych za pośrednictwem jednego portu hello [podziału danych] [ split] modułu i połowa za pomocą hello innych.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-167">This means that a random half of hello data is output through one port of hello [Split Data][split] module, and half through hello other.</span></span> <span data-ttu-id="9f6ed-168">Użytkownik może dostosować te parametry, a także hello **Random seed** parametru hello toochange podzielony między celów szkoleniowych i testów danych.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-168">You can adjust these parameters, as well as hello **Random seed** parameter, toochange hello split between training and testing data.</span></span> <span data-ttu-id="9f6ed-169">Na przykład możemy pozostaw je jako — jest.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-169">For this example, we leave them as-is.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="9f6ed-170">Witaj właściwości **ułamek wierszy w hello najpierw wyjściowy zestaw danych** Określa, ile danych hello przekazywane za pośrednictwem hello są *po lewej stronie* output portu.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-170">hello property **Fraction of rows in hello first output dataset** determines how much of hello data is output through hello *left* output port.</span></span> <span data-ttu-id="9f6ed-171">Na przykład jeśli ustawisz too0.7 stosunek hello, 70% hello danych są kierowane za pośrednictwem hello lewego portu i 30% za pośrednictwem hello prawy port.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-171">For instance, if you set hello ratio too0.7, then 70% of hello data is output through hello left port and 30% through hello right port.</span></span>  
   > 
   > 

3. <span data-ttu-id="9f6ed-172">Kliknij dwukrotnie hello [podziału danych] [ split] modułu i wprowadź komentarz Witaj, "dane szkoleniowe/testowania podzielić 50%".</span><span class="sxs-lookup"><span data-stu-id="9f6ed-172">Double-click hello [Split Data][split] module and enter hello comment, "Training/testing data split 50%".</span></span> 

<span data-ttu-id="9f6ed-173">Możemy użyć hello elementy wyjściowe hello [podziału danych] [ split] modułu jednak firma Microsoft, takich jak, ale ta funkcja pozwala wybrać toouse hello po lewej stronie dane wyjściowe jako dane szkoleniowe i hello prawo testowania jako dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-173">We can use hello outputs of hello [Split Data][split] module however we like, but let's choose toouse hello left output as training data and hello right output as testing data.</span></span>  

<span data-ttu-id="9f6ed-174">Jak wspomniano w hello [poprzedniego kroku](machine-learning-walkthrough-2-upload-data.md), misclassifying ryzyko kredytowe wysokiej jako niski koszt hello jest pięć razy wyższa niż koszt hello misclassifying niskie ryzyko kredytowe jako wysoki.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-174">As mentioned in hello [previous step](machine-learning-walkthrough-2-upload-data.md), hello cost of misclassifying a high credit risk as low is five times higher than hello cost of misclassifying a low credit risk as high.</span></span> <span data-ttu-id="9f6ed-175">tooaccount tego, firma Microsoft generuje nowy zestaw danych, które odzwierciedla tej funkcji koszt.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-175">tooaccount for this, we generate a new dataset that reflects this cost function.</span></span> <span data-ttu-id="9f6ed-176">W hello nowy zestaw danych każdy przykład wysokiego ryzyka są replikowane pięć razy, gdy nie jest replikowany każdy przykład niskiego ryzyka.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-176">In hello new dataset, each high risk example is replicated five times, while each low risk example is not replicated.</span></span>   

<span data-ttu-id="9f6ed-177">Możemy replikacja za pomocą kodu języka R:</span><span class="sxs-lookup"><span data-stu-id="9f6ed-177">We can do this replication using R code:</span></span>  

1. <span data-ttu-id="9f6ed-178">Znajdź i przeciągnij hello [wykonanie skryptu języka R] [ execute-r-script] modułu na kanwie eksperymentu hello.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-178">Find and drag hello [Execute R Script][execute-r-script] module onto hello experiment canvas.</span></span> 

2. <span data-ttu-id="9f6ed-179">Połącz hello pozostałych portem wyjściowym hello [podziału danych] [ split] toohello modułu pierwsze dane wejściowe portu ("Dataset1") z hello [wykonanie skryptu języka R] [ execute-r-script] Moduł.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-179">Connect hello left output port of hello [Split Data][split] module toohello first input port ("Dataset1") of hello [Execute R Script][execute-r-script] module.</span></span>

3. <span data-ttu-id="9f6ed-180">Kliknij dwukrotnie hello [wykonanie skryptu języka R] [ execute-r-script] modułu, a następnie wprowadź komentarz Witaj, "Ustaw korekty kosztu".</span><span class="sxs-lookup"><span data-stu-id="9f6ed-180">Double-click hello [Execute R Script][execute-r-script] module and enter hello comment, "Set cost adjustment".</span></span>

4. <span data-ttu-id="9f6ed-181">W hello **właściwości** okienku i Usuń hello domyślny tekst w hello **skrypt języka R** parametr, a następnie wprowadź ten skrypt:</span><span class="sxs-lookup"><span data-stu-id="9f6ed-181">In hello **Properties** pane, delete hello default text in hello **R Script** parameter and enter this script:</span></span>
   
       dataset1 <- maml.mapInputPort(1)
       data.set<-dataset1[dataset1[,21]==1,]
       pos<-dataset1[dataset1[,21]==2,]
       for (i in 1:5) data.set<-rbind(data.set,pos)
       maml.mapOutputPort("data.set")

    ![Skrypt języka R w module wykonanie skryptu języka R hello][9]

<span data-ttu-id="9f6ed-183">Potrzebujemy toodo tej samej operacji replikacji dla każdego danych wyjściowych hello [podziału danych] [ split] moduł, tak że hello celów szkoleniowych i testów danych ma takie same hello Koszt korekty.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-183">We need toodo this same replication operation for each output of hello [Split Data][split] module so that hello training and testing data have hello same cost adjustment.</span></span> <span data-ttu-id="9f6ed-184">Witaj najprostszym toodo sposób jest duplikując hello [wykonanie skryptu języka R] [ execute-r-script] modułu właśnie wprowadziliśmy i połączenia jej toohello innych danych wyjściowych port hello [podziału danych] [ split] modułu.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-184">hello easiest way toodo this is by duplicating hello [Execute R Script][execute-r-script] module we just made and connecting it toohello other output port of hello [Split Data][split] module.</span></span>

1. <span data-ttu-id="9f6ed-185">Kliknij prawym przyciskiem myszy hello [wykonanie skryptu języka R] [ execute-r-script] modułu, a następnie wybierz **kopiowania**.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-185">Right-click hello [Execute R Script][execute-r-script] module and select **Copy**.</span></span>

2. <span data-ttu-id="9f6ed-186">Kliknij prawym przyciskiem myszy hello roboczego eksperymentu, a następnie wybierz **Wklej**.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-186">Right-click hello experiment canvas and select **Paste**.</span></span>

3. <span data-ttu-id="9f6ed-187">Przeciągnij hello nowy moduł w określonej pozycji, a następnie połącz port wyjściowy prawo hello hello [podziału danych] [ split] toohello modułu pierwsze dane wejściowe port to nowy [wykonanie skryptu języka R] [ execute-r-script] modułu.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-187">Drag hello new module into position, and then connect hello right output port of hello [Split Data][split] module toohello first input port of this new [Execute R Script][execute-r-script] module.</span></span> 

4. <span data-ttu-id="9f6ed-188">U dołu hello hello kanwy, kliknij przycisk **Uruchom**.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-188">At hello bottom of hello canvas, click **Run**.</span></span> 

> [!TIP]
> <span data-ttu-id="9f6ed-189">Hello kopii modułu wykonania skryptu języka R hello zawiera hello sam skrypt jako hello oryginalnego modułu.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-189">hello copy of hello Execute R Script module contains hello same script as hello original module.</span></span> <span data-ttu-id="9f6ed-190">Podczas kopiowania i wklejania modułu na kanwie hello kopiowania hello zachowuje wszystkie właściwości hello hello oryginalnego.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-190">When you copy and paste a module on hello canvas, hello copy retains all hello properties of hello original.</span></span>  
> 
> 

<span data-ttu-id="9f6ed-191">Naszym doświadczeniu teraz wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="9f6ed-191">Our experiment now looks something like this:</span></span>

![Dodanie modułu podziału i skrypty języka R][4]

<span data-ttu-id="9f6ed-193">Aby uzyskać więcej informacji na używanie skryptów języka R w eksperymentów, zobacz [rozszerzanie eksperymentu z R](machine-learning-extend-your-experiment-with-r.md).</span><span class="sxs-lookup"><span data-stu-id="9f6ed-193">For more information on using R scripts in your experiments, see [Extend your experiment with R](machine-learning-extend-your-experiment-with-r.md).</span></span>

<span data-ttu-id="9f6ed-194">**Następnie: [pociągu i ocena hello modeli](machine-learning-walkthrough-4-train-and-evaluate-models.md)**</span><span class="sxs-lookup"><span data-stu-id="9f6ed-194">**Next: [Train and evaluate hello models](machine-learning-walkthrough-4-train-and-evaluate-models.md)**</span></span>

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
