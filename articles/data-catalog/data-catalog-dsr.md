---
title: "aaaSupported źródeł danych w usłudze Azure Data Catalog | Dokumentacja firmy Microsoft"
description: "W tym artykule wymieniono specyfikacje źródeł danych hello obecnie obsługiwane."
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
ms.openlocfilehash: 4bfcabf31bf9fd781c939a5026abc42a5407df32
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="supported-data-sources-in-azure-data-catalog"></a><span data-ttu-id="98178-103">Obsługiwanych źródeł danych w wykazie danych Azure</span><span class="sxs-lookup"><span data-stu-id="98178-103">Supported data sources in Azure Data Catalog</span></span>

<span data-ttu-id="98178-104">Metadanych można opublikować za pomocą publiczny interfejs API lub przez kliknięcie — raz narzędzia rejestracji, lub ręcznie wprowadzając informacje bezpośrednio w portalu sieci web toohello Azure Data Catalog.</span><span class="sxs-lookup"><span data-stu-id="98178-104">You can publish metadata by using a public API or a click-once registration tool, or by manually entering information directly toohello Azure Data Catalog web portal.</span></span> <span data-ttu-id="98178-105">Witaj Poniższa tabela zawiera podsumowanie wszystkich źródeł danych, które są obecnie obsługiwane przez hello katalogu i hello możliwości publikowania dla każdego.</span><span class="sxs-lookup"><span data-stu-id="98178-105">hello following table summarizes all data sources that are supported by hello catalog today, and hello publishing capabilities for each.</span></span> <span data-ttu-id="98178-106">Liście są również hello danych zewnętrznych narzędzi, które każdego źródła danych można uruchomić na naszym doświadczeniu portal "Otwórz w".</span><span class="sxs-lookup"><span data-stu-id="98178-106">Also listed are hello external data tools that each data source can launch from our portal "open-in" experience.</span></span> <span data-ttu-id="98178-107">druga tabela Hello zawiera specyfikację techniczne każdej właściwości połączenia źródła danych.</span><span class="sxs-lookup"><span data-stu-id="98178-107">hello second table contains a more technical specification of each data-source connection property.</span></span>


## <a name="list-of-supported-data-sources"></a><span data-ttu-id="98178-108">Listę obsługiwanych źródeł danych</span><span class="sxs-lookup"><span data-stu-id="98178-108">List of supported data sources</span></span>

