---
title: "Samouczek Azure Analysis Services: lekcja uzupełniająca — niewyrównane hierarchie | Microsoft Docs"
description: "Opisuje sposób naprawiania niewyrównanych hierarchii w samouczku usług Azure Analysis Services."
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
ms.date: 05/26/2017
ms.author: owend
ms.openlocfilehash: 0f02ff73eb126cc397312e87bde50b3ee2d6ce53
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="supplemental-lesson---ragged-hierarchies"></a><span data-ttu-id="456bf-103">Lekcja uzupełniająca — niewyrównane hierarchie</span><span class="sxs-lookup"><span data-stu-id="456bf-103">Supplemental lesson - Ragged hierarchies</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="456bf-104">W tej lekcji uzupełniającej przedstawione zostanie rozwiązanie często występującego problemu polegającego na tworzeniu tabeli przestawnej dla hierarchii zawierających puste wartości (elementy członkowskie) na różnych poziomach.</span><span class="sxs-lookup"><span data-stu-id="456bf-104">In this supplemental lesson, you resolve a common problem when pivoting on hierarchies that contain blank values (members) at different levels.</span></span> <span data-ttu-id="456bf-105">Przykładem może być organizacja, w której menedżer wysokiego szczebla jako bezpośrednich podwładnych ma menedżerów działów oraz osoby niebędące menedżerami.</span><span class="sxs-lookup"><span data-stu-id="456bf-105">For example, an organization where a high-level manager has both departmental managers and non-managers as direct reports.</span></span> <span data-ttu-id="456bf-106">Innym przykładem mogą być hierarchie geograficzne składające się z kraju, regionu i miasta, gdzie niektóre miasta nie mają nadrzędnego kraju lub regionu, jak Waszyngton czy Watykan.</span><span class="sxs-lookup"><span data-stu-id="456bf-106">Or, geographic hierarchies composed of Country-Region-City, where some cities lack a parent State or Province, such as Washington D.C., Vatican City.</span></span> <span data-ttu-id="456bf-107">Hierarchie o pustych elementach członkowskich często osiągają różne, niewyrównane poziomy.</span><span class="sxs-lookup"><span data-stu-id="456bf-107">When a hierarchy has blank members, it often descends to different, or ragged, levels.</span></span>

![aas-lesson-detail-ragged-hierarchies-table](../tutorials/media/aas-lesson-detail-ragged-hierarchies-table.png)

<span data-ttu-id="456bf-109">Modele tabelaryczne o poziomie zgodności 1400 zapewniają dodatkową właściwość hierarchii o nazwie **Ukryj elementy członkowskie**.</span><span class="sxs-lookup"><span data-stu-id="456bf-109">Tabular models at the 1400 compatibility level have an additional **Hide Members** property for hierarchies.</span></span> <span data-ttu-id="456bf-110">Ustawienie **Domyślne** zakłada, że na żadnym poziomie nie występują puste elementy członkowskie.</span><span class="sxs-lookup"><span data-stu-id="456bf-110">The **Default** setting assumes there are no blank members at any level.</span></span> <span data-ttu-id="456bf-111">Ustawienie **Ukryj puste elementy członkowskie** wyklucza puste elementy członkowskie z hierarchii w przypadku ich dodania do tabeli przestawnej lub raportu.</span><span class="sxs-lookup"><span data-stu-id="456bf-111">The **Hide blank members** setting excludes blank members from the hierarchy when added to a PivotTable or report.</span></span>  
  
<span data-ttu-id="456bf-112">Szacowany czas trwania lekcji: **20 minut**</span><span class="sxs-lookup"><span data-stu-id="456bf-112">Estimated time to complete this lesson: **20 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="456bf-113">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="456bf-113">Prerequisites</span></span>  
<span data-ttu-id="456bf-114">Ta lekcja uzupełniająca stanowi część samouczka modelowania tabelarycznego.</span><span class="sxs-lookup"><span data-stu-id="456bf-114">This supplemental lesson topic is part of a tabular modeling tutorial.</span></span> <span data-ttu-id="456bf-115">Przed wykonaniem zadań w tej lekcji uzupełniającej należy ukończyć wszystkie poprzednie lekcje lub wykonać przykładowy projekt modelu Adventure Works Internet Sales.</span><span class="sxs-lookup"><span data-stu-id="456bf-115">Before performing the tasks in this supplemental lesson, you should have completed all previous lessons or have a completed Adventure Works Internet Sales sample model project.</span></span> 

