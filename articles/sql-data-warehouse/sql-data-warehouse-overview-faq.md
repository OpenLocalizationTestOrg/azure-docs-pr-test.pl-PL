---
title: "Magazyn danych Azure SQL — często zadawane pytania | Dokumentacja firmy Microsoft"
description: "W tym artykule wymieniono się często zadawane pytania dotyczące usługi Azure SQL Data Warehouse z klientów i deweloperów"
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: johnmac
editor: 
ms.assetid: 812CA525-3BF3-49DF-8DF3-FB4342464F4F
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: overview
ms.date: 3/1/2017
ms.author: elbutter;barbkess
ms.openlocfilehash: 4c00710ecc0c91f8407eca81b78176075fcbd6ad
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="sql-data-warehouse-frequently-asked-questions"></a><span data-ttu-id="cdc6d-103">SQL Data Warehouse często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="cdc6d-103">SQL Data Warehouse Frequently asked questions</span></span>

## <a name="general"></a><span data-ttu-id="cdc6d-104">Ogólne</span><span class="sxs-lookup"><span data-stu-id="cdc6d-104">General</span></span>

<span data-ttu-id="cdc6d-105">Q.</span><span class="sxs-lookup"><span data-stu-id="cdc6d-105">Q.</span></span> <span data-ttu-id="cdc6d-106">Co oferuje magazynu danych SQL dla bezpieczeństwa danych?</span><span class="sxs-lookup"><span data-stu-id="cdc6d-106">What does SQL DW offer for data security?</span></span>

<span data-ttu-id="cdc6d-107">A.</span><span class="sxs-lookup"><span data-stu-id="cdc6d-107">A.</span></span> <span data-ttu-id="cdc6d-108">Magazynu danych SQL oferuje kilka rozwiązań do ochrony danych, takich jak funkcji TDE i inspekcji.</span><span class="sxs-lookup"><span data-stu-id="cdc6d-108">SQL DW offers several solutions for protecting data such as TDE and auditing.</span></span> <span data-ttu-id="cdc6d-109">Aby uzyskać więcej informacji, zobacz [zabezpieczeń].</span><span class="sxs-lookup"><span data-stu-id="cdc6d-109">For more information, see [Security].</span></span>

<span data-ttu-id="cdc6d-110">Q.</span><span class="sxs-lookup"><span data-stu-id="cdc6d-110">Q.</span></span> <span data-ttu-id="cdc6d-111">Gdzie mogę znaleźć się, jakie normy prawnych lub biznesowych jest SQL magazynu danych zgodne z?</span><span class="sxs-lookup"><span data-stu-id="cdc6d-111">Where can I find out what legal or business standards is SQL DW compliant with?</span></span>

<span data-ttu-id="cdc6d-112">A.</span><span class="sxs-lookup"><span data-stu-id="cdc6d-112">A.</span></span> <span data-ttu-id="cdc6d-113">Odwiedź stronę [Compliance Microsoft] strony dla różnych ofert zgodności przez produktów, takich jak SOC i ISO.</span><span class="sxs-lookup"><span data-stu-id="cdc6d-113">Visit the [Microsoft Compliance] page for various compliance offerings by product such as SOC and ISO.</span></span> <span data-ttu-id="cdc6d-114">Najpierw wybierz przez tytuł zgodności, a następnie rozwiń węzeł Azure w sekcji firmy Microsoft w zakresie chmury usług w prawej strony, aby sprawdzić, jakie usługi są Azure usługi są zgodne.</span><span class="sxs-lookup"><span data-stu-id="cdc6d-114">First choose by Compliance title, then expand Azure in the Microsoft in-scope cloud services section on the right side of the page to see what services are Azure services are compliant.</span></span>

<span data-ttu-id="cdc6d-115">Q.</span><span class="sxs-lookup"><span data-stu-id="cdc6d-115">Q.</span></span> <span data-ttu-id="cdc6d-116">Czy można połączyć usługi Power BI?</span><span class="sxs-lookup"><span data-stu-id="cdc6d-116">Can I connect PowerBI?</span></span>

