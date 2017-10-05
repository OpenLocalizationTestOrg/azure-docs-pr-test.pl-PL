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
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="azure-storage-client-tools"></a><span data-ttu-id="dcba9-103">Azure Storage Client Tools</span><span class="sxs-lookup"><span data-stu-id="dcba9-103">Azure Storage Client Tools</span></span>
<span data-ttu-id="dcba9-104">Użytkownicy usługi Azure Storage często ma być możliwe do widoku/interakcji z danymi za pomocą narzędzia klienta usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="dcba9-104">Users of Azure Storage frequently want to be able to view/interact with their data using an Azure Storage client tool.</span></span> <span data-ttu-id="dcba9-105">W poniższych tabelach na listę wiele narzędzi, dzięki którym można to zrobić.</span><span class="sxs-lookup"><span data-stu-id="dcba9-105">In the tables below, we list a number of tools that allow you to do this.</span></span> <span data-ttu-id="dcba9-106">Testujemy symbol "X" w każdym bloku, jeśli zapewnia możliwość albo wyliczyć i/lub uzyskać dostępu do pozyskiwania danych.</span><span class="sxs-lookup"><span data-stu-id="dcba9-106">We put an "X" in each block if it provides the ability to either enumerate and/or access the data abstraction.</span></span> <span data-ttu-id="dcba9-107">W tabeli przedstawiono również, czy narzędzia jest bezpłatna.</span><span class="sxs-lookup"><span data-stu-id="dcba9-107">The table also shows if the tools is free or not.</span></span> <span data-ttu-id="dcba9-108">"W wersji próbnej" wskazuje, czy istnieje bezpłatna wersja próbna, ale nie ma wolnego produkt w pełnym.</span><span class="sxs-lookup"><span data-stu-id="dcba9-108">"Trial" indicates that there is a free trial, but the full product is not free.</span></span> <span data-ttu-id="dcba9-109">"T/N" wskazuje, że wersja jest dostępna bezpłatnie, gdy inna wersja jest dostępne do zakupu.</span><span class="sxs-lookup"><span data-stu-id="dcba9-109">"Y/N" indicates that a version is available for free, while a different version is available for purchase.</span></span>

<span data-ttu-id="dcba9-110">Przygotowaliśmy migawki dostępnych narzędzi klienta usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="dcba9-110">We've only provided a snapshot of the available Azure Storage client tools.</span></span> <span data-ttu-id="dcba9-111">Te narzędzia mogą nadal ewoluują i zwiększa się funkcje.</span><span class="sxs-lookup"><span data-stu-id="dcba9-111">These tools may continue to evolve and grow in functionality.</span></span> <span data-ttu-id="dcba9-112">Jeśli istnieją poprawki lub aktualizacje, zostaw komentarz, aby poinformować nas.</span><span class="sxs-lookup"><span data-stu-id="dcba9-112">If there are corrections or updates, please leave a comment to let us know.</span></span> <span data-ttu-id="dcba9-113">Jest taka sama wartość true, jeśli znasz narzędzia, które powinny być tutaj — firma Microsoft będzie chętnie je dodać.</span><span class="sxs-lookup"><span data-stu-id="dcba9-113">The same is true if you know of tools that ought to be here - we'd be happy to add them.</span></span>

<span data-ttu-id="dcba9-114">**Narzędzia klienta magazynu Microsoft Azure**</span><span class="sxs-lookup"><span data-stu-id="dcba9-114">**Microsoft Azure Storage Client Tools**</span></span>

