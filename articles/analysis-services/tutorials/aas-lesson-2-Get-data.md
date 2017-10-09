---
<span data-ttu-id="bbbb6-101">title: aaa "Azure Analysis Services lekcji samouczek 2: pobieranie danych | Opis elementu Microsoft Docs": w tym artykule opisano, jak tooget, a następnie zaimportuj dane w hello projekt samouczka usług Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="bbbb6-101">title: aaa"Azure Analysis Services tutorial lesson 2: Get data | Microsoft Docs" description: Describes how tooget and import data in hello Azure Analysis Services tutorial project.</span></span> <span data-ttu-id="bbbb6-102">usługi: documentationcenter usług analysis services: "Autor: minewiskan Menedżera: Edytor erikre:" tagów: "</span><span class="sxs-lookup"><span data-stu-id="bbbb6-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="bbbb6-103">MS.AssetID: ms.service: ms.devlang usług analysis services: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: ms.author 2017-06/01: owend</span><span class="sxs-lookup"><span data-stu-id="bbbb6-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 06/01/2017 ms.author: owend</span></span>
---

# <a name="lesson-2-get-data"></a><span data-ttu-id="bbbb6-104">Lekcja 2. Pobieranie danych</span><span class="sxs-lookup"><span data-stu-id="bbbb6-104">Lesson 2: Get data</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="bbbb6-105">W tej lekcji Pobierz dane programu SSDT tooconnect toohello AdventureWorksDW2014 — przykładowa baza danych, wybierz dane, w wersji zapoznawczej i filtr, a następnie zaimportować do modelu obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="bbbb6-105">In this lesson, you use Get Data in SSDT tooconnect toohello AdventureWorksDW2014 sample database, select data, preview and filter, and then import into your model workspace.</span></span>  
  
<span data-ttu-id="bbbb6-106">Funkcja pobierania danych umożliwia importowanie danych z wielu różnych źródeł, takich jak: baza danych SQL Azure, Oracle, Sybase, kanał informacyjny OData, Teradata, pliki itp.</span><span class="sxs-lookup"><span data-stu-id="bbbb6-106">By using Get Data, you can import data from a wide variety of sources: Azure SQL Database, Oracle, Sybase, OData Feed, Teradata, files and more.</span></span> <span data-ttu-id="bbbb6-107">Można również wykonywać kwerendy danych przy użyciu wyrażeń formuły Power Query M.</span><span class="sxs-lookup"><span data-stu-id="bbbb6-107">Data can also be queried using a Power Query M formula expression.</span></span>
  
<span data-ttu-id="bbbb6-108">Szacowany czas toocomplete tej lekcji: **10 minut**</span><span class="sxs-lookup"><span data-stu-id="bbbb6-108">Estimated time toocomplete this lesson: **10 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="bbbb6-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="bbbb6-109">Prerequisites</span></span>  
<span data-ttu-id="bbbb6-110">Ten temat stanowi część samouczka modelowania tabelarycznego, który należy wykonać w podanej kolejności.</span><span class="sxs-lookup"><span data-stu-id="bbbb6-110">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="bbbb6-111">Przed wykonaniem zadania hello w tej lekcji, powinno mieć ukończone poprzedniej lekcji hello: [Lekcja 1: Tworzenie nowego projektu modelu tabelarycznego](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md).</span><span class="sxs-lookup"><span data-stu-id="bbbb6-111">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 1: Create a new tabular model project](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md).</span></span>  
  
## <a name="create-a-connection"></a><span data-ttu-id="bbbb6-112">Tworzenie połączenia</span><span class="sxs-lookup"><span data-stu-id="bbbb6-112">Create a connection</span></span>  
  
#### <a name="toocreate-a-connection-toohello-adventureworksdw2014-database"></a><span data-ttu-id="bbbb6-113">toocreate toohello AdventureWorksDW2014 połączenia bazy danych</span><span class="sxs-lookup"><span data-stu-id="bbbb6-113">toocreate a connection toohello AdventureWorksDW2014 database</span></span>  
  
