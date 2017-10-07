---
title: plik danych aaaLoad z pliku CSV do bazy danych SQL Azure (bcp) | Dokumentacja firmy Microsoft
description: "Rozmiar danych w małych używa bcp tooimport danych do bazy danych SQL Azure."
services: sql-database
documentationcenter: NA
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 875f9b8d-f1a1-4895-b717-f45570fb7f80
ms.service: sql-database
ms.custom: load & move data
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 01/10/2017
ms.author: carlrab
ms.openlocfilehash: 9350e459aa844223820fbbd849a830cf0354d4e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-csv-into-azure-sql-database-flat-files"></a><span data-ttu-id="082f2-103">Ładowanie danych z pliku CSV do usługi Azure SQL Database (pliki proste)</span><span class="sxs-lookup"><span data-stu-id="082f2-103">Load data from CSV into Azure SQL Database (flat files)</span></span>
<span data-ttu-id="082f2-104">W bazie danych SQL Azure, można użyć danych tooimport narzędzia wiersza polecenia bcp hello z pliku CSV.</span><span class="sxs-lookup"><span data-stu-id="082f2-104">You can use hello bcp command-line utility tooimport data from a CSV file into Azure SQL Database.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="082f2-105">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="082f2-105">Before you begin</span></span>
### <a name="prerequisites"></a><span data-ttu-id="082f2-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="082f2-106">Prerequisites</span></span>
<span data-ttu-id="082f2-107">Witaj toocomplete kroków w tym artykule, należy:</span><span class="sxs-lookup"><span data-stu-id="082f2-107">toocomplete hello steps in this article, you need:</span></span>

* <span data-ttu-id="082f2-108">Serwer logiczny i baza danych usługi Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="082f2-108">An Azure SQL Database logical server and database</span></span>
* <span data-ttu-id="082f2-109">Narzędzie wiersza polecenia bcp Hello zainstalowany</span><span class="sxs-lookup"><span data-stu-id="082f2-109">hello bcp command-line utility installed</span></span>
* <span data-ttu-id="082f2-110">narzędzia wiersza polecenia sqlcmd Hello zainstalowany</span><span class="sxs-lookup"><span data-stu-id="082f2-110">hello sqlcmd command-line utility installed</span></span>

<span data-ttu-id="082f2-111">Witaj narzędzia bcp i sqlcmd można pobrać z hello [Microsoft Download Center][Microsoft Download Center].</span><span class="sxs-lookup"><span data-stu-id="082f2-111">You can download hello bcp and sqlcmd utilities from hello [Microsoft Download Center][Microsoft Download Center].</span></span>

### <a name="data-in-ascii-or-utf-16-format"></a><span data-ttu-id="082f2-112">Dane w formacie ASCII lub UTF-16</span><span class="sxs-lookup"><span data-stu-id="082f2-112">Data in ASCII or UTF-16 format</span></span>
<span data-ttu-id="082f2-113">W przypadku tego samouczka z użyciem własnych danych, dane wymagają toouse hello ASCII lub kodowania UTF-16, ponieważ narzędzie bcp nie obsługuje UTF-8.</span><span class="sxs-lookup"><span data-stu-id="082f2-113">If you are trying this tutorial with your own data, your data needs toouse hello ASCII or UTF-16 encoding since bcp does not support UTF-8.</span></span> 

## <a name="1-create-a-destination-table"></a><span data-ttu-id="082f2-114">1. Tworzenie tabeli docelowej</span><span class="sxs-lookup"><span data-stu-id="082f2-114">1. Create a destination table</span></span>
<span data-ttu-id="082f2-115">Zdefiniuj tabelę w bazie danych SQL jako hello tabeli docelowej.</span><span class="sxs-lookup"><span data-stu-id="082f2-115">Define a table in SQL Database as hello destination table.</span></span> <span data-ttu-id="082f2-116">Witaj kolumn w tabeli hello musi odpowiadać toohello danych w poszczególnych wierszach pliku danych.</span><span class="sxs-lookup"><span data-stu-id="082f2-116">hello columns in hello table must correspond toohello data in each row of your data file.</span></span>

<span data-ttu-id="082f2-117">toocreate tabelę, otwórz wiersz polecenia i użyj hello toorun sqlcmd.exe następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="082f2-117">toocreate a table, open a command prompt and use sqlcmd.exe toorun hello following command:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    CREATE TABLE DimDate2
    (
        DateId INT NOT NULL,
        CalendarQuarter TINYINT NOT NULL,
        FiscalQuarter TINYINT NOT NULL
    )
    ;
