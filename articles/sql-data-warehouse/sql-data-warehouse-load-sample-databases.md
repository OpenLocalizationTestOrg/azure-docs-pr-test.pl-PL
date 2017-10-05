---
title: "Ładowanie przykładowych danych do usługi SQL Data Warehouse | Dokumentacja firmy Microsoft"
description: "Ładowanie przykładowych danych do usługi SQL Data Warehouse"
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: e338ecf8-cfee-419b-b7b6-98108d381c62
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 1e0df958a2f18fe1e988168918e5cfd293f84e64
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="load-sample-data-into-sql-data-warehouse"></a><span data-ttu-id="13085-103">Ładowanie przykładowych danych do usługi SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="13085-103">Load sample data into SQL Data Warehouse</span></span>
<span data-ttu-id="13085-104">Wykonaj poniższe kroki proste do ładowania i w bazie danych firmy Adventure Works próbki.</span><span class="sxs-lookup"><span data-stu-id="13085-104">Follow these simple steps to load and query the Adventure Works Sample database.</span></span> <span data-ttu-id="13085-105">Skrypty te należy najpierw użyć narzędzia sqlcmd można uruchomić programu SQL, co spowoduje utworzenie tabel i widoków.</span><span class="sxs-lookup"><span data-stu-id="13085-105">These scripts first use sqlcmd to run SQL which will create tables and views.</span></span> <span data-ttu-id="13085-106">Po utworzeniu tabel skrypty użyje bcp można załadować danych.</span><span class="sxs-lookup"><span data-stu-id="13085-106">Once tables have been created, the scripts will use bcp to load data.</span></span>  <span data-ttu-id="13085-107">Jeśli nie masz jeszcze sqlcmd i zainstalować narzędzia bcp, skorzystaj z poniższych linków, aby [zainstalować narzędzia bcp] [ install bcp] i [zainstalować narzędzia sqlcmd][install sqlcmd].</span><span class="sxs-lookup"><span data-stu-id="13085-107">If you don't already have sqlcmd and bcp installed, follow these links to [install bcp][install bcp] and to [install sqlcmd][install sqlcmd].</span></span>

## <a name="load-sample-data"></a><span data-ttu-id="13085-108">Ładuj dane przykładowe</span><span class="sxs-lookup"><span data-stu-id="13085-108">Load sample data</span></span>
1. <span data-ttu-id="13085-109">Pobierz [Adventure Works przykładowe skrypty dla usługi SQL Data Warehouse] [ Adventure Works Sample Scripts for SQL Data Warehouse] pliku zip.</span><span class="sxs-lookup"><span data-stu-id="13085-109">Download the [Adventure Works Sample Scripts for SQL Data Warehouse][Adventure Works Sample Scripts for SQL Data Warehouse] zip file.</span></span>
2. <span data-ttu-id="13085-110">Wyodrębnij pliki z pobranego zip do katalogu na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="13085-110">Extract the files from downloaded zip to a directory on your local machine.</span></span>
3. <span data-ttu-id="13085-111">Edytuj aw_create.bat wyodrębnionego pliku i ustaw następujące zmienne znajdujących się u góry pliku.</span><span class="sxs-lookup"><span data-stu-id="13085-111">Edit the extracted file aw_create.bat and set the following variables found at the top of the file.</span></span>  <span data-ttu-id="13085-112">Pamiętaj pozostawić nie spacji między "=" i parametr.</span><span class="sxs-lookup"><span data-stu-id="13085-112">Be sure to leave no whitespace between the "=" and the parameter.</span></span>  <span data-ttu-id="13085-113">Poniżej przedstawiono przykłady może wyglądać dokonanych zmian.</span><span class="sxs-lookup"><span data-stu-id="13085-113">Below are examples of how your edits might look.</span></span>
   
    ```
    server=mylogicalserver.database.windows.net
    user=mydwuser
    password=Mydwpassw0rd
    database=mydwdatabase
    ```
4. <span data-ttu-id="13085-114">W wierszu polecenia systemu Windows uruchom aw_create.bat edytowany.</span><span class="sxs-lookup"><span data-stu-id="13085-114">From a Windows cmd prompt, run the edited aw_create.bat.</span></span>  <span data-ttu-id="13085-115">Upewnij się, że jesteś w katalogu, w którym zapisano aw_create.bat Twojego zmodyfikowaną wersję.</span><span class="sxs-lookup"><span data-stu-id="13085-115">Be sure you are in the directory where you saved your edited version of aw_create.bat.</span></span>
   <span data-ttu-id="13085-116">Ten skrypt zostanie...</span><span class="sxs-lookup"><span data-stu-id="13085-116">This script will...</span></span>
   
   * <span data-ttu-id="13085-117">Upuść Adventure Works tabel ani widoków, które już istnieją w bazie danych</span><span class="sxs-lookup"><span data-stu-id="13085-117">Drop any Adventure Works tables or views that already exist in your database</span></span>
   * <span data-ttu-id="13085-118">Utwórz Adventure Works tabele i widoki</span><span class="sxs-lookup"><span data-stu-id="13085-118">Create the Adventure Works tables and views</span></span>
   * <span data-ttu-id="13085-119">Ładowanie każdej tabeli Adventure Works przy użyciu narzędzia bcp</span><span class="sxs-lookup"><span data-stu-id="13085-119">Load each Adventure Works table using bcp</span></span>
   * <span data-ttu-id="13085-120">Sprawdzanie poprawności liczby wierszy dla każdej tabeli Adventure Works</span><span class="sxs-lookup"><span data-stu-id="13085-120">Validate the row counts for each Adventure Works table</span></span>
   * <span data-ttu-id="13085-121">Zbieranie statystyk w każdej kolumnie dla każdej tabeli Adventure Works</span><span class="sxs-lookup"><span data-stu-id="13085-121">Collect statistics on every column for each Adventure Works table</span></span>

