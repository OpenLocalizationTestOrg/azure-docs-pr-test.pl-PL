---
title: "aaaLoad danych z programu SQL Server do usługi Azure SQL Data Warehouse (bcp) | Dokumentacja firmy Microsoft"
description: "Rozmiar danych w małych używa bcp tooexport danych z plików tooflat programu SQL Server i zaimportuj dane hello bezpośrednio do usługi Azure SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: f87d8d7c-8276-43c5-90e7-d4ccc0e3a224
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: a03b5403d123e8814ae73a7cce8e6851c8b264a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-sql-server-into-azure-sql-data-warehouse-flat-files"></a><span data-ttu-id="1fe81-103">Ładowanie danych z programu SQL Server do usługi Azure SQL Data Warehouse (pliki proste)</span><span class="sxs-lookup"><span data-stu-id="1fe81-103">Load data from SQL Server into Azure SQL Data Warehouse (flat files)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1fe81-104">SSIS</span><span class="sxs-lookup"><span data-stu-id="1fe81-104">SSIS</span></span>](sql-data-warehouse-load-from-sql-server-with-integration-services.md)
> * [<span data-ttu-id="1fe81-105">PolyBase</span><span class="sxs-lookup"><span data-stu-id="1fe81-105">PolyBase</span></span>](sql-data-warehouse-load-from-sql-server-with-polybase.md)
> * [<span data-ttu-id="1fe81-106">bcp</span><span class="sxs-lookup"><span data-stu-id="1fe81-106">bcp</span></span>](sql-data-warehouse-load-from-sql-server-with-bcp.md)
> 
> 

<span data-ttu-id="1fe81-107">Dla małych zestawów danych można użyć hello bcp narzędzia wiersza polecenia tooexport danych z programu SQL Server i następnie ładowania ich bezpośrednio tooAzure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="1fe81-107">For small data sets, you can use hello bcp command-line utility tooexport data from SQL Server and then load it directly tooAzure SQL Data Warehouse.</span></span>

<span data-ttu-id="1fe81-108">W tym samouczku przy użyciu programu bcp zostaną wykonane następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="1fe81-108">In this tutorial, you will use bcp to:</span></span>

* <span data-ttu-id="1fe81-109">Eksportowanie tabeli z z programu SQL Server przy użyciu hello polecenia bcp out (lub tworzenie prostego pliku przykładowego)</span><span class="sxs-lookup"><span data-stu-id="1fe81-109">Export a table from from SQL Server by using hello bcp out command (or create a simple sample file)</span></span>
* <span data-ttu-id="1fe81-110">Tabela hello Import z pliku prostego tooSQL hurtowni danych.</span><span class="sxs-lookup"><span data-stu-id="1fe81-110">Import hello table from a flat file tooSQL Data Warehouse.</span></span>
* <span data-ttu-id="1fe81-111">Tworzenie statystyk na powitania załadować danych.</span><span class="sxs-lookup"><span data-stu-id="1fe81-111">Create statistics on hello loaded data.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-data-into-Azure-SQL-Data-Warehouse-with-BCP/player]
> 
> 

## <a name="before-you-begin"></a><span data-ttu-id="1fe81-112">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="1fe81-112">Before you begin</span></span>
### <a name="prerequisites"></a><span data-ttu-id="1fe81-113">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="1fe81-113">Prerequisites</span></span>
<span data-ttu-id="1fe81-114">toostep opisanych w tym samouczku, potrzebne są:</span><span class="sxs-lookup"><span data-stu-id="1fe81-114">toostep through this tutorial, you need:</span></span>

* <span data-ttu-id="1fe81-115">Baza danych usługi SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="1fe81-115">A SQL Data Warehouse database</span></span>
* <span data-ttu-id="1fe81-116">Narzędzie wiersza polecenia bcp Hello zainstalowany</span><span class="sxs-lookup"><span data-stu-id="1fe81-116">hello bcp command-line utility installed</span></span>
* <span data-ttu-id="1fe81-117">narzędzia wiersza polecenia sqlcmd Hello zainstalowany</span><span class="sxs-lookup"><span data-stu-id="1fe81-117">hello sqlcmd command-line utility installed</span></span>

<span data-ttu-id="1fe81-118">Witaj narzędzia bcp i sqlcmd można pobrać z hello [Microsoft Download Center][Microsoft Download Center].</span><span class="sxs-lookup"><span data-stu-id="1fe81-118">You can download hello bcp and sqlcmd utilities from hello [Microsoft Download Center][Microsoft Download Center].</span></span>

