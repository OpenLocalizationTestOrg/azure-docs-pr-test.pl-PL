---
title: "Samouczek Azure Analysis Services: lekcja 5 — tworzenie kolumn obliczeniowych | Microsoft Docs"
description: "Opisuje sposób tworzenia kolumn obliczeniowych w projekcie samouczka usług Azure Analysis Services."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 06/01/2017
ms.author: owend
ms.openlocfilehash: 893371145d77e156843271907aeef0c3756d0403
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="lesson-5-create-calculated-columns"></a><span data-ttu-id="eebe1-103">Lekcja 5. Tworzenie kolumn obliczeniowych</span><span class="sxs-lookup"><span data-stu-id="eebe1-103">Lesson 5: Create calculated columns</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="eebe1-104">W tej lekcji utworzysz dane w modelu przez dodanie kolumn obliczeniowych.</span><span class="sxs-lookup"><span data-stu-id="eebe1-104">In this lesson, you create data in your model by adding calculated columns.</span></span> <span data-ttu-id="eebe1-105">Możesz tworzyć kolumny obliczeniowe (jako kolumny niestandardowe) podczas korzystania z funkcji pobierania danych i edytora zapytań, lub też później, przy użyciu projektanta modeli zgodnie z opisem poniżej.</span><span class="sxs-lookup"><span data-stu-id="eebe1-105">You can create calculated columns (as custom columns) when using Get Data, by using the Query Editor, or later in the model designer like you do here.</span></span> <span data-ttu-id="eebe1-106">Aby dowiedzieć się więcej, zobacz temat [Kolumny obliczeniowe](https://docs.microsoft.com/sql/analysis-services/tabular-models/ssas-calculated-columns).</span><span class="sxs-lookup"><span data-stu-id="eebe1-106">To learn more, see [Calculated columns](https://docs.microsoft.com/sql/analysis-services/tabular-models/ssas-calculated-columns).</span></span>
  
<span data-ttu-id="eebe1-107">Zostanie utworzonych pięć nowych kolumn obliczeniowych w trzech różnych tabelach.</span><span class="sxs-lookup"><span data-stu-id="eebe1-107">You create five new calculated columns in three different tables.</span></span> <span data-ttu-id="eebe1-108">Czynności w poszczególnych zadaniach nieco się różnią, pokazując rożne sposoby tworzenia kolumn, zmieniania ich nazw oraz umieszczania ich w różnych miejscach tabeli.</span><span class="sxs-lookup"><span data-stu-id="eebe1-108">The steps are slightly different for each task showing there are several ways to create columns, rename them, and place them in various locations in a table.</span></span>  

<span data-ttu-id="eebe1-109">W tej lekcji po raz pierwszy zostanie użyty język DAX (Data Analysis Expresions).</span><span class="sxs-lookup"><span data-stu-id="eebe1-109">This lesson is also where you first use Data Analysis Expressions (DAX).</span></span> <span data-ttu-id="eebe1-110">DAX to specjalny język przeznaczony do tworzenia wyrażeń formuł dla modeli tabelarycznych, które można w wysokim stopniu dostosowywać.</span><span class="sxs-lookup"><span data-stu-id="eebe1-110">DAX is a special language for creating highly customizable formula expressions for tabular models.</span></span> <span data-ttu-id="eebe1-111">W tym samouczku język DAX zostanie użyty do tworzenia kolumn obliczeniowych, miar i filtrów ról.</span><span class="sxs-lookup"><span data-stu-id="eebe1-111">In this tutorial, you use DAX to create calculated columns, measures, and role filters.</span></span> <span data-ttu-id="eebe1-112">Aby dowiedzieć się więcej, zobacz temat [Język DAX w modelach tabelarycznych](https://docs.microsoft.com/sql/analysis-services/tabular-models/understanding-dax-in-tabular-models-ssas-tabular).</span><span class="sxs-lookup"><span data-stu-id="eebe1-112">To learn more, see [DAX in tabular models](https://docs.microsoft.com/sql/analysis-services/tabular-models/understanding-dax-in-tabular-models-ssas-tabular).</span></span> 
  
<span data-ttu-id="eebe1-113">Szacowany czas trwania lekcji: **15 minut**</span><span class="sxs-lookup"><span data-stu-id="eebe1-113">Estimated time to complete this lesson: **15 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="eebe1-114">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="eebe1-114">Prerequisites</span></span>  
<span data-ttu-id="eebe1-115">Ten temat stanowi część samouczka modelowania tabelarycznego, który należy wykonać w podanej kolejności.</span><span class="sxs-lookup"><span data-stu-id="eebe1-115">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="eebe1-116">Przed przystąpieniem do wykonywania zadań w tej lekcji należy ukończyć lekcję poprzednią: [Lekcja 4. Tworzenie relacji](../tutorials/aas-lesson-4-create-relationships.md).</span><span class="sxs-lookup"><span data-stu-id="eebe1-116">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 4: Create relationships](../tutorials/aas-lesson-4-create-relationships.md).</span></span> 
  
## <a name="create-calculated-columns"></a><span data-ttu-id="eebe1-117">Tworzenie kolumn obliczeniowych</span><span class="sxs-lookup"><span data-stu-id="eebe1-117">Create calculated columns</span></span>  
  
#### <a name="create-a-monthcalendar-calculated-column-in-the-dimdate-table"></a><span data-ttu-id="eebe1-118">Tworzenie kolumny obliczeniowej MonthCalendar w tabeli DimDate</span><span class="sxs-lookup"><span data-stu-id="eebe1-118">Create a MonthCalendar calculated column in the DimDate table</span></span>  
  
1.  <span data-ttu-id="eebe1-119">W menu **Model** kliknij pozycje **Widok modelu** > **Widok danych**.</span><span class="sxs-lookup"><span data-stu-id="eebe1-119">Click the **Model** menu > **Model View** > **Data View**.</span></span>  
  
    <span data-ttu-id="eebe1-120">Kolumny obliczeniowe można tworzyć przy użyciu projektanta modeli tylko w widoku danych.</span><span class="sxs-lookup"><span data-stu-id="eebe1-120">Calculated columns can only be created by using the model designer in Data View.</span></span>  
  
2.  <span data-ttu-id="eebe1-121">W projektancie modeli kliknij tabelę **DimDate** (karta).</span><span class="sxs-lookup"><span data-stu-id="eebe1-121">In the model designer, click the **DimDate** table (tab).</span></span>  
  
3.  <span data-ttu-id="eebe1-122">Kliknij prawym przyciskiem myszy nagłówek kolumny **CalendarQuarter**, a następnie kliknij pozycję **Wstaw kolumnę**.</span><span class="sxs-lookup"><span data-stu-id="eebe1-122">Right-click the **CalendarQuarter** column header, and then click **Insert Column**.</span></span>  
  
    <span data-ttu-id="eebe1-123">Nowa kolumna o nazwie **Kolumna obliczeniowa 1** zostanie wstawiona po lewej stronie kolumny **Kwartał kalendarzowy**.</span><span class="sxs-lookup"><span data-stu-id="eebe1-123">A new column named **Calculated Column 1** is inserted to the left of the **Calendar Quarter** column.</span></span>  
  
4.  <span data-ttu-id="eebe1-124">Na pasku formuły powyżej tabeli wpisz następującą formułę języka DAX: funkcja Autouzupełnianie ułatwia wpisywanie w pełni kwalifikowanych nazw kolumn i tabel oraz podaje listę dostępnych funkcji.</span><span class="sxs-lookup"><span data-stu-id="eebe1-124">In the formula bar above the table, type the following DAX formula: AutoComplete helps you type the fully qualified names of columns and tables, and lists the functions that are available.</span></span>  
  
    ```  
    =RIGHT(" " & FORMAT([MonthNumberOfYear],"#0"), 2) & " - " & [EnglishMonthName]  
    ``` 
  
    <span data-ttu-id="eebe1-125">Wszystkie wiersze w kolumnie obliczeniowej zostaną wypełnione wartościami.</span><span class="sxs-lookup"><span data-stu-id="eebe1-125">Values are then populated for all the rows in the calculated column.</span></span> <span data-ttu-id="eebe1-126">Po przewinięciu w dół tabeli widać, że wiersze tej kolumny mogą mieć różne wartości, w zależności od danych zawartych w poszczególnych wierszach.</span><span class="sxs-lookup"><span data-stu-id="eebe1-126">If you scroll down through the table, you see rows can have different values for this column, based on the data in each row.</span></span>    
  
5.  <span data-ttu-id="eebe1-127">Zmień nazwę tej kolumny na **MonthCalendar**.</span><span class="sxs-lookup"><span data-stu-id="eebe1-127">Rename this column to **MonthCalendar**.</span></span> 

    ![aas-lesson5-newcolumn](../tutorials/media/aas-lesson5-newcolumn.png) 
  
<span data-ttu-id="eebe1-129">Kolumna obliczeniowa MonthCalendar zawiera nazwę miesiąca możliwą do sortowania.</span><span class="sxs-lookup"><span data-stu-id="eebe1-129">The MonthCalendar calculated column provides a sortable name for Month.</span></span>  
  
#### <a name="create-a-dayofweek-calculated-column-in-the-dimdate-table"></a><span data-ttu-id="eebe1-130">Tworzenie kolumny obliczeniowej DayOfWeek w tabeli DimDate</span><span class="sxs-lookup"><span data-stu-id="eebe1-130">Create a DayOfWeek calculated column in the DimDate table</span></span>  
  
1.  <span data-ttu-id="eebe1-131">W nadal aktywnej tabeli **DimDate** kliknij menu **Kolumna**, a następnie kliknij pozycję **Dodaj kolumnę**.</span><span class="sxs-lookup"><span data-stu-id="eebe1-131">With the **DimDate** table still active, click the **Column** menu, and then click **Add Column**.</span></span>  
  
2.  <span data-ttu-id="eebe1-132">Na pasku formuły wpisz następującą formułę:</span><span class="sxs-lookup"><span data-stu-id="eebe1-132">In the formula bar, type the following formula:</span></span>  
    
    ```
    =RIGHT(" " & FORMAT([DayNumberOfWeek],"#0"), 2) & " - " & [EnglishDayNameOfWeek]  
    ```
    
    <span data-ttu-id="eebe1-133">Po zakończeniu tworzenia formuły naciśnij klawisz ENTER.</span><span class="sxs-lookup"><span data-stu-id="eebe1-133">When you've finished building the formula, press ENTER.</span></span> <span data-ttu-id="eebe1-134">Nowa kolumna zostanie dodana po prawej stronie tabeli.</span><span class="sxs-lookup"><span data-stu-id="eebe1-134">The new column is added to the far right of the table.</span></span>  
  
3.  <span data-ttu-id="eebe1-135">Zmień nazwę kolumny na **DayOfWeek**.</span><span class="sxs-lookup"><span data-stu-id="eebe1-135">Rename the column to **DayOfWeek**.</span></span>  
  
4.  <span data-ttu-id="eebe1-136">Kliknij nagłówek kolumny, a następnie przeciągnij kolumnę pomiędzy kolumny **EnglishDayNameOfWeek** i **DayNumberOfMonth**.</span><span class="sxs-lookup"><span data-stu-id="eebe1-136">Click the column heading, and then drag the column between the **EnglishDayNameOfWeek** column and the **DayNumberOfMonth** column.</span></span>  
  
    > [!TIP]  
    > <span data-ttu-id="eebe1-137">Przeniesienie kolumn w tabeli ułatwia nawigację.</span><span class="sxs-lookup"><span data-stu-id="eebe1-137">Moving columns in your table makes it easier to navigate.</span></span>  
  
<span data-ttu-id="eebe1-138">Kolumna obliczeniowa DayOfWeek zawiera nazwę dnia tygodnia możliwą do sortowania.</span><span class="sxs-lookup"><span data-stu-id="eebe1-138">The DayOfWeek calculated column provides a sortable name for the day of week.</span></span>  
  
#### <a name="create-a-productsubcategoryname-calculated-column-in-the-dimproduct-table"></a><span data-ttu-id="eebe1-139">Tworzenie kolumny obliczeniowej ProductSubcategoryName w tabeli DimProduct</span><span class="sxs-lookup"><span data-stu-id="eebe1-139">Create a ProductSubcategoryName calculated column in the DimProduct table</span></span>  
  
  
1.  <span data-ttu-id="eebe1-140">Przewiń tabelę **DimProduct** do prawej strony.</span><span class="sxs-lookup"><span data-stu-id="eebe1-140">In the **DimProduct** table, scroll to the far right of the table.</span></span> <span data-ttu-id="eebe1-141">Zwróć uwagę, że ostatnia kolumna po prawej stronie nosi nazwę **Dodaj kolumnę** (kursywą). Kliknij nagłówek tej kolumny.</span><span class="sxs-lookup"><span data-stu-id="eebe1-141">Notice the right-most column is named **Add Column** (italicized), click the column heading.</span></span>  
  
2.  <span data-ttu-id="eebe1-142">Na pasku formuły wpisz następującą formułę:</span><span class="sxs-lookup"><span data-stu-id="eebe1-142">In the formula bar, type the following formula:</span></span>  
    
    ```
    =RELATED('DimProductSubcategory'[EnglishProductSubcategoryName])  
    ```
  
3.  <span data-ttu-id="eebe1-143">Zmień nazwę kolumny na **ProductSubcategoryName**.</span><span class="sxs-lookup"><span data-stu-id="eebe1-143">Rename the column to **ProductSubcategoryName**.</span></span>  
  
<span data-ttu-id="eebe1-144">Kolumna obliczeniowa ProductSubcategoryName służy do tworzenia hierarchii w tabeli DimProduct, która obejmuje dane z kolumny EnglishProductSubcategoryName w tabeli DimProductSubcategory.</span><span class="sxs-lookup"><span data-stu-id="eebe1-144">The ProductSubcategoryName calculated column is used to create a hierarchy in the DimProduct table, which includes data from the EnglishProductSubcategoryName column in the DimProductSubcategory table.</span></span> <span data-ttu-id="eebe1-145">Hierarchie mogą obejmować maksymalnie jedną tabelę.</span><span class="sxs-lookup"><span data-stu-id="eebe1-145">Hierarchies cannot span more than one table.</span></span> <span data-ttu-id="eebe1-146">Hierarchie zostaną utworzone później, w lekcji 9.</span><span class="sxs-lookup"><span data-stu-id="eebe1-146">You create hierarchies later in Lesson 9.</span></span>  
  
#### <a name="create-a-productcategoryname-calculated-column-in-the-dimproduct-table"></a><span data-ttu-id="eebe1-147">Tworzenie kolumny obliczeniowej ProductCategoryName w tabeli DimProduct</span><span class="sxs-lookup"><span data-stu-id="eebe1-147">Create a ProductCategoryName calculated column in the DimProduct table</span></span>  
  
1.  <span data-ttu-id="eebe1-148">W nadal aktywnej tabeli **DimProduct** kliknij menu **Kolumna**, a następnie kliknij pozycję **Dodaj kolumnę**.</span><span class="sxs-lookup"><span data-stu-id="eebe1-148">With the **DimProduct** table still active, click the **Column** menu, and then click **Add Column**.</span></span>  
  
2.  <span data-ttu-id="eebe1-149">Na pasku formuły wpisz następującą formułę:</span><span class="sxs-lookup"><span data-stu-id="eebe1-149">In the formula bar, type the following formula:</span></span>  
  
    ```
    =RELATED('DimProductCategory'[EnglishProductCategoryName]) 
    ```
    
3.  <span data-ttu-id="eebe1-150">Zmień nazwę kolumny na **ProductCategoryName**.</span><span class="sxs-lookup"><span data-stu-id="eebe1-150">Rename the column to **ProductCategoryName**.</span></span>  
  
<span data-ttu-id="eebe1-151">Kolumna obliczeniowa ProductCategoryName służy do tworzenia hierarchii w tabeli DimProduct, która obejmuje dane z kolumny EnglishProductCategoryName w tabeli DimProductCategory.</span><span class="sxs-lookup"><span data-stu-id="eebe1-151">The ProductCategoryName calculated column is used to create a hierarchy in the DimProduct table, which includes data from the EnglishProductCategoryName column in the DimProductCategory table.</span></span> <span data-ttu-id="eebe1-152">Hierarchie mogą obejmować maksymalnie jedną tabelę.</span><span class="sxs-lookup"><span data-stu-id="eebe1-152">Hierarchies cannot span more than one table.</span></span>  
  
#### <a name="create-a-margin-calculated-column-in-the-factinternetsales-table"></a><span data-ttu-id="eebe1-153">Tworzenie kolumny obliczeniowej Margin w tabeli FactInternetSales</span><span class="sxs-lookup"><span data-stu-id="eebe1-153">Create a Margin calculated column in the FactInternetSales table</span></span>  
  
1.  <span data-ttu-id="eebe1-154">W projektancie modeli wybierz tabelę **FactInternetSales**.</span><span class="sxs-lookup"><span data-stu-id="eebe1-154">In the model designer, select the **FactInternetSales** table.</span></span>  
  
2.  <span data-ttu-id="eebe1-155">Utwórz nową kolumnę obliczeniową między kolumnami **SalesAmount** i **TaxAmt**.</span><span class="sxs-lookup"><span data-stu-id="eebe1-155">Create a new calculated column between the **SalesAmount** column and the **TaxAmt** column.</span></span>  
  
3.  <span data-ttu-id="eebe1-156">Na pasku formuły wpisz następującą formułę:</span><span class="sxs-lookup"><span data-stu-id="eebe1-156">In the formula bar, type the following formula:</span></span>  
  
    ```
    =[SalesAmount]-[TotalProductCost]
    ``` 

4.  <span data-ttu-id="eebe1-157">Zmień nazwę kolumny na **Margin** (Marż).</span><span class="sxs-lookup"><span data-stu-id="eebe1-157">Rename the column to **Margin**.</span></span>  
 
      ![aas-lesson5-newmargin](../tutorials/media/aas-lesson5-newmargin.png)
      
    <span data-ttu-id="eebe1-159">Kolumna obliczeniowa Margin jest używana do analizowania marży poszczególnych transakcji sprzedaży.</span><span class="sxs-lookup"><span data-stu-id="eebe1-159">The Margin calculated column is used to analyze profit margins for each sale.</span></span>  
  
## <a name="whats-next"></a><span data-ttu-id="eebe1-160">Co dalej?</span><span class="sxs-lookup"><span data-stu-id="eebe1-160">What's next?</span></span>
<span data-ttu-id="eebe1-161">[Lekcja 6. Tworzenie miar](../tutorials/aas-lesson-6-create-measures.md).</span><span class="sxs-lookup"><span data-stu-id="eebe1-161">[Lesson 6: Create measures](../tutorials/aas-lesson-6-create-measures.md).</span></span>
  
  
  