<span data-ttu-id="cdc6d-117">A.</span><span class="sxs-lookup"><span data-stu-id="cdc6d-117">A.</span></span> <span data-ttu-id="cdc6d-118">Tak!</span><span class="sxs-lookup"><span data-stu-id="cdc6d-118">Yes!</span></span> <span data-ttu-id="cdc6d-119">Chociaż usługa Power BI obsługuje zapytania bezpośredniego z magazynu danych SQL, nie jest przeznaczony dla dużej liczby użytkowników lub danych w czasie rzeczywistym.</span><span class="sxs-lookup"><span data-stu-id="cdc6d-119">Though PowerBI supports direct query with SQL DW, it’s not intended for large number of users or real-time data.</span></span> <span data-ttu-id="cdc6d-120">Do użytku produkcyjnego usługi Power BI zaleca się przy użyciu usługi Power BI na górze usług Azure Analysis Services lub analizy usługi IaaS.</span><span class="sxs-lookup"><span data-stu-id="cdc6d-120">For production use of PowerBI, we recommend using PowerBI on top of Azure Analysis Services or Analysis Service IaaS.</span></span> 

<span data-ttu-id="cdc6d-121">Q.</span><span class="sxs-lookup"><span data-stu-id="cdc6d-121">Q.</span></span> <span data-ttu-id="cdc6d-122">Jakie są limity pojemności magazynu danych SQL?</span><span class="sxs-lookup"><span data-stu-id="cdc6d-122">What are SQL Data Warehouse Capacity Limits?</span></span>

<span data-ttu-id="cdc6d-123">A.</span><span class="sxs-lookup"><span data-stu-id="cdc6d-123">A.</span></span> <span data-ttu-id="cdc6d-124">Zobacz nasze bieżące [limity pojemności] strony.</span><span class="sxs-lookup"><span data-stu-id="cdc6d-124">See our current [capacity limits] page.</span></span> 

<span data-ttu-id="cdc6d-125">Q.</span><span class="sxs-lookup"><span data-stu-id="cdc6d-125">Q.</span></span> <span data-ttu-id="cdc6d-126">Dlaczego moja skali/wstrzymanie/wznowienie trwa tak długo?</span><span class="sxs-lookup"><span data-stu-id="cdc6d-126">Why is my Scale/Pause/Resume taking so long?</span></span>

<span data-ttu-id="cdc6d-127">A.</span><span class="sxs-lookup"><span data-stu-id="cdc6d-127">A.</span></span> <span data-ttu-id="cdc6d-128">Różne czynniki mogą mieć wpływ czasu dla operacji zarządzania obliczeń.</span><span class="sxs-lookup"><span data-stu-id="cdc6d-128">A variety of factors can influence the time for compute management operations.</span></span> <span data-ttu-id="cdc6d-129">Typowy przypadek długotrwałe operacje jest transakcyjna wycofywania.</span><span class="sxs-lookup"><span data-stu-id="cdc6d-129">A common case for  long running operations is transactional rollback.</span></span> <span data-ttu-id="cdc6d-130">Po zainicjowaniu operacji skalowania lub Wstrzymaj wszystkie sesje przychodzące są blokowane, a zostały opróżnione zapytania.</span><span class="sxs-lookup"><span data-stu-id="cdc6d-130">When a scale or pause operation is initiated, all incoming sessions are blocked and queries are drained.</span></span> <span data-ttu-id="cdc6d-131">Aby opuścić system stabilna, transakcje muszą wycofana, przed rozpoczęciem operacji.</span><span class="sxs-lookup"><span data-stu-id="cdc6d-131">In order to leave the system in a stable state, transactions must be rolled back before an operation can commence.</span></span> <span data-ttu-id="cdc6d-132">Większa liczba i większa rozmiaru dziennika transakcji, zostanie zablokowany im dłuższy operacji przywracania systemu do stabilności.</span><span class="sxs-lookup"><span data-stu-id="cdc6d-132">The greater the number and larger the log size of transactions, the longer the operation will be stalled restoring the system to a stable state.</span></span>