### <a name="data-in-ascii-or-utf-16-format"></a><span data-ttu-id="1fe81-119">Dane w formacie ASCII lub UTF-16</span><span class="sxs-lookup"><span data-stu-id="1fe81-119">Data in ASCII or UTF-16 format</span></span>
<span data-ttu-id="1fe81-120">W przypadku tego samouczka z użyciem własnych danych, dane wymagają toouse hello ASCII lub kodowania UTF-16, ponieważ narzędzie bcp nie obsługuje UTF-8.</span><span class="sxs-lookup"><span data-stu-id="1fe81-120">If you are trying this tutorial with your own data, your data needs toouse hello ASCII or UTF-16 encoding since bcp does not support UTF-8.</span></span> 

<span data-ttu-id="1fe81-121">Aparat PolyBase obsługuje format UTF-8, ale nie obsługuje jeszcze formatu UTF-16.</span><span class="sxs-lookup"><span data-stu-id="1fe81-121">PolyBase supports UTF-8 but doesn't yet support UTF-16.</span></span> <span data-ttu-id="1fe81-122">Należy pamiętać, że jeśli bcp toocombine przy użyciu programu PolyBase konieczne będzie danych hello tootransform tooUTF-8 po ich wyeksportowaniu z programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="1fe81-122">Note that if you want toocombine bcp with PolyBase you will need tootransform hello data tooUTF-8 after it is exported from SQL Server.</span></span> 

## <a name="1-create-a-destination-table"></a><span data-ttu-id="1fe81-123">1. Tworzenie tabeli docelowej</span><span class="sxs-lookup"><span data-stu-id="1fe81-123">1. Create a destination table</span></span>
<span data-ttu-id="1fe81-124">Zdefiniuj tabelę w magazynie danych SQL, która będzie tabelą docelową hello hello obciążenia.</span><span class="sxs-lookup"><span data-stu-id="1fe81-124">Define a table in SQL Data Warehouse that will be hello destination table for hello load.</span></span> <span data-ttu-id="1fe81-125">Witaj kolumn w tabeli hello musi odpowiadać toohello danych w poszczególnych wierszach pliku danych.</span><span class="sxs-lookup"><span data-stu-id="1fe81-125">hello columns in hello table must correspond toohello data in each row of your data file.</span></span>

<span data-ttu-id="1fe81-126">toocreate tabelę, otwórz wiersz polecenia i użyj hello toorun sqlcmd.exe następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="1fe81-126">toocreate a table, open a command prompt and use sqlcmd.exe toorun hello following command:</span></span>

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


## <a name="2-create-a-source-data-file"></a><span data-ttu-id="1fe81-127">2. Tworzenie źródłowego pliku danych</span><span class="sxs-lookup"><span data-stu-id="1fe81-127">2. Create a source data file</span></span>
<span data-ttu-id="1fe81-128">Otwórz hello Notatnik i skopiuj następujące wiersze danych do nowego pliku tekstowego, a następnie zapisz ten plik tooyour lokalnym katalogu tymczasowym, C:\Temp\DimDate2.txt.</span><span class="sxs-lookup"><span data-stu-id="1fe81-128">Open Notepad and copy hello following lines of data into a new text file and then save this file tooyour local temp directory, C:\Temp\DimDate2.txt.</span></span> <span data-ttu-id="1fe81-129">Te dane są w formacie ASCII.</span><span class="sxs-lookup"><span data-stu-id="1fe81-129">This data is in ASCII format.</span></span>

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

<span data-ttu-id="1fe81-130">(Opcjonalnie) tooexport dane z bazy danych programu SQL Server otwórz wiersz polecenia i uruchom następujące polecenie hello.</span><span class="sxs-lookup"><span data-stu-id="1fe81-130">(Optional) tooexport your own data from a SQL Server database, open a command prompt and run hello following command.</span></span> <span data-ttu-id="1fe81-131">Zastąp parametry TableName, ServerName, DatabaseName, Username i Password odpowiednimi informacjami.</span><span class="sxs-lookup"><span data-stu-id="1fe81-131">Replace TableName, ServerName, DatabaseName, Username, and Password with your own information.</span></span>

```sql
bcp <TableName> out C:\Temp\DimDate2_export.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <Password> -q -c -t ','
```



