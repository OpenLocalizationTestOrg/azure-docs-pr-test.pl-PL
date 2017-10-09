---
title: aaa "lekcji samouczka usług Azure Analysis Services 6: tworzenie miar | Opis elementu Microsoft Docs": w tym artykule opisano, jak toocreate środki w projekcie samouczek hello Azure Analysis Services. usługi: documentationcenter usług analysis services: "Autor: minewiskan Menedżera: Edytor erikre:" tagów: "

MS.AssetID: ms.service: ms.devlang usług analysis services: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: ms.author 2017-06/01: owend
---
# <a name="lesson-6-create-measures"></a>Lekcja 6. Tworzenie miar

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

W tej lekcji możesz utworzyć toobe miar zawarte w modelu. Podobne toohello obliczane kolumny, które utworzono, miary jest obliczenie utworzony przy użyciu formuły języka DAX. Jednak w odróżnieniu od kolumn obliczeniowych miary są szacowane na podstawie *filtru* wybranego przez użytkownika. Na przykład określonej kolumny lub fragmentatora dodane toohello pole etykiety wierszy w tabeli przestawnej. Wartość każdej komórki w filtrze hello następnie jest obliczana na podstawie miary hello zastosowane. Środki są wydajne i elastyczne obliczeń, które mają tooinclude prawie wszystkie modele tabelaryczne tooperform dynamiczne obliczeń na dane liczbowe. toolearn więcej, zobacz [środki](https://docs.microsoft.com/sql/analysis-services/tabular-models/measures-ssas-tabular).
  
środki toocreate używasz hello *siatce miar*. Każda tabela domyślnie zawiera pustą siatkę miar. Zwykle jednak nie tworzy się miar dla każdej tabeli. Siatka miary Hello pojawia się poniżej tabeli w Projektancie modeli hello w widoku danych. toohide lub wyświetla hello miary siatki dla tabeli, kliknij przycisk hello **tabeli** menu, a następnie kliknij przycisk **Pokaż siatkę miary**.  
  
Klikając pustej komórki w siatce miar hello, a następnie wpisując formuły języka DAX na pasku formuły hello można utworzyć miary. Gdy kliknij wprowadź formułę hello toocomplete, miary hello następnie pojawi się w komórce hello. Można również utworzyć środki przy użyciu standardowych agregacji, klikając kolumnę, a następnie klikając hello przycisku Autosumowanie (**∑**) na powitania narzędzi. Środki utworzone za pomocą funkcji Autosumowania hello są wyświetlane w komórce siatki miary hello bezpośrednio pod hello kolumny, ale mogą zostać przeniesione.  
  
W tej lekcji utworzysz środki wprowadzając zarówno formuły języka DAX na pasku formuły hello i za pomocą funkcji Autosumowania hello.  
  
Szacowany czas toocomplete tej lekcji: **30 minut**  
  
## <a name="prerequisites"></a>Wymagania wstępne  
Ten temat stanowi część samouczka modelowania tabelarycznego, który należy wykonać w podanej kolejności. Przed wykonaniem zadania hello w tej lekcji, powinno mieć ukończone poprzedniej lekcji hello: [lekcji 5: Tworzenie kolumn obliczeniowych](../tutorials/aas-lesson-5-create-calculated-columns.md).  
  
## <a name="create-measures"></a>Tworzenie miar  
  
#### <a name="toocreate-a-dayscurrentquartertodate-measure-in-hello-dimdate-table"></a>toocreate DaysCurrentQuarterToDate miary w tabeli DimDate hello  
  
1.  W Konstruktorze modelu powitania kliknij hello **DimDate** tabeli.  
  
2.  W siatce miar hello kliknij przycisk hello lewego górnego pustej komórki.  
  
3.  Na pasku formuły hello wpisz hello następującej formuły:  
  
    ```
    DaysCurrentQuarterToDate:=COUNTROWS( DATESQTD( 'DimDate'[Date])) 
    ```
  
    Powiadomienie hello lewego górnego komórki zawiera teraz nazwę miary **DaysCurrentQuarterToDate**, a następnie wynik hello **92**.
    
      ![aas-lesson6-newmeasure](../tutorials/media/aas-lesson6-newmeasure.png) 
    
    W odróżnieniu od kolumny obliczeniowej z formułami miary możesz wpisać hello Nazwa miary, wprowadź dwukropek, następuje hello wyrażenia formuły.

  
#### <a name="toocreate-a-daysincurrentquarter-measure-in-hello-dimdate-table"></a>toocreate DaysInCurrentQuarter miary w tabeli DimDate hello  
  
1.  Z hello **DimDate** tabeli nadal aktywne w Konstruktorze modelu hello w siatce miar hello, kliknij przycisk hello pustej komórki poniżej miary hello został utworzony.  
  
2.  Na pasku formuły hello wpisz hello następującej formuły:  
  
    ```
    DaysInCurrentQuarter:=COUNTROWS( DATESBETWEEN( 'DimDate'[Date], STARTOFQUARTER( LASTDATE('DimDate'[Date])), ENDOFQUARTER('DimDate'[Date])))
    ```
  
    Podczas tworzenia porównania proporcje jednego okresu niekompletne hello poprzedniego okresu. Formuła Hello należy obliczyć hello część hello okresu, który upłynął i porównania go toohello sam udział procentowy w hello poprzedniego okresu. W tym przypadku [DaysCurrentQuarterToDate] / [DaysInCurrentQuarter] zapewnia hello udział, który upłynął w hello bieżącego okresu.  
  
#### <a name="toocreate-an-internetdistinctcountsalesorder-measure-in-hello-factinternetsales-table"></a>toocreate środek InternetDistinctCountSalesOrder w Tabela FactInternetSales hello  
  
1.  Kliknij przycisk hello **FactInternetSales** tabeli.   
  
2.  Kliknij przycisk hello **SalesOrderNumber** nagłówek kolumny.  
  
3.  Na pasku narzędzi hello, kliknij przycisk Dalej toohello Strzałka w dół hello Autosumowanie (**∑**) przycisk, a następnie wybierz **DistinctCount**.  
  
    funkcja Autosumowania Hello automatycznie tworzy miary dla wybranej kolumny hello przy użyciu formuły standardowe agregacji DistinctCount hello.  
    
       ![aas-lesson6-newmeasure2](../tutorials/media/aas-lesson6-newmeasure2.png)
  
4.  W siatce miar hello, kliknij przycisk hello nowej miary, a następnie w hello **właściwości** okna w **Nazwa miary**, zmiany nazwy miary hello zbyt**InternetDistinctCountSalesOrder**. 
 
  
#### <a name="toocreate-additional-measures-in-hello-factinternetsales-table"></a>dodatkowe środki toocreate w Tabela FactInternetSales hello  
  
1.  Za pomocą funkcji Autosumowania hello, Utwórz i nazwa hello następujące miary:  

    |Kolumna|Nazwa miary|Autosumowanie (∑)|Formuła|  
    |----------------|----------|-----------------|-----------|  
    |SalesOrderLineNumber|InternetOrderLinesCount|Licznik|=COUNTA([SalesOrderLineNumber])|  
    |OrderQuantity|InternetTotalUnits|Suma|=SUM([OrderQuantity])|  
    |DiscountAmount|InternetTotalDiscountAmount|Suma|=SUM([DiscountAmount])|  
    |TotalProductCost|InternetTotalProductCost|Suma|=SUM([TotalProductCost])|  
    |SalesAmount|InternetTotalSales|Suma|=SUM([SalesAmount])|  
    |Margin|InternetTotalMargin|Suma|=SUM([Margin])|  
    |TaxAmt|InternetTotalTaxAmt|Suma|=SUM([TaxAmt])|  
    |Freight|InternetTotalFreight|Suma|=SUM([Freight])|  
  
2.  Klikając przycisk Utwórz pustej komórki w siatce miar hello i za pomocą hello pasku formuły, i nazwę hello następujące środki w kolejności:  
  
      ```
      InternetPreviousQuarterMargin:=CALCULATE([InternetTotalMargin],PREVIOUSQUARTER('DimDate'[Date]))
      ```
      
      ```
      InternetCurrentQuarterMargin:=TOTALQTD([InternetTotalMargin],'DimDate'[Date])
      ```
  
      ```
      InternetPreviousQuarterMarginProportionToQTD:=[InternetPreviousQuarterMargin]*([DaysCurrentQuarterToDate]/[DaysInCurrentQuarter])
      ```
  
      ```
      InternetPreviousQuarterSales:=CALCULATE([InternetTotalSales],PREVIOUSQUARTER('DimDate'[Date]))
      ```
  
      ```
      InternetCurrentQuarterSales:=TOTALQTD([InternetTotalSales],'DimDate'[Date])
      ```
      
      ```
      InternetPreviousQuarterSalesProportionToQTD:=[InternetPreviousQuarterSales]*([DaysCurrentQuarterToDate]/[DaysInCurrentQuarter])
      ```
  
Środki utworzone dla Tabela FactInternetSales hello mogą być używane tooanalyze krytyczne dane finansowe takie jak sprzedaż, kosztów i marża dla elementów zdefiniowanych przez wybrany filtr użytkownika hello.  
  
## <a name="whats-next"></a>Co dalej?
[Lekcja 7. Tworzenie kluczowych wskaźników wydajności](../tutorials/aas-lesson-7-create-key-performance-indicators.md).  

  