<span data-ttu-id="456bf-116">Jeśli projekt AW Internet Sales został utworzony w ramach tego samouczka, model nie zawiera jeszcze żadnych danych ani hierarchii niewyrównanych.</span><span class="sxs-lookup"><span data-stu-id="456bf-116">If you've created the AW Internet Sales project as part of the tutorial, your model does not yet contain any data or hierarchies that are ragged.</span></span> <span data-ttu-id="456bf-117">W celu ukończenia tej lekcji uzupełniającej należy najpierw utworzyć problem, dodając pewne dodatkowe tabele oraz tworząc relacje, kolumny obliczeniowe, miarę i nową hierarchię organizacji.</span><span class="sxs-lookup"><span data-stu-id="456bf-117">To complete this supplemental lesson, you first have to create the problem by adding some additional tables, create relationships, calculated columns, a measure, and a new Organization hierarchy.</span></span> <span data-ttu-id="456bf-118">Zajmie to ok. 15 minut.</span><span class="sxs-lookup"><span data-stu-id="456bf-118">That part takes about 15 minutes.</span></span> <span data-ttu-id="456bf-119">Następnie można rozwiązać problem w ciągu kilku minut.</span><span class="sxs-lookup"><span data-stu-id="456bf-119">Then, you get to solve it in just a few minutes.</span></span>  

## <a name="add-tables-and-objects"></a><span data-ttu-id="456bf-120">Dodawanie tabel i obiektów</span><span class="sxs-lookup"><span data-stu-id="456bf-120">Add tables and objects</span></span>
  
### <a name="to-add-new-tables-to-your-model"></a><span data-ttu-id="456bf-121">Dodawanie nowych tabel do modelu</span><span class="sxs-lookup"><span data-stu-id="456bf-121">To add new tables to your model</span></span>
  
1.  <span data-ttu-id="456bf-122">W Eksploratorze modeli tabelarycznych rozwiń pozycję **Źródła danych**, a następnie prawym przyciskiem myszy kliknij połączenie i kliknij pozycję **Importuj nowe tabele**.</span><span class="sxs-lookup"><span data-stu-id="456bf-122">In Tabular Model Explorer, expand **Data Sources**, then right-click your connection > **Import New Tables**.</span></span>
  
2.  <span data-ttu-id="456bf-123">W oknie Nawigator wybierz tabele **DimEmployee** oraz **FactResellerSales**, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="456bf-123">In Navigator, select **DimEmployee** and **FactResellerSales**, and then click **OK**.</span></span>

3.  <span data-ttu-id="456bf-124">W edytorze zapytań kliknij opcję **Importuj**</span><span class="sxs-lookup"><span data-stu-id="456bf-124">In Query Editor, click **Import**</span></span>

