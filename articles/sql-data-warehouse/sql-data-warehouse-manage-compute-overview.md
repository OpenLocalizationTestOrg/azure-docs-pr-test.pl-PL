---
title: "aaaManage obliczeniowe zasilania w usłudze Azure SQL Data Warehouse (omówienie) | Dokumentacja firmy Microsoft"
description: "Wydajność skalowania możliwości w usłudze Azure SQL Data Warehouse. Skalowanie w poziomie przez dostosowanie wartości dwu lub wstrzymywać i wznawiać koszty toosave zasobów obliczeniowych."
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
ms.openlocfilehash: 1ffbe8d694ac181eaeb6f585a2cee87a570ed7d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-overview"></a><span data-ttu-id="3c8a8-104">Zarządzanie moc obliczeniową w usłudze Azure SQL Data Warehouse (omówienie)</span><span class="sxs-lookup"><span data-stu-id="3c8a8-104">Manage compute power in Azure SQL Data Warehouse (Overview)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3c8a8-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="3c8a8-105">Overview</span></span>](sql-data-warehouse-manage-compute-overview.md)
> * [<span data-ttu-id="3c8a8-106">Portal</span><span class="sxs-lookup"><span data-stu-id="3c8a8-106">Portal</span></span>](sql-data-warehouse-manage-compute-portal.md)
> * [<span data-ttu-id="3c8a8-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3c8a8-107">PowerShell</span></span>](sql-data-warehouse-manage-compute-powershell.md)
> * [<span data-ttu-id="3c8a8-108">REST</span><span class="sxs-lookup"><span data-stu-id="3c8a8-108">REST</span></span>](sql-data-warehouse-manage-compute-rest-api.md)
> * [<span data-ttu-id="3c8a8-109">TSQL</span><span class="sxs-lookup"><span data-stu-id="3c8a8-109">TSQL</span></span>](sql-data-warehouse-manage-compute-tsql.md)
>
>

<span data-ttu-id="3c8a8-110">Architektura Hello usługi SQL Data Warehouse oddziela magazynu i zasobów obliczeniowych, dzięki czemu każdy tooscale niezależnie.</span><span class="sxs-lookup"><span data-stu-id="3c8a8-110">hello architecture of SQL Data Warehouse separates storage and compute, allowing each tooscale independently.</span></span> <span data-ttu-id="3c8a8-111">W związku z tym obliczeń może być skalowana toomeet wymagań dotyczących wydajności niezależne od hello ilości danych.</span><span class="sxs-lookup"><span data-stu-id="3c8a8-111">As a result, compute can be scaled toomeet performance demands independent of hello amount of data.</span></span> <span data-ttu-id="3c8a8-112">Fizyczne konsekwencją tej architektury jest to, że [rozliczeń] [ billed] dla zasobów obliczeniowych i magazynu jest oddzielona.</span><span class="sxs-lookup"><span data-stu-id="3c8a8-112">A natural consequence of this architecture is that [billing][billed] for compute and storage is separate.</span></span> 

<span data-ttu-id="3c8a8-113">Ten przegląd zawiera opis sposobu skalowania współpracuje z magazynu danych SQL i jak tooutilize Witaj, wstrzymywanie, wznawianie i możliwości skalowania usługi SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="3c8a8-113">This overview describes how scale out works with SQL Data Warehouse and how tooutilize hello pause, resume, and scale capabilities of SQL Data Warehouse.</span></span> <span data-ttu-id="3c8a8-114">Zapoznaj się hello [jednostki (jednostek dwu) magazynu danych] [ data warehouse units (DWUs)] toolearn strony jak jednostek dwu i wydajności są powiązane.</span><span class="sxs-lookup"><span data-stu-id="3c8a8-114">Consult hello [data warehouse units (DWUs)][data warehouse units (DWUs)] page toolearn how DWUs and performance are related.</span></span> 

## <a name="how-compute-management-operations-work-in-sql-data-warehouse"></a><span data-ttu-id="3c8a8-115">Jak obliczeń operacje zarządzania działają w usłudze SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="3c8a8-115">How compute management operations work in SQL Data Warehouse</span></span>
<span data-ttu-id="3c8a8-116">Architektura Hello magazynu danych SQL składa się z węzłem sterowania, węzły obliczeniowe i hello rozmieszczenie 60 dystrybucje warstwy magazynu.</span><span class="sxs-lookup"><span data-stu-id="3c8a8-116">hello architecture for SQL Data Warehouse consists of a control node, compute nodes, and hello storage layer spread across 60 distributions.</span></span> 

