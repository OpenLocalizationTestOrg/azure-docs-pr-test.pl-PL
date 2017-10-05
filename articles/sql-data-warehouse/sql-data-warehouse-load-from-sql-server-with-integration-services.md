---
title: "Ładowanie danych z programu SQL Server do magazynu danych SQL Azure (SSIS) | Dokumentacja firmy Microsoft"
description: "Pokazuje, jak utworzyć pakiet SQL Server Integration Services (SSIS) do przenoszenia danych z różnych źródeł danych do usługi SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: e2c252e9-0828-47c2-a808-e3bea46c134a
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 03/30/2017
ms.author: cakarst;douglasl;barbkess
ms.openlocfilehash: 6c9cebdd715b6997d0633bc725a3945ba9e0c357
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="load-data-from-sql-server-into-azure-sql-data-warehouse-ssis"></a><span data-ttu-id="11add-103">Ładowanie danych z programu SQL Server do magazynu danych SQL Azure (SSIS)</span><span class="sxs-lookup"><span data-stu-id="11add-103">Load data from SQL Server into Azure SQL Data Warehouse (SSIS)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="11add-104">SSIS</span><span class="sxs-lookup"><span data-stu-id="11add-104">SSIS</span></span>](sql-data-warehouse-load-from-sql-server-with-integration-services.md)
> * [<span data-ttu-id="11add-105">PolyBase</span><span class="sxs-lookup"><span data-stu-id="11add-105">PolyBase</span></span>](sql-data-warehouse-load-from-sql-server-with-polybase.md)
> * [<span data-ttu-id="11add-106">bcp</span><span class="sxs-lookup"><span data-stu-id="11add-106">bcp</span></span>](sql-data-warehouse-load-from-sql-server-with-bcp.md)
> 
> 

<span data-ttu-id="11add-107">Utwórz pakiet SQL Server Integration Services (SSIS) ładowanie danych z programu SQL Server do usługi Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="11add-107">Create a SQL Server Integration Services (SSIS) package to load data from SQL Server into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="11add-108">Można opcjonalnie restrukturyzacji, przekształcanie i czyszczenia danych, ponieważ przechodzi ona przez przepływ danych usług SSIS.</span><span class="sxs-lookup"><span data-stu-id="11add-108">You can optionally restructure, transform, and cleanse the data as it passes through the SSIS data flow.</span></span>

<span data-ttu-id="11add-109">W tym samouczku zostaną wykonane następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="11add-109">In this tutorial, you will:</span></span>

* <span data-ttu-id="11add-110">Utwórz nowy projekt usług integracji w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="11add-110">Create a new Integration Services project in Visual Studio.</span></span>
* <span data-ttu-id="11add-111">Łączenie ze źródłami danych, w tym programu SQL Server (jako źródło) i usługi SQL Data Warehouse (jako miejsce docelowe).</span><span class="sxs-lookup"><span data-stu-id="11add-111">Connect to data sources, including SQL Server (as a source) and SQL Data Warehouse (as a destination).</span></span>
* <span data-ttu-id="11add-112">Projekt SSIS pakietu, który ładuje dane ze źródła do miejsca docelowego.</span><span class="sxs-lookup"><span data-stu-id="11add-112">Design an SSIS package that loads data from the source into the destination.</span></span>
* <span data-ttu-id="11add-113">Uruchom pakiet SSIS do ładowania danych.</span><span class="sxs-lookup"><span data-stu-id="11add-113">Run the SSIS package to load the data.</span></span>

<span data-ttu-id="11add-114">Ten samouczek używa programu SQL Server jako źródła danych.</span><span class="sxs-lookup"><span data-stu-id="11add-114">This tutorial uses SQL Server as the data source.</span></span> <span data-ttu-id="11add-115">SQL Server może działać lokalnie lub w maszynie wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="11add-115">SQL Server could be running on premises or in an Azure virtual machine.</span></span>

## <a name="basic-concepts"></a><span data-ttu-id="11add-116">Podstawowe pojęcia</span><span class="sxs-lookup"><span data-stu-id="11add-116">Basic concepts</span></span>
<span data-ttu-id="11add-117">Pakiet jest jednostka pracy w SSIS.</span><span class="sxs-lookup"><span data-stu-id="11add-117">The package is the unit of work in SSIS.</span></span> <span data-ttu-id="11add-118">Pakiety powiązane są pogrupowane w projektach.</span><span class="sxs-lookup"><span data-stu-id="11add-118">Related packages are grouped in projects.</span></span> <span data-ttu-id="11add-119">W programie Visual Studio z programu SQL Server Data Tools jest tworzenie projektów i pakietów projektów.</span><span class="sxs-lookup"><span data-stu-id="11add-119">You create projects and design packages in Visual Studio with SQL Server Data Tools.</span></span> <span data-ttu-id="11add-120">Proces projektowania jest procesem visual, w którym możesz przeciągnij i upuść składniki z przybornika do powierzchni projektu, podłącz je i ustawiania ich właściwości.</span><span class="sxs-lookup"><span data-stu-id="11add-120">The design process is a visual process in which you drag and drop components from the Toolbox to the design surface, connect them, and set their properties.</span></span> <span data-ttu-id="11add-121">Po zakończeniu pakietu, można opcjonalnie wdrożyć go do programu SQL Server kompleksowego zarządzania, monitorowania i zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="11add-121">After you finish your package, you can optionally deploy it to SQL Server for comprehensive management, monitoring, and security.</span></span>

