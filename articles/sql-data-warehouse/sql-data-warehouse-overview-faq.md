---
title: "aaaAzure SQL Data Warehouse — często zadawane pytania | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 09fd3f65d9507b09fcb8f477742c7d020add2755
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="sql-data-warehouse-frequently-asked-questions"></a><span data-ttu-id="b57d4-103">SQL Data Warehouse często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="b57d4-103">SQL Data Warehouse Frequently asked questions</span></span>

## <a name="general"></a><span data-ttu-id="b57d4-104">Ogólne</span><span class="sxs-lookup"><span data-stu-id="b57d4-104">General</span></span>

<span data-ttu-id="b57d4-105">Q.</span><span class="sxs-lookup"><span data-stu-id="b57d4-105">Q.</span></span> <span data-ttu-id="b57d4-106">Co oferuje magazynu danych SQL dla bezpieczeństwa danych?</span><span class="sxs-lookup"><span data-stu-id="b57d4-106">What does SQL DW offer for data security?</span></span>

<span data-ttu-id="b57d4-107">A.</span><span class="sxs-lookup"><span data-stu-id="b57d4-107">A.</span></span> <span data-ttu-id="b57d4-108">Magazynu danych SQL oferuje kilka rozwiązań do ochrony danych, takich jak funkcji TDE i inspekcji.</span><span class="sxs-lookup"><span data-stu-id="b57d4-108">SQL DW offers several solutions for protecting data such as TDE and auditing.</span></span> <span data-ttu-id="b57d4-109">Aby uzyskać więcej informacji, zobacz [zabezpieczeń].</span><span class="sxs-lookup"><span data-stu-id="b57d4-109">For more information, see [Security].</span></span>

<span data-ttu-id="b57d4-110">Q.</span><span class="sxs-lookup"><span data-stu-id="b57d4-110">Q.</span></span> <span data-ttu-id="b57d4-111">Gdzie mogę znaleźć się, jakie normy prawnych lub biznesowych jest SQL magazynu danych zgodne z?</span><span class="sxs-lookup"><span data-stu-id="b57d4-111">Where can I find out what legal or business standards is SQL DW compliant with?</span></span>

<span data-ttu-id="b57d4-112">A.</span><span class="sxs-lookup"><span data-stu-id="b57d4-112">A.</span></span> <span data-ttu-id="b57d4-113">Odwiedź hello [Compliance Microsoft] strony dla różnych ofert zgodności przez produktów, takich jak SOC i ISO.</span><span class="sxs-lookup"><span data-stu-id="b57d4-113">Visit hello [Microsoft Compliance] page for various compliance offerings by product such as SOC and ISO.</span></span> <span data-ttu-id="b57d4-114">Najpierw wybierz przez tytuł zgodności, a następnie rozwiń węzeł Azure hello firmy Microsoft w zakresie chmury usługi część hello prawej strony toosee strony hello usług są usług platformy Azure są zgodne.</span><span class="sxs-lookup"><span data-stu-id="b57d4-114">First choose by Compliance title, then expand Azure in hello Microsoft in-scope cloud services section on hello right side of hello page toosee what services are Azure services are compliant.</span></span>

<span data-ttu-id="b57d4-115">Q.</span><span class="sxs-lookup"><span data-stu-id="b57d4-115">Q.</span></span> <span data-ttu-id="b57d4-116">Czy można połączyć usługi Power BI?</span><span class="sxs-lookup"><span data-stu-id="b57d4-116">Can I connect PowerBI?</span></span>