"
```


## <a name="2-create-a-source-data-file"></a><span data-ttu-id="082f2-118">2. Tworzenie źródłowego pliku danych</span><span class="sxs-lookup"><span data-stu-id="082f2-118">2. Create a source data file</span></span>
<span data-ttu-id="082f2-119">Otwórz hello Notatnik i skopiuj następujące wiersze danych do nowego pliku tekstowego, a następnie zapisz ten plik tooyour lokalnym katalogu tymczasowym, C:\Temp\DimDate2.txt.</span><span class="sxs-lookup"><span data-stu-id="082f2-119">Open Notepad and copy hello following lines of data into a new text file and then save this file tooyour local temp directory, C:\Temp\DimDate2.txt.</span></span> <span data-ttu-id="082f2-120">Te dane są w formacie ASCII.</span><span class="sxs-lookup"><span data-stu-id="082f2-120">This data is in ASCII format.</span></span>

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

<span data-ttu-id="082f2-121">(Opcjonalnie) tooexport dane z bazy danych programu SQL Server otwórz wiersz polecenia i uruchom następujące polecenie hello.</span><span class="sxs-lookup"><span data-stu-id="082f2-121">(Optional) tooexport your own data from a SQL Server database, open a command prompt and run hello following command.</span></span> <span data-ttu-id="082f2-122">Zastąp parametry TableName, ServerName, DatabaseName, Username i Password odpowiednimi informacjami.</span><span class="sxs-lookup"><span data-stu-id="082f2-122">Replace TableName, ServerName, DatabaseName, Username, and Password with your own information.</span></span>

```bcp
bcp <TableName> out C:\Temp\DimDate2_export.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <Password> -q -c -t , 
```

## <a name="3-load-hello-data"></a><span data-ttu-id="082f2-123">3. Ładowanie danych hello</span><span class="sxs-lookup"><span data-stu-id="082f2-123">3. Load hello data</span></span>
<span data-ttu-id="082f2-124">tooload hello danych, otwórz wiersz polecenia i uruchom hello następujące polecenie, zastępując hello wartości dla nazwy serwera, nazwę bazy danych, nazwę użytkownika i hasło z odpowiednimi informacjami.</span><span class="sxs-lookup"><span data-stu-id="082f2-124">tooload hello data, open a command prompt and run hello following command, replacing hello values for Server Name, Database name, Username, and Password with your own information.</span></span>

```bcp
bcp DimDate2 in C:\Temp\DimDate2.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <password> -q -c -t  ,
```

<span data-ttu-id="082f2-125">Użyj tego polecenia tooverify hello dane zostały załadowane poprawnie</span><span class="sxs-lookup"><span data-stu-id="082f2-125">Use this command tooverify hello data was loaded properly</span></span>

```bcp
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

<span data-ttu-id="082f2-126">Witaj wyniki powinny wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="082f2-126">hello results should look like this:</span></span>

