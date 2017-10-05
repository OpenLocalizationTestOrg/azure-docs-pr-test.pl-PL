---
title: "Ładowanie danych z programu SQL Server do usługi Azure SQL Data Warehouse (PolyBase) | Microsoft Docs"
description: "Eksportowanie danych z programu SQL Server do plików prostych przy użyciu programu bcpw, importowanie danych do usługi Azure Blob Storage przy użyciu programu AZCopy oraz pozyskiwanie danych do usługi Azure SQL Data Warehouse przy użyciu programu PolyBase."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: 4d42786a-fb28-43c9-9c3b-72d19c0ecc11
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 08f94bc26d8b1e1f5a56dfccd41e394dbd721024
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="load-data-from-sql-server-into-azure-sql-data-warehouse-azcopy"></a><span data-ttu-id="fa4e9-103">Ładowanie danych z programu SQL Server do usługi Azure SQL Data Warehouse (AZCopy)</span><span class="sxs-lookup"><span data-stu-id="fa4e9-103">Load data from SQL Server into Azure SQL Data Warehouse (AZCopy)</span></span>
<span data-ttu-id="fa4e9-104">Użyj narzędzia bcp i narzędzia wiersza polecenia AZCopy do ładowania danych z programu SQL Server do usługi Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="fa4e9-104">Use bcp and AZCopy command-line utilities to load data from SQL Server to Azure blob storage.</span></span> <span data-ttu-id="fa4e9-105">Następnie zastosuj technologię PolyBase lub usługę Azure Data Factory do ładowania danych do usługi Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="fa4e9-105">Then use PolyBase or Azure Data Factory to load the data into Azure SQL Data Warehouse.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="fa4e9-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="fa4e9-106">Prerequisites</span></span>
<span data-ttu-id="fa4e9-107">Do wykonania kroków opisanych w tym samouczku potrzebne są:</span><span class="sxs-lookup"><span data-stu-id="fa4e9-107">To step through this tutorial, you need:</span></span>

* <span data-ttu-id="fa4e9-108">Baza danych usługi SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="fa4e9-108">A SQL Data Warehouse database</span></span>
* <span data-ttu-id="fa4e9-109">Zainstalowane narzędzie wiersza polecenia bcp</span><span class="sxs-lookup"><span data-stu-id="fa4e9-109">The bcp command line utility installed</span></span>
* <span data-ttu-id="fa4e9-110">Zainstalowane narzędzie wiersza polecenia SQLCMD</span><span class="sxs-lookup"><span data-stu-id="fa4e9-110">The SQLCMD command line utility installed</span></span>

> [!NOTE]
> <span data-ttu-id="fa4e9-111">Narzędzia bcp i sqlcmd można pobrać z [Centrum pobierania Microsoft][Microsoft Download Center].</span><span class="sxs-lookup"><span data-stu-id="fa4e9-111">You can download the bcp and sqlcmd utilities from the [Microsoft Download Center][Microsoft Download Center].</span></span>
> 
> 

## <a name="import-data-into-sql-data-warehouse"></a><span data-ttu-id="fa4e9-112">Importowanie danych do usługi SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="fa4e9-112">Import data into SQL Data Warehouse</span></span>
<span data-ttu-id="fa4e9-113">W tym samouczku utworzysz tabelę w usłudze Azure SQL Data Warehouse i zaimportujesz dane do tej tabeli.</span><span class="sxs-lookup"><span data-stu-id="fa4e9-113">In this tutorial, you will create a table in Azure SQL Data Warehouse and import data into the table.</span></span>

### <a name="step-1-create-a-table-in-azure-sql-data-warehouse"></a><span data-ttu-id="fa4e9-114">Krok 1: tworzenie tabeli w usłudze Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="fa4e9-114">Step 1: Create a table in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="fa4e9-115">W wierszu polecenia użyj polecenia sqlcmd, aby uruchomić następujące zapytanie w celu utworzenia tabeli w wystąpieniu:</span><span class="sxs-lookup"><span data-stu-id="fa4e9-115">From a command prompt, use sqlcmd to run the following query to create a table on your instance:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    CREATE TABLE DimDate2
    (
        DateId INT NOT NULL,
        CalendarQuarter TINYINT NOT NULL,
        FiscalQuarter TINYINT NOT NULL
    )
    WITH
    (
        CLUSTERED COLUMNSTORE INDEX,
        DISTRIBUTION = ROUND_ROBIN
    );