<span data-ttu-id="3c8a8-117">Podczas normalnej sesji aktywnych w usłudze SQL Data Warehouse węzła głównego systemu zarządza hello metadanych i zawiera Optymalizator zapytań rozproszonych hello.</span><span class="sxs-lookup"><span data-stu-id="3c8a8-117">During a normal active session in SQL Data Warehouse, your system's head node manages hello metadata and contains hello distributed query optimizer.</span></span> <span data-ttu-id="3c8a8-118">Poniżej tego węzła głównego są węzłów obliczeniowych i warstwą magazynu.</span><span class="sxs-lookup"><span data-stu-id="3c8a8-118">Beneath this head node are your compute nodes and your storage layer.</span></span> <span data-ttu-id="3c8a8-119">400 DWU system ma jednego węzła głównego, czterech węzłów obliczeniowych i hello magazynu, składającego się z 60 dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="3c8a8-119">For a DWU 400, your system has one head node, four compute nodes, and hello storage layer, consisting of 60 distributions.</span></span> 

<span data-ttu-id="3c8a8-120">Przejście skali lub wstrzymać działania systemu hello najpierw Kasuje wszystkie zapytania przychodzące i wycofa następnie tooensure transakcji spójne.</span><span class="sxs-lookup"><span data-stu-id="3c8a8-120">When you undergo a scale or pause operation, hello system first kills all incoming queries and then rolls back transactions tooensure a consistent state.</span></span> <span data-ttu-id="3c8a8-121">Dla operacji skalowania skalowanie będzie miało miejsce tylko po zakończeniu tego transakcyjne wycofywania.</span><span class="sxs-lookup"><span data-stu-id="3c8a8-121">For scale operations, scaling will only occur once this transactional rollback has completed.</span></span> <span data-ttu-id="3c8a8-122">Dla operacji skalowania w górę przepisy systemu hello hello bardzo odpowiednią liczbę węzłów obliczeniowych, a następnie rozpoczyna podłączenie warstwy magazynu toohello węzły obliczeniowe hello.</span><span class="sxs-lookup"><span data-stu-id="3c8a8-122">For a scale-up operation, hello system provisions hello extra desired number of compute nodes, and then begins reattaching hello compute nodes toohello storage layer.</span></span> <span data-ttu-id="3c8a8-123">Dla operacji dół hello niepotrzebnych węzły są wydawane, a pozostałe węzły obliczeniowe hello Przyłącz się ponownie toohello odpowiedniej liczby dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="3c8a8-123">For a scale-down operation, hello unneeded nodes are released and hello remaining compute nodes reattach themselves toohello appropriate number of distributions.</span></span> <span data-ttu-id="3c8a8-124">Dla operacji Wstrzymaj obliczeniowe wszystkie węzły są wydawane i systemu zostaną poddane różnych tooleave operacji metadanych systemu końcowego stabilna.</span><span class="sxs-lookup"><span data-stu-id="3c8a8-124">For a pause operation, all compute nodes are released and your system will undergo a variety of metadata operations tooleave your final system in a stable state.</span></span>

