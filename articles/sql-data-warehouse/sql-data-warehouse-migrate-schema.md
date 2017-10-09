---
title: aaaMigrate Twojego tooSQL schematu magazynu danych | Dokumentacja firmy Microsoft
description: "Wskazówki dotyczące migrowania tooAzure Twojego schematu SQL Data Warehouse związane z opracowywaniem rozwiązań."
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: 538b60c9-a07f-49bf-9ea3-1082ed6699fb
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 10/31/2016
ms.author: joeyong;barbkess
ms.openlocfilehash: 1309b743b78564575695038a4856d9d25a2b18d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-schemas-toosql-data-warehouse"></a><span data-ttu-id="a2e16-103">Migracja z tooSQL schematów magazynu danych</span><span class="sxs-lookup"><span data-stu-id="a2e16-103">Migrate your schemas tooSQL Data Warehouse</span></span>
<span data-ttu-id="a2e16-104">Wskazówki dotyczące migrowania tooSQL schematy programu SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="a2e16-104">Guidance for migrating your SQL schemas tooSQL Data Warehouse.</span></span> 

## <a name="plan-your-schema-migration"></a><span data-ttu-id="a2e16-105">Planowanie migracji do schematu</span><span class="sxs-lookup"><span data-stu-id="a2e16-105">Plan your schema migration</span></span>

<span data-ttu-id="a2e16-106">Podczas planowania migracji, zobacz hello [omówienie tabeli] [ table overview] toobecome zapoznać się z tabeli projektowania, takich jak statystyka, dystrybucja, partycjonowanie i indeksowania.</span><span class="sxs-lookup"><span data-stu-id="a2e16-106">As you plan a migration, see hello [table overview][table overview] toobecome familiar with table design considerations such as statistics, distribution, partitioning, and indexing.</span></span>  <span data-ttu-id="a2e16-107">Przedstawiono także niektóre [nieobsługiwane funkcje tabeli] [ unsupported table features] i ich obejścia.</span><span class="sxs-lookup"><span data-stu-id="a2e16-107">It also lists some [unsupported table features][unsupported table features] and their workarounds.</span></span>

## <a name="use-user-defined-schemas-tooconsolidate-databases"></a><span data-ttu-id="a2e16-108">Użyj bazy danych tooconsolidate schematy zdefiniowane przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="a2e16-108">Use user-defined schemas tooconsolidate databases</span></span>

<span data-ttu-id="a2e16-109">Obciążenie istniejących prawdopodobnie ma więcej niż jednej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="a2e16-109">Your existing workload probably has more than one database.</span></span> <span data-ttu-id="a2e16-110">Na przykład magazynu danych programu SQL Server może obejmować tymczasowej bazy danych, bazy danych magazynu danych i niektóre bazy danych składnicy danych.</span><span class="sxs-lookup"><span data-stu-id="a2e16-110">For example, a SQL Server data warehouse might include a staging database, a data warehouse database, and some data mart databases.</span></span> <span data-ttu-id="a2e16-111">W tej topologii każda baza danych jest uruchamiany jako oddzielny obciążenia przy użyciu zasad zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="a2e16-111">In this topology, each database runs as a separate workload with separate security policies.</span></span>

<span data-ttu-id="a2e16-112">Z kolei SQL Data Warehouse uruchamia obciążeniu magazynu danych całego hello w ramach jednej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="a2e16-112">By contrast, SQL Data Warehouse runs hello entire data warehouse workload within one database.</span></span> <span data-ttu-id="a2e16-113">Sprzężenia między bazy danych nie są dozwolone.</span><span class="sxs-lookup"><span data-stu-id="a2e16-113">Cross database joins are not permitted.</span></span> <span data-ttu-id="a2e16-114">W związku z tym usługi SQL Data Warehouse oczekuje, że wszystkie tabele używane przez toobe magazynu danych hello przechowywane w hello jedną bazę danych.</span><span class="sxs-lookup"><span data-stu-id="a2e16-114">Therefore, SQL Data Warehouse expects all tables used by hello data warehouse toobe stored within hello one database.</span></span>

<span data-ttu-id="a2e16-115">Firma Microsoft zaleca używanie tooconsolidate użytkownika schematy istniejące obciążenia na jedną bazę danych.</span><span class="sxs-lookup"><span data-stu-id="a2e16-115">We recommend using user-defined schemas tooconsolidate your existing workload into one database.</span></span> <span data-ttu-id="a2e16-116">Przykłady można znaleźć [schematy zdefiniowane przez użytkownika](sql-data-warehouse-develop-user-defined-schemas.md)</span><span class="sxs-lookup"><span data-stu-id="a2e16-116">For examples, see [User-defined schemas](sql-data-warehouse-develop-user-defined-schemas.md)</span></span>