| <span data-ttu-id="082f2-127">DateId</span><span class="sxs-lookup"><span data-stu-id="082f2-127">DateId</span></span> | <span data-ttu-id="082f2-128">CalendarQuarter</span><span class="sxs-lookup"><span data-stu-id="082f2-128">CalendarQuarter</span></span> | <span data-ttu-id="082f2-129">FiscalQuarter</span><span class="sxs-lookup"><span data-stu-id="082f2-129">FiscalQuarter</span></span> |
| --- | --- | --- |
| <span data-ttu-id="082f2-130">20150101</span><span class="sxs-lookup"><span data-stu-id="082f2-130">20150101</span></span> |<span data-ttu-id="082f2-131">1</span><span class="sxs-lookup"><span data-stu-id="082f2-131">1</span></span> |<span data-ttu-id="082f2-132">3</span><span class="sxs-lookup"><span data-stu-id="082f2-132">3</span></span> |
| <span data-ttu-id="082f2-133">20150201</span><span class="sxs-lookup"><span data-stu-id="082f2-133">20150201</span></span> |<span data-ttu-id="082f2-134">1</span><span class="sxs-lookup"><span data-stu-id="082f2-134">1</span></span> |<span data-ttu-id="082f2-135">3</span><span class="sxs-lookup"><span data-stu-id="082f2-135">3</span></span> |
| <span data-ttu-id="082f2-136">20150301</span><span class="sxs-lookup"><span data-stu-id="082f2-136">20150301</span></span> |<span data-ttu-id="082f2-137">1</span><span class="sxs-lookup"><span data-stu-id="082f2-137">1</span></span> |<span data-ttu-id="082f2-138">3</span><span class="sxs-lookup"><span data-stu-id="082f2-138">3</span></span> |
| <span data-ttu-id="082f2-139">20150401</span><span class="sxs-lookup"><span data-stu-id="082f2-139">20150401</span></span> |<span data-ttu-id="082f2-140">2</span><span class="sxs-lookup"><span data-stu-id="082f2-140">2</span></span> |<span data-ttu-id="082f2-141">4</span><span class="sxs-lookup"><span data-stu-id="082f2-141">4</span></span> |
| <span data-ttu-id="082f2-142">20150501</span><span class="sxs-lookup"><span data-stu-id="082f2-142">20150501</span></span> |<span data-ttu-id="082f2-143">2</span><span class="sxs-lookup"><span data-stu-id="082f2-143">2</span></span> |<span data-ttu-id="082f2-144">4</span><span class="sxs-lookup"><span data-stu-id="082f2-144">4</span></span> |
| <span data-ttu-id="082f2-145">20150601</span><span class="sxs-lookup"><span data-stu-id="082f2-145">20150601</span></span> |<span data-ttu-id="082f2-146">2</span><span class="sxs-lookup"><span data-stu-id="082f2-146">2</span></span> |<span data-ttu-id="082f2-147">4</span><span class="sxs-lookup"><span data-stu-id="082f2-147">4</span></span> |
| <span data-ttu-id="082f2-148">20150701</span><span class="sxs-lookup"><span data-stu-id="082f2-148">20150701</span></span> |<span data-ttu-id="082f2-149">3</span><span class="sxs-lookup"><span data-stu-id="082f2-149">3</span></span> |<span data-ttu-id="082f2-150">1</span><span class="sxs-lookup"><span data-stu-id="082f2-150">1</span></span> |
| <span data-ttu-id="082f2-151">20150801</span><span class="sxs-lookup"><span data-stu-id="082f2-151">20150801</span></span> |<span data-ttu-id="082f2-152">3</span><span class="sxs-lookup"><span data-stu-id="082f2-152">3</span></span> |<span data-ttu-id="082f2-153">1</span><span class="sxs-lookup"><span data-stu-id="082f2-153">1</span></span> |
| <span data-ttu-id="082f2-154">20150801</span><span class="sxs-lookup"><span data-stu-id="082f2-154">20150801</span></span> |<span data-ttu-id="082f2-155">3</span><span class="sxs-lookup"><span data-stu-id="082f2-155">3</span></span> |<span data-ttu-id="082f2-156">1</span><span class="sxs-lookup"><span data-stu-id="082f2-156">1</span></span> |
| <span data-ttu-id="082f2-157">20151001</span><span class="sxs-lookup"><span data-stu-id="082f2-157">20151001</span></span> |<span data-ttu-id="082f2-158">4</span><span class="sxs-lookup"><span data-stu-id="082f2-158">4</span></span> |<span data-ttu-id="082f2-159">2</span><span class="sxs-lookup"><span data-stu-id="082f2-159">2</span></span> |
| <span data-ttu-id="082f2-160">20151101</span><span class="sxs-lookup"><span data-stu-id="082f2-160">20151101</span></span> |<span data-ttu-id="082f2-161">4</span><span class="sxs-lookup"><span data-stu-id="082f2-161">4</span></span> |<span data-ttu-id="082f2-162">2</span><span class="sxs-lookup"><span data-stu-id="082f2-162">2</span></span> |
| <span data-ttu-id="082f2-163">20151201</span><span class="sxs-lookup"><span data-stu-id="082f2-163">20151201</span></span> |<span data-ttu-id="082f2-164">4</span><span class="sxs-lookup"><span data-stu-id="082f2-164">4</span></span> |<span data-ttu-id="082f2-165">2</span><span class="sxs-lookup"><span data-stu-id="082f2-165">2</span></span> |

## <a name="next-steps"></a><span data-ttu-id="082f2-166">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="082f2-166">Next steps</span></span>
<span data-ttu-id="082f2-167">toomigrate bazy danych programu SQL Server, zobacz [migracja bazy danych programu SQL Server](sql-database-cloud-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="082f2-167">toomigrate a SQL Server database, see [SQL Server database migration](sql-database-cloud-migrate.md).</span></span>

<!--MSDN references-->
[bcp]: https://msdn.microsoft.com/library/ms162802.aspx
[CREATE TABLE syntax]: https://msdn.microsoft.com/library/mt203953.aspx

<!--Other Web references-->
[Microsoft Download Center]: https://www.microsoft.com/download/details.aspx?id=36433
