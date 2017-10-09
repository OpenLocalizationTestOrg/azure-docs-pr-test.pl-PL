---
title: "aaaUse bcp tooload danych do usługi SQL Data Warehouse | Dokumentacja firmy Microsoft"
description: "Dowiedz się, czym jest program bcp i jak toouse go w scenariuszach dotyczących magazynów danych."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: f9467d11-fcd6-4131-a65a-2022d2c32d24
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 09a2980585097644924c71899f9e74fb32fbc26d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-with-bcp"></a><span data-ttu-id="bc9f5-103">Ładowanie danych za pomocą narzędzia BCP</span><span class="sxs-lookup"><span data-stu-id="bc9f5-103">Load data with bcp</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="bc9f5-104">Redgate</span><span class="sxs-lookup"><span data-stu-id="bc9f5-104">Redgate</span></span>](sql-data-warehouse-load-with-redgate.md)  
> * [<span data-ttu-id="bc9f5-105">Data Factory</span><span class="sxs-lookup"><span data-stu-id="bc9f5-105">Data Factory</span></span>](sql-data-warehouse-get-started-load-with-azure-data-factory.md)  
> * [<span data-ttu-id="bc9f5-106">PolyBase</span><span class="sxs-lookup"><span data-stu-id="bc9f5-106">PolyBase</span></span>](sql-data-warehouse-get-started-load-with-polybase.md)  
> * [<span data-ttu-id="bc9f5-107">BCP</span><span class="sxs-lookup"><span data-stu-id="bc9f5-107">BCP</span></span>](sql-data-warehouse-load-with-bcp.md)
> 
> 

<span data-ttu-id="bc9f5-108">**[Narzędzie BCP] [ bcp]**  to narzędzie obciążenia zbiorczego wiersza polecenia, które pozwala toocopy danych między programami SQL Server, plików danych i magazyn danych SQL.</span><span class="sxs-lookup"><span data-stu-id="bc9f5-108">**[bcp][bcp]** is a command-line bulk load utility that allows you toocopy data between SQL Server, data files, and SQL Data Warehouse.</span></span> <span data-ttu-id="bc9f5-109">Za pomocą narzędzia bcp tooimport dużą liczbę wierszy do tabel SQL Data Warehouse lub tooexport dane z tabel programu SQL Server do plików danych.</span><span class="sxs-lookup"><span data-stu-id="bc9f5-109">Use bcp tooimport large numbers of rows into SQL Data Warehouse tables or tooexport data from SQL Server tables into data files.</span></span> <span data-ttu-id="bc9f5-110">Z wyjątkiem przypadków obejmujących użycie opcji queryout hello bcp nie wymaga żadnej znajomości języka Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="bc9f5-110">Except when used with hello queryout option, bcp requires no knowledge of Transact-SQL.</span></span>

<span data-ttu-id="bc9f5-111">BCP można szybko i łatwo toomove mniejszych zestawów danych do i z bazy danych SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="bc9f5-111">bcp is a quick and easy way toomove smaller data sets into and out of a SQL Data Warehouse database.</span></span> <span data-ttu-id="bc9f5-112">zależy od rodzaju Hello dokładną ilość danych zaleca się tooload/wyodrębniania za pomocą narzędzia bcp w sieci centrum danych Azure toohello połączenia.</span><span class="sxs-lookup"><span data-stu-id="bc9f5-112">hello exact amount of data that is recommended tooload/extract via bcp will depend on you network connection toohello Azure data center.</span></span>  <span data-ttu-id="bc9f5-113">Ogólnie rzecz biorąc, przy użyciu narzędzia bcp można łatwo ładować tabele wymiarów i wyodrębniać z nich dane, jednak narzędzie to nie jest zalecane dla ładowania lub wyodrębniania dużych ilości danych.</span><span class="sxs-lookup"><span data-stu-id="bc9f5-113">Generally, dimension tables can be loaded and extracted readily with bcp, however, bcp is not recommended for loading or extracting large volumes of data.</span></span>  <span data-ttu-id="bc9f5-114">Program Polybase jest hello zalecane narzędziem do ładowania i wyodrębnianie dużych ilości danych, jak lepiej zadanie, wykorzystując architekturę masowego przetwarzania równoległego hello usługi SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="bc9f5-114">Polybase is hello recommended tool for loading and extracting large volumes of data as it does a better job leveraging hello massively parallel processing architecture of SQL Data Warehouse.</span></span>

<span data-ttu-id="bc9f5-115">Narzędzie bcp umożliwia:</span><span class="sxs-lookup"><span data-stu-id="bc9f5-115">With bcp you can:</span></span>

