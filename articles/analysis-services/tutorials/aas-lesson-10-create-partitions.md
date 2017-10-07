---
<span data-ttu-id="3b81f-101">title: aaa "lekcji samouczka usług Azure Analysis Services 10: tworzenie partycji | Opis elementu Microsoft Docs": w tym artykule opisano, jak toocreate partycje w projekcie samouczek hello Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="3b81f-101">title: aaa"Azure Analysis Services tutorial lesson 10: Create partitions | Microsoft Docs" description: Describes how toocreate partitions in hello Azure Analysis Services tutorial project.</span></span> <span data-ttu-id="3b81f-102">usługi: documentationcenter usług analysis services: "Autor: minewiskan Menedżera: Edytor erikre:" tagów: "</span><span class="sxs-lookup"><span data-stu-id="3b81f-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="3b81f-103">MS.AssetID: ms.service: ms.devlang usług analysis services: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend</span><span class="sxs-lookup"><span data-stu-id="3b81f-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend</span></span>
---
# <a name="lesson-10-create-partitions"></a><span data-ttu-id="3b81f-104">Lekcja 10. Tworzenie partycji</span><span class="sxs-lookup"><span data-stu-id="3b81f-104">Lesson 10: Create partitions</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="3b81f-105">W tej lekcji zostanie utworzona tabela FactInternetSales hello toodivide partycji na mniejsze części logiczne, które mogą być przetworzone (odświeżyć) niezależnie od innych partycji.</span><span class="sxs-lookup"><span data-stu-id="3b81f-105">In this lesson, you create partitions toodivide hello FactInternetSales table into smaller logical parts that can be processed (refreshed) independent of other partitions.</span></span> <span data-ttu-id="3b81f-106">Domyślnie w każdej tabeli, który można dołączyć do modelu ma jedną partycję, która obejmuje wszystkie tabeli hello kolumn i wierszy.</span><span class="sxs-lookup"><span data-stu-id="3b81f-106">By default, every table you include in your model has one partition, which includes all hello table’s columns and rows.</span></span> <span data-ttu-id="3b81f-107">Dla Tabela FactInternetSales hello chcemy toodivide hello danych przez rok; jedna partycja dla każdego z pięciu lat. hello tabeli.</span><span class="sxs-lookup"><span data-stu-id="3b81f-107">For hello FactInternetSales table, we want toodivide hello data by year; one partition for each of hello table’s five years.</span></span> <span data-ttu-id="3b81f-108">Każda partycja będzie mogła być przetwarzana niezależnie.</span><span class="sxs-lookup"><span data-stu-id="3b81f-108">Each partition can then be processed independently.</span></span> <span data-ttu-id="3b81f-109">toolearn więcej, zobacz [partycji](https://docs.microsoft.com/sql/analysis-services/tabular-models/partitions-ssas-tabular).</span><span class="sxs-lookup"><span data-stu-id="3b81f-109">toolearn more, see [Partitions](https://docs.microsoft.com/sql/analysis-services/tabular-models/partitions-ssas-tabular).</span></span> 
  
<span data-ttu-id="3b81f-110">Szacowany czas toocomplete tej lekcji: **15 minut**</span><span class="sxs-lookup"><span data-stu-id="3b81f-110">Estimated time toocomplete this lesson: **15 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="3b81f-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="3b81f-111">Prerequisites</span></span>  
<span data-ttu-id="3b81f-112">Ten temat stanowi część samouczka modelowania tabelarycznego, który należy wykonać w podanej kolejności.</span><span class="sxs-lookup"><span data-stu-id="3b81f-112">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="3b81f-113">Przed wykonaniem zadania hello w tej lekcji, powinno mieć ukończone poprzedniej lekcji hello: [lekcji 9: tworzenia hierarchii](../tutorials/aas-lesson-9-create-hierarchies.md).</span><span class="sxs-lookup"><span data-stu-id="3b81f-113">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 9: Create Hierarchies](../tutorials/aas-lesson-9-create-hierarchies.md).</span></span>  
  
