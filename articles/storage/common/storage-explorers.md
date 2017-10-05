---
title: "Narzędzia do pracy z usługą Azure Storage | Dokumentacja firmy Microsoft"
description: "Lista narzędzi, które umożliwiają wyświetlanie/interakcję z danymi usługi Azure Storage."
services: storage
documentationcenter: 
author: dineshmurthy
manager: jahogg
editor: tysonn
ms.assetid: e4748642-98c4-437e-b0ed-4f9641c2e894
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: dineshmurthy
ms.openlocfilehash: 620efda06d8225b21b6bb9b104b79061ebb6515c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="azure-storage-client-tools"></a><span data-ttu-id="1473f-103">Azure Storage Client Tools</span><span class="sxs-lookup"><span data-stu-id="1473f-103">Azure Storage Client Tools</span></span>
<span data-ttu-id="1473f-104">Użytkownicy usługi Azure Storage często ma być możliwe do widoku/interakcji z danymi za pomocą narzędzia klienta usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="1473f-104">Users of Azure Storage frequently want to be able to view/interact with their data using an Azure Storage client tool.</span></span> <span data-ttu-id="1473f-105">W poniższych tabelach na listę wiele narzędzi, dzięki którym można to zrobić.</span><span class="sxs-lookup"><span data-stu-id="1473f-105">In the tables below, we list a number of tools that allow you to do this.</span></span> <span data-ttu-id="1473f-106">Testujemy symbol "X" w każdym bloku, jeśli zapewnia możliwość albo wyliczyć i/lub uzyskać dostępu do pozyskiwania danych.</span><span class="sxs-lookup"><span data-stu-id="1473f-106">We put an "X" in each block if it provides the ability to either enumerate and/or access the data abstraction.</span></span> <span data-ttu-id="1473f-107">W tabeli przedstawiono również, czy narzędzia jest bezpłatna.</span><span class="sxs-lookup"><span data-stu-id="1473f-107">The table also shows if the tools is free or not.</span></span> <span data-ttu-id="1473f-108">"W wersji próbnej" wskazuje, czy istnieje bezpłatna wersja próbna, ale nie ma wolnego produkt w pełnym.</span><span class="sxs-lookup"><span data-stu-id="1473f-108">"Trial" indicates that there is a free trial, but the full product is not free.</span></span> <span data-ttu-id="1473f-109">"T/N" wskazuje, że wersja jest dostępna bezpłatnie, gdy inna wersja jest dostępne do zakupu.</span><span class="sxs-lookup"><span data-stu-id="1473f-109">"Y/N" indicates that a version is available for free, while a different version is available for purchase.</span></span>

<span data-ttu-id="1473f-110">Przygotowaliśmy migawki dostępnych narzędzi klienta usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="1473f-110">We've only provided a snapshot of the available Azure Storage client tools.</span></span> <span data-ttu-id="1473f-111">Te narzędzia mogą nadal ewoluują i zwiększa się funkcje.</span><span class="sxs-lookup"><span data-stu-id="1473f-111">These tools may continue to evolve and grow in functionality.</span></span> <span data-ttu-id="1473f-112">Jeśli istnieją poprawki lub aktualizacje, zostaw komentarz, aby poinformować nas.</span><span class="sxs-lookup"><span data-stu-id="1473f-112">If there are corrections or updates, please leave a comment to let us know.</span></span> <span data-ttu-id="1473f-113">Jest taka sama wartość true, jeśli znasz narzędzia, które powinny być tutaj — firma Microsoft będzie chętnie je dodać.</span><span class="sxs-lookup"><span data-stu-id="1473f-113">The same is true if you know of tools that ought to be here - we'd be happy to add them.</span></span>

<span data-ttu-id="1473f-114">**Narzędzia klienta magazynu Microsoft Azure**</span><span class="sxs-lookup"><span data-stu-id="1473f-114">**Microsoft Azure Storage Client Tools**</span></span>

