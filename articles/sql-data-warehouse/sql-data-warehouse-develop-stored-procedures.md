---
title: "procedury aaaStored w usłudze SQL Data Warehouse | Dokumentacja firmy Microsoft"
description: "Wskazówki dotyczące implementowania procedur przechowywanych w usłudze Azure SQL Data Warehouse związane z opracowywaniem rozwiązań."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: 9b238789-6efe-4820-bf77-5a5da2afa0e8
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 416252dd3dea95c66aa5e886860b933b22578002
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="stored-procedures-in-sql-data-warehouse"></a><span data-ttu-id="458ed-103">Procedury składowane w usłudze SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="458ed-103">Stored procedures in SQL Data Warehouse</span></span>
<span data-ttu-id="458ed-104">Magazyn danych SQL obsługuje wiele funkcji języka Transact-SQL hello dostępnych w programie SQL Server.</span><span class="sxs-lookup"><span data-stu-id="458ed-104">SQL Data Warehouse supports many of hello Transact-SQL features found in SQL Server.</span></span> <span data-ttu-id="458ed-105">Są ważniejsze skalowania w poziomie określonych funkcji, firma Microsoft będzie tooleverage toomaximize hello wydajność rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="458ed-105">More importantly there are scale out specific features that we will want tooleverage toomaximize hello performance of your solution.</span></span>

<span data-ttu-id="458ed-106">Toomaintain hello skalowalność i wydajność usługi SQL Data Warehouse są jednak także pewne funkcje i możliwości, mające różnice funkcjonalne i inne osoby, które nie są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="458ed-106">However, toomaintain hello scale and performance of SQL Data Warehouse there are also some features and functionality that have behavioral differences and others that are not supported.</span></span>

<span data-ttu-id="458ed-107">W tym artykule opisano, jak tooimplement przechowywanych procedur w usłudze SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="458ed-107">This article explains how tooimplement stored procedures within SQL Data Warehouse.</span></span>

## <a name="introducing-stored-procedures"></a><span data-ttu-id="458ed-108">Wprowadzenie do procedury składowane</span><span class="sxs-lookup"><span data-stu-id="458ed-108">Introducing stored procedures</span></span>
<span data-ttu-id="458ed-109">Procedury składowane są to dobry sposób na hermetyzując kodu SQL; przechowywanie ich danych zamknij tooyour w hello hurtowni danych.</span><span class="sxs-lookup"><span data-stu-id="458ed-109">Stored procedures are a great way for encapsulating your SQL code; storing it close tooyour data in hello data warehouse.</span></span> <span data-ttu-id="458ed-110">Hermetyzując hello kodu w jednostki zarządzane procedur składowanych pomóc deweloperom modularyzacji ich rozwiązań. ułatwianie większa ponownego wykorzystywania kodu.</span><span class="sxs-lookup"><span data-stu-id="458ed-110">By encapsulating hello code into manageable units stored procedures help developers modularize their solutions; facilitating greater re-usability of code.</span></span> <span data-ttu-id="458ed-111">Każdej procedury składowanej także zaakceptować toomake parametry im bardziej elastyczne.</span><span class="sxs-lookup"><span data-stu-id="458ed-111">Each stored procedure can also accept parameters toomake them even more flexible.</span></span>

<span data-ttu-id="458ed-112">Magazyn danych SQL zawiera implementację uproszczony i zoptymalizowany procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="458ed-112">SQL Data Warehouse provides a simplified and streamlined stored procedure implementation.</span></span> <span data-ttu-id="458ed-113">Witaj największych różnicę w porównaniu tooSQL serwera jest który hello procedury składowanej nie jest wstępnie skompilowanego kodu.</span><span class="sxs-lookup"><span data-stu-id="458ed-113">hello biggest difference compared tooSQL Server is that hello stored procedure is not pre-compiled code.</span></span> <span data-ttu-id="458ed-114">W hurtowni danych możemy dotyczy ogólnie mniej hello czas kompilacji.</span><span class="sxs-lookup"><span data-stu-id="458ed-114">In data warehouses we are generally less concerned with hello compilation time.</span></span> <span data-ttu-id="458ed-115">Jest większe znaczenie kodu procedury przechowywane hello poprawnie są zoptymalizowane podczas działania względem dużych ilości danych.</span><span class="sxs-lookup"><span data-stu-id="458ed-115">It is more important that hello stored procedure code is correctly optimised when operating against large data volumes.</span></span> <span data-ttu-id="458ed-116">Celem Hello jest toosave godziny, minuty i sekundy nie milisekund.</span><span class="sxs-lookup"><span data-stu-id="458ed-116">hello goal is toosave hours, minutes and seconds not milliseconds.</span></span> <span data-ttu-id="458ed-117">Dlatego jest bardziej użyteczne toothink procedur składowanych jako kontenery logiki SQL.</span><span class="sxs-lookup"><span data-stu-id="458ed-117">It is therefore more helpful toothink of stored procedures as containers for SQL logic.</span></span>     

