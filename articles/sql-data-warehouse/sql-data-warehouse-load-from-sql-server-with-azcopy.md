---
title: "aaaLoad danych z programu SQL Server do usługi Azure SQL Data Warehouse (PolyBase) | Dokumentacja firmy Microsoft"
description: "Używa bcp tooexport danych z plików tooflat programu SQL Server, magazynu obiektów blob tooAzure danych tooimport AZCopy i PolyBase tooingest hello danych do usługi Azure SQL Data Warehouse."
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
ms.openlocfilehash: 89e2a91bc97642e9fc18545cb802b42d8dc4ad95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-sql-server-into-azure-sql-data-warehouse-azcopy"></a><span data-ttu-id="4aef2-103">Ładowanie danych z programu SQL Server do usługi Azure SQL Data Warehouse (AZCopy)</span><span class="sxs-lookup"><span data-stu-id="4aef2-103">Load data from SQL Server into Azure SQL Data Warehouse (AZCopy)</span></span>
<span data-ttu-id="4aef2-104">Użyj narzędzia bcp i danych tooload narzędzia wiersza polecenia AZCopy z magazynu obiektów blob tooAzure programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="4aef2-104">Use bcp and AZCopy command-line utilities tooload data from SQL Server tooAzure blob storage.</span></span> <span data-ttu-id="4aef2-105">Następnie należy użyć danych hello tooload PolyBase lub fabrykę danych Azure do usługi Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="4aef2-105">Then use PolyBase or Azure Data Factory tooload hello data into Azure SQL Data Warehouse.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="4aef2-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="4aef2-106">Prerequisites</span></span>
<span data-ttu-id="4aef2-107">toostep opisanych w tym samouczku, potrzebne są:</span><span class="sxs-lookup"><span data-stu-id="4aef2-107">toostep through this tutorial, you need:</span></span>

* <span data-ttu-id="4aef2-108">Baza danych usługi SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="4aef2-108">A SQL Data Warehouse database</span></span>
* <span data-ttu-id="4aef2-109">zainstalowane narzędzie wiersza polecenia bcp Hello</span><span class="sxs-lookup"><span data-stu-id="4aef2-109">hello bcp command line utility installed</span></span>
* <span data-ttu-id="4aef2-110">Witaj zainstalowane narzędzie wiersza polecenia SQLCMD</span><span class="sxs-lookup"><span data-stu-id="4aef2-110">hello SQLCMD command line utility installed</span></span>

> [!NOTE]
> <span data-ttu-id="4aef2-111">Witaj narzędzia bcp i sqlcmd można pobrać z hello [Microsoft Download Center][Microsoft Download Center].</span><span class="sxs-lookup"><span data-stu-id="4aef2-111">You can download hello bcp and sqlcmd utilities from hello [Microsoft Download Center][Microsoft Download Center].</span></span>
> 
> 

## <a name="import-data-into-sql-data-warehouse"></a><span data-ttu-id="4aef2-112">Importowanie danych do usługi SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="4aef2-112">Import data into SQL Data Warehouse</span></span>
<span data-ttu-id="4aef2-113">W tym samouczku utworzysz tabelę w usłudze Azure SQL Data Warehouse i zaimportuj dane do tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="4aef2-113">In this tutorial, you will create a table in Azure SQL Data Warehouse and import data into hello table.</span></span>

### <a name="step-1-create-a-table-in-azure-sql-data-warehouse"></a><span data-ttu-id="4aef2-114">Krok 1: tworzenie tabeli w usłudze Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="4aef2-114">Step 1: Create a table in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="4aef2-115">Z wiersza polecenia użyj następującego zapytania toocreate tabeli w wystąpieniu hello toorun sqlcmd:</span><span class="sxs-lookup"><span data-stu-id="4aef2-115">From a command prompt, use sqlcmd toorun hello following query toocreate a table on your instance:</span></span>

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
> <span data-ttu-id="4aef2-116">Zobacz [omówienie tabeli] [ Table Overview] lub [składni polecenia CREATE TABLE] [ CREATE TABLE syntax] Aby uzyskać więcej informacji dotyczących tworzenia tabel SQL Data Warehouse i hello  Opcje dostępne w klauzuli WITH hello.</span><span class="sxs-lookup"><span data-stu-id="4aef2-116">See [Table Overview][Table Overview] or [CREATE TABLE syntax][CREATE TABLE syntax] for more information about creating a table on SQL Data Warehouse and hello  options available in hello WITH clause.</span></span>
> 
> 