4.  <span data-ttu-id="456bf-125">Utwórz następującą [relację](../tutorials/aas-lesson-4-create-relationships.md):</span><span class="sxs-lookup"><span data-stu-id="456bf-125">Create the following [relationships](../tutorials/aas-lesson-4-create-relationships.md):</span></span>

    | <span data-ttu-id="456bf-126">Tabela 1</span><span class="sxs-lookup"><span data-stu-id="456bf-126">Table 1</span></span>           | <span data-ttu-id="456bf-127">Kolumna</span><span class="sxs-lookup"><span data-stu-id="456bf-127">Column</span></span>       | <span data-ttu-id="456bf-128">Kierunek filtru</span><span class="sxs-lookup"><span data-stu-id="456bf-128">Filter Direction</span></span>   | <span data-ttu-id="456bf-129">Tabela 2</span><span class="sxs-lookup"><span data-stu-id="456bf-129">Table 2</span></span>     | <span data-ttu-id="456bf-130">Kolumna</span><span class="sxs-lookup"><span data-stu-id="456bf-130">Column</span></span>      | <span data-ttu-id="456bf-131">Aktywne</span><span class="sxs-lookup"><span data-stu-id="456bf-131">Active</span></span> |
    |-------------------|--------------|--------------------|-------------|-------------|--------|
    | <span data-ttu-id="456bf-132">FactResellerSales</span><span class="sxs-lookup"><span data-stu-id="456bf-132">FactResellerSales</span></span> | <span data-ttu-id="456bf-133">OrderDateKey</span><span class="sxs-lookup"><span data-stu-id="456bf-133">OrderDateKey</span></span> | <span data-ttu-id="456bf-134">Domyślne</span><span class="sxs-lookup"><span data-stu-id="456bf-134">Default</span></span>            | <span data-ttu-id="456bf-135">DimDate</span><span class="sxs-lookup"><span data-stu-id="456bf-135">DimDate</span></span>     | <span data-ttu-id="456bf-136">Date</span><span class="sxs-lookup"><span data-stu-id="456bf-136">Date</span></span>        | <span data-ttu-id="456bf-137">Tak</span><span class="sxs-lookup"><span data-stu-id="456bf-137">Yes</span></span>    |
    | <span data-ttu-id="456bf-138">FactResellerSales</span><span class="sxs-lookup"><span data-stu-id="456bf-138">FactResellerSales</span></span> | <span data-ttu-id="456bf-139">DueDate</span><span class="sxs-lookup"><span data-stu-id="456bf-139">DueDate</span></span>      | <span data-ttu-id="456bf-140">Domyślne</span><span class="sxs-lookup"><span data-stu-id="456bf-140">Default</span></span>            | <span data-ttu-id="456bf-141">DimDate</span><span class="sxs-lookup"><span data-stu-id="456bf-141">DimDate</span></span>     | <span data-ttu-id="456bf-142">Date</span><span class="sxs-lookup"><span data-stu-id="456bf-142">Date</span></span>        | <span data-ttu-id="456bf-143">Nie</span><span class="sxs-lookup"><span data-stu-id="456bf-143">No</span></span>     |
    | <span data-ttu-id="456bf-144">FactResellerSales</span><span class="sxs-lookup"><span data-stu-id="456bf-144">FactResellerSales</span></span> | <span data-ttu-id="456bf-145">ShipDateKey</span><span class="sxs-lookup"><span data-stu-id="456bf-145">ShipDateKey</span></span>  | <span data-ttu-id="456bf-146">Domyślne</span><span class="sxs-lookup"><span data-stu-id="456bf-146">Default</span></span>            | <span data-ttu-id="456bf-147">DimDate</span><span class="sxs-lookup"><span data-stu-id="456bf-147">DimDate</span></span>     | <span data-ttu-id="456bf-148">Date</span><span class="sxs-lookup"><span data-stu-id="456bf-148">Date</span></span>        | <span data-ttu-id="456bf-149">Nie</span><span class="sxs-lookup"><span data-stu-id="456bf-149">No</span></span>     |
    | <span data-ttu-id="456bf-150">FactResellerSales</span><span class="sxs-lookup"><span data-stu-id="456bf-150">FactResellerSales</span></span> | <span data-ttu-id="456bf-151">ProductKey</span><span class="sxs-lookup"><span data-stu-id="456bf-151">ProductKey</span></span>   | <span data-ttu-id="456bf-152">Domyślne</span><span class="sxs-lookup"><span data-stu-id="456bf-152">Default</span></span>            | <span data-ttu-id="456bf-153">DimProduct</span><span class="sxs-lookup"><span data-stu-id="456bf-153">DimProduct</span></span>  | <span data-ttu-id="456bf-154">ProductKey</span><span class="sxs-lookup"><span data-stu-id="456bf-154">ProductKey</span></span>  | <span data-ttu-id="456bf-155">Tak</span><span class="sxs-lookup"><span data-stu-id="456bf-155">Yes</span></span>    |
    | <span data-ttu-id="456bf-156">FactResellerSales</span><span class="sxs-lookup"><span data-stu-id="456bf-156">FactResellerSales</span></span> | <span data-ttu-id="456bf-157">EmployeeKey</span><span class="sxs-lookup"><span data-stu-id="456bf-157">EmployeeKey</span></span>  | <span data-ttu-id="456bf-158">Do obu tabel</span><span class="sxs-lookup"><span data-stu-id="456bf-158">To Both Tables</span></span> | <span data-ttu-id="456bf-159">DimEmployee</span><span class="sxs-lookup"><span data-stu-id="456bf-159">DimEmployee</span></span> | <span data-ttu-id="456bf-160">EmployeeKey</span><span class="sxs-lookup"><span data-stu-id="456bf-160">EmployeeKey</span></span> | <span data-ttu-id="456bf-161">Tak</span><span class="sxs-lookup"><span data-stu-id="456bf-161">Yes</span></span>    |