<table>
    <tr>
       <td><span data-ttu-id="98178-109"><b>Obiekt źródła danych</b></span><span class="sxs-lookup"><span data-stu-id="98178-109"><b>Data source object</b></span></span></td>
       <td><span data-ttu-id="98178-110"><b>Interfejs API</b></span><span class="sxs-lookup"><span data-stu-id="98178-110"><b>API</b></span></span></td>
       <td><span data-ttu-id="98178-111"><b>Ręczne wprowadzanie</b></span><span class="sxs-lookup"><span data-stu-id="98178-111"><b>Manual entry</b></span></span></td>
       <td><span data-ttu-id="98178-112"><b>Narzędzie do rejestracji</b></span><span class="sxs-lookup"><span data-stu-id="98178-112"><b>Registration tool</b></span></span></td>
       <td><span data-ttu-id="98178-113"><b>Otwórz w narzędziach</b></span><span class="sxs-lookup"><span data-stu-id="98178-113"><b>Open-in tools</b></span></span></td>
       <td><span data-ttu-id="98178-114"><b>Uwagi</b></span><span class="sxs-lookup"><span data-stu-id="98178-114"><b>Notes</b></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-115">Katalog usługi Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="98178-115">Azure Data Lake Store directory</span></span></td>
      <td><span data-ttu-id="98178-116">✓</span><span class="sxs-lookup"><span data-stu-id="98178-116">✓</span></span></td>
      <td><span data-ttu-id="98178-117">✓</span><span class="sxs-lookup"><span data-stu-id="98178-117">✓</span></span></td>
      <td><span data-ttu-id="98178-118">✓</span><span class="sxs-lookup"><span data-stu-id="98178-118">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-119">Azure Data Lake — magazyn plików</span><span class="sxs-lookup"><span data-stu-id="98178-119">Azure Data Lake Store file</span></span></td>
      <td><span data-ttu-id="98178-120">✓</span><span class="sxs-lookup"><span data-stu-id="98178-120">✓</span></span></td>
      <td><span data-ttu-id="98178-121">✓</span><span class="sxs-lookup"><span data-stu-id="98178-121">✓</span></span></td>
      <td><span data-ttu-id="98178-122">✓</span><span class="sxs-lookup"><span data-stu-id="98178-122">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-123">Azure Blob Storage</span><span class="sxs-lookup"><span data-stu-id="98178-123">Azure Blob storage</span></span></td>
      <td><span data-ttu-id="98178-124">✓</span><span class="sxs-lookup"><span data-stu-id="98178-124">✓</span></span></td>
      <td><span data-ttu-id="98178-125">✓</span><span class="sxs-lookup"><span data-stu-id="98178-125">✓</span></span></td>
      <td><span data-ttu-id="98178-126">✓</span><span class="sxs-lookup"><span data-stu-id="98178-126">✓</span></span></td>
      <td><span data-ttu-id="98178-127"><font size=2>Power BI</font></span><span class="sxs-lookup"><span data-stu-id="98178-127"><font size=2>Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-128">Katalog magazynu Azure</span><span class="sxs-lookup"><span data-stu-id="98178-128">Azure Storage directory</span></span></td>
      <td><span data-ttu-id="98178-129">✓</span><span class="sxs-lookup"><span data-stu-id="98178-129">✓</span></span></td>
      <td><span data-ttu-id="98178-130">✓</span><span class="sxs-lookup"><span data-stu-id="98178-130">✓</span></span></td>
      <td><span data-ttu-id="98178-131">✓</span><span class="sxs-lookup"><span data-stu-id="98178-131">✓</span></span></td>
      <td><span data-ttu-id="98178-132"><font size=2>Power BI</font></span><span class="sxs-lookup"><span data-stu-id="98178-132"><font size=2>Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-133">Tabela magazynu Azure</span><span class="sxs-lookup"><span data-stu-id="98178-133">Azure Storage table</span></span></td>
      <td><span data-ttu-id="98178-134">✓</span><span class="sxs-lookup"><span data-stu-id="98178-134">✓</span></span></td>
      <td><span data-ttu-id="98178-135">✓</span><span class="sxs-lookup"><span data-stu-id="98178-135">✓</span></span></td>
      <td><span data-ttu-id="98178-136">✓</span><span class="sxs-lookup"><span data-stu-id="98178-136">✓</span></span></td>
      <td>
        <font size="2"></font>
      </td>
      <td>
        <font size="2"></font>
      </td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-137">Katalog systemu plików HDFS</span><span class="sxs-lookup"><span data-stu-id="98178-137">HDFS directory</span></span></td>
      <td><span data-ttu-id="98178-138">✓</span><span class="sxs-lookup"><span data-stu-id="98178-138">✓</span></span></td>
      <td><span data-ttu-id="98178-139">✓</span><span class="sxs-lookup"><span data-stu-id="98178-139">✓</span></span></td>
      <td><span data-ttu-id="98178-140">✓</span><span class="sxs-lookup"><span data-stu-id="98178-140">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-141">System plików HDFS pliku</span><span class="sxs-lookup"><span data-stu-id="98178-141">HDFS file</span></span></td>
      <td><span data-ttu-id="98178-142">✓</span><span class="sxs-lookup"><span data-stu-id="98178-142">✓</span></span></td>
      <td><span data-ttu-id="98178-143">✓</span><span class="sxs-lookup"><span data-stu-id="98178-143">✓</span></span></td>
      <td><span data-ttu-id="98178-144">✓</span><span class="sxs-lookup"><span data-stu-id="98178-144">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-145">Tabelę programu hive</span><span class="sxs-lookup"><span data-stu-id="98178-145">Hive table</span></span></td>
      <td><span data-ttu-id="98178-146">✓</span><span class="sxs-lookup"><span data-stu-id="98178-146">✓</span></span></td>
      <td><span data-ttu-id="98178-147">✓</span><span class="sxs-lookup"><span data-stu-id="98178-147">✓</span></span></td>
      <td><span data-ttu-id="98178-148">✓</span><span class="sxs-lookup"><span data-stu-id="98178-148">✓</span></span></td>
      <td><span data-ttu-id="98178-149"><font size=2>Excel</font></span><span class="sxs-lookup"><span data-stu-id="98178-149"><font size=2>Excel</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-150">Widok gałęzi</span><span class="sxs-lookup"><span data-stu-id="98178-150">Hive view</span></span></td>
      <td><span data-ttu-id="98178-151">✓</span><span class="sxs-lookup"><span data-stu-id="98178-151">✓</span></span></td>
      <td><span data-ttu-id="98178-152">✓</span><span class="sxs-lookup"><span data-stu-id="98178-152">✓</span></span></td>
      <td><span data-ttu-id="98178-153">✓</span><span class="sxs-lookup"><span data-stu-id="98178-153">✓</span></span></td>
      <td><span data-ttu-id="98178-154"><font size=2>Excel</font></span><span class="sxs-lookup"><span data-stu-id="98178-154"><font size=2>Excel</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-155">Tabela MySQL</span><span class="sxs-lookup"><span data-stu-id="98178-155">MySQL table</span></span></td>
      <td><span data-ttu-id="98178-156">✓</span><span class="sxs-lookup"><span data-stu-id="98178-156">✓</span></span></td>
      <td><span data-ttu-id="98178-157">✓</span><span class="sxs-lookup"><span data-stu-id="98178-157">✓</span></span></td>
      <td><span data-ttu-id="98178-158">✓</span><span class="sxs-lookup"><span data-stu-id="98178-158">✓</span></span></td>
      <td><span data-ttu-id="98178-159"><font size=2>Program Excel, usłudze Power BI</font></span><span class="sxs-lookup"><span data-stu-id="98178-159"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-160">Widok MySQL</span><span class="sxs-lookup"><span data-stu-id="98178-160">MySQL view</span></span></td>
      <td><span data-ttu-id="98178-161">✓</span><span class="sxs-lookup"><span data-stu-id="98178-161">✓</span></span></td>
      <td><span data-ttu-id="98178-162">✓</span><span class="sxs-lookup"><span data-stu-id="98178-162">✓</span></span></td>
      <td><span data-ttu-id="98178-163">✓</span><span class="sxs-lookup"><span data-stu-id="98178-163">✓</span></span></td>
      <td><span data-ttu-id="98178-164"><font size=2>Program Excel, usłudze Power BI</font></span><span class="sxs-lookup"><span data-stu-id="98178-164"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-165">Tabela bazy danych programu Oracle</span><span class="sxs-lookup"><span data-stu-id="98178-165">Oracle Database table</span></span></td>
      <td><span data-ttu-id="98178-166">✓</span><span class="sxs-lookup"><span data-stu-id="98178-166">✓</span></span></td>
      <td><span data-ttu-id="98178-167">✓</span><span class="sxs-lookup"><span data-stu-id="98178-167">✓</span></span></td>
      <td><span data-ttu-id="98178-168">✓</span><span class="sxs-lookup"><span data-stu-id="98178-168">✓</span></span></td>
      <td><span data-ttu-id="98178-169"><font size=2>Program Excel, usłudze Power BI</font></span><span class="sxs-lookup"><span data-stu-id="98178-169"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-170">Widok bazy danych programu Oracle</span><span class="sxs-lookup"><span data-stu-id="98178-170">Oracle Database view</span></span></td>
      <td><span data-ttu-id="98178-171">✓</span><span class="sxs-lookup"><span data-stu-id="98178-171">✓</span></span></td>
      <td><span data-ttu-id="98178-172">✓</span><span class="sxs-lookup"><span data-stu-id="98178-172">✓</span></span></td>
      <td><span data-ttu-id="98178-173">✓</span><span class="sxs-lookup"><span data-stu-id="98178-173">✓</span></span></td>
      <td><span data-ttu-id="98178-174"><font size=2>Program Excel, usłudze Power BI</font></span><span class="sxs-lookup"><span data-stu-id="98178-174"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-175">Inne (ogólnego zasobów)</span><span class="sxs-lookup"><span data-stu-id="98178-175">Other (generic asset)</span></span></td>
      <td><span data-ttu-id="98178-176">✓</span><span class="sxs-lookup"><span data-stu-id="98178-176">✓</span></span></td>
      <td><span data-ttu-id="98178-177">✓</span><span class="sxs-lookup"><span data-stu-id="98178-177">✓</span></span></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-178">Tabela magazynu danych SQL Azure</span><span class="sxs-lookup"><span data-stu-id="98178-178">Azure SQL Data Warehouse table</span></span></td>
      <td><span data-ttu-id="98178-179">✓</span><span class="sxs-lookup"><span data-stu-id="98178-179">✓</span></span></td>
      <td><span data-ttu-id="98178-180">✓</span><span class="sxs-lookup"><span data-stu-id="98178-180">✓</span></span></td>
      <td><span data-ttu-id="98178-181">✓</span><span class="sxs-lookup"><span data-stu-id="98178-181">✓</span></span></td>
      <td><span data-ttu-id="98178-182"><font size=2>Narzędzia danych programu SQL Server programu Excel, usłudze Power BI</font></span><span class="sxs-lookup"><span data-stu-id="98178-182"><font size=2>Excel, Power BI, SQL Server data tools</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-183">Widok SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="98178-183">SQL Data Warehouse view</span></span></td>
      <td><span data-ttu-id="98178-184">✓</span><span class="sxs-lookup"><span data-stu-id="98178-184">✓</span></span></td>
      <td><span data-ttu-id="98178-185">✓</span><span class="sxs-lookup"><span data-stu-id="98178-185">✓</span></span></td>
      <td><span data-ttu-id="98178-186">✓</span><span class="sxs-lookup"><span data-stu-id="98178-186">✓</span></span></td>
      <td><span data-ttu-id="98178-187"><font size=2>Narzędzia danych programu SQL Server programu Excel, usłudze Power BI</font></span><span class="sxs-lookup"><span data-stu-id="98178-187"><font size=2>Excel, Power BI, SQL Server data tools</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-188">Wymiar usług SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="98178-188">SQL Server Analysis Services dimension</span></span></td>
      <td><span data-ttu-id="98178-189">✓</span><span class="sxs-lookup"><span data-stu-id="98178-189">✓</span></span></td>
      <td><span data-ttu-id="98178-190">✓</span><span class="sxs-lookup"><span data-stu-id="98178-190">✓</span></span></td>
      <td><span data-ttu-id="98178-191">✓</span><span class="sxs-lookup"><span data-stu-id="98178-191">✓</span></span></td>
      <td><span data-ttu-id="98178-192"><font size=2>Program Excel, usłudze Power BI</font></span><span class="sxs-lookup"><span data-stu-id="98178-192"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-193">SQL Server Analysis Services wskaźnika KPI</span><span class="sxs-lookup"><span data-stu-id="98178-193">SQL Server Analysis Services KPI</span></span></td>
      <td><span data-ttu-id="98178-194">✓</span><span class="sxs-lookup"><span data-stu-id="98178-194">✓</span></span></td>
      <td><span data-ttu-id="98178-195">✓</span><span class="sxs-lookup"><span data-stu-id="98178-195">✓</span></span></td>
      <td><span data-ttu-id="98178-196">✓</span><span class="sxs-lookup"><span data-stu-id="98178-196">✓</span></span></td>
      <td><span data-ttu-id="98178-197"><font size=2>Program Excel, usłudze Power BI</font></span><span class="sxs-lookup"><span data-stu-id="98178-197"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-198">Miara usług SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="98178-198">SQL Server Analysis Services measure</span></span></td>
      <td><span data-ttu-id="98178-199">✓</span><span class="sxs-lookup"><span data-stu-id="98178-199">✓</span></span></td>
      <td><span data-ttu-id="98178-200">✓</span><span class="sxs-lookup"><span data-stu-id="98178-200">✓</span></span></td>
      <td><span data-ttu-id="98178-201">✓</span><span class="sxs-lookup"><span data-stu-id="98178-201">✓</span></span></td>
      <td><span data-ttu-id="98178-202"><font size=2>Program Excel, usłudze Power BI</font></span><span class="sxs-lookup"><span data-stu-id="98178-202"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-203">Tabela SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="98178-203">SQL Server Analysis Services table</span></span></td>
      <td><span data-ttu-id="98178-204">✓</span><span class="sxs-lookup"><span data-stu-id="98178-204">✓</span></span></td>
      <td><span data-ttu-id="98178-205">✓</span><span class="sxs-lookup"><span data-stu-id="98178-205">✓</span></span></td>
      <td><span data-ttu-id="98178-206">✓</span><span class="sxs-lookup"><span data-stu-id="98178-206">✓</span></span></td>
      <td><span data-ttu-id="98178-207"><font size=2>Program Excel, usłudze Power BI</font></span><span class="sxs-lookup"><span data-stu-id="98178-207"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-208">Raport programu SQL Server Reporting Services</span><span class="sxs-lookup"><span data-stu-id="98178-208">SQL Server Reporting Services report</span></span></td>
      <td><span data-ttu-id="98178-209">✓</span><span class="sxs-lookup"><span data-stu-id="98178-209">✓</span></span></td>
      <td><span data-ttu-id="98178-210">✓</span><span class="sxs-lookup"><span data-stu-id="98178-210">✓</span></span></td>
      <td><span data-ttu-id="98178-211">✓</span><span class="sxs-lookup"><span data-stu-id="98178-211">✓</span></span></td>
      <td><span data-ttu-id="98178-212"><font size=2>Przeglądarka</font></span><span class="sxs-lookup"><span data-stu-id="98178-212"><font size=2>Browser</font></span></span></td>
      <td><span data-ttu-id="98178-213"><font size=2>Tylko serwerów w trybie macierzystym. Tryb programu SharePoint nie jest obsługiwany.</font></span><span class="sxs-lookup"><span data-stu-id="98178-213"><font size=2>Native mode servers only. SharePoint mode is not supported.</font></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-214">Tabeli programu SQL Server</span><span class="sxs-lookup"><span data-stu-id="98178-214">SQL Server table</span></span></td>
      <td><span data-ttu-id="98178-215">✓</span><span class="sxs-lookup"><span data-stu-id="98178-215">✓</span></span></td>
      <td><span data-ttu-id="98178-216">✓</span><span class="sxs-lookup"><span data-stu-id="98178-216">✓</span></span></td>
      <td><span data-ttu-id="98178-217">✓</span><span class="sxs-lookup"><span data-stu-id="98178-217">✓</span></span></td>
      <td><span data-ttu-id="98178-218"><font size=2>Narzędzia danych programu SQL Server programu Excel, usłudze Power BI</font></span><span class="sxs-lookup"><span data-stu-id="98178-218"><font size=2>Excel, Power BI, SQL Server data tools</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-219">Widok SQL Server</span><span class="sxs-lookup"><span data-stu-id="98178-219">SQL Server view</span></span></td>
      <td><span data-ttu-id="98178-220">✓</span><span class="sxs-lookup"><span data-stu-id="98178-220">✓</span></span></td>
      <td><span data-ttu-id="98178-221">✓</span><span class="sxs-lookup"><span data-stu-id="98178-221">✓</span></span></td>
      <td><span data-ttu-id="98178-222">✓</span><span class="sxs-lookup"><span data-stu-id="98178-222">✓</span></span></td>
      <td><span data-ttu-id="98178-223"><font size=2>Narzędzia danych programu SQL Server programu Excel, usłudze Power BI</font></span><span class="sxs-lookup"><span data-stu-id="98178-223"><font size=2>Excel, Power BI, SQL Server data tools</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-224">Tabela programu Teradata</span><span class="sxs-lookup"><span data-stu-id="98178-224">Teradata table</span></span></td>
      <td><span data-ttu-id="98178-225">✓</span><span class="sxs-lookup"><span data-stu-id="98178-225">✓</span></span></td>
      <td><span data-ttu-id="98178-226">✓</span><span class="sxs-lookup"><span data-stu-id="98178-226">✓</span></span></td>
      <td><span data-ttu-id="98178-227">✓</span><span class="sxs-lookup"><span data-stu-id="98178-227">✓</span></span></td>
      <td><span data-ttu-id="98178-228"><font size=2>Excel</font></span><span class="sxs-lookup"><span data-stu-id="98178-228"><font size=2>Excel</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-229">Widok programu Teradata</span><span class="sxs-lookup"><span data-stu-id="98178-229">Teradata view</span></span></td>
      <td><span data-ttu-id="98178-230">✓</span><span class="sxs-lookup"><span data-stu-id="98178-230">✓</span></span></td>
      <td><span data-ttu-id="98178-231">✓</span><span class="sxs-lookup"><span data-stu-id="98178-231">✓</span></span></td>
      <td><span data-ttu-id="98178-232">✓</span><span class="sxs-lookup"><span data-stu-id="98178-232">✓</span></span></td>
      <td><span data-ttu-id="98178-233"><font size=2>Excel</font></span><span class="sxs-lookup"><span data-stu-id="98178-233"><font size=2>Excel</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-234">Widok SAP HANA</span><span class="sxs-lookup"><span data-stu-id="98178-234">SAP HANA view</span></span></td>
      <td><span data-ttu-id="98178-235">✓</span><span class="sxs-lookup"><span data-stu-id="98178-235">✓</span></span></td>
      <td><span data-ttu-id="98178-236">✓</span><span class="sxs-lookup"><span data-stu-id="98178-236">✓</span></span></td>
      <td><span data-ttu-id="98178-237">✓</span><span class="sxs-lookup"><span data-stu-id="98178-237">✓</span></span></td>
      <td><span data-ttu-id="98178-238"><font size=2>Power BI</font></span><span class="sxs-lookup"><span data-stu-id="98178-238"><font size=2>Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-239">Tabela bazy danych DB2</span><span class="sxs-lookup"><span data-stu-id="98178-239">DB2 table</span></span></td>
      <td><span data-ttu-id="98178-240">✓</span><span class="sxs-lookup"><span data-stu-id="98178-240">✓</span></span></td>
      <td><span data-ttu-id="98178-241">✓</span><span class="sxs-lookup"><span data-stu-id="98178-241">✓</span></span></td>
      <td><span data-ttu-id="98178-242">✓</span><span class="sxs-lookup"><span data-stu-id="98178-242">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-243">Widok bazy danych DB2</span><span class="sxs-lookup"><span data-stu-id="98178-243">DB2 view</span></span></td>
      <td><span data-ttu-id="98178-244">✓</span><span class="sxs-lookup"><span data-stu-id="98178-244">✓</span></span></td>
      <td><span data-ttu-id="98178-245">✓</span><span class="sxs-lookup"><span data-stu-id="98178-245">✓</span></span></td>
      <td><span data-ttu-id="98178-246">✓</span><span class="sxs-lookup"><span data-stu-id="98178-246">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-247">Pliku</span><span class="sxs-lookup"><span data-stu-id="98178-247">File system file</span></span></td>
      <td><span data-ttu-id="98178-248">✓</span><span class="sxs-lookup"><span data-stu-id="98178-248">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-249">Katalogu FTP</span><span class="sxs-lookup"><span data-stu-id="98178-249">FTP directory</span></span></td>
      <td><span data-ttu-id="98178-250">✓</span><span class="sxs-lookup"><span data-stu-id="98178-250">✓</span></span></td>
      <td><span data-ttu-id="98178-251">✓</span><span class="sxs-lookup"><span data-stu-id="98178-251">✓</span></span></td>
      <td><span data-ttu-id="98178-252">✓</span><span class="sxs-lookup"><span data-stu-id="98178-252">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-253">Plik FTP</span><span class="sxs-lookup"><span data-stu-id="98178-253">FTP file</span></span></td>
      <td><span data-ttu-id="98178-254">✓</span><span class="sxs-lookup"><span data-stu-id="98178-254">✓</span></span></td>
      <td><span data-ttu-id="98178-255">✓</span><span class="sxs-lookup"><span data-stu-id="98178-255">✓</span></span></td>
      <td><span data-ttu-id="98178-256">✓</span><span class="sxs-lookup"><span data-stu-id="98178-256">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-257">Raport HTTP</span><span class="sxs-lookup"><span data-stu-id="98178-257">HTTP report</span></span></td>
      <td><span data-ttu-id="98178-258">✓</span><span class="sxs-lookup"><span data-stu-id="98178-258">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-259">Punkt końcowy HTTP</span><span class="sxs-lookup"><span data-stu-id="98178-259">HTTP endpoint</span></span></td>
      <td><span data-ttu-id="98178-260">✓</span><span class="sxs-lookup"><span data-stu-id="98178-260">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-261">Plik HTTP</span><span class="sxs-lookup"><span data-stu-id="98178-261">HTTP file</span></span></td>
      <td><span data-ttu-id="98178-262">✓</span><span class="sxs-lookup"><span data-stu-id="98178-262">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-263">Zestaw jednostek OData</span><span class="sxs-lookup"><span data-stu-id="98178-263">OData entity set</span></span></td>
      <td><span data-ttu-id="98178-264">✓</span><span class="sxs-lookup"><span data-stu-id="98178-264">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-265">Funkcję OData</span><span class="sxs-lookup"><span data-stu-id="98178-265">OData function</span></span></td>
      <td><span data-ttu-id="98178-266">✓</span><span class="sxs-lookup"><span data-stu-id="98178-266">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-267">Tabela PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="98178-267">PostgreSQL table</span></span></td>
      <td><span data-ttu-id="98178-268">✓</span><span class="sxs-lookup"><span data-stu-id="98178-268">✓</span></span></td>
      <td><span data-ttu-id="98178-269">✓</span><span class="sxs-lookup"><span data-stu-id="98178-269">✓</span></span></td>
      <td><span data-ttu-id="98178-270">✓</span><span class="sxs-lookup"><span data-stu-id="98178-270">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-271">Widok PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="98178-271">PostgreSQL view</span></span></td>
      <td><span data-ttu-id="98178-272">✓</span><span class="sxs-lookup"><span data-stu-id="98178-272">✓</span></span></td>
      <td><span data-ttu-id="98178-273">✓</span><span class="sxs-lookup"><span data-stu-id="98178-273">✓</span></span></td>
      <td><span data-ttu-id="98178-274">✓</span><span class="sxs-lookup"><span data-stu-id="98178-274">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-275">Widok SAP HANA</span><span class="sxs-lookup"><span data-stu-id="98178-275">SAP HANA view</span></span></td>
      <td><span data-ttu-id="98178-276">✓</span><span class="sxs-lookup"><span data-stu-id="98178-276">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td> <span data-ttu-id="98178-277">Obiekt SalesForce</span><span class="sxs-lookup"><span data-stu-id="98178-277">Salesforce object</span></span></td>
      <td><span data-ttu-id="98178-278">✓</span><span class="sxs-lookup"><span data-stu-id="98178-278">✓</span></span></td>
      <td><span data-ttu-id="98178-279">✓</span><span class="sxs-lookup"><span data-stu-id="98178-279">✓</span></span></td>
      <td><span data-ttu-id="98178-280">✓</span><span class="sxs-lookup"><span data-stu-id="98178-280">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-281">Listy programu SharePoint</span><span class="sxs-lookup"><span data-stu-id="98178-281">SharePoint list</span></span> </td>
      <td><span data-ttu-id="98178-282">✓</span><span class="sxs-lookup"><span data-stu-id="98178-282">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-283">Azure DB rozwiązania Cosmos kolekcji</span><span class="sxs-lookup"><span data-stu-id="98178-283">Azure Cosmos DB collection</span></span></td>
      <td><span data-ttu-id="98178-284">✓</span><span class="sxs-lookup"><span data-stu-id="98178-284">✓</span></span></td>
      <td><span data-ttu-id="98178-285">✓</span><span class="sxs-lookup"><span data-stu-id="98178-285">✓</span></span></td>
      <td><span data-ttu-id="98178-286">✓</span><span class="sxs-lookup"><span data-stu-id="98178-286">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-287">Ogólny tabeli ODBC</span><span class="sxs-lookup"><span data-stu-id="98178-287">Generic ODBC table</span></span></td>
      <td><span data-ttu-id="98178-288">✓</span><span class="sxs-lookup"><span data-stu-id="98178-288">✓</span></span></td>
      <td><span data-ttu-id="98178-289">✓</span><span class="sxs-lookup"><span data-stu-id="98178-289">✓</span></span></td>
      <td><span data-ttu-id="98178-290">✓</span><span class="sxs-lookup"><span data-stu-id="98178-290">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-291">Ogólny widok ODBC</span><span class="sxs-lookup"><span data-stu-id="98178-291">Generic ODBC view</span></span></td>
      <td><span data-ttu-id="98178-292">✓</span><span class="sxs-lookup"><span data-stu-id="98178-292">✓</span></span></td>
      <td><span data-ttu-id="98178-293">✓</span><span class="sxs-lookup"><span data-stu-id="98178-293">✓</span></span></td>
      <td><span data-ttu-id="98178-294">✓</span><span class="sxs-lookup"><span data-stu-id="98178-294">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-295">Tabela Cassandra</span><span class="sxs-lookup"><span data-stu-id="98178-295">Cassandra table</span></span></td>
      <td><span data-ttu-id="98178-296">✓</span><span class="sxs-lookup"><span data-stu-id="98178-296">✓</span></span></td>
      <td><span data-ttu-id="98178-297">✓</span><span class="sxs-lookup"><span data-stu-id="98178-297">✓</span></span></td>
      <td><span data-ttu-id="98178-298">✓</span><span class="sxs-lookup"><span data-stu-id="98178-298">✓</span></span></td>
      <td><font size=2></font></td>
      <td><span data-ttu-id="98178-299"><font size=2>Publikuj jako ogólnego zasobów ODBC</font></span><span class="sxs-lookup"><span data-stu-id="98178-299"><font size=2>Publish as a generic ODBC asset</font></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-300">Widok Cassandra</span><span class="sxs-lookup"><span data-stu-id="98178-300">Cassandra view</span></span></td>
      <td><span data-ttu-id="98178-301">✓</span><span class="sxs-lookup"><span data-stu-id="98178-301">✓</span></span></td>
      <td><span data-ttu-id="98178-302">✓</span><span class="sxs-lookup"><span data-stu-id="98178-302">✓</span></span></td>
      <td><span data-ttu-id="98178-303">✓</span><span class="sxs-lookup"><span data-stu-id="98178-303">✓</span></span></td>
      <td><font size=2></font></td>
      <td><span data-ttu-id="98178-304"><font size=2>Publikuj jako ogólnego zasobów ODBC</font></span><span class="sxs-lookup"><span data-stu-id="98178-304"><font size=2>Publish as a generic ODBC asset</font></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-305">Tabela programu Sybase</span><span class="sxs-lookup"><span data-stu-id="98178-305">Sybase table</span></span></td>
      <td><span data-ttu-id="98178-306">✓</span><span class="sxs-lookup"><span data-stu-id="98178-306">✓</span></span></td>
      <td><span data-ttu-id="98178-307">✓</span><span class="sxs-lookup"><span data-stu-id="98178-307">✓</span></span></td>
      <td><span data-ttu-id="98178-308">✓</span><span class="sxs-lookup"><span data-stu-id="98178-308">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-309">Widok programu Sybase</span><span class="sxs-lookup"><span data-stu-id="98178-309">Sybase view</span></span></td>
      <td><span data-ttu-id="98178-310">✓</span><span class="sxs-lookup"><span data-stu-id="98178-310">✓</span></span></td>
      <td><span data-ttu-id="98178-311">✓</span><span class="sxs-lookup"><span data-stu-id="98178-311">✓</span></span></td>
      <td><span data-ttu-id="98178-312">✓</span><span class="sxs-lookup"><span data-stu-id="98178-312">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-313">Tabela bazy danych MongoDB</span><span class="sxs-lookup"><span data-stu-id="98178-313">MongoDB table</span></span></td>
      <td><span data-ttu-id="98178-314">✓</span><span class="sxs-lookup"><span data-stu-id="98178-314">✓</span></span></td>
      <td><span data-ttu-id="98178-315">✓</span><span class="sxs-lookup"><span data-stu-id="98178-315">✓</span></span></td>
      <td><span data-ttu-id="98178-316">✓</span><span class="sxs-lookup"><span data-stu-id="98178-316">✓</span></span></td>
      <td><font size=2></font></td>
      <td><span data-ttu-id="98178-317"><font size=2>Publikuj jako ogólnego zasobów ODBC</font></span><span class="sxs-lookup"><span data-stu-id="98178-317"><font size=2>Publish as a generic ODBC asset</font></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-318">Widok bazy danych MongoDB</span><span class="sxs-lookup"><span data-stu-id="98178-318">MongoDB view</span></span></td>
      <td><span data-ttu-id="98178-319">✓</span><span class="sxs-lookup"><span data-stu-id="98178-319">✓</span></span></td>
      <td><span data-ttu-id="98178-320">✓</span><span class="sxs-lookup"><span data-stu-id="98178-320">✓</span></span></td>
      <td><span data-ttu-id="98178-321">✓</span><span class="sxs-lookup"><span data-stu-id="98178-321">✓</span></span></td>
      <td><font size=2></font></td>
      <td><span data-ttu-id="98178-322"><font size=2>Publikuj jako ogólnego zasobów ODBC</font></span><span class="sxs-lookup"><span data-stu-id="98178-322"><font size=2>Publish as a generic ODBC asset</font></span></span></td>
    </tr>
