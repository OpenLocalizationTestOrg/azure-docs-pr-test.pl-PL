---
<span data-ttu-id="c0947-101">title: aaa "samouczek lekcji dodatkowych usług Azure Analysis Services: niewyrównanych hierarchie | Opis elementu Microsoft Docs": w tym artykule opisano, jak toofix niewyrównanych hierarchie hello samouczka usług Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="c0947-101">title: aaa"Azure Analysis Services tutorial supplemental lesson: Ragged hierarchies | Microsoft Docs" description: Describes how toofix ragged hierarchies in hello Azure Analysis Services tutorial.</span></span>
<span data-ttu-id="c0947-102">usługi: documentationcenter usług analysis services: "Autor: minewiskan Menedżera: Edytor erikre:" tagów: "</span><span class="sxs-lookup"><span data-stu-id="c0947-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="c0947-103">MS.AssetID: ms.service: ms.devlang usług analysis services: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend</span><span class="sxs-lookup"><span data-stu-id="c0947-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend</span></span>
---
# <a name="supplemental-lesson---ragged-hierarchies"></a><span data-ttu-id="c0947-104">Lekcja uzupełniająca — niewyrównane hierarchie</span><span class="sxs-lookup"><span data-stu-id="c0947-104">Supplemental lesson - Ragged hierarchies</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="c0947-105">W tej lekcji uzupełniającej przedstawione zostanie rozwiązanie często występującego problemu polegającego na tworzeniu tabeli przestawnej dla hierarchii zawierających puste wartości (elementy członkowskie) na różnych poziomach.</span><span class="sxs-lookup"><span data-stu-id="c0947-105">In this supplemental lesson, you resolve a common problem when pivoting on hierarchies that contain blank values (members) at different levels.</span></span> <span data-ttu-id="c0947-106">Przykładem może być organizacja, w której menedżer wysokiego szczebla jako bezpośrednich podwładnych ma menedżerów działów oraz osoby niebędące menedżerami.</span><span class="sxs-lookup"><span data-stu-id="c0947-106">For example, an organization where a high-level manager has both departmental managers and non-managers as direct reports.</span></span> <span data-ttu-id="c0947-107">Innym przykładem mogą być hierarchie geograficzne składające się z kraju, regionu i miasta, gdzie niektóre miasta nie mają nadrzędnego kraju lub regionu, jak Waszyngton czy Watykan.</span><span class="sxs-lookup"><span data-stu-id="c0947-107">Or, geographic hierarchies composed of Country-Region-City, where some cities lack a parent State or Province, such as Washington D.C., Vatican City.</span></span> <span data-ttu-id="c0947-108">Gdy w hierarchii jest puste elementy członkowskie, jego często descends toodifferent lub niewyrównanych poziomów.</span><span class="sxs-lookup"><span data-stu-id="c0947-108">When a hierarchy has blank members, it often descends toodifferent, or ragged, levels.</span></span>

![aas-lesson-detail-ragged-hierarchies-table](../tutorials/media/aas-lesson-detail-ragged-hierarchies-table.png)

<span data-ttu-id="c0947-110">Modeli tabelarycznych przy poziomie zgodności hello 1400 ma dodatkowe **Ukryj elementy członkowskie** właściwości dla hierarchii.</span><span class="sxs-lookup"><span data-stu-id="c0947-110">Tabular models at hello 1400 compatibility level have an additional **Hide Members** property for hierarchies.</span></span> <span data-ttu-id="c0947-111">Witaj **domyślne** ustawienia obowiązuje założenie, nie ma żadnych członków puste na dowolnym poziomie.</span><span class="sxs-lookup"><span data-stu-id="c0947-111">hello **Default** setting assumes there are no blank members at any level.</span></span> <span data-ttu-id="c0947-112">Witaj **Ukryj puste elementy członkowskie** wyklucza puste elementy członkowskie z hierarchii powitania po dodaniu tooa tabeli przestawnej lub raportu.</span><span class="sxs-lookup"><span data-stu-id="c0947-112">hello **Hide blank members** setting excludes blank members from hello hierarchy when added tooa PivotTable or report.</span></span>  
  
