---
title: "aaaUse usługi Azure Machine Learning z usługą Magazyn danych SQL | Dokumentacja firmy Microsoft"
description: "Samouczek korzystania z usługi Azure Machine Learning z usługą Azure SQL Data Warehouse w celu opracowywania rozwiązań."
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: barbkess
editor: 
ms.assetid: ac6bc731-6add-47a9-b3fe-68996e656f4d
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: kevin;barbkess
ms.openlocfilehash: fdfe8c936d2bb7a02163a0bbf6435e1ebd518d4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-machine-learning-with-sql-data-warehouse"></a><span data-ttu-id="294c9-103">Użyj usługi Azure Machine Learning z usługą Magazyn danych SQL</span><span class="sxs-lookup"><span data-stu-id="294c9-103">Use Azure Machine Learning with SQL Data Warehouse</span></span>
<span data-ttu-id="294c9-104">Usługa Azure Machine Learning to usługa analizy predykcyjnej w pełni zarządzana, użyj modeli predykcyjnych toocreate względem danych w magazynie danych SQL, a następnie opublikować jako gotowe do użycia usług sieci web.</span><span class="sxs-lookup"><span data-stu-id="294c9-104">Azure Machine Learning is a fully managed predictive analytics service that you can use toocreate predictive models against your data in SQL Data Warehouse, and then publish as ready-to-consume web services.</span></span> <span data-ttu-id="294c9-105">Można dowiedzieć się hello podstaw analizy predykcyjnej i uczenia maszynowego, odczytując [tooMachine wprowadzenie Learning na platformie Azure][Introduction tooMachine Learning on Azure].</span><span class="sxs-lookup"><span data-stu-id="294c9-105">You can learn hello basics of predictive analytics and machine learning by reading [Introduction tooMachine Learning on Azure][Introduction tooMachine Learning on Azure].</span></span>  <span data-ttu-id="294c9-106">Można następnie dowiesz się, jak toocreate, uczenia, wynik i przetestowania modelu uczenia maszynowego przy użyciu hello [tworzenie eksperymentu samouczek][Create experiment tutorial].</span><span class="sxs-lookup"><span data-stu-id="294c9-106">You can then learn how toocreate, train, score and test a machine learning model using hello [Create experiment tutorial][Create experiment tutorial].</span></span>

<span data-ttu-id="294c9-107">W tym artykule przedstawiono sposób hello toodo po użyciu hello [Azure Machine Learning Studio][Azure Machine Learning Studio]:</span><span class="sxs-lookup"><span data-stu-id="294c9-107">In this article, you will learn how toodo hello following using hello [Azure Machine Learning Studio][Azure Machine Learning Studio]:</span></span>

* <span data-ttu-id="294c9-108">Odczytywanie danych z programu toocreate bazy danych, szkolenia i score model predykcyjny</span><span class="sxs-lookup"><span data-stu-id="294c9-108">Read data from your database toocreate, train and score a predictive model</span></span>
* <span data-ttu-id="294c9-109">Zapisu bazy danych tooyour danych</span><span class="sxs-lookup"><span data-stu-id="294c9-109">Write data tooyour database</span></span>

## <a name="read-data-from-sql-data-warehouse"></a><span data-ttu-id="294c9-110">Odczyt danych z magazynu danych SQL</span><span class="sxs-lookup"><span data-stu-id="294c9-110">Read data from SQL Data Warehouse</span></span>
<span data-ttu-id="294c9-111">Firma Microsoft będzie odczytywać dane z tabeli produktu w bazie danych AdventureWorksDW hello.</span><span class="sxs-lookup"><span data-stu-id="294c9-111">We will read data from Product table in hello AdventureWorksDW database.</span></span>

