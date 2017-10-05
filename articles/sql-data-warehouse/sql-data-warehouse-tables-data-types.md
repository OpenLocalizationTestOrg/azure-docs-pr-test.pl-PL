---
title: "Typy danych wskazówki - Azure SQL Data Warehouse | Dokumentacja firmy Microsoft"
description: "Zalecenia dotyczące Definiowanie typów danych, które są zgodne z usługą Magazyn danych SQL."
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: barbkess
editor: 
ms.assetid: d4a1f0a3-ba9f-44b9-95f6-16a4f30746d6
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 06/02/2017
ms.author: shigu;barbkess
ms.openlocfilehash: 5c24c71af16bd9851d9caf15fecfa4bb76f5f77e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="guidance-for-defining-data-types-for-tables-in-sql-data-warehouse"></a><span data-ttu-id="3b74b-103">Wskazówki dotyczące definiowania typów danych w przypadku tabel w usłudze SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="3b74b-103">Guidance for defining data types for tables in SQL Data Warehouse</span></span>
<span data-ttu-id="3b74b-104">Zalecenia te umożliwiają definiowanie typów danych tabeli, które są zgodne z usługą Magazyn danych SQL.</span><span class="sxs-lookup"><span data-stu-id="3b74b-104">Use these recommendations to define table data types that are compatible with SQL Data Warehouse.</span></span> <span data-ttu-id="3b74b-105">Oprócz zgodności minimalizując rozmiar typów danych o poprawia wydajność kwerend.</span><span class="sxs-lookup"><span data-stu-id="3b74b-105">In addition to compatibility, minimizing the size of data types improves query performance.</span></span>