## <a name="user-support"></a><span data-ttu-id="cdc6d-133">Obsługa użytkowników</span><span class="sxs-lookup"><span data-stu-id="cdc6d-133">User support</span></span>

<span data-ttu-id="cdc6d-134">Q.</span><span class="sxs-lookup"><span data-stu-id="cdc6d-134">Q.</span></span> <span data-ttu-id="cdc6d-135">Mam zgłoszenie dotyczące funkcji, gdzie jest przesyłanie?</span><span class="sxs-lookup"><span data-stu-id="cdc6d-135">I have a feature request, where do I submit it?</span></span>

<span data-ttu-id="cdc6d-136">A.</span><span class="sxs-lookup"><span data-stu-id="cdc6d-136">A.</span></span> <span data-ttu-id="cdc6d-137">Jeśli żądanie funkcji, Prześlij go na naszych [UserVoice] strony</span><span class="sxs-lookup"><span data-stu-id="cdc6d-137">If you have a feature request, submit it on our [UserVoice] page</span></span>

<span data-ttu-id="cdc6d-138">Q.</span><span class="sxs-lookup"><span data-stu-id="cdc6d-138">Q.</span></span> <span data-ttu-id="cdc6d-139">Jak mogę przeprowadzić x?</span><span class="sxs-lookup"><span data-stu-id="cdc6d-139">How can I do x?</span></span>

<span data-ttu-id="cdc6d-140">A.</span><span class="sxs-lookup"><span data-stu-id="cdc6d-140">A.</span></span> <span data-ttu-id="cdc6d-141">Aby uzyskać pomoc w tworzeniu z usługą Magazyn danych SQL, można zadawać pytania na naszych [przepełnienie stosu] strony.</span><span class="sxs-lookup"><span data-stu-id="cdc6d-141">For help in developing with SQL Data Warehouse, you can ask questions on our [Stack Overflow] page.</span></span> 

<span data-ttu-id="cdc6d-142">Q.</span><span class="sxs-lookup"><span data-stu-id="cdc6d-142">Q.</span></span> <span data-ttu-id="cdc6d-143">Jak przesłać biletu pomocy technicznej</span><span class="sxs-lookup"><span data-stu-id="cdc6d-143">How do I submit a support ticket?</span></span>

<span data-ttu-id="cdc6d-144">A.</span><span class="sxs-lookup"><span data-stu-id="cdc6d-144">A.</span></span> <span data-ttu-id="cdc6d-145">[Bilety obsługi] można złożyć za pośrednictwem portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="cdc6d-145">[Support Tickets] can be filed through Azure portal.</span></span>

## <a name="sql-languagefeature-support"></a><span data-ttu-id="cdc6d-146">Obsługa języka/funkcja SQL</span><span class="sxs-lookup"><span data-stu-id="cdc6d-146">SQL language/feature support</span></span> 

<span data-ttu-id="cdc6d-147">Q.</span><span class="sxs-lookup"><span data-stu-id="cdc6d-147">Q.</span></span> <span data-ttu-id="cdc6d-148">Jakie typy danych obsługuje magazyn danych SQL?</span><span class="sxs-lookup"><span data-stu-id="cdc6d-148">What datatypes does SQL Data Warehouse support?</span></span>

<span data-ttu-id="cdc6d-149">A.</span><span class="sxs-lookup"><span data-stu-id="cdc6d-149">A.</span></span> <span data-ttu-id="cdc6d-150">Zobacz SQL Data Warehouse [typy danych].</span><span class="sxs-lookup"><span data-stu-id="cdc6d-150">See SQL Data Warehouse [data types].</span></span>

<span data-ttu-id="cdc6d-151">Q.</span><span class="sxs-lookup"><span data-stu-id="cdc6d-151">Q.</span></span> <span data-ttu-id="cdc6d-152">Jakie funkcje tabeli są obsługiwane?</span><span class="sxs-lookup"><span data-stu-id="cdc6d-152">What table features do you support?</span></span>

