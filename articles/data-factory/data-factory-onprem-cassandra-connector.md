---
title: "Przenoszenia danych z Cassandra przy użyciu fabryki danych | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat sposobu przenoszenia danych z Cassandra lokalną bazą danych przy użyciu fabryki danych Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 085cc312-42ca-4f43-aa35-535b35a102d5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jingwang
ms.openlocfilehash: f2b225bdbdf2880d26a6ab5f992301bf0a804b0d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="move-data-from-an-on-premises-cassandra-database-using-azure-data-factory"></a><span data-ttu-id="7b6bd-103">Przenoszenia danych z Cassandra lokalną bazą danych przy użyciu fabryki danych Azure</span><span class="sxs-lookup"><span data-stu-id="7b6bd-103">Move data from an on-premises Cassandra database using Azure Data Factory</span></span>
<span data-ttu-id="7b6bd-104">W tym artykule opisano sposób używania działania kopiowania w fabryce danych Azure do przenoszenia danych z lokalną bazą danych Cassandra.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises Cassandra database.</span></span> <span data-ttu-id="7b6bd-105">Opiera się na [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, który przedstawia ogólny przegląd przenoszenia danych z działania kopiowania.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="7b6bd-106">Można skopiować danych z lokalnego magazynu danych Cassandra żadnych obsługiwanych ujścia magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-106">You can copy data from an on-premises Cassandra data store to any supported sink data store.</span></span> <span data-ttu-id="7b6bd-107">Lista magazynów danych obsługiwane jako wychwytywanie przez działanie kopiowania, zobacz [obsługiwane magazyny danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabeli.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="7b6bd-108">Fabryka danych aktualnie obsługuje tylko dane przenoszenie, z magazynu danych Cassandra do innych magazynów danych, ale nie do przenoszenia danych z innych magazynów danych w magazynie danych Cassandra.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-108">Data factory currently supports only moving data from a Cassandra data store to other data stores, but not for moving data from other data stores to a Cassandra data store.</span></span> 

## <a name="supported-versions"></a><span data-ttu-id="7b6bd-109">Obsługiwane wersje</span><span class="sxs-lookup"><span data-stu-id="7b6bd-109">Supported versions</span></span>
<span data-ttu-id="7b6bd-110">Łącznik Cassandra obsługuje następujące wersje Cassandra: 2.X.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-110">The Cassandra connector supports the following versions of Cassandra: 2.X.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7b6bd-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="7b6bd-111">Prerequisites</span></span>
<span data-ttu-id="7b6bd-112">Dla usługi fabryka danych Azure można było nawiązać połączenia z lokalną bazą danych Cassandra należy zainstalować bramę zarządzania danymi na tym samym komputerze, który jest hostem bazy danych lub na osobnym komputerze, aby uniknąć konkurowanie o zasoby z bazą danych.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-112">For the Azure Data Factory service to be able to connect to your on-premises Cassandra database, you must install a Data Management Gateway on the same machine that hosts the database or on a separate machine to avoid competing for resources with the database.</span></span> <span data-ttu-id="7b6bd-113">Brama zarządzania danymi jest składnikiem, który łączy lokalnych źródeł danych do usługi w chmurze w sposób bezpieczny i zarządzanie nimi.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-113">Data Management Gateway is a component that connects on-premises data sources to cloud services in a secure and managed way.</span></span> <span data-ttu-id="7b6bd-114">Zobacz [brama zarządzania danymi](data-factory-data-management-gateway.md) artykułu, aby uzyskać więcej informacji dotyczących bramy zarządzania danymi.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-114">See [Data Management Gateway](data-factory-data-management-gateway.md) article for details about Data Management Gateway.</span></span> <span data-ttu-id="7b6bd-115">Zobacz [przenoszenia danych z lokalnymi do chmury](data-factory-move-data-between-onprem-and-cloud.md) artykułu, aby uzyskać instrukcje krok po kroku dotyczące konfigurowania bramy danych potoku do przenoszenia danych.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-115">See [Move data from on-premises to cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on setting up the gateway a data pipeline to move data.</span></span>

<span data-ttu-id="7b6bd-116">Należy używać bramy do połączenia z bazą danych Cassandra nawet wtedy, gdy baza danych znajduje się w chmurze, na przykład na maszynie Wirtualnej platformy Azure IaaS.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-116">You must use the gateway to connect to a Cassandra database even if the database is hosted in the cloud, for example, on an Azure IaaS VM.</span></span> <span data-ttu-id="7b6bd-117">Y może masz bramy na tej samej maszyny Wirtualnej, który jest hostem bazy danych lub na oddzielnych maszynie Wirtualnej tak długo, jak bramy można połączyć z bazą danych.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-117">Y You can have the gateway on the same VM that hosts the database or on a separate VM as long as the gateway can connect to the database.</span></span>  

<span data-ttu-id="7b6bd-118">Po zainstalowaniu bramy, automatycznie instaluje sterownik Microsoft Cassandra ODBC używane do łączenia z bazą danych Cassandra.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-118">When you install the gateway, it automatically installs a Microsoft Cassandra ODBC driver used to connect to Cassandra database.</span></span> <span data-ttu-id="7b6bd-119">W związku z tym nie trzeba ręcznie zainstalowania sterownika na komputerze bramy, podczas kopiowania danych z bazy danych Cassandra.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-119">Therefore, you don't need to manually install any driver on the gateway machine when copying data from the Cassandra database.</span></span> 

> [!NOTE]
> <span data-ttu-id="7b6bd-120">Zobacz [rozwiązywania problemów bramy](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) porady dotyczące rozwiązywania problemów z bramy/połączenia problemy związane z.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-120">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="getting-started"></a><span data-ttu-id="7b6bd-121">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="7b6bd-121">Getting started</span></span>
<span data-ttu-id="7b6bd-122">Można utworzyć potok z działania kopiowania, który przenosi dane z magazynu lokalnego Cassandra danych przy użyciu różnych narzędzi/interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-122">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="7b6bd-123">Najprostszym sposobem, aby utworzyć potok jest użycie **kreatora kopiowania**.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-123">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="7b6bd-124">Zobacz [samouczek: tworzenie potoku za pomocą Kreatora kopiowania](data-factory-copy-data-wizard-tutorial.md) szybkie przewodnik dotyczący tworzenia potoku za pomocą Kreatora kopiowania danych.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-124">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span> 
- <span data-ttu-id="7b6bd-125">Umożliwia także następujące narzędzia do tworzenia potoku: **portalu Azure**, **programu Visual Studio**, **programu Azure PowerShell**, **szablonu usługi Azure Resource Manager**, **interfejs API .NET**, i **interfejsu API REST**.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-125">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="7b6bd-126">Zobacz [samouczek działania kopiowania](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) instrukcje krok po kroku utworzyć potok z działaniem kopiowania.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-126">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="7b6bd-127">Czy można użyć narzędzia i interfejsy API, należy wykonać następujące kroki, aby utworzyć potok, który przenosi dane z magazynu danych źródła do ujścia magazynu danych:</span><span class="sxs-lookup"><span data-stu-id="7b6bd-127">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="7b6bd-128">Utwórz **połączone usługi** Aby połączyć dane wejściowe i wyjściowe są przechowywane w fabryce danych.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-128">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="7b6bd-129">Utwórz **zestawów danych** do reprezentowania danych wejściowych i wyjściowych operacji kopiowania.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-129">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="7b6bd-130">Utwórz **potoku** aktywnością kopiowania zestawu danych jako dane wejściowe i zestawu danych jako dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-130">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="7b6bd-131">Korzystając z kreatora, definicje JSON do tych jednostek fabryki danych (połączone usługi, zestawy danych i potoki) są tworzone automatycznie dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-131">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="7b6bd-132">Korzystając z narzędzi/API (z wyjątkiem interfejs API .NET), należy zdefiniować tych jednostek fabryki danych w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-132">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="7b6bd-133">Dla przykładu z definicji JSON dla jednostek fabryki danych, które służą do kopiowania danych z magazynu danych Cassandra lokalnych, zobacz [przykład JSON: kopiowanie danych z Cassandra do obiektów Blob platformy Azure](#json-example-copy-data-from-cassandra-to-azure-blob) sekcji tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-133">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises Cassandra data store, see [JSON example: Copy data from Cassandra to Azure Blob](#json-example-copy-data-from-cassandra-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="7b6bd-134">Poniższe sekcje zawierają szczegółowe informacje o właściwości JSON, które są używane do definiowania jednostek fabryki danych określonej w magazynie danych Cassandra:</span><span class="sxs-lookup"><span data-stu-id="7b6bd-134">The following sections provide details about JSON properties that are used to define Data Factory entities specific to a Cassandra data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="7b6bd-135">Połączona usługa właściwości</span><span class="sxs-lookup"><span data-stu-id="7b6bd-135">Linked service properties</span></span>
<span data-ttu-id="7b6bd-136">Poniższa tabela zawiera opis specyficzne dla usługi Cassandra połączone elementy JSON.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-136">The following table provides description for JSON elements specific to Cassandra linked service.</span></span>

| <span data-ttu-id="7b6bd-137">Właściwość</span><span class="sxs-lookup"><span data-stu-id="7b6bd-137">Property</span></span> | <span data-ttu-id="7b6bd-138">Opis</span><span class="sxs-lookup"><span data-stu-id="7b6bd-138">Description</span></span> | <span data-ttu-id="7b6bd-139">Wymagane</span><span class="sxs-lookup"><span data-stu-id="7b6bd-139">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7b6bd-140">type</span><span class="sxs-lookup"><span data-stu-id="7b6bd-140">type</span></span> |<span data-ttu-id="7b6bd-141">Właściwość type musi mieć ustawioną: **OnPremisesCassandra**</span><span class="sxs-lookup"><span data-stu-id="7b6bd-141">The type property must be set to: **OnPremisesCassandra**</span></span> |<span data-ttu-id="7b6bd-142">Tak</span><span class="sxs-lookup"><span data-stu-id="7b6bd-142">Yes</span></span> |
| <span data-ttu-id="7b6bd-143">Host</span><span class="sxs-lookup"><span data-stu-id="7b6bd-143">host</span></span> |<span data-ttu-id="7b6bd-144">Jeden lub więcej adresów IP lub nazw hostów serwerów Cassandra.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-144">One or more IP addresses or host names of Cassandra servers.</span></span><br/><br/><span data-ttu-id="7b6bd-145">Określ rozdzielaną przecinkami listę adresów IP lub nazw hostów, aby nawiązać połączenie wszystkie serwery jednocześnie.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-145">Specify a comma-separated list of IP addresses or host names to connect to all servers concurrently.</span></span> |<span data-ttu-id="7b6bd-146">Tak</span><span class="sxs-lookup"><span data-stu-id="7b6bd-146">Yes</span></span> |
| <span data-ttu-id="7b6bd-147">port</span><span class="sxs-lookup"><span data-stu-id="7b6bd-147">port</span></span> |<span data-ttu-id="7b6bd-148">Port TCP używany przez serwer Cassandra nasłuchiwanie dla połączeń klienta.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-148">The TCP port that the Cassandra server uses to listen for client connections.</span></span> |<span data-ttu-id="7b6bd-149">Nie, wartość domyślna: 9042</span><span class="sxs-lookup"><span data-stu-id="7b6bd-149">No, default value: 9042</span></span> |
| <span data-ttu-id="7b6bd-150">Typ authenticationType</span><span class="sxs-lookup"><span data-stu-id="7b6bd-150">authenticationType</span></span> |<span data-ttu-id="7b6bd-151">Podstawowa lub anonimowe</span><span class="sxs-lookup"><span data-stu-id="7b6bd-151">Basic, or Anonymous</span></span> |<span data-ttu-id="7b6bd-152">Tak</span><span class="sxs-lookup"><span data-stu-id="7b6bd-152">Yes</span></span> |
| <span data-ttu-id="7b6bd-153">nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="7b6bd-153">username</span></span> |<span data-ttu-id="7b6bd-154">Określ nazwę użytkownika dla konta użytkownika.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-154">Specify user name for the user account.</span></span> |<span data-ttu-id="7b6bd-155">Tak, jeśli authenticationType ustawiany jest podstawowy.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-155">Yes, if authenticationType is set to Basic.</span></span> |
| <span data-ttu-id="7b6bd-156">hasło</span><span class="sxs-lookup"><span data-stu-id="7b6bd-156">password</span></span> |<span data-ttu-id="7b6bd-157">Określ hasło dla konta użytkownika.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-157">Specify password for the user account.</span></span> |<span data-ttu-id="7b6bd-158">Tak, jeśli authenticationType ustawiany jest podstawowy.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-158">Yes, if authenticationType is set to Basic.</span></span> |
| <span data-ttu-id="7b6bd-159">gatewayName</span><span class="sxs-lookup"><span data-stu-id="7b6bd-159">gatewayName</span></span> |<span data-ttu-id="7b6bd-160">Nazwa bramy, która służy do łączenia z bazą danych Cassandra lokalnymi.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-160">The name of the gateway that is used to connect to the on-premises Cassandra database.</span></span> |<span data-ttu-id="7b6bd-161">Tak</span><span class="sxs-lookup"><span data-stu-id="7b6bd-161">Yes</span></span> |
| <span data-ttu-id="7b6bd-162">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="7b6bd-162">encryptedCredential</span></span> |<span data-ttu-id="7b6bd-163">Poświadczenie szyfrowane przez bramę.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-163">Credential encrypted by the gateway.</span></span> |<span data-ttu-id="7b6bd-164">Nie</span><span class="sxs-lookup"><span data-stu-id="7b6bd-164">No</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="7b6bd-165">Właściwości zestawu danych</span><span class="sxs-lookup"><span data-stu-id="7b6bd-165">Dataset properties</span></span>
<span data-ttu-id="7b6bd-166">Aby uzyskać pełną listę sekcje & właściwości dostępne do definiowania zestawów danych, zobacz [Tworzenie zbiorów danych](data-factory-create-datasets.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-166">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="7b6bd-167">Sekcje zawierają informacje, takie jak struktury, dostępności i zasad zestawu danych JSON są podobne dla wszystkich typów obiektów dataset (Azure SQL, obiektów blob platformy Azure, Azure tabeli itp.).</span><span class="sxs-lookup"><span data-stu-id="7b6bd-167">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="7b6bd-168">**TypeProperties** sekcja jest różne dla każdego typu zestawu danych i zawiera informacje o lokalizacji danych w magazynie danych.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-168">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="7b6bd-169">TypeProperties sekcja dla zestawu danych typu **CassandraTable** ma następujące właściwości</span><span class="sxs-lookup"><span data-stu-id="7b6bd-169">The typeProperties section for dataset of type **CassandraTable** has the following properties</span></span>

| <span data-ttu-id="7b6bd-170">Właściwość</span><span class="sxs-lookup"><span data-stu-id="7b6bd-170">Property</span></span> | <span data-ttu-id="7b6bd-171">Opis</span><span class="sxs-lookup"><span data-stu-id="7b6bd-171">Description</span></span> | <span data-ttu-id="7b6bd-172">Wymagane</span><span class="sxs-lookup"><span data-stu-id="7b6bd-172">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7b6bd-173">przestrzeni kluczy</span><span class="sxs-lookup"><span data-stu-id="7b6bd-173">keyspace</span></span> |<span data-ttu-id="7b6bd-174">Nazwa schematu bazy danych Cassandra lub przestrzeni kluczy.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-174">Name of the keyspace or schema in Cassandra database.</span></span> |<span data-ttu-id="7b6bd-175">Tak (Jeśli **zapytania** dla **CassandraSource** nie jest zdefiniowana).</span><span class="sxs-lookup"><span data-stu-id="7b6bd-175">Yes (If **query** for **CassandraSource** is not defined).</span></span> |
| <span data-ttu-id="7b6bd-176">tableName</span><span class="sxs-lookup"><span data-stu-id="7b6bd-176">tableName</span></span> |<span data-ttu-id="7b6bd-177">Nazwa tabeli w bazie danych Cassandra.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-177">Name of the table in Cassandra database.</span></span> |<span data-ttu-id="7b6bd-178">Tak (Jeśli **zapytania** dla **CassandraSource** nie jest zdefiniowana).</span><span class="sxs-lookup"><span data-stu-id="7b6bd-178">Yes (If **query** for **CassandraSource** is not defined).</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="7b6bd-179">Właściwości działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="7b6bd-179">Copy activity properties</span></span>
<span data-ttu-id="7b6bd-180">Pełną listę sekcje & właściwości dostępne do definiowania działań, zobacz [tworzenie potoków](data-factory-create-pipelines.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-180">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="7b6bd-181">Właściwości, takie jak nazwa, opis, dane wejściowe i wyjściowe tabel i zasady są dostępne dla wszystkich typów działań.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-181">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="7b6bd-182">Właściwości, które są dostępne w sekcji typeProperties działania różnić się z każdym typem działania.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-182">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="7b6bd-183">Dla działania kopiowania różnią się w zależności od typów źródeł i sink.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-183">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="7b6bd-184">Jeśli źródło jest typu **CassandraSource**, w sekcji typeProperties dostępne są następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="7b6bd-184">When source is of type **CassandraSource**, the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="7b6bd-185">Właściwość</span><span class="sxs-lookup"><span data-stu-id="7b6bd-185">Property</span></span> | <span data-ttu-id="7b6bd-186">Opis</span><span class="sxs-lookup"><span data-stu-id="7b6bd-186">Description</span></span> | <span data-ttu-id="7b6bd-187">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="7b6bd-187">Allowed values</span></span> | <span data-ttu-id="7b6bd-188">Wymagane</span><span class="sxs-lookup"><span data-stu-id="7b6bd-188">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="7b6bd-189">query</span><span class="sxs-lookup"><span data-stu-id="7b6bd-189">query</span></span> |<span data-ttu-id="7b6bd-190">Użyj niestandardowych zapytania można odczytać danych.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-190">Use the custom query to read data.</span></span> |<span data-ttu-id="7b6bd-191">Zapytania SQL 92 lub CQL zapytania.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-191">SQL-92 query or CQL query.</span></span> <span data-ttu-id="7b6bd-192">Zobacz [odwołania CQL](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html).</span><span class="sxs-lookup"><span data-stu-id="7b6bd-192">See [CQL reference](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html).</span></span> <br/><br/><span data-ttu-id="7b6bd-193">Korzystając z zapytania SQL, określ **przestrzeni kluczy name.table nazwy** do reprezentowania tabeli ma dotyczyć zapytanie.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-193">When using SQL query, specify **keyspace name.table name** to represent the table you want to query.</span></span> |<span data-ttu-id="7b6bd-194">Nie (jeśli są zdefiniowane tableName oraz przestrzeni kluczy w zestawie danych).</span><span class="sxs-lookup"><span data-stu-id="7b6bd-194">No (if tableName and keyspace on dataset are defined).</span></span> |
| <span data-ttu-id="7b6bd-195">consistencyLevel</span><span class="sxs-lookup"><span data-stu-id="7b6bd-195">consistencyLevel</span></span> |<span data-ttu-id="7b6bd-196">Poziom spójności Określa, jak wiele replik musi odpowiedzieć na żądanie odczytu przed zwróceniem danych do aplikacji klienckiej.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-196">The consistency level specifies how many replicas must respond to a read request before returning data to the client application.</span></span> <span data-ttu-id="7b6bd-197">Cassandra sprawdza określonej liczby replik danych do spełnienia żądania odczytu.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-197">Cassandra checks the specified number of replicas for data to satisfy the read request.</span></span> |<span data-ttu-id="7b6bd-198">JEDNĄ, DWIE, TRZY, KWORUM, WSZYSTKIE, LOCAL_QUORUM EACH_QUORUM, LOCAL_ONE.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-198">ONE, TWO, THREE, QUORUM, ALL, LOCAL_QUORUM, EACH_QUORUM, LOCAL_ONE.</span></span> <span data-ttu-id="7b6bd-199">Zobacz [Konfigurowanie spójność danych](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-199">See [Configuring data consistency](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) for details.</span></span> |<span data-ttu-id="7b6bd-200">Nie.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-200">No.</span></span> <span data-ttu-id="7b6bd-201">Domyślna wartość to jeden.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-201">Default value is ONE.</span></span> |

## <a name="json-example-copy-data-from-cassandra-to-azure-blob"></a><span data-ttu-id="7b6bd-202">Przykład JSON: kopiowanie danych z Cassandra do obiektów Blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="7b6bd-202">JSON example: Copy data from Cassandra to Azure Blob</span></span>
<span data-ttu-id="7b6bd-203">W poniższym przykładzie przedstawiono przykładowe definicje JSON, które można użyć, aby utworzyć potok przy użyciu [portalu Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) lub [programu Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) lub [programu Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="7b6bd-203">This example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="7b6bd-204">Widoczny jest sposób kopiowania danych z lokalną bazą danych Cassandra do magazynu obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-204">It shows how to copy data from an on-premises Cassandra database to an Azure Blob Storage.</span></span> <span data-ttu-id="7b6bd-205">Jednak można skopiować danych do dowolnego wychwytywanie podane [tutaj](data-factory-data-movement-activities.md#supported-data-stores-and-formats) za pomocą działania kopiowania w fabryce danych Azure.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-205">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7b6bd-206">W tym przykładzie przedstawiono fragmenty kodu JSON.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-206">This sample provides JSON snippets.</span></span> <span data-ttu-id="7b6bd-207">Zawiera instrukcje krok po kroku dotyczące tworzenia fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-207">It does not include step-by-step instructions for creating the data factory.</span></span> <span data-ttu-id="7b6bd-208">Zobacz [przenoszenie danych między lokalizacji lokalnej i w chmurze](data-factory-move-data-between-onprem-and-cloud.md) artykułu, aby uzyskać instrukcje krok po kroku.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-208">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="7b6bd-209">Przykład zawiera następujące obiekty fabryki danych:</span><span class="sxs-lookup"><span data-stu-id="7b6bd-209">The sample has the following data factory entities:</span></span>

* <span data-ttu-id="7b6bd-210">Połączonej usługi typu [OnPremisesCassandra](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="7b6bd-210">A linked service of type [OnPremisesCassandra](#linked-service-properties).</span></span>
* <span data-ttu-id="7b6bd-211">Połączonej usługi typu [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="7b6bd-211">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="7b6bd-212">Dane wejściowe [dataset](data-factory-create-datasets.md) typu [CassandraTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="7b6bd-212">An input [dataset](data-factory-create-datasets.md) of type [CassandraTable](#dataset-properties).</span></span>
* <span data-ttu-id="7b6bd-213">Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="7b6bd-213">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="7b6bd-214">A [potoku](data-factory-create-pipelines.md) z działaniem kopii, która używa [CassandraSource](#copy-activity-properties) i [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="7b6bd-214">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [CassandraSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="7b6bd-215">**Cassandra połączonej usługi:**</span><span class="sxs-lookup"><span data-stu-id="7b6bd-215">**Cassandra linked service:**</span></span>

<span data-ttu-id="7b6bd-216">W tym przykładzie użyto **Cassandra** połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-216">This example uses the **Cassandra** linked service.</span></span> <span data-ttu-id="7b6bd-217">Zobacz [Cassandra połączona usługa](#linked-service-properties) sekcji właściwości obsługiwanych przez tej połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-217">See [Cassandra linked service](#linked-service-properties) section for the properties supported by this linked service.</span></span>  

```json
{
    "name": "CassandraLinkedService",
    "properties":
    {
        "type": "OnPremisesCassandra",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "host": "mycassandraserver",
            "port": 9042,
            "username": "user",
            "password": "password",
            "gatewayName": "mygateway"
        }
    }
}
```

<span data-ttu-id="7b6bd-218">**Połączonej usługi magazynu Azure:**</span><span class="sxs-lookup"><span data-stu-id="7b6bd-218">**Azure Storage linked service:**</span></span>

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

<span data-ttu-id="7b6bd-219">**Zestaw danych wejściowych Cassandra:**</span><span class="sxs-lookup"><span data-stu-id="7b6bd-219">**Cassandra input dataset:**</span></span>

```json
{
    "name": "CassandraInput",
    "properties": {
        "linkedServiceName": "CassandraLinkedService",
        "type": "CassandraTable",
        "typeProperties": {
            "tableName": "mytable",
            "keySpace": "mykeyspace"
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

<span data-ttu-id="7b6bd-220">Ustawienie **zewnętrznych** do **true** usługi fabryka danych informuje, czy zestaw danych jest zewnętrzne do fabryki danych i nie jest generowany przez działanie w fabryce danych.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-220">Setting **external** to **true** informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

<span data-ttu-id="7b6bd-221">**Azure Blob wyjściowy zestaw danych:**</span><span class="sxs-lookup"><span data-stu-id="7b6bd-221">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="7b6bd-222">Dane są zapisywane do nowego obiektu blob co godzinę (częstotliwość: godziny, interwał: 1).</span><span class="sxs-lookup"><span data-stu-id="7b6bd-222">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span>

```json
{
    "name": "AzureBlobOutput",
    "properties":
    {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties":
        {
            "folderPath": "adfgetstarted/fromcassandra"
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="7b6bd-223">**Aktywność kopiowania w potoku z Cassandra źródłowy i odbiorczy obiektów Blob:**</span><span class="sxs-lookup"><span data-stu-id="7b6bd-223">**Copy activity in a pipeline with Cassandra source and Blob sink:**</span></span>

<span data-ttu-id="7b6bd-224">Potok zawiera działanie kopiowania, który jest skonfigurowany do używania wejściowe i wyjściowe zestawy danych i jest zaplanowane co godzinę.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-224">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="7b6bd-225">W definicji JSON potoku **źródła** ustawiono typ **CassandraSource** i **zbiornika** ustawiono typ **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-225">In the pipeline JSON definition, the **source** type is set to **CassandraSource** and **sink** type is set to **BlobSink**.</span></span>

<span data-ttu-id="7b6bd-226">Zobacz [właściwości typu RelationalSource](#copy-activity-properties) listę obsługiwanych przez RelationalSource właściwości.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-226">See [RelationalSource type properties](#copy-activity-properties) for the list of properties supported by the RelationalSource.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2016-06-01T18:00:00",
        "end":"2016-06-01T19:00:00",
        "description":"pipeline with copy activity",
        "activities":[  
        {
            "name": "CassandraToAzureBlob",
            "description": "Copy from Cassandra to an Azure blob",
            "type": "Copy",
            "inputs": [
            {
                "name": "CassandraInput"
            }
            ],
            "outputs": [
            {
                "name": "AzureBlobOutput"
            }
            ],
            "typeProperties": {
                "source": {
                    "type": "CassandraSource",
                    "query": "select id, firstname, lastname from mykeyspace.mytable"

                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }
        ]    
    }
}
```

### <a name="type-mapping-for-cassandra"></a><span data-ttu-id="7b6bd-227">Mapowanie typu dla Cassandra</span><span class="sxs-lookup"><span data-stu-id="7b6bd-227">Type mapping for Cassandra</span></span>
| <span data-ttu-id="7b6bd-228">Typ Cassandra</span><span class="sxs-lookup"><span data-stu-id="7b6bd-228">Cassandra Type</span></span> | <span data-ttu-id="7b6bd-229">Typ na podstawie .net</span><span class="sxs-lookup"><span data-stu-id="7b6bd-229">.Net Based Type</span></span> |
| --- | --- |
| <span data-ttu-id="7b6bd-230">ASCII</span><span class="sxs-lookup"><span data-stu-id="7b6bd-230">ASCII</span></span> |<span data-ttu-id="7b6bd-231">Ciąg</span><span class="sxs-lookup"><span data-stu-id="7b6bd-231">String</span></span> |
| <span data-ttu-id="7b6bd-232">BIGINT</span><span class="sxs-lookup"><span data-stu-id="7b6bd-232">BIGINT</span></span> |<span data-ttu-id="7b6bd-233">Int64</span><span class="sxs-lookup"><span data-stu-id="7b6bd-233">Int64</span></span> |
| <span data-ttu-id="7b6bd-234">OBIEKT BLOB</span><span class="sxs-lookup"><span data-stu-id="7b6bd-234">BLOB</span></span> |<span data-ttu-id="7b6bd-235">Byte]</span><span class="sxs-lookup"><span data-stu-id="7b6bd-235">Byte[]</span></span> |
| <span data-ttu-id="7b6bd-236">WARTOŚĆ LOGICZNA</span><span class="sxs-lookup"><span data-stu-id="7b6bd-236">BOOLEAN</span></span> |<span data-ttu-id="7b6bd-237">Wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="7b6bd-237">Boolean</span></span> |
| <span data-ttu-id="7b6bd-238">DECIMAL</span><span class="sxs-lookup"><span data-stu-id="7b6bd-238">DECIMAL</span></span> |<span data-ttu-id="7b6bd-239">Decimal</span><span class="sxs-lookup"><span data-stu-id="7b6bd-239">Decimal</span></span> |
| <span data-ttu-id="7b6bd-240">O PODWÓJNEJ PRECYZJI</span><span class="sxs-lookup"><span data-stu-id="7b6bd-240">DOUBLE</span></span> |<span data-ttu-id="7b6bd-241">O podwójnej precyzji</span><span class="sxs-lookup"><span data-stu-id="7b6bd-241">Double</span></span> |
| <span data-ttu-id="7b6bd-242">FLOAT</span><span class="sxs-lookup"><span data-stu-id="7b6bd-242">FLOAT</span></span> |<span data-ttu-id="7b6bd-243">Pojedynczy</span><span class="sxs-lookup"><span data-stu-id="7b6bd-243">Single</span></span> |
| <span data-ttu-id="7b6bd-244">INET</span><span class="sxs-lookup"><span data-stu-id="7b6bd-244">INET</span></span> |<span data-ttu-id="7b6bd-245">Ciąg</span><span class="sxs-lookup"><span data-stu-id="7b6bd-245">String</span></span> |
| <span data-ttu-id="7b6bd-246">INT</span><span class="sxs-lookup"><span data-stu-id="7b6bd-246">INT</span></span> |<span data-ttu-id="7b6bd-247">Int32</span><span class="sxs-lookup"><span data-stu-id="7b6bd-247">Int32</span></span> |
| <span data-ttu-id="7b6bd-248">TEKST</span><span class="sxs-lookup"><span data-stu-id="7b6bd-248">TEXT</span></span> |<span data-ttu-id="7b6bd-249">Ciąg</span><span class="sxs-lookup"><span data-stu-id="7b6bd-249">String</span></span> |
| <span data-ttu-id="7b6bd-250">ZNACZNIK CZASU</span><span class="sxs-lookup"><span data-stu-id="7b6bd-250">TIMESTAMP</span></span> |<span data-ttu-id="7b6bd-251">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="7b6bd-251">DateTime</span></span> |
| <span data-ttu-id="7b6bd-252">TIMEUUID</span><span class="sxs-lookup"><span data-stu-id="7b6bd-252">TIMEUUID</span></span> |<span data-ttu-id="7b6bd-253">Identyfikator GUID</span><span class="sxs-lookup"><span data-stu-id="7b6bd-253">Guid</span></span> |
| <span data-ttu-id="7b6bd-254">IDENTYFIKATOR UUID</span><span class="sxs-lookup"><span data-stu-id="7b6bd-254">UUID</span></span> |<span data-ttu-id="7b6bd-255">Identyfikator GUID</span><span class="sxs-lookup"><span data-stu-id="7b6bd-255">Guid</span></span> |
| <span data-ttu-id="7b6bd-256">VARCHAR</span><span class="sxs-lookup"><span data-stu-id="7b6bd-256">VARCHAR</span></span> |<span data-ttu-id="7b6bd-257">Ciąg</span><span class="sxs-lookup"><span data-stu-id="7b6bd-257">String</span></span> |
| <span data-ttu-id="7b6bd-258">VARINT</span><span class="sxs-lookup"><span data-stu-id="7b6bd-258">VARINT</span></span> |<span data-ttu-id="7b6bd-259">Decimal</span><span class="sxs-lookup"><span data-stu-id="7b6bd-259">Decimal</span></span> |

> [!NOTE]
> <span data-ttu-id="7b6bd-260">Kolekcja typów (mapy, zestaw, listy itp.), można znaleźć w [współpracy z typami kolekcji Cassandra za pomocą tabeli wirtualnej](#work-with-collections-using-virtual-table) sekcji.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-260">For collection types (map, set, list, etc.), refer to [Work with Cassandra collection types using virtual table](#work-with-collections-using-virtual-table) section.</span></span>
>
> <span data-ttu-id="7b6bd-261">Typy definiowane przez użytkownika nie są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-261">User-defined types are not supported.</span></span>
>
> <span data-ttu-id="7b6bd-262">Długość kolumny typu Binary i kolumny typu String długości nie może być większa niż 4000.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-262">The length of Binary Column and String Column lengths cannot be greater than 4000.</span></span>
>
>

## <a name="work-with-collections-using-virtual-table"></a><span data-ttu-id="7b6bd-263">Praca z kolekcji za pomocą tabeli wirtualnej</span><span class="sxs-lookup"><span data-stu-id="7b6bd-263">Work with collections using virtual table</span></span>
<span data-ttu-id="7b6bd-264">Fabryka danych Azure używa wbudowanego sterownika ODBC do nawiązania połączenia, a następnie skopiować dane z bazy danych Cassandra.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-264">Azure Data Factory uses a built-in ODBC driver to connect to and copy data from your Cassandra database.</span></span> <span data-ttu-id="7b6bd-265">Dla typów kolekcji, w tym mapy, zestaw i listy sterownik renormalizes dane w odpowiadających jej tabel wirtualnego.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-265">For collection types including map, set and list, the driver renormalizes the data into corresponding virtual tables.</span></span> <span data-ttu-id="7b6bd-266">W szczególności jeśli tabela zawiera wszystkie kolumny w kolekcji, sterownik generuje następujące tabele wirtualne:</span><span class="sxs-lookup"><span data-stu-id="7b6bd-266">Specifically, if a table contains any collection columns, the driver generates the following virtual tables:</span></span>

* <span data-ttu-id="7b6bd-267">A **tabeli podstawowej**, który zawiera te same dane jako prawdziwe tabeli z wyjątkiem kolumny kolekcji.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-267">A **base table**, which contains the same data as the real table except for the collection columns.</span></span> <span data-ttu-id="7b6bd-268">Tabela podstawowa używa tej samej nazwie jako prawdziwe tabeli, która reprezentuje.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-268">The base table uses the same name as the real table that it represents.</span></span>
* <span data-ttu-id="7b6bd-269">A **tabeli wirtualnej** dla każdej kolekcji kolumny, która rozszerza zagnieżdżone dane.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-269">A **virtual table** for each collection column, which expands the nested data.</span></span> <span data-ttu-id="7b6bd-270">Wirtualny tabel, które reprezentują kolekcje są nazywane przy użyciu nazwy tabeli rzeczywistych separator "*vt*" i nazwę kolumny.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-270">The virtual tables that represent collections are named using the name of the real table, a separator “*vt*” and the name of the column.</span></span>

<span data-ttu-id="7b6bd-271">Tabele wirtualne odwołują się do danych w tabeli prawdziwe, włączanie dostępu do danych nieznormalizowany sterownika.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-271">Virtual tables refer to the data in the real table, enabling the driver to access the denormalized data.</span></span> <span data-ttu-id="7b6bd-272">Zobacz sekcję przykład, aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-272">See Example section for details.</span></span> <span data-ttu-id="7b6bd-273">Ma dostęp do zawartości Cassandra kolekcji, zapytań i przyłączanie tabel wirtualnego.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-273">You can access the content of Cassandra collections by querying and joining the virtual tables.</span></span>

<span data-ttu-id="7b6bd-274">Można użyć [kreatora kopiowania](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity) intuicyjnie wyświetlić listę tabel w bazie danych Cassandra tym tabele wirtualne i przeglądać dane wewnątrz.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-274">You can use the [Copy Wizard](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity) to intuitively view the list of tables in Cassandra database including the virtual tables, and preview the data inside.</span></span> <span data-ttu-id="7b6bd-275">Można również utworzyć zapytanie w kreatorze kopiowania i weryfikacji, aby zobaczyć wynik.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-275">You can also construct a query in the Copy Wizard and validate to see the result.</span></span>

### <a name="example"></a><span data-ttu-id="7b6bd-276">Przykład</span><span class="sxs-lookup"><span data-stu-id="7b6bd-276">Example</span></span>
<span data-ttu-id="7b6bd-277">Na przykład następujące "ExampleTable" jest Cassandra tabeli bazy danych, która zawiera całkowitą kolumna klucza podstawowego o nazwie "pk_int", kolumna tekst o nazwie wartość kolumny listy, kolumny mapy i zestawu kolumn (o nazwie "StringSet").</span><span class="sxs-lookup"><span data-stu-id="7b6bd-277">For example, the following “ExampleTable” is a Cassandra database table that contains an integer primary key column named “pk_int”, a text column named value, a list column, a map column, and a set column (named “StringSet”).</span></span>

| <span data-ttu-id="7b6bd-278">pk_int</span><span class="sxs-lookup"><span data-stu-id="7b6bd-278">pk_int</span></span> | <span data-ttu-id="7b6bd-279">Wartość</span><span class="sxs-lookup"><span data-stu-id="7b6bd-279">Value</span></span> | <span data-ttu-id="7b6bd-280">List</span><span class="sxs-lookup"><span data-stu-id="7b6bd-280">List</span></span> | <span data-ttu-id="7b6bd-281">mapy</span><span class="sxs-lookup"><span data-stu-id="7b6bd-281">Map</span></span> | <span data-ttu-id="7b6bd-282">StringSet</span><span class="sxs-lookup"><span data-stu-id="7b6bd-282">StringSet</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="7b6bd-283">1</span><span class="sxs-lookup"><span data-stu-id="7b6bd-283">1</span></span> |<span data-ttu-id="7b6bd-284">"Przykładowa wartość 1"</span><span class="sxs-lookup"><span data-stu-id="7b6bd-284">"sample value 1"</span></span> |<span data-ttu-id="7b6bd-285">["1", "2", "3"]</span><span class="sxs-lookup"><span data-stu-id="7b6bd-285">["1", "2", "3"]</span></span> |<span data-ttu-id="7b6bd-286">{"S1": "", "S2": "b"}</span><span class="sxs-lookup"><span data-stu-id="7b6bd-286">{"S1": "a", "S2": "b"}</span></span> |<span data-ttu-id="7b6bd-287">{"", "B", "C"}</span><span class="sxs-lookup"><span data-stu-id="7b6bd-287">{"A", "B", "C"}</span></span> |
| <span data-ttu-id="7b6bd-288">3</span><span class="sxs-lookup"><span data-stu-id="7b6bd-288">3</span></span> |<span data-ttu-id="7b6bd-289">"przykład value 3"</span><span class="sxs-lookup"><span data-stu-id="7b6bd-289">"sample value 3"</span></span> |<span data-ttu-id="7b6bd-290">["100", "101", "102", "105"]</span><span class="sxs-lookup"><span data-stu-id="7b6bd-290">["100", "101", "102", "105"]</span></span> |<span data-ttu-id="7b6bd-291">{"S1": "t"}</span><span class="sxs-lookup"><span data-stu-id="7b6bd-291">{"S1": "t"}</span></span> |<span data-ttu-id="7b6bd-292">{"", "E"}</span><span class="sxs-lookup"><span data-stu-id="7b6bd-292">{"A", "E"}</span></span> |

<span data-ttu-id="7b6bd-293">Sterownik przetwarzający generuje wiele tabel wirtualnego do reprezentowania tej pojedynczej tabeli.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-293">The driver would generate multiple virtual tables to represent this single table.</span></span> <span data-ttu-id="7b6bd-294">Kolumny klucza obcego w tabeli wirtualnej odwołania kolumn klucza podstawowego w tabeli rzeczywistych i wskazać, który odpowiada wiersz tabeli wirtualnej wiersz tabeli prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-294">The foreign key columns in the virtual tables reference the primary key columns in the real table, and indicate which real table row the virtual table row corresponds to.</span></span>

<span data-ttu-id="7b6bd-295">Pierwsza tabela wirtualnego jest tabeli podstawowej o nazwie "ExampleTable" przedstawiono w poniższej tabeli.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-295">The first virtual table is the base table named “ExampleTable” is shown in the following table.</span></span> <span data-ttu-id="7b6bd-296">Podstawowa tabela zawiera te same dane jako oryginalnej tabeli bazy danych, z wyjątkiem kolekcje, które są pominięte w tej tabeli i rozwinięty w innych tabelach wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-296">The base table contains the same data as the original database table except for the collections, which are omitted from this table and expanded in other virtual tables.</span></span>

| <span data-ttu-id="7b6bd-297">pk_int</span><span class="sxs-lookup"><span data-stu-id="7b6bd-297">pk_int</span></span> | <span data-ttu-id="7b6bd-298">Wartość</span><span class="sxs-lookup"><span data-stu-id="7b6bd-298">Value</span></span> |
| --- | --- |
| <span data-ttu-id="7b6bd-299">1</span><span class="sxs-lookup"><span data-stu-id="7b6bd-299">1</span></span> |<span data-ttu-id="7b6bd-300">"Przykładowa wartość 1"</span><span class="sxs-lookup"><span data-stu-id="7b6bd-300">"sample value 1"</span></span> |
| <span data-ttu-id="7b6bd-301">3</span><span class="sxs-lookup"><span data-stu-id="7b6bd-301">3</span></span> |<span data-ttu-id="7b6bd-302">"przykład value 3"</span><span class="sxs-lookup"><span data-stu-id="7b6bd-302">"sample value 3"</span></span> |

<span data-ttu-id="7b6bd-303">W poniższych tabelach przedstawiono wirtualnego tabel, które renormalize danych z listy, mapy i StringSet kolumn.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-303">The following tables show the virtual tables that renormalize the data from the List, Map, and StringSet columns.</span></span> <span data-ttu-id="7b6bd-304">Kolumny o nazwach kończyć "_index" lub "_klucza" wskazać pozycję danych w oryginalnej listy lub mapy.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-304">The columns with names that end with “_index” or “_key” indicate the position of the data within the original list or map.</span></span> <span data-ttu-id="7b6bd-305">Kolumny o nazwach kończących się znakiem "_value" zawierają rozszerzonych danych z kolekcji.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-305">The columns with names that end with “_value” contain the expanded data from the collection.</span></span>

#### <a name="table-exampletablevtlist"></a><span data-ttu-id="7b6bd-306">Tabela "ExampleTable_vt_List":</span><span class="sxs-lookup"><span data-stu-id="7b6bd-306">Table “ExampleTable_vt_List”:</span></span>
| <span data-ttu-id="7b6bd-307">pk_int</span><span class="sxs-lookup"><span data-stu-id="7b6bd-307">pk_int</span></span> | <span data-ttu-id="7b6bd-308">List_index</span><span class="sxs-lookup"><span data-stu-id="7b6bd-308">List_index</span></span> | <span data-ttu-id="7b6bd-309">List_value</span><span class="sxs-lookup"><span data-stu-id="7b6bd-309">List_value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7b6bd-310">1</span><span class="sxs-lookup"><span data-stu-id="7b6bd-310">1</span></span> |<span data-ttu-id="7b6bd-311">0</span><span class="sxs-lookup"><span data-stu-id="7b6bd-311">0</span></span> |<span data-ttu-id="7b6bd-312">1</span><span class="sxs-lookup"><span data-stu-id="7b6bd-312">1</span></span> |
| <span data-ttu-id="7b6bd-313">1</span><span class="sxs-lookup"><span data-stu-id="7b6bd-313">1</span></span> |<span data-ttu-id="7b6bd-314">1</span><span class="sxs-lookup"><span data-stu-id="7b6bd-314">1</span></span> |<span data-ttu-id="7b6bd-315">2</span><span class="sxs-lookup"><span data-stu-id="7b6bd-315">2</span></span> |
| <span data-ttu-id="7b6bd-316">1</span><span class="sxs-lookup"><span data-stu-id="7b6bd-316">1</span></span> |<span data-ttu-id="7b6bd-317">2</span><span class="sxs-lookup"><span data-stu-id="7b6bd-317">2</span></span> |<span data-ttu-id="7b6bd-318">3</span><span class="sxs-lookup"><span data-stu-id="7b6bd-318">3</span></span> |
| <span data-ttu-id="7b6bd-319">3</span><span class="sxs-lookup"><span data-stu-id="7b6bd-319">3</span></span> |<span data-ttu-id="7b6bd-320">0</span><span class="sxs-lookup"><span data-stu-id="7b6bd-320">0</span></span> |<span data-ttu-id="7b6bd-321">100</span><span class="sxs-lookup"><span data-stu-id="7b6bd-321">100</span></span> |
| <span data-ttu-id="7b6bd-322">3</span><span class="sxs-lookup"><span data-stu-id="7b6bd-322">3</span></span> |<span data-ttu-id="7b6bd-323">1</span><span class="sxs-lookup"><span data-stu-id="7b6bd-323">1</span></span> |<span data-ttu-id="7b6bd-324">101</span><span class="sxs-lookup"><span data-stu-id="7b6bd-324">101</span></span> |
| <span data-ttu-id="7b6bd-325">3</span><span class="sxs-lookup"><span data-stu-id="7b6bd-325">3</span></span> |<span data-ttu-id="7b6bd-326">2</span><span class="sxs-lookup"><span data-stu-id="7b6bd-326">2</span></span> |<span data-ttu-id="7b6bd-327">102</span><span class="sxs-lookup"><span data-stu-id="7b6bd-327">102</span></span> |
| <span data-ttu-id="7b6bd-328">3</span><span class="sxs-lookup"><span data-stu-id="7b6bd-328">3</span></span> |<span data-ttu-id="7b6bd-329">3</span><span class="sxs-lookup"><span data-stu-id="7b6bd-329">3</span></span> |<span data-ttu-id="7b6bd-330">103</span><span class="sxs-lookup"><span data-stu-id="7b6bd-330">103</span></span> |

#### <a name="table-exampletablevtmap"></a><span data-ttu-id="7b6bd-331">Tabela "ExampleTable_vt_Map":</span><span class="sxs-lookup"><span data-stu-id="7b6bd-331">Table “ExampleTable_vt_Map”:</span></span>
| <span data-ttu-id="7b6bd-332">pk_int</span><span class="sxs-lookup"><span data-stu-id="7b6bd-332">pk_int</span></span> | <span data-ttu-id="7b6bd-333">Map_key</span><span class="sxs-lookup"><span data-stu-id="7b6bd-333">Map_key</span></span> | <span data-ttu-id="7b6bd-334">Map_value</span><span class="sxs-lookup"><span data-stu-id="7b6bd-334">Map_value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7b6bd-335">1</span><span class="sxs-lookup"><span data-stu-id="7b6bd-335">1</span></span> |<span data-ttu-id="7b6bd-336">S1</span><span class="sxs-lookup"><span data-stu-id="7b6bd-336">S1</span></span> |<span data-ttu-id="7b6bd-337">A</span><span class="sxs-lookup"><span data-stu-id="7b6bd-337">A</span></span> |
| <span data-ttu-id="7b6bd-338">1</span><span class="sxs-lookup"><span data-stu-id="7b6bd-338">1</span></span> |<span data-ttu-id="7b6bd-339">S2</span><span class="sxs-lookup"><span data-stu-id="7b6bd-339">S2</span></span> |<span data-ttu-id="7b6bd-340">B</span><span class="sxs-lookup"><span data-stu-id="7b6bd-340">b</span></span> |
| <span data-ttu-id="7b6bd-341">3</span><span class="sxs-lookup"><span data-stu-id="7b6bd-341">3</span></span> |<span data-ttu-id="7b6bd-342">S1</span><span class="sxs-lookup"><span data-stu-id="7b6bd-342">S1</span></span> |<span data-ttu-id="7b6bd-343">T</span><span class="sxs-lookup"><span data-stu-id="7b6bd-343">t</span></span> |

#### <a name="table-exampletablevtstringset"></a><span data-ttu-id="7b6bd-344">Tabela "ExampleTable_vt_StringSet":</span><span class="sxs-lookup"><span data-stu-id="7b6bd-344">Table “ExampleTable_vt_StringSet”:</span></span>
| <span data-ttu-id="7b6bd-345">pk_int</span><span class="sxs-lookup"><span data-stu-id="7b6bd-345">pk_int</span></span> | <span data-ttu-id="7b6bd-346">StringSet_value</span><span class="sxs-lookup"><span data-stu-id="7b6bd-346">StringSet_value</span></span> |
| --- | --- |
| <span data-ttu-id="7b6bd-347">1</span><span class="sxs-lookup"><span data-stu-id="7b6bd-347">1</span></span> |<span data-ttu-id="7b6bd-348">A</span><span class="sxs-lookup"><span data-stu-id="7b6bd-348">A</span></span> |
| <span data-ttu-id="7b6bd-349">1</span><span class="sxs-lookup"><span data-stu-id="7b6bd-349">1</span></span> |<span data-ttu-id="7b6bd-350">B</span><span class="sxs-lookup"><span data-stu-id="7b6bd-350">B</span></span> |
| <span data-ttu-id="7b6bd-351">1</span><span class="sxs-lookup"><span data-stu-id="7b6bd-351">1</span></span> |<span data-ttu-id="7b6bd-352">C</span><span class="sxs-lookup"><span data-stu-id="7b6bd-352">C</span></span> |
| <span data-ttu-id="7b6bd-353">3</span><span class="sxs-lookup"><span data-stu-id="7b6bd-353">3</span></span> |<span data-ttu-id="7b6bd-354">A</span><span class="sxs-lookup"><span data-stu-id="7b6bd-354">A</span></span> |
| <span data-ttu-id="7b6bd-355">3</span><span class="sxs-lookup"><span data-stu-id="7b6bd-355">3</span></span> |<span data-ttu-id="7b6bd-356">E</span><span class="sxs-lookup"><span data-stu-id="7b6bd-356">E</span></span> |

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="7b6bd-357">Obiekt sink kolumn mapy źródła</span><span class="sxs-lookup"><span data-stu-id="7b6bd-357">Map source to sink columns</span></span>
<span data-ttu-id="7b6bd-358">Aby uzyskać informacje dotyczące mapowania kolumn w zestawie źródła danych do kolumn w zestawie danych zbiornika, zobacz [mapowania kolumnach dataset w fabryce danych Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="7b6bd-358">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="7b6bd-359">Odczyt powtarzalny ze źródłami relacyjnymi</span><span class="sxs-lookup"><span data-stu-id="7b6bd-359">Repeatable read from relational sources</span></span>
<span data-ttu-id="7b6bd-360">Podczas kopiowania danych z danych relacyjnych przechowuje, należy pamiętać, aby uniknąć niezamierzone wyniki powtarzalności.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-360">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="7b6bd-361">Fabryka danych Azure możesz ponownie ręcznie wycinek.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-361">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="7b6bd-362">Można również skonfigurować zasady ponawiania dla zestawu danych, aby wycinek jest uruchamiany ponownie, gdy wystąpi błąd.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-362">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="7b6bd-363">Podczas wycinek zostanie uruchomiona ponownie w obu przypadkach, należy się upewnić, że te same dane jest do odczytu niezależnie od tego, ile razy wycinek jest uruchamiany.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-363">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="7b6bd-364">Zobacz [Repeatable odczytywać źródłami relacyjnymi](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="7b6bd-364">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="7b6bd-365">Wydajność i dostrajania</span><span class="sxs-lookup"><span data-stu-id="7b6bd-365">Performance and Tuning</span></span>
<span data-ttu-id="7b6bd-366">Zobacz [wydajności działania kopiowania & dostrajanie przewodnik](data-factory-copy-activity-performance.md) Aby dowiedzieć się więcej o kluczowych czynników tego wydajność wpływ przenoszenia danych (działanie kopiowania) w usłudze fabryka danych Azure i zoptymalizować ją na różne sposoby.</span><span class="sxs-lookup"><span data-stu-id="7b6bd-366">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