<span data-ttu-id="b57d4-117">A.</span><span class="sxs-lookup"><span data-stu-id="b57d4-117">A.</span></span> <span data-ttu-id="b57d4-118">Tak!</span><span class="sxs-lookup"><span data-stu-id="b57d4-118">Yes!</span></span> <span data-ttu-id="b57d4-119">Chociaż usługa Power BI obsługuje zapytania bezpośredniego z magazynu danych SQL, nie jest przeznaczony dla dużej liczby użytkowników lub danych w czasie rzeczywistym.</span><span class="sxs-lookup"><span data-stu-id="b57d4-119">Though PowerBI supports direct query with SQL DW, it’s not intended for large number of users or real-time data.</span></span> <span data-ttu-id="b57d4-120">Do użytku produkcyjnego usługi Power BI zaleca się przy użyciu usługi Power BI na górze usług Azure Analysis Services lub analizy usługi IaaS.</span><span class="sxs-lookup"><span data-stu-id="b57d4-120">For production use of PowerBI, we recommend using PowerBI on top of Azure Analysis Services or Analysis Service IaaS.</span></span> 

<span data-ttu-id="b57d4-121">Q.</span><span class="sxs-lookup"><span data-stu-id="b57d4-121">Q.</span></span> <span data-ttu-id="b57d4-122">Jakie są limity pojemności magazynu danych SQL?</span><span class="sxs-lookup"><span data-stu-id="b57d4-122">What are SQL Data Warehouse Capacity Limits?</span></span>

<span data-ttu-id="b57d4-123">A.</span><span class="sxs-lookup"><span data-stu-id="b57d4-123">A.</span></span> <span data-ttu-id="b57d4-124">Zobacz nasze bieżące [limity pojemności] strony.</span><span class="sxs-lookup"><span data-stu-id="b57d4-124">See our current [capacity limits] page.</span></span> 

<span data-ttu-id="b57d4-125">Q.</span><span class="sxs-lookup"><span data-stu-id="b57d4-125">Q.</span></span> <span data-ttu-id="b57d4-126">Dlaczego moja skali/wstrzymanie/wznowienie trwa tak długo?</span><span class="sxs-lookup"><span data-stu-id="b57d4-126">Why is my Scale/Pause/Resume taking so long?</span></span>

<span data-ttu-id="b57d4-127">A.</span><span class="sxs-lookup"><span data-stu-id="b57d4-127">A.</span></span> <span data-ttu-id="b57d4-128">Różne czynniki mogą mieć wpływ hello czasu dla operacji zarządzania obliczeń.</span><span class="sxs-lookup"><span data-stu-id="b57d4-128">A variety of factors can influence hello time for compute management operations.</span></span> <span data-ttu-id="b57d4-129">Typowy przypadek długotrwałe operacje jest transakcyjna wycofywania.</span><span class="sxs-lookup"><span data-stu-id="b57d4-129">A common case for  long running operations is transactional rollback.</span></span> <span data-ttu-id="b57d4-130">Po zainicjowaniu operacji skalowania lub Wstrzymaj wszystkie sesje przychodzące są blokowane, a zostały opróżnione zapytania.</span><span class="sxs-lookup"><span data-stu-id="b57d4-130">When a scale or pause operation is initiated, all incoming sessions are blocked and queries are drained.</span></span> <span data-ttu-id="b57d4-131">W systemie hello tooleave kolejności stabilna transakcje musi wycofana, przed rozpoczęciem operacji.</span><span class="sxs-lookup"><span data-stu-id="b57d4-131">In order tooleave hello system in a stable state, transactions must be rolled back before an operation can commence.</span></span> <span data-ttu-id="b57d4-132">Witaj większą liczbą hello i większy rozmiar dziennika hello transakcji, hello dłużej hello operacji zostanie zablokowany, przywracanie hello systemu tooa stabilności.</span><span class="sxs-lookup"><span data-stu-id="b57d4-132">hello greater hello number and larger hello log size of transactions, hello longer hello operation will be stalled restoring hello system tooa stable state.</span></span>

## <a name="user-support"></a><span data-ttu-id="b57d4-133">Obsługa użytkowników</span><span class="sxs-lookup"><span data-stu-id="b57d4-133">User support</span></span>

<span data-ttu-id="b57d4-134">Q.</span><span class="sxs-lookup"><span data-stu-id="b57d4-134">Q.</span></span> <span data-ttu-id="b57d4-135">Mam zgłoszenie dotyczące funkcji, gdzie jest przesyłanie?</span><span class="sxs-lookup"><span data-stu-id="b57d4-135">I have a feature request, where do I submit it?</span></span>