## <a name="use-compatible-data-types"></a><span data-ttu-id="a2e16-117">Użyj kompatybilne typy danych</span><span class="sxs-lookup"><span data-stu-id="a2e16-117">Use compatible data types</span></span>
<span data-ttu-id="a2e16-118">Modyfikowanie użytkownika toobe typy danych zgodne z usługą Magazyn danych SQL.</span><span class="sxs-lookup"><span data-stu-id="a2e16-118">Modify your data types toobe compatible with SQL Data Warehouse.</span></span> <span data-ttu-id="a2e16-119">Dla listy typów obsługiwanych i nieobsługiwanych danych, zobacz [typy danych][data types].</span><span class="sxs-lookup"><span data-stu-id="a2e16-119">For a list of supported and unsupported data types, see [data types][data types].</span></span> <span data-ttu-id="a2e16-120">Ten temat stanowi obejścia hello nieobsługiwane typy.</span><span class="sxs-lookup"><span data-stu-id="a2e16-120">That topic gives workarounds for hello unsupported types.</span></span> <span data-ttu-id="a2e16-121">Udostępnia również zapytania tooidentify istniejących typów, które nie są obsługiwane w usłudze SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="a2e16-121">It also provides a query tooidentify existing types that are not supported in SQL Data Warehouse.</span></span>

## <a name="minimize-row-size"></a><span data-ttu-id="a2e16-122">Minimalizuj rozmiar wiersza</span><span class="sxs-lookup"><span data-stu-id="a2e16-122">Minimize row size</span></span>
<span data-ttu-id="a2e16-123">Aby uzyskać najlepszą wydajność zminimalizować hello długość wiersza równą tabel.</span><span class="sxs-lookup"><span data-stu-id="a2e16-123">For best performance, minimize hello row length of your tables.</span></span> <span data-ttu-id="a2e16-124">Ponieważ krótszą długości wiersza prowadzić toobetter wydajności, należy użyć hello najmniejszą typów danych, które działają danych.</span><span class="sxs-lookup"><span data-stu-id="a2e16-124">Since shorter row lengths lead toobetter performance, use hello smallest data types that work for your data.</span></span> 

<span data-ttu-id="a2e16-125">Szerokość wiersza tabeli PolyBase ma limit 1 MB.</span><span class="sxs-lookup"><span data-stu-id="a2e16-125">For table row width, PolyBase has a 1 MB limit.</span></span>  <span data-ttu-id="a2e16-126">Jeśli planujesz tooload danych do usługi SQL Data Warehouse przy użyciu programu PolyBase, zaktualizuj tabele toohave wiersza maksymalnej szerokości mniej niż 1 MB.</span><span class="sxs-lookup"><span data-stu-id="a2e16-126">If you plan tooload data into SQL Data Warehouse with PolyBase, update your tables toohave maximum row widths of less than 1 MB.</span></span> 

<!--
- For example, this table uses variable length data but hello largest possible size of hello row is still less than 1 MB. PolyBase will load data into this table.

- This table uses variable length data and hello defined row width is less than one MB. When loading rows, PolyBase allocates hello full length of hello variable-length data. hello full length of this row is greater than one MB.  PolyBase will not load data into this table.  

-->

## <a name="specify-hello-distribution-option"></a><span data-ttu-id="a2e16-127">Wybierz opcję dystrybucji hello</span><span class="sxs-lookup"><span data-stu-id="a2e16-127">Specify hello distribution option</span></span>
<span data-ttu-id="a2e16-128">Usługa SQL Data Warehouse to system rozproszoną bazę danych.</span><span class="sxs-lookup"><span data-stu-id="a2e16-128">SQL Data Warehouse is a distributed database system.</span></span> <span data-ttu-id="a2e16-129">Każda tabela jest dystrybuowane lub replikowane w węzłach obliczeniowych hello.</span><span class="sxs-lookup"><span data-stu-id="a2e16-129">Each table is distributed or replicated across hello Compute nodes.</span></span> <span data-ttu-id="a2e16-130">Brak opcji tabeli, która pozwala określić, jak toodistribute hello danych.</span><span class="sxs-lookup"><span data-stu-id="a2e16-130">There's a table option that lets you specify how toodistribute hello data.</span></span> <span data-ttu-id="a2e16-131">Wybór Hello jest działanie okrężne, replikowane, albo rozproszone wyznaczania wartości skrótu.</span><span class="sxs-lookup"><span data-stu-id="a2e16-131">hello choices are  round-robin, replicated, or hash distributed.</span></span> <span data-ttu-id="a2e16-132">Każdy ma zalet i wad.</span><span class="sxs-lookup"><span data-stu-id="a2e16-132">Each has pros and cons.</span></span> <span data-ttu-id="a2e16-133">Jeśli nie określisz opcję dystrybucji hello SQL Data Warehouse użyje okrężnego jako domyślny hello.</span><span class="sxs-lookup"><span data-stu-id="a2e16-133">If you don't specify hello distribution option, SQL Data Warehouse will use round-robin as hello default.</span></span>

