---
title: "aaaAnalyze danych za pomocą usługi Azure Machine Learning | Dokumentacja firmy Microsoft"
description: "Użyj usługi Azure Machine Learning toobuild predykcyjnej maszyny uczenie modelu, w oparciu o dane przechowywane w magazynie danych SQL Azure."
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: 
ms.assetid: 95635460-150f-4a50-be9c-5ddc5797f8a9
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 03/02/2017
ms.author: kevin;barbkess
ms.openlocfilehash: 337a2cd77aaad4467683827c56e5015b262b2554
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-data-with-azure-machine-learning"></a><span data-ttu-id="c3de4-103">Analizowanie danych przy użyciu usługi Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="c3de4-103">Analyze data with Azure Machine Learning</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c3de4-104">Power BI</span><span class="sxs-lookup"><span data-stu-id="c3de4-104">Power BI</span></span>](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [<span data-ttu-id="c3de4-105">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="c3de4-105">Azure Machine Learning</span></span>](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [<span data-ttu-id="c3de4-106">Program Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c3de4-106">Visual Studio</span></span>](sql-data-warehouse-query-visual-studio.md)
> * [<span data-ttu-id="c3de4-107">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="c3de4-107">sqlcmd</span></span>](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [<span data-ttu-id="c3de4-108">SSMS</span><span class="sxs-lookup"><span data-stu-id="c3de4-108">SSMS</span></span>](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="c3de4-109">W tym samouczku używa usługi Azure Machine Learning toobuild predykcyjnej maszyny, uczenie modelu, w oparciu o dane przechowywane w magazynie danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="c3de4-109">This tutorial uses Azure Machine Learning toobuild a predictive machine learning model based on data stored in Azure SQL Data Warehouse.</span></span> <span data-ttu-id="c3de4-110">W szczególności to z kolei ukierunkowaną kampanię marketingową dla firmy Adventure Works, sklep roweru hello, przez Jeśli klient jest prawdopodobnie toobuy roweru lub nie.</span><span class="sxs-lookup"><span data-stu-id="c3de4-110">Specifically, this builds a targeted marketing campaign for Adventure Works, hello bike shop, by predicting if a customer is likely toobuy a bike or not.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Integrating-Azure-Machine-Learning-with-Azure-SQL-Data-Warehouse/player]
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="c3de4-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="c3de4-111">Prerequisites</span></span>
<span data-ttu-id="c3de4-112">toostep opisanych w tym samouczku, potrzebne są:</span><span class="sxs-lookup"><span data-stu-id="c3de4-112">toostep through this tutorial, you need:</span></span>

* <span data-ttu-id="c3de4-113">Baza danych usługi SQL Data Warehouse. ze wstępnie załadowanymi danymi z bazy danych AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="c3de4-113">A SQL Data Warehouse pre-loaded with AdventureWorksDW sample data.</span></span> <span data-ttu-id="c3de4-114">tooprovision tego, zobacz [Tworzenie usługi SQL Data Warehouse] [ Create a SQL Data Warehouse] i wybierz polecenie tooload hello przykładowych danych.</span><span class="sxs-lookup"><span data-stu-id="c3de4-114">tooprovision this, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse] and choose tooload hello sample data.</span></span> <span data-ttu-id="c3de4-115">Jeśli masz już magazyn danych, ale bez przykładowych danych, możesz [ręcznie załadować przykładowe dane][load sample data manually].</span><span class="sxs-lookup"><span data-stu-id="c3de4-115">If you already have a data warehouse but do not have sample data, you can [load sample data manually][load sample data manually].</span></span>

## <a name="1-get-hello-data"></a><span data-ttu-id="c3de4-116">1. Pobierz dane hello</span><span class="sxs-lookup"><span data-stu-id="c3de4-116">1. Get hello data</span></span>
<span data-ttu-id="c3de4-117">dane Hello jest hello widoku dbo.vTargetMail w bazie danych AdventureWorksDW hello.</span><span class="sxs-lookup"><span data-stu-id="c3de4-117">hello data is in hello dbo.vTargetMail view in hello AdventureWorksDW database.</span></span> <span data-ttu-id="c3de4-118">tooread te dane:</span><span class="sxs-lookup"><span data-stu-id="c3de4-118">tooread this data:</span></span>

1. <span data-ttu-id="c3de4-119">Zaloguj się do programu [Azure Machine Learning Studio][Azure Machine Learning studio] i kliknij eksperymenty.</span><span class="sxs-lookup"><span data-stu-id="c3de4-119">Sign into [Azure Machine Learning studio][Azure Machine Learning studio] and click on my experiments.</span></span>
2. <span data-ttu-id="c3de4-120">Kliknij przycisk **+ NOWE** i wybierz pozycję **Blank Experiment** (Pusty eksperyment).</span><span class="sxs-lookup"><span data-stu-id="c3de4-120">Click **+NEW** and select **Blank Experiment**.</span></span>
3. <span data-ttu-id="c3de4-121">Wprowadź nazwę swojego eksperymentu: Targeted Marketing (Marketing docelowy).</span><span class="sxs-lookup"><span data-stu-id="c3de4-121">Enter a name for your experiment: Targeted Marketing.</span></span>
4. <span data-ttu-id="c3de4-122">Przeciągnij hello **czytnika** modułu na podstawie hello okienka modułów do kanwy hello.</span><span class="sxs-lookup"><span data-stu-id="c3de4-122">Drag hello **Reader** module from hello modules pane into hello canvas.</span></span>
5. <span data-ttu-id="c3de4-123">Określ szczegóły hello bazy danych magazynu danych SQL w okienku Properties hello.</span><span class="sxs-lookup"><span data-stu-id="c3de4-123">Specify hello details of your SQL Data Warehouse database in hello Properties pane.</span></span>
6. <span data-ttu-id="c3de4-124">Określ bazę danych hello **zapytania** tooread hello dane.</span><span class="sxs-lookup"><span data-stu-id="c3de4-124">Specify hello database **query** tooread hello data of interest.</span></span>

```sql
SELECT [CustomerKey]
  ,[GeographyKey]
  ,[CustomerAlternateKey]
  ,[MaritalStatus]
  ,[Gender]
  ,cast ([YearlyIncome] as int) as SalaryYear
  ,[TotalChildren]
  ,[NumberChildrenAtHome]
  ,[EnglishEducation]
  ,[EnglishOccupation]
  ,[HouseOwnerFlag]
  ,[NumberCarsOwned]
  ,[CommuteDistance]
  ,[Region]
  ,[Age]
  ,[BikeBuyer]
FROM [dbo].[vTargetMail]
```

<span data-ttu-id="c3de4-125">Uruchom eksperyment hello, klikając **Uruchom** w obszarze hello kanwy eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="c3de4-125">Run hello experiment by clicking **Run** under hello experiment canvas.</span></span>
<span data-ttu-id="c3de4-126">![Uruchom eksperyment hello][1]</span><span class="sxs-lookup"><span data-stu-id="c3de4-126">![Run hello experiment][1]</span></span>

<span data-ttu-id="c3de4-127">Po zakończeniu eksperymentu hello pomyślnie wykonywane kliknij port wyjściowy hello u dołu hello moduł czytnika hello i wybierz **wizualizacja** toosee hello zaimportowała dane.</span><span class="sxs-lookup"><span data-stu-id="c3de4-127">After hello experiment finishes running successfully, click hello output port at hello bottom of hello Reader module and select **Visualize** toosee hello imported data.</span></span>
<span data-ttu-id="c3de4-128">![Wyświetlanie zaimportowanych danych][3]</span><span class="sxs-lookup"><span data-stu-id="c3de4-128">![View imported data][3]</span></span>

## <a name="2-clean-hello-data"></a><span data-ttu-id="c3de4-129">2. Wyczyść hello danych</span><span class="sxs-lookup"><span data-stu-id="c3de4-129">2. Clean hello data</span></span>
<span data-ttu-id="c3de4-130">dane hello tooclean, usunąć niektóre kolumny, które nie są istotne dla modelu hello.</span><span class="sxs-lookup"><span data-stu-id="c3de4-130">tooclean hello data, drop some columns that are not relevant for hello model.</span></span> <span data-ttu-id="c3de4-131">toodo to:</span><span class="sxs-lookup"><span data-stu-id="c3de4-131">toodo this:</span></span>

1. <span data-ttu-id="c3de4-132">Przeciągnij hello **kolumny projektu** modułu na kanwie hello.</span><span class="sxs-lookup"><span data-stu-id="c3de4-132">Drag hello **Project Columns** module into hello canvas.</span></span>
2. <span data-ttu-id="c3de4-133">Kliknij przycisk **Uruchom selektor kolumn** w okienku toospecify właściwości hello, które kolumny mają toodrop.</span><span class="sxs-lookup"><span data-stu-id="c3de4-133">Click **Launch column selector** in hello Properties pane toospecify which columns you wish toodrop.</span></span>
   <span data-ttu-id="c3de4-134">![Kolumny projektu][4]</span><span class="sxs-lookup"><span data-stu-id="c3de4-134">![Project Columns][4]</span></span>
3. <span data-ttu-id="c3de4-135">Wyklucz dwie kolumny: CustomerAlternateKey i GeographyKey.</span><span class="sxs-lookup"><span data-stu-id="c3de4-135">Exclude two columns: CustomerAlternateKey and GeographyKey.</span></span>
   <span data-ttu-id="c3de4-136">![Usuwanie zbędnych kolumn][5]</span><span class="sxs-lookup"><span data-stu-id="c3de4-136">![Remove unnecessary columns][5]</span></span>

## <a name="3-build-hello-model"></a><span data-ttu-id="c3de4-137">3. Tworzenie modelu hello</span><span class="sxs-lookup"><span data-stu-id="c3de4-137">3. Build hello model</span></span>
<span data-ttu-id="c3de4-138">Podzielimy dane hello proporcji 80 – 20: 80% tootrain modelu uczenia maszynowego i 20% tootest hello modelu.</span><span class="sxs-lookup"><span data-stu-id="c3de4-138">We will split hello data 80-20: 80% tootrain a machine learning model and 20% tootest hello model.</span></span> <span data-ttu-id="c3de4-139">Firma Microsoft będzie wprowadzać użyj algorytmów "Dwuklasowych" hello, w przypadku tego problemu klasyfikacji binarnej.</span><span class="sxs-lookup"><span data-stu-id="c3de4-139">We will make use of hello “Two-Class” algorithms for this binary classification problem.</span></span>

1. <span data-ttu-id="c3de4-140">Przeciągnij hello **podziału** modułu na kanwie hello.</span><span class="sxs-lookup"><span data-stu-id="c3de4-140">Drag hello **Split** module into hello canvas.</span></span>
2. <span data-ttu-id="c3de4-141">Wprowadź wartość 0,8 w ułamek wierszy w hello pierwszy wyjściowy zestaw danych w okienku Properties hello.</span><span class="sxs-lookup"><span data-stu-id="c3de4-141">Enter 0.8 for Fraction of rows in hello first output dataset in hello Properties pane.</span></span>
   <span data-ttu-id="c3de4-142">![Podział danych na zestaw szkoleniowy i zestaw testowy][6]</span><span class="sxs-lookup"><span data-stu-id="c3de4-142">![Split data into training and test set][6]</span></span>
3. <span data-ttu-id="c3de4-143">Przeciągnij hello **Two-Class Boosted drzewa decyzyjnego** modułu na kanwie hello.</span><span class="sxs-lookup"><span data-stu-id="c3de4-143">Drag hello **Two-Class Boosted Decision Tree** module into hello canvas.</span></span>
4. <span data-ttu-id="c3de4-144">Przeciągnij hello **Train Model** modułu do hello obszaru roboczego i określ hello danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="c3de4-144">Drag hello **Train Model** module into hello canvas and specify hello inputs.</span></span> <span data-ttu-id="c3de4-145">Następnie kliknij przycisk **Uruchom selektor kolumn** w okienku Properties hello.</span><span class="sxs-lookup"><span data-stu-id="c3de4-145">Then, click **Launch column selector** in hello Properties pane.</span></span>
   * <span data-ttu-id="c3de4-146">Pierwsze dane wejściowe: algorytm uczenia maszynowego.</span><span class="sxs-lookup"><span data-stu-id="c3de4-146">First input: ML algorithm.</span></span>
   * <span data-ttu-id="c3de4-147">Drugie dane wejściowe: algorytm hello tootrain danych na.</span><span class="sxs-lookup"><span data-stu-id="c3de4-147">Second input: Data tootrain hello algorithm on.</span></span>
     <span data-ttu-id="c3de4-148">![Łączenie modułu Train Model hello][7]</span><span class="sxs-lookup"><span data-stu-id="c3de4-148">![Connect hello Train Model module][7]</span></span>
5. <span data-ttu-id="c3de4-149">Wybierz hello **BikeBuyer** kolumny hello toopredict kolumny.</span><span class="sxs-lookup"><span data-stu-id="c3de4-149">Select hello **BikeBuyer** column as hello column toopredict.</span></span>
   <span data-ttu-id="c3de4-150">![Wybierz kolumny toopredict][8]</span><span class="sxs-lookup"><span data-stu-id="c3de4-150">![Select Column toopredict][8]</span></span>

## <a name="4-score-hello-model"></a><span data-ttu-id="c3de4-151">4. Wynik hello modelu</span><span class="sxs-lookup"><span data-stu-id="c3de4-151">4. Score hello model</span></span>
<span data-ttu-id="c3de4-152">Zostanie teraz przetestować sposób wykonywania hello modelu na danych testowych.</span><span class="sxs-lookup"><span data-stu-id="c3de4-152">Now, we will test how hello model performs on test data.</span></span> <span data-ttu-id="c3de4-153">Porównamy algorytm hello z toosee innego algorytmu, który działa lepiej.</span><span class="sxs-lookup"><span data-stu-id="c3de4-153">We will compare hello algorithm of our choice with a different algorithm toosee which performs better.</span></span>

1. <span data-ttu-id="c3de4-154">Przeciągnij **Score Model** modułu na kanwie hello.</span><span class="sxs-lookup"><span data-stu-id="c3de4-154">Drag **Score Model** module into hello canvas.</span></span>
    <span data-ttu-id="c3de4-155">Pierwsze dane wejściowe: Uczony model drugie dane wejściowe: dane testowe ![Score hello model][9]</span><span class="sxs-lookup"><span data-stu-id="c3de4-155">First input: Trained model Second input: Test data ![Score hello model][9]</span></span>
2. <span data-ttu-id="c3de4-156">Przeciągnij hello **maszyna punktu Bayesa Two-Class** do kanwy eksperymentu hello.</span><span class="sxs-lookup"><span data-stu-id="c3de4-156">Drag hello **Two-Class Bayes Point Machine** into hello experiment canvas.</span></span> <span data-ttu-id="c3de4-157">Porównamy, jak ten algorytm wykonuje porównania toohello Two-Class Boosted drzewa decyzyjnego.</span><span class="sxs-lookup"><span data-stu-id="c3de4-157">We will compare how this algorithm performs in comparison toohello Two-Class Boosted Decision Tree.</span></span>
3. <span data-ttu-id="c3de4-158">Kopiuj i Wklej hello moduły Train Model i Score Model hello kanwy.</span><span class="sxs-lookup"><span data-stu-id="c3de4-158">Copy and Paste hello modules Train Model and Score Model in hello canvas.</span></span>
4. <span data-ttu-id="c3de4-159">Przeciągnij hello **Evaluate Model** modułu algorytmów hello kanwy toocompare hello dwa.</span><span class="sxs-lookup"><span data-stu-id="c3de4-159">Drag hello **Evaluate Model** module into hello canvas toocompare hello two algorithms.</span></span>
5. <span data-ttu-id="c3de4-160">**Uruchom** hello eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="c3de4-160">**Run** hello experiment.</span></span>
   <span data-ttu-id="c3de4-161">![Uruchom eksperyment hello][10]</span><span class="sxs-lookup"><span data-stu-id="c3de4-161">![Run hello experiment][10]</span></span>
6. <span data-ttu-id="c3de4-162">Kliknij port wyjściowy hello u dołu hello hello modułu Evaluate Model, a następnie kliknij pozycję Visualize.</span><span class="sxs-lookup"><span data-stu-id="c3de4-162">Click hello output port at hello bottom of hello Evaluate Model module and click Visualize.</span></span>
   <span data-ttu-id="c3de4-163">![Wizualizacja wyników oceny][11]</span><span class="sxs-lookup"><span data-stu-id="c3de4-163">![Visualize evaluation results][11]</span></span>

<span data-ttu-id="c3de4-164">podane metryki Hello są hello krzywą ROC, diagram precision-recall i podnieś krzywą.</span><span class="sxs-lookup"><span data-stu-id="c3de4-164">hello metrics provided are hello ROC curve, precision-recall diagram and lift curve.</span></span> <span data-ttu-id="c3de4-165">Na podstawie tych metryk, możemy stwierdzić, tym hello pierwszy model działa lepiej niż drugi hello.</span><span class="sxs-lookup"><span data-stu-id="c3de4-165">Looking at these metrics, we can see that hello first model performed better than hello second one.</span></span> <span data-ttu-id="c3de4-166">toolook na powitania co hello pierwszego modelu, kliknij port wyjściowy hello Score Model i kliknij pozycję Visualize.</span><span class="sxs-lookup"><span data-stu-id="c3de4-166">toolook at hello what hello first model predicted, click on output port of hello Score Model and click Visualize.</span></span>
<span data-ttu-id="c3de4-167">![Wizualizacja wyników klasyfikacji][12]</span><span class="sxs-lookup"><span data-stu-id="c3de4-167">![Visualize score results][12]</span></span>

<span data-ttu-id="c3de4-168">Zobaczysz, że dwie kolumny dodane tooyour zestawu danych testowych.</span><span class="sxs-lookup"><span data-stu-id="c3de4-168">You will see two more columns added tooyour test dataset.</span></span>

* <span data-ttu-id="c3de4-169">Scored Probabilities: hello prawdopodobieństwo, że klient jest nabywcą roweru.</span><span class="sxs-lookup"><span data-stu-id="c3de4-169">Scored Probabilities: hello likelihood that a customer is a bike buyer.</span></span>
* <span data-ttu-id="c3de4-170">Scored etykiety: hello klasyfikacja dokonana przez hello model — nabywca roweru (1) czy nie (0).</span><span class="sxs-lookup"><span data-stu-id="c3de4-170">Scored Labels: hello classification done by hello model – bike buyer (1) or not (0).</span></span> <span data-ttu-id="c3de4-171">Próg prawdopodobieństwa etykietowania ustawiono too50% i można go dostosować.</span><span class="sxs-lookup"><span data-stu-id="c3de4-171">This probability threshold for labeling is set too50% and can be adjusted.</span></span>

<span data-ttu-id="c3de4-172">Porównywanie kolumny hello BikeBuyer (rzeczywiste) z etykietami oceniane hello (Prognozowane), widać, jak wykonał hello modelu.</span><span class="sxs-lookup"><span data-stu-id="c3de4-172">Comparing hello column BikeBuyer (actual) with hello Scored Labels (prediction), you can see how well hello model has performed.</span></span> <span data-ttu-id="c3de4-173">W kolejnych krokach można użyć tego modelu toomake prognoz dotyczących nowych klientów i opublikować ten model jako usługę sieci web lub zapisać wyniki wstecz tooSQL hurtowni danych.</span><span class="sxs-lookup"><span data-stu-id="c3de4-173">As next steps, you can use this model toomake predictions for new customers and publish this model as a web service or write results back tooSQL Data Warehouse.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c3de4-174">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c3de4-174">Next steps</span></span>
<span data-ttu-id="c3de4-175">toolearn więcej informacji na temat tworzenia predykcyjnych modeli, uczenia maszynowego można znaleźć zbyt[tooMachine wprowadzenie Learning na platformie Azure][Introduction tooMachine Learning on Azure].</span><span class="sxs-lookup"><span data-stu-id="c3de4-175">toolearn more about building predictive machine learning models, refer too[Introduction tooMachine Learning on Azure][Introduction tooMachine Learning on Azure].</span></span>

<!--Image references-->
[1]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img1_reader.png
[2]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img2_visualize.png
[3]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img3_readerdata.png
[4]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img4_projectcolumns.png
[5]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img5_columnselector.png
[6]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img6_split.png
[7]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img7_train.png
[8]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img8_traincolumnselector.png
[9]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img9_score.png
[10]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img10_evaluate.png
[11]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img11_evalresults.png
[12]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img12_scoreresults.png


<!--Article references-->
[Azure Machine Learning studio]:https://studio.azureml.net/
[Introduction tooMachine Learning on Azure]:https://azure.microsoft.com/documentation/articles/machine-learning-what-is-machine-learning/
[load sample data manually]: sql-data-warehouse-load-sample-databases.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
