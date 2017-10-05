---
title: "Obsługiwane źródeł danych w usłudze Azure Data Catalog | Dokumentacja firmy Microsoft"
description: "W tym artykule wymieniono specyfikacje aktualnie obsługiwanych źródeł danych."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: jstevens
editor: 
tags: 
ms.assetid: fd4345ca-2ed8-4c5e-9c4b-f954be2fc9f9
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: d6867c73bc6ea3c238cceef8a68466d451f3365c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="supported-data-sources-in-azure-data-catalog"></a><span data-ttu-id="980af-103">Obsługiwanych źródeł danych w wykazie danych Azure</span><span class="sxs-lookup"><span data-stu-id="980af-103">Supported data sources in Azure Data Catalog</span></span>

<span data-ttu-id="980af-104">Metadane można opublikować za pomocą publiczny interfejs API lub przez kliknięcie — po rejestracji narzędzie, lub ręcznie wprowadzić informacje bezpośrednio do usługi Azure Data Catalog sieci web portalu.</span><span class="sxs-lookup"><span data-stu-id="980af-104">You can publish metadata by using a public API or a click-once registration tool, or by manually entering information directly to the Azure Data Catalog web portal.</span></span> <span data-ttu-id="980af-105">Poniższa tabela zawiera podsumowanie wszystkich źródeł danych, które są obsługiwane przez katalog, w obecnie oraz możliwości publikowania dla każdego.</span><span class="sxs-lookup"><span data-stu-id="980af-105">The following table summarizes all data sources that are supported by the catalog today, and the publishing capabilities for each.</span></span> <span data-ttu-id="980af-106">Liście są również narzędzia danych zewnętrznych, które każdego źródła danych można uruchomić na naszym doświadczeniu portal "Otwórz w".</span><span class="sxs-lookup"><span data-stu-id="980af-106">Also listed are the external data tools that each data source can launch from our portal "open-in" experience.</span></span> <span data-ttu-id="980af-107">Druga tabela zawiera specyfikację techniczne każdej właściwości połączenia źródła danych.</span><span class="sxs-lookup"><span data-stu-id="980af-107">The second table contains a more technical specification of each data-source connection property.</span></span>


## <a name="list-of-supported-data-sources"></a><span data-ttu-id="980af-108">Listę obsługiwanych źródeł danych</span><span class="sxs-lookup"><span data-stu-id="980af-108">List of supported data sources</span></span>

