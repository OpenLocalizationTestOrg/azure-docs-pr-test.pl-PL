---
title: "OLTP w pamięci poprawia wydajności transakcji SQL | Dokumentacja firmy Microsoft"
description: "Przyjąć OLTP w pamięci, aby zwiększyć wydajność transakcyjnych w istniejącej bazy danych SQL."
services: sql-database
documentationcenter: 
author: jodebrui
manager: jhubbard
editor: MightyPen
ms.assetid: c2bf14a0-905b-47b4-afb6-efe9a61147d5
ms.service: sql-database
ms.custom: develop databases
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/22/2016
ms.author: jodebrui
ms.openlocfilehash: 50eed9aed417778bd497f55e20c8e732fdae9cf9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="use-in-memory-oltp-to-improve-your-application-performance-in-sql-database"></a><span data-ttu-id="e54aa-103">Użyj OLTP w pamięci aby poprawić wydajność aplikacji w bazie danych SQL</span><span class="sxs-lookup"><span data-stu-id="e54aa-103">Use In-Memory OLTP to improve your application performance in SQL Database</span></span>
<span data-ttu-id="e54aa-104">[OLTP w pamięci](sql-database-in-memory.md) można użyć w celu poprawy wydajności przetwarzania transakcji, wprowadzanie danych i scenariusze przejściowej danych [Premium](sql-database-service-tiers.md) baz danych SQL Azure bez zwiększania warstwę cenową.</span><span class="sxs-lookup"><span data-stu-id="e54aa-104">[In-Memory OLTP](sql-database-in-memory.md) can be used to improve the performance of transaction processing, data ingestion, and transient data scenarios, in  [Premium](sql-database-service-tiers.md) Azure SQL Databases without increasing the pricing tier.</span></span> 

> [!NOTE] 
> <span data-ttu-id="e54aa-105">Dowiedz się, jak [kworum podwaja obciążenia klucza bazy danych podczas opuszczania jednostek dtu w warstwie 70% z bazy danych SQL](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database)</span><span class="sxs-lookup"><span data-stu-id="e54aa-105">Learn how [Quorum doubles key database’s workload while lowering DTU by 70% with SQL Database](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database)</span></span>


<span data-ttu-id="e54aa-106">Wykonaj poniższe kroki przyjąć OLTP w pamięci w istniejącej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="e54aa-106">Follow these steps to adopt In-Memory OLTP in your existing database.</span></span>

## <a name="step-1-ensure-you-are-using-a-premium-database"></a><span data-ttu-id="e54aa-107">Krok 1: Upewnij się, że w przypadku korzystania z bazy danych — warstwa Premium</span><span class="sxs-lookup"><span data-stu-id="e54aa-107">Step 1: Ensure you are using a Premium database</span></span>
<span data-ttu-id="e54aa-108">OLTP w pamięci jest obsługiwana tylko w bazach danych Premium.</span><span class="sxs-lookup"><span data-stu-id="e54aa-108">In-Memory OLTP is supported only in Premium databases.</span></span> <span data-ttu-id="e54aa-109">W pamięci jest obsługiwany, jeśli zwrócony wynik jest 1 (nie 0):</span><span class="sxs-lookup"><span data-stu-id="e54aa-109">In-Memory is supported if the returned result is 1 (not 0):</span></span>

```
SELECT DatabasePropertyEx(Db_Name(), 'IsXTPSupported');
```

<span data-ttu-id="e54aa-110">*XTP* oznacza *Extreme przetwarzania transakcji*</span><span class="sxs-lookup"><span data-stu-id="e54aa-110">*XTP* stands for *Extreme Transaction Processing*</span></span>



## <a name="step-2-identify-objects-to-migrate-to-in-memory-oltp"></a><span data-ttu-id="e54aa-111">Krok 2: Zidentyfikować obiekty do migracji do OLTP w pamięci</span><span class="sxs-lookup"><span data-stu-id="e54aa-111">Step 2: Identify objects to migrate to In-Memory OLTP</span></span>
<span data-ttu-id="e54aa-112">Obejmuje narzędzia SSMS **omówienie analizy wydajności transakcji** raport, który można uruchomić na bazie danych z aktywnego obciążenia.</span><span class="sxs-lookup"><span data-stu-id="e54aa-112">SSMS includes a **Transaction Performance Analysis Overview** report that you can run against a database with an active workload.</span></span> <span data-ttu-id="e54aa-113">Raport identyfikuje tabele i procedury składowane, przeznaczone do migracji do OLTP w pamięci.</span><span class="sxs-lookup"><span data-stu-id="e54aa-113">The report identifies tables and stored procedures that are candidates for migration to In-Memory OLTP.</span></span>

