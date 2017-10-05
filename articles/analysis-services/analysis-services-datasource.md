---
title: "Źródła danych obsługiwane w usłudze Azure Analysis Services | Dokumentacja firmy Microsoft"
description: "Zawiera opis źródła danych obsługiwane w przypadku modeli danych z usług Azure Analysis Services."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 6ec63319-ff9b-4b01-a1cd-274481dc8995
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 8bd6c3b5a923ce2f3cd0f60af82e59c5cc27cbb4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="data-sources-supported-in-azure-analysis-services"></a><span data-ttu-id="237c8-103">Źródła danych obsługiwane w usłudze Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="237c8-103">Data sources supported in Azure Analysis Services</span></span>
<span data-ttu-id="237c8-104">Azure serwery usług Analysis Services obsługują połączenia ze źródłami danych w chmurze i lokalnie w Twojej organizacji.</span><span class="sxs-lookup"><span data-stu-id="237c8-104">Azure Analysis Services servers support connecting to data sources in the cloud and on-premises in your organization.</span></span> <span data-ttu-id="237c8-105">Dodatkowe obsługiwanych źródeł danych są dodawane przez cały czas.</span><span class="sxs-lookup"><span data-stu-id="237c8-105">Additional supported data sources are being added all the time.</span></span> <span data-ttu-id="237c8-106">Zaglądaj tu.</span><span class="sxs-lookup"><span data-stu-id="237c8-106">Check back often.</span></span> 

<span data-ttu-id="237c8-107">Obecnie obsługiwane są następujące źródła danych:</span><span class="sxs-lookup"><span data-stu-id="237c8-107">The following data sources are currently supported:</span></span>

| <span data-ttu-id="237c8-108">Chmura</span><span class="sxs-lookup"><span data-stu-id="237c8-108">Cloud</span></span>  |
|---|
| <span data-ttu-id="237c8-109">Magazyn obiektów Blob platformy Azure *</span><span class="sxs-lookup"><span data-stu-id="237c8-109">Azure Blob Storage*</span></span>  |
| <span data-ttu-id="237c8-110">Usługa Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="237c8-110">Azure SQL Database</span></span>  |
| <span data-ttu-id="237c8-111">Magazyn danych Azure</span><span class="sxs-lookup"><span data-stu-id="237c8-111">Azure Data Warehouse</span></span> |


| <span data-ttu-id="237c8-112">Lokalnie</span><span class="sxs-lookup"><span data-stu-id="237c8-112">On-premises</span></span>  |   |   |   |
|---|---|---|---|
| <span data-ttu-id="237c8-113">Dostępu do bazy danych</span><span class="sxs-lookup"><span data-stu-id="237c8-113">Access Database</span></span>  | <span data-ttu-id="237c8-114">Folder *</span><span class="sxs-lookup"><span data-stu-id="237c8-114">Folder*</span></span> | <span data-ttu-id="237c8-115">Baza danych Oracle</span><span class="sxs-lookup"><span data-stu-id="237c8-115">Oracle Database</span></span>  | <span data-ttu-id="237c8-116">Baza danych programu Teradata</span><span class="sxs-lookup"><span data-stu-id="237c8-116">Teradata Database</span></span> |
| <span data-ttu-id="237c8-117">Active Directory *</span><span class="sxs-lookup"><span data-stu-id="237c8-117">Active Directory*</span></span>  | <span data-ttu-id="237c8-118">Dokument JSON *</span><span class="sxs-lookup"><span data-stu-id="237c8-118">JSON document*</span></span>  | <span data-ttu-id="237c8-119">Baza danych Postgre SQL *</span><span class="sxs-lookup"><span data-stu-id="237c8-119">Postgre SQL Database*</span></span>  |<span data-ttu-id="237c8-120">Tabela XML *</span><span class="sxs-lookup"><span data-stu-id="237c8-120">XML table*</span></span> |
| <span data-ttu-id="237c8-121">Analysis Services</span><span class="sxs-lookup"><span data-stu-id="237c8-121">Analysis Services</span></span>  | <span data-ttu-id="237c8-122">Wiersze z danych binarnych *</span><span class="sxs-lookup"><span data-stu-id="237c8-122">Lines from binary*</span></span>  | <span data-ttu-id="237c8-123">SAP HANA *</span><span class="sxs-lookup"><span data-stu-id="237c8-123">SAP HANA*</span></span>  |
| <span data-ttu-id="237c8-124">Analytics Platform System</span><span class="sxs-lookup"><span data-stu-id="237c8-124">Analytics Platform System</span></span>  | <span data-ttu-id="237c8-125">Baza danych MySQL</span><span class="sxs-lookup"><span data-stu-id="237c8-125">MySQL Database</span></span>  | <span data-ttu-id="237c8-126">SAP Business Warehouse *</span><span class="sxs-lookup"><span data-stu-id="237c8-126">SAP Business Warehouse*</span></span>  | |
| <span data-ttu-id="237c8-127">Dynamics CRM *</span><span class="sxs-lookup"><span data-stu-id="237c8-127">Dynamics CRM*</span></span>  | <span data-ttu-id="237c8-128">Źródła danych OData *</span><span class="sxs-lookup"><span data-stu-id="237c8-128">OData Feed*</span></span>  | <span data-ttu-id="237c8-129">SharePoint *</span><span class="sxs-lookup"><span data-stu-id="237c8-129">SharePoint*</span></span>  |
| <span data-ttu-id="237c8-130">Skoroszyt programu Excel</span><span class="sxs-lookup"><span data-stu-id="237c8-130">Excel workbook</span></span>  | <span data-ttu-id="237c8-131">Zapytanie ODBC</span><span class="sxs-lookup"><span data-stu-id="237c8-131">ODBC query</span></span>  | <span data-ttu-id="237c8-132">SQL Database</span><span class="sxs-lookup"><span data-stu-id="237c8-132">SQL Database</span></span>  |
| <span data-ttu-id="237c8-133">Exchange *</span><span class="sxs-lookup"><span data-stu-id="237c8-133">Exchange*</span></span>  | <span data-ttu-id="237c8-134">OLE DB</span><span class="sxs-lookup"><span data-stu-id="237c8-134">OLE DB</span></span>  | <span data-ttu-id="237c8-135">Baza danych programu Sybase</span><span class="sxs-lookup"><span data-stu-id="237c8-135">Sybase Database</span></span>  |

