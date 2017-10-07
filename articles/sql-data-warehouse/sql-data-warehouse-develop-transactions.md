---
title: "aaaTransactions w usłudze SQL Data Warehouse | Dokumentacja firmy Microsoft"
description: "Wskazówki dotyczące implementowania transakcji w magazynie danych SQL Azure związane z opracowywaniem rozwiązań."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: ae621788-e575-41f5-8bfe-fa04dc4b0b53
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 7c541648553238443b407666612561918096eb61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="transactions-in-sql-data-warehouse"></a><span data-ttu-id="5027a-103">Transakcje w usłudze SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="5027a-103">Transactions in SQL Data Warehouse</span></span>
<span data-ttu-id="5027a-104">Jak można oczekiwać, Magazyn danych SQL obsługuje transakcje jako część obciążenia magazynu danych hello.</span><span class="sxs-lookup"><span data-stu-id="5027a-104">As you would expect, SQL Data Warehouse supports transactions as part of hello data warehouse workload.</span></span> <span data-ttu-id="5027a-105">Jednak tooensure hello wydajności usługi SQL Data Warehouse jest zachowywana na dużą skalę, niektóre funkcje są ograniczone, kiedy porównaniu tooSQL serwera.</span><span class="sxs-lookup"><span data-stu-id="5027a-105">However, tooensure hello performance of SQL Data Warehouse is maintained at scale some features are limited when compared tooSQL Server.</span></span> <span data-ttu-id="5027a-106">W tym artykule wyróżnia różnice hello i list hello innych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="5027a-106">This article highlights hello differences and lists hello others.</span></span> 

## <a name="transaction-isolation-levels"></a><span data-ttu-id="5027a-107">Poziom izolacji transakcji</span><span class="sxs-lookup"><span data-stu-id="5027a-107">Transaction isolation levels</span></span>
<span data-ttu-id="5027a-108">Usługa SQL Data Warehouse implementuje transakcje ACID.</span><span class="sxs-lookup"><span data-stu-id="5027a-108">SQL Data Warehouse implements ACID transactions.</span></span> <span data-ttu-id="5027a-109">Hello izolacji Obsługa transakcyjna hello jest jednak ograniczona zbyt`READ UNCOMMITTED` i nie można zmienić.</span><span class="sxs-lookup"><span data-stu-id="5027a-109">However, hello Isolation of hello transactional support is limited too`READ UNCOMMITTED` and this cannot be changed.</span></span> <span data-ttu-id="5027a-110">Można zaimplementować wiele metod kodowania, które tooprevent zanieczyszczone odczytuje danych, jeśli jest to istotny.</span><span class="sxs-lookup"><span data-stu-id="5027a-110">You can implement a number of coding methods tooprevent dirty reads of data if this is a concern for you.</span></span> <span data-ttu-id="5027a-111">Witaj najpopularniejszych metod wykorzystać CTAS i przełączanie partycji tabeli (często określane jako hello wzorca przesuwanego okna) tooprevent użytkownikom wykonywanie zapytania na danych, który jest nadal przygotowany.</span><span class="sxs-lookup"><span data-stu-id="5027a-111">hello most popular methods leverage both CTAS and table partition switching (often known as hello sliding window pattern) tooprevent users from querying data that is still being prepared.</span></span> <span data-ttu-id="5027a-112">Widoki danych filtr wstępny hello jest również popularnych podejście.</span><span class="sxs-lookup"><span data-stu-id="5027a-112">Views that pre-filter hello data is also a popular approach.</span></span>  

