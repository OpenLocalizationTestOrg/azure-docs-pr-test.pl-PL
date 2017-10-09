---
title: "aaaLoad przykładowych danych do usługi SQL Data Warehouse | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 3459c42f3aae51c27fd35db7874faf99e1e577e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="load-sample-data-into-sql-data-warehouse"></a><span data-ttu-id="b4c08-103">Ładowanie przykładowych danych do usługi SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="b4c08-103">Load sample data into SQL Data Warehouse</span></span>
<span data-ttu-id="b4c08-104">Wykonaj te tooload prostych kroków i bazy danych firmy Adventure Works próbki hello zapytania.</span><span class="sxs-lookup"><span data-stu-id="b4c08-104">Follow these simple steps tooload and query hello Adventure Works Sample database.</span></span> <span data-ttu-id="b4c08-105">Skrypty te należy najpierw użyć narzędzia sqlcmd toorun SQL, co spowoduje utworzenie tabel i widoków.</span><span class="sxs-lookup"><span data-stu-id="b4c08-105">These scripts first use sqlcmd toorun SQL which will create tables and views.</span></span> <span data-ttu-id="b4c08-106">Po utworzeniu tabel skrypty hello użyje bcp tooload danych.</span><span class="sxs-lookup"><span data-stu-id="b4c08-106">Once tables have been created, hello scripts will use bcp tooload data.</span></span>  <span data-ttu-id="b4c08-107">Jeśli nie masz jeszcze sqlcmd i zainstalować narzędzia bcp, skorzystaj z poniższych linków za[zainstalować narzędzia bcp] [ install bcp] i zbyt[zainstalować narzędzia sqlcmd][install sqlcmd].</span><span class="sxs-lookup"><span data-stu-id="b4c08-107">If you don't already have sqlcmd and bcp installed, follow these links too[install bcp][install bcp] and too[install sqlcmd][install sqlcmd].</span></span>

## <a name="load-sample-data"></a><span data-ttu-id="b4c08-108">Ładuj dane przykładowe</span><span class="sxs-lookup"><span data-stu-id="b4c08-108">Load sample data</span></span>
1. <span data-ttu-id="b4c08-109">Pobierz hello [Adventure Works przykładowe skrypty dla usługi SQL Data Warehouse] [ Adventure Works Sample Scripts for SQL Data Warehouse] pliku zip.</span><span class="sxs-lookup"><span data-stu-id="b4c08-109">Download hello [Adventure Works Sample Scripts for SQL Data Warehouse][Adventure Works Sample Scripts for SQL Data Warehouse] zip file.</span></span>
2. <span data-ttu-id="b4c08-110">Wyodrębnij pliki hello z katalogu tooa zip pobranego na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="b4c08-110">Extract hello files from downloaded zip tooa directory on your local machine.</span></span>
3. <span data-ttu-id="b4c08-111">Edytuj hello wyodrębniony plik aw_create.bat i ustaw następujące zmienne u góry pliku hello hello hello.</span><span class="sxs-lookup"><span data-stu-id="b4c08-111">Edit hello extracted file aw_create.bat and set hello following variables found at hello top of hello file.</span></span>  <span data-ttu-id="b4c08-112">Można tooleave się nie spacji między hello "=" i hello parametru.</span><span class="sxs-lookup"><span data-stu-id="b4c08-112">Be sure tooleave no whitespace between hello "=" and hello parameter.</span></span>  <span data-ttu-id="b4c08-113">Poniżej przedstawiono przykłady może wyglądać dokonanych zmian.</span><span class="sxs-lookup"><span data-stu-id="b4c08-113">Below are examples of how your edits might look.</span></span>
   
    ```
    server=mylogicalserver.database.windows.net
    user=mydwuser
    password=Mydwpassw0rd
    database=mydwdatabase
    ```