1.  <span data-ttu-id="bbbb6-114">W Eksploratorze modeli tabelarycznych kliknij prawym przyciskiem myszy pozycje **Źródła danych** > **Importuj ze źródła danych**.</span><span class="sxs-lookup"><span data-stu-id="bbbb6-114">In Tabular Model Explorer, right-click **Data Sources** > **Import from Data Source**.</span></span>  
  
    <span data-ttu-id="bbbb6-115">Spowoduje to uruchomienie pobieranie danych, który prowadzi użytkownika przez źródło danych tooa nawiązującego połączenie.</span><span class="sxs-lookup"><span data-stu-id="bbbb6-115">This launches Get Data, which guides you through connecting tooa data source.</span></span> <span data-ttu-id="bbbb6-116">Jeśli nie widzisz Eksplorator modelu tabelarycznego, w **Eksploratora rozwiązań**, kliknij dwukrotnie **Model.bim** tooopen hello modelu w Projektancie hello.</span><span class="sxs-lookup"><span data-stu-id="bbbb6-116">If you don't see Tabular Model Explorer, in **Solution Explorer**, double-click **Model.bim** tooopen hello model in hello designer.</span></span> 
    
    ![aas-lesson2-getdata](../tutorials/media/aas-lesson2-getdata.png)
  
2.  <span data-ttu-id="bbbb6-118">W oknie Pobierz dane kliknij kolejno opcje **Baza danych** > **Baza danych SQL Server** > **Połącz**.</span><span class="sxs-lookup"><span data-stu-id="bbbb6-118">In Get Data, click **Database** > **SQL Server Database** > **Connect**.</span></span>  
  
3.  <span data-ttu-id="bbbb6-119">W hello **bazy danych programu SQL Server** okna dialogowego, w **serwera**, wpisz nazwę powitania serwera hello zainstalowaną hello AdventureWorksDW2014 bazy danych, a następnie kliknij przycisk **Connect**.</span><span class="sxs-lookup"><span data-stu-id="bbbb6-119">In hello **SQL Server Database** dialog, in **Server**, type hello name of hello server where you installed hello AdventureWorksDW2014 database, and then click **Connect**.</span></span>  

4.  <span data-ttu-id="bbbb6-120">Po wyświetleniu monitu poświadczeń tooenter należy toospecify hello poświadczenia usług Analysis Services używa tooconnect toohello źródła danych podczas importowania i przetwarzania danych.</span><span class="sxs-lookup"><span data-stu-id="bbbb6-120">When prompted tooenter credentials, you need toospecify hello credentials Analysis Services uses tooconnect toohello data source when importing and processing data.</span></span> <span data-ttu-id="bbbb6-121">W obszarze **Tryb personifikacji** wybierz pozycję **Personifikuj konto**, a następnie wprowadź poświadczenia i kliknij przycisk **Połącz**.</span><span class="sxs-lookup"><span data-stu-id="bbbb6-121">In **Impersonation Mode**, select **Impersonate Account**, then enter credentials, and then click **Connect**.</span></span> <span data-ttu-id="bbbb6-122">Zaleca się, że używasz konta, gdzie hello hasło nie traci ważności.</span><span class="sxs-lookup"><span data-stu-id="bbbb6-122">It's recommended you use an account where hello password doesn't expire.</span></span>

    ![aas-lesson2-account](../tutorials/media/aas-lesson2-account.png)
  
    > [!NOTE]  
    > <span data-ttu-id="bbbb6-124">Przy użyciu konta użytkownika systemu Windows i hasło zawiera hello najbezpieczniejszą metodą źródła danych tooa nawiązującego połączenie.</span><span class="sxs-lookup"><span data-stu-id="bbbb6-124">Using a Windows user account and password provides hello most secure method of connecting tooa data source.</span></span>
  
5.  <span data-ttu-id="bbbb6-125">W Nawigatorze, wybierz hello **AdventureWorksDW2014** bazy danych, a następnie kliknij przycisk **OK**. Spowoduje to utworzenie hello połączenia toohello w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="bbbb6-125">In Navigator, select hello **AdventureWorksDW2014** database, and then click **OK**.This creates hello connection toohello database.</span></span> 
  
