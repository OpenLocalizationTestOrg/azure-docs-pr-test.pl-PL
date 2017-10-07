---
title: "aaaTools do pracy z usługą Azure Storage | Dokumentacja firmy Microsoft"
description: "Lista narzędzi umożliwiających tooview/interakcję z danymi usługi Azure Storage."
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
ms.openlocfilehash: 3308de2153099a05a676ab1d76426bd932e8a96c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-client-tools"></a><span data-ttu-id="afd11-103">Azure Storage Client Tools</span><span class="sxs-lookup"><span data-stu-id="afd11-103">Azure Storage Client Tools</span></span>
<span data-ttu-id="afd11-104">Użytkownicy usługi Azure Storage często mają toobe stanie tooview/interakcję z danymi za pomocą narzędzia klienta usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="afd11-104">Users of Azure Storage frequently want toobe able tooview/interact with their data using an Azure Storage client tool.</span></span> <span data-ttu-id="afd11-105">W poniższych tabelach hello listę wiele narzędzi umożliwiających toodo to.</span><span class="sxs-lookup"><span data-stu-id="afd11-105">In hello tables below, we list a number of tools that allow you toodo this.</span></span> <span data-ttu-id="afd11-106">Testujemy symbol "X" w każdym bloku Jeśli zapewnia możliwość hello tooeither wyliczyć i/lub dostępu hello pozyskiwania danych.</span><span class="sxs-lookup"><span data-stu-id="afd11-106">We put an "X" in each block if it provides hello ability tooeither enumerate and/or access hello data abstraction.</span></span> <span data-ttu-id="afd11-107">Witaj tabeli przedstawiono również, czy narzędzia hello jest bezpłatna.</span><span class="sxs-lookup"><span data-stu-id="afd11-107">hello table also shows if hello tools is free or not.</span></span> <span data-ttu-id="afd11-108">"Wersja próbna" wskazuje istnieje bezpłatna wersja próbna, że produkt w pełnym hello nie ma wolnego.</span><span class="sxs-lookup"><span data-stu-id="afd11-108">"Trial" indicates that there is a free trial, but hello full product is not free.</span></span> <span data-ttu-id="afd11-109">"T/N" wskazuje, że wersja jest dostępna bezpłatnie, gdy inna wersja jest dostępne do zakupu.</span><span class="sxs-lookup"><span data-stu-id="afd11-109">"Y/N" indicates that a version is available for free, while a different version is available for purchase.</span></span>

<span data-ttu-id="afd11-110">Przygotowaliśmy migawki hello dostępnych narzędzi klienta usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="afd11-110">We've only provided a snapshot of hello available Azure Storage client tools.</span></span> <span data-ttu-id="afd11-111">Te narzędzia mogą kontynuować tooevolve i zwiększa się funkcje.</span><span class="sxs-lookup"><span data-stu-id="afd11-111">These tools may continue tooevolve and grow in functionality.</span></span> <span data-ttu-id="afd11-112">Jeśli istnieją poprawki lub aktualizacje, pozostaw toolet komentarz, który nam znać.</span><span class="sxs-lookup"><span data-stu-id="afd11-112">If there are corrections or updates, please leave a comment toolet us know.</span></span> <span data-ttu-id="afd11-113">Hello sam ma wartość true Jeśli wiadomo, narzędzi, które powinno toobe tutaj — będzie mamy przyjemność tooadd je.</span><span class="sxs-lookup"><span data-stu-id="afd11-113">hello same is true if you know of tools that ought toobe here - we'd be happy tooadd them.</span></span>

<span data-ttu-id="afd11-114">**Narzędzia klienta magazynu Microsoft Azure**</span><span class="sxs-lookup"><span data-stu-id="afd11-114">**Microsoft Azure Storage Client Tools**</span></span>