<span data-ttu-id="b57d4-136">A.</span><span class="sxs-lookup"><span data-stu-id="b57d4-136">A.</span></span> <span data-ttu-id="b57d4-137">Jeśli żądanie funkcji, Prześlij go na naszych [UserVoice] strony</span><span class="sxs-lookup"><span data-stu-id="b57d4-137">If you have a feature request, submit it on our [UserVoice] page</span></span>

<span data-ttu-id="b57d4-138">Q.</span><span class="sxs-lookup"><span data-stu-id="b57d4-138">Q.</span></span> <span data-ttu-id="b57d4-139">Jak mogę przeprowadzić x?</span><span class="sxs-lookup"><span data-stu-id="b57d4-139">How can I do x?</span></span>

<span data-ttu-id="b57d4-140">A.</span><span class="sxs-lookup"><span data-stu-id="b57d4-140">A.</span></span> <span data-ttu-id="b57d4-141">Aby uzyskać pomoc w tworzeniu z usługą Magazyn danych SQL, można zadawać pytania na naszych [przepełnienie stosu] strony.</span><span class="sxs-lookup"><span data-stu-id="b57d4-141">For help in developing with SQL Data Warehouse, you can ask questions on our [Stack Overflow] page.</span></span> 

<span data-ttu-id="b57d4-142">Q.</span><span class="sxs-lookup"><span data-stu-id="b57d4-142">Q.</span></span> <span data-ttu-id="b57d4-143">Jak przesłać biletu pomocy technicznej</span><span class="sxs-lookup"><span data-stu-id="b57d4-143">How do I submit a support ticket?</span></span>

<span data-ttu-id="b57d4-144">A.</span><span class="sxs-lookup"><span data-stu-id="b57d4-144">A.</span></span> <span data-ttu-id="b57d4-145">[Bilety obsługi] można złożyć za pośrednictwem portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="b57d4-145">[Support Tickets] can be filed through Azure portal.</span></span>

## <a name="sql-languagefeature-support"></a><span data-ttu-id="b57d4-146">Obsługa języka/funkcja SQL</span><span class="sxs-lookup"><span data-stu-id="b57d4-146">SQL language/feature support</span></span> 

<span data-ttu-id="b57d4-147">Q.</span><span class="sxs-lookup"><span data-stu-id="b57d4-147">Q.</span></span> <span data-ttu-id="b57d4-148">Jakie typy danych obsługuje magazyn danych SQL?</span><span class="sxs-lookup"><span data-stu-id="b57d4-148">What datatypes does SQL Data Warehouse support?</span></span>

<span data-ttu-id="b57d4-149">A.</span><span class="sxs-lookup"><span data-stu-id="b57d4-149">A.</span></span> <span data-ttu-id="b57d4-150">Zobacz SQL Data Warehouse [typy danych].</span><span class="sxs-lookup"><span data-stu-id="b57d4-150">See SQL Data Warehouse [data types].</span></span>

<span data-ttu-id="b57d4-151">Q.</span><span class="sxs-lookup"><span data-stu-id="b57d4-151">Q.</span></span> <span data-ttu-id="b57d4-152">Jakie funkcje tabeli są obsługiwane?</span><span class="sxs-lookup"><span data-stu-id="b57d4-152">What table features do you support?</span></span>

<span data-ttu-id="b57d4-153">A.</span><span class="sxs-lookup"><span data-stu-id="b57d4-153">A.</span></span> <span data-ttu-id="b57d4-154">Podczas gdy magazyn danych SQL obsługuje wiele funkcji, niektóre nie są obsługiwane i są udokumentowane w artykule [nieobsługiwanych funkcji tabeli].</span><span class="sxs-lookup"><span data-stu-id="b57d4-154">While SQL Data Warehouse supports many features, some are not supported and are documented in [Unsupported Table Features].</span></span>

