---
title: "Przenoszenia danych z programu SAP Business Warehouse przy użyciu fabryki danych Azure | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat sposobu przenoszenia danych z programu SAP Business Warehouse przy użyciu fabryki danych Azure."
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
ms.date: 05/16/2017
ms.author: jingwang
ms.openlocfilehash: 220ccc8b94797880d335385046001c5f3b17c862
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-from-sap-business-warehouse-using-azure-data-factory"></a><span data-ttu-id="b90b1-103">Przenoszenie danych z programu SAP Business Warehouse przy użyciu fabryki danych Azure</span><span class="sxs-lookup"><span data-stu-id="b90b1-103">Move data From SAP Business Warehouse using Azure Data Factory</span></span>
<span data-ttu-id="b90b1-104">W tym artykule opisano sposób używania działania kopiowania w fabryce danych Azure do przenoszenia danych z lokalnego SAP Business magazynu (BW).</span><span class="sxs-lookup"><span data-stu-id="b90b1-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises SAP Business Warehouse (BW).</span></span> <span data-ttu-id="b90b1-105">Opiera się na [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, który przedstawia ogólny przegląd przenoszenia danych z działania kopiowania.</span><span class="sxs-lookup"><span data-stu-id="b90b1-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="b90b1-106">Można skopiować danych z lokalnego magazynu danych SAP Business Warehouse żadnych obsługiwanych ujścia magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="b90b1-106">You can copy data from an on-premises SAP Business Warehouse data store to any supported sink data store.</span></span> <span data-ttu-id="b90b1-107">Lista magazynów danych obsługiwane jako wychwytywanie przez działanie kopiowania, zobacz [obsługiwane magazyny danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabeli.</span><span class="sxs-lookup"><span data-stu-id="b90b1-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="b90b1-108">Fabryki danych aktualnie obsługuje tylko dane przenoszenie, z SAP Business Warehouse do innych magazynów danych, ale nie do przenoszenia danych z innych magazynów danych do programu SAP Business Warehouse.</span><span class="sxs-lookup"><span data-stu-id="b90b1-108">Data factory currently supports only moving data from an SAP Business Warehouse to other data stores, but not for moving data from other data stores to an SAP Business Warehouse.</span></span> 

## <a name="supported-versions-and-installation"></a><span data-ttu-id="b90b1-109">Obsługiwane wersje i instalacji</span><span class="sxs-lookup"><span data-stu-id="b90b1-109">Supported versions and installation</span></span>
<span data-ttu-id="b90b1-110">Ten łącznik obsługuje wersję SAP Business Warehouse 7.x.</span><span class="sxs-lookup"><span data-stu-id="b90b1-110">This connector supports SAP Business Warehouse version 7.x.</span></span> <span data-ttu-id="b90b1-111">Obsługuje ona kopiowania danych z InfoCubes i QueryCubes (takie jak zapytania BEx) przy użyciu zapytania MDX.</span><span class="sxs-lookup"><span data-stu-id="b90b1-111">It supports copying data from InfoCubes and QueryCubes (including BEx queries) using MDX queries.</span></span>

<span data-ttu-id="b90b1-112">Aby umożliwić łączność z wystąpienia programu SAP BW, należy zainstalować następujące składniki:</span><span class="sxs-lookup"><span data-stu-id="b90b1-112">To enable the connectivity to the SAP BW instance, install the following components:</span></span>
- <span data-ttu-id="b90b1-113">**Brama zarządzania danymi**: łączenie z danymi lokalnymi obsługuje usługi fabryka danych magazynów (w tym SAP Business Warehouse) przy użyciu składnika o nazwie brama zarządzania danymi.</span><span class="sxs-lookup"><span data-stu-id="b90b1-113">**Data Management Gateway**: Data Factory service supports connecting to on-premises data stores (including SAP Business Warehouse) using a component called Data Management Gateway.</span></span> <span data-ttu-id="b90b1-114">Informacje na temat bramy zarządzania danymi i szczegółowe instrukcje dotyczące konfigurowania bramy, zobacz [przenoszenie danych między danymi lokalnymi magazynu do magazynu danych w chmurze](data-factory-move-data-between-onprem-and-cloud.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="b90b1-114">To learn about Data Management Gateway and step-by-step instructions for setting up the gateway, see [Moving data between on-premises data store to cloud data store](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span> <span data-ttu-id="b90b1-115">Nawet jeśli SAP Business Warehouse znajduje się na maszynie wirtualnej platformy Azure IaaS (VM), wymagana jest brama.</span><span class="sxs-lookup"><span data-stu-id="b90b1-115">Gateway is required even if the SAP Business Warehouse is hosted in an Azure IaaS virtual machine (VM).</span></span> <span data-ttu-id="b90b1-116">Można zainstalować bramę na tej samej maszyny Wirtualnej do przechowywania danych lub w innej maszyny Wirtualnej, tak długo, jak bramy można połączyć z bazą danych.</span><span class="sxs-lookup"><span data-stu-id="b90b1-116">You can install the gateway on the same VM as the data store or on a different VM as long as the gateway can connect to the database.</span></span>
- <span data-ttu-id="b90b1-117">**SAP NetWeaver biblioteki** na komputerze bramy.</span><span class="sxs-lookup"><span data-stu-id="b90b1-117">**SAP NetWeaver library** on the gateway machine.</span></span> <span data-ttu-id="b90b1-118">Biblioteka SAP Netweaver można uzyskać od administratora SAP, lub bezpośrednio z [Centrum pobierania oprogramowania SAP](https://support.sap.com/swdc).</span><span class="sxs-lookup"><span data-stu-id="b90b1-118">You can get the SAP Netweaver library from your SAP administrator, or directly from the [SAP Software Download Center](https://support.sap.com/swdc).</span></span> <span data-ttu-id="b90b1-119">Wyszukaj **&#1025361; Uwaga SAP** można pobrać lokalizację pobierania najnowszej wersji.</span><span class="sxs-lookup"><span data-stu-id="b90b1-119">Search for the **SAP Note #1025361** to get the download location for the most recent version.</span></span> <span data-ttu-id="b90b1-120">Upewnij się, czy architektura biblioteki SAP NetWeaver (32-bitowy lub 64-bitowy) jest zgodna instalacji bramy.</span><span class="sxs-lookup"><span data-stu-id="b90b1-120">Make sure that the architecture for the SAP NetWeaver library (32-bit or 64-bit) matches your gateway installation.</span></span> <span data-ttu-id="b90b1-121">Następnie zainstaluj wszystkie pliki zawarte w zestawie SDK programu SAP NetWeaver RFC zgodnie z Uwaga SAP.</span><span class="sxs-lookup"><span data-stu-id="b90b1-121">Then install all files included in the SAP NetWeaver RFC SDK according to the SAP Note.</span></span> <span data-ttu-id="b90b1-122">Biblioteka programu SAP NetWeaver znajduje się również w narzędziach klienckich SAP instalacji.</span><span class="sxs-lookup"><span data-stu-id="b90b1-122">The SAP NetWeaver library is also included in the SAP Client Tools installation.</span></span>

> [!TIP]
> <span data-ttu-id="b90b1-123">Umieść wyodrębniony z zestawu SDK RFC NetWeaver w folderze system32 bibliotek DLL.</span><span class="sxs-lookup"><span data-stu-id="b90b1-123">Put the dlls extracted from the NetWeaver RFC SDK into system32 folder.</span></span>

## <a name="getting-started"></a><span data-ttu-id="b90b1-124">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="b90b1-124">Getting started</span></span>
<span data-ttu-id="b90b1-125">Można utworzyć potok z działania kopiowania, który przenosi dane z magazynu lokalnego Cassandra danych przy użyciu różnych narzędzi/interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="b90b1-125">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="b90b1-126">Najprostszym sposobem, aby utworzyć potok jest użycie **kreatora kopiowania**.</span><span class="sxs-lookup"><span data-stu-id="b90b1-126">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="b90b1-127">Zobacz [samouczek: tworzenie potoku za pomocą Kreatora kopiowania](data-factory-copy-data-wizard-tutorial.md) szybkie przewodnik dotyczący tworzenia potoku za pomocą Kreatora kopiowania danych.</span><span class="sxs-lookup"><span data-stu-id="b90b1-127">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span> 
- <span data-ttu-id="b90b1-128">Umożliwia także następujące narzędzia do tworzenia potoku: **portalu Azure**, **programu Visual Studio**, **programu Azure PowerShell**, **szablonu usługi Azure Resource Manager**, **interfejs API .NET**, i **interfejsu API REST**.</span><span class="sxs-lookup"><span data-stu-id="b90b1-128">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="b90b1-129">Zobacz [samouczek działania kopiowania](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) instrukcje krok po kroku utworzyć potok z działaniem kopiowania.</span><span class="sxs-lookup"><span data-stu-id="b90b1-129">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="b90b1-130">Czy można użyć narzędzia i interfejsy API, należy wykonać następujące kroki, aby utworzyć potok, który przenosi dane z magazynu danych źródła do ujścia magazynu danych:</span><span class="sxs-lookup"><span data-stu-id="b90b1-130">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="b90b1-131">Utwórz **połączone usługi** Aby połączyć dane wejściowe i wyjściowe są przechowywane w fabryce danych.</span><span class="sxs-lookup"><span data-stu-id="b90b1-131">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="b90b1-132">Utwórz **zestawów danych** do reprezentowania danych wejściowych i wyjściowych operacji kopiowania.</span><span class="sxs-lookup"><span data-stu-id="b90b1-132">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="b90b1-133">Utwórz **potoku** aktywnością kopiowania zestawu danych jako dane wejściowe i zestawu danych jako dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="b90b1-133">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="b90b1-134">Korzystając z kreatora, definicje JSON do tych jednostek fabryki danych (połączone usługi, zestawy danych i potoki) są tworzone automatycznie dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="b90b1-134">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="b90b1-135">Korzystając z narzędzi/API (z wyjątkiem interfejs API .NET), należy zdefiniować tych jednostek fabryki danych w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="b90b1-135">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="b90b1-136">Dla przykładu z definicji JSON dla jednostek fabryki danych, które są używane do skopiowania danych z lokalnego SAP Business Warehouse, zobacz [przykład JSON: kopiowanie danych z programu SAP Business Warehouse do obiektów Blob platformy Azure](#json-example-copy-data-from-sap-business-warehouse-to-azure-blob) sekcji tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="b90b1-136">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises SAP Business Warehouse, see [JSON example: Copy data from SAP Business Warehouse to Azure Blob](#json-example-copy-data-from-sap-business-warehouse-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="b90b1-137">Poniższe sekcje zawierają szczegółowe informacje o właściwości JSON, które są używane do definiowania jednostek fabryki danych określonej do magazynu danych programu SAP BW:</span><span class="sxs-lookup"><span data-stu-id="b90b1-137">The following sections provide details about JSON properties that are used to define Data Factory entities specific to an SAP BW data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="b90b1-138">Połączona usługa właściwości</span><span class="sxs-lookup"><span data-stu-id="b90b1-138">Linked service properties</span></span>
<span data-ttu-id="b90b1-139">Poniższa tabela zawiera opis specyficzne dla usługi programu SAP Business magazynu (BW) połączone elementy JSON.</span><span class="sxs-lookup"><span data-stu-id="b90b1-139">The following table provides description for JSON elements specific to SAP Business Warehouse (BW) linked service.</span></span>

<span data-ttu-id="b90b1-140">Właściwość</span><span class="sxs-lookup"><span data-stu-id="b90b1-140">Property</span></span> | <span data-ttu-id="b90b1-141">Opis</span><span class="sxs-lookup"><span data-stu-id="b90b1-141">Description</span></span> | <span data-ttu-id="b90b1-142">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="b90b1-142">Allowed values</span></span> | <span data-ttu-id="b90b1-143">Wymagane</span><span class="sxs-lookup"><span data-stu-id="b90b1-143">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="b90b1-144">serwer</span><span class="sxs-lookup"><span data-stu-id="b90b1-144">server</span></span> | <span data-ttu-id="b90b1-145">Nazwa serwera, na którym znajduje się wystąpienie programu SAP BW.</span><span class="sxs-lookup"><span data-stu-id="b90b1-145">Name of the server on which the SAP BW instance resides.</span></span> | <span data-ttu-id="b90b1-146">Ciąg</span><span class="sxs-lookup"><span data-stu-id="b90b1-146">string</span></span> | <span data-ttu-id="b90b1-147">Tak</span><span class="sxs-lookup"><span data-stu-id="b90b1-147">Yes</span></span>
<span data-ttu-id="b90b1-148">systemNumber</span><span class="sxs-lookup"><span data-stu-id="b90b1-148">systemNumber</span></span> | <span data-ttu-id="b90b1-149">Numer systemu systemu SAP BW.</span><span class="sxs-lookup"><span data-stu-id="b90b1-149">System number of the SAP BW system.</span></span> | <span data-ttu-id="b90b1-150">Liczba dziesiętna dwucyfrowe reprezentowany jako ciąg.</span><span class="sxs-lookup"><span data-stu-id="b90b1-150">Two-digit decimal number represented as a string.</span></span> | <span data-ttu-id="b90b1-151">Tak</span><span class="sxs-lookup"><span data-stu-id="b90b1-151">Yes</span></span>
<span data-ttu-id="b90b1-152">clientId</span><span class="sxs-lookup"><span data-stu-id="b90b1-152">clientId</span></span> | <span data-ttu-id="b90b1-153">Identyfikator klienta w systemie SAP W klienta.</span><span class="sxs-lookup"><span data-stu-id="b90b1-153">Client ID of the client in the SAP W system.</span></span> | <span data-ttu-id="b90b1-154">Trzycyfrowa liczba dziesiętna reprezentowany jako ciąg.</span><span class="sxs-lookup"><span data-stu-id="b90b1-154">Three-digit decimal number represented as a string.</span></span> | <span data-ttu-id="b90b1-155">Tak</span><span class="sxs-lookup"><span data-stu-id="b90b1-155">Yes</span></span>
<span data-ttu-id="b90b1-156">nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="b90b1-156">username</span></span> | <span data-ttu-id="b90b1-157">Nazwa użytkownika, który ma dostęp do serwera SAP</span><span class="sxs-lookup"><span data-stu-id="b90b1-157">Name of the user who has access to the SAP server</span></span> | <span data-ttu-id="b90b1-158">Ciąg</span><span class="sxs-lookup"><span data-stu-id="b90b1-158">string</span></span> | <span data-ttu-id="b90b1-159">Tak</span><span class="sxs-lookup"><span data-stu-id="b90b1-159">Yes</span></span>
<span data-ttu-id="b90b1-160">hasło</span><span class="sxs-lookup"><span data-stu-id="b90b1-160">password</span></span> | <span data-ttu-id="b90b1-161">Hasło dla użytkownika.</span><span class="sxs-lookup"><span data-stu-id="b90b1-161">Password for the user.</span></span> | <span data-ttu-id="b90b1-162">Ciąg</span><span class="sxs-lookup"><span data-stu-id="b90b1-162">string</span></span> | <span data-ttu-id="b90b1-163">Tak</span><span class="sxs-lookup"><span data-stu-id="b90b1-163">Yes</span></span>
<span data-ttu-id="b90b1-164">gatewayName</span><span class="sxs-lookup"><span data-stu-id="b90b1-164">gatewayName</span></span> | <span data-ttu-id="b90b1-165">Nazwa bramy, która powinna być używana do nawiązania połączenia lokalnego wystąpienia programu SAP BW usługi fabryka danych.</span><span class="sxs-lookup"><span data-stu-id="b90b1-165">Name of the gateway that the Data Factory service should use to connect to the on-premises SAP BW instance.</span></span> | <span data-ttu-id="b90b1-166">Ciąg</span><span class="sxs-lookup"><span data-stu-id="b90b1-166">string</span></span> | <span data-ttu-id="b90b1-167">Tak</span><span class="sxs-lookup"><span data-stu-id="b90b1-167">Yes</span></span>
<span data-ttu-id="b90b1-168">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="b90b1-168">encryptedCredential</span></span> | <span data-ttu-id="b90b1-169">Ciąg zaszyfrowane poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="b90b1-169">The encrypted credential string.</span></span> | <span data-ttu-id="b90b1-170">Ciąg</span><span class="sxs-lookup"><span data-stu-id="b90b1-170">string</span></span> | <span data-ttu-id="b90b1-171">Nie</span><span class="sxs-lookup"><span data-stu-id="b90b1-171">No</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="b90b1-172">Właściwości zestawu danych</span><span class="sxs-lookup"><span data-stu-id="b90b1-172">Dataset properties</span></span>
<span data-ttu-id="b90b1-173">Aby uzyskać pełną listę sekcje & właściwości dostępne do definiowania zestawów danych, zobacz [Tworzenie zbiorów danych](data-factory-create-datasets.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="b90b1-173">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="b90b1-174">Sekcje zawierają informacje, takie jak struktury, dostępności i zasad zestawu danych JSON są podobne dla wszystkich typów obiektów dataset (Azure SQL, obiektów blob platformy Azure, Azure tabeli itp.).</span><span class="sxs-lookup"><span data-stu-id="b90b1-174">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="b90b1-175">**TypeProperties** sekcja jest różne dla każdego typu zestawu danych i zawiera informacje o lokalizacji danych w magazynie danych.</span><span class="sxs-lookup"><span data-stu-id="b90b1-175">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="b90b1-176">Nie ma żadnych właściwości specyficzne dla typu obsługiwane dla zestawu danych SAP BW typu **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="b90b1-176">There are no type-specific properties supported for the SAP BW dataset of type **RelationalTable**.</span></span> 


## <a name="copy-activity-properties"></a><span data-ttu-id="b90b1-177">Właściwości działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="b90b1-177">Copy activity properties</span></span>
<span data-ttu-id="b90b1-178">Pełną listę sekcje & właściwości dostępne do definiowania działań, zobacz [tworzenie potoków](data-factory-create-pipelines.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="b90b1-178">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="b90b1-179">Właściwości, takie jak nazwa, opis i tabel wejściowych i wyjściowych, czy zasady są dostępne dla wszystkich typów działań.</span><span class="sxs-lookup"><span data-stu-id="b90b1-179">Properties such as name, description, input and output tables, are policies are available for all types of activities.</span></span>

<span data-ttu-id="b90b1-180">Właściwości dostępne w **typeProperties** sekcji działania zależne od każdego typu działania.</span><span class="sxs-lookup"><span data-stu-id="b90b1-180">Whereas, properties available in the **typeProperties** section of the activity vary with each activity type.</span></span> <span data-ttu-id="b90b1-181">Dla działania kopiowania różnią się w zależności od typów źródeł i sink.</span><span class="sxs-lookup"><span data-stu-id="b90b1-181">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="b90b1-182">Gdy źródło w przypadku działania kopiowania jest typu **RelationalSource** (która obejmuje programu SAP BW), w sekcji typeProperties dostępne są następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="b90b1-182">When source in copy activity is of type **RelationalSource** (which includes SAP BW), the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="b90b1-183">Właściwość</span><span class="sxs-lookup"><span data-stu-id="b90b1-183">Property</span></span> | <span data-ttu-id="b90b1-184">Opis</span><span class="sxs-lookup"><span data-stu-id="b90b1-184">Description</span></span> | <span data-ttu-id="b90b1-185">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="b90b1-185">Allowed values</span></span> | <span data-ttu-id="b90b1-186">Wymagane</span><span class="sxs-lookup"><span data-stu-id="b90b1-186">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b90b1-187">query</span><span class="sxs-lookup"><span data-stu-id="b90b1-187">query</span></span> | <span data-ttu-id="b90b1-188">Określa zapytanie MDX, które można odczytać danych z wystąpienia programu SAP BW.</span><span class="sxs-lookup"><span data-stu-id="b90b1-188">Specifies the MDX query to read data from the SAP BW instance.</span></span> | <span data-ttu-id="b90b1-189">Zapytania MDX.</span><span class="sxs-lookup"><span data-stu-id="b90b1-189">MDX query.</span></span> | <span data-ttu-id="b90b1-190">Tak</span><span class="sxs-lookup"><span data-stu-id="b90b1-190">Yes</span></span> |


## <a name="json-example-copy-data-from-sap-business-warehouse-to-azure-blob"></a><span data-ttu-id="b90b1-191">Przykład JSON: kopiowanie danych z programu SAP Business Warehouse do obiektów Blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="b90b1-191">JSON example: Copy data from SAP Business Warehouse to Azure Blob</span></span>
<span data-ttu-id="b90b1-192">W poniższym przykładzie przedstawiono przykładowe definicje JSON, które można użyć, aby utworzyć potok przy użyciu [portalu Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) lub [programu Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) lub [programu Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="b90b1-192">The following example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="b90b1-193">W tym przykładzie pokazano, jak można skopiować danych z lokalnego SAP Business Warehouse do magazynu obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="b90b1-193">This sample shows how to copy data from an on-premises SAP Business Warehouse to an Azure Blob Storage.</span></span> <span data-ttu-id="b90b1-194">Jednak dane mogą być kopiowane **bezpośrednio** do dowolnego wychwytywanie podane [tutaj](data-factory-data-movement-activities.md#supported-data-stores-and-formats) za pomocą działania kopiowania w fabryce danych Azure.</span><span class="sxs-lookup"><span data-stu-id="b90b1-194">However, data can be copied **directly** to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="b90b1-195">W tym przykładzie przedstawiono fragmenty kodu JSON.</span><span class="sxs-lookup"><span data-stu-id="b90b1-195">This sample provides JSON snippets.</span></span> <span data-ttu-id="b90b1-196">Zawiera instrukcje krok po kroku dotyczące tworzenia fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="b90b1-196">It does not include step-by-step instructions for creating the data factory.</span></span> <span data-ttu-id="b90b1-197">Zobacz [przenoszenie danych między lokalizacji lokalnej i w chmurze](data-factory-move-data-between-onprem-and-cloud.md) artykułu, aby uzyskać instrukcje krok po kroku.</span><span class="sxs-lookup"><span data-stu-id="b90b1-197">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="b90b1-198">Przykład zawiera następujące obiekty fabryki danych:</span><span class="sxs-lookup"><span data-stu-id="b90b1-198">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="b90b1-199">Połączonej usługi typu [SapBw](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="b90b1-199">A linked service of type [SapBw](#linked-service-properties).</span></span>
2. <span data-ttu-id="b90b1-200">Połączonej usługi typu [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="b90b1-200">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="b90b1-201">Dane wejściowe [dataset](data-factory-create-datasets.md) typu [RelationalTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="b90b1-201">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
4. <span data-ttu-id="b90b1-202">Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="b90b1-202">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="b90b1-203">A [potoku](data-factory-create-pipelines.md) z działaniem kopii, która używa [RelationalSource](#copy-activity-properties) i [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="b90b1-203">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="b90b1-204">Przykład kopiuje dane z wystąpieniem SAP Business Warehouse obiektów blob platformy Azure co godzinę.</span><span class="sxs-lookup"><span data-stu-id="b90b1-204">The sample copies data from an SAP Business Warehouse instance to an Azure blob hourly.</span></span> <span data-ttu-id="b90b1-205">Właściwości JSON używane w te przykłady są opisane w sekcjach poniżej próbek.</span><span class="sxs-lookup"><span data-stu-id="b90b1-205">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="b90b1-206">Pierwszym krokiem konfiguracji bramy zarządzania danymi.</span><span class="sxs-lookup"><span data-stu-id="b90b1-206">As a first step, setup the data management gateway.</span></span> <span data-ttu-id="b90b1-207">Instrukcje znajdują się w [przenoszenie danych między lokalizacji lokalnej i w chmurze](data-factory-move-data-between-onprem-and-cloud.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="b90b1-207">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

### <a name="sap-business-warehouse-linked-service"></a><span data-ttu-id="b90b1-208">SAP Business Warehouse połączona usługa</span><span class="sxs-lookup"><span data-stu-id="b90b1-208">SAP Business Warehouse linked service</span></span>
<span data-ttu-id="b90b1-209">To połączone usługi łączy wystąpienia programu SAP BW fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="b90b1-209">This linked service links your SAP BW instance to the data factory.</span></span> <span data-ttu-id="b90b1-210">Właściwość type ma ustawioną **SapBw**.</span><span class="sxs-lookup"><span data-stu-id="b90b1-210">The type property is set to **SapBw**.</span></span> <span data-ttu-id="b90b1-211">Sekcja typeProperties zawiera informacje o połączeniu dla wystąpienia programu SAP BW.</span><span class="sxs-lookup"><span data-stu-id="b90b1-211">The typeProperties section provides connection information for the SAP BW instance.</span></span> 

```json
{
    "name": "SapBwLinkedService",
    "properties":
    {
        "type": "SapBw",
        "typeProperties":
        {
            "server": "<server name>",
            "systemNumber": "<system number>",
            "clientId": "<client id>",
            "username": "<SAP user>",
            "password": "<Password for SAP user>",
            "gatewayName": "<gateway name>"
        }
    }
}
```

### <a name="azure-storage-linked-service"></a><span data-ttu-id="b90b1-212">Połączona usługa Azure Storage</span><span class="sxs-lookup"><span data-stu-id="b90b1-212">Azure Storage linked service</span></span>
<span data-ttu-id="b90b1-213">Łącza usługi to połączone konta magazynu Azure do fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="b90b1-213">This linked service links your Azure Storage account to the data factory.</span></span> <span data-ttu-id="b90b1-214">Właściwość type ma ustawioną **AzureStorage**.</span><span class="sxs-lookup"><span data-stu-id="b90b1-214">The type property is set to **AzureStorage**.</span></span> <span data-ttu-id="b90b1-215">Sekcja typeProperties zawiera informacje o połączeniu dla konta usługi Magazyn Azure.</span><span class="sxs-lookup"><span data-stu-id="b90b1-215">The typeProperties section provides connection information for the Azure Storage account.</span></span>

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

### <a name="sap-bw-input-dataset"></a><span data-ttu-id="b90b1-216">Wejściowy zestaw danych SAP BW</span><span class="sxs-lookup"><span data-stu-id="b90b1-216">SAP BW input dataset</span></span>
<span data-ttu-id="b90b1-217">Ten zestaw danych definiuje zestaw danych SAP Business Warehouse.</span><span class="sxs-lookup"><span data-stu-id="b90b1-217">This dataset defines the SAP Business Warehouse dataset.</span></span> <span data-ttu-id="b90b1-218">Ustaw typ fabryki danych zestawu danych do **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="b90b1-218">You set the type of the Data Factory dataset to **RelationalTable**.</span></span> <span data-ttu-id="b90b1-219">Obecnie nie określisz żadnych właściwości określonego typu dla programu SAP BW zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="b90b1-219">Currently, you do not specify any type-specific properties for an SAP BW dataset.</span></span> <span data-ttu-id="b90b1-220">Zapytania w definicji działania kopiowania Określa, jakie dane do odczytu z wystąpienia programu SAP BW.</span><span class="sxs-lookup"><span data-stu-id="b90b1-220">The query in the Copy Activity definition specifies what data to read from the SAP BW instance.</span></span> 

<span data-ttu-id="b90b1-221">Ustawienie właściwości zewnętrznych true informuje o usługi fabryka danych czy tabeli zewnętrznej dla fabryki danych i nie jest generowany przez działanie w fabryce danych.</span><span class="sxs-lookup"><span data-stu-id="b90b1-221">Setting external property to true informs the Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

<span data-ttu-id="b90b1-222">Częstotliwość i interwał właściwości definiuje harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="b90b1-222">Frequency and interval properties defines the schedule.</span></span> <span data-ttu-id="b90b1-223">W takim przypadku dane są odczytywane z wystąpienia programu SAP BW co godzinę.</span><span class="sxs-lookup"><span data-stu-id="b90b1-223">In this case, the data is read from the SAP BW instance hourly.</span></span> 

```json
{
    "name": "SapBwDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "SapBwLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```



### <a name="azure-blob-output-dataset"></a><span data-ttu-id="b90b1-224">Wyjściowy zestaw danych obiektów blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="b90b1-224">Azure Blob output dataset</span></span>
<span data-ttu-id="b90b1-225">Ten zestaw danych określa wyjściowego zestawu danych obiektów Blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b90b1-225">This dataset defines the output Azure Blob dataset.</span></span> <span data-ttu-id="b90b1-226">Właściwość type ma ustawioną AzureBlob.</span><span class="sxs-lookup"><span data-stu-id="b90b1-226">The type property is set to AzureBlob.</span></span> <span data-ttu-id="b90b1-227">Sekcji typeProperties miejsce, w którym są przechowywane dane skopiowane z wystąpienia programu SAP BW.</span><span class="sxs-lookup"><span data-stu-id="b90b1-227">The typeProperties section provides where the data copied from the SAP BW instance is stored.</span></span> <span data-ttu-id="b90b1-228">Dane są zapisywane do nowego obiektu blob co godzinę (częstotliwość: godziny, interwał: 1).</span><span class="sxs-lookup"><span data-stu-id="b90b1-228">The data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="b90b1-229">Ścieżka folderu dla obiekt blob jest dynamicznie obliczane na podstawie czasu rozpoczęcia wycinek, który jest przetwarzana.</span><span class="sxs-lookup"><span data-stu-id="b90b1-229">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="b90b1-230">Ścieżka folderu używa rok, miesiąc, dzień i godziny części czas rozpoczęcia.</span><span class="sxs-lookup"><span data-stu-id="b90b1-230">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```json
{
    "name": "AzureBlobDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/sapbw/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


### <a name="pipeline-with-copy-activity"></a><span data-ttu-id="b90b1-231">W potoku z działanie kopiowania</span><span class="sxs-lookup"><span data-stu-id="b90b1-231">Pipeline with Copy activity</span></span>
<span data-ttu-id="b90b1-232">Potok zawiera działanie kopiowania, który jest skonfigurowany do używania wejściowe i wyjściowe zestawy danych i jest zaplanowane co godzinę.</span><span class="sxs-lookup"><span data-stu-id="b90b1-232">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="b90b1-233">W definicji JSON potoku **źródła** ustawiono typ **RelationalSource** (dla programu SAP BW źródła) i **zbiornika** ustawiono typ **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="b90b1-233">In the pipeline JSON definition, the **source** type is set to **RelationalSource** (for SAP BW source) and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="b90b1-234">Zapytanie określone dla **zapytania** właściwości wybiera dane w ostatniej godziny do skopiowania.</span><span class="sxs-lookup"><span data-stu-id="b90b1-234">The query specified for the **query** property selects the data in the past hour to copy.</span></span>

```json
{
    "name": "CopySapBwToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "<MDX query for SAP BW>"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "SapBwDataset"
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
                "name": "SapBwToBlob"
            }
        ],
        "start": "2017-03-01T18:00:00Z",
        "end": "2017-03-01T19:00:00Z"
    }
}
```



### <a name="type-mapping-for-sap-bw"></a><span data-ttu-id="b90b1-235">Mapowanie typu dla programu SAP BW</span><span class="sxs-lookup"><span data-stu-id="b90b1-235">Type mapping for SAP BW</span></span>
<span data-ttu-id="b90b1-236">Jak wspomniano w [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, automatyczne konwersje z typów źródła do zbiornika typy z następujących rozwinięcie wykonuje działania kopiowania:</span><span class="sxs-lookup"><span data-stu-id="b90b1-236">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following two-step approach:</span></span>

1. <span data-ttu-id="b90b1-237">Konwertowanie typów natywnych źródła na typ architektury .NET</span><span class="sxs-lookup"><span data-stu-id="b90b1-237">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="b90b1-238">Konwertowanie na typ macierzysty ujścia typ architektury .NET</span><span class="sxs-lookup"><span data-stu-id="b90b1-238">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="b90b1-239">Podczas przenoszenia danych z programu SAP BW, następujące mapowania są używane z programu SAP BW typów do typów .NET.</span><span class="sxs-lookup"><span data-stu-id="b90b1-239">When moving data from SAP BW, the following mappings are used from SAP BW types to .NET types.</span></span>

<span data-ttu-id="b90b1-240">Typ danych w słowniku ABAP</span><span class="sxs-lookup"><span data-stu-id="b90b1-240">Data type in the ABAP Dictionary</span></span> | <span data-ttu-id="b90b1-241">Typ danych .net</span><span class="sxs-lookup"><span data-stu-id="b90b1-241">.Net Data Type</span></span>
-------------------------------- | --------------
<span data-ttu-id="b90b1-242">ACCP</span><span class="sxs-lookup"><span data-stu-id="b90b1-242">ACCP</span></span> |  <span data-ttu-id="b90b1-243">int</span><span class="sxs-lookup"><span data-stu-id="b90b1-243">Int</span></span>
<span data-ttu-id="b90b1-244">CHAR</span><span class="sxs-lookup"><span data-stu-id="b90b1-244">CHAR</span></span> | <span data-ttu-id="b90b1-245">Ciąg</span><span class="sxs-lookup"><span data-stu-id="b90b1-245">String</span></span>
<span data-ttu-id="b90b1-246">CLNT</span><span class="sxs-lookup"><span data-stu-id="b90b1-246">CLNT</span></span> | <span data-ttu-id="b90b1-247">Ciąg</span><span class="sxs-lookup"><span data-stu-id="b90b1-247">String</span></span>
<span data-ttu-id="b90b1-248">BI</span><span class="sxs-lookup"><span data-stu-id="b90b1-248">CURR</span></span> | <span data-ttu-id="b90b1-249">Decimal</span><span class="sxs-lookup"><span data-stu-id="b90b1-249">Decimal</span></span>
<span data-ttu-id="b90b1-250">CUKY</span><span class="sxs-lookup"><span data-stu-id="b90b1-250">CUKY</span></span> | <span data-ttu-id="b90b1-251">Ciąg</span><span class="sxs-lookup"><span data-stu-id="b90b1-251">String</span></span>
<span data-ttu-id="b90b1-252">DEC</span><span class="sxs-lookup"><span data-stu-id="b90b1-252">DEC</span></span> | <span data-ttu-id="b90b1-253">Decimal</span><span class="sxs-lookup"><span data-stu-id="b90b1-253">Decimal</span></span>
<span data-ttu-id="b90b1-254">FLTP</span><span class="sxs-lookup"><span data-stu-id="b90b1-254">FLTP</span></span> | <span data-ttu-id="b90b1-255">O podwójnej precyzji</span><span class="sxs-lookup"><span data-stu-id="b90b1-255">Double</span></span>
<span data-ttu-id="b90b1-256">INT1</span><span class="sxs-lookup"><span data-stu-id="b90b1-256">INT1</span></span> | <span data-ttu-id="b90b1-257">Bajtów</span><span class="sxs-lookup"><span data-stu-id="b90b1-257">Byte</span></span>
<span data-ttu-id="b90b1-258">INT2</span><span class="sxs-lookup"><span data-stu-id="b90b1-258">INT2</span></span> | <span data-ttu-id="b90b1-259">Int16</span><span class="sxs-lookup"><span data-stu-id="b90b1-259">Int16</span></span>
<span data-ttu-id="b90b1-260">INT4</span><span class="sxs-lookup"><span data-stu-id="b90b1-260">INT4</span></span> | <span data-ttu-id="b90b1-261">int</span><span class="sxs-lookup"><span data-stu-id="b90b1-261">Int</span></span>
<span data-ttu-id="b90b1-262">JĘZYK</span><span class="sxs-lookup"><span data-stu-id="b90b1-262">LANG</span></span> | <span data-ttu-id="b90b1-263">Ciąg</span><span class="sxs-lookup"><span data-stu-id="b90b1-263">String</span></span>
<span data-ttu-id="b90b1-264">LCHR</span><span class="sxs-lookup"><span data-stu-id="b90b1-264">LCHR</span></span> | <span data-ttu-id="b90b1-265">Ciąg</span><span class="sxs-lookup"><span data-stu-id="b90b1-265">String</span></span>
<span data-ttu-id="b90b1-266">LRAW</span><span class="sxs-lookup"><span data-stu-id="b90b1-266">LRAW</span></span> | <span data-ttu-id="b90b1-267">Byte]</span><span class="sxs-lookup"><span data-stu-id="b90b1-267">Byte[]</span></span>
<span data-ttu-id="b90b1-268">PREC</span><span class="sxs-lookup"><span data-stu-id="b90b1-268">PREC</span></span> | <span data-ttu-id="b90b1-269">Int16</span><span class="sxs-lookup"><span data-stu-id="b90b1-269">Int16</span></span>
<span data-ttu-id="b90b1-270">QUAN</span><span class="sxs-lookup"><span data-stu-id="b90b1-270">QUAN</span></span> | <span data-ttu-id="b90b1-271">Decimal</span><span class="sxs-lookup"><span data-stu-id="b90b1-271">Decimal</span></span>
<span data-ttu-id="b90b1-272">NIEPRZETWORZONE</span><span class="sxs-lookup"><span data-stu-id="b90b1-272">RAW</span></span> | <span data-ttu-id="b90b1-273">Byte]</span><span class="sxs-lookup"><span data-stu-id="b90b1-273">Byte[]</span></span>
<span data-ttu-id="b90b1-274">RAWSTRING</span><span class="sxs-lookup"><span data-stu-id="b90b1-274">RAWSTRING</span></span> | <span data-ttu-id="b90b1-275">Byte]</span><span class="sxs-lookup"><span data-stu-id="b90b1-275">Byte[]</span></span>
<span data-ttu-id="b90b1-276">CIĄG</span><span class="sxs-lookup"><span data-stu-id="b90b1-276">STRING</span></span> | <span data-ttu-id="b90b1-277">Ciąg</span><span class="sxs-lookup"><span data-stu-id="b90b1-277">String</span></span>
<span data-ttu-id="b90b1-278">JEDNOSTKI</span><span class="sxs-lookup"><span data-stu-id="b90b1-278">UNIT</span></span> | <span data-ttu-id="b90b1-279">Ciąg</span><span class="sxs-lookup"><span data-stu-id="b90b1-279">String</span></span>
<span data-ttu-id="b90b1-280">DATS</span><span class="sxs-lookup"><span data-stu-id="b90b1-280">DATS</span></span> | <span data-ttu-id="b90b1-281">Ciąg</span><span class="sxs-lookup"><span data-stu-id="b90b1-281">String</span></span>
<span data-ttu-id="b90b1-282">NUMC</span><span class="sxs-lookup"><span data-stu-id="b90b1-282">NUMC</span></span> | <span data-ttu-id="b90b1-283">Ciąg</span><span class="sxs-lookup"><span data-stu-id="b90b1-283">String</span></span>
<span data-ttu-id="b90b1-284">TIMS</span><span class="sxs-lookup"><span data-stu-id="b90b1-284">TIMS</span></span> | <span data-ttu-id="b90b1-285">Ciąg</span><span class="sxs-lookup"><span data-stu-id="b90b1-285">String</span></span>

> [!NOTE]
> <span data-ttu-id="b90b1-286">Aby mapować kolumn z zestawu źródła danych do kolumn z obiektu sink zestawu danych, zobacz [mapowania kolumnach dataset w fabryce danych Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="b90b1-286">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>


## <a name="map-source-to-sink-columns"></a><span data-ttu-id="b90b1-287">Obiekt sink kolumn mapy źródła</span><span class="sxs-lookup"><span data-stu-id="b90b1-287">Map source to sink columns</span></span>
<span data-ttu-id="b90b1-288">Aby uzyskać informacje dotyczące mapowania kolumn w zestawie źródła danych do kolumn w zestawie danych zbiornika, zobacz [mapowania kolumnach dataset w fabryce danych Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="b90b1-288">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="b90b1-289">Odczyt powtarzalny ze źródłami relacyjnymi</span><span class="sxs-lookup"><span data-stu-id="b90b1-289">Repeatable read from relational sources</span></span>
<span data-ttu-id="b90b1-290">Podczas kopiowania danych z danych relacyjnych przechowuje, należy pamiętać, aby uniknąć niezamierzone wyniki powtarzalności.</span><span class="sxs-lookup"><span data-stu-id="b90b1-290">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="b90b1-291">Fabryka danych Azure możesz ponownie ręcznie wycinek.</span><span class="sxs-lookup"><span data-stu-id="b90b1-291">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="b90b1-292">Można również skonfigurować zasady ponawiania dla zestawu danych, aby wycinek jest uruchamiany ponownie, gdy wystąpi błąd.</span><span class="sxs-lookup"><span data-stu-id="b90b1-292">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="b90b1-293">Podczas wycinek zostanie uruchomiona ponownie w obu przypadkach, należy się upewnić, że te same dane jest do odczytu niezależnie od tego, ile razy wycinek jest uruchamiany.</span><span class="sxs-lookup"><span data-stu-id="b90b1-293">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="b90b1-294">Zobacz [Repeatable odczytywać relacyjne źródła](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span><span class="sxs-lookup"><span data-stu-id="b90b1-294">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="b90b1-295">Wydajność i dostrajania</span><span class="sxs-lookup"><span data-stu-id="b90b1-295">Performance and Tuning</span></span>
<span data-ttu-id="b90b1-296">Zobacz [wydajności działania kopiowania & dostrajanie przewodnik](data-factory-copy-activity-performance.md) Aby dowiedzieć się więcej o kluczowych czynników tego wydajność wpływ przenoszenia danych (działanie kopiowania) w usłudze fabryka danych Azure i zoptymalizować ją na różne sposoby.</span><span class="sxs-lookup"><span data-stu-id="b90b1-296">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
