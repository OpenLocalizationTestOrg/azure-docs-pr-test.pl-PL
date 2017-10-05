---
title: "Przenoszenie danych z programu MySQL przy użyciu fabryki danych Azure | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat sposobu przenoszenia danych z bazy danych MySQL przy użyciu fabryki danych Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 452f4fce-9eb5-40a0-92f8-1e98691bea4c
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: jingwang
ms.openlocfilehash: 05159bfd98977d0b57b43fbc02e4579439f7ce4c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-from-mysql-using-azure-data-factory"></a><span data-ttu-id="c90ed-103">Przenoszenie danych z MySQL przy użyciu fabryki danych Azure</span><span class="sxs-lookup"><span data-stu-id="c90ed-103">Move data From MySQL using Azure Data Factory</span></span>
<span data-ttu-id="c90ed-104">W tym artykule opisano sposób używania działania kopiowania w fabryce danych Azure do przenoszenia danych z lokalną bazą danych MySQL.</span><span class="sxs-lookup"><span data-stu-id="c90ed-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises MySQL database.</span></span> <span data-ttu-id="c90ed-105">Opiera się na [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, który przedstawia ogólny przegląd przenoszenia danych z działania kopiowania.</span><span class="sxs-lookup"><span data-stu-id="c90ed-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="c90ed-106">Wszystkie obsługiwanych ujścia magazynu danych można skopiować danych z lokalnego magazynu danych MySQL.</span><span class="sxs-lookup"><span data-stu-id="c90ed-106">You can copy data from an on-premises MySQL data store to any supported sink data store.</span></span> <span data-ttu-id="c90ed-107">Lista magazynów danych obsługiwane jako wychwytywanie przez działanie kopiowania, zobacz [obsługiwane magazyny danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabeli.</span><span class="sxs-lookup"><span data-stu-id="c90ed-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="c90ed-108">Fabryka danych aktualnie obsługuje tylko dane przenoszenie, z magazynu danych MySQL do innych magazynów danych, ale nie do przenoszenia danych z innych magazynów danych z magazynem danych MySQL.</span><span class="sxs-lookup"><span data-stu-id="c90ed-108">Data factory currently supports only moving data from a MySQL data store to other data stores, but not for moving data from other data stores to an MySQL data store.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="c90ed-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="c90ed-109">Prerequisites</span></span>
<span data-ttu-id="c90ed-110">Usługi fabryka danych obsługuje połączenia ze źródłami MySQL lokalnymi przy użyciu bramy zarządzania danymi.</span><span class="sxs-lookup"><span data-stu-id="c90ed-110">Data Factory service supports connecting to on-premises MySQL sources using the Data Management Gateway.</span></span> <span data-ttu-id="c90ed-111">Zobacz [przenoszenie danych między lokalizacji lokalnej i w chmurze](data-factory-move-data-between-onprem-and-cloud.md) artykułu, aby dowiedzieć się więcej na temat bramy zarządzania danymi i instrukcje krok po kroku dotyczące konfigurowania bramy.</span><span class="sxs-lookup"><span data-stu-id="c90ed-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span></span>

<span data-ttu-id="c90ed-112">Nawet wtedy, gdy baza danych programu MySQL znajduje się na maszynie wirtualnej platformy Azure IaaS (VM), wymagana jest brama.</span><span class="sxs-lookup"><span data-stu-id="c90ed-112">Gateway is required even if the MySQL database is hosted in an Azure IaaS virtual machine (VM).</span></span> <span data-ttu-id="c90ed-113">Można zainstalować bramę na tej samej maszyny Wirtualnej do przechowywania danych lub w innej maszyny Wirtualnej, tak długo, jak bramy można połączyć z bazą danych.</span><span class="sxs-lookup"><span data-stu-id="c90ed-113">You can install the gateway on the same VM as the data store or on a different VM as long as the gateway can connect to the database.</span></span>

> [!NOTE]
> <span data-ttu-id="c90ed-114">Zobacz [rozwiązywania problemów bramy](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) porady dotyczące rozwiązywania problemów z bramy/połączenia problemy związane z.</span><span class="sxs-lookup"><span data-stu-id="c90ed-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="c90ed-115">Obsługiwane wersje i instalacji</span><span class="sxs-lookup"><span data-stu-id="c90ed-115">Supported versions and installation</span></span>
<span data-ttu-id="c90ed-116">Dla bramy zarządzania danymi do łączenia z bazą danych MySQL, musisz zainstalować [MySQL Connector/Net systemu Microsoft Windows](https://dev.mysql.com/downloads/connector/net/) (wersja 6.6.5 lub nowszego) na tym samym systemie co brama zarządzania danymi.</span><span class="sxs-lookup"><span data-stu-id="c90ed-116">For Data Management Gateway to connect to the MySQL Database, you need to install the [MySQL Connector/Net for Microsoft Windows](https://dev.mysql.com/downloads/connector/net/) (version 6.6.5 or above) on the same system as the Data Management Gateway.</span></span> <span data-ttu-id="c90ed-117">MySQL w wersji 5.1 i nowszych jest obsługiwany.</span><span class="sxs-lookup"><span data-stu-id="c90ed-117">MySQL version 5.1 and above is supported.</span></span>

> [!TIP]
> <span data-ttu-id="c90ed-118">Jeśli zostanie osiągnięty błąd "Uwierzytelnianie nie powiodło się, ponieważ strona zdalna zamknęła strumień transportu.", należy wziąć pod uwagę, aby uaktualnić MySQL Connector/Net do nowszej wersji.</span><span class="sxs-lookup"><span data-stu-id="c90ed-118">If you hit error on "Authentication failed because the remote party has closed the transport stream.", consider to upgrade the MySQL Connector/Net to higher version.</span></span>

## <a name="getting-started"></a><span data-ttu-id="c90ed-119">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="c90ed-119">Getting started</span></span>
<span data-ttu-id="c90ed-120">Można utworzyć potok z działania kopiowania, który przenosi dane z magazynu lokalnego Cassandra danych przy użyciu różnych narzędzi/interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="c90ed-120">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="c90ed-121">Najprostszym sposobem, aby utworzyć potok jest użycie **kreatora kopiowania**.</span><span class="sxs-lookup"><span data-stu-id="c90ed-121">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="c90ed-122">Zobacz [samouczek: tworzenie potoku za pomocą Kreatora kopiowania](data-factory-copy-data-wizard-tutorial.md) szybkie przewodnik dotyczący tworzenia potoku za pomocą Kreatora kopiowania danych.</span><span class="sxs-lookup"><span data-stu-id="c90ed-122">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span> 
- <span data-ttu-id="c90ed-123">Umożliwia także następujące narzędzia do tworzenia potoku: **portalu Azure**, **programu Visual Studio**, **programu Azure PowerShell**, **szablonu usługi Azure Resource Manager**, **interfejs API .NET**, i **interfejsu API REST**.</span><span class="sxs-lookup"><span data-stu-id="c90ed-123">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="c90ed-124">Zobacz [samouczek działania kopiowania](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) instrukcje krok po kroku utworzyć potok z działaniem kopiowania.</span><span class="sxs-lookup"><span data-stu-id="c90ed-124">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="c90ed-125">Czy można użyć narzędzia i interfejsy API, należy wykonać następujące kroki, aby utworzyć potok, który przenosi dane z magazynu danych źródła do ujścia magazynu danych:</span><span class="sxs-lookup"><span data-stu-id="c90ed-125">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="c90ed-126">Utwórz **połączone usługi** Aby połączyć dane wejściowe i wyjściowe są przechowywane w fabryce danych.</span><span class="sxs-lookup"><span data-stu-id="c90ed-126">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="c90ed-127">Utwórz **zestawów danych** do reprezentowania danych wejściowych i wyjściowych operacji kopiowania.</span><span class="sxs-lookup"><span data-stu-id="c90ed-127">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="c90ed-128">Utwórz **potoku** aktywnością kopiowania zestawu danych jako dane wejściowe i zestawu danych jako dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="c90ed-128">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="c90ed-129">Korzystając z kreatora, definicje JSON do tych jednostek fabryki danych (połączone usługi, zestawy danych i potoki) są tworzone automatycznie dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="c90ed-129">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="c90ed-130">Korzystając z narzędzi/API (z wyjątkiem interfejs API .NET), należy zdefiniować tych jednostek fabryki danych w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="c90ed-130">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="c90ed-131">Dla przykładu z definicji JSON dla jednostek fabryki danych, które służą do kopiowania danych z lokalnego magazynu danych MySQL, zobacz [przykład JSON: kopiowanie danych z programu MySQL do obiektów Blob platformy Azure](#json-example-copy-data-from-mysql-to-azure-blob) sekcji tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="c90ed-131">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises MySQL data store, see [JSON example: Copy data from MySQL to Azure Blob](#json-example-copy-data-from-mysql-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="c90ed-132">Poniższe sekcje zawierają szczegółowe informacje o właściwości JSON, które są używane do definiowania jednostek fabryki danych określonej w magazynie danych MySQL:</span><span class="sxs-lookup"><span data-stu-id="c90ed-132">The following sections provide details about JSON properties that are used to define Data Factory entities specific to a MySQL data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="c90ed-133">Połączona usługa właściwości</span><span class="sxs-lookup"><span data-stu-id="c90ed-133">Linked service properties</span></span>
<span data-ttu-id="c90ed-134">Poniższa tabela zawiera opis specyficzne dla usługi MySQL połączone elementy JSON.</span><span class="sxs-lookup"><span data-stu-id="c90ed-134">The following table provides description for JSON elements specific to MySQL linked service.</span></span>

| <span data-ttu-id="c90ed-135">Właściwość</span><span class="sxs-lookup"><span data-stu-id="c90ed-135">Property</span></span> | <span data-ttu-id="c90ed-136">Opis</span><span class="sxs-lookup"><span data-stu-id="c90ed-136">Description</span></span> | <span data-ttu-id="c90ed-137">Wymagane</span><span class="sxs-lookup"><span data-stu-id="c90ed-137">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c90ed-138">type</span><span class="sxs-lookup"><span data-stu-id="c90ed-138">type</span></span> |<span data-ttu-id="c90ed-139">Właściwość type musi mieć ustawioną: **OnPremisesMySql**</span><span class="sxs-lookup"><span data-stu-id="c90ed-139">The type property must be set to: **OnPremisesMySql**</span></span> |<span data-ttu-id="c90ed-140">Tak</span><span class="sxs-lookup"><span data-stu-id="c90ed-140">Yes</span></span> |
| <span data-ttu-id="c90ed-141">serwer</span><span class="sxs-lookup"><span data-stu-id="c90ed-141">server</span></span> |<span data-ttu-id="c90ed-142">Nazwa serwera MySQL.</span><span class="sxs-lookup"><span data-stu-id="c90ed-142">Name of the MySQL server.</span></span> |<span data-ttu-id="c90ed-143">Tak</span><span class="sxs-lookup"><span data-stu-id="c90ed-143">Yes</span></span> |
| <span data-ttu-id="c90ed-144">Bazy danych</span><span class="sxs-lookup"><span data-stu-id="c90ed-144">database</span></span> |<span data-ttu-id="c90ed-145">Nazwa bazy danych MySQL.</span><span class="sxs-lookup"><span data-stu-id="c90ed-145">Name of the MySQL database.</span></span> |<span data-ttu-id="c90ed-146">Tak</span><span class="sxs-lookup"><span data-stu-id="c90ed-146">Yes</span></span> |
| <span data-ttu-id="c90ed-147">Schemat</span><span class="sxs-lookup"><span data-stu-id="c90ed-147">schema</span></span> |<span data-ttu-id="c90ed-148">Nazwa schematu w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="c90ed-148">Name of the schema in the database.</span></span> |<span data-ttu-id="c90ed-149">Nie</span><span class="sxs-lookup"><span data-stu-id="c90ed-149">No</span></span> |
| <span data-ttu-id="c90ed-150">Typ authenticationType</span><span class="sxs-lookup"><span data-stu-id="c90ed-150">authenticationType</span></span> |<span data-ttu-id="c90ed-151">Typ uwierzytelniania używany do łączenia z bazą danych MySQL.</span><span class="sxs-lookup"><span data-stu-id="c90ed-151">Type of authentication used to connect to the MySQL database.</span></span> <span data-ttu-id="c90ed-152">Możliwe wartości to: `Basic`.</span><span class="sxs-lookup"><span data-stu-id="c90ed-152">Possible values are: `Basic`.</span></span> |<span data-ttu-id="c90ed-153">Tak</span><span class="sxs-lookup"><span data-stu-id="c90ed-153">Yes</span></span> |
| <span data-ttu-id="c90ed-154">nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="c90ed-154">username</span></span> |<span data-ttu-id="c90ed-155">Określ nazwę użytkownika do połączenia z bazą danych MySQL.</span><span class="sxs-lookup"><span data-stu-id="c90ed-155">Specify user name to connect to the MySQL database.</span></span> |<span data-ttu-id="c90ed-156">Tak</span><span class="sxs-lookup"><span data-stu-id="c90ed-156">Yes</span></span> |
| <span data-ttu-id="c90ed-157">hasło</span><span class="sxs-lookup"><span data-stu-id="c90ed-157">password</span></span> |<span data-ttu-id="c90ed-158">Określ hasło dla określonego konta użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c90ed-158">Specify password for the user account you specified.</span></span> |<span data-ttu-id="c90ed-159">Tak</span><span class="sxs-lookup"><span data-stu-id="c90ed-159">Yes</span></span> |
| <span data-ttu-id="c90ed-160">gatewayName</span><span class="sxs-lookup"><span data-stu-id="c90ed-160">gatewayName</span></span> |<span data-ttu-id="c90ed-161">Nazwa bramy, która powinna być używana przez usługi fabryka danych nawiązać połączenia z lokalną bazą danych MySQL.</span><span class="sxs-lookup"><span data-stu-id="c90ed-161">Name of the gateway that the Data Factory service should use to connect to the on-premises MySQL database.</span></span> |<span data-ttu-id="c90ed-162">Tak</span><span class="sxs-lookup"><span data-stu-id="c90ed-162">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="c90ed-163">Właściwości zestawu danych</span><span class="sxs-lookup"><span data-stu-id="c90ed-163">Dataset properties</span></span>
<span data-ttu-id="c90ed-164">Aby uzyskać pełną listę sekcje & właściwości dostępne do definiowania zestawów danych, zobacz [Tworzenie zbiorów danych](data-factory-create-datasets.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="c90ed-164">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="c90ed-165">Sekcje zawierają informacje, takie jak struktury, dostępności i zasad zestawu danych JSON są podobne dla wszystkich typów obiektów dataset (Azure SQL, obiektów blob platformy Azure, Azure tabeli itp.).</span><span class="sxs-lookup"><span data-stu-id="c90ed-165">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="c90ed-166">**TypeProperties** sekcja jest różne dla każdego typu zestawu danych i zawiera informacje o lokalizacji danych w magazynie danych.</span><span class="sxs-lookup"><span data-stu-id="c90ed-166">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="c90ed-167">TypeProperties sekcja dla zestawu danych typu **RelationalTable** (w tym zestawie danych MySQL) ma następujące właściwości</span><span class="sxs-lookup"><span data-stu-id="c90ed-167">The typeProperties section for dataset of type **RelationalTable** (which includes MySQL dataset) has the following properties</span></span>

| <span data-ttu-id="c90ed-168">Właściwość</span><span class="sxs-lookup"><span data-stu-id="c90ed-168">Property</span></span> | <span data-ttu-id="c90ed-169">Opis</span><span class="sxs-lookup"><span data-stu-id="c90ed-169">Description</span></span> | <span data-ttu-id="c90ed-170">Wymagane</span><span class="sxs-lookup"><span data-stu-id="c90ed-170">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c90ed-171">tableName</span><span class="sxs-lookup"><span data-stu-id="c90ed-171">tableName</span></span> |<span data-ttu-id="c90ed-172">Nazwa tabeli w wystąpieniu bazy danych MySQL, odnoszący się do połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="c90ed-172">Name of the table in the MySQL Database instance that linked service refers to.</span></span> |<span data-ttu-id="c90ed-173">Nie (Jeśli **zapytania** z **RelationalSource** jest określona)</span><span class="sxs-lookup"><span data-stu-id="c90ed-173">No (if **query** of **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="c90ed-174">Właściwości działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="c90ed-174">Copy activity properties</span></span>
<span data-ttu-id="c90ed-175">Pełną listę sekcje & właściwości dostępne do definiowania działań, zobacz [tworzenie potoków](data-factory-create-pipelines.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="c90ed-175">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="c90ed-176">Właściwości, takie jak nazwa, opis i tabel wejściowych i wyjściowych, czy zasady są dostępne dla wszystkich typów działań.</span><span class="sxs-lookup"><span data-stu-id="c90ed-176">Properties such as name, description, input and output tables, are policies are available for all types of activities.</span></span>

<span data-ttu-id="c90ed-177">Właściwości dostępne w **typeProperties** sekcji działania zależne od każdego typu działania.</span><span class="sxs-lookup"><span data-stu-id="c90ed-177">Whereas, properties available in the **typeProperties** section of the activity vary with each activity type.</span></span> <span data-ttu-id="c90ed-178">Dla działania kopiowania różnią się w zależności od typów źródeł i sink.</span><span class="sxs-lookup"><span data-stu-id="c90ed-178">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="c90ed-179">Gdy źródło w przypadku działania kopiowania jest typu **RelationalSource** (która obejmuje MySQL), w sekcji typeProperties dostępne są następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="c90ed-179">When source in copy activity is of type **RelationalSource** (which includes MySQL), the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="c90ed-180">Właściwość</span><span class="sxs-lookup"><span data-stu-id="c90ed-180">Property</span></span> | <span data-ttu-id="c90ed-181">Opis</span><span class="sxs-lookup"><span data-stu-id="c90ed-181">Description</span></span> | <span data-ttu-id="c90ed-182">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="c90ed-182">Allowed values</span></span> | <span data-ttu-id="c90ed-183">Wymagane</span><span class="sxs-lookup"><span data-stu-id="c90ed-183">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="c90ed-184">query</span><span class="sxs-lookup"><span data-stu-id="c90ed-184">query</span></span> |<span data-ttu-id="c90ed-185">Użyj niestandardowych zapytania można odczytać danych.</span><span class="sxs-lookup"><span data-stu-id="c90ed-185">Use the custom query to read data.</span></span> |<span data-ttu-id="c90ed-186">Ciąg zapytania SQL.</span><span class="sxs-lookup"><span data-stu-id="c90ed-186">SQL query string.</span></span> <span data-ttu-id="c90ed-187">Na przykład: Wybierz * z MyTable.</span><span class="sxs-lookup"><span data-stu-id="c90ed-187">For example: select * from MyTable.</span></span> |<span data-ttu-id="c90ed-188">Nie (Jeśli **tableName** z **dataset** jest określona)</span><span class="sxs-lookup"><span data-stu-id="c90ed-188">No (if **tableName** of **dataset** is specified)</span></span> |


## <a name="json-example-copy-data-from-mysql-to-azure-blob"></a><span data-ttu-id="c90ed-189">Przykład JSON: kopiowanie danych z programu MySQL do obiektów Blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="c90ed-189">JSON example: Copy data from MySQL to Azure Blob</span></span>
<span data-ttu-id="c90ed-190">W poniższym przykładzie przedstawiono przykładowe definicje JSON, które można użyć, aby utworzyć potok przy użyciu [portalu Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) lub [programu Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) lub [programu Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="c90ed-190">This example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="c90ed-191">Widoczny jest sposób kopiowania danych z lokalną bazą danych MySQL do magazynu obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="c90ed-191">It shows how to copy data from an on-premises MySQL database to an Azure Blob Storage.</span></span> <span data-ttu-id="c90ed-192">Jednak można skopiować danych do dowolnego wychwytywanie podane [tutaj](data-factory-data-movement-activities.md#supported-data-stores-and-formats) za pomocą działania kopiowania w fabryce danych Azure.</span><span class="sxs-lookup"><span data-stu-id="c90ed-192">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c90ed-193">W tym przykładzie przedstawiono fragmenty kodu JSON.</span><span class="sxs-lookup"><span data-stu-id="c90ed-193">This sample provides JSON snippets.</span></span> <span data-ttu-id="c90ed-194">Zawiera instrukcje krok po kroku dotyczące tworzenia fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="c90ed-194">It does not include step-by-step instructions for creating the data factory.</span></span> <span data-ttu-id="c90ed-195">Zobacz [przenoszenie danych między lokalizacji lokalnej i w chmurze](data-factory-move-data-between-onprem-and-cloud.md) artykułu, aby uzyskać instrukcje krok po kroku.</span><span class="sxs-lookup"><span data-stu-id="c90ed-195">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="c90ed-196">Przykład zawiera następujące obiekty fabryki danych:</span><span class="sxs-lookup"><span data-stu-id="c90ed-196">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="c90ed-197">Połączonej usługi typu [OnPremisesMySql](data-factory-onprem-mysql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="c90ed-197">A linked service of type [OnPremisesMySql](data-factory-onprem-mysql-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="c90ed-198">Połączonej usługi typu [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="c90ed-198">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="c90ed-199">Dane wejściowe [dataset](data-factory-create-datasets.md) typu [RelationalTable](data-factory-onprem-mysql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="c90ed-199">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](data-factory-onprem-mysql-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="c90ed-200">Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="c90ed-200">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="c90ed-201">A [potoku](data-factory-create-pipelines.md) z działaniem kopii, która używa [RelationalSource](data-factory-onprem-mysql-connector.md#copy-activity-properties) i [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="c90ed-201">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](data-factory-onprem-mysql-connector.md#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="c90ed-202">Przykład kopiuje dane z wyniku kwerendy w bazie danych MySQL do obiektu blob co godzinę.</span><span class="sxs-lookup"><span data-stu-id="c90ed-202">The sample copies data from a query result in MySQL database to a blob hourly.</span></span> <span data-ttu-id="c90ed-203">Właściwości JSON używane w te przykłady są opisane w sekcjach poniżej próbek.</span><span class="sxs-lookup"><span data-stu-id="c90ed-203">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="c90ed-204">Pierwszym krokiem konfiguracji bramy zarządzania danymi.</span><span class="sxs-lookup"><span data-stu-id="c90ed-204">As a first step, setup the data management gateway.</span></span> <span data-ttu-id="c90ed-205">Instrukcje znajdują się w [przenoszenie danych między lokalizacji lokalnej i w chmurze](data-factory-move-data-between-onprem-and-cloud.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="c90ed-205">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="c90ed-206">**MySQL połączonej usługi:**</span><span class="sxs-lookup"><span data-stu-id="c90ed-206">**MySQL linked service:**</span></span>

```JSON
    {
      "name": "OnPremMySqlLinkedService",
      "properties": {
        "type": "OnPremisesMySql",
        "typeProperties": {
          "server": "<server name>",
          "database": "<database name>",
          "schema": "<schema name>",
          "authenticationType": "<authentication type>",
          "userName": "<user name>",
          "password": "<password>",
          "gatewayName": "<gateway>"
        }
      }
    }
```

<span data-ttu-id="c90ed-207">**Połączonej usługi magazynu Azure:**</span><span class="sxs-lookup"><span data-stu-id="c90ed-207">**Azure Storage linked service:**</span></span>

```JSON
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

<span data-ttu-id="c90ed-208">**Wejściowy zestaw danych MySQL:**</span><span class="sxs-lookup"><span data-stu-id="c90ed-208">**MySQL input dataset:**</span></span>

<span data-ttu-id="c90ed-209">Przykładzie przyjęto założenie, utworzysz tabelę "MyTable" MySQL i zawiera kolumnę o nazwie "timestampcolumn" dla czasu serii danych.</span><span class="sxs-lookup"><span data-stu-id="c90ed-209">The sample assumes you have created a table “MyTable” in MySQL and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="c90ed-210">Ustawienie "external": "prawda" informuje usługi fabryka danych czy tabeli zewnętrznej dla fabryki danych i nie jest generowany przez działanie w fabryce danych.</span><span class="sxs-lookup"><span data-stu-id="c90ed-210">Setting “external”: ”true” informs the Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

```JSON
    {
        "name": "MySqlDataSet",
        "properties": {
            "published": false,
            "type": "RelationalTable",
            "linkedServiceName": "OnPremMySqlLinkedService",
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

<span data-ttu-id="c90ed-211">**Azure Blob wyjściowy zestaw danych:**</span><span class="sxs-lookup"><span data-stu-id="c90ed-211">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="c90ed-212">Dane są zapisywane do nowego obiektu blob co godzinę (częstotliwość: godziny, interwał: 1).</span><span class="sxs-lookup"><span data-stu-id="c90ed-212">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="c90ed-213">Ścieżka folderu dla obiekt blob jest dynamicznie obliczane na podstawie czasu rozpoczęcia wycinek, który jest przetwarzana.</span><span class="sxs-lookup"><span data-stu-id="c90ed-213">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="c90ed-214">Ścieżka folderu używa rok, miesiąc, dzień i godziny części czas rozpoczęcia.</span><span class="sxs-lookup"><span data-stu-id="c90ed-214">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```JSON
    {
        "name": "AzureBlobMySqlDataSet",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "folderPath": "mycontainer/mysql/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

<span data-ttu-id="c90ed-215">**W potoku z działania kopiowania:**</span><span class="sxs-lookup"><span data-stu-id="c90ed-215">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="c90ed-216">Potok zawiera działanie kopiowania, który jest skonfigurowany do używania wejściowe i wyjściowe zestawy danych i jest zaplanowane co godzinę.</span><span class="sxs-lookup"><span data-stu-id="c90ed-216">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="c90ed-217">W definicji JSON potoku **źródła** ustawiono typ **RelationalSource** i **zbiornika** ustawiono typ **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="c90ed-217">In the pipeline JSON definition, the **source** type is set to **RelationalSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="c90ed-218">Określony dla zapytania SQL **zapytania** właściwości wybiera dane w ostatniej godziny do skopiowania.</span><span class="sxs-lookup"><span data-stu-id="c90ed-218">The SQL query specified for the **query** property selects the data in the past hour to copy.</span></span>

```JSON
    {
        "name": "CopyMySqlToBlob",
        "properties": {
            "description": "pipeline for copy activity",
            "activities": [
                {
                    "type": "Copy",
                    "typeProperties": {
                        "source": {
                            "type": "RelationalSource",
                            "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                        },
                        "sink": {
                            "type": "BlobSink",
                            "writeBatchSize": 0,
                            "writeBatchTimeout": "00:00:00"
                        }
                    },
                    "inputs": [
                        {
                            "name": "MySqlDataSet"
                        }
                    ],
                    "outputs": [
                        {
                            "name": "AzureBlobMySqlDataSet"
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
                    "name": "MySqlToBlob"
                }
            ],
            "start": "2014-06-01T18:00:00Z",
            "end": "2014-06-01T19:00:00Z"
        }
    }
```


### <a name="type-mapping-for-mysql"></a><span data-ttu-id="c90ed-219">Mapowanie typu dla programu MySQL</span><span class="sxs-lookup"><span data-stu-id="c90ed-219">Type mapping for MySQL</span></span>
<span data-ttu-id="c90ed-220">Jak wspomniano w [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, automatyczne konwersje z typów źródła do zbiornika typy z następujących rozwinięcie wykonuje działania kopiowania:</span><span class="sxs-lookup"><span data-stu-id="c90ed-220">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following two-step approach:</span></span>

1. <span data-ttu-id="c90ed-221">Konwertowanie typów natywnych źródła na typ architektury .NET</span><span class="sxs-lookup"><span data-stu-id="c90ed-221">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="c90ed-222">Konwertowanie na typ macierzysty ujścia typ architektury .NET</span><span class="sxs-lookup"><span data-stu-id="c90ed-222">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="c90ed-223">Podczas przenoszenia danych na MySQL, następujące mapowania są używane do typów .NET z typów MySQL.</span><span class="sxs-lookup"><span data-stu-id="c90ed-223">When moving data to MySQL, the following mappings are used from MySQL types to .NET types.</span></span>

| <span data-ttu-id="c90ed-224">Typ bazy danych MySQL</span><span class="sxs-lookup"><span data-stu-id="c90ed-224">MySQL Database type</span></span> | <span data-ttu-id="c90ed-225">Typ programu .NET framework</span><span class="sxs-lookup"><span data-stu-id="c90ed-225">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="c90ed-226">bigint bez znaku</span><span class="sxs-lookup"><span data-stu-id="c90ed-226">bigint unsigned</span></span> |<span data-ttu-id="c90ed-227">Decimal</span><span class="sxs-lookup"><span data-stu-id="c90ed-227">Decimal</span></span> |
| <span data-ttu-id="c90ed-228">bigint</span><span class="sxs-lookup"><span data-stu-id="c90ed-228">bigint</span></span> |<span data-ttu-id="c90ed-229">Int64</span><span class="sxs-lookup"><span data-stu-id="c90ed-229">Int64</span></span> |
| <span data-ttu-id="c90ed-230">bitowe</span><span class="sxs-lookup"><span data-stu-id="c90ed-230">bit</span></span> |<span data-ttu-id="c90ed-231">Decimal</span><span class="sxs-lookup"><span data-stu-id="c90ed-231">Decimal</span></span> |
| <span data-ttu-id="c90ed-232">Obiekt blob</span><span class="sxs-lookup"><span data-stu-id="c90ed-232">blob</span></span> |<span data-ttu-id="c90ed-233">Byte]</span><span class="sxs-lookup"><span data-stu-id="c90ed-233">Byte[]</span></span> |
| <span data-ttu-id="c90ed-234">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="c90ed-234">bool</span></span> |<span data-ttu-id="c90ed-235">Wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="c90ed-235">Boolean</span></span> |
| <span data-ttu-id="c90ed-236">char</span><span class="sxs-lookup"><span data-stu-id="c90ed-236">char</span></span> |<span data-ttu-id="c90ed-237">Ciąg</span><span class="sxs-lookup"><span data-stu-id="c90ed-237">String</span></span> |
| <span data-ttu-id="c90ed-238">Data</span><span class="sxs-lookup"><span data-stu-id="c90ed-238">date</span></span> |<span data-ttu-id="c90ed-239">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="c90ed-239">Datetime</span></span> |
| <span data-ttu-id="c90ed-240">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="c90ed-240">datetime</span></span> |<span data-ttu-id="c90ed-241">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="c90ed-241">Datetime</span></span> |
| <span data-ttu-id="c90ed-242">Decimal</span><span class="sxs-lookup"><span data-stu-id="c90ed-242">decimal</span></span> |<span data-ttu-id="c90ed-243">Decimal</span><span class="sxs-lookup"><span data-stu-id="c90ed-243">Decimal</span></span> |
| <span data-ttu-id="c90ed-244">podwójnej precyzji</span><span class="sxs-lookup"><span data-stu-id="c90ed-244">double precision</span></span> |<span data-ttu-id="c90ed-245">O podwójnej precyzji</span><span class="sxs-lookup"><span data-stu-id="c90ed-245">Double</span></span> |
| <span data-ttu-id="c90ed-246">O podwójnej precyzji</span><span class="sxs-lookup"><span data-stu-id="c90ed-246">double</span></span> |<span data-ttu-id="c90ed-247">O podwójnej precyzji</span><span class="sxs-lookup"><span data-stu-id="c90ed-247">Double</span></span> |
| <span data-ttu-id="c90ed-248">wyliczenia</span><span class="sxs-lookup"><span data-stu-id="c90ed-248">enum</span></span> |<span data-ttu-id="c90ed-249">Ciąg</span><span class="sxs-lookup"><span data-stu-id="c90ed-249">String</span></span> |
| <span data-ttu-id="c90ed-250">Float</span><span class="sxs-lookup"><span data-stu-id="c90ed-250">float</span></span> |<span data-ttu-id="c90ed-251">Pojedynczy</span><span class="sxs-lookup"><span data-stu-id="c90ed-251">Single</span></span> |
| <span data-ttu-id="c90ed-252">int unsigned</span><span class="sxs-lookup"><span data-stu-id="c90ed-252">int unsigned</span></span> |<span data-ttu-id="c90ed-253">Int64</span><span class="sxs-lookup"><span data-stu-id="c90ed-253">Int64</span></span> |
| <span data-ttu-id="c90ed-254">int</span><span class="sxs-lookup"><span data-stu-id="c90ed-254">int</span></span> |<span data-ttu-id="c90ed-255">Int32</span><span class="sxs-lookup"><span data-stu-id="c90ed-255">Int32</span></span> |
| <span data-ttu-id="c90ed-256">Liczba całkowita bez znaku</span><span class="sxs-lookup"><span data-stu-id="c90ed-256">integer unsigned</span></span> |<span data-ttu-id="c90ed-257">Int64</span><span class="sxs-lookup"><span data-stu-id="c90ed-257">Int64</span></span> |
| <span data-ttu-id="c90ed-258">Liczba całkowita</span><span class="sxs-lookup"><span data-stu-id="c90ed-258">integer</span></span> |<span data-ttu-id="c90ed-259">Int32</span><span class="sxs-lookup"><span data-stu-id="c90ed-259">Int32</span></span> |
| <span data-ttu-id="c90ed-260">długie varbinary</span><span class="sxs-lookup"><span data-stu-id="c90ed-260">long varbinary</span></span> |<span data-ttu-id="c90ed-261">Byte]</span><span class="sxs-lookup"><span data-stu-id="c90ed-261">Byte[]</span></span> |
| <span data-ttu-id="c90ed-262">varchar długa</span><span class="sxs-lookup"><span data-stu-id="c90ed-262">long varchar</span></span> |<span data-ttu-id="c90ed-263">Ciąg</span><span class="sxs-lookup"><span data-stu-id="c90ed-263">String</span></span> |
| <span data-ttu-id="c90ed-264">longblob</span><span class="sxs-lookup"><span data-stu-id="c90ed-264">longblob</span></span> |<span data-ttu-id="c90ed-265">Byte]</span><span class="sxs-lookup"><span data-stu-id="c90ed-265">Byte[]</span></span> |
| <span data-ttu-id="c90ed-266">LONGTEXT</span><span class="sxs-lookup"><span data-stu-id="c90ed-266">longtext</span></span> |<span data-ttu-id="c90ed-267">Ciąg</span><span class="sxs-lookup"><span data-stu-id="c90ed-267">String</span></span> |
| <span data-ttu-id="c90ed-268">mediumblob</span><span class="sxs-lookup"><span data-stu-id="c90ed-268">mediumblob</span></span> |<span data-ttu-id="c90ed-269">Byte]</span><span class="sxs-lookup"><span data-stu-id="c90ed-269">Byte[]</span></span> |
| <span data-ttu-id="c90ed-270">mediumint bez znaku</span><span class="sxs-lookup"><span data-stu-id="c90ed-270">mediumint unsigned</span></span> |<span data-ttu-id="c90ed-271">Int64</span><span class="sxs-lookup"><span data-stu-id="c90ed-271">Int64</span></span> |
| <span data-ttu-id="c90ed-272">mediumint</span><span class="sxs-lookup"><span data-stu-id="c90ed-272">mediumint</span></span> |<span data-ttu-id="c90ed-273">Int32</span><span class="sxs-lookup"><span data-stu-id="c90ed-273">Int32</span></span> |
| <span data-ttu-id="c90ed-274">mediumtext</span><span class="sxs-lookup"><span data-stu-id="c90ed-274">mediumtext</span></span> |<span data-ttu-id="c90ed-275">Ciąg</span><span class="sxs-lookup"><span data-stu-id="c90ed-275">String</span></span> |
| <span data-ttu-id="c90ed-276">numeryczne</span><span class="sxs-lookup"><span data-stu-id="c90ed-276">numeric</span></span> |<span data-ttu-id="c90ed-277">Decimal</span><span class="sxs-lookup"><span data-stu-id="c90ed-277">Decimal</span></span> |
| <span data-ttu-id="c90ed-278">rzeczywiste</span><span class="sxs-lookup"><span data-stu-id="c90ed-278">real</span></span> |<span data-ttu-id="c90ed-279">O podwójnej precyzji</span><span class="sxs-lookup"><span data-stu-id="c90ed-279">Double</span></span> |
| <span data-ttu-id="c90ed-280">zestaw</span><span class="sxs-lookup"><span data-stu-id="c90ed-280">set</span></span> |<span data-ttu-id="c90ed-281">Ciąg</span><span class="sxs-lookup"><span data-stu-id="c90ed-281">String</span></span> |
| <span data-ttu-id="c90ed-282">smallint bez znaku</span><span class="sxs-lookup"><span data-stu-id="c90ed-282">smallint unsigned</span></span> |<span data-ttu-id="c90ed-283">Int32</span><span class="sxs-lookup"><span data-stu-id="c90ed-283">Int32</span></span> |
| <span data-ttu-id="c90ed-284">smallint</span><span class="sxs-lookup"><span data-stu-id="c90ed-284">smallint</span></span> |<span data-ttu-id="c90ed-285">Int16</span><span class="sxs-lookup"><span data-stu-id="c90ed-285">Int16</span></span> |
| <span data-ttu-id="c90ed-286">Tekst</span><span class="sxs-lookup"><span data-stu-id="c90ed-286">text</span></span> |<span data-ttu-id="c90ed-287">Ciąg</span><span class="sxs-lookup"><span data-stu-id="c90ed-287">String</span></span> |
| <span data-ttu-id="c90ed-288">time</span><span class="sxs-lookup"><span data-stu-id="c90ed-288">time</span></span> |<span data-ttu-id="c90ed-289">Zakres czasu</span><span class="sxs-lookup"><span data-stu-id="c90ed-289">TimeSpan</span></span> |
| <span data-ttu-id="c90ed-290">sygnatura czasowa</span><span class="sxs-lookup"><span data-stu-id="c90ed-290">timestamp</span></span> |<span data-ttu-id="c90ed-291">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="c90ed-291">Datetime</span></span> |
| <span data-ttu-id="c90ed-292">tinyblob</span><span class="sxs-lookup"><span data-stu-id="c90ed-292">tinyblob</span></span> |<span data-ttu-id="c90ed-293">Byte]</span><span class="sxs-lookup"><span data-stu-id="c90ed-293">Byte[]</span></span> |
| <span data-ttu-id="c90ed-294">tinyint bez znaku</span><span class="sxs-lookup"><span data-stu-id="c90ed-294">tinyint unsigned</span></span> |<span data-ttu-id="c90ed-295">Int16</span><span class="sxs-lookup"><span data-stu-id="c90ed-295">Int16</span></span> |
| <span data-ttu-id="c90ed-296">tinyint</span><span class="sxs-lookup"><span data-stu-id="c90ed-296">tinyint</span></span> |<span data-ttu-id="c90ed-297">Int16</span><span class="sxs-lookup"><span data-stu-id="c90ed-297">Int16</span></span> |
| <span data-ttu-id="c90ed-298">tinytext</span><span class="sxs-lookup"><span data-stu-id="c90ed-298">tinytext</span></span> |<span data-ttu-id="c90ed-299">Ciąg</span><span class="sxs-lookup"><span data-stu-id="c90ed-299">String</span></span> |
| <span data-ttu-id="c90ed-300">varchar</span><span class="sxs-lookup"><span data-stu-id="c90ed-300">varchar</span></span> |<span data-ttu-id="c90ed-301">Ciąg</span><span class="sxs-lookup"><span data-stu-id="c90ed-301">String</span></span> |
| <span data-ttu-id="c90ed-302">Roku</span><span class="sxs-lookup"><span data-stu-id="c90ed-302">year</span></span> |<span data-ttu-id="c90ed-303">int</span><span class="sxs-lookup"><span data-stu-id="c90ed-303">Int</span></span> |

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="c90ed-304">Obiekt sink kolumn mapy źródła</span><span class="sxs-lookup"><span data-stu-id="c90ed-304">Map source to sink columns</span></span>
<span data-ttu-id="c90ed-305">Aby uzyskać informacje dotyczące mapowania kolumn w zestawie źródła danych do kolumn w zestawie danych zbiornika, zobacz [mapowania kolumnach dataset w fabryce danych Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="c90ed-305">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="c90ed-306">Odczyt powtarzalny ze źródłami relacyjnymi</span><span class="sxs-lookup"><span data-stu-id="c90ed-306">Repeatable read from relational sources</span></span>
<span data-ttu-id="c90ed-307">Podczas kopiowania danych z danych relacyjnych przechowuje, należy pamiętać, aby uniknąć niezamierzone wyniki powtarzalności.</span><span class="sxs-lookup"><span data-stu-id="c90ed-307">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="c90ed-308">Fabryka danych Azure możesz ponownie ręcznie wycinek.</span><span class="sxs-lookup"><span data-stu-id="c90ed-308">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="c90ed-309">Można również skonfigurować zasady ponawiania dla zestawu danych, aby wycinek jest uruchamiany ponownie, gdy wystąpi błąd.</span><span class="sxs-lookup"><span data-stu-id="c90ed-309">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="c90ed-310">Podczas wycinek zostanie uruchomiona ponownie w obu przypadkach, należy się upewnić, że te same dane jest do odczytu niezależnie od tego, ile razy wycinek jest uruchamiany.</span><span class="sxs-lookup"><span data-stu-id="c90ed-310">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="c90ed-311">Zobacz [Repeatable odczytywać źródłami relacyjnymi](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="c90ed-311">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="c90ed-312">Wydajność i dostrajania</span><span class="sxs-lookup"><span data-stu-id="c90ed-312">Performance and Tuning</span></span>
<span data-ttu-id="c90ed-313">Zobacz [wydajności działania kopiowania & dostrajanie przewodnik](data-factory-copy-activity-performance.md) Aby dowiedzieć się więcej o kluczowych czynników tego wydajność wpływ przenoszenia danych (działanie kopiowania) w usłudze fabryka danych Azure i zoptymalizować ją na różne sposoby.</span><span class="sxs-lookup"><span data-stu-id="c90ed-313">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