## <a name="options-for-loading-data-with-ssis"></a><span data-ttu-id="11add-122">Opcje dotyczące ładowania danych z usług SSIS</span><span class="sxs-lookup"><span data-stu-id="11add-122">Options for loading data with SSIS</span></span>
<span data-ttu-id="11add-123">SQL Server Integration Services (SSIS) to elastyczne zestaw narzędzi, która zapewnia różne opcje połączenie i ładowania danych do usługi SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="11add-123">SQL Server Integration Services (SSIS) is a flexible set of tools that provides a variety of options for connecting to, and loading data into, SQL Data Warehouse.</span></span>

1. <span data-ttu-id="11add-124">Docelowy NET ADO używana do łączenia usługi SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="11add-124">Use an ADO NET Destination to connect to SQL Data Warehouse.</span></span> <span data-ttu-id="11add-125">W tym samouczku używa docelowego NET ADO ponieważ składa się z najmniejszą liczbą opcji konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="11add-125">This tutorial uses an ADO NET Destination because it has the fewest configuration options.</span></span>
2. <span data-ttu-id="11add-126">OLE DB docelowym używana do łączenia usługi SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="11add-126">Use an OLE DB Destination to connect to SQL Data Warehouse.</span></span> <span data-ttu-id="11add-127">Ta opcja może zapewnić nieco lepszą wydajność niż docelowy NET ADO.</span><span class="sxs-lookup"><span data-stu-id="11add-127">This option may provide slightly better performance than the ADO NET Destination.</span></span>
3. <span data-ttu-id="11add-128">Aby przemieścić danych w magazynie obiektów Blob Azure, użyj zadań przekazania obiektu Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="11add-128">Use the Azure Blob Upload Task to stage the data in Azure Blob Storage.</span></span> <span data-ttu-id="11add-129">Następnie użyć zadania SSIS wykonaj instrukcję SQL, aby uruchomić skrypt programu Polybase, który ładuje dane do usługi SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="11add-129">Then use the SSIS Execute SQL task to launch a Polybase script that loads the data into SQL Data Warehouse.</span></span> <span data-ttu-id="11add-130">Ta opcja zapewnia najlepszą wydajność trzy opcje wymienione w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="11add-130">This option provides the best performance of the three options listed here.</span></span> <span data-ttu-id="11add-131">Aby uzyskać zadanie przekazania obiektu Blob Azure, Pobierz [Microsoft SQL Server 2016 integracji usług Feature Pack dla systemu Azure][Microsoft SQL Server 2016 Integration Services Feature Pack for Azure].</span><span class="sxs-lookup"><span data-stu-id="11add-131">To get the Azure Blob Upload task, download the [Microsoft SQL Server 2016 Integration Services Feature Pack for Azure][Microsoft SQL Server 2016 Integration Services Feature Pack for Azure].</span></span> <span data-ttu-id="11add-132">Aby dowiedzieć się więcej na temat programu Polybase, zobacz [Przewodnik po programie PolyBase][PolyBase Guide].</span><span class="sxs-lookup"><span data-stu-id="11add-132">To learn more about Polybase, see [PolyBase Guide][PolyBase Guide].</span></span>

## <a name="before-you-start"></a><span data-ttu-id="11add-133">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="11add-133">Before you start</span></span>
<span data-ttu-id="11add-134">Do wykonania kroków opisanych w tym samouczku potrzebne są:</span><span class="sxs-lookup"><span data-stu-id="11add-134">To step through this tutorial, you need:</span></span>

