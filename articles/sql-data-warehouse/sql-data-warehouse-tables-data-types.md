---
title: "aaaData typy wskazówki - Azure SQL Data Warehouse | Dokumentacja firmy Microsoft"
description: "Zalecenia dotyczące danych toodefine typy, które są zgodne z usługi SQL Data Warehouse."
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
ms.openlocfilehash: a2f7a394feb73d273b25101735b00eb12db2b292
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="guidance-for-defining-data-types-for-tables-in-sql-data-warehouse"></a><span data-ttu-id="3dbd4-103">Wskazówki dotyczące definiowania typów danych w przypadku tabel w usłudze SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="3dbd4-103">Guidance for defining data types for tables in SQL Data Warehouse</span></span>
<span data-ttu-id="3dbd4-104">Użyj tych zaleceń toodefine tabeli typów danych, które są zgodne z usługą Magazyn danych SQL.</span><span class="sxs-lookup"><span data-stu-id="3dbd4-104">Use these recommendations toodefine table data types that are compatible with SQL Data Warehouse.</span></span> <span data-ttu-id="3dbd4-105">Ponadto toocompatibility, minimalizując hello rozmiar typów danych zwiększa wydajność zapytań.</span><span class="sxs-lookup"><span data-stu-id="3dbd4-105">In addition toocompatibility, minimizing hello size of data types improves query performance.</span></span>