* <span data-ttu-id="bc9f5-116">Użyj danych tooload prostego narzędzia wiersza polecenia do usługi SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="bc9f5-116">Use a simple command-line utility tooload data into SQL Data Warehouse.</span></span>
* <span data-ttu-id="bc9f5-117">Użyj danych tooextract prostego narzędzia wiersza polecenia z magazynu danych SQL.</span><span class="sxs-lookup"><span data-stu-id="bc9f5-117">Use a simple command-line utility tooextract data from SQL Data Warehouse.</span></span>

<span data-ttu-id="bc9f5-118">Ten samouczek przedstawia sposób wykonania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="bc9f5-118">This tutorial will show you how to:</span></span>

* <span data-ttu-id="bc9f5-119">Importowanie danych do tabeli za pomocą narzędzia bcp hello w poleceniu</span><span class="sxs-lookup"><span data-stu-id="bc9f5-119">Import data into a table using hello bcp in command</span></span>
* <span data-ttu-id="bc9f5-120">Eksportowanie danych z tabeli budynkach hello polecenia bcp out</span><span class="sxs-lookup"><span data-stu-id="bc9f5-120">Export data from a table uisng hello bcp out command</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-data-into-Azure-SQL-Data-Warehouse-with-BCP/player]
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="bc9f5-121">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="bc9f5-121">Prerequisites</span></span>
<span data-ttu-id="bc9f5-122">toostep opisanych w tym samouczku, potrzebne są:</span><span class="sxs-lookup"><span data-stu-id="bc9f5-122">toostep through this tutorial, you need:</span></span>

* <span data-ttu-id="bc9f5-123">Baza danych usługi SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="bc9f5-123">A SQL Data Warehouse database</span></span>
* <span data-ttu-id="bc9f5-124">zainstalowane narzędzie wiersza polecenia bcp Hello</span><span class="sxs-lookup"><span data-stu-id="bc9f5-124">hello bcp command line utility installed</span></span>
* <span data-ttu-id="bc9f5-125">Witaj zainstalowane narzędzie wiersza polecenia SQLCMD</span><span class="sxs-lookup"><span data-stu-id="bc9f5-125">hello SQLCMD command line utility installed</span></span>

> [!NOTE]
> <span data-ttu-id="bc9f5-126">Witaj narzędzia bcp i sqlcmd można pobrać z hello [Microsoft Download Center][Microsoft Download Center].</span><span class="sxs-lookup"><span data-stu-id="bc9f5-126">You can download hello bcp and sqlcmd utilities from hello [Microsoft Download Center][Microsoft Download Center].</span></span>
> 
> 

## <a name="import-data-into-sql-data-warehouse"></a><span data-ttu-id="bc9f5-127">Importowanie danych do usługi SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="bc9f5-127">Import data into SQL Data Warehouse</span></span>
<span data-ttu-id="bc9f5-128">W tym samouczku utworzysz tabelę w usłudze Azure SQL Data Warehouse i zaimportuj dane do tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="bc9f5-128">In this tutorial, you will create a table in Azure SQL Data Warehouse and import data into hello table.</span></span>

### <a name="step-1-create-a-table-in-azure-sql-data-warehouse"></a><span data-ttu-id="bc9f5-129">Krok 1: tworzenie tabeli w usłudze Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="bc9f5-129">Step 1: Create a table in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="bc9f5-130">Z wiersza polecenia użyj następującego zapytania toocreate tabeli w wystąpieniu hello toorun sqlcmd:</span><span class="sxs-lookup"><span data-stu-id="bc9f5-130">From a command prompt, use sqlcmd toorun hello following query toocreate a table on your instance:</span></span>

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
> <span data-ttu-id="bc9f5-131">Zobacz [omówienie tabeli] [ Table Overview] lub [składni polecenia CREATE TABLE] [ CREATE TABLE syntax] Aby uzyskać więcej informacji dotyczących tworzenia tabel SQL Data Warehouse i hello  Opcje dostępne w klauzuli WITH hello.</span><span class="sxs-lookup"><span data-stu-id="bc9f5-131">See [Table Overview][Table Overview] or [CREATE TABLE syntax][CREATE TABLE syntax] for more information about creating a table on SQL Data Warehouse and hello  options available in hello WITH clause.</span></span>
> 
> 