<span data-ttu-id="237c8-136">\*Tylko modele w 1400 tabelarycznych.</span><span class="sxs-lookup"><span data-stu-id="237c8-136">\* Tabular 1400 models only.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="237c8-137">Łączenie ze źródłami danych lokalnych wymagają [bramy danych lokalnych](analysis-services-gateway.md) zainstalowany na komputerze w danym środowisku.</span><span class="sxs-lookup"><span data-stu-id="237c8-137">Connecting to on-premises data sources require an [On-premises data gateway](analysis-services-gateway.md) installed on a computer in your environment.</span></span>

## <a name="data-providers"></a><span data-ttu-id="237c8-138">Dostawcy danych</span><span class="sxs-lookup"><span data-stu-id="237c8-138">Data providers</span></span>

<span data-ttu-id="237c8-139">Modeli danych z usług Azure Analysis Services może wymagać różnych dostawców podczas nawiązywania połączenia z niektórych źródeł danych.</span><span class="sxs-lookup"><span data-stu-id="237c8-139">Data models in Azure Analysis Services may require different data providers when connecting to certain data sources.</span></span> <span data-ttu-id="237c8-140">W niektórych przypadkach modeli tabelarycznych łączenie ze źródłami danych przy użyciu macierzystych dostawców, takich jak SQL Server Native Client (SQLNCLI11) może zostać zwrócony błąd.</span><span class="sxs-lookup"><span data-stu-id="237c8-140">In some cases, tabular models connecting to data sources using native providers such as SQL Server Native Client (SQLNCLI11) may return an error.</span></span>

<span data-ttu-id="237c8-141">W przypadku modeli danych, które nawiązania połączenia danych w chmurze źródło takich jak bazy danych SQL Azure, jeśli używasz macierzystych dostawców innych niż SQLOLEDB, może zostać wyświetlony komunikat o błędzie: **"Dostawca"SQLNCLI11.1"nie jest zarejestrowana."**</span><span class="sxs-lookup"><span data-stu-id="237c8-141">For data models that connect to a cloud data source such as Azure SQL Database, if you use native providers other than SQLOLEDB, you may see error message: **“The provider 'SQLNCLI11.1' is not registered.”**</span></span> <span data-ttu-id="237c8-142">Lub, jeśli masz model zapytania bezpośredniego połączenia ze źródłami danych lokalnych, jeśli używasz macierzystych dostawców może zostać wyświetlony komunikat o błędzie: **"błąd podczas tworzenia zestawu wierszy OLE DB. Błędna składnia w pobliżu "Granica" "**.</span><span class="sxs-lookup"><span data-stu-id="237c8-142">Or, if you have a DirectQuery model connecting to on-premises data sources, if you use native providers you may see error message: **“Error creating OLE DB row set. Incorrect syntax near 'LIMIT'”**.</span></span>