## <a name="transaction-size"></a><span data-ttu-id="5027a-113">Rozmiar transakcji</span><span class="sxs-lookup"><span data-stu-id="5027a-113">Transaction size</span></span>
<span data-ttu-id="5027a-114">Rozmiar jest ograniczony transakcji modyfikacji danych.</span><span class="sxs-lookup"><span data-stu-id="5027a-114">A single data modification transaction is limited in size.</span></span> <span data-ttu-id="5027a-115">Hello limit dzisiaj jest stosowana "dystrybucji".</span><span class="sxs-lookup"><span data-stu-id="5027a-115">hello limit today is applied "per distribution".</span></span> <span data-ttu-id="5027a-116">W związku z tym hello całkowitej alokacji Oblicza iloczyn hello limit liczby dystrybucji hello.</span><span class="sxs-lookup"><span data-stu-id="5027a-116">Therefore, hello total allocation can be calculated by multiplying hello limit by hello distribution count.</span></span> <span data-ttu-id="5027a-117">tooapproximate hello maksymalną liczbę wierszy w transakcji hello dzielenia zakończenia dystrybucji hello przez hello całkowity rozmiar każdego wiersza.</span><span class="sxs-lookup"><span data-stu-id="5027a-117">tooapproximate hello maximum number of rows in hello transaction divide hello distribution cap by hello total size of each row.</span></span> <span data-ttu-id="5027a-118">Dla kolumn o zmiennej długości należy wziąć pod uwagę biorąc długość kolumny średni zamiast hello maksymalny rozmiar.</span><span class="sxs-lookup"><span data-stu-id="5027a-118">For variable length columns consider taking an average column length rather than using hello maximum size.</span></span>

<span data-ttu-id="5027a-119">W tabeli hello poniżej hello zostały wprowadzone następujące założenia:</span><span class="sxs-lookup"><span data-stu-id="5027a-119">In hello table below hello following assumptions have been made:</span></span>

* <span data-ttu-id="5027a-120">Wystąpił nawet rozkład danych</span><span class="sxs-lookup"><span data-stu-id="5027a-120">An even distribution of data has occurred</span></span> 
* <span data-ttu-id="5027a-121">Długość wiersza średni Hello jest 250 bajtów</span><span class="sxs-lookup"><span data-stu-id="5027a-121">hello average row length is 250 bytes</span></span>

