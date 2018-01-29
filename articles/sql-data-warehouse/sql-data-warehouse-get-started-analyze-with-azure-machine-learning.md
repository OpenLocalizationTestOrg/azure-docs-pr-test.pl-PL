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
ms.sourcegitcommit: 68aec76e471d677fd9a6333dc60ed098d1072cfc
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/18/2017
---
# <a name="analyze-data-with-azure-machine-learning"></a>Analizowanie danych przy użyciu usługi Azure Machine Learning
> [!div class="op_single_selector"]
> * [Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [Azure Machine Learning](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [Program Visual Studio](sql-data-warehouse-query-visual-studio.md)
> * [sqlcmd](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [SSMS](sql-data-warehouse-query-ssms.md)
> 
> 

Ten samouczek przedstawia sposób tworzenia predykcyjnego modelu uczenia maszynowego przy użyciu usługi Azure Machine Learning korzystającej z danych przechowywanych w usłudze Azure SQL Data Warehouse. W szczególności ten samouczek omawia tworzenie ukierunkowanej kampanii marketingowej dla sklepu rowerowego Adventure Works przez prognozowanie prawdopodobieństwa zakupu roweru przez klienta.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Integrating-Azure-Machine-Learning-with-Azure-SQL-Data-Warehouse/player]
> 
> 

## <a name="prerequisites"></a>Wymagania wstępne
Do wykonania kroków opisanych w tym samouczku potrzebne są:

* Baza danych usługi SQL Data Warehouse. ze wstępnie załadowanymi danymi z bazy danych AdventureWorksDW. Aby dowiedzieć się, jak załadować dane przykładowe, zobacz [Tworzenie magazynu danych SQL Data Warehouse][Create a SQL Data Warehouse]. Jeśli masz już magazyn danych, ale bez przykładowych danych, możesz [ręcznie załadować przykładowe dane][load sample data manually].

## <a name="1-get-the-data"></a>1. Pobieranie danych
Dane znajdują się w widoku dbo.vTargetMail w bazie danych AdventureWorksDW. Aby odczytać te dane:

1. Zaloguj się do programu [Azure Machine Learning Studio][Azure Machine Learning studio] i kliknij eksperymenty.
2. Kliknij przycisk **+ NOWE** i wybierz pozycję **Blank Experiment** (Pusty eksperyment).
3. Wprowadź nazwę swojego eksperymentu: Targeted Marketing (Marketing docelowy).
4. Przeciągnij moduł **Reader** (Czytnik) z okienka modułów do kanwy.
5. Określ szczegóły bazy danych usługi SQL Data Warehouse w okienku Properties (Właściwości).
6. Określ **zapytanie** do bazy danych, aby odczytać potrzebne dane.

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

Aby uruchomić eksperyment, kliknij pozycję **Run** (Uruchom) na kanwie eksperymentu.
![Uruchamianie eksperymentu][1]

Po pomyślnym wykonaniu eksperymentu kliknij port wyjściowy na dole modułu Reader (Czytnik) i wybierz opcję **Visualize** (Wizualizacja), aby wyświetlić zaimportowane danych.
![Wyświetlanie zaimportowanych danych][3]

## <a name="2-clean-the-data"></a>2. Czyszczenie danych
Aby wyczyścić dane, usuń kilka kolumn, które nie są istotne dla modelu. W tym celu:

1. Przeciągnij moduł **Project Columns** (Kolumny projektu) na kanwę.
2. Kliknij pozycję **Launch column selector** (Uruchom selektor kolumn) w okienku Properties (Właściwości), aby wskazać kolumny do usunięcia.
   ![Kolumny projektu][4]
3. Wyklucz dwie kolumny: CustomerAlternateKey i GeographyKey.
   ![Usuwanie zbędnych kolumn][5]

## <a name="3-build-the-model"></a>3. Tworzenie modelu
Podzielimy dane w proporcji 80–20: 80% do trenowania tworzenia modelu uczenia maszynowego i 20% do testowania modelu. Użyjemy algorytmów „dwuklasowych” do rozwiązania tego problemu klasyfikacji binarnej.

1. Przeciągnij moduł **Split** (Podział) na kanwę.
2. Wprowadź wartość 0,8 w polu Fraction of rows in the first output dataset (Ułamek wierszy w pierwszym zestawie danych wyjściowych) w okienku Properties (Właściwości).
   ![Podział danych na zestaw szkoleniowy i zestaw testowy][6]
3. Przeciągnij moduł **Two-Class Boosted Decision Tree** (Dwuklasowe wzmocnione drzewo decyzyjne) na kanwę.
4. Przeciągnij moduł **Train Model** (Model szkoleniowy) na kanwę i określ dane wejściowe. Następnie kliknij przycisk **Launch column selector** (Uruchom selektor kolumn) w okienku Properties (Właściwości).
   * Pierwsze dane wejściowe: algorytm uczenia maszynowego.
   * Drugie dane wejściowe: dane do szkolenia w zakresie algorytmu.
     ![Łączenie modułu Train Model (Model szkoleniowy)][7]
5. Wybierz kolumnę **BikeBuyer** (Nabywca roweru) jako kolumnę do prognozowania.
   ![Wybór kolumny do prognozowania][8]

## <a name="4-score-the-model"></a>4. Ocena modelu
Teraz przetestujemy działanie modelu na danych testowych. Porównamy wybrany algorytm z innym algorytmem, aby zobaczyć, który działa lepiej.

1. Przeciągnij moduł **Score model** (Model klasyfikacyjny) na kanwę.
    Pierwsze dane wejściowe: model szkoleniowy Drugie dane wejściowe: dane testowe ![Klasyfikacja modelu][9]
2. Przeciągnij moduł **Two-Class Bayes Point Machine** (Dwuklasowa maszyna punktu Bayesa) do kanwy eksperymentu. Porównamy działanie tego algorytmu z algorytmem Two-Class Boosted Decision Tree (Dwuklasowe wzmocnione drzewo decyzyjne).
3. Skopiuj i wklej moduły Train Model (Model szkoleniowy) i Score Model (Model klasyfikacyjny) do kanwy.
4. Przeciągnij moduł **Evaluate Model** (Ocena modelu) do kanwy, aby porównać oba algorytmy.
5. Kliknij przycisk **Run** (Uruchom), aby uruchomić eksperyment
   ![Uruchamianie eksperymentu][10]
6. Kliknij port wyjściowy w dolnej części modułu Evaluate Model (Ocena modelu), a następnie kliknij pozycję Visualize (Wizualizacja).
   ![Wizualizacja wyników oceny][11]

Podane metryki obejmują krzywą ROC, diagram precision-recall oraz krzywą wzrostu. Na podstawie tych metryk możemy stwierdzić, że pierwszy model działa lepiej niż drugi. Aby przyjrzeć się prognozom pierwszego modelu, kliknij port wyjściowy modułu Score Model (Model klasyfikacyjny) i kliknij pozycję Visualize (Wizualizacja).
![Wizualizacja wyników klasyfikacji][12]

Zostaną wyświetlone dwie kolumny dodane do zestawu danych testowych.

* Scored Probabilities (Sklasyfikowane prawdopodobieństwo): prawdopodobieństwo, że klient jest nabywcą roweru.
* Scored Labels (Sklasyfikowane etykiety): klasyfikacja dokonana przez model — nabywca roweru (1) lub nie (0). Ustawiony próg prawdopodobieństwa etykietowania wynosi 50% i można go dostosować.

Porównując wartości w kolumnach BikeBuyer (Nabywca roweru) (rzeczywiste) oraz Scored Labels (Sklasyfikowane etykiety) (prognozowane), można określić prawidłowość działania modelu. W kolejnych krokach można użyć tego modelu w celu tworzenia prognoz dotyczących nowych klientów i opublikować ten model jako usługę sieci Web lub zapisać wyniki z powrotem w bazie danych usługi SQL Data Warehouse.

## <a name="next-steps"></a>Następne kroki
Aby dowiedzieć się więcej o tworzeniu predykcyjnych modeli uczenia maszynowego, zapoznaj się z artykułem [Wprowadzenie do usługi Machine Learning na platformie Azure][Introduction to Machine Learning on Azure].

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