<span data-ttu-id="237c8-143">Następujący dostawcy źródła danych są obsługiwane w pamięci lub modeli danych zapytania bezpośredniego, podczas nawiązywania połączenia ze źródłami danych w chmurze lub lokalne:</span><span class="sxs-lookup"><span data-stu-id="237c8-143">The following datasource providers are supported for in-memory or DirectQuery data models when connecting to data sources in the cloud or on-premises:</span></span>

### <a name="cloud"></a><span data-ttu-id="237c8-144">Chmura</span><span class="sxs-lookup"><span data-stu-id="237c8-144">Cloud</span></span>
| <span data-ttu-id="237c8-145">**Źródło danych**</span><span class="sxs-lookup"><span data-stu-id="237c8-145">**Datasource**</span></span> | <span data-ttu-id="237c8-146">**W pamięci**</span><span class="sxs-lookup"><span data-stu-id="237c8-146">**In-memory**</span></span> | <span data-ttu-id="237c8-147">**Zapytania bezpośredniego**</span><span class="sxs-lookup"><span data-stu-id="237c8-147">**DirectQuery**</span></span> |
|  --- | --- | --- |
| <span data-ttu-id="237c8-148">Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="237c8-148">Azure SQL Data Warehouse</span></span> |<span data-ttu-id="237c8-149">.NET framework Data Provider for SQL Server</span><span class="sxs-lookup"><span data-stu-id="237c8-149">.NET Framework Data Provider for SQL Server</span></span> |<span data-ttu-id="237c8-150">.NET framework Data Provider for SQL Server</span><span class="sxs-lookup"><span data-stu-id="237c8-150">.NET Framework Data Provider for SQL Server</span></span> |
| <span data-ttu-id="237c8-151">Usługa Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="237c8-151">Azure SQL Database</span></span> |<span data-ttu-id="237c8-152">.NET framework Data Provider for SQL Server</span><span class="sxs-lookup"><span data-stu-id="237c8-152">.NET Framework Data Provider for SQL Server</span></span> |<span data-ttu-id="237c8-153">.NET framework Data Provider for SQL Server</span><span class="sxs-lookup"><span data-stu-id="237c8-153">.NET Framework Data Provider for SQL Server</span></span> | |