5. <span data-ttu-id="456bf-162">W tabeli **DimEmployee** utwórz następujące [kolumny obliczeniowe](../tutorials/aas-lesson-5-create-calculated-columns.md):</span><span class="sxs-lookup"><span data-stu-id="456bf-162">In the **DimEmployee** table, create the following [calculated columns](../tutorials/aas-lesson-5-create-calculated-columns.md):</span></span> 

    <span data-ttu-id="456bf-163">**Ścieżka**</span><span class="sxs-lookup"><span data-stu-id="456bf-163">**Path**</span></span> 
    ```
    =PATH([EmployeeKey],[ParentEmployeeKey])
    ```

    <span data-ttu-id="456bf-164">**FullName**</span><span class="sxs-lookup"><span data-stu-id="456bf-164">**FullName**</span></span> 
    ```
    =[FirstName] & " " & [MiddleName] & " " & [LastName]
    ```

    <span data-ttu-id="456bf-165">**Level1**</span><span class="sxs-lookup"><span data-stu-id="456bf-165">**Level1**</span></span> 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,1)) 
    ```

    <span data-ttu-id="456bf-166">**Level2**</span><span class="sxs-lookup"><span data-stu-id="456bf-166">**Level2**</span></span> 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,2)) 
    ```

    <span data-ttu-id="456bf-167">**Level3**</span><span class="sxs-lookup"><span data-stu-id="456bf-167">**Level3**</span></span> 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,3)) 
    ```

    <span data-ttu-id="456bf-168">**Level4**</span><span class="sxs-lookup"><span data-stu-id="456bf-168">**Level4**</span></span> 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,4)) 
    ```

    <span data-ttu-id="456bf-169">**Level5**</span><span class="sxs-lookup"><span data-stu-id="456bf-169">**Level5**</span></span> 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,5)) 
    ```

6.  <span data-ttu-id="456bf-170">W tabeli **DimEmployee** utwórz [hierarchię](../tutorials/aas-lesson-9-create-hierarchies.md) o nazwie **Organization** (Organizacja).</span><span class="sxs-lookup"><span data-stu-id="456bf-170">In the **DimEmployee** table, create a [hierarchy](../tutorials/aas-lesson-9-create-hierarchies.md) named **Organization**.</span></span> <span data-ttu-id="456bf-171">Dodaj następujące kolumny w podanej kolejności: **Level1**, **Level2**, **Level3**, **Level4**, **Level5**.</span><span class="sxs-lookup"><span data-stu-id="456bf-171">Add the following columns in-order: **Level1**, **Level2**, **Level3**, **Level4**, **Level5**.</span></span>

7.  <span data-ttu-id="456bf-172">W tabeli **FactResellerSales** utwórz następującą [miarę](../tutorials/aas-lesson-6-create-measures.md):</span><span class="sxs-lookup"><span data-stu-id="456bf-172">In the **FactResellerSales** table, create the following [measure](../tutorials/aas-lesson-6-create-measures.md):</span></span>

    ```
    ResellerTotalSales:=SUM([SalesAmount])
    ```

8.  <span data-ttu-id="456bf-173">Użyj funkcji [Analiza w programie Excel](../tutorials/aas-lesson-12-analyze-in-excel.md), aby otworzyć program Excel i automatycznie utworzyć tabelę przestawną.</span><span class="sxs-lookup"><span data-stu-id="456bf-173">Use [Analyze in Excel](../tutorials/aas-lesson-12-analyze-in-excel.md) to open Excel and automatically create a PivotTable.</span></span>

9.  <span data-ttu-id="456bf-174">W obszarze **Pola tabeli przestawnej** dodaj hierarchię **Organization** z tabeli **DimEmployee** do pola **Wiersze** i miarę **ResellerTotalSales** z tabeli **FactResellerSales** do pola **Wartości**.</span><span class="sxs-lookup"><span data-stu-id="456bf-174">In **PivotTable Fields**, add the **Organization** hierarchy from the **DimEmployee** table to **Rows**, and the **ResellerTotalSales** measure from the **FactResellerSales**  table to **Values**.</span></span>

    ![aas-lesson-detail-ragged-hierarchies-pivottable](../tutorials/media/aas-lesson-detail-ragged-hierarchies-pivottable.png)

    <span data-ttu-id="456bf-176">Jak widać w tabeli przestawnej, w hierarchii wyświetlane są wiersze niewyrównane.</span><span class="sxs-lookup"><span data-stu-id="456bf-176">As you can see in the PivotTable, the hierarchy displays rows that are ragged.</span></span> <span data-ttu-id="456bf-177">Istnieje wiele wierszy, w których są widoczne puste elementy członkowskie.</span><span class="sxs-lookup"><span data-stu-id="456bf-177">There are many rows where blank members are shown.</span></span>

## <a name="to-fix-the-ragged-hierarchy-by-setting-the-hide-members-property"></a><span data-ttu-id="456bf-178">Rozwiązywanie niewyrównanej hierarchii przez ustawienie właściwości Ukryj elementy członkowskie</span><span class="sxs-lookup"><span data-stu-id="456bf-178">To fix the ragged hierarchy by setting the Hide members property</span></span>

1.  <span data-ttu-id="456bf-179">W **Eksploratorze modeli tabelarycznych** rozwiń węzeł **Tabele** > **DimEmployee** > **Hierarchie** > **Organization**.</span><span class="sxs-lookup"><span data-stu-id="456bf-179">In **Tabular Model Explorer**, expand **Tables** > **DimEmployee** > **Hierarchies** > **Organization**.</span></span>

2.  <span data-ttu-id="456bf-180">W obszarze **Właściwości** > **Ukryj elementy członkowskie** wybierz pozycję **Ukryj puste elementy członkowskie**.</span><span class="sxs-lookup"><span data-stu-id="456bf-180">In **Properties** > **Hide Members**, select **Hide blank members**.</span></span> 

    ![aas-lesson-detail-ragged-hierarchies-hidemembers](../tutorials/media/aas-lesson-detail-ragged-hierarchies-hidemembers.png)

3.  <span data-ttu-id="456bf-182">Po powrocie do programu Excel odśwież tabelę przestawną.</span><span class="sxs-lookup"><span data-stu-id="456bf-182">Back in Excel, refresh the PivotTable.</span></span> 

    ![aas-lesson-detail-ragged-hierarchies-pivottable-refresh](../tutorials/media/aas-lesson-detail-ragged-hierarchies-pivottable-refresh.png)

    <span data-ttu-id="456bf-184">Teraz tabela wygląda o wiele lepiej.</span><span class="sxs-lookup"><span data-stu-id="456bf-184">Now that looks a whole lot better!</span></span>

## <a name="see-also"></a><span data-ttu-id="456bf-185">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="456bf-185">See Also</span></span>   
[<span data-ttu-id="456bf-186">Lekcja 9. Tworzenie hierarchii</span><span class="sxs-lookup"><span data-stu-id="456bf-186">Lesson 9: Create hierarchies</span></span>](../tutorials/aas-lesson-9-create-hierarchies.md)  
[<span data-ttu-id="456bf-187">Lekcja uzupełniająca — zabezpieczenia dynamiczne</span><span class="sxs-lookup"><span data-stu-id="456bf-187">Supplemental Lesson - Dynamic security</span></span>](../tutorials/aas-supplemental-lesson-dynamic-security.md)  
[<span data-ttu-id="456bf-188">Lekcja uzupełniająca — wiersze szczegółów</span><span class="sxs-lookup"><span data-stu-id="456bf-188">Supplemental Lesson - Detail rows</span></span>](../tutorials/aas-supplemental-lesson-detail-rows.md)  