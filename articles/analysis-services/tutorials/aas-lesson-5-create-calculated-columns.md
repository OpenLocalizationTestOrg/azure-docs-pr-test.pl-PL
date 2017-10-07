---
<span data-ttu-id="5edf2-101">title: aaa "lekcji samouczka usług Azure Analysis Services 5: Tworzenie kolumn obliczeniowych | Opis elementu Microsoft Docs": w tym artykule opisano, jak toocreate obliczane kolumny w projekcie samouczek hello Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="5edf2-101">title: aaa"Azure Analysis Services tutorial lesson 5: Create calculated columns | Microsoft Docs" description: Describes how toocreate calculated columns in hello Azure Analysis Services tutorial project.</span></span> <span data-ttu-id="5edf2-102">usługi: documentationcenter usług analysis services: "Autor: minewiskan Menedżera: Edytor erikre:" tagów: "</span><span class="sxs-lookup"><span data-stu-id="5edf2-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="5edf2-103">MS.AssetID: ms.service: ms.devlang usług analysis services: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: ms.author 2017-06/01: owend</span><span class="sxs-lookup"><span data-stu-id="5edf2-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 06/01/2017 ms.author: owend</span></span>
---
# <a name="lesson-5-create-calculated-columns"></a><span data-ttu-id="5edf2-104">Lekcja 5. Tworzenie kolumn obliczeniowych</span><span class="sxs-lookup"><span data-stu-id="5edf2-104">Lesson 5: Create calculated columns</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="5edf2-105">W tej lekcji utworzysz dane w modelu przez dodanie kolumn obliczeniowych.</span><span class="sxs-lookup"><span data-stu-id="5edf2-105">In this lesson, you create data in your model by adding calculated columns.</span></span> <span data-ttu-id="5edf2-106">Można utworzyć kolumny obliczeniowej (jako kolumny niestandardowe) podczas korzystania z pobieranie danych, za pomocą hello edytora zapytań, lub później w notacji projektanta hello modelu można to zrobić na stronie.</span><span class="sxs-lookup"><span data-stu-id="5edf2-106">You can create calculated columns (as custom columns) when using Get Data, by using hello Query Editor, or later in hello model designer like you do here.</span></span> <span data-ttu-id="5edf2-107">toolearn więcej, zobacz [kolumn obliczeniowych](https://docs.microsoft.com/sql/analysis-services/tabular-models/ssas-calculated-columns).</span><span class="sxs-lookup"><span data-stu-id="5edf2-107">toolearn more, see [Calculated columns](https://docs.microsoft.com/sql/analysis-services/tabular-models/ssas-calculated-columns).</span></span>
  
<span data-ttu-id="5edf2-108">Zostanie utworzonych pięć nowych kolumn obliczeniowych w trzech różnych tabelach.</span><span class="sxs-lookup"><span data-stu-id="5edf2-108">You create five new calculated columns in three different tables.</span></span> <span data-ttu-id="5edf2-109">kroki Hello są nieco inne dla każdego zadania istnieje kilka sposobów toocreate kolumn, zmień ich oraz umieścić je w różnych miejscach w tabeli.</span><span class="sxs-lookup"><span data-stu-id="5edf2-109">hello steps are slightly different for each task showing there are several ways toocreate columns, rename them, and place them in various locations in a table.</span></span>  