## <a name="3-load-hello-data"></a><span data-ttu-id="1fe81-132">3. Ładowanie danych hello</span><span class="sxs-lookup"><span data-stu-id="1fe81-132">3. Load hello data</span></span>
<span data-ttu-id="1fe81-133">tooload hello danych, otwórz wiersz polecenia i uruchom hello następujące polecenie, zastępując hello wartości dla nazwy serwera, nazwę bazy danych, nazwę użytkownika i hasło z odpowiednimi informacjami.</span><span class="sxs-lookup"><span data-stu-id="1fe81-133">tooload hello data, open a command prompt and run hello following command, replacing hello values for Server Name, Database name, Username, and Password with your own information.</span></span>

```sql
bcp DimDate2 in C:\Temp\DimDate2.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <password> -q -c -t  ','
```

<span data-ttu-id="1fe81-134">Użyj tego polecenia tooverify hello dane zostały załadowane poprawnie</span><span class="sxs-lookup"><span data-stu-id="1fe81-134">Use this command tooverify hello data was loaded properly</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

<span data-ttu-id="1fe81-135">Witaj wyniki powinny wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="1fe81-135">hello results should look like this:</span></span>

| <span data-ttu-id="1fe81-136">DateId</span><span class="sxs-lookup"><span data-stu-id="1fe81-136">DateId</span></span> | <span data-ttu-id="1fe81-137">CalendarQuarter</span><span class="sxs-lookup"><span data-stu-id="1fe81-137">CalendarQuarter</span></span> | <span data-ttu-id="1fe81-138">FiscalQuarter</span><span class="sxs-lookup"><span data-stu-id="1fe81-138">FiscalQuarter</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1fe81-139">20150101</span><span class="sxs-lookup"><span data-stu-id="1fe81-139">20150101</span></span> |<span data-ttu-id="1fe81-140">1</span><span class="sxs-lookup"><span data-stu-id="1fe81-140">1</span></span> |<span data-ttu-id="1fe81-141">3</span><span class="sxs-lookup"><span data-stu-id="1fe81-141">3</span></span> |
| <span data-ttu-id="1fe81-142">20150201</span><span class="sxs-lookup"><span data-stu-id="1fe81-142">20150201</span></span> |<span data-ttu-id="1fe81-143">1</span><span class="sxs-lookup"><span data-stu-id="1fe81-143">1</span></span> |<span data-ttu-id="1fe81-144">3</span><span class="sxs-lookup"><span data-stu-id="1fe81-144">3</span></span> |
| <span data-ttu-id="1fe81-145">20150301</span><span class="sxs-lookup"><span data-stu-id="1fe81-145">20150301</span></span> |<span data-ttu-id="1fe81-146">1</span><span class="sxs-lookup"><span data-stu-id="1fe81-146">1</span></span> |<span data-ttu-id="1fe81-147">3</span><span class="sxs-lookup"><span data-stu-id="1fe81-147">3</span></span> |
| <span data-ttu-id="1fe81-148">20150401</span><span class="sxs-lookup"><span data-stu-id="1fe81-148">20150401</span></span> |<span data-ttu-id="1fe81-149">2</span><span class="sxs-lookup"><span data-stu-id="1fe81-149">2</span></span> |<span data-ttu-id="1fe81-150">4</span><span class="sxs-lookup"><span data-stu-id="1fe81-150">4</span></span> |
| <span data-ttu-id="1fe81-151">20150501</span><span class="sxs-lookup"><span data-stu-id="1fe81-151">20150501</span></span> |<span data-ttu-id="1fe81-152">2</span><span class="sxs-lookup"><span data-stu-id="1fe81-152">2</span></span> |<span data-ttu-id="1fe81-153">4</span><span class="sxs-lookup"><span data-stu-id="1fe81-153">4</span></span> |
| <span data-ttu-id="1fe81-154">20150601</span><span class="sxs-lookup"><span data-stu-id="1fe81-154">20150601</span></span> |<span data-ttu-id="1fe81-155">2</span><span class="sxs-lookup"><span data-stu-id="1fe81-155">2</span></span> |<span data-ttu-id="1fe81-156">4</span><span class="sxs-lookup"><span data-stu-id="1fe81-156">4</span></span> |
| <span data-ttu-id="1fe81-157">20150701</span><span class="sxs-lookup"><span data-stu-id="1fe81-157">20150701</span></span> |<span data-ttu-id="1fe81-158">3</span><span class="sxs-lookup"><span data-stu-id="1fe81-158">3</span></span> |<span data-ttu-id="1fe81-159">1</span><span class="sxs-lookup"><span data-stu-id="1fe81-159">1</span></span> |
| <span data-ttu-id="1fe81-160">20150801</span><span class="sxs-lookup"><span data-stu-id="1fe81-160">20150801</span></span> |<span data-ttu-id="1fe81-161">3</span><span class="sxs-lookup"><span data-stu-id="1fe81-161">3</span></span> |<span data-ttu-id="1fe81-162">1</span><span class="sxs-lookup"><span data-stu-id="1fe81-162">1</span></span> |
| <span data-ttu-id="1fe81-163">20150801</span><span class="sxs-lookup"><span data-stu-id="1fe81-163">20150801</span></span> |<span data-ttu-id="1fe81-164">3</span><span class="sxs-lookup"><span data-stu-id="1fe81-164">3</span></span> |<span data-ttu-id="1fe81-165">1</span><span class="sxs-lookup"><span data-stu-id="1fe81-165">1</span></span> |
| <span data-ttu-id="1fe81-166">20151001</span><span class="sxs-lookup"><span data-stu-id="1fe81-166">20151001</span></span> |<span data-ttu-id="1fe81-167">4</span><span class="sxs-lookup"><span data-stu-id="1fe81-167">4</span></span> |<span data-ttu-id="1fe81-168">2</span><span class="sxs-lookup"><span data-stu-id="1fe81-168">2</span></span> |
| <span data-ttu-id="1fe81-169">20151101</span><span class="sxs-lookup"><span data-stu-id="1fe81-169">20151101</span></span> |<span data-ttu-id="1fe81-170">4</span><span class="sxs-lookup"><span data-stu-id="1fe81-170">4</span></span> |<span data-ttu-id="1fe81-171">2</span><span class="sxs-lookup"><span data-stu-id="1fe81-171">2</span></span> |
| <span data-ttu-id="1fe81-172">20151201</span><span class="sxs-lookup"><span data-stu-id="1fe81-172">20151201</span></span> |<span data-ttu-id="1fe81-173">4</span><span class="sxs-lookup"><span data-stu-id="1fe81-173">4</span></span> |<span data-ttu-id="1fe81-174">2</span><span class="sxs-lookup"><span data-stu-id="1fe81-174">2</span></span> |