<span data-ttu-id="3b74b-106">Magazyn danych SQL obsługuje najczęściej używane typy danych.</span><span class="sxs-lookup"><span data-stu-id="3b74b-106">SQL Data Warehouse supports the most commonly used data types.</span></span> <span data-ttu-id="3b74b-107">Aby uzyskać listę obsługiwanych typów danych, zobacz [typy danych](/sql/docs/t-sql/statements/create-table-azure-sql-data-warehouse.md#datatypes) w instrukcji CREATE TABLE.</span><span class="sxs-lookup"><span data-stu-id="3b74b-107">For a list of the supported data types, see [data types](/sql/docs/t-sql/statements/create-table-azure-sql-data-warehouse.md#datatypes) in the CREATE TABLE statement.</span></span> 


## <a name="minimize-row-length"></a><span data-ttu-id="3b74b-108">Minimalizowanie długość wiersza</span><span class="sxs-lookup"><span data-stu-id="3b74b-108">Minimize row length</span></span>
<span data-ttu-id="3b74b-109">Minimalizowanie rozmiar typów danych o skraca długość wiersza, co prowadzi do poprawy wydajności zapytania.</span><span class="sxs-lookup"><span data-stu-id="3b74b-109">Minimizing the size of data types shortens the row length, which leads to better query performance.</span></span> <span data-ttu-id="3b74b-110">Użyj najmniejszą typu danych, który działa danych.</span><span class="sxs-lookup"><span data-stu-id="3b74b-110">Use the smallest data type that works for your data.</span></span> 

- <span data-ttu-id="3b74b-111">Unikaj definiowania kolumn znakowych o długości dużych domyślne.</span><span class="sxs-lookup"><span data-stu-id="3b74b-111">Avoid defining character columns with a large default length.</span></span> <span data-ttu-id="3b74b-112">Na przykład jeśli wartość najdłuższym 25 znaków, następnie zdefiniuj kolumny jako VARCHAR(25).</span><span class="sxs-lookup"><span data-stu-id="3b74b-112">For example, if the longest value is 25 characters, then define your column as VARCHAR(25).</span></span> 
- <span data-ttu-id="3b74b-113">Unikaj używania [NVARCHAR] [ NVARCHAR] potrzebne tylko VARCHAR.</span><span class="sxs-lookup"><span data-stu-id="3b74b-113">Avoid using [NVARCHAR][NVARCHAR] when you only need VARCHAR.</span></span>
- <span data-ttu-id="3b74b-114">Jeśli to możliwe, zamiast VARCHAR(MAX) lub NVARCHAR(MAX), albo użyć NVARCHAR(4000) lub VARCHAR(8000).</span><span class="sxs-lookup"><span data-stu-id="3b74b-114">When possible, use NVARCHAR(4000) or VARCHAR(8000) instead of NVARCHAR(MAX) or VARCHAR(MAX).</span></span>

<span data-ttu-id="3b74b-115">Jeśli używasz programu Polybase można załadować tabel, określona długość wiersza tabeli nie może przekraczać 1 MB.</span><span class="sxs-lookup"><span data-stu-id="3b74b-115">If you are using Polybase to load your tables, the defined length of the table row cannot exceed 1 MB.</span></span> <span data-ttu-id="3b74b-116">Jeśli wiersz o zmiennej długości danych przekracza 1 MB, można załadować wiersza za pomocą narzędzia BCP, ale nie przy użyciu programu PolyBase.</span><span class="sxs-lookup"><span data-stu-id="3b74b-116">When a row with variable-length data exceeds 1 MB, you can load the row with BCP, but not with PolyBase.</span></span>

## <a name="identify-unsupported-data-types"></a><span data-ttu-id="3b74b-117">Zidentyfikuj nieobsługiwane typy danych</span><span class="sxs-lookup"><span data-stu-id="3b74b-117">Identify unsupported data types</span></span>
<span data-ttu-id="3b74b-118">W przypadku migracji z innej bazy danych SQL bazy danych, może wystąpić typy danych, które nie są obsługiwane w usłudze SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="3b74b-118">If you are migrating your database from another SQL database, you might encounter data types that are not supported in SQL Data Warehouse.</span></span> <span data-ttu-id="3b74b-119">Skorzystaj z tej kwerendy, aby odnaleźć nieobsługiwane typy danych w istniejącej schematu SQL.</span><span class="sxs-lookup"><span data-stu-id="3b74b-119">Use this query to discover unsupported data types in your existing SQL schema.</span></span>

```sql
SELECT  t.[name], c.[name], c.[system_type_id], c.[user_type_id], y.[is_user_defined], y.[name]
FROM sys.tables  t
JOIN sys.columns c on t.[object_id]    = c.[object_id]
JOIN sys.types   y on c.[user_type_id] = y.[user_type_id]
WHERE y.[name] IN ('geography','geometry','hierarchyid','image','text','ntext','sql_variant','timestamp','xml')
 AND  y.[is_user_defined] = 1;
```


## <span data-ttu-id="3b74b-120"><a name="unsupported-data-types"></a>Użyj obejścia nieobsługiwane typy danych</span><span class="sxs-lookup"><span data-stu-id="3b74b-120"><a name="unsupported-data-types"></a>Use workarounds for unsupported data types</span></span>

<span data-ttu-id="3b74b-121">Na poniższej liście przedstawiono typy danych nie obsługuje usługi SQL Data Warehouse, a udostępnia opis rozwiązań alternatywnych, których można użyć zamiast nieobsługiwane typy danych.</span><span class="sxs-lookup"><span data-stu-id="3b74b-121">The following list shows the data types that SQL Data Warehouse does not support and gives alternatives that you can use instead of the unsupported data types.</span></span>

| <span data-ttu-id="3b74b-122">Nieobsługiwany typ danych</span><span class="sxs-lookup"><span data-stu-id="3b74b-122">Unsupported data type</span></span> | <span data-ttu-id="3b74b-123">Obejście problemu</span><span class="sxs-lookup"><span data-stu-id="3b74b-123">Workaround</span></span> |
| --- | --- |
| <span data-ttu-id="3b74b-124">[Geometria][geometry]</span><span class="sxs-lookup"><span data-stu-id="3b74b-124">[geometry][geometry]</span></span> |<span data-ttu-id="3b74b-125">[varbinary][varbinary]</span><span class="sxs-lookup"><span data-stu-id="3b74b-125">[varbinary][varbinary]</span></span> |
| <span data-ttu-id="3b74b-126">[Lokalizacja geograficzna][geography]</span><span class="sxs-lookup"><span data-stu-id="3b74b-126">[geography][geography]</span></span> |<span data-ttu-id="3b74b-127">[varbinary][varbinary]</span><span class="sxs-lookup"><span data-stu-id="3b74b-127">[varbinary][varbinary]</span></span> |
| <span data-ttu-id="3b74b-128">[Identyfikator hierarchii][hierarchyid]</span><span class="sxs-lookup"><span data-stu-id="3b74b-128">[hierarchyid][hierarchyid]</span></span> |<span data-ttu-id="3b74b-129">[nvarchar][nvarchar](4000)</span><span class="sxs-lookup"><span data-stu-id="3b74b-129">[nvarchar][nvarchar](4000)</span></span> |
| <span data-ttu-id="3b74b-130">[Obraz][ntext,text,image]</span><span class="sxs-lookup"><span data-stu-id="3b74b-130">[image][ntext,text,image]</span></span> |<span data-ttu-id="3b74b-131">[varbinary][varbinary]</span><span class="sxs-lookup"><span data-stu-id="3b74b-131">[varbinary][varbinary]</span></span> |
| <span data-ttu-id="3b74b-132">[tekst][ntext,text,image]</span><span class="sxs-lookup"><span data-stu-id="3b74b-132">[text][ntext,text,image]</span></span> |<span data-ttu-id="3b74b-133">[varchar][varchar]</span><span class="sxs-lookup"><span data-stu-id="3b74b-133">[varchar][varchar]</span></span> |
| <span data-ttu-id="3b74b-134">[ntext][ntext,text,image]</span><span class="sxs-lookup"><span data-stu-id="3b74b-134">[ntext][ntext,text,image]</span></span> |<span data-ttu-id="3b74b-135">[nvarchar][nvarchar]</span><span class="sxs-lookup"><span data-stu-id="3b74b-135">[nvarchar][nvarchar]</span></span> |
| <span data-ttu-id="3b74b-136">[sql_variant][sql_variant]</span><span class="sxs-lookup"><span data-stu-id="3b74b-136">[sql_variant][sql_variant]</span></span> |<span data-ttu-id="3b74b-137">Podziel kolumnę na kilka jednoznacznie kolumn.</span><span class="sxs-lookup"><span data-stu-id="3b74b-137">Split column into several strongly typed columns.</span></span> |
| <span data-ttu-id="3b74b-138">[Tabela][table]</span><span class="sxs-lookup"><span data-stu-id="3b74b-138">[table][table]</span></span> |<span data-ttu-id="3b74b-139">Konwertuj do tabel tymczasowych.</span><span class="sxs-lookup"><span data-stu-id="3b74b-139">Convert to temporary tables.</span></span> |
| <span data-ttu-id="3b74b-140">[Znacznik czasu][timestamp]</span><span class="sxs-lookup"><span data-stu-id="3b74b-140">[timestamp][timestamp]</span></span> |<span data-ttu-id="3b74b-141">Zmian kodu w celu użycia [datetime2] [ datetime2] i `CURRENT_TIMESTAMP` funkcji.</span><span class="sxs-lookup"><span data-stu-id="3b74b-141">Rework code to use [datetime2][datetime2] and `CURRENT_TIMESTAMP` function.</span></span>  <span data-ttu-id="3b74b-142">Obsługiwane są tylko stałe jako domyślne, w związku z tym current_timestamp nie może być zdefiniowana jako ograniczenie domyślne.</span><span class="sxs-lookup"><span data-stu-id="3b74b-142">Only constants are supported as defaults, therefore current_timestamp cannot be defined as a default constraint.</span></span> <span data-ttu-id="3b74b-143">Jeśli trzeba migrować wartości wersji wierszy z typu kolumny znaczników czasu, użyj [BINARNE][BINARY](8) lub [VARBINARY][BINARY](8) dla nie wartość NULL lub Wiersz wersji wartości NULL.</span><span class="sxs-lookup"><span data-stu-id="3b74b-143">If you need to migrate row version values from a timestamp typed column, then use [BINARY][BINARY](8) or [VARBINARY][BINARY](8) for NOT NULL or NULL row version values.</span></span> |
| <span data-ttu-id="3b74b-144">[XML][xml]</span><span class="sxs-lookup"><span data-stu-id="3b74b-144">[xml][xml]</span></span> |<span data-ttu-id="3b74b-145">[varchar][varchar]</span><span class="sxs-lookup"><span data-stu-id="3b74b-145">[varchar][varchar]</span></span> |
| <span data-ttu-id="3b74b-146">[Typ zdefiniowany przez użytkownika][user defined types]</span><span class="sxs-lookup"><span data-stu-id="3b74b-146">[user-defined type][user defined types]</span></span> |<span data-ttu-id="3b74b-147">Przekonwertować typu danych natywnych, gdy jest to możliwe.</span><span class="sxs-lookup"><span data-stu-id="3b74b-147">Convert back to the native data type when possible.</span></span> |
| <span data-ttu-id="3b74b-148">wartości domyślne</span><span class="sxs-lookup"><span data-stu-id="3b74b-148">default values</span></span> | <span data-ttu-id="3b74b-149">Wartości domyślne obsługuje literały i tylko stałe.</span><span class="sxs-lookup"><span data-stu-id="3b74b-149">Default values support literals and constants only.</span></span>  <span data-ttu-id="3b74b-150">Inne niż deterministyczne wyrażenia lub funkcje, takie jak `GETDATE()` lub `CURRENT_TIMESTAMP`, nie są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="3b74b-150">Non-deterministic expressions or functions, such as `GETDATE()` or `CURRENT_TIMESTAMP`, are not supported.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="3b74b-151">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3b74b-151">Next steps</span></span>
<span data-ttu-id="3b74b-152">Aby dowiedzieć się więcej, zobacz:</span><span class="sxs-lookup"><span data-stu-id="3b74b-152">To learn more, see:</span></span>

- <span data-ttu-id="3b74b-153">[Najlepsze rozwiązania magazynu danych SQL][SQL Data Warehouse Best Practices]</span><span class="sxs-lookup"><span data-stu-id="3b74b-153">[SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices]</span></span>
- <span data-ttu-id="3b74b-154">[Przegląd tabeli][Overview]</span><span class="sxs-lookup"><span data-stu-id="3b74b-154">[Table Overview][Overview]</span></span>
- <span data-ttu-id="3b74b-155">[Dystrybucja tabeli][Distribute]</span><span class="sxs-lookup"><span data-stu-id="3b74b-155">[Distributing a Table][Distribute]</span></span>
- <span data-ttu-id="3b74b-156">[Indeksowanie tabeli][Index]</span><span class="sxs-lookup"><span data-stu-id="3b74b-156">[Indexing a Table][Index]</span></span>
- <span data-ttu-id="3b74b-157">[Podział na partycje tabeli][Partition]</span><span class="sxs-lookup"><span data-stu-id="3b74b-157">[Partitioning a Table][Partition]</span></span>
- <span data-ttu-id="3b74b-158">[Obsługa statystyk tabeli][Statistics]</span><span class="sxs-lookup"><span data-stu-id="3b74b-158">[Maintaining Table Statistics][Statistics]</span></span>
- <span data-ttu-id="3b74b-159">[Tabele tymczasowe][Temporary]</span><span class="sxs-lookup"><span data-stu-id="3b74b-159">[Temporary Tables][Temporary]</span></span>

<!--Image references-->

<!--Article references-->
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data Types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md

<!--MSDN references-->

<!--Other Web references-->
[create table]: https://msdn.microsoft.com/library/mt203953.aspx
[bigint]: https://msdn.microsoft.com/library/ms187745.aspx
[binary]: https://msdn.microsoft.com/library/ms188362.aspx
[bit]: https://msdn.microsoft.com/library/ms177603.aspx
[char]: https://msdn.microsoft.com/library/ms176089.aspx
[date]: https://msdn.microsoft.com/library/bb630352.aspx
[datetime]: https://msdn.microsoft.com/library/ms187819.aspx
[datetime2]: https://msdn.microsoft.com/library/bb677335.aspx
[datetimeoffset]: https://msdn.microsoft.com/library/bb630289.aspx
[decimal]: https://msdn.microsoft.com/library/ms187746.aspx
[float]: https://msdn.microsoft.com/library/ms173773.aspx
[geometry]: https://msdn.microsoft.com/library/cc280487.aspx
[geography]: https://msdn.microsoft.com/library/cc280766.aspx
[hierarchyid]: https://msdn.microsoft.com/library/bb677290.aspx
[int]: https://msdn.microsoft.com/library/ms187745.aspx
[money]: https://msdn.microsoft.com/library/ms179882.aspx
[nchar]: https://msdn.microsoft.com/library/ms186939.aspx
[nvarchar]: https://msdn.microsoft.com/library/ms186939.aspx
[ntext,text,image]: https://msdn.microsoft.com/library/ms187993.aspx
[real]: https://msdn.microsoft.com/library/ms173773.aspx
[smalldatetime]: https://msdn.microsoft.com/library/ms182418.aspx
[smallint]: https://msdn.microsoft.com/library/ms187745.aspx
[smallmoney]: https://msdn.microsoft.com/library/ms179882.aspx
[sql_variant]: https://msdn.microsoft.com/library/ms173829.aspx
[sysname]: https://msdn.microsoft.com/library/ms186939.aspx
[table]: https://msdn.microsoft.com/library/ms175010.aspx
[time]: https://msdn.microsoft.com/library/bb677243.aspx
[timestamp]: https://msdn.microsoft.com/library/ms182776.aspx
[tinyint]: https://msdn.microsoft.com/library/ms187745.aspx
[uniqueidentifier]: https://msdn.microsoft.com/library/ms187942.aspx
[varbinary]: https://msdn.microsoft.com/library/ms188362.aspx
[varchar]: https://msdn.microsoft.com/library/ms186939.aspx
[xml]: https://msdn.microsoft.com/library/ms187339.aspx
[user defined types]: https://msdn.microsoft.com/library/ms131694.aspx