<table>
  <tr>
    <th rowspan="2"><span data-ttu-id="afd11-115">Narzędzie klienta magazynu Azure</span><span class="sxs-lookup"><span data-stu-id="afd11-115">Azure Storage Client Tool</span></span></th>
    <th rowspan="2"><span data-ttu-id="afd11-116">Blokowych obiektów Blob</span><span class="sxs-lookup"><span data-stu-id="afd11-116">Block Blob</span></span></th>
    <th rowspan="2"><span data-ttu-id="afd11-117">Stronicowych obiektów Blob</span><span class="sxs-lookup"><span data-stu-id="afd11-117">Page Blob</span></span></th>
    <th rowspan="2"><span data-ttu-id="afd11-118">Dołącz obiektów Blob</span><span class="sxs-lookup"><span data-stu-id="afd11-118">Append Blob</span></span></th>
    <th rowspan="2"><span data-ttu-id="afd11-119">Tabele</span><span class="sxs-lookup"><span data-stu-id="afd11-119">Tables</span></span></th>
    <th rowspan="2"><span data-ttu-id="afd11-120">Kolejki</span><span class="sxs-lookup"><span data-stu-id="afd11-120">Queues</span></span></th>
    <th rowspan="2"><span data-ttu-id="afd11-121">Pliki</span><span class="sxs-lookup"><span data-stu-id="afd11-121">Files</span></span></th>
    <th rowspan="2"><span data-ttu-id="afd11-122">Bezpłatna</span><span class="sxs-lookup"><span data-stu-id="afd11-122">Free</span></span></th>
    <th colspan="4"><span data-ttu-id="afd11-123">Platforma</span><span class="sxs-lookup"><span data-stu-id="afd11-123">Platform</span></span></th>
  </tr>
  <tr>
    <td><span data-ttu-id="afd11-124">Sieć Web</span><span class="sxs-lookup"><span data-stu-id="afd11-124">Web</span></span></td>
    <td><span data-ttu-id="afd11-125">Windows</span><span class="sxs-lookup"><span data-stu-id="afd11-125">Windows</span></span></td>
    <td><span data-ttu-id="afd11-126">OSX</span><span class="sxs-lookup"><span data-stu-id="afd11-126">OSX</span></span></td>
    <td><span data-ttu-id="afd11-127">Linux</span><span class="sxs-lookup"><span data-stu-id="afd11-127">Linux</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="afd11-128"><a href="https://azure.microsoft.com/features/azure-portal/">Portal Microsoft Azure</a></span><span class="sxs-lookup"><span data-stu-id="afd11-128"><a href="https://azure.microsoft.com/features/azure-portal/">Microsoft Azure Portal</a></span></span></td>
    <td><span data-ttu-id="afd11-129">X</span><span class="sxs-lookup"><span data-stu-id="afd11-129">X</span></span></td>
    <td><span data-ttu-id="afd11-130">X</span><span class="sxs-lookup"><span data-stu-id="afd11-130">X</span></span></td>
    <td><span data-ttu-id="afd11-131">X</span><span class="sxs-lookup"><span data-stu-id="afd11-131">X</span></span></td>
    <td><span data-ttu-id="afd11-132">X</span><span class="sxs-lookup"><span data-stu-id="afd11-132">X</span></span></td>
    <td><span data-ttu-id="afd11-133">X</span><span class="sxs-lookup"><span data-stu-id="afd11-133">X</span></span></td>
    <td><span data-ttu-id="afd11-134">X</span><span class="sxs-lookup"><span data-stu-id="afd11-134">X</span></span></td>
    <td><span data-ttu-id="afd11-135">Tak</span><span class="sxs-lookup"><span data-stu-id="afd11-135">Y</span></span></td>
    <td><span data-ttu-id="afd11-136">X</span><span class="sxs-lookup"><span data-stu-id="afd11-136">X</span></span></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="afd11-137"><a href="http://storageexplorer.com/">Microsoft Azure Storage Explorer</a></span><span class="sxs-lookup"><span data-stu-id="afd11-137"><a href="http://storageexplorer.com/">Microsoft Azure Storage Explorer</a></span></span></td>
    <td><span data-ttu-id="afd11-138">X</span><span class="sxs-lookup"><span data-stu-id="afd11-138">X</span></span></td>
    <td><span data-ttu-id="afd11-139">X</span><span class="sxs-lookup"><span data-stu-id="afd11-139">X</span></span></td>
    <td><span data-ttu-id="afd11-140">X</span><span class="sxs-lookup"><span data-stu-id="afd11-140">X</span></span></td>
    <td><span data-ttu-id="afd11-141">X</span><span class="sxs-lookup"><span data-stu-id="afd11-141">X</span></span></td>
    <td><span data-ttu-id="afd11-142">X</span><span class="sxs-lookup"><span data-stu-id="afd11-142">X</span></span></td>
    <td><span data-ttu-id="afd11-143">X</span><span class="sxs-lookup"><span data-stu-id="afd11-143">X</span></span></td>
    <td><span data-ttu-id="afd11-144">Tak</span><span class="sxs-lookup"><span data-stu-id="afd11-144">Y</span></span></td>
    <td></td>
    <td><span data-ttu-id="afd11-145">X</span><span class="sxs-lookup"><span data-stu-id="afd11-145">X</span></span></td>
    <td><span data-ttu-id="afd11-146">X</span><span class="sxs-lookup"><span data-stu-id="afd11-146">X</span></span></td>
    <td><span data-ttu-id="afd11-147">X</span><span class="sxs-lookup"><span data-stu-id="afd11-147">X</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="afd11-148"><a href="https://www.visualstudio.com/features/azure-tools-vs.aspx">Microsoft Visual Studio w Eksploratorze serwera</a></span><span class="sxs-lookup"><span data-stu-id="afd11-148"><a href="https://www.visualstudio.com/features/azure-tools-vs.aspx">Microsoft Visual Studio Server Explorer</a></span></span></td>
    <td><span data-ttu-id="afd11-149">X</span><span class="sxs-lookup"><span data-stu-id="afd11-149">X</span></span></td>
    <td><span data-ttu-id="afd11-150">X</span><span class="sxs-lookup"><span data-stu-id="afd11-150">X</span></span></td>
    <td><span data-ttu-id="afd11-151">X</span><span class="sxs-lookup"><span data-stu-id="afd11-151">X</span></span></td>
    <td><span data-ttu-id="afd11-152">X</span><span class="sxs-lookup"><span data-stu-id="afd11-152">X</span></span></td>
    <td><span data-ttu-id="afd11-153">X</span><span class="sxs-lookup"><span data-stu-id="afd11-153">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="afd11-154">Tak</span><span class="sxs-lookup"><span data-stu-id="afd11-154">Y</span></span></td>
    <td></td>
    <td><span data-ttu-id="afd11-155">X</span><span class="sxs-lookup"><span data-stu-id="afd11-155">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