### <a name="on-premises-via-gateway"></a><span data-ttu-id="237c8-154">Lokalne (za pośrednictwem bramy)</span><span class="sxs-lookup"><span data-stu-id="237c8-154">On-premises (via Gateway)</span></span>
|<span data-ttu-id="237c8-155">**Źródło danych**</span><span class="sxs-lookup"><span data-stu-id="237c8-155">**Datasource**</span></span> | <span data-ttu-id="237c8-156">**W pamięci**</span><span class="sxs-lookup"><span data-stu-id="237c8-156">**In-memory**</span></span> | <span data-ttu-id="237c8-157">**Zapytania bezpośredniego**</span><span class="sxs-lookup"><span data-stu-id="237c8-157">**DirectQuery**</span></span> |
|  --- | --- | --- |
| <span data-ttu-id="237c8-158">Oprogramowanie SQL Server</span><span class="sxs-lookup"><span data-stu-id="237c8-158">SQL Server</span></span> |<span data-ttu-id="237c8-159">SQL Server Native Client 11.0</span><span class="sxs-lookup"><span data-stu-id="237c8-159">SQL Server Native Client 11.0</span></span> |<span data-ttu-id="237c8-160">.NET framework Data Provider for SQL Server</span><span class="sxs-lookup"><span data-stu-id="237c8-160">.NET Framework Data Provider for SQL Server</span></span> |
| <span data-ttu-id="237c8-161">Oprogramowanie SQL Server</span><span class="sxs-lookup"><span data-stu-id="237c8-161">SQL Server</span></span> |<span data-ttu-id="237c8-162">Dostawca Microsoft OLE DB dla programu SQL Server</span><span class="sxs-lookup"><span data-stu-id="237c8-162">Microsoft OLE DB Provider for SQL Server</span></span> |<span data-ttu-id="237c8-163">.NET framework Data Provider for SQL Server</span><span class="sxs-lookup"><span data-stu-id="237c8-163">.NET Framework Data Provider for SQL Server</span></span> | |
| <span data-ttu-id="237c8-164">Oprogramowanie SQL Server</span><span class="sxs-lookup"><span data-stu-id="237c8-164">SQL Server</span></span> |<span data-ttu-id="237c8-165">.NET framework Data Provider for SQL Server</span><span class="sxs-lookup"><span data-stu-id="237c8-165">.NET Framework Data Provider for SQL Server</span></span> |<span data-ttu-id="237c8-166">.NET framework Data Provider for SQL Server</span><span class="sxs-lookup"><span data-stu-id="237c8-166">.NET Framework Data Provider for SQL Server</span></span> | |
| <span data-ttu-id="237c8-167">Oracle</span><span class="sxs-lookup"><span data-stu-id="237c8-167">Oracle</span></span> |<span data-ttu-id="237c8-168">Dostawca Microsoft OLE DB dla programu Oracle</span><span class="sxs-lookup"><span data-stu-id="237c8-168">Microsoft OLE DB Provider for Oracle</span></span> |<span data-ttu-id="237c8-169">Dostawca danych programu Oracle dla platformy .NET</span><span class="sxs-lookup"><span data-stu-id="237c8-169">Oracle Data Provider for .NET</span></span> | |
| <span data-ttu-id="237c8-170">Oracle</span><span class="sxs-lookup"><span data-stu-id="237c8-170">Oracle</span></span> |<span data-ttu-id="237c8-171">Dostawca danych programu Oracle dla platformy .NET</span><span class="sxs-lookup"><span data-stu-id="237c8-171">Oracle Data Provider for .NET</span></span> |<span data-ttu-id="237c8-172">Dostawca danych programu Oracle dla platformy .NET</span><span class="sxs-lookup"><span data-stu-id="237c8-172">Oracle Data Provider for .NET</span></span> | |
| <span data-ttu-id="237c8-173">Teradata</span><span class="sxs-lookup"><span data-stu-id="237c8-173">Teradata</span></span> |<span data-ttu-id="237c8-174">Dostawca OLE DB dla programu Teradata</span><span class="sxs-lookup"><span data-stu-id="237c8-174">OLE DB Provider for Teradata</span></span> |<span data-ttu-id="237c8-175">Dostawca danych programu Teradata dla platformy .NET</span><span class="sxs-lookup"><span data-stu-id="237c8-175">Teradata Data Provider for .NET</span></span> | |
| <span data-ttu-id="237c8-176">Teradata</span><span class="sxs-lookup"><span data-stu-id="237c8-176">Teradata</span></span> |<span data-ttu-id="237c8-177">Dostawca danych programu Teradata dla platformy .NET</span><span class="sxs-lookup"><span data-stu-id="237c8-177">Teradata Data Provider for .NET</span></span> |<span data-ttu-id="237c8-178">Dostawca danych programu Teradata dla platformy .NET</span><span class="sxs-lookup"><span data-stu-id="237c8-178">Teradata Data Provider for .NET</span></span> | |
| <span data-ttu-id="237c8-179">Analytics Platform System</span><span class="sxs-lookup"><span data-stu-id="237c8-179">Analytics Platform System</span></span> |<span data-ttu-id="237c8-180">.NET framework Data Provider for SQL Server</span><span class="sxs-lookup"><span data-stu-id="237c8-180">.NET Framework Data Provider for SQL Server</span></span> |<span data-ttu-id="237c8-181">.NET framework Data Provider for SQL Server</span><span class="sxs-lookup"><span data-stu-id="237c8-181">.NET Framework Data Provider for SQL Server</span></span> | |

> [!NOTE]
> <span data-ttu-id="237c8-182">Upewnij się, że zainstalowano dostawców 64-bitowym, podczas korzystania z bramy lokalnej.</span><span class="sxs-lookup"><span data-stu-id="237c8-182">Ensure 64-bit providers are installed when using On-premises gateway.</span></span>
> 
> 

<span data-ttu-id="237c8-183">Podczas migrowania lokalnymi modelu tabelarycznego usług SQL Server Analysis Services do usług Azure Analysis Services, może być konieczna zmiana dostawcy.</span><span class="sxs-lookup"><span data-stu-id="237c8-183">When migrating an on-premises SQL Server Analysis Services tabular model to Azure Analysis Services, it may be necessary to change the provider.</span></span>