| <span data-ttu-id="3c8a8-125">DWU</span><span class="sxs-lookup"><span data-stu-id="3c8a8-125">DWU</span></span>  | <span data-ttu-id="3c8a8-126">\#węzły obliczeniowe</span><span class="sxs-lookup"><span data-stu-id="3c8a8-126">\#of compute nodes</span></span> | <span data-ttu-id="3c8a8-127">\#dystrybucji na węzeł</span><span class="sxs-lookup"><span data-stu-id="3c8a8-127">\# of distributions per node</span></span> |
| ---- | ------------------ | ---------------------------- |
| <span data-ttu-id="3c8a8-128">100</span><span class="sxs-lookup"><span data-stu-id="3c8a8-128">100</span></span>  | <span data-ttu-id="3c8a8-129">1</span><span class="sxs-lookup"><span data-stu-id="3c8a8-129">1</span></span>                  | <span data-ttu-id="3c8a8-130">60</span><span class="sxs-lookup"><span data-stu-id="3c8a8-130">60</span></span>                           |
| <span data-ttu-id="3c8a8-131">200</span><span class="sxs-lookup"><span data-stu-id="3c8a8-131">200</span></span>  | <span data-ttu-id="3c8a8-132">2</span><span class="sxs-lookup"><span data-stu-id="3c8a8-132">2</span></span>                  | <span data-ttu-id="3c8a8-133">30</span><span class="sxs-lookup"><span data-stu-id="3c8a8-133">30</span></span>                           |
| <span data-ttu-id="3c8a8-134">300</span><span class="sxs-lookup"><span data-stu-id="3c8a8-134">300</span></span>  | <span data-ttu-id="3c8a8-135">3</span><span class="sxs-lookup"><span data-stu-id="3c8a8-135">3</span></span>                  | <span data-ttu-id="3c8a8-136">20</span><span class="sxs-lookup"><span data-stu-id="3c8a8-136">20</span></span>                           |
| <span data-ttu-id="3c8a8-137">400</span><span class="sxs-lookup"><span data-stu-id="3c8a8-137">400</span></span>  | <span data-ttu-id="3c8a8-138">4</span><span class="sxs-lookup"><span data-stu-id="3c8a8-138">4</span></span>                  | <span data-ttu-id="3c8a8-139">15</span><span class="sxs-lookup"><span data-stu-id="3c8a8-139">15</span></span>                           |
| <span data-ttu-id="3c8a8-140">500</span><span class="sxs-lookup"><span data-stu-id="3c8a8-140">500</span></span>  | <span data-ttu-id="3c8a8-141">5</span><span class="sxs-lookup"><span data-stu-id="3c8a8-141">5</span></span>                  | <span data-ttu-id="3c8a8-142">12</span><span class="sxs-lookup"><span data-stu-id="3c8a8-142">12</span></span>                           |
| <span data-ttu-id="3c8a8-143">600</span><span class="sxs-lookup"><span data-stu-id="3c8a8-143">600</span></span>  | <span data-ttu-id="3c8a8-144">6</span><span class="sxs-lookup"><span data-stu-id="3c8a8-144">6</span></span>                  | <span data-ttu-id="3c8a8-145">10</span><span class="sxs-lookup"><span data-stu-id="3c8a8-145">10</span></span>                           |
| <span data-ttu-id="3c8a8-146">1000</span><span class="sxs-lookup"><span data-stu-id="3c8a8-146">1000</span></span> | <span data-ttu-id="3c8a8-147">10</span><span class="sxs-lookup"><span data-stu-id="3c8a8-147">10</span></span>                 | <span data-ttu-id="3c8a8-148">6</span><span class="sxs-lookup"><span data-stu-id="3c8a8-148">6</span></span>                            |
| <span data-ttu-id="3c8a8-149">1200</span><span class="sxs-lookup"><span data-stu-id="3c8a8-149">1200</span></span> | <span data-ttu-id="3c8a8-150">12</span><span class="sxs-lookup"><span data-stu-id="3c8a8-150">12</span></span>                 | <span data-ttu-id="3c8a8-151">5</span><span class="sxs-lookup"><span data-stu-id="3c8a8-151">5</span></span>                            |
| <span data-ttu-id="3c8a8-152">1500</span><span class="sxs-lookup"><span data-stu-id="3c8a8-152">1500</span></span> | <span data-ttu-id="3c8a8-153">15</span><span class="sxs-lookup"><span data-stu-id="3c8a8-153">15</span></span>                 | <span data-ttu-id="3c8a8-154">4</span><span class="sxs-lookup"><span data-stu-id="3c8a8-154">4</span></span>                            |
| <span data-ttu-id="3c8a8-155">2000</span><span class="sxs-lookup"><span data-stu-id="3c8a8-155">2000</span></span> | <span data-ttu-id="3c8a8-156">20</span><span class="sxs-lookup"><span data-stu-id="3c8a8-156">20</span></span>                 | <span data-ttu-id="3c8a8-157">3</span><span class="sxs-lookup"><span data-stu-id="3c8a8-157">3</span></span>                            |
| <span data-ttu-id="3c8a8-158">3000</span><span class="sxs-lookup"><span data-stu-id="3c8a8-158">3000</span></span> | <span data-ttu-id="3c8a8-159">30</span><span class="sxs-lookup"><span data-stu-id="3c8a8-159">30</span></span>                 | <span data-ttu-id="3c8a8-160">2</span><span class="sxs-lookup"><span data-stu-id="3c8a8-160">2</span></span>                            |
| <span data-ttu-id="3c8a8-161">6000</span><span class="sxs-lookup"><span data-stu-id="3c8a8-161">6000</span></span> | <span data-ttu-id="3c8a8-162">60</span><span class="sxs-lookup"><span data-stu-id="3c8a8-162">60</span></span>                 | <span data-ttu-id="3c8a8-163">1</span><span class="sxs-lookup"><span data-stu-id="3c8a8-163">1</span></span>                            |

<span data-ttu-id="3c8a8-164">Witaj trzy podstawowe funkcje zarządzania obliczeniowe są:</span><span class="sxs-lookup"><span data-stu-id="3c8a8-164">hello three primary functions for managing compute are:</span></span>

