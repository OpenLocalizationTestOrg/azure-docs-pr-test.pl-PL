---
title: aaa "lekcji samouczka usług Azure Analysis Services 5: Tworzenie kolumn obliczeniowych | Opis elementu Microsoft Docs": w tym artykule opisano, jak toocreate obliczane kolumny w projekcie samouczek hello Azure Analysis Services. usługi: documentationcenter usług analysis services: "Autor: minewiskan Menedżera: Edytor erikre:" tagów: "

MS.AssetID: ms.service: ms.devlang usług analysis services: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: ms.author 2017-06/01: owend
---
# <a name="lesson-5-create-calculated-columns"></a>Lekcja 5. Tworzenie kolumn obliczeniowych

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

W tej lekcji utworzysz dane w modelu przez dodanie kolumn obliczeniowych. Można utworzyć kolumny obliczeniowej (jako kolumny niestandardowe) podczas korzystania z pobieranie danych, za pomocą hello edytora zapytań, lub później w notacji projektanta hello modelu można to zrobić na stronie. toolearn więcej, zobacz [kolumn obliczeniowych](https://docs.microsoft.com/sql/analysis-services/tabular-models/ssas-calculated-columns).
  
Zostanie utworzonych pięć nowych kolumn obliczeniowych w trzech różnych tabelach. kroki Hello są nieco inne dla każdego zadania istnieje kilka sposobów toocreate kolumn, zmień ich oraz umieścić je w różnych miejscach w tabeli.  

W tej lekcji po raz pierwszy zostanie użyty język DAX (Data Analysis Expresions). DAX to specjalny język przeznaczony do tworzenia wyrażeń formuł dla modeli tabelarycznych, które można w wysokim stopniu dostosowywać. W tym samouczku użyjesz kolumny obliczane toocreate, miary i roli filtry języka DAX. toolearn więcej, zobacz [DAX w modelach tabelarycznym](https://docs.microsoft.com/sql/analysis-services/tabular-models/understanding-dax-in-tabular-models-ssas-tabular). 
  
Szacowany czas toocomplete tej lekcji: **15 minut**  
  
## <a name="prerequisites"></a>Wymagania wstępne  
Ten temat stanowi część samouczka modelowania tabelarycznego, który należy wykonać w podanej kolejności. Przed wykonaniem zadania hello w tej lekcji, powinno mieć ukończone poprzedniej lekcji hello: [lekcji 4: tworzenie relacji](../tutorials/aas-lesson-4-create-relationships.md). 
  
## <a name="create-calculated-columns"></a>Tworzenie kolumn obliczeniowych  
  
#### <a name="create-a-monthcalendar-calculated-column-in-hello-dimdate-table"></a>Utwórz pole obliczeniowe MonthCalendar w tabeli DimDate hello  
  
1.  Kliknij przycisk hello **modelu** menu > **widok modelu** > **widoku danych**.  
  
    Kolumn obliczanych można tworzyć tylko za pomocą projektanta modelu hello w widoku danych.  
  
2.  W Konstruktorze modelu powitania kliknij hello **DimDate** tabeli (karta).  
  
3.  Kliknij prawym przyciskiem myszy hello **CalendarQuarter** nagłówek kolumny, a następnie kliknij przycisk **Wstaw kolumnę**.  
  
    Nową kolumnę o nazwie **kolumna obliczana 1** jest toohello wstawiony po lewej hello **kwartału** kolumny.  
  
4.  Na pasku formuły hello powyżej hello tabeli, wpisz hello następującej formuły języka DAX: pomaga autouzupełniania wpisania hello w pełni kwalifikowane nazwy kolumn i tabel i list hello funkcje, które są dostępne.  
  
    ```  
    =RIGHT(" " & FORMAT([MonthNumberOfYear],"#0"), 2) & " - " & [EnglishMonthName]  
    ``` 
  
    Dla wszystkich wierszy hello w kolumnie obliczeniowej hello jest następnie zapełniana wartościami. Jeśli przewijania w dół hello tabeli, zobacz wiersze mogą mieć różne wartości dla tej kolumny, na podstawie danych hello w każdym wierszu.    
  
5.  Zmień nazwę tej kolumny zbyt**MonthCalendar**. 

    ![aas-lesson5-newcolumn](../tutorials/media/aas-lesson5-newcolumn.png) 
  
kolumna obliczeniowa MonthCalendar Hello zawiera nazwę sortowania dla miesiąca.  
  
#### <a name="create-a-dayofweek-calculated-column-in-hello-dimdate-table"></a>Utwórz pole obliczeniowe DayOfWeek w tabeli DimDate hello  
  
1.  Z hello **DimDate** tabeli nadal aktywne, kliknij przycisk hello **kolumny** menu, a następnie kliknij przycisk **Dodaj kolumnę**.  
  
2.  Na pasku formuły hello wpisz hello następującej formuły:  
    
    ```
    =RIGHT(" " & FORMAT([DayNumberOfWeek],"#0"), 2) & " - " & [EnglishDayNameOfWeek]  
    ```
    
    Po zakończeniu tworzenia hello formuły, naciśnij klawisz ENTER. Kolumna Hello zostanie dodana toohello prawej tabeli hello.  
  
3.  Zmień nazwę kolumny hello zbyt**DayOfWeek**.  
  
4.  Kliknij nagłówek kolumny hello, a następnie przeciągnij kolumny hello między hello **EnglishDayNameOfWeek** kolumny i hello **DayNumberOfMonth** kolumny.  
  
    > [!TIP]  
    > Przenoszenie kolumn w tabeli umożliwia łatwiejsze toonavigate.  
  
kolumna obliczeniowa DayOfWeek Hello poda nazwę sortowania hello dzień tygodnia.  
  
#### <a name="create-a-productsubcategoryname-calculated-column-in-hello-dimproduct-table"></a>Utwórz pole obliczeniowe ProductSubcategoryName w tabeli DimProduct hello  
  
  
1.  W hello **DimProduct** tabeli, przewiń toohello prawej krawędzi tabeli hello. Powiadomienie hello prawej kolumna nosiła nazwę **Dodaj kolumnę** (kursywą), kliknij nagłówek kolumny hello.  
  
2.  Na pasku formuły hello wpisz hello następującej formuły:  
    
    ```
    =RELATED('DimProductSubcategory'[EnglishProductSubcategoryName])  
    ```
  
3.  Zmień nazwę kolumny hello zbyt**ProductSubcategoryName**.  
  
kolumny obliczeniowej ProductSubcategoryName Hello jest używany toocreate hierarchii w tabeli DimProduct hello, która zawiera dane z hello EnglishProductSubcategoryName kolumny w tabeli DimProductSubcategory hello. Hierarchie mogą obejmować maksymalnie jedną tabelę. Hierarchie zostaną utworzone później, w lekcji 9.  
  
#### <a name="create-a-productcategoryname-calculated-column-in-hello-dimproduct-table"></a>Utwórz pole obliczeniowe ProductCategoryName w tabeli DimProduct hello  
  
1.  Z hello **DimProduct** tabeli nadal aktywne, kliknij przycisk hello **kolumny** menu, a następnie kliknij przycisk **Dodaj kolumnę**.  
  
2.  Na pasku formuły hello wpisz hello następującej formuły:  
  
    ```
    =RELATED('DimProductCategory'[EnglishProductCategoryName]) 
    ```
    
3.  Zmień nazwę kolumny hello zbyt**ProductCategoryName**.  
  
kolumny obliczeniowej ProductCategoryName Hello jest używany toocreate hierarchii w tabeli DimProduct hello, która zawiera dane z hello EnglishProductCategoryName kolumny w tabeli DimProductCategory hello. Hierarchie mogą obejmować maksymalnie jedną tabelę.  
  
#### <a name="create-a-margin-calculated-column-in-hello-factinternetsales-table"></a>Utwórz pole obliczeniowe margines w Tabela FactInternetSales hello  
  
1.  Projektant modelu hello, wybierz hello **FactInternetSales** tabeli.  
  
2.  Utwórz nową kolumnę obliczeniową między hello **kwoty sprzedaży** kolumny i hello **TaxAmt** kolumny.  
  
3.  Na pasku formuły hello wpisz hello następującej formuły:  
  
    ```
    =[SalesAmount]-[TotalProductCost]
    ``` 

4.  Zmień nazwę kolumny hello zbyt**margines**.  
 
      ![aas-lesson5-newmargin](../tutorials/media/aas-lesson5-newmargin.png)
      
    kolumny obliczeniowej margines Hello jest używany tooanalyze marży dla każdej sprzedaży.  
  
## <a name="whats-next"></a>Co dalej?
[Lekcja 6. Tworzenie miar](../tutorials/aas-lesson-6-create-measures.md).
  
  
  