## <a name="create-partitions"></a><span data-ttu-id="3b81f-114">Tworzenie partycji</span><span class="sxs-lookup"><span data-stu-id="3b81f-114">Create partitions</span></span>  
  
#### <a name="toocreate-partitions-in-hello-factinternetsales-table"></a><span data-ttu-id="3b81f-115">partycje toocreate w Tabela FactInternetSales hello</span><span class="sxs-lookup"><span data-stu-id="3b81f-115">toocreate partitions in hello FactInternetSales table</span></span>  
  
1.  <span data-ttu-id="3b81f-116">W Eksploratorze modeli tabelarycznych rozwiń węzeł **Tabele**, a następnie kliknij prawym przyciskiem myszy pozycje **FactInternetSales** > **Partycje**.</span><span class="sxs-lookup"><span data-stu-id="3b81f-116">In Tabular Model Explorer, expand **Tables**, and then right-click **FactInternetSales** > **Partitions**.</span></span>  
  
2.  <span data-ttu-id="3b81f-117">W Menedżerze partycji kliknij **kopiowania**, a następnie zmień nazwę hello zbyt**FactInternetSales2010**.</span><span class="sxs-lookup"><span data-stu-id="3b81f-117">In Partition Manager, click **Copy**, and then change hello name too**FactInternetSales2010**.</span></span>
  
    <span data-ttu-id="3b81f-118">Ponieważ tooinclude partycji hello tylko tych wierszy, które w określonym czasie, dla roku hello 2010, należy zmodyfikować hello wyrażenia zapytania.</span><span class="sxs-lookup"><span data-stu-id="3b81f-118">Because you want hello partition tooinclude only those rows within a certain period, for hello year 2010, you must modify hello query expression.</span></span>
  
4.  <span data-ttu-id="3b81f-119">Kliknij przycisk **projekt** tooopen edytora zapytań, a następnie kliknij przycisk hello **FactInternetSales2010** zapytania.</span><span class="sxs-lookup"><span data-stu-id="3b81f-119">Click **Design** tooopen Query Editor, and then click hello **FactInternetSales2010** query.</span></span>

5.  <span data-ttu-id="3b81f-120">W wersji zapoznawczej, kliknij przycisk hello strzałkę w hello **OrderDate** nagłówek kolumny, a następnie kliknij przycisk **filtry daty/godziny** > **między**.</span><span class="sxs-lookup"><span data-stu-id="3b81f-120">In preview, click hello down arrow in hello **OrderDate** column heading, and then click **Date/Time Filters** > **Between**.</span></span>

    ![aas-lesson10-query-editor](../tutorials/media/aas-lesson10-query-editor.png)

6.  <span data-ttu-id="3b81f-122">Okno dialogowe Filtr wierszy hello w **Pokaż wiersze, w których: OrderDate**, pozostaw **wypada po lub w dniu**, a następnie w polu Data hello, wprowadź **2010-1-1**.</span><span class="sxs-lookup"><span data-stu-id="3b81f-122">In hello Filter Rows dialog box, in **Show rows where: OrderDate**, leave **is after or equal to**, and then in hello date field, enter **1/1/2010**.</span></span> <span data-ttu-id="3b81f-123">Pozostaw hello **i** operator zaznaczone, następnie wybierz **przed**, następnie w polu Data hello, wprowadź **2011-1-1**, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="3b81f-123">Leave hello **And** operator selected, then select **is before**, then in hello date field, enter **1/1/2011**, and then click **OK**.</span></span>

    ![aas-lesson10-filter-rows](../tutorials/media/aas-lesson10-filter-rows.png)
    
    <span data-ttu-id="3b81f-125">Zwróć uwagę, że w części ZASTOSOWANE KROKI w Edytorze zapytań widać kolejny krok o nazwie Przefiltrowano wiersze.</span><span class="sxs-lookup"><span data-stu-id="3b81f-125">Notice in Query Editor, in APPLIED STEPS, you see another step named Filtered Rows.</span></span> <span data-ttu-id="3b81f-126">Ten filtr jest tylko dat zamówienia tooselect z 2010.</span><span class="sxs-lookup"><span data-stu-id="3b81f-126">This filter is tooselect only order dates from 2010.</span></span>

