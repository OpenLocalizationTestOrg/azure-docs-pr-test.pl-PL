---
title: "Samouczek Azure Analysis Services: lekcja uzupełniająca — niewyrównane hierarchie | Microsoft Docs"
description: "Opisuje sposób naprawiania niewyrównanych hierarchii w samouczku usług Azure Analysis Services."
services: analysis-services
documentationcenter: 
author: Minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 05/26/2017
ms.author: owend
ms.openlocfilehash: d34b2123153406640cf03bc9f57efa557af4cfaa
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/11/2017
---
# <a name="supplemental-lesson---ragged-hierarchies"></a>Lekcja uzupełniająca — niewyrównane hierarchie

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

W tej lekcji uzupełniającej przedstawione zostanie rozwiązanie często występującego problemu polegającego na tworzeniu tabeli przestawnej dla hierarchii zawierających puste wartości (elementy członkowskie) na różnych poziomach. Przykładem może być organizacja, w której menedżer wysokiego szczebla jako bezpośrednich podwładnych ma menedżerów działów oraz osoby niebędące menedżerami. Innym przykładem mogą być hierarchie geograficzne składające się z kraju, regionu i miasta, gdzie niektóre miasta nie mają nadrzędnego kraju lub regionu, jak Waszyngton czy Watykan. Hierarchie o pustych elementach członkowskich często osiągają różne, niewyrównane poziomy.

![aas-lesson-detail-ragged-hierarchies-table](../tutorials/media/aas-lesson-detail-ragged-hierarchies-table.png)

Modele tabelaryczne o poziomie zgodności 1400 zapewniają dodatkową właściwość hierarchii o nazwie **Ukryj elementy członkowskie**. Ustawienie **Domyślne** zakłada, że na żadnym poziomie nie występują puste elementy członkowskie. Ustawienie **Ukryj puste elementy członkowskie** wyklucza puste elementy członkowskie z hierarchii w przypadku ich dodania do tabeli przestawnej lub raportu.  
  
Szacowany czas trwania lekcji: **20 minut**  
  
## <a name="prerequisites"></a>Wymagania wstępne  
Ta lekcja uzupełniająca stanowi część samouczka modelowania tabelarycznego. Przed wykonaniem zadań w tej lekcji uzupełniającej należy ukończyć wszystkie poprzednie lekcje lub wykonać przykładowy projekt modelu Adventure Works Internet Sales. 

Jeśli projekt AW Internet Sales został utworzony w ramach tego samouczka, model nie zawiera jeszcze żadnych danych ani hierarchii niewyrównanych. W celu ukończenia tej lekcji uzupełniającej należy najpierw utworzyć problem, dodając pewne dodatkowe tabele oraz tworząc relacje, kolumny obliczeniowe, miarę i nową hierarchię organizacji. Zajmie to ok. 15 minut. Następnie można rozwiązać problem w ciągu kilku minut.  

## <a name="add-tables-and-objects"></a>Dodawanie tabel i obiektów
  
### <a name="to-add-new-tables-to-your-model"></a>Dodawanie nowych tabel do modelu
  
1.  W Eksploratorze modeli tabelarycznych rozwiń pozycję **Źródła danych**, a następnie prawym przyciskiem myszy kliknij połączenie i kliknij pozycję **Importuj nowe tabele**.
  
2.  W oknie Nawigator wybierz tabele **DimEmployee** oraz **FactResellerSales**, a następnie kliknij przycisk **OK**.

3.  W edytorze zapytań kliknij opcję **Importuj**

4.  Utwórz następującą [relację](../tutorials/aas-lesson-4-create-relationships.md):

    | Tabela 1           | Kolumna       | Kierunek filtru   | Tabela 2     | Kolumna      | Aktywne |
    |-------------------|--------------|--------------------|-------------|-------------|--------|
    | FactResellerSales | OrderDateKey | Domyślne            | DimDate     | Date        | Tak    |
    | FactResellerSales | DueDate      | Domyślne            | DimDate     | Date        | Nie     |
    | FactResellerSales | ShipDateKey  | Domyślne            | DimDate     | Date        | Nie     |
    | FactResellerSales | ProductKey   | Domyślne            | DimProduct  | ProductKey  | Tak    |
    | FactResellerSales | EmployeeKey  | Do obu tabel | DimEmployee | EmployeeKey | Tak    |

5. W tabeli **DimEmployee** utwórz następujące [kolumny obliczeniowe](../tutorials/aas-lesson-5-create-calculated-columns.md): 

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

6.  W tabeli **DimEmployee** utwórz [hierarchię](../tutorials/aas-lesson-9-create-hierarchies.md) o nazwie **Organization** (Organizacja). Dodaj następujące kolumny w podanej kolejności: **Level1**, **Level2**, **Level3**, **Level4**, **Level5**.

7.  W tabeli **FactResellerSales** utwórz następującą [miarę](../tutorials/aas-lesson-6-create-measures.md):

    ```
    ResellerTotalSales:=SUM([SalesAmount])
    ```

8.  Użyj funkcji [Analiza w programie Excel](../tutorials/aas-lesson-12-analyze-in-excel.md), aby otworzyć program Excel i automatycznie utworzyć tabelę przestawną.

9.  W obszarze **Pola tabeli przestawnej** dodaj hierarchię **Organization** z tabeli **DimEmployee** do pola **Wiersze** i miarę **ResellerTotalSales** z tabeli **FactResellerSales** do pola **Wartości**.

    ![aas-lesson-detail-ragged-hierarchies-pivottable](../tutorials/media/aas-lesson-detail-ragged-hierarchies-pivottable.png)

    Jak widać w tabeli przestawnej, w hierarchii wyświetlane są wiersze niewyrównane. Istnieje wiele wierszy, w których są widoczne puste elementy członkowskie.

## <a name="to-fix-the-ragged-hierarchy-by-setting-the-hide-members-property"></a>Rozwiązywanie niewyrównanej hierarchii przez ustawienie właściwości Ukryj elementy członkowskie

1.  W **Eksploratorze modeli tabelarycznych** rozwiń węzeł **Tabele** > **DimEmployee** > **Hierarchie** > **Organization**.

2.  W obszarze **Właściwości** > **Ukryj elementy członkowskie** wybierz pozycję **Ukryj puste elementy członkowskie**. 

    ![aas-lesson-detail-ragged-hierarchies-hidemembers](../tutorials/media/aas-lesson-detail-ragged-hierarchies-hidemembers.png)

3.  Po powrocie do programu Excel odśwież tabelę przestawną. 

    ![aas-lesson-detail-ragged-hierarchies-pivottable-refresh](../tutorials/media/aas-lesson-detail-ragged-hierarchies-pivottable-refresh.png)

    Teraz tabela wygląda o wiele lepiej.

## <a name="see-also"></a>Zobacz też   
[Lekcja 9. Tworzenie hierarchii](../tutorials/aas-lesson-9-create-hierarchies.md)  
[Lekcja uzupełniająca — zabezpieczenia dynamiczne](../tutorials/aas-supplemental-lesson-dynamic-security.md)  
[Lekcja uzupełniająca — wiersze szczegółów](../tutorials/aas-supplemental-lesson-detail-rows.md)  