1. <span data-ttu-id="11add-135">**SQL Server Integration Services (SSIS)**.</span><span class="sxs-lookup"><span data-stu-id="11add-135">**SQL Server Integration Services (SSIS)**.</span></span> <span data-ttu-id="11add-136">SSIS jest składnikiem programu SQL Server i wymaga wersji próbnej lub licencjonowanej wersji programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="11add-136">SSIS is a component of SQL Server and requires an evaluation version or a licensed version of SQL Server.</span></span> <span data-ttu-id="11add-137">Aby pobrać wersję ewaluacyjną programu SQL Server 2016 w wersji zapoznawczej, zobacz [programu SQL Server ocen][SQL Server Evaluations].</span><span class="sxs-lookup"><span data-stu-id="11add-137">To get an evaluation version of SQL Server 2016 Preview, see [SQL Server Evaluations][SQL Server Evaluations].</span></span>
2. <span data-ttu-id="11add-138">Program **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="11add-138">**Visual Studio**.</span></span> <span data-ttu-id="11add-139">Aby uzyskać bezpłatne Visual Studio Community Edition, zobacz [Visual Studio Community][Visual Studio Community].</span><span class="sxs-lookup"><span data-stu-id="11add-139">To get the free Visual Studio Community Edition, see [Visual Studio Community][Visual Studio Community].</span></span>
3. <span data-ttu-id="11add-140">**SQL Server Data Tools dla programu Visual Studio (SSDT)**.</span><span class="sxs-lookup"><span data-stu-id="11add-140">**SQL Server Data Tools for Visual Studio (SSDT)**.</span></span> <span data-ttu-id="11add-141">Aby uzyskać SQL Server Data Tools dla programu Visual Studio, zobacz [Pobierz programu SQL Server Data Tools (SSDT)][Download SQL Server Data Tools (SSDT)].</span><span class="sxs-lookup"><span data-stu-id="11add-141">To get SQL Server Data Tools for Visual Studio, see [Download SQL Server Data Tools (SSDT)][Download SQL Server Data Tools (SSDT)].</span></span>
4. <span data-ttu-id="11add-142">**Przykładowe dane**.</span><span class="sxs-lookup"><span data-stu-id="11add-142">**Sample data**.</span></span> <span data-ttu-id="11add-143">Ten samouczek używa przykładowe dane przechowywane w programie SQL Server w przykładowej bazie danych AdventureWorks jako źródło danych do załadowania do usługi SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="11add-143">This tutorial uses sample data stored in SQL Server in the AdventureWorks sample database as the source data to be loaded into SQL Data Warehouse.</span></span> <span data-ttu-id="11add-144">Aby pobrać przykładową bazę danych AdventureWorks, zobacz [AdventureWorks 2014 przykładowe bazy danych][AdventureWorks 2014 Sample Databases].</span><span class="sxs-lookup"><span data-stu-id="11add-144">To get the AdventureWorks sample database, see [AdventureWorks 2014 Sample Databases][AdventureWorks 2014 Sample Databases].</span></span>
5. <span data-ttu-id="11add-145">**Baza danych SQL Data Warehouse i uprawnienia**.</span><span class="sxs-lookup"><span data-stu-id="11add-145">**A SQL Data Warehouse database and permissions**.</span></span> <span data-ttu-id="11add-146">W tym samouczku łączy się z wystąpieniem usługi SQL Data Warehouse i ładuje dane do niego.</span><span class="sxs-lookup"><span data-stu-id="11add-146">This tutorial connects to a SQL Data Warehouse instance and loads data into it.</span></span> <span data-ttu-id="11add-147">Musisz mieć uprawnienia do tworzenia tabeli i ładowanie danych.</span><span class="sxs-lookup"><span data-stu-id="11add-147">You have to have permissions to create a table and to load data.</span></span>
6. <span data-ttu-id="11add-148">**Reguły zapory**.</span><span class="sxs-lookup"><span data-stu-id="11add-148">**A firewall rule**.</span></span> <span data-ttu-id="11add-149">Należy utworzyć regułę zapory na SQL Data Warehouse przy użyciu adresu IP komputera lokalnego, przed może przekazywać dane do usługi SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="11add-149">You have to create a firewall rule on SQL Data Warehouse with the IP address of your local computer before you can upload data to the SQL Data Warehouse.</span></span>

## <a name="step-1-create-a-new-integration-services-project"></a><span data-ttu-id="11add-150">Krok 1: Utwórz nowy projekt usług Integration Services</span><span class="sxs-lookup"><span data-stu-id="11add-150">Step 1: Create a new Integration Services project</span></span>
1. <span data-ttu-id="11add-151">Uruchom program Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="11add-151">Launch Visual Studio.</span></span>
2. <span data-ttu-id="11add-152">Na **pliku** menu, wybierz opcję **nowy | Projekt**.</span><span class="sxs-lookup"><span data-stu-id="11add-152">On the **File** menu, select **New | Project**.</span></span>
3. <span data-ttu-id="11add-153">Przejdź do **zainstalowane | Szablony | Analiza biznesowa | Usługi integracji** typy projektów.</span><span class="sxs-lookup"><span data-stu-id="11add-153">Navigate to the **Installed | Templates | Business Intelligence | Integration Services** project types.</span></span>
4. <span data-ttu-id="11add-154">Wybierz **projektu usług integracji**.</span><span class="sxs-lookup"><span data-stu-id="11add-154">Select **Integration Services Project**.</span></span> <span data-ttu-id="11add-155">Podaj wartości dla **nazwa** i **lokalizacji**, a następnie wybierz **OK**.</span><span class="sxs-lookup"><span data-stu-id="11add-155">Provide values for **Name** and **Location**, and then select **OK**.</span></span>