6.  <span data-ttu-id="bbbb6-126">W Nawigatorze, wybierz hello pola wyboru dla hello następujących tabel: **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**,  **DimProductCategory**, **DimProductSubcategory**, i **FactInternetSales**.</span><span class="sxs-lookup"><span data-stu-id="bbbb6-126">In Navigator, select hello check box for hello following tables: **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**, **DimProductCategory**, **DimProductSubcategory**, and **FactInternetSales**.</span></span>  

    ![aas-lesson2-select-tables](../tutorials/media/aas-lesson2-select-tables.png)
  
<span data-ttu-id="bbbb6-128">Kliknięcie przycisku OK spowoduje otwarcie edytora zapytań.</span><span class="sxs-lookup"><span data-stu-id="bbbb6-128">After you click OK, Query Editor opens.</span></span> <span data-ttu-id="bbbb6-129">W następnej sekcji hello można wybrać tylko hello dane, które mają tooimport.</span><span class="sxs-lookup"><span data-stu-id="bbbb6-129">In hello next section, you select only hello data you want tooimport.</span></span>

  
## <a name="filter-hello-table-data"></a><span data-ttu-id="bbbb6-130">Filtrowanie danych tabeli hello</span><span class="sxs-lookup"><span data-stu-id="bbbb6-130">Filter hello table data</span></span>  
<span data-ttu-id="bbbb6-131">Tabele w bazie danych przykładowych AdventureWorksDW2014 hello istnieją dane, które nie jest konieczne tooinclude w modelu.</span><span class="sxs-lookup"><span data-stu-id="bbbb6-131">Tables in hello AdventureWorksDW2014 sample database have data that isn't necessary tooinclude in your model.</span></span> <span data-ttu-id="bbbb6-132">Jeśli to możliwe, ma toofilter limit miejsca w pamięci toosave zbędne dane używane przez hello modelu.</span><span class="sxs-lookup"><span data-stu-id="bbbb6-132">When possible, you want toofilter out unnecessary data toosave in-memory space used by hello model.</span></span> <span data-ttu-id="bbbb6-133">Możesz filtrować hello kolumn z tabel, nie zaimportowaniu do bazy danych obszaru roboczego hello hello modelu bazy danych lub po jej wdrożeniu.</span><span class="sxs-lookup"><span data-stu-id="bbbb6-133">You filter out some of hello columns from tables so they're not imported into hello workspace database, or hello model database after it has been deployed.</span></span> 
  
#### <a name="toofilter-hello-table-data-before-importing"></a><span data-ttu-id="bbbb6-134">dane tabeli hello toofilter przed zaimportowaniem</span><span class="sxs-lookup"><span data-stu-id="bbbb6-134">toofilter hello table data before importing</span></span>  
  
1.  <span data-ttu-id="bbbb6-135">W edytorze zapytań wybierz hello **DimCustomer** tabeli.</span><span class="sxs-lookup"><span data-stu-id="bbbb6-135">In Query Editor, select hello **DimCustomer** table.</span></span> <span data-ttu-id="bbbb6-136">Zostanie wyświetlony widok tabeli DimCustomer hello na powitania źródła danych (AdventureWorksDWQ2014 przykładowej bazy danych).</span><span class="sxs-lookup"><span data-stu-id="bbbb6-136">A view of hello DimCustomer table at hello datasource (your AdventureWorksDWQ2014 sample database) appears.</span></span> 
  
2.  <span data-ttu-id="bbbb6-137">Korzystając z funkcji wyboru wielokrotnego (Ctrl + kliknięcie), wybierz pozycje **SpanishEducation**, **FrenchEducation**, **SpanishOccupation**, **FrenchOccupation**, kliknij je prawym przyciskiem myszy, a następnie kliknij pozycję **Usuń kolumny**.</span><span class="sxs-lookup"><span data-stu-id="bbbb6-137">Multi-select (Ctrl + click) **SpanishEducation**, **FrenchEducation**, **SpanishOccupation**, **FrenchOccupation**, then right-click, and then click **Remove Columns**.</span></span> 

    ![aas-lesson2-remove-columns](../tutorials/media/aas-lesson2-remove-columns.png)
  
    <span data-ttu-id="bbbb6-139">Ponieważ hello wartości dla tych kolumn nie są istotne tooInternet analizy sprzedaży, nie jest brak konieczności tooimport tych kolumn.</span><span class="sxs-lookup"><span data-stu-id="bbbb6-139">Since hello values for these columns are not relevant tooInternet sales analysis, there is no need tooimport these columns.</span></span> <span data-ttu-id="bbbb6-140">Dzięki wyeliminowaniu zbędnych kolumn model jest mniejszy i wydajniejszy.</span><span class="sxs-lookup"><span data-stu-id="bbbb6-140">Eliminating unnecessary columns makes your model smaller and more efficient.</span></span>  
  