<span data-ttu-id="e54aa-114">W programie SSMS do wygenerowania raportu:</span><span class="sxs-lookup"><span data-stu-id="e54aa-114">In SSMS, to generate the report:</span></span>

* <span data-ttu-id="e54aa-115">W **Eksplorator obiektów**, kliknij prawym przyciskiem myszy węzeł bazy danych.</span><span class="sxs-lookup"><span data-stu-id="e54aa-115">In the **Object Explorer**, right-click your database node.</span></span>
* <span data-ttu-id="e54aa-116">Kliknij przycisk **raporty** > **raportów standardowych** > **omówienie analizy wydajności transakcji**.</span><span class="sxs-lookup"><span data-stu-id="e54aa-116">Click **Reports** > **Standard Reports** > **Transaction Performance Analysis Overview**.</span></span>

<span data-ttu-id="e54aa-117">Aby uzyskać więcej informacji, zobacz [Określanie tabela lub przechowywane procedury powinny być przenoszone OLTP w pamięci](http://msdn.microsoft.com/library/dn205133.aspx).</span><span class="sxs-lookup"><span data-stu-id="e54aa-117">For more information, see [Determining if a Table or Stored Procedure Should Be Ported to In-Memory OLTP](http://msdn.microsoft.com/library/dn205133.aspx).</span></span>

## <a name="step-3-create-a-comparable-test-database"></a><span data-ttu-id="e54aa-118">Krok 3: Tworzenie testu można porównywać pod względem bazy danych</span><span class="sxs-lookup"><span data-stu-id="e54aa-118">Step 3: Create a comparable test database</span></span>
<span data-ttu-id="e54aa-119">Załóżmy, że raport wskazuje, że baza danych zawiera tabelę, która będzie korzystać z konwertowanej do tabeli zoptymalizowanej pod kątem pamięci.</span><span class="sxs-lookup"><span data-stu-id="e54aa-119">Suppose the report indicates your database has a table that would benefit from being converted to a memory-optimized table.</span></span> <span data-ttu-id="e54aa-120">Firma Microsoft zaleca, należy najpierw przetestować potwierdzenia wskazanie przez testowania.</span><span class="sxs-lookup"><span data-stu-id="e54aa-120">We recommend that you first test to confirm the indication by testing.</span></span>

<span data-ttu-id="e54aa-121">Należy kopię bazy danych produkcyjnych.</span><span class="sxs-lookup"><span data-stu-id="e54aa-121">You need a test copy of your production database.</span></span> <span data-ttu-id="e54aa-122">Bazy danych testu powinien być na tym samym poziomie warstwy usługi, co w produkcyjnej bazie danych.</span><span class="sxs-lookup"><span data-stu-id="e54aa-122">The test database should be at the same service tier level as your production database.</span></span>

<span data-ttu-id="e54aa-123">Aby ułatwić testowanie, dostosować bazy danych testu w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="e54aa-123">To ease testing, tweak your test database as follows:</span></span>

1. <span data-ttu-id="e54aa-124">Połączenia z bazą danych testów przy użyciu narzędzia SSMS.</span><span class="sxs-lookup"><span data-stu-id="e54aa-124">Connect to the test database by using SSMS.</span></span>
2. <span data-ttu-id="e54aa-125">Aby uniknąć konieczności opcji WITH (SNAPSHOT) w zapytaniach, ustawić opcji bazy danych, jak pokazano w poniższych instrukcji T-SQL:</span><span class="sxs-lookup"><span data-stu-id="e54aa-125">To avoid needing the WITH (SNAPSHOT) option in queries, set the database option as shown in the following T-SQL statement:</span></span>
   
   ```
   ALTER DATABASE CURRENT
    SET
        MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT = ON;
   ```

## <a name="step-4-migrate-tables"></a><span data-ttu-id="e54aa-126">Krok 4: Migrowanie tabel</span><span class="sxs-lookup"><span data-stu-id="e54aa-126">Step 4: Migrate tables</span></span>
<span data-ttu-id="e54aa-127">Należy utworzyć i wypełnić kopii zoptymalizowanych pod kątem pamięci tabeli, która ma zostać przetestowana.</span><span class="sxs-lookup"><span data-stu-id="e54aa-127">You must create and populate a memory-optimized copy of the table you want to test.</span></span> <span data-ttu-id="e54aa-128">Można go utworzyć za pomocą:</span><span class="sxs-lookup"><span data-stu-id="e54aa-128">You can create it by using either:</span></span>

* <span data-ttu-id="e54aa-129">Przydatną Kreator optymalizacji pamięci w programie SSMS.</span><span class="sxs-lookup"><span data-stu-id="e54aa-129">The handy Memory Optimization Wizard in SSMS.</span></span>
* <span data-ttu-id="e54aa-130">Ręczne T-SQL.</span><span class="sxs-lookup"><span data-stu-id="e54aa-130">Manual T-SQL.</span></span>

#### <a name="memory-optimization-wizard-in-ssms"></a><span data-ttu-id="e54aa-131">Kreator optymalizacji pamięci w programie SSMS</span><span class="sxs-lookup"><span data-stu-id="e54aa-131">Memory Optimization Wizard in SSMS</span></span>
<span data-ttu-id="e54aa-132">Aby użyć tej opcji migracji:</span><span class="sxs-lookup"><span data-stu-id="e54aa-132">To use this migration option:</span></span>

1. <span data-ttu-id="e54aa-133">Połączenia z bazą danych testów z SSMS.</span><span class="sxs-lookup"><span data-stu-id="e54aa-133">Connect to the test database with SSMS.</span></span>
2. <span data-ttu-id="e54aa-134">W **Eksplorator obiektów**, kliknij prawym przyciskiem myszy w tabeli, a następnie kliknij przycisk **Advisor optymalizacji pamięci**.</span><span class="sxs-lookup"><span data-stu-id="e54aa-134">In the **Object Explorer**, right-click on the table, and then click **Memory Optimization Advisor**.</span></span>
   
   * <span data-ttu-id="e54aa-135">**Advisor optymalizacji pamięci tabeli** zostanie wyświetlony Kreator.</span><span class="sxs-lookup"><span data-stu-id="e54aa-135">The **Table Memory Optimizer Advisor** wizard is displayed.</span></span>
3. <span data-ttu-id="e54aa-136">W kreatorze kliknij **weryfikacji migracji** (lub **dalej** przycisk) aby zobaczyć, czy tabela zawiera nieobsługiwane funkcje, które nie są obsługiwane w tabelach zoptymalizowanych pod kątem pamięci.</span><span class="sxs-lookup"><span data-stu-id="e54aa-136">In the wizard, click **Migration validation** (or the **Next** button) to see if the table has any unsupported features that are unsupported in memory-optimized tables.</span></span> <span data-ttu-id="e54aa-137">Aby uzyskać więcej informacji, zobacz:</span><span class="sxs-lookup"><span data-stu-id="e54aa-137">For more information, see:</span></span>
   
   * <span data-ttu-id="e54aa-138">*Lista kontrolna optymalizacji pamięci* w [Advisor optymalizacji pamięci](http://msdn.microsoft.com/library/dn284308.aspx).</span><span class="sxs-lookup"><span data-stu-id="e54aa-138">The *memory optimization checklist* in [Memory Optimization Advisor](http://msdn.microsoft.com/library/dn284308.aspx).</span></span>
   * <span data-ttu-id="e54aa-139">[Konstrukcje języka Transact-SQL nie są obsługiwane przez OLTP w pamięci](http://msdn.microsoft.com/library/dn246937.aspx).</span><span class="sxs-lookup"><span data-stu-id="e54aa-139">[Transact-SQL Constructs Not Supported by In-Memory OLTP](http://msdn.microsoft.com/library/dn246937.aspx).</span></span>
   * <span data-ttu-id="e54aa-140">[Migrowanie do OLTP w pamięci](http://msdn.microsoft.com/library/dn247639.aspx).</span><span class="sxs-lookup"><span data-stu-id="e54aa-140">[Migrating to In-Memory OLTP](http://msdn.microsoft.com/library/dn247639.aspx).</span></span>
4. <span data-ttu-id="e54aa-141">Jeśli tabela nie zawiera nieobsługiwany funkcji, Doradcę można wykonywać rzeczywiste schematu i migrację danych za użytkownika.</span><span class="sxs-lookup"><span data-stu-id="e54aa-141">If the table has no unsupported features, the advisor can perform the actual schema and data migration for you.</span></span>

#### <a name="manual-t-sql"></a><span data-ttu-id="e54aa-142">Ręczne T-SQL</span><span class="sxs-lookup"><span data-stu-id="e54aa-142">Manual T-SQL</span></span>
<span data-ttu-id="e54aa-143">Aby użyć tej opcji migracji:</span><span class="sxs-lookup"><span data-stu-id="e54aa-143">To use this migration option:</span></span>

1. <span data-ttu-id="e54aa-144">Połączenia z bazą danych testów przy użyciu narzędzia SSMS (lub podobny narzędzia).</span><span class="sxs-lookup"><span data-stu-id="e54aa-144">Connect to your test database by using SSMS (or a similar utility).</span></span>
2. <span data-ttu-id="e54aa-145">Uzyskaj pełną skryptu T-SQL dla tabeli i jego indeksy.</span><span class="sxs-lookup"><span data-stu-id="e54aa-145">Obtain the complete T-SQL script for your table and its indexes.</span></span>
   
   * <span data-ttu-id="e54aa-146">W programie SSMS kliknij prawym przyciskiem myszy węzeł tabeli.</span><span class="sxs-lookup"><span data-stu-id="e54aa-146">In SSMS, right-click your table node.</span></span>
   * <span data-ttu-id="e54aa-147">Kliknij przycisk **skryptu tabeli jako** > **utworzyć** > **okna nowej kwerendy**.</span><span class="sxs-lookup"><span data-stu-id="e54aa-147">Click **Script Table As** > **CREATE To** > **New Query Window**.</span></span>
3. <span data-ttu-id="e54aa-148">W oknie skryptu, Dodaj WITH (MEMORY_OPTIMIZED = ON) w instrukcji CREATE TABLE.</span><span class="sxs-lookup"><span data-stu-id="e54aa-148">In the script window, add WITH (MEMORY_OPTIMIZED = ON) to the CREATE TABLE statement.</span></span>
4. <span data-ttu-id="e54aa-149">Jeśli istnieje indeks KLASTROWANY, zmień go na NONCLUSTERED.</span><span class="sxs-lookup"><span data-stu-id="e54aa-149">If there is a CLUSTERED index, change it to NONCLUSTERED.</span></span>
5. <span data-ttu-id="e54aa-150">Zmień nazwę istniejącej tabeli za pomocą obiekt SP_RENAME.</span><span class="sxs-lookup"><span data-stu-id="e54aa-150">Rename the existing table by using SP_RENAME.</span></span>
6. <span data-ttu-id="e54aa-151">Utwórz nową kopię zoptymalizowanych pod kątem pamięci tabeli, uruchamiając skrypt CREATE TABLE edytowany.</span><span class="sxs-lookup"><span data-stu-id="e54aa-151">Create the new memory-optimized copy of the table by running your edited CREATE TABLE script.</span></span>
7. <span data-ttu-id="e54aa-152">Skopiuj dane do tabeli zoptymalizowanej pod kątem pamięci przy użyciu INSERT... WYBIERZ * DO:</span><span class="sxs-lookup"><span data-stu-id="e54aa-152">Copy the data to your memory-optimized table by using INSERT...SELECT * INTO:</span></span>

```
INSERT INTO <new_memory_optimized_table>
        SELECT * FROM <old_disk_based_table>;
```


## <a name="step-5-optional-migrate-stored-procedures"></a><span data-ttu-id="e54aa-153">Krok 5 (opcjonalny): Migrowanie procedury składowane</span><span class="sxs-lookup"><span data-stu-id="e54aa-153">Step 5 (optional): Migrate stored procedures</span></span>
<span data-ttu-id="e54aa-154">Funkcja w pamięci można również zmodyfikować procedury składowanej zwiększonej wydajności.</span><span class="sxs-lookup"><span data-stu-id="e54aa-154">The In-Memory feature can also modify a stored procedure for improved performance.</span></span>

### <a name="considerations-with-natively-compiled-stored-procedures"></a><span data-ttu-id="e54aa-155">Zagadnienia w procedurach składowanych skompilowanych w sposób macierzysty</span><span class="sxs-lookup"><span data-stu-id="e54aa-155">Considerations with natively compiled stored procedures</span></span>
<span data-ttu-id="e54aa-156">Procedurę składowaną skompilowanych w sposób macierzysty musi mieć na jej klauzula T-SQL z następujących opcji:</span><span class="sxs-lookup"><span data-stu-id="e54aa-156">A natively compiled stored procedure must have the following options on its T-SQL WITH clause:</span></span>

* <span data-ttu-id="e54aa-157">OPCJĘ WITH NATIVE_COMPILATION</span><span class="sxs-lookup"><span data-stu-id="e54aa-157">NATIVE_COMPILATION</span></span>
* <span data-ttu-id="e54aa-158">SCHEMABINDING: tabele, co oznacza, że procedura składowana nie może mieć ich definicje kolumn zmienione w dowolny sposób, które będą wpływać na procedurę składowaną, chyba że porzucić procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="e54aa-158">SCHEMABINDING: meaning tables that the stored procedure cannot have their column definitions changed in any way that would affect the stored procedure, unless you drop the stored procedure.</span></span>

<span data-ttu-id="e54aa-159">Moduł macierzysty muszą używać jednej big [bloków ATOMIC](http://msdn.microsoft.com/library/dn452281.aspx) zarządzania transakcji.</span><span class="sxs-lookup"><span data-stu-id="e54aa-159">A native module must use one big [ATOMIC blocks](http://msdn.microsoft.com/library/dn452281.aspx) for transaction management.</span></span> <span data-ttu-id="e54aa-160">Brak role jawne BEGIN TRANSACTION lub ROLLBACK TRANSACTION.</span><span class="sxs-lookup"><span data-stu-id="e54aa-160">There is no role for an explicit BEGIN TRANSACTION, or for ROLLBACK TRANSACTION.</span></span> <span data-ttu-id="e54aa-161">Jeśli kod wykryje naruszenie reguł biznesowych, może obsłużyć atomic bloku [THROW](http://msdn.microsoft.com/library/ee677615.aspx) instrukcji.</span><span class="sxs-lookup"><span data-stu-id="e54aa-161">If your code detects a violation of a business rule, it can terminate the atomic block with a [THROW](http://msdn.microsoft.com/library/ee677615.aspx) statement.</span></span>

### <a name="typical-create-procedure-for-natively-compiled"></a><span data-ttu-id="e54aa-162">Typowy CREATE PROCEDURE dla skompilowanych w sposób macierzysty</span><span class="sxs-lookup"><span data-stu-id="e54aa-162">Typical CREATE PROCEDURE for natively compiled</span></span>
<span data-ttu-id="e54aa-163">Zwykle T-SQL, aby utworzyć skompilowanych w sposób macierzysty procedury składowanej jest podobny do następującego szablonu:</span><span class="sxs-lookup"><span data-stu-id="e54aa-163">Typically the T-SQL to create a natively compiled stored procedure is similar to the following template:</span></span>

```
CREATE PROCEDURE schemaname.procedurename
    @param1 type1, …
    WITH NATIVE_COMPILATION, SCHEMABINDING
    AS
        BEGIN ATOMIC WITH
            (TRANSACTION ISOLATION LEVEL = SNAPSHOT,
            LANGUAGE = N'your_language__see_sys.languages'
            )
        …
        END;
```

* <span data-ttu-id="e54aa-164">Dla TRANSACTION_ISOLATION_LEVEL MIGAWKA jest najbardziej typowe wartości dla procedury składowanej skompilowanych w sposób macierzysty.</span><span class="sxs-lookup"><span data-stu-id="e54aa-164">For the TRANSACTION_ISOLATION_LEVEL, SNAPSHOT is the most common value for the natively compiled stored procedure.</span></span> <span data-ttu-id="e54aa-165">Jednak podzbiór inne wartości są również obsługiwane:</span><span class="sxs-lookup"><span data-stu-id="e54aa-165">However,  a subset of the other values are also supported:</span></span>
  
  * <span data-ttu-id="e54aa-166">REPEATABLE READ</span><span class="sxs-lookup"><span data-stu-id="e54aa-166">REPEATABLE READ</span></span>
  * <span data-ttu-id="e54aa-167">MOŻLIWY DO SERIALIZACJI</span><span class="sxs-lookup"><span data-stu-id="e54aa-167">SERIALIZABLE</span></span>
* <span data-ttu-id="e54aa-168">Wartość języka musi być obecny w widoku sys.languages.</span><span class="sxs-lookup"><span data-stu-id="e54aa-168">The LANGUAGE value must be present in the sys.languages view.</span></span>

### <a name="how-to-migrate-a-stored-procedure"></a><span data-ttu-id="e54aa-169">Jak przeprowadzić migrację procedury składowanej</span><span class="sxs-lookup"><span data-stu-id="e54aa-169">How to migrate a stored procedure</span></span>
<span data-ttu-id="e54aa-170">Kroki migracji są:</span><span class="sxs-lookup"><span data-stu-id="e54aa-170">The migration steps are:</span></span>

1. <span data-ttu-id="e54aa-171">Uzyskaj skryptu CREATE PROCEDURE regularne interpretowany procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="e54aa-171">Obtain the CREATE PROCEDURE script to the regular interpreted stored procedure.</span></span>
2. <span data-ttu-id="e54aa-172">Należy zmodyfikować jej nagłówka do dopasowywania poprzedni szablon.</span><span class="sxs-lookup"><span data-stu-id="e54aa-172">Rewrite its header to match the previous template.</span></span>
3. <span data-ttu-id="e54aa-173">Należy upewnić się, czy procedura składowana kodu T-SQL korzysta z żadnych funkcji, które nie są obsługiwane dla procedur składowanych skompilowanych w sposób macierzysty.</span><span class="sxs-lookup"><span data-stu-id="e54aa-173">Ascertain whether the stored procedure T-SQL code uses any features that are not supported for natively compiled stored procedures.</span></span> <span data-ttu-id="e54aa-174">Implementowanie rozwiązania, w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="e54aa-174">Implement workarounds if necessary.</span></span>
   
   * <span data-ttu-id="e54aa-175">Aby uzyskać więcej informacji, zobacz [problemy przy migracji dla natywnie skompilowany na procedur składowanych](http://msdn.microsoft.com/library/dn296678.aspx).</span><span class="sxs-lookup"><span data-stu-id="e54aa-175">For details see [Migration Issues for Natively Compiled Stored Procedures](http://msdn.microsoft.com/library/dn296678.aspx).</span></span>
4. <span data-ttu-id="e54aa-176">Zmień nazwę starego procedury składowanej przy użyciu obiekt SP_RENAME.</span><span class="sxs-lookup"><span data-stu-id="e54aa-176">Rename the old stored procedure by using SP_RENAME.</span></span> <span data-ttu-id="e54aa-177">Lub po prostu UPUSZCZANIA.</span><span class="sxs-lookup"><span data-stu-id="e54aa-177">Or simply DROP it.</span></span>
5. <span data-ttu-id="e54aa-178">Uruchom skrypt edytowany Tworzenie procedury T-SQL.</span><span class="sxs-lookup"><span data-stu-id="e54aa-178">Run your edited CREATE PROCEDURE T-SQL script.</span></span>

## <a name="step-6-run-your-workload-in-test"></a><span data-ttu-id="e54aa-179">Krok 6: Uruchamianie obciążenia w teście</span><span class="sxs-lookup"><span data-stu-id="e54aa-179">Step 6: Run your workload in test</span></span>
<span data-ttu-id="e54aa-180">Uruchom obciążenia testu bazy danych podobny do obciążeniem, które jest uruchamiany w sieci produkcyjnej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="e54aa-180">Run a workload in your test database that is similar to the workload that runs in your production database.</span></span> <span data-ttu-id="e54aa-181">To powinno ujawnić, bardziej wydajne realizowane za korzystanie z funkcji w pamięci dla tabel i procedur składowanych.</span><span class="sxs-lookup"><span data-stu-id="e54aa-181">This should reveal the performance gain achieved by your use of the In-Memory feature for tables and stored procedures.</span></span>

<span data-ttu-id="e54aa-182">Atrybuty głównych obciążenia są:</span><span class="sxs-lookup"><span data-stu-id="e54aa-182">Major attributes of the workload are:</span></span>

* <span data-ttu-id="e54aa-183">Liczba równoczesnych połączeń.</span><span class="sxs-lookup"><span data-stu-id="e54aa-183">Number of concurrent connections.</span></span>
* <span data-ttu-id="e54aa-184">Stosunek odczytu/zapisu.</span><span class="sxs-lookup"><span data-stu-id="e54aa-184">Read/write ratio.</span></span>

<span data-ttu-id="e54aa-185">Aby dostosować i uruchomić test obciążenia, należy rozważyć użycie narzędzia przydatną ostress.exe, które przedstawiono w [tutaj](sql-database-in-memory.md).</span><span class="sxs-lookup"><span data-stu-id="e54aa-185">To tailor and run the test workload, consider using the handy ostress.exe tool, which illustrated in [here](sql-database-in-memory.md).</span></span>

<span data-ttu-id="e54aa-186">Aby zminimalizować opóźnienie sieci, uruchom test, w tym samym regionie geograficznym Azure którym baza danych istnieje.</span><span class="sxs-lookup"><span data-stu-id="e54aa-186">To minimize network latency, run your test in the same Azure geographic region where the database exists.</span></span>

## <a name="step-7-post-implementation-monitoring"></a><span data-ttu-id="e54aa-187">Krok 7: Monitorowanie po wdrożeniu</span><span class="sxs-lookup"><span data-stu-id="e54aa-187">Step 7: Post-implementation monitoring</span></span>
<span data-ttu-id="e54aa-188">Należy rozważyć monitorowanie wydajności skutków implementacjach użytkownika w pamięci w środowisku produkcyjnym:</span><span class="sxs-lookup"><span data-stu-id="e54aa-188">Consider monitoring the performance effects of your In-Memory implementations in production:</span></span>

* <span data-ttu-id="e54aa-189">[Monitorowanie magazynu w pamięci](sql-database-in-memory-oltp-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="e54aa-189">[Monitor In-Memory Storage](sql-database-in-memory-oltp-monitoring.md).</span></span>
* [<span data-ttu-id="e54aa-190">Monitorowanie usługi Azure SQL Database przy użyciu dynamicznych widoków zarządzania</span><span class="sxs-lookup"><span data-stu-id="e54aa-190">Monitoring Azure SQL Database using dynamic management views</span></span>](sql-database-monitoring-with-dmvs.md)

## <a name="related-links"></a><span data-ttu-id="e54aa-191">Powiązane linki</span><span class="sxs-lookup"><span data-stu-id="e54aa-191">Related links</span></span>
* [<span data-ttu-id="e54aa-192">(Optymalizacja w pamięci) OLTP w pamięci</span><span class="sxs-lookup"><span data-stu-id="e54aa-192">In-Memory OLTP (In-Memory Optimization)</span></span>](http://msdn.microsoft.com/library/dn133186.aspx)
* [<span data-ttu-id="e54aa-193">Wprowadzenie do procedur składowanych skompilowanych w sposób macierzysty</span><span class="sxs-lookup"><span data-stu-id="e54aa-193">Introduction to Natively Compiled Stored Procedures</span></span>](http://msdn.microsoft.com/library/dn133184.aspx)
* [<span data-ttu-id="e54aa-194">Klasyfikator optymalizacji pamięci</span><span class="sxs-lookup"><span data-stu-id="e54aa-194">Memory Optimization Advisor</span></span>](http://msdn.microsoft.com/library/dn284308.aspx)