1. <span data-ttu-id="3c8a8-165">Wstrzymaj</span><span class="sxs-lookup"><span data-stu-id="3c8a8-165">Pause</span></span>
2. <span data-ttu-id="3c8a8-166">Resume</span><span class="sxs-lookup"><span data-stu-id="3c8a8-166">Resume</span></span>
3. <span data-ttu-id="3c8a8-167">Skalowanie</span><span class="sxs-lookup"><span data-stu-id="3c8a8-167">Scale</span></span>

<span data-ttu-id="3c8a8-168">Każda z tych operacji może potrwać kilka minut toocomplete.</span><span class="sxs-lookup"><span data-stu-id="3c8a8-168">Each of these operations may take several minutes toocomplete.</span></span> <span data-ttu-id="3c8a8-169">Jeśli jesteś skalowanie/wstrzymywanie/wznawianie automatycznie, może być tooimplement tooensure logiki to pewność, że operacje zostały zakończone przed kontynuowaniem innej akcji.</span><span class="sxs-lookup"><span data-stu-id="3c8a8-169">If you are scaling/pausing/resuming automatically, you may want tooimplement logic tooensure that certain operations have been completed before proceeding with another action.</span></span> 

<span data-ttu-id="3c8a8-170">Sprawdzanie stanu bazy danych hello za pośrednictwem różnych punktów końcowych pozwoli toocorrectly automatyzacji implementacji takich operacji.</span><span class="sxs-lookup"><span data-stu-id="3c8a8-170">Checking hello database state through various endpoints will allow you toocorrectly implement automation of such operations.</span></span> <span data-ttu-id="3c8a8-171">Hello portal zapewni powiadomienie po zakończeniu operacji i hello bazy danych bieżący stan, ale nie jest możliwe programowe sprawdzania stanu.</span><span class="sxs-lookup"><span data-stu-id="3c8a8-171">hello portal will provide notification upon completion of an operation and hello databases current state but does not allow for programmatic checking of state.</span></span> 

>  [!NOTE]
>
>  <span data-ttu-id="3c8a8-172">Funkcja zarządzania nie istnieje we wszystkich punktów końcowych obliczeń.</span><span class="sxs-lookup"><span data-stu-id="3c8a8-172">Compute management functionality does not exist across all endpoints.</span></span>
>
>  

|              | <span data-ttu-id="3c8a8-173">Wstrzymanie/wznowienie</span><span class="sxs-lookup"><span data-stu-id="3c8a8-173">Pause/Resume</span></span> | <span data-ttu-id="3c8a8-174">Skalowanie</span><span class="sxs-lookup"><span data-stu-id="3c8a8-174">Scale</span></span> | <span data-ttu-id="3c8a8-175">Sprawdź stan bazy danych</span><span class="sxs-lookup"><span data-stu-id="3c8a8-175">Check database state</span></span> |
| ------------ | ------------ | ----- | -------------------- |
| <span data-ttu-id="3c8a8-176">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="3c8a8-176">Azure portal</span></span> | <span data-ttu-id="3c8a8-177">Tak</span><span class="sxs-lookup"><span data-stu-id="3c8a8-177">Yes</span></span>          | <span data-ttu-id="3c8a8-178">Tak</span><span class="sxs-lookup"><span data-stu-id="3c8a8-178">Yes</span></span>   | <span data-ttu-id="3c8a8-179">**Nie**</span><span class="sxs-lookup"><span data-stu-id="3c8a8-179">**No**</span></span>               |
| <span data-ttu-id="3c8a8-180">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3c8a8-180">PowerShell</span></span>   | <span data-ttu-id="3c8a8-181">Tak</span><span class="sxs-lookup"><span data-stu-id="3c8a8-181">Yes</span></span>          | <span data-ttu-id="3c8a8-182">Tak</span><span class="sxs-lookup"><span data-stu-id="3c8a8-182">Yes</span></span>   | <span data-ttu-id="3c8a8-183">Tak</span><span class="sxs-lookup"><span data-stu-id="3c8a8-183">Yes</span></span>                  |
| <span data-ttu-id="3c8a8-184">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="3c8a8-184">REST API</span></span>     | <span data-ttu-id="3c8a8-185">Tak</span><span class="sxs-lookup"><span data-stu-id="3c8a8-185">Yes</span></span>          | <span data-ttu-id="3c8a8-186">Tak</span><span class="sxs-lookup"><span data-stu-id="3c8a8-186">Yes</span></span>   | <span data-ttu-id="3c8a8-187">Tak</span><span class="sxs-lookup"><span data-stu-id="3c8a8-187">Yes</span></span>                  |
| <span data-ttu-id="3c8a8-188">T-SQL</span><span class="sxs-lookup"><span data-stu-id="3c8a8-188">T-SQL</span></span>        | <span data-ttu-id="3c8a8-189">**Nie**</span><span class="sxs-lookup"><span data-stu-id="3c8a8-189">**No**</span></span>       | <span data-ttu-id="3c8a8-190">Tak</span><span class="sxs-lookup"><span data-stu-id="3c8a8-190">Yes</span></span>   | <span data-ttu-id="3c8a8-191">Tak</span><span class="sxs-lookup"><span data-stu-id="3c8a8-191">Yes</span></span>                  |