<span data-ttu-id="5edf2-110">W tej lekcji po raz pierwszy zostanie użyty język DAX (Data Analysis Expresions).</span><span class="sxs-lookup"><span data-stu-id="5edf2-110">This lesson is also where you first use Data Analysis Expressions (DAX).</span></span> <span data-ttu-id="5edf2-111">DAX to specjalny język przeznaczony do tworzenia wyrażeń formuł dla modeli tabelarycznych, które można w wysokim stopniu dostosowywać.</span><span class="sxs-lookup"><span data-stu-id="5edf2-111">DAX is a special language for creating highly customizable formula expressions for tabular models.</span></span> <span data-ttu-id="5edf2-112">W tym samouczku użyjesz kolumny obliczane toocreate, miary i roli filtry języka DAX.</span><span class="sxs-lookup"><span data-stu-id="5edf2-112">In this tutorial, you use DAX toocreate calculated columns, measures, and role filters.</span></span> <span data-ttu-id="5edf2-113">toolearn więcej, zobacz [DAX w modelach tabelarycznym](https://docs.microsoft.com/sql/analysis-services/tabular-models/understanding-dax-in-tabular-models-ssas-tabular).</span><span class="sxs-lookup"><span data-stu-id="5edf2-113">toolearn more, see [DAX in tabular models](https://docs.microsoft.com/sql/analysis-services/tabular-models/understanding-dax-in-tabular-models-ssas-tabular).</span></span> 
  
<span data-ttu-id="5edf2-114">Szacowany czas toocomplete tej lekcji: **15 minut**</span><span class="sxs-lookup"><span data-stu-id="5edf2-114">Estimated time toocomplete this lesson: **15 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="5edf2-115">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="5edf2-115">Prerequisites</span></span>  
<span data-ttu-id="5edf2-116">Ten temat stanowi część samouczka modelowania tabelarycznego, który należy wykonać w podanej kolejności.</span><span class="sxs-lookup"><span data-stu-id="5edf2-116">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="5edf2-117">Przed wykonaniem zadania hello w tej lekcji, powinno mieć ukończone poprzedniej lekcji hello: [lekcji 4: tworzenie relacji](../tutorials/aas-lesson-4-create-relationships.md).</span><span class="sxs-lookup"><span data-stu-id="5edf2-117">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 4: Create relationships](../tutorials/aas-lesson-4-create-relationships.md).</span></span> 
  
## <a name="create-calculated-columns"></a><span data-ttu-id="5edf2-118">Tworzenie kolumn obliczeniowych</span><span class="sxs-lookup"><span data-stu-id="5edf2-118">Create calculated columns</span></span>  
  
#### <a name="create-a-monthcalendar-calculated-column-in-hello-dimdate-table"></a><span data-ttu-id="5edf2-119">Utwórz pole obliczeniowe MonthCalendar w tabeli DimDate hello</span><span class="sxs-lookup"><span data-stu-id="5edf2-119">Create a MonthCalendar calculated column in hello DimDate table</span></span>  
  
1.  <span data-ttu-id="5edf2-120">Kliknij przycisk hello **modelu** menu > **widok modelu** > **widoku danych**.</span><span class="sxs-lookup"><span data-stu-id="5edf2-120">Click hello **Model** menu > **Model View** > **Data View**.</span></span>  
  
    <span data-ttu-id="5edf2-121">Kolumn obliczanych można tworzyć tylko za pomocą projektanta modelu hello w widoku danych.</span><span class="sxs-lookup"><span data-stu-id="5edf2-121">Calculated columns can only be created by using hello model designer in Data View.</span></span>  
  
2.  <span data-ttu-id="5edf2-122">W Konstruktorze modelu powitania kliknij hello **DimDate** tabeli (karta).</span><span class="sxs-lookup"><span data-stu-id="5edf2-122">In hello model designer, click hello **DimDate** table (tab).</span></span>  
  
3.  <span data-ttu-id="5edf2-123">Kliknij prawym przyciskiem myszy hello **CalendarQuarter** nagłówek kolumny, a następnie kliknij przycisk **Wstaw kolumnę**.</span><span class="sxs-lookup"><span data-stu-id="5edf2-123">Right-click hello **CalendarQuarter** column header, and then click **Insert Column**.</span></span>  
  
    <span data-ttu-id="5edf2-124">Nową kolumnę o nazwie **kolumna obliczana 1** jest toohello wstawiony po lewej hello **kwartału** kolumny.</span><span class="sxs-lookup"><span data-stu-id="5edf2-124">A new column named **Calculated Column 1** is inserted toohello left of hello **Calendar Quarter** column.</span></span>  
  