### <a name="step-2-create-a-source-data-file"></a><span data-ttu-id="bc9f5-132">Krok 2: tworzenie źródłowego pliku danych</span><span class="sxs-lookup"><span data-stu-id="bc9f5-132">Step 2: Create a source data file</span></span>
<span data-ttu-id="bc9f5-133">Otwórz hello Notatnik i skopiuj następujące wiersze danych do nowego pliku tekstowego, a następnie zapisz ten plik tooyour lokalnym katalogu tymczasowym, C:\Temp\DimDate2.txt.</span><span class="sxs-lookup"><span data-stu-id="bc9f5-133">Open Notepad and copy hello following lines of data into a new text file and then save this file tooyour local temp directory, C:\Temp\DimDate2.txt.</span></span>

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
> <span data-ttu-id="bc9f5-134">Jest ważne tooremember program bcp.exe nie obsługuje kodowania pliku hello UTF-8.</span><span class="sxs-lookup"><span data-stu-id="bc9f5-134">It is important tooremember that bcp.exe does not support hello UTF-8 file encoding.</span></span> <span data-ttu-id="bc9f5-135">Podczas korzystania z programu bcp.exe należy używać plików kodowanych w formacie ASCII lub UTF-16.</span><span class="sxs-lookup"><span data-stu-id="bc9f5-135">Please use ASCII files or UTF-16 encoded files when using bcp.exe.</span></span>
> 
> 

### <a name="step-3-connect-and-import-hello-data"></a><span data-ttu-id="bc9f5-136">Krok 3: Łączenie i zaimportuj dane hello</span><span class="sxs-lookup"><span data-stu-id="bc9f5-136">Step 3: Connect and import hello data</span></span>
<span data-ttu-id="bc9f5-137">Przy użyciu narzędzia bcp, możesz łączyć i zaimportować dane hello przy użyciu hello następujące polecenia zastąpienie wartości hello zależnie od potrzeb:</span><span class="sxs-lookup"><span data-stu-id="bc9f5-137">Using bcp, you can connect and import hello data using hello following command replacing hello values as appropriate:</span></span>

```sql
bcp DimDate2 in C:\Temp\DimDate2.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t  ','
```

<span data-ttu-id="bc9f5-138">Można sprawdzić hello załadowania danych, uruchamiając następujące zapytanie przy użyciu narzędzia sqlcmd hello:</span><span class="sxs-lookup"><span data-stu-id="bc9f5-138">You can verify hello data was loaded by running hello following query using sqlcmd:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

<span data-ttu-id="bc9f5-139">Powinny zostać zwrócone hello następujące wyniki:</span><span class="sxs-lookup"><span data-stu-id="bc9f5-139">This should return hello following results:</span></span>