### <a name="step-2-create-a-source-data-file"></a><span data-ttu-id="4aef2-117">Krok 2: tworzenie źródłowego pliku danych</span><span class="sxs-lookup"><span data-stu-id="4aef2-117">Step 2: Create a source data file</span></span>
<span data-ttu-id="4aef2-118">Otwórz hello Notatnik i skopiuj następujące wiersze danych do nowego pliku tekstowego, a następnie zapisz ten plik tooyour lokalnym katalogu tymczasowym, C:\Temp\DimDate2.txt.</span><span class="sxs-lookup"><span data-stu-id="4aef2-118">Open Notepad and copy hello following lines of data into a new text file and then save this file tooyour local temp directory, C:\Temp\DimDate2.txt.</span></span>

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
> <span data-ttu-id="4aef2-119">Jest ważne tooremember program bcp.exe nie obsługuje kodowania pliku hello UTF-8.</span><span class="sxs-lookup"><span data-stu-id="4aef2-119">It is important tooremember that bcp.exe does not support hello UTF-8 file encoding.</span></span> <span data-ttu-id="4aef2-120">Podczas korzystania z programu bcp.exe należy używać plików kodowanych w formacie ASCII lub UTF-16.</span><span class="sxs-lookup"><span data-stu-id="4aef2-120">Please use ASCII files or UTF-16 encoded files when using bcp.exe.</span></span>
> 
> 

### <a name="step-3-connect-and-import-hello-data"></a><span data-ttu-id="4aef2-121">Krok 3: Łączenie i zaimportuj dane hello</span><span class="sxs-lookup"><span data-stu-id="4aef2-121">Step 3: Connect and import hello data</span></span>
<span data-ttu-id="4aef2-122">Przy użyciu narzędzia bcp, możesz łączyć i zaimportować dane hello przy użyciu hello następujące polecenia zastąpienie wartości hello zależnie od potrzeb:</span><span class="sxs-lookup"><span data-stu-id="4aef2-122">Using bcp, you can connect and import hello data using hello following command replacing hello values as appropriate:</span></span>

```sql
bcp DimDate2 in C:\Temp\DimDate2.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t  ','
```

<span data-ttu-id="4aef2-123">Można sprawdzić hello załadowania danych, uruchamiając następujące zapytanie przy użyciu narzędzia sqlcmd hello:</span><span class="sxs-lookup"><span data-stu-id="4aef2-123">You can verify hello data was loaded by running hello following query using sqlcmd:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

<span data-ttu-id="4aef2-124">Powinny zostać zwrócone hello następujące wyniki:</span><span class="sxs-lookup"><span data-stu-id="4aef2-124">This should return hello following results:</span></span>