<a name="scale-compute-bk"></a>

## <a name="scale-compute"></a><span data-ttu-id="3c8a8-192">Skalowanie możliwości obliczeniowych</span><span class="sxs-lookup"><span data-stu-id="3c8a8-192">Scale compute</span></span>

<span data-ttu-id="3c8a8-193">Wydajność w usłudze SQL Data Warehouse jest mierzony w [jednostki (jednostek dwu) magazynu danych] [ data warehouse units (DWUs)] czyli abstracted miary zasoby obliczeniowe, takie jak procesor CPU, pamięci i we/wy przepustowości.</span><span class="sxs-lookup"><span data-stu-id="3c8a8-193">Performance in SQL Data Warehouse is measured in [data warehouse units (DWUs)][data warehouse units (DWUs)] which is an abstracted measure of compute resources such as CPU, memory, and I/O bandwidth.</span></span> <span data-ttu-id="3c8a8-194">Użytkownik, który chce tooscale wydajność ich systemu to zrobić za pośrednictwem różnych środków, takich jak za pośrednictwem portalu hello, T-SQL i interfejsów API REST.</span><span class="sxs-lookup"><span data-stu-id="3c8a8-194">A user who wishes tooscale their system's performance can do so through various means, such as through hello portal, T-SQL, and REST APIs.</span></span> 

### <a name="how-do-i-scale-compute"></a><span data-ttu-id="3c8a8-195">Jak skalować obliczeń?</span><span class="sxs-lookup"><span data-stu-id="3c8a8-195">How do I scale compute?</span></span>
<span data-ttu-id="3c8a8-196">Moc obliczeniową odbywa się SQL Data Warehouse, zmieniając ustawienie wartości DWU hello.</span><span class="sxs-lookup"><span data-stu-id="3c8a8-196">Compute power is managed for you SQL Data Warehouse by changing hello DWU setting.</span></span> <span data-ttu-id="3c8a8-197">Zwiększa wydajność [liniowo] [ linearly] jak dodać więcej DWU dla niektórych operacji.</span><span class="sxs-lookup"><span data-stu-id="3c8a8-197">Performance increases [linearly][linearly] as you add more DWU for certain operations.</span></span>  <span data-ttu-id="3c8a8-198">Firma Microsoft oferuje ofert DWU, zapewniający, że gdy system skalować w górę lub w dół znacznie zmienić wydajność.</span><span class="sxs-lookup"><span data-stu-id="3c8a8-198">We offer DWU offerings that ensure that your performance will change noticeably when you scale your system up or down.</span></span> 

<span data-ttu-id="3c8a8-199">tooadjust jednostek dwu służy jednej z tych poszczególnych metod.</span><span class="sxs-lookup"><span data-stu-id="3c8a8-199">tooadjust DWUs, you can use any of these individual methods.</span></span>

* <span data-ttu-id="3c8a8-200">[Skala obliczeniowe zasilania z portalu Azure][Scale compute power with Azure portal]</span><span class="sxs-lookup"><span data-stu-id="3c8a8-200">[Scale compute power with Azure portal][Scale compute power with Azure portal]</span></span>
* <span data-ttu-id="3c8a8-201">[Skala obliczeniowe zasilania przy użyciu programu PowerShell][Scale compute power with PowerShell]</span><span class="sxs-lookup"><span data-stu-id="3c8a8-201">[Scale compute power with PowerShell][Scale compute power with PowerShell]</span></span>
* <span data-ttu-id="3c8a8-202">[Moc obliczeniową skali z interfejsów API REST][Scale compute power with REST APIs]</span><span class="sxs-lookup"><span data-stu-id="3c8a8-202">[Scale compute power with REST APIs][Scale compute power with REST APIs]</span></span>
* <span data-ttu-id="3c8a8-203">[Skala obliczeniowe zasilania przy użyciu języka TSQL][Scale compute power with TSQL]</span><span class="sxs-lookup"><span data-stu-id="3c8a8-203">[Scale compute power with TSQL][Scale compute power with TSQL]</span></span>

### <a name="how-many-dwus-should-i-use"></a><span data-ttu-id="3c8a8-204">Liczbę jednostek dwu należy używać?</span><span class="sxs-lookup"><span data-stu-id="3c8a8-204">How many DWUs should I use?</span></span>

