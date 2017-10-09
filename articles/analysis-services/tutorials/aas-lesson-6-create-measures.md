---
<span data-ttu-id="5c0d0-101">title: aaa "lekcji samouczka usług Azure Analysis Services 6: tworzenie miar | Opis elementu Microsoft Docs": w tym artykule opisano, jak toocreate środki w projekcie samouczek hello Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="5c0d0-101">title: aaa"Azure Analysis Services tutorial lesson 6: Create measures | Microsoft Docs" description: Describes how toocreate measures in hello Azure Analysis Services tutorial project.</span></span> <span data-ttu-id="5c0d0-102">usługi: documentationcenter usług analysis services: "Autor: minewiskan Menedżera: Edytor erikre:" tagów: "</span><span class="sxs-lookup"><span data-stu-id="5c0d0-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="5c0d0-103">MS.AssetID: ms.service: ms.devlang usług analysis services: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: ms.author 2017-06/01: owend</span><span class="sxs-lookup"><span data-stu-id="5c0d0-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 06/01/2017 ms.author: owend</span></span>
---
# <a name="lesson-6-create-measures"></a><span data-ttu-id="5c0d0-104">Lekcja 6. Tworzenie miar</span><span class="sxs-lookup"><span data-stu-id="5c0d0-104">Lesson 6: Create measures</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="5c0d0-105">W tej lekcji możesz utworzyć toobe miar zawarte w modelu.</span><span class="sxs-lookup"><span data-stu-id="5c0d0-105">In this lesson, you create measures toobe included in your model.</span></span> <span data-ttu-id="5c0d0-106">Podobne toohello obliczane kolumny, które utworzono, miary jest obliczenie utworzony przy użyciu formuły języka DAX.</span><span class="sxs-lookup"><span data-stu-id="5c0d0-106">Similar toohello calculated columns you created, a measure is a calculation created by using a DAX formula.</span></span> <span data-ttu-id="5c0d0-107">Jednak w odróżnieniu od kolumn obliczeniowych miary są szacowane na podstawie *filtru* wybranego przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="5c0d0-107">However, unlike calculated columns, measures are evaluated based on a user selected *filter*.</span></span> <span data-ttu-id="5c0d0-108">Na przykład określonej kolumny lub fragmentatora dodane toohello pole etykiety wierszy w tabeli przestawnej.</span><span class="sxs-lookup"><span data-stu-id="5c0d0-108">For example, a particular column or slicer added toohello Row Labels field in a PivotTable.</span></span> <span data-ttu-id="5c0d0-109">Wartość każdej komórki w filtrze hello następnie jest obliczana na podstawie miary hello zastosowane.</span><span class="sxs-lookup"><span data-stu-id="5c0d0-109">A value for each cell in hello filter is then calculated by hello applied measure.</span></span> <span data-ttu-id="5c0d0-110">Środki są wydajne i elastyczne obliczeń, które mają tooinclude prawie wszystkie modele tabelaryczne tooperform dynamiczne obliczeń na dane liczbowe.</span><span class="sxs-lookup"><span data-stu-id="5c0d0-110">Measures are powerful, flexible calculations that you want tooinclude in almost all tabular models tooperform dynamic calculations on numerical data.</span></span> <span data-ttu-id="5c0d0-111">toolearn więcej, zobacz [środki](https://docs.microsoft.com/sql/analysis-services/tabular-models/measures-ssas-tabular).</span><span class="sxs-lookup"><span data-stu-id="5c0d0-111">toolearn more, see [Measures](https://docs.microsoft.com/sql/analysis-services/tabular-models/measures-ssas-tabular).</span></span>
  