### <a name="step-1"></a><span data-ttu-id="294c9-112">Krok 1</span><span class="sxs-lookup"><span data-stu-id="294c9-112">Step 1</span></span>
<span data-ttu-id="294c9-113">Uruchom nowy eksperyment, klikając + nowy u dołu okna Machine Learning Studio hello hello wybierz EKSPERYMENTU, a następnie wybierz, pusty eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="294c9-113">Start a new experiment by clicking +NEW at hello bottom of hello Machine Learning Studio window, select EXPERIMENT, and then select Blank Experiment.</span></span> <span data-ttu-id="294c9-114">Wybierz hello domyślne nazwy u góry hello hello kanwy eksperymentu i zmień jego nazwę na toosomething opisowy, na przykład Prognozowanie cen roweru.</span><span class="sxs-lookup"><span data-stu-id="294c9-114">Select hello default experiment name at hello top of hello canvas and rename it toosomething meaningful, for example, Bicycle price prediction.</span></span>

### <a name="step-2"></a><span data-ttu-id="294c9-115">Krok 2</span><span class="sxs-lookup"><span data-stu-id="294c9-115">Step 2</span></span>
<span data-ttu-id="294c9-116">Poszukaj moduł czytnika hello w palecie hello zestawów danych i moduły powitania po lewej stronie kanwy eksperymentu hello.</span><span class="sxs-lookup"><span data-stu-id="294c9-116">Look for hello Reader module in hello palette of datasets and modules on hello left of hello experiment canvas.</span></span> <span data-ttu-id="294c9-117">Przeciągnij hello modułu toohello eksperymentu w obszarze roboczym.</span><span class="sxs-lookup"><span data-stu-id="294c9-117">Drag hello module toohello experiment canvas.</span></span>
![][drag_reader]

### <a name="step-3"></a><span data-ttu-id="294c9-118">Krok 3</span><span class="sxs-lookup"><span data-stu-id="294c9-118">Step 3</span></span>
<span data-ttu-id="294c9-119">Wybierz moduł czytnika hello i wypełnij hello w okienku właściwości.</span><span class="sxs-lookup"><span data-stu-id="294c9-119">Select hello Reader module and fill out hello properties pane.</span></span>

1. <span data-ttu-id="294c9-120">Wybierz bazę danych SQL Azure jako hello źródła danych.</span><span class="sxs-lookup"><span data-stu-id="294c9-120">Select Azure SQL Database as hello Data Source.</span></span>
2. <span data-ttu-id="294c9-121">Nazwa serwera bazy danych: Nazwa serwera hello typu.</span><span class="sxs-lookup"><span data-stu-id="294c9-121">Database server name: Type hello server name.</span></span> <span data-ttu-id="294c9-122">Można użyć hello [portalu Azure] [ Azure portal] toofind to.</span><span class="sxs-lookup"><span data-stu-id="294c9-122">You can use hello [Azure portal][Azure portal] toofind this.</span></span>

![][server_name]

1. <span data-ttu-id="294c9-123">Nazwa bazy danych: Nazwa typu hello bazy danych na serwerze hello właśnie zostało określone.</span><span class="sxs-lookup"><span data-stu-id="294c9-123">Database name: Type hello name of a database on hello server you just specified.</span></span>
2. <span data-ttu-id="294c9-124">Nazwa konta użytkownika serwera: nazwa użytkownika hello typu konta, które ma uprawnienia dostępu do bazy danych hello.</span><span class="sxs-lookup"><span data-stu-id="294c9-124">Server user account name:  Type hello user name of an account that has access permissions for hello database.</span></span>
3. <span data-ttu-id="294c9-125">Hasło konta użytkownika serwera: Podaj hasło hello hello określone konto użytkownika.</span><span class="sxs-lookup"><span data-stu-id="294c9-125">Server user account password: Provide hello password for hello specified user account.</span></span>
4. <span data-ttu-id="294c9-126">Dowolny certyfikat serwera Zaakceptuj: użyć tej opcji (mniej bezpieczna opcja), jeśli tooskip recenzowania hello certyfikatu witryny, przed przeczytaniem danych.</span><span class="sxs-lookup"><span data-stu-id="294c9-126">Accept any server certificate: Use this option (less secure) if you want tooskip reviewing hello site certificate before you read your data.</span></span>
5. <span data-ttu-id="294c9-127">Zapytanie bazy danych: wprowadź instrukcję SQL opisujący hello dane, które mają tooread.</span><span class="sxs-lookup"><span data-stu-id="294c9-127">Database query: Enter a SQL statement that describes hello data you want tooread.</span></span> <span data-ttu-id="294c9-128">W takim przypadku firma Microsoft będzie odczytywać dane z tabel produktu za pomocą hello następującego zapytania.</span><span class="sxs-lookup"><span data-stu-id="294c9-128">In this case, we will read data from Product table using hello following query.</span></span>