<span data-ttu-id="c0947-113">Szacowany czas toocomplete tej lekcji: **20 minut**</span><span class="sxs-lookup"><span data-stu-id="c0947-113">Estimated time toocomplete this lesson: **20 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="c0947-114">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="c0947-114">Prerequisites</span></span>  
<span data-ttu-id="c0947-115">Ta lekcja uzupełniająca stanowi część samouczka modelowania tabelarycznego.</span><span class="sxs-lookup"><span data-stu-id="c0947-115">This supplemental lesson topic is part of a tabular modeling tutorial.</span></span> <span data-ttu-id="c0947-116">Przed wykonaniem zadania hello w tym uzupełniające lekcji, powinno mieć ukończone wszystkie poprzednie — lekcje lub zakończonych projektu modelu przykładowej firmy Adventure Works Internet sprzedaży.</span><span class="sxs-lookup"><span data-stu-id="c0947-116">Before performing hello tasks in this supplemental lesson, you should have completed all previous lessons or have a completed Adventure Works Internet Sales sample model project.</span></span> 

<span data-ttu-id="c0947-117">Jeśli po utworzeniu projektu sprzedaży Internet AW hello jako części samouczka hello model nie zawiera jeszcze żadnych danych lub hierarchiami niewyrównane.</span><span class="sxs-lookup"><span data-stu-id="c0947-117">If you've created hello AW Internet Sales project as part of hello tutorial, your model does not yet contain any data or hierarchies that are ragged.</span></span> <span data-ttu-id="c0947-118">toocomplete tej lekcji uzupełniające, konieczne jest przeprowadzenie najpierw toocreate hello problem, dodając niektóre dodatkowe tabele, Utwórz relacje, kolumn obliczeniowych, miary i nowej hierarchii organizacji.</span><span class="sxs-lookup"><span data-stu-id="c0947-118">toocomplete this supplemental lesson, you first have toocreate hello problem by adding some additional tables, create relationships, calculated columns, a measure, and a new Organization hierarchy.</span></span> <span data-ttu-id="c0947-119">Zajmie to ok. 15 minut.</span><span class="sxs-lookup"><span data-stu-id="c0947-119">That part takes about 15 minutes.</span></span> <span data-ttu-id="c0947-120">Następnie należy pobrać toosolve w ciągu kilku minut.</span><span class="sxs-lookup"><span data-stu-id="c0947-120">Then, you get toosolve it in just a few minutes.</span></span>  

## <a name="add-tables-and-objects"></a><span data-ttu-id="c0947-121">Dodawanie tabel i obiektów</span><span class="sxs-lookup"><span data-stu-id="c0947-121">Add tables and objects</span></span>
  
### <a name="tooadd-new-tables-tooyour-model"></a><span data-ttu-id="c0947-122">nowy model tooyour tabele tooadd</span><span class="sxs-lookup"><span data-stu-id="c0947-122">tooadd new tables tooyour model</span></span>
  
1.  <span data-ttu-id="c0947-123">W Eksploratorze modeli tabelarycznych rozwiń pozycję **Źródła danych**, a następnie prawym przyciskiem myszy kliknij połączenie i kliknij pozycję **Importuj nowe tabele**.</span><span class="sxs-lookup"><span data-stu-id="c0947-123">In Tabular Model Explorer, expand **Data Sources**, then right-click your connection > **Import New Tables**.</span></span>
  
2.  <span data-ttu-id="c0947-124">W oknie Nawigator wybierz tabele **DimEmployee** oraz **FactResellerSales**, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="c0947-124">In Navigator, select **DimEmployee** and **FactResellerSales**, and then click **OK**.</span></span>

3.  <span data-ttu-id="c0947-125">W edytorze zapytań kliknij opcję **Importuj**</span><span class="sxs-lookup"><span data-stu-id="c0947-125">In Query Editor, click **Import**</span></span>