</table>

<span data-ttu-id="98178-323">Jeśli potrzebujesz pomocy technicznej dla dodatkowych źródeł, przesłać toohello żądania funkcji [forum usługi Azure Data Catalog](http://go.microsoft.com/fwlink/?LinkID=616424&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="98178-323">If you need support for additional sources, submit a feature request toohello [Azure Data Catalog forum](http://go.microsoft.com/fwlink/?LinkID=616424&clcid=0x409).</span></span>


## <a name="data-source-reference-specification"></a><span data-ttu-id="98178-324">Specyfikacja odwołanie do źródła danych</span><span class="sxs-lookup"><span data-stu-id="98178-324">Data-source reference specification</span></span>
> [!NOTE]
> <span data-ttu-id="98178-325">Witaj **struktury DSL** w hello w poniższej tabeli wymieniono tylko hello właściwości połączenia dla zbioru właściwości "address" używane przez usługi Azure Data Catalog.</span><span class="sxs-lookup"><span data-stu-id="98178-325">hello **DSL structure** column in hello following table lists only hello connection properties for "address" property bag that are used by Azure Data Catalog.</span></span> <span data-ttu-id="98178-326">Oznacza to zbiór właściwości "address" może zawierać innych właściwości połączenia źródła danych hello Azure Data Catalog będzie się powtarzać, ale nie używa.</span><span class="sxs-lookup"><span data-stu-id="98178-326">That is, "address" property bag can contain other connection properties of hello data source which Azure Data Catalog persists, but does not use.</span></span>

<table>
    <tr>
       <td><span data-ttu-id="98178-327"><b>Typ źródła</b></span><span class="sxs-lookup"><span data-stu-id="98178-327"><b>Source type</b></span></span></td>
       <td><span data-ttu-id="98178-328"><b>Typ zasobu</b></span><span class="sxs-lookup"><span data-stu-id="98178-328"><b>Asset type</b></span></span></td>
       <td><span data-ttu-id="98178-329"><b>Typy obiektów</b></span><span class="sxs-lookup"><span data-stu-id="98178-329"><b>Object types</b></span></span></td>
       <td><span data-ttu-id="98178-330"><b>Struktura DSL<b></span><span class="sxs-lookup"><span data-stu-id="98178-330"><b>DSL structure<b></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-331">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="98178-331">Azure Data Lake Store</span></span></td>
      <td><span data-ttu-id="98178-332">Kontener</span><span class="sxs-lookup"><span data-stu-id="98178-332">Container</span></span></td>
      <td><span data-ttu-id="98178-333">Data Lake</span><span class="sxs-lookup"><span data-stu-id="98178-333">Data Lake</span></span></td>
      <td><span data-ttu-id="98178-334">
        <font size=2>Protokół: webhdfs</span><span class="sxs-lookup"><span data-stu-id="98178-334">
        <font size=2> Protocol: webhdfs</span></span> <br><span data-ttu-id="98178-335">Uwierzytelnianie: {podstawowe, oauth}</span><span class="sxs-lookup"><span data-stu-id="98178-335">Authentication: {basic, oauth}</span></span> <br><span data-ttu-id="98178-336">Adres:</span><span class="sxs-lookup"><span data-stu-id="98178-336">Address:</span></span> <br><span data-ttu-id="98178-337">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;adres URL</font>
      </span><span class="sxs-lookup"><span data-stu-id="98178-337">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-338">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="98178-338">Azure Data Lake Store</span></span></td>
      <td><span data-ttu-id="98178-339">Tabela</span><span class="sxs-lookup"><span data-stu-id="98178-339">Table</span></span></td>
      <td><span data-ttu-id="98178-340">Plik w katalogu</span><span class="sxs-lookup"><span data-stu-id="98178-340">Directory, file</span></span></td>
      <td><span data-ttu-id="98178-341">
        <font size=2>Protokół: webhdfs</span><span class="sxs-lookup"><span data-stu-id="98178-341">
        <font size=2> Protocol: webhdfs</span></span> <br><span data-ttu-id="98178-342">Uwierzytelnianie: {podstawowe, oauth}</span><span class="sxs-lookup"><span data-stu-id="98178-342">Authentication: {basic, oauth}</span></span> <br><span data-ttu-id="98178-343">Adres:</span><span class="sxs-lookup"><span data-stu-id="98178-343">Address:</span></span> <br><span data-ttu-id="98178-344">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;adres URL</font>
      </span><span class="sxs-lookup"><span data-stu-id="98178-344">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-345">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="98178-345">Azure Storage</span></span></td>
      <td><span data-ttu-id="98178-346">Kontener</span><span class="sxs-lookup"><span data-stu-id="98178-346">Container</span></span></td>
      <td><span data-ttu-id="98178-347">Kontener</span><span class="sxs-lookup"><span data-stu-id="98178-347">Container</span></span></td>
      <td><span data-ttu-id="98178-348">
        <font size=2>Protokół: obiektach blob azure</span><span class="sxs-lookup"><span data-stu-id="98178-348">
        <font size=2> Protocol: azure-blobs</span></span> <br><span data-ttu-id="98178-349">Uwierzytelnianie: {azure klawisza dostępu}</span><span class="sxs-lookup"><span data-stu-id="98178-349">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="98178-350">Adres:</span><span class="sxs-lookup"><span data-stu-id="98178-350">Address:</span></span> <br><span data-ttu-id="98178-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;domeny</span><span class="sxs-lookup"><span data-stu-id="98178-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span></span> <br><span data-ttu-id="98178-352">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;konta</span><span class="sxs-lookup"><span data-stu-id="98178-352">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account</span></span> <br><span data-ttu-id="98178-353">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;kontener</font>
      </span><span class="sxs-lookup"><span data-stu-id="98178-353">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; container </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-354">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="98178-354">Azure Storage</span></span></td>
      <td><span data-ttu-id="98178-355">Tabela</span><span class="sxs-lookup"><span data-stu-id="98178-355">Table</span></span></td>
      <td><span data-ttu-id="98178-356">Obiekt blob, katalogu</span><span class="sxs-lookup"><span data-stu-id="98178-356">Blob, directory</span></span></td>
      <td><span data-ttu-id="98178-357">
        <font size=2>Protokół: obiektach blob azure</span><span class="sxs-lookup"><span data-stu-id="98178-357">
        <font size=2> Protocol: azure-blobs</span></span> <br><span data-ttu-id="98178-358">Uwierzytelnianie: {azure klawisza dostępu}</span><span class="sxs-lookup"><span data-stu-id="98178-358">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="98178-359">Adres:</span><span class="sxs-lookup"><span data-stu-id="98178-359">Address:</span></span> <br><span data-ttu-id="98178-360">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;domeny</span><span class="sxs-lookup"><span data-stu-id="98178-360">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span></span> <br><span data-ttu-id="98178-361">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;konta</span><span class="sxs-lookup"><span data-stu-id="98178-361">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account</span></span> <br><span data-ttu-id="98178-362">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;kontener</span><span class="sxs-lookup"><span data-stu-id="98178-362">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; container</span></span> <br><span data-ttu-id="98178-363">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Nazwa</font>
      </span><span class="sxs-lookup"><span data-stu-id="98178-363">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; name </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-364">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="98178-364">Azure Storage</span></span></td>
      <td><span data-ttu-id="98178-365">Kontener</span><span class="sxs-lookup"><span data-stu-id="98178-365">Container</span></span></td>
      <td><span data-ttu-id="98178-366">Kontener</span><span class="sxs-lookup"><span data-stu-id="98178-366">Container</span></span></td>
      <td><span data-ttu-id="98178-367">
        <font size=2>Protokół: azure — tabele</span><span class="sxs-lookup"><span data-stu-id="98178-367">
        <font size=2> Protocol: azure-tables</span></span> <br><span data-ttu-id="98178-368">Uwierzytelnianie: {azure klawisza dostępu}</span><span class="sxs-lookup"><span data-stu-id="98178-368">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="98178-369">Adres:</span><span class="sxs-lookup"><span data-stu-id="98178-369">Address:</span></span> <br><span data-ttu-id="98178-370">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;domeny</span><span class="sxs-lookup"><span data-stu-id="98178-370">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span></span> <br><span data-ttu-id="98178-371">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;konta</font>
      </span><span class="sxs-lookup"><span data-stu-id="98178-371">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-372">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="98178-372">Azure Storage</span></span></td>
      <td><span data-ttu-id="98178-373">Tabela</span><span class="sxs-lookup"><span data-stu-id="98178-373">Table</span></span></td>
      <td><span data-ttu-id="98178-374">Tabela</span><span class="sxs-lookup"><span data-stu-id="98178-374">Table</span></span></td>
      <td><span data-ttu-id="98178-375">
        <font size=2>Protokół: azure — tabele</span><span class="sxs-lookup"><span data-stu-id="98178-375">
        <font size=2> Protocol: azure-tables</span></span> <br><span data-ttu-id="98178-376">Uwierzytelnianie: {azure klawisza dostępu}</span><span class="sxs-lookup"><span data-stu-id="98178-376">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="98178-377">Adres:</span><span class="sxs-lookup"><span data-stu-id="98178-377">Address:</span></span> <br><span data-ttu-id="98178-378">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;domeny</span><span class="sxs-lookup"><span data-stu-id="98178-378">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span></span> <br><span data-ttu-id="98178-379">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;konta</span><span class="sxs-lookup"><span data-stu-id="98178-379">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account</span></span> <br><span data-ttu-id="98178-380">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Nazwa</font>
      </span><span class="sxs-lookup"><span data-stu-id="98178-380">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; name </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-381">Rozwiązania cosmos</span><span class="sxs-lookup"><span data-stu-id="98178-381">Cosmos</span></span></td>
      <td><span data-ttu-id="98178-382">Kontener</span><span class="sxs-lookup"><span data-stu-id="98178-382">Container</span></span></td>
      <td><span data-ttu-id="98178-383">Klaster wirtualny</span><span class="sxs-lookup"><span data-stu-id="98178-383">Virtual cluster</span></span></td>
      <td><span data-ttu-id="98178-384">
        <font size=2>Protokół: rozwiązania cosmos</span><span class="sxs-lookup"><span data-stu-id="98178-384">
        <font size=2> Protocol: cosmos</span></span> <br><span data-ttu-id="98178-385">Uwierzytelnianie: {podstawowe, windows}</span><span class="sxs-lookup"><span data-stu-id="98178-385">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="98178-386">Adres:</span><span class="sxs-lookup"><span data-stu-id="98178-386">Address:</span></span> <br><span data-ttu-id="98178-387">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;adres URL</font>
      </span><span class="sxs-lookup"><span data-stu-id="98178-387">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-388">Rozwiązania cosmos</span><span class="sxs-lookup"><span data-stu-id="98178-388">Cosmos</span></span></td>
      <td><span data-ttu-id="98178-389">Tabela</span><span class="sxs-lookup"><span data-stu-id="98178-389">Table</span></span></td>
      <td><span data-ttu-id="98178-390">Strumień, zestaw strumienia widoku</span><span class="sxs-lookup"><span data-stu-id="98178-390">Stream, stream set, view</span></span></td>
      <td><span data-ttu-id="98178-391">
        <font size=2>Protokół: rozwiązania cosmos</span><span class="sxs-lookup"><span data-stu-id="98178-391">
        <font size=2> Protocol: cosmos</span></span> <br><span data-ttu-id="98178-392">Uwierzytelnianie: {podstawowe, windows}</span><span class="sxs-lookup"><span data-stu-id="98178-392">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="98178-393">Adres:</span><span class="sxs-lookup"><span data-stu-id="98178-393">Address:</span></span> <br><span data-ttu-id="98178-394">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;adres URL</font>
      </span><span class="sxs-lookup"><span data-stu-id="98178-394">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-395">Datazen</span><span class="sxs-lookup"><span data-stu-id="98178-395">Datazen</span></span></td>
      <td><span data-ttu-id="98178-396">Kontener</span><span class="sxs-lookup"><span data-stu-id="98178-396">Container</span></span></td>
      <td><span data-ttu-id="98178-397">Lokacji</span><span class="sxs-lookup"><span data-stu-id="98178-397">Site</span></span></td>
      <td><span data-ttu-id="98178-398">
        <font size=2>Protokół: http</span><span class="sxs-lookup"><span data-stu-id="98178-398">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="98178-399">Uwierzytelnianie: {none, basic, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="98178-399">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="98178-400">Adres:</span><span class="sxs-lookup"><span data-stu-id="98178-400">Address:</span></span> <br><span data-ttu-id="98178-401">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;adres URL</font>
      </span><span class="sxs-lookup"><span data-stu-id="98178-401">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-402">Datazen</span><span class="sxs-lookup"><span data-stu-id="98178-402">Datazen</span></span></td>
      <td><span data-ttu-id="98178-403">Raport</span><span class="sxs-lookup"><span data-stu-id="98178-403">Report</span></span></td>
      <td><span data-ttu-id="98178-404">Raport, pulpit nawigacyjny</span><span class="sxs-lookup"><span data-stu-id="98178-404">Report, dashboard</span></span></td>
      <td><span data-ttu-id="98178-405">
        <font size=2>Protokół: http</span><span class="sxs-lookup"><span data-stu-id="98178-405">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="98178-406">Uwierzytelnianie: {none, basic, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="98178-406">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="98178-407">Adres:</span><span class="sxs-lookup"><span data-stu-id="98178-407">Address:</span></span> <br><span data-ttu-id="98178-408">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;adres URL</font>
      </span><span class="sxs-lookup"><span data-stu-id="98178-408">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-409">DB2</span><span class="sxs-lookup"><span data-stu-id="98178-409">DB2</span></span></td>
      <td><span data-ttu-id="98178-410">Kontener</span><span class="sxs-lookup"><span data-stu-id="98178-410">Container</span></span></td>
      <td><span data-ttu-id="98178-411">Database (Baza danych)</span><span class="sxs-lookup"><span data-stu-id="98178-411">Database</span></span></td>
      <td><span data-ttu-id="98178-412">
        <font size=2>Protokół: bazy danych db2</span><span class="sxs-lookup"><span data-stu-id="98178-412">
        <font size=2> Protocol: db2</span></span> <br><span data-ttu-id="98178-413">Uwierzytelnianie: {podstawowe, windows}</span><span class="sxs-lookup"><span data-stu-id="98178-413">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="98178-414">Adres:</span><span class="sxs-lookup"><span data-stu-id="98178-414">Address:</span></span> <br><span data-ttu-id="98178-415">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Serwer</span><span class="sxs-lookup"><span data-stu-id="98178-415">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="98178-416">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bazy danych</font>
      </span><span class="sxs-lookup"><span data-stu-id="98178-416">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-417">DB2</span><span class="sxs-lookup"><span data-stu-id="98178-417">DB2</span></span></td>
      <td><span data-ttu-id="98178-418">Tabela</span><span class="sxs-lookup"><span data-stu-id="98178-418">Table</span></span></td>
      <td><span data-ttu-id="98178-419">Tabela, widok</span><span class="sxs-lookup"><span data-stu-id="98178-419">Table, view</span></span></td>
      <td><span data-ttu-id="98178-420">
        <font size=2>Protokół: bazy danych db2</span><span class="sxs-lookup"><span data-stu-id="98178-420">
        <font size=2> Protocol: db2</span></span> <br><span data-ttu-id="98178-421">Uwierzytelnianie: {podstawowe, windows}</span><span class="sxs-lookup"><span data-stu-id="98178-421">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="98178-422">Adres:</span><span class="sxs-lookup"><span data-stu-id="98178-422">Address:</span></span> <br><span data-ttu-id="98178-423">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Serwer</span><span class="sxs-lookup"><span data-stu-id="98178-423">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="98178-424">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bazy danych</span><span class="sxs-lookup"><span data-stu-id="98178-424">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="98178-425">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;obiekt</span><span class="sxs-lookup"><span data-stu-id="98178-425">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="98178-426">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Schemat</font>
      </span><span class="sxs-lookup"><span data-stu-id="98178-426">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-427">System plików</span><span class="sxs-lookup"><span data-stu-id="98178-427">File system</span></span></td>
      <td><span data-ttu-id="98178-428">Tabela</span><span class="sxs-lookup"><span data-stu-id="98178-428">Table</span></span></td>
      <td><span data-ttu-id="98178-429">Plik</span><span class="sxs-lookup"><span data-stu-id="98178-429">File</span></span></td>
      <td><span data-ttu-id="98178-430">
        <font size=2>Protokół: plik</span><span class="sxs-lookup"><span data-stu-id="98178-430">
        <font size=2> Protocol: file</span></span> <br><span data-ttu-id="98178-431">Uwierzytelnianie: {none, basic, windows}</span><span class="sxs-lookup"><span data-stu-id="98178-431">Authentication: {none, basic, windows}</span></span> <br><span data-ttu-id="98178-432">Adres:</span><span class="sxs-lookup"><span data-stu-id="98178-432">Address:</span></span> <br><span data-ttu-id="98178-433">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Ścieżka</font>
      </span><span class="sxs-lookup"><span data-stu-id="98178-433">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; path </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-434">FTP</span><span class="sxs-lookup"><span data-stu-id="98178-434">FTP</span></span></td>
      <td><span data-ttu-id="98178-435">Tabela</span><span class="sxs-lookup"><span data-stu-id="98178-435">Table</span></span></td>
      <td><span data-ttu-id="98178-436">Plik w katalogu</span><span class="sxs-lookup"><span data-stu-id="98178-436">Directory, file</span></span></td>
      <td><span data-ttu-id="98178-437">
        <font size=2>Protokół: ftp</span><span class="sxs-lookup"><span data-stu-id="98178-437">
        <font size=2> Protocol: ftp</span></span> <br><span data-ttu-id="98178-438">Uwierzytelnianie: {none, basic, windows}</span><span class="sxs-lookup"><span data-stu-id="98178-438">Authentication: {none, basic, windows}</span></span> <br><span data-ttu-id="98178-439">Adres:</span><span class="sxs-lookup"><span data-stu-id="98178-439">Address:</span></span> <br><span data-ttu-id="98178-440">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;adres URL</font>
      </span><span class="sxs-lookup"><span data-stu-id="98178-440">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-441">Hadoop rozproszonego systemu plików</span><span class="sxs-lookup"><span data-stu-id="98178-441">Hadoop Distributed File System</span></span></td>
      <td><span data-ttu-id="98178-442">Kontener</span><span class="sxs-lookup"><span data-stu-id="98178-442">Container</span></span></td>
      <td><span data-ttu-id="98178-443">Klaster</span><span class="sxs-lookup"><span data-stu-id="98178-443">Cluster</span></span></td>
      <td><span data-ttu-id="98178-444">
        <font size=2>Protokół: webhdfs</span><span class="sxs-lookup"><span data-stu-id="98178-444">
        <font size=2> Protocol: webhdfs</span></span> <br><span data-ttu-id="98178-445">Uwierzytelnianie: {podstawowe, oauth}</span><span class="sxs-lookup"><span data-stu-id="98178-445">Authentication: {basic, oauth}</span></span> <br><span data-ttu-id="98178-446">Adres:</span><span class="sxs-lookup"><span data-stu-id="98178-446">Address:</span></span> <br><span data-ttu-id="98178-447">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;adres URL</font>
      </span><span class="sxs-lookup"><span data-stu-id="98178-447">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-448">Hadoop rozproszonego systemu plików</span><span class="sxs-lookup"><span data-stu-id="98178-448">Hadoop Distributed File System</span></span></td>
      <td><span data-ttu-id="98178-449">Tabela</span><span class="sxs-lookup"><span data-stu-id="98178-449">Table</span></span></td>
      <td><span data-ttu-id="98178-450">Plik w katalogu</span><span class="sxs-lookup"><span data-stu-id="98178-450">Directory, file</span></span></td>
      <td><span data-ttu-id="98178-451">
        <font size=2>Protokół: webhdfs</span><span class="sxs-lookup"><span data-stu-id="98178-451">
        <font size=2> Protocol: webhdfs</span></span> <br><span data-ttu-id="98178-452">Uwierzytelnianie: {podstawowe, oauth}</span><span class="sxs-lookup"><span data-stu-id="98178-452">Authentication: {basic, oauth}</span></span> <br><span data-ttu-id="98178-453">Adres:</span><span class="sxs-lookup"><span data-stu-id="98178-453">Address:</span></span> <br><span data-ttu-id="98178-454">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;adres URL</font>
      </span><span class="sxs-lookup"><span data-stu-id="98178-454">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-455">Hive</span><span class="sxs-lookup"><span data-stu-id="98178-455">Hive</span></span></td>
      <td><span data-ttu-id="98178-456">Kontener</span><span class="sxs-lookup"><span data-stu-id="98178-456">Container</span></span></td>
      <td><span data-ttu-id="98178-457">Database (Baza danych)</span><span class="sxs-lookup"><span data-stu-id="98178-457">Database</span></span></td>
      <td><span data-ttu-id="98178-458">
        <font size=2>Protokół: gałęzi</span><span class="sxs-lookup"><span data-stu-id="98178-458">
        <font size=2> Protocol: hive</span></span> <br><span data-ttu-id="98178-459">Uwierzytelnianie: {HDInsight, basic, username, Brak}</span><span class="sxs-lookup"><span data-stu-id="98178-459">Authentication: {HDInsight, basic, username, none}</span></span> <br><span data-ttu-id="98178-460">Adres:</span><span class="sxs-lookup"><span data-stu-id="98178-460">Address:</span></span> <br><span data-ttu-id="98178-461">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Serwer</span><span class="sxs-lookup"><span data-stu-id="98178-461">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="98178-462">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bazy danych</span><span class="sxs-lookup"><span data-stu-id="98178-462">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="98178-463">connectionProperties:</span><span class="sxs-lookup"><span data-stu-id="98178-463">connectionProperties:</span></span> <br><span data-ttu-id="98178-464">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;serverProtocol: {hive2}</font>
      </span><span class="sxs-lookup"><span data-stu-id="98178-464">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; serverProtocol: {hive2} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-465">Hive</span><span class="sxs-lookup"><span data-stu-id="98178-465">Hive</span></span></td>
      <td><span data-ttu-id="98178-466">Tabela</span><span class="sxs-lookup"><span data-stu-id="98178-466">Table</span></span></td>
      <td><span data-ttu-id="98178-467">Tabela, widok</span><span class="sxs-lookup"><span data-stu-id="98178-467">Table, view</span></span></td>
      <td><span data-ttu-id="98178-468">
        <font size=2>Protokół: gałęzi</span><span class="sxs-lookup"><span data-stu-id="98178-468">
        <font size=2> Protocol: hive</span></span> <br><span data-ttu-id="98178-469">Uwierzytelnianie: {HDInsight, basic, username, Brak}</span><span class="sxs-lookup"><span data-stu-id="98178-469">Authentication: {HDInsight, basic, username, none}</span></span> <br><span data-ttu-id="98178-470">Adres:</span><span class="sxs-lookup"><span data-stu-id="98178-470">Address:</span></span> <br><span data-ttu-id="98178-471">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Serwer</span><span class="sxs-lookup"><span data-stu-id="98178-471">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="98178-472">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bazy danych</span><span class="sxs-lookup"><span data-stu-id="98178-472">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="98178-473">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;obiekt</span><span class="sxs-lookup"><span data-stu-id="98178-473">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="98178-474">connectionProperties:</span><span class="sxs-lookup"><span data-stu-id="98178-474">connectionProperties:</span></span> <br><span data-ttu-id="98178-475">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;serverProtocol: {hive2}</font>
      </span><span class="sxs-lookup"><span data-stu-id="98178-475">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; serverProtocol: {hive2} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-476">HTTP</span><span class="sxs-lookup"><span data-stu-id="98178-476">HTTP</span></span></td>
      <td><span data-ttu-id="98178-477">Kontener</span><span class="sxs-lookup"><span data-stu-id="98178-477">Container</span></span></td>
      <td><span data-ttu-id="98178-478">Lokacji</span><span class="sxs-lookup"><span data-stu-id="98178-478">Site</span></span></td>
      <td><span data-ttu-id="98178-479">
        <font size=2>Protokół: http</span><span class="sxs-lookup"><span data-stu-id="98178-479">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="98178-480">Uwierzytelnianie: {none, basic, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="98178-480">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="98178-481">Adres:</span><span class="sxs-lookup"><span data-stu-id="98178-481">Address:</span></span> <br><span data-ttu-id="98178-482">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;adres URL</font>
      </span><span class="sxs-lookup"><span data-stu-id="98178-482">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-483">HTTP</span><span class="sxs-lookup"><span data-stu-id="98178-483">HTTP</span></span></td>
      <td><span data-ttu-id="98178-484">Raport</span><span class="sxs-lookup"><span data-stu-id="98178-484">Report</span></span></td>
      <td><span data-ttu-id="98178-485">Raport, pulpit nawigacyjny</span><span class="sxs-lookup"><span data-stu-id="98178-485">Report, dashboard</span></span></td>
      <td><span data-ttu-id="98178-486">
        <font size=2>Protokół: http</span><span class="sxs-lookup"><span data-stu-id="98178-486">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="98178-487">Uwierzytelnianie: {none, basic, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="98178-487">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="98178-488">Adres:</span><span class="sxs-lookup"><span data-stu-id="98178-488">Address:</span></span> <br><span data-ttu-id="98178-489">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;adres URL</font>
      </span><span class="sxs-lookup"><span data-stu-id="98178-489">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-490">HTTP</span><span class="sxs-lookup"><span data-stu-id="98178-490">HTTP</span></span></td>
      <td><span data-ttu-id="98178-491">Tabela</span><span class="sxs-lookup"><span data-stu-id="98178-491">Table</span></span></td>
      <td><span data-ttu-id="98178-492">Punkt końcowy, plik</span><span class="sxs-lookup"><span data-stu-id="98178-492">Endpoint, file</span></span></td>
      <td><span data-ttu-id="98178-493">
        <font size=2>Protokół: http</span><span class="sxs-lookup"><span data-stu-id="98178-493">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="98178-494">Uwierzytelnianie: {none, basic, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="98178-494">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="98178-495">Adres:</span><span class="sxs-lookup"><span data-stu-id="98178-495">Address:</span></span> <br><span data-ttu-id="98178-496">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;adres URL</font>
      </span><span class="sxs-lookup"><span data-stu-id="98178-496">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-497">MySQL</span><span class="sxs-lookup"><span data-stu-id="98178-497">MySQL</span></span></td>
      <td><span data-ttu-id="98178-498">Kontener</span><span class="sxs-lookup"><span data-stu-id="98178-498">Container</span></span></td>
      <td><span data-ttu-id="98178-499">Database (Baza danych)</span><span class="sxs-lookup"><span data-stu-id="98178-499">Database</span></span></td>
      <td><span data-ttu-id="98178-500">
        <font size=2>Protokół: mysql</span><span class="sxs-lookup"><span data-stu-id="98178-500">
        <font size=2> Protocol: mysql</span></span> <br><span data-ttu-id="98178-501">Uwierzytelnianie: {protokołu, windows}</span><span class="sxs-lookup"><span data-stu-id="98178-501">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="98178-502">Adres:</span><span class="sxs-lookup"><span data-stu-id="98178-502">Address:</span></span> <br><span data-ttu-id="98178-503">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Serwer</span><span class="sxs-lookup"><span data-stu-id="98178-503">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="98178-504">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bazy danych</font>
      </span><span class="sxs-lookup"><span data-stu-id="98178-504">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-505">MySQL</span><span class="sxs-lookup"><span data-stu-id="98178-505">MySQL</span></span></td>
      <td><span data-ttu-id="98178-506">Tabela</span><span class="sxs-lookup"><span data-stu-id="98178-506">Table</span></span></td>
      <td><span data-ttu-id="98178-507">Tabela, widok</span><span class="sxs-lookup"><span data-stu-id="98178-507">Table, view</span></span></td>
      <td><span data-ttu-id="98178-508">
        <font size=2>Protokół: mysql</span><span class="sxs-lookup"><span data-stu-id="98178-508">
        <font size=2> Protocol: mysql</span></span> <br><span data-ttu-id="98178-509">Uwierzytelnianie: {protokołu, windows}</span><span class="sxs-lookup"><span data-stu-id="98178-509">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="98178-510">Adres:</span><span class="sxs-lookup"><span data-stu-id="98178-510">Address:</span></span> <br><span data-ttu-id="98178-511">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Serwer</span><span class="sxs-lookup"><span data-stu-id="98178-511">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="98178-512">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bazy danych</span><span class="sxs-lookup"><span data-stu-id="98178-512">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="98178-513">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;obiekt</font>
      </span><span class="sxs-lookup"><span data-stu-id="98178-513">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-514">OData</span><span class="sxs-lookup"><span data-stu-id="98178-514">OData</span></span></td>
      <td><span data-ttu-id="98178-515">Kontener</span><span class="sxs-lookup"><span data-stu-id="98178-515">Container</span></span></td>
      <td><span data-ttu-id="98178-516">Kontenera jednostek</span><span class="sxs-lookup"><span data-stu-id="98178-516">Entity container</span></span></td>
      <td><span data-ttu-id="98178-517">
        <font size=2>Protokół: odata</span><span class="sxs-lookup"><span data-stu-id="98178-517">
        <font size=2> Protocol: odata</span></span> <br><span data-ttu-id="98178-518">Uwierzytelnianie: {none, basic, windows}</span><span class="sxs-lookup"><span data-stu-id="98178-518">Authentication: {none, basic, windows}</span></span> <br><span data-ttu-id="98178-519">Adres:</span><span class="sxs-lookup"><span data-stu-id="98178-519">Address:</span></span> <br><span data-ttu-id="98178-520">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;adres URL</font>
      </span><span class="sxs-lookup"><span data-stu-id="98178-520">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-521">OData</span><span class="sxs-lookup"><span data-stu-id="98178-521">OData</span></span></td>
      <td><span data-ttu-id="98178-522">Tabela</span><span class="sxs-lookup"><span data-stu-id="98178-522">Table</span></span></td>
      <td><span data-ttu-id="98178-523">Zestaw jednostek, funkcja</span><span class="sxs-lookup"><span data-stu-id="98178-523">Entity set, function</span></span></td>
      <td><span data-ttu-id="98178-524">
        <font size=2>Protokół: odata</span><span class="sxs-lookup"><span data-stu-id="98178-524">
        <font size=2> Protocol: odata</span></span> <br><span data-ttu-id="98178-525">Uwierzytelnianie: {none, basic, windows}</span><span class="sxs-lookup"><span data-stu-id="98178-525">Authentication: {none, basic, windows}</span></span> <br><span data-ttu-id="98178-526">Adres:</span><span class="sxs-lookup"><span data-stu-id="98178-526">Address:</span></span> <br><span data-ttu-id="98178-527">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;adres URL</span><span class="sxs-lookup"><span data-stu-id="98178-527">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span></span> <br><span data-ttu-id="98178-528">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;zasobów</font>
      </span><span class="sxs-lookup"><span data-stu-id="98178-528">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; resource </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-529">Baza danych Oracle</span><span class="sxs-lookup"><span data-stu-id="98178-529">Oracle Database</span></span></td>
      <td><span data-ttu-id="98178-530">Kontener</span><span class="sxs-lookup"><span data-stu-id="98178-530">Container</span></span></td>
      <td><span data-ttu-id="98178-531">Database (Baza danych)</span><span class="sxs-lookup"><span data-stu-id="98178-531">Database</span></span></td>
      <td><span data-ttu-id="98178-532">
        <font size=2>Protokół: oracle</span><span class="sxs-lookup"><span data-stu-id="98178-532">
        <font size=2> Protocol: oracle</span></span> <br><span data-ttu-id="98178-533">Uwierzytelnianie: {protokołu, windows}</span><span class="sxs-lookup"><span data-stu-id="98178-533">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="98178-534">Adres:</span><span class="sxs-lookup"><span data-stu-id="98178-534">Address:</span></span> <br><span data-ttu-id="98178-535">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Serwer</span><span class="sxs-lookup"><span data-stu-id="98178-535">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="98178-536">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bazy danych</font>
      </span><span class="sxs-lookup"><span data-stu-id="98178-536">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-537">Baza danych Oracle</span><span class="sxs-lookup"><span data-stu-id="98178-537">Oracle Database</span></span></td>
      <td><span data-ttu-id="98178-538">Tabela</span><span class="sxs-lookup"><span data-stu-id="98178-538">Table</span></span></td>
      <td><span data-ttu-id="98178-539">Tabela, widok</span><span class="sxs-lookup"><span data-stu-id="98178-539">Table, view</span></span></td>
      <td><span data-ttu-id="98178-540">
        <font size=2>Protokół: oracle</span><span class="sxs-lookup"><span data-stu-id="98178-540">
        <font size=2> Protocol: oracle</span></span> <br><span data-ttu-id="98178-541">Uwierzytelnianie: {protokołu, windows}</span><span class="sxs-lookup"><span data-stu-id="98178-541">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="98178-542">Adres:</span><span class="sxs-lookup"><span data-stu-id="98178-542">Address:</span></span> <br><span data-ttu-id="98178-543">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Serwer</span><span class="sxs-lookup"><span data-stu-id="98178-543">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="98178-544">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bazy danych</span><span class="sxs-lookup"><span data-stu-id="98178-544">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="98178-545">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Schemat</span><span class="sxs-lookup"><span data-stu-id="98178-545">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="98178-546">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;obiekt</font>
      </span><span class="sxs-lookup"><span data-stu-id="98178-546">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-547">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="98178-547">PostgreSQL</span></span></td>
      <td><span data-ttu-id="98178-548">Kontener</span><span class="sxs-lookup"><span data-stu-id="98178-548">Container</span></span></td>
      <td><span data-ttu-id="98178-549">Database (Baza danych)</span><span class="sxs-lookup"><span data-stu-id="98178-549">Database</span></span></td>
      <td><span data-ttu-id="98178-550">
        <font size=2>Protokół: postgresql</span><span class="sxs-lookup"><span data-stu-id="98178-550">
        <font size=2> Protocol: postgresql</span></span> <br><span data-ttu-id="98178-551">Uwierzytelnianie: {podstawowe, windows}</span><span class="sxs-lookup"><span data-stu-id="98178-551">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="98178-552">Adres:</span><span class="sxs-lookup"><span data-stu-id="98178-552">Address:</span></span> <br><span data-ttu-id="98178-553">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Serwer</span><span class="sxs-lookup"><span data-stu-id="98178-553">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="98178-554">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bazy danych</font>
      </span><span class="sxs-lookup"><span data-stu-id="98178-554">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-555">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="98178-555">PostgreSQL</span></span></td>
      <td><span data-ttu-id="98178-556">Tabela</span><span class="sxs-lookup"><span data-stu-id="98178-556">Table</span></span></td>
      <td><span data-ttu-id="98178-557">Tabela, widok</span><span class="sxs-lookup"><span data-stu-id="98178-557">Table, view</span></span></td>
      <td><span data-ttu-id="98178-558">
        <font size=2>Protokół: postgresql</span><span class="sxs-lookup"><span data-stu-id="98178-558">
        <font size=2> Protocol: postgresql</span></span> <br><span data-ttu-id="98178-559">Uwierzytelnianie: {podstawowe, windows}</span><span class="sxs-lookup"><span data-stu-id="98178-559">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="98178-560">Adres:</span><span class="sxs-lookup"><span data-stu-id="98178-560">Address:</span></span> <br><span data-ttu-id="98178-561">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Serwer</span><span class="sxs-lookup"><span data-stu-id="98178-561">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="98178-562">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bazy danych</span><span class="sxs-lookup"><span data-stu-id="98178-562">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="98178-563">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Schemat</span><span class="sxs-lookup"><span data-stu-id="98178-563">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="98178-564">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;obiekt</font>
      </span><span class="sxs-lookup"><span data-stu-id="98178-564">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-565">Power BI</span><span class="sxs-lookup"><span data-stu-id="98178-565">Power BI</span></span></td>
      <td><span data-ttu-id="98178-566">Kontener</span><span class="sxs-lookup"><span data-stu-id="98178-566">Container</span></span></td>
      <td><span data-ttu-id="98178-567">Lokacji</span><span class="sxs-lookup"><span data-stu-id="98178-567">Site</span></span></td>
      <td><span data-ttu-id="98178-568">
        <font size=2>Protokół: http</span><span class="sxs-lookup"><span data-stu-id="98178-568">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="98178-569">Uwierzytelnianie: {none, basic, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="98178-569">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="98178-570">Adres:</span><span class="sxs-lookup"><span data-stu-id="98178-570">Address:</span></span> <br><span data-ttu-id="98178-571">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;adres URL</font>
      </span><span class="sxs-lookup"><span data-stu-id="98178-571">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-572">Power BI</span><span class="sxs-lookup"><span data-stu-id="98178-572">Power BI</span></span></td>
      <td><span data-ttu-id="98178-573">Raport</span><span class="sxs-lookup"><span data-stu-id="98178-573">Report</span></span></td>
      <td><span data-ttu-id="98178-574">Raport, pulpit nawigacyjny</span><span class="sxs-lookup"><span data-stu-id="98178-574">Report, dashboard</span></span></td>
      <td><span data-ttu-id="98178-575">
        <font size=2>Protokół: http</span><span class="sxs-lookup"><span data-stu-id="98178-575">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="98178-576">Uwierzytelnianie: {none, basic, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="98178-576">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="98178-577">Adres:</span><span class="sxs-lookup"><span data-stu-id="98178-577">Address:</span></span> <br><span data-ttu-id="98178-578">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;adres URL</font>
      </span><span class="sxs-lookup"><span data-stu-id="98178-578">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-579">Dodatek Power Query</span><span class="sxs-lookup"><span data-stu-id="98178-579">Power Query</span></span></td>
      <td><span data-ttu-id="98178-580">Tabela</span><span class="sxs-lookup"><span data-stu-id="98178-580">Table</span></span></td>
      <td><span data-ttu-id="98178-581">Dane zestawu połączonych danych</span><span class="sxs-lookup"><span data-stu-id="98178-581">Data mashup</span></span></td>
      <td><span data-ttu-id="98178-582">
        <font size=2>Protokół: dodatku power query</span><span class="sxs-lookup"><span data-stu-id="98178-582">
        <font size=2> Protocol: power-query</span></span> <br><span data-ttu-id="98178-583">Uwierzytelnianie: {oauth}</span><span class="sxs-lookup"><span data-stu-id="98178-583">Authentication: {oauth}</span></span> <br><span data-ttu-id="98178-584">Adres:</span><span class="sxs-lookup"><span data-stu-id="98178-584">Address:</span></span> <br><span data-ttu-id="98178-585">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;adres URL</font>
      </span><span class="sxs-lookup"><span data-stu-id="98178-585">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-586">SalesForce</span><span class="sxs-lookup"><span data-stu-id="98178-586">Salesforce</span></span></td>
      <td><span data-ttu-id="98178-587">Tabela</span><span class="sxs-lookup"><span data-stu-id="98178-587">Table</span></span></td>
      <td><span data-ttu-id="98178-588">Obiekt</span><span class="sxs-lookup"><span data-stu-id="98178-588">Object</span></span></td>
      <td><span data-ttu-id="98178-589">
        <font size=2>Protokół: salesforce-com</span><span class="sxs-lookup"><span data-stu-id="98178-589">
        <font size=2> Protocol: salesforce-com</span></span> <br><span data-ttu-id="98178-590">Uwierzytelnianie: {podstawowe, windows}</span><span class="sxs-lookup"><span data-stu-id="98178-590">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="98178-591">Adres:</span><span class="sxs-lookup"><span data-stu-id="98178-591">Address:</span></span> <br><span data-ttu-id="98178-592">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;loginServer</span><span class="sxs-lookup"><span data-stu-id="98178-592">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; loginServer</span></span> <br><span data-ttu-id="98178-593">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;klasy</span><span class="sxs-lookup"><span data-stu-id="98178-593">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; class</span></span> <br><span data-ttu-id="98178-594">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Nazwa elementu</font>
      </span><span class="sxs-lookup"><span data-stu-id="98178-594">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; itemName </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-595">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="98178-595">SAP HANA</span></span></td>
      <td><span data-ttu-id="98178-596">Kontener</span><span class="sxs-lookup"><span data-stu-id="98178-596">Container</span></span></td>
      <td><span data-ttu-id="98178-597">Serwer</span><span class="sxs-lookup"><span data-stu-id="98178-597">Server</span></span></td>
      <td><span data-ttu-id="98178-598">
        <font size=2>Protokół: sap hana-sql</span><span class="sxs-lookup"><span data-stu-id="98178-598">
        <font size=2> Protocol: sap-hana-sql</span></span> <br><span data-ttu-id="98178-599">Uwierzytelnianie: {protokołu, windows}</span><span class="sxs-lookup"><span data-stu-id="98178-599">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="98178-600">Adres:</span><span class="sxs-lookup"><span data-stu-id="98178-600">Address:</span></span> <br><span data-ttu-id="98178-601">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Serwer</font>
      </span><span class="sxs-lookup"><span data-stu-id="98178-601">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-602">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="98178-602">SAP HANA</span></span></td>
      <td><span data-ttu-id="98178-603">Tabela</span><span class="sxs-lookup"><span data-stu-id="98178-603">Table</span></span></td>
      <td><span data-ttu-id="98178-604">Widok</span><span class="sxs-lookup"><span data-stu-id="98178-604">View</span></span></td>
      <td><span data-ttu-id="98178-605">
        <font size=2>Protokół: sap hana-sql</span><span class="sxs-lookup"><span data-stu-id="98178-605">
        <font size=2> Protocol: sap-hana-sql</span></span> <br><span data-ttu-id="98178-606">Uwierzytelnianie: {protokołu, windows}</span><span class="sxs-lookup"><span data-stu-id="98178-606">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="98178-607">Adres:</span><span class="sxs-lookup"><span data-stu-id="98178-607">Address:</span></span> <br><span data-ttu-id="98178-608">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Serwer</span><span class="sxs-lookup"><span data-stu-id="98178-608">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="98178-609">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Schemat</span><span class="sxs-lookup"><span data-stu-id="98178-609">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="98178-610">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;obiekt</font>
      </span><span class="sxs-lookup"><span data-stu-id="98178-610">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-611">Sharepoint</span><span class="sxs-lookup"><span data-stu-id="98178-611">SharePoint</span></span></td>
      <td><span data-ttu-id="98178-612">Tabela</span><span class="sxs-lookup"><span data-stu-id="98178-612">Table</span></span></td>
      <td><span data-ttu-id="98178-613">List</span><span class="sxs-lookup"><span data-stu-id="98178-613">List</span></span></td>
      <td><span data-ttu-id="98178-614">
        <font size=2>Protokołów: listy programu sharepoint</span><span class="sxs-lookup"><span data-stu-id="98178-614">
        <font size=2> Protocol: sharepoint-list</span></span> <br><span data-ttu-id="98178-615">Uwierzytelnianie: {podstawowe, windows}</span><span class="sxs-lookup"><span data-stu-id="98178-615">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="98178-616">Adres:</span><span class="sxs-lookup"><span data-stu-id="98178-616">Address:</span></span> <br><span data-ttu-id="98178-617">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;adres URL</font>
      </span><span class="sxs-lookup"><span data-stu-id="98178-617">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-618">Magazyn danych SQL</span><span class="sxs-lookup"><span data-stu-id="98178-618">SQL Data Warehouse</span></span></td>
      <td><span data-ttu-id="98178-619">Polecenie</span><span class="sxs-lookup"><span data-stu-id="98178-619">Command</span></span></td>
      <td><span data-ttu-id="98178-620">Procedura składowana</span><span class="sxs-lookup"><span data-stu-id="98178-620">Stored procedure</span></span></td>
      <td><span data-ttu-id="98178-621">
        <font size=2>Protokół: tds</span><span class="sxs-lookup"><span data-stu-id="98178-621">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="98178-622">Uwierzytelnianie: {protokołu, windows}</span><span class="sxs-lookup"><span data-stu-id="98178-622">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="98178-623">Adres:</span><span class="sxs-lookup"><span data-stu-id="98178-623">Address:</span></span> <br><span data-ttu-id="98178-624">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Serwer</span><span class="sxs-lookup"><span data-stu-id="98178-624">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="98178-625">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bazy danych</span><span class="sxs-lookup"><span data-stu-id="98178-625">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="98178-626">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Schemat</span><span class="sxs-lookup"><span data-stu-id="98178-626">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="98178-627">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;obiekt</font>
      </span><span class="sxs-lookup"><span data-stu-id="98178-627">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-628">Magazyn danych SQL</span><span class="sxs-lookup"><span data-stu-id="98178-628">SQL Data Warehouse</span></span></td>
      <td><span data-ttu-id="98178-629">TableValuedFunction</span><span class="sxs-lookup"><span data-stu-id="98178-629">TableValuedFunction</span></span></td>
      <td><span data-ttu-id="98178-630">Funkcja zwracająca tabelę</span><span class="sxs-lookup"><span data-stu-id="98178-630">Table-valued function</span></span></td>
      <td><span data-ttu-id="98178-631">
        <font size=2>Protokół: tds</span><span class="sxs-lookup"><span data-stu-id="98178-631">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="98178-632">Uwierzytelnianie: {protokołu, windows}</span><span class="sxs-lookup"><span data-stu-id="98178-632">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="98178-633">Adres:</span><span class="sxs-lookup"><span data-stu-id="98178-633">Address:</span></span> <br><span data-ttu-id="98178-634">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Serwer</span><span class="sxs-lookup"><span data-stu-id="98178-634">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="98178-635">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bazy danych</span><span class="sxs-lookup"><span data-stu-id="98178-635">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="98178-636">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Schemat</span><span class="sxs-lookup"><span data-stu-id="98178-636">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="98178-637">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;obiekt</font>
      </span><span class="sxs-lookup"><span data-stu-id="98178-637">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-638">Magazyn danych SQL</span><span class="sxs-lookup"><span data-stu-id="98178-638">SQL Data Warehouse</span></span></td>
      <td><span data-ttu-id="98178-639">Kontener</span><span class="sxs-lookup"><span data-stu-id="98178-639">Container</span></span></td>
      <td><span data-ttu-id="98178-640">Database (Baza danych)</span><span class="sxs-lookup"><span data-stu-id="98178-640">Database</span></span></td>
      <td><span data-ttu-id="98178-641">
        <font size=2>Protokół: tds</span><span class="sxs-lookup"><span data-stu-id="98178-641">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="98178-642">Uwierzytelnianie: {protokołu, windows}</span><span class="sxs-lookup"><span data-stu-id="98178-642">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="98178-643">Adres:</span><span class="sxs-lookup"><span data-stu-id="98178-643">Address:</span></span> <br><span data-ttu-id="98178-644">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Serwer</span><span class="sxs-lookup"><span data-stu-id="98178-644">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="98178-645">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bazy danych</font>
      </span><span class="sxs-lookup"><span data-stu-id="98178-645">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-646">Magazyn danych SQL</span><span class="sxs-lookup"><span data-stu-id="98178-646">SQL Data Warehouse</span></span></td>
      <td><span data-ttu-id="98178-647">Tabela</span><span class="sxs-lookup"><span data-stu-id="98178-647">Table</span></span></td>
      <td><span data-ttu-id="98178-648">Tabela, widok</span><span class="sxs-lookup"><span data-stu-id="98178-648">Table, view</span></span></td>
      <td><span data-ttu-id="98178-649">
        <font size=2>Protokół: tds</span><span class="sxs-lookup"><span data-stu-id="98178-649">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="98178-650">Uwierzytelnianie: {protokołu, windows}</span><span class="sxs-lookup"><span data-stu-id="98178-650">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="98178-651">Adres:</span><span class="sxs-lookup"><span data-stu-id="98178-651">Address:</span></span> <br><span data-ttu-id="98178-652">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Serwer</span><span class="sxs-lookup"><span data-stu-id="98178-652">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="98178-653">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bazy danych</span><span class="sxs-lookup"><span data-stu-id="98178-653">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="98178-654">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Schemat</span><span class="sxs-lookup"><span data-stu-id="98178-654">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="98178-655">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;obiekt</font>
      </span><span class="sxs-lookup"><span data-stu-id="98178-655">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-656">Oprogramowanie SQL Server</span><span class="sxs-lookup"><span data-stu-id="98178-656">SQL Server</span></span></td>
      <td><span data-ttu-id="98178-657">Polecenie</span><span class="sxs-lookup"><span data-stu-id="98178-657">Command</span></span></td>
      <td><span data-ttu-id="98178-658">Procedura składowana</span><span class="sxs-lookup"><span data-stu-id="98178-658">Stored procedure</span></span></td>
      <td><span data-ttu-id="98178-659">
        <font size=2>Protokół: tds</span><span class="sxs-lookup"><span data-stu-id="98178-659">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="98178-660">Uwierzytelnianie: {protokołu, windows}</span><span class="sxs-lookup"><span data-stu-id="98178-660">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="98178-661">Adres:</span><span class="sxs-lookup"><span data-stu-id="98178-661">Address:</span></span> <br><span data-ttu-id="98178-662">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Serwer</span><span class="sxs-lookup"><span data-stu-id="98178-662">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="98178-663">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bazy danych</span><span class="sxs-lookup"><span data-stu-id="98178-663">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="98178-664">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Schemat</span><span class="sxs-lookup"><span data-stu-id="98178-664">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="98178-665">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;obiekt</font>
      </span><span class="sxs-lookup"><span data-stu-id="98178-665">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-666">Oprogramowanie SQL Server</span><span class="sxs-lookup"><span data-stu-id="98178-666">SQL Server</span></span></td>
      <td><span data-ttu-id="98178-667">TableValuedFunction</span><span class="sxs-lookup"><span data-stu-id="98178-667">TableValuedFunction</span></span></td>
      <td><span data-ttu-id="98178-668">Funkcja zwracająca tabelę</span><span class="sxs-lookup"><span data-stu-id="98178-668">Table-valued function</span></span></td>
      <td><span data-ttu-id="98178-669">
        <font size=2>Protokół: tds</span><span class="sxs-lookup"><span data-stu-id="98178-669">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="98178-670">Uwierzytelnianie: {protokołu, windows}</span><span class="sxs-lookup"><span data-stu-id="98178-670">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="98178-671">Adres:</span><span class="sxs-lookup"><span data-stu-id="98178-671">Address:</span></span> <br><span data-ttu-id="98178-672">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Serwer</span><span class="sxs-lookup"><span data-stu-id="98178-672">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="98178-673">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bazy danych</span><span class="sxs-lookup"><span data-stu-id="98178-673">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="98178-674">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Schemat</span><span class="sxs-lookup"><span data-stu-id="98178-674">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="98178-675">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;obiekt</font>
      </span><span class="sxs-lookup"><span data-stu-id="98178-675">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-676">Oprogramowanie SQL Server</span><span class="sxs-lookup"><span data-stu-id="98178-676">SQL Server</span></span></td>
      <td><span data-ttu-id="98178-677">Kontener</span><span class="sxs-lookup"><span data-stu-id="98178-677">Container</span></span></td>
      <td><span data-ttu-id="98178-678">Database (Baza danych)</span><span class="sxs-lookup"><span data-stu-id="98178-678">Database</span></span></td>
      <td><span data-ttu-id="98178-679">
        <font size=2>Protokół: tds</span><span class="sxs-lookup"><span data-stu-id="98178-679">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="98178-680">Uwierzytelnianie: {protokołu, windows}</span><span class="sxs-lookup"><span data-stu-id="98178-680">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="98178-681">Adres:</span><span class="sxs-lookup"><span data-stu-id="98178-681">Address:</span></span> <br><span data-ttu-id="98178-682">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Serwer</span><span class="sxs-lookup"><span data-stu-id="98178-682">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="98178-683">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bazy danych</font>
      </span><span class="sxs-lookup"><span data-stu-id="98178-683">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-684">Oprogramowanie SQL Server</span><span class="sxs-lookup"><span data-stu-id="98178-684">SQL Server</span></span></td>
      <td><span data-ttu-id="98178-685">Tabela</span><span class="sxs-lookup"><span data-stu-id="98178-685">Table</span></span></td>
      <td><span data-ttu-id="98178-686">Tabela, widok</span><span class="sxs-lookup"><span data-stu-id="98178-686">Table, view</span></span></td>
      <td><span data-ttu-id="98178-687">
        <font size=2>Protokół: tds</span><span class="sxs-lookup"><span data-stu-id="98178-687">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="98178-688">Uwierzytelnianie: {protokołu, windows}</span><span class="sxs-lookup"><span data-stu-id="98178-688">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="98178-689">Adres:</span><span class="sxs-lookup"><span data-stu-id="98178-689">Address:</span></span> <br><span data-ttu-id="98178-690">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Serwer</span><span class="sxs-lookup"><span data-stu-id="98178-690">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="98178-691">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bazy danych</span><span class="sxs-lookup"><span data-stu-id="98178-691">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="98178-692">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Schemat</span><span class="sxs-lookup"><span data-stu-id="98178-692">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="98178-693">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;obiekt</font>
      </span><span class="sxs-lookup"><span data-stu-id="98178-693">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-694">SQL Server Analysis Services wielowymiarowe</span><span class="sxs-lookup"><span data-stu-id="98178-694">SQL Server Analysis Services multidimensional</span></span></td>
      <td><span data-ttu-id="98178-695">Kontener</span><span class="sxs-lookup"><span data-stu-id="98178-695">Container</span></span></td>
      <td><span data-ttu-id="98178-696">Model</span><span class="sxs-lookup"><span data-stu-id="98178-696">Model</span></span></td>
      <td><span data-ttu-id="98178-697">
        <font size=2>Protokół: usługi analysis services</span><span class="sxs-lookup"><span data-stu-id="98178-697">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="98178-698">Uwierzytelnianie: {systemu windows, basic anonimowe, Brak}</span><span class="sxs-lookup"><span data-stu-id="98178-698">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="98178-699">Adres:</span><span class="sxs-lookup"><span data-stu-id="98178-699">Address:</span></span> <br><span data-ttu-id="98178-700">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Serwer</span><span class="sxs-lookup"><span data-stu-id="98178-700">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="98178-701">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bazy danych</span><span class="sxs-lookup"><span data-stu-id="98178-701">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="98178-702">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Model</font>
      </span><span class="sxs-lookup"><span data-stu-id="98178-702">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-703">SQL Server Analysis Services wielowymiarowe</span><span class="sxs-lookup"><span data-stu-id="98178-703">SQL Server Analysis Services multidimensional</span></span></td>
      <td><span data-ttu-id="98178-704">WSKAŹNIK KPI</span><span class="sxs-lookup"><span data-stu-id="98178-704">KPI</span></span></td>
      <td><span data-ttu-id="98178-705">WSKAŹNIK KPI</span><span class="sxs-lookup"><span data-stu-id="98178-705">KPI</span></span></td>
      <td><span data-ttu-id="98178-706">
        <font size=2>Protokół: usługi analysis services</span><span class="sxs-lookup"><span data-stu-id="98178-706">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="98178-707">Uwierzytelnianie: {systemu windows, basic anonimowe, Brak}</span><span class="sxs-lookup"><span data-stu-id="98178-707">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="98178-708">Adres:</span><span class="sxs-lookup"><span data-stu-id="98178-708">Address:</span></span> <br><span data-ttu-id="98178-709">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Serwer</span><span class="sxs-lookup"><span data-stu-id="98178-709">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="98178-710">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bazy danych</span><span class="sxs-lookup"><span data-stu-id="98178-710">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="98178-711">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Model</span><span class="sxs-lookup"><span data-stu-id="98178-711">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="98178-712">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;obiekt</span><span class="sxs-lookup"><span data-stu-id="98178-712">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="98178-713">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Typ obiektu: {KPI}</font>
      </span><span class="sxs-lookup"><span data-stu-id="98178-713">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {KPI} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-714">SQL Server Analysis Services wielowymiarowe</span><span class="sxs-lookup"><span data-stu-id="98178-714">SQL Server Analysis Services multidimensional</span></span></td>
      <td><span data-ttu-id="98178-715">Miary</span><span class="sxs-lookup"><span data-stu-id="98178-715">Measure</span></span></td>
      <td><span data-ttu-id="98178-716">Miary</span><span class="sxs-lookup"><span data-stu-id="98178-716">Measure</span></span></td>
      <td><span data-ttu-id="98178-717">
        <font size=2>Protokół: usługi analysis services</span><span class="sxs-lookup"><span data-stu-id="98178-717">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="98178-718">Uwierzytelnianie: {systemu windows, basic anonimowe, Brak}</span><span class="sxs-lookup"><span data-stu-id="98178-718">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="98178-719">Adres:</span><span class="sxs-lookup"><span data-stu-id="98178-719">Address:</span></span> <br><span data-ttu-id="98178-720">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Serwer</span><span class="sxs-lookup"><span data-stu-id="98178-720">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="98178-721">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bazy danych</span><span class="sxs-lookup"><span data-stu-id="98178-721">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="98178-722">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Model</span><span class="sxs-lookup"><span data-stu-id="98178-722">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="98178-723">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;obiekt</span><span class="sxs-lookup"><span data-stu-id="98178-723">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="98178-724">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Typ obiektu: {Measure}</font>
      </span><span class="sxs-lookup"><span data-stu-id="98178-724">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Measure} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-725">SQL Server Analysis Services wielowymiarowe</span><span class="sxs-lookup"><span data-stu-id="98178-725">SQL Server Analysis Services multidimensional</span></span></td>
      <td><span data-ttu-id="98178-726">Tabela</span><span class="sxs-lookup"><span data-stu-id="98178-726">Table</span></span></td>
      <td><span data-ttu-id="98178-727">Wymiar</span><span class="sxs-lookup"><span data-stu-id="98178-727">Dimension</span></span></td>
      <td><span data-ttu-id="98178-728">
        <font size=2>Protokół: usługi analysis services</span><span class="sxs-lookup"><span data-stu-id="98178-728">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="98178-729">Uwierzytelnianie: {systemu windows, basic anonimowe, Brak}</span><span class="sxs-lookup"><span data-stu-id="98178-729">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="98178-730">Adres:</span><span class="sxs-lookup"><span data-stu-id="98178-730">Address:</span></span> <br><span data-ttu-id="98178-731">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Serwer</span><span class="sxs-lookup"><span data-stu-id="98178-731">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="98178-732">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bazy danych</span><span class="sxs-lookup"><span data-stu-id="98178-732">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="98178-733">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Model</span><span class="sxs-lookup"><span data-stu-id="98178-733">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="98178-734">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;obiekt</span><span class="sxs-lookup"><span data-stu-id="98178-734">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="98178-735">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Typ obiektu: {wymiaru}</font>
      </span><span class="sxs-lookup"><span data-stu-id="98178-735">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Dimension} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-736">SQL Server Analysis Services tabelarycznym</span><span class="sxs-lookup"><span data-stu-id="98178-736">SQL Server Analysis Services tabular</span></span></td>
      <td><span data-ttu-id="98178-737">Kontener</span><span class="sxs-lookup"><span data-stu-id="98178-737">Container</span></span></td>
      <td><span data-ttu-id="98178-738">Model</span><span class="sxs-lookup"><span data-stu-id="98178-738">Model</span></span></td>
      <td><span data-ttu-id="98178-739">
        <font size=2>Protokół: usługi analysis services</span><span class="sxs-lookup"><span data-stu-id="98178-739">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="98178-740">Uwierzytelnianie: {systemu windows, basic anonimowe, Brak}</span><span class="sxs-lookup"><span data-stu-id="98178-740">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="98178-741">Adres:</span><span class="sxs-lookup"><span data-stu-id="98178-741">Address:</span></span> <br><span data-ttu-id="98178-742">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Serwer</span><span class="sxs-lookup"><span data-stu-id="98178-742">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="98178-743">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bazy danych</span><span class="sxs-lookup"><span data-stu-id="98178-743">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="98178-744">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Model</font>
      </span><span class="sxs-lookup"><span data-stu-id="98178-744">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-745">SQL Server Analysis Services tabelarycznym</span><span class="sxs-lookup"><span data-stu-id="98178-745">SQL Server Analysis Services tabular</span></span></td>
      <td><span data-ttu-id="98178-746">WSKAŹNIK KPI</span><span class="sxs-lookup"><span data-stu-id="98178-746">KPI</span></span></td>
      <td><span data-ttu-id="98178-747">WSKAŹNIK KPI</span><span class="sxs-lookup"><span data-stu-id="98178-747">KPI</span></span></td>
      <td><span data-ttu-id="98178-748">
        <font size=2>Protokół: usługi analysis services</span><span class="sxs-lookup"><span data-stu-id="98178-748">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="98178-749">Uwierzytelnianie: {systemu windows, basic anonimowe, Brak}</span><span class="sxs-lookup"><span data-stu-id="98178-749">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="98178-750">Adres:</span><span class="sxs-lookup"><span data-stu-id="98178-750">Address:</span></span> <br><span data-ttu-id="98178-751">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Serwer</span><span class="sxs-lookup"><span data-stu-id="98178-751">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="98178-752">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bazy danych</span><span class="sxs-lookup"><span data-stu-id="98178-752">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="98178-753">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Model</span><span class="sxs-lookup"><span data-stu-id="98178-753">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="98178-754">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;obiekt</span><span class="sxs-lookup"><span data-stu-id="98178-754">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="98178-755">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Typ obiektu: {KPI}</font>
      </span><span class="sxs-lookup"><span data-stu-id="98178-755">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {KPI} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-756">SQL Server Analysis Services tabelarycznym</span><span class="sxs-lookup"><span data-stu-id="98178-756">SQL Server Analysis Services tabular</span></span></td>
      <td><span data-ttu-id="98178-757">Miary</span><span class="sxs-lookup"><span data-stu-id="98178-757">Measure</span></span></td>
      <td><span data-ttu-id="98178-758">Miary</span><span class="sxs-lookup"><span data-stu-id="98178-758">Measure</span></span></td>
      <td><span data-ttu-id="98178-759">
        <font size=2>Protokół: usługi analysis services</span><span class="sxs-lookup"><span data-stu-id="98178-759">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="98178-760">Uwierzytelnianie: {systemu windows, basic anonimowe, Brak}</span><span class="sxs-lookup"><span data-stu-id="98178-760">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="98178-761">Adres:</span><span class="sxs-lookup"><span data-stu-id="98178-761">Address:</span></span> <br><span data-ttu-id="98178-762">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Serwer</span><span class="sxs-lookup"><span data-stu-id="98178-762">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="98178-763">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bazy danych</span><span class="sxs-lookup"><span data-stu-id="98178-763">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="98178-764">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Model</span><span class="sxs-lookup"><span data-stu-id="98178-764">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="98178-765">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;obiekt</span><span class="sxs-lookup"><span data-stu-id="98178-765">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="98178-766">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Typ obiektu: {Measure}</font>
      </span><span class="sxs-lookup"><span data-stu-id="98178-766">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Measure} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-767">SQL Server Analysis Services tabelarycznym</span><span class="sxs-lookup"><span data-stu-id="98178-767">SQL Server Analysis Services tabular</span></span></td>
      <td><span data-ttu-id="98178-768">Tabela</span><span class="sxs-lookup"><span data-stu-id="98178-768">Table</span></span></td>
      <td><span data-ttu-id="98178-769">Tabela</span><span class="sxs-lookup"><span data-stu-id="98178-769">Table</span></span></td>
      <td><span data-ttu-id="98178-770">
        <font size=2>Protokół: usługi analysis services</span><span class="sxs-lookup"><span data-stu-id="98178-770">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="98178-771">Uwierzytelnianie: {systemu windows, basic anonimowe, Brak}</span><span class="sxs-lookup"><span data-stu-id="98178-771">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="98178-772">Adres:</span><span class="sxs-lookup"><span data-stu-id="98178-772">Address:</span></span> <br><span data-ttu-id="98178-773">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Serwer</span><span class="sxs-lookup"><span data-stu-id="98178-773">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="98178-774">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bazy danych</span><span class="sxs-lookup"><span data-stu-id="98178-774">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="98178-775">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Model</span><span class="sxs-lookup"><span data-stu-id="98178-775">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="98178-776">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;obiekt</span><span class="sxs-lookup"><span data-stu-id="98178-776">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="98178-777">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Typ obiektu: {Table}</font>
      </span><span class="sxs-lookup"><span data-stu-id="98178-777">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Table} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-778">SQL Server Reporting Services</span><span class="sxs-lookup"><span data-stu-id="98178-778">SQL Server Reporting Services</span></span></td>
      <td><span data-ttu-id="98178-779">Kontener</span><span class="sxs-lookup"><span data-stu-id="98178-779">Container</span></span></td>
      <td><span data-ttu-id="98178-780">Serwer</span><span class="sxs-lookup"><span data-stu-id="98178-780">Server</span></span></td>
      <td><span data-ttu-id="98178-781">
        <font size=2>Protokołów: usług raportowania</span><span class="sxs-lookup"><span data-stu-id="98178-781">
        <font size=2> Protocol: reporting-services</span></span> <br><span data-ttu-id="98178-782">Uwierzytelnianie: {windows}</span><span class="sxs-lookup"><span data-stu-id="98178-782">Authentication: {windows}</span></span> <br><span data-ttu-id="98178-783">Adres:</span><span class="sxs-lookup"><span data-stu-id="98178-783">Address:</span></span> <br><span data-ttu-id="98178-784">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Serwer</span><span class="sxs-lookup"><span data-stu-id="98178-784">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="98178-785">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Wersja: {ReportingService2010}</font>
      </span><span class="sxs-lookup"><span data-stu-id="98178-785">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version: {ReportingService2010} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-786">SQL Server Reporting Services</span><span class="sxs-lookup"><span data-stu-id="98178-786">SQL Server Reporting Services</span></span></td>
      <td><span data-ttu-id="98178-787">Raport</span><span class="sxs-lookup"><span data-stu-id="98178-787">Report</span></span></td>
      <td><span data-ttu-id="98178-788">Raport</span><span class="sxs-lookup"><span data-stu-id="98178-788">Report</span></span></td>
      <td><span data-ttu-id="98178-789">
        <font size=2>Protokołów: usług raportowania</span><span class="sxs-lookup"><span data-stu-id="98178-789">
        <font size=2> Protocol: reporting-services</span></span> <br><span data-ttu-id="98178-790">Uwierzytelnianie: {windows}</span><span class="sxs-lookup"><span data-stu-id="98178-790">Authentication: {windows}</span></span> <br><span data-ttu-id="98178-791">Adres:</span><span class="sxs-lookup"><span data-stu-id="98178-791">Address:</span></span> <br><span data-ttu-id="98178-792">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Serwer</span><span class="sxs-lookup"><span data-stu-id="98178-792">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="98178-793">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Ścieżka</span><span class="sxs-lookup"><span data-stu-id="98178-793">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; path</span></span> <br><span data-ttu-id="98178-794">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Wersja: {ReportingService2010}</font>
      </span><span class="sxs-lookup"><span data-stu-id="98178-794">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version: {ReportingService2010} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-795">Teradata</span><span class="sxs-lookup"><span data-stu-id="98178-795">Teradata</span></span></td>
      <td><span data-ttu-id="98178-796">Kontener</span><span class="sxs-lookup"><span data-stu-id="98178-796">Container</span></span></td>
      <td><span data-ttu-id="98178-797">Database (Baza danych)</span><span class="sxs-lookup"><span data-stu-id="98178-797">Database</span></span></td>
      <td><span data-ttu-id="98178-798">
        <font size=2>Protokół: teradata</span><span class="sxs-lookup"><span data-stu-id="98178-798">
        <font size=2> Protocol: teradata</span></span> <br><span data-ttu-id="98178-799">Uwierzytelnianie: {protokołu, windows}</span><span class="sxs-lookup"><span data-stu-id="98178-799">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="98178-800">Adres:</span><span class="sxs-lookup"><span data-stu-id="98178-800">Address:</span></span> <br><span data-ttu-id="98178-801">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Serwer</span><span class="sxs-lookup"><span data-stu-id="98178-801">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="98178-802">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bazy danych</font>
      </span><span class="sxs-lookup"><span data-stu-id="98178-802">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-803">Teradata</span><span class="sxs-lookup"><span data-stu-id="98178-803">Teradata</span></span></td>
      <td><span data-ttu-id="98178-804">Tabela</span><span class="sxs-lookup"><span data-stu-id="98178-804">Table</span></span></td>
      <td><span data-ttu-id="98178-805">Tabela, widok</span><span class="sxs-lookup"><span data-stu-id="98178-805">Table, view</span></span></td>
      <td><span data-ttu-id="98178-806">
        <font size=2>Protokół: teradata</span><span class="sxs-lookup"><span data-stu-id="98178-806">
        <font size=2> Protocol: teradata</span></span> <br><span data-ttu-id="98178-807">Uwierzytelnianie: {protokołu, windows}</span><span class="sxs-lookup"><span data-stu-id="98178-807">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="98178-808">Adres:</span><span class="sxs-lookup"><span data-stu-id="98178-808">Address:</span></span> <br><span data-ttu-id="98178-809">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Serwer</span><span class="sxs-lookup"><span data-stu-id="98178-809">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="98178-810">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bazy danych</span><span class="sxs-lookup"><span data-stu-id="98178-810">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="98178-811">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;obiekt</font>
      </span><span class="sxs-lookup"><span data-stu-id="98178-811">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-812">SQL Server Master Data Services</span><span class="sxs-lookup"><span data-stu-id="98178-812">SQL Server Master Data Services</span></span></td>
      <td><span data-ttu-id="98178-813">Kontener</span><span class="sxs-lookup"><span data-stu-id="98178-813">Container</span></span></td>
      <td><span data-ttu-id="98178-814">Model</span><span class="sxs-lookup"><span data-stu-id="98178-814">Model</span></span></td>
      <td><span data-ttu-id="98178-815">
        <font size="2">Protokół: mssql-mds</span><span class="sxs-lookup"><span data-stu-id="98178-815">
        <font size="2"> Protocol: mssql-mds</span></span> <br><span data-ttu-id="98178-816">Uwierzytelnianie: {windows}</span><span class="sxs-lookup"><span data-stu-id="98178-816">Authentication: {windows}</span></span> <br><span data-ttu-id="98178-817">Adres:</span><span class="sxs-lookup"><span data-stu-id="98178-817">Address:</span></span> <br><span data-ttu-id="98178-818">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;adres URL</span><span class="sxs-lookup"><span data-stu-id="98178-818">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span></span> <br><span data-ttu-id="98178-819">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Model</span><span class="sxs-lookup"><span data-stu-id="98178-819">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="98178-820">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Wersja</font>
      </span><span class="sxs-lookup"><span data-stu-id="98178-820">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-821">SQL Server Master Data Services</span><span class="sxs-lookup"><span data-stu-id="98178-821">SQL Server Master Data Services</span></span></td>
      <td><span data-ttu-id="98178-822">Tabela</span><span class="sxs-lookup"><span data-stu-id="98178-822">Table</span></span></td>
      <td><span data-ttu-id="98178-823">Jednostka</span><span class="sxs-lookup"><span data-stu-id="98178-823">Entity</span></span></td>
      <td><span data-ttu-id="98178-824">
        <font size="2">Protokół: mssql-mds</span><span class="sxs-lookup"><span data-stu-id="98178-824">
        <font size="2"> Protocol: mssql-mds</span></span> <br><span data-ttu-id="98178-825">Uwierzytelnianie: {windows}</span><span class="sxs-lookup"><span data-stu-id="98178-825">Authentication: {windows}</span></span> <br><span data-ttu-id="98178-826">Adres:</span><span class="sxs-lookup"><span data-stu-id="98178-826">Address:</span></span> <br><span data-ttu-id="98178-827">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;adres URL</span><span class="sxs-lookup"><span data-stu-id="98178-827">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span></span> <br><span data-ttu-id="98178-828">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Model</span><span class="sxs-lookup"><span data-stu-id="98178-828">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="98178-829">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Wersja</span><span class="sxs-lookup"><span data-stu-id="98178-829">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version</span></span> <br><span data-ttu-id="98178-830">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;jednostki</font>
      </span><span class="sxs-lookup"><span data-stu-id="98178-830">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; entity </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-831">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="98178-831">Azure Cosmos DB</span></span></td>
      <td><span data-ttu-id="98178-832">Kontener</span><span class="sxs-lookup"><span data-stu-id="98178-832">Container</span></span></td>
      <td><span data-ttu-id="98178-833">Database (Baza danych)</span><span class="sxs-lookup"><span data-stu-id="98178-833">Database</span></span></td>
      <td><span data-ttu-id="98178-834">
        <font size=2>Protokół: bazie danych dokumentów</span><span class="sxs-lookup"><span data-stu-id="98178-834">
        <font size=2> Protocol: document-db</span></span> <br><span data-ttu-id="98178-835">Uwierzytelnianie: {azure klawisza dostępu}</span><span class="sxs-lookup"><span data-stu-id="98178-835">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="98178-836">Adres:</span><span class="sxs-lookup"><span data-stu-id="98178-836">Address:</span></span> <br><span data-ttu-id="98178-837">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;adres URL</span><span class="sxs-lookup"><span data-stu-id="98178-837">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span></span> <br><span data-ttu-id="98178-838">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bazy danych</font>
      </span><span class="sxs-lookup"><span data-stu-id="98178-838">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-839">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="98178-839">Azure Cosmos DB</span></span></td>
      <td><span data-ttu-id="98178-840">Collection</span><span class="sxs-lookup"><span data-stu-id="98178-840">Collection</span></span></td>
      <td><span data-ttu-id="98178-841">Collection</span><span class="sxs-lookup"><span data-stu-id="98178-841">Collection</span></span></td>
      <td><span data-ttu-id="98178-842">
        <font size=2>Protokół: bazie danych dokumentów</span><span class="sxs-lookup"><span data-stu-id="98178-842">
        <font size=2> Protocol: document-db</span></span> <br><span data-ttu-id="98178-843">Uwierzytelnianie: {azure klawisza dostępu}</span><span class="sxs-lookup"><span data-stu-id="98178-843">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="98178-844">Adres:</span><span class="sxs-lookup"><span data-stu-id="98178-844">Address:</span></span> <br><span data-ttu-id="98178-845">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;adres URL</span><span class="sxs-lookup"><span data-stu-id="98178-845">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span></span> <br><span data-ttu-id="98178-846">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bazy danych</span><span class="sxs-lookup"><span data-stu-id="98178-846">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="98178-847">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Kolekcja</font>
      </span><span class="sxs-lookup"><span data-stu-id="98178-847">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; collection </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-848">Ogólne ODBC</span><span class="sxs-lookup"><span data-stu-id="98178-848">Generic ODBC</span></span></td>
      <td><span data-ttu-id="98178-849">Kontener</span><span class="sxs-lookup"><span data-stu-id="98178-849">Container</span></span></td>
      <td><span data-ttu-id="98178-850">Database (Baza danych)</span><span class="sxs-lookup"><span data-stu-id="98178-850">Database</span></span></td>
      <td><span data-ttu-id="98178-851">
        <font size=2>Protokół: odbc</span><span class="sxs-lookup"><span data-stu-id="98178-851">
        <font size=2> Protocol: odbc</span></span> <br><span data-ttu-id="98178-852">Uwierzytelnianie: {podstawowe, windows}</span><span class="sxs-lookup"><span data-stu-id="98178-852">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="98178-853">Adres:</span><span class="sxs-lookup"><span data-stu-id="98178-853">Address:</span></span> <br><span data-ttu-id="98178-854">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Opcje</span><span class="sxs-lookup"><span data-stu-id="98178-854">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; options</span></span> <br><span data-ttu-id="98178-855">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bazy danych</font>
      </span><span class="sxs-lookup"><span data-stu-id="98178-855">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-856">Ogólne ODBC</span><span class="sxs-lookup"><span data-stu-id="98178-856">Generic ODBC</span></span></td>
      <td><span data-ttu-id="98178-857">Tabela</span><span class="sxs-lookup"><span data-stu-id="98178-857">Table</span></span></td>
      <td><span data-ttu-id="98178-858">Tabela, widok</span><span class="sxs-lookup"><span data-stu-id="98178-858">Table, View</span></span></td>
      <td><span data-ttu-id="98178-859">
        <font size=2>Protokół: odbc</span><span class="sxs-lookup"><span data-stu-id="98178-859">
        <font size=2> Protocol: odbc</span></span> <br><span data-ttu-id="98178-860">Uwierzytelnianie: {podstawowe, windows}</span><span class="sxs-lookup"><span data-stu-id="98178-860">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="98178-861">Adres:</span><span class="sxs-lookup"><span data-stu-id="98178-861">Address:</span></span> <br><span data-ttu-id="98178-862">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Opcje</span><span class="sxs-lookup"><span data-stu-id="98178-862">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; options</span></span> <br><span data-ttu-id="98178-863">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bazy danych</span><span class="sxs-lookup"><span data-stu-id="98178-863">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="98178-864">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;obiekt</span><span class="sxs-lookup"><span data-stu-id="98178-864">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="98178-865">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Schemat</font>
      </span><span class="sxs-lookup"><span data-stu-id="98178-865">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-866">Sybase</span><span class="sxs-lookup"><span data-stu-id="98178-866">Sybase</span></span></td>
      <td><span data-ttu-id="98178-867">Kontener</span><span class="sxs-lookup"><span data-stu-id="98178-867">Container</span></span></td>
      <td><span data-ttu-id="98178-868">Database (Baza danych)</span><span class="sxs-lookup"><span data-stu-id="98178-868">Database</span></span></td>
      <td><span data-ttu-id="98178-869">
        <font size=2>Protokół: sybase</span><span class="sxs-lookup"><span data-stu-id="98178-869">
        <font size=2> protocol: sybase</span></span> <br><span data-ttu-id="98178-870">Uwierzytelnianie: {podstawowe, windows}</span><span class="sxs-lookup"><span data-stu-id="98178-870">authentication: {basic, windows}</span></span> <br><span data-ttu-id="98178-871">Adres:</span><span class="sxs-lookup"><span data-stu-id="98178-871">address:</span></span> <br><span data-ttu-id="98178-872">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Serwer</span><span class="sxs-lookup"><span data-stu-id="98178-872">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="98178-873">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bazy danych</font>
      </span><span class="sxs-lookup"><span data-stu-id="98178-873">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-874">Sybase</span><span class="sxs-lookup"><span data-stu-id="98178-874">Sybase</span></span></td>
      <td><span data-ttu-id="98178-875">Tabela</span><span class="sxs-lookup"><span data-stu-id="98178-875">Table</span></span></td>
      <td><span data-ttu-id="98178-876">Tabela, widok</span><span class="sxs-lookup"><span data-stu-id="98178-876">Table, View</span></span></td>
      <td><span data-ttu-id="98178-877">
        <font size=2>Protokół: sybase</span><span class="sxs-lookup"><span data-stu-id="98178-877">
        <font size=2> protocol: sybase</span></span> <br><span data-ttu-id="98178-878">Uwierzytelnianie: {podstawowe, windows}</span><span class="sxs-lookup"><span data-stu-id="98178-878">authentication: {basic, windows}</span></span> <br><span data-ttu-id="98178-879">Adres:</span><span class="sxs-lookup"><span data-stu-id="98178-879">address:</span></span> <br><span data-ttu-id="98178-880">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Serwer</span><span class="sxs-lookup"><span data-stu-id="98178-880">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="98178-881">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bazy danych</span><span class="sxs-lookup"><span data-stu-id="98178-881">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="98178-882">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Schemat</span><span class="sxs-lookup"><span data-stu-id="98178-882">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="98178-883">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;obiekt</font>
      </span><span class="sxs-lookup"><span data-stu-id="98178-883">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="98178-884">Inne (Brak hello powyżej)</span><span class="sxs-lookup"><span data-stu-id="98178-884">Other (none of hello above)</span></span></td>
      <td>\*</td>
      <td>\*</td>
      <td><span data-ttu-id="98178-885">
        <font size=2>Protokół: ogólny zasobów</span><span class="sxs-lookup"><span data-stu-id="98178-885">
        <font size=2> Protocol: generic-asset</span></span> <br><span data-ttu-id="98178-886">Adres:</span><span class="sxs-lookup"><span data-stu-id="98178-886">Address:</span></span> <br><span data-ttu-id="98178-887">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;assetId</font>
      </span><span class="sxs-lookup"><span data-stu-id="98178-887">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; assetId </font>
      </span></span></td>
    </tr>
</table>
