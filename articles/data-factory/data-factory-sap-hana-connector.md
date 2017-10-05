---
title: "Przenoszenia danych z programu SAP HANA przy użyciu fabryki danych Azure | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat sposobu przenoszenia danych z programu SAP HANA przy użyciu fabryki danych Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: 
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: 2ab488d82d24999a6231e40cb719715463c51d64
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-from-sap-hana-using-azure-data-factory"></a><span data-ttu-id="48232-103">Przenoszenie danych z SAP HANA przy użyciu fabryki danych Azure</span><span class="sxs-lookup"><span data-stu-id="48232-103">Move data From SAP HANA using Azure Data Factory</span></span>
<span data-ttu-id="48232-104">W tym artykule opisano sposób używania działania kopiowania w fabryce danych Azure do przenoszenia danych z lokalnego SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="48232-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises SAP HANA.</span></span> <span data-ttu-id="48232-105">Opiera się na [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, który przedstawia ogólny przegląd przenoszenia danych z działania kopiowania.</span><span class="sxs-lookup"><span data-stu-id="48232-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="48232-106">Wszystkie obsługiwanych ujścia magazynu danych można skopiować danych z lokalnego magazynu danych SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="48232-106">You can copy data from an on-premises SAP HANA data store to any supported sink data store.</span></span> <span data-ttu-id="48232-107">Lista magazynów danych obsługiwane jako wychwytywanie przez działanie kopiowania, zobacz [obsługiwane magazyny danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabeli.</span><span class="sxs-lookup"><span data-stu-id="48232-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="48232-108">Fabryka danych obsługują obecnie tylko danych przenoszenie, z SAP HANA do innych magazynów danych, ale nie do przenoszenia danych z innych magazynów danych do SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="48232-108">Data factory currently supports only moving data from an SAP HANA to other data stores, but not for moving data from other data stores to an SAP HANA.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="48232-109">Obsługiwane wersje i instalacji</span><span class="sxs-lookup"><span data-stu-id="48232-109">Supported versions and installation</span></span>
<span data-ttu-id="48232-110">Ten łącznik obsługuje dowolnej wersji bazy danych SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="48232-110">This connector supports any version of SAP HANA database.</span></span> <span data-ttu-id="48232-111">Obsługuje ona kopiowanie danych z tabel wierszy i kolumn, za pomocą zapytań SQL i HANA modelach informacji (takich jak widoki analityczne i obliczeń).</span><span class="sxs-lookup"><span data-stu-id="48232-111">It supports copying data from HANA information models (such as Analytic and Calculation views) and Row/Column tables using SQL queries.</span></span>

<span data-ttu-id="48232-112">Aby umożliwić łączność z wystąpieniem SAP HANA, należy zainstalować następujące składniki:</span><span class="sxs-lookup"><span data-stu-id="48232-112">To enable the connectivity to the SAP HANA instance, install the following components:</span></span>
- <span data-ttu-id="48232-113">**Brama zarządzania danymi**: łączenie z danymi lokalnymi obsługuje usługi fabryka danych magazynów (w tym SAP HANA) przy użyciu składnika o nazwie brama zarządzania danymi.</span><span class="sxs-lookup"><span data-stu-id="48232-113">**Data Management Gateway**: Data Factory service supports connecting to on-premises data stores (including SAP HANA) using a component called Data Management Gateway.</span></span> <span data-ttu-id="48232-114">Informacje na temat bramy zarządzania danymi i szczegółowe instrukcje dotyczące konfigurowania bramy, zobacz [przenoszenie danych między danymi lokalnymi magazynu do magazynu danych w chmurze](data-factory-move-data-between-onprem-and-cloud.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="48232-114">To learn about Data Management Gateway and step-by-step instructions for setting up the gateway, see [Moving data between on-premises data store to cloud data store](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span> <span data-ttu-id="48232-115">Nawet jeśli SAP HANA znajduje się na maszynie wirtualnej platformy Azure IaaS (VM), wymagana jest brama.</span><span class="sxs-lookup"><span data-stu-id="48232-115">Gateway is required even if the SAP HANA is hosted in an Azure IaaS virtual machine (VM).</span></span> <span data-ttu-id="48232-116">Można zainstalować bramę na tej samej maszyny Wirtualnej do przechowywania danych lub w innej maszyny Wirtualnej, tak długo, jak bramy można połączyć z bazą danych.</span><span class="sxs-lookup"><span data-stu-id="48232-116">You can install the gateway on the same VM as the data store or on a different VM as long as the gateway can connect to the database.</span></span>
- <span data-ttu-id="48232-117">**Sterownik SAP HANA ODBC** na komputerze bramy.</span><span class="sxs-lookup"><span data-stu-id="48232-117">**SAP HANA ODBC driver** on the gateway machine.</span></span> <span data-ttu-id="48232-118">Możesz pobrać sterownik SAP HANA ODBC z [Centrum pobierania oprogramowania SAP](https://support.sap.com/swdc).</span><span class="sxs-lookup"><span data-stu-id="48232-118">You can download the SAP HANA ODBC driver from the [SAP Software Download Center](https://support.sap.com/swdc).</span></span> <span data-ttu-id="48232-119">Wyszukiwanie ze słowem kluczowym **SAP HANA klienta dla systemu Windows**.</span><span class="sxs-lookup"><span data-stu-id="48232-119">Search with the keyword **SAP HANA CLIENT for Windows**.</span></span> 

## <a name="getting-started"></a><span data-ttu-id="48232-120">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="48232-120">Getting started</span></span>
<span data-ttu-id="48232-121">Można utworzyć potok z działania kopiowania, który przenosi dane z magazynu lokalnego Cassandra danych przy użyciu różnych narzędzi/interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="48232-121">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="48232-122">Najprostszym sposobem, aby utworzyć potok jest użycie **kreatora kopiowania**.</span><span class="sxs-lookup"><span data-stu-id="48232-122">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="48232-123">Zobacz [samouczek: tworzenie potoku za pomocą Kreatora kopiowania](data-factory-copy-data-wizard-tutorial.md) szybkie przewodnik dotyczący tworzenia potoku za pomocą Kreatora kopiowania danych.</span><span class="sxs-lookup"><span data-stu-id="48232-123">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span> 
- <span data-ttu-id="48232-124">Umożliwia także następujące narzędzia do tworzenia potoku: **portalu Azure**, **programu Visual Studio**, **programu Azure PowerShell**, **szablonu usługi Azure Resource Manager**, **interfejs API .NET**, i **interfejsu API REST**.</span><span class="sxs-lookup"><span data-stu-id="48232-124">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="48232-125">Zobacz [samouczek działania kopiowania](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) instrukcje krok po kroku utworzyć potok z działaniem kopiowania.</span><span class="sxs-lookup"><span data-stu-id="48232-125">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="48232-126">Czy można użyć narzędzia i interfejsy API, należy wykonać następujące kroki, aby utworzyć potok, który przenosi dane z magazynu danych źródła do ujścia magazynu danych:</span><span class="sxs-lookup"><span data-stu-id="48232-126">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="48232-127">Utwórz **połączone usługi** Aby połączyć dane wejściowe i wyjściowe są przechowywane w fabryce danych.</span><span class="sxs-lookup"><span data-stu-id="48232-127">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="48232-128">Utwórz **zestawów danych** do reprezentowania danych wejściowych i wyjściowych operacji kopiowania.</span><span class="sxs-lookup"><span data-stu-id="48232-128">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="48232-129">Utwórz **potoku** aktywnością kopiowania zestawu danych jako dane wejściowe i zestawu danych jako dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="48232-129">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="48232-130">Korzystając z kreatora, definicje JSON do tych jednostek fabryki danych (połączone usługi, zestawy danych i potoki) są tworzone automatycznie dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="48232-130">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="48232-131">Korzystając z narzędzi/API (z wyjątkiem interfejs API .NET), należy zdefiniować tych jednostek fabryki danych w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="48232-131">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="48232-132">Dla przykładu z definicji JSON dla jednostek fabryki danych, które są używane do skopiowania danych SAP HANA lokalnych, zobacz [przykład JSON: kopiowanie danych z programu SAP HANA do obiektów Blob platformy Azure](#json-example-copy-data-from-sap-hana-to-azure-blob) sekcji tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="48232-132">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises SAP HANA, see [JSON example: Copy data from SAP HANA to Azure Blob](#json-example-copy-data-from-sap-hana-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="48232-133">Poniższe sekcje zawierają szczegółowe informacje o właściwości JSON, które są używane do definiowania jednostek fabryki danych określonej do magazynu danych SAP HANA:</span><span class="sxs-lookup"><span data-stu-id="48232-133">The following sections provide details about JSON properties that are used to define Data Factory entities specific to an SAP HANA data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="48232-134">Połączona usługa właściwości</span><span class="sxs-lookup"><span data-stu-id="48232-134">Linked service properties</span></span>
<span data-ttu-id="48232-135">Poniższa tabela zawiera opis specyficzne dla usługi SAP HANA połączone elementy JSON.</span><span class="sxs-lookup"><span data-stu-id="48232-135">The following table provides description for JSON elements specific to SAP HANA linked service.</span></span>

<span data-ttu-id="48232-136">Właściwość</span><span class="sxs-lookup"><span data-stu-id="48232-136">Property</span></span> | <span data-ttu-id="48232-137">Opis</span><span class="sxs-lookup"><span data-stu-id="48232-137">Description</span></span> | <span data-ttu-id="48232-138">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="48232-138">Allowed values</span></span> | <span data-ttu-id="48232-139">Wymagane</span><span class="sxs-lookup"><span data-stu-id="48232-139">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="48232-140">serwer</span><span class="sxs-lookup"><span data-stu-id="48232-140">server</span></span> | <span data-ttu-id="48232-141">Nazwa serwera, na którym znajduje się z wystąpieniem SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="48232-141">Name of the server on which the SAP HANA instance resides.</span></span> <span data-ttu-id="48232-142">Jeśli serwer używa portu dostosowane, określ `server:port`.</span><span class="sxs-lookup"><span data-stu-id="48232-142">If your server is using a customized port, specify `server:port`.</span></span> | <span data-ttu-id="48232-143">Ciąg</span><span class="sxs-lookup"><span data-stu-id="48232-143">string</span></span> | <span data-ttu-id="48232-144">Tak</span><span class="sxs-lookup"><span data-stu-id="48232-144">Yes</span></span>
<span data-ttu-id="48232-145">Typ authenticationType</span><span class="sxs-lookup"><span data-stu-id="48232-145">authenticationType</span></span> | <span data-ttu-id="48232-146">Typ uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="48232-146">Type of authentication.</span></span> | <span data-ttu-id="48232-147">Ciąg.</span><span class="sxs-lookup"><span data-stu-id="48232-147">string.</span></span> <span data-ttu-id="48232-148">"Basic" lub "Windows"</span><span class="sxs-lookup"><span data-stu-id="48232-148">"Basic" or "Windows"</span></span> | <span data-ttu-id="48232-149">Tak</span><span class="sxs-lookup"><span data-stu-id="48232-149">Yes</span></span> 
<span data-ttu-id="48232-150">nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="48232-150">username</span></span> | <span data-ttu-id="48232-151">Nazwa użytkownika, który ma dostęp do serwera SAP</span><span class="sxs-lookup"><span data-stu-id="48232-151">Name of the user who has access to the SAP server</span></span> | <span data-ttu-id="48232-152">Ciąg</span><span class="sxs-lookup"><span data-stu-id="48232-152">string</span></span> | <span data-ttu-id="48232-153">Tak</span><span class="sxs-lookup"><span data-stu-id="48232-153">Yes</span></span>
<span data-ttu-id="48232-154">hasło</span><span class="sxs-lookup"><span data-stu-id="48232-154">password</span></span> | <span data-ttu-id="48232-155">Hasło dla użytkownika.</span><span class="sxs-lookup"><span data-stu-id="48232-155">Password for the user.</span></span> | <span data-ttu-id="48232-156">Ciąg</span><span class="sxs-lookup"><span data-stu-id="48232-156">string</span></span> | <span data-ttu-id="48232-157">Tak</span><span class="sxs-lookup"><span data-stu-id="48232-157">Yes</span></span>
<span data-ttu-id="48232-158">gatewayName</span><span class="sxs-lookup"><span data-stu-id="48232-158">gatewayName</span></span> | <span data-ttu-id="48232-159">Nazwa bramy, która powinna być używana przez usługi fabryka danych nawiązywania połączenia z lokalnym wystąpieniem SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="48232-159">Name of the gateway that the Data Factory service should use to connect to the on-premises SAP HANA instance.</span></span> | <span data-ttu-id="48232-160">Ciąg</span><span class="sxs-lookup"><span data-stu-id="48232-160">string</span></span> | <span data-ttu-id="48232-161">Tak</span><span class="sxs-lookup"><span data-stu-id="48232-161">Yes</span></span>
<span data-ttu-id="48232-162">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="48232-162">encryptedCredential</span></span> | <span data-ttu-id="48232-163">Ciąg zaszyfrowane poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="48232-163">The encrypted credential string.</span></span> | <span data-ttu-id="48232-164">Ciąg</span><span class="sxs-lookup"><span data-stu-id="48232-164">string</span></span> | <span data-ttu-id="48232-165">Nie</span><span class="sxs-lookup"><span data-stu-id="48232-165">No</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="48232-166">Właściwości zestawu danych</span><span class="sxs-lookup"><span data-stu-id="48232-166">Dataset properties</span></span>
<span data-ttu-id="48232-167">Aby uzyskać pełną listę sekcje & właściwości dostępne do definiowania zestawów danych, zobacz [Tworzenie zbiorów danych](data-factory-create-datasets.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="48232-167">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="48232-168">Sekcje zawierają informacje, takie jak struktury, dostępności i zasad zestawu danych JSON są podobne dla wszystkich typów obiektów dataset (Azure SQL, obiektów blob platformy Azure, Azure tabeli itp.).</span><span class="sxs-lookup"><span data-stu-id="48232-168">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="48232-169">**TypeProperties** sekcja jest różne dla każdego typu zestawu danych i zawiera informacje o lokalizacji danych w magazynie danych.</span><span class="sxs-lookup"><span data-stu-id="48232-169">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="48232-170">Nie ma żadnych właściwości specyficzne dla typu obsługiwane dla zestawu danych SAP HANA typu **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="48232-170">There are no type-specific properties supported for the SAP HANA dataset of type **RelationalTable**.</span></span> 


## <a name="copy-activity-properties"></a><span data-ttu-id="48232-171">Właściwości działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="48232-171">Copy activity properties</span></span>
<span data-ttu-id="48232-172">Pełną listę sekcje & właściwości dostępne do definiowania działań, zobacz [tworzenie potoków](data-factory-create-pipelines.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="48232-172">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="48232-173">Właściwości, takie jak nazwa, opis i tabel wejściowych i wyjściowych, czy zasady są dostępne dla wszystkich typów działań.</span><span class="sxs-lookup"><span data-stu-id="48232-173">Properties such as name, description, input and output tables, are policies are available for all types of activities.</span></span>

<span data-ttu-id="48232-174">Właściwości dostępne w **typeProperties** sekcji działania zależne od każdego typu działania.</span><span class="sxs-lookup"><span data-stu-id="48232-174">Whereas, properties available in the **typeProperties** section of the activity vary with each activity type.</span></span> <span data-ttu-id="48232-175">Dla działania kopiowania różnią się w zależności od typów źródeł i sink.</span><span class="sxs-lookup"><span data-stu-id="48232-175">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="48232-176">Gdy źródło w przypadku działania kopiowania jest typu **RelationalSource** (która obejmuje SAP HANA), w sekcji typeProperties dostępne są następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="48232-176">When source in copy activity is of type **RelationalSource** (which includes SAP HANA), the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="48232-177">Właściwość</span><span class="sxs-lookup"><span data-stu-id="48232-177">Property</span></span> | <span data-ttu-id="48232-178">Opis</span><span class="sxs-lookup"><span data-stu-id="48232-178">Description</span></span> | <span data-ttu-id="48232-179">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="48232-179">Allowed values</span></span> | <span data-ttu-id="48232-180">Wymagane</span><span class="sxs-lookup"><span data-stu-id="48232-180">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="48232-181">query</span><span class="sxs-lookup"><span data-stu-id="48232-181">query</span></span> | <span data-ttu-id="48232-182">Określa zapytanie SQL do odczytywania danych z wystąpieniem SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="48232-182">Specifies the SQL query to read data from the SAP HANA instance.</span></span> | <span data-ttu-id="48232-183">Zapytanie SQL.</span><span class="sxs-lookup"><span data-stu-id="48232-183">SQL query.</span></span> | <span data-ttu-id="48232-184">Tak</span><span class="sxs-lookup"><span data-stu-id="48232-184">Yes</span></span> |

## <a name="json-example-copy-data-from-sap-hana-to-azure-blob"></a><span data-ttu-id="48232-185">Przykład JSON: kopiowanie danych z programu SAP HANA do obiektów Blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="48232-185">JSON example: Copy data from SAP HANA to Azure Blob</span></span>
<span data-ttu-id="48232-186">Poniższy przykład zawiera definicje JSON, których można utworzyć potok przy użyciu [portalu Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) lub [programu Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) lub [programu Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="48232-186">The following sample provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="48232-187">W tym przykładzie pokazano, jak można skopiować danych z lokalnego SAP HANA do magazynu obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="48232-187">This sample shows how to copy data from an on-premises SAP HANA to an Azure Blob Storage.</span></span> <span data-ttu-id="48232-188">Jednak dane mogą być kopiowane **bezpośrednio** do dowolnego wychwytywanie wymienione [tutaj](data-factory-data-movement-activities.md#supported-data-stores-and-formats) za pomocą działania kopiowania w fabryce danych Azure.</span><span class="sxs-lookup"><span data-stu-id="48232-188">However, data can be copied **directly** to any of the sinks listed [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="48232-189">W tym przykładzie przedstawiono fragmenty kodu JSON.</span><span class="sxs-lookup"><span data-stu-id="48232-189">This sample provides JSON snippets.</span></span> <span data-ttu-id="48232-190">Zawiera instrukcje krok po kroku dotyczące tworzenia fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="48232-190">It does not include step-by-step instructions for creating the data factory.</span></span> <span data-ttu-id="48232-191">Zobacz [przenoszenie danych między lokalizacji lokalnej i w chmurze](data-factory-move-data-between-onprem-and-cloud.md) artykułu, aby uzyskać instrukcje krok po kroku.</span><span class="sxs-lookup"><span data-stu-id="48232-191">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="48232-192">Przykład zawiera następujące obiekty fabryki danych:</span><span class="sxs-lookup"><span data-stu-id="48232-192">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="48232-193">Połączonej usługi typu [SapHana](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="48232-193">A linked service of type [SapHana](#linked-service-properties).</span></span>
2. <span data-ttu-id="48232-194">Połączonej usługi typu [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="48232-194">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="48232-195">Dane wejściowe [dataset](data-factory-create-datasets.md) typu [RelationalTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="48232-195">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
4. <span data-ttu-id="48232-196">Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="48232-196">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="48232-197">A [potoku](data-factory-create-pipelines.md) z działaniem kopii, która używa [RelationalSource](#copy-activity-properties) i [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="48232-197">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="48232-198">Przykład kopiuje dane z wystąpieniem SAP HANA obiektów blob platformy Azure co godzinę.</span><span class="sxs-lookup"><span data-stu-id="48232-198">The sample copies data from an SAP HANA instance to an Azure blob hourly.</span></span> <span data-ttu-id="48232-199">Właściwości JSON używane w te przykłady są opisane w sekcjach poniżej próbek.</span><span class="sxs-lookup"><span data-stu-id="48232-199">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="48232-200">Pierwszym krokiem konfiguracji bramy zarządzania danymi.</span><span class="sxs-lookup"><span data-stu-id="48232-200">As a first step, setup the data management gateway.</span></span> <span data-ttu-id="48232-201">Instrukcje znajdują się w [przenoszenie danych między lokalizacji lokalnej i w chmurze](data-factory-move-data-between-onprem-and-cloud.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="48232-201">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

### <a name="sap-hana-linked-service"></a><span data-ttu-id="48232-202">SAP HANA połączone usługi</span><span class="sxs-lookup"><span data-stu-id="48232-202">SAP HANA linked service</span></span>
<span data-ttu-id="48232-203">To połączone usługi łączy wystąpieniem SAP HANA fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="48232-203">This linked service links your SAP HANA instance to the data factory.</span></span> <span data-ttu-id="48232-204">Właściwość type ma ustawioną **SapHana**.</span><span class="sxs-lookup"><span data-stu-id="48232-204">The type property is set to **SapHana**.</span></span> <span data-ttu-id="48232-205">Sekcja typeProperties zawiera informacje o połączeniu dla wystąpienia programu SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="48232-205">The typeProperties section provides connection information for the SAP HANA instance.</span></span>

```json
{
    "name": "SapHanaLinkedService",
    "properties":
    {
        "type": "SapHana",
        "typeProperties":
        {
            "server": "<server name>",
            "authenticationType": "<Basic, or Windows>",
            "username": "<SAP user>",
            "password": "<Password for SAP user>",
            "gatewayName": "<gateway name>"
        }
    }
}

```

### <a name="azure-storage-linked-service"></a><span data-ttu-id="48232-206">Połączona usługa Azure Storage</span><span class="sxs-lookup"><span data-stu-id="48232-206">Azure Storage linked service</span></span>
<span data-ttu-id="48232-207">Łącza usługi to połączone konta magazynu Azure do fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="48232-207">This linked service links your Azure Storage account to the data factory.</span></span> <span data-ttu-id="48232-208">Właściwość type ma ustawioną **AzureStorage**.</span><span class="sxs-lookup"><span data-stu-id="48232-208">The type property is set to **AzureStorage**.</span></span> <span data-ttu-id="48232-209">Sekcja typeProperties zawiera informacje o połączeniu dla konta usługi Magazyn Azure.</span><span class="sxs-lookup"><span data-stu-id="48232-209">The typeProperties section provides connection information for the Azure Storage account.</span></span>

```json
{
  "name": "AzureStorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```

### <a name="sap-hana-input-dataset"></a><span data-ttu-id="48232-210">Zestaw danych wejściowych SAP HANA</span><span class="sxs-lookup"><span data-stu-id="48232-210">SAP HANA input dataset</span></span>

<span data-ttu-id="48232-211">Ten zestaw danych definiuje zestaw danych SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="48232-211">This dataset defines the SAP HANA dataset.</span></span> <span data-ttu-id="48232-212">Ustaw typ fabryki danych zestawu danych do **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="48232-212">You set the type of the Data Factory dataset to **RelationalTable**.</span></span> <span data-ttu-id="48232-213">Obecnie nie określisz żadnych właściwości określonego typu dla zestawu danych SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="48232-213">Currently, you do not specify any type-specific properties for an SAP HANA dataset.</span></span> <span data-ttu-id="48232-214">Zapytania w definicji działania kopiowania Określa, jakie dane do odczytu z wystąpieniem SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="48232-214">The query in the Copy Activity definition specifies what data to read from the SAP HANA instance.</span></span> 

<span data-ttu-id="48232-215">Ustawienie właściwości zewnętrznych true informuje o usługi fabryka danych czy tabeli zewnętrznej dla fabryki danych i nie jest generowany przez działanie w fabryce danych.</span><span class="sxs-lookup"><span data-stu-id="48232-215">Setting external property to true informs the Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

<span data-ttu-id="48232-216">Częstotliwość i interwał właściwości definiuje harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="48232-216">Frequency and interval properties defines the schedule.</span></span> <span data-ttu-id="48232-217">W takim przypadku dane są odczytywane z wystąpieniem SAP HANA co godzinę.</span><span class="sxs-lookup"><span data-stu-id="48232-217">In this case, the data is read from the SAP HANA instance hourly.</span></span> 

```json
{
    "name": "SapHanaDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "SapHanaLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

### <a name="azure-blob-output-dataset"></a><span data-ttu-id="48232-218">Wyjściowy zestaw danych obiektów blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="48232-218">Azure Blob output dataset</span></span>
<span data-ttu-id="48232-219">Ten zestaw danych określa wyjściowego zestawu danych obiektów Blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="48232-219">This dataset defines the output Azure Blob dataset.</span></span> <span data-ttu-id="48232-220">Właściwość type ma ustawioną AzureBlob.</span><span class="sxs-lookup"><span data-stu-id="48232-220">The type property is set to AzureBlob.</span></span> <span data-ttu-id="48232-221">Sekcja typeProperties zawiera, gdzie są przechowywane dane skopiowane z wystąpieniem SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="48232-221">The typeProperties section provides where the data copied from the SAP HANA instance is stored.</span></span> <span data-ttu-id="48232-222">Dane są zapisywane do nowego obiektu blob co godzinę (częstotliwość: godziny, interwał: 1).</span><span class="sxs-lookup"><span data-stu-id="48232-222">The data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="48232-223">Ścieżka folderu dla obiekt blob jest dynamicznie obliczane na podstawie czasu rozpoczęcia wycinek, który jest przetwarzana.</span><span class="sxs-lookup"><span data-stu-id="48232-223">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="48232-224">Ścieżka folderu używa rok, miesiąc, dzień i godziny części czas rozpoczęcia.</span><span class="sxs-lookup"><span data-stu-id="48232-224">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```json
{
    "name": "AzureBlobDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/saphana/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            },
            "partitionedBy": [
                {
                    "name": "Year",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "yyyy"
                    }
                },
                {
                    "name": "Month",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "MM"
                    }
                },
                {
                    "name": "Day",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "dd"
                    }
                },
                {
                    "name": "Hour",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "HH"
                    }
                }
            ]
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```


### <a name="pipeline-with-copy-activity"></a><span data-ttu-id="48232-225">W potoku z działanie kopiowania</span><span class="sxs-lookup"><span data-stu-id="48232-225">Pipeline with Copy activity</span></span>

<span data-ttu-id="48232-226">Potok zawiera działanie kopiowania, który jest skonfigurowany do używania wejściowe i wyjściowe zestawy danych i jest zaplanowane co godzinę.</span><span class="sxs-lookup"><span data-stu-id="48232-226">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="48232-227">W definicji JSON potoku **źródła** ustawiono typ **RelationalSource** (dla źródła SAP HANA) i **zbiornika** ustawiono typ **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="48232-227">In the pipeline JSON definition, the **source** type is set to **RelationalSource** (for SAP HANA source) and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="48232-228">Określony dla zapytania SQL **zapytania** właściwości wybiera dane w ostatniej godziny do skopiowania.</span><span class="sxs-lookup"><span data-stu-id="48232-228">The SQL query specified for the **query** property selects the data in the past hour to copy.</span></span>

```json
{
    "name": "CopySapHanaToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "<SQL Query for HANA>"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "SapHanaDataset"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobDataSet"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "SapHanaToBlob"
            }
        ],
        "start": "2017-03-01T18:00:00Z",
        "end": "2017-03-01T19:00:00Z"
    }
}
```


### <a name="type-mapping-for-sap-hana"></a><span data-ttu-id="48232-229">Mapowanie typu dla SAP HANA</span><span class="sxs-lookup"><span data-stu-id="48232-229">Type mapping for SAP HANA</span></span>
<span data-ttu-id="48232-230">Jak wspomniano w [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, automatyczne konwersje z typów źródła do zbiornika typy z następujących rozwinięcie wykonuje działania kopiowania:</span><span class="sxs-lookup"><span data-stu-id="48232-230">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following two-step approach:</span></span>

1. <span data-ttu-id="48232-231">Konwertowanie typów natywnych źródła na typ architektury .NET</span><span class="sxs-lookup"><span data-stu-id="48232-231">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="48232-232">Konwertowanie na typ macierzysty ujścia typ architektury .NET</span><span class="sxs-lookup"><span data-stu-id="48232-232">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="48232-233">Podczas przenoszenia danych z programu SAP HANA, następujące mapowania są używane do typów .NET z typów SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="48232-233">When moving data from SAP HANA, the following mappings are used from SAP HANA types to .NET types.</span></span>

<span data-ttu-id="48232-234">SAP HANA typu</span><span class="sxs-lookup"><span data-stu-id="48232-234">SAP HANA Type</span></span> | <span data-ttu-id="48232-235">Typ na podstawie .NET</span><span class="sxs-lookup"><span data-stu-id="48232-235">.NET Based Type</span></span>
------------- | ---------------
<span data-ttu-id="48232-236">TINYINT</span><span class="sxs-lookup"><span data-stu-id="48232-236">TINYINT</span></span> | <span data-ttu-id="48232-237">Bajtów</span><span class="sxs-lookup"><span data-stu-id="48232-237">Byte</span></span>
<span data-ttu-id="48232-238">SMALLINT</span><span class="sxs-lookup"><span data-stu-id="48232-238">SMALLINT</span></span> | <span data-ttu-id="48232-239">Int16</span><span class="sxs-lookup"><span data-stu-id="48232-239">Int16</span></span>
<span data-ttu-id="48232-240">INT</span><span class="sxs-lookup"><span data-stu-id="48232-240">INT</span></span> | <span data-ttu-id="48232-241">Int32</span><span class="sxs-lookup"><span data-stu-id="48232-241">Int32</span></span>
<span data-ttu-id="48232-242">BIGINT</span><span class="sxs-lookup"><span data-stu-id="48232-242">BIGINT</span></span> | <span data-ttu-id="48232-243">Int64</span><span class="sxs-lookup"><span data-stu-id="48232-243">Int64</span></span>
<span data-ttu-id="48232-244">RZECZYWISTE</span><span class="sxs-lookup"><span data-stu-id="48232-244">REAL</span></span> | <span data-ttu-id="48232-245">Pojedynczy</span><span class="sxs-lookup"><span data-stu-id="48232-245">Single</span></span>
<span data-ttu-id="48232-246">O PODWÓJNEJ PRECYZJI</span><span class="sxs-lookup"><span data-stu-id="48232-246">DOUBLE</span></span> | <span data-ttu-id="48232-247">Pojedynczy</span><span class="sxs-lookup"><span data-stu-id="48232-247">Single</span></span>
<span data-ttu-id="48232-248">DECIMAL</span><span class="sxs-lookup"><span data-stu-id="48232-248">DECIMAL</span></span> | <span data-ttu-id="48232-249">Decimal</span><span class="sxs-lookup"><span data-stu-id="48232-249">Decimal</span></span>
<span data-ttu-id="48232-250">WARTOŚĆ LOGICZNA</span><span class="sxs-lookup"><span data-stu-id="48232-250">BOOLEAN</span></span> | <span data-ttu-id="48232-251">Bajtów</span><span class="sxs-lookup"><span data-stu-id="48232-251">Byte</span></span>
<span data-ttu-id="48232-252">VARCHAR</span><span class="sxs-lookup"><span data-stu-id="48232-252">VARCHAR</span></span> | <span data-ttu-id="48232-253">Ciąg</span><span class="sxs-lookup"><span data-stu-id="48232-253">String</span></span>
<span data-ttu-id="48232-254">NVARCHAR</span><span class="sxs-lookup"><span data-stu-id="48232-254">NVARCHAR</span></span> | <span data-ttu-id="48232-255">Ciąg</span><span class="sxs-lookup"><span data-stu-id="48232-255">String</span></span>
<span data-ttu-id="48232-256">CLOB</span><span class="sxs-lookup"><span data-stu-id="48232-256">CLOB</span></span> | <span data-ttu-id="48232-257">Byte]</span><span class="sxs-lookup"><span data-stu-id="48232-257">Byte[]</span></span>
<span data-ttu-id="48232-258">ALPHANUM</span><span class="sxs-lookup"><span data-stu-id="48232-258">ALPHANUM</span></span> | <span data-ttu-id="48232-259">Ciąg</span><span class="sxs-lookup"><span data-stu-id="48232-259">String</span></span>
<span data-ttu-id="48232-260">OBIEKT BLOB</span><span class="sxs-lookup"><span data-stu-id="48232-260">BLOB</span></span> | <span data-ttu-id="48232-261">Byte]</span><span class="sxs-lookup"><span data-stu-id="48232-261">Byte[]</span></span>
<span data-ttu-id="48232-262">DATA</span><span class="sxs-lookup"><span data-stu-id="48232-262">DATE</span></span> | <span data-ttu-id="48232-263">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="48232-263">DateTime</span></span>
<span data-ttu-id="48232-264">CZAS</span><span class="sxs-lookup"><span data-stu-id="48232-264">TIME</span></span> | <span data-ttu-id="48232-265">Zakres czasu</span><span class="sxs-lookup"><span data-stu-id="48232-265">TimeSpan</span></span>
<span data-ttu-id="48232-266">ZNACZNIK CZASU</span><span class="sxs-lookup"><span data-stu-id="48232-266">TIMESTAMP</span></span> | <span data-ttu-id="48232-267">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="48232-267">DateTime</span></span>
<span data-ttu-id="48232-268">SECONDDATE</span><span class="sxs-lookup"><span data-stu-id="48232-268">SECONDDATE</span></span> | <span data-ttu-id="48232-269">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="48232-269">DateTime</span></span>

## <a name="known-limitations"></a><span data-ttu-id="48232-270">Znane ograniczenia</span><span class="sxs-lookup"><span data-stu-id="48232-270">Known limitations</span></span>
<span data-ttu-id="48232-271">Podczas kopiowania danych z programu SAP HANA istnieje kilka znane ograniczenia:</span><span class="sxs-lookup"><span data-stu-id="48232-271">There are a few known limitations when copying data from SAP HANA:</span></span>

- <span data-ttu-id="48232-272">Ciągi NVARCHAR są zaokrąglane do maksymalnie 4000 znaków Unicode</span><span class="sxs-lookup"><span data-stu-id="48232-272">NVARCHAR strings are truncated to maximum length of 4000 Unicode characters</span></span>
- <span data-ttu-id="48232-273">SMALLDECIMAL nie jest obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="48232-273">SMALLDECIMAL is not supported</span></span>
- <span data-ttu-id="48232-274">VARBINARY nie jest obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="48232-274">VARBINARY is not supported</span></span>
- <span data-ttu-id="48232-275">Prawidłowe daty należą do zakresu od 30-1899/12, a 9999-12/31</span><span class="sxs-lookup"><span data-stu-id="48232-275">Valid Dates are between 1899/12/30 and 9999/12/31</span></span>

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="48232-276">Obiekt sink kolumn mapy źródła</span><span class="sxs-lookup"><span data-stu-id="48232-276">Map source to sink columns</span></span>
<span data-ttu-id="48232-277">Aby uzyskać informacje dotyczące mapowania kolumn w zestawie źródła danych do kolumn w zestawie danych zbiornika, zobacz [mapowania kolumnach dataset w fabryce danych Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="48232-277">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="48232-278">Odczyt powtarzalny ze źródłami relacyjnymi</span><span class="sxs-lookup"><span data-stu-id="48232-278">Repeatable read from relational sources</span></span>
<span data-ttu-id="48232-279">Podczas kopiowania danych z danych relacyjnych przechowuje, należy pamiętać, aby uniknąć niezamierzone wyniki powtarzalności.</span><span class="sxs-lookup"><span data-stu-id="48232-279">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="48232-280">Fabryka danych Azure możesz ponownie ręcznie wycinek.</span><span class="sxs-lookup"><span data-stu-id="48232-280">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="48232-281">Można również skonfigurować zasady ponawiania dla zestawu danych, aby wycinek jest uruchamiany ponownie, gdy wystąpi błąd.</span><span class="sxs-lookup"><span data-stu-id="48232-281">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="48232-282">Podczas wycinek zostanie uruchomiona ponownie w obu przypadkach, należy się upewnić, że te same dane jest do odczytu niezależnie od tego, ile razy wycinek jest uruchamiany.</span><span class="sxs-lookup"><span data-stu-id="48232-282">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="48232-283">Zobacz [Repeatable odczytywać relacyjne źródła](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span><span class="sxs-lookup"><span data-stu-id="48232-283">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="48232-284">Wydajność i dostrajania</span><span class="sxs-lookup"><span data-stu-id="48232-284">Performance and Tuning</span></span>
<span data-ttu-id="48232-285">Zobacz [wydajności działania kopiowania & dostrajanie przewodnik](data-factory-copy-activity-performance.md) Aby dowiedzieć się więcej o kluczowych czynników tego wydajność wpływ przenoszenia danych (działanie kopiowania) w usłudze fabryka danych Azure i zoptymalizować ją na różne sposoby.</span><span class="sxs-lookup"><span data-stu-id="48232-285">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