4.  <span data-ttu-id="c0947-126">Utwórz następujące hello [relacje](../tutorials/aas-lesson-4-create-relationships.md):</span><span class="sxs-lookup"><span data-stu-id="c0947-126">Create hello following [relationships](../tutorials/aas-lesson-4-create-relationships.md):</span></span>

    | <span data-ttu-id="c0947-127">Tabela 1</span><span class="sxs-lookup"><span data-stu-id="c0947-127">Table 1</span></span>           | <span data-ttu-id="c0947-128">Kolumna</span><span class="sxs-lookup"><span data-stu-id="c0947-128">Column</span></span>       | <span data-ttu-id="c0947-129">Kierunek filtru</span><span class="sxs-lookup"><span data-stu-id="c0947-129">Filter Direction</span></span>   | <span data-ttu-id="c0947-130">Tabela 2</span><span class="sxs-lookup"><span data-stu-id="c0947-130">Table 2</span></span>     | <span data-ttu-id="c0947-131">Kolumna</span><span class="sxs-lookup"><span data-stu-id="c0947-131">Column</span></span>      | <span data-ttu-id="c0947-132">Aktywne</span><span class="sxs-lookup"><span data-stu-id="c0947-132">Active</span></span> |
    |-------------------|--------------|--------------------|-------------|-------------|--------|
    | <span data-ttu-id="c0947-133">FactResellerSales</span><span class="sxs-lookup"><span data-stu-id="c0947-133">FactResellerSales</span></span> | <span data-ttu-id="c0947-134">OrderDateKey</span><span class="sxs-lookup"><span data-stu-id="c0947-134">OrderDateKey</span></span> | <span data-ttu-id="c0947-135">Domyślne</span><span class="sxs-lookup"><span data-stu-id="c0947-135">Default</span></span>            | <span data-ttu-id="c0947-136">DimDate</span><span class="sxs-lookup"><span data-stu-id="c0947-136">DimDate</span></span>     | <span data-ttu-id="c0947-137">Date</span><span class="sxs-lookup"><span data-stu-id="c0947-137">Date</span></span>        | <span data-ttu-id="c0947-138">Tak</span><span class="sxs-lookup"><span data-stu-id="c0947-138">Yes</span></span>    |
    | <span data-ttu-id="c0947-139">FactResellerSales</span><span class="sxs-lookup"><span data-stu-id="c0947-139">FactResellerSales</span></span> | <span data-ttu-id="c0947-140">DueDate</span><span class="sxs-lookup"><span data-stu-id="c0947-140">DueDate</span></span>      | <span data-ttu-id="c0947-141">Domyślne</span><span class="sxs-lookup"><span data-stu-id="c0947-141">Default</span></span>            | <span data-ttu-id="c0947-142">DimDate</span><span class="sxs-lookup"><span data-stu-id="c0947-142">DimDate</span></span>     | <span data-ttu-id="c0947-143">Date</span><span class="sxs-lookup"><span data-stu-id="c0947-143">Date</span></span>        | <span data-ttu-id="c0947-144">Nie</span><span class="sxs-lookup"><span data-stu-id="c0947-144">No</span></span>     |
    | <span data-ttu-id="c0947-145">FactResellerSales</span><span class="sxs-lookup"><span data-stu-id="c0947-145">FactResellerSales</span></span> | <span data-ttu-id="c0947-146">ShipDateKey</span><span class="sxs-lookup"><span data-stu-id="c0947-146">ShipDateKey</span></span>  | <span data-ttu-id="c0947-147">Domyślne</span><span class="sxs-lookup"><span data-stu-id="c0947-147">Default</span></span>            | <span data-ttu-id="c0947-148">DimDate</span><span class="sxs-lookup"><span data-stu-id="c0947-148">DimDate</span></span>     | <span data-ttu-id="c0947-149">Date</span><span class="sxs-lookup"><span data-stu-id="c0947-149">Date</span></span>        | <span data-ttu-id="c0947-150">Nie</span><span class="sxs-lookup"><span data-stu-id="c0947-150">No</span></span>     |
    | <span data-ttu-id="c0947-151">FactResellerSales</span><span class="sxs-lookup"><span data-stu-id="c0947-151">FactResellerSales</span></span> | <span data-ttu-id="c0947-152">ProductKey</span><span class="sxs-lookup"><span data-stu-id="c0947-152">ProductKey</span></span>   | <span data-ttu-id="c0947-153">Domyślne</span><span class="sxs-lookup"><span data-stu-id="c0947-153">Default</span></span>            | <span data-ttu-id="c0947-154">DimProduct</span><span class="sxs-lookup"><span data-stu-id="c0947-154">DimProduct</span></span>  | <span data-ttu-id="c0947-155">ProductKey</span><span class="sxs-lookup"><span data-stu-id="c0947-155">ProductKey</span></span>  | <span data-ttu-id="c0947-156">Tak</span><span class="sxs-lookup"><span data-stu-id="c0947-156">Yes</span></span>    |
    | <span data-ttu-id="c0947-157">FactResellerSales</span><span class="sxs-lookup"><span data-stu-id="c0947-157">FactResellerSales</span></span> | <span data-ttu-id="c0947-158">EmployeeKey</span><span class="sxs-lookup"><span data-stu-id="c0947-158">EmployeeKey</span></span>  | <span data-ttu-id="c0947-159">Tabele tooBoth</span><span class="sxs-lookup"><span data-stu-id="c0947-159">tooBoth Tables</span></span> | <span data-ttu-id="c0947-160">DimEmployee</span><span class="sxs-lookup"><span data-stu-id="c0947-160">DimEmployee</span></span> | <span data-ttu-id="c0947-161">EmployeeKey</span><span class="sxs-lookup"><span data-stu-id="c0947-161">EmployeeKey</span></span> | <span data-ttu-id="c0947-162">Tak</span><span class="sxs-lookup"><span data-stu-id="c0947-162">Yes</span></span>    |

