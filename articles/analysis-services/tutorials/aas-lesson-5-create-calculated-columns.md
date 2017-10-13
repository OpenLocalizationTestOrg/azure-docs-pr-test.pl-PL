---
title: "Samouczek Azure Analysis Services: lekcja 5 — tworzenie kolumn obliczeniowych | Microsoft Docs"
description: "Opisuje sposób tworzenia kolumn obliczeniowych w projekcie samouczka usług Azure Analysis Services."
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
ms.date: 09/20/2017
ms.author: owend
ms.openlocfilehash: eab74fbadc6a143ca5a2bc57a1762539a6d489c1
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/11/2017
---
# <a name="lesson-5-create-calculated-columns"></a>Lekcja 5. Tworzenie kolumn obliczeniowych

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

W tej lekcji utworzysz dane w modelu przez dodanie kolumn obliczeniowych. Możesz tworzyć kolumny obliczeniowe (jako kolumny niestandardowe) podczas korzystania z funkcji pobierania danych i edytora zapytań, lub też później, przy użyciu projektanta modeli zgodnie z opisem poniżej. Aby dowiedzieć się więcej, zobacz temat [Kolumny obliczeniowe](https://docs.microsoft.com/sql/analysis-services/tabular-models/ssas-calculated-columns).
  
Zostanie utworzonych pięć nowych kolumn obliczeniowych w trzech różnych tabelach. Czynności w poszczególnych zadaniach nieco się różnią, pokazując rożne sposoby tworzenia kolumn, zmieniania ich nazw oraz umieszczania ich w różnych miejscach tabeli.  

W tej lekcji po raz pierwszy zostanie użyty język DAX (Data Analysis Expresions). DAX to specjalny język przeznaczony do tworzenia wyrażeń formuł dla modeli tabelarycznych, które można w wysokim stopniu dostosowywać. W tym samouczku język DAX zostanie użyty do tworzenia kolumn obliczeniowych, miar i filtrów ról. Aby dowiedzieć się więcej, zobacz temat [Język DAX w modelach tabelarycznych](https://docs.microsoft.com/sql/analysis-services/tabular-models/understanding-dax-in-tabular-models-ssas-tabular). 
  
Szacowany czas trwania lekcji: **15 minut**  
  
## <a name="prerequisites"></a>Wymagania wstępne  
Ten temat stanowi część samouczka modelowania tabelarycznego, który należy wykonać w podanej kolejności. Przed przystąpieniem do wykonywania zadań w tej lekcji należy ukończyć lekcję poprzednią: [Lekcja 4. Tworzenie relacji](../tutorials/aas-lesson-4-create-relationships.md). 
  
## <a name="create-calculated-columns"></a>Tworzenie kolumn obliczeniowych  
  
#### <a name="create-a-monthcalendar-calculated-column-in-the-dimdate-table"></a>Tworzenie kolumny obliczeniowej MonthCalendar w tabeli DimDate  
  
1.  W menu **Model** kliknij pozycje **Widok modelu** > **Widok danych**.  
  
    Kolumny obliczeniowe można tworzyć przy użyciu projektanta modeli tylko w widoku danych.  
  
2.  W projektancie modeli kliknij tabelę **DimDate** (karta).  
  
3.  Kliknij prawym przyciskiem myszy nagłówek kolumny **CalendarQuarter**, a następnie kliknij pozycję **Wstaw kolumnę**.  
  
    Nowa kolumna o nazwie **Kolumna obliczeniowa 1** zostanie wstawiona po lewej stronie kolumny **Kwartał kalendarzowy**.  
  
4.  Na pasku formuły powyżej tabeli wpisz następującą formułę języka DAX: funkcja Autouzupełnianie ułatwia wpisywanie w pełni kwalifikowanych nazw kolumn i tabel oraz podaje listę dostępnych funkcji.  
  
    ```  
    =RIGHT(" " & FORMAT([MonthNumberOfYear],"#0"), 2) & " - " & [EnglishMonthName]  
    ``` 
  
    Wszystkie wiersze w kolumnie obliczeniowej zostaną wypełnione wartościami. Po przewinięciu w dół tabeli widać, że wiersze tej kolumny mogą mieć różne wartości, w zależności od danych zawartych w poszczególnych wierszach.    
  
5.  Zmień nazwę tej kolumny na **MonthCalendar**. 

    ![aas-lesson5-newcolumn](../tutorials/media/aas-lesson5-newcolumn.png) 
  
Kolumna obliczeniowa MonthCalendar zawiera nazwę miesiąca możliwą do sortowania.  
  
#### <a name="create-a-dayofweek-calculated-column-in-the-dimdate-table"></a>Tworzenie kolumny obliczeniowej DayOfWeek w tabeli DimDate  
  
1.  W nadal aktywnej tabeli **DimDate** kliknij menu **Kolumna**, a następnie kliknij pozycję **Dodaj kolumnę**.  
  
2.  Na pasku formuły wpisz następującą formułę:  
    
    ```
    =RIGHT(" " & FORMAT([DayNumberOfWeek],"#0"), 2) & " - " & [EnglishDayNameOfWeek]  
    ```
    
    Po zakończeniu tworzenia formuły naciśnij klawisz ENTER. Nowa kolumna zostanie dodana po prawej stronie tabeli.  
  
3.  Zmień nazwę kolumny na **DayOfWeek**.  
  
4.  Kliknij nagłówek kolumny, a następnie przeciągnij kolumnę pomiędzy kolumny **EnglishDayNameOfWeek** i **DayNumberOfMonth**.  
  
    > [!TIP]  
    > Przeniesienie kolumn w tabeli ułatwia nawigację.  
  
Kolumna obliczeniowa DayOfWeek zawiera nazwę dnia tygodnia możliwą do sortowania.  
  
#### <a name="create-a-productsubcategoryname-calculated-column-in-the-dimproduct-table"></a>Tworzenie kolumny obliczeniowej ProductSubcategoryName w tabeli DimProduct  
  
  
1.  Przewiń tabelę **DimProduct** do prawej strony. Zwróć uwagę, że ostatnia kolumna po prawej stronie nosi nazwę **Dodaj kolumnę** (kursywą). Kliknij nagłówek tej kolumny.  
  
2.  Na pasku formuły wpisz następującą formułę:  
    
    ```
    =RELATED('DimProductSubcategory'[EnglishProductSubcategoryName])  
    ```
  
3.  Zmień nazwę kolumny na **ProductSubcategoryName**.  
  
Kolumna obliczeniowa ProductSubcategoryName służy do tworzenia hierarchii w tabeli DimProduct, która obejmuje dane z kolumny EnglishProductSubcategoryName w tabeli DimProductSubcategory. Hierarchie mogą obejmować maksymalnie jedną tabelę. Hierarchie zostaną utworzone później, w lekcji 9.  
  
#### <a name="create-a-productcategoryname-calculated-column-in-the-dimproduct-table"></a>Tworzenie kolumny obliczeniowej ProductCategoryName w tabeli DimProduct  
  
1.  W nadal aktywnej tabeli **DimProduct** kliknij menu **Kolumna**, a następnie kliknij pozycję **Dodaj kolumnę**.  
  
2.  Na pasku formuły wpisz następującą formułę:  
  
    ```
    =RELATED('DimProductCategory'[EnglishProductCategoryName]) 
    ```
    
3.  Zmień nazwę kolumny na **ProductCategoryName**.  
  
Kolumna obliczeniowa ProductCategoryName służy do tworzenia hierarchii w tabeli DimProduct, która obejmuje dane z kolumny EnglishProductCategoryName w tabeli DimProductCategory. Hierarchie mogą obejmować maksymalnie jedną tabelę.  
  
#### <a name="create-a-margin-calculated-column-in-the-factinternetsales-table"></a>Tworzenie kolumny obliczeniowej Margin w tabeli FactInternetSales  
  
1.  W projektancie modeli wybierz tabelę **FactInternetSales**.  
  
2.  Utwórz nową kolumnę obliczeniową między kolumnami **SalesAmount** i **TaxAmt**.  
  
3.  Na pasku formuły wpisz następującą formułę:  
  
    ```
    =[SalesAmount]-[TotalProductCost]
    ``` 

4.  Zmień nazwę kolumny na **Margin** (Marż).  
 
      ![aas-lesson5-newmargin](../tutorials/media/aas-lesson5-newmargin.png)
      
    Kolumna obliczeniowa Margin jest używana do analizowania marży poszczególnych transakcji sprzedaży.  
  
## <a name="whats-next"></a>Co dalej?
[Lekcja 6. Tworzenie miar](../tutorials/aas-lesson-6-create-measures.md).
  
  
  