- <span data-ttu-id="a2e16-134">Działanie okrężne jest domyślnym hello.</span><span class="sxs-lookup"><span data-stu-id="a2e16-134">Round-robin is hello default.</span></span> <span data-ttu-id="a2e16-135">Jest najprostsza toouse hello i ładuje hello dane tak szybko, jak to możliwe, ale sprzęga wymaga przenoszenia danych, co zmniejsza szybkość działania zapytania.</span><span class="sxs-lookup"><span data-stu-id="a2e16-135">It is hello simplest toouse, and loads hello data as fast as possible, but joins will require data movement which slows query performance.</span></span>
- <span data-ttu-id="a2e16-136">Zreplikowane magazyny kopii tabeli hello w każdym węźle obliczeń.</span><span class="sxs-lookup"><span data-stu-id="a2e16-136">Replicated stores a copy of hello table on each Compute node.</span></span> <span data-ttu-id="a2e16-137">Zreplikowane tabele są wydajność, ponieważ nie wymaga przenoszenia danych do sprzęgania i agregacji.</span><span class="sxs-lookup"><span data-stu-id="a2e16-137">Replicated tables are performant because they do not require data movement for joins and aggregations.</span></span> <span data-ttu-id="a2e16-138">One wymagają dodatkowe miejsce do magazynowania, a w związku z tym najlepiej dla mniejszych tabel.</span><span class="sxs-lookup"><span data-stu-id="a2e16-138">They do require extra storage, and therefore work best for smaller tables.</span></span>
- <span data-ttu-id="a2e16-139">Skrót rozproszonych dystrybuuje wiersze hello we wszystkich węzłach hello za pomocą funkcji skrótu.</span><span class="sxs-lookup"><span data-stu-id="a2e16-139">Hash distributed distributes hello rows across all hello nodes via a hash function.</span></span> <span data-ttu-id="a2e16-140">Tabele hash rozproszone są hello Puls usługi SQL Data Warehouse, ponieważ są one zaprojektowane tooprovide wysoką wydajność zapytań na dużych tabel.</span><span class="sxs-lookup"><span data-stu-id="a2e16-140">Hash distributed tables are hello heart of SQL Data Warehouse since they are designed tooprovide high query performance on large tables.</span></span> <span data-ttu-id="a2e16-141">Ta opcja wymaga niektórych planowania tooselect hello najlepsze kolumny o danych hello toodistribute.</span><span class="sxs-lookup"><span data-stu-id="a2e16-141">This option requires some planning tooselect hello best column on which toodistribute hello data.</span></span> <span data-ttu-id="a2e16-142">Jednak jeśli nie wybierzesz hello najlepsze hello kolumny po raz pierwszy, można łatwo ponownie dystrybuować hello dane na inną kolumnę.</span><span class="sxs-lookup"><span data-stu-id="a2e16-142">However, if you don't choose hello best column hello first time, you can easily re-distribute hello data on a different column.</span></span> 

<span data-ttu-id="a2e16-143">Zobacz toochoose hello najlepszych opcji dystrybucji dla każdej tabeli [rozproszonych tabel](sql-data-warehouse-tables-distribute.md).</span><span class="sxs-lookup"><span data-stu-id="a2e16-143">toochoose hello best distribution option for each table, see [Distributed tables](sql-data-warehouse-tables-distribute.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="a2e16-144">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a2e16-144">Next steps</span></span>
<span data-ttu-id="a2e16-145">Po pomyślnej migracji z tooSQL schematu bazy danych magazynu danych można kontynuować tooone hello następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="a2e16-145">Once you have successfully migrated your database schema tooSQL Data Warehouse, proceed tooone of hello following articles:</span></span>

* <span data-ttu-id="a2e16-146">[Migrowanie danych][Migrate your data]</span><span class="sxs-lookup"><span data-stu-id="a2e16-146">[Migrate your data][Migrate your data]</span></span>
* <span data-ttu-id="a2e16-147">[Migrowanie kodu][Migrate your code]</span><span class="sxs-lookup"><span data-stu-id="a2e16-147">[Migrate your code][Migrate your code]</span></span>

<span data-ttu-id="a2e16-148">Aby uzyskać więcej informacji o najlepszych rozwiązaniach SQL Data Warehouse, zobacz hello [najlepsze rozwiązania] [ best practices] artykułu.</span><span class="sxs-lookup"><span data-stu-id="a2e16-148">For more about SQL Data Warehouse best practices, see hello [best practices][best practices] article.</span></span>

<!--Image references-->

<!--Article references-->
[Migrate your code]: ./sql-data-warehouse-migrate-code.md
[Migrate your data]: ./sql-data-warehouse-migrate-data.md
[best practices]: ./sql-data-warehouse-best-practices.md
[table overview]: ./sql-data-warehouse-tables-overview.md
[unsupported table features]: ./sql-data-warehouse-tables-overview.md#unsupported-table-features
[data types]: ./sql-data-warehouse-tables-data-types.md
[unsupported data types]: ./sql-data-warehouse-tables-data-types.md#unsupported-data-types

<!--MSDN references-->


<!--Other Web references-->