| <span data-ttu-id="5027a-122">[JEDNOSTKA DWU][DWU]</span><span class="sxs-lookup"><span data-stu-id="5027a-122">[DWU][DWU]</span></span> | <span data-ttu-id="5027a-123">Cap na dystrybucji (GiB)</span><span class="sxs-lookup"><span data-stu-id="5027a-123">Cap per distribution (GiB)</span></span> | <span data-ttu-id="5027a-124">Liczba dystrybucji</span><span class="sxs-lookup"><span data-stu-id="5027a-124">Number of Distributions</span></span> | <span data-ttu-id="5027a-125">Maksymalny rozmiar transakcji (GiB)</span><span class="sxs-lookup"><span data-stu-id="5027a-125">MAX transaction size (GiB)</span></span> | <span data-ttu-id="5027a-126"># Wierszy na dystrybucji</span><span class="sxs-lookup"><span data-stu-id="5027a-126"># Rows per distribution</span></span> | <span data-ttu-id="5027a-127">Maksymalna liczba wierszy na transakcję</span><span class="sxs-lookup"><span data-stu-id="5027a-127">Max Rows per transaction</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="5027a-128">DW100</span><span class="sxs-lookup"><span data-stu-id="5027a-128">DW100</span></span> |<span data-ttu-id="5027a-129">1</span><span class="sxs-lookup"><span data-stu-id="5027a-129">1</span></span> |<span data-ttu-id="5027a-130">60</span><span class="sxs-lookup"><span data-stu-id="5027a-130">60</span></span> |<span data-ttu-id="5027a-131">60</span><span class="sxs-lookup"><span data-stu-id="5027a-131">60</span></span> |<span data-ttu-id="5027a-132">4,000,000</span><span class="sxs-lookup"><span data-stu-id="5027a-132">4,000,000</span></span> |<span data-ttu-id="5027a-133">240,000,000</span><span class="sxs-lookup"><span data-stu-id="5027a-133">240,000,000</span></span> |
| <span data-ttu-id="5027a-134">DW200</span><span class="sxs-lookup"><span data-stu-id="5027a-134">DW200</span></span> |<span data-ttu-id="5027a-135">1.5</span><span class="sxs-lookup"><span data-stu-id="5027a-135">1.5</span></span> |<span data-ttu-id="5027a-136">60</span><span class="sxs-lookup"><span data-stu-id="5027a-136">60</span></span> |<span data-ttu-id="5027a-137">90</span><span class="sxs-lookup"><span data-stu-id="5027a-137">90</span></span> |<span data-ttu-id="5027a-138">6 000 000</span><span class="sxs-lookup"><span data-stu-id="5027a-138">6,000,000</span></span> |<span data-ttu-id="5027a-139">360,000,000</span><span class="sxs-lookup"><span data-stu-id="5027a-139">360,000,000</span></span> |
| <span data-ttu-id="5027a-140">DW300</span><span class="sxs-lookup"><span data-stu-id="5027a-140">DW300</span></span> |<span data-ttu-id="5027a-141">2.25</span><span class="sxs-lookup"><span data-stu-id="5027a-141">2.25</span></span> |<span data-ttu-id="5027a-142">60</span><span class="sxs-lookup"><span data-stu-id="5027a-142">60</span></span> |<span data-ttu-id="5027a-143">135</span><span class="sxs-lookup"><span data-stu-id="5027a-143">135</span></span> |<span data-ttu-id="5027a-144">9,000,000</span><span class="sxs-lookup"><span data-stu-id="5027a-144">9,000,000</span></span> |<span data-ttu-id="5027a-145">540,000,000</span><span class="sxs-lookup"><span data-stu-id="5027a-145">540,000,000</span></span> |
| <span data-ttu-id="5027a-146">DW400</span><span class="sxs-lookup"><span data-stu-id="5027a-146">DW400</span></span> |<span data-ttu-id="5027a-147">3</span><span class="sxs-lookup"><span data-stu-id="5027a-147">3</span></span> |<span data-ttu-id="5027a-148">60</span><span class="sxs-lookup"><span data-stu-id="5027a-148">60</span></span> |<span data-ttu-id="5027a-149">180</span><span class="sxs-lookup"><span data-stu-id="5027a-149">180</span></span> |<span data-ttu-id="5027a-150">12,000,000</span><span class="sxs-lookup"><span data-stu-id="5027a-150">12,000,000</span></span> |<span data-ttu-id="5027a-151">720,000,000</span><span class="sxs-lookup"><span data-stu-id="5027a-151">720,000,000</span></span> |
| <span data-ttu-id="5027a-152">DW500</span><span class="sxs-lookup"><span data-stu-id="5027a-152">DW500</span></span> |<span data-ttu-id="5027a-153">3.75</span><span class="sxs-lookup"><span data-stu-id="5027a-153">3.75</span></span> |<span data-ttu-id="5027a-154">60</span><span class="sxs-lookup"><span data-stu-id="5027a-154">60</span></span> |<span data-ttu-id="5027a-155">225</span><span class="sxs-lookup"><span data-stu-id="5027a-155">225</span></span> |<span data-ttu-id="5027a-156">15,000,000</span><span class="sxs-lookup"><span data-stu-id="5027a-156">15,000,000</span></span> |<span data-ttu-id="5027a-157">900,000,000</span><span class="sxs-lookup"><span data-stu-id="5027a-157">900,000,000</span></span> |
| <span data-ttu-id="5027a-158">DW600</span><span class="sxs-lookup"><span data-stu-id="5027a-158">DW600</span></span> |<span data-ttu-id="5027a-159">4.5</span><span class="sxs-lookup"><span data-stu-id="5027a-159">4.5</span></span> |<span data-ttu-id="5027a-160">60</span><span class="sxs-lookup"><span data-stu-id="5027a-160">60</span></span> |<span data-ttu-id="5027a-161">270</span><span class="sxs-lookup"><span data-stu-id="5027a-161">270</span></span> |<span data-ttu-id="5027a-162">18,000,000</span><span class="sxs-lookup"><span data-stu-id="5027a-162">18,000,000</span></span> |<span data-ttu-id="5027a-163">1,080,000,000</span><span class="sxs-lookup"><span data-stu-id="5027a-163">1,080,000,000</span></span> |
| <span data-ttu-id="5027a-164">DW1000</span><span class="sxs-lookup"><span data-stu-id="5027a-164">DW1000</span></span> |<span data-ttu-id="5027a-165">7.5</span><span class="sxs-lookup"><span data-stu-id="5027a-165">7.5</span></span> |<span data-ttu-id="5027a-166">60</span><span class="sxs-lookup"><span data-stu-id="5027a-166">60</span></span> |<span data-ttu-id="5027a-167">450</span><span class="sxs-lookup"><span data-stu-id="5027a-167">450</span></span> |<span data-ttu-id="5027a-168">30,000,000</span><span class="sxs-lookup"><span data-stu-id="5027a-168">30,000,000</span></span> |<span data-ttu-id="5027a-169">1,800,000,000</span><span class="sxs-lookup"><span data-stu-id="5027a-169">1,800,000,000</span></span> |
| <span data-ttu-id="5027a-170">DW1200</span><span class="sxs-lookup"><span data-stu-id="5027a-170">DW1200</span></span> |<span data-ttu-id="5027a-171">9</span><span class="sxs-lookup"><span data-stu-id="5027a-171">9</span></span> |<span data-ttu-id="5027a-172">60</span><span class="sxs-lookup"><span data-stu-id="5027a-172">60</span></span> |<span data-ttu-id="5027a-173">540</span><span class="sxs-lookup"><span data-stu-id="5027a-173">540</span></span> |<span data-ttu-id="5027a-174">36,000,000</span><span class="sxs-lookup"><span data-stu-id="5027a-174">36,000,000</span></span> |<span data-ttu-id="5027a-175">2,160,000,000</span><span class="sxs-lookup"><span data-stu-id="5027a-175">2,160,000,000</span></span> |
| <span data-ttu-id="5027a-176">DW1500</span><span class="sxs-lookup"><span data-stu-id="5027a-176">DW1500</span></span> |<span data-ttu-id="5027a-177">11.25</span><span class="sxs-lookup"><span data-stu-id="5027a-177">11.25</span></span> |<span data-ttu-id="5027a-178">60</span><span class="sxs-lookup"><span data-stu-id="5027a-178">60</span></span> |<span data-ttu-id="5027a-179">675</span><span class="sxs-lookup"><span data-stu-id="5027a-179">675</span></span> |<span data-ttu-id="5027a-180">45,000,000</span><span class="sxs-lookup"><span data-stu-id="5027a-180">45,000,000</span></span> |<span data-ttu-id="5027a-181">2,700,000,000</span><span class="sxs-lookup"><span data-stu-id="5027a-181">2,700,000,000</span></span> |
| <span data-ttu-id="5027a-182">DW2000</span><span class="sxs-lookup"><span data-stu-id="5027a-182">DW2000</span></span> |<span data-ttu-id="5027a-183">15</span><span class="sxs-lookup"><span data-stu-id="5027a-183">15</span></span> |<span data-ttu-id="5027a-184">60</span><span class="sxs-lookup"><span data-stu-id="5027a-184">60</span></span> |<span data-ttu-id="5027a-185">900</span><span class="sxs-lookup"><span data-stu-id="5027a-185">900</span></span> |<span data-ttu-id="5027a-186">60,000,000</span><span class="sxs-lookup"><span data-stu-id="5027a-186">60,000,000</span></span> |<span data-ttu-id="5027a-187">3,600,000,000</span><span class="sxs-lookup"><span data-stu-id="5027a-187">3,600,000,000</span></span> |
| <span data-ttu-id="5027a-188">DW3000</span><span class="sxs-lookup"><span data-stu-id="5027a-188">DW3000</span></span> |<span data-ttu-id="5027a-189">22.5</span><span class="sxs-lookup"><span data-stu-id="5027a-189">22.5</span></span> |<span data-ttu-id="5027a-190">60</span><span class="sxs-lookup"><span data-stu-id="5027a-190">60</span></span> |<span data-ttu-id="5027a-191">1,350</span><span class="sxs-lookup"><span data-stu-id="5027a-191">1,350</span></span> |<span data-ttu-id="5027a-192">90,000,000</span><span class="sxs-lookup"><span data-stu-id="5027a-192">90,000,000</span></span> |<span data-ttu-id="5027a-193">5,400,000,000</span><span class="sxs-lookup"><span data-stu-id="5027a-193">5,400,000,000</span></span> |
| <span data-ttu-id="5027a-194">DW6000</span><span class="sxs-lookup"><span data-stu-id="5027a-194">DW6000</span></span> |<span data-ttu-id="5027a-195">45</span><span class="sxs-lookup"><span data-stu-id="5027a-195">45</span></span> |<span data-ttu-id="5027a-196">60</span><span class="sxs-lookup"><span data-stu-id="5027a-196">60</span></span> |<span data-ttu-id="5027a-197">2,700</span><span class="sxs-lookup"><span data-stu-id="5027a-197">2,700</span></span> |<span data-ttu-id="5027a-198">180,000,000</span><span class="sxs-lookup"><span data-stu-id="5027a-198">180,000,000</span></span> |<span data-ttu-id="5027a-199">10,800,000,000</span><span class="sxs-lookup"><span data-stu-id="5027a-199">10,800,000,000</span></span> |

