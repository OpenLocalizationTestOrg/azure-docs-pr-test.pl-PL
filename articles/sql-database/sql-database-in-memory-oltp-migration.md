---
title: "Pamięć aaaIn OLTP poprawia wydajności transakcji SQL | Dokumentacja firmy Microsoft"
description: "OLTP w pamięci przyjąć tooimprove transakcyjnych wydajności w istniejącej bazy danych SQL."
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
ms.openlocfilehash: 1bed796069565eb6741953837cf0477c2ddd8519
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-in-memory-oltp-tooimprove-your-application-performance-in-sql-database"></a><span data-ttu-id="f4c89-103">Użyj OLTP w pamięci tooimprove wydajność aplikacji w bazie danych SQL</span><span class="sxs-lookup"><span data-stu-id="f4c89-103">Use In-Memory OLTP tooimprove your application performance in SQL Database</span></span>
<span data-ttu-id="f4c89-104">[OLTP w pamięci](sql-database-in-memory.md) może być wydajności hello tooimprove używane przetwarzanie transakcji, wprowadzanie danych i scenariusze przejściowej danych w [Premium](sql-database-service-tiers.md) baz danych SQL Azure bez zwiększania hello warstwę cenową.</span><span class="sxs-lookup"><span data-stu-id="f4c89-104">[In-Memory OLTP](sql-database-in-memory.md) can be used tooimprove hello performance of transaction processing, data ingestion, and transient data scenarios, in  [Premium](sql-database-service-tiers.md) Azure SQL Databases without increasing hello pricing tier.</span></span> 

> [!NOTE] 
> <span data-ttu-id="f4c89-105">Dowiedz się, jak [kworum podwaja obciążenia klucza bazy danych podczas opuszczania jednostek dtu w warstwie 70% z bazy danych SQL](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database)</span><span class="sxs-lookup"><span data-stu-id="f4c89-105">Learn how [Quorum doubles key database’s workload while lowering DTU by 70% with SQL Database](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database)</span></span>


<span data-ttu-id="f4c89-106">Wykonaj te kroki tooadopt OLTP w pamięci w istniejącej bazie danych.</span><span class="sxs-lookup"><span data-stu-id="f4c89-106">Follow these steps tooadopt In-Memory OLTP in your existing database.</span></span>

## <a name="step-1-ensure-you-are-using-a-premium-database"></a><span data-ttu-id="f4c89-107">Krok 1: Upewnij się, że w przypadku korzystania z bazy danych — warstwa Premium</span><span class="sxs-lookup"><span data-stu-id="f4c89-107">Step 1: Ensure you are using a Premium database</span></span>
<span data-ttu-id="f4c89-108">OLTP w pamięci jest obsługiwana tylko w bazach danych Premium.</span><span class="sxs-lookup"><span data-stu-id="f4c89-108">In-Memory OLTP is supported only in Premium databases.</span></span> <span data-ttu-id="f4c89-109">W pamięci jest obsługiwany, jeśli hello zwrócony wynik 1 (nie 0):</span><span class="sxs-lookup"><span data-stu-id="f4c89-109">In-Memory is supported if hello returned result is 1 (not 0):</span></span>

```
SELECT DatabasePropertyEx(Db_Name(), 'IsXTPSupported');
```

<span data-ttu-id="f4c89-110">*XTP* oznacza *Extreme przetwarzania transakcji*</span><span class="sxs-lookup"><span data-stu-id="f4c89-110">*XTP* stands for *Extreme Transaction Processing*</span></span>



## <a name="step-2-identify-objects-toomigrate-tooin-memory-oltp"></a><span data-ttu-id="f4c89-111">Krok 2: Określenie tooIn toomigrate obiektów pamięci OLTP</span><span class="sxs-lookup"><span data-stu-id="f4c89-111">Step 2: Identify objects toomigrate tooIn-Memory OLTP</span></span>
<span data-ttu-id="f4c89-112">Obejmuje narzędzia SSMS **omówienie analizy wydajności transakcji** raport, który można uruchomić na bazie danych z aktywnego obciążenia.</span><span class="sxs-lookup"><span data-stu-id="f4c89-112">SSMS includes a **Transaction Performance Analysis Overview** report that you can run against a database with an active workload.</span></span> <span data-ttu-id="f4c89-113">Raport Hello identyfikuje tabele i procedury składowane, przeznaczone do migracji pamięci tooIn OLTP.</span><span class="sxs-lookup"><span data-stu-id="f4c89-113">hello report identifies tables and stored procedures that are candidates for migration tooIn-Memory OLTP.</span></span>