8.  <span data-ttu-id="3b81f-127">Kliknij przycisk **Importuj**.</span><span class="sxs-lookup"><span data-stu-id="3b81f-127">Click **Import**.</span></span>

    <span data-ttu-id="3b81f-128">W Menedżerze partycji zauważyć zapytań hello teraz wyrażenie ma dodatkowe klauzuli filtrowane wierszy.</span><span class="sxs-lookup"><span data-stu-id="3b81f-128">In Partition Manager, notice hello query expression now has an additional Filtered Rows clause.</span></span>

    ![aas-lesson10-query](../tutorials/media/aas-lesson10-query.png)
  
    <span data-ttu-id="3b81f-130">Ta partycja powinna zawierać tylko dane hello w tych wierszach, w którym hello OrderDate trwa hello 2010 roku kalendarzowym, jak określono w klauzuli filtrowane wiersze hello określa tej instrukcji.</span><span class="sxs-lookup"><span data-stu-id="3b81f-130">This statement specifies this partition should include only hello data in those rows where hello OrderDate is in hello 2010 calendar year as specified in hello filtered rows clause.</span></span>  
  
  
#### <a name="toocreate-a-partition-for-hello-2011-year"></a><span data-ttu-id="3b81f-131">toocreate partycji dla hello 2011 roku</span><span class="sxs-lookup"><span data-stu-id="3b81f-131">toocreate a partition for hello 2011 year</span></span>  
  
1.  <span data-ttu-id="3b81f-132">Powitania kliknij na liście partycji hello **FactInternetSales2010** partycji utworzony, a następnie kliknij przycisk **kopiowania**.</span><span class="sxs-lookup"><span data-stu-id="3b81f-132">In hello partitions list, click hello **FactInternetSales2010** partition you created, and then click **Copy**.</span></span>  <span data-ttu-id="3b81f-133">Zmień nazwę partycji hello zbyt**FactInternetSales2011**.</span><span class="sxs-lookup"><span data-stu-id="3b81f-133">Change hello partition name too**FactInternetSales2011**.</span></span> 

    <span data-ttu-id="3b81f-134">Nie trzeba toouse toocreate edytora zapytań nową klauzulę filtrowane wiersze.</span><span class="sxs-lookup"><span data-stu-id="3b81f-134">You do not need toouse Query Editor toocreate a new filtered rows clause.</span></span> <span data-ttu-id="3b81f-135">Ponieważ utworzono kopię zapytania hello 2010 toodo wystarczy wprowadzić zmianę nieznaczne w zapytaniu hello 2011 dla.</span><span class="sxs-lookup"><span data-stu-id="3b81f-135">Because you created a copy of hello query for 2010, all you need toodo is make a slight change in hello query for 2011.</span></span>
  
2.  <span data-ttu-id="3b81f-136">W **wyrażenia zapytania**, w kolejności dla tej partycji tooinclude tylko te wiersze hello 2011 roku, Zastąp hello lat w klauzuli filtrowane wiersze hello z **2011** i **2012**, takich jak:</span><span class="sxs-lookup"><span data-stu-id="3b81f-136">In **Query Expression**, in-order for this partition tooinclude only those rows for hello 2011 year, replace hello years in hello Filtered Rows clause with **2011** and **2012**, respectively, like:</span></span>  
  
    ```  
    let
        Source = #"SQL/localhost;AdventureWorksDW2014",
        dbo_FactInternetSales = Source{[Schema="dbo",Item="FactInternetSales"]}[Data],
        #"Removed Columns" = Table.RemoveColumns(dbo_FactInternetSales,{"OrderDateKey", "DueDateKey", "ShipDateKey"}),
        #"Filtered Rows" = Table.SelectRows(#"Removed Columns", each [OrderDate] >= #datetime(2011, 1, 1, 0, 0, 0) and [OrderDate] < #datetime(2012, 1, 1, 0, 0, 0))
    in
        #"Filtered Rows"
   
    ```  
  