<table>
  <tr>
    <th rowspan="2"><span data-ttu-id="dcba9-115">Narzędzie klienta magazynu Azure</span><span class="sxs-lookup"><span data-stu-id="dcba9-115">Azure Storage Client Tool</span></span></th>
    <th rowspan="2"><span data-ttu-id="dcba9-116">Blokowych obiektów Blob</span><span class="sxs-lookup"><span data-stu-id="dcba9-116">Block Blob</span></span></th>
    <th rowspan="2"><span data-ttu-id="dcba9-117">Stronicowych obiektów Blob</span><span class="sxs-lookup"><span data-stu-id="dcba9-117">Page Blob</span></span></th>
    <th rowspan="2"><span data-ttu-id="dcba9-118">Dołącz obiektów Blob</span><span class="sxs-lookup"><span data-stu-id="dcba9-118">Append Blob</span></span></th>
    <th rowspan="2"><span data-ttu-id="dcba9-119">Tabele</span><span class="sxs-lookup"><span data-stu-id="dcba9-119">Tables</span></span></th>
    <th rowspan="2"><span data-ttu-id="dcba9-120">Kolejki</span><span class="sxs-lookup"><span data-stu-id="dcba9-120">Queues</span></span></th>
    <th rowspan="2"><span data-ttu-id="dcba9-121">Pliki</span><span class="sxs-lookup"><span data-stu-id="dcba9-121">Files</span></span></th>
    <th rowspan="2"><span data-ttu-id="dcba9-122">Bezpłatna</span><span class="sxs-lookup"><span data-stu-id="dcba9-122">Free</span></span></th>
    <th colspan="4"><span data-ttu-id="dcba9-123">Platforma</span><span class="sxs-lookup"><span data-stu-id="dcba9-123">Platform</span></span></th>
  </tr>
  <tr>
    <td><span data-ttu-id="dcba9-124">Sieć Web</span><span class="sxs-lookup"><span data-stu-id="dcba9-124">Web</span></span></td>
    <td><span data-ttu-id="dcba9-125">Windows</span><span class="sxs-lookup"><span data-stu-id="dcba9-125">Windows</span></span></td>
    <td><span data-ttu-id="dcba9-126">OSX</span><span class="sxs-lookup"><span data-stu-id="dcba9-126">OSX</span></span></td>
    <td><span data-ttu-id="dcba9-127">Linux</span><span class="sxs-lookup"><span data-stu-id="dcba9-127">Linux</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="dcba9-128"><a href="https://azure.microsoft.com/features/azure-portal/">Portal Microsoft Azure</a></span><span class="sxs-lookup"><span data-stu-id="dcba9-128"><a href="https://azure.microsoft.com/features/azure-portal/">Microsoft Azure Portal</a></span></span></td>
    <td><span data-ttu-id="dcba9-129">X</span><span class="sxs-lookup"><span data-stu-id="dcba9-129">X</span></span></td>
    <td><span data-ttu-id="dcba9-130">X</span><span class="sxs-lookup"><span data-stu-id="dcba9-130">X</span></span></td>
    <td><span data-ttu-id="dcba9-131">X</span><span class="sxs-lookup"><span data-stu-id="dcba9-131">X</span></span></td>
    <td><span data-ttu-id="dcba9-132">X</span><span class="sxs-lookup"><span data-stu-id="dcba9-132">X</span></span></td>
    <td><span data-ttu-id="dcba9-133">X</span><span class="sxs-lookup"><span data-stu-id="dcba9-133">X</span></span></td>
    <td><span data-ttu-id="dcba9-134">X</span><span class="sxs-lookup"><span data-stu-id="dcba9-134">X</span></span></td>
    <td><span data-ttu-id="dcba9-135">Tak</span><span class="sxs-lookup"><span data-stu-id="dcba9-135">Y</span></span></td>
    <td><span data-ttu-id="dcba9-136">X</span><span class="sxs-lookup"><span data-stu-id="dcba9-136">X</span></span></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="dcba9-137"><a href="http://storageexplorer.com/">Microsoft Azure Storage Explorer</a></span><span class="sxs-lookup"><span data-stu-id="dcba9-137"><a href="http://storageexplorer.com/">Microsoft Azure Storage Explorer</a></span></span></td>
    <td><span data-ttu-id="dcba9-138">X</span><span class="sxs-lookup"><span data-stu-id="dcba9-138">X</span></span></td>
    <td><span data-ttu-id="dcba9-139">X</span><span class="sxs-lookup"><span data-stu-id="dcba9-139">X</span></span></td>
    <td><span data-ttu-id="dcba9-140">X</span><span class="sxs-lookup"><span data-stu-id="dcba9-140">X</span></span></td>
    <td><span data-ttu-id="dcba9-141">X</span><span class="sxs-lookup"><span data-stu-id="dcba9-141">X</span></span></td>
    <td><span data-ttu-id="dcba9-142">X</span><span class="sxs-lookup"><span data-stu-id="dcba9-142">X</span></span></td>
    <td><span data-ttu-id="dcba9-143">X</span><span class="sxs-lookup"><span data-stu-id="dcba9-143">X</span></span></td>
    <td><span data-ttu-id="dcba9-144">Tak</span><span class="sxs-lookup"><span data-stu-id="dcba9-144">Y</span></span></td>
    <td></td>
    <td><span data-ttu-id="dcba9-145">X</span><span class="sxs-lookup"><span data-stu-id="dcba9-145">X</span></span></td>
    <td><span data-ttu-id="dcba9-146">X</span><span class="sxs-lookup"><span data-stu-id="dcba9-146">X</span></span></td>
    <td><span data-ttu-id="dcba9-147">X</span><span class="sxs-lookup"><span data-stu-id="dcba9-147">X</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="dcba9-148"><a href="https://www.visualstudio.com/features/azure-tools-vs.aspx">Microsoft Visual Studio w Eksploratorze serwera</a></span><span class="sxs-lookup"><span data-stu-id="dcba9-148"><a href="https://www.visualstudio.com/features/azure-tools-vs.aspx">Microsoft Visual Studio Server Explorer</a></span></span></td>
    <td><span data-ttu-id="dcba9-149">X</span><span class="sxs-lookup"><span data-stu-id="dcba9-149">X</span></span></td>
    <td><span data-ttu-id="dcba9-150">X</span><span class="sxs-lookup"><span data-stu-id="dcba9-150">X</span></span></td>
    <td><span data-ttu-id="dcba9-151">X</span><span class="sxs-lookup"><span data-stu-id="dcba9-151">X</span></span></td>
    <td><span data-ttu-id="dcba9-152">X</span><span class="sxs-lookup"><span data-stu-id="dcba9-152">X</span></span></td>
    <td><span data-ttu-id="dcba9-153">X</span><span class="sxs-lookup"><span data-stu-id="dcba9-153">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="dcba9-154">Tak</span><span class="sxs-lookup"><span data-stu-id="dcba9-154">Y</span></span></td>
    <td></td>
    <td><span data-ttu-id="dcba9-155">X</span><span class="sxs-lookup"><span data-stu-id="dcba9-155">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