```SQL
SELECT ProductKey, EnglishProductName, StandardCost,
        ListPrice, Size, Weight, DaysToManufacture,
        Class, Style, Color
FROM dbo.DimProduct;
```

![][reader_properties]

### <a name="step-4"></a><span data-ttu-id="294c9-129">Krok 4</span><span class="sxs-lookup"><span data-stu-id="294c9-129">Step 4</span></span>
1. <span data-ttu-id="294c9-130">Uruchom eksperyment hello klikając przycisk Uruchom obszarze kanwy eksperymentu hello.</span><span class="sxs-lookup"><span data-stu-id="294c9-130">Run hello experiment by clicking Run under hello experiment canvas.</span></span>
2. <span data-ttu-id="294c9-131">Po zakończeniu eksperymentu hello moduł czytnika hello będzie miał tooindicate zielony znacznik wyboru, która została pomyślnie ukończona.</span><span class="sxs-lookup"><span data-stu-id="294c9-131">When hello experiment finishes, hello Reader module will have a green check mark tooindicate that it has completed successfully.</span></span> <span data-ttu-id="294c9-132">Zwróć uwagę, również hello bieżący stan w prawym górnym rogu hello zakończone.</span><span class="sxs-lookup"><span data-stu-id="294c9-132">Notice also hello Finished running status in hello upper-right corner.</span></span>

![][run]

1. <span data-ttu-id="294c9-133">toosee hello importowanych danych, kliknij port wyjściowy hello u dołu hello hello samochodów zestawu danych i wybierz wizualizacja.</span><span class="sxs-lookup"><span data-stu-id="294c9-133">toosee hello imported data, click hello output port at hello bottom of hello automobile dataset and select Visualize.</span></span>

## <a name="create-train-and-score-a-model"></a><span data-ttu-id="294c9-134">Tworzenie, uczenie i score model</span><span class="sxs-lookup"><span data-stu-id="294c9-134">Create, train and score a model</span></span>
<span data-ttu-id="294c9-135">Teraz można używać tego elementu dataset do:</span><span class="sxs-lookup"><span data-stu-id="294c9-135">Now you can use this dataset to:</span></span>

* <span data-ttu-id="294c9-136">Tworzenie modelu: przetwarzanie danych i zdefiniować funkcji</span><span class="sxs-lookup"><span data-stu-id="294c9-136">Create a Model: Process data and define features</span></span>
* <span data-ttu-id="294c9-137">Train hello model: Wybieranie i stosowanie algorytmu uczenia</span><span class="sxs-lookup"><span data-stu-id="294c9-137">Train hello model: Choose and apply a learning algorithm</span></span>
* <span data-ttu-id="294c9-138">Oceny i testowania hello modelu: przewidywanie nowych cen rowerów</span><span class="sxs-lookup"><span data-stu-id="294c9-138">Score and test hello model: Predict new bicycle price</span></span>

![][model]

<span data-ttu-id="294c9-139">więcej informacji na temat sposobu toocreate, uczenia, generowanie wyników i testowanie hello Użyj modelu uczenia maszynowego toolearn [tworzenie eksperymentu samouczek][Create experiment tutorial].</span><span class="sxs-lookup"><span data-stu-id="294c9-139">toolearn more about how toocreate, train, score and test a machine learning model use hello [Create experiment tutorial][Create experiment tutorial].</span></span>