<table>
  <tr>
    <th rowspan="2"><span data-ttu-id="1473f-115">Narzędzie klienta magazynu Azure</span><span class="sxs-lookup"><span data-stu-id="1473f-115">Azure Storage Client Tool</span></span></th>
    <th rowspan="2"><span data-ttu-id="1473f-116">Blokowych obiektów Blob</span><span class="sxs-lookup"><span data-stu-id="1473f-116">Block Blob</span></span></th>
    <th rowspan="2"><span data-ttu-id="1473f-117">Stronicowych obiektów Blob</span><span class="sxs-lookup"><span data-stu-id="1473f-117">Page Blob</span></span></th>
    <th rowspan="2"><span data-ttu-id="1473f-118">Dołącz obiektów Blob</span><span class="sxs-lookup"><span data-stu-id="1473f-118">Append Blob</span></span></th>
    <th rowspan="2"><span data-ttu-id="1473f-119">Tabele</span><span class="sxs-lookup"><span data-stu-id="1473f-119">Tables</span></span></th>
    <th rowspan="2"><span data-ttu-id="1473f-120">Kolejki</span><span class="sxs-lookup"><span data-stu-id="1473f-120">Queues</span></span></th>
    <th rowspan="2"><span data-ttu-id="1473f-121">Pliki</span><span class="sxs-lookup"><span data-stu-id="1473f-121">Files</span></span></th>
    <th rowspan="2"><span data-ttu-id="1473f-122">Bezpłatna</span><span class="sxs-lookup"><span data-stu-id="1473f-122">Free</span></span></th>
    <th colspan="4"><span data-ttu-id="1473f-123">Platforma</span><span class="sxs-lookup"><span data-stu-id="1473f-123">Platform</span></span></th>
  </tr>
  <tr>
    <td><span data-ttu-id="1473f-124">Sieć Web</span><span class="sxs-lookup"><span data-stu-id="1473f-124">Web</span></span></td>
    <td><span data-ttu-id="1473f-125">Windows</span><span class="sxs-lookup"><span data-stu-id="1473f-125">Windows</span></span></td>
    <td><span data-ttu-id="1473f-126">OSX</span><span class="sxs-lookup"><span data-stu-id="1473f-126">OSX</span></span></td>
    <td><span data-ttu-id="1473f-127">Linux</span><span class="sxs-lookup"><span data-stu-id="1473f-127">Linux</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="1473f-128"><a href="https://azure.microsoft.com/features/azure-portal/">Portal Microsoft Azure</a></span><span class="sxs-lookup"><span data-stu-id="1473f-128"><a href="https://azure.microsoft.com/features/azure-portal/">Microsoft Azure Portal</a></span></span></td>
    <td><span data-ttu-id="1473f-129">X</span><span class="sxs-lookup"><span data-stu-id="1473f-129">X</span></span></td>
    <td><span data-ttu-id="1473f-130">X</span><span class="sxs-lookup"><span data-stu-id="1473f-130">X</span></span></td>
    <td><span data-ttu-id="1473f-131">X</span><span class="sxs-lookup"><span data-stu-id="1473f-131">X</span></span></td>
    <td><span data-ttu-id="1473f-132">X</span><span class="sxs-lookup"><span data-stu-id="1473f-132">X</span></span></td>
    <td><span data-ttu-id="1473f-133">X</span><span class="sxs-lookup"><span data-stu-id="1473f-133">X</span></span></td>
    <td><span data-ttu-id="1473f-134">X</span><span class="sxs-lookup"><span data-stu-id="1473f-134">X</span></span></td>
    <td><span data-ttu-id="1473f-135">Tak</span><span class="sxs-lookup"><span data-stu-id="1473f-135">Y</span></span></td>
    <td><span data-ttu-id="1473f-136">X</span><span class="sxs-lookup"><span data-stu-id="1473f-136">X</span></span></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="1473f-137"><a href="http://storageexplorer.com/">Microsoft Azure Storage Explorer</a></span><span class="sxs-lookup"><span data-stu-id="1473f-137"><a href="http://storageexplorer.com/">Microsoft Azure Storage Explorer</a></span></span></td>
    <td><span data-ttu-id="1473f-138">X</span><span class="sxs-lookup"><span data-stu-id="1473f-138">X</span></span></td>
    <td><span data-ttu-id="1473f-139">X</span><span class="sxs-lookup"><span data-stu-id="1473f-139">X</span></span></td>
    <td><span data-ttu-id="1473f-140">X</span><span class="sxs-lookup"><span data-stu-id="1473f-140">X</span></span></td>
    <td><span data-ttu-id="1473f-141">X</span><span class="sxs-lookup"><span data-stu-id="1473f-141">X</span></span></td>
    <td><span data-ttu-id="1473f-142">X</span><span class="sxs-lookup"><span data-stu-id="1473f-142">X</span></span></td>
    <td><span data-ttu-id="1473f-143">X</span><span class="sxs-lookup"><span data-stu-id="1473f-143">X</span></span></td>
    <td><span data-ttu-id="1473f-144">Tak</span><span class="sxs-lookup"><span data-stu-id="1473f-144">Y</span></span></td>
    <td></td>
    <td><span data-ttu-id="1473f-145">X</span><span class="sxs-lookup"><span data-stu-id="1473f-145">X</span></span></td>
    <td><span data-ttu-id="1473f-146">X</span><span class="sxs-lookup"><span data-stu-id="1473f-146">X</span></span></td>
    <td><span data-ttu-id="1473f-147">X</span><span class="sxs-lookup"><span data-stu-id="1473f-147">X</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="1473f-148"><a href="https://www.visualstudio.com/features/azure-tools-vs.aspx">Microsoft Visual Studio w Eksploratorze serwera</a></span><span class="sxs-lookup"><span data-stu-id="1473f-148"><a href="https://www.visualstudio.com/features/azure-tools-vs.aspx">Microsoft Visual Studio Server Explorer</a></span></span></td>
    <td><span data-ttu-id="1473f-149">X</span><span class="sxs-lookup"><span data-stu-id="1473f-149">X</span></span></td>
    <td><span data-ttu-id="1473f-150">X</span><span class="sxs-lookup"><span data-stu-id="1473f-150">X</span></span></td>
    <td><span data-ttu-id="1473f-151">X</span><span class="sxs-lookup"><span data-stu-id="1473f-151">X</span></span></td>
    <td><span data-ttu-id="1473f-152">X</span><span class="sxs-lookup"><span data-stu-id="1473f-152">X</span></span></td>
    <td><span data-ttu-id="1473f-153">X</span><span class="sxs-lookup"><span data-stu-id="1473f-153">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="1473f-154">Tak</span><span class="sxs-lookup"><span data-stu-id="1473f-154">Y</span></span></td>
    <td></td>
    <td><span data-ttu-id="1473f-155">X</span><span class="sxs-lookup"><span data-stu-id="1473f-155">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