<span data-ttu-id="11add-156">Visual Studio otwierania i tworzenia nowego projektu Integration Services (SSIS).</span><span class="sxs-lookup"><span data-stu-id="11add-156">Visual Studio opens and creates a new Integration Services (SSIS) project.</span></span> <span data-ttu-id="11add-157">Następnie Visual Studio otworzy projektanta dla jednego nowego pakietu SSIS (Package.dtsx) w projekcie.</span><span class="sxs-lookup"><span data-stu-id="11add-157">Then Visual Studio opens the designer for the single new SSIS package (Package.dtsx) in the project.</span></span> <span data-ttu-id="11add-158">Zostanie wyświetlony ekran następujących obszarów:</span><span class="sxs-lookup"><span data-stu-id="11add-158">You see the following screen areas:</span></span>

* <span data-ttu-id="11add-159">Po lewej stronie **przybornika** składników usług SSIS.</span><span class="sxs-lookup"><span data-stu-id="11add-159">On the left, the **Toolbox** of SSIS components.</span></span>
* <span data-ttu-id="11add-160">W środku powierzchnię projektu z wieloma kartami.</span><span class="sxs-lookup"><span data-stu-id="11add-160">In the middle, the design surface, with multiple tabs.</span></span> <span data-ttu-id="11add-161">Używane zwykle co najmniej **przepływ sterowania** i **przepływu danych** karty.</span><span class="sxs-lookup"><span data-stu-id="11add-161">You typically use at least the **Control Flow** and the **Data Flow** tabs.</span></span>
* <span data-ttu-id="11add-162">Po prawej stronie **Eksploratora rozwiązań** i **właściwości** okienka.</span><span class="sxs-lookup"><span data-stu-id="11add-162">On the right, the **Solution Explorer** and the **Properties** panes.</span></span>
  
    ![][01]

## <a name="step-2-create-the-basic-data-flow"></a><span data-ttu-id="11add-163">Krok 2: Tworzenie przepływu danych podstawowych</span><span class="sxs-lookup"><span data-stu-id="11add-163">Step 2: Create the basic data flow</span></span>
1. <span data-ttu-id="11add-164">Przeciągnij zadania przepływu danych z przybornika do środka powierzchni projektu (na **przepływ sterowania** kartę).</span><span class="sxs-lookup"><span data-stu-id="11add-164">Drag a Data Flow Task from the Toolbox to the center of the design surface (on the **Control Flow** tab).</span></span>
   
    ![][02]
2. <span data-ttu-id="11add-165">Kliknij dwukrotnie zadania przepływu danych, aby przełączyć na kartę przepływu danych.</span><span class="sxs-lookup"><span data-stu-id="11add-165">Double-click the Data Flow Task to switch to the Data Flow tab.</span></span>
3. <span data-ttu-id="11add-166">Na liście innych źródeł w przyborniku przeciągnij źródła danych ADO.NET na powierzchnię projektu.</span><span class="sxs-lookup"><span data-stu-id="11add-166">From the Other Sources list in the Toolbox, drag an ADO.NET Source to the design surface.</span></span> <span data-ttu-id="11add-167">Z kartą źródła wciąż zaznaczony, zmień jego nazwę, aby **źródła SQL Server** w **właściwości** okienka.</span><span class="sxs-lookup"><span data-stu-id="11add-167">With the source adapter still selected, change its name to **SQL Server source** in the **Properties** pane.</span></span>
4. <span data-ttu-id="11add-168">Na liście inne miejsca docelowe w przyborniku przeciągnij docelowego ADO.NET na powierzchnię projektu w źródle danych ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="11add-168">From the Other Destinations list in the Toolbox, drag an ADO.NET Destination to the design surface under the ADO.NET Source.</span></span> <span data-ttu-id="11add-169">Z kartą docelowego nadal zaznaczone, zmień jego nazwę, aby **docelowego SQL DW** w **właściwości** okienka.</span><span class="sxs-lookup"><span data-stu-id="11add-169">With the destination adapter still selected, change its name to **SQL DW destination** in the **Properties** pane.</span></span>
   
    ![][09]

## <a name="step-3-configure-the-source-adapter"></a><span data-ttu-id="11add-170">Krok 3: Konfigurowanie karty źródła</span><span class="sxs-lookup"><span data-stu-id="11add-170">Step 3: Configure the source adapter</span></span>
1. <span data-ttu-id="11add-171">Kliknij dwukrotnie kartę źródła, aby otworzyć **Edytor źródła ADO.NET**.</span><span class="sxs-lookup"><span data-stu-id="11add-171">Double-click the source adapter to open the **ADO.NET Source Editor**.</span></span>
   
    ![][03]
2. <span data-ttu-id="11add-172">Na **Menedżera połączeń** karty **Edytor źródła ADO.NET**, kliknij przycisk **nowy** znajdujący się obok **Menedżera połączeń ADO.NET** listy, aby otworzyć **Konfigurowanie Menedżera połączeń ADO.NET** okno dialogowe i utworzyć ustawienia połączenia dla bazy danych programu SQL Server, z którego ten samouczek ładuje dane.</span><span class="sxs-lookup"><span data-stu-id="11add-172">On the **Connection Manager** tab of the **ADO.NET Source Editor**, click the **New** button next to the **ADO.NET connection manager** list to open the **Configure ADO.NET Connection Manager** dialog box and create connection settings for the SQL Server database from which this tutorial loads data.</span></span>
   
    ![][04]