<span data-ttu-id="cdc6d-153">A.</span><span class="sxs-lookup"><span data-stu-id="cdc6d-153">A.</span></span> <span data-ttu-id="cdc6d-154">Podczas gdy magazyn danych SQL obsługuje wiele funkcji, niektóre nie są obsługiwane i są udokumentowane w artykule [nieobsługiwanych funkcji tabeli].</span><span class="sxs-lookup"><span data-stu-id="cdc6d-154">While SQL Data Warehouse supports many features, some are not supported and are documented in [Unsupported Table Features].</span></span>

## <a name="tooling-and-administration"></a><span data-ttu-id="cdc6d-155">Narzędzia i administracji</span><span class="sxs-lookup"><span data-stu-id="cdc6d-155">Tooling and administration</span></span>

<span data-ttu-id="cdc6d-156">Q.</span><span class="sxs-lookup"><span data-stu-id="cdc6d-156">Q.</span></span> <span data-ttu-id="cdc6d-157">Obsługuje projektów bazy danych w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cdc6d-157">Do you support Database projects in Visual Studio.</span></span>

<span data-ttu-id="cdc6d-158">A.</span><span class="sxs-lookup"><span data-stu-id="cdc6d-158">A.</span></span> <span data-ttu-id="cdc6d-159">Obecnie nie obsługujemy projektów baz danych w programie Visual Studio dla usługi SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="cdc6d-159">We currently do not support Database projects in Visual Studio for SQL Data Warehouse.</span></span> <span data-ttu-id="cdc6d-160">Jeśli chcesz oddanych głosów można pobrać tej funkcji, można znaleźć w naszych User Voice [projektów bazy danych funkcji żądania].</span><span class="sxs-lookup"><span data-stu-id="cdc6d-160">If you'd like to cast a vote to get this feature, visit our User Voice [Database projects feature request].</span></span>

<span data-ttu-id="cdc6d-161">Q.</span><span class="sxs-lookup"><span data-stu-id="cdc6d-161">Q.</span></span> <span data-ttu-id="cdc6d-162">Magazyn danych SQL obsługuje interfejsy API REST?</span><span class="sxs-lookup"><span data-stu-id="cdc6d-162">Does SQL Data Warehouse support REST APIs?</span></span>

<span data-ttu-id="cdc6d-163">A.</span><span class="sxs-lookup"><span data-stu-id="cdc6d-163">A.</span></span> <span data-ttu-id="cdc6d-164">Tak.</span><span class="sxs-lookup"><span data-stu-id="cdc6d-164">Yes.</span></span> <span data-ttu-id="cdc6d-165">Większość funkcji REST, które mogą być używane z bazą danych SQL jest również dostępna w programie SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="cdc6d-165">Most REST functionality that can be used with SQL Database is also available with SQL Data Warehouse.</span></span> <span data-ttu-id="cdc6d-166">Możesz znaleźć informacji interfejsu API REST stron z dokumentacją lub [MSDN].</span><span class="sxs-lookup"><span data-stu-id="cdc6d-166">You can find API information within REST documentation pages or [MSDN].</span></span>


## <a name="loading"></a><span data-ttu-id="cdc6d-167">Ładowanie</span><span class="sxs-lookup"><span data-stu-id="cdc6d-167">Loading</span></span>

<span data-ttu-id="cdc6d-168">Q.</span><span class="sxs-lookup"><span data-stu-id="cdc6d-168">Q.</span></span> <span data-ttu-id="cdc6d-169">Jakie sterowniki klienta są obsługiwane?</span><span class="sxs-lookup"><span data-stu-id="cdc6d-169">What client drivers do you support?</span></span>

<span data-ttu-id="cdc6d-170">A.</span><span class="sxs-lookup"><span data-stu-id="cdc6d-170">A.</span></span> <span data-ttu-id="cdc6d-171">Obsługa sterowników dla magazynu danych można znaleźć w [parametry połączenia] strony</span><span class="sxs-lookup"><span data-stu-id="cdc6d-171">Driver support for DW can be found on the [Connection Strings] page</span></span>

