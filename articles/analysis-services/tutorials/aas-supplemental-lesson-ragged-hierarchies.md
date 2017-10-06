---
title: aaa "samouczek lekcji dodatkowych usług Azure Analysis Services: niewyrównanych hierarchie | Opis elementu Microsoft Docs": w tym artykule opisano, jak toofix niewyrównanych hierarchie hello samouczka usług Azure Analysis Services.
usługi: documentationcenter usług analysis services: "Autor: minewiskan Menedżera: Edytor erikre:" tagów: "

MS.AssetID: ms.service: ms.devlang usług analysis services: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend
---
# <a name="supplemental-lesson---ragged-hierarchies"></a>Lekcja uzupełniająca — niewyrównane hierarchie

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

W tej lekcji uzupełniającej przedstawione zostanie rozwiązanie często występującego problemu polegającego na tworzeniu tabeli przestawnej dla hierarchii zawierających puste wartości (elementy członkowskie) na różnych poziomach. Przykładem może być organizacja, w której menedżer wysokiego szczebla jako bezpośrednich podwładnych ma menedżerów działów oraz osoby niebędące menedżerami. Innym przykładem mogą być hierarchie geograficzne składające się z kraju, regionu i miasta, gdzie niektóre miasta nie mają nadrzędnego kraju lub regionu, jak Waszyngton czy Watykan. Gdy w hierarchii jest puste elementy członkowskie, jego często descends toodifferent lub niewyrównanych poziomów.

![aas-lesson-detail-ragged-hierarchies-table](../tutorials/media/aas-lesson-detail-ragged-hierarchies-table.png)

Modeli tabelarycznych przy poziomie zgodności hello 1400 ma dodatkowe **Ukryj elementy członkowskie** właściwości dla hierarchii. Witaj **domyślne** ustawienia obowiązuje założenie, nie ma żadnych członków puste na dowolnym poziomie. Witaj **Ukryj puste elementy członkowskie** wyklucza puste elementy członkowskie z hierarchii powitania po dodaniu tooa tabeli przestawnej lub raportu.  
  
Szacowany czas toocomplete tej lekcji: **20 minut**  
  
## <a name="prerequisites"></a>Wymagania wstępne  
Ta lekcja uzupełniająca stanowi część samouczka modelowania tabelarycznego. Przed wykonaniem zadania hello w tym uzupełniające lekcji, powinno mieć ukończone wszystkie poprzednie — lekcje lub zakończonych projektu modelu przykładowej firmy Adventure Works Internet sprzedaży. 

Jeśli po utworzeniu projektu sprzedaży Internet AW hello jako części samouczka hello model nie zawiera jeszcze żadnych danych lub hierarchiami niewyrównane. toocomplete tej lekcji uzupełniające, konieczne jest przeprowadzenie najpierw toocreate hello problem, dodając niektóre dodatkowe tabele, Utwórz relacje, kolumn obliczeniowych, miary i nowej hierarchii organizacji. Zajmie to ok. 15 minut. Następnie należy pobrać toosolve w ciągu kilku minut.  

## <a name="add-tables-and-objects"></a>Dodawanie tabel i obiektów
  
### <a name="tooadd-new-tables-tooyour-model"></a>nowy model tooyour tabele tooadd
  
1.  W Eksploratorze modeli tabelarycznych rozwiń pozycję **Źródła danych**, a następnie prawym przyciskiem myszy kliknij połączenie i kliknij pozycję **Importuj nowe tabele**.
  
2.  W oknie Nawigator wybierz tabele **DimEmployee** oraz **FactResellerSales**, a następnie kliknij przycisk **OK**.

3.  W edytorze zapytań kliknij opcję **Importuj**

