---
title: aaa "lekcji samouczka usług Azure Analysis Services 10: tworzenie partycji | Opis elementu Microsoft Docs": w tym artykule opisano, jak toocreate partycje w projekcie samouczek hello Azure Analysis Services. usługi: documentationcenter usług analysis services: "Autor: minewiskan Menedżera: Edytor erikre:" tagów: "

MS.AssetID: ms.service: ms.devlang usług analysis services: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend
---
# <a name="lesson-10-create-partitions"></a>Lekcja 10. Tworzenie partycji

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

W tej lekcji zostanie utworzona tabela FactInternetSales hello toodivide partycji na mniejsze części logiczne, które mogą być przetworzone (odświeżyć) niezależnie od innych partycji. Domyślnie w każdej tabeli, który można dołączyć do modelu ma jedną partycję, która obejmuje wszystkie tabeli hello kolumn i wierszy. Dla Tabela FactInternetSales hello chcemy toodivide hello danych przez rok; jedna partycja dla każdego z pięciu lat. hello tabeli. Każda partycja będzie mogła być przetwarzana niezależnie. toolearn więcej, zobacz [partycji](https://docs.microsoft.com/sql/analysis-services/tabular-models/partitions-ssas-tabular). 
  
Szacowany czas toocomplete tej lekcji: **15 minut**  
  
## <a name="prerequisites"></a>Wymagania wstępne  
Ten temat stanowi część samouczka modelowania tabelarycznego, który należy wykonać w podanej kolejności. Przed wykonaniem zadania hello w tej lekcji, powinno mieć ukończone poprzedniej lekcji hello: [lekcji 9: tworzenia hierarchii](../tutorials/aas-lesson-9-create-hierarchies.md).  
  
## <a name="create-partitions"></a>Tworzenie partycji  
  
#### <a name="toocreate-partitions-in-hello-factinternetsales-table"></a>partycje toocreate w Tabela FactInternetSales hello  
  
1.  W Eksploratorze modeli tabelarycznych rozwiń węzeł **Tabele**, a następnie kliknij prawym przyciskiem myszy pozycje **FactInternetSales** > **Partycje**.  
  
2.  W Menedżerze partycji kliknij **kopiowania**, a następnie zmień nazwę hello zbyt**FactInternetSales2010**.
  
    Ponieważ tooinclude partycji hello tylko tych wierszy, które w określonym czasie, dla roku hello 2010, należy zmodyfikować hello wyrażenia zapytania.
  
4.  Kliknij przycisk **projekt** tooopen edytora zapytań, a następnie kliknij przycisk hello **FactInternetSales2010** zapytania.

5.  W wersji zapoznawczej, kliknij przycisk hello strzałkę w hello **OrderDate** nagłówek kolumny, a następnie kliknij przycisk **filtry daty/godziny** > **między**.

    ![aas-lesson10-query-editor](../tutorials/media/aas-lesson10-query-editor.png)

6.  Okno dialogowe Filtr wierszy hello w **Pokaż wiersze, w których: OrderDate**, pozostaw **wypada po lub w dniu**, a następnie w polu Data hello, wprowadź **2010-1-1**. Pozostaw hello **i** operator zaznaczone, następnie wybierz **przed**, następnie w polu Data hello, wprowadź **2011-1-1**, a następnie kliknij przycisk **OK**.

    ![aas-lesson10-filter-rows](../tutorials/media/aas-lesson10-filter-rows.png)
    
    Zwróć uwagę, że w części ZASTOSOWANE KROKI w Edytorze zapytań widać kolejny krok o nazwie Przefiltrowano wiersze. Ten filtr jest tylko dat zamówienia tooselect z 2010.

8.  Kliknij przycisk **Importuj**.

    W Menedżerze partycji zauważyć zapytań hello teraz wyrażenie ma dodatkowe klauzuli filtrowane wierszy.

    ![aas-lesson10-query](../tutorials/media/aas-lesson10-query.png)
  
    Ta partycja powinna zawierać tylko dane hello w tych wierszach, w którym hello OrderDate trwa hello 2010 roku kalendarzowym, jak określono w klauzuli filtrowane wiersze hello określa tej instrukcji.  
  
  
#### <a name="toocreate-a-partition-for-hello-2011-year"></a>toocreate partycji dla hello 2011 roku  
  
1.  Powitania kliknij na liście partycji hello **FactInternetSales2010** partycji utworzony, a następnie kliknij przycisk **kopiowania**.  Zmień nazwę partycji hello zbyt**FactInternetSales2011**. 

    Nie trzeba toouse toocreate edytora zapytań nową klauzulę filtrowane wiersze. Ponieważ utworzono kopię zapytania hello 2010 toodo wystarczy wprowadzić zmianę nieznaczne w zapytaniu hello 2011 dla.
  
2.  W **wyrażenia zapytania**, w kolejności dla tej partycji tooinclude tylko te wiersze hello 2011 roku, Zastąp hello lat w klauzuli filtrowane wiersze hello z **2011** i **2012**, takich jak:  
  
    ```  
    let
        Source = #"SQL/localhost;AdventureWorksDW2014",
        dbo_FactInternetSales = Source{[Schema="dbo",Item="FactInternetSales"]}[Data],
        #"Removed Columns" = Table.RemoveColumns(dbo_FactInternetSales,{"OrderDateKey", "DueDateKey", "ShipDateKey"}),
        #"Filtered Rows" = Table.SelectRows(#"Removed Columns", each [OrderDate] >= #datetime(2011, 1, 1, 0, 0, 0) and [OrderDate] < #datetime(2012, 1, 1, 0, 0, 0))
    in
        #"Filtered Rows"
   
    ```  
  
#### <a name="toocreate-partitions-for-2012-2013-and-2014"></a>partycje toocreate 2012, 2013 i 2014 r.  
  
- Wykonaj hello poprzednie kroki, tworzenie partycji 2012, 2013 i 2014 r., zmiana hello lat hello filtrowane wierszy klauzuli tooinclude tylko wiersze w roku. 
  

## <a name="delete-hello-factinternetsales-partition"></a>Usuń hello FactInternetSales partycji
Teraz, gdy masz partycji dla każdego roku, można usunąć partycji FactInternetSales hello; w przypadku wybrania przetwórz wszystkie podczas przetwarzania partycji, co uniemożliwia nakładają się na siebie.

#### <a name="toodelete-hello-factinternetsales-partition"></a>Witaj toodelete FactInternetSales partycji
-  Kliknij hello FactInternetSales partycji, a następnie kliknij przycisk **usunąć**.



## <a name="process-partitions"></a>Przetwarzanie partycji  
W Menedżerze partycji zauważyć hello **ostatniego przetwarzania** kolumny dla wszystkich nowych partycji hello utworzone przedstawiono te partycje nigdy nie zostaną przetworzone. Podczas tworzenia partycji, należy uruchomić partycje procesu lub proces tabeli operacji toorefresh hello danych w tych partycji.  
  
#### <a name="tooprocess-hello-factinternetsales-partitions"></a>tooprocess hello FactInternetSales partycji  
  
1.  Kliknij przycisk **OK** tooclose Menedżera partycji.  
  
2.  Kliknij przycisk hello **FactInternetSales** tabeli, a następnie kliknij przycisk hello **modelu** menu > **procesu** > **partycje procesu**.  
  
3.  Okno dialogowe partycje procesu hello, sprawdź **tryb** ustawiono zbyt**domyślny proces**.  
  
4.  Zaznacz pole wyboru hello w hello **procesu** kolumny dla każdego hello pięciu partycje utworzony, a następnie kliknij przycisk **OK**.  

    ![aas-lesson10-process-partitions](../tutorials/media/aas-lesson10-process-partitions.png)
  
    Jeśli zostanie wyświetlony monit o poświadczenia personifikacji, wprowadź nazwę użytkownika systemu Windows hello i hasło określone Lekcja 2.  
  
    Witaj **przetwarzania danych** okno dialogowe zostanie wyświetlone i wyświetla szczegóły procesu dla każdej partycji. Zwróć uwagę, że dla każdej partycji przenoszona jest inna liczba wierszy. Każda partycja zawiera tylko tych wierszy, dla roku hello określony w klauzuli WHERE w instrukcji SQL hello hello. Po zakończeniu przetwarzania Przejdź dalej i zamknąć okno dialogowe hello przetwarzania danych.  
  
    ![aas-lesson10-process-complete](../tutorials/media/aas-lesson10-process-complete.png)
  
 ## <a name="whats-next"></a>Co dalej?
Toohello Przejdź dalej lekcji: [lekcji 11: tworzenie ról](../tutorials/aas-lesson-11-create-roles.md). 