5. <span data-ttu-id="c0947-163">W hello **DimEmployee** tabeli, należy utworzyć następujące hello [kolumn obliczeniowych](../tutorials/aas-lesson-5-create-calculated-columns.md):</span><span class="sxs-lookup"><span data-stu-id="c0947-163">In hello **DimEmployee** table, create hello following [calculated columns](../tutorials/aas-lesson-5-create-calculated-columns.md):</span></span> 

    <span data-ttu-id="c0947-164">**Ścieżka**</span><span class="sxs-lookup"><span data-stu-id="c0947-164">**Path**</span></span> 
    ```
    =PATH([EmployeeKey],[ParentEmployeeKey])
    ```

    <span data-ttu-id="c0947-165">**FullName**</span><span class="sxs-lookup"><span data-stu-id="c0947-165">**FullName**</span></span> 
    ```
    =[FirstName] & " " & [MiddleName] & " " & [LastName]
    ```

    <span data-ttu-id="c0947-166">**Level1**</span><span class="sxs-lookup"><span data-stu-id="c0947-166">**Level1**</span></span> 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,1)) 
    ```

    <span data-ttu-id="c0947-167">**Level2**</span><span class="sxs-lookup"><span data-stu-id="c0947-167">**Level2**</span></span> 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,2)) 
    ```

    <span data-ttu-id="c0947-168">**Level3**</span><span class="sxs-lookup"><span data-stu-id="c0947-168">**Level3**</span></span> 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,3)) 
    ```

    <span data-ttu-id="c0947-169">**Level4**</span><span class="sxs-lookup"><span data-stu-id="c0947-169">**Level4**</span></span> 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,4)) 
    ```

    <span data-ttu-id="c0947-170">**Level5**</span><span class="sxs-lookup"><span data-stu-id="c0947-170">**Level5**</span></span> 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,5)) 
    ```

6.  <span data-ttu-id="c0947-171">W hello **DimEmployee** tabeli, należy utworzyć [hierarchii](../tutorials/aas-lesson-9-create-hierarchies.md) o nazwie **organizacji**.</span><span class="sxs-lookup"><span data-stu-id="c0947-171">In hello **DimEmployee** table, create a [hierarchy](../tutorials/aas-lesson-9-create-hierarchies.md) named **Organization**.</span></span> <span data-ttu-id="c0947-172">Dodaj następujące kolumny w kolejności hello: **Level1**, **Level2**, **Level3**, **Level4**, **Level5**.</span><span class="sxs-lookup"><span data-stu-id="c0947-172">Add hello following columns in-order: **Level1**, **Level2**, **Level3**, **Level4**, **Level5**.</span></span>

7.  <span data-ttu-id="c0947-173">W hello **FactResellerSales** tabeli, należy utworzyć następujące hello [miary](../tutorials/aas-lesson-6-create-measures.md):</span><span class="sxs-lookup"><span data-stu-id="c0947-173">In hello **FactResellerSales** table, create hello following [measure](../tutorials/aas-lesson-6-create-measures.md):</span></span>

    ```
    ResellerTotalSales:=SUM([SalesAmount])
    ```

8.  <span data-ttu-id="c0947-174">Użyj [analizy w programie Excel](../tutorials/aas-lesson-12-analyze-in-excel.md) tooopen programu Excel i automatycznie utworzyć tabelę przestawną.</span><span class="sxs-lookup"><span data-stu-id="c0947-174">Use [Analyze in Excel](../tutorials/aas-lesson-12-analyze-in-excel.md) tooopen Excel and automatically create a PivotTable.</span></span>

9.  <span data-ttu-id="c0947-175">W **pól tabeli przestawnej**, Dodaj hello **organizacji** hierarchii z hello **DimEmployee** tabeli zbyt**wierszy**i hello **ResellerTotalSales** miarę z hello **FactResellerSales** tabeli zbyt**wartości**.</span><span class="sxs-lookup"><span data-stu-id="c0947-175">In **PivotTable Fields**, add hello **Organization** hierarchy from hello **DimEmployee** table too**Rows**, and hello **ResellerTotalSales** measure from hello **FactResellerSales**  table too**Values**.</span></span>

    ![aas-lesson-detail-ragged-hierarchies-pivottable](../tutorials/media/aas-lesson-detail-ragged-hierarchies-pivottable.png)

    <span data-ttu-id="c0947-177">Jak widać w tabeli przestawnej hello hierarchii hello wyświetla wiersze, które są niewyrównane.</span><span class="sxs-lookup"><span data-stu-id="c0947-177">As you can see in hello PivotTable, hello hierarchy displays rows that are ragged.</span></span> <span data-ttu-id="c0947-178">Istnieje wiele wierszy, w których są widoczne puste elementy członkowskie.</span><span class="sxs-lookup"><span data-stu-id="c0947-178">There are many rows where blank members are shown.</span></span>

## <a name="toofix-hello-ragged-hierarchy-by-setting-hello-hide-members-property"></a><span data-ttu-id="c0947-179">Witaj toofix niewyrównanych hierarchii poprzez ustawienie właściwości elementów członkowskich Ukryj hello</span><span class="sxs-lookup"><span data-stu-id="c0947-179">toofix hello ragged hierarchy by setting hello Hide members property</span></span>

1.  <span data-ttu-id="c0947-180">W **Eksploratorze modeli tabelarycznych** rozwiń węzeł **Tabele** > **DimEmployee** > **Hierarchie** > **Organization**.</span><span class="sxs-lookup"><span data-stu-id="c0947-180">In **Tabular Model Explorer**, expand **Tables** > **DimEmployee** > **Hierarchies** > **Organization**.</span></span>

2.  <span data-ttu-id="c0947-181">W obszarze **Właściwości** > **Ukryj elementy członkowskie** wybierz pozycję **Ukryj puste elementy członkowskie**.</span><span class="sxs-lookup"><span data-stu-id="c0947-181">In **Properties** > **Hide Members**, select **Hide blank members**.</span></span> 

    ![aas-lesson-detail-ragged-hierarchies-hidemembers](../tutorials/media/aas-lesson-detail-ragged-hierarchies-hidemembers.png)

3.  <span data-ttu-id="c0947-183">W programie Excel Odśwież hello tabeli przestawnej.</span><span class="sxs-lookup"><span data-stu-id="c0947-183">Back in Excel, refresh hello PivotTable.</span></span> 

    ![aas-lesson-detail-ragged-hierarchies-pivottable-refresh](../tutorials/media/aas-lesson-detail-ragged-hierarchies-pivottable-refresh.png)

    <span data-ttu-id="c0947-185">Teraz tabela wygląda o wiele lepiej.</span><span class="sxs-lookup"><span data-stu-id="c0947-185">Now that looks a whole lot better!</span></span>

## <a name="see-also"></a><span data-ttu-id="c0947-186">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="c0947-186">See Also</span></span>   
[<span data-ttu-id="c0947-187">Lekcja 9. Tworzenie hierarchii</span><span class="sxs-lookup"><span data-stu-id="c0947-187">Lesson 9: Create hierarchies</span></span>](../tutorials/aas-lesson-9-create-hierarchies.md)  
[<span data-ttu-id="c0947-188">Lekcja uzupełniająca — zabezpieczenia dynamiczne</span><span class="sxs-lookup"><span data-stu-id="c0947-188">Supplemental Lesson - Dynamic security</span></span>](../tutorials/aas-supplemental-lesson-dynamic-security.md)  
[<span data-ttu-id="c0947-189">Lekcja uzupełniająca — wiersze szczegółów</span><span class="sxs-lookup"><span data-stu-id="c0947-189">Supplemental Lesson - Detail rows</span></span>](../tutorials/aas-supplemental-lesson-detail-rows.md)  