3. <span data-ttu-id="11add-173">W **Konfigurowanie Menedżera połączeń ADO.NET** okno dialogowe, kliknij przycisk **nowy** przycisk, aby otworzyć **Menedżera połączeń** okno dialogowe i utworzyć nowe połączenie danych.</span><span class="sxs-lookup"><span data-stu-id="11add-173">In the **Configure ADO.NET Connection Manager** dialog box, click the **New** button to open the **Connection Manager** dialog box and create a new data connection.</span></span>
   
    ![][05]
4. <span data-ttu-id="11add-174">W **Menedżera połączeń** okno dialogowe, wykonaj następujące czynności.</span><span class="sxs-lookup"><span data-stu-id="11add-174">In the **Connection Manager** dialog box, do the following things.</span></span>
   
   1. <span data-ttu-id="11add-175">Aby uzyskać **dostawcy**, wybierz dostawcę danych SqlClient.</span><span class="sxs-lookup"><span data-stu-id="11add-175">For **Provider**, select the SqlClient Data Provider.</span></span>
   2. <span data-ttu-id="11add-176">Aby uzyskać **nazwy serwera**, wprowadź nazwę serwera SQL.</span><span class="sxs-lookup"><span data-stu-id="11add-176">For **Server name**, enter the SQL Server name.</span></span>
   3. <span data-ttu-id="11add-177">W **Zaloguj się do serwera** wybierz lub wprowadź informacje dotyczące uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="11add-177">In the **Log on to the server** section, select or enter authentication information.</span></span>
   4. <span data-ttu-id="11add-178">W **połączenie z bazą danych** Wybierz przykładową bazę danych AdventureWorks.</span><span class="sxs-lookup"><span data-stu-id="11add-178">In the **Connect to a database** section, select the AdventureWorks sample database.</span></span>
   5. <span data-ttu-id="11add-179">Kliknij przycisk **połączenie testowe**.</span><span class="sxs-lookup"><span data-stu-id="11add-179">Click **Test Connection**.</span></span>
      
       ![][06]
   6. <span data-ttu-id="11add-180">W oknie dialogowym wyświetla wyniki testu połączenia, kliknij przycisk **OK** aby powrócić do **Menedżera połączeń** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="11add-180">In the dialog box that reports the results of the connection test, click **OK** to return to the **Connection Manager** dialog box.</span></span>
   7. <span data-ttu-id="11add-181">W **Menedżera połączeń** okno dialogowe, kliknij przycisk **OK** aby powrócić do **Konfigurowanie Menedżera połączeń ADO.NET** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="11add-181">In the **Connection Manager** dialog box, click **OK** to return to the **Configure ADO.NET Connection Manager** dialog box.</span></span>
5. <span data-ttu-id="11add-182">W **Konfigurowanie Menedżera połączeń ADO.NET** okno dialogowe, kliknij przycisk **OK** aby powrócić do **Edytor źródła ADO.NET**.</span><span class="sxs-lookup"><span data-stu-id="11add-182">In the **Configure ADO.NET Connection Manager** dialog box, click **OK** to return to the **ADO.NET Source Editor**.</span></span>
6. <span data-ttu-id="11add-183">W **Edytor źródła ADO.NET**w **nazwę tabeli lub widoku** listy, wybierz **Sales.SalesOrderDetail** tabeli.</span><span class="sxs-lookup"><span data-stu-id="11add-183">In the **ADO.NET Source Editor**, in the **Name of the table or the view** list, select the **Sales.SalesOrderDetail** table.</span></span>
   
    ![][07]
7. <span data-ttu-id="11add-184">Kliknij przycisk **Podgląd** aby zobaczyć pierwszych 200 wierszy danych w tabeli źródłowej w **Podgląd wyników zapytania** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="11add-184">Click **Preview** to see the first 200 rows of data in the source table in the **Preview Query Results** dialog box.</span></span>
   
    ![][08]
8. <span data-ttu-id="11add-185">W **Podgląd wyników zapytania** okno dialogowe, kliknij przycisk **Zamknij** aby powrócić do **Edytor źródła ADO.NET**.</span><span class="sxs-lookup"><span data-stu-id="11add-185">In the **Preview Query Results** dialog box, click **Close** to return to the **ADO.NET Source Editor**.</span></span>
9. <span data-ttu-id="11add-186">W **Edytor źródła ADO.NET**, kliknij przycisk **OK** do zakończenia konfigurowania źródła danych.</span><span class="sxs-lookup"><span data-stu-id="11add-186">In the **ADO.NET Source Editor**, click **OK** to finish configuring the data source.</span></span>

