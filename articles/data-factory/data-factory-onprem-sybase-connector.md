---
title: "Przenoszenia danych z programu Sybase przy użyciu fabryki danych Azure | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat sposobu przenoszenia danych z bazy danych programu Sybase przy użyciu fabryki danych Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: b379ee10-0ff5-4974-8c87-c95f82f1c5c6
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jingwang
ms.openlocfilehash: 617e604b220b8bc1c452e67da83f733448e16c0b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="move-data-from-sybase-using-azure-data-factory"></a><span data-ttu-id="daa6f-103">Przenoszenia danych z programu Sybase przy użyciu fabryki danych Azure</span><span class="sxs-lookup"><span data-stu-id="daa6f-103">Move data from Sybase using Azure Data Factory</span></span>
<span data-ttu-id="daa6f-104">W tym artykule opisano sposób używania działania kopiowania w fabryce danych Azure do przenoszenia danych z lokalną bazą danych programu Sybase.</span><span class="sxs-lookup"><span data-stu-id="daa6f-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises Sybase database.</span></span> <span data-ttu-id="daa6f-105">Opiera się na [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, który przedstawia ogólny przegląd przenoszenia danych z działania kopiowania.</span><span class="sxs-lookup"><span data-stu-id="daa6f-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="daa6f-106">Można skopiować danych z magazynu danych programu Sybase lokalnymi żadnych obsługiwanych ujścia magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="daa6f-106">You can copy data from an on-premises Sybase data store to any supported sink data store.</span></span> <span data-ttu-id="daa6f-107">Lista magazynów danych obsługiwane jako wychwytywanie przez działanie kopiowania, zobacz [obsługiwane magazyny danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabeli.</span><span class="sxs-lookup"><span data-stu-id="daa6f-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="daa6f-108">Fabryka danych aktualnie obsługuje tylko dane przenoszenie, z magazynu danych programu Sybase do innych magazynów danych, ale nie do przenoszenia danych z innych magazynów danych w magazynie danych programu Sybase.</span><span class="sxs-lookup"><span data-stu-id="daa6f-108">Data factory currently supports only moving data from a Sybase data store to other data stores, but not for moving data from other data stores to a Sybase data store.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="daa6f-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="daa6f-109">Prerequisites</span></span>
<span data-ttu-id="daa6f-110">Usługi fabryka danych obsługuje połączenia ze źródłami Sybase lokalnymi przy użyciu bramy zarządzania danymi.</span><span class="sxs-lookup"><span data-stu-id="daa6f-110">Data Factory service supports connecting to on-premises Sybase sources using the Data Management Gateway.</span></span> <span data-ttu-id="daa6f-111">Zobacz [przenoszenie danych między lokalizacji lokalnej i w chmurze](data-factory-move-data-between-onprem-and-cloud.md) artykułu, aby dowiedzieć się więcej na temat bramy zarządzania danymi i instrukcje krok po kroku dotyczące konfigurowania bramy.</span><span class="sxs-lookup"><span data-stu-id="daa6f-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span></span>

<span data-ttu-id="daa6f-112">Wymagana jest brama, nawet wtedy, gdy baza danych programu Sybase znajduje się w maszynie Wirtualnej platformy Azure IaaS.</span><span class="sxs-lookup"><span data-stu-id="daa6f-112">Gateway is required even if the Sybase database is hosted in an Azure IaaS VM.</span></span> <span data-ttu-id="daa6f-113">Można zainstalować bramę na tej samej maszyny Wirtualnej IaaS do przechowywania danych lub w innej maszyny Wirtualnej, tak długo, jak bramy można połączyć z bazą danych.</span><span class="sxs-lookup"><span data-stu-id="daa6f-113">You can install the gateway on the same IaaS VM as the data store or on a different VM as long as the gateway can connect to the database.</span></span>

> [!NOTE]
> <span data-ttu-id="daa6f-114">Zobacz [rozwiązywania problemów bramy](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) porady dotyczące rozwiązywania problemów z bramy/połączenia problemy związane z.</span><span class="sxs-lookup"><span data-stu-id="daa6f-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="daa6f-115">Obsługiwane wersje i instalacji</span><span class="sxs-lookup"><span data-stu-id="daa6f-115">Supported versions and installation</span></span>
<span data-ttu-id="daa6f-116">Dla bramy zarządzania danymi do łączenia z bazą danych programu Sybase, musisz zainstalować [dostawcy danych programu Sybase iAnywhere.Data.SQLAnywhere](http://go.microsoft.com/fwlink/?linkid=324846) 16 lub nowszej na tym samym systemie co brama zarządzania danymi.</span><span class="sxs-lookup"><span data-stu-id="daa6f-116">For Data Management Gateway to connect to the Sybase Database, you need to install the [data provider for Sybase iAnywhere.Data.SQLAnywhere](http://go.microsoft.com/fwlink/?linkid=324846) 16 or above on the same system as the Data Management Gateway.</span></span> <span data-ttu-id="daa6f-117">Sybase wersji 16 i nowszej jest obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="daa6f-117">Sybase version 16 and above is supported.</span></span>

## <a name="getting-started"></a><span data-ttu-id="daa6f-118">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="daa6f-118">Getting started</span></span>
<span data-ttu-id="daa6f-119">Można utworzyć potok z działania kopiowania, który przenosi dane z magazynu lokalnego Cassandra danych przy użyciu różnych narzędzi/interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="daa6f-119">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="daa6f-120">Najprostszym sposobem, aby utworzyć potok jest użycie **kreatora kopiowania**.</span><span class="sxs-lookup"><span data-stu-id="daa6f-120">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="daa6f-121">Zobacz [samouczek: tworzenie potoku za pomocą Kreatora kopiowania](data-factory-copy-data-wizard-tutorial.md) szybkie przewodnik dotyczący tworzenia potoku za pomocą Kreatora kopiowania danych.</span><span class="sxs-lookup"><span data-stu-id="daa6f-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span> 
- <span data-ttu-id="daa6f-122">Umożliwia także następujące narzędzia do tworzenia potoku: **portalu Azure**, **programu Visual Studio**, **programu Azure PowerShell**, **szablonu usługi Azure Resource Manager**, **interfejs API .NET**, i **interfejsu API REST**.</span><span class="sxs-lookup"><span data-stu-id="daa6f-122">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="daa6f-123">Zobacz [samouczek działania kopiowania](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) instrukcje krok po kroku utworzyć potok z działaniem kopiowania.</span><span class="sxs-lookup"><span data-stu-id="daa6f-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="daa6f-124">Czy można użyć narzędzia i interfejsy API, należy wykonać następujące kroki, aby utworzyć potok, który przenosi dane z magazynu danych źródła do ujścia magazynu danych:</span><span class="sxs-lookup"><span data-stu-id="daa6f-124">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="daa6f-125">Utwórz **połączone usługi** Aby połączyć dane wejściowe i wyjściowe są przechowywane w fabryce danych.</span><span class="sxs-lookup"><span data-stu-id="daa6f-125">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="daa6f-126">Utwórz **zestawów danych** do reprezentowania danych wejściowych i wyjściowych operacji kopiowania.</span><span class="sxs-lookup"><span data-stu-id="daa6f-126">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="daa6f-127">Utwórz **potoku** aktywnością kopiowania zestawu danych jako dane wejściowe i zestawu danych jako dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="daa6f-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="daa6f-128">Korzystając z kreatora, definicje JSON do tych jednostek fabryki danych (połączone usługi, zestawy danych i potoki) są tworzone automatycznie dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="daa6f-128">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="daa6f-129">Korzystając z narzędzi/API (z wyjątkiem interfejs API .NET), należy zdefiniować tych jednostek fabryki danych w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="daa6f-129">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="daa6f-130">Dla przykładu z definicji JSON dla jednostek fabryki danych, które służą do kopiowania danych z magazynu danych programu Sybase lokalnych, zobacz [przykład JSON: kopiowanie danych z programu Sybase do obiektów Blob platformy Azure](#json-example-copy-data-from-sybase-to-azure-blob) sekcji tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="daa6f-130">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises Sybase data store, see [JSON example: Copy data from Sybase to Azure Blob](#json-example-copy-data-from-sybase-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="daa6f-131">Poniższe sekcje zawierają szczegółowe informacje o właściwości JSON, które są używane do definiowania jednostek fabryki danych określonej w magazynie danych programu Sybase:</span><span class="sxs-lookup"><span data-stu-id="daa6f-131">The following sections provide details about JSON properties that are used to define Data Factory entities specific to a Sybase data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="daa6f-132">Połączona usługa właściwości</span><span class="sxs-lookup"><span data-stu-id="daa6f-132">Linked service properties</span></span>
<span data-ttu-id="daa6f-133">Poniższa tabela zawiera opis specyficzne dla usługi programu Sybase połączone elementy JSON.</span><span class="sxs-lookup"><span data-stu-id="daa6f-133">The following table provides description for JSON elements specific to Sybase linked service.</span></span>

| <span data-ttu-id="daa6f-134">Właściwość</span><span class="sxs-lookup"><span data-stu-id="daa6f-134">Property</span></span> | <span data-ttu-id="daa6f-135">Opis</span><span class="sxs-lookup"><span data-stu-id="daa6f-135">Description</span></span> | <span data-ttu-id="daa6f-136">Wymagane</span><span class="sxs-lookup"><span data-stu-id="daa6f-136">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="daa6f-137">type</span><span class="sxs-lookup"><span data-stu-id="daa6f-137">type</span></span> |<span data-ttu-id="daa6f-138">Właściwość type musi mieć ustawioną: **OnPremisesSybase**</span><span class="sxs-lookup"><span data-stu-id="daa6f-138">The type property must be set to: **OnPremisesSybase**</span></span> |<span data-ttu-id="daa6f-139">Tak</span><span class="sxs-lookup"><span data-stu-id="daa6f-139">Yes</span></span> |
| <span data-ttu-id="daa6f-140">serwer</span><span class="sxs-lookup"><span data-stu-id="daa6f-140">server</span></span> |<span data-ttu-id="daa6f-141">Nazwa serwera programu Sybase.</span><span class="sxs-lookup"><span data-stu-id="daa6f-141">Name of the Sybase server.</span></span> |<span data-ttu-id="daa6f-142">Tak</span><span class="sxs-lookup"><span data-stu-id="daa6f-142">Yes</span></span> |
| <span data-ttu-id="daa6f-143">Bazy danych</span><span class="sxs-lookup"><span data-stu-id="daa6f-143">database</span></span> |<span data-ttu-id="daa6f-144">Nazwa bazy danych programu Sybase.</span><span class="sxs-lookup"><span data-stu-id="daa6f-144">Name of the Sybase database.</span></span> |<span data-ttu-id="daa6f-145">Tak</span><span class="sxs-lookup"><span data-stu-id="daa6f-145">Yes</span></span> |
| <span data-ttu-id="daa6f-146">Schemat</span><span class="sxs-lookup"><span data-stu-id="daa6f-146">schema</span></span> |<span data-ttu-id="daa6f-147">Nazwa schematu w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="daa6f-147">Name of the schema in the database.</span></span> |<span data-ttu-id="daa6f-148">Nie</span><span class="sxs-lookup"><span data-stu-id="daa6f-148">No</span></span> |
| <span data-ttu-id="daa6f-149">Typ authenticationType</span><span class="sxs-lookup"><span data-stu-id="daa6f-149">authenticationType</span></span> |<span data-ttu-id="daa6f-150">Typ uwierzytelniania używany do łączenia z bazą danych programu Sybase.</span><span class="sxs-lookup"><span data-stu-id="daa6f-150">Type of authentication used to connect to the Sybase database.</span></span> <span data-ttu-id="daa6f-151">Możliwe wartości to: anonimowe, podstawowe i systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="daa6f-151">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="daa6f-152">Tak</span><span class="sxs-lookup"><span data-stu-id="daa6f-152">Yes</span></span> |
| <span data-ttu-id="daa6f-153">nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="daa6f-153">username</span></span> |<span data-ttu-id="daa6f-154">Określ nazwę użytkownika, jeśli korzystasz z uwierzytelniania podstawowego lub systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="daa6f-154">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="daa6f-155">Nie</span><span class="sxs-lookup"><span data-stu-id="daa6f-155">No</span></span> |
| <span data-ttu-id="daa6f-156">hasło</span><span class="sxs-lookup"><span data-stu-id="daa6f-156">password</span></span> |<span data-ttu-id="daa6f-157">Określ hasło dla konta użytkownika, określone nazwy użytkownika.</span><span class="sxs-lookup"><span data-stu-id="daa6f-157">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="daa6f-158">Nie</span><span class="sxs-lookup"><span data-stu-id="daa6f-158">No</span></span> |
| <span data-ttu-id="daa6f-159">gatewayName</span><span class="sxs-lookup"><span data-stu-id="daa6f-159">gatewayName</span></span> |<span data-ttu-id="daa6f-160">Nazwa bramy, która powinna być używana przez usługi fabryka danych nawiązać połączenia z lokalną bazą danych programu Sybase.</span><span class="sxs-lookup"><span data-stu-id="daa6f-160">Name of the gateway that the Data Factory service should use to connect to the on-premises Sybase database.</span></span> |<span data-ttu-id="daa6f-161">Tak</span><span class="sxs-lookup"><span data-stu-id="daa6f-161">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="daa6f-162">Właściwości zestawu danych</span><span class="sxs-lookup"><span data-stu-id="daa6f-162">Dataset properties</span></span>
<span data-ttu-id="daa6f-163">Aby uzyskać pełną listę sekcje & właściwości dostępne do definiowania zestawów danych, zobacz [Tworzenie zbiorów danych](data-factory-create-datasets.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="daa6f-163">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="daa6f-164">Sekcje zawierają informacje, takie jak struktury, dostępności i zasad zestawu danych JSON są podobne dla wszystkich typów obiektów dataset (Azure SQL, obiektów blob platformy Azure, Azure tabeli itp.).</span><span class="sxs-lookup"><span data-stu-id="daa6f-164">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="daa6f-165">Sekcja typeProperties jest różne dla każdego typu zestawu danych i zawiera informacje o lokalizacji danych w magazynie danych.</span><span class="sxs-lookup"><span data-stu-id="daa6f-165">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="daa6f-166">**TypeProperties** sekcja dla zestawu danych typu **RelationalTable** (w tym zestawie danych programu Sybase) ma następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="daa6f-166">The **typeProperties** section for dataset of type **RelationalTable** (which includes Sybase dataset) has the following properties:</span></span>

| <span data-ttu-id="daa6f-167">Właściwość</span><span class="sxs-lookup"><span data-stu-id="daa6f-167">Property</span></span> | <span data-ttu-id="daa6f-168">Opis</span><span class="sxs-lookup"><span data-stu-id="daa6f-168">Description</span></span> | <span data-ttu-id="daa6f-169">Wymagane</span><span class="sxs-lookup"><span data-stu-id="daa6f-169">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="daa6f-170">tableName</span><span class="sxs-lookup"><span data-stu-id="daa6f-170">tableName</span></span> |<span data-ttu-id="daa6f-171">Nazwa tabeli w wystąpieniu bazy danych programu Sybase, odnoszący się do połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="daa6f-171">Name of the table in the Sybase Database instance that linked service refers to.</span></span> |<span data-ttu-id="daa6f-172">Nie (Jeśli **zapytania** z **RelationalSource** jest określona)</span><span class="sxs-lookup"><span data-stu-id="daa6f-172">No (if **query** of **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="daa6f-173">Właściwości działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="daa6f-173">Copy activity properties</span></span>
<span data-ttu-id="daa6f-174">Pełną listę sekcje & właściwości dostępne do definiowania działań, zobacz [tworzenie potoków](data-factory-create-pipelines.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="daa6f-174">For a full list of sections & properties available for defining activities, see [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="daa6f-175">Właściwości, takie jak nazwa, opis, dane wejściowe i wyjściowe tabel i zasady są dostępne dla wszystkich typów działań.</span><span class="sxs-lookup"><span data-stu-id="daa6f-175">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="daa6f-176">Właściwości, które są dostępne w sekcji typeProperties działania różnić się z każdym typem działania.</span><span class="sxs-lookup"><span data-stu-id="daa6f-176">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="daa6f-177">Dla działania kopiowania różnią się w zależności od typów źródeł i sink.</span><span class="sxs-lookup"><span data-stu-id="daa6f-177">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="daa6f-178">Jeśli źródło jest typu **RelationalSource** (która obejmuje Sybase), są dostępne w następujących właściwości **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="daa6f-178">When the source is of type **RelationalSource** (which includes Sybase), the following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="daa6f-179">Właściwość</span><span class="sxs-lookup"><span data-stu-id="daa6f-179">Property</span></span> | <span data-ttu-id="daa6f-180">Opis</span><span class="sxs-lookup"><span data-stu-id="daa6f-180">Description</span></span> | <span data-ttu-id="daa6f-181">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="daa6f-181">Allowed values</span></span> | <span data-ttu-id="daa6f-182">Wymagane</span><span class="sxs-lookup"><span data-stu-id="daa6f-182">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="daa6f-183">query</span><span class="sxs-lookup"><span data-stu-id="daa6f-183">query</span></span> |<span data-ttu-id="daa6f-184">Użyj niestandardowych zapytania można odczytać danych.</span><span class="sxs-lookup"><span data-stu-id="daa6f-184">Use the custom query to read data.</span></span> |<span data-ttu-id="daa6f-185">Ciąg zapytania SQL.</span><span class="sxs-lookup"><span data-stu-id="daa6f-185">SQL query string.</span></span> <span data-ttu-id="daa6f-186">Na przykład: Wybierz * z MyTable.</span><span class="sxs-lookup"><span data-stu-id="daa6f-186">For example: select * from MyTable.</span></span> |<span data-ttu-id="daa6f-187">Nie (Jeśli **tableName** z **dataset** jest określona)</span><span class="sxs-lookup"><span data-stu-id="daa6f-187">No (if **tableName** of **dataset** is specified)</span></span> |


## <a name="json-example-copy-data-from-sybase-to-azure-blob"></a><span data-ttu-id="daa6f-188">Przykład JSON: kopiowanie danych z programu Sybase do obiektów Blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="daa6f-188">JSON example: Copy data from Sybase to Azure Blob</span></span>
<span data-ttu-id="daa6f-189">W poniższym przykładzie przedstawiono przykładowe definicje JSON, które można użyć, aby utworzyć potok przy użyciu [portalu Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) lub [programu Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) lub [programu Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="daa6f-189">The following example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="daa6f-190">Przedstawiają sposób kopiowania danych z bazy danych programu Sybase do magazynu obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="daa6f-190">They show how to copy data from Sybase database to Azure Blob Storage.</span></span> <span data-ttu-id="daa6f-191">Jednak można skopiować danych do dowolnego wychwytywanie podane [tutaj](data-factory-data-movement-activities.md#supported-data-stores-and-formats) za pomocą działania kopiowania w fabryce danych Azure.</span><span class="sxs-lookup"><span data-stu-id="daa6f-191">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>   

<span data-ttu-id="daa6f-192">Przykład zawiera następujące obiekty fabryki danych:</span><span class="sxs-lookup"><span data-stu-id="daa6f-192">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="daa6f-193">Połączonej usługi typu [OnPremisesSybase](data-factory-onprem-sybase-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="daa6f-193">A linked service of type [OnPremisesSybase](data-factory-onprem-sybase-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="daa6f-194">Liked usługi typu [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="daa6f-194">A liked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="daa6f-195">Dane wejściowe [dataset](data-factory-create-datasets.md) typu [RelationalTable](data-factory-onprem-sybase-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="daa6f-195">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](data-factory-onprem-sybase-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="daa6f-196">Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="daa6f-196">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="daa6f-197">[Potoku](data-factory-create-pipelines.md) z działaniem kopii, która używa [RelationalSource](data-factory-onprem-sybase-connector.md#copy-activity-properties) i [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="daa6f-197">The [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](data-factory-onprem-sybase-connector.md#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="daa6f-198">Przykład kopiuje dane z wyniku kwerendy w bazie danych programu Sybase do obiektu blob co godzinę.</span><span class="sxs-lookup"><span data-stu-id="daa6f-198">The sample copies data from a query result in Sybase database to a blob every hour.</span></span> <span data-ttu-id="daa6f-199">Właściwości JSON używane w te przykłady są opisane w sekcjach poniżej próbek.</span><span class="sxs-lookup"><span data-stu-id="daa6f-199">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="daa6f-200">Pierwszym krokiem konfiguracji bramy zarządzania danymi.</span><span class="sxs-lookup"><span data-stu-id="daa6f-200">As a first step, setup the data management gateway.</span></span> <span data-ttu-id="daa6f-201">Instrukcje znajdują się w [przenoszenie danych między lokalizacji lokalnej i w chmurze](data-factory-move-data-between-onprem-and-cloud.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="daa6f-201">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="daa6f-202">**Sybase połączonej usługi:**</span><span class="sxs-lookup"><span data-stu-id="daa6f-202">**Sybase linked service:**</span></span>

```JSON
{
    "name": "OnPremSybaseLinkedService",
    "properties": {
        "type": "OnPremisesSybase",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
            "schema": "<schema>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```

<span data-ttu-id="daa6f-203">**Magazyn obiektów Blob Azure połączonej usługi:**</span><span class="sxs-lookup"><span data-stu-id="daa6f-203">**Azure Blob storage linked service:**</span></span>

```JSON
{
    "name": "AzureStorageLinkedService",
    "properties": {
        "type": "AzureStorageLinkedService",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<AccountName>;AccountKey=<AccountKey>"
        }
    }
}
```

<span data-ttu-id="daa6f-204">**Wejściowy zestaw danych programu Sybase:**</span><span class="sxs-lookup"><span data-stu-id="daa6f-204">**Sybase input dataset:**</span></span>

<span data-ttu-id="daa6f-205">Przykład przyjęto założenie, utworzysz tabelę "MyTable" Sybase i zawiera kolumnę o nazwie "timestamp" dla czasu serii danych.</span><span class="sxs-lookup"><span data-stu-id="daa6f-205">The sample assumes you have created a table “MyTable” in Sybase and it contains a column called “timestamp” for time series data.</span></span>

<span data-ttu-id="daa6f-206">Ustawienie "external": true usługi fabryka danych informuje, że ten zestaw danych jest zewnętrzne do fabryki danych i nie jest generowany przez działanie w fabryce danych.</span><span class="sxs-lookup"><span data-stu-id="daa6f-206">Setting “external”: true informs the Data Factory service that this dataset is external to the data factory and is not produced by an activity in the data factory.</span></span> <span data-ttu-id="daa6f-207">Zwróć uwagę, że **typu** połączonej usługi jest ustawiony na wartość: **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="daa6f-207">Notice that the **type** of the linked service is set to: **RelationalTable**.</span></span>

```JSON
{
    "name": "SybaseDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremSybaseLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="daa6f-208">**Azure Blob wyjściowy zestaw danych:**</span><span class="sxs-lookup"><span data-stu-id="daa6f-208">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="daa6f-209">Dane są zapisywane do nowego obiektu blob co godzinę (częstotliwość: godziny, interwał: 1).</span><span class="sxs-lookup"><span data-stu-id="daa6f-209">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="daa6f-210">Ścieżka folderu dla obiekt blob jest dynamicznie obliczane na podstawie czasu rozpoczęcia wycinek, który jest przetwarzana.</span><span class="sxs-lookup"><span data-stu-id="daa6f-210">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="daa6f-211">Ścieżka folderu używa rok, miesiąc, dzień i godziny części czas rozpoczęcia.</span><span class="sxs-lookup"><span data-stu-id="daa6f-211">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```JSON
{
    "name": "AzureBlobSybaseDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/sybase/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

<span data-ttu-id="daa6f-212">**W potoku z działania kopiowania:**</span><span class="sxs-lookup"><span data-stu-id="daa6f-212">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="daa6f-213">Potok zawiera działanie kopiowania, który jest skonfigurowany do używania wejściowe i wyjściowe zestawy danych i jest zaplanowane co godzinę.</span><span class="sxs-lookup"><span data-stu-id="daa6f-213">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run hourly.</span></span> <span data-ttu-id="daa6f-214">W definicji JSON potoku **źródła** ustawiono typ **RelationalSource** i **zbiornika** ustawiono typ **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="daa6f-214">In the pipeline JSON definition, the **source** type is set to **RelationalSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="daa6f-215">Określony dla zapytania SQL **zapytania** właściwości wybiera dane z administrator bazy danych. Tabela zamówień w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="daa6f-215">The SQL query specified for the **query** property selects the data from the DBA.Orders table in the database.</span></span>

```JSON
{
    "name": "CopySybaseToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "select * from DBA.Orders"
                    },
                    "sink": {
                        "type": "BlobSink"
                    }
                },
                "inputs": [
                    {
                        "name": "SybaseDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobSybaseDataSet"
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
                "name": "SybaseToBlob"
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```

## <a name="type-mapping-for-sybase"></a><span data-ttu-id="daa6f-216">Mapowanie typu dla programu Sybase</span><span class="sxs-lookup"><span data-stu-id="daa6f-216">Type mapping for Sybase</span></span>
<span data-ttu-id="daa6f-217">Jak wspomniano w [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, wykonuje działanie kopiowania automatyczne konwersje z typów źródła do zbiornika typów o następujące podejście krok 2:</span><span class="sxs-lookup"><span data-stu-id="daa6f-217">As mentioned in the [Data Movement Activities](data-factory-data-movement-activities.md) article, the Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="daa6f-218">Konwertowanie typów natywnych źródła na typ architektury .NET</span><span class="sxs-lookup"><span data-stu-id="daa6f-218">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="daa6f-219">Konwertowanie na typ macierzysty ujścia typ architektury .NET</span><span class="sxs-lookup"><span data-stu-id="daa6f-219">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="daa6f-220">Sybase obsługuje T-SQL i typy T-SQL.</span><span class="sxs-lookup"><span data-stu-id="daa6f-220">Sybase supports T-SQL and T-SQL types.</span></span> <span data-ttu-id="daa6f-221">Dla tabeli mapowania typów sql do typów .NET, zobacz [Łącznik usług SQL Azure](data-factory-azure-sql-connector.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="daa6f-221">For a mapping table from sql types to .NET type, see [Azure SQL Connector](data-factory-azure-sql-connector.md) article.</span></span>

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="daa6f-222">Obiekt sink kolumn mapy źródła</span><span class="sxs-lookup"><span data-stu-id="daa6f-222">Map source to sink columns</span></span>
<span data-ttu-id="daa6f-223">Aby uzyskać informacje dotyczące mapowania kolumn w zestawie źródła danych do kolumn w zestawie danych zbiornika, zobacz [mapowania kolumnach dataset w fabryce danych Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="daa6f-223">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="daa6f-224">Odczyt powtarzalny ze źródłami relacyjnymi</span><span class="sxs-lookup"><span data-stu-id="daa6f-224">Repeatable read from relational sources</span></span>
<span data-ttu-id="daa6f-225">Podczas kopiowania danych z danych relacyjnych przechowuje, należy pamiętać, aby uniknąć niezamierzone wyniki powtarzalności.</span><span class="sxs-lookup"><span data-stu-id="daa6f-225">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="daa6f-226">Fabryka danych Azure możesz ponownie ręcznie wycinek.</span><span class="sxs-lookup"><span data-stu-id="daa6f-226">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="daa6f-227">Można również skonfigurować zasady ponawiania dla zestawu danych, aby wycinek jest uruchamiany ponownie, gdy wystąpi błąd.</span><span class="sxs-lookup"><span data-stu-id="daa6f-227">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="daa6f-228">Podczas wycinek zostanie uruchomiona ponownie w obu przypadkach, należy się upewnić, że te same dane jest do odczytu niezależnie od tego, ile razy wycinek jest uruchamiany.</span><span class="sxs-lookup"><span data-stu-id="daa6f-228">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="daa6f-229">Zobacz [Repeatable odczytywać źródłami relacyjnymi](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="daa6f-229">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="daa6f-230">Wydajność i dostrajania</span><span class="sxs-lookup"><span data-stu-id="daa6f-230">Performance and Tuning</span></span>
<span data-ttu-id="daa6f-231">Zobacz [wydajności działania kopiowania & dostrajanie przewodnik](data-factory-copy-activity-performance.md) Aby dowiedzieć się więcej o kluczowych czynników tego wydajność wpływ przenoszenia danych (działanie kopiowania) w usłudze fabryka danych Azure i zoptymalizować ją na różne sposoby.</span><span class="sxs-lookup"><span data-stu-id="daa6f-231">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