<span data-ttu-id="5c0d0-112">środki toocreate używasz hello *siatce miar*.</span><span class="sxs-lookup"><span data-stu-id="5c0d0-112">toocreate measures, you use hello *Measure Grid*.</span></span> <span data-ttu-id="5c0d0-113">Każda tabela domyślnie zawiera pustą siatkę miar. Zwykle jednak nie tworzy się miar dla każdej tabeli.</span><span class="sxs-lookup"><span data-stu-id="5c0d0-113">By default, each table has an empty measure grid; however, you typically do not create measures for every table.</span></span> <span data-ttu-id="5c0d0-114">Siatka miary Hello pojawia się poniżej tabeli w Projektancie modeli hello w widoku danych.</span><span class="sxs-lookup"><span data-stu-id="5c0d0-114">hello measure grid appears below a table in hello model designer when in Data View.</span></span> <span data-ttu-id="5c0d0-115">toohide lub wyświetla hello miary siatki dla tabeli, kliknij przycisk hello **tabeli** menu, a następnie kliknij przycisk **Pokaż siatkę miary**.</span><span class="sxs-lookup"><span data-stu-id="5c0d0-115">toohide or show hello measure grid for a table, click hello **Table** menu, and then click **Show Measure Grid**.</span></span>  
  
<span data-ttu-id="5c0d0-116">Klikając pustej komórki w siatce miar hello, a następnie wpisując formuły języka DAX na pasku formuły hello można utworzyć miary.</span><span class="sxs-lookup"><span data-stu-id="5c0d0-116">You can create a measure by clicking an empty cell in hello measure grid, and then typing a DAX formula in hello formula bar.</span></span> <span data-ttu-id="5c0d0-117">Gdy kliknij wprowadź formułę hello toocomplete, miary hello następnie pojawi się w komórce hello.</span><span class="sxs-lookup"><span data-stu-id="5c0d0-117">When you click ENTER toocomplete hello formula, hello measure then appears in hello cell.</span></span> <span data-ttu-id="5c0d0-118">Można również utworzyć środki przy użyciu standardowych agregacji, klikając kolumnę, a następnie klikając hello przycisku Autosumowanie (**∑**) na powitania narzędzi.</span><span class="sxs-lookup"><span data-stu-id="5c0d0-118">You can also create measures using a standard aggregation function by clicking a column, and then clicking hello AutoSum button (**∑**) on hello toolbar.</span></span> <span data-ttu-id="5c0d0-119">Środki utworzone za pomocą funkcji Autosumowania hello są wyświetlane w komórce siatki miary hello bezpośrednio pod hello kolumny, ale mogą zostać przeniesione.</span><span class="sxs-lookup"><span data-stu-id="5c0d0-119">Measures created using hello AutoSum feature appear in hello measure grid cell directly beneath hello column, but can be moved.</span></span>  
  
<span data-ttu-id="5c0d0-120">W tej lekcji utworzysz środki wprowadzając zarówno formuły języka DAX na pasku formuły hello i za pomocą funkcji Autosumowania hello.</span><span class="sxs-lookup"><span data-stu-id="5c0d0-120">In this lesson, you create measures by both entering a DAX formula in hello formula bar, and by using hello AutoSum feature.</span></span>  
  
<span data-ttu-id="5c0d0-121">Szacowany czas toocomplete tej lekcji: **30 minut**</span><span class="sxs-lookup"><span data-stu-id="5c0d0-121">Estimated time toocomplete this lesson: **30 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="5c0d0-122">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="5c0d0-122">Prerequisites</span></span>  
<span data-ttu-id="5c0d0-123">Ten temat stanowi część samouczka modelowania tabelarycznego, który należy wykonać w podanej kolejności.</span><span class="sxs-lookup"><span data-stu-id="5c0d0-123">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="5c0d0-124">Przed wykonaniem zadania hello w tej lekcji, powinno mieć ukończone poprzedniej lekcji hello: [lekcji 5: Tworzenie kolumn obliczeniowych](../tutorials/aas-lesson-5-create-calculated-columns.md).</span><span class="sxs-lookup"><span data-stu-id="5c0d0-124">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 5: Create calculated columns](../tutorials/aas-lesson-5-create-calculated-columns.md).</span></span>  
  
## <a name="create-measures"></a><span data-ttu-id="5c0d0-125">Tworzenie miar</span><span class="sxs-lookup"><span data-stu-id="5c0d0-125">Create measures</span></span>  
  