## <a name="step-4-connect-the-source-adapter-to-the-destination-adapter"></a><span data-ttu-id="11add-187">Krok 4: Połącz kartę źródła adapter miejsca docelowego</span><span class="sxs-lookup"><span data-stu-id="11add-187">Step 4: Connect the source adapter to the destination adapter</span></span>
1. <span data-ttu-id="11add-188">Wybierz kartę źródła na powierzchni projektu.</span><span class="sxs-lookup"><span data-stu-id="11add-188">Select the source adapter on the design surface.</span></span>
2. <span data-ttu-id="11add-189">Wybierz niebieską strzałką, rozszerzający z karty źródła i przeciągnij go do docelowego edytora, dopóki nie zostanie zablokowany na miejscu.</span><span class="sxs-lookup"><span data-stu-id="11add-189">Select the blue arrow that extends from the source adapter and drag it to the destination editor until it snaps into place.</span></span>
   
    ![][10]
   
    <span data-ttu-id="11add-190">W typowych pakietów SSIS umożliwia wiele innych składników z przybornika SSIS Between źródłową i docelową restrukturyzacji, transformacji i czyszczenia danych, ponieważ przechodzi ona przez przepływ danych usług SSIS.</span><span class="sxs-lookup"><span data-stu-id="11add-190">In a typical SSIS package, you use a number of other components from the SSIS Toolbox in between the source and the destination to restructure, transform, and cleanse your data as it passes through the SSIS data flow.</span></span> <span data-ttu-id="11add-191">Aby zachować w tym przykładzie jest tak proste, jak to możliwe, możemy ustanawiane jest połączenie źródło bezpośrednio do miejsca docelowego.</span><span class="sxs-lookup"><span data-stu-id="11add-191">To keep this example as simple as possible, we’re connecting the source directly to the destination.</span></span>

## <a name="step-5-configure-the-destination-adapter"></a><span data-ttu-id="11add-192">Krok 5: Konfigurowanie adapter miejsca docelowego</span><span class="sxs-lookup"><span data-stu-id="11add-192">Step 5: Configure the destination adapter</span></span>
1. <span data-ttu-id="11add-193">Kliknij dwukrotnie kartę docelowego, aby otworzyć **ADO.NET docelowego edytora**.</span><span class="sxs-lookup"><span data-stu-id="11add-193">Double-click the destination adapter to open the **ADO.NET Destination Editor**.</span></span>
   
    ![][11]
2. <span data-ttu-id="11add-194">Na **Menedżera połączeń** karty **ADO.NET docelowego edytora**, kliknij przycisk **nowy** znajdujący się obok **Menedżera połączeń** listy, aby otworzyć **Konfigurowanie Menedżera połączeń ADO.NET** okno dialogowe i utworzyć ustawienia połączenia dla bazy danych Azure SQL Data Warehouse, w którym w tym samouczku ładuje dane.</span><span class="sxs-lookup"><span data-stu-id="11add-194">On the **Connection Manager** tab of the **ADO.NET Destination Editor**, click the **New** button next to the **Connection manager** list to open the **Configure ADO.NET Connection Manager** dialog box and create connection settings for the Azure SQL Data Warehouse database into which this tutorial loads data.</span></span>
3. <span data-ttu-id="11add-195">W **Konfigurowanie Menedżera połączeń ADO.NET** okno dialogowe, kliknij przycisk **nowy** przycisk, aby otworzyć **Menedżera połączeń** okno dialogowe i utworzyć nowe połączenie danych.</span><span class="sxs-lookup"><span data-stu-id="11add-195">In the **Configure ADO.NET Connection Manager** dialog box, click the **New** button to open the **Connection Manager** dialog box and create a new data connection.</span></span>
4. <span data-ttu-id="11add-196">W **Menedżera połączeń** okno dialogowe, wykonaj następujące czynności.</span><span class="sxs-lookup"><span data-stu-id="11add-196">In the **Connection Manager** dialog box, do the following things.</span></span>
   1. <span data-ttu-id="11add-197">Aby uzyskać **dostawcy**, wybierz dostawcę danych SqlClient.</span><span class="sxs-lookup"><span data-stu-id="11add-197">For **Provider**, select the SqlClient Data Provider.</span></span>
   2. <span data-ttu-id="11add-198">Aby uzyskać **nazwy serwera**, wprowadź nazwę usługi SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="11add-198">For **Server name**, enter the SQL Data Warehouse name.</span></span>
   3. <span data-ttu-id="11add-199">W **Zaloguj się do serwera** zaznacz **uwierzytelniania programu SQL Server używana** , a następnie wprowadź informacje dotyczące uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="11add-199">In the **Log on to the server** section, select **Use SQL Server authentication** and enter authentication information.</span></span>
   4. <span data-ttu-id="11add-200">W **połączenie z bazą danych** wybierz istniejącą bazę danych usługi SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="11add-200">In the **Connect to a database** section, select an existing SQL Data Warehouse database.</span></span>
   5. <span data-ttu-id="11add-201">Kliknij przycisk **połączenie testowe**.</span><span class="sxs-lookup"><span data-stu-id="11add-201">Click **Test Connection**.</span></span>
   6. <span data-ttu-id="11add-202">W oknie dialogowym wyświetla wyniki testu połączenia, kliknij przycisk **OK** aby powrócić do **Menedżera połączeń** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="11add-202">In the dialog box that reports the results of the connection test, click **OK** to return to the **Connection Manager** dialog box.</span></span>
   7. <span data-ttu-id="11add-203">W **Menedżera połączeń** okno dialogowe, kliknij przycisk **OK** aby powrócić do **Konfigurowanie Menedżera połączeń ADO.NET** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="11add-203">In the **Connection Manager** dialog box, click **OK** to return to the **Configure ADO.NET Connection Manager** dialog box.</span></span>