## <a name="4-create-statistics"></a><span data-ttu-id="1fe81-175">4. Tworzenie statystyk</span><span class="sxs-lookup"><span data-stu-id="1fe81-175">4. Create statistics</span></span>
<span data-ttu-id="1fe81-176">Usługa SQL Data Warehouse nie obsługuje jeszcze automatycznego tworzenia ani aktualizowania statystyk.</span><span class="sxs-lookup"><span data-stu-id="1fe81-176">SQL Data Warehouse does not yet support auto-create or auto-update statistics.</span></span> <span data-ttu-id="1fe81-177">tooget hello najlepszą wydajność zapytań, jest ważne toocreate statystyki dla wszystkich kolumn wszystkich tabel po pierwszym załadowaniu hello lub w danych powitania po każdej istotnej zmianie.</span><span class="sxs-lookup"><span data-stu-id="1fe81-177">tooget hello best query performance, it's important toocreate statistics on all columns of all tables after hello first load or after any substantial changes occur in hello data.</span></span> <span data-ttu-id="1fe81-178">Aby uzyskać szczegółowy opis statystyk, zobacz [statystyki][Statistics].</span><span class="sxs-lookup"><span data-stu-id="1fe81-178">For a detailed explanation of statistics, see [Statistics][Statistics].</span></span> 