</table>

<span data-ttu-id="dcba9-156">**Narzędzia klienta magazynu Azure innych firm**</span><span class="sxs-lookup"><span data-stu-id="dcba9-156">**Third-Party Azure Storage Client Tools**</span></span>

<span data-ttu-id="dcba9-157">Firma Microsoft nie została zweryfikowana funkcji lub jakości przejęte przez następujących narzędzi innych firm, a ich lista nie oznacza potwierdzenia przez firmę Microsoft.</span><span class="sxs-lookup"><span data-stu-id="dcba9-157">We have not verified the functionality or quality claimed by the following third-party tools and their listing does not imply an endorsement by Microsoft.</span></span>

<table>
  <tr>
    <th rowspan="2"><span data-ttu-id="dcba9-158">Narzędzie klienta magazynu Azure</span><span class="sxs-lookup"><span data-stu-id="dcba9-158">Azure Storage Client Tool</span></span></th>
    <th rowspan="2"><span data-ttu-id="dcba9-159">Blokowych obiektów Blob</span><span class="sxs-lookup"><span data-stu-id="dcba9-159">Block Blob</span></span></th>
    <th rowspan="2"><span data-ttu-id="dcba9-160">Stronicowych obiektów Blob</span><span class="sxs-lookup"><span data-stu-id="dcba9-160">Page Blob</span></span></th>
    <th rowspan="2"><span data-ttu-id="dcba9-161">Dołącz obiektów Blob</span><span class="sxs-lookup"><span data-stu-id="dcba9-161">Append Blob</span></span></th>
    <th rowspan="2"><span data-ttu-id="dcba9-162">Tabele</span><span class="sxs-lookup"><span data-stu-id="dcba9-162">Tables</span></span></th>
    <th rowspan="2"><span data-ttu-id="dcba9-163">Kolejki</span><span class="sxs-lookup"><span data-stu-id="dcba9-163">Queues</span></span></th>
    <th rowspan="2"><span data-ttu-id="dcba9-164">Pliki</span><span class="sxs-lookup"><span data-stu-id="dcba9-164">Files</span></span></th>
    <th rowspan="2"><span data-ttu-id="dcba9-165">Bezpłatna</span><span class="sxs-lookup"><span data-stu-id="dcba9-165">Free</span></span></th>
    <th colspan="4"><span data-ttu-id="dcba9-166">Platforma</span><span class="sxs-lookup"><span data-stu-id="dcba9-166">Platform</span></span></th>
  </tr>
  <tr>
    <td><span data-ttu-id="dcba9-167">Sieć Web</span><span class="sxs-lookup"><span data-stu-id="dcba9-167">Web</span></span></td>
    <td><span data-ttu-id="dcba9-168">Windows</span><span class="sxs-lookup"><span data-stu-id="dcba9-168">Windows</span></span></td>
    <td><span data-ttu-id="dcba9-169">OSX</span><span class="sxs-lookup"><span data-stu-id="dcba9-169">OSX</span></span></td>
    <td><span data-ttu-id="dcba9-170">Linux</span><span class="sxs-lookup"><span data-stu-id="dcba9-170">Linux</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="dcba9-171"><a href="http://www.cloudportam.com/">Portam chmury</a></span><span class="sxs-lookup"><span data-stu-id="dcba9-171"><a href="http://www.cloudportam.com/">Cloud Portam</a></span></span></td>
    <td><span data-ttu-id="dcba9-172">X</span><span class="sxs-lookup"><span data-stu-id="dcba9-172">X</span></span></td>
    <td><span data-ttu-id="dcba9-173">X</span><span class="sxs-lookup"><span data-stu-id="dcba9-173">X</span></span></td>
    <td><span data-ttu-id="dcba9-174">X</span><span class="sxs-lookup"><span data-stu-id="dcba9-174">X</span></span></td>
    <td><span data-ttu-id="dcba9-175">X</span><span class="sxs-lookup"><span data-stu-id="dcba9-175">X</span></span></td>
    <td><span data-ttu-id="dcba9-176">X</span><span class="sxs-lookup"><span data-stu-id="dcba9-176">X</span></span></td>
    <td><span data-ttu-id="dcba9-177">X</span><span class="sxs-lookup"><span data-stu-id="dcba9-177">X</span></span></td>
    <td><span data-ttu-id="dcba9-178">Wersja próbna</span><span class="sxs-lookup"><span data-stu-id="dcba9-178">Trial</span></span></td>
    <td><span data-ttu-id="dcba9-179">X</span><span class="sxs-lookup"><span data-stu-id="dcba9-179">X</span></span></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="dcba9-180"><a href="http://www.cerebrata.com/products/azure-management-studio/introduction">Cerabrata: Azure Management Studio</a></span><span class="sxs-lookup"><span data-stu-id="dcba9-180"><a href="http://www.cerebrata.com/products/azure-management-studio/introduction">Cerabrata: Azure Management Studio</a></span></span></td>
    <td><span data-ttu-id="dcba9-181">X</span><span class="sxs-lookup"><span data-stu-id="dcba9-181">X</span></span></td>
    <td><span data-ttu-id="dcba9-182">X</span><span class="sxs-lookup"><span data-stu-id="dcba9-182">X</span></span></td>
    <td><span data-ttu-id="dcba9-183">X</span><span class="sxs-lookup"><span data-stu-id="dcba9-183">X</span></span></td>
    <td><span data-ttu-id="dcba9-184">X</span><span class="sxs-lookup"><span data-stu-id="dcba9-184">X</span></span></td>
    <td><span data-ttu-id="dcba9-185">X</span><span class="sxs-lookup"><span data-stu-id="dcba9-185">X</span></span></td>
    <td><span data-ttu-id="dcba9-186">X</span><span class="sxs-lookup"><span data-stu-id="dcba9-186">X</span></span></td>
    <td><span data-ttu-id="dcba9-187">Wersja próbna</span><span class="sxs-lookup"><span data-stu-id="dcba9-187">Trial</span></span></td>
    <td></td>
    <td><span data-ttu-id="dcba9-188">X</span><span class="sxs-lookup"><span data-stu-id="dcba9-188">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="dcba9-189"><a href="http://www.cerebrata.com/products/azure-explorer/introduction">Cerabrata: Eksplorator Azure</a></span><span class="sxs-lookup"><span data-stu-id="dcba9-189"><a href="http://www.cerebrata.com/products/azure-explorer/introduction">Cerabrata: Azure Explorer</a></span></span></td>
    <td><span data-ttu-id="dcba9-190">X</span><span class="sxs-lookup"><span data-stu-id="dcba9-190">X</span></span></td>
    <td><span data-ttu-id="dcba9-191">X</span><span class="sxs-lookup"><span data-stu-id="dcba9-191">X</span></span></td>
    <td><span data-ttu-id="dcba9-192">X</span><span class="sxs-lookup"><span data-stu-id="dcba9-192">X</span></span></td>
    <td></td>
    <td></td>
    <td><span data-ttu-id="dcba9-193">X</span><span class="sxs-lookup"><span data-stu-id="dcba9-193">X</span></span></td>
    <td><span data-ttu-id="dcba9-194">Tak</span><span class="sxs-lookup"><span data-stu-id="dcba9-194">Y</span></span></td>
    <td></td>
    <td><span data-ttu-id="dcba9-195">X</span><span class="sxs-lookup"><span data-stu-id="dcba9-195">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="dcba9-196"><a href="https://github.com/sebagomez/azurestorageexplorer">Azure Storage Explorer</a></span><span class="sxs-lookup"><span data-stu-id="dcba9-196"><a href="https://github.com/sebagomez/azurestorageexplorer">Azure Storage Explorer</a></span></span></td>
    <td><span data-ttu-id="dcba9-197">X</span><span class="sxs-lookup"><span data-stu-id="dcba9-197">X</span></span></td>
    <td><span data-ttu-id="dcba9-198">X</span><span class="sxs-lookup"><span data-stu-id="dcba9-198">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="dcba9-199">X</span><span class="sxs-lookup"><span data-stu-id="dcba9-199">X</span></span></td>
    <td><span data-ttu-id="dcba9-200">X</span><span class="sxs-lookup"><span data-stu-id="dcba9-200">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="dcba9-201">Tak</span><span class="sxs-lookup"><span data-stu-id="dcba9-201">Y</span></span></td>
    <td></td>
    <td><span data-ttu-id="dcba9-202">X</span><span class="sxs-lookup"><span data-stu-id="dcba9-202">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="dcba9-203"><a href="http://www.cloudberrylab.com/free-microsoft-azure-explorer.aspx">Eksplorator cloudBerry</a></span><span class="sxs-lookup"><span data-stu-id="dcba9-203"><a href="http://www.cloudberrylab.com/free-microsoft-azure-explorer.aspx">CloudBerry Explorer</a></span></span></td>
    <td><span data-ttu-id="dcba9-204">X</span><span class="sxs-lookup"><span data-stu-id="dcba9-204">X</span></span></td>
    <td><span data-ttu-id="dcba9-205">X</span><span class="sxs-lookup"><span data-stu-id="dcba9-205">X</span></span></td>
    <td></td>
    <td></td>
    <td></td>
    <td><span data-ttu-id="dcba9-206">X</span><span class="sxs-lookup"><span data-stu-id="dcba9-206">X</span></span></td>
    <td><span data-ttu-id="dcba9-207">T/N</span><span class="sxs-lookup"><span data-stu-id="dcba9-207">Y/N</span></span></td>
    <td></td>
    <td><span data-ttu-id="dcba9-208">X</span><span class="sxs-lookup"><span data-stu-id="dcba9-208">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="dcba9-209"><a href="http://www.gapotchenko.com/cloudcombine">Łączenie w chmurze</a></span><span class="sxs-lookup"><span data-stu-id="dcba9-209"><a href="http://www.gapotchenko.com/cloudcombine">Cloud Combine</a></span></span></td>
    <td><span data-ttu-id="dcba9-210">X</span><span class="sxs-lookup"><span data-stu-id="dcba9-210">X</span></span></td>
    <td><span data-ttu-id="dcba9-211">X</span><span class="sxs-lookup"><span data-stu-id="dcba9-211">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="dcba9-212">X</span><span class="sxs-lookup"><span data-stu-id="dcba9-212">X</span></span></td>
    <td><span data-ttu-id="dcba9-213">X</span><span class="sxs-lookup"><span data-stu-id="dcba9-213">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="dcba9-214">Wersja próbna</span><span class="sxs-lookup"><span data-stu-id="dcba9-214">Trial</span></span></td>
    <td></td>
    <td><span data-ttu-id="dcba9-215">X</span><span class="sxs-lookup"><span data-stu-id="dcba9-215">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="dcba9-216"><a href="http://clumsyleaf.com">ClumsyLeaf: TableXplorer AzureXplorer, CloudXplorer,</a></span><span class="sxs-lookup"><span data-stu-id="dcba9-216"><a href="http://clumsyleaf.com">ClumsyLeaf: AzureXplorer, CloudXplorer, TableXplorer</a></span></span></td>
    <td><span data-ttu-id="dcba9-217">X</span><span class="sxs-lookup"><span data-stu-id="dcba9-217">X</span></span></td>
    <td><span data-ttu-id="dcba9-218">X</span><span class="sxs-lookup"><span data-stu-id="dcba9-218">X</span></span></td>
    <td><span data-ttu-id="dcba9-219">X</span><span class="sxs-lookup"><span data-stu-id="dcba9-219">X</span></span></td>
    <td><span data-ttu-id="dcba9-220">X</span><span class="sxs-lookup"><span data-stu-id="dcba9-220">X</span></span></td>
    <td><span data-ttu-id="dcba9-221">X</span><span class="sxs-lookup"><span data-stu-id="dcba9-221">X</span></span></td>
    <td><span data-ttu-id="dcba9-222">X</span><span class="sxs-lookup"><span data-stu-id="dcba9-222">X</span></span></td>
    <td><span data-ttu-id="dcba9-223">Tak</span><span class="sxs-lookup"><span data-stu-id="dcba9-223">Y</span></span></td>
    <td></td>
    <td><span data-ttu-id="dcba9-224">X</span><span class="sxs-lookup"><span data-stu-id="dcba9-224">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="dcba9-225"><a href="http://www.gladinet.com/Azure-Storage/index.htm">Gladinet chmury</a></span><span class="sxs-lookup"><span data-stu-id="dcba9-225"><a href="http://www.gladinet.com/Azure-Storage/index.htm">Gladinet Cloud</a></span></span></td>
    <td><span data-ttu-id="dcba9-226">X</span><span class="sxs-lookup"><span data-stu-id="dcba9-226">X</span></span></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td><span data-ttu-id="dcba9-227">Wersja próbna</span><span class="sxs-lookup"><span data-stu-id="dcba9-227">Trial</span></span></td>
    <td></td>
    <td><span data-ttu-id="dcba9-228">X</span><span class="sxs-lookup"><span data-stu-id="dcba9-228">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="dcba9-229"><a href="http://storageexplorer.codeplex.com/">Eksplorator usługi sieci Web platformy Azure Storage</a></span><span class="sxs-lookup"><span data-stu-id="dcba9-229"><a href="http://storageexplorer.codeplex.com/">Azure Web Storage Explorer</a></span></span></td>
    <td><span data-ttu-id="dcba9-230">X</span><span class="sxs-lookup"><span data-stu-id="dcba9-230">X</span></span></td>
    <td><span data-ttu-id="dcba9-231">X</span><span class="sxs-lookup"><span data-stu-id="dcba9-231">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="dcba9-232">X</span><span class="sxs-lookup"><span data-stu-id="dcba9-232">X</span></span></td>
    <td><span data-ttu-id="dcba9-233">X</span><span class="sxs-lookup"><span data-stu-id="dcba9-233">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="dcba9-234">Tak</span><span class="sxs-lookup"><span data-stu-id="dcba9-234">Y</span></span></td>
    <td><span data-ttu-id="dcba9-235">X</span><span class="sxs-lookup"><span data-stu-id="dcba9-235">X</span></span></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="dcba9-236"><a href="https://zudio.co/">Zudio</a></span><span class="sxs-lookup"><span data-stu-id="dcba9-236"><a href="https://zudio.co/">Zudio</a></span></span></td>
    <td><span data-ttu-id="dcba9-237">X</span><span class="sxs-lookup"><span data-stu-id="dcba9-237">X</span></span></td>
    <td><span data-ttu-id="dcba9-238">X</span><span class="sxs-lookup"><span data-stu-id="dcba9-238">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="dcba9-239">X</span><span class="sxs-lookup"><span data-stu-id="dcba9-239">X</span></span></td>
    <td><span data-ttu-id="dcba9-240">X</span><span class="sxs-lookup"><span data-stu-id="dcba9-240">X</span></span></td>
    <td><span data-ttu-id="dcba9-241">X</span><span class="sxs-lookup"><span data-stu-id="dcba9-241">X</span></span></td>
    <td><span data-ttu-id="dcba9-242">Wersja próbna</span><span class="sxs-lookup"><span data-stu-id="dcba9-242">Trial</span></span></td>
    <td><span data-ttu-id="dcba9-243">X</span><span class="sxs-lookup"><span data-stu-id="dcba9-243">X</span></span></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
</table>