4.  <span data-ttu-id="bbbb6-141">Filtruj hello pozostałych tabel przez usunięcie hello następujących kolumn w każdej tabeli:</span><span class="sxs-lookup"><span data-stu-id="bbbb6-141">Filter hello remaining tables by removing hello following columns in each table:</span></span>  
    
    <span data-ttu-id="bbbb6-142">**DimDate**</span><span class="sxs-lookup"><span data-stu-id="bbbb6-142">**DimDate**</span></span>
    
      |<span data-ttu-id="bbbb6-143">Kolumna</span><span class="sxs-lookup"><span data-stu-id="bbbb6-143">Column</span></span>|  
      |--------|  
      |<span data-ttu-id="bbbb6-144">DateKey</span><span class="sxs-lookup"><span data-stu-id="bbbb6-144">DateKey</span></span>|  
      |<span data-ttu-id="bbbb6-145">**SpanishDayNameOfWeek**</span><span class="sxs-lookup"><span data-stu-id="bbbb6-145">**SpanishDayNameOfWeek**</span></span>|  
      |<span data-ttu-id="bbbb6-146">**FrenchDayNameOfWeek**</span><span class="sxs-lookup"><span data-stu-id="bbbb6-146">**FrenchDayNameOfWeek**</span></span>|  
      |<span data-ttu-id="bbbb6-147">**SpanishMonthName**</span><span class="sxs-lookup"><span data-stu-id="bbbb6-147">**SpanishMonthName**</span></span>|  
      |<span data-ttu-id="bbbb6-148">**FrenchMonthName**</span><span class="sxs-lookup"><span data-stu-id="bbbb6-148">**FrenchMonthName**</span></span>|  
  
    <span data-ttu-id="bbbb6-149">**DimGeography**</span><span class="sxs-lookup"><span data-stu-id="bbbb6-149">**DimGeography**</span></span>
  
      |<span data-ttu-id="bbbb6-150">Kolumna</span><span class="sxs-lookup"><span data-stu-id="bbbb6-150">Column</span></span>|  
      |-------------|  
      |<span data-ttu-id="bbbb6-151">**SpanishCountryRegionName**</span><span class="sxs-lookup"><span data-stu-id="bbbb6-151">**SpanishCountryRegionName**</span></span>|  
      |<span data-ttu-id="bbbb6-152">**FrenchCountryRegionName**</span><span class="sxs-lookup"><span data-stu-id="bbbb6-152">**FrenchCountryRegionName**</span></span>|  
      |<span data-ttu-id="bbbb6-153">**IpAddressLocator**</span><span class="sxs-lookup"><span data-stu-id="bbbb6-153">**IpAddressLocator**</span></span>|  
  
    <span data-ttu-id="bbbb6-154">**DimProduct**</span><span class="sxs-lookup"><span data-stu-id="bbbb6-154">**DimProduct**</span></span>
  
      |<span data-ttu-id="bbbb6-155">Kolumna</span><span class="sxs-lookup"><span data-stu-id="bbbb6-155">Column</span></span>|  
      |-----------|  
      |<span data-ttu-id="bbbb6-156">**SpanishProductName**</span><span class="sxs-lookup"><span data-stu-id="bbbb6-156">**SpanishProductName**</span></span>|  
      |<span data-ttu-id="bbbb6-157">**FrenchProductName**</span><span class="sxs-lookup"><span data-stu-id="bbbb6-157">**FrenchProductName**</span></span>|  
      |<span data-ttu-id="bbbb6-158">**FrenchDescription**</span><span class="sxs-lookup"><span data-stu-id="bbbb6-158">**FrenchDescription**</span></span>|  
      |<span data-ttu-id="bbbb6-159">**ChineseDescription**</span><span class="sxs-lookup"><span data-stu-id="bbbb6-159">**ChineseDescription**</span></span>|  
      |<span data-ttu-id="bbbb6-160">**ArabicDescription**</span><span class="sxs-lookup"><span data-stu-id="bbbb6-160">**ArabicDescription**</span></span>|  
      |<span data-ttu-id="bbbb6-161">**HebrewDescription**</span><span class="sxs-lookup"><span data-stu-id="bbbb6-161">**HebrewDescription**</span></span>|  
      |<span data-ttu-id="bbbb6-162">**ThaiDescription**</span><span class="sxs-lookup"><span data-stu-id="bbbb6-162">**ThaiDescription**</span></span>|  
      |<span data-ttu-id="bbbb6-163">**GermanDescription**</span><span class="sxs-lookup"><span data-stu-id="bbbb6-163">**GermanDescription**</span></span>|  
      |<span data-ttu-id="bbbb6-164">**JapaneseDescription**</span><span class="sxs-lookup"><span data-stu-id="bbbb6-164">**JapaneseDescription**</span></span>|  
      |<span data-ttu-id="bbbb6-165">**TurkishDescription**</span><span class="sxs-lookup"><span data-stu-id="bbbb6-165">**TurkishDescription**</span></span>|  
  
    <span data-ttu-id="bbbb6-166">**DimProductCategory**</span><span class="sxs-lookup"><span data-stu-id="bbbb6-166">**DimProductCategory**</span></span>
  
      |<span data-ttu-id="bbbb6-167">Kolumna</span><span class="sxs-lookup"><span data-stu-id="bbbb6-167">Column</span></span>|  
      |--------------------|  
      |<span data-ttu-id="bbbb6-168">**SpanishProductCategoryName**</span><span class="sxs-lookup"><span data-stu-id="bbbb6-168">**SpanishProductCategoryName**</span></span>|  
      |<span data-ttu-id="bbbb6-169">**FrenchProductCategoryName**</span><span class="sxs-lookup"><span data-stu-id="bbbb6-169">**FrenchProductCategoryName**</span></span>|  
  
    <span data-ttu-id="bbbb6-170">**DimProductSubcategory**</span><span class="sxs-lookup"><span data-stu-id="bbbb6-170">**DimProductSubcategory**</span></span>
  
      |<span data-ttu-id="bbbb6-171">Kolumna</span><span class="sxs-lookup"><span data-stu-id="bbbb6-171">Column</span></span>|  
      |-----------------------|  
      |<span data-ttu-id="bbbb6-172">**SpanishProductSubcategoryName**</span><span class="sxs-lookup"><span data-stu-id="bbbb6-172">**SpanishProductSubcategoryName**</span></span>|  
      |<span data-ttu-id="bbbb6-173">**FrenchProductSubcategoryName**</span><span class="sxs-lookup"><span data-stu-id="bbbb6-173">**FrenchProductSubcategoryName**</span></span>|  
  
    <span data-ttu-id="bbbb6-174">**FactInternetSales**</span><span class="sxs-lookup"><span data-stu-id="bbbb6-174">**FactInternetSales**</span></span>
  
      |<span data-ttu-id="bbbb6-175">Kolumna</span><span class="sxs-lookup"><span data-stu-id="bbbb6-175">Column</span></span>|  
      |------------------|  
      |<span data-ttu-id="bbbb6-176">**OrderDateKey**</span><span class="sxs-lookup"><span data-stu-id="bbbb6-176">**OrderDateKey**</span></span>|  
      |<span data-ttu-id="bbbb6-177">**DueDateKey**</span><span class="sxs-lookup"><span data-stu-id="bbbb6-177">**DueDateKey**</span></span>|  
      |<span data-ttu-id="bbbb6-178">**ShipDateKey**</span><span class="sxs-lookup"><span data-stu-id="bbbb6-178">**ShipDateKey**</span></span>|   
  
