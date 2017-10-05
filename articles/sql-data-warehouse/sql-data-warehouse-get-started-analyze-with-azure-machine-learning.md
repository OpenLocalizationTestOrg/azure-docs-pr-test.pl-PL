---
title: "Analizowanie danych przy użyciu usługi Azure Machine Learning | Microsoft Docs"
description: "Używając usługi Azure Machine Learning, można utworzyć predykcyjny model uczenia maszynowego korzystający z danych przechowywanych w usłudze Azure SQL Data Warehouse."
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
ms.openlocfilehash: 3197948e32fe5c95b111fe5495a0e5f85966a24b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="analyze-data-with-azure-machine-learning"></a><span data-ttu-id="c3477-103">Analizowanie danych przy użyciu usługi Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="c3477-103">Analyze data with Azure Machine Learning</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c3477-104">Power BI</span><span class="sxs-lookup"><span data-stu-id="c3477-104">Power BI</span></span>](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [<span data-ttu-id="c3477-105">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="c3477-105">Azure Machine Learning</span></span>](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [<span data-ttu-id="c3477-106">Program Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c3477-106">Visual Studio</span></span>](sql-data-warehouse-query-visual-studio.md)
> * [<span data-ttu-id="c3477-107">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="c3477-107">sqlcmd</span></span>](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [<span data-ttu-id="c3477-108">SSMS</span><span class="sxs-lookup"><span data-stu-id="c3477-108">SSMS</span></span>](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="c3477-109">Ten samouczek przedstawia sposób tworzenia predykcyjnego modelu uczenia maszynowego przy użyciu usługi Azure Machine Learning korzystającej z danych przechowywanych w usłudze Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c3477-109">This tutorial uses Azure Machine Learning to build a predictive machine learning model based on data stored in Azure SQL Data Warehouse.</span></span> <span data-ttu-id="c3477-110">W szczególności ten samouczek omawia tworzenie ukierunkowanej kampanii marketingowej dla sklepu rowerowego Adventure Works przez prognozowanie prawdopodobieństwa zakupu roweru przez klienta.</span><span class="sxs-lookup"><span data-stu-id="c3477-110">Specifically, this builds a targeted marketing campaign for Adventure Works, the bike shop, by predicting if a customer is likely to buy a bike or not.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Integrating-Azure-Machine-Learning-with-Azure-SQL-Data-Warehouse/player]
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="c3477-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="c3477-111">Prerequisites</span></span>
<span data-ttu-id="c3477-112">Do wykonania kroków opisanych w tym samouczku potrzebne są:</span><span class="sxs-lookup"><span data-stu-id="c3477-112">To step through this tutorial, you need:</span></span>

* <span data-ttu-id="c3477-113">Baza danych usługi SQL Data Warehouse. ze wstępnie załadowanymi danymi z bazy danych AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="c3477-113">A SQL Data Warehouse pre-loaded with AdventureWorksDW sample data.</span></span> <span data-ttu-id="c3477-114">Aby dowiedzieć się, jak załadować dane przykładowe, zobacz [Tworzenie magazynu danych SQL Data Warehouse][Create a SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="c3477-114">To provision this, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse] and choose to load the sample data.</span></span> <span data-ttu-id="c3477-115">Jeśli masz już magazyn danych, ale bez przykładowych danych, możesz [ręcznie załadować przykładowe dane][load sample data manually].</span><span class="sxs-lookup"><span data-stu-id="c3477-115">If you already have a data warehouse but do not have sample data, you can [load sample data manually][load sample data manually].</span></span>

## <a name="1-get-the-data"></a><span data-ttu-id="c3477-116">1. Pobieranie danych</span><span class="sxs-lookup"><span data-stu-id="c3477-116">1. Get the data</span></span>
<span data-ttu-id="c3477-117">Dane znajdują się w widoku dbo.vTargetMail w bazie danych AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="c3477-117">The data is in the dbo.vTargetMail view in the AdventureWorksDW database.</span></span> <span data-ttu-id="c3477-118">Aby odczytać te dane:</span><span class="sxs-lookup"><span data-stu-id="c3477-118">To read this data:</span></span>

1. <span data-ttu-id="c3477-119">Zaloguj się do programu [Azure Machine Learning Studio][Azure Machine Learning studio] i kliknij eksperymenty.</span><span class="sxs-lookup"><span data-stu-id="c3477-119">Sign into [Azure Machine Learning studio][Azure Machine Learning studio] and click on my experiments.</span></span>
2. <span data-ttu-id="c3477-120">Kliknij przycisk **+ NOWE** i wybierz pozycję **Blank Experiment** (Pusty eksperyment).</span><span class="sxs-lookup"><span data-stu-id="c3477-120">Click **+NEW** and select **Blank Experiment**.</span></span>
3. <span data-ttu-id="c3477-121">Wprowadź nazwę swojego eksperymentu: Targeted Marketing (Marketing docelowy).</span><span class="sxs-lookup"><span data-stu-id="c3477-121">Enter a name for your experiment: Targeted Marketing.</span></span>
4. <span data-ttu-id="c3477-122">Przeciągnij moduł **Reader** (Czytnik) z okienka modułów do kanwy.</span><span class="sxs-lookup"><span data-stu-id="c3477-122">Drag the **Reader** module from the modules pane into the canvas.</span></span>
5. <span data-ttu-id="c3477-123">Określ szczegóły bazy danych usługi SQL Data Warehouse w okienku Properties (Właściwości).</span><span class="sxs-lookup"><span data-stu-id="c3477-123">Specify the details of your SQL Data Warehouse database in the Properties pane.</span></span>
6. <span data-ttu-id="c3477-124">Określ **zapytanie** do bazy danych, aby odczytać potrzebne dane.</span><span class="sxs-lookup"><span data-stu-id="c3477-124">Specify the database **query** to read the data of interest.</span></span>

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

<span data-ttu-id="c3477-125">Aby uruchomić eksperyment, kliknij pozycję **Run** (Uruchom) na kanwie eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="c3477-125">Run the experiment by clicking **Run** under the experiment canvas.</span></span>
<span data-ttu-id="c3477-126">![Uruchamianie eksperymentu][1]</span><span class="sxs-lookup"><span data-stu-id="c3477-126">![Run the experiment][1]</span></span>

<span data-ttu-id="c3477-127">Po pomyślnym wykonaniu eksperymentu kliknij port wyjściowy na dole modułu Reader (Czytnik) i wybierz opcję **Visualize** (Wizualizacja), aby wyświetlić zaimportowane danych.</span><span class="sxs-lookup"><span data-stu-id="c3477-127">After the experiment finishes running successfully, click the output port at the bottom of the Reader module and select **Visualize** to see the imported data.</span></span>
<span data-ttu-id="c3477-128">![Wyświetlanie zaimportowanych danych][3]</span><span class="sxs-lookup"><span data-stu-id="c3477-128">![View imported data][3]</span></span>

## <a name="2-clean-the-data"></a><span data-ttu-id="c3477-129">2. Czyszczenie danych</span><span class="sxs-lookup"><span data-stu-id="c3477-129">2. Clean the data</span></span>
<span data-ttu-id="c3477-130">Aby wyczyścić dane, usuń kilka kolumn, które nie są istotne dla modelu.</span><span class="sxs-lookup"><span data-stu-id="c3477-130">To clean the data, drop some columns that are not relevant for the model.</span></span> <span data-ttu-id="c3477-131">W tym celu:</span><span class="sxs-lookup"><span data-stu-id="c3477-131">To do this:</span></span>

1. <span data-ttu-id="c3477-132">Przeciągnij moduł **Project Columns** (Kolumny projektu) na kanwę.</span><span class="sxs-lookup"><span data-stu-id="c3477-132">Drag the **Project Columns** module into the canvas.</span></span>
2. <span data-ttu-id="c3477-133">Kliknij pozycję **Launch column selector** (Uruchom selektor kolumn) w okienku Properties (Właściwości), aby wskazać kolumny do usunięcia.</span><span class="sxs-lookup"><span data-stu-id="c3477-133">Click **Launch column selector** in the Properties pane to specify which columns you wish to drop.</span></span>
   <span data-ttu-id="c3477-134">![Kolumny projektu][4]</span><span class="sxs-lookup"><span data-stu-id="c3477-134">![Project Columns][4]</span></span>
3. <span data-ttu-id="c3477-135">Wyklucz dwie kolumny: CustomerAlternateKey i GeographyKey.</span><span class="sxs-lookup"><span data-stu-id="c3477-135">Exclude two columns: CustomerAlternateKey and GeographyKey.</span></span>
   <span data-ttu-id="c3477-136">![Usuwanie zbędnych kolumn][5]</span><span class="sxs-lookup"><span data-stu-id="c3477-136">![Remove unnecessary columns][5]</span></span>

## <a name="3-build-the-model"></a><span data-ttu-id="c3477-137">3. Tworzenie modelu</span><span class="sxs-lookup"><span data-stu-id="c3477-137">3. Build the model</span></span>
<span data-ttu-id="c3477-138">Podzielimy dane w proporcji 80–20: 80% do trenowania tworzenia modelu uczenia maszynowego i 20% do testowania modelu.</span><span class="sxs-lookup"><span data-stu-id="c3477-138">We will split the data 80-20: 80% to train a machine learning model and 20% to test the model.</span></span> <span data-ttu-id="c3477-139">Użyjemy algorytmów „dwuklasowych” do rozwiązania tego problemu klasyfikacji binarnej.</span><span class="sxs-lookup"><span data-stu-id="c3477-139">We will make use of the “Two-Class” algorithms for this binary classification problem.</span></span>

1. <span data-ttu-id="c3477-140">Przeciągnij moduł **Split** (Podział) na kanwę.</span><span class="sxs-lookup"><span data-stu-id="c3477-140">Drag the **Split** module into the canvas.</span></span>
2. <span data-ttu-id="c3477-141">Wprowadź wartość 0,8 w polu Fraction of rows in the first output dataset (Ułamek wierszy w pierwszym zestawie danych wyjściowych) w okienku Properties (Właściwości).</span><span class="sxs-lookup"><span data-stu-id="c3477-141">Enter 0.8 for Fraction of rows in the first output dataset in the Properties pane.</span></span>
   <span data-ttu-id="c3477-142">![Podział danych na zestaw szkoleniowy i zestaw testowy][6]</span><span class="sxs-lookup"><span data-stu-id="c3477-142">![Split data into training and test set][6]</span></span>
3. <span data-ttu-id="c3477-143">Przeciągnij moduł **Two-Class Boosted Decision Tree** (Dwuklasowe wzmocnione drzewo decyzyjne) na kanwę.</span><span class="sxs-lookup"><span data-stu-id="c3477-143">Drag the **Two-Class Boosted Decision Tree** module into the canvas.</span></span>
4. <span data-ttu-id="c3477-144">Przeciągnij moduł **Train Model** (Model szkoleniowy) na kanwę i określ dane wejściowe.</span><span class="sxs-lookup"><span data-stu-id="c3477-144">Drag the **Train Model** module into the canvas and specify the inputs.</span></span> <span data-ttu-id="c3477-145">Następnie kliknij przycisk **Launch column selector** (Uruchom selektor kolumn) w okienku Properties (Właściwości).</span><span class="sxs-lookup"><span data-stu-id="c3477-145">Then, click **Launch column selector** in the Properties pane.</span></span>
   * <span data-ttu-id="c3477-146">Pierwsze dane wejściowe: algorytm uczenia maszynowego.</span><span class="sxs-lookup"><span data-stu-id="c3477-146">First input: ML algorithm.</span></span>
   * <span data-ttu-id="c3477-147">Drugie dane wejściowe: dane do szkolenia w zakresie algorytmu.</span><span class="sxs-lookup"><span data-stu-id="c3477-147">Second input: Data to train the algorithm on.</span></span>
     <span data-ttu-id="c3477-148">![Łączenie modułu Train Model (Model szkoleniowy)][7]</span><span class="sxs-lookup"><span data-stu-id="c3477-148">![Connect the Train Model module][7]</span></span>
5. <span data-ttu-id="c3477-149">Wybierz kolumnę **BikeBuyer** (Nabywca roweru) jako kolumnę do prognozowania.</span><span class="sxs-lookup"><span data-stu-id="c3477-149">Select the **BikeBuyer** column as the column to predict.</span></span>
   <span data-ttu-id="c3477-150">![Wybór kolumny do prognozowania][8]</span><span class="sxs-lookup"><span data-stu-id="c3477-150">![Select Column to predict][8]</span></span>

## <a name="4-score-the-model"></a><span data-ttu-id="c3477-151">4. Ocena modelu</span><span class="sxs-lookup"><span data-stu-id="c3477-151">4. Score the model</span></span>
<span data-ttu-id="c3477-152">Teraz przetestujemy działanie modelu na danych testowych.</span><span class="sxs-lookup"><span data-stu-id="c3477-152">Now, we will test how the model performs on test data.</span></span> <span data-ttu-id="c3477-153">Porównamy wybrany algorytm z innym algorytmem, aby zobaczyć, który działa lepiej.</span><span class="sxs-lookup"><span data-stu-id="c3477-153">We will compare the algorithm of our choice with a different algorithm to see which performs better.</span></span>

1. <span data-ttu-id="c3477-154">Przeciągnij moduł **Score model** (Model klasyfikacyjny) na kanwę.</span><span class="sxs-lookup"><span data-stu-id="c3477-154">Drag **Score Model** module into the canvas.</span></span>
    <span data-ttu-id="c3477-155">Pierwsze dane wejściowe: model szkoleniowy Drugie dane wejściowe: dane testowe ![Klasyfikacja modelu][9]</span><span class="sxs-lookup"><span data-stu-id="c3477-155">First input: Trained model Second input: Test data ![Score the model][9]</span></span>
2. <span data-ttu-id="c3477-156">Przeciągnij moduł **Two-Class Bayes Point Machine** (Dwuklasowa maszyna punktu Bayesa) do kanwy eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="c3477-156">Drag the **Two-Class Bayes Point Machine** into the experiment canvas.</span></span> <span data-ttu-id="c3477-157">Porównamy działanie tego algorytmu z algorytmem Two-Class Boosted Decision Tree (Dwuklasowe wzmocnione drzewo decyzyjne).</span><span class="sxs-lookup"><span data-stu-id="c3477-157">We will compare how this algorithm performs in comparison to the Two-Class Boosted Decision Tree.</span></span>
3. <span data-ttu-id="c3477-158">Skopiuj i wklej moduły Train Model (Model szkoleniowy) i Score Model (Model klasyfikacyjny) do kanwy.</span><span class="sxs-lookup"><span data-stu-id="c3477-158">Copy and Paste the modules Train Model and Score Model in the canvas.</span></span>
4. <span data-ttu-id="c3477-159">Przeciągnij moduł **Evaluate Model** (Ocena modelu) do kanwy, aby porównać oba algorytmy.</span><span class="sxs-lookup"><span data-stu-id="c3477-159">Drag the **Evaluate Model** module into the canvas to compare the two algorithms.</span></span>
5. <span data-ttu-id="c3477-160">Kliknij przycisk **Run** (Uruchom), aby uruchomić eksperyment</span><span class="sxs-lookup"><span data-stu-id="c3477-160">**Run** the experiment.</span></span>
   <span data-ttu-id="c3477-161">![Uruchamianie eksperymentu][10]</span><span class="sxs-lookup"><span data-stu-id="c3477-161">![Run the experiment][10]</span></span>
6. <span data-ttu-id="c3477-162">Kliknij port wyjściowy w dolnej części modułu Evaluate Model (Ocena modelu), a następnie kliknij pozycję Visualize (Wizualizacja).</span><span class="sxs-lookup"><span data-stu-id="c3477-162">Click the output port at the bottom of the Evaluate Model module and click Visualize.</span></span>
   <span data-ttu-id="c3477-163">![Wizualizacja wyników oceny][11]</span><span class="sxs-lookup"><span data-stu-id="c3477-163">![Visualize evaluation results][11]</span></span>

<span data-ttu-id="c3477-164">Podane metryki obejmują krzywą ROC, diagram precision-recall oraz krzywą wzrostu.</span><span class="sxs-lookup"><span data-stu-id="c3477-164">The metrics provided are the ROC curve, precision-recall diagram and lift curve.</span></span> <span data-ttu-id="c3477-165">Na podstawie tych metryk możemy stwierdzić, że pierwszy model działa lepiej niż drugi.</span><span class="sxs-lookup"><span data-stu-id="c3477-165">Looking at these metrics, we can see that the first model performed better than the second one.</span></span> <span data-ttu-id="c3477-166">Aby przyjrzeć się prognozom pierwszego modelu, kliknij port wyjściowy modułu Score Model (Model klasyfikacyjny) i kliknij pozycję Visualize (Wizualizacja).</span><span class="sxs-lookup"><span data-stu-id="c3477-166">To look at the what the first model predicted, click on output port of the Score Model and click Visualize.</span></span>
<span data-ttu-id="c3477-167">![Wizualizacja wyników klasyfikacji][12]</span><span class="sxs-lookup"><span data-stu-id="c3477-167">![Visualize score results][12]</span></span>

<span data-ttu-id="c3477-168">Zostaną wyświetlone dwie kolumny dodane do zestawu danych testowych.</span><span class="sxs-lookup"><span data-stu-id="c3477-168">You will see two more columns added to your test dataset.</span></span>

* <span data-ttu-id="c3477-169">Scored Probabilities (Sklasyfikowane prawdopodobieństwo): prawdopodobieństwo, że klient jest nabywcą roweru.</span><span class="sxs-lookup"><span data-stu-id="c3477-169">Scored Probabilities: the likelihood that a customer is a bike buyer.</span></span>
* <span data-ttu-id="c3477-170">Scored Labels (Sklasyfikowane etykiety): klasyfikacja dokonana przez model — nabywca roweru (1) lub nie (0).</span><span class="sxs-lookup"><span data-stu-id="c3477-170">Scored Labels: the classification done by the model – bike buyer (1) or not (0).</span></span> <span data-ttu-id="c3477-171">Ustawiony próg prawdopodobieństwa etykietowania wynosi 50% i można go dostosować.</span><span class="sxs-lookup"><span data-stu-id="c3477-171">This probability threshold for labeling is set to 50% and can be adjusted.</span></span>

<span data-ttu-id="c3477-172">Porównując wartości w kolumnach BikeBuyer (Nabywca roweru) (rzeczywiste) oraz Scored Labels (Sklasyfikowane etykiety) (prognozowane), można określić prawidłowość działania modelu.</span><span class="sxs-lookup"><span data-stu-id="c3477-172">Comparing the column BikeBuyer (actual) with the Scored Labels (prediction), you can see how well the model has performed.</span></span> <span data-ttu-id="c3477-173">W kolejnych krokach można użyć tego modelu w celu tworzenia prognoz dotyczących nowych klientów i opublikować ten model jako usługę sieci Web lub zapisać wyniki z powrotem w bazie danych usługi SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c3477-173">As next steps, you can use this model to make predictions for new customers and publish this model as a web service or write results back to SQL Data Warehouse.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c3477-174">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c3477-174">Next steps</span></span>
<span data-ttu-id="c3477-175">Aby dowiedzieć się więcej o tworzeniu predykcyjnych modeli uczenia maszynowego, zapoznaj się z artykułem [Wprowadzenie do usługi Machine Learning na platformie Azure][Introduction to Machine Learning on Azure].</span><span class="sxs-lookup"><span data-stu-id="c3477-175">To learn more about building predictive machine learning models, refer to [Introduction to Machine Learning on Azure][Introduction to Machine Learning on Azure].</span></span>

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
[Introduction to Machine Learning on Azure]:https://azure.microsoft.com/documentation/articles/machine-learning-what-is-machine-learning/
[load sample data manually]: sql-data-warehouse-load-sample-databases.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