<span data-ttu-id="3dbd4-106">Magazyn danych SQL obsługuje hello najczęściej używane typy danych.</span><span class="sxs-lookup"><span data-stu-id="3dbd4-106">SQL Data Warehouse supports hello most commonly used data types.</span></span> <span data-ttu-id="3dbd4-107">Aby uzyskać listę hello obsługiwane typy danych, zobacz [typy danych](/sql/docs/t-sql/statements/create-table-azure-sql-data-warehouse.md#datatypes) w instrukcji CREATE TABLE hello.</span><span class="sxs-lookup"><span data-stu-id="3dbd4-107">For a list of hello supported data types, see [data types](/sql/docs/t-sql/statements/create-table-azure-sql-data-warehouse.md#datatypes) in hello CREATE TABLE statement.</span></span> 


## <a name="minimize-row-length"></a><span data-ttu-id="3dbd4-108">Minimalizowanie długość wiersza</span><span class="sxs-lookup"><span data-stu-id="3dbd4-108">Minimize row length</span></span>
<span data-ttu-id="3dbd4-109">Minimalizowanie hello rozmiar typów danych skraca hello długość wiersza, która prowadzi toobetter wydajności zapytania.</span><span class="sxs-lookup"><span data-stu-id="3dbd4-109">Minimizing hello size of data types shortens hello row length, which leads toobetter query performance.</span></span> <span data-ttu-id="3dbd4-110">Użyj hello najmniejszą typ danych, który działa w przypadku danych.</span><span class="sxs-lookup"><span data-stu-id="3dbd4-110">Use hello smallest data type that works for your data.</span></span> 

- <span data-ttu-id="3dbd4-111">Unikaj definiowania kolumn znakowych o długości dużych domyślne.</span><span class="sxs-lookup"><span data-stu-id="3dbd4-111">Avoid defining character columns with a large default length.</span></span> <span data-ttu-id="3dbd4-112">Na przykład jeśli wartość najdłuższym hello 25 znaków, następnie zdefiniuj kolumny jako VARCHAR(25).</span><span class="sxs-lookup"><span data-stu-id="3dbd4-112">For example, if hello longest value is 25 characters, then define your column as VARCHAR(25).</span></span> 
- <span data-ttu-id="3dbd4-113">Unikaj używania [NVARCHAR] [ NVARCHAR] potrzebne tylko VARCHAR.</span><span class="sxs-lookup"><span data-stu-id="3dbd4-113">Avoid using [NVARCHAR][NVARCHAR] when you only need VARCHAR.</span></span>
- <span data-ttu-id="3dbd4-114">Jeśli to możliwe, zamiast VARCHAR(MAX) lub NVARCHAR(MAX), albo użyć NVARCHAR(4000) lub VARCHAR(8000).</span><span class="sxs-lookup"><span data-stu-id="3dbd4-114">When possible, use NVARCHAR(4000) or VARCHAR(8000) instead of NVARCHAR(MAX) or VARCHAR(MAX).</span></span>

<span data-ttu-id="3dbd4-115">Jeśli używasz programu Polybase tooload tabel, długość hello zdefiniowane hello wiersza tabeli nie może przekraczać 1 MB.</span><span class="sxs-lookup"><span data-stu-id="3dbd4-115">If you are using Polybase tooload your tables, hello defined length of hello table row cannot exceed 1 MB.</span></span> <span data-ttu-id="3dbd4-116">Jeśli wiersz o zmiennej długości danych przekracza 1 MB, można załadować wiersza hello za pomocą narzędzia BCP, ale nie przy użyciu programu PolyBase.</span><span class="sxs-lookup"><span data-stu-id="3dbd4-116">When a row with variable-length data exceeds 1 MB, you can load hello row with BCP, but not with PolyBase.</span></span>

## <a name="identify-unsupported-data-types"></a><span data-ttu-id="3dbd4-117">Zidentyfikuj nieobsługiwane typy danych</span><span class="sxs-lookup"><span data-stu-id="3dbd4-117">Identify unsupported data types</span></span>
<span data-ttu-id="3dbd4-118">W przypadku migracji z innej bazy danych SQL bazy danych, może wystąpić typy danych, które nie są obsługiwane w usłudze SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="3dbd4-118">If you are migrating your database from another SQL database, you might encounter data types that are not supported in SQL Data Warehouse.</span></span> <span data-ttu-id="3dbd4-119">Użyj typów danych toodiscover nieobsługiwany tego zapytania w istniejącego schematu SQL.</span><span class="sxs-lookup"><span data-stu-id="3dbd4-119">Use this query toodiscover unsupported data types in your existing SQL schema.</span></span>

```sql
SELECT  t.[name], c.[name], c.[system_type_id], c.[user_type_id], y.[is_user_defined], y.[name]
FROM sys.tables  t
JOIN sys.columns c on t.[object_id]    = c.[object_id]
JOIN sys.types   y on c.[user_type_id] = y.[user_type_id]
WHERE y.[name] IN ('geography','geometry','hierarchyid','image','text','ntext','sql_variant','timestamp','xml')
 AND  y.[is_user_defined] = 1;
```


## <span data-ttu-id="3dbd4-120"><a name="unsupported-data-types"></a>Użyj obejścia nieobsługiwane typy danych</span><span class="sxs-lookup"><span data-stu-id="3dbd4-120"><a name="unsupported-data-types"></a>Use workarounds for unsupported data types</span></span>

<span data-ttu-id="3dbd4-121">Witaj Poniższa lista zawiera hello typy danych, które nie obsługuje usługi SQL Data Warehouse i zapewnia rozwiązań alternatywnych, których można użyć zamiast hello nieobsługiwane typy danych.</span><span class="sxs-lookup"><span data-stu-id="3dbd4-121">hello following list shows hello data types that SQL Data Warehouse does not support and gives alternatives that you can use instead of hello unsupported data types.</span></span>

| <span data-ttu-id="3dbd4-122">Nieobsługiwany typ danych</span><span class="sxs-lookup"><span data-stu-id="3dbd4-122">Unsupported data type</span></span> | <span data-ttu-id="3dbd4-123">Obejście problemu</span><span class="sxs-lookup"><span data-stu-id="3dbd4-123">Workaround</span></span> |
| --- | --- |
| <span data-ttu-id="3dbd4-124">[Geometria][geometry]</span><span class="sxs-lookup"><span data-stu-id="3dbd4-124">[geometry][geometry]</span></span> |<span data-ttu-id="3dbd4-125">[varbinary][varbinary]</span><span class="sxs-lookup"><span data-stu-id="3dbd4-125">[varbinary][varbinary]</span></span> |
| <span data-ttu-id="3dbd4-126">[Lokalizacja geograficzna][geography]</span><span class="sxs-lookup"><span data-stu-id="3dbd4-126">[geography][geography]</span></span> |<span data-ttu-id="3dbd4-127">[varbinary][varbinary]</span><span class="sxs-lookup"><span data-stu-id="3dbd4-127">[varbinary][varbinary]</span></span> |
| <span data-ttu-id="3dbd4-128">[Identyfikator hierarchii][hierarchyid]</span><span class="sxs-lookup"><span data-stu-id="3dbd4-128">[hierarchyid][hierarchyid]</span></span> |<span data-ttu-id="3dbd4-129">[nvarchar][nvarchar](4000)</span><span class="sxs-lookup"><span data-stu-id="3dbd4-129">[nvarchar][nvarchar](4000)</span></span> |
| <span data-ttu-id="3dbd4-130">[Obraz][ntext,text,image]</span><span class="sxs-lookup"><span data-stu-id="3dbd4-130">[image][ntext,text,image]</span></span> |<span data-ttu-id="3dbd4-131">[varbinary][varbinary]</span><span class="sxs-lookup"><span data-stu-id="3dbd4-131">[varbinary][varbinary]</span></span> |
| <span data-ttu-id="3dbd4-132">[tekst][ntext,text,image]</span><span class="sxs-lookup"><span data-stu-id="3dbd4-132">[text][ntext,text,image]</span></span> |<span data-ttu-id="3dbd4-133">[varchar][varchar]</span><span class="sxs-lookup"><span data-stu-id="3dbd4-133">[varchar][varchar]</span></span> |
| <span data-ttu-id="3dbd4-134">[ntext][ntext,text,image]</span><span class="sxs-lookup"><span data-stu-id="3dbd4-134">[ntext][ntext,text,image]</span></span> |<span data-ttu-id="3dbd4-135">[nvarchar][nvarchar]</span><span class="sxs-lookup"><span data-stu-id="3dbd4-135">[nvarchar][nvarchar]</span></span> |
| <span data-ttu-id="3dbd4-136">[sql_variant][sql_variant]</span><span class="sxs-lookup"><span data-stu-id="3dbd4-136">[sql_variant][sql_variant]</span></span> |<span data-ttu-id="3dbd4-137">Podziel kolumnę na kilka jednoznacznie kolumn.</span><span class="sxs-lookup"><span data-stu-id="3dbd4-137">Split column into several strongly typed columns.</span></span> |
| <span data-ttu-id="3dbd4-138">[Tabela][table]</span><span class="sxs-lookup"><span data-stu-id="3dbd4-138">[table][table]</span></span> |<span data-ttu-id="3dbd4-139">Konwertuj tootemporary tabel.</span><span class="sxs-lookup"><span data-stu-id="3dbd4-139">Convert tootemporary tables.</span></span> |
| <span data-ttu-id="3dbd4-140">[Znacznik czasu][timestamp]</span><span class="sxs-lookup"><span data-stu-id="3dbd4-140">[timestamp][timestamp]</span></span> |<span data-ttu-id="3dbd4-141">Zmian kodu toouse [datetime2] [ datetime2] i `CURRENT_TIMESTAMP` funkcji.</span><span class="sxs-lookup"><span data-stu-id="3dbd4-141">Rework code toouse [datetime2][datetime2] and `CURRENT_TIMESTAMP` function.</span></span>  <span data-ttu-id="3dbd4-142">Obsługiwane są tylko stałe jako domyślne, w związku z tym current_timestamp nie może być zdefiniowana jako ograniczenie domyślne.</span><span class="sxs-lookup"><span data-stu-id="3dbd4-142">Only constants are supported as defaults, therefore current_timestamp cannot be defined as a default constraint.</span></span> <span data-ttu-id="3dbd4-143">Jeśli potrzebujesz toomigrate wartości wersji wierszy z kolumny typu znacznik czasu, użyj [BINARNE][BINARY](8) lub [VARBINARY][BINARY](8) dla nie wartość NULL lub Wiersz wersji wartości NULL.</span><span class="sxs-lookup"><span data-stu-id="3dbd4-143">If you need toomigrate row version values from a timestamp typed column, then use [BINARY][BINARY](8) or [VARBINARY][BINARY](8) for NOT NULL or NULL row version values.</span></span> |
| <span data-ttu-id="3dbd4-144">[XML][xml]</span><span class="sxs-lookup"><span data-stu-id="3dbd4-144">[xml][xml]</span></span> |<span data-ttu-id="3dbd4-145">[varchar][varchar]</span><span class="sxs-lookup"><span data-stu-id="3dbd4-145">[varchar][varchar]</span></span> |
| <span data-ttu-id="3dbd4-146">[Typ zdefiniowany przez użytkownika][user defined types]</span><span class="sxs-lookup"><span data-stu-id="3dbd4-146">[user-defined type][user defined types]</span></span> |<span data-ttu-id="3dbd4-147">Przekonwertować typu danych natywnych toohello Wstecz, gdy jest to możliwe.</span><span class="sxs-lookup"><span data-stu-id="3dbd4-147">Convert back toohello native data type when possible.</span></span> |
| <span data-ttu-id="3dbd4-148">wartości domyślne</span><span class="sxs-lookup"><span data-stu-id="3dbd4-148">default values</span></span> | <span data-ttu-id="3dbd4-149">Wartości domyślne obsługuje literały i tylko stałe.</span><span class="sxs-lookup"><span data-stu-id="3dbd4-149">Default values support literals and constants only.</span></span>  <span data-ttu-id="3dbd4-150">Inne niż deterministyczne wyrażenia lub funkcje, takie jak `GETDATE()` lub `CURRENT_TIMESTAMP`, nie są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="3dbd4-150">Non-deterministic expressions or functions, such as `GETDATE()` or `CURRENT_TIMESTAMP`, are not supported.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="3dbd4-151">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3dbd4-151">Next steps</span></span>
<span data-ttu-id="3dbd4-152">toolearn więcej, zobacz:</span><span class="sxs-lookup"><span data-stu-id="3dbd4-152">toolearn more, see:</span></span>

- <span data-ttu-id="3dbd4-153">[Najlepsze rozwiązania magazynu danych SQL][SQL Data Warehouse Best Practices]</span><span class="sxs-lookup"><span data-stu-id="3dbd4-153">[SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices]</span></span>
- <span data-ttu-id="3dbd4-154">[Przegląd tabeli][Overview]</span><span class="sxs-lookup"><span data-stu-id="3dbd4-154">[Table Overview][Overview]</span></span>
- <span data-ttu-id="3dbd4-155">[Dystrybucja tabeli][Distribute]</span><span class="sxs-lookup"><span data-stu-id="3dbd4-155">[Distributing a Table][Distribute]</span></span>
- <span data-ttu-id="3dbd4-156">[Indeksowanie tabeli][Index]</span><span class="sxs-lookup"><span data-stu-id="3dbd4-156">[Indexing a Table][Index]</span></span>
- <span data-ttu-id="3dbd4-157">[Podział na partycje tabeli][Partition]</span><span class="sxs-lookup"><span data-stu-id="3dbd4-157">[Partitioning a Table][Partition]</span></span>
- <span data-ttu-id="3dbd4-158">[Obsługa statystyk tabeli][Statistics]</span><span class="sxs-lookup"><span data-stu-id="3dbd4-158">[Maintaining Table Statistics][Statistics]</span></span>
- <span data-ttu-id="3dbd4-159">[Tabele tymczasowe][Temporary]</span><span class="sxs-lookup"><span data-stu-id="3dbd4-159">[Temporary Tables][Temporary]</span></span>

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