"
```

> [!NOTE]
> <span data-ttu-id="fa4e9-116">Zobacz artykuł [Omówienie tabel][Table Overview] lub [Składnia polecenia CREATE TABLE][CREATE TABLE syntax], aby uzyskać więcej informacji dotyczących tworzenia tabel w usłudze SQL Data Warehouse oraz dostępnych opcji klauzuli WITH.</span><span class="sxs-lookup"><span data-stu-id="fa4e9-116">See [Table Overview][Table Overview] or [CREATE TABLE syntax][CREATE TABLE syntax] for more information about creating a table on SQL Data Warehouse and the  options available in the WITH clause.</span></span>
> 
> 

### <a name="step-2-create-a-source-data-file"></a><span data-ttu-id="fa4e9-117">Krok 2: tworzenie źródłowego pliku danych</span><span class="sxs-lookup"><span data-stu-id="fa4e9-117">Step 2: Create a source data file</span></span>
<span data-ttu-id="fa4e9-118">Otwórz program Notatnik i skopiuj następujące wiersze danych do nowego pliku tekstowego, a następnie zapisz ten plik w lokalnym katalogu tymczasowym: C:\Temp\DimDate2.txt.</span><span class="sxs-lookup"><span data-stu-id="fa4e9-118">Open Notepad and copy the following lines of data into a new text file and then save this file to your local temp directory, C:\Temp\DimDate2.txt.</span></span>

```
20150301,1,3
20150501,2,4
20151001,4,2
20150201,1,3
20151201,4,2
20150801,3,1
20150601,2,4
20151101,4,2
20150401,2,4
20150701,3,1
20150901,3,1
20150101,1,3
```

> [!NOTE]
> <span data-ttu-id="fa4e9-119">Należy pamiętać, że program bcp.exe nie obsługuje kodowania pliku w formacie UTF-8.</span><span class="sxs-lookup"><span data-stu-id="fa4e9-119">It is important to remember that bcp.exe does not support the UTF-8 file encoding.</span></span> <span data-ttu-id="fa4e9-120">Podczas korzystania z programu bcp.exe należy używać plików kodowanych w formacie ASCII lub UTF-16.</span><span class="sxs-lookup"><span data-stu-id="fa4e9-120">Please use ASCII files or UTF-16 encoded files when using bcp.exe.</span></span>
> 
> 

### <a name="step-3-connect-and-import-the-data"></a><span data-ttu-id="fa4e9-121">Krok 3: nawiązywanie połączenia i importowanie danych</span><span class="sxs-lookup"><span data-stu-id="fa4e9-121">Step 3: Connect and import the data</span></span>
<span data-ttu-id="fa4e9-122">Przy użyciu narzędzia bcp można nawiązać połączenie i zaimportować dane, stosując następujące polecenie z odpowiednio zastąpionymi wartościami:</span><span class="sxs-lookup"><span data-stu-id="fa4e9-122">Using bcp, you can connect and import the data using the following command replacing the values as appropriate:</span></span>

```sql
bcp DimDate2 in C:\Temp\DimDate2.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t  ','
```

<span data-ttu-id="fa4e9-123">Poprawność załadowania danych można sprawdzić za pomocą następującego zapytania uruchomionego przy użyciu narzędzia sqlcmd:</span><span class="sxs-lookup"><span data-stu-id="fa4e9-123">You can verify the data was loaded by running the following query using sqlcmd:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

<span data-ttu-id="fa4e9-124">Powinny zostać zwrócone następujące wyniki:</span><span class="sxs-lookup"><span data-stu-id="fa4e9-124">This should return the following results:</span></span>

| <span data-ttu-id="fa4e9-125">DateId</span><span class="sxs-lookup"><span data-stu-id="fa4e9-125">DateId</span></span> | <span data-ttu-id="fa4e9-126">CalendarQuarter</span><span class="sxs-lookup"><span data-stu-id="fa4e9-126">CalendarQuarter</span></span> | <span data-ttu-id="fa4e9-127">FiscalQuarter</span><span class="sxs-lookup"><span data-stu-id="fa4e9-127">FiscalQuarter</span></span> |
| --- | --- | --- |
| <span data-ttu-id="fa4e9-128">20150101</span><span class="sxs-lookup"><span data-stu-id="fa4e9-128">20150101</span></span> |<span data-ttu-id="fa4e9-129">1</span><span class="sxs-lookup"><span data-stu-id="fa4e9-129">1</span></span> |<span data-ttu-id="fa4e9-130">3</span><span class="sxs-lookup"><span data-stu-id="fa4e9-130">3</span></span> |
| <span data-ttu-id="fa4e9-131">20150201</span><span class="sxs-lookup"><span data-stu-id="fa4e9-131">20150201</span></span> |<span data-ttu-id="fa4e9-132">1</span><span class="sxs-lookup"><span data-stu-id="fa4e9-132">1</span></span> |<span data-ttu-id="fa4e9-133">3</span><span class="sxs-lookup"><span data-stu-id="fa4e9-133">3</span></span> |
| <span data-ttu-id="fa4e9-134">20150301</span><span class="sxs-lookup"><span data-stu-id="fa4e9-134">20150301</span></span> |<span data-ttu-id="fa4e9-135">1</span><span class="sxs-lookup"><span data-stu-id="fa4e9-135">1</span></span> |<span data-ttu-id="fa4e9-136">3</span><span class="sxs-lookup"><span data-stu-id="fa4e9-136">3</span></span> |
| <span data-ttu-id="fa4e9-137">20150401</span><span class="sxs-lookup"><span data-stu-id="fa4e9-137">20150401</span></span> |<span data-ttu-id="fa4e9-138">2</span><span class="sxs-lookup"><span data-stu-id="fa4e9-138">2</span></span> |<span data-ttu-id="fa4e9-139">4</span><span class="sxs-lookup"><span data-stu-id="fa4e9-139">4</span></span> |
| <span data-ttu-id="fa4e9-140">20150501</span><span class="sxs-lookup"><span data-stu-id="fa4e9-140">20150501</span></span> |<span data-ttu-id="fa4e9-141">2</span><span class="sxs-lookup"><span data-stu-id="fa4e9-141">2</span></span> |<span data-ttu-id="fa4e9-142">4</span><span class="sxs-lookup"><span data-stu-id="fa4e9-142">4</span></span> |
| <span data-ttu-id="fa4e9-143">20150601</span><span class="sxs-lookup"><span data-stu-id="fa4e9-143">20150601</span></span> |<span data-ttu-id="fa4e9-144">2</span><span class="sxs-lookup"><span data-stu-id="fa4e9-144">2</span></span> |<span data-ttu-id="fa4e9-145">4</span><span class="sxs-lookup"><span data-stu-id="fa4e9-145">4</span></span> |
| <span data-ttu-id="fa4e9-146">20150701</span><span class="sxs-lookup"><span data-stu-id="fa4e9-146">20150701</span></span> |<span data-ttu-id="fa4e9-147">3</span><span class="sxs-lookup"><span data-stu-id="fa4e9-147">3</span></span> |<span data-ttu-id="fa4e9-148">1</span><span class="sxs-lookup"><span data-stu-id="fa4e9-148">1</span></span> |
| <span data-ttu-id="fa4e9-149">20150801</span><span class="sxs-lookup"><span data-stu-id="fa4e9-149">20150801</span></span> |<span data-ttu-id="fa4e9-150">3</span><span class="sxs-lookup"><span data-stu-id="fa4e9-150">3</span></span> |<span data-ttu-id="fa4e9-151">1</span><span class="sxs-lookup"><span data-stu-id="fa4e9-151">1</span></span> |
| <span data-ttu-id="fa4e9-152">20150801</span><span class="sxs-lookup"><span data-stu-id="fa4e9-152">20150801</span></span> |<span data-ttu-id="fa4e9-153">3</span><span class="sxs-lookup"><span data-stu-id="fa4e9-153">3</span></span> |<span data-ttu-id="fa4e9-154">1</span><span class="sxs-lookup"><span data-stu-id="fa4e9-154">1</span></span> |
| <span data-ttu-id="fa4e9-155">20151001</span><span class="sxs-lookup"><span data-stu-id="fa4e9-155">20151001</span></span> |<span data-ttu-id="fa4e9-156">4</span><span class="sxs-lookup"><span data-stu-id="fa4e9-156">4</span></span> |<span data-ttu-id="fa4e9-157">2</span><span class="sxs-lookup"><span data-stu-id="fa4e9-157">2</span></span> |
| <span data-ttu-id="fa4e9-158">20151101</span><span class="sxs-lookup"><span data-stu-id="fa4e9-158">20151101</span></span> |<span data-ttu-id="fa4e9-159">4</span><span class="sxs-lookup"><span data-stu-id="fa4e9-159">4</span></span> |<span data-ttu-id="fa4e9-160">2</span><span class="sxs-lookup"><span data-stu-id="fa4e9-160">2</span></span> |
| <span data-ttu-id="fa4e9-161">20151201</span><span class="sxs-lookup"><span data-stu-id="fa4e9-161">20151201</span></span> |<span data-ttu-id="fa4e9-162">4</span><span class="sxs-lookup"><span data-stu-id="fa4e9-162">4</span></span> |<span data-ttu-id="fa4e9-163">2</span><span class="sxs-lookup"><span data-stu-id="fa4e9-163">2</span></span> |

### <a name="step-4-create-statistics-on-your-newly-loaded-data"></a><span data-ttu-id="fa4e9-164">Krok 4: tworzenie statystyk na podstawie nowo załadowanych danych</span><span class="sxs-lookup"><span data-stu-id="fa4e9-164">Step 4: Create Statistics on your newly loaded data</span></span>
<span data-ttu-id="fa4e9-165">Usługa Azure SQL Data Warehouse nie obsługuje jeszcze automatycznego tworzenia ani aktualizowania statystyk.</span><span class="sxs-lookup"><span data-stu-id="fa4e9-165">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span> <span data-ttu-id="fa4e9-166">W celu uzyskania najlepszej wydajności zapytań należy utworzyć statystyki dla wszystkich kolumn wszystkich tabel po pierwszym załadowaniu danych, a następnie po każdej istotnej zmianie.</span><span class="sxs-lookup"><span data-stu-id="fa4e9-166">In order to get the best performance from your queries, it's important that statistics be created on all columns of all tables after the first load or any substantial changes occur in the data.</span></span> <span data-ttu-id="fa4e9-167">Szczegółowy opis statystyk znajduje się w temacie [Statystyki][Statistics] w grupie artykułów dla deweloperów.</span><span class="sxs-lookup"><span data-stu-id="fa4e9-167">For a detailed explanation of statistics, see the [Statistics][Statistics] topic in the Develop group of topics.</span></span> <span data-ttu-id="fa4e9-168">Poniżej przedstawiono prosty przykład tworzenia statystyk dotyczących tabeli załadowanej w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="fa4e9-168">Below is a quick example of how to create statistics on the tabled loaded in this example</span></span>

<span data-ttu-id="fa4e9-169">W wierszu polecenia sqlcmd wykonaj następującą instrukcję CREATE STATISTICS:</span><span class="sxs-lookup"><span data-stu-id="fa4e9-169">Execute the following CREATE STATISTICS statements from a sqlcmd prompt:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    create statistics [DateId] on [DimDate2] ([DateId]);
    create statistics [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
    create statistics [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
"
```