#### <a name="toocreate-a-dayscurrentquartertodate-measure-in-hello-dimdate-table"></a><span data-ttu-id="5c0d0-126">toocreate DaysCurrentQuarterToDate miary w tabeli DimDate hello</span><span class="sxs-lookup"><span data-stu-id="5c0d0-126">toocreate a DaysCurrentQuarterToDate measure in hello DimDate table</span></span>  
  
1.  <span data-ttu-id="5c0d0-127">W Konstruktorze modelu powitania kliknij hello **DimDate** tabeli.</span><span class="sxs-lookup"><span data-stu-id="5c0d0-127">In hello model designer, click hello **DimDate** table.</span></span>  
  
2.  <span data-ttu-id="5c0d0-128">W siatce miar hello kliknij przycisk hello lewego górnego pustej komórki.</span><span class="sxs-lookup"><span data-stu-id="5c0d0-128">In hello measure grid, click hello top-left empty cell.</span></span>  
  
3.  <span data-ttu-id="5c0d0-129">Na pasku formuły hello wpisz hello następującej formuły:</span><span class="sxs-lookup"><span data-stu-id="5c0d0-129">In hello formula bar, type hello following formula:</span></span>  
  
    ```
    DaysCurrentQuarterToDate:=COUNTROWS( DATESQTD( 'DimDate'[Date])) 
    ```
  
    <span data-ttu-id="5c0d0-130">Powiadomienie hello lewego górnego komórki zawiera teraz nazwę miary **DaysCurrentQuarterToDate**, a następnie wynik hello **92**.</span><span class="sxs-lookup"><span data-stu-id="5c0d0-130">Notice hello top-left cell now contains a measure name, **DaysCurrentQuarterToDate**, followed by hello result, **92**.</span></span>
    
      ![aas-lesson6-newmeasure](../tutorials/media/aas-lesson6-newmeasure.png) 
    
    <span data-ttu-id="5c0d0-132">W odróżnieniu od kolumny obliczeniowej z formułami miary możesz wpisać hello Nazwa miary, wprowadź dwukropek, następuje hello wyrażenia formuły.</span><span class="sxs-lookup"><span data-stu-id="5c0d0-132">Unlike calculated columns, with measure formulas you can type hello measure name, followed by a colon, followed by hello formula expression.</span></span>

  
#### <a name="toocreate-a-daysincurrentquarter-measure-in-hello-dimdate-table"></a><span data-ttu-id="5c0d0-133">toocreate DaysInCurrentQuarter miary w tabeli DimDate hello</span><span class="sxs-lookup"><span data-stu-id="5c0d0-133">toocreate a DaysInCurrentQuarter measure in hello DimDate table</span></span>  
  
1.  <span data-ttu-id="5c0d0-134">Z hello **DimDate** tabeli nadal aktywne w Konstruktorze modelu hello w siatce miar hello, kliknij przycisk hello pustej komórki poniżej miary hello został utworzony.</span><span class="sxs-lookup"><span data-stu-id="5c0d0-134">With hello **DimDate** table still active in hello model designer, in hello measure grid, click hello empty cell below hello measure you created.</span></span>  
  
