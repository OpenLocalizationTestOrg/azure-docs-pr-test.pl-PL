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
# <a name="analyze-data-with-azure-machine-learning"></a>Analizowanie danych przy użyciu usługi Azure Machine Learning
> [!div class="op_single_selector"]
> * [Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [Azure Machine Learning](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [Program Visual Studio](sql-data-warehouse-query-visual-studio.md)
> * [sqlcmd](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [SSMS](sql-data-warehouse-query-ssms.md)
> 
> 

W tym samouczku używa usługi Azure Machine Learning toobuild predykcyjnej maszyny, uczenie modelu, w oparciu o dane przechowywane w magazynie danych SQL Azure. W szczególności to z kolei ukierunkowaną kampanię marketingową dla firmy Adventure Works, sklep roweru hello, przez Jeśli klient jest prawdopodobnie toobuy roweru lub nie.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Integrating-Azure-Machine-Learning-with-Azure-SQL-Data-Warehouse/player]
> 
> 

## <a name="prerequisites"></a>Wymagania wstępne
toostep opisanych w tym samouczku, potrzebne są:

* Baza danych usługi SQL Data Warehouse. ze wstępnie załadowanymi danymi z bazy danych AdventureWorksDW. tooprovision tego, zobacz [Tworzenie usługi SQL Data Warehouse] [ Create a SQL Data Warehouse] i wybierz polecenie tooload hello przykładowych danych. Jeśli masz już magazyn danych, ale bez przykładowych danych, możesz [ręcznie załadować przykładowe dane][load sample data manually].

## <a name="1-get-hello-data"></a>1. Pobierz dane hello
dane Hello jest hello widoku dbo.vTargetMail w bazie danych AdventureWorksDW hello. tooread te dane:

1. Zaloguj się do programu [Azure Machine Learning Studio][Azure Machine Learning studio] i kliknij eksperymenty.
2. Kliknij przycisk **+ NOWE** i wybierz pozycję **Blank Experiment** (Pusty eksperyment).
3. Wprowadź nazwę swojego eksperymentu: Targeted Marketing (Marketing docelowy).
4. Przeciągnij hello **czytnika** modułu na podstawie hello okienka modułów do kanwy hello.
5. Określ szczegóły hello bazy danych magazynu danych SQL w okienku Properties hello.
6. Określ bazę danych hello **zapytania** tooread hello dane.

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

Uruchom eksperyment hello, klikając **Uruchom** w obszarze hello kanwy eksperymentu.
![Uruchom eksperyment hello][1]

Po zakończeniu eksperymentu hello pomyślnie wykonywane kliknij port wyjściowy hello u dołu hello moduł czytnika hello i wybierz **wizualizacja** toosee hello zaimportowała dane.
![Wyświetlanie zaimportowanych danych][3]

## <a name="2-clean-hello-data"></a>2. Wyczyść hello danych
dane hello tooclean, usunąć niektóre kolumny, które nie są istotne dla modelu hello. toodo to:

1. Przeciągnij hello **kolumny projektu** modułu na kanwie hello.
2. Kliknij przycisk **Uruchom selektor kolumn** w okienku toospecify właściwości hello, które kolumny mają toodrop.
   ![Kolumny projektu][4]
3. Wyklucz dwie kolumny: CustomerAlternateKey i GeographyKey.
   ![Usuwanie zbędnych kolumn][5]

## <a name="3-build-hello-model"></a>3. Tworzenie modelu hello
Podzielimy dane hello proporcji 80 – 20: 80% tootrain modelu uczenia maszynowego i 20% tootest hello modelu. Firma Microsoft będzie wprowadzać użyj algorytmów "Dwuklasowych" hello, w przypadku tego problemu klasyfikacji binarnej.

1. Przeciągnij hello **podziału** modułu na kanwie hello.
2. Wprowadź wartość 0,8 w ułamek wierszy w hello pierwszy wyjściowy zestaw danych w okienku Properties hello.
   ![Podział danych na zestaw szkoleniowy i zestaw testowy][6]
3. Przeciągnij hello **Two-Class Boosted drzewa decyzyjnego** modułu na kanwie hello.
4. Przeciągnij hello **Train Model** modułu do hello obszaru roboczego i określ hello danych wejściowych. Następnie kliknij przycisk **Uruchom selektor kolumn** w okienku Properties hello.
   * Pierwsze dane wejściowe: algorytm uczenia maszynowego.
   * Drugie dane wejściowe: algorytm hello tootrain danych na.
     ![Łączenie modułu Train Model hello][7]
5. Wybierz hello **BikeBuyer** kolumny hello toopredict kolumny.
   ![Wybierz kolumny toopredict][8]

## <a name="4-score-hello-model"></a>4. Wynik hello modelu
Zostanie teraz przetestować sposób wykonywania hello modelu na danych testowych. Porównamy algorytm hello z toosee innego algorytmu, który działa lepiej.

1. Przeciągnij **Score Model** modułu na kanwie hello.
    Pierwsze dane wejściowe: Uczony model drugie dane wejściowe: dane testowe ![Score hello model][9]
2. Przeciągnij hello **maszyna punktu Bayesa Two-Class** do kanwy eksperymentu hello. Porównamy, jak ten algorytm wykonuje porównania toohello Two-Class Boosted drzewa decyzyjnego.
3. Kopiuj i Wklej hello moduły Train Model i Score Model hello kanwy.
4. Przeciągnij hello **Evaluate Model** modułu algorytmów hello kanwy toocompare hello dwa.
5. **Uruchom** hello eksperymentu.
   ![Uruchom eksperyment hello][10]
6. Kliknij port wyjściowy hello u dołu hello hello modułu Evaluate Model, a następnie kliknij pozycję Visualize.
   ![Wizualizacja wyników oceny][11]

podane metryki Hello są hello krzywą ROC, diagram precision-recall i podnieś krzywą. Na podstawie tych metryk, możemy stwierdzić, tym hello pierwszy model działa lepiej niż drugi hello. toolook na powitania co hello pierwszego modelu, kliknij port wyjściowy hello Score Model i kliknij pozycję Visualize.
![Wizualizacja wyników klasyfikacji][12]

Zobaczysz, że dwie kolumny dodane tooyour zestawu danych testowych.

* Scored Probabilities: hello prawdopodobieństwo, że klient jest nabywcą roweru.
* Scored etykiety: hello klasyfikacja dokonana przez hello model — nabywca roweru (1) czy nie (0). Próg prawdopodobieństwa etykietowania ustawiono too50% i można go dostosować.

Porównywanie kolumny hello BikeBuyer (rzeczywiste) z etykietami oceniane hello (Prognozowane), widać, jak wykonał hello modelu. W kolejnych krokach można użyć tego modelu toomake prognoz dotyczących nowych klientów i opublikować ten model jako usługę sieci web lub zapisać wyniki wstecz tooSQL hurtowni danych.

## <a name="next-steps"></a>Następne kroki
toolearn więcej informacji na temat tworzenia predykcyjnych modeli, uczenia maszynowego można znaleźć zbyt[tooMachine wprowadzenie Learning na platformie Azure][Introduction tooMachine Learning on Azure].

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