| <span data-ttu-id="4aef2-125">DateId</span><span class="sxs-lookup"><span data-stu-id="4aef2-125">DateId</span></span> | <span data-ttu-id="4aef2-126">CalendarQuarter</span><span class="sxs-lookup"><span data-stu-id="4aef2-126">CalendarQuarter</span></span> | <span data-ttu-id="4aef2-127">FiscalQuarter</span><span class="sxs-lookup"><span data-stu-id="4aef2-127">FiscalQuarter</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4aef2-128">20150101</span><span class="sxs-lookup"><span data-stu-id="4aef2-128">20150101</span></span> |<span data-ttu-id="4aef2-129">1</span><span class="sxs-lookup"><span data-stu-id="4aef2-129">1</span></span> |<span data-ttu-id="4aef2-130">3</span><span class="sxs-lookup"><span data-stu-id="4aef2-130">3</span></span> |
| <span data-ttu-id="4aef2-131">20150201</span><span class="sxs-lookup"><span data-stu-id="4aef2-131">20150201</span></span> |<span data-ttu-id="4aef2-132">1</span><span class="sxs-lookup"><span data-stu-id="4aef2-132">1</span></span> |<span data-ttu-id="4aef2-133">3</span><span class="sxs-lookup"><span data-stu-id="4aef2-133">3</span></span> |
| <span data-ttu-id="4aef2-134">20150301</span><span class="sxs-lookup"><span data-stu-id="4aef2-134">20150301</span></span> |<span data-ttu-id="4aef2-135">1</span><span class="sxs-lookup"><span data-stu-id="4aef2-135">1</span></span> |<span data-ttu-id="4aef2-136">3</span><span class="sxs-lookup"><span data-stu-id="4aef2-136">3</span></span> |
| <span data-ttu-id="4aef2-137">20150401</span><span class="sxs-lookup"><span data-stu-id="4aef2-137">20150401</span></span> |<span data-ttu-id="4aef2-138">2</span><span class="sxs-lookup"><span data-stu-id="4aef2-138">2</span></span> |<span data-ttu-id="4aef2-139">4</span><span class="sxs-lookup"><span data-stu-id="4aef2-139">4</span></span> |
| <span data-ttu-id="4aef2-140">20150501</span><span class="sxs-lookup"><span data-stu-id="4aef2-140">20150501</span></span> |<span data-ttu-id="4aef2-141">2</span><span class="sxs-lookup"><span data-stu-id="4aef2-141">2</span></span> |<span data-ttu-id="4aef2-142">4</span><span class="sxs-lookup"><span data-stu-id="4aef2-142">4</span></span> |
| <span data-ttu-id="4aef2-143">20150601</span><span class="sxs-lookup"><span data-stu-id="4aef2-143">20150601</span></span> |<span data-ttu-id="4aef2-144">2</span><span class="sxs-lookup"><span data-stu-id="4aef2-144">2</span></span> |<span data-ttu-id="4aef2-145">4</span><span class="sxs-lookup"><span data-stu-id="4aef2-145">4</span></span> |
| <span data-ttu-id="4aef2-146">20150701</span><span class="sxs-lookup"><span data-stu-id="4aef2-146">20150701</span></span> |<span data-ttu-id="4aef2-147">3</span><span class="sxs-lookup"><span data-stu-id="4aef2-147">3</span></span> |<span data-ttu-id="4aef2-148">1</span><span class="sxs-lookup"><span data-stu-id="4aef2-148">1</span></span> |
| <span data-ttu-id="4aef2-149">20150801</span><span class="sxs-lookup"><span data-stu-id="4aef2-149">20150801</span></span> |<span data-ttu-id="4aef2-150">3</span><span class="sxs-lookup"><span data-stu-id="4aef2-150">3</span></span> |<span data-ttu-id="4aef2-151">1</span><span class="sxs-lookup"><span data-stu-id="4aef2-151">1</span></span> |
| <span data-ttu-id="4aef2-152">20150801</span><span class="sxs-lookup"><span data-stu-id="4aef2-152">20150801</span></span> |<span data-ttu-id="4aef2-153">3</span><span class="sxs-lookup"><span data-stu-id="4aef2-153">3</span></span> |<span data-ttu-id="4aef2-154">1</span><span class="sxs-lookup"><span data-stu-id="4aef2-154">1</span></span> |
| <span data-ttu-id="4aef2-155">20151001</span><span class="sxs-lookup"><span data-stu-id="4aef2-155">20151001</span></span> |<span data-ttu-id="4aef2-156">4</span><span class="sxs-lookup"><span data-stu-id="4aef2-156">4</span></span> |<span data-ttu-id="4aef2-157">2</span><span class="sxs-lookup"><span data-stu-id="4aef2-157">2</span></span> |
| <span data-ttu-id="4aef2-158">20151101</span><span class="sxs-lookup"><span data-stu-id="4aef2-158">20151101</span></span> |<span data-ttu-id="4aef2-159">4</span><span class="sxs-lookup"><span data-stu-id="4aef2-159">4</span></span> |<span data-ttu-id="4aef2-160">2</span><span class="sxs-lookup"><span data-stu-id="4aef2-160">2</span></span> |
| <span data-ttu-id="4aef2-161">20151201</span><span class="sxs-lookup"><span data-stu-id="4aef2-161">20151201</span></span> |<span data-ttu-id="4aef2-162">4</span><span class="sxs-lookup"><span data-stu-id="4aef2-162">4</span></span> |<span data-ttu-id="4aef2-163">2</span><span class="sxs-lookup"><span data-stu-id="4aef2-163">2</span></span> |

### <a name="step-4-create-statistics-on-your-newly-loaded-data"></a><span data-ttu-id="4aef2-164">Krok 4: tworzenie statystyk na podstawie nowo załadowanych danych</span><span class="sxs-lookup"><span data-stu-id="4aef2-164">Step 4: Create Statistics on your newly loaded data</span></span>
<span data-ttu-id="4aef2-165">Usługa Azure SQL Data Warehouse nie obsługuje jeszcze automatycznego tworzenia ani aktualizowania statystyk.</span><span class="sxs-lookup"><span data-stu-id="4aef2-165">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span> <span data-ttu-id="4aef2-166">W kolejności tooget hello najlepszą wydajność zapytań należy utworzyć statystyki dla wszystkich kolumn wszystkich tabel po pierwszym załadowaniu hello lub każdej istotnej zmianie występują w danych hello.</span><span class="sxs-lookup"><span data-stu-id="4aef2-166">In order tooget hello best performance from your queries, it's important that statistics be created on all columns of all tables after hello first load or any substantial changes occur in hello data.</span></span> <span data-ttu-id="4aef2-167">Aby uzyskać szczegółowy opis statystyk, zobacz hello [statystyki] [ Statistics] tematu w hello grupie artykułów dla programistów.</span><span class="sxs-lookup"><span data-stu-id="4aef2-167">For a detailed explanation of statistics, see hello [Statistics][Statistics] topic in hello Develop group of topics.</span></span> <span data-ttu-id="4aef2-168">Poniżej przedstawiono sposób toocreate statystyk na powitania przedłożenia załadowany w tym przykładzie przedstawiono prosty przykład</span><span class="sxs-lookup"><span data-stu-id="4aef2-168">Below is a quick example of how toocreate statistics on hello tabled loaded in this example</span></span>