## <a name="write-data-tooazure-sql-data-warehouse"></a><span data-ttu-id="294c9-140">Zapis tooAzure danych magazynu danych SQL</span><span class="sxs-lookup"><span data-stu-id="294c9-140">Write data tooAzure SQL Data Warehouse</span></span>
<span data-ttu-id="294c9-141">Firma Microsoft będzie zapisywać tabeli tooProductPriceForecast zestaw wyników hello w bazie danych AdventureWorksDW hello.</span><span class="sxs-lookup"><span data-stu-id="294c9-141">We will write hello result set tooProductPriceForecast table in hello AdventureWorksDW database.</span></span>

### <a name="step-1"></a><span data-ttu-id="294c9-142">Krok 1</span><span class="sxs-lookup"><span data-stu-id="294c9-142">Step 1</span></span>
<span data-ttu-id="294c9-143">Poszukaj hello moduł zapisu w palecie hello zestawów danych i moduły powitania po lewej stronie kanwy eksperymentu hello.</span><span class="sxs-lookup"><span data-stu-id="294c9-143">Look for hello Writer module in hello palette of datasets and modules on hello left of hello experiment canvas.</span></span> <span data-ttu-id="294c9-144">Przeciągnij hello modułu toohello eksperymentu w obszarze roboczym.</span><span class="sxs-lookup"><span data-stu-id="294c9-144">Drag hello module toohello experiment canvas.</span></span>

![][drag_writer]

### <a name="step-2"></a><span data-ttu-id="294c9-145">Krok 2</span><span class="sxs-lookup"><span data-stu-id="294c9-145">Step 2</span></span>
<span data-ttu-id="294c9-146">Wybierz moduł zapisywania hello i wypełnij hello w okienku właściwości.</span><span class="sxs-lookup"><span data-stu-id="294c9-146">Select hello Writer module and fill out hello properties pane.</span></span>

