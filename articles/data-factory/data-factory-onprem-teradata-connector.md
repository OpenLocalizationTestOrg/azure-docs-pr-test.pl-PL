---
title: "Przenoszenia danych z programu Teradata przy użyciu fabryki danych Azure | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat programu Teradata Connector dla usługi fabryka danych, które umożliwia przenoszenie danych z bazy danych programu Teradata"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 98eb76d8-5f3d-4667-b76e-e59ed3eea3ae
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jingwang
ms.openlocfilehash: 01edb32cd9e20d4199feac5b98a73aa06b74fec2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="move-data-from-teradata-using-azure-data-factory"></a><span data-ttu-id="5d544-103">Przenoszenia danych z programu Teradata przy użyciu fabryki danych Azure</span><span class="sxs-lookup"><span data-stu-id="5d544-103">Move data from Teradata using Azure Data Factory</span></span>
<span data-ttu-id="5d544-104">W tym artykule opisano sposób używania działania kopiowania w fabryce danych Azure do przenoszenia danych z lokalną bazą danych programu Teradata.</span><span class="sxs-lookup"><span data-stu-id="5d544-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises Teradata database.</span></span> <span data-ttu-id="5d544-105">Opiera się na [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, który przedstawia ogólny przegląd przenoszenia danych z działania kopiowania.</span><span class="sxs-lookup"><span data-stu-id="5d544-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="5d544-106">Można skopiować danych z magazynu danych programu Teradata lokalnymi żadnych obsługiwanych ujścia magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="5d544-106">You can copy data from an on-premises Teradata data store to any supported sink data store.</span></span> <span data-ttu-id="5d544-107">Lista magazynów danych obsługiwane jako wychwytywanie przez działanie kopiowania, zobacz [obsługiwane magazyny danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabeli.</span><span class="sxs-lookup"><span data-stu-id="5d544-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="5d544-108">Fabryka danych aktualnie obsługuje tylko dane przenoszenie, z magazynu danych programu Teradata do innych magazynów danych, ale nie do przenoszenia danych z innych magazynów danych w magazynie danych programu Teradata.</span><span class="sxs-lookup"><span data-stu-id="5d544-108">Data factory currently supports only moving data from a Teradata data store to other data stores, but not for moving data from other data stores to a Teradata data store.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="5d544-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="5d544-109">Prerequisites</span></span>
<span data-ttu-id="5d544-110">Fabryka danych obsługuje połączenia ze źródłami Teradata lokalnej za pośrednictwem bramy zarządzania danymi.</span><span class="sxs-lookup"><span data-stu-id="5d544-110">Data factory supports connecting to on-premises Teradata sources via the Data Management Gateway.</span></span> <span data-ttu-id="5d544-111">Zobacz [przenoszenie danych między lokalizacji lokalnej i w chmurze](data-factory-move-data-between-onprem-and-cloud.md) artykułu, aby dowiedzieć się więcej na temat bramy zarządzania danymi i instrukcje krok po kroku dotyczące konfigurowania bramy.</span><span class="sxs-lookup"><span data-stu-id="5d544-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span></span>

<span data-ttu-id="5d544-112">Wymagana jest brama, nawet jeśli Teradata znajduje się w maszynie Wirtualnej platformy Azure IaaS.</span><span class="sxs-lookup"><span data-stu-id="5d544-112">Gateway is required even if the Teradata is hosted in an Azure IaaS VM.</span></span> <span data-ttu-id="5d544-113">Można zainstalować bramę na tej samej maszyny Wirtualnej IaaS do przechowywania danych lub w innej maszyny Wirtualnej, tak długo, jak bramy można połączyć z bazą danych.</span><span class="sxs-lookup"><span data-stu-id="5d544-113">You can install the gateway on the same IaaS VM as the data store or on a different VM as long as the gateway can connect to the database.</span></span>

> [!NOTE]
> <span data-ttu-id="5d544-114">Zobacz [rozwiązywania problemów bramy](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) porady dotyczące rozwiązywania problemów z bramy/połączenia problemy związane z.</span><span class="sxs-lookup"><span data-stu-id="5d544-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="5d544-115">Obsługiwane wersje i instalacji</span><span class="sxs-lookup"><span data-stu-id="5d544-115">Supported versions and installation</span></span>
<span data-ttu-id="5d544-116">Dla bramy zarządzania danymi do łączenia z bazą danych programu Teradata, musisz zainstalować [dostawcy danych .NET dla programu Teradata](http://go.microsoft.com/fwlink/?LinkId=278886) wersji 14 lub nowszej na tym samym systemie co brama zarządzania danymi.</span><span class="sxs-lookup"><span data-stu-id="5d544-116">For Data Management Gateway to connect to the Teradata Database, you need to install the [.NET Data Provider for Teradata](http://go.microsoft.com/fwlink/?LinkId=278886) version 14 or above on the same system as the Data Management Gateway.</span></span> <span data-ttu-id="5d544-117">Teradata wersji 12 i nowszej jest obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="5d544-117">Teradata version 12 and above is supported.</span></span>

## <a name="getting-started"></a><span data-ttu-id="5d544-118">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="5d544-118">Getting started</span></span>
<span data-ttu-id="5d544-119">Można utworzyć potok z działania kopiowania, który przenosi dane z magazynu lokalnego Cassandra danych przy użyciu różnych narzędzi/interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="5d544-119">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="5d544-120">Najprostszym sposobem, aby utworzyć potok jest użycie **kreatora kopiowania**.</span><span class="sxs-lookup"><span data-stu-id="5d544-120">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="5d544-121">Zobacz [samouczek: tworzenie potoku za pomocą Kreatora kopiowania](data-factory-copy-data-wizard-tutorial.md) szybkie przewodnik dotyczący tworzenia potoku za pomocą Kreatora kopiowania danych.</span><span class="sxs-lookup"><span data-stu-id="5d544-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span> 
- <span data-ttu-id="5d544-122">Umożliwia także następujące narzędzia do tworzenia potoku: **portalu Azure**, **programu Visual Studio**, **programu Azure PowerShell**, **szablonu usługi Azure Resource Manager**, **interfejs API .NET**, i **interfejsu API REST**.</span><span class="sxs-lookup"><span data-stu-id="5d544-122">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="5d544-123">Zobacz [samouczek działania kopiowania](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) instrukcje krok po kroku utworzyć potok z działaniem kopiowania.</span><span class="sxs-lookup"><span data-stu-id="5d544-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="5d544-124">Czy można użyć narzędzia i interfejsy API, należy wykonać następujące kroki, aby utworzyć potok, który przenosi dane z magazynu danych źródła do ujścia magazynu danych:</span><span class="sxs-lookup"><span data-stu-id="5d544-124">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="5d544-125">Utwórz **połączone usługi** Aby połączyć dane wejściowe i wyjściowe są przechowywane w fabryce danych.</span><span class="sxs-lookup"><span data-stu-id="5d544-125">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="5d544-126">Utwórz **zestawów danych** do reprezentowania danych wejściowych i wyjściowych operacji kopiowania.</span><span class="sxs-lookup"><span data-stu-id="5d544-126">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="5d544-127">Utwórz **potoku** aktywnością kopiowania zestawu danych jako dane wejściowe i zestawu danych jako dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="5d544-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="5d544-128">Korzystając z kreatora, definicje JSON do tych jednostek fabryki danych (połączone usługi, zestawy danych i potoki) są tworzone automatycznie dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="5d544-128">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="5d544-129">Korzystając z narzędzi/API (z wyjątkiem interfejs API .NET), należy zdefiniować tych jednostek fabryki danych w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="5d544-129">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="5d544-130">Przykładowy z definicji JSON dla jednostek fabryki danych, które są używane do skopiowania danych na lokalnym magazynem danych programu Teradata [przykład JSON: kopiowanie danych z programu Teradata do obiektów Blob platformy Azure](#json-example-copy-data-from-teradata-to-azure-blob) sekcji tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="5d544-130">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises Teradata data store, see [JSON example: Copy data from Teradata to Azure Blob](#json-example-copy-data-from-teradata-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="5d544-131">Poniższe sekcje zawierają szczegółowe informacje o właściwości JSON, które są używane do definiowania jednostek fabryki danych określonej w magazynie danych programu Teradata:</span><span class="sxs-lookup"><span data-stu-id="5d544-131">The following sections provide details about JSON properties that are used to define Data Factory entities specific to a Teradata data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="5d544-132">Połączona usługa właściwości</span><span class="sxs-lookup"><span data-stu-id="5d544-132">Linked service properties</span></span>
<span data-ttu-id="5d544-133">Poniższa tabela zawiera opis specyficzne dla usługi programu Teradata połączone elementy JSON.</span><span class="sxs-lookup"><span data-stu-id="5d544-133">The following table provides description for JSON elements specific to Teradata linked service.</span></span>

| <span data-ttu-id="5d544-134">Właściwość</span><span class="sxs-lookup"><span data-stu-id="5d544-134">Property</span></span> | <span data-ttu-id="5d544-135">Opis</span><span class="sxs-lookup"><span data-stu-id="5d544-135">Description</span></span> | <span data-ttu-id="5d544-136">Wymagane</span><span class="sxs-lookup"><span data-stu-id="5d544-136">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5d544-137">type</span><span class="sxs-lookup"><span data-stu-id="5d544-137">type</span></span> |<span data-ttu-id="5d544-138">Właściwość type musi mieć ustawioną: **OnPremisesTeradata**</span><span class="sxs-lookup"><span data-stu-id="5d544-138">The type property must be set to: **OnPremisesTeradata**</span></span> |<span data-ttu-id="5d544-139">Tak</span><span class="sxs-lookup"><span data-stu-id="5d544-139">Yes</span></span> |
| <span data-ttu-id="5d544-140">serwer</span><span class="sxs-lookup"><span data-stu-id="5d544-140">server</span></span> |<span data-ttu-id="5d544-141">Nazwa serwera programu Teradata.</span><span class="sxs-lookup"><span data-stu-id="5d544-141">Name of the Teradata server.</span></span> |<span data-ttu-id="5d544-142">Tak</span><span class="sxs-lookup"><span data-stu-id="5d544-142">Yes</span></span> |
| <span data-ttu-id="5d544-143">Typ authenticationType</span><span class="sxs-lookup"><span data-stu-id="5d544-143">authenticationType</span></span> |<span data-ttu-id="5d544-144">Typ uwierzytelniania używany do łączenia z bazą danych programu Teradata.</span><span class="sxs-lookup"><span data-stu-id="5d544-144">Type of authentication used to connect to the Teradata database.</span></span> <span data-ttu-id="5d544-145">Możliwe wartości to: anonimowe, podstawowe i systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="5d544-145">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="5d544-146">Tak</span><span class="sxs-lookup"><span data-stu-id="5d544-146">Yes</span></span> |
| <span data-ttu-id="5d544-147">nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="5d544-147">username</span></span> |<span data-ttu-id="5d544-148">Określ nazwę użytkownika, jeśli korzystasz z uwierzytelniania podstawowego lub systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="5d544-148">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="5d544-149">Nie</span><span class="sxs-lookup"><span data-stu-id="5d544-149">No</span></span> |
| <span data-ttu-id="5d544-150">hasło</span><span class="sxs-lookup"><span data-stu-id="5d544-150">password</span></span> |<span data-ttu-id="5d544-151">Określ hasło dla konta użytkownika, określone nazwy użytkownika.</span><span class="sxs-lookup"><span data-stu-id="5d544-151">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="5d544-152">Nie</span><span class="sxs-lookup"><span data-stu-id="5d544-152">No</span></span> |
| <span data-ttu-id="5d544-153">gatewayName</span><span class="sxs-lookup"><span data-stu-id="5d544-153">gatewayName</span></span> |<span data-ttu-id="5d544-154">Nazwa bramy, która powinna być używana przez usługi fabryka danych nawiązać połączenia z lokalną bazą danych programu Teradata.</span><span class="sxs-lookup"><span data-stu-id="5d544-154">Name of the gateway that the Data Factory service should use to connect to the on-premises Teradata database.</span></span> |<span data-ttu-id="5d544-155">Tak</span><span class="sxs-lookup"><span data-stu-id="5d544-155">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="5d544-156">Właściwości zestawu danych</span><span class="sxs-lookup"><span data-stu-id="5d544-156">Dataset properties</span></span>
<span data-ttu-id="5d544-157">Aby uzyskać pełną listę sekcje & właściwości dostępne do definiowania zestawów danych, zobacz [Tworzenie zbiorów danych](data-factory-create-datasets.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="5d544-157">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="5d544-158">Sekcje zawierają informacje, takie jak struktury, dostępności i zasad zestawu danych JSON są podobne dla wszystkich typów obiektów dataset (Azure SQL, obiektów blob platformy Azure, Azure tabeli itp.).</span><span class="sxs-lookup"><span data-stu-id="5d544-158">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="5d544-159">**TypeProperties** sekcja jest różne dla każdego typu zestawu danych i zawiera informacje o lokalizacji danych w magazynie danych.</span><span class="sxs-lookup"><span data-stu-id="5d544-159">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="5d544-160">Obecnie nie ma żadnych właściwości typu, obsługiwane dla zestawu danych programu Teradata.</span><span class="sxs-lookup"><span data-stu-id="5d544-160">Currently, there are no type properties supported for the Teradata dataset.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="5d544-161">Właściwości działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="5d544-161">Copy activity properties</span></span>
<span data-ttu-id="5d544-162">Pełną listę sekcje & właściwości dostępne do definiowania działań, zobacz [tworzenie potoków](data-factory-create-pipelines.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="5d544-162">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="5d544-163">Właściwości, takie jak nazwa, opis, dane wejściowe i wyjściowe tabel i zasady są dostępne dla wszystkich typów działań.</span><span class="sxs-lookup"><span data-stu-id="5d544-163">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="5d544-164">Właściwości, które są dostępne w sekcji typeProperties działania różnić się z każdym typem działania.</span><span class="sxs-lookup"><span data-stu-id="5d544-164">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="5d544-165">Dla działania kopiowania różnią się w zależności od typów źródeł i sink.</span><span class="sxs-lookup"><span data-stu-id="5d544-165">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="5d544-166">Jeśli źródło jest typu **RelationalSource** (która obejmuje Teradata), są dostępne w następujących właściwości **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="5d544-166">When the source is of type **RelationalSource** (which includes Teradata), the following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="5d544-167">Właściwość</span><span class="sxs-lookup"><span data-stu-id="5d544-167">Property</span></span> | <span data-ttu-id="5d544-168">Opis</span><span class="sxs-lookup"><span data-stu-id="5d544-168">Description</span></span> | <span data-ttu-id="5d544-169">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="5d544-169">Allowed values</span></span> | <span data-ttu-id="5d544-170">Wymagane</span><span class="sxs-lookup"><span data-stu-id="5d544-170">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="5d544-171">query</span><span class="sxs-lookup"><span data-stu-id="5d544-171">query</span></span> |<span data-ttu-id="5d544-172">Użyj niestandardowych zapytania można odczytać danych.</span><span class="sxs-lookup"><span data-stu-id="5d544-172">Use the custom query to read data.</span></span> |<span data-ttu-id="5d544-173">Ciąg zapytania SQL.</span><span class="sxs-lookup"><span data-stu-id="5d544-173">SQL query string.</span></span> <span data-ttu-id="5d544-174">Na przykład: Wybierz * z MyTable.</span><span class="sxs-lookup"><span data-stu-id="5d544-174">For example: select * from MyTable.</span></span> |<span data-ttu-id="5d544-175">Tak</span><span class="sxs-lookup"><span data-stu-id="5d544-175">Yes</span></span> |

### <a name="json-example-copy-data-from-teradata-to-azure-blob"></a><span data-ttu-id="5d544-176">Przykład JSON: kopiowanie danych z programu Teradata do obiektów Blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="5d544-176">JSON example: Copy data from Teradata to Azure Blob</span></span>
<span data-ttu-id="5d544-177">W poniższym przykładzie przedstawiono przykładowe definicje JSON, które można użyć, aby utworzyć potok przy użyciu [portalu Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) lub [programu Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) lub [programu Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="5d544-177">The following example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="5d544-178">Przedstawiają sposób kopiowania danych z programu Teradata do magazynu obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="5d544-178">They show how to copy data from Teradata to Azure Blob Storage.</span></span> <span data-ttu-id="5d544-179">Jednak można skopiować danych do dowolnego wychwytywanie podane [tutaj](data-factory-data-movement-activities.md#supported-data-stores-and-formats) za pomocą działania kopiowania w fabryce danych Azure.</span><span class="sxs-lookup"><span data-stu-id="5d544-179">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>   

<span data-ttu-id="5d544-180">Przykład zawiera następujące obiekty fabryki danych:</span><span class="sxs-lookup"><span data-stu-id="5d544-180">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="5d544-181">Połączonej usługi typu [OnPremisesTeradata](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="5d544-181">A linked service of type [OnPremisesTeradata](#linked-service-properties).</span></span>
2. <span data-ttu-id="5d544-182">Połączonej usługi typu [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="5d544-182">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="5d544-183">Dane wejściowe [dataset](data-factory-create-datasets.md) typu [RelationalTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="5d544-183">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
4. <span data-ttu-id="5d544-184">Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="5d544-184">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="5d544-185">[Potoku](data-factory-create-pipelines.md) z działaniem kopii, która używa [RelationalSource](#copy-activity-properties) i [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="5d544-185">The [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="5d544-186">Przykład kopiuje dane z wyniku kwerendy w bazie danych programu Teradata do obiektu blob co godzinę.</span><span class="sxs-lookup"><span data-stu-id="5d544-186">The sample copies data from a query result in Teradata database to a blob every hour.</span></span> <span data-ttu-id="5d544-187">Właściwości JSON używane w te przykłady są opisane w sekcjach poniżej próbek.</span><span class="sxs-lookup"><span data-stu-id="5d544-187">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="5d544-188">Pierwszym krokiem konfiguracji bramy zarządzania danymi.</span><span class="sxs-lookup"><span data-stu-id="5d544-188">As a first step, setup the data management gateway.</span></span> <span data-ttu-id="5d544-189">Instrukcje znajdują się w [przenoszenie danych między lokalizacji lokalnej i w chmurze](data-factory-move-data-between-onprem-and-cloud.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="5d544-189">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="5d544-190">**Teradata połączonej usługi:**</span><span class="sxs-lookup"><span data-stu-id="5d544-190">**Teradata linked service:**</span></span>

```json
{
    "name": "OnPremTeradataLinkedService",
    "properties": {
        "type": "OnPremisesTeradata",
        "typeProperties": {
            "server": "<server>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```

<span data-ttu-id="5d544-191">**Magazyn obiektów Blob Azure połączonej usługi:**</span><span class="sxs-lookup"><span data-stu-id="5d544-191">**Azure Blob storage linked service:**</span></span>

```json
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

<span data-ttu-id="5d544-192">**Wejściowy zestaw danych programu Teradata:**</span><span class="sxs-lookup"><span data-stu-id="5d544-192">**Teradata input dataset:**</span></span>

<span data-ttu-id="5d544-193">Przykładzie przyjęto założenie, utworzysz tabelę "MyTable" Teradata i zawiera kolumnę o nazwie "timestamp" dla czasu serii danych.</span><span class="sxs-lookup"><span data-stu-id="5d544-193">The sample assumes you have created a table “MyTable” in Teradata and it contains a column called “timestamp” for time series data.</span></span>

<span data-ttu-id="5d544-194">Ustawienie "external": true usługi fabryka danych informuje, że w tabeli zewnętrznej dla fabryki danych i nie jest generowany przez działanie w fabryce danych.</span><span class="sxs-lookup"><span data-stu-id="5d544-194">Setting “external”: true informs the Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

```json
{
    "name": "TeradataDataSet",
    "properties": {
        "published": false,
        "type": "RelationalTable",
        "linkedServiceName": "OnPremTeradataLinkedService",
        "typeProperties": {
        },
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

<span data-ttu-id="5d544-195">**Azure Blob wyjściowy zestaw danych:**</span><span class="sxs-lookup"><span data-stu-id="5d544-195">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="5d544-196">Dane są zapisywane do nowego obiektu blob co godzinę (częstotliwość: godziny, interwał: 1).</span><span class="sxs-lookup"><span data-stu-id="5d544-196">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="5d544-197">Ścieżka folderu dla obiekt blob jest dynamicznie obliczane na podstawie czasu rozpoczęcia wycinek, który jest przetwarzana.</span><span class="sxs-lookup"><span data-stu-id="5d544-197">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="5d544-198">Ścieżka folderu używa rok, miesiąc, dzień i godziny części czas rozpoczęcia.</span><span class="sxs-lookup"><span data-stu-id="5d544-198">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```json
{
    "name": "AzureBlobTeradataDataSet",
    "properties": {
        "published": false,
        "location": {
            "type": "AzureBlobLocation",
            "folderPath": "mycontainer/teradata/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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
            ],
            "linkedServiceName": "AzureStorageLinkedService"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```
<span data-ttu-id="5d544-199">**W potoku z działania kopiowania:**</span><span class="sxs-lookup"><span data-stu-id="5d544-199">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="5d544-200">Potok zawiera działanie kopiowania, który jest skonfigurowany do używania wejściowe i wyjściowe zestawy danych i jest zaplanowane co godzinę.</span><span class="sxs-lookup"><span data-stu-id="5d544-200">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run hourly.</span></span> <span data-ttu-id="5d544-201">W definicji JSON potoku **źródła** ustawiono typ **RelationalSource** i **zbiornika** ustawiono typ **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="5d544-201">In the pipeline JSON definition, the **source** type is set to **RelationalSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="5d544-202">Określony dla zapytania SQL **zapytania** właściwości wybiera dane w ostatniej godziny do skopiowania.</span><span class="sxs-lookup"><span data-stu-id="5d544-202">The SQL query specified for the **query** property selects the data in the past hour to copy.</span></span>

```json
{
    "name": "CopyTeradataToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', SliceStart, SliceEnd)"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "TeradataDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobTeradataDataSet"
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
                "name": "TeradataToBlob"
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z",
        "isPaused": false
    }
}
```
## <a name="type-mapping-for-teradata"></a><span data-ttu-id="5d544-203">Mapowanie typu dla programu Teradata</span><span class="sxs-lookup"><span data-stu-id="5d544-203">Type mapping for Teradata</span></span>
<span data-ttu-id="5d544-204">Jak wspomniano w [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, wykonuje działanie kopiowania automatyczne konwersje z typów źródła do zbiornika typów o następujące podejście krok 2:</span><span class="sxs-lookup"><span data-stu-id="5d544-204">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, the Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="5d544-205">Konwertowanie typów natywnych źródła na typ architektury .NET</span><span class="sxs-lookup"><span data-stu-id="5d544-205">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="5d544-206">Konwertowanie na typ macierzysty ujścia typ architektury .NET</span><span class="sxs-lookup"><span data-stu-id="5d544-206">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="5d544-207">Podczas przenoszenia danych do programu Teradata, następujące mapowania są używane z typu Teradata do typ architektury .NET.</span><span class="sxs-lookup"><span data-stu-id="5d544-207">When moving data to Teradata, the following mappings are used from Teradata type to .NET type.</span></span>

| <span data-ttu-id="5d544-208">Typ bazy danych programu Teradata</span><span class="sxs-lookup"><span data-stu-id="5d544-208">Teradata Database type</span></span> | <span data-ttu-id="5d544-209">Typ programu .NET framework</span><span class="sxs-lookup"><span data-stu-id="5d544-209">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="5d544-210">char</span><span class="sxs-lookup"><span data-stu-id="5d544-210">Char</span></span> |<span data-ttu-id="5d544-211">Ciąg</span><span class="sxs-lookup"><span data-stu-id="5d544-211">String</span></span> |
| <span data-ttu-id="5d544-212">CLOB</span><span class="sxs-lookup"><span data-stu-id="5d544-212">Clob</span></span> |<span data-ttu-id="5d544-213">Ciąg</span><span class="sxs-lookup"><span data-stu-id="5d544-213">String</span></span> |
| <span data-ttu-id="5d544-214">Grafika</span><span class="sxs-lookup"><span data-stu-id="5d544-214">Graphic</span></span> |<span data-ttu-id="5d544-215">Ciąg</span><span class="sxs-lookup"><span data-stu-id="5d544-215">String</span></span> |
| <span data-ttu-id="5d544-216">VarChar</span><span class="sxs-lookup"><span data-stu-id="5d544-216">VarChar</span></span> |<span data-ttu-id="5d544-217">Ciąg</span><span class="sxs-lookup"><span data-stu-id="5d544-217">String</span></span> |
| <span data-ttu-id="5d544-218">VarGraphic</span><span class="sxs-lookup"><span data-stu-id="5d544-218">VarGraphic</span></span> |<span data-ttu-id="5d544-219">Ciąg</span><span class="sxs-lookup"><span data-stu-id="5d544-219">String</span></span> |
| <span data-ttu-id="5d544-220">Obiekt blob</span><span class="sxs-lookup"><span data-stu-id="5d544-220">Blob</span></span> |<span data-ttu-id="5d544-221">Byte]</span><span class="sxs-lookup"><span data-stu-id="5d544-221">Byte[]</span></span> |
| <span data-ttu-id="5d544-222">Bajtów</span><span class="sxs-lookup"><span data-stu-id="5d544-222">Byte</span></span> |<span data-ttu-id="5d544-223">Byte]</span><span class="sxs-lookup"><span data-stu-id="5d544-223">Byte[]</span></span> |
| <span data-ttu-id="5d544-224">VarByte</span><span class="sxs-lookup"><span data-stu-id="5d544-224">VarByte</span></span> |<span data-ttu-id="5d544-225">Byte]</span><span class="sxs-lookup"><span data-stu-id="5d544-225">Byte[]</span></span> |
| <span data-ttu-id="5d544-226">BigInt</span><span class="sxs-lookup"><span data-stu-id="5d544-226">BigInt</span></span> |<span data-ttu-id="5d544-227">Int64</span><span class="sxs-lookup"><span data-stu-id="5d544-227">Int64</span></span> |
| <span data-ttu-id="5d544-228">ByteInt</span><span class="sxs-lookup"><span data-stu-id="5d544-228">ByteInt</span></span> |<span data-ttu-id="5d544-229">Int16</span><span class="sxs-lookup"><span data-stu-id="5d544-229">Int16</span></span> |
| <span data-ttu-id="5d544-230">Decimal</span><span class="sxs-lookup"><span data-stu-id="5d544-230">Decimal</span></span> |<span data-ttu-id="5d544-231">Decimal</span><span class="sxs-lookup"><span data-stu-id="5d544-231">Decimal</span></span> |
| <span data-ttu-id="5d544-232">O podwójnej precyzji</span><span class="sxs-lookup"><span data-stu-id="5d544-232">Double</span></span> |<span data-ttu-id="5d544-233">O podwójnej precyzji</span><span class="sxs-lookup"><span data-stu-id="5d544-233">Double</span></span> |
| <span data-ttu-id="5d544-234">Liczba całkowita</span><span class="sxs-lookup"><span data-stu-id="5d544-234">Integer</span></span> |<span data-ttu-id="5d544-235">Int32</span><span class="sxs-lookup"><span data-stu-id="5d544-235">Int32</span></span> |
| <span data-ttu-id="5d544-236">Numer</span><span class="sxs-lookup"><span data-stu-id="5d544-236">Number</span></span> |<span data-ttu-id="5d544-237">O podwójnej precyzji</span><span class="sxs-lookup"><span data-stu-id="5d544-237">Double</span></span> |
| <span data-ttu-id="5d544-238">SmallInt</span><span class="sxs-lookup"><span data-stu-id="5d544-238">SmallInt</span></span> |<span data-ttu-id="5d544-239">Int16</span><span class="sxs-lookup"><span data-stu-id="5d544-239">Int16</span></span> |
| <span data-ttu-id="5d544-240">Date</span><span class="sxs-lookup"><span data-stu-id="5d544-240">Date</span></span> |<span data-ttu-id="5d544-241">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="5d544-241">DateTime</span></span> |
| <span data-ttu-id="5d544-242">Time</span><span class="sxs-lookup"><span data-stu-id="5d544-242">Time</span></span> |<span data-ttu-id="5d544-243">Zakres czasu</span><span class="sxs-lookup"><span data-stu-id="5d544-243">TimeSpan</span></span> |
| <span data-ttu-id="5d544-244">Czas ze strefą czasową</span><span class="sxs-lookup"><span data-stu-id="5d544-244">Time With Time Zone</span></span> |<span data-ttu-id="5d544-245">Ciąg</span><span class="sxs-lookup"><span data-stu-id="5d544-245">String</span></span> |
| <span data-ttu-id="5d544-246">Znacznik czasu</span><span class="sxs-lookup"><span data-stu-id="5d544-246">Timestamp</span></span> |<span data-ttu-id="5d544-247">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="5d544-247">DateTime</span></span> |
| <span data-ttu-id="5d544-248">Sygnatura czasowa ze strefą czasową</span><span class="sxs-lookup"><span data-stu-id="5d544-248">Timestamp With Time Zone</span></span> |<span data-ttu-id="5d544-249">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="5d544-249">DateTimeOffset</span></span> |
| <span data-ttu-id="5d544-250">Interwał dnia</span><span class="sxs-lookup"><span data-stu-id="5d544-250">Interval Day</span></span> |<span data-ttu-id="5d544-251">Zakres czasu</span><span class="sxs-lookup"><span data-stu-id="5d544-251">TimeSpan</span></span> |
| <span data-ttu-id="5d544-252">Interwał dzień na godzinę</span><span class="sxs-lookup"><span data-stu-id="5d544-252">Interval Day To Hour</span></span> |<span data-ttu-id="5d544-253">Zakres czasu</span><span class="sxs-lookup"><span data-stu-id="5d544-253">TimeSpan</span></span> |
| <span data-ttu-id="5d544-254">Interwał dzień na minutę</span><span class="sxs-lookup"><span data-stu-id="5d544-254">Interval Day To Minute</span></span> |<span data-ttu-id="5d544-255">Zakres czasu</span><span class="sxs-lookup"><span data-stu-id="5d544-255">TimeSpan</span></span> |
| <span data-ttu-id="5d544-256">Interwał dzień na sekundę</span><span class="sxs-lookup"><span data-stu-id="5d544-256">Interval Day To Second</span></span> |<span data-ttu-id="5d544-257">Zakres czasu</span><span class="sxs-lookup"><span data-stu-id="5d544-257">TimeSpan</span></span> |
| <span data-ttu-id="5d544-258">Interwał, godzinę</span><span class="sxs-lookup"><span data-stu-id="5d544-258">Interval Hour</span></span> |<span data-ttu-id="5d544-259">Zakres czasu</span><span class="sxs-lookup"><span data-stu-id="5d544-259">TimeSpan</span></span> |
| <span data-ttu-id="5d544-260">Interwał godzinę, minutę</span><span class="sxs-lookup"><span data-stu-id="5d544-260">Interval Hour To Minute</span></span> |<span data-ttu-id="5d544-261">Zakres czasu</span><span class="sxs-lookup"><span data-stu-id="5d544-261">TimeSpan</span></span> |
| <span data-ttu-id="5d544-262">Interwał godzinę na sekundę</span><span class="sxs-lookup"><span data-stu-id="5d544-262">Interval Hour To Second</span></span> |<span data-ttu-id="5d544-263">Zakres czasu</span><span class="sxs-lookup"><span data-stu-id="5d544-263">TimeSpan</span></span> |
| <span data-ttu-id="5d544-264">Interwał minutę</span><span class="sxs-lookup"><span data-stu-id="5d544-264">Interval Minute</span></span> |<span data-ttu-id="5d544-265">Zakres czasu</span><span class="sxs-lookup"><span data-stu-id="5d544-265">TimeSpan</span></span> |
| <span data-ttu-id="5d544-266">Interwał minutę na sekundę</span><span class="sxs-lookup"><span data-stu-id="5d544-266">Interval Minute To Second</span></span> |<span data-ttu-id="5d544-267">Zakres czasu</span><span class="sxs-lookup"><span data-stu-id="5d544-267">TimeSpan</span></span> |
| <span data-ttu-id="5d544-268">Interwał drugi</span><span class="sxs-lookup"><span data-stu-id="5d544-268">Interval Second</span></span> |<span data-ttu-id="5d544-269">Zakres czasu</span><span class="sxs-lookup"><span data-stu-id="5d544-269">TimeSpan</span></span> |
| <span data-ttu-id="5d544-270">Interwał roku</span><span class="sxs-lookup"><span data-stu-id="5d544-270">Interval Year</span></span> |<span data-ttu-id="5d544-271">Ciąg</span><span class="sxs-lookup"><span data-stu-id="5d544-271">String</span></span> |
| <span data-ttu-id="5d544-272">Interwał rok, miesiąc</span><span class="sxs-lookup"><span data-stu-id="5d544-272">Interval Year To Month</span></span> |<span data-ttu-id="5d544-273">Ciąg</span><span class="sxs-lookup"><span data-stu-id="5d544-273">String</span></span> |
| <span data-ttu-id="5d544-274">Interwał miesiąca</span><span class="sxs-lookup"><span data-stu-id="5d544-274">Interval Month</span></span> |<span data-ttu-id="5d544-275">Ciąg</span><span class="sxs-lookup"><span data-stu-id="5d544-275">String</span></span> |
| <span data-ttu-id="5d544-276">Period(Date)</span><span class="sxs-lookup"><span data-stu-id="5d544-276">Period(Date)</span></span> |<span data-ttu-id="5d544-277">Ciąg</span><span class="sxs-lookup"><span data-stu-id="5d544-277">String</span></span> |
| <span data-ttu-id="5d544-278">Period(Time)</span><span class="sxs-lookup"><span data-stu-id="5d544-278">Period(Time)</span></span> |<span data-ttu-id="5d544-279">Ciąg</span><span class="sxs-lookup"><span data-stu-id="5d544-279">String</span></span> |
| <span data-ttu-id="5d544-280">Okres (czas ze strefą czasową)</span><span class="sxs-lookup"><span data-stu-id="5d544-280">Period(Time With Time Zone)</span></span> |<span data-ttu-id="5d544-281">Ciąg</span><span class="sxs-lookup"><span data-stu-id="5d544-281">String</span></span> |
| <span data-ttu-id="5d544-282">Period(TimeStamp)</span><span class="sxs-lookup"><span data-stu-id="5d544-282">Period(Timestamp)</span></span> |<span data-ttu-id="5d544-283">Ciąg</span><span class="sxs-lookup"><span data-stu-id="5d544-283">String</span></span> |
| <span data-ttu-id="5d544-284">Okres (sygnatura ze strefą czasową)</span><span class="sxs-lookup"><span data-stu-id="5d544-284">Period(Timestamp With Time Zone)</span></span> |<span data-ttu-id="5d544-285">Ciąg</span><span class="sxs-lookup"><span data-stu-id="5d544-285">String</span></span> |
| <span data-ttu-id="5d544-286">XML</span><span class="sxs-lookup"><span data-stu-id="5d544-286">Xml</span></span> |<span data-ttu-id="5d544-287">Ciąg</span><span class="sxs-lookup"><span data-stu-id="5d544-287">String</span></span> |

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="5d544-288">Obiekt sink kolumn mapy źródła</span><span class="sxs-lookup"><span data-stu-id="5d544-288">Map source to sink columns</span></span>
<span data-ttu-id="5d544-289">Aby uzyskać informacje dotyczące mapowania kolumn w zestawie źródła danych do kolumn w zestawie danych zbiornika, zobacz [mapowania kolumnach dataset w fabryce danych Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="5d544-289">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="5d544-290">Odczyt powtarzalny ze źródłami relacyjnymi</span><span class="sxs-lookup"><span data-stu-id="5d544-290">Repeatable read from relational sources</span></span>
<span data-ttu-id="5d544-291">Podczas kopiowania danych z danych relacyjnych przechowuje, należy pamiętać, aby uniknąć niezamierzone wyniki powtarzalności.</span><span class="sxs-lookup"><span data-stu-id="5d544-291">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="5d544-292">Fabryka danych Azure możesz ponownie ręcznie wycinek.</span><span class="sxs-lookup"><span data-stu-id="5d544-292">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="5d544-293">Można również skonfigurować zasady ponawiania dla zestawu danych, aby wycinek jest uruchamiany ponownie, gdy wystąpi błąd.</span><span class="sxs-lookup"><span data-stu-id="5d544-293">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="5d544-294">Podczas wycinek zostanie uruchomiona ponownie w obu przypadkach, należy się upewnić, że te same dane jest do odczytu niezależnie od tego, ile razy wycinek jest uruchamiany.</span><span class="sxs-lookup"><span data-stu-id="5d544-294">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="5d544-295">Zobacz [Repeatable odczytywać źródłami relacyjnymi](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="5d544-295">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="5d544-296">Wydajność i dostrajania</span><span class="sxs-lookup"><span data-stu-id="5d544-296">Performance and Tuning</span></span>
<span data-ttu-id="5d544-297">Zobacz [wydajności działania kopiowania & dostrajanie przewodnik](data-factory-copy-activity-performance.md) Aby dowiedzieć się więcej o kluczowych czynników tego wydajność wpływ przenoszenia danych (działanie kopiowania) w usłudze fabryka danych Azure i zoptymalizować ją na różne sposoby.</span><span class="sxs-lookup"><span data-stu-id="5d544-297">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