2.  <span data-ttu-id="5c0d0-135">Na pasku formuły hello wpisz hello następującej formuły:</span><span class="sxs-lookup"><span data-stu-id="5c0d0-135">In hello formula bar, type hello following formula:</span></span>  
  
    ```
    DaysInCurrentQuarter:=COUNTROWS( DATESBETWEEN( 'DimDate'[Date], STARTOFQUARTER( LASTDATE('DimDate'[Date])), ENDOFQUARTER('DimDate'[Date])))
    ```
  
    <span data-ttu-id="5c0d0-136">Podczas tworzenia porównania proporcje jednego okresu niekompletne hello poprzedniego okresu.</span><span class="sxs-lookup"><span data-stu-id="5c0d0-136">When creating a comparison ratio between one incomplete period and hello previous period.</span></span> <span data-ttu-id="5c0d0-137">Formuła Hello należy obliczyć hello część hello okresu, który upłynął i porównania go toohello sam udział procentowy w hello poprzedniego okresu.</span><span class="sxs-lookup"><span data-stu-id="5c0d0-137">hello formula must calculate hello proportion of hello period that has elapsed and compare it toohello same proportion in hello previous period.</span></span> <span data-ttu-id="5c0d0-138">W tym przypadku [DaysCurrentQuarterToDate] / [DaysInCurrentQuarter] zapewnia hello udział, który upłynął w hello bieżącego okresu.</span><span class="sxs-lookup"><span data-stu-id="5c0d0-138">In this case, [DaysCurrentQuarterToDate]/[DaysInCurrentQuarter] gives hello proportion elapsed in hello current period.</span></span>  
  
#### <a name="toocreate-an-internetdistinctcountsalesorder-measure-in-hello-factinternetsales-table"></a><span data-ttu-id="5c0d0-139">toocreate środek InternetDistinctCountSalesOrder w Tabela FactInternetSales hello</span><span class="sxs-lookup"><span data-stu-id="5c0d0-139">toocreate an InternetDistinctCountSalesOrder measure in hello FactInternetSales table</span></span>  
  
1.  <span data-ttu-id="5c0d0-140">Kliknij przycisk hello **FactInternetSales** tabeli.</span><span class="sxs-lookup"><span data-stu-id="5c0d0-140">Click hello **FactInternetSales** table.</span></span>   
  
2.  <span data-ttu-id="5c0d0-141">Kliknij przycisk hello **SalesOrderNumber** nagłówek kolumny.</span><span class="sxs-lookup"><span data-stu-id="5c0d0-141">Click hello **SalesOrderNumber** column heading.</span></span>  
  
3.  <span data-ttu-id="5c0d0-142">Na pasku narzędzi hello, kliknij przycisk Dalej toohello Strzałka w dół hello Autosumowanie (**∑**) przycisk, a następnie wybierz **DistinctCount**.</span><span class="sxs-lookup"><span data-stu-id="5c0d0-142">On hello toolbar, click hello down-arrow next toohello AutoSum (**∑**) button, and then select **DistinctCount**.</span></span>  
  
    <span data-ttu-id="5c0d0-143">funkcja Autosumowania Hello automatycznie tworzy miary dla wybranej kolumny hello przy użyciu formuły standardowe agregacji DistinctCount hello.</span><span class="sxs-lookup"><span data-stu-id="5c0d0-143">hello AutoSum feature automatically creates a measure for hello selected column using hello DistinctCount standard aggregation formula.</span></span>  
    
       ![aas-lesson6-newmeasure2](../tutorials/media/aas-lesson6-newmeasure2.png)
  
4.  <span data-ttu-id="5c0d0-145">W siatce miar hello, kliknij przycisk hello nowej miary, a następnie w hello **właściwości** okna w **Nazwa miary**, zmiany nazwy miary hello zbyt**InternetDistinctCountSalesOrder**.</span><span class="sxs-lookup"><span data-stu-id="5c0d0-145">In hello measure grid, click hello new measure, and then in hello **Properties** window, in **Measure Name**, rename hello measure too**InternetDistinctCountSalesOrder**.</span></span> 
 
  
#### <a name="toocreate-additional-measures-in-hello-factinternetsales-table"></a><span data-ttu-id="5c0d0-146">dodatkowe środki toocreate w Tabela FactInternetSales hello</span><span class="sxs-lookup"><span data-stu-id="5c0d0-146">toocreate additional measures in hello FactInternetSales table</span></span>  
  