<span data-ttu-id="458ed-118">Gdy usługi SQL Data Warehouse wykonuje instrukcji SQL procedury składowanej hello są przeanalizować, translacji i zoptymalizowany w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="458ed-118">When SQL Data Warehouse executes your stored procedure hello SQL statements are parsed, translated and optimized at run time.</span></span> <span data-ttu-id="458ed-119">W trakcie tego procesu każda instrukcja jest konwertowany na zapytań rozproszonych.</span><span class="sxs-lookup"><span data-stu-id="458ed-119">During this process each statement is converted into distributed queries.</span></span> <span data-ttu-id="458ed-120">Witaj kodu SQL, który faktycznie jest wykonywane względem danych hello jest kwerenda różnych toohello przesłane.</span><span class="sxs-lookup"><span data-stu-id="458ed-120">hello SQL code that is actually executed against hello data is different toohello query submitted.</span></span>

## <a name="nesting-stored-procedures"></a><span data-ttu-id="458ed-121">Procedury przechowywane zagnieżdżenia</span><span class="sxs-lookup"><span data-stu-id="458ed-121">Nesting stored procedures</span></span>
<span data-ttu-id="458ed-122">Jeśli procedury składowane wywołania innych procedur składowanych lub wykonać dynamicznej sql, a następnie procedurę składowaną wewnętrzny hello lub wywołanie kodu jest nazywany toobe zagnieżdżone.</span><span class="sxs-lookup"><span data-stu-id="458ed-122">When stored procedures call other stored procedures or execute dynamic sql then hello inner stored procedure or code invocation is said toobe nested.</span></span>

<span data-ttu-id="458ed-123">Magazyn danych SQL obsługuje maksymalnie 8 poziomów zagnieżdżenia.</span><span class="sxs-lookup"><span data-stu-id="458ed-123">SQL Data Warehouse support a maximum of 8 nesting levels.</span></span> <span data-ttu-id="458ed-124">Jest to tooSQL nieco inny serwer.</span><span class="sxs-lookup"><span data-stu-id="458ed-124">This is slightly different tooSQL Server.</span></span> <span data-ttu-id="458ed-125">poziom zagnieżdżania Hello w programie SQL Server to 32.</span><span class="sxs-lookup"><span data-stu-id="458ed-125">hello nest level in SQL Server is 32.</span></span>

<span data-ttu-id="458ed-126">Wywołanie najwyższego poziomu procedury składowanej Hello oznacza toonest poziomu 1</span><span class="sxs-lookup"><span data-stu-id="458ed-126">hello top level stored procedure call equates toonest level 1</span></span>

```sql
EXEC prc_nesting
```
<span data-ttu-id="458ed-127">Jeśli hello przechowywane procedury powoduje EXEC innego wywołania, spowoduje to zwiększenie too2 poziomu zagnieżdżania hello</span><span class="sxs-lookup"><span data-stu-id="458ed-127">If hello stored procedure also makes another EXEC call then this will increase hello nest level too2</span></span>

```sql
CREATE PROCEDURE prc_nesting
AS
EXEC prc_nesting_2  -- This call is nest level 2
GO
EXEC prc_nesting
```
<span data-ttu-id="458ed-128">Jeśli drugiej procedury hello następnie wykonuje niektóre dynamiczne sql następnie zwiększy to too3 poziomu zagnieżdżania hello</span><span class="sxs-lookup"><span data-stu-id="458ed-128">If hello second procedure then executes some dynamic sql then this will increase hello nest level too3</span></span>

```sql
CREATE PROCEDURE prc_nesting_2
AS
EXEC sp_executesql 'SELECT 'another nest level'  -- This call is nest level 2
GO
EXEC prc_nesting
```

<span data-ttu-id="458ed-129">Uwaga SQL Data Warehouse nie obsługuje obecnie@NESTLEVEL.</span><span class="sxs-lookup"><span data-stu-id="458ed-129">Note SQL Data Warehouse does not currently support @@NESTLEVEL.</span></span> <span data-ttu-id="458ed-130">Konieczne będzie tookeep ścieżką poziom zagnieżdżania samodzielnie.</span><span class="sxs-lookup"><span data-stu-id="458ed-130">You will need tookeep a track of your nest level yourself.</span></span> <span data-ttu-id="458ed-131">Jest mało prawdopodobne, nastąpi trafienie poziomu limit zagnieżdżania hello 8, ale jeśli użytkownik czy należy toore pracy kodu, a "spłaszczanie" go tak, aby zmieścił się w ten limit.</span><span class="sxs-lookup"><span data-stu-id="458ed-131">It is unlikely you will hit hello 8 nest level limit but if you do you will need toore-work your code and "flatten" it so that it fits within this limit.</span></span>