<span data-ttu-id="cdc6d-172">Pytanie: jakie formaty plików są obsługiwane przez aparat PolyBase z magazynu danych SQL?</span><span class="sxs-lookup"><span data-stu-id="cdc6d-172">Q: What file formats are supported by PolyBase with SQL Data Warehouse?</span></span>

<span data-ttu-id="cdc6d-173">Odpowiedź: Orc, RC Parquet i płaskiej tekstu rozdzielanego</span><span class="sxs-lookup"><span data-stu-id="cdc6d-173">A: Orc, RC, Parquet, and flat delimited text</span></span>

<span data-ttu-id="cdc6d-174">Pytanie: jakie mogą I łączyć się z magazynu danych SQL przy użyciu programu PolyBase?</span><span class="sxs-lookup"><span data-stu-id="cdc6d-174">Q: What can I connect to from SQL DW using PolyBase?</span></span> 

<span data-ttu-id="cdc6d-175">Odpowiedź: [usługi Azure Data Lake Store] i [obiektów blob magazynu Azure]</span><span class="sxs-lookup"><span data-stu-id="cdc6d-175">A: [Azure Data Lake Store] and [Azure Storage Blobs]</span></span>

<span data-ttu-id="cdc6d-176">Pytanie: jest przekazywanie obliczeń możliwe podczas nawiązywania połączenia obiektach blob magazynu Azure lub ADLS?</span><span class="sxs-lookup"><span data-stu-id="cdc6d-176">Q: Is computation pushdown possible  when connecting to Azure Storage Blobs or ADLS?</span></span> 

<span data-ttu-id="cdc6d-177">Odpowiedź: nie PolyBase magazynu danych SQL interakcja składników magazynu.</span><span class="sxs-lookup"><span data-stu-id="cdc6d-177">A: No, SQL DW PolyBase only interacts the storage components.</span></span> 

<span data-ttu-id="cdc6d-178">Pytanie: czy można podłączyć do HDI?</span><span class="sxs-lookup"><span data-stu-id="cdc6d-178">Q: Can I connect to HDI?</span></span>

<span data-ttu-id="cdc6d-179">Odpowiedź: HDI służy ADLS lub WASB warstwy systemu plików HDFS.</span><span class="sxs-lookup"><span data-stu-id="cdc6d-179">A: HDI can use either ADLS or WASB as the HDFS layer.</span></span> <span data-ttu-id="cdc6d-180">Jeśli masz jako warstwa systemu plików HDFS można załadować danych do magazynu danych SQL.</span><span class="sxs-lookup"><span data-stu-id="cdc6d-180">If you have either as your HDFS layer, then you can load that data into SQL DW.</span></span> <span data-ttu-id="cdc6d-181">Jednak nie można wygenerować obliczeń przekazywanie do wystąpienia HDI.</span><span class="sxs-lookup"><span data-stu-id="cdc6d-181">However, you cannot generate pushdown computation to the HDI instance.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="cdc6d-182">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="cdc6d-182">Next steps</span></span>
<span data-ttu-id="cdc6d-183">Aby uzyskać więcej informacji na magazyn danych SQL jako całość, zobacz nasze [omówienie] strony.</span><span class="sxs-lookup"><span data-stu-id="cdc6d-183">For more information on SQL Data Warehouse as a whole, see our [Overview] page.</span></span>