## <a name="query-sample-data"></a><span data-ttu-id="13085-122">Dane przykładowe zapytania</span><span class="sxs-lookup"><span data-stu-id="13085-122">Query sample data</span></span>
<span data-ttu-id="13085-123">Po przykładowych danych zostało załadowane do magazynu danych SQL, można szybko uruchomić kilka zapytań.</span><span class="sxs-lookup"><span data-stu-id="13085-123">Once you've loaded some sample data into your SQL Data Warehouse, you can quickly run a few queries.</span></span>  <span data-ttu-id="13085-124">Aby uruchomić kwerendę, połączyć się z nowo utworzone bazy danych firmy Adventure Works w magazynu danych SQL Azure za pomocą programu Visual Studio i narzędzi SSDT, zgodnie z opisem w [zapytania z programem Visual Studio] [ query with Visual Studio] dokumentu.</span><span class="sxs-lookup"><span data-stu-id="13085-124">To run a query, connect to your newly created Adventure Works database in Azure SQL DW using Visual Studio and SSDT, as described in the [query with Visual Studio][query with Visual Studio] document.</span></span>

<span data-ttu-id="13085-125">Przykład prostego instrukcji select, aby uzyskać wszystkie informacje o pracowników:</span><span class="sxs-lookup"><span data-stu-id="13085-125">Example of simple select statement to get all the info of the employees:</span></span>

```sql
SELECT * FROM DimEmployee;
```

<span data-ttu-id="13085-126">Przykład bardziej złożonego zapytania przy użyciu konstrukcji, takich jak GROUP BY aby przyjrzeć się suma wszystkich sprzedaży każdego dnia:</span><span class="sxs-lookup"><span data-stu-id="13085-126">Example of a more complex query using constructs such as GROUP BY to look at the total amount for all sales on each day:</span></span>

```sql
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales
FROM FactInternetSales
GROUP BY OrderDateKey
ORDER BY OrderDateKey;
```

<span data-ttu-id="13085-127">Przykład SELECT z klauzulą WHERE filtrowanie zleceń przed określonej daty:</span><span class="sxs-lookup"><span data-stu-id="13085-127">Example of a SELECT with a WHERE clause to filter out orders from before a certain date:</span></span>

```
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales
FROM FactInternetSales
WHERE OrderDateKey > '20020801'
GROUP BY OrderDateKey
ORDER BY OrderDateKey;
```

<span data-ttu-id="13085-128">Magazyn danych SQL obsługuje prawie wszystkie konstrukcje T-SQL, które obsługuje program SQL Server.</span><span class="sxs-lookup"><span data-stu-id="13085-128">SQL Data Warehouse supports almost all T-SQL constructs which SQL Server supports.</span></span>  <span data-ttu-id="13085-129">Różnice są udokumentowane w naszym [Migrowanie kodu] [ migrate code] dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="13085-129">Any differences are documented in our [migrate code][migrate code] documentation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="13085-130">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="13085-130">Next steps</span></span>
<span data-ttu-id="13085-131">Skoro już wcześniej masz szansę wypróbować kilka zapytań z przykładowymi danymi, sprawdź informacje dotyczące sposobu [opracowanie][develop], [załadować][load], lub [ Migrowanie] [ migrate] SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="13085-131">Now that you've had a chance to try some queries with sample data, check out how to [develop][develop], [load][load], or [migrate][migrate] to SQL Data Warehouse.</span></span>

<!--Image references-->

<!--Article references-->
[migrate]: sql-data-warehouse-overview-migrate.md
[develop]: sql-data-warehouse-overview-develop.md
[load]: sql-data-warehouse-overview-load.md
[query with Visual Studio]: sql-data-warehouse-query-visual-studio.md
[migrate code]: sql-data-warehouse-migrate-code.md
[install bcp]: sql-data-warehouse-load-with-bcp.md
[install sqlcmd]: sql-data-warehouse-get-started-connect-sqlcmd.md

<!--Other Web references-->
[Adventure Works Sample Scripts for SQL Data Warehouse]: https://migrhoststorage.blob.core.windows.net/sqldwsample/AdventureWorksSQLDW2012.zip