#### <a name="toocreate-partitions-for-2012-2013-and-2014"></a><span data-ttu-id="3b81f-137">partycje toocreate 2012, 2013 i 2014 r.</span><span class="sxs-lookup"><span data-stu-id="3b81f-137">toocreate partitions for 2012, 2013, and 2014.</span></span>  
  
- <span data-ttu-id="3b81f-138">Wykonaj hello poprzednie kroki, tworzenie partycji 2012, 2013 i 2014 r., zmiana hello lat hello filtrowane wierszy klauzuli tooinclude tylko wiersze w roku.</span><span class="sxs-lookup"><span data-stu-id="3b81f-138">Follow hello previous steps, creating partitions for 2012, 2013, and 2014, changing hello years in hello Filtered Rows clause tooinclude only rows for that year.</span></span> 
  

## <a name="delete-hello-factinternetsales-partition"></a><span data-ttu-id="3b81f-139">Usuń hello FactInternetSales partycji</span><span class="sxs-lookup"><span data-stu-id="3b81f-139">Delete hello FactInternetSales partition</span></span>
<span data-ttu-id="3b81f-140">Teraz, gdy masz partycji dla każdego roku, można usunąć partycji FactInternetSales hello; w przypadku wybrania przetwórz wszystkie podczas przetwarzania partycji, co uniemożliwia nakładają się na siebie.</span><span class="sxs-lookup"><span data-stu-id="3b81f-140">Now that you have partitions for each year, you can delete hello FactInternetSales partition; preventing overlap when choosing Process all when processing partitions.</span></span>

#### <a name="toodelete-hello-factinternetsales-partition"></a><span data-ttu-id="3b81f-141">Witaj toodelete FactInternetSales partycji</span><span class="sxs-lookup"><span data-stu-id="3b81f-141">toodelete hello FactInternetSales partition</span></span>
-  <span data-ttu-id="3b81f-142">Kliknij hello FactInternetSales partycji, a następnie kliknij przycisk **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="3b81f-142">Click hello FactInternetSales partition, and then click **Delete**.</span></span>



## <a name="process-partitions"></a><span data-ttu-id="3b81f-143">Przetwarzanie partycji</span><span class="sxs-lookup"><span data-stu-id="3b81f-143">Process partitions</span></span>  
<span data-ttu-id="3b81f-144">W Menedżerze partycji zauważyć hello **ostatniego przetwarzania** kolumny dla wszystkich nowych partycji hello utworzone przedstawiono te partycje nigdy nie zostaną przetworzone.</span><span class="sxs-lookup"><span data-stu-id="3b81f-144">In Partition Manager, notice hello **Last Processed** column for each of hello new partitions you created shows these partitions have never been processed.</span></span> <span data-ttu-id="3b81f-145">Podczas tworzenia partycji, należy uruchomić partycje procesu lub proces tabeli operacji toorefresh hello danych w tych partycji.</span><span class="sxs-lookup"><span data-stu-id="3b81f-145">When you create partitions, you should run a Process Partitions or Process Table operation toorefresh hello data in those partitions.</span></span>  
  
#### <a name="tooprocess-hello-factinternetsales-partitions"></a><span data-ttu-id="3b81f-146">tooprocess hello FactInternetSales partycji</span><span class="sxs-lookup"><span data-stu-id="3b81f-146">tooprocess hello FactInternetSales partitions</span></span>  
  