## <a name="export-data-from-sql-data-warehouse"></a><span data-ttu-id="fa4e9-170">Eksportowanie danych z usługi SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="fa4e9-170">Export data from SQL Data Warehouse</span></span>
<span data-ttu-id="fa4e9-171">W tym samouczku utworzysz plik danych z tabeli w usłudze SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="fa4e9-171">In this tutorial, you will create a data file from a table in SQL Data Warehouse.</span></span> <span data-ttu-id="fa4e9-172">Wyeksportujemy dane utworzone powyżej do nowego pliku danych o nazwie DimDate2_export.txt.</span><span class="sxs-lookup"><span data-stu-id="fa4e9-172">We will export the data we created above to a new data file called DimDate2_export.txt.</span></span>

### <a name="step-1-export-the-data"></a><span data-ttu-id="fa4e9-173">Krok 1: eksportowanie danych</span><span class="sxs-lookup"><span data-stu-id="fa4e9-173">Step 1: Export the data</span></span>
<span data-ttu-id="fa4e9-174">Przy użyciu narzędzia bcp można nawiązać połączenie i wyeksportować dane za pomocą następującego polecenia z odpowiednio zastąpionymi wartościami:</span><span class="sxs-lookup"><span data-stu-id="fa4e9-174">Using the bcp utility, you can connect and export data using the following command replacing the values as appropriate:</span></span>