<span data-ttu-id="5027a-200">limit rozmiaru transakcji Hello jest stosowane osobno do każdej operacji lub transakcji.</span><span class="sxs-lookup"><span data-stu-id="5027a-200">hello transaction size limit is applied per transaction or operation.</span></span> <span data-ttu-id="5027a-201">Nie została zastosowana we wszystkich równoczesnych transakcji.</span><span class="sxs-lookup"><span data-stu-id="5027a-201">It is not applied across all concurrent transactions.</span></span> <span data-ttu-id="5027a-202">W związku z tym każda transakcja jest dozwolone toowrite ilość danych toohello dziennika.</span><span class="sxs-lookup"><span data-stu-id="5027a-202">Therefore each transaction is permitted toowrite this amount of data toohello log.</span></span> 

<span data-ttu-id="5027a-203">toooptimize i zminimalizować ilość hello zapisanych dziennika toohello danych można znaleźć toohello [transakcji najlepsze rozwiązania] [ Transactions best practices] artykułu.</span><span class="sxs-lookup"><span data-stu-id="5027a-203">toooptimize and minimize hello amount of data written toohello log please refer toohello [Transactions best practices][Transactions best practices] article.</span></span>

> [!WARNING]
> <span data-ttu-id="5027a-204">Maksymalny rozmiar transakcji można osiągnąć jedynie dla skrótu lub tabele ROUND_ROBIN rozproszonych gdzie hello rozprzestrzeniania się hello danych Hello jest parzysta.</span><span class="sxs-lookup"><span data-stu-id="5027a-204">hello maximum transaction size can only be achieved for HASH or ROUND_ROBIN distributed tables where hello spread of hello data is even.</span></span> <span data-ttu-id="5027a-205">Jeśli transakcji hello zapisuje dane w sposób spowodowałoby zafałszowanie dystrybucje toohello następnie hello limit jest prawdopodobnie toobe osiągnął toohello poprzednich transakcji maksymalny rozmiar.</span><span class="sxs-lookup"><span data-stu-id="5027a-205">If hello transaction is writing data in a skewed fashion toohello distributions then hello limit is likely toobe reached prior toohello maximum transaction size.</span></span>
> <!--REPLICATED_TABLE-->
> 
> 