<table>
    <tr>
       <td><span data-ttu-id="980af-109"><b>Obiekt źródła danych</b></span><span class="sxs-lookup"><span data-stu-id="980af-109"><b>Data source object</b></span></span></td>
       <td><span data-ttu-id="980af-110"><b>Interfejs API</b></span><span class="sxs-lookup"><span data-stu-id="980af-110"><b>API</b></span></span></td>
       <td><span data-ttu-id="980af-111"><b>Ręczne wprowadzanie</b></span><span class="sxs-lookup"><span data-stu-id="980af-111"><b>Manual entry</b></span></span></td>
       <td><span data-ttu-id="980af-112"><b>Narzędzie do rejestracji</b></span><span class="sxs-lookup"><span data-stu-id="980af-112"><b>Registration tool</b></span></span></td>
       <td><span data-ttu-id="980af-113"><b>Otwórz w narzędziach</b></span><span class="sxs-lookup"><span data-stu-id="980af-113"><b>Open-in tools</b></span></span></td>
       <td><span data-ttu-id="980af-114"><b>Uwagi</b></span><span class="sxs-lookup"><span data-stu-id="980af-114"><b>Notes</b></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-115">Katalog usługi Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="980af-115">Azure Data Lake Store directory</span></span></td>
      <td><span data-ttu-id="980af-116">✓</span><span class="sxs-lookup"><span data-stu-id="980af-116">✓</span></span></td>
      <td><span data-ttu-id="980af-117">✓</span><span class="sxs-lookup"><span data-stu-id="980af-117">✓</span></span></td>
      <td><span data-ttu-id="980af-118">✓</span><span class="sxs-lookup"><span data-stu-id="980af-118">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-119">Azure Data Lake — magazyn plików</span><span class="sxs-lookup"><span data-stu-id="980af-119">Azure Data Lake Store file</span></span></td>
      <td><span data-ttu-id="980af-120">✓</span><span class="sxs-lookup"><span data-stu-id="980af-120">✓</span></span></td>
      <td><span data-ttu-id="980af-121">✓</span><span class="sxs-lookup"><span data-stu-id="980af-121">✓</span></span></td>
      <td><span data-ttu-id="980af-122">✓</span><span class="sxs-lookup"><span data-stu-id="980af-122">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-123">Azure Blob Storage</span><span class="sxs-lookup"><span data-stu-id="980af-123">Azure Blob storage</span></span></td>
      <td><span data-ttu-id="980af-124">✓</span><span class="sxs-lookup"><span data-stu-id="980af-124">✓</span></span></td>
      <td><span data-ttu-id="980af-125">✓</span><span class="sxs-lookup"><span data-stu-id="980af-125">✓</span></span></td>
      <td><span data-ttu-id="980af-126">✓</span><span class="sxs-lookup"><span data-stu-id="980af-126">✓</span></span></td>
      <td><span data-ttu-id="980af-127"><font size=2>Power BI</font></span><span class="sxs-lookup"><span data-stu-id="980af-127"><font size=2>Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-128">Katalog magazynu Azure</span><span class="sxs-lookup"><span data-stu-id="980af-128">Azure Storage directory</span></span></td>
      <td><span data-ttu-id="980af-129">✓</span><span class="sxs-lookup"><span data-stu-id="980af-129">✓</span></span></td>
      <td><span data-ttu-id="980af-130">✓</span><span class="sxs-lookup"><span data-stu-id="980af-130">✓</span></span></td>
      <td><span data-ttu-id="980af-131">✓</span><span class="sxs-lookup"><span data-stu-id="980af-131">✓</span></span></td>
      <td><span data-ttu-id="980af-132"><font size=2>Power BI</font></span><span class="sxs-lookup"><span data-stu-id="980af-132"><font size=2>Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-133">Tabela magazynu Azure</span><span class="sxs-lookup"><span data-stu-id="980af-133">Azure Storage table</span></span></td>
      <td><span data-ttu-id="980af-134">✓</span><span class="sxs-lookup"><span data-stu-id="980af-134">✓</span></span></td>
      <td><span data-ttu-id="980af-135">✓</span><span class="sxs-lookup"><span data-stu-id="980af-135">✓</span></span></td>
      <td><span data-ttu-id="980af-136">✓</span><span class="sxs-lookup"><span data-stu-id="980af-136">✓</span></span></td>
      <td>
        <font size="2"></font>
      </td>
      <td>
        <font size="2"></font>
      </td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-137">Katalog systemu plików HDFS</span><span class="sxs-lookup"><span data-stu-id="980af-137">HDFS directory</span></span></td>
      <td><span data-ttu-id="980af-138">✓</span><span class="sxs-lookup"><span data-stu-id="980af-138">✓</span></span></td>
      <td><span data-ttu-id="980af-139">✓</span><span class="sxs-lookup"><span data-stu-id="980af-139">✓</span></span></td>
      <td><span data-ttu-id="980af-140">✓</span><span class="sxs-lookup"><span data-stu-id="980af-140">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-141">System plików HDFS pliku</span><span class="sxs-lookup"><span data-stu-id="980af-141">HDFS file</span></span></td>
      <td><span data-ttu-id="980af-142">✓</span><span class="sxs-lookup"><span data-stu-id="980af-142">✓</span></span></td>
      <td><span data-ttu-id="980af-143">✓</span><span class="sxs-lookup"><span data-stu-id="980af-143">✓</span></span></td>
      <td><span data-ttu-id="980af-144">✓</span><span class="sxs-lookup"><span data-stu-id="980af-144">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-145">Tabelę programu hive</span><span class="sxs-lookup"><span data-stu-id="980af-145">Hive table</span></span></td>
      <td><span data-ttu-id="980af-146">✓</span><span class="sxs-lookup"><span data-stu-id="980af-146">✓</span></span></td>
      <td><span data-ttu-id="980af-147">✓</span><span class="sxs-lookup"><span data-stu-id="980af-147">✓</span></span></td>
      <td><span data-ttu-id="980af-148">✓</span><span class="sxs-lookup"><span data-stu-id="980af-148">✓</span></span></td>
      <td><span data-ttu-id="980af-149"><font size=2>Excel</font></span><span class="sxs-lookup"><span data-stu-id="980af-149"><font size=2>Excel</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-150">Widok gałęzi</span><span class="sxs-lookup"><span data-stu-id="980af-150">Hive view</span></span></td>
      <td><span data-ttu-id="980af-151">✓</span><span class="sxs-lookup"><span data-stu-id="980af-151">✓</span></span></td>
      <td><span data-ttu-id="980af-152">✓</span><span class="sxs-lookup"><span data-stu-id="980af-152">✓</span></span></td>
      <td><span data-ttu-id="980af-153">✓</span><span class="sxs-lookup"><span data-stu-id="980af-153">✓</span></span></td>
      <td><span data-ttu-id="980af-154"><font size=2>Excel</font></span><span class="sxs-lookup"><span data-stu-id="980af-154"><font size=2>Excel</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-155">Tabela MySQL</span><span class="sxs-lookup"><span data-stu-id="980af-155">MySQL table</span></span></td>
      <td><span data-ttu-id="980af-156">✓</span><span class="sxs-lookup"><span data-stu-id="980af-156">✓</span></span></td>
      <td><span data-ttu-id="980af-157">✓</span><span class="sxs-lookup"><span data-stu-id="980af-157">✓</span></span></td>
      <td><span data-ttu-id="980af-158">✓</span><span class="sxs-lookup"><span data-stu-id="980af-158">✓</span></span></td>
      <td><span data-ttu-id="980af-159"><font size=2>Program Excel, usłudze Power BI</font></span><span class="sxs-lookup"><span data-stu-id="980af-159"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-160">Widok MySQL</span><span class="sxs-lookup"><span data-stu-id="980af-160">MySQL view</span></span></td>
      <td><span data-ttu-id="980af-161">✓</span><span class="sxs-lookup"><span data-stu-id="980af-161">✓</span></span></td>
      <td><span data-ttu-id="980af-162">✓</span><span class="sxs-lookup"><span data-stu-id="980af-162">✓</span></span></td>
      <td><span data-ttu-id="980af-163">✓</span><span class="sxs-lookup"><span data-stu-id="980af-163">✓</span></span></td>
      <td><span data-ttu-id="980af-164"><font size=2>Program Excel, usłudze Power BI</font></span><span class="sxs-lookup"><span data-stu-id="980af-164"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-165">Tabela bazy danych programu Oracle</span><span class="sxs-lookup"><span data-stu-id="980af-165">Oracle Database table</span></span></td>
      <td><span data-ttu-id="980af-166">✓</span><span class="sxs-lookup"><span data-stu-id="980af-166">✓</span></span></td>
      <td><span data-ttu-id="980af-167">✓</span><span class="sxs-lookup"><span data-stu-id="980af-167">✓</span></span></td>
      <td><span data-ttu-id="980af-168">✓</span><span class="sxs-lookup"><span data-stu-id="980af-168">✓</span></span></td>
      <td><span data-ttu-id="980af-169"><font size=2>Program Excel, usłudze Power BI</font></span><span class="sxs-lookup"><span data-stu-id="980af-169"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-170">Widok bazy danych programu Oracle</span><span class="sxs-lookup"><span data-stu-id="980af-170">Oracle Database view</span></span></td>
      <td><span data-ttu-id="980af-171">✓</span><span class="sxs-lookup"><span data-stu-id="980af-171">✓</span></span></td>
      <td><span data-ttu-id="980af-172">✓</span><span class="sxs-lookup"><span data-stu-id="980af-172">✓</span></span></td>
      <td><span data-ttu-id="980af-173">✓</span><span class="sxs-lookup"><span data-stu-id="980af-173">✓</span></span></td>
      <td><span data-ttu-id="980af-174"><font size=2>Program Excel, usłudze Power BI</font></span><span class="sxs-lookup"><span data-stu-id="980af-174"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-175">Inne (ogólnego zasobów)</span><span class="sxs-lookup"><span data-stu-id="980af-175">Other (generic asset)</span></span></td>
      <td><span data-ttu-id="980af-176">✓</span><span class="sxs-lookup"><span data-stu-id="980af-176">✓</span></span></td>
      <td><span data-ttu-id="980af-177">✓</span><span class="sxs-lookup"><span data-stu-id="980af-177">✓</span></span></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-178">Tabela magazynu danych SQL Azure</span><span class="sxs-lookup"><span data-stu-id="980af-178">Azure SQL Data Warehouse table</span></span></td>
      <td><span data-ttu-id="980af-179">✓</span><span class="sxs-lookup"><span data-stu-id="980af-179">✓</span></span></td>
      <td><span data-ttu-id="980af-180">✓</span><span class="sxs-lookup"><span data-stu-id="980af-180">✓</span></span></td>
      <td><span data-ttu-id="980af-181">✓</span><span class="sxs-lookup"><span data-stu-id="980af-181">✓</span></span></td>
      <td><span data-ttu-id="980af-182"><font size=2>Narzędzia danych programu SQL Server programu Excel, usłudze Power BI</font></span><span class="sxs-lookup"><span data-stu-id="980af-182"><font size=2>Excel, Power BI, SQL Server data tools</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-183">Widok SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="980af-183">SQL Data Warehouse view</span></span></td>
      <td><span data-ttu-id="980af-184">✓</span><span class="sxs-lookup"><span data-stu-id="980af-184">✓</span></span></td>
      <td><span data-ttu-id="980af-185">✓</span><span class="sxs-lookup"><span data-stu-id="980af-185">✓</span></span></td>
      <td><span data-ttu-id="980af-186">✓</span><span class="sxs-lookup"><span data-stu-id="980af-186">✓</span></span></td>
      <td><span data-ttu-id="980af-187"><font size=2>Narzędzia danych programu SQL Server programu Excel, usłudze Power BI</font></span><span class="sxs-lookup"><span data-stu-id="980af-187"><font size=2>Excel, Power BI, SQL Server data tools</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-188">Wymiar usług SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="980af-188">SQL Server Analysis Services dimension</span></span></td>
      <td><span data-ttu-id="980af-189">✓</span><span class="sxs-lookup"><span data-stu-id="980af-189">✓</span></span></td>
      <td><span data-ttu-id="980af-190">✓</span><span class="sxs-lookup"><span data-stu-id="980af-190">✓</span></span></td>
      <td><span data-ttu-id="980af-191">✓</span><span class="sxs-lookup"><span data-stu-id="980af-191">✓</span></span></td>
      <td><span data-ttu-id="980af-192"><font size=2>Program Excel, usłudze Power BI</font></span><span class="sxs-lookup"><span data-stu-id="980af-192"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-193">SQL Server Analysis Services wskaźnika KPI</span><span class="sxs-lookup"><span data-stu-id="980af-193">SQL Server Analysis Services KPI</span></span></td>
      <td><span data-ttu-id="980af-194">✓</span><span class="sxs-lookup"><span data-stu-id="980af-194">✓</span></span></td>
      <td><span data-ttu-id="980af-195">✓</span><span class="sxs-lookup"><span data-stu-id="980af-195">✓</span></span></td>
      <td><span data-ttu-id="980af-196">✓</span><span class="sxs-lookup"><span data-stu-id="980af-196">✓</span></span></td>
      <td><span data-ttu-id="980af-197"><font size=2>Program Excel, usłudze Power BI</font></span><span class="sxs-lookup"><span data-stu-id="980af-197"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-198">Miara usług SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="980af-198">SQL Server Analysis Services measure</span></span></td>
      <td><span data-ttu-id="980af-199">✓</span><span class="sxs-lookup"><span data-stu-id="980af-199">✓</span></span></td>
      <td><span data-ttu-id="980af-200">✓</span><span class="sxs-lookup"><span data-stu-id="980af-200">✓</span></span></td>
      <td><span data-ttu-id="980af-201">✓</span><span class="sxs-lookup"><span data-stu-id="980af-201">✓</span></span></td>
      <td><span data-ttu-id="980af-202"><font size=2>Program Excel, usłudze Power BI</font></span><span class="sxs-lookup"><span data-stu-id="980af-202"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-203">Tabela SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="980af-203">SQL Server Analysis Services table</span></span></td>
      <td><span data-ttu-id="980af-204">✓</span><span class="sxs-lookup"><span data-stu-id="980af-204">✓</span></span></td>
      <td><span data-ttu-id="980af-205">✓</span><span class="sxs-lookup"><span data-stu-id="980af-205">✓</span></span></td>
      <td><span data-ttu-id="980af-206">✓</span><span class="sxs-lookup"><span data-stu-id="980af-206">✓</span></span></td>
      <td><span data-ttu-id="980af-207"><font size=2>Program Excel, usłudze Power BI</font></span><span class="sxs-lookup"><span data-stu-id="980af-207"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-208">Raport programu SQL Server Reporting Services</span><span class="sxs-lookup"><span data-stu-id="980af-208">SQL Server Reporting Services report</span></span></td>
      <td><span data-ttu-id="980af-209">✓</span><span class="sxs-lookup"><span data-stu-id="980af-209">✓</span></span></td>
      <td><span data-ttu-id="980af-210">✓</span><span class="sxs-lookup"><span data-stu-id="980af-210">✓</span></span></td>
      <td><span data-ttu-id="980af-211">✓</span><span class="sxs-lookup"><span data-stu-id="980af-211">✓</span></span></td>
      <td><span data-ttu-id="980af-212"><font size=2>Przeglądarka</font></span><span class="sxs-lookup"><span data-stu-id="980af-212"><font size=2>Browser</font></span></span></td>
      <td><span data-ttu-id="980af-213"><font size=2>Tylko serwerów w trybie macierzystym. Tryb programu SharePoint nie jest obsługiwany.</font></span><span class="sxs-lookup"><span data-stu-id="980af-213"><font size=2>Native mode servers only. SharePoint mode is not supported.</font></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-214">Tabeli programu SQL Server</span><span class="sxs-lookup"><span data-stu-id="980af-214">SQL Server table</span></span></td>
      <td><span data-ttu-id="980af-215">✓</span><span class="sxs-lookup"><span data-stu-id="980af-215">✓</span></span></td>
      <td><span data-ttu-id="980af-216">✓</span><span class="sxs-lookup"><span data-stu-id="980af-216">✓</span></span></td>
      <td><span data-ttu-id="980af-217">✓</span><span class="sxs-lookup"><span data-stu-id="980af-217">✓</span></span></td>
      <td><span data-ttu-id="980af-218"><font size=2>Narzędzia danych programu SQL Server programu Excel, usłudze Power BI</font></span><span class="sxs-lookup"><span data-stu-id="980af-218"><font size=2>Excel, Power BI, SQL Server data tools</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-219">Widok SQL Server</span><span class="sxs-lookup"><span data-stu-id="980af-219">SQL Server view</span></span></td>
      <td><span data-ttu-id="980af-220">✓</span><span class="sxs-lookup"><span data-stu-id="980af-220">✓</span></span></td>
      <td><span data-ttu-id="980af-221">✓</span><span class="sxs-lookup"><span data-stu-id="980af-221">✓</span></span></td>
      <td><span data-ttu-id="980af-222">✓</span><span class="sxs-lookup"><span data-stu-id="980af-222">✓</span></span></td>
      <td><span data-ttu-id="980af-223"><font size=2>Narzędzia danych programu SQL Server programu Excel, usłudze Power BI</font></span><span class="sxs-lookup"><span data-stu-id="980af-223"><font size=2>Excel, Power BI, SQL Server data tools</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-224">Tabela programu Teradata</span><span class="sxs-lookup"><span data-stu-id="980af-224">Teradata table</span></span></td>
      <td><span data-ttu-id="980af-225">✓</span><span class="sxs-lookup"><span data-stu-id="980af-225">✓</span></span></td>
      <td><span data-ttu-id="980af-226">✓</span><span class="sxs-lookup"><span data-stu-id="980af-226">✓</span></span></td>
      <td><span data-ttu-id="980af-227">✓</span><span class="sxs-lookup"><span data-stu-id="980af-227">✓</span></span></td>
      <td><span data-ttu-id="980af-228"><font size=2>Excel</font></span><span class="sxs-lookup"><span data-stu-id="980af-228"><font size=2>Excel</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-229">Widok programu Teradata</span><span class="sxs-lookup"><span data-stu-id="980af-229">Teradata view</span></span></td>
      <td><span data-ttu-id="980af-230">✓</span><span class="sxs-lookup"><span data-stu-id="980af-230">✓</span></span></td>
      <td><span data-ttu-id="980af-231">✓</span><span class="sxs-lookup"><span data-stu-id="980af-231">✓</span></span></td>
      <td><span data-ttu-id="980af-232">✓</span><span class="sxs-lookup"><span data-stu-id="980af-232">✓</span></span></td>
      <td><span data-ttu-id="980af-233"><font size=2>Excel</font></span><span class="sxs-lookup"><span data-stu-id="980af-233"><font size=2>Excel</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-234">Widok SAP HANA</span><span class="sxs-lookup"><span data-stu-id="980af-234">SAP HANA view</span></span></td>
      <td><span data-ttu-id="980af-235">✓</span><span class="sxs-lookup"><span data-stu-id="980af-235">✓</span></span></td>
      <td><span data-ttu-id="980af-236">✓</span><span class="sxs-lookup"><span data-stu-id="980af-236">✓</span></span></td>
      <td><span data-ttu-id="980af-237">✓</span><span class="sxs-lookup"><span data-stu-id="980af-237">✓</span></span></td>
      <td><span data-ttu-id="980af-238"><font size=2>Power BI</font></span><span class="sxs-lookup"><span data-stu-id="980af-238"><font size=2>Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-239">Tabela bazy danych DB2</span><span class="sxs-lookup"><span data-stu-id="980af-239">DB2 table</span></span></td>
      <td><span data-ttu-id="980af-240">✓</span><span class="sxs-lookup"><span data-stu-id="980af-240">✓</span></span></td>
      <td><span data-ttu-id="980af-241">✓</span><span class="sxs-lookup"><span data-stu-id="980af-241">✓</span></span></td>
      <td><span data-ttu-id="980af-242">✓</span><span class="sxs-lookup"><span data-stu-id="980af-242">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-243">Widok bazy danych DB2</span><span class="sxs-lookup"><span data-stu-id="980af-243">DB2 view</span></span></td>
      <td><span data-ttu-id="980af-244">✓</span><span class="sxs-lookup"><span data-stu-id="980af-244">✓</span></span></td>
      <td><span data-ttu-id="980af-245">✓</span><span class="sxs-lookup"><span data-stu-id="980af-245">✓</span></span></td>
      <td><span data-ttu-id="980af-246">✓</span><span class="sxs-lookup"><span data-stu-id="980af-246">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-247">Pliku</span><span class="sxs-lookup"><span data-stu-id="980af-247">File system file</span></span></td>
      <td><span data-ttu-id="980af-248">✓</span><span class="sxs-lookup"><span data-stu-id="980af-248">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-249">Katalogu FTP</span><span class="sxs-lookup"><span data-stu-id="980af-249">FTP directory</span></span></td>
      <td><span data-ttu-id="980af-250">✓</span><span class="sxs-lookup"><span data-stu-id="980af-250">✓</span></span></td>
      <td><span data-ttu-id="980af-251">✓</span><span class="sxs-lookup"><span data-stu-id="980af-251">✓</span></span></td>
      <td><span data-ttu-id="980af-252">✓</span><span class="sxs-lookup"><span data-stu-id="980af-252">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-253">Plik FTP</span><span class="sxs-lookup"><span data-stu-id="980af-253">FTP file</span></span></td>
      <td><span data-ttu-id="980af-254">✓</span><span class="sxs-lookup"><span data-stu-id="980af-254">✓</span></span></td>
      <td><span data-ttu-id="980af-255">✓</span><span class="sxs-lookup"><span data-stu-id="980af-255">✓</span></span></td>
      <td><span data-ttu-id="980af-256">✓</span><span class="sxs-lookup"><span data-stu-id="980af-256">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-257">Raport HTTP</span><span class="sxs-lookup"><span data-stu-id="980af-257">HTTP report</span></span></td>
      <td><span data-ttu-id="980af-258">✓</span><span class="sxs-lookup"><span data-stu-id="980af-258">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-259">Punkt końcowy HTTP</span><span class="sxs-lookup"><span data-stu-id="980af-259">HTTP endpoint</span></span></td>
      <td><span data-ttu-id="980af-260">✓</span><span class="sxs-lookup"><span data-stu-id="980af-260">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-261">Plik HTTP</span><span class="sxs-lookup"><span data-stu-id="980af-261">HTTP file</span></span></td>
      <td><span data-ttu-id="980af-262">✓</span><span class="sxs-lookup"><span data-stu-id="980af-262">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-263">Zestaw jednostek OData</span><span class="sxs-lookup"><span data-stu-id="980af-263">OData entity set</span></span></td>
      <td><span data-ttu-id="980af-264">✓</span><span class="sxs-lookup"><span data-stu-id="980af-264">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-265">Funkcję OData</span><span class="sxs-lookup"><span data-stu-id="980af-265">OData function</span></span></td>
      <td><span data-ttu-id="980af-266">✓</span><span class="sxs-lookup"><span data-stu-id="980af-266">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-267">Tabela PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="980af-267">PostgreSQL table</span></span></td>
      <td><span data-ttu-id="980af-268">✓</span><span class="sxs-lookup"><span data-stu-id="980af-268">✓</span></span></td>
      <td><span data-ttu-id="980af-269">✓</span><span class="sxs-lookup"><span data-stu-id="980af-269">✓</span></span></td>
      <td><span data-ttu-id="980af-270">✓</span><span class="sxs-lookup"><span data-stu-id="980af-270">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-271">Widok PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="980af-271">PostgreSQL view</span></span></td>
      <td><span data-ttu-id="980af-272">✓</span><span class="sxs-lookup"><span data-stu-id="980af-272">✓</span></span></td>
      <td><span data-ttu-id="980af-273">✓</span><span class="sxs-lookup"><span data-stu-id="980af-273">✓</span></span></td>
      <td><span data-ttu-id="980af-274">✓</span><span class="sxs-lookup"><span data-stu-id="980af-274">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-275">Widok SAP HANA</span><span class="sxs-lookup"><span data-stu-id="980af-275">SAP HANA view</span></span></td>
      <td><span data-ttu-id="980af-276">✓</span><span class="sxs-lookup"><span data-stu-id="980af-276">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td> <span data-ttu-id="980af-277">Obiekt SalesForce</span><span class="sxs-lookup"><span data-stu-id="980af-277">Salesforce object</span></span></td>
      <td><span data-ttu-id="980af-278">✓</span><span class="sxs-lookup"><span data-stu-id="980af-278">✓</span></span></td>
      <td><span data-ttu-id="980af-279">✓</span><span class="sxs-lookup"><span data-stu-id="980af-279">✓</span></span></td>
      <td><span data-ttu-id="980af-280">✓</span><span class="sxs-lookup"><span data-stu-id="980af-280">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-281">Listy programu SharePoint</span><span class="sxs-lookup"><span data-stu-id="980af-281">SharePoint list</span></span> </td>
      <td><span data-ttu-id="980af-282">✓</span><span class="sxs-lookup"><span data-stu-id="980af-282">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-283">Azure DB rozwiązania Cosmos kolekcji</span><span class="sxs-lookup"><span data-stu-id="980af-283">Azure Cosmos DB collection</span></span></td>
      <td><span data-ttu-id="980af-284">✓</span><span class="sxs-lookup"><span data-stu-id="980af-284">✓</span></span></td>
      <td><span data-ttu-id="980af-285">✓</span><span class="sxs-lookup"><span data-stu-id="980af-285">✓</span></span></td>
      <td><span data-ttu-id="980af-286">✓</span><span class="sxs-lookup"><span data-stu-id="980af-286">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-287">Ogólny tabeli ODBC</span><span class="sxs-lookup"><span data-stu-id="980af-287">Generic ODBC table</span></span></td>
      <td><span data-ttu-id="980af-288">✓</span><span class="sxs-lookup"><span data-stu-id="980af-288">✓</span></span></td>
      <td><span data-ttu-id="980af-289">✓</span><span class="sxs-lookup"><span data-stu-id="980af-289">✓</span></span></td>
      <td><span data-ttu-id="980af-290">✓</span><span class="sxs-lookup"><span data-stu-id="980af-290">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-291">Ogólny widok ODBC</span><span class="sxs-lookup"><span data-stu-id="980af-291">Generic ODBC view</span></span></td>
      <td><span data-ttu-id="980af-292">✓</span><span class="sxs-lookup"><span data-stu-id="980af-292">✓</span></span></td>
      <td><span data-ttu-id="980af-293">✓</span><span class="sxs-lookup"><span data-stu-id="980af-293">✓</span></span></td>
      <td><span data-ttu-id="980af-294">✓</span><span class="sxs-lookup"><span data-stu-id="980af-294">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-295">Tabela Cassandra</span><span class="sxs-lookup"><span data-stu-id="980af-295">Cassandra table</span></span></td>
      <td><span data-ttu-id="980af-296">✓</span><span class="sxs-lookup"><span data-stu-id="980af-296">✓</span></span></td>
      <td><span data-ttu-id="980af-297">✓</span><span class="sxs-lookup"><span data-stu-id="980af-297">✓</span></span></td>
      <td><span data-ttu-id="980af-298">✓</span><span class="sxs-lookup"><span data-stu-id="980af-298">✓</span></span></td>
      <td><font size=2></font></td>
      <td><span data-ttu-id="980af-299"><font size=2>Publikuj jako ogólnego zasobów ODBC</font></span><span class="sxs-lookup"><span data-stu-id="980af-299"><font size=2>Publish as a generic ODBC asset</font></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-300">Widok Cassandra</span><span class="sxs-lookup"><span data-stu-id="980af-300">Cassandra view</span></span></td>
      <td><span data-ttu-id="980af-301">✓</span><span class="sxs-lookup"><span data-stu-id="980af-301">✓</span></span></td>
      <td><span data-ttu-id="980af-302">✓</span><span class="sxs-lookup"><span data-stu-id="980af-302">✓</span></span></td>
      <td><span data-ttu-id="980af-303">✓</span><span class="sxs-lookup"><span data-stu-id="980af-303">✓</span></span></td>
      <td><font size=2></font></td>
      <td><span data-ttu-id="980af-304"><font size=2>Publikuj jako ogólnego zasobów ODBC</font></span><span class="sxs-lookup"><span data-stu-id="980af-304"><font size=2>Publish as a generic ODBC asset</font></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-305">Tabela programu Sybase</span><span class="sxs-lookup"><span data-stu-id="980af-305">Sybase table</span></span></td>
      <td><span data-ttu-id="980af-306">✓</span><span class="sxs-lookup"><span data-stu-id="980af-306">✓</span></span></td>
      <td><span data-ttu-id="980af-307">✓</span><span class="sxs-lookup"><span data-stu-id="980af-307">✓</span></span></td>
      <td><span data-ttu-id="980af-308">✓</span><span class="sxs-lookup"><span data-stu-id="980af-308">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-309">Widok programu Sybase</span><span class="sxs-lookup"><span data-stu-id="980af-309">Sybase view</span></span></td>
      <td><span data-ttu-id="980af-310">✓</span><span class="sxs-lookup"><span data-stu-id="980af-310">✓</span></span></td>
      <td><span data-ttu-id="980af-311">✓</span><span class="sxs-lookup"><span data-stu-id="980af-311">✓</span></span></td>
      <td><span data-ttu-id="980af-312">✓</span><span class="sxs-lookup"><span data-stu-id="980af-312">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-313">Tabela bazy danych MongoDB</span><span class="sxs-lookup"><span data-stu-id="980af-313">MongoDB table</span></span></td>
      <td><span data-ttu-id="980af-314">✓</span><span class="sxs-lookup"><span data-stu-id="980af-314">✓</span></span></td>
      <td><span data-ttu-id="980af-315">✓</span><span class="sxs-lookup"><span data-stu-id="980af-315">✓</span></span></td>
      <td><span data-ttu-id="980af-316">✓</span><span class="sxs-lookup"><span data-stu-id="980af-316">✓</span></span></td>
      <td><font size=2></font></td>
      <td><span data-ttu-id="980af-317"><font size=2>Publikuj jako ogólnego zasobów ODBC</font></span><span class="sxs-lookup"><span data-stu-id="980af-317"><font size=2>Publish as a generic ODBC asset</font></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-318">Widok bazy danych MongoDB</span><span class="sxs-lookup"><span data-stu-id="980af-318">MongoDB view</span></span></td>
      <td><span data-ttu-id="980af-319">✓</span><span class="sxs-lookup"><span data-stu-id="980af-319">✓</span></span></td>
      <td><span data-ttu-id="980af-320">✓</span><span class="sxs-lookup"><span data-stu-id="980af-320">✓</span></span></td>
      <td><span data-ttu-id="980af-321">✓</span><span class="sxs-lookup"><span data-stu-id="980af-321">✓</span></span></td>
      <td><font size=2></font></td>
      <td><span data-ttu-id="980af-322"><font size=2>Publikuj jako ogólnego zasobów ODBC</font></span><span class="sxs-lookup"><span data-stu-id="980af-322"><font size=2>Publish as a generic ODBC asset</font></span></span></td>
    </tr>