1. <span data-ttu-id="294c9-147">Wybierz bazę danych SQL Azure jako hello miejsce docelowe danych.</span><span class="sxs-lookup"><span data-stu-id="294c9-147">Select Azure SQL Database as hello Data Destination.</span></span>
2. <span data-ttu-id="294c9-148">Nazwa serwera bazy danych: Nazwa serwera hello typu.</span><span class="sxs-lookup"><span data-stu-id="294c9-148">Database server name: Type hello server name.</span></span> <span data-ttu-id="294c9-149">Można użyć hello [portalu Azure] [ Azure portal] toofind to.</span><span class="sxs-lookup"><span data-stu-id="294c9-149">You can use hello [Azure portal][Azure portal] toofind this.</span></span>
3. <span data-ttu-id="294c9-150">Nazwa bazy danych: Nazwa typu hello bazy danych na serwerze hello właśnie zostało określone.</span><span class="sxs-lookup"><span data-stu-id="294c9-150">Database name: Type hello name of a database on hello server you just specified.</span></span>
4. <span data-ttu-id="294c9-151">Nazwa konta użytkownika serwera: nazwa użytkownika hello typu konta, które ma uprawnienia do zapisu dla hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="294c9-151">Server user account name:  Type hello user name of an account that has write permissions for hello database.</span></span>
5. <span data-ttu-id="294c9-152">Hasło konta użytkownika serwera: Podaj hasło hello hello określone konto użytkownika.</span><span class="sxs-lookup"><span data-stu-id="294c9-152">Server user account password: Provide hello password for hello specified user account.</span></span>
6. <span data-ttu-id="294c9-153">Zaakceptuj wszystkie certyfikatu serwera (niebezpieczne): Wybierz tę opcję, jeśli nie chcesz tooview hello certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="294c9-153">Accept any server certificate (insecure): Select this option if you don’t want tooview hello certificate.</span></span>
7. <span data-ttu-id="294c9-154">Rozdzielana przecinkami lista kolumn toobe zapisane: Podaj listę hello zestawu danych lub wynik kolumn, które mają toooutput.</span><span class="sxs-lookup"><span data-stu-id="294c9-154">Comma-separated list of columns toobe saved: Provide a list of hello dataset or result columns that you want toooutput.</span></span>
8. <span data-ttu-id="294c9-155">Nazwa tabeli danych: Określ nazwę hello hello danych tabeli.</span><span class="sxs-lookup"><span data-stu-id="294c9-155">Data table name: Specify hello name of hello data table.</span></span>
9. <span data-ttu-id="294c9-156">Rozdzielana przecinkami lista kolumn elementu datatable: Określ toouse nazwy kolumny hello hello nowej tabeli.</span><span class="sxs-lookup"><span data-stu-id="294c9-156">Comma-separated list of datatable columns:  Specify hello column names toouse in hello new table.</span></span> <span data-ttu-id="294c9-157">Witaj nazwy kolumny może różnić się od hello widocznych w zestawie hello źródła danych, ale musi zawierać taką samą liczbę kolumn w tym miejscu zdefiniowane dla tabeli wyjściowej hello hello.</span><span class="sxs-lookup"><span data-stu-id="294c9-157">hello column names can be different from hello ones in hello source dataset, but you must list hello same number of columns here that you define for hello output table.</span></span>
10. <span data-ttu-id="294c9-158">Liczba wierszy, zapisany dla operacji SQL Azure: można skonfigurować hello liczby wierszy, które są zapisywane tooa bazy danych SQL w ramach jednej operacji.</span><span class="sxs-lookup"><span data-stu-id="294c9-158">Number of rows written per SQL Azure operation: You can configure hello number of rows that are written tooa SQL database in one operation.</span></span>

![][writer_properties]

### <a name="step-3"></a><span data-ttu-id="294c9-159">Krok 3</span><span class="sxs-lookup"><span data-stu-id="294c9-159">Step 3</span></span>
1. <span data-ttu-id="294c9-160">Uruchom eksperyment hello klikając przycisk Uruchom obszarze kanwy eksperymentu hello.</span><span class="sxs-lookup"><span data-stu-id="294c9-160">Run hello experiment by clicking Run under hello experiment canvas.</span></span>
2. <span data-ttu-id="294c9-161">Po zakończeniu eksperymentu hello wszystkie moduły będą mieć tooindicate zielony znacznik wyboru, które zostały ukończone pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="294c9-161">When hello experiment finishes, all modules will have a green check mark tooindicate that they completed successfully.</span></span>

## <a name="next-steps"></a><span data-ttu-id="294c9-162">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="294c9-162">Next steps</span></span>
<span data-ttu-id="294c9-163">Więcej porad dla deweloperów znajduje się w artykule [Omówienie programowania w usłudze SQL Data Warehouse][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="294c9-163">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

<!--Image references-->

[drag_reader]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-drag-reader.png
[server_name]: ./media/sql-data-warehouse-integrate-azure-machine-learning/dw-server-name.png
[reader_properties]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-reader-properties.png
[run]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-finished-running.png
[model]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-create-train-score-model.png
[drag_writer]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-drag-writer.png
[writer_properties]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-writer-properties.png

<!--Article references-->

[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
[Create experiment tutorial]: https://azure.microsoft.com/documentation/articles/machine-learning-create-experiment/
[Introduction toomachine learning on Azure]: https://azure.microsoft.com/documentation/articles/machine-learning-what-is-machine-learning/
[Azure Machine Learning Studio]: https://studio.azureml.net/Home
[Azure portal]: https://portal.azure.com/

<!--MSDN references-->

<!--Other Web references-->

[Azure Machine Learning documentation]: http://azure.microsoft.com/documentation/services/machine-learning/