## <a name="transaction-state"></a><span data-ttu-id="5027a-206">Stan transakcji</span><span class="sxs-lookup"><span data-stu-id="5027a-206">Transaction state</span></span>
<span data-ttu-id="5027a-207">Usługa SQL Data Warehouse używa hello XACT_STATE() funkcja tooreport transakcji nie powiodło się przy użyciu wartości hello -2.</span><span class="sxs-lookup"><span data-stu-id="5027a-207">SQL Data Warehouse uses hello XACT_STATE() function tooreport a failed transaction using hello value -2.</span></span> <span data-ttu-id="5027a-208">Oznacza to, że hello transakcji nie powiodło się i jest oznaczony do wycofania tylko</span><span class="sxs-lookup"><span data-stu-id="5027a-208">This means that hello transaction has failed and is marked for rollback only</span></span>

> [!NOTE]
> <span data-ttu-id="5027a-209">Witaj użyć-2 toodenote funkcja XACT_STATE hello nieudanych transakcji tooSQL inaczej reprezentuje serwera.</span><span class="sxs-lookup"><span data-stu-id="5027a-209">hello use of -2 by hello XACT_STATE function toodenote a failed transaction represents different behavior tooSQL Server.</span></span> <span data-ttu-id="5027a-210">Program SQL Server używa hello wartość -1 toorepresent której transakcji.</span><span class="sxs-lookup"><span data-stu-id="5027a-210">SQL Server uses hello value -1 toorepresent an un-committable transaction.</span></span> <span data-ttu-id="5027a-211">SQL Server może tolerować błędy wewnątrz transakcji bez konieczności toobe oznaczony jako której.</span><span class="sxs-lookup"><span data-stu-id="5027a-211">SQL Server can tolerate some errors inside a transaction without it having toobe marked as un-committable.</span></span> <span data-ttu-id="5027a-212">Na przykład `SELECT 1/0` może spowodować błąd, ale nie wymusić transakcji, w której stan.</span><span class="sxs-lookup"><span data-stu-id="5027a-212">For example `SELECT 1/0` would cause an error but not force a transaction into an un-committable state.</span></span> <span data-ttu-id="5027a-213">SQL Server umożliwia również odczytów w hello której transakcji.</span><span class="sxs-lookup"><span data-stu-id="5027a-213">SQL Server also permits reads in hello un-committable transaction.</span></span> <span data-ttu-id="5027a-214">Jednak usługa SQL Data Warehouse nie zezwala na to zrobić.</span><span class="sxs-lookup"><span data-stu-id="5027a-214">However, SQL Data Warehouse does not let you do this.</span></span> <span data-ttu-id="5027a-215">W przypadku wystąpienia błędu wewnątrz transakcji SQL Data Warehouse automatycznie wprowadzi stanu hello -2 i nie będą mogli toomake wszelkie dodatkowe wybierz instrukcje dopóki instrukcji hello została wycofana.</span><span class="sxs-lookup"><span data-stu-id="5027a-215">If an error occurs inside a SQL Data Warehouse transaction it will automatically enter hello -2 state and you will not be able toomake any further select statements until hello statement has been rolled back.</span></span> <span data-ttu-id="5027a-216">Dlatego jest ważne toocheck czy toosee kodu aplikacji, gdy jest używana podczas XACT_STATE() może być konieczne toomake modyfikacji kodu.</span><span class="sxs-lookup"><span data-stu-id="5027a-216">It is therefore important toocheck that your application code toosee if it uses  XACT_STATE() as you may need toomake code modifications.</span></span>
> 
> 