1.  <span data-ttu-id="3b81f-147">Kliknij przycisk **OK** tooclose Menedżera partycji.</span><span class="sxs-lookup"><span data-stu-id="3b81f-147">Click **OK** tooclose Partition Manager.</span></span>  
  
2.  <span data-ttu-id="3b81f-148">Kliknij przycisk hello **FactInternetSales** tabeli, a następnie kliknij przycisk hello **modelu** menu > **procesu** > **partycje procesu**.</span><span class="sxs-lookup"><span data-stu-id="3b81f-148">Click hello **FactInternetSales** table, then click hello **Model** menu > **Process** > **Process Partitions**.</span></span>  
  
3.  <span data-ttu-id="3b81f-149">Okno dialogowe partycje procesu hello, sprawdź **tryb** ustawiono zbyt**domyślny proces**.</span><span class="sxs-lookup"><span data-stu-id="3b81f-149">In hello Process Partitions dialog box, verify **Mode** is set too**Process Default**.</span></span>  
  
4.  <span data-ttu-id="3b81f-150">Zaznacz pole wyboru hello w hello **procesu** kolumny dla każdego hello pięciu partycje utworzony, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="3b81f-150">Select hello checkbox in hello **Process** column for each of hello five partitions you created, and then click **OK**.</span></span>  

    ![aas-lesson10-process-partitions](../tutorials/media/aas-lesson10-process-partitions.png)
  
    <span data-ttu-id="3b81f-152">Jeśli zostanie wyświetlony monit o poświadczenia personifikacji, wprowadź nazwę użytkownika systemu Windows hello i hasło określone Lekcja 2.</span><span class="sxs-lookup"><span data-stu-id="3b81f-152">If you're prompted for Impersonation credentials, enter hello Windows user name and password you specified in Lesson 2.</span></span>  
  
    <span data-ttu-id="3b81f-153">Witaj **przetwarzania danych** okno dialogowe zostanie wyświetlone i wyświetla szczegóły procesu dla każdej partycji.</span><span class="sxs-lookup"><span data-stu-id="3b81f-153">hello **Data Processing** dialog box appears and displays process details for each partition.</span></span> <span data-ttu-id="3b81f-154">Zwróć uwagę, że dla każdej partycji przenoszona jest inna liczba wierszy.</span><span class="sxs-lookup"><span data-stu-id="3b81f-154">Notice that a different number of rows for each partition are transferred.</span></span> <span data-ttu-id="3b81f-155">Każda partycja zawiera tylko tych wierszy, dla roku hello określony w klauzuli WHERE w instrukcji SQL hello hello.</span><span class="sxs-lookup"><span data-stu-id="3b81f-155">Each partition includes only those rows for hello year specified in hello WHERE clause in hello SQL Statement.</span></span> <span data-ttu-id="3b81f-156">Po zakończeniu przetwarzania Przejdź dalej i zamknąć okno dialogowe hello przetwarzania danych.</span><span class="sxs-lookup"><span data-stu-id="3b81f-156">When processing is finished, go ahead and close hello Data Processing dialog box.</span></span>  
  
    ![aas-lesson10-process-complete](../tutorials/media/aas-lesson10-process-complete.png)
  
 ## <a name="whats-next"></a><span data-ttu-id="3b81f-158">Co dalej?</span><span class="sxs-lookup"><span data-stu-id="3b81f-158">What's next?</span></span>
<span data-ttu-id="3b81f-159">Toohello Przejdź dalej lekcji: [lekcji 11: tworzenie ról](../tutorials/aas-lesson-11-create-roles.md).</span><span class="sxs-lookup"><span data-stu-id="3b81f-159">Go toohello next lesson: [Lesson 11: Create Roles](../tutorials/aas-lesson-11-create-roles.md).</span></span> 