<span data-ttu-id="3c8a8-205">toounderstand jest jakie idealna wartość DWU, spróbuj skalowanie w górę i w dół oraz Uruchom kilka zapytań po załadowaniu danych.</span><span class="sxs-lookup"><span data-stu-id="3c8a8-205">toounderstand what your ideal DWU value is, try scaling up and down, and running a few queries after loading your data.</span></span> <span data-ttu-id="3c8a8-206">Ponieważ skalowanie odbywa się szybko, możesz wypróbować różne poziomy wydajności w ciągu godziny lub mniej.</span><span class="sxs-lookup"><span data-stu-id="3c8a8-206">Since scaling is quick, you can try various performance levels in an hour or less.</span></span> 

> [!Note] 
> <span data-ttu-id="3c8a8-207">Magazyn danych SQL jest zaprojektowana tooprocess dużych ilości danych.</span><span class="sxs-lookup"><span data-stu-id="3c8a8-207">SQL Data Warehouse is designed tooprocess large amounts of data.</span></span> <span data-ttu-id="3c8a8-208">toosee true możliwości skalowania, zwłaszcza na większą liczbę jednostek dwu, ma toouse dużych zestawów danych, które zbliża się lub przekracza 1 TB.</span><span class="sxs-lookup"><span data-stu-id="3c8a8-208">toosee its true capabilities for scaling, especially at larger DWUs, you want toouse a large data set which approaches or exceeds 1 TB.</span></span>

<span data-ttu-id="3c8a8-209">Zalecenia dotyczące znajdowania hello DWU najlepsze dla obciążenia:</span><span class="sxs-lookup"><span data-stu-id="3c8a8-209">Recommendations for finding hello best DWU for your workload:</span></span>

1. <span data-ttu-id="3c8a8-210">Dla magazynu danych na programowanie rozpocząć wybierając mniejszą wydajnością DWU.</span><span class="sxs-lookup"><span data-stu-id="3c8a8-210">For a data warehouse in development, begin by selecting a smaller DWU performance level.</span></span>  <span data-ttu-id="3c8a8-211">Dobry punkt wyjścia jest DW400 lub DW200.</span><span class="sxs-lookup"><span data-stu-id="3c8a8-211">A good starting point is DW400 or DW200.</span></span>
2. <span data-ttu-id="3c8a8-212">Monitorowanie wydajności aplikacji, obserwowania hello liczby jednostek dwu wybrany porównanych toohello wydajności, które należy obserwować.</span><span class="sxs-lookup"><span data-stu-id="3c8a8-212">Monitor your application performance, observing hello number of DWUs selected compared toohello performance you observe.</span></span>
3. <span data-ttu-id="3c8a8-213">Określ, ile szybciej lub wolniej wydajności powinny mieć możesz tooreach hello optymalny poziom wydajności dla wymagań przejmując skali liniowej.</span><span class="sxs-lookup"><span data-stu-id="3c8a8-213">Determine how much faster or slower performance should be for you tooreach hello optimum performance level for your requirements by assuming linear scale.</span></span>
4. <span data-ttu-id="3c8a8-214">Zwiększ lub Zmniejsz liczbę hello jednostek dwu w proporcji toohow znacznie szybciej lub wolniej ma tooperform Twojego obciążenia.</span><span class="sxs-lookup"><span data-stu-id="3c8a8-214">Increase or decrease hello number of DWUs in proportion toohow much faster or slower you want your workload tooperform.</span></span> 
5. <span data-ttu-id="3c8a8-215">Kontynuuj, wprowadzić zmiany, aż do uzyskania optymalnej wydajności poziom dla potrzeb biznesowych.</span><span class="sxs-lookup"><span data-stu-id="3c8a8-215">Continue making adjustments until you reach an optimum performance level for your business requirements.</span></span>

> [!NOTE]
>
> <span data-ttu-id="3c8a8-216">Wydajność zapytań tylko zwiększa się wraz z paralelizacja więcej jeśli hello pracy może zostać podzielony między węzły obliczeń.</span><span class="sxs-lookup"><span data-stu-id="3c8a8-216">Query performance only increases with more parallelization if hello work can be split between compute nodes.</span></span> <span data-ttu-id="3c8a8-217">Jeśli okaże się, że skalowanie nie zmienia się na wydajność, można znaleźć na naszych dostrajanie toocheck artykuły, czy dane jest nierównomiernie dystrybuowane lub jeśli udostępniono dużą ilość ruchu danych wydajności.</span><span class="sxs-lookup"><span data-stu-id="3c8a8-217">If you find that scaling is not changing your performance, please check out our performance tuning articles toocheck whether your data is unevenly distributed or if you are introducing a large amount of data movement.</span></span> 