<span data-ttu-id="5027a-217">Na przykład w programie SQL Server można napotkać transakcji, która wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="5027a-217">For example, in SQL Server you might see a transaction that looks like this:</span></span>

```sql
SET NOCOUNT ON;
DECLARE @xact_state smallint = 0;

BEGIN TRAN
    BEGIN TRY
        DECLARE @i INT;
        SET     @i = CONVERT(INT,'ABC');
    END TRY
    BEGIN CATCH
        SET @xact_state = XACT_STATE();

        SELECT  ERROR_NUMBER()    AS ErrNumber
        ,       ERROR_SEVERITY()  AS ErrSeverity
        ,       ERROR_STATE()     AS ErrState
        ,       ERROR_PROCEDURE() AS ErrProcedure
        ,       ERROR_MESSAGE()   AS ErrMessage
        ;

        IF @@TRANCOUNT > 0
        BEGIN
            PRINT 'ROLLBACK';
            ROLLBACK TRAN;
        END

    END CATCH;

IF @@TRANCOUNT >0
BEGIN
    PRINT 'COMMIT';
    COMMIT TRAN;
END

SELECT @xact_state AS TransactionState;
```

<span data-ttu-id="5027a-218">Jeśli pozostanie kodu, ponieważ jest powyżej zostanie wyświetlony następujący komunikat o błędzie hello:</span><span class="sxs-lookup"><span data-stu-id="5027a-218">If you leave your code as it is above then you will get hello following error message:</span></span>

<span data-ttu-id="5027a-219">Msg 111233, poziom 16, stan 1 wiersz 1 111233; hello bieżąca transakcja została przerwana, a wszystkie oczekujące zmiany mają została wycofana.</span><span class="sxs-lookup"><span data-stu-id="5027a-219">Msg 111233, Level 16, State 1, Line 1 111233;hello current transaction has aborted, and any pending changes have been rolled back.</span></span> <span data-ttu-id="5027a-220">Przyczyna: W stanie tylko do wycofania transakcji nie zostało jawnie wycofane przed DDL i DML instrukcji SELECT.</span><span class="sxs-lookup"><span data-stu-id="5027a-220">Cause: A transaction in a rollback-only state was not explicitly rolled back before a DDL, DML or SELECT statement.</span></span>

<span data-ttu-id="5027a-221">Nie również otrzymasz dane wyjściowe hello hello ERROR_ * funkcji.</span><span class="sxs-lookup"><span data-stu-id="5027a-221">You will also not get hello output of hello ERROR_* functions.</span></span>