## <a name="tooling-and-administration"></a><span data-ttu-id="b57d4-155">Narzędzia i administracji</span><span class="sxs-lookup"><span data-stu-id="b57d4-155">Tooling and administration</span></span>

<span data-ttu-id="b57d4-156">Q.</span><span class="sxs-lookup"><span data-stu-id="b57d4-156">Q.</span></span> <span data-ttu-id="b57d4-157">Obsługuje projektów bazy danych w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b57d4-157">Do you support Database projects in Visual Studio.</span></span>

<span data-ttu-id="b57d4-158">A.</span><span class="sxs-lookup"><span data-stu-id="b57d4-158">A.</span></span> <span data-ttu-id="b57d4-159">Obecnie nie obsługujemy projektów baz danych w programie Visual Studio dla usługi SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="b57d4-159">We currently do not support Database projects in Visual Studio for SQL Data Warehouse.</span></span> <span data-ttu-id="b57d4-160">Jeśli chcesz toocast tooget głos tej funkcji, można znaleźć w naszych User Voice [projektów bazy danych funkcji żądania].</span><span class="sxs-lookup"><span data-stu-id="b57d4-160">If you'd like toocast a vote tooget this feature, visit our User Voice [Database projects feature request].</span></span>

<span data-ttu-id="b57d4-161">Q.</span><span class="sxs-lookup"><span data-stu-id="b57d4-161">Q.</span></span> <span data-ttu-id="b57d4-162">Magazyn danych SQL obsługuje interfejsy API REST?</span><span class="sxs-lookup"><span data-stu-id="b57d4-162">Does SQL Data Warehouse support REST APIs?</span></span>

<span data-ttu-id="b57d4-163">A.</span><span class="sxs-lookup"><span data-stu-id="b57d4-163">A.</span></span> <span data-ttu-id="b57d4-164">Tak.</span><span class="sxs-lookup"><span data-stu-id="b57d4-164">Yes.</span></span> <span data-ttu-id="b57d4-165">Większość funkcji REST, które mogą być używane z bazą danych SQL jest również dostępna w programie SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="b57d4-165">Most REST functionality that can be used with SQL Database is also available with SQL Data Warehouse.</span></span> <span data-ttu-id="b57d4-166">Możesz znaleźć informacji interfejsu API REST stron z dokumentacją lub [MSDN].</span><span class="sxs-lookup"><span data-stu-id="b57d4-166">You can find API information within REST documentation pages or [MSDN].</span></span>


## <a name="loading"></a><span data-ttu-id="b57d4-167">Ładowanie</span><span class="sxs-lookup"><span data-stu-id="b57d4-167">Loading</span></span>

<span data-ttu-id="b57d4-168">Q.</span><span class="sxs-lookup"><span data-stu-id="b57d4-168">Q.</span></span> <span data-ttu-id="b57d4-169">Jakie sterowniki klienta są obsługiwane?</span><span class="sxs-lookup"><span data-stu-id="b57d4-169">What client drivers do you support?</span></span>

<span data-ttu-id="b57d4-170">A.</span><span class="sxs-lookup"><span data-stu-id="b57d4-170">A.</span></span> <span data-ttu-id="b57d4-171">Obsługa sterowników dla magazynu danych można znaleźć na powitania [parametry połączenia] strony</span><span class="sxs-lookup"><span data-stu-id="b57d4-171">Driver support for DW can be found on hello [Connection Strings] page</span></span>

<span data-ttu-id="b57d4-172">Pytanie: jakie formaty plików są obsługiwane przez aparat PolyBase z magazynu danych SQL?</span><span class="sxs-lookup"><span data-stu-id="b57d4-172">Q: What file formats are supported by PolyBase with SQL Data Warehouse?</span></span>

<span data-ttu-id="b57d4-173">Odpowiedź: Orc, RC Parquet i płaskiej tekstu rozdzielanego</span><span class="sxs-lookup"><span data-stu-id="b57d4-173">A: Orc, RC, Parquet, and flat delimited text</span></span>