<span data-ttu-id="237c8-184">**Aby określić dostawcę źródła danych**</span><span class="sxs-lookup"><span data-stu-id="237c8-184">**To specify a datasource provider**</span></span>

1. <span data-ttu-id="237c8-185">Programu SSDT > **Eksplorator modelu tabelarycznego** > **źródeł danych**, kliknij prawym przyciskiem myszy połączenie ze źródłem danych, a następnie kliknij przycisk **Edytuj źródło danych**.</span><span class="sxs-lookup"><span data-stu-id="237c8-185">In SSDT > **Tabular Model Explorer** > **Data Sources**, right-click a data source connection, and then click **Edit Data Source**.</span></span>
2. <span data-ttu-id="237c8-186">W **Edytuj połączenie**, kliknij przycisk **zaawansowane** aby otworzyć okno właściwości wyprzedzeniem.</span><span class="sxs-lookup"><span data-stu-id="237c8-186">In **Edit Connection**, click **Advanced** to open the Advance properties window.</span></span>
3. <span data-ttu-id="237c8-187">W **ustawić właściwości zaawansowane** > **dostawców**, następnie wybierz odpowiedniego dostawcę.</span><span class="sxs-lookup"><span data-stu-id="237c8-187">In **Set Advanced Properties** > **Providers**, then select the appropriate provider.</span></span>

## <a name="impersonation"></a><span data-ttu-id="237c8-188">Personifikacja</span><span class="sxs-lookup"><span data-stu-id="237c8-188">Impersonation</span></span>
<span data-ttu-id="237c8-189">W niektórych przypadkach może być konieczne określenie konta różnych personifikacji.</span><span class="sxs-lookup"><span data-stu-id="237c8-189">In some cases, it may be necessary to specify a different impersonation account.</span></span> <span data-ttu-id="237c8-190">Można określić konta personifikacji w SSDT lub SSMS.</span><span class="sxs-lookup"><span data-stu-id="237c8-190">Impersonation account can be specified in SSDT or SSMS.</span></span>

<span data-ttu-id="237c8-191">Dla lokalnych źródeł danych:</span><span class="sxs-lookup"><span data-stu-id="237c8-191">For on-premises data sources:</span></span>

* <span data-ttu-id="237c8-192">Jeśli uwierzytelnianie SQL personifikacji powinna być konta usługi.</span><span class="sxs-lookup"><span data-stu-id="237c8-192">If using SQL authentication, impersonation should be Service Account.</span></span>
* <span data-ttu-id="237c8-193">Jeśli przy użyciu uwierzytelniania systemu Windows, należy ustawić hasło użytkownika systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="237c8-193">If using Windows authentication, set Windows user/password.</span></span> <span data-ttu-id="237c8-194">Dla programu SQL Server uwierzytelnianie systemu Windows przy użyciu konta personifikacji określonych jest obsługiwana tylko w przypadku modeli danych w pamięci.</span><span class="sxs-lookup"><span data-stu-id="237c8-194">For SQL Server, Windows authentication with a specific impersonation account is supported only for in-memory data models.</span></span>

<span data-ttu-id="237c8-195">Dla źródeł danych w chmurze:</span><span class="sxs-lookup"><span data-stu-id="237c8-195">For cloud data sources:</span></span>

* <span data-ttu-id="237c8-196">Jeśli uwierzytelnianie SQL personifikacji powinna być konta usługi.</span><span class="sxs-lookup"><span data-stu-id="237c8-196">If using SQL authentication, impersonation should be Service Account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="237c8-197">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="237c8-197">Next steps</span></span>
<span data-ttu-id="237c8-198">Jeśli masz lokalnych źródeł danych, należy zainstalować [brama lokalna](analysis-services-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="237c8-198">If you have on-premises data sources, be sure to install the [On-premises gateway](analysis-services-gateway.md).</span></span>   
<span data-ttu-id="237c8-199">Aby dowiedzieć się więcej na temat zarządzania serwerem w SSDT lub SSMS, zobacz [Zarządzanie serwerem](analysis-services-manage.md).</span><span class="sxs-lookup"><span data-stu-id="237c8-199">To learn more about managing your server in SSDT or SSMS, see [Manage your server](analysis-services-manage.md).</span></span>