```sql
bcp DimDate2 out C:\Temp\DimDate2_export.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t ','
```
<span data-ttu-id="fa4e9-175">Możesz sprawdzić, czy dane zostały poprawnie wyeksportowane, otwierając nowy plik.</span><span class="sxs-lookup"><span data-stu-id="fa4e9-175">You can verify the data was exported correctly by opening the new file.</span></span> <span data-ttu-id="fa4e9-176">Dane w pliku powinny zawierać poniższy tekst:</span><span class="sxs-lookup"><span data-stu-id="fa4e9-176">The data in the file should match the text below:</span></span>

```
20150301,1,3
20150501,2,4
20151001,4,2
20150201,1,3
20151201,4,2
20150801,3,1
20150601,2,4
20151101,4,2
20150401,2,4
20150701,3,1
20150901,3,1
20150101,1,3
```

> [!NOTE]
> <span data-ttu-id="fa4e9-177">Ze względu na specyfikę systemów rozproszonych kolejność danych w bazach danych usługi SQL Data Warehouse może się różnić.</span><span class="sxs-lookup"><span data-stu-id="fa4e9-177">Due to the nature of distributed systems, the data order may not be the same across SQL Data Warehouse databases.</span></span> <span data-ttu-id="fa4e9-178">Innym rozwiązaniem jest użycie funkcji **queryout** programu bcp, aby napisać zapytanie wyodrębniające, zamiast eksportowania całej tabeli.</span><span class="sxs-lookup"><span data-stu-id="fa4e9-178">Another option is to use the **queryout** function of bcp to write a query extract rather than export the entire table.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="fa4e9-179">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="fa4e9-179">Next steps</span></span>
<span data-ttu-id="fa4e9-180">Omówienie ładowania można znaleźć w artykule [Ładowanie danych do usługi SQL Data Warehouse][Load data into SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="fa4e9-180">For an overview of loading, see [Load data into SQL Data Warehouse][Load data into SQL Data Warehouse].</span></span>
<span data-ttu-id="fa4e9-181">Więcej porad dla deweloperów znajduje się w artykule [Omówienie programowania w usłudze SQL Data Warehouse][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="fa4e9-181">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

<!--Image references-->

<!--Article references-->

[Load data into SQL Data Warehouse]: ./sql-data-warehouse-overview-load.md
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
[Table Overview]: ./sql-data-warehouse-tables-overview.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md

<!--MSDN references-->
[bcp]: https://msdn.microsoft.com/library/ms162802.aspx
[CREATE TABLE syntax]: https://msdn.microsoft.com/library/mt203953.aspx

<!--Other Web references-->
[Microsoft Download Center]: https://www.microsoft.com/download/details.aspx?id=36433