| <span data-ttu-id="bc9f5-140">DateId</span><span class="sxs-lookup"><span data-stu-id="bc9f5-140">DateId</span></span> | <span data-ttu-id="bc9f5-141">CalendarQuarter</span><span class="sxs-lookup"><span data-stu-id="bc9f5-141">CalendarQuarter</span></span> | <span data-ttu-id="bc9f5-142">FiscalQuarter</span><span class="sxs-lookup"><span data-stu-id="bc9f5-142">FiscalQuarter</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bc9f5-143">20150101</span><span class="sxs-lookup"><span data-stu-id="bc9f5-143">20150101</span></span> |<span data-ttu-id="bc9f5-144">1</span><span class="sxs-lookup"><span data-stu-id="bc9f5-144">1</span></span> |<span data-ttu-id="bc9f5-145">3</span><span class="sxs-lookup"><span data-stu-id="bc9f5-145">3</span></span> |
| <span data-ttu-id="bc9f5-146">20150201</span><span class="sxs-lookup"><span data-stu-id="bc9f5-146">20150201</span></span> |<span data-ttu-id="bc9f5-147">1</span><span class="sxs-lookup"><span data-stu-id="bc9f5-147">1</span></span> |<span data-ttu-id="bc9f5-148">3</span><span class="sxs-lookup"><span data-stu-id="bc9f5-148">3</span></span> |
| <span data-ttu-id="bc9f5-149">20150301</span><span class="sxs-lookup"><span data-stu-id="bc9f5-149">20150301</span></span> |<span data-ttu-id="bc9f5-150">1</span><span class="sxs-lookup"><span data-stu-id="bc9f5-150">1</span></span> |<span data-ttu-id="bc9f5-151">3</span><span class="sxs-lookup"><span data-stu-id="bc9f5-151">3</span></span> |
| <span data-ttu-id="bc9f5-152">20150401</span><span class="sxs-lookup"><span data-stu-id="bc9f5-152">20150401</span></span> |<span data-ttu-id="bc9f5-153">2</span><span class="sxs-lookup"><span data-stu-id="bc9f5-153">2</span></span> |<span data-ttu-id="bc9f5-154">4</span><span class="sxs-lookup"><span data-stu-id="bc9f5-154">4</span></span> |
| <span data-ttu-id="bc9f5-155">20150501</span><span class="sxs-lookup"><span data-stu-id="bc9f5-155">20150501</span></span> |<span data-ttu-id="bc9f5-156">2</span><span class="sxs-lookup"><span data-stu-id="bc9f5-156">2</span></span> |<span data-ttu-id="bc9f5-157">4</span><span class="sxs-lookup"><span data-stu-id="bc9f5-157">4</span></span> |
| <span data-ttu-id="bc9f5-158">20150601</span><span class="sxs-lookup"><span data-stu-id="bc9f5-158">20150601</span></span> |<span data-ttu-id="bc9f5-159">2</span><span class="sxs-lookup"><span data-stu-id="bc9f5-159">2</span></span> |<span data-ttu-id="bc9f5-160">4</span><span class="sxs-lookup"><span data-stu-id="bc9f5-160">4</span></span> |
| <span data-ttu-id="bc9f5-161">20150701</span><span class="sxs-lookup"><span data-stu-id="bc9f5-161">20150701</span></span> |<span data-ttu-id="bc9f5-162">3</span><span class="sxs-lookup"><span data-stu-id="bc9f5-162">3</span></span> |<span data-ttu-id="bc9f5-163">1</span><span class="sxs-lookup"><span data-stu-id="bc9f5-163">1</span></span> |
| <span data-ttu-id="bc9f5-164">20150801</span><span class="sxs-lookup"><span data-stu-id="bc9f5-164">20150801</span></span> |<span data-ttu-id="bc9f5-165">3</span><span class="sxs-lookup"><span data-stu-id="bc9f5-165">3</span></span> |<span data-ttu-id="bc9f5-166">1</span><span class="sxs-lookup"><span data-stu-id="bc9f5-166">1</span></span> |
| <span data-ttu-id="bc9f5-167">20150801</span><span class="sxs-lookup"><span data-stu-id="bc9f5-167">20150801</span></span> |<span data-ttu-id="bc9f5-168">3</span><span class="sxs-lookup"><span data-stu-id="bc9f5-168">3</span></span> |<span data-ttu-id="bc9f5-169">1</span><span class="sxs-lookup"><span data-stu-id="bc9f5-169">1</span></span> |
| <span data-ttu-id="bc9f5-170">20151001</span><span class="sxs-lookup"><span data-stu-id="bc9f5-170">20151001</span></span> |<span data-ttu-id="bc9f5-171">4</span><span class="sxs-lookup"><span data-stu-id="bc9f5-171">4</span></span> |<span data-ttu-id="bc9f5-172">2</span><span class="sxs-lookup"><span data-stu-id="bc9f5-172">2</span></span> |
| <span data-ttu-id="bc9f5-173">20151101</span><span class="sxs-lookup"><span data-stu-id="bc9f5-173">20151101</span></span> |<span data-ttu-id="bc9f5-174">4</span><span class="sxs-lookup"><span data-stu-id="bc9f5-174">4</span></span> |<span data-ttu-id="bc9f5-175">2</span><span class="sxs-lookup"><span data-stu-id="bc9f5-175">2</span></span> |
| <span data-ttu-id="bc9f5-176">20151201</span><span class="sxs-lookup"><span data-stu-id="bc9f5-176">20151201</span></span> |<span data-ttu-id="bc9f5-177">4</span><span class="sxs-lookup"><span data-stu-id="bc9f5-177">4</span></span> |<span data-ttu-id="bc9f5-178">2</span><span class="sxs-lookup"><span data-stu-id="bc9f5-178">2</span></span> |

### <a name="step-4-create-statistics-on-your-newly-loaded-data"></a><span data-ttu-id="bc9f5-179">Krok 4: tworzenie statystyk na podstawie nowo załadowanych danych</span><span class="sxs-lookup"><span data-stu-id="bc9f5-179">Step 4: Create Statistics on your newly loaded data</span></span>
<span data-ttu-id="bc9f5-180">Usługa Azure SQL Data Warehouse nie obsługuje jeszcze automatycznego tworzenia ani aktualizowania statystyk.</span><span class="sxs-lookup"><span data-stu-id="bc9f5-180">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span> <span data-ttu-id="bc9f5-181">W kolejności tooget hello najlepszą wydajność zapytań należy utworzyć statystyki dla wszystkich kolumn wszystkich tabel po pierwszym załadowaniu hello lub każdej istotnej zmianie występują w danych hello.</span><span class="sxs-lookup"><span data-stu-id="bc9f5-181">In order tooget hello best performance from your queries, it's important that statistics be created on all columns of all tables after hello first load or any substantial changes occur in hello data.</span></span> <span data-ttu-id="bc9f5-182">Aby uzyskać szczegółowy opis statystyk, zobacz hello [statystyki] [ Statistics] tematu w hello grupie artykułów dla programistów.</span><span class="sxs-lookup"><span data-stu-id="bc9f5-182">For a detailed explanation of statistics, see hello [Statistics][Statistics] topic in hello Develop group of topics.</span></span> <span data-ttu-id="bc9f5-183">Poniżej przedstawiono sposób toocreate statystyk na powitania przedłożenia załadowany w tym przykładzie przedstawiono prosty przykład</span><span class="sxs-lookup"><span data-stu-id="bc9f5-183">Below is a quick example of how toocreate statistics on hello tabled loaded in this example</span></span>

