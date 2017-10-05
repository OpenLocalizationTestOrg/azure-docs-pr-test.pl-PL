---
title: "Zarządzanie moc obliczeniową w usłudze Azure SQL Data Warehouse (omówienie) | Dokumentacja firmy Microsoft"
description: "Wydajność skalowania możliwości w usłudze Azure SQL Data Warehouse. Skalowanie w poziomie przez dostosowanie wartości dwu lub wstrzymywać i wznawiać zasobów obliczeniowych w celu ograniczenia kosztów."
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: johnmac
editor: 
ms.assetid: e13a82b0-abfe-429f-ac3c-f2b6789a70c6
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 03/22/2017
ms.author: elbutter
ms.openlocfilehash: abe22f542a79714f6e894870872ee6b76ffe7633
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-overview"></a><span data-ttu-id="cf130-104">Zarządzanie moc obliczeniową w usłudze Azure SQL Data Warehouse (omówienie)</span><span class="sxs-lookup"><span data-stu-id="cf130-104">Manage compute power in Azure SQL Data Warehouse (Overview)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="cf130-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="cf130-105">Overview</span></span>](sql-data-warehouse-manage-compute-overview.md)
> * [<span data-ttu-id="cf130-106">Portal</span><span class="sxs-lookup"><span data-stu-id="cf130-106">Portal</span></span>](sql-data-warehouse-manage-compute-portal.md)
> * [<span data-ttu-id="cf130-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="cf130-107">PowerShell</span></span>](sql-data-warehouse-manage-compute-powershell.md)
> * [<span data-ttu-id="cf130-108">REST</span><span class="sxs-lookup"><span data-stu-id="cf130-108">REST</span></span>](sql-data-warehouse-manage-compute-rest-api.md)
> * [<span data-ttu-id="cf130-109">TSQL</span><span class="sxs-lookup"><span data-stu-id="cf130-109">TSQL</span></span>](sql-data-warehouse-manage-compute-tsql.md)
>
>

<span data-ttu-id="cf130-110">Architektura usługi SQL Data Warehouse oddziela magazynu i zasobów obliczeniowych, umożliwiając niezależne skalowanie.</span><span class="sxs-lookup"><span data-stu-id="cf130-110">The architecture of SQL Data Warehouse separates storage and compute, allowing each to scale independently.</span></span> <span data-ttu-id="cf130-111">W związku z tym obliczeniowe mogą być skalowane do wymagań dotyczących wydajności niezależnie od ilości danych.</span><span class="sxs-lookup"><span data-stu-id="cf130-111">As a result, compute can be scaled to meet performance demands independent of the amount of data.</span></span> <span data-ttu-id="cf130-112">Fizyczne konsekwencją tej architektury jest to, że [rozliczeń] [ billed] dla zasobów obliczeniowych i magazynu jest oddzielona.</span><span class="sxs-lookup"><span data-stu-id="cf130-112">A natural consequence of this architecture is that [billing][billed] for compute and storage is separate.</span></span> 

<span data-ttu-id="cf130-113">Ten przegląd zawiera opis jak skalować w poziomie współpracuje z usługi SQL Data Warehouse i jak wykorzystywać wstrzymania, wznowienia i skalować możliwości usługi SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="cf130-113">This overview describes how scale out works with SQL Data Warehouse and how to utilize the pause, resume, and scale capabilities of SQL Data Warehouse.</span></span> <span data-ttu-id="cf130-114">Zapoznaj się [jednostki (jednostek dwu) magazynu danych] [ data warehouse units (DWUs)] stronę, aby dowiedzieć się jak powiązanych jednostek dwu i wydajność.</span><span class="sxs-lookup"><span data-stu-id="cf130-114">Consult the [data warehouse units (DWUs)][data warehouse units (DWUs)] page to learn how DWUs and performance are related.</span></span> 

## <a name="how-compute-management-operations-work-in-sql-data-warehouse"></a><span data-ttu-id="cf130-115">Jak obliczeń operacje zarządzania działają w usłudze SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="cf130-115">How compute management operations work in SQL Data Warehouse</span></span>
<span data-ttu-id="cf130-116">Architektura magazynu danych SQL składa się z węzeł kontrolny, węzłów obliczeniowych i warstwy magazynu rozmieszczenie dystrybucje 60.</span><span class="sxs-lookup"><span data-stu-id="cf130-116">The architecture for SQL Data Warehouse consists of a control node, compute nodes, and the storage layer spread across 60 distributions.</span></span> 

<span data-ttu-id="cf130-117">Podczas normalnej sesji aktywnych w usłudze SQL Data Warehouse węzła głównego systemu zarządza metadanych i zawiera Optymalizator zapytań rozproszonych.</span><span class="sxs-lookup"><span data-stu-id="cf130-117">During a normal active session in SQL Data Warehouse, your system's head node manages the metadata and contains the distributed query optimizer.</span></span> <span data-ttu-id="cf130-118">Poniżej tego węzła głównego są węzłów obliczeniowych i warstwą magazynu.</span><span class="sxs-lookup"><span data-stu-id="cf130-118">Beneath this head node are your compute nodes and your storage layer.</span></span> <span data-ttu-id="cf130-119">400 DWU system ma jednego węzła głównego, czterech węzłów obliczeniowych i magazynu, składającego się z 60 dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="cf130-119">For a DWU 400, your system has one head node, four compute nodes, and the storage layer, consisting of 60 distributions.</span></span> 

<span data-ttu-id="cf130-120">Przejście skali lub wstrzymać działanie, system najpierw Kasuje wszystkie zapytania przychodzące i wycofa następnie transakcji w celu zapewnienia spójnego stanu.</span><span class="sxs-lookup"><span data-stu-id="cf130-120">When you undergo a scale or pause operation, the system first kills all incoming queries and then rolls back transactions to ensure a consistent state.</span></span> <span data-ttu-id="cf130-121">Dla operacji skalowania skalowanie będzie miało miejsce tylko po zakończeniu tego transakcyjne wycofywania.</span><span class="sxs-lookup"><span data-stu-id="cf130-121">For scale operations, scaling will only occur once this transactional rollback has completed.</span></span> <span data-ttu-id="cf130-122">Dla operacji skalowania w górę przepisy systemu nadmiarowe żądaną liczbę węzły obliczeniowe, a następnie rozpoczyna podłączenie węzłów obliczeniowych do warstwy magazynu.</span><span class="sxs-lookup"><span data-stu-id="cf130-122">For a scale-up operation, the system provisions the extra desired number of compute nodes, and then begins reattaching the compute nodes to the storage layer.</span></span> <span data-ttu-id="cf130-123">Dla operacji dół niepotrzebnych węzły są wydawane i pozostałe węzły obliczeniowe ponownie podłączyć się do odpowiedniej liczby dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="cf130-123">For a scale-down operation, the unneeded nodes are released and the remaining compute nodes reattach themselves to the appropriate number of distributions.</span></span> <span data-ttu-id="cf130-124">Dla operacji Wstrzymaj obliczeniowe wszystkie węzły są wydawane i systemu zostaną poddane różnych operacji na metadanych pozostawić końcowego systemu stabilna.</span><span class="sxs-lookup"><span data-stu-id="cf130-124">For a pause operation, all compute nodes are released and your system will undergo a variety of metadata operations to leave your final system in a stable state.</span></span>

| <span data-ttu-id="cf130-125">DWU</span><span class="sxs-lookup"><span data-stu-id="cf130-125">DWU</span></span>  | <span data-ttu-id="cf130-126">\#węzły obliczeniowe</span><span class="sxs-lookup"><span data-stu-id="cf130-126">\#of compute nodes</span></span> | <span data-ttu-id="cf130-127">\#dystrybucji na węzeł</span><span class="sxs-lookup"><span data-stu-id="cf130-127">\# of distributions per node</span></span> |
| ---- | ------------------ | ---------------------------- |
| <span data-ttu-id="cf130-128">100</span><span class="sxs-lookup"><span data-stu-id="cf130-128">100</span></span>  | <span data-ttu-id="cf130-129">1</span><span class="sxs-lookup"><span data-stu-id="cf130-129">1</span></span>                  | <span data-ttu-id="cf130-130">60</span><span class="sxs-lookup"><span data-stu-id="cf130-130">60</span></span>                           |
| <span data-ttu-id="cf130-131">200</span><span class="sxs-lookup"><span data-stu-id="cf130-131">200</span></span>  | <span data-ttu-id="cf130-132">2</span><span class="sxs-lookup"><span data-stu-id="cf130-132">2</span></span>                  | <span data-ttu-id="cf130-133">30</span><span class="sxs-lookup"><span data-stu-id="cf130-133">30</span></span>                           |
| <span data-ttu-id="cf130-134">300</span><span class="sxs-lookup"><span data-stu-id="cf130-134">300</span></span>  | <span data-ttu-id="cf130-135">3</span><span class="sxs-lookup"><span data-stu-id="cf130-135">3</span></span>                  | <span data-ttu-id="cf130-136">20</span><span class="sxs-lookup"><span data-stu-id="cf130-136">20</span></span>                           |
| <span data-ttu-id="cf130-137">400</span><span class="sxs-lookup"><span data-stu-id="cf130-137">400</span></span>  | <span data-ttu-id="cf130-138">4</span><span class="sxs-lookup"><span data-stu-id="cf130-138">4</span></span>                  | <span data-ttu-id="cf130-139">15</span><span class="sxs-lookup"><span data-stu-id="cf130-139">15</span></span>                           |
| <span data-ttu-id="cf130-140">500</span><span class="sxs-lookup"><span data-stu-id="cf130-140">500</span></span>  | <span data-ttu-id="cf130-141">5</span><span class="sxs-lookup"><span data-stu-id="cf130-141">5</span></span>                  | <span data-ttu-id="cf130-142">12</span><span class="sxs-lookup"><span data-stu-id="cf130-142">12</span></span>                           |
| <span data-ttu-id="cf130-143">600</span><span class="sxs-lookup"><span data-stu-id="cf130-143">600</span></span>  | <span data-ttu-id="cf130-144">6</span><span class="sxs-lookup"><span data-stu-id="cf130-144">6</span></span>                  | <span data-ttu-id="cf130-145">10</span><span class="sxs-lookup"><span data-stu-id="cf130-145">10</span></span>                           |
| <span data-ttu-id="cf130-146">1000</span><span class="sxs-lookup"><span data-stu-id="cf130-146">1000</span></span> | <span data-ttu-id="cf130-147">10</span><span class="sxs-lookup"><span data-stu-id="cf130-147">10</span></span>                 | <span data-ttu-id="cf130-148">6</span><span class="sxs-lookup"><span data-stu-id="cf130-148">6</span></span>                            |
| <span data-ttu-id="cf130-149">1200</span><span class="sxs-lookup"><span data-stu-id="cf130-149">1200</span></span> | <span data-ttu-id="cf130-150">12</span><span class="sxs-lookup"><span data-stu-id="cf130-150">12</span></span>                 | <span data-ttu-id="cf130-151">5</span><span class="sxs-lookup"><span data-stu-id="cf130-151">5</span></span>                            |
| <span data-ttu-id="cf130-152">1500</span><span class="sxs-lookup"><span data-stu-id="cf130-152">1500</span></span> | <span data-ttu-id="cf130-153">15</span><span class="sxs-lookup"><span data-stu-id="cf130-153">15</span></span>                 | <span data-ttu-id="cf130-154">4</span><span class="sxs-lookup"><span data-stu-id="cf130-154">4</span></span>                            |
| <span data-ttu-id="cf130-155">2000</span><span class="sxs-lookup"><span data-stu-id="cf130-155">2000</span></span> | <span data-ttu-id="cf130-156">20</span><span class="sxs-lookup"><span data-stu-id="cf130-156">20</span></span>                 | <span data-ttu-id="cf130-157">3</span><span class="sxs-lookup"><span data-stu-id="cf130-157">3</span></span>                            |
| <span data-ttu-id="cf130-158">3000</span><span class="sxs-lookup"><span data-stu-id="cf130-158">3000</span></span> | <span data-ttu-id="cf130-159">30</span><span class="sxs-lookup"><span data-stu-id="cf130-159">30</span></span>                 | <span data-ttu-id="cf130-160">2</span><span class="sxs-lookup"><span data-stu-id="cf130-160">2</span></span>                            |
| <span data-ttu-id="cf130-161">6000</span><span class="sxs-lookup"><span data-stu-id="cf130-161">6000</span></span> | <span data-ttu-id="cf130-162">60</span><span class="sxs-lookup"><span data-stu-id="cf130-162">60</span></span>                 | <span data-ttu-id="cf130-163">1</span><span class="sxs-lookup"><span data-stu-id="cf130-163">1</span></span>                            |

<span data-ttu-id="cf130-164">Trzy podstawowe funkcje zarządzania obliczeniowe są:</span><span class="sxs-lookup"><span data-stu-id="cf130-164">The three primary functions for managing compute are:</span></span>

1. <span data-ttu-id="cf130-165">Wstrzymaj</span><span class="sxs-lookup"><span data-stu-id="cf130-165">Pause</span></span>
2. <span data-ttu-id="cf130-166">Resume</span><span class="sxs-lookup"><span data-stu-id="cf130-166">Resume</span></span>
3. <span data-ttu-id="cf130-167">Skalowanie</span><span class="sxs-lookup"><span data-stu-id="cf130-167">Scale</span></span>

<span data-ttu-id="cf130-168">Każda z tych operacji może potrwać kilka minut.</span><span class="sxs-lookup"><span data-stu-id="cf130-168">Each of these operations may take several minutes to complete.</span></span> <span data-ttu-id="cf130-169">Jeśli jesteś skalowanie/wstrzymywanie/wznawianie automatycznie, można wdrożyć logikę, aby upewnić się, czy niektóre operacje zostały zakończone przed kontynuowaniem inną akcję.</span><span class="sxs-lookup"><span data-stu-id="cf130-169">If you are scaling/pausing/resuming automatically, you may want to implement logic to ensure that certain operations have been completed before proceeding with another action.</span></span> 

<span data-ttu-id="cf130-170">Sprawdzanie stanu bazy danych za pośrednictwem różnych punktów końcowych pozwoli prawidłowo zaimplementować automatyzacji takich operacji.</span><span class="sxs-lookup"><span data-stu-id="cf130-170">Checking the database state through various endpoints will allow you to correctly implement automation of such operations.</span></span> <span data-ttu-id="cf130-171">Portalu zapewni powiadomienie po zakończeniu operacji i bazy danych bieżący stan, ale nie jest możliwe programowe sprawdzania stanu.</span><span class="sxs-lookup"><span data-stu-id="cf130-171">The portal will provide notification upon completion of an operation and the databases current state but does not allow for programmatic checking of state.</span></span> 

>  [!NOTE]
>
>  <span data-ttu-id="cf130-172">Funkcja zarządzania nie istnieje we wszystkich punktów końcowych obliczeń.</span><span class="sxs-lookup"><span data-stu-id="cf130-172">Compute management functionality does not exist across all endpoints.</span></span>
>
>  

|              | <span data-ttu-id="cf130-173">Wstrzymanie/wznowienie</span><span class="sxs-lookup"><span data-stu-id="cf130-173">Pause/Resume</span></span> | <span data-ttu-id="cf130-174">Skalowanie</span><span class="sxs-lookup"><span data-stu-id="cf130-174">Scale</span></span> | <span data-ttu-id="cf130-175">Sprawdź stan bazy danych</span><span class="sxs-lookup"><span data-stu-id="cf130-175">Check database state</span></span> |
| ------------ | ------------ | ----- | -------------------- |
| <span data-ttu-id="cf130-176">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="cf130-176">Azure portal</span></span> | <span data-ttu-id="cf130-177">Tak</span><span class="sxs-lookup"><span data-stu-id="cf130-177">Yes</span></span>          | <span data-ttu-id="cf130-178">Tak</span><span class="sxs-lookup"><span data-stu-id="cf130-178">Yes</span></span>   | <span data-ttu-id="cf130-179">**Nie**</span><span class="sxs-lookup"><span data-stu-id="cf130-179">**No**</span></span>               |
| <span data-ttu-id="cf130-180">PowerShell</span><span class="sxs-lookup"><span data-stu-id="cf130-180">PowerShell</span></span>   | <span data-ttu-id="cf130-181">Tak</span><span class="sxs-lookup"><span data-stu-id="cf130-181">Yes</span></span>          | <span data-ttu-id="cf130-182">Tak</span><span class="sxs-lookup"><span data-stu-id="cf130-182">Yes</span></span>   | <span data-ttu-id="cf130-183">Tak</span><span class="sxs-lookup"><span data-stu-id="cf130-183">Yes</span></span>                  |
| <span data-ttu-id="cf130-184">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="cf130-184">REST API</span></span>     | <span data-ttu-id="cf130-185">Tak</span><span class="sxs-lookup"><span data-stu-id="cf130-185">Yes</span></span>          | <span data-ttu-id="cf130-186">Tak</span><span class="sxs-lookup"><span data-stu-id="cf130-186">Yes</span></span>   | <span data-ttu-id="cf130-187">Tak</span><span class="sxs-lookup"><span data-stu-id="cf130-187">Yes</span></span>                  |
| <span data-ttu-id="cf130-188">T-SQL</span><span class="sxs-lookup"><span data-stu-id="cf130-188">T-SQL</span></span>        | <span data-ttu-id="cf130-189">**Nie**</span><span class="sxs-lookup"><span data-stu-id="cf130-189">**No**</span></span>       | <span data-ttu-id="cf130-190">Tak</span><span class="sxs-lookup"><span data-stu-id="cf130-190">Yes</span></span>   | <span data-ttu-id="cf130-191">Tak</span><span class="sxs-lookup"><span data-stu-id="cf130-191">Yes</span></span>                  |



<a name="scale-compute-bk"></a>

## <a name="scale-compute"></a><span data-ttu-id="cf130-192">Skalowanie możliwości obliczeniowych</span><span class="sxs-lookup"><span data-stu-id="cf130-192">Scale compute</span></span>

<span data-ttu-id="cf130-193">Wydajność w usłudze SQL Data Warehouse jest mierzony w [jednostki (jednostek dwu) magazynu danych] [ data warehouse units (DWUs)] czyli abstracted miary zasoby obliczeniowe, takie jak procesor CPU, pamięci i we/wy przepustowości.</span><span class="sxs-lookup"><span data-stu-id="cf130-193">Performance in SQL Data Warehouse is measured in [data warehouse units (DWUs)][data warehouse units (DWUs)] which is an abstracted measure of compute resources such as CPU, memory, and I/O bandwidth.</span></span> <span data-ttu-id="cf130-194">Użytkownik, który chce skalowania wydajności ich systemu to zrobić za pomocą różnych środków, takich jak za pośrednictwem portalu, T-SQL i interfejsów API REST.</span><span class="sxs-lookup"><span data-stu-id="cf130-194">A user who wishes to scale their system's performance can do so through various means, such as through the portal, T-SQL, and REST APIs.</span></span> 

### <a name="how-do-i-scale-compute"></a><span data-ttu-id="cf130-195">Jak skalować obliczeń?</span><span class="sxs-lookup"><span data-stu-id="cf130-195">How do I scale compute?</span></span>
<span data-ttu-id="cf130-196">Obliczeń zasilania odbywa się SQL Data Warehouse, zmieniając ustawienie wartości DWU.</span><span class="sxs-lookup"><span data-stu-id="cf130-196">Compute power is managed for you SQL Data Warehouse by changing the DWU setting.</span></span> <span data-ttu-id="cf130-197">Zwiększa wydajność [liniowo] [ linearly] jak dodać więcej DWU dla niektórych operacji.</span><span class="sxs-lookup"><span data-stu-id="cf130-197">Performance increases [linearly][linearly] as you add more DWU for certain operations.</span></span>  <span data-ttu-id="cf130-198">Firma Microsoft oferuje ofert DWU, zapewniający, że gdy system skalować w górę lub w dół znacznie zmienić wydajność.</span><span class="sxs-lookup"><span data-stu-id="cf130-198">We offer DWU offerings that ensure that your performance will change noticeably when you scale your system up or down.</span></span> 

<span data-ttu-id="cf130-199">Aby dostosować liczbę jednostek dwu, można użyć dowolnej z tych poszczególnych metod.</span><span class="sxs-lookup"><span data-stu-id="cf130-199">To adjust DWUs, you can use any of these individual methods.</span></span>

* <span data-ttu-id="cf130-200">[Skala obliczeniowe zasilania z portalu Azure][Scale compute power with Azure portal]</span><span class="sxs-lookup"><span data-stu-id="cf130-200">[Scale compute power with Azure portal][Scale compute power with Azure portal]</span></span>
* <span data-ttu-id="cf130-201">[Skala obliczeniowe zasilania przy użyciu programu PowerShell][Scale compute power with PowerShell]</span><span class="sxs-lookup"><span data-stu-id="cf130-201">[Scale compute power with PowerShell][Scale compute power with PowerShell]</span></span>
* <span data-ttu-id="cf130-202">[Moc obliczeniową skali z interfejsów API REST][Scale compute power with REST APIs]</span><span class="sxs-lookup"><span data-stu-id="cf130-202">[Scale compute power with REST APIs][Scale compute power with REST APIs]</span></span>
* <span data-ttu-id="cf130-203">[Skala obliczeniowe zasilania przy użyciu języka TSQL][Scale compute power with TSQL]</span><span class="sxs-lookup"><span data-stu-id="cf130-203">[Scale compute power with TSQL][Scale compute power with TSQL]</span></span>

### <a name="how-many-dwus-should-i-use"></a><span data-ttu-id="cf130-204">Liczbę jednostek dwu należy używać?</span><span class="sxs-lookup"><span data-stu-id="cf130-204">How many DWUs should I use?</span></span>

<span data-ttu-id="cf130-205">Aby przekonać się, jaka jest idealna wartość DWU, skaluj w górę i w dół oraz uruchom kilka zapytań po załadowaniu danych.</span><span class="sxs-lookup"><span data-stu-id="cf130-205">To understand what your ideal DWU value is, try scaling up and down, and running a few queries after loading your data.</span></span> <span data-ttu-id="cf130-206">Ponieważ skalowanie odbywa się szybko, możesz wypróbować różne poziomy wydajności w ciągu godziny lub mniej.</span><span class="sxs-lookup"><span data-stu-id="cf130-206">Since scaling is quick, you can try various performance levels in an hour or less.</span></span> 

> [!Note] 
> <span data-ttu-id="cf130-207">Usługa SQL Data Warehouse zaprojektowano w celu przetwarzania dużych ilości danych.</span><span class="sxs-lookup"><span data-stu-id="cf130-207">SQL Data Warehouse is designed to process large amounts of data.</span></span> <span data-ttu-id="cf130-208">Aby wyświetlić jego wartość true, możliwości skalowania, zwłaszcza na większą liczbę jednostek dwu, chcesz użyć dużych zestawów danych, które zbliża się lub przekracza 1 TB.</span><span class="sxs-lookup"><span data-stu-id="cf130-208">To see its true capabilities for scaling, especially at larger DWUs, you want to use a large data set which approaches or exceeds 1 TB.</span></span>

<span data-ttu-id="cf130-209">Zalecenia dotyczące znajdowania wartość DWU najlepsze dla obciążenia:</span><span class="sxs-lookup"><span data-stu-id="cf130-209">Recommendations for finding the best DWU for your workload:</span></span>

1. <span data-ttu-id="cf130-210">Dla magazynu danych na programowanie rozpocząć wybierając mniejszą wydajnością DWU.</span><span class="sxs-lookup"><span data-stu-id="cf130-210">For a data warehouse in development, begin by selecting a smaller DWU performance level.</span></span>  <span data-ttu-id="cf130-211">Dobry punkt wyjścia jest DW400 lub DW200.</span><span class="sxs-lookup"><span data-stu-id="cf130-211">A good starting point is DW400 or DW200.</span></span>
2. <span data-ttu-id="cf130-212">Monitorowanie wydajności aplikacji, obserwowania liczby jednostek dwu wybrane w porównaniu do wydajności, które należy obserwować.</span><span class="sxs-lookup"><span data-stu-id="cf130-212">Monitor your application performance, observing the number of DWUs selected compared to the performance you observe.</span></span>
3. <span data-ttu-id="cf130-213">Określ, ile szybciej lub wolniej wydajność powinna być można osiągnąć poziom optymalną wydajność do wymagań przejmując skali liniowej.</span><span class="sxs-lookup"><span data-stu-id="cf130-213">Determine how much faster or slower performance should be for you to reach the optimum performance level for your requirements by assuming linear scale.</span></span>
4. <span data-ttu-id="cf130-214">Zwiększanie lub zmniejszanie liczby jednostek dwu proporcjonalnie do jak znacznie szybciej lub wolniej ma obciążenia do wykonania.</span><span class="sxs-lookup"><span data-stu-id="cf130-214">Increase or decrease the number of DWUs in proportion to how much faster or slower you want your workload to perform.</span></span> 
5. <span data-ttu-id="cf130-215">Kontynuuj, wprowadzić zmiany, aż do uzyskania optymalnej wydajności poziom dla potrzeb biznesowych.</span><span class="sxs-lookup"><span data-stu-id="cf130-215">Continue making adjustments until you reach an optimum performance level for your business requirements.</span></span>

> [!NOTE]
>
> <span data-ttu-id="cf130-216">Wydajność zapytań tylko zwiększa się wraz z paralelizacja więcej jeśli pracy może zostać podzielony między węzły obliczeń.</span><span class="sxs-lookup"><span data-stu-id="cf130-216">Query performance only increases with more parallelization if the work can be split between compute nodes.</span></span> <span data-ttu-id="cf130-217">Jeśli okaże się, że skalowanie nie zmienia się na wydajność, można znaleźć na naszych dostrajanie artykuły, aby sprawdzić, czy dane jest nierównomiernie dystrybuowane lub jeśli udostępniono dużą ilość ruchu danych wydajności.</span><span class="sxs-lookup"><span data-stu-id="cf130-217">If you find that scaling is not changing your performance, please check out our performance tuning articles to check whether your data is unevenly distributed or if you are introducing a large amount of data movement.</span></span> 

### <a name="when-should-i-scale-dwus"></a><span data-ttu-id="cf130-218">Kiedy skalować liczbę jednostek dwu?</span><span class="sxs-lookup"><span data-stu-id="cf130-218">When should I scale DWUs?</span></span>
<span data-ttu-id="cf130-219">Skalowanie jednostek dwu powoduje zmianę następujących ważne scenariusze:</span><span class="sxs-lookup"><span data-stu-id="cf130-219">Scaling DWUs alters the following important scenarios:</span></span>

1. <span data-ttu-id="cf130-220">Liniowo Zmiana wydajności systemu pod kątem skanowania, agregacji i CTAS — instrukcje</span><span class="sxs-lookup"><span data-stu-id="cf130-220">Linearly changing performance of the system for scans, aggregations, and CTAS statements</span></span>
2. <span data-ttu-id="cf130-221">Zwiększenie liczby czytelników i zapisywania podczas ładowania przy użyciu programu PolyBase</span><span class="sxs-lookup"><span data-stu-id="cf130-221">Increasing the number of readers and writers when loading with PolyBase</span></span>
3. <span data-ttu-id="cf130-222">Maksymalna liczba równoczesnych zapytań i gniazda współbieżności</span><span class="sxs-lookup"><span data-stu-id="cf130-222">Maximum number of concurrent queries and concurrency slots</span></span>

<span data-ttu-id="cf130-223">Zalecenia dotyczące Kiedy skalować liczbę jednostek dwu:</span><span class="sxs-lookup"><span data-stu-id="cf130-223">Recommendations for when to scale DWUs:</span></span>

1. <span data-ttu-id="cf130-224">Przed wykonaniem operacji ładowania i przekształcania dużej ilości danych, skalowanie w górę liczbę jednostek dwu tak, aby szybciej Twoje dane są dostępne.</span><span class="sxs-lookup"><span data-stu-id="cf130-224">Before you perform a heavy data loading or transformation operation, scale up DWUs so that your data is available more quickly.</span></span>
2. <span data-ttu-id="cf130-225">W godzinach szczytu skalowanie w celu uwzględnienia większej liczby równoczesnych zapytań.</span><span class="sxs-lookup"><span data-stu-id="cf130-225">During peak business hours, scale to accommodate larger numbers of concurrent queries.</span></span> 

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a><span data-ttu-id="cf130-226">Wstrzymaj obliczeń</span><span class="sxs-lookup"><span data-stu-id="cf130-226">Pause compute</span></span>
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

<span data-ttu-id="cf130-227">Aby wstrzymać bazy danych, użyj jednej z tych poszczególnych metod.</span><span class="sxs-lookup"><span data-stu-id="cf130-227">To pause a database, use any of these individual methods.</span></span>

* <span data-ttu-id="cf130-228">[Wstrzymaj obliczeń z portalu Azure][Pause compute with Azure portal]</span><span class="sxs-lookup"><span data-stu-id="cf130-228">[Pause compute with Azure portal][Pause compute with Azure portal]</span></span>
* <span data-ttu-id="cf130-229">[Wstrzymaj obliczeń przy użyciu programu PowerShell][Pause compute with PowerShell]</span><span class="sxs-lookup"><span data-stu-id="cf130-229">[Pause compute with PowerShell][Pause compute with PowerShell]</span></span>
* <span data-ttu-id="cf130-230">[Wstrzymaj obliczeń z interfejsów API REST][Pause compute with REST APIs]</span><span class="sxs-lookup"><span data-stu-id="cf130-230">[Pause compute with REST APIs][Pause compute with REST APIs]</span></span>

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a><span data-ttu-id="cf130-231">Wznów obliczeń</span><span class="sxs-lookup"><span data-stu-id="cf130-231">Resume compute</span></span>
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

<span data-ttu-id="cf130-232">Aby wznowić działanie bazy danych, użyj jednej z tych poszczególnych metod.</span><span class="sxs-lookup"><span data-stu-id="cf130-232">To resume a database, use any of these individual methods.</span></span>

* <span data-ttu-id="cf130-233">[Wznów obliczeń z portalu Azure][Resume compute with Azure portal]</span><span class="sxs-lookup"><span data-stu-id="cf130-233">[Resume compute with Azure portal][Resume compute with Azure portal]</span></span>
* <span data-ttu-id="cf130-234">[Wznów obliczeń przy użyciu programu PowerShell][Resume compute with PowerShell]</span><span class="sxs-lookup"><span data-stu-id="cf130-234">[Resume compute with PowerShell][Resume compute with PowerShell]</span></span>
* <span data-ttu-id="cf130-235">[Wznów obliczeń z interfejsów API REST][Resume compute with REST APIs]</span><span class="sxs-lookup"><span data-stu-id="cf130-235">[Resume compute with REST APIs][Resume compute with REST APIs]</span></span>

<a name="check-compute-bk"></a>

## <a name="check-database-state"></a><span data-ttu-id="cf130-236">Sprawdź stan bazy danych</span><span class="sxs-lookup"><span data-stu-id="cf130-236">Check database state</span></span> 

<span data-ttu-id="cf130-237">Aby wznowić działanie bazy danych, użyj jednej z tych poszczególnych metod.</span><span class="sxs-lookup"><span data-stu-id="cf130-237">To resume a database, use any of these individual methods.</span></span>

- <span data-ttu-id="cf130-238">[Sprawdź stan bazy danych z T-SQL][Check database state with T-SQL]</span><span class="sxs-lookup"><span data-stu-id="cf130-238">[Check database state with T-SQL][Check database state with T-SQL]</span></span>
- <span data-ttu-id="cf130-239">[Sprawdź stan bazy danych przy użyciu programu PowerShell][Check database state with PowerShell]</span><span class="sxs-lookup"><span data-stu-id="cf130-239">[Check database state with PowerShell][Check database state with PowerShell]</span></span>
- <span data-ttu-id="cf130-240">[Sprawdź stan bazy danych z interfejsów API REST][Check database state with REST APIs]</span><span class="sxs-lookup"><span data-stu-id="cf130-240">[Check database state with REST APIs][Check database state with REST APIs]</span></span>

## <a name="permissions"></a><span data-ttu-id="cf130-241">Uprawnienia</span><span class="sxs-lookup"><span data-stu-id="cf130-241">Permissions</span></span>

<span data-ttu-id="cf130-242">Skalowanie bazy danych musi mieć uprawnienia opisanego w [ALTER DATABASE][ALTER DATABASE].</span><span class="sxs-lookup"><span data-stu-id="cf130-242">Scaling the database requires the permissions described in [ALTER DATABASE][ALTER DATABASE].</span></span>  <span data-ttu-id="cf130-243">Wstrzymywanie i wznawianie wymagają [Współautor bazy danych SQL] [ SQL DB Contributor] uprawnienia, w szczególności Microsoft.Sql/servers/databases/action.</span><span class="sxs-lookup"><span data-stu-id="cf130-243">Pause and Resume require the [SQL DB Contributor][SQL DB Contributor] permission, specifically Microsoft.Sql/servers/databases/action.</span></span>

<a name="next-steps-bk"></a>

## <a name="next-steps"></a><span data-ttu-id="cf130-244">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="cf130-244">Next steps</span></span>
<span data-ttu-id="cf130-245">Zobacz następujące artykuły, aby ułatwić zrozumienie pojęcia niektóre dodatkowe wydajności:</span><span class="sxs-lookup"><span data-stu-id="cf130-245">Refer to the following articles to help you understand some additional key performance concepts:</span></span>

* <span data-ttu-id="cf130-246">[Zarządzanie obciążenia i współbieżność][Workload and concurrency management]</span><span class="sxs-lookup"><span data-stu-id="cf130-246">[Workload and concurrency management][Workload and concurrency management]</span></span>
* <span data-ttu-id="cf130-247">[Omówienie projektowania tabeli][Table design overview]</span><span class="sxs-lookup"><span data-stu-id="cf130-247">[Table design overview][Table design overview]</span></span>
* <span data-ttu-id="cf130-248">[Dystrybucja tabeli][Table distribution]</span><span class="sxs-lookup"><span data-stu-id="cf130-248">[Table distribution][Table distribution]</span></span>
* <span data-ttu-id="cf130-249">[Indeksowanie tabeli][Table indexing]</span><span class="sxs-lookup"><span data-stu-id="cf130-249">[Table indexing][Table indexing]</span></span>
* <span data-ttu-id="cf130-250">[Partycjonowanie tabel][Table partitioning]</span><span class="sxs-lookup"><span data-stu-id="cf130-250">[Table partitioning][Table partitioning]</span></span>
* <span data-ttu-id="cf130-251">[Statystyk tabeli][Table statistics]</span><span class="sxs-lookup"><span data-stu-id="cf130-251">[Table statistics][Table statistics]</span></span>
* <span data-ttu-id="cf130-252">[Najlepsze praktyki][Best practices]</span><span class="sxs-lookup"><span data-stu-id="cf130-252">[Best practices][Best practices]</span></span>

<!--Image reference-->

<!--Article references-->
[data warehouse units (DWUs)]: ./sql-data-warehouse-overview-what-is.md#predictable-and-scalable-performance-with-data-warehouse-units
[billed]: https://azure.microsoft.com/en-us/pricing/details/sql-data-warehouse/
[linearly]: ./sql-data-warehouse-overview-what-is.md#predictable-and-scalable-performance-with-data-warehouse-units
[Scale compute power with Azure portal]: ./sql-data-warehouse-manage-compute-portal.md#scale-compute-power
[Scale compute power with PowerShell]: ./sql-data-warehouse-manage-compute-powershell.md#scale-compute-bk
[Scale compute power with REST APIs]: ./sql-data-warehouse-manage-compute-rest-api.md#scale-compute-bk
[Scale compute power with TSQL]: ./sql-data-warehouse-manage-compute-tsql.md#scale-compute-bk

[capacity limits]: ./sql-data-warehouse-service-capacity-limits.md

[Pause compute with Azure portal]:  ./sql-data-warehouse-manage-compute-portal.md#pause-compute-bk
[Pause compute with PowerShell]: ./sql-data-warehouse-manage-compute-powershell.md#pause-compute-bk
[Pause compute with REST APIs]: ./sql-data-warehouse-manage-compute-rest-api.md#pause-compute-bk

[Resume compute with Azure portal]:  ./sql-data-warehouse-manage-compute-portal.md#resume-compute-bk
[Resume compute with PowerShell]: ./sql-data-warehouse-manage-compute-powershell.md#resume-compute-bk
[Resume compute with REST APIs]: ./sql-data-warehouse-manage-compute-rest-api.md#resume-compute-bk

[Check database state with T-SQL]: ./sql-data-warehouse-manage-compute-tsql.md#check-database-state-and-operation-progress
[Check database state with PowerShell]: ./sql-data-warehouse-manage-compute-powershell.md#check-database-state
[Check database state with REST APIs]: ./sql-data-warehouse-manage-compute-rest-api.md#check-database-state

[Workload and concurrency management]: ./sql-data-warehouse-develop-concurrency.md
[Table design overview]: ./sql-data-warehouse-tables-overview.md
[Table distribution]: ./sql-data-warehouse-tables-distribute.md
[Table indexing]: ./sql-data-warehouse-tables-index.md
[Table partitioning]: ./sql-data-warehouse-tables-partition.md
[Table statistics]: ./sql-data-warehouse-tables-statistics.md
[Best practices]: ./sql-data-warehouse-best-practices.md
[development overview]: ./sql-data-warehouse-overview-develop.md

[SQL DB Contributor]: ../active-directory/role-based-access-built-in-roles.md#sql-db-contributor

<!--MSDN references-->
[ALTER DATABASE]: https://msdn.microsoft.com/library/mt204042.aspx

<!--Other Web references-->
[Azure portal]: http://portal.azure.com/