<span data-ttu-id="5027a-222">W usłudze SQL Data Warehouse kodu hello musi toobe nieco zmodyfikowany:</span><span class="sxs-lookup"><span data-stu-id="5027a-222">In SQL Data Warehouse hello code needs toobe slightly altered:</span></span>

```sql
SET NOCOUNT ON;
DECLARE @xact_state smallint = 0;

BEGIN TRAN
    BEGIN TRY
        DECLARE @i INT;
        SET     @i = CONVERT(INT,'ABC');
    END TRY
    BEGIN CATCH
        SET @xact_state = XACT_STATE();

        IF @@TRANCOUNT > 0
        BEGIN
            PRINT 'ROLLBACK';
            ROLLBACK TRAN;
        END

        SELECT  ERROR_NUMBER()    AS ErrNumber
        ,       ERROR_SEVERITY()  AS ErrSeverity
        ,       ERROR_STATE()     AS ErrState
        ,       ERROR_PROCEDURE() AS ErrProcedure
        ,       ERROR_MESSAGE()   AS ErrMessage
        ;
    END CATCH;

IF @@TRANCOUNT >0
BEGIN
    PRINT 'COMMIT';
    COMMIT TRAN;
END

SELECT @xact_state AS TransactionState;
```

<span data-ttu-id="5027a-223">Hello oczekuje się, że zachowanie jest teraz przestrzegane.</span><span class="sxs-lookup"><span data-stu-id="5027a-223">hello expected behavior is now observed.</span></span> <span data-ttu-id="5027a-224">Błąd Hello w transakcji hello jest zarządzana i hello ERROR_ * funkcji Podaj wartości, zgodnie z oczekiwaniami.</span><span class="sxs-lookup"><span data-stu-id="5027a-224">hello error in hello transaction is managed and hello ERROR_* functions provide values as expected.</span></span>

<span data-ttu-id="5027a-225">Zmieniono jest tym hello `ROLLBACK` z hello transakcji wcześniej toohappen hello odczytu informacji o błędach hello w hello `CATCH` bloku.</span><span class="sxs-lookup"><span data-stu-id="5027a-225">All that has changed is that hello `ROLLBACK` of hello transaction had toohappen before hello read of hello error information in hello `CATCH` block.</span></span>

## <a name="errorline-function"></a><span data-ttu-id="5027a-226">ERROR_LINE() — funkcja</span><span class="sxs-lookup"><span data-stu-id="5027a-226">Error_Line() function</span></span>
<span data-ttu-id="5027a-227">Warto również zauważyć, że usługi SQL Data Warehouse wdrożenia lub nie obsługuje hello ERROR_LINE() — funkcja.</span><span class="sxs-lookup"><span data-stu-id="5027a-227">It is also worth noting that SQL Data Warehouse does not implement or support hello ERROR_LINE() function.</span></span> <span data-ttu-id="5027a-228">Jeśli masz to w kodzie należy tooremove go toobe zgodne z usługą Magazyn danych SQL.</span><span class="sxs-lookup"><span data-stu-id="5027a-228">If you have this in your code you will need tooremove it toobe compliant with SQL Data Warehouse.</span></span> <span data-ttu-id="5027a-229">W zamian użyj etykiet zapytania w kodzie tooimplement równoważne funkcje.</span><span class="sxs-lookup"><span data-stu-id="5027a-229">Use query labels in your code instead tooimplement equivalent functionality.</span></span> <span data-ttu-id="5027a-230">Zobacz toohello [etykiety] [ LABEL] artykułu, aby uzyskać więcej informacji na temat tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="5027a-230">Please refer toohello [LABEL][LABEL] article for more details on this feature.</span></span>

## <a name="using-throw-and-raiserror"></a><span data-ttu-id="5027a-231">Przy użyciu THROW i RAISERROR</span><span class="sxs-lookup"><span data-stu-id="5027a-231">Using THROW and RAISERROR</span></span>
<span data-ttu-id="5027a-232">THROW jest hello nowoczesną wykonania na występowanie wyjątków w usłudze SQL Data Warehouse, ale obsługiwana jest również RAISERROR.</span><span class="sxs-lookup"><span data-stu-id="5027a-232">THROW is hello more modern implementation for raising exceptions in SQL Data Warehouse but RAISERROR is also supported.</span></span> <span data-ttu-id="5027a-233">Istnieje kilka różnic, które warto płatności toohowever uwagi.</span><span class="sxs-lookup"><span data-stu-id="5027a-233">There are a few differences that are worth paying attention toohowever.</span></span>