4.  <span data-ttu-id="5edf2-125">Na pasku formuły hello powyżej hello tabeli, wpisz hello następującej formuły języka DAX: pomaga autouzupełniania wpisania hello w pełni kwalifikowane nazwy kolumn i tabel i list hello funkcje, które są dostępne.</span><span class="sxs-lookup"><span data-stu-id="5edf2-125">In hello formula bar above hello table, type hello following DAX formula: AutoComplete helps you type hello fully qualified names of columns and tables, and lists hello functions that are available.</span></span>  
  
    ```  
    =RIGHT(" " & FORMAT([MonthNumberOfYear],"#0"), 2) & " - " & [EnglishMonthName]  
    ``` 
  
    <span data-ttu-id="5edf2-126">Dla wszystkich wierszy hello w kolumnie obliczeniowej hello jest następnie zapełniana wartościami.</span><span class="sxs-lookup"><span data-stu-id="5edf2-126">Values are then populated for all hello rows in hello calculated column.</span></span> <span data-ttu-id="5edf2-127">Jeśli przewijania w dół hello tabeli, zobacz wiersze mogą mieć różne wartości dla tej kolumny, na podstawie danych hello w każdym wierszu.</span><span class="sxs-lookup"><span data-stu-id="5edf2-127">If you scroll down through hello table, you see rows can have different values for this column, based on hello data in each row.</span></span>    
  
5.  <span data-ttu-id="5edf2-128">Zmień nazwę tej kolumny zbyt**MonthCalendar**.</span><span class="sxs-lookup"><span data-stu-id="5edf2-128">Rename this column too**MonthCalendar**.</span></span> 

    ![aas-lesson5-newcolumn](../tutorials/media/aas-lesson5-newcolumn.png) 
  
<span data-ttu-id="5edf2-130">kolumna obliczeniowa MonthCalendar Hello zawiera nazwę sortowania dla miesiąca.</span><span class="sxs-lookup"><span data-stu-id="5edf2-130">hello MonthCalendar calculated column provides a sortable name for Month.</span></span>  
  
#### <a name="create-a-dayofweek-calculated-column-in-hello-dimdate-table"></a><span data-ttu-id="5edf2-131">Utwórz pole obliczeniowe DayOfWeek w tabeli DimDate hello</span><span class="sxs-lookup"><span data-stu-id="5edf2-131">Create a DayOfWeek calculated column in hello DimDate table</span></span>  
  
1.  <span data-ttu-id="5edf2-132">Z hello **DimDate** tabeli nadal aktywne, kliknij przycisk hello **kolumny** menu, a następnie kliknij przycisk **Dodaj kolumnę**.</span><span class="sxs-lookup"><span data-stu-id="5edf2-132">With hello **DimDate** table still active, click hello **Column** menu, and then click **Add Column**.</span></span>  
  
2.  <span data-ttu-id="5edf2-133">Na pasku formuły hello wpisz hello następującej formuły:</span><span class="sxs-lookup"><span data-stu-id="5edf2-133">In hello formula bar, type hello following formula:</span></span>  
    
    ```
    =RIGHT(" " & FORMAT([DayNumberOfWeek],"#0"), 2) & " - " & [EnglishDayNameOfWeek]  
    ```
    
    <span data-ttu-id="5edf2-134">Po zakończeniu tworzenia hello formuły, naciśnij klawisz ENTER.</span><span class="sxs-lookup"><span data-stu-id="5edf2-134">When you've finished building hello formula, press ENTER.</span></span> <span data-ttu-id="5edf2-135">Kolumna Hello zostanie dodana toohello prawej tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="5edf2-135">hello new column is added toohello far right of hello table.</span></span>  
  
3.  <span data-ttu-id="5edf2-136">Zmień nazwę kolumny hello zbyt**DayOfWeek**.</span><span class="sxs-lookup"><span data-stu-id="5edf2-136">Rename hello column too**DayOfWeek**.</span></span>  
  