## <span data-ttu-id="bbbb6-179"><a name="Import"></a>Importuj hello wybrane tabele i kolumny danych</span><span class="sxs-lookup"><span data-stu-id="bbbb6-179"><a name="Import"></a>Import hello selected tables and column data</span></span>  
<span data-ttu-id="bbbb6-180">Teraz, po podglądu i odfiltrowane zbędne dane, można zaimportować hello reszty hello danych, które mają.</span><span class="sxs-lookup"><span data-stu-id="bbbb6-180">Now that you've previewed and filtered out unnecessary data, you can import hello rest of hello data you do want.</span></span> <span data-ttu-id="bbbb6-181">Kreator Hello importuje hello tabeli danych oraz relacje między tabelami.</span><span class="sxs-lookup"><span data-stu-id="bbbb6-181">hello wizard imports hello table data along with any relationships between tables.</span></span> <span data-ttu-id="bbbb6-182">Nowe tabele i kolumny są tworzone w modelu hello i dane, które można odfiltrować nie został zaimportowany.</span><span class="sxs-lookup"><span data-stu-id="bbbb6-182">New tables and columns are created in hello model and data that you filtered out is not be imported.</span></span>  
  
#### <a name="tooimport-hello-selected-tables-and-column-data"></a><span data-ttu-id="bbbb6-183">tooimport hello wybrane tabele i kolumny danych</span><span class="sxs-lookup"><span data-stu-id="bbbb6-183">tooimport hello selected tables and column data</span></span>  
  