1.  <span data-ttu-id="5c0d0-147">Za pomocą funkcji Autosumowania hello, Utwórz i nazwa hello następujące miary:</span><span class="sxs-lookup"><span data-stu-id="5c0d0-147">By using hello AutoSum feature, create and name hello following measures:</span></span>  

    |<span data-ttu-id="5c0d0-148">Kolumna</span><span class="sxs-lookup"><span data-stu-id="5c0d0-148">Column</span></span>|<span data-ttu-id="5c0d0-149">Nazwa miary</span><span class="sxs-lookup"><span data-stu-id="5c0d0-149">Measure name</span></span>|<span data-ttu-id="5c0d0-150">Autosumowanie (∑)</span><span class="sxs-lookup"><span data-stu-id="5c0d0-150">AutoSum (∑)</span></span>|<span data-ttu-id="5c0d0-151">Formuła</span><span class="sxs-lookup"><span data-stu-id="5c0d0-151">Formula</span></span>|  
    |----------------|----------|-----------------|-----------|  
    |<span data-ttu-id="5c0d0-152">SalesOrderLineNumber</span><span class="sxs-lookup"><span data-stu-id="5c0d0-152">SalesOrderLineNumber</span></span>|<span data-ttu-id="5c0d0-153">InternetOrderLinesCount</span><span class="sxs-lookup"><span data-stu-id="5c0d0-153">InternetOrderLinesCount</span></span>|<span data-ttu-id="5c0d0-154">Licznik</span><span class="sxs-lookup"><span data-stu-id="5c0d0-154">Count</span></span>|<span data-ttu-id="5c0d0-155">=COUNTA([SalesOrderLineNumber])</span><span class="sxs-lookup"><span data-stu-id="5c0d0-155">=COUNTA([SalesOrderLineNumber])</span></span>|  
    |<span data-ttu-id="5c0d0-156">OrderQuantity</span><span class="sxs-lookup"><span data-stu-id="5c0d0-156">OrderQuantity</span></span>|<span data-ttu-id="5c0d0-157">InternetTotalUnits</span><span class="sxs-lookup"><span data-stu-id="5c0d0-157">InternetTotalUnits</span></span>|<span data-ttu-id="5c0d0-158">Suma</span><span class="sxs-lookup"><span data-stu-id="5c0d0-158">Sum</span></span>|<span data-ttu-id="5c0d0-159">=SUM([OrderQuantity])</span><span class="sxs-lookup"><span data-stu-id="5c0d0-159">=SUM([OrderQuantity])</span></span>|  
    |<span data-ttu-id="5c0d0-160">DiscountAmount</span><span class="sxs-lookup"><span data-stu-id="5c0d0-160">DiscountAmount</span></span>|<span data-ttu-id="5c0d0-161">InternetTotalDiscountAmount</span><span class="sxs-lookup"><span data-stu-id="5c0d0-161">InternetTotalDiscountAmount</span></span>|<span data-ttu-id="5c0d0-162">Suma</span><span class="sxs-lookup"><span data-stu-id="5c0d0-162">Sum</span></span>|<span data-ttu-id="5c0d0-163">=SUM([DiscountAmount])</span><span class="sxs-lookup"><span data-stu-id="5c0d0-163">=SUM([DiscountAmount])</span></span>|  
    |<span data-ttu-id="5c0d0-164">TotalProductCost</span><span class="sxs-lookup"><span data-stu-id="5c0d0-164">TotalProductCost</span></span>|<span data-ttu-id="5c0d0-165">InternetTotalProductCost</span><span class="sxs-lookup"><span data-stu-id="5c0d0-165">InternetTotalProductCost</span></span>|<span data-ttu-id="5c0d0-166">Suma</span><span class="sxs-lookup"><span data-stu-id="5c0d0-166">Sum</span></span>|<span data-ttu-id="5c0d0-167">=SUM([TotalProductCost])</span><span class="sxs-lookup"><span data-stu-id="5c0d0-167">=SUM([TotalProductCost])</span></span>|  
    |<span data-ttu-id="5c0d0-168">SalesAmount</span><span class="sxs-lookup"><span data-stu-id="5c0d0-168">SalesAmount</span></span>|<span data-ttu-id="5c0d0-169">InternetTotalSales</span><span class="sxs-lookup"><span data-stu-id="5c0d0-169">InternetTotalSales</span></span>|<span data-ttu-id="5c0d0-170">Suma</span><span class="sxs-lookup"><span data-stu-id="5c0d0-170">Sum</span></span>|<span data-ttu-id="5c0d0-171">=SUM([SalesAmount])</span><span class="sxs-lookup"><span data-stu-id="5c0d0-171">=SUM([SalesAmount])</span></span>|  
    |<span data-ttu-id="5c0d0-172">Margin</span><span class="sxs-lookup"><span data-stu-id="5c0d0-172">Margin</span></span>|<span data-ttu-id="5c0d0-173">InternetTotalMargin</span><span class="sxs-lookup"><span data-stu-id="5c0d0-173">InternetTotalMargin</span></span>|<span data-ttu-id="5c0d0-174">Suma</span><span class="sxs-lookup"><span data-stu-id="5c0d0-174">Sum</span></span>|<span data-ttu-id="5c0d0-175">=SUM([Margin])</span><span class="sxs-lookup"><span data-stu-id="5c0d0-175">=SUM([Margin])</span></span>|  
    |<span data-ttu-id="5c0d0-176">TaxAmt</span><span class="sxs-lookup"><span data-stu-id="5c0d0-176">TaxAmt</span></span>|<span data-ttu-id="5c0d0-177">InternetTotalTaxAmt</span><span class="sxs-lookup"><span data-stu-id="5c0d0-177">InternetTotalTaxAmt</span></span>|<span data-ttu-id="5c0d0-178">Suma</span><span class="sxs-lookup"><span data-stu-id="5c0d0-178">Sum</span></span>|<span data-ttu-id="5c0d0-179">=SUM([TaxAmt])</span><span class="sxs-lookup"><span data-stu-id="5c0d0-179">=SUM([TaxAmt])</span></span>|  
    |<span data-ttu-id="5c0d0-180">Freight</span><span class="sxs-lookup"><span data-stu-id="5c0d0-180">Freight</span></span>|<span data-ttu-id="5c0d0-181">InternetTotalFreight</span><span class="sxs-lookup"><span data-stu-id="5c0d0-181">InternetTotalFreight</span></span>|<span data-ttu-id="5c0d0-182">Suma</span><span class="sxs-lookup"><span data-stu-id="5c0d0-182">Sum</span></span>|<span data-ttu-id="5c0d0-183">=SUM([Freight])</span><span class="sxs-lookup"><span data-stu-id="5c0d0-183">=SUM([Freight])</span></span>|  
  