4.  <span data-ttu-id="5edf2-137">Kliknij nagłówek kolumny hello, a następnie przeciągnij kolumny hello między hello **EnglishDayNameOfWeek** kolumny i hello **DayNumberOfMonth** kolumny.</span><span class="sxs-lookup"><span data-stu-id="5edf2-137">Click hello column heading, and then drag hello column between hello **EnglishDayNameOfWeek** column and hello **DayNumberOfMonth** column.</span></span>  
  
    > [!TIP]  
    > <span data-ttu-id="5edf2-138">Przenoszenie kolumn w tabeli umożliwia łatwiejsze toonavigate.</span><span class="sxs-lookup"><span data-stu-id="5edf2-138">Moving columns in your table makes it easier toonavigate.</span></span>  
  
<span data-ttu-id="5edf2-139">kolumna obliczeniowa DayOfWeek Hello poda nazwę sortowania hello dzień tygodnia.</span><span class="sxs-lookup"><span data-stu-id="5edf2-139">hello DayOfWeek calculated column provides a sortable name for hello day of week.</span></span>  
  
#### <a name="create-a-productsubcategoryname-calculated-column-in-hello-dimproduct-table"></a><span data-ttu-id="5edf2-140">Utwórz pole obliczeniowe ProductSubcategoryName w tabeli DimProduct hello</span><span class="sxs-lookup"><span data-stu-id="5edf2-140">Create a ProductSubcategoryName calculated column in hello DimProduct table</span></span>  
  
  
1.  <span data-ttu-id="5edf2-141">W hello **DimProduct** tabeli, przewiń toohello prawej krawędzi tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="5edf2-141">In hello **DimProduct** table, scroll toohello far right of hello table.</span></span> <span data-ttu-id="5edf2-142">Powiadomienie hello prawej kolumna nosiła nazwę **Dodaj kolumnę** (kursywą), kliknij nagłówek kolumny hello.</span><span class="sxs-lookup"><span data-stu-id="5edf2-142">Notice hello right-most column is named **Add Column** (italicized), click hello column heading.</span></span>  
  
2.  <span data-ttu-id="5edf2-143">Na pasku formuły hello wpisz hello następującej formuły:</span><span class="sxs-lookup"><span data-stu-id="5edf2-143">In hello formula bar, type hello following formula:</span></span>  
    
    ```
    =RELATED('DimProductSubcategory'[EnglishProductSubcategoryName])  
    ```
  
3.  <span data-ttu-id="5edf2-144">Zmień nazwę kolumny hello zbyt**ProductSubcategoryName**.</span><span class="sxs-lookup"><span data-stu-id="5edf2-144">Rename hello column too**ProductSubcategoryName**.</span></span>  
  
<span data-ttu-id="5edf2-145">kolumny obliczeniowej ProductSubcategoryName Hello jest używany toocreate hierarchii w tabeli DimProduct hello, która zawiera dane z hello EnglishProductSubcategoryName kolumny w tabeli DimProductSubcategory hello.</span><span class="sxs-lookup"><span data-stu-id="5edf2-145">hello ProductSubcategoryName calculated column is used toocreate a hierarchy in hello DimProduct table, which includes data from hello EnglishProductSubcategoryName column in hello DimProductSubcategory table.</span></span> <span data-ttu-id="5edf2-146">Hierarchie mogą obejmować maksymalnie jedną tabelę.</span><span class="sxs-lookup"><span data-stu-id="5edf2-146">Hierarchies cannot span more than one table.</span></span> <span data-ttu-id="5edf2-147">Hierarchie zostaną utworzone później, w lekcji 9.</span><span class="sxs-lookup"><span data-stu-id="5edf2-147">You create hierarchies later in Lesson 9.</span></span>  
  
#### <a name="create-a-productcategoryname-calculated-column-in-hello-dimproduct-table"></a><span data-ttu-id="5edf2-148">Utwórz pole obliczeniowe ProductCategoryName w tabeli DimProduct hello</span><span class="sxs-lookup"><span data-stu-id="5edf2-148">Create a ProductCategoryName calculated column in hello DimProduct table</span></span>  
  
1.  <span data-ttu-id="5edf2-149">Z hello **DimProduct** tabeli nadal aktywne, kliknij przycisk hello **kolumny** menu, a następnie kliknij przycisk **Dodaj kolumnę**.</span><span class="sxs-lookup"><span data-stu-id="5edf2-149">With hello **DimProduct** table still active, click hello **Column** menu, and then click **Add Column**.</span></span>  
  