5. <span data-ttu-id="11add-204">W **Konfigurowanie Menedżera połączeń ADO.NET** okno dialogowe, kliknij przycisk **OK** aby powrócić do **ADO.NET docelowego edytora**.</span><span class="sxs-lookup"><span data-stu-id="11add-204">In the **Configure ADO.NET Connection Manager** dialog box, click **OK** to return to the **ADO.NET Destination Editor**.</span></span>
6. <span data-ttu-id="11add-205">W **ADO.NET docelowego edytora**, kliknij przycisk **nowy** obok **za pomocą tabeli lub widoku** listy, aby otworzyć **Create Table** okno dialogowe, aby utworzyć nową tabelę miejsce docelowe z listy kolumn, który odpowiada tabeli źródłowej.</span><span class="sxs-lookup"><span data-stu-id="11add-205">In the **ADO.NET Destination Editor**, click **New** next to the **Use a table or view** list to open the **Create Table** dialog box to create a new destination table with a column list that matches the source table.</span></span>
   
    ![][12a]
7. <span data-ttu-id="11add-206">W **Create Table** okno dialogowe, wykonaj następujące czynności.</span><span class="sxs-lookup"><span data-stu-id="11add-206">In the **Create Table** dialog box, do the following things.</span></span>
   
   1. <span data-ttu-id="11add-207">Zmień nazwę tabeli docelowej do **szczegóły zamówienia sprzedaży**.</span><span class="sxs-lookup"><span data-stu-id="11add-207">Change the name of the destination table to **SalesOrderDetail**.</span></span>
   2. <span data-ttu-id="11add-208">Usuń **rowguid** kolumny.</span><span class="sxs-lookup"><span data-stu-id="11add-208">Remove the **rowguid** column.</span></span> <span data-ttu-id="11add-209">**Uniqueidentifier** — typ danych nie jest obsługiwana w usłudze SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="11add-209">The **uniqueidentifier** data type is not supported in SQL Data Warehouse.</span></span>
   3. <span data-ttu-id="11add-210">Zmień typ danych **LineTotal** kolumny **pieniędzy**.</span><span class="sxs-lookup"><span data-stu-id="11add-210">Change the data type of the **LineTotal** column to **money**.</span></span> <span data-ttu-id="11add-211">**Dziesiętną** — typ danych nie jest obsługiwana w usłudze SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="11add-211">The **decimal** data type is not supported in SQL Data Warehouse.</span></span> <span data-ttu-id="11add-212">Informacje o obsługiwane typy danych, zobacz [CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)][CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)].</span><span class="sxs-lookup"><span data-stu-id="11add-212">For info about supported data types, see [CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)][CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)].</span></span>
      
       ![][12b]
   4. <span data-ttu-id="11add-213">Kliknij przycisk **OK** do utworzenia tabeli, a następnie wróć do **ADO.NET docelowego edytora**.</span><span class="sxs-lookup"><span data-stu-id="11add-213">Click **OK** to create the table and return to the **ADO.NET Destination Editor**.</span></span>
8. <span data-ttu-id="11add-214">W **ADO.NET docelowego edytora**, wybierz pozycję **mapowania** kartę, aby zobaczyć, jak kolumny w źródle są mapowane na kolumny w lokalizacji docelowej.</span><span class="sxs-lookup"><span data-stu-id="11add-214">In the **ADO.NET Destination Editor**, select the **Mappings** tab to see how columns in the source are mapped to columns in the destination.</span></span>
   
    ![][13]
9. <span data-ttu-id="11add-215">Kliknij przycisk **OK** do zakończenia konfigurowania źródła danych.</span><span class="sxs-lookup"><span data-stu-id="11add-215">Click **OK** to finish configuring the data source.</span></span>

## <a name="step-6-run-the-package-to-load-the-data"></a><span data-ttu-id="11add-216">Krok 6: Uruchamianie pakietu do ładowania danych</span><span class="sxs-lookup"><span data-stu-id="11add-216">Step 6: Run the package to load the data</span></span>
<span data-ttu-id="11add-217">Uruchom pakiet, klikając **Start** przycisk na pasku narzędzi lub wybierając jedną z **Uruchom** opcje na **debugowania** menu.</span><span class="sxs-lookup"><span data-stu-id="11add-217">Run the package by clicking the **Start** button on the toolbar or by selecting one of the **Run** options on the **Debug** menu.</span></span>