<span data-ttu-id="1fe81-179">Witaj uruchom następujące polecenie toocreate statystyki dotyczące nowo załadowanej tabeli.</span><span class="sxs-lookup"><span data-stu-id="1fe81-179">Run hello following command toocreate statistics on your newly loaded table.</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    create statistics [DateId] on [DimDate2] ([DateId]);
    create statistics [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
    create statistics [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
"
```

## <a name="5-export-data-from-sql-data-warehouse"></a><span data-ttu-id="1fe81-180">5. Eksportowanie danych z usługi SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="1fe81-180">5. Export data from SQL Data Warehouse</span></span>
<span data-ttu-id="1fe81-181">Dla zabawy możesz wyeksportować dane hello załadowane przed chwilą wstecz poza SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="1fe81-181">For fun, you can export hello data that you just loaded back out of SQL Data Warehouse.</span></span>  <span data-ttu-id="1fe81-182">tooexport polecenia Hello jest hello dokładnie tak jak w przypadku eksportowania z programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="1fe81-182">hello command tooexport is exactly hello same as exporting from SQL Server.</span></span>

<span data-ttu-id="1fe81-183">Istnieje jednak różnica w wynikach hello.</span><span class="sxs-lookup"><span data-stu-id="1fe81-183">However, there is a difference in hello results.</span></span> <span data-ttu-id="1fe81-184">Ponieważ hello dane są przechowywane w rozproszonych lokalizacjach w usłudze SQL Data Warehouse, podczas eksportowania danych każdy węzeł obliczeniowy zapisuje plik wyjściowy toohello danych.</span><span class="sxs-lookup"><span data-stu-id="1fe81-184">Since hello data is stored in distributed locations within SQL Data Warehouse, when you export data each Compute node writes it data toohello output file.</span></span> <span data-ttu-id="1fe81-185">kolejność Hello hello danych w pliku wyjściowym hello jest prawdopodobnie inna niż kolejność hello hello danych w pliku wejściowym hello toobe.</span><span class="sxs-lookup"><span data-stu-id="1fe81-185">hello order of hello data in hello output file is likely toobe different than hello order of hello data in hello input file.</span></span>

### <a name="export-a-table-and-compare-exported-results"></a><span data-ttu-id="1fe81-186">Eksportowanie tabeli i porównywanie wyeksportowanych wyników</span><span class="sxs-lookup"><span data-stu-id="1fe81-186">Export a table and compare exported results</span></span>
<span data-ttu-id="1fe81-187">toosee hello wyeksportowane dane, otwórz wiersz polecenia i uruchom to polecenie z własnymi parametrami.</span><span class="sxs-lookup"><span data-stu-id="1fe81-187">toosee hello exported data, open a command prompt and run this command using your own parameters.</span></span> <span data-ttu-id="1fe81-188">ServerName jest nazwą powitania serwera logicznego SQL platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1fe81-188">ServerName is hello name of your Azure logical SQL Server.</span></span>

```sql
bcp DimDate2 out C:\Temp\DimDate2_export.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t ','
```
<span data-ttu-id="1fe81-189">Możesz sprawdzić powitalne dane zostały poprawnie wyeksportowane, otwierając nowy plik hello.</span><span class="sxs-lookup"><span data-stu-id="1fe81-189">You can verify hello data was exported correctly by opening hello new file.</span></span> <span data-ttu-id="1fe81-190">Witaj dane w pliku hello powinny odpowiadać tekstowi hello poniżej, ale prawdopodobnie będą posortowane w innej kolejności:</span><span class="sxs-lookup"><span data-stu-id="1fe81-190">hello data in hello file should match hello text below, but will likely be sorted in a different order:</span></span>

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

### <a name="export-hello-results-of-a-query"></a><span data-ttu-id="1fe81-191">Eksportowanie hello wyników zapytania</span><span class="sxs-lookup"><span data-stu-id="1fe81-191">Export hello results of a query</span></span>
<span data-ttu-id="1fe81-192">Można użyć hello **queryout** funkcja bcp tooexport hello wyniki zapytania, zamiast eksportować całą tabelę hello.</span><span class="sxs-lookup"><span data-stu-id="1fe81-192">You can use hello **queryout** function of bcp tooexport hello results of a query instead of exporting hello entire table.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="1fe81-193">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1fe81-193">Next steps</span></span>
<span data-ttu-id="1fe81-194">Omówienie ładowania można znaleźć w artykule [Ładowanie danych do usługi SQL Data Warehouse][Load data into SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="1fe81-194">For an overview of loading, see [Load data into SQL Data Warehouse][Load data into SQL Data Warehouse].</span></span>
<span data-ttu-id="1fe81-195">Więcej porad dla deweloperów znajduje się w artykule [Omówienie programowania w usłudze SQL Data Warehouse][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="1fe81-195">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>
<span data-ttu-id="1fe81-196">Zobacz [omówienie tabeli] [ Table Overview] lub [składni polecenia CREATE TABLE] [ CREATE TABLE syntax] uzyskać więcej informacji dotyczących tworzenia tabel w magazynie danych SQL.</span><span class="sxs-lookup"><span data-stu-id="1fe81-196">See [Table Overview][Table Overview] or [CREATE TABLE syntax][CREATE TABLE syntax] for more information about creating a table on SQL Data Warehouse.</span></span>

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