2.  <span data-ttu-id="5c0d0-184">Klikając przycisk Utwórz pustej komórki w siatce miar hello i za pomocą hello pasku formuły, i nazwę hello następujące środki w kolejności:</span><span class="sxs-lookup"><span data-stu-id="5c0d0-184">By clicking an empty cell in hello measure grid, and by using hello formula bar, create, and name hello following measures in order:</span></span>  
  
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
  
<span data-ttu-id="5c0d0-185">Środki utworzone dla Tabela FactInternetSales hello mogą być używane tooanalyze krytyczne dane finansowe takie jak sprzedaż, kosztów i marża dla elementów zdefiniowanych przez wybrany filtr użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="5c0d0-185">Measures created for hello FactInternetSales table can be used tooanalyze critical financial data such as sales, costs, and profit margin for items defined by hello user selected filter.</span></span>  
  
## <a name="whats-next"></a><span data-ttu-id="5c0d0-186">Co dalej?</span><span class="sxs-lookup"><span data-stu-id="5c0d0-186">What's next?</span></span>
<span data-ttu-id="5c0d0-187">[Lekcja 7. Tworzenie kluczowych wskaźników wydajności](../tutorials/aas-lesson-7-create-key-performance-indicators.md).</span><span class="sxs-lookup"><span data-stu-id="5c0d0-187">[Lesson 7: Create Key Performance Indicators](../tutorials/aas-lesson-7-create-key-performance-indicators.md).</span></span>  

  