<span data-ttu-id="bc9f5-184">Wykonaj następujące instrukcję CREATE STATISTICS w wierszu polecenia sqlcmd hello:</span><span class="sxs-lookup"><span data-stu-id="bc9f5-184">Execute hello following CREATE STATISTICS statements from a sqlcmd prompt:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    create statistics [DateId] on [DimDate2] ([DateId]);
    create statistics [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
    create statistics [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
"
```

## <a name="export-data-from-sql-data-warehouse"></a><span data-ttu-id="bc9f5-185">Eksportowanie danych z usługi SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="bc9f5-185">Export data from SQL Data Warehouse</span></span>
<span data-ttu-id="bc9f5-186">W tym samouczku utworzysz plik danych z tabeli w usłudze SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="bc9f5-186">In this tutorial, you will create a data file from a table in SQL Data Warehouse.</span></span> <span data-ttu-id="bc9f5-187">Firma Microsoft będzie eksportować hello wyeksportujemy dane utworzone powyżej tooa nowy plik danych o nazwie DimDate2_export.txt.</span><span class="sxs-lookup"><span data-stu-id="bc9f5-187">We will export hello data we created above tooa new data file called DimDate2_export.txt.</span></span>

### <a name="step-1-export-hello-data"></a><span data-ttu-id="bc9f5-188">Krok 1: Eksportowanie danych hello</span><span class="sxs-lookup"><span data-stu-id="bc9f5-188">Step 1: Export hello data</span></span>
<span data-ttu-id="bc9f5-189">Przy użyciu narzędzia bcp hello, możesz łączyć i wyeksportować dane za pomocą hello następujące polecenia zastąpienie wartości hello zależnie od potrzeb:</span><span class="sxs-lookup"><span data-stu-id="bc9f5-189">Using hello bcp utility, you can connect and export data using hello following command replacing hello values as appropriate:</span></span>

```sql
bcp DimDate2 out C:\Temp\DimDate2_export.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t ','
```
<span data-ttu-id="bc9f5-190">Możesz sprawdzić powitalne dane zostały poprawnie wyeksportowane, otwierając nowy plik hello.</span><span class="sxs-lookup"><span data-stu-id="bc9f5-190">You can verify hello data was exported correctly by opening hello new file.</span></span> <span data-ttu-id="bc9f5-191">Witaj dane w pliku hello powinny odpowiadać tekstowi hello poniżej:</span><span class="sxs-lookup"><span data-stu-id="bc9f5-191">hello data in hello file should match hello text below:</span></span>

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
> <span data-ttu-id="bc9f5-192">Powodu toohello specyfikę systemów rozproszonych kolejność danych hello nie może być takie same hello między bazami danych magazynu danych SQL.</span><span class="sxs-lookup"><span data-stu-id="bc9f5-192">Due toohello nature of distributed systems, hello data order may not be hello same across SQL Data Warehouse databases.</span></span> <span data-ttu-id="bc9f5-193">Innym rozwiązaniem jest toouse hello **queryout** funkcja toowrite bcp zapytanie wyodrębniające, zamiast eksportować całą tabelę hello.</span><span class="sxs-lookup"><span data-stu-id="bc9f5-193">Another option is toouse hello **queryout** function of bcp toowrite a query extract rather than export hello entire table.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="bc9f5-194">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="bc9f5-194">Next steps</span></span>
<span data-ttu-id="bc9f5-195">Omówienie ładowania można znaleźć w artykule [Ładowanie danych do usługi SQL Data Warehouse][Load data into SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="bc9f5-195">For an overview of loading, see [Load data into SQL Data Warehouse][Load data into SQL Data Warehouse].</span></span>
<span data-ttu-id="bc9f5-196">Więcej porad dla deweloperów znajduje się w artykule [Omówienie programowania w usłudze SQL Data Warehouse][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="bc9f5-196">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

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