</table>

<span data-ttu-id="980af-323">Jeśli potrzebujesz pomocy technicznej dla dodatkowych źródeł, należy przesłać żądanie funkcji [forum usługi Azure Data Catalog](http://go.microsoft.com/fwlink/?LinkID=616424&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="980af-323">If you need support for additional sources, submit a feature request to the [Azure Data Catalog forum](http://go.microsoft.com/fwlink/?LinkID=616424&clcid=0x409).</span></span>


## <a name="data-source-reference-specification"></a><span data-ttu-id="980af-324">Specyfikacja odwołanie do źródła danych</span><span class="sxs-lookup"><span data-stu-id="980af-324">Data-source reference specification</span></span>
> [!NOTE]
> <span data-ttu-id="980af-325">**Struktury DSL** kolumny w tabeli poniżej wymieniono tylko właściwości połączenia "address" w zbiorze właściwości używanych przez usługi Azure Data Catalog.</span><span class="sxs-lookup"><span data-stu-id="980af-325">The **DSL structure** column in the following table lists only the connection properties for "address" property bag that are used by Azure Data Catalog.</span></span> <span data-ttu-id="980af-326">Oznacza to zbiór właściwości "address" może zawierać innych właściwości połączenia źródła danych, które Azure Data Catalog będzie się powtarzać, ale nie używa.</span><span class="sxs-lookup"><span data-stu-id="980af-326">That is, "address" property bag can contain other connection properties of the data source which Azure Data Catalog persists, but does not use.</span></span>

<table>
    <tr>
       <td><span data-ttu-id="980af-327"><b>Typ źródła</b></span><span class="sxs-lookup"><span data-stu-id="980af-327"><b>Source type</b></span></span></td>
       <td><span data-ttu-id="980af-328"><b>Typ zasobu</b></span><span class="sxs-lookup"><span data-stu-id="980af-328"><b>Asset type</b></span></span></td>
       <td><span data-ttu-id="980af-329"><b>Typy obiektów</b></span><span class="sxs-lookup"><span data-stu-id="980af-329"><b>Object types</b></span></span></td>
       <td><span data-ttu-id="980af-330"><b>Struktura DSL<b></span><span class="sxs-lookup"><span data-stu-id="980af-330"><b>DSL structure<b></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-331">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="980af-331">Azure Data Lake Store</span></span></td>
      <td><span data-ttu-id="980af-332">Kontener</span><span class="sxs-lookup"><span data-stu-id="980af-332">Container</span></span></td>
      <td><span data-ttu-id="980af-333">Data Lake</span><span class="sxs-lookup"><span data-stu-id="980af-333">Data Lake</span></span></td>
      <td><span data-ttu-id="980af-334">
        <font size=2>Protokół: webhdfs</span><span class="sxs-lookup"><span data-stu-id="980af-334">
        <font size=2> Protocol: webhdfs</span></span> <br><span data-ttu-id="980af-335">Uwierzytelnianie: {podstawowe, oauth}</span><span class="sxs-lookup"><span data-stu-id="980af-335">Authentication: {basic, oauth}</span></span> <br><span data-ttu-id="980af-336">Adres:</span><span class="sxs-lookup"><span data-stu-id="980af-336">Address:</span></span> <br><span data-ttu-id="980af-337">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;adres URL</font>
      </span><span class="sxs-lookup"><span data-stu-id="980af-337">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-338">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="980af-338">Azure Data Lake Store</span></span></td>
      <td><span data-ttu-id="980af-339">Tabela</span><span class="sxs-lookup"><span data-stu-id="980af-339">Table</span></span></td>
      <td><span data-ttu-id="980af-340">Plik w katalogu</span><span class="sxs-lookup"><span data-stu-id="980af-340">Directory, file</span></span></td>
      <td><span data-ttu-id="980af-341">
        <font size=2>Protokół: webhdfs</span><span class="sxs-lookup"><span data-stu-id="980af-341">
        <font size=2> Protocol: webhdfs</span></span> <br><span data-ttu-id="980af-342">Uwierzytelnianie: {podstawowe, oauth}</span><span class="sxs-lookup"><span data-stu-id="980af-342">Authentication: {basic, oauth}</span></span> <br><span data-ttu-id="980af-343">Adres:</span><span class="sxs-lookup"><span data-stu-id="980af-343">Address:</span></span> <br><span data-ttu-id="980af-344">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;adres URL</font>
      </span><span class="sxs-lookup"><span data-stu-id="980af-344">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-345">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="980af-345">Azure Storage</span></span></td>
      <td><span data-ttu-id="980af-346">Kontener</span><span class="sxs-lookup"><span data-stu-id="980af-346">Container</span></span></td>
      <td><span data-ttu-id="980af-347">Kontener</span><span class="sxs-lookup"><span data-stu-id="980af-347">Container</span></span></td>
      <td><span data-ttu-id="980af-348">
        <font size=2>Protokół: obiektach blob azure</span><span class="sxs-lookup"><span data-stu-id="980af-348">
        <font size=2> Protocol: azure-blobs</span></span> <br><span data-ttu-id="980af-349">Uwierzytelnianie: {azure klawisza dostępu}</span><span class="sxs-lookup"><span data-stu-id="980af-349">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="980af-350">Adres:</span><span class="sxs-lookup"><span data-stu-id="980af-350">Address:</span></span> <br><span data-ttu-id="980af-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;domeny</span><span class="sxs-lookup"><span data-stu-id="980af-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span></span> <br><span data-ttu-id="980af-352">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;konta</span><span class="sxs-lookup"><span data-stu-id="980af-352">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account</span></span> <br><span data-ttu-id="980af-353">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;kontener</font>
      </span><span class="sxs-lookup"><span data-stu-id="980af-353">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; container </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-354">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="980af-354">Azure Storage</span></span></td>
      <td><span data-ttu-id="980af-355">Tabela</span><span class="sxs-lookup"><span data-stu-id="980af-355">Table</span></span></td>
      <td><span data-ttu-id="980af-356">Obiekt blob, katalogu</span><span class="sxs-lookup"><span data-stu-id="980af-356">Blob, directory</span></span></td>
      <td><span data-ttu-id="980af-357">
        <font size=2>Protokół: obiektach blob azure</span><span class="sxs-lookup"><span data-stu-id="980af-357">
        <font size=2> Protocol: azure-blobs</span></span> <br><span data-ttu-id="980af-358">Uwierzytelnianie: {azure klawisza dostępu}</span><span class="sxs-lookup"><span data-stu-id="980af-358">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="980af-359">Adres:</span><span class="sxs-lookup"><span data-stu-id="980af-359">Address:</span></span> <br><span data-ttu-id="980af-360">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;domeny</span><span class="sxs-lookup"><span data-stu-id="980af-360">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span></span> <br><span data-ttu-id="980af-361">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;konta</span><span class="sxs-lookup"><span data-stu-id="980af-361">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account</span></span> <br><span data-ttu-id="980af-362">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;kontener</span><span class="sxs-lookup"><span data-stu-id="980af-362">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; container</span></span> <br><span data-ttu-id="980af-363">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Nazwa</font>
      </span><span class="sxs-lookup"><span data-stu-id="980af-363">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; name </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-364">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="980af-364">Azure Storage</span></span></td>
      <td><span data-ttu-id="980af-365">Kontener</span><span class="sxs-lookup"><span data-stu-id="980af-365">Container</span></span></td>
      <td><span data-ttu-id="980af-366">Kontener</span><span class="sxs-lookup"><span data-stu-id="980af-366">Container</span></span></td>
      <td><span data-ttu-id="980af-367">
        <font size=2>Protokół: azure — tabele</span><span class="sxs-lookup"><span data-stu-id="980af-367">
        <font size=2> Protocol: azure-tables</span></span> <br><span data-ttu-id="980af-368">Uwierzytelnianie: {azure klawisza dostępu}</span><span class="sxs-lookup"><span data-stu-id="980af-368">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="980af-369">Adres:</span><span class="sxs-lookup"><span data-stu-id="980af-369">Address:</span></span> <br><span data-ttu-id="980af-370">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;domeny</span><span class="sxs-lookup"><span data-stu-id="980af-370">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span></span> <br><span data-ttu-id="980af-371">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;konta</font>
      </span><span class="sxs-lookup"><span data-stu-id="980af-371">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-372">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="980af-372">Azure Storage</span></span></td>
      <td><span data-ttu-id="980af-373">Tabela</span><span class="sxs-lookup"><span data-stu-id="980af-373">Table</span></span></td>
      <td><span data-ttu-id="980af-374">Tabela</span><span class="sxs-lookup"><span data-stu-id="980af-374">Table</span></span></td>
      <td><span data-ttu-id="980af-375">
        <font size=2>Protokół: azure — tabele</span><span class="sxs-lookup"><span data-stu-id="980af-375">
        <font size=2> Protocol: azure-tables</span></span> <br><span data-ttu-id="980af-376">Uwierzytelnianie: {azure klawisza dostępu}</span><span class="sxs-lookup"><span data-stu-id="980af-376">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="980af-377">Adres:</span><span class="sxs-lookup"><span data-stu-id="980af-377">Address:</span></span> <br><span data-ttu-id="980af-378">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;domeny</span><span class="sxs-lookup"><span data-stu-id="980af-378">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span></span> <br><span data-ttu-id="980af-379">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;konta</span><span class="sxs-lookup"><span data-stu-id="980af-379">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account</span></span> <br><span data-ttu-id="980af-380">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Nazwa</font>
      </span><span class="sxs-lookup"><span data-stu-id="980af-380">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; name </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-381">Rozwiązania cosmos</span><span class="sxs-lookup"><span data-stu-id="980af-381">Cosmos</span></span></td>
      <td><span data-ttu-id="980af-382">Kontener</span><span class="sxs-lookup"><span data-stu-id="980af-382">Container</span></span></td>
      <td><span data-ttu-id="980af-383">Klaster wirtualny</span><span class="sxs-lookup"><span data-stu-id="980af-383">Virtual cluster</span></span></td>
      <td><span data-ttu-id="980af-384">
        <font size=2>Protokół: rozwiązania cosmos</span><span class="sxs-lookup"><span data-stu-id="980af-384">
        <font size=2> Protocol: cosmos</span></span> <br><span data-ttu-id="980af-385">Uwierzytelnianie: {podstawowe, windows}</span><span class="sxs-lookup"><span data-stu-id="980af-385">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="980af-386">Adres:</span><span class="sxs-lookup"><span data-stu-id="980af-386">Address:</span></span> <br><span data-ttu-id="980af-387">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;adres URL</font>
      </span><span class="sxs-lookup"><span data-stu-id="980af-387">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-388">Rozwiązania cosmos</span><span class="sxs-lookup"><span data-stu-id="980af-388">Cosmos</span></span></td>
      <td><span data-ttu-id="980af-389">Tabela</span><span class="sxs-lookup"><span data-stu-id="980af-389">Table</span></span></td>
      <td><span data-ttu-id="980af-390">Strumień, zestaw strumienia widoku</span><span class="sxs-lookup"><span data-stu-id="980af-390">Stream, stream set, view</span></span></td>
      <td><span data-ttu-id="980af-391">
        <font size=2>Protokół: rozwiązania cosmos</span><span class="sxs-lookup"><span data-stu-id="980af-391">
        <font size=2> Protocol: cosmos</span></span> <br><span data-ttu-id="980af-392">Uwierzytelnianie: {podstawowe, windows}</span><span class="sxs-lookup"><span data-stu-id="980af-392">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="980af-393">Adres:</span><span class="sxs-lookup"><span data-stu-id="980af-393">Address:</span></span> <br><span data-ttu-id="980af-394">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;adres URL</font>
      </span><span class="sxs-lookup"><span data-stu-id="980af-394">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-395">Datazen</span><span class="sxs-lookup"><span data-stu-id="980af-395">Datazen</span></span></td>
      <td><span data-ttu-id="980af-396">Kontener</span><span class="sxs-lookup"><span data-stu-id="980af-396">Container</span></span></td>
      <td><span data-ttu-id="980af-397">Lokacji</span><span class="sxs-lookup"><span data-stu-id="980af-397">Site</span></span></td>
      <td><span data-ttu-id="980af-398">
        <font size=2>Protokół: http</span><span class="sxs-lookup"><span data-stu-id="980af-398">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="980af-399">Uwierzytelnianie: {none, basic, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="980af-399">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="980af-400">Adres:</span><span class="sxs-lookup"><span data-stu-id="980af-400">Address:</span></span> <br><span data-ttu-id="980af-401">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;adres URL</font>
      </span><span class="sxs-lookup"><span data-stu-id="980af-401">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-402">Datazen</span><span class="sxs-lookup"><span data-stu-id="980af-402">Datazen</span></span></td>
      <td><span data-ttu-id="980af-403">Raport</span><span class="sxs-lookup"><span data-stu-id="980af-403">Report</span></span></td>
      <td><span data-ttu-id="980af-404">Raport, pulpit nawigacyjny</span><span class="sxs-lookup"><span data-stu-id="980af-404">Report, dashboard</span></span></td>
      <td><span data-ttu-id="980af-405">
        <font size=2>Protokół: http</span><span class="sxs-lookup"><span data-stu-id="980af-405">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="980af-406">Uwierzytelnianie: {none, basic, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="980af-406">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="980af-407">Adres:</span><span class="sxs-lookup"><span data-stu-id="980af-407">Address:</span></span> <br><span data-ttu-id="980af-408">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;adres URL</font>
      </span><span class="sxs-lookup"><span data-stu-id="980af-408">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-409">DB2</span><span class="sxs-lookup"><span data-stu-id="980af-409">DB2</span></span></td>
      <td><span data-ttu-id="980af-410">Kontener</span><span class="sxs-lookup"><span data-stu-id="980af-410">Container</span></span></td>
      <td><span data-ttu-id="980af-411">Database (Baza danych)</span><span class="sxs-lookup"><span data-stu-id="980af-411">Database</span></span></td>
      <td><span data-ttu-id="980af-412">
        <font size=2>Protokół: bazy danych db2</span><span class="sxs-lookup"><span data-stu-id="980af-412">
        <font size=2> Protocol: db2</span></span> <br><span data-ttu-id="980af-413">Uwierzytelnianie: {podstawowe, windows}</span><span class="sxs-lookup"><span data-stu-id="980af-413">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="980af-414">Adres:</span><span class="sxs-lookup"><span data-stu-id="980af-414">Address:</span></span> <br><span data-ttu-id="980af-415">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Serwer</span><span class="sxs-lookup"><span data-stu-id="980af-415">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="980af-416">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bazy danych</font>
      </span><span class="sxs-lookup"><span data-stu-id="980af-416">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-417">DB2</span><span class="sxs-lookup"><span data-stu-id="980af-417">DB2</span></span></td>
      <td><span data-ttu-id="980af-418">Tabela</span><span class="sxs-lookup"><span data-stu-id="980af-418">Table</span></span></td>
      <td><span data-ttu-id="980af-419">Tabela, widok</span><span class="sxs-lookup"><span data-stu-id="980af-419">Table, view</span></span></td>
      <td><span data-ttu-id="980af-420">
        <font size=2>Protokół: bazy danych db2</span><span class="sxs-lookup"><span data-stu-id="980af-420">
        <font size=2> Protocol: db2</span></span> <br><span data-ttu-id="980af-421">Uwierzytelnianie: {podstawowe, windows}</span><span class="sxs-lookup"><span data-stu-id="980af-421">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="980af-422">Adres:</span><span class="sxs-lookup"><span data-stu-id="980af-422">Address:</span></span> <br><span data-ttu-id="980af-423">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Serwer</span><span class="sxs-lookup"><span data-stu-id="980af-423">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="980af-424">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bazy danych</span><span class="sxs-lookup"><span data-stu-id="980af-424">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="980af-425">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;obiekt</span><span class="sxs-lookup"><span data-stu-id="980af-425">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="980af-426">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Schemat</font>
      </span><span class="sxs-lookup"><span data-stu-id="980af-426">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-427">System plików</span><span class="sxs-lookup"><span data-stu-id="980af-427">File system</span></span></td>
      <td><span data-ttu-id="980af-428">Tabela</span><span class="sxs-lookup"><span data-stu-id="980af-428">Table</span></span></td>
      <td><span data-ttu-id="980af-429">Plik</span><span class="sxs-lookup"><span data-stu-id="980af-429">File</span></span></td>
      <td><span data-ttu-id="980af-430">
        <font size=2>Protokół: plik</span><span class="sxs-lookup"><span data-stu-id="980af-430">
        <font size=2> Protocol: file</span></span> <br><span data-ttu-id="980af-431">Uwierzytelnianie: {none, basic, windows}</span><span class="sxs-lookup"><span data-stu-id="980af-431">Authentication: {none, basic, windows}</span></span> <br><span data-ttu-id="980af-432">Adres:</span><span class="sxs-lookup"><span data-stu-id="980af-432">Address:</span></span> <br><span data-ttu-id="980af-433">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Ścieżka</font>
      </span><span class="sxs-lookup"><span data-stu-id="980af-433">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; path </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-434">FTP</span><span class="sxs-lookup"><span data-stu-id="980af-434">FTP</span></span></td>
      <td><span data-ttu-id="980af-435">Tabela</span><span class="sxs-lookup"><span data-stu-id="980af-435">Table</span></span></td>
      <td><span data-ttu-id="980af-436">Plik w katalogu</span><span class="sxs-lookup"><span data-stu-id="980af-436">Directory, file</span></span></td>
      <td><span data-ttu-id="980af-437">
        <font size=2>Protokół: ftp</span><span class="sxs-lookup"><span data-stu-id="980af-437">
        <font size=2> Protocol: ftp</span></span> <br><span data-ttu-id="980af-438">Uwierzytelnianie: {none, basic, windows}</span><span class="sxs-lookup"><span data-stu-id="980af-438">Authentication: {none, basic, windows}</span></span> <br><span data-ttu-id="980af-439">Adres:</span><span class="sxs-lookup"><span data-stu-id="980af-439">Address:</span></span> <br><span data-ttu-id="980af-440">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;adres URL</font>
      </span><span class="sxs-lookup"><span data-stu-id="980af-440">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-441">Hadoop rozproszonego systemu plików</span><span class="sxs-lookup"><span data-stu-id="980af-441">Hadoop Distributed File System</span></span></td>
      <td><span data-ttu-id="980af-442">Kontener</span><span class="sxs-lookup"><span data-stu-id="980af-442">Container</span></span></td>
      <td><span data-ttu-id="980af-443">Klaster</span><span class="sxs-lookup"><span data-stu-id="980af-443">Cluster</span></span></td>
      <td><span data-ttu-id="980af-444">
        <font size=2>Protokół: webhdfs</span><span class="sxs-lookup"><span data-stu-id="980af-444">
        <font size=2> Protocol: webhdfs</span></span> <br><span data-ttu-id="980af-445">Uwierzytelnianie: {podstawowe, oauth}</span><span class="sxs-lookup"><span data-stu-id="980af-445">Authentication: {basic, oauth}</span></span> <br><span data-ttu-id="980af-446">Adres:</span><span class="sxs-lookup"><span data-stu-id="980af-446">Address:</span></span> <br><span data-ttu-id="980af-447">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;adres URL</font>
      </span><span class="sxs-lookup"><span data-stu-id="980af-447">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-448">Hadoop rozproszonego systemu plików</span><span class="sxs-lookup"><span data-stu-id="980af-448">Hadoop Distributed File System</span></span></td>
      <td><span data-ttu-id="980af-449">Tabela</span><span class="sxs-lookup"><span data-stu-id="980af-449">Table</span></span></td>
      <td><span data-ttu-id="980af-450">Plik w katalogu</span><span class="sxs-lookup"><span data-stu-id="980af-450">Directory, file</span></span></td>
      <td><span data-ttu-id="980af-451">
        <font size=2>Protokół: webhdfs</span><span class="sxs-lookup"><span data-stu-id="980af-451">
        <font size=2> Protocol: webhdfs</span></span> <br><span data-ttu-id="980af-452">Uwierzytelnianie: {podstawowe, oauth}</span><span class="sxs-lookup"><span data-stu-id="980af-452">Authentication: {basic, oauth}</span></span> <br><span data-ttu-id="980af-453">Adres:</span><span class="sxs-lookup"><span data-stu-id="980af-453">Address:</span></span> <br><span data-ttu-id="980af-454">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;adres URL</font>
      </span><span class="sxs-lookup"><span data-stu-id="980af-454">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-455">Hive</span><span class="sxs-lookup"><span data-stu-id="980af-455">Hive</span></span></td>
      <td><span data-ttu-id="980af-456">Kontener</span><span class="sxs-lookup"><span data-stu-id="980af-456">Container</span></span></td>
      <td><span data-ttu-id="980af-457">Database (Baza danych)</span><span class="sxs-lookup"><span data-stu-id="980af-457">Database</span></span></td>
      <td><span data-ttu-id="980af-458">
        <font size=2>Protokół: gałęzi</span><span class="sxs-lookup"><span data-stu-id="980af-458">
        <font size=2> Protocol: hive</span></span> <br><span data-ttu-id="980af-459">Uwierzytelnianie: {HDInsight, basic, username, Brak}</span><span class="sxs-lookup"><span data-stu-id="980af-459">Authentication: {HDInsight, basic, username, none}</span></span> <br><span data-ttu-id="980af-460">Adres:</span><span class="sxs-lookup"><span data-stu-id="980af-460">Address:</span></span> <br><span data-ttu-id="980af-461">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Serwer</span><span class="sxs-lookup"><span data-stu-id="980af-461">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="980af-462">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bazy danych</span><span class="sxs-lookup"><span data-stu-id="980af-462">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="980af-463">connectionProperties:</span><span class="sxs-lookup"><span data-stu-id="980af-463">connectionProperties:</span></span> <br><span data-ttu-id="980af-464">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;serverProtocol: {hive2}</font>
      </span><span class="sxs-lookup"><span data-stu-id="980af-464">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; serverProtocol: {hive2} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-465">Hive</span><span class="sxs-lookup"><span data-stu-id="980af-465">Hive</span></span></td>
      <td><span data-ttu-id="980af-466">Tabela</span><span class="sxs-lookup"><span data-stu-id="980af-466">Table</span></span></td>
      <td><span data-ttu-id="980af-467">Tabela, widok</span><span class="sxs-lookup"><span data-stu-id="980af-467">Table, view</span></span></td>
      <td><span data-ttu-id="980af-468">
        <font size=2>Protokół: gałęzi</span><span class="sxs-lookup"><span data-stu-id="980af-468">
        <font size=2> Protocol: hive</span></span> <br><span data-ttu-id="980af-469">Uwierzytelnianie: {HDInsight, basic, username, Brak}</span><span class="sxs-lookup"><span data-stu-id="980af-469">Authentication: {HDInsight, basic, username, none}</span></span> <br><span data-ttu-id="980af-470">Adres:</span><span class="sxs-lookup"><span data-stu-id="980af-470">Address:</span></span> <br><span data-ttu-id="980af-471">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Serwer</span><span class="sxs-lookup"><span data-stu-id="980af-471">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="980af-472">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bazy danych</span><span class="sxs-lookup"><span data-stu-id="980af-472">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="980af-473">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;obiekt</span><span class="sxs-lookup"><span data-stu-id="980af-473">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="980af-474">connectionProperties:</span><span class="sxs-lookup"><span data-stu-id="980af-474">connectionProperties:</span></span> <br><span data-ttu-id="980af-475">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;serverProtocol: {hive2}</font>
      </span><span class="sxs-lookup"><span data-stu-id="980af-475">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; serverProtocol: {hive2} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-476">HTTP</span><span class="sxs-lookup"><span data-stu-id="980af-476">HTTP</span></span></td>
      <td><span data-ttu-id="980af-477">Kontener</span><span class="sxs-lookup"><span data-stu-id="980af-477">Container</span></span></td>
      <td><span data-ttu-id="980af-478">Lokacji</span><span class="sxs-lookup"><span data-stu-id="980af-478">Site</span></span></td>
      <td><span data-ttu-id="980af-479">
        <font size=2>Protokół: http</span><span class="sxs-lookup"><span data-stu-id="980af-479">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="980af-480">Uwierzytelnianie: {none, basic, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="980af-480">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="980af-481">Adres:</span><span class="sxs-lookup"><span data-stu-id="980af-481">Address:</span></span> <br><span data-ttu-id="980af-482">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;adres URL</font>
      </span><span class="sxs-lookup"><span data-stu-id="980af-482">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-483">HTTP</span><span class="sxs-lookup"><span data-stu-id="980af-483">HTTP</span></span></td>
      <td><span data-ttu-id="980af-484">Raport</span><span class="sxs-lookup"><span data-stu-id="980af-484">Report</span></span></td>
      <td><span data-ttu-id="980af-485">Raport, pulpit nawigacyjny</span><span class="sxs-lookup"><span data-stu-id="980af-485">Report, dashboard</span></span></td>
      <td><span data-ttu-id="980af-486">
        <font size=2>Protokół: http</span><span class="sxs-lookup"><span data-stu-id="980af-486">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="980af-487">Uwierzytelnianie: {none, basic, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="980af-487">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="980af-488">Adres:</span><span class="sxs-lookup"><span data-stu-id="980af-488">Address:</span></span> <br><span data-ttu-id="980af-489">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;adres URL</font>
      </span><span class="sxs-lookup"><span data-stu-id="980af-489">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-490">HTTP</span><span class="sxs-lookup"><span data-stu-id="980af-490">HTTP</span></span></td>
      <td><span data-ttu-id="980af-491">Tabela</span><span class="sxs-lookup"><span data-stu-id="980af-491">Table</span></span></td>
      <td><span data-ttu-id="980af-492">Punkt końcowy, plik</span><span class="sxs-lookup"><span data-stu-id="980af-492">Endpoint, file</span></span></td>
      <td><span data-ttu-id="980af-493">
        <font size=2>Protokół: http</span><span class="sxs-lookup"><span data-stu-id="980af-493">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="980af-494">Uwierzytelnianie: {none, basic, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="980af-494">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="980af-495">Adres:</span><span class="sxs-lookup"><span data-stu-id="980af-495">Address:</span></span> <br><span data-ttu-id="980af-496">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;adres URL</font>
      </span><span class="sxs-lookup"><span data-stu-id="980af-496">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-497">MySQL</span><span class="sxs-lookup"><span data-stu-id="980af-497">MySQL</span></span></td>
      <td><span data-ttu-id="980af-498">Kontener</span><span class="sxs-lookup"><span data-stu-id="980af-498">Container</span></span></td>
      <td><span data-ttu-id="980af-499">Database (Baza danych)</span><span class="sxs-lookup"><span data-stu-id="980af-499">Database</span></span></td>
      <td><span data-ttu-id="980af-500">
        <font size=2>Protokół: mysql</span><span class="sxs-lookup"><span data-stu-id="980af-500">
        <font size=2> Protocol: mysql</span></span> <br><span data-ttu-id="980af-501">Uwierzytelnianie: {protokołu, windows}</span><span class="sxs-lookup"><span data-stu-id="980af-501">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="980af-502">Adres:</span><span class="sxs-lookup"><span data-stu-id="980af-502">Address:</span></span> <br><span data-ttu-id="980af-503">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Serwer</span><span class="sxs-lookup"><span data-stu-id="980af-503">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="980af-504">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bazy danych</font>
      </span><span class="sxs-lookup"><span data-stu-id="980af-504">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-505">MySQL</span><span class="sxs-lookup"><span data-stu-id="980af-505">MySQL</span></span></td>
      <td><span data-ttu-id="980af-506">Tabela</span><span class="sxs-lookup"><span data-stu-id="980af-506">Table</span></span></td>
      <td><span data-ttu-id="980af-507">Tabela, widok</span><span class="sxs-lookup"><span data-stu-id="980af-507">Table, view</span></span></td>
      <td><span data-ttu-id="980af-508">
        <font size=2>Protokół: mysql</span><span class="sxs-lookup"><span data-stu-id="980af-508">
        <font size=2> Protocol: mysql</span></span> <br><span data-ttu-id="980af-509">Uwierzytelnianie: {protokołu, windows}</span><span class="sxs-lookup"><span data-stu-id="980af-509">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="980af-510">Adres:</span><span class="sxs-lookup"><span data-stu-id="980af-510">Address:</span></span> <br><span data-ttu-id="980af-511">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Serwer</span><span class="sxs-lookup"><span data-stu-id="980af-511">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="980af-512">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bazy danych</span><span class="sxs-lookup"><span data-stu-id="980af-512">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="980af-513">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;obiekt</font>
      </span><span class="sxs-lookup"><span data-stu-id="980af-513">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-514">OData</span><span class="sxs-lookup"><span data-stu-id="980af-514">OData</span></span></td>
      <td><span data-ttu-id="980af-515">Kontener</span><span class="sxs-lookup"><span data-stu-id="980af-515">Container</span></span></td>
      <td><span data-ttu-id="980af-516">Kontenera jednostek</span><span class="sxs-lookup"><span data-stu-id="980af-516">Entity container</span></span></td>
      <td><span data-ttu-id="980af-517">
        <font size=2>Protokół: odata</span><span class="sxs-lookup"><span data-stu-id="980af-517">
        <font size=2> Protocol: odata</span></span> <br><span data-ttu-id="980af-518">Uwierzytelnianie: {none, basic, windows}</span><span class="sxs-lookup"><span data-stu-id="980af-518">Authentication: {none, basic, windows}</span></span> <br><span data-ttu-id="980af-519">Adres:</span><span class="sxs-lookup"><span data-stu-id="980af-519">Address:</span></span> <br><span data-ttu-id="980af-520">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;adres URL</font>
      </span><span class="sxs-lookup"><span data-stu-id="980af-520">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-521">OData</span><span class="sxs-lookup"><span data-stu-id="980af-521">OData</span></span></td>
      <td><span data-ttu-id="980af-522">Tabela</span><span class="sxs-lookup"><span data-stu-id="980af-522">Table</span></span></td>
      <td><span data-ttu-id="980af-523">Zestaw jednostek, funkcja</span><span class="sxs-lookup"><span data-stu-id="980af-523">Entity set, function</span></span></td>
      <td><span data-ttu-id="980af-524">
        <font size=2>Protokół: odata</span><span class="sxs-lookup"><span data-stu-id="980af-524">
        <font size=2> Protocol: odata</span></span> <br><span data-ttu-id="980af-525">Uwierzytelnianie: {none, basic, windows}</span><span class="sxs-lookup"><span data-stu-id="980af-525">Authentication: {none, basic, windows}</span></span> <br><span data-ttu-id="980af-526">Adres:</span><span class="sxs-lookup"><span data-stu-id="980af-526">Address:</span></span> <br><span data-ttu-id="980af-527">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;adres URL</span><span class="sxs-lookup"><span data-stu-id="980af-527">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span></span> <br><span data-ttu-id="980af-528">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;zasobów</font>
      </span><span class="sxs-lookup"><span data-stu-id="980af-528">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; resource </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-529">Baza danych Oracle</span><span class="sxs-lookup"><span data-stu-id="980af-529">Oracle Database</span></span></td>
      <td><span data-ttu-id="980af-530">Kontener</span><span class="sxs-lookup"><span data-stu-id="980af-530">Container</span></span></td>
      <td><span data-ttu-id="980af-531">Database (Baza danych)</span><span class="sxs-lookup"><span data-stu-id="980af-531">Database</span></span></td>
      <td><span data-ttu-id="980af-532">
        <font size=2>Protokół: oracle</span><span class="sxs-lookup"><span data-stu-id="980af-532">
        <font size=2> Protocol: oracle</span></span> <br><span data-ttu-id="980af-533">Uwierzytelnianie: {protokołu, windows}</span><span class="sxs-lookup"><span data-stu-id="980af-533">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="980af-534">Adres:</span><span class="sxs-lookup"><span data-stu-id="980af-534">Address:</span></span> <br><span data-ttu-id="980af-535">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Serwer</span><span class="sxs-lookup"><span data-stu-id="980af-535">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="980af-536">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bazy danych</font>
      </span><span class="sxs-lookup"><span data-stu-id="980af-536">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-537">Baza danych Oracle</span><span class="sxs-lookup"><span data-stu-id="980af-537">Oracle Database</span></span></td>
      <td><span data-ttu-id="980af-538">Tabela</span><span class="sxs-lookup"><span data-stu-id="980af-538">Table</span></span></td>
      <td><span data-ttu-id="980af-539">Tabela, widok</span><span class="sxs-lookup"><span data-stu-id="980af-539">Table, view</span></span></td>
      <td><span data-ttu-id="980af-540">
        <font size=2>Protokół: oracle</span><span class="sxs-lookup"><span data-stu-id="980af-540">
        <font size=2> Protocol: oracle</span></span> <br><span data-ttu-id="980af-541">Uwierzytelnianie: {protokołu, windows}</span><span class="sxs-lookup"><span data-stu-id="980af-541">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="980af-542">Adres:</span><span class="sxs-lookup"><span data-stu-id="980af-542">Address:</span></span> <br><span data-ttu-id="980af-543">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Serwer</span><span class="sxs-lookup"><span data-stu-id="980af-543">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="980af-544">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bazy danych</span><span class="sxs-lookup"><span data-stu-id="980af-544">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="980af-545">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Schemat</span><span class="sxs-lookup"><span data-stu-id="980af-545">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="980af-546">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;obiekt</font>
      </span><span class="sxs-lookup"><span data-stu-id="980af-546">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-547">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="980af-547">PostgreSQL</span></span></td>
      <td><span data-ttu-id="980af-548">Kontener</span><span class="sxs-lookup"><span data-stu-id="980af-548">Container</span></span></td>
      <td><span data-ttu-id="980af-549">Database (Baza danych)</span><span class="sxs-lookup"><span data-stu-id="980af-549">Database</span></span></td>
      <td><span data-ttu-id="980af-550">
        <font size=2>Protokół: postgresql</span><span class="sxs-lookup"><span data-stu-id="980af-550">
        <font size=2> Protocol: postgresql</span></span> <br><span data-ttu-id="980af-551">Uwierzytelnianie: {podstawowe, windows}</span><span class="sxs-lookup"><span data-stu-id="980af-551">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="980af-552">Adres:</span><span class="sxs-lookup"><span data-stu-id="980af-552">Address:</span></span> <br><span data-ttu-id="980af-553">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Serwer</span><span class="sxs-lookup"><span data-stu-id="980af-553">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="980af-554">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bazy danych</font>
      </span><span class="sxs-lookup"><span data-stu-id="980af-554">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-555">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="980af-555">PostgreSQL</span></span></td>
      <td><span data-ttu-id="980af-556">Tabela</span><span class="sxs-lookup"><span data-stu-id="980af-556">Table</span></span></td>
      <td><span data-ttu-id="980af-557">Tabela, widok</span><span class="sxs-lookup"><span data-stu-id="980af-557">Table, view</span></span></td>
      <td><span data-ttu-id="980af-558">
        <font size=2>Protokół: postgresql</span><span class="sxs-lookup"><span data-stu-id="980af-558">
        <font size=2> Protocol: postgresql</span></span> <br><span data-ttu-id="980af-559">Uwierzytelnianie: {podstawowe, windows}</span><span class="sxs-lookup"><span data-stu-id="980af-559">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="980af-560">Adres:</span><span class="sxs-lookup"><span data-stu-id="980af-560">Address:</span></span> <br><span data-ttu-id="980af-561">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Serwer</span><span class="sxs-lookup"><span data-stu-id="980af-561">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="980af-562">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bazy danych</span><span class="sxs-lookup"><span data-stu-id="980af-562">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="980af-563">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Schemat</span><span class="sxs-lookup"><span data-stu-id="980af-563">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="980af-564">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;obiekt</font>
      </span><span class="sxs-lookup"><span data-stu-id="980af-564">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-565">Power BI</span><span class="sxs-lookup"><span data-stu-id="980af-565">Power BI</span></span></td>
      <td><span data-ttu-id="980af-566">Kontener</span><span class="sxs-lookup"><span data-stu-id="980af-566">Container</span></span></td>
      <td><span data-ttu-id="980af-567">Lokacji</span><span class="sxs-lookup"><span data-stu-id="980af-567">Site</span></span></td>
      <td><span data-ttu-id="980af-568">
        <font size=2>Protokół: http</span><span class="sxs-lookup"><span data-stu-id="980af-568">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="980af-569">Uwierzytelnianie: {none, basic, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="980af-569">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="980af-570">Adres:</span><span class="sxs-lookup"><span data-stu-id="980af-570">Address:</span></span> <br><span data-ttu-id="980af-571">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;adres URL</font>
      </span><span class="sxs-lookup"><span data-stu-id="980af-571">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-572">Power BI</span><span class="sxs-lookup"><span data-stu-id="980af-572">Power BI</span></span></td>
      <td><span data-ttu-id="980af-573">Raport</span><span class="sxs-lookup"><span data-stu-id="980af-573">Report</span></span></td>
      <td><span data-ttu-id="980af-574">Raport, pulpit nawigacyjny</span><span class="sxs-lookup"><span data-stu-id="980af-574">Report, dashboard</span></span></td>
      <td><span data-ttu-id="980af-575">
        <font size=2>Protokół: http</span><span class="sxs-lookup"><span data-stu-id="980af-575">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="980af-576">Uwierzytelnianie: {none, basic, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="980af-576">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="980af-577">Adres:</span><span class="sxs-lookup"><span data-stu-id="980af-577">Address:</span></span> <br><span data-ttu-id="980af-578">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;adres URL</font>
      </span><span class="sxs-lookup"><span data-stu-id="980af-578">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-579">Dodatek Power Query</span><span class="sxs-lookup"><span data-stu-id="980af-579">Power Query</span></span></td>
      <td><span data-ttu-id="980af-580">Tabela</span><span class="sxs-lookup"><span data-stu-id="980af-580">Table</span></span></td>
      <td><span data-ttu-id="980af-581">Dane zestawu połączonych danych</span><span class="sxs-lookup"><span data-stu-id="980af-581">Data mashup</span></span></td>
      <td><span data-ttu-id="980af-582">
        <font size=2>Protokół: dodatku power query</span><span class="sxs-lookup"><span data-stu-id="980af-582">
        <font size=2> Protocol: power-query</span></span> <br><span data-ttu-id="980af-583">Uwierzytelnianie: {oauth}</span><span class="sxs-lookup"><span data-stu-id="980af-583">Authentication: {oauth}</span></span> <br><span data-ttu-id="980af-584">Adres:</span><span class="sxs-lookup"><span data-stu-id="980af-584">Address:</span></span> <br><span data-ttu-id="980af-585">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;adres URL</font>
      </span><span class="sxs-lookup"><span data-stu-id="980af-585">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-586">SalesForce</span><span class="sxs-lookup"><span data-stu-id="980af-586">Salesforce</span></span></td>
      <td><span data-ttu-id="980af-587">Tabela</span><span class="sxs-lookup"><span data-stu-id="980af-587">Table</span></span></td>
      <td><span data-ttu-id="980af-588">Obiekt</span><span class="sxs-lookup"><span data-stu-id="980af-588">Object</span></span></td>
      <td><span data-ttu-id="980af-589">
        <font size=2>Protokół: salesforce-com</span><span class="sxs-lookup"><span data-stu-id="980af-589">
        <font size=2> Protocol: salesforce-com</span></span> <br><span data-ttu-id="980af-590">Uwierzytelnianie: {podstawowe, windows}</span><span class="sxs-lookup"><span data-stu-id="980af-590">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="980af-591">Adres:</span><span class="sxs-lookup"><span data-stu-id="980af-591">Address:</span></span> <br><span data-ttu-id="980af-592">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;loginServer</span><span class="sxs-lookup"><span data-stu-id="980af-592">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; loginServer</span></span> <br><span data-ttu-id="980af-593">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;klasy</span><span class="sxs-lookup"><span data-stu-id="980af-593">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; class</span></span> <br><span data-ttu-id="980af-594">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Nazwa elementu</font>
      </span><span class="sxs-lookup"><span data-stu-id="980af-594">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; itemName </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-595">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="980af-595">SAP HANA</span></span></td>
      <td><span data-ttu-id="980af-596">Kontener</span><span class="sxs-lookup"><span data-stu-id="980af-596">Container</span></span></td>
      <td><span data-ttu-id="980af-597">Serwer</span><span class="sxs-lookup"><span data-stu-id="980af-597">Server</span></span></td>
      <td><span data-ttu-id="980af-598">
        <font size=2>Protokół: sap hana-sql</span><span class="sxs-lookup"><span data-stu-id="980af-598">
        <font size=2> Protocol: sap-hana-sql</span></span> <br><span data-ttu-id="980af-599">Uwierzytelnianie: {protokołu, windows}</span><span class="sxs-lookup"><span data-stu-id="980af-599">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="980af-600">Adres:</span><span class="sxs-lookup"><span data-stu-id="980af-600">Address:</span></span> <br><span data-ttu-id="980af-601">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Serwer</font>
      </span><span class="sxs-lookup"><span data-stu-id="980af-601">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-602">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="980af-602">SAP HANA</span></span></td>
      <td><span data-ttu-id="980af-603">Tabela</span><span class="sxs-lookup"><span data-stu-id="980af-603">Table</span></span></td>
      <td><span data-ttu-id="980af-604">Widok</span><span class="sxs-lookup"><span data-stu-id="980af-604">View</span></span></td>
      <td><span data-ttu-id="980af-605">
        <font size=2>Protokół: sap hana-sql</span><span class="sxs-lookup"><span data-stu-id="980af-605">
        <font size=2> Protocol: sap-hana-sql</span></span> <br><span data-ttu-id="980af-606">Uwierzytelnianie: {protokołu, windows}</span><span class="sxs-lookup"><span data-stu-id="980af-606">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="980af-607">Adres:</span><span class="sxs-lookup"><span data-stu-id="980af-607">Address:</span></span> <br><span data-ttu-id="980af-608">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Serwer</span><span class="sxs-lookup"><span data-stu-id="980af-608">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="980af-609">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Schemat</span><span class="sxs-lookup"><span data-stu-id="980af-609">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="980af-610">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;obiekt</font>
      </span><span class="sxs-lookup"><span data-stu-id="980af-610">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-611">Sharepoint</span><span class="sxs-lookup"><span data-stu-id="980af-611">SharePoint</span></span></td>
      <td><span data-ttu-id="980af-612">Tabela</span><span class="sxs-lookup"><span data-stu-id="980af-612">Table</span></span></td>
      <td><span data-ttu-id="980af-613">List</span><span class="sxs-lookup"><span data-stu-id="980af-613">List</span></span></td>
      <td><span data-ttu-id="980af-614">
        <font size=2>Protokołów: listy programu sharepoint</span><span class="sxs-lookup"><span data-stu-id="980af-614">
        <font size=2> Protocol: sharepoint-list</span></span> <br><span data-ttu-id="980af-615">Uwierzytelnianie: {podstawowe, windows}</span><span class="sxs-lookup"><span data-stu-id="980af-615">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="980af-616">Adres:</span><span class="sxs-lookup"><span data-stu-id="980af-616">Address:</span></span> <br><span data-ttu-id="980af-617">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;adres URL</font>
      </span><span class="sxs-lookup"><span data-stu-id="980af-617">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-618">Magazyn danych SQL</span><span class="sxs-lookup"><span data-stu-id="980af-618">SQL Data Warehouse</span></span></td>
      <td><span data-ttu-id="980af-619">Polecenie</span><span class="sxs-lookup"><span data-stu-id="980af-619">Command</span></span></td>
      <td><span data-ttu-id="980af-620">Procedura składowana</span><span class="sxs-lookup"><span data-stu-id="980af-620">Stored procedure</span></span></td>
      <td><span data-ttu-id="980af-621">
        <font size=2>Protokół: tds</span><span class="sxs-lookup"><span data-stu-id="980af-621">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="980af-622">Uwierzytelnianie: {protokołu, windows}</span><span class="sxs-lookup"><span data-stu-id="980af-622">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="980af-623">Adres:</span><span class="sxs-lookup"><span data-stu-id="980af-623">Address:</span></span> <br><span data-ttu-id="980af-624">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Serwer</span><span class="sxs-lookup"><span data-stu-id="980af-624">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="980af-625">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bazy danych</span><span class="sxs-lookup"><span data-stu-id="980af-625">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="980af-626">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Schemat</span><span class="sxs-lookup"><span data-stu-id="980af-626">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="980af-627">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;obiekt</font>
      </span><span class="sxs-lookup"><span data-stu-id="980af-627">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-628">Magazyn danych SQL</span><span class="sxs-lookup"><span data-stu-id="980af-628">SQL Data Warehouse</span></span></td>
      <td><span data-ttu-id="980af-629">TableValuedFunction</span><span class="sxs-lookup"><span data-stu-id="980af-629">TableValuedFunction</span></span></td>
      <td><span data-ttu-id="980af-630">Funkcja zwracająca tabelę</span><span class="sxs-lookup"><span data-stu-id="980af-630">Table-valued function</span></span></td>
      <td><span data-ttu-id="980af-631">
        <font size=2>Protokół: tds</span><span class="sxs-lookup"><span data-stu-id="980af-631">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="980af-632">Uwierzytelnianie: {protokołu, windows}</span><span class="sxs-lookup"><span data-stu-id="980af-632">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="980af-633">Adres:</span><span class="sxs-lookup"><span data-stu-id="980af-633">Address:</span></span> <br><span data-ttu-id="980af-634">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Serwer</span><span class="sxs-lookup"><span data-stu-id="980af-634">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="980af-635">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bazy danych</span><span class="sxs-lookup"><span data-stu-id="980af-635">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="980af-636">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Schemat</span><span class="sxs-lookup"><span data-stu-id="980af-636">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="980af-637">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;obiekt</font>
      </span><span class="sxs-lookup"><span data-stu-id="980af-637">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-638">Magazyn danych SQL</span><span class="sxs-lookup"><span data-stu-id="980af-638">SQL Data Warehouse</span></span></td>
      <td><span data-ttu-id="980af-639">Kontener</span><span class="sxs-lookup"><span data-stu-id="980af-639">Container</span></span></td>
      <td><span data-ttu-id="980af-640">Database (Baza danych)</span><span class="sxs-lookup"><span data-stu-id="980af-640">Database</span></span></td>
      <td><span data-ttu-id="980af-641">
        <font size=2>Protokół: tds</span><span class="sxs-lookup"><span data-stu-id="980af-641">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="980af-642">Uwierzytelnianie: {protokołu, windows}</span><span class="sxs-lookup"><span data-stu-id="980af-642">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="980af-643">Adres:</span><span class="sxs-lookup"><span data-stu-id="980af-643">Address:</span></span> <br><span data-ttu-id="980af-644">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Serwer</span><span class="sxs-lookup"><span data-stu-id="980af-644">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="980af-645">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bazy danych</font>
      </span><span class="sxs-lookup"><span data-stu-id="980af-645">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-646">Magazyn danych SQL</span><span class="sxs-lookup"><span data-stu-id="980af-646">SQL Data Warehouse</span></span></td>
      <td><span data-ttu-id="980af-647">Tabela</span><span class="sxs-lookup"><span data-stu-id="980af-647">Table</span></span></td>
      <td><span data-ttu-id="980af-648">Tabela, widok</span><span class="sxs-lookup"><span data-stu-id="980af-648">Table, view</span></span></td>
      <td><span data-ttu-id="980af-649">
        <font size=2>Protokół: tds</span><span class="sxs-lookup"><span data-stu-id="980af-649">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="980af-650">Uwierzytelnianie: {protokołu, windows}</span><span class="sxs-lookup"><span data-stu-id="980af-650">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="980af-651">Adres:</span><span class="sxs-lookup"><span data-stu-id="980af-651">Address:</span></span> <br><span data-ttu-id="980af-652">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Serwer</span><span class="sxs-lookup"><span data-stu-id="980af-652">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="980af-653">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bazy danych</span><span class="sxs-lookup"><span data-stu-id="980af-653">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="980af-654">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Schemat</span><span class="sxs-lookup"><span data-stu-id="980af-654">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="980af-655">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;obiekt</font>
      </span><span class="sxs-lookup"><span data-stu-id="980af-655">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-656">Oprogramowanie SQL Server</span><span class="sxs-lookup"><span data-stu-id="980af-656">SQL Server</span></span></td>
      <td><span data-ttu-id="980af-657">Polecenie</span><span class="sxs-lookup"><span data-stu-id="980af-657">Command</span></span></td>
      <td><span data-ttu-id="980af-658">Procedura składowana</span><span class="sxs-lookup"><span data-stu-id="980af-658">Stored procedure</span></span></td>
      <td><span data-ttu-id="980af-659">
        <font size=2>Protokół: tds</span><span class="sxs-lookup"><span data-stu-id="980af-659">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="980af-660">Uwierzytelnianie: {protokołu, windows}</span><span class="sxs-lookup"><span data-stu-id="980af-660">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="980af-661">Adres:</span><span class="sxs-lookup"><span data-stu-id="980af-661">Address:</span></span> <br><span data-ttu-id="980af-662">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Serwer</span><span class="sxs-lookup"><span data-stu-id="980af-662">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="980af-663">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bazy danych</span><span class="sxs-lookup"><span data-stu-id="980af-663">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="980af-664">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Schemat</span><span class="sxs-lookup"><span data-stu-id="980af-664">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="980af-665">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;obiekt</font>
      </span><span class="sxs-lookup"><span data-stu-id="980af-665">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-666">Oprogramowanie SQL Server</span><span class="sxs-lookup"><span data-stu-id="980af-666">SQL Server</span></span></td>
      <td><span data-ttu-id="980af-667">TableValuedFunction</span><span class="sxs-lookup"><span data-stu-id="980af-667">TableValuedFunction</span></span></td>
      <td><span data-ttu-id="980af-668">Funkcja zwracająca tabelę</span><span class="sxs-lookup"><span data-stu-id="980af-668">Table-valued function</span></span></td>
      <td><span data-ttu-id="980af-669">
        <font size=2>Protokół: tds</span><span class="sxs-lookup"><span data-stu-id="980af-669">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="980af-670">Uwierzytelnianie: {protokołu, windows}</span><span class="sxs-lookup"><span data-stu-id="980af-670">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="980af-671">Adres:</span><span class="sxs-lookup"><span data-stu-id="980af-671">Address:</span></span> <br><span data-ttu-id="980af-672">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Serwer</span><span class="sxs-lookup"><span data-stu-id="980af-672">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="980af-673">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bazy danych</span><span class="sxs-lookup"><span data-stu-id="980af-673">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="980af-674">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Schemat</span><span class="sxs-lookup"><span data-stu-id="980af-674">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="980af-675">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;obiekt</font>
      </span><span class="sxs-lookup"><span data-stu-id="980af-675">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-676">Oprogramowanie SQL Server</span><span class="sxs-lookup"><span data-stu-id="980af-676">SQL Server</span></span></td>
      <td><span data-ttu-id="980af-677">Kontener</span><span class="sxs-lookup"><span data-stu-id="980af-677">Container</span></span></td>
      <td><span data-ttu-id="980af-678">Database (Baza danych)</span><span class="sxs-lookup"><span data-stu-id="980af-678">Database</span></span></td>
      <td><span data-ttu-id="980af-679">
        <font size=2>Protokół: tds</span><span class="sxs-lookup"><span data-stu-id="980af-679">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="980af-680">Uwierzytelnianie: {protokołu, windows}</span><span class="sxs-lookup"><span data-stu-id="980af-680">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="980af-681">Adres:</span><span class="sxs-lookup"><span data-stu-id="980af-681">Address:</span></span> <br><span data-ttu-id="980af-682">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Serwer</span><span class="sxs-lookup"><span data-stu-id="980af-682">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="980af-683">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bazy danych</font>
      </span><span class="sxs-lookup"><span data-stu-id="980af-683">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-684">Oprogramowanie SQL Server</span><span class="sxs-lookup"><span data-stu-id="980af-684">SQL Server</span></span></td>
      <td><span data-ttu-id="980af-685">Tabela</span><span class="sxs-lookup"><span data-stu-id="980af-685">Table</span></span></td>
      <td><span data-ttu-id="980af-686">Tabela, widok</span><span class="sxs-lookup"><span data-stu-id="980af-686">Table, view</span></span></td>
      <td><span data-ttu-id="980af-687">
        <font size=2>Protokół: tds</span><span class="sxs-lookup"><span data-stu-id="980af-687">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="980af-688">Uwierzytelnianie: {protokołu, windows}</span><span class="sxs-lookup"><span data-stu-id="980af-688">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="980af-689">Adres:</span><span class="sxs-lookup"><span data-stu-id="980af-689">Address:</span></span> <br><span data-ttu-id="980af-690">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Serwer</span><span class="sxs-lookup"><span data-stu-id="980af-690">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="980af-691">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bazy danych</span><span class="sxs-lookup"><span data-stu-id="980af-691">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="980af-692">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Schemat</span><span class="sxs-lookup"><span data-stu-id="980af-692">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="980af-693">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;obiekt</font>
      </span><span class="sxs-lookup"><span data-stu-id="980af-693">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-694">SQL Server Analysis Services wielowymiarowe</span><span class="sxs-lookup"><span data-stu-id="980af-694">SQL Server Analysis Services multidimensional</span></span></td>
      <td><span data-ttu-id="980af-695">Kontener</span><span class="sxs-lookup"><span data-stu-id="980af-695">Container</span></span></td>
      <td><span data-ttu-id="980af-696">Model</span><span class="sxs-lookup"><span data-stu-id="980af-696">Model</span></span></td>
      <td><span data-ttu-id="980af-697">
        <font size=2>Protokół: usługi analysis services</span><span class="sxs-lookup"><span data-stu-id="980af-697">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="980af-698">Uwierzytelnianie: {systemu windows, basic anonimowe, Brak}</span><span class="sxs-lookup"><span data-stu-id="980af-698">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="980af-699">Adres:</span><span class="sxs-lookup"><span data-stu-id="980af-699">Address:</span></span> <br><span data-ttu-id="980af-700">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Serwer</span><span class="sxs-lookup"><span data-stu-id="980af-700">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="980af-701">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bazy danych</span><span class="sxs-lookup"><span data-stu-id="980af-701">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="980af-702">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Model</font>
      </span><span class="sxs-lookup"><span data-stu-id="980af-702">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-703">SQL Server Analysis Services wielowymiarowe</span><span class="sxs-lookup"><span data-stu-id="980af-703">SQL Server Analysis Services multidimensional</span></span></td>
      <td><span data-ttu-id="980af-704">WSKAŹNIK KPI</span><span class="sxs-lookup"><span data-stu-id="980af-704">KPI</span></span></td>
      <td><span data-ttu-id="980af-705">WSKAŹNIK KPI</span><span class="sxs-lookup"><span data-stu-id="980af-705">KPI</span></span></td>
      <td><span data-ttu-id="980af-706">
        <font size=2>Protokół: usługi analysis services</span><span class="sxs-lookup"><span data-stu-id="980af-706">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="980af-707">Uwierzytelnianie: {systemu windows, basic anonimowe, Brak}</span><span class="sxs-lookup"><span data-stu-id="980af-707">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="980af-708">Adres:</span><span class="sxs-lookup"><span data-stu-id="980af-708">Address:</span></span> <br><span data-ttu-id="980af-709">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Serwer</span><span class="sxs-lookup"><span data-stu-id="980af-709">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="980af-710">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bazy danych</span><span class="sxs-lookup"><span data-stu-id="980af-710">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="980af-711">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Model</span><span class="sxs-lookup"><span data-stu-id="980af-711">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="980af-712">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;obiekt</span><span class="sxs-lookup"><span data-stu-id="980af-712">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="980af-713">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Typ obiektu: {KPI}</font>
      </span><span class="sxs-lookup"><span data-stu-id="980af-713">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {KPI} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-714">SQL Server Analysis Services wielowymiarowe</span><span class="sxs-lookup"><span data-stu-id="980af-714">SQL Server Analysis Services multidimensional</span></span></td>
      <td><span data-ttu-id="980af-715">Miary</span><span class="sxs-lookup"><span data-stu-id="980af-715">Measure</span></span></td>
      <td><span data-ttu-id="980af-716">Miary</span><span class="sxs-lookup"><span data-stu-id="980af-716">Measure</span></span></td>
      <td><span data-ttu-id="980af-717">
        <font size=2>Protokół: usługi analysis services</span><span class="sxs-lookup"><span data-stu-id="980af-717">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="980af-718">Uwierzytelnianie: {systemu windows, basic anonimowe, Brak}</span><span class="sxs-lookup"><span data-stu-id="980af-718">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="980af-719">Adres:</span><span class="sxs-lookup"><span data-stu-id="980af-719">Address:</span></span> <br><span data-ttu-id="980af-720">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Serwer</span><span class="sxs-lookup"><span data-stu-id="980af-720">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="980af-721">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bazy danych</span><span class="sxs-lookup"><span data-stu-id="980af-721">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="980af-722">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Model</span><span class="sxs-lookup"><span data-stu-id="980af-722">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="980af-723">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;obiekt</span><span class="sxs-lookup"><span data-stu-id="980af-723">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="980af-724">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Typ obiektu: {Measure}</font>
      </span><span class="sxs-lookup"><span data-stu-id="980af-724">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Measure} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-725">SQL Server Analysis Services wielowymiarowe</span><span class="sxs-lookup"><span data-stu-id="980af-725">SQL Server Analysis Services multidimensional</span></span></td>
      <td><span data-ttu-id="980af-726">Tabela</span><span class="sxs-lookup"><span data-stu-id="980af-726">Table</span></span></td>
      <td><span data-ttu-id="980af-727">Wymiar</span><span class="sxs-lookup"><span data-stu-id="980af-727">Dimension</span></span></td>
      <td><span data-ttu-id="980af-728">
        <font size=2>Protokół: usługi analysis services</span><span class="sxs-lookup"><span data-stu-id="980af-728">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="980af-729">Uwierzytelnianie: {systemu windows, basic anonimowe, Brak}</span><span class="sxs-lookup"><span data-stu-id="980af-729">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="980af-730">Adres:</span><span class="sxs-lookup"><span data-stu-id="980af-730">Address:</span></span> <br><span data-ttu-id="980af-731">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Serwer</span><span class="sxs-lookup"><span data-stu-id="980af-731">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="980af-732">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bazy danych</span><span class="sxs-lookup"><span data-stu-id="980af-732">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="980af-733">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Model</span><span class="sxs-lookup"><span data-stu-id="980af-733">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="980af-734">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;obiekt</span><span class="sxs-lookup"><span data-stu-id="980af-734">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="980af-735">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Typ obiektu: {wymiaru}</font>
      </span><span class="sxs-lookup"><span data-stu-id="980af-735">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Dimension} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-736">SQL Server Analysis Services tabelarycznym</span><span class="sxs-lookup"><span data-stu-id="980af-736">SQL Server Analysis Services tabular</span></span></td>
      <td><span data-ttu-id="980af-737">Kontener</span><span class="sxs-lookup"><span data-stu-id="980af-737">Container</span></span></td>
      <td><span data-ttu-id="980af-738">Model</span><span class="sxs-lookup"><span data-stu-id="980af-738">Model</span></span></td>
      <td><span data-ttu-id="980af-739">
        <font size=2>Protokół: usługi analysis services</span><span class="sxs-lookup"><span data-stu-id="980af-739">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="980af-740">Uwierzytelnianie: {systemu windows, basic anonimowe, Brak}</span><span class="sxs-lookup"><span data-stu-id="980af-740">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="980af-741">Adres:</span><span class="sxs-lookup"><span data-stu-id="980af-741">Address:</span></span> <br><span data-ttu-id="980af-742">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Serwer</span><span class="sxs-lookup"><span data-stu-id="980af-742">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="980af-743">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bazy danych</span><span class="sxs-lookup"><span data-stu-id="980af-743">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="980af-744">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Model</font>
      </span><span class="sxs-lookup"><span data-stu-id="980af-744">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-745">SQL Server Analysis Services tabelarycznym</span><span class="sxs-lookup"><span data-stu-id="980af-745">SQL Server Analysis Services tabular</span></span></td>
      <td><span data-ttu-id="980af-746">WSKAŹNIK KPI</span><span class="sxs-lookup"><span data-stu-id="980af-746">KPI</span></span></td>
      <td><span data-ttu-id="980af-747">WSKAŹNIK KPI</span><span class="sxs-lookup"><span data-stu-id="980af-747">KPI</span></span></td>
      <td><span data-ttu-id="980af-748">
        <font size=2>Protokół: usługi analysis services</span><span class="sxs-lookup"><span data-stu-id="980af-748">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="980af-749">Uwierzytelnianie: {systemu windows, basic anonimowe, Brak}</span><span class="sxs-lookup"><span data-stu-id="980af-749">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="980af-750">Adres:</span><span class="sxs-lookup"><span data-stu-id="980af-750">Address:</span></span> <br><span data-ttu-id="980af-751">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Serwer</span><span class="sxs-lookup"><span data-stu-id="980af-751">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="980af-752">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bazy danych</span><span class="sxs-lookup"><span data-stu-id="980af-752">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="980af-753">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Model</span><span class="sxs-lookup"><span data-stu-id="980af-753">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="980af-754">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;obiekt</span><span class="sxs-lookup"><span data-stu-id="980af-754">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="980af-755">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Typ obiektu: {KPI}</font>
      </span><span class="sxs-lookup"><span data-stu-id="980af-755">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {KPI} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-756">SQL Server Analysis Services tabelarycznym</span><span class="sxs-lookup"><span data-stu-id="980af-756">SQL Server Analysis Services tabular</span></span></td>
      <td><span data-ttu-id="980af-757">Miary</span><span class="sxs-lookup"><span data-stu-id="980af-757">Measure</span></span></td>
      <td><span data-ttu-id="980af-758">Miary</span><span class="sxs-lookup"><span data-stu-id="980af-758">Measure</span></span></td>
      <td><span data-ttu-id="980af-759">
        <font size=2>Protokół: usługi analysis services</span><span class="sxs-lookup"><span data-stu-id="980af-759">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="980af-760">Uwierzytelnianie: {systemu windows, basic anonimowe, Brak}</span><span class="sxs-lookup"><span data-stu-id="980af-760">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="980af-761">Adres:</span><span class="sxs-lookup"><span data-stu-id="980af-761">Address:</span></span> <br><span data-ttu-id="980af-762">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Serwer</span><span class="sxs-lookup"><span data-stu-id="980af-762">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="980af-763">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bazy danych</span><span class="sxs-lookup"><span data-stu-id="980af-763">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="980af-764">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Model</span><span class="sxs-lookup"><span data-stu-id="980af-764">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="980af-765">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;obiekt</span><span class="sxs-lookup"><span data-stu-id="980af-765">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="980af-766">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Typ obiektu: {Measure}</font>
      </span><span class="sxs-lookup"><span data-stu-id="980af-766">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Measure} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-767">SQL Server Analysis Services tabelarycznym</span><span class="sxs-lookup"><span data-stu-id="980af-767">SQL Server Analysis Services tabular</span></span></td>
      <td><span data-ttu-id="980af-768">Tabela</span><span class="sxs-lookup"><span data-stu-id="980af-768">Table</span></span></td>
      <td><span data-ttu-id="980af-769">Tabela</span><span class="sxs-lookup"><span data-stu-id="980af-769">Table</span></span></td>
      <td><span data-ttu-id="980af-770">
        <font size=2>Protokół: usługi analysis services</span><span class="sxs-lookup"><span data-stu-id="980af-770">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="980af-771">Uwierzytelnianie: {systemu windows, basic anonimowe, Brak}</span><span class="sxs-lookup"><span data-stu-id="980af-771">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="980af-772">Adres:</span><span class="sxs-lookup"><span data-stu-id="980af-772">Address:</span></span> <br><span data-ttu-id="980af-773">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Serwer</span><span class="sxs-lookup"><span data-stu-id="980af-773">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="980af-774">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bazy danych</span><span class="sxs-lookup"><span data-stu-id="980af-774">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="980af-775">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Model</span><span class="sxs-lookup"><span data-stu-id="980af-775">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="980af-776">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;obiekt</span><span class="sxs-lookup"><span data-stu-id="980af-776">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="980af-777">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Typ obiektu: {Table}</font>
      </span><span class="sxs-lookup"><span data-stu-id="980af-777">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Table} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-778">SQL Server Reporting Services</span><span class="sxs-lookup"><span data-stu-id="980af-778">SQL Server Reporting Services</span></span></td>
      <td><span data-ttu-id="980af-779">Kontener</span><span class="sxs-lookup"><span data-stu-id="980af-779">Container</span></span></td>
      <td><span data-ttu-id="980af-780">Serwer</span><span class="sxs-lookup"><span data-stu-id="980af-780">Server</span></span></td>
      <td><span data-ttu-id="980af-781">
        <font size=2>Protokołów: usług raportowania</span><span class="sxs-lookup"><span data-stu-id="980af-781">
        <font size=2> Protocol: reporting-services</span></span> <br><span data-ttu-id="980af-782">Uwierzytelnianie: {windows}</span><span class="sxs-lookup"><span data-stu-id="980af-782">Authentication: {windows}</span></span> <br><span data-ttu-id="980af-783">Adres:</span><span class="sxs-lookup"><span data-stu-id="980af-783">Address:</span></span> <br><span data-ttu-id="980af-784">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Serwer</span><span class="sxs-lookup"><span data-stu-id="980af-784">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="980af-785">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Wersja: {ReportingService2010}</font>
      </span><span class="sxs-lookup"><span data-stu-id="980af-785">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version: {ReportingService2010} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-786">SQL Server Reporting Services</span><span class="sxs-lookup"><span data-stu-id="980af-786">SQL Server Reporting Services</span></span></td>
      <td><span data-ttu-id="980af-787">Raport</span><span class="sxs-lookup"><span data-stu-id="980af-787">Report</span></span></td>
      <td><span data-ttu-id="980af-788">Raport</span><span class="sxs-lookup"><span data-stu-id="980af-788">Report</span></span></td>
      <td><span data-ttu-id="980af-789">
        <font size=2>Protokołów: usług raportowania</span><span class="sxs-lookup"><span data-stu-id="980af-789">
        <font size=2> Protocol: reporting-services</span></span> <br><span data-ttu-id="980af-790">Uwierzytelnianie: {windows}</span><span class="sxs-lookup"><span data-stu-id="980af-790">Authentication: {windows}</span></span> <br><span data-ttu-id="980af-791">Adres:</span><span class="sxs-lookup"><span data-stu-id="980af-791">Address:</span></span> <br><span data-ttu-id="980af-792">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Serwer</span><span class="sxs-lookup"><span data-stu-id="980af-792">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="980af-793">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Ścieżka</span><span class="sxs-lookup"><span data-stu-id="980af-793">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; path</span></span> <br><span data-ttu-id="980af-794">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Wersja: {ReportingService2010}</font>
      </span><span class="sxs-lookup"><span data-stu-id="980af-794">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version: {ReportingService2010} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-795">Teradata</span><span class="sxs-lookup"><span data-stu-id="980af-795">Teradata</span></span></td>
      <td><span data-ttu-id="980af-796">Kontener</span><span class="sxs-lookup"><span data-stu-id="980af-796">Container</span></span></td>
      <td><span data-ttu-id="980af-797">Database (Baza danych)</span><span class="sxs-lookup"><span data-stu-id="980af-797">Database</span></span></td>
      <td><span data-ttu-id="980af-798">
        <font size=2>Protokół: teradata</span><span class="sxs-lookup"><span data-stu-id="980af-798">
        <font size=2> Protocol: teradata</span></span> <br><span data-ttu-id="980af-799">Uwierzytelnianie: {protokołu, windows}</span><span class="sxs-lookup"><span data-stu-id="980af-799">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="980af-800">Adres:</span><span class="sxs-lookup"><span data-stu-id="980af-800">Address:</span></span> <br><span data-ttu-id="980af-801">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Serwer</span><span class="sxs-lookup"><span data-stu-id="980af-801">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="980af-802">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bazy danych</font>
      </span><span class="sxs-lookup"><span data-stu-id="980af-802">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-803">Teradata</span><span class="sxs-lookup"><span data-stu-id="980af-803">Teradata</span></span></td>
      <td><span data-ttu-id="980af-804">Tabela</span><span class="sxs-lookup"><span data-stu-id="980af-804">Table</span></span></td>
      <td><span data-ttu-id="980af-805">Tabela, widok</span><span class="sxs-lookup"><span data-stu-id="980af-805">Table, view</span></span></td>
      <td><span data-ttu-id="980af-806">
        <font size=2>Protokół: teradata</span><span class="sxs-lookup"><span data-stu-id="980af-806">
        <font size=2> Protocol: teradata</span></span> <br><span data-ttu-id="980af-807">Uwierzytelnianie: {protokołu, windows}</span><span class="sxs-lookup"><span data-stu-id="980af-807">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="980af-808">Adres:</span><span class="sxs-lookup"><span data-stu-id="980af-808">Address:</span></span> <br><span data-ttu-id="980af-809">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Serwer</span><span class="sxs-lookup"><span data-stu-id="980af-809">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="980af-810">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bazy danych</span><span class="sxs-lookup"><span data-stu-id="980af-810">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="980af-811">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;obiekt</font>
      </span><span class="sxs-lookup"><span data-stu-id="980af-811">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-812">SQL Server Master Data Services</span><span class="sxs-lookup"><span data-stu-id="980af-812">SQL Server Master Data Services</span></span></td>
      <td><span data-ttu-id="980af-813">Kontener</span><span class="sxs-lookup"><span data-stu-id="980af-813">Container</span></span></td>
      <td><span data-ttu-id="980af-814">Model</span><span class="sxs-lookup"><span data-stu-id="980af-814">Model</span></span></td>
      <td><span data-ttu-id="980af-815">
        <font size="2">Protokół: mssql-mds</span><span class="sxs-lookup"><span data-stu-id="980af-815">
        <font size="2"> Protocol: mssql-mds</span></span> <br><span data-ttu-id="980af-816">Uwierzytelnianie: {windows}</span><span class="sxs-lookup"><span data-stu-id="980af-816">Authentication: {windows}</span></span> <br><span data-ttu-id="980af-817">Adres:</span><span class="sxs-lookup"><span data-stu-id="980af-817">Address:</span></span> <br><span data-ttu-id="980af-818">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;adres URL</span><span class="sxs-lookup"><span data-stu-id="980af-818">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span></span> <br><span data-ttu-id="980af-819">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Model</span><span class="sxs-lookup"><span data-stu-id="980af-819">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="980af-820">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Wersja</font>
      </span><span class="sxs-lookup"><span data-stu-id="980af-820">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-821">SQL Server Master Data Services</span><span class="sxs-lookup"><span data-stu-id="980af-821">SQL Server Master Data Services</span></span></td>
      <td><span data-ttu-id="980af-822">Tabela</span><span class="sxs-lookup"><span data-stu-id="980af-822">Table</span></span></td>
      <td><span data-ttu-id="980af-823">Jednostka</span><span class="sxs-lookup"><span data-stu-id="980af-823">Entity</span></span></td>
      <td><span data-ttu-id="980af-824">
        <font size="2">Protokół: mssql-mds</span><span class="sxs-lookup"><span data-stu-id="980af-824">
        <font size="2"> Protocol: mssql-mds</span></span> <br><span data-ttu-id="980af-825">Uwierzytelnianie: {windows}</span><span class="sxs-lookup"><span data-stu-id="980af-825">Authentication: {windows}</span></span> <br><span data-ttu-id="980af-826">Adres:</span><span class="sxs-lookup"><span data-stu-id="980af-826">Address:</span></span> <br><span data-ttu-id="980af-827">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;adres URL</span><span class="sxs-lookup"><span data-stu-id="980af-827">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span></span> <br><span data-ttu-id="980af-828">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Model</span><span class="sxs-lookup"><span data-stu-id="980af-828">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="980af-829">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Wersja</span><span class="sxs-lookup"><span data-stu-id="980af-829">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version</span></span> <br><span data-ttu-id="980af-830">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;jednostki</font>
      </span><span class="sxs-lookup"><span data-stu-id="980af-830">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; entity </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-831">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="980af-831">Azure Cosmos DB</span></span></td>
      <td><span data-ttu-id="980af-832">Kontener</span><span class="sxs-lookup"><span data-stu-id="980af-832">Container</span></span></td>
      <td><span data-ttu-id="980af-833">Database (Baza danych)</span><span class="sxs-lookup"><span data-stu-id="980af-833">Database</span></span></td>
      <td><span data-ttu-id="980af-834">
        <font size=2>Protokół: bazie danych dokumentów</span><span class="sxs-lookup"><span data-stu-id="980af-834">
        <font size=2> Protocol: document-db</span></span> <br><span data-ttu-id="980af-835">Uwierzytelnianie: {azure klawisza dostępu}</span><span class="sxs-lookup"><span data-stu-id="980af-835">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="980af-836">Adres:</span><span class="sxs-lookup"><span data-stu-id="980af-836">Address:</span></span> <br><span data-ttu-id="980af-837">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;adres URL</span><span class="sxs-lookup"><span data-stu-id="980af-837">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span></span> <br><span data-ttu-id="980af-838">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bazy danych</font>
      </span><span class="sxs-lookup"><span data-stu-id="980af-838">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-839">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="980af-839">Azure Cosmos DB</span></span></td>
      <td><span data-ttu-id="980af-840">Collection</span><span class="sxs-lookup"><span data-stu-id="980af-840">Collection</span></span></td>
      <td><span data-ttu-id="980af-841">Collection</span><span class="sxs-lookup"><span data-stu-id="980af-841">Collection</span></span></td>
      <td><span data-ttu-id="980af-842">
        <font size=2>Protokół: bazie danych dokumentów</span><span class="sxs-lookup"><span data-stu-id="980af-842">
        <font size=2> Protocol: document-db</span></span> <br><span data-ttu-id="980af-843">Uwierzytelnianie: {azure klawisza dostępu}</span><span class="sxs-lookup"><span data-stu-id="980af-843">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="980af-844">Adres:</span><span class="sxs-lookup"><span data-stu-id="980af-844">Address:</span></span> <br><span data-ttu-id="980af-845">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;adres URL</span><span class="sxs-lookup"><span data-stu-id="980af-845">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span></span> <br><span data-ttu-id="980af-846">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bazy danych</span><span class="sxs-lookup"><span data-stu-id="980af-846">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="980af-847">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Kolekcja</font>
      </span><span class="sxs-lookup"><span data-stu-id="980af-847">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; collection </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-848">Ogólne ODBC</span><span class="sxs-lookup"><span data-stu-id="980af-848">Generic ODBC</span></span></td>
      <td><span data-ttu-id="980af-849">Kontener</span><span class="sxs-lookup"><span data-stu-id="980af-849">Container</span></span></td>
      <td><span data-ttu-id="980af-850">Database (Baza danych)</span><span class="sxs-lookup"><span data-stu-id="980af-850">Database</span></span></td>
      <td><span data-ttu-id="980af-851">
        <font size=2>Protokół: odbc</span><span class="sxs-lookup"><span data-stu-id="980af-851">
        <font size=2> Protocol: odbc</span></span> <br><span data-ttu-id="980af-852">Uwierzytelnianie: {podstawowe, windows}</span><span class="sxs-lookup"><span data-stu-id="980af-852">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="980af-853">Adres:</span><span class="sxs-lookup"><span data-stu-id="980af-853">Address:</span></span> <br><span data-ttu-id="980af-854">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Opcje</span><span class="sxs-lookup"><span data-stu-id="980af-854">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; options</span></span> <br><span data-ttu-id="980af-855">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bazy danych</font>
      </span><span class="sxs-lookup"><span data-stu-id="980af-855">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-856">Ogólne ODBC</span><span class="sxs-lookup"><span data-stu-id="980af-856">Generic ODBC</span></span></td>
      <td><span data-ttu-id="980af-857">Tabela</span><span class="sxs-lookup"><span data-stu-id="980af-857">Table</span></span></td>
      <td><span data-ttu-id="980af-858">Tabela, widok</span><span class="sxs-lookup"><span data-stu-id="980af-858">Table, View</span></span></td>
      <td><span data-ttu-id="980af-859">
        <font size=2>Protokół: odbc</span><span class="sxs-lookup"><span data-stu-id="980af-859">
        <font size=2> Protocol: odbc</span></span> <br><span data-ttu-id="980af-860">Uwierzytelnianie: {podstawowe, windows}</span><span class="sxs-lookup"><span data-stu-id="980af-860">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="980af-861">Adres:</span><span class="sxs-lookup"><span data-stu-id="980af-861">Address:</span></span> <br><span data-ttu-id="980af-862">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Opcje</span><span class="sxs-lookup"><span data-stu-id="980af-862">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; options</span></span> <br><span data-ttu-id="980af-863">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bazy danych</span><span class="sxs-lookup"><span data-stu-id="980af-863">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="980af-864">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;obiekt</span><span class="sxs-lookup"><span data-stu-id="980af-864">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="980af-865">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Schemat</font>
      </span><span class="sxs-lookup"><span data-stu-id="980af-865">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-866">Sybase</span><span class="sxs-lookup"><span data-stu-id="980af-866">Sybase</span></span></td>
      <td><span data-ttu-id="980af-867">Kontener</span><span class="sxs-lookup"><span data-stu-id="980af-867">Container</span></span></td>
      <td><span data-ttu-id="980af-868">Database (Baza danych)</span><span class="sxs-lookup"><span data-stu-id="980af-868">Database</span></span></td>
      <td><span data-ttu-id="980af-869">
        <font size=2>Protokół: sybase</span><span class="sxs-lookup"><span data-stu-id="980af-869">
        <font size=2> protocol: sybase</span></span> <br><span data-ttu-id="980af-870">Uwierzytelnianie: {podstawowe, windows}</span><span class="sxs-lookup"><span data-stu-id="980af-870">authentication: {basic, windows}</span></span> <br><span data-ttu-id="980af-871">Adres:</span><span class="sxs-lookup"><span data-stu-id="980af-871">address:</span></span> <br><span data-ttu-id="980af-872">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Serwer</span><span class="sxs-lookup"><span data-stu-id="980af-872">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="980af-873">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bazy danych</font>
      </span><span class="sxs-lookup"><span data-stu-id="980af-873">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-874">Sybase</span><span class="sxs-lookup"><span data-stu-id="980af-874">Sybase</span></span></td>
      <td><span data-ttu-id="980af-875">Tabela</span><span class="sxs-lookup"><span data-stu-id="980af-875">Table</span></span></td>
      <td><span data-ttu-id="980af-876">Tabela, widok</span><span class="sxs-lookup"><span data-stu-id="980af-876">Table, View</span></span></td>
      <td><span data-ttu-id="980af-877">
        <font size=2>Protokół: sybase</span><span class="sxs-lookup"><span data-stu-id="980af-877">
        <font size=2> protocol: sybase</span></span> <br><span data-ttu-id="980af-878">Uwierzytelnianie: {podstawowe, windows}</span><span class="sxs-lookup"><span data-stu-id="980af-878">authentication: {basic, windows}</span></span> <br><span data-ttu-id="980af-879">Adres:</span><span class="sxs-lookup"><span data-stu-id="980af-879">address:</span></span> <br><span data-ttu-id="980af-880">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Serwer</span><span class="sxs-lookup"><span data-stu-id="980af-880">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="980af-881">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bazy danych</span><span class="sxs-lookup"><span data-stu-id="980af-881">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="980af-882">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Schemat</span><span class="sxs-lookup"><span data-stu-id="980af-882">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="980af-883">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;obiekt</font>
      </span><span class="sxs-lookup"><span data-stu-id="980af-883">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="980af-884">Inne (żadne z powyższych)</span><span class="sxs-lookup"><span data-stu-id="980af-884">Other (none of the above)</span></span></td>
      <td>\*</td>
      <td>\*</td>
      <td><span data-ttu-id="980af-885">
        <font size=2>Protokół: ogólny zasobów</span><span class="sxs-lookup"><span data-stu-id="980af-885">
        <font size=2> Protocol: generic-asset</span></span> <br><span data-ttu-id="980af-886">Adres:</span><span class="sxs-lookup"><span data-stu-id="980af-886">Address:</span></span> <br><span data-ttu-id="980af-887">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;assetId</font>
      </span><span class="sxs-lookup"><span data-stu-id="980af-887">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; assetId </font>
      </span></span></td>
    </tr>
</table>