1.  <span data-ttu-id="bbbb6-184">Przejrzyj wybrane pozycje.</span><span class="sxs-lookup"><span data-stu-id="bbbb6-184">Review your selections.</span></span> <span data-ttu-id="bbbb6-185">Jeśli wszystko wygląda poprawnie, kliknij przycisk **Importuj**.</span><span class="sxs-lookup"><span data-stu-id="bbbb6-185">If everything looks okay, click **Import**.</span></span> <span data-ttu-id="bbbb6-186">Witaj przetwarzania danych w oknie dialogowym Wyświetla stan hello importowanych z Twojego źródła danych do bazy danych obszaru roboczego danych.</span><span class="sxs-lookup"><span data-stu-id="bbbb6-186">hello Data Processing dialog shows hello status of data being imported from your datasource into your workspace database.</span></span>
  
    ![aas-lesson2-success](../tutorials/media/aas-lesson2-success.png) 
  
2.  <span data-ttu-id="bbbb6-188">Kliknij przycisk **Zamknij**.</span><span class="sxs-lookup"><span data-stu-id="bbbb6-188">Click **Close**.</span></span>  

  
## <a name="save-your-model-project"></a><span data-ttu-id="bbbb6-189">Zapisanie projektu modelu</span><span class="sxs-lookup"><span data-stu-id="bbbb6-189">Save your model project</span></span>  
<span data-ttu-id="bbbb6-190">Koniecznie toofrequently zapisać projekt z modelem.</span><span class="sxs-lookup"><span data-stu-id="bbbb6-190">It's important toofrequently save your model project.</span></span>  
  
#### <a name="toosave-hello-model-project"></a><span data-ttu-id="bbbb6-191">Projekt z modelem hello toosave</span><span class="sxs-lookup"><span data-stu-id="bbbb6-191">toosave hello model project</span></span>  
  
-   <span data-ttu-id="bbbb6-192">Kliknij kolejno opcje **Plik** > **Zapisz wszystko**.</span><span class="sxs-lookup"><span data-stu-id="bbbb6-192">Click **File** > **Save All**.</span></span>  
  
## <a name="whats-next"></a><span data-ttu-id="bbbb6-193">Co dalej?</span><span class="sxs-lookup"><span data-stu-id="bbbb6-193">What's next?</span></span>
<span data-ttu-id="bbbb6-194">[Lekcja 3. Oznaczanie jako tabeli dat](../tutorials/aas-lesson-3-mark-as-date-table.md).</span><span class="sxs-lookup"><span data-stu-id="bbbb6-194">[Lesson 3: Mark as Date Table](../tutorials/aas-lesson-3-mark-as-date-table.md).</span></span>

  
  