4.  Utwórz następujące hello [relacje](../tutorials/aas-lesson-4-create-relationships.md):

    | Tabela 1           | Kolumna       | Kierunek filtru   | Tabela 2     | Kolumna      | Aktywne |
    |-------------------|--------------|--------------------|-------------|-------------|--------|
    | FactResellerSales | OrderDateKey | Domyślne            | DimDate     | Date        | Tak    |
    | FactResellerSales | DueDate      | Domyślne            | DimDate     | Date        | Nie     |
    | FactResellerSales | ShipDateKey  | Domyślne            | DimDate     | Date        | Nie     |
    | FactResellerSales | ProductKey   | Domyślne            | DimProduct  | ProductKey  | Tak    |
    | FactResellerSales | EmployeeKey  | Tabele tooBoth | DimEmployee | EmployeeKey | Tak    |

5. W hello **DimEmployee** tabeli, należy utworzyć następujące hello [kolumn obliczeniowych](../tutorials/aas-lesson-5-create-calculated-columns.md): 

    **Ścieżka** 
    ```
    =PATH([EmployeeKey],[ParentEmployeeKey])
    ```

    **FullName** 
    ```
    =[FirstName] & " " & [MiddleName] & " " & [LastName]
    ```

    **Level1** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,1)) 
    ```

    **Level2** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,2)) 
    ```

    **Level3** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,3)) 
    ```

    **Level4** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,4)) 
    ```

    **Level5** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,5)) 
    ```

6.  W hello **DimEmployee** tabeli, należy utworzyć [hierarchii](../tutorials/aas-lesson-9-create-hierarchies.md) o nazwie **organizacji**. Dodaj następujące kolumny w kolejności hello: **Level1**, **Level2**, **Level3**, **Level4**, **Level5**.

7.  W hello **FactResellerSales** tabeli, należy utworzyć następujące hello [miary](../tutorials/aas-lesson-6-create-measures.md):

    ```
    ResellerTotalSales:=SUM([SalesAmount])
    ```

8.  Użyj [analizy w programie Excel](../tutorials/aas-lesson-12-analyze-in-excel.md) tooopen programu Excel i automatycznie utworzyć tabelę przestawną.

9.  W **pól tabeli przestawnej**, Dodaj hello **organizacji** hierarchii z hello **DimEmployee** tabeli zbyt**wierszy**i hello **ResellerTotalSales** miarę z hello **FactResellerSales** tabeli zbyt**wartości**.

    ![aas-lesson-detail-ragged-hierarchies-pivottable](../tutorials/media/aas-lesson-detail-ragged-hierarchies-pivottable.png)

    Jak widać w tabeli przestawnej hello hierarchii hello wyświetla wiersze, które są niewyrównane. Istnieje wiele wierszy, w których są widoczne puste elementy członkowskie.

## <a name="toofix-hello-ragged-hierarchy-by-setting-hello-hide-members-property"></a>Witaj toofix niewyrównanych hierarchii poprzez ustawienie właściwości elementów członkowskich Ukryj hello

1.  W **Eksploratorze modeli tabelarycznych** rozwiń węzeł **Tabele** > **DimEmployee** > **Hierarchie** > **Organization**.

2.  W obszarze **Właściwości** > **Ukryj elementy członkowskie** wybierz pozycję **Ukryj puste elementy członkowskie**. 

    ![aas-lesson-detail-ragged-hierarchies-hidemembers](../tutorials/media/aas-lesson-detail-ragged-hierarchies-hidemembers.png)

3.  W programie Excel Odśwież hello tabeli przestawnej. 

    ![aas-lesson-detail-ragged-hierarchies-pivottable-refresh](../tutorials/media/aas-lesson-detail-ragged-hierarchies-pivottable-refresh.png)

    Teraz tabela wygląda o wiele lepiej.

## <a name="see-also"></a>Zobacz też   
[Lekcja 9. Tworzenie hierarchii](../tutorials/aas-lesson-9-create-hierarchies.md)  
[Lekcja uzupełniająca — zabezpieczenia dynamiczne](../tutorials/aas-supplemental-lesson-dynamic-security.md)  
[Lekcja uzupełniająca — wiersze szczegółów](../tutorials/aas-supplemental-lesson-detail-rows.md)  