2.  <span data-ttu-id="5edf2-150">Na pasku formuły hello wpisz hello następującej formuły:</span><span class="sxs-lookup"><span data-stu-id="5edf2-150">In hello formula bar, type hello following formula:</span></span>  
  
    ```
    =RELATED('DimProductCategory'[EnglishProductCategoryName]) 
    ```
    
3.  <span data-ttu-id="5edf2-151">Zmień nazwę kolumny hello zbyt**ProductCategoryName**.</span><span class="sxs-lookup"><span data-stu-id="5edf2-151">Rename hello column too**ProductCategoryName**.</span></span>  
  
<span data-ttu-id="5edf2-152">kolumny obliczeniowej ProductCategoryName Hello jest używany toocreate hierarchii w tabeli DimProduct hello, która zawiera dane z hello EnglishProductCategoryName kolumny w tabeli DimProductCategory hello.</span><span class="sxs-lookup"><span data-stu-id="5edf2-152">hello ProductCategoryName calculated column is used toocreate a hierarchy in hello DimProduct table, which includes data from hello EnglishProductCategoryName column in hello DimProductCategory table.</span></span> <span data-ttu-id="5edf2-153">Hierarchie mogą obejmować maksymalnie jedną tabelę.</span><span class="sxs-lookup"><span data-stu-id="5edf2-153">Hierarchies cannot span more than one table.</span></span>  
  
#### <a name="create-a-margin-calculated-column-in-hello-factinternetsales-table"></a><span data-ttu-id="5edf2-154">Utwórz pole obliczeniowe margines w Tabela FactInternetSales hello</span><span class="sxs-lookup"><span data-stu-id="5edf2-154">Create a Margin calculated column in hello FactInternetSales table</span></span>  
  
1.  <span data-ttu-id="5edf2-155">Projektant modelu hello, wybierz hello **FactInternetSales** tabeli.</span><span class="sxs-lookup"><span data-stu-id="5edf2-155">In hello model designer, select hello **FactInternetSales** table.</span></span>  
  
2.  <span data-ttu-id="5edf2-156">Utwórz nową kolumnę obliczeniową między hello **kwoty sprzedaży** kolumny i hello **TaxAmt** kolumny.</span><span class="sxs-lookup"><span data-stu-id="5edf2-156">Create a new calculated column between hello **SalesAmount** column and hello **TaxAmt** column.</span></span>  
  
3.  <span data-ttu-id="5edf2-157">Na pasku formuły hello wpisz hello następującej formuły:</span><span class="sxs-lookup"><span data-stu-id="5edf2-157">In hello formula bar, type hello following formula:</span></span>  
  
    ```
    =[SalesAmount]-[TotalProductCost]
    ``` 

4.  <span data-ttu-id="5edf2-158">Zmień nazwę kolumny hello zbyt**margines**.</span><span class="sxs-lookup"><span data-stu-id="5edf2-158">Rename hello column too**Margin**.</span></span>  
 
      ![aas-lesson5-newmargin](../tutorials/media/aas-lesson5-newmargin.png)
      
    <span data-ttu-id="5edf2-160">kolumny obliczeniowej margines Hello jest używany tooanalyze marży dla każdej sprzedaży.</span><span class="sxs-lookup"><span data-stu-id="5edf2-160">hello Margin calculated column is used tooanalyze profit margins for each sale.</span></span>  
  
## <a name="whats-next"></a><span data-ttu-id="5edf2-161">Co dalej?</span><span class="sxs-lookup"><span data-stu-id="5edf2-161">What's next?</span></span>
<span data-ttu-id="5edf2-162">[Lekcja 6. Tworzenie miar](../tutorials/aas-lesson-6-create-measures.md).</span><span class="sxs-lookup"><span data-stu-id="5edf2-162">[Lesson 6: Create measures](../tutorials/aas-lesson-6-create-measures.md).</span></span>
  
  
  