</table>

<span data-ttu-id="afd11-156">**Narzędzia klienta magazynu Azure innych firm**</span><span class="sxs-lookup"><span data-stu-id="afd11-156">**Third-Party Azure Storage Client Tools**</span></span>

<span data-ttu-id="afd11-157">Firma Microsoft nie została zweryfikowana, że funkcje hello lub jakości przejęte przez hello narzędzi innych firm i ich lista nie oznacza oznacza, że firma Microsoft.</span><span class="sxs-lookup"><span data-stu-id="afd11-157">We have not verified hello functionality or quality claimed by hello following third-party tools and their listing does not imply an endorsement by Microsoft.</span></span>

<table>
  <tr>
    <th rowspan="2"><span data-ttu-id="afd11-158">Narzędzie klienta magazynu Azure</span><span class="sxs-lookup"><span data-stu-id="afd11-158">Azure Storage Client Tool</span></span></th>
    <th rowspan="2"><span data-ttu-id="afd11-159">Blokowych obiektów Blob</span><span class="sxs-lookup"><span data-stu-id="afd11-159">Block Blob</span></span></th>
    <th rowspan="2"><span data-ttu-id="afd11-160">Stronicowych obiektów Blob</span><span class="sxs-lookup"><span data-stu-id="afd11-160">Page Blob</span></span></th>
    <th rowspan="2"><span data-ttu-id="afd11-161">Dołącz obiektów Blob</span><span class="sxs-lookup"><span data-stu-id="afd11-161">Append Blob</span></span></th>
    <th rowspan="2"><span data-ttu-id="afd11-162">Tabele</span><span class="sxs-lookup"><span data-stu-id="afd11-162">Tables</span></span></th>
    <th rowspan="2"><span data-ttu-id="afd11-163">Kolejki</span><span class="sxs-lookup"><span data-stu-id="afd11-163">Queues</span></span></th>
    <th rowspan="2"><span data-ttu-id="afd11-164">Pliki</span><span class="sxs-lookup"><span data-stu-id="afd11-164">Files</span></span></th>
    <th rowspan="2"><span data-ttu-id="afd11-165">Bezpłatna</span><span class="sxs-lookup"><span data-stu-id="afd11-165">Free</span></span></th>
    <th colspan="4"><span data-ttu-id="afd11-166">Platforma</span><span class="sxs-lookup"><span data-stu-id="afd11-166">Platform</span></span></th>
  </tr>
  <tr>
    <td><span data-ttu-id="afd11-167">Sieć Web</span><span class="sxs-lookup"><span data-stu-id="afd11-167">Web</span></span></td>
    <td><span data-ttu-id="afd11-168">Windows</span><span class="sxs-lookup"><span data-stu-id="afd11-168">Windows</span></span></td>
    <td><span data-ttu-id="afd11-169">OSX</span><span class="sxs-lookup"><span data-stu-id="afd11-169">OSX</span></span></td>
    <td><span data-ttu-id="afd11-170">Linux</span><span class="sxs-lookup"><span data-stu-id="afd11-170">Linux</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="afd11-171"><a href="http://www.cloudportam.com/">Portam chmury</a></span><span class="sxs-lookup"><span data-stu-id="afd11-171"><a href="http://www.cloudportam.com/">Cloud Portam</a></span></span></td>
    <td><span data-ttu-id="afd11-172">X</span><span class="sxs-lookup"><span data-stu-id="afd11-172">X</span></span></td>
    <td><span data-ttu-id="afd11-173">X</span><span class="sxs-lookup"><span data-stu-id="afd11-173">X</span></span></td>
    <td><span data-ttu-id="afd11-174">X</span><span class="sxs-lookup"><span data-stu-id="afd11-174">X</span></span></td>
    <td><span data-ttu-id="afd11-175">X</span><span class="sxs-lookup"><span data-stu-id="afd11-175">X</span></span></td>
    <td><span data-ttu-id="afd11-176">X</span><span class="sxs-lookup"><span data-stu-id="afd11-176">X</span></span></td>
    <td><span data-ttu-id="afd11-177">X</span><span class="sxs-lookup"><span data-stu-id="afd11-177">X</span></span></td>
    <td><span data-ttu-id="afd11-178">Wersja próbna</span><span class="sxs-lookup"><span data-stu-id="afd11-178">Trial</span></span></td>
    <td><span data-ttu-id="afd11-179">X</span><span class="sxs-lookup"><span data-stu-id="afd11-179">X</span></span></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="afd11-180"><a href="http://www.cerebrata.com/products/azure-management-studio/introduction">Cerabrata: Azure Management Studio</a></span><span class="sxs-lookup"><span data-stu-id="afd11-180"><a href="http://www.cerebrata.com/products/azure-management-studio/introduction">Cerabrata: Azure Management Studio</a></span></span></td>
    <td><span data-ttu-id="afd11-181">X</span><span class="sxs-lookup"><span data-stu-id="afd11-181">X</span></span></td>
    <td><span data-ttu-id="afd11-182">X</span><span class="sxs-lookup"><span data-stu-id="afd11-182">X</span></span></td>
    <td><span data-ttu-id="afd11-183">X</span><span class="sxs-lookup"><span data-stu-id="afd11-183">X</span></span></td>
    <td><span data-ttu-id="afd11-184">X</span><span class="sxs-lookup"><span data-stu-id="afd11-184">X</span></span></td>
    <td><span data-ttu-id="afd11-185">X</span><span class="sxs-lookup"><span data-stu-id="afd11-185">X</span></span></td>
    <td><span data-ttu-id="afd11-186">X</span><span class="sxs-lookup"><span data-stu-id="afd11-186">X</span></span></td>
    <td><span data-ttu-id="afd11-187">Wersja próbna</span><span class="sxs-lookup"><span data-stu-id="afd11-187">Trial</span></span></td>
    <td></td>
    <td><span data-ttu-id="afd11-188">X</span><span class="sxs-lookup"><span data-stu-id="afd11-188">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="afd11-189"><a href="http://www.cerebrata.com/products/azure-explorer/introduction">Cerabrata: Eksplorator Azure</a></span><span class="sxs-lookup"><span data-stu-id="afd11-189"><a href="http://www.cerebrata.com/products/azure-explorer/introduction">Cerabrata: Azure Explorer</a></span></span></td>
    <td><span data-ttu-id="afd11-190">X</span><span class="sxs-lookup"><span data-stu-id="afd11-190">X</span></span></td>
    <td><span data-ttu-id="afd11-191">X</span><span class="sxs-lookup"><span data-stu-id="afd11-191">X</span></span></td>
    <td><span data-ttu-id="afd11-192">X</span><span class="sxs-lookup"><span data-stu-id="afd11-192">X</span></span></td>
    <td></td>
    <td></td>
    <td><span data-ttu-id="afd11-193">X</span><span class="sxs-lookup"><span data-stu-id="afd11-193">X</span></span></td>
    <td><span data-ttu-id="afd11-194">Tak</span><span class="sxs-lookup"><span data-stu-id="afd11-194">Y</span></span></td>
    <td></td>
    <td><span data-ttu-id="afd11-195">X</span><span class="sxs-lookup"><span data-stu-id="afd11-195">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="afd11-196"><a href="https://github.com/sebagomez/azurestorageexplorer">Azure Storage Explorer</a></span><span class="sxs-lookup"><span data-stu-id="afd11-196"><a href="https://github.com/sebagomez/azurestorageexplorer">Azure Storage Explorer</a></span></span></td>
    <td><span data-ttu-id="afd11-197">X</span><span class="sxs-lookup"><span data-stu-id="afd11-197">X</span></span></td>
    <td><span data-ttu-id="afd11-198">X</span><span class="sxs-lookup"><span data-stu-id="afd11-198">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="afd11-199">X</span><span class="sxs-lookup"><span data-stu-id="afd11-199">X</span></span></td>
    <td><span data-ttu-id="afd11-200">X</span><span class="sxs-lookup"><span data-stu-id="afd11-200">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="afd11-201">Tak</span><span class="sxs-lookup"><span data-stu-id="afd11-201">Y</span></span></td>
    <td></td>
    <td><span data-ttu-id="afd11-202">X</span><span class="sxs-lookup"><span data-stu-id="afd11-202">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="afd11-203"><a href="http://www.cloudberrylab.com/free-microsoft-azure-explorer.aspx">Eksplorator cloudBerry</a></span><span class="sxs-lookup"><span data-stu-id="afd11-203"><a href="http://www.cloudberrylab.com/free-microsoft-azure-explorer.aspx">CloudBerry Explorer</a></span></span></td>
    <td><span data-ttu-id="afd11-204">X</span><span class="sxs-lookup"><span data-stu-id="afd11-204">X</span></span></td>
    <td><span data-ttu-id="afd11-205">X</span><span class="sxs-lookup"><span data-stu-id="afd11-205">X</span></span></td>
    <td></td>
    <td></td>
    <td></td>
    <td><span data-ttu-id="afd11-206">X</span><span class="sxs-lookup"><span data-stu-id="afd11-206">X</span></span></td>
    <td><span data-ttu-id="afd11-207">T/N</span><span class="sxs-lookup"><span data-stu-id="afd11-207">Y/N</span></span></td>
    <td></td>
    <td><span data-ttu-id="afd11-208">X</span><span class="sxs-lookup"><span data-stu-id="afd11-208">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="afd11-209"><a href="http://www.gapotchenko.com/cloudcombine">Łączenie w chmurze</a></span><span class="sxs-lookup"><span data-stu-id="afd11-209"><a href="http://www.gapotchenko.com/cloudcombine">Cloud Combine</a></span></span></td>
    <td><span data-ttu-id="afd11-210">X</span><span class="sxs-lookup"><span data-stu-id="afd11-210">X</span></span></td>
    <td><span data-ttu-id="afd11-211">X</span><span class="sxs-lookup"><span data-stu-id="afd11-211">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="afd11-212">X</span><span class="sxs-lookup"><span data-stu-id="afd11-212">X</span></span></td>
    <td><span data-ttu-id="afd11-213">X</span><span class="sxs-lookup"><span data-stu-id="afd11-213">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="afd11-214">Wersja próbna</span><span class="sxs-lookup"><span data-stu-id="afd11-214">Trial</span></span></td>
    <td></td>
    <td><span data-ttu-id="afd11-215">X</span><span class="sxs-lookup"><span data-stu-id="afd11-215">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="afd11-216"><a href="http://clumsyleaf.com">ClumsyLeaf: TableXplorer AzureXplorer, CloudXplorer,</a></span><span class="sxs-lookup"><span data-stu-id="afd11-216"><a href="http://clumsyleaf.com">ClumsyLeaf: AzureXplorer, CloudXplorer, TableXplorer</a></span></span></td>
    <td><span data-ttu-id="afd11-217">X</span><span class="sxs-lookup"><span data-stu-id="afd11-217">X</span></span></td>
    <td><span data-ttu-id="afd11-218">X</span><span class="sxs-lookup"><span data-stu-id="afd11-218">X</span></span></td>
    <td><span data-ttu-id="afd11-219">X</span><span class="sxs-lookup"><span data-stu-id="afd11-219">X</span></span></td>
    <td><span data-ttu-id="afd11-220">X</span><span class="sxs-lookup"><span data-stu-id="afd11-220">X</span></span></td>
    <td><span data-ttu-id="afd11-221">X</span><span class="sxs-lookup"><span data-stu-id="afd11-221">X</span></span></td>
    <td><span data-ttu-id="afd11-222">X</span><span class="sxs-lookup"><span data-stu-id="afd11-222">X</span></span></td>
    <td><span data-ttu-id="afd11-223">Tak</span><span class="sxs-lookup"><span data-stu-id="afd11-223">Y</span></span></td>
    <td></td>
    <td><span data-ttu-id="afd11-224">X</span><span class="sxs-lookup"><span data-stu-id="afd11-224">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="afd11-225"><a href="http://www.gladinet.com/Azure-Storage/index.htm">Gladinet chmury</a></span><span class="sxs-lookup"><span data-stu-id="afd11-225"><a href="http://www.gladinet.com/Azure-Storage/index.htm">Gladinet Cloud</a></span></span></td>
    <td><span data-ttu-id="afd11-226">X</span><span class="sxs-lookup"><span data-stu-id="afd11-226">X</span></span></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td><span data-ttu-id="afd11-227">Wersja próbna</span><span class="sxs-lookup"><span data-stu-id="afd11-227">Trial</span></span></td>
    <td></td>
    <td><span data-ttu-id="afd11-228">X</span><span class="sxs-lookup"><span data-stu-id="afd11-228">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="afd11-229"><a href="http://storageexplorer.codeplex.com/">Eksplorator usługi sieci Web platformy Azure Storage</a></span><span class="sxs-lookup"><span data-stu-id="afd11-229"><a href="http://storageexplorer.codeplex.com/">Azure Web Storage Explorer</a></span></span></td>
    <td><span data-ttu-id="afd11-230">X</span><span class="sxs-lookup"><span data-stu-id="afd11-230">X</span></span></td>
    <td><span data-ttu-id="afd11-231">X</span><span class="sxs-lookup"><span data-stu-id="afd11-231">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="afd11-232">X</span><span class="sxs-lookup"><span data-stu-id="afd11-232">X</span></span></td>
    <td><span data-ttu-id="afd11-233">X</span><span class="sxs-lookup"><span data-stu-id="afd11-233">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="afd11-234">Tak</span><span class="sxs-lookup"><span data-stu-id="afd11-234">Y</span></span></td>
    <td><span data-ttu-id="afd11-235">X</span><span class="sxs-lookup"><span data-stu-id="afd11-235">X</span></span></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="afd11-236"><a href="https://zudio.co/">Zudio</a></span><span class="sxs-lookup"><span data-stu-id="afd11-236"><a href="https://zudio.co/">Zudio</a></span></span></td>
    <td><span data-ttu-id="afd11-237">X</span><span class="sxs-lookup"><span data-stu-id="afd11-237">X</span></span></td>
    <td><span data-ttu-id="afd11-238">X</span><span class="sxs-lookup"><span data-stu-id="afd11-238">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="afd11-239">X</span><span class="sxs-lookup"><span data-stu-id="afd11-239">X</span></span></td>
    <td><span data-ttu-id="afd11-240">X</span><span class="sxs-lookup"><span data-stu-id="afd11-240">X</span></span></td>
    <td><span data-ttu-id="afd11-241">X</span><span class="sxs-lookup"><span data-stu-id="afd11-241">X</span></span></td>
    <td><span data-ttu-id="afd11-242">Wersja próbna</span><span class="sxs-lookup"><span data-stu-id="afd11-242">Trial</span></span></td>
    <td><span data-ttu-id="afd11-243">X</span><span class="sxs-lookup"><span data-stu-id="afd11-243">X</span></span></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
</table>