## <a name="insertexecute"></a><span data-ttu-id="458ed-132">INSERT... WYKONANIE</span><span class="sxs-lookup"><span data-stu-id="458ed-132">INSERT..EXECUTE</span></span>
<span data-ttu-id="458ed-133">Usługa SQL Data Warehouse pozwala tooconsume hello zestawu wyników procedury składowanej z instrukcji INSERT.</span><span class="sxs-lookup"><span data-stu-id="458ed-133">SQL Data Warehouse does not permit you tooconsume hello result set of a stored procedure with an INSERT statement.</span></span> <span data-ttu-id="458ed-134">Istnieje jednak alternatywne podejście, których można użyć.</span><span class="sxs-lookup"><span data-stu-id="458ed-134">However, there is an alternative approach you can use.</span></span>

<span data-ttu-id="458ed-135">Zobacz toohello poniższego artykułu [tabel tymczasowych] na przykład o tym, jak toodo to.</span><span class="sxs-lookup"><span data-stu-id="458ed-135">Please refer toohello following article on [temporary tables] for an example on how toodo this.</span></span>

## <a name="limitations"></a><span data-ttu-id="458ed-136">Ograniczenia</span><span class="sxs-lookup"><span data-stu-id="458ed-136">Limitations</span></span>
<span data-ttu-id="458ed-137">Brak niektórych aspektów procedury przechowywanej Transact-SQL, które nie są zaimplementowane w usłudze SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="458ed-137">There are some aspects of Transact-SQL stored procedures that are not implemented in SQL Data Warehouse.</span></span>

<span data-ttu-id="458ed-138">Są to:</span><span class="sxs-lookup"><span data-stu-id="458ed-138">They are:</span></span>

* <span data-ttu-id="458ed-139">tymczasowych procedur składowanych</span><span class="sxs-lookup"><span data-stu-id="458ed-139">temporary stored procedures</span></span>
* <span data-ttu-id="458ed-140">numerowane procedury składowane</span><span class="sxs-lookup"><span data-stu-id="458ed-140">numbered stored procedures</span></span>
* <span data-ttu-id="458ed-141">rozszerzone procedury składowane</span><span class="sxs-lookup"><span data-stu-id="458ed-141">extended stored procedures</span></span>
* <span data-ttu-id="458ed-142">Procedur składowanych CLR</span><span class="sxs-lookup"><span data-stu-id="458ed-142">CLR stored procedures</span></span>
* <span data-ttu-id="458ed-143">Opcja szyfrowania</span><span class="sxs-lookup"><span data-stu-id="458ed-143">encryption option</span></span>
* <span data-ttu-id="458ed-144">opcji replikacji</span><span class="sxs-lookup"><span data-stu-id="458ed-144">replication option</span></span>
* <span data-ttu-id="458ed-145">Parametry przechowywanymi w tabeli</span><span class="sxs-lookup"><span data-stu-id="458ed-145">table-valued parameters</span></span>
* <span data-ttu-id="458ed-146">Parametry tylko do odczytu</span><span class="sxs-lookup"><span data-stu-id="458ed-146">read-only parameters</span></span>
* <span data-ttu-id="458ed-147">domyślne parametry</span><span class="sxs-lookup"><span data-stu-id="458ed-147">default parameters</span></span>
* <span data-ttu-id="458ed-148">Kontekst wykonywania</span><span class="sxs-lookup"><span data-stu-id="458ed-148">execution contexts</span></span>
* <span data-ttu-id="458ed-149">Return — instrukcja</span><span class="sxs-lookup"><span data-stu-id="458ed-149">return statement</span></span>

## <a name="next-steps"></a><span data-ttu-id="458ed-150">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="458ed-150">Next steps</span></span>
<span data-ttu-id="458ed-151">Aby uzyskać więcej porad programistycznych, zobacz [omówienie tworzenia][development overview].</span><span class="sxs-lookup"><span data-stu-id="458ed-151">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[tabel tymczasowych]: ./sql-data-warehouse-tables-temporary.md#modularizing-code
[development overview]: ./sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[nest level]: https://msdn.microsoft.com/library/ms187371.aspx

<!--Other Web references-->