* <span data-ttu-id="5027a-234">Komunikaty o błędach cyfr nie może być w hello 150 000 100 000 zakres THROW zdefiniowane przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="5027a-234">User defined error messages numbers cannot be in hello 100,000 - 150,000 range for THROW</span></span>
* <span data-ttu-id="5027a-235">Komunikaty o błędach RAISERROR są ustalone na poziomie 50 000</span><span class="sxs-lookup"><span data-stu-id="5027a-235">RAISERROR error messages are fixed at 50,000</span></span>
* <span data-ttu-id="5027a-236">Korzystanie z widoku sys.messages nie jest obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="5027a-236">Use of sys.messages is not supported</span></span>

## <a name="limitiations"></a><span data-ttu-id="5027a-237">Limitiations</span><span class="sxs-lookup"><span data-stu-id="5027a-237">Limitiations</span></span>
<span data-ttu-id="5027a-238">Magazyn danych SQL ma kilka ograniczeń, które odnoszą się tootransactions.</span><span class="sxs-lookup"><span data-stu-id="5027a-238">SQL Data Warehouse does have a few other restrictions that relate tootransactions.</span></span>

<span data-ttu-id="5027a-239">Są one w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="5027a-239">They are as follows:</span></span>

* <span data-ttu-id="5027a-240">Nie transakcji rozproszonych</span><span class="sxs-lookup"><span data-stu-id="5027a-240">No distributed transactions</span></span>
* <span data-ttu-id="5027a-241">Nie transakcji zagnieżdżonych dozwolone</span><span class="sxs-lookup"><span data-stu-id="5027a-241">No nested transactions permitted</span></span>
* <span data-ttu-id="5027a-242">Bez zapisu punkty dozwolone</span><span class="sxs-lookup"><span data-stu-id="5027a-242">No save points allowed</span></span>
* <span data-ttu-id="5027a-243">Brak transakcji o nazwie</span><span class="sxs-lookup"><span data-stu-id="5027a-243">No named transactions</span></span>
* <span data-ttu-id="5027a-244">Nie zaznaczonych transakcji</span><span class="sxs-lookup"><span data-stu-id="5027a-244">No marked transactions</span></span>
* <span data-ttu-id="5027a-245">Brak obsługi języka DDL, takie jak `CREATE TABLE` wewnątrz użytkownika zdefiniowanych transakcji</span><span class="sxs-lookup"><span data-stu-id="5027a-245">No support for DDL such as `CREATE TABLE` inside a user defined transaction</span></span>

## <a name="next-steps"></a><span data-ttu-id="5027a-246">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5027a-246">Next steps</span></span>
<span data-ttu-id="5027a-247">toolearn więcej informacji na temat optymalizacji transakcji, zobacz [transakcji najlepsze rozwiązania][Transactions best practices].</span><span class="sxs-lookup"><span data-stu-id="5027a-247">toolearn more about optimizing transactions, see [Transactions best practices][Transactions best practices].</span></span>  <span data-ttu-id="5027a-248">toolearn dotyczące innych najlepszych rozwiązań usługi SQL Data Warehouse, zobacz [najlepsze rozwiązania w zakresie usługi SQL Data Warehouse][SQL Data Warehouse best practices].</span><span class="sxs-lookup"><span data-stu-id="5027a-248">toolearn about other SQL Data Warehouse best practices, see [SQL Data Warehouse best practices][SQL Data Warehouse best practices].</span></span>

<!--Image references-->

<!--Article references-->
[DWU]: ./sql-data-warehouse-overview-what-is.md
[development overview]: ./sql-data-warehouse-overview-develop.md
[Transactions best practices]: ./sql-data-warehouse-develop-best-practices-transactions.md
[SQL Data Warehouse best practices]: ./sql-data-warehouse-best-practices.md
[LABEL]: ./sql-data-warehouse-develop-label.md

<!--MSDN references-->

<!--Other Web references-->