4. <span data-ttu-id="b4c08-114">W wierszu polecenia systemu Windows uruchom aw_create.bat hello edytować.</span><span class="sxs-lookup"><span data-stu-id="b4c08-114">From a Windows cmd prompt, run hello edited aw_create.bat.</span></span>  <span data-ttu-id="b4c08-115">Upewnij się, że znajdują się w katalogu hello, w którym zapisano aw_create.bat Twojego zmodyfikowaną wersję.</span><span class="sxs-lookup"><span data-stu-id="b4c08-115">Be sure you are in hello directory where you saved your edited version of aw_create.bat.</span></span>
   <span data-ttu-id="b4c08-116">Ten skrypt zostanie...</span><span class="sxs-lookup"><span data-stu-id="b4c08-116">This script will...</span></span>
   
   * <span data-ttu-id="b4c08-117">Upuść Adventure Works tabel ani widoków, które już istnieją w bazie danych</span><span class="sxs-lookup"><span data-stu-id="b4c08-117">Drop any Adventure Works tables or views that already exist in your database</span></span>
   * <span data-ttu-id="b4c08-118">Utwórz hello Adventure Works tabele i widoki</span><span class="sxs-lookup"><span data-stu-id="b4c08-118">Create hello Adventure Works tables and views</span></span>
   * <span data-ttu-id="b4c08-119">Ładowanie każdej tabeli Adventure Works przy użyciu narzędzia bcp</span><span class="sxs-lookup"><span data-stu-id="b4c08-119">Load each Adventure Works table using bcp</span></span>
   * <span data-ttu-id="b4c08-120">Sprawdź poprawność hello liczb wierszy dla każdej tabeli Adventure Works</span><span class="sxs-lookup"><span data-stu-id="b4c08-120">Validate hello row counts for each Adventure Works table</span></span>
   * <span data-ttu-id="b4c08-121">Zbieranie statystyk w każdej kolumnie dla każdej tabeli Adventure Works</span><span class="sxs-lookup"><span data-stu-id="b4c08-121">Collect statistics on every column for each Adventure Works table</span></span>

## <a name="query-sample-data"></a><span data-ttu-id="b4c08-122">Dane przykładowe zapytania</span><span class="sxs-lookup"><span data-stu-id="b4c08-122">Query sample data</span></span>
<span data-ttu-id="b4c08-123">Po przykładowych danych zostało załadowane do magazynu danych SQL, można szybko uruchomić kilka zapytań.</span><span class="sxs-lookup"><span data-stu-id="b4c08-123">Once you've loaded some sample data into your SQL Data Warehouse, you can quickly run a few queries.</span></span>  <span data-ttu-id="b4c08-124">toorun kwerendy, połączenia bazy danych firmy Adventure Works tooyour nowo utworzonego w magazynie danych SQL Azure za pomocą programu Visual Studio i narzędzi SSDT, zgodnie z opisem w hello [zapytania z programem Visual Studio] [ query with Visual Studio] dokumentu.</span><span class="sxs-lookup"><span data-stu-id="b4c08-124">toorun a query, connect tooyour newly created Adventure Works database in Azure SQL DW using Visual Studio and SSDT, as described in hello [query with Visual Studio][query with Visual Studio] document.</span></span>

<span data-ttu-id="b4c08-125">Przykładem prostej wybierz tooget instrukcji wszystkie informacje hello hello pracowników:</span><span class="sxs-lookup"><span data-stu-id="b4c08-125">Example of simple select statement tooget all hello info of hello employees:</span></span>

```sql
SELECT * FROM DimEmployee;
```

<span data-ttu-id="b4c08-126">Przykład bardziej złożonego zapytania używając konstrukcji, takich jak toolook GROUP BY w hello łączna kwota sprzedaży wszystkich każdego dnia:</span><span class="sxs-lookup"><span data-stu-id="b4c08-126">Example of a more complex query using constructs such as GROUP BY toolook at hello total amount for all sales on each day:</span></span>

```sql
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales
FROM FactInternetSales
GROUP BY OrderDateKey
ORDER BY OrderDateKey;
```

<span data-ttu-id="b4c08-127">Przykład SELECT z toofilter klauzuli WHERE, limit zamówień z przed określonej daty:</span><span class="sxs-lookup"><span data-stu-id="b4c08-127">Example of a SELECT with a WHERE clause toofilter out orders from before a certain date:</span></span>

```
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales
FROM FactInternetSales
WHERE OrderDateKey > '20020801'
GROUP BY OrderDateKey
ORDER BY OrderDateKey;
```

<span data-ttu-id="b4c08-128">Magazyn danych SQL obsługuje prawie wszystkie konstrukcje T-SQL, które obsługuje program SQL Server.</span><span class="sxs-lookup"><span data-stu-id="b4c08-128">SQL Data Warehouse supports almost all T-SQL constructs which SQL Server supports.</span></span>  <span data-ttu-id="b4c08-129">Różnice są udokumentowane w naszym [Migrowanie kodu] [ migrate code] dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="b4c08-129">Any differences are documented in our [migrate code][migrate code] documentation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b4c08-130">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b4c08-130">Next steps</span></span>
<span data-ttu-id="b4c08-131">Teraz, gdy użytkownik miał tootry szansy kilka zapytań z przykładowymi danymi, sprawdź, jak za[opracowanie][develop], [załadować][load], lub [ Migrowanie] [ migrate] tooSQL hurtowni danych.</span><span class="sxs-lookup"><span data-stu-id="b4c08-131">Now that you've had a chance tootry some queries with sample data, check out how too[develop][develop], [load][load], or [migrate][migrate] tooSQL Data Warehouse.</span></span>

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