<span data-ttu-id="f4c89-114">W programie SSMS toogenerate hello raportu:</span><span class="sxs-lookup"><span data-stu-id="f4c89-114">In SSMS, toogenerate hello report:</span></span>

* <span data-ttu-id="f4c89-115">W hello **Eksplorator obiektów**, kliknij prawym przyciskiem myszy węzeł bazy danych.</span><span class="sxs-lookup"><span data-stu-id="f4c89-115">In hello **Object Explorer**, right-click your database node.</span></span>
* <span data-ttu-id="f4c89-116">Kliknij przycisk **raporty** > **raportów standardowych** > **omówienie analizy wydajności transakcji**.</span><span class="sxs-lookup"><span data-stu-id="f4c89-116">Click **Reports** > **Standard Reports** > **Transaction Performance Analysis Overview**.</span></span>

<span data-ttu-id="f4c89-117">Aby uzyskać więcej informacji, zobacz [Określanie tabela lub przechowywane procedury powinny być przenoszone OLTP pamięci tooIn](http://msdn.microsoft.com/library/dn205133.aspx).</span><span class="sxs-lookup"><span data-stu-id="f4c89-117">For more information, see [Determining if a Table or Stored Procedure Should Be Ported tooIn-Memory OLTP](http://msdn.microsoft.com/library/dn205133.aspx).</span></span>

## <a name="step-3-create-a-comparable-test-database"></a><span data-ttu-id="f4c89-118">Krok 3: Tworzenie testu można porównywać pod względem bazy danych</span><span class="sxs-lookup"><span data-stu-id="f4c89-118">Step 3: Create a comparable test database</span></span>
<span data-ttu-id="f4c89-119">Załóżmy, że raport hello wskazuje bazy danych zawiera tabelę, która będzie korzystać z przekonwertować tabel zoptymalizowanych pod kątem pamięci tooa.</span><span class="sxs-lookup"><span data-stu-id="f4c89-119">Suppose hello report indicates your database has a table that would benefit from being converted tooa memory-optimized table.</span></span> <span data-ttu-id="f4c89-120">Zaleca się najpierw przetestować wskazanie hello tooconfirm podczas testów.</span><span class="sxs-lookup"><span data-stu-id="f4c89-120">We recommend that you first test tooconfirm hello indication by testing.</span></span>

<span data-ttu-id="f4c89-121">Należy kopię bazy danych produkcyjnych.</span><span class="sxs-lookup"><span data-stu-id="f4c89-121">You need a test copy of your production database.</span></span> <span data-ttu-id="f4c89-122">Witaj testu baza danych powinna być na powitania samym poziomie usług, warstwy jako baza danych w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="f4c89-122">hello test database should be at hello same service tier level as your production database.</span></span>

<span data-ttu-id="f4c89-123">tooease testowania, dostosować bazy danych testu w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="f4c89-123">tooease testing, tweak your test database as follows:</span></span>

1. <span data-ttu-id="f4c89-124">Połączenia bazy danych testów toohello przy użyciu narzędzia SSMS.</span><span class="sxs-lookup"><span data-stu-id="f4c89-124">Connect toohello test database by using SSMS.</span></span>
2. <span data-ttu-id="f4c89-125">tooavoid wymagające hello opcji WITH (SNAPSHOT) w zapytaniach, należy ustawić opcję bazy danych hello, jak pokazano w powitania po instrukcji T-SQL:</span><span class="sxs-lookup"><span data-stu-id="f4c89-125">tooavoid needing hello WITH (SNAPSHOT) option in queries, set hello database option as shown in hello following T-SQL statement:</span></span>
   
   ```
   ALTER DATABASE CURRENT
    SET
        MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT = ON;
   ```

## <a name="step-4-migrate-tables"></a><span data-ttu-id="f4c89-126">Krok 4: Migrowanie tabel</span><span class="sxs-lookup"><span data-stu-id="f4c89-126">Step 4: Migrate tables</span></span>
<span data-ttu-id="f4c89-127">Należy utworzyć i wypełnić kopię zoptymalizowanych pod kątem pamięci tabeli hello ma tootest.</span><span class="sxs-lookup"><span data-stu-id="f4c89-127">You must create and populate a memory-optimized copy of hello table you want tootest.</span></span> <span data-ttu-id="f4c89-128">Można go utworzyć za pomocą:</span><span class="sxs-lookup"><span data-stu-id="f4c89-128">You can create it by using either:</span></span>

* <span data-ttu-id="f4c89-129">Witaj przydatną Kreator optymalizacji pamięci w programie SSMS.</span><span class="sxs-lookup"><span data-stu-id="f4c89-129">hello handy Memory Optimization Wizard in SSMS.</span></span>
* <span data-ttu-id="f4c89-130">Ręczne T-SQL.</span><span class="sxs-lookup"><span data-stu-id="f4c89-130">Manual T-SQL.</span></span>

#### <a name="memory-optimization-wizard-in-ssms"></a><span data-ttu-id="f4c89-131">Kreator optymalizacji pamięci w programie SSMS</span><span class="sxs-lookup"><span data-stu-id="f4c89-131">Memory Optimization Wizard in SSMS</span></span>
<span data-ttu-id="f4c89-132">toouse tej opcji migracji:</span><span class="sxs-lookup"><span data-stu-id="f4c89-132">toouse this migration option:</span></span>

1. <span data-ttu-id="f4c89-133">Połączenie bazy danych testów toohello z SSMS.</span><span class="sxs-lookup"><span data-stu-id="f4c89-133">Connect toohello test database with SSMS.</span></span>
2. <span data-ttu-id="f4c89-134">W hello **Eksplorator obiektów**, kliknij prawym przyciskiem myszy na powitania tabeli, a następnie kliknij przycisk **Advisor optymalizacji pamięci**.</span><span class="sxs-lookup"><span data-stu-id="f4c89-134">In hello **Object Explorer**, right-click on hello table, and then click **Memory Optimization Advisor**.</span></span>
   
   * <span data-ttu-id="f4c89-135">Witaj **Advisor optymalizacji pamięci tabeli** zostanie wyświetlony Kreator.</span><span class="sxs-lookup"><span data-stu-id="f4c89-135">hello **Table Memory Optimizer Advisor** wizard is displayed.</span></span>
3. <span data-ttu-id="f4c89-136">W Kreatorze powitania kliknij **weryfikacji migracji** (lub hello **dalej** przycisk) toosee, jeśli tabela hello ma jakiekolwiek nieobsługiwane funkcje, które nie są obsługiwane w tabelach zoptymalizowanych pod kątem pamięci.</span><span class="sxs-lookup"><span data-stu-id="f4c89-136">In hello wizard, click **Migration validation** (or hello **Next** button) toosee if hello table has any unsupported features that are unsupported in memory-optimized tables.</span></span> <span data-ttu-id="f4c89-137">Aby uzyskać więcej informacji, zobacz:</span><span class="sxs-lookup"><span data-stu-id="f4c89-137">For more information, see:</span></span>
   
   * <span data-ttu-id="f4c89-138">Witaj *Lista kontrolna optymalizacji pamięci* w [Advisor optymalizacji pamięci](http://msdn.microsoft.com/library/dn284308.aspx).</span><span class="sxs-lookup"><span data-stu-id="f4c89-138">hello *memory optimization checklist* in [Memory Optimization Advisor](http://msdn.microsoft.com/library/dn284308.aspx).</span></span>
   * <span data-ttu-id="f4c89-139">[Konstrukcje języka Transact-SQL nie są obsługiwane przez OLTP w pamięci](http://msdn.microsoft.com/library/dn246937.aspx).</span><span class="sxs-lookup"><span data-stu-id="f4c89-139">[Transact-SQL Constructs Not Supported by In-Memory OLTP](http://msdn.microsoft.com/library/dn246937.aspx).</span></span>
   * <span data-ttu-id="f4c89-140">[Migrowanie OLTP pamięci tooIn](http://msdn.microsoft.com/library/dn247639.aspx).</span><span class="sxs-lookup"><span data-stu-id="f4c89-140">[Migrating tooIn-Memory OLTP](http://msdn.microsoft.com/library/dn247639.aspx).</span></span>
4. <span data-ttu-id="f4c89-141">Jeśli hello tabela nie zawiera nieobsługiwany funkcji, hello advisor może wykonywać hello rzeczywiste schematu i migracji danych dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="f4c89-141">If hello table has no unsupported features, hello advisor can perform hello actual schema and data migration for you.</span></span>

#### <a name="manual-t-sql"></a><span data-ttu-id="f4c89-142">Ręczne T-SQL</span><span class="sxs-lookup"><span data-stu-id="f4c89-142">Manual T-SQL</span></span>
<span data-ttu-id="f4c89-143">toouse tej opcji migracji:</span><span class="sxs-lookup"><span data-stu-id="f4c89-143">toouse this migration option:</span></span>

1. <span data-ttu-id="f4c89-144">Połączenia bazy danych testów tooyour przy użyciu narzędzia SSMS (lub podobny narzędzia).</span><span class="sxs-lookup"><span data-stu-id="f4c89-144">Connect tooyour test database by using SSMS (or a similar utility).</span></span>
2. <span data-ttu-id="f4c89-145">Uzyskaj hello pełną skryptu T-SQL dla tabeli i jego indeksy.</span><span class="sxs-lookup"><span data-stu-id="f4c89-145">Obtain hello complete T-SQL script for your table and its indexes.</span></span>
   
   * <span data-ttu-id="f4c89-146">W programie SSMS kliknij prawym przyciskiem myszy węzeł tabeli.</span><span class="sxs-lookup"><span data-stu-id="f4c89-146">In SSMS, right-click your table node.</span></span>
   * <span data-ttu-id="f4c89-147">Kliknij przycisk **skryptu tabeli jako** > **utworzyć** > **okna nowej kwerendy**.</span><span class="sxs-lookup"><span data-stu-id="f4c89-147">Click **Script Table As** > **CREATE To** > **New Query Window**.</span></span>
3. <span data-ttu-id="f4c89-148">W oknie Skrypt hello, Dodaj WITH (MEMORY_OPTIMIZED = ON) toohello instrukcji CREATE TABLE.</span><span class="sxs-lookup"><span data-stu-id="f4c89-148">In hello script window, add WITH (MEMORY_OPTIMIZED = ON) toohello CREATE TABLE statement.</span></span>
4. <span data-ttu-id="f4c89-149">Jeśli istnieje indeks KLASTROWANY, zmień go tooNONCLUSTERED.</span><span class="sxs-lookup"><span data-stu-id="f4c89-149">If there is a CLUSTERED index, change it tooNONCLUSTERED.</span></span>
5. <span data-ttu-id="f4c89-150">Zmień nazwę istniejącej tabeli hello przy użyciu obiekt SP_RENAME.</span><span class="sxs-lookup"><span data-stu-id="f4c89-150">Rename hello existing table by using SP_RENAME.</span></span>
6. <span data-ttu-id="f4c89-151">Utworzenie hello nowe zoptymalizowanych pod kątem pamięci kopii tabeli hello, uruchamiając skrypt CREATE TABLE edytowany.</span><span class="sxs-lookup"><span data-stu-id="f4c89-151">Create hello new memory-optimized copy of hello table by running your edited CREATE TABLE script.</span></span>
7. <span data-ttu-id="f4c89-152">Kopiuj hello danych tooyour zoptymalizowanych pod kątem pamięci tabeli za pomocą INSERT... WYBIERZ * DO:</span><span class="sxs-lookup"><span data-stu-id="f4c89-152">Copy hello data tooyour memory-optimized table by using INSERT...SELECT * INTO:</span></span>

```
INSERT INTO <new_memory_optimized_table>
        SELECT * FROM <old_disk_based_table>;
```


## <a name="step-5-optional-migrate-stored-procedures"></a><span data-ttu-id="f4c89-153">Krok 5 (opcjonalny): Migrowanie procedury składowane</span><span class="sxs-lookup"><span data-stu-id="f4c89-153">Step 5 (optional): Migrate stored procedures</span></span>
<span data-ttu-id="f4c89-154">Witaj w pamięci funkcji można również zmodyfikować procedury składowanej zwiększonej wydajności.</span><span class="sxs-lookup"><span data-stu-id="f4c89-154">hello In-Memory feature can also modify a stored procedure for improved performance.</span></span>

### <a name="considerations-with-natively-compiled-stored-procedures"></a><span data-ttu-id="f4c89-155">Zagadnienia w procedurach składowanych skompilowanych w sposób macierzysty</span><span class="sxs-lookup"><span data-stu-id="f4c89-155">Considerations with natively compiled stored procedures</span></span>
<span data-ttu-id="f4c89-156">Procedurę składowaną skompilowanych w sposób macierzysty musi mieć następujące opcje w jej klauzula T-SQL z hello:</span><span class="sxs-lookup"><span data-stu-id="f4c89-156">A natively compiled stored procedure must have hello following options on its T-SQL WITH clause:</span></span>

* <span data-ttu-id="f4c89-157">OPCJĘ WITH NATIVE_COMPILATION</span><span class="sxs-lookup"><span data-stu-id="f4c89-157">NATIVE_COMPILATION</span></span>
* <span data-ttu-id="f4c89-158">SCHEMABINDING: tabel znaczenie, które hello procedury składowanej nie może mieć ich definicje kolumn zmienione w dowolny sposób, które będą wpływać na powitania przechowywane procedury, chyba że porzucić hello przechowywane procedury.</span><span class="sxs-lookup"><span data-stu-id="f4c89-158">SCHEMABINDING: meaning tables that hello stored procedure cannot have their column definitions changed in any way that would affect hello stored procedure, unless you drop hello stored procedure.</span></span>

<span data-ttu-id="f4c89-159">Moduł macierzysty muszą używać jednej big [bloków ATOMIC](http://msdn.microsoft.com/library/dn452281.aspx) zarządzania transakcji.</span><span class="sxs-lookup"><span data-stu-id="f4c89-159">A native module must use one big [ATOMIC blocks](http://msdn.microsoft.com/library/dn452281.aspx) for transaction management.</span></span> <span data-ttu-id="f4c89-160">Brak role jawne BEGIN TRANSACTION lub ROLLBACK TRANSACTION.</span><span class="sxs-lookup"><span data-stu-id="f4c89-160">There is no role for an explicit BEGIN TRANSACTION, or for ROLLBACK TRANSACTION.</span></span> <span data-ttu-id="f4c89-161">Jeśli kod wykryje naruszenie reguł biznesowych, może obsłużyć hello atomic blok z [THROW](http://msdn.microsoft.com/library/ee677615.aspx) instrukcji.</span><span class="sxs-lookup"><span data-stu-id="f4c89-161">If your code detects a violation of a business rule, it can terminate hello atomic block with a [THROW](http://msdn.microsoft.com/library/ee677615.aspx) statement.</span></span>

### <a name="typical-create-procedure-for-natively-compiled"></a><span data-ttu-id="f4c89-162">Typowy CREATE PROCEDURE dla skompilowanych w sposób macierzysty</span><span class="sxs-lookup"><span data-stu-id="f4c89-162">Typical CREATE PROCEDURE for natively compiled</span></span>
<span data-ttu-id="f4c89-163">Zazwyczaj toocreate hello T-SQL skompilowanych w sposób macierzysty procedury składowanej jest podobne toohello następującego szablonu:</span><span class="sxs-lookup"><span data-stu-id="f4c89-163">Typically hello T-SQL toocreate a natively compiled stored procedure is similar toohello following template:</span></span>

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

* <span data-ttu-id="f4c89-164">W przypadku hello TRANSACTION_ISOLATION_LEVEL MIGAWKI jest hello najbardziej typowe wartości dla skompilowanych w sposób macierzysty hello przechowywanej procedury.</span><span class="sxs-lookup"><span data-stu-id="f4c89-164">For hello TRANSACTION_ISOLATION_LEVEL, SNAPSHOT is hello most common value for hello natively compiled stored procedure.</span></span> <span data-ttu-id="f4c89-165">Jednak podzbiór hello inne wartości są również obsługiwane:</span><span class="sxs-lookup"><span data-stu-id="f4c89-165">However,  a subset of hello other values are also supported:</span></span>
  
  * <span data-ttu-id="f4c89-166">REPEATABLE READ</span><span class="sxs-lookup"><span data-stu-id="f4c89-166">REPEATABLE READ</span></span>
  * <span data-ttu-id="f4c89-167">MOŻLIWY DO SERIALIZACJI</span><span class="sxs-lookup"><span data-stu-id="f4c89-167">SERIALIZABLE</span></span>
* <span data-ttu-id="f4c89-168">Witaj wartość języka musi być obecny w widoku sys.languages hello.</span><span class="sxs-lookup"><span data-stu-id="f4c89-168">hello LANGUAGE value must be present in hello sys.languages view.</span></span>

### <a name="how-toomigrate-a-stored-procedure"></a><span data-ttu-id="f4c89-169">Jak toomigrate procedury składowanej</span><span class="sxs-lookup"><span data-stu-id="f4c89-169">How toomigrate a stored procedure</span></span>
<span data-ttu-id="f4c89-170">kroki migracji Hello są:</span><span class="sxs-lookup"><span data-stu-id="f4c89-170">hello migration steps are:</span></span>

1. <span data-ttu-id="f4c89-171">Uzyskaj hello CREATE PROCEDURE skryptu toohello regularne interpretowany procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="f4c89-171">Obtain hello CREATE PROCEDURE script toohello regular interpreted stored procedure.</span></span>
2. <span data-ttu-id="f4c89-172">Należy zmodyfikować jej nagłówka toomatch hello poprzedniego szablonu.</span><span class="sxs-lookup"><span data-stu-id="f4c89-172">Rewrite its header toomatch hello previous template.</span></span>
3. <span data-ttu-id="f4c89-173">Należy upewnić się, czy procedury przechowywane hello kodu T-SQL korzysta z żadnych funkcji, które nie są obsługiwane dla procedur składowanych skompilowanych w sposób macierzysty.</span><span class="sxs-lookup"><span data-stu-id="f4c89-173">Ascertain whether hello stored procedure T-SQL code uses any features that are not supported for natively compiled stored procedures.</span></span> <span data-ttu-id="f4c89-174">Implementowanie rozwiązania, w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="f4c89-174">Implement workarounds if necessary.</span></span>
   
   * <span data-ttu-id="f4c89-175">Aby uzyskać więcej informacji, zobacz [problemy przy migracji dla natywnie skompilowany na procedur składowanych](http://msdn.microsoft.com/library/dn296678.aspx).</span><span class="sxs-lookup"><span data-stu-id="f4c89-175">For details see [Migration Issues for Natively Compiled Stored Procedures](http://msdn.microsoft.com/library/dn296678.aspx).</span></span>
4. <span data-ttu-id="f4c89-176">Zmień nazwę procedury składowanej starego hello przy użyciu obiekt SP_RENAME.</span><span class="sxs-lookup"><span data-stu-id="f4c89-176">Rename hello old stored procedure by using SP_RENAME.</span></span> <span data-ttu-id="f4c89-177">Lub po prostu UPUSZCZANIA.</span><span class="sxs-lookup"><span data-stu-id="f4c89-177">Or simply DROP it.</span></span>
5. <span data-ttu-id="f4c89-178">Uruchom skrypt edytowany Tworzenie procedury T-SQL.</span><span class="sxs-lookup"><span data-stu-id="f4c89-178">Run your edited CREATE PROCEDURE T-SQL script.</span></span>

## <a name="step-6-run-your-workload-in-test"></a><span data-ttu-id="f4c89-179">Krok 6: Uruchamianie obciążenia w teście</span><span class="sxs-lookup"><span data-stu-id="f4c89-179">Step 6: Run your workload in test</span></span>
<span data-ttu-id="f4c89-180">Uruchom obciążenia w sieci testowej bazy danych jest podobne obciążenia toohello działający w sieci produkcyjnej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="f4c89-180">Run a workload in your test database that is similar toohello workload that runs in your production database.</span></span> <span data-ttu-id="f4c89-181">To powinno ujawnić, bardziej wydajne hello realizowane za korzystanie z funkcji w pamięci hello tabele i procedury składowane.</span><span class="sxs-lookup"><span data-stu-id="f4c89-181">This should reveal hello performance gain achieved by your use of hello In-Memory feature for tables and stored procedures.</span></span>

<span data-ttu-id="f4c89-182">Atrybuty głównych obciążenia hello są:</span><span class="sxs-lookup"><span data-stu-id="f4c89-182">Major attributes of hello workload are:</span></span>

* <span data-ttu-id="f4c89-183">Liczba równoczesnych połączeń.</span><span class="sxs-lookup"><span data-stu-id="f4c89-183">Number of concurrent connections.</span></span>
* <span data-ttu-id="f4c89-184">Stosunek odczytu/zapisu.</span><span class="sxs-lookup"><span data-stu-id="f4c89-184">Read/write ratio.</span></span>

<span data-ttu-id="f4c89-185">tootailor i hello wykonywania testu obciążenia, należy rozważyć użycie hello ostress.exe przydatne narzędzie, które przedstawiono w [tutaj](sql-database-in-memory.md).</span><span class="sxs-lookup"><span data-stu-id="f4c89-185">tootailor and run hello test workload, consider using hello handy ostress.exe tool, which illustrated in [here](sql-database-in-memory.md).</span></span>

<span data-ttu-id="f4c89-186">Opóźnienie sieci toominimize, uruchom test w hello tym samym regionie geograficznym Azure gdzie hello baza danych istnieje.</span><span class="sxs-lookup"><span data-stu-id="f4c89-186">toominimize network latency, run your test in hello same Azure geographic region where hello database exists.</span></span>

## <a name="step-7-post-implementation-monitoring"></a><span data-ttu-id="f4c89-187">Krok 7: Monitorowanie po wdrożeniu</span><span class="sxs-lookup"><span data-stu-id="f4c89-187">Step 7: Post-implementation monitoring</span></span>
<span data-ttu-id="f4c89-188">Należy rozważyć monitorowanie wydajności hello skutków implementacjach użytkownika w pamięci w środowisku produkcyjnym:</span><span class="sxs-lookup"><span data-stu-id="f4c89-188">Consider monitoring hello performance effects of your In-Memory implementations in production:</span></span>

* <span data-ttu-id="f4c89-189">[Monitorowanie magazynu w pamięci](sql-database-in-memory-oltp-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="f4c89-189">[Monitor In-Memory Storage](sql-database-in-memory-oltp-monitoring.md).</span></span>
* [<span data-ttu-id="f4c89-190">Monitorowanie usługi Azure SQL Database przy użyciu dynamicznych widoków zarządzania</span><span class="sxs-lookup"><span data-stu-id="f4c89-190">Monitoring Azure SQL Database using dynamic management views</span></span>](sql-database-monitoring-with-dmvs.md)

## <a name="related-links"></a><span data-ttu-id="f4c89-191">Powiązane linki</span><span class="sxs-lookup"><span data-stu-id="f4c89-191">Related links</span></span>
* [<span data-ttu-id="f4c89-192">(Optymalizacja w pamięci) OLTP w pamięci</span><span class="sxs-lookup"><span data-stu-id="f4c89-192">In-Memory OLTP (In-Memory Optimization)</span></span>](http://msdn.microsoft.com/library/dn133186.aspx)
* [<span data-ttu-id="f4c89-193">Wprowadzenie tooNatively skompilowanych procedur składowanych</span><span class="sxs-lookup"><span data-stu-id="f4c89-193">Introduction tooNatively Compiled Stored Procedures</span></span>](http://msdn.microsoft.com/library/dn133184.aspx)
* [<span data-ttu-id="f4c89-194">Klasyfikator optymalizacji pamięci</span><span class="sxs-lookup"><span data-stu-id="f4c89-194">Memory Optimization Advisor</span></span>](http://msdn.microsoft.com/library/dn284308.aspx)