</table>

<span data-ttu-id="1473f-156">**Narzędzia klienta magazynu Azure innych firm**</span><span class="sxs-lookup"><span data-stu-id="1473f-156">**Third-Party Azure Storage Client Tools**</span></span>

<span data-ttu-id="1473f-157">Firma Microsoft nie została zweryfikowana funkcji lub jakości przejęte przez następujących narzędzi innych firm, a ich lista nie oznacza potwierdzenia przez firmę Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1473f-157">We have not verified the functionality or quality claimed by the following third-party tools and their listing does not imply an endorsement by Microsoft.</span></span>

<table>
  <tr>
    <th rowspan="2"><span data-ttu-id="1473f-158">Narzędzie klienta magazynu Azure</span><span class="sxs-lookup"><span data-stu-id="1473f-158">Azure Storage Client Tool</span></span></th>
    <th rowspan="2"><span data-ttu-id="1473f-159">Blokowych obiektów Blob</span><span class="sxs-lookup"><span data-stu-id="1473f-159">Block Blob</span></span></th>
    <th rowspan="2"><span data-ttu-id="1473f-160">Stronicowych obiektów Blob</span><span class="sxs-lookup"><span data-stu-id="1473f-160">Page Blob</span></span></th>
    <th rowspan="2"><span data-ttu-id="1473f-161">Dołącz obiektów Blob</span><span class="sxs-lookup"><span data-stu-id="1473f-161">Append Blob</span></span></th>
    <th rowspan="2"><span data-ttu-id="1473f-162">Tabele</span><span class="sxs-lookup"><span data-stu-id="1473f-162">Tables</span></span></th>
    <th rowspan="2"><span data-ttu-id="1473f-163">Kolejki</span><span class="sxs-lookup"><span data-stu-id="1473f-163">Queues</span></span></th>
    <th rowspan="2"><span data-ttu-id="1473f-164">Pliki</span><span class="sxs-lookup"><span data-stu-id="1473f-164">Files</span></span></th>
    <th rowspan="2"><span data-ttu-id="1473f-165">Bezpłatna</span><span class="sxs-lookup"><span data-stu-id="1473f-165">Free</span></span></th>
    <th colspan="4"><span data-ttu-id="1473f-166">Platforma</span><span class="sxs-lookup"><span data-stu-id="1473f-166">Platform</span></span></th>
  </tr>
  <tr>
    <td><span data-ttu-id="1473f-167">Sieć Web</span><span class="sxs-lookup"><span data-stu-id="1473f-167">Web</span></span></td>
    <td><span data-ttu-id="1473f-168">Windows</span><span class="sxs-lookup"><span data-stu-id="1473f-168">Windows</span></span></td>
    <td><span data-ttu-id="1473f-169">OSX</span><span class="sxs-lookup"><span data-stu-id="1473f-169">OSX</span></span></td>
    <td><span data-ttu-id="1473f-170">Linux</span><span class="sxs-lookup"><span data-stu-id="1473f-170">Linux</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="1473f-171"><a href="http://www.cloudportam.com/">Portam chmury</a></span><span class="sxs-lookup"><span data-stu-id="1473f-171"><a href="http://www.cloudportam.com/">Cloud Portam</a></span></span></td>
    <td><span data-ttu-id="1473f-172">X</span><span class="sxs-lookup"><span data-stu-id="1473f-172">X</span></span></td>
    <td><span data-ttu-id="1473f-173">X</span><span class="sxs-lookup"><span data-stu-id="1473f-173">X</span></span></td>
    <td><span data-ttu-id="1473f-174">X</span><span class="sxs-lookup"><span data-stu-id="1473f-174">X</span></span></td>
    <td><span data-ttu-id="1473f-175">X</span><span class="sxs-lookup"><span data-stu-id="1473f-175">X</span></span></td>
    <td><span data-ttu-id="1473f-176">X</span><span class="sxs-lookup"><span data-stu-id="1473f-176">X</span></span></td>
    <td><span data-ttu-id="1473f-177">X</span><span class="sxs-lookup"><span data-stu-id="1473f-177">X</span></span></td>
    <td><span data-ttu-id="1473f-178">Wersja próbna</span><span class="sxs-lookup"><span data-stu-id="1473f-178">Trial</span></span></td>
    <td><span data-ttu-id="1473f-179">X</span><span class="sxs-lookup"><span data-stu-id="1473f-179">X</span></span></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="1473f-180"><a href="http://www.cerebrata.com/products/azure-management-studio/introduction">Cerabrata: Azure Management Studio</a></span><span class="sxs-lookup"><span data-stu-id="1473f-180"><a href="http://www.cerebrata.com/products/azure-management-studio/introduction">Cerabrata: Azure Management Studio</a></span></span></td>
    <td><span data-ttu-id="1473f-181">X</span><span class="sxs-lookup"><span data-stu-id="1473f-181">X</span></span></td>
    <td><span data-ttu-id="1473f-182">X</span><span class="sxs-lookup"><span data-stu-id="1473f-182">X</span></span></td>
    <td><span data-ttu-id="1473f-183">X</span><span class="sxs-lookup"><span data-stu-id="1473f-183">X</span></span></td>
    <td><span data-ttu-id="1473f-184">X</span><span class="sxs-lookup"><span data-stu-id="1473f-184">X</span></span></td>
    <td><span data-ttu-id="1473f-185">X</span><span class="sxs-lookup"><span data-stu-id="1473f-185">X</span></span></td>
    <td><span data-ttu-id="1473f-186">X</span><span class="sxs-lookup"><span data-stu-id="1473f-186">X</span></span></td>
    <td><span data-ttu-id="1473f-187">Wersja próbna</span><span class="sxs-lookup"><span data-stu-id="1473f-187">Trial</span></span></td>
    <td></td>
    <td><span data-ttu-id="1473f-188">X</span><span class="sxs-lookup"><span data-stu-id="1473f-188">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="1473f-189"><a href="http://www.cerebrata.com/products/azure-explorer/introduction">Cerabrata: Eksplorator Azure</a></span><span class="sxs-lookup"><span data-stu-id="1473f-189"><a href="http://www.cerebrata.com/products/azure-explorer/introduction">Cerabrata: Azure Explorer</a></span></span></td>
    <td><span data-ttu-id="1473f-190">X</span><span class="sxs-lookup"><span data-stu-id="1473f-190">X</span></span></td>
    <td><span data-ttu-id="1473f-191">X</span><span class="sxs-lookup"><span data-stu-id="1473f-191">X</span></span></td>
    <td><span data-ttu-id="1473f-192">X</span><span class="sxs-lookup"><span data-stu-id="1473f-192">X</span></span></td>
    <td></td>
    <td></td>
    <td><span data-ttu-id="1473f-193">X</span><span class="sxs-lookup"><span data-stu-id="1473f-193">X</span></span></td>
    <td><span data-ttu-id="1473f-194">Tak</span><span class="sxs-lookup"><span data-stu-id="1473f-194">Y</span></span></td>
    <td></td>
    <td><span data-ttu-id="1473f-195">X</span><span class="sxs-lookup"><span data-stu-id="1473f-195">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="1473f-196"><a href="https://github.com/sebagomez/azurestorageexplorer">Azure Storage Explorer</a></span><span class="sxs-lookup"><span data-stu-id="1473f-196"><a href="https://github.com/sebagomez/azurestorageexplorer">Azure Storage Explorer</a></span></span></td>
    <td><span data-ttu-id="1473f-197">X</span><span class="sxs-lookup"><span data-stu-id="1473f-197">X</span></span></td>
    <td><span data-ttu-id="1473f-198">X</span><span class="sxs-lookup"><span data-stu-id="1473f-198">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="1473f-199">X</span><span class="sxs-lookup"><span data-stu-id="1473f-199">X</span></span></td>
    <td><span data-ttu-id="1473f-200">X</span><span class="sxs-lookup"><span data-stu-id="1473f-200">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="1473f-201">Tak</span><span class="sxs-lookup"><span data-stu-id="1473f-201">Y</span></span></td>
    <td></td>
    <td><span data-ttu-id="1473f-202">X</span><span class="sxs-lookup"><span data-stu-id="1473f-202">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="1473f-203"><a href="http://www.cloudberrylab.com/free-microsoft-azure-explorer.aspx">Eksplorator cloudBerry</a></span><span class="sxs-lookup"><span data-stu-id="1473f-203"><a href="http://www.cloudberrylab.com/free-microsoft-azure-explorer.aspx">CloudBerry Explorer</a></span></span></td>
    <td><span data-ttu-id="1473f-204">X</span><span class="sxs-lookup"><span data-stu-id="1473f-204">X</span></span></td>
    <td><span data-ttu-id="1473f-205">X</span><span class="sxs-lookup"><span data-stu-id="1473f-205">X</span></span></td>
    <td></td>
    <td></td>
    <td></td>
    <td><span data-ttu-id="1473f-206">X</span><span class="sxs-lookup"><span data-stu-id="1473f-206">X</span></span></td>
    <td><span data-ttu-id="1473f-207">T/N</span><span class="sxs-lookup"><span data-stu-id="1473f-207">Y/N</span></span></td>
    <td></td>
    <td><span data-ttu-id="1473f-208">X</span><span class="sxs-lookup"><span data-stu-id="1473f-208">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="1473f-209"><a href="http://www.gapotchenko.com/cloudcombine">Łączenie w chmurze</a></span><span class="sxs-lookup"><span data-stu-id="1473f-209"><a href="http://www.gapotchenko.com/cloudcombine">Cloud Combine</a></span></span></td>
    <td><span data-ttu-id="1473f-210">X</span><span class="sxs-lookup"><span data-stu-id="1473f-210">X</span></span></td>
    <td><span data-ttu-id="1473f-211">X</span><span class="sxs-lookup"><span data-stu-id="1473f-211">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="1473f-212">X</span><span class="sxs-lookup"><span data-stu-id="1473f-212">X</span></span></td>
    <td><span data-ttu-id="1473f-213">X</span><span class="sxs-lookup"><span data-stu-id="1473f-213">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="1473f-214">Wersja próbna</span><span class="sxs-lookup"><span data-stu-id="1473f-214">Trial</span></span></td>
    <td></td>
    <td><span data-ttu-id="1473f-215">X</span><span class="sxs-lookup"><span data-stu-id="1473f-215">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="1473f-216"><a href="http://clumsyleaf.com">ClumsyLeaf: TableXplorer AzureXplorer, CloudXplorer,</a></span><span class="sxs-lookup"><span data-stu-id="1473f-216"><a href="http://clumsyleaf.com">ClumsyLeaf: AzureXplorer, CloudXplorer, TableXplorer</a></span></span></td>
    <td><span data-ttu-id="1473f-217">X</span><span class="sxs-lookup"><span data-stu-id="1473f-217">X</span></span></td>
    <td><span data-ttu-id="1473f-218">X</span><span class="sxs-lookup"><span data-stu-id="1473f-218">X</span></span></td>
    <td><span data-ttu-id="1473f-219">X</span><span class="sxs-lookup"><span data-stu-id="1473f-219">X</span></span></td>
    <td><span data-ttu-id="1473f-220">X</span><span class="sxs-lookup"><span data-stu-id="1473f-220">X</span></span></td>
    <td><span data-ttu-id="1473f-221">X</span><span class="sxs-lookup"><span data-stu-id="1473f-221">X</span></span></td>
    <td><span data-ttu-id="1473f-222">X</span><span class="sxs-lookup"><span data-stu-id="1473f-222">X</span></span></td>
    <td><span data-ttu-id="1473f-223">Tak</span><span class="sxs-lookup"><span data-stu-id="1473f-223">Y</span></span></td>
    <td></td>
    <td><span data-ttu-id="1473f-224">X</span><span class="sxs-lookup"><span data-stu-id="1473f-224">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="1473f-225"><a href="http://www.gladinet.com/Azure-Storage/index.htm">Gladinet chmury</a></span><span class="sxs-lookup"><span data-stu-id="1473f-225"><a href="http://www.gladinet.com/Azure-Storage/index.htm">Gladinet Cloud</a></span></span></td>
    <td><span data-ttu-id="1473f-226">X</span><span class="sxs-lookup"><span data-stu-id="1473f-226">X</span></span></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td><span data-ttu-id="1473f-227">Wersja próbna</span><span class="sxs-lookup"><span data-stu-id="1473f-227">Trial</span></span></td>
    <td></td>
    <td><span data-ttu-id="1473f-228">X</span><span class="sxs-lookup"><span data-stu-id="1473f-228">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="1473f-229"><a href="http://storageexplorer.codeplex.com/">Eksplorator usługi sieci Web platformy Azure Storage</a></span><span class="sxs-lookup"><span data-stu-id="1473f-229"><a href="http://storageexplorer.codeplex.com/">Azure Web Storage Explorer</a></span></span></td>
    <td><span data-ttu-id="1473f-230">X</span><span class="sxs-lookup"><span data-stu-id="1473f-230">X</span></span></td>
    <td><span data-ttu-id="1473f-231">X</span><span class="sxs-lookup"><span data-stu-id="1473f-231">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="1473f-232">X</span><span class="sxs-lookup"><span data-stu-id="1473f-232">X</span></span></td>
    <td><span data-ttu-id="1473f-233">X</span><span class="sxs-lookup"><span data-stu-id="1473f-233">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="1473f-234">Tak</span><span class="sxs-lookup"><span data-stu-id="1473f-234">Y</span></span></td>
    <td><span data-ttu-id="1473f-235">X</span><span class="sxs-lookup"><span data-stu-id="1473f-235">X</span></span></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="1473f-236"><a href="https://zudio.co/">Zudio</a></span><span class="sxs-lookup"><span data-stu-id="1473f-236"><a href="https://zudio.co/">Zudio</a></span></span></td>
    <td><span data-ttu-id="1473f-237">X</span><span class="sxs-lookup"><span data-stu-id="1473f-237">X</span></span></td>
    <td><span data-ttu-id="1473f-238">X</span><span class="sxs-lookup"><span data-stu-id="1473f-238">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="1473f-239">X</span><span class="sxs-lookup"><span data-stu-id="1473f-239">X</span></span></td>
    <td><span data-ttu-id="1473f-240">X</span><span class="sxs-lookup"><span data-stu-id="1473f-240">X</span></span></td>
    <td><span data-ttu-id="1473f-241">X</span><span class="sxs-lookup"><span data-stu-id="1473f-241">X</span></span></td>
    <td><span data-ttu-id="1473f-242">Wersja próbna</span><span class="sxs-lookup"><span data-stu-id="1473f-242">Trial</span></span></td>
    <td><span data-ttu-id="1473f-243">X</span><span class="sxs-lookup"><span data-stu-id="1473f-243">X</span></span></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
</table>