<span data-ttu-id="b57d4-174">Pytanie: jakie można podłączyć toofrom SQL DW przy użyciu programu PolyBase?</span><span class="sxs-lookup"><span data-stu-id="b57d4-174">Q: What can I connect toofrom SQL DW using PolyBase?</span></span> 

<span data-ttu-id="b57d4-175">Odpowiedź: [usługi Azure Data Lake Store] i [obiektów blob magazynu Azure]</span><span class="sxs-lookup"><span data-stu-id="b57d4-175">A: [Azure Data Lake Store] and [Azure Storage Blobs]</span></span>

<span data-ttu-id="b57d4-176">Pytanie: jest przekazywanie obliczeń możliwe podczas łączenia tooAzure magazynu obiektów blob lub ADLS?</span><span class="sxs-lookup"><span data-stu-id="b57d4-176">Q: Is computation pushdown possible  when connecting tooAzure Storage Blobs or ADLS?</span></span> 

<span data-ttu-id="b57d4-177">Odpowiedź: nie PolyBase magazynu danych SQL współdziała hello składników magazynu.</span><span class="sxs-lookup"><span data-stu-id="b57d4-177">A: No, SQL DW PolyBase only interacts hello storage components.</span></span> 

<span data-ttu-id="b57d4-178">Pytanie: czy można podłączyć tooHDI?</span><span class="sxs-lookup"><span data-stu-id="b57d4-178">Q: Can I connect tooHDI?</span></span>

<span data-ttu-id="b57d4-179">Odpowiedź: HDI służy ADLS lub WASB hello systemu plików HDFS warstwy.</span><span class="sxs-lookup"><span data-stu-id="b57d4-179">A: HDI can use either ADLS or WASB as hello HDFS layer.</span></span> <span data-ttu-id="b57d4-180">Jeśli masz jako warstwa systemu plików HDFS można załadować danych do magazynu danych SQL.</span><span class="sxs-lookup"><span data-stu-id="b57d4-180">If you have either as your HDFS layer, then you can load that data into SQL DW.</span></span> <span data-ttu-id="b57d4-181">Jednak nie można wygenerować wystąpienia HDI toohello obliczeń przekazywanie.</span><span class="sxs-lookup"><span data-stu-id="b57d4-181">However, you cannot generate pushdown computation toohello HDI instance.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="b57d4-182">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b57d4-182">Next steps</span></span>
<span data-ttu-id="b57d4-183">Aby uzyskać więcej informacji na magazyn danych SQL jako całość, zobacz nasze [omówienie] strony.</span><span class="sxs-lookup"><span data-stu-id="b57d4-183">For more information on SQL Data Warehouse as a whole, see our [Overview] page.</span></span>


<!-- Article references -->
[UserVoice]: https://feedback.azure.com/forums/307516-sql-data-warehouse
[parametry połączenia]: ./sql-data-warehouse-connection-strings.md
[przepełnienie stosu]: http://stackoverflow.com/questions/tagged/azure-sqldw
[Bilety obsługi]: ./sql-data-warehouse-get-started-create-support-ticket.md
[zabezpieczeń]: ./sql-data-warehouse-overview-manage-security.md
[Compliance Microsoft]: https://www.microsoft.com/en-us/trustcenter/compliance/complianceofferings
[limity pojemności]: ./sql-data-warehouse-service-capacity-limits.md
[typy danych]: ./sql-data-warehouse-tables-data-types.md
[nieobsługiwanych funkcji tabeli]: ./sql-data-warehouse-tables-overview.md#unsupported-table-features
[usługi Azure Data Lake Store]: ./sql-data-warehouse-load-from-azure-data-lake-store.md
[obiektów blob magazynu Azure]: ./sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md
[projektów bazy danych funkcji żądania]: https://feedback.azure.com/forums/307516-sql-data-warehouse/suggestions/13313247-database-project-from-visual-studio-to-support-azu
[MSDN]: https://msdn.microsoft.com/en-us/library/azure/mt163685.aspx
[omówienie]: ./sql-data-warehouse-overview-faq.md