<span data-ttu-id="4aef2-169">Wykonaj następujące instrukcję CREATE STATISTICS w wierszu polecenia sqlcmd hello:</span><span class="sxs-lookup"><span data-stu-id="4aef2-169">Execute hello following CREATE STATISTICS statements from a sqlcmd prompt:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    create statistics [DateId] on [DimDate2] ([DateId]);
    create statistics [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
    create statistics [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
"
```

## <a name="export-data-from-sql-data-warehouse"></a><span data-ttu-id="4aef2-170">Eksportowanie danych z usługi SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="4aef2-170">Export data from SQL Data Warehouse</span></span>
<span data-ttu-id="4aef2-171">W tym samouczku utworzysz plik danych z tabeli w usłudze SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="4aef2-171">In this tutorial, you will create a data file from a table in SQL Data Warehouse.</span></span> <span data-ttu-id="4aef2-172">Firma Microsoft będzie eksportować hello wyeksportujemy dane utworzone powyżej tooa nowy plik danych o nazwie DimDate2_export.txt.</span><span class="sxs-lookup"><span data-stu-id="4aef2-172">We will export hello data we created above tooa new data file called DimDate2_export.txt.</span></span>

### <a name="step-1-export-hello-data"></a><span data-ttu-id="4aef2-173">Krok 1: Eksportowanie danych hello</span><span class="sxs-lookup"><span data-stu-id="4aef2-173">Step 1: Export hello data</span></span>
<span data-ttu-id="4aef2-174">Przy użyciu narzędzia bcp hello, możesz łączyć i wyeksportować dane za pomocą hello następujące polecenia zastąpienie wartości hello zależnie od potrzeb:</span><span class="sxs-lookup"><span data-stu-id="4aef2-174">Using hello bcp utility, you can connect and export data using hello following command replacing hello values as appropriate:</span></span>

```sql
bcp DimDate2 out C:\Temp\DimDate2_export.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t ','
```
<span data-ttu-id="4aef2-175">Możesz sprawdzić powitalne dane zostały poprawnie wyeksportowane, otwierając nowy plik hello.</span><span class="sxs-lookup"><span data-stu-id="4aef2-175">You can verify hello data was exported correctly by opening hello new file.</span></span> <span data-ttu-id="4aef2-176">Witaj dane w pliku hello powinny odpowiadać tekstowi hello poniżej:</span><span class="sxs-lookup"><span data-stu-id="4aef2-176">hello data in hello file should match hello text below:</span></span>

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
> <span data-ttu-id="4aef2-177">Powodu toohello specyfikę systemów rozproszonych kolejność danych hello nie może być takie same hello między bazami danych magazynu danych SQL.</span><span class="sxs-lookup"><span data-stu-id="4aef2-177">Due toohello nature of distributed systems, hello data order may not be hello same across SQL Data Warehouse databases.</span></span> <span data-ttu-id="4aef2-178">Innym rozwiązaniem jest toouse hello **queryout** funkcja toowrite bcp zapytanie wyodrębniające, zamiast eksportować całą tabelę hello.</span><span class="sxs-lookup"><span data-stu-id="4aef2-178">Another option is toouse hello **queryout** function of bcp toowrite a query extract rather than export hello entire table.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="4aef2-179">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4aef2-179">Next steps</span></span>
<span data-ttu-id="4aef2-180">Omówienie ładowania można znaleźć w artykule [Ładowanie danych do usługi SQL Data Warehouse][Load data into SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="4aef2-180">For an overview of loading, see [Load data into SQL Data Warehouse][Load data into SQL Data Warehouse].</span></span>
<span data-ttu-id="4aef2-181">Więcej porad dla deweloperów znajduje się w artykule [Omówienie programowania w usłudze SQL Data Warehouse][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="4aef2-181">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

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