<span data-ttu-id="11add-218">Pakiet po rozpoczęciu do uruchomienia, zostanie wyświetlony żółty koła Obracająca, aby wskazać, działania, a także liczbę wierszy do tej pory przetworzone.</span><span class="sxs-lookup"><span data-stu-id="11add-218">As the package begins to run, you see yellow spinning wheels to indicate activity as well as the number of rows processed so far.</span></span>

![][14]

<span data-ttu-id="11add-219">Gdy pakiet zakończył działanie, zostanie wyświetlony zielony znaczniki wyboru w celu wskazania powodzenia, jak również całkowita liczba wierszy danych załadowanych od źródła do miejsca docelowego.</span><span class="sxs-lookup"><span data-stu-id="11add-219">When the package has finished running, you see green check marks to indicate success as well as the total number of rows of data loaded from the source to the destination.</span></span>

![][15]

<span data-ttu-id="11add-220">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="11add-220">Congratulations!</span></span> <span data-ttu-id="11add-221">SQL Server Integration Services została pomyślnie użyta, ładowanie danych do usługi Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="11add-221">You’ve successfully used SQL Server Integration Services to load data into Azure SQL Data Warehouse.</span></span>

## <a name="next-steps"></a><span data-ttu-id="11add-222">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="11add-222">Next steps</span></span>
* <span data-ttu-id="11add-223">Dowiedz się więcej na temat przepływu danych usług SSIS.</span><span class="sxs-lookup"><span data-stu-id="11add-223">Learn more about the SSIS data flow.</span></span> <span data-ttu-id="11add-224">Zacznij tutaj: [przepływu danych][Data Flow].</span><span class="sxs-lookup"><span data-stu-id="11add-224">Start here: [Data Flow][Data Flow].</span></span>
* <span data-ttu-id="11add-225">Dowiedz się, jak debugowania i rozwiązywania problemów z uprawnienie pakiety w środowisku projektowym.</span><span class="sxs-lookup"><span data-stu-id="11add-225">Learn how to debug and troubleshoot your packages right in the design environment.</span></span> <span data-ttu-id="11add-226">Zacznij tutaj: [Rozwiązywanie problemów z narzędzia do tworzenia pakietu][Troubleshooting Tools for Package Development].</span><span class="sxs-lookup"><span data-stu-id="11add-226">Start here: [Troubleshooting Tools for Package Development][Troubleshooting Tools for Package Development].</span></span>
* <span data-ttu-id="11add-227">Dowiedz się, jak wdrożyć swoje projekty SSIS i pakietów, na serwer usług Integration Services lub do innej lokalizacji magazynu.</span><span class="sxs-lookup"><span data-stu-id="11add-227">Learn how to deploy your SSIS projects and packages to Integration Services Server or to another storage location.</span></span> <span data-ttu-id="11add-228">Zacznij tutaj: [projekty wdrożeń i pakietów][Deployment of Projects and Packages].</span><span class="sxs-lookup"><span data-stu-id="11add-228">Start here: [Deployment of Projects and Packages][Deployment of Projects and Packages].</span></span>

<!-- Image references -->
[01]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ssis-designer-01.png
[02]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ssis-data-flow-task-02.png
[03]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-source-03.png
[04]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-connection-manager-04.png
[05]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-connection-05.png
[06]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/test-connection-06.png
[07]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-source-07.png
[08]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/preview-data-08.png
[09]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/source-destination-09.png
[10]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/connect-source-destination-10.png
[11]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-destination-11.png
[12a]: ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/destination-query-before-12a.png
[12b]: ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/destination-query-after-12b.png
[13]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/column-mapping-13.png
[14]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/package-running-14.png
[15]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/package-success-15.png

<!-- Article references -->

<!-- MSDN references -->
[PolyBase Guide]: https://msdn.microsoft.com/library/mt143171.aspx
[Download SQL Server Data Tools (SSDT)]: https://msdn.microsoft.com/library/mt204009.aspx
[CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)]: https://msdn.microsoft.com/library/mt203953.aspx
[Data Flow]: https://msdn.microsoft.com/library/ms140080.aspx
[Troubleshooting Tools for Package Development]: https://msdn.microsoft.com/library/ms137625.aspx
[Deployment of Projects and Packages]: https://msdn.microsoft.com/library/hh213290.aspx

<!--Other Web references-->
[Microsoft SQL Server 2016 Integration Services Feature Pack for Azure]: http://go.microsoft.com/fwlink/?LinkID=626967
[SQL Server Evaluations]: https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016
[Visual Studio Community]: https://www.visualstudio.com/en-us/products/visual-studio-community-vs.aspx
[AdventureWorks 2014 Sample Databases]: https://msftdbprodsamples.codeplex.com/releases/view/125550