<!-- Article references -->
<span data-ttu-id="cdc6d-184">[UserVoice]: https://feedback.azure.com/forums/307516-sql-data-warehouse</span><span class="sxs-lookup"><span data-stu-id="cdc6d-184">[UserVoice]: https://feedback.azure.com/forums/307516-sql-data-warehouse</span></span>
<span data-ttu-id="cdc6d-185">[parametry połączenia]: ./sql-data-warehouse-connection-strings.md</span><span class="sxs-lookup"><span data-stu-id="cdc6d-185">[Connection Strings]: ./sql-data-warehouse-connection-strings.md</span></span>
<span data-ttu-id="cdc6d-186">[przepełnienie stosu]: http://stackoverflow.com/questions/tagged/azure-sqldw</span><span class="sxs-lookup"><span data-stu-id="cdc6d-186">[Stack Overflow]: http://stackoverflow.com/questions/tagged/azure-sqldw</span></span>
<span data-ttu-id="cdc6d-187">[Bilety obsługi]: ./sql-data-warehouse-get-started-create-support-ticket.md</span><span class="sxs-lookup"><span data-stu-id="cdc6d-187">[Support Tickets]: ./sql-data-warehouse-get-started-create-support-ticket.md</span></span>
<span data-ttu-id="cdc6d-188">[zabezpieczeń]: ./sql-data-warehouse-overview-manage-security.md</span><span class="sxs-lookup"><span data-stu-id="cdc6d-188">[Security]: ./sql-data-warehouse-overview-manage-security.md</span></span>
<span data-ttu-id="cdc6d-189">[Compliance Microsoft]: https://www.microsoft.com/en-us/trustcenter/compliance/complianceofferings</span><span class="sxs-lookup"><span data-stu-id="cdc6d-189">[Microsoft Compliance]: https://www.microsoft.com/en-us/trustcenter/compliance/complianceofferings</span></span>
<span data-ttu-id="cdc6d-190">[limity pojemności]: ./sql-data-warehouse-service-capacity-limits.md</span><span class="sxs-lookup"><span data-stu-id="cdc6d-190">[capacity limits]: ./sql-data-warehouse-service-capacity-limits.md</span></span>
<span data-ttu-id="cdc6d-191">[typy danych]: ./sql-data-warehouse-tables-data-types.md</span><span class="sxs-lookup"><span data-stu-id="cdc6d-191">[data types]: ./sql-data-warehouse-tables-data-types.md</span></span>
<span data-ttu-id="cdc6d-192">[nieobsługiwanych funkcji tabeli]: ./sql-data-warehouse-tables-overview.md#unsupported-table-features</span><span class="sxs-lookup"><span data-stu-id="cdc6d-192">[Unsupported Table Features]: ./sql-data-warehouse-tables-overview.md#unsupported-table-features</span></span>
<span data-ttu-id="cdc6d-193">[usługi Azure Data Lake Store]: ./sql-data-warehouse-load-from-azure-data-lake-store.md</span><span class="sxs-lookup"><span data-stu-id="cdc6d-193">[Azure Data Lake Store]: ./sql-data-warehouse-load-from-azure-data-lake-store.md</span></span>
<span data-ttu-id="cdc6d-194">[obiektów blob magazynu Azure]: ./sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md</span><span class="sxs-lookup"><span data-stu-id="cdc6d-194">[Azure Storage Blobs]: ./sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md</span></span>
<span data-ttu-id="cdc6d-195">[projektów bazy danych funkcji żądania]: https://feedback.azure.com/forums/307516-sql-data-warehouse/suggestions/13313247-database-project-from-visual-studio-to-support-azu</span><span class="sxs-lookup"><span data-stu-id="cdc6d-195">[Database projects feature request]: https://feedback.azure.com/forums/307516-sql-data-warehouse/suggestions/13313247-database-project-from-visual-studio-to-support-azu</span></span>
<span data-ttu-id="cdc6d-196">[MSDN]: https://msdn.microsoft.com/en-us/library/azure/mt163685.aspx</span><span class="sxs-lookup"><span data-stu-id="cdc6d-196">[MSDN]: https://msdn.microsoft.com/en-us/library/azure/mt163685.aspx</span></span>
<span data-ttu-id="cdc6d-197">[omówienie]: ./sql-data-warehouse-overview-faq.md</span><span class="sxs-lookup"><span data-stu-id="cdc6d-197">[Overview]: ./sql-data-warehouse-overview-faq.md</span></span>