### <a name="when-should-i-scale-dwus"></a><span data-ttu-id="3c8a8-218">Kiedy skalować liczbę jednostek dwu?</span><span class="sxs-lookup"><span data-stu-id="3c8a8-218">When should I scale DWUs?</span></span>
<span data-ttu-id="3c8a8-219">Skalowanie jednostek dwu zmienia powitania po ważne scenariusze:</span><span class="sxs-lookup"><span data-stu-id="3c8a8-219">Scaling DWUs alters hello following important scenarios:</span></span>

1. <span data-ttu-id="3c8a8-220">Liniowo Zmiana wydajności systemu hello skanowania, agregacji i CTAS — instrukcje</span><span class="sxs-lookup"><span data-stu-id="3c8a8-220">Linearly changing performance of hello system for scans, aggregations, and CTAS statements</span></span>
2. <span data-ttu-id="3c8a8-221">Zwiększenie liczby hello czytelników i zapisywania podczas ładowania przy użyciu programu PolyBase</span><span class="sxs-lookup"><span data-stu-id="3c8a8-221">Increasing hello number of readers and writers when loading with PolyBase</span></span>
3. <span data-ttu-id="3c8a8-222">Maksymalna liczba równoczesnych zapytań i gniazda współbieżności</span><span class="sxs-lookup"><span data-stu-id="3c8a8-222">Maximum number of concurrent queries and concurrency slots</span></span>

<span data-ttu-id="3c8a8-223">Zalecenia dotyczące kiedy tooscale jednostek dwu:</span><span class="sxs-lookup"><span data-stu-id="3c8a8-223">Recommendations for when tooscale DWUs:</span></span>

1. <span data-ttu-id="3c8a8-224">Przed wykonaniem operacji ładowania i przekształcania dużej ilości danych, skalowanie w górę liczbę jednostek dwu tak, aby szybciej Twoje dane są dostępne.</span><span class="sxs-lookup"><span data-stu-id="3c8a8-224">Before you perform a heavy data loading or transformation operation, scale up DWUs so that your data is available more quickly.</span></span>
2. <span data-ttu-id="3c8a8-225">W godzinach szczytu skalowanie tooaccommodate większej liczby równoczesnych zapytań.</span><span class="sxs-lookup"><span data-stu-id="3c8a8-225">During peak business hours, scale tooaccommodate larger numbers of concurrent queries.</span></span> 

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a><span data-ttu-id="3c8a8-226">Wstrzymaj obliczeń</span><span class="sxs-lookup"><span data-stu-id="3c8a8-226">Pause compute</span></span>
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

<span data-ttu-id="3c8a8-227">toopause bazy danych, użyj jednej z tych poszczególnych metod.</span><span class="sxs-lookup"><span data-stu-id="3c8a8-227">toopause a database, use any of these individual methods.</span></span>

* <span data-ttu-id="3c8a8-228">[Wstrzymaj obliczeń z portalu Azure][Pause compute with Azure portal]</span><span class="sxs-lookup"><span data-stu-id="3c8a8-228">[Pause compute with Azure portal][Pause compute with Azure portal]</span></span>
* <span data-ttu-id="3c8a8-229">[Wstrzymaj obliczeń przy użyciu programu PowerShell][Pause compute with PowerShell]</span><span class="sxs-lookup"><span data-stu-id="3c8a8-229">[Pause compute with PowerShell][Pause compute with PowerShell]</span></span>
* <span data-ttu-id="3c8a8-230">[Wstrzymaj obliczeń z interfejsów API REST][Pause compute with REST APIs]</span><span class="sxs-lookup"><span data-stu-id="3c8a8-230">[Pause compute with REST APIs][Pause compute with REST APIs]</span></span>

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a><span data-ttu-id="3c8a8-231">Wznów obliczeń</span><span class="sxs-lookup"><span data-stu-id="3c8a8-231">Resume compute</span></span>
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

<span data-ttu-id="3c8a8-232">tooresume bazy danych, użyj jednej z tych poszczególnych metod.</span><span class="sxs-lookup"><span data-stu-id="3c8a8-232">tooresume a database, use any of these individual methods.</span></span>

* <span data-ttu-id="3c8a8-233">[Wznów obliczeń z portalu Azure][Resume compute with Azure portal]</span><span class="sxs-lookup"><span data-stu-id="3c8a8-233">[Resume compute with Azure portal][Resume compute with Azure portal]</span></span>
* <span data-ttu-id="3c8a8-234">[Wznów obliczeń przy użyciu programu PowerShell][Resume compute with PowerShell]</span><span class="sxs-lookup"><span data-stu-id="3c8a8-234">[Resume compute with PowerShell][Resume compute with PowerShell]</span></span>
* <span data-ttu-id="3c8a8-235">[Wznów obliczeń z interfejsów API REST][Resume compute with REST APIs]</span><span class="sxs-lookup"><span data-stu-id="3c8a8-235">[Resume compute with REST APIs][Resume compute with REST APIs]</span></span>

<a name="check-compute-bk"></a>

## <a name="check-database-state"></a><span data-ttu-id="3c8a8-236">Sprawdź stan bazy danych</span><span class="sxs-lookup"><span data-stu-id="3c8a8-236">Check database state</span></span> 

<span data-ttu-id="3c8a8-237">tooresume bazy danych, użyj jednej z tych poszczególnych metod.</span><span class="sxs-lookup"><span data-stu-id="3c8a8-237">tooresume a database, use any of these individual methods.</span></span>

- <span data-ttu-id="3c8a8-238">[Sprawdź stan bazy danych z T-SQL][Check database state with T-SQL]</span><span class="sxs-lookup"><span data-stu-id="3c8a8-238">[Check database state with T-SQL][Check database state with T-SQL]</span></span>
- <span data-ttu-id="3c8a8-239">[Sprawdź stan bazy danych przy użyciu programu PowerShell][Check database state with PowerShell]</span><span class="sxs-lookup"><span data-stu-id="3c8a8-239">[Check database state with PowerShell][Check database state with PowerShell]</span></span>
- <span data-ttu-id="3c8a8-240">[Sprawdź stan bazy danych z interfejsów API REST][Check database state with REST APIs]</span><span class="sxs-lookup"><span data-stu-id="3c8a8-240">[Check database state with REST APIs][Check database state with REST APIs]</span></span>

## <a name="permissions"></a><span data-ttu-id="3c8a8-241">Uprawnienia</span><span class="sxs-lookup"><span data-stu-id="3c8a8-241">Permissions</span></span>

<span data-ttu-id="3c8a8-242">Skalowania hello bazy danych wymaga uprawnień hello opisanego w [ALTER DATABASE][ALTER DATABASE].</span><span class="sxs-lookup"><span data-stu-id="3c8a8-242">Scaling hello database requires hello permissions described in [ALTER DATABASE][ALTER DATABASE].</span></span>  <span data-ttu-id="3c8a8-243">Wstrzymywanie i wznawianie wymagają hello [Współautor bazy danych SQL] [ SQL DB Contributor] uprawnienia, w szczególności Microsoft.Sql/servers/databases/action.</span><span class="sxs-lookup"><span data-stu-id="3c8a8-243">Pause and Resume require hello [SQL DB Contributor][SQL DB Contributor] permission, specifically Microsoft.Sql/servers/databases/action.</span></span>

<a name="next-steps-bk"></a>

## <a name="next-steps"></a><span data-ttu-id="3c8a8-244">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3c8a8-244">Next steps</span></span>
<span data-ttu-id="3c8a8-245">Zapoznaj się następujące artykuły toohelp pojęciami niektóre dodatkowe wydajności toohello:</span><span class="sxs-lookup"><span data-stu-id="3c8a8-245">Refer toohello following articles toohelp you understand some additional key performance concepts:</span></span>

* <span data-ttu-id="3c8a8-246">[Zarządzanie obciążenia i współbieżność][Workload and concurrency management]</span><span class="sxs-lookup"><span data-stu-id="3c8a8-246">[Workload and concurrency management][Workload and concurrency management]</span></span>
* <span data-ttu-id="3c8a8-247">[Omówienie projektowania tabeli][Table design overview]</span><span class="sxs-lookup"><span data-stu-id="3c8a8-247">[Table design overview][Table design overview]</span></span>
* <span data-ttu-id="3c8a8-248">[Dystrybucja tabeli][Table distribution]</span><span class="sxs-lookup"><span data-stu-id="3c8a8-248">[Table distribution][Table distribution]</span></span>
* <span data-ttu-id="3c8a8-249">[Indeksowanie tabeli][Table indexing]</span><span class="sxs-lookup"><span data-stu-id="3c8a8-249">[Table indexing][Table indexing]</span></span>
* <span data-ttu-id="3c8a8-250">[Partycjonowanie tabel][Table partitioning]</span><span class="sxs-lookup"><span data-stu-id="3c8a8-250">[Table partitioning][Table partitioning]</span></span>
* <span data-ttu-id="3c8a8-251">[Statystyk tabeli][Table statistics]</span><span class="sxs-lookup"><span data-stu-id="3c8a8-251">[Table statistics][Table statistics]</span></span>
* <span data-ttu-id="3c8a8-252">[Najlepsze praktyki][Best practices]</span><span class="sxs-lookup"><span data-stu-id="3c8a8-252">[Best practices][Best practices]</span></